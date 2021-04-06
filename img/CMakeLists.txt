cmake_minimum_required( VERSION 3.16.1 ) # Latest version of CMake when this file was created.

# Make sure DLL and EXE targets go to the same directory.
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib) # Output directory for static lib (.LIB)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin) # Output directory for shared lib (.DLL)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin) # Output directory for executables (.EXE)

project( BKRender )

# Assimp
set( ASSIMP_BUILD_ASSIMP_TOOLS OFF CACHE BOOL "Build Assimp Tools" FORCE )
set( ASSIMP_BUILD_SAMPLES OFF CACHE BOOL "Build Assimp Samples" FORCE )
set( ASSIMP_BUILD_TESTS OFF CACHE BOOL "Build Assimp Tests" FORCE )
add_subdirectory( Extern/assimp )
set_target_properties( assimp IrrXML uninstall UpdateAssimpLibsDebugSymbolsAndDLLs zlib zlibstatic 
    PROPERTIES
        FOLDER assimp 
)

add_subdirectory( Extern/DirectXTex )

add_subdirectory(DX12Lib)
add_subdirectory(Samples/01-ClearScreen)
add_subdirectory(Samples/02-Cube)
add_subdirectory(Samples/03-Texture)

set_target_properties( 01-ClearScreen 02-Cube 03-Texture
    PROPERTIES
        FOLDER Samples
)