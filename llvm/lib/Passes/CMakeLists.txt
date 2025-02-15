add_llvm_component_library(LLVMPasses
  OptimizationLevel.cpp
  PassBuilder.cpp
  PassBuilderBindings.cpp
  PassBuilderPipelines.cpp
  PassPlugin.cpp
  StandardInstrumentations.cpp

  ADDITIONAL_HEADER_DIRS
  ${LLVM_MAIN_INCLUDE_DIR}/llvm
  ${LLVM_MAIN_INCLUDE_DIR}/llvm/Passes

  DEPENDS
  intrinsics_gen

  LINK_COMPONENTS
  AggressiveInstCombine
  Analysis
  Core
  Coroutines
  IPO
  InstCombine
  ObjCARC
  Scalar
  Support
  Target
  TransformUtils
  Vectorize
  Instrumentation
  )

if (LLVM_BUILD_INJECTION)
  add_compile_definitions(LLVM_BUILD_INJECTION)
  message("-- LLVMPass not dependencies guard")
else()
  # 非注入模式下需要依赖
  add_dependencies(LLVMPasses Guard)
  target_link_libraries(LLVMPasses PRIVATE Guard)
  message("-- LLVMPass dependencies guard")
endif()