---
title: "aaaSecurely bağlanma tooBackEnd bir uygulama hizmeti ortamı kaynaklardan"
description: "Nasıl toosecurely toobackend kaynaklar bağlantı bir uygulama hizmeti ortamındaki hakkında bilgi edinin."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: f82eb283-a6e7-4923-a00b-4b4ccf7c4b5b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 6311d3fc301512ea3c4ed8f14f268f75755aa415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="securely-connecting-toobackend-resources-from-an-app-service-environment"></a>Güvenli bir şekilde bağlanma tooBackend bir uygulama hizmeti ortamı kaynaklardan
## <a name="overview"></a>Genel Bakış
Uygulama hizmeti ortamı'nda her zaman oluşturulduğundan **ya da** bir Azure Resource Manager sanal ağ **veya** Klasik dağıtım modeli [sanal ağ] [ virtualnetwork], bir uygulama hizmeti ortamı tooother arka uç kaynaklarına giden bağlantılar yalnızca hello sanal ağ üzerinden akış.  Haziran 2016'da yapılan son bir değişiklikle ASEs ortak adres aralıkları veya RFC1918 adres alanları (özel adresleri) kullanan sanal ağları içinde dağıtılabilir.  

Örneğin, bağlantı noktası 1433 kilitli olan sanal makinelerin bir kümede çalışan bir SQL Server olabilir.  Merhaba endpoint tooonly üzerindeki diğer kaynaklardan erişime izin ACLd olabilir hello aynı sanal ağ.  

Başka bir örnek olarak, hassas uç noktaları şirket içi ve çalıştıran ya da aracılığıyla bağlı tooAzure [siteden siteye] [ SiteToSite] veya [Azure ExpressRoute] [ ExpressRoute] bağlantıları.  Sonuç olarak, sanal ağlar yalnızca kaynaklarında toohello siteden siteye bağlı veya ExpressRoute tüneller mümkün tooaccess şirket içi uç noktaları olacaktır.

Tüm bu senaryolar için bir uygulama hizmeti ortamı üzerinde çalışan uygulamalar olması mümkün toosecurely bağlanan toohello çeşitli sunucuları ve kaynakları.  Bir uygulama hizmeti ortamı tooprivate uç noktaları hello içinde çalışan uygulamalardan giden trafiği aynı sanal ağ (veya bağlı toohello aynı sanal ağ), yalnızca akış hello sanal ağ üzerinden olacaktır.  Uç noktaları üzerinden akar değil giden trafiği tooprivate genel Internet hello.

Bir uyarı toooutbound trafiği sanal ağ içindeki bir uygulama hizmeti ortamı tooendpoints gelen geçerlidir.  Uygulama hizmeti ortamları uç noktaları hello bulunan sanal makinelerin erişemiyor **aynı** uygulama hizmeti ortamı hello gibi bir alt ağ.  Uygulama hizmeti ortamları yalnızca hello uygulama hizmeti ortamı'tarafından özel kullanım için ayrılmış bir alt ağ içinde dağıtılan sürece bu normalde bir sorun olmamalıdır.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a>Giden bağlantısı ve DNS gereksinimleri
Bir uygulama hizmeti ortamı toofunction için düzgün şekilde giden erişim toovarious uç noktaları gerektirir. Tam bir ana tarafından kullanılan hello dış uç noktalar hello hello "Ağ bağlantısı gerekli" bölümünde listelenmiştir [ExpressRoute için ağ yapılandırması](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) makalesi.

Uygulama hizmeti ortamları hello sanal ağ için yapılandırılmış geçerli bir DNS altyapısı gerektirir.  Bir uygulama hizmeti ortamı oluşturulduktan sonra herhangi bir nedenle hello için DNS yapılandırması değiştirildiğinde, geliştiricilerin bir uygulama hizmeti ortamı toopick hello yeni DNS yapılandırması zorlayabilirsiniz.  Merhaba uygulama hizmeti ortamı Hello üstünde bulunan hello "Yeniden Başlat" simgesini kullanarak çalışırken bir ortamı yeniden başlatma tetikleyen yönetim dikey penceresinde hello portal hello ortamı toopick hello yeni DNS yapılandırması neden olur.

Merhaba vnet hiçbir özel DNS sunucularında Kurulum zaman önceki toocreating bir uygulama hizmeti ortamı öncesinde olması önerilir.  Bir uygulama hizmeti ortamı oluşturulurken bir sanal ağın DNS yapılandırması değiştiyse, hello uygulama hizmeti ortamı oluşturma işlemi başarısız neden olur.  Özel bir DNS sunucusu üzerinde hello varsa, benzer bir damarlı içinde başka bir VPN ağ geçidi ve hello DNS sunucusu erişilemez veya kullanılamaz hello uygulama hizmeti ortamı oluşturma işlemi de başarısız olacak sonudur.

## <a name="connecting-tooa-sql-server"></a>SQL Server tooa bağlanma
Yaygın olarak kullanılan SQL Server yapılandırması 1433 bağlantı noktasını dinleyen bir uç nokta vardır:

![SQL sunucusu uç noktası][SqlServerEndpoint]

Trafik toothis endpoint kısıtlama için iki yaklaşım vardır:

* [Ağ erişim denetim listeleri] [ NetworkAccessControlLists] (ağ ACL'leri)
* [Ağ güvenlik grupları][NetworkSecurityGroups]

## <a name="restricting-access-with-a-network-acl"></a>Bir ağ ACL ile erişimi kısıtlama
Bağlantı noktası 1433'ü bir ağ erişim denetimi listesi kullanılarak güvenli hale getirilebilir.  bir sanal ağ içinde kaynaklanan whitelists istemci aşağıdaki Hello örnekte adresleri ve diğer istemciler tooall erişimi.

![Ağ erişim denetim listesi örneği][NetworkAccessControlListExample]

Uygulama hizmeti ortamı'nda çalışan tüm uygulamaların aynı sanal ağ hello SQL Server hello kullanarak mümkün tooconnect toohello SQL Server örneği olarak hello **VNet iç** hello SQL Server sanal makine için IP adresi.  

Merhaba örnek bağlantı dizesi başvuruları aşağıda özel IP adresini kullanarak SQL Server hello.

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

Merhaba sanal makine genel bir uç nokta da olsa da, hello genel IP adresi kullanılarak yapılan bağlantı girişimleri hello ağ ACL nedeniyle kabul edilmeyecek. 

## <a name="restricting-access-with-a-network-security-group"></a>Bir ağ güvenlik grubu ile erişimi kısıtlama
Bir ağ güvenlik grubuyla erişim güvenliğini sağlamak için alternatif bir yaklaşımdır.  Ağ güvenlik grupları uygulanan tooindividual sanal makine ya da sanal makineleri içeren tooa alt olabilir.

İlk ağ güvenlik grubu oluşturulan toobe gerekir:

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

Erişim tooonly VNet iç trafiği kısıtlama, bir ağ güvenlik grubuyla çok kolaydır.  bir ağ güvenlik grubundaki Hello varsayılan kuralları yalnızca erişime izin hello'diğer ağ istemcilerden aynı sanal ağ.

Sonuç olarak erişim tooSQL kilitleme sunucu bir ağ güvenlik grubu, varsayılan kuralları tooeither hello SQL Server ya da hello sanal makineleri içeren hello alt çalışan sanal makineler ile uygulama olarak kadar basittir.

Aşağıdaki Hello örneği bir ağ güvenlik grubu toohello içeren alt geçerlidir:

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

Merhaba Nihai sonuç, VNet iç erişim sağlarken dış erişimi engelleme güvenlik kurallar kümesidir:

![Varsayılan ağ güvenlik kuralları][DefaultNetworkSecurityRules]

## <a name="getting-started"></a>Başlarken
Tüm makaleler ve nasıl-için uygulama hizmeti ortamları hello kullanılabilir için kullanıcının [uygulama hizmeti ortamları için Benioku](../app-service/app-service-app-service-environments-readme.md).

Uygulama hizmeti ortamları ile çalışmaya tooget bakın [giriş tooApp hizmeti ortamı][IntroToAppServiceEnvironment]

Denetleme gelen trafiği tooyour uygulama hizmeti ortamı geçici daha fazla bilgi için bkz [gelen trafik tooan uygulama hizmeti ortamı denetleme][ControlInboundASE]

Hello Azure App Service platformu hakkında daha fazla bilgi için bkz: [Azure App Service][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ControlInboundASE]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/ 

<!-- IMAGES -->
[SqlServerEndpoint]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 
