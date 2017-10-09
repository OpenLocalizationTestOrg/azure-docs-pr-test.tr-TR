---
title: "aaaMedia Hizmetleri operations REST API genel bakış | Microsoft Docs"
description: "Media Services REST API genel bakış"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a5f1c5e7-ec52-4e26-9a44-d9ea699f68d9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b54f4d9123486d6cae832c9817688b0f3da5b401
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-operations-rest-api-overview"></a>Media Services operations REST API genel bakış
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

Merhaba **Media Services Operations REST** API işleri, varlıklar, erişim ilkeleri ve nesneler üzerinde başka işlemler bir medya hizmeti hesabı oluşturmak için kullanılır. Daha fazla bilgi için bkz: [Media Services Operations REST API Başvurusu](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).

Microsoft Azure Media Services OData göre HTTP isteklerini kabul eden bir hizmettir ve geri ayrıntılı JSON veya atom + pub biçiminde yanıtlayabilir. Media Services tooAzure tasarım yönergeleri uyumlu olmadığından kullanılabilir İsteğe bağlı üstbilgi kümesi yanı sıra her istemci tooMedia Hizmetleri bağlanırken kullanması gereken gerekli HTTP üstbilgi kümesi yoktur. Merhaba aşağıdaki bölümlerde açıklanmaktadır hello üstbilgileri ve ne zaman kullanabilir HTTP fiilleri istekleri oluşturma ve yanıtları Media Services'den alma.

Bu konu hakkında genel bakış sunar toouse REST v2 Media Services ile.

## <a name="considerations"></a>Dikkat edilmesi gerekenler

ilgili önemli noktalar aşağıdaki hello REST kullanılırken uygulanır.

* Varlıkları sorgulanırken ortak REST v2 sorgu sonuçları too1000 sonuçları sınırladığından aynı anda döndürülen 1000 varlıkların bir sınırı yoktur. Toouse gerek **atla** ve **ele** (.NET) / **üst** (açıklandığı gibi REST) [bu .NET örnek](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) ve [bu REST API'si örnek](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities). 
* JSON kullanarak ve toouse hello belirterek **__metadata** hello isteğinde hello ayarlamanız gerekir (örneğin, bağlantılı nesne tooreferences) anahtar sözcüğü **kabul** üstbilgisi çok[JSON Verbose biçimi ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/) (Merhaba aşağıdaki örneğine bakın). OData hello anlamak değil **__metadata** tooverbose ayarlanmadığı sürece hello özelliğinde isteği.  
  
        POST https://media.windows.net/API/Jobs HTTP/1.1
        Content-Type: application/json;odata=verbose
        Accept: application/json;odata=verbose
        DataServiceVersion: 3.0
        MaxDataServiceVersion: 3.0
        x-ms-version: 2.11
        Authorization: Bearer <token> 
        Host: media.windows.net
  
        {
            "Name" : "NewTestJob", 
            "InputMediaAssets" : 
                [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aba5356eb-30ff-4dc6-9e5a-41e4223540e7')"}}]
        . . . 

## <a name="standard-http-request-headers-supported-by-media-services"></a>Media Services tarafından desteklenen standart HTTP isteği üstbilgileri
Medya Hizmetleri içine yaptığınız her çağrı için gerekli başlıklar İsteğinizde içermelidir yoktur ve ayrıca isteğe bağlı üstbilgi kümesi isteyebilir tooinclude. Aşağıdaki tabloda listeleri hello hello üstbilgileri gerekli:

| Üstbilgi | Tür | Değer |
| --- | --- | --- |
| Yetkilendirme |Taşıyıcı |Taşıyıcı yetkilendirme mekanizması hello yalnızca kabul ' dir. ACS tarafından sağlanan hello erişim belirteci Hello değeri de dahil etmelisiniz. |
| x-ms-version |Ondalık |2.11 |
| DataServiceVersion |Ondalık |3.0 |
| MaxDataServiceVersion |Ondalık |3.0 |

> [!NOTE]
> Media Services OData tooexpose kullandığından, temel alınan varlık meta veri deposu hello DataServiceVersion ve MaxDataServiceVersion üstbilgileri REST API'leri aracılığıyla herhangi bir istek eklenmelidir; değilse, ancak daha sonra şu anda Media Services hello DataServiceVersion değeri kullanımda 3.0 olduğunu varsayar.
> 
> 

Merhaba, isteğe bağlı üstbilgi kümesi aşağıdadır:

| Üstbilgi | Tür | Değer |
| --- | --- | --- |
| Tarih |RFC 1123 tarih |Merhaba isteğinin zaman damgası |
| Kabul et |İçerik türü |Merhaba istenen hello aşağıdaki gibi hello yanıtı için içerik türü:<p> -Uygulama/json; odata = verbose<p> -Uygulama/atom + xml<p> Yanıtlar, başarılı bir yanıt hello blob akışı hello yükü olarak burada içerecek bir blob getirme gibi farklı bir içerik türü olabilir. |
| Kabul kodlama |GZIP, deflate |GZIP ve DEFLATE, uygun olduğunda kodlama. Not: büyük kaynaklar için Media Services bu başlığı yoksay ve küçülen veri döndürür. |
| Kabul dili |"en", "es" ve benzeri. |Merhaba yanıtı için tercih edilen hello dilini belirtir. |
| Accept-Charset |"UTF-8" gibi Charset türü |Varsayılan UTF-8'dir. |
| X HTTP yöntemi |HTTP yöntemi |İstemcileri veya HTTP yöntemleri PUT ya da DELETE toouse gibi desteklemeyen güvenlik duvarları GET çağrısıyla tünelli bu yöntemleri sağlar. |
| İçerik türü |İçerik türü |İçerik türünü hello istek gövdesinde PUT veya POST istekleri. |
| İstemci istek kimliği |Dize |İstek verilen hello tanımlayan bir arayan tanımlı bir değer. Belirtilmişse, bu değer hello yanıt iletisinde bir şekilde toomap hello talebi olarak dahil edilir. <p><p>**Önemli**<p>Değerleri 2096b tutulabilir (2k). |

## <a name="standard-http-response-headers-supported-by-media-services"></a>Media Services tarafından desteklenen standart HTTP yanıt üstbilgileri
Merhaba aşağıdaki tooyou isteyen hello kaynak bağlı olarak döndürülebilir ve tooperform hedeflenen eylem hello üst bilgileri kümesidir.

| Üstbilgi | Tür | Değer |
| --- | --- | --- |
| İstek Kimliği |Dize |Merhaba geçerli işlem, oluşturulan hizmet için benzersiz bir tanımlayıcı. |
| İstemci istek kimliği |Dize |Varsa hello özgün istekteki hello çağıran tarafından belirtilen bir tanımlayıcı. |
| Tarih |RFC 1123 tarih |Başlangıç tarihi, hello isteği işlendi. |
| İçerik türü |Değişir |içerik türü hello yanıt gövdesi Hello. |
| İçerik kodlama |Değişir |Gzip veya deflate uygun şekilde. |

## <a name="standard-http-verbs-supported-by-media-services"></a>Media Services tarafından desteklenen standart HTTP fiilleri
Merhaba, HTTP yapmak istediğinde, kullanılabilen HTTP fiilleri tam bir listesi verilmiştir:

| Fiil | Açıklama |
| --- | --- |
| AL |Bir nesnenin geçerli değeri döndürür hello. |
| YAYINLA |Sağlanan hello verilerine dayalı bir nesne oluşturur veya bir komut gönderir. |
| PUT |Bir nesne değiştirir veya (uygunsa) adlı bir nesne oluşturur. |
| SİL |Bir nesneyi siler. |
| BİRLEŞTİRME |Varolan bir nesne belirtilen özellik değişikliklerle güncelleştirir. |
| HEAD |Bir nesnenin GET yanıt meta verileri döndürür. |

## <a name="discover-media-services-model"></a>Medya Hizmetleri modeli keşfedin
toomake Media Services varlıklar daha bulunabilirlik hello $metadata işlemi kullanılabilir. Tooretrieve tanır tüm geçerli bir varlık türleri, varlık özellikleri, ilişkileri, İşlevler, Eylemler ve benzeri. Merhaba aşağıdaki örnekte nasıl tooconstruct hello URI gösterir: https://media.windows.net/API/$ meta verileri.

Eklemeniz gerekir "? api-version=2.x" Merhaba tooview hello meta verileri bir tarayıcıda istiyorsanız veya hello x-ms-version üstbilgi İsteğinizde içermez URI toohello sonu.

## <a name="connect-toomedia-services"></a>TooMedia Hizmetleri'ne Bağlama

Nasıl tooconnect toohello AMS API, bkz. bilgi [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md). Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız. Sonraki çağrılar toohello yapmanız gereken yeni bir URI.

## <a name="next-steps"></a>Sonraki adımlar

tooaccess AMS API'lerinin REST ile bkz [kullanım Azure AD kimlik doğrulama tooaccess hello Azure Media Services API REST ile](media-services-rest-connect-with-aad.md).

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

