include_directories(. .. ../../include)

add_library(
	digest

	OBJECT

	digest.c
	digests.c
	digest_error.c
)

add_executable(
	digest_test

	digest_test.c
)

set_executable_props(digest_test)

target_link_libraries(digest_test crypto)
