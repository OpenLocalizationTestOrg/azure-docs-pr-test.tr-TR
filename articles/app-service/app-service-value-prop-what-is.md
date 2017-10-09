---
title: "web, mobil ve API uygulamaları için uygulama hizmeti aaaAzure | Microsoft Docs"
description: "Azure App Service’in web uygulamalarını ve mobil uygulamaları geliştirmenize, dağıtmanıza ve yönetmenize nasıl yardımcı olduğunu öğrenin."
keywords: "app service, azure app service, app service maliyeti, ölçek, ölçeklenebilir, uygulama dağıtımı, azure uygulama dağıtımı, paas, hizmet olarak platform, websitesi, web sitesi, azure mobil"
services: app-service
documentationcenter: 
author: omarkmsft
manager: erikre
editor: cephalin
ms.assetid: 979cafa8-eeb6-4d3b-87cf-764a821c3e4f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: 22f414c7d79092d87406a8d3538b946881fb4580
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-app-service"></a>Azure App Service nedir?
*App Service*, Microsoft Azure’un bir [hizmet olarak platform](https://en.wikipedia.org/wiki/Platform_as_a_service) (PaaS) teklifidir. Herhangi bir platform veya cihaz için web ve mobil uygulamalar oluşturun. Uygulamalarınızı SaaS çözümleriyle tümleştirin, şirket içi uygulamalara bağlanın ve iş süreçlerinizi otomatikleştirin. Azure, uygulamalarınızı tam yönetilen sanal makineler (VM) üzerinde, seçtiğiniz paylaşılan VM kaynakları veya özel VM’ler ile çalıştırır.

Uygulama hizmeti hello web ve biz daha önce ayrı olarak Azure Web siteleri ve Azure Mobile Services teslim mobil özelliklerini içerir. Ayrıca iş süreçlerini otomatikleştirmek ve bulut API'leri barındırmak için yeni özellikler içerir. Tek bir tümleşik hizmet olarak App Service; web siteleri, mobil uygulama arka uçları, RESTful API’leri ve iş süreçleri gibi çeşitli bileşenleri tek bir çözümde oluşturmanıza olanak sağlar.

Merhaba aşağıdaki 4 dakikalık video sağlar tooearlier Azure uygulama hizmeti ilişkilendirilme şekli hakkında kısa bir açıklama teklifleri ve içinde yenilikler.

> [!VIDEO https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/app-service-history-lesson/player]
> 
> 

## <a name="why-use-app-service"></a>App Service nedir?
App Service’in temel özelliklerinden bazıları şunlardır:

* **Birden çok dil ve çerçeve** - App Service ASP.NET, Node.js, Java, PHP ve Python için birinci sınıf destek sunar. Ayrıca, App Service sanal makineleri üzerinde [Windows PowerShell ve diğer betikleri veya yürütülebilir dosyaları](../app-service-web/web-sites-create-web-jobs.md) çalıştırabilirsiniz.
* **DevOps iyileştirmesi** - Visual Studio Team Services, GitHub veya BitBucket ile [sürekli tümleştirme ve dağıtım](../app-service-web/app-service-continuous-deployment.md) ayarlayın. [Test ve hazırlık ortamları](../app-service-web/web-sites-staged-publishing.md) aracılığıyla güncelleştirmeleri yükseltin. [A/B testi](../app-service-web/app-service-web-test-in-production-get-start.md) gerçekleştirin. Kullanarak uygulamalarınızı App Service'de yönetin [Azure PowerShell](/powershell/azureps-cmdlets-docs) veya hello [platformlar arası komut satırı arabirimi (CLI)](../cli-install-nodejs.md).
* **Yüksek kullanılabilirlik ile küresel ölçeklendirme** - El ile veya otomatik olarak ölçek [artırabilir](../app-service-web/web-sites-scale.md) veya [genişletebilirsiniz](../monitoring-and-diagnostics/insights-how-to-scale.md). Uygulamalarınızı Microsoft'un küresel veri merkezi altyapılarının herhangi bir yerinde barındırın ve uygulama hizmeti hello [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) yüksek kullanılabilirlik taahhüt eder.
* **Bağlantıları tooSaaS platformları ve şirket içi veri** -50'den fazla seçin [Bağlayıcılar](../connectors/apis-list.md) (Salesforce ve Office 365 gibi), SaaS (örneğin, SAP, Siebel ve Oracle) Kurumsal sistemler için hizmetleri ve Internet Hizmetleri (örneğin, Facebook ve Twitter). [Karma Bağlantılar](../biztalk-services/integration-hybrid-connection-overview.md)’ı ve [Azure Sanal Ağlar](../app-service-web/web-sites-integrate-with-vnet.md)’ı kullanarak şirket içi verilere erişin.
* **Güvenlik ve uyumluluk** - App Service [ISO, SOC ve PCI uyumludur](https://www.microsoft.com/TrustCenter/).
* **Uygulama Şablonları** -hello şablonlarında kapsamlı bir listesini arasından [Azure Marketi](https://azure.microsoft.com/marketplace/) imkan sağlayan bir sihirbaz tooinstall popüler açık kaynak yazılım WordPress, Joomla ve Drupal gibi kullanın.
* **Visual Studio tümleştirmesi** -Visual Studio'daki ayrılmış Araçlar oluşturma, dağıtma ve hata ayıklama hello işlemlerini kolaylaştırır.

## <a name="app-types-in-app-service"></a>App Service’deki uygulama türleri
Uygulama hizmeti sunar birkaç *uygulama türleri*, her hedeflenen toohost belirli bir iş yükü olduğu:

* [**Web Apps**](../app-service-web/app-service-web-overview.md) - Web sitelerini ve web uygulamalarını barındırmaya yöneliktir.
* [**Mobile Apps**](../app-service-mobile/app-service-mobile-value-prop.md) Mobil uygulama arka uçlarını barındırmaya yöneliktir.
* [**API Apps**](../app-service-api/app-service-api-apps-why-best-platform.md) - RESTful API'lerini barındırmaya yöneliktir.
* [**Logic Apps**](../logic-apps/logic-apps-what-are-logic-apps.md) - İş süreçlerini otomatikleştirmeye ve sistemler ile verileri kod yazmadan bulut üzerinde tümleştirmeye yöneliktir.

Merhaba word *uygulama* burada kaynakları ayrılmış toorunning bir iş yükü barındırma toohello başvuruyor. "Örnek olarak web uygulaması" alma, büyük olasılıkla olduğunuz hello işlem kaynaklarını ve uygulama bu sunan işlevselliği tooa tarayıcı kod gibi bir web uygulaması toothinking alışmanızı. Ancak App Service'te bir *web uygulaması* hello olan, uygulama kodunuzun barındırılması için Azure sağlar işlem kaynakları. 

Uygulamanız farklı türlerde birden fazla App Service uygulamasından oluşabilir. Örneğin, uygulamanız bir web ön ucu ve bir RESTful API arka ucundan oluşuyorsa şunları yapabilirsiniz:

- Hem (ön uç ve API) dağıtmak tooa tek bir web uygulaması  
- Ön uç kodu tooa web uygulamanız ve arka uç kodu tooan API uygulamanızı dağıtın. 



## <a name="app-service-plans"></a>App Service planları
[Uygulama hizmeti planları](azure-web-sites-web-hosting-plans-in-depth-overview.md) uygulamalarınızı kullanılan fiziksel kaynakları toohost hello koleksiyonunu temsil eder.

App Service planları şunları tanımlar:

- **Bölge** (Batı ABD, Doğu ABD vb.)
- **Ölçek sayısı** (bir, iki, üç örnek, vb.)
- **Örnek boyutu** (Küçük, Orta, Büyük)
- **SKU** (Ücretsiz, Paylaşılan, Temel, Standart, Premium)

Atanan tüm uygulamalar için tooan **uygulama hizmeti planı** paylaşmak hello kaynakları tanımladığı toosave maliyet birden fazla uygulama barındırdığında izin verme.

**Uygulama hizmeti planı** gelen ölçeklendirebilirsiniz **serbest** ve **paylaşılan** SKU'ları çok**temel**, **standart**, ve **Premium** , vermiş SKU'ları erişim toomore kaynakları ve özellikleri hello boyunca yolu. Uygulama hizmeti planınız çok ayarlandıktan sonra**temel** ya da daha yüksek ayrıca hello denetleyebilirsiniz **boyutu** ve ölçeklendirme hello VM'ler sayısı.

Merhaba **SKU** ve **ölçek** Merhaba uygulama hizmeti planı hello maliyet ve değil hello sayısını içinde barındırılan uygulamalar belirler. 

Daha fazla ölçeklenebilirlik ve ağ yalıtımını gerekiyorsa uygulamalarınızı bir [App Service Ortamı](../app-service-web/app-service-app-service-environment-intro.md) içinde çalıştırabilirsiniz.

## <a name="pricing"></a>Fiyatlandırma
App Service’in maliyeti hakkında bilgi için bkz. [App Service Fiyatlandırması](https://azure.microsoft.com/pricing/details/app-service/).

## <a name="test-drive-app-service"></a>App Service'i Deneyin
Herhangi bir kredi kartına gerek olmadan, taahhüt vermeden veya sorun yaşamadan [örnek bir web uygulaması, mobil uygulama veya mantıksal uygulama oluşturun](https://azure.microsoft.com/try/app-service/) ve uygulamanızı 1 saat boyunca deneyin.

Ya da bir [ücretsiz Azure hesabı](https://azure.microsoft.com/pricing/free-trial/) açıp, kullanmaya başlama öğreticilerimizden birini deneyin:

* [Öğretici: Web uygulaması oluşturma](../app-service-web/app-service-web-get-started.md)
* [Öğretici: Mobil uygulama oluşturma](../app-service-mobile/app-service-mobile-android-get-started.md)
* [Öğretici: API uygulaması oluşturma](../app-service-api/app-service-api-dotnet-get-started.md)
* [Öğretici: Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md)

