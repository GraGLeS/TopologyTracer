#to compile the TopologyTracer which handles binary microstructure snapshots with MPI I/O
cmake_minimum_required(VERSION 2.6)
project(topotracer2d3d_intel16)

set(CMAKE_BUILD_DIR "build")

set ( CMAKE_CXX_FLAGS -O3 ) 
#set ( CMAKE_C_FLAGS -00 ) 

#utlizing C-style fseek functionality on 64bit architecture for files larger than 2^32 byte?
#compile with option -D_FILE_OFFSET_BITS=64

#ADD_LIBRARY(jasonevansmalloc3 STATIC IMPORTED)
#SET_TARGET_PROPERTIES(jasonevansmalloc3 PROPERTIES IMPORTED_LOCATION /home/mk958655/2016TopologyTracer2D3D/src/libjemalloc.a)


find_package(MPI REQUIRED)
include_directories(${MPI_INCLUDE_PATH})
add_executable(topotracer2d3d_intel16
			../src/allocator.cpp
			../src/TopologyTracer2D3D_Settings.cpp
			../src/TopologyTracer2D3D_Math.cpp
#			../src/TopologyTracer2D3D_Snapshot.cpp
			../src/TopologyTracer2D3D_Topohdl.cpp
			../src/TopologyTracer2D3D_Main.cpp
#			allocator.cpp
#			TopologyTracer2D3D_Settings.cpp
#			TopologyTracer2D3D_Iohdl.cpp
#			TopologyTracer2D3D_Main.cpp
)

ADD_DEFINITIONS("-std=c++0x")

#target_link_libraries(topotracer2d3d_intel16 -lpthread -lm -lnuma jasonevansmalloc3 ${MPI_LIBRARIES} ) #-lm
##currently not working to link J.Malloc be
##Linking CXX executable topotracer2d3d_intel16
##../src/libjemalloc.a(jemalloc.o): In function `malloc_init_hard_recursible':
##/rwthfs/rz/cluster/home/mk958655/2016TopologyTracer2D3D/jemalloc/jemalloc-4.2.1/src/jemalloc.c:1339: undefined reference to `pthread_atfork'
##make[2]: *** [topotracer2d3d_intel16] Error 1
##make[1]: *** [CMakeFiles/topotracer2d3d_intel16.dir/all] Error 2
##make: *** [all] Error 2


target_link_libraries(topotracer2d3d_intel16 -lm -lnuma ${MPI_LIBRARIES} ) #-ljemalloc 


if(MPI_COMPILE_FLAGS)
  set_target_properties(topotracer2d3d_intel16 PROPERTIES
    COMPILE_FLAGS "${MPI_COMPILE_FLAGS}")
endif()

if(MPI_LINK_FLAGS)
  set_target_properties(topotracer2d3d_intel16 PROPERTIES
    LINK_FLAGS "${MPI_LINK_FLAGS}")
endif()
