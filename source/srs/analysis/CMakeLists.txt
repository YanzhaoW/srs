target_sources(srs PRIVATE DataProcessor.cpp DataStructs.cpp DataWriter.cpp)

target_link_libraries(srs PRIVATE onetbb::onetbb glaze::glaze)
target_include_directories(srs PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})

if(ROOT_FOUND)
    target_link_libraries(srs PRIVATE ROOT::RIO ROOT::Tree)
    target_compile_definitions(srs PRIVATE HAS_ROOT=1)
    target_compile_options(srs PRIVATE "-Wno-cpp")
    root_generate_dictionary(
        srs_dict
        DataStructs.hpp
        MODULE
        srs
        LINKDEF
        SRSLinkDef.hpp)
endif()
