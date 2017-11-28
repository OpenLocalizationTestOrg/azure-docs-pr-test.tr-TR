---
title: "Hızlı Başlangıç: Azure Machine Learning önerileri API'si (sürüm 1) | Microsoft Docs"
description: "Azure Machine Learning önerileri - Hızlı Başlangıç Kılavuzu"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 5bce1a4a-1ad6-473f-812b-84f800fdc09a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d8f98e85f723a1104cb169b26d797934140979f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-start-guide-for-hello-machine-learning-recommendations-api-version-1"></a><span data-ttu-id="81ae1-104">Merhaba Machine Learning önerileri API'si (sürüm 1) için Hızlı Başlangıç Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="81ae1-104">Quick start guide for hello Machine Learning Recommendations API (version 1)</span></span>

> [!NOTE]
> <span data-ttu-id="81ae1-105">Hello kullanarak başlamalıdır [önerileri API Bilişsel hizmeti](https://www.microsoft.com/cognitive-services/recommendations-api) bu sürümü yerine.</span><span class="sxs-lookup"><span data-stu-id="81ae1-105">You should start using hello [Recommendations API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api) instead of this version.</span></span> <span data-ttu-id="81ae1-106">Merhaba önerileri Bilişsel hizmet bu hizmeti koyacağınız ve tüm hello yeni özellikler vardır geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="81ae1-106">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="81ae1-107">Toplu işlem desteği, daha iyi API'si Gezgini, bir temizleyici API yüzeyi, daha tutarlı kaydolma/faturalandırma deneyimi, vb. gibi yeni özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="81ae1-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
>
> <span data-ttu-id="81ae1-108">Daha fazla bilgi edinmek [geçiş toohello yeni Bilişsel hizmet](http://aka.ms/recomigrate).</span><span class="sxs-lookup"><span data-stu-id="81ae1-108">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate).</span></span>
> 
> 

<span data-ttu-id="81ae1-109">Bu belgede açıklanan nasıl tooonboard, hizmet veya uygulama toouse Microsoft Azure Machine Learning öneriler.</span><span class="sxs-lookup"><span data-stu-id="81ae1-109">This document describes how tooonboard your service or application toouse Microsoft Azure Machine Learning Recommendations.</span></span> <span data-ttu-id="81ae1-110">Merhaba hello önerileri API'si hakkında daha fazla ayrıntı bulabilirsiniz [Cortana Intelligence Galerisi](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span><span class="sxs-lookup"><span data-stu-id="81ae1-110">You can find more details on hello Recommendations API in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a><span data-ttu-id="81ae1-111">Genel bir bakış</span><span class="sxs-lookup"><span data-stu-id="81ae1-111">General overview</span></span>
<span data-ttu-id="81ae1-112">Azure Machine Learning önerileri toouse, aşağıdaki adımları tootake hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="81ae1-112">toouse Azure Machine Learning Recommendations, you need tootake hello following steps:</span></span>

* <span data-ttu-id="81ae1-113">Bir model oluşturma - bir model kullanım verileri, katalog verilerini ve hello öneri modeli, bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="81ae1-113">Create a model - A model is a container of your usage data, catalog data, and hello recommendation model.</span></span>
* <span data-ttu-id="81ae1-114">İçeri aktarma katalog verilerini - katalog hello öğeler üzerinde meta veri bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="81ae1-114">Import catalog data - A catalog contains metadata information on hello items.</span></span> 
* <span data-ttu-id="81ae1-115">İçeri aktarma kullanım verilerini - kullanım verilerini iki yoldan biriyle (veya her ikisi de) yüklenebilir:</span><span class="sxs-lookup"><span data-stu-id="81ae1-115">Import usage data - Usage data can be uploaded in one of two ways (or both):</span></span>
  * <span data-ttu-id="81ae1-116">Merhaba kullanım verilerini içeren bir dosyayı karşıya yükleyerek.</span><span class="sxs-lookup"><span data-stu-id="81ae1-116">By uploading a file that contains hello usage data.</span></span>
  * <span data-ttu-id="81ae1-117">Veri alma olaylarını göndererek.</span><span class="sxs-lookup"><span data-stu-id="81ae1-117">By sending data acquisition events.</span></span>
    <span data-ttu-id="81ae1-118">Genellikle bir sipariş toobe mümkün toocreate (önyükleme) bir ilk öneri modeli kullanım dosyayı karşıya yükleme ve hello veri alım biçimi kullanarak hello sistem yeterli veri toplayan kadar kullanın.</span><span class="sxs-lookup"><span data-stu-id="81ae1-118">Usually you upload a usage file in order toobe able toocreate an initial recommendation model (bootstrap) and use it until hello system gathers enough data by using hello data acquisition format.</span></span>
* <span data-ttu-id="81ae1-119">Bir öneri model oluşturma - bu zaman uyumsuz bir işlemin hangi hello öneri sistem, tüm hello kullanım verileri alır ve bir öneri modeli oluşturur.</span><span class="sxs-lookup"><span data-stu-id="81ae1-119">Build a recommendation model - This is an asynchronous operation in which hello recommendation system takes all hello usage data and creates a recommendation model.</span></span> <span data-ttu-id="81ae1-120">Bu işlem birkaç dakika alabilir veya hello bağlı olarak birkaç saat boyutunu hello veri ve hello yapı yapılandırma parametreleri.</span><span class="sxs-lookup"><span data-stu-id="81ae1-120">This operation can take several minutes or several hours depending on hello size of hello data and hello build configuration parameters.</span></span> <span data-ttu-id="81ae1-121">Merhaba yapı tetiklendiğinde bir yapı kimliği alırsınız</span><span class="sxs-lookup"><span data-stu-id="81ae1-121">When triggering hello build, you will get a build ID.</span></span> <span data-ttu-id="81ae1-122">Tooconsume önerileri başlatmadan önce Hello derleme işlem sona erdiğinde toocheck kullanın.</span><span class="sxs-lookup"><span data-stu-id="81ae1-122">Use it toocheck when hello build process has ended before starting tooconsume recommendations.</span></span>
* <span data-ttu-id="81ae1-123">Öneriler - Get önerileri belirli öğesi veya öğeleri listesi için kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="81ae1-123">Consume recommendations - Get recommendations for a specific item or list of items.</span></span>

<span data-ttu-id="81ae1-124">Yukarıdaki tüm hello adımları hello Azure Machine Learning önerileri API'si yapılır.</span><span class="sxs-lookup"><span data-stu-id="81ae1-124">All hello steps above are done through hello Azure Machine Learning Recommendations API.</span></span>  <span data-ttu-id="81ae1-125">Merhaba öğesinden bu adımların her biri uygulayan bir örnek uygulama indirebilirsiniz [de Galerisi.](http://1drv.ms/1xeO2F3)</span><span class="sxs-lookup"><span data-stu-id="81ae1-125">You can download a sample application that implements each of these steps from hello [gallery as well.](http://1drv.ms/1xeO2F3)</span></span>

## <a name="limitations"></a><span data-ttu-id="81ae1-126">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="81ae1-126">Limitations</span></span>
* <span data-ttu-id="81ae1-127">Merhaba en büyük abonelik başına model sayısı 10'dur.</span><span class="sxs-lookup"><span data-stu-id="81ae1-127">hello maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="81ae1-128">Merhaba en fazla bir katalog tutabilir öğe sayısı 100. 000 ' dir.</span><span class="sxs-lookup"><span data-stu-id="81ae1-128">hello maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="81ae1-129">Merhaba maksimum tutulur kullanım noktaları ~ 5,000,000 sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="81ae1-129">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="81ae1-130">Yeni bir tane karşıya bildirilen veya gereken hello eski silinir.</span><span class="sxs-lookup"><span data-stu-id="81ae1-130">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="81ae1-131">Merhaba en büyük boyutu (örneğin, veri içeri aktar katalog kullanım verileri İçeri Aktar) POSTASINA gönderilen veri 200 MB'tır.</span><span class="sxs-lookup"><span data-stu-id="81ae1-131">hello maximum size of data that can be sent in POST (for example, import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="81ae1-132">Merhaba işlem etkin olmadığından bir öneri modeli derlemesi için saniye başına sayısı olan ~ 2TPS.</span><span class="sxs-lookup"><span data-stu-id="81ae1-132">hello number of transactions per second for a recommendation model build that is not active is ~2TPS.</span></span> <span data-ttu-id="81ae1-133">Etkin bir öneri modeli yapı too20TPS basılı tutabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81ae1-133">A recommendation model build that is active can hold up too20TPS.</span></span>

## <a name="integration"></a><span data-ttu-id="81ae1-134">Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="81ae1-134">Integration</span></span>
### <a name="authentication"></a><span data-ttu-id="81ae1-135">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="81ae1-135">Authentication</span></span>
<span data-ttu-id="81ae1-136">Microsoft Azure Market ya da hello temel veya OAuth kimlik doğrulama yöntemini destekler.</span><span class="sxs-lookup"><span data-stu-id="81ae1-136">Microsoft Azure Marketplace supports either hello Basic or OAuth authentication method.</span></span> <span data-ttu-id="81ae1-137">Merhaba Market altında toohello anahtarlarında giderek hello hesabı anahtarları kolayca bulabilirsiniz [hesap ayarlarınızı](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="81ae1-137">You can easily find hello account keys by navigating toohello keys in hello marketplace under [your account settings](https://datamarket.azure.com/account/keys).</span></span> 

#### <a name="basic-authentication"></a><span data-ttu-id="81ae1-138">Temel kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="81ae1-138">Basic Authentication</span></span>
<span data-ttu-id="81ae1-139">Merhaba Authorization Üstbilgisi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="81ae1-139">Add hello Authorization header:</span></span>

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

<span data-ttu-id="81ae1-140">TooBase64 dönüştürme (C#)</span><span class="sxs-lookup"><span data-stu-id="81ae1-140">Convert tooBase64 (C#)</span></span>

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

<span data-ttu-id="81ae1-141">TooBase64 dönüştürme (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="81ae1-141">Convert tooBase64 (JavaScript)</span></span>

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a><span data-ttu-id="81ae1-142">Hizmet URI'si</span><span class="sxs-lookup"><span data-stu-id="81ae1-142">Service URI</span></span>
<span data-ttu-id="81ae1-143">hello Azure Machine Learning önerileri API'leri için Hello hizmet kök URI [burada.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span><span class="sxs-lookup"><span data-stu-id="81ae1-143">hello service root URI for hello Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span></span>

<span data-ttu-id="81ae1-144">Merhaba tam hizmet URI'si hello OData belirtimi öğeleri kullanılarak ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="81ae1-144">hello full service URI is expressed using elements of hello OData specification.</span></span>

### <a name="api-version"></a><span data-ttu-id="81ae1-145">API sürümü</span><span class="sxs-lookup"><span data-stu-id="81ae1-145">API version</span></span>
<span data-ttu-id="81ae1-146">Her API çağrısı, hello sonunda ayarlanmalıdır apiVersion adlı bir sorgu parametresi sahip olur "1.0" çok.</span><span class="sxs-lookup"><span data-stu-id="81ae1-146">Each API call will have, at hello end, a query parameter called apiVersion that should be set too"1.0".</span></span>

### <a name="ids-are-case-sensitive"></a><span data-ttu-id="81ae1-147">Kimlikleri büyük/küçük harfe duyarlıdır</span><span class="sxs-lookup"><span data-stu-id="81ae1-147">IDs are case-sensitive</span></span>
<span data-ttu-id="81ae1-148">Herhangi bir hello API ' ları tarafından döndürülen kimlikleri, büyük küçük harfe duyarlıdır ve bu nedenle sonraki API çağrıları parametre olarak geçirilen kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="81ae1-148">IDs, returned by any of hello APIs, are case-sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="81ae1-149">Örneğin, model kimlikleri ve Katalog büyük küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="81ae1-149">For instance, model IDs and catalog IDs are case-sensitive.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="81ae1-150">Bir model oluşturma</span><span class="sxs-lookup"><span data-stu-id="81ae1-150">Create a model</span></span>
<span data-ttu-id="81ae1-151">"Model oluşturma" isteği oluşturma:</span><span class="sxs-lookup"><span data-stu-id="81ae1-151">Creating a "create model" request:</span></span>

| <span data-ttu-id="81ae1-152">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="81ae1-152">HTTP Method</span></span> | <span data-ttu-id="81ae1-153">URI</span><span class="sxs-lookup"><span data-stu-id="81ae1-153">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="81ae1-154">YAYINLA</span><span class="sxs-lookup"><span data-stu-id="81ae1-154">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="81ae1-155">Örnek:</span><span class="sxs-lookup"><span data-stu-id="81ae1-155">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="81ae1-156">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="81ae1-156">Parameter Name</span></span> | <span data-ttu-id="81ae1-157">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="81ae1-157">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="81ae1-158">modelName</span><span class="sxs-lookup"><span data-stu-id="81ae1-158">modelName</span></span> |<span data-ttu-id="81ae1-159">Yalnızca harf (A-Z, a-z), sayılar (0-9), tireler (-) ve alt çizgi (_).</span><span class="sxs-lookup"><span data-stu-id="81ae1-159">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="81ae1-160">En fazla uzunluk: 20</span><span class="sxs-lookup"><span data-stu-id="81ae1-160">Max length: 20</span></span> |
| <span data-ttu-id="81ae1-161">apiVersion</span><span class="sxs-lookup"><span data-stu-id="81ae1-161">apiVersion</span></span> |<span data-ttu-id="81ae1-162">1.0</span><span class="sxs-lookup"><span data-stu-id="81ae1-162">1.0</span></span> |
|  | |
| <span data-ttu-id="81ae1-163">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="81ae1-163">Request Body</span></span> |<span data-ttu-id="81ae1-164">YOK</span><span class="sxs-lookup"><span data-stu-id="81ae1-164">NONE</span></span> |

<span data-ttu-id="81ae1-165">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="81ae1-165">**Response**:</span></span>

<span data-ttu-id="81ae1-166">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="81ae1-166">HTTP Status code: 200</span></span>

* <span data-ttu-id="81ae1-167">`feed/entry/content/properties/id`-Hello model kimliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="81ae1-167">`feed/entry/content/properties/id` - Contains hello model ID.</span></span>
  <span data-ttu-id="81ae1-168">Merhaba model kimliği büyük küçük harfe duyarlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="81ae1-168">Note that hello model ID is case-sensitive.</span></span>

<span data-ttu-id="81ae1-169">OData XML</span><span class="sxs-lookup"><span data-stu-id="81ae1-169">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">a658c626-2baa-43a7-ac98-f6ee26120a12</d:Id>
        <d:Name m:type="Edm.String">MyFirstModel</d:Name>
        <d:Date m:type="Edm.String">10/5/2014 6:35:19 AM</d:Date>
        <d:Status m:type="Edm.String">Created</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:UserName>
        <d:Description m:type="Edm.String"></d:Description>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-catalog-data"></a><span data-ttu-id="81ae1-170">Katalog verilerini al</span><span class="sxs-lookup"><span data-stu-id="81ae1-170">Import catalog data</span></span>
<span data-ttu-id="81ae1-171">Aynı model birkaç katalog dosyaları toohello birkaç çağrılarla yüklerseniz, biz yalnızca hello yeni katalog öğeleri ekler.</span><span class="sxs-lookup"><span data-stu-id="81ae1-171">If you upload several catalog files toohello same model with several calls, we will insert only hello new catalog items.</span></span> <span data-ttu-id="81ae1-172">Varolan öğeleri hello özgün değerleriyle kalır.</span><span class="sxs-lookup"><span data-stu-id="81ae1-172">Existing items will remain with hello original values.</span></span>

| <span data-ttu-id="81ae1-173">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="81ae1-173">HTTP Method</span></span> | <span data-ttu-id="81ae1-174">URI</span><span class="sxs-lookup"><span data-stu-id="81ae1-174">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="81ae1-175">YAYINLA</span><span class="sxs-lookup"><span data-stu-id="81ae1-175">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="81ae1-176">Örnek:</span><span class="sxs-lookup"><span data-stu-id="81ae1-176">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="81ae1-177">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="81ae1-177">Parameter Name</span></span> | <span data-ttu-id="81ae1-178">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="81ae1-178">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="81ae1-179">modelId</span><span class="sxs-lookup"><span data-stu-id="81ae1-179">modelId</span></span> |<span data-ttu-id="81ae1-180">Benzersiz tanımlayıcı hello modelinin (büyük küçük harfe duyarlı)</span><span class="sxs-lookup"><span data-stu-id="81ae1-180">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="81ae1-181">Dosya adı</span><span class="sxs-lookup"><span data-stu-id="81ae1-181">filename</span></span> |<span data-ttu-id="81ae1-182">Başlangıç kataloğu metinsel tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="81ae1-182">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="81ae1-183">Yalnızca harf (A-Z, a-z), sayılar (0-9), tireler (-) ve alt çizgi (_).</span><span class="sxs-lookup"><span data-stu-id="81ae1-183">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="81ae1-184">En fazla uzunluk: 50</span><span class="sxs-lookup"><span data-stu-id="81ae1-184">Max length: 50</span></span> |
| <span data-ttu-id="81ae1-185">apiVersion</span><span class="sxs-lookup"><span data-stu-id="81ae1-185">apiVersion</span></span> |<span data-ttu-id="81ae1-186">1.0</span><span class="sxs-lookup"><span data-stu-id="81ae1-186">1.0</span></span> |
|  | |
| <span data-ttu-id="81ae1-187">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="81ae1-187">Request Body</span></span> |<span data-ttu-id="81ae1-188">Veri Kataloğu.</span><span class="sxs-lookup"><span data-stu-id="81ae1-188">Catalog data.</span></span> <span data-ttu-id="81ae1-189">Biçimi:</span><span class="sxs-lookup"><span data-stu-id="81ae1-189">Format:</span></span><br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th><span data-ttu-id="81ae1-190">Ad</span><span class="sxs-lookup"><span data-stu-id="81ae1-190">Name</span></span></th><th><span data-ttu-id="81ae1-191">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="81ae1-191">Mandatory</span></span></th><th><span data-ttu-id="81ae1-192">Tür</span><span class="sxs-lookup"><span data-stu-id="81ae1-192">Type</span></span></th><th><span data-ttu-id="81ae1-193">Açıklama</span><span class="sxs-lookup"><span data-stu-id="81ae1-193">Description</span></span></th></tr><tr><td><span data-ttu-id="81ae1-194">Öğe kimliği</span><span class="sxs-lookup"><span data-stu-id="81ae1-194">Item Id</span></span></td><td><span data-ttu-id="81ae1-195">Evet</span><span class="sxs-lookup"><span data-stu-id="81ae1-195">Yes</span></span></td><td><span data-ttu-id="81ae1-196">Alfasayısal, en fazla uzunluğu 50</span><span class="sxs-lookup"><span data-stu-id="81ae1-196">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="81ae1-197">Bir öğeyi benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="81ae1-197">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="81ae1-198">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="81ae1-198">Item Name</span></span></td><td><span data-ttu-id="81ae1-199">Evet</span><span class="sxs-lookup"><span data-stu-id="81ae1-199">Yes</span></span></td><td><span data-ttu-id="81ae1-200">Alfasayısal, en fazla uzunluğu 255</span><span class="sxs-lookup"><span data-stu-id="81ae1-200">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="81ae1-201">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="81ae1-201">Item name</span></span></td></tr><tr><td><span data-ttu-id="81ae1-202">Öğesi kategorisi</span><span class="sxs-lookup"><span data-stu-id="81ae1-202">Item Category</span></span></td><td><span data-ttu-id="81ae1-203">Evet</span><span class="sxs-lookup"><span data-stu-id="81ae1-203">Yes</span></span></td><td><span data-ttu-id="81ae1-204">Alfasayısal, en fazla uzunluğu 255</span><span class="sxs-lookup"><span data-stu-id="81ae1-204">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="81ae1-205">Bu öğe (örneğin, pişirme Books ekranda...) ait olduğu kategoriyi toowhich</span><span class="sxs-lookup"><span data-stu-id="81ae1-205">Category toowhich this item belongs (for example, Cooking Books, Drama…)</span></span></td></tr><tr><td><span data-ttu-id="81ae1-206">Açıklama</span><span class="sxs-lookup"><span data-stu-id="81ae1-206">Description</span></span></td><td><span data-ttu-id="81ae1-207">Hayır</span><span class="sxs-lookup"><span data-stu-id="81ae1-207">No</span></span></td><td><span data-ttu-id="81ae1-208">Alfasayısal, en fazla uzunluğu 4000</span><span class="sxs-lookup"><span data-stu-id="81ae1-208">Alphanumeric, max length 4000</span></span></td><td><span data-ttu-id="81ae1-209">Bu öğenin açıklaması</span><span class="sxs-lookup"><span data-stu-id="81ae1-209">Description of this item</span></span></td></tr></table><br><span data-ttu-id="81ae1-210">En büyük dosya boyutu 200 MB'tır.</span><span class="sxs-lookup"><span data-stu-id="81ae1-210">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="81ae1-211">Örnek:</span><span class="sxs-lookup"><span data-stu-id="81ae1-211">Example:</span></span><br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

<span data-ttu-id="81ae1-212">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="81ae1-212">**Response**:</span></span>

<span data-ttu-id="81ae1-213">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="81ae1-213">HTTP Status code: 200</span></span>

* <span data-ttu-id="81ae1-214">`Feed\entry\content\properties\LineCount`-Kabul satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="81ae1-214">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="81ae1-215">`Feed\entry\content\properties\ErrorCount`-Tooan hata eklenmemiş satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="81ae1-215">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>

<span data-ttu-id="81ae1-216">OData XML</span><span class="sxs-lookup"><span data-stu-id="81ae1-216">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
          <subtitle type="text">Import catalog file</subtitle>
          <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:58:04Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">ImportCatalogFileEntity2</title>
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">4</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-usage-data"></a><span data-ttu-id="81ae1-217">Kullanım verilerini alma</span><span class="sxs-lookup"><span data-stu-id="81ae1-217">Import usage data</span></span>
#### <a name="uploading-a-file"></a><span data-ttu-id="81ae1-218">Bir dosyayı karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="81ae1-218">Uploading a file</span></span>
<span data-ttu-id="81ae1-219">Bu bölümde gösterilmiştir nasıl dosyası kullanarak tooupload kullanım verileri.</span><span class="sxs-lookup"><span data-stu-id="81ae1-219">This section shows how tooupload usage data by using a file.</span></span> <span data-ttu-id="81ae1-220">Bu API birkaç kez ile kullanım verilerini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81ae1-220">You can call this API several times with usage data.</span></span> <span data-ttu-id="81ae1-221">Tüm kullanım verileri tüm çağrıları için kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="81ae1-221">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="81ae1-222">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="81ae1-222">HTTP Method</span></span> | <span data-ttu-id="81ae1-223">URI</span><span class="sxs-lookup"><span data-stu-id="81ae1-223">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="81ae1-224">YAYINLA</span><span class="sxs-lookup"><span data-stu-id="81ae1-224">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="81ae1-225">Örnek:</span><span class="sxs-lookup"><span data-stu-id="81ae1-225">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="81ae1-226">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="81ae1-226">Parameter Name</span></span> | <span data-ttu-id="81ae1-227">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="81ae1-227">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="81ae1-228">modelId</span><span class="sxs-lookup"><span data-stu-id="81ae1-228">modelId</span></span> |<span data-ttu-id="81ae1-229">Benzersiz tanımlayıcı hello modelinin (büyük küçük harfe duyarlı)</span><span class="sxs-lookup"><span data-stu-id="81ae1-229">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="81ae1-230">Dosya adı</span><span class="sxs-lookup"><span data-stu-id="81ae1-230">filename</span></span> |<span data-ttu-id="81ae1-231">Başlangıç kataloğu metinsel tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="81ae1-231">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="81ae1-232">Yalnızca harf (A-Z, a-z), sayılar (0-9), tireler (-) ve alt çizgi (_).</span><span class="sxs-lookup"><span data-stu-id="81ae1-232">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="81ae1-233">En fazla uzunluk: 50</span><span class="sxs-lookup"><span data-stu-id="81ae1-233">Max length: 50</span></span> |
| <span data-ttu-id="81ae1-234">apiVersion</span><span class="sxs-lookup"><span data-stu-id="81ae1-234">apiVersion</span></span> |<span data-ttu-id="81ae1-235">1.0</span><span class="sxs-lookup"><span data-stu-id="81ae1-235">1.0</span></span> |
|  | |
| <span data-ttu-id="81ae1-236">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="81ae1-236">Request Body</span></span> |<span data-ttu-id="81ae1-237">Kullanım verileri.</span><span class="sxs-lookup"><span data-stu-id="81ae1-237">Usage data.</span></span> <span data-ttu-id="81ae1-238">Biçimi:</span><span class="sxs-lookup"><span data-stu-id="81ae1-238">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="81ae1-239">Ad</span><span class="sxs-lookup"><span data-stu-id="81ae1-239">Name</span></span></th><th><span data-ttu-id="81ae1-240">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="81ae1-240">Mandatory</span></span></th><th><span data-ttu-id="81ae1-241">Tür</span><span class="sxs-lookup"><span data-stu-id="81ae1-241">Type</span></span></th><th><span data-ttu-id="81ae1-242">Açıklama</span><span class="sxs-lookup"><span data-stu-id="81ae1-242">Description</span></span></th></tr><tr><td><span data-ttu-id="81ae1-243">Kullanıcı Kimliği</span><span class="sxs-lookup"><span data-stu-id="81ae1-243">User Id</span></span></td><td><span data-ttu-id="81ae1-244">Evet</span><span class="sxs-lookup"><span data-stu-id="81ae1-244">Yes</span></span></td><td><span data-ttu-id="81ae1-245">Alfasayısal</span><span class="sxs-lookup"><span data-stu-id="81ae1-245">Alphanumeric</span></span></td><td><span data-ttu-id="81ae1-246">Bir kullanıcının benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="81ae1-246">Unique identifier of a user</span></span></td></tr><tr><td><span data-ttu-id="81ae1-247">Öğe kimliği</span><span class="sxs-lookup"><span data-stu-id="81ae1-247">Item Id</span></span></td><td><span data-ttu-id="81ae1-248">Evet</span><span class="sxs-lookup"><span data-stu-id="81ae1-248">Yes</span></span></td><td><span data-ttu-id="81ae1-249">Alfasayısal, en fazla uzunluğu 50</span><span class="sxs-lookup"><span data-stu-id="81ae1-249">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="81ae1-250">Bir öğeyi benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="81ae1-250">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="81ae1-251">Zaman</span><span class="sxs-lookup"><span data-stu-id="81ae1-251">Time</span></span></td><td><span data-ttu-id="81ae1-252">Hayır</span><span class="sxs-lookup"><span data-stu-id="81ae1-252">No</span></span></td><td><span data-ttu-id="81ae1-253">Tarih biçiminde: YYYY/AA/ddTHH (örneğin, 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="81ae1-253">Date in format: YYYY/MM/DDTHH:MM:SS (for example, 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="81ae1-254">Veri saati</span><span class="sxs-lookup"><span data-stu-id="81ae1-254">Time of data</span></span></td></tr><tr><td><span data-ttu-id="81ae1-255">Olay</span><span class="sxs-lookup"><span data-stu-id="81ae1-255">Event</span></span></td><td><span data-ttu-id="81ae1-256">Sağlanan daha sonra tarih de konulmalıdır yok</span><span class="sxs-lookup"><span data-stu-id="81ae1-256">No, if supplied then must also put date</span></span></td><td><span data-ttu-id="81ae1-257">Merhaba aşağıdakilerden biri:</span><span class="sxs-lookup"><span data-stu-id="81ae1-257">One of hello following:</span></span><br><span data-ttu-id="81ae1-258">• Tıklatın</span><span class="sxs-lookup"><span data-stu-id="81ae1-258">• Click</span></span><br><span data-ttu-id="81ae1-259">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="81ae1-259">• RecommendationClick</span></span><br><span data-ttu-id="81ae1-260">• AddShopCart</span><span class="sxs-lookup"><span data-stu-id="81ae1-260">•    AddShopCart</span></span><br><span data-ttu-id="81ae1-261">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="81ae1-261">• RemoveShopCart</span></span><br><span data-ttu-id="81ae1-262">• Satın alma</span><span class="sxs-lookup"><span data-stu-id="81ae1-262">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="81ae1-263">En büyük dosya boyutu 200 MB'tır.</span><span class="sxs-lookup"><span data-stu-id="81ae1-263">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="81ae1-264">Örnek:</span><span class="sxs-lookup"><span data-stu-id="81ae1-264">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="81ae1-265">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="81ae1-265">**Response**:</span></span>

<span data-ttu-id="81ae1-266">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="81ae1-266">HTTP Status code: 200</span></span>

* <span data-ttu-id="81ae1-267">`Feed\entry\content\properties\LineCount`-Kabul satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="81ae1-267">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="81ae1-268">`Feed\entry\content\properties\ErrorCount`-Tooan hata eklenmemiş satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="81ae1-268">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>
* <span data-ttu-id="81ae1-269">`Feed\entry\content\properties\FileId`-Dosya tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="81ae1-269">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="81ae1-270">OData XML</span><span class="sxs-lookup"><span data-stu-id="81ae1-270">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="using-data-acquisition"></a><span data-ttu-id="81ae1-271">Veri alma kullanma</span><span class="sxs-lookup"><span data-stu-id="81ae1-271">Using data acquisition</span></span>
<span data-ttu-id="81ae1-272">Bu bölüm, gerçek toosend olayları tooAzure Machine Learning önerileri, genellikle Web sitenizi nasıl zaman gösterir.</span><span class="sxs-lookup"><span data-stu-id="81ae1-272">This section shows how toosend events in real time tooAzure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="81ae1-273">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="81ae1-273">HTTP Method</span></span> | <span data-ttu-id="81ae1-274">URI</span><span class="sxs-lookup"><span data-stu-id="81ae1-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="81ae1-275">YAYINLA</span><span class="sxs-lookup"><span data-stu-id="81ae1-275">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="81ae1-276">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="81ae1-276">Parameter Name</span></span> | <span data-ttu-id="81ae1-277">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="81ae1-277">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="81ae1-278">apiVersion</span><span class="sxs-lookup"><span data-stu-id="81ae1-278">apiVersion</span></span> |<span data-ttu-id="81ae1-279">1.0</span><span class="sxs-lookup"><span data-stu-id="81ae1-279">1.0</span></span> |
|  | |
| <span data-ttu-id="81ae1-280">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="81ae1-280">Request body</span></span> |<span data-ttu-id="81ae1-281">Olay veri girişi toosend istediğiniz her olay için.</span><span class="sxs-lookup"><span data-stu-id="81ae1-281">Event data entry for each event you want toosend.</span></span> <span data-ttu-id="81ae1-282">Merhaba aynı kullanıcı veya tarayıcı oturumunu hello için aynı kimliği hello SessionID alanında göndermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="81ae1-282">You should send for hello same user or browser session hello same ID in hello SessionId field.</span></span> <span data-ttu-id="81ae1-283">(Olay gövdesi aşağıdaki örneği bakın.)</span><span class="sxs-lookup"><span data-stu-id="81ae1-283">(See sample of event body below.)</span></span> |

* <span data-ttu-id="81ae1-284">Olay 'Tıklatın' Örneğin:</span><span class="sxs-lookup"><span data-stu-id="81ae1-284">Example for event 'Click':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
        <Name>Click</Name>
        <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="81ae1-285">Olay 'RecommendationClick' Örneğin:</span><span class="sxs-lookup"><span data-stu-id="81ae1-285">Example for event 'RecommendationClick':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RecommendationClick</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="81ae1-286">Olay 'AddShopCart' Örneğin:</span><span class="sxs-lookup"><span data-stu-id="81ae1-286">Example for event 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="81ae1-287">Olay 'RemoveShopCart' Örneğin:</span><span class="sxs-lookup"><span data-stu-id="81ae1-287">Example for event 'RemoveShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RemoveShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="81ae1-288">Olay 'Satınalma' Örneğin:</span><span class="sxs-lookup"><span data-stu-id="81ae1-288">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
            <Name>Purchase</Name> 
            <PurchaseItems>
            <PurchaseItems>
                <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                <Count>3</Count>
            </PurchaseItems>
        </PurchaseItems>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="81ae1-289">Örnek 2 olayları, 'Düğmesini tıklatarak' ve 'AddShopCart' gönderme:</span><span class="sxs-lookup"><span data-stu-id="81ae1-289">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>Click</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
          <ItemName>itemName</ItemName>
          <ItemDescription>item description</ItemDescription>
          <ItemCategory>category</ItemCategory>
        </EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>552A1940-21E4-4399-82BB-594B46D7ED54</ItemId>
        </EventData>
          </EventData>
        </Event>

<span data-ttu-id="81ae1-290">**Yanıt**: HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="81ae1-290">**Response**: HTTP Status code: 200</span></span>

### <a name="build-a-recommendation-model"></a><span data-ttu-id="81ae1-291">Bir öneri model oluşturma</span><span class="sxs-lookup"><span data-stu-id="81ae1-291">Build a recommendation model</span></span>
| <span data-ttu-id="81ae1-292">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="81ae1-292">HTTP Method</span></span> | <span data-ttu-id="81ae1-293">URI</span><span class="sxs-lookup"><span data-stu-id="81ae1-293">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="81ae1-294">YAYINLA</span><span class="sxs-lookup"><span data-stu-id="81ae1-294">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="81ae1-295">Örnek:</span><span class="sxs-lookup"><span data-stu-id="81ae1-295">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| <span data-ttu-id="81ae1-296">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="81ae1-296">Parameter Name</span></span> | <span data-ttu-id="81ae1-297">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="81ae1-297">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="81ae1-298">modelId</span><span class="sxs-lookup"><span data-stu-id="81ae1-298">modelId</span></span> |<span data-ttu-id="81ae1-299">Benzersiz tanımlayıcı hello modelinin (büyük küçük harfe duyarlı)</span><span class="sxs-lookup"><span data-stu-id="81ae1-299">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="81ae1-300">userDescription</span><span class="sxs-lookup"><span data-stu-id="81ae1-300">userDescription</span></span> |<span data-ttu-id="81ae1-301">Başlangıç kataloğu metinsel tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="81ae1-301">Textual identifier of hello catalog.</span></span> <span data-ttu-id="81ae1-302">Boşluklar kullanırsanız, % 20 yerine kodlamak gerekir olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="81ae1-302">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="81ae1-303">Yukarıdaki örnekte bkz.</span><span class="sxs-lookup"><span data-stu-id="81ae1-303">See example above.</span></span><br><span data-ttu-id="81ae1-304">En fazla uzunluk: 50</span><span class="sxs-lookup"><span data-stu-id="81ae1-304">Max length: 50</span></span> |
| <span data-ttu-id="81ae1-305">apiVersion</span><span class="sxs-lookup"><span data-stu-id="81ae1-305">apiVersion</span></span> |<span data-ttu-id="81ae1-306">1.0</span><span class="sxs-lookup"><span data-stu-id="81ae1-306">1.0</span></span> |
|  | |
| <span data-ttu-id="81ae1-307">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="81ae1-307">Request Body</span></span> |<span data-ttu-id="81ae1-308">YOK</span><span class="sxs-lookup"><span data-stu-id="81ae1-308">NONE</span></span> |

<span data-ttu-id="81ae1-309">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="81ae1-309">**Response**:</span></span>

<span data-ttu-id="81ae1-310">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="81ae1-310">HTTP Status code: 200</span></span>

<span data-ttu-id="81ae1-311">Bu zaman uyumsuz bir API'dir.</span><span class="sxs-lookup"><span data-stu-id="81ae1-311">This is an asynchronous API.</span></span> <span data-ttu-id="81ae1-312">Yanıt olarak bir yapı kimliği alırsınız.</span><span class="sxs-lookup"><span data-stu-id="81ae1-312">You will get a build ID as a response.</span></span> <span data-ttu-id="81ae1-313">Merhaba derleme sona erdiğinde tooknow hello "Get derlemeler durumu bir modelin" API çağrısı ve gerekir bulun hello yanıtta bu derleme kimliği.</span><span class="sxs-lookup"><span data-stu-id="81ae1-313">tooknow when hello build has ended, you should call hello "Get Builds Status of a Model" API and locate this build ID in hello response.</span></span> <span data-ttu-id="81ae1-314">Bir yapı dakika toohours hello hello verilerin boyutuna bağlı olarak gelen alabileceğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="81ae1-314">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="81ae1-315">Merhaba yapı kadar sona erer önerileri kullanamayacaklarını.</span><span class="sxs-lookup"><span data-stu-id="81ae1-315">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="81ae1-316">Geçerli yapı durumu:</span><span class="sxs-lookup"><span data-stu-id="81ae1-316">Valid build status:</span></span>

* <span data-ttu-id="81ae1-317">Oluştur – modeli oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="81ae1-317">Create – Model was created.</span></span>
* <span data-ttu-id="81ae1-318">Sıraya – modeli yapı tetiklendi ve kuyruğa alınır.</span><span class="sxs-lookup"><span data-stu-id="81ae1-318">Queued – Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="81ae1-319">Yapı – modeli oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="81ae1-319">Building – Model is being built.</span></span>
* <span data-ttu-id="81ae1-320">Başarılı – yapı başarılı bir şekilde sona erdi.</span><span class="sxs-lookup"><span data-stu-id="81ae1-320">Success – Build ended successfully.</span></span>
* <span data-ttu-id="81ae1-321">Hata – derleme bir hata ile sona erdi.</span><span class="sxs-lookup"><span data-stu-id="81ae1-321">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="81ae1-322">İptal – derleme iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="81ae1-322">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="81ae1-323">İptal etme – yapı iptal edilir.</span><span class="sxs-lookup"><span data-stu-id="81ae1-323">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="81ae1-324">Kimliği yolu izleyerek hello altında bulunabilir bu hello yapı dikkat edin:`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="81ae1-324">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="81ae1-325">OData XML</span><span class="sxs-lookup"><span data-stu-id="81ae1-325">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="get-build-status-of-a-model"></a><span data-ttu-id="81ae1-326">Bir modelin yapı durumunu Al</span><span class="sxs-lookup"><span data-stu-id="81ae1-326">Get build status of a model</span></span>
| <span data-ttu-id="81ae1-327">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="81ae1-327">HTTP Method</span></span> | <span data-ttu-id="81ae1-328">URI</span><span class="sxs-lookup"><span data-stu-id="81ae1-328">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="81ae1-329">AL</span><span class="sxs-lookup"><span data-stu-id="81ae1-329">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="81ae1-330">Örnek:</span><span class="sxs-lookup"><span data-stu-id="81ae1-330">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="81ae1-331">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="81ae1-331">Parameter Name</span></span> | <span data-ttu-id="81ae1-332">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="81ae1-332">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="81ae1-333">modelId</span><span class="sxs-lookup"><span data-stu-id="81ae1-333">modelId</span></span> |<span data-ttu-id="81ae1-334">Benzersiz tanımlayıcı hello modelinin (büyük küçük harfe duyarlı)</span><span class="sxs-lookup"><span data-stu-id="81ae1-334">Unique identifier of hello model  (case-sensitive)</span></span> |
| <span data-ttu-id="81ae1-335">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="81ae1-335">onlyLastBuild</span></span> |<span data-ttu-id="81ae1-336">Gösteren tüm hello tooreturn hello modeli geçmişini ya da hello en son yapı yalnızca hello durumunu derleme.</span><span class="sxs-lookup"><span data-stu-id="81ae1-336">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build.</span></span> |
| <span data-ttu-id="81ae1-337">apiVersion</span><span class="sxs-lookup"><span data-stu-id="81ae1-337">apiVersion</span></span> |<span data-ttu-id="81ae1-338">1.0</span><span class="sxs-lookup"><span data-stu-id="81ae1-338">1.0</span></span> |

<span data-ttu-id="81ae1-339">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="81ae1-339">**Response**:</span></span>

<span data-ttu-id="81ae1-340">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="81ae1-340">HTTP Status code: 200</span></span>

<span data-ttu-id="81ae1-341">Merhaba yanıt yapı her bir giriş içerir.</span><span class="sxs-lookup"><span data-stu-id="81ae1-341">hello response includes one entry per build.</span></span> <span data-ttu-id="81ae1-342">Her giriş verileri aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="81ae1-342">Each entry has hello following data:</span></span>

* <span data-ttu-id="81ae1-343">`feed/entry/content/properties/UserName`– Hello kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="81ae1-343">`feed/entry/content/properties/UserName` – Name of hello user.</span></span>
* <span data-ttu-id="81ae1-344">`feed/entry/content/properties/ModelName`– Hello model adı.</span><span class="sxs-lookup"><span data-stu-id="81ae1-344">`feed/entry/content/properties/ModelName` – Name of hello model.</span></span>
* <span data-ttu-id="81ae1-345">`feed/entry/content/properties/ModelId`– Model benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="81ae1-345">`feed/entry/content/properties/ModelId` – Model unique identifier.</span></span>
* <span data-ttu-id="81ae1-346">`feed/entry/content/properties/IsDeployed`– Merhaba yapı (paketini dağıtılan olup olmadığı</span><span class="sxs-lookup"><span data-stu-id="81ae1-346">`feed/entry/content/properties/IsDeployed` – Whether hello build is deployed (a.k.a.</span></span> <span data-ttu-id="81ae1-347">Etkin yapı).</span><span class="sxs-lookup"><span data-stu-id="81ae1-347">active build).</span></span>
* <span data-ttu-id="81ae1-348">`feed/entry/content/properties/BuildId`– Benzersiz tanımlayıcısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="81ae1-348">`feed/entry/content/properties/BuildId` – Build unique identifier.</span></span>
* <span data-ttu-id="81ae1-349">`feed/entry/content/properties/BuildType`-Hello yapı türü.</span><span class="sxs-lookup"><span data-stu-id="81ae1-349">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="81ae1-350">`feed/entry/content/properties/Status`– Oluşturma durumu.</span><span class="sxs-lookup"><span data-stu-id="81ae1-350">`feed/entry/content/properties/Status` – Build status.</span></span> <span data-ttu-id="81ae1-351">Merhaba aşağıdakilerden biri olabilir: hata, yapı, sıraya alınan, iptal etme, iptal edildi, başarılı</span><span class="sxs-lookup"><span data-stu-id="81ae1-351">Can be one of hello following: Error, Building, Queued, Canceling, Canceled, Success</span></span>
* <span data-ttu-id="81ae1-352">`feed/entry/content/properties/StatusMessage`– Ayrıntılı durum iletisi (yalnızca toospecific durumlar geçerlidir).</span><span class="sxs-lookup"><span data-stu-id="81ae1-352">`feed/entry/content/properties/StatusMessage` – Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="81ae1-353">`feed/entry/content/properties/Progress`– İlerleme durumu (%) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="81ae1-353">`feed/entry/content/properties/Progress` – Build progress (%).</span></span>
* <span data-ttu-id="81ae1-354">`feed/entry/content/properties/StartTime`– Yapı Başlama zamanı.</span><span class="sxs-lookup"><span data-stu-id="81ae1-354">`feed/entry/content/properties/StartTime` – Build start time.</span></span>
* <span data-ttu-id="81ae1-355">`feed/entry/content/properties/EndTime`– Bitiş saati oluşturun.</span><span class="sxs-lookup"><span data-stu-id="81ae1-355">`feed/entry/content/properties/EndTime` – Build end time.</span></span>
* <span data-ttu-id="81ae1-356">`feed/entry/content/properties/ExecutionTime`– Yapı süresi.</span><span class="sxs-lookup"><span data-stu-id="81ae1-356">`feed/entry/content/properties/ExecutionTime` – Build duration.</span></span>
* <span data-ttu-id="81ae1-357">`feed/entry/content/properties/ProgressStep`– Devam eden bir derleme hello geçerli aşaması hakkında ayrıntılar.</span><span class="sxs-lookup"><span data-stu-id="81ae1-357">`feed/entry/content/properties/ProgressStep` – Details about hello current stage that a build in progress is in.</span></span>

<span data-ttu-id="81ae1-358">Geçerli yapı durumu:</span><span class="sxs-lookup"><span data-stu-id="81ae1-358">Valid build status:</span></span>

* <span data-ttu-id="81ae1-359">Oluşturulan – yapı isteği girdisi oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="81ae1-359">Created – Build request entry was created.</span></span>
* <span data-ttu-id="81ae1-360">Sıraya – oluşturma isteği tetiklendi ve kuyruğa alınır.</span><span class="sxs-lookup"><span data-stu-id="81ae1-360">Queued – Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="81ae1-361">Yapı – derleme işlemi devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="81ae1-361">Building – Build is in process.</span></span>
* <span data-ttu-id="81ae1-362">Başarılı – yapı başarılı bir şekilde sona erdi.</span><span class="sxs-lookup"><span data-stu-id="81ae1-362">Success – Build ended successfully.</span></span>
* <span data-ttu-id="81ae1-363">Hata – derleme bir hata ile sona erdi.</span><span class="sxs-lookup"><span data-stu-id="81ae1-363">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="81ae1-364">İptal – derleme iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="81ae1-364">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="81ae1-365">İptal etme – yapı iptal edilir.</span><span class="sxs-lookup"><span data-stu-id="81ae1-365">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="81ae1-366">Derleme türü için geçerli değerler:</span><span class="sxs-lookup"><span data-stu-id="81ae1-366">Valid values for build type:</span></span>

* <span data-ttu-id="81ae1-367">RANK - derece oluşturun.</span><span class="sxs-lookup"><span data-stu-id="81ae1-367">Rank - Rank build.</span></span> <span data-ttu-id="81ae1-368">(Ayrıntıları rank için yapı görüntülenirken hata oluştu, lütfen toohello "Machine Learning öneri API belgelerine" Belge bakın.)</span><span class="sxs-lookup"><span data-stu-id="81ae1-368">(For rank build details, please refer toohello "Machine Learning Recommendation API documentation" document.)</span></span>
* <span data-ttu-id="81ae1-369">Öneri - öneri derleme.</span><span class="sxs-lookup"><span data-stu-id="81ae1-369">Recommendation - Recommendation build.</span></span>
* <span data-ttu-id="81ae1-370">Fbt - sık satın birlikte derleme.</span><span class="sxs-lookup"><span data-stu-id="81ae1-370">Fbt - Frequently bought together build.</span></span>

<span data-ttu-id="81ae1-371">OData XML</span><span class="sxs-lookup"><span data-stu-id="81ae1-371">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get builds status of a model</subtitle>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetBuildsStatusEntity</title>
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
        <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
        <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
        <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
        <d:BuildId m:type="Edm.String">1000272</d:BuildId>
        <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
        <d:Status m:type="Edm.String">Success</d:Status>
        <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
        <d:Progress m:type="Edm.String">0</d:Progress>
        <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
        <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
        <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
        <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
        <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
      </m:properties>
     </content>
    </entry>
    </feed>


### <a name="get-recommendations"></a><span data-ttu-id="81ae1-372">Öneriler alın</span><span class="sxs-lookup"><span data-stu-id="81ae1-372">Get recommendations</span></span>
| <span data-ttu-id="81ae1-373">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="81ae1-373">HTTP Method</span></span> | <span data-ttu-id="81ae1-374">URI</span><span class="sxs-lookup"><span data-stu-id="81ae1-374">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="81ae1-375">AL</span><span class="sxs-lookup"><span data-stu-id="81ae1-375">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="81ae1-376">Örnek:</span><span class="sxs-lookup"><span data-stu-id="81ae1-376">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="81ae1-377">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="81ae1-377">Parameter Name</span></span> | <span data-ttu-id="81ae1-378">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="81ae1-378">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="81ae1-379">modelId</span><span class="sxs-lookup"><span data-stu-id="81ae1-379">modelId</span></span> |<span data-ttu-id="81ae1-380">Benzersiz tanımlayıcı hello modelinin (büyük küçük harfe duyarlı)</span><span class="sxs-lookup"><span data-stu-id="81ae1-380">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="81ae1-381">öğe kimliklerinin</span><span class="sxs-lookup"><span data-stu-id="81ae1-381">itemIds</span></span> |<span data-ttu-id="81ae1-382">Merhaba öğeleri toorecommend için virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="81ae1-382">Comma-separated list of hello items toorecommend for.</span></span><br><span data-ttu-id="81ae1-383">En fazla uzunluk: 1024</span><span class="sxs-lookup"><span data-stu-id="81ae1-383">Max length: 1024</span></span> |
| <span data-ttu-id="81ae1-384">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="81ae1-384">numberOfResults</span></span> |<span data-ttu-id="81ae1-385">Gerekli sonuç sayısı</span><span class="sxs-lookup"><span data-stu-id="81ae1-385">Number of required results</span></span> |
| <span data-ttu-id="81ae1-386">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="81ae1-386">includeMetatadata</span></span> |<span data-ttu-id="81ae1-387">Gelecekte kullanmak, her zaman yanlış</span><span class="sxs-lookup"><span data-stu-id="81ae1-387">Future use, always false</span></span> |
| <span data-ttu-id="81ae1-388">apiVersion</span><span class="sxs-lookup"><span data-stu-id="81ae1-388">apiVersion</span></span> |<span data-ttu-id="81ae1-389">1.0</span><span class="sxs-lookup"><span data-stu-id="81ae1-389">1.0</span></span> |

<span data-ttu-id="81ae1-390">**Yanıtı:**</span><span class="sxs-lookup"><span data-stu-id="81ae1-390">**Response:**</span></span>

<span data-ttu-id="81ae1-391">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="81ae1-391">HTTP Status code: 200</span></span>

<span data-ttu-id="81ae1-392">Merhaba yanıt önerilen öğe başına bir giriş içerir.</span><span class="sxs-lookup"><span data-stu-id="81ae1-392">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="81ae1-393">Her giriş verileri aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="81ae1-393">Each entry has hello following data:</span></span>

* <span data-ttu-id="81ae1-394">`Feed\entry\content\properties\Id`-Önerilen öğesi kimliği</span><span class="sxs-lookup"><span data-stu-id="81ae1-394">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="81ae1-395">`Feed\entry\content\properties\Name`-Hello öğesinin adı.</span><span class="sxs-lookup"><span data-stu-id="81ae1-395">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="81ae1-396">`Feed\entry\content\properties\Rating`-Hello öneri derecesi; daha yüksek numarası, daha yüksek güvenilirlik anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="81ae1-396">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="81ae1-397">`Feed\entry\content\properties\Reasoning`-Öneri mantığı (örneğin, öneri açıklamaları).</span><span class="sxs-lookup"><span data-stu-id="81ae1-397">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (for example, recommendation explanations).</span></span>

<span data-ttu-id="81ae1-398">OData XML</span><span class="sxs-lookup"><span data-stu-id="81ae1-398">OData XML</span></span>

<span data-ttu-id="81ae1-399">Aşağıdaki örnek yanıt Hello 10 önerilen öğeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="81ae1-399">hello example response below includes 10 recommended items:</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">159</d:Id>
        <d:Name m:type="Edm.String">159</d:Name>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">52</d:Id>
        <d:Name m:type="Edm.String">52</d:Name>
        <d:Rating m:type="Edm.Double">0.539588900748721</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">35</d:Id>
        <d:Name m:type="Edm.String">35</d:Name>
        <d:Rating m:type="Edm.Double">0.53842946443853</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '35'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">124</d:Id>
        <d:Name m:type="Edm.String">124</d:Name>
        <d:Rating m:type="Edm.Double">0.536712832792886</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '124'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">120</d:Id>
        <d:Name m:type="Edm.String">120</d:Name>
        <d:Rating m:type="Edm.Double">0.533673023762878</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '120'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">96</d:Id>
        <d:Name m:type="Edm.String">96</d:Name>
        <d:Rating m:type="Edm.Double">0.532544826370521</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '96'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">69</d:Id>
        <d:Name m:type="Edm.String">69</d:Name>
        <d:Rating m:type="Edm.Double">0.531678607847759</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '69'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">172</d:Id>
        <d:Name m:type="Edm.String">172</d:Name>
        <d:Rating m:type="Edm.Double">0.530957821375951</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '172'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">155</d:Id>
        <d:Name m:type="Edm.String">155</d:Name>
        <d:Rating m:type="Edm.Double">0.529093541481333</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '155'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">32</d:Id>
        <d:Name m:type="Edm.String">32</d:Name>
        <d:Rating m:type="Edm.Double">0.528917978168322</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '32'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="update-model"></a><span data-ttu-id="81ae1-400">Bir güncelleştirme modeli</span><span class="sxs-lookup"><span data-stu-id="81ae1-400">Update model</span></span>
<span data-ttu-id="81ae1-401">Merhaba modeli güncelleştirmesi ya da etkin yapı kimliği hello</span><span class="sxs-lookup"><span data-stu-id="81ae1-401">You can update hello model description or hello active build ID.</span></span>
<span data-ttu-id="81ae1-402">*Etkin yapı kimliği* -her derleme her model için bir yapı kimliği vardır.</span><span class="sxs-lookup"><span data-stu-id="81ae1-402">*Active build ID* - Every build for every model has a build ID.</span></span> <span data-ttu-id="81ae1-403">Merhaba etkin yapı kimliği hello ilk başarılı her yeni modelinin yapıdır.</span><span class="sxs-lookup"><span data-stu-id="81ae1-403">hello active build ID is hello first successful build of every new model.</span></span> <span data-ttu-id="81ae1-404">Bir etkin yapı Kimliğine sahip ve ek derlemeler hello için bunu bir kez aynı modelin ihtiyacınız tooexplicitly ayarlayın, bu, hello varsayılan derleme gibi kimliği istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="81ae1-404">Once you have an active build ID and you do additional builds for hello same model, you need tooexplicitly set it as hello default build ID if you want to.</span></span> <span data-ttu-id="81ae1-405">Ne zaman toouse, bir otomatik olarak kullanılacak hello varsayılan istediğiniz hello derleme kimliği belirtmezseniz, öneriler, tüketir.</span><span class="sxs-lookup"><span data-stu-id="81ae1-405">When you consume recommendations, if you do not specify hello build ID that you want toouse, hello default one will be used automatically.</span></span>

<span data-ttu-id="81ae1-406">Üretim - toobuild yeni modelleri öneri modeline sahiptir ve bunları yükseltmeden önce bunları tooproduction test sonra bu düzenek - sağlar.</span><span class="sxs-lookup"><span data-stu-id="81ae1-406">This mechanism enables you - once you have a recommendation model in production - toobuild new models and test them before you promote them tooproduction.</span></span>

| <span data-ttu-id="81ae1-407">HTTP yöntemi</span><span class="sxs-lookup"><span data-stu-id="81ae1-407">HTTP Method</span></span> | <span data-ttu-id="81ae1-408">URI</span><span class="sxs-lookup"><span data-stu-id="81ae1-408">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="81ae1-409">PUT</span><span class="sxs-lookup"><span data-stu-id="81ae1-409">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="81ae1-410">Örnek:</span><span class="sxs-lookup"><span data-stu-id="81ae1-410">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="81ae1-411">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="81ae1-411">Parameter Name</span></span> | <span data-ttu-id="81ae1-412">Geçerli Değerler</span><span class="sxs-lookup"><span data-stu-id="81ae1-412">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="81ae1-413">id</span><span class="sxs-lookup"><span data-stu-id="81ae1-413">id</span></span> |<span data-ttu-id="81ae1-414">Benzersiz tanımlayıcı hello modelinin (büyük küçük harfe duyarlı)</span><span class="sxs-lookup"><span data-stu-id="81ae1-414">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="81ae1-415">apiVersion</span><span class="sxs-lookup"><span data-stu-id="81ae1-415">apiVersion</span></span> |<span data-ttu-id="81ae1-416">1.0</span><span class="sxs-lookup"><span data-stu-id="81ae1-416">1.0</span></span> |
|  | |
| <span data-ttu-id="81ae1-417">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="81ae1-417">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br><span data-ttu-id="81ae1-418">Merhaba XML açıklama etiketleri ve ActiveBuildId isteğe bağlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="81ae1-418">Note that hello XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="81ae1-419">Açıklama veya ActiveBuildId tooset istemiyorsanız hello tüm etiket kaldırın.</span><span class="sxs-lookup"><span data-stu-id="81ae1-419">If you do not want tooset Description or ActiveBuildId, remove hello entire tag.</span></span> |

<span data-ttu-id="81ae1-420">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="81ae1-420">**Response**:</span></span>

<span data-ttu-id="81ae1-421">HTTP durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="81ae1-421">HTTP Status code: 200</span></span>

<span data-ttu-id="81ae1-422">OData XML</span><span class="sxs-lookup"><span data-stu-id="81ae1-422">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a><span data-ttu-id="81ae1-423">Yasal Bilgiler</span><span class="sxs-lookup"><span data-stu-id="81ae1-423">Legal</span></span>
<span data-ttu-id="81ae1-424">Bu belgede sağlanan "olarak-olan".</span><span class="sxs-lookup"><span data-stu-id="81ae1-424">This document is provided "as-is".</span></span> <span data-ttu-id="81ae1-425">URL ve diğer Internet Web sitesi başvuruları dahil olmak üzere bu belgede belirtilen bilgiler ve görüntüler bildirim yapılmadan değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="81ae1-425">Information and views expressed in this document, including URL and other Internet website references, may change without notice.</span></span> <span data-ttu-id="81ae1-426">Burada açıklanan bazı örnekler yalnızca çizim için sağlanmıştır ve kurgusaldır.</span><span class="sxs-lookup"><span data-stu-id="81ae1-426">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="81ae1-427">Gerçek bir ilişki veya bağlantı amaçlanmamıştır veya çıkarılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="81ae1-427">No real association or connection is intended or should be inferred.</span></span> <span data-ttu-id="81ae1-428">Bu belge, herhangi bir yasal hak ile herhangi bir Microsoft ürünü üzerinde tooany fikri mülkiyet sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="81ae1-428">This document does not provide you with any legal rights tooany intellectual property in any Microsoft product.</span></span> <span data-ttu-id="81ae1-429">Kopyalayabilir ve bu belgeyi şirket içinde kullanmak başvuru amaçlıdır.</span><span class="sxs-lookup"><span data-stu-id="81ae1-429">You may copy and use this document for your internal, reference purposes.</span></span> <span data-ttu-id="81ae1-430">© 2014 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="81ae1-430">© 2014 Microsoft.</span></span> <span data-ttu-id="81ae1-431">Tüm hakları saklıdır.</span><span class="sxs-lookup"><span data-stu-id="81ae1-431">All rights reserved.</span></span> 

