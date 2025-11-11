add_executable(application
    main.c
)

# pull in common dependencies
target_link_libraries(application pico_stdlib)

# create map/bin/hex/uf2 file etc.
pico_add_extra_outputs(application)
