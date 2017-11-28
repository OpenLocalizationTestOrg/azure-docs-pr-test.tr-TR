---
title: Azure Scheduler aaaWhat mi? | Microsoft Belgeleri
description: "Azure Zamanlayıcı verir toodeclaratively Eylemler toorun hello bulutta açıklanmaktadır. Sonra, bu eylemleri otomatik olarak zamanlar ve çalıştırır."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 52aa6ae1-4c3d-43fb-81b0-6792c84bcfae
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 062e25ae473510264dc0038198c05e7ac1e86210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-scheduler"></a><span data-ttu-id="7a0c0-105">Azure Scheduler nedir?</span><span class="sxs-lookup"><span data-stu-id="7a0c0-105">What is Azure Scheduler?</span></span>
<span data-ttu-id="7a0c0-106">Azure Zamanlayıcı verir toodeclaratively Eylemler toorun hello bulutta açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7a0c0-106">Azure Scheduler allows you toodeclaratively describe actions toorun in hello cloud.</span></span> <span data-ttu-id="7a0c0-107">Sonra, bu eylemleri otomatik olarak zamanlar ve çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="7a0c0-107">It then schedules and runs those actions automatically.</span></span>  <span data-ttu-id="7a0c0-108">Zamanlayıcı olmadığından bu kullanarak [Azure portal hello](scheduler-get-started-portal.md), kod, [REST API](https://msdn.microsoft.com/library/mt629143.aspx), ya da Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7a0c0-108">Scheduler does this by using [hello Azure portal](scheduler-get-started-portal.md), code, [REST API](https://msdn.microsoft.com/library/mt629143.aspx), or Azure PowerShell.</span></span>

<span data-ttu-id="7a0c0-109">Scheduler zamanlanan iş oluşturur, korur ve çağırır.</span><span class="sxs-lookup"><span data-stu-id="7a0c0-109">Scheduler creates, maintains, and invokes scheduled work.</span></span>  <span data-ttu-id="7a0c0-110">Scheduler iş yükü barındırmaz ya da kod çalıştırmaz.</span><span class="sxs-lookup"><span data-stu-id="7a0c0-110">Scheduler does not host any workloads or run any code.</span></span> <span data-ttu-id="7a0c0-111">Yalnızca başka bir yerde (Azure’da, şirket içi ya da başka sağlayıcıda) barındırılan kodu *çağırır*.</span><span class="sxs-lookup"><span data-stu-id="7a0c0-111">It only *invokes* code hosted elsewhere—in Azure, on-premises, or with another provider.</span></span> <span data-ttu-id="7a0c0-112">HTTP, HTTPS, depolama kuyruğu, hizmet veri yolu kuyruğu ya da hizmet veri yolu konusu aracılığıyla çağırır.</span><span class="sxs-lookup"><span data-stu-id="7a0c0-112">It invokes via HTTP, HTTPS, a storage queue, a service bus queue, or a service bus topic.</span></span>

<span data-ttu-id="7a0c0-113">Zamanlayıcı zamanlamaları [işleri](scheduler-concepts-terms.md), bir gözden geçirebileceğiniz ve kesin ve güvenilir bir şekilde zamanlamaları iş yükleri toobe çalıştırın iş yürütme sonuçlarının geçmişini tutar.</span><span class="sxs-lookup"><span data-stu-id="7a0c0-113">Scheduler schedules [jobs](scheduler-concepts-terms.md), keeps a history of job execution results that one can review, and deterministically and reliably schedules workloads toobe run.</span></span> <span data-ttu-id="7a0c0-114">Azure WebJobs (Azure App Service Web Apps özelliğini hello parçası) ve diğer Azure zamanlama özellikleri hello arka planda Zamanlayıcısı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7a0c0-114">Azure WebJobs (part of hello Web Apps feature in Azure App Service) and other Azure scheduling capabilities use Scheduler in hello background.</span></span> <span data-ttu-id="7a0c0-115">Merhaba [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx) hello bu eylemler için iletişimi yönetmeye yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7a0c0-115">hello [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx) helps manage hello communication for these actions.</span></span> <span data-ttu-id="7a0c0-116">Bu şekilde, Scheduler kolayca [karmaşık zamanlamalar ve gelişmiş yineleme oluşturmayı](scheduler-advanced-complexity.md) destekler.</span><span class="sxs-lookup"><span data-stu-id="7a0c0-116">As such, Scheduler supports [complex schedules and advanced recurrence](scheduler-advanced-complexity.md) easily.</span></span>

<span data-ttu-id="7a0c0-117">Kendilerini Scheduler toohello kullanımını ödünç birkaç senaryo vardır.</span><span class="sxs-lookup"><span data-stu-id="7a0c0-117">There are several scenarios that lend themselves toohello usage of Scheduler.</span></span> <span data-ttu-id="7a0c0-118">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="7a0c0-118">For example:</span></span>

* <span data-ttu-id="7a0c0-119">*Yinelenen uygulama eylemleri:* Twitter’dan akışa düzenli aralıklarla veri toplama.</span><span class="sxs-lookup"><span data-stu-id="7a0c0-119">*Recurring application actions:* Periodically gathering data from Twitter into a feed.</span></span>
* <span data-ttu-id="7a0c0-120">*Günlük bakım:* Günlüklerin günlük ayıklanması, yedeklemelerin ve diğer bakım görevlerinin gerçekleştirilmesi.</span><span class="sxs-lookup"><span data-stu-id="7a0c0-120">*Daily maintenance:* Daily pruning of logs, performing backups, and other maintenance tasks.</span></span> <span data-ttu-id="7a0c0-121">Örneğin, bir yönetici tooback hello veritabanını 1: 00'da tercih edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7a0c0-121">For example, an administrator may choose tooback up hello database at 1:00 A.M.</span></span> <span data-ttu-id="7a0c0-122">her gün hello için sonraki dokuz ay.</span><span class="sxs-lookup"><span data-stu-id="7a0c0-122">every day for hello next nine months.</span></span>

<span data-ttu-id="7a0c0-123">Zamanlayıcı toocreate sağlar, Güncelleştir, Sil, görüntülemek ve işlerini yönetmek ve [iş koleksiyonları](scheduler-concepts-terms.md) komut dosyalarını kullanarak programlı ve hello Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="7a0c0-123">Scheduler allows you toocreate, update, delete, view, and manage jobs and [job collections](scheduler-concepts-terms.md) programmatically, by using scripts, and in hello portal.</span></span>

## <a name="see-also"></a><span data-ttu-id="7a0c0-124">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="7a0c0-124">See also</span></span>
 [<span data-ttu-id="7a0c0-125">Azure Scheduler kavramları, terminolojisi ve varlık hiyerarşisi</span><span class="sxs-lookup"><span data-stu-id="7a0c0-125">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="7a0c0-126">Zamanlayıcı hello Azure portalını kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="7a0c0-126">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="7a0c0-127">Azure Scheduler’da planlar ve faturalama</span><span class="sxs-lookup"><span data-stu-id="7a0c0-127">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="7a0c0-128">Nasıl toobuild karmaşık zamanlar ve Gelişmiş yineleme Azure Scheduler ile</span><span class="sxs-lookup"><span data-stu-id="7a0c0-128">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="7a0c0-129">Azure Scheduler REST API başvurusu</span><span class="sxs-lookup"><span data-stu-id="7a0c0-129">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="7a0c0-130">Azure Scheduler PowerShell cmdlet’leri başvurusu</span><span class="sxs-lookup"><span data-stu-id="7a0c0-130">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="7a0c0-131">Yüksek Azure Scheduler kullanılabilirliği ve güvenilirliği</span><span class="sxs-lookup"><span data-stu-id="7a0c0-131">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="7a0c0-132">Azure Scheduler sınırları, varsayılanları ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="7a0c0-132">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="7a0c0-133">Azure Scheduler giden bağlantı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="7a0c0-133">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

