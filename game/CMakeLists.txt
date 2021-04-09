project(examples)
cmake_minimum_required(VERSION 3.5.1)

set(CMAKE_CXX_STANDARD 11)

find_package(Threads REQUIRED)
if(THREADS_HAVE_PTHREAD_ARG)
  target_compile_options(my_app PUBLIC "-pthread")
endif()

set(Boost_USE_MULTITHREADED ON)
set(Boost_USE_STATIC_LIBS ${STATIC_BOOST})
find_package(Boost REQUIRED COMPONENTS system thread date_time)
include_directories(BEFORE ${Boost_INCLUDE_DIRS})

message(STATUS "Boost_INCLUDE_DIRS: ${Boost_INCLUDE_DIRS}")
message(STATUS "Boost_LIBRARIES: ${Boost_LIBRARIES}")

find_library(TRANSACTIONS_CXX transactions_cxx)
message(STATUS "transactions:" ${TRANSACTIONS_CXX})

add_executable(game_server game_server.cxx)
target_link_libraries(game_server ${CMAKE_THREAD_LIBS_INIT} ${TRANSACTIONS_CXX} ${Boost_LIBRARIES})

