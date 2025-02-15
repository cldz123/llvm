add_llvm_component_library(LLVMipo
  AlwaysInliner.cpp
  Annotation2Metadata.cpp
  ArgumentPromotion.cpp
  Attributor.cpp
  AttributorAttributes.cpp
  BarrierNoopPass.cpp
  BlockExtractor.cpp
  CalledValuePropagation.cpp
  ConstantMerge.cpp
  CrossDSOCFI.cpp
  DeadArgumentElimination.cpp
  ElimAvailExtern.cpp
  ExtractGV.cpp
  ForceFunctionAttrs.cpp
  FunctionAttrs.cpp
  FunctionImport.cpp
  FunctionSpecialization.cpp
  GlobalDCE.cpp
  GlobalOpt.cpp
  GlobalSplit.cpp
  HotColdSplitting.cpp
  IPO.cpp
  IROutliner.cpp
  InferFunctionAttrs.cpp
  InlineSimple.cpp
  Inliner.cpp
  Internalize.cpp
  LoopExtractor.cpp
  LowerTypeTests.cpp
  MergeFunctions.cpp
  ModuleInliner.cpp
  OpenMPOpt.cpp
  PartialInlining.cpp
  PassManagerBuilder.cpp
  PruneEH.cpp
  SampleContextTracker.cpp
  SampleProfile.cpp
  SampleProfileProbe.cpp
  SCCP.cpp
  StripDeadPrototypes.cpp
  StripSymbols.cpp
  SyntheticCountsPropagation.cpp
  ThinLTOBitcodeWriter.cpp
  WholeProgramDevirt.cpp

  ADDITIONAL_HEADER_DIRS
  ${LLVM_MAIN_INCLUDE_DIR}/llvm/Transforms
  ${LLVM_MAIN_INCLUDE_DIR}/llvm/Transforms/IPO

  DEPENDS
  intrinsics_gen
  omp_gen

  COMPONENT_NAME
  IPO

  LINK_COMPONENTS
  AggressiveInstCombine
  Analysis
  BitReader
  BitWriter
  Core
  FrontendOpenMP
  InstCombine
  IRReader
  Linker
  Object
  ProfileData
  Scalar
  Support
  TransformUtils
  Vectorize
  Instrumentation
  Scalar
  )

if (LLVM_BUILD_INJECTION)
  add_compile_definitions(LLVM_BUILD_INJECTION)
  message("-- LLVMipo not dependencies guard")
else()
  # 非注入模式下需要依赖
  add_dependencies(LLVMipo Guard)
  target_link_libraries(LLVMipo PRIVATE Guard)
  message("-- LLVMipo dependencies guard")
endif()