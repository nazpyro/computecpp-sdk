set(SOURCE_NAME "matrix-multiply")
add_executable(
  ${SOURCE_NAME}
  ${CMAKE_CURRENT_SOURCE_DIR}/${SOURCE_NAME}.cpp
)
if(NOT MSVC)
  target_compile_options(
    ${SOURCE_NAME}
    PUBLIC -Wno-unknown-pragmas
  )
endif()
add_sycl_to_target(
  ${SOURCE_NAME}
  ${CMAKE_CURRENT_BINARY_DIR}
  ${CMAKE_CURRENT_SOURCE_DIR}/${SOURCE_NAME}.cpp
)
add_test(
  NAME ${SOURCE_NAME}_omp
  COMMAND ${SOURCE_NAME} 64 omp
)
add_test(
  NAME ${SOURCE_NAME}_sycl
  COMMAND ${SOURCE_NAME} 64 sycl
)
install(
  TARGETS ${SOURCE_NAME}
  RUNTIME DESTINATION bin
)
