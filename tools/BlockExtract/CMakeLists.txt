PROTOBUF_GENERATE_CPP(IR_PROTO_SRCS IR_PROTO_HDRS ${codeReason_SOURCE_DIR}/libs/IR/IR.proto)

include_directories(${codeReason_SOURCE_DIR}/libs/IR ${codeReason_SOURCE_DIR}/libs/IR ${codeReason_SOURCE_DIR}/libs/VEE ${codeReason_SOURCE_DIR}/libs/getExecSections ${codeReason_SOURCE_DIR}/lua-5.3.0/src ${codeReason_SOURCE_DIR}/libs/RopLib ${CMAKE_CURRENT_BINARY_DIR} )

link_directories(${Boost_LIBRARY_DIRS})
add_definitions(-D__STDC_LIMIT_MACROS)

add_executable( BlockExtract 
                BlockExtract.cpp
                ${IR_PROTO_SRCS}
                ${IR_PROTO_HDRS})

IF(WIN32)
target_link_libraries(  BlockExtract 
                        ${PROTOBUF_LIBRARIES} 
                        VEE 
                        RopLib 
                        IR 
                        getExecSections 
                        lua 
                        ${PE-PARSE_LIB}
                        ${VEX_LIB} 
                        ${CMAKE_THREAD_LIBS_INIT} 
                        ${Boost_LIBRARIES} )
ELSE(WIN32)
target_link_libraries(  BlockExtract 
                        ${PROTOBUF_LIBRARIES}
                        VEE 
                        RopLib 
                        IR 
                        getExecSections 
                        MachOLib 
                        lua 
                        ${PE-PARSE_LIB}
                        ${VEX_LIB} 
                        ${CMAKE_THREAD_LIBS_INIT} 
                        ${Boost_LIBRARIES} 
                        dl)
ENDIF(WIN32)
