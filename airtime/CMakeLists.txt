# Copyright Airtime Media 2014

# Allow reading location of libraries
cmake_policy(SET CMP0026 OLD)

set(at_boringssl_include_dir ${CMAKE_CURRENT_SOURCE_DIR}/../include CACHE INTERNAL "")

set(ORIG_CMAKE_SYSTEM_PROCESSOR ${CMAKE_SYSTEM_PROCESSOR})

if (${at_target_arch} MATCHES armv7)
  # boringssl configures itself based on CMAKE_SYSTEM_PROCESSOR
  set(CMAKE_SYSTEM_PROCESSOR "arm")
elseif (${at_target_arch} MATCHES arm64)
  set(CMAKE_SYSTEM_PROCESSOR "aarch64")
elseif (IOS)
  # NOTE(tom): this is a hack to handle the simulator case
  # it works because the setting the processor to arm only causes boringssl to
  # add architecture-specific assembly files, but we exclude those when building
  # for iOS since clang can't compile them. See
  # https://github.com/airtimemedia/boringssl/commit/19a96365f5ecb168cd0826cff89948335373a2e6
  set(CMAKE_SYSTEM_PROCESSOR "arm")
else()
  set(CMAKE_SYSTEM_PROCESSOR ${at_target_arch})
endif()

if (IOS OR ANDROID)
  set(BORINGSSL_NO_ASM YES)
  set(OPENSSL_NO_ASM YES)
endif()

if (IOS)
  set(BORINGSSL_DEVELOPMENT_TEAM "8TJ4VFPP54")
endif()

# Disable warnings introduced in Xcode 7.3
add_compile_options(-Wno-logical-not-parentheses -Wno-implicit-fallthrough)

add_subdirectory(.. ${CMAKE_CURRENT_BINARY_DIR}/boringssl)
set(CMAKE_SYSTEM_PROCESSOR ${ORIG_CMAKE_SYSTEM_PROCESSOR})

get_property(boringssl_ssl_lib TARGET ssl PROPERTY LOCATION)
get_filename_component(boringssl_ssl_dir ${boringssl_ssl_lib} DIRECTORY)
set(at_boringssl_ssl_dir ${boringssl_ssl_dir} CACHE INTERNAL "")

get_property(boringssl_crypto_lib TARGET crypto PROPERTY LOCATION)
get_filename_component(boringssl_crypto_dir ${boringssl_crypto_lib} DIRECTORY)
set(at_boringssl_crypto_dir ${boringssl_crypto_dir} CACHE INTERNAL "")

add_library(at_boringssl INTERFACE)
target_include_directories(at_boringssl INTERFACE ${at_boringssl_include_dir})
target_link_libraries(at_boringssl INTERFACE ssl crypto)
add_dependencies(at_boringssl ssl crypto)  # CAR-1049: Add explicit dependency

