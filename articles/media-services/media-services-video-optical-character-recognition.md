---
title: Azure medya analizi OCR aaaDigitize metinle | Microsoft Docs
description: "Azure medya analizi OCR (optik karakter tanıma) düzenlenebilir, aranabilir dijital metne video dosyalarında tooconvert metin içeriği sağlar.  Bu, medya video sinyali hello anlamlı meta verilerin tooautomate hello ayıklama sağlar."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 307c196e-3a50-4f4b-b982-51585448ffc6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 0476c3ba3942b2c5182a34a429909adbf5c75ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-analytics-tooconvert-text-content-in-video-files-into-digital-text"></a><span data-ttu-id="4effb-104">Azure medya analizi tooconvert metin içeriği video dosyalarında dijital metne kullanın.</span><span class="sxs-lookup"><span data-stu-id="4effb-104">Use Azure Media Analytics tooconvert text content in video files into digital text</span></span>
## <a name="overview"></a><span data-ttu-id="4effb-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="4effb-105">Overview</span></span>
<span data-ttu-id="4effb-106">Video dosyalarından tooextract metin içerik gerekir ve düzenlenebilir, aranabilir dijital metin oluşturan Azure medya analizi OCR (optik karakter tanıma) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4effb-106">If you need tooextract text content from your video files and generate an editable, searchable digital text, you should use Azure Media Analytics OCR (optical character recognition).</span></span> <span data-ttu-id="4effb-107">Bu Azure medya işlemcisi video dosyalarında metin içeriği algılar ve kendi kullanımınız için metin dosyaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4effb-107">This Azure Media Processor detects text content in your video files and generates text files for your use.</span></span> <span data-ttu-id="4effb-108">OCR, tooautomate hello ayıklama anlamlı meta verilerin hello video sinyali medyanızın sağlar.</span><span class="sxs-lookup"><span data-stu-id="4effb-108">OCR enables you tooautomate hello extraction of meaningful metadata from hello video signal of your media.</span></span>

<span data-ttu-id="4effb-109">Bir arama motoru ile birlikte kullanıldığında, kolayca medyanızı metin dizin ve içeriğinizi hello bulunabilirliğini artırmak.</span><span class="sxs-lookup"><span data-stu-id="4effb-109">When used in conjunction with a search engine, you can easily index your media by text, and enhance hello discoverability of your content.</span></span> <span data-ttu-id="4effb-110">Bu bir video kaydı veya bir slayt gösterisi sunumu ekran yakalama gibi yüksek oranda metinsel videoda son derece yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="4effb-110">This is extremely useful in highly textual video, like a video recording or screen-capture of a slideshow presentation.</span></span> <span data-ttu-id="4effb-111">Hello Azure OCR medya işlemcisi dijital metin için optimize edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4effb-111">hello Azure OCR Media Processor is optimized for digital text.</span></span>

<span data-ttu-id="4effb-112">Merhaba **Azure medya OCR** medya işlemcisi şu anda önizlemede.</span><span class="sxs-lookup"><span data-stu-id="4effb-112">hello **Azure Media OCR** media processor is currently in Preview.</span></span>

<span data-ttu-id="4effb-113">Bu konu hakkında ayrıntılar verir **Azure medya OCR** ve gösterir nasıl toouse .NET için Media Services SDK'sı ile.</span><span class="sxs-lookup"><span data-stu-id="4effb-113">This topic gives details about  **Azure Media OCR** and shows how toouse it with Media Services SDK for .NET.</span></span> <span data-ttu-id="4effb-114">Ek bilgi ve örnekler için bkz: [bu blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span><span class="sxs-lookup"><span data-stu-id="4effb-114">For additional information and examples, see [this blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span></span>

## <a name="ocr-input-files"></a><span data-ttu-id="4effb-115">OCR giriş dosyaları</span><span class="sxs-lookup"><span data-stu-id="4effb-115">OCR input files</span></span>
<span data-ttu-id="4effb-116">Video dosyaları.</span><span class="sxs-lookup"><span data-stu-id="4effb-116">Video files.</span></span> <span data-ttu-id="4effb-117">Şu anda biçimleri aşağıdaki hello desteklenir: MP4, MOV ve WMV.</span><span class="sxs-lookup"><span data-stu-id="4effb-117">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration"></a><span data-ttu-id="4effb-118">Görev yapılandırması</span><span class="sxs-lookup"><span data-stu-id="4effb-118">Task configuration</span></span>
<span data-ttu-id="4effb-119">Görev yapılandırması (hazır).</span><span class="sxs-lookup"><span data-stu-id="4effb-119">Task configuration (preset).</span></span> <span data-ttu-id="4effb-120">Bir görev oluştururken **Azure medya OCR**, JSON veya XML kullanarak önceden belirlenmiş bir yapılandırma belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4effb-120">When creating a task with **Azure Media OCR**, you must specify a configuration preset using JSON  or XML.</span></span> 

>[!NOTE]
><span data-ttu-id="4effb-121">Merhaba OCR altyapısı minimum 40 piksel toomaximum 32000 piksel görüntü bölgesiyle hem yükseklik/genişlik içinde geçerli bir giriş olarak yalnızca alır.</span><span class="sxs-lookup"><span data-stu-id="4effb-121">hello OCR engine only takes an image region with minimum 40 pixels toomaximum 32000 pixels as a valid input in both height/width.</span></span>
>

### <a name="attribute-descriptions"></a><span data-ttu-id="4effb-122">Öznitelik tanımlarını</span><span class="sxs-lookup"><span data-stu-id="4effb-122">Attribute descriptions</span></span>
| <span data-ttu-id="4effb-123">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="4effb-123">Attribute name</span></span> | <span data-ttu-id="4effb-124">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4effb-124">Description</span></span> |
| --- | --- |
|<span data-ttu-id="4effb-125">AdvancedOutput</span><span class="sxs-lookup"><span data-stu-id="4effb-125">AdvancedOutput</span></span>| <span data-ttu-id="4effb-126">Merhaba JSON çıktısını AdvancedOutput tootrue ayarlarsanız, her tek Word'de (toplama toophrases ve bölgeler) için konumsal veri içermez.</span><span class="sxs-lookup"><span data-stu-id="4effb-126">If you set AdvancedOutput tootrue, hello JSON output will contain positional data for every single word (in addition toophrases and regions).</span></span> <span data-ttu-id="4effb-127">Bu ayrıntılar toosee istemiyorsanız hello bayrağı toofalse ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4effb-127">If you do not want toosee these details, set hello flag toofalse.</span></span> <span data-ttu-id="4effb-128">Merhaba varsayılan değer false şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="4effb-128">hello default value is false.</span></span> <span data-ttu-id="4effb-129">Daha fazla bilgi için bkz: [bu blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span><span class="sxs-lookup"><span data-stu-id="4effb-129">For more information, see [this blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span></span>|
| <span data-ttu-id="4effb-130">Dil</span><span class="sxs-lookup"><span data-stu-id="4effb-130">Language</span></span> |<span data-ttu-id="4effb-131">(isteğe bağlı) için hangi toolook metin hello dilini açıklar.</span><span class="sxs-lookup"><span data-stu-id="4effb-131">(optional) describes hello language of text for which toolook.</span></span> <span data-ttu-id="4effb-132">Merhaba aşağıdakilerden biri: Otomatik Algıla (varsayılan), Arapça, ChineseSimplified, ChineseTraditional, Çekçe Danca, Felemenkçe, İngilizce, Fince, Fransızca, Almanca, Yunanca, Macarca, İtalyanca, Japonca, Korece, Norveççe, Lehçe, Portekizce, Rumence, Rusça, SerbianCyrillic, SerbianLatin, Slovakça, İspanyolca, İsveççe, Türkçe.</span><span class="sxs-lookup"><span data-stu-id="4effb-132">One of hello following: AutoDetect (default), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German,  Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span></span> |
| <span data-ttu-id="4effb-133">TextOrientation</span><span class="sxs-lookup"><span data-stu-id="4effb-133">TextOrientation</span></span> |<span data-ttu-id="4effb-134">(isteğe bağlı) için hangi toolook metnin hello yönünü açıklar.</span><span class="sxs-lookup"><span data-stu-id="4effb-134">(optional) describes hello orientation of text for which toolook.</span></span>  <span data-ttu-id="4effb-135">Tüm harfler üstündeki hello "Sol" anlamına gelir hello sola doğru işaret.</span><span class="sxs-lookup"><span data-stu-id="4effb-135">"Left" means that hello top of all letters are pointed towards hello left.</span></span>  <span data-ttu-id="4effb-136">Varsayılan metin (örneğin, kitaptaki bulunan) "Yedekleme" yönlendirilmiş çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="4effb-136">Default text (like that which can be found in a book) can be called "Up" oriented.</span></span>  <span data-ttu-id="4effb-137">Merhaba aşağıdakilerden biri: Otomatik Algıla (varsayılan), sağ, aşağı, sol.</span><span class="sxs-lookup"><span data-stu-id="4effb-137">One of hello following: AutoDetect (default), Up, Right, Down, Left.</span></span> |
| <span data-ttu-id="4effb-138">TimeInterval</span><span class="sxs-lookup"><span data-stu-id="4effb-138">TimeInterval</span></span> |<span data-ttu-id="4effb-139">(isteğe bağlı) hello örnekleme oranını açıklar.</span><span class="sxs-lookup"><span data-stu-id="4effb-139">(optional) describes hello sampling rate.</span></span>  <span data-ttu-id="4effb-140">1/2 saniyede varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="4effb-140">Default is every 1/2 second.</span></span><br/><span data-ttu-id="4effb-141">JSON biçimi – SS: dd:. SSS (varsayılan 00:00:00.500)</span><span class="sxs-lookup"><span data-stu-id="4effb-141">JSON format – HH:mm:ss.SSS (default 00:00:00.500)</span></span><br/><span data-ttu-id="4effb-142">XML biçiminde – W3C XSD süresi ilkel (varsayılan PT0.5)</span><span class="sxs-lookup"><span data-stu-id="4effb-142">XML format – W3C XSD duration primitive (default PT0.5)</span></span> |
| <span data-ttu-id="4effb-143">DetectRegions</span><span class="sxs-lookup"><span data-stu-id="4effb-143">DetectRegions</span></span> |<span data-ttu-id="4effb-144">(isteğe bağlı) Hangi toodetect metinde hello video çerçevesinde bölgeler belirtme DetectRegion nesnelerinin bir dizisi.</span><span class="sxs-lookup"><span data-stu-id="4effb-144">(optional) An array of DetectRegion objects specifying regions within hello video frame in which toodetect text.</span></span><br/><span data-ttu-id="4effb-145">Bir DetectRegion nesnesi dört tamsayı değerleri aşağıdaki hello yapılır:</span><span class="sxs-lookup"><span data-stu-id="4effb-145">A DetectRegion object is made of hello following four integer values:</span></span><br/><span data-ttu-id="4effb-146">Sol – hello sol kenar boşluğu piksellerden</span><span class="sxs-lookup"><span data-stu-id="4effb-146">Left – pixels from hello left-margin</span></span><br/><span data-ttu-id="4effb-147">Üst – hello üst kenar boşluğu piksellerden</span><span class="sxs-lookup"><span data-stu-id="4effb-147">Top – pixels from hello top-margin</span></span><br/><span data-ttu-id="4effb-148">Genişlik – hello bölge piksel cinsinden genişliği</span><span class="sxs-lookup"><span data-stu-id="4effb-148">Width – width of hello region in pixels</span></span><br/><span data-ttu-id="4effb-149">Yükseklik – hello bölge piksel cinsinden yüksekliği</span><span class="sxs-lookup"><span data-stu-id="4effb-149">Height – height of hello region in pixels</span></span> |

#### <a name="json-preset-example"></a><span data-ttu-id="4effb-150">Örnek JSON hazır</span><span class="sxs-lookup"><span data-stu-id="4effb-150">JSON preset example</span></span>

    {
        "Version":1.0, 
        "Options": 
        {
            "AdvancedOutput":"true",
            "Language":"English", 
            "TimeInterval":"00:00:01.5",
            "TextOrientation":"Up",
            "DetectRegions": [
                    {
                       "Left": 10,
                       "Top": 10,
                       "Width": 100,
                       "Height": 50
                    }
             ]
        }
    }


#### <a name="xml-preset-example"></a><span data-ttu-id="4effb-151">XML hazır örneği</span><span class="sxs-lookup"><span data-stu-id="4effb-151">XML preset example</span></span>
    <?xml version=""1.0"" encoding=""utf-16""?>
    <VideoOcrPreset xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" Version=""1.0"" xmlns=""http://www.windowsazure.com/media/encoding/Preset/2014/03"">
      <Options>
         <AdvancedOutput>true</AdvancedOutput>
         <Language>English</Language>
         <TimeInterval>PT1.5S</TimeInterval>
         <DetectRegions>
             <DetectRegion>
                   <Left>10</Left>
                   <Top>10</Top>
                   <Width>100</Width>
                   <Height>50</Height>
            </DetectRegion>
       </DetectRegions>
       <TextOrientation>Up</TextOrientation>
      </Options>
    </VideoOcrPreset>

## <a name="ocr-output-files"></a><span data-ttu-id="4effb-152">OCR çıktı dosyaları</span><span class="sxs-lookup"><span data-stu-id="4effb-152">OCR output files</span></span>
<span data-ttu-id="4effb-153">Merhaba çıktı hello OCR medya işlemcisi bir JSON dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="4effb-153">hello output of hello OCR media processor is a JSON file.</span></span>

### <a name="elements-of-hello-output-json-file"></a><span data-ttu-id="4effb-154">Merhaba çıkış JSON dosyasının öğeleri</span><span class="sxs-lookup"><span data-stu-id="4effb-154">Elements of hello output JSON file</span></span>
<span data-ttu-id="4effb-155">Merhaba Video OCR çıktı hello karakterler videonuzu içinde bulundu zaman kesimli veri sağlar.</span><span class="sxs-lookup"><span data-stu-id="4effb-155">hello Video OCR output provides time-segmented data on hello characters found in your video.</span></span>  <span data-ttu-id="4effb-156">Tam olarak çözümlenmesinde ilgilenen hello sözcükleri dil veya yönde toohone gibi öznitelikleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4effb-156">You can use attributes such as language or orientation toohone-in on exactly hello words that you are interested in analyzing.</span></span> 

<span data-ttu-id="4effb-157">Merhaba çıkış öznitelikleri aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="4effb-157">hello output contains hello following attributes:</span></span>

| <span data-ttu-id="4effb-158">Öğesi</span><span class="sxs-lookup"><span data-stu-id="4effb-158">Element</span></span> | <span data-ttu-id="4effb-159">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4effb-159">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4effb-160">Zaman Çizelgesi</span><span class="sxs-lookup"><span data-stu-id="4effb-160">Timescale</span></span> |<span data-ttu-id="4effb-161">Merhaba videonun saniyede "çizgilerine"</span><span class="sxs-lookup"><span data-stu-id="4effb-161">"ticks" per second of hello video</span></span> |
| <span data-ttu-id="4effb-162">Uzaklık</span><span class="sxs-lookup"><span data-stu-id="4effb-162">Offset</span></span> |<span data-ttu-id="4effb-163">zaman damgaları için uzaklık.</span><span class="sxs-lookup"><span data-stu-id="4effb-163">time offset for timestamps.</span></span> <span data-ttu-id="4effb-164">Video API'leri 1.0 sürümünde, bu her zaman 0 olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4effb-164">In version 1.0 of Video APIs, this will always be 0.</span></span> |
| <span data-ttu-id="4effb-165">Kare hızı</span><span class="sxs-lookup"><span data-stu-id="4effb-165">Framerate</span></span> |<span data-ttu-id="4effb-166">Saniyedeki kare hello video sayısı</span><span class="sxs-lookup"><span data-stu-id="4effb-166">Frames per second of hello video</span></span> |
| <span data-ttu-id="4effb-167">Genişlik</span><span class="sxs-lookup"><span data-stu-id="4effb-167">width</span></span> |<span data-ttu-id="4effb-168">Merhaba video piksel cinsinden genişliği</span><span class="sxs-lookup"><span data-stu-id="4effb-168">width of hello video in pixels</span></span> |
| <span data-ttu-id="4effb-169">Yükseklik</span><span class="sxs-lookup"><span data-stu-id="4effb-169">height</span></span> |<span data-ttu-id="4effb-170">Merhaba piksel cinsinden görüntü yüksekliği</span><span class="sxs-lookup"><span data-stu-id="4effb-170">height of hello video in pixels</span></span> |
| <span data-ttu-id="4effb-171">Parçaları</span><span class="sxs-lookup"><span data-stu-id="4effb-171">Fragments</span></span> |<span data-ttu-id="4effb-172">hangi hello meta verileri öbekli video zamana dayalı parçalarını dizisi</span><span class="sxs-lookup"><span data-stu-id="4effb-172">array of time-based chunks of video into which hello metadata is chunked</span></span> |
| <span data-ttu-id="4effb-173">start</span><span class="sxs-lookup"><span data-stu-id="4effb-173">start</span></span> |<span data-ttu-id="4effb-174">Başlangıç saati "çizgilerine" parçadaki</span><span class="sxs-lookup"><span data-stu-id="4effb-174">start time of a fragment in "ticks"</span></span> |
| <span data-ttu-id="4effb-175">Süre</span><span class="sxs-lookup"><span data-stu-id="4effb-175">duration</span></span> |<span data-ttu-id="4effb-176">"çizgilerine" parçadaki uzunluğu</span><span class="sxs-lookup"><span data-stu-id="4effb-176">length of a fragment in "ticks"</span></span> |
| <span data-ttu-id="4effb-177">interval</span><span class="sxs-lookup"><span data-stu-id="4effb-177">interval</span></span> |<span data-ttu-id="4effb-178">Parça verilen hello içinde her olayın aralığı</span><span class="sxs-lookup"><span data-stu-id="4effb-178">interval of each event within hello given fragment</span></span> |
| <span data-ttu-id="4effb-179">etkinlikler</span><span class="sxs-lookup"><span data-stu-id="4effb-179">events</span></span> |<span data-ttu-id="4effb-180">bölgeleri içeren bir dizi</span><span class="sxs-lookup"><span data-stu-id="4effb-180">array containing regions</span></span> |
| <span data-ttu-id="4effb-181">Bölge</span><span class="sxs-lookup"><span data-stu-id="4effb-181">region</span></span> |<span data-ttu-id="4effb-182">nesnesini temsil eden kelimeler ve ifadeler algılandı</span><span class="sxs-lookup"><span data-stu-id="4effb-182">object representing detected words or phrases</span></span> |
| <span data-ttu-id="4effb-183">Dil</span><span class="sxs-lookup"><span data-stu-id="4effb-183">language</span></span> |<span data-ttu-id="4effb-184">bir bölge içinde algılanan hello metin dili</span><span class="sxs-lookup"><span data-stu-id="4effb-184">language of hello text detected within a region</span></span> |
| <span data-ttu-id="4effb-185">Yönlendirme</span><span class="sxs-lookup"><span data-stu-id="4effb-185">orientation</span></span> |<span data-ttu-id="4effb-186">bir bölge içinde algılanan hello metnin yönünü</span><span class="sxs-lookup"><span data-stu-id="4effb-186">orientation of hello text detected within a region</span></span> |
| <span data-ttu-id="4effb-187">satırları</span><span class="sxs-lookup"><span data-stu-id="4effb-187">lines</span></span> |<span data-ttu-id="4effb-188">bir bölge içinde algılanan metin satırı dizisi</span><span class="sxs-lookup"><span data-stu-id="4effb-188">array of lines of text detected within a region</span></span> |
| <span data-ttu-id="4effb-189">Metin</span><span class="sxs-lookup"><span data-stu-id="4effb-189">text</span></span> |<span data-ttu-id="4effb-190">Merhaba gerçek metin</span><span class="sxs-lookup"><span data-stu-id="4effb-190">hello actual text</span></span> |

### <a name="json-output-example"></a><span data-ttu-id="4effb-191">JSON çıkış örneği</span><span class="sxs-lookup"><span data-stu-id="4effb-191">JSON output example</span></span>
<span data-ttu-id="4effb-192">Merhaba aşağıdaki çıktı örneği hello genel video bilgi ve birkaç video parçalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="4effb-192">hello following output example contains hello general video information and several video fragments.</span></span> <span data-ttu-id="4effb-193">Video her parçasında OCR MP hello dili ve onun metin hizalamasını tarafından algılanan her bölge içerir.</span><span class="sxs-lookup"><span data-stu-id="4effb-193">In every video fragment, it contains every region which is detected by OCR MP with hello language and its text orientation.</span></span> <span data-ttu-id="4effb-194">Merhaba bölge ayrıca her word satır hello hattın metin, hello satırın konumunu ve bu satırdaki her bir word bilgileri (word içerik, konum ve güvenilirlik) ile bu bölgede yer alır.</span><span class="sxs-lookup"><span data-stu-id="4effb-194">hello region also contains every word line in this region with hello line’s text, hello line’s position, and every word information (word content, position and confidence) in this line.</span></span> <span data-ttu-id="4effb-195">Merhaba aşağıda bir örnek verilmiştir ve bazı açıklamalar satır içi yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="4effb-195">hello following is an example, and I put some comments inline.</span></span>

    {
        "version": 1, 
        "timescale": 90000, 
        "offset": 0, 
        "framerate": 30, 
        "width": 640, 
        "height": 480,  // general video information
        "fragments": [
            {
                "start": 0, 
                "duration": 180000, 
                "interval": 90000,  // hello time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // hello detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including hello text and hello position
                                    {
                                        "text": "One Two", 
                                        "left": 10, 
                                        "top": 10, 
                                        "right": 210, 
                                        "bottom": 110, 
                                        "word": [  // word information array in this line
                                            {
                                                "text": "One", 
                                                "left": 10, 
                                                "top": 10, 
                                                "right": 110, 
                                                "bottom": 110, 
                                                "confidence": 900
                                            }, 
                                            {
                                                "text": "Two", 
                                                "left": 110, 
                                                "top": 10, 
                                                "right": 210, 
                                                "bottom": 110, 
                                                "confidence": 910
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                ]
            }
        ]
    }

## <a name="net-sample-code"></a><span data-ttu-id="4effb-196">.NET örnek kod</span><span class="sxs-lookup"><span data-stu-id="4effb-196">.NET sample code</span></span>

<span data-ttu-id="4effb-197">Merhaba aşağıdaki program gösterir nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="4effb-197">hello following program shows how to:</span></span>

1. <span data-ttu-id="4effb-198">Bir varlık oluşturun ve hello varlığa bir medya dosyasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4effb-198">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="4effb-199">İşi bir OCR yapılandırma/hazır dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4effb-199">Create a job with an OCR configuration/preset file.</span></span>
3. <span data-ttu-id="4effb-200">Merhaba çıkış JSON dosyalarını indirin.</span><span class="sxs-lookup"><span data-stu-id="4effb-200">Download hello output JSON files.</span></span> 
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="4effb-201">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4effb-201">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="4effb-202">Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="4effb-202">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="4effb-203">Örnek</span><span class="sxs-lookup"><span data-stu-id="4effb-203">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace OCR
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

                // Run hello OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference tooAzure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="4effb-204">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="4effb-204">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4effb-205">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="4effb-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="4effb-206">İlgili bağlantılar</span><span class="sxs-lookup"><span data-stu-id="4effb-206">Related links</span></span>
[<span data-ttu-id="4effb-207">Azure Media Services Analytics a genel bakış</span><span class="sxs-lookup"><span data-stu-id="4effb-207">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

