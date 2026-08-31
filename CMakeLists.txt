if(ESP_PLATFORM)
    idf_component_register(
        SRCS            "sps30.c"
        INCLUDE_DIRS    "."
    )
else()
    add_library(sps30 STATIC sps30.c)
    target_include_directories(sps30 PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
endif()
