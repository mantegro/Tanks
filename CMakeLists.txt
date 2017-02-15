cmake_minimum_required(VERSION 3.0.2 FATAL_ERROR)

set(CMAKE_CXX_STANDARD 11) # C++11...
set(CMAKE_CXX_STANDARD_REQUIRED ON) #...is required...
set(CMAKE_CXX_EXTENSIONS OFF) #...without compiler extensions like gnu++11

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR}/lib/Debug)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR}/lib/Debug)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR}/bin/Debug)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR}/lib/Release)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR}/lib/Release)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR}/bin/Release)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_RELWITHDEBINFO ${CMAKE_BINARY_DIR}/lib/RelWithDebInfo)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_RELWITHDEBINFO ${CMAKE_BINARY_DIR}/lib/RelWithDebInfo)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELWITHDEBINFO ${CMAKE_BINARY_DIR}/bin/RelWithDebInfo)

set (PROJECT_NAME Bot)
project (${PROJECT_NAME}) 

find_package (OpenGL REQUIRED)




#==================================================================#
#                              GLFW                                #
#==================================================================#
set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)

add_subdirectory (external/glfw-3.2.1/)
include_directories (external/glfw-3.2.1/include/)
#==================================================================#






#==================================================================#
#                              GLEW                                #
#==================================================================#
include_directories (external/glew-2.0.0/include/)
add_definitions(-DGLEW_STATIC)
add_library(glew STATIC
  external/glew-2.0.0/src/glew.c
  external/glew-2.0.0/include
)
#==================================================================#



#==================================================================#
#                              GLM                                 #
#==================================================================#
include_directories (external/glm-0.9.8.4/)
#==================================================================#



set(ALL_EXTERNAL_LIBS
	${OPENGL_LIBRARY}
	glfw ${GLFW_STATIC_LIBRARIES}
	glew
)



set (MAIN_SOURCES
    src/main.cpp
)
    
#add_subdirectory (src/Renderer)
  
set (HEADERS
    #src/Renderer/ShaderProgram.h
)
 
 
set (SOURCES 
	#src/Renderer/ShaderProgram.cpp
)


add_executable (${PROJECT_NAME} ${MAIN_SOURCES} ${HEADERS} ${SOURCES})
target_link_libraries (${PROJECT_NAME} ${ALL_EXTERNAL_LIBS}) 
#target_link_libraries (${PROJECT_NAME} ${ALL_EXTERNAL_LIBS} Renderer) 