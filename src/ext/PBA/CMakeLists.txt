if (CMAKE_SYSTEM_PROCESSOR MATCHES "^(arm.*|ARM.*)" OR "^(aarch64.*|AARCH64.*)")
  if(CMAKE_SYSTEM_PROCESSOR MATCHES "^(arm.*|ARM.*)")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC -O3 -pthread -march=arm")
  endif()
  if(CMAKE_SYSTEM_PROCESSOR MATCHES "^(aarch64.*|AARCH64.*)")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC -O3 -pthread -march=aarch64")
  endif()
endif()



if(CUDA_ENABLED)
    # Fix for Ubuntu 16.04.
    add_definitions("-D_FORCE_INLINES")

    set(PBA_GPU_SOURCE_FILES
        ConfigBA.cpp
        ConfigBA.h
        CuTexImage.cpp
        CuTexImage.h
        DataInterface.h
        pba.cpp
        pba.h
        ProgramCU.cu
        ProgramCU.h
        SparseBundleCPU.cpp
        SparseBundleCPU.h
        SparseBundleCU.cpp
        SparseBundleCU.h
        util.h)
    COLMAP_CUDA_ADD_LIBRARY(pba ${PBA_GPU_SOURCE_FILES})
else()
    set(PBA_CPU_SOURCE_FILES
        ConfigBA.cpp
        ConfigBA.h
        DataInterface.h
        pba.cpp
        pba.h
        SparseBundleCPU.cpp
        SparseBundleCPU.h
        util.h)
    COLMAP_ADD_LIBRARY(pba ${PBA_CPU_SOURCE_FILES})
    set_target_properties(pba PROPERTIES COMPILE_FLAGS "-DPBA_NO_GPU")
endif()
