include_directories(../include)

add_executable(
	bssl

	args.cc
	client.cc
	server.cc
	const.cc
	pkcs12.cc
	speed.cc
	tool.cc
	transport_common.cc
)

set_executable_props(bssl)

if (APPLE OR WIN32)
	target_link_libraries(bssl ssl crypto)
else()
	target_link_libraries(bssl ssl crypto -lrt)
endif()
