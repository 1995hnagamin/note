# ImcompleteArray
要素数が明示されていない配列.
`int A[]`とか。
[Type.h](http://clang.llvm.org/doxygen/Type_8h_source.html#l02527)

# VariableArray
要素数が変数の配列.(そんなものはない)
[Type.h](http://clang.llvm.org/doxygen/Type_8h_source.html#l02560)

# DependentSizedArray
要素数がconstexprで指定された配列.
[Type.h](http://clang.llvm.org/doxygen/Type_8h_source.html#l02614)

# Canonical Type
typedefされていない型.

# -fdump-record-layouts

# -fsyntax-only

# -emit-llvm

# -ast-dump

# clang::attr::Kind
列挙型。
* Annotate,
* CFConsumed,
* CarriesDependency,
* NSConsumed, LAST\_INHERITABLE\_PARAM = NSConsumed,
* AMDGPUNumSGPR,
* AMDGPUNumVGPR,
* ARMInterrupt,
* AcquireCapability,
* AcquiredAfter,
* AcquiredBefore,
* AlignMac68k,
* Aligned,
* AlwaysInline,
* AnalyzerNoReturn,
* ArcWeakrefUnavailable,
* ArgumentWithTypeTag,
* AsmLabel,
* AssertCapability,
* AssertExclusiveLock,
* AssertSharedLock,
* AssumeAligned,
* Availability,
* Blocks,
* C11NoReturn,
* CDecl,
* CFAuditedTransfer,
* CFReturnsNotRetained,
* CFReturnsRetained,
* CFUnknownTransfer,
* CUDAConstant,
* CUDADevice,
* CUDAGlobal,
* CUDAHost,
* CUDAInvalidTarget,
* CUDALaunchBounds,
* CUDAShared,
* CXX11NoReturn,
* CallableWhen,
* Capability,
* CapturedRecord,
* Cleanup,
* Cold,
* Common,
* Const,
* Constructor,
* Consumable,
* ConsumableAutoCast,
* ConsumableSetOnRead,
* DLLExport,
* DLLImport,
* Deprecated,
* Destructor,
* EnableIf,
* ExclusiveTrylockFunction,
* FastCall,
* Final,
* FlagEnum,
* Flatten,
* Format,
* FormatArg,
* GNUInline,
* GuardedBy,
* GuardedVar,
* Hot,
* IBAction,
* IBOutlet,
* IBOutletCollection,
* InitPriority,
* IntelOclBicc,
* LockReturned,
* LocksExcluded,
* MSABI,
* MSInheritance,
* MSNoVTable,
* MSP430Interrupt,
* MSStruct,
* MSVtorDisp,
* MaxFieldAlignment,
* MayAlias,
* MinSize,
* Mips16,
* NSConsumesSelf,
* NSReturnsAutoreleased,
* NSReturnsNotRetained,
* NSReturnsRetained,
* Naked,
* NoCommon,
* NoDebug,
* NoDuplicate,
* NoInline,
* NoInstrumentFunction,
* NoMips16,
* NoReturn,
* NoSanitize,
* NoSplitStack,
* NoThreadSafetyAnalysis,
* NoThrow,
* NonNull,
* OMPThreadPrivateDecl,
* ObjCBridge,
* ObjCBridgeMutable,
* ObjCBridgeRelated,
* ObjCException,
* ObjCExplicitProtocolImpl,
* ObjCIndependentClass,
* ObjCMethodFamily,
* ObjCNSObject,
* ObjCPreciseLifetime,
* ObjCRequiresPropertyDefs,
* ObjCRequiresSuper,
* ObjCReturnsInnerPointer,
* ObjCRootClass,
* OpenCLKernel,
* OptimizeNone,
* Override,
* Ownership,
* Packed,
* ParamTypestate,
* Pascal,
* Pcs,
* PtGuardedBy,
* PtGuardedVar,
* Pure,
* ReleaseCapability,
* ReqdWorkGroupSize,
* RequiresCapability,
* Restrict,
* ReturnTypestate,
* ReturnsNonNull,
* ReturnsTwice,
* ScopedLockable,
* Section,
* SelectAny,
* Sentinel,
* SetTypestate,
* SharedTrylockFunction,
* StdCall,
* SysVABI,
* TLSModel,
* Target,
* TestTypestate,
* ThisCall,
* TransparentUnion,
* TryAcquireCapability,
* TypeTagForDatatype,
* TypeVisibility,
* Unavailable,
* Unused,
* Used,
* Uuid,
* VecReturn,
* VecTypeHint,
* VectorCall,
* Visibility,
* WarnUnused,
* WarnUnusedResult,
* Weak,
* WeakImport,
* WeakRef,
* WorkGroupSizeHint,
* X86ForceAlignArgPointer, LAST\_INHERITABLE = X86ForceAlignArgPointer,
* Alias,
* AlignValue,
* FallThrough,
* InitSeg,
* LoopHint,
* Mode,
* ObjCBoxable,
* ObjCDesignatedInitializer,
* ObjCRuntimeName,
* OpenCLImageAccess,
* Overloadable,
* Thread,
* NUM\_ATTRS