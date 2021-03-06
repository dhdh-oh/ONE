set(ONE_COMMAND_FILES
    one-import
    one-import-tf
    one-import-tflite
    one-optimize
    one-quantize
    one-pack
    one-codegen
)

foreach(ONE_COMMAND IN ITEMS ${ONE_COMMAND_FILES})

  set(ONE_COMMAND_FILE ${ONE_COMMAND})
  set(ONE_COMMAND_SRC "${CMAKE_CURRENT_SOURCE_DIR}/${ONE_COMMAND_FILE}")
  set(ONE_COMMAND_BIN "${CMAKE_CURRENT_BINARY_DIR}/${ONE_COMMAND_FILE}")
  set(ONE_COMMAND_TARGET "${ONE_COMMAND}_target")

  add_custom_command(OUTPUT ${ONE_COMMAND_BIN}
    COMMAND ${CMAKE_COMMAND} -E copy "${ONE_COMMAND_SRC}" "${ONE_COMMAND_BIN}"
    DEPENDS ${ONE_COMMAND_SRC}
    COMMENT "Generate ${ONE_COMMAND_BIN}"
  )

  add_custom_target(${ONE_COMMAND_TARGET} ALL DEPENDS ${ONE_COMMAND_BIN})

  install(FILES ${ONE_COMMAND}
          PERMISSIONS OWNER_WRITE OWNER_READ OWNER_EXECUTE
                      GROUP_READ GROUP_WRITE GROUP_EXECUTE
                      WORLD_READ WORLD_EXECUTE
          DESTINATION bin)
          
endforeach(ONE_COMMAND)
