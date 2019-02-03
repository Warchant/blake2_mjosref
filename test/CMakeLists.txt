enable_testing()

add_executable(blake2s_test test_main.c)
add_test(NAME blake2s_test COMMAND blake2s_test)
target_link_libraries(blake2s_test blake2s)
