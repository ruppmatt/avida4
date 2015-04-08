include(ExternalProject)

PROJECT(avida4)

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


#ADD_SUBDIRECTORY(avida4-core)

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

SET(EXTERNAL_LIBRARY_OUTPUT_PATH
   ${PROJECT_BINARY_DIR}
   )

get_filename_component(BOOST_SRC_ROOT "libs/boost" ABSOLUTE)


# These have to be manually synchrnoized with the Boost
# libraries required to build ealib.  Presently, these
# libraries are located:
# libs/ealib/libea/Jamfile
# which is the Jamfile.v2 used by the b2 build system.
SET(EALIB_BOOST_LIBRARIES
   serialization
   iostreams
   regex
   system
   filesystem
   program_options
   )

# Now convert our list into a comma separated string for boost's 
# configuration (bootstrap) step
string(REPLACE ";" "," WITH_BOOST_LIBS "${EALIB_BOOST_LIBRARIES}")

ExternalProject_Add(local_boost
   SOURCE_DIR ../libs/boost
   CONFIGURE_COMMAND cd ${BOOST_SRC_ROOT} && pwd && ./bootstrap.sh 
      --prefix=${EXTERNAL_LIBRARY_OUTPUT_PATH} 
      --with-libraries=${WITH_BOOST_LIBS}
   BUILD_COMMAND cd ${BOOST_SRC_ROOT} && ./b2 headers && ./b2 link=static 
   INSTALL_COMMAND cd ${BOOST_SRC_ROOT} && ./b2 install
)


