---
title: "aaaNetwork App Service ortamları, mimarisi genel bakış"
description: "Ağ topolojisi ofApp hizmeti ortamları mimarisine genel bakış."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 13d03a37-1fe2-4e3e-9d57-46dfb330ba52
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 3cbc86883f5687a9ada35a3ab2f577a450a3fa0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="network-architecture-overview-of-app-service-environments"></a>App Service Ortamlarının Ağ Mimarisine Genel Bakış
## <a name="introduction"></a>Giriş
Uygulama hizmeti ortamları her zaman bir alt ağ içinde oluşturulmuş bir [sanal ağ] [ virtualnetwork] -uygulama hizmeti ortamı'nda çalışan uygulamalar ile özel iletişim uç noktalar aynı sanal hello içinde bulunan Ağ topolojisi.  Müşteriler kendi sanal ağ altyapısı bölümlerini kilitlemek olduğundan, bir uygulama hizmeti ortamı ile ortaya ağ iletişimi akışlarının önemli toounderstand hello türleri kalır.

## <a name="general-network-flow"></a>Genel ağ akışı
Uygulama hizmeti ortamı (ana) uygulamaları için ortak bir sanal IP adresi (VIP) kullandığında, tüm gelen trafiği, genel VIP ulaşır.  Bu uygulamalar için HTTP ve HTTPS trafiğini yanı sıra, diğer trafik FTP, uzaktan hata ayıklama işlevselliği ve Azure yönetim işlemleri için içerir.  Merhaba tam listesi için hello ortak VIP kullanılabilen belirli bağlantı noktaları (gerekli ve isteğe bağlı) üzerinde hello makalesine bakın [gelen trafik denetleme] [ controllinginboundtraffic] tooan uygulama hizmeti ortamı. 

Uygulama hizmeti ortamları da çalışan destek tooa sanal ağ yalnızca iç adresi, bağlı olan uygulamalar da tooas bir ILB (iç yük dengeleyici) adresi denir.  Uygulamalar ve bunun yanı sıra uzaktan hata ayıklama çağrıları için etkin ana, HTTP ve HTTPS trafiği üzerinde bir ILB ILB adresi hello üzerinde ulaşır.  ILB ana yapılandırmaların çoğu için FTP/FTPS trafiğinin ILB adresi hello üzerinde de ulaşırsınız.  Ancak Azure yönetim işlemlerini hala tooports 454/455 bir ILB, genel VIP hello üzerinde akar ana etkin.

Merhaba diyagrama hello genel bir bakış uygulama hizmeti ortamı hello uygulamaları ilişkili tooa genel sanal IP adresi olduğu için çeşitli gelen ve giden ağ akışları gösterir:

![Genel ağ akışlar][GeneralNetworkFlows]

Bir uygulama hizmeti ortamı çeşitli özel müşteri uç noktalar ile iletişim kurabilir.  Örneğin, uygulama hizmeti ortamı Iaas sanal makinelerde çalışan toodatabase sunucuları bağlanabilir hello çalışan uygulamalar aynı sanal ağ topolojisi hello.

> [!IMPORTANT]
> Merhaba Ağ Diyagramı baktığınızda, hello diğer işlem kaynaklarını"" Merhaba uygulama hizmeti ortamı'ndan farklı bir alt ağ dağıtılır. Merhaba kaynaklarında dağıtma hello ana ile aynı alt ağda ana toothose kaynakları (dışında belirli içi ana yönlendirme) bağlantısını engeller. Tooa dağıtmak farklı alt yerine (içinde aynı sanal ağı hello). Uygulama hizmeti ortamı Hello ardından mümkün tooconnect olacaktır. Hiçbir ek yapılandırma gerekli değildir.
> 
> 

Uygulama hizmeti ortamları yönetme ve bir uygulama hizmeti ortamı işletim için gerekli kaynaklar da Sql DB ve Azure Storage ile iletişim kurar.  Bir uygulama hizmeti ortamı kurduğu hello Sql ve depolama kaynaklarını bazıları hello bulunan hello başkalarının uzaktan Azure bölgelerinde bulunan uygulama hizmeti ortamı, aynı bölgeye.  Sonuç olarak, giden bağlantı toohello Internet her zaman doğru bir uygulama hizmeti ortamı toofunction için gereklidir. 

Bir uygulama hizmeti ortamı bir alt ağda dağıtılan olduğundan, ağ güvenlik grupları kullanılan toocontrol olabilir gelen trafik toohello alt.  Merhaba aşağıdaki nasıl toocontrol gelen trafiği tooan uygulama hizmeti ortamı hakkında daha fazla bilgi için bkz [makale][controllinginboundtraffic].

Ayrıntılar için bir uygulama hizmeti ortamı tooallow giden Internet bağlantısı ile çalışma hakkında makale aşağıdaki hello bkz [hızlı rota][ExpressRoute].  Siteden siteye bağlantı çalışma ve kullanarak Hello makalesinde açıklanan aynı yaklaşımı uygulanır hello zorlanan tünel.

## <a name="outbound-network-addresses"></a>Giden ağ adresleri
Bir IP adresi, her zaman bir uygulama hizmeti ortamı giden çağrı yaptığında hello giden çağrıları ile ilişkilidir.  kullanılan hello belirli IP adresi çağrılan hello endpoint hello sanal ağ topolojisi içinde veya dışında hello sanal ağ topolojisi bulunduğu olmasına bağlıdır.

Çağrılan hello uç nokta ise **dışında** hello sanal ağ topolojisi sonra hello kullanılan giden (diğer adıyla hello giden NAT adresi) hello uygulama hizmeti ortamı, genel VIP hello adresidir.  Bu adres hello portal kullanıcı arabirimi özellikleri dikey penceresinde hello uygulama hizmeti ortamı için bulunabilir.

![Giden IP adresi][OutboundIPAddress]

Bu adres, genel VIP hello uygulama hizmeti ortamı bir uygulama oluşturma ve ardından gerçekleştirme yeterlidir ASEs için de belirlenebilir bir *nslookup* hello uygulamanın adresinde. Merhaba sonuç IP adresi hem hello genel VIP yanı sıra hello uygulama hizmeti ortamı'nın giden NAT adresi değil.

Çağrılan hello uç nokta ise **içinde** hello sanal ağ topolojisi, hello iç IP adresi hello uygulamayı çalıştıran hello tek tek işlem kaynağının hello giden adresi hello arama uygulaması olacaktır.  Ancak yok sanal ağ iç IP adreslerini tooapps kalıcı eşlemesi.  Uygulamaları farklı işlem kaynakları arasında hareket etmek ve bir uygulama hizmeti ortamı kullanılabilir işlem kaynakları hello havuzu tooscaling işlemleri değiştirebilirsiniz.

Ancak, bir uygulama hizmeti ortamı her zaman bir alt ağ içinde bulunduğundan, bir uygulama çalıştıran bir işlem kaynağı hello iç IP adresi her zaman hello CIDR aralığı hello alt ağ içinde kalan sağlanır.  Sonuç olarak, hassas ACL'leri ya da ağ güvenlik grupları kullanıldığında toosecure tooother uç noktalarda hello sanal ağ erişim, erişim izni hello uygulama hizmeti ortamı gereksinimlerini toobe içeren alt ağ aralığı hello.

Merhaba Aşağıdaki diyagramda bu kavramları daha ayrıntılı olarak gösterilmiştir:

![Giden ağ adresleri][OutboundNetworkAddresses]

Yukarıdaki diyagramda Hello:

* Merhaba uygulama hizmeti ortamı, genel VIP Hello 192.23.1.2 olduğundan olan çağrıları çok yapılırken kullanılan hello giden IP adresi "Internet" uç noktaları.
* Merhaba hello uygulama hizmeti ortamı için alt ağ içeren hello CIDR aralığı 10.0.1.0/26 ' dir.  Diğer uç noktaları hello içinde aynı sanal ağ altyapısı çağrıları uygulamalardan herhangi bir yerde bu adres aralığı içinde kaynaklanan olarak görürsünüz.

## <a name="calls-between-app-service-environments"></a>Uygulama hizmeti ortamları arasında çağrıları
Birden fazla App Service ortamları dağıtırsanız, daha karmaşık bir senaryo ortaya çıkabilir hello aynı sanal ağ ve bir uygulama hizmeti ortamı tooanother uygulama hizmeti ortamı'ndan giden çağrıları yapma.  Bu tür uygulama hizmeti ortamı'nın çağrıları ayrıca "Internet" çağrısı olarak kabul edilecek arası.

(örneğin, üzerinde bir uygulama hizmeti ortamı diyagramı aşağıdaki hello uygulamalarıyla katmanlı mimari örneği gösterilmektedir Web uygulamaları "Ön kapı") uygulamaları (örn. iç uç API uygulamaları belirtmezseniz toobe Internet hello erişilebilir) ikinci bir uygulama hizmeti ortamı çağrılması. 

![Uygulama hizmeti ortamları arasında çağrıları][CallsBetweenAppServiceEnvironments] 

Hello uygulama hizmeti ortamı "Ana bir" Merhaba Yukarıdaki örnek 192.23.1.2 giden IP adresi vardır.  Bu uygulama hizmeti ortamı üzerinde çalışan bir uygulama bir ikinci uygulama hizmeti aynı sanal ağ, hello hello bulunan ortamı ("ana iki") giden çalışan bir giden çağrı tooan uygulama yaparsa çağrı kabul "Internet" çağrısı olarak.  Merhaba ağ trafiği üzerinde hello ulaşan ikinci uygulama hizmeti ortamı sonucunda gösterecektir 192.23.1.2 kaynaklanan olarak (örn. ilk uygulama hizmeti ortamı hello değil hello alt ağ adres aralığı).

Rağmen hem App Service ortamları aynı Azure bölgesinde hello ağ trafiğini hello bölgesel Azure ağ üzerinde kalır ve değil fiziksel olarak akar hello bulunduğunda çağrıları farklı uygulama hizmeti ortamları arasında "Internet" çağrısı olarak kabul edilir üzerinden genel Internet hello.  Sonuç olarak bir ağ güvenlik grubu kullanabilirsiniz hello hello alt ağda tooonly izin gelen gelen çağrıları ikinci uygulama hizmeti ortamı hello ilk uygulama hizmeti (yalnızca giden IP adresidir 192.23.1.2) böylece hello arasında güvenli iletişim sağlama ortamı, Uygulama hizmeti ortamları.

## <a name="additional-links-and-information"></a>Ek bağlantıları ve bilgileri
Tüm makaleler ve nasıl-için uygulama hizmeti ortamları hello kullanılabilir için kullanıcının [uygulama hizmeti ortamları için Benioku](../app-service/app-service-app-service-environments-readme.md).

İlgili Ayrıntılar gelen App Service ortamları tarafından kullanılan bağlantı noktaları ve ağ güvenlik grupları toocontrol kullanarak gelen trafik kullanılabilir [burada][controllinginboundtraffic].

Kullanıcı tanımlı yollar toogrant giden Internet erişimi tooApp hizmeti ortamları kullanımıyla ilgili ayrıntılar bu konuda kullanılabilir [makale][ExpressRoute]. 

<!-- LINKS -->
[virtualnetwork]: http://azure.microsoft.com/services/virtual-network/
[controllinginboundtraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[ExpressRoute]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/

<!-- IMAGES -->
[GeneralNetworkFlows]: ./media/app-service-app-service-environment-network-architecture-overview/NetworkOverview-1.png
[OutboundIPAddress]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundIPAddress-1.png
[OutboundNetworkAddresses]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundNetworkAddresses-1.png
[CallsBetweenAppServiceEnvironments]: ./media/app-service-app-service-environment-network-architecture-overview/CallsBetweenEnvironments-1.png

