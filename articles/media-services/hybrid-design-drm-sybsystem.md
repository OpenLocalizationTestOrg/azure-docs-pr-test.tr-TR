---
title: "Azure Media Services'i kullanarak DRM subsystem(s) aaaHybrid tasarımını | Microsoft Docs"
description: "Bu konu Azure Media Services'i kullanarak DRM subsystem(s) karma tasarımını açıklar."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 4206248420ccd4dbfc9a87a86f4763534c6254a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-design-of-drm-subsystems"></a><span data-ttu-id="8c9ea-103">DRM subsystem(s) karma tasarımı</span><span class="sxs-lookup"><span data-stu-id="8c9ea-103">Hybrid design of DRM subsystem(s)</span></span>

<span data-ttu-id="8c9ea-104">Bu konu Azure Media Services'i kullanarak DRM subsystem(s) karma tasarımını açıklar.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-104">This topic discusses hybrid design of DRM subsystem(s) using Azure Media Services.</span></span>

## <a name="overview"></a><span data-ttu-id="8c9ea-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="8c9ea-105">Overview</span></span>

<span data-ttu-id="8c9ea-106">Azure Media Services üç DRM sistem aşağıdaki hello için destek sağlar:</span><span class="sxs-lookup"><span data-stu-id="8c9ea-106">Azure Media Services provides support for hello following three DRM system:</span></span>

* <span data-ttu-id="8c9ea-107">PlayReady</span><span class="sxs-lookup"><span data-stu-id="8c9ea-107">PlayReady</span></span>
* <span data-ttu-id="8c9ea-108">Widevine (modüler)</span><span class="sxs-lookup"><span data-stu-id="8c9ea-108">Widevine (Modular)</span></span>
* <span data-ttu-id="8c9ea-109">FairPlay</span><span class="sxs-lookup"><span data-stu-id="8c9ea-109">FairPlay</span></span>

<span data-ttu-id="8c9ea-110">Merhaba DRM desteği, Azure Media Player tarayıcı player SDK'sı tüm 3 DRMs destekleme ile DRM şifreleme (dinamik şifreleme) ve lisans teslimat içerir.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-110">hello DRM support includes DRM encryption (dynamic encryption) and license delivery, with Azure Media Player supporting all 3 DRMs as a browser player SDK.</span></span>

<span data-ttu-id="8c9ea-111">DRM/CENC alt sistemi tasarım ve uygulama ayrıntılı işlenmesi için lütfen başlıklı hello belgesine bakın [çoklu DRM ve erişim denetimi ile CENC](media-services-cenc-with-multidrm-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="8c9ea-111">For a detailed treatment of DRM/CENC subsystem design and implementation, please see hello document titled [CENC with Multi-DRM and Access Control](media-services-cenc-with-multidrm-access-control.md).</span></span>

<span data-ttu-id="8c9ea-112">Bazen üç DRM sistemi için tam destek sunuyoruz rağmen müşterilerin kendi altyapı/alt toplama tooAzure Media Services toobuild karma DRM alt sistemi çeşitli kısımlarını toouse gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-112">Although we offer complete support for three DRM systems, sometimes customers need toouse various parts of their own infrastructure/subsystems in addition tooAzure Media Services toobuild a hybrid DRM subsystem.</span></span>

<span data-ttu-id="8c9ea-113">Aşağıda bazı sık sorulan soruları müşteriler tarafından istenir:</span><span class="sxs-lookup"><span data-stu-id="8c9ea-113">Below are some common questions asked by customers:</span></span>

* <span data-ttu-id="8c9ea-114">"Kendi DRM lisans sunucularını kullanabilir miyim?"</span><span class="sxs-lookup"><span data-stu-id="8c9ea-114">"Can I use my own DRM license servers?"</span></span> <span data-ttu-id="8c9ea-115">(Bu durumda, müşterilerin DRM lisans sunucusu grubunda katıştırılmış iş mantığı ile yatırım yapmış kullanıcılar).</span><span class="sxs-lookup"><span data-stu-id="8c9ea-115">(In this case, customers have invested in DRM license server farm with embedded business logic).</span></span>
* <span data-ttu-id="8c9ea-116">"Yalnızca, DRM lisans teslimat Azure Media Services AMS içeriği barındırma olmadan kullanabilir miyim?"</span><span class="sxs-lookup"><span data-stu-id="8c9ea-116">"Can I use only your DRM license delivery in Azure Media Services without hosting content in AMS?"</span></span>

## <a name="modularity-of-hello-ams-drm-platform"></a><span data-ttu-id="8c9ea-117">Merhaba AMS DRM platform modülerlik</span><span class="sxs-lookup"><span data-stu-id="8c9ea-117">Modularity of hello AMS DRM platform</span></span>

<span data-ttu-id="8c9ea-118">Kapsamlı bulut video platformu bir parçası olarak, Azure Media Services DRM göz önünde esneklik ve modülerlik ile bir tasarıma sahiptir.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-118">As part of a comprehensive cloud video platform, Azure Media Services DRM has a design with flexibility and modularity in mind.</span></span> <span data-ttu-id="8c9ea-119">Azure Media Services, farklı birleşimler (Merhaba tablosunda kullanılan hello gösterimi açıklaması izleyen) hello aşağıdaki tabloda açıklanan aşağıdaki hello biriyle kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-119">You can use Azure Media Services with any of hello following different combinations described in hello table below (an explanation of hello notation used in hello table follows).</span></span> 

|<span data-ttu-id="8c9ea-120">**Barındırma & Kaynak içerik**</span><span class="sxs-lookup"><span data-stu-id="8c9ea-120">**Content hosting & origin**</span></span>|<span data-ttu-id="8c9ea-121">**İçerik şifreleme**</span><span class="sxs-lookup"><span data-stu-id="8c9ea-121">**Content encryption**</span></span>|<span data-ttu-id="8c9ea-122">**DRM lisansı teslimi**</span><span class="sxs-lookup"><span data-stu-id="8c9ea-122">**DRM license delivery**</span></span>|
|---|---|---|
|<span data-ttu-id="8c9ea-123">AMS</span><span class="sxs-lookup"><span data-stu-id="8c9ea-123">AMS</span></span>|<span data-ttu-id="8c9ea-124">AMS</span><span class="sxs-lookup"><span data-stu-id="8c9ea-124">AMS</span></span>|<span data-ttu-id="8c9ea-125">AMS</span><span class="sxs-lookup"><span data-stu-id="8c9ea-125">AMS</span></span>|
|<span data-ttu-id="8c9ea-126">AMS</span><span class="sxs-lookup"><span data-stu-id="8c9ea-126">AMS</span></span>|<span data-ttu-id="8c9ea-127">AMS</span><span class="sxs-lookup"><span data-stu-id="8c9ea-127">AMS</span></span>|<span data-ttu-id="8c9ea-128">Üçüncü taraf</span><span class="sxs-lookup"><span data-stu-id="8c9ea-128">Third-party</span></span>|
|<span data-ttu-id="8c9ea-129">AMS</span><span class="sxs-lookup"><span data-stu-id="8c9ea-129">AMS</span></span>|<span data-ttu-id="8c9ea-130">Üçüncü taraf</span><span class="sxs-lookup"><span data-stu-id="8c9ea-130">Third-party</span></span>|<span data-ttu-id="8c9ea-131">AMS</span><span class="sxs-lookup"><span data-stu-id="8c9ea-131">AMS</span></span>|
|<span data-ttu-id="8c9ea-132">AMS</span><span class="sxs-lookup"><span data-stu-id="8c9ea-132">AMS</span></span>|<span data-ttu-id="8c9ea-133">Üçüncü taraf</span><span class="sxs-lookup"><span data-stu-id="8c9ea-133">Third-party</span></span>|<span data-ttu-id="8c9ea-134">Üçüncü taraf</span><span class="sxs-lookup"><span data-stu-id="8c9ea-134">Third-party</span></span>|
|<span data-ttu-id="8c9ea-135">Üçüncü taraf</span><span class="sxs-lookup"><span data-stu-id="8c9ea-135">Third-party</span></span>|<span data-ttu-id="8c9ea-136">Üçüncü taraf</span><span class="sxs-lookup"><span data-stu-id="8c9ea-136">Third-party</span></span>|<span data-ttu-id="8c9ea-137">AMS</span><span class="sxs-lookup"><span data-stu-id="8c9ea-137">AMS</span></span>|

### <a name="content-hosting--origin"></a><span data-ttu-id="8c9ea-138">Barındırma & Kaynak içerik</span><span class="sxs-lookup"><span data-stu-id="8c9ea-138">Content hosting & origin</span></span>

* <span data-ttu-id="8c9ea-139">AMS: varlığı AMS içinde barındırılır ve akış AMS akış uç noktalarını (ancak mutlaka dinamik paketleme) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-139">AMS: video asset is hosted in AMS and streaming is through AMS streaming endpoints (but not necessarily dynamic packaging).</span></span>
* <span data-ttu-id="8c9ea-140">Üçüncü taraf: video barındırılan ve AMS dışında bir üçüncü taraf akış platformunda teslim.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-140">Third-party: video is hosted and delivered on a third-party streaming platform outside of AMS.</span></span>

### <a name="content-encryption"></a><span data-ttu-id="8c9ea-141">İçerik şifreleme</span><span class="sxs-lookup"><span data-stu-id="8c9ea-141">Content encryption</span></span>

* <span data-ttu-id="8c9ea-142">AMS: gerçekleştirilen dinamik olarak/isteğe bağlı AMS dinamik şifreleme tarafından içerik şifrelemesidir.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-142">AMS: content encryption is performed dynamically/on-demand by AMS dynamic encryption.</span></span>
* <span data-ttu-id="8c9ea-143">Üçüncü taraf: işleme öncesi iş akışını kullanarak AMS dışında içerik şifreleme gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-143">Third-party: content encryption is performed outside of AMS using a pre-processing workflow.</span></span>

### <a name="drm-license-delivery"></a><span data-ttu-id="8c9ea-144">DRM lisansı verme</span><span class="sxs-lookup"><span data-stu-id="8c9ea-144">DRM license delivery</span></span>

* <span data-ttu-id="8c9ea-145">AMS: DRM lisans AMS lisans teslimat hizmeti tarafından teslim edilir.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-145">AMS: DRM license is delivered by AMS license delivery service.</span></span>
* <span data-ttu-id="8c9ea-146">Üçüncü taraf: DRM lisans AMS dışında bir üçüncü taraf DRM lisans sunucusu tarafından teslim edilir.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-146">Third-party: DRM license is delivered by a third-party DRM license server outside of AMS.</span></span>

## <a name="configure-based-on-your-hybrid-scenario"></a><span data-ttu-id="8c9ea-147">Yapılandırma karma senaryoyu temel</span><span class="sxs-lookup"><span data-stu-id="8c9ea-147">Configure based on your hybrid scenario</span></span>

### <a name="content-key"></a><span data-ttu-id="8c9ea-148">İçerik anahtarı</span><span class="sxs-lookup"><span data-stu-id="8c9ea-148">Content key</span></span>

<span data-ttu-id="8c9ea-149">Bir içerik anahtarı yapılandırma yoluyla, AMS dinamik şifreleme ve AMS lisans teslimat hizmeti özniteliklerini aşağıdaki hello denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8c9ea-149">Through configuration of a content key, you can control hello following attributes of both AMS dynamic encryption and AMS license delivery service:</span></span>

* <span data-ttu-id="8c9ea-150">dinamik DRM şifreleme için kullanılan hello içerik anahtarı.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-150">hello content key used for dynamic DRM encryption.</span></span>
* <span data-ttu-id="8c9ea-151">DRM lisans içerik toobe lisans teslim hizmetleri tarafından sunulan: hakları, içerik anahtarı ve kısıtlamaları.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-151">DRM license content toobe delivered by license delivery services: rights, content key and restrictions.</span></span>
* <span data-ttu-id="8c9ea-152">Tür **içerik anahtarı yetkilendirme ilkesini kısıtlama**: IP veya belirteç kısıtlamasına açın.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-152">Type of **content key authorization policy restriction**: open, IP, or token restriction.</span></span>
* <span data-ttu-id="8c9ea-153">Varsa **belirteci** türü **içerik anahtarı yetkilendirme ilkesini kısıtlama kullanılır**, hello **içerik anahtarı yetkilendirme ilkesini kısıtlama** lisans verilmeden önce karşılanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-153">If **token** type of **content key authorization policy restriction is used**, hello **content key authorization policy restriction** must be met before a license is issued.</span></span>

### <a name="asset-delivery-policy"></a><span data-ttu-id="8c9ea-154">Varlık teslim ilkesini</span><span class="sxs-lookup"><span data-stu-id="8c9ea-154">Asset delivery policy</span></span>

<span data-ttu-id="8c9ea-155">Bir varlık teslim ilkesini yapılandırma yoluyla, AMS dinamik Paketleyici ve akış uç noktası bir AMS dinamik şifreleme tarafından kullanılan öznitelikleri aşağıdaki hello denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8c9ea-155">Through configuration of an asset delivery policy, you can control hello following attributes used by AMS dynamic packager and dynamic encryption of an AMS streaming endpoint:</span></span>

* <span data-ttu-id="8c9ea-156">Protokol ve DRM şifreleme birleşimi, tire (PlayReady ve Widevine), CENC altında gibi altında PlayReady, Widevine veya PlayReady altında HLS akış kesintisiz akış.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-156">Streaming protocol and DRM encryption combination, such as DASH under CENC (PlayReady and Widevine), smooth streaming under PlayReady, HLS under Widevine or PlayReady.</span></span>
* <span data-ttu-id="8c9ea-157">Merhaba varsayılan ve katıştırılmış lisans teslimat URL'leri her hello DRMs dahil.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-157">hello default/embedded license delivery URLs for each of hello involved DRMs.</span></span>
* <span data-ttu-id="8c9ea-158">Olup tire MPD (LA_URLs) URL'lerinde edinme lisans veya HLS çalma listesi içeren sorgu dizesi kimliği (çocuk) anahtarının Widevine ve FairPlay, sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-158">Whether license acquisition URLs (LA_URLs) in DASH MPD or HLS playlist contain query string of key ID (KID) for Widevine and FairPlay, respectively.</span></span>

## <a name="scenarios-and-samples"></a><span data-ttu-id="8c9ea-159">Senaryolar ve örnekler</span><span class="sxs-lookup"><span data-stu-id="8c9ea-159">Scenarios and samples</span></span>

<span data-ttu-id="8c9ea-160">Merhaba önceki bölümdeki hello açıklamaları bağlı olarak, beş karma senaryolar aşağıdaki hello kullanmak ilgili **içerik anahtarı**-**varlık teslim ilkesini** yapılandırması bileşimleri (Merhaba Merhaba son sütununda belirtilen örnekleri hello tablo izleyin):</span><span class="sxs-lookup"><span data-stu-id="8c9ea-160">Based on hello explanations in hello previous section, hello following five hybrid scenarios use respective **Content key**-**Asset delivery policy** configuration combinations (hello samples mentioned in hello last column follow hello table):</span></span>

|<span data-ttu-id="8c9ea-161">**Barındırma & Kaynak içerik**</span><span class="sxs-lookup"><span data-stu-id="8c9ea-161">**Content hosting & origin**</span></span>|<span data-ttu-id="8c9ea-162">**DRM şifreleme**</span><span class="sxs-lookup"><span data-stu-id="8c9ea-162">**DRM encryption**</span></span>|<span data-ttu-id="8c9ea-163">**DRM lisansı teslimi**</span><span class="sxs-lookup"><span data-stu-id="8c9ea-163">**DRM license delivery**</span></span>|<span data-ttu-id="8c9ea-164">**İçerik anahtarı yapılandırın**</span><span class="sxs-lookup"><span data-stu-id="8c9ea-164">**Configure content key**</span></span>|<span data-ttu-id="8c9ea-165">**Varlık teslim ilkesini yapılandırma**</span><span class="sxs-lookup"><span data-stu-id="8c9ea-165">**Configure asset delivery policy**</span></span>|<span data-ttu-id="8c9ea-166">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="8c9ea-166">**Sample**</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="8c9ea-167">AMS</span><span class="sxs-lookup"><span data-stu-id="8c9ea-167">AMS</span></span>|<span data-ttu-id="8c9ea-168">AMS</span><span class="sxs-lookup"><span data-stu-id="8c9ea-168">AMS</span></span>|<span data-ttu-id="8c9ea-169">AMS</span><span class="sxs-lookup"><span data-stu-id="8c9ea-169">AMS</span></span>|<span data-ttu-id="8c9ea-170">Evet</span><span class="sxs-lookup"><span data-stu-id="8c9ea-170">Yes</span></span>|<span data-ttu-id="8c9ea-171">Evet</span><span class="sxs-lookup"><span data-stu-id="8c9ea-171">Yes</span></span>|<span data-ttu-id="8c9ea-172">Örnek 1</span><span class="sxs-lookup"><span data-stu-id="8c9ea-172">Sample 1</span></span>|
|<span data-ttu-id="8c9ea-173">AMS</span><span class="sxs-lookup"><span data-stu-id="8c9ea-173">AMS</span></span>|<span data-ttu-id="8c9ea-174">AMS</span><span class="sxs-lookup"><span data-stu-id="8c9ea-174">AMS</span></span>|<span data-ttu-id="8c9ea-175">Üçüncü taraf</span><span class="sxs-lookup"><span data-stu-id="8c9ea-175">Third-party</span></span>|<span data-ttu-id="8c9ea-176">Evet</span><span class="sxs-lookup"><span data-stu-id="8c9ea-176">Yes</span></span>|<span data-ttu-id="8c9ea-177">Evet</span><span class="sxs-lookup"><span data-stu-id="8c9ea-177">Yes</span></span>|<span data-ttu-id="8c9ea-178">Örnek 2</span><span class="sxs-lookup"><span data-stu-id="8c9ea-178">Sample 2</span></span>|
|<span data-ttu-id="8c9ea-179">AMS</span><span class="sxs-lookup"><span data-stu-id="8c9ea-179">AMS</span></span>|<span data-ttu-id="8c9ea-180">Üçüncü taraf</span><span class="sxs-lookup"><span data-stu-id="8c9ea-180">Third-party</span></span>|<span data-ttu-id="8c9ea-181">AMS</span><span class="sxs-lookup"><span data-stu-id="8c9ea-181">AMS</span></span>|<span data-ttu-id="8c9ea-182">Evet</span><span class="sxs-lookup"><span data-stu-id="8c9ea-182">Yes</span></span>|<span data-ttu-id="8c9ea-183">Hayır</span><span class="sxs-lookup"><span data-stu-id="8c9ea-183">No</span></span>|<span data-ttu-id="8c9ea-184">Örnek 3</span><span class="sxs-lookup"><span data-stu-id="8c9ea-184">Sample 3</span></span>|
|<span data-ttu-id="8c9ea-185">AMS</span><span class="sxs-lookup"><span data-stu-id="8c9ea-185">AMS</span></span>|<span data-ttu-id="8c9ea-186">Üçüncü taraf</span><span class="sxs-lookup"><span data-stu-id="8c9ea-186">Third-party</span></span>|<span data-ttu-id="8c9ea-187">Dışında</span><span class="sxs-lookup"><span data-stu-id="8c9ea-187">Outside</span></span>|<span data-ttu-id="8c9ea-188">Hayır</span><span class="sxs-lookup"><span data-stu-id="8c9ea-188">No</span></span>|<span data-ttu-id="8c9ea-189">Hayır</span><span class="sxs-lookup"><span data-stu-id="8c9ea-189">No</span></span>|<span data-ttu-id="8c9ea-190">Örnek 4</span><span class="sxs-lookup"><span data-stu-id="8c9ea-190">Sample 4</span></span>|
|<span data-ttu-id="8c9ea-191">Üçüncü taraf</span><span class="sxs-lookup"><span data-stu-id="8c9ea-191">Third-party</span></span>|<span data-ttu-id="8c9ea-192">Üçüncü taraf</span><span class="sxs-lookup"><span data-stu-id="8c9ea-192">Third-party</span></span>|<span data-ttu-id="8c9ea-193">AMS</span><span class="sxs-lookup"><span data-stu-id="8c9ea-193">AMS</span></span>|<span data-ttu-id="8c9ea-194">Evet</span><span class="sxs-lookup"><span data-stu-id="8c9ea-194">Yes</span></span>|<span data-ttu-id="8c9ea-195">Hayır</span><span class="sxs-lookup"><span data-stu-id="8c9ea-195">No</span></span>|    

<span data-ttu-id="8c9ea-196">Merhaba örneklerinde PlayReady koruma tire hem de kesintisiz akış için çalışır.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-196">In hello samples, PlayReady protection works for both DASH and smooth streaming.</span></span> <span data-ttu-id="8c9ea-197">Kesintisiz akış URL'lerini Hello aşağıda bir video URL.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-197">hello video URLs below are smooth streaming URLs.</span></span> <span data-ttu-id="8c9ea-198">tooget karşılık gelen tire URL'leri Merhaba, yalnızca Ekle "(biçim mpd zaman csf =)".</span><span class="sxs-lookup"><span data-stu-id="8c9ea-198">tooget hello corresponding DASH URLs, just append "(format=mpd-time-csf)".</span></span> <span data-ttu-id="8c9ea-199">Merhaba kullanabileceğinizi [azure media player test](http://aka.ms/amtest) bir tarayıcıda tootest.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-199">You could use hello [azure media test player](http://aka.ms/amtest) tootest in a browser.</span></span> <span data-ttu-id="8c9ea-200">Tooconfigure izin verir, hangi teknik altında Protokolü toouse akış.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-200">It allows you tooconfigure which streaming protocol toouse, under which tech.</span></span> <span data-ttu-id="8c9ea-201">IE11 ve Windows 10 MS Edge PlayReady EME aracılığıyla destekler.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-201">IE11 and MS Edge on Windows 10 support PlayReady through EME.</span></span> <span data-ttu-id="8c9ea-202">Daha fazla bilgi için bkz: [hello ayrıntılarını test aracı](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span><span class="sxs-lookup"><span data-stu-id="8c9ea-202">For more information, see [details about hello test tool](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span></span>

### <a name="sample-1"></a><span data-ttu-id="8c9ea-203">Örnek 1</span><span class="sxs-lookup"><span data-stu-id="8c9ea-203">Sample 1</span></span>

* <span data-ttu-id="8c9ea-204">Kaynak (Temel) URL: https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="8c9ea-204">Source (base) URL: https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span></span> 
* <span data-ttu-id="8c9ea-205">PlayReady LA_URL (tire & kesintisiz): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="8c9ea-205">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 
* <span data-ttu-id="8c9ea-206">Widevine LA_URL (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span><span class="sxs-lookup"><span data-stu-id="8c9ea-206">Widevine LA_URL (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span></span> 
* <span data-ttu-id="8c9ea-207">FairPlay LA_URL (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span><span class="sxs-lookup"><span data-stu-id="8c9ea-207">FairPlay LA_URL (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span></span> 

### <a name="sample-2"></a><span data-ttu-id="8c9ea-208">Örnek 2</span><span class="sxs-lookup"><span data-stu-id="8c9ea-208">Sample 2</span></span>

* <span data-ttu-id="8c9ea-209">Kaynak (Temel) URL: http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="8c9ea-209">Source (base) URL: http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span></span> 
* <span data-ttu-id="8c9ea-210">PlayReady LA_URL (tire & kesintisiz): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span><span class="sxs-lookup"><span data-stu-id="8c9ea-210">PlayReady LA_URL (DASH & smooth): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span></span> 

### <a name="sample-3"></a><span data-ttu-id="8c9ea-211">Örnek 3</span><span class="sxs-lookup"><span data-stu-id="8c9ea-211">Sample 3</span></span>

* <span data-ttu-id="8c9ea-212">Kaynak URL: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="8c9ea-212">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="8c9ea-213">PlayReady LA_URL (tire & kesintisiz): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="8c9ea-213">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 

### <a name="sample-4"></a><span data-ttu-id="8c9ea-214">Örnek 4</span><span class="sxs-lookup"><span data-stu-id="8c9ea-214">Sample 4</span></span>

* <span data-ttu-id="8c9ea-215">Kaynak URL: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="8c9ea-215">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="8c9ea-216">PlayReady LA_URL (tire & kesintisiz): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span><span class="sxs-lookup"><span data-stu-id="8c9ea-216">PlayReady LA_URL (DASH & smooth): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span></span> 

## <a name="summary"></a><span data-ttu-id="8c9ea-217">Özet</span><span class="sxs-lookup"><span data-stu-id="8c9ea-217">Summary</span></span>

<span data-ttu-id="8c9ea-218">Özet olarak, Azure Media Services DRM bileşenlerini esnektir, bunları bir karma senaryoda düzgün içerik anahtarı ve varlık teslim ilkesini yapılandırarak bu konu başlığı altında açıklandığı gibi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-218">In summary, Azure Media Services DRM components are flexible, you can use them in a hybrid scenario by properly configuring content key and asset delivery policy, as described in this topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c9ea-219">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8c9ea-219">Next steps</span></span>
<span data-ttu-id="8c9ea-220">Görünüm Media Services'i öğrenme yolları.</span><span class="sxs-lookup"><span data-stu-id="8c9ea-220">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8c9ea-221">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="8c9ea-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

