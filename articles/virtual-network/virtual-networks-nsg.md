---
title: "azure'da aaaNetwork güvenlik grupları | Microsoft Docs"
description: "Tooisolate ve denetim trafiğinin nasıl gerçekleştiğini ağ güvenlik gruplarını kullanarak Azure'da hello dağıtılmış Güvenlik Duvarı'nı kullanarak sanal ağlarınıza içinde öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 20e850fc-6456-4b5f-9a3f-a8379b052bc9
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: jdial
ms.openlocfilehash: 3528ce833dab17977327c3c9ae0e78316e5e6a05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="filter-network-traffic-with-network-security-groups"></a>Ağ güvenlik grupları ile ağ trafiğini filtreleme

Bir ağ güvenlik grubu (NSG) izin veren veya reddeden ağ trafiği tooresources tooAzure sanal ağ (VNet) bağlı güvenlik kurallarının bir listesini içerir. Nsg'ler ilişkili toosubnets, tek tek sanal makineleri (Klasik) olabilir veya tek tek ağ arabirimleri (NIC) tooVMs (Resource Manager) bağlı. Bir NSG'yi ilişkili tooa alt olduğunda hello kuralları tooall kaynaklara bağlı toohello alt uygulayın. Trafik daha da bir NSG tooa VM veya NIC ilişkilendirerek kısıtlanabilir

> [!NOTE]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md). Bu makalede, her iki modeli kullanarak yer almaktadır, ancak Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

## <a name="nsg-resource"></a>NSG kaynağı
Nsg'ler aşağıdaki özelliklere hello içerir:

| Özellik | Açıklama | Kısıtlamalar | Dikkat edilmesi gerekenler |
| --- | --- | --- | --- |
| Ad |Merhaba NSG için ad |Merhaba bölge içinde benzersiz olmalıdır.<br/>Harf, sayı, alt çizgi, nokta ve kısa çizgi içerebilir.<br/>Bir harf veya sayı ile başlamalıdır.<br/>Bir harf, sayı veya alt çizgi ile bitmelidir.<br/>80 karakterden uzun olamaz. |Birden fazla Nsg toocreate gerekebileceği kolay tooidentify hello işlevi nsg'lerinizin kolaylaştıran bir adlandırma kuralınızın bulunduğundan emin olun. |
| Bölge |Azure [bölge](https://azure.microsoft.com/regions) burada hello NSG oluşturulur. |Nsg'ler yalnızca ilişkili tooresources hello içinde olması hello NSG aynı bölgede. |kaç adet Nsg'ye hakkında toolearn bölge başına olabilir okuma hello [Azure sınırlar](../azure-subscription-service-limits.md#virtual-networking-limits-classic) makalesi.|
| Kaynak grubu |Merhaba [kaynak grubu](../azure-resource-manager/resource-group-overview.md#resource-groups) hello NSG bulunmaktadır. |Bir NSG bir kaynak grubunda var ancak hello kaynak hello parçası olduğu sürece, herhangi bir kaynak grubunda ilişkili tooresources olabilir hello NSG olduğu Azure bölgesinin. |Kaynak grupları birden çok kaynak birlikte bir dağıtım birimi olarak kullanılan toomanage yok.<br/>Merhaba NSG'yi ilişkili olduğu kaynaklarla gruplandırmayı değerlendirebilirsiniz. |
| Kurallar |Hangi trafiklere izin verildiğini veya reddedildiğini tanımlayan gelen veya giden kuralları. | |Merhaba bkz [NSG kuralları](#Nsg-rules) bu makalenin. |

> [!NOTE]
> Uç nokta tabanlı ACL'ler ve ağ güvenlik grupları desteklenmez aynı VM örneğinde hello. Toouse bir NSG'yi istediğiniz ve bir uç nokta ACL'si zaten kullanıyor, ilk hello uç nokta ACL'sini kaldırın. nasıl tooremove bir ACL okuma toolearn hello [yönetme erişim denetim listeleri (ACL'ler) PowerShell kullanarak uç noktalar için](virtual-networks-acl-powershell.md) makalesi.
> 

### <a name="nsg-rules"></a>NSG kuralları
NSG kuralları aşağıdaki özelliklere hello içerir:

| Özellik | Açıklama | Kısıtlamalar | Dikkat edilmesi gerekenler |
| --- | --- | --- | --- |
| **Ad** |Merhaba kural adı. |Merhaba bölge içinde benzersiz olmalıdır.<br/>Harf, sayı, alt çizgi, nokta ve kısa çizgi içerebilir.<br/>Bir harf veya sayı ile başlamalıdır.<br/>Bir harf, sayı veya alt çizgi ile bitmelidir.<br/>80 karakterden uzun olamaz. |Bir NSG içinde çeşitli kurallara sahip olabilir, bu nedenle tooidentify hello işlevini sağlayan bir adlandırma kuralını uyguladığınızdan emin olun. |
| **Protokol** |Protokol toomatch hello kuralı için. |TCP, UDP veya * |Kullanarak * ICMP (yalnızca Doğu-Batı trafiği) bir protokolünü içeren gibi olarak UDP ve TCP yanı sıra ve hello ihtiyacınız olan kuralların sayısını azaltabilir.<br/>AT aynı Merhaba, kullanarak istediğiniz zaman * kullanmanız önerilir böylece çok geniş bir yaklaşım olabilir * yalnızca gerekli olduğunda. |
| **Kaynak bağlantı noktası aralığı** |Kaynak bağlantı noktası aralığı toomatch hello kuralı için. |Tek bir bağlantı noktası numarasından 1 too65535, bağlantı noktası aralığı (örneğin: 1-65535), veya * (tüm bağlantı noktaları için). |Kaynak bağlantı noktaları kısa ömürlü olabilir. İstemci programınız belirli bir bağlantı noktasını kullanmadığı sürece, çoğu durum için * kullanın.<br/>Olası tooavoid hello gerektiği kadar birden çok kural için toouse bağlantı noktası aralıkları deneyin.<br/>Birden çok bağlantı noktası veya bağlantı noktası aralığı virgülle birleştirilemez. |
| **Hedef bağlantı noktası aralığı** |Hedef bağlantı noktası aralığı toomatch hello kuralı için. |Tek bir bağlantı noktası numarasından 1 too65535, bağlantı noktası aralığı (örneğin: 1-65535), veya \* (için tüm bağlantı noktaları). |Olası tooavoid hello gerektiği kadar birden çok kural için toouse bağlantı noktası aralıkları deneyin.<br/>Birden çok bağlantı noktası veya bağlantı noktası aralığı virgülle birleştirilemez. |
| **Kaynak adres ön eki** |Kaynak adres ön eki veya etiketi toomatch hello kuralı için. |tek IP adresi (örnek: 10.10.10.10), IP alt ağı (örnek: 192.168.1.0/24), [varsayılan etiket](#default-tags) veya * (tüm adresler için). |Aralıklar, varsayılan etiketler kullanmayı düşünün ve * tooreduce hello kural sayısı. |
| **Hedef adres ön eki** |Hedef adres ön eki veya etiketi toomatch hello kuralı için. | tek IP adresi (örnek: 10.10.10.10), IP alt ağı (örnek: 192.168.1.0/24), [varsayılan etiket](#default-tags) veya * (tüm adresler için). |Aralıklar, varsayılan etiketler kullanmayı düşünün ve * tooreduce hello kural sayısı. |
| **Yön** |Merhaba kuralı için trafiği toomatch yönü. |Gelen veya giden. |Gelen veya giden kuralları, yöne bağlı olarak ayrı ayrı işlenir. |
| **Öncelik** |Kuralları hello öncelik sırasına göre denetlenir. Bir kural uygulandığı zaman eşleştirme için başka hiçbir kural test edilmez. | 100 ile 4096 arasında bir sayı. | Hello gelecekte oluşturacağınız yeni kurallar için her kural tooleave alanı için 100 ile öncelikleri lü adımlarla atlayarak kuralları oluşturmayı düşünün. |
| **Erişim** |Merhaba kuralın eşleşmesi durumunda erişim tooapply türü. | İzin ver veya reddet. | Bir paket için bir izin verme kuralı bulunmazsa, hello paketin bırakılacağını göz önünde bulundurun. |

NSG'ler iki kural kümesi içerir: Gelen ve giden. bir kural için Hello öncelik her küme içinde benzersiz olmalıdır. 

![NSG kuralının işlenmesi](./media/virtual-network-nsg-overview/figure3.png) 

Merhaba önceki resimde NSG kuralların nasıl işlendiği gösterilmektedir.

### <a name="default-tags"></a>Varsayılan Etiketler
Varsayılan, sistem tarafından sağlanan tanımlayıcıları tooaddress IP adreslerinin bir kategori etiketleridir. Hello varsayılan etiketleri kullanabilirsiniz **kaynak adres ön eki** ve **hedef adres ön eki** herhangi bir kural özelliklerini. Kullanabileceğiniz üç varsayılan etiket vardır:

* **VirtualNetwork** (Resource Manager) (**vırtual_network** classic için): hello sanal ağ adresi alanını (Azure'da tanımlanan CIDR aralıkları) bu etiketi içeren, tüm bağlı şirket içi adres alanlarını ve bağlı Azure sanal ağlar (yerel ağlar).
* **AzureLoadBalancer** (Resource Manager) (Klasik için **AZURE_LOADBALANCER**): Bu etiket Azure altyapı infrastructure yük dengeleyicisini belirtir. Merhaba etiketi burada Azure'nın sistem durumu araştırmalarının Azure veri merkezi kaynağı tooan çevirir.
* **Internet** (Resource Manager) (**Internet** classic için): Bu etiket hello sanal ağ dışında ve genel Internet ile ulaşılabilen hello IP adresi alanını belirtir. Merhaba aralık içerir hello [Azure ait genel IP alanı](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="default-rules"></a>Varsayılan kurallar
Tüm NSG'ler bir varsayılan kurallar kümesini içerir. Merhaba varsayılan kurallar silinemez ancak hello en düşük öncelik atandığı için oluşturduğunuz hello kurallarıyla kılınabilir. 

Merhaba varsayılan kuralları ve trafik şu şekilde izin vermeyecek izin ver:
- **Sanal ağ:** Kaynağı bir sanal ağ olan ve bir sanal ağda biten trafiğe hem gelen hem de giden yönlerde izin verilir.
- **Internet:** Giden trafiğe izin verilir, ancak gelen trafik engellenir.
- **Yük Dengeleyici:** izin Azure'nın yük dengeleyici tooprobe hello durumunu VM'ler ve rol örnekleri. Yük dengeli bir küme kullanmıyorsanız bu kuralı geçersiz kılabilirsiniz.

**Gelen trafik için varsayılan kurallar**

| Ad | Öncelik | Kaynak IP | Kaynak Bağlantı Noktası | Hedef IP | Hedef Bağlantı Noktası | Protokol | Access |
| --- | --- | --- | --- | --- | --- | --- | --- |
| AllowVNetInBound |65000 | VirtualNetwork | * | VirtualNetwork | * | * | İzin Ver |
| AllowAzureLoadBalancerInBound | 65001 | AzureLoadBalancer | * | * | * | * | İzin Ver |
| DenyAllInBound |65500 | * | * | * | * | * | Reddet |

**Giden trafik için varsayılan kurallar**

| Ad | Öncelik | Kaynak IP | Kaynak Bağlantı Noktası | Hedef IP | Hedef Bağlantı Noktası | Protokol | Access |
| --- | --- | --- | --- | --- | --- | --- | --- |
| AllowVnetOutBound | 65000 | VirtualNetwork | * | VirtualNetwork | * | * | İzin Ver |
| AllowInternetOutBound | 65001 | * | * | Internet | * | * | İzin Ver |
| DenyAllOutBound | 65500 | * | * | * | * | * | Reddet |

## <a name="associating-nsgs"></a>NSG'leri ilişkilendirme
Bir NSG tooVMs, NIC'lerle ve alt ağlar, aşağıdaki gibi kullandığınız hello dağıtım modeline bağlı olarak ilişkilendirebilirsiniz:

* **VM (yalnızca klasik):** güvenlik kuralları uygulanır tooall trafiği hello VM /. 
* **NIC (yalnızca Resource Manager):** güvenlik kuralları uygulanır tooall/hello NIC hello NSG trafiğidir için ilişkili. Multi-NIC VM ile farklı uygulama (veya aynı hello) NSG tooeach NIC ayrı ayrı. 
* **Alt ağ (Resource Manager ve klasik):** güvenlik kuralları uygulanır tooany trafiği/herhangi bir kaynağa bağlı toohello VNet.

Farklı Nsg'leri tooa VM (veya hello dağıtım modeline bağlı olarak NIC) ilişkilendirin ve NIC'nin veya VM'nin bağlı olduğu alt ağ hello. Uygulanan toohello trafiği, sipariş Merhaba, her nsg'deki öncelik tarafından takip güvenlik kuralları:

- **Gelen trafik**

  1. **NSG uygulanır toosubnet:** NSG bir alt ağ bir eşleşen kuralı toodeny trafiği varsa, hello paket bırakılır.

  2. **NSG uygulanan tooNIC** (Resource Manager) veya VM (Klasik): varsa VM\NIC NSG trafiği engellediği bir eşleşen kuralı sahipse, paketleri NSG bir alt ağ trafiğe izin veren bir eşleşen kuralı olsa bile VM\NIC, hello atlanıyor.

- **Giden trafik**

  1. **NSG uygulanan tooNIC** (Resource Manager) veya VM (Klasik): VM\NIC NSG trafiği engellediği eşleşen bir kuralı varsa, paket bırakılır.

  2. **NSG uygulanır toosubnet:** NSG bir alt ağ trafiğini engellediği eşleşen bir kuralı varsa, trafiğe izin veren bir eşleşen kuralı VM\NIC NSG olsa bile, paketler, bırakılır.

> [!NOTE]
> Yalnızca bir tek NSG tooa alt ağı, VM veya NIC ilişkilendirebilirsiniz rağmen; ilişkilendirmek istediğiniz kadar çok kaynak aynı NSG tooas hello.
>

## <a name="implementation"></a>Uygulama
Merhaba Resource Manager veya araçları aşağıdaki hello kullanarak Klasik dağıtım modellerinde Nsg'leri uygulayabilirsiniz:

| Dağıtım aracı | Klasik | Resource Manager |
| --- | --- | --- |
| Azure portalına   | Evet | [Evet](virtual-networks-create-nsg-arm-pportal.md) |
| PowerShell     | [Evet](virtual-networks-create-nsg-classic-ps.md) | [Evet](virtual-networks-create-nsg-arm-ps.md) |
| Azure CLI **V1**   | [Evet](virtual-networks-create-nsg-classic-cli.md) | [Evet](virtual-networks-create-nsg-cli-nodejs.md) |
| Azure CLI **V2**   | Hayır | [Evet](virtual-networks-create-nsg-arm-cli.md) |
| Azure Resource Manager şablonu   | Hayır  | [Evet](virtual-networks-create-nsg-arm-template.md) |

## <a name="planning"></a>Planlama
Nsg'leri uygulamadan önce aşağıdaki soruları tooanswer hello gerekir:

1. Hangi tür kaynaklara gelen toofilter trafiği tooor istiyor musunuz? Ağ arabirimleri (Resource Manager), VM’ler (klasik), Cloud Services, Uygulama Hizmeti Ortamları ve VM Ölçek Kümeleri gibi kaynakları bağlayabilirsiniz. 
2. Toofilter trafiğe çift varolan vnet'lerdeki bağlı toosubnets hello kaynakları misiniz?

Hello Azure ağ güvenliği planlaması hakkında daha fazla bilgi için okuma [bulut Hizmetleri ve ağ güvenliği](../best-practices-network-security.md) makalesi. 

## <a name="design-considerations"></a>Tasarım konusunda dikkat edilmesi gerekenler
Merhaba toohello sorulara hello yanıtlar öğrendikten sonra [planlama](#Planning) bölümünde, Nsg'lerinizi tanımlamadan önce bölümleri aşağıdaki hello gözden geçirin:

### <a name="limits"></a>Sınırlar
Toohello sayısını bir abonelikte olabilir ve NSG başına kural sayısı sınırlamaları vardır. Merhaba okuma hello sınırları hakkında daha fazla toolearn [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) makalesi.

### <a name="vnet-and-subnet-design"></a>Sanal ağ ve alt ağ tasarımı
Nsg'ler uygulanan toosubnets olabileceği için hello sayısını kaynaklarınızı alt ağa göre gruplandırma ve Nsg'ler toosubnets uygulayarak en aza indirebilirsiniz.  Tooapply Nsg'ler toosubnets karar verirseniz, var olan sanal ağlarınızın ve alt ağlarınızın Nsg'ler göz önünde tanımlanmış olduğunu fark edebilirsiniz. NSG tasarımınızı toodefine yeni sanal ağlar ve alt ağları toosupport ihtiyacınız ve yeni kaynaklar tooyour yeni alt dağıtın. Ardından, kaynakları toohello yeni alt ağlar varolan bir geçiş stratejisi toomove tanımlayabilirsiniz. 

### <a name="special-rules"></a>Özel kurallar
Kuralları aşağıdaki hello tarafından izin verilen trafiği engellerseniz altyapınız temel Azure Hizmetleri ile iletişim kuramıyor:

* **Merhaba ana bilgisayar düğümünün sanal IP'si:** temel altyapı hizmetleri gibi DHCP, DNS ve sistem durumu izleme hello sanallaştırılmış ana bilgisayar üzerinden IP adresi 168.63.129.16 sağlanır. Bu genel IP adresi tooMicrosoft aittir ve tüm bölgelerde bu amaç için kullanılan hello yalnızca sanallaştırılmış IP adresidir. Bu IP adresi hello VM barındırma toohello fiziksel IP adresi hello sunucu makinesinin (ana bilgisayar düğümü) eşler. Hello DHCP geçiş, hello DNS özyinelemeli çözümleyici ve hello araştırma kaynağı hello için yük dengeleyici durum araştırması ve hello makine durumu araştırması hello ana bilgisayar düğümü çalışır. İletişim toothis IP adresi saldırının değil.
* **Lisanslama (Anahtar Yönetimi Hizmeti):** VM’lerde çalışan Windows görüntülerinin lisanslanması gerekir. tooensure lisans isteği sorgularını işleyen anahtar yönetimi hizmeti ana bilgisayar sunucuları toohello gönderilir. Merhaba istek bağlantı noktası 1688 üzerinden giden yapılır.

### <a name="icmp-traffic"></a>ICMP trafiği
Merhaba geçerli NSG kuralları yalnızca protokolleri izin *TCP* veya *UDP*. *ICMP* için belirli bir etiket bulunmaz. Ancak, ICMP trafiği sanal ağ içinde herhangi bir bağlantı noktası ve protokol hello VNet içinde gelen trafiği tooand izin veren hello AllowVNetInBound varsayılan kuralı izin verilir.

### <a name="subnets"></a>Alt ağlar
* Merhaba yükünüzün gerektirdiği katmanların sayısını göz önünde bulundurun. Her katman bir NSG uygulanır toohello alt ağ ile bir alt ağ kullanılarak yalıtılabilir. 
* Bir VPN ağ geçidi veya expressroute bağlantı hattı için bir alt ağ tooimplement ihtiyacınız varsa, yapmanız **değil** bir NSG toothat alt uygulayın. Aksi halde sanal ağlar arası veya şirket içi ve dışı karma bağlantılar çalışmayabilir. 
* Tooimplement ağ sanal gereç (NVA) gerekiyorsa, hello NVA tooits kendi alt bağlanmak ve kullanıcı tanımlı yolları (UDR) tooand NVA hello oluşturun. Alt ağ düzeyinde NSG toofilter trafiği ve bu alt ağ dışındaki bir uygulayabilirsiniz. Merhaba okuma Udr'ler hakkında daha fazla toolearn [kullanıcı tanımlı yollar](virtual-networks-udr-overview.md) makalesi.

### <a name="load-balancers"></a>Yük dengeleyiciler
* Merhaba Yük Dengeleme ve ağ adresi çevirisi (NAT) kuralları her iş yüklerinizi tarafından kullanılan her yük dengeleyici için göz önünde bulundurun. NAT, NIC'ler (Resource Manager) veya VM'ler/bulut Hizmetleri rol örnekleri (Klasik) içeren ilişkili tooa arka uç havuzu kurallardır. Merhaba yük dengeleyicilerde uygulanan hello kurallar yoluyla eşlenen yalnızca trafiğe izin her arka uç havuzu için bir NSG oluşturmayı düşünün. Her bir arka uç havuzu için bir NSG oluşturma toohello arka uç havuzu (yerine doğrudan hello yük dengeleyici aracılığıyla), gelen trafiğin de filtrelenmesini olduğunu güvence altına alır.
* Klasik dağıtımlarda, bir yük dengeleyici tooports Vm'lerinizdeki veya rol örnekleri bağlantı noktalarına eşleyen uç noktalar oluşturursunuz. Resource Manager ile genel kullanıma yönelik bireysel yük dengeleyicinizi de oluşturabilirsiniz. gelen trafik için Hello hedef bağlantı hello gerçek bağlantı noktası hello VM veya rol örneğine, olmayan bir yük dengeleyici tarafından kullanıma sunulan hello bağlantı noktasıdır. Merhaba kaynak bağlantı noktası ve adresi VM üzerinde bir bağlantı noktası ve adresi olduğunu hello bağlantı toohello için hello Internet'teki Uzak bilgisayar, değil hello bağlantı noktası ve hello yük dengeleyici tarafından kullanıma sunulan hello.
* Bir iç yük dengeleyici (ILB) gelen Nsg'ler toofilter trafik oluşturduğunuzda, uygulanan hello kaynak bağlantı noktasının ve adres aralığı olan bilgisayar, hello yük dengeleyici kaynaklanan hello. Merhaba hedef bağlantı noktasının ve adres aralığı bilgilerdir hello hedef bilgisayarın, hello yük dengeleyici.

### <a name="other"></a>Diğer
* Uç nokta tabanlı erişim denetimi listeleri (ACL) ve Nsg'ler hello üzerinde desteklenmiyor aynı VM örneği. Toouse bir NSG'yi istediğiniz ve bir uç nokta ACL'si zaten kullanıyor, ilk hello uç nokta ACL'sini kaldırın. Hakkında bilgi için uç nokta ACL, bir tooremove bkz hello [uç nokta ACL'lerini yönetme](virtual-networks-acl-powershell.md) makalesi.
* Kaynak Yöneticisi'nde, bir NIC başına temelinde birden çok NIC tooenable Yönetimi (uzaktan erişim) ile ilişkili NSG tooa NIC VM'ler için kullanabilirsiniz. Benzersiz Nsg'ler tooeach NIC ilişkilendirme NIC'ler arasında trafik türlerini ayrımı sağlar.
* Diğer sanal ağlardan gelen trafik filtreleme, yük Dengeleyiciler, benzer toohello kullanımı, hello uzak bilgisayar, değil hello ağ geçidi hello sanal ağlara bağlanma hello kaynak adres aralığını kullanmanız gerekir.
* Çoğu Azure hizmeti bağlı tooVNets olamaz. Bir Azure kaynağı bağlı tooa VNet değilse, bir NSG toofilter trafiği toohello kaynağı kullanamazsınız.  Merhaba hizmet bağlı tooa VNet olabilir olup olmadığını hello Hizmetleri hello belgelerini okuyun toodetermine kullanın.

## <a name="sample-deployment"></a>Örnek dağıtımı
Bu makalede, hello bilgilerinin tooillustrate Merhaba uygulaması resim aşağıdaki hello gösterilen iki katmanı uygulaması için yaygın bir senaryo göz önünde bulundurun:

![NSG'ler](./media/virtual-network-nsg-overview/figure1.png)

Merhaba diyagramda gösterildiği gibi hello *Web1* ve *Web2* VM'ler olan bağlı toohello *ön uç* alt ağı ve hello *DB1* ve *DB2* VM'ler olan bağlı toohello *arka uç* alt ağ.  Her iki alt ağ hello parçası olan *TestVNet* VNet. Merhaba uygulama bileşenleri her bir Azure VM bağlı tooa VNet içinde çalıştırın. Merhaba senaryonun gereksinimlerine hello vardır:

1. Merhaba WEB ve veritabanı sunucuları arasındaki trafiğin ayrılması.
2. Yükü Dengeleme kuralları iletme trafiğini hello yük dengeleyici tooall web sunucularından bağlantı noktası 80 üzerinde.
3. Merhaba yük dengeleyici hello WEB1 VM üzerinde tooport 3389 numaralı bağlantı noktası 50001 üzerinde gelen dengeleyicisi NAT kuralları iletme trafik yükleyin.
4. Hiçbir erişim toohello hello Internet, 2 ve 3 gereksinimleri dışında ön uç veya arka uç Vm'lerden.
5. Hiçbir giden Internet erişimi hello WEB veya DB sunucularından.
6. Merhaba ön uç alt ağından erişim tooport 3389 herhangi bir web sunucusunun verilir.
7. Merhaba ön uç alt ağından erişim tooport 3389 herhangi bir DB sunucusunun verilir.
8. Merhaba ön uç alt ağından erişim tooport 1433 tüm DB sunucuların verilir.
9. DB sunucularındaki farklı ağ arabirimlerinde yönetim trafiğinin (3389 numaralı bağlantı noktası) ve veritabanı trafiğinin (1433) ayrılması.

1-6 (dışında gereksinimlerini 3 ve 4) tüm yalıtılmış toosubnet alanları gereksinimleridir. Merhaba aşağıdaki Nsg'ler hello önceki gerekli Nsg'ler hello sayısını en aza indirerek gereksinimleri:

### <a name="frontend"></a>FrontEnd
**Gelen kuralları**

| Kural | Access | Öncelik | Kaynak adres aralığı | Kaynak bağlantı noktası | Hedef adres aralığı | Hedef bağlantı noktası | Protokol |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-HTTP-Internet | İzin Ver | 100 | Internet | * | * | 80 | TCP |
| Allow-Inbound-RDP-Internet | İzin Ver | 200 | Internet | * | * | 3389 | TCP |
| Deny-Inbound-All | Reddet | 300 | Internet | * | * | * | TCP |

**Giden kuralları**

| Kural | Access | Öncelik | Kaynak adres aralığı | Kaynak bağlantı noktası | Hedef adres aralığı | Hedef bağlantı noktası | Protokol |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All |Reddet |100 | * | * | Internet | * | * |

### <a name="backend"></a>BackEnd
**Gelen kuralları**

| Kural | Access | Öncelik | Kaynak adres aralığı | Kaynak bağlantı noktası | Hedef adres aralığı | Hedef bağlantı noktası | Protokol |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All | Reddet | 100 | Internet | * | * | * | * |

**Giden kuralları**

| Kural | Access | Öncelik | Kaynak adres aralığı | Kaynak bağlantı noktası | Hedef adres aralığı | Hedef bağlantı noktası | Protokol |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All | Reddet | 100 | * | * | Internet | * | * |

Aşağıdaki Nsg'ler oluşturulur ve sanal makineleri aşağıdaki hello tooNICs ilişkili hello:

### <a name="web1"></a>WEB1
**Gelen kuralları**

| Kural | Access | Öncelik | Kaynak adres aralığı | Kaynak bağlantı noktası | Hedef adres aralığı | Hedef bağlantı noktası | Protokol |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-RDP-Internet | İzin Ver | 100 | Internet | * | * | 3389 | TCP |
| Allow-Inbound-HTTP-Internet | İzin Ver | 200 | Internet | * | * | 80 | TCP |

> [!NOTE]
> Merhaba kaynak adres aralığı hello önceki kuralları için **Internet**, hello yük dengeleyici sanal IP adresini hello değil. Merhaba kaynak bağlantı noktası * 500001. Yük Dengeleyiciler için NAT kuralları olan değil hello NSG güvenlik kuralları ile aynı. NSG güvenlik kuralları her zaman ilgili toohello orijinal kaynağı ve son hedefi trafik **değil** hello yük dengeleyici hello iki arasında. 
> 
> 

### <a name="web2"></a>WEB2
**Gelen kuralları**

| Kural | Access | Öncelik | Kaynak adres aralığı | Kaynak bağlantı noktası | Hedef adres aralığı | Hedef bağlantı noktası | Protokol |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Inbound-RDP-Internet | Reddet | 100 | Internet | * | * | 3389 | TCP |
| Allow-Inbound-HTTP-Internet | İzin Ver | 200 | Internet | * | * | 80 | TCP |

### <a name="db-servers-management-nic"></a>DB sunucuları (Yönetim ağ arabirimi)
**Gelen kuralları**

| Kural | Access | Öncelik | Kaynak adres aralığı | Kaynak bağlantı noktası | Hedef adres aralığı | Hedef bağlantı noktası | Protokol |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-RDP-Front-end | İzin Ver | 100 | 192.168.1.0/24 | * | * | 3389 | TCP |

### <a name="db-servers-database-traffic-nic"></a>DB sunucuları (Veritabanı trafiği ağ arabirimi)
**Gelen kuralları**

| Kural | Access | Öncelik | Kaynak adres aralığı | Kaynak bağlantı noktası | Hedef adres aralığı | Hedef bağlantı noktası | Protokol |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-SQL-Front-end | İzin Ver | 100 | 192.168.1.0/24 | * | * | 1433 | TCP |

Merhaba Nsg'ler bazıları ilişkili tooindividual NIC'ler olduğundan, hello Resource Manager aracılığıyla dağıtılan kaynaklar için kurallardır. Nasıl ilişkilendirildiklerine bağlı olarak, kurallar alt ağ ve ağ arabirimi için birleştirilir. 

## <a name="next-steps"></a>Sonraki adımlar
* [NSG Dağıtma (Resource Manager)](virtual-networks-create-nsg-arm-pportal.md).
* [NSG Dağıtma (klasik)](virtual-networks-create-nsg-classic-ps.md).
* [NSG günlüklerini yönetin](virtual-network-nsg-manage-log.md).
* [NSG’ler ile ilgili sorun giderme] (virtual-network-nsg-troubleshoot-portal.md)
