---
title: aaaAdd CDN tooan Azure App Service | Microsoft Docs
description: "Bir içerik teslim ağı (CDN) tooan Azure uygulama hizmeti toocache ekleyin ve statik dosyalarınızı sunucularından Merhaba Dünya Kapat tooyour müşterilere teslim."
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 88b7fd884517279064472b804a6d1dc2921cbd24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-content-delivery-network-cdn-tooan-azure-app-service"></a>İçerik teslim ağı (CDN) tooan Azure uygulama hizmeti Ekle

[Azure içerik teslim ağı (CDN)](../cdn/cdn-overview.md) içerik toousers teslim stratejik olarak yerleştirilmiş konumlardaki tooprovide en yüksek verimlilik statik web içeriği önbelleğe alır. Hello CDN web uygulamanız üzerindeki sunucu yükü de azalır. Bu öğreticide gösterilmiştir nasıl tooadd Azure CDN tooa [Azure App Service'in web uygulamasında](app-service-web-overview.md). 

Merhaba giriş sayfası ile çalışan hello örnek statik HTML sitesinin şöyledir:

![Örnek uygulama ana sayfası](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

Öğrenecekleriniz:

> [!div class="checklist"]
> * CDN uç noktası oluşturma.
> * Önbelleğe alınan varlıkları yenileme.
> * Önbelleğe alınmış toocontrol sürümleri kullanım sorgu dizeleri.
> * Özel bir etki alanı hello CDN uç noktası için kullanın.

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğretici:

- [Git'i yükleyin](https://git-scm.com/)
- [Azure CLI 2.0 yükleyin](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-web-app"></a>Merhaba web uygulaması oluşturma

ile izleme hello karşılaşmayacağınızı toocreate hello web uygulaması [statik HTML Hızlı Başlangıç](app-service-web-get-started-html.md) hello aracılığıyla **Gözat toohello uygulama** adım.

### <a name="have-a-custom-domain-ready"></a>Özel bir etki alanına sahip olma

toocomplete hello özel etki alanı adım Bu öğreticinin tooown özel bir etki alanı gerekir ve etki alanı sağlayıcınızın (örneğin, GoDaddy) erişim tooyour DNS kayıt defteri sahip. Örneğin, için DNS girişleri tooadd `contoso.com` ve `www.contoso.com`, erişim tooconfigure hello DNS ayarlarını hello olmalıdır `contoso.com` kök etki alanı.

Bir etki alanı adı zaten yoksa, hello göz önünde bulundurun [uygulama hizmeti etki alanı öğretici](custom-dns-web-site-buydomains-web-app.md) kullanarak bir etki alanı toopurchase hello Azure portalı. 

## <a name="log-in-toohello-azure-portal"></a>Toohello Azure portalında oturum açın

Bir tarayıcı açın ve toohello gidin [Azure portal](https://portal.azure.com).

## <a name="create-a-cdn-profile-and-endpoint"></a>CDN profili ve uç noktası oluşturma

Sol gezinti hello seçin **uygulama hizmetleri**ve ardından hello oluşturulan hello uygulama [statik HTML Hızlı Başlangıç](app-service-web-get-started-html.md).

![App Service uygulaması hello Portalı'nda seçin](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

Merhaba, **uygulama hizmeti** sayfasında hello **ayarları** bölümünde, select **Ağ > yapılandırma Azure CDN uygulamanız için**.

![CDN hello Portalı'nda seçin](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

Merhaba, **Azure içerik teslim ağı** sayfasında, hello sağlayın **yeni uç nokta** hello tabloda belirtildiği gibi ayarlar.

![Profil ve uç hello Portalı'nda oluşturma](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| Ayar | Önerilen değer | Açıklama |
| ------- | --------------- | ----------- |
| **CDN profili** | myCDNProfile | Seçin **Yeni Oluştur** toocreate CDN profili. CDN profili, CDN uç hello ile koleksiyonudur aynı fiyatlandırma katmanı. |
| **Fiyatlandırma katmanı** | Standart Akamai | Merhaba [fiyatlandırma katmanı](../cdn/cdn-overview.md#azure-cdn-features) hello sağlayıcısı ve kullanılabilir özellikler belirtir. Bu öğreticide, standart Akamai kullanıyoruz. |
| **CDN uç noktası adı** | Merhaba azureedge.net etki alanında benzersiz olan herhangi bir ad | Merhaba etki alanındaki önbelleğe alınmış kaynaklarınıza erişen  *\<endpointname >. azureedge.net*.

**Oluştur**’u seçin.

Azure hello profil ve uç noktası oluşturur. Merhaba yeni uç nokta görünür hello **uç noktaları** listesini hello aynı sayfa ve onu sağlandığında hello durumudur **çalıştıran**.

![Listede yeni uç nokta](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-hello-cdn-endpoint"></a>Test hello CDN uç noktası

Verizon fiyatlandırma katmanını seçtiyseniz, uç noktayı yayma işlemi genellikle yaklaşık 90 dakika sürer. Akamai için, yayma işlemi birkaç dakika sürer

Merhaba örnek uygulaması olan bir `index.html` dosya ve *css*, *img*, ve *js* diğer statik varlıklarını içeren klasörleri. Tüm bu dosyaların yolları içerik Hello hello aynı hello CDN uç noktada. Örneğin, aşağıdaki URL'lere hello her ikisi de hello erişim *bootstrap.css* hello dosyasında *css* klasörü:

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

URL aşağıdaki tarayıcı toohello gidin:

```
http://<endpointname>.azureedge.net/index.html
```

![CDN'den sunulan örnek uygulama ana sayfası](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 Daha önce bir Azure web uygulamasında çalışan aynı sayfa hello bakın. Azure CDN hello kaynak web uygulamanızın varlıklar alınan ve bunları hello CDN uç noktasından hizmet

tooensure bu sayfayı hello CDN, yenileme hello sayfası önbelleğe alınır. Merhaba aynı varlık için bazen gerekli hello CDN toocache hello için istenen içerik iki ister.

Azure CDN profilleri ve uç noktaları oluşturma hakkında daha fazla bilgi için bkz. [Azure CDN kullanmaya başlama](../cdn/cdn-create-new-endpoint.md).

## <a name="purge-hello-cdn"></a>Merhaba CDN Temizle

Merhaba CDN kaynaklarını hello yaşam süresi (TTL) yapılandırmasını temel alarak hello kaynak web uygulamasından düzenli aralıklarla yeniler. Merhaba varsayılan TTL yedi gündür.

Bazen güncelleştirilmiş içerik toohello web uygulaması dağıttığınızda hello TTL sona erme--önce toorefresh hello CDN Örneğin, gerekebilir. bir yenileme tootrigger hello CDN kaynakları el ile temizleyebilirsiniz. 

Merhaba öğreticinin bu bölümünde bir değişiklik toohello web uygulaması dağıtma ve hello CDN tootrigger hello CDN toorefresh önbelleğini Temizle.

### <a name="deploy-a-change-toohello-web-app"></a>Bir değişiklik toohello web uygulaması dağıtma

Açık hello `index.html` dosya ve ekleme "-V2" hello aşağıdaki örnekte gösterildiği gibi toohello H1 başlığını: 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

Değişikliklerinizi kaydetmek ve toohello web uygulaması dağıtma.

```bash
git commit -am "version 2"
git push azure master
```

Dağıtım tamamlandıktan sonra Gözat toohello web uygulaması URL'si ve değiştirme hello bakın.

```
http://<appname>.azurewebsites.net/index.html
```

![Web uygulamasındaki başlıkta V2](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

Toohello CDN uç noktası URL'si hello giriş sayfası ve hello önbelleğe alınmış hello CDN sürümünde henüz dolmadığından olduğundan değişiklik hello görmüyorum göz atın. 

```
http://<endpointname>.azureedge.net/index.html
```

![CDN'deki başlıkta V2 yok](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-hello-cdn-in-hello-portal"></a>Merhaba CDN hello portalında Temizle

tootrigger CDN tooupdate önbelleğe alınan sürüm Merhaba, hello CDN Temizle.

Merhaba portal sol gezinti bölmesinde seçin **kaynak grupları**ve ardından web uygulamanız için (contoso.com) oluşturulan hello kaynak grubunu seçin.

![Kaynak grubu seçin](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

CDN uç noktanız kaynakların Hello listeden seçin.

![Uç nokta seçin](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

Merhaba hello üstündeki **Endpoint** sayfasında, **Temizleme**.

![Temizleme seçin](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

Merhaba içerik yolları toopurge istediğiniz girin. Bir tam dosya yolunu toopurge tek bir dosyayı veya bir yol kesimi toopurge geçirmek ve bir klasördeki tüm içeriği yenileyin. Değiştirdiğiniz beri `index.html`, hello yollarından biri olan emin olun.

Merhaba sayfasının Hello altında seçin **Temizleme**.

![Sayfayı temizleyin](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-hello-cdn-is-updated"></a>CDN güncelleştirilmiş bu hello doğrulayın

Merhaba temizleme isteği işleme, genellikle birkaç dakika tamamlanana kadar bekleyin. toosee hello geçerli durumu, select hello zil simgesine hello sayfanın üst kısmındaki hello. 

![Temizleme bildirimi](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

Toohello CDN uç noktası URL'si Gözat `index.html`, ve şimdi hello hello giriş sayfasında toohello başlık eklenen V2 bakın. Bu, hello CDN önbellek yenileninceye olduğunu gösterir.

```
http://<endpointname>.azureedge.net/index.html
```

![CDN'deki başlıkta V2](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

Daha fazla bilgi için bkz. [Azure CDN uç noktasını temizleme](../cdn/cdn-purge-endpoint.md). 

## <a name="use-query-strings-tooversion-content"></a>Sorgu dizeleri tooversion içeriği kullanın

Hello Azure CDN önbelleğe alma davranışı seçeneklerini aşağıdaki hello sunar:

* Sorgu dizelerini yoksay
* Sorgu dizeleri için önbelleğe almayı atla
* Her benzersiz URL'yi önbelleğe al 

ilk hello bunlardan yalnızca bir önbelleğe alınan sürümü hello URL'de hello sorgu dizesi bağımsız olarak bir varlık yok demektir hello varsayılan değerdir. 

Hello öğreticinin bu bölümünde her benzersiz URL'yi önbelleğe alma davranışını toocache hello değiştirin.

### <a name="change-hello-cache-behavior"></a>Merhaba önbellek davranışını değiştirme

Hello Azure portal'ın **CDN uç noktası** sayfasında, **önbellek**.

Seçin **her benzersiz URL'yi önbelleğe** hello gelen **sorgu dizesini önbelleğe alma davranışı** aşağı açılan liste.

**Kaydet**’i seçin.

![Sorgu dizesini önbelleğe alma davranışı seçin](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a>Benzersiz URL'lerin ayrı olarak önbelleğe alındığını doğrulayın

Bir tarayıcıda hello CDN uç noktada toohello giriş sayfasına gidin, ancak bir sorgu dizesi içerir: 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

Merhaba CDN "V2" Merhaba başlığına içeren hello geçerli uygulama, web içeriği döndürür. 

tooensure bu sayfayı hello CDN, yenileme hello sayfası önbelleğe alınır. 

Açık `index.html` değiştirip "V2" çok "V3" ve hello değişiklik dağıtın. 

```bash
git commit -am "version 3"
git push azure master
```

Bir tarayıcıda toohello CDN uç noktası URL'si ile yeni bir sorgu dizesi gibi Git `q=2`. Merhaba CDN hello geçerli alır `index.html` dosya ve "V3" görüntüler.  Ancak toohello CDN uç noktasıyla hello giderseniz `q=1` sorgu dizesi, "V2" konusuna bakın.

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![CDN'deki başlıkta V3, sorgu dizesi 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![CDN'deki başlıkta V2, sorgu dizesi 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

Bu çıktı, her sorgu dizesi farklı şekilde ele gösterir:

* q = 1 kullanıldı önce şekilde ön belleğe alınmış içeriği (V2) döndürülür.
* q = 2'dir yeni, böylece hello en son web uygulama içeriği alınır ve (V3) döndürdü.

Daha fazla bilgi için bkz. [Sorgu dizeleri içeren Azure CDN önbelleğe alma davranışını kontrol etme](../cdn/cdn-query-string.md).

## <a name="map-a-custom-domain-tooa-cdn-endpoint"></a>Bir özel etki alanı tooa CDN uç noktası eşleme

CNAME kaydı oluşturarak, özel etki alanı tooyour CDN uç noktası eşleme. Bir CNAME kaydı, bir kaynak etki alanı tooa hedef etki alanını eşleyen bir DNS özelliğidir. Örneğin, eşleyebilir `cdn.contoso.com` veya `static.contoso.com` çok`contoso.azureedge.net`.

Özel bir etki alanı yoksa, hello göz önünde bulundurun [uygulama hizmeti etki alanı öğretici](custom-dns-web-site-buydomains-web-app.md) kullanarak bir etki alanı toopurchase hello Azure portalı. 

### <a name="find-hello-hostname-toouse-with-hello-cname"></a>Merhaba hostname toouse hello CNAME ile Bul

Hello Azure portal'ın **Endpoint** sayfasında, emin olun **genel bakış** sol gezinti ve ardından hello hello seçili **+ özel etki alanı** hello sayfanın üst kısmındaki hello düğmesi.

![Özel Etki Alanı Ekle'yi seçin](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

Merhaba, **özel bir etki alanı ekleme** sayfaya, bir CNAME kaydı oluşturma hello uç noktası ana bilgisayar adı toouse bakın. Merhaba ana bilgisayar adı, CDN uç nokta URL'sini türetilmiş:  **&lt;EndpointName >. azureedge.net**. 

![Etki Alanı Ekle sayfası](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-hello-cname-with-your-domain-registrar"></a>Etki alanı kayıt şirketinizle Hello CNAME yapılandırın

Tooyour etki alanı kayıt şirketinizin web sitesine gidin ve DNS kayıtları oluşturmak için hello bölümünü bulun. Bunu, **Etki Alanı Adı**, **DNS** veya **Ad Sunucusu Yönetimi** gibi bir bölümde bulabilirsiniz.

Merhaba bölümü CNAME'ler yönetmek için bulunamıyor. CNAME, diğer ad veya alt etki alanları hello sözcüklerinin olup olmadığına bakın ve toogo tooan Gelişmiş Ayarları sayfası olabilirsiniz.

Seçilen alt eşleyen bir CNAME kaydı oluşturun (örneğin, **statik** veya **cdn**) toohello **uç noktası ana bilgisayar adı** hello portalında daha önce gösterilen. 

### <a name="enter-hello-custom-domain-in-azure"></a>Azure'da Hello özel etki alanı girin

Toohello iade **özel bir etki alanı ekleme** sayfasında ve hello alt etki alanı, hello iletişim kutusunda dahil olmak üzere, özel etki alanı adı girin. Örneğin, `cdn.contoso.com` girin.   
   
Azure hello CNAME kaydı için hello etki alanı adı girdiğiniz var olduğunu doğrular. Merhaba CNAME doğru ise, özel etki alanınız doğrulandı.

Merhaba Internet üzerinde hello CNAME kaydı toopropagate tooname sunucuları için zaman alabilir. Etki alanınızı hemen doğrulanmaz, birkaç dakika bekleyin ve yeniden deneyin.

### <a name="test-hello-custom-domain"></a>Test hello özel etki alanı

Bir tarayıcıda toohello gidin `index.html` özel etki alanınızı kullanarak dosya (örneğin, `cdn.contoso.com/index.html`) hello sonuç tooverify hello aynı olduğunda, doğrudan çok Git olarak`<endpointname>azureedge.net/index.html`.

![Özel etki alanı URL'si kullanan örnek uygulama ana sayfası](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

Daha fazla bilgi için bkz: [harita Azure CDN içerik tooa özel etki alanı](../cdn/cdn-map-content-to-custom-domain.md).

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Sonraki adımlar

Öğrendiklerinizi:

> [!div class="checklist"]
> * CDN uç noktası oluşturma.
> * Önbelleğe alınan varlıkları yenileme.
> * Önbelleğe alınmış toocontrol sürümleri kullanım sorgu dizeleri.
> * Özel bir etki alanı hello CDN uç noktası için kullanın.

Aşağıdaki hello toooptimize CDN performansı nasıl makaleler öğrenin:

> [!div class="nextstepaction"]
> [Azure CDN’de dosyaları sıkıştırarak performansı geliştirme](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [Azure CDN uç noktasında varlıkları önceden yükleme](../cdn/cdn-preload-endpoint.md)
