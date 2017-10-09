---
title: "aaaCreate hello portalında bir Azure Search Hizmeti | Microsoft Docs"
description: "Azure Search Hizmeti hello portalında sağlayın."
services: search
manager: jhubbard
author: HeidiSteen
documentationcenter: 
ms.assetid: c8c88922-69aa-4099-b817-60f7b54e62df
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: f1c7197a1467e32bd4b360b165c9059e6bb0e496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-service-in-hello-portal"></a><span data-ttu-id="1ceaa-103">Merhaba portalda Azure Search hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ceaa-103">Create an Azure Search service in hello portal</span></span>

<span data-ttu-id="1ceaa-104">Bu makalede nasıl toocreate veya sağlama Azure Search Hizmeti hello Portalı'nda açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-104">This article explains how toocreate or provision an Azure Search service in hello portal.</span></span> <span data-ttu-id="1ceaa-105">PowerShell yönergeleri için bkz: [PowerShell ile yönetme Azure Search](search-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1ceaa-105">For PowerShell instructions, see [Manage Azure Search with PowerShell](search-manage-powershell.md).</span></span>

## <a name="subscribe-free-or-paid"></a><span data-ttu-id="1ceaa-106">(Ücretsiz veya Ücretli) abone olma</span><span class="sxs-lookup"><span data-stu-id="1ceaa-106">Subscribe (free or paid)</span></span>

<span data-ttu-id="1ceaa-107">[Ücretsiz bir Azure hesabı açın](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ve Azure Hizmetleri Ücretli ücretsiz krediler tootry çıkışı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-107">[Open a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) and use free credits tootry out paid Azure services.</span></span> <span data-ttu-id="1ceaa-108">Krediler bitmiş olsa, hello hesabı sürdürebilir ve Web siteleri gibi toouse ücretsiz Azure hizmetlerinden devam edin.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-108">After credits are used up, keep hello account and continue toouse free Azure services, such as Websites.</span></span> <span data-ttu-id="1ceaa-109">Açıkça ayarlarınızı değiştirip ücret toobe isteyin sürece kredi kartınızdan asla ücret kesilir.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-109">Your credit card is never charged unless you explicitly change your settings and ask toobe charged.</span></span>

<span data-ttu-id="1ceaa-110">Alternatif olarak, [MSDN abone Avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="1ceaa-110">Alternatively, [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span> <span data-ttu-id="1ceaa-111">Bir MSDN aboneliğiniz, ücretli Azure hizmetlerinizi kullanabildiğiniz her ay krediler sağlar.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-111">An MSDN subscription gives you credits every month you can use for paid Azure services.</span></span> 

## <a name="find-azure-search"></a><span data-ttu-id="1ceaa-112">Azure Arama Bul</span><span class="sxs-lookup"><span data-stu-id="1ceaa-112">Find Azure Search</span></span>
1. <span data-ttu-id="1ceaa-113">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1ceaa-113">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1ceaa-114">Merhaba artı işareti ("+") içinde hello üst köşe sol tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-114">Click hello plus sign ("+") in hello top left corner.</span></span>
3. <span data-ttu-id="1ceaa-115">Seçin **Web + mobil** > **Azure arama**.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-115">Select **Web + Mobile** > **Azure Search**.</span></span>

![](./media/search-create-service-portal/find-search2.png)

## <a name="name-hello-service-and-url-endpoint"></a><span data-ttu-id="1ceaa-116">Ad hello hizmeti ve URL uç noktası</span><span class="sxs-lookup"><span data-stu-id="1ceaa-116">Name hello service and URL endpoint</span></span>

<span data-ttu-id="1ceaa-117">Bir hizmet adı API çağrıları karşı verildiği hello URL uç noktası'nın bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-117">A service name is part of hello URL endpoint against which API calls are issued.</span></span> <span data-ttu-id="1ceaa-118">Hello hizmet adınızı yazın **URL** alan.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-118">Type your service name in hello **URL** field.</span></span> 

<span data-ttu-id="1ceaa-119">Hizmet adı gereksinimleri:</span><span class="sxs-lookup"><span data-stu-id="1ceaa-119">Service name requirements:</span></span>
   * <span data-ttu-id="1ceaa-120">uzunluğu 2 ile 60 karakter</span><span class="sxs-lookup"><span data-stu-id="1ceaa-120">2 and 60 characters in length</span></span>
   * <span data-ttu-id="1ceaa-121">küçük harf, rakam veya kısa çizgi ("-")</span><span class="sxs-lookup"><span data-stu-id="1ceaa-121">lowercase letters, digits, or dashes ("-")</span></span>
   * <span data-ttu-id="1ceaa-122">hiçbir kısa çizgi ("-") ilk 2 karakteri veya son tek karakter hello gibi</span><span class="sxs-lookup"><span data-stu-id="1ceaa-122">no dash ("-") as hello first 2 characters or last single character</span></span>
   * <span data-ttu-id="1ceaa-123">Art arda gelen tirelere ("--")</span><span class="sxs-lookup"><span data-stu-id="1ceaa-123">no consecutive dashes ("--")</span></span>

## <a name="select-a-subscription"></a><span data-ttu-id="1ceaa-124">Abonelik seçin</span><span class="sxs-lookup"><span data-stu-id="1ceaa-124">Select a subscription</span></span>
<span data-ttu-id="1ceaa-125">Birden fazla aboneliğiniz varsa, veri veya dosya depolama hizmetleri de sahip seçin.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-125">If you have more than one subscription, choose one that also has data or file storage services.</span></span> <span data-ttu-id="1ceaa-126">Azure arama otomatik algıla Azure Table ve Blob Depolama, SQL Database ve Azure Cosmos DB aracılığıyla dizin oluşturma için *dizin oluşturucular*, ancak yalnızca hello hizmetler için aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-126">Azure Search can auto-detect Azure Table and Blob storage, SQL Database, and Azure Cosmos DB for indexing via *indexers*, but only for services in hello same subscription.</span></span>

## <a name="select-a-resource-group"></a><span data-ttu-id="1ceaa-127">Kaynak grubu seç</span><span class="sxs-lookup"><span data-stu-id="1ceaa-127">Select a resource group</span></span>
<span data-ttu-id="1ceaa-128">Bir kaynak grubu, Azure Hizmetleri ve birlikte kullanılan kaynakları koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-128">A resource group is a collection of Azure services and resources used together.</span></span> <span data-ttu-id="1ceaa-129">Azure Search tooindex bir SQL veritabanı kullanıyorsanız, örneğin, ardından her iki hizmet hello parçası olmalıdır aynı kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-129">For example, if you are using Azure Search tooindex a SQL database, then both services should be part of hello same resource group.</span></span>

> [!TIP]
> <span data-ttu-id="1ceaa-130">Bir kaynak grubunu silme hello Hizmetleri içindeki siler.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-130">Deleting a resource group also deletes hello services within it.</span></span> <span data-ttu-id="1ceaa-131">Merhaba proje bittikten sonra birden çok hizmet yararlanarak, bunların tümünün hello koyma prototip projeleri için aynı kaynak grubunu temizleme kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-131">For prototype projects utilizing multiple services, putting all of them in hello same resource group makes cleanup easier after hello project is over.</span></span> 

## <a name="select-a-hosting-location"></a><span data-ttu-id="1ceaa-132">Bir barındırma konumu seçin</span><span class="sxs-lookup"><span data-stu-id="1ceaa-132">Select a hosting location</span></span> 
<span data-ttu-id="1ceaa-133">Bir Azure hizmeti Azure arama Merhaba Dünya veri merkezlerinde barındırılabilir.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-133">As an Azure service, Azure Search can be hosted in datacenters around hello world.</span></span> <span data-ttu-id="1ceaa-134">Unutmayın [fiyatlar farklı](https://azure.microsoft.com/pricing/details/search/) coğrafyaya.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-134">Note that [prices can differ](https://azure.microsoft.com/pricing/details/search/) by geography.</span></span>

## <a name="select-a-pricing-tier-sku"></a><span data-ttu-id="1ceaa-135">(SKU) bir fiyatlandırma katmanı seçin</span><span class="sxs-lookup"><span data-stu-id="1ceaa-135">Select a pricing tier (SKU)</span></span>
<span data-ttu-id="1ceaa-136">[Azure arama şu anda birden çok fiyatlandırma katmanında sunulan](https://azure.microsoft.com/pricing/details/search/): ücretsiz, temel veya standart.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-136">[Azure Search is currently offered in multiple pricing tiers](https://azure.microsoft.com/pricing/details/search/): Free, Basic, or Standard.</span></span> <span data-ttu-id="1ceaa-137">Her katman kendi sahip [kapasite ve sınırlar](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="1ceaa-137">Each tier has its own [capacity and limits](search-limits-quotas-capacity.md).</span></span> <span data-ttu-id="1ceaa-138">Bkz: [bir fiyatlandırma katmanı SKU seçin veya](search-sku-tier.md) Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-138">See [Choose a pricing tier or SKU](search-sku-tier.md) for guidance.</span></span>

<span data-ttu-id="1ceaa-139">Bu kılavuzda, biz hello standart katmanı hizmetimizi için seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-139">In this walkthrough, we have chosen hello Standard tier for our service.</span></span>

## <a name="create-your-service"></a><span data-ttu-id="1ceaa-140">Hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ceaa-140">Create your service</span></span>

<span data-ttu-id="1ceaa-141">Oturum zaman toopin hizmet toohello panonuz kolay erişim için unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-141">Remember toopin your service toohello dashboard for easy access whenever you sign in.</span></span>

![](./media/search-create-service-portal/new-service2.png)

## <a name="scale-your-service"></a><span data-ttu-id="1ceaa-142">Hizmetinizi ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="1ceaa-142">Scale your service</span></span>
<span data-ttu-id="1ceaa-143">Bu işlem birkaç dakika toocreate (15 dakika veya daha fazla hello katmanına bağlı olarak) bir hizmet alabilir.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-143">It can take a few minutes toocreate a service (15 minutes or more depending on hello tier).</span></span> <span data-ttu-id="1ceaa-144">Hizmetinizi sağlandıktan sonra toomeet ölçeklendirebilirsiniz gereksinimlerinizi.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-144">After your service is provisioned, you can scale it toomeet your needs.</span></span> <span data-ttu-id="1ceaa-145">Azure Search hizmetinizin hello standart katmanı seçtiğinden hizmetinizi iki boyut ölçeklendirebilirsiniz: çoğaltmaları ve bölümler.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-145">Because you chose hello Standard tier for your Azure Search service, you can scale your service in two dimensions: replicas and partitions.</span></span> <span data-ttu-id="1ceaa-146">Merhaba temel katmana tercih etmiş, çoğaltmaları yalnızca ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-146">Had you chosen hello Basic tier, you can only add replicas.</span></span> <span data-ttu-id="1ceaa-147">Merhaba ücretsiz hizmet sağlanan, Ölçek kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-147">If you provisioned hello free service, scale is not available.</span></span>

<span data-ttu-id="1ceaa-148">***Bölümler*** hizmet toostore ve daha fazla belge arama izin verir.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-148">***Partitions*** allow your service toostore and search through more documents.</span></span>

<span data-ttu-id="1ceaa-149">***Çoğaltmaları*** hizmet toohandle arama sorguları daha yüksek yükü izin.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-149">***Replicas*** allow your service toohandle a higher load of search queries.</span></span>

> [!Important]
> <span data-ttu-id="1ceaa-150">Bir hizmet olmalıdır [salt okunur SLA için 2 çoğaltma ve 3 çoğaltmaları için okuma/yazma SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span><span class="sxs-lookup"><span data-stu-id="1ceaa-150">A service must have [2 replicas for read-only SLA and 3 replicas for read/write SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span></span>

1. <span data-ttu-id="1ceaa-151">Tooyour arama hizmeti dikey penceresinde hello Azure portalına gidin.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-151">Go tooyour search service blade in hello Azure portal.</span></span>
2. <span data-ttu-id="1ceaa-152">Merhaba sol gezinti bölmesinde seçin **ayarları** > **ölçek**.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-152">In hello left-navigation pane, select **Settings** > **Scale**.</span></span>
3. <span data-ttu-id="1ceaa-153">Merhaba slidebar tooadd çoğaltmaları veya bölümleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-153">Use hello slidebar tooadd Replicas or Partitions.</span></span>

![](./media/search-create-service-portal/settings-scale.png)

> [!Note] 
> <span data-ttu-id="1ceaa-154">Her katman farklı olan [sınırları](search-limits-quotas-capacity.md) hello arama birimi tek bir hizmet olarak izin verilen toplam sayısı (çoğaltmaları * bölümleri toplam arama birimi =).</span><span class="sxs-lookup"><span data-stu-id="1ceaa-154">Each tier has different [limits](search-limits-quotas-capacity.md) on hello total number of Search Units allowed in a single service (Replicas * Partitions = Total Search Units).</span></span>

## <a name="when-tooadd-a-second-service"></a><span data-ttu-id="1ceaa-155">Zaman tooadd ikinci bir hizmeti</span><span class="sxs-lookup"><span data-stu-id="1ceaa-155">When tooadd a second service</span></span>

<span data-ttu-id="1ceaa-156">Müşteriler büyük bir çoğunluğu kullanmak hello sağlayan bir katmanını sağlanan tek hizmet [sağ kaynakları bakiyesini](search-sku-tier.md).</span><span class="sxs-lookup"><span data-stu-id="1ceaa-156">A large majority of customers use just one service provisioned at a tier that provides hello [right balance of resources](search-sku-tier.md).</span></span> <span data-ttu-id="1ceaa-157">Bir hizmet birden çok dizin, konu toohello barındırabilir [seçtiğiniz hello katmanının maksimum sınırları](search-capacity-planning.md), başka bir yalıtılmış her dizine sahip.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-157">One service can host multiple indexes, subject toohello [maximum limits of hello tier you select](search-capacity-planning.md), with each index isolated from another.</span></span> <span data-ttu-id="1ceaa-158">Yönlendirilmiş tooone dizin olmalıdır, diğer yanlışlıkla veya kasıtlı veri alma hello olasılığını en aza hello aynı dizinler yalnızca Azure Search'te istekleri için hizmet.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-158">In Azure Search, requests can only be directed tooone index, minimizing hello chance of accidental or intentional data retrieval from other indexes in hello same service.</span></span>

<span data-ttu-id="1ceaa-159">Müşterilerin çoğu yalnızca bir hizmet kullansa da, hizmet artıklık işletimsel gereksinimlerini hello aşağıdaki eklerseniz gerekli olabilir:</span><span class="sxs-lookup"><span data-stu-id="1ceaa-159">Although most customers use just one service, service redundancy might be necessary if operational requirements include hello following:</span></span>

+ <span data-ttu-id="1ceaa-160">Olağanüstü Durum Kurtarma (veri merkezi kesintisinden).</span><span class="sxs-lookup"><span data-stu-id="1ceaa-160">Disaster recovery (data center outage).</span></span> <span data-ttu-id="1ceaa-161">Azure arama kesinti hello olayı içinde anlık yük devretme sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-161">Azure Search does not provide instant failover in hello event of an outage.</span></span> <span data-ttu-id="1ceaa-162">Öneriler ve yönergeler için bkz: [Hizmet Yönetim](search-manage.md).</span><span class="sxs-lookup"><span data-stu-id="1ceaa-162">For recommendations and guidance, see [Service administration](search-manage.md).</span></span>
+ <span data-ttu-id="1ceaa-163">Araştırmanızı çoklu kiracı model ek hizmetler hello en uygun tasarımı olduğunu belirledi.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-163">Your investigation of multi-tenancy modeling has determined that additional services is hello optimal design.</span></span> <span data-ttu-id="1ceaa-164">Daha fazla bilgi için bkz: [çoklu kiracı için tasarım](search-modeling-multitenant-saas-applications.md).</span><span class="sxs-lookup"><span data-stu-id="1ceaa-164">For more information, see [Design for multi-tenancy](search-modeling-multitenant-saas-applications.md).</span></span>
+ <span data-ttu-id="1ceaa-165">Genel olarak dağıtılan uygulamalar için birden çok bölgeleri toominimize gecikme uygulamanızın uluslararası trafiği Azure Search örneğini gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-165">For globally deployed applications, you might require an instance of Azure Search in multiple regions toominimize latency of your application’s international traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="1ceaa-166">Azure Search'te dizin oluşturma ve sorgulama iş yükleri kurabilmeleri olamaz; Bu nedenle, birden fazla hizmet ayrı iş yükleri için hiçbir zaman oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-166">In Azure Search, you cannot segregate indexing and querying workloads; thus, you would never create multiple services for segregated workloads.</span></span> <span data-ttu-id="1ceaa-167">Bir dizin kapsamda oluşturulan hello hizmette her zaman sorgulanan (bir hizmetinde bir dizin oluşturamaz veya tooanother Kopyala).</span><span class="sxs-lookup"><span data-stu-id="1ceaa-167">An index is always queried on hello service in which it was created (you cannot create an index in one service and copy it tooanother).</span></span>
>

<span data-ttu-id="1ceaa-168">İkinci bir hizmet yüksek kullanılabilirlik için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-168">A second service is not required for high availability.</span></span> <span data-ttu-id="1ceaa-169">Yüksek kullanılabilirlik sorgular için 2'yi kullanın ya da daha fazla yinelemede aynı hizmet hello elde edilir.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-169">High availability for queries is achieved when you use 2 or more replicas in hello same service.</span></span> <span data-ttu-id="1ceaa-170">Çoğaltma güncelleştirmeleri sıralı, bir hizmet güncelleştirmesi gezinirken en az bir işlem olduğu anlamına gelir. Açık kalma süresi hakkında daha fazla bilgi için bkz: [hizmet düzeyi sözleşmeleri](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span><span class="sxs-lookup"><span data-stu-id="1ceaa-170">Replica updates are sequential, which means at least one is operational when a service update is rolled out. For more information about uptime, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ceaa-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1ceaa-171">Next steps</span></span>
<span data-ttu-id="1ceaa-172">Azure Search Hizmeti sağladıktan sonra çok hazır olduğunuz[bir dizin tanımla](search-what-is-an-index.md) karşıya yükleme ve verilerinizi arama.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-172">After provisioning an Azure Search service, you are ready too[define an index](search-what-is-an-index.md) so you can upload and search your data.</span></span>

<span data-ttu-id="1ceaa-173">tooaccess hello hizmetinden kod veya komut dosyası, hello URL'si sağlayın (*hizmet adı*. search.windows.net) ve anahtar.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-173">tooaccess hello service from code or script, provide hello URL (*service-name*.search.windows.net) and a key.</span></span> <span data-ttu-id="1ceaa-174">Yönetici anahtarlarına tam erişim; Sorgu anahtarları salt okunur erişim verin.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-174">Admin keys grant full access; query keys grant read-only access.</span></span> <span data-ttu-id="1ceaa-175">Bkz: [toouse Azure arama nasıl .NET](search-howto-dotnet-sdk.md) tooget başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-175">See [How toouse Azure Search in .NET](search-howto-dotnet-sdk.md) tooget started.</span></span>

<span data-ttu-id="1ceaa-176">Bkz: [oluşturmak ve ilk dizininizi sorgulama](search-get-started-portal.md) portal tabanlı hızlı bir öğretici.</span><span class="sxs-lookup"><span data-stu-id="1ceaa-176">See [Build and query your first index](search-get-started-portal.md) for a quick portal-based tutorial.</span></span>

