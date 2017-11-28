---
title: "Azure portal: SQL Database esnek havuzunu yönetme & Oluştur | Microsoft Docs"
description: "Nasıl toouse Azure portal ve SQL Database'in yerleşik zekaya toomanage, İzleyici ve boyutlandırmanıza ölçeklenebilir bir esnek havuz toooptimize veritabanı performansını hello ve maliyet yönetmek öğrenin."
keywords: 
services: sql-database
documentationcenter: 
author: ninarn
manager: jhubbard
editor: cgronlun
ms.assetid: 3dc9b7a3-4b10-423a-8e44-9174aca5cf3d
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 06/06/2016
ms.author: ninarn
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: e0de952bc0c91177f64c04363630783d72435741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-hello-azure-portal"></a><span data-ttu-id="bc7c7-103">Oluşturma ve bir esnek havuz hello Azure portal ile yönetme</span><span class="sxs-lookup"><span data-stu-id="bc7c7-103">Create and manage an elastic pool with hello Azure portal</span></span>
<span data-ttu-id="bc7c7-104">Bu konu, nasıl gösterir toocreate ve ölçeklenebilir yönetmek [esnek havuzlar](sql-database-elastic-pool.md) hello Azure portal ile.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with hello Azure portal.</span></span> <span data-ttu-id="bc7c7-105">Ayrıca oluşturabilir ve ile Azure esnek havuzunu yönetme [PowerShell](sql-database-elastic-pool-manage-powershell.md), REST API hello veya [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="bc7c7-105">You can also create and manage an Azure elastic pool with [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="bc7c7-106">Ayrıca oluşturun ve içine ve dışına esnek havuzlar kullanarak veritabanlarını taşıma [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="bc7c7-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

## <a name="create-an-elastic-pool"></a><span data-ttu-id="bc7c7-107">Esnek havuz oluşturma</span><span class="sxs-lookup"><span data-stu-id="bc7c7-107">Create an elastic pool</span></span> 

<span data-ttu-id="bc7c7-108">Bir esnek havuz oluşturmanın iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-108">There are two ways you can create an elastic pool.</span></span> <span data-ttu-id="bc7c7-109">İstediğiniz ya da bir öneri hello hizmetinden başlayın hello havuz kurulumunu biliyorsanız sıfırdan yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-109">You can do it from scratch if you know hello pool setup you want, or start with a recommendation from hello service.</span></span> <span data-ttu-id="bc7c7-110">SQL veritabanı maliyet açısından daha verimli kullanım telemetri veritabanlarınız için geçmiş hello temel alarak için ise, bir esnek havuz Kurulumu önerdiği yerleşik zekaya sahiptir.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-110">SQL Database has built-in intelligence that recommends an elastic pool setup if it's more cost-efficient for you based on hello past usage telemetry for your databases.</span></span>

<span data-ttu-id="bc7c7-111">Bir sunucuda birden çok havuz oluşturabilirsiniz, ancak hello farklı sunuculara ait veritabanlarını ekleyemezsiniz aynı havuzu.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-111">You can create multiple pools on a server, but you can't add databases from different servers into hello same pool.</span></span> 

> [!NOTE]
> <span data-ttu-id="bc7c7-112">Esnek havuzlar şu anda önizleme aşamasında oldukları Batı Hindistan dışında tüm Azure bölgelerinde genel olarak kullanılabilir (GA) durumdadır.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-112">Elastic pools are generally available (GA) in all Azure regions except West India where it is currently in preview.</span></span>  <span data-ttu-id="bc7c7-113">Bu bölgede esnek havuz GA’sı olabildiğince çabuk ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-113">GA of elastic pools in this region will occur as soon as possible.</span></span>
>

### <a name="step-1-create-an-elastic-pool"></a><span data-ttu-id="bc7c7-114">1. adım: bir esnek havuz oluşturma</span><span class="sxs-lookup"><span data-stu-id="bc7c7-114">Step 1: Create an elastic pool</span></span>

<span data-ttu-id="bc7c7-115">Mevcut bir esnek havuz oluşturma **server** dikey penceresinde hello portal hello en kolay yolu toomove varolan veritabanlarına bir esnek havuz değil.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-115">Creating an elastic pool from an existing **server** blade in hello portal is hello easiest way toomove existing databases into an elastic pool.</span></span>

> [!NOTE]
> <span data-ttu-id="bc7c7-116">Arayarak bir esnek havuz oluşturabilirsiniz **SQL esnek havuzu** hello içinde **Market** veya tıklatarak **+ Ekle** hello içinde **SQL esnek havuzu**dikey göz atın.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-116">You can also create an elastic pool by searching **SQL elastic pool** in hello **Marketplace** or clicking **+Add** in hello **SQL elastic pools** browse blade.</span></span> <span data-ttu-id="bc7c7-117">Mümkün toospecify yeni veya var olan bir sunucu iş akışı sağlama bu havuzu üzerinden var.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-117">You are able toospecify a new or existing server through this pool provisioning workflow.</span></span>
>
>

1. <span data-ttu-id="bc7c7-118">Merhaba, [Azure portal](http://portal.azure.com/), tıklatın **daha fazla hizmet**  **>**  **SQL sunucuları**ve hello içeren hello server'ı tıklatın veritabanları tooadd tooan esnek havuz istiyor.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-118">In hello [Azure portal](http://portal.azure.com/), click **More services** **>** **SQL servers**, and then click hello server that contains hello databases you want tooadd tooan elastic pool.</span></span>
2. <span data-ttu-id="bc7c7-119">**Yeni havuz** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-119">Click **New pool**.</span></span>

    ![Havuz tooa sunucu ekleme](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    <span data-ttu-id="bc7c7-121">**-VEYA-**</span><span class="sxs-lookup"><span data-stu-id="bc7c7-121">**-OR-**</span></span>

    <span data-ttu-id="bc7c7-122">Bulunduğunu belirten bir ileti esnek havuzlar hello sunucu için önerilen görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-122">You may see a message saying there are recommended elastic pools for hello server.</span></span> <span data-ttu-id="bc7c7-123">Önerilen havuzları geçmişe yönelik veritabanı kullanımı telemetrisi göz önünde bulundurularak hello ileti toosee hello tıklatın hello katmanı toosee daha fazla ayrıntı ve ardından hello havuzu özelleştirmek.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-123">Click hello message toosee hello recommended pools based on historical database usage telemetry, and then click hello tier toosee more details and customize hello pool.</span></span> <span data-ttu-id="bc7c7-124">Bkz: [havuz önerilerini anlama](#understand-elastic-pool-recommendations) hello öneri nasıl sunulacağını için bu konudaki sonraki.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-124">See [Understand pool recommendations](#understand-elastic-pool-recommendations) later in this topic for how hello recommendation is made.</span></span>

    ![önerilen havuz](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. <span data-ttu-id="bc7c7-126">Merhaba **esnek havuz** dikey penceresi görünür, hello ayarları havuzunuz için burada belirttiğiniz olduğu.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-126">hello **elastic pool** blade appears, which is where you specify hello settings for your pool.</span></span> <span data-ttu-id="bc7c7-127">Tıkladıysanız **yeni havuz** fiyatlandırma katmanı hello hello önceki adımda olduğu **standart** varsayılan ve hiçbir veritabanı tarafından seçilir.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-127">If you clicked **New pool** in hello previous step, hello pricing tier is **Standard** by default and no databases is selected.</span></span> <span data-ttu-id="bc7c7-128">Boş bir havuz oluşturmak veya mevcut veritabanlarından bu sunucu toomove kümesi hello havuza belirtin.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-128">You can create an empty pool, or specify a set of existing databases from that server toomove into hello pool.</span></span> <span data-ttu-id="bc7c7-129">Önerilen bir havuzu oluşturuyorsanız, fiyatlandırma katmanı, performans ayarlarını hello önerilen ve veritabanlarının listesini önceden doldurulmaz ancak hala bunları değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-129">If you are creating a recommended pool, hello recommended pricing tier, performance settings, and list of databases are prepopulated, but you can still change them.</span></span>

    ![Esnek havuzu yapılandırma](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. <span data-ttu-id="bc7c7-131">Merhaba esnek havuz için bir ad belirtin veya hello varsayılan olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-131">Specify a name for hello elastic pool, or leave it as hello default.</span></span>

### <a name="step-2-choose-a-pricing-tier"></a><span data-ttu-id="bc7c7-132">2. Adım: Fiyatlandırma katmanı seçme</span><span class="sxs-lookup"><span data-stu-id="bc7c7-132">Step 2: Choose a pricing tier</span></span>

<span data-ttu-id="bc7c7-133">Merhaba havuzun fiyatlandırma katmanı hello kullanılabilir toohello elastics hello havuzu ve hello maksimum sayısını Edtu (Maks eDTU) ve depolama (GB) kullanılabilir tooeach veritabanı özellikleri belirler.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-133">hello pool's pricing tier determines hello features available toohello elastics in hello pool, and hello maximum number of eDTUs (eDTU MAX), and storage (GBs) available tooeach database.</span></span> <span data-ttu-id="bc7c7-134">Ayrıntılı bilgi için bkz. Hizmet Katmanları.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-134">For details, see Service Tiers.</span></span>

<span data-ttu-id="bc7c7-135">Merhaba havuzu için toochange hello fiyatlandırma Katmanı'nı tıklatın **fiyatlandırma katmanı**, fiyatlandırma katmanı ve ardından hello tıklatın **seçin**.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-135">toochange hello pricing tier for hello pool, click **Pricing tier**, click hello pricing tier you want, and then click **Select**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc7c7-136">Merhaba fiyatlandırma katmanı seçin ve değişikliklerinizi tıklatılarak sonra **Tamam** hello son adımda fiyatlandırma katmanı hello havuzunun mümkün toochange hello olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-136">After you choose hello pricing tier and commit your changes by clicking **OK** in hello last step, you won't be able toochange hello pricing tier of hello pool.</span></span> <span data-ttu-id="bc7c7-137">toochange var olan bir esnek havuz için fiyatlandırma katmanı Merhaba, hello istenen fiyatlandırma katmanında bir esnek havuz oluşturun ve hello veritabanları toothis yeni havuzunu geçirin.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-137">toochange hello pricing tier for an existing elastic pool, create an elastic pool in hello desired pricing tier and migrate hello databases toothis new pool.</span></span>
>

![Fiyatlandırma katmanı seçme](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-hello-pool"></a><span data-ttu-id="bc7c7-139">3. adım: hello havuzu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bc7c7-139">Step 3: Configure hello pool</span></span>

<span data-ttu-id="bc7c7-140">Fiyatlandırma katmanı hello ayarladıktan sonra havuzu Yapılandır veritabanları, havuz edtu'larını ve depolama (havuz GB) ekleyebilir ve hello havuzunda hello minimum ve maksimum Edtu hello elastics için ayarladığınız tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-140">After setting hello pricing tier, click Configure pool where you add databases, set pool eDTUs and storage (pool GBs), and where you set hello min and max eDTUs for hello elastics in hello pool.</span></span>

1. <span data-ttu-id="bc7c7-141">**Havuzu yapılandır**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-141">Click **Configure pool**</span></span>
2. <span data-ttu-id="bc7c7-142">Tooadd toohello havuzu istediğiniz hello veritabanlarını seçin.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-142">Select hello databases you want tooadd toohello pool.</span></span> <span data-ttu-id="bc7c7-143">Merhaba havuz oluşturulurken bu adım isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-143">This step is optional while creating hello pool.</span></span> <span data-ttu-id="bc7c7-144">Merhaba havuzu oluşturulduktan sonra veritabanları eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-144">Databases can be added after hello pool has been created.</span></span>
    <span data-ttu-id="bc7c7-145">tooadd veritabanları'nı **veritabanı Ekle**, tooadd istediğiniz ve hello ardından hello veritabanları'nı **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-145">tooadd databases, click **Add database**, click hello databases that you want tooadd, and then click hello **Select** button.</span></span>

    ![Veritabanı ekleme](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    <span data-ttu-id="bc7c7-147">Merhaba veritabanları ile çalışırken yeterli geçmiş kullanımı telemetri varsa, hello **tahmini eDTU ve GB kullanımı** grafik ve hello **gerçek eDTU kullanımı** çubuk grafik güncelleştirme toohelp, yaptığınız yapılandırma kararlar.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-147">If hello databases you're working with have enough historical usage telemetry, hello **Estimated eDTU and GB usage** graph and hello **Actual eDTU usage** bar chart update toohelp you make configuration decisions.</span></span> <span data-ttu-id="bc7c7-148">Ayrıca, hello hizmeti, bir öneri iletisi toohelp verebilir, boyutlandırmanıza hello havuzu.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-148">Also, hello service may give you a recommendation message toohelp you right-size hello pool.</span></span> <span data-ttu-id="bc7c7-149">Bkz. [Dinamik Öneriler](#understand-elastic-pool-recommendations).</span><span class="sxs-lookup"><span data-stu-id="bc7c7-149">See [Dynamic Recommendations](#understand-elastic-pool-recommendations).</span></span>

3. <span data-ttu-id="bc7c7-150">Merhaba Hello denetimleri kullanın **havuzu yapılandırma** sayfa tooexplore ayarları ve havuzunuzu yapılandırmak.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-150">Use hello controls on hello **Configure pool** page tooexplore settings and configure your pool.</span></span> <span data-ttu-id="bc7c7-151">Bkz: [esnek havuz sınırları](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) daha fazla bilgi için her bir hizmet katmanına yönelik sınırlar hakkında ayrıntı ve bkz [esnek havuzlar için fiyat ve performans konuları](sql-database-elastic-pool.md) ayrıntılı yönergeler boyutlandırmaya bir esnek havuz.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-151">See [Elastic pools limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for more detail about limits for each service tier, and see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md) for detailed guidance on right-sizing an elastic pool.</span></span> <span data-ttu-id="bc7c7-152">Havuz ayarları hakkında daha fazla bilgi için bkz: [esnek havuz özellikleri](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span><span class="sxs-lookup"><span data-stu-id="bc7c7-152">For more information about pool settings, see [Elastic pool properties](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span></span>

    ![Esnek Havuzu Yapılandırma](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. <span data-ttu-id="bc7c7-154">Tıklatın **seçin** hello içinde **havuzu Yapılandır** dikey ayarlarını değiştirdikten sonra.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-154">Click **Select** in hello **Configure Pool** blade after changing settings.</span></span>
5. <span data-ttu-id="bc7c7-155">Tıklatın **Tamam** toocreate hello havuzu.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-155">Click **OK** toocreate hello pool.</span></span>

## <a name="understand-elastic-pool-recommendations"></a><span data-ttu-id="bc7c7-156">Esnek havuz önerilerini anlama</span><span class="sxs-lookup"><span data-stu-id="bc7c7-156">Understand elastic pool recommendations</span></span>

<span data-ttu-id="bc7c7-157">Merhaba SQL veritabanı hizmetinin kullanım geçmişini değerlendirir ve onu tek veritabanlarını kullanmaktan daha verimliyse bir veya daha fazla havuzun kullanılmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-157">hello SQL Database service evaluates usage history and recommends one or more pools when it is more cost-effective than using single databases.</span></span> <span data-ttu-id="bc7c7-158">Her öneri hello havuzu en uygun hello sunucunun veritabanlarına benzersiz bir alt kümesiyle yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-158">Each recommendation is configured with a unique subset of hello server's databases that best fit hello pool.</span></span>

![önerilen havuz](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

<span data-ttu-id="bc7c7-160">Merhaba havuz önerisi şunları kapsar:</span><span class="sxs-lookup"><span data-stu-id="bc7c7-160">hello pool recommendation comprises:</span></span>

- <span data-ttu-id="bc7c7-161">Merhaba havuzu (temel, standart, Premium veya Premium RS) için bir fiyatlandırma katmanı</span><span class="sxs-lookup"><span data-stu-id="bc7c7-161">A pricing tier for hello pool (Basic, Standard, Premium, or Premium RS)</span></span>
- <span data-ttu-id="bc7c7-162">Uygun **HAVUZ eDTU'ları** (havuz başına maksimum eDTU olarak da adlandırılır)</span><span class="sxs-lookup"><span data-stu-id="bc7c7-162">Appropriate **POOL eDTUs** (also called Max eDTUs per pool)</span></span>
- <span data-ttu-id="bc7c7-163">Merhaba **maksimum eDTU** ve **eDTU minimum** veritabanı başına</span><span class="sxs-lookup"><span data-stu-id="bc7c7-163">hello **eDTU MAX** and **eDTU Min** per database</span></span>
- <span data-ttu-id="bc7c7-164">Merhaba hello havuzu için önerilen veritabanlarının listesi</span><span class="sxs-lookup"><span data-stu-id="bc7c7-164">hello list of recommended databases for hello pool</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc7c7-165">Merhaba hizmet Merhaba, son 30 gün telemetri havuzları öneren zaman dikkate alır.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-165">hello service takes hello last 30 days of telemetry into account when recommending pools.</span></span> <span data-ttu-id="bc7c7-166">Esnek havuz için aday olarak kabul veritabanı toobe en az 7 gündür bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-166">For a database toobe considered as a candidate for an elastic pool, it must exist for at least 7 days.</span></span> <span data-ttu-id="bc7c7-167">Zaten bir elastik havuzda bulunan veritabanları, elastik havuz önerileri için aday olarak kabul edilmez.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-167">Databases that are already in an elastic pool are not considered as candidates for elastic pool recommendations.</span></span>
>

<span data-ttu-id="bc7c7-168">Merhaba hizmeti kaynak gereksinimlerini değerlendirir ve maliyet verimliliğini taşıma hello tek veritabanlarını her hizmet katmanında hello havuzları halinde aynı katmanı.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-168">hello service evaluates resource needs and cost effectiveness of moving hello single databases in each service tier into pools of hello same tier.</span></span> <span data-ttu-id="bc7c7-169">Örneğin, bir sunucudaki tüm Standart veritabanları Standart Esnek Havuz'a uygunluk açısından değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-169">For example, all Standard databases on a server are assessed for their fit into a Standard Elastic Pool.</span></span> <span data-ttu-id="bc7c7-170">Bu, hello hizmeti bir standart veritabanının bir Premium havuza taşınması gibi çapraz katmanlı önerilerde bulunmadığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-170">This means hello service does not make cross-tier recommendations such as moving a Standard database into a Premium pool.</span></span>

<span data-ttu-id="bc7c7-171">Veritabanlarını toohello havuzuna eklendikten sonra öneriler dinamik olarak hello geçmiş kullanımı, seçtiğiniz hello veritabanlarının dikkate alarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-171">After adding databases toohello pool, recommendations are dynamically generated based on hello historical usage of hello databases you have selected.</span></span> <span data-ttu-id="bc7c7-172">Bu öneriler hello eDTU ve GB kullanım grafiğinde ve bir öneri başlığının hello hello üstünde gösterilir **havuzu yapılandırma** dikey.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-172">These recommendations are shown in hello eDTU and GB usage chart and in a recommendation banner at hello top of hello **Configure pool** blade.</span></span> <span data-ttu-id="bc7c7-173">Bu öneriler, bir esnek havuz oluşturma belirli veritabanlarınız için iyileştirilmiş hedeflenen tooassist içindir.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-173">These recommendations are intended tooassist you in creating an elastic pool optimized for your specific databases.</span></span>

![dinamik öneriler](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a><span data-ttu-id="bc7c7-175">Yönetme ve bir esnek Havuz izleme</span><span class="sxs-lookup"><span data-stu-id="bc7c7-175">Manage and monitor an elastic pool</span></span>

<span data-ttu-id="bc7c7-176">Hello Azure portal toomonitor kullanın ve hello havuzu hello veritabanlarını ve esnek havuz yönetin.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-176">You can use hello Azure portal toomonitor and manage an elastic pool and hello databases in hello pool.</span></span> <span data-ttu-id="bc7c7-177">Merhaba Portalı'ndan bir esnek havuz ve hello veritabanları aynı havuz içindeki hello kullanımını izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-177">From hello portal, you can monitor hello utilization of an elastic pool and hello databases within that pool.</span></span> <span data-ttu-id="bc7c7-178">Ayrıca bir değişiklik kümesini tooyour esnek havuzu yapmak ve tüm değişiklikler hello aynı gönderme zamanı.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-178">You can also make a set of changes tooyour elastic pool and submit all changes at hello same time.</span></span> <span data-ttu-id="bc7c7-179">Bu değişiklikler ekleyerek veya veritabanları kaldırma, esnek havuz ayarlarınızı değiştirme veya veritabanı ayarlarını değiştirerek içerir.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-179">These changes include adding or removing databases, changing your elastic pool settings, or changing your database settings.</span></span>

<span data-ttu-id="bc7c7-180">Grafiği aşağıdaki hello bir örnek esnek havuz gösterir.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-180">hello following graphic shows an example elastic pool.</span></span> <span data-ttu-id="bc7c7-181">Merhaba görünümü içerir:</span><span class="sxs-lookup"><span data-stu-id="bc7c7-181">hello view includes:</span></span>

*  <span data-ttu-id="bc7c7-182">Kaynak kullanımını hello esnek havuz ve hello havuzunda kapsanan hello veritabanlarını izleme grafikleri.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-182">Charts for monitoring resource usage of both hello elastic pool and hello databases contained in hello pool.</span></span>
*  <span data-ttu-id="bc7c7-183">Merhaba **yapılandırma** havuzu düğmesi toomake toohello esnek havuz değiştirir.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-183">hello **Configure** pool button toomake changes toohello elastic pool.</span></span>
*  <span data-ttu-id="bc7c7-184">Merhaba **veritabanı oluşturma** bir veritabanı oluşturur düğmesi ve toohello geçerli esnek havuz ekler.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-184">hello **Create database** button that creates a database and adds it toohello current elastic pool.</span></span>
*  <span data-ttu-id="bc7c7-185">Yardımcı esnek işler, listedeki tüm veritabanlarında Transact SQL komut dosyaları çalıştırarak veritabanları çok sayıda yönetin.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-185">Elastic jobs that help you manage large numbers of databases by running Transact SQL scripts against all databases in a list.</span></span>

![Havuz görünümü][2]

<span data-ttu-id="bc7c7-187">Kaynak kullanımı tooa belirli havuzu toosee gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-187">You can go tooa particular pool toosee its resource utilization.</span></span> <span data-ttu-id="bc7c7-188">Varsayılan olarak, hello hello son saat için yapılandırılmış tooshow depolama ve eDTU kullanımı havuzudur.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-188">By default, hello pool is configured tooshow storage and eDTU usage for hello last hour.</span></span> <span data-ttu-id="bc7c7-189">Merhaba grafik yapılandırılmış tooshow farklı ölçümleri çeşitli zaman pencereleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-189">hello chart can be configured tooshow different metrics over various time windows.</span></span>

1. <span data-ttu-id="bc7c7-190">Esnek havuz toowork ile seçin.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-190">Select an elastic pool toowork with.</span></span>
2. <span data-ttu-id="bc7c7-191">Altında **esnek Havuz izleme** olan etiketli bir grafik **kaynak kullanımı**.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-191">Under **Elastic Pool Monitoring** is a chart labeled **Resource utilization**.</span></span> <span data-ttu-id="bc7c7-192">Merhaba grafiği tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-192">Click hello chart.</span></span>

    ![Esnek Havuz izleme][3]

    <span data-ttu-id="bc7c7-194">Merhaba **ölçüm** , hello belirtilen zaman penceresi belirtilen ölçümleri hello ayrıntılı görünümünü gösteren dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-194">hello **Metric** blade opens, showing a detailed view of hello specified metrics over hello specified time window.</span></span>   

    ![Ölçüm dikey penceresi][9]

### <a name="toocustomize-hello-chart-display"></a><span data-ttu-id="bc7c7-196">toocustomize hello grafik görüntüleme</span><span class="sxs-lookup"><span data-stu-id="bc7c7-196">toocustomize hello chart display</span></span>

<span data-ttu-id="bc7c7-197">CPU yüzdesi, veri g/ç yüzdesi ve kullanılan günlük GÇ yüzdesi gibi diğer ölçümleri hello grafik ve hello ölçüm dikey penceresi toodisplay düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-197">You can edit hello chart and hello metric blade toodisplay other metrics such as CPU percentage, data IO percentage, and log IO percentage used.</span></span>

1. <span data-ttu-id="bc7c7-198">Merhaba ölçüm dikey penceresinde **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-198">On hello metric blade, click **Edit**.</span></span>

    ![Düzenle'yi tıklatın][6]

2. <span data-ttu-id="bc7c7-200">Merhaba, **grafiği Düzenle** dikey penceresinde bir zaman aralığı (saat, bugün, geçmiş veya geçen hafta) seçin veya tıklatın **özel** tooselect herhangi bir tarih aralığı hello son iki hafta.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-200">In hello **Edit Chart** blade, select a time range (past hour, today, or past week), or click **custom** tooselect any date range in hello last two weeks.</span></span> <span data-ttu-id="bc7c7-201">Merhaba grafik türü (çubuğu veya satırı) seçin, sonra hello kaynakları toomonitor seçin.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-201">Select hello chart type (bar or line), then select hello resources toomonitor.</span></span>

   > [!Note]
   > <span data-ttu-id="bc7c7-202">Aynı ölçü hello görüntülenebilir hello Ölçümleriyle hello aynı grafik yalnızca saat.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-202">Only metrics with hello same unit of measure can be displayed in hello chart at hello same time.</span></span> <span data-ttu-id="bc7c7-203">"EDTU yüzdesi" seçeneğini belirlerseniz Örneğin, ardından yalnızca diğer ölçümleri yüzdesiyle hello ölçü seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-203">For example, if you select "eDTU percentage" then you can only select other metrics with percentage as hello unit of measure.</span></span>
   >

    ![Düzenle'yi tıklatın](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. <span data-ttu-id="bc7c7-205">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-205">Then click **OK**.</span></span>

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a><span data-ttu-id="bc7c7-206">Yönetme ve esnek havuzdaki veritabanları izleme</span><span class="sxs-lookup"><span data-stu-id="bc7c7-206">Manage and monitor databases in an elastic pool</span></span>

<span data-ttu-id="bc7c7-207">Tek tek veritabanları için olası sorun de izlenebilir.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-207">Individual databases can also be monitored for potential trouble.</span></span>

1. <span data-ttu-id="bc7c7-208">Altında **esnek veritabanı izleme**, beş veritabanları için ölçümleri görüntüleyen bir grafik yoktur.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-208">Under **Elastic Database Monitoring**, there is a chart that displays metrics for five databases.</span></span> <span data-ttu-id="bc7c7-209">Varsayılan olarak, hello grafik hello üst 5 veritabanları hello havuzunda hello ortalama eDTU kullanımı tarafından son bir saat görüntüler.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-209">By default, hello chart displays hello top 5 databases in hello pool by average eDTU usage in hello past hour.</span></span> <span data-ttu-id="bc7c7-210">Merhaba grafiği tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-210">Click hello chart.</span></span>

    ![Esnek Havuz izleme][4]

2. <span data-ttu-id="bc7c7-212">Merhaba **veritabanı kaynak kullanımını** dikey penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-212">hello **Database Resource Utilization** blade appears.</span></span> <span data-ttu-id="bc7c7-213">Merhaba havuzunda hello veritabanı kullanımının ayrıntılı bir görünüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-213">This provides a detailed view of hello database usage in hello pool.</span></span> <span data-ttu-id="bc7c7-214">Merhaba dikey pencerenin alt bölümünde hello Hello kılavuzunda kullanarak, kullanım (yukarı too5 veritabanları) hello grafikte hello havuzu toodisplay tüm veritabanları seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-214">Using hello grid in hello lower part of hello blade, you can select any databases in hello pool toodisplay its usage in hello chart (up too5 databases).</span></span> <span data-ttu-id="bc7c7-215">Tıklayarak hello grafikte görüntülenen hello ölçümleri ve zaman penceresini özelleştirebilirsiniz **grafiği Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-215">You can also customize hello metrics and time window displayed in hello chart by clicking **Edit chart**.</span></span>

    ![Veritabanı kaynak kullanımı dikey][8]

### <a name="toocustomize-hello-view"></a><span data-ttu-id="bc7c7-217">toocustomize hello görünümü</span><span class="sxs-lookup"><span data-stu-id="bc7c7-217">toocustomize hello view</span></span>

1. <span data-ttu-id="bc7c7-218">Merhaba, **veritabanı kaynak kullanımını** dikey penceresinde tıklatın **grafiği Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-218">In hello **Database resource utilization** blade, click **Edit chart**.</span></span>

    ![Grafiği Düzenle'yi tıklatın](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. <span data-ttu-id="bc7c7-220">Merhaba, **Düzenle** grafik dikey penceresinde, bir zaman aralığı (saat sonraya veya son 24 saat) seçin veya **özel** tooselect 2 hafta toodisplay geçmiş hello farklı günde bir.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-220">In hello **Edit** chart blade, select a time range (past hour or past 24 hours), or click **custom** tooselect a different day in hello past 2 weeks toodisplay.</span></span>

    ![Özel'i tıklatın](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. <span data-ttu-id="bc7c7-222">Merhaba tıklatın **karşılaştırmak veritabanı tarafından** açılır tooselect veritabanları karşılaştırıldığında farklı bir ölçüm toouse.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-222">Click hello **Compare databases by** dropdown tooselect a different metric toouse when comparing databases.</span></span>

    ![Merhaba grafiği Düzenle](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a><span data-ttu-id="bc7c7-224">tooselect veritabanları toomonitor</span><span class="sxs-lookup"><span data-stu-id="bc7c7-224">tooselect databases toomonitor</span></span>

<span data-ttu-id="bc7c7-225">Merhaba hello veritabanı listesinde **veritabanı kaynak kullanımını** dikey penceresinde bulabilirsiniz belirli veritabanları hello listesinde hello sayfaları aracılığıyla bakarak veya veritabanının hello adını yazarak.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-225">In hello database list in hello **Database Resource Utilization** blade, you can find particular databases by looking through hello pages in hello list or by typing in hello name of a database.</span></span> <span data-ttu-id="bc7c7-226">Merhaba onay kutusunu tooselect hello veritabanını kullanın.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-226">Use hello checkbox tooselect hello database.</span></span>

![Veritabanlarını toomonitor arayın][7]


## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="bc7c7-228">Bir uyarı tooan esnek havuz kaynak ekleyin</span><span class="sxs-lookup"><span data-stu-id="bc7c7-228">Add an alert tooan elastic pool resource</span></span>

<span data-ttu-id="bc7c7-229">Merhaba esnek havuz sizin ayarladığınız bir kullanım eşiği geldiğinde, toopeople veya uyarı dizeleri tooURL uç noktaları e-posta Gönder kuralları tooan esnek havuz ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-229">You can add rules tooan elastic pool that send email toopeople or alert strings tooURL endpoints when hello elastic pool hits a utilization threshold that you set up.</span></span>

<span data-ttu-id="bc7c7-230">**bir uyarı tooany kaynak tooadd:**</span><span class="sxs-lookup"><span data-stu-id="bc7c7-230">**tooadd an alert tooany resource:**</span></span>

1. <span data-ttu-id="bc7c7-231">Hello tıklatın **kaynak kullanımı** grafik tooopen hello **ölçüm** dikey penceresinde tıklatın **uyarı Ekle**ve ardından hello hello bilgileri doldurun **uyarı ekleme Kural** dikey (**kaynak** toobe hello havuzu ile çalışırken yukarı otomatik olarak ayarlanır).</span><span class="sxs-lookup"><span data-stu-id="bc7c7-231">Click hello **Resource utilization** chart tooopen hello **Metric** blade, click **Add alert**, and then fill out hello information in hello **Add an alert rule** blade (**Resource** is automatically set up toobe hello pool you're working with).</span></span>
2. <span data-ttu-id="bc7c7-232">Tür a **adı** ve **açıklama** hello uyarı tooyou ve hello alıcıları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-232">Type a **Name** and **Description** that identifies hello alert tooyou and hello recipients.</span></span>
3. <span data-ttu-id="bc7c7-233">Seçin bir **ölçüm** hello listeden tooalert istiyor.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-233">Choose a **Metric** that you want tooalert from hello list.</span></span>

    <span data-ttu-id="bc7c7-234">Merhaba grafik bir eşik seçin, ölçüm toohelp için kaynak kullanımını dinamik olarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-234">hello chart dynamically shows resource utilization for that metric toohelp you choose a threshold.</span></span>

4. <span data-ttu-id="bc7c7-235">Seçin bir **koşulu** (büyüktür, küçüktür, vs.) ve bir **eşik**.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-235">Choose a **Condition** (greater than, less than, etc.) and a **Threshold**.</span></span>
5. <span data-ttu-id="bc7c7-236">Seçin bir **süresi** ölçüm hello süresini hello uyarı Tetikleyicileri önce kural sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-236">Choose a **Period** of time that hello metric rule must be satisfied before hello alert triggers.</span></span>
6. <span data-ttu-id="bc7c7-237">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-237">Click **OK**.</span></span>

<span data-ttu-id="bc7c7-238">Daha fazla bilgi için bkz: [Azure Portalı'nda SQL veritabanı uyarıları oluşturma](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bc7c7-238">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="bc7c7-239">Bir veritabanını bir esnek havuza taşıma</span><span class="sxs-lookup"><span data-stu-id="bc7c7-239">Move a database into an elastic pool</span></span>

<span data-ttu-id="bc7c7-240">Ekleyebilir veya var olan bir havuzdan veritabanları kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-240">You can add or remove databases from an existing pool.</span></span> <span data-ttu-id="bc7c7-241">Merhaba veritabanları diğer havuzlarında olabilir.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-241">hello databases can be in other pools.</span></span> <span data-ttu-id="bc7c7-242">Ancak, üzerinde aynı hello olan veritabanları yalnızca ekleyebileceğiniz mantıksal sunucu.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-242">However, you can only add databases that are on hello same logical server.</span></span>

1. <span data-ttu-id="bc7c7-243">Hello dikey penceresinde hello havuzunun altında **esnek veritabanları** tıklatın **havuzu yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-243">In hello blade for hello pool, under **Elastic databases** click **Configure pool**.</span></span>

    ![Havuzu Yapılandır'ı tıklatın][1]

2. <span data-ttu-id="bc7c7-245">Merhaba, **havuzu yapılandırma** dikey penceresinde tıklatın **toopool eklemek**.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-245">In hello **Configure pool** blade, click **Add toopool**.</span></span>

    ![Ekle toopool tıklatın](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. <span data-ttu-id="bc7c7-247">Merhaba, **eklemek veritabanları** dikey penceresinde, select hello veritabanı veya veritabanları tooadd toohello havuzu.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-247">In hello **Add databases** blade, select hello database or databases tooadd toohello pool.</span></span> <span data-ttu-id="bc7c7-248">Ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-248">Then click **Select**.</span></span>

    ![Veritabanlarını tooadd seçin](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    <span data-ttu-id="bc7c7-250">Merhaba **havuzu yapılandırma** listeleri, kendi durumu çok ayarlanmış eklenen toobe seçtiğiniz veritabanı hello artık dikey**bekleyen**.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-250">hello **Configure pool** blade now lists hello database you selected toobe added, with its status set too**Pending**.</span></span>

    ![Bekleyen havuzu ekleme](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. <span data-ttu-id="bc7c7-252">Merhaba, **yapılandırma havuzu dikey**, tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-252">In hello **Configure pool blade**, click **Save**.</span></span>

    ![Kaydet’e tıklayın.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="bc7c7-254">Bir veritabanını bir esnek havuz dışına taşıma</span><span class="sxs-lookup"><span data-stu-id="bc7c7-254">Move a database out of an elastic pool</span></span>

1. <span data-ttu-id="bc7c7-255">Merhaba, **havuzu yapılandırma** dikey penceresinde, select hello veritabanı veya veritabanları tooremove.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-255">In hello **Configure pool** blade, select hello database or databases tooremove.</span></span>

    ![veritabanları listeleme](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. <span data-ttu-id="bc7c7-257">Tıklatın **havuzundan kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-257">Click **Remove from pool**.</span></span>

    ![veritabanları listeleme](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    <span data-ttu-id="bc7c7-259">Merhaba **havuzu yapılandırma** kendi durumu çok ayarlanmış kaldırılan toobe seçtiğiniz veritabanı listeleri hello artık dikey**bekleyen**.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-259">hello **Configure pool** blade now lists hello database you selected toobe removed with its status set too**Pending**.</span></span>

    ![Önizleme veritabanı ekleme ve kaldırma](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. <span data-ttu-id="bc7c7-261">Merhaba, **yapılandırma havuzu dikey**, tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-261">In hello **Configure pool blade**, click **Save**.</span></span>

    ![Kaydet’e tıklayın.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="bc7c7-263">Bir esnek havuz performans ayarlarını değiştir</span><span class="sxs-lookup"><span data-stu-id="bc7c7-263">Change performance settings of an elastic pool</span></span>

<span data-ttu-id="bc7c7-264">Bir esnek havuz hello kaynak kullanımını izleme gibi bazı ayarlamalar gereklidir fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-264">As you monitor hello resource utilization of an elastic pool, you may discover that some adjustments are needed.</span></span> <span data-ttu-id="bc7c7-265">Belki de hello havuzu hello performansı veya depolama sınırları değişikliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-265">Maybe hello pool needs a change in hello performance or storage limits.</span></span> <span data-ttu-id="bc7c7-266">Büyük olasılıkla toochange hello veritabanı ayarlarını hello havuzunda istiyor.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-266">Possibly you want toochange hello database settings in hello pool.</span></span> <span data-ttu-id="bc7c7-267">Merhaba havuzu hiçbir zaman tooget hello iyi dengeyi performans ve maliyet konumunda hello Kurulumu değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-267">You can change hello setup of hello pool at any time tooget hello best balance of performance and cost.</span></span> <span data-ttu-id="bc7c7-268">Bkz: [ne zaman bir esnek havuz kullanılmalıdır?](sql-database-elastic-pool.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-268">See [When should an elastic pool be used?](sql-database-elastic-pool.md) for more information.</span></span>

<span data-ttu-id="bc7c7-269">toochange hello edtu'ları veya depolama havuzunu ve veritabanı başına Edtu başına sınırları:</span><span class="sxs-lookup"><span data-stu-id="bc7c7-269">toochange hello eDTUs or storage limits per pool, and eDTUs per database:</span></span>

1. <span data-ttu-id="bc7c7-270">Açık hello **havuzu yapılandırma** dikey.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-270">Open hello **Configure pool** blade.</span></span>

    <span data-ttu-id="bc7c7-271">Altında **esnek havuzu ayarlarını**, her iki kaydırıcı toochange hello havuzu ayarlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-271">Under **elastic pool settings**, use either slider toochange hello pool settings.</span></span>

    ![Esnek havuz kaynak kullanımı](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. <span data-ttu-id="bc7c7-273">Merhaba ayarını değiştirdiğinde hello görüntü hello hello değişiklik aylık maliyeti tahmini gösterir.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-273">When hello setting changes, hello display shows hello estimated monthly cost of hello change.</span></span>

    ![Bir esnek havuz ve yeni aylık maliyeti güncelleştirme](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="bc7c7-275">Esnek havuz işlemlerinin gecikme süresi</span><span class="sxs-lookup"><span data-stu-id="bc7c7-275">Latency of elastic pool operations</span></span>
* <span data-ttu-id="bc7c7-276">Veritabanı veya en büyük veritabanı başına Edtu başına Hello min Edtu'lar genellikle değiştirme 5 dakika veya daha az tamamlar.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-276">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="bc7c7-277">Merhaba Edtu havuzu başına değiştirme hello toplam hello havuzdaki tüm veritabanları tarafından kullanılan alanı miktarına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-277">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="bc7c7-278">Değişiklikler 100 GB için ortalama 90 dakika veya daha az sürer.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-278">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="bc7c7-279">Örneğin, tarafından kullanılan hello toplam alanı hello havuzdaki tüm veritabanları ise 200 GB hello havuz eDTU havuzu başına değiştirmek için gecikme süresi 3 saattir hello beklenen sonra veya daha az.</span><span class="sxs-lookup"><span data-stu-id="bc7c7-279">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc7c7-280">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bc7c7-280">Next steps</span></span>

- <span data-ttu-id="bc7c7-281">bir esnek havuz olup toounderstand [SQL Database esnek havuzunu](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="bc7c7-281">toounderstand what an elastic pool is, see [SQL Database elastic pool](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="bc7c7-282">Esnek havuzlar kullanma ile ilgili yönergeler için bkz: [esnek havuzlar için fiyat ve performans konuları](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="bc7c7-282">For guidance on using elastic pools, see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="bc7c7-283">toouse esnek iş toorun Transact-SQL betikleri hello havuzdaki veritabanları herhangi bir sayıda karşı bkz [esnek iş genel bakış](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bc7c7-283">toouse elastic jobs toorun Transact-SQL scripts against any number of databases in hello pool, see [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span>
- <span data-ttu-id="bc7c7-284">herhangi bir sayıda hello havuzdaki veritabanları arasında tooquery bkz [esnek sorgu genel bakış](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bc7c7-284">tooquery across any number of databases in hello pool, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
- <span data-ttu-id="bc7c7-285">İşlemleri için herhangi bir sayıda hello havuzdaki veritabanları Bkz [esnek işlemleri](sql-database-elastic-transactions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bc7c7-285">For transactions any number of databases in hello pool, see [Elastic transactions](sql-database-elastic-transactions-overview.md).</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-pool-manage-portal/configure-pool.png
[2]: ./media/sql-database-elastic-pool-manage-portal/basic.png
[3]: ./media/sql-database-elastic-pool-manage-portal/basic-2.png
[4]: ./media/sql-database-elastic-pool-manage-portal/basic-3.png
[5]: ./media/sql-database-elastic-pool-manage-portal/elastic-jobs.png
[6]: ./media/sql-database-elastic-pool-manage-portal/edit-metric.png
[7]: ./media/sql-database-elastic-pool-manage-portal/select-dbs.png
[8]: ./media/sql-database-elastic-pool-manage-portal/db-utilization.png
[9]: ./media/sql-database-elastic-pool-manage-portal/metric.png
