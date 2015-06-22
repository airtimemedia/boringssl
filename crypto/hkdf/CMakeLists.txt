include_directories(. .. ../../include)

add_library(
  hkdf

  OBJECT

  hkdf.c
)

add_executable(
  hkdf_test

  hkdf_test.c
)

set_executable_props(hkdf_test)

target_link_libraries(hkdf_test crypto)
