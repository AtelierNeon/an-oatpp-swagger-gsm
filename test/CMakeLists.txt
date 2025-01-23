
## define path to swagger-ui res folder
add_definitions(-DOATPP_SWAGGER_RES_PATH="${CMAKE_CURRENT_LIST_DIR}/../res")

add_executable(oatpp-swagger-tests
        oatpp-swagger/tests.cpp
        oatpp-swagger/test-controllers/TestController.hpp
        oatpp-swagger/test-controllers/TestAsyncController.hpp
        oatpp-swagger/ControllerTest.cpp
        oatpp-swagger/ControllerTest.hpp
        oatpp-swagger/AsyncControllerTest.cpp
        oatpp-swagger/AsyncControllerTest.hpp
)

set_target_properties(oatpp-swagger-tests PROPERTIES
        CXX_STANDARD 11
        CXX_EXTENSIONS OFF
        CXX_STANDARD_REQUIRED ON
)

target_include_directories(oatpp-swagger-tests
        PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}
)

if(OATPP_MODULES_LOCATION STREQUAL OATPP_MODULES_LOCATION_EXTERNAL)
    add_dependencies(oatpp-swagger-tests ${LIB_OATPP_EXTERNAL})
endif()

add_dependencies(oatpp-swagger-tests ${OATPP_THIS_MODULE_NAME})

target_link_oatpp(oatpp-swagger-tests)

target_link_libraries(oatpp-swagger-tests
        PRIVATE ${OATPP_THIS_MODULE_NAME}
)

## TODO link dependencies here (if some)

add_test(oatpp-swagger-tests oatpp-swagger-tests)
