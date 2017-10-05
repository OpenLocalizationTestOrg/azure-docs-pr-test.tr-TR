---
title: "REST kullanarak medya işlemcisi örneği alma | Microsoft Docs"
description: "Kodlama, biçimine dönüştürmek, şifrelemek veya medya içeriği için Azure Media Services şifresini çözmek için bir medya işlemci bileşeni oluşturmayı öğrenin."
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
ms.openlocfilehash: 4ad90ad979c5bd74fc55155098c88d5c13cb12e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="1b471-103">Medya işlemcisi örneği alma</span><span class="sxs-lookup"><span data-stu-id="1b471-103">How to get a Media Processor instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1b471-104">.NET</span><span class="sxs-lookup"><span data-stu-id="1b471-104">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="1b471-105">REST</span><span class="sxs-lookup"><span data-stu-id="1b471-105">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="1b471-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="1b471-106">Overview</span></span>
<span data-ttu-id="1b471-107">Medya işlemcisi kodlama gibi kodlama, ek olarak, belirli işleme görevi işleyen bir bileşenidir Media Services'de şifreleme veya medya içeriği çözme dönüştürme biçimi.</span><span class="sxs-lookup"><span data-stu-id="1b471-107">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="1b471-108">Kodlama, şifreleme veya medya içeriği biçimine dönüştürmek için bir görev oluştururken genellikle medya işlemcisi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1b471-108">You typically create a media processor when you are creating a task to encode, encrypt, or convert the format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="1b471-109">Azure medya işlemcileri</span><span class="sxs-lookup"><span data-stu-id="1b471-109">Azure media processors</span></span> 

<span data-ttu-id="1b471-110">Aşağıdaki konu medya işlemcileri listesi sağlar:</span><span class="sxs-lookup"><span data-stu-id="1b471-110">The following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="1b471-111">Kodlama medya işlemcileri</span><span class="sxs-lookup"><span data-stu-id="1b471-111">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="1b471-112">Analizi medya işlemcileri</span><span class="sxs-lookup"><span data-stu-id="1b471-112">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
><span data-ttu-id="1b471-113">Varlıklar Media Services erişirken, HTTP istekleri özel üstbilgi alanlarını ve değerlerini ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b471-113">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="1b471-114">Daha fazla bilgi için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="1b471-114">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="1b471-115">Media Services’e bağlanmak</span><span class="sxs-lookup"><span data-stu-id="1b471-115">Connect to Media Services</span></span>

<span data-ttu-id="1b471-116">AMS API'sine bağlanma hakkında daha fazla bilgi için bkz: [Azure AD kimlik doğrulaması ile Azure Media Services API erişim](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="1b471-116">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="1b471-117">Başarıyla https://media.windows.net için bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız.</span><span class="sxs-lookup"><span data-stu-id="1b471-117">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="1b471-118">Yeni bir URI yapılan sonraki çağrılar yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b471-118">You must make subsequent calls to the new URI.</span></span>

## <a name="get-a-media-processor"></a><span data-ttu-id="1b471-119">Medya işlemcisi Al</span><span class="sxs-lookup"><span data-stu-id="1b471-119">Get a media processor</span></span>

<span data-ttu-id="1b471-120">Medya işlemcisi örneği tarafından adını almak nasıl aşağıdaki REST çağrısı gösterir (Bu durumda, **Medya Kodlayıcısı standart**).</span><span class="sxs-lookup"><span data-stu-id="1b471-120">The following REST call shows how to get a media processor instance by name (in this case, **Media Encoder Standard**).</span></span> 

<span data-ttu-id="1b471-121">İsteği:</span><span class="sxs-lookup"><span data-stu-id="1b471-121">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="1b471-122">Yanıtı:</span><span class="sxs-lookup"><span data-stu-id="1b471-122">Response:</span></span>

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


## <a name="media-services-learning-paths"></a><span data-ttu-id="1b471-123">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="1b471-123">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1b471-124">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="1b471-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="1b471-125">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="1b471-125">Next Steps</span></span>
<span data-ttu-id="1b471-126">Medya işlemcisi örneği alma bildiğinize göre Git [bir varlık kodlama](media-services-rest-get-started.md) konu Medya Kodlayıcısı standart bir varlık kodlama için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="1b471-126">Now that you know how to get a media processor instance, go to the [How to Encode an Asset](media-services-rest-get-started.md) topic which will show you how to use the Media Encoder Standard to encode an asset.</span></span>

