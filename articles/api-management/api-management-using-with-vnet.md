---
title: "Sanal ağlarla aaaHow toouse Azure API Yönetimi"
description: "Toosetup bir bağlantı tooa sanal ağında Azure API Management ve erişim web üzerinden hizmetleri nasıl öğrenin."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 64b58f7b-ca22-47dc-89c0-f6bb0af27a48
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 426b3974e4fed7daffdb0c3f02381edbc326dc28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-api-management-with-virtual-networks"></a>Nasıl toouse Azure API Management ile sanal ağlar
Azure sanal ağlar (Vnet'ler) herhangi birini Azure kaynaklarınızı denetim Internet olmayan routeable ağ erişimi tooplace izin verin. Bu ağlar sonra çeşitli VPN teknolojilerini kullanarak bağlı tooyour şirket içi ağlar olabilir. Azure sanal ağlar hakkında daha fazla Başlat burada hello bilgilerle toolearn: [Azure Virtual Network'e genel bakış](../virtual-network/virtual-networks-overview.md).

Merhaba ağından arka uç hizmetlerini erişebilmesi için azure API Management hello sanal ağ (VNET) içinde dağıtılabilir. Geliştirici Portalı ve API ağ geçidi Merhaba, yapılandırılmış toobe hello Internet ya da yalnızca hello sanal ağ içinde erişilebilir.

> [!NOTE]
> Azure API Management hem Klasik hem de Azure Kaynak Yöneticisi sanal ağlar destekler.
>
>

## <a name="enable-vpn"></a>Etkinleştir VNET bağlantısı
> [!NOTE]
> VNET bağlantısı hello kullanılabilir **Premium** ve **Geliştirici** katmanları. Merhaba katmanları arasında tooswitch API Management hizmetiniz hello Azure portalını açın, sonra hello açın **ölçek ve fiyatlandırma** sekmesi. Merhaba altında **fiyatlandırma katmanı** bölümünde hello Premium veya Geliştirici katmanı seçin ve Kaydet'i tıklatın.
>

tooenable VNET bağlantısı, API Management hizmetiniz hello Azure portalını açın ve açmak hello **sanal ağ** sayfası.

![Sanal ağ menü API Yönetimi][api-management-using-vnet-menu]

İstenen hello erişim türünü seçin:

* **Dış**: hello API Yönetimi ağ geçidi ve Geliştirici Portalı erişilebilir ortak Internet üzerinden bir dış yük dengeleyici hello. Merhaba ağ geçidi hello sanal ağ içindeki kaynaklara erişebilir.

![Ortak eşleme][api-management-vnet-public]

* **İç**: hello API Yönetimi ağ geçidi ve Geliştirici Portalı bir iç yük dengeleyici aracılığıyla hello sanal ağ içinde yalnızca üzerinden erişilebilir. Merhaba ağ geçidi hello sanal ağ içindeki kaynaklara erişebilir.

![Özel eşleme][api-management-vnet-private]

API Management hizmetiniz burada sağlanan tüm bölgelerin bir listesi şimdi görürsünüz. VNET ve her bölge için alt ağ seçin. Merhaba liste Klasik ve Resource Manager yapılandırmakta olduğunuz hello bölgede kurulmuş, Azure aboneliklerinize bulunan sanal ağlar ile doldurulur.

> [!NOTE]
> **Hizmet uç noktası** Ağ Geçidi/Proxy, yayımcı portalında, Geliştirici Portalı, GIT ve hello doğrudan yönetim uç noktası diyagramı yukarıda hello içerir.
> **Yönetim uç noktası** hello diyagramı yukarıda yer hello hizmet toomanage yapılandırması Azure portal ve Powershell aracılığıyla barındırılan hello uç noktası.
> Ayrıca, aşağıdakilere dikkat edin, hello diyagramı IP adreslerini çeşitli uç için API Management hizmeti göstermektedir olsa bile, **yalnızca** üzerinde yapılandırılmış kendi ana bilgisayar adları yanıt verir.

> [!IMPORTANT]
> Bir Azure API Management örneği tooa Resource Manager VNET'i dağıtırken hello hizmeti Azure API Management örnekleri dışında başka kaynaklar içeren özel bir alt ağda olmalıdır. Bir Azure API Management örneği tooa içeren diğer kaynaklar, hello dağıtım Resource Manager VNET'i alt girişimde toodeploy başarısız olur.
>
>

![VPN seçin][api-management-setup-vpn-select]

Tıklatın **kaydetmek** Merhaba ekranında hello üstünde.

> [!NOTE]
> Merhaba VIP adresi hello API Management örneğinin VNET etkin veya devre dışı her zaman değiştirir.  
> Merhaba VIP adresi API Management gelen taşındığında da değiştirir **dış** çok**dahili** veya tersi
>


> [!IMPORTANT]
> API Management bir sanal ağdan kaldırın veya bir içinde dağıtılan hello değiştirin, daha önce kullanılan VNET kalabileceği hello için too4 saatleri kilitli. Bu süre boyunca bu değil olası toodelete hello VNET veya kaldırılacak yeni bir kaynak tooit dağıtın.

## <a name="enable-vnet-powershell"></a>PowerShell cmdlet'lerini kullanarak etkinleştir VNET bağlantısı
VNET bağlantısı hello PowerShell cmdlet'lerini kullanarak da etkinleştirebilirsiniz

* **Bir sanal ağ içinde bir API Management hizmeti oluşturma**: hello cmdlet'ini kullanın [yeni AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate VNET içinde bir Azure API Management hizmeti.

* **VNET içinde varolan bir API Management hizmetini dağıtma**: hello cmdlet'ini kullanın [güncelleştirme AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove bir sanal ağ içinde var olan bir Azure API Management hizmeti.

## <a name="connect-vnet"></a>Bir sanal ağ içinde barındırılan tooa web hizmetine bağlanma
API Management hizmetiniz bağlı toohello VNET sonra içindeki arka uç hizmetlerine erişme ortak Hizmetleri erişimden çok farklı değildir. Yalnızca hello hello yerel IP adresi veya web hizmeti (DNS sunucusu VNET hello için yapılandırılmışsa) hello ana bilgisayar adı yazın **Web hizmeti URL'si** alan yeni bir API oluştururken veya var olan bir düzenleme.

![VPN bağlantısını API ekleme][api-management-setup-vpn-add-api]

## <a name="network-configuration-issues"></a>Ortak ağ yapılandırma sorunları
Sanal ağınıza API Management hizmeti dağıtırken oluşabilecek yaygın yetersizliğini sorunların bir listesi verilmiştir.

* **Özel DNS Sunucusu Kurulumu**: hello API Management hizmeti üzerinde çeşitli Azure hizmetlerine bağlıdır. API Management, özel bir DNS sunucusu ile bir VNET içinde barındırıldığında Azure hizmetlerin tooresolve hello ana bilgisayar adı gerekiyor. Lütfen izleyin [bu](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) özel DNS kurulumu hakkında yönergeler. Hello bağlantı noktalarını tabloda ve diğer ağ gereksinimleri başvuru konusuna bakın.

> [!IMPORTANT]
> Merhaba VNET özel DNS sunucularını kullanıyorsanız, ayarladığınız, önerilen **önce** içine bir API Management hizmeti dağıtma. Aksi takdirde, çok hello API Management hizmeti hello DNS sunucuları (s) değiştirdiğinizde hello çalıştırarak güncelleştirmeniz [ağ yapılandırma işlemi Uygula](https://docs.microsoft.com/en-us/rest/api/apimanagement/apimanagementservice#ApiManagementService_ApplyNetworkConfigurationUpdates)

* **API yönetimi için gereken bağlantı noktaları**: gelen ve giden trafik API Management dağıtıldığı hello alt içine kullanılarak denetlenebilir [ağ güvenlik grubu][Network Security Group]. Bu bağlantı noktalarının hiçbirinde yoksa, API Management düzgün çalışmayabilir ve erişilemez duruma gelebilir. Bir veya daha fazla engellenen Bu bağlantı noktalarına sahip başka bir ortak yetersizliğini API Management bir VNET ile birlikte kullanırken bir sorundur.

API Management hizmet örneği sanal ağ içinde barındırıldığında, aşağıdaki tablonun hello hello bağlantı noktaları kullanılır.

| Kaynak / hedef bağlantı noktaları | Yön | Aktarım Protokolü | Amaç | Kaynak / hedef | Erişim türü |
| --- | --- | --- | --- | --- | --- |
| * / 80, 443 |Gelen |TCP |İstemci iletişimi tooAPI Yönetimi |INTERNET / VIRTUAL_NETWORK |Dış |
| * / 3443 |Gelen |TCP |Azure portalı ve Powershell yönetim uç noktası |INTERNET / VIRTUAL_NETWORK |Dış & iç |
| * / 80, 443 |Giden |TCP |Azure depolama ve Azure hizmet veri yolu bağımlılığı |VIRTUAL_NETWORK / INTERNET |Dış & iç |
| * / 1433 |Giden |TCP |Azure SQL bağımlılığı |VIRTUAL_NETWORK / INTERNET |Dış & iç |
| * / 11000 - 11999 |Giden |TCP |Azure SQL V12 bağımlılığı |VIRTUAL_NETWORK / INTERNET |Dış & iç |
| * / 14000 - 14999 |Giden |TCP |Azure SQL V12 bağımlılığı |VIRTUAL_NETWORK / INTERNET |Dış & iç |
| * / 5671 |Giden |AMQP |Bağımlılık günlük tooEvent Hub İlkesi ve İzleme Aracısı |VIRTUAL_NETWORK / INTERNET |Dış & iç |
| 6381 - 6383 / 6381 - 6383 |Gelen ve giden |UDP |Redis önbelleği bağımlılığı |VIRTUAL_NETWORK / VIRTUAL_NETWORK |Dış & iç |-
| * / 445 |Giden |TCP |Azure dosya paylaşımı için GIT bağımlılığı |VIRTUAL_NETWORK / INTERNET |Dış & iç |
| * / * | Gelen |TCP |Azure altyapı yük dengeleyici | AZURE_LOAD_BALANCER / VIRTUAL_NETWORK |Dış & iç |

* **SSL işlevselliği**: tooenable SSL sertifika zinciri oluşturma ve doğrulama hello API Management hizmeti, giden ağ bağlantısı tooocsp.msocsp.com, mscrl.microsoft.com ve crl.microsoft.com gerekiyor. Merhaba tam zincir toohello CA kök tooAPI yönetim karşıya yüklediğiniz herhangi bir sertifika içeriyorsa, bu bağımlılık gerekli değil.

* **DNS erişim**: DNS sunucuları ile iletişim için bağlantı noktası 53 giden erişim gereklidir. Özel bir DNS sunucusu üzerinde varsa bir VPN ağ geçidi diğer ucundaki Merhaba, hello DNS Sunucusu API Management barındırma hello alt ağ üzerinden erişilebilir olması gerekir.

* **Ölçümleri ve sistem durumu izleme**: hangi etki alanları aşağıdaki hello altında çözmek giden ağ bağlantısı tooAzure izleme uç noktaları,: global.metrics.nsatc.net, shoebox2.metrics.nsatc.net, prod3.metrics.nsatc.net.

* **Hızlı rota Kurulum**: genel bir müşteri yapılandırma toodefine giden Internet trafiği tooinstead akış içi zorlar kendi varsayılan yol (0.0.0.0/0) olacaktır. Bu trafik akışı neredeyse şaşmaz biçimde hello giden trafiği ya da engellenen şirket içi veya NAT tooan tanınmayan artık çeşitli Azure uç noktaları ile çalışma adresleri kümesini 'd olduğundan Azure API Management ile bağlantısını keser. Merhaba toodefine bir (veya daha fazla) kullanıcı tanımlı yollar çözümdür ([Udr'ler][UDRs]) hello Azure API Management içeren hello alt ağdaki. Bir UDR hello varsayılan yol yerine uyulacaktır alt özel yollar tanımlar.
  Mümkünse, bu yapılandırma aşağıdaki toouse hello önerilir:
 * Merhaba ExpressRoute yapılandırma 0.0.0.0/0 tanıtır ve varsayılan olarak tüm giden trafiği şirket içi zorlamalı tünel oluşturur.
 * Merhaba uygulanan UDR toohello alt ağ Hello Azure API Management içeren Internet sonraki atlama türü olan 0.0.0.0/0 tanımlar.
 Merhaba birleşik bu adımları hello alt düzey UDR hello böylece Azure API Management hello giden Internet erişimden sağlama zorlanan tünel, ExpressRoute üzerinden öncelik kazanır etkisidir.

>[!WARNING]  
>Azure API Management ile ExpressRoute yapılandırmaları desteklenmez, **yanlış cross-hello ortak eşleme yolu toohello özel eşleme yolu yolları tanıtma**. Yapılandırılmış, ortak eşleme sahip ExpressRoute yapılandırmaları alacağı Yol tanıtımlarını Microsoft'tan çok sayıda Microsoft Azure IP adres aralıkları için. Bu adres aralıklarını yanlış cross-hello özel eşleme yoluna tanıtılan varsa, hello sonuç tüm giden ağ paketlerinin hello Azure API Management örneğinin alt ağdan hatalı zorlamalı tünel tooa müşterinin şirket içi ağ olmasıdır Altyapı. Bu ağ akışı Azure API Management keser. Merhaba ortak eşleme yolu toohello özel eşleme yolu toostop arası reklam yolları Hello çözüm toothis sorunudur.


## <a name="troubleshooting"></a>Sorunlarını giderme
Değişiklikleri tooyour ağ yaparken çok başvuran[NetworkStatus API](https://docs.microsoft.com/en-us/rest/api/apimanagement/networkstatus), hello API Management hizmeti erişim tooany Merhaba, bağlı olduğu kritik kaynaklara değil kaybederse toovalidate. Merhaba bağlantı durumunun her 15 dakikada güncelleştirilmesi gerekir.

## <a name="limitations"></a>Sınırlamaları
* API Management örnekleri içeren bir alt ağ başka bir Azure kaynak türleri içeremez.
* Merhaba alt ağı ve hello API Management hizmeti olması gerekir. aynı abonelik hello.
* API Management örnekleri içeren bir alt ağ, abonelikler arasında taşınamaz.
* Merhaba aralığı iç IP adresi kullanılabilir yalnızca bir iç sanal ağ kullanırken, belirtilen [RFC 1918](https://tools.ietf.org/html/rfc1918), bir ortak IP adresi sağlanamaz.
* Bölgeli API Management dağıtımları için yapılandırılmış, iç sanal ağlar ile kullanıcılar, kendi yük hello DNS oldukları gibi Dengeleme yönetmek için sorumludur.


## <a name="related-content"></a>İlgili içerik
* [VPN ağ geçidi kullanarak bir sanal ağ toobackend bağlanma](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti)
* [Farklı dağıtım modelinden bir sanal ağa bağlanma](../vpn-gateway/vpn-gateway-connect-different-deployment-models-powershell.md)
* [Azure API Management'te toouse hello API denetçisi tootrace nasıl çağırır](api-management-howto-api-inspector.md)

[api-management-using-vnet-menu]: ./media/api-management-using-with-vnet/api-management-menu-vnet.png
[api-management-setup-vpn-select]: ./media/api-management-using-with-vnet/api-management-using-vnet-type.png
[api-management-setup-vpn-select]: ./media/api-management-using-with-vnet/api-management-using-vnet-select.png
[api-management-setup-vpn-add-api]: ./media/api-management-using-with-vnet/api-management-using-vnet-add-api.png
[api-management-vnet-private]: ./media/api-management-using-with-vnet/api-management-vnet-private.png
[api-management-vnet-public]: ./media/api-management-using-with-vnet/api-management-vnet-public.png

[Enable VPN connections]: #enable-vpn
[Connect tooa web service behind VPN]: #connect-vpn
[Related content]: #related-content

[UDRs]: ../virtual-network/virtual-networks-udr-overview.md
[Network Security Group]: ../virtual-network/virtual-networks-nsg.md
