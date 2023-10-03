cmake_minimum_required(VERSION 3.16)

project(QtSampleApp VERSION 1.0.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Qt6 REQUIRED COMPONENTS Widgets)
qt_standard_project_setup()

qt_add_executable(QtSampleApp
    mainwindow.ui
    mainwindow.cpp
    main.cpp
)

target_link_libraries(QtSampleApp PRIVATE Qt6::Widgets)

set_target_properties(QtSampleApp PROPERTIES
    WIN32_EXECUTABLE ON
    MACOSX_BUNDLE ON
)

# Install the executable into "${CMAKE_INSTALL_PREFIX}/bin".
install(TARGETS QtSampleApp
    BUNDLE  DESTINATION .
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

# Generate the deployment script for the target QtSampleApp.
qt_generate_deploy_app_script(
    TARGET QtSampleApp
    OUTPUT_SCRIPT deploy_script
    NO_UNSUPPORTED_PLATFORM_ERROR
)

# Call the deployment script on "cmake --install".
install(SCRIPT ${deploy_script})

set(CPACK_PACKAGE_NAME QtSampleApp)
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "The amazing QT sample app")
set(CPACK_PACKAGE_INSTALL_DIRECTORY ${CPACK_PACKAGE_NAME})
set(CPACK_VERBATIM_VARIABLES ON)
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Daniel Hafner")
set(CPACK_DEBIAN_PACKAGE_DEPENDS libc6 libstdc++6 libgcc-s1)
include(CPack)