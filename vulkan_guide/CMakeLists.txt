project(vulkan_guide)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${PROJECT_SOURCE_DIR}/bin")

find_program(GLSL_VALIDATOR glslangValidator HINTS "$ENV{VULKAN_SDK}/Bin")

file(GLOB_RECURSE GLSL_SOURCE_FILES
    ${PROJECT_SOURCE_DIR}/shaders/*.frag
    ${PROJECT_SOURCE_DIR}/shaders/*.vert
    ${PROJECT_SOURCE_DIR}/shaders/*.comp)

foreach (GLSL ${GLSL_SOURCE_FILES})
    message(STATUS "Compiling shader: ${GLSL}")

    get_filename_component(FILE_NAME ${GLSL} NAME)
    set(SPIRV ${PROJECT_SOURCE_DIR}/bin/${FILE_NAME}.spv)

    add_custom_command(
        OUTPUT ${SPIRV}
        COMMAND ${GLSL_VALIDATOR} -V ${GLSL} -o ${SPIRV}
        DEPENDS ${GLSL})

    list(APPEND SPIRV_BINARY_FILES ${SPIRV})
endforeach (GLSL)

add_custom_target(
    Shaders
    DEPENDS ${SPIRV_BINARY_FILES})

add_subdirectory(chapter0)
add_subdirectory(chapter1)
