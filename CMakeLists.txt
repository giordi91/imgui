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

	file(COPY ${HEADER_FILES} DESTINATION "${CMAKE_SOURCE_DIR}/SirEngineThe3rdLib/vendors/includes/imgui" )


    #adding the executable
    add_library(${PROJECT_NAME} STATIC ${SOURCE_FILES} ${INCLUDES_FILES})
	#set(CMAKE_BINARY_DIR  )
	#SET(EXECUTABLE_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/bin)
	SET(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR}/bin)

	#setting the plug-in folder in the solution
	set_target_properties (${PROJECT_NAME} PROPERTIES
    FOLDER vendors)

	#target_link_libraries(${PROJECT_NAME} d3dcompiler DXGI D3D12)
	#d3dcompiler.lib;DXGI.lib;D3D12.lib;