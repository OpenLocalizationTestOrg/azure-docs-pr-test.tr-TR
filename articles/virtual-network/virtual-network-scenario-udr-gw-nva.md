---
title: "2 katmanlı uygulama aaaHybrid bağlantıyla | Microsoft Docs"
description: "Bilgi nasıl toodeploy sanal gereçler ve UDR toocreate azure'da çok katmanlı uygulama ortamı"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 1f509bec-bdd1-470d-8aa4-3cf2bb7f6134
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/05/2016
ms.author: jdial
ms.openlocfilehash: 53599862289dbf9c6ab3289b0cb8dda6430f20f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-appliance-scenario"></a>Sanal gereç senaryosu
Erişim toohello geri katmanından bir şirket içi veri merkezi verirken hello gerek tooprovide kullanıma sunulan iki katmanlı uygulama toohello Internet büyük Azure müşteri arasında yaygın bir senaryo var. Bu belge hello aşağıdaki gereksinimleri karşılayan iki katmanlı bir ortam kullanıcı tanımlı yolları (UDR), VPN ağ geçidi ve ağ sanal Gereçleri toodeploy kullanan bir senaryo yol gösterecek:

* Web uygulaması erişilebilir olmalıdır yalnızca genel Internet hello.
* Web sunucusu barındırma hello uygulaması mümkün tooaccess bir arka uç uygulama sunucusu olması gerekir.
* Merhaba Internet toohello web uygulaması gelen tüm trafiği bir güvenlik duvarı sanal gereç aracılığıyla gitmeniz gerekir. Bu sanal gereç yalnızca Internet trafiği için kullanılır.
* Toohello uygulama sunucusu giden tüm trafiği bir güvenlik duvarı sanal gereç aracılığıyla gitmeniz gerekir. Bu sanal gereç erişim toohello arka uç sunucusu ve VPN ağ geçidi hello şirket içi ağdan gelen erişim için kullanılır.
* Yöneticiler mümkün toomanage hello güvenlik duvarı sanal gereçler kullanıcıların şirket bilgisayarlarından olmalıdır, üçüncü bir güvenlik duvarı kullanarak sanal gereç özel yönetim amaçlar için kullanılır.

Bu standart DMZ DMZ ve korumalı ağ ile bir senaryodur. Bu senaryo, Azure'da Nsg'ler, güvenlik duvarı sanal gereçler veya her ikisinin birleşimini kullanarak oluşturulabilir. Merhaba tabloda hello Artıları ve eksileri Nsg'ler ve güvenlik duvarı sanal gereçler arasında bazılarını gösterir.

|  | Uzmanları | Simgeler |
| --- | --- | --- |
| NSG |Ücret ödemeden. <br/>Azure RBAC ile tümleşik. <br/>ARM şablonlarını kuralları oluşturulabilir. |Karmaşıklık büyük ortamlarda değişiklik yapacaktır. |
| Güvenlik duvarı |Veri düzlemi üzerinde tam denetim. <br/>Güvenlik Duvarı konsolunu aracılığıyla merkezi yönetimi. |Güvenlik Duvarı gerecini maliyeti. <br/>Azure RBAC ile tümleşik değildir. |

Merhaba çözüm aşağıdaki güvenlik duvarı sanal gereçler tooimplement DMZ ve korumalı ağ senaryo kullanır.

## <a name="considerations"></a>Dikkat edilmesi gerekenler
Bugün, aşağıdaki gibi farklı özellikler kullanılabilir kullanarak Azure'da yukarıda açıklanan hello ortamı dağıtabilirsiniz.

* **Sanal ağ (VNet)**. Bir Azure VNet benzer şekilde tooan şirket ağında görür ve bir veya daha fazla alt ağlar tooprovide trafik yalıtımı ve sorunları ayrılması bölümlenmiş.
* **Sanal gereç**. Birkaç iş ortaklarının sanal gereçler hello yukarıda açıklanan hello üç güvenlik duvarları için kullanılan Azure Marketi de sağlar. 
* **Kullanıcı tanımlı yolları (UDR)**. Yönlendirme tabloları paketlerin bir sanal ağ içindeki Azure ağ toocontrol hello akışı tarafından kullanılan Udr'ler içerebilir. Bu yol tablolarını uygulanan toosubnets olabilir. Azure'da hello yeni özellikler hello özelliği tooapply bir rota tablosu toohello hello özelliği tooforward hello Azure VNet bir karma bağlantı tooa sanal Gereci gelen tüm trafik sağlayarak GatewaySubnet, biri.
* **IP iletimi**. Varsayılan olarak, hello Azure ağ altyapısı iletin paketleri toovirtual ağ arabirimi kartlarıyla (NIC) yalnızca hello paketin hedef IP adresi hello NIC IP adresi eşleşiyorsa. Bu nedenle, bir UDR bir paket sanal gereç verilen tooa gönderilmelidir tanımlıyorsa, hello Azure ağ altyapısı o paketin bırakın. tooensure hello paket tooa hello gerçek hedef hello paket için değil (Bu durumda bir sanal gereç) VM teslim, tooenable IP iletimi hello sanal Gereci için gerekir.
* **Ağ güvenlik grupları (Nsg'ler)**. Aşağıdaki Hello örnek yapmaz Nsg'ler kullanın, ancak bu çözüm toofurther hello giden trafiği filtrelemek bu alt ağ ve NIC'ler içinde uygulanan Nsg'ler toohello alt ağları ve/veya NIC kullanabilirsiniz.

![IPv6 bağlantısı](./media/virtual-network-scenario-udr-gw-nva/figure01.png)

Bu örnekte hello aşağıdakileri içeren bir abonelik vardır:

* Merhaba şemada gösterilmez 2 kaynak grubu. 
  * **ONPREMRG**. Tüm kaynakları gerekli toosimulate bir şirket içi ağ içerir.
  * **AZURERG**. Hello Azure sanal ağı ortamı için gerekli tüm kaynaklar içeriyor. 
* Adlı bir VNet **onpremvnet** bir şirket içi veri merkezi kesimli aşağıda listelenen toomimic kullanılır.
  * **onpremsn1**. Bir Ubuntu toomimic bir şirket içi sunucusu çalıştıran sanal makine (VM) içeren bir alt ağ.
  * **onpremsn2**. Bir yönetici tarafından kullanılan bir şirket içi bilgisayarın ubuntu toomimic çalıştıran bir VM'de içeren alt ağ.
* Adlı bir güvenlik duvarı sanal Gereci yoktur **OPFW** üzerinde **onpremvnet** toomaintain tünel çok kullanılan**azurevnet**.
* Adlı bir VNet **azurevnet** aşağıda listelenen bölümlenmiş.
  * **azsn1**. Dış güvenlik duvarı özel olarak hello dış güvenlik duvarı için kullanılan alt ağ. Tüm Internet trafiğini bu alt ağ ile birlikte gelir. Bu alt ağ yalnızca bağlı NIC toohello dış güvenlik duvarı içerir.
  * **azsn2**. Ön uç alt Internet hello erişilecek bir web sunucusu olarak çalışan bir VM barındırma.
  * **azsn3**. Backend alt ağı hello ön uç web sunucusu tarafından erişilecek bir arka uç uygulama sunucusu çalıştıran bir VM'de barındırma.
  * **azsn4**. Yönetim Alt özel olarak tooprovide yönetim erişim tooall güvenlik duvarı sanal gereçler kullanılır. Bu alt ağ yalnızca hello çözümde kullanılan her güvenlik duvarı sanal Gereci için bir NIC içerir.
  * **GatewaySubnet**. Azure karma bağlantı alt Azure sanal ağlar ve diğer ağlar arasında ExpressRoute ve VPN ağ geçidi tooprovide bağlantısı için gereklidir. 
* Merhaba, 3 güvenlik duvarı sanal gereçler vardır **azurevnet** ağ. 
  * **AZF1**. Kullanıma sunulan dış güvenlik duvarı toohello Azure'da genel IP adresi kaynağı kullanarak genel Internet. Bir şablon hello Market veya doğrudan Gereci satıcınız, bu hükümleri 3-NIC sanal gereç sahip tooensure gerekir.
  * **AZF2**. İç güvenlik duvarı kullanılan arasındaki toocontrol trafiği **azsn2** ve **azsn3**. Bu, 3-NIC sanal gereç de geçerlidir.
  * **AZF3**. Yönetimi Güvenlik Duvarı erişilebilir tooadministrators hello gelen içi veri merkezi ve bağlı tooa yönetimi alt toomanage tüm güvenlik duvarı Gereçleri kullanılır. 2 NIC sanal gereç şablonları hello Market bulunamadı veya doğrudan Gereci satıcınızdan isteyin.

## <a name="user-defined-routing-udr"></a>Kullanıcı tanımlı yönlendirme (UDR)
Azure her alt ağ, alt ağ içinde başlatılan trafiğinin nasıl yönlendirildiğini bağlantılı tooa UDR kullanılan tablo toodefine olabilir. Hiçbir Udr'ler tanımlanmışsa, Azure varsayılan yollar tooallow trafiği tooflow bir alt ağ tooanother gelen kullanır. toobetter Udr'ler anlamak, ziyaret [kullanıcı tanımlı yollar ve IP iletimi nedir](virtual-networks-udr-overview.md#ip-forwarding).

tooensure iletişim hello son gereksinimini yukarıdaki tabanlı hello doğru güvenlik duvarı gereç aracılığıyla yapılır, toocreate hello aşağıdakiler rota tablosu içindeki Udr'ler içeren **azurevnet**.

### <a name="azgwudr"></a>azgwudr
Bu senaryoda, şirket içi tooAzure akan trafik kullanılan toomanage hello güvenlik duvarları çok bağlanarak olacaktır yalnızca hello**AZF3**, ve trafik hello iç güvenlik duvarı aracılığıyla gitmelidir **AZF2**. Bu nedenle, yalnızca bir rota hello gereklidir **GatewaySubnet** aşağıda gösterildiği gibi.

| Hedef | Sonraki atlama | Açıklama |
| --- | --- | --- |
| 10.0.4.0/24 |10.0.3.11 |Şirket içi trafiği tooreach Yönetimi Güvenlik Duvarı **AZF3** |

### <a name="azsn2udr"></a>azsn2udr
| Hedef | Sonraki atlama | Açıklama |
| --- | --- | --- |
| 10.0.3.0/24 |10.0.2.11 |Barındırma Hello uygulama sunucusu üzerinden trafik toohello arka uç alt verir **AZF2** |
| 0.0.0.0/0 |10.0.2.10 |Aracılığıyla yönlendirilen diğer tüm trafik toobe sağlayan **AZF1** |

### <a name="azsn3udr"></a>azsn3udr
| Hedef | Sonraki atlama | Açıklama |
| --- | --- | --- |
| 10.0.2.0/24 |10.0.3.10 |Çok trafiğe izin veren**azsn2** uygulama sunucusu toohello Web gelen tooflow **AZF2** |

Ayrıca toocreate yönlendirme tabloları hello alt ağlar için gereksinim duyduğunuz **onpremvnet** toomimic hello şirket içi veri merkezi.

### <a name="onpremsn1udr"></a>onpremsn1udr
| Hedef | Sonraki atlama | Açıklama |
| --- | --- | --- |
| 192.168.2.0/24 |192.168.1.4 |Çok trafiğe izin veren**onpremsn2** aracılığıyla **OPFW** |

### <a name="onpremsn2udr"></a>onpremsn2udr
| Hedef | Sonraki atlama | Açıklama |
| --- | --- | --- |
| 10.0.3.0/24 |192.168.2.4 |Azure üzerinden trafik yedeklenen toohello alt verir **OPFW** |
| 192.168.1.0/24 |192.168.2.4 |Çok trafiğe izin veren**onpremsn1** aracılığıyla **OPFW** |

## <a name="ip-forwarding"></a>IP İletimi
UDR ve IP iletimi birleşimi tooallow sanal gereçler kullanılan toobe toocontrol trafik akışı bir Azure VNet içinde kullanabileceğiniz özellikleridir.  Bir sanal gereç kullanılan uygulama toohandle ağ trafiğinin bir güvenlik duvarı veya NAT cihazı gibi herhangi bir şekilde çalışan bir VM'den fazla bir şey değildir.

Bu sanal gereç VM olan mümkün tooreceive gelen trafiği olmalıdır tooitself ele değil. tooallow VM tooreceive trafik tooother hedefleri ele, IP iletimi hello VM için etkinleştirmeniz gerekir. Bu ayar, bir ayar değildir hello konuk işletim sistemindeki bir Azure olur. Bazı uygulama toohandle tür, sanal gereç hala gereksinimlerini toorun gelen trafiği hello ve uygun şekilde rota.

IP iletimi, hakkında daha fazla toolearn ziyaret [kullanıcı tanımlı yollar ve IP iletimi nedir](virtual-networks-udr-overview.md#ip-forwarding).

Örnek olarak, bir Azure sanal kurulumunda aşağıdaki hello olduğunu düşünün:

* Alt ağ **onpremsn1** adlı bir VM'den içeren **onpremvm1**.
* Alt ağ **onpremsn2** adlı bir VM'den içeren **onpremvm2**.
* Adlı bir sanal gereç **OPFW** çok bağlı**onpremsn1** ve **onpremsn2**.
* Bir kullanıcı tanımlı yol bağlı çok**onpremsn1** tüm çok trafiği olduğunu belirtir**onpremsn2** çok gönderilmelidir**OPFW**.

AT noktada, varsa **onpremvm1** tooestablish bir bağlantıyla çalışır **onpremvm2**hello UDR kullanılacak ve trafik çok gönderilecek**OPFW** hello sonraki atlama olarak. Gerçek paket hedef hello unutmayın değiştirilmez, hala yazacaktır **onpremvm2** hello hedefi. 

IP iletme için etkinleştirilmiş olmadan **OPFW**hello Azure sanal ağ mantığı Karşılama paketleri bırakma, yalnızca paketleri gönderilen toobe tooa VM hello varsa izin verilir hello hedef hello paket için sanal makinenin IP adresi taşımaktadır.

IP iletimi ile hello Azure sanal ağı mantığı özgün hedef adresini değiştirmeden hello paketleri tooOPFW iletir. **OPFW** Karşılama paketleri işlemek ve onlarla hangi toodo belirlemek gerekir.

Toowork yukarıda Hello senaryo için IP iletimi için hello nıc'lerde etkinleştirmelisiniz **OPFW**, **AZF1**, **AZF2**, ve **AZF3** için kullanılır (Merhaba olanları bağlantılı toohello yönetimi alt dışındaki tüm NIC'ler) yönlendirme. 

## <a name="firewall-rules"></a>Güvenlik Duvarı Kuralları
Yukarıda açıklandığı gibi yalnızca IP iletimi toohello sanal gereçler gönderilen paket sağlar. Aygıtınızın hala bu paketleri ile hangi toodo toodecide gerekiyor. Merhaba senaryoda yukarıdaki gereçleriniz kuralları aşağıdaki toocreate hello gerekir:

### <a name="opfw"></a>OPFW
OPFW kuralları aşağıdaki hello içeren bir şirket içi aygıtını temsil eder:

* **Rota**: tüm trafiği too10.0.0.0/16 (**azurevnet**) tünel üzerinden gönderilen **ONPREMAZURE**.
* **İlke**: arasındaki tüm çift yönlü trafiğine izin **port2** ve **ONPREMAZURE**.

### <a name="azf1"></a>AZF1
AZF1 kuralları aşağıdaki hello içeren bir Azure sanal Gereci temsil eder:

* **İlke**: arasındaki tüm çift yönlü trafiğine izin **port1** ve **port2**.

### <a name="azf2"></a>AZF2
AZF2 kuralları aşağıdaki hello içeren bir Azure sanal Gereci temsil eder:

* **Rota**: tüm trafiği too10.0.0.0/16 (**onpremvnet**) toohello Azure ağ geçidi IP adresi (örneğin, 10.0.0.1) üzerinden gönderilmesi gereken **port1**.
* **İlke**: arasındaki tüm çift yönlü trafiğine izin **port1** ve **port2**.

## <a name="network-security-groups-nsgs"></a>Ağ güvenlik grupları (Nsg'ler)
Bu senaryoda, Nsg'ler kullanılmayan. Ancak, gelen ve giden Nsg'ler tooeach alt ağ toorestrict trafiği uygulayabilirsiniz. Örneğin, NSG kuralları toohello dış FW alt aşağıdaki hello uygulayabilirsiniz.

**Gelen**

* Tüm VM üzerinde hello Internet tooport 80 gelen tüm TCP trafiği hello alt ağda izin verin.
* Diğer tüm trafik, Internet hello reddedin.

**Giden**

* Tüm trafiği toohello Internet reddedin.

## <a name="high-level-steps"></a>Yüksek düzey adımları
toodeploy bu senaryo, hello yüksek düzey adımları aşağıdaki.

1. Oturum açma tooyour Azure aboneliği.
2. Toodeploy VNet toomimic hello şirket içi ağ istiyorsanız parçası olan hello kaynakları sağlamak **ONPREMRG**.
3. Sağlama parçası olan hello kaynakları **AZURERG**.
4. Sağlama hello tünel gelen **onpremvnet** çok**azurevnet**.
5. Tüm kaynaklar sağlandıktan sonra çok oturum**onpremvm2** arasında ping 10.0.3.101 tootest bağlantı ve **onpremsn2** ve **azsn3**.

