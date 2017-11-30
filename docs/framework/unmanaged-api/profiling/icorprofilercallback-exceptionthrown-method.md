---
title: "Метод ICorProfilerCallback::ExceptionThrown"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerCallback.ExceptionThrown
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerCallback::ExceptionThrown
helpviewer_keywords:
- ExceptionThrown method [.NET Framework profiling]
- ICorProfilerCallback::ExceptionThrown method [.NET Framework profiling]
ms.assetid: f1a23f3b-ac21-4905-8abf-8ea59f15af53
topic_type: apiref
caps.latest.revision: "12"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 3986ca8205297a36bb54825a7af72aeb9821f75b
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="icorprofilercallbackexceptionthrown-method"></a><span data-ttu-id="7fe96-102">Метод ICorProfilerCallback::ExceptionThrown</span><span class="sxs-lookup"><span data-stu-id="7fe96-102">ICorProfilerCallback::ExceptionThrown Method</span></span>
<span data-ttu-id="7fe96-103">Уведомляет профилировщик о том, что было создано исключение.</span><span class="sxs-lookup"><span data-stu-id="7fe96-103">Notifies the profiler that an exception has been thrown.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="7fe96-104">Эта функция вызывается только в том случае, если исключение достигает управляемого кода.</span><span class="sxs-lookup"><span data-stu-id="7fe96-104">This function is called only if the exception reaches managed code.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="7fe96-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="7fe96-105">Syntax</span></span>  
  
```  
HRESULT ExceptionThrown(  
    [in] ObjectID thrownObjectId);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="7fe96-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="7fe96-106">Parameters</span></span>  
 `thrownObjectId`  
 <span data-ttu-id="7fe96-107">[in] Идентификатор объекта, вызвавшего исключение.</span><span class="sxs-lookup"><span data-stu-id="7fe96-107">[in] The ID of the object that caused the exception to be thrown.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="7fe96-108">Примечания</span><span class="sxs-lookup"><span data-stu-id="7fe96-108">Remarks</span></span>  
 <span data-ttu-id="7fe96-109">Профилировщик не должен блокироваться при реализации этого метода, так как стек может находиться в состоянии, допускающем сборку мусора, и поэтому не удастся включить сборку мусора.</span><span class="sxs-lookup"><span data-stu-id="7fe96-109">The profiler should not block in its implementation of this method because the stack may not be in a state that allows garbage collection, and therefore preemptive garbage collection cannot be enabled.</span></span> <span data-ttu-id="7fe96-110">Если здесь профилировщик блокируется и выполняется сборка мусора, среда выполнения будет блокироваться до возвращает этот обратный вызов.</span><span class="sxs-lookup"><span data-stu-id="7fe96-110">If the profiler blocks here and garbage collection is attempted, the runtime will block until this callback returns.</span></span>  
  
 <span data-ttu-id="7fe96-111">Реализация этого метода профилировщика не должны вызывать управляемый код или каким-либо образом вызывать распределения управляемой памяти.</span><span class="sxs-lookup"><span data-stu-id="7fe96-111">The profiler's implementation of this method should not call into managed code or in any way cause a managed-memory allocation.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="7fe96-112">Требования</span><span class="sxs-lookup"><span data-stu-id="7fe96-112">Requirements</span></span>  
 <span data-ttu-id="7fe96-113">**Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="7fe96-113">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="7fe96-114">**Заголовок:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="7fe96-114">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="7fe96-115">**Библиотека:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="7fe96-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="7fe96-116">**Версии платформы .NET framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="7fe96-116">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7fe96-117">См. также</span><span class="sxs-lookup"><span data-stu-id="7fe96-117">See Also</span></span>  
 [<span data-ttu-id="7fe96-118">Интерфейс ICorProfilerCallback</span><span class="sxs-lookup"><span data-stu-id="7fe96-118">ICorProfilerCallback Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)