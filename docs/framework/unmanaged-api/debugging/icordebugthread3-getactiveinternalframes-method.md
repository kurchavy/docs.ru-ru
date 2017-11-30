---
title: "Метод ICorDebugThread3::GetActiveInternalFrames"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugThread3.GetActiveInternalFrames Method
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugThread3::GetActiveInternalFrames
helpviewer_keywords:
- ICorDebugThread3::GetActiveInternalFrames method [.NET Framework debugging]
- GetActiveInternalFrames method [.NET Framework debugging]
ms.assetid: d69796b4-5b6d-457c-85f6-2cf42e8a8773
topic_type: apiref
caps.latest.revision: "7"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: b9b94827ac49c69c5e72c2e300a80914774cc498
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="icordebugthread3getactiveinternalframes-method"></a><span data-ttu-id="076f6-102">Метод ICorDebugThread3::GetActiveInternalFrames</span><span class="sxs-lookup"><span data-stu-id="076f6-102">ICorDebugThread3::GetActiveInternalFrames Method</span></span>
<span data-ttu-id="076f6-103">Возвращает массив внутренних кадрах ([ICorDebugInternalFrame2](../../../../docs/framework/unmanaged-api/debugging/icordebuginternalframe2-interface.md) объектов) в стеке.</span><span class="sxs-lookup"><span data-stu-id="076f6-103">Returns an array of internal frames ([ICorDebugInternalFrame2](../../../../docs/framework/unmanaged-api/debugging/icordebuginternalframe2-interface.md) objects) on the stack.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="076f6-104">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="076f6-104">Syntax</span></span>  
  
```  
HRESULT GetActiveInternalFrames  
      (  
      [in] ULONG32 cInternalFrames,  
      [out] ULONG32 *pcInternalFrames,  
      [in, out,size_is(cInternalFrames), length_is(*pcInternalFrames)]  
            ICorDebugInternalFrame2 * ppInternalFrames[]  
      );  
```  
  
#### <a name="parameters"></a><span data-ttu-id="076f6-105">Параметры</span><span class="sxs-lookup"><span data-stu-id="076f6-105">Parameters</span></span>  
 `cInternalFrames`  
 <span data-ttu-id="076f6-106">[in] Количество внутренних кадрах, ожидаемая в `ppInternalFrames`.</span><span class="sxs-lookup"><span data-stu-id="076f6-106">[in] The number of internal frames expected in `ppInternalFrames`.</span></span>  
  
 `pcInternalFrames`  
 <span data-ttu-id="076f6-107">[out] Указатель на `ULONG32` , содержащее количество внутренних кадров в стеке.</span><span class="sxs-lookup"><span data-stu-id="076f6-107">[out] A pointer to a `ULONG32` that contains the number of internal frames on the stack.</span></span>  
  
 `ppInternalFrames`  
 <span data-ttu-id="076f6-108">[in, out] Указатель на адрес массива внутренних кадров в стеке.</span><span class="sxs-lookup"><span data-stu-id="076f6-108">[in, out] A pointer to the address of an array of internal frames on the stack.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="076f6-109">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="076f6-109">Return Value</span></span>  
 <span data-ttu-id="076f6-110">Этот метод возвращает следующие конкретные результаты HRESULT, а также ошибки HRESULT, которые указывают на сбой метода.</span><span class="sxs-lookup"><span data-stu-id="076f6-110">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span>  
  
|<span data-ttu-id="076f6-111">HRESULT</span><span class="sxs-lookup"><span data-stu-id="076f6-111">HRESULT</span></span>|<span data-ttu-id="076f6-112">Описание</span><span class="sxs-lookup"><span data-stu-id="076f6-112">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="076f6-113">S_OK</span><span class="sxs-lookup"><span data-stu-id="076f6-113">S_OK</span></span>|<span data-ttu-id="076f6-114">[ICorDebugInternalFrame2](../../../../docs/framework/unmanaged-api/debugging/icordebuginternalframe2-interface.md) объект был успешно создан.</span><span class="sxs-lookup"><span data-stu-id="076f6-114">The [ICorDebugInternalFrame2](../../../../docs/framework/unmanaged-api/debugging/icordebuginternalframe2-interface.md) object was successfully created.</span></span>|  
|<span data-ttu-id="076f6-115">E_INVALIDARG</span><span class="sxs-lookup"><span data-stu-id="076f6-115">E_INVALIDARG</span></span>|<span data-ttu-id="076f6-116">`cInternalFrames`не равно нулю и `ppInternalFrames` — `null`, или `pcInternalFrames` — `null`.</span><span class="sxs-lookup"><span data-stu-id="076f6-116">`cInternalFrames` is not zero and `ppInternalFrames` is `null`, or `pcInternalFrames` is `null`.</span></span>|  
|<span data-ttu-id="076f6-117">HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)</span><span class="sxs-lookup"><span data-stu-id="076f6-117">HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)</span></span>|<span data-ttu-id="076f6-118">`ppInternalFrames`меньше количество внутренних кадрах.</span><span class="sxs-lookup"><span data-stu-id="076f6-118">`ppInternalFrames` is smaller than the count of internal frames.</span></span>|  
  
## <a name="exceptions"></a><span data-ttu-id="076f6-119">Исключения</span><span class="sxs-lookup"><span data-stu-id="076f6-119">Exceptions</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="076f6-120">Примечания</span><span class="sxs-lookup"><span data-stu-id="076f6-120">Remarks</span></span>  
 <span data-ttu-id="076f6-121">Внутренние кадры — это структуры данных, переданные в стек средой выполнения для хранения временных данных.</span><span class="sxs-lookup"><span data-stu-id="076f6-121">Internal frames are data structures pushed onto the stack by the runtime to store temporary data.</span></span>  
  
 <span data-ttu-id="076f6-122">При первом вызове `GetActiveInternalFrames`, следует задать `cInternalFrames` в значение 0 (ноль) и `ppInternalFrames` параметр в значение null.</span><span class="sxs-lookup"><span data-stu-id="076f6-122">When you first call `GetActiveInternalFrames`, you should set the `cInternalFrames` parameter to 0 (zero), and the `ppInternalFrames` parameter to null.</span></span> <span data-ttu-id="076f6-123">Когда `GetActiveInternalFrames` сначала возвращает `pcInternalFrames` содержит количество внутренних кадров в стеке.</span><span class="sxs-lookup"><span data-stu-id="076f6-123">When `GetActiveInternalFrames` first returns, `pcInternalFrames` contains the count of the internal frames on the stack.</span></span>  
  
 <span data-ttu-id="076f6-124">`GetActiveInternalFrames`затем вызывать следует еще раз.</span><span class="sxs-lookup"><span data-stu-id="076f6-124">`GetActiveInternalFrames` should then be called a second time.</span></span> <span data-ttu-id="076f6-125">Необходимо передать правильное значение (`pcInternalFrames`) в `cInternalFrames` параметра, и задать указатель на массив подходящего размера в `ppInternalFrames`.</span><span class="sxs-lookup"><span data-stu-id="076f6-125">You should pass the proper count (`pcInternalFrames`) in the `cInternalFrames` parameter, and specify a pointer to an appropriately sized array in `ppInternalFrames`.</span></span>  
  
 <span data-ttu-id="076f6-126">Используйте [ICorDebugStackWalk::GetFrame](../../../../docs/framework/unmanaged-api/debugging/icordebugthread3-getactiveinternalframes-method.md) метод для возврата фактическое фреймов стека.</span><span class="sxs-lookup"><span data-stu-id="076f6-126">Use the [ICorDebugStackWalk::GetFrame](../../../../docs/framework/unmanaged-api/debugging/icordebugthread3-getactiveinternalframes-method.md) method to return actual stack frames.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="076f6-127">Требования</span><span class="sxs-lookup"><span data-stu-id="076f6-127">Requirements</span></span>  
 <span data-ttu-id="076f6-128">**Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="076f6-128">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="076f6-129">**Заголовок:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="076f6-129">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="076f6-130">**Библиотека:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="076f6-130">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="076f6-131">**Версии платформы .NET framework:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="076f6-131">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="076f6-132">См. также</span><span class="sxs-lookup"><span data-stu-id="076f6-132">See Also</span></span>  
 [<span data-ttu-id="076f6-133">Интерфейсы отладки</span><span class="sxs-lookup"><span data-stu-id="076f6-133">Debugging Interfaces</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)  
 [<span data-ttu-id="076f6-134">Отладка</span><span class="sxs-lookup"><span data-stu-id="076f6-134">Debugging</span></span>](../../../../docs/framework/unmanaged-api/debugging/index.md)