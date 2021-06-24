```makefile
# must!
cmake_minimum_required(VERSION 3.x)
# must!
project($projectname)

# attention! if change cmakelist, build dir (cache dir) should be del

# add sourcefile
add_executable($execname $srcdir/sourcefilename;$another)
add_executable($execname 
  $sourcefilename
  $another
)

# config variable in cmake
project($projname VERSION 1.0)
# ep: define in t.h
# t.h
# #define a @$projname_VERSION_MAJOR@ 
configure_file(t.h.in t.h)
# above -> a binary willbe created
# add binary
target_include_directories($execname PUBLIC
                            ${PROJECT_BINARY_DIR})
# above -> during compile, @var@ will be repalced by var in CMAEK

# expilict c++ shandard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# build and link
mkdir build
cd build
cmake ../
cmake --build

# add a lib in a subdir
# in subdir, new a cmakelist.txt and input -> below
add_library($libname $libsrcname.cpp)
# in main cmakelist
# add dir to tree, add include
add_subdirectory($subdirname)
target_include_directories($projname PUBLIC ${PROJECT_SOURCE_DIR}/$subdirname)

# tips！
# all the variable can be "/path" /path ${var} "${var}"
# but message("xxx") message("${car}")

# macro to use a lib
option(USE_MYMATH "Use tutorial provided math implementation" ON)
if(USE_MYMATH)
  add_subdirectory(MathFunctions)
  list(APPEND EXTRA_LIBS MathFunctions)
  list(APPEND EXTRA_INCLUDES "${PROJECT_SOURCE_DIR}/MathFunctions")
endif()
# same in .h
# ifdef USE_MYMATH
#   include "MathFunctions.h"
# endif
# same in .h.in
# cmakedefine USE_MYMATH
# use "cmake ../ -DUSE_MYMATH=OFF"

# if there is a lib in proj, before lib been built,
# main source can't be built
# add -->> "depend" <<-- relation

# find a 3rdparty package
# if pack is a office pack, no need to set $packname_DIR to find packconfig.cmake 
set($packname_DIR /path/to/config.cmake)
# MODULE: declare module to find; REQUIRED: find pack and its dependence
find_package($packname MODULE
  $modname
  REQUIRED)

# add include path for proj
add_include_directories($projname
  subdir/include/
  ${pack_INCLUDE_DIRS}
  /usr/include/)

# use link_directories to indicate path to find lib, if can't find lib in target_link_libraries
# but do recommand to use it
link_directories(/path/to/lib)

# link static and dynatic lib
target_link_libraries($execname 
  ${pack_LIBRARIES}
  # if conflict happens, solve and note here
  /path/to/.so
  # if .a need to link .a, and depended lib should behind lib which depend it
  # usually, difficult to arrange them, use -Wl group
  # use group can also indicate which .a to link .a, to avoid version conflict
  -Wl,-start-group
  /path/to/.a
  -Wl,--end-group
  # if use link_directories
  .a/.so)

# attention! Boost lib version is very important!
# avoid boost lib ver conflict! and pay attention to lib deps on boost! Symbol conflict in compile, lib load problem in runtime!

# add compile options
add_compile_options(-std=c++11)
## or
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fpic")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fpic")

#add link options
add_link_options(-pg)	# gprof, to generate gmon.out

set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -std=c++11 ")
# this means add -std=c++11 to CMAKE_CXX_FLAGS_RELEASE.

```
