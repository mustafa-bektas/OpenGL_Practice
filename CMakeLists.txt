cmake_minimum_required(VERSION 3.10)
project(OpenGL_Practice)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Find OpenGL
find_package(OpenGL REQUIRED)

add_subdirectory(external/glfw)

# Add GLAD
add_library(glad external/glad/src/glad.c)
target_include_directories(glad PUBLIC external/glad/include)

# Create executable
add_executable(${PROJECT_NAME} 
    src/main.cpp
    src/stb_image.cpp
)

# Include directories
target_include_directories(${PROJECT_NAME} PRIVATE 
    external/glad/include
    external/glfw/include
    ./include
)

# Link libraries
target_link_libraries(${PROJECT_NAME} 
    ${OPENGL_LIBRARIES}
    glfw
    glad
)

# macOS specific settings
if(APPLE)
    target_link_libraries(${PROJECT_NAME} 
        "-framework Cocoa"
        "-framework IOKit"
        "-framework CoreVideo"
    )
endif()