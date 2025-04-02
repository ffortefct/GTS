cmake_minimum_required(VERSION 3.22)

project(GTS LANGUAGES CXX CUDA)

cmake_policy(SET CMP0146 OLD)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CUDA_STANDARD 11)
set(CUDA_SEPARABLE_COMPILATION ON)

include_directories(include)

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
aux_source_directory(src SRC_LIST)

find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})

add_executable(${PROJECT_NAME} ${SRC_LIST})

target_compile_options(${PROJECT_NAME} PRIVATE
  $<$<COMPILE_LANGUAGE:CUDA>:-Xcompiler=-O2>
)

target_link_libraries(${PROJECT_NAME} PRIVATE
  ${OpenCV_LIBS}
)
