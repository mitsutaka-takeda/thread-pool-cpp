#tests

function(build_test test_name)
    add_executable(${test_name}_test ${ARGN}) 
    target_compile_options(${test_name}_test PRIVATE -Wall -Wextra -Wsign-compare)
    target_link_libraries(${test_name}_test ThreadPoolCpp::ThreadPoolCpp pthread gtest gtest_main)
    add_test(NAME ${test_name}.test COMMAND ./${test_name}_test)
endfunction()

build_test(fixed_function fixed_function.t.cpp)
build_test(thread_pool thread_pool.t.cpp)
build_test(thread_pool_options thread_pool_options.t.cpp)
