file(GLOB PUBLIC_HEADERS "freetype/include/ft2build.h" "freetype/include/freetype/*.h")
file(GLOB PUBLIC_CONFIG_HEADERS "freetype/include/freetype/config/*.h")
file(GLOB PRIVATE_HEADERS "freetype/include/freetype/internal/*.h")

add_library(freetype
  ${PUBLIC_HEADERS}
  ${PUBLIC_CONFIG_HEADERS}
  ${PRIVATE_HEADERS}
  freetype/src/autofit/autofit.c
  freetype/src/base/ftbase.c
  freetype/src/base/ftbbox.c
  freetype/src/base/ftbdf.c
  freetype/src/base/ftbitmap.c
  freetype/src/base/ftcid.c
  freetype/src/base/ftdebug.c
  freetype/src/base/ftfstype.c
  freetype/src/base/ftgasp.c
  freetype/src/base/ftglyph.c
  freetype/src/base/ftgxval.c
  freetype/src/base/ftinit.c
  freetype/src/base/ftmm.c
  freetype/src/base/ftotval.c
  freetype/src/base/ftpatent.c
  freetype/src/base/ftpfr.c
  freetype/src/base/ftstroke.c
  freetype/src/base/ftsynth.c
  freetype/src/base/ftsystem.c
  freetype/src/base/fttype1.c
  freetype/src/base/ftwinfnt.c
  freetype/src/bdf/bdf.c
  freetype/src/bzip2/ftbzip2.c
  freetype/src/cache/ftcache.c
  freetype/src/cff/cff.c
  freetype/src/cid/type1cid.c
  freetype/src/gzip/ftgzip.c
  freetype/src/lzw/ftlzw.c
  freetype/src/pcf/pcf.c
  freetype/src/pfr/pfr.c
  freetype/src/psaux/psaux.c
  freetype/src/pshinter/pshinter.c
  freetype/src/psnames/psnames.c
  freetype/src/raster/raster.c
  freetype/src/sdf/sdf.c
  freetype/src/sfnt/sfnt.c
  freetype/src/smooth/smooth.c
  freetype/src/truetype/truetype.c
  freetype/src/type1/type1.c
  freetype/src/type42/type42.c
  freetype/src/winfonts/winfnt.c
)
target_compile_definitions(freetype PRIVATE FT2_BUILD_LIBRARY)
target_include_directories(freetype PRIVATE ${CMAKE_CURRENT_BINARY_DIR}/freetype/include ${CMAKE_CURRENT_SOURCE_DIR}/freetype/include)

file(GLOB_RECURSE MSDFGEN_CORE_HEADERS RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} "core/*.h" "core/*.hpp" "ext/*.h" "ext/*.hpp")
file(GLOB_RECURSE MSDFGEN_CORE_SOURCES RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} "core/*.cpp" "ext/*.cpp" "lib/*.cpp")
add_library(msdfgen "${CMAKE_CURRENT_SOURCE_DIR}/msdfgen.h" ${MSDFGEN_CORE_HEADERS} ${MSDFGEN_CORE_SOURCES})
set_target_properties(msdfgen PROPERTIES PUBLIC_HEADER "${MSDFGEN_CORE_HEADERS}")
target_include_directories(msdfgen PUBLIC "freetype/include" "include")
target_link_libraries(msdfgen freetype)
