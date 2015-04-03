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


ADD_SUBDIRECTORY(libs/ealib)
ADD_SUBDIRECTORY(libs/boost)
ADD_SUBDIRECTORY(avida4-core)

# Default location for installed software/configs is the build directory
SET(CMAKE_INSTALL_PREFIX
   "${PROJECT_BINARY_DIR}"
   CACHE PATH
   "Install path prefix, prepended onto all install directories."
   FORCE
   )


