project(UQTk)

enable_language(Fortran)

SET(tools_HEADERS
  combin.h
  gq.h
  minmax.h
  multiindex.h
  pcmaps.h
  probability.h
  rosenblatt.h
  func.h
  tools.h
  )

FILE(GLOB slsrc "*.cpp")
FILE(GLOB fsrc  toolsf.f)

add_library(uqtktools ${fsrc} ${slsrc})

include_directories (../include)
include_directories (../array  )
include_directories (../pce)
include_directories (../quad)

include_directories (../../../dep/dsfmt )
target_link_libraries(uqtktools m lapack ${LAPACK_LIBRARIES})
include_directories (../../../dep/slatec )
include_directories (../../../dep/figtree)
include_directories (${CMAKE_SUNDIALS_DIR}/include)
if( BUILD_SUNDIALS)
  include_directories ("${PROJECT_BINARY_DIR}/../../../dep/sundials/include")
  include_directories (../../../dep/sundials/include )
endif()

# Install the library
INSTALL(TARGETS uqtktools DESTINATION lib)

# Install the header files
INSTALL(FILES ${tools_HEADERS} DESTINATION include/uqtk)
