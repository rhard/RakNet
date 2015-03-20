project(PostgreSQLInterface)
IF (NOT WIN32 AND UNIX)
	FILE(GLOB ALL_HEADER_SRCS *.h)
	FILE(GLOB ALL_CPP_SRCS *.cpp)
	FINDPOSTGRE()
	include_directories(./ ${RAKNETHEADERFILES} ${POSTGRESQL_INCLUDE_DIR}) 
	add_library(LibPostgreSQLInterface STATIC ${ALL_CPP_SRCS} ${ALL_HEADER_SRCS})
	target_link_libraries (LibPostgreSQLInterface ${RAKNET_COMMON_LIBS} ${POSTGRESQL_LIBRARIES})
	VSUBFOLDER(LibPostgreSQLInterface "DependentExtensions")
ELSE(NOT WIN32 AND UNIX)
	FILE(GLOB ALL_HEADER_SRCS *.h)
	FILE(GLOB ALL_CPP_SRCS *.cpp)
	FINDPOSTGRE()
	include_directories(./ ${RAKNETHEADERFILES} ${POSTGRESQL_INCLUDE_DIR}) 
	add_library(LibPostgreSQLInterface STATIC ${ALL_CPP_SRCS} ${ALL_HEADER_SRCS})
	set_target_properties(LibPostgreSQLInterface PROPERTIES DEBUG_POSTFIX d)
	target_link_libraries (LibPostgreSQLInterface ${RAKNET_COMMON_LIBS} ${POSTGRESQL_LIBRARIES})
	VSUBFOLDER(LibPostgreSQLInterface "DependentExtensions")

	install (TARGETS LibPostgreSQLInterface
	RUNTIME DESTINATION bin
	LIBRARY DESTINATION lib${LIB_SUFFIX}
	ARCHIVE DESTINATION lib${LIB_SUFFIX}
	)
	
	install (FILES
	${ALL_HEADER_SRCS}
	DESTINATION include/postgresqlinterface
	)	
ENDIF(NOT WIN32 AND UNIX)

