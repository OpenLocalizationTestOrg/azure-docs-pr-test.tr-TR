---
title: "aaaConfiguring uygulama hizmeti ortamı bir Web uygulaması Güvenlik Duvarı (WAF)"
description: "Tooconfigure bir web uygulaması uygulama hizmeti ortamınızı önünde nasıl Güvenlik Duvarı hakkında bilgi edinin."
services: app-service\web
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: a2101291-83ba-4169-98a2-2c0ed9a65e8d
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: naziml
ms.openlocfilehash: 0fcf62aea871751c9d4f294d2d24df2186fc0e7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a>Bir Web uygulaması Güvenlik Duvarı (WAF) için uygulama hizmeti ortamını yapılandırma
## <a name="overview"></a>Genel Bakış
Web uygulaması güvenlik duvarı hello gibi [Barracuda WAF Azure](https://www.barracuda.com/programs/azure) hello üzerinde kullanılabilir [Azure Marketi](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) yardımcı olur, gelen web trafiği tooblock SQL inceleyerek, web uygulamalarınızı güvenli eklemelerini, siteler arası komut dosyası, kötü amaçlı yazılım yüklemeleri ve uygulama DDoS ve diğer saldırılara. Ayrıca hello yanıtları hello arka uç web sunucularından veri kaybını önleme (DLP) inceler. Merhaba yalıtım ve App Service ortamları tarafından sağlanan ek ölçeklendirme birlikte, bu toowithstand kötü amaçlı istekleri ve yüksek hacimli trafik gerek toohost iş kritik web uygulamaları ideal bir ortam sağlar.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a>Kurulum
Biz yapılandırmak için bu belgenin böylece yalnızca hello WAF gelen trafiği hello uygulama hizmeti ortamı erişebilir ve DMZ hello erişilebilir olmaz Barracuda WAF örneklerini bizim uygulama hizmeti ortamı arkasında birden fazla yük dengeli. Azure veri merkezlerinde ve bölgeler arasında biz de bizim Barracuda WAF örnekleri tooload Bakiye önünde Azure Traffic Manager gerekir. Merhaba Kurulum üst düzey bir diyagramını ne aşağıda gösterilen gibi görünür.

![Mimari][Architecture] 

> Not: ile Merhaba giriş [ILB desteklemek için uygulama hizmeti ortamı](app-service-environment-with-internal-load-balancer.md), hello ana toobe DMZ hello erişilemez yapılandırabilir ve yalnızca kullanılabilir toohello özel ağ olabilir. 
> 
> 

## <a name="configuring-your-app-service-environment"></a>Uygulama hizmeti ortamınızı yapılandırma
bir uygulama hizmeti ortamı tooconfigure başvurmak çok[Belgelerimizi](app-service-web-how-to-create-an-app-service-environment.md) hello konu üzerinde. Oluşturulan bir uygulama hizmeti ortamı olduktan sonra oluşturabileceğiniz [Web Apps](app-service-web-overview.md), [API uygulamaları](../app-service-api/app-service-api-apps-why-best-platform.md) ve [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) Bu ortamdaki tüm hello WAF korunur biz Merhaba sonraki bölümde yapılandırın.

## <a name="configuring-your-barracuda-waf-cloud-service"></a>Barracuda WAF bulut hizmetini yapılandırma
Barracuda sahip bir [ayrıntılı makale](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) kendi WAF azure'da bir sanal makinede dağıtma. Ancak biz artıklık istediğiniz ve tek hata noktası tanıtmak değil çünkü toodeploy en az 2 WAF örneğine VM'ler hello istediğiniz aynı bulut bu yönergeleri izleyerek hizmet.

### <a name="adding-endpoints-toocloud-service"></a>Uç noktaları tooCloud hizmet ekleme
2 veya daha fazla WAF VM bulut hizmetiniz örnekleri sonra hello kullanarak [Azure portal](https://portal.azure.com/) hello resimde gösterildiği gibi uygulamanız tarafından kullanılan tooadd HTTP ve HTTPS uç noktaları.

![Uç noktasını yapılandırma][ConfigureEndpoint]

Uygulamalarınız diğer uç noktaları kullanıyorsa, bu toothis listesi de emin tooadd olun. 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a>Barracuda WAF kendi Yönetim Portalı üzerinden yapılandırma
Barracuda WAF TCP bağlantı noktası 8000 kendi Yönetim Portalı aracılığıyla yapılandırması için kullanır. Merhaba WAF VM'ler birden çok örneğini sahibiz bu yana her bir VM örneği için burada toorepeat hello adımları gerekir. 

> Not: WAF yapılandırmayla tamamladıktan sonra hello TCP/8000 uç noktası, tüm WAF VM'ler tookeep güvenli, WAF kaldırın.
> 
> 

Barracuda WAF hello görüntü tooconfigure aşağıda gösterildiği gibi hello yönetim uç noktası ekleyin.

![Yönetim uç nokta ekleyin][AddManagementEndpoint]

Bir tarayıcı toobrowse toohello yönetim uç bulut hizmetinizde kullanın. Bulut hizmetinizi test.cloudapp.net çağrılırsa, bu uç noktaya toohttp://test.cloudapp.net:8000 göz atarak erişir. Bir oturum açma sayfası görmelisiniz aşağıdaki gibi hello WAF VM kurulumu aşamasında belirtilen kimlik bilgilerini kullanarak oturum açabilir.

![Yönetim oturum açma sayfası][ManagementLoginPage]

Bir kez hello bir Pano görürsünüz, oturum açma hello görüntü aşağıdan birinde hello WAF koruma hakkında temel istatistikleri sunacaktır.

![Yönetim Panosu][ManagementDashboard]

Merhaba Hizmetleri sekmesini tıklatarak, sizin WAF koruduğu hizmetler için yapılandırma olanak tanır. Barracuda WAF yapılandırma hakkında daha fazla ayrıntı için başvurabilirsiniz [kendi belgelerine](https://techlib.barracuda.com/waf/getstarted1). Bir Azure Web uygulaması aşağıda hello örnekte HTTP ve HTTPS trafiğini hizmet veren yapılandırıldı.

![Yönetim Hizmetleri Ekle][ManagementAddServices]

> Not: uygulamalarınızı nasıl yapılandırılır ve hangi özelliklerin uygulama hizmeti ortamı'nda kullanıldığını bağlı olarak, tooforward trafiği 80 ve 443 dışındaki TCP bağlantı noktaları için örneğin gerekir bir Web uygulaması için IP SSL Kurulum varsa. Uygulama hizmeti ortamlarında kullanılan ağ bağlantı noktalarının listesi için lütfen çok bakın[denetim gelen trafiği belgelerine'nın](app-service-app-service-environment-control-inbound-traffic.md) ağ bağlantı noktaları bölümü.
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a>Microsoft Azure trafik Yöneticisi (isteğe bağlı) yapılandırma
Uygulamanız birden çok bölgede kullanılabilir sonra tooload Bakiye istersiniz arkasında bunları [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md). bir uç nokta hello ekleyebilmek toodo [Klasik Azure portalı](https://manage.azure.com) hello resimde gösterildiği gibi hello trafik Yöneticisi profili, WAF hello bulut hizmeti adını kullanarak. 

![Trafik Yöneticisi uç noktası][TrafficManagerEndpoint]

Uygulamanızın kimlik doğrulaması gerektiriyorsa, trafik Yöneticisi tooping uygulamanızın hello kullanılabilirlik için herhangi bir kimlik doğrulaması gerektirmeyen bazı kaynak olduğundan emin olun. Merhaba üzerinde hello URL hello yapılandırma bölümüne altında yapılandırabilirsiniz [Klasik Azure portalı](https://manage.azure.com) aşağıda gösterildiği gibi.

![Traffic Manager'ı yapılandırma][ConfigureTrafficManager]

tooforward hello trafik Yöneticisi ping WAF tooyour uygulamanızdan toosetup Web sitesi çevirileri hello aşağıdaki örnekte gösterildiği gibi Barracuda WAF tooforward trafiği tooyour uygulamanız gerekir.

![Web sitesi çevirileri][WebsiteTranslations]

## <a name="securing-traffic-tooapp-service-environment-using-network-security-groups-nsg"></a>Trafik tooApp hizmet ortamı kullanarak ağ güvenlik grupları (NSG) güvenliğini sağlama
Merhaba izleyin [denetim gelen trafiği belgelerine](app-service-app-service-environment-control-inbound-traffic.md) yalnızca bulut hizmetinizin hello VIP adresi kullanarak kısıtlama Ayrıntılar tooyour uygulama hizmeti ortamı hello WAF gelen trafik için. Burada, TCP bağlantı noktası 80 bu görevi gerçekleştirmek için bir örnek Powershell komut verilmiştir.

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

Merhaba SourceAddressPrefix hello WAF's bulut hizmetinin sanal IP adresi (VIP) ile değiştirin.

> Not: silin ve hello bulut hizmeti yeniden oluştururken hello VIP bulut hizmetinizin değiştirin. Yapma emin tooupdate başlangıç IP adresi Bunu yaptıktan sonra hello ağ kaynak grubunda. 
> 
> 

<!-- IMAGES -->
[Architecture]: ./media/app-service-app-service-environment-web-application-firewall/Architecture.png
[ConfigureEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureEndpoint.png
[AddManagementEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/AddManagementEndpoint.png
[ManagementAddServices]: ./media/app-service-app-service-environment-web-application-firewall/ManagementAddServices.png
[ManagementDashboard]: ./media/app-service-app-service-environment-web-application-firewall/ManagementDashboard.png
[ManagementLoginPage]: ./media/app-service-app-service-environment-web-application-firewall/ManagementLoginPage.png
[TrafficManagerEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/TrafficManagerEndpoint.png
[ConfigureTrafficManager]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureTrafficManager.png
[WebsiteTranslations]: ./media/app-service-app-service-environment-web-application-firewall/WebsiteTranslations.png
