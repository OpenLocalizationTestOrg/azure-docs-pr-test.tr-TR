---
title: aaaProtect API'nizi Azure API Management ile | Microsoft Docs
description: "Bilgi nasıl tooprotect API'nizi kotalar ve azaltma (hız sınırlama) ilkeleri."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 450dc368-d005-401d-ae64-3e1a2229b12f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3113fd277d434da0c051b8b90fd629a102bf4867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a>API’nizi, Azure API Management kullanarak hız sınırlarıyla koruma | Microsoft Azure
Bu kılavuz size nasıl kolay tooadd koruma arka uç API'niz için Azure API Management ile hız sınırı ve kota ilkeleri yapılandırarak olduğunu gösterir.

Bu öğreticide geliştiricilerinin sağlayan "Ücretsiz deneme" API ürünü oluşturacaksınız toomake tooa maksimum 200 çağrı hello kullanarak hafta tooyour API başına yukarı too10 çağrıları dakikada kurup [abonelik başına çağrı hızını sınırla](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) ve [ Abonelik başına kullanım kotası ayarla](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) ilkeleri. Sonra yayımlama hello API ve hello hız sınırı ilkesini test.

Daha gelişmiş azaltma senaryoları hello için [anahtar tarafından hızı sınırı](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) ve [kota anahtarı](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) ilkeleri Bkz [Gelişmiş istek azaltma Azure API Management ile](api-management-sample-flexible-throttling.md).

## <a name="create-product"></a>toocreate bir ürün
Bu adımda, abonelik onayı gerektirmeyen bir Ücretsiz Deneme ürünü oluşturacaksınız.

> [!NOTE]
> Zaten yapılandırılmış bir ürününüz varsa ve toouse istediğiniz varsa, Bu öğretici için önceden çok atlayabilirsiniz[yapılandırma çağrı hızı sınırı ve kota ilkeleri] [ Configure call rate limit and quota policies] ve ürününüzü kullanarak buradan hello öğreticisini izleyin Merhaba ücretsiz deneme ürünü yerine.
> 
> 

başlatıldı, tooget tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda.

![Yayımcı portalı][api-management-management-console]

> Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [ilk API'nizi Azure API Management'te yönetme] [ Manage your first API in Azure API Management] Öğreticisi.
> 
> 

Tıklatın **ürünleri** hello içinde **API Management** hello sol toodisplay hello menüsünde **ürünleri** sayfası.

![Ürün ekleme][api-management-add-product]

Tıklatın **Ekle ürün** toodisplay hello **Ekle yeni ürün** iletişim kutusu.

![Yeni ürün ekleme][api-management-new-product-window]

Merhaba, **başlık** kutusuna **ücretsiz deneme**.

Merhaba, **açıklama** kutusu, metin aşağıdaki türü hello: **aboneleri mümkün toorun 10 çağrıları dakikada tooa en fazla 200 çağrı/hafta sonra erişim reddedildi yukarı olacaktır.**

API Management ürünleri açık ya da korumalı olabilir. Korumalı ürünlerin kullanılabilmesi için abone toobefore olması gerekir. Açık ürünler abonelik olmadan kullanılabilir. Emin **abonelik iste** seçili toocreate bir abonelik gerektiren korumalı bir üründür. Merhaba varsayılan ayar budur.

Bir yönetici tooreview istediğiniz ve kabul edin veya reddedin abonelik girişimleri toothis ürün varsa belirleyin **abonelik onayı iste**. Hello onay kutusu seçili değilse abonelik girişimleri otomatik olarak onaylanır. Bu örnekte, abonelik otomatik olarak, hello kutuyu işaretlemeyin şekilde onaylanır.

tooallow Geliştirici hesaplarını toosubscribe birden çok kez toohello yeni ürün, select hello **birden çok aboneliğe izin** onay kutusu. Bu öğretici aynı anda birden çok abonelik kullanmaz, bu nedenle onay kutusunu işaretlenmemiş olarak bırakın.

Tüm değerleri girdikten sonra tıklatın **kaydetmek** toocreate hello ürün.

![Ürün eklendi][api-management-product-added]

Varsayılan olarak, yeni ürünleri hello içinde görünür toousers olan **Yöneticiler** grubu. Biz tooadd hello kalacaklarını **geliştiriciler** grubu. ' I tıklatın **ücretsiz deneme**ve ardından hello **görünürlük** sekmesi.

> API Management'te, ürünlerin toodevelopers kullanılan toomanage hello görünürlüğünü gruplarıdır. Ürünler görünürlük toogroups vermek ve geliştiricilerin görüntülemek ve, ait oldukları görünür toohello grupları toohello ürünleri abone. Daha fazla bilgi için bkz: [nasıl toocreate ve kullanım grupları Azure API Management'te][How toocreate and use groups in Azure API Management].
> 
> 

![Geliştiriciler grubu ekleme][api-management-add-developers-group]

Select hello **geliştiriciler** onay kutusunu işaretleyin ve ardından **kaydetmek**.

## <a name="add-api"></a>tooadd bir API toohello ürün
Merhaba öğreticinin bu adımında, hello Echo API'si toohello yeni ücretsiz deneme ürünü ekleyeceğiz.

> Her API Management hizmet örneği ile kullanılan tooexperiment ve API Management hakkında bilgi edinin bir Echo API'si ile önceden yapılandırılmış olarak gelir. Daha fazla bilgi için bkz. [Azure API Management'te ilk API'nizi yönetme][Manage your first API in Azure API Management].
> 
> 

Tıklatın **ürünleri** hello gelen **API Management** sol hello ve ardından menüsünde **ücretsiz deneme** tooconfigure hello ürün.

![Ürünü yapılandırma][api-management-configure-product]

Tıklatın **API Ekle tooproduct**.

![API tooproduct Ekle][api-management-add-api]

**Echo API’si** seçeneğini belirleyin ve ardından **Kaydet**’e tıklayın.

![Echo API’si ekleme][api-management-add-echo-api]

## <a name="policies"></a>tooconfigure çağrı hızı sınırı ve kota ilkeleri
Oran sınırları ve kotalar hello İlkesi Düzenleyicisi'nde yapılandırılır. Biz ekleyerek bu öğreticide hello iki ilkelerdir hello [abonelik başına çağrı hızını sınırla](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) ve [abonelik başına kullanım kotası ayarla](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) ilkeleri. Bu ilkeler hello ürün kapsamda uygulanmış olması gerekir.

Tıklatın **ilkeleri** hello altında **API Management** hello sol menüsünde. Merhaba, **ürün** tıklatın **ücretsiz deneme**.

![Ürün ilkesi][api-management-product-policy]

Tıklatın **ilke Ekle** tooimport hello ilkesi şablonunu ve hello hız sınırı ve kota ilkeleri oluşturmaya başlamak.

![İlke ekleme][api-management-add-policy]

Hız sınırı ve kota ilkeleri gelen hello gelen öğesindeki bunu konumu hello imleç ilkeleridir.

![İlke düzenleyicisi][api-management-policy-editor-inbound]

İlkeleri hello listesini kaydırın ve hello bulun **abonelik başına çağrı hızını sınırla** İlkesi girişi.

![İlke deyimleri][api-management-limit-policies]

Merhaba sonra imleç hello konumlandırıldı **gelen** ilke öğesi hello yanındaki oka **abonelik başına çağrı hızını sınırla** tooinsert kendi ilke şablonunu.

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

Merhaba parçacığı görebileceğiniz gibi hello İlkesi sınırlarını ayarlama hello ürünün API'ler ve işlemler için sağlar. Bu öğreticide biz değil Bu özelliği kullanın, böylece hello silme **API** ve **işlemi** hello öğelerinden **hızı sınırı** öğesi, yalnızca dış hellogibi**hızı sınırı** hello aşağıdaki örnekte gösterildiği gibi öğe kalır.

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

Merhaba Ücretsiz Deneme ürününde hello izin verilen maksimum çağrı hızı dakikada 10 çağrı olan, bu nedenle **10** hello hello değeri olarak **çağrıları** özniteliği ve **60** hello için**yenileme süresini** özniteliği.

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

tooconfigure hello **abonelik başına kullanım kotası ayarla** ilke, konum imlecinizi hello hemen altında yeni eklenen **hızı sınırı** öğesi hello içinde **gelen** öğesini ve ardından bulup hello ok toohello solundaki tıklayın **abonelik başına kullanım kotası ayarla**.

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

Benzer şekilde toohello **abonelik başına kullanım kotası ayarla** İlkesi **abonelik başına kullanım kotası ayarla** ilke verir hello ürünün API'ler ve işlemler büyük harfler için ayarlama. Bu öğreticide biz değil Bu özelliği kullanın, böylece hello silme **API** ve **işlemi** hello öğelerinden **kota** hello aşağıdaki örnekte gösterildiği gibi öğesi.

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

Kotalar hello başına çağrı sayısı aralık, bant genişliği veya her ikisini temel alabilir. Bu öğreticide, biz bant genişliği temelinde azaltma yapmıyoruz, bu nedenle hello silme **bant genişliği** özniteliği.

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

Merhaba Ücretsiz Deneme ürününde hello kota haftada 200 çağrı ' dir. Belirtin **200** hello hello değeri olarak **çağrıları** özniteliği ve ardından belirtin **604800** hello hello değeri olarak **yenileme süresini** özniteliği.

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> İlke aralıkları saniye cinsinden belirtilir. toocalculate hello aralığı bir hafta hello hello (60)'hello bir dakikadaki (60) saniye sayısı'e kadar bir saatteki dakika sayısı (24) günde saat sayısını (7) günlere hello sayısı Çarp: 7 * 24 * 60 * 60 = 604800.
> 
> 

Merhaba ilke yapılandırmayı tamamladığınızda, aşağıdaki örneğine hello eşleşmelidir.

```xml
<policies>
    <inbound>
        <rate-limit calls="10" renewal-period="60">
        </rate-limit>
        <quota calls="200" renewal-period="604800">
        </quota>
        <base />

</inbound>
<outbound>

    <base />

    </outbound>
</policies>
```

İlkeleri yapılandırılır Hello istenen sonra tıklayın **kaydetmek**.

![İlkeyi kaydetme][api-management-policy-save]

## <a name="publish-product"></a> toopublish hello ürün
Böylece geliştiriciler tarafından kullanılan hello hello API'ler eklenmiştir ve hello ilkelerin yapılandırıldığına göre hello ürünün yayımlanması gerekir. Tıklatın **ürünleri** hello gelen **API Management** sol hello ve ardından menüsünde **ücretsiz deneme** tooconfigure hello ürün.

![Ürünü yapılandırma][api-management-configure-product]

Tıklatın **Yayımla**ve ardından **Evet, Yayımla** tooconfirm.

![Ürünü yayımlama][api-management-publish-product]

## <a name="subscribe-account"></a>toosubscribe bir geliştirici hesabı toohello ürün
Merhaba ürünün yayımlanan artık, geliştiriciler tarafından kullanılan abone kullanılabilir toobe tooand olur.

> Bir API Management örneğinin yöneticileri otomatik olarak abone tooevery ürün olur. Bu öğretici adımında, biz hello yönetici olmayan Geliştirici hesaplarını toohello ücretsiz deneme ürünü birini abone olur. Geliştirici hesabınızda hello Yöneticiler rolünün bir parçası ise, zaten abone olmanıza rağmen bu adımın üzerinden izleyebilirsiniz.
> 
> 

Tıklatın **kullanıcılar** hello üzerinde **API Management** hello menüsünde sol ve ardından Geliştirici hesabınızın hello adına tıklayın. Bu örnekte, hello kullanıyoruz **Clayton Gragg** Geliştirici hesabı.

![Geliştirici yapılandırma][api-management-configure-developer]

**Abonelik Ekle**’ye tıklayın.

![Abonelik ekleme][api-management-add-subscription-menu]

**Ücretsiz Deneme**’yi seçin ve ardından **Abone ol**’a tıklayın.

![Abonelik ekleme][api-management-add-subscription]

> [!NOTE]
> Bu öğreticide, birden çok aboneliğe hello ücretsiz deneme ürünü için etkin değil. Etkin olsaydı hello aşağıdaki örnekte gösterildiği gibi istendiğinde tooname hello abonelik olacaktır.
> 
> 

![Abonelik ekleme][api-management-add-subscription-multiple]

' I tıklattıktan sonra **abone ol**, hello ürün görünür hello **abonelik** hello kullanıcıya listesi.

![Abonelik eklendi][api-management-subscription-added]

## <a name="test-rate-limit"></a>toocall bir işlemi ve test hello hızı sınırı
Merhaba ücretsiz deneme ürünü yayımlanmış ve yapılandırılmış olduğuna göre biz bazı işlemler çağırabilir ve hello hız sınırı ilkesini test.
Anahtar toohello Geliştirici Portalı'ı tıklatarak **Geliştirici Portalı** hello sağ üst menüsünde.

![Geliştirici portalı][api-management-developer-portal-menu]

Tıklatın **API'leri** hello üst menü ve ardından **Echo API'si**.

![Geliştirici portalı][api-management-developer-portal-api-menu]

**GET Kaynağı**’na ve ardından **Deneyin**’e tıklayın.

![Konsolu açma][api-management-open-console]

Merhaba varsayılan parametre değerlerini koruyun ve ardından hello ücretsiz deneme ürünü için abonelik anahtarınızı seçin.

![Abonelik anahtarı][api-management-select-key]

> [!NOTE]
> Birden çok aboneliğiniz varsa, emin tooselect hello anahtarı olması **ücretsiz deneme**, veya hello önceki adımlarda yapılandırılmış başka hello ilkeleri etkili olmayacak.
> 
> 

Tıklatın **Gönder**ve ardından hello yanıtı görüntüleyin. Not hello **yanıt durumu** , **200 Tamam**.

![İşlem sonuçları][api-management-http-get-results]

Tıklatın **Gönder** dakikada 10 çağrı hello hız sınır ilkesinden daha büyük bir hızda. Merhaba hız sınırı İlkesi aşıldıktan sonra yanıt durumu **429 çok fazla istek** döndürülür.

![İşlem sonuçları][api-management-http-get-429]

Merhaba **yanıt içeriği** hello yeniden denemeler başarılı olmadan önce kalan aralığı gösterir.

Dakikada 10 çağrı Hello hız sınırı ilkesi etkinken, hello 60 saniye geçinceye kadar sonraki çağrılar başarısız olur hello hız sınırı aşılmadan önce hello 10 başarılı çağrının toohello ürünün ilk. Bu örnekte, aralık kalan hello 54 saniyedir.

## <a name="next-steps"> </a>Sonraki adımlar
* Video aşağıdaki hello oran sınırlarını ve kotaları ayarlama gösterisini izleyin.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-product-with-rules/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-product-with-rules/api-management-add-product.png
[api-management-new-product-window]: ./media/api-management-howto-product-with-rules/api-management-new-product-window.png
[api-management-product-added]: ./media/api-management-howto-product-with-rules/api-management-product-added.png
[api-management-add-policy]: ./media/api-management-howto-product-with-rules/api-management-add-policy.png
[api-management-policy-editor-inbound]: ./media/api-management-howto-product-with-rules/api-management-policy-editor-inbound.png
[api-management-limit-policies]: ./media/api-management-howto-product-with-rules/api-management-limit-policies.png
[api-management-policy-save]: ./media/api-management-howto-product-with-rules/api-management-policy-save.png
[api-management-configure-product]: ./media/api-management-howto-product-with-rules/api-management-configure-product.png
[api-management-add-api]: ./media/api-management-howto-product-with-rules/api-management-add-api.png
[api-management-add-echo-api]: ./media/api-management-howto-product-with-rules/api-management-add-echo-api.png
[api-management-developer-portal-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-menu.png
[api-management-publish-product]: ./media/api-management-howto-product-with-rules/api-management-publish-product.png
[api-management-configure-developer]: ./media/api-management-howto-product-with-rules/api-management-configure-developer.png
[api-management-add-subscription-menu]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-menu.png
[api-management-add-subscription]: ./media/api-management-howto-product-with-rules/api-management-add-subscription.png
[api-management-developer-portal-api-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-api-menu.png
[api-management-open-console]: ./media/api-management-howto-product-with-rules/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-product-with-rules/api-management-http-get.png
[api-management-http-get-results]: ./media/api-management-howto-product-with-rules/api-management-http-get-results.png
[api-management-http-get-429]: ./media/api-management-howto-product-with-rules/api-management-http-get-429.png
[api-management-product-policy]: ./media/api-management-howto-product-with-rules/api-management-product-policy.png
[api-management-add-developers-group]: ./media/api-management-howto-product-with-rules/api-management-add-developers-group.png
[api-management-select-key]: ./media/api-management-howto-product-with-rules/api-management-select-key.png
[api-management-subscription-added]: ./media/api-management-howto-product-with-rules/api-management-subscription-added.png
[api-management-add-subscription-multiple]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-multiple.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How toocreate and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers tooa product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API toohello product]: #add-api
[Publish hello product]: #publish-product
[Subscribe a developer account toohello product]: #subscribe-account
[Call an operation and test hello rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
