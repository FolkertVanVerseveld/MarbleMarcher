cmake_minimum_required(VERSION 3.0)
project(MarbleMarcher)
set(CMAKE_CXX_STANDARD 11)

# Set to TRUE to use tracy profiler framework
set(PROFILING TRUE)

## DEPENDENCIES

find_package(Eigen3 3.3 REQUIRED)
find_package(SFML 2.5 COMPONENTS system window graphics audio REQUIRED)

if(PROFILING)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DTRACY_ENABLE=1")
  set(PROFILE_SOURCES "vendor/tracy/TracyClient.cpp")
endif()

## TARGETS

add_subdirectory(src)
target_include_directories(MarbleMarcherSources PUBLIC
  ${EIGEN3_INCLUDE_DIR}
  ${SFML_INCLUDE_DIR}
)
target_compile_definitions(MarbleMarcherSources PRIVATE SFML_STATIC)

add_subdirectory(vendor/imgui-sfml)

if(WIN32)
  add_executable(MarbleMarcher WIN32 src/Main.cpp "${PROFILE_SOURCES}" src/Resource.rc assets/icon.ico)
  set_source_files_properties(icon.ico Resource.rc PROPERTIES LANGUAGE RC)
else()
  add_executable(MarbleMarcher src/Main.cpp "${PROFILE_SOURCES}")
endif()
target_compile_definitions(MarbleMarcher PRIVATE SFML_STATIC)
target_link_libraries(MarbleMarcher
  MarbleMarcherSources
  sfml-system
  sfml-window
  sfml-graphics
  sfml-audio
  ImGui-SFML::ImGui-SFML
)

file(COPY "assets" DESTINATION ${CMAKE_BINARY_DIR})
