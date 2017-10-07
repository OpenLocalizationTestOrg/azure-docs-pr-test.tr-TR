---
title: "aaaMachine öğrenme önerileri API belgeleri | Microsoft Docs"
description: "Azure Machine Learning önerileri API'si belgeleri önerileri altyapısının hello Microsoft Azure Market kullanılabilir."
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 32c3ab2f-fdd7-48cc-b501-ad55c79b87dc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: LuisCa
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d1cec228bf23870c05c8ab8df2779b0c3c65b06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a>Azure Machine Learning Öneri API’si Belgeleri
> [!NOTE]
> Merhaba önerileri API Bilişsel hizmeti yerine bu sürümünü kullanarak başlamanız gerekir. Merhaba önerileri Bilişsel hizmet bu hizmeti koyacağınız ve tüm hello yeni özellikler vardır geliştirilmiştir. Toplu işlem desteği, daha iyi API'si Gezgini, bir temizleyici API yüzeyi, daha tutarlı kaydolma/faturalandırma deneyimi, vb. gibi yeni özellikler vardır.
> Daha fazla bilgi edinmek [geçiş toohello yeni Bilişsel hizmeti](http://aka.ms/recomigrate)
> 
> 

Bu belgede, Microsoft Azure Machine Learning önerileri API'leri gösterir.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1. Genel bir bakış
Bu belge, bir API Başvurusu değil. "Azure Machine Learning öneri – Hızlı Başlat" Merhaba belgeyle başlamanız gerekir.

Hello Azure Machine Learning önerileri API'si mantıksal gruplar aşağıdaki hello ayrılabilir:

* <ins>Sınırlamalar</ins> -önerileri API sınırlamaları.
* <ins>Genel bilgiler</ins> -kimlik doğrulaması hakkında bilgi hizmet URI'si ve sürüm oluşturma.
* <ins>Model Basic</ins> -toodo hello temel işlemleri modeli sağlayan API (örneğin oluşturma, güncelleştirme ve bir modeli silme).
* <ins>Model Gelişmiş</ins> -hello model üzerinde Gelişmiş tooget veri ınsights'ı etkinleştir API'leri.
* <ins>Model iş kuralları</ins> -toomanage iş kuralları hello modeli öneri sonuçlarını sağlayan API.
* <ins>Katalog</ins> -toodo temel işlemleri modeli katalogunda sağlayan API. Bir katalog hello Kullanım verilerinin hello öğelerde meta veri bilgileri içerir.
* <ins>Özellik</ins> -tooget Öngörüler öğede hello kataloğuna sağlayan API ve nasıl toouse bu bilgileri toobuild daha iyi öneriler.
* <ins>Kullanım verileri</ins> -toodo temel işlemleri hello modeli kullanım verilerini sağlayan API. Kullanım verileri hello temel formda çiftlerini &#60; UserID &#62; içeren satırları oluşur, &#60; ItemId &#62;.
* <ins>Yapı</ins> - bir model tootrigger sağlayan API yapı ve ilgili toothis temel işlemleri oluşturun. Değerli kullanım verileri bulduktan sonra model yapı tetikleyebilir.
* <ins>Öneri</ins> -hello derleme bir modelin sona erince tooconsume öneriler sağlayan API.
* <ins>Kullanıcı verilerini</ins> -hello kullanıcı kullanım verilerini toofetch bilgi sağlayan API.
* <ins>Bildirimleri</ins> -tooyour API işlemleri ilgili sorunları tooreceive bildirimlerini sağlayan API'ler. (Örneğin, kullanım verilerini veri alımı ve hello olayları işleme testlerden çoğunu aracılığıyla bildirdiğiniz. Bir hata bildirimi gerçekleştirilecektir.)

## <a name="2-limitations"></a>2. Sınırlamalar
* Merhaba en büyük abonelik başına model sayısı 10'dur.
* Merhaba derlemeleri modeli başına en fazla 20'dir.
* Merhaba en fazla bir katalog tutabilir öğe sayısı 100. 000 ' dir.
* Merhaba maksimum tutulur kullanım noktaları ~ 5,000,000 sayısıdır. Yeni bir tane karşıya bildirilen veya gereken hello eski silinir.
* Merhaba en büyük boyutu (örn. içeri aktarma katalog verilerini, kullanım verileri İçeri Aktar) POSTASINA gönderilen veri 200 MB'tır.
* Merhaba maksimum öneriler alınırken 150 olduğunda için sorulan öğe sayısı.

## <a name="3-apis---general-information"></a>3. API - genel bilgiler
### <a name="31-authentication"></a>3.1. Kimlik Doğrulaması
Lütfen kimlik doğrulaması ile ilgili hello Microsoft Azure Market yönergeleri izleyin. Merhaba Market ya da hello temel veya OAuth kimlik doğrulama yöntemini destekler.

### <a name="32-service-uri"></a>3.2. Hizmet URI'si
hello Azure Machine Learning önerileri API'leri için Hello hizmet kök URI [burada.](https://api.datamarket.azure.com/amla/recommendations/v3/)

Merhaba tam hizmet URI'si hello OData belirtimi öğeleri kullanılarak ifade edilir.  

### <a name="33-api-version"></a>3.3. API sürümü
Her API çağrısı, hello sonunda too1.0 ayarlanmalıdır apiVersion adlı bir sorgu parametresi sahip olur.

### <a name="34-ids-are-case-sensitive"></a>3.4. Kimlikleri büyük küçük harf duyarlıdır
Herhangi bir hello API ' ları tarafından döndürülen kimlikleri, büyük/küçük harfe duyarlıdır ve bu nedenle sonraki API çağrıları parametre olarak geçirilen kullanılmalıdır. Örneğin, model kimlikleri ve Katalog büyük küçük harfe duyarlı.

## <a name="4-recommendations-quality-and-cold-items"></a>4. Öneriler kalite ve soğuk öğeleri
### <a name="41-recommendation-quality"></a>4.1. Öneri kalitesi
Öneri model oluşturma genellikle yeterli tooallow hello sistem tooprovide önerileri olur. Bununla birlikte, öneri kalitesini işlenen hello kullanıma göre değişir ve hello katalog kapsamını hello. Örneğin çok soğuk öğelerinin (öğeleri önemli kullanım olmadan) varsa, bu tür bir öğe için bir öneri sağlama veya böyle bir öğe önerilen bir kullanarak sorunlar hello sistem olacaktır. Sipariş tooovercome hello soğuk öğesi sorunda hello sistem hello öğeleri tooenhance hello önerileri meta verileri hello kullanılmasına izin verir. Bu meta veriler başvurulan tooas özellik gibidir. Bir kitaptaki yazar veya bir film aktör Bunun tipik özellikleridir. Özellikler anahtar/değer dizeleri hello biçiminde hello katalog aracılığıyla sağlanır. Merhaba tam biçim hello katalog dosyası için lütfen toohello bakın [alma katalog bölümü](#81-import-catalog-data). 

### <a name="42-rank-build"></a>4.2. RANK derleme
Özellikleri hello öneri modeli artırabilir, ancak toodo şekilde anlamlı özellikleri hello kullanımını gerektirir. Yeni bir yapı tanıtılan - bu amaç için bir sıra oluşturun. Bu yapı özellikleri hello yararlılığı rank. Anlamlı bir özellik, bir sıra puan 2 ve yedekleme ile bir özelliktir.
Merhaba özelliklerinin anlamlı olan anlama sonra anlamlı özelliklerinin hello listesi (veya alt liste) içeren bir öneri yapı tetikler. Bunlar için hello geliştirme soğuk öğeleri ve yarı öğelerinin özellik olası toouse olur. Bunları sıcak öğeleri için sipariş toouse hello `UseFeatureInModel` yapı parametresi ayarlanmalıdır. Soğuk öğeleri için sipariş toouse özellikleri hello `AllowColdItemPlacement` yapı parametresi etkinleştirilmesi gerekir.
Not: Bu olası tooenable değil `AllowColdItemPlacement` etkinleştirmeden `UseFeatureInModel`.

### <a name="43-recommendation-reasoning"></a>4.3. Öneri mantığı
Öneri mantığı özellik kullanımı başka bir yönüdür. Aslında, hello Azure Machine Learning önerileri altyapısı özellikleri tooprovide öneri açıklamaları (paketini kullanabilirsiniz akıl), toomore güvenirlik hello öndeki öğe hello öneri tüketiciden önerilir.
tooenable, hello akıl `AllowFeatureCorrelation` ve `ReasoningFeatureList` parametreleri Kurulum önceki toorequesting bir öneri yapı olması gerekir.

## <a name="5-model-basic"></a>5. Temel modeli
### <a name="51-create-model"></a>5.1. Model oluşturma
"Model oluşturma" isteği oluşturur.

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
  **Not**: model kimliği büyük küçük harfe duyarlı.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="52-get-model"></a>5.2. Model alma
"Get modeli" isteği oluşturur.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br>Örnek:<br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| id |Benzersiz tanımlayıcı hello modelinin (büyük küçük harf duyarlı) |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

Merhaba model veri öğeleri aşağıdaki hello altında bulunabilir:

* `feed/entry/content/properties/Id`-Model benzersiz kimliği
* `feed/entry/content/properties/Name`-Model adı.
* `feed/entry/content/properties/Date`-Model oluşturulma tarihi.
* `feed/entry/content/properties/Status`-Model durumu. Merhaba aşağıdakilerden biri:
  * Oluşturulan - modeli oluşturulur ve Katalog ve kullanım içermiyor.
  * ReadyForBuild - Model oluşturulur ve Katalog ve kullanım içerir.
* `feed/entry/content/properties/HasActiveBuild`-Hello model başarıyla yerleşik gösterir.
* `feed/entry/content/properties/BuildId`-Model etkin yapı kimliği
* `feed/entry/content/properties/Mpr`-Model ortalama yüzdebirlik Derecelendirme (MPR - ModelInsight daha fazla bilgi için bkz.).
* `feed/entry/content/properties/UserName`-Model iç kullanıcı adı.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get A List Of All Models</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T14:35:51Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
        <d:Name m:type="Edm.String">vah-11111</d:Name>
        <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
        <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
        <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
        <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
        <d:Description m:type="Edm.String">short description</d:Description>
        <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="53----get-all-models"></a>5.3.    Tüm modelleri Al
Merhaba geçerli kullanıcının tüm modelleri alır.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br>Örnek:<br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

* `feed/entry/content/properties/Id`-Model benzersiz kimliği
* `feed/entry/content/properties/Name`-Model adı.
* `feed/entry/content/properties/Date`-Model oluşturulma tarihi.
* `feed/entry/content/properties/Status`-Model durumu. Merhaba aşağıdakilerden biri:
  * Oluşturulan - modeli oluşturulur ve Katalog ve kullanım içermiyor.
  * ReadyForBuild - Model oluşturulur ve Katalog ve kullanım içerir.
* `feed/entry/content/properties/HasActiveBuild`-Hello model başarıyla yerleşik gösterir.
* `feed/entry/content/properties/BuildId`-Model etkin yapı kimliği
* `feed/entry/content/properties/Mpr`-Model MPR (daha fazla bilgi için bkz: ModelInsight).
* `feed/entry/content/properties/UserName`-Model iç kullanıcı adı.
* `feed/entry/content/properties/UsageFileNames`-Model kullanım dosyalar virgülle ayrılmış listesi.
* `feed/entry/content/properties/CatalogId`-Model katalog kimliği
* `feed/entry/content/properties/Description`-Model açıklaması.
* `feed/entry/content/properties/CatalogFileName`-Model katalog dosyası adı.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get A List Of All Models</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-28T14:35:51Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
                    <d:Name m:type="Edm.String">vah-11111</d:Name>
                    <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
                    <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
                    <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
                    <d:BuildId m:type="Edm.String">-1</d:BuildId>
                    <d:Mpr m:type="Edm.String">0</d:Mpr>
                    <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
                    <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
                    <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
                    <d:Description m:type="Edm.String">short description</d:Description>
                    <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="54----update-model"></a>5.4.    Bir güncelleştirme modeli
Merhaba modeli güncelleştirmesi ya da etkin yapı kimliği hello<br>
<ins>Etkin yapı kimliği</ins> -her derleme her model için bir yapı kimliği vardır. Merhaba etkin yapı kimliği hello ilk başarılı her yeni modelinin yapıdır. Bir etkin yapı Kimliğine sahip ve ek derlemeler hello için bunu bir kez aynı modelin ihtiyacınız tooexplicitly ayarlayın, bu, hello varsayılan derleme gibi kimliği istiyorsanız. Ne zaman toouse, bir otomatik olarak kullanılacak hello varsayılan istediğiniz hello derleme kimliği belirtmezseniz, öneriler, tüketir.<br>
Üretim - toobuild yeni modelleri öneri modeline sahiptir ve bunları yükseltmeden önce bunları tooproduction test sonra bu düzenek - sağlar.

| HTTP yöntemi | URI |
|:--- |:--- |
| PUT |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br>Örnek:<br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| id |Benzersiz tanımlayıcı hello modelinin (büyük küçük harf duyarlı) |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br>Merhaba XML açıklama etiketleri ve ActiveBuildId isteğe bağlı olduğunu unutmayın. Açıklama veya ActiveBuildId tooset istemiyorsanız hello tüm etiket kaldırın. |

**Yanıt**:

HTTP durum kodu: 200

### <a name="55----delete-model"></a>5.5.    Model Sil
Kimliğe göre var olan bir model siler

| HTTP yöntemi | URI |
|:--- |:--- |
| SİL |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br>Örnek:<br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| id |Benzersiz tanımlayıcı hello modelinin (büyük küçük harf duyarlı) |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Delete Model by Id</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T10:39:33Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">DeleteModelByIdEntity</title>
    <updated>2014-10-28T10:39:33Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:string m:type="Edm.String"></d:string>
      </m:properties>
    </content>
      </entry>
    </feed>

## <a name="6-model-advanced"></a>6. Gelişmiş modeli
### <a name="61----model-data-insight"></a>6.1.    Model veri öngörüleri
İstatistik bilgileri, bu model ile oluşturulmuş hello kullanım verilerini döndürür.

Yalnızca öneri derleme için kullanılabilir.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>Örnek:<br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

Merhaba veri özellikleri koleksiyonu döndürülür.

* `feed/entry/id/content/properties/key`-Hello özellik adı tutar.
* `feed/entry/id/content/properties/value`-Başlangıç özellik değeri tutar.

Merhaba tabloda her anahtar temsil eden hello değeri gösterir.

| Anahtar | Açıklama |
|:--- |:--- |
| AvgItemLength |Her öğe ayrı kullanıcıların ortalama sayısı. |
| AvgUserLength |Kullanıcı başına farklı öğelerin ortalama sayısı. |
| DensificationNumberOfItems |Modelled olamaz ayıklama öğeleri sonra öğe sayısı. |
| DensificationNumberOfUsers |Ayıklama kullanıcılar ve modelled olamaz öğeler sonra kullanım sayısını gösterir. |
| DensificationNumberOfRecords |Ayıklama kullanıcılar ve modelled olamaz öğeler sonra kullanım sayısını gösterir. |
| MaxItemLength |Merhaba en popüler öğesi için benzersiz kullanıcı sayısı. |
| MaxUserLength |Bir kullanıcı için farklı öğe sayısı üst sınırından. |
| MinItemLength |Bir öğe için benzersiz kullanıcı sayısı üst sınırından. |
| MinUserLength |En az bir kullanıcı için farklı öğe sayısı. |
| RawNumberOfItems |Merhaba kullanım dosyalar öğelerin sayısı. |
| RawNumberOfUsers |Tüm ayıklama önce kullanım noktalarını sayısı. |
| RawNumberOfRecords |Tüm ayıklama önce kullanım noktalarını sayısı. |
| SamplingNumberOfItems |Yok |
| SamplingNumberOfRecords |Yok |
| SamplingNumberOfUsers |Yok |

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get data insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgItemLength</d:Key>
        <d:Value m:type="Edm.String">18.936</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgUserLength</d:Key>
        <d:Value m:type="Edm.String">51.879</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfItems</d:Key>
        <d:Value m:type="Edm.String">2,000</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfRecords</d:Key>
        <d:Value m:type="Edm.String">37,872</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
        <m:properties>
            <d:Key m:type="Edm.String">DensificationNumberOfUsers</d:Key>
            <d:Value m:type="Edm.String">730</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxItemLength</d:Key>
                <d:Value m:type="Edm.String">4,704</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxUserLength</d:Key>
                <d:Value m:type="Edm.String">190</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinItemLength</d:Key>
                <d:Value m:type="Edm.String">8</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinUserLength</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="62----model-insight"></a>6.2.    Model Insight
Döndürür model Insight hello etkin yapı üzerinde veya (belirtilmişse) belirli bir yapı üzerinde.

Yalnızca öneri derleme için kullanılabilir.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |Etkin yapı Kimliğine sahip:<br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br>Özel derleme Kimliğine sahip:<br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| Buildıd |İsteğe bağlı - başarılı bir yapı tanımlayan bir numara. |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

Merhaba veri özellikleri koleksiyonu döndürülür.

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

Merhaba tabloda her anahtar temsil eden hello değeri gösterir.

| Anahtar | Açıklama |
|:--- |:--- |
| CatalogCoverage |Başlangıç kataloğu hangi kısmının ile kullanım desenlerini modelled. Merhaba rest hello öğelerinin içerik tabanlı özellikleri gerekir. |
| Mpr |Merhaba modeli yüzdebirlik sıralamasını anlamına gelir. Daha düşük daha iyidir. |
| NumberOfDimensions |Merhaba matris factorization algoritması tarafından kullanılan dimensions sayısı. |

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get model insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">CatalogCoverage</d:Key>
                <d:Value m:type="Edm.String">1.000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">Mpr</d:Key>
                <d:Value m:type="Edm.String">0.367</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">NumberOfDimensions</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="63----get-model-sample"></a>6.3.    Model örnek alma
Merhaba öneri model örneği alır.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>Örnek:<br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br>Özel derleme Kimliğine sahip:<br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br>Örnek:<br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

OData XML

Yanıt ham metin biçiminde verilir:

<pre>
Level 1
---------------
655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel
    655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel Rating: 0.5215
    3f471802-f84f-44a0-99c8-6d2e7418eec1, Black Hawk Down: A Story of Modern War Rating: 0.5151
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5148
    6afc18e4-8c2a-43d1-9021-57543d6b11d8, Imajica Rating: 0.5146
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.514
56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai
    56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai Rating: 0.5218
    53156702-cc0c-443d-b718-6fb74b2491d3, Son of \ Rating: 0.5212
    fb8cf7a6-8719-46ee-97d4-92f931d77a3a, Smoke and Mirrors: Short Fictions and Illusions Rating: 0.5188
    8f5fe006-79e4-4679-816b-950989d1db4b, A Place I've Never Been (Contemporary American Fiction) Rating: 0.5156
    d8db4583-cc0f-49ce-bc95-b7fa3491623f, Happiness: A Novel Rating: 0.5156
50471eec-9aeb-4900-84d7-21567ab18546, If hello Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of hello Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on hello Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in hello Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, hello Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On hello Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, hello Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories tooTell in hello Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, hello Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic hello Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in hello Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, hello Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, hello X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell hello President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In hello Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, hello Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of hello Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, hello Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in hello Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (hello Official Guide toohello X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, hello Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, hello Truth Is Out There (hello Official Guide toohello X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, hello Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of hello Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where hello Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, hello God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (hello Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in hello Time of Cholera (Penguin Great Books of hello 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, hello Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories tooTell In hello Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from hello Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a>7. Model iş kuralları
Bu, desteklenen kuralları hello türleri şunlardır:

* <strong>Engelleme</strong> -engelleme tooprovide hello öneri sonuçlarında tooreturn istiyor musunuz öğelerinin bir listesini sağlar. 
* <strong>FeatureBlockList</strong> -özelliğini engelleme özelliklerinin hello değerlerine göre tooblock öğeleri sağlar.

*1000'den fazla öğe tek engelleme kuralında gönderme veya aramanız zaman aşımı olabilir. 1000'den fazla öğe tooblock gerekiyorsa, birkaç engelleme çağrıları yapabilirsiniz.*

* <strong>Upsale</strong> -Upsale tooenforce öğeleri tooreturn hello öneri sonuçlarında sağlar.
* <strong>Beyaz liste</strong> -beyaz liste etkinleştirir, tooonly öğelerin listesini önerileri öneririz.
* <strong>FeatureWhiteList</strong> -özellik beyaz listesi belirli özellik değerlerine sahip tooonly öneri öğeleri sağlar.
* <strong>PerSeedBlockList</strong> - çekirdek engelleme listesi etkinleştirir, tooprovide her bir öneri sonuçları olarak döndürülen öğe listesi öğesi başına.

### <a name="71----get-model-rules"></a>7.1.    Modeli kuralları Al
| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>Örnek:<br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

* `feed/entry/content/properties/Id`-Bu kural benzersiz tanımlayıcısı.
* `feed/entry/content/properties/Type`-Hello kural türü.
* `feed/entry/content/properties/Parameter`-Kural parametresi.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get a list of rules for a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T12:58:57Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000043</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1000"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000044</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1001"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="72----add-rule"></a>7.2.    Kural Ekle
| HTTP yöntemi | URI |
|:--- |:--- |
| YAYINLA |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| ÜSTBİLGİ |`"Content-Type", "text/xml"` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi | |

<ins>Öğesi kimlikleri için iş kuralları sağlayan her emin toouse hello hello öğesinin dış kimliği yapın (Merhaba katalog dosyasında kullanılan aynı kimliği hello)</ins><br>
<ins>tooadd engelleme kuralı:</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><ins>
<ins>tooadd FeatureBlockList kural:</ins><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><ins>tooadd bir Upsale kuralı:</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br>
<ins>tooadd bir beyaz liste kural:</ins><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><ins>
<ins>tooadd FeatureWhiteList kural:</ins><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><ins>tooadd PerSeedBlockList kural:</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

**Yanıt**:

HTTP durum kodu: 200

Merhaba API Yeni kuralın ayrıntılarını ile oluşturulan hello döndürür. Merhaba kuralları özellik yolları aşağıdaki hello alınabilir:

* `feed/entry/content/properties/Id`-Bu kural benzersiz tanımlayıcısı.
* `feed/entry/content/properties/Type`-Hello kural türü: engelleme veya Upsale.
* `feed/entry/content/properties/Parameter`-Kural parametresi.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Add A Rule</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T11:13:28Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AddARuleEntity</title>
        <updated>2014-11-05T11:13:28Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000041</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1002"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="73----delete-rule"></a>7.3.    Kural silme
| HTTP yöntemi | URI |
|:--- |:--- |
| SİL |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| filterId |Merhaba filtre benzersiz tanıtıcısı |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

### <a name="74----delete-all-rules"></a>7.4.    Tüm kuralları Sil
| HTTP yöntemi | URI |
|:--- |:--- |
| SİL |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

## <a name="8-catalog"></a>8. Katalog
### <a name="81----import-catalog-data"></a>8.1.    Katalog verileri içeri aktar
Aynı model birkaç katalog dosyaları toohello birkaç çağrılarla yüklerseniz, biz yalnızca hello yeni katalog öğeleri ekler. Varolan öğeleri hello özgün değerleriyle kalır. Bu yöntemi kullanarak katalog verilerini güncelleştirilemiyor.

başlangıç kataloğu veri biçimini izleyen hello izlemelidir:

* Özellikleri-`<Item Id>,<Item Name>,<Item Category>[,<Description>]`
* İle özellikleri-`<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`

Not: hello en büyük dosya boyutu 200 MB'tır.

** Ayrıntıları Biçimlendir **

| Ad | Zorunlu | Tür | Açıklama |
|:--- |:--- |:--- |:--- |
| Öğe kimliği |Evet |[A-z], [a-z], [0-9], [_] &#40; Alt çizgi &#41; [-] &#40; çizgi &#41;<br> En fazla uzunluk: 50 |Bir öğeyi benzersiz tanımlayıcısı. |
| Öğe adı |Evet |Herhangi bir alfasayısal karakter<br> En fazla uzunluk: 255 |Öğe adı. |
| Öğesi kategorisi |Evet |Herhangi bir alfasayısal karakter <br> En fazla uzunluk: 255 |Kategori toowhich bu öğenin ait olduğu (örneğin pişirme kitapları, ekranda...); boş olabilir. |
| Açıklama |Hayır, özellikleri olmadıkça var (ancak boş olabilir) |Herhangi bir alfasayısal karakter <br> En fazla uzunluk: 4000 |Bu öğenin açıklaması. |
| Özellikler listesi |Hayır |Herhangi bir alfasayısal karakter <br> En fazla uzunluk: 4000; Özellikler: 20 sayısı üst sınırı |Özellik adı virgülle ayrılmış listesini = kullanılan tooenhance modeli öneri; olabilir özellik değeri bkz: [konuları Gelişmiş](#2-advanced-topics) bölümü. |

| HTTP yöntemi | URI |
|:--- |:--- |
| YAYINLA |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| ÜSTBİLGİ |`"Content-Type", "text/xml"` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| Dosya adı |Başlangıç kataloğu metinsel tanımlayıcısı.<br>Yalnızca harf (A-Z, a-z), sayılar (0-9), tireler (-) ve alt çizgi (_).<br>En fazla uzunluk: 50 |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |Örnek (özelliklerle ile):<br/>Clara Callan, kitap hello kitap açıklama 2406e770-769c-4189-89de-1c9283f93a96, yazar Richard Erikli = yayımcı Harper Flamingo Kanada = yıl 2001 =<br>21bf8088-b6c0-4509-870c-e1c7ac78304a, hello Forgetting yer: A kurgu (Byzantium defteri), kitap,, yazar Nick Bantock = yayımcı Harpercollins, = yıl 1997 =<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23, Spadework, kitap,, yazar Attila Findley = yayımcı HarperFlamingo Kanada = yıl 2001 =<br>552a1940-21e4-4399-82bb-594b46d7ed54, Restraint, hayvanlar, kitap, hello kitap açıklama Yazar Magnus değirmenler = yayımcı Arcade yayımlama = yıl 1998 =</pre> |

**Yanıt**:

HTTP durum kodu: 200

Merhaba API hello alma raporunu döndürür.

* `feed\entry\content\properties\LineCount`-Kabul satır sayısı.
* `feed\entry\content\properties\ErrorCount`-Tooan hata eklenmemiş satır sayısı.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Import catalog file</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
    <entry>
       <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ImportCatalogFileEntity2</title>
        <updated>2014-10-05T06:58:04Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:LineCount m:type="Edm.String">4</d:LineCount>
                <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="82----get-catalog"></a>8.2.    Katalog alma
Tüm katalog öğelerini alır.
başlangıç kataloğu olacaktır aynı anda bir sayfa alınır. Belirli dizinindeki tooget öğe istiyorsanız hello $skip odata parametresini kullanabilirsiniz. Örneğin, 100 konumdan başlayarak tooget öğe istiyorsanız, hello parametre $skip ekleme = 100 toohello istek.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

Merhaba yanıt katalog öğesi her bir giriş içerir. Her giriş verileri aşağıdaki hello sahiptir:

* `feed/entry/content/properties/ExternalId`-Katalog öğesi dış kimliği, bir hello müşteri tarafından sağlanan hello.
* `feed/entry/content/properties/InternalId`-Katalog öğesi iç kimliği, Azure Machine Learning önerileri oluşturan bir hello.
* `feed/entry/content/properties/Name`-Katalog öğesi adı.
* `feed/entry/content/properties/Category`-Katalog öğesi kategorisi.
* `feed/entry/content/properties/Description`-Katalog öğesi açıklaması.
* `feed/entry/content/properties/Metadata`-Öğe meta verisi katalog.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get All Catalog Items</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">552A1940-21E4-4399-82BB-594B46D7ED54</d:ExternalId>
                <d:InternalId m:type="Edm.String">060db26a-e6a6-464e-bb52-436d2da82a50</d:InternalId>
                <d:Name m:type="Edm.String">Restraint of Beasts</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:ExternalId>
                <d:InternalId m:type="Edm.String">209d7bfe-2eb9-4455-92a3-7c867a41a74a</d:InternalId>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">3BB5CB44-D143-4BDD-A55C-443964BF4B23</d:ExternalId>
                <d:InternalId m:type="Edm.String">913ff79b-059b-4d4d-8042-6fa4cc1391dd</d:InternalId>
                <d:Name m:type="Edm.String">Spadework</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">21BF8088-B6C0-4509-870C-E1C7AC78304A</d:ExternalId>
                <d:InternalId m:type="Edm.String">ea65e4fa-768c-40b4-92c3-69d3e8178691</d:InternalId>
                <d:Name m:type="Edm.String">hello Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a>8.3.    Katalog öğeleri belirteci göre alma
| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| Belirteç |Belirteç hello katalog öğesi'nin adı. En az 3 karakter içermelidir. |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

Merhaba yanıt katalog öğesi her bir giriş içerir. Her giriş verileri aşağıdaki hello sahiptir:

* `feed/entry/content/properties/InternalId`-Katalog öğesi iç kimliği, Azure Machine Learning önerileri oluşturan bir hello.
* `feed/entry/content/properties/Name`-Katalog öğesi adı.
* `feed/entry/content/properties/Rating`-(gelecekte kullanmak için)
* `feed/entry/content/properties/Reasoning`-(gelecekte kullanmak için)
* `feed/entry/content/properties/Metadata`-(gelecekte kullanmak için)
* `feed/entry/content/properties/FormattedRating`-(gelecekte kullanmak için)

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get Catalog items that contain a token</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:48:19Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">CatalogItemsThatContainATokenEntity</title>
            <updated>2014-10-29T11:48:19Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                  <m:properties>
                    <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                    <d:Name m:type="Edm.String">Clara Callan</d:Name>
                    <d:Rating m:type="Edm.Double">0</d:Rating>
                    <d:Reasoning m:type="Edm.String"></d:Reasoning>
                    <d:Metadata m:type="Edm.String"></d:Metadata>
                    <d:FormattedRating m:type="Edm.Double" m:null="true"></d:FormattedRating>
                  </m:properties>
            </content>
        </entry>
    </feed>

## <a name="9-usage-data"></a>9. Kullanım verileri
### <a name="91----import-usage-data"></a>9.1.    Kullanım verilerini alma
#### <a name="911-uploading-file"></a>9.1.1. Dosya karşıya yükleme
Bu bölümde gösterilmiştir nasıl dosyası kullanarak tooupload kullanım verileri. Bu API birkaç kez ile kullanım verilerini çağırabilirsiniz. Tüm kullanım verileri tüm çağrıları için kaydedilir.

| HTTP yöntemi | URI |
|:--- |:--- |
| YAYINLA |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| Dosya adı |Başlangıç kataloğu metinsel tanımlayıcısı.<br>Yalnızca harf (A-Z, a-z), sayılar (0-9), tireler (-) ve alt çizgi (_).<br>En fazla uzunluk: 50 |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |Kullanım verileri. Biçimi:<br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th>Ad</th><th>Zorunlu</th><th>Tür</th><th>Açıklama</th></tr><tr><td>Kullanıcı Kimliği</td><td>Evet</td><td>[A-z], [a-z], [0-9], [_] &#40; Alt çizgi &#41; [-] &#40; çizgi &#41;<br> En fazla uzunluk: 255 </td><td>Bir kullanıcının benzersiz tanıtıcısı.</td></tr><tr><td>Öğe kimliği</td><td>Evet</td><td>[A-z], [a-z], [0-9], [&#95;] &#40; Alt çizgi &#41; [-] &#40; çizgi &#41;<br> En fazla uzunluk: 50</td><td>Bir öğeyi benzersiz tanımlayıcısı.</td></tr><tr><td>Zaman</td><td>Hayır</td><td>Tarih biçiminde: YYYY/AA/ddTHH (örneğin 2013/06/20T10:00:00)</td><td>Veri zamanı.</td></tr><tr><td>Olay</td><td>Yok; sağlanan daha sonra tarih de konulmalıdır</td><td>Merhaba aşağıdakilerden biri:<br>• Tıklatın<br>• RecommendationClick<br>• AddShopCart<br>• RemoveShopCart<br>• Satın alma</td><td></td></tr></table><br>En büyük dosya boyutu: 200MB<br><br>Örnek:<br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

**Yanıt**:

HTTP durum kodu: 200

* `Feed\entry\content\properties\LineCount`-Kabul satır sayısı.
* `Feed\entry\content\properties\ErrorCount`-Tooan hata eklenmemiş satır sayısı.
* `Feed\entry\content\properties\FileId`-Dosya tanımlayıcısı.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="912-using-data-acquisition"></a>9.1.2. Veri alma kullanma
Bu bölüm, gerçek toosend olayları tooAzure Machine Learning önerileri, genellikle Web sitenizi nasıl zaman gösterir.

| HTTP yöntemi | URI |
|:--- |:--- |
| YAYINLA |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| ÜSTBİLGİ |`"Content-Type", "text/xml"` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| apiVersion |1.0 |
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
                    <PurchaseItem>
                        <ItemId>ABBF8081-C5C0-4F09-9701-E1C7AC78304A</ItemId>
                        <Count>1</Count>
                    </PurchaseItem>
                    <PurchaseItem>
                        <ItemId>21BF8088-B6C0-4509-870C-11C0AC7F304B</ItemId>
                        <Count>3</Count>
                    </PurchaseItem>
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

### <a name="92----list-model-usage-files"></a>9.2.    Liste modeli kullanım dosyalar
Tüm model kullanım dosyalar meta verilerini alır.
Merhaba kullanım dosyalar olacak bir sayfa aynı anda aldı. Her sayfa içerir 100 öğeleri. Belirli dizinindeki tooget öğe istiyorsanız hello $skip odata parametresini kullanabilirsiniz. Örneğin, 100 konumdan başlayarak tooget öğe istiyorsanız, hello parametre $skip ekleme = 100 toohello istek.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| forModelId |Merhaba modeli benzersiz tanıtıcısı |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

Merhaba yanıt kullanım dosyasını her bir giriş içerir. Her giriş verileri aşağıdaki hello sahiptir:

* `feed\entry\content\properties\Id`-Kullanım dosya kimliği
* `feed\entry\content\properties\Length`-MB cinsinden kullanım dosya uzunluğu.
* `feed\entry\content\properties\DateModified`-Hello kullanım dosyasını oluşturulduğu tarih.
* `feed\entry\content\properties\UseInModel`-Olup hello kullanım dosyasını hello modelinde kullanılır.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of model's usage files info</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
            <updated>2014-10-30T09:40:25Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">4c067b42-e975-4cb2-8c98-a6ab80ed6d63</d:Id>
                    <d:Length m:type="Edm.Double">0</d:Length>
                    <d:DateModified m:type="Edm.String">10/30/2014 9:19:57 AM</d:DateModified>
                    <d:UseInModel m:type="Edm.String">true</d:UseInModel>
                </m:properties>
            </content>
        </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">3126d816-4e80-4248-8339-1ebbdb9d544d</d:Id>
                <d:Length m:type="Edm.Double">0.001</d:Length>
                <d:DateModified m:type="Edm.String">10/30/2014 9:21:44 AM</d:DateModified>
                <d:UseInModel m:type="Edm.String">true</d:UseInModel>
              </m:properties>
        </content>
    </entry>
</feed>

### <a name="93----get-usage-statistics"></a>9.3.    Kullanım istatistiklerini alın
Kullanım istatistiklerini alır.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| StartDate |Başlangıç tarihi. Biçimi: yyyy/aa/ddTHH |
| endDate |Bitiş tarihi. Biçimi: yyyy/aa/ddTHH |
| eventTypes |Virgülle ayrılmış dize olay türleri veya tüm olayları tooget null |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

Anahtar/değer öğeleri koleksiyonu. Her bir saate göre gruplandırılmış belirli bir olay türü için olayları hello toplamını içeriyor.

* `feed\entry[i]\content\properties\Key`-Başlangıç saati (saate göre gruplandırılmış) içerir ve hello olay türü.
* `feed\entry[i]\content\properties\Value`-Toplam olay sayısı.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get usage statistics</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-18T11:39:16Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;Click</d:Event>
                <d:Value m:type="Edm.String">5</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;RecommendationClick</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
              </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/1/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/5/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="94----get-usage-file-sample"></a>9.4.    Kullanım örneği Al
Alır kullanım dosya içeriğinin ilk 2 KB hello.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| Fileıd |Merhaba modeli kullanım dosyanın benzersiz tanıtıcısı |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

Yanıt ham metin biçiminde verilir:

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
</pre>


### <a name="95----get-model-usage-file"></a>9.5.    Model kullanım dosyasını Al
Merhaba tam hello kullanım dosyasının içeriğini alır.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| Orta |Merhaba modeli benzersiz tanıtıcısı |
| FID |Merhaba modeli kullanım dosyanın benzersiz tanıtıcısı |
| İndirme |1 |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

Yanıt ham metin biçiminde verilir:

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
244881,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
50547,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
213090,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
260655,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
72214,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
36326,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189336,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260655,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
162100,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
54946,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260965,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
102758,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
112602,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
163925,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
262998,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
144717,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
</pre>

### <a name="96----delete-usage-file"></a>9.6.    Kullanım dosyasını silin
Merhaba belirtilen model kullanım dosyasını siler.

| HTTP yöntemi | URI |
|:--- |:--- |
| SİL |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| Fileıd |Silinen hello dosya toobe benzersiz tanıtıcısı |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

### <a name="97----delete-all-usage-files"></a>9.7.    Tüm kullanım dosyalarını silin
Tüm model kullanım dosyalarını siler.

| HTTP yöntemi | URI |
|:--- |:--- |
| SİL |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

## <a name="10-features"></a>10. Özellikler
Bu bölümde tooretrieve özellik içeri hello özellikleri ve bunların değerleri, kendi derece gibi bilgileri nasıl ve ne zaman bu derece ayrıldı gösterir. Özellikler hello katalog verilerini bir parçası olarak içe aktarılır ve bunların derece derece yapı yapıldığında sonra ilişkilendirilir.
Özellik derece kullanım verilerini ve tür öğelerinin according toohello düzenini değiştirebilirsiniz. Ancak tutarlı kullanım/öğeler için yalnızca küçük dalgalanmaları hello derece olması gerekir.
Özellikler Hello derecesini negatif olmayan bir sayıdır. Merhaba numarası 0 bu hello özelliği olmayan derece anlamına gelir (Bu hello ilk derece yapı API önceki toohello tamamlanmasından çağırma olur). hangi hello derece öznitelikli hello tarih hello puan yenilik adı verilir.

### <a name="101-get-features-info-for-last-rank-build"></a>10.1. (İçin son derece derleme) özellikleri bilgilerini al
Merhaba son başarılı derece yapı için bir derecelendirme hello özellik bilgilerini alır.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| samplingSize |Başlangıç Kataloğu'nda mevcut toohello verileri göre her bir özellik için değerleri tooinclude sayısı. <br/>Olası değerler şunlardır:<br> -1 - tüm örnekleri. <br>0 - hiçbir örnekleme. <br>N - her bir özellik adı için dönüş N örneklerini içerir. |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

Merhaba yanıt özellik bilgileri girişlerinin listesini içerir. Her giriş içerir:

* `feed/entry/content/m:properties/d:Name`-Özellik adı.
* `feed/entry/content/m:properties/d:RankUpdateDate`-Date ayrılmış toothis özellik, sıralama sırasında hangi hello paketini: puan yenilik özelliği. Geçmiş bir tarih ('0001-01-01T00:00:00') hiçbir derece yapı gerçekleştirildiğini anlamına gelir.
* `feed/entry/content/m:properties/d:Rank`-Özellik derece (kayan nokta). 2.0 ve yedekleme bir derece iyi bir özellik olarak kabul edilir.
* `feed/entry/content/m:properties/d:SampleValues`-İstenen toohello örnekleme boyut değerleri virgülle ayrılmış listesi.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get hello features of a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-01-08T13:15:02Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Author</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Publisher</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1"/>
        <contenttype="application/xml">
        <m:properties>
            <d:Name m:type="Edm.String">Year</d:Name>
            <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
            <d:Rank m:type="Edm.String">0</d:Rank>
            <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
        </m:properties>
        </content>
    </entry>
</feed>

### <a name="102-get-features-info-for-specific-rank-build"></a>10.2. (Belirli derece derleme için) özellikleri bilgilerini al
Belirli bir derece yapı sıralaması hello hello özellik bilgilerini alır.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| samplingSize |Başlangıç Kataloğu'nda mevcut toohello verileri göre her bir özellik için değerleri tooinclude sayısı.<br/> Olası değerler şunlardır:<br> -1 - tüm örnekleri. <br>0 - hiçbir örnekleme. <br>N - her bir özellik adı için dönüş N örneklerini içerir. |
| rankBuildId |Merhaba derece yapı veya -1 hello son derece yapı için benzersiz tanıtıcısı |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

Merhaba yanıt özellik bilgileri girişlerinin listesini içerir. Her giriş içerir:

* `feed/entry/content/m:properties/d:Name`-Özellik adı.
* `feed/entry/content/m:properties/d:RankUpdateDate`-Date ayrılmış toothis özellik, sıralama sırasında hangi hello paketini: puan yenilik özelliği. Geçmiş bir tarih ('0001-01-01T00:00:00') hiçbir derece yapı gerçekleştirildiğini anlamına gelir.
* `feed/entry/content/m:properties/d:Rank`-Özellik derece (kayan nokta). 2.0 ve yedekleme bir derece iyi bir özellik olarak kabul edilir.
* `feed/entry/content/m:properties/d:SampleValues`-İstenen toohello örnekleme boyut değerleri virgülle ayrılmış listesi.

OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get hello features of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:54:22Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Author</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">3.38867426</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Publisher</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.67839336</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Year</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.12352145</d:Rank>
                    <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
                </m:properties>
            </content>
        </entry>
    </feed>


## <a name="11-build"></a>11. Oluşturma
  Bu bölümde hello açıklanmaktadır toobuilds ilgili farklı API'ler. Derleme 3 türleri vardır: bir öneri yapı, derece yapı ve (sık birlikte satın) FBT derleme.

Merhaba öneri yapı, bir öneri modeli tahminleri için kullanılan toogenerate amaçtır. Öngörüler (için yapı bu tür) içinde iki özellikleri getirir:

* I2I - paketini Madde tooItem önerileri - verilen öğeyi veya liste öğelerinin bu seçenek, büyük olasılıkla toobe çok ilgisini çeken öğeleri listesini tahmin.
* U2I - paketini Kullanıcı tooItem önerileri verilen bir kullanıcı kimliği (ve isteğe bağlı olarak bir öğe listesi) - Bu seçenek, büyük olasılıkla toobe verilen kullanıcı (ve ek dilediği öğelerinin) hello çok ilgisini öğeleri listesini tahmin etmek. Merhaba U2I önerileri hello model oluşturulmuş toohello süresini hello kullanıcının ilgi olan öğelerin hello geçmişini dayanır.

Bir derece yapı özelliklerinizi hello yararlılığı hakkında toolearn sağlayan teknik bir yapıdır. Genellikle, sipariş tooget hello en iyi sonucu özellikleri içeren bir öneri model için aşağıdaki adımları hello izlemesi gerekir:

* (Özelliklerinizi hello puanı kararlı değilse) derece bir derlemeyi tetiklemeyi ve hello özelliği puanı almak kadar bekleyin.
* Arama hello tarafından özelliklerinizi Hello derecesini almak [özellikleri bilgi al](#101-get-features-info-for-last-rank-build) API.
* Bir öneri yapı şu parametreler hello ile yapılandırın:
  * `useFeatureInModel`-TooTrue ayarlayın.
  * `ModelingFeatureList`-2.0 veya daha fazla puanı özelliklerinin set tooa virgülle ayrılmış listesi (Merhaba önceki adımda alınan toohello sıralar according).
  * `AllowColdItemPlacement`-TooTrue ayarlayın.
  * İsteğe bağlı olarak ayarlayabilirsiniz `EnableFeatureCorrelation` tooTrue ve `ReasoningFeatureList` toohello açıklamalarını (genellikle aynı özelliklerin listesi kullanılan Model oluşturma veya bir alt liste hello) toouse istediğiniz özelliklerin listesi.
* Merhaba öneri yapı yapılandırılmış hello parametrelerle tetikler.

Not: herhangi bir parametre yapılandırmazsanız (örneğin hello öneri yapı parametresiz çağırma) veya açıkça özellikleri hello kullanımını devre dışı değil (örneğin `UseFeatureInModel` ayarlamak tooFalse), hello sistem hello özelliği ile ilgili parametreleri ayarlayacak derece yapı mevcut durumda toohello değerleri yukarıdaki açıklanmıştır.

Bir derece yapı çalıştırma sınırlaması yoktur ve bir öneri yapı eşzamanlı olarak Merhaba aynı modeli. Bununla birlikte, aynı aynı paralel olarak model hello yazın hello iki derlemelerini çalıştırılamıyor.

(Sık birlikte satın) FBT yapı henüz doğası gereği homojen olmayan katalogları için yararlı olan "Klasik" bazen öneren adlı başka bir önerileri algoritmasıdır (homojen: defterleri, filmler, bazı yemek deneyerek; homojen olmayan: bilgisayar ve cihazlar, etki alanları arası, oldukça farklı).

Not: hello karşıya yüklediğiniz kullanım dosyalar içeriyorsa hello isteğe bağlı alan "olay türü", daha sonra FBT için yalnızca "Satın Al" olayları modelleme kullanılacaktır. Olay türü sağlanırsa tüm olayları satın alma olarak kabul edilir.

#### <a name="111-build-parameters"></a>11.1 parametreleri derleme
Her bir yapı türü (aşağıda gösterilen) parametreleri kümesini aracılığıyla yapılandırılabilir. Merhaba parametreleri yapılandırmazsanız, hello sistem otomatik olarak toohello bilgi hello zaman mevcut bir derlemeyi tetiklemeyi göre değerleri toohello parametreleri öznitelik.

##### <a name="1111-usage-condenser"></a>11.1.1. Kullanım Kondansatör
Kullanıcılar veya birkaç kullanım noktalarıyla öğeleri bilgileri'den daha fazla gürültü içerebilir. Merhaba sistem toopredict hello en az bir model kullanılan kullanıcı/öğe toobe başına kullanım noktası denemesi sayısı. Bu numara, hello ItemCutoffLowerBound ve öğeleri ve hello UserCutOffLowerBound ve kullanıcılar için UserCutoffUpperBound parametreleri tarafından tanımlanan hello aralık ItemCutoffUpperBound parametreleri tarafından tanımlanan hello aralıkta olacaktır. Merhaba Kondansatör etkisi öğeler veya kullanıcıların ayarıyla hello karşılık gelen sınırları toozero en az biri en aza indirgenebilir.

##### <a name="1112-rank-build-parameters"></a>11.1.2. RANK yapı parametreleri
Merhaba tabloda derece bir yapı için hello yapı parametreleri gösterilmektedir.

| Anahtar | Açıklama | Tür | Geçerli bir değer |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |Merhaba hello modeli gerçekleştirir yineleme sayısını hello tarafından yansıtılan zaman ve hello model doğruluğundan genel işlem. Merhaba daha yüksek hello sayı, hello daha iyi doğruluk alırsınız, ancak hello hesaplamak için daha uzun sürer. |Tamsayı |10-50 |
| NumberOfModelDimensions |Merhaba dimensions sayısı 'Özellikler' hello modeli toohello sayısı toofind verilerinizi içinde deneyecek ilişkilendirir. Boyutlar Hello sayısını artırmayı daha iyi hello sonuçlarını daha küçük kümeler halinde hassas ayar yapma izin verir. Ancak, çok fazla boyutları bulmalarını bağıntıları öğeleri arasında hello modeli engeller. |Tamsayı |10-40 |
| ItemCutOffLowerBound |Merhaba öğesi alt sınır hello Kondansatör için tanımlar. Yukarıdaki kullanım Kondansatör bakın. |Tamsayı |2 veya daha fazla (0 Kondansatör devre dışı) |
| ItemCutOffUpperBound |Merhaba öğesi üst sınır hello Kondansatör için tanımlar. Yukarıdaki kullanım Kondansatör bakın. |Tamsayı |2 veya daha fazla (0 Kondansatör devre dışı) |
| UserCutOffLowerBound |Merhaba kullanıcı alt sınır hello Kondansatör için tanımlar. Yukarıdaki kullanım Kondansatör bakın. |Tamsayı |2 veya daha fazla (0 Kondansatör devre dışı) |
| UserCutOffUpperBound |Merhaba kullanıcı üst sınır hello Kondansatör için tanımlar. Yukarıdaki kullanım Kondansatör bakın. |Tamsayı |2 veya daha fazla (0 Kondansatör devre dışı) |

##### <a name="1113-recommendation-build-parameters"></a>11.1.3. Öneri yapı parametreleri
Merhaba tabloda öneri yapı için hello yapı parametreleri gösterilmektedir.

| Anahtar | Açıklama | Tür | Geçerli bir değer |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |Merhaba hello modeli gerçekleştirir yineleme sayısını hello tarafından yansıtılan zaman ve hello model doğruluğundan genel işlem. Merhaba daha yüksek hello sayı, hello daha iyi doğruluk alırsınız, ancak hello hesaplamak için daha uzun sürer. |Tamsayı |10-50 |
| NumberOfModelDimensions |Merhaba dimensions sayısı 'Özellikler' hello modeli toohello sayısı toofind verilerinizi içinde deneyecek ilişkilendirir. Boyutlar Hello sayısını artırmayı daha iyi hello sonuçlarını daha küçük kümeler halinde hassas ayar yapma izin verir. Ancak, çok fazla boyutları bulmalarını bağıntıları öğeleri arasında hello modeli engeller. |Tamsayı |10-40 |
| ItemCutOffLowerBound |Merhaba öğesi alt sınır hello Kondansatör için tanımlar. Yukarıdaki kullanım Kondansatör bakın. |Tamsayı |2 veya daha fazla (0 Kondansatör devre dışı) |
| ItemCutOffUpperBound |Merhaba öğesi üst sınır hello Kondansatör için tanımlar. Yukarıdaki kullanım Kondansatör bakın. |Tamsayı |2 veya daha fazla (0 Kondansatör devre dışı) |
| UserCutOffLowerBound |Merhaba kullanıcı alt sınır hello Kondansatör için tanımlar. Yukarıdaki kullanım Kondansatör bakın. |Tamsayı |2 veya daha fazla (0 Kondansatör devre dışı) |
| UserCutOffUpperBound |Merhaba kullanıcı üst sınır hello Kondansatör için tanımlar. Yukarıdaki kullanım Kondansatör bakın. |Tamsayı |2 veya daha fazla (0 Kondansatör devre dışı) |
| Açıklama |Açıklama oluşturun. |Dize |Herhangi bir metin en çok 512 karakter |
| EnableModelingInsights |Merhaba öneri model üzerinde toocompute ölçümleri sağlar. |Boole değeri |True/False |
| UseFeaturesInModel |Özellikler sipariş tooenhance hello öneri modelinde kullandıysanız gösterir. |Boole değeri |True/False |
| ModelingFeatureList |Sipariş tooenhance hello öneri de hello öneri derlemede kullanılan özellik adları toobe virgülle ayrılmış listesi. |Dize |Özellik adlarını, too512 karakter |
| AllowColdItemPlacement |Hello öneri de soğuk öğeleri özelliği benzerlik anında olmadığını gösterir. |Boole değeri |True/False |
| EnableFeatureCorrelation |Mantığı içinde kullanılabilir özellikleri gösterir. |Boole değeri |True/False |
| ReasoningFeatureList |Tümceler (örn. öneri açıklamaları) akıl için kullanılan özellik adları toobe virgülle ayrılmış listesi. |Dize |Özellik adlarını, too512 karakter |
| EnableU2I |Kişiselleştirilmiş hello öneri paketini izin ver U2I (kullanıcı tooitem öneriler). |Boole değeri |True/False (varsayılan true) |

##### <a name="1114-fbt-build-parameters"></a>11.1.4. FBT yapı parametreleri
Merhaba tabloda öneri yapı için hello yapı parametreleri gösterilmektedir.

| Anahtar | Açıklama | Tür | Geçerli değer (varsayılan) |
|:--- |:--- |:--- |:--- |
| FbtSupportThreshold |Koruyucu hello modeli nasıl. Modelleme için kabul öğeleri toobe ortak oluşumları sayısı. |Tamsayı |3-50 (6) |
| FbtMaxItemSetSize |Öğe sık kümesinde sınırları hello sayısı. |Tamsayı |2-3 (2) |
| FbtMinimalScore |Sık kümesi hello dahil sipariş toobe içinde döndürülen en az puan sonuçlanır. Merhaba yüksek hello daha iyi. |Çift |0 ve üstünde (0) |
| FbtSimilarityFunction |Merhaba yapı tarafından kullanılan hello benzerlik işlevi toobe tanımlar. Yükseltme serendipity korur, ortak oluşumu öngörülebilirlik ayrıcalıklı kılar ve Jaccard hello iki arasında iyi bir seçim değil. |Dize |cooccurrence, yükseltme, jaccard (yükseltme) |

### <a name="112-trigger-a-recommendation-build"></a>11.2. Tetikleyici bir öneri derleme
  Varsayılan olarak bu API öneri modeli yapı tetikler. tootrigger bir derece derleme (sipariş tooscore özelliklerinde), hello yapı API değişken yapı tür parametresi birlikte kullanılmalıdır.

| HTTP yöntemi | URI |
|:--- |:--- |
| YAYINLA |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| ÜSTBİLGİ |`"Content-Type", "text/xml"`(İstek gövdesi gönderiliyorsa) |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| userDescription |Başlangıç kataloğu metinsel tanımlayıcısı. Boşluklar kullanırsanız, % 20 yerine kodlamak gerekir olduğunu unutmayın. Yukarıdaki örnekte bkz.<br>En fazla uzunluk: 50 |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |Boş bırakılırsa hello yapı hello varsayılan derleme parametrelerle yürütülür.<br><br>Hello parametreleri XML olarak tooset hello yapı parametreleri isterseniz, örnek aşağıdaki hello olduğu gibi hello gövdesine gönderin. (Merhaba parametreleri bir açıklaması için hello "yapı parametreleri" bölümüne bakın.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>` |

**Yanıt**:

HTTP durum kodu: 200

Bu zaman uyumsuz bir API'dir. Yanıt olarak bir yapı kimliği alırsınız. Merhaba derleme sona erdiğinde tooknow hello "Get derlemeler durumu bir modelin" API çağrısı ve gerekir bulun hello yanıtta bu derleme kimliği. Bir yapı dakika toohours hello hello verilerin boyutuna bağlı olarak gelen alabileceğine dikkat edin.

Merhaba yapı kadar sona erer önerileri kullanamayacaklarını.

Geçerli yapı durumu:

* Oluşturma - yapı isteği oluşturuldu.
* Sıraya alınmış - yapı isteği gönderildi ve kuyruğa alınır.
* Yapı - Yapı devam ediyor.
* Başarılı - yapı başarılı bir şekilde sona erdi.
* Hata - derleme bir hata ile sona erdi.
* İptal - derleme iptal edildi.
* İptal etme - hello yapı için bir iptal etme isteği gönderildi.

Kimliği yolu izleyerek hello altında bulunabilir bu hello yapı dikkat edin:`Feed\entry\content\properties\Id`

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a>11.3. Tetikleyici yapı (öneri, derece veya FBT)
| HTTP yöntemi | URI |
|:--- |:--- |
| YAYINLA |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| ÜSTBİLGİ |`"Content-Type", "text/xml"`(İstek gövdesi gönderiliyorsa) |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| userDescription |Başlangıç kataloğu metinsel tanımlayıcısı. Boşluklar kullanırsanız, % 20 yerine kodlamak gerekir olduğunu unutmayın. Yukarıdaki örnekte bkz.<br>En fazla uzunluk: 50 |
| buildType |Merhaba yapı tooinvoke türü: <br/> -Öneri yapı ' Önerisi' <br> -'Rank derleme için sıralaması' <br/> -FBT yapı için ' Fbt' |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |Boş bırakılırsa hello yapı hello varsayılan derleme parametrelerle yürütülür.<br><br>Merhaba gövdesinde gibi örnek aşağıdaki hello içine tooset yapı parametreleri istiyorsanız, bunları XML olarak gönderin. (Bir açıklama ve hello parametrelerin tam listesi için hello "yapı parametreleri" bölümüne bakın.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>` |

**Yanıt**:

HTTP durum kodu: 200

Bu zaman uyumsuz bir API'dir. Yanıt olarak bir yapı kimliği alırsınız. Merhaba derleme sona erdiğinde tooknow hello "Get derlemeler durumu bir modelin" API çağrısı ve gerekir bulun hello yanıtta bu derleme kimliği. Bir yapı dakika toohours hello hello verilerin boyutuna bağlı olarak gelen alabileceğine dikkat edin.

Merhaba yapı kadar sona erer önerileri kullanamayacaklarını.

Geçerli yapı durumu:

* Oluşturma - Model oluşturuldu.
* Sıraya alınmış - Model yapı tetiklendi ve kuyruğa alınır.
* Yapı - modeli oluşturuluyor.
* Başarılı - yapı başarılı bir şekilde sona erdi.
* Hata - derleme bir hata ile sona erdi.
* İptal - derleme iptal edildi.
* İptal etme - derleme iptal edildi.

Kimliği yolu izleyerek hello altında bulunabilir bu hello yapı dikkat edin:`Feed\entry\content\properties\Id`

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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




### <a name="114-get-builds-status-of-a-model"></a>11.4. Bir modelin derlemeleri durumunu Al
Yapılar ve belirtilen bir model için durumlarını alır.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| onlyLastBuild |Gösteren tüm hello tooreturn hello modeli geçmişini ya da hello en son yapı yalnızca hello durumunu derleme |
| apiVersion |1.0 |

**Yanıt**:

HTTP durum kodu: 200

Merhaba yanıt yapı her bir giriş içerir. Her giriş verileri aşağıdaki hello sahiptir:

* `feed/entry/content/properties/UserName`-Hello kullanıcı adı.
* `feed/entry/content/properties/ModelName`-Hello model adı.
* `feed/entry/content/properties/ModelId`-Model benzersiz tanımlayıcısı.
* `feed/entry/content/properties/IsDeployed`-Olup hello yapı (paketini dağıtılır Etkin yapı).
* `feed/entry/content/properties/BuildId`-Benzersiz tanımlayıcısı oluşturun.
* `feed/entry/content/properties/BuildType`-Hello yapı türü.
* `feed/entry/content/properties/Status`-Durum oluşturun. Merhaba aşağıdakilerden biri olabilir: hata, yapı, sıraya alınan, Cancelling, iptal edildi, başarılı.
* `feed/entry/content/properties/StatusMessage`-Ayrıntılı durum iletisi (yalnızca toospecific durumlar geçerlidir).
* `feed/entry/content/properties/Progress`-İlerleme durumu (%) oluşturun.
* `feed/entry/content/properties/StartTime`-Başlangıç saati oluşturun.
* `feed/entry/content/properties/EndTime`-Bitiş saati oluşturun.
* `feed/entry/content/properties/ExecutionTime`-Yapı süresi.
* `feed/entry/content/properties/ProgressStep`-Devam eden bir derleme geçerli aşamasını hello hakkında ayrıntılar.

Geçerli yapı durumu:

* Oluşturulan - yapı isteği girdisi oluşturuldu.
* Sıraya alınmış - oluşturma isteği tetiklendi ve kuyruğa alınır.
* Yapı - Yapı işlemi devam ediyor.
* Başarılı - yapı başarılı bir şekilde sona erdi.
* Hata - derleme bir hata ile sona erdi.
* İptal - derleme iptal edildi.
* İptal etme - derleme iptal edildi.

Derleme türü için geçerli değerler:

* RANK - derece oluşturun.
* Öneri - öneri derleme.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T17:51:10Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T17:51:10Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="115-get-builds-status"></a>11.5. Derlemeleri durumunu Al
Alır, bir kullanıcının tüm modellerin durumlar oluşturun.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| onlyLastBuild |Gösteren tüm hello tooreturn hello modeli geçmişini ya da hello en son yapı yalnızca hello durumunu derleme. |
| apiVersion |1.0 |

**Yanıt**:

HTTP durum kodu: 200

Merhaba yanıt yapı her bir giriş içerir. Her giriş verileri aşağıdaki hello sahiptir:

* `feed/entry/content/properties/UserName`-Hello kullanıcı adı.
* `feed/entry/content/properties/ModelName`-Hello model adı.
* `feed/entry/content/properties/ModelId`-Model benzersiz tanımlayıcısı.
* `feed/entry/content/properties/IsDeployed`-Olup hello yapı dağıtılır.
* `feed/entry/content/properties/BuildId`-Benzersiz tanımlayıcısı oluşturun.
* `feed/entry/content/properties/BuildType`-Hello yapı türü.
* `feed/entry/content/properties/Status`-Durum oluşturun. Merhaba aşağıdakilerden biri olabilir: hata, yapı, sıraya alınan, iptal edildi, Cancelling, başarılı.
* `feed/entry/content/properties/StatusMessage`-Ayrıntılı durum iletisi (yalnızca toospecific durumlar geçerlidir).
* `feed/entry/content/properties/Progress`-İlerleme durumu (%) oluşturun.
* `feed/entry/content/properties/StartTime`-Başlangıç saati oluşturun.
* `feed/entry/content/properties/EndTime`-Bitiş saati oluşturun.
* `feed/entry/content/properties/ExecutionTime`-Yapı süresi.
* `feed/entry/content/properties/ProgressStep`-Devam eden bir derleme geçerli aşamasını hello hakkında ayrıntılar.

Geçerli yapı durumu:

* Oluşturulan - yapı isteği girdisi oluşturuldu.
* Sıraya alınmış - oluşturma isteği tetiklendi ve kuyruğa alınır.
* Yapı - Yapı işlemi devam ediyor.
* Başarılı - yapı başarılı bir şekilde sona erdi.
* Hata - derleme bir hata ile sona erdi.
* İptal - derleme iptal edildi.
* İptal etme - derleme iptal edildi.

Derleme türü için geçerli değerler:

* RANK - derece oluşturun.
* Öneri - öneri derleme.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T18:41:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T18:41:21Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="116-delete-build"></a>11.6. Yapı Sil
Bir yapı siler.

NOT: <br>Etkin bir yapı silemezsiniz. Merhaba modeli olmalıdır tooa farklı etkin yapı silmeden önce güncelleştirildi.<br>Devam eden yapı silemezsiniz. Merhaba yapı ilk çağırarak iptal <strong>iptal yapı</strong>.

| HTTP yöntemi | URI |
|:--- |:--- |
| SİL |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| Buildıd |Merhaba yapı benzersiz tanımlayıcısı. |
| apiVersion |1.0 |

**Yanıtı:**

HTTP durum kodu: 200

### <a name="117-cancel-build"></a>11.7. Derleme iptal et
Durum oluşturulmasında, bir derlemede iptal eder.

| HTTP yöntemi | URI |
|:--- |:--- |
| PUT |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| Buildıd |Merhaba yapı benzersiz tanımlayıcısı. |
| apiVersion |1.0 |

**Yanıtı:**

HTTP durum kodu: 200

### <a name="118-get-build-parameters"></a>11.8. Yapı parametreleri Al
Alır parametreleri oluşturun.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| Buildıd |Merhaba yapı benzersiz tanımlayıcısı. |
| apiVersion |1.0 |

**Yanıtı:**

HTTP durum kodu: 200

Bu API anahtar/değer öğe koleksiyonunu döndürür. Her öğe bir parametre ve değerini temsil eder:

* `feed/entry/content/properties/Key`-Parametre adı oluşturun.
* `feed/entry/content/properties/Value`-Parametre değeri oluşturun.

Merhaba tabloda her anahtar temsil eden hello değeri gösterir.

| Anahtar | Açıklama | Tür | Geçerli bir değer |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |Merhaba hello modeli gerçekleştirir yineleme sayısını hello tarafından yansıtılan zaman ve hello model doğruluğundan genel işlem. Merhaba daha yüksek hello sayı, hello daha iyi doğruluk alırsınız, ancak hello hesaplamak için daha uzun sürer. |Tamsayı |10-50 |
| NumberOfModelDimensions |Merhaba dimensions sayısı 'Özellikler' hello modeli toohello sayısı toofind verilerinizi içinde deneyecek ilişkilendirir. Boyutlar Hello sayısını artırmayı daha iyi hello sonuçlarını daha küçük kümeler halinde hassas ayar yapma izin verir. Ancak, çok fazla boyutları bulmalarını bağıntıları öğeleri arasında hello modeli engeller. |Tamsayı |10-40 |
| ItemCutOffLowerBound |Merhaba öğesi alt sınır hello Kondansatör için tanımlar. Yukarıdaki kullanım Kondansatör bakın. |Tamsayı |2 veya daha fazla (0 Kondansatör devre dışı) |
| ItemCutOffUpperBound |Merhaba öğesi üst sınır hello Kondansatör için tanımlar. Yukarıdaki kullanım Kondansatör bakın. |Tamsayı |2 veya daha fazla (0 Kondansatör devre dışı) |
| UserCutOffLowerBound |Merhaba kullanıcı alt sınır hello Kondansatör için tanımlar. Yukarıdaki kullanım Kondansatör bakın. |Tamsayı |2 veya daha fazla (0 Kondansatör devre dışı) |
| UserCutOffUpperBound |Merhaba kullanıcı üst sınır hello Kondansatör için tanımlar. Yukarıdaki kullanım Kondansatör bakın. |Tamsayı |2 veya daha fazla (0 Kondansatör devre dışı) |
| Açıklama |Açıklama oluşturun. |Dize |Herhangi bir metin en çok 512 karakter |
| EnableModelingInsights |Merhaba öneri model üzerinde toocompute ölçümleri sağlar. |Boole değeri |True/False |
| UseFeaturesInModel |Özellikler sipariş tooenhance hello öneri modelinde kullandıysanız gösterir. |Boole değeri |True/False |
| ModelingFeatureList |Sipariş tooenhance hello öneri de hello öneri derlemede kullanılan özellik adları toobe virgülle ayrılmış listesi. |Dize |Özellik adlarını, too512 karakter |
| AllowColdItemPlacement |Hello öneri de soğuk öğeleri özelliği benzerlik anında olmadığını gösterir. |Boole değeri |True/False |
| EnableFeatureCorrelation |Mantığı içinde kullanılabilir özellikleri gösterir. |Boole değeri |True/False |
| ReasoningFeatureList |Tümceler (örn. öneri açıklamaları) akıl için kullanılan özellik adları toobe virgülle ayrılmış listesi. |Dize |Özellik adlarını, too512 karakter |

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get build parameters</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:50:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UseFeaturesInModel</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">AllowColdItemPlacement</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableFeatureCorrelation</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableModelingInsights</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelIterations</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
            <titletype="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelDimensions</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <linkrel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ModelingFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ReasoningFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">Description</d:Key>
                    <d:Value m:type="Edm.String">rankBuild</d:Value>
                </m:properties>
            </content>
        </entry>
    </feed>

## <a name="12-recommendation"></a>12. Öneri
### <a name="121-get-item-recommendations-for-active-build"></a>12.1. (İçin etkin yapı) öğesi öneriler alın
"Öneri" Merhaba etkin yapı türü önerileri alın veya "Fbt" oluştururken Çekirdeği (giriş) öğelerinin bir listesini esas.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| öğe kimliklerinin |Merhaba öğeleri toorecommend için virgülle ayrılmış listesi. <br>Merhaba etkin yapı ise yalnızca bir öğe gönderebilirsiniz sonra FBT yazın. <br>En fazla uzunluk: 1024 |
| numberOfResults |Gerekli sonuç sayısı <br> En fazla: 150 |
| includeMetatadata |Gelecekte kullanmak, her zaman yanlış |
| apiVersion |1.0 |

**Yanıtı:**

HTTP durum kodu: 200

Merhaba yanıt önerilen öğe başına bir giriş içerir. Her giriş verileri aşağıdaki hello sahiptir:

* `Feed\entry\content\properties\Id`-Önerilen öğesi kimliği
* `Feed\entry\content\properties\Name`-Hello öğesinin adı.
* `Feed\entry\content\properties\Rating`-Hello öneri derecesi; daha yüksek numarası, daha yüksek güvenilirlik anlamına gelir.
* `Feed\entry\content\properties\Reasoning`-Öneri (örn. öneri açıklamaları) akıl.

Aşağıdaki örnek yanıt Hello 10 önerilen öğeleri içerir.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
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

### <a name="122-get-item-recommendations-of-a-specific-build"></a>12.2. (Biri, belirli bir yapı) öğesi öneriler alın
Belli bir yapı türü "Öneri" veya "Fbt" öneriler alın.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| öğe kimliklerinin |Merhaba öğeleri toorecommend için virgülle ayrılmış listesi. <br>Merhaba etkin yapı ise yalnızca bir öğe gönderebilirsiniz sonra FBT yazın. <br>En fazla uzunluk: 1024 |
| numberOfResults |Gerekli sonuç sayısı <br> En fazla: 150 |
| includeMetatadata |Gelecekte kullanmak, her zaman yanlış |
| Buildıd |Bu öneri istek kimliği toouse Hello derleme |
| apiVersion |1.0 |

**Yanıtı:**

HTTP durum kodu: 200

Merhaba yanıt önerilen öğe başına bir giriş içerir. Her giriş verileri aşağıdaki hello sahiptir:

* `Feed\entry\content\properties\Id`-Önerilen öğesi kimliği
* `Feed\entry\content\properties\Name`-Hello öğesinin adı.
* `Feed\entry\content\properties\Rating`-Hello öneri derecesi; daha yüksek numarası, daha yüksek güvenilirlik anlamına gelir.
* `Feed\entry\content\properties\Reasoning`-Öneri (örn. öneri açıklamaları) akıl.

12,1 yanıt örnekte bkz:

### <a name="123-get-fbt-recommendations-for-active-build"></a>12.3. (İçin etkin yapı) FBT öneriler alın
Bir çekirdek (giriş) öğesi "Fbt" temel türü hello etkin yapı öneriler alın.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| öğe kimliği |Öğe toorecommend için. <br>En fazla uzunluk: 1024 |
| numberOfResults |Gerekli sonuç sayısı <br>En fazla: 150 |
| minimalScore |Sık kümesi hello dahil sipariş toobe içinde döndürülen en az puan sonuçları |
| includeMetatadata |Gelecekte kullanmak, her zaman yanlış |
| apiVersion |1.0 |

**Yanıtı:**

HTTP durum kodu: 200

Merhaba yanıt önerilen öğesi kümesi (genellikle hello çekirdek/giriş öğesi ile birlikte satın öğeleri kümesi) her bir giriş içerir. Her giriş verileri aşağıdaki hello sahiptir:

* `Feed\entry\content\properties\Id1`-Önerilen öğesi kimliği
* `Feed\entry\content\properties\Name1`-Hello öğesinin adı.
* `Feed\entry\content\properties\Id2`-2 önerilen öğesi kimliği (isteğe bağlı).
* `Feed\entry\content\properties\Name2`-Öğesinin adı hello 2 (isteğe bağlı).
* `Feed\entry\content\properties\Rating`-Hello öneri derecesi; daha yüksek numarası, daha yüksek güvenilirlik anlamına gelir.
* `Feed\entry\content\properties\Reasoning`-Öneri (örn. öneri açıklamaları) akıl.

Merhaba örnek yanıt aşağıdaki 3 önerilen öğesi ayarlar içerir.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemId='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">159</d:Id1>
        <d:Name1 m:type="Edm.String">159</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">52</d:Id1>
        <d:Name1 m:type="Edm.String">52</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.533343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">35</d:Id1>
        <d:Name1 m:type="Edm.String">35</d:Name1>
        <d:Id2 m:type="Edm.String">102</d:Id2>
        <d:Name2 m:type="Edm.String">102</d:Name2>
        <d:Rating m:type="Edm.Double">0.523343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '35' and '102'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a>12.4. (Biri, belirli bir yapı) FBT öneriler alın
Belli bir yapı türü "Fbt" öneriler alın.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| öğe kimliği |Öğe toorecommend için. <br>En fazla uzunluk: 1024 |
| numberOfResults |Gerekli sonuç sayısı <br>En fazla: 150 |
| minimalScore |Sık kümesi hello dahil sipariş toobe içinde döndürülen en az puan sonuçları |
| includeMetatadata |Gelecekte kullanmak, her zaman yanlış |
| Buildıd |Bu öneri istek kimliği toouse Hello derleme |
| apiVersion |1.0 |

**Yanıtı:**

HTTP durum kodu: 200

Merhaba yanıt önerilen öğesi kümesi (genellikle hello çekirdek/giriş öğesi ile birlikte satın öğeleri kümesi) her bir giriş içerir. Her giriş verileri aşağıdaki hello sahiptir:

* `Feed\entry\content\properties\Id1`-Önerilen öğesi kimliği
* `Feed\entry\content\properties\Name1`-Hello öğesinin adı.
* `Feed\entry\content\properties\Id2`-2 önerilen öğesi kimliği (isteğe bağlı).
* `Feed\entry\content\properties\Name2`-Öğesinin adı hello 2 (isteğe bağlı).
* `Feed\entry\content\properties\Rating`-Hello öneri derecesi; daha yüksek numarası, daha yüksek güvenilirlik anlamına gelir.
* `Feed\entry\content\properties\Reasoning`-Öneri (örn. öneri açıklamaları) akıl.

12.3 yanıt örnekte bkz:

### <a name="125-get-user-recommendations-for-active-build"></a>12.5. Kullanıcı öneriler alın (etkin derleme için)
Tür "Öneri" etkin yapı işaretlenmiş bir yapı kullanıcı öneriler alın.

Merhaba API hello kullanıcı toohello kullanım geçmişine göre tahmin edilen madde listesini döndürür.

Notlar: 

1. FBT derleme için hiçbir kullanıcı öneri yok.
2. Bu yöntem bir hata döndürür olacak FBT Hello etkin yapı ise.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| Kullanıcı Kimliği |Merhaba kullanıcının benzersiz tanıtıcısı |
| numberOfResults |Gerekli sonuç sayısı |
| includeMetatadata |Gelecekte kullanmak, her zaman yanlış |
| apiVersion |1.0 |

**Yanıtı:**

HTTP durum kodu: 200

Merhaba yanıt önerilen öğe başına bir giriş içerir. Her giriş verileri aşağıdaki hello sahiptir:

* `Feed\entry\content\properties\Id`-Önerilen öğesi kimliği
* `Feed\entry\content\properties\Name`-Hello öğesinin adı.
* `Feed\entry\content\properties\Rating`-Hello öneri derecesi; daha yüksek numarası, daha yüksek güvenilirlik anlamına gelir.
* `Feed\entry\content\properties\Reasoning`-Öneri (örn. öneri açıklamaları) akıl.

12,1 yanıt örnekte bkz:

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a>12.6. Kullanıcı öneriler öğesi listesiyle (için etkin yapı) alın.
Tür "Öneri" ek öğeler listesi ile etkin yapı olarak işaretlenmiş bir yapı kullanıcı öneriler alın

Merhaba API hello kullanıcı ve hello ek sağlanan öğeleri toohello kullanım geçmişine göre tahmin edilen madde listesini döndürür.

Notlar: 

1. FBT derleme için hiçbir kullanıcı öneri yok.
2. Bu yöntem bir hata döndürür olacak FBT Hello etkin yapı ise.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| Kullanıcı Kimliği |Merhaba kullanıcının benzersiz tanıtıcısı |
| itemsIds |Merhaba öğeleri toorecommend için virgülle ayrılmış listesi. En fazla uzunluk: 1024 |
| numberOfResults |Gerekli sonuç sayısı |
| includeMetatadata |Gelecekte kullanmak, her zaman yanlış |
| apiVersion |1.0 |

**Yanıtı:**

HTTP durum kodu: 200

Merhaba yanıt önerilen öğe başına bir giriş içerir. Her giriş verileri aşağıdaki hello sahiptir:

* `Feed\entry\content\properties\Id`-Önerilen öğesi kimliği
* `Feed\entry\content\properties\Name`-Hello öğesinin adı.
* `Feed\entry\content\properties\Rating`-Hello öneri derecesi; daha yüksek numarası, daha yüksek güvenilirlik anlamına gelir.
* `Feed\entry\content\properties\Reasoning`-Öneri (örn. öneri açıklamaları) akıl.

12,1 yanıt örnekte bkz:

### <a name="127-get-user-recommendations--of-a-specific-build"></a>12.7. (Biri, belirli bir yapı) kullanıcı öneriler alın
Belli bir yapı türü "Öneri" kullanıcı öneriler alın.

Merhaba API (Merhaba belirli derlemede kullanılan) hello kullanıcı toohello kullanım geçmişine göre tahmin edilen madde listesini döndürür.

Not: FBT derleme için hiçbir kullanıcı öneri yok.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| Kullanıcı Kimliği |Merhaba kullanıcının benzersiz tanıtıcısı |
| numberOfResults |Gerekli sonuç sayısı |
| includeMetatadata |Gelecekte kullanmak, her zaman yanlış |
| Buildıd |Bu öneri istek kimliği toouse Hello derleme |
| apiVersion |1.0 |

**Yanıtı:**

HTTP durum kodu: 200

Merhaba yanıt önerilen öğe başına bir giriş içerir. Her giriş verileri aşağıdaki hello sahiptir:

* `Feed\entry\content\properties\Id`-Önerilen öğesi kimliği
* `Feed\entry\content\properties\Name`-Hello öğesinin adı.
* `Feed\entry\content\properties\Rating`-Hello öneri derecesi; daha yüksek numarası, daha yüksek güvenilirlik anlamına gelir.
* `Feed\entry\content\properties\Reasoning`-Öneri (örn. öneri açıklamaları) akıl.

12,1 yanıt örnekte bkz:

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a>12.8. Öğe listesi (belirli bir yapı) ile kullanıcı öneriler alın
Belirli bir yapı türü "Öneri" kullanıcı öneriler ve ek öğeler hello listesini alın.

Merhaba API hello kullanıcı toohello kullanım geçmişini ve hello ek öğeler listesi göre tahmin edilen madde listesini döndürür.

Not: Työnetici, FBT yapı için hiçbir kullanıcı önerilir.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| Kullanıcı Kimliği |Merhaba kullanıcının benzersiz tanıtıcısı |
| öğe kimliklerinin |Merhaba öğeleri toorecommend için virgülle ayrılmış listesi. En fazla uzunluk: 1024 |
| numberOfResults |Gerekli sonuç sayısı |
| includeMetatadata |Gelecekte kullanmak, her zaman yanlış |
| Buildıd |Bu öneri istek kimliği toouse Hello derleme |
| apiVersion |1.0 |

**Yanıtı:**

HTTP durum kodu: 200

Merhaba yanıt önerilen öğe başına bir giriş içerir. Her giriş verileri aşağıdaki hello sahiptir:

* `Feed\entry\content\properties\Id`-Önerilen öğesi kimliği
* `Feed\entry\content\properties\Name`-Hello öğesinin adı.
* `Feed\entry\content\properties\Rating`-Hello öneri derecesi; daha yüksek numarası, daha yüksek güvenilirlik anlamına gelir.
* `Feed\entry\content\properties\Reasoning`-Öneri (örn. öneri açıklamaları) akıl.

12,1 yanıt örnekte bkz:

## <a name="13-user-usage-history"></a>13. Kullanıcı Kullanım Geçmişi
Bir öneri model oluşturulmuş bir kez hello sistem hello derleme için kullanılan tooretrieve hello kullanıcı geçmişi (öğeleri ilişkili tooa belirli kullanıcı) izin verir.
Bu API izin tooretrieve hello kullanıcı geçmişi

Not: hello kullanıcı geçmişi yalnızca öneri derlemeler için şu anda büyük/küçük harf yok.

### <a name="131-retrieve-user-history"></a>13,1 kullanıcı geçmişi alma
Alma hello hello etkin kullanılan öğe listesi oluşturmak veya kullanıcı kimliği verilen hello için belirtilen hello oluşturabilirsiniz.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |Merhaba kullanıcı geçmişi hello etkin yapı için alın.<br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/>Yapı verilen Merhaba Hello kullanıcı geçmişini alma`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`<br/><br/>Örnek:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba hello modelinin benzersiz tanımlayıcısı. |
| Kullanıcı Kimliği |Merhaba hello kullanıcının benzersiz tanımlayıcısı. |
| Buildıd |İsteğe bağlı bir parametre hangi yapıdan hello kullanıcı geçmişi fetch olmalıdır tooindicate izin ver |
| apiVersion |1.0 |

**Yanıtı:**

HTTP durum kodu: 200

Merhaba yanıt önerilen öğe başına bir giriş içerir. Her giriş verileri aşağıdaki hello sahiptir:

* `Feed\entry\content\properties\Id`-Önerilen öğesi kimliği
* `Feed\entry\content\properties\Name`-Hello öğesinin adı.
* `Feed\entry\content\properties\Rating`-YOK.
* `Feed\entry\content\properties\Reasoning`-YOK.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get User History</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-05-26T15:32:47Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">CatalogItemsThatContainATokenEntity</title>
        <updated>2015-05-26T15:32:47Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Rating m:type="Edm.Double">0</d:Rating>
                <d:Reasoning m:type="Edm.String"/>
                <d:Metadata m:type="Edm.String"/>
                <d:FormattedRating m:type="Edm.Double" m:null="true"/>
            </m:properties>
        </content>
    </entry>
</feed>

## <a name="14-notifications"></a>14. Bildirimler
Hello sistemde kalıcı hata oluştuğunda azure Machine Learning önerileri bildirimleri oluşturur. 3 bildirim türleri şunlardır:

1. Derleme hatası: Bu bildirim için her derleme hatası tetiklenir.
2. Veri alma hatası: Bu bildirim işleme 100'den fazla hataları hello son 5 dakika içinde kullanım olaylarının modeli başına hello işleme sahip olduğumuz geldiğinde tetiklenir.
3. Biz 100'den fazla hataları hello son 5 dakika içinde bir öneri istekleri modeli başına hello işlenmesini varsa öneri tüketim hatası - Bu bildirim tetiklenir.

### <a name="141-get-notifications"></a>14.1. Bildirimleri alma
Tek bir model veya tüm modelleri için tüm hello bildirimleri alır.

| HTTP yöntemi | URI |
|:--- |:--- |
| AL |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Tüm modelleri için tüm bildirimleri alma:<br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br>Örneğin, belirli bir model için bildirimleri almak için:<br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |İsteğe bağlı parametre. Atlanırsa, tüm modelleri için tüm bildirim alırsınız. <br>Geçerli değer: hello modelinin benzersiz tanımlayıcısı. |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıtı:**

HTTP durum kodu: 200

OData XML

    hello response includes one entry per notification. Each entry has hello following data:
        * feed\entry\content\properties\UserName - Internal user name identification.
        * feed\entry\content\properties\ModelId - Model ID.
        * feed\entry\content\properties\Message - Notification message.
        * feed\entry\content\properties\DateCreated - Date that this notification was created in UTC format.
        * feed\entry\content\properties\NotificationType - Notification types. Values are BuildFailure, RecommendationFailure, and DataAquisitionFailure.

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of Notifications for a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-04T13:24:23Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'" />
        <entry>
                <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfNotificationsForAUserEntity</title>
            <updated>2014-11-04T13:24:23Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">515506bc-3693-4dce-a5e2-81cb3e8efb56@dm.com</d:UserName>
                    <d:ModelId m:type="Edm.String">967136e8-f868-4258-9331-10d567f87fae</d:ModelId>
                    <d:Message m:type="Edm.String">Build failed for user</d:Message>
                    <d:DateCreated m:type="Edm.String">2014-11-04T13:23:14.383</d:DateCreated>
                    <d:NotificationType m:type="Edm.String">BuildFailure</d:NotificationType>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="142-delete-model-notifications"></a>14.2. Model uyarılarını silme
Bir model için tüm okuma bildirimleri siler.

| HTTP yöntemi | URI |
|:--- |:--- |
| SİL |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br>Örnek:<br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| modelId |Merhaba modeli benzersiz tanıtıcısı |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

### <a name="143-delete-user-notifications"></a>14.3. Kullanıcı bildirimleri Sil
Tüm modelleri ilişkin tüm bildirimler siler.

| HTTP yöntemi | URI |
|:--- |:--- |
| SİL |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| Parametre Adı | Geçerli Değerler |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| İstek Gövdesi |YOK |

**Yanıt**:

HTTP durum kodu: 200

## <a name="15-legal"></a>15. Yasal Bilgiler
Bu belgede sağlanan "olarak-olan". URL ve diğer Internet Web sitesi başvuruları dahil olmak üzere bu belgede belirtilen bilgiler ve görüntüler bildirim yapılmadan değiştirilebilir.<br><br>
Burada açıklanan bazı örnekler yalnızca çizim için sağlanmıştır ve kurgusaldır. Gerçek bir ilişki veya bağlantı amaçlanmamıştır veya çıkarılmamalıdır.<br><br>
Bu belge, herhangi bir yasal hak ile herhangi bir Microsoft ürünü üzerinde tooany fikri mülkiyet sağlamaz. Kopyalayabilir ve bu belgeyi şirket içinde kullanmak başvuru amaçlıdır.<br><br>
© 2015 Microsoft. Tüm hakları saklıdır.

