---
title: "Medya Kodlayıcısı standart biçimleri ve codec bileşenleri"
description: "Bu konuda Medya Kodlayıcısı standart biçimleri ve codec bileşenleri genel bakış sağlar."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: f334b1ce-2f56-4968-a019-f0a2b0016d9f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 1115408443e11c8b0d26b83217c5f63e4b6ba819
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="media-encoder-standard-formats-and-codecs"></a><span data-ttu-id="82beb-103">Media Encoder Standard Biçimleri ve Kodlayıcılar</span><span class="sxs-lookup"><span data-stu-id="82beb-103">Media Encoder Standard Formats and Codecs</span></span>
<span data-ttu-id="82beb-104">Bu belge, Medya Kodlayıcısı standart ile kullanabileceğiniz dışa aktarma dosyası biçimi ve en yaygın alma listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="82beb-104">This document contains a list of the most common import and export file formats that you can use with Media Encoder Standard.</span></span>

## <a name="input-containerfile-formats"></a><span data-ttu-id="82beb-105">Kapsayıcı/dosya biçimleri giriş</span><span class="sxs-lookup"><span data-stu-id="82beb-105">Input Container/File Formats</span></span>
| <span data-ttu-id="82beb-106">Dosya biçimleri (dosya uzantıları)</span><span class="sxs-lookup"><span data-stu-id="82beb-106">File formats (file extensions)</span></span> | <span data-ttu-id="82beb-107">Destekleniyor</span><span class="sxs-lookup"><span data-stu-id="82beb-107">Supported</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="82beb-108">(İle H.264 ve AAC codec bileşenleri) FLV (.flv)</span><span class="sxs-lookup"><span data-stu-id="82beb-108">FLV (with H.264 and AAC codecs) (.flv)</span></span> |<span data-ttu-id="82beb-109">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-109">Yes</span></span> |
| <span data-ttu-id="82beb-110">MXF (.mxf)</span><span class="sxs-lookup"><span data-stu-id="82beb-110">MXF    (.mxf)</span></span> |<span data-ttu-id="82beb-111">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-111">Yes</span></span> |
| <span data-ttu-id="82beb-112">GXF (.gxf)</span><span class="sxs-lookup"><span data-stu-id="82beb-112">GXF    (.gxf)</span></span> |<span data-ttu-id="82beb-113">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-113">Yes</span></span> |
| <span data-ttu-id="82beb-114">MPEG2 PS, MPEG2-TS 3GP (.ts, .ps, .3gp, .3gpp, .mpg)</span><span class="sxs-lookup"><span data-stu-id="82beb-114">MPEG2-PS, MPEG2-TS, 3GP (.ts, .ps, .3gp, .3gpp, .mpg)</span></span> |<span data-ttu-id="82beb-115">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-115">Yes</span></span> |
| <span data-ttu-id="82beb-116">Windows Media Video (WMV) / ASF (.wmv, .asf)</span><span class="sxs-lookup"><span data-stu-id="82beb-116">Windows Media Video (WMV)/ASF (.wmv, .asf)</span></span> |<span data-ttu-id="82beb-117">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-117">Yes</span></span> |
| <span data-ttu-id="82beb-118">AVI (sıkıştırılmamış 8 bit/10 bit) (.avi)</span><span class="sxs-lookup"><span data-stu-id="82beb-118">AVI (Uncompressed 8bit/10bit) (.avi)</span></span> |<span data-ttu-id="82beb-119">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-119">Yes</span></span> |
| <span data-ttu-id="82beb-120">MP4 (.mp4, .m4a, .m4v) / ISMV (.isma, .ismv)</span><span class="sxs-lookup"><span data-stu-id="82beb-120">MP4 (.mp4, .m4a, .m4v)/ISMV (.isma, .ismv)</span></span> |<span data-ttu-id="82beb-121">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-121">Yes</span></span> |
| <span data-ttu-id="82beb-122">[Microsoft Dijital Video Recording(DVR-MS)](https://msdn.microsoft.com/library/windows/desktop/dd692984) (.dvr-ms)</span><span class="sxs-lookup"><span data-stu-id="82beb-122">[Microsoft Digital Video Recording(DVR-MS)](https://msdn.microsoft.com/library/windows/desktop/dd692984) (.dvr-ms)</span></span> |<span data-ttu-id="82beb-123">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-123">Yes</span></span> |
| <span data-ttu-id="82beb-124">Matroska/WebM (.mkv)</span><span class="sxs-lookup"><span data-stu-id="82beb-124">Matroska/WebM (.mkv)</span></span> |<span data-ttu-id="82beb-125">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-125">Yes</span></span> |
| <span data-ttu-id="82beb-126">WAVE/WAV (.wav)</span><span class="sxs-lookup"><span data-stu-id="82beb-126">WAVE/WAV (.wav)</span></span> |<span data-ttu-id="82beb-127">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-127">Yes</span></span> |
| <span data-ttu-id="82beb-128">QuickTime (.mov)</span><span class="sxs-lookup"><span data-stu-id="82beb-128">QuickTime (.mov)</span></span> |<span data-ttu-id="82beb-129">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-129">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="82beb-130">Yukarıdaki daha yaygın olarak karşılaşılan dosya uzantıları listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="82beb-130">Above is a list of the more commonly encountered file extensions.</span></span> <span data-ttu-id="82beb-131">Medya Kodlayıcısı standart destek diğer birçok (örneğin: .m2ts, .mpeg2video, .qt).</span><span class="sxs-lookup"><span data-stu-id="82beb-131">Media Encoder Standard does support many others (for example: .m2ts, .mpeg2video, .qt).</span></span> <span data-ttu-id="82beb-132">Lütfen bir dosya kodlamak deneyin ve biçimi desteklenmiyor ilgili bir hata iletisi alırsanız bir geri bildirim sağlamak [burada](https://feedback.azure.com/forums/169396-media-services/category/144411-encoding-and-processing/).</span><span class="sxs-lookup"><span data-stu-id="82beb-132">If you try to encode a file and you get an error message about the format not being supported, please provide a feedback [here](https://feedback.azure.com/forums/169396-media-services/category/144411-encoding-and-processing/).</span></span>
> 
> 

### <a name="audio-formats-in-input-containers"></a><span data-ttu-id="82beb-133">Giriş kapsayıcılarında ses biçimleri</span><span class="sxs-lookup"><span data-stu-id="82beb-133">Audio formats in input containers</span></span>
<span data-ttu-id="82beb-134">Medya Kodlayıcısı standart giriş kapsayıcıları ses aşağıdaki biçimlerde taşıyan destekler:</span><span class="sxs-lookup"><span data-stu-id="82beb-134">Media Encoder Standard supports carrying the following audio formats in input containers:</span></span>

* <span data-ttu-id="82beb-135">MXF, GXF ve QuickTime dosyaları araya eklemeli stereo ile ses izleri veya 5.1 örnekleri olan</span><span class="sxs-lookup"><span data-stu-id="82beb-135">MXF, GXF and QuickTime files which have audio tracks with interleaved stereo or 5.1 samples</span></span>

<span data-ttu-id="82beb-136">or</span><span class="sxs-lookup"><span data-stu-id="82beb-136">or</span></span>

* <span data-ttu-id="82beb-137">Burada ses ayrı PCM parçaları aktarılan, ancak kanal eşleme (stereo veya 5.1) dosya meta verileri anlaşılan MXF, GXF ve QuickTime dosyaları</span><span class="sxs-lookup"><span data-stu-id="82beb-137">MXF, GXF and QuickTime files where the audio is carried as separate PCM tracks but the channel mapping (to stereo or 5.1) can be deduced from the file metadata</span></span>

<span data-ttu-id="82beb-138">Açık/kullanıcı tarafından sağlanan kanal eşleme yakın gelecekte sağlanacak için destekleyen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="82beb-138">Note that support for explicit/user-supplied channel mapping will be provided in the near future.</span></span>

## <a name="input-video-codecs"></a><span data-ttu-id="82beb-139">Görüntü codec bileşenleri giriş</span><span class="sxs-lookup"><span data-stu-id="82beb-139">Input Video Codecs</span></span>
| <span data-ttu-id="82beb-140">Görüntü codec bileşenleri giriş</span><span class="sxs-lookup"><span data-stu-id="82beb-140">Input Video Codecs</span></span> | <span data-ttu-id="82beb-141">Destekleniyor</span><span class="sxs-lookup"><span data-stu-id="82beb-141">Supported</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="82beb-142">AVC 8 bit/10-en fazla 4 bit: AVCIntra dahil olmak üzere 2:2</span><span class="sxs-lookup"><span data-stu-id="82beb-142">AVC 8-bit/10-bit, up to 4:2:2, including AVCIntra</span></span> |<span data-ttu-id="82beb-143">8 bit 4:2:0. ve 4:2:2</span><span class="sxs-lookup"><span data-stu-id="82beb-143">8 bit 4:2:0 and 4:2:2</span></span> |
| <span data-ttu-id="82beb-144">Hırslı DNxHD (içinde MXF)</span><span class="sxs-lookup"><span data-stu-id="82beb-144">Avid DNxHD (in MXF)</span></span> |<span data-ttu-id="82beb-145">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-145">Yes</span></span> |
| <span data-ttu-id="82beb-146">DVCPro/DVCProHD (içinde MXF)</span><span class="sxs-lookup"><span data-stu-id="82beb-146">DVCPro/DVCProHD (in MXF)</span></span> |<span data-ttu-id="82beb-147">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-147">Yes</span></span> |
| <span data-ttu-id="82beb-148">Dijital video (DV) (AVI dosyaları)</span><span class="sxs-lookup"><span data-stu-id="82beb-148">Digital video (DV) (in AVI files)</span></span> |<span data-ttu-id="82beb-149">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-149">Yes</span></span> |
| <span data-ttu-id="82beb-150">JPEG 2000</span><span class="sxs-lookup"><span data-stu-id="82beb-150">JPEG 2000</span></span> |<span data-ttu-id="82beb-151">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-151">Yes</span></span> |
| <span data-ttu-id="82beb-152">MPEG-2 (422 profili ve yüksek düzey kadar; XDCAM, XDCAM HD, XDCAM IMX, CableLabs® ve D10 gibi çeşitleri dahil)</span><span class="sxs-lookup"><span data-stu-id="82beb-152">MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span> |<span data-ttu-id="82beb-153">En fazla 422 profili</span><span class="sxs-lookup"><span data-stu-id="82beb-153">Up to 422 Profile</span></span> |
| <span data-ttu-id="82beb-154">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="82beb-154">MPEG-1</span></span> |<span data-ttu-id="82beb-155">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-155">Yes</span></span> |
| <span data-ttu-id="82beb-156">VC-1/WMV9</span><span class="sxs-lookup"><span data-stu-id="82beb-156">VC-1/WMV9</span></span> |<span data-ttu-id="82beb-157">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-157">Yes</span></span> |
| <span data-ttu-id="82beb-158">Canopus denetim merkezini/HQX</span><span class="sxs-lookup"><span data-stu-id="82beb-158">Canopus HQ/HQX</span></span> |<span data-ttu-id="82beb-159">Hayır</span><span class="sxs-lookup"><span data-stu-id="82beb-159">No</span></span> |
| <span data-ttu-id="82beb-160">MPEG-4 bölüm 2</span><span class="sxs-lookup"><span data-stu-id="82beb-160">MPEG-4 Part 2</span></span> |<span data-ttu-id="82beb-161">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-161">Yes</span></span> |
| [<span data-ttu-id="82beb-162">Theora</span><span class="sxs-lookup"><span data-stu-id="82beb-162">Theora</span></span>](https://en.wikipedia.org/wiki/Theora) |<span data-ttu-id="82beb-163">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-163">Yes</span></span> |
| <span data-ttu-id="82beb-164">Sıkıştırılmamış YUV420 veya Ara</span><span class="sxs-lookup"><span data-stu-id="82beb-164">YUV420 uncompressed, or mezzanine</span></span> |<span data-ttu-id="82beb-165">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-165">Yes</span></span> |
| <span data-ttu-id="82beb-166">Apple ProRes 422</span><span class="sxs-lookup"><span data-stu-id="82beb-166">Apple ProRes 422</span></span> |<span data-ttu-id="82beb-167">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-167">Yes</span></span> |
| <span data-ttu-id="82beb-168">Apple ProRes 422 LT</span><span class="sxs-lookup"><span data-stu-id="82beb-168">Apple ProRes 422 LT</span></span> |<span data-ttu-id="82beb-169">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-169">Yes</span></span> |
| <span data-ttu-id="82beb-170">Apple ProRes 422 denetim merkezini</span><span class="sxs-lookup"><span data-stu-id="82beb-170">Apple ProRes 422 HQ</span></span> |<span data-ttu-id="82beb-171">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-171">Yes</span></span> |
| <span data-ttu-id="82beb-172">Apple ProRes Proxy</span><span class="sxs-lookup"><span data-stu-id="82beb-172">Apple ProRes Proxy</span></span> |<span data-ttu-id="82beb-173">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-173">Yes</span></span> |
| <span data-ttu-id="82beb-174">Apple ProRes 4444</span><span class="sxs-lookup"><span data-stu-id="82beb-174">Apple ProRes 4444</span></span> |<span data-ttu-id="82beb-175">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-175">Yes</span></span> |
| <span data-ttu-id="82beb-176">Apple ProRes 4444 XQ</span><span class="sxs-lookup"><span data-stu-id="82beb-176">Apple ProRes 4444 XQ</span></span> |<span data-ttu-id="82beb-177">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-177">Yes</span></span> |

## <a name="input-audio-codecs"></a><span data-ttu-id="82beb-178">Giriş ses codec bileşenleri</span><span class="sxs-lookup"><span data-stu-id="82beb-178">Input Audio Codecs</span></span>
| <span data-ttu-id="82beb-179">Giriş ses codec bileşenleri</span><span class="sxs-lookup"><span data-stu-id="82beb-179">Input Audio Codecs</span></span> | <span data-ttu-id="82beb-180">Destekleniyor</span><span class="sxs-lookup"><span data-stu-id="82beb-180">Supported</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="82beb-181">AAC (AAC-LC, HE AAC ve AAC-HEv2; kadar 5.1)</span><span class="sxs-lookup"><span data-stu-id="82beb-181">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1)</span></span> |<span data-ttu-id="82beb-182">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-182">Yes</span></span> |
| <span data-ttu-id="82beb-183">MPEG Katman 2</span><span class="sxs-lookup"><span data-stu-id="82beb-183">MPEG Layer 2</span></span> |<span data-ttu-id="82beb-184">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-184">Yes</span></span> |
| <span data-ttu-id="82beb-185">MP3 (MPEG-1 ses Katman 3)</span><span class="sxs-lookup"><span data-stu-id="82beb-185">MP3 (MPEG-1 Audio Layer 3)</span></span> |<span data-ttu-id="82beb-186">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-186">Yes</span></span> |
| <span data-ttu-id="82beb-187">Windows Media Ses</span><span class="sxs-lookup"><span data-stu-id="82beb-187">Windows Media Audio</span></span> |<span data-ttu-id="82beb-188">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-188">Yes</span></span> |
| <span data-ttu-id="82beb-189">WAV/PCM</span><span class="sxs-lookup"><span data-stu-id="82beb-189">WAV/PCM</span></span> |<span data-ttu-id="82beb-190">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-190">Yes</span></span> |
| <span data-ttu-id="82beb-191">[FLAC](https://en.wikipedia.org/wiki/FLAC)</a></span><span class="sxs-lookup"><span data-stu-id="82beb-191">[FLAC](https://en.wikipedia.org/wiki/FLAC)</a></span></span> |<span data-ttu-id="82beb-192">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-192">Yes</span></span> |
| [<span data-ttu-id="82beb-193">Geçerli</span><span class="sxs-lookup"><span data-stu-id="82beb-193">Opus</span></span>](http://go.microsoft.com/fwlink/?LinkId=822667) |<span data-ttu-id="82beb-194">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-194">Yes</span></span> |
| <span data-ttu-id="82beb-195">[Vorbis](https://en.wikipedia.org/wiki/Vorbis)</a></span><span class="sxs-lookup"><span data-stu-id="82beb-195">[Vorbis](https://en.wikipedia.org/wiki/Vorbis)</a></span></span> |<span data-ttu-id="82beb-196">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-196">Yes</span></span> |
| <span data-ttu-id="82beb-197">AMR (Uyarlamalı çok hızı)</span><span class="sxs-lookup"><span data-stu-id="82beb-197">AMR (adaptive multi-rate)</span></span> |<span data-ttu-id="82beb-198">Evet</span><span class="sxs-lookup"><span data-stu-id="82beb-198">Yes</span></span> |
| <span data-ttu-id="82beb-199">AES (SMPTE 331 M ve 302 M, AES3 2003)</span><span class="sxs-lookup"><span data-stu-id="82beb-199">AES (SMPTE 331M and 302M, AES3-2003)</span></span> |<span data-ttu-id="82beb-200">Hayır</span><span class="sxs-lookup"><span data-stu-id="82beb-200">No</span></span> |
| <span data-ttu-id="82beb-201">Dolby® E</span><span class="sxs-lookup"><span data-stu-id="82beb-201">Dolby® E</span></span> |<span data-ttu-id="82beb-202">Hayır</span><span class="sxs-lookup"><span data-stu-id="82beb-202">No</span></span> |
| <span data-ttu-id="82beb-203">Dolby® dijital (AC3)</span><span class="sxs-lookup"><span data-stu-id="82beb-203">Dolby® Digital (AC3)</span></span> |<span data-ttu-id="82beb-204">Hayır</span><span class="sxs-lookup"><span data-stu-id="82beb-204">No</span></span> |
| <span data-ttu-id="82beb-205">Dolby® dijital artı (E-AC3)</span><span class="sxs-lookup"><span data-stu-id="82beb-205">Dolby® Digital Plus (E-AC3)</span></span> |<span data-ttu-id="82beb-206">Hayır</span><span class="sxs-lookup"><span data-stu-id="82beb-206">No</span></span> |

## <a name="output-formats-and-codecs"></a><span data-ttu-id="82beb-207">Çıktı biçimi ve codec bileşenleri</span><span class="sxs-lookup"><span data-stu-id="82beb-207">Output Formats and codecs</span></span>
<span data-ttu-id="82beb-208">Aşağıdaki tabloda dışa aktarmak için desteklenen codec bileşenleri ve dosya biçimlerini listeler.</span><span class="sxs-lookup"><span data-stu-id="82beb-208">The following table lists the codecs and file formats that are supported for export.</span></span>

| <span data-ttu-id="82beb-209">Dosya biçimi</span><span class="sxs-lookup"><span data-stu-id="82beb-209">File Format</span></span> | <span data-ttu-id="82beb-210">Görüntü Codec</span><span class="sxs-lookup"><span data-stu-id="82beb-210">Video Codec</span></span> | <span data-ttu-id="82beb-211">Ses Codec</span><span class="sxs-lookup"><span data-stu-id="82beb-211">Audio Codec</span></span> |
| --- | --- | --- |
| <span data-ttu-id="82beb-212">MP4</span><span class="sxs-lookup"><span data-stu-id="82beb-212">MP4</span></span> <br/><br/><span data-ttu-id="82beb-213">(Çoklu bit hızlı MP4 kapsayıcıları dahil)</span><span class="sxs-lookup"><span data-stu-id="82beb-213">(including multi-bitrate MP4 containers)</span></span> |<span data-ttu-id="82beb-214">H.264 (yüksek, ana ve temel profilleri)</span><span class="sxs-lookup"><span data-stu-id="82beb-214">H.264 (High, Main, and Baseline Profiles)</span></span> |<span data-ttu-id="82beb-215">AAC-LC, HE-AAC v1, HE-AAC v2</span><span class="sxs-lookup"><span data-stu-id="82beb-215">AAC-LC, HE-AAC v1, HE-AAC v2</span></span> |
| <span data-ttu-id="82beb-216">MPEG2 TS</span><span class="sxs-lookup"><span data-stu-id="82beb-216">MPEG2-TS</span></span> |<span data-ttu-id="82beb-217">H.264 (yüksek, ana ve temel profilleri)</span><span class="sxs-lookup"><span data-stu-id="82beb-217">H.264 (High, Main, and Baseline Profiles)</span></span> |<span data-ttu-id="82beb-218">AAC-LC, HE-AAC v1, HE-AAC v2</span><span class="sxs-lookup"><span data-stu-id="82beb-218">AAC-LC, HE-AAC v1, HE-AAC v2</span></span> |

## <a name="media-services-learning-paths"></a><span data-ttu-id="82beb-219">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="82beb-219">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="82beb-220">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="82beb-220">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="82beb-221">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="82beb-221">See also</span></span>
[<span data-ttu-id="82beb-222">Azure Media Services ile isteğe bağlı içerik kodlama</span><span class="sxs-lookup"><span data-stu-id="82beb-222">Encoding On-Demand Content with Azure Media Services</span></span>](media-services-encode-asset.md)

[<span data-ttu-id="82beb-223">Medya Kodlayıcısı standart ile kodlamak nasıl</span><span class="sxs-lookup"><span data-stu-id="82beb-223">How to encode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

