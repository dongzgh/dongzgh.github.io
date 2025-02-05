# //external/MyLibrary/CMakeLists.txt
# MyLibrary target
add_library(MyLibrary
    include/my_library.h
    src/my_library.cpp
)

# Include directories for MyLibrary
target_include_directories(MyLibrary PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
