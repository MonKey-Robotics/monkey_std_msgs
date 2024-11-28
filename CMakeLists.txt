
cmake_minimum_required(VERSION 3.8)
project(monkey_std_msgs)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# Find dependencies
find_package(ament_cmake REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(rosidl_default_generators REQUIRED)

# Include the function for finding .srv and .action files
function(find_rosidl_interfaces TARGET_VAR DIRECTORY)
  # Search for .srv files
  file(GLOB_RECURSE SRV_FILES RELATIVE ${DIRECTORY} "${DIRECTORY}/srv/*.srv")
  foreach(SRV_FILE ${SRV_FILES})
    list(APPEND INTERFACE_FILES ${SRV_FILE})
  endforeach()

  # Search for .action files
  file(GLOB_RECURSE ACTION_FILES RELATIVE ${DIRECTORY} "${DIRECTORY}/action/*.action")
  foreach(ACTION_FILE ${ACTION_FILES})
    list(APPEND INTERFACE_FILES ${ACTION_FILE})
  endforeach()

  # Search for .msg files
  file(GLOB_RECURSE MSG_FILES RELATIVE ${DIRECTORY} "${DIRECTORY}/msg/*.msg")
  foreach(MSG_FILE ${MSG_FILES})
    list(APPEND INTERFACE_FILES ${MSG_FILE})
  endforeach()

  # Output the results to the target variable
  set(${TARGET_VAR} ${INTERFACE_FILES} PARENT_SCOPE)
endfunction()

# Use the function to find .srv, .action and .msg files in the current source directory
find_rosidl_interfaces(INTERFACE_FILES ${CMAKE_CURRENT_SOURCE_DIR})

# Debug: Output the found interface files (optional)
message(STATUS "Discovered Interface Files: ${INTERFACE_FILES}")

# Generate interfaces with only relative paths
rosidl_generate_interfaces(${PROJECT_NAME}
  ${INTERFACE_FILES}
  DEPENDENCIES geometry_msgs
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  set(ament_cmake_cpplint_FOUND TRUE) # Skip cpplint if needed
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
