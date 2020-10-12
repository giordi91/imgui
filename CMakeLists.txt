cmake_minimum_required(VERSION 3.6.0)

project(imgui)   

    #looking for  files
    file(GLOB SOURCE_FILES "*.cpp" "*.h")

    file(GLOB HEADER_FILES  "*.h")

    include_directories(${CMAKE_CURRENT_SOURCE_DIR} )

	#lets add specific windows build definitions
	#if (WIN32)
	#	add_compile_definitions(SE_PLATFORM_WINDOWS SE_BUILD_DLL _UNICODE QUIT_ESCAPE)
	#endif (WIN32)

	#making sure to add the common cpp flags, that are defined in the main cpp file
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${COMMON_CXX_FLAGS}")


    #adding the executable
    add_library(${PROJECT_NAME} STATIC ${SOURCE_FILES} ${HEADER_FILES})

	if(APPLE)
	elseif(UNIX)
	elseif(WIN32)
		#copying built lib to the output
		add_custom_command(
		TARGET ${PROJECT_NAME} 
		POST_BUILD
		COMMAND ${CMAKE_COMMAND} -E copy
		  $<TARGET_FILE:${PROJECT_NAME}>
		  ${CMAKE_SOURCE_DIR}/../builtDependencies/windows/$<CONFIGURATION>/$<TARGET_FILE_NAME:${PROJECT_NAME}>)		
	endif()

	file(COPY ${HEADER_FILES} DESTINATION ${CMAKE_SOURCE_DIR}/../builtDependencies/includes/imgui)

