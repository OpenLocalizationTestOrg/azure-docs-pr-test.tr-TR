---
title: aaaManage ilk API'nizi Azure API Management | Microsoft Docs
description: "Nasıl toocreate API'leri, işlemleri ekleyin ve API Management ile çalışmaya başlama öğrenin."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a>İlk API’nizi Azure API Management’te yönetme
## <a name="overview"> </a>Genel Bakış
Bu kılavuz size nasıl tooquickly Azure API Management'i kullanmaya başlayacağınızı ve ilk API çağrınızı yapmayı gösterir.

## <a name="concepts"> </a>Azure API Management nedir?
Azure API Management tootake herhangi bir arka uçtan kullanın ve temel alan tam özellikli bir API programını başlatın.

Yaygın senaryolar şunlardır:

* **Mobil altyapıyı koruma**: API anahtarlarına erişim geçişi sağlayarak, azaltma ile DOS saldırılarını önleyerek ya da JWT belirtecini doğrulama gibi gelişmiş güvenlik ilkelerini kullanarak mobil altyapıyı koruyun.
* **ISV iş ortağı ekosistemlerini etkinleştirme** hello Geliştirici üzerinden hızlı iş ortağı ekleme sunarak portal ve API cephesi toodecouple dahili uygulamalardan gelen derleme iş ortağı kullanımı için hazır değil.
* **Bir dahili API programı çalıştırma** hello kuruluş toocommunicate hello kullanılabilirliği ve son hakkında tooAPIs değişiklikleri için merkezi bir konumda sunarak, Kurumsal hesaplar temelinde erişim geçişi sağlayarak tüm temel alarak arasında güvenli bir kanalı API ağ geçidi hello ve arka uç hello.

Merhaba sistem bileşenleri aşağıdaki Merhaba oluşur:

* Merhaba **API ağ geçidi** hello uç noktası:
  
  * API çağrıları ve bunları tooyour arka uçlarını yönlendiren kabul eder.
  * API anahtarları, JWT belirteçleri, sertifikaları ve diğer kimlik bilgilerini doğrular.
  * Kullanım kotalarını ve oran limitlerini uygular.
  * Merhaba çalışma sırasında kod değişiklikleri olmadan API'nizi dönüştürür.
  * Ayarlandığında arka uç yanıtlarını önbelleğe kaydeder.
  * Analiz amaçlı çağrı meta verilerini günlüğe kaydeder.
* Merhaba **yayımcı portalına** API programınızı ayarladığınız hello yönetim arabirimidir. Bunu şunlar için kullanın:
  
  * API şeması tanımlama ya da içeri aktarma.
  * API'leri ürünler halinde paketleme.
  * Kota veya dönüşüm hello API'leri gibi ilkeleri ayarlayın.
  * Analizlerden öngörüler edinme
  * Kullanıcıları yönetme.
* Merhaba **Geliştirici Portalı** yapabileceği hello ana web varlığı görevi geliştiriciler için hizmet eder:
  
  * API belgelerini okuma.
  * Merhaba etkileşimli konsol üzerinden bir API'yi deneyin.
  * Bir hesap oluşturun ve tooget API anahtarları abone olabilirsiniz.
  * Kendi kullanımlarına ilişkin analize erişme.

## <a name="create-service-instance"> </a>API Management örneği oluşturma
> [!NOTE]
> toocomplete Bu öğretici bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][Azure Free Trial].
> 
> 

API Management ile çalışmanın hello ilk adımı toocreate bir hizmet örneği oluşturur. İçinde toohello oturum [Azure Portal] [ Azure Portal] tıklatıp **yeni**, **Web + mobil**, **API Management**.

![Yeni API Management örneği][api-management-create-instance-menu]

İçin **adı**, benzersiz bir alt etki alanı adı toouse hello hizmeti URL'sini belirtin.

İstenen hello seçin **abonelik**, **kaynak grubu** ve **konumu** hizmet Örneğiniz için.

Girin **Contoso Ltd.** hello için **kuruluş adı**ve e-posta adresinizi hello **yönetici e-posta** alan.

> [!NOTE]
> Bu e-posta adresi hello API Management sisteminden gelen bildirimler için kullanılır. Daha fazla bilgi için bkz: [nasıl tooconfigure bildirimleri ve e-posta şablonları Azure API Management'te][How tooconfigure notifications and email templates in Azure API Management].
> 
> 

![Yeni API Management hizmeti][api-management-create-instance-step1]

API Management hizmeti örnekleri üç katmanda kullanılabilir: Geliştirici, Standart ve Premium.

> [!NOTE]
> Merhaba Geliştirici katmanı, geliştirme, test ve pilot API programları yüksek kullanılabilirlik ilgili bir sorun olduğu için ' dir. Merhaba standart ve Premium katmanlar, daha fazla trafik ayrılmış birim sayısı toohandle ölçeklendirebilirsiniz. Merhaba standart ve Premium katmanlar, API Management hizmeti ile Merhaba çoğu işlem gücü ve performans sağlar. Bu öğreticiyi herhangi bir katmanı kullanarak tamamlayabilirsiniz. API Management katmanları hakkında daha fazla bilgi için bkz. [API Management fiyatlandırması][API Management pricing].
> 
> 

Tıklatın **oluşturma** toostart, hizmet örneği sağlama.

![Yeni API Management hizmeti][api-management-instance-created]

Merhaba hizmet örneği oluşturulduktan sonra hello sonraki adıma toocreate olduğunu veya bir API içeri aktarın.

## <a name="create-api"> </a>Bir API'yi içeri aktarma
Bir API, istemci uygulamasından çağrılabilen işlemler grubundan oluşur. API işlemleri yönlendirilirken tooexisting web hizmetleridir.

API'ler el ile oluşturulabilir (ve API’lere işlem eklenebilir) veya içeri aktarılabilir. Bu öğreticide, size Microsoft tarafından sağlanan ve Azure üzerinde barındırılan bir örnek hesaplayıcı web hizmeti için API hello alacak.

> [!NOTE]
> API oluşturma ve işlemleri el ile ekleme hakkında yönergeler için bkz [nasıl toocreate API'leri](api-management-howto-create-apis.md) ve [nasıl tooadd işlemleri tooan API](api-management-howto-add-operations.md).
> 
> 

API hello yayımcı Portalı'ndan yapılandırılır. tooreach, tıklatın **yayımcı portalına** hello hizmet araç çubuğundan.

![Yayımcı portalı][api-management-management-console]

tooimport hello hesaplayıcı API'sini, tıklatın **API'leri** hello gelen **API Management** sol hello ve ardından menüsünde **içeri aktarma API'si**.

![API’yi İçeri Aktar düğmesi][api-management-import-api]

Aşağıdaki adımları tooconfigure hello hesaplayıcı API'si hello gerçekleştirin:

1. Tıklatın **URL'den**, girin **http://calcapi.cloudapp.net/calcapi.json** hello içine **belirtim belgesi URL'si** metin kutusuna ve hello tıklatın **Swagger**  radyo düğmesi.
2. Tür **calc** hello içine **Web API'si URL soneki** metin kutusu.
3. Tıklatın hello **ürünler (isteğe bağlı)** kutusuna ve seçin **Starter**.
4. Tıklatın **kaydetmek** tooimport hello API.

![Yeni API ekle][api-management-import-new-api]

> [!NOTE]
> **API Management** şu anda içeri aktarma için Swagger belgesinin 1.2 ve 2.0 sürümünü destekler. [Swagger 2.0 belirtimi](http://swagger.io/specification) `host`, `basePath` ve `schemes` özelliklerinin isteğe bağlı olduğunu belirtse dahi, Swagger 2.0 belgeniz bu özellikleri **İÇERMELİDİR**; aksi takdirde içeri aktarılmaz. 
> 
> 

Merhaba API içeri aktarıldığında hello hello API için Özet sayfasında hello yayımcı Portalı'nda görüntülenir.

![API özeti][api-management-imported-api-summary]

Merhaba API bölümünde birden çok sekme bulunur. Merhaba **Özet** sekmesi, temel ölçümleri ve hello API hakkında bilgileri görüntüler. Merhaba [ayarları](api-management-howto-create-apis.md#configure-api-settings) sekme kullanılan tooview ve düzenleme hello API yapılandırmasını kullanılır. Merhaba [Operations](api-management-howto-add-operations.md) sekme kullanılan toomanage hello API'nin işlemlerini kullanılır. Merhaba **güvenlik** sekmesi, temel kimlik doğrulaması kullanarak hello arka uç sunucusu için kullanılan tooconfigure Ağ Geçidi kimlik doğrulaması olabilir veya [karşılıklı sertifika kimlik doğrulaması](api-management-howto-mutual-certificates.md)ve tooconfigure [ OAuth 2.0 kullanarak kullanıcı kimlik doğrulaması](api-management-howto-oauth2.md).  Merhaba **sorunları** sekmesi, Apı'lerinizi kullanan hello geliştiriciler tarafından bildirilen kullanılan tooview sorunları aynıdır. Merhaba **ürünleri** sekmesi bu API'yi içeren kullanılan tooconfigure hello ürünleri aynıdır.

Varsayılan olarak, her bir API Management örneği iki örnek ürün ile birlikte gelir:

* **Başlangıç**
* **Sınırsız**

Merhaba API içeri aktarılırken Bu öğreticide, toohello Starter ürün hello temel hesaplayıcı API'si eklenmiştir.

Sipariş toomake çağrıları tooan API'si, geliştiricilerin önce erişim tooit verir tooa ürün abone olmalısınız. Geliştiriciler hello Geliştirici Portalı'nda tooproducts abone olabilir ya da yöneticiler geliştiricileri tooproducts hello yayımcı portalında abone olabilirsiniz. Zaten abone tooevery ürün varsayılan olacak şekilde hello API Management örneği hello önceki adımları hello öğreticide oluşturduğunuz olduğundan, bir yönetici demektir.

## <a name="call-operation"></a>Hello Geliştirici portalından bir işlem çağırma
İşlemler uygun şekilde tooview sağlayan doğrudan hello Geliştirici portalından çağrılabilir ve bir API'nin işlemlerini hello test edin. Bu öğretici adımında hello temel hesaplayıcı API'SİNİN çağıracak **iki tamsayı Ekle** işlemi. Tıklatın **Geliştirici Portalı** hello hello menüden hello yayımcı portalının sağ üst.

![Geliştirici portalı][api-management-developer-portal-menu]

Tıklatın **API'leri** hello üst menüsünden ve ardından **temel hesaplayıcı** toosee hello kullanılabilir işlemleri.

![Geliştirici portalı][api-management-developer-portal-calc-api]

Merhaba örnek açıklamalarını ve hello API ve bu işlemi kullanacak hello geliştiriciler için belgeleri sağlayarak işlemlerini birlikte aktarılan parametreleri unutmayın. İşlemler el ile eklendiğinde de bu açıklamalar eklenebilir.

toocall hello **iki tamsayı Ekle** işlemi, tıklatın **deneyin**.

![Deneyin][api-management-developer-portal-calc-api-console]

Merhaba parametreler için bazı değerler girin veya hello Varsayılanları tutun ve ardından **Gönder**.

![HTTP Al][api-management-invoke-get]

Bir işlem çağrıldıktan sonra hello Geliştirici Portalı hello görüntüler **yanıt durumu**, hello **yanıt üstbilgilerini**ve tüm **yanıt içeriği**.

![Yanıt][api-management-invoke-get-response]

## <a name="view-analytics">.</a>Analizi görüntüleme
Temel hesaplayıcı, anahtar seçerek yayımcı portalına geri toohello için tooview analiz **Yönet** hello hello menüden hello Geliştirici portalının sağ üst.

![Yönet][api-management-manage-menu]

Merhaba hello yayımcı portalı için varsayılan görünüm olan hello **Pano**, API Management Örneğinize genel bir bakış sağlar.

![Pano][api-management-dashboard]

Vurgulu hello fare hello grafiği için üzerinden **temel hesaplayıcı** toosee hello belirli ölçümleri belirli bir süre için API hello hello kullanımı.

> [!NOTE]
> Grafiğinizde grafiğinizde satır görmüyorsanız, geri toohello Geliştirici portalına geçin ve hello API bazı çağrılar yapın, birkaç dakika bekleyin ve toohello panoya geri dönün.
> 
> 

Tıklatın **ayrıntıları görüntüle** tooview hello Özet sayfası hello görüntülenen hello ölçümleri daha büyük bir sürümü de dahil olmak üzere API.

![Analiz][api-management-mouse-over]

![Özet][api-management-api-summary-metrics]

Ayrıntılı Ölçümler ve raporlar için tıklatın **Analytics** hello gelen **API Management** hello sol menüsünde.

![Genel Bakış][api-management-analytics-overview]

Merhaba **Analytics** bölümü aşağıdaki dört sekme hello sahiptir:

* **Bir bakışta** genel kullanım ve sistem durumu ölçümleri yanı sıra üst geliştiriciler, en iyi ürünler, sık kullanılan API'ler ve sık kullanılan işlemleri hello sağlar.
* **Kullanım** sekmesi coğrafi bir temsil dahil olmak üzere API çağrıları ve bant genişliğine ilişkin ayrıntılı bir bakış sunar.
* **Durum**sekmesi durum kodları, önbellek başarı oranları, yanıt zamanları ve API ve hizmet yanıt zamanlarına odaklanır.
* **Etkinlik** geliştirici, ürün, API ve işleme göre belirli etkinlik hello detaya raporlar sağlar.

## <a name="next-steps"> </a>Sonraki adımlar
* Nasıl çok öğrenin[API'nizi oran sınırları ile koruma](api-management-howto-product-with-rules.md).

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
