---
title: "aaaIntroduction tooAzure uygulama hizmeti ortamları"
description: "Azure uygulama hizmeti ortamları kısa genel bakış"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 3c7eaefa-1850-4643-8540-428e8982b7cb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 9261041333cf59374974a039edf89c4983c45cdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environments"></a>Giriş tooApp Service ortamları #
 
## <a name="overview"></a>Genel Bakış ##

Azure uygulama hizmeti ortamı App Service uygulamalarını yüksek ölçekte güvenli bir şekilde çalıştırmak için tam yalıtılmış ve ayrılmış bir ortam sağlayan bir Azure uygulama hizmeti özelliğidir. Bu özellik barındırabilir, [web uygulamaları][webapps], [mobil uygulamaları][mobileapps], [API uygulamaları][APIapps], ve [işlevleri][Functions].

Uygulama hizmeti ortamları (ASEs) gerektiren uygulama iş yükleri için uygundur:

- Çok büyük ölçekli.
- Yalıtım ve güvenli ağ erişimi.
- Yüksek bellek kullanımı.

Müşteriler, birden çok ASEs tek bir Azure bölgesi içinde veya birden çok Azure bölgeleri oluşturabilirsiniz. Bu esneklik ASEs yatay olarak ölçekleme durum bilgisiz uygulama katmanları yüksek RPS iş yüklerini desteklemek için ideal hale getirir.

ASEs yalıtılmış toorunning yalnızca tek bir müşterinin uygulamalardır, her zaman bir sanal ağ içinde dağıtılır. Müşteriniz uygulama gelen ve giden ağ trafiği üzerinde hassas bir denetim yok. Uygulamaları yüksek hızlı güvenli VPN tooon içi şirket kaynaklarına bağlantı kurabilir.

Tüm makaleler ve nasıl tooinstructions ASEs hakkında hello kullanılabilir [uygulama hizmeti ortamları için Benioku][ASEReadme]:

* Güvenli ağ erişimi ile yüksek ölçekli uygulama barındırma ASEs etkinleştirin. Daha fazla bilgi için bkz: Merhaba [AzureCon derinlemesine](https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/) ASEs üzerinde.
* Birden çok ASEs kullanılan tooscale yatay olabilir. Daha fazla bilgi için bkz: [nasıl tooset coğrafi olarak dağıtılan uygulama ayak izini yukarı](https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/).
* ASEs kullanılan tooconfigure güvenlik mimarisi hello AzureCon derinlemesine gösterildiği gibi olabilir. toosee nasıl hello AzureCon derinlemesine gösterilen hello güvenlik mimarisi yapılandırılmışsa, bkz: Merhaba [nasıl makale tooimplement katmanlı güvenlik mimarisi](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-layered-security) uygulama hizmeti ortamları ile.
* ASEs üzerinde çalışan uygulamalar, web uygulaması Güvenlik Duvarı (WAFs) gibi Yukarı Akış cihazlar tarafından geçişli erişimleri olabilir. Daha fazla bilgi için bkz: [WAF uygulama hizmeti ortamları için yapılandırma](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-web-application-firewall).

## <a name="dedicated-environment"></a>Ayrılmış ortamda ##

Bir ana olan özel olarak tooa tek bir abonelik ayrılmış ve 100 örnekleri barındırabilir. Merhaba aralığı 100 örnekleri tek bir uygulama hizmeti planı too100 Tek Örnekli uygulama hizmeti planları ve arasındaki her şeyi yayılabilir.

Bir ana ön uçlar ve çalışanları oluşur. HTTP/HTTPS sonlandırma ve bir ana içinde uygulama isteklerinin otomatik Yük Dengeleme için ön uçlar sorumludur. Ön Uçları hello ana uygulama hizmeti planlarında çıkışı ölçeklenir hello olarak otomatik olarak eklenir.

Çalışanları müşteri uygulamaları barındıran rolleridir. Çalışanlar, üç sabit boyutlarında kullanılabilir:

* Bir çekirdek/3.5 GB RAM
* İki çekirdek/7 GB RAM
* Dört çekirdek/14 GB RAM

Müşteriler toomanage ön uçlar ve çalışanları gerekmez. Tüm altyapı, kendi uygulama hizmeti planları müşterilerin ölçeklenebilir olarak otomatik olarak eklenir. Uygulama planları oluşturulur veya ASE'de ölçeklendirilmiş hizmet olarak altyapı eklenip uygun şekilde kaldırılabilir hello gereklidir.

Merhaba altyapısı için ödenen ve hello ana hello boyutuyla değişmez bir ana için düz aylık bir oranı yoktur. Ayrıca, uygulama hizmeti planı çekirdek başına bir maliyeti yoktur. ASE'de barındırılan tüm hello uygulamalardır SKU fiyatlandırma yalıtılır. Hello için bir ana fiyatlandırma hakkında daha fazla bilgi için bkz [uygulama hizmeti fiyatlandırma] [ Pricing] sayfasında ve hello ASEs için kullanılabilir seçenekleri gözden geçirin.

## <a name="virtual-network-support"></a>Sanal ağ desteği ##

Bir ana yalnızca bir Azure Resource Manager sanal ağında oluşturulabilir. Azure sanal ağlar hakkında daha fazla toolearn bkz hello [Azure sanal ağları SSS](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/). Bir ana sanal ağ ve daha hassas bir şekilde her zaman bir sanal ağ alt ağı içerisinde bulunmaktadır. Gelen ve giden sanal ağlar toocontrol hello güvenlik özelliklerini kullanabilirsiniz ağ iletişimlerinin uygulamalarınız için.

Bir ana İnternete dönük bir genel IP adresiyle veya dahili kullanıma yönelik yalnızca Azure iç yük dengeleyiciye (ILB) adresi olabilir.

[Ağ güvenlik grupları] [ NSGs] gelen ağ iletişimi toohello bir ana bulunduğu alt ağ kısıtlayın. Nsg'ler toorun uygulamaları Yukarı Akış aygıtlar ve WAFs ve ağ SaaS sağlayıcıları gibi hizmetler arkasında kullanabilirsiniz.

Uygulamalar da sıklıkla iç veritabanları ve web Hizmetleri gibi şirket kaynaklarına tooaccess gerekir. Bir VPN bağlantısı toohello şirket içi ağı olan bir sanal ağda hello ana dağıtırsanız, hello ana hello uygulamalarında hello şirket içi kaynaklara erişebilir. Bu özellik hello VPN olup olmadığına bakılmaksızın doğru bir [siteden siteye](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/) veya [Azure ExpressRoute](http://azure.microsoft.com/services/expressroute/) VPN.

ASEs sanal ağlar ve şirket içi ağlar ile nasıl çalıştığı hakkında daha fazla bilgi için bkz: [uygulama hizmeti ortamı ağ konuları][ASENetwork].

## <a name="app-service-environment-v1"></a>App Service Ortamı v1 ##

Uygulama hizmeti ortamı iki sürümü vardır: ASEv1 ve ASEv2. Önceki bilgilere hello üzerinde ASEv2 dayanır. Bu bölümde ASEv1 ve ASEv2 arasındaki farklar hello gösterir. 

ASEv1 içinde toomanage gerek duyduğunuz tüm hello kaynakları el ile. Merhaba ön uçları, çalışanlar ve IP tabanlı SSL için kullanılan IP adresleri dahildir. Uygulama hizmeti planınızı ölçeklendirebilirsiniz önce toofirst ihtiyacınız toohost istediğiniz hello çalışan havuzunda, ölçeklendirin.

ASEv1 ASEv2 öğesinden farklı bir fiyatlandırma modelini kullanır. ASEv1 içinde ayrılmış her çekirdek için ücret ödersiniz. Ön Uçları veya tüm iş yükleri barındıran olmayan çalışanlar için kullanılan çekirdek dahildir. ASEv1 içinde hello varsayılan en büyük ölçekli bir ana boyutunu 55 toplam konakları ' dir. Bu, çalışanlar ve ön uçlar içerir. Bu bir Klasik sanal ağı ve Resource Manager sanal ağ içinde dağıtılabilir bir avantajı tooASEv1 olur. toolearn ASEv1, hakkında daha fazla bilgi görmek [uygulama hizmeti ortamı v1 giriş][ASEv1Intro].

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
