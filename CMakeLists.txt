cmake_minimum_required(VERSION 2.8)

project (object-wrap-cmake-js)

find_package(OpenCV REQUIRED)

# Include N-API wrappers
execute_process(COMMAND node -p "require('node-addon-api').include"
        WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
        OUTPUT_VARIABLE NODE_ADDON_API_DIR
        )
string(REPLACE "\n" "" NODE_ADDON_API_DIR ${NODE_ADDON_API_DIR})
string(REPLACE "\"" "" NODE_ADDON_API_INC_DIR ${NODE_ADDON_API_DIR})

message(NOTICE ${NODE_ADDON_API_INC_DIR})

include_directories(${CMAKE_JS_INC} ${NODE_ADDON_API_INC_DIR} ${OpenCV_INC_DIRS})

set(SOURCE_FILES src/object_wrap_demo.cpp)

add_library(${PROJECT_NAME} SHARED ${SOURCE_FILES} ${CMAKE_JS_SRC})
set_target_properties(${PROJECT_NAME} PROPERTIES PREFIX "" SUFFIX ".node")
target_link_libraries(${PROJECT_NAME} ${CMAKE_JS_LIB} ${OpenCV_LIBS})
