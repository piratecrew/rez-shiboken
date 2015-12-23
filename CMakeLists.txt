CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

include(RezBuild)
include(ExternalProject)

set(shiboken_version ${SHIBOKEN_VERSION})

set(url_shiboken https://github.com/PySide/Shiboken.git)

set(make_args -j1 VERBOSE=on)

if(${REZ_BUILD_INSTALL})
    set(install_cmd make install ${make_args})
else()
    set(install_cmd "")
endif()

ExternalProject_add(
    shiboken-src
    GIT_REPOSITORY ${url_shiboken}
    GIT_TAG ${shiboken_version}
    PREFIX shiboken-src
    BUILD_COMMAND make -j1 VERBOSE=on
    CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}
    BUILD_IN_SOURCE 0
)
