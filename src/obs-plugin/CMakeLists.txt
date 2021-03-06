project(obs-plugin)

find_package(Libobs REQUIRED)

find_library(AVFOUNDATION AVFoundation)
find_library(COCOA Cocoa)
find_library(COREFOUNDATION CoreFoundation)
find_library(COREMEDIA CoreMedia)
find_library(COREVIDEO CoreVideo)
find_library(COCOA Cocoa)
find_library(COREMEDIAIO CoreMediaIO)
find_library(IOSURFACE IOSurface)
find_library(IOKIT IOKit)

set(CMAKE_PREFIX_PATH "${QTDIR}")
find_package(Qt5Core REQUIRED)
find_package(Qt5Widgets REQUIRED)

include_directories(${AVFOUNDATION}
                    ${COCOA}
                    ${COREFOUNDATION}
                    ${COREMEDIA}
                    ${COREVIDEO}
                    ${COREMEDIAIO}
                    ${COCOA}
                    ${IOSURFACE}
                    ${LIBOBS_INCLUDE_DIR}
                    "${LIBOBS_INCLUDE_DIR}/../UI/obs-frontend-api"
                    ${Qt5Core_INCLUDES}
                    ${Qt5Widgets_INCLUDES}
                    ../common/CoreMediaIO/PublicUtility
                    ../common/CoreAudio/PublicUtility
                    ../common/CoreMediaIO/PublicUtility/IOSurfaceAssistant
                    ../common/CoreMediaIO/PublicUtility/POSIXThreadAssistant
                    ../common/CoreMediaIO/PublicUtility/IOVideoAssistant
                    ../common/CoreMediaIO/PublicUtility/IOStreamAssistant
                    ../common/CoreMediaIO/PublicUtility/IOKitAssistant
                    ../common/CoreMediaIO/PublicUtility/CoreMediaAssistant
                    ../common/CoreMediaIO/PublicUtility/CoreVideoAssistant
                    ../common/CoreMediaIO/DeviceAbstractionLayer/Devices/DP/Properties
                    ../common/CoreMediaIO/DeviceAbstractionLayer/Devices/DP/Base
                    ../common/CoreMediaIO/DeviceAbstractionLayer/Devices/IOV/PlugIn
                    ../common/CoreMediaIO/DeviceAbstractionLayer/Devices/Sample
                    ../common/CoreMediaIO/DeviceAbstractionLayer/Devices/Sample/Assistant
                    ../common/CoreMediaIO/DeviceAbstractionLayer/Devices/Sample/Assistant/Server
                    ../common/CoreMediaIO/DeviceAbstractionLayer/Devices/Sample/Assistant/Server/Device
                    ./)

set(obs-plugin_SOURCES
	../common/CoreMediaIO/PublicUtility/IOSurfaceAssistant/CMIO_SA_Assistance.cpp
	../common/CoreMediaIO/PublicUtility/POSIXThreadAssistant/CMIO_PTA_NotificationPortThread.cpp
	../common/CoreMediaIO/PublicUtility/IOVideoAssistant/CMIO_IOVA_Assistance.cpp
	../common/CoreMediaIO/PublicUtility/IOStreamAssistant/CMIO_IOSA_Assistance.cpp
	../common/CoreMediaIO/PublicUtility/IOKitAssistant/CMIO_IOKA_NotificationPort.cpp
	../common/CoreMediaIO/DeviceAbstractionLayer/Devices/DP/Properties/CMIO_DP_Property_FirstOutputPresentationTimeStamp.cpp
	../common/CoreMediaIO/DeviceAbstractionLayer/Devices/DP/Properties/CMIO_DP_Property_Deck.cpp
	../common/CoreMediaIO/DeviceAbstractionLayer/Devices/Sample/Assistant/Server/CMIO_DPA_Sample_VCamServer.cpp
	../common/CoreMediaIO/DeviceAbstractionLayer/Devices/DP/Properties/CMIO_DP_Property_Base.cpp
	../common/CoreMediaIO/DeviceAbstractionLayer/Devices/DP/Base/CMIO_DP_ControlDictionary.cpp
	../common/CoreMediaIO/DeviceAbstractionLayer/Devices/IOV/PlugIn/CMIO_DP_IOV_ControlDictionary.cpp
	../common/CoreMediaIO/DeviceAbstractionLayer/Devices/Sample/Assistant/Server/Device/CMIO_DPA_Sample_Server_VCamInputStream.cpp
	../common/CoreMediaIO/DeviceAbstractionLayer/Devices/Sample/Assistant/Server/Device/CMIO_DPA_Sample_Server_Stream.cpp
	../common/CoreMediaIO/DeviceAbstractionLayer/Devices/Sample/Assistant/Server/CMIO_DPA_Sample_Server_VCamAssistant.cpp
	../common/CoreMediaIO/DeviceAbstractionLayer/Devices/Sample/Assistant/Server/Device/CMIO_DPA_Sample_Server_VCamDevice.cpp
	../common/CoreMediaIO/DeviceAbstractionLayer/Devices/Sample/Assistant/Server/CMIO_DPA_Sample_Server_MIGInterface.cpp
	../common/CoreMediaIO/DeviceAbstractionLayer/Devices/Sample/Assistant/Server/Device/CMIO_DPA_Sample_Server_Frame.cpp
	../common/CoreMediaIO/DeviceAbstractionLayer/Devices/Sample/Assistant/Server/Device/CMIO_DPA_Sample_Server_Deck.cpp
	../common/CoreMediaIO/DeviceAbstractionLayer/Devices/Sample/Assistant/Server/Device/CMIO_DPA_Sample_Server_Device.cpp
	../common/CoreMediaIO/DeviceAbstractionLayer/Devices/Sample/Assistant/Server/Device/CMIO_DPA_Sample_Server_ClientStream.cpp
	../common/CoreMediaIO/DeviceAbstractionLayer/Devices/Sample/Assistant/Server/CMIO_DPA_Sample_Server_Assistant.cpp
	../common/CoreMediaIO/PublicUtility/DALAssistant/CMIO_DALA_Object.cpp
	../common/CoreMediaIO/PublicUtility/CMIODebugMacros.cpp
	../common/CoreAudio/PublicUtility/CAProcess.cpp
	../common/CoreAudio/PublicUtility/CAPThread.cpp
	../common/CoreAudio/PublicUtility/CAMutex.cpp
	../common/CoreAudio/PublicUtility/CAHostTimeBase.cpp
	../common/CoreAudio/PublicUtility/CAGuard.cpp
	../common/CoreAudio/PublicUtility/CACFString.cpp
	../common/CoreAudio/PublicUtility/CACFNumber.cpp
	../common/CoreAudio/PublicUtility/CACFDictionary.cpp
	../common/CoreAudio/PublicUtility/CACFArray.cpp
	CMIODPASampleServer.cpp
	plugin-main.cpp)

add_library(obs-plugin MODULE
	${obs-plugin_SOURCES}
	${obs-plugin_HEADERS})

target_link_libraries(obs-plugin
	${AVFOUNDATION}
	${COCOA}
	${COREFOUNDATION}
	${COREMEDIA}
	${COREVIDEO}
	${COREMEDIAIO}
	${IOSURFACE}
	${IOKIT}
	${LIBOBS_LIB}
	${OBS_FRONTEND_LIB}
	Qt5::Core
	Qt5::Widgets)

set_target_properties(obs-plugin PROPERTIES
	PREFIX ""
	OUTPUT_NAME "obs-mac-virtualcam")
