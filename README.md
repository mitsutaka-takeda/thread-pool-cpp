thread-pool-cpp
=================
[![Build Status](https://travis-ci.org/warchant/thread-pool-cpp.svg?branch=master)](https://travis-ci.org/inkooboo/thread-pool-cpp)
[![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](./LICENSE)

 * It is highly scalable and fast.
 * It is header only.
 * No external dependencies, only standard library needed.
 * It implements both work-stealing and work-distribution balancing startegies.
 * It implements cooperative scheduling strategy.

Example run:
Post job to thread pool is much faster than for boost::asio based thread pool.

    Benchmark job reposting
    ***thread pool cpp***
    reposted 1000001 in 61.6754 ms
    reposted 1000001 in 62.0187 ms
    reposted 1000001 in 62.8785 ms
    reposted 1000001 in 70.2714 ms
    ***asio thread pool***
    reposted 1000001 in 1381.58 ms
    reposted 1000001 in 1390.35 ms
    reposted 1000001 in 1391.84 ms
    reposted 1000001 in 1393.19 ms

See benchmark/benchmark.cpp for benchmark code.

All code except [MPMCBoundedQueue](https://github.com/inkooboo/thread-pool-cpp/blob/master/include/thread_pool/mpmc_bounded_queue.hpp)
is under MIT license.

# Build instructions

This thread pool can be build for:
- linux
    [x] g++-5 and higher
    [x] clang-4 and higher
- mac os
    [x] g++
    [x] clang

```
mkdir build
cd build
cmake .. -DCMAKE_BUILD_TYPE=Release -DTESTS=ON -DINSTALL=ON -DBENCHMARK=ON -DCOVERAGE=OFF
make
```
