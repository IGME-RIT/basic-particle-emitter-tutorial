
if(WIN32)
cmake_minimum_required (VERSION 3.1)
else()
cmake_minimum_required (VERSION 3.0)
endif()

project(basic-particle-emitter-tutorial)

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

set (basic-particle-emitter-tutorial_VERSION_MAJOR 1)
set (basic-particle-emitter-tutorial_VERSION_MINOR 0)
set (basic-particle-emitter-tutorial_VERSION_BUILD 0)

FILE(GLOB HEADERS_FILES src/include/*.h*)
source_group("Header Files" FILES ${HEADERS_FILES})

FILE(GLOB SOURCE_FILES
  src/main.cpp
  src/source/*.cpp
)
source_group("Source Files" FILES ${SOURCE_FILES})

include_directories(${CMAKE_SOURCE_DIR}/src/include/)

add_executable(basic-particle-emitter-tutorial ${HEADERS_FILES} ${SOURCE_FILES})

if (MSVC)
    file(
        COPY ${CMAKE_SOURCE_DIR}/lib/glew-1.13.0-win32.zip
        DESTINATION ${CMAKE_BINARY_DIR}
    )
    execute_process(
        COMMAND ${CMAKE_COMMAND} -E tar xfz ${CMAKE_BINARY_DIR}/glew-1.13.0-win32.zip
        WORKING_DIRECTORY ${CMAKE_BINARY_DIR}
    )
    file(
        COPY ${CMAKE_SOURCE_DIR}/lib/glfw-3.1.2.bin.WIN32.zip
        DESTINATION ${CMAKE_BINARY_DIR}
    )
    execute_process(
        COMMAND ${CMAKE_COMMAND} -E tar xfz ${CMAKE_BINARY_DIR}/glfw-3.1.2.bin.WIN32.zip
        WORKING_DIRECTORY ${CMAKE_BINARY_DIR}
    )
    file(
        COPY ${CMAKE_SOURCE_DIR}/lib/glm-0.9.7.1.zip
        DESTINATION ${CMAKE_BINARY_DIR}
    )
    execute_process(
        COMMAND ${CMAKE_COMMAND} -E tar xfz ${CMAKE_BINARY_DIR}/glm-0.9.7.1.zip
        WORKING_DIRECTORY ${CMAKE_BINARY_DIR}
    )
    file(
        COPY ${CMAKE_SOURCE_DIR}/lib/FreeImage3170Win32Win64.zip
        DESTINATION ${CMAKE_BINARY_DIR}
    )
    execute_process(
        COMMAND ${CMAKE_COMMAND} -E tar xfz ${CMAKE_BINARY_DIR}/FreeImage3170Win32Win64.zip
        WORKING_DIRECTORY ${CMAKE_BINARY_DIR}
    )

    target_link_libraries(basic-particle-emitter-tutorial
      ${CMAKE_BINARY_DIR}/glew-1.13.0/lib/Release/Win32/glew32.lib
      ${CMAKE_BINARY_DIR}/glfw-3.1.2.bin.WIN32/lib-vc2015/glfw3.lib
      ${CMAKE_BINARY_DIR}/FreeImage/Dist/x32/FreeImage.lib
      opengl32.lib
    )

    include_directories(
        ${CMAKE_BINARY_DIR}/glew-1.13.0/include
        ${CMAKE_BINARY_DIR}/glfw-3.1.2.bin.WIN32/include
        ${CMAKE_BINARY_DIR}/glm
        ${CMAKE_BINARY_DIR}/FreeImage/Dist/x32
    )

    add_custom_command(TARGET basic-particle-emitter-tutorial POST_BUILD        # Adds a post-build event to MyTest
        COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
            "${CMAKE_BINARY_DIR}/glew-1.13.0/bin/Release/Win32/glew32.dll"      # <--this is in-file
            $<TARGET_FILE_DIR:basic-particle-emitter-tutorial>)

    add_custom_command(TARGET basic-particle-emitter-tutorial POST_BUILD        # Adds a post-build event to MyTest
        COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
            "${CMAKE_SOURCE_DIR}/src/vshader.glsl"      # <--this is in-file
            ${CMAKE_BINARY_DIR})

    add_custom_command(TARGET basic-particle-emitter-tutorial POST_BUILD        # Adds a post-build event to MyTest
        COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
            "${CMAKE_SOURCE_DIR}/src/fshader.glsl"      # <--this is in-file
            ${CMAKE_BINARY_DIR})

    add_custom_command(TARGET basic-particle-emitter-tutorial POST_BUILD        # Adds a post-build event to MyTest
        COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
            "${CMAKE_SOURCE_DIR}/src/particleFrag.glsl"      # <--this is in-file
          "${CMAKE_BINARY_DIR}")

    add_custom_command(TARGET basic-particle-emitter-tutorial POST_BUILD        # Adds a post-build event to MyTest
        COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
            "${CMAKE_SOURCE_DIR}/src/particleVert.glsl"      # <--this is in-file
            "${CMAKE_BINARY_DIR}")

    add_custom_command(TARGET basic-particle-emitter-tutorial POST_BUILD        # Adds a post-build event to MyTest
        COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
            "${CMAKE_SOURCE_DIR}/src/particleGeo.glsl"      # <--this is in-file
            "${CMAKE_BINARY_DIR}")

    add_custom_command(TARGET basic-particle-emitter-tutorial POST_BUILD        # Adds a post-build event to MyTest
        COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
            "${CMAKE_BINARY_DIR}/FreeImage/Dist/x32/FreeImage.dll"
            $<TARGET_FILE_DIR:basic-particle-emitter-tutorial>)
endif (MSVC)

add_custom_command(TARGET basic-particle-emitter-tutorial POST_BUILD        # Adds a post-build event to MyTest
    COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
        "${CMAKE_SOURCE_DIR}/assets/sprite.png"
        "${CMAKE_BINARY_DIR}")
add_custom_command(TARGET basic-particle-emitter-tutorial POST_BUILD        # Adds a post-build event to MyTest
    COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
    	"${CMAKE_SOURCE_DIR}/assets/Cube.obj"
        "${CMAKE_BINARY_DIR}")
add_custom_command(TARGET basic-particle-emitter-tutorial POST_BUILD        # Adds a post-build event to MyTest
    COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
    	"${CMAKE_SOURCE_DIR}/assets/Sphere.obj"
        "${CMAKE_BINARY_DIR}")
add_custom_command(TARGET basic-particle-emitter-tutorial POST_BUILD        # Adds a post-build event to MyTest
    COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
    	"${CMAKE_SOURCE_DIR}/assets/Plane.obj"
        "${CMAKE_BINARY_DIR}")
add_custom_command(TARGET basic-particle-emitter-tutorial POST_BUILD        # Adds a post-build event to MyTest
    COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
    	"${CMAKE_SOURCE_DIR}/assets/Quad.obj"
        "${CMAKE_BINARY_DIR}")
# vim: ts=4 sw=4 et
