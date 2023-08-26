# CMakeList.txt : CMake project for OpenglTutus, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)

# Enable Hot Reload for MSVC compilers if supported.
if (POLICY CMP0141)
  cmake_policy(SET CMP0141 NEW)
  set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

project ("OpenglTutus")

# Add source to this project's executable.
add_executable (OpenglTutus "src/OpenglTutus.cpp" "src/OpenglTutus.h")

if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET OpenglTutus PROPERTY CXX_STANDARD 20)
endif()
 if(${CMAKE_BUILD_TYPE} EQUAL Release)
	target_link_directories(OpenglTutus PRIVATE lib/glew-2.1.0/lib/Release/x64)
elseif(${CMAKE_BUILD_TYPE} EQUAL "Debug")
	target_link_directories(OpenglTutus PRIVATE lib/glew-2.1.0/lib/Debug/x64)
endif()
message(${CMAKE_BUILD_TYPE})
add_subdirectory(lib/glfw)
target_link_directories(OpenglTutus PRIVATE lib/glew-2.1.0/lib/Debug/x64)

add_definitions(-DGLEW_STATIC)
target_link_directories(OpenglTutus PRIVATE lib/glfw)
target_link_libraries(OpenglTutus opengl32 glfw glew32sd)
target_include_directories(OpenglTutus PRIVATE lib/glew-2.1.0/include lib/glfw/include)