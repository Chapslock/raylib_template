cmake_minimum_required(VERSION 3.0)
project(raylib_template C CXX)

set(CMAKE_CXX_STANDARD 17)

#This collects all the files in src/ and adds them to the executable
file(GLOB_RECURSE PROJECT_SOURCE_FILES CONFIGURE_DEPENDS
        "src/*.cpp"
        "src/*.h"
)

add_executable(${PROJECT_NAME}
        ${PROJECT_SOURCE_FILES}
)

# Raylib
add_subdirectory(libs/raylib) #Add the raylib dir to the build
# Setting parameters for raylib
set(BUILD_EXAMPLES OFF CACHE BOOL "" FORCE) # don't build the supplied examples
set(BUILD_GAMES    OFF CACHE BOOL "" FORCE) # or games


target_link_libraries(${PROJECT_NAME}
        PRIVATE raylib
)
target_compile_definitions(${PROJECT_NAME}
        PUBLIC ASSETS_PATH="${CMAKE_CURRENT_SOURCE_DIR}/assets/" # Set the asset path macro to the absolute path on the dev machine
)
#target_compile_definitions(${PROJECT_NAME} PUBLIC ASSETS_PATH="relative-path-to-assets-in-the-game-package") # Set the asset path macro in release mode
