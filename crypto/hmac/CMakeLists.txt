include_directories(. .. ../../include)

add_library(
	hmac

	OBJECT

	hmac.c
)

set_source_files_properties(
       hmac.c
       PROPERTIES COMPILE_FLAGS "-Wno-tautological-compare"
)

add_executable(
	hmac_test

	hmac_test.c
)

target_link_libraries(hmac_test crypto)
