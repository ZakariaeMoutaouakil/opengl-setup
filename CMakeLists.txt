cmake_minimum_required(VERSION 3.30)
project(opengl)

set(CMAKE_CXX_STANDARD 20)

include(FetchContent)

# GLFW setup (from before)
FetchContent_Declare(
        glfw
        GIT_REPOSITORY https://github.com/glfw/glfw.git
        GIT_TAG        master
)

# GLAD setup with latest commit
FetchContent_Declare(
        glad
        GIT_REPOSITORY https://github.com/Dav1dde/glad.git
        GIT_TAG        glad2
)

FetchContent_MakeAvailable(glfw glad)

# Configure GLAD
add_subdirectory(${glad_SOURCE_DIR}/cmake glad_cmake)
glad_add_library(glad_lib API gl:core=4.6)

# Find OpenGL
find_package(OpenGL REQUIRED)

# Create your executable
add_executable(your_program src/main.cpp)

# Add include directories for GLAD
target_include_directories(your_program PRIVATE
        ${glad_BINARY_DIR}/include
)

# Link everything
target_link_libraries(your_program PRIVATE
        glfw
        OpenGL::GL
        glad_lib
)