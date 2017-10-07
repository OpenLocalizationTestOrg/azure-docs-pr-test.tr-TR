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
# <a name="how-tooget-a-media-processor-instance"></a>Nasıl tooget bir medya işlemcisi örneği
> [!div class="op_single_selector"]
> * [.NET](media-services-get-media-processor.md)
> * [REST](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a>Genel Bakış
Medya işlemcisi kodlama gibi kodlama, ek olarak, belirli işleme görevi işleyen bir bileşenidir Media Services'de şifreleme veya medya içeriği çözme dönüştürme biçimi. Genellikle bir görev tooencode oluşturulurken medya işlemcisi oluşturma, şifrelemek veya medya içeriği hello biçimine dönüştürün.

## <a name="azure-media-processors"></a>Azure medya işlemcileri 

konu aşağıdaki hello medya işlemcileri listesi sağlar:

* [Kodlama medya işlemcileri](scenarios-and-availability.md#encoding-media-processors)
* [Analizi medya işlemcileri](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
>Varlıklar Media Services erişirken, HTTP istekleri özel üstbilgi alanlarını ve değerlerini ayarlamanız gerekir. Daha fazla bilgi için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).

## <a name="connect-toomedia-services"></a>TooMedia Hizmetleri'ne Bağlama

Nasıl tooconnect toohello AMS API, bkz. bilgi [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız. Sonraki çağrılar toohello yapmanız gereken yeni bir URI.

## <a name="get-a-media-processor"></a>Medya işlemcisi Al

REST çağrısı aşağıdaki hello gösterir nasıl tooget medya işlemcisi örneği adıyla (Bu durumda, **Medya Kodlayıcısı standart**). 

İsteği:

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

Yanıtı:

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


## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Sonraki Adımlar
Artık bildiğinize göre nasıl tooget medya işlemci örneği Git toohello [nasıl tooEncode bir varlık](media-services-rest-get-started.md) nasıl toouse hello Medya Kodlayıcısı standart tooencode bir varlık gösterecektir konu.

