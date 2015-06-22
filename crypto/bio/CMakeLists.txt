include_directories(. .. ../../include)

add_library(
  bio

  OBJECT

  bio.c
  bio_mem.c
  buffer.c
  connect.c
  fd.c
  file.c
  hexdump.c
  pair.c
  printf.c
  socket.c
  socket_helper.c
)

set_source_files_properties(
	pair.c
	PROPERTIES COMPILE_FLAGS "-Wno-tautological-compare"
)

add_executable(
  bio_test

  bio_test.cc
)

set_executable_props(bio_test)

target_link_libraries(bio_test crypto)
if (WIN32)
  target_link_libraries(bio_test ws2_32)
endif()
