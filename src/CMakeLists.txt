CMAKE_MINIMUM_REQUIRED(VERSION 3.0.0)
CMAKE_POLICY(SET CMP0048 OLD)
PROJECT(qscintilla2)
SET(CMAKE_CXX_STANDARD 11)

FUNCTION(INSTALL_FILES_HIERARCHY)
  SET(options OPTIONAL)
  SET(multiValueArgs FILES)
  SET(oneValueArgs DESTINATION)

  CMAKE_PARSE_ARGUMENTS(INSTALL_FILES_HIERARCHY "${options}" "${oneValueArgs}" "${multiValueArgs}" ${ARGN})
  FOREACH(file ${INSTALL_FILES_HIERARCHY_FILES})
    GET_FILENAME_COMPONENT(dir ${file} DIRECTORY)
    INSTALL(FILES ${file} DESTINATION ${INSTALL_FILES_HIERARCHY_DESTINATION}/${dir})
  ENDFOREACH()
ENDFUNCTION()

SET(CMAKE_AUTOMOC ON)
FIND_PACKAGE(Qt6 COMPONENTS Core Gui Widgets LinguistTools)
#SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${Qt6Core_EXECUTABLE_COMPILE_FLAGS} ${Qt6Gui_EXECUTABLE_COMPILE_FLAGS} ${Qt6Widgets_EXECUTABLE_COMPILE_FLAGS}")
IF(Qt6_POSITION_INDEPENDENT_CODE)
  SET(CMAKE_POSITION_INDEPENDENT_CODE ON)
ENDIF(Qt6_POSITION_INDEPENDENT_CODE)
IF(CMAKE_SYSTEM_NAME MATCHES "Darwin")
  FIND_PACKAGE(Qt6 COMPONENTS MacExtras)
  SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${Qt6MacExtras_EXECUTABLE_COMPILE_FLAGS}")
ENDIF()
  
INCLUDE_DIRECTORIES(. ../scintilla/include ../scintilla/lexlib ../scintilla/src)
ADD_DEFINITIONS(-DSCINTILLA_QT -DSCI_LEXER -DFASTO)

# If the user did not customize the install prefix,
# set it to live under build so we don't inadvertently pollute /usr/local
IF(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
  SET(CMAKE_INSTALL_PREFIX "${CMAKE_BINARY_DIR}/install" CACHE PATH "default install path" FORCE)
ENDIF(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)

SET(HEADER_INCLUDE
  Qsci/qsciscintilla.h
  Qsci/qsciscintillabase.h
  Qsci/qsciabstractapis.h
  Qsci/qsciapis.h
  Qsci/qscilexer.h
  Qsci/qscilexercustom.h
  Qsci/qsciglobal.h
  Qsci/qscicommand.h
  Qsci/qscidocument.h
  Qsci/qscilexerjson.h
  Qsci/qscilexerxml.h
  Qsci/qscilexerhtml.h
  Qsci/qscilexerpython.h
  Qsci/qscilexerjavascript.h
  Qsci/qscilexercpp.h
)

SET(HEADERS
    #Qsci/qscilexerbash.h
    #Qsci/qscilexerbatch.h
    #Qsci/qscilexercmake.h
    #Qsci/qscilexercpp.h
    #Qsci/qscilexercsharp.h
    #Qsci/qscilexercss.h
    #Qsci/qscilexerd.h
    #Qsci/qscilexerdiff.h
    #Qsci/qscilexerfortran.h
    #Qsci/qscilexerfortran77.h
    #Qsci/qscilexeridl.h
    #Qsci/qscilexerjava.h
    #Qsci/qscilexerjavascript.h
    #Qsci/qscilexerlua.h
    #Qsci/qscilexermakefile.h
    #Qsci/qscilexermatlab.h
    #Qsci/qscilexeroctave.h
    #Qsci/qscilexerpascal.h
    #Qsci/qscilexerperl.h
    #Qsci/qscilexerpostscript.h
    #Qsci/qscilexerpov.h
    #Qsci/qscilexerproperties.h
    #Qsci/qscilexerpython.h
    #Qsci/qscilexerruby.h
    #Qsci/qscilexerspice.h
    #Qsci/qscilexersql.h
    #Qsci/qscilexertcl.h
    #Qsci/qscilexertex.h
    #Qsci/qscilexerverilog.h
    #Qsci/qscilexervhdl.h
    #Qsci/qscilexerxml.h
    #Qsci/qscilexerhtml.h
    #Qsci/qscilexeryaml.h
    #Qsci/qscimacro.h
    SciClasses.h
    SciAccessibility.h
    ScintillaQt.h
    ../scintilla/src/XPM.h
    Qsci/qsciglobal.h
    Qsci/qscicommand.h
    Qsci/qscicommandset.h
    Qsci/qscidocument.h
    Qsci/qsciprinter.h
    Qsci/qscistyle.h
    ../scintilla/src/ViewStyle.h
    Qsci/qscistyledtext.h
    ListBoxQt.h
    #SciNamespace.h    
    ../scintilla/include/ILexer.h
    ../scintilla/include/Platform.h
    ../scintilla/include/SciLexer.h
    ../scintilla/include/Scintilla.h
    ../scintilla/include/ScintillaWidget.h
    ../scintilla/src/UniConversion.h
    ../scintilla/lexlib/Accessor.h
    ../scintilla/lexlib/CharacterCategory.h
    ../scintilla/lexlib/CharacterSet.h
    ../scintilla/lexlib/LexAccessor.h
    ../scintilla/lexlib/LexerBase.h
    ../scintilla/lexlib/LexerModule.h
    ../scintilla/lexlib/LexerNoExceptions.h
    ../scintilla/lexlib/LexerSimple.h
    ../scintilla/lexlib/OptionSet.h
    #../scintilla/src/UnicodeFromUTF8.h
    ../scintilla/lexlib/PropSetSimple.h
    ../scintilla/lexlib/StyleContext.h
    ../scintilla/lexlib/SubStyles.h
    ../scintilla/lexlib/WordList.h
    ../scintilla/src/AutoComplete.h
    ../scintilla/src/CallTip.h
    ../scintilla/src/CaseConvert.h
    ../scintilla/src/CaseFolder.h
    ../scintilla/src/Catalogue.h
    ../scintilla/src/CellBuffer.h
    ../scintilla/src/CharClassify.h
    ../scintilla/src/ContractionState.h
    ../scintilla/src/Decoration.h
    ../scintilla/src/Document.h
    ../scintilla/src/Editor.h
    ../scintilla/src/EditView.h
    ../scintilla/src/EditModel.h
    ../scintilla/src/MarginView.h
    ../scintilla/src/ExternalLexer.h
    ../scintilla/src/FontQuality.h
    ../scintilla/src/Indicator.h
    ../scintilla/src/KeyMap.h
    ../scintilla/src/Style.h
    ../scintilla/src/LineMarker.h
    ../scintilla/src/Partitioning.h
    ../scintilla/src/PerLine.h
    ../scintilla/src/PositionCache.h
    ../scintilla/src/RESearch.h
    ../scintilla/src/RunStyles.h
    ../scintilla/src/ScintillaBase.h
    ../scintilla/src/Selection.h
    ../scintilla/src/SplitVector.h
)
SET(SOURCES
    qsciscintilla.cpp
    qsciscintillabase.cpp
    qsciabstractapis.cpp
    qsciapis.cpp
    qscicommand.cpp
    qscicommandset.cpp
    qscidocument.cpp
    qscilexer.cpp
    #qscilexerbash.cpp
    #qscilexerbatch.cpp
    #qscilexercmake.cpp
    qscilexercpp.cpp
    #qscilexercsharp.cpp
    #qscilexercss.cpp
    qscilexerjson.cpp
    qscilexerxml.cpp
    qscilexercustom.cpp
    #qscilexerd.cpp
    #qscilexerdiff.cpp
    #qscilexerfortran.cpp
    #qscilexerfortran77.cpp
    qscilexerhtml.cpp
    #qscilexeridl.cpp
    #qscilexerjava.cpp
    qscilexerjavascript.cpp
    #qscilexerlua.cpp
    #qscilexermakefile.cpp
    #qscilexermatlab.cpp
    #qscilexeroctave.cpp
    #qscilexerpascal.cpp
    #qscilexerperl.cpp
    #qscilexerpostscript.cpp
    #qscilexerpov.cpp
    #qscilexerproperties.cpp
    qscilexerpython.cpp
    #qscilexerruby.cpp
    #qscilexerspice.cpp
    #qscilexersql.cpp
    #qscilexertcl.cpp
    #qscilexertex.cpp
    #qscilexerverilog.cpp
    #qscilexervhdl.cpp
    #qscilexerxml.cpp
    #qscilexeryaml.cpp
    #qscimacro.cpp
    #qsciprinter.cpp
    qscistyle.cpp
    qscistyledtext.cpp
    MacPasteboardMime.cpp
    InputMethod.cpp
    SciClasses.cpp
    SciAccessibility.cpp
    ListBoxQt.cpp
    PlatQt.cpp
    ScintillaQt.cpp
    ../scintilla/lexers/LexA68k.cpp
    ../scintilla/lexers/LexAbaqus.cpp
    ../scintilla/lexers/LexAda.cpp
    ../scintilla/lexers/LexAPDL.cpp
    ../scintilla/lexers/LexAsm.cpp
    ../scintilla/lexers/LexAsn1.cpp
    ../scintilla/lexers/LexASY.cpp
    ../scintilla/lexers/LexAU3.cpp
    ../scintilla/lexers/LexAVE.cpp
    ../scintilla/lexers/LexAVS.cpp
    ../scintilla/lexers/LexBaan.cpp
    ../scintilla/lexers/LexBash.cpp
    ../scintilla/lexers/LexBasic.cpp
    ../scintilla/lexers/LexBatch.cpp
    ../scintilla/lexers/LexBullant.cpp
    ../scintilla/lexers/LexCaml.cpp
    ../scintilla/lexers/LexCLW.cpp
    ../scintilla/lexers/LexCmake.cpp
    ../scintilla/lexers/LexCOBOL.cpp
    ../scintilla/lexers/LexCoffeeScript.cpp
    ../scintilla/lexers/LexConf.cpp
    ../scintilla/lexers/LexCPP.cpp
    ../scintilla/lexers/LexCrontab.cpp
    ../scintilla/lexers/LexCsound.cpp
    ../scintilla/lexers/LexCSS.cpp
    ../scintilla/lexers/LexD.cpp
    ../scintilla/lexers/LexDiff.cpp
    ../scintilla/lexers/LexECL.cpp
    ../scintilla/lexers/LexEiffel.cpp
    ../scintilla/lexers/LexErlang.cpp
    ../scintilla/lexers/LexErrorList.cpp
    ../scintilla/lexers/LexEScript.cpp
    ../scintilla/lexers/LexFlagship.cpp
    ../scintilla/lexers/LexForth.cpp
    ../scintilla/lexers/LexFortran.cpp
    ../scintilla/lexers/LexGAP.cpp
    ../scintilla/lexers/LexGui4Cli.cpp
    ../scintilla/lexers/LexHaskell.cpp
    ../scintilla/lexers/LexHTML.cpp
    ../scintilla/lexers/LexInno.cpp
    ../scintilla/lexers/LexKix.cpp
    ../scintilla/lexers/LexKVIrc.cpp
    ../scintilla/lexers/LexLaTeX.cpp
    ../scintilla/lexers/LexLisp.cpp
    ../scintilla/lexers/LexLout.cpp
    ../scintilla/lexers/LexLua.cpp
    ../scintilla/lexers/LexMagik.cpp
    ../scintilla/lexers/LexMake.cpp
    ../scintilla/lexers/LexMarkdown.cpp
    ../scintilla/lexers/LexMatlab.cpp
    ../scintilla/lexers/LexMetapost.cpp
    ../scintilla/lexers/LexMMIXAL.cpp
    ../scintilla/lexers/LexModula.cpp
    ../scintilla/lexers/LexMPT.cpp
    ../scintilla/lexers/LexMSSQL.cpp
    ../scintilla/lexers/LexMySQL.cpp
    ../scintilla/lexers/LexNimrod.cpp
    ../scintilla/lexers/LexNsis.cpp
    ../scintilla/lexers/LexNull.cpp
    ../scintilla/lexers/LexOpal.cpp
    ../scintilla/lexers/LexOScript.cpp
    #..scintilla//lexers/LexOthers.cpp
    ../scintilla/lexers/LexPascal.cpp
    ../scintilla/lexers/LexPB.cpp
    ../scintilla/lexers/LexPerl.cpp
    ../scintilla/lexers/LexPLM.cpp
    ../scintilla/lexers/LexPO.cpp
    ../scintilla/lexers/LexPOV.cpp
    ../scintilla/lexers/LexPowerPro.cpp
    ../scintilla/lexers/LexPowerShell.cpp
    ../scintilla/lexers/LexProgress.cpp
    ../scintilla/lexers/LexProps.cpp
    ../scintilla/lexers/LexPS.cpp
    ../scintilla/lexers/LexPython.cpp
    ../scintilla/lexers/LexR.cpp
    ../scintilla/lexers/LexRebol.cpp
    ../scintilla/lexers/LexRuby.cpp
    ../scintilla/lexers/LexRust.cpp
    ../scintilla/lexers/LexScriptol.cpp
    ../scintilla/lexers/LexSmalltalk.cpp
    ../scintilla/lexers/LexSML.cpp
    ../scintilla/lexers/LexSorcus.cpp
    ../scintilla/lexers/LexSpecman.cpp
    ../scintilla/lexers/LexSpice.cpp
    ../scintilla/lexers/LexSQL.cpp
    ../scintilla/lexers/LexSTTXT.cpp
    ../scintilla/lexers/LexTACL.cpp
    ../scintilla/lexers/LexTADS3.cpp
    ../scintilla/lexers/LexTAL.cpp
    ../scintilla/lexers/LexTCL.cpp
    ../scintilla/lexers/LexTCMD.cpp
    ../scintilla/lexers/LexTeX.cpp
    ../scintilla/lexers/LexTxt2tags.cpp
    ../scintilla/lexers/LexVB.cpp
    ../scintilla/lexers/LexVerilog.cpp
    ../scintilla/lexers/LexVHDL.cpp
    ../scintilla/lexers/LexVisualProlog.cpp
    ../scintilla/lexers/LexYAML.cpp
    ../scintilla/lexers/LexDMIS.cpp
    ../scintilla/lexers/LexHex.cpp
    ../scintilla/lexers/LexRegistry.cpp
    ../scintilla/lexers/LexDMAP.cpp
    ../scintilla/lexers/LexJSON.cpp
    ../scintilla/lexers/LexEDIFACT.cpp
    ../scintilla/lexlib/Accessor.cpp
    ../scintilla/lexlib/CharacterCategory.cpp
    ../scintilla/lexlib/CharacterSet.cpp
    ../scintilla/lexlib/LexerBase.cpp
    ../scintilla/lexlib/LexerModule.cpp
    ../scintilla/lexlib/LexerNoExceptions.cpp
    ../scintilla/lexlib/LexerSimple.cpp
    ../scintilla/lexlib/PropSetSimple.cpp
    ../scintilla/lexlib/StyleContext.cpp
    ../scintilla/lexlib/WordList.cpp
    ../scintilla/lexers/LexBibTeX.cpp
    ../scintilla/src/AutoComplete.cpp
    ../scintilla/src/CallTip.cpp
    ../scintilla/src/CaseConvert.cpp
    ../scintilla/src/CaseFolder.cpp
    ../scintilla/src/Catalogue.cpp
    ../scintilla/src/CellBuffer.cpp
    ../scintilla/src/CharClassify.cpp
    ../scintilla/src/ContractionState.cpp
    ../scintilla/src/Decoration.cpp
    ../scintilla/src/Document.cpp
    ../scintilla/src/Editor.cpp
    ../scintilla/src/EditView.cpp
    ../scintilla/src/EditModel.cpp
    ../scintilla/src/MarginView.cpp
    ../scintilla/src/ExternalLexer.cpp
    ../scintilla/src/Indicator.cpp
    ../scintilla/src/KeyMap.cpp
    ../scintilla/src/LineMarker.cpp
    ../scintilla/src/PerLine.cpp
    ../scintilla/src/PositionCache.cpp
    ../scintilla/src/RESearch.cpp
    ../scintilla/src/RunStyles.cpp
    ../scintilla/src/ScintillaBase.cpp
    ../scintilla/src/Selection.cpp
    ../scintilla/src/Style.cpp
    ../scintilla/src/UniConversion.cpp
    ../scintilla/src/ViewStyle.cpp
    ../scintilla/src/XPM.cpp
)
SOURCE_GROUP(sources FILES ${HEADERS} ${HEADER_INCLUDE} ${SOURCES})
SET(TS_FILES qscintilla_cs.ts qscintilla_de.ts qscintilla_es.ts qscintilla_fr.ts qscintilla_pt_br.ts)
QT_ADD_TRANSLATION(QM_FILES ${TS_FILES})
SOURCE_GROUP("translations" FILES ${TS_FILES})
SOURCE_GROUP("qm-files" FILES ${QM_FILES})

ADD_LIBRARY(${PROJECT_NAME} STATIC ${HEADERS} ${HEADER_INCLUDE} ${SOURCES} ${QM_FILES})
TARGET_LINK_LIBRARIES(${PROJECT_NAME} ${Qt6Core_LIBRARIES} ${Qt6Gui_LIBRARIES} ${Qt6Widgets_LIBRARIES} ${Qt6MacExtras_LIBRARIES})

SET(TARGET_INSTALL_DESTINATION lib)
SET(HEADERS_INSTALL_DESTINATION include)

INSTALL(TARGETS ${PROJECT_NAME} DESTINATION ${TARGET_INSTALL_DESTINATION} COMPONENT APPLICATIONS)
INSTALL_FILES_HIERARCHY(FILES ${HEADER_INCLUDE} DESTINATION ${HEADERS_INSTALL_DESTINATION})
