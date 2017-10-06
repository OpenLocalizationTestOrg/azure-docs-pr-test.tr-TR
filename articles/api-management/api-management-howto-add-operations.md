---
title: Azure API Management'te aaaHow tooadd operations tooan API | Microsoft Docs
description: "Bilgi nasıl Azure API Management'te tooadd işlemleri tooan API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 1158a023-1913-4e9c-93de-9164b672f9b3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: d57fa59a2b0ceb392cde23150a0cbb326e52d27d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-operations-tooan-api-in-azure-api-management"></a>Nasıl Azure API Management'te tooadd işlemleri tooan API
Bir API API Management kullanmadan önce operations eklenmesi gerekir. Bu kılavuzu gösterir nasıl tooadd ve API Management işlemleri tooan API farklı türlerde yapılandırın.

## <a name="add-operation"></a>Bir işlem ekleme
Operations eklenir ve tooan API hello yayımcı portalında yapılandırılır. tooaccess hello yayımcı portalı, tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda.

![Yayımcı portalı][api-management-management-console]

> Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.
> 
> 

Select hello istenen API hello yayımcı portalı ve ardından hello **Operations** sekmesi. 

![İşlemler][api-management-operations]

Tıklatın **ekleme işlemi** tooadd yeni işlem. Merhaba **yeni işlem** görüntülenir ve hello **imza** sekmesi varsayılan olarak seçilir.

![Ekleme işlemi][api-management-add-operation]

Merhaba belirtin **HTTP fiili** hello aşağı açılan listeden seçerek.

![HTTP yöntemi][api-management-http-method]

<a name="url-template"></a>

Bir veya daha fazla URL yolu kesimleri ve sıfır veya daha fazla sorgu dizesi parametreleri oluşan bir URL parçadaki yazarak Hello URL şablon tanımlayın. Merhaba URL şablonu, eklenmiş toohello temel URL'sini hello API, tek bir HTTP işlemi tanımlar. Daha fazla küme ayraçları tanımlanan değişken bölümleri adlı veya birini içerebilir. Bu değişken bölümleri şablon parametreleri olarak adlandırılır ve hello isteği hello API Yönetimi platformunuz tarafından işlendiğinde hello isteğin URL'den ayıklanan değerler dinamik olarak atanır.

> Merhaba URL şablon joker karakter düzenleri içerebilir. Örneğin, belirten `/*` tüm istekler bu HTTP yöntemini toohello için hizmet İleri sona erer.

![URL şablonu][api-management-url-template]

<a name="rewrite-url-template"></a>

İsterseniz, hello belirtin **URL yeniden yazma şablon**. Bu, toouse hello standart URL şablon hello ön uç üzerinde gelen istekleri işlemek için sayesinde, hello arka uç toohello göre dönüştürülen bir URL aracılığıyla çağrılırken şablonu yeniden yazın. Şablon parametreleri hello URL şablondan hello yeniden yazma şablonunda kullanılmalıdır. Merhaba aşağıdaki örnek hello önceki örnekteki hello web hizmeti yol kesimi hello bir sorgu parametresi olarak API hello hello URL şablonları kullanarak API Management platform yayımlanan sağlanabilir olarak kodlanmış nasıl içerik türünü gösterir.

![URL şablonu yeniden yazma][api-management-url-template-rewrite]

Arayanlar toohello işlemi hello biçimi kullanın `/customers?customerid=ALFKI` ve bu çok eşlenecek`/Customers('ALFKI')` hello arka uç hizmetine zaman çağrılır.

**Görüntü** adı ve **açıklama** hello işlemi bir açıklama belirtin ve kullanılan tooprovide belgelerine hello Geliştirici Portalı'nda bu API'yi kullanarak toohello geliştiricilerin önerilir.

![Açıklama][api-management-description]

Merhaba işlemi açıklama belirtilebilir düz metin veya HTML hello **açıklama** metin kutusu.

## <a name="operation-caching"></a>İşlemi önbelleğe alma
Yanıt önbelleğe alma düşürmeye bant genişliği tüketimi hello API tüketiciler tarafından algılanan gecikmesini azaltır ve hello HTTP web hizmeti uygulama düşüşleri hello yükle hello API. 

tooeasily ve hızlı bir şekilde select hello hello işlem için önbelleğe almayı etkinleştir **önbelleğe alma** sekmesinde ve hello denetleyin **etkinleştirmek** onay kutusu.

![Önbelleğe alma][api-management-caching-tab]

**Süre** hello sırasında hangi hello işlemi yanıt hello önbellekte kalır süreyi belirtir. Merhaba varsayılan değer 3600 saniye veya 1 saat olur.

Önbellek anahtarlarını yanıtları arasında kullanılan toodifferentiate içindir tooeach farklı önbellek anahtarını karşılık gelen hello yanıt kendi ayrı önbelleğe alınan değeri alır. İsteğe bağlı olarak, özel bir sorgu dizesi parametreleri ve/veya HTTP üstbilgileri toobe hello önbellek anahtar değerlerini bilgisayar kullanılan girin **sorgu dizesi parametrelerine göre değişiklik gösterebilir** ve **üstbilgileri göre değişiklik gösterebilir** metin kutuları sırasıyla. Ne zaman belirtilen, tam istek URL'si yok ve HTTP üstbilgi değerlerini aşağıdaki hello önbellek anahtar oluşturma kullanılır: **kabul** ve **Accept-Charset**.

> Önbelleğe alma ve önbelleğe alma ilkeleri hakkında daha fazla bilgi için bkz: [nasıl toocache işlemi Azure API Management'te sonuçları][How toocache operation results in Azure API Management].
> 
> 

## <a name="request-parameters"></a>Parametreleri
İşlem parametrelerini hello parametreleri sekmesinde yönetilir. Hello belirtilen parametreleri **URL şablonu** hello üzerinde **imza** sekmesinde otomatik olarak eklenir ve yalnızca hello URL şablonu düzenleyerek değiştirilebilir. Ek parametreler el ile girilebilir.

Yeni bir sorgu parametresi tooadd tıklatın **sorgu parametresi Ekle** ve aşağıdaki bilgilerle hello girin:

* **Ad** -parametre adı.
* **Açıklama** -hello parametre (isteğe bağlı) kısa bir açıklaması.
* **Tür** -hello açılan seçilen parametre türü.
* **Değerleri** -toothis parametresi atanabilir değerleri. Merhaba değerlerden birini varsayılan olarak (isteğe bağlı) işaretlenebilir.
* **Gerekli** -hello onay kutusunu işaretleyerek hello parametre zorunlu kılabilir. 

![İstek parametreleri][api-management-request-parameters]

## <a name="request-body"></a>İstek gövdesinde
Merhaba işlemi izin veriyorsa (örneğin, PUT, POST) ve onu hello tümünde örneği sağlayabilir gövde desteklenen gösterimi biçimleri (örneğin json, XML) gerektirir. 

> Merhaba istek gövdesi yalnızca belgeleri amaçlar için kullanılır ve doğrulanmazsa.
> 
> 

bir istek gövdesi tooenter geçiş toohello **gövde** sekmesi.

Tıklatın **eklemek gösterimi**, istenen içerik türü (örn. uygulama/json), adını yazarak Başlat'ı seçin, hello açılır ve Yapıştır hello istenen istek gövdesi örnek hello seçilen biçiminde hello metin kutusuna. 

![İstek gövdesi][api-management-request-body]

Ek toorepresentations içinde hello isteğe bağlı metnini açıklamada da belirtebilirsiniz **açıklama** metin kutusu.

## <a name="responses"></a>Yanıtları
Yanıtlar hello işlemi üretebilir tüm durum kodları için iyi bir uygulama tooprovide örnekleri olur. Birden fazla yanıt gövdesi örnek her durum koduna sahip olabilir, her hello desteklenen içerik türleri. 

tooadd bir yanıt tıklatın **Ekle** ve istenen hello durum kodu yazmaya başlayın. Bu örnek hello durum kodudur **200 Tamam**. Merhaba kod hello açılan listesinde görüntülendikten sonra seçin ve hello yanıt kodu oluşturulan ve eklenen tooyour işlemdir.

![Yanıt kodu][api-management-response-code]

Tıklatın **eklemek gösterimi**hello istediğiniz içerik türü adı (örn. uygulama/json) yazmaya başlayın ve ardından hello içinde açılır.

![Gövde içerik türü][api-management-response-body-content-type]

Merhaba yanıt gövdesi örneği hello seçili biçiminde hello metin kutusuna yapıştırın. 

![Yanıt gövdesi][api-management-response-body]

İsterseniz, isteğe bağlı bir açıklama hello içine ekleme **açıklama** metin kutusu.

Merhaba işlemi yapılandırıldıktan sonra tıklatın **kaydetmek**.

## <a name="next-steps"> </a>Sonraki adımlar
Merhaba işlemleri tooan API eklendikten sonra hello sonraki adıma tooassociate hello API bir ürüne sahip olan ve böylece geliştiriciler işlemlerini çağırabilirsiniz yayımlayın.

* [Nasıl toocreate ürün ve yayımlama][How toocreate and publish a product]

[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
