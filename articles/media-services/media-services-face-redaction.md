---
title: "Azure medya Analizi ile yüzeyleri Redaksiyon | Microsoft Docs"
description: "Bu konuda, Azure medya Analizi ile yüzeyleri Redaksiyon gösterilmiştir."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5b6d8b8c-5f4d-4fef-b3d6-dc22c6b5a0f5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;
ms.openlocfilehash: 747f3ae1a7484515083c590942de3da22568cd39
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a><span data-ttu-id="deeda-103">Azure medya Analizi ile yüzeyleri Redaksiyon</span><span class="sxs-lookup"><span data-stu-id="deeda-103">Redact faces with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="deeda-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="deeda-104">Overview</span></span>
<span data-ttu-id="deeda-105">**Azure Media Redactor** olan bir [Azure medya analizi](media-services-analytics-overview.md) medya işlemcisi (MP) ölçeklenebilir yüz Redaksiyon bulutta sunar.</span><span class="sxs-lookup"><span data-stu-id="deeda-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="deeda-106">Yüz Redaksiyon seçili kişiler yüzeyleri ölçeklendirilmelidir için videonuzu değiştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="deeda-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span></span> <span data-ttu-id="deeda-107">Genel güvenlik ve haber medya senaryolarda yüz Redaksiyon hizmeti kullanmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="deeda-107">You may want to use the face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="deeda-108">Birden çok yüzeyleri içeren çekimi birkaç dakika el ile Redaksiyon saat sürebilir, ancak bu hizmet ile birkaç basit adımla yüz Redaksiyon işlem gerektirir.</span><span class="sxs-lookup"><span data-stu-id="deeda-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="deeda-109">Daha fazla bilgi için bkz: [bu](https://azure.microsoft.com/blog/azure-media-redactor/) blogu.</span><span class="sxs-lookup"><span data-stu-id="deeda-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="deeda-110">Bu konu hakkında ayrıntılar verir **Azure medya Redactor** ve Media Services SDK'sı ile .NET için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="deeda-110">This topic gives details about **Azure Media Redactor** and shows how to use it with Media Services SDK for .NET.</span></span>

<span data-ttu-id="deeda-111">**Azure medya Redactor** MP şu anda önizlemede.</span><span class="sxs-lookup"><span data-stu-id="deeda-111">The **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="deeda-112">Tüm ortak Azure bölgeleri yanı sıra ABD devlet kurumları ve Çin veri merkezleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="deeda-112">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="deeda-113">Bu önizleme şu anda ücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="deeda-113">This preview is currently free of charge.</span></span> 

## <a name="face-redaction-modes"></a><span data-ttu-id="deeda-114">Yüz Redaksiyon modları</span><span class="sxs-lookup"><span data-stu-id="deeda-114">Face redaction modes</span></span>
<span data-ttu-id="deeda-115">Böylece aynı tek diğer açıları bulanık yüz Redaksiyon her çerçevesinde video yüz algılama ve her iki yüz nesne, zaman içindeki iletir ve geriye doğru izleme çalışır.</span><span class="sxs-lookup"><span data-stu-id="deeda-115">Facial redaction works by detecting faces in every frame of video and tracking the face object both forwards and backwards in time, so that the same individual can be blurred from other angles as well.</span></span> <span data-ttu-id="deeda-116">Otomatik Redaksiyon çok karmaşık bir işlemdir ve mu değil her zaman ürettiği % 100'ünü bu nedenle medya analizi için istenen çıkış sağlar, çeşitli şekillerde son çıkışı değiştirilecek.</span><span class="sxs-lookup"><span data-stu-id="deeda-116">The automated redaction process is very complex and does not always produce 100% of desired output, for this reason Media Analytics provides you with a couple of ways to modify the final output.</span></span>

<span data-ttu-id="deeda-117">Tamamen otomatik modu ek olarak, seçim/Kaldır-selection kimlikleri listesini aracılığıyla bulunan yazıtipleri, sağlayan iki geçişi iş akışı yok.</span><span class="sxs-lookup"><span data-stu-id="deeda-117">In addition to a fully automatic mode, there is a two-pass workflow which allows the selection/de-selection of found faces via a list of IDs.</span></span> <span data-ttu-id="deeda-118">Ayrıca, çerçeve ayarlamalar MP rasgele yapmak için bir meta veri dosyası JSON biçiminde kullanır.</span><span class="sxs-lookup"><span data-stu-id="deeda-118">Also, to make arbitrary per frame adjustments the MP uses a metadata file in JSON format.</span></span> <span data-ttu-id="deeda-119">Bu iş akışı bölündüğünü **Çözümle** ve **Redact** modları.</span><span class="sxs-lookup"><span data-stu-id="deeda-119">This workflow is split into **Analyze** and **Redact** modes.</span></span> <span data-ttu-id="deeda-120">Her iki görevi bir işe çalıştıran tek bir geçiş iki modda birleştirebilirsiniz. Bu mod adlı **birleştirilmiş**.</span><span class="sxs-lookup"><span data-stu-id="deeda-120">You can combine the two modes in a single pass that runs both tasks in one job; this mode is called **Combined**.</span></span>

### <a name="combined-mode"></a><span data-ttu-id="deeda-121">Birleşik modu</span><span class="sxs-lookup"><span data-stu-id="deeda-121">Combined mode</span></span>
<span data-ttu-id="deeda-122">Bu Redaksiyonu yapılmış bir mp4 otomatik olarak giriş herhangi bir el ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="deeda-122">This will produce a redacted mp4 automatically without any manual input.</span></span>

| <span data-ttu-id="deeda-123">Aşama</span><span class="sxs-lookup"><span data-stu-id="deeda-123">Stage</span></span> | <span data-ttu-id="deeda-124">Dosya adı</span><span class="sxs-lookup"><span data-stu-id="deeda-124">File Name</span></span> | <span data-ttu-id="deeda-125">Notlar</span><span class="sxs-lookup"><span data-stu-id="deeda-125">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="deeda-126">Giriş varlık</span><span class="sxs-lookup"><span data-stu-id="deeda-126">Input asset</span></span> |<span data-ttu-id="deeda-127">foo.bar</span><span class="sxs-lookup"><span data-stu-id="deeda-127">foo.bar</span></span> |<span data-ttu-id="deeda-128">Video WMV, MOV veya MP4 biçimindeki</span><span class="sxs-lookup"><span data-stu-id="deeda-128">Video in WMV, MOV, or MP4 format</span></span> |
| <span data-ttu-id="deeda-129">Giriş yapılandırma</span><span class="sxs-lookup"><span data-stu-id="deeda-129">Input config</span></span> |<span data-ttu-id="deeda-130">İş yapılandırması hazır</span><span class="sxs-lookup"><span data-stu-id="deeda-130">Job configuration preset</span></span> |<span data-ttu-id="deeda-131">{'version':'1.0 ', 'Seçenekler': {'modu': 'birleştirilmiş'}}</span><span class="sxs-lookup"><span data-stu-id="deeda-131">{'version':'1.0', 'options': {'mode':'combined'}}</span></span> |
| <span data-ttu-id="deeda-132">Çıkış varlık</span><span class="sxs-lookup"><span data-stu-id="deeda-132">Output asset</span></span> |<span data-ttu-id="deeda-133">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="deeda-133">foo_redacted.mp4</span></span> |<span data-ttu-id="deeda-134">Uygulanan Bulanıklaştırma ile video</span><span class="sxs-lookup"><span data-stu-id="deeda-134">Video with blurring applied</span></span> |

#### <a name="input-example"></a><span data-ttu-id="deeda-135">Giriş örnek:</span><span class="sxs-lookup"><span data-stu-id="deeda-135">Input example:</span></span>
[<span data-ttu-id="deeda-136">Bu videoyu izleyin</span><span class="sxs-lookup"><span data-stu-id="deeda-136">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a><span data-ttu-id="deeda-137">Çıkış örneği:</span><span class="sxs-lookup"><span data-stu-id="deeda-137">Output example:</span></span>
[<span data-ttu-id="deeda-138">Bu videoyu izleyin</span><span class="sxs-lookup"><span data-stu-id="deeda-138">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a><span data-ttu-id="deeda-139">Mod Çözümle</span><span class="sxs-lookup"><span data-stu-id="deeda-139">Analyze mode</span></span>
<span data-ttu-id="deeda-140">**Analiz** geçişi iki geçişi iş akışının video girdi alır ve yüz konumların bir JSON dosyası oluşturur ve her birinin jpg görüntüleri yüz algılandı.</span><span class="sxs-lookup"><span data-stu-id="deeda-140">The **analyze** pass of the two-pass workflow takes a video input and produces a JSON file of face locations, and jpg images of each detected face.</span></span>

| <span data-ttu-id="deeda-141">Aşama</span><span class="sxs-lookup"><span data-stu-id="deeda-141">Stage</span></span> | <span data-ttu-id="deeda-142">Dosya adı</span><span class="sxs-lookup"><span data-stu-id="deeda-142">File Name</span></span> | <span data-ttu-id="deeda-143">Notlar</span><span class="sxs-lookup"><span data-stu-id="deeda-143">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="deeda-144">Giriş varlık</span><span class="sxs-lookup"><span data-stu-id="deeda-144">Input asset</span></span> |<span data-ttu-id="deeda-145">foo.bar</span><span class="sxs-lookup"><span data-stu-id="deeda-145">foo.bar</span></span> |<span data-ttu-id="deeda-146">Video WMV, MPV veya MP4 biçimindeki</span><span class="sxs-lookup"><span data-stu-id="deeda-146">Video in WMV, MPV, or MP4 format</span></span> |
| <span data-ttu-id="deeda-147">Giriş yapılandırma</span><span class="sxs-lookup"><span data-stu-id="deeda-147">Input config</span></span> |<span data-ttu-id="deeda-148">İş yapılandırması hazır</span><span class="sxs-lookup"><span data-stu-id="deeda-148">Job configuration preset</span></span> |<span data-ttu-id="deeda-149">{'version':'1.0 ', 'Seçenekler': {'modu': 'çözümleyin'}}</span><span class="sxs-lookup"><span data-stu-id="deeda-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span></span> |
| <span data-ttu-id="deeda-150">Çıkış varlık</span><span class="sxs-lookup"><span data-stu-id="deeda-150">Output asset</span></span> |<span data-ttu-id="deeda-151">foo_annotations.JSON</span><span class="sxs-lookup"><span data-stu-id="deeda-151">foo_annotations.json</span></span> |<span data-ttu-id="deeda-152">Ek açıklama verileri JSON biçiminde yüz konumu.</span><span class="sxs-lookup"><span data-stu-id="deeda-152">Annotation data of face locations in JSON format.</span></span> <span data-ttu-id="deeda-153">Bu sınırlayıcı kutular Bulanıklaştırma değiştirmek için kullanıcı tarafından düzenlenebilir.</span><span class="sxs-lookup"><span data-stu-id="deeda-153">This can be edited by the user to modify the blurring bounding boxes.</span></span> <span data-ttu-id="deeda-154">Aşağıdaki örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="deeda-154">See sample below.</span></span> |
| <span data-ttu-id="deeda-155">Çıkış varlık</span><span class="sxs-lookup"><span data-stu-id="deeda-155">Output asset</span></span> |<span data-ttu-id="deeda-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span><span class="sxs-lookup"><span data-stu-id="deeda-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span></span> |<span data-ttu-id="deeda-157">Yüz burada yüz labelId sayıyı belirtir, her kırpılmış jpg algılandı</span><span class="sxs-lookup"><span data-stu-id="deeda-157">A cropped jpg of each detected face, where the number indicates the labelId of the face</span></span> |

#### <a name="output-example"></a><span data-ttu-id="deeda-158">Çıkış örneği:</span><span class="sxs-lookup"><span data-stu-id="deeda-158">Output example:</span></span>

    {
      "version": 1,
      "timescale": 24000,
      "offset": 0,
      "framerate": 23.976,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 48048,
          "interval": 1001,
          "events": [
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [
              {
                "index": 13,
                "id": 1138,
                "x": 0.29537,
                "y": -0.18987,
                "width": 0.36239,
                "height": 0.80335
              },
              {
                "index": 13,
                "id": 2028,
                "x": 0.60427,
                "y": 0.16098,
                "width": 0.26958,
                "height": 0.57943
              }
            ],

    … truncated

### <a name="redact-mode"></a><span data-ttu-id="deeda-159">Mod Redaksiyon</span><span class="sxs-lookup"><span data-stu-id="deeda-159">Redact mode</span></span>
<span data-ttu-id="deeda-160">İkinci geçişi iş akışının çok sayıda tek bir varlığa birleştirilmelidir girişleri alır.</span><span class="sxs-lookup"><span data-stu-id="deeda-160">The second pass of the workflow takes a larger number of inputs that must be combined into a single asset.</span></span>

<span data-ttu-id="deeda-161">Bu ölçeklendirilmelidir kimlikleri, özgün video ve ek açıklamalar JSON listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="deeda-161">This includes a list of IDs to blur, the original video, and the annotations JSON.</span></span> <span data-ttu-id="deeda-162">Bu mod, video giriş Bulanıklaştırma uygulamak için ek açıklamalar kullanır.</span><span class="sxs-lookup"><span data-stu-id="deeda-162">This mode uses the annotations to apply blurring on the input video.</span></span>

<span data-ttu-id="deeda-163">Çözümle geçişi çıktısını özgün video içermez.</span><span class="sxs-lookup"><span data-stu-id="deeda-163">The output from the Analyze pass does not include the original video.</span></span> <span data-ttu-id="deeda-164">Video Redact modu görev için giriş varlık içine yüklenebilir ve birincil dosya olarak seçili gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="deeda-164">The video needs to be uploaded into the input asset for the Redact mode task and selected as the primary file.</span></span>

| <span data-ttu-id="deeda-165">Aşama</span><span class="sxs-lookup"><span data-stu-id="deeda-165">Stage</span></span> | <span data-ttu-id="deeda-166">Dosya adı</span><span class="sxs-lookup"><span data-stu-id="deeda-166">File Name</span></span> | <span data-ttu-id="deeda-167">Notlar</span><span class="sxs-lookup"><span data-stu-id="deeda-167">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="deeda-168">Giriş varlık</span><span class="sxs-lookup"><span data-stu-id="deeda-168">Input asset</span></span> |<span data-ttu-id="deeda-169">foo.bar</span><span class="sxs-lookup"><span data-stu-id="deeda-169">foo.bar</span></span> |<span data-ttu-id="deeda-170">Video WMV, MPV veya MP4 biçimindeki.</span><span class="sxs-lookup"><span data-stu-id="deeda-170">Video in WMV, MPV, or MP4 format.</span></span> <span data-ttu-id="deeda-171">Aynı 1. adım olduğu gibi video.</span><span class="sxs-lookup"><span data-stu-id="deeda-171">Same video as in step 1.</span></span> |
| <span data-ttu-id="deeda-172">Giriş varlık</span><span class="sxs-lookup"><span data-stu-id="deeda-172">Input asset</span></span> |<span data-ttu-id="deeda-173">foo_annotations.JSON</span><span class="sxs-lookup"><span data-stu-id="deeda-173">foo_annotations.json</span></span> |<span data-ttu-id="deeda-174">meta veri dosyasından birinci aşaması, isteğe bağlı değişiklik yapılması açısından ek açıklamaları.</span><span class="sxs-lookup"><span data-stu-id="deeda-174">annotations metadata file from phase one, with optional modifications.</span></span> |
| <span data-ttu-id="deeda-175">Giriş varlık</span><span class="sxs-lookup"><span data-stu-id="deeda-175">Input asset</span></span> |<span data-ttu-id="deeda-176">foo_IDList.txt (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="deeda-176">foo_IDList.txt (Optional)</span></span> |<span data-ttu-id="deeda-177">İsteğe bağlı yeni bir satırla ayrılmış yüz Redaksiyon kimliklerinin listesi.</span><span class="sxs-lookup"><span data-stu-id="deeda-177">Optional new line separated list of face IDs to redact.</span></span> <span data-ttu-id="deeda-178">Boş bırakılırsa, bu tüm yüzeyleri bulanıklaştırır.</span><span class="sxs-lookup"><span data-stu-id="deeda-178">If left blank, this blurs all faces.</span></span> |
| <span data-ttu-id="deeda-179">Giriş yapılandırma</span><span class="sxs-lookup"><span data-stu-id="deeda-179">Input config</span></span> |<span data-ttu-id="deeda-180">İş yapılandırması hazır</span><span class="sxs-lookup"><span data-stu-id="deeda-180">Job configuration preset</span></span> |<span data-ttu-id="deeda-181">{'version':'1.0 ', 'Seçenekler': {'modu': 'Redaksiyon'}}</span><span class="sxs-lookup"><span data-stu-id="deeda-181">{'version':'1.0', 'options': {'mode':'redact'}}</span></span> |
| <span data-ttu-id="deeda-182">Çıkış varlık</span><span class="sxs-lookup"><span data-stu-id="deeda-182">Output asset</span></span> |<span data-ttu-id="deeda-183">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="deeda-183">foo_redacted.mp4</span></span> |<span data-ttu-id="deeda-184">Ek açıklamalar uygulanan Bulanıklaştırma ile video dayalı</span><span class="sxs-lookup"><span data-stu-id="deeda-184">Video with blurring applied based on annotations</span></span> |

#### <a name="example-output"></a><span data-ttu-id="deeda-185">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="deeda-185">Example output</span></span>
<span data-ttu-id="deeda-186">Seçili bir Kimliğine sahip bir IDList çıkışı budur.</span><span class="sxs-lookup"><span data-stu-id="deeda-186">This is the output from an IDList with one ID selected.</span></span>

[<span data-ttu-id="deeda-187">Bu videoyu izleyin</span><span class="sxs-lookup"><span data-stu-id="deeda-187">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

<span data-ttu-id="deeda-188">Örnek foo_IDList.txt</span><span class="sxs-lookup"><span data-stu-id="deeda-188">Example foo_IDList.txt</span></span>
 
     1
     2
     3

## <a name="blur-types"></a><span data-ttu-id="deeda-189">Türleri ölçeklendirilmelidir</span><span class="sxs-lookup"><span data-stu-id="deeda-189">Blur types</span></span>

<span data-ttu-id="deeda-190">İçinde **birleştirilmiş** veya **Redact** modu, seçim yapabileceğiniz JSON giriş yapılandırma 5 farklı Bulanıklaştırma modu vardır: **düşük**, **Med**, **Yüksek**, **hata ayıklama**, ve **siyah**.</span><span class="sxs-lookup"><span data-stu-id="deeda-190">In the **Combined** or **Redact** mode, there are 5 different blur modes you can choose from via the JSON input configuration: **Low**, **Med**, **High**, **Debug**, and **Black**.</span></span> <span data-ttu-id="deeda-191">Varsayılan olarak **Med** kullanılır.</span><span class="sxs-lookup"><span data-stu-id="deeda-191">By default **Med** is used.</span></span>

<span data-ttu-id="deeda-192">Bulanıklaştırma türlerinin örnekleri bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="deeda-192">You can find samples of the blur types below.</span></span>

### <a name="example-json"></a><span data-ttu-id="deeda-193">Örnek JSON:</span><span class="sxs-lookup"><span data-stu-id="deeda-193">Example JSON:</span></span>

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a><span data-ttu-id="deeda-194">Düşük</span><span class="sxs-lookup"><span data-stu-id="deeda-194">Low</span></span>

![Düşük](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a><span data-ttu-id="deeda-196">MED</span><span class="sxs-lookup"><span data-stu-id="deeda-196">Med</span></span>

![MED](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a><span data-ttu-id="deeda-198">Yüksek</span><span class="sxs-lookup"><span data-stu-id="deeda-198">High</span></span>

![Yüksek](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a><span data-ttu-id="deeda-200">Hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="deeda-200">Debug</span></span>

![Hata ayıklama](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a><span data-ttu-id="deeda-202">Siyah</span><span class="sxs-lookup"><span data-stu-id="deeda-202">Black</span></span>

![Siyah](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-the-output-json-file"></a><span data-ttu-id="deeda-204">Çıkış JSON dosyasının öğeleri</span><span class="sxs-lookup"><span data-stu-id="deeda-204">Elements of the output JSON file</span></span>

<span data-ttu-id="deeda-205">İzleme özelliği en fazla 64 İnsan yüzeyleri video çerçevede algılayabilir ve yüksek düzeyde hassasiyet yüz konumu algılama Redaksiyon MP sağlar.</span><span class="sxs-lookup"><span data-stu-id="deeda-205">The Redaction MP provides high precision face location detection and tracking that can detect up to 64 human faces in a video frame.</span></span> <span data-ttu-id="deeda-206">Yan yüz sırasında ve küçük yazıtipleri (küçük veya eşittir 24 x 24 piksel) zor, en iyi sonuçlar tamamen çıplak yüzeyleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="deeda-206">Frontal faces provide the best results, while side faces and small faces (less than or equal to 24x24 pixels) are challenging.</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a><span data-ttu-id="deeda-207">.NET örnek kod</span><span class="sxs-lookup"><span data-stu-id="deeda-207">.NET sample code</span></span>

<span data-ttu-id="deeda-208">Aşağıdaki program gösterir nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="deeda-208">The following program shows how to:</span></span>

1. <span data-ttu-id="deeda-209">Bir varlık oluşturun ve varlığa bir medya dosyasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="deeda-209">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="deeda-210">Aşağıdaki json hazır içeren bir yapılandırma dosyasına dayalı yüz Redaksiyon görevle ilgili bir iş oluşturun.</span><span class="sxs-lookup"><span data-stu-id="deeda-210">Create a job with a face redaction task based on a configuration file that contains the following json preset.</span></span> 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
3. <span data-ttu-id="deeda-211">Çıkış JSON dosyalarını indirin.</span><span class="sxs-lookup"><span data-stu-id="deeda-211">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="deeda-212">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="deeda-212">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="deeda-213">Geliştirme ortamınızı kurun ve app.config dosyanızı [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md) bölümünde açıklandığı gibi bağlantı bilgileriyle doldurun.</span><span class="sxs-lookup"><span data-stu-id="deeda-213">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="deeda-214">Örnek</span><span class="sxs-lookup"><span data-stu-id="deeda-214">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace FaceRedaction
    {
        class Program
        {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Run the FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download the job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload the input media file to storage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference to Azure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from the specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with the encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify the input asset.
            task.InputAssets.Add(asset);

            // Add an output asset to contain the results of the job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

            // Use the following event handler to check job progress.  
            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

            // Launch the job.
            job.Submit();

            // Check job execution and wait for job to finish.
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

            progressJobTask.Wait();

            // If job state is Error, the event handling
            // method for job progress should log errors.  Here we check
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
            ErrorDetail error = job.Tasks.First().ErrorDetails.First();
            Console.WriteLine(string.Format("Error: {0}. {1}",
                            error.Code,
                            error.Message));
            return null;
            }

            return job.OutputMediaAssets[0];
        }

        static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
        {
            IAsset asset = _context.Assets.Create(assetName, options);

            var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
            assetFile.Upload(filePath);

            return asset;
        }

        static void DownloadAsset(IAsset asset, string outputDirectory)
        {
            foreach (IAssetFile file in asset.AssetFiles)
            {
            file.Download(Path.Combine(outputDirectory, file.Name));
            }
        }

        static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors
            .Where(p => p.Name == mediaProcessorName)
            .ToList()
            .OrderBy(p => new Version(p.Version))
            .LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                   mediaProcessorName));

            return processor;
        }

        static private void StateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);

            switch (e.CurrentState)
            {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("Job is finished.");
                Console.WriteLine();
                break;
            case JobState.Canceling:
            case JobState.Queued:
            case JobState.Scheduled:
            case JobState.Processing:
                Console.WriteLine("Please wait...\n");
                break;
            case JobState.Canceled:
            case JobState.Error:
                // Cast sender as a job.
                IJob job = (IJob)sender;
                // Display or log error details as needed.
                // LogJobStop(job.Id);
                break;
            default:
                break;
            }
        }
        }
    }

## <a name="next-steps"></a><span data-ttu-id="deeda-215">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="deeda-215">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="deeda-216">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="deeda-216">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="deeda-217">İlgili bağlantılar</span><span class="sxs-lookup"><span data-stu-id="deeda-217">Related links</span></span>
[<span data-ttu-id="deeda-218">Azure Media Services Analytics a genel bakış</span><span class="sxs-lookup"><span data-stu-id="deeda-218">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="deeda-219">Azure medya analizi gösterileri</span><span class="sxs-lookup"><span data-stu-id="deeda-219">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

