cmake_minimum_required(VERSION 3.18)

project("libmicrohttpd-playground")

set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -static")

# find_package(portaudio 19 EXACT REQUIRED) # PATHS "P:\\Downloads\\cpp-libraries\\portaudio\\build\\cmake\\portaudio")
add_library(libmicrohttpd STATIC IMPORTED)

set_property(
  TARGET libmicrohttpd APPEND PROPERTY IMPORTED_CONFIGURATIONS RELEASE
)

set_target_properties(libmicrohttpd PROPERTIES
  IMPORTED_LINK_INTERFACE_LANGUAGES_RELEASE "C"
  IMPORTED_LOCATION_RELEASE "${libmicrohttpd_ROOT}/lib/libmicrohttpd.a"
)
  
set_target_properties(libmicrohttpd PROPERTIES
  MAP_IMPORTED_CONFIG_MINSIZEREL Release
  MAP_IMPORTED_CONFIG_RELWITHDEBINFO Release
)

target_include_directories(libmicrohttpd INTERFACE "${libmicrohttpd_ROOT}/include")

add_executable(${PROJECT_NAME}
    "src/main.c"
)

target_link_libraries(${PROJECT_NAME} libmicrohttpd ws2_32)
