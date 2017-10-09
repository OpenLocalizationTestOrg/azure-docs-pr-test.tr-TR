---
title: "Azure Redis önbelleği aaaHow tooconfigure | Microsoft Docs"
description: "Azure Redis önbelleği için Hello varsayılan Redis yapılandırma anlamak ve nasıl tooconfigure Azure Redis öğrenin önbellek örneklerinde"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: d0bf2e1f-6a26-4e62-85ba-d82b35fc5aa6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 08/22/2017
ms.author: sdanie
ms.openlocfilehash: 46bffb74cdf40e0e0a99c3a83dbe06d6fe1ea65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-azure-redis-cache"></a><span data-ttu-id="e8a91-103">Nasıl tooconfigure Azure Redis önbelleği</span><span class="sxs-lookup"><span data-stu-id="e8a91-103">How tooconfigure Azure Redis Cache</span></span>
<span data-ttu-id="e8a91-104">Bu konuda, Azure Redis önbelleği örnekleri için yapılandırma ve Azure Redis önbelleği örnekleri için kapsar hello varsayılan Redis sunucu yapılandırması nasıl tooreview ve güncelleştirme hello açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e8a91-104">This topic describes how tooreview and update hello configuration for your Azure Redis Cache instances, and covers hello default Redis server configuration for Azure Redis Cache instances.</span></span>

> [!NOTE]
> <span data-ttu-id="e8a91-105">Yapılandırma ve premium önbellek özellikleri kullanma hakkında daha fazla bilgi için bkz: [nasıl tooconfigure kalıcılığı](cache-how-to-premium-persistence.md), [nasıl kümeleme tooconfigure](cache-how-to-premium-clustering.md), ve [tooconfigure sanal ağ'ı nasıl destekler ](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="e8a91-105">For more information on configuring and using premium cache features, see [How tooconfigure persistence](cache-how-to-premium-persistence.md), [How tooconfigure clustering](cache-how-to-premium-clustering.md), and [How tooconfigure Virtual Network support](cache-how-to-premium-vnet.md).</span></span>
> 
> 

## <a name="configure-redis-cache-settings"></a><span data-ttu-id="e8a91-106">Redis önbelleği ayarları</span><span class="sxs-lookup"><span data-stu-id="e8a91-106">Configure Redis cache settings</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="e8a91-107">Azure Redis önbelleği ayarları görüntülenebilir ve hello üzerinde yapılandırılmış **Redis önbelleği** hello kullanarak dikey **kaynak menü**.</span><span class="sxs-lookup"><span data-stu-id="e8a91-107">Azure Redis Cache settings are viewed and configured on hello **Redis Cache** blade using hello **Resource Menu**.</span></span>

![Redis önbelleği ayarları](./media/cache-configure/redis-cache-settings.png)

<span data-ttu-id="e8a91-109">Görüntüleyebilir ve ayarlarını hello kullanarak aşağıdaki hello yapılandırabilirsiniz **kaynak menü**.</span><span class="sxs-lookup"><span data-stu-id="e8a91-109">You can view and configure hello following settings using hello **Resource Menu**.</span></span>

* [<span data-ttu-id="e8a91-110">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e8a91-110">Overview</span></span>](#overview)
* [<span data-ttu-id="e8a91-111">Etkinlik Günlüğü</span><span class="sxs-lookup"><span data-stu-id="e8a91-111">Activity log</span></span>](#activity-log)
* [<span data-ttu-id="e8a91-112">Erişim denetimi (IAM)</span><span class="sxs-lookup"><span data-stu-id="e8a91-112">Access control (IAM)</span></span>](#access-control-iam)
* [<span data-ttu-id="e8a91-113">Etiketler</span><span class="sxs-lookup"><span data-stu-id="e8a91-113">Tags</span></span>](#tags)
* [<span data-ttu-id="e8a91-114">Sorunları tanılama ve çözme</span><span class="sxs-lookup"><span data-stu-id="e8a91-114">Diagnose and solve problems</span></span>](#diagnose-and-solve-problems)
* [<span data-ttu-id="e8a91-115">Ayarlar</span><span class="sxs-lookup"><span data-stu-id="e8a91-115">Settings</span></span>](#settings)
    * [<span data-ttu-id="e8a91-116">Erişim tuşları</span><span class="sxs-lookup"><span data-stu-id="e8a91-116">Access keys</span></span>](#access-keys)
    * [<span data-ttu-id="e8a91-117">Gelişmiş ayarlar</span><span class="sxs-lookup"><span data-stu-id="e8a91-117">Advanced settings</span></span>](#advanced-settings)
    * [<span data-ttu-id="e8a91-118">Redis önbelleği Danışmanı</span><span class="sxs-lookup"><span data-stu-id="e8a91-118">Redis Cache Advisor</span></span>](#redis-cache-advisor)
    * [<span data-ttu-id="e8a91-119">Ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="e8a91-119">Scale</span></span>](#scale)
    * [<span data-ttu-id="e8a91-120">Küme boyutu redis</span><span class="sxs-lookup"><span data-stu-id="e8a91-120">Redis cluster size</span></span>](#cluster-size)
    * [<span data-ttu-id="e8a91-121">Redis veri kalıcılığını</span><span class="sxs-lookup"><span data-stu-id="e8a91-121">Redis data persistence</span></span>](#redis-data-persistence)
    * [<span data-ttu-id="e8a91-122">Güncelleştirmeleri zamanlama</span><span class="sxs-lookup"><span data-stu-id="e8a91-122">Schedule updates</span></span>](#schedule-updates)
    * [<span data-ttu-id="e8a91-123">Coğrafi çoğaltma</span><span class="sxs-lookup"><span data-stu-id="e8a91-123">Geo-replication</span></span>](#geo-replication)
    * [<span data-ttu-id="e8a91-124">Sanal Ağ</span><span class="sxs-lookup"><span data-stu-id="e8a91-124">Virtual Network</span></span>](#virtual-network)
    * [<span data-ttu-id="e8a91-125">Güvenlik duvarı</span><span class="sxs-lookup"><span data-stu-id="e8a91-125">Firewall</span></span>](#firewall)
    * [<span data-ttu-id="e8a91-126">Özellikleri</span><span class="sxs-lookup"><span data-stu-id="e8a91-126">Properties</span></span>](#properties)
    * [<span data-ttu-id="e8a91-127">Kilitler</span><span class="sxs-lookup"><span data-stu-id="e8a91-127">Locks</span></span>](#locks)
    * [<span data-ttu-id="e8a91-128">Otomasyon komut dosyası</span><span class="sxs-lookup"><span data-stu-id="e8a91-128">Automation script</span></span>](#automation-script)
* [<span data-ttu-id="e8a91-129">Yönetim</span><span class="sxs-lookup"><span data-stu-id="e8a91-129">Administration</span></span>](#administration)
    * [<span data-ttu-id="e8a91-130">Veri alma</span><span class="sxs-lookup"><span data-stu-id="e8a91-130">Import data</span></span>](#importexport)
    * [<span data-ttu-id="e8a91-131">Verileri dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="e8a91-131">Export data</span></span>](#importexport)
    * [<span data-ttu-id="e8a91-132">Yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="e8a91-132">Reboot</span></span>](#reboot)
* [<span data-ttu-id="e8a91-133">İzleme</span><span class="sxs-lookup"><span data-stu-id="e8a91-133">Monitoring</span></span>](#monitoring)
    * [<span data-ttu-id="e8a91-134">Ölçümleri redis</span><span class="sxs-lookup"><span data-stu-id="e8a91-134">Redis metrics</span></span>](#redis-metrics)
    * [<span data-ttu-id="e8a91-135">Uyarı kuralları</span><span class="sxs-lookup"><span data-stu-id="e8a91-135">Alert rules</span></span>](#alert-rules)
    * [<span data-ttu-id="e8a91-136">Tanılama</span><span class="sxs-lookup"><span data-stu-id="e8a91-136">Diagnostics</span></span>](#diagnostics)
* [<span data-ttu-id="e8a91-137">Destek ve sorun giderme ayarları</span><span class="sxs-lookup"><span data-stu-id="e8a91-137">Support & troubleshooting settings</span></span>](#support-amp-troubleshooting-settings)
    * [<span data-ttu-id="e8a91-138">Kaynak durumu</span><span class="sxs-lookup"><span data-stu-id="e8a91-138">Resource health</span></span>](#resource-health)
    * [<span data-ttu-id="e8a91-139">Yeni destek isteği</span><span class="sxs-lookup"><span data-stu-id="e8a91-139">New support request</span></span>](#new-support-request)


## <a name="overview"></a><span data-ttu-id="e8a91-140">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e8a91-140">Overview</span></span>

<span data-ttu-id="e8a91-141">**Genel Bakış** , fiyatlandırma katmanı ve seçilen önbellek ölçümleri adı gibi önbelleğiniz hakkında temel bilgileri sizinle bağlantı noktaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8a91-141">**Overview** provides you with basic information about your cache, such as name, ports, pricing tier, and selected cache metrics.</span></span>

### <a name="activity-log"></a><span data-ttu-id="e8a91-142">Etkinlik günlüğü</span><span class="sxs-lookup"><span data-stu-id="e8a91-142">Activity log</span></span>

<span data-ttu-id="e8a91-143">Tıklatın **etkinlik günlüğü** tooview eylemleri önbelleğiniz üzerinde.</span><span class="sxs-lookup"><span data-stu-id="e8a91-143">Click **Activity log** tooview actions performed on your cache.</span></span> <span data-ttu-id="e8a91-144">Bu görünüm tooinclude filtreleme tooexpand de kullanabilirsiniz diğer kaynakları.</span><span class="sxs-lookup"><span data-stu-id="e8a91-144">You can also use filtering tooexpand this view tooinclude other resources.</span></span> <span data-ttu-id="e8a91-145">Denetim günlükleri ile çalışma hakkında daha fazla bilgi için bkz: [denetim işlemleri Resource Manager ile](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="e8a91-145">For more information on working with audit logs, see [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md).</span></span> <span data-ttu-id="e8a91-146">Azure Redis önbelleği olaylar izleme hakkında daha fazla bilgi için bkz: [işlemleri ve Uyarıları](cache-how-to-monitor.md#operations-and-alerts).</span><span class="sxs-lookup"><span data-stu-id="e8a91-146">For more information on monitoring Azure Redis Cache events, see [Operations and alerts](cache-how-to-monitor.md#operations-and-alerts).</span></span>

### <a name="access-control-iam"></a><span data-ttu-id="e8a91-147">Erişim denetimi (IAM)</span><span class="sxs-lookup"><span data-stu-id="e8a91-147">Access control (IAM)</span></span>

<span data-ttu-id="e8a91-148">Merhaba **erişim denetimi (IAM)** bölüm desteği sağlar. rol tabanlı erişim denetimi (RBAC) hello Azure portal toohelp kuruluşlar karşılamak erişim yönetimi gereksinimlerine sadece ve tam olarak.</span><span class="sxs-lookup"><span data-stu-id="e8a91-148">hello **Access control (IAM)** section provides support for role-based access control (RBAC) in hello Azure portal toohelp organizations meet their access management requirements simply and precisely.</span></span> <span data-ttu-id="e8a91-149">Daha fazla bilgi için bkz: [hello Azure portalında rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e8a91-149">For more information, see [Role-based access control in hello Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>

### <a name="tags"></a><span data-ttu-id="e8a91-150">Etiketler</span><span class="sxs-lookup"><span data-stu-id="e8a91-150">Tags</span></span>

<span data-ttu-id="e8a91-151">Merhaba **etiketleri** bölüm kaynaklarınızı düzenlemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="e8a91-151">hello **Tags** section helps you organize your resources.</span></span> <span data-ttu-id="e8a91-152">Daha fazla bilgi için bkz: [kullanarak Azure kaynaklarınızı tooorganize etiketler](../azure-resource-manager/resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="e8a91-152">For more information, see [Using tags tooorganize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>


### <a name="diagnose-and-solve-problems"></a><span data-ttu-id="e8a91-153">Sorunları tanılama ve çözme</span><span class="sxs-lookup"><span data-stu-id="e8a91-153">Diagnose and solve problems</span></span>

<span data-ttu-id="e8a91-154">Tıklatın **Tanıla ve sorunları** ortak sorunlar ve stratejileri çözümlemek için sağlanan toobe.</span><span class="sxs-lookup"><span data-stu-id="e8a91-154">Click **Diagnose and solve problems** toobe provided with common issues and strategies for resolving them.</span></span>



## <a name="settings"></a><span data-ttu-id="e8a91-155">Ayarlar</span><span class="sxs-lookup"><span data-stu-id="e8a91-155">Settings</span></span>
<span data-ttu-id="e8a91-156">Merhaba **ayarları** bölüm tooaccess sağlar ve önbelleğiniz için ayarları aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e8a91-156">hello **Settings** section allows you tooaccess and configure hello following settings for your cache.</span></span>

* [<span data-ttu-id="e8a91-157">Erişim tuşları</span><span class="sxs-lookup"><span data-stu-id="e8a91-157">Access keys</span></span>](#access-keys)
* [<span data-ttu-id="e8a91-158">Gelişmiş ayarlar</span><span class="sxs-lookup"><span data-stu-id="e8a91-158">Advanced settings</span></span>](#advanced-settings)
* [<span data-ttu-id="e8a91-159">Redis önbelleği Danışmanı</span><span class="sxs-lookup"><span data-stu-id="e8a91-159">Redis Cache Advisor</span></span>](#redis-cache-advisor)
* [<span data-ttu-id="e8a91-160">Ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="e8a91-160">Scale</span></span>](#scale)
* [<span data-ttu-id="e8a91-161">Küme boyutu redis</span><span class="sxs-lookup"><span data-stu-id="e8a91-161">Redis cluster size</span></span>](#cluster-size)
* [<span data-ttu-id="e8a91-162">Redis veri kalıcılığını</span><span class="sxs-lookup"><span data-stu-id="e8a91-162">Redis data persistence</span></span>](#redis-data-persistence)
* [<span data-ttu-id="e8a91-163">Güncelleştirmeleri zamanlama</span><span class="sxs-lookup"><span data-stu-id="e8a91-163">Schedule updates</span></span>](#schedule-updates)
* [<span data-ttu-id="e8a91-164">Coğrafi çoğaltma</span><span class="sxs-lookup"><span data-stu-id="e8a91-164">Geo-replication</span></span>](#geo-replication)
* [<span data-ttu-id="e8a91-165">Sanal Ağ</span><span class="sxs-lookup"><span data-stu-id="e8a91-165">Virtual Network</span></span>](#virtual-network)
* [<span data-ttu-id="e8a91-166">Güvenlik duvarı</span><span class="sxs-lookup"><span data-stu-id="e8a91-166">Firewall</span></span>](#firewall)
* [<span data-ttu-id="e8a91-167">Özellikleri</span><span class="sxs-lookup"><span data-stu-id="e8a91-167">Properties</span></span>](#properties)
* [<span data-ttu-id="e8a91-168">Kilitler</span><span class="sxs-lookup"><span data-stu-id="e8a91-168">Locks</span></span>](#locks)
* [<span data-ttu-id="e8a91-169">Otomasyon komut dosyası</span><span class="sxs-lookup"><span data-stu-id="e8a91-169">Automation script</span></span>](#automation-script)



### <a name="access-keys"></a><span data-ttu-id="e8a91-170">Erişim tuşları</span><span class="sxs-lookup"><span data-stu-id="e8a91-170">Access keys</span></span>
<span data-ttu-id="e8a91-171">Tıklatın **erişim anahtarları** tooview veya yeniden hello erişim tuşları önbelleğiniz için.</span><span class="sxs-lookup"><span data-stu-id="e8a91-171">Click **Access keys** tooview or regenerate hello access keys for your cache.</span></span> <span data-ttu-id="e8a91-172">Bu anahtarlar tooyour önbellek bağlanan hello istemcileri tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e8a91-172">These keys are used by hello clients connecting tooyour cache.</span></span>

![Redis önbelleği erişim tuşları](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a><span data-ttu-id="e8a91-174">Gelişmiş ayarlar</span><span class="sxs-lookup"><span data-stu-id="e8a91-174">Advanced settings</span></span>
<span data-ttu-id="e8a91-175">Merhaba aşağıdaki ayarları hello üzerinde yapılandırılmış **Gelişmiş ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="e8a91-175">hello following settings are configured on hello **Advanced settings** blade.</span></span>

* [<span data-ttu-id="e8a91-176">Erişim bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="e8a91-176">Access Ports</span></span>](#access-ports)
* [<span data-ttu-id="e8a91-177">Bellek ilkeleri</span><span class="sxs-lookup"><span data-stu-id="e8a91-177">Memory policies</span></span>](#memory-policies)
* [<span data-ttu-id="e8a91-178">Keyspace bildirimleri (Gelişmiş ayarları)</span><span class="sxs-lookup"><span data-stu-id="e8a91-178">Keyspace notifications (advanced settings)</span></span>](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a><span data-ttu-id="e8a91-179">Erişim bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="e8a91-179">Access Ports</span></span>
<span data-ttu-id="e8a91-180">SSL olmayan erişim yeni önbellekler için varsayılan olarak devre dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="e8a91-180">By default, non-SSL access is disabled for new caches.</span></span> <span data-ttu-id="e8a91-181">tooenable hello SSL olmayan bağlantı noktası, tıklatın **Hayır** için **yalnızca SSL aracılığıyla erişime izin ver** hello üzerinde **Gelişmiş ayarları** dikey ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="e8a91-181">tooenable hello non-SSL port, click **No** for **Allow access only via SSL** on hello **Advanced settings** blade and then click **Save**.</span></span>

![Redis önbelleği erişim bağlantı noktaları](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a><span data-ttu-id="e8a91-183">Bellek ilkeleri</span><span class="sxs-lookup"><span data-stu-id="e8a91-183">Memory policies</span></span>
<span data-ttu-id="e8a91-184">Merhaba **Maxmemory İlkesi**, **maxmemory ayrılmış**, ve **maxfragmentationmemory ayrılmış** hello ayarlarını **Gelişmiş ayarları**dikey penceresinde hello bellek ilkeleri hello önbelleği için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e8a91-184">hello **Maxmemory policy**, **maxmemory-reserved**, and **maxfragmentationmemory-reserved** settings on hello **Advanced settings** blade configure hello memory policies for hello cache.</span></span>

![Redis önbelleği Maxmemory İlkesi](./media/cache-configure/redis-cache-maxmemory-policy.png)

<span data-ttu-id="e8a91-186">**Maxmemory İlkesi** hello çıkarma İlkesi hello önbelleği için yapılandırır ve çıkarma ilkelere hello gelen toochoose sağlar:</span><span class="sxs-lookup"><span data-stu-id="e8a91-186">**Maxmemory policy** configures hello eviction policy for hello cache and allows you toochoose from hello following eviction policies:</span></span>

* <span data-ttu-id="e8a91-187">`volatile-lru`-Bu hello varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="e8a91-187">`volatile-lru` - this is hello default.</span></span>
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

<span data-ttu-id="e8a91-188">Hakkında daha fazla bilgi için `maxmemory` ilkeleri Bkz [çıkarma ilkeleri](http://redis.io/topics/lru-cache#eviction-policies).</span><span class="sxs-lookup"><span data-stu-id="e8a91-188">For more information about `maxmemory` policies, see [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies).</span></span>

<span data-ttu-id="e8a91-189">Merhaba **maxmemory ayrılmış** ayarı, MB olarak çoğaltma yük devretme sırasında gibi önbellek olmayan işlemleri için ayrılmış bellek miktarı hello yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="e8a91-189">hello **maxmemory-reserved** setting configures hello amount of memory in MB that is reserved for non-cache operations such as replication during failover.</span></span> <span data-ttu-id="e8a91-190">Bu değer ayarlandığında yük değişiklik gösterdiğinde toohave daha tutarlı bir Redis sunucu deneyim da sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8a91-190">Setting this value allows you toohave a more consistent Redis server experience when your load varies.</span></span> <span data-ttu-id="e8a91-191">Bu değer ağır yazma iş yükleri için yüksek ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-191">This value should be set higher for workloads that are write heavy.</span></span> <span data-ttu-id="e8a91-192">Bu tür işlemler için ayrılmış bellek, önbelleğe alınan veri depolama için kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="e8a91-192">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="e8a91-193">Merhaba **maxfragmentationmemory ayrılmış** ayarı, MB olarak bellek parçalanması için ayrılmış tooaccommodate olan hello bellek miktarını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="e8a91-193">hello **maxfragmentationmemory-reserved** setting configures hello amount of memory in MB that is reserved tooaccommodate for memory fragmentation.</span></span> <span data-ttu-id="e8a91-194">Bu değer ayarlandığında toohave daha tutarlı bir Redis sunucu deneyim hello önbellek dolu veya kapat toofull ve hello parçalanma oranı de yüksek olduğunda izin verir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-194">Setting this value allows you toohave a more consistent Redis server experience when hello cache is full or close toofull and hello fragmentation ratio is also high.</span></span> <span data-ttu-id="e8a91-195">Bu tür işlemler için ayrılmış bellek, önbelleğe alınan veri depolama için kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="e8a91-195">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="e8a91-196">Yeni bir bellek ayırma değeri seçerken tek şey tooconsider (**maxmemory ayrılmış** veya **maxfragmentationmemory ayrılmış**) ile çalışan bir önbellek bu değişiklik nasıl etkileyebileceğini olduğu büyük miktarlarda veri da.</span><span class="sxs-lookup"><span data-stu-id="e8a91-196">One thing tooconsider when choosing a new memory reservation value (**maxmemory-reserved** or **maxfragmentationmemory-reserved**) is how this change might affect a cache that is already running with large amounts of data in it.</span></span> <span data-ttu-id="e8a91-197">49 GB veri 53 GB'a önbellekle sahip ardından hello ayırma değeri too8 GB değiştirin, örneğin, bu too45 GB aşağı hello sistemi için en fazla kullanılabilir bellek hello bırakılmasına neden olacak.</span><span class="sxs-lookup"><span data-stu-id="e8a91-197">For instance, if you have a 53 GB cache with 49 GB of data, then change hello reservation value too8 GB, this will drop hello max available memory for hello system down too45 GB.</span></span> <span data-ttu-id="e8a91-198">Her iki geçerli `used_memory` veya `used_memory_rss` değerlerdir hello yeni 45 GB sınırından daha sonra hello sistem tooevict veri sahip olacak kadar her ikisi de `used_memory` ve `used_memory_rss` 45 GB olan.</span><span class="sxs-lookup"><span data-stu-id="e8a91-198">If either your current `used_memory` or your `used_memory_rss` values are higher than hello new limit of 45 GB, then hello system will have tooevict data until both `used_memory` and `used_memory_rss` are below 45 GB.</span></span> <span data-ttu-id="e8a91-199">Çıkarma sunucu yükü ve bellek parçalanması artırabilir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-199">Eviction can increase server load and memory fragmentation.</span></span> <span data-ttu-id="e8a91-200">Önbellek ölçümleri gibi hakkında daha fazla bilgi için `used_memory` ve `used_memory_rss`, bkz: [kullanılabilir Ölçümler ve aralıklarını raporlama](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span><span class="sxs-lookup"><span data-stu-id="e8a91-200">For more information on cache metrics such as `used_memory` and `used_memory_rss`, see [Available metrics and reporting intervals](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8a91-201">Merhaba **maxmemory ayrılmış** ve **maxfragmentationmemory ayrılmış** ayarlarını bulunan ve yalnızca için standart ve Premium önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="e8a91-201">hello **maxmemory-reserved** and **maxfragmentationmemory-reserved** settings are only available for Standard and Premium caches.</span></span>
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a><span data-ttu-id="e8a91-202">Keyspace bildirimleri (Gelişmiş ayarları)</span><span class="sxs-lookup"><span data-stu-id="e8a91-202">Keyspace notifications (advanced settings)</span></span>
<span data-ttu-id="e8a91-203">Keyspace bildirimleri hello üzerinde yapılandırılmış olan redis **Gelişmiş ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="e8a91-203">Redis keyspace notifications are configured on hello **Advanced settings** blade.</span></span> <span data-ttu-id="e8a91-204">Belirli olaylar oluştuğunda Keyspace bildirimleri istemcileri tooreceive bildirimlerine izin verin.</span><span class="sxs-lookup"><span data-stu-id="e8a91-204">Keyspace notifications allow clients tooreceive notifications when certain events occur.</span></span>

![Redis önbelleği Gelişmiş ayarlar](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> <span data-ttu-id="e8a91-206">Keyspace bildirimleri ve hello **bildir-keyspace-olayları** ayarı bulunan ve yalnızca standart ve Premium önbellekler için.</span><span class="sxs-lookup"><span data-stu-id="e8a91-206">Keyspace notifications and hello **notify-keyspace-events** setting are only available for Standard and Premium caches.</span></span>
> 
> 

<span data-ttu-id="e8a91-207">Daha fazla bilgi için bkz: [Redis Keyspace bildirimleri](http://redis.io/topics/notifications).</span><span class="sxs-lookup"><span data-stu-id="e8a91-207">For more information, see [Redis Keyspace Notifications](http://redis.io/topics/notifications).</span></span> <span data-ttu-id="e8a91-208">Örnek kod için bkz: Merhaba [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) hello dosyasında [Merhaba Dünya](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) örnek.</span><span class="sxs-lookup"><span data-stu-id="e8a91-208">For sample code, see hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) file in hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a><span data-ttu-id="e8a91-209">Redis önbelleği Danışmanı</span><span class="sxs-lookup"><span data-stu-id="e8a91-209">Redis Cache Advisor</span></span>
<span data-ttu-id="e8a91-210">Merhaba **Redis önbelleği Danışmanı** dikey önbelleğiniz için öneriler görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e8a91-210">hello **Redis Cache Advisor** blade displays recommendations for your cache.</span></span> <span data-ttu-id="e8a91-211">Normal işlemler sırasında öneri yok görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-211">During normal operations, no recommendations are displayed.</span></span> 

![Öneriler](./media/cache-configure/redis-cache-no-recommendations.png)

<span data-ttu-id="e8a91-213">Önbelleğinizin yüksek bellek kullanımı, ağ bant genişliği veya sunucu iş yükü gibi hello işlemleri sırasında tüm koşullar meydana gelirse, bir uyarı hello üzerinde görüntülenir **Redis önbelleği** dikey.</span><span class="sxs-lookup"><span data-stu-id="e8a91-213">If any conditions occur during hello operations of your cache such as high memory usage, network bandwidth, or server load, an alert is displayed on hello **Redis Cache** blade.</span></span>

![Öneriler](./media/cache-configure/redis-cache-recommendations-alert.png)

<span data-ttu-id="e8a91-215">Merhaba hakkında daha fazla bilgi bulunabilir **önerileri** dikey.</span><span class="sxs-lookup"><span data-stu-id="e8a91-215">Further information can be found on hello **Recommendations** blade.</span></span>

![Öneriler](./media/cache-configure/redis-cache-recommendations.png)

<span data-ttu-id="e8a91-217">Bu ölçümleri hello izleyebilirsiniz [izleme grafikleri](cache-how-to-monitor.md#monitoring-charts) ve [kullanım grafiklerini](cache-how-to-monitor.md#usage-charts) hello bölümlerini **Redis önbelleği** dikey.</span><span class="sxs-lookup"><span data-stu-id="e8a91-217">You can monitor these metrics on hello [Monitoring charts](cache-how-to-monitor.md#monitoring-charts) and [Usage charts](cache-how-to-monitor.md#usage-charts) sections of hello **Redis Cache** blade.</span></span>

<span data-ttu-id="e8a91-218">Her fiyatlandırma katmanının istemci bağlantıları, bellek ve bant genişliği için farklı sınırları vardır.</span><span class="sxs-lookup"><span data-stu-id="e8a91-218">Each pricing tier has different limits for client connections, memory, and bandwidth.</span></span> <span data-ttu-id="e8a91-219">Bir öneri, önbelleğiniz aralıksız bir süre boyunca Bu ölçümler için maksimum kapasite yaklaşıyor değilse oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e8a91-219">If your cache approaches maximum capacity for these metrics over a sustained period of time, a recommendation is created.</span></span> <span data-ttu-id="e8a91-220">Merhaba ölçümleri ve hello tarafından gözden sınırları hakkında daha fazla bilgi için **önerileri** aracı, aşağıdaki tablonun hello bakın:</span><span class="sxs-lookup"><span data-stu-id="e8a91-220">For more information about hello metrics and limits reviewed by hello **Recommendations** tool, see hello following table:</span></span>

| <span data-ttu-id="e8a91-221">Redis önbelleği ölçüm</span><span class="sxs-lookup"><span data-stu-id="e8a91-221">Redis Cache metric</span></span> | <span data-ttu-id="e8a91-222">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="e8a91-222">More information</span></span> |
| --- | --- |
| <span data-ttu-id="e8a91-223">Ağ bant genişliği kullanımı</span><span class="sxs-lookup"><span data-stu-id="e8a91-223">Network bandwidth usage</span></span> |[<span data-ttu-id="e8a91-224">Önbellek performansı - kullanılabilir bant genişliği</span><span class="sxs-lookup"><span data-stu-id="e8a91-224">Cache performance - available bandwidth</span></span>](cache-faq.md#cache-performance) |
| <span data-ttu-id="e8a91-225">Bağlanan istemciler</span><span class="sxs-lookup"><span data-stu-id="e8a91-225">Connected clients</span></span> |[<span data-ttu-id="e8a91-226">Redis sunucu yapılandırması - maxclients varsayılan</span><span class="sxs-lookup"><span data-stu-id="e8a91-226">Default Redis server configuration - maxclients</span></span>](#maxclients) |
| <span data-ttu-id="e8a91-227">Sunucu iş yükü</span><span class="sxs-lookup"><span data-stu-id="e8a91-227">Server load</span></span> |[<span data-ttu-id="e8a91-228">Kullanım grafikler - Redis sunucu iş yükü</span><span class="sxs-lookup"><span data-stu-id="e8a91-228">Usage charts - Redis Server Load</span></span>](cache-how-to-monitor.md#usage-charts) |
| <span data-ttu-id="e8a91-229">Bellek kullanımı</span><span class="sxs-lookup"><span data-stu-id="e8a91-229">Memory usage</span></span> |[<span data-ttu-id="e8a91-230">Önbellek performansı - boyutu</span><span class="sxs-lookup"><span data-stu-id="e8a91-230">Cache performance - size</span></span>](cache-faq.md#cache-performance) |

<span data-ttu-id="e8a91-231">tooupgrade, önbellek tıklatın **Şimdi Yükselt** toochange hello fiyatlandırma katmanı ve [ölçek](#scale) önbelleğiniz.</span><span class="sxs-lookup"><span data-stu-id="e8a91-231">tooupgrade your cache, click **Upgrade now** toochange hello pricing tier and [scale](#scale) your cache.</span></span> <span data-ttu-id="e8a91-232">Bir fiyatlandırma katmanı seçme hakkında daha fazla bilgi için bkz: [hangi Redis önbelleği teklifini ve boyutunu kullanmalıyım?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span><span class="sxs-lookup"><span data-stu-id="e8a91-232">For more information on choosing a pricing tier, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span></span>


### <a name="scale"></a><span data-ttu-id="e8a91-233">Ölçek</span><span class="sxs-lookup"><span data-stu-id="e8a91-233">Scale</span></span>
<span data-ttu-id="e8a91-234">Tıklatın **ölçek** fiyatlandırma katmanı önbelleğiniz için tooview ya da değişiklik hello.</span><span class="sxs-lookup"><span data-stu-id="e8a91-234">Click **Scale** tooview or change hello pricing tier for your cache.</span></span> <span data-ttu-id="e8a91-235">Ölçeklendirme ile ilgili daha fazla bilgi için bkz: [nasıl tooScale Azure Redis önbelleği](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="e8a91-235">For more information on scaling, see [How tooScale Azure Redis Cache](cache-how-to-scale.md).</span></span>

![Redis önbelleği fiyatlandırma katmanı](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a><span data-ttu-id="e8a91-237">Küme boyutu redis</span><span class="sxs-lookup"><span data-stu-id="e8a91-237">Redis Cluster Size</span></span>
<span data-ttu-id="e8a91-238">Tıklatın **(Önizleme) Redis küme boyutu** önbellek toochange hello küme boyutu çalışan premium için kümeleme özelliği etkinleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="e8a91-238">Click **(PREVIEW) Redis Cluster Size** toochange hello cluster size for a running premium cache with clustering enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="e8a91-239">Merhaba katmanı bırakıldı Azure Redis önbelleği Premium sırasında tooGeneral kullanılabilirlik, hello Redis küme boyutu özelliği yayımlanan şu anda önizlemede olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e8a91-239">Note that while hello Azure Redis Cache Premium tier has been released tooGeneral Availability, hello Redis Cluster Size feature is currently in preview.</span></span>
> 
> 

![Küme boyutu redis](./media/cache-configure/redis-cache-redis-cluster-size.png)

<span data-ttu-id="e8a91-241">toochange hello küme boyutu, hello kaydırıcıyı kullanın veya hello 1 ile 10 arasında bir sayı yazın **parça sayısı** metin kutusu ve tıklatın **Tamam** toosave.</span><span class="sxs-lookup"><span data-stu-id="e8a91-241">toochange hello cluster size, use hello slider or type a number between 1 and 10 in hello **Shard count** text box and click **OK** toosave.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8a91-242">Redis kümeleme yalnızca Premium önbellekler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-242">Redis clustering is only available for Premium caches.</span></span> <span data-ttu-id="e8a91-243">Daha fazla bilgi için bkz: [nasıl bir Premium Azure Redis önbelleği için kümeleri tooconfigure](cache-how-to-premium-clustering.md).</span><span class="sxs-lookup"><span data-stu-id="e8a91-243">For more information, see [How tooconfigure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>
> 
> 


### <a name="redis-data-persistence"></a><span data-ttu-id="e8a91-244">Redis veri kalıcılığını</span><span class="sxs-lookup"><span data-stu-id="e8a91-244">Redis data persistence</span></span>
<span data-ttu-id="e8a91-245">Tıklatın **Redis veri kalıcılığını** tooenable, devre dışı bırakın ya da premium önbelleğiniz veri kalıcılığını yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="e8a91-245">Click **Redis data persistence** tooenable, disable, or configure data persistence for your premium cache.</span></span> <span data-ttu-id="e8a91-246">Azure Redis önbelleği Redis kalıcılığı kullanarak sunar [RDB kalıcılığı](cache-how-to-premium-persistence.md#configure-rdb-persistence) veya [AOF kalıcılığı](cache-how-to-premium-persistence.md#configure-aof-persistence).</span><span class="sxs-lookup"><span data-stu-id="e8a91-246">Azure Redis Cache offers Redis persistence using either [RDB persistence](cache-how-to-premium-persistence.md#configure-rdb-persistence) or [AOF persistence](cache-how-to-premium-persistence.md#configure-aof-persistence).</span></span>

<span data-ttu-id="e8a91-247">Daha fazla bilgi için bkz: [nasıl Premium Azure Redis önbelleği için kalıcılığı tooconfigure](cache-how-to-premium-persistence.md).</span><span class="sxs-lookup"><span data-stu-id="e8a91-247">For more information, see [How tooconfigure persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="e8a91-248">Redis veri kalıcılığını yalnızca Premium önbellekler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-248">Redis data persistence is only available for Premium caches.</span></span> 
> 
> 

### <a name="schedule-updates"></a><span data-ttu-id="e8a91-249">Güncelleştirmeleri zamanlama</span><span class="sxs-lookup"><span data-stu-id="e8a91-249">Schedule updates</span></span>
<span data-ttu-id="e8a91-250">Merhaba **zamanlama güncelleştirmeleri** dikey toodesignate önbelleğiniz için Redis server güncelleştirmeleri için bir bakım penceresi sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8a91-250">hello **Schedule updates** blade allows you toodesignate a maintenance window for Redis server updates for your cache.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e8a91-251">Merhaba bakım penceresi yalnızca tooRedis server güncelleştirmeleri ve değil Azure güncelleştirir veya hello önbelleği barındırmak hello VM'lerin toohello işletim sistemi güncelleştirmelerini tooany geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-251">hello maintenance window applies only tooRedis server updates, and not tooany Azure updates or updates toohello operating system of hello VMs that host hello cache.</span></span>
> 
> 

![Güncelleştirmeleri zamanlama](./media/cache-configure/redis-schedule-updates.png)

<span data-ttu-id="e8a91-253">toospecify bir bakım penceresi istenen hello gün kontrol edin ve her gün için hello bakım penceresi başlangıç saati belirtin ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e8a91-253">toospecify a maintenance window, check hello desired days and specify hello maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="e8a91-254">Merhaba bakım penceresi saati UTC biçiminde olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e8a91-254">Note that hello maintenance window time is in UTC.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e8a91-255">Merhaba **zamanlama güncelleştirmeleri** işlevdir yalnızca Premium katmanı önbellekler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-255">hello **Schedule updates** functionality is only available for Premium tier caches.</span></span> <span data-ttu-id="e8a91-256">Daha fazla bilgi ve yönergeler için bkz: [Azure Redis önbelleği yönetim - güncelleştirmeleri zamanla](cache-administration.md#schedule-updates).</span><span class="sxs-lookup"><span data-stu-id="e8a91-256">For more information and instructions, see [Azure Redis Cache administration - Schedule updates](cache-administration.md#schedule-updates).</span></span>
> 
> 

### <a name="geo-replication"></a><span data-ttu-id="e8a91-257">Coğrafi çoğaltma</span><span class="sxs-lookup"><span data-stu-id="e8a91-257">Geo-replication</span></span>

<span data-ttu-id="e8a91-258">Merhaba **coğrafi çoğaltma** dikey iki Premium katmanı Azure Redis önbelleği örnekleri bağlama için bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8a91-258">hello **Geo-replication** blade provides a mechanism for linking two Premium tier Azure Redis Cache instances.</span></span> <span data-ttu-id="e8a91-259">Bir önbellek hello birincil bağlantılı önbellek ve hello hello ikincil bağlantılı önbelleği gibi diğer olarak atanır.</span><span class="sxs-lookup"><span data-stu-id="e8a91-259">One cache is designated as hello primary linked cache, and hello other as hello secondary linked cache.</span></span> <span data-ttu-id="e8a91-260">Merhaba ikincil bağlantılı önbellek salt okunur olur ve yazılı toohello birincil önbelleği veri toohello ikincil bağlantılı önbellek çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="e8a91-260">hello secondary linked cache becomes read-only, and data written toohello primary cache is replicated toohello secondary linked cache.</span></span> <span data-ttu-id="e8a91-261">Bu işlev Azure bölgeler arasında kullanılan tooreplicate bir önbellek olabilir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-261">This functionality can be used tooreplicate a cache across Azure regions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8a91-262">**Coğrafi çoğaltma** yalnızca Premium katmanı önbellekler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-262">**Geo-replication** is only available for Premium tier caches.</span></span> <span data-ttu-id="e8a91-263">Daha fazla bilgi ve yönergeler için bkz: [nasıl Azure Redis önbelleği için coğrafi çoğaltma tooconfigure](cache-how-to-geo-replication.md).</span><span class="sxs-lookup"><span data-stu-id="e8a91-263">For more information and instructions, see [How tooconfigure Geo-replication for Azure Redis Cache](cache-how-to-geo-replication.md).</span></span>
> 
> 

### <a name="virtual-network"></a><span data-ttu-id="e8a91-264">Sanal Ağ</span><span class="sxs-lookup"><span data-stu-id="e8a91-264">Virtual Network</span></span>
<span data-ttu-id="e8a91-265">Merhaba **sanal ağ** bölümü önbelleğiniz için tooconfigure hello sanal ağ ayarlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8a91-265">hello **Virtual Network** section allows you tooconfigure hello virtual network settings for your cache.</span></span> <span data-ttu-id="e8a91-266">VNET ile birlikte premium önbelleği oluşturma hakkında bilgi için destek ve ayarlarını güncelleştirmek, bkz: [tooconfigure sanal ağ desteği nasıl Premium Azure Redis önbelleği için](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="e8a91-266">For information on creating a premium cache with VNET support and updating its settings, see [How tooconfigure Virtual Network Support for a Premium Azure Redis Cache](cache-how-to-premium-vnet.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8a91-267">Sanal ağ ayarları yapılandırıldı premium önbelleklere kullanılabilir yalnızca önbellek oluşturma sırasında VNET desteğiyle.</span><span class="sxs-lookup"><span data-stu-id="e8a91-267">Virtual network settings are only available for premium caches that were configured with VNET support during cache creation.</span></span> 
> 
> 

### <a name="firewall"></a><span data-ttu-id="e8a91-268">Güvenlik duvarı</span><span class="sxs-lookup"><span data-stu-id="e8a91-268">Firewall</span></span>

<span data-ttu-id="e8a91-269">Tıklatın **Güvenlik Duvarı** tooview, Premium Azure Redis önbelleği için güvenlik duvarı kuralları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e8a91-269">Click **Firewall** tooview and configure firewall rules for your Premium Azure Redis Cache.</span></span>

![Güvenlik duvarı](./media/cache-configure/redis-firewall-rules.png)

<span data-ttu-id="e8a91-271">Güvenlik duvarı kuralları ile bir başlangıç ve bitiş IP adresi aralığı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8a91-271">You can specify firewall rules with a start and end IP address range.</span></span> <span data-ttu-id="e8a91-272">Güvenlik duvarı kuralları yapılandırıldığında, IP adres aralıklarını toohello önbellek bağlanabilir yalnızca hello'ten istemci bağlantılarını belirtildi.</span><span class="sxs-lookup"><span data-stu-id="e8a91-272">When firewall rules are configured, only client connections from hello specified IP address ranges can connect toohello cache.</span></span> <span data-ttu-id="e8a91-273">Bir güvenlik duvarı kuralı kaydedildiğinde vardır kısa bir gecikme hello kural etkilidir önce.</span><span class="sxs-lookup"><span data-stu-id="e8a91-273">When a firewall rule is saved there is a short delay before hello rule is effective.</span></span> <span data-ttu-id="e8a91-274">Bu gecikme, normal bir dakikadan az olur.</span><span class="sxs-lookup"><span data-stu-id="e8a91-274">This delay is typically less than one minute.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8a91-275">Güvenlik duvarı kuralları yapılandırılmış olsa bile Azure Redis önbelleği sistemleri izleme bağlantılarından her zaman, izin verilir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-275">Connections from Azure Redis Cache monitoring systems are always permitted, even if firewall rules are configured.</span></span>
> 
> <span data-ttu-id="e8a91-276">Güvenlik duvarı kuralları yalnızca Premium katmanı önbellekler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-276">Firewall rules are only available for Premium tier caches.</span></span>
> 
> 

### <a name="properties"></a><span data-ttu-id="e8a91-277">Özellikler</span><span class="sxs-lookup"><span data-stu-id="e8a91-277">Properties</span></span>
<span data-ttu-id="e8a91-278">Tıklatın **özellikleri** hello önbellek uç noktası ve bağlantı noktaları da dahil olmak üzere önbelleğiniz hakkında tooview bilgi.</span><span class="sxs-lookup"><span data-stu-id="e8a91-278">Click **Properties** tooview information about your cache, including hello cache endpoint and ports.</span></span>

![Redis önbelleği özellikleri](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a><span data-ttu-id="e8a91-280">Kilitler</span><span class="sxs-lookup"><span data-stu-id="e8a91-280">Locks</span></span>
<span data-ttu-id="e8a91-281">Merhaba **kilitler** bölümü sağlar, size, toolock bir abonelik, kaynak grubu veya kaynak tooprevent yanlışlıkla silinmesi ya da kritik kaynaklara değiştirme kuruluşunuzdaki diğer kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="e8a91-281">hello **Locks** section allows you toolock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="e8a91-282">Daha fazla bilgi için bkz. [Azure Resource Manager ile kaynakları kilitleme](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="e8a91-282">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

### <a name="automation-script"></a><span data-ttu-id="e8a91-283">Otomasyon komut dosyası</span><span class="sxs-lookup"><span data-stu-id="e8a91-283">Automation script</span></span>

<span data-ttu-id="e8a91-284">Tıklatın **Otomasyon betiğini** toobuild ve dağıtılmış kaynaklarınızın gelecekteki dağıtımlar için şablonu dışarı aktarma.</span><span class="sxs-lookup"><span data-stu-id="e8a91-284">Click **Automation script** toobuild and export a template of your deployed resources for future deployments.</span></span> <span data-ttu-id="e8a91-285">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [kaynakları Azure Resource Manager şablonları ile dağıtma](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e8a91-285">For more information about working with templates, see [Deploy resources with Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

## <a name="administration-settings"></a><span data-ttu-id="e8a91-286">Yönetim ayarları</span><span class="sxs-lookup"><span data-stu-id="e8a91-286">Administration settings</span></span>
<span data-ttu-id="e8a91-287">Merhaba hello ayarlarında **Yönetim** bölüm önbelleğiniz için yönetim görevleri aşağıdaki tooperform hello izin.</span><span class="sxs-lookup"><span data-stu-id="e8a91-287">hello settings in hello **Administration** section allow you tooperform hello following administrative tasks for your cache.</span></span> 

![Yönetim](./media/cache-configure/redis-cache-administration.png)

* [<span data-ttu-id="e8a91-289">Veri alma</span><span class="sxs-lookup"><span data-stu-id="e8a91-289">Import data</span></span>](#importexport)
* [<span data-ttu-id="e8a91-290">Verileri dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="e8a91-290">Export data</span></span>](#importexport)
* [<span data-ttu-id="e8a91-291">Yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="e8a91-291">Reboot</span></span>](#reboot)


### <a name="importexport"></a><span data-ttu-id="e8a91-292">İçeri/Dışarı Aktarma</span><span class="sxs-lookup"><span data-stu-id="e8a91-292">Import/Export</span></span>
<span data-ttu-id="e8a91-293">İçeri/dışarı aktarma alma ve Redis önbelleği veritabanı'nı (RDB) anlık bir Azure depolama hesabındaki premium önbellek tooa sayfa blobu dışarı aktarma tarafından hello önbelleğinde tooimport ve dışarı aktarma veri sağlayan bir Azure Redis önbelleği veri yönetimi, bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-293">Import/Export is an Azure Redis Cache data management operation, which allows you tooimport and export data in hello cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache tooa page blob in an Azure Storage Account.</span></span> <span data-ttu-id="e8a91-294">İçeri/dışarı aktarma farklı Azure Redis önbelleği örnekleri arasında toomigrate etkinleştirir veya hello önbellek kullanmadan önce verilerle doldurma.</span><span class="sxs-lookup"><span data-stu-id="e8a91-294">Import/Export enables you toomigrate between different Azure Redis Cache instances or populate hello cache with data before use.</span></span>

<span data-ttu-id="e8a91-295">İçeri aktarma kullanılan toobring Redis uyumlu RDB dosyalarından herhangi bir bulut veya ortamını Linux, Windows ya da herhangi bir bulut sağlayıcısına Amazon Web Hizmetleri ve diğerleri gibi çalışan Redis çalıştıran herhangi bir Redis sunucu olabilir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-295">Import can be used toobring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="e8a91-296">Veri alma kolay bir yolu toocreate önceden doldurulmuş haldedir verilerle bir önbellek olur.</span><span class="sxs-lookup"><span data-stu-id="e8a91-296">Importing data is an easy way toocreate a cache with pre-populated data.</span></span> <span data-ttu-id="e8a91-297">Merhaba içeri aktarma işlemi sırasında Azure Redis önbelleği hello RDB dosyaları Azure Storage'dan belleğe yükler ve sonra hello anahtarları hello önbelleğine ekler.</span><span class="sxs-lookup"><span data-stu-id="e8a91-297">During hello import process, Azure Redis Cache loads hello RDB files from Azure storage into memory, and then inserts hello keys into hello cache.</span></span>

<span data-ttu-id="e8a91-298">Dışarı aktarma Azure Redis önbelleği tooRedis uyumlu RDB dosyalarında depolanan tooexport hello verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8a91-298">Export allows you tooexport hello data stored in Azure Redis Cache tooRedis compatible RDB files.</span></span> <span data-ttu-id="e8a91-299">Bu özellik toomove verilerden bir Azure Redis önbelleği örneği tooanother veya tooanother Redis sunucusu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8a91-299">You can use this feature toomove data from one Azure Redis Cache instance tooanother or tooanother Redis server.</span></span> <span data-ttu-id="e8a91-300">Hello dışa aktarma işlemi sırasında Azure Redis önbelleği sunucu örneği konakları hello ve depolama hesabı belirlenmiş karşıya yüklenen toohello hello dosyadır VM hello üzerinde geçici bir dosya oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e8a91-300">During hello export process, a temporary file is created on hello VM that hosts hello Azure Redis Cache server instance, and hello file is uploaded toohello designated storage account.</span></span> <span data-ttu-id="e8a91-301">Merhaba dışa aktarma işlemi ya da durumunu başarı veya hata ile tamamlandığında hello geçici dosya silindi.</span><span class="sxs-lookup"><span data-stu-id="e8a91-301">When hello export operation completes with either a status of success or failure, hello temporary file is deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8a91-302">İçeri/dışarı aktarma yalnızca Premium katmanı önbellekler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-302">Import/Export is only available for Premium tier caches.</span></span> <span data-ttu-id="e8a91-303">Daha fazla bilgi ve yönergeler için bkz: [içeri ve dışarı aktarma Azure Redis önbelleği verilerde](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="e8a91-303">For more information and instructions, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

### <a name="reboot"></a><span data-ttu-id="e8a91-304">Yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="e8a91-304">Reboot</span></span>
<span data-ttu-id="e8a91-305">Merhaba **yeniden** dikey tooreboot hello önbelleğiniz düğümlerinin sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8a91-305">hello **Reboot** blade allows you tooreboot hello nodes of your cache.</span></span> <span data-ttu-id="e8a91-306">Bir önbellek düğümü ise bu yeniden başlatma yeteneği, tootest, uygulamanız için esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8a91-306">This reboot capability enables you tootest your application for resiliency if there is a failure of a cache node.</span></span>

![Yeniden başlatma](./media/cache-configure/redis-cache-reboot.png)

<span data-ttu-id="e8a91-308">Kümeleme özelliği etkinleştirilmiş bir premium önbelleği varsa, hangi parça hello önbellek tooreboot birini seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8a91-308">If you have a premium cache with clustering enabled, you can select which shards of hello cache tooreboot.</span></span>

![Yeniden başlatma](./media/cache-configure/redis-cache-reboot-cluster.png)

<span data-ttu-id="e8a91-310">tooreboot, önbellek, bir veya daha fazla düğümlerinin istenen hello düğümleri tıklatıp **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="e8a91-310">tooreboot one or more nodes of your cache, select hello desired nodes and click **Reboot**.</span></span> <span data-ttu-id="e8a91-311">Kümeleme özelliği etkinleştirilmiş bir premium önbelleği varsa hello shard(s) tooreboot seçin ve ardından **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="e8a91-311">If you have a premium cache with clustering enabled, select hello shard(s) tooreboot and then click **Reboot**.</span></span> <span data-ttu-id="e8a91-312">Birkaç dakika sonra seçili düğümü yeniden başlatma hello ve birkaç dakika sonra yeniden çevrimiçi.</span><span class="sxs-lookup"><span data-stu-id="e8a91-312">After a few minutes, hello selected node(s) reboot, and are back online a few minutes later.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8a91-313">Yeniden başlatma için tüm fiyatlandırma katmanlarına kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="e8a91-313">Reboot is now available for all pricing tiers.</span></span> <span data-ttu-id="e8a91-314">Daha fazla bilgi ve yönergeler için bkz: [Azure Redis önbelleği yönetim - yeniden başlatma](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="e8a91-314">For more information and instructions, see [Azure Redis Cache administration - Reboot](cache-administration.md#reboot).</span></span>
> 
> 


## <a name="monitoring"></a><span data-ttu-id="e8a91-315">İzleme</span><span class="sxs-lookup"><span data-stu-id="e8a91-315">Monitoring</span></span>

<span data-ttu-id="e8a91-316">Merhaba **izleme** bölümü sağlar, size, tooconfigure tanılama ve Redis önbelleği için izleme.</span><span class="sxs-lookup"><span data-stu-id="e8a91-316">hello **Monitoring** section allows you tooconfigure diagnostics and monitoring for your Redis Cache.</span></span> <span data-ttu-id="e8a91-317">Azure Redis önbelleği izleme ve Tanılama hakkında daha fazla bilgi için bkz: [nasıl toomonitor Azure Redis önbelleği](cache-how-to-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="e8a91-317">For more information on Azure Redis Cache monitoring and diagnostics, see [How toomonitor Azure Redis Cache](cache-how-to-monitor.md).</span></span>

![Tanılama](./media/cache-configure/redis-cache-diagnostics.png)

* [<span data-ttu-id="e8a91-319">Ölçümleri redis</span><span class="sxs-lookup"><span data-stu-id="e8a91-319">Redis metrics</span></span>](#redis-metrics)
* [<span data-ttu-id="e8a91-320">Uyarı kuralları</span><span class="sxs-lookup"><span data-stu-id="e8a91-320">Alert rules</span></span>](#alert-rules)
* [<span data-ttu-id="e8a91-321">Tanılama</span><span class="sxs-lookup"><span data-stu-id="e8a91-321">Diagnostics</span></span>](#diagnostics)

### <a name="redis-metrics"></a><span data-ttu-id="e8a91-322">Ölçümleri redis</span><span class="sxs-lookup"><span data-stu-id="e8a91-322">Redis metrics</span></span>
<span data-ttu-id="e8a91-323">Tıklatın **Redis ölçümleri** çok[görüntülemek ölçümleri](cache-how-to-monitor.md#view-cache-metrics) önbelleğiniz için.</span><span class="sxs-lookup"><span data-stu-id="e8a91-323">Click **Redis metrics** too[view metrics](cache-how-to-monitor.md#view-cache-metrics) for your cache.</span></span>

### <a name="alert-rules"></a><span data-ttu-id="e8a91-324">Uyarı kuralları</span><span class="sxs-lookup"><span data-stu-id="e8a91-324">Alert rules</span></span>

<span data-ttu-id="e8a91-325">Tıklatın **uyarı kuralları** tooconfigure uyarıları temel Redis önbelleği ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="e8a91-325">Click **Alert rules** tooconfigure alerts based on Redis Cache metrics.</span></span> <span data-ttu-id="e8a91-326">Daha fazla bilgi için bkz: [uyarıları](cache-how-to-monitor.md#alerts).</span><span class="sxs-lookup"><span data-stu-id="e8a91-326">For more information, see [Alerts](cache-how-to-monitor.md#alerts).</span></span>

### <a name="diagnostics"></a><span data-ttu-id="e8a91-327">Tanılama</span><span class="sxs-lookup"><span data-stu-id="e8a91-327">Diagnostics</span></span>

<span data-ttu-id="e8a91-328">Önbellek ölçümleridir Azure İzleyicisi'nde varsayılan olarak, [30 gün boyunca depolanan](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) ve ardından silinir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-328">By default, cache metrics in Azure Monitor are [stored for 30 days](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) and then deleted.</span></span> <span data-ttu-id="e8a91-329">30 günden uzun, önbellek ölçümlerinizi toopersist tıklatın **tanılama** çok[hello depolama hesabı yapılandırma](cache-how-to-monitor.md#export-cache-metrics) toostore önbellek tanılamayı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e8a91-329">toopersist your cache metrics for longer than 30 days, click **Diagnostics** too[configure hello storage account](cache-how-to-monitor.md#export-cache-metrics) used toostore cache diagnostics.</span></span>

>[!NOTE]
><span data-ttu-id="e8a91-330">Toplama tooarchiving, önbellek ölçümleri toostorage kullanabileceğiniz [tooan olay hub'ı akış veya tooLog Analytics Gönder](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span><span class="sxs-lookup"><span data-stu-id="e8a91-330">In addition tooarchiving your cache metrics toostorage, you can also [stream them tooan Event hub or send them tooLog Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span></span>
>
>

## <a name="support--troubleshooting-settings"></a><span data-ttu-id="e8a91-331">Destek ve sorun giderme ayarları</span><span class="sxs-lookup"><span data-stu-id="e8a91-331">Support & troubleshooting settings</span></span>
<span data-ttu-id="e8a91-332">Merhaba hello ayarlarında **destek + sorun giderme** bölüm sağlar, önbellek ile ilgili sorunları çözmek için Seçenekler.</span><span class="sxs-lookup"><span data-stu-id="e8a91-332">hello settings in hello **Support + troubleshooting** section provide you with options for resolving issues with your cache.</span></span>

![Destek + sorunlarını giderme](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [<span data-ttu-id="e8a91-334">Kaynak durumu</span><span class="sxs-lookup"><span data-stu-id="e8a91-334">Resource health</span></span>](#resource-health)
* [<span data-ttu-id="e8a91-335">Yeni destek isteği</span><span class="sxs-lookup"><span data-stu-id="e8a91-335">New support request</span></span>](#new-support-request)

### <a name="resource-health"></a><span data-ttu-id="e8a91-336">Kaynak durumu</span><span class="sxs-lookup"><span data-stu-id="e8a91-336">Resource health</span></span>
<span data-ttu-id="e8a91-337">**Kaynak durumu** kaynağınız izler ve beklendiği gibi çalışıp çalışmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-337">**Resource health** watches your resource and tells you if it's running as expected.</span></span> <span data-ttu-id="e8a91-338">Hello Azure kaynak sistem durumu hizmeti hakkında daha fazla bilgi için bkz: [Azure kaynak sistem durumu genel bakış](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e8a91-338">For more information about hello Azure Resource health service, see [Azure Resource health overview](../resource-health/resource-health-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e8a91-339">Kaynak durumu hello durumu sanal ağında barındırılan Azure Redis önbelleği örnekleri üzerinde şu anda işleyemiyor tooreport ' dir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-339">Resource health is currently unable tooreport on hello health of Azure Redis Cache instances hosted in a virtual network.</span></span> <span data-ttu-id="e8a91-340">Daha fazla bilgi için bkz: [tüm önbellek özellikleri VNET önbelleğinde barındırdığında çalışır?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span><span class="sxs-lookup"><span data-stu-id="e8a91-340">For more information, see [Do all cache features work when hosting a cache in a VNET?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span></span>
> 
> 

### <a name="new-support-request"></a><span data-ttu-id="e8a91-341">Yeni destek isteği</span><span class="sxs-lookup"><span data-stu-id="e8a91-341">New support request</span></span>
<span data-ttu-id="e8a91-342">Tıklatın **yeni destek isteği** tooopen önbellek hesabınız için bir destek isteği.</span><span class="sxs-lookup"><span data-stu-id="e8a91-342">Click **New support request** tooopen a support request for your cache.</span></span>





## <a name="default-redis-server-configuration"></a><span data-ttu-id="e8a91-343">Varsayılan Redis sunucu yapılandırması</span><span class="sxs-lookup"><span data-stu-id="e8a91-343">Default Redis server configuration</span></span>
<span data-ttu-id="e8a91-344">Yeni Azure Redis önbelleği örnekleri varsayılan Redis yapılandırma değerlerini aşağıdaki hello ile yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="e8a91-344">New Azure Redis Cache instances are configured with hello following default Redis configuration values.</span></span>

> [!NOTE]
> <span data-ttu-id="e8a91-345">Bu bölümdeki Hello ayarları değiştirilemiyor hello kullanarak `StackExchange.Redis.IServer.ConfigSet` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e8a91-345">hello settings in this section cannot be changed using hello `StackExchange.Redis.IServer.ConfigSet` method.</span></span> <span data-ttu-id="e8a91-346">Bu yöntem, bu bölümdeki hello komutlar biriyle çağrılırsa, bir özel durum benzer toohello aşağıdaki oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="e8a91-346">If this method is called with one of hello commands in this section, an exception similar toohello following is thrown:</span></span>  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> <span data-ttu-id="e8a91-347">Yapılandırılabilir gibi herhangi bir değeri **en fazla bellek İlkesi**, hello Azure portalında veya Azure CLI veya PowerShell gibi komut satırı yönetim araçları aracılığıyla yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-347">Any values that are configurable, such as **max-memory-policy**, are configurable through hello Azure portal or command-line management tools such as Azure CLI or PowerShell.</span></span>
> 
> 

| <span data-ttu-id="e8a91-348">Ayar</span><span class="sxs-lookup"><span data-stu-id="e8a91-348">Setting</span></span> | <span data-ttu-id="e8a91-349">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="e8a91-349">Default value</span></span> | <span data-ttu-id="e8a91-350">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e8a91-350">Description</span></span> |
| --- | --- | --- |
| `databases` |<span data-ttu-id="e8a91-351">16</span><span class="sxs-lookup"><span data-stu-id="e8a91-351">16</span></span> |<span data-ttu-id="e8a91-352">Merhaba varsayılan veritabanı sayısı 16'dır, ancak fiyatlandırma katmanı bir farklı sayı göre hello yapılandırabilirsiniz. <sup>1</sup> hello varsayılan veritabanı DB 0, farklı bir bağlantı başına kullanma temel seçebileceğiniz `connection.GetDatabase(dbid)` nerede `dbid` arasında bir sayı `0` ve `databases - 1`.</span><span class="sxs-lookup"><span data-stu-id="e8a91-352">hello default number of databases is 16 but you can configure a different number based on hello pricing tier.<sup>1</sup> hello default database is DB 0, you can select a different one on a per-connection basis using `connection.GetDatabase(dbid)` where `dbid` is a number between `0` and `databases - 1`.</span></span> |
| `maxclients` |<span data-ttu-id="e8a91-353">Fiyatlandırma katmanı hello üzerinde bağlıdır<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="e8a91-353">Depends on hello pricing tier<sup>2</sup></span></span> |<span data-ttu-id="e8a91-354">En fazla bağlı istemciyi aynı hello izin hello budur zaman.</span><span class="sxs-lookup"><span data-stu-id="e8a91-354">This is hello maximum number of connected clients allowed at hello same time.</span></span> <span data-ttu-id="e8a91-355">Merhaba sınırına ulaşıldığında Redis tüm hello yeni bağlantıları, 'max sayısı sınırına istemcileri' hata dönülür.</span><span class="sxs-lookup"><span data-stu-id="e8a91-355">Once hello limit is reached Redis closes all hello new connections, returning a 'max number of clients reached' error.</span></span> |
| `maxmemory-policy` |`volatile-lru` |<span data-ttu-id="e8a91-356">Maxmemory İlkesi Redis hangi tooremove nasıl seçtiği için hello ayarı olduğu zaman `maxmemory` (Merhaba önbellek oluşturduğunuzda seçtiğiniz sunumu hello önbellek boyutunu hello) ulaşıldığında.</span><span class="sxs-lookup"><span data-stu-id="e8a91-356">Maxmemory policy is hello setting for how Redis selects what tooremove when `maxmemory` (hello size of hello cache offering you selected when you created hello cache) is reached.</span></span> <span data-ttu-id="e8a91-357">Azure Redis önbelleği hello varsayılan ayardır `volatile-lru`, LRU algoritması kullanılarak ayarlanan bir sona erme ile Merhaba anahtarlarını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="e8a91-357">With Azure Redis Cache hello default setting is `volatile-lru`, which removes hello keys with an expiration set using an LRU algorithm.</span></span> <span data-ttu-id="e8a91-358">Bu ayar hello Azure portal yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-358">This setting can be configured in hello Azure portal.</span></span> <span data-ttu-id="e8a91-359">Daha fazla bilgi için bkz: [bellek ilkeleri](#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="e8a91-359">For more information, see [Memory policies](#memory-policies).</span></span> |
| `maxmemory-samples` |<span data-ttu-id="e8a91-360">3</span><span class="sxs-lookup"><span data-stu-id="e8a91-360">3</span></span> |<span data-ttu-id="e8a91-361">toosave bellek, LRU ve TTL algoritmaları en az hassas algoritmaları yerine yaklaşık algoritmaları şunlardır.</span><span class="sxs-lookup"><span data-stu-id="e8a91-361">toosave memory, LRU and minimal TTL algorithms are approximated algorithms instead of precise algorithms.</span></span> <span data-ttu-id="e8a91-362">Varsayılan olarak, daha az kısa bir süre önce kullanılan denetimleri üç anahtarları ve çekmeleri hello bir Redis.</span><span class="sxs-lookup"><span data-stu-id="e8a91-362">By default Redis checks three keys and picks hello one that was used less recently.</span></span> |
| `lua-time-limit` |<span data-ttu-id="e8a91-363">5,000</span><span class="sxs-lookup"><span data-stu-id="e8a91-363">5,000</span></span> |<span data-ttu-id="e8a91-364">Milisaniye cinsinden Lua komut dosyası yürütme zaman sınırı.</span><span class="sxs-lookup"><span data-stu-id="e8a91-364">Max execution time of a Lua script in milliseconds.</span></span> <span data-ttu-id="e8a91-365">Merhaba maksimum yürütme süresi ulaştıysanız, Redis bir komut dosyası izin verilen süresi hala yürütme içinde hello maksimum sonra ve bir hata ile tooreply tooqueries başlatır günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="e8a91-365">If hello maximum execution time is reached, Redis logs that a script is still in execution after hello maximum allowed time, and starts tooreply tooqueries with an error.</span></span> |
| `lua-event-limit` |<span data-ttu-id="e8a91-366">500</span><span class="sxs-lookup"><span data-stu-id="e8a91-366">500</span></span> |<span data-ttu-id="e8a91-367">Komut dosyası olay sırasının en büyük boyutu.</span><span class="sxs-lookup"><span data-stu-id="e8a91-367">Max size of script event queue.</span></span> |
| <span data-ttu-id="e8a91-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span><span class="sxs-lookup"><span data-stu-id="e8a91-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span></span> |<span data-ttu-id="e8a91-369">0 0 032mb 8mb 60</span><span class="sxs-lookup"><span data-stu-id="e8a91-369">0 0 032mb 8mb 60</span></span> |<span data-ttu-id="e8a91-370">Merhaba istemci çıkış arabelleği sınırları olabilir veri hello sunucudan yeterince hızlı (ortak bir nedeni Pub/alt istemci iletileri hello yayımcı oluşturmak üzere kadar hızlı kullanamayacaklarını) herhangi bir nedenden dolayı okuyorsanız olmayan istemciler tooforce bağlantısının kesilmesi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e8a91-370">hello client output buffer limits can be used tooforce disconnection of clients that are not reading data from hello server fast enough for some reason (a common reason is that a Pub/Sub client can't consume messages as fast as hello publisher can produce them).</span></span> <span data-ttu-id="e8a91-371">Daha fazla bilgi için bkz: [http://redis.io/topics/clients](http://redis.io/topics/clients).</span><span class="sxs-lookup"><span data-stu-id="e8a91-371">For more information, see [http://redis.io/topics/clients](http://redis.io/topics/clients).</span></span> |

<span data-ttu-id="e8a91-372"><a name="databases"></a>
<sup>1</sup>hello sınırı `databases` her Azure Redis fiyatlandırma katmanı önbelleği için farklıdır ve önbellek oluşturma sırasında ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-372"><a name="databases"></a>
<sup>1</sup>hello limit for `databases` is different for each Azure Redis Cache pricing tier and can be set at cache creation.</span></span> <span data-ttu-id="e8a91-373">Öyle değilse `databases` ayarı belirtilen önbellek oluşturma sırasında hello varsayılandır 16.</span><span class="sxs-lookup"><span data-stu-id="e8a91-373">If no `databases` setting is specified during cache creation, hello default is 16.</span></span>

* <span data-ttu-id="e8a91-374">Temel ve standart önbellekler</span><span class="sxs-lookup"><span data-stu-id="e8a91-374">Basic and Standard caches</span></span>
  * <span data-ttu-id="e8a91-375">C0 - too16 veritabanlarını (250 MB) önbelleği</span><span class="sxs-lookup"><span data-stu-id="e8a91-375">C0 (250 MB) cache - up too16 databases</span></span>
  * <span data-ttu-id="e8a91-376">C1 - too16 veritabanlarını (1 GB) önbelleği</span><span class="sxs-lookup"><span data-stu-id="e8a91-376">C1 (1 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="e8a91-377">C2 - too16 veritabanlarını (2,5 GB) önbelleği</span><span class="sxs-lookup"><span data-stu-id="e8a91-377">C2 (2.5 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="e8a91-378">C3 (6 GB) önbelleği - too16 veritabanları</span><span class="sxs-lookup"><span data-stu-id="e8a91-378">C3 (6 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="e8a91-379">C4 (13 GB) önbelleği - too32 veritabanları</span><span class="sxs-lookup"><span data-stu-id="e8a91-379">C4 (13 GB) cache - up too32 databases</span></span>
  * <span data-ttu-id="e8a91-380">C5 (26 GB) önbelleği - too48 veritabanları</span><span class="sxs-lookup"><span data-stu-id="e8a91-380">C5 (26 GB) cache - up too48 databases</span></span>
  * <span data-ttu-id="e8a91-381">C6 (53 GB'a) önbelleği - too64 veritabanları</span><span class="sxs-lookup"><span data-stu-id="e8a91-381">C6 (53 GB) cache - up too64 databases</span></span>
* <span data-ttu-id="e8a91-382">Premium önbelleklere</span><span class="sxs-lookup"><span data-stu-id="e8a91-382">Premium caches</span></span>
  * <span data-ttu-id="e8a91-383">P1 (6 GB - 60 GB) - too16 veritabanlarını</span><span class="sxs-lookup"><span data-stu-id="e8a91-383">P1 (6 GB - 60 GB) - up too16 databases</span></span>
  * <span data-ttu-id="e8a91-384">P2 (13 GB - 130 GB) - too32 veritabanlarını</span><span class="sxs-lookup"><span data-stu-id="e8a91-384">P2 (13 GB - 130 GB) - up too32 databases</span></span>
  * <span data-ttu-id="e8a91-385">P3 (26 GB - 260 GB) - too48 veritabanlarını</span><span class="sxs-lookup"><span data-stu-id="e8a91-385">P3 (26 GB - 260 GB) - up too48 databases</span></span>
  * <span data-ttu-id="e8a91-386">P4 (53 GB'a - 530 GB) - too64 veritabanlarını</span><span class="sxs-lookup"><span data-stu-id="e8a91-386">P4 (53 GB - 530 GB) - up too64 databases</span></span>
  * <span data-ttu-id="e8a91-387">Etkin - Redis kümesi ile tüm premium önbelleklere Redis küme veritabanı 0 kullanımını şekilde hello destekler `databases` herhangi premium önbelleği etkin Redis kümesi ile etkili bir şekilde 1 ve hello için sınırlamak [seçin](http://redis.io/commands/select) komutu izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="e8a91-387">All premium caches with Redis cluster enabled - Redis cluster only supports use of database 0 so hello `databases` limit for any premium cache with Redis cluster enabled is effectively 1 and hello [Select](http://redis.io/commands/select) command is not allowed.</span></span> <span data-ttu-id="e8a91-388">Daha fazla bilgi için bkz: [toomake kümeleme tüm değişiklikleri toomy istemci uygulaması toouse ihtiyacım var?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span><span class="sxs-lookup"><span data-stu-id="e8a91-388">For more information, see [Do I need toomake any changes toomy client application toouse clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span></span>

<span data-ttu-id="e8a91-389">Veritabanları hakkında daha fazla bilgi için bkz: [Redis veritabanları nelerdir?](cache-faq.md#what-are-redis-databases)</span><span class="sxs-lookup"><span data-stu-id="e8a91-389">For more information about databases, see [What are Redis databases?](cache-faq.md#what-are-redis-databases)</span></span>

> [!NOTE]
> <span data-ttu-id="e8a91-390">Merhaba `databases` ayarını önbelleği oluşturma sırasında yalnızca yapılandırılmış ve yalnızca PowerShell, CLI veya diğer yönetim istemcileri kullanarak olabilir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-390">hello `databases` setting can be configured only during cache creation and only using PowerShell, CLI, or other management clients.</span></span> <span data-ttu-id="e8a91-391">Yapılandırma örneği için `databases` PowerShell kullanarak önbellek oluşturma sırasında bkz [yeni AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span><span class="sxs-lookup"><span data-stu-id="e8a91-391">For an example of configuring `databases` during cache creation using PowerShell, see [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span></span>
> 
> 

<span data-ttu-id="e8a91-392"><a name="maxclients"></a>
<sup>2</sup> `maxclients` her Azure Redis fiyatlandırma katmanı önbelleği için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="e8a91-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients` is different for each Azure Redis Cache pricing tier.</span></span>

* <span data-ttu-id="e8a91-393">Temel ve standart önbellekler</span><span class="sxs-lookup"><span data-stu-id="e8a91-393">Basic and Standard caches</span></span>
  * <span data-ttu-id="e8a91-394">C0 (250 MB) önbelleği - too256 bağlantıları</span><span class="sxs-lookup"><span data-stu-id="e8a91-394">C0 (250 MB) cache - up too256 connections</span></span>
  * <span data-ttu-id="e8a91-395">C1 (1 GB) önbelleği - too1, 000 bağlantıları</span><span class="sxs-lookup"><span data-stu-id="e8a91-395">C1 (1 GB) cache - up too1,000 connections</span></span>
  * <span data-ttu-id="e8a91-396">C2 (2,5 GB) önbelleği - too2, 000 bağlantıları</span><span class="sxs-lookup"><span data-stu-id="e8a91-396">C2 (2.5 GB) cache - up too2,000 connections</span></span>
  * <span data-ttu-id="e8a91-397">C3 (6 GB) önbelleği - too5, 000 bağlantıları</span><span class="sxs-lookup"><span data-stu-id="e8a91-397">C3 (6 GB) cache - up too5,000 connections</span></span>
  * <span data-ttu-id="e8a91-398">C4 (13 GB) önbelleği - too10, 000 bağlantıları</span><span class="sxs-lookup"><span data-stu-id="e8a91-398">C4 (13 GB) cache - up too10,000 connections</span></span>
  * <span data-ttu-id="e8a91-399">C5 (26 GB) önbelleği - too15, 000 bağlantıları</span><span class="sxs-lookup"><span data-stu-id="e8a91-399">C5 (26 GB) cache - up too15,000 connections</span></span>
  * <span data-ttu-id="e8a91-400">C6 (53 GB'a) önbelleği - too20, 000 bağlantıları</span><span class="sxs-lookup"><span data-stu-id="e8a91-400">C6 (53 GB) cache - up too20,000 connections</span></span>
* <span data-ttu-id="e8a91-401">Premium önbelleklere</span><span class="sxs-lookup"><span data-stu-id="e8a91-401">Premium caches</span></span>
  * <span data-ttu-id="e8a91-402">P1 (6 GB - 60 GB) - too7, 500 bağlantılar kurma</span><span class="sxs-lookup"><span data-stu-id="e8a91-402">P1 (6 GB - 60 GB) - up too7,500 connections</span></span>
  * <span data-ttu-id="e8a91-403">P2 (13 GB - 130 GB) - too15, 000 bağlantıları kurma</span><span class="sxs-lookup"><span data-stu-id="e8a91-403">P2 (13 GB - 130 GB) - up too15,000 connections</span></span>
  * <span data-ttu-id="e8a91-404">P3 (26 GB - 260 GB) - too30, 000 bağlantıları kurma</span><span class="sxs-lookup"><span data-stu-id="e8a91-404">P3 (26 GB - 260 GB) - up too30,000 connections</span></span>
  * <span data-ttu-id="e8a91-405">P4 (53 GB'a - 530 GB) - too40, 000 bağlantıları kurma</span><span class="sxs-lookup"><span data-stu-id="e8a91-405">P4 (53 GB - 530 GB) - up too40,000 connections</span></span>

> [!NOTE]
> <span data-ttu-id="e8a91-406">Her önbellek boyutunu sağlar, ancak *kadar* belirli bir sayıda bağlantıları, her bağlantı tooRedis ek yükü ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="e8a91-406">While each size of cache allows *up to* a certain number of connections, each connection tooRedis has overhead associated with it.</span></span> <span data-ttu-id="e8a91-407">TLS/SSL şifreleme sonucunda CPU ve bellek kullanımı gibi ek yükü örneği olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e8a91-407">An example of such overhead would be CPU and memory usage as a result of TLS/SSL encryption.</span></span> <span data-ttu-id="e8a91-408">Belirtilen önbellek boyutu Hello en fazla bağlantı sınırı hafifçe yüklü bir önbellek varsayar.</span><span class="sxs-lookup"><span data-stu-id="e8a91-408">hello maximum connection limit for a given cache size assumes a lightly loaded cache.</span></span> <span data-ttu-id="e8a91-409">Varsa yük bağlantı yükünü *artı* istemci işlemleri yükü hello sistem kapasitesini aşıyor, hello geçerli önbellek boyutu hello bağlantı sınırını aştınız değil olsa bile, hello önbellek kapasite sorunları deneyimi.</span><span class="sxs-lookup"><span data-stu-id="e8a91-409">If load from connection overhead *plus* load from client operations exceeds capacity for hello system, hello cache can experience capacity issues even if you have not exceeded hello connection limit for hello current cache size.</span></span>
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a><span data-ttu-id="e8a91-410">Azure Redis Önbelleği'nde desteklenmeyen komutlar redis</span><span class="sxs-lookup"><span data-stu-id="e8a91-410">Redis commands not supported in Azure Redis Cache</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e8a91-411">Microsoft tarafından yapılandırma ve Azure Redis önbelleği örnekleri yönetimini yönetilir çünkü hello aşağıdaki komutları devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="e8a91-411">Because configuration and management of Azure Redis Cache instances is managed by Microsoft, hello following commands are disabled.</span></span> <span data-ttu-id="e8a91-412">Tooinvoke denerseniz, bunları, çok benzer bir hata iletisi alıyorsunuz`"(error) ERR unknown command"`.</span><span class="sxs-lookup"><span data-stu-id="e8a91-412">If you try tooinvoke them, you receive an error message similar too`"(error) ERR unknown command"`.</span></span>
> 
> * <span data-ttu-id="e8a91-413">BGREWRITEAOF</span><span class="sxs-lookup"><span data-stu-id="e8a91-413">BGREWRITEAOF</span></span>
> * <span data-ttu-id="e8a91-414">BGSAVE</span><span class="sxs-lookup"><span data-stu-id="e8a91-414">BGSAVE</span></span>
> * <span data-ttu-id="e8a91-415">YAPILANDIRMA</span><span class="sxs-lookup"><span data-stu-id="e8a91-415">CONFIG</span></span>
> * <span data-ttu-id="e8a91-416">HATA AYIKLAMA</span><span class="sxs-lookup"><span data-stu-id="e8a91-416">DEBUG</span></span>
> * <span data-ttu-id="e8a91-417">GEÇİRME</span><span class="sxs-lookup"><span data-stu-id="e8a91-417">MIGRATE</span></span>
> * <span data-ttu-id="e8a91-418">KAYDET</span><span class="sxs-lookup"><span data-stu-id="e8a91-418">SAVE</span></span>
> * <span data-ttu-id="e8a91-419">KAPATMA</span><span class="sxs-lookup"><span data-stu-id="e8a91-419">SHUTDOWN</span></span>
> * <span data-ttu-id="e8a91-420">SLAVEOF</span><span class="sxs-lookup"><span data-stu-id="e8a91-420">SLAVEOF</span></span>
> * <span data-ttu-id="e8a91-421">Küme - komutları devre dışı bırakılır yazma ancak salt okunur Küme komutları izin verilir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-421">CLUSTER - Cluster write commands are disabled, but read-only Cluster commands are permitted.</span></span>
> 
> 

<span data-ttu-id="e8a91-422">Redis komutları hakkında daha fazla bilgi için bkz: [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="e8a91-422">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>

## <a name="redis-console"></a><span data-ttu-id="e8a91-423">Konsol redis</span><span class="sxs-lookup"><span data-stu-id="e8a91-423">Redis console</span></span>
<span data-ttu-id="e8a91-424">Komutları tooyour Azure Redis önbelleği örnekleri hello kullanarak güvenli bir şekilde verebilir **Redis konsol**, hello tüm ön bellek katmanlarını için Azure portalı içinde kullanılabilir olduğu.</span><span class="sxs-lookup"><span data-stu-id="e8a91-424">You can securely issue commands tooyour Azure Redis Cache instances using hello **Redis Console**, which is available in hello Azure portal for all cache tiers.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="e8a91-425">Merhaba Redis konsolu ile çalışmıyor [VNET](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="e8a91-425">hello Redis Console does not work with [VNET](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="e8a91-426">Önbelleğinizi VNET parçası olduğunda, yalnızca hello VNET istemcilerinde hello önbelleğe erişebilir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-426">When your cache is part of a VNET, only clients in hello VNET can access hello cache.</span></span> <span data-ttu-id="e8a91-427">Redis konsol VNET hello dışında olan yerel tarayıcınızda çalıştığından tooyour önbellek bağlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="e8a91-427">Because Redis Console runs in your local browser, which is outside hello VNET, it can't connect tooyour cache.</span></span>
> - <span data-ttu-id="e8a91-428">Azure Redis Önbelleği'nde desteklenen tüm Redis komutları.</span><span class="sxs-lookup"><span data-stu-id="e8a91-428">Not all Redis commands are supported in Azure Redis Cache.</span></span> <span data-ttu-id="e8a91-429">Önceki hello Azure Redis önbelleği için devre dışı Redis komutların listesi için bkz: [Redis Azure Redis Önbelleği'nde desteklenmeyen komutlar](#redis-commands-not-supported-in-azure-redis-cache) bölümü.</span><span class="sxs-lookup"><span data-stu-id="e8a91-429">For a list of Redis commands that are disabled for Azure Redis Cache, see hello previous [Redis commands not supported in Azure Redis Cache](#redis-commands-not-supported-in-azure-redis-cache) section.</span></span> <span data-ttu-id="e8a91-430">Redis komutları hakkında daha fazla bilgi için bkz: [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="e8a91-430">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>
> 
> 

<span data-ttu-id="e8a91-431">tooaccess hello Redis konsol tıklatın **konsol** hello gelen **Redis önbelleği** dikey.</span><span class="sxs-lookup"><span data-stu-id="e8a91-431">tooaccess hello Redis Console, click **Console** from hello **Redis Cache** blade.</span></span>

![Konsol redis](./media/cache-configure/redis-console-menu.png)

<span data-ttu-id="e8a91-433">Önbellek örneğinizin karşı tooissue komutları, yalnızca türü hello komutu hello konsoluna istenen.</span><span class="sxs-lookup"><span data-stu-id="e8a91-433">tooissue commands against your cache instance, simply type hello desired command into hello console.</span></span>

![Konsol redis](./media/cache-configure/redis-console.png)


### <a name="using-hello-redis-console-with-a-premium-clustered-cache"></a><span data-ttu-id="e8a91-435">Hello kullanarak bir premium konsoluyla Redis önbelleği kümelenmiş</span><span class="sxs-lookup"><span data-stu-id="e8a91-435">Using hello Redis Console with a premium clustered cache</span></span>

<span data-ttu-id="e8a91-436">Önbellek kümelenmiş bir premium ile Merhaba Redis konsolunu kullanarak, komutları tooa tek parça hello önbelleğin verebilir.</span><span class="sxs-lookup"><span data-stu-id="e8a91-436">When using hello Redis Console with a premium clustered cache, you can issue commands tooa single shard of hello cache.</span></span> <span data-ttu-id="e8a91-437">bir komut tooa belirli parça tooissue bağlanmanız toohello istenen parça hello parça seçici üzerinde tıklayarak.</span><span class="sxs-lookup"><span data-stu-id="e8a91-437">tooissue a command tooa specific shard, first connect toohello desired shard by clicking it on hello shard picker.</span></span>

![Konsol redis](./media/cache-configure/redis-console-premium-cluster.png)

<span data-ttu-id="e8a91-439">Tooaccess bağlı parça hello daha farklı bir parça içinde depolanan bir anahtarı çalışırsanız iletiden bir hata iletisi benzer bir toohello alıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="e8a91-439">If you attempt tooaccess a key that is stored in a different shard than hello connected shard, you receive an error message similar toohello following message.</span></span>

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

<span data-ttu-id="e8a91-440">Merhaba önceki örnekte hello Seçili parça parça 1 olan ancak `myKey` parça 0, hello tarafından belirtildiği şekilde bulunur `(shard 0)` hello hata iletisi kısmı.</span><span class="sxs-lookup"><span data-stu-id="e8a91-440">In hello previous example, shard 1 is hello selected shard, but `myKey` is located in shard 0, as indicated by hello `(shard 0)` portion of hello error message.</span></span> <span data-ttu-id="e8a91-441">Bu örnekte, tooaccess `myKey`seçin parça 0 kullanarak hello parça Seçici ve sorunu istenen hello komutu.</span><span class="sxs-lookup"><span data-stu-id="e8a91-441">In this example, tooaccess `myKey`, select shard 0 using hello shard picker, and then issue hello desired command.</span></span>


## <a name="move-your-cache-tooa-new-subscription"></a><span data-ttu-id="e8a91-442">Önbellek tooa yeni abonelik taşıma</span><span class="sxs-lookup"><span data-stu-id="e8a91-442">Move your cache tooa new subscription</span></span>
<span data-ttu-id="e8a91-443">Tıklayarak önbellek tooa yeni abonelik taşıyabilirsiniz **taşıma**.</span><span class="sxs-lookup"><span data-stu-id="e8a91-443">You can move your cache tooa new subscription by clicking **Move**.</span></span>

![Redis önbelleği taşıma](./media/cache-configure/redis-cache-move.png)

<span data-ttu-id="e8a91-445">Bir kaynak grubu tooanother ve bir abonelik tooanother kaynakları taşıma hakkında daha fazla bilgi için bkz: [kaynakları toonew kaynak grubuna veya aboneliğe taşıma](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="e8a91-445">For information on moving resources from one resource group tooanother, and from one subscription tooanother, see [Move resources toonew resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8a91-446">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e8a91-446">Next steps</span></span>
* <span data-ttu-id="e8a91-447">Redis komutları ile çalışma hakkında daha fazla bilgi için bkz: [nasıl ı çalıştırabilirsiniz Redis komutları?](cache-faq.md#how-can-i-run-redis-commands)</span><span class="sxs-lookup"><span data-stu-id="e8a91-447">For more information on working with Redis commands, see [How can I run Redis commands?](cache-faq.md#how-can-i-run-redis-commands)</span></span>

