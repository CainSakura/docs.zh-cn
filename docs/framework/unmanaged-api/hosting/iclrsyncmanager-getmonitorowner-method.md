---
title: "ICLRSyncManager::GetMonitorOwner 方法"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICLRSyncManager.GetMonitorOwner
api_location: mscoree.dll
api_type: COM
f1_keywords: ICLRSyncManager::GetMonitorOwner
helpviewer_keywords:
- ICLRSyncManager::GetMonitorOwner method [.NET Framework hosting]
- GetMonitorOwner method [.NET Framework hosting]
ms.assetid: 840983a4-396d-47b4-86a0-d35f9b437cdb
topic_type: apiref
caps.latest.revision: "10"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 90fbba9a5aead27d79c5355d69bc12481e826b65
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="iclrsyncmanagergetmonitorowner-method"></a><span data-ttu-id="297ca-102">ICLRSyncManager::GetMonitorOwner 方法</span><span class="sxs-lookup"><span data-stu-id="297ca-102">ICLRSyncManager::GetMonitorOwner Method</span></span>
<span data-ttu-id="297ca-103">获取[IHostTask](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)拥有由指定的 cookie 的监视器的实例。</span><span class="sxs-lookup"><span data-stu-id="297ca-103">Gets the [IHostTask](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md) instance that owns the monitor identified by the specified cookie.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="297ca-104">语法</span><span class="sxs-lookup"><span data-stu-id="297ca-104">Syntax</span></span>  
  
```  
HRESULT GetMonitorOwner (  
    [in]  SIZE_T     cookie,  
    [out] IHostTask *ppOwnerHostTask  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="297ca-105">参数</span><span class="sxs-lookup"><span data-stu-id="297ca-105">Parameters</span></span>  
 `cookie`  
 <span data-ttu-id="297ca-106">[in]与监视器关联的 cookie。</span><span class="sxs-lookup"><span data-stu-id="297ca-106">[in] The cookie associated with the monitor.</span></span>  
  
 `ppOwnerHostTask`  
 <span data-ttu-id="297ca-107">[out]指向的指针`IHostTask`，当前拥有的监视器或为 null 如果没有任何任务有所有权。</span><span class="sxs-lookup"><span data-stu-id="297ca-107">[out] A pointer to the `IHostTask` that currently owns the monitor, or null if no task has ownership.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="297ca-108">返回值</span><span class="sxs-lookup"><span data-stu-id="297ca-108">Return Value</span></span>  
  
|<span data-ttu-id="297ca-109">HRESULT</span><span class="sxs-lookup"><span data-stu-id="297ca-109">HRESULT</span></span>|<span data-ttu-id="297ca-110">描述</span><span class="sxs-lookup"><span data-stu-id="297ca-110">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="297ca-111">S_OK</span><span class="sxs-lookup"><span data-stu-id="297ca-111">S_OK</span></span>|<span data-ttu-id="297ca-112">`GetMonitorOwner`已成功返回。</span><span class="sxs-lookup"><span data-stu-id="297ca-112">`GetMonitorOwner` returned successfully.</span></span>|  
|<span data-ttu-id="297ca-113">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="297ca-113">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="297ca-114">CLR 尚未加载到进程中，或 CLR 处于不能运行托管的代码或成功处理调用的状态。</span><span class="sxs-lookup"><span data-stu-id="297ca-114">The CLR has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="297ca-115">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="297ca-115">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="297ca-116">调用操作已超时。</span><span class="sxs-lookup"><span data-stu-id="297ca-116">The call timed out.</span></span>|  
|<span data-ttu-id="297ca-117">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="297ca-117">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="297ca-118">调用方不拥有该锁。</span><span class="sxs-lookup"><span data-stu-id="297ca-118">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="297ca-119">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="297ca-119">HOST_E_ABANDONED</span></span>|<span data-ttu-id="297ca-120">事件已被取消时被阻塞的线程，或者纤程正在等待它。</span><span class="sxs-lookup"><span data-stu-id="297ca-120">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="297ca-121">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="297ca-121">E_FAIL</span></span>|<span data-ttu-id="297ca-122">出现未知的灾难性故障。</span><span class="sxs-lookup"><span data-stu-id="297ca-122">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="297ca-123">如果某方法返回 E_FAIL，CLR 不再可用进程内。</span><span class="sxs-lookup"><span data-stu-id="297ca-123">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="297ca-124">到托管方法的后续调用会返回 HOST_E_CLRNOTAVAILABLE。</span><span class="sxs-lookup"><span data-stu-id="297ca-124">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="297ca-125">备注</span><span class="sxs-lookup"><span data-stu-id="297ca-125">Remarks</span></span>  
 <span data-ttu-id="297ca-126">主机通常调用`GetMonitorOwner`作为死锁检测机制的一部分。</span><span class="sxs-lookup"><span data-stu-id="297ca-126">The host typically calls `GetMonitorOwner` as part of a deadlock-detection mechanism.</span></span> <span data-ttu-id="297ca-127">通过调用创建时，cookie 是与监视器关联[ihostsyncmanager:: Createmonitorevent](../../../../docs/framework/unmanaged-api/hosting/ihostsyncmanager-createmonitorevent-method.md)。</span><span class="sxs-lookup"><span data-stu-id="297ca-127">The cookie is associated with a monitor when it is created by using a call to [IHostSyncManager::CreateMonitorEvent](../../../../docs/framework/unmanaged-api/hosting/ihostsyncmanager-createmonitorevent-method.md).</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="297ca-128">释放基础监视器的事件的调用可能会阻止-但不是会死锁-如果此方法的调用当前实际上在与该监视器关联的 cookie。</span><span class="sxs-lookup"><span data-stu-id="297ca-128">A call to release the event underlying the monitor might block—but will not deadlock—if a call to this method is currently in effect on the cookie associated with that monitor.</span></span> <span data-ttu-id="297ca-129">如果用户尝试获取此监视器，也可能会阻止其他任务。</span><span class="sxs-lookup"><span data-stu-id="297ca-129">Other tasks might also block if they attempt to acquire this monitor.</span></span>  
  
 <span data-ttu-id="297ca-130">`GetMonitorOwner`始终将立即返回，可以调用后调用的任何时间`CreateMonitorEvent`。</span><span class="sxs-lookup"><span data-stu-id="297ca-130">`GetMonitorOwner` always returns immediately and can be called any time after a call to `CreateMonitorEvent`.</span></span> <span data-ttu-id="297ca-131">主机不需要等待，直到某任务正在等待事件。</span><span class="sxs-lookup"><span data-stu-id="297ca-131">The host does not need to wait until a task is waiting on the event.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="297ca-132">要求</span><span class="sxs-lookup"><span data-stu-id="297ca-132">Requirements</span></span>  
 <span data-ttu-id="297ca-133">**平台：**请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="297ca-133">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="297ca-134">**标头：** MSCorEE.h</span><span class="sxs-lookup"><span data-stu-id="297ca-134">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="297ca-135">**库：**作为 MSCorEE.dll 中的资源</span><span class="sxs-lookup"><span data-stu-id="297ca-135">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="297ca-136">**.NET framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="297ca-136">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="297ca-137">另请参阅</span><span class="sxs-lookup"><span data-stu-id="297ca-137">See Also</span></span>  
 [<span data-ttu-id="297ca-138">ICLRSyncManager 接口</span><span class="sxs-lookup"><span data-stu-id="297ca-138">ICLRSyncManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/iclrsyncmanager-interface.md)  
 [<span data-ttu-id="297ca-139">IHostSyncManager 接口</span><span class="sxs-lookup"><span data-stu-id="297ca-139">IHostSyncManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostsyncmanager-interface.md)