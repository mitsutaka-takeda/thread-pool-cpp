#benchmark

add_executable(benchmark benchmark.cpp)
target_compile_options(
  benchmark
  PRIVATE
  -Wall
  -Wextra
  -Wsign-compare
  )
target_link_libraries(benchmark ThreadPoolCpp::ThreadPoolCpp pthread)
