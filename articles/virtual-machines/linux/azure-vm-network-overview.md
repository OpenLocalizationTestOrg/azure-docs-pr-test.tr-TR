---
title: "aaaAzure ve Linux VM ağ genel bakış | Microsoft Docs"
description: "Azure ve Linux VM ağ genel bakış."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: b5420e35-0463-4456-9803-6142db150f2e
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: c3de2dc583c62160e10c0e97e96fef49b9eaffbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux-vm-network-overview"></a>Azure ve Linux VM ağına genel bakış
## <a name="virtual-networks"></a>Sanal Ağlar
Bir Azure sanal ağı (VNet), kendi ağ hello bulutta gösterimidir. Merhaba ayrılmış Azure bulut tooyour abonelik mantıksal yalıtımının olur. Başlangıç IP adresi blokları, DNS ayarları, güvenlik ilkeleri ve bu ağ içindeki yol tablolarını tam olarak denetleyebilirsiniz. Ayrıca, sanal ağınızı alt ağlara ayırabilir ve Azure Iaas sanal makineleri (VM'ler) ve/veya Bulut hizmetlerini (PaaS rolü örnekleri) başlatın. Ayrıca, mevcut hello bağlantı seçeneklerinden birini kullanarak hello sanal ağ tooyour şirket ağına bağlanabilir. Esas olarak, Azure sunduğu Kurumsal ölçek hello yararı IP adres blokları üzerinde tam denetim, ağ tooAzure genişletebilirsiniz.

* [Sanal ağ genel bakış](../../virtual-network/virtual-networks-overview.md)

toocreate kullanarak bir VNet Azure CLI aracılığıyla gidin burada toofollow hello ilerlemesi hello.

* [Azure CLI kullanarak bir VNet toocreate hello nasıl](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

## <a name="network-security-groups"></a>Ağ Güvenlik Grupları
Ağ güvenlik grubu (NSG) izin veren veya bir sanal ağ tooyour VM örnekleri ağ trafiği reddeden erişim denetimi listesi (ACL) kurallarının bir listesini içerir. NSG'ler alt ağlarla veya bu alt ağların içindeki tekil VM örnekleriyle ilişkili olabilir. Bir NSG bir alt ağ ile ilişkili olduğunda hello ACL kuralları bu alt ağdaki tooall hello VM örnekleri uygulayın. Buna ek olarak, trafiği tooan tek tek VM kısıtlanabilir başka bir NSG ilişkilendirerek doğrudan toothat VM.

* [Ağ Güvenlik Grubu (NSG) Nedir?](../../virtual-network/virtual-networks-nsg.md)
* [Azure CLI toocreate Nsg'ler nasıl hello](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

## <a name="user-defined-routes"></a>Kullanıcı Tanımlı Yollar
Azure'da sanal makine (VM) tooa sanal ağ (VNet) eklediğinizde, hello VM'ler hello ağ üzerinden birbirleriyle mümkün toocommunicate otomatik olarak olduğunu fark edeceksiniz. Merhaba VM'ler olsa da farklı alt ağlarda bir ağ geçidi toospecify gerekmez. Merhaba aynı hello VM'ler toohello gelen iletişimi için doğru ortak Internet ve Azure tooyour karma bağlantısından sahip olduğunda datacenter varsa bile tooyour şirket içi ağ.

* [Kullanıcı Tanımlı Yollar ve IP İletimi nedir?](../../virtual-network/virtual-networks-udr-overview.md)
* [Bir UDR hello Azure CLI oluşturma](../../virtual-network/virtual-network-create-udr-arm-cli.md)

## <a name="associating-a-fqdn-tooyour-linux-vm"></a>FQDN tooyour Linux VM ilişkilendirme
Merhaba Resource Manager dağıtım modeli, bir ortak IP kullanarak bir sanal makine (VM) hello Azure portal oluşturduğunuzda hello sanal makine için kaynak otomatik olarak oluşturulur. Bu IP adresi tooremotely erişim hello VM kullanın. Merhaba portalı varsayılan olarak bir tam etki alanı adını veya FQDN, oluşturmaz rağmen hello VM oluşturulduktan sonra bir tane ekleyebilirsiniz.

* [Tam etki alanı adı hello Azure portal oluşturma](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="network-interfaces"></a>Ağ arabirimleri
Bir ağ arabirimi (NIC) bir sanal makine (VM) ve yazılım ağ temel hello arasında hello Bağlantısı ' dir. Bu makalede açıklanır hangi bir ağ arabirimi ve hello Azure Resource Manager dağıtım modelinde nasıl kullanılır.

* [Sanal ağ arabirimleri](../../virtual-network/virtual-network-network-interface.md)

## <a name="virtual-nics-and-dns-labeling"></a>Sanal NIC ve DNS etiketleme
Toobe kalıcı gerekir, ancak sunucu cattle kabul edilir ve bozuk bir sunucu varsa ve sık dağıtılan hello VNET üzerinde NIC toopersist hello adına DNS toouse etiketleme isteyeceksiniz.  Gözden geçirme aşağıdaki hello ile bir statik IP kalıcı olarak adlandırılmış bir NIC Kurulum.

* [Hello Azure CLI kullanarak eksiksiz bir Linux ortamı oluşturma](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="virtual-network-gateways"></a>Sanal Ağ Geçitleri
Bir sanal ağ geçidi kullanılan Azure sanal ağlar ve şirket içi konumlara arasında ve aynı zamanda azure'da (VNet-VNet) sanal ağlar arasında ağ trafiğini toosend. Bir VPN ağ geçidini yapılandırdığınızda sanal bir ağ geçidi ve sanal ağ geçidi bağlantısı oluşturup yapılandırmanız gerekir.

* [VPN Gateway hakkında](../../vpn-gateway/vpn-gateway-about-vpngateways.md)

## <a name="internal-load-balancing"></a>İç Yük Dengeleme
Azure Load Balancer bir Katman 4 (TCP, UDP) yük dengeleyicidir. Merhaba yük dengeleyici, gelen trafiği bulut Hizmetleri sağlıklı hizmet örnekleri veya bir yük dengeleyici kümesindeki sanal makineler arasında dağıtarak yüksek kullanılabilirlik sağlar. Ayrıca, Azure Load Balancer bu hizmetleri birden çok bağlantı noktasında, birden çok IP adresinde ya da her ikisinde birden sağlayabilir.

* [Bir iç yük dengeleyici Hello Azure CLI kullanarak oluşturma](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)

