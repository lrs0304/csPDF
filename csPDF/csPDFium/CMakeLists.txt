### Project ##################################################################

set(csPDFium_HEADERS
  include/csPDFium/csPDFium.h
  include/csPDFium/csPDFiumContentsModel.h
  include/csPDFium/csPDFiumContentsNode.h
  include/csPDFium/csPDFiumDest.h
  include/csPDFium/csPDFiumDocument.h
  include/csPDFium/csPDFiumLink.h
  include/csPDFium/csPDFiumPage.h
  include/csPDFium/csPDFiumText.h
  include/csPDFium/csPDFiumTextPage.h
  include/csPDFium/csPDFiumUtil.h
  include/csPDFium/cspdfium_config.h
  include/internal/csPDFiumDocumentImpl.h
  include/internal/csPDFiumPageImpl.h
  include/internal/fpdf_util.h
  )

set(csPDFium_SOURCES
  src/csPDFium.cpp
  src/csPDFiumContentsModel.cpp
  src/csPDFiumContentsNode.cpp
  src/csPDFiumDocument.cpp
  src/csPDFiumPage.cpp
  src/util_contents.cpp
  src/util_page.cpp
  src/util_paths.cpp
  src/util_text.cpp
  )

### Target ###################################################################

add_library(csPDFium SHARED
  ${csPDFium_HEADERS} ${csPDFium_SOURCES}
  )

format_output_name(csPDFium "csPDFium")

set_target_properties(csPDFium PROPERTIES
  AUTOMOC ON
  )

target_compile_definitions(csPDFium
  PRIVATE CS_BUILD_PDFIUM_LIB
  )

target_include_directories(csPDFium
  PUBLIC  ${CMAKE_CURRENT_SOURCE_DIR}/include
  PRIVATE ${pdfium_INCLUDES}
  )

target_link_libraries(csPDFium
  PRIVATE PDFium
  PUBLIC  Qt5::Widgets
  )

### Install ##################################################################

install(TARGETS csPDFium
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
  )

install(DIRECTORY include/
  DESTINATION include
  PATTERN "internal" EXCLUDE
  )
