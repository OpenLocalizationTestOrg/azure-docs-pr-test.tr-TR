---
title: "aaaMedia Kodlayıcı Premium iş akışı biçimleri ve codec bileşenleri | Microsoft Docs"
description: "Bu konuda Medya Kodlayıcısı Premium iş akışı biçimleri biçimleri ve codec bileşenleri hakkında genel bir bakış sağlar"
services: media-services
documentationcenter: 
author: juliako
manager: erik43
editor: 
ms.assetid: b197fce8-3b9b-4189-8d08-486810c0426f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;anilmur
ms.openlocfilehash: e781384ca8f08926f00c83b6710fd413ce2a3e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-premium-workflow-formats-and-codecs"></a><span data-ttu-id="65451-103">Medya Kodlayıcısı Premium iş akışı biçimleri ve codec bileşenleri</span><span class="sxs-lookup"><span data-stu-id="65451-103">Media Encoder Premium Workflow formats and codecs</span></span>
> [!NOTE]
> <span data-ttu-id="65451-104">Premium Kodlayıcı sorular için mepd adresindeki Microsoft.com e-posta.</span><span class="sxs-lookup"><span data-stu-id="65451-104">For premium encoder questions, email mepd at Microsoft.com.</span></span>
> 
> <span data-ttu-id="65451-105">Bu konuda tartışılan Medya Kodlayıcısı Premium iş akışı medya işlemcisi Çin'de kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="65451-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span> 
> 
> 

<span data-ttu-id="65451-106">Bu belge giriş ve çıkış dosya biçimlerini ve hello genel Önizleme sürümü hello tarafından desteklenen codec bileşenleri listesini içeren **Medya Kodlayıcısı Premium iş akışı** Kodlayıcı.</span><span class="sxs-lookup"><span data-stu-id="65451-106">This document contains a list of input and output file formats and codecs that are supported by hello public preview version of hello **Media Encoder Premium Workflow** encoder.</span></span>

[<span data-ttu-id="65451-107">Medya Kodlayıcısı Premium Worflow giriş biçimlerini ve codec bileşenleri</span><span class="sxs-lookup"><span data-stu-id="65451-107">Media Encoder Premium Worflow Input Formats and Codecs</span></span>](#input_formats)

[<span data-ttu-id="65451-108">Medya Kodlayıcısı Premium Worflow Çıkış biçimleri ve codec bileşenleri</span><span class="sxs-lookup"><span data-stu-id="65451-108">Media Encoder Premium Worflow Output Formats and Codecs</span></span>](#output_formats)

<span data-ttu-id="65451-109">**Medya Kodlayıcısı Premium iş akışı** destekler kapalı açıklanan açıklamalı alt yazı [bu](#closed_captioning) bölümü.</span><span class="sxs-lookup"><span data-stu-id="65451-109">**Media Encoder Premium Workflow** supports closed captioning described in [this](#closed_captioning) section.</span></span> 

## <span data-ttu-id="65451-110"><a id="input_formats"></a>Medya Kodlayıcısı Premium iş akışı giriş biçimlerini ve codec bileşenleri</span><span class="sxs-lookup"><span data-stu-id="65451-110"><a id="input_formats"></a>Media Encoder Premium Workflow Input Formats and Codecs</span></span>
<span data-ttu-id="65451-111">bölümden hello girdi olarak bu medya işlemcisi destekleyen hello codec bileşenleri ve dosya biçimlerini listeler.</span><span class="sxs-lookup"><span data-stu-id="65451-111">hello following section lists hello codecs and file formats that this media processor supports as input.</span></span>

### <a name="input-containerfile-formats"></a><span data-ttu-id="65451-112">Kapsayıcı/dosya biçimleri giriş</span><span class="sxs-lookup"><span data-stu-id="65451-112">Input Container/File Formats</span></span>
* <span data-ttu-id="65451-113">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="65451-113">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="65451-114">MXF/SMPTE 377M</span><span class="sxs-lookup"><span data-stu-id="65451-114">MXF/SMPTE 377M</span></span>
* <span data-ttu-id="65451-115">GXF</span><span class="sxs-lookup"><span data-stu-id="65451-115">GXF</span></span>
* <span data-ttu-id="65451-116">MPEG-2 aktarım akışları</span><span class="sxs-lookup"><span data-stu-id="65451-116">MPEG-2 Transport Streams</span></span>
* <span data-ttu-id="65451-117">MPEG-2 Program akışları</span><span class="sxs-lookup"><span data-stu-id="65451-117">MPEG-2 Program Streams</span></span>
* <span data-ttu-id="65451-118">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="65451-118">MPEG-4/MP4</span></span>
* <span data-ttu-id="65451-119">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="65451-119">Windows Media/ASF</span></span>
* <span data-ttu-id="65451-120">AVI (sıkıştırılmamış 8 bit/10 bit)</span><span class="sxs-lookup"><span data-stu-id="65451-120">AVI (Uncompressed 8bit/10bit)</span></span>

### <a name="input-video-codecs"></a><span data-ttu-id="65451-121">Görüntü codec bileşenleri giriş</span><span class="sxs-lookup"><span data-stu-id="65451-121">Input Video Codecs</span></span>
* <span data-ttu-id="65451-122">AVC 8 bit/10-bit too4:2:2 AVCIntra dahil olmak üzere, ayarlama</span><span class="sxs-lookup"><span data-stu-id="65451-122">AVC 8-bit/10-bit, up too4:2:2, including AVCIntra</span></span>
* <span data-ttu-id="65451-123">Hırslı DNxHD (içinde MXF)</span><span class="sxs-lookup"><span data-stu-id="65451-123">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="65451-124">DVCPro/DVCProHD (içinde MXF)</span><span class="sxs-lookup"><span data-stu-id="65451-124">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="65451-125">JPEG2000</span><span class="sxs-lookup"><span data-stu-id="65451-125">JPEG2000</span></span>
* <span data-ttu-id="65451-126">MPEG-2 (too422 profili ve yüksek düzey; XDCAM, XDCAM HD, XDCAM IMX, CableLabs® ve D10 gibi çeşitleri dahil)</span><span class="sxs-lookup"><span data-stu-id="65451-126">MPEG-2 (up too422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="65451-127">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="65451-127">MPEG-1</span></span>
* <span data-ttu-id="65451-128">Windows Media Video/VC-1</span><span class="sxs-lookup"><span data-stu-id="65451-128">Windows Media Video/VC-1</span></span>

### <a name="input-audio-codecs"></a><span data-ttu-id="65451-129">Giriş ses codec bileşenleri</span><span class="sxs-lookup"><span data-stu-id="65451-129">Input Audio Codecs</span></span>
* <span data-ttu-id="65451-130">AES (SMPTE 331 M ve 302 M, AES3 2003)</span><span class="sxs-lookup"><span data-stu-id="65451-130">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="65451-131">Dolby® E</span><span class="sxs-lookup"><span data-stu-id="65451-131">Dolby® E</span></span>
* <span data-ttu-id="65451-132">Dolby® dijital (AC3)</span><span class="sxs-lookup"><span data-stu-id="65451-132">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="65451-133">AAC (AAC-LC, HE AAC ve AAC-HEv2; too5.1 yukarı)</span><span class="sxs-lookup"><span data-stu-id="65451-133">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up too5.1)</span></span>
* <span data-ttu-id="65451-134">MPEG Katman 2</span><span class="sxs-lookup"><span data-stu-id="65451-134">MPEG Layer 2</span></span>
* <span data-ttu-id="65451-135">MP3 (MPEG-1 ses Katman 3)</span><span class="sxs-lookup"><span data-stu-id="65451-135">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="65451-136">Windows Media Ses</span><span class="sxs-lookup"><span data-stu-id="65451-136">Windows Media Audio</span></span>
* <span data-ttu-id="65451-137">WAV/PCM</span><span class="sxs-lookup"><span data-stu-id="65451-137">WAV/PCM</span></span>

## <span data-ttu-id="65451-138"><a id="output_format"></a>Medya Kodlayıcısı Premium iş akışı Çıkış biçimleri ve codec bileşenleri</span><span class="sxs-lookup"><span data-stu-id="65451-138"><a id="output_format"></a>Media Encoder Premium Workflow Output Formats and Codecs</span></span>
<span data-ttu-id="65451-139">Merhaba aşağıdaki bölümde bu medya işlemcisi çıktısı olarak desteklenen hello codec bileşenleri ve dosya biçimlerini listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="65451-139">hello following section lists hello codecs and file formats that are supported as output from this media processor.</span></span>

### <a name="output-containerfile-formats"></a><span data-ttu-id="65451-140">Çıktı kapsayıcı/dosya biçimleri</span><span class="sxs-lookup"><span data-stu-id="65451-140">Output Container/File Formats</span></span>
* <span data-ttu-id="65451-141">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="65451-141">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="65451-142">MXF (OP1a, XDCAM ve AS02)</span><span class="sxs-lookup"><span data-stu-id="65451-142">MXF (OP1a, XDCAM and AS02)</span></span>
* <span data-ttu-id="65451-143">DPP (AS11 dahil)</span><span class="sxs-lookup"><span data-stu-id="65451-143">DPP (including AS11)</span></span>
* <span data-ttu-id="65451-144">GXF</span><span class="sxs-lookup"><span data-stu-id="65451-144">GXF</span></span>
* <span data-ttu-id="65451-145">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="65451-145">MPEG-4/MP4</span></span>
* <span data-ttu-id="65451-146">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="65451-146">Windows Media/ASF</span></span>
* <span data-ttu-id="65451-147">AVI (sıkıştırılmamış 8 bit/10 bit)</span><span class="sxs-lookup"><span data-stu-id="65451-147">AVI (Uncompressed 8bit/10bit)</span></span>
* <span data-ttu-id="65451-148">Kesintisiz akış dosyası biçimi (PIFF 1.3)</span><span class="sxs-lookup"><span data-stu-id="65451-148">Smooth Streaming File Format (PIFF 1.3)</span></span>
* <span data-ttu-id="65451-149">MPEG-TS</span><span class="sxs-lookup"><span data-stu-id="65451-149">MPEG-TS</span></span> 

### <a name="output-video-codecs"></a><span data-ttu-id="65451-150">Çıktı görüntü codec bileşenleri</span><span class="sxs-lookup"><span data-stu-id="65451-150">Output Video Codecs</span></span>
* <span data-ttu-id="65451-151">AVC (H.264; 8 bit; yukarı tooHigh profili düzeyi 5.2; 4K Ultra HD; AVC içi)</span><span class="sxs-lookup"><span data-stu-id="65451-151">AVC (H.264; 8-bit; up tooHigh Profile, Level 5.2; 4K Ultra HD; AVC Intra)</span></span>
* <span data-ttu-id="65451-152">Hırslı DNxHD (içinde MXF)</span><span class="sxs-lookup"><span data-stu-id="65451-152">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="65451-153">DVCPro/DVCProHD (içinde MXF)</span><span class="sxs-lookup"><span data-stu-id="65451-153">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="65451-154">MPEG-2 (too422 profili ve yüksek düzey; XDCAM, XDCAM HD, XDCAM IMX, CableLabs® ve D10 gibi çeşitleri dahil)</span><span class="sxs-lookup"><span data-stu-id="65451-154">MPEG-2 (up too422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="65451-155">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="65451-155">MPEG-1</span></span>
* <span data-ttu-id="65451-156">Windows Media Video/VC-1</span><span class="sxs-lookup"><span data-stu-id="65451-156">Windows Media Video/VC-1</span></span>
* <span data-ttu-id="65451-157">JPEG küçük resim oluşturma</span><span class="sxs-lookup"><span data-stu-id="65451-157">JPEG thumbnail creation</span></span>

### <a name="output-audio-codecs"></a><span data-ttu-id="65451-158">Çıktı ses codec bileşenleri</span><span class="sxs-lookup"><span data-stu-id="65451-158">Output Audio Codecs</span></span>
* <span data-ttu-id="65451-159">AES (SMPTE 331 M ve 302 M, AES3 2003)</span><span class="sxs-lookup"><span data-stu-id="65451-159">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="65451-160">Dolby® dijital (AC3)</span><span class="sxs-lookup"><span data-stu-id="65451-160">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="65451-161">Dolby® dijital Plus (E-AC3) too7.1 ayarlama</span><span class="sxs-lookup"><span data-stu-id="65451-161">Dolby® Digital Plus (E-AC3) up too7.1</span></span>
* <span data-ttu-id="65451-162">AAC (AAC-LC, HE AAC ve AAC-HEv2; too5.1 yukarı)</span><span class="sxs-lookup"><span data-stu-id="65451-162">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up too5.1)</span></span>
* <span data-ttu-id="65451-163">MPEG Katman 2</span><span class="sxs-lookup"><span data-stu-id="65451-163">MPEG Layer 2</span></span>
* <span data-ttu-id="65451-164">MP3 (MPEG-1 ses Katman 3)</span><span class="sxs-lookup"><span data-stu-id="65451-164">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="65451-165">Windows Media Ses</span><span class="sxs-lookup"><span data-stu-id="65451-165">Windows Media Audio</span></span>

>[!NOTE]
><span data-ttu-id="65451-166">TooDolby kodlamak varsa® dijital (AC3) hello çıktı yalnızca bir ISO MP4 dosyasına yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="65451-166">If you encode tooDolby® Digital (AC3), hello output can only be written into an ISO MP4 file.</span></span>

## <span data-ttu-id="65451-167"><a id="closed_captioning"></a>Kapalı açıklamalı alt yazıları için destek</span><span class="sxs-lookup"><span data-stu-id="65451-167"><a id="closed_captioning"></a>Support for Closed Captioning</span></span>
<span data-ttu-id="65451-168">Üzerinde alma **Medya Kodlayıcısı Premium iş akışı** destekler:</span><span class="sxs-lookup"><span data-stu-id="65451-168">On ingest, **Media Encoder Premium Workflow** supports:</span></span>

1. <span data-ttu-id="65451-169">SCC dosyaları</span><span class="sxs-lookup"><span data-stu-id="65451-169">SCC files</span></span>
2. <span data-ttu-id="65451-170">SMPTE TT dosyaları</span><span class="sxs-lookup"><span data-stu-id="65451-170">SMPTE-TT files</span></span>
3. <span data-ttu-id="65451-171">CEA-608/CEA-708 – kullanıcı verilerini (H.264 başlangıç akışları, ATSC/53, SCTE20 SHİ iletilerin) gerçekleştirilen veya bulunabilecek veri MXF/GXF dosyaları olarak gerçekleştirilen</span><span class="sxs-lookup"><span data-stu-id="65451-171">CEA-608/CEA-708 – carried as user data (SEI messages of H.264 elementary streams, ATSC/53, SCTE20) or carried as ancillary data in MXF/GXF files</span></span>
4. <span data-ttu-id="65451-172">STL alt başlık dosyaları</span><span class="sxs-lookup"><span data-stu-id="65451-172">STL subtitle files</span></span>

<span data-ttu-id="65451-173">Çıktı, aşağıdaki seçenekleri şu hello kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="65451-173">On output, hello following options are available:</span></span>

1. <span data-ttu-id="65451-174">CEA 608 tooCEA 708 çevirisi</span><span class="sxs-lookup"><span data-stu-id="65451-174">CEA-608 tooCEA-708 translation</span></span>
2. <span data-ttu-id="65451-175">CEA-608/CEA-708 geçirmek aracılığıyla (H.264 başlangıç akışları SHİ iletilerinde katıştırılmış veya olarak bulunabilecek verileri MXF dosyalarında taşınan)</span><span class="sxs-lookup"><span data-stu-id="65451-175">CEA-608/CEA-708 pass through (embedded in SEI messages of H.264 elementary streams, or carried as ancillary data in MXF files)</span></span>
3. <span data-ttu-id="65451-176">SCC</span><span class="sxs-lookup"><span data-stu-id="65451-176">SCC</span></span>
4. <span data-ttu-id="65451-177">SMPTE zaman aşımına metinden (kaynak CEA 608 SMPTE RP2052 başına; DFXP dosya oluşturma dahil)</span><span class="sxs-lookup"><span data-stu-id="65451-177">SMPTE Timed Text (from source CEA-608 per SMPTE RP2052; including DFXP file creation)</span></span>
5. <span data-ttu-id="65451-178">SRT altyazısı dosyası</span><span class="sxs-lookup"><span data-stu-id="65451-178">SRT Subtitle file</span></span>
6. <span data-ttu-id="65451-179">DVB altyazısı akışlar</span><span class="sxs-lookup"><span data-stu-id="65451-179">DVB subtitle streams</span></span>

<span data-ttu-id="65451-180">Not: tüm çıkış biçimleri yukarıda hello Azure Media Services akış aracılığıyla teslim için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="65451-180">Note: not all of hello above output formats are supported for delivery via streaming in Azure Media Services.</span></span>

## <a name="known-issues"></a><span data-ttu-id="65451-181">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="65451-181">Known issues</span></span>
<span data-ttu-id="65451-182">Giriş videonuzun kapalı açıklamalı alt yazı içermiyorsa hello varlık hala boş bir TTML dosya içerecektir çıktı.</span><span class="sxs-lookup"><span data-stu-id="65451-182">If your input video does not contain closed captioning, hello output Asset will still contain an empty TTML file.</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="65451-183">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="65451-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="65451-184">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="65451-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

