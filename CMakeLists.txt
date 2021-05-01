cmake_minimum_required(VERSION 2.8)  # CMake version check
project(main_project)               # Create project "main_project"

# Add main.c file of project root directory as source file
set(SOURCE_FILES main.c)

# Add executable target with source files listed in SOURCE_FILES variable
add_executable(simple_example ${SOURCE_FILES})
