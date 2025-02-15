# Use LLVM_HEADERS for each `tablegen(LLVM)` in subdirectories
# LLVM_HEADERS_TABLEGEN points to `llvm-min-tblgen`
set(LLVM_TABLEGEN_PROJECT LLVM_HEADERS)

if (OLLVM_BUILD_DEBUG)
  add_compile_definitions(OLLVM_BUILD_DEBUG)
endif()

add_subdirectory(CodeGen)
add_subdirectory(IR)
add_subdirectory(Support)
add_subdirectory(Frontend)
add_subdirectory(TargetParser)
