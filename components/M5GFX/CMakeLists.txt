set(COMPONENT_ADD_INCLUDEDIRS
    src
    )

# Only include sources if the target is NOT esp32s2
if(NOT "${IDF_TARGET}" STREQUAL "esp32s2")
  file(GLOB SRCS
       src/*.cpp
       src/lgfx/Fonts/efont/*.c
       src/lgfx/Fonts/IPA/*.c
       src/lgfx/utility/*.c
       src/lgfx/v1/*.cpp
       src/lgfx/v1/misc/*.cpp
       src/lgfx/v1/panel/*.cpp
       src/lgfx/v1/platforms/esp32/*.cpp
       src/lgfx/v1/platforms/esp32c3/*.cpp
       src/lgfx/v1/platforms/esp32s3/*.cpp
       src/lgfx/v1/touch/*.cpp
       )
  set(COMPONENT_SRCS ${SRCS})
else()
  # For esp32s2, define an empty source list
  set(COMPONENT_SRCS "")
endif()

if (IDF_VERSION_MAJOR GREATER_EQUAL 5)
    set(COMPONENT_REQUIRES nvs_flash efuse driver esp_timer)
elseif ((IDF_VERSION_MAJOR EQUAL 4) AND (IDF_VERSION_MINOR GREATER 3) OR IDF_VERSION_MAJOR GREATER 4)
    set(COMPONENT_REQUIRES nvs_flash efuse esp_lcd)
else()
    set(COMPONENT_REQUIRES nvs_flash efuse)
endif()

### If you use arduino-esp32 components, please activate next comment line.
# list(APPEND COMPONENT_REQUIRES arduino-esp32)


message(STATUS "M5GFX use components = ${COMPONENT_REQUIRES}")

register_component()
