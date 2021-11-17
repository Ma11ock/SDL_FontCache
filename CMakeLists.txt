cmake_minimum_required(VERSION 3.1)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")

project(SDL_FontCache VERSION 0.10.0 LANGUAGES C)

find_package(SDL2)

if(NOT SDL2_FOUND OR NOT SDL2MAIN_LIBRARY)
  message(FATAL_ERROR "Could not find system SDL library")
endif()

find_package(SDL2_ttf)

if(NOT SDL2_TTF_FOUND)
  message(FATAL_ERROR "Could not find system SDL_ttf")
endif()

add_library(FontCache
    SDL_FontCache.h
    SDL_FontCache.c
)

target_link_libraries(FontCache PUBLIC ${SDL2_LIBRARY})
target_link_libraries(FontCache PUBLIC ${SDL2_TTF_LIBRARIES})
target_include_directories(FontCache PUBLIC ${SDL2_INCLUDE_DIR})
target_include_directories(FontCache PUBLIC ${SDL2_TTF_INCLUDE_DIRS})
target_include_directories(FontCache PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

target_link_libraries(FontCache PUBLIC ${SDL_GPU_LINKED_LIB})
target_include_directories(FontCache PUBLIC ${SDL2_GPU_INCLUDE_DIR})

target_compile_definitions(FontCache PUBLIC FC_USE_SDL_GPU)
