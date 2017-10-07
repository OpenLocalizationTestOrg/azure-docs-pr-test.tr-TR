---
title: aaaMedia Analytics hello Media Services platformunda | Microsoft Docs
description: "Medya analizi, Kurumsal ölçek, uyumluluk, güvenlik ve genel ulaşma konuşma ve bilgisayar görme hizmetler koleksiyonu genel önizlemesi genel bakış"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c56e3781-8510-4f7f-b5ff-a218c1bb6f4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2017
ms.author: milanga;juliako;johndeu
ms.openlocfilehash: 7545f0532d7618164ebe65e2f4232c5f63453cfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="media-analytics-on-hello-media-services-platform"></a><span data-ttu-id="48e31-103">Medya analizi hello Media Services platformda</span><span class="sxs-lookup"><span data-stu-id="48e31-103">Media Analytics on hello Media Services platform</span></span>
## <a name="overview"></a><span data-ttu-id="48e31-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="48e31-104">Overview</span></span>
<span data-ttu-id="48e31-105">Daha fazla kuruluşlar video tercih edilen Orta tootrain hello gibi çalışanların kullanıyorsanız, müşterileri ve belge iş işlevleri gerçekleştirmesine.</span><span class="sxs-lookup"><span data-stu-id="48e31-105">More organizations are using video as hello preferred medium tootrain their employees, engage their customers, and document business functions.</span></span> <span data-ttu-id="48e31-106">Sağlayan bir şekilde toostore bulut akış ve bu büyük medya dosyalarını erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48e31-106">Cloud computing provides a way toostore, stream, and access these large media files.</span></span> <span data-ttu-id="48e31-107">Ancak bir şirketin kitaplığı video içeriğinin büyüdükçe Öngörüler Merhaba içeriğine ayıklanması, eşit etkili bir yol gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="48e31-107">But as a company's library of video content grows, it needs an equally effective means of extracting insights from hello content.</span></span> 

<span data-ttu-id="48e31-108">tooaddress Azure Media Services bu büyüyen gereksiniminin Azure medya analizi sunar.</span><span class="sxs-lookup"><span data-stu-id="48e31-108">tooaddress this growing need, Azure Media Services offers Azure Media Analytics.</span></span> <span data-ttu-id="48e31-109">Medya analizi, kuruluş ve işletmelerin tooderive eyleme dönüştürülebilir Öngörüler kendi video dosyalarından kolaylaştırır konuşma ve görme bileşenidir koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="48e31-109">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="48e31-110">Merhaba çekirdek Media Services platform bileşenleri kullanılarak oluşturulmuş, medya analizi medya gün bir ölçekte işleme işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="48e31-110">Built by using hello core Media Services platform components, Media Analytics can handle media processing at scale on day one.</span></span>

<span data-ttu-id="48e31-111">Medya Analizi ile geliştiricilerin hızla Gelişmiş video işlevselliği uygulamalara kullanıma sunabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48e31-111">With Media Analytics, developers can quickly bring advanced video functionality into applications.</span></span> <span data-ttu-id="48e31-112">Kurumsal ortamlarda hello tam ölçekli, uyumluluk, güvenlik ve büyük kuruluşlar tarafından gerekli genel erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="48e31-112">It provides enterprise environments with hello full scale, compliance, security, and global reach required by large organizations.</span></span>

<span data-ttu-id="48e31-113">Merhaba Aşağıdaki diyagramda medya analizi ve hello Media Services platformunun diğer başlıca parçaları gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="48e31-113">hello following diagram shows Media Analytics and other major parts of hello Media Services platform.</span></span> 

![VoD iş akışı](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

<span data-ttu-id="48e31-115">Medya Analizi medya işlemcileri MP4 veya JSON dosyaları üretir.</span><span class="sxs-lookup"><span data-stu-id="48e31-115">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="48e31-116">Medya işlemcisi bir MP4 dosyası oluşturursa hello dosyayı aşamalı olarak indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48e31-116">If a media processor produces an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="48e31-117">Medya işlemcisi bir JSON dosyası oluşturursa, Azure Blob depolama alanından hello dosyayı indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48e31-117">If a media processor produces a JSON file, you can download hello file from Azure Blob storage.</span></span> 

## <a name="media-analytics-services"></a><span data-ttu-id="48e31-118">Medya analizi hizmetlerinden</span><span class="sxs-lookup"><span data-stu-id="48e31-118">Media Analytics services</span></span>

### <a name="indexer"></a><span data-ttu-id="48e31-119">Dizinleyici</span><span class="sxs-lookup"><span data-stu-id="48e31-119">Indexer</span></span>
<span data-ttu-id="48e31-120">Azure Media Indexer ile aranabilir içerik ve kapalı açıklamalı parçaları oluşturmak yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48e31-120">With Azure Media Indexer, you can make content searchable and generate closed-captioning tracks.</span></span> <span data-ttu-id="48e31-121">Karşılaştırılan toohello önceki sürümü, Azure Media Indexer 2 Önizleme hızlı dizin oluşturma ve daha geniş dil desteği içerir.</span><span class="sxs-lookup"><span data-stu-id="48e31-121">Compared toohello previous version, Azure Media Indexer 2 Preview has faster indexing and broader language support.</span></span> <span data-ttu-id="48e31-122">Desteklenen diller, İngilizce, İspanyolca, Fransızca, Almanca, İtalyanca, Çince, Portekizce ve Arapça içerir.</span><span class="sxs-lookup"><span data-stu-id="48e31-122">Supported languages include English, Spanish, French, German, Italian, Chinese, Portuguese, and Arabic.</span></span> <span data-ttu-id="48e31-123">Ayrıntılı bilgi ve örnekler için bkz: [Azure Media Indexer 2 ile video işleme](media-services-process-content-with-indexer2.md).</span><span class="sxs-lookup"><span data-stu-id="48e31-123">For detailed information and examples, see [Process videos with Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span></span>
### <a name="hyperlapse"></a><span data-ttu-id="48e31-124">Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="48e31-124">Hyperlapse</span></span>
<span data-ttu-id="48e31-125">Microsoft Hyperlapse video sabitlemeyi ve zaman atlama yetenek toocreate hızlı, kaynaklarda videoların uzun formlu içeriğinizi birleştirir.</span><span class="sxs-lookup"><span data-stu-id="48e31-125">Microsoft Hyperlapse combines video stabilization and time-lapse capability toocreate quick, consumable videos from your long-form content.</span></span> <span data-ttu-id="48e31-126">Zaman atlama video oluşturmanın yanı sıra Hyperlapse toocreate kararlı videoların cep telefonları ve kameralar aracılığıyla yakalanan shaky videolar kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48e31-126">Besides creating time-lapse video, you can use Hyperlapse toocreate stable videos from shaky videos captured via cell phones and camcorders.</span></span> <span data-ttu-id="48e31-127">Ayrıntılı bilgi ve örnekler için bkz: [Hyperlapse Azure medya Hyperlapse ile medya dosyalarını](media-services-hyperlapse-content.md).</span><span class="sxs-lookup"><span data-stu-id="48e31-127">For detailed information and examples, see [Hyperlapse media files with Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span></span>
### <a name="motion-detector"></a><span data-ttu-id="48e31-128">Hareket Algılayıcısı</span><span class="sxs-lookup"><span data-stu-id="48e31-128">Motion Detector</span></span>
<span data-ttu-id="48e31-129">Hareket algılayıcısı toodetect hareket video sabit arka plan ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48e31-129">You can use Motion Detector toodetect motion in a video with stationary backgrounds.</span></span> <span data-ttu-id="48e31-130">Bu, hatalı pozitif sonuç için olası toocheck hareket olayları izleme kameralarını tarafından algılanan kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="48e31-130">This makes it possible toocheck for false positives on motion events detected by surveillance cameras.</span></span> <span data-ttu-id="48e31-131">Ayrıntılı bilgi ve örnekler için bkz: [hareket algılama Azure medya analizi için](media-services-motion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="48e31-131">For detailed information and examples, see [Motion detection for Azure Media Analytics](media-services-motion-detection.md).</span></span>
### <a name="face-detector"></a><span data-ttu-id="48e31-132">Yüz Algılayıcısı</span><span class="sxs-lookup"><span data-stu-id="48e31-132">Face Detector</span></span>
<span data-ttu-id="48e31-133">Yüz algılayıcısı kullanarak, kişilerin yüzeyleri ve mutluluk, sadness ve beklenmedik biçimde dahil olmak üzere kendi duygular algılayabilir.</span><span class="sxs-lookup"><span data-stu-id="48e31-133">By using Face Detector, you can detect people’s faces and their emotions, including happiness, sadness, and surprise.</span></span> <span data-ttu-id="48e31-134">Bu, toplama ve analiz etme tepki olaya katılan kişilerin de dahil olmak üzere daha sonra açıklanan çeşitli yararlı endüstri uygulamalar, sahiptir.</span><span class="sxs-lookup"><span data-stu-id="48e31-134">This has several useful industry applications, described later, including aggregating and analyzing reactions of people attending an event.</span></span> <span data-ttu-id="48e31-135">Ayrıntılı bilgi ve örnekler için bkz: [Azure medya analizi için yüz ve duygu algılama](media-services-face-and-emotion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="48e31-135">For detailed information and examples, see [Face and emotion detection for Azure Media Analytics](media-services-face-and-emotion-detection.md).</span></span>
### <a name="video-summarization"></a><span data-ttu-id="48e31-136">Video özetleme</span><span class="sxs-lookup"><span data-stu-id="48e31-136">Video summarization</span></span>
<span data-ttu-id="48e31-137">Video özetleme otomatik olarak hello kaynak video ilginç parçacıkları'i seçerek uzun videoları özetlerini oluşturmanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="48e31-137">Video summarization can help you create summaries of long videos by automatically selecting interesting snippets from hello source video.</span></span> <span data-ttu-id="48e31-138">Bu özellik, tooprovide hangi tooexpect uzun videoda hızlı bir genel bakış istediğinizde yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="48e31-138">This ability is useful when you want tooprovide a quick overview of what tooexpect in a long video.</span></span> <span data-ttu-id="48e31-139">Ayrıntılı bilgi ve örnekler için bkz: [kullanım Azure medya Video küçük resimleri toocreate video özetleme](media-services-video-summarization.md).</span><span class="sxs-lookup"><span data-stu-id="48e31-139">For detailed information and examples, see [Use Azure Media Video Thumbnails toocreate video summarization](media-services-video-summarization.md).</span></span>
### <a name="optical-character-recognition"></a><span data-ttu-id="48e31-140">Optik karakter tanıma</span><span class="sxs-lookup"><span data-stu-id="48e31-140">Optical character recognition</span></span>
<span data-ttu-id="48e31-141">Azure Media ORC (optik karakter tanıma) ile video dosyaları metin içeriği düzenlenebilir, aranabilir dijital metne dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48e31-141">With Azure Media OCR (optical character recognition), you can convert text content in video files into editable, searchable digital text.</span></span> <span data-ttu-id="48e31-142">Ardından hello video sinyali medyanızın anlamlı meta verilerin hello ayıklama otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48e31-142">You can then automate hello extraction of meaningful metadata from hello video signal of your media.</span></span>
### <a name="scalable-face-redaction"></a><span data-ttu-id="48e31-143">Ölçeklenebilir yüz Redaksiyon</span><span class="sxs-lookup"><span data-stu-id="48e31-143">Scalable face redaction</span></span>
<span data-ttu-id="48e31-144">Azure Media Redactor ölçeklenebilir yüz Redaksiyon hello bulutta sunan medya analizi medya işlemcisi ' dir.</span><span class="sxs-lookup"><span data-stu-id="48e31-144">Azure Media Redactor is a Media Analytics media processor that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="48e31-145">Yüz Redaksiyon kullanarak, seçilen kişilerin, video tooblur yüzeyleri değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48e31-145">By using face redaction, you can modify your video tooblur faces of selected individuals.</span></span> <span data-ttu-id="48e31-146">Toouse hello yüz Redaksiyon hizmet haber ortamda veya ortak güvenlik söz konusu olduğunda isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48e31-146">You might want toouse hello face redaction service in news media or when public safety is involved.</span></span> <span data-ttu-id="48e31-147">Saat tooredact el ile birden çok yüzeyleri içeren çekimi birkaç dakika sürebilir, ancak bu hizmetle yüz Redaksiyon birkaç basit adımla alır.</span><span class="sxs-lookup"><span data-stu-id="48e31-147">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service, face redaction takes just a few simple steps.</span></span> <span data-ttu-id="48e31-148">Merhaba daha fazla bilgi için bkz: [Redaksiyon yüzeyleri Azure medya Analizi ile](media-services-face-redaction.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="48e31-148">For more information, see hello [Redact faces with Azure Media Analytics](media-services-face-redaction.md) article.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="48e31-149">Genel senaryolar</span><span class="sxs-lookup"><span data-stu-id="48e31-149">Common scenarios</span></span>
<span data-ttu-id="48e31-150">Medya analizi kuruluşlara yardımcı olur ve işletmelerin video ilişkin yeni bilgiler glean ve daha etkili bir şekilde video içeriği büyük miktarda yönetin.</span><span class="sxs-lookup"><span data-stu-id="48e31-150">Media Analytics can help organizations and enterprises glean new insights from video and more effectively manage large volumes of video content.</span></span> <span data-ttu-id="48e31-151">Burada, çeşitli senaryolar vardır:</span><span class="sxs-lookup"><span data-stu-id="48e31-151">Here are several scenarios:</span></span>

* <span data-ttu-id="48e31-152">**Çağrı merkezleri**.</span><span class="sxs-lookup"><span data-stu-id="48e31-152">**Call centers**.</span></span> <span data-ttu-id="48e31-153">Hatta hello geliştirilirken sosyal medya ile müşteri çağrı merkezleri hala müşteri hizmetleri işlemleri büyük bir yüzdesini kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="48e31-153">Even with hello advent of social media, customer call centers still facilitate a large percentage of customer-service transactions.</span></span> <span data-ttu-id="48e31-154">Bu ses verilerde büyük miktarda olabilir müşteri bilgi tooachieve daha yüksek müşteri memnuniyetini analiz kodlanır.</span><span class="sxs-lookup"><span data-stu-id="48e31-154">Encoded in this audio data is a large amount of customer information that can be analyzed tooachieve higher customer satisfaction.</span></span> <span data-ttu-id="48e31-155">Kuruluşlar, medya Dizin Oluşturucu kullanarak metin ayıklayın ve arama dizinlerini ve panolar oluşturmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="48e31-155">By using Media Indexer, organizations can extract text and build search indexes and dashboards.</span></span> <span data-ttu-id="48e31-156">Ardından bunlar yaygın şikayetlerinden, şikayetlerinden kaynaklarını ve diğer ilgili verileri çevresinde Intelligence ayıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48e31-156">Then they can extract intelligence around common complaints, sources of complaints, and other relevant data.</span></span>
* <span data-ttu-id="48e31-157">**Kullanıcı tarafından oluşturulmuş içerik yönetimini**.</span><span class="sxs-lookup"><span data-stu-id="48e31-157">**User-generated content moderation**.</span></span> <span data-ttu-id="48e31-158">Haber medya çıkışlar toopolice bölümlerden çoğu kuruluş, videolar ve resimler gibi kullanıcı tarafından oluşturulan medya kabul genel kullanıma yönelik portalları sahiptir.</span><span class="sxs-lookup"><span data-stu-id="48e31-158">From news media outlets toopolice departments, many organizations have public-facing portals that accept user-generated media such as videos and images.</span></span> <span data-ttu-id="48e31-159">İçerik Hello hacmi toounexpected olaylar ani değişiklik.</span><span class="sxs-lookup"><span data-stu-id="48e31-159">hello volume of content can spike due toounexpected events.</span></span> <span data-ttu-id="48e31-160">Bu senaryolarda, bu site için içeriği etkili el ile incelemeler zor tooconduct olur.</span><span class="sxs-lookup"><span data-stu-id="48e31-160">In these scenarios, it is difficult tooconduct effective manual reviews of content for appropriateness.</span></span> <span data-ttu-id="48e31-161">Müşteriler, uygun olan içerik üzerinde hello içerik yönetimini hizmet toofocus üzerinde güvenebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48e31-161">Customers can rely on hello content-moderation service toofocus on content that is appropriate.</span></span>
* <span data-ttu-id="48e31-162">**İzleme**.</span><span class="sxs-lookup"><span data-stu-id="48e31-162">**Surveillance**.</span></span> <span data-ttu-id="48e31-163">Merhaba ile kullanımı büyüme IP kamera gözetleme video büyüyen bir envanterini gelir.</span><span class="sxs-lookup"><span data-stu-id="48e31-163">With hello growth in use of IP cameras comes a growing inventory of surveillance video.</span></span> <span data-ttu-id="48e31-164">El ile izleme video gözden geçirme zamanı yoğun ve saldırıya toohuman hatasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="48e31-164">Manually reviewing surveillance video is time intensive and prone toohuman error.</span></span> <span data-ttu-id="48e31-165">Medya analizi hareket algılama, yüz algılama ve gözden geçirme, yönetme ve türevleri daha kolay oluşturma Hyperlapse toomake hello işlemi gibi hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="48e31-165">Media Analytics provides services such as motion detection, face detection, and Hyperlapse toomake hello process of reviewing, managing, and creating derivatives easier.</span></span>

## <a name="media-analytics-media-processors"></a><span data-ttu-id="48e31-166">Medya analizi medya işlemcileri</span><span class="sxs-lookup"><span data-stu-id="48e31-166">Media Analytics media processors</span></span>
<span data-ttu-id="48e31-167">Bu bölümün listeleri hello medya analizi medya işlemcileri ve programlarını nasıl toouse .NET veya REST tooget medya işlemci (MP) nesnesi.</span><span class="sxs-lookup"><span data-stu-id="48e31-167">This section lists hello Media Analytics media processors and shows how toouse .NET or REST tooget a media processor (MP) object.</span></span>

### <a name="mp-names"></a><span data-ttu-id="48e31-168">MP adları</span><span class="sxs-lookup"><span data-stu-id="48e31-168">MP names</span></span>
* <span data-ttu-id="48e31-169">Azure Media Indexer 2 Önizleme</span><span class="sxs-lookup"><span data-stu-id="48e31-169">Azure Media Indexer 2 Preview</span></span>
* <span data-ttu-id="48e31-170">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="48e31-170">Azure Media Indexer</span></span>
* <span data-ttu-id="48e31-171">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="48e31-171">Azure Media Hyperlapse</span></span>
* <span data-ttu-id="48e31-172">Azure Media Face Detector</span><span class="sxs-lookup"><span data-stu-id="48e31-172">Azure Media Face Detector</span></span>
* <span data-ttu-id="48e31-173">Azure Media Motion Detector</span><span class="sxs-lookup"><span data-stu-id="48e31-173">Azure Media Motion Detector</span></span>
* <span data-ttu-id="48e31-174">Azure Media Video Thumbnails</span><span class="sxs-lookup"><span data-stu-id="48e31-174">Azure Media Video Thumbnails</span></span>
* <span data-ttu-id="48e31-175">Azure Media OCR</span><span class="sxs-lookup"><span data-stu-id="48e31-175">Azure Media OCR</span></span>

### <a name="net"></a><span data-ttu-id="48e31-176">.NET</span><span class="sxs-lookup"><span data-stu-id="48e31-176">.NET</span></span>
<span data-ttu-id="48e31-177">Merhaba, bir işlev alır aşağıdaki hello belirtilen MP adları ve bir MP nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="48e31-177">hello following function takes one of hello specified MP names and returns an MP object.</span></span>

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


### <a name="rest"></a><span data-ttu-id="48e31-178">REST</span><span class="sxs-lookup"><span data-stu-id="48e31-178">REST</span></span>
<span data-ttu-id="48e31-179">İsteği:</span><span class="sxs-lookup"><span data-stu-id="48e31-179">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

<span data-ttu-id="48e31-180">Yanıtı:</span><span class="sxs-lookup"><span data-stu-id="48e31-180">Response:</span></span>

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:074c3899-d9fb-448f-9ae1-4ebcbe633056",
             "Description":"Azure Media OCR",
             "Name":"Azure Media OCR",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

## <a name="demos"></a><span data-ttu-id="48e31-181">Gösterileri</span><span class="sxs-lookup"><span data-stu-id="48e31-181">Demos</span></span>
<span data-ttu-id="48e31-182">Bkz: [Azure medya analizi gösterileri](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span><span class="sxs-lookup"><span data-stu-id="48e31-182">See [Azure Media Analytics demos](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="48e31-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="48e31-183">Next steps</span></span>
<span data-ttu-id="48e31-184">Media Services öğrenme yollarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="48e31-184">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="48e31-185">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="48e31-185">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="48e31-186">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="48e31-186">Related articles</span></span>
<span data-ttu-id="48e31-187">Bkz: [medya Hizmetleri analizi duyuru](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span><span class="sxs-lookup"><span data-stu-id="48e31-187">See [Media Services Analytics announcement](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span></span>

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
