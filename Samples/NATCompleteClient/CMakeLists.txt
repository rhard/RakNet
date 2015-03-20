cmake_minimum_required(VERSION 2.6)
GETCURRENTFOLDER()
#SET(EXTRALIBS "") #Extra libraries, we have none
#note the .h files are included so they show up in the windows project
#FILE(GLOB XML_FILES ${RakNet_SOURCE_DIR}/DependentExtensions/XML/*.cpp ${RakNet_SOURCE_DIR}/DependentExtensions/XML/*.h)#grab all files from xml folder and put them in the XML_FILES var
#FILE(GLOB UPNP_FILES ${RakNet_SOURCE_DIR}/DependentExtensions/miniupnpc-1.9.20150206/*.h) #grab all files from UPNP folder and put them in the UPNP_FILES var
#SET(EXTRASOURCES ${UPNP_FILES} ${XML_FILES}) #set the grabbed files as extra sources
SET(EXTRAINCLUDES ${RakNet_SOURCE_DIR}/DependentExtensions/miniupnpc-1.9.20150206)#add the include directories
STANDARDSUBPROJECTWITHOPTIONSSET(${current_folder})
add_library(UPNP_LIB STATIC IMPORTED)
 set_property(TARGET UPNP_LIB PROPERTY IMPORTED_LOCATION_RELEASE ${RakNet_SOURCE_DIR}/DependentExtensions/miniupnpc-1.9.20150206/Release/miniupnpc.lib)
 set_property(TARGET UPNP_LIB PROPERTY IMPORTED_LOCATION_DEBUG   ${RakNet_SOURCE_DIR}/DependentExtensions/miniupnpc-1.9.20150206/Debug/miniupnpcd.lib)
target_link_libraries(${current_folder} UPNP_LIB iphlpapi.lib)
add_definitions(-DMINIUPNP_STATICLIB)
VSUBFOLDER(${current_folder} "Samples/NAT Punchthrough")





