set(bench_dir_list "${CMAKE_CURRENT_SOURCE_DIR}/lib")

foreach(bench_dir ${bench_dir_list})
    file(GLOB_RECURSE bench_files "${bench_dir}/*-bench.cpp" "${bench_dir}/*-bench.cc")
    get_filename_component(dir_name ${bench_dir} NAME)

    set(bench_name ${dir_name}_bench)
    add_executable(${bench_name} EXCLUDE_FROM_ALL ${bench_files})
    target_link_libraries(${bench_name} PRIVATE lib_obj benchmark::benchmark)

    add_custom_target(
        bench-${dir_name}
        COMMENT "Running bench ${bench_name}..."
        COMMAND ${bench_name}
    )
    set_target_properties(${bench_name} PROPERTIES RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/benches")

    list(APPEND BENCH_TARGETS ${bench_name})
endforeach(bench_dir ${bench_dir_list})