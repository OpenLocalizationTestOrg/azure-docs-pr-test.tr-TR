---
title: Azure medya Analizi ile aaaDetect hareketlerin | Microsoft Docs
description: "Merhaba, tooefficiently aksi uzun ve olaysız video içinde ilgi bölümleri tanımlamak Azure medya hareket algılayıcısı medya işlemci (MP) etkinleştirir."
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
ms.openlocfilehash: cb431375c92222053ed2239dd4e45767524dab68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a><span data-ttu-id="b2da3-103">Azure medya Analizi ile hareketlerin Algıla</span><span class="sxs-lookup"><span data-stu-id="b2da3-103">Detect Motions with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="b2da3-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b2da3-104">Overview</span></span>
<span data-ttu-id="b2da3-105">Merhaba **Azure medya hareket algılayıcısı** , tooefficiently aksi uzun ve olaysız video içinde ilgi bölümleri tanımlamak medya işlemci (MP) etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="b2da3-105">hello **Azure Media Motion Detector** media processor (MP) enables you tooefficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="b2da3-106">Hareket algılama hareket oluştuğu statik kamera görüntülerinin tooidentify bölümlerini hello video üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b2da3-106">Motion detection can be used on static camera footage tooidentify sections of hello video where motion occurs.</span></span> <span data-ttu-id="b2da3-107">Zaman damgaları ve bölge hello olayın gerçekleştiği sınırlayıcı hello meta verileri içeren bir JSON dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b2da3-107">It generates a JSON file containing a metadata with timestamps and hello bounding region where hello event occurred.</span></span>

<span data-ttu-id="b2da3-108">Doğru güvenlik video akışları hedeflenen, bu mümkün toocategorize hareket ilgili olayları ve hatalı pozitif sonuç gölgeleri ve aydınlatma değişiklikleri gibi teknolojisidir.</span><span class="sxs-lookup"><span data-stu-id="b2da3-108">Targeted towards security video feeds, this technology is able toocategorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="b2da3-109">Bu işlem, sonsuz ilgisiz olaylarıyla aşırı uzun gözetleme videolar gelen ilgi mümkün tooextract dakika devam ederken adresinize olmadan kamera akışları toogenerate güvenlik uyarıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2da3-109">This allows you toogenerate security alerts from camera feeds without being spammed with endless irrelevant events, while being able tooextract moments of interest from extremely long surveillance videos.</span></span>

<span data-ttu-id="b2da3-110">Merhaba **Azure medya hareket algılayıcısı** MP şu anda önizlemede.</span><span class="sxs-lookup"><span data-stu-id="b2da3-110">hello **Azure Media Motion Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="b2da3-111">Bu konu hakkında ayrıntılar verir **Azure medya hareket algılayıcısı** ve gösterir nasıl toouse .NET için Media Services SDK'sı ile</span><span class="sxs-lookup"><span data-stu-id="b2da3-111">This topic gives details about  **Azure Media Motion Detector** and shows how toouse it with Media Services SDK for .NET</span></span>

## <a name="motion-detector-input-files"></a><span data-ttu-id="b2da3-112">Hareket algılayıcısı giriş dosyaları</span><span class="sxs-lookup"><span data-stu-id="b2da3-112">Motion Detector input files</span></span>
<span data-ttu-id="b2da3-113">Video dosyaları.</span><span class="sxs-lookup"><span data-stu-id="b2da3-113">Video files.</span></span> <span data-ttu-id="b2da3-114">Şu anda biçimleri aşağıdaki hello desteklenir: MP4, MOV ve WMV.</span><span class="sxs-lookup"><span data-stu-id="b2da3-114">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="b2da3-115">Görev yapılandırması (hazır)</span><span class="sxs-lookup"><span data-stu-id="b2da3-115">Task configuration (preset)</span></span>
<span data-ttu-id="b2da3-116">Bir görev oluştururken **Azure medya hareket algılayıcısı**, bir yapılandırma hazır belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2da3-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span></span> 

### <a name="parameters"></a><span data-ttu-id="b2da3-117">Parametreler</span><span class="sxs-lookup"><span data-stu-id="b2da3-117">Parameters</span></span>
<span data-ttu-id="b2da3-118">Şu parametreler hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b2da3-118">You can use hello following parameters:</span></span>

| <span data-ttu-id="b2da3-119">Ad</span><span class="sxs-lookup"><span data-stu-id="b2da3-119">Name</span></span> | <span data-ttu-id="b2da3-120">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="b2da3-120">Options</span></span> | <span data-ttu-id="b2da3-121">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b2da3-121">Description</span></span> | <span data-ttu-id="b2da3-122">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="b2da3-122">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b2da3-123">sensitivityLevel</span><span class="sxs-lookup"><span data-stu-id="b2da3-123">sensitivityLevel</span></span> |<span data-ttu-id="b2da3-124">Dize: 'düşük', 'Orta', 'yüksek'</span><span class="sxs-lookup"><span data-stu-id="b2da3-124">String:'low', 'medium', 'high'</span></span> |<span data-ttu-id="b2da3-125">Hangi hareketlerin adresindeki bildirilir Hello hassasiyet düzeyini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b2da3-125">Sets hello sensitivity level at which motions is reported.</span></span> <span data-ttu-id="b2da3-126">Bu hatalı pozitif sonuç tooadjust miktarını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b2da3-126">Adjust this tooadjust amount of false positives.</span></span> |<span data-ttu-id="b2da3-127">'Orta'</span><span class="sxs-lookup"><span data-stu-id="b2da3-127">'medium'</span></span> |
| <span data-ttu-id="b2da3-128">frameSamplingValue</span><span class="sxs-lookup"><span data-stu-id="b2da3-128">frameSamplingValue</span></span> |<span data-ttu-id="b2da3-129">Pozitif tamsayı</span><span class="sxs-lookup"><span data-stu-id="b2da3-129">Positive integer</span></span> |<span data-ttu-id="b2da3-130">Merhaba sıklığı algoritması çalıştığı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b2da3-130">Sets hello frequency at which algorithm runs.</span></span> <span data-ttu-id="b2da3-131">Her çerçeve eşittir 1, 2 her 2 çerçeve ve benzeri anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b2da3-131">1 equals every frame, 2 means every 2nd frame, and so on.</span></span> |<span data-ttu-id="b2da3-132">1</span><span class="sxs-lookup"><span data-stu-id="b2da3-132">1</span></span> |
| <span data-ttu-id="b2da3-133">detectLightChange</span><span class="sxs-lookup"><span data-stu-id="b2da3-133">detectLightChange</span></span> |<span data-ttu-id="b2da3-134">Boolean: 'true', 'false'</span><span class="sxs-lookup"><span data-stu-id="b2da3-134">Boolean:'true', 'false'</span></span> |<span data-ttu-id="b2da3-135">Hafif değişiklikleri hello sonuçlarında bildirilen olup olmadığını belirler</span><span class="sxs-lookup"><span data-stu-id="b2da3-135">Sets whether light changes are reported in hello results</span></span> |<span data-ttu-id="b2da3-136">'False'</span><span class="sxs-lookup"><span data-stu-id="b2da3-136">'False'</span></span> |
| <span data-ttu-id="b2da3-137">mergeTimeThreshold</span><span class="sxs-lookup"><span data-stu-id="b2da3-137">mergeTimeThreshold</span></span> |<span data-ttu-id="b2da3-138">Xs zamanı: Ss: dd:</span><span class="sxs-lookup"><span data-stu-id="b2da3-138">Xs-time: Hh:mm:ss</span></span><br/><span data-ttu-id="b2da3-139">Örnek: 00:00:03</span><span class="sxs-lookup"><span data-stu-id="b2da3-139">Example: 00:00:03</span></span> |<span data-ttu-id="b2da3-140">Burada 2 olayları birleştirilmiş ve olması 1 bildirilen hareket olaylar arasındaki Hello zaman penceresi belirtir.</span><span class="sxs-lookup"><span data-stu-id="b2da3-140">Specifies hello time window between motion events where 2 events will be combined and reported as 1.</span></span> |<span data-ttu-id="b2da3-141">00:00:00</span><span class="sxs-lookup"><span data-stu-id="b2da3-141">00:00:00</span></span> |
| <span data-ttu-id="b2da3-142">detectionZones</span><span class="sxs-lookup"><span data-stu-id="b2da3-142">detectionZones</span></span> |<span data-ttu-id="b2da3-143">Algılama bölgeleri dizisi:</span><span class="sxs-lookup"><span data-stu-id="b2da3-143">An array of detection zones:</span></span><br/><span data-ttu-id="b2da3-144">-3 veya daha fazla noktalar dizisi algılama bölgedir</span><span class="sxs-lookup"><span data-stu-id="b2da3-144">- Detection Zone is an array of 3 or more points</span></span><br/><span data-ttu-id="b2da3-145">-Noktasıdır x ve y 0 too1 gelen koordinat.</span><span class="sxs-lookup"><span data-stu-id="b2da3-145">- Point is a x and y coordinate from 0 too1.</span></span> |<span data-ttu-id="b2da3-146">Çokgen algılama bölgeleri toobe kullanılan Hello listesi açıklar.</span><span class="sxs-lookup"><span data-stu-id="b2da3-146">Describes hello list of polygonal detection zones toobe used.</span></span><br/><span data-ttu-id="b2da3-147">Sonuçları hello ilk olma 'ID' ile bir kimliği olarak hello bölge ile bildirilir: 0</span><span class="sxs-lookup"><span data-stu-id="b2da3-147">Results will be reported with hello zones as an ID, with hello first one being 'id':0</span></span> |<span data-ttu-id="b2da3-148">Merhaba tüm çerçeve kapsayan tek bir bölge.</span><span class="sxs-lookup"><span data-stu-id="b2da3-148">Single zone which covers hello entire frame.</span></span> |

### <a name="json-example"></a><span data-ttu-id="b2da3-149">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="b2da3-149">JSON example</span></span>
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


## <a name="motion-detector-output-files"></a><span data-ttu-id="b2da3-150">Hareket algılayıcısı çıktı dosyaları</span><span class="sxs-lookup"><span data-stu-id="b2da3-150">Motion Detector output files</span></span>
<span data-ttu-id="b2da3-151">Hareket algılama işi hello hareket uyarılar ve bunların kategorilerde hello video tanımlayan hello çıkış varlık bir JSON dosyası döndürür.</span><span class="sxs-lookup"><span data-stu-id="b2da3-151">A motion detection job will return a JSON file in hello output asset which describes hello motion alerts, and their categories, within hello video.</span></span> <span data-ttu-id="b2da3-152">Merhaba dosyası başlangıç saatini ve süresini hello video algılanan hareket hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="b2da3-152">hello file will contain information about hello time and duration of motion detected in hello video.</span></span>

<span data-ttu-id="b2da3-153">bir sabit arka planda video (örn. bir izleme video) hareket nesneleri olduğunuzda hello hareket algılayıcısı API göstergeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2da3-153">hello Motion Detector API provides indicators once there are objects in motion in a fixed background video (e.g. a surveillance video).</span></span> <span data-ttu-id="b2da3-154">Merhaba hareket algılayıcısı aydınlatma ve gölge değişiklikleri gibi eğitilen tooreduce yanlış alarmlar ' dir.</span><span class="sxs-lookup"><span data-stu-id="b2da3-154">hello Motion Detector is trained tooreduce false alarms, such as lighting and shadow changes.</span></span> <span data-ttu-id="b2da3-155">Geçerli sınırlamalar hello algoritmalarının gece görme videoları, yarı saydam nesneleri ve küçük nesneleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b2da3-155">Current limitations of hello algorithms include night vision videos, semi-transparent objects, and small objects.</span></span>

### <span data-ttu-id="b2da3-156"><a id="output_elements"></a>Merhaba çıkış JSON dosyasının öğeleri</span><span class="sxs-lookup"><span data-stu-id="b2da3-156"><a id="output_elements"></a>Elements of hello output JSON file</span></span>
> [!NOTE]
> <span data-ttu-id="b2da3-157">Merhaba en son sürümdeki hello çıkış JSON biçimi değişti ve bazı müşteriler için önemli bir değişiklik gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="b2da3-157">In hello latest release, hello Output JSON format has changed and may represent a breaking change for some customers.</span></span>
> 
> 

<span data-ttu-id="b2da3-158">Merhaba aşağıdaki tabloda hello çıkış JSON dosyasının öğelerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="b2da3-158">hello following table describes elements of hello output JSON file.</span></span>

| <span data-ttu-id="b2da3-159">Öğesi</span><span class="sxs-lookup"><span data-stu-id="b2da3-159">Element</span></span> | <span data-ttu-id="b2da3-160">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b2da3-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b2da3-161">Sürüm</span><span class="sxs-lookup"><span data-stu-id="b2da3-161">Version</span></span> |<span data-ttu-id="b2da3-162">Bu toohello hello Video API sürümü ifade eder.</span><span class="sxs-lookup"><span data-stu-id="b2da3-162">This refers toohello version of hello Video API.</span></span> <span data-ttu-id="b2da3-163">Merhaba geçerli sürüm 2'dir.</span><span class="sxs-lookup"><span data-stu-id="b2da3-163">hello current version is 2.</span></span> |
| <span data-ttu-id="b2da3-164">Zaman Çizelgesi</span><span class="sxs-lookup"><span data-stu-id="b2da3-164">Timescale</span></span> |<span data-ttu-id="b2da3-165">"Hello videonun saniyede"çizgilerine.</span><span class="sxs-lookup"><span data-stu-id="b2da3-165">"Ticks" per second of hello video.</span></span> |
| <span data-ttu-id="b2da3-166">Uzaklık</span><span class="sxs-lookup"><span data-stu-id="b2da3-166">Offset</span></span> |<span data-ttu-id="b2da3-167">"çizgilerine" veritabanındaki tarih damgası Hello zaman uzaklığı.</span><span class="sxs-lookup"><span data-stu-id="b2da3-167">hello time offset for timestamps in "ticks".</span></span> <span data-ttu-id="b2da3-168">Video API'leri 1.0 sürümünde, bu her zaman 0 olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b2da3-168">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="b2da3-169">Gelecekte destekliyoruz senaryoları, bu değeri değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2da3-169">In future scenarios we support, this value may change.</span></span> |
| <span data-ttu-id="b2da3-170">Kare hızı</span><span class="sxs-lookup"><span data-stu-id="b2da3-170">Framerate</span></span> |<span data-ttu-id="b2da3-171">Saniyedeki kare sayısı hello video.</span><span class="sxs-lookup"><span data-stu-id="b2da3-171">Frames per second of hello video.</span></span> |
| <span data-ttu-id="b2da3-172">Genişlik, Yükseklik</span><span class="sxs-lookup"><span data-stu-id="b2da3-172">Width, Height</span></span> |<span data-ttu-id="b2da3-173">Toohello genişliğini ve yüksekliğini piksel cinsinden görüntü hello başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="b2da3-173">Refers toohello width and height of hello video in pixels.</span></span> |
| <span data-ttu-id="b2da3-174">Başlatma</span><span class="sxs-lookup"><span data-stu-id="b2da3-174">Start</span></span> |<span data-ttu-id="b2da3-175">Merhaba "çizgilerine" timestamp başlatın.</span><span class="sxs-lookup"><span data-stu-id="b2da3-175">hello start timestamp in "ticks".</span></span> |
| <span data-ttu-id="b2da3-176">Süre</span><span class="sxs-lookup"><span data-stu-id="b2da3-176">Duration</span></span> |<span data-ttu-id="b2da3-177">Merhaba olayda "çizgilerine" Merhaba uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="b2da3-177">hello length of hello event, in "ticks".</span></span> |
| <span data-ttu-id="b2da3-178">aralığı</span><span class="sxs-lookup"><span data-stu-id="b2da3-178">Interval</span></span> |<span data-ttu-id="b2da3-179">Her giriş hello olayda "çizgilerine" Merhaba aralığı.</span><span class="sxs-lookup"><span data-stu-id="b2da3-179">hello interval of each entry in hello event, in "ticks".</span></span> |
| <span data-ttu-id="b2da3-180">Olaylar</span><span class="sxs-lookup"><span data-stu-id="b2da3-180">Events</span></span> |<span data-ttu-id="b2da3-181">Her olay parça bu süre içinde algılanan hello hareket içerir.</span><span class="sxs-lookup"><span data-stu-id="b2da3-181">Each event fragment contains hello motion detected within that time duration.</span></span> |
| <span data-ttu-id="b2da3-182">Tür</span><span class="sxs-lookup"><span data-stu-id="b2da3-182">Type</span></span> |<span data-ttu-id="b2da3-183">Merhaba geçerli sürümde, bu her zaman genel hareket ' 2' dir.</span><span class="sxs-lookup"><span data-stu-id="b2da3-183">In hello current version, this is always ‘2’ for generic motion.</span></span> <span data-ttu-id="b2da3-184">Bu etiket Video API'leri hello esneklik toocategorize hareket gelecekteki sürümlerde de sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2da3-184">This label gives Video APIs hello flexibility toocategorize motion in future versions.</span></span> |
| <span data-ttu-id="b2da3-185">RegionID</span><span class="sxs-lookup"><span data-stu-id="b2da3-185">RegionID</span></span> |<span data-ttu-id="b2da3-186">Yukarıda açıklandığı şekilde, bu her zaman bu sürümde 0 olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b2da3-186">As explained above, this will always be 0 in this version.</span></span> <span data-ttu-id="b2da3-187">Bu etiket Video API hello esneklik toofind hareket gelecekteki sürümlerinde çeşitli bölgelerdeki sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2da3-187">This label gives Video API hello flexibility toofind motion in various regions in future versions.</span></span> |
| <span data-ttu-id="b2da3-188">Bölgeler</span><span class="sxs-lookup"><span data-stu-id="b2da3-188">Regions</span></span> |<span data-ttu-id="b2da3-189">Toohello alanında hareket hakkında burada verdiğiniz videonuzu başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="b2da3-189">Refers toohello area in your video where you care about motion.</span></span> <br/><br/><span data-ttu-id="b2da3-190">-"id" Merhaba Bölge alanı temsil eder – Bu sürümde yalnızca bir olduğundan, kimliği 0.</span><span class="sxs-lookup"><span data-stu-id="b2da3-190">-"id" represents hello region area – in this version there is only one, ID 0.</span></span> <br/><span data-ttu-id="b2da3-191">-"tür" Merhaba bölge önem verdiğiniz hareket hello şeklini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="b2da3-191">-"type" represents hello shape of hello region you care about for motion.</span></span> <span data-ttu-id="b2da3-192">Şu anda, "dikdörtgen" ve "Çokgen" desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b2da3-192">Currently, "rectangle" and "polygon" are supported.</span></span><br/> <span data-ttu-id="b2da3-193">"Dikdörtgen" belirtilmişse hello bölge boyutu X, vardır. Y, genişlik ve yükseklik.</span><span class="sxs-lookup"><span data-stu-id="b2da3-193">If you specified "rectangle", hello region has dimensions in X, Y, Width, and Height.</span></span> <span data-ttu-id="b2da3-194">Merhaba X ve Y koordinatları hello üst sol XY koordinatları 0.0 too1.0 normalleştirilmiş ölçeğini hello bölgede temsil eder.</span><span class="sxs-lookup"><span data-stu-id="b2da3-194">hello X and Y coordinates represent hello upper left hand XY coordinates of hello region in a normalized scale of 0.0 too1.0.</span></span> <span data-ttu-id="b2da3-195">Merhaba genişlik ve yükseklik 0.0 too1.0 normalleştirilmiş ölçeğini hello bölgede hello boyutunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="b2da3-195">hello width and height represent hello size of hello region in a normalized scale of 0.0 too1.0.</span></span> <span data-ttu-id="b2da3-196">Merhaba geçerli sürümde, X, Y, genişlik ve yükseklik her zaman giderilen 0, 0 ve 1, 1.</span><span class="sxs-lookup"><span data-stu-id="b2da3-196">In hello current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span></span> <br/><span data-ttu-id="b2da3-197">"Çokgen" belirtilmişse, hello bölge boyutları noktalar vardır.</span><span class="sxs-lookup"><span data-stu-id="b2da3-197">If you specified "polygon", hello region has dimensions in points.</span></span> <br/> |
| <span data-ttu-id="b2da3-198">Parçaları</span><span class="sxs-lookup"><span data-stu-id="b2da3-198">Fragments</span></span> |<span data-ttu-id="b2da3-199">Merhaba meta verilerini yukarı parçaları olarak adlandırılan farklı kesimler halinde öbekli.</span><span class="sxs-lookup"><span data-stu-id="b2da3-199">hello metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="b2da3-200">Her parça başlangıç, süre, aralığı sayısı ve olay içerir.</span><span class="sxs-lookup"><span data-stu-id="b2da3-200">Each fragment contains a start, duration, interval number, and event(s).</span></span> <span data-ttu-id="b2da3-201">Hiçbir olay ile bir parça yok hareket bu başlangıç saatini ve süresini sırasında algılandı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b2da3-201">A fragment with no events means that no motion was detected during that start time and duration.</span></span> |
| <span data-ttu-id="b2da3-202">Köşeli ayraçlar]</span><span class="sxs-lookup"><span data-stu-id="b2da3-202">Brackets []</span></span> |<span data-ttu-id="b2da3-203">Her köşeli ayraç hello olay bir aralığa temsil eder.</span><span class="sxs-lookup"><span data-stu-id="b2da3-203">Each bracket represents one interval in hello event.</span></span> <span data-ttu-id="b2da3-204">Boş köşeli ayraçlar hiçbir hareket anlamına bu aralık için algılandı.</span><span class="sxs-lookup"><span data-stu-id="b2da3-204">Empty brackets for that interval means that no motion was detected.</span></span> |
| <span data-ttu-id="b2da3-205">Konumları</span><span class="sxs-lookup"><span data-stu-id="b2da3-205">locations</span></span> |<span data-ttu-id="b2da3-206">Bu yeni girişi olayları altında hello hareket oluştuğu hello konumunu listeler.</span><span class="sxs-lookup"><span data-stu-id="b2da3-206">This new entry under events lists hello location where hello motion occurred.</span></span> <span data-ttu-id="b2da3-207">Merhaba algılama bölgeleri daha fazla belirli budur.</span><span class="sxs-lookup"><span data-stu-id="b2da3-207">This is more specific than hello detection zones.</span></span> |

<span data-ttu-id="b2da3-208">bir JSON çıktı örneği Hello aşağıda verilmiştir</span><span class="sxs-lookup"><span data-stu-id="b2da3-208">hello following is a JSON output example</span></span>

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
## <a name="limitations"></a><span data-ttu-id="b2da3-209">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="b2da3-209">Limitations</span></span>
* <span data-ttu-id="b2da3-210">desteklenen hello giriş video biçimleri MP4, MOV ve WMV içerir.</span><span class="sxs-lookup"><span data-stu-id="b2da3-210">hello supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="b2da3-211">Hareket algılama sabit arka plan videolar için optimize edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b2da3-211">Motion Detection is optimized for stationary background videos.</span></span> <span data-ttu-id="b2da3-212">Merhaba algoritması aydınlatma değişiklikleri ve gölgeleri gibi yanlış alarmlar azaltma odaklanır.</span><span class="sxs-lookup"><span data-stu-id="b2da3-212">hello algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span></span>
* <span data-ttu-id="b2da3-213">Bazı hareket tootechnical zorluklar algılanamayabilir; Örneğin gece görme videoları, yarı saydam nesneler ve küçük nesneleri.</span><span class="sxs-lookup"><span data-stu-id="b2da3-213">Some motion may not be detected due tootechnical challenges; e.g. night vision videos, semi-transparent objects, and small objects.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="b2da3-214">.NET örnek kod</span><span class="sxs-lookup"><span data-stu-id="b2da3-214">.NET sample code</span></span>

<span data-ttu-id="b2da3-215">Merhaba aşağıdaki program gösterir nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="b2da3-215">hello following program shows how to:</span></span>

1. <span data-ttu-id="b2da3-216">Bir varlık oluşturun ve hello varlığa bir medya dosyasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b2da3-216">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="b2da3-217">Json hazır aşağıdaki hello içeren bir yapılandırma dosyasına dayalı bir video hareket algılama görev ile bir iş oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b2da3-217">Create a job with a video motion detection task based on a configuration file that contains hello following json preset.</span></span> 
   
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
3. <span data-ttu-id="b2da3-218">Merhaba çıkış JSON dosyalarını indirin.</span><span class="sxs-lookup"><span data-stu-id="b2da3-218">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="b2da3-219">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b2da3-219">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="b2da3-220">Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="b2da3-220">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="b2da3-221">Örnek</span><span class="sxs-lookup"><span data-stu-id="b2da3-221">Example</span></span>


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

                // Run hello VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference tooAzure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="b2da3-222">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="b2da3-222">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b2da3-223">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="b2da3-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="b2da3-224">İlgili bağlantılar</span><span class="sxs-lookup"><span data-stu-id="b2da3-224">Related links</span></span>
[<span data-ttu-id="b2da3-225">Azure Media Services hareket algılayıcısı blogu</span><span class="sxs-lookup"><span data-stu-id="b2da3-225">Azure Media Services Motion Detector blog</span></span>](https://azure.microsoft.com/blog/motion-detector-update/)

[<span data-ttu-id="b2da3-226">Azure Media Services Analytics a genel bakış</span><span class="sxs-lookup"><span data-stu-id="b2da3-226">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="b2da3-227">Azure medya analizi gösterileri</span><span class="sxs-lookup"><span data-stu-id="b2da3-227">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

