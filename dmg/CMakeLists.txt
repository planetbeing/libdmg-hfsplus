INCLUDE(FindZLIB)

IF(NOT ZLIB_FOUND)
	message(FATAL_ERROR "zlib is required for dmg!")
ENDIF(NOT ZLIB_FOUND)

include_directories(${ZLIB_INCLUDE_DIR})
link_directories(${ZLIB_LIBRARIES})

link_directories(${PROJECT_BINARY_DIR}/common ${PROJECT_BINARY_DIR}/hfs)

add_library(dmg adc.c base64.c checksum.c dmgfile.c dmglib.c filevault.c io.c partition.c resources.c udif.c)

target_link_libraries(dmg common hfs z)

add_executable(dmg-bin dmg.c)
target_link_libraries (dmg-bin dmg)

set_target_properties(dmg-bin PROPERTIES OUTPUT_NAME "dmg")

install(TARGETS dmg-bin DESTINATION .)

