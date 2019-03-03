find_package(JlCxx REQUIRED)

add_library(im ${PROJECT_SOURCE_DIR}/visualdl/logic/im.cc)
add_library(sdk ${PROJECT_SOURCE_DIR}/visualdl/logic/sdk.cc ${PROJECT_SOURCE_DIR}/visualdl/utils/image.h)
add_dependencies(im storage_proto)
add_dependencies(sdk entry binary_record storage storage_proto eigen3)

add_library(vdljl SHARED vdljl.cc)
add_dependencies(vdljl im entry tablet sdk storage protobuf eigen3)
target_link_libraries(vdljl PRIVATE JlCxx::cxxwrap_julia entry binary_record im tablet storage sdk protobuf ${OPTIONAL_LINK_FLAGS})

install(TARGETS vdljl
    RUNTIME DESTINATION lib
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib)