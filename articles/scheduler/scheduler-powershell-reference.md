---
title: "aaaScheduler PowerShell cmdlet'leri başvurusu"
description: "Scheduler PowerShell cmdlet'leri başvurusu"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 9a26c457-d7a1-4e4a-bc79-f26592155218
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: a2b23bcd3e4493ffba1dbf21fbb87818be7c01e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-powershell-cmdlets-reference"></a><span data-ttu-id="43c48-103">Scheduler PowerShell cmdlet'leri başvurusu</span><span class="sxs-lookup"><span data-stu-id="43c48-103">Scheduler PowerShell Cmdlets Reference</span></span>
<span data-ttu-id="43c48-104">Aşağıdaki tablonun hello açıklar ve her bir ana cmdlet'leri Azure Scheduler hello toohello başvuru sayfası bağlar.</span><span class="sxs-lookup"><span data-stu-id="43c48-104">hello following table describes and links toohello reference page of each of hello major cmdlets in Azure Scheduler.</span></span>

<span data-ttu-id="43c48-105">tooinstall Azure PowerShell ve Azure aboneliğinizle ilişkilendirmek için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="43c48-105">tooinstall Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

<span data-ttu-id="43c48-106">Hakkında daha fazla bilgi için [Azure Resource Manager cmdlet'lerini](/powershell/azure/overview), bkz: [Azure PowerShell kullanarak Azure Resource Manager ile](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="43c48-106">For more information about [Azure Resource Manager cmdlets](/powershell/azure/overview), see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

| <span data-ttu-id="43c48-107">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="43c48-107">Cmdlet</span></span> | <span data-ttu-id="43c48-108">Cmdlet açıklaması</span><span class="sxs-lookup"><span data-stu-id="43c48-108">Cmdlet Description</span></span> |
| --- | --- |
| [<span data-ttu-id="43c48-109">AzureRmSchedulerJobCollection devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="43c48-109">Disable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/disable-azurermschedulerjobcollection) |<span data-ttu-id="43c48-110">İş koleksiyonu devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="43c48-110">Disables a job collection.</span></span> |
| [<span data-ttu-id="43c48-111">Enable-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="43c48-111">Enable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/enable-azurermschedulerjobcollection) |<span data-ttu-id="43c48-112">İş koleksiyonu sağlar.</span><span class="sxs-lookup"><span data-stu-id="43c48-112">Enables a job collection.</span></span> |
| [<span data-ttu-id="43c48-113">Get-AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="43c48-113">Get-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjob) |<span data-ttu-id="43c48-114">Zamanlayıcı işlerinin alır.</span><span class="sxs-lookup"><span data-stu-id="43c48-114">Gets Scheduler jobs.</span></span> |
| [<span data-ttu-id="43c48-115">Get-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="43c48-115">Get-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobcollection) |<span data-ttu-id="43c48-116">Alır koleksiyonları işi.</span><span class="sxs-lookup"><span data-stu-id="43c48-116">Gets job collections.</span></span> |
| [<span data-ttu-id="43c48-117">Get-AzureRmSchedulerJobHistory</span><span class="sxs-lookup"><span data-stu-id="43c48-117">Get-AzureRmSchedulerJobHistory</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobhistory) |<span data-ttu-id="43c48-118">Alır geçmişi işi.</span><span class="sxs-lookup"><span data-stu-id="43c48-118">Gets job history.</span></span> |
| [<span data-ttu-id="43c48-119">AzureRmSchedulerHttpJob yeni</span><span class="sxs-lookup"><span data-stu-id="43c48-119">New-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerhttpjob) |<span data-ttu-id="43c48-120">Bir HTTP işi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="43c48-120">Creates an HTTP job.</span></span> |
| [<span data-ttu-id="43c48-121">AzureRmSchedulerJobCollection yeni</span><span class="sxs-lookup"><span data-stu-id="43c48-121">New-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerjobcollection) |<span data-ttu-id="43c48-122">İş koleksiyonu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="43c48-122">Creates a job collection.</span></span> |
| [<span data-ttu-id="43c48-123">AzureRmSchedulerServiceBusQueueJob yeni</span><span class="sxs-lookup"><span data-stu-id="43c48-123">New-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebusqueuejob) |<span data-ttu-id="43c48-124">Bir hizmet veri yolu kuyruğu işi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="43c48-124">Creates a service bus queue job.</span></span> |
| [<span data-ttu-id="43c48-125">AzureRmSchedulerServiceBusTopicJob yeni</span><span class="sxs-lookup"><span data-stu-id="43c48-125">New-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebustopicjob) |<span data-ttu-id="43c48-126">Bir service bus konu işi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="43c48-126">Creates a service bus topic job.</span></span> |
| [<span data-ttu-id="43c48-127">AzureRmSchedulerStorageQueueJob yeni</span><span class="sxs-lookup"><span data-stu-id="43c48-127">New-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerstoragequeuejob) |<span data-ttu-id="43c48-128">Bir depolama kuyruğu işi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="43c48-128">Creates a storage queue job.</span></span> |
| [<span data-ttu-id="43c48-129">Remove-AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="43c48-129">Remove-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjob) |<span data-ttu-id="43c48-130">Scheduler işi kaldırır.</span><span class="sxs-lookup"><span data-stu-id="43c48-130">Removes a Scheduler job.</span></span> |
| [<span data-ttu-id="43c48-131">Remove-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="43c48-131">Remove-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjobcollection) |<span data-ttu-id="43c48-132">İş koleksiyonu kaldırır.</span><span class="sxs-lookup"><span data-stu-id="43c48-132">Removes a job collection.</span></span> |
| [<span data-ttu-id="43c48-133">Set-AzureRmSchedulerHttpJob</span><span class="sxs-lookup"><span data-stu-id="43c48-133">Set-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerhttpjob) |<span data-ttu-id="43c48-134">Bir zamanlayıcı HTTP işi değiştirir.</span><span class="sxs-lookup"><span data-stu-id="43c48-134">Modifies a Scheduler HTTP job.</span></span> |
| [<span data-ttu-id="43c48-135">Set-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="43c48-135">Set-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerjobcollection) |<span data-ttu-id="43c48-136">İş koleksiyonu değiştirir.</span><span class="sxs-lookup"><span data-stu-id="43c48-136">Modifies a job collection.</span></span> |
| [<span data-ttu-id="43c48-137">Set-AzureRmSchedulerServiceBusQueueJob</span><span class="sxs-lookup"><span data-stu-id="43c48-137">Set-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebusqueuejob) |<span data-ttu-id="43c48-138">Hizmet veri yolu kuyruğu işi değiştirir.</span><span class="sxs-lookup"><span data-stu-id="43c48-138">Modifies a service bus queue job.</span></span> |
| [<span data-ttu-id="43c48-139">Set-AzureRmSchedulerServiceBusTopicJob</span><span class="sxs-lookup"><span data-stu-id="43c48-139">Set-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebustopicjob) |<span data-ttu-id="43c48-140">Hizmet veri yolu konusu işi değiştirir.</span><span class="sxs-lookup"><span data-stu-id="43c48-140">Modifies a service bus topic job.</span></span> |
| [<span data-ttu-id="43c48-141">Set-AzureRmSchedulerStorageQueueJob</span><span class="sxs-lookup"><span data-stu-id="43c48-141">Set-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerstoragequeuejob) |<span data-ttu-id="43c48-142">Bir depolama kuyruğu işi değiştirir.</span><span class="sxs-lookup"><span data-stu-id="43c48-142">Modifies a storage queue job.</span></span> |

<span data-ttu-id="43c48-143">Daha ayrıntılı bilgi için aşağıdaki cmdlet'leri hello çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="43c48-143">For more detailed information, you can run any of hello following cmdlets:</span></span> 

```
Get-Help <cmdlet name> -Detailed
```
```
Get-Help <cmdlet name> -Examples
```
```
Get-Help <cmdlet name> -Full
```

## <a name="see-also"></a><span data-ttu-id="43c48-144">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="43c48-144">See Also</span></span>
 [<span data-ttu-id="43c48-145">Scheduler nedir?</span><span class="sxs-lookup"><span data-stu-id="43c48-145">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="43c48-146">Azure Scheduler kavramları, terminolojisi ve varlık hiyerarşisi</span><span class="sxs-lookup"><span data-stu-id="43c48-146">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="43c48-147">Zamanlayıcı hello Azure portalını kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="43c48-147">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="43c48-148">Azure Scheduler’da planlar ve faturalama</span><span class="sxs-lookup"><span data-stu-id="43c48-148">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="43c48-149">Azure Scheduler REST API başvurusu</span><span class="sxs-lookup"><span data-stu-id="43c48-149">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="43c48-150">Yüksek Azure Scheduler kullanılabilirliği ve güvenilirliği</span><span class="sxs-lookup"><span data-stu-id="43c48-150">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="43c48-151">Azure Scheduler sınırları, varsayılanları ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="43c48-151">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="43c48-152">Azure Scheduler giden bağlantı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="43c48-152">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

