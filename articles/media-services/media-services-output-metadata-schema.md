---
title: "aaaAzure Media Services çıkış meta veri şema | Microsoft Docs"
description: "Merhaba konu Azure Media Services çıkış meta veri şema genel bir bakış sağlar."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 1ed84c88-eea5-4a24-9c4f-f2428157d08a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 7f07d6accbe0b171d0408b15d5e1e6b5afd6c367
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="output-metadata"></a><span data-ttu-id="44482-103">Meta verileri çıktı</span><span class="sxs-lookup"><span data-stu-id="44482-103">Output Metadata</span></span>
## <a name="overview"></a><span data-ttu-id="44482-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="44482-104">Overview</span></span>
<span data-ttu-id="44482-105">Kodlama işinin bir giriş varlık (veya varlıklar) ile ilişkili istediğiniz tooperform kodlama bazı görevler.</span><span class="sxs-lookup"><span data-stu-id="44482-105">An encoding job is associated with an input asset (or assets) on which you want tooperform some encoding tasks.</span></span> <span data-ttu-id="44482-106">Örneğin, bir MP4 dosyası tooH.264 MP4 bit hızı Uyarlamalı kodlamak ayarlar; küçük resim oluşturma; yer paylaşımları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="44482-106">For example, encode an MP4 file tooH.264 MP4 adaptive bitrate sets; create a thumbnail; create overlays.</span></span> <span data-ttu-id="44482-107">Bir görev tamamlandığında, çıkış varlık oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="44482-107">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="44482-108">Merhaba çıkış varlık içeriyor video, ses, küçük resimleri, vb. hello çıkış varlığına hello çıkış varlık hakkındaki meta verileri dosyasıyla de içerir.</span><span class="sxs-lookup"><span data-stu-id="44482-108">hello output asset contains video, audio, thumbnails, etc. hello output asset also contains a file with metadata about hello output asset.</span></span> <span data-ttu-id="44482-109">Merhaba hello meta veri XML dosyası adına sahip biçimini izleyen hello: &lt;source_file_name&gt;_manifest.xml (örneğin, BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="44482-109">hello name of hello metadata XML file has hello following format: &lt;source_file_name&gt;_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span>  

<span data-ttu-id="44482-110">Tooexamine hello meta veri dosyası istiyorsanız, oluşturabileceğiniz bir **SAS** Bulucu ve indirme hello dosya tooyour yerel bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="44482-110">If you want tooexamine hello metadata file, you can create a **SAS** locator and download hello file tooyour local computer.</span></span>  

<span data-ttu-id="44482-111">Bu konuda hangi hello çıktı metada ele alınmıştır, hello öğeleri ve hello XML Şeması türleri (&lt;source_file_name&gt;_manifest.xml) dayanır.</span><span class="sxs-lookup"><span data-stu-id="44482-111">This topic discusses hello elements and types of hello XML schema on which hello output metada (&lt;source_file_name&gt;_manifest.xml) is based.</span></span> <span data-ttu-id="44482-112">Merhaba giriş varlık hakkında meta veriler içeren hello dosyası hakkında daha fazla bilgi için bkz: [giriş meta verileri](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="44482-112">For information about hello file that contains metadata about hello input asset, see [Input Metadata](media-services-input-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="44482-113">Merhaba tam şeması kod ve bu konuda hello sonunda XML örneği bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44482-113">You can find hello complete schema code and XML example at hello end of this topic.</span></span>  
>
>

## <span data-ttu-id="44482-114"><a name="AssetFiles "></a>AssetFiles kök öğesi</span><span class="sxs-lookup"><span data-stu-id="44482-114"><a name="AssetFiles "></a> AssetFiles root element</span></span>
<span data-ttu-id="44482-115">Merhaba kodlama işinin AssetFile girişlerinde koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="44482-115">Collection of AssetFile entries for hello encoding job.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="44482-116">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="44482-116">Child elements</span></span>
| <span data-ttu-id="44482-117">Ad</span><span class="sxs-lookup"><span data-stu-id="44482-117">Name</span></span> | <span data-ttu-id="44482-118">Açıklama</span><span class="sxs-lookup"><span data-stu-id="44482-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="44482-119">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="44482-119">**AssetFile**</span></span><br/><br/> <span data-ttu-id="44482-120">minOccurs = "0" maxOccurs = "1"</span><span class="sxs-lookup"><span data-stu-id="44482-120">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="44482-121">Bir [AssetFile öğesi](media-services-output-metadata-schema.md) parçası olan hello AssetFiles koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="44482-121">An [AssetFile element](media-services-output-metadata-schema.md) that is part of hello AssetFiles collection.</span></span> |

## <span data-ttu-id="44482-122"><a name="AssetFile "></a>AssetFile öğesi</span><span class="sxs-lookup"><span data-stu-id="44482-122"><a name="AssetFile "></a> AssetFile element</span></span>
<span data-ttu-id="44482-123">Bir XML örneğinde bulabilirsiniz [XML örneği](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="44482-123">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="44482-124">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="44482-124">Attributes</span></span>
| <span data-ttu-id="44482-125">Ad</span><span class="sxs-lookup"><span data-stu-id="44482-125">Name</span></span> | <span data-ttu-id="44482-126">Tür</span><span class="sxs-lookup"><span data-stu-id="44482-126">Type</span></span> | <span data-ttu-id="44482-127">Açıklama</span><span class="sxs-lookup"><span data-stu-id="44482-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44482-128">**Ad**</span><span class="sxs-lookup"><span data-stu-id="44482-128">**Name**</span></span><br/><br/> <span data-ttu-id="44482-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-129">Required</span></span> |<span data-ttu-id="44482-130">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="44482-130">**xs:string**</span></span> |<span data-ttu-id="44482-131">Merhaba medya varlık dosya adı.</span><span class="sxs-lookup"><span data-stu-id="44482-131">hello media asset file name.</span></span> |
| <span data-ttu-id="44482-132">**Boyut**</span><span class="sxs-lookup"><span data-stu-id="44482-132">**Size**</span></span><br/><br/> <span data-ttu-id="44482-133">minInclusive = "0"</span><span class="sxs-lookup"><span data-stu-id="44482-133">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="44482-134">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-134">Required</span></span> |<span data-ttu-id="44482-135">**xs:Long**</span><span class="sxs-lookup"><span data-stu-id="44482-135">**xs:long**</span></span> |<span data-ttu-id="44482-136">Merhaba varlık dosyasının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="44482-136">Size of hello asset file in bytes.</span></span> |
| <span data-ttu-id="44482-137">**Süre**</span><span class="sxs-lookup"><span data-stu-id="44482-137">**Duration**</span></span><br/><br/> <span data-ttu-id="44482-138">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-138">Required</span></span> |<span data-ttu-id="44482-139">**xs: Duration**</span><span class="sxs-lookup"><span data-stu-id="44482-139">**xs:duration**</span></span> |<span data-ttu-id="44482-140">İçerik play geri süresi.</span><span class="sxs-lookup"><span data-stu-id="44482-140">Content play back duration.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="44482-141">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="44482-141">Child elements</span></span>
| <span data-ttu-id="44482-142">Ad</span><span class="sxs-lookup"><span data-stu-id="44482-142">Name</span></span> | <span data-ttu-id="44482-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="44482-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="44482-144">**Kaynakları**</span><span class="sxs-lookup"><span data-stu-id="44482-144">**Sources**</span></span> |<span data-ttu-id="44482-145">İşlenmiş giriş/kaynak medya dosyaları koleksiyonu içinde bu AssetFile tooproduce sipariş.</span><span class="sxs-lookup"><span data-stu-id="44482-145">Collection of input/source media files, that was processed in order tooproduce this AssetFile.</span></span> <span data-ttu-id="44482-146">Daha fazla bilgi için bkz: [Source öğesi](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="44482-146">For more information, see [Source element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="44482-147">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="44482-147">**VideoTracks**</span></span><br/><br/> <span data-ttu-id="44482-148">minOccurs = "0" maxOccurs = "1"</span><span class="sxs-lookup"><span data-stu-id="44482-148">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="44482-149">Her fiziksel AssetFile içinde uygun bir kapsayıcı biçimi, araya eklemeli sıfır veya daha fazla video parçaları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="44482-149">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="44482-150">Bu hello bu video parçaları koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="44482-150">This is hello collection of all those video tracks.</span></span> <span data-ttu-id="44482-151">Daha fazla bilgi için bkz: [VideoTracks öğesi](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="44482-151">For more information, see [VideoTracks element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="44482-152">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="44482-152">**AudioTracks**</span></span><br/><br/> <span data-ttu-id="44482-153">minOccurs = "0" maxOccurs = "1"</span><span class="sxs-lookup"><span data-stu-id="44482-153">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="44482-154">Her fiziksel AssetFile içinde uygun bir kapsayıcı biçimi, araya eklemeli sıfır veya daha fazla ses izleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="44482-154">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="44482-155">Bu hello bu ses izleri koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="44482-155">This is hello collection of all those audio tracks.</span></span> <span data-ttu-id="44482-156">Daha fazla bilgi için bkz: [AudioTracks öğesi](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="44482-156">For more information, see [AudioTracks element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="44482-157"><a name="Sources "></a>Sources öğesi</span><span class="sxs-lookup"><span data-stu-id="44482-157"><a name="Sources "></a> Sources element</span></span>
<span data-ttu-id="44482-158">İşlenmiş giriş/kaynak medya dosyaları koleksiyonu içinde bu AssetFile tooproduce sipariş.</span><span class="sxs-lookup"><span data-stu-id="44482-158">Collection of input/source media files, that was processed in order tooproduce this AssetFile.</span></span>  

<span data-ttu-id="44482-159">Bir XML örneğinde bulabilirsiniz [XML örneği](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="44482-159">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="44482-160">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="44482-160">Child elements</span></span>
| <span data-ttu-id="44482-161">Ad</span><span class="sxs-lookup"><span data-stu-id="44482-161">Name</span></span> | <span data-ttu-id="44482-162">Açıklama</span><span class="sxs-lookup"><span data-stu-id="44482-162">Description</span></span> |
| --- | --- |
| <span data-ttu-id="44482-163">**Kaynak**</span><span class="sxs-lookup"><span data-stu-id="44482-163">**Source**</span></span><br/><br/> <span data-ttu-id="44482-164">minOccurs "1" maxOccurs = "unbounded" =</span><span class="sxs-lookup"><span data-stu-id="44482-164">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="44482-165">Bu varlık oluşturulurken kullanılan bir giriş/kaynak dosyası.</span><span class="sxs-lookup"><span data-stu-id="44482-165">An input/source file used when generating this asset.</span></span> <span data-ttu-id="44482-166">Daha fazla bilgi için bkz: [Source öğesi](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="44482-166">For more information see [Source element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="44482-167"><a name="Source "></a>Source öğesi</span><span class="sxs-lookup"><span data-stu-id="44482-167"><a name="Source "></a> Source element</span></span>
<span data-ttu-id="44482-168">Bu varlık oluşturulurken kullanılan bir giriş/kaynak dosyası.</span><span class="sxs-lookup"><span data-stu-id="44482-168">An input/source file used when generating this asset.</span></span>  

<span data-ttu-id="44482-169">Bir XML örneğinde bulabilirsiniz [XML örneği](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="44482-169">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="44482-170">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="44482-170">Attributes</span></span>
| <span data-ttu-id="44482-171">Ad</span><span class="sxs-lookup"><span data-stu-id="44482-171">Name</span></span> | <span data-ttu-id="44482-172">Tür</span><span class="sxs-lookup"><span data-stu-id="44482-172">Type</span></span> | <span data-ttu-id="44482-173">Açıklama</span><span class="sxs-lookup"><span data-stu-id="44482-173">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44482-174">**Ad**</span><span class="sxs-lookup"><span data-stu-id="44482-174">**Name**</span></span><br/><br/> <span data-ttu-id="44482-175">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-175">Required</span></span> |<span data-ttu-id="44482-176">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="44482-176">**xs:string**</span></span> |<span data-ttu-id="44482-177">Giriş kaynağının dosya adı.</span><span class="sxs-lookup"><span data-stu-id="44482-177">Input source file name.</span></span> |

## <span data-ttu-id="44482-178"><a name="VideoTracks "></a>VideoTracks öğesi</span><span class="sxs-lookup"><span data-stu-id="44482-178"><a name="VideoTracks "></a> VideoTracks element</span></span>
<span data-ttu-id="44482-179">Her fiziksel AssetFile içinde uygun bir kapsayıcı biçimi, araya eklemeli sıfır veya daha fazla video parçaları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="44482-179">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="44482-180">Bu hello bu video parçaları koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="44482-180">This is hello collection of all those video tracks.</span></span>  

<span data-ttu-id="44482-181">Bir XML örneğinde bulabilirsiniz [XML örneği](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="44482-181">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="44482-182">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="44482-182">Child elements</span></span>
| <span data-ttu-id="44482-183">Ad</span><span class="sxs-lookup"><span data-stu-id="44482-183">Name</span></span> | <span data-ttu-id="44482-184">Açıklama</span><span class="sxs-lookup"><span data-stu-id="44482-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="44482-185">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="44482-185">**VideoTrack**</span></span><br/><br/> <span data-ttu-id="44482-186">minOccurs "1" maxOccurs = "unbounded" =</span><span class="sxs-lookup"><span data-stu-id="44482-186">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="44482-187">Belirli bir video hello üst AssetFile izler.</span><span class="sxs-lookup"><span data-stu-id="44482-187">A specific video track in hello parent AssetFile.</span></span> <span data-ttu-id="44482-188">Daha fazla bilgi için bkz: [VideoTrack öğesi](media-services-output-metadata-schema.md#VideoTrack).</span><span class="sxs-lookup"><span data-stu-id="44482-188">For more information, see [VideoTrack element](media-services-output-metadata-schema.md#VideoTrack).</span></span> |

## <span data-ttu-id="44482-189"><a name="VideoTrack"></a>VideoTrack öğesi</span><span class="sxs-lookup"><span data-stu-id="44482-189"><a name="VideoTrack"></a> VideoTrack element</span></span>
<span data-ttu-id="44482-190">Belirli bir video hello üst AssetFile izler.</span><span class="sxs-lookup"><span data-stu-id="44482-190">A specific video track in hello parent AssetFile.</span></span>  

<span data-ttu-id="44482-191">Bir XML örneğinde bulabilirsiniz [XML örneği](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="44482-191">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="44482-192">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="44482-192">Attributes</span></span>
| <span data-ttu-id="44482-193">Ad</span><span class="sxs-lookup"><span data-stu-id="44482-193">Name</span></span> | <span data-ttu-id="44482-194">Tür</span><span class="sxs-lookup"><span data-stu-id="44482-194">Type</span></span> | <span data-ttu-id="44482-195">Açıklama</span><span class="sxs-lookup"><span data-stu-id="44482-195">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44482-196">**Kimliği**</span><span class="sxs-lookup"><span data-stu-id="44482-196">**Id**</span></span><br/><br/> <span data-ttu-id="44482-197">minInclusive = "0"</span><span class="sxs-lookup"><span data-stu-id="44482-197">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="44482-198">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-198">Required</span></span> |<span data-ttu-id="44482-199">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="44482-199">**xs:int**</span></span> |<span data-ttu-id="44482-200">Bu video izlemeyi sıfır tabanlı dizini. **Not:** bu mutlaka hello olarak kullanılan bir MP4 dosyasına TrackID değil.</span><span class="sxs-lookup"><span data-stu-id="44482-200">Zero-based index of this video track. **Note:**  This is not necessarily hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="44482-201">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="44482-201">**FourCC**</span></span><br/><br/> <span data-ttu-id="44482-202">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-202">Required</span></span> |<span data-ttu-id="44482-203">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="44482-203">**xs:string**</span></span> |<span data-ttu-id="44482-204">Görüntü codec FourCC kodu.</span><span class="sxs-lookup"><span data-stu-id="44482-204">Video codec FourCC code.</span></span> |
| <span data-ttu-id="44482-205">**Profili**</span><span class="sxs-lookup"><span data-stu-id="44482-205">**Profile**</span></span> |<span data-ttu-id="44482-206">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="44482-206">**xs:string**</span></span> |<span data-ttu-id="44482-207">H264 profili (yalnızca geçerli tooH264 codec).</span><span class="sxs-lookup"><span data-stu-id="44482-207">H264 profile (only applicable tooH264 codec).</span></span> |
| <span data-ttu-id="44482-208">**Düzeyi**</span><span class="sxs-lookup"><span data-stu-id="44482-208">**Level**</span></span> |<span data-ttu-id="44482-209">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="44482-209">**xs:string**</span></span> |<span data-ttu-id="44482-210">H264 düzeyi (yalnızca geçerli tooH264 codec).</span><span class="sxs-lookup"><span data-stu-id="44482-210">H264 level (only applicable tooH264 codec).</span></span> |
| <span data-ttu-id="44482-211">**Genişlik**</span><span class="sxs-lookup"><span data-stu-id="44482-211">**Width**</span></span><br/><br/> <span data-ttu-id="44482-212">minInclusive = "0"</span><span class="sxs-lookup"><span data-stu-id="44482-212">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="44482-213">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-213">Required</span></span> |<span data-ttu-id="44482-214">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="44482-214">**xs:int**</span></span> |<span data-ttu-id="44482-215">Kodlanmış video genişliğini piksel cinsinden.</span><span class="sxs-lookup"><span data-stu-id="44482-215">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="44482-216">**Yükseklik**</span><span class="sxs-lookup"><span data-stu-id="44482-216">**Height**</span></span><br/><br/> <span data-ttu-id="44482-217">minInclusive = "0"</span><span class="sxs-lookup"><span data-stu-id="44482-217">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="44482-218">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-218">Required</span></span> |<span data-ttu-id="44482-219">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="44482-219">**xs:int**</span></span> |<span data-ttu-id="44482-220">Piksel cinsinden görüntü yüksekliği kodlanmış.</span><span class="sxs-lookup"><span data-stu-id="44482-220">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="44482-221">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="44482-221">**DisplayAspectRatioNumerator**</span></span><br/><br/> <span data-ttu-id="44482-222">minInclusive = "0"</span><span class="sxs-lookup"><span data-stu-id="44482-222">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="44482-223">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-223">Required</span></span> |<span data-ttu-id="44482-224">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="44482-224">**xs:double**</span></span> |<span data-ttu-id="44482-225">Video görüntü en boy oranını pay.</span><span class="sxs-lookup"><span data-stu-id="44482-225">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="44482-226">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="44482-226">**DisplayAspectRatioDenominator**</span></span><br/><br/> <span data-ttu-id="44482-227">minInclusive = "0"</span><span class="sxs-lookup"><span data-stu-id="44482-227">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="44482-228">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-228">Required</span></span> |<span data-ttu-id="44482-229">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="44482-229">**xs:double**</span></span> |<span data-ttu-id="44482-230">Video görüntü en boy oranını payda.</span><span class="sxs-lookup"><span data-stu-id="44482-230">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="44482-231">**Kare hızı**</span><span class="sxs-lookup"><span data-stu-id="44482-231">**Framerate**</span></span><br/><br/> <span data-ttu-id="44482-232">minInclusive = "0"</span><span class="sxs-lookup"><span data-stu-id="44482-232">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="44482-233">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-233">Required</span></span> |<span data-ttu-id="44482-234">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="44482-234">**xs:decimal**</span></span> |<span data-ttu-id="44482-235">Video kare hızı .3f biçiminde ölçülür.</span><span class="sxs-lookup"><span data-stu-id="44482-235">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="44482-236">**TargetFramerate**</span><span class="sxs-lookup"><span data-stu-id="44482-236">**TargetFramerate**</span></span><br/><br/> <span data-ttu-id="44482-237">minInclusive = "0"</span><span class="sxs-lookup"><span data-stu-id="44482-237">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="44482-238">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-238">Required</span></span> |<span data-ttu-id="44482-239">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="44482-239">**xs:decimal**</span></span> |<span data-ttu-id="44482-240">Hedef video kare hızı .3f biçiminde hazır.</span><span class="sxs-lookup"><span data-stu-id="44482-240">Preset target video frame rate in .3f format.</span></span> |
| <span data-ttu-id="44482-241">**Bit hızı**</span><span class="sxs-lookup"><span data-stu-id="44482-241">**Bitrate**</span></span><br/><br/> <span data-ttu-id="44482-242">minInclusive = "0"</span><span class="sxs-lookup"><span data-stu-id="44482-242">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="44482-243">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-243">Required</span></span> |<span data-ttu-id="44482-244">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="44482-244">**xs:int**</span></span> |<span data-ttu-id="44482-245">Ortalama video bit hızı hello AssetFile gelen hesaplanan olarak kilobit / saniye.</span><span class="sxs-lookup"><span data-stu-id="44482-245">Average video bit rate in kilobits per second, as calculated from hello AssetFile.</span></span> <span data-ttu-id="44482-246">Yalnızca hello başlangıç akışı yükü sayar ve hello paketleme yükünü içermez.</span><span class="sxs-lookup"><span data-stu-id="44482-246">Counts only hello elementary stream payload, and does not include hello packaging overhead.</span></span> |
| <span data-ttu-id="44482-247">**TargetBitrate**</span><span class="sxs-lookup"><span data-stu-id="44482-247">**TargetBitrate**</span></span><br/><br/> <span data-ttu-id="44482-248">minInclusive = "0"</span><span class="sxs-lookup"><span data-stu-id="44482-248">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="44482-249">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-249">Required</span></span> |<span data-ttu-id="44482-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="44482-250">**xs:int**</span></span> |<span data-ttu-id="44482-251">Bu video izlemek için ortalama bit hızı kilobit hello kodlama hazır aracılığıyla istendiği gibi hedefleyin.</span><span class="sxs-lookup"><span data-stu-id="44482-251">Target average bitrate for this video track, as requested via hello encoding preset, in kilobits per second.</span></span> |
| <span data-ttu-id="44482-252">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="44482-252">**MaxGOPBitrate**</span></span><br/><br/> <span data-ttu-id="44482-253">minInclusive = "0"</span><span class="sxs-lookup"><span data-stu-id="44482-253">minInclusive ="0"</span></span> |<span data-ttu-id="44482-254">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="44482-254">**xs:int**</span></span> |<span data-ttu-id="44482-255">Max GOP ortalama bit hızı kilobit bu video izlemek için.</span><span class="sxs-lookup"><span data-stu-id="44482-255">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |

## <span data-ttu-id="44482-256"><a name="AudioTracks "></a>AudioTracks öğesi</span><span class="sxs-lookup"><span data-stu-id="44482-256"><a name="AudioTracks "></a> AudioTracks element</span></span>
<span data-ttu-id="44482-257">Her fiziksel AssetFile içinde uygun bir kapsayıcı biçimi, araya eklemeli sıfır veya daha fazla ses izleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="44482-257">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="44482-258">Bu hello bu ses izleri koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="44482-258">This is hello collection of all those audio tracks.</span></span>  

<span data-ttu-id="44482-259">Bir XML örneğinde bulabilirsiniz [XML örneği](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="44482-259">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="44482-260">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="44482-260">Child elements</span></span>
| <span data-ttu-id="44482-261">Ad</span><span class="sxs-lookup"><span data-stu-id="44482-261">Name</span></span> | <span data-ttu-id="44482-262">Açıklama</span><span class="sxs-lookup"><span data-stu-id="44482-262">Description</span></span> |
| --- | --- |
| <span data-ttu-id="44482-263">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="44482-263">**AudioTrack**</span></span><br/><br/> <span data-ttu-id="44482-264">minOccurs "1" maxOccurs = "unbounded" =</span><span class="sxs-lookup"><span data-stu-id="44482-264">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="44482-265">Belirli bir ses hello üst AssetFile izler.</span><span class="sxs-lookup"><span data-stu-id="44482-265">A specific audio track in hello parent AssetFile.</span></span> <span data-ttu-id="44482-266">Daha fazla bilgi için bkz: [AudioTrack öğesi](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="44482-266">For more information, see [AudioTrack element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="44482-267"><a name="AudioTrack "></a>AudioTrack öğesi</span><span class="sxs-lookup"><span data-stu-id="44482-267"><a name="AudioTrack "></a> AudioTrack element</span></span>
<span data-ttu-id="44482-268">Belirli bir ses hello üst AssetFile izler.</span><span class="sxs-lookup"><span data-stu-id="44482-268">A specific audio track in hello parent AssetFile.</span></span>  

<span data-ttu-id="44482-269">Bir XML örneğinde bulabilirsiniz [XML örneği](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="44482-269">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="44482-270">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="44482-270">Attributes</span></span>
| <span data-ttu-id="44482-271">Ad</span><span class="sxs-lookup"><span data-stu-id="44482-271">Name</span></span> | <span data-ttu-id="44482-272">Tür</span><span class="sxs-lookup"><span data-stu-id="44482-272">Type</span></span> | <span data-ttu-id="44482-273">Açıklama</span><span class="sxs-lookup"><span data-stu-id="44482-273">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44482-274">**Kimliği**</span><span class="sxs-lookup"><span data-stu-id="44482-274">**Id**</span></span><br/><br/> <span data-ttu-id="44482-275">minInclusive = "0"</span><span class="sxs-lookup"><span data-stu-id="44482-275">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="44482-276">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-276">Required</span></span> |<span data-ttu-id="44482-277">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="44482-277">**xs:int**</span></span> |<span data-ttu-id="44482-278">Bu ses parça sıfır tabanlı dizini. **Not:** bu mutlaka hello olarak kullanılan bir MP4 dosyasına TrackID değil.</span><span class="sxs-lookup"><span data-stu-id="44482-278">Zero-based index of this audio track. **Note:**  This is not necessarily hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="44482-279">**Codec**</span><span class="sxs-lookup"><span data-stu-id="44482-279">**Codec**</span></span> |<span data-ttu-id="44482-280">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="44482-280">**xs:string**</span></span> |<span data-ttu-id="44482-281">Ses izleme codec dizesi.</span><span class="sxs-lookup"><span data-stu-id="44482-281">Audio track codec string.</span></span> |
| <span data-ttu-id="44482-282">**EncoderVersion**</span><span class="sxs-lookup"><span data-stu-id="44482-282">**EncoderVersion**</span></span> |<span data-ttu-id="44482-283">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="44482-283">**xs:string**</span></span> |<span data-ttu-id="44482-284">EAC3 için gereken isteğe bağlı Kodlayıcı sürüm dizesi.</span><span class="sxs-lookup"><span data-stu-id="44482-284">Optional encoder version string, required for EAC3.</span></span> |
| <span data-ttu-id="44482-285">**Kanalları**</span><span class="sxs-lookup"><span data-stu-id="44482-285">**Channels**</span></span><br/><br/> <span data-ttu-id="44482-286">minInclusive = "0"</span><span class="sxs-lookup"><span data-stu-id="44482-286">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="44482-287">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-287">Required</span></span> |<span data-ttu-id="44482-288">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="44482-288">**xs:int**</span></span> |<span data-ttu-id="44482-289">Ses kanal sayısı.</span><span class="sxs-lookup"><span data-stu-id="44482-289">Number of audio channels.</span></span> |
| <span data-ttu-id="44482-290">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="44482-290">**SamplingRate**</span></span><br/><br/> <span data-ttu-id="44482-291">minInclusive = "0"</span><span class="sxs-lookup"><span data-stu-id="44482-291">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="44482-292">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-292">Required</span></span> |<span data-ttu-id="44482-293">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="44482-293">**xs:int**</span></span> |<span data-ttu-id="44482-294">Saniye başına örnekleri veya Hz ses örnekleme hızı.</span><span class="sxs-lookup"><span data-stu-id="44482-294">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="44482-295">**Bit hızı**</span><span class="sxs-lookup"><span data-stu-id="44482-295">**Bitrate**</span></span><br/><br/> <span data-ttu-id="44482-296">minInclusive = "0"</span><span class="sxs-lookup"><span data-stu-id="44482-296">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="44482-297">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-297">Required</span></span> |<span data-ttu-id="44482-298">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="44482-298">**xs:int**</span></span> |<span data-ttu-id="44482-299">Merhaba AssetFile gelen hesaplanan olarak saniyedeki ortalama ses bit hızı.</span><span class="sxs-lookup"><span data-stu-id="44482-299">Average audio bit rate in bits per second, as calculated from hello AssetFile.</span></span> <span data-ttu-id="44482-300">Yalnızca hello başlangıç akışı yükü sayar ve hello paketleme yükünü içermez.</span><span class="sxs-lookup"><span data-stu-id="44482-300">Counts only hello elementary stream payload, and does not include hello packaging overhead.</span></span> |
| <span data-ttu-id="44482-301">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="44482-301">**BitsPerSample**</span></span><br/><br/> <span data-ttu-id="44482-302">minInclusive = "0"</span><span class="sxs-lookup"><span data-stu-id="44482-302">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="44482-303">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-303">Required</span></span> |<span data-ttu-id="44482-304">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="44482-304">**xs:int**</span></span> |<span data-ttu-id="44482-305">Merhaba wFormatTag biçimi için örnek başına bit yazın.</span><span class="sxs-lookup"><span data-stu-id="44482-305">Bits per sample for hello wFormatTag format type.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="44482-306">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="44482-306">Child elements</span></span>
| <span data-ttu-id="44482-307">Ad</span><span class="sxs-lookup"><span data-stu-id="44482-307">Name</span></span> | <span data-ttu-id="44482-308">Açıklama</span><span class="sxs-lookup"><span data-stu-id="44482-308">Description</span></span> |
| --- | --- |
| <span data-ttu-id="44482-309">**LoudnessMeteringResultParameters**</span><span class="sxs-lookup"><span data-stu-id="44482-309">**LoudnessMeteringResultParameters**</span></span><br/><br/> <span data-ttu-id="44482-310">minOccurs = "0" maxOccurs = "1"</span><span class="sxs-lookup"><span data-stu-id="44482-310">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="44482-311">Sonuç parametreleri ölçüm ses yüksekliği.</span><span class="sxs-lookup"><span data-stu-id="44482-311">Loudness metering result parameters.</span></span> <span data-ttu-id="44482-312">Daha fazla bilgi için bkz: [LoudnessMeteringResultParameters öğesi](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="44482-312">For more information, see [LoudnessMeteringResultParameters element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="44482-313"><a name="LoudnessMeteringResultParameters "></a>LoudnessMeteringResultParameters öğesi</span><span class="sxs-lookup"><span data-stu-id="44482-313"><a name="LoudnessMeteringResultParameters "></a> LoudnessMeteringResultParameters element</span></span>
<span data-ttu-id="44482-314">Sonuç parametreleri ölçüm ses yüksekliği.</span><span class="sxs-lookup"><span data-stu-id="44482-314">Loudness metering result parameters.</span></span>  

<span data-ttu-id="44482-315">Bir XML örneğinde bulabilirsiniz [XML örneği](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="44482-315">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="44482-316">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="44482-316">Attributes</span></span>
| <span data-ttu-id="44482-317">Ad</span><span class="sxs-lookup"><span data-stu-id="44482-317">Name</span></span> | <span data-ttu-id="44482-318">Tür</span><span class="sxs-lookup"><span data-stu-id="44482-318">Type</span></span> | <span data-ttu-id="44482-319">Açıklama</span><span class="sxs-lookup"><span data-stu-id="44482-319">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44482-320">**DPLMVersionInformation**</span><span class="sxs-lookup"><span data-stu-id="44482-320">**DPLMVersionInformation**</span></span> |<span data-ttu-id="44482-321">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="44482-321">**xs:string**</span></span> |<span data-ttu-id="44482-322">**Dolby** Geliştirme Seti sürüm ölçümü profesyonel ses yüksekliği.</span><span class="sxs-lookup"><span data-stu-id="44482-322">**Dolby** professional loudness metering development kit version.</span></span> |
| <span data-ttu-id="44482-323">**DialogNormalization**</span><span class="sxs-lookup"><span data-stu-id="44482-323">**DialogNormalization**</span></span><br/><br/> <span data-ttu-id="44482-324">minInclusive "-31" maxInclusive = = "-1"</span><span class="sxs-lookup"><span data-stu-id="44482-324">minInclusive="-31" maxInclusive="-1"</span></span><br/><br/> <span data-ttu-id="44482-325">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-325">Required</span></span> |<span data-ttu-id="44482-326">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="44482-326">**xs:int**</span></span> |<span data-ttu-id="44482-327">LoudnessMetering ayarlandığında gerekli DPLM oluşturulan DialogNormalization</span><span class="sxs-lookup"><span data-stu-id="44482-327">DialogNormalization generated through DPLM, required when LoudnessMetering is set</span></span> |
| <span data-ttu-id="44482-328">**IntegratedLoudness**</span><span class="sxs-lookup"><span data-stu-id="44482-328">**IntegratedLoudness**</span></span><br/><br/> <span data-ttu-id="44482-329">minInclusive "-70" maxInclusive = = "10"</span><span class="sxs-lookup"><span data-stu-id="44482-329">minInclusive="-70" maxInclusive="10"</span></span><br/><br/> <span data-ttu-id="44482-330">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-330">Required</span></span> |<span data-ttu-id="44482-331">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="44482-331">**xs:float**</span></span> |<span data-ttu-id="44482-332">Tümleşik ses yüksekliği</span><span class="sxs-lookup"><span data-stu-id="44482-332">Integrated loudness</span></span> |
| <span data-ttu-id="44482-333">**IntegratedLoudnessUnit**</span><span class="sxs-lookup"><span data-stu-id="44482-333">**IntegratedLoudnessUnit**</span></span><br/><br/> <span data-ttu-id="44482-334">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-334">Required</span></span> |<span data-ttu-id="44482-335">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="44482-335">**xs:string**</span></span> |<span data-ttu-id="44482-336">Tümleşik ses yüksekliği birimi.</span><span class="sxs-lookup"><span data-stu-id="44482-336">Integrated loudness unit.</span></span> |
| <span data-ttu-id="44482-337">**IntegratedLoudnessGatingMethod**</span><span class="sxs-lookup"><span data-stu-id="44482-337">**IntegratedLoudnessGatingMethod**</span></span><br/><br/> <span data-ttu-id="44482-338">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-338">Required</span></span> |<span data-ttu-id="44482-339">**xs: String**</span><span class="sxs-lookup"><span data-stu-id="44482-339">**xs:string**</span></span> |<span data-ttu-id="44482-340">Tanımlayıcı geçişi</span><span class="sxs-lookup"><span data-stu-id="44482-340">Gating identifier</span></span> |
| <span data-ttu-id="44482-341">**IntegratedLoudnessSpeechPercentage**</span><span class="sxs-lookup"><span data-stu-id="44482-341">**IntegratedLoudnessSpeechPercentage**</span></span><br/><br/> <span data-ttu-id="44482-342">minInclusive "0" maxInclusive = = "100"</span><span class="sxs-lookup"><span data-stu-id="44482-342">minInclusive ="0" maxInclusive="100"</span></span> |<span data-ttu-id="44482-343">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="44482-343">**xs:float**</span></span> |<span data-ttu-id="44482-344">Yüzde olarak hello programı üzerinden konuşma içeriği.</span><span class="sxs-lookup"><span data-stu-id="44482-344">Speech content over hello program, as a percentage.</span></span> |
| <span data-ttu-id="44482-345">**SamplePeak**</span><span class="sxs-lookup"><span data-stu-id="44482-345">**SamplePeak**</span></span><br/><br/> <span data-ttu-id="44482-346">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-346">Required</span></span> |<span data-ttu-id="44482-347">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="44482-347">**xs:float**</span></span> |<span data-ttu-id="44482-348">Yoğun mutlak örnek değeri, sıfırlama veya son başlatıldığından beri kanal başına kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="44482-348">Peak absolute sample value, since reset or since it was last cleared, per channel.</span></span>  <span data-ttu-id="44482-349">DBFS birimleridir.</span><span class="sxs-lookup"><span data-stu-id="44482-349">Units are dBFS.</span></span> |
| <span data-ttu-id="44482-350">**SamplePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="44482-350">**SamplePeakUnit**</span></span><br/><br/> <span data-ttu-id="44482-351">Sabit "dBFS" =</span><span class="sxs-lookup"><span data-stu-id="44482-351">fixed="dBFS"</span></span><br/><br/> <span data-ttu-id="44482-352">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-352">Required</span></span> |<span data-ttu-id="44482-353">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="44482-353">**xs:anySimpleType**</span></span> |<span data-ttu-id="44482-354">Örnek en yüksek birim.</span><span class="sxs-lookup"><span data-stu-id="44482-354">Sample peak unit.</span></span> |
| <span data-ttu-id="44482-355">**TruePeak**</span><span class="sxs-lookup"><span data-stu-id="44482-355">**TruePeak**</span></span><br/><br/> <span data-ttu-id="44482-356">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-356">Required</span></span> |<span data-ttu-id="44482-357">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="44482-357">**xs:float**</span></span> |<span data-ttu-id="44482-358">Kanal başına en fazla true en yüksek değer, göredir ITU-R BS.1770-2, sıfırlama veya son başlatıldığından beri temizlendi.</span><span class="sxs-lookup"><span data-stu-id="44482-358">Maximum true peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.</span></span> <span data-ttu-id="44482-359">DBTP birimleridir.</span><span class="sxs-lookup"><span data-stu-id="44482-359">Units are dBTP.</span></span> |
| <span data-ttu-id="44482-360">**TruePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="44482-360">**TruePeakUnit**</span></span><br/><br/> <span data-ttu-id="44482-361">Sabit "dBTP" =</span><span class="sxs-lookup"><span data-stu-id="44482-361">fixed="dBTP"</span></span><br/><br/> <span data-ttu-id="44482-362">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44482-362">Required</span></span> |<span data-ttu-id="44482-363">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="44482-363">**xs:anySimpleType**</span></span> |<span data-ttu-id="44482-364">TRUE en yüksek birim.</span><span class="sxs-lookup"><span data-stu-id="44482-364">True peak unit.</span></span> |

## <a name="schema-code"></a><span data-ttu-id="44482-365">Şema kodu</span><span class="sxs-lookup"><span data-stu-id="44482-365">Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.2"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               elementFormDefault="qualified">  
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
                  <xs:element name="Sources">  
                    <xs:annotation>  
                      <xs:documentation>Collection of input/source media files, that was processed in order tooproduce this AssetFile</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Source" minOccurs="1" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>An input/source file used when generating this asset</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:attribute name="Name" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>input source file name</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
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
                            <xs:attribute name="FourCC" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>video codec FourCC code</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Profile" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 profile (only appliable for H264 codec)</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Level" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 level (only appliable for H264 codec)</xs:documentation>  
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
                            <xs:attribute name="Framerate" use="required">  
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
                            <xs:attribute name="TargetFramerate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>preset target video frame rate in .3f format</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:decimal">  
                                  <xs:minInclusive value="0"/>  
                                  <xs:fractionDigits value="3"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="TargetBitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>target average bitrate for this video track, as requested via hello encoding preset, in kilobits per second</xs:documentation>  
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
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:sequence>  
                              <xs:element name="LoudnessMeteringResultParameters" minOccurs="0" maxOccurs="1">  
                                <xs:annotation>  
                                  <xs:documentation>Loudness Metering Result Parameters</xs:documentation>  
                                </xs:annotation>  
                                <xs:complexType>  
                                  <xs:attribute name="DPLMVersionInformation" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Dolby Professional Loudness Metering Development Kit Version</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="DialogNormalization" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation> DialogNormalization generated through DPLM, required when LoudnessMetering is set</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:int">  
                                        <xs:minInclusive value="-31"/>  
                                        <xs:maxInclusive value="-1"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudness" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation>Integrated loudness</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="-70"/>  
                                        <xs:maxInclusive value="10"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessUnit" use="required" type="xs:string">  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessGatingMethod" use="required" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Gating identifier</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessSpeechPercentage">  
                                    <xs:annotation>  
                                      <xs:documentation>Speech content over hello program, as a percentage.</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="0"/>  
                                        <xs:maxInclusive value="100"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Peak absolute sample value, since reset or since it was last cleared, per channel.  Units are dBFS.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeakUnit" use="required" fixed="dBFS">  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Maximum True Peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.  Units are dBTP.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeakUnit" use="required" fixed="dBTP">  
                                  </xs:attribute>  
                                </xs:complexType>  
                              </xs:element>  
                            </xs:sequence>  
                            <xs:attribute name="Id" use="required">  
                              <xs:annotation>  
                                <xs:documentation>zero-based index of this audio track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Codec" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>audio track codec string</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="EncoderVersion" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>optional encoder version string, required for EAC3</xs:documentation>  
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
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="BitsPerSample" use="required">  
                              <xs:annotation>  
                                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
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
                <xs:attribute name="Duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:duration"/>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  



## <span data-ttu-id="44482-366"><a name="xml"></a>XML örneği</span><span class="sxs-lookup"><span data-stu-id="44482-366"><a name="xml"></a> XML example</span></span>
 <span data-ttu-id="44482-367">Merhaba, hello çıkış meta veri dosyası örneği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="44482-367">hello following is an example of hello Output metadata file.</span></span>  

    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
                xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata">  
      <AssetFile Name="BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4" Size="4646283" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.2" Width="1280" Height="720" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="4250" TargetBitrate="3400" MaxGOPBitrate="5514"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4" Size="3166728" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="2846" TargetBitrate="2250" MaxGOPBitrate="3630"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4" Size="2205095" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1932" TargetBitrate="1500" MaxGOPBitrate="2513"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4" Size="1508567" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1271" TargetBitrate="1000" MaxGOPBitrate="1527"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4" Size="1057155" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="843" TargetBitrate="650" MaxGOPBitrate="1086"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4" Size="699262" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="1.3" Width="320" Height="180" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="503" TargetBitrate="400" MaxGOPBitrate="661"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_96kbps.mp4" Size="166780" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_56kbps.mp4" Size="124576" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="53" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a><span data-ttu-id="44482-368">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="44482-368">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="44482-369">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="44482-369">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
