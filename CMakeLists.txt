PROJECT(avida4)

CMAKE_MINIMUM_REQUIRED(VERSION 3.0)


# Final software is built in the cbuild directory
SET(EXECUTABLE_OUTPUT_PATH
   ${PROJECT_BINARY_DIR}/bin
   CACHE PATH
   "Directory containing all built executables."
   )


# Place all built libraries (including external)
# libraries in this directory
SET(LIBRARY_OUTPUT_PATH
   ${PROJECT_BINARY_DIR}/lib
   CACHE PATH
   "Directory containing built libraries."
   )


ADD_SUBDIRECTORY(avida4-core)

# Default location for installed software/configs is the build directory
SET(CMAKE_INSTALL_PREFIX
   "${PROJECT_BINARY_DIR}"
   CACHE PATH
   "Install path prefix, prepended onto all install directories."
   FORCE
   )


# Because we're going to be using our own build system
# to compile these libraries, we will have to rely on
# keeping as much of the CMake infastructure on the
# source branch that we directly maintain.

SET(EALIB_SOURCE_ROOT
   "${PROJECT_BINARY_DIR}../libs/ealib"
   CACHE PATH
   "Location of the ealib submodule"
   )


SET(BOOST_SOURCE_ROOT
   "${PROJECT_BINARY_DIR}../libs/boost"
   CACHE PATH
   "Location of the main boost submodule"
   )


