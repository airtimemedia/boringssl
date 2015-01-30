include_directories(. .. ../../include)

add_library(
	ecdsa

	OBJECT

	ecdsa.c
	ecdsa_asn1.c
	ecdsa_error.c
)


add_executable(
	ecdsa_test

	ecdsa_test.c
)

set_executable_props(ecdsa_test)

target_link_libraries(ecdsa_test crypto)
