function(add_chapter CHAPTER_NAME)

    file(GLOB SOURCES ./${CHAPTER_NAME}/*.h ./${CHAPTER_NAME}/*.cpp)
    add_executable(${CHAPTER_NAME} ${SOURCES})
    set_target_properties(${CHAPTER_NAME} PROPERTIES
        RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${CHAPTER_NAME})
    set_target_properties(${CHAPTER_NAME} PROPERTIES CXX_STANDARD 17)
    target_link_libraries(${CHAPTER_NAME} Vulkan::Vulkan glfw)
    target_include_directories(${CHAPTER_NAME} PRIVATE ${STB_INCLUDEDIR})

endfunction()

add_chapter(00_base_code)
add_chapter(01_instance_creation)
add_chapter(02_validation_layers)