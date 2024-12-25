set(TARGET_NAME CGALDemoApp)
find_package(CGAL REQUIRED COMPONENTS Qt6 Core)
find_package(Qt6 REQUIRED Core Gui ShaderTools Widgets)  
qt_standard_project_setup()


file(GLOB_RECURSE CPP_HEAD_FILES  ${CMAKE_CURRENT_SOURCE_DIR}/*.h)
file(GLOB_RECURSE CPP_SOUCE_FILES  ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)
# file(GLOB_RECURSE SHADER_FILES_ABS  ${CMAKE_CURRENT_SOURCE_DIR}/shaders/*)
# set(SHADER_FILES_REL "")
# foreach(SHADER_FILE_ABS ${SHADER_FILES_ABS})
#     file(RELATIVE_PATH SHADER_FILE_REL ${CMAKE_CURRENT_SOURCE_DIR} ${SHADER_FILE_ABS})
#     list(APPEND SHADER_FILES_REL ${SHADER_FILE_REL})
# endforeach()


source_group(TREE ${CMAKE_CURRENT_LIST_DIR} FILES ${CPP_HEAD_FILES} ${CPP_SOUCE_FILES})

qt_add_executable(${TARGET_NAME} ${CPP_HEAD_FILES} ${CPP_SOUCE_FILES})
set_target_properties(${TARGET_NAME} PROPERTIES FOLDER Apps)


target_link_libraries(${TARGET_NAME}
PUBLIC
Qt6::Widgets
Qt6::Gui
CGAL::CGAL_Basic_viewer
)

# qt_add_resources(${TARGET_NAME} "images"
#     PREFIX "/"
#     FILES qt256.png
# )

# qt_add_shaders(${TARGET_NAME} "shaders"
# GLSL "310es, 430"
# PREFIX
# "/"
# FILES
# ${SHADER_FILES_REL}
# )

qt_generate_deploy_app_script(
    TARGET ${TARGET_NAME}
    OUTPUT_SCRIPT deploy_script
    NO_UNSUPPORTED_PLATFORM_ERROR
)
install(SCRIPT ${deploy_script})