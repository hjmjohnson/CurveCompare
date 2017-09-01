cmake_minimum_required(VERSION 3.5)
 
project(CurveCompare)

find_package(GenerateCLP REQUIRED)
if(GenerateCLP_FOUND)
  include(${GenerateCLP_USE_FILE})
else()
  message(FATAL_ERROR
          "GenerateCLP not found. Please set GenerateCLP_DIR.")
endif()

find_package(ITK COMPONENTS
  ITKCommon
  ITKIOImageBase
  ITKImageAdaptors
  ITKImageFunction
  ITKImageStatistics
  ITKRegistrationCommon
  ITKSpatialObjects
  ITKTransform
  ${ITK_IO_MODULES_USED}
  REQUIRED
)
include(${ITK_USE_FILE})

find_package(VTK COMPONENTS
  vtkCommonComputationalGeometry
  vtkCommonCore
  vtkCommonDataModel
  vtkFiltersSources
  vtkIOLegacy
  vtkIOXML
  vtkInteractionWidgets
  vtkViewsInfovis
)
include(${VTK_USE_FILE})

if( ${ITK_VERSION_MAJOR} VERSION_LESS 4 )
  message( FATAL_ERROR "CurveCompare needs ITKv4 to compile" )
endif()

include_directories(${PROJECT_SOURCE_DIR})

set(src CurveCompare.cxx)
GENERATECLP(src CurveCompare.xml)
add_executable( CurveCompare ${src})

target_link_libraries( CurveCompare ${ITK_LIBRARIES} ${VTK_LIBRARIES})
