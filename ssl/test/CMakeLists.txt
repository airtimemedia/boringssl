include_directories(../../include)

add_executable(
  bssl_shim

  async_bio.cc
  bssl_shim.cc
  packeted_bio.cc
  test_config.cc

  $<TARGET_OBJECTS:test_support>
)

set_executable_props(bssl_shim)

target_link_libraries(bssl_shim ssl crypto)
