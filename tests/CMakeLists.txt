enable_testing()


# TODO how to read from the local directory
set(test_dir_list "${CMAKE_CURRENT_SOURCE_DIR}/lib")

foreach(test_dir ${test_dir_list})
    file(GLOB_RECURSE test_files "${test_dir}/*-test.cpp" "${test_dir}/*-test.cc")
    get_filename_component(dir_name ${test_dir} NAME)

    set(test_name ${dir_name}_test)
    add_executable(${test_name} EXCLUDE_FROM_ALL ${test_files})
    target_link_libraries(${test_name} PRIVATE lib_obj gtest gmock_main)

    add_custom_target(
        test-${dir_name}
        COMMENT "Running test ${test_name}..."
        COMMAND ${test_name}
    )
    set_target_properties(${test_name} PROPERTIES RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/tests")

    list(APPEND TEST_TARGETS ${test_name})
    add_test(NAME ${test_name} COMMAND ${test_name})
endforeach(test_dir ${test_dir_list})

add_custom_target(run-tests
    COMMAND ${CMAKE_CTEST_COMMAND} -C Debug
    DEPENDS ${TEST_TARGETS}
    COMMENT "Build and Run All Tests..."
)

add_custom_target(check-tests
    COMMAND ${CMAKE_CTEST_COMMAND} -C Debug --verbose
    DEPENDS ${TEST_TARGETS}
    COMMENT "Runnig All Tests..."
)
