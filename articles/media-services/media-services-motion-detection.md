---
title: "Azure medya Analizi ile hareketlerin algılamak | Microsoft Docs"
description: "Azure Media hareket algılayıcısı medya işlemcisi (MP), aksi takdirde uzun ve olaysız video içinde ilgi bölümleri verimli bir şekilde tanımlamak sağlar."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: d144f813-1a55-442f-a895-5c4cb6d0aeae
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: milanga;juliako;
ms.openlocfilehash: 115ad9dfd88062f23d5d17eed8897ce5d2ca8484
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a><span data-ttu-id="aa83e-103">Azure medya Analizi ile hareketlerin Algıla</span><span class="sxs-lookup"><span data-stu-id="aa83e-103">Detect Motions with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="aa83e-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="aa83e-104">Overview</span></span>
<span data-ttu-id="aa83e-105">**Azure medya hareket algılayıcısı** medya işlemcisi (MP), aksi takdirde uzun ve olaysız video içinde ilgi bölümleri verimli bir şekilde tanımlamak sağlar.</span><span class="sxs-lookup"><span data-stu-id="aa83e-105">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="aa83e-106">Hareket algılama statik kamera görüntülerinin video hareket oluştuğu bölümlerini belirlemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="aa83e-106">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span></span> <span data-ttu-id="aa83e-107">Zaman damgaları ve olayın gerçekleştiği sınırlayıcı bölge ile meta verileri içeren bir JSON dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="aa83e-107">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span></span>

<span data-ttu-id="aa83e-108">Doğru güvenlik video akışları hedeflenen, bu teknolojiyi ilgili olayları ve hatalı pozitif sonuç gölgeleri ve aydınlatma değişiklikleri gibi hareket kategorilere yapabiliyor.</span><span class="sxs-lookup"><span data-stu-id="aa83e-108">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="aa83e-109">Bu, güvenlik uyarıları sonsuz ilgisiz olaylarıyla aşırı uzun gözetleme videoların ilgi dakika ayıklayın kullanabilmeye devam ederken adresinize olmadan kamera Akışları'oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="aa83e-109">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from extremely long surveillance videos.</span></span>

<span data-ttu-id="aa83e-110">**Azure medya hareket algılayıcısı** MP şu anda önizlemede.</span><span class="sxs-lookup"><span data-stu-id="aa83e-110">The **Azure Media Motion Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="aa83e-111">Bu konu hakkında ayrıntılar verir **Azure medya hareket algılayıcısı** ve .NET için Media Services SDK'sı ile kullanmak nasıl gösterir</span><span class="sxs-lookup"><span data-stu-id="aa83e-111">This topic gives details about  **Azure Media Motion Detector** and shows how to use it with Media Services SDK for .NET</span></span>

## <a name="motion-detector-input-files"></a><span data-ttu-id="aa83e-112">Hareket algılayıcısı giriş dosyaları</span><span class="sxs-lookup"><span data-stu-id="aa83e-112">Motion Detector input files</span></span>
<span data-ttu-id="aa83e-113">Video dosyaları.</span><span class="sxs-lookup"><span data-stu-id="aa83e-113">Video files.</span></span> <span data-ttu-id="aa83e-114">Şu anda aşağıdaki biçimlerden desteklenir: MP4, MOV ve WMV.</span><span class="sxs-lookup"><span data-stu-id="aa83e-114">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="aa83e-115">Görev yapılandırması (hazır)</span><span class="sxs-lookup"><span data-stu-id="aa83e-115">Task configuration (preset)</span></span>
<span data-ttu-id="aa83e-116">Bir görev oluştururken **Azure medya hareket algılayıcısı**, bir yapılandırma hazır belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="aa83e-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span></span> 

### <a name="parameters"></a><span data-ttu-id="aa83e-117">Parametreler</span><span class="sxs-lookup"><span data-stu-id="aa83e-117">Parameters</span></span>
<span data-ttu-id="aa83e-118">Şu parametreleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="aa83e-118">You can use the following parameters:</span></span>

| <span data-ttu-id="aa83e-119">Ad</span><span class="sxs-lookup"><span data-stu-id="aa83e-119">Name</span></span> | <span data-ttu-id="aa83e-120">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="aa83e-120">Options</span></span> | <span data-ttu-id="aa83e-121">Açıklama</span><span class="sxs-lookup"><span data-stu-id="aa83e-121">Description</span></span> | <span data-ttu-id="aa83e-122">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="aa83e-122">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="aa83e-123">sensitivityLevel</span><span class="sxs-lookup"><span data-stu-id="aa83e-123">sensitivityLevel</span></span> |<span data-ttu-id="aa83e-124">Dize: 'düşük', 'Orta', 'yüksek'</span><span class="sxs-lookup"><span data-stu-id="aa83e-124">String:'low', 'medium', 'high'</span></span> |<span data-ttu-id="aa83e-125">Hangi hareketlerin duyarlılık düzeyinde bildirilen ayarlar.</span><span class="sxs-lookup"><span data-stu-id="aa83e-125">Sets the sensitivity level at which motions is reported.</span></span> <span data-ttu-id="aa83e-126">Hatalı pozitif sonuç miktarını ayarlamak için bunu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="aa83e-126">Adjust this to adjust amount of false positives.</span></span> |<span data-ttu-id="aa83e-127">'Orta'</span><span class="sxs-lookup"><span data-stu-id="aa83e-127">'medium'</span></span> |
| <span data-ttu-id="aa83e-128">frameSamplingValue</span><span class="sxs-lookup"><span data-stu-id="aa83e-128">frameSamplingValue</span></span> |<span data-ttu-id="aa83e-129">Pozitif tamsayı</span><span class="sxs-lookup"><span data-stu-id="aa83e-129">Positive integer</span></span> |<span data-ttu-id="aa83e-130">Algoritmayı sıklığında çalışan ayarlar.</span><span class="sxs-lookup"><span data-stu-id="aa83e-130">Sets the frequency at which algorithm runs.</span></span> <span data-ttu-id="aa83e-131">Her çerçeve eşittir 1, 2 her 2 çerçeve ve benzeri anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="aa83e-131">1 equals every frame, 2 means every 2nd frame, and so on.</span></span> |<span data-ttu-id="aa83e-132">1</span><span class="sxs-lookup"><span data-stu-id="aa83e-132">1</span></span> |
| <span data-ttu-id="aa83e-133">detectLightChange</span><span class="sxs-lookup"><span data-stu-id="aa83e-133">detectLightChange</span></span> |<span data-ttu-id="aa83e-134">Boolean: 'true', 'false'</span><span class="sxs-lookup"><span data-stu-id="aa83e-134">Boolean:'true', 'false'</span></span> |<span data-ttu-id="aa83e-135">Hafif değişiklikleri sonuçlarında bildirilen olup olmadığını belirler</span><span class="sxs-lookup"><span data-stu-id="aa83e-135">Sets whether light changes are reported in the results</span></span> |<span data-ttu-id="aa83e-136">'False'</span><span class="sxs-lookup"><span data-stu-id="aa83e-136">'False'</span></span> |
| <span data-ttu-id="aa83e-137">mergeTimeThreshold</span><span class="sxs-lookup"><span data-stu-id="aa83e-137">mergeTimeThreshold</span></span> |<span data-ttu-id="aa83e-138">Xs zamanı: Ss: dd:</span><span class="sxs-lookup"><span data-stu-id="aa83e-138">Xs-time: Hh:mm:ss</span></span><br/><span data-ttu-id="aa83e-139">Örnek: 00:00:03</span><span class="sxs-lookup"><span data-stu-id="aa83e-139">Example: 00:00:03</span></span> |<span data-ttu-id="aa83e-140">Burada 2 olayları birleştirilmiş ve olması 1 bildirilen hareket olaylar arasındaki zaman penceresi belirtir.</span><span class="sxs-lookup"><span data-stu-id="aa83e-140">Specifies the time window between motion events where 2 events will be combined and reported as 1.</span></span> |<span data-ttu-id="aa83e-141">00:00:00</span><span class="sxs-lookup"><span data-stu-id="aa83e-141">00:00:00</span></span> |
| <span data-ttu-id="aa83e-142">detectionZones</span><span class="sxs-lookup"><span data-stu-id="aa83e-142">detectionZones</span></span> |<span data-ttu-id="aa83e-143">Algılama bölgeleri dizisi:</span><span class="sxs-lookup"><span data-stu-id="aa83e-143">An array of detection zones:</span></span><br/><span data-ttu-id="aa83e-144">-3 veya daha fazla noktalar dizisi algılama bölgedir</span><span class="sxs-lookup"><span data-stu-id="aa83e-144">- Detection Zone is an array of 3 or more points</span></span><br/><span data-ttu-id="aa83e-145">-Noktasıdır x ve y koordinat 0'dan 1.</span><span class="sxs-lookup"><span data-stu-id="aa83e-145">- Point is a x and y coordinate from 0 to 1.</span></span> |<span data-ttu-id="aa83e-146">Kullanılacak Çokgen algılama bölgelerinin listesi açıklar.</span><span class="sxs-lookup"><span data-stu-id="aa83e-146">Describes the list of polygonal detection zones to be used.</span></span><br/><span data-ttu-id="aa83e-147">Sonuçları ilk olan 'ID' ile bir kimliği olarak bölge ile bildirilir: 0</span><span class="sxs-lookup"><span data-stu-id="aa83e-147">Results will be reported with the zones as an ID, with the first one being 'id':0</span></span> |<span data-ttu-id="aa83e-148">Tüm çerçeve kapsayan tek bir bölge.</span><span class="sxs-lookup"><span data-stu-id="aa83e-148">Single zone which covers the entire frame.</span></span> |

### <a name="json-example"></a><span data-ttu-id="aa83e-149">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="aa83e-149">JSON example</span></span>
    {
      "version": "1.0",
      "options": {
        "sensitivityLevel": "medium",
        "frameSamplingValue": 1,
        "detectLightChange": "False",
        "mergeTimeThreshold":
        "00:00:02",
        "detectionZones": [
          [
            {"x": 0, "y": 0},
            {"x": 0.5, "y": 0},
            {"x": 0, "y": 1}
           ],
          [
            {"x": 0.3, "y": 0.3},
            {"x": 0.55, "y": 0.3},
            {"x": 0.8, "y": 0.3},
            {"x": 0.8, "y": 0.55},
            {"x": 0.8, "y": 0.8},
            {"x": 0.55, "y": 0.8},
            {"x": 0.3, "y": 0.8},
            {"x": 0.3, "y": 0.55}
          ]
        ]
      }
    }


## <a name="motion-detector-output-files"></a><span data-ttu-id="aa83e-150">Hareket algılayıcısı çıktı dosyaları</span><span class="sxs-lookup"><span data-stu-id="aa83e-150">Motion Detector output files</span></span>
<span data-ttu-id="aa83e-151">Hareket algılama işi hareket uyarılar ve video içinde kendi kategorilerine tanımlayan çıkış varlığına bir JSON dosyası döndürür.</span><span class="sxs-lookup"><span data-stu-id="aa83e-151">A motion detection job will return a JSON file in the output asset which describes the motion alerts, and their categories, within the video.</span></span> <span data-ttu-id="aa83e-152">Dosyanın saatini ve süresini videoda algılanan hareket hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="aa83e-152">The file will contain information about the time and duration of motion detected in the video.</span></span>

<span data-ttu-id="aa83e-153">Bir sabit arka planda video (örn. bir izleme video) hareket nesneleri olduğunuzda hareket algılayıcısı API göstergeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="aa83e-153">The Motion Detector API provides indicators once there are objects in motion in a fixed background video (e.g. a surveillance video).</span></span> <span data-ttu-id="aa83e-154">Hareket algılayıcısı aydınlatma ve gölge değişiklikleri gibi yanlış alarmlar azaltmak için eğitildi.</span><span class="sxs-lookup"><span data-stu-id="aa83e-154">The Motion Detector is trained to reduce false alarms, such as lighting and shadow changes.</span></span> <span data-ttu-id="aa83e-155">Geçerli sınırlamalar algoritmalarının gece görme videoları, yarı saydam nesneleri ve küçük nesneleri içerir.</span><span class="sxs-lookup"><span data-stu-id="aa83e-155">Current limitations of the algorithms include night vision videos, semi-transparent objects, and small objects.</span></span>

### <span data-ttu-id="aa83e-156"><a id="output_elements"></a>Çıkış JSON dosyasının öğeleri</span><span class="sxs-lookup"><span data-stu-id="aa83e-156"><a id="output_elements"></a>Elements of the output JSON file</span></span>
> [!NOTE]
> <span data-ttu-id="aa83e-157">En son sürümdeki çıkış JSON biçimi değişti ve bazı müşteriler için önemli bir değişiklik gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="aa83e-157">In the latest release, the Output JSON format has changed and may represent a breaking change for some customers.</span></span>
> 
> 

<span data-ttu-id="aa83e-158">Aşağıdaki tabloda çıkış JSON dosyasının öğelerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="aa83e-158">The following table describes elements of the output JSON file.</span></span>

| <span data-ttu-id="aa83e-159">Öğesi</span><span class="sxs-lookup"><span data-stu-id="aa83e-159">Element</span></span> | <span data-ttu-id="aa83e-160">Açıklama</span><span class="sxs-lookup"><span data-stu-id="aa83e-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="aa83e-161">Sürüm</span><span class="sxs-lookup"><span data-stu-id="aa83e-161">Version</span></span> |<span data-ttu-id="aa83e-162">Video API sürümüne başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="aa83e-162">This refers to the version of the Video API.</span></span> <span data-ttu-id="aa83e-163">Geçerli sürüm 2'dir.</span><span class="sxs-lookup"><span data-stu-id="aa83e-163">The current version is 2.</span></span> |
| <span data-ttu-id="aa83e-164">Zaman Çizelgesi</span><span class="sxs-lookup"><span data-stu-id="aa83e-164">Timescale</span></span> |<span data-ttu-id="aa83e-165">Videonun saniyede "çizgilerine".</span><span class="sxs-lookup"><span data-stu-id="aa83e-165">"Ticks" per second of the video.</span></span> |
| <span data-ttu-id="aa83e-166">Uzaklık</span><span class="sxs-lookup"><span data-stu-id="aa83e-166">Offset</span></span> |<span data-ttu-id="aa83e-167">Veritabanındaki tarih damgası "çizgilerine" zaman uzaklığı.</span><span class="sxs-lookup"><span data-stu-id="aa83e-167">The time offset for timestamps in "ticks".</span></span> <span data-ttu-id="aa83e-168">Video API'leri 1.0 sürümünde, bu her zaman 0 olacaktır.</span><span class="sxs-lookup"><span data-stu-id="aa83e-168">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="aa83e-169">Gelecekte destekliyoruz senaryoları, bu değeri değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa83e-169">In future scenarios we support, this value may change.</span></span> |
| <span data-ttu-id="aa83e-170">Kare hızı</span><span class="sxs-lookup"><span data-stu-id="aa83e-170">Framerate</span></span> |<span data-ttu-id="aa83e-171">Videonun Saniyedeki çerçeve sayısı.</span><span class="sxs-lookup"><span data-stu-id="aa83e-171">Frames per second of the video.</span></span> |
| <span data-ttu-id="aa83e-172">Genişlik, Yükseklik</span><span class="sxs-lookup"><span data-stu-id="aa83e-172">Width, Height</span></span> |<span data-ttu-id="aa83e-173">Genişlik ve yükseklik piksel cinsinden videonun ifade eder.</span><span class="sxs-lookup"><span data-stu-id="aa83e-173">Refers to the width and height of the video in pixels.</span></span> |
| <span data-ttu-id="aa83e-174">Başlatma</span><span class="sxs-lookup"><span data-stu-id="aa83e-174">Start</span></span> |<span data-ttu-id="aa83e-175">Başlangıç zaman damgasına "çizgilerine".</span><span class="sxs-lookup"><span data-stu-id="aa83e-175">The start timestamp in "ticks".</span></span> |
| <span data-ttu-id="aa83e-176">Süre</span><span class="sxs-lookup"><span data-stu-id="aa83e-176">Duration</span></span> |<span data-ttu-id="aa83e-177">Olay, "çizgilerine" uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="aa83e-177">The length of the event, in "ticks".</span></span> |
| <span data-ttu-id="aa83e-178">aralığı</span><span class="sxs-lookup"><span data-stu-id="aa83e-178">Interval</span></span> |<span data-ttu-id="aa83e-179">Her giriş olayda "çizgilerine" aralığı.</span><span class="sxs-lookup"><span data-stu-id="aa83e-179">The interval of each entry in the event, in "ticks".</span></span> |
| <span data-ttu-id="aa83e-180">Olaylar</span><span class="sxs-lookup"><span data-stu-id="aa83e-180">Events</span></span> |<span data-ttu-id="aa83e-181">Her olay parça bu süre içinde algılanan hareket içerir.</span><span class="sxs-lookup"><span data-stu-id="aa83e-181">Each event fragment contains the motion detected within that time duration.</span></span> |
| <span data-ttu-id="aa83e-182">Tür</span><span class="sxs-lookup"><span data-stu-id="aa83e-182">Type</span></span> |<span data-ttu-id="aa83e-183">Geçerli sürümde, bu her zaman genel hareket ' 2' dir.</span><span class="sxs-lookup"><span data-stu-id="aa83e-183">In the current version, this is always ‘2’ for generic motion.</span></span> <span data-ttu-id="aa83e-184">Bu etiket verir Video kategorilere ayırmak için API esnekliği gelecekteki sürümleri hareket.</span><span class="sxs-lookup"><span data-stu-id="aa83e-184">This label gives Video APIs the flexibility to categorize motion in future versions.</span></span> |
| <span data-ttu-id="aa83e-185">RegionID</span><span class="sxs-lookup"><span data-stu-id="aa83e-185">RegionID</span></span> |<span data-ttu-id="aa83e-186">Yukarıda açıklandığı şekilde, bu her zaman bu sürümde 0 olacaktır.</span><span class="sxs-lookup"><span data-stu-id="aa83e-186">As explained above, this will always be 0 in this version.</span></span> <span data-ttu-id="aa83e-187">Bu etiket Video API gelecekteki sürümlerinde çeşitli bölgelerdeki hareket bulmak için esneklik sunar.</span><span class="sxs-lookup"><span data-stu-id="aa83e-187">This label gives Video API the flexibility to find motion in various regions in future versions.</span></span> |
| <span data-ttu-id="aa83e-188">Bölgeler</span><span class="sxs-lookup"><span data-stu-id="aa83e-188">Regions</span></span> |<span data-ttu-id="aa83e-189">Hareket hakkında burada verdiğiniz videonuzu alanına başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="aa83e-189">Refers to the area in your video where you care about motion.</span></span> <br/><br/><span data-ttu-id="aa83e-190">-"id" temsil Bölge alanı – bu sürümde yalnızca bir olduğundan, kimliği 0.</span><span class="sxs-lookup"><span data-stu-id="aa83e-190">-"id" represents the region area – in this version there is only one, ID 0.</span></span> <br/><span data-ttu-id="aa83e-191">-"tür" önem verdiğiniz hareket bölge şekli temsil eder.</span><span class="sxs-lookup"><span data-stu-id="aa83e-191">-"type" represents the shape of the region you care about for motion.</span></span> <span data-ttu-id="aa83e-192">Şu anda, "dikdörtgen" ve "Çokgen" desteklenir.</span><span class="sxs-lookup"><span data-stu-id="aa83e-192">Currently, "rectangle" and "polygon" are supported.</span></span><br/> <span data-ttu-id="aa83e-193">"Dikdörtgen" belirtilmişse, bölge boyutu X, vardır. Y, genişlik ve yükseklik.</span><span class="sxs-lookup"><span data-stu-id="aa83e-193">If you specified "rectangle", the region has dimensions in X, Y, Width, and Height.</span></span> <span data-ttu-id="aa83e-194">X ve Y koordinatları 0.0 ile 1.0 normalleştirilmiş ölçeğini bölgede üst sol XY koordinatları temsil eder.</span><span class="sxs-lookup"><span data-stu-id="aa83e-194">The X and Y coordinates represent the upper left hand XY coordinates of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="aa83e-195">Genişlik ve yükseklik 0.0 ile 1.0 normalleştirilmiş ölçeğini bölgede boyutunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="aa83e-195">The width and height represent the size of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="aa83e-196">Geçerli sürümde X, Y, genişlik ve yükseklik her zaman giderilen 0, 0 ve 1, 1.</span><span class="sxs-lookup"><span data-stu-id="aa83e-196">In the current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span></span> <br/><span data-ttu-id="aa83e-197">"Çokgen" belirtilmişse, bölge boyutları noktalar vardır.</span><span class="sxs-lookup"><span data-stu-id="aa83e-197">If you specified "polygon", the region has dimensions in points.</span></span> <br/> |
| <span data-ttu-id="aa83e-198">Parçaları</span><span class="sxs-lookup"><span data-stu-id="aa83e-198">Fragments</span></span> |<span data-ttu-id="aa83e-199">Meta verileri ayarlama parçaları olarak adlandırılan farklı kesimler halinde öbekli.</span><span class="sxs-lookup"><span data-stu-id="aa83e-199">The metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="aa83e-200">Her parça başlangıç, süre, aralığı sayısı ve olay içerir.</span><span class="sxs-lookup"><span data-stu-id="aa83e-200">Each fragment contains a start, duration, interval number, and event(s).</span></span> <span data-ttu-id="aa83e-201">Hiçbir olay ile bir parça yok hareket bu başlangıç saatini ve süresini sırasında algılandı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="aa83e-201">A fragment with no events means that no motion was detected during that start time and duration.</span></span> |
| <span data-ttu-id="aa83e-202">Köşeli ayraçlar]</span><span class="sxs-lookup"><span data-stu-id="aa83e-202">Brackets []</span></span> |<span data-ttu-id="aa83e-203">Her köşeli ayraç olay bir aralığa temsil eder.</span><span class="sxs-lookup"><span data-stu-id="aa83e-203">Each bracket represents one interval in the event.</span></span> <span data-ttu-id="aa83e-204">Boş köşeli ayraçlar hiçbir hareket anlamına bu aralık için algılandı.</span><span class="sxs-lookup"><span data-stu-id="aa83e-204">Empty brackets for that interval means that no motion was detected.</span></span> |
| <span data-ttu-id="aa83e-205">Konumları</span><span class="sxs-lookup"><span data-stu-id="aa83e-205">locations</span></span> |<span data-ttu-id="aa83e-206">Bu yeni girişi olayları altında hareket gerçekleştiği konum listeler.</span><span class="sxs-lookup"><span data-stu-id="aa83e-206">This new entry under events lists the location where the motion occurred.</span></span> <span data-ttu-id="aa83e-207">Bu algılama bölgeleri daha fazla özeldir.</span><span class="sxs-lookup"><span data-stu-id="aa83e-207">This is more specific than the detection zones.</span></span> |

<span data-ttu-id="aa83e-208">JSON çıkış örnek verilmiştir</span><span class="sxs-lookup"><span data-stu-id="aa83e-208">The following is a JSON output example</span></span>

    {
      "version": 2,
      "timescale": 23976,
      "offset": 0,
      "framerate": 24,
      "width": 1280,
      "height": 720,
      "regions": [
        {
          "id": 0,
          "type": "polygon",
          "points": [{'x': 0, 'y': 0},
            {'x': 0.5, 'y': 0},
            {'x': 0, 'y': 1}]
        }
      ],
      "fragments": [
        {
          "start": 0,
          "duration": 226765
        },
        {
          "start": 226765,
          "duration": 47952,
          "interval": 999,
          "events": [
            [
              {
                "type": 2,
                "typeName": "motion",
                "locations": [
                  {
                    "x": 0.004184,
                    "y": 0.007463,
                    "width": 0.991667,
                    "height": 0.985185
                  }
                ],
                "regionId": 0
              }
            ],

    …
## <a name="limitations"></a><span data-ttu-id="aa83e-209">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="aa83e-209">Limitations</span></span>
* <span data-ttu-id="aa83e-210">Desteklenen giriş video biçimleri MP4, MOV ve WMV içerir.</span><span class="sxs-lookup"><span data-stu-id="aa83e-210">The supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="aa83e-211">Hareket algılama sabit arka plan videolar için optimize edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="aa83e-211">Motion Detection is optimized for stationary background videos.</span></span> <span data-ttu-id="aa83e-212">Algoritma aydınlatma değişiklikleri ve gölgeleri gibi yanlış alarmlar azaltma odaklanır.</span><span class="sxs-lookup"><span data-stu-id="aa83e-212">The algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span></span>
* <span data-ttu-id="aa83e-213">Bazı hareket nedeniyle teknik zorluklar algılanamayabilir; Örneğin gece görme videoları, yarı saydam nesneler ve küçük nesneleri.</span><span class="sxs-lookup"><span data-stu-id="aa83e-213">Some motion may not be detected due to technical challenges; e.g. night vision videos, semi-transparent objects, and small objects.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="aa83e-214">.NET örnek kod</span><span class="sxs-lookup"><span data-stu-id="aa83e-214">.NET sample code</span></span>

<span data-ttu-id="aa83e-215">Aşağıdaki program gösterir nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="aa83e-215">The following program shows how to:</span></span>

1. <span data-ttu-id="aa83e-216">Bir varlık oluşturun ve varlığa bir medya dosyasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="aa83e-216">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="aa83e-217">Aşağıdaki json hazır içeren bir yapılandırma dosyasına dayalı bir video hareket algılama görev ile bir iş oluşturun.</span><span class="sxs-lookup"><span data-stu-id="aa83e-217">Create a job with a video motion detection task based on a configuration file that contains the following json preset.</span></span> 
   
        {
          "Version": "1.0",
          "Options": {
            "SensitivityLevel": "medium",
            "FrameSamplingValue": 1,
            "DetectLightChange": "False",
            "MergeTimeThreshold":
            "00:00:02",
            "DetectionZones": [
              [
                {"x": 0, "y": 0},
                {"x": 0.5, "y": 0},
                {"x": 0, "y": 1}
               ],
              [
                {"x": 0.3, "y": 0.3},
                {"x": 0.55, "y": 0.3},
                {"x": 0.8, "y": 0.3},
                {"x": 0.8, "y": 0.55},
                {"x": 0.8, "y": 0.8},
                {"x": 0.55, "y": 0.8},
                {"x": 0.3, "y": 0.8},
                {"x": 0.3, "y": 0.55}
              ]
            ]
          }
        }
3. <span data-ttu-id="aa83e-218">Çıkış JSON dosyalarını indirin.</span><span class="sxs-lookup"><span data-stu-id="aa83e-218">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="aa83e-219">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="aa83e-219">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="aa83e-220">Geliştirme ortamınızı kurun ve app.config dosyanızı [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md) bölümünde açıklandığı gibi bağlantı bilgileriyle doldurun.</span><span class="sxs-lookup"><span data-stu-id="aa83e-220">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="aa83e-221">Örnek</span><span class="sxs-lookup"><span data-stu-id="aa83e-221">Example</span></span>


    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoMotionDetection
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

                // Run the VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference to Azure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="aa83e-222">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="aa83e-222">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="aa83e-223">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="aa83e-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="aa83e-224">İlgili bağlantılar</span><span class="sxs-lookup"><span data-stu-id="aa83e-224">Related links</span></span>
[<span data-ttu-id="aa83e-225">Azure Media Services hareket algılayıcısı blogu</span><span class="sxs-lookup"><span data-stu-id="aa83e-225">Azure Media Services Motion Detector blog</span></span>](https://azure.microsoft.com/blog/motion-detector-update/)

[<span data-ttu-id="aa83e-226">Azure Media Services Analytics a genel bakış</span><span class="sxs-lookup"><span data-stu-id="aa83e-226">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="aa83e-227">Azure medya analizi gösterileri</span><span class="sxs-lookup"><span data-stu-id="aa83e-227">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

