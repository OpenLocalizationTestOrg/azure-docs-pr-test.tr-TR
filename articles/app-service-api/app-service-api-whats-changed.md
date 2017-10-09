---
title: "aaaApp hizmeti API uygulamaları - Değiştirilenler | Microsoft Docs"
description: "Azure uygulama hizmetinde API uygulamaları için yenilikleri öğrenin."
services: app-service\api
documentationcenter: .net
author: mohitsriv
manager: erikre
editor: tdykstra
ms.assetid: a9b58066-e8fd-48b8-a651-4613b1736433
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: rachelap
ms.openlocfilehash: 79df54f1dae91d7c5d3b66d208d0d1c1d7d55ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-api-apps---whats-changed"></a>App Service API Apps - Değiştirilenler
Kasım 2015'te Hello Connect() olay, bir dizi geliştirmeleri tooAzure uygulama hizmeti olan [Duyuruldu](https://azure.microsoft.com/blog/azure-app-service-updates-november-2015/). Bu geliştirmeler tooAPI uygulamaları toobetter mobil ve Web uygulamaları ile align, kavram sayısını azaltın ve dağıtım ve çalışma zamanı performansı temel değişiklikleri içerir. 30 Kasım 2015 yeni API uygulamaları başlatma hello Azure yönetim portalını kullanarak oluşturduğunuz veya hello son araç bu değişiklikleri yansıtır. Bu makalede bu değişiklikler de nasıl açıklanır tooredeploy mevcut uygulamaları tootake yeteneklerinden hello.

## <a name="feature-changes"></a>Özellik değişiklikleri
doğrudan uygulama hizmetinde API uygulamaları – kimlik doğrulaması, CORS ve API meta verilerini – temel özellikleri Hello taşınmış. Bu değişiklikle hello özellikleri Web, mobil ve API uygulamaları kullanılabilir. Aslında, tüm üç paylaşımı hello aynı **Microsoft.Web/sites** Kaynak Yöneticisi'nde kaynak türü. Merhaba API uygulamaları ağ geçidi artık gerekli veya API uygulamaları ile sunulan. Yalnızca hello tek API Yönetimi ağ geçidi olacağından bu aynı zamanda, daha kolay toouse Azure API Management kolaylaştırır.

![API Apps'e genel bakış](./media/app-service-api-whats-changed/api-apps-overview.png)

Tooenable API uygulamaları güncelleştirme hello ile temel tasarım ilkesidir API'nizi olarak değil, seçim dilinizde toobring.  API'nizi zaten bir Web uygulaması veya mobil uygulama dağıtılırsa, uygulama tootake hello yeni özelliklerden tooredeploy yok. API Apps Önizleme'şu anda varsa, Geçiş Kılavuzu aşağıda ayrıntılı olarak verilmiştir.

### <a name="authentication"></a>Kimlik Doğrulaması
Hello varolan anahtar teslimi API Apps, Mobile Services/uygulamaları ve Web uygulamaları kimlik doğrulama özellikleri birleşik ve tek bir Azure App Service kimlik doğrulama dikey hello Yönetim Portalı'nda mevcuttur. App Service'te bir giriş tooauthentication Hizmetleri için bkz: [genişletme App Service kimlik doğrulama / yetkilendirme](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/).

API senaryoları için birkaç ilgili yeni özellikleri vardır:

* **Azure Active Directory kullanarak doğrudan desteği**, istemci kodu tooexchange hello AAD belirtecini Oturum belirteci için sahip olmadan: istemci yalnızca hello AAD belirteçleri hello yetkilendirme üstbilgisinde toohello taşıyıcı belirteci göre içerebilir belirtimi. Bu, ayrıca uygulama hizmete özgü SDK hello istemci veya sunucu tarafında gerekli anlamına gelir. 
* **Hizmetten hizmete veya "Dahili" erişim**: arka plan programı işlemi veya erişim tooAPIs bir arabirimi olmadan gerektiren başka bir istemci varsa, bir AAD hizmet sorumlusu kullanarak bir belirteç istemek ve tooApp hizmet kimlik doğrulaması için geçirin ile uygulama.
* **Yetkilendirme ertelenmiş**: Merhaba uygulaması farklı kısımlarını değişen erişim kısıtlamalarını birçok uygulama sahip. Belki başkalarının oturum açma gerektirirken genel kullanıma açık, bazı API toobe istiyor. Merhaba özgün kimlik doğrulama/yetkilendirme özelliğini oturum açma gerektiren hello tüm sitesiyle ya hep ya hiç,. Bu seçenek hala var, ancak uygulama hizmeti hello kullanıcı kimliğini doğrulamasından sonra alternatif olarak, uygulama kodunuzun toorender erişim kararları izin verebilirsiniz.

Merhaba yeni kimlik doğrulama özellikleri hakkında daha fazla bilgi için bkz: [kimlik doğrulama ve yetkilendirme Azure uygulama hizmetinde API uygulamaları için](app-service-api-authentication.md). Toomigrate varolan API uygulamaları hello önceki API uygulamalardan toohello yeni bir, bkz: nasıl modeli hakkında bilgi için [geçiş varolan API uygulamaları](#migrating-existing-api-apps) bu makalenin ilerisinde yer.

### <a name="cors"></a>CORS
Virgülle ayrılmış yerine **MS_CrossDomainOrigins** uygulama ayarı yok şimdi bir dikey pencere CORS yapılandırma hello Azure Yönetim Portalı'nda. Alternatif olarak, Kaynak Yöneticisi'ni CLI Azure PowerShell gibi araçları kullanarak yapılandırılabilir veya [kaynak Gezgini](https://resources.azure.com/). Set hello **cors** hello özellikte **Microsoft.Web/sites/config** kaynak türü için  **&lt;site adı&gt;/web** kaynak. Örneğin:

    {
        "cors": {
            "allowedOrigins": [
                "https://localhost:44300"
            ]
        }
    } 

### <a name="api-metadata"></a>API meta verileri
Merhaba API tanımı dikey Web, mobil ve API uygulamaları kullanıma sunulmuştur. Merhaba Yönetim Portalı'nda, göreli bir url veya tooan endpoint API'nizi o ana Swagger 2.0 gösterimini işaret eden mutlak bir url belirtebilirsiniz. Alternatif olarak, kaynak yöneticisi araçları kullanılarak yapılandırılabilir. Set hello **apiDefinition** hello özellikte **Microsoft.Web/sites/config** kaynak türü için  **&lt;site adı&gt;/web** kaynak. Örneğin:

    {
        "apiDefinition":
        {
            "url": "https://myStorageAccount.blob.core.windows.net/swagger/apiDefinition.json"
        }
    }

Şu anda hello meta veri uç noktasının toobe kimlik doğrulaması olmadan genel olarak erişilebilir birçok aşağı akış istemcileri (örn. Visual Studio REST API İstemci oluşturma ve PowerApps "API Ekle" akış) tooconsume için gereken bu. Bu, App Service kimlik doğrulaması kullanıyorsanız ve tooexpose hello API tanımı, uygulamanızın içinde istiyorsanız hello rota tooyour Swagger meta verileri ortak böylece daha önce açıklanan toouse hello ertelenmiş kimlik doğrulaması seçeneği gerekir anlamına gelmez.

## <a name="management-portal"></a>Yönetim Portalı
Seçme **yeni > Web + mobil > API uygulaması** hello portal hello yeni özellikler hello makalesinde açıklanan yansıtacak API uygulamaları oluşturur. **Gözat > API uygulamaları** bu yeni API uygulamaları yalnızca Göster olur. API uygulamaya Gözat sonra hello dikey paylaşımları aynı düzeni ve bu Web ve mobil uygulamaları olarak yetenekleri hello. Hello yalnızca farklar hızlı başlangıç içeriği ve ayarları sıralama ' dir.

Varolan API uygulamaları (veya mantığı uygulamalardan oluşturulan Market API uygulamaları) ile Merhaba önceki Önizleme özellikleri hala kaynak grubundaki tüm kaynakların göz atarken görünür hello Logic Apps Tasarımcısı'nda ve olacaktır.

## <a name="visual-studio"></a>Visual Studio
Çoğu Web Araçları, yeni API uygulamaları ile çalışır, paylaştıkları beri uygulamaları hello aynı temel **Microsoft.Web/sites** kaynak türü. Hello Azure Visual Studio Araçları, ancak, yükseltilen tooversion 2.8.1 ile olmalıdır veya bu yana sonraki yetenekleri belirli tooAPIs sayısını kullanıma sunar. Hello Hello SDK Yükle [Azure indirmeler sayfası](https://azure.microsoft.com/downloads/).

Yayımlama Hello yeterli duruma getirilmesi, uygulama hizmet türleri hello ile aynı zamanda altında birleşik **Yayımla > Microsoft Azure App Service**:

![API uygulamaları yayımlama](./media/app-service-api-whats-changed/api-apps-publish.png)

SDK 2.8.1 ile okuma hello duyuru hakkında daha fazla toolearn [blog gönderisi](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/).

Alternatif olarak, el ile Merhaba içeri aktarabilirsiniz yayımlama hello Yönetim Portalı tooenable profilinden yayımlayın. Ancak, SDK 2.8.1 ile bulut Gezgini, kod oluşturma ve API uygulaması seçimi/oluşturma gerektirir ya da daha yüksek.

## <a name="migrating-existing-api-apps"></a>Varolan API uygulamaları geçirme
Özel API'nizi dağıtılan toohello önceki Önizleme sürümü API uygulamaları ise, 31 Aralık 2015 tarafından API uygulamaları için toohello yeni model geçirme isteyin. App Service içinde barındırılan Web API'leri hem hello eski ve yeni model dayalı olduğundan, var olan kodu hello çoğunluğu yeniden kullanılabilir.

### <a name="hosting-and-redeployment"></a>Barındırma ve yeniden dağıtım
hello adımları yükleyecek olan hello varolan tüm Web API tooApp hizmet dağıtma aynı. adımlar:

1. Boş bir API uygulaması oluşturun. Bu yeni ile Merhaba portalında yapılabilir > Yayımla veya Kaynak Yöneticisi Araçları Visual Studio API uygulaması. Kaynak Yöneticisi Araçları veya şablonları kullanıyorsanız, hello ayarlamak **türü** çok değer**API** hello üzerinde **Microsoft.Web/sites** kaynak türü toohave hello quickstarts ve ayarları API senaryolarında yönelik hello Yönetim Portalı.
2. Bağlanmak ve App Service tarafından desteklenen hello dağıtım düzenekleri birini kullanarak proje toohello boş API uygulamasına dağıtabilirsiniz. Okuma [Azure uygulama hizmeti dağıtım belgeleri](../app-service-web/web-sites-deploy.md) toolearn daha fazla. 

### <a name="authentication"></a>Kimlik Doğrulaması
Merhaba App Service kimlik doğrulama hizmetleri desteği hello hello önceki API uygulamaları modeliyle kullanılabilir aynı yetenekleri. Oturum belirteçleri kullanarak ve SDK'ları gerektirir, istemci ve sunucu SDK aşağıdaki hello kullanın:

* İstemci: [Azure mobil istemci SDK'sı](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/)
* Sunucu: [Microsoft Azure mobil uygulaması .NET kimlik doğrulaması uzantısı](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/) 

Bunun yerine hello uygulama hizmeti alfa SDK kullanıyorsanız, bunlar artık kullanımdan kaldırıldı:

* İstemci: [Microsoft Azure uygulama hizmeti SDK'sı](http://www.nuget.org/packages/Microsoft.Azure.AppService)
* Sunucu: [Microsoft.Azure.AppService.ApiApps.Service](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service)

Hello AAD belirtecini doğrudan kullanıyorsanız, özellikle Azure Active Directory ile ancak hiçbir uygulama hizmete özgü gereklidir.

### <a name="internal-access"></a>İç erişim
Merhaba önceki API uygulamaları modeli yerleşik iç erişim düzeyi dahil. Bu, hello SDK kullanımını imzalama istekleri için gereklidir. Merhaba yeni API uygulamaları modeliyle daha önce açıklandığı gibi AAD hizmet asıl adı alternatif olarak hizmet kimlik doğrulaması için bir uygulama hizmete özgü SDK gerektirmeden kullanılabilir. Daha fazla bilgi edinin [hizmet asıl kimlik doğrulaması Azure uygulama hizmetinde API uygulamaları için](app-service-api-dotnet-service-principal-auth.md).

### <a name="discovery"></a>Bulma
önceki API modeli, çalışma zamanında diğer API uygulamaları bulmak için API sahip uygulamaları hello arkasındaki aynı kaynak grubunu hello hello aynı ağ geçidi. Mikro hizmet desenleri uygulayan mimarilerinde özellikle yararlıdır. Bu doğrudan desteklenmez, ancak çeşitli seçenekler mevcuttur:

1. Hello Azure Resource Manager API'nin bulma için kullanın.
2. Azure API Management, uygulama hizmeti barındırılan API'ler önüne yerleştirin. Azure API Management cephesi görev yapar ve kararlı bir dış karşılıklı url, iç topoloji değişse bile sağlayabilir.
3. Kendi bulma API uygulaması oluşturma ve başlangıçta hello bulma uygulamasıyla kaydetme diğer API uygulamaları vardır.
4. Dağıtım sırasında hello uygulama ayarlarını ve tüm hello API apps (istemciler) diğer API uygulamaları hello hello uç ile doldurun. Bu şablon dağıtımda ve API uygulamaları artık size bu yana uygun denetim hello URL'si.

## <a name="using-api-apps-with-logic-apps"></a>API Apps Logic Apps ile kullanma
Merhaba yeni API apps modeli çalışır ile iyi [mantıksal uygulamalar şema sürümü 2015-08-01](../logic-apps/logic-apps-schema-2015-08-01.md).

## <a name="next-steps"></a>Sonraki Adımlar
toolearn daha fazlasını okuyun hello hello makalelerinde [API Apps belge bölümü](https://azure.microsoft.com/documentation/services/app-service/api/). Bunlar API uygulamaları için güncelleştirilmiş tooreflect hello yeni model olmuştur. Ayrıca, ek ayrıntılar veya geçiş hakkında yönergeler için hello forumları üzerinde ulaşmak:

* [MSDN forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps)
* [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-api-apps)

