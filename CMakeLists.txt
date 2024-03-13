cmake_minimum_required(VERSION 3.16.0 FATAL_ERROR)

set(CMAKE_SYSTEM_VERSION 10.0 CACHE STRING "" FORCE)

project(H3_Astar_V2 CXX)

################################################################################
# Set target arch type if empty. Visual studio solution generator provides it.
################################################################################
if(NOT CMAKE_VS_PLATFORM_NAME)
    set(CMAKE_VS_PLATFORM_NAME "x64")
endif()
message("${CMAKE_VS_PLATFORM_NAME} architecture in use")

if(NOT ("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64"
     OR "${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86"))
    message(FATAL_ERROR "${CMAKE_VS_PLATFORM_NAME} arch is not supported!")
endif()

################################################################################
# Global configuration types
################################################################################
set(CMAKE_CONFIGURATION_TYPES
    "Debug"
    "Release"
    CACHE STRING "" FORCE
)

################################################################################
# Global compiler options
################################################################################
if(MSVC)
    # remove default flags provided with CMake for MSVC
    set(CMAKE_CXX_FLAGS "")
    set(CMAKE_CXX_FLAGS_DEBUG "")
    set(CMAKE_CXX_FLAGS_RELEASE "")
endif()

################################################################################
# Global linker options
################################################################################
if(MSVC)
    # remove default flags provided with CMake for MSVC
    set(CMAKE_EXE_LINKER_FLAGS "")
    set(CMAKE_MODULE_LINKER_FLAGS "")
    set(CMAKE_SHARED_LINKER_FLAGS "")
    set(CMAKE_STATIC_LINKER_FLAGS "")
    set(CMAKE_EXE_LINKER_FLAGS_DEBUG "${CMAKE_EXE_LINKER_FLAGS}")
    set(CMAKE_MODULE_LINKER_FLAGS_DEBUG "${CMAKE_MODULE_LINKER_FLAGS}")
    set(CMAKE_SHARED_LINKER_FLAGS_DEBUG "${CMAKE_SHARED_LINKER_FLAGS}")
    set(CMAKE_STATIC_LINKER_FLAGS_DEBUG "${CMAKE_STATIC_LINKER_FLAGS}")
    set(CMAKE_EXE_LINKER_FLAGS_RELEASE "${CMAKE_EXE_LINKER_FLAGS}")
    set(CMAKE_MODULE_LINKER_FLAGS_RELEASE "${CMAKE_MODULE_LINKER_FLAGS}")
    set(CMAKE_SHARED_LINKER_FLAGS_RELEASE "${CMAKE_SHARED_LINKER_FLAGS}")
    set(CMAKE_STATIC_LINKER_FLAGS_RELEASE "${CMAKE_STATIC_LINKER_FLAGS}")
endif()

################################################################################
# Nuget packages function stub.
################################################################################
function(use_package TARGET PACKAGE VERSION)
    message(WARNING "No implementation of use_package. Create yours. "
                    "Package \"${PACKAGE}\" with version \"${VERSION}\" "
                    "for target \"${TARGET}\" is ignored!")
endfunction()

################################################################################
# Common utils
################################################################################
include(CMake/Utils.cmake)

################################################################################
# Additional Global Settings(add specific info there)
################################################################################
include(CMake/GlobalSettingsInclude.cmake OPTIONAL)

################################################################################
# Use solution folders feature
################################################################################
set_property(GLOBAL PROPERTY USE_FOLDERS ON)

################################################################################
# Sub-projects
################################################################################



























set(PROJECT_NAME H3_Astar_V2DR)

################################################################################
# Source groups
################################################################################
set(no_group_source_files
    "h3.dll"
    "log.txt"
    "test.html"
    "多粒度.geojson"
)
source_group("" FILES ${no_group_source_files})

set(
    "Astar.h"
    "h3api.h"
    "include/pareto/archive.h"
    "include/pareto/boost_tree.h"
    "include/pareto/common/common.h"
    "include/pareto/common/default_allocator.h"
    "include/pareto/common/demangle.h"
    "include/pareto/common/hypervolume.h"
    "include/pareto/common/keywords.h"
    "include/pareto/common/metaprogramming.h"
    "include/pareto/common/operators.h"
    "include/pareto/front.h"
    "include/pareto/implicit_tree.h"
    "include/pareto/kd_tree.h"
    "include/pareto/matplot/archive.h"
    "include/pareto/matplot/front.h"
    "include/pareto/point.h"
    "include/pareto/quad_tree.h"
    "include/pareto/query/disjoint.h"
    "include/pareto/query/intersects.h"
    "include/pareto/query/nearest.h"
    "include/pareto/query/predicate_list.h"
    "include/pareto/query/predicate_variant.h"
    "include/pareto/query/predicates.h"
    "include/pareto/query/query_box.h"
    "include/pareto/query/satisfies.h"
    "include/pareto/query/within.h"
    "include/pareto/r_star_tree.h"
    "include/pareto/r_tree.h"
    "include/pareto/spatial_map.h"
    "Node.h"
    "resource.h"
    "Task.h"
    "threadPool.h"
    "type_def.h"
    "Util.h"
    "Vinoroi.h"
)
source_group("头文件" FILES ${})

set(__Multi_Object
    "Multi_Astar.h"
    "parameter.h"
    "Point.h"
)
source_group("头文件\\Multi_Object" FILES ${__Multi_Object})

set(
    "Astar.cpp"
    "Multi_Astar.cpp"
    "Start.cpp"
    "Util.cpp"
    "Vinoroi.cpp"
)
source_group("源文件" FILES ${})

set(ALL_FILES
    ${no_group_source_files}
    ${}
    ${__Multi_Object}
    ${}
)
set(src 
    "Astar.cpp"
    "Multi_Astar.cpp"
    "Start.cpp"
    "Util.cpp"
    "Vinoroi.cpp"
)

set(EXECUTABLE_OUTPUT_PATH ./)
# file(GLOB_RECURSE HEAD &{PROJECT_SOURCE_DIR}/*.h)
# include_directories(${PROJECT_SOURCE_DIR})
# include_directories(${PROJECT_SOURCE_DIR}/include)
# include_directories(${PROJECT_SOURCE_DIR}/include/pareto)
link_directories(${PROJECT_SOURCE_DIR}\\Python311\\libs)
link_directories(${PROJECT_SOURCE_DIR})
################################################################################
# Target
################################################################################
# add_executable(${PROJECT_NAME} ${ALL_FILES})
add_executable(${PROJECT_NAME} ${src})

use_props(${PROJECT_NAME} "${CMAKE_CONFIGURATION_TYPES}" "${DEFAULT_CXX_PROPS}")
set(ROOT_NAMESPACE H3AstarV2)

set_target_properties(${PROJECT_NAME} PROPERTIES
    VS_GLOBAL_KEYWORD "Win32Proj"
)
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        INTERPROCEDURAL_OPTIMIZATION_RELEASE "TRUE"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        INTERPROCEDURAL_OPTIMIZATION_RELEASE "TRUE"
    )
endif()
################################################################################
# Include directories
################################################################################
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    target_include_directories(${PROJECT_NAME} PUBLIC
        # "${CMAKE_CURRENT_SOURCE_DIR}/../Python311/include"
        # "${CMAKE_CURRENT_SOURCE_DIR}/../Python311/libs"
        "${PROJECT_SOURCE_DIR}\\Python311\\include"
        "${PROJECT_SOURCE_DIR}\\Python311\\libs"
        "${PROJECT_SOURCE_DIR}"
        "${PROJECT_SOURCE_DIR}/include"
        "${PROJECT_SOURCE_DIR}/include/pareto"
    )
endif()

################################################################################
# Compile definitions
################################################################################
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    target_compile_definitions(${PROJECT_NAME} PRIVATE
        "$<$<CONFIG:Debug>:"
            "_DEBUG;"
            "_CRT_SECURE_NO_WARNINGS"
        ">"
        "$<$<CONFIG:Release>:"
            "NDEBUG"
        ">"
        "_CONSOLE;"
        "UNICODE;"
        "_UNICODE"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    target_compile_definitions(${PROJECT_NAME} PRIVATE
        "$<$<CONFIG:Debug>:"
            "_DEBUG"
        ">"
        "$<$<CONFIG:Release>:"
            "NDEBUG"
        ">"
        "WIN32;"
        "_CONSOLE;"
        "UNICODE;"
        "_UNICODE"
    )
endif()

################################################################################
# Compile and link options
################################################################################
if(MSVC)
    if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
        target_compile_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /std:c++17
            >
            $<$<CONFIG:Release>:
                /Oi;
                /Gy
            >
            /permissive-;
            /sdl;
            /W3;
            ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT};
            ${DEFAULT_CXX_EXCEPTION_HANDLING}
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
        target_compile_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Release>:
                /Oi;
                /Gy
            >
            /permissive-;
            /sdl;
            /W3;
            ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT};
            ${DEFAULT_CXX_EXCEPTION_HANDLING}
        )
    endif()
    if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
        target_link_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /INCREMENTAL
            >
            $<$<CONFIG:Release>:
                /OPT:REF;
                /OPT:ICF;
                /INCREMENTAL:NO
            >
            /DEBUG;
            /SUBSYSTEM:CONSOLE
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
        target_link_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /INCREMENTAL
            >
            $<$<CONFIG:Release>:
                /OPT:REF;
                /OPT:ICF;
                /INCREMENTAL:NO
            >
            /DEBUG;
            /SUBSYSTEM:CONSOLE
        )
    endif()
endif()

################################################################################
# Dependencies
################################################################################
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    set(ADDITIONAL_LIBRARY_DEPENDENCIES
        "$<$<CONFIG:Debug>:"
            # "C:\\H3_Astar_V2\\h3.lib"
            "h3"
            "python311"
        ">"
        "$<$<CONFIG:Release>:"
            "h3"
            "python311_d"
        ">"
    )
endif()

target_link_libraries(${PROJECT_NAME} PRIVATE 
    "${ADDITIONAL_LIBRARY_DEPENDENCIES}"
)

