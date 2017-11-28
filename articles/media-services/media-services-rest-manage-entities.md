---
title: "aaaManaging Media Services REST varlıklarıyla | Microsoft Docs"
description: "Toomanage medya hizmetleri nasıl öğrenin REST API'si olan varlık."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 95262a32-0f2a-4286-b9e2-1a1ca6399b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: bcdc5288e422ebc4e6f682a97da4e925ce237a79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-media-services-entities-with-rest"></a><span data-ttu-id="ea4bb-103">Media Services REST varlıklarıyla yönetme</span><span class="sxs-lookup"><span data-stu-id="ea4bb-103">Managing Media Services entities with REST</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea4bb-104">REST</span><span class="sxs-lookup"><span data-stu-id="ea4bb-104">REST</span></span>](media-services-rest-manage-entities.md)
> * [<span data-ttu-id="ea4bb-105">.NET</span><span class="sxs-lookup"><span data-stu-id="ea4bb-105">.NET</span></span>](media-services-dotnet-manage-entities.md)
> 
> 

<span data-ttu-id="ea4bb-106">Microsoft Azure Media Services OData v3 üzerinde oluşturulmuş bir REST tabanlı hizmettir.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-106">Microsoft Azure Media Services is a REST-based service built on OData v3.</span></span> <span data-ttu-id="ea4bb-107">Yolu, başka bir OData hizmet gibi ekleyebilir, sorgu, güncelleştirme ve silme varlıkları çok aynı hello.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-107">You can add, query, update, and delete entities in much hello same way as you can on any other OData service.</span></span> <span data-ttu-id="ea4bb-108">Özel durumlar gerekli olduğunda çağrılacak.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-108">Exceptions will be called out when applicable.</span></span> <span data-ttu-id="ea4bb-109">OData hakkında daha fazla bilgi için bkz: [açık veri Protokolü belgeleri](http://www.odata.org/documentation/).</span><span class="sxs-lookup"><span data-stu-id="ea4bb-109">For more information on OData, see [Open Data Protocol documentation](http://www.odata.org/documentation/).</span></span>

<span data-ttu-id="ea4bb-110">Bu konu, nasıl gösterir toomanage Azure Media Services REST varlıklarıyla.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-110">This topic shows you how toomanage Azure Media Services entities with REST.</span></span>

>[!NOTE]
> <span data-ttu-id="ea4bb-111">Merhaba toplam kayıt sayısı hello en yüksek kota altında olsa bile 1 Nisan 2017 başlangıç 90 günden daha eski hesabınızda herhangi bir işi kaydının otomatik olarak, ilişkili görev kayıtlarını yanı sıra, silinir.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-111">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if hello total number of records is below hello maximum quota.</span></span> <span data-ttu-id="ea4bb-112">Örneğin, 1 Nisan 2017 üzerinde 31 Aralık 2016'den daha eski hesabınızda herhangi bir işi kaydının otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-112">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="ea4bb-113">Tooarchive hello iş/görevi bilgiye ihtiyacınız varsa, bu konuda açıklanan hello kodu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-113">If you need tooarchive hello job/task information, you can use hello code described in this topic.</span></span>

## <a name="considerations"></a><span data-ttu-id="ea4bb-114">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="ea4bb-114">Considerations</span></span>  

<span data-ttu-id="ea4bb-115">Varlıklar Media Services erişirken, HTTP istekleri özel üstbilgi alanlarını ve değerlerini ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-115">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="ea4bb-116">Daha fazla bilgi için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="ea4bb-116">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="ea4bb-117">TooMedia Hizmetleri'ne Bağlama</span><span class="sxs-lookup"><span data-stu-id="ea4bb-117">Connect tooMedia Services</span></span>

<span data-ttu-id="ea4bb-118">Nasıl tooconnect toohello AMS API, bkz. bilgi [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="ea4bb-118">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="ea4bb-119">Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-119">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="ea4bb-120">Sonraki çağrılar toohello yapmanız gereken yeni bir URI.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-120">You must make subsequent calls toohello new URI.</span></span>

## <a name="adding-entities"></a><span data-ttu-id="ea4bb-121">Varlıklar ekleme</span><span class="sxs-lookup"><span data-stu-id="ea4bb-121">Adding entities</span></span>
<span data-ttu-id="ea4bb-122">Media Services her varlık tooan varlık kümesi, varlıklar gibi bir HTTP POST isteği üzerinden eklenir.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-122">Every entity in Media Services is added tooan entity set, such as Assets, through a POST HTTP request.</span></span>

<span data-ttu-id="ea4bb-123">örnekte gösterildiği nasıl aşağıdaki hello toocreate bir AccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-123">hello following example shows how toocreate an AccessPolicy.</span></span>

    POST https://media.windows.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

## <a name="querying-entities"></a><span data-ttu-id="ea4bb-124">Varlıkları sorgulama</span><span class="sxs-lookup"><span data-stu-id="ea4bb-124">Querying entities</span></span>
<span data-ttu-id="ea4bb-125">Sorgulamak ve varlıkları listeleyen basittir ve yalnızca bir HTTP GET isteği ve isteğe bağlı OData işlemleri içerir.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-125">Querying and listing entities is straightforward and only involves a GET HTTP request and optional OData operations.</span></span>
<span data-ttu-id="ea4bb-126">Merhaba aşağıdaki örnekte tüm MediaProcessor varlıkların listesini alır.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-126">hello following example retrieves a list of all MediaProcessor entities.</span></span>

    GET https://media.windows.net/API/MediaProcessors HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="ea4bb-127">Ayrıca, belirli bir varlık veya hello örnekler aşağıdaki gibi belirli bir varlıkla ilişkilendirilen tüm varlık kümelerini alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ea4bb-127">You can also retrieve a specific entity or all entity sets associated with a specific entity, such as in hello following examples:</span></span>

    GET https://media.windows.net/API/JobTemplates('nb:jtid:UUID:e81192f5-576f-b247-b781-70a790c20e7c') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336907474&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=OpuY0CeTylqFFcFaP4pKUVGesT4PGx4CP55zDf2zXnc%3d
    Host: media.windows.net

    GET https://media.windows.net/API/JobTemplates('nb:jtid:UUID:e81192f5-576f-b247-b781-70a790c20e7c')/TaskTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336907474&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=OpuY0CeTylqFFcFaP4pKUVGesT4PGx4CP55zDf2zXnc%3d
    Host: media.windows.net

<span data-ttu-id="ea4bb-128">Merhaba aşağıdaki örnekte yalnızca hello durumu özelliği tüm işlerin döndürür.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-128">hello following example returns only hello State property of all Jobs.</span></span>

    GET https://media.windows.net/API/Jobs?$select=State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="ea4bb-129">Merhaba aşağıdaki örnek verir tüm JobTemplates hello adlı "SampleTemplate."</span><span class="sxs-lookup"><span data-stu-id="ea4bb-129">hello following example returns all JobTemplates with hello name "SampleTemplate."</span></span>

    GET https://media.windows.net/API/JobTemplates?$filter=startswith(Name,%20'SampleTemplate') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

> [!NOTE]
> <span data-ttu-id="ea4bb-130">Merhaba $expand işlemi Media Services yanı sıra LINQ konuları (WCF Veri Hizmetleri) açıklanan desteklenmeyen LINQ yöntemleri hello desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-130">hello $expand operation is not supported in Media Services as well as hello unsupported LINQ methods described in LINQ Considerations (WCF Data Services).</span></span>
> 
> 

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="ea4bb-131">Varlıkları büyük koleksiyonlarına numaralandırma</span><span class="sxs-lookup"><span data-stu-id="ea4bb-131">Enumerating through large collections of entities</span></span>
<span data-ttu-id="ea4bb-132">Varlıkları sorgulanırken ortak REST v2 sorgu sonuçları too1000 sonuçları sınırladığından aynı anda döndürülen 1000 varlıkların bir sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-132">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results too1000 results.</span></span> <span data-ttu-id="ea4bb-133">Kullanım **atla** ve **üst** hello büyük varlık koleksiyonunu aracılığıyla tooenumerate.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-133">Use **skip** and **top** tooenumerate through hello large collection of entities.</span></span> 

<span data-ttu-id="ea4bb-134">örnekte gösterildiği nasıl aşağıdaki hello toouse **atla** ve **üst** tooskip hello ilk 2000 işleri ve get hello sonraki 1000 işler.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-134">hello following example shows how toouse **skip** and **top** tooskip hello first 2000 jobs and get hello next 1000 jobs.</span></span>  

    GET https://media.windows.net/api/Jobs()?$skip=2000&$top=1000 HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

## <a name="updating-entities"></a><span data-ttu-id="ea4bb-135">Varlıkları güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="ea4bb-135">Updating entities</span></span>
<span data-ttu-id="ea4bb-136">Merhaba varlık türü ve olarak hello durumuna bağlı olarak, PUT ya da birleştirme HTTP isteklerini bir düzeltme eki aracılığıyla bu varlıkta özellikleri güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-136">Depending on hello entity type and hello state that it is in, you can update properties on that entity through a PATCH, PUT, or MERGE HTTP requests.</span></span> <span data-ttu-id="ea4bb-137">Bu işlemler hakkında daha fazla bilgi için bkz: [PUT/düzeltme eki/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea4bb-137">For more information about these operations, see [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="ea4bb-138">Aşağıdaki kod örneğine hello nasıl tooupdate hello Name özelliğine göre bir varlık varlık gösterir.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-138">hello following code example shows how tooupdate hello Name property on an Asset entity.</span></span>

    MERGE https://media.windows.net/API/Assets('nb:cid:UUID:80782407-3f87-4e60-a43e-5e4454232f60') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337083279&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=DMLQXWah4jO0icpfwyws5k%2b1aCDfz9KDGIGao20xk6g%3d
    Host: media.windows.net
    Content-Length: 21
    Expect: 100-continue

    {"Name" : "NewName" }

## <a name="deleting-entities"></a><span data-ttu-id="ea4bb-139">Varlıkları silme</span><span class="sxs-lookup"><span data-stu-id="ea4bb-139">Deleting entities</span></span>
<span data-ttu-id="ea4bb-140">Varlıkları silme HTTP isteği kullanarak Media Services silinebilir.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-140">Entities can be deleted in Media Services by using a DELETE HTTP request.</span></span> <span data-ttu-id="ea4bb-141">Merhaba varlık bağlı olarak, varlıkları silme hello sırası önemli olabilir.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-141">Depending on hello entity, hello order in which you delete entities may be important.</span></span> <span data-ttu-id="ea4bb-142">Örneğin, varlıklar gibi varlıkları gerektiren, iptal etme (veya Sil) hello varlık silmeden önce bu belirli varlık başvurusu tüm Bulucular.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-142">For example, entities such as Assets require that you revoke (or delete) all Locators that reference that particular Asset before deleting hello Asset.</span></span>

<span data-ttu-id="ea4bb-143">örnekte gösterildiği nasıl aşağıdaki hello toodelete blob depolama alanına kullanılan tooupload bir dosya olan bir Bulucu.</span><span class="sxs-lookup"><span data-stu-id="ea4bb-143">hello following example shows how toodelete a Locator that was used tooupload a file into blob storage.</span></span>

    DELETE https://media.windows.net/API/Locators('nb:lid:UUID:76dcc8e8-4230-463d-97b0-ce25c41b5c8d') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 0

## <a name="media-services-learning-paths"></a><span data-ttu-id="ea4bb-144">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="ea4bb-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ea4bb-145">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="ea4bb-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

