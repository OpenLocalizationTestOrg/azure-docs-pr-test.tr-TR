---
title: "Azure App Service ortamlarına giriş"
description: "Azure App Service ortamlarına kısa genel bakış"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 3c7eaefa-1850-4643-8540-428e8982b7cb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 06/13/2017
ms.author: ccompy
ms.custom: mvc
ms.openlocfilehash: 803a1cde5387b549504b42346d1a2e6a5df04746
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/04/2017
---
# <a name="introduction-to-app-service-environments"></a>App Service ortamlarına giriş #
 
## <a name="overview"></a>Genel Bakış ##

Azure App Service Ortamı, App Service uygulamalarını yüksek ölçekte güvenli olarak çalıştırmak için tamamen ayrı ve özel bir ortam sağlayan, bir Azure App Service özelliğidir. Bu özellik, web uygulamalarınızı, [mobil uygulamalarınızı][mobileapps], API uygulamalarınızı ve [işlevlerinizi][Functions] barındırabilir.

App Service ortamları (ASE), şunları gerektiren uygulama iş yükleri için uygundur:

- Çok yüksek ölçek.
- Yalıtım ve güvenli ağ erişimi.
- Yüksek bellek kullanımı.

Müşteriler tek bir Azure bölgesinde veya birden fazla Azure bölgesi arasında birden çok ASE oluşturabilir. Bu esneklik ASE’leri yüksek RPS iş yüklerini desteklemek üzere durum bilgisi olmayan uygulama katmanlarını yatay yönde ölçeklendirmek için ideal hale getirir.

ASE’ler yalnızca tek bir müşterinin uygulamalarını çalıştırmak üzere yalıtılmıştır ve her zaman bir sanal ağa dağıtılır. Müşteriler gelen ve giden uygulama ağ trafiği üzerinde ayrıntılı denetime sahiptir. Uygulamalar VPN üzerinden şirket içi kurumsal kaynaklara yüksek hızda güvenli bağlantılar kurabilir.

* ASE’ler güvenli ağ erişimi ile yüksek ölçekli uygulama barındırmayı sağlar. Daha fazla bilgi için bkz. ASE’ler hakkında [AzureCon Ayrıntılı Bakış](https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/).
* Yatay yönde ölçeklendirme için birden çok ASE kullanılabilir. Daha fazla bilgi için bkz. [Coğrafi olarak dağıtılmış bir uygulama ayak izi ayarlama](app-service-app-service-environment-geo-distributed-scale.md).
* ASE’ler, AzureCon Ayrıntılı Bakışında gösterildiği gibi güvenlik mimarisini yapılandırmak için kullanılabilir. AzureCon Ayrıntılı Bakışında gösterilen güvenlik mimarisinin nasıl yapılandırıldığını görmek için App Service ortamları ile [katmanlı güvenlik mimarisi uygulama makalesine](app-service-app-service-environment-layered-security.md) bakın.
* ASE’ler üzerinde çalışan uygulamalara erişim, web uygulaması güvenlik duvarları (WAF) gibi yukarı akış cihazları tarafından sağlanabilir. Daha fazla bilgi için bkz. [WAF’yi App Service ortamları için yapılandırma](app-service-app-service-environment-web-application-firewall.md).

## <a name="dedicated-environment"></a>Ayrılmış ortam ##

Bir ASE yalnızca tek bir aboneliğe ayrılmıştır ve 100 örneği barındırabilir. Aralık tek bir App Service planında 100 örnek ile 100 tek örnekli App Service planı arasındaki bir değer ve bunların arasındaki her değer olabilir.

ASE, ön uçlar ve çalışanlardan oluşur. Ön uçlar HTTP/HTTPS sonlandırmadan ve bir ASE içindeki uygulama isteklerinin otomatik yük dengelemesinden sorumludur. ASE içindeki App Service planlarının ölçeği artırıldıkça ön uçlar otomatik olarak eklenir.

Çalışanlar, müşteri uygulamalarını barındıran rollerdir. Çalışanlar üç sabit boyutta mevcuttur:

* Bir vCPU/3,5 GB RAM
* İki vCPU/7 GB RAM
* Dört vCPU/14 GB RAM

Müşterilerin ön uçları ve çalışanları yönetmesi gerekmez. Müşteriler App Service planlarının ölçeğini genişlettikçe tüm altyapı otomatik olarak eklenir. Bir ASE’de App Service planları oluşturulduğunda veya ölçeklendirildiğinde, gerekli altyapı uygun şekilde eklenir veya kaldırılır.

ASE için altyapıya ilişkin ödeme yapan ve ASE’nin boyutuna göre değişmeyen sabit bir aylık fiyat mevcuttur. Ayrıca, App Service planı vCPU’su için bir maliyet mevcuttur. ASE'de barındırılan tüm uygulamalar, Yalıtılmış fiyatlandırma SKU’su içindedir. ASE fiyatlandırması hakkında bilgi için [App Service fiyatlandırma][Pricing] sayfasına bakın ve ASE’ler için kullanılabilir seçenekleri gözden geçirin.

## <a name="virtual-network-support"></a>Sanal ağ desteği ##

Bir ASE yalnızca bir Azure Resource Manager sanal ağında oluşturulabilir. Azure sanal ağları hakkında daha fazla bilgi için bkz. [Azure sanal ağları ile ilgili SSS](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/). Bir ASE her zaman bir sanal ağda ve daha kesin bir şekilde bir sanal ağın alt ağında bulunur. Uygulamalarınıza ilişkin gelen ve giden ağ iletişimini denetlemek için sanal ağların güvenlik özelliklerini kullanabilirsiniz.

ASE bir genel IP adresi ile İnternet’e yönelik veya sadece bir Azure iç yük dengeleyici (ILB) adresi ile iç ağa yönelik olabilir.

[Ağ Güvenlik Grupları][NSGs], bir ASE’nin bulunduğu alt ağa gelen ağ iletişimini kısıtlar. WAF’ler ve ağ SaaS sağlayıcıları gibi yukarı akış cihazlarının ve hizmetlerinin arkasında uygulamaları çalıştırmak için NSG’leri kullanabilirsiniz.

Uygulamalar, iç veritabanları ve web hizmetleri gibi şirket kaynaklarına da sıklıkla erişmelidir. ASE’yi şirket içi ağınızla VPN bağlantısı olan bir sanal ağa dağıtırsanız, ASE’deki uygulamalar şirket içi kaynaklara erişebilir. Bu özellik, VPN’nin [siteden siteye](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/) veya [Azure ExpressRoute](http://azure.microsoft.com/services/expressroute/) VPN olmasından bağımsız olarak geçerli olabilir.

ASE’lerin sanal ağlar ve şirket ağlarla nasıl çalıştığı hakkında daha fazla bilgi için bkz. [App Service Ortamı ağ konuları][ASENetwork].

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Application-Service-Environments-v2-Private-PaaS-Environments-in-the-Cloud/player]

## <a name="app-service-environment-v1"></a>App Service Ortamı v1 ##

App Service Ortamının iki sürümü vardır: ASEv1 ve ASEv2. Yukarıdaki bilgiler ASEv2’yi temel alır. Bu bölümde ASEv1 ile ASEv2 arasındaki farklar gösterilmektedir. 

ASEv1’de tüm kaynakları el ile yönetmeniz gerekir. Buna ön uçlar, çalışanlar ve IP tabanlı SSL için kullanılan IP adresleri dahildir. App Service planınızın ölçeğini artırabilmeniz için, öncelikle planınızı barındırmak istediğiniz çalışan havuzunun ölçeğini artırmanız gerekir.

ASEv1, ASEv2’den farklı bir fiyatlandırma modeli kullanır. ASEv1’de ayrılmış her vCPU için ücret ödersiniz. Buna herhangi bir iş yükünü barındırmayan ön uçlar veya çalışanlar için kullanılan vCPU’lar dahildir. ASEv1’de bir ASE’nin varsayılan en büyük ölçek boyutu toplam 55 konaktır. Buna çalışanlar ve ön uçlar dahildir. ASEv1’in bir avantajı, klasik bir sanal ağa ve bir Resource Manager sanal ağına dağıtılabilmesidir. ASEv1 hakkında daha fazla bilgi için bkz. [App Service Ortamı v1’e giriş][ASEv1Intro].

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: app-service-app-service-environment-intro.md
[webapps]: ../app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[ASEWAF]: app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
