# Builds the uisupport module

if(WITH_QT5)
  setup_qt_variables(Widgets Network)
else(WITH_QT5)
  setup_qt_variables(Gui Network)
endif(WITH_QT5)

set(SOURCES
    abstractbuffercontainer.cpp
    abstractitemview.cpp
    abstractnotificationbackend.cpp
    action.cpp
    actioncollection.cpp
    bufferhotlistfilter.cpp
    bufferview.cpp
    bufferviewfilter.cpp
    bufferviewoverlayfilter.cpp
    clearablelineedit.cpp
    clickable.cpp
    clickablelabel.cpp
    colorbutton.cpp
    contextmenuactionprovider.cpp
    flatproxymodel.cpp
    fontselector.cpp
    graphicalui.cpp
    icon.cpp
    iconloader.cpp
    multilineedit.cpp
    networkmodelcontroller.cpp
    nickview.cpp
    nickviewfilter.cpp
    qssparser.cpp
    resizingstackedwidget.cpp
    settingspage.cpp
    styledlabel.cpp
    tabcompleter.cpp
    toolbaractionprovider.cpp
    uisettings.cpp
    uistyle.cpp
   )

set(MOC_HDRS
    abstractbuffercontainer.h
    abstractitemview.h
    abstractnotificationbackend.h
    action.h
    actioncollection.h
    bufferhotlistfilter.h
    bufferview.h
    bufferviewfilter.h
    bufferviewoverlayfilter.h
    clearablelineedit.h
    clickablelabel.h
    colorbutton.h
    contextmenuactionprovider.h
    flatproxymodel.h
    fontselector.h
    graphicalui.h
    iconloader.h
    multilineedit.h
    networkmodelcontroller.h
    nickview.h
    nickviewfilter.h
    resizingstackedwidget.h
    settingspage.h
    styledlabel.h
    tabcompleter.h
    toolbaractionprovider.h
    uistyle.h
   )

set(HEADERS
    clickable.h
    icon.h
    qssparser.h
    uisettings.h
   )

if(HAVE_KDE)
    set(SOURCES ${SOURCES} kcmdlinewrapper.cpp)
    set(HEADERS ${HEADERS} kcmdlinewrapper.h)
endif(HAVE_KDE)

if(CUSTOM_SPELLER)
    set(SOURCES ${SOURCES}
        speller/speller_qtextedit.cpp
        speller/hunspell_adapter.cpp

        ../../3rdparty/hunspell/affentry.cxx
        ../../3rdparty/hunspell/affixmgr.cxx
        ../../3rdparty/hunspell/csutil.cxx
        ../../3rdparty/hunspell/dictmgr.cxx
        ../../3rdparty/hunspell/filemgr.cxx
        ../../3rdparty/hunspell/hashmgr.cxx
        ../../3rdparty/hunspell/hunspell.cxx
        ../../3rdparty/hunspell/hunzip.cxx
        ../../3rdparty/hunspell/phonet.cxx
        ../../3rdparty/hunspell/replist.cxx
        ../../3rdparty/hunspell/suggestmgr.cxx

        ../../3rdparty/mythes/mythes.cxx
    )
    set(MOC_HDRS ${MOC_HDRS}
        speller/speller_qtextedit.h
    )
    set(HEADERS ${HEADERS}
        speller/speller_adapter.h

        ../../3rdparty/hunspell/affentry.hxx
        ../../3rdparty/hunspell/affixmgr.hxx
        ../../3rdparty/hunspell/atypes.hxx
        ../../3rdparty/hunspell/baseaffix.hxx
        ../../3rdparty/hunspell/config.h
        ../../3rdparty/hunspell/csutil.hxx
        ../../3rdparty/hunspell/dictmgr.hxx
        ../../3rdparty/hunspell/filemgr.hxx
        ../../3rdparty/hunspell/hashmgr.hxx
        ../../3rdparty/hunspell/htypes.hxx
        ../../3rdparty/hunspell/hunspell.h
        ../../3rdparty/hunspell/hunspell.hxx
        ../../3rdparty/hunspell/hunvisapi.h
        ../../3rdparty/hunspell/hunzip.hxx
        ../../3rdparty/hunspell/langnum.hxx
        ../../3rdparty/hunspell/phonet.hxx
        ../../3rdparty/hunspell/replist.hxx
        ../../3rdparty/hunspell/suggestmgr.hxx
        ../../3rdparty/hunspell/w_char.hxx

        ../../3rdparty/mythes/mythes.hxx
    )
endif(CUSTOM_SPELLER)

include_directories(${CMAKE_SOURCE_DIR}/src/common
                    ${CMAKE_SOURCE_DIR}/src/client
                    ${QUASSEL_QT_INCLUDES})

if(HAVE_QCA2)
  include_directories(${QCA2_INCLUDE_DIR})
endif(HAVE_QCA2)

if(NOT WITH_QT5)
  qt4_wrap_cpp(MOC ${MOC_HDRS})
endif(NOT WITH_QT5)

add_library(mod_uisupport STATIC ${SOURCES} ${MOC} ${HEADERS})
add_dependencies(mod_uisupport mod_common mod_client)
set_target_properties(mod_uisupport PROPERTIES COMPILE_FLAGS "${QUASSEL_QT_COMPILEFLAGS}")
