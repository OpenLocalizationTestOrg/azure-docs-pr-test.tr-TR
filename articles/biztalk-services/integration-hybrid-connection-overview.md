---
title: "aaaHybrid bağlantılara genel bakış | Microsoft Docs"
description: "Karma Bağlantılar, güvenlik, TCP bağlantı noktaları ve desteklenen yapılandırmalar hakkında bilgi edinin. MABS, WABS."
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: 216e4927-6863-46e7-aa7c-77fec575c8a6
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: f092c6019aae761e1e73f13d1af8446a896515c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-connections-overview"></a>Karma Bağlantılara genel bakış

> [!IMPORTANT]
> BizTalk Karma Bağlantılar kullanımdan kalktı ve yerine App Service Karma Bağlantılar kullanıma sunuldu. Daha fazla bilgi için mevcut BizTalk karma bağlantılar nasıl toomanage bakın dahil olmak üzere [Azure App Service karma bağlantılar](../app-service/app-service-hybrid-connections.md).

Giriş tooHybrid bağlantıları, hello desteklenen yapılandırmaları listeler ve gerekli TCP bağlantı noktalarını listeler hello.

## <a name="what-is-a-hybrid-connection"></a>Karma bağlantı nedir
Karma Bağlantılar, Azure BizTalk Services’ın bir özelliğidir. Karma bağlantılar, bir kolay ve uygun şekilde tooconnect hello Web Apps Özelliği Azure App Service'te (önceden Web siteleri) ve Azure App Service (önceden Mobile Services) tooon içi kaynaklar, güvenlik duvarının arkasında hello Mobile Apps özelliği sağlar.

![Karma Bağlantılar][HCImage]

Karma Bağlantılar’ın yararları:

* Web Uygulamaları ve Mobile Apps mevcut şirket içi verilere ve hizmetlere güvenli erişebilir.
* Birden çok Web uygulamaları veya Mobile Apps karma bağlantı tooaccess bir şirket içi kaynağa paylaşabilirsiniz.
* En az TCP bağlantı noktaları gerekli tooaccess ağınıza şunlardır.
* Karma bağlantılar kullanarak uygulamaları, yayımlanan hello belirli şirket içi kaynağa hello karma bağlantı erişim.
* SQL Server, MySQL, HTTP Web API'leri ve birçok özel Web hizmeti gibi statik TCP bağlantı kullanan tooany şirket içi kaynaklara bağlanabilir.
  
  > [!NOTE]
  > Dinamik bağlantı noktaları (örneğin, FTP Pasif modu veya Genişletilmiş Pasif modu) kullanan TCP tabanlı hizmetler şu anda desteklenmemektedir. LDAP de desteklenmemektedir. LDAP statik bir TCP bağlantı noktasını kullansa da, UDP de kullanmaktadır. Sonuç olarak desteklenmemektedir.
  > 
  > 
* Web Uygulamaları (.NET, PHP, Java, Python, Node.js) ve Mobile Apps (Node.js, .NET) tarafından desteklenen tüm altyapılarla kullanılabilir.
* Web uygulamaları ve Mobile Apps tam olarak hello şirket içi kaynaklara erişebilir aynı şekilde hello Web veya mobil uygulama yerel ağınızda olarak bulunuyorsa. Örneğin, aynı bağlantı dizesine kullanılan şirket içi Azure üzerinde de kullanılabilir hello.

Karma bağlantılar da kurum yöneticilerinin denetleyip görselleştirmesini de dahil olmak üzere karma uygulamalar tarafından erişilen hello şirket kaynaklarına sağlar:

* Grup İlkesi ayarlarını kullanarak, yöneticiler karma bağlantılar hello ağda izin ve aynı zamanda karma uygulamalar tarafından erişilen kaynakları atayabilir.
* Hello şirket ağındaki etkinlik ve Denetim günlükleri karma bağlantılar tarafından erişilen hello kaynaklar görünürlük sağlar.

## <a name="example-scenarios"></a>Örnek senaryolar
Karma bağlantılar aşağıdaki altyapı ve uygulama bileşimlerini hello destekler:

* .NET framework erişim tooSQL sunucu
* .NET framework erişim tooHTTP/HTTPS Hizmetleri WebClient ile
* PHP erişim tooSQL Server, MySQL
* Java erişim tooSQL Server, MySQL ve Oracle
* Java erişim tooHTTP/HTTPS Hizmetleri

Karma bağlantılar tooaccess kullanarak SQL Server içi, hello aşağıdakileri göz önünde bulundurun:

* SQL Express adlandırılmış örnekleri statik bağlantı noktaları yapılandırılmış toouse olması gerekir. Varsayılan olarak, SQL Express adlandırılmış örnekleri dinamik bağlantı noktalarını kullanır.
* SQL Express Varsayılan Örnekleri statik bağlantı noktasını kullansa da TCP’nin de etkinleştirilmesi gerekir. Varsayılan olarak, TCP etkin değildir.
* Kümeleme veya kullanılabilirlik grupları kullanılırken hello `MultiSubnetFailover=true` modu şu anda desteklenmiyor.
* Merhaba `ApplicationIntent=ReadOnly` şu anda desteklenmiyor.
* SQL kimlik doğrulaması hello Azure uygulamanızı ve hello şirket içi SQL server tarafından desteklenen hello uçtan uca yetkilendirme yöntemi olarak gerekli olabilir.

## <a name="security-and-ports"></a>Güvenlik ve bağlantı noktaları
Karma bağlantılar kullanabilmesi paylaşılan erişim imzası (SAS) yetkilendirme toosecure hello bağlantıları hello Azure ' uygulamaları ve hello şirket içi karma Bağlantı Yöneticisi toohello karma bağlantı. Merhaba uygulama için ayrı bağlantı anahtarları oluşturulur ve hello içi karma Bağlantı Yöneticisi. Bu bağlantı anahtarları uzatılabilir ve bağımsız olarak iptal edilebilir.

Merhaba içi karma Bağlantı Yöneticisi ve hello anahtarları toohello uygulamaları sorunsuz ve güvenli dağıtım için karma bağlantılar sağlar.

Bkz. [Karma Bağlantıları Oluşturma ve Yönetme](integration-hybrid-connection-create-manage.md).

*Uygulama yetkilendirmesi karma bağlantı hello ayrı*. Uygun herhangi bir yetkilendirme yöntemi kullanılabilir. Merhaba yetkilendirme yöntemi hello Azure Bulut ve hello şirket içi bileşenler arasında desteklenen hello uçtan uca yetkilendirme yöntemlerine bağlıdır. Örneğin, Azure uygulamanız bir şirket içi SQL Server’a erişir. Bu senaryoda, SQL yetkilendirme desteklenen uçtan uca hello yetkilendirme yöntemi olabilir.

#### <a name="tcp-ports"></a>TCP bağlantı noktaları
Karma Bağlantılar için, yalnızca özel ağınızdan giden TCP veya HTTP bağlantısı gerekir. Değil, herhangi bir güvenlik duvarı bağlantı tooopen gerekir veya ağ çevre yapılandırmasını tooallow gelen bağlantılara ağınıza değiştirin.

TCP bağlantı noktaları aşağıdaki hello karma bağlantılar tarafından kullanılır:

| Bağlantı noktası | Neden gerekiyor |
| --- | --- |
| 9350 - 9354 |Bu bağlantı noktaları veri aktarımı için kullanılır. TCP bağlantısı olup olmadığını hello hizmet veri yolu Geçişi Yöneticisi bağlantı noktası 9350 toodetermine araştırmaları. Varsa, 9352 adlı bağlantı noktasının da olduğu varsayılır. Veri trafiği 9352 bağlantı noktası üzerinden gider. <br/><br/>Giden bağlantılar toothese bağlantı noktalarına izin verecek. |
| 5671 |9352 adlı bağlantı noktası veri trafiği için kullanıldığında, bağlantı noktası 5671 hello denetim kanalını kullanılır. <br/><br/>Giden bağlantılar toothis bağlantı noktasına izin verin. |
| 80, 443 |Bu bağlantı noktaları, bazı veri isteklerini tooAzure için kullanılır. Ayrıca, 9352 ve 5671 bağlantı noktaları kullanılabilir değilse *sonra* 80 ve 443 numaralı bağlantı noktalarını veri iletimi ve hello denetim kanalı için kullanılan hello geri dönüş bağlantı noktaları olduğundan.<br/><br/>Giden bağlantılar toothese bağlantı noktalarına izin verecek. <br/><br/>**Not** olmayan diğer TCP bağlantı noktaları geri dönüş bağlantı noktaları hello yerine hello gibi toouse bu önerilir. Merhaba HTTP/WebSocket, veri kanallarına yönelik yerel TCP yerine hello protokol olarak kullanılır. Düşük performansa neden olabilir. |

## <a name="next-steps"></a>Sonraki adımlar
[Karma Bağlantıları oluşturma ve yönetme](integration-hybrid-connection-create-manage.md)<br/>
[Azure Web Apps tooan bağlanmak şirket içi kaynak](../app-service-web/web-sites-hybrid-connection-get-started.md)<br/>
[Bir Azure web uygulamasından tooon içi SQL Server'a bağlanma](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)<br/>

## <a name="see-also"></a>Ayrıca Bkz.
[Microsoft Azure’de BizTalk hizmetlerinin yönetilmesi için REST API](http://msdn.microsoft.com/library/azure/dn232347.aspx)
[BizTalk Services: Sürümler Grafiği](biztalk-editions-feature-chart.md)<br/>
[Azure portalını kullanarak BizTalk Hizmeti oluşturma](biztalk-provision-services.md)<br/>
[BizTalk Services: Pano, İzleyici ve Ölçek sekmeleri](biztalk-dashboard-monitor-scale-tabs.md)<br/>

[HCImage]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionImage.png
[HybridConnectionTab]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionManageConn.png
