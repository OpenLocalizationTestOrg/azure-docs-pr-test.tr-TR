---
title: "aaaHow tooencode medya Kodlayıcı standart kullanarak bir Azure varlığını | Microsoft Docs"
description: "Azure Media Services toouse Medya Kodlayıcısı standart tooencode medya nasıl içerik öğrenin. Kod örnekleri, REST API kullanın."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2a7273c6-8a22-4f82-9bfe-4509ff32d4a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b766bafded7ee98eda3e6ef149c31d5d8fe406fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencode-an-asset-by-using-media-encoder-standard"></a><span data-ttu-id="03b44-104">Nasıl tooencode medya Kodlayıcı standart kullanarak bir varlık</span><span class="sxs-lookup"><span data-stu-id="03b44-104">How tooencode an asset by using Media Encoder Standard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="03b44-105">.NET</span><span class="sxs-lookup"><span data-stu-id="03b44-105">.NET</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [<span data-ttu-id="03b44-106">REST</span><span class="sxs-lookup"><span data-stu-id="03b44-106">REST</span></span>](media-services-rest-encode-asset.md)
> * [<span data-ttu-id="03b44-107">Portal</span><span class="sxs-lookup"><span data-stu-id="03b44-107">Portal</span></span>](media-services-portal-encode.md)
>
>

## <a name="overview"></a><span data-ttu-id="03b44-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="03b44-108">Overview</span></span>
<span data-ttu-id="03b44-109">toodeliver hello Internet üzerinden dijital video, hello medyayı sıkıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="03b44-109">toodeliver digital video over hello Internet, you must compress hello media.</span></span> <span data-ttu-id="03b44-110">Dijital video dosyaları büyük ve çok büyük toodeliver düzgün şekilde hello Internet üzerinden veya müşterilerinizin aygıtları toodisplay olabilir.</span><span class="sxs-lookup"><span data-stu-id="03b44-110">Digital video files are large and may be too big toodeliver over hello Internet, or for your customers’ devices toodisplay properly.</span></span> <span data-ttu-id="03b44-111">Kodlama müşterilerinizin medyanızı görüntüleyebilmeniz için video ve ses sıkıştırma hello işlemidir.</span><span class="sxs-lookup"><span data-stu-id="03b44-111">Encoding is hello process of compressing video and audio so your customers can view your media.</span></span>

<span data-ttu-id="03b44-112">Kodlama işleri hello en yaygın işlemleri Azure Media Services biridir.</span><span class="sxs-lookup"><span data-stu-id="03b44-112">Encoding jobs are one of hello most common processing operations in Azure Media Services.</span></span> <span data-ttu-id="03b44-113">Bir kodlama tooanother kodlama işleri tooconvert medya dosyaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="03b44-113">You create encoding jobs tooconvert media files from one encoding tooanother.</span></span> <span data-ttu-id="03b44-114">Kodlarken, hello Media Services yerleşik Kodlayıcı (Medya Kodlayıcısı standart) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03b44-114">When you encode, you can use hello Media Services built-in encoder (Media Encoder Standard).</span></span> <span data-ttu-id="03b44-115">Bir Media Services iş ortağı tarafından sağlanan bir kodlayıcı de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03b44-115">You can also use an encoder provided by a Media Services partner.</span></span> <span data-ttu-id="03b44-116">Üçüncü taraf kodlayıcılar hello Azure Market kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="03b44-116">Third-party encoders are available through hello Azure Marketplace.</span></span> <span data-ttu-id="03b44-117">Kodlayıcı için tanımlanan Önayar dizeleri veya önceden belirlenmiş yapılandırma dosyalarını kullanarak kodlama görevlerine hello ayrıntılarını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03b44-117">You can specify hello details of encoding tasks by using preset strings defined for your encoder, or by using preset configuration files.</span></span> <span data-ttu-id="03b44-118">kullanılabilir hazır toosee hello türlerini görmek [Medya Kodlayıcısı standart için görev hazır](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="03b44-118">toosee hello types of presets that are available, see [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="03b44-119">Her iş sahip olabilir veya tooaccomplish, işleme hello türüne bağlı olarak daha fazla görev istiyor.</span><span class="sxs-lookup"><span data-stu-id="03b44-119">Each job can have one or more tasks depending on hello type of processing that you want tooaccomplish.</span></span> <span data-ttu-id="03b44-120">Hello REST API, işler ve bunların ilgili görevleri aşağıdaki iki yöntemden biriyle oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="03b44-120">Through hello REST API, you can create jobs and their related tasks in one of two ways:</span></span>

* <span data-ttu-id="03b44-121">Görevler, satır içi olarak tanımlanan iş varlıkları hello görevleri gezinti özelliği aracılığıyla gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="03b44-121">Tasks can be defined inline through hello Tasks navigation property on Job entities.</span></span>
* <span data-ttu-id="03b44-122">OData toplu işleme kullanın.</span><span class="sxs-lookup"><span data-stu-id="03b44-122">Use OData batch processing.</span></span>

<span data-ttu-id="03b44-123">Her zaman Kaynak dosyalarınız Uyarlamalı bit hızlı MP4 kümesi kodlamak ve ardından kullanarak hello kümesi toohello istenen biçimine dönüştürmek öneririz [dinamik paketleme](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="03b44-123">We recommend that you always encode your source files into an adaptive bitrate MP4 set, and then convert hello set toohello desired format by using [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="03b44-124">Çıkış varlığına depolama şifrelenmiş ise, hello varlık teslim ilkesini yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="03b44-124">If your output asset is storage encrypted, you must configure hello asset delivery policy.</span></span> <span data-ttu-id="03b44-125">Daha fazla bilgi için bkz: [varlık teslim ilkesini yapılandırma](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="03b44-125">For more information, see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="03b44-126">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="03b44-126">Considerations</span></span>

<span data-ttu-id="03b44-127">Varlıklar Media Services erişirken, HTTP istekleri özel üstbilgi alanlarını ve değerlerini ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="03b44-127">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="03b44-128">Daha fazla bilgi için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="03b44-128">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

<span data-ttu-id="03b44-129">Medya işlemcileri başvuran başlamadan önce yüklü hello olduğunu doğru medya işlemci kimliğini doğrulayın</span><span class="sxs-lookup"><span data-stu-id="03b44-129">Before you start referencing media processors, verify that you have hello correct media processor ID.</span></span> <span data-ttu-id="03b44-130">Daha fazla bilgi için bkz: [alma medya işlemcileri](media-services-rest-get-media-processor.md).</span><span class="sxs-lookup"><span data-stu-id="03b44-130">For more information, see [Get media processors](media-services-rest-get-media-processor.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="03b44-131">TooMedia Hizmetleri'ne Bağlama</span><span class="sxs-lookup"><span data-stu-id="03b44-131">Connect tooMedia Services</span></span>

<span data-ttu-id="03b44-132">Nasıl tooconnect toohello AMS API, bkz. bilgi [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="03b44-132">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="03b44-133">Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız.</span><span class="sxs-lookup"><span data-stu-id="03b44-133">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="03b44-134">Sonraki çağrılar toohello yapmanız gereken yeni bir URI.</span><span class="sxs-lookup"><span data-stu-id="03b44-134">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-a-job-with-a-single-encoding-task"></a><span data-ttu-id="03b44-135">Bir işi ile tek bir kodlama görev oluşturma</span><span class="sxs-lookup"><span data-stu-id="03b44-135">Create a job with a single encoding task</span></span>
> [!NOTE]
> <span data-ttu-id="03b44-136">Media Services REST API hello ile çalışırken, hello aşağıdaki maddeler geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="03b44-136">When you're working with hello Media Services REST API, hello following considerations apply:</span></span>
>
> <span data-ttu-id="03b44-137">Varlıklar Media Services erişirken, HTTP istekleri özel üstbilgi alanlarını ve değerlerini ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="03b44-137">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="03b44-138">Daha fazla bilgi için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="03b44-138">For more information, see [Setup for Media Services REST API development](media-services-rest-how-to-use.md).</span></span>
>
> <span data-ttu-id="03b44-139">Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız.</span><span class="sxs-lookup"><span data-stu-id="03b44-139">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="03b44-140">Sonraki çağrılar toohello yapmanız gereken yeni bir URI.</span><span class="sxs-lookup"><span data-stu-id="03b44-140">You must make subsequent calls toohello new URI.</span></span> <span data-ttu-id="03b44-141">Nasıl tooconnect toohello AMS API, bkz. bilgi [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="03b44-141">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
>
> <span data-ttu-id="03b44-142">JSON kullanarak ve toouse hello belirterek **__metadata** hello isteğinde hello ayarlamanız gerekir (örneğin, tooreferences bağlantılı nesne), anahtar sözcüğü **kabul** üstbilgisi çok[JSON Verbose biçimi ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Kabul: uygulama/json; odata = verbose.</span><span class="sxs-lookup"><span data-stu-id="03b44-142">When using JSON and specifying toouse hello **__metadata** keyword in hello request (for example, tooreferences a linked object), you must set hello **Accept** header too[JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.</span></span>
>
>

<span data-ttu-id="03b44-143">Aşağıdaki örneğine hello nasıl toocreate ve sonrası bir görev bir işle tooencode bir video belirli çözümleme ve kalite ayarlama gösterir.</span><span class="sxs-lookup"><span data-stu-id="03b44-143">hello following example shows you how toocreate and post a job with one task set tooencode a video at a specific resolution and quality.</span></span> <span data-ttu-id="03b44-144">Medya Kodlayıcısı standart ile kodlamak, belirtilen görev yapılandırması hazır kullanabilirsiniz [burada](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="03b44-144">When you encode with Media Encoder Standard, you can use task configuration presets specified [here](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="03b44-145">İsteği:</span><span class="sxs-lookup"><span data-stu-id="03b44-145">Request:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net

    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aaab7f15b-3136-4ddf-9962-e9ecb28fb9d2')"}}],  "Tasks" : [{"Configuration" : "Adaptive Streaming", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",  "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}

<span data-ttu-id="03b44-146">Yanıtı:</span><span class="sxs-lookup"><span data-stu-id="03b44-146">Response:</span></span>

    HTTP/1.1 201 Created

    . . .

### <a name="set-hello-output-assets-name"></a><span data-ttu-id="03b44-147">Merhaba çıkış varlığın adı ayarlama</span><span class="sxs-lookup"><span data-stu-id="03b44-147">Set hello output asset's name</span></span>
<span data-ttu-id="03b44-148">Aşağıdaki örnek hello nasıl tooset hello assetName özniteliği gösterir:</span><span class="sxs-lookup"><span data-stu-id="03b44-148">hello following example shows how tooset hello assetName attribute:</span></span>

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a><span data-ttu-id="03b44-149">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="03b44-149">Considerations</span></span>
* <span data-ttu-id="03b44-150">TaskBody özellikleri değişmez değer XML toodefine hello sayısı giriş veya başlangıç görevi tarafından kullanılan çıkış varlıklar kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="03b44-150">TaskBody properties must use literal XML toodefine hello number of input, or output assets that are used by hello task.</span></span> <span data-ttu-id="03b44-151">Merhaba görev konu hello XML Merhaba XML şema tanımı içerir.</span><span class="sxs-lookup"><span data-stu-id="03b44-151">hello task topic contains hello XML Schema Definition for hello XML.</span></span>
* <span data-ttu-id="03b44-152">Her iç Hello TaskBody tanımı, değer <inputAsset> ve <outputAsset> JobInputAsset(value) veya JobOutputAsset(value) ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="03b44-152">In hello TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="03b44-153">Bir görev, birden fazla çıkış varlığına sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="03b44-153">A task can have multiple output assets.</span></span> <span data-ttu-id="03b44-154">Bir JobOutputAsset(x) yalnızca bir kez bir görevin bir İşte bir çıkış olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="03b44-154">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="03b44-155">Bir görev bir giriş varlık JobInputAsset veya JobOutputAsset belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03b44-155">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="03b44-156">Görevler bir döngü oluşturmuyor gerekir.</span><span class="sxs-lookup"><span data-stu-id="03b44-156">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="03b44-157">tooJobInputAsset veya JobOutputAsset geçirmek hello değer parametresi bir varlık için hello dizin değerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="03b44-157">hello value parameter that you pass tooJobInputAsset or JobOutputAsset represents hello index value for an asset.</span></span> <span data-ttu-id="03b44-158">Merhaba gerçek varlıklar hello InputMediaAssets ve OutputMediaAssets Gezinti özellikleri hello işi varlık açıklamasında tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="03b44-158">hello actual assets are defined in hello InputMediaAssets and OutputMediaAssets navigation properties on hello job entity definition.</span></span>
* <span data-ttu-id="03b44-159">Media Services üzerinde OData v3 oluşturulduğundan, tek tek varlıkları hello InputMediaAssets hello ve OutputMediaAssets gezinti özelliği koleksiyonlar aracılığıyla başvurulan bir "__metadata: URI" ad-değer çifti.</span><span class="sxs-lookup"><span data-stu-id="03b44-159">Because Media Services is built on OData v3, hello individual assets in hello InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
* <span data-ttu-id="03b44-160">InputMediaAssets tooone veya Media Services ile oluşturulan daha fazla varlıklar eşler.</span><span class="sxs-lookup"><span data-stu-id="03b44-160">InputMediaAssets maps tooone or more assets that you created in Media Services.</span></span> <span data-ttu-id="03b44-161">OutputMediaAssets hello sistem tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="03b44-161">OutputMediaAssets are created by hello system.</span></span> <span data-ttu-id="03b44-162">Bunlar, var olan bir varlık başvurusu yok.</span><span class="sxs-lookup"><span data-stu-id="03b44-162">They don't reference an existing asset.</span></span>
* <span data-ttu-id="03b44-163">Merhaba assetName özniteliğini kullanarak OutputMediaAssets adlandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="03b44-163">OutputMediaAssets can be named by using hello assetName attribute.</span></span> <span data-ttu-id="03b44-164">Bu öznitelik yok sonra hello hello OutputMediaAsset adıdır hello ne olursa olsun hello iç metin değeri <outputAsset> öğesidir hello iş adı değeri veya hello iş kimliği değeri (durumda hello Name özelliği tanımlanmadı burada hello) soneki.</span><span class="sxs-lookup"><span data-stu-id="03b44-164">If this attribute is not present, then hello name of hello OutputMediaAsset is whatever hello inner text value of hello <outputAsset> element is with a suffix of either hello Job Name value, or hello Job Id value (in hello case where hello Name property isn't defined).</span></span> <span data-ttu-id="03b44-165">AssetName için bir değer ayarlarsanız, örneğin, çok "Örnek" sonra hello OutputMediaAsset özelliği ayarlanmış adı çok "Sample."</span><span class="sxs-lookup"><span data-stu-id="03b44-165">For example, if you set a value for assetName too"Sample," then hello OutputMediaAsset Name property is set too"Sample."</span></span> <span data-ttu-id="03b44-166">AssetName için bir değer ayarlamadınız ancak hello iş adı ayarlama ancak, çok "NewJob" sonra hello OutputMediaAsset adı "JobOutputAsset (değer) _NewJob." olacaktır</span><span class="sxs-lookup"><span data-stu-id="03b44-166">However, if you didn't set a value for assetName, but did set hello job name too"NewJob," then hello OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob."</span></span>

## <a name="create-a-job-with-chained-tasks"></a><span data-ttu-id="03b44-167">Bir iş ile zincirleme görevler oluşturma</span><span class="sxs-lookup"><span data-stu-id="03b44-167">Create a job with chained tasks</span></span>
<span data-ttu-id="03b44-168">Birçok uygulama senaryolarında geliştiriciler toocreate bir dizi görevleri işleme istiyor.</span><span class="sxs-lookup"><span data-stu-id="03b44-168">In many application scenarios, developers want toocreate a series of processing tasks.</span></span> <span data-ttu-id="03b44-169">Media Services'de zincirleme görevleri bir dizi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03b44-169">In Media Services, you can create a series of chained tasks.</span></span> <span data-ttu-id="03b44-170">Her görev, farklı işleme adımları gerçekleştirir ve farklı medya işlemcileri kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="03b44-170">Each task performs different processing steps and can use different media processors.</span></span> <span data-ttu-id="03b44-171">Zincirleme hello görevleri bir varlık hello varlık üzerinde doğrusal bir görev dizisini gerçekleştiren bir görev tooanother el.</span><span class="sxs-lookup"><span data-stu-id="03b44-171">hello chained tasks can hand off an asset from one task tooanother, performing a linear sequence of tasks on hello asset.</span></span> <span data-ttu-id="03b44-172">Ancak, bir işi gerçekleştirilen hello görevler bir sırayla gerekli toobe değildir.</span><span class="sxs-lookup"><span data-stu-id="03b44-172">However, hello tasks performed in a job are not required toobe in a sequence.</span></span> <span data-ttu-id="03b44-173">Zincirleme bir görev oluşturduğunuzda, hello zincirleme **ITask** nesneler, tek bir oluşturulur **IJob** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="03b44-173">When you create a chained task, hello chained **ITask** objects are created in a single **IJob** object.</span></span>

> [!NOTE]
> <span data-ttu-id="03b44-174">Şu anda iş başına 30 görevlerin bir sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="03b44-174">There is currently a limit of 30 tasks per job.</span></span> <span data-ttu-id="03b44-175">30'dan fazla görevleri toochain ihtiyacınız varsa, birden fazla iş toocontain hello Görevler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="03b44-175">If you need toochain more than 30 tasks, create more than one job toocontain hello tasks.</span></span>
>
>

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://testrest.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A910ffdc1-2e25-4b17-8a42-61ffd4b8914c')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          },
          {  
             "Configuration":"H264 Smooth Streaming 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-16\"?><taskBody><inputAsset>JobOutputAsset(0)</inputAsset><outputAsset>JobOutputAsset(1)</outputAsset></taskBody>"
          }
       ]
    }


### <a name="considerations"></a><span data-ttu-id="03b44-176">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="03b44-176">Considerations</span></span>
<span data-ttu-id="03b44-177">tooenable görev zincirleme:</span><span class="sxs-lookup"><span data-stu-id="03b44-177">tooenable task chaining:</span></span>

* <span data-ttu-id="03b44-178">Bir işi, en az iki görev olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="03b44-178">A job must have at least two tasks.</span></span>
* <span data-ttu-id="03b44-179">En az bir görev girişi hello hello işteki başka bir görev çıkışıdır olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="03b44-179">There must be at least one task whose input is hello output of another task in hello job.</span></span>

## <a name="use-odata-batch-processing"></a><span data-ttu-id="03b44-180">OData toplu işleme</span><span class="sxs-lookup"><span data-stu-id="03b44-180">Use OData batch processing</span></span>
<span data-ttu-id="03b44-181">Aşağıdaki örnek hello nasıl toouse OData toplu işleme toocreate bir işi ve görevleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="03b44-181">hello following example shows how toouse OData batch processing toocreate a job and tasks.</span></span> <span data-ttu-id="03b44-182">Toplu işleme hakkında daha fazla bilgi için bkz: [açık veri Protokolü (OData) toplu işleme](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="03b44-182">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

    POST https://media.windows.net/api/$batch HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: multipart/mixed; boundary=batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Accept: multipart/mixed
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net


    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Content-Type: multipart/mixed; boundary=changeset_122fb0a4-cd80-4958-820f-346309967e4d

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-ID: 1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {"Name" : "NewTestJob", "InputMediaAssets@odata.bind":["https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A2a22445d-1500-80c6-4b34-f1e5190d33c6')"]}

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/$1/Tasks HTTP/1.1
    Content-ID: 2
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
       "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
       "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"Custom output name\">JobOutputAsset(0)</outputAsset></taskBody>"
    }

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d--
    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e--



## <a name="create-a-job-by-using-a-jobtemplate"></a><span data-ttu-id="03b44-183">Bir JobTemplate kullanarak bir iş oluşturma</span><span class="sxs-lookup"><span data-stu-id="03b44-183">Create a job by using a JobTemplate</span></span>
<span data-ttu-id="03b44-184">Ne zaman birden çok varlığı görevler, bir JobTemplate toospecify hello varsayılan görev hazır ayarları kullanın veya görevlerin tooset hello sırası ortak bir dizi kullanarak işleyin.</span><span class="sxs-lookup"><span data-stu-id="03b44-184">When you process multiple assets by using a common set of tasks, use a JobTemplate toospecify hello default task presets, or tooset hello order of tasks.</span></span>

<span data-ttu-id="03b44-185">Aşağıdaki örnek hello nasıl satır içi toocreate JobTemplate olan bir TaskTemplate ile tanımlanan gösterir.</span><span class="sxs-lookup"><span data-stu-id="03b44-185">hello following example shows how toocreate a JobTemplate with a TaskTemplate that is defined inline.</span></span> <span data-ttu-id="03b44-186">Merhaba TaskTemplate hello Medya Kodlayıcısı standart hello MediaProcessor tooencode hello varlık dosyası olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="03b44-186">hello TaskTemplate uses hello Media Encoder Standard as hello MediaProcessor tooencode hello asset file.</span></span> <span data-ttu-id="03b44-187">Ancak, diğer MediaProcessors de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="03b44-187">However, other MediaProcessors can be used as well.</span></span>

    POST https://media.windows.net/API/JobTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewJobTemplate25", "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H264 Smooth Streaming 720p", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }


> [!NOTE]
> <span data-ttu-id="03b44-188">Diğer Media Services varlıklar farklı olarak, her TaskTemplate için yeni bir GUID tanımlayıcısı tanımlayın ve istek gövdesinde hello taskTemplateId ve ID özelliği yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="03b44-188">Unlike other Media Services entities, you must define a new GUID identifier for each TaskTemplate and place it in hello taskTemplateId and Id property in your request body.</span></span> <span data-ttu-id="03b44-189">Merhaba içerik tanımlama düzeni tanımlamak Azure Media Services varlıklarda tanımlanan hello düzenini izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="03b44-189">hello content identification scheme must follow hello scheme described in Identify Azure Media Services Entities.</span></span> <span data-ttu-id="03b44-190">Ayrıca, JobTemplates güncelleştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="03b44-190">Also, JobTemplates cannot be updated.</span></span> <span data-ttu-id="03b44-191">Bunun yerine, güncelleştirilmiş değişikliklerinizi içeren yeni bir tane oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="03b44-191">Instead, you must create a new one with your updated changes.</span></span>
>
>

<span data-ttu-id="03b44-192">Başarılı olursa, yanıt aşağıdaki hello verilir:</span><span class="sxs-lookup"><span data-stu-id="03b44-192">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .


<span data-ttu-id="03b44-193">örnekte gösterildiği nasıl aşağıdaki hello toocreate JobTemplate kimliği başvuran bir iş:</span><span class="sxs-lookup"><span data-stu-id="03b44-193">hello following example shows how toocreate a job that references a JobTemplate Id:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


<span data-ttu-id="03b44-194">Başarılı olursa, yanıt aşağıdaki hello verilir:</span><span class="sxs-lookup"><span data-stu-id="03b44-194">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a><span data-ttu-id="03b44-195">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="03b44-195">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="03b44-196">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="03b44-196">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="03b44-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="03b44-197">Next steps</span></span>
<span data-ttu-id="03b44-198">Varlık, bir iş tooencode toocreate nasıl görürüm bildiğinize göre [nasıl toocheck iş ilerleme Media Services ile](media-services-rest-check-job-progress.md).</span><span class="sxs-lookup"><span data-stu-id="03b44-198">Now that you know how toocreate a job tooencode an asset, see [How toocheck job progress with Media Services](media-services-rest-check-job-progress.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="03b44-199">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="03b44-199">See also</span></span>
[<span data-ttu-id="03b44-200">Medya işlemcileri Al</span><span class="sxs-lookup"><span data-stu-id="03b44-200">Get Media Processors</span></span>](media-services-rest-get-media-processor.md)
