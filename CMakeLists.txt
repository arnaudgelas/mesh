project( mesh )

cmake_minimum_required( VERSION 2.6 )

set( mesh_VERSION 1.3 )

find_package( Qt3 REQUIRED )
find_package( X11 )
find_package( OpenGL )

set( cxx_srcs
Basic3DViewerWidget.cpp
ColorMapWidget.cpp
Error3DViewerWidget.cpp
InitWidget.cpp
Lighted3DViewerWidget.cpp
mesh.cpp
ScreenWidget.cpp
TextWidget.cpp
)

set( moc_srcs
Basic3DViewerWidget.h
Lighted3DViewerWidget.h
Error3DViewerWidget.h
ScreenWidget.h
InitWidget.h
ColorMapWidget.h
)

set( c_srcs
colormap.c
compute_error.c
mesh_run.c
model_analysis.c
reporting.c
xalloc.c
lib3d/src/geomutils.c
lib3d/src/model_in.c
lib3d/src/model_in_raw.c
lib3d/src/model_in_smf.c
lib3d/src/model_in_ply.c
lib3d/src/model_in_vrml_iv.c
lib3d/src/model_in_off.c
lib3d/src/block_list.c
)

add_definitions( ${QT_DEFINITIONS} )

include_directories(
  ${CMAKE_CURRENT_SOURCE_DIR}
  ${CMAKE_CURRENT_SOURCE_DIR}/lib3d/include
  ${CMAKE_CURRENT_BINARY_DIR}
  ${QT_INCLUDE_DIR}
  ${X11_INCLUDE_DIR}
)

qt_wrap_cpp( mesh moc_cxx ${moc_srcs} )

add_executable( mesh ${cxx_srcs} ${moc_cxx} ${c_srcs} )
target_link_libraries( mesh ${QT_LIBRARIES} ${X11_LIBRARIES} ${OPENGL_LIBRARIES} )
