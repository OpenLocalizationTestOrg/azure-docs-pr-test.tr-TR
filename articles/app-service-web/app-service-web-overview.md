---
title: "aaaWeb uygulamalarına genel bakış | Microsoft Docs"
description: "Azure App Service’in web uygulamaları geliştirmenize ve barındırmanıza nasıl yardımcı olabileceğini öğrenin."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 94af2caf-a2ec-4415-a097-f60694b860b3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 01/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: ce27519bddd62a7fca6ba1fb23c763d0fc378c2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="web-apps-overview"></a>Web Apps’e Genel Bakış
*App Service Web Apps* web sitelerini ve web uygulamalarını barındırmak için en uygun hale getirilmiş tam olarak yönetilen bir işlem platformudur. Bu [hizmet olarak platform](https://en.wikipedia.org/wiki/Platform_as_a_service) (PaaS) teklifi Microsoft Azure, Azure alır hello altyapı toorun ilgilenirken işlerinize odaklanmanızı ve uygulamalarınızı ölçeklendirme sağlar.

5 dakikalık videoyu izleyerek hello Azure App Service Web Apps tanıtır.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Web-Apps-with-Yochay-Kiriaty/player]
>
>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

## <a name="what-is-a-web-app-in-app-service"></a>App Service’teki bir web uygulaması nedir?
App Service'te bir *web uygulaması* hello olan bir Web sitesi veya web uygulamasını barındırmak için Azure sağlar işlem kaynakları.  

Merhaba işlem kaynakları, paylaşılan veya ayrılmış sanal makinelerde (VM'ler) fiyatlandırma seçtiğiniz katmanı hello bağlı olabilir. Uygulama kodlarınız, diğer müşterilerden yalıtılmış yönetilen bir sanal makinede çalıştırılır.

Kodlarınız, ASP.NET, Node.js, Java, PHP veya Python [Azure App Service](../app-service/app-service-value-prop-what-is.md) tarafından desteklenen herhangi bir dilde veya çerçevede olabilir. Ayrıca, bir web uygulamasında [PowerShell ve diğer betik dosyası oluşturma dillerini](web-sites-create-web-jobs.md#acceptablefiles) kullanan betikler çalıştırabilirsiniz.

Web uygulamaları için bkz: kullanabileceğiniz tipik uygulama senaryo örnekleri için [Web uygulaması senaryoları](https://azure.microsoft.com/documentation/scenarios/web-app/) ve hello **senaryolar ve öneriler** bölümünü [Azure App Service, sanal Makineler, Service Fabric ve Cloud Services karşılaştırması](choose-web-site-cloud-service-vm.md#scenarios).

## <a name="why-use-web-apps"></a>Web Apps neden kullanılır?
TooWeb uygulamaları geçerli bazı önemli özelliklerinden App Service'in şunlardır:

* **Birden çok dil ve çerçeve** - App Service ASP.NET, Node.js, Java, PHP ve Python için birinci sınıf destek sunar. Ayrıca, App Service sanal makineleri üzerinde [PowerShell ve diğer betikleri veya yürütülebilirleri](web-sites-create-web-jobs.md) çalıştırabilirsiniz.
* **DevOps iyileştirmesi** - Visual Studio Team Services, GitHub veya BitBucket ile [sürekli tümleştirme ve dağıtım](app-service-continuous-deployment.md) ayarlayın. [Test ve hazırlık ortamları](web-sites-staged-publishing.md) aracılığıyla güncelleştirmeleri yükseltin. [A/B testi](app-service-web-test-in-production-get-start.md) gerçekleştirin. Kullanarak uygulamalarınızı App Service'de yönetin [Azure PowerShell](/powershell/azureps-cmdlets-docs) veya hello [platformlar arası komut satırı arabirimi (CLI)](../cli-install-nodejs.md).
* **Yüksek kullanılabilirlik ile küresel ölçeklendirme** - El ile veya otomatik olarak ölçek [artırabilir](web-sites-scale.md) veya [genişletebilirsiniz](../monitoring-and-diagnostics/insights-how-to-scale.md). Uygulamalarınızı Microsoft'un küresel veri merkezi altyapılarının herhangi bir yerinde barındırın ve uygulama hizmeti hello [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) yüksek kullanılabilirlik taahhüt eder.
* **Bağlantıları tooSaaS platformları ve şirket içi veri** -50'den fazla seçin [Bağlayıcılar](../connectors/apis-list.md) (Salesforce ve Office 365 gibi), SaaS (örneğin, SAP, Siebel ve Oracle) Kurumsal sistemler için hizmetleri ve Internet Hizmetleri (örneğin, Facebook ve Twitter). [Karma Bağlantılar](../biztalk-services/integration-hybrid-connection-overview.md)’ı ve [Azure Sanal Ağlar](web-sites-integrate-with-vnet.md)’ı kullanarak şirket içi verilere erişin.
* **Güvenlik ve uyumluluk** - App Service [ISO, SOC ve PCI uyumludur](https://www.microsoft.com/TrustCenter/).
* **Uygulama Şablonları** -hello uygulama şablonlarında kapsamlı bir listesini arasından [Azure Marketi](https://azure.microsoft.com/marketplace/) imkan sağlayan bir sihirbaz tooinstall popüler açık kaynak yazılım WordPress, Joomla ve Drupal gibi kullanın.
* **Visual Studio tümleştirmesi** -Visual Studio'daki ayrılmış Araçlar oluşturma, dağıtma ve hata ayıklama hello işlemlerini kolaylaştırır.

Ayrıca, web uygulamasında [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) (CORS desteği gibi) ve [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) (anında iletme bildirimleri) tarafından sunulan özelliklerden yararlanılabilir. App Service’teki uygulama türleri hakkında daha fazla bilgi için bkz. [Azure App Service’e genel bakış](../app-service/app-service-value-prop-what-is.md).

Azure, App Service’te Web Apps’in yanı sıra web siteleri ve web uygulamaları barındırmak için kullanılabilen başka hizmetler de sunar. Çoğu senaryoda, Web uygulamaları hello en iyi seçimdir.  Mikro hizmet mimarisi için göz önünde bulundurun [Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric)ve hello kodunuzun çalıştığı VM'ler hakkında daha fazla denetime ihtiyacınız varsa, göz önünde bulundurun [Azure sanal makineleri](https://azure.microsoft.com/documentation/services/virtual-machines/). Hakkında daha fazla bilgi için bu Azure hizmetleri arasında toochoose bkz [Azure App Service, sanal makineleri, Service Fabric ve Cloud Services karşılaştırması](choose-web-site-cloud-service-vm.md).

## <a name="getting-started"></a>Başlarken
Örnek kod tooa yeni web uygulaması App Service'te dağıtarak başlatılan tooget açılan kutusundan aşağıdaki hello hello eğitimlerine birini izleyin. Ücretsiz Azure hesabınızın olması gerekir.

> [!div class="op_single_selector"]
> * [5 dakika içinde ilk ASP.NET web uygulaması tooAzure dağıtma](app-service-web-get-started-dotnet.md)
> * [5 dakika içinde ilk PHP web uygulaması tooAzure dağıtma](app-service-web-get-started-php.md)
> * [5 dakika içinde ilk Node.js web uygulaması tooAzure dağıtma](app-service-web-get-started-nodejs.md)
> * [5 dakika içinde ilk Java web uygulaması tooAzure dağıtma](app-service-web-get-started-java.md)
> * [5 dakika içinde ilk Python web uygulaması tooAzure dağıtma](app-service-web-get-started-python.md)
> * [5 dakika içinde ilk HTML site tooAzure dağıtma](app-service-web-get-started-html.md)
> 
> 

> [!NOTE]
> Azure hesabınız olmadan [App Service'i Deneyebilirsiniz](https://azure.microsoft.com/try/app-service/). Bir başlangıç uygulaması oluşturun ve tooan saat--beraberinde, gerekli herhangi bir kredi kartı veya bir taahhüt yürütebilirsiniz.
> 
> 
