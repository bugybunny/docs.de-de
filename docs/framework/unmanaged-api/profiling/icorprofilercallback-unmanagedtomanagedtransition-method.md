---
title: ICorProfilerCallback::UnmanagedToManagedTransition-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerCallback.UnmanagedToManagedTransition
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerCallback::UnmanagedToManagedTransition
helpviewer_keywords:
- ICorProfilerCallback::UnmanagedToManagedTransition method [.NET Framework profiling]
- UnmanagedToManagedTransition method [.NET Framework profiling]
ms.assetid: ade2cc01-9b81-4e09-a5f9-b3b9dda27e96
topic_type: apiref
caps.latest.revision: "12"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 45a2ceb53263e317c5c72695d6bc1e93f8f70bbb
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="icorprofilercallbackunmanagedtomanagedtransition-method"></a><span data-ttu-id="ab7e3-102">ICorProfilerCallback::UnmanagedToManagedTransition-Methode</span><span class="sxs-lookup"><span data-stu-id="ab7e3-102">ICorProfilerCallback::UnmanagedToManagedTransition Method</span></span>
<span data-ttu-id="ab7e3-103">Benachrichtigt den Profiler, dass ein Übergang zwischen nicht verwaltetem Code zu verwaltetem Code aufgetreten ist.</span><span class="sxs-lookup"><span data-stu-id="ab7e3-103">Notifies the profiler that a transition from unmanaged code to managed code has occurred.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="ab7e3-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="ab7e3-104">Syntax</span></span>  
  
```  
HRESULT UnmanagedToManagedTransition(  
    [in] FunctionID functionId,  
    [in] COR_PRF_TRANSITION_REASON reason);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="ab7e3-105">Parameter</span><span class="sxs-lookup"><span data-stu-id="ab7e3-105">Parameters</span></span>  
 `functionId`  
 <span data-ttu-id="ab7e3-106">[in] Die ID der Funktion, die aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="ab7e3-106">[in] The ID of the function that is being called.</span></span>  
  
 `reason`  
 <span data-ttu-id="ab7e3-107">[in] Der Wert der [COR_PRF_TRANSITION_REASON](../../../../docs/framework/unmanaged-api/profiling/cor-prf-transition-reason-enumeration.md) Enumeration, der angibt, ob der Übergang aufgrund eines Aufrufs von nicht verwaltetem Code zu verwaltetem Code oder aufgrund einer Rückgabe von einer verwalteten Funktion aufgerufen wird, indem Sie eine verwaltete aufgetreten ist.</span><span class="sxs-lookup"><span data-stu-id="ab7e3-107">[in] A value of the [COR_PRF_TRANSITION_REASON](../../../../docs/framework/unmanaged-api/profiling/cor-prf-transition-reason-enumeration.md) enumeration that indicates whether the transition occurred because of a call into managed code from unmanaged code, or because of a return from an unmanaged function called by a managed one.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="ab7e3-108">Hinweise</span><span class="sxs-lookup"><span data-stu-id="ab7e3-108">Remarks</span></span>  
 <span data-ttu-id="ab7e3-109">Wenn der Wert der `reason` COR_PRF_TRANSITION_RETURN und `functionId` nicht null ist, ist die Funktion-ID ist, die nicht verwaltete Funktion und wird nie wurden kompiliert den Just-in-Time (JIT)-Compiler verwenden.</span><span class="sxs-lookup"><span data-stu-id="ab7e3-109">If the value of `reason` is COR_PRF_TRANSITION_RETURN and `functionId` is not null, the function ID is that of the unmanaged function, and will never have been compiled using the just-in-time (JIT) compiler.</span></span> <span data-ttu-id="ab7e3-110">Nicht verwaltete Funktionen haben einige grundlegende Informationen zugeordnet werden, z. B. einen Namen und einige Metadaten.</span><span class="sxs-lookup"><span data-stu-id="ab7e3-110">Unmanaged functions have some basic information associated with them, such as a name and some metadata.</span></span>  
  
 <span data-ttu-id="ab7e3-111">Wenn der Wert des `reason` COR_PRF_TRANSITION_CALL, ist es eventuell möglich, dass die aufgerufene Funktion (d. h. die verwaltete Funktion) noch kein JIT-kompiliert wurde.</span><span class="sxs-lookup"><span data-stu-id="ab7e3-111">If the value of `reason` is COR_PRF_TRANSITION_CALL, it may be possible that the called function (that is, the managed function) has not yet been JIT-compiled.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="ab7e3-112">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="ab7e3-112">Requirements</span></span>  
 <span data-ttu-id="ab7e3-113">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="ab7e3-113">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="ab7e3-114">**Header:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="ab7e3-114">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="ab7e3-115">**Bibliothek:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="ab7e3-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="ab7e3-116">**.NET Framework-Versionen:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="ab7e3-116">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ab7e3-117">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="ab7e3-117">See Also</span></span>  
 [<span data-ttu-id="ab7e3-118">ICorProfilerCallback-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="ab7e3-118">ICorProfilerCallback Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)  
 [<span data-ttu-id="ab7e3-119">ManagedToUnmanagedTransition-Methode</span><span class="sxs-lookup"><span data-stu-id="ab7e3-119">ManagedToUnmanagedTransition Method</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-managedtounmanagedtransition-method.md)  
 [<span data-ttu-id="ab7e3-120">Verwenden von explizitem PInvoke in C++ (DllImport-Attribut)</span><span class="sxs-lookup"><span data-stu-id="ab7e3-120">Using Explicit PInvoke in C++ (DllImport Attribute)</span></span>](/cpp/dotnet/using-explicit-pinvoke-in-cpp-dllimport-attribute)  
 [<span data-ttu-id="ab7e3-121">Verwenden von C++-Interop (implizites PInvoke)</span><span class="sxs-lookup"><span data-stu-id="ab7e3-121">Using C++ Interop (Implicit PInvoke)</span></span>](/cpp/dotnet/using-cpp-interop-implicit-pinvoke)