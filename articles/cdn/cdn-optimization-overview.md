---
title: "aaaOptimize senaryonuz için Azure içerik teslim"
description: "Nasıl toooptimize teslim içeriğinizin belirli senaryoları için"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: 922a92fdbf7e6e21f2b5ae9a2fb4ac32735fc15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-azure-content-delivery-for-your-scenario"></a><span data-ttu-id="69e81-103">Azure içerik teslim senaryonuz için en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="69e81-103">Optimize Azure content delivery for your scenario</span></span>

<span data-ttu-id="69e81-104">İçerik tooa geniş global kullanıcılara iletirken, içeriğinizin kritik tooensure en iyi duruma getirilmiş hello teslimat olur.</span><span class="sxs-lookup"><span data-stu-id="69e81-104">When you deliver content tooa large global audience, it's critical tooensure hello optimized delivery of your content.</span></span> <span data-ttu-id="69e81-105">Hello Azure içerik teslim ağı hello teslim deneyimi hello sahip olduğunuz içerik türüne göre en iyi duruma getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69e81-105">hello Azure Content Delivery Network can optimize hello delivery experience based on hello type of content you have.</span></span> <span data-ttu-id="69e81-106">Bir Web sitesi, bir canlı akış, bir video veya büyük bir dosya yüklemek için içerik olabilir.</span><span class="sxs-lookup"><span data-stu-id="69e81-106">Content can be a website, a live stream, a video, or a large file for download.</span></span> <span data-ttu-id="69e81-107">Bir içerik teslim ağı (CDN) uç noktası oluşturduğunuzda, bir senaryo hello belirttiğiniz **için en iyi duruma getirilmiş** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="69e81-107">When you create a content delivery network (CDN) endpoint, you specify a scenario in hello **Optimized for** option.</span></span> <span data-ttu-id="69e81-108">Tercih ettiğiniz hangi iyileştirme uygulanan toohello içerik hello CDN uç noktasından teslim belirler.</span><span class="sxs-lookup"><span data-stu-id="69e81-108">Your choice determines which optimization is applied toohello content delivered from hello CDN endpoint.</span></span>

<span data-ttu-id="69e81-109">Tasarlanmış toouse en iyi yöntem davranışları tooimprove içerik teslim performansı en iyi duruma getirme seçimlerdir ve daha iyi kaynak boşaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69e81-109">Optimization choices are designed toouse best-practice behaviors tooimprove content delivery performance and better origin offload.</span></span> <span data-ttu-id="69e81-110">Senaryo seçimlerinizi kısmi önbelleğe alma, nesne Öbekleme ve hello Kaynak başarısızlığı yeniden deneme ilkesi için yapılandırmaları değiştirerek performansını etkiler.</span><span class="sxs-lookup"><span data-stu-id="69e81-110">Your scenario choices affect performance by modifying configurations for partial caching, object chunking, and hello origin failure retry policy.</span></span> 

<span data-ttu-id="69e81-111">Bu makale, çeşitli en iyi duruma getirme özellikleri ve ne zaman kullanmanız gerektiğine genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="69e81-111">This article provides an overview of various optimization features and when you should use them.</span></span> <span data-ttu-id="69e81-112">Özellikleri ve sınırlamaları hakkında daha fazla bilgi için her tek tek en iyi duruma getirme türü hello ilgili makalelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="69e81-112">For more information on features and limitations, see hello respective articles on each individual optimization type.</span></span>

> [!NOTE]
> <span data-ttu-id="69e81-113">**İçin en iyi duruma getirilmiş** seçenekleri seçtiğiniz hello sağlayıcısı göre değişir.</span><span class="sxs-lookup"><span data-stu-id="69e81-113">Your **Optimized for** options can vary based on hello provider you select.</span></span> <span data-ttu-id="69e81-114">CDN sağlayıcıları geliştirme hello senaryo bağlı olarak, farklı şekillerde uygulayın.</span><span class="sxs-lookup"><span data-stu-id="69e81-114">CDN providers apply enhancement in different ways, depending on hello scenario.</span></span> 

## <a name="provider-options"></a><span data-ttu-id="69e81-115">Sağlayıcı seçenekleri</span><span class="sxs-lookup"><span data-stu-id="69e81-115">Provider options</span></span>

<span data-ttu-id="69e81-116">Merhaba akamai'den Azure içerik teslim ağı destekler:</span><span class="sxs-lookup"><span data-stu-id="69e81-116">hello Azure Content Delivery Network from Akamai supports:</span></span>

* <span data-ttu-id="69e81-117">Genel web teslim</span><span class="sxs-lookup"><span data-stu-id="69e81-117">General web delivery</span></span> 

* <span data-ttu-id="69e81-118">Genel medya</span><span class="sxs-lookup"><span data-stu-id="69e81-118">General media streaming</span></span>

* <span data-ttu-id="69e81-119">İsteğe bağlı video medya</span><span class="sxs-lookup"><span data-stu-id="69e81-119">Video-on-demand media streaming</span></span>

* <span data-ttu-id="69e81-120">Büyük dosya indirme</span><span class="sxs-lookup"><span data-stu-id="69e81-120">Large file download</span></span>

* <span data-ttu-id="69e81-121">Dinamik site hızlandırma</span><span class="sxs-lookup"><span data-stu-id="69e81-121">Dynamic site acceleration</span></span> 

<span data-ttu-id="69e81-122">Merhaba verizon'dan Azure içerik teslim ağı yalnızca genel web teslim destekler.</span><span class="sxs-lookup"><span data-stu-id="69e81-122">hello Azure Content Delivery Network from Verizon supports general web delivery only.</span></span> <span data-ttu-id="69e81-123">Video isteğe bağlı ve büyük dosya indirme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="69e81-123">It can be used for video on demand and large file download.</span></span> <span data-ttu-id="69e81-124">Bir en iyi duruma getirme türü tooselect yok.</span><span class="sxs-lookup"><span data-stu-id="69e81-124">You don't have tooselect an optimization type.</span></span>

<span data-ttu-id="69e81-125">Farklı sağlayıcı tooselect Merhaba, teslimat için en iyi sağlayıcısı arasındaki performans Çeşitlemeler test öneririz.</span><span class="sxs-lookup"><span data-stu-id="69e81-125">We highly recommend that you test performance variations between different providers tooselect hello optimal provider for your delivery.</span></span>

## <a name="select-and-configure-optimization-types"></a><span data-ttu-id="69e81-126">Seçin ve en iyi duruma getirme türlerini yapılandır</span><span class="sxs-lookup"><span data-stu-id="69e81-126">Select and configure optimization types</span></span>

<span data-ttu-id="69e81-127">Yeni bir uç noktası toocreate hello senaryo en iyi şekilde eşleşen bir en iyi duruma getirme türü ve uç nokta toodeliver hello istediğiniz içerik türü seçin.</span><span class="sxs-lookup"><span data-stu-id="69e81-127">toocreate a new endpoint, select an optimization type that best matches hello scenario and type of content that you want hello endpoint toodeliver.</span></span> <span data-ttu-id="69e81-128">**Genel web teslim** hello varsayılan seçimdir.</span><span class="sxs-lookup"><span data-stu-id="69e81-128">**General web delivery** is hello default selection.</span></span> <span data-ttu-id="69e81-129">Herhangi bir zamanda herhangi bir varolan Akamai uç nokta için hello en iyi duruma getirme seçeneği güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69e81-129">You can update hello optimization option for any existing Akamai endpoint at any time.</span></span> <span data-ttu-id="69e81-130">Bu değişiklik hello CDN teslimat kesme değil.</span><span class="sxs-lookup"><span data-stu-id="69e81-130">This change doesn't interrupt delivery from hello CDN.</span></span> 

1. <span data-ttu-id="69e81-131">Standart Akamai profilindeki bir uç nokta seçin.</span><span class="sxs-lookup"><span data-stu-id="69e81-131">Select an endpoint within a Standard Akamai profile.</span></span>

    ![<span data-ttu-id="69e81-132">Uç nokta seçimi</span><span class="sxs-lookup"><span data-stu-id="69e81-132">Endpoint selection</span></span> ](./media/cdn-optimization-overview/01_Akamai.png)

2. <span data-ttu-id="69e81-133">Altında **ayarları**seçin **en iyi duruma getirme**.</span><span class="sxs-lookup"><span data-stu-id="69e81-133">Under **SETTINGS**, select **Optimization**.</span></span> <span data-ttu-id="69e81-134">Merhaba sonra bir türü seçin **için en iyi duruma getirilmiş** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="69e81-134">Then select a type from hello **Optimized for** drop-down list.</span></span>

    ![En iyi duruma getirme ve türü seçimi](./media/cdn-optimization-overview/02_Select.png)

## <a name="optimization-for-specific-scenarios"></a><span data-ttu-id="69e81-136">Belirli senaryolar için en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="69e81-136">Optimization for specific scenarios</span></span>

<span data-ttu-id="69e81-137">Merhaba CDN uç senaryoları aşağıdaki hello biri için en iyi duruma getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69e81-137">You can optimize hello CDN endpoint for one of hello following scenarios.</span></span> 

### <a name="general-web-delivery"></a><span data-ttu-id="69e81-138">Genel web teslim</span><span class="sxs-lookup"><span data-stu-id="69e81-138">General web delivery</span></span>

<span data-ttu-id="69e81-139">Genel web teslim hello en yaygın iyileştirme seçenektir.</span><span class="sxs-lookup"><span data-stu-id="69e81-139">General web delivery is hello most common optimization option.</span></span> <span data-ttu-id="69e81-140">Web sayfaları ve web uygulamaları gibi genel web içerik iyileştirme için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="69e81-140">It's designed for general web content optimization, such as webpages and web applications.</span></span> <span data-ttu-id="69e81-141">Bu iyileştirme dosyası için de kullanılabilir ve video indirir.</span><span class="sxs-lookup"><span data-stu-id="69e81-141">This optimization also can be used for file and video downloads.</span></span>

<span data-ttu-id="69e81-142">Tipik bir Web sitesi dinamik ve statik içeriği içerir.</span><span class="sxs-lookup"><span data-stu-id="69e81-142">A typical website contains static and dynamic content.</span></span> <span data-ttu-id="69e81-143">Statik içerik görüntüleri, JavaScript kitaplıklarını ve önbelleğe alınmış ve toodifferent kullanıcılar teslim stil sayfaları içerir.</span><span class="sxs-lookup"><span data-stu-id="69e81-143">Static content includes images, JavaScript libraries, and style sheets that can be cached and delivered toodifferent users.</span></span> <span data-ttu-id="69e81-144">Haber öğeleri tooa kullanıcı profili uyarlanmış gibi dinamik içerik bireysel bir kullanıcı için kişiselleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="69e81-144">Dynamic content is personalized for an individual user, such as news items that are tailored tooa user profile.</span></span> <span data-ttu-id="69e81-145">Alışveriş sepeti içeriği gibi benzersiz tooeach kullanıcı olduğundan dinamik içerik önbelleğe değil.</span><span class="sxs-lookup"><span data-stu-id="69e81-145">Dynamic content isn't cached because it's unique tooeach user, such as shopping cart contents.</span></span> <span data-ttu-id="69e81-146">Genel web teslim, Web sitenizin tamamını en iyi duruma getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69e81-146">General web delivery can optimize your entire website.</span></span> 

> [!NOTE]
> <span data-ttu-id="69e81-147">Merhaba akamai'den Azure içerik teslim ağı kullanırsanız, bu en iyi duruma getirme, ortalama dosya boyutu 10 MB'den küçük ise toouse isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69e81-147">If you use hello Azure Content Delivery Network from Akamai, you might want toouse this optimization if your average file size is smaller than 10 MB.</span></span> <span data-ttu-id="69e81-148">Ortalama dosya boyutu 10 MB'den büyük ise, seçin **büyük dosya indirme** hello gelen **için en iyi duruma getirilmiş** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="69e81-148">If your average file size is larger than 10 MB, select **Large file download** from hello **Optimized for** drop-down list.</span></span>

### <a name="general-media-streaming"></a><span data-ttu-id="69e81-149">Genel medya</span><span class="sxs-lookup"><span data-stu-id="69e81-149">General media streaming</span></span>

<span data-ttu-id="69e81-150">Canlı akış ve isteğe bağlı video akış için toouse hello uç noktası gerekiyorsa, en iyi duruma getirme Genel medya öneririz.</span><span class="sxs-lookup"><span data-stu-id="69e81-150">If you need toouse hello endpoint for live streaming and video-on-demand streaming, we recommend general media streaming optimization.</span></span>

<span data-ttu-id="69e81-151">Geç hello istemcide gelmesini paketleri sık video içeriği arabelleğe alma gibi ek olarak, düzeyi düşürülmüş görüntüleme deneyimini neden olabileceğinden Media akışı hassas, saattir.</span><span class="sxs-lookup"><span data-stu-id="69e81-151">Media streaming is time sensitive, because packets that arrive late on hello client can cause a degraded viewing experience, such as frequent buffering of video content.</span></span> <span data-ttu-id="69e81-152">En iyi duruma getirme medya medya içerik teslimat hello gecikmesini azaltır ve kullanıcılar için kesintisiz bir akış deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="69e81-152">Media streaming optimization reduces hello latency of media content delivery and provides a smooth streaming experience for users.</span></span> 

<span data-ttu-id="69e81-153">Bu senaryo, Azure medya hizmeti müşteriler için yaygın bir durumdur.</span><span class="sxs-lookup"><span data-stu-id="69e81-153">This scenario is common for Azure media service customers.</span></span> <span data-ttu-id="69e81-154">Azure media Services'i kullanırken, canlı ve isteğe bağlı akış için kullanılan bir akış uç noktasını alın.</span><span class="sxs-lookup"><span data-stu-id="69e81-154">When you use Azure media services, you get one streaming endpoint that can be used for both live and on-demand streaming.</span></span> <span data-ttu-id="69e81-155">Canlı tooon isteğe bağlı Akış değiştirdiğinizde, bu senaryo ile tooswitch tooanother endpoint müşteriler gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="69e81-155">With this scenario, customers don't need tooswitch tooanother endpoint when they change from live tooon-demand streaming.</span></span> <span data-ttu-id="69e81-156">Genel ortam akış en iyi duruma getirme, bu tür senaryosu destekler.</span><span class="sxs-lookup"><span data-stu-id="69e81-156">General media streaming optimization supports this type of scenario.</span></span>

<span data-ttu-id="69e81-157">Merhaba verizon'dan Azure içerik teslim ağı hello genel web teslim en iyi duruma getirme türü toodeliver akış medya içeriği kullanır.</span><span class="sxs-lookup"><span data-stu-id="69e81-157">hello Azure Content Delivery Network from Verizon uses hello general web delivery optimization type toodeliver streaming media content.</span></span>

<span data-ttu-id="69e81-158">toolearn daha iyileştirme, akış medya hakkında bkz [en iyi duruma getirme medya](cdn-media-streaming-optimization.md).</span><span class="sxs-lookup"><span data-stu-id="69e81-158">toolearn more about media streaming optimization, see [Media streaming optimization](cdn-media-streaming-optimization.md).</span></span>

### <a name="video-on-demand-media-streaming"></a><span data-ttu-id="69e81-159">İsteğe bağlı video medya</span><span class="sxs-lookup"><span data-stu-id="69e81-159">Video-on-demand media streaming</span></span>

<span data-ttu-id="69e81-160">İsteğe bağlı video medya akış iyileştirme isteğe bağlı video akış içeriği artırır.</span><span class="sxs-lookup"><span data-stu-id="69e81-160">Video-on-demand media streaming optimization improves video-on-demand streaming content.</span></span> <span data-ttu-id="69e81-161">İsteğe bağlı video akış için bir uç nokta kullanırsanız, bu seçenek toouse isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69e81-161">If you use an endpoint for video-on-demand streaming, you might want toouse this option.</span></span>

<span data-ttu-id="69e81-162">Merhaba verizon'dan Azure içerik teslim ağı hello genel web teslim en iyi duruma getirme türü toodeliver akış medya içeriği kullanır.</span><span class="sxs-lookup"><span data-stu-id="69e81-162">hello Azure Content Delivery Network from Verizon uses hello general web delivery optimization type toodeliver streaming media content.</span></span>

<span data-ttu-id="69e81-163">toolearn daha iyileştirme, akış medya hakkında bkz [en iyi duruma getirme medya](cdn-media-streaming-optimization.md).</span><span class="sxs-lookup"><span data-stu-id="69e81-163">toolearn more about media streaming optimization, see [Media streaming optimization](cdn-media-streaming-optimization.md).</span></span>

> [!NOTE]
> <span data-ttu-id="69e81-164">Merhaba endpoint isteğe bağlı video içeriği öncelikle hizmet veriyorsa, bu en iyi duruma getirme türünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="69e81-164">If hello endpoint primarily serves video-on-demand content, use this optimization type.</span></span> <span data-ttu-id="69e81-165">Bu en iyi duruma getirme ve hello genel medya akış iyileştirme arasındaki temel farklardan Hello hello bağlantı yeniden deneme zaman aşımı ' dir. Merhaba zaman aşımı çok kısa toowork canlı akış senaryolarında ' dir.</span><span class="sxs-lookup"><span data-stu-id="69e81-165">hello major difference between this optimization and hello general media streaming optimization is hello connection retry time-out. hello time-out is much shorter toowork with live streaming scenarios.</span></span>

### <a name="large-file-download"></a><span data-ttu-id="69e81-166">Büyük dosya indirme</span><span class="sxs-lookup"><span data-stu-id="69e81-166">Large file download</span></span>

<span data-ttu-id="69e81-167">Merhaba akamai'den Azure içerik teslim ağı kullanırsanız, büyük dosya indirme toodeliver dosyaları 1,8 GB'den büyük kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="69e81-167">If you use hello Azure Content Delivery Network from Akamai, you must use large file download toodeliver files larger than 1.8 GB.</span></span> <span data-ttu-id="69e81-168">Merhaba verizon'dan Azure içerik teslim ağı dosya indirme boyutu, genel web teslim iyileştirmeden bir sınırlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="69e81-168">hello Azure Content Delivery Network from Verizon doesn't have a limitation on file download size in its general web delivery optimization.</span></span>

<span data-ttu-id="69e81-169">Merhaba akamai'den Azure içerik teslim ağı kullanırsanız, büyük dosya yüklemeleri 10 MB'den büyük içerik için en iyi duruma getirilir.</span><span class="sxs-lookup"><span data-stu-id="69e81-169">If you use hello Azure Content Delivery Network from Akamai, large file downloads are optimized for content larger than 10 MB.</span></span> <span data-ttu-id="69e81-170">Ortalama dosya boyutu 10 MB'den daha küçükse, toouse genel web teslim isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69e81-170">If your average file size is smaller than 10 MB, you might want toouse general web delivery.</span></span> <span data-ttu-id="69e81-171">Ortalama dosya boyutu 10 MB'den büyük tutarlı bir şekilde daha verimli toocreate büyük dosyalar için ayrı bir uç noktası geçersiz olabilir.</span><span class="sxs-lookup"><span data-stu-id="69e81-171">If your average files sizes are consistently larger than 10 MB, it might be more efficient toocreate a separate endpoint for large files.</span></span> <span data-ttu-id="69e81-172">Örneğin, bellenim ve yazılım güncelleştirmeleri genellikle büyük dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="69e81-172">For example, firmware or software updates typically are large files.</span></span>

<span data-ttu-id="69e81-173">Merhaba verizon'dan Azure içerik teslim ağı hello genel web teslim en iyi duruma getirme türü toodeliver akış medya içeriği kullanır.</span><span class="sxs-lookup"><span data-stu-id="69e81-173">hello Azure Content Delivery Network from Verizon uses hello general web delivery optimization type toodeliver streaming media content.</span></span>

<span data-ttu-id="69e81-174">toolearn büyük dosya iyileştirme hakkında daha fazla bilgi görmek [büyük dosya iyileştirme](cdn-large-file-optimization.md).</span><span class="sxs-lookup"><span data-stu-id="69e81-174">toolearn more about large file optimization, see [Large file optimization](cdn-large-file-optimization.md).</span></span>

### <a name="dynamic-site-acceleration"></a><span data-ttu-id="69e81-175">Dinamik site hızlandırma</span><span class="sxs-lookup"><span data-stu-id="69e81-175">Dynamic site acceleration</span></span>

 <span data-ttu-id="69e81-176">Dinamik site hızlandırma Akamai ve Verizon içerik teslim ağı profillerden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="69e81-176">Dynamic site acceleration is available from both Akamai and Verizon Content Delivery Network profiles.</span></span> <span data-ttu-id="69e81-177">Bu iyileştirme bir ek ücret toouse içerir.</span><span class="sxs-lookup"><span data-stu-id="69e81-177">This optimization involves an additional fee toouse.</span></span> <span data-ttu-id="69e81-178">Daha fazla bilgi için fiyatlandırma sayfası hello bakın.</span><span class="sxs-lookup"><span data-stu-id="69e81-178">For more information, see hello pricing page.</span></span>

<span data-ttu-id="69e81-179">Dinamik site hızlandırma hello gecikme süresi ve dinamik içerik performansını çeşitli teknikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="69e81-179">Dynamic site acceleration includes various techniques that benefit hello latency and performance of dynamic content.</span></span> <span data-ttu-id="69e81-180">Teknikler rota ve ağ iyileştirme, TCP en iyi duruma getirme ve daha fazlasını içerir.</span><span class="sxs-lookup"><span data-stu-id="69e81-180">Techniques include route and network optimization, TCP optimization, and more.</span></span> 

<span data-ttu-id="69e81-181">Bu en iyi duruma getirme tooaccelerate alınabilir bulunmayan çok sayıda yanıtları içeren bir web uygulamasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69e81-181">You can use this optimization tooaccelerate a web app that includes numerous responses that aren't cacheable.</span></span> <span data-ttu-id="69e81-182">Arama sonuçları, teslim alma işlemleri veya gerçek zamanlı verileri örnektir.</span><span class="sxs-lookup"><span data-stu-id="69e81-182">Examples are search results, checkout transactions, or real-time data.</span></span> <span data-ttu-id="69e81-183">Toouse çekirdek CDN statik verileri önbelleğe alma özelliklerini devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69e81-183">You can continue toouse core CDN caching capabilities for static data.</span></span> 



