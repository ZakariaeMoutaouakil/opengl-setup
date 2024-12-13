cmake_minimum_required(VERSION 3.30)
project(opengl)

set(CMAKE_CXX_STANDARD 20)

# Find OpenGL
find_package(OpenGL REQUIRED)

include(FetchContent)

FetchContent_Declare(
        glfw
        GIT_REPOSITORY https://github.com/glfw/glfw.git
        GIT_TAG        master    # This will get the latest commit
)

FetchContent_MakeAvailable(glfw)

# Create your executable
add_executable(your_program src/main.cpp)

# Link against both GLFW and OpenGL
target_link_libraries(your_program PRIVATE glfw OpenGL::GL)