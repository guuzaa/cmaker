file(GLOB_RECURSE EXAMPLE_SOURCES "${PROJECT_SOURCE_DIR}/examples/*.cc" "${PROJECT_SOURCE_DIR}/examples/*.cpp")

add_custom_target(example)

foreach (example_source ${EXAMPLE_SOURCES})
    get_filename_component(example_filename ${example_source} NAME)
    add_executable(${example_filename} EXCLUDE_FROM_ALL ${example_source})

    add_custom_command(
        TARGET example
        COMMENT "Running example ${example_filename}..."
        COMMAND $<TARGET_FILE:${example_filename}>
        USES_TERMINAL
    )

    target_link_libraries(${example_filename} PRIVATE lib_obj)

    set_target_properties(${example_filename}
            PROPERTIES
            RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/examples"
            COMMAND ${example_filename}
    )

    add_custom_target("example-${example_filename}"
        COMMENT "Running example ${example_filename}..."
        COMMAND ${example_filename}
    )
endforeach ()
