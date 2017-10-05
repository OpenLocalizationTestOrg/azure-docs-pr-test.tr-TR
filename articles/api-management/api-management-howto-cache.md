---
title: "Azure API Management performansını artırmak için önbelleğe alma ekleme | Microsoft Belgeleri"
description: "API Management hizmeti çağrıları için gecikme, bant genişliği kullanımı ve web hizmeti yüklerini geliştirmeyi öğrenin."
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
ms.openlocfilehash: 59c595f0d5ce849f44c46fdb6cab0b44d35fffa0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-caching-to-improve-performance-in-azure-api-management"></a>Azure API Management performansını artırmak için önbelleğe alma ekleme
API Management işlemleri yanıt önbelleğe alma için yapılandırılabilir. Yanıt önbelleğe alma, çok sık değişmeyen veriler için API gecikmesi, bant genişliği kullanımı ve web hizmeti yükünü önemli ölçüde azaltabilir.

Bu kılavuz size API’nize yanıt önbelleğe alma eklemeyi ve örnek Echo API işlemleri için ilkeleri yapılandırmayı gösterir. Böylece önbelleğe alma eylemini doğrulamak için işlemi geliştirici portalından çağırabilirsiniz.

> [!NOTE]
> Anahtar kullanım ilkesi ifadeleri hakkında daha fazla bilgi için bkz. [Azure API Management’te özel önbelleğe alma](api-management-sample-cache-by-key.md).
> 
> 

## <a name="prerequisites"></a>Ön koşullar
Bu kılavuzdaki adımları izlemeden önce, API ve ürün yapılandırılmış bir API Management hizmeti örneğine sahip olmalısınız. Henüz bir API Management hizmeti örneği oluşturmadıysanız, [Azure API Management'i kullanmaya başlama][Get started with Azure API Management] öğreticisinde [API Management hizmet örneği oluşturma][Create an API Management service instance]'ya bakın.

## <a name="configure-caching"> </a>Önbelleğe almak için bir işlemi yapılandırma
Bu adımda, örnek Echo API’sinin **GET Kaynağı (önbelleğe alınmış)** işleminin önbelleğe alma ayarlarını inceleyeceksiniz.

> [!NOTE]
> Her API Management hizmeti örneği, API Management’i denemek ve hakkında bilgi almak için kullanılabilecek bir Echo API’si ile önceden yapılandırılmış olarak gelir. Daha fazla bilgi için bkz. [Azure API Management'i kullanmaya başlama][Get started with Azure API Management].
> 
> 

Kullanmaya başlamak için API Management hizmetiniz için Azure Portal'da **Yayımcı portalı**’na tıklayın. Bu sizi API Management yayımcı portalına götürür.

![Yayımcı portalı][api-management-management-console]

Soldaki **API Management** menüsünde **API'ler**’e ve ardından **Echo API’si**’ne tıklayın.

![Echo API’si][api-management-echo-api]

**İşlemler** sekmesine tıklayın ve ardından **İşlemler** listesinde **GET Kaynağı (önbelleğe alınmış)** işlemine tıklayın.

![Echo API’si işlemleri][api-management-echo-api-operations]

Bu işlemin önbelleğe alma ayarlarını görüntülemek için **Önbelleğe alma**’ya tıklayın.

![Önbelleğe alma sekmesi][api-management-caching-tab]

Bir işlem için önbelleğe almayı etkinleştirmek üzere **Etkinleştir** onay kutusunu seçin. Bu örnekte, önbelleğe alma etkindir.

Her işlem, **Sorgu dizesi parametrelerine göre değişiklik gösterebilir** ve **Üst bilgilere göre değişiklik gösterebilir** alanlarındaki değerlere göre anahtarlanır ve bunları temel alır. Sorgu dizesi parametreleri veya üst bilgileri temel alan birden çok yanıtı önbelleğe almak istiyorsanız, bunları bu iki alanda yapılandırabilirsiniz.

**Süre** önbelleğe alınan yanıtların sona erme aralığını belirtir. Bu örnekte, aralık bir saate eşit olan **3600** saniyedir.

Bu örnekte önbelleğe alma yapılandırması kullanılarak, **GET Kaynağı (önbelleğe alınmış)** işlemine yapılan ilk istek işlemi arka uç hizmetinden bir yanıt döndürür. Bu yanıt, belirtilen üst bilgiler ve sorgu dizesi parametreleri tarafından önbelleğe alınır ve anahtarlanır. Eşleşen parametrelerle, işleme yapılan sonraki çağrılar, önbelleğe alma süresi aralığı sona erinceye kadar, önbelleğe alınan yanıtın döndürülmesini sağlar.

## <a name="caching-policies"> </a>Önbelleğe alma ilkelerini gözden geçirme
Bu adımda, örnek Echo API’sinin **GET Kaynağı (önbelleğe alınmış)** işleminin önbelleğe alma ayarlarını incelersiniz.

Bir işlem için **Önbelleğe alma** sekmesinde önbelleğe alma ayarları yapılandırıldığında, işlem için önbelleğe alma ilkeleri eklenir. Bu ilkeler ilke düzenleyicisinde görüntülenip düzenlenebilir.

Soldaki **API Management** menüsünde **İlkeler**’e tıklayın ve ardından **İşlem** açılır listesinde **Echo API’si / GET Kaynağı (önbelleğe alınmış)** öğesini seçin.

![İlke kapsamı işlemi][api-management-operation-dropdown]

Bu, bu işlemin ilkelerini ilke düzenleyicisinde görüntüler.

![API Management ilkesi düzenleyicisi][api-management-policy-editor]

Bu işlem için ilke tanımı, önceki adımda **Önbelleğe alma** sekmesi kullanılarak gözden geçirilen önbelleğe alma yapılandırmasını tanımlayan ilkeleri içerir.

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
> İlk düzenleyicisinde önbelleğe alma ilkelerinde yapılan değişiklikler işlemin **Önbelleğe alma** sekmesinde yansıtılır ve bu durumun tersi de geçerlidir.
> 
> 

## <a name="test-operation"> </a>İşlem çağırma ve önbelleğe almayı test etme
Önbelleğe alma eylemini görmek için, işlemi geliştirici portalından çağırabiliriz. Sağ üstteki menüde **Geliştirici Portalı**’na tıklayın.

![Geliştirici portalı][api-management-developer-portal-menu]

Üstteki menüde **API'ler**’e tıklayıp **Echo API’si**’ni seçin.

![Echo API’si][api-management-apis-echo-api]

> Yapılandırılmış ya da hesabınıza görünen yalnızca bir API’niz varsa, API’lere tıklamak sizi doğrudan bu API’nin işlemlerine götürür.
> 
> 

**GET Kaynağı (önbelleğe alınmış)** işlemini seçin ve ardından **Konsolu Aç**’a tıklayın.

![Konsolu açma][api-management-open-console]

Konsol, işlemleri doğrudan geliştirici portalından çağırmanızı sağlar.

![Konsol][api-management-console]

**param1** ve **param2** için varsayılan değerleri tutun.

**subscription-key** açılır listesinde istediğiniz anahtarı seçin. Hesabınızda yalnızca bir abonelik varsa, bu zaten seçilir.

**İstek üst bilgileri** metin kutusuna **sampleheader:value1** değerini girin.

**HTTP Al**’a tıklayın ve yanıt üst bilgilerini not edin.

**İstek üst bilgileri** metin kutusuna **sampleheader:value2** değerini girin ve ardından **HTTP Get**’e tıklayın.

**sampleheader** değerinin hala yanıttaki **value1** olduğuna dikkat edin. Bazı farklı değerler deneyin ve ilk çağrıya gelen önbelleğe alınan yanıtın döndürüldüğüne dikkat edin.

**param2** alanına **25** değerini girin ve ardından **HTTP Get**’e tıklayın.

Yanıttaki **sampleheader** değerinin artık **value2** olduğuna dikkat edin. İşlem sonuçları sorgu dizesi tarafından anahtarlandığından, önceki önbelleğe alınan yanıt döndürülmedi.

## <a name="next-steps"> </a>Sonraki adımlar
* Önbelleğe alma ilkeleri hakkında daha fazla bilgi için bkz. [API Management ilke başvurusunda][API Management policy reference] [Önbelleğe alma ilkeleri][Caching policies].
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


[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review the caching policies]: #caching-policies
[Call an operation and test the caching]: #test-operation
[Next steps]: #next-steps
