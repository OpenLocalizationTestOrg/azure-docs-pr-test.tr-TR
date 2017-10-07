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
# <a name="quick-start-guide-for-hello-machine-learning-recommendations-api-version-1"></a>Merhaba Machine Learning önerileri API'si (sürüm 1) için Hızlı Başlangıç Kılavuzu

> [!NOTE]
> Hello kullanarak başlamalıdır [önerileri API Bilişsel hizmeti](https://www.microsoft.com/cognitive-services/recommendations-api) bu sürümü yerine. Merhaba önerileri Bilişsel hizmet bu hizmeti koyacağınız ve tüm hello yeni özellikler vardır geliştirilmiştir. Toplu işlem desteği, daha iyi API'si Gezgini, bir temizleyici API yüzeyi, daha tutarlı kaydolma/faturalandırma deneyimi, vb. gibi yeni özellikler vardır.
>
> Daha fazla bilgi edinmek [geçiş toohello yeni Bilişsel hizmet](http://aka.ms/recomigrate).
> 
> 

Bu belgede açıklanan nasıl tooonboard, hizmet veya uygulama toouse Microsoft Azure Machine Learning öneriler. Merhaba hello önerileri API'si hakkında daha fazla ayrıntı bulabilirsiniz [Cortana Intelligence Galerisi](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a>Genel bir bakış
Azure Machine Learning önerileri toouse, aşağıdaki adımları tootake hello gerekir:

* Bir model oluşturma - bir model kullanım verileri, katalog verilerini ve hello öneri modeli, bir kapsayıcısıdır.
* İçeri aktarma katalog verilerini - katalog hello öğeler üzerinde meta veri bilgileri içerir. 
* İçeri aktarma kullanım verilerini - kullanım verilerini iki yoldan biriyle (veya her ikisi de) yüklenebilir:
  * Merhaba kullanım verilerini içeren bir dosyayı karşıya yükleyerek.
  * Veri alma olaylarını göndererek.
    Genellikle bir sipariş toobe mümkün toocreate (önyükleme) bir ilk öneri modeli kullanım dosyayı karşıya yükleme ve hello veri alım biçimi kullanarak hello sistem yeterli veri toplayan kadar kullanın.
* Bir öneri model oluşturma - bu zaman uyumsuz bir işlemin hangi hello öneri sistem, tüm hello kullanım verileri alır ve bir öneri modeli oluşturur. Bu işlem birkaç dakika alabilir veya hello bağlı olarak birkaç saat boyutunu hello veri ve hello yapı yapılandırma parametreleri. Merhaba yapı tetiklendiğinde bir yapı kimliği alırsınız Tooconsume önerileri başlatmadan önce Hello derleme işlem sona erdiğinde toocheck kullanın.
* Öneriler - Get önerileri belirli öğesi veya öğeleri listesi için kullanabilir.

Yukarıdaki tüm hello adımları hello Azure Machine Learning önerileri API'si yapılır.  Merhaba öğesinden bu adımların her biri uygulayan bir örnek uygulama indirebilirsiniz [de Galerisi.](http://1drv.ms/1xeO2F3)

## <a name="limitations"></a>Sınırlamalar
* Merhaba en büyük abonelik başına model sayısı 10'dur.
* Merhaba en fazla bir katalog tutabilir öğe sayısı 100. 000 ' dir.
* Merhaba maksimum tutulur kullanım noktaları ~ 5,000,000 sayısıdır. Yeni bir tane karşıya bildirilen veya gereken hello eski silinir.
* Merhaba en büyük boyutu (örneğin, veri içeri aktar katalog kullanım verileri İçeri Aktar) POSTASINA gönderilen veri 200 MB'tır.
* Merhaba işlem etkin olmadığından bir öneri modeli derlemesi için saniye başına sayısı olan ~ 2TPS. Etkin bir öneri modeli yapı too20TPS basılı tutabilirsiniz.

## <a name="integration"></a>Tümleştirme
### <a name="authentication"></a>Kimlik Doğrulaması
Microsoft Azure Market ya da hello temel veya OAuth kimlik doğrulama yöntemini destekler. Merhaba Market altında toohello anahtarlarında giderek hello hesabı anahtarları kolayca bulabilirsiniz [hesap ayarlarınızı](https://datamarket.azure.com/account/keys). 

#### <a name="basic-authentication"></a>Temel kimlik doğrulaması
Merhaba Authorization Üstbilgisi ekleyin:

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

TooBase64 dönüştürme (C#)

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

TooBase64 dönüştürme (JavaScript)

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a>Hizmet URI'si
hello Azure Machine Learning önerileri API'leri için Hello hizmet kök URI [burada.](https://api.datamarket.azure.com/amla/recommendations/v2/)

Merhaba tam hizmet URI'si hello OData belirtimi öğeleri kullanılarak ifade edilir.

### <a name="api-version"></a>API sürümü
Her API çağrısı, hello sonunda ayarlanmalıdır apiVersion adlı bir sorgu parametresi sahip olur "1.0" çok.

### <a name="ids-are-case-sensitive"></a>Kimlikleri büyük/küçük harfe duyarlıdır
Herhangi bir hello API ' ları tarafından döndürülen kimlikleri, büyük küçük harfe duyarlıdır ve bu nedenle sonraki API çağrıları parametre olarak geçirilen kullanılmalıdır. Örneğin, model kimlikleri ve Katalog büyük küçük harfe duyarlıdır.

### <a name="create-a-model"></a>Bir model oluşturma
"Model oluşturma" isteği oluşturma:

| HTTP yöntemi | URI |
|:--- |:--- |
| YAYINLA |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelName |Yalnızca harf (A-Z, a-z), sayılar (0-9), tireler (-) ve alt çizgi (_).<br>En fazla uzunluk: 20 |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

* `feed/entry/content/properties/id`-Hello model kimliğini içerir.
  Merhaba model kimliği büyük küçük harfe duyarlı olduğunu unutmayın.

OData XML

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


### <a name="import-catalog-data"></a>Katalog verilerini al
Aynı model birkaç katalog dosyaları toohello birkaç çağrılarla yüklerseniz, biz yalnızca hello yeni katalog öğeleri ekler. Varolan öğeleri hello özgün değerleriyle kalır.

| HTTP yöntemi | URI |
|:--- |:--- |
| YAYINLA |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Benzersiz tanımlayıcı hello modelinin (büyük küçük harfe duyarlı) |
| Dosya adı |Başlangıç kataloğu metinsel tanımlayıcısı.<br>Yalnızca harf (A-Z, a-z), sayılar (0-9), tireler (-) ve alt çizgi (_).<br>En fazla uzunluk: 50 |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |Veri Kataloğu. Biçimi:<br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th>Ad</th><th>Zorunlu</th><th>Tür</th><th>Açıklama</th></tr><tr><td>Öğe kimliği</td><td>Evet</td><td>Alfasayısal, en fazla uzunluğu 50</td><td>Bir öğeyi benzersiz tanıtıcısı</td></tr><tr><td>Öğe adı</td><td>Evet</td><td>Alfasayısal, en fazla uzunluğu 255</td><td>Öğe adı</td></tr><tr><td>Öğesi kategorisi</td><td>Evet</td><td>Alfasayısal, en fazla uzunluğu 255</td><td>Bu öğe (örneğin, pişirme Books ekranda...) ait olduğu kategoriyi toowhich</td></tr><tr><td>Açıklama</td><td>Hayır</td><td>Alfasayısal, en fazla uzunluğu 4000</td><td>Bu öğenin açıklaması</td></tr></table><br>En büyük dosya boyutu 200 MB'tır.<br><br>Örnek:<br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

**Yanıt**:

HTTP durum kodu: 200

* `Feed\entry\content\properties\LineCount`-Kabul satır sayısı.
* `Feed\entry\content\properties\ErrorCount`-Tooan hata eklenmemiş satır sayısı.

OData XML

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


### <a name="import-usage-data"></a>Kullanım verilerini alma
#### <a name="uploading-a-file"></a>Bir dosyayı karşıya yükleme
Bu bölümde gösterilmiştir nasıl dosyası kullanarak tooupload kullanım verileri. Bu API birkaç kez ile kullanım verilerini çağırabilirsiniz. Tüm kullanım verileri tüm çağrıları için kaydedilir.

| HTTP yöntemi | URI |
|:--- |:--- |
| YAYINLA |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Benzersiz tanımlayıcı hello modelinin (büyük küçük harfe duyarlı) |
| Dosya adı |Başlangıç kataloğu metinsel tanımlayıcısı.<br>Yalnızca harf (A-Z, a-z), sayılar (0-9), tireler (-) ve alt çizgi (_).<br>En fazla uzunluk: 50 |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |Kullanım verileri. Biçimi:<br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th>Ad</th><th>Zorunlu</th><th>Tür</th><th>Açıklama</th></tr><tr><td>Kullanıcı Kimliği</td><td>Evet</td><td>Alfasayısal</td><td>Bir kullanıcının benzersiz tanıtıcısı</td></tr><tr><td>Öğe kimliği</td><td>Evet</td><td>Alfasayısal, en fazla uzunluğu 50</td><td>Bir öğeyi benzersiz tanıtıcısı</td></tr><tr><td>Zaman</td><td>Hayır</td><td>Tarih biçiminde: YYYY/AA/ddTHH (örneğin, 2013/06/20T10:00:00)</td><td>Veri saati</td></tr><tr><td>Olay</td><td>Sağlanan daha sonra tarih de konulmalıdır yok</td><td>Merhaba aşağıdakilerden biri:<br>• Tıklatın<br>• RecommendationClick<br>• AddShopCart<br>• RemoveShopCart<br>• Satın alma</td><td></td></tr></table><br>En büyük dosya boyutu 200 MB'tır.<br><br>Örnek:<br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

**Yanıt**:

HTTP durum kodu: 200

* `Feed\entry\content\properties\LineCount`-Kabul satır sayısı.
* `Feed\entry\content\properties\ErrorCount`-Tooan hata eklenmemiş satır sayısı.
* `Feed\entry\content\properties\FileId`-Dosya tanımlayıcısı.

OData XML

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


#### <a name="using-data-acquisition"></a>Veri alma kullanma
Bu bölüm, gerçek toosend olayları tooAzure Machine Learning önerileri, genellikle Web sitenizi nasıl zaman gösterir.

| HTTP yöntemi | URI |
|:--- |:--- |
| YAYINLA |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| İstek gövdesi |Olay veri girişi toosend istediğiniz her olay için. Merhaba aynı kullanıcı veya tarayıcı oturumunu hello için aynı kimliği hello SessionID alanında göndermesi gerekir. (Olay gövdesi aşağıdaki örneği bakın.) |

* Olay 'Tıklatın' Örneğin:
  
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
* Olay 'RecommendationClick' Örneğin:
  
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
* Olay 'AddShopCart' Örneğin:
  
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
* Olay 'RemoveShopCart' Örneğin:
  
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
* Olay 'Satınalma' Örneğin:
  
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
* Örnek 2 olayları, 'Düğmesini tıklatarak' ve 'AddShopCart' gönderme:
  
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

**Yanıt**: HTTP durum kodu: 200

### <a name="build-a-recommendation-model"></a>Bir öneri model oluşturma
| HTTP yöntemi | URI |
|:--- |:--- |
| YAYINLA |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Benzersiz tanımlayıcı hello modelinin (büyük küçük harfe duyarlı) |
| userDescription |Başlangıç kataloğu metinsel tanımlayıcısı. Boşluklar kullanırsanız, % 20 yerine kodlamak gerekir olduğunu unutmayın. Yukarıdaki örnekte bkz.<br>En fazla uzunluk: 50 |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

Bu zaman uyumsuz bir API'dir. Yanıt olarak bir yapı kimliği alırsınız. Merhaba derleme sona erdiğinde tooknow hello "Get derlemeler durumu bir modelin" API çağrısı ve gerekir bulun hello yanıtta bu derleme kimliği. Bir yapı dakika toohours hello hello verilerin boyutuna bağlı olarak gelen alabileceğine dikkat edin.

Merhaba yapı kadar sona erer önerileri kullanamayacaklarını.

Geçerli yapı durumu:

* Oluştur – modeli oluşturuldu.
* Sıraya – modeli yapı tetiklendi ve kuyruğa alınır.
* Yapı – modeli oluşturuluyor.
* Başarılı – yapı başarılı bir şekilde sona erdi.
* Hata – derleme bir hata ile sona erdi.
* İptal – derleme iptal edildi.
* İptal etme – yapı iptal edilir.

Kimliği yolu izleyerek hello altında bulunabilir bu hello yapı dikkat edin:`Feed\entry\content\properties\Id`

OData XML

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

### <a name="get-build-status-of-a-model"></a>Bir modelin yapı durumunu Al
| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Benzersiz tanımlayıcı hello modelinin (büyük küçük harfe duyarlı) |
| onlyLastBuild |Gösteren tüm hello tooreturn hello modeli geçmişini ya da hello en son yapı yalnızca hello durumunu derleme. |
| apiVersion |1.0 |

**Yanıt**:

HTTP durum kodu: 200

Merhaba yanıt yapı her bir giriş içerir. Her giriş verileri aşağıdaki hello sahiptir:

* `feed/entry/content/properties/UserName`– Hello kullanıcı adı.
* `feed/entry/content/properties/ModelName`– Hello model adı.
* `feed/entry/content/properties/ModelId`– Model benzersiz tanımlayıcısı.
* `feed/entry/content/properties/IsDeployed`– Merhaba yapı (paketini dağıtılan olup olmadığı Etkin yapı).
* `feed/entry/content/properties/BuildId`– Benzersiz tanımlayıcısı oluşturun.
* `feed/entry/content/properties/BuildType`-Hello yapı türü.
* `feed/entry/content/properties/Status`– Oluşturma durumu. Merhaba aşağıdakilerden biri olabilir: hata, yapı, sıraya alınan, iptal etme, iptal edildi, başarılı
* `feed/entry/content/properties/StatusMessage`– Ayrıntılı durum iletisi (yalnızca toospecific durumlar geçerlidir).
* `feed/entry/content/properties/Progress`– İlerleme durumu (%) oluşturun.
* `feed/entry/content/properties/StartTime`– Yapı Başlama zamanı.
* `feed/entry/content/properties/EndTime`– Bitiş saati oluşturun.
* `feed/entry/content/properties/ExecutionTime`– Yapı süresi.
* `feed/entry/content/properties/ProgressStep`– Devam eden bir derleme hello geçerli aşaması hakkında ayrıntılar.

Geçerli yapı durumu:

* Oluşturulan – yapı isteği girdisi oluşturuldu.
* Sıraya – oluşturma isteği tetiklendi ve kuyruğa alınır.
* Yapı – derleme işlemi devam ediyor.
* Başarılı – yapı başarılı bir şekilde sona erdi.
* Hata – derleme bir hata ile sona erdi.
* İptal – derleme iptal edildi.
* İptal etme – yapı iptal edilir.

Derleme türü için geçerli değerler:

* RANK - derece oluşturun. (Ayrıntıları rank için yapı görüntülenirken hata oluştu, lütfen toohello "Machine Learning öneri API belgelerine" Belge bakın.)
* Öneri - öneri derleme.
* Fbt - sık satın birlikte derleme.

OData XML

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


### <a name="get-recommendations"></a>Öneriler alın
| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Benzersiz tanımlayıcı hello modelinin (büyük küçük harfe duyarlı) |
| öğe kimliklerinin |Merhaba öğeleri toorecommend için virgülle ayrılmış listesi.<br>En fazla uzunluk: 1024 |
| numberOfResults |Gerekli sonuç sayısı |
| includeMetatadata |Gelecekte kullanmak, her zaman yanlış |
| apiVersion |1.0 |

**Yanıtı:**

HTTP durum kodu: 200

Merhaba yanıt önerilen öğe başına bir giriş içerir. Her giriş verileri aşağıdaki hello sahiptir:

* `Feed\entry\content\properties\Id`-Önerilen öğesi kimliği
* `Feed\entry\content\properties\Name`-Hello öğesinin adı.
* `Feed\entry\content\properties\Rating`-Hello öneri derecesi; daha yüksek numarası, daha yüksek güvenilirlik anlamına gelir.
* `Feed\entry\content\properties\Reasoning`-Öneri mantığı (örneğin, öneri açıklamaları).

OData XML

Aşağıdaki örnek yanıt Hello 10 önerilen öğeleri içerir:

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

### <a name="update-model"></a>Bir güncelleştirme modeli
Merhaba modeli güncelleştirmesi ya da etkin yapı kimliği hello
*Etkin yapı kimliği* -her derleme her model için bir yapı kimliği vardır. Merhaba etkin yapı kimliği hello ilk başarılı her yeni modelinin yapıdır. Bir etkin yapı Kimliğine sahip ve ek derlemeler hello için bunu bir kez aynı modelin ihtiyacınız tooexplicitly ayarlayın, bu, hello varsayılan derleme gibi kimliği istiyorsanız. Ne zaman toouse, bir otomatik olarak kullanılacak hello varsayılan istediğiniz hello derleme kimliği belirtmezseniz, öneriler, tüketir.

Üretim - toobuild yeni modelleri öneri modeline sahiptir ve bunları yükseltmeden önce bunları tooproduction test sonra bu düzenek - sağlar.

| HTTP yöntemi | URI |
|:--- |:--- |
| PUT |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| id |Benzersiz tanımlayıcı hello modelinin (büyük küçük harfe duyarlı) |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br>Merhaba XML açıklama etiketleri ve ActiveBuildId isteğe bağlı olduğunu unutmayın. Açıklama veya ActiveBuildId tooset istemiyorsanız hello tüm etiket kaldırın. |

**Yanıt**:

HTTP durum kodu: 200

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a>Yasal Bilgiler
Bu belgede sağlanan "olarak-olan". URL ve diğer Internet Web sitesi başvuruları dahil olmak üzere bu belgede belirtilen bilgiler ve görüntüler bildirim yapılmadan değiştirilebilir. Burada açıklanan bazı örnekler yalnızca çizim için sağlanmıştır ve kurgusaldır. Gerçek bir ilişki veya bağlantı amaçlanmamıştır veya çıkarılmamalıdır. Bu belge, herhangi bir yasal hak ile herhangi bir Microsoft ürünü üzerinde tooany fikri mülkiyet sağlamaz. Kopyalayabilir ve bu belgeyi şirket içinde kullanmak başvuru amaçlıdır. © 2014 Microsoft. Tüm hakları saklıdır. 

