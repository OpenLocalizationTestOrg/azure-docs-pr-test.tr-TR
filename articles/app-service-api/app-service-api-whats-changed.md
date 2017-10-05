---
title: "App Service API Apps - Değiştirilenler | Microsoft Docs"
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
ms.openlocfilehash: e4e25f2cd1d39bb0113e3fe2bc37120f92227b28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="app-service-api-apps---whats-changed"></a>App Service API Apps - Değiştirilenler
Bazı geliştirmeler Azure App Service'e Kasım 2015'te Connect() etkinlikte olan [Duyuruldu](https://azure.microsoft.com/blog/azure-app-service-updates-november-2015/). Bu geliştirmeler daha iyi mobil ve Web uygulamaları ile hizalamak, kavram sayısını azaltın ve dağıtım ve çalışma zamanı performansı artırmak için API uygulamaları için temel alınan değişiklikleri içerir. 30 Kasım 2015 yeni API uygulamaları başlatma Azure Yönetim Portalı'nı kullanarak oluşturduğunuz veya son araç bu değişiklikleri yansıtır. Bu makalede özelliklerinden yararlanmak için var olan uygulamaları dağıtmak nasıl yanı sıra, bu değişiklikler açıklanmaktadır.

## <a name="feature-changes"></a>Özellik değişiklikleri
Doğrudan uygulama hizmetinde API uygulamaları – kimlik doğrulaması, CORS ve API meta verilerini – anahtar özelliklerini taşınmış. Bu değişiklikle özellikler Web, mobil ve API uygulamaları kullanılabilir. Aslında, tüm üç aynı paylaşmak **Microsoft.Web/sites** Kaynak Yöneticisi'nde kaynak türü. API Apps ağ geçidi artık gerekli veya API uygulamaları ile sunulan. Bu ayrıca, yalnızca tek API Yönetimi ağ geçidi olacağından Azure API Management'i kullanmak kolaylaştırır.

![API Apps'e genel bakış](./media/app-service-api-whats-changed/api-apps-overview.png)

Temel tasarım ilkesine API uygulamaları güncelleştirme, seçim dilinizde olduğu gibi API getirmek sağlamaktır.  API'nizi zaten bir Web uygulaması veya mobil uygulama dağıtılırsa, yeni özelliklerden yararlanmak için uygulamanızı dağıtmanız gerekmez. API Apps Önizleme'şu anda varsa, Geçiş Kılavuzu aşağıda ayrıntılı olarak verilmiştir.

### <a name="authentication"></a>Kimlik Doğrulaması
Varolan anahtar teslimi API Apps, Mobile Services/uygulamaları ve Web uygulamaları kimlik doğrulama özellikleri birleşik ve Yönetim Portalı'nda tek bir Azure App Service kimlik doğrulama dikey penceresinde kullanılabilir. App Service içinde kimlik doğrulama Hizmetleri giriş için bkz: [genişletme App Service kimlik doğrulama / yetkilendirme](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/).

API senaryoları için birkaç ilgili yeni özellikleri vardır:

* **Azure Active Directory kullanarak doğrudan desteği**, istemci kodu Oturum belirteci için AAD belirtecini exchange zorunda kalmadan: istemci yalnızca AAD belirteçleri yetkilendirme üstbilgisinde taşıyıcı belirteci belirtimine göre içerebilir. Bu ayrıca istemci veya sunucu tarafında hiçbir uygulama hizmete özgü SDK gerekli anlamına gelir. 
* **Hizmetten hizmete veya "Dahili" erişim**: arka plan programı işlemi veya arabirim olmadan API'lerine erişim gerektiren başka bir istemci varsa, bir AAD hizmet sorumlusu kullanarak bir belirteç istemek ve kimlik doğrulaması için App Service'e geçirmek, uygulama.
* **Yetkilendirme ertelenmiş**: birçok uygulama uygulamanın farklı bölümleri için değişen erişim kısıtlamalar söz konusudur. Belki başkalarının oturum açma gerektirirken genel olarak kullanılabilir olması için bazı API'leri istiyor. Özgün kimlik doğrulama/yetkilendirme özelliğini ya hep ya hiç, oturum açma gerektiren tüm site. Bu seçenek hala var, ancak bunun yerine uygulama hizmeti kullanıcı kimliğini doğrulamasından sonra erişim kararları işlemek uygulama kodunuz izin verebilirsiniz.

Yeni kimlik doğrulama özellikleri hakkında daha fazla bilgi için bkz: [kimlik doğrulama ve yetkilendirme Azure uygulama hizmetinde API uygulamaları için](app-service-api-authentication.md). Varolan API uygulamaları için yeni bir önceki API apps modelden geçirme hakkında daha fazla bilgi için bkz: [geçiş varolan API uygulamaları](#migrating-existing-api-apps) bu makalenin ilerisinde yer.

### <a name="cors"></a>CORS
Virgülle ayrılmış yerine **MS_CrossDomainOrigins** uygulama ayarı yok şimdi bir dikey pencere CORS yapılandırmak için Azure Yönetim Portalı'nda. Alternatif olarak, Kaynak Yöneticisi'ni CLI Azure PowerShell gibi araçları kullanarak yapılandırılabilir veya [kaynak Gezgini](https://resources.azure.com/). Ayarlama **cors** özelliği **Microsoft.Web/sites/config** kaynak türü için  **&lt;site adı&gt;/web** kaynak. Örneğin:

    {
        "cors": {
            "allowedOrigins": [
                "https://localhost:44300"
            ]
        }
    } 

### <a name="api-metadata"></a>API meta verileri
API tanımı dikey Web, mobil ve API uygulamaları kullanıma sunulmuştur. Yönetim Portalı'nda, göreli bir url veya bir uç nokta API'nizi o ana Swagger 2.0 gösterimini işaret eden mutlak bir url belirtebilirsiniz. Alternatif olarak, kaynak yöneticisi araçları kullanılarak yapılandırılabilir. Ayarlama **apiDefinition** özelliği **Microsoft.Web/sites/config** kaynak türü için  **&lt;site adı&gt;/web** kaynak. Örneğin:

    {
        "apiDefinition":
        {
            "url": "https://myStorageAccount.blob.core.windows.net/swagger/apiDefinition.json"
        }
    }

Şu anda meta veri uç noktasının birçok aşağı akış istemcileri (örneğin Visual Studio REST API İstemci oluşturma ve PowerApps "API Ekle" akış) bunu kullanmak için kimlik doğrulaması olmadan genel olarak erişilebilir olması gerekir. Bu, App Service kimlik doğrulaması kullanıyorsanız ve API tanımı, uygulamanızın içinde kullanıma sunmak istiyorsanız, Swagger meta verileriniz için rota ortak böylece daha önce açıklanan ertelenmiş kimlik doğrulaması seçeneği kullanmanız gerekecektir anlamına gelmez.

## <a name="management-portal"></a>Yönetim Portalı
Seçme **yeni > Web + mobil > API uygulaması** Portalı'nda açıklanan yeni özellikleri yansıtacak API uygulamaları oluşturur. **Gözat > API uygulamaları** bu yeni API uygulamaları yalnızca Göster olur. API uygulamaya Gözat sonra dikey aynı düzeni ve Web ve mobil uygulamaları içeriğiyle olarak özellikleri paylaşır. Yalnızca farklar hızlı başlangıç içeriği ve ayarları sıralama ' dir.

Varolan API uygulamaları (veya mantığı uygulamalardan oluşturulan Market API uygulamaları) önceki Önizleme özellikleri hala kaynak grubundaki tüm kaynakların göz atarken görünür Logic Apps Tasarımcısı'nda ve olacaktır.

## <a name="visual-studio"></a>Visual Studio
Aynı temel paylaştıkları beri çoğu Web Apps araç yeni API uygulamalarıyla çalışacak **Microsoft.Web/sites** kaynak türü. Bu yana birtakım API'lerine belirli yetenekler sunan Azure Visual Studio'ı tooling, ancak 2.8.1 ile sürümüne yükseltilmiş veya üzeri olmalıdır. SDK'dan gelen indirme [Azure indirmeler sayfası](https://azure.microsoft.com/downloads/).

Uygulama hizmeti türleri yeterli duruma getirilmesi ile yayımlama altında da birleşik **Yayımla > Microsoft Azure App Service**:

![API uygulamaları yayımlama](./media/app-service-api-whats-changed/api-apps-publish.png)

SDK 2.8.1 ile hakkında daha fazla bilgi için duyuruyu okuma [blog gönderisi](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/).

Alternatif olarak, yayımlama etkinleştirmek için yönetim portalından el ile yayımlama profilini içeri aktarabilirsiniz. Ancak, SDK 2.8.1 ile bulut Gezgini, kod oluşturma ve API uygulaması seçimi/oluşturma gerektirir ya da daha yüksek.

## <a name="migrating-existing-api-apps"></a>Varolan API uygulamaları geçirme
API Apps önceki Önizleme sürümü için özel API'nizi dağıtılırsa, 31 Aralık 2015 tarafından API uygulamaları için yeni modele geçirme isteyin. App Service içinde barındırılan Web API'lerde hem eski ve yeni model tabanlı olduğundan, var olan kodu çoğunu yeniden kullanılabilir.

### <a name="hosting-and-redeployment"></a>Barındırma ve yeniden dağıtım
Dağıtarak adımlarını var olan tüm Web API App Service'e dağıtma aynıdır. adımlar:

1. Boş bir API uygulaması oluşturun. Bu yeni ile portalında yapılabilir > Yayımla veya Kaynak Yöneticisi Araçları Visual Studio API uygulaması. Kaynak Yöneticisi Araçları veya şablonları kullanıyorsanız, ayarlamak **türü** değeri **API** üzerinde **Microsoft.Web/sites** quickstarts ve ayarları için kaynak türü API senaryolarında yönelik Yönetim Portalı.
2. Bağlanma ve projenizin App Service tarafından desteklenen dağıtım düzenekleri birini kullanarak boş API uygulaması dağıtın. Okuma [Azure uygulama hizmeti dağıtım belgeleri](../app-service-web/web-sites-deploy.md) daha fazla bilgi için. 

### <a name="authentication"></a>Kimlik Doğrulaması
Uygulama hizmeti kimlik doğrulama hizmetleri önceki API uygulamaları modeliyle kullanılabilir aynı yetenekleri için destek. Oturum belirteçleri kullanıyorsanız ve SDK'ları gerektiren aşağıdaki istemci ve sunucu SDK'ları kullanın:

* İstemci: [Azure mobil istemci SDK'sı](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/)
* Sunucu: [Microsoft Azure mobil uygulaması .NET kimlik doğrulaması uzantısı](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/) 

Bunun yerine uygulama hizmeti alfa SDK kullanıyorsanız, bunlar artık kullanımdan kaldırıldı:

* İstemci: [Microsoft Azure uygulama hizmeti SDK'sı](http://www.nuget.org/packages/Microsoft.Azure.AppService)
* Sunucu: [Microsoft.Azure.AppService.ApiApps.Service](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service)

AAD belirtecini doğrudan kullanıyorsanız, özellikle Azure Active Directory ile ancak hiçbir uygulama hizmete özgü gereklidir.

### <a name="internal-access"></a>İç erişim
Önceki API uygulamaları modeli yerleşik iç erişim düzeyi dahil. Bu SDK'sının kullanım istekleri imzalamak için gereklidir. Yeni API uygulamaları modeliyle daha önce açıklandığı gibi AAD hizmet asıl adı alternatif olarak hizmet kimlik doğrulaması için bir uygulama hizmete özgü SDK gerektirmeden kullanılabilir. Daha fazla bilgi edinin [hizmet asıl kimlik doğrulaması Azure uygulama hizmetinde API uygulamaları için](app-service-api-dotnet-service-principal-auth.md).

### <a name="discovery"></a>Bulma
Önceki API uygulamaları model, aynı kaynak grubunda aynı ağ geçidi arkasında çalışma zamanında diğer API uygulamaları bulmak için API vardı. Mikro hizmet desenleri uygulayan mimarilerinde özellikle yararlıdır. Bu doğrudan desteklenmez, ancak çeşitli seçenekler mevcuttur:

1. Azure Resource Manager API'nin bulma için kullanın.
2. Azure API Management, uygulama hizmeti barındırılan API'ler önüne yerleştirin. Azure API Management cephesi görev yapar ve kararlı bir dış karşılıklı url, iç topoloji değişse bile sağlayabilir.
3. Kendi bulma API uygulaması oluşturma ve başlangıçta bulma uygulamasıyla kaydetme diğer API uygulamaları vardır.
4. Dağıtım sırasında uygulama ayarlarını ve tüm API uygulamaları (istemciler) bir API uygulamaları uç ile doldurun. Bu şablon dağıtımda ve API uygulamaları artık size bu yana uygun denetim URL'si.

## <a name="using-api-apps-with-logic-apps"></a>API Apps Logic Apps ile kullanma
Yeni API apps modeli ile iyi çalışır [mantıksal uygulamalar şema sürümü 2015-08-01](../logic-apps/logic-apps-schema-2015-08-01.md).

## <a name="next-steps"></a>Sonraki Adımlar
Daha fazla bilgi için makalelerinde okuma [API Apps belge bölümü](https://azure.microsoft.com/documentation/services/app-service/api/). Yeni model için API uygulamaları yansıtacak şekilde güncelleştirildi. Ayrıca, ek ayrıntılar veya geçiş hakkında yönergeler için forumlarda ulaşmak:

* [MSDN forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps)
* [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-api-apps)

