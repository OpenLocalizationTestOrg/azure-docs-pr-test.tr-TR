---
title: aaaAzure Virtual Network SSS | Microsoft Docs
description: "Microsoft Azure sanal ağlar hakkında sık sorulan soruları yanıtlar toohello."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 54bee086-a8a5-4312-9866-19a1fba913d0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/18/2017
ms.author: jdial
ms.openlocfilehash: c2f9faee41b9c45e8bb196c58282d597ae732e54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-network-frequently-asked-questions-faq"></a>Azure sanal ağı sık sorulan sorular (SSS)

## <a name="virtual-network-basics"></a>Sanal ağ temelleri

### <a name="what-is-an-azure-virtual-network-vnet"></a>Bir Azure sanal ağı (VNet) nedir?
Bir Azure sanal ağı (VNet), kendi ağ hello bulutta gösterimidir. Merhaba ayrılmış Azure bulut tooyour abonelik mantıksal yalıtımının olur. Sanal ağlar tooprovision kullanın ve sanal özel ağları (VPN'ler) Azure ve isteğe bağlı olarak, diğer sanal ağlar Azure veya şirket içi sanal ağlara bağlantı hello yönetmek karma veya şirket içi BT altyapısı toocreate çözümleri. Oluşturduğunuz her bir Vnet'teki kendi CIDR bloğu olan ve hello CIDR blokları çakışmaması sürece bağlantılı tooother sanal ağlar ve şirket içi ağlar olabilir. Ayrıca sanal ağlar için DNS sunucu ayarları denetimi ve alt ağlar içine hello VNet ayrılmasını vardır.

Sanal ağlar için kullanın:

* Bir adanmış özel yalnızca bulut VNet çözümünüz için bir şirket içi yapılandırma gerektirmeyen bazen oluşturun. Bir sanal ağ oluşturduğunuzda, hizmetleri ve sanal makineleri sanal ağınızın içinde doğrudan ve güvenli bir şekilde birbirleri ile Merhaba bulutta iletişim kurabilir. Bu trafiği güvenli bir şekilde hello VNet içinde tutar, ancak hala tooconfigure uç nokta bağlantılarında hello VM'ler ve Internet iletişimi, çözümün parçası olarak gerekli hizmetler sağlar.
* Güvenli bir şekilde, veri merkezinizdeki sanal ağlar ile genişletmek, veri merkezi kapasitenizi geleneksel siteden siteye (S2S) VPN toosecurely ölçek oluşturabilirsiniz. S2S VPN IPSec tooprovide şirket VPN ağ geçidi ve Azure arasında güvenli bir bağlantı kullanın.
* Karma bulut senaryolara olanak sanal ağlar size esneklik toosupport karma bulut senaryolarında bir dizi hello. Bulut tabanlı uygulamalar tooany türüne ana bilgisayarlar gibi şirket içi sistem Unix sistemlerinden ve güvenli bir şekilde bağlanabilir.

### <a name="how-do-i-know-if-i-need-a-vnet"></a>Bir VNet gerekip gerekmediğini nasıl anlarım?
Merhaba [sanal ağa genel bakış](virtual-networks-overview.md) makale hello için en iyi ağ tasarım seçeneği, karar vermenize yardımcı olacak bir karar tablo sağlar.

### <a name="how-do-i-get-started"></a>Nasıl kullanmaya başlayabilirim?
Merhaba ziyaret [sanal ağ belgeleri](https://docs.microsoft.com/azure/virtual-network/) tooget başlatıldı. Bu içerik tüm hello VNet özellikleri için genel bakış ve dağıtım bilgileri sağlar.

### <a name="can-i-use-vnets-without-cross-premises-connectivity"></a>Sanal ağlar arası bağlantı kullanabilir miyim?
Evet. Karma bağlantısı kullanmadan bir VNet kullanabilirsiniz. Toorun Microsoft Windows Server Active Directory etki alanı denetleyicileri ve azure'da SharePoint grupları istiyorsanız, bu özellikle yararlıdır.

### <a name="can-i-perform-wan-optimization-between-vnets-or-a-vnet-and-my-on-premises-data-center"></a>Sanal ağlar veya bir VNet ile my şirket içi veri merkezi arasında WAN iyileştirmesi gerçekleştirebilir miyim?

Evet. Dağıtabilmeniz için bir [WAN iyileştirmesi ağ sanal gereç](https://azure.microsoft.com/marketplace/?term=wan+optimization) hello Azure Market üzerinden birkaç satıcılardan.

## <a name="configuration"></a>Yapılandırma

### <a name="what-tools-do-i-use-toocreate-a-vnet"></a>Araçlar ne toocreate VNet kullanabilir miyim?
Araçlar toocreate aşağıdaki hello kullanın veya bir sanal ağ yapılandırın:

* Azure Portal (için Klasik ve Resource Manager sanal ağlar).
* Ağ yapılandırma dosyası (netcfg - yalnızca klasik sanal ağlar için). Merhaba bkz [bir ağ yapılandırma dosyası kullanarak bir sanal ağ yapılandırma](virtual-networks-using-network-configuration-file.md) makalesi.
* PowerShell (için Klasik ve Resource Manager sanal ağlar).
* Azure CLI (için Klasik ve Resource Manager sanal ağlar).

### <a name="what-address-ranges-can-i-use-in-my-vnets"></a>Hangi adres aralıklarını my Vnet'lerde kullanabilir miyim?
Herhangi bir IP adresi aralığını tanımlanan [RFC 1918](http://tools.ietf.org/html/rfc1918). Örneğin, 10.0.0.0/16.

### <a name="can-i-have-public-ip-addresses-in-my-vnets"></a>My Vnet'ler genel IP adresleri olabilir mi?
Evet. Ortak IP adresi aralıkları hakkında daha fazla bilgi için bkz: Merhaba [ortak IP adres alanı sanal ağ](virtual-networks-public-ip-within-vnet.md) makale. Ortak IP adreslerinizi hello Internet ' doğrudan erişilebilir olmaz.

### <a name="is-there-a-limit-toohello-number-of-subnets-in-my-vnet"></a>Sanal ağıma alt sınırı toohello sayısı var mı?
Evet. Okuma hello [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) Ayrıntılar için makale. Alt ağ adres alanları birbirine gelemez.

### <a name="are-there-any-restrictions-on-using-ip-addresses-within-these-subnets"></a>Bu alt ağ içindeki IP adresleri kullanma kısıtlamaları var mı?
Evet. Azure bazı IP adreslerini her alt ağ içindeki ayırır. Merhaba ilk ve son IP adresleri hello alt Azure Hizmetleri için kullanılan 3 daha fazla adres birlikte Protokolü uyum için ayrılmıştır.

### <a name="how-small-and-how-large-can-vnets-and-subnets-be"></a>Küçük ve ne kadar büyük nasıl sanal ağlar ve alt ağları olabilir?
destekliyoruz hello en küçük alt ağ/29 ise ve en büyük hello (CIDR alt ağ tanımlarının kullanarak) bir 8 uzunluğudur.

### <a name="can-i-bring-my-vlans-tooazure-using-vnets"></a>Sanal ağlar kullanarak my VLAN tooAzure getirebilir miyim?
Hayır. Sanal ağlar Katman 3 yer paylaşımları ' dir. Azure, Katman-2 semantiği desteklemez.

### <a name="can-i-specify-custom-routing-policies-on-my-vnets-and-subnets"></a>Özel yönlendirme ilkeleri my sanal ağlar ve alt ağları belirtebilir miyim?
Evet. Kullanıcı tanımlı yönlendirme (UDR) kullanabilirsiniz. UDR hakkında daha fazla bilgi için ziyaret [kullanıcı tanımlı yollar ve IP iletimi](virtual-networks-udr-overview.md).

### <a name="do-vnets-support-multicast-or-broadcast"></a>Sanal ağlar, çok noktaya yayın veya çok noktaya yayın destekliyor musunuz?
Hayır. Çok noktaya yayın veya çok noktaya yayın desteklemez.

### <a name="what-protocols-can-i-use-within-vnets"></a>Hangi protokolleri içinde sanal ağlar kullanabilir miyim?
Sanal ağlar içinde TCP, UDP ve TCP/IP'yi ICMP protokoller kullanabilir. Çok noktaya yayın, yayın, IP-kapsüllenmiş IP paketlerinin ve Genel Yönlendirme Kapsüllemesi (GRE) paketleri Vnet'ler engellenir. 

### <a name="can-i-ping-my-default-routers-within-a-vnet"></a>Bir sanal ağ içindeki my varsayılan yönlendiricileri ping?
Hayır.

### <a name="can-i-use-tracert-toodiagnose-connectivity"></a>Tracert toodiagnose bağlantı kullanabilir miyim?
Hayır.

### <a name="can-i-add-subnets-after-hello-vnet-is-created"></a>Merhaba VNet oluşturulduktan sonra alt ağlar ekleyebilir miyim?
Evet. Alt ağlar Hello alt ağ adresi hello VNet içindeki başka bir alt ağının parçası değil sürece herhangi bir zamanda tooVNets eklenebilir.

### <a name="can-i-modify-hello-size-of-my-subnet-after-i-create-it"></a>Alt hello boyutu, onu oluşturduktan sonra değişiklik yapabilirsiniz?
Evet. Ekle, Kaldır, genişletin veya sanal makineleri veya Hizmetleri içinde dağıtılan yoksa bir alt ağ küçültür.

### <a name="can-i-modify-subnets-after-i-created-them"></a>Alt ağlar, bunları oluşturduktan sonra değişiklik yapabilirsiniz?
Evet. Ekleme, kaldırma ve sanal ağ tarafından kullanılan hello CIDR blokları değiştirme.

### <a name="can-i-connect-toohello-internet-if-i-am-running-my-services-in-a-vnet"></a>Toohello bağlanmak sanal ağ içinde Hizmetlerim çalıştırdığım varsa internet?
Evet. Bir sanal ağ içinde dağıtılan tüm hizmetlerin toohello bağlanabilmesi için internet. Azure üzerinde dağıtılan her bir bulut hizmeti tooit atanan genel olarak adreslenebilir bir VIP sahiptir. Bu hizmetleri tooaccept bağlantılarından hello toodefine PaaS rol için giriş uç noktaları ve sanal makineleri tooenable için uç noktaları olacaktır Internet.

### <a name="do-vnets-support-ipv6"></a>Sanal ağlar IPv6 destekliyor musunuz?
Hayır. Şu anda sanal ağlar ile IPv6 kullanamazsınız.

### <a name="can-a-vnet-span-regions"></a>Bir sanal ağ bölgeleri yayılabilir mi?
Hayır. Bir VNet sınırlı tooa tek bölgedir.

### <a name="can-i-connect-a-vnet-tooanother-vnet-in-azure"></a>VNet tooanother azure'da VNet bağlayabilir miyim?
Evet. Bir VNet tooanother VNet kullanarak bağlanabilir:
- Bir Azure VPN ağ geçidi. Okuma hello [VNet-VNet bağlantı yapılandırma](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) Ayrıntılar için makale. 
- VNet eşlemesi. Okuma hello [VNet eşleme genel bakış](virtual-network-peering-overview.md) Ayrıntılar için makale.

## <a name="name-resolution-dns"></a>Ad çözümlemesi (DNS)

### <a name="what-are-my-dns-options-for-vnets"></a>Sanal ağlar için DNS seçeneklerim nelerdir?
Hello kullan hello karar tablosunda [VM'ler ve rol örnekleri için ad çözümlemesi](virtual-networks-name-resolution-for-vms-and-role-instances.md) sayfa tooguide tüm size hello DNS seçenekleri kullanılabilir.

### <a name="can-i-specify-dns-servers-for-a-vnet"></a>DNS sunucuları için bir VNet belirtebilir miyim?
Evet. DNS sunucusu IP adreslerini hello VNet ayarlarını belirtebilirsiniz. Bu hello varsayılan DNS sunucuları hello VNet içindeki tüm VM'ler için uygulanır.

### <a name="how-many-dns-servers-can-i-specify"></a>Kaç tane DNS sunucuları ı belirtebilir miyim?
Başvuru hello [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) Ayrıntılar için makale.

### <a name="can-i-modify-my-dns-servers-after-i-have-created-hello-network"></a>My DNS sunucuları, hello ağ oluşturmuş olduğunuz sonra değişiklik yapabilirsiniz?
Evet. Merhaba DNS sunucusu listesinde ağınız için dilediğiniz zaman değiştirebilirsiniz. DNS sunucusu listesinde değiştirirseniz, toorestart her hello VM'lerin bunları sırayla, VNet içinde toopick hello yeni DNS sunucusu gerekir.

### <a name="what-is-azure-provided-dns-and-does-it-work-with-vnets"></a>Azure tarafından sağlanan DNS nedir ve sanal ağlar ile çalışır mı?
Azure tarafından sağlanan DNS, Microsoft tarafından sunulan çok kiracılı bir DNS hizmetidir. Azure VM'ler ve bulut hizmet rolü örneklerinin tümünde bu hizmetinde kaydeder. Bu hizmet ad çözümlemesi VM'ler ve rol örnekleri aynı bulut hizmetine ve VM'ler ve rol örnekleri için FQDN DEĞERİNE göre hello aynı hello içinde yer alan için ana bilgisayar adı tarafından sağlar VNet. Okuma hello [VM'ler ve rol örnekleri için ad çözümlemesi](virtual-networks-name-resolution-for-vms-and-role-instances.md) makale toolearn DNS hakkında daha fazla bilgi.

> [!NOTE]
> Bir sınırlama vardır bu zaman toohello konumundaki ilk 100 bulut Hizmetleri Azure tarafından sağlanan DNS kullanarak çapraz Kiracı adı çözümlemesi için bir VNet içinde. Kendi DNS sunucusu kullanıyorsanız, bu kısıtlama geçerli değildir.
> 
> 

### <a name="can-i-override-my-dns-settings-on-a-per-vm--service-basis"></a>Miyim bir VM başına my DNS ayarlarını geçersiz kılmak / temel service?
Evet. DNS sunucularının bir başına bulut hizmeti temel toooverride hello varsayılan ağ ayarları ayarlayabilirsiniz. Ancak, ağ çapında DNS mümkün olduğunca kullanmanızı öneririz.

### <a name="can-i-bring-my-own-dns-suffix"></a>Kendi DNS soneki getirebilir miyim?
Hayır. Özel bir DNS soneki, sanal ağlar için belirtilemez.

## <a name="connecting-virtual-machines"></a>Sanal makineler bağlanma

### <a name="can-i-deploy-vms-tooa-vnet"></a>Sanal makineleri tooa VNet dağıtabilir miyim?
Evet. VM hello Resource Manager dağıtım modeli aracılığıyla dağıtılan tüm ağ arabirimleri (NIC) bağlı tooa bağlı tooa VNet olması gerekir. Merhaba Klasik dağıtım modeli aracılığıyla dağıtılan VM'ler isteğe bağlı olarak bağlı tooa VNet olabilir.

### <a name="what-are-hello-different-types-of-ip-addresses-i-can-assign-toovms"></a>Merhaba farklı türleri nelerdir IP adreslerini ı tooVMs atayabilirsiniz?
* **Özel:** tooeach her VM dahilinde NIC atanmış. Başlangıç adresi hello statik veya dinamik yöntemlerden birini kullanarak atanır. Özel IP adresleri'ağınızı hello alt ayarlarında belirtilen hello aralığından atanır. Merhaba Klasik dağıtım modeli aracılığıyla dağıtılan kaynakları, özel IP adresleri atanır, bağlı olmasanız bile tooa VNet. Merhaba kaynak silinene kadar tooa kaynak hello dinamik yöntemi kalan atanan özel bir IP adresi atanmış (VM'ler veya Bulut hizmeti dağıtım yuvaları). Bir VM durduruldu (serbest bırakıldığında) durumu Hello edilmiş sonra yeniden başlatıldığında hello dinamik yöntemiyle atanan özel bir IP adresi değişebilir. Merhaba kaynak silinene kadar hello statik yöntemi atanmış kalır tooa kaynakla atanmış bir özel IP adresi. Tooensure gerekiyorsa hello kaynak silinene kadar bu hello özel IP adresi bir kaynak için hiç değiştirir, hello statik yöntemi ile özel bir IP adresi atayın.
* **Genel:** isteğe bağlı olarak atanan tooNICs hello Azure Resource Manager dağıtım modeli aracılığıyla dağıtılan tooVMs bağlı. Başlangıç adresi hello statik veya dinamik ayırma yöntemiyle atanabilir. Atanmış bir bulut hizmetinde Hello Klasik dağıtım modeli aracılığıyla dağıtılan tüm sanal makineleri ve bulut Hizmetleri rol örnekleri mevcut bir *dinamik*, genel sanal IP (VIP) adresi. Ortak bir *statik* IP adresi olarak adlandırılan bir [ayrılmış IP adresi](virtual-networks-reserved-public-ip.md), isteğe bağlı bir VIP atanabilir. Sanal makineleri veya Bulut Hizmetleri rol örnekleri hello Klasik dağıtım modeli aracılığıyla dağıtılan ortak IP adresleri tooindividual atayabilirsiniz. Bu adresler adlı [örnek düzeyinde ortak IP (ILPIP](virtual-networks-instance-level-public-ip.md) adresleri ve dinamik olarak atanabilir.

### <a name="can-i-reserve-a-private-ip-address-for-a-vm-that-i-will-create-at-a-later-time"></a>Özel bir IP adresi daha sonraki bir zamanda oluşturmak bir VM için ayırabilirsiniz?
Hayır. Özel bir IP adresi rezerve edemezsiniz. Özel bir IP adresi varsa hello DHCP sunucusu tarafından tooa VM'deki veya rol örneğindeki atanır. VM olabilir veya olmayabilir hello atanan hello özel IP adresi toobe istediğiniz. Ancak, önceden oluşturulmuş VM tooany kullanılabilir bir özel IP adresi hello özel IP adresini değiştirebilirsiniz.

### <a name="do-private-ip-addresses-change-for-vms-in-a-vnet"></a>Bir sanal ağ içindeki VM'ler için özel IP adresleri değişiklik yapmak?
Duruma göre değişir. Dinamik özel IP adresleri, bir VM ile kendi durdurulmuş kadar (serbest bırakıldı) kalır veya silinmiş. Özel statik IP adresleri, silinene kadar bir VM'den serbest değil.

### <a name="can-i-manually-assign-ip-addresses-toonics-within-hello-vm-operating-system"></a>IP adreslerini tooNICs hello VM işletim sistemi içinde atamak el ile?
Evet, ancak önerilmez. Başlangıç IP adresi tooa NIC hello Azure VM içinde atanan toochange olsaydı el ile bir sanal makinenin işletim sistemi içinde bir NIC hello IP adresini değiştirme toolosing bağlantı toohello VM olası neden olabilir.

### <a name="what-happens-toomy-ip-addresses-if-i-stop-a-cloud-service-deployment-slot-or-shutdown-a-vm-from-within-hello-operating-system"></a>Bir bulut hizmeti dağıtım yuvası veya kapatma hello işletim sistemi içinde bir VM'den Durdur toomy IP adreslerini ne olur?
Bir şey yok. Merhaba IP adresleri (ortak VIP, ortak ve özel) atanan toohello bulut hizmeti dağıtım yuvası veya VM kalır. Bir VM'yi (serbest bırakıldığında) durursa, dinamik adresleri serbest yalnızca veya silinen, ya bir bulut hizmeti dağıtım yuvası silinir. Tıklatmak hello **durdurmak** bir VM hello Azure portalı içinde (serbest bırakıldı) kendi durumu tooStopped ayarlar için düğmesine tıklayın. Bu durumda, hello VM IP adreslerini kaybedersiniz.

### <a name="can-i-move-vms-from-one-subnet-tooanother-subnet-in-a-vnet-without-re-deploying"></a>I VM'ler bir VNet içindeki bir alt ağ tooanother alt ağdan yeniden dağıtmadan taşıyabilir miyim?
Evet. Hello daha fazla bilgi bulabilirsiniz [nasıl toomove bir VM ya da rol örneği tooa farklı alt](virtual-networks-move-vm-role-to-subnet.md) makalesi.

### <a name="can-i-configure-a-static-mac-address-for-my-vm"></a>VM'im için statik bir MAC adresi yapılandırabilir miyim?
Hayır. Bir MAC adresi statik olarak yapılandırılamaz.

### <a name="will-hello-mac-address-remain-hello-same-for-my-vm-once-it-has-been-created"></a>Merhaba MAC adresi kalacak oluşturulduktan sonra aynı VM'im için hello?
Evet, hello MAC adresi silinene kadar hello Resource Manager ve klasik dağıtım modeli bir VM için aynı dağıtılan hello kalır. Daha önce hello MAC adresi hello VM (serbest bırakıldığında) durduruldu ancak hello VM durumu Serbest hello olduğunda bile hello MAC adresi şimdi korunur yayımlanmıştır.

### <a name="can-i-connect-toohello-internet-from-a-vm-in-a-vnet"></a>Toohello bağlanmak bir VM sanal ağda Internet'ten?
Evet. Bir sanal ağ içinde dağıtılan tüm sanal makineleri ve bulut Hizmetleri rol örnekleri toohello Internet bağlanabilir.

## <a name="azure-services-that-connect-toovnets"></a>TooVNets bağlanmak azure Hizmetleri

### <a name="can-i-use-azure-app-service-web-apps-with-a-vnet"></a>Azure App Service Web Apps bir VNet ile birlikte kullanabilir miyim?
Evet. Bir ana (uygulama hizmeti ortamı) kullanarak VNet içindeki Web uygulamaları dağıtabilirsiniz. Tüm Web uygulamaları güvenli bir şekilde bağlanmak ve ağınız için yapılandırılmış bir noktadan siteye bağlantınız varsa, Azure sanal kaynaklara erişebilir. Daha fazla bilgi için aşağıdaki makaleler hello bakın:

* [Bir uygulama hizmeti ortamı'nda Web uygulamaları oluşturma](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Uygulamanızı Azure sanal ağı ile tümleştirme](../app-service-web/web-sites-integrate-with-vnet.md)
* [VNet tümleştirme ve karma bağlantılar Web uygulamaları ile kullanma](../app-service-web/web-sites-integrate-with-vnet.md#hybrid-connections-and-app-service-environments)

### <a name="can-i-deploy-cloud-services-with-web-and-worker-roles-paas-in-a-vnet"></a>Bulut Hizmetleri web ve çalışan rolleri (PaaS) bir VNet ile dağıtabilirsiniz?
Evet. Sanal ağlar içindeki bulut Hizmetleri rol örnekleri (isteğe bağlı) dağıtabilirsiniz. toodo hello VNet adı ve hello rol/alt eşlemeleri hello ağ yapılandırma bölümünde, hizmet yapılandırması, belirtin. Sayesinde, ikili dosyaları hiçbirini herhangi bir tooupdate gerekmez.

### <a name="can-i-connect-a-virtual-machine-scale-set-vmss-tooa-vnet"></a>Bir sanal makine ölçek kümesi (VMSS) tooa Vnet'e bağlayabilir miyim?
Evet. VMSS tooa VNet bağlanmanız gerekir.

### <a name="can-i-move-my-services-in-and-out-of-vnets"></a>Sanal ağlar ve Hizmetlerim taşıyabilir miyim?
Hayır. Sanal ağlar hizmetlerde taşınamıyor. Toodelete sahip ve hello hizmet toomove yeniden dağıtın, tooanother VNet.

## <a name="security"></a>Güvenlik

### <a name="what-is-hello-security-model-for-vnets"></a>Sanal ağlar için hello güvenlik modeli nedir?
Sanal ağlar birbirlerinden tamamen yalıtılmıştır ve diğer hizmetleri hello Azure altyapı barındırılan. Bir VNet bir güven sınırı ' dir.

### <a name="can-i-restrict-inbound-or-outbound-traffic-flow-toovnet-connected-resources"></a>Gelen veya giden trafik akışı tooVNet bağlı kaynaklar kısıtlayabilir miyiz?
Evet. Uygulayabileceğiniz [ağ güvenlik grupları](virtual-networks-nsg.md) tooindividual alt ağlar tooa VNet veya her ikisi de bir sanal ağ içinde NIC bağlı.

### <a name="can-i-implement-a-firewall-between-vnet-connected-resources"></a>VNet bağlı kaynaklar arasında bir güvenlik duvarı uygulamak?
Evet. Dağıtabilmeniz için bir [güvenlik duvarı ağ sanal gereç](https://azure.microsoft.com/en-us/marketplace/?term=firewall) hello Azure Market üzerinden birkaç satıcılardan.

### <a name="is-there-information-available-about-securing-vnets"></a>Var. bilgi sanal ağlar güvenliğini sağlama hakkında var mı?
Evet. Merhaba bkz [Azure ağ güvenliğine genel bakış](../security/security-network-overview.md) Ayrıntılar için makale.

## <a name="apis-schemas-and-tools"></a>API'leri, şemalar ve araçları

### <a name="can-i-manage-vnets-from-code"></a>Sanal ağlar koddan yönetebilir miyim?
Evet. Hello sanal ağlar için REST API'ler kullanabilirsiniz [Azure Resource Manager](https://msdn.microsoft.com/library/mt163658.aspx) ve [Klasik (Hizmet Yönetimi)](http://go.microsoft.com/fwlink/?LinkId=296833)) dağıtım modeli.

### <a name="is-there-tooling-support-for-vnets"></a>Sanal ağlar için araç desteği vardır?
Evet. Kullanma hakkında daha fazla bilgi edinin:
- Azure portal toodeploy sanal ağlar hello aracılığıyla hello [Azure Resource Manager](virtual-networks-create-vnet-arm-pportal.md) ve [Klasik](virtual-networks-create-vnet-classic-pportal.md) dağıtım modeli.
- Sanal ağlar dağıtılan hello PowerShell toomanage [Resource Manager](/powershell/resourcemanager/azurerm.network/v3.1.0/azurerm.network.md) ve [Klasik](/powershell/module/azure/?view=azuresmps-3.7.0) dağıtım modeli.
- Merhaba [Azure komut satırı arabirimi (CLI)](../virtual-machines/azure-cli-arm-commands.md#azure-network-commands-to-manage-network-resources) toomanage sanal ağlar her iki dağıtım modeli dağıtılabilir.  
