cmake_minimum_required(VERSION 3.5)
 
PROJECT(CurveCompare)

FIND_PACKAGE(GenerateCLP REQUIRED)
IF(GenerateCLP_FOUND)
  INCLUDE(${GenerateCLP_USE_FILE})
ELSE(GenerateCLP_FOUND)
  MESSAGE(FATAL_ERROR
          "GenerateCLP not found. Please set GenerateCLP_DIR.")
ENDIF(GenerateCLP_FOUND)

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

SET(src CurveCompare.cxx)
GENERATECLP(src CurveCompare.xml)
ADD_EXECUTABLE( CurveCompare ${src})

TARGET_LINK_LIBRARIES( CurveCompare ${ITK_LIBRARIES} ${VTK_LIBRARIES})
