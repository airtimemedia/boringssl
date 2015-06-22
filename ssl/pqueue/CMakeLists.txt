include_directories(../../include)

add_library(
  pqueue

  OBJECT

  pqueue.c
)

add_executable(
  pqueue_test

  pqueue_test.c
)

set_executable_props(pqueue_test)

target_link_libraries(pqueue_test ssl crypto)
