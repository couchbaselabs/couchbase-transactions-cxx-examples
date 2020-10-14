project(examples)
cmake_minimum_required(VERSION 2.8)

macro(define_example name)
    add_executable(${name} ${name}.cxx)
    target_link_libraries(${name} ${CMAKE_THREAD_LIBS_INIT} transactions_cxx ${Boost_LIBRARIES})
endmacro()

define_example(game_server)
