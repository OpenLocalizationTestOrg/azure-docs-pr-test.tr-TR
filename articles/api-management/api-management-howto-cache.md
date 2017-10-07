---
title: "Azure API Management tooimprove performansını önbelleğe alma aaaAdd | Microsoft Docs"
description: "API Management hizmeti çağrıları için nasıl tooimprove hello gecikme, bant genişliği kullanımını ve web hizmeti yükleme hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 056ab7cf788218327e30bd5c028b76e3b1977fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-caching-tooimprove-performance-in-azure-api-management"></a>Azure API Management'te önbelleğe alma tooimprove performans ekleme
API Management işlemleri yanıt önbelleğe alma için yapılandırılabilir. Yanıt önbelleğe alma, çok sık değişmeyen veriler için API gecikmesi, bant genişliği kullanımı ve web hizmeti yükünü önemli ölçüde azaltabilir.

Bu kılavuz size nasıl gösterir tooadd yanıt API için önbelleğe alma ve hello örnek Echo API işlemleri için ilkeleri yapılandırın. Merhaba işlemi hello Geliştirici Portalı tooverify önbelleğe alma eylemini öğesinden sonra çağırabilirsiniz.

> [!NOTE]
> Anahtar kullanım ilkesi ifadeleri hakkında daha fazla bilgi için bkz. [Azure API Management’te özel önbelleğe alma](api-management-sample-cache-by-key.md).
> 
> 

## <a name="prerequisites"></a>Ön koşullar
Bu kılavuzda aşağıdaki hello adımları önce bir API Management hizmeti örneği bir API ve yapılandırılmış bir ürününüz olmalıdır. Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.

## <a name="configure-caching"> </a>Önbelleğe almak için bir işlemi yapılandırma
Bu adımda, önbelleğe alma hello ayarları hello inceleyeceksiniz **GET kaynağı (önbelleğe alınmış)** hello örnek Echo API'SİNİN işlemi.

> [!NOTE]
> Her API Management hizmet örneği ile kullanılan tooexperiment ve API Management hakkında bilgi edinin bir Echo API'si ile önceden yapılandırılmış olarak gelir. Daha fazla bilgi için bkz. [Azure API Management'i kullanmaya başlama][Get started with Azure API Management].
> 
> 

başlatıldı, tooget tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda. Bu toohello API Management yayımcı portalına götürür.

![Yayımcı portalı][api-management-management-console]

Tıklatın **API'leri** hello gelen **API Management** sol hello ve ardından menüsünde **Echo API'si**.

![Echo API’si][api-management-echo-api]

Merhaba tıklatın **Operations** sekmesini ve sonra hello **GET kaynağı (önbelleğe alınmış)** hello işleminden **Operations** listesi.

![Echo API’si işlemleri][api-management-echo-api-operations]

Merhaba tıklatın **önbelleğe alma** sekmesini tooview hello ayarları bu işlem için önbelleğe alma.

![Önbelleğe alma sekmesi][api-management-caching-tab]

tooenable select hello bir işlem için önbelleğe alma **etkinleştirmek** onay kutusu. Bu örnekte, önbelleğe alma etkindir.

Her işlem yanıtı, hello içinde hello değerlere göre anahtarlanır **sorgu dizesi parametrelerine göre değişiklik gösterebilir** ve **üstbilgileri göre değişiklik gösterebilir** alanları. Sorgu dizesi parametreleri veya üst bilgileri temel alarak birden çok yanıtlarını toocache istiyorsanız, bunları bu iki alanda yapılandırabilirsiniz.

**Süre** hello hello önbelleğe alınan yanıtların sona erme aralığını belirtir. Bu örnekte, hello aralığıdır **3600** eşdeğer tooone saattir saniye.

Bu örnekte yapılandırma önbelleği hello kullanarak, ilk isteği toohello hello **GET kaynağı (önbelleğe alınmış)** işlemi hello arka uç hizmetinden bir yanıt döndürür. Bu yanıt, belirtilen hello tarafından önbelleğe alınır ve anahtarlanır üst bilgilerinin ve sorgu dize parametreleri. Parametreler, eşleşen toohello işlemi hello olacaktır sonraki çağrılar hello önbellek süresi aralığı sona erinceye kadar döndürülen yanıt önbelleğe alınmış.

## <a name="caching-policies"></a>Gözden geçirme hello önbelleğe alma ilkeleri
Bu adımda, hello ayarlarını önbelleğe alma hello gözden **GET kaynağı (önbelleğe alınmış)** hello örnek Echo API'SİNİN işlemi.

Ne zaman önbelleğe alma ayarları yapılandırıldığında hello üzerinde bir işlemi için **önbelleğe alma** sekmesinde, önbelleğe alma ilkeleri hello işlemi için eklenir. Bu ilkeler görüntülenebilir ve hello İlkesi Düzenleyicisi'nde düzenlenebilir.

Tıklatın **ilkeleri** hello gelen **API Management** hello sol ve ardından menüsünde **Echo API'si / GET kaynağı (önbelleğe alınmış)** hello gelen **işlemi**aşağı açılan liste.

![İlke kapsamı işlemi][api-management-operation-dropdown]

Bu, hello İlkesi Düzenleyicisi'nde hello ilkeleri bu işlem için görüntüler.

![API Management ilkesi düzenleyicisi][api-management-policy-editor]

Bu işlem için Hello ilke tanımı hello kullanılarak gözden geçirilen yapılandırma önbelleği hello tanımlayan hello ilkelerini içerir **önbelleğe alma** hello önceki adımda sekmesi.

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> Yapılan değişiklikler toohello önbelleğe alma ilkeleri hello İlkesi Düzenleyicisi'nde hello üzerinde yansıtılır **önbelleğe alma** bir işlemi ve tam tersini sekmesinde.
> 
> 

## <a name="test-operation"></a>Bir işlem çağırma ve hello önbelleğe almayı test etme
toosee hello önbelleğe alma eylemini, biz hello işlemi hello Geliştirici portalından çağırabilirsiniz. Tıklatın **Geliştirici Portalı** hello sağ üst menüsündeki içinde.

![Geliştirici portalı][api-management-developer-portal-menu]

Tıklatın **API'leri** hello üst menü ve ardından **Echo API'si**.

![Echo API’si][api-management-apis-echo-api]

> Yapılandırılmış tek bir API veya görünür tooyour hesabı, API'lere tıklamak sizi doğrudan bu API'nin toohello işlemlerine götürür varsa.
> 
> 

Select hello **GET kaynağı (önbelleğe alınmış)** işlemi ve ardından **açık Konsolu**.

![Konsolu açma][api-management-open-console]

Merhaba konsol hello Geliştirici portalından doğrudan tooinvoke işlemlere izin verir.

![Konsol][api-management-console]

Merhaba varsayılan değerleri tutun **param1** ve **param2**.

Select hello hello istediğiniz anahtarı **abonelik anahtarı** aşağı açılan liste. Hesabınızda yalnızca bir abonelik varsa, bu zaten seçilir.

Girin **sampleheader:value1** hello içinde **istek üst** metin kutusu.

Tıklatın **HTTP Get** ve yanıt üstbilgileri hello not edin.

Girin **sampleheader:value2** hello içinde **istek üst** metin kutusuna ve ardından **HTTP Get**.

Bu hello değeri Not **sampleheader** hala **value1** hello yanıt. Bazı farklı değerler deneyin ve önbelleğe alınan yanıt hello ilk çağrısından hello Not döndürülür.

Girin **25** hello içine **param2** alan ve ardından **HTTP Get**.

Bu hello değeri Not **sampleheader** hello yanıt sunulmuştur **value2**. Merhaba işlem sonuçları sorgu dizesi tarafından anahtarlandığından hello önceki önbelleğe alınan yanıt döndürülmedi.

## <a name="next-steps"> </a>Sonraki adımlar
* Önbelleğe alma ilkeleri hakkında daha fazla bilgi için bkz: [önbelleğe alma ilkeleri] [ Caching policies] hello içinde [API Management ilke başvurusu][API Management policy reference].
* Anahtar kullanım ilkesi ifadeleri hakkında daha fazla bilgi için bkz. [Azure API Management’te özel önbelleğe alma](api-management-sample-cache-by-key.md).

[api-management-management-console]: ./media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: ./media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: ./media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: ./media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: ./media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: ./media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: ./media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: ./media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: ./media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: ./media/api-management-howto-cache/api-management-console.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review hello caching policies]: #caching-policies
[Call an operation and test hello caching]: #test-operation
[Next steps]: #next-steps
