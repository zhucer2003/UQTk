project(UQTk)

SET(gproc_HEADERS
  gproc.h
  )

add_library(uqtkgproc gproc.cpp)

include_directories (../include)
include_directories (../array  )
include_directories (../tools  )
include_directories (../quad   )
include_directories (../pce    )
include_directories (../bcs    )

target_link_libraries(uqtkgproc blas lapack)
include_directories (../../../dep/lbfgs)
include_directories (../../../dep/dsfmt)
include_directories (../../../dep/figtree)
include_directories (${CMAKE_SUNDIALS_DIR}/include)
if( BUILD_SUNDIALS)
  include_directories ("${PROJECT_BINARY_DIR}/../../../dep/sundials/include")
  include_directories (../../../dep/sundials/include )
endif()

# Install the library
INSTALL(TARGETS uqtkgproc DESTINATION lib)

# Install the header files
INSTALL(FILES ${gproc_HEADERS} DESTINATION include/uqtk)
