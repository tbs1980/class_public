cmake_minimum_required(VERSION 2.8)
project(class C)

# guard against in-source builds (got this from Eigen)
if(${CMAKE_SOURCE_DIR} STREQUAL ${CMAKE_BINARY_DIR})
  message(FATAL_ERROR "In-source builds not allowed. Please make a new directory (called a build directory) and run CMake from there. You may need to remove CMakeCache.txt. ")
endif()

if(UNIX)
	if(CMAKE_COMPILER_IS_GNUCC)
		set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -std=gnu99 -pedantic -Wall -Wextra -Wfatal-errors -g -fPIC")
		set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -std=gnu99 -O3 -ffast-math -fPIC -march=native")
		set(CMAKE_C_FLAGS ${CMAKE_C_FLAGS_RELEASE})
	#is the compiler clang?
	elseif ("${CMAKE_C_COMPILER_ID}" STREQUAL "Clang")
		set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -std=gnu99 -pedantic -Wall -Wextra -g -fPIC ")
		set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -std=gnu99 -O3 -march=native -fPIC ")
		set(CMAKE_C_FLAGS ${CMAKE_C_FLAGS_RELEASE})
	elseif("${CMAKE_C_COMPILER_ID}" STREQUAL "Intel")
		set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -std=gnu99 -pedantic -w3 -g -fpic")
		set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -std=gnu99 -O3 -openmp -fpic")
		set(CMAKE_C_FLAGS ${CMAKE_C_FLAGS_RELEASE})
	endif()
endif(UNIX)

ADD_DEFINITIONS(-D__CLASSDIR__="${CMAKE_CURRENT_SOURCE_DIR}")

find_package(OpenMP)

set(EXTERNAL_DIR "${CMAKE_SOURCE_DIR}/hyrec")
set(TOOLS_DIR "${CMAKE_SOURCE_DIR}/tools")
set(SOURCE_DIR "${CMAKE_SOURCE_DIR}/source")
set(MAIN_DIR "${CMAKE_SOURCE_DIR}/main")

set(TOOLS 
	${TOOLS_DIR}/growTable.c 
	${TOOLS_DIR}/dei_rkck.c 
	${TOOLS_DIR}/sparse.c 
	${TOOLS_DIR}/evolver_rkck.c  
	${TOOLS_DIR}/evolver_ndf15.c 
	${TOOLS_DIR}/arrays.c 
	${TOOLS_DIR}/parser.c 
	${TOOLS_DIR}/quadrature.c 
	${TOOLS_DIR}/hyperspherical.c 
	${TOOLS_DIR}/common.c)

set(SOURCE 
	${SOURCE_DIR}/input.c 
	${SOURCE_DIR}/background.c 
	${SOURCE_DIR}/thermodynamics.c 
	${SOURCE_DIR}/perturbations.c 
	${SOURCE_DIR}/primordial.c 
	${SOURCE_DIR}/nonlinear.c 
	${SOURCE_DIR}/transfer.c 
	${SOURCE_DIR}/spectra.c 
	${SOURCE_DIR}/lensing.c)

set(EXTERNAL 
	${EXTERNAL_DIR}/hyrectools.c 
	${EXTERNAL_DIR}/helium.c 
	${EXTERNAL_DIR}/hydrogen.c 
	${EXTERNAL_DIR}/history.c)

set(OUTPUT ${SOURCE_DIR}/output.c)

set(CLASS_MAIN ${MAIN_DIR}/class.c)

include_directories(${CMAKE_SOURCE_DIR}/include)

add_library(class ${TOOLS} ${SOURCE} ${EXTERNAL})

# CMAKE DOES NOT ALLOW DUPLICATE TARGETS
# WE HAVE ALREADY DEFINED CLASS FOR THE LIBRARY
# A SIMPLE WORK AROUND IS TO CREATE CLASS.EXE AND
# THEN SET THE TARGET OUTPUT NAME AS CLASS
add_executable(class.exe  ${TOOLS} ${SOURCE} ${EXTERNAL} ${OUTPUT} ${CLASS_MAIN})
set_target_properties(class.exe PROPERTIES OUTPUT_NAME "class")
# link against libm
target_link_libraries(class.exe m)

