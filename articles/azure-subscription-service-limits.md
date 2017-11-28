---
title: "aaaAzure abonelik sınırlarını ve kotaları | Microsoft Docs"
description: "Ortak Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları listesini sağlar. Bu, nasıl tooincrease yanı sıra en yüksek değerleri sınırlar hakkında bilgi içerir."
services: 
documentationcenter: 
author: rothja
manager: jeffreyg
editor: 
tags: billing
ms.assetid: 60d848f9-ff26-496e-a5ec-ccf92ad7d125
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: byvinyal
ms.openlocfilehash: a754d56124520791254ab8f1729808f0750ff222
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a><span data-ttu-id="474fe-104">Azure aboneliği ve hizmet sınırları, kotalar ve kısıtlamalar</span><span class="sxs-lookup"><span data-stu-id="474fe-104">Azure subscription and service limits, quotas, and constraints</span></span>
<span data-ttu-id="474fe-105">Bu belge, bazen kotaları verilen hello en yaygın Microsoft Azure sınırları, bazıları listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="474fe-105">This document lists some of hello most common Microsoft Azure limits, which are also sometimes called quotas.</span></span> <span data-ttu-id="474fe-106">Bu belge şu anda tüm Azure hizmetlerini kapsamaz.</span><span class="sxs-lookup"><span data-stu-id="474fe-106">This document doesn't currently cover all Azure services.</span></span> <span data-ttu-id="474fe-107">Zaman içerisinde, hello listesi genişletilecek ve hello platformun daha fazla toocover güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="474fe-107">Over time, hello list will be expanded and updated toocover more of hello platform.</span></span>

<span data-ttu-id="474fe-108">Lütfen şu adresi ziyaret [Azure fiyatlandırma genel bakış](https://azure.microsoft.com/pricing/) toolearn Azure fiyatlandırma hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="474fe-108">Please visit [Azure Pricing Overview](https://azure.microsoft.com/pricing/) toolearn more about Azure pricing.</span></span> <span data-ttu-id="474fe-109">Burada, hello kullanarak maliyetlerinizi tahmin edebilirsiniz [fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/) veya fiyatlandırma ayrıntıları sayfası bir hizmet için hello ziyaret (örneğin, [Windows VM'ler](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span><span class="sxs-lookup"><span data-stu-id="474fe-109">There, you can estimate your costs using hello [Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) or by visiting hello pricing details page for a service (for example, [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span></span> <span data-ttu-id="474fe-110">Maliyetleriniz için ipuçları toohelp yönetmek için bkz: [Azure faturalama ve maliyet yönetimi ile beklenmeyen maliyetleri önlemek](billing/billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="474fe-110">For tips toohelp manage your costs, see [Prevent unexpected costs with Azure billing and cost management](billing/billing-getting-started.md).</span></span>

> [!NOTE]
> <span data-ttu-id="474fe-111">Tooraise hello sınırı veya hello yukarıda kota isteyip istemediğinizi **varsayılan sınır**, [ücretsiz bir çevrimiçi müşteri destek isteği açma](azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="474fe-111">If you want tooraise hello limit or quota above hello **Default Limit**, [open an online customer support request at no charge](azure-supportability/resource-manager-core-quotas-request.md).</span></span> <span data-ttu-id="474fe-112">Merhaba sınırları hello yükseltilemez **sınırına** tabloları aşağıdaki hello gösterilen değeri.</span><span class="sxs-lookup"><span data-stu-id="474fe-112">hello limits can't be raised above hello **Maximum Limit** value shown in hello following tables.</span></span> <span data-ttu-id="474fe-113">Varsa hiçbir **sınırına** sütununda, ardından hello kaynak ayarlanabilir sınırları sahip değil.</span><span class="sxs-lookup"><span data-stu-id="474fe-113">If there is no **Maximum Limit** column, then hello resource doesn't have adjustable limits.</span></span> 
> 
> <span data-ttu-id="474fe-114">Ücretsiz deneme abonelikleri için sınır uygun olmayan veya kota artırır.</span><span class="sxs-lookup"><span data-stu-id="474fe-114">Free Trial subscriptions are not eligible for limit or quota increases.</span></span> <span data-ttu-id="474fe-115">Ücretsiz deneme sürümü varsa, tooa yükseltebilirsiniz [Kullandıkça Öde](https://azure.microsoft.com/offers/ms-azr-0003p/) abonelik.</span><span class="sxs-lookup"><span data-stu-id="474fe-115">If you have a Free Trial, you can upgrade tooa [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) subscription.</span></span> <span data-ttu-id="474fe-116">Daha fazla bilgi için bkz: [yükseltme Azure ücretsiz deneme sürümü tooPay olarak-size-Git](billing/billing-upgrade-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="474fe-116">For more information, see [Upgrade Azure Free Trial tooPay-As-You-Go](billing/billing-upgrade-azure-subscription.md).</span></span>
> 

## <a name="limits-and-hello-azure-resource-manager"></a><span data-ttu-id="474fe-117">Sınırları ve hello Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="474fe-117">Limits and hello Azure Resource Manager</span></span>
<span data-ttu-id="474fe-118">Olası toocombine sunulmuştur tooa içinde birden çok Azure kaynaklarını tek bir Azure kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="474fe-118">It is now possible toocombine multiple Azure resources in tooa single Azure Resource Group.</span></span> <span data-ttu-id="474fe-119">Kaynak grupları kullanırken, bir kez genel sınırları hello Azure Resource Manager ile bölgesel düzeyde yönetilmesine.</span><span class="sxs-lookup"><span data-stu-id="474fe-119">When using Resource Groups, limits that once were global become managed at a regional level with hello Azure Resource Manager.</span></span> <span data-ttu-id="474fe-120">Azure kaynak grupları hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="474fe-120">For more information about Azure Resource Groups, see [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="474fe-121">Aşağıda, yeni bir tablo hello sınırları eklenen tooreflect sınırları farklılıkları hello Azure Kaynak Yöneticisi'ni kullanırken olmuştur.</span><span class="sxs-lookup"><span data-stu-id="474fe-121">In hello limits below, a new table has been added tooreflect any differences in limits when using hello Azure Resource Manager.</span></span> <span data-ttu-id="474fe-122">Örneğin, bir **abonelik sınırları** tablo ve **abonelik sınırları - Azure Resource Manager** tablo.</span><span class="sxs-lookup"><span data-stu-id="474fe-122">For example, there is a **Subscription Limits** table and a **Subscription Limits - Azure Resource Manager** table.</span></span> <span data-ttu-id="474fe-123">Bir sınır tooboth senaryoları uyguladığında hello ilk tabloda yalnızca gösterilir.</span><span class="sxs-lookup"><span data-stu-id="474fe-123">When a limit applies tooboth scenarios, it is only shown in hello first table.</span></span> <span data-ttu-id="474fe-124">Aksi belirtilmedikçe, tüm bölgeler arasında genel kısıtlamalardır.</span><span class="sxs-lookup"><span data-stu-id="474fe-124">Unless otherwise indicated, limits are global across all regions.</span></span>

> [!NOTE]
> <span data-ttu-id="474fe-125">Merhaba Hizmet Yönetimi kotalar Azure kaynak grupları, kaynaklar için kotalar başına bölge aboneliğinizi tarafından erişilebilir olan ve abonelik başına, olmayan önemli tooemphasize olur.</span><span class="sxs-lookup"><span data-stu-id="474fe-125">It is important tooemphasize that quotas for resources in Azure Resource Groups are per-region accessible by your subscription, and are not per-subscription, as hello service management quotas are.</span></span> <span data-ttu-id="474fe-126">Şimdi çekirdek kotalarını örnek olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="474fe-126">Let's use core quotas as an example.</span></span> <span data-ttu-id="474fe-127">Kota artırma çekirdekleri desteğiyle toorequest gerekiyorsa, toodecide nasıl gereksinim toouse hangi bölgelerde istediğiniz ve ardından Azure kaynak grubu için belirli bir istekte bulunun pek çok çekirdek kotaları çekirdek hello tutarlar ve istediğiniz bölgeler için.</span><span class="sxs-lookup"><span data-stu-id="474fe-127">If you need toorequest a quota increase with support for cores, you need toodecide how many cores you want toouse in which regions, and then make a specific request for Azure Resource Group core quotas for hello amounts and regions that you want.</span></span> <span data-ttu-id="474fe-128">Bu nedenle, toouse 30 gerekiyorsa Batı Avrupa toorun uygulamanız var. çekirdek; Özellikle, Batı Avrupa 30 çekirdeğini istemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="474fe-128">Therefore, if you need toouse 30 cores in West Europe toorun your application there; you should specifically request 30 cores in West Europe.</span></span> <span data-ttu-id="474fe-129">Ancak, diğer herhangi bir bölgede artırmak çekirdek kota sahip olmaz – yalnızca Batı Avrupa hello 30-çekirdek kotası olacak.</span><span class="sxs-lookup"><span data-stu-id="474fe-129">But you will not have a core quota increase in any other region -- only West Europe will have hello 30-core quota.</span></span>
> <!-- -->
> <span data-ttu-id="474fe-130">Sonuç olarak, Azure kaynak grubu kotaları toobe herhangi bir bölge ve istek, içine dağıtım dikkate her bölgede tutar iş yükü gerekenler karar yararlı tooconsider fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="474fe-130">As a result, you may find it useful tooconsider deciding what your Azure Resource Group quotas need toobe for your workload in any one region, and request that amount in each region into which you are considering deployment.</span></span> <span data-ttu-id="474fe-131">Bkz: [dağıtım sorunlarını giderme](resource-manager-common-deployment-errors.md) özel bölgeler için geçerli kotalar keşfetme daha fazla yardım için.</span><span class="sxs-lookup"><span data-stu-id="474fe-131">See [troubleshooting deployment issues](resource-manager-common-deployment-errors.md) for more help discovering your current quotas for specific regions.</span></span>
> 
> 

## <a name="service-specific-limits"></a><span data-ttu-id="474fe-132">Hizmete özgü sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-132">Service-specific limits</span></span>
* [<span data-ttu-id="474fe-133">Active Directory</span><span class="sxs-lookup"><span data-stu-id="474fe-133">Active Directory</span></span>](#active-directory-limits)
* [<span data-ttu-id="474fe-134">API Management</span><span class="sxs-lookup"><span data-stu-id="474fe-134">API Management</span></span>](#api-management-limits)
* [<span data-ttu-id="474fe-135">App Service</span><span class="sxs-lookup"><span data-stu-id="474fe-135">App Service</span></span>](#app-service-limits)
* [<span data-ttu-id="474fe-136">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="474fe-136">Application Gateway</span></span>](#application-gateway-limits)
* [<span data-ttu-id="474fe-137">Application Insights</span><span class="sxs-lookup"><span data-stu-id="474fe-137">Application Insights</span></span>](#application-insights-limits)
* [<span data-ttu-id="474fe-138">Otomasyon</span><span class="sxs-lookup"><span data-stu-id="474fe-138">Automation</span></span>](#automation-limits)
* [<span data-ttu-id="474fe-139">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="474fe-139">Azure Cosmos DB</span></span>](#azure-cosmos-db-limits)
* [<span data-ttu-id="474fe-140">Azure Event kılavuz</span><span class="sxs-lookup"><span data-stu-id="474fe-140">Azure Event Grid</span></span>](#azure-event-grid-limits)
* [<span data-ttu-id="474fe-141">Azure Redis Önbelleği</span><span class="sxs-lookup"><span data-stu-id="474fe-141">Azure Redis Cache</span></span>](#azure-redis-cache-limits)
* [<span data-ttu-id="474fe-142">Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="474fe-142">Azure RemoteApp</span></span>](#azure-remoteapp-limits)
* [<span data-ttu-id="474fe-143">Backup</span><span class="sxs-lookup"><span data-stu-id="474fe-143">Backup</span></span>](#backup-limits)
* [<span data-ttu-id="474fe-144">Batch</span><span class="sxs-lookup"><span data-stu-id="474fe-144">Batch</span></span>](#batch-limits)
* [<span data-ttu-id="474fe-145">BizTalk Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="474fe-145">BizTalk Services</span></span>](#biztalk-services-limits)
* [<span data-ttu-id="474fe-146">CDN</span><span class="sxs-lookup"><span data-stu-id="474fe-146">CDN</span></span>](#cdn-limits)
* [<span data-ttu-id="474fe-147">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="474fe-147">Cloud Services</span></span>](#cloud-services-limits)
* [<span data-ttu-id="474fe-148">Container Instances</span><span class="sxs-lookup"><span data-stu-id="474fe-148">Container Instances</span></span>](#container-instances-limits)
* [<span data-ttu-id="474fe-149">Data Factory</span><span class="sxs-lookup"><span data-stu-id="474fe-149">Data Factory</span></span>](#data-factory-limits)
* [<span data-ttu-id="474fe-150">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="474fe-150">Data Lake Analytics</span></span>](#data-lake-analytics-limits)
* [<span data-ttu-id="474fe-151">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="474fe-151">Data Lake Store</span></span>](#data-lake-store-limits)
* [<span data-ttu-id="474fe-152">DNS</span><span class="sxs-lookup"><span data-stu-id="474fe-152">DNS</span></span>](#dns-limits)
* [<span data-ttu-id="474fe-153">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="474fe-153">Event Hubs</span></span>](#event-hubs-limits)
* [<span data-ttu-id="474fe-154">IoT Hub’ı</span><span class="sxs-lookup"><span data-stu-id="474fe-154">IoT Hub</span></span>](#iot-hub-limits)
* [<span data-ttu-id="474fe-155">Anahtar Kasası</span><span class="sxs-lookup"><span data-stu-id="474fe-155">Key Vault</span></span>](#key-vault-limits)
* [<span data-ttu-id="474fe-156">Günlük analizi / Operational Insights</span><span class="sxs-lookup"><span data-stu-id="474fe-156">Log Analytics / Operational Insights</span></span>](#log-analytics-limits)
* [<span data-ttu-id="474fe-157">Media Services</span><span class="sxs-lookup"><span data-stu-id="474fe-157">Media Services</span></span>](#media-services-limits)
* [<span data-ttu-id="474fe-158">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="474fe-158">Mobile Engagement</span></span>](#mobile-engagement-limits)
* [<span data-ttu-id="474fe-159">Mobil hizmetler</span><span class="sxs-lookup"><span data-stu-id="474fe-159">Mobile Services</span></span>](#mobile-services-limits)
* [<span data-ttu-id="474fe-160">İzleme</span><span class="sxs-lookup"><span data-stu-id="474fe-160">Monitor</span></span>](#monitor-limits)
* [<span data-ttu-id="474fe-161">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="474fe-161">Multi-Factor Authentication</span></span>](#multi-factor-authentication)
* [<span data-ttu-id="474fe-162">Ağ</span><span class="sxs-lookup"><span data-stu-id="474fe-162">Networking</span></span>](#networking-limits)
* [<span data-ttu-id="474fe-163">Ağ İzleyicisi</span><span class="sxs-lookup"><span data-stu-id="474fe-163">Network Watcher</span></span>](#network-watcher-limits)
* [<span data-ttu-id="474fe-164">Bildirim hub'ı hizmeti</span><span class="sxs-lookup"><span data-stu-id="474fe-164">Notification Hub Service</span></span>](#notification-hub-service-limits)
* [<span data-ttu-id="474fe-165">Kaynak Grubu</span><span class="sxs-lookup"><span data-stu-id="474fe-165">Resource Group</span></span>](#resource-group-limits)
* [<span data-ttu-id="474fe-166">Scheduler</span><span class="sxs-lookup"><span data-stu-id="474fe-166">Scheduler</span></span>](#scheduler-limits)
* [<span data-ttu-id="474fe-167">Search</span><span class="sxs-lookup"><span data-stu-id="474fe-167">Search</span></span>](#search-limits)
* [<span data-ttu-id="474fe-168">Service Bus</span><span class="sxs-lookup"><span data-stu-id="474fe-168">Service Bus</span></span>](#service-bus-limits)
* [<span data-ttu-id="474fe-169">Site Recovery</span><span class="sxs-lookup"><span data-stu-id="474fe-169">Site Recovery</span></span>](#site-recovery-limits)
* [<span data-ttu-id="474fe-170">SQL Veritabanı</span><span class="sxs-lookup"><span data-stu-id="474fe-170">SQL Database</span></span>](#sql-database-limits)
* [<span data-ttu-id="474fe-171">Depolama</span><span class="sxs-lookup"><span data-stu-id="474fe-171">Storage</span></span>](#storage-limits)
* [<span data-ttu-id="474fe-172">StorSimple sistemi</span><span class="sxs-lookup"><span data-stu-id="474fe-172">StorSimple System</span></span>](#storsimple-system-limits)
* [<span data-ttu-id="474fe-173">Akış Analizi</span><span class="sxs-lookup"><span data-stu-id="474fe-173">Stream Analytics</span></span>](#stream-analytics-limits)
* [<span data-ttu-id="474fe-174">Abonelik</span><span class="sxs-lookup"><span data-stu-id="474fe-174">Subscription</span></span>](#subscription-limits)
* [<span data-ttu-id="474fe-175">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="474fe-175">Traffic Manager</span></span>](#traffic-manager-limits)
* [<span data-ttu-id="474fe-176">Sanal Makineler</span><span class="sxs-lookup"><span data-stu-id="474fe-176">Virtual Machines</span></span>](#virtual-machines-limits)
* [<span data-ttu-id="474fe-177">Sanal Makine Ölçek Kümeleri</span><span class="sxs-lookup"><span data-stu-id="474fe-177">Virtual Machine Scale Sets</span></span>](#virtual-machine-scale-sets-limits)

### <a name="subscription-limits"></a><span data-ttu-id="474fe-178">Abonelik sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-178">Subscription limits</span></span>
#### <a name="subscription-limits"></a><span data-ttu-id="474fe-179">Abonelik sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-179">Subscription limits</span></span>
[!INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a><span data-ttu-id="474fe-180">Abonelik sınırları - Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="474fe-180">Subscription limits - Azure Resource Manager</span></span>
<span data-ttu-id="474fe-181">sınırları aşağıdaki hello hello Azure Resource Manager ve Azure kaynak gruplarını kullanılırken uygulanır.</span><span class="sxs-lookup"><span data-stu-id="474fe-181">hello following limits apply when using hello Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="474fe-182">Hello Azure Resource Manager ile değişmemiştir sınırları aşağıda listelenen değil.</span><span class="sxs-lookup"><span data-stu-id="474fe-182">Limits that have not changed with hello Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="474fe-183">Lütfen bu sınırları toohello önceki tabloda bakın.</span><span class="sxs-lookup"><span data-stu-id="474fe-183">Please refer toohello previous table for those limits.</span></span>

<span data-ttu-id="474fe-184">Resource Manager istekleri sınırları işleme hakkında daha fazla bilgi için bkz: [azaltma Resource Manager istekleri](resource-manager-request-limits.md).</span><span class="sxs-lookup"><span data-stu-id="474fe-184">For information about handling limits on Resource Manager requests, see [Throttling Resource Manager requests](resource-manager-request-limits.md).</span></span>

[!INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]

### <a name="resource-group-limits"></a><span data-ttu-id="474fe-185">Kaynak grubu sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-185">Resource Group limits</span></span>
[!INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a><span data-ttu-id="474fe-186">Sanal makineler sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-186">Virtual Machines limits</span></span>
#### <a name="virtual-machine-limits"></a><span data-ttu-id="474fe-187">Sanal makine sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-187">Virtual Machine limits</span></span>
[!INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]

#### <a name="virtual-machines-limits---azure-resource-manager"></a><span data-ttu-id="474fe-188">Sanal makineler sınırları - Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="474fe-188">Virtual Machines limits - Azure Resource Manager</span></span>
<span data-ttu-id="474fe-189">sınırları aşağıdaki hello hello Azure Resource Manager ve Azure kaynak gruplarını kullanılırken uygulanır.</span><span class="sxs-lookup"><span data-stu-id="474fe-189">hello following limits apply when using hello Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="474fe-190">Hello Azure Resource Manager ile değişmemiştir sınırları aşağıda listelenen değil.</span><span class="sxs-lookup"><span data-stu-id="474fe-190">Limits that have not changed with hello Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="474fe-191">Lütfen bu sınırları toohello önceki tabloda bakın.</span><span class="sxs-lookup"><span data-stu-id="474fe-191">Please refer toohello previous table for those limits.</span></span>

[!INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a><span data-ttu-id="474fe-192">Sanal makine ölçek kümeleri sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-192">Virtual Machine Scale Sets limits</span></span>
[!INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="container-instances-limits"></a><span data-ttu-id="474fe-193">Kapsayıcı sınırları örnekleri</span><span class="sxs-lookup"><span data-stu-id="474fe-193">Container Instances Limits</span></span>
[!INCLUDE [container-instances-limits](../includes/container-instances-limits.md)]

### <a name="networking-limits"></a><span data-ttu-id="474fe-194">Ağ limitleri</span><span class="sxs-lookup"><span data-stu-id="474fe-194">Networking limits</span></span>
[!INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a><span data-ttu-id="474fe-195">Ağ limitleri</span><span class="sxs-lookup"><span data-stu-id="474fe-195">Networking limits</span></span>
[!INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a><span data-ttu-id="474fe-196">Uygulama ağ geçidi sınırlar</span><span class="sxs-lookup"><span data-stu-id="474fe-196">Application Gateway limits</span></span>
[!INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="network-watcher-limits"></a><span data-ttu-id="474fe-197">Ağ İzleyicisi sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-197">Network Watcher limits</span></span>
[!INCLUDE [network-watcher-limits](../includes/network-watcher-limits.md)]

#### <a name="traffic-manager-limits"></a><span data-ttu-id="474fe-198">Trafik Yöneticisi sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-198">Traffic Manager limits</span></span>
[!INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a><span data-ttu-id="474fe-199">DNS sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-199">DNS limits</span></span>
[!INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a><span data-ttu-id="474fe-200">Depolama sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-200">Storage limits</span></span>
<span data-ttu-id="474fe-201">Depolama hesabı sınırları hakkında daha fazla ayrıntı için bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage/common/storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="474fe-201">For additional details on storage account limits, see [Azure Storage Scalability and Performance Targets](storage/common/storage-scalability-targets.md).</span></span>
<!--like # storage accts --> 
#### <a name="storage-service-limits"></a><span data-ttu-id="474fe-202">Depolama hizmet sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-202">Storage Service limits</span></span>
[!INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
#### <a name="virtual-machine-disk-limits"></a><span data-ttu-id="474fe-203">Sanal makine disk sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-203">Virtual machine disk limits</span></span> 
[!INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

<span data-ttu-id="474fe-204">Bkz: [sanal makine boyutlarını](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ek ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="474fe-204">See [Virtual machine sizes](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional details.</span></span>

#### <a name="managed-virtual-machine-disks"></a><span data-ttu-id="474fe-205">Yönetilen sanal makine disklerini</span><span class="sxs-lookup"><span data-stu-id="474fe-205">Managed virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-managed](../includes/azure-storage-limits-vm-disks-managed.md)]

#### <a name="unmanaged-virtual-machine-disks"></a><span data-ttu-id="474fe-206">Yönetilmeyen sanal makine disklerini</span><span class="sxs-lookup"><span data-stu-id="474fe-206">Unmanaged virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a><span data-ttu-id="474fe-207">Depolama kaynak sağlayıcısı sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-207">Storage Resource Provider limits</span></span>
[!INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]

### <a name="cloud-services-limits"></a><span data-ttu-id="474fe-208">Bulut Hizmetleri sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-208">Cloud Services limits</span></span>
[!INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]

### <a name="app-service-limits"></a><span data-ttu-id="474fe-209">Uygulama hizmeti sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-209">App Service limits</span></span>
<span data-ttu-id="474fe-210">Uygulama hizmeti sınırları hello sınırları Web Apps, Mobile Apps, API Apps ve Logic Apps için şunlardır.</span><span class="sxs-lookup"><span data-stu-id="474fe-210">hello following App Service limits include limits for Web Apps, Mobile Apps, API Apps, and Logic Apps.</span></span>

[!INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a><span data-ttu-id="474fe-211">Scheduler sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-211">Scheduler limits</span></span>
[!INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a><span data-ttu-id="474fe-212">Toplu iş sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-212">Batch limits</span></span>
[!INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

### <a name="biztalk-services-limits"></a><span data-ttu-id="474fe-213">BizTalk Services sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-213">BizTalk Services limits</span></span>
<span data-ttu-id="474fe-214">Merhaba aşağıdaki tabloda hello sınırları için Azure Biztalk Services gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="474fe-214">hello following table shows hello limits for Azure Biztalk Services.</span></span>

[!INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]

### <a name="azure-cosmos-db-limits"></a><span data-ttu-id="474fe-215">Azure Cosmos DB sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-215">Azure Cosmos DB limits</span></span>
<span data-ttu-id="474fe-216">Azure Cosmos DB hangi işleme ve depolama ölçeklendirilmiş toohandle ne olursa olsun uygulamanızın gerektirdiği olabilir bir küresel ölçekteki veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="474fe-216">Azure Cosmos DB is a global scale database in which throughput and storage can be scaled toohandle whatever your application requires.</span></span> <span data-ttu-id="474fe-217">Azure Cosmos DB sağlar hello ölçek hakkında sorularınız varsa lütfen e-posta Gönder tooaskcosmosdb@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="474fe-217">If you have any questions about hello scale Azure Cosmos DB provides, please send email tooaskcosmosdb@microsoft.com.</span></span>

### <a name="mobile-engagement-limits"></a><span data-ttu-id="474fe-218">Mobile Engagement sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-218">Mobile Engagement limits</span></span>
[!INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]

### <a name="search-limits"></a><span data-ttu-id="474fe-219">Arama sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-219">Search limits</span></span>
<span data-ttu-id="474fe-220">Fiyatlandırma katmanlarına hello kapasite ve arama hizmetinizi sınırları belirler.</span><span class="sxs-lookup"><span data-stu-id="474fe-220">Pricing tiers determine hello capacity and limits of your search service.</span></span> <span data-ttu-id="474fe-221">Katmanları mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="474fe-221">Tiers include:</span></span>

* <span data-ttu-id="474fe-222">*Ücretsiz* diğer Azure aboneleriyle paylaşılan çok kiracılı hizmeti projeleri değerlendirme ve küçük geliştirme için amaçlar.</span><span class="sxs-lookup"><span data-stu-id="474fe-222">*Free* multi-tenant service, shared with other Azure subscribers, intended for evaluation and small development projects.</span></span>
* <span data-ttu-id="474fe-223">*Temel* özel bilgi işlem kaynakları daha küçük ölçekli üretim iş yükleri için yüksek oranda kullanılabilir sorgu iş yükleri için toothree çoğaltmaları yukarı sağlar.</span><span class="sxs-lookup"><span data-stu-id="474fe-223">*Basic* provides dedicated computing resources for production workloads at a smaller scale, with up toothree replicas for highly available query workloads.</span></span>
* <span data-ttu-id="474fe-224">*Standart (S1, S2, S3, S3 yüksek yoğunluk)* büyük üretim iş yükleri için değil.</span><span class="sxs-lookup"><span data-stu-id="474fe-224">*Standard (S1, S2, S3, S3 High Density)* is for larger production workloads.</span></span> <span data-ttu-id="474fe-225">İş yükü profilinizi en iyi şekilde eşleşen bir kaynak yapılandırması seçebilmeniz hello standart katman içinde birden çok düzeyi yok.</span><span class="sxs-lookup"><span data-stu-id="474fe-225">Multiple levels exist within hello standard tier so that you can choose a resource configuration that best matches your workload profile.</span></span>

<span data-ttu-id="474fe-226">**Abonelik başına sınırları**</span><span class="sxs-lookup"><span data-stu-id="474fe-226">**Limits per subscription**</span></span>

[!INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

<span data-ttu-id="474fe-227">**Arama hizmeti başına sınırları**</span><span class="sxs-lookup"><span data-stu-id="474fe-227">**Limits per search service**</span></span>

[!INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

<span data-ttu-id="474fe-228">Belge boyutu, sorguları ikinci, anahtarları, istekleri ve yanıtları, her gibi daha ayrıntılı bir düzeyde sınırları hakkında daha fazla toolearn bkz [hizmet sınırları Azure Search'te](search/search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="474fe-228">toolearn more about limits on a more granular level, such as document size, queries per second, keys, requests, and responses, see [Service limits in Azure Search](search/search-limits-quotas-capacity.md).</span></span>

### <a name="media-services-limits"></a><span data-ttu-id="474fe-229">Media Services sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-229">Media Services limits</span></span>
[!INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a><span data-ttu-id="474fe-230">CDN sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-230">CDN limits</span></span>
[!INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a><span data-ttu-id="474fe-231">Mobile Services sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-231">Mobile Services limits</span></span>
[!INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitor-limits"></a><span data-ttu-id="474fe-232">İzleyici sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-232">Monitor limits</span></span>
[!INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a><span data-ttu-id="474fe-233">Bildirim hub'ı hizmet sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-233">Notification Hub Service limits</span></span>
[!INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a><span data-ttu-id="474fe-234">Olay hub'ları sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-234">Event Hubs limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a><span data-ttu-id="474fe-235">Hizmet veri yolu sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-235">Service Bus limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a><span data-ttu-id="474fe-236">IOT hub'ı sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-236">IoT Hub limits</span></span>
[!INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a><span data-ttu-id="474fe-237">Veri Fabrikası sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-237">Data Factory limits</span></span>
[!INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a><span data-ttu-id="474fe-238">Data Lake Analytics sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-238">Data Lake Analytics limits</span></span>
[!INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="data-lake-store-limits"></a><span data-ttu-id="474fe-239">Data Lake Store sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-239">Data Lake Store limits</span></span>
[!INCLUDE [azure-data-lake-store-limits](../includes/azure-data-lake-store-limits.md)]

### <a name="stream-analytics-limits"></a><span data-ttu-id="474fe-240">Akış analizi sınırlar</span><span class="sxs-lookup"><span data-stu-id="474fe-240">Stream Analytics limits</span></span>
[!INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a><span data-ttu-id="474fe-241">Active Directory sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-241">Active Directory limits</span></span>
[!INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]

### <a name="azure-event-grid-limits"></a><span data-ttu-id="474fe-242">Azure olay kılavuz sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-242">Azure Event Grid limits</span></span>
[!INCLUDE [event-grid-limits](../includes/event-grid-limits.md)]

### <a name="azure-remoteapp-limits"></a><span data-ttu-id="474fe-243">Azure RemoteApp sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-243">Azure RemoteApp limits</span></span>
[!INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a><span data-ttu-id="474fe-244">StorSimple sistemi sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-244">StorSimple System limits</span></span>
[!INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]

### <a name="log-analytics-limits"></a><span data-ttu-id="474fe-245">Günlük analizi sınırlar</span><span class="sxs-lookup"><span data-stu-id="474fe-245">Log Analytics limits</span></span>
[!INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a><span data-ttu-id="474fe-246">Yedekleme sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-246">Backup limits</span></span>
[!INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a><span data-ttu-id="474fe-247">Site Recovery limitleri</span><span class="sxs-lookup"><span data-stu-id="474fe-247">Site Recovery limits</span></span>
[!INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a><span data-ttu-id="474fe-248">Uygulama Öngörüler sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-248">Application Insights limits</span></span>
[!INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a><span data-ttu-id="474fe-249">API Management sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-249">API Management limits</span></span>
[!INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a><span data-ttu-id="474fe-250">Azure Redis önbelleği sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-250">Azure Redis Cache limits</span></span>
[!INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a><span data-ttu-id="474fe-251">Anahtar kasası sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-251">Key Vault limits</span></span>
[!INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a><span data-ttu-id="474fe-252">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="474fe-252">Multi-Factor Authentication</span></span>
[!INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a><span data-ttu-id="474fe-253">Otomasyon sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-253">Automation limits</span></span>
[!INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a><span data-ttu-id="474fe-254">SQL veritabanı sınırları</span><span class="sxs-lookup"><span data-stu-id="474fe-254">SQL Database limits</span></span>
<span data-ttu-id="474fe-255">SQL veritabanı sınırları için bkz: [SQL veritabanı kaynak sınırları](sql-database/sql-database-resource-limits.md).</span><span class="sxs-lookup"><span data-stu-id="474fe-255">For SQL Database limits, see [SQL Database Resource Limits](sql-database/sql-database-resource-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="474fe-256">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="474fe-256">See also</span></span>
[<span data-ttu-id="474fe-257">Azure sınırları ve artar anlama</span><span class="sxs-lookup"><span data-stu-id="474fe-257">Understanding Azure Limits and Increases</span></span>](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[<span data-ttu-id="474fe-258">Sanal makine ve bulut hizmeti boyutları Azure</span><span class="sxs-lookup"><span data-stu-id="474fe-258">Virtual Machine and Cloud Service Sizes for Azure</span></span>](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="474fe-259">Cloud Services boyutları</span><span class="sxs-lookup"><span data-stu-id="474fe-259">Sizes for Cloud Services</span></span>](cloud-services/cloud-services-sizes-specs.md)

