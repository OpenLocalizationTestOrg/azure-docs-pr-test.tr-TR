---
title: "aaaAzure Media Services giriş meta veri şema | Microsoft Docs"
description: "Merhaba konu Azure Media Services giriş meta veri şema genel bir bakış sağlar."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d72848e2-4b65-4c84-94bc-e2a90a6e7f47
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 9b72c6ff317aa98451ea75548465dc6023b44a55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="input-metadata"></a><span data-ttu-id="09658-103">Meta veri girişi</span><span class="sxs-lookup"><span data-stu-id="09658-103">Input Metadata</span></span>
<span data-ttu-id="09658-104">Kodlama işinin bir giriş varlık (veya varlıklar) ile ilişkili istediğiniz tooperform kodlama bazı görevler.</span><span class="sxs-lookup"><span data-stu-id="09658-104">An encoding job is associated with an input asset (or assets) on which you want tooperform some encoding tasks.</span></span>  <span data-ttu-id="09658-105">Bir görev tamamlandığında, çıkış varlık oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="09658-105">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="09658-106">video, ses, küçük resimleri, bildirim Hello çıkış varlık içeriyor, vb. hello çıkış varlığına hello giriş varlık hakkındaki meta verileri dosyasıyla de içerir.</span><span class="sxs-lookup"><span data-stu-id="09658-106">hello output asset contains video, audio, thumbnails, manifest, etc. hello output asset also contains a file with metadata about hello input asset.</span></span> <span data-ttu-id="09658-107">Merhaba hello meta veri XML dosyası adına sahip biçimini izleyen hello: &lt;asset_id&gt;_metadata.xml (örneğin, 41114ad3-eb5e - 4c 57-8d 92-5354e2b7d4a4_metadata.xml), burada &lt;asset_id&gt; hello AssetID olduğu Merhaba giriş varlık değeri.</span><span class="sxs-lookup"><span data-stu-id="09658-107">hello name of hello metadata XML file has hello following format: &lt;asset_id&gt;_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where &lt;asset_id&gt; is hello AssetId value of hello input asset.</span></span>  

<span data-ttu-id="09658-108">Tooexamine hello meta veri dosyası istiyorsanız, oluşturabileceğiniz bir **SAS** Bulucu ve indirme hello dosya tooyour yerel bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="09658-108">If you want tooexamine hello metadata file, you can create a **SAS** locator and download hello file tooyour local computer.</span></span> <span data-ttu-id="09658-109">Hakkında bir örnek bulabilirsiniz toocreate bir SAS Bulucu ve dosya indirme [hello Media Services .NET SDK uzantıları kullanarak](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="09658-109">You can find an example on how toocreate a SAS locator and download a file  [Using hello Media Services .NET SDK Extensions](media-services-dotnet-get-started.md).</span></span>  

<span data-ttu-id="09658-110">Bu konuda hangi hello giriş metada ele alınmıştır, hello öğeleri ve hello XML Şeması türleri (&lt;asset_id&gt;_metadata.xml) dayanır.</span><span class="sxs-lookup"><span data-stu-id="09658-110">This topic discusses hello elements and types of hello XML schema on which hello input metada (&lt;asset_id&gt;_metadata.xml) is based.</span></span>  <span data-ttu-id="09658-111">Merhaba çıkış varlık hakkında meta veriler içeren hello dosyası hakkında daha fazla bilgi için bkz: [çıkış meta verileri](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="09658-111">For information about hello file that contains metadata about hello output asset, see [Output Metadata](media-services-output-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="09658-112">Merhaba bulabilirsiniz [şeması kodu](media-services-input-metadata-schema.md#code) bir [XML örneği](media-services-input-metadata-schema.md#xml) hello sonunda bu konuda.</span><span class="sxs-lookup"><span data-stu-id="09658-112">You can find hello [Schema Code](media-services-input-metadata-schema.md#code) an [XML example](media-services-input-metadata-schema.md#xml) at hello end of this topic.</span></span>  
> 
> 

## <span data-ttu-id="09658-113"><a name="AssetFiles"></a>AssetFiles öğesi (kök öğesi)</span><span class="sxs-lookup"><span data-stu-id="09658-113"><a name="AssetFiles"></a> AssetFiles element (root element)</span></span>
<span data-ttu-id="09658-114">Bir koleksiyonu içerir [AssetFile öğesi](media-services-input-metadata-schema.md#AssetFile)hello kodlama işi için s.</span><span class="sxs-lookup"><span data-stu-id="09658-114">Contains a collection of [AssetFile element](media-services-input-metadata-schema.md#AssetFile)s for hello encoding job.</span></span>  

<span data-ttu-id="09658-115">XML örneği hello sonunda bu konuda bkz: [XML örneği](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="09658-115">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

| <span data-ttu-id="09658-116">Ad</span><span class="sxs-lookup"><span data-stu-id="09658-116">Name</span></span> | <span data-ttu-id="09658-117">Açıklama</span><span class="sxs-lookup"><span data-stu-id="09658-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="09658-118">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="09658-118">**AssetFile**</span></span><br /><br /> <span data-ttu-id="09658-119">minOccurs "1" maxOccurs = "unbounded" =</span><span class="sxs-lookup"><span data-stu-id="09658-119">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="09658-120">Tek bir alt öğe.</span><span class="sxs-lookup"><span data-stu-id="09658-120">A single child element.</span></span> <span data-ttu-id="09658-121">Daha fazla bilgi için bkz: [AssetFile öğesi](media-services-input-metadata-schema.md#AssetFile).</span><span class="sxs-lookup"><span data-stu-id="09658-121">For more information, see [AssetFile element](media-services-input-metadata-schema.md#AssetFile).</span></span> |

## <span data-ttu-id="09658-122"><a name="AssetFile"></a>AssetFile öğesi</span><span class="sxs-lookup"><span data-stu-id="09658-122"><a name="AssetFile"></a> AssetFile element</span></span>
 <span data-ttu-id="09658-123">Öznitelikler ve bir varlık dosyası açıklayan öğeler içerir.</span><span class="sxs-lookup"><span data-stu-id="09658-123">Contains attributes and elements that describe an asset file.</span></span>  

 <span data-ttu-id="09658-124">XML örneği hello sonunda bu konuda bkz: [XML örneği](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="09658-124">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="09658-125">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="09658-125">Attributes</span></span>
| <span data-ttu-id="09658-126">Ad</span><span class="sxs-lookup"><span data-stu-id="09658-126">Name</span></span> | <span data-ttu-id="09658-127">Tür</span><span class="sxs-lookup"><span data-stu-id="09658-127">Type</span></span> | <span data-ttu-id="09658-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="09658-128">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="09658-129">**Ad**</span><span class="sxs-lookup"><span data-stu-id="09658-129">**Name**</span></span><br /><br /> <span data-ttu-id="09658-130">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-130">Required</span></span> |<span data-ttu-id="09658-131">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="09658-131">**xs:string**</span></span> |<span data-ttu-id="09658-132">Varlık dosya adı.</span><span class="sxs-lookup"><span data-stu-id="09658-132">Asset file name.</span></span> |
| <span data-ttu-id="09658-133">**Boyut**</span><span class="sxs-lookup"><span data-stu-id="09658-133">**Size**</span></span><br /><br /> <span data-ttu-id="09658-134">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-134">Required</span></span> |<span data-ttu-id="09658-135">**xs:Long**</span><span class="sxs-lookup"><span data-stu-id="09658-135">**xs:long**</span></span> |<span data-ttu-id="09658-136">Merhaba varlık dosyasının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="09658-136">Size of hello asset file in bytes.</span></span> |
| <span data-ttu-id="09658-137">**Süre**</span><span class="sxs-lookup"><span data-stu-id="09658-137">**Duration**</span></span><br /><br /> <span data-ttu-id="09658-138">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-138">Required</span></span> |<span data-ttu-id="09658-139">**xs: Duration**</span><span class="sxs-lookup"><span data-stu-id="09658-139">**xs:duration**</span></span> |<span data-ttu-id="09658-140">İçerik play geri süresi.</span><span class="sxs-lookup"><span data-stu-id="09658-140">Content play back duration.</span></span> <span data-ttu-id="09658-141">Örnek: Süre = "PT25M37.757S".</span><span class="sxs-lookup"><span data-stu-id="09658-141">Example: Duration="PT25M37.757S".</span></span> |
| <span data-ttu-id="09658-142">**NumberOfStreams**</span><span class="sxs-lookup"><span data-stu-id="09658-142">**NumberOfStreams**</span></span><br /><br /> <span data-ttu-id="09658-143">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-143">Required</span></span> |<span data-ttu-id="09658-144">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-144">**xs:int**</span></span> |<span data-ttu-id="09658-145">Merhaba varlık dosyası akış sayısı.</span><span class="sxs-lookup"><span data-stu-id="09658-145">Number of streams in hello asset file.</span></span> |
| <span data-ttu-id="09658-146">**FormatNames**</span><span class="sxs-lookup"><span data-stu-id="09658-146">**FormatNames**</span></span><br /><br /> <span data-ttu-id="09658-147">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-147">Required</span></span> |<span data-ttu-id="09658-148">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="09658-148">**xs:string**</span></span> |<span data-ttu-id="09658-149">Biçim adları.</span><span class="sxs-lookup"><span data-stu-id="09658-149">Format names.</span></span> |
| <span data-ttu-id="09658-150">**FormatVerboseNames**</span><span class="sxs-lookup"><span data-stu-id="09658-150">**FormatVerboseNames**</span></span><br /><br /> <span data-ttu-id="09658-151">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-151">Required</span></span> |<span data-ttu-id="09658-152">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="09658-152">**xs:string**</span></span> |<span data-ttu-id="09658-153">Biçim ayrıntılı adları.</span><span class="sxs-lookup"><span data-stu-id="09658-153">Format verbose names.</span></span> |
| <span data-ttu-id="09658-154">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="09658-154">**StartTime**</span></span> |<span data-ttu-id="09658-155">**xs: Duration**</span><span class="sxs-lookup"><span data-stu-id="09658-155">**xs:duration**</span></span> |<span data-ttu-id="09658-156">İçerik başlangıç saati.</span><span class="sxs-lookup"><span data-stu-id="09658-156">Content start time.</span></span> <span data-ttu-id="09658-157">Örnek: StartTime = "PT2.669S".</span><span class="sxs-lookup"><span data-stu-id="09658-157">Example: StartTime="PT2.669S".</span></span> |
| <span data-ttu-id="09658-158">**OverallBitRate**</span><span class="sxs-lookup"><span data-stu-id="09658-158">**OverallBitRate**</span></span> |<span data-ttu-id="09658-159">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-159">**xs:int**</span></span> |<span data-ttu-id="09658-160">Ortalama bit hızı hello varlık dosyasının KB/sn.</span><span class="sxs-lookup"><span data-stu-id="09658-160">Average bitrate of hello asset file in kbps.</span></span> |

> [!NOTE]
> <span data-ttu-id="09658-161">4 alt öğelerini aşağıdaki hello bir sırada yer almalıdır.</span><span class="sxs-lookup"><span data-stu-id="09658-161">hello following 4 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="09658-162">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="09658-162">Child elements</span></span>
| <span data-ttu-id="09658-163">Ad</span><span class="sxs-lookup"><span data-stu-id="09658-163">Name</span></span> | <span data-ttu-id="09658-164">Tür</span><span class="sxs-lookup"><span data-stu-id="09658-164">Type</span></span> | <span data-ttu-id="09658-165">Açıklama</span><span class="sxs-lookup"><span data-stu-id="09658-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="09658-166">**Programlar**</span><span class="sxs-lookup"><span data-stu-id="09658-166">**Programs**</span></span><br /><br /> <span data-ttu-id="09658-167">minOccurs = "0"</span><span class="sxs-lookup"><span data-stu-id="09658-167">minOccurs="0"</span></span> | |<span data-ttu-id="09658-168">Tüm koleksiyon [programları öğesi](media-services-input-metadata-schema.md#Programs) hello varlık dosyası MPEG-TS biçiminde olduğunda.</span><span class="sxs-lookup"><span data-stu-id="09658-168">Collection of all [Programs element](media-services-input-metadata-schema.md#Programs) when hello asset file is in MPEG-TS format.</span></span> |
| <span data-ttu-id="09658-169">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="09658-169">**VideoTracks**</span></span><br /><br /> <span data-ttu-id="09658-170">minOccurs = "0"</span><span class="sxs-lookup"><span data-stu-id="09658-170">minOccurs="0"</span></span> | |<span data-ttu-id="09658-171">Her fiziksel varlık dosyası, uygun bir kapsayıcı biçimi, araya eklemeli sıfır veya daha fazla video parçaları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="09658-171">Each physical asset file can contain zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="09658-172">Bu öğe tüm koleksiyonunu içerir [VideoTracks öğesi](media-services-input-metadata-schema.md#VideoTracks) hello varlık dosyası bir parçası.</span><span class="sxs-lookup"><span data-stu-id="09658-172">This element contains a collection of all [VideoTracks element](media-services-input-metadata-schema.md#VideoTracks) that are part of hello asset file.</span></span> |
| <span data-ttu-id="09658-173">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="09658-173">**AudioTracks**</span></span><br /><br /> <span data-ttu-id="09658-174">minOccurs = "0"</span><span class="sxs-lookup"><span data-stu-id="09658-174">minOccurs="0"</span></span> | |<span data-ttu-id="09658-175">Her fiziksel varlık dosyası, uygun bir kapsayıcı biçimi, araya eklemeli sıfır veya daha fazla ses izleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="09658-175">Each physical asset file can contain zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="09658-176">Bu öğe tüm koleksiyonunu içerir [AudioTracks öğesi](media-services-input-metadata-schema.md#AudioTracks) hello varlık dosyası bir parçası.</span><span class="sxs-lookup"><span data-stu-id="09658-176">This element contains a collection of all [AudioTracks element](media-services-input-metadata-schema.md#AudioTracks) that are part of hello asset file.</span></span> |
| <span data-ttu-id="09658-177">**Meta veriler**</span><span class="sxs-lookup"><span data-stu-id="09658-177">**Metadata**</span></span><br /><br /> <span data-ttu-id="09658-178">minOccurs "0" maxOccurs = "unbounded" =</span><span class="sxs-lookup"><span data-stu-id="09658-178">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="09658-179">MetadataType</span><span class="sxs-lookup"><span data-stu-id="09658-179">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="09658-180">Varlık dosyanın meta verilerini key\value dize olarak temsil.</span><span class="sxs-lookup"><span data-stu-id="09658-180">Asset file’s metadata represented as key\value strings.</span></span> <span data-ttu-id="09658-181">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="09658-181">For example:</span></span><br /><br /> <span data-ttu-id="09658-182">**&lt;Meta verilerinin anahtarı "language" value = "eng" = /&gt;**</span><span class="sxs-lookup"><span data-stu-id="09658-182">**&lt;Metadata key="language" value="eng" /&gt;**</span></span> |

## <span data-ttu-id="09658-183"><a name="TrackType"></a>TrackType</span><span class="sxs-lookup"><span data-stu-id="09658-183"><a name="TrackType"></a> TrackType</span></span>
<span data-ttu-id="09658-184">XML örneği hello sonunda bu konuda bkz: [XML örneği](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="09658-184">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="09658-185">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="09658-185">Attributes</span></span>
| <span data-ttu-id="09658-186">Ad</span><span class="sxs-lookup"><span data-stu-id="09658-186">Name</span></span> | <span data-ttu-id="09658-187">Tür</span><span class="sxs-lookup"><span data-stu-id="09658-187">Type</span></span> | <span data-ttu-id="09658-188">Açıklama</span><span class="sxs-lookup"><span data-stu-id="09658-188">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="09658-189">**Kimliği**</span><span class="sxs-lookup"><span data-stu-id="09658-189">**Id**</span></span><br /><br /> <span data-ttu-id="09658-190">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-190">Required</span></span> |<span data-ttu-id="09658-191">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-191">**xs:int**</span></span> |<span data-ttu-id="09658-192">Bu ses veya video izlemeyi sıfır tabanlı dizini.</span><span class="sxs-lookup"><span data-stu-id="09658-192">Zero-based index of this audio or video track.</span></span><br /><br /> <span data-ttu-id="09658-193">Bu mutlaka o hello olarak kullanılan bir MP4 dosyasına TrackID değildir.</span><span class="sxs-lookup"><span data-stu-id="09658-193">This is not necessarily that hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="09658-194">**Codec**</span><span class="sxs-lookup"><span data-stu-id="09658-194">**Codec**</span></span> |<span data-ttu-id="09658-195">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="09658-195">**xs:string**</span></span> |<span data-ttu-id="09658-196">Video İzle codec dizesi.</span><span class="sxs-lookup"><span data-stu-id="09658-196">Video track codec string.</span></span> |
| <span data-ttu-id="09658-197">**CodecLongName**</span><span class="sxs-lookup"><span data-stu-id="09658-197">**CodecLongName**</span></span> |<span data-ttu-id="09658-198">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="09658-198">**xs:string**</span></span> |<span data-ttu-id="09658-199">Ses veya video izleme codec uzun adı.</span><span class="sxs-lookup"><span data-stu-id="09658-199">Audio or video track codec long name.</span></span> |
| <span data-ttu-id="09658-200">**Zaman temeli**</span><span class="sxs-lookup"><span data-stu-id="09658-200">**TimeBase**</span></span><br /><br /> <span data-ttu-id="09658-201">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-201">Required</span></span> |<span data-ttu-id="09658-202">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="09658-202">**xs:string**</span></span> |<span data-ttu-id="09658-203">Süresi tabanı.</span><span class="sxs-lookup"><span data-stu-id="09658-203">Time base.</span></span> <span data-ttu-id="09658-204">Örnek: Zaman temeli "1/48000" =</span><span class="sxs-lookup"><span data-stu-id="09658-204">Example: TimeBase="1/48000"</span></span> |
| <span data-ttu-id="09658-205">**NumberOfFrames**</span><span class="sxs-lookup"><span data-stu-id="09658-205">**NumberOfFrames**</span></span> |<span data-ttu-id="09658-206">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-206">**xs:int**</span></span> |<span data-ttu-id="09658-207">Çerçeve (video parçalar mevcut) sayısı.</span><span class="sxs-lookup"><span data-stu-id="09658-207">Number of frames (present for video tracks).</span></span> |
| <span data-ttu-id="09658-208">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="09658-208">**StartTime**</span></span> |<span data-ttu-id="09658-209">**xs: Duration**</span><span class="sxs-lookup"><span data-stu-id="09658-209">**xs:duration**</span></span> |<span data-ttu-id="09658-210">İzleme başlangıç saati.</span><span class="sxs-lookup"><span data-stu-id="09658-210">Track start time.</span></span> <span data-ttu-id="09658-211">Örnek: StartTime "PT2.669S" =</span><span class="sxs-lookup"><span data-stu-id="09658-211">Example: StartTime="PT2.669S"</span></span> |
| <span data-ttu-id="09658-212">**Süre**</span><span class="sxs-lookup"><span data-stu-id="09658-212">**Duration**</span></span> |<span data-ttu-id="09658-213">**xs: Duration**</span><span class="sxs-lookup"><span data-stu-id="09658-213">**xs:duration**</span></span> |<span data-ttu-id="09658-214">Süre izler.</span><span class="sxs-lookup"><span data-stu-id="09658-214">Track duration.</span></span> <span data-ttu-id="09658-215">Örnek: Süre = "PTSampleFormat M37.757S".</span><span class="sxs-lookup"><span data-stu-id="09658-215">Example: Duration="PTSampleFormat M37.757S".</span></span> |

> [!NOTE]
> <span data-ttu-id="09658-216">2 alt öğelerini aşağıdaki hello bir sırada yer almalıdır.</span><span class="sxs-lookup"><span data-stu-id="09658-216">hello following 2 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="09658-217">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="09658-217">Child elements</span></span>
| <span data-ttu-id="09658-218">Ad</span><span class="sxs-lookup"><span data-stu-id="09658-218">Name</span></span> | <span data-ttu-id="09658-219">Tür</span><span class="sxs-lookup"><span data-stu-id="09658-219">Type</span></span> | <span data-ttu-id="09658-220">Açıklama</span><span class="sxs-lookup"><span data-stu-id="09658-220">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="09658-221">**Değerlendirme**</span><span class="sxs-lookup"><span data-stu-id="09658-221">**Disposition**</span></span><br /><br /> <span data-ttu-id="09658-222">minOccurs = "0" maxOccurs = "1"</span><span class="sxs-lookup"><span data-stu-id="09658-222">minOccurs="0" maxOccurs="1"</span></span> |[<span data-ttu-id="09658-223">StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="09658-223">StreamDispositionType</span></span>](media-services-input-metadata-schema.md#StreamDispositionType) |<span data-ttu-id="09658-224">Sunu bilgileri (örneğin, belirli bir ses izleme görme engelli izleyicilere olup olmadığı) içerir.</span><span class="sxs-lookup"><span data-stu-id="09658-224">Contains presentation information (for example, whether a particular audio track is for visually impaired viewers).</span></span> |
| <span data-ttu-id="09658-225">**Meta veriler**</span><span class="sxs-lookup"><span data-stu-id="09658-225">**Metadata**</span></span><br /><br /> <span data-ttu-id="09658-226">minOccurs "0" maxOccurs = "unbounded" =</span><span class="sxs-lookup"><span data-stu-id="09658-226">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="09658-227">MetadataType</span><span class="sxs-lookup"><span data-stu-id="09658-227">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="09658-228">Kullanılan toohold bilgi çeşitli olabilir genel anahtar/değer dizeleri.</span><span class="sxs-lookup"><span data-stu-id="09658-228">Generic key/value strings that can be used toohold a variety of information.</span></span> <span data-ttu-id="09658-229">Örneğin, anahtar = "dil" değeri "eng" =.</span><span class="sxs-lookup"><span data-stu-id="09658-229">For example, key=”language”, and value=”eng”.</span></span> |

## <span data-ttu-id="09658-230"><a name="AudioTrackType"></a>AudioTrackType (TrackType devralan)</span><span class="sxs-lookup"><span data-stu-id="09658-230"><a name="AudioTrackType"></a> AudioTrackType (inherits from TrackType)</span></span>
 <span data-ttu-id="09658-231">**AudioTrackType** devraldığı genel bir karmaşık tür [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="09658-231">**AudioTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

 <span data-ttu-id="09658-232">belirli bir ses İzle hello varlık dosyası'Hello türünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="09658-232">hello type represents a specific audio track in hello asset file.</span></span>  

 <span data-ttu-id="09658-233">XML örneği hello sonunda bu konuda bkz: [XML örneği](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="09658-233">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="09658-234">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="09658-234">Attributes</span></span>
| <span data-ttu-id="09658-235">Ad</span><span class="sxs-lookup"><span data-stu-id="09658-235">Name</span></span> | <span data-ttu-id="09658-236">Tür</span><span class="sxs-lookup"><span data-stu-id="09658-236">Type</span></span> | <span data-ttu-id="09658-237">Açıklama</span><span class="sxs-lookup"><span data-stu-id="09658-237">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="09658-238">**SampleFormat**</span><span class="sxs-lookup"><span data-stu-id="09658-238">**SampleFormat**</span></span> |<span data-ttu-id="09658-239">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="09658-239">**xs:string**</span></span> |<span data-ttu-id="09658-240">Örnek biçimi.</span><span class="sxs-lookup"><span data-stu-id="09658-240">Sample format.</span></span> |
| <span data-ttu-id="09658-241">**ChannelLayout**</span><span class="sxs-lookup"><span data-stu-id="09658-241">**ChannelLayout**</span></span> |<span data-ttu-id="09658-242">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="09658-242">**xs:string**</span></span> |<span data-ttu-id="09658-243">Kanal düzeni.</span><span class="sxs-lookup"><span data-stu-id="09658-243">Channel layout.</span></span> |
| <span data-ttu-id="09658-244">**Kanalları**</span><span class="sxs-lookup"><span data-stu-id="09658-244">**Channels**</span></span><br /><br /> <span data-ttu-id="09658-245">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-245">Required</span></span> |<span data-ttu-id="09658-246">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-246">**xs:int**</span></span> |<span data-ttu-id="09658-247">(0 veya daha fazla) ses kanal sayısı.</span><span class="sxs-lookup"><span data-stu-id="09658-247">Number (0 or more) of audio channels.</span></span> |
| <span data-ttu-id="09658-248">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="09658-248">**SamplingRate**</span></span><br /><br /> <span data-ttu-id="09658-249">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-249">Required</span></span> |<span data-ttu-id="09658-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-250">**xs:int**</span></span> |<span data-ttu-id="09658-251">Saniye başına örnekleri veya Hz ses örnekleme hızı.</span><span class="sxs-lookup"><span data-stu-id="09658-251">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="09658-252">**Bit hızı**</span><span class="sxs-lookup"><span data-stu-id="09658-252">**Bitrate**</span></span> |<span data-ttu-id="09658-253">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-253">**xs:int**</span></span> |<span data-ttu-id="09658-254">Merhaba varlık dosyasından hesaplanan olarak saniyedeki ortalama ses bit hızı.</span><span class="sxs-lookup"><span data-stu-id="09658-254">Average audio bit rate in bits per second, as calculated from hello asset file.</span></span> <span data-ttu-id="09658-255">Yalnızca hello başlangıç akışı yükü kabul edilir ve bu sayıma hello paketleme yükünü dahil değil.</span><span class="sxs-lookup"><span data-stu-id="09658-255">Only hello elementary stream payload is counted, and hello packaging overhead is not included in this count.</span></span> |
| <span data-ttu-id="09658-256">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="09658-256">**BitsPerSample**</span></span> |<span data-ttu-id="09658-257">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-257">**xs:int**</span></span> |<span data-ttu-id="09658-258">Merhaba wFormatTag biçimi için örnek başına bit yazın.</span><span class="sxs-lookup"><span data-stu-id="09658-258">Bits per sample for hello wFormatTag format type.</span></span> |

## <span data-ttu-id="09658-259"><a name="VideoTrackType"></a>VideoTrackType (TrackType devralan)</span><span class="sxs-lookup"><span data-stu-id="09658-259"><a name="VideoTrackType"></a> VideoTrackType (inherits from TrackType)</span></span>
<span data-ttu-id="09658-260">**VideoTrackType** devraldığı genel bir karmaşık tür [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="09658-260">**VideoTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

<span data-ttu-id="09658-261">belirli bir video izlemek hello varlık dosyasındaki Hello türünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="09658-261">hello type represents a specific video track in hello asset file.</span></span>  

<span data-ttu-id="09658-262">XML örneği hello sonunda bu konuda bkz: [XML örneği](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="09658-262">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="09658-263">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="09658-263">Attributes</span></span>
| <span data-ttu-id="09658-264">Ad</span><span class="sxs-lookup"><span data-stu-id="09658-264">Name</span></span> | <span data-ttu-id="09658-265">Tür</span><span class="sxs-lookup"><span data-stu-id="09658-265">Type</span></span> | <span data-ttu-id="09658-266">Açıklama</span><span class="sxs-lookup"><span data-stu-id="09658-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="09658-267">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="09658-267">**FourCC**</span></span><br /><br /> <span data-ttu-id="09658-268">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-268">Required</span></span> |<span data-ttu-id="09658-269">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="09658-269">**xs:string**</span></span> |<span data-ttu-id="09658-270">Görüntü codec FourCC kodu.</span><span class="sxs-lookup"><span data-stu-id="09658-270">Video codec FourCC code.</span></span> |
| <span data-ttu-id="09658-271">**Profili**</span><span class="sxs-lookup"><span data-stu-id="09658-271">**Profile**</span></span> |<span data-ttu-id="09658-272">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="09658-272">**xs:string**</span></span> |<span data-ttu-id="09658-273">Video parçasının profili.</span><span class="sxs-lookup"><span data-stu-id="09658-273">Video track's profile.</span></span> |
| <span data-ttu-id="09658-274">**Düzeyi**</span><span class="sxs-lookup"><span data-stu-id="09658-274">**Level**</span></span> |<span data-ttu-id="09658-275">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="09658-275">**xs:string**</span></span> |<span data-ttu-id="09658-276">Video parçasının düzeyi.</span><span class="sxs-lookup"><span data-stu-id="09658-276">Video track's level.</span></span> |
| <span data-ttu-id="09658-277">**PixelFormat**</span><span class="sxs-lookup"><span data-stu-id="09658-277">**PixelFormat**</span></span> |<span data-ttu-id="09658-278">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="09658-278">**xs:string**</span></span> |<span data-ttu-id="09658-279">Video parçasının piksel biçimi.</span><span class="sxs-lookup"><span data-stu-id="09658-279">Video track's pixel format.</span></span> |
| <span data-ttu-id="09658-280">**Genişlik**</span><span class="sxs-lookup"><span data-stu-id="09658-280">**Width**</span></span><br /><br /> <span data-ttu-id="09658-281">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-281">Required</span></span> |<span data-ttu-id="09658-282">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-282">**xs:int**</span></span> |<span data-ttu-id="09658-283">Kodlanmış video genişliğini piksel cinsinden.</span><span class="sxs-lookup"><span data-stu-id="09658-283">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="09658-284">**Yükseklik**</span><span class="sxs-lookup"><span data-stu-id="09658-284">**Height**</span></span><br /><br /> <span data-ttu-id="09658-285">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-285">Required</span></span> |<span data-ttu-id="09658-286">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-286">**xs:int**</span></span> |<span data-ttu-id="09658-287">Piksel cinsinden görüntü yüksekliği kodlanmış.</span><span class="sxs-lookup"><span data-stu-id="09658-287">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="09658-288">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="09658-288">**DisplayAspectRatioNumerator**</span></span><br /><br /> <span data-ttu-id="09658-289">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-289">Required</span></span> |<span data-ttu-id="09658-290">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="09658-290">**xs:double**</span></span> |<span data-ttu-id="09658-291">Video görüntü en boy oranını pay.</span><span class="sxs-lookup"><span data-stu-id="09658-291">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="09658-292">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="09658-292">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="09658-293">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-293">Required</span></span> |<span data-ttu-id="09658-294">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="09658-294">**xs:double**</span></span> |<span data-ttu-id="09658-295">Video görüntü en boy oranını payda.</span><span class="sxs-lookup"><span data-stu-id="09658-295">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="09658-296">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="09658-296">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="09658-297">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-297">Required</span></span> |<span data-ttu-id="09658-298">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="09658-298">**xs:double**</span></span> |<span data-ttu-id="09658-299">Video örneği en boy oranını pay.</span><span class="sxs-lookup"><span data-stu-id="09658-299">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="09658-300">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="09658-300">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="09658-301">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="09658-301">**xs:double**</span></span> |<span data-ttu-id="09658-302">Video örneği en boy oranını pay.</span><span class="sxs-lookup"><span data-stu-id="09658-302">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="09658-303">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="09658-303">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="09658-304">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="09658-304">**xs:double**</span></span> |<span data-ttu-id="09658-305">Video örneği en boy oranını payda.</span><span class="sxs-lookup"><span data-stu-id="09658-305">Video sample aspect ratio denominator.</span></span> |
| <span data-ttu-id="09658-306">**Kare hızı**</span><span class="sxs-lookup"><span data-stu-id="09658-306">**FrameRate**</span></span><br /><br /> <span data-ttu-id="09658-307">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-307">Required</span></span> |<span data-ttu-id="09658-308">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="09658-308">**xs:decimal**</span></span> |<span data-ttu-id="09658-309">Video kare hızı .3f biçiminde ölçülür.</span><span class="sxs-lookup"><span data-stu-id="09658-309">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="09658-310">**Bit hızı**</span><span class="sxs-lookup"><span data-stu-id="09658-310">**Bitrate**</span></span> |<span data-ttu-id="09658-311">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-311">**xs:int**</span></span> |<span data-ttu-id="09658-312">Ortalama video bit hızı hello varlık dosyasından hesaplanan olarak kilobit / saniye.</span><span class="sxs-lookup"><span data-stu-id="09658-312">Average video bit rate in kilobits per second, as calculated from hello asset file.</span></span> <span data-ttu-id="09658-313">Yalnızca hello başlangıç akışı yükü kabul edilir ve hello paketleme ek yük dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="09658-313">Only hello elementary stream payload is counted, and hello packaging overhead is not included.</span></span> |
| <span data-ttu-id="09658-314">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="09658-314">**MaxGOPBitrate**</span></span> |<span data-ttu-id="09658-315">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-315">**xs:int**</span></span> |<span data-ttu-id="09658-316">Max GOP ortalama bit hızı kilobit bu video izlemek için.</span><span class="sxs-lookup"><span data-stu-id="09658-316">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |
| <span data-ttu-id="09658-317">**HasBFrames**</span><span class="sxs-lookup"><span data-stu-id="09658-317">**HasBFrames**</span></span> |<span data-ttu-id="09658-318">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-318">**xs:int**</span></span> |<span data-ttu-id="09658-319">Video parça B çerçeve sayısı.</span><span class="sxs-lookup"><span data-stu-id="09658-319">Video track number of B frames.</span></span> |

## <span data-ttu-id="09658-320"><a name="MetadataType"></a>MetadataType</span><span class="sxs-lookup"><span data-stu-id="09658-320"><a name="MetadataType"></a> MetadataType</span></span>
<span data-ttu-id="09658-321">**MetadataType** anahtar/değer dize olarak bir varlık dosya meta verileri tanımlayan genel bir karmaşık türü.</span><span class="sxs-lookup"><span data-stu-id="09658-321">**MetadataType** is a global complex type that describes metadata of an asset file as key/value strings.</span></span> <span data-ttu-id="09658-322">Örneğin, anahtar = "dil" değeri "eng" =.</span><span class="sxs-lookup"><span data-stu-id="09658-322">For example, key=”language”, and value=”eng”.</span></span>  

<span data-ttu-id="09658-323">XML örneği hello sonunda bu konuda bkz: [XML örneği](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="09658-323">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="09658-324">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="09658-324">Attributes</span></span>
| <span data-ttu-id="09658-325">Ad</span><span class="sxs-lookup"><span data-stu-id="09658-325">Name</span></span> | <span data-ttu-id="09658-326">Tür</span><span class="sxs-lookup"><span data-stu-id="09658-326">Type</span></span> | <span data-ttu-id="09658-327">Açıklama</span><span class="sxs-lookup"><span data-stu-id="09658-327">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="09658-328">**anahtarı**</span><span class="sxs-lookup"><span data-stu-id="09658-328">**key**</span></span><br /><br /> <span data-ttu-id="09658-329">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-329">Required</span></span> |<span data-ttu-id="09658-330">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="09658-330">**xs:string**</span></span> |<span data-ttu-id="09658-331">Merhaba anahtar/değer çifti Hello anahtar.</span><span class="sxs-lookup"><span data-stu-id="09658-331">hello key in hello key/value pair.</span></span> |
| <span data-ttu-id="09658-332">**değer**</span><span class="sxs-lookup"><span data-stu-id="09658-332">**value**</span></span><br /><br /> <span data-ttu-id="09658-333">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-333">Required</span></span> |<span data-ttu-id="09658-334">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="09658-334">**xs:string**</span></span> |<span data-ttu-id="09658-335">Merhaba anahtar/değer çifti Hello değeri.</span><span class="sxs-lookup"><span data-stu-id="09658-335">hello value in hello key/value pair.</span></span> |

## <span data-ttu-id="09658-336"><a name="ProgramType"></a>ProgramType</span><span class="sxs-lookup"><span data-stu-id="09658-336"><a name="ProgramType"></a> ProgramType</span></span>
<span data-ttu-id="09658-337">**ProgramType** bir programı anlatır genel bir karmaşık tür.</span><span class="sxs-lookup"><span data-stu-id="09658-337">**ProgramType** is a global complex type that describes a program.</span></span>  

### <a name="attributes"></a><span data-ttu-id="09658-338">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="09658-338">Attributes</span></span>
| <span data-ttu-id="09658-339">Ad</span><span class="sxs-lookup"><span data-stu-id="09658-339">Name</span></span> | <span data-ttu-id="09658-340">Tür</span><span class="sxs-lookup"><span data-stu-id="09658-340">Type</span></span> | <span data-ttu-id="09658-341">Açıklama</span><span class="sxs-lookup"><span data-stu-id="09658-341">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="09658-342">**ProgramId**</span><span class="sxs-lookup"><span data-stu-id="09658-342">**ProgramId**</span></span><br /><br /> <span data-ttu-id="09658-343">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-343">Required</span></span> |<span data-ttu-id="09658-344">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-344">**xs:int**</span></span> |<span data-ttu-id="09658-345">Program Kimliği</span><span class="sxs-lookup"><span data-stu-id="09658-345">Program Id</span></span> |
| <span data-ttu-id="09658-346">**NumberOfPrograms**</span><span class="sxs-lookup"><span data-stu-id="09658-346">**NumberOfPrograms**</span></span><br /><br /> <span data-ttu-id="09658-347">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-347">Required</span></span> |<span data-ttu-id="09658-348">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-348">**xs:int**</span></span> |<span data-ttu-id="09658-349">Programları sayısı.</span><span class="sxs-lookup"><span data-stu-id="09658-349">Number of programs.</span></span> |
| <span data-ttu-id="09658-350">**PmtPid**</span><span class="sxs-lookup"><span data-stu-id="09658-350">**PmtPid**</span></span><br /><br /> <span data-ttu-id="09658-351">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-351">Required</span></span> |<span data-ttu-id="09658-352">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-352">**xs:int**</span></span> |<span data-ttu-id="09658-353">Program eşleme tabloları (PMTs) programlar hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="09658-353">Program Map Tables (PMTs) contain information about programs.</span></span>  <span data-ttu-id="09658-354">Daha fazla bilgi için bkz: [DEVRESEL_ÖDEME](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span><span class="sxs-lookup"><span data-stu-id="09658-354">For more information, see [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span></span> |
| <span data-ttu-id="09658-355">**PcrPid**</span><span class="sxs-lookup"><span data-stu-id="09658-355">**PcrPid**</span></span><br /><br /> <span data-ttu-id="09658-356">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-356">Required</span></span> |<span data-ttu-id="09658-357">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-357">**xs:int**</span></span> |<span data-ttu-id="09658-358">Kod Çözücü tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="09658-358">Used by decoder.</span></span> <span data-ttu-id="09658-359">Daha fazla bilgi için bkz: [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span><span class="sxs-lookup"><span data-stu-id="09658-359">For more information, see [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span></span> |
| <span data-ttu-id="09658-360">**StartPTS**</span><span class="sxs-lookup"><span data-stu-id="09658-360">**StartPTS**</span></span> |<span data-ttu-id="09658-361">**xs: uzun**</span><span class="sxs-lookup"><span data-stu-id="09658-361">**xs: long**</span></span> |<span data-ttu-id="09658-362">Sunu zaman damgası başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="09658-362">Starting presentation time stamp.</span></span> |
| <span data-ttu-id="09658-363">**EndPTS**</span><span class="sxs-lookup"><span data-stu-id="09658-363">**EndPTS**</span></span> |<span data-ttu-id="09658-364">**xs: uzun**</span><span class="sxs-lookup"><span data-stu-id="09658-364">**xs: long**</span></span> |<span data-ttu-id="09658-365">Bitiş sunu zaman damgası.</span><span class="sxs-lookup"><span data-stu-id="09658-365">Ending presentation time stamp.</span></span> |

## <span data-ttu-id="09658-366"><a name="StreamDispositionType"></a>StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="09658-366"><a name="StreamDispositionType"></a> StreamDispositionType</span></span>
<span data-ttu-id="09658-367">**StreamDispositionType** hello akışı açıklanır genel bir karmaşık tür.</span><span class="sxs-lookup"><span data-stu-id="09658-367">**StreamDispositionType** is a global complex type that describes hello stream.</span></span>  

<span data-ttu-id="09658-368">XML örneği hello sonunda bu konuda bkz: [XML örneği](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="09658-368">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="09658-369">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="09658-369">Attributes</span></span>
| <span data-ttu-id="09658-370">Ad</span><span class="sxs-lookup"><span data-stu-id="09658-370">Name</span></span> | <span data-ttu-id="09658-371">Tür</span><span class="sxs-lookup"><span data-stu-id="09658-371">Type</span></span> | <span data-ttu-id="09658-372">Açıklama</span><span class="sxs-lookup"><span data-stu-id="09658-372">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="09658-373">**Varsayılan**</span><span class="sxs-lookup"><span data-stu-id="09658-373">**Default**</span></span><br /><br /> <span data-ttu-id="09658-374">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-374">Required</span></span> |<span data-ttu-id="09658-375">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-375">**xs:int**</span></span> |<span data-ttu-id="09658-376">Bu öznitelik too1 tooindicate bu hello varsayılan sunu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="09658-376">Set this attribute too1 tooindicate this is hello default presentation.</span></span> |
| <span data-ttu-id="09658-377">**Dub**</span><span class="sxs-lookup"><span data-stu-id="09658-377">**Dub**</span></span><br /><br /> <span data-ttu-id="09658-378">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-378">Required</span></span> |<span data-ttu-id="09658-379">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-379">**xs:int**</span></span> |<span data-ttu-id="09658-380">Bu öznitelik too1 tooindicate ayarlamanız hello sunu Dublaj.</span><span class="sxs-lookup"><span data-stu-id="09658-380">Set this attribute too1 tooindicate this is hello dubbed presentation.</span></span> |
| <span data-ttu-id="09658-381">**Özgün**</span><span class="sxs-lookup"><span data-stu-id="09658-381">**Original**</span></span><br /><br /> <span data-ttu-id="09658-382">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-382">Required</span></span> |<span data-ttu-id="09658-383">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-383">**xs:int**</span></span> |<span data-ttu-id="09658-384">Bu öznitelik too1 tooindicate bu hello özgün sunu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="09658-384">Set this attribute too1 tooindicate this is hello original presentation.</span></span> |
| <span data-ttu-id="09658-385">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="09658-385">**Comment**</span></span><br /><br /> <span data-ttu-id="09658-386">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-386">Required</span></span> |<span data-ttu-id="09658-387">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-387">**xs:int**</span></span> |<span data-ttu-id="09658-388">Bu öznitelik too1 tooindicate ayarlamanız izleme yorumlar içerir.</span><span class="sxs-lookup"><span data-stu-id="09658-388">Set this attribute too1 tooindicate this track contains commentary.</span></span> |
| <span data-ttu-id="09658-389">**Sözleri**</span><span class="sxs-lookup"><span data-stu-id="09658-389">**Lyrics**</span></span><br /><br /> <span data-ttu-id="09658-390">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-390">Required</span></span> |<span data-ttu-id="09658-391">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-391">**xs:int**</span></span> |<span data-ttu-id="09658-392">Bu öznitelik too1 tooindicate ayarlamanız izleme sözleri içerir.</span><span class="sxs-lookup"><span data-stu-id="09658-392">Set this attribute too1 tooindicate this track contains lyrics.</span></span> |
| <span data-ttu-id="09658-393">**Karaoke**</span><span class="sxs-lookup"><span data-stu-id="09658-393">**Karaoke**</span></span><br /><br /> <span data-ttu-id="09658-394">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-394">Required</span></span> |<span data-ttu-id="09658-395">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-395">**xs:int**</span></span> |<span data-ttu-id="09658-396">Bu öznitelik too1 tooindicate ayarlamanız hello karaoke İzle (arka plan müzik, hiçbir vokallerle) temsil eder.</span><span class="sxs-lookup"><span data-stu-id="09658-396">Set this attribute too1 tooindicate this represents hello karaoke track (background music, no vocals).</span></span> |
| <span data-ttu-id="09658-397">**Zorla**</span><span class="sxs-lookup"><span data-stu-id="09658-397">**Forced**</span></span><br /><br /> <span data-ttu-id="09658-398">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-398">Required</span></span> |<span data-ttu-id="09658-399">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-399">**xs:int**</span></span> |<span data-ttu-id="09658-400">Bu öznitelik too1 tooindicate bu zorunlu hello sunu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="09658-400">Set this attribute too1 tooindicate this is hello forced presentation.</span></span> |
| <span data-ttu-id="09658-401">**HearingImpaired**</span><span class="sxs-lookup"><span data-stu-id="09658-401">**HearingImpaired**</span></span><br /><br /> <span data-ttu-id="09658-402">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-402">Required</span></span> |<span data-ttu-id="09658-403">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-403">**xs:int**</span></span> |<span data-ttu-id="09658-404">Bu izleme için hello işitme engelli olduğundan bu öznitelik too1 tooindicate ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="09658-404">Set this attribute too1 tooindicate this track is for hello hearing impaired.</span></span> |
| <span data-ttu-id="09658-405">**VisualImpaired**</span><span class="sxs-lookup"><span data-stu-id="09658-405">**VisualImpaired**</span></span><br /><br /> <span data-ttu-id="09658-406">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-406">Required</span></span> |<span data-ttu-id="09658-407">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-407">**xs:int**</span></span> |<span data-ttu-id="09658-408">Bu izleme görme engelli hello için olan bu öznitelik too1 tooindicate ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="09658-408">Set this attribute too1 tooindicate this track is for hello visually impaired.</span></span> |
| <span data-ttu-id="09658-409">**CleanEffects**</span><span class="sxs-lookup"><span data-stu-id="09658-409">**CleanEffects**</span></span><br /><br /> <span data-ttu-id="09658-410">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-410">Required</span></span> |<span data-ttu-id="09658-411">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-411">**xs:int**</span></span> |<span data-ttu-id="09658-412">Bu izi varsa bu öznitelik too1 tooindicate temiz etkileri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="09658-412">Set this attribute too1 tooindicate this track has clean effects.</span></span> |
| <span data-ttu-id="09658-413">**AttachedPic**</span><span class="sxs-lookup"><span data-stu-id="09658-413">**AttachedPic**</span></span><br /><br /> <span data-ttu-id="09658-414">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09658-414">Required</span></span> |<span data-ttu-id="09658-415">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="09658-415">**xs:int**</span></span> |<span data-ttu-id="09658-416">Bu izi varsa bu öznitelik too1 tooindicate resimleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="09658-416">Set this attribute too1 tooindicate this track has pictures.</span></span> |

## <span data-ttu-id="09658-417"><a name="Programs"></a>Programları öğesi</span><span class="sxs-lookup"><span data-stu-id="09658-417"><a name="Programs"></a> Programs element</span></span>
<span data-ttu-id="09658-418">Birden çok tutan kapsayıcı öğe **Program** öğeleri.</span><span class="sxs-lookup"><span data-stu-id="09658-418">Wrapper element holding multiple **Program** elements.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="09658-419">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="09658-419">Child elements</span></span>
| <span data-ttu-id="09658-420">Ad</span><span class="sxs-lookup"><span data-stu-id="09658-420">Name</span></span> | <span data-ttu-id="09658-421">Tür</span><span class="sxs-lookup"><span data-stu-id="09658-421">Type</span></span> | <span data-ttu-id="09658-422">Açıklama</span><span class="sxs-lookup"><span data-stu-id="09658-422">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="09658-423">**Program**</span><span class="sxs-lookup"><span data-stu-id="09658-423">**Program**</span></span><br /><br /> <span data-ttu-id="09658-424">minOccurs "0" maxOccurs = "unbounded" =</span><span class="sxs-lookup"><span data-stu-id="09658-424">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="09658-425">ProgramType</span><span class="sxs-lookup"><span data-stu-id="09658-425">ProgramType</span></span>](media-services-input-metadata-schema.md#ProgramType) |<span data-ttu-id="09658-426">MPEG-TS biçimindeki varlık dosyaları için hello varlık dosyasındaki programlar hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="09658-426">For asset files that are in MPEG-TS format, contains information about programs in hello asset file.</span></span> |

## <span data-ttu-id="09658-427"><a name="VideoTracks"></a>VideoTracks öğesi</span><span class="sxs-lookup"><span data-stu-id="09658-427"><a name="VideoTracks"></a> VideoTracks element</span></span>
 <span data-ttu-id="09658-428">Birden çok tutan kapsayıcı öğe **VideoTrack** öğeleri.</span><span class="sxs-lookup"><span data-stu-id="09658-428">Wrapper element holding multiple **VideoTrack** elements.</span></span>  

 <span data-ttu-id="09658-429">XML örneği hello sonunda bu konuda bkz: [XML örneği](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="09658-429">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="09658-430">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="09658-430">Child elements</span></span>
| <span data-ttu-id="09658-431">Ad</span><span class="sxs-lookup"><span data-stu-id="09658-431">Name</span></span> | <span data-ttu-id="09658-432">Tür</span><span class="sxs-lookup"><span data-stu-id="09658-432">Type</span></span> | <span data-ttu-id="09658-433">Açıklama</span><span class="sxs-lookup"><span data-stu-id="09658-433">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="09658-434">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="09658-434">**VideoTrack**</span></span><br /><br /> <span data-ttu-id="09658-435">minOccurs "0" maxOccurs = "unbounded" =</span><span class="sxs-lookup"><span data-stu-id="09658-435">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="09658-436">VideoTrackType (TrackType devralan)</span><span class="sxs-lookup"><span data-stu-id="09658-436">VideoTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#VideoTrackType) |<span data-ttu-id="09658-437">Merhaba varlık dosyasındaki video parçaları hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="09658-437">Contains information about video tracks in hello asset file.</span></span> |

## <span data-ttu-id="09658-438"><a name="AudioTracks"></a>AudioTracks öğesi</span><span class="sxs-lookup"><span data-stu-id="09658-438"><a name="AudioTracks"></a> AudioTracks element</span></span>
 <span data-ttu-id="09658-439">Birden çok tutan kapsayıcı öğe **AudioTrack** öğeleri.</span><span class="sxs-lookup"><span data-stu-id="09658-439">Wrapper element holding multiple **AudioTrack** elements.</span></span>  

 <span data-ttu-id="09658-440">XML örneği hello sonunda bu konuda bkz: [XML örneği](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="09658-440">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="elements"></a><span data-ttu-id="09658-441">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="09658-441">elements</span></span>
| <span data-ttu-id="09658-442">Ad</span><span class="sxs-lookup"><span data-stu-id="09658-442">Name</span></span> | <span data-ttu-id="09658-443">Tür</span><span class="sxs-lookup"><span data-stu-id="09658-443">Type</span></span> | <span data-ttu-id="09658-444">Açıklama</span><span class="sxs-lookup"><span data-stu-id="09658-444">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="09658-445">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="09658-445">**AudioTrack**</span></span><br /><br /> <span data-ttu-id="09658-446">minOccurs "0" maxOccurs = "unbounded" =</span><span class="sxs-lookup"><span data-stu-id="09658-446">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="09658-447">AudioTrackType (TrackType devralan)</span><span class="sxs-lookup"><span data-stu-id="09658-447">AudioTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#AudioTrackType) |<span data-ttu-id="09658-448">Merhaba varlık dosyasındaki ses izleri hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="09658-448">Contains information about audio tracks in hello asset file.</span></span> |

## <span data-ttu-id="09658-449"><a name="code"></a>Şema kodu</span><span class="sxs-lookup"><span data-stu-id="09658-449"><a name="code"></a> Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.0"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               elementFormDefault="qualified">  

      <xs:complexType name="MetadataType">  
        <xs:attribute name="key"   type="xs:string" use="required"/>  
        <xs:attribute name="value" type="xs:string" use="required"/>  
      </xs:complexType>  

      <xs:complexType name="ProgramType">  
        <xs:attribute name="ProgramId" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Program Id</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfPrograms" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Number of programs</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PmtPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pmt pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PcrPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pcr pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="StartPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>start pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="EndPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>end pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="StreamDispositionType">  
        <xs:attribute name="Default"          type="xs:int" use="required" />  
        <xs:attribute name="Dub"              type="xs:int" use="required" />  
        <xs:attribute name="Original"         type="xs:int" use="required" />  
        <xs:attribute name="Comment"          type="xs:int" use="required" />  
        <xs:attribute name="Lyrics"           type="xs:int" use="required" />  
        <xs:attribute name="Karaoke"          type="xs:int" use="required" />  
        <xs:attribute name="Forced"           type="xs:int" use="required" />  
        <xs:attribute name="HearingImpaired"  type="xs:int" use="required" />  
        <xs:attribute name="VisualImpaired"   type="xs:int" use="required" />  
        <xs:attribute name="CleanEffects"     type="xs:int" use="required" />  
        <xs:attribute name="AttachedPic"      type="xs:int" use="required" />  
      </xs:complexType>  

      <xs:complexType name="TrackType" abstract="true">  
        <xs:sequence>  
          <xs:element name="Disposition" type="StreamDispositionType" minOccurs="0" maxOccurs="1"/>  
          <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded"/>  
        </xs:sequence>  
        <xs:attribute name="Id" use="required">  
          <xs:annotation>  
            <xs:documentation>zero-based index of this video track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="Codec" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec string</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="CodecLongName" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec long name</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="TimeBase"  type="xs:string" use="required">  
          <xs:annotation>  
            <xs:documentation>Time base. Example: TimeBase="1/48000"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfFrames">  
          <xs:annotation>  
            <xs:documentation>number of frames</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="StartTime" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track start time. Example: StartTime="PT2.669S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="Duration" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track duration. Example: Duration="PT25M37.757S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="VideoTrackType">  
        <xs:annotation>  
          <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="FourCC" type="xs:string" use="required">  
              <xs:annotation>  
                <xs:documentation>video codec FourCC code</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Profile" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>profile</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Level" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>level</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="PixelFormat" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>Video track's pixel format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Width" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video width in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Height" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video height in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioNumerator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioDenominator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioNumerator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioDenominator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="FrameRate" use="required">  
              <xs:annotation>  
                <xs:documentation>measured video frame rate in .3f format</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:decimal">  
                  <xs:minInclusive value="0"/>  
                  <xs:fractionDigits value="3"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="MaxGOPBitrate">  
              <xs:annotation>  
                <xs:documentation>Max GOP average bitrate for this video track, in kilobits per second</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="HasBFrames" type="xs:int">  
              <xs:annotation>  
                <xs:documentation>video track number of B frames</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:complexType name="AudioTrackType">  
        <xs:annotation>  
          <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="SampleFormat"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>sample format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="ChannelLayout"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>channel layout</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Channels" use="required">  
              <xs:annotation>  
                <xs:documentation>number of audio channels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SamplingRate" use="required">  
              <xs:annotation>  
                <xs:documentation>audio sampling rate in samples/sec or Hz</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for hello encoding job</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="AssetFile" minOccurs="1" maxOccurs="unbounded">  
              <xs:annotation>  
                <xs:documentation>asset file</xs:documentation>  
              </xs:annotation>  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="Programs" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>This is hello collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" type="AudioTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded" />  
                </xs:sequence>  
                <xs:attribute name="Name" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>hello media asset file name</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Size" use="required">  
                  <xs:annotation>  
                    <xs:documentation>size of file in bytes</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:long">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
                <xs:attribute name="Duration" type="xs:duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration. Example: Duration="PT25M37.757S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="NumberOfStreams" type="xs:int" use="required">  
                  <xs:annotation>  
                    <xs:documentation>number of streams in asset file</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatNames" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatVerboseName" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format verbose names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="StartTime" type="xs:duration">  
                  <xs:annotation>  
                    <xs:documentation>content start time. Example: StartTime="PT2.669S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="OverallBitRate">  
                  <xs:annotation>  
                    <xs:documentation>average bitrate of hello asset file in kbps</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:int">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  


## <span data-ttu-id="09658-450"><a name="xml"></a>XML örneği</span><span class="sxs-lookup"><span data-stu-id="09658-450"><a name="xml"></a> XML example</span></span>
<span data-ttu-id="09658-451">Merhaba, hello giriş meta veri dosyası örneği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="09658-451">hello following is an example of hello Input metadata file.</span></span>  

    <?xml version="1.0" encoding="utf-8"?>  
    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata">  
      <AssetFile Name="bear.mp4" Size="1973733" Duration="PT12.678S" NumberOfStreams="2" FormatNames="mov,mp4,m4a,3gp,3g2,mj2" FormatVerboseName="QuickTime / MOV" StartTime="PT0S" OverallBitRate="1245">  
        <VideoTracks>  
          <VideoTrack Id="1" Codec="h264" CodecLongName="H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10" TimeBase="1/29970" NumberOfFrames="375" StartTime="PT0.034S" Duration="PT12.645S" FourCC="avc1" Profile="High" Level="4.1" PixelFormat="yuv420p" Width="512" Height="384" DisplayAspectRatioNumerator="4" DisplayAspectRatioDenominator="3" SampleAspectRatioNumerator="1" SampleAspectRatioDenominator="1" FrameRate="29.656" Bitrate="1043" HasBFrames="1">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Video Media Handler" />  
          </VideoTrack>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="aac" CodecLongName="AAC (Advanced Audio Coding)" TimeBase="1/44100" NumberOfFrames="546" StartTime="PT0S" Duration="PT12.678S" SampleFormat="fltp" ChannelLayout="stereo" Channels="2" SamplingRate="44100" Bitrate="156" BitsPerSample="0">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Sound Media Handler" />  
          </AudioTrack>  
        </AudioTracks>  
        <Metadata key="major_brand" value="mp42" />  
        <Metadata key="minor_version" value="0" />  
        <Metadata key="compatible_brands" value="mp42mp41" />  
        <Metadata key="creation_time" value="2010-03-10 16:11:53" />  
        <Metadata key="comment" value="Courtesy of National Geographic.  Used by Permission." />  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a><span data-ttu-id="09658-452">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="09658-452">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="09658-453">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="09658-453">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

