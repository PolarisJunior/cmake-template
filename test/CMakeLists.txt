
# Add executables by specifying the path of the test without the .cpp extension
set(
    ALL_TESTS 
    example
)

function(add_test_binary TEST_NAME)
    STRING(REGEX REPLACE "/" "_" TEST_TARGET ${TEST_NAME})

    add_executable(
        ${TEST_TARGET}
        ${TEST_NAME}.cpp
    )

    target_link_libraries(
        ${TEST_TARGET}
        GTest::GTest
        ${LIB_NAME}
    )

    gtest_add_tests(
        TARGET
        ${TEST_TARGET}
    )
endfunction(add_test_binary)

foreach(TEST_NAME ${ALL_TESTS})
    add_test_binary(${TEST_NAME})
endforeach()
