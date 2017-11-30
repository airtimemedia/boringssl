add_subdirectory(bio)
add_subdirectory(blowfish)
add_subdirectory(cast)
add_subdirectory(des)
add_subdirectory(evp)
add_subdirectory(rsa)
add_subdirectory(xts)

add_library(
  decrepit

  # airtime: start
  # DEVOPS-1090: libdecrepit.a is not created by Xcode generator
  # unless it has a real source file (not just referencing TARGET_OBJECTS)
  # See https://gitlab.kitware.com/cmake/cmake/issues/16524
  airtime_dummy_file.c
  # airtime: end

  $<TARGET_OBJECTS:bio_decrepit>
  $<TARGET_OBJECTS:blowfish>
  $<TARGET_OBJECTS:cast>
  $<TARGET_OBJECTS:des_decrepit>
  $<TARGET_OBJECTS:evp_decrepit>
  $<TARGET_OBJECTS:rsa_decrepit>
  $<TARGET_OBJECTS:xts>
)

target_link_libraries(decrepit crypto)
