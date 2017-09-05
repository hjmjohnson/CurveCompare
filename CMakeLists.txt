cmake_minimum_required(VERSION 3.5)
 
project(CurveCompare)

find_package(SlicerExecutionModel REQUIRED)
include(${SlicerExecutionModel_USE_FILE})

find_package(ITK 4 REQUIRED COMPONENTS
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

if(NOT VTK_RENDERING_BACKEND)
  set(VTK_RENDERING_BACKEND OpenGL)
endif()
find_package(VTK REQUIRED COMPONENTS
  vtkCommonComputationalGeometry
  vtkCommonCore
  vtkCommonDataModel
  vtkFiltersSources
  vtkIOLegacy
  vtkIOXML
  vtkInteractionWidgets
  vtkRendering${VTK_RENDERING_BACKEND}
  vtkViewsInfovis
)
include(${VTK_USE_FILE})

SEMMacroBuildCLI(
  NAME CurveCompare
  TARGET_LIBRARIES ${ITK_LIBRARIES} ${VTK_LIBRARIES}
  EXECUTABLE_ONLY
  )

