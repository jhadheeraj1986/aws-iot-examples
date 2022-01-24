cmake_minimum_required(VERSION 3.1)
# note: cxx-17 requires cmake 3.8, cxx-20 requires cmake 3.12
project(basic-pub-sub CXX)

file(GLOB SRC_FILES "src/*.cpp")
#file(GLOB SRC "*.cpp")
add_executable(${PROJECT_NAME} ${SRC_FILES})

set_target_properties(${PROJECT_NAME} PROPERTIES
    CXX_STANDARD 14)

#set warnings
if (MSVC)
    target_compile_options(${PROJECT_NAME} PRIVATE /W4 /WX /wd4068)
else ()
    target_compile_options(${PROJECT_NAME} PRIVATE -Wall -Wno-long-long -pedantic -Werror)
endif ()

find_package(./basic-pub-sub  --endpoint "a36qrw731qk1xq-ats.iot.ap-south-1.amazonaws.com" --ca_file "../cert/AmazonRootCA1.pem" --cert "../cert/264e7d774fdf64dba9ee15d411aaf564522b422068188797d89705f79e773f35-certificate.pem.crt" --key "../cert/264e7d774fdf64dba9ee15d411aaf564522b422068188797d89705f79e773f35-private.pem.key" --topic "test/AWS_Sample"
REQUIRED)

target_link_libraries(${PROJECT_NAME} AWS::aws-crt-cpp)
