---
title: "Метод ICorDebugInternalFrame2::GetFrameAddress"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugInternalFrame2.GetFrameAddress Method
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugInternalFrame2::GetFrameAddress
helpviewer_keywords:
- GetFrameAddress method [.NET Framework debugging]
- ICorDebugInternalFrame2::GetFrameAddress method [.NET Framework debugging]
ms.assetid: 4ee8d058-ffc8-4967-9133-a5adfef4e518
topic_type: apiref
caps.latest.revision: "6"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 9ee867afe99fc5d2f2eb27bb1e6888aef8341d71
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="icordebuginternalframe2getframeaddress-method"></a><span data-ttu-id="91099-102">Метод ICorDebugInternalFrame2::GetFrameAddress</span><span class="sxs-lookup"><span data-stu-id="91099-102">ICorDebugInternalFrame2::GetFrameAddress Method</span></span>
<span data-ttu-id="91099-103">Возвращает адрес внутреннего кадра стека.</span><span class="sxs-lookup"><span data-stu-id="91099-103">Returns the stack address of the internal frame.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="91099-104">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="91099-104">Syntax</span></span>  
  
```  
HRESULT GetFrameAddress([out] CORDB_ADDRESS *pAddress);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="91099-105">Параметры</span><span class="sxs-lookup"><span data-stu-id="91099-105">Parameters</span></span>  
 `pAddress`  
 <span data-ttu-id="91099-106">[out] Указатель на `CORDB_ADDRESS` для внутреннего фрейма.</span><span class="sxs-lookup"><span data-stu-id="91099-106">[out] Pointer to the `CORDB_ADDRESS` for the internal frame.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="91099-107">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="91099-107">Return Value</span></span>  
 <span data-ttu-id="91099-108">Этот метод возвращает следующие конкретные результаты HRESULT, а также ошибки HRESULT, которые указывают на сбой метода.</span><span class="sxs-lookup"><span data-stu-id="91099-108">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span>  
  
|<span data-ttu-id="91099-109">HRESULT</span><span class="sxs-lookup"><span data-stu-id="91099-109">HRESULT</span></span>|<span data-ttu-id="91099-110">Описание</span><span class="sxs-lookup"><span data-stu-id="91099-110">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="91099-111">S_OK</span><span class="sxs-lookup"><span data-stu-id="91099-111">S_OK</span></span>|<span data-ttu-id="91099-112">Адрес внутреннего кадра успешно возвращен.</span><span class="sxs-lookup"><span data-stu-id="91099-112">The address of the internal frame was successfully returned.</span></span>|  
|<span data-ttu-id="91099-113">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="91099-113">E_FAIL</span></span>|<span data-ttu-id="91099-114">Не удалось вернуть адрес внутреннего кадра.</span><span class="sxs-lookup"><span data-stu-id="91099-114">The address of the internal frame could not be returned.</span></span>|  
|<span data-ttu-id="91099-115">E_INVALIDARG</span><span class="sxs-lookup"><span data-stu-id="91099-115">E_INVALIDARG</span></span>|<span data-ttu-id="91099-116">Свойство `pAddress` имеет значение `null`.</span><span class="sxs-lookup"><span data-stu-id="91099-116">`pAddress` is `null`.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="91099-117">Примечания</span><span class="sxs-lookup"><span data-stu-id="91099-117">Remarks</span></span>  
 <span data-ttu-id="91099-118">Значение, возвращаемое в `pAddress` может использоваться для определения положения внутреннего кадра относительно других кадров в стеке.</span><span class="sxs-lookup"><span data-stu-id="91099-118">The value returned in `pAddress` can be used to determine the location of the internal frame relative to other frames on the stack.</span></span> <span data-ttu-id="91099-119">Даже на компьютерах с архитектурой IA-64 внутренний кадр существует только в стеке и нет соответствующего указателя в резервное хранилище.</span><span class="sxs-lookup"><span data-stu-id="91099-119">Even on IA-64-based computers, the internal frame lives on the stack only, and there is no corresponding pointer to a backing store.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="91099-120">Требования</span><span class="sxs-lookup"><span data-stu-id="91099-120">Requirements</span></span>  
 <span data-ttu-id="91099-121">**Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="91099-121">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="91099-122">**Заголовок:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="91099-122">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="91099-123">**Библиотека:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="91099-123">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="91099-124">**Версии платформы .NET framework:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="91099-124">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="91099-125">См. также</span><span class="sxs-lookup"><span data-stu-id="91099-125">See Also</span></span>  
 [<span data-ttu-id="91099-126">Интерфейс ICorDebugInternalFrame2</span><span class="sxs-lookup"><span data-stu-id="91099-126">ICorDebugInternalFrame2 Interface</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebuginternalframe2-interface.md)  
 [<span data-ttu-id="91099-127">Интерфейсы отладки</span><span class="sxs-lookup"><span data-stu-id="91099-127">Debugging Interfaces</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)  
 [<span data-ttu-id="91099-128">Отладка</span><span class="sxs-lookup"><span data-stu-id="91099-128">Debugging</span></span>](../../../../docs/framework/unmanaged-api/debugging/index.md)