---
title: "Medya işlemcisi örneği kullanarak tooget nasıl REST aaa | Microsoft Docs"
description: "Nasıl toocreate medya işlemci bileşeni tooencode biçimine dönüştürmek, şifrelemek veya medya içeriği şifresini çözmek için Azure Media Services öğrenin."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f9ff1997-0da6-4528-aaed-792837e5be41
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 9f423648ab73c90405c64895ce0f5b6a457862e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-a-media-processor-instance"></a><span data-ttu-id="61d39-103">Nasıl tooget bir medya işlemcisi örneği</span><span class="sxs-lookup"><span data-stu-id="61d39-103">How tooget a Media Processor instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="61d39-104">.NET</span><span class="sxs-lookup"><span data-stu-id="61d39-104">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="61d39-105">REST</span><span class="sxs-lookup"><span data-stu-id="61d39-105">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="61d39-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="61d39-106">Overview</span></span>
<span data-ttu-id="61d39-107">Medya işlemcisi kodlama gibi kodlama, ek olarak, belirli işleme görevi işleyen bir bileşenidir Media Services'de şifreleme veya medya içeriği çözme dönüştürme biçimi.</span><span class="sxs-lookup"><span data-stu-id="61d39-107">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="61d39-108">Genellikle bir görev tooencode oluşturulurken medya işlemcisi oluşturma, şifrelemek veya medya içeriği hello biçimine dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="61d39-108">You typically create a media processor when you are creating a task tooencode, encrypt, or convert hello format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="61d39-109">Azure medya işlemcileri</span><span class="sxs-lookup"><span data-stu-id="61d39-109">Azure media processors</span></span> 

<span data-ttu-id="61d39-110">konu aşağıdaki hello medya işlemcileri listesi sağlar:</span><span class="sxs-lookup"><span data-stu-id="61d39-110">hello following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="61d39-111">Kodlama medya işlemcileri</span><span class="sxs-lookup"><span data-stu-id="61d39-111">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="61d39-112">Analizi medya işlemcileri</span><span class="sxs-lookup"><span data-stu-id="61d39-112">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
><span data-ttu-id="61d39-113">Varlıklar Media Services erişirken, HTTP istekleri özel üstbilgi alanlarını ve değerlerini ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="61d39-113">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="61d39-114">Daha fazla bilgi için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="61d39-114">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="61d39-115">TooMedia Hizmetleri'ne Bağlama</span><span class="sxs-lookup"><span data-stu-id="61d39-115">Connect tooMedia Services</span></span>

<span data-ttu-id="61d39-116">Nasıl tooconnect toohello AMS API, bkz. bilgi [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="61d39-116">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="61d39-117">Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız.</span><span class="sxs-lookup"><span data-stu-id="61d39-117">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="61d39-118">Sonraki çağrılar toohello yapmanız gereken yeni bir URI.</span><span class="sxs-lookup"><span data-stu-id="61d39-118">You must make subsequent calls toohello new URI.</span></span>

## <a name="get-a-media-processor"></a><span data-ttu-id="61d39-119">Medya işlemcisi Al</span><span class="sxs-lookup"><span data-stu-id="61d39-119">Get a media processor</span></span>

<span data-ttu-id="61d39-120">REST çağrısı aşağıdaki hello gösterir nasıl tooget medya işlemcisi örneği adıyla (Bu durumda, **Medya Kodlayıcısı standart**).</span><span class="sxs-lookup"><span data-stu-id="61d39-120">hello following REST call shows how tooget a media processor instance by name (in this case, **Media Encoder Standard**).</span></span> 

<span data-ttu-id="61d39-121">İsteği:</span><span class="sxs-lookup"><span data-stu-id="61d39-121">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="61d39-122">Yanıtı:</span><span class="sxs-lookup"><span data-stu-id="61d39-122">Response:</span></span>

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="61d39-123">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="61d39-123">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="61d39-124">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="61d39-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="61d39-125">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="61d39-125">Next Steps</span></span>
<span data-ttu-id="61d39-126">Artık bildiğinize göre nasıl tooget medya işlemci örneği Git toohello [nasıl tooEncode bir varlık](media-services-rest-get-started.md) nasıl toouse hello Medya Kodlayıcısı standart tooencode bir varlık gösterecektir konu.</span><span class="sxs-lookup"><span data-stu-id="61d39-126">Now that you know how tooget a media processor instance, go toohello [How tooEncode an Asset](media-services-rest-get-started.md) topic which will show you how toouse hello Media Encoder Standard tooencode an asset.</span></span>

