cmake_minimum_required(VERSION 3.3)

project(TSP)

find_package(SCIP REQUIRED)
include_directories(${SCIP_INCLUDE_DIRS})

add_executable(sciptsp
   src/ConshdlrSubtour.cpp
   src/cppmain.cpp
   src/EventhdlrNewSol.cpp
   src/GomoryHuTree.cpp
   src/Heur2opt.cpp
   src/HeurFarthestInsert.cpp
   src/HeurFrats.cpp
   src/ProbDataTSP.cpp
   src/ReaderTSP.cpp
   src/gzstream.cpp)

target_link_libraries(sciptsp ${SCIP_LIBRARIES})

find_package(ZLIB)
if(ZLIB_FOUND)
   target_link_libraries(sciptsp ${ZLIB_LIBRARIES})
endif()

if( TARGET examples )
    add_dependencies( examples sciptsp )
endif()

add_subdirectory(check)
enable_testing()
