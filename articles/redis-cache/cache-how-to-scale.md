---
title: "Azure Redis önbelleği aaaHow tooScale | Microsoft Docs"
description: "Nasıl tooscale Azure Redis öğrenin önbellek örneklerinde"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 350db214-3b7c-4877-bd43-fef6df2db96c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: sdanie
ms.openlocfilehash: 8d7c015a539f872913056392aa080bf3f445bd03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-azure-redis-cache"></a><span data-ttu-id="c2aac-103">Nasıl tooScale Azure Redis önbelleği</span><span class="sxs-lookup"><span data-stu-id="c2aac-103">How tooScale Azure Redis Cache</span></span>
<span data-ttu-id="c2aac-104">Azure Redis önbelleği, önbellek boyutunu ve özelliklerini hello seçimi esneklik sağlayan farklı önbellek teklifleri vardır.</span><span class="sxs-lookup"><span data-stu-id="c2aac-104">Azure Redis Cache has different cache offerings, which provide flexibility in hello choice of cache size and features.</span></span> <span data-ttu-id="c2aac-105">Bir önbellek oluşturulduktan sonra hello boyutu ve uygulamanızın hello gereksinimleri değiştirirseniz, fiyatlandırma katmanı hello önbelleğin hello ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2aac-105">After a cache is created, you can scale hello size and hello pricing tier of hello cache if hello requirements of your application change.</span></span> <span data-ttu-id="c2aac-106">Bu makalede, Azure PowerShell ve Azure CLI gibi tooscale önbelleğiniz hem hello Azure portal, hem de kullanarak nasıl araçları gösterir.</span><span class="sxs-lookup"><span data-stu-id="c2aac-106">This article shows you how tooscale your cache in both hello Azure portal and using tools such as Azure PowerShell and Azure CLI.</span></span>

## <a name="when-tooscale"></a><span data-ttu-id="c2aac-107">Zaman tooscale</span><span class="sxs-lookup"><span data-stu-id="c2aac-107">When tooscale</span></span>
<span data-ttu-id="c2aac-108">Merhaba kullanabilirsiniz [izleme](cache-how-to-monitor.md) Azure Redis önbelleği toomonitor özelliklerini hello sistem durumunu ve performansını önbelleğiniz ve ne zaman tooscale hello önbellek belirlemenize yardımcı olması.</span><span class="sxs-lookup"><span data-stu-id="c2aac-108">You can use hello [monitoring](cache-how-to-monitor.md) features of Azure Redis Cache toomonitor hello health and performance of your cache and help determine when tooscale hello cache.</span></span> 

<span data-ttu-id="c2aac-109">Merhaba aşağıdaki izleyebilirsiniz ölçümleri toohelp tooscale gerekip gerekmediğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="c2aac-109">You can monitor hello following metrics toohelp determine if you need tooscale.</span></span>

* <span data-ttu-id="c2aac-110">Redis sunucu iş yükü</span><span class="sxs-lookup"><span data-stu-id="c2aac-110">Redis Server Load</span></span>
* <span data-ttu-id="c2aac-111">Bellek kullanımı</span><span class="sxs-lookup"><span data-stu-id="c2aac-111">Memory Usage</span></span>
* <span data-ttu-id="c2aac-112">Ağ bant genişliği</span><span class="sxs-lookup"><span data-stu-id="c2aac-112">Network Bandwidth</span></span>
* <span data-ttu-id="c2aac-113">CPU kullanımı</span><span class="sxs-lookup"><span data-stu-id="c2aac-113">CPU Usage</span></span>

<span data-ttu-id="c2aac-114">Önbelleğinizi artık uygulamanızın gereksinimlerini karşılıyor mu karar verirseniz, fiyatlandırma katmanı, uygulamanız için doğru tooa daha büyük veya küçük önbellek ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2aac-114">If you determine that your cache is no longer meeting your application's requirements, you can scale tooa larger or smaller cache pricing tier that is right for your application.</span></span> <span data-ttu-id="c2aac-115">Hangi fiyatlandırma katmanı toouse önbelleğe belirleme hakkında daha fazla bilgi için bkz: [hangi Redis önbelleği teklifini ve boyutunu kullanmalıyım](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span><span class="sxs-lookup"><span data-stu-id="c2aac-115">For more information on determining which cache pricing tier toouse, see [What Redis Cache offering and size should I use](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span></span>

## <a name="scale-a-cache"></a><span data-ttu-id="c2aac-116">Ölçek bir önbellek</span><span class="sxs-lookup"><span data-stu-id="c2aac-116">Scale a cache</span></span>
<span data-ttu-id="c2aac-117">tooscale, önbellek [toohello önbelleği Gözat](cache-configure.md#configure-redis-cache-settings) hello içinde [Azure portal](https://portal.azure.com) tıklatıp **ölçek** hello gelen **kaynak menü**.</span><span class="sxs-lookup"><span data-stu-id="c2aac-117">tooscale your cache, [browse toohello cache](cache-configure.md#configure-redis-cache-settings) in hello [Azure portal](https://portal.azure.com) and click **Scale** from hello **Resource menu**.</span></span>

![Ölçek](./media/cache-how-to-scale/redis-cache-scale-menu.png)

<span data-ttu-id="c2aac-119">Select hello istenen fiyatlandırma Katmanı'ndan hello **fiyatlandırma katmanı seçme** tıklayın ve dikey **seçin**.</span><span class="sxs-lookup"><span data-stu-id="c2aac-119">Select hello desired pricing tier from hello **Select pricing tier** blade and click **Select**.</span></span>

![Fiyatlandırma katmanı][redis-cache-pricing-tier-blade]


<span data-ttu-id="c2aac-121">Tooa kısıtlamaları aşağıdaki hello ile fiyatlandırma katmanı farklı ölçeklendirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c2aac-121">You can scale tooa different pricing tier with hello following restrictions:</span></span>

* <span data-ttu-id="c2aac-122">Bir daha yüksek fiyatlandırma katmanı tooa fiyatlandırma katmanı alt ölçeklendirme olamaz.</span><span class="sxs-lookup"><span data-stu-id="c2aac-122">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
  * <span data-ttu-id="c2aac-123">Ölçeklendirme olamaz bir **Premium** tooa aşağı önbellek **standart** veya **temel** önbelleği.</span><span class="sxs-lookup"><span data-stu-id="c2aac-123">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="c2aac-124">Ölçeklendirme olamaz bir **standart** tooa aşağı önbellek **temel** önbelleği.</span><span class="sxs-lookup"><span data-stu-id="c2aac-124">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
* <span data-ttu-id="c2aac-125">Ölçeklendirme yapılabilir bir **temel** tooa önbelleğe **standart** önbellek ancak hello hello boyutta değiştiremiyor aynı anda.</span><span class="sxs-lookup"><span data-stu-id="c2aac-125">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="c2aac-126">Farklı bir boyut gerekiyorsa, bir sonraki ölçeklendirme işlemi istenen toohello boyutu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2aac-126">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
* <span data-ttu-id="c2aac-127">Ölçeklendirme olamaz bir **temel** doğrudan tooa önbelleğe **Premium** önbelleği.</span><span class="sxs-lookup"><span data-stu-id="c2aac-127">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="c2aac-128">Ölçeklendirme gerekir **temel** çok**standart** bir ölçeklendirme işlemi ve ardından gelen **standart** çok**Premium** , sonraki ölçeklendirme işlem.</span><span class="sxs-lookup"><span data-stu-id="c2aac-128">You must scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="c2aac-129">Büyük bir değerden toohello aşağı ölçeklendirme olamaz **C0 (250 MB)** boyutu.</span><span class="sxs-lookup"><span data-stu-id="c2aac-129">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>
 
<span data-ttu-id="c2aac-130">Merhaba önbellek toohello yeni fiyatlandırma katmanı, ölçekleme sırasında bir **ölçeklendirme** durum hello görüntülenen **Redis önbelleği** dikey.</span><span class="sxs-lookup"><span data-stu-id="c2aac-130">While hello cache is scaling toohello new pricing tier, a **Scaling** status is displayed in hello **Redis Cache** blade.</span></span>

![Ölçeklendirme][redis-cache-scaling]

<span data-ttu-id="c2aac-132">Ölçeklendirme tamamlandığında hello durum değişiklikleri **ölçeklendirme** çok**çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="c2aac-132">When scaling is complete, hello status changes from **Scaling** too**Running**.</span></span>

## <a name="how-tooautomate-a-scaling-operation"></a><span data-ttu-id="c2aac-133">Nasıl tooautomate bir ölçeklendirme işlemi</span><span class="sxs-lookup"><span data-stu-id="c2aac-133">How tooautomate a scaling operation</span></span>
<span data-ttu-id="c2aac-134">Toplama tooscaling önbellek örneklerinizi Azure portal Merhaba, PowerShell cmdlet'leri, Azure CLI kullanarak ölçeklendirme ve Microsoft Azure yönetim kitaplıkları (MAML) hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c2aac-134">In addition tooscaling your cache instances in hello Azure portal, you can scale using PowerShell cmdlets, Azure CLI, and by using hello Microsoft Azure Management Libraries (MAML).</span></span> 

* [<span data-ttu-id="c2aac-135">PowerShell kullanarak ölçek</span><span class="sxs-lookup"><span data-stu-id="c2aac-135">Scale using PowerShell</span></span>](#scale-using-powershell)
* [<span data-ttu-id="c2aac-136">Azure CLI kullanarak ölçek</span><span class="sxs-lookup"><span data-stu-id="c2aac-136">Scale using Azure CLI</span></span>](#scale-using-azure-cli)
* [<span data-ttu-id="c2aac-137">Ölçek MAML kullanma</span><span class="sxs-lookup"><span data-stu-id="c2aac-137">Scale using MAML</span></span>](#scale-using-maml)

### <a name="scale-using-powershell"></a><span data-ttu-id="c2aac-138">PowerShell kullanarak ölçek</span><span class="sxs-lookup"><span data-stu-id="c2aac-138">Scale using PowerShell</span></span>
<span data-ttu-id="c2aac-139">Hello kullanarak PowerShell ile Azure Redis önbelleği örneklerinizi ölçeklendirebilirsiniz [kümesi AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet hello zaman `Size`, `Sku`, veya `ShardCount` özellikleri değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="c2aac-139">You can scale your Azure Redis Cache instances with PowerShell by using hello [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet when hello `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> <span data-ttu-id="c2aac-140">Merhaba aşağıdaki örnekte nasıl tooscale bir önbellek adlı gösterir `myCache` tooa 2,5 GB önbellek.</span><span class="sxs-lookup"><span data-stu-id="c2aac-140">hello following example shows how tooscale a cache named `myCache` tooa 2.5 GB cache.</span></span> 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="c2aac-141">PowerShell ile ölçeklendirme ile ilgili daha fazla bilgi için bkz: [tooscale bir Redis önbelleğe Powershell kullanarak](cache-howto-manage-redis-cache-powershell.md#scale).</span><span class="sxs-lookup"><span data-stu-id="c2aac-141">For more information on scaling with PowerShell, see [tooscale a Redis cache using Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span></span>

### <a name="scale-using-azure-cli"></a><span data-ttu-id="c2aac-142">Azure CLI kullanarak ölçek</span><span class="sxs-lookup"><span data-stu-id="c2aac-142">Scale using Azure CLI</span></span>
<span data-ttu-id="c2aac-143">Azure CLI kullanarak Azure Redis önbelleği örneklerinizi tooscale çağrısı hello `azure rediscache set` komut ve yeni boyutu, sku veya hello bağlı olarak küme boyutu dahil istenen hello yapılandırma değişikliklerini geçişinde istenen ölçekleme işlemi.</span><span class="sxs-lookup"><span data-stu-id="c2aac-143">tooscale your Azure Redis Cache instances using Azure CLI, call hello `azure rediscache set` command and pass in hello desired configuration changes that include a new size, sku, or cluster size, depending on hello desired scaling operation.</span></span>

<span data-ttu-id="c2aac-144">Azure CLI ile ölçeklendirme ile ilgili daha fazla bilgi için bkz: [var olan bir Redis Önbelleği Ayarları Değiştir](cache-manage-cli.md#scale).</span><span class="sxs-lookup"><span data-stu-id="c2aac-144">For more information on scaling with Azure CLI, see [Change settings of an existing Redis Cache](cache-manage-cli.md#scale).</span></span>

### <a name="scale-using-maml"></a><span data-ttu-id="c2aac-145">Ölçek MAML kullanma</span><span class="sxs-lookup"><span data-stu-id="c2aac-145">Scale using MAML</span></span>
<span data-ttu-id="c2aac-146">tooscale hello kullanarak, Azure Redis önbelleği örnekleri [Microsoft Azure yönetim kitaplıkları (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), çağrı hello `IRedisOperations.CreateOrUpdate` yöntemi ve yeni boyutu hello hello geçişinde `RedisProperties.SKU.Capacity`.</span><span class="sxs-lookup"><span data-stu-id="c2aac-146">tooscale your Azure Redis Cache instances using hello [Microsoft Azure Management Libraries (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), call hello `IRedisOperations.CreateOrUpdate` method and pass in hello new size for hello `RedisProperties.SKU.Capacity`.</span></span>

    static void Main(string[] args)
    {
        // For instructions on getting hello access token, see
        // https://azure.microsoft.com/documentation/articles/cache-configure/#access-keys
        string token = GetAuthorizationHeader();

        TokenCloudCredentials creds = new TokenCloudCredentials(subscriptionId,token);

        RedisManagementClient client = new RedisManagementClient(creds);
        var redisProperties = new RedisProperties();

        // tooscale, set a new size for hello redisSKUCapacity parameter.
        redisProperties.Sku = new Sku(redisSKUName,redisSKUFamily,redisSKUCapacity);
        redisProperties.RedisVersion = redisVersion;
        var redisParams = new RedisCreateOrUpdateParameters(redisProperties, redisCacheRegion);
        client.Redis.CreateOrUpdate(resourceGroupName,cacheName, redisParams);
    }

<span data-ttu-id="c2aac-147">Daha fazla bilgi için bkz: Merhaba [yönetmek MAML kullanarak Redis önbelleği](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) örnek.</span><span class="sxs-lookup"><span data-stu-id="c2aac-147">For more information, see hello [Manage Redis Cache using MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample.</span></span>

## <a name="scaling-faq"></a><span data-ttu-id="c2aac-148">Ölçeklendirme ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="c2aac-148">Scaling FAQ</span></span>
<span data-ttu-id="c2aac-149">Merhaba aşağıdaki listede Azure Redis önbelleği ölçeklendirme hakkında sorular yanıtlar toocommonly içerir.</span><span class="sxs-lookup"><span data-stu-id="c2aac-149">hello following list contains answers toocommonly asked questions about Azure Redis Cache scaling.</span></span>

* [<span data-ttu-id="c2aac-150">İçin ya da Premium önbelleği içinde ölçekleme?</span><span class="sxs-lookup"><span data-stu-id="c2aac-150">Can I scale to, from, or within a Premium cache?</span></span>](#can-i-scale-to-from-or-within-a-premium-cache)
* [<span data-ttu-id="c2aac-151">Ölçeklendirme sonra ı toochange my önbellek adını veya erişim anahtarları var mı?</span><span class="sxs-lookup"><span data-stu-id="c2aac-151">After scaling, do I have toochange my cache name or access keys?</span></span>](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [<span data-ttu-id="c2aac-152">Ölçeklendirme nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="c2aac-152">How does scaling work?</span></span>](#how-does-scaling-work)
* [<span data-ttu-id="c2aac-153">Ölçeklendirme sırasında ı my önbellekten veri kaybedersiniz?</span><span class="sxs-lookup"><span data-stu-id="c2aac-153">Will I lose data from my cache during scaling?</span></span>](#will-i-lose-data-from-my-cache-during-scaling)
* [<span data-ttu-id="c2aac-154">My özel veritabanlarını ölçeklendirme sırasında etkilenen ayarlıyor?</span><span class="sxs-lookup"><span data-stu-id="c2aac-154">Is my custom databases setting affected during scaling?</span></span>](#is-my-custom-databases-setting-affected-during-scaling)
* [<span data-ttu-id="c2aac-155">My önbellek ölçeklendirme sırasında kullanılabilir olacak?</span><span class="sxs-lookup"><span data-stu-id="c2aac-155">Will my cache be available during scaling?</span></span>](#will-my-cache-be-available-during-scaling)
* [<span data-ttu-id="c2aac-156">Desteklenmeyen işlemleri</span><span class="sxs-lookup"><span data-stu-id="c2aac-156">Operations that are not supported</span></span>](#operations-that-are-not-supported)
* [<span data-ttu-id="c2aac-157">Ne kadar ölçeklendirme sürer?</span><span class="sxs-lookup"><span data-stu-id="c2aac-157">How long does scaling take?</span></span>](#how-long-does-scaling-take)
* [<span data-ttu-id="c2aac-158">Ölçeklendirme tamamlandığında nasıl anlayabilirim?</span><span class="sxs-lookup"><span data-stu-id="c2aac-158">How can I tell when scaling is complete?</span></span>](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a><span data-ttu-id="c2aac-159">İçin ya da Premium önbelleği içinde ölçekleme?</span><span class="sxs-lookup"><span data-stu-id="c2aac-159">Can I scale to, from, or within a Premium cache?</span></span>
* <span data-ttu-id="c2aac-160">Ölçeklendirme olamaz bir **Premium** tooa aşağı önbellek **temel** veya **standart** fiyatlandırma katmanı.</span><span class="sxs-lookup"><span data-stu-id="c2aac-160">You can't scale from a **Premium** cache down tooa **Basic** or **Standard** pricing tier.</span></span>
* <span data-ttu-id="c2aac-161">Birinden ölçeklendirebilirsiniz **Premium** önbellek fiyatlandırma katmanı tooanother.</span><span class="sxs-lookup"><span data-stu-id="c2aac-161">You can scale from one **Premium** cache pricing tier tooanother.</span></span>
* <span data-ttu-id="c2aac-162">Ölçeklendirme olamaz bir **temel** doğrudan tooa önbelleğe **Premium** önbelleği.</span><span class="sxs-lookup"><span data-stu-id="c2aac-162">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="c2aac-163">Öğesinden önce Ölçeklendirmesi gerekir **temel** çok**standart** bir ölçeklendirme işlemi ve ardından gelen **standart** çok**Premium** sonraki ölçeklendirme işlemi.</span><span class="sxs-lookup"><span data-stu-id="c2aac-163">You must first scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="c2aac-164">Kümeleme etkinleştirilirse oluşturduğunuzda, **Premium** önbellek, şunları yapabilirsiniz [hello küme boyutunu değiştirme](cache-how-to-premium-clustering.md#cluster-size).</span><span class="sxs-lookup"><span data-stu-id="c2aac-164">If you enabled clustering when you created your **Premium** cache, you can [change hello cluster size](cache-how-to-premium-clustering.md#cluster-size).</span></span> <span data-ttu-id="c2aac-165">Önbelleğinizi etkin Kümeleme olmadan oluşturulduysa, daha sonraki bir zamanda kümeleme yapılandıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="c2aac-165">If your cache was created without clustering enabled, you can't configure clustering at a later time.</span></span>
  
  <span data-ttu-id="c2aac-166">Daha fazla bilgi için bkz: [nasıl bir Premium Azure Redis önbelleği için kümeleri tooconfigure](cache-how-to-premium-clustering.md).</span><span class="sxs-lookup"><span data-stu-id="c2aac-166">For more information, see [How tooconfigure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>

### <a name="after-scaling-do-i-have-toochange-my-cache-name-or-access-keys"></a><span data-ttu-id="c2aac-167">Ölçeklendirme sonra ı toochange my önbellek adını veya erişim anahtarları var mı?</span><span class="sxs-lookup"><span data-stu-id="c2aac-167">After scaling, do I have toochange my cache name or access keys?</span></span>
<span data-ttu-id="c2aac-168">Hayır, önbellek adı ve anahtarları bir ölçeklendirme işlemi sırasında değiştirilmez.</span><span class="sxs-lookup"><span data-stu-id="c2aac-168">No, your cache name and keys are unchanged during a scaling operation.</span></span>

### <a name="how-does-scaling-work"></a><span data-ttu-id="c2aac-169">Ölçeklendirme nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="c2aac-169">How does scaling work?</span></span>
* <span data-ttu-id="c2aac-170">Zaman bir **temel** önbellek ölçeklendirilmiş tooa farklı boyutu, onu kapatılır ve yeni bir önbellek hello yeni boyut kullanılarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="c2aac-170">When a **Basic** cache is scaled tooa different size, it is shut down and a new cache is provisioned using hello new size.</span></span> <span data-ttu-id="c2aac-171">Bu süre boyunca hello önbellek kullanılamıyor ve hello önbelleğindeki verilerin tümü kaybolur.</span><span class="sxs-lookup"><span data-stu-id="c2aac-171">During this time, hello cache is unavailable and all data in hello cache is lost.</span></span>
* <span data-ttu-id="c2aac-172">Zaman bir **temel** önbelleğidir ölçeklendirilmiş tooa **standart** önbellek, çoğaltma önbelleği hazırlanmıştır ve hello veri hello birincil önbellek toohello çoğaltma önbellekten kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="c2aac-172">When a **Basic** cache is scaled tooa **Standard** cache, a replica cache is provisioned and hello data is copied from hello primary cache toohello replica cache.</span></span> <span data-ttu-id="c2aac-173">Merhaba önbellek işlem ölçeklendirme hello sırasında kullanılabilir olarak kalır.</span><span class="sxs-lookup"><span data-stu-id="c2aac-173">hello cache remains available during hello scaling process.</span></span>
* <span data-ttu-id="c2aac-174">Zaman bir **standart** önbelleğidir ölçeklendirilmiş tooa farklı boyutu veya tooa **Premium** önbellek, biri hello çoğaltmaları kapatılması ve yeniden sağlanan üzerinden aktarılan toohello yeni boyutunu ve hello verileri ve hello diğer Çoğaltma, yeniden sağlanmadan önce yük devretme, başarısızlığın hello önbellek düğümlerinden biri sırasında oluşan benzer toohello işlem gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="c2aac-174">When a **Standard** cache is scaled tooa different size or tooa **Premium** cache, one of hello replicas is shut down and re-provisioned toohello new size and hello data transferred over, and then hello other replica performs a failover before it is re-provisioned, similar toohello process that occurs during a failure of one of hello cache nodes.</span></span>

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a><span data-ttu-id="c2aac-175">Ölçeklendirme sırasında ı my önbellekten veri kaybedersiniz?</span><span class="sxs-lookup"><span data-stu-id="c2aac-175">Will I lose data from my cache during scaling?</span></span>
* <span data-ttu-id="c2aac-176">Zaman bir **temel** ölçeklendirilmiş tooa yeni boyutu, tüm veriler kaybolur ve hello önbellek işlemi ölçeklendirme hello sırasında kullanılamıyorsa önbelleği.</span><span class="sxs-lookup"><span data-stu-id="c2aac-176">When a **Basic** cache is scaled tooa new size, all data is lost and hello cache is unavailable during hello scaling operation.</span></span>
* <span data-ttu-id="c2aac-177">Zaman bir **temel** önbelleğidir ölçeklendirilmiş tooa **standart** önbelleğe, hello hello önbellekteki veri genellikle korunur.</span><span class="sxs-lookup"><span data-stu-id="c2aac-177">When a **Basic** cache is scaled tooa **Standard** cache, hello data in hello cache is typically preserved.</span></span>
* <span data-ttu-id="c2aac-178">Zaman bir **standart** önbelleğidir ölçeklendirilmiş tooa büyük ya da katmanı, veya bir **Premium** önbellek ölçeklendirilmiş tooa büyük boyut, tüm verileri genellikle korunur.</span><span class="sxs-lookup"><span data-stu-id="c2aac-178">When a **Standard** cache is scaled tooa larger size or tier, or a **Premium** cache is scaled tooa larger size, all data is typically preserved.</span></span> <span data-ttu-id="c2aac-179">Ölçekleme sırasında bir **standart** veya **Premium** tooa daha küçük boyutu, veri aşağı önbellek kaybolabilir ne kadar veri hello önbelleğinde olan bağlı olarak ilgili toohello yeni boyutu, ölçeklendirilir olduğunda.</span><span class="sxs-lookup"><span data-stu-id="c2aac-179">When scaling a **Standard** or **Premium** cache down tooa smaller size, data may be lost depending on how much data is in hello cache related toohello new size when it is scaled.</span></span> <span data-ttu-id="c2aac-180">Veri ölçeklendirdiğinizde kaybolursa, anahtarları hello kullanarak çıkarılacak [allkeys lru](http://redis.io/topics/lru-cache) çıkarma ilkesi.</span><span class="sxs-lookup"><span data-stu-id="c2aac-180">If data is lost when scaling down, keys are evicted using hello [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span></span> 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a><span data-ttu-id="c2aac-181">My özel veritabanlarını ölçeklendirme sırasında etkilenen ayarlıyor?</span><span class="sxs-lookup"><span data-stu-id="c2aac-181">Is my custom databases setting affected during scaling?</span></span>
<span data-ttu-id="c2aac-182">Bazı fiyatlandırma katmanları farklı sahip [veritabanları sınırları](cache-configure.md#databases), böylece bazı noktalar IF ölçekleme hello için özel bir değer yapılandırıldığında `databases` önbellek oluşturma sırasında ayarlama.</span><span class="sxs-lookup"><span data-stu-id="c2aac-182">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when scaling down if you configured a custom value for hello `databases` setting during cache creation.</span></span>

* <span data-ttu-id="c2aac-183">Fiyatlandırma katmanı ile bir alt tooa'ne zaman ölçeklendirme `databases` hello geçerli katmanı sınırından:</span><span class="sxs-lookup"><span data-stu-id="c2aac-183">When scaling tooa pricing tier with a lower `databases` limit than hello current tier:</span></span>
  * <span data-ttu-id="c2aac-184">Merhaba varsayılan sayısı kullanıyorsanız `databases` tüm fiyatlandırma katmanlarına 16 olduğu, veri kaybı olmamasına.</span><span class="sxs-lookup"><span data-stu-id="c2aac-184">If you are using hello default number of `databases` which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="c2aac-185">Özel bir dizi kullanıyorsanız `databases` ölçeklendirme, hello katmanı toowhich için hello sınırları içinde kalan bu `databases` ayarı tutulur ve veri kaybı olmamasına.</span><span class="sxs-lookup"><span data-stu-id="c2aac-185">If you are using a custom number of `databases` that falls within hello limits for hello tier toowhich you are scaling, this `databases` setting is retained and no data is lost.</span></span>
  * <span data-ttu-id="c2aac-186">Özel bir dizi kullanıyorsanız `databases` , hello sınırlarını hello yeni katmanının hello aşıyor `databases` ayarı hello yeni katmanı alçaltılmış toohello sınırları ve kaldırılmış hello veritabanlarındaki verilerin tümü kaybolur.</span><span class="sxs-lookup"><span data-stu-id="c2aac-186">If you are using a custom number of `databases` that exceeds hello limits of hello new tier, hello `databases` setting is lowered toohello limits of hello new tier and all data in hello removed databases is lost.</span></span>
* <span data-ttu-id="c2aac-187">Aynı veya daha yüksek fiyatlandırma katmanı hello ile tooa'ne zaman ölçeklendirme `databases` hello geçerli katmanı sınırından, `databases` ayarı tutulur ve veri kaybı olmamasına.</span><span class="sxs-lookup"><span data-stu-id="c2aac-187">When scaling tooa pricing tier with hello same or higher `databases` limit than hello current tier your `databases` setting is retained and no data is lost.</span></span>

<span data-ttu-id="c2aac-188">% 99,9 SLA kullanılabilirlik için standart ve Premium önbellekleri sahip olsa da, veri kaybı için hiçbir SLA yoktur.</span><span class="sxs-lookup"><span data-stu-id="c2aac-188">Note that while Standard and Premium caches have a 99.9% SLA for availability, there is no SLA for data loss.</span></span>

### <a name="will-my-cache-be-available-during-scaling"></a><span data-ttu-id="c2aac-189">My önbellek ölçeklendirme sırasında kullanılabilir olacak?</span><span class="sxs-lookup"><span data-stu-id="c2aac-189">Will my cache be available during scaling?</span></span>
* <span data-ttu-id="c2aac-190">**Standart** ve **Premium** önbellekleri kullanılabilir olmaya devam eder işlemi ölçeklendirme hello sırasında.</span><span class="sxs-lookup"><span data-stu-id="c2aac-190">**Standard** and **Premium** caches remain available during hello scaling operation.</span></span>
* <span data-ttu-id="c2aac-191">**Temel** önbellekleri işlemleri tooa farklı boyutu ölçeklendirme sırasında çevrimdışı, ancak gelen ölçekleme sırasında kullanılabilir olmaya devam etmesi **temel** çok**standart**.</span><span class="sxs-lookup"><span data-stu-id="c2aac-191">**Basic** caches are offline during scaling operations tooa different size, but remain available when scaling from **Basic** too**Standard**.</span></span>

### <a name="operations-that-are-not-supported"></a><span data-ttu-id="c2aac-192">Desteklenmeyen işlemleri</span><span class="sxs-lookup"><span data-stu-id="c2aac-192">Operations that are not supported</span></span>
* <span data-ttu-id="c2aac-193">Bir daha yüksek fiyatlandırma katmanı tooa fiyatlandırma katmanı alt ölçeklendirme olamaz.</span><span class="sxs-lookup"><span data-stu-id="c2aac-193">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
  * <span data-ttu-id="c2aac-194">Ölçeklendirme olamaz bir **Premium** tooa aşağı önbellek **standart** veya **temel** önbelleği.</span><span class="sxs-lookup"><span data-stu-id="c2aac-194">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="c2aac-195">Ölçeklendirme olamaz bir **standart** tooa aşağı önbellek **temel** önbelleği.</span><span class="sxs-lookup"><span data-stu-id="c2aac-195">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
* <span data-ttu-id="c2aac-196">Ölçeklendirme yapılabilir bir **temel** tooa önbelleğe **standart** önbellek ancak hello hello boyutta değiştiremiyor aynı anda.</span><span class="sxs-lookup"><span data-stu-id="c2aac-196">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="c2aac-197">Farklı bir boyut gerekiyorsa, bir sonraki ölçeklendirme işlemi istenen toohello boyutu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2aac-197">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
* <span data-ttu-id="c2aac-198">Ölçeklendirme olamaz bir **temel** doğrudan tooa önbelleğe **Premium** önbelleği.</span><span class="sxs-lookup"><span data-stu-id="c2aac-198">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="c2aac-199">Öğesinden önce Ölçeklendirmesi gerekir **temel** çok**standart** bir ölçeklendirme işlemi ve ardından gelen **standart** çok**Premium** sonraki ölçeklendirme işlemi.</span><span class="sxs-lookup"><span data-stu-id="c2aac-199">You must first scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="c2aac-200">Büyük bir değerden toohello aşağı ölçeklendirme olamaz **C0 (250 MB)** boyutu.</span><span class="sxs-lookup"><span data-stu-id="c2aac-200">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>

<span data-ttu-id="c2aac-201">Bir ölçeklendirme işlemi başarısız olursa, hello hizmet toorevert hello işlemi deneyecek ve hello önbellek toohello özgün boyutunu döner.</span><span class="sxs-lookup"><span data-stu-id="c2aac-201">If a scaling operation fails, hello service will try toorevert hello operation and hello cache will revert toohello original size.</span></span>

### <a name="how-long-does-scaling-take"></a><span data-ttu-id="c2aac-202">Ne kadar ölçeklendirme sürer?</span><span class="sxs-lookup"><span data-stu-id="c2aac-202">How long does scaling take?</span></span>
<span data-ttu-id="c2aac-203">Yaklaşık 20 hello önbellekte ne kadar veri bağlı olarak dakika sürer ölçeklendirme.</span><span class="sxs-lookup"><span data-stu-id="c2aac-203">Scaling takes approximately 20 minutes, depending on how much data is in hello cache.</span></span>

### <a name="how-can-i-tell-when-scaling-is-complete"></a><span data-ttu-id="c2aac-204">Ölçeklendirme tamamlandığında nasıl anlayabilirim?</span><span class="sxs-lookup"><span data-stu-id="c2aac-204">How can I tell when scaling is complete?</span></span>
<span data-ttu-id="c2aac-205">Hello Azure portal, devam eden işlemi ölçeklendirme hello görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2aac-205">In hello Azure portal you can see hello scaling operation in progress.</span></span> <span data-ttu-id="c2aac-206">Ölçeklendirme tamamlandığında hello önbelleği değişiklikleri durumunu çok hello**çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="c2aac-206">When scaling is complete, hello status of hello cache changes too**Running**.</span></span>

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



