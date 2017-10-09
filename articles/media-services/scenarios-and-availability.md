---
title: "Azure Media Services aaaMicrosoft senaryolar ve veri merkezleri arasında özelliklerin kullanılabilirliği | Microsoft Docs"
description: "Bu konu başlığı altında, Microsoft Azure Media Services senaryolarına ve özelliklerle hizmetlerin veri merkezleri arasında kullanılabilirliğine genel bir bakış sağlanır."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 3dbab6998ed5da738baf8f1e2fb096dfba336e19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-and-availability-of-media-services-features-across-datacenters"></a><span data-ttu-id="db899-103">Senaryolar ve Media Services özelliklerinin veri merkezleri arasında kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="db899-103">Scenarios and availability of Media Services features across datacenters</span></span>

<span data-ttu-id="db899-104">Microsoft Azure Media Services (AMS) toosecurely karşıya yükleme sağlar, depolama, kodlamak ve hem isteğe bağlı ve canlı akış teslimi toovarious istemcileri için (örneğin, TV, PC ve mobil aygıtlar) video ve ses içeriklerini paketini.</span><span class="sxs-lookup"><span data-stu-id="db899-104">Microsoft Azure Media Services (AMS) enables you toosecurely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery toovarious clients (for example, TV, PC, and mobile devices).</span></span>

<span data-ttu-id="db899-105">Birden çok veri merkezlerinde Merhaba Dünya AMS çalışır.</span><span class="sxs-lookup"><span data-stu-id="db899-105">AMS operates in multiple data centers around hello world.</span></span> <span data-ttu-id="db899-106">Bu veri merkezlerinde nereye koyacağınızı seçmek esneklik vermiş toogeographic bölgelerdeki gruplandırılır toobuild uygulamalarınızı.</span><span class="sxs-lookup"><span data-stu-id="db899-106">These data centers are grouped in toogeographic regions, giving you flexibility in choosing where toobuild your applications.</span></span> <span data-ttu-id="db899-107">Merhaba gözden geçirebilirsiniz [bölgeler ve konumlarını listesi](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="db899-107">You can review hello [list of regions and their locations](https://azure.microsoft.com/regions/).</span></span> 

<span data-ttu-id="db899-108">Bu konu başlığı altında, içeriğinizin [canlı](#live_scenarios) veya [isteğe bağlı](#vod_scenarios) teslimiyle ilgili yaygın senaryolar gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="db899-108">This topic shows common scenarios for delivering your content [live](#live_scenarios) or [on-demand](#vod_scenarios).</span></span> <span data-ttu-id="db899-109">Merhaba konu aynı zamanda veri merkezleri arasında ortam özellikleri ve hizmetlerin kullanılabilirliğini hakkında ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="db899-109">hello topic also provides details about availability of media features and services across data centers.</span></span>

## <a name="overview"></a><span data-ttu-id="db899-110">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="db899-110">Overview</span></span>

### <a name="prerequisites"></a><span data-ttu-id="db899-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="db899-111">Prerequisites</span></span>

<span data-ttu-id="db899-112">Azure Media Services'i kullanarak toostart hello şunlara sahip olmanız:</span><span class="sxs-lookup"><span data-stu-id="db899-112">toostart using Azure Media Services, you should have hello following:</span></span>

* <span data-ttu-id="db899-113">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="db899-113">An Azure account.</span></span> <span data-ttu-id="db899-114">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db899-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="db899-115">Ayrıntılar için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="db899-115">For details, see [Azure Free Trial](https://azure.microsoft.com).</span></span>
* <span data-ttu-id="db899-116">Bir Azure Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="db899-116">An Azure Media Services account.</span></span> <span data-ttu-id="db899-117">Daha fazla bilgi için bkz. [Hesap Oluşturma](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="db899-117">For more information, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="db899-118">Akış uç noktası toostream içerik istediğiniz hello sahip toobe hello **çalıştıran** durumu.</span><span class="sxs-lookup"><span data-stu-id="db899-118">hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

    <span data-ttu-id="db899-119">AMS hesabınızı oluştururken bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu.</span><span class="sxs-lookup"><span data-stu-id="db899-119">When your AMS account is created, a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="db899-120">İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme, akış uç noktası hello akış toostart sahip toobe hello **çalıştıran** durumu.</span><span class="sxs-lookup"><span data-stu-id="db899-120">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint has toobe in hello **Running** state.</span></span>

### <a name="commonly-used-objects-when-developing-against-hello-ams-odata-model"></a><span data-ttu-id="db899-121">AMS OData modeli hello karşı geliştirirken yaygın olarak kullanılan nesneleri</span><span class="sxs-lookup"><span data-stu-id="db899-121">Commonly used objects when developing against hello AMS OData model</span></span>

<span data-ttu-id="db899-122">Merhaba aşağıdaki görüntüde bazılarını hello en yaygın olarak kullanılan nesneler hello Media Services OData modeline göre geliştirirken gösterir.</span><span class="sxs-lookup"><span data-stu-id="db899-122">hello following image shows some of hello most commonly used objects when developing against hello Media Services OData model.</span></span>

<span data-ttu-id="db899-123">Merhaba görüntü tooview boyutu tam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="db899-123">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-overview/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-overview/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="db899-124">Merhaba tüm model görüntüleyebilirsiniz [burada](https://media.windows.net/API/$metadata?api-version=2.15).</span><span class="sxs-lookup"><span data-stu-id="db899-124">You can view hello whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="protect-content-in-storage-and-deliver-streaming-media-in-hello-clear-non-encrypted"></a><span data-ttu-id="db899-125">Depolama alanında içeriği koruma ve (şifrelenmemiş) teslim akan medyayı hello temizleyin</span><span class="sxs-lookup"><span data-stu-id="db899-125">Protect content in storage and deliver streaming media in hello clear (non-encrypted)</span></span>

![VoD iş akışı](./media/scenarios-and-availability/scenarios-and-availability01.png)

1. <span data-ttu-id="db899-127">Yüksek kaliteli bir medya dosyasını bir varlığa yükleyin.</span><span class="sxs-lookup"><span data-stu-id="db899-127">Upload a high-quality media file into an asset.</span></span>

    <span data-ttu-id="db899-128">İçeriğinizi sırasında karşıya yükleme ve deposunda kalan while sipariş tooprotect tooapply depolama şifreleme seçeneği tooyour varlığı önerilir.</span><span class="sxs-lookup"><span data-stu-id="db899-128">It is recommended tooapply storage encryption option tooyour asset in order tooprotect your content during upload and while at rest in storage.</span></span>
2. <span data-ttu-id="db899-129">Bit hızı Uyarlamalı MP4 dosyaları tooa kodlayın.</span><span class="sxs-lookup"><span data-stu-id="db899-129">Encode tooa set of adaptive bitrate MP4 files.</span></span>

    <span data-ttu-id="db899-130">İçeriğinizi beklerken sipariş tooprotect varlığı tooapply depolama şifreleme seçeneği toohello çıkış önerilir.</span><span class="sxs-lookup"><span data-stu-id="db899-130">It is recommended tooapply storage encryption option toohello output asset in order tooprotect your content at rest.</span></span>
3. <span data-ttu-id="db899-131">Varlık teslim ilkesini (dinamik paketleme tarafından kullanılır) yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="db899-131">Configure asset delivery policy (used by dynamic packaging).</span></span>

    <span data-ttu-id="db899-132">Varlığınıza depolama şifrelemesi uygulanmışsa varlık teslim ilkesini yapılandırmanız **gerekir**.</span><span class="sxs-lookup"><span data-stu-id="db899-132">If your asset is storage encrypted, you **must** configure asset delivery policy.</span></span>
4. <span data-ttu-id="db899-133">Bir OnDemand Bulucu oluşturarak Hello varlığı yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="db899-133">Publish hello asset by creating an OnDemand locator.</span></span>
5. <span data-ttu-id="db899-134">Yayımlanan içeriği akışla aktarın.</span><span class="sxs-lookup"><span data-stu-id="db899-134">Stream published content.</span></span>

<span data-ttu-id="db899-135">Merhaba veri merkezlerinde kullanılabilirliği hakkında daha fazla bilgi için bkz [kullanılabilirlik](#availability) bölümü.</span><span class="sxs-lookup"><span data-stu-id="db899-135">For information about availability in datacenters, see hello [Availability](#availability) section.</span></span>

## <a name="protect-content-in-storage-deliver-dynamically-encrypted-streaming-media"></a><span data-ttu-id="db899-136">Depolama alanında içeriği koruma, dinamik olarak şifrelenmiş akan medya teslim etme</span><span class="sxs-lookup"><span data-stu-id="db899-136">Protect content in storage, deliver dynamically encrypted streaming media</span></span>

![PlayReady ile koruma](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

1. <span data-ttu-id="db899-138">Yüksek kaliteli bir medya dosyasını bir varlığa yükleyin.</span><span class="sxs-lookup"><span data-stu-id="db899-138">Upload a high-quality media file into an asset.</span></span> <span data-ttu-id="db899-139">Depolama şifrelemesi seçeneğini toohello varlık uygulayın.</span><span class="sxs-lookup"><span data-stu-id="db899-139">Apply storage encryption option toohello asset.</span></span>
2. <span data-ttu-id="db899-140">Bit hızı Uyarlamalı MP4 dosyaları tooa kodlayın.</span><span class="sxs-lookup"><span data-stu-id="db899-140">Encode tooa set of adaptive bitrate MP4 files.</span></span> <span data-ttu-id="db899-141">Depolama şifrelemesi seçeneğini toohello çıkış varlığına uygulayın.</span><span class="sxs-lookup"><span data-stu-id="db899-141">Apply storage encryption option toohello output asset.</span></span>
3. <span data-ttu-id="db899-142">Kayıttan yürütme sırasında dinamik olarak şifrelenmiş toobe istediğiniz hello varlık için şifreleme içerik anahtarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="db899-142">Create encryption content key for hello asset you want toobe dynamically encrypted during playback.</span></span>
4. <span data-ttu-id="db899-143">İçerik anahtarı yetkilendirme ilkesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="db899-143">Configure content key authorization policy.</span></span>
5. <span data-ttu-id="db899-144">Varlık teslim ilkesini (dinamik paketleme ve dinamik şifreleme tarafından kullanılır) yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="db899-144">Configure asset delivery policy (used by dynamic packaging and dynamic encryption).</span></span>
6. <span data-ttu-id="db899-145">Bir OnDemand Bulucu oluşturarak Hello varlığı yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="db899-145">Publish hello asset by creating an OnDemand locator.</span></span>
7. <span data-ttu-id="db899-146">Yayımlanan içeriği akışla aktarın.</span><span class="sxs-lookup"><span data-stu-id="db899-146">Stream published content.</span></span>

<span data-ttu-id="db899-147">Merhaba veri merkezlerinde kullanılabilirliği hakkında daha fazla bilgi için bkz [kullanılabilirlik](#availability) bölümü.</span><span class="sxs-lookup"><span data-stu-id="db899-147">For information about availability in datacenters, see hello [Availability](#availability) section.</span></span>

## <a name="use-media-analytics-tooderive-actionable-insights-from-your-videos"></a><span data-ttu-id="db899-148">Medya analizi tooderive eyleme dönüştürülebilir Öngörüler videolarınızı gelen kullanın</span><span class="sxs-lookup"><span data-stu-id="db899-148">Use Media Analytics tooderive actionable insights from your videos</span></span>

<span data-ttu-id="db899-149">Medya analizi, kuruluş ve işletmelerin tooderive eyleme dönüştürülebilir Öngörüler kendi video dosyalarından kolaylaştırmak için konuşma ve görme bileşenleri koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="db899-149">Media Analytics is a collection of speech and vision components that make it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="db899-150">Daha fazla bilgi için bkz. [Azure Media Services Analizi’ne Genel Bakış](media-services-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="db899-150">For more information, see [Azure Media Services Analytics Overview](media-services-analytics-overview.md).</span></span>

1. <span data-ttu-id="db899-151">Yüksek kaliteli bir medya dosyasını bir varlığa yükleyin.</span><span class="sxs-lookup"><span data-stu-id="db899-151">Upload a high-quality media file into an asset.</span></span>
2. <span data-ttu-id="db899-152">İle hello açıklanan hello medya analizi hizmetlerinden birini kullanarak videolarınızı işleyin [medya analizi genel bakış](media-services-analytics-overview.md) bölümü.</span><span class="sxs-lookup"><span data-stu-id="db899-152">Process your videos with one of hello Media Analytics services described in hello [Media Analytics overview](media-services-analytics-overview.md) section.</span></span>
3. <span data-ttu-id="db899-153">Medya Analizi medya işlemcileri MP4 veya JSON dosyaları üretir.</span><span class="sxs-lookup"><span data-stu-id="db899-153">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="db899-154">Medya işlemcisi bir MP4 dosyası oluşturduysa hello dosyayı aşamalı olarak indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db899-154">If a media processor produced an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="db899-155">Medya işlemcisi bir JSON dosyası oluşturduysa hello Azure blob depolama hello dosyayı indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db899-155">If a media processor produced a JSON file, you can download hello file from hello Azure blob storage.</span></span>

<span data-ttu-id="db899-156">Merhaba veri merkezlerinde kullanılabilirliği hakkında daha fazla bilgi için bkz [kullanılabilirlik](#availability) bölümü.</span><span class="sxs-lookup"><span data-stu-id="db899-156">For information about availability in datacenters, see hello [Availability](#availability) section.</span></span>

## <a name="deliver-progressive-download"></a><span data-ttu-id="db899-157">Aşamalı indirme teslimi</span><span class="sxs-lookup"><span data-stu-id="db899-157">Deliver progressive download</span></span>

1. <span data-ttu-id="db899-158">Yüksek kaliteli bir medya dosyasını bir varlığa yükleyin.</span><span class="sxs-lookup"><span data-stu-id="db899-158">Upload a high-quality media file into an asset.</span></span>
2. <span data-ttu-id="db899-159">Tooa tek MP4 dosyasına kodlayın.</span><span class="sxs-lookup"><span data-stu-id="db899-159">Encode tooa single MP4 file.</span></span>
3. <span data-ttu-id="db899-160">Bir OnDemand veya SAS Bulucu oluşturarak Hello varlığı yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="db899-160">Publish hello asset by creating an OnDemand or SAS locator.</span></span>

    <span data-ttu-id="db899-161">SAS Bulucu kullanıyorsanız hello içerik hello Azure blob depolama indirilir.</span><span class="sxs-lookup"><span data-stu-id="db899-161">If using SAS locator, hello content is downloaded from hello Azure blob storage.</span></span> <span data-ttu-id="db899-162">Bu durumda, akış uç noktaları başlatılmış durumda toohave gerekmez.</span><span class="sxs-lookup"><span data-stu-id="db899-162">In this case, you do not need toohave streaming endpoints in started state.</span></span>
4. <span data-ttu-id="db899-163">Aşamalı olarak içerik indirin.</span><span class="sxs-lookup"><span data-stu-id="db899-163">Progressively download content.</span></span>

## <span data-ttu-id="db899-164"><a id="live_scenarios"></a>Canlı akış olayları teslimi</span><span class="sxs-lookup"><span data-stu-id="db899-164"><a id="live_scenarios"></a>Delivering live-streaming events</span></span> 

1. <span data-ttu-id="db899-165">Çeşitli canlı akış protokollerini (RTMP veya Kesintisiz Akış gibi) kullanarak canlı içerik alın.</span><span class="sxs-lookup"><span data-stu-id="db899-165">Ingest live content using various live streaming protocols (for example RTMP or Smooth Streaming).</span></span>
2. <span data-ttu-id="db899-166">(isteğe bağlı) Akışınızı, bit hızı uyarlamalı akışa kodlayın.</span><span class="sxs-lookup"><span data-stu-id="db899-166">(optionally) Encode your stream into adaptive bitrate stream.</span></span>
3. <span data-ttu-id="db899-167">Canlı akışınızın önizlemesini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="db899-167">Preview your live stream.</span></span>
4. <span data-ttu-id="db899-168">Merhaba içeriği yaygın akış protokolleri (örneğin, MPEG DASH, kesintisiz, HLS) aracılığıyla teslim tooyour müşteriler doğrudan ya da daha fazla dağıtım tooa içerik teslim ağı (CDN).</span><span class="sxs-lookup"><span data-stu-id="db899-168">Deliver hello content through common streaming protocols (for example, MPEG DASH, Smooth, HLS) directly tooyour customers, or tooa Content Delivery Network (CDN) for further distribution.</span></span>

    <span data-ttu-id="db899-169">-veya-</span><span class="sxs-lookup"><span data-stu-id="db899-169">-or-</span></span>

    <span data-ttu-id="db899-170">Sipariş toobe kaydı ve deposu hello alınan içeriği daha sonra (isteğe bağlı video) akışı.</span><span class="sxs-lookup"><span data-stu-id="db899-170">Record and store hello ingested content in order toobe streamed later (Video-on-Demand).</span></span>

<span data-ttu-id="db899-171">Canlı akış yaparken yönlendirir hello aşağıdakilerden birini seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="db899-171">When doing live streaming, you can choose one of hello following routes:</span></span>

### <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a><span data-ttu-id="db899-172">Şirket içi kodlayıcılardan çoklu bit hızlı canlı akış alan kanallar ile çalışma (doğrudan geçiş)</span><span class="sxs-lookup"><span data-stu-id="db899-172">Working with channels that receive multi-bitrate live stream from on-premises encoders (pass-through)</span></span>

<span data-ttu-id="db899-173">Merhaba Aşağıdaki diyagramda hello oynayan başlıca parçaları hello AMS platformunun hello gösterilmektedir **doğrudan** iş akışı.</span><span class="sxs-lookup"><span data-stu-id="db899-173">hello following diagram shows hello major parts of hello AMS platform that are involved in hello **pass-through** workflow.</span></span>

![Canlı iş akışı](./media/scenarios-and-availability/media-services-live-streaming-current.png)

<span data-ttu-id="db899-175">Daha fazla bilgi için bkz. [Şirket İçi Kodlayıcılardan Çoklu Bit Hızlı Canlı Akış Alan Kanallar ile Çalışma](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="db899-175">For more information, see [Working with Channels that Receive Multi-bitrate Live Stream from On-premises Encoders](media-services-live-streaming-with-onprem-encoders.md).</span></span>

### <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a><span data-ttu-id="db899-176">Azure Media Services ile kodlama Canlı tooperform olan kanallar ile çalışma etkin</span><span class="sxs-lookup"><span data-stu-id="db899-176">Working with channels that are enabled tooperform live encoding with Azure Media Services</span></span>

<span data-ttu-id="db899-177">Merhaba Aşağıdaki diyagramda hello önemli bir kanal olduğu canlı akış iş akışında oynayan parçaları hello AMS platformunun tooperform Media Services ile kodlama Canlı etkin gösterir.</span><span class="sxs-lookup"><span data-stu-id="db899-177">hello following diagram shows hello major parts of hello AMS platform that are involved in Live Streaming workflow where a Channel is enabled tooperform live encoding with Media Services.</span></span>

![Canlı iş akışı](./media/scenarios-and-availability/media-services-live-streaming-new.png)

<span data-ttu-id="db899-179">Daha fazla bilgi için bkz: [etkin tooPerform Canlı Azure Media Services ile kodlama olan kanallar ile çalışma](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="db899-179">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="db899-180">Merhaba veri merkezlerinde kullanılabilirliği hakkında daha fazla bilgi için bkz [kullanılabilirlik](#availability) bölümü.</span><span class="sxs-lookup"><span data-stu-id="db899-180">For information about availability in datacenters, see hello [Availability](#availability) section.</span></span>

## <a name="consuming-content"></a><span data-ttu-id="db899-181">İçerik kullanma</span><span class="sxs-lookup"><span data-stu-id="db899-181">Consuming content</span></span>

<span data-ttu-id="db899-182">Azure Media Services sağlar hello araçları toocreate zengin gereksinim dinamik istemci oynatıcı uygulamaları dahil olmak üzere çoğu Platform: iOS cihazları, Android cihazları, Windows, Windows Phone, Xbox ve alıcı kutuları.</span><span class="sxs-lookup"><span data-stu-id="db899-182">Azure Media Services provides hello tools you need toocreate rich, dynamic client player applications for most platforms including: iOS Devices, Android Devices, Windows, Windows Phone, Xbox, and Set-top boxes.</span></span> <span data-ttu-id="db899-183">konu aşağıdaki hello bağlantılar tooSDKs ve oynatıcı çerçevelerine Media Services akış medyadan tüketebileceği kendi istemci uygulamalarınızı toodevelop kullanabilirsiniz sağlar.</span><span class="sxs-lookup"><span data-stu-id="db899-183">hello following topic provides links tooSDKs and Player Frameworks that you can use toodevelop your own client applications that can consume streaming media from Media Services.</span></span> <span data-ttu-id="db899-184">Daha fazla bilgi için bkz. [Video oynatma uygulamaları geliştirme](media-services-develop-video-players.md)</span><span class="sxs-lookup"><span data-stu-id="db899-184">For more information, see [Developing video payer applications](media-services-develop-video-players.md)</span></span>

## <a name="enabling-azure-cdn"></a><span data-ttu-id="db899-185">Azure CDN'yi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="db899-185">Enabling Azure CDN</span></span>

<span data-ttu-id="db899-186">Media Services, Azure CDN ile tümleştirmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="db899-186">Media Services supports integration with Azure CDN.</span></span> <span data-ttu-id="db899-187">Hakkında bilgi için bkz tooenable Azure CDN [nasıl tooManage akış uç noktalarını Media Services hesabı](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="db899-187">For information on how tooenable Azure CDN, see [How tooManage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>

## <span data-ttu-id="db899-188"><a id="scaling"></a>Media Services hesabını ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="db899-188"><a id="scaling"></a>Scaling a Media Services account</span></span>

<span data-ttu-id="db899-189">AMS müşterileri akış uç noktalarını, medya işleme ve depolamayı kendi AMS hesaplarında ölçeklendirebilir.</span><span class="sxs-lookup"><span data-stu-id="db899-189">AMS customers can scale streaming endpoints, media processing, and storage in their AMS accounts.</span></span>

* <span data-ttu-id="db899-190">Media Services müşterileri **Standart** akış uç noktası veya **Premium** akış uç noktası seçebilir.</span><span class="sxs-lookup"><span data-stu-id="db899-190">Media Services customers can choose either a **Standard** streaming endpoint or a **Premium** streaming endpoint.</span></span> <span data-ttu-id="db899-191">**Standart** akış uç noktası çoğu akış iş yükü için uygundur.</span><span class="sxs-lookup"><span data-stu-id="db899-191">A **Standard** streaming endpoint is suitable for most streaming workloads.</span></span> <span data-ttu-id="db899-192">Aynı özellikleri olarak hello içeren bir **Premium** uç noktaları ve ölçekler giden bant genişliği otomatik olarak akış.</span><span class="sxs-lookup"><span data-stu-id="db899-192">It includes hello same features as a **Premium** streaming endpoints and scales outbound bandwidth automatically.</span></span> 

    <span data-ttu-id="db899-193">**Premium** akış uç noktaları, adanmış ve ölçeklenebilir bant genişliği kapasitesi sağlar; dolayısıyla gelişmiş iş yükleri için uygundur.</span><span class="sxs-lookup"><span data-stu-id="db899-193">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="db899-194">**Premium** akış uç noktası olan müşteriler, varsayılan olarak bir akış birimi (SU) alır.</span><span class="sxs-lookup"><span data-stu-id="db899-194">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="db899-195">Akış uç noktası hello SUs eklenerek genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="db899-195">hello streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="db899-196">Her SU ek bant genişliği kapasitesi toohello uygulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="db899-196">Each SU provides additional bandwidth capacity toohello application.</span></span> <span data-ttu-id="db899-197">Ölçeklendirme hakkında daha fazla bilgi için **Premium** akış uç noktaları, hello bkz [akış uç noktalarını ölçeklendirme](media-services-portal-scale-streaming-endpoints.md) konu.</span><span class="sxs-lookup"><span data-stu-id="db899-197">For more information about scaling **Premium** streaming endpoints, see hello [Scaling streaming endpoints](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

* <span data-ttu-id="db899-198">Bir Media Services hesabı bir ayrılmış birim görevleri işleme medyanızı işlenme hello hızı belirleyen türü ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="db899-198">A Media Services account is associated with a Reserved Unit Type, which determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="db899-199">Merhaba aşağıdaki arasında seçim yapabilirsiniz ayrılmış birim türleri: **S1**, **S2**, veya **S3**.</span><span class="sxs-lookup"><span data-stu-id="db899-199">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="db899-200">Örneğin, aynı kodlama işi çalıştıktan daha hızlı hello kullandığınızda hello **S2** ayrılmış birim türü karşılaştırma toohello **S1** türü.</span><span class="sxs-lookup"><span data-stu-id="db899-200">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span>

    <span data-ttu-id="db899-201">Ayrıca toospecifying hello ayrılmış birim türü, hesabınızla tooprovision belirtebilirsiniz **ayrılan birimler** (RUs).</span><span class="sxs-lookup"><span data-stu-id="db899-201">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="db899-202">sağlanan RUs Hello sayısı belirli bir hesap eşzamanlı olarak işlenebilecek ortam görevleri hello sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="db899-202">hello number of provisioned RUs determines hello number of media tasks that can be processed concurrently in a given account.</span></span>

    >[!NOTE]
    ><span data-ttu-id="db899-203">RU, tüm medya işlemesini paralel hale getirmek için çalışır ve Azure Media Indexer’ın kullanıldığı dizin oluşturma işleri de buna dahildir.</span><span class="sxs-lookup"><span data-stu-id="db899-203">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="db899-204">Bununla birlikte kodlamadan farklı olarak, dizin oluşturma işleri daha hızlı ayrılmış birimlerde daha hızlı işlenmez.</span><span class="sxs-lookup"><span data-stu-id="db899-204">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

    <span data-ttu-id="db899-205">Daha fazla bilgi için bkz. [Medya işlemeyi ölçeklendirme](media-services-portal-scale-media-processing.md).</span><span class="sxs-lookup"><span data-stu-id="db899-205">For more information see, [Scale media processing](media-services-portal-scale-media-processing.md).</span></span>
* <span data-ttu-id="db899-206">Media Services hesabınızı depolama hesapları tooit ekleyerek de ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db899-206">You can also scale your Media Services account by adding storage accounts tooit.</span></span> <span data-ttu-id="db899-207">Her Depolama hesabı sınırlı too500 TB'tır.</span><span class="sxs-lookup"><span data-stu-id="db899-207">Each storage account is limited too500 TB.</span></span> <span data-ttu-id="db899-208">tooexpand deponuzda hello varsayılan sınırlamaların ötesine birden çok depolama hesapları tooa tek Media Services hesabı tooattach seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db899-208">tooexpand your storage beyond hello default limitations, you can choose tooattach multiple storage accounts tooa single Media Services account.</span></span> <span data-ttu-id="db899-209">Daha fazla bilgi için bkz. [Depolama hesaplarını yönetme](meda-services-managing-multiple-storage-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="db899-209">For more information, see [Manage storage accounts](meda-services-managing-multiple-storage-accounts.md).</span></span>

##<span data-ttu-id="db899-210"><a id="availability"></a> Media Services özelliklerinin veri merkezleri arasında kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="db899-210"><a id="availability"></a> Availability of Media Services features across datacenters</span></span>

<span data-ttu-id="db899-211">Bu bölümde, Media Services özelliklerinin veri merkezleri arasında kullanılabilirliği hakkındaki ayrıntılar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="db899-211">This section provides details about availability of Media Services features across datacenters.</span></span>

### <a name="ams-accounts"></a><span data-ttu-id="db899-212">AMS hesapları</span><span class="sxs-lookup"><span data-stu-id="db899-212">AMS accounts</span></span>

#### <a name="availability"></a><span data-ttu-id="db899-213">Kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="db899-213">Availability</span></span>

<span data-ttu-id="db899-214">Bölgeler şu hello Media Services hesapları oluşturabilirsiniz: Kuzey Avrupa, Batı Avrupa, Batı ABD, Doğu ABD, Güneydoğu Asya, Doğu Asya, Japonya Batı, Japonya Doğu, Brezilya Güney, Hindistan Batı, Hindistan Güney ve Hindistan orta.</span><span class="sxs-lookup"><span data-stu-id="db899-214">You can create Media Services accounts in hello following regions: North Europe, West Europe, West US, East US, Southeast Asia, East Asia, Japan West, Japan East, Brazil South, India West, India South, and India Central.</span></span> 

### <a name="streaming-endpoints"></a><span data-ttu-id="db899-215">Akış uç noktaları</span><span class="sxs-lookup"><span data-stu-id="db899-215">Streaming endpoints</span></span> 

<span data-ttu-id="db899-216">Media Services müşterileri **Standart** akış uç noktası veya **Premium** akış uç noktası seçebilir.</span><span class="sxs-lookup"><span data-stu-id="db899-216">Media Services customers can choose either a **Standard** streaming endpoint or a **Premium** streaming endpoint.</span></span> <span data-ttu-id="db899-217">Daha fazla bilgi için bkz: Merhaba [ölçeklendirme](#scaling) bölümü.</span><span class="sxs-lookup"><span data-stu-id="db899-217">For more information, see hello [scaling](#scaling) section.</span></span>

#### <a name="availability"></a><span data-ttu-id="db899-218">Kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="db899-218">Availability</span></span>

|<span data-ttu-id="db899-219">Ad</span><span class="sxs-lookup"><span data-stu-id="db899-219">Name</span></span>|<span data-ttu-id="db899-220">Durum</span><span class="sxs-lookup"><span data-stu-id="db899-220">Status</span></span>|<span data-ttu-id="db899-221">Veri merkezleri</span><span class="sxs-lookup"><span data-stu-id="db899-221">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="db899-222">Standart</span><span class="sxs-lookup"><span data-stu-id="db899-222">Standard</span></span>|<span data-ttu-id="db899-223">GA</span><span class="sxs-lookup"><span data-stu-id="db899-223">GA</span></span>|<span data-ttu-id="db899-224">Tümü</span><span class="sxs-lookup"><span data-stu-id="db899-224">All</span></span>|
|<span data-ttu-id="db899-225">Premium</span><span class="sxs-lookup"><span data-stu-id="db899-225">Premium</span></span>|<span data-ttu-id="db899-226">GA</span><span class="sxs-lookup"><span data-stu-id="db899-226">GA</span></span>|<span data-ttu-id="db899-227">Tümü</span><span class="sxs-lookup"><span data-stu-id="db899-227">All</span></span>|

### <a name="live-encoding"></a><span data-ttu-id="db899-228">Live encoding</span><span class="sxs-lookup"><span data-stu-id="db899-228">Live encoding</span></span>

#### <a name="availability"></a><span data-ttu-id="db899-229">Kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="db899-229">Availability</span></span>

<span data-ttu-id="db899-230">Şu bölgeler hariç tüm veri merkezlerinde kullanılabilir: Almanya, Brezilya Güney, Hindistan Batı, Hindistan Güney ve Hindistan Orta.</span><span class="sxs-lookup"><span data-stu-id="db899-230">Available in all datacenters except: Germany, Brazil South, India West, India South, and India Central.</span></span> 

### <a name="encoding-media-processors"></a><span data-ttu-id="db899-231">Kodlama medya işleyicileri</span><span class="sxs-lookup"><span data-stu-id="db899-231">Encoding media processors</span></span>

<span data-ttu-id="db899-232">AMS, isteğe bağlı iki kodlayıcı sunar: **Media Encoder Standard** ve **Media Encoder Premium İş Akışı**.</span><span class="sxs-lookup"><span data-stu-id="db899-232">AMS offers two on-demand encoders **Media Encoder Standard** and **Media Encoder Premium Workflow**.</span></span> <span data-ttu-id="db899-233">Daha fazla bilgi için bkz. [Azure isteğe bağlı medya kodlayıcılarına genel bakış ve karşılaştırma](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="db899-233">For more information, see [Overview and comparison of Azure on-demand media encoders](media-services-encode-asset.md).</span></span> 

#### <a name="availability"></a><span data-ttu-id="db899-234">Kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="db899-234">Availability</span></span>

|<span data-ttu-id="db899-235">Medya işlemci adı</span><span class="sxs-lookup"><span data-stu-id="db899-235">Media processor name</span></span>|<span data-ttu-id="db899-236">Durum</span><span class="sxs-lookup"><span data-stu-id="db899-236">Status</span></span>|<span data-ttu-id="db899-237">Veri merkezleri</span><span class="sxs-lookup"><span data-stu-id="db899-237">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="db899-238">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="db899-238">Media Encoder Standard</span></span>|<span data-ttu-id="db899-239">GA</span><span class="sxs-lookup"><span data-stu-id="db899-239">GA</span></span>|<span data-ttu-id="db899-240">Tümü</span><span class="sxs-lookup"><span data-stu-id="db899-240">All</span></span>|
|<span data-ttu-id="db899-241">Media Encoder Premium İş Akışı</span><span class="sxs-lookup"><span data-stu-id="db899-241">Media Encoder Premium Workflow</span></span>|<span data-ttu-id="db899-242">GA</span><span class="sxs-lookup"><span data-stu-id="db899-242">GA</span></span>|<span data-ttu-id="db899-243">Çin dışında tümü</span><span class="sxs-lookup"><span data-stu-id="db899-243">All except China</span></span>|

### <a name="analytics-media-processors"></a><span data-ttu-id="db899-244">Analiz medya işlemcileri</span><span class="sxs-lookup"><span data-stu-id="db899-244">Analytics media processors</span></span>

<span data-ttu-id="db899-245">Medya analizi, kuruluş ve işletmelerin tooderive eyleme dönüştürülebilir Öngörüler kendi video dosyalarından kolaylaştırır konuşma ve görme bileşenidir koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="db899-245">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="db899-246">Daha fazla bilgi için bkz. [Azure Media Services Analizi’ne Genel Bakış](media-services-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="db899-246">For more information, see [Azure Media Services Analytics Overview](media-services-analytics-overview.md).</span></span>

#### <a name="availability"></a><span data-ttu-id="db899-247">Kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="db899-247">Availability</span></span>

|<span data-ttu-id="db899-248">Medya işlemci adı</span><span class="sxs-lookup"><span data-stu-id="db899-248">Media processor name</span></span>|<span data-ttu-id="db899-249">Durum</span><span class="sxs-lookup"><span data-stu-id="db899-249">Status</span></span>|<span data-ttu-id="db899-250">Veri merkezleri</span><span class="sxs-lookup"><span data-stu-id="db899-250">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="db899-251">Azure Media Face Detector</span><span class="sxs-lookup"><span data-stu-id="db899-251">Azure Media Face Detector</span></span>|<span data-ttu-id="db899-252">Önizleme</span><span class="sxs-lookup"><span data-stu-id="db899-252">Preview</span></span>|<span data-ttu-id="db899-253">Tümü</span><span class="sxs-lookup"><span data-stu-id="db899-253">All</span></span>|
|<span data-ttu-id="db899-254">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="db899-254">Azure Media Hyperlapse</span></span>|<span data-ttu-id="db899-255">Önizleme</span><span class="sxs-lookup"><span data-stu-id="db899-255">Preview</span></span>|<span data-ttu-id="db899-256">Tümü</span><span class="sxs-lookup"><span data-stu-id="db899-256">All</span></span>|
|<span data-ttu-id="db899-257">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="db899-257">Azure Media Indexer</span></span>|<span data-ttu-id="db899-258">GA</span><span class="sxs-lookup"><span data-stu-id="db899-258">GA</span></span>|<span data-ttu-id="db899-259">Tümü</span><span class="sxs-lookup"><span data-stu-id="db899-259">All</span></span>|
|<span data-ttu-id="db899-260">Azure Media Motion Detector</span><span class="sxs-lookup"><span data-stu-id="db899-260">Azure Media Motion Detector</span></span>|<span data-ttu-id="db899-261">Önizleme</span><span class="sxs-lookup"><span data-stu-id="db899-261">Preview</span></span>|<span data-ttu-id="db899-262">Tümü</span><span class="sxs-lookup"><span data-stu-id="db899-262">All</span></span>|
|<span data-ttu-id="db899-263">Azure Media OCR</span><span class="sxs-lookup"><span data-stu-id="db899-263">Azure Media OCR</span></span>|<span data-ttu-id="db899-264">Önizleme</span><span class="sxs-lookup"><span data-stu-id="db899-264">Preview</span></span>|<span data-ttu-id="db899-265">Tümü</span><span class="sxs-lookup"><span data-stu-id="db899-265">All</span></span>|
|<span data-ttu-id="db899-266">Azure Media Redactor</span><span class="sxs-lookup"><span data-stu-id="db899-266">Azure Media Redactor</span></span>|<span data-ttu-id="db899-267">Önizleme</span><span class="sxs-lookup"><span data-stu-id="db899-267">Preview</span></span>|<span data-ttu-id="db899-268">Tümü</span><span class="sxs-lookup"><span data-stu-id="db899-268">All</span></span>|
|<span data-ttu-id="db899-269">Azure Media Stabilizer</span><span class="sxs-lookup"><span data-stu-id="db899-269">Azure Media Stabilizer</span></span>|<span data-ttu-id="db899-270">Önizleme</span><span class="sxs-lookup"><span data-stu-id="db899-270">Preview</span></span>|<span data-ttu-id="db899-271">Tümü</span><span class="sxs-lookup"><span data-stu-id="db899-271">All</span></span>|
|<span data-ttu-id="db899-272">Azure Media Video Thumbnails</span><span class="sxs-lookup"><span data-stu-id="db899-272">Azure Media Video Thumbnails</span></span>|<span data-ttu-id="db899-273">Önizleme</span><span class="sxs-lookup"><span data-stu-id="db899-273">Preview</span></span>|<span data-ttu-id="db899-274">Tümü</span><span class="sxs-lookup"><span data-stu-id="db899-274">All</span></span>|
|<span data-ttu-id="db899-275">Azure Media Indexer 2</span><span class="sxs-lookup"><span data-stu-id="db899-275">Azure Media Indexer 2</span></span>|<span data-ttu-id="db899-276">Önizleme</span><span class="sxs-lookup"><span data-stu-id="db899-276">Preview</span></span>|<span data-ttu-id="db899-277">Çin ve Federal Devlet bölgesi dışında tümü</span><span class="sxs-lookup"><span data-stu-id="db899-277">All except China and Federal Government region</span></span>|

### <a name="protection"></a><span data-ttu-id="db899-278">Koruma</span><span class="sxs-lookup"><span data-stu-id="db899-278">Protection</span></span>

<span data-ttu-id="db899-279">Microsoft Azure Media Services, toosecure, depolama, işleme ve teslim üzerinden bilgisayarınıza hello çıkışında medyanızdan sağlar.</span><span class="sxs-lookup"><span data-stu-id="db899-279">Microsoft Azure Media Services enables you toosecure your media from hello time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="db899-280">Daha fazla bilgi için bkz. [AMS içeriğini koruma](media-services-content-protection-overview.md).</span><span class="sxs-lookup"><span data-stu-id="db899-280">For more information, see [Protecting AMS content](media-services-content-protection-overview.md).</span></span>

#### <a name="availability"></a><span data-ttu-id="db899-281">Kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="db899-281">Availability</span></span>

|<span data-ttu-id="db899-282">Şifreleme</span><span class="sxs-lookup"><span data-stu-id="db899-282">Encryption</span></span>|<span data-ttu-id="db899-283">Durum</span><span class="sxs-lookup"><span data-stu-id="db899-283">Status</span></span>|<span data-ttu-id="db899-284">Veri merkezleri</span><span class="sxs-lookup"><span data-stu-id="db899-284">Datacenters</span></span>|
|---|---|---| 
|<span data-ttu-id="db899-285">Depolama</span><span class="sxs-lookup"><span data-stu-id="db899-285">Storage</span></span>|<span data-ttu-id="db899-286">GA</span><span class="sxs-lookup"><span data-stu-id="db899-286">GA</span></span>|<span data-ttu-id="db899-287">Tümü</span><span class="sxs-lookup"><span data-stu-id="db899-287">All</span></span>|
|<span data-ttu-id="db899-288">AES-128 anahtarları</span><span class="sxs-lookup"><span data-stu-id="db899-288">AES-128 keys</span></span>|<span data-ttu-id="db899-289">GA</span><span class="sxs-lookup"><span data-stu-id="db899-289">GA</span></span>|<span data-ttu-id="db899-290">Tümü</span><span class="sxs-lookup"><span data-stu-id="db899-290">All</span></span>|
|<span data-ttu-id="db899-291">Fairplay</span><span class="sxs-lookup"><span data-stu-id="db899-291">Fairplay</span></span>|<span data-ttu-id="db899-292">GA</span><span class="sxs-lookup"><span data-stu-id="db899-292">GA</span></span>|<span data-ttu-id="db899-293">Tümü</span><span class="sxs-lookup"><span data-stu-id="db899-293">All</span></span>|
|<span data-ttu-id="db899-294">PlayReady</span><span class="sxs-lookup"><span data-stu-id="db899-294">PlayReady</span></span>|<span data-ttu-id="db899-295">GA</span><span class="sxs-lookup"><span data-stu-id="db899-295">GA</span></span>|<span data-ttu-id="db899-296">Tümü</span><span class="sxs-lookup"><span data-stu-id="db899-296">All</span></span>|
|<span data-ttu-id="db899-297">Widevine</span><span class="sxs-lookup"><span data-stu-id="db899-297">Widevine</span></span>|<span data-ttu-id="db899-298">GA</span><span class="sxs-lookup"><span data-stu-id="db899-298">GA</span></span>|<span data-ttu-id="db899-299">Almanya, Federal Devlet ve Çin dışında tümü.</span><span class="sxs-lookup"><span data-stu-id="db899-299">All except Germany, Federal Government and China.</span></span>

### <a name="reserved-units-rus"></a><span data-ttu-id="db899-300">Ayrılmış birimler (RU)</span><span class="sxs-lookup"><span data-stu-id="db899-300">Reserved units (RUs)</span></span>

<span data-ttu-id="db899-301">sağlanan ayrılmış birim Hello sayısı belirli bir hesap eşzamanlı olarak işlenebilecek ortam görevleri hello sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="db899-301">hello number of provisioned reserved units determines hello number of media tasks that can be processed concurrently in a given account.</span></span> 

<span data-ttu-id="db899-302">Daha fazla bilgi için bkz: Merhaba [ölçeklendirme](#scaling) bölümü.</span><span class="sxs-lookup"><span data-stu-id="db899-302">For more information, see hello [scaling](#scaling) section.</span></span>

#### <a name="availability"></a><span data-ttu-id="db899-303">Kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="db899-303">Availability</span></span>

<span data-ttu-id="db899-304">Tüm veri merkezlerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="db899-304">Available in all datacenters.</span></span>

### <a name="reserved-unit-ru-type"></a><span data-ttu-id="db899-305">Ayrılmış birim (RU) türü</span><span class="sxs-lookup"><span data-stu-id="db899-305">Reserved unit (RU) type</span></span>

<span data-ttu-id="db899-306">Bir Media Services hesabı görevleri işleme medyanızı işlenme hello hızını belirler ve ayrılmış birim türü ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="db899-306">A Media Services account is associated with a Reserved unit type, which determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="db899-307">Merhaba aşağıdaki arasında seçim yapabilirsiniz ayrılmış birim türleri: S1, S2 ve S3.</span><span class="sxs-lookup"><span data-stu-id="db899-307">You can pick between hello following reserved unit types: S1, S2, or S3.</span></span>

<span data-ttu-id="db899-308">Daha fazla bilgi için bkz: Merhaba [ölçeklendirme](#scaling) bölümü.</span><span class="sxs-lookup"><span data-stu-id="db899-308">For more information, see hello [scaling](#scaling) section.</span></span>

#### <a name="availability"></a><span data-ttu-id="db899-309">Kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="db899-309">Availability</span></span>

|<span data-ttu-id="db899-310">RU türü adı</span><span class="sxs-lookup"><span data-stu-id="db899-310">RU type name</span></span>|<span data-ttu-id="db899-311">Durum</span><span class="sxs-lookup"><span data-stu-id="db899-311">Status</span></span>|<span data-ttu-id="db899-312">Veri merkezleri</span><span class="sxs-lookup"><span data-stu-id="db899-312">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="db899-313">S1</span><span class="sxs-lookup"><span data-stu-id="db899-313">S1</span></span>|<span data-ttu-id="db899-314">GA</span><span class="sxs-lookup"><span data-stu-id="db899-314">GA</span></span>|<span data-ttu-id="db899-315">Tümü</span><span class="sxs-lookup"><span data-stu-id="db899-315">All</span></span>|
|<span data-ttu-id="db899-316">S2</span><span class="sxs-lookup"><span data-stu-id="db899-316">S2</span></span>|<span data-ttu-id="db899-317">GA</span><span class="sxs-lookup"><span data-stu-id="db899-317">GA</span></span>|<span data-ttu-id="db899-318">Brezilya Güney ve Hindistan Batı dışında tümü</span><span class="sxs-lookup"><span data-stu-id="db899-318">All except Brazil South, and India West</span></span>|
|<span data-ttu-id="db899-319">S3</span><span class="sxs-lookup"><span data-stu-id="db899-319">S3</span></span>|<span data-ttu-id="db899-320">GA</span><span class="sxs-lookup"><span data-stu-id="db899-320">GA</span></span>|<span data-ttu-id="db899-321">Hindistan Batı dışında tümü</span><span class="sxs-lookup"><span data-stu-id="db899-321">All except India West</span></span>|

## <a name="next-steps"></a><span data-ttu-id="db899-322">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="db899-322">Next steps</span></span>

<span data-ttu-id="db899-323">Media Services öğrenme yollarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="db899-323">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="db899-324">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="db899-324">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

