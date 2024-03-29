cmake_minimum_required(VERSION 3.8)
project(xfce4-no-sleep-on-battery-lid-closed LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include(GNUInstallDirs)

find_package(PkgConfig REQUIRED)

pkg_check_modules(GIO REQUIRED IMPORTED_TARGET gio-unix-2.0)
pkg_check_modules(X11 REQUIRED IMPORTED_TARGET xcb xcb-randr)
pkg_check_modules(Xfconf REQUIRED IMPORTED_TARGET libxfconf-0)

add_executable(${PROJECT_NAME}
    main.cpp
)

target_link_libraries(${PROJECT_NAME}
    PRIVATE
    PkgConfig::GIO
    PkgConfig::X11
    PkgConfig::Xfconf
)

configure_file(
    "${CMAKE_SOURCE_DIR}/xfce4-no-sleep-on-battery-lid-closed.desktop.in"
    "${CMAKE_BINARY_DIR}/xfce4-no-sleep-on-battery-lid-closed.desktop"
    IMMEDIATE @ONLY
)

install(TARGETS ${PROJECT_NAME}
    DESTINATION ${CMAKE_INSTALL_BINDIR}
)
install(FILES "${CMAKE_BINARY_DIR}/xfce4-no-sleep-on-battery-lid-closed.desktop"
    DESTINATION "${CMAKE_INSTALL_FULL_SYSCONFDIR}/xdg/autostart"
)

if(NOT TARGET uninstall)
    configure_file(
        "${CMAKE_CURRENT_SOURCE_DIR}/cmake_uninstall.cmake.in"
        "${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake"
        IMMEDIATE @ONLY
    )

    add_custom_target(uninstall
        COMMAND ${CMAKE_COMMAND} -P ${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake
    )
endif()
