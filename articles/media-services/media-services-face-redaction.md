---
title: "Azure medya Analizi ile aaaRedact yüzeyleri | Microsoft Docs"
description: "Bu konuda, nasıl Azure medya Analizi ile tooredact bakarken gösterilir."
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
ms.openlocfilehash: 1f5688a8c6374151c526a9c702b904d8c3e46164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a><span data-ttu-id="0e4a7-103">Azure medya Analizi ile yüzeyleri Redaksiyon</span><span class="sxs-lookup"><span data-stu-id="0e4a7-103">Redact faces with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="0e4a7-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0e4a7-104">Overview</span></span>
<span data-ttu-id="0e4a7-105">**Azure Media Redactor** olan bir [Azure medya analizi](media-services-analytics-overview.md) medya işlemcisi (MP) ölçeklenebilir yüz Redaksiyon hello bulutta sunar.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="0e4a7-106">Yüz Redaksiyon sipariş tooblur yüzeyleri seçilen kişilerin, video, toomodify sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-106">Face redaction enables you toomodify your video in order tooblur faces of selected individuals.</span></span> <span data-ttu-id="0e4a7-107">Toouse hello yüz Redaksiyon hizmeti ortak güvenliği ve haber medya senaryolarda isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-107">You may want toouse hello face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="0e4a7-108">Saat tooredact el ile birden çok yüzeyleri içeren çekimi birkaç dakika sürebilir, ancak bu hizmet hello yüz ile birkaç basit adımla Redaksiyon işlem gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-108">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service hello face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="0e4a7-109">Daha fazla bilgi için bkz: [bu](https://azure.microsoft.com/blog/azure-media-redactor/) blogu.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="0e4a7-110">Bu konu hakkında ayrıntılar verir **Azure medya Redactor** ve gösterir nasıl toouse .NET için Media Services SDK'sı ile.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-110">This topic gives details about **Azure Media Redactor** and shows how toouse it with Media Services SDK for .NET.</span></span>

<span data-ttu-id="0e4a7-111">Merhaba **Azure medya Redactor** MP şu anda önizlemede.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-111">hello **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="0e4a7-112">Tüm ortak Azure bölgeleri yanı sıra ABD devlet kurumları ve Çin veri merkezleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-112">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="0e4a7-113">Bu önizleme şu anda ücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-113">This preview is currently free of charge.</span></span> 

## <a name="face-redaction-modes"></a><span data-ttu-id="0e4a7-114">Yüz Redaksiyon modları</span><span class="sxs-lookup"><span data-stu-id="0e4a7-114">Face redaction modes</span></span>
<span data-ttu-id="0e4a7-115">Böylece Hello aynı tek diğer açıları bulanık her çerçevesinde video yüz algılama ve hello yüz izleme tarafından yüz Redaksiyon works her ikisi de iletir ve geriye doğru zaman içindeki nesne.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-115">Facial redaction works by detecting faces in every frame of video and tracking hello face object both forwards and backwards in time, so that hello same individual can be blurred from other angles as well.</span></span> <span data-ttu-id="0e4a7-116">Merhaba otomatik Redaksiyon işlemi çok karmaşık olduğu ve her zaman % 100'istenen çıkış, bu nedenle medya analizi, çeşitli şekillerde toomodify hello son çıktı sağlar üretmez.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-116">hello automated redaction process is very complex and does not always produce 100% of desired output, for this reason Media Analytics provides you with a couple of ways toomodify hello final output.</span></span>

<span data-ttu-id="0e4a7-117">Toplama tooa tamamen otomatik modda hello Seçimi/Kaldır-selection kimlikleri listesini aracılığıyla bulunan yazıtipleri, sağlayan iki geçişi iş akışı yok.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-117">In addition tooa fully automatic mode, there is a two-pass workflow which allows hello selection/de-selection of found faces via a list of IDs.</span></span> <span data-ttu-id="0e4a7-118">Ayrıca, toomake çerçeve ayarlamalar hello MP rastgele JSON biçiminde bir meta veri dosyası kullanır.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-118">Also, toomake arbitrary per frame adjustments hello MP uses a metadata file in JSON format.</span></span> <span data-ttu-id="0e4a7-119">Bu iş akışı bölündüğünü **Çözümle** ve **Redact** modları.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-119">This workflow is split into **Analyze** and **Redact** modes.</span></span> <span data-ttu-id="0e4a7-120">Her iki görevi bir işe çalıştıran tek bir geçiş iki modda hello birleştirebilirsiniz. Bu mod adlı **birleştirilmiş**.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-120">You can combine hello two modes in a single pass that runs both tasks in one job; this mode is called **Combined**.</span></span>

### <a name="combined-mode"></a><span data-ttu-id="0e4a7-121">Birleşik modu</span><span class="sxs-lookup"><span data-stu-id="0e4a7-121">Combined mode</span></span>
<span data-ttu-id="0e4a7-122">Bu Redaksiyonu yapılmış bir mp4 otomatik olarak giriş herhangi bir el ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-122">This will produce a redacted mp4 automatically without any manual input.</span></span>

| <span data-ttu-id="0e4a7-123">Aşama</span><span class="sxs-lookup"><span data-stu-id="0e4a7-123">Stage</span></span> | <span data-ttu-id="0e4a7-124">Dosya adı</span><span class="sxs-lookup"><span data-stu-id="0e4a7-124">File Name</span></span> | <span data-ttu-id="0e4a7-125">Notlar</span><span class="sxs-lookup"><span data-stu-id="0e4a7-125">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0e4a7-126">Giriş varlık</span><span class="sxs-lookup"><span data-stu-id="0e4a7-126">Input asset</span></span> |<span data-ttu-id="0e4a7-127">foo.bar</span><span class="sxs-lookup"><span data-stu-id="0e4a7-127">foo.bar</span></span> |<span data-ttu-id="0e4a7-128">Video WMV, MOV veya MP4 biçimindeki</span><span class="sxs-lookup"><span data-stu-id="0e4a7-128">Video in WMV, MOV, or MP4 format</span></span> |
| <span data-ttu-id="0e4a7-129">Giriş yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0e4a7-129">Input config</span></span> |<span data-ttu-id="0e4a7-130">İş yapılandırması hazır</span><span class="sxs-lookup"><span data-stu-id="0e4a7-130">Job configuration preset</span></span> |<span data-ttu-id="0e4a7-131">{'version':'1.0 ', 'Seçenekler': {'modu': 'birleştirilmiş'}}</span><span class="sxs-lookup"><span data-stu-id="0e4a7-131">{'version':'1.0', 'options': {'mode':'combined'}}</span></span> |
| <span data-ttu-id="0e4a7-132">Çıkış varlık</span><span class="sxs-lookup"><span data-stu-id="0e4a7-132">Output asset</span></span> |<span data-ttu-id="0e4a7-133">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="0e4a7-133">foo_redacted.mp4</span></span> |<span data-ttu-id="0e4a7-134">Uygulanan Bulanıklaştırma ile video</span><span class="sxs-lookup"><span data-stu-id="0e4a7-134">Video with blurring applied</span></span> |

#### <a name="input-example"></a><span data-ttu-id="0e4a7-135">Giriş örnek:</span><span class="sxs-lookup"><span data-stu-id="0e4a7-135">Input example:</span></span>
[<span data-ttu-id="0e4a7-136">Bu videoyu izleyin</span><span class="sxs-lookup"><span data-stu-id="0e4a7-136">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a><span data-ttu-id="0e4a7-137">Çıkış örneği:</span><span class="sxs-lookup"><span data-stu-id="0e4a7-137">Output example:</span></span>
[<span data-ttu-id="0e4a7-138">Bu videoyu izleyin</span><span class="sxs-lookup"><span data-stu-id="0e4a7-138">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a><span data-ttu-id="0e4a7-139">Mod Çözümle</span><span class="sxs-lookup"><span data-stu-id="0e4a7-139">Analyze mode</span></span>
<span data-ttu-id="0e4a7-140">Merhaba **analiz** geçişi hello iki geçişi iş akışının bir video girdi alır ve yüz konumların bir JSON dosyası oluşturur ve her jpg görüntüleri yüz algılandı.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-140">hello **analyze** pass of hello two-pass workflow takes a video input and produces a JSON file of face locations, and jpg images of each detected face.</span></span>

| <span data-ttu-id="0e4a7-141">Aşama</span><span class="sxs-lookup"><span data-stu-id="0e4a7-141">Stage</span></span> | <span data-ttu-id="0e4a7-142">Dosya adı</span><span class="sxs-lookup"><span data-stu-id="0e4a7-142">File Name</span></span> | <span data-ttu-id="0e4a7-143">Notlar</span><span class="sxs-lookup"><span data-stu-id="0e4a7-143">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0e4a7-144">Giriş varlık</span><span class="sxs-lookup"><span data-stu-id="0e4a7-144">Input asset</span></span> |<span data-ttu-id="0e4a7-145">foo.bar</span><span class="sxs-lookup"><span data-stu-id="0e4a7-145">foo.bar</span></span> |<span data-ttu-id="0e4a7-146">Video WMV, MPV veya MP4 biçimindeki</span><span class="sxs-lookup"><span data-stu-id="0e4a7-146">Video in WMV, MPV, or MP4 format</span></span> |
| <span data-ttu-id="0e4a7-147">Giriş yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0e4a7-147">Input config</span></span> |<span data-ttu-id="0e4a7-148">İş yapılandırması hazır</span><span class="sxs-lookup"><span data-stu-id="0e4a7-148">Job configuration preset</span></span> |<span data-ttu-id="0e4a7-149">{'version':'1.0 ', 'Seçenekler': {'modu': 'çözümleyin'}}</span><span class="sxs-lookup"><span data-stu-id="0e4a7-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span></span> |
| <span data-ttu-id="0e4a7-150">Çıkış varlık</span><span class="sxs-lookup"><span data-stu-id="0e4a7-150">Output asset</span></span> |<span data-ttu-id="0e4a7-151">foo_annotations.JSON</span><span class="sxs-lookup"><span data-stu-id="0e4a7-151">foo_annotations.json</span></span> |<span data-ttu-id="0e4a7-152">Ek açıklama verileri JSON biçiminde yüz konumu.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-152">Annotation data of face locations in JSON format.</span></span> <span data-ttu-id="0e4a7-153">Bu, hello kullanıcı toomodify hello sınırlayıcı kutular Bulanıklaştırma tarafından düzenlenebilir.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-153">This can be edited by hello user toomodify hello blurring bounding boxes.</span></span> <span data-ttu-id="0e4a7-154">Aşağıdaki örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-154">See sample below.</span></span> |
| <span data-ttu-id="0e4a7-155">Çıkış varlık</span><span class="sxs-lookup"><span data-stu-id="0e4a7-155">Output asset</span></span> |<span data-ttu-id="0e4a7-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span><span class="sxs-lookup"><span data-stu-id="0e4a7-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span></span> |<span data-ttu-id="0e4a7-157">Yüz burada hello numarası hello labelId hello yazıtipinin gösterir, her kırpılmış jpg algılandı</span><span class="sxs-lookup"><span data-stu-id="0e4a7-157">A cropped jpg of each detected face, where hello number indicates hello labelId of hello face</span></span> |

#### <a name="output-example"></a><span data-ttu-id="0e4a7-158">Çıkış örneği:</span><span class="sxs-lookup"><span data-stu-id="0e4a7-158">Output example:</span></span>

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

### <a name="redact-mode"></a><span data-ttu-id="0e4a7-159">Mod Redaksiyon</span><span class="sxs-lookup"><span data-stu-id="0e4a7-159">Redact mode</span></span>
<span data-ttu-id="0e4a7-160">Merhaba ikinci geçişi hello iş akışının çok sayıda tek bir varlığa birleştirilmelidir girişleri alır.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-160">hello second pass of hello workflow takes a larger number of inputs that must be combined into a single asset.</span></span>

<span data-ttu-id="0e4a7-161">Bu kimlikleri tooblur, hello özgün video ve hello ek açıklamaları JSON listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-161">This includes a list of IDs tooblur, hello original video, and hello annotations JSON.</span></span> <span data-ttu-id="0e4a7-162">Bu mod hello ek açıklamaları tooapply hello giriş video Bulanıklaştırma kullanır.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-162">This mode uses hello annotations tooapply blurring on hello input video.</span></span>

<span data-ttu-id="0e4a7-163">Merhaba hello Çözümle geçişi çıktısını hello özgün video içermez.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-163">hello output from hello Analyze pass does not include hello original video.</span></span> <span data-ttu-id="0e4a7-164">Merhaba video hello giriş varlık hello Redact modu görev için içine yüklenir ve hello birincil dosya olarak seçili toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-164">hello video needs toobe uploaded into hello input asset for hello Redact mode task and selected as hello primary file.</span></span>

| <span data-ttu-id="0e4a7-165">Aşama</span><span class="sxs-lookup"><span data-stu-id="0e4a7-165">Stage</span></span> | <span data-ttu-id="0e4a7-166">Dosya adı</span><span class="sxs-lookup"><span data-stu-id="0e4a7-166">File Name</span></span> | <span data-ttu-id="0e4a7-167">Notlar</span><span class="sxs-lookup"><span data-stu-id="0e4a7-167">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0e4a7-168">Giriş varlık</span><span class="sxs-lookup"><span data-stu-id="0e4a7-168">Input asset</span></span> |<span data-ttu-id="0e4a7-169">foo.bar</span><span class="sxs-lookup"><span data-stu-id="0e4a7-169">foo.bar</span></span> |<span data-ttu-id="0e4a7-170">Video WMV, MPV veya MP4 biçimindeki.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-170">Video in WMV, MPV, or MP4 format.</span></span> <span data-ttu-id="0e4a7-171">Aynı 1. adım olduğu gibi video.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-171">Same video as in step 1.</span></span> |
| <span data-ttu-id="0e4a7-172">Giriş varlık</span><span class="sxs-lookup"><span data-stu-id="0e4a7-172">Input asset</span></span> |<span data-ttu-id="0e4a7-173">foo_annotations.JSON</span><span class="sxs-lookup"><span data-stu-id="0e4a7-173">foo_annotations.json</span></span> |<span data-ttu-id="0e4a7-174">meta veri dosyasından birinci aşaması, isteğe bağlı değişiklik yapılması açısından ek açıklamaları.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-174">annotations metadata file from phase one, with optional modifications.</span></span> |
| <span data-ttu-id="0e4a7-175">Giriş varlık</span><span class="sxs-lookup"><span data-stu-id="0e4a7-175">Input asset</span></span> |<span data-ttu-id="0e4a7-176">foo_IDList.txt (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="0e4a7-176">foo_IDList.txt (Optional)</span></span> |<span data-ttu-id="0e4a7-177">İsteğe bağlı yeni bir satırla ayrılmış yüz kimlikleri tooredact listesi.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-177">Optional new line separated list of face IDs tooredact.</span></span> <span data-ttu-id="0e4a7-178">Boş bırakılırsa, bu tüm yüzeyleri bulanıklaştırır.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-178">If left blank, this blurs all faces.</span></span> |
| <span data-ttu-id="0e4a7-179">Giriş yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0e4a7-179">Input config</span></span> |<span data-ttu-id="0e4a7-180">İş yapılandırması hazır</span><span class="sxs-lookup"><span data-stu-id="0e4a7-180">Job configuration preset</span></span> |<span data-ttu-id="0e4a7-181">{'version':'1.0 ', 'Seçenekler': {'modu': 'Redaksiyon'}}</span><span class="sxs-lookup"><span data-stu-id="0e4a7-181">{'version':'1.0', 'options': {'mode':'redact'}}</span></span> |
| <span data-ttu-id="0e4a7-182">Çıkış varlık</span><span class="sxs-lookup"><span data-stu-id="0e4a7-182">Output asset</span></span> |<span data-ttu-id="0e4a7-183">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="0e4a7-183">foo_redacted.mp4</span></span> |<span data-ttu-id="0e4a7-184">Ek açıklamalar uygulanan Bulanıklaştırma ile video dayalı</span><span class="sxs-lookup"><span data-stu-id="0e4a7-184">Video with blurring applied based on annotations</span></span> |

#### <a name="example-output"></a><span data-ttu-id="0e4a7-185">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="0e4a7-185">Example output</span></span>
<span data-ttu-id="0e4a7-186">Seçili bir Kimliğine sahip bir IDList hello çıktısını budur.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-186">This is hello output from an IDList with one ID selected.</span></span>

[<span data-ttu-id="0e4a7-187">Bu videoyu izleyin</span><span class="sxs-lookup"><span data-stu-id="0e4a7-187">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

<span data-ttu-id="0e4a7-188">Örnek foo_IDList.txt</span><span class="sxs-lookup"><span data-stu-id="0e4a7-188">Example foo_IDList.txt</span></span>
 
     1
     2
     3

## <a name="blur-types"></a><span data-ttu-id="0e4a7-189">Türleri ölçeklendirilmelidir</span><span class="sxs-lookup"><span data-stu-id="0e4a7-189">Blur types</span></span>

<span data-ttu-id="0e4a7-190">Merhaba, **birleştirilmiş** veya **Redact** modu, seçim yapabileceğiniz hello JSON giriş yapılandırılması yoluyla 5 farklı Bulanıklaştırma modu vardır: **düşük**, **Med**, **Yüksek**, **hata ayıklama**, ve **siyah**.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-190">In hello **Combined** or **Redact** mode, there are 5 different blur modes you can choose from via hello JSON input configuration: **Low**, **Med**, **High**, **Debug**, and **Black**.</span></span> <span data-ttu-id="0e4a7-191">Varsayılan olarak **Med** kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-191">By default **Med** is used.</span></span>

<span data-ttu-id="0e4a7-192">Merhaba örnekleri türleri aşağıdaki ölçeklendirilmelidir bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-192">You can find samples of hello blur types below.</span></span>

### <a name="example-json"></a><span data-ttu-id="0e4a7-193">Örnek JSON:</span><span class="sxs-lookup"><span data-stu-id="0e4a7-193">Example JSON:</span></span>

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a><span data-ttu-id="0e4a7-194">Düşük</span><span class="sxs-lookup"><span data-stu-id="0e4a7-194">Low</span></span>

![Düşük](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a><span data-ttu-id="0e4a7-196">MED</span><span class="sxs-lookup"><span data-stu-id="0e4a7-196">Med</span></span>

![MED](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a><span data-ttu-id="0e4a7-198">Yüksek</span><span class="sxs-lookup"><span data-stu-id="0e4a7-198">High</span></span>

![Yüksek](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a><span data-ttu-id="0e4a7-200">Hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="0e4a7-200">Debug</span></span>

![Hata ayıklama](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a><span data-ttu-id="0e4a7-202">Siyah</span><span class="sxs-lookup"><span data-stu-id="0e4a7-202">Black</span></span>

![Siyah](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-hello-output-json-file"></a><span data-ttu-id="0e4a7-204">Merhaba çıkış JSON dosyasının öğeleri</span><span class="sxs-lookup"><span data-stu-id="0e4a7-204">Elements of hello output JSON file</span></span>

<span data-ttu-id="0e4a7-205">Merhaba Redaksiyon MP Yüksek duyarlılık yüz konumu algılama ve video çerçevesinde too64 İnsan Yüz Yukarı algılayabilir izleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-205">hello Redaction MP provides high precision face location detection and tracking that can detect up too64 human faces in a video frame.</span></span> <span data-ttu-id="0e4a7-206">Tamamen çıplak yüzeyleri yan yüz ve küçük yazıtipleri hello en iyi sonuçlar sağlayın (değerinden büyük veya eşit too24x24 piksel) zor olan.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-206">Frontal faces provide hello best results, while side faces and small faces (less than or equal too24x24 pixels) are challenging.</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a><span data-ttu-id="0e4a7-207">.NET örnek kod</span><span class="sxs-lookup"><span data-stu-id="0e4a7-207">.NET sample code</span></span>

<span data-ttu-id="0e4a7-208">Merhaba aşağıdaki program gösterir nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="0e4a7-208">hello following program shows how to:</span></span>

1. <span data-ttu-id="0e4a7-209">Bir varlık oluşturun ve hello varlığa bir medya dosyasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-209">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="0e4a7-210">Json hazır aşağıdaki hello içeren bir yapılandırma dosyasına dayalı yüz Redaksiyon görevle ilgili bir iş oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-210">Create a job with a face redaction task based on a configuration file that contains hello following json preset.</span></span> 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
3. <span data-ttu-id="0e4a7-211">Merhaba çıkış JSON dosyalarını indirin.</span><span class="sxs-lookup"><span data-stu-id="0e4a7-211">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="0e4a7-212">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0e4a7-212">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="0e4a7-213">Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="0e4a7-213">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="0e4a7-214">Örnek</span><span class="sxs-lookup"><span data-stu-id="0e4a7-214">Example</span></span>

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
        // Read values from hello App.config file.
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

            // Run hello FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download hello job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload hello input media file toostorage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference tooAzure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from hello specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify hello input asset.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

            // Use hello following event handler toocheck job progress.  
            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

            // Launch hello job.
            job.Submit();

            // Check job execution and wait for job toofinish.
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

            progressJobTask.Wait();

            // If job state is Error, hello event handling
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

## <a name="next-steps"></a><span data-ttu-id="0e4a7-215">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0e4a7-215">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0e4a7-216">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="0e4a7-216">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="0e4a7-217">İlgili bağlantılar</span><span class="sxs-lookup"><span data-stu-id="0e4a7-217">Related links</span></span>
[<span data-ttu-id="0e4a7-218">Azure Media Services Analytics a genel bakış</span><span class="sxs-lookup"><span data-stu-id="0e4a7-218">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="0e4a7-219">Azure medya analizi gösterileri</span><span class="sxs-lookup"><span data-stu-id="0e4a7-219">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

