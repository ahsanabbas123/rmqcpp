find_package(Threads REQUIRED) # CMake 3.26-rc3 Bug https://gitlab.kitware.com/cmake/cmake/-/issues/24505
include(CMakeFindDependencyMacro)
find_dependency(ZLIB REQUIRED)
find_dependency(Boost REQUIRED)
set(OPENSSL_USE_STATIC_LIBS TRUE)
find_dependency(OpenSSL REQUIRED)
find_dependency(GTest REQUIRED)

if( CMAKE_SIZEOF_VOID_P EQUAL 8 )
    set(BDE_PACKAGE_SEARCH_PATH "share/bde;lib64/cmake")
else()
    set(BDE_PACKAGE_SEARCH_PATH "share/bde;lib/cmake")
endif()

# BDE-required subpackages
find_package(bal REQUIRED)

add_subdirectory(rmq)
add_subdirectory(rmqtestmocks)
add_subdirectory(tests)
