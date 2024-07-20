file(GLOB obj_files "${CMAKE_CURRENT_SOURCE_DIR}/*.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/*.c")

add_library(
    lib_obj
    OBJECT
    ${obj_files}
)

set(ALL_OBJECT_FILES ${ALL_OBJECT_FILES} $<TARGET_OBJECTS:lib_obj> PARENT_SCOPE)