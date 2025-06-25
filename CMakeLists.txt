cmake_minimum_required(VERSION 3.22)
project(adt-creator VERSION 1.0)
include(FetchContent)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

fetchcontent_declare(
  thread_pool
  GIT_REPOSITORY https://github.com/bshoshany/thread-pool.git
  GIT_TAG v3.1.0
)
fetchcontent_makeavailable(thread_pool)

file(GLOB sources "*.h" "*.cpp")

add_executable(adt-creator ${sources})
target_include_directories(adt-creator PUBLIC "${PROJECT_SOURCE_DIR}" ${thread_pool_SOURCE_DIR})

if(UNIX)
  set(THREADS_PREFER_PTHREAD_FLAG ON)
  find_package(Threads REQUIRED)
  target_link_libraries(adt-creator PRIVATE Threads::Threads)
endif()
