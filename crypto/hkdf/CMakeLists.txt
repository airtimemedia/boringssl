include_directories(../../include)

add_library(
  hkdf

  OBJECT

  hkdf.c
)

add_executable(
  hkdf_test

  hkdf_test.c

  $<TARGET_OBJECTS:test_support>
)

set_executable_props(hkdf_test)
link_cplusplus(hkdf_test)

target_link_libraries(hkdf_test crypto)
add_dependencies(all_tests hkdf_test)
