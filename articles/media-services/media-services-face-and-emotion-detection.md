---
title: "aaaDetect yüz ve duygu Azure medya Analizi ile | Microsoft Docs"
description: "Bu konuda nasıl toodetect bakarken ve duygular Azure medya Analizi ile gösterilir."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5ca4692c-23f1-451d-9d82-cbc8bf0fd707
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: f58d81d82dde08a694cdb4d92c6bab6a40a9c157
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a><span data-ttu-id="31ee7-103">Yüz ve duygu Azure medya Analizi ile Algıla</span><span class="sxs-lookup"><span data-stu-id="31ee7-103">Detect Face and Emotion with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="31ee7-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="31ee7-104">Overview</span></span>
<span data-ttu-id="31ee7-105">Merhaba **Azure medya yüz algılayıcısı** medya işlemcisi (MP) etkinleştirir, size, toocount, izleme hareketleri ve hatta ölçer İzleyici katılım ve tepki yüz ifadeleri aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="31ee7-105">hello **Azure Media Face Detector** media processor (MP) enables you toocount, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="31ee7-106">Bu hizmet, iki özellik içerir:</span><span class="sxs-lookup"><span data-stu-id="31ee7-106">This service contains two features:</span></span> 

* <span data-ttu-id="31ee7-107">**Yüz algılama**</span><span class="sxs-lookup"><span data-stu-id="31ee7-107">**Face detection**</span></span>
  
    <span data-ttu-id="31ee7-108">Yüz algılama bulur ve video içinde İnsan yüzeyleri izler.</span><span class="sxs-lookup"><span data-stu-id="31ee7-108">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="31ee7-109">Birden çok yüzeyleri algılanabilir ve bunların geçici bir JSON dosyası döndürülen hello zaman ve yer meta verilerle taşırken sonradan izlenmesi.</span><span class="sxs-lookup"><span data-stu-id="31ee7-109">Multiple faces can be detected and subsequently be tracked as they move around, with hello time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="31ee7-110">İzleme sırasında toogive obstructed veya kısaca hello çerçeve bırakın olsa bile hello kişi ekranında dolaşma sırada aynı yönde tutarlı bir kimliği toohello dener.</span><span class="sxs-lookup"><span data-stu-id="31ee7-110">During tracking, it will attempt toogive a consistent ID toohello same face while hello person is moving around on screen, even if they are obstructed or briefly leave hello frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="31ee7-111">Bu hizmet, yüz tanıma gerçekleştirmez.</span><span class="sxs-lookup"><span data-stu-id="31ee7-111">This service does not perform facial recognition.</span></span> <span data-ttu-id="31ee7-112">Merhaba çerçeve ayrıldığında ya da için obstructed hale bir kişi döndürmeleri zaman uzun yeni bir kimlik verilir.</span><span class="sxs-lookup"><span data-stu-id="31ee7-112">An individual who leaves hello frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="31ee7-113">**Duygu algılama**</span><span class="sxs-lookup"><span data-stu-id="31ee7-113">**Emotion detection**</span></span>
  
    <span data-ttu-id="31ee7-114">Duygu algılama hello analiz mutluluk, sadness, Korku, öfke ve daha fazlası da dahil olmak üzere algılandı, hello yüzeyleri birden çok kendini özniteliklerinde döndürür yüz algılama medya işlemcisi isteğe bağlı bir bileşenidir.</span><span class="sxs-lookup"><span data-stu-id="31ee7-114">Emotion Detection is an optional component of hello Face Detection Media Processor that returns analysis on multiple emotional attributes from hello faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

<span data-ttu-id="31ee7-115">Merhaba **Azure medya yüz algılayıcısı** MP şu anda önizlemede.</span><span class="sxs-lookup"><span data-stu-id="31ee7-115">hello **Azure Media Face Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="31ee7-116">Bu konu hakkında ayrıntılar verir **Azure medya yüz algılayıcısı** ve gösterir nasıl toouse .NET için Media Services SDK'sı ile.</span><span class="sxs-lookup"><span data-stu-id="31ee7-116">This topic gives details about  **Azure Media Face Detector** and shows how toouse it with Media Services SDK for .NET.</span></span>

## <a name="face-detector-input-files"></a><span data-ttu-id="31ee7-117">Yüz algılayıcısı giriş dosyaları</span><span class="sxs-lookup"><span data-stu-id="31ee7-117">Face Detector input files</span></span>
<span data-ttu-id="31ee7-118">Video dosyaları.</span><span class="sxs-lookup"><span data-stu-id="31ee7-118">Video files.</span></span> <span data-ttu-id="31ee7-119">Şu anda biçimleri aşağıdaki hello desteklenir: MP4, MOV ve WMV.</span><span class="sxs-lookup"><span data-stu-id="31ee7-119">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="face-detector-output-files"></a><span data-ttu-id="31ee7-120">Yüz algılayıcısı çıktı dosyaları</span><span class="sxs-lookup"><span data-stu-id="31ee7-120">Face Detector output files</span></span>
<span data-ttu-id="31ee7-121">Merhaba yüz algılama ve İzleme API, Yüksek duyarlılık yüz konumu algılama ve bir video too64 İnsan Yüz Yukarı algılayabilir izleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="31ee7-121">hello face detection and tracking API provides high precision face location detection and tracking that can detect up too64 human faces in a video.</span></span> <span data-ttu-id="31ee7-122">Tamamen çıplak yüzeyleri yan yüz ve küçük yazıtipleri hello en iyi sonuçlar sağlayın (değerinden büyük veya eşit too24x24 piksel) olarak doğru olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="31ee7-122">Frontal faces provide hello best results, while side faces and small faces (less than or equal too24x24 pixels) might not be as accurate.</span></span>

<span data-ttu-id="31ee7-123">Merhaba algılanan ve izlenen yüzeyleri döndürülür (sol, üst, genişlik ve yükseklik) koordinatlarıyla yüz kimliği numara belirten bir yanı sıra hello yüzeyleri piksel cinsinden hello görüntüdeki konumunu belirten, tek tek izlenmesini hello.</span><span class="sxs-lookup"><span data-stu-id="31ee7-123">hello detected and tracked faces are returned with coordinates (left, top, width, and height) indicating hello location of faces in hello image in pixels, as well as a face ID number indicating hello tracking of that individual.</span></span> <span data-ttu-id="31ee7-124">Merhaba tamamen çıplak yüz kaybolduğunda veya hello çerçevede çakışan yüz kimliği koşullarda yatkın tooreset birden çok kimliği atanan bazı kişiler kaynaklanan numaralarıdır.</span><span class="sxs-lookup"><span data-stu-id="31ee7-124">Face ID numbers are prone tooreset under circumstances when hello frontal face is lost or overlapped in hello frame, resulting in some individuals getting assigned multiple IDs.</span></span>

## <span data-ttu-id="31ee7-125"><a id="output_elements"></a>Merhaba çıkış JSON dosyasının öğeleri</span><span class="sxs-lookup"><span data-stu-id="31ee7-125"><a id="output_elements"></a>Elements of hello output JSON file</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

<span data-ttu-id="31ee7-126">Yüz algılayıcısı (çok büyük alma durumunda burada hello olayları ayrılır) (burada zamana dayalı yığınlar halinde hello meta verileri bölünmüştür ve yalnızca ihtiyacınız yükleyebilirsiniz) parçalanma ve kesimlere ayırma teknikleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="31ee7-126">Face Detector uses techniques of fragmentation (where hello metadata can be broken up in time-based chunks and you can download only what you need), and segmentation (where hello events are broken up in case they get too large).</span></span> <span data-ttu-id="31ee7-127">Bazı basit hesaplamalar hello veri dönüştürme yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="31ee7-127">Some simple calculations can help you transform hello data.</span></span> <span data-ttu-id="31ee7-128">Örneğin, bir olay 2997 (çizgilerine/sn) bir ölçeğini 6300 (çizgilerine) başlatılan ve kare 29.97 (Çerçeve/sn), ardından hızına:</span><span class="sxs-lookup"><span data-stu-id="31ee7-128">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and framerate of 29.97 (frames/sec), then:</span></span>

* <span data-ttu-id="31ee7-129">Başlat/ölçeği = 2.1 saniye</span><span class="sxs-lookup"><span data-stu-id="31ee7-129">Start/Timescale = 2.1 seconds</span></span>
* <span data-ttu-id="31ee7-130">X frameRate saniye 63 çerçeveler =</span><span class="sxs-lookup"><span data-stu-id="31ee7-130">Seconds x Framerate = 63 frames</span></span>

## <a name="face-detection-input-and-output-example"></a><span data-ttu-id="31ee7-131">Algılama giriş yüz ve örnek çıkış</span><span class="sxs-lookup"><span data-stu-id="31ee7-131">Face detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="31ee7-132">Giriş video</span><span class="sxs-lookup"><span data-stu-id="31ee7-132">Input video</span></span>
[<span data-ttu-id="31ee7-133">Video girişi</span><span class="sxs-lookup"><span data-stu-id="31ee7-133">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="31ee7-134">Görev yapılandırması (hazır)</span><span class="sxs-lookup"><span data-stu-id="31ee7-134">Task configuration (preset)</span></span>
<span data-ttu-id="31ee7-135">Bir görev oluştururken **Azure medya yüz algılayıcısı**, bir yapılandırma hazır belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="31ee7-135">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="31ee7-136">Yapılandırma hazır aşağıdaki hello yalnızca yüz algılama için ' dir.</span><span class="sxs-lookup"><span data-stu-id="31ee7-136">hello following configuration preset is just for face detection.</span></span>

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a><span data-ttu-id="31ee7-137">Öznitelik tanımlarını</span><span class="sxs-lookup"><span data-stu-id="31ee7-137">Attribute descriptions</span></span>
| <span data-ttu-id="31ee7-138">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="31ee7-138">Attribute name</span></span> | <span data-ttu-id="31ee7-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="31ee7-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="31ee7-140">Modu</span><span class="sxs-lookup"><span data-stu-id="31ee7-140">Mode</span></span> |<span data-ttu-id="31ee7-141">Hızlı - hızı, ancak daha az doğru (varsayılan) hızlı işleniyor.</span><span class="sxs-lookup"><span data-stu-id="31ee7-141">Fast - fast processing speed, but less accurate (default).</span></span>|

### <a name="json-output"></a><span data-ttu-id="31ee7-142">JSON çıktısını</span><span class="sxs-lookup"><span data-stu-id="31ee7-142">JSON output</span></span>
<span data-ttu-id="31ee7-143">Aşağıdaki örnek JSON çıktısını hello kesildi.</span><span class="sxs-lookup"><span data-stu-id="31ee7-143">hello following example of JSON output was truncated.</span></span>

    {
    "version": 1,
    "timescale": 30000,
    "offset": 0,
    "framerate": 29.97,
    "width": 1280,
    "height": 720,
    "fragments": [
        {
        "start": 0,
        "duration": 60060
        },
        {
        "start": 60060,
        "duration": 60060,
        "interval": 1001,
        "events": [
            [
            {
                "id": 0,
                "x": 0.519531,
                "y": 0.180556,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517969,
                "y": 0.181944,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517187,
                "y": 0.183333,
                "width": 0.0851562,
                "height": 0.151389
            }
            ],

        . . . 

## <a name="emotion-detection-input-and-output-example"></a><span data-ttu-id="31ee7-144">Giriş ve çıkış duygu algılama örneği</span><span class="sxs-lookup"><span data-stu-id="31ee7-144">Emotion detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="31ee7-145">Giriş video</span><span class="sxs-lookup"><span data-stu-id="31ee7-145">Input video</span></span>
[<span data-ttu-id="31ee7-146">Video girişi</span><span class="sxs-lookup"><span data-stu-id="31ee7-146">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="31ee7-147">Görev yapılandırması (hazır)</span><span class="sxs-lookup"><span data-stu-id="31ee7-147">Task configuration (preset)</span></span>
<span data-ttu-id="31ee7-148">Bir görev oluştururken **Azure medya yüz algılayıcısı**, bir yapılandırma hazır belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="31ee7-148">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="31ee7-149">Merhaba yapılandırma hazır aşağıdaki JSON tabanlı hello duygu algılama üzerinde toocreate belirtir.</span><span class="sxs-lookup"><span data-stu-id="31ee7-149">hello following configuration preset specifies toocreate JSON based on hello emotion detection.</span></span>

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a><span data-ttu-id="31ee7-150">Öznitelik tanımlarını</span><span class="sxs-lookup"><span data-stu-id="31ee7-150">Attribute descriptions</span></span>
| <span data-ttu-id="31ee7-151">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="31ee7-151">Attribute name</span></span> | <span data-ttu-id="31ee7-152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="31ee7-152">Description</span></span> |
| --- | --- |
| <span data-ttu-id="31ee7-153">Modu</span><span class="sxs-lookup"><span data-stu-id="31ee7-153">Mode</span></span> |<span data-ttu-id="31ee7-154">Yazıtipleri: Yalnızca algılama karşılaşıyor.</span><span class="sxs-lookup"><span data-stu-id="31ee7-154">Faces: Only face detection.</span></span><br/><span data-ttu-id="31ee7-155">PerFaceEmotion: her yüz algılama için ayrı ayrı duygu döndür.</span><span class="sxs-lookup"><span data-stu-id="31ee7-155">PerFaceEmotion: Return emotion independently for each face detection.</span></span><br/><span data-ttu-id="31ee7-156">AggregateEmotion: Tüm yüzeyleri çerçevesinde dönüş ortalama duygu değerleri.</span><span class="sxs-lookup"><span data-stu-id="31ee7-156">AggregateEmotion: Return average emotion values for all faces in frame.</span></span> |
| <span data-ttu-id="31ee7-157">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="31ee7-157">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="31ee7-158">AggregateEmotion modunu seçtiyseniz kullanın.</span><span class="sxs-lookup"><span data-stu-id="31ee7-158">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="31ee7-159">Merhaba video kullanılan tooproduce her bir toplama sonucu milisaniye cinsinden belirtir.</span><span class="sxs-lookup"><span data-stu-id="31ee7-159">Specifies hello length of video used tooproduce each aggregate result, in milliseconds.</span></span> |
| <span data-ttu-id="31ee7-160">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="31ee7-160">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="31ee7-161">AggregateEmotion modunu seçtiyseniz kullanın.</span><span class="sxs-lookup"><span data-stu-id="31ee7-161">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="31ee7-162">Hangi sıklığı tooproduce toplama sonuçları ile belirtir.</span><span class="sxs-lookup"><span data-stu-id="31ee7-162">Specifies with what frequency tooproduce aggregate results.</span></span> |

#### <a name="aggregate-defaults"></a><span data-ttu-id="31ee7-163">Birleşik Varsayılanları</span><span class="sxs-lookup"><span data-stu-id="31ee7-163">Aggregate defaults</span></span>
<span data-ttu-id="31ee7-164">Aşağıdaki değerler hello toplama penceresi ve aralığı ayarları için önerilir.</span><span class="sxs-lookup"><span data-stu-id="31ee7-164">Below are recommended values for hello aggregate window and interval settings.</span></span> <span data-ttu-id="31ee7-165">AggregateEmotionWindowMs AggregateEmotionIntervalMs uzun olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="31ee7-165">AggregateEmotionWindowMs should be longer than AggregateEmotionIntervalMs.</span></span>

|| <span data-ttu-id="31ee7-166">Varsayılanları (s)</span><span class="sxs-lookup"><span data-stu-id="31ee7-166">Defaults(s)</span></span> | <span data-ttu-id="31ee7-167">Min(s)</span><span class="sxs-lookup"><span data-stu-id="31ee7-167">Min(s)</span></span> | <span data-ttu-id="31ee7-168">Max(s)</span><span class="sxs-lookup"><span data-stu-id="31ee7-168">Max(s)</span></span> |
|--- | --- | --- | --- |
| <span data-ttu-id="31ee7-169">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="31ee7-169">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="31ee7-170">0.5</span><span class="sxs-lookup"><span data-stu-id="31ee7-170">0.5</span></span> |<span data-ttu-id="31ee7-171">2</span><span class="sxs-lookup"><span data-stu-id="31ee7-171">2</span></span> |<span data-ttu-id="31ee7-172">0.25</span><span class="sxs-lookup"><span data-stu-id="31ee7-172">0.25</span></span>|
| <span data-ttu-id="31ee7-173">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="31ee7-173">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="31ee7-174">0.5</span><span class="sxs-lookup"><span data-stu-id="31ee7-174">0.5</span></span> |<span data-ttu-id="31ee7-175">1</span><span class="sxs-lookup"><span data-stu-id="31ee7-175">1</span></span> |<span data-ttu-id="31ee7-176">0.25</span><span class="sxs-lookup"><span data-stu-id="31ee7-176">0.25</span></span>|

### <a name="json-output"></a><span data-ttu-id="31ee7-177">JSON çıktısını</span><span class="sxs-lookup"><span data-stu-id="31ee7-177">JSON output</span></span>
<span data-ttu-id="31ee7-178">JSON (kesilmiş) toplama duygu tanıma için çıktı:</span><span class="sxs-lookup"><span data-stu-id="31ee7-178">JSON output for aggregate emotion (truncated):</span></span>

    {
     "version": 1,
     "timescale": 30000,
     "offset": 0,
     "framerate": 29.97,
     "width": 1280,
     "height": 720,
     "fragments": [
       {
         "start": 0,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ]
         ]
       },
       {
         "start": 60060,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0.688541,
                 "happiness": 0.0586323,
                 "surprise": 0.227184,
                 "sadness": 0.00945675,
                 "anger": 0.00592107,
                 "disgust": 0.00154993,
                 "fear": 0.00450447,
                 "contempt": 0.0042109
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,

## <a name="limitations"></a><span data-ttu-id="31ee7-179">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="31ee7-179">Limitations</span></span>
* <span data-ttu-id="31ee7-180">desteklenen hello giriş video biçimleri MP4, MOV ve WMV içerir.</span><span class="sxs-lookup"><span data-stu-id="31ee7-180">hello supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="31ee7-181">Merhaba algılanabilir yüz boyutu aralığı 24 x 24 too2048x2048 pikseldir.</span><span class="sxs-lookup"><span data-stu-id="31ee7-181">hello detectable face size range is 24x24 too2048x2048 pixels.</span></span> <span data-ttu-id="31ee7-182">Bu aralık dışında Hello yüzeyleri algılanmaz.</span><span class="sxs-lookup"><span data-stu-id="31ee7-182">hello faces out of this range will not be detected.</span></span>
* <span data-ttu-id="31ee7-183">Her video için hello en fazla döndürülen yüzeyleri 64 sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="31ee7-183">For each video, hello maximum number of faces returned is 64.</span></span>
* <span data-ttu-id="31ee7-184">Bazı yüzeyleri tootechnical zorluklar algılanamayabilir; Örneğin çok büyük yüz açısı (poz head) ve büyük kapanması.</span><span class="sxs-lookup"><span data-stu-id="31ee7-184">Some faces may not be detected due tootechnical challenges; e.g. very large face angles (head-pose), and large occlusion.</span></span> <span data-ttu-id="31ee7-185">Tamamen çıplak ve tamamen yakın yüzler hello en iyi sonuçlar sahip.</span><span class="sxs-lookup"><span data-stu-id="31ee7-185">Frontal and near-frontal faces have hello best results.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="31ee7-186">.NET örnek kod</span><span class="sxs-lookup"><span data-stu-id="31ee7-186">.NET sample code</span></span>

<span data-ttu-id="31ee7-187">Merhaba aşağıdaki program gösterir nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="31ee7-187">hello following program shows how to:</span></span>

1. <span data-ttu-id="31ee7-188">Bir varlık oluşturun ve hello varlığa bir medya dosyasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="31ee7-188">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="31ee7-189">Json hazır aşağıdaki hello içeren bir yapılandırma dosyasına dayalı yüz algılama görevle ilgili bir iş oluşturun.</span><span class="sxs-lookup"><span data-stu-id="31ee7-189">Create a job with a face detection task based on a configuration file that contains hello following json preset.</span></span> 
   
        {
            "version": "1.0"
        }
3. <span data-ttu-id="31ee7-190">Merhaba çıkış JSON dosyalarını indirin.</span><span class="sxs-lookup"><span data-stu-id="31ee7-190">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="31ee7-191">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="31ee7-191">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="31ee7-192">Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="31ee7-192">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="31ee7-193">Örnek</span><span class="sxs-lookup"><span data-stu-id="31ee7-193">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace FaceDetection
    {
        class Program
        {
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

                // Run hello FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference tooAzure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="31ee7-194">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="31ee7-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="31ee7-195">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="31ee7-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="31ee7-196">İlgili bağlantılar</span><span class="sxs-lookup"><span data-stu-id="31ee7-196">Related links</span></span>
[<span data-ttu-id="31ee7-197">Azure Media Services Analytics a genel bakış</span><span class="sxs-lookup"><span data-stu-id="31ee7-197">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="31ee7-198">Azure medya analizi gösterileri</span><span class="sxs-lookup"><span data-stu-id="31ee7-198">Azure Media Analytics demos</span></span>](http://amslabs.azurewebsites.net/demos/Analytics.html)

