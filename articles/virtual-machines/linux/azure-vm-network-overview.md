---
title: "Azure ve Linux VM ağ genel bakış | Microsoft Docs"
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
ms.openlocfilehash: 1ff4a0482d6dc6ec0eceaa89ca4b87ba1e2f89a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-and-linux-vm-network-overview"></a>Azure ve Linux VM ağına genel bakış
## <a name="virtual-networks"></a>Sanal Ağlar
Azure Virtual Network (VNet) buluttaki kendi ağınızın bir gösterimidir. Azure bulutunun aboneliğinize adanmış mantıksal bir yalıtımıdır. Bu ağ içindeki IP adres bloklarını, DNS ayarlarını, güvenlik ilkelerini ve yol tablolarını tam olarak denetleyebilirsiniz. Ayrıca, sanal ağınızı alt ağlara ayırabilir ve Azure Iaas sanal makineleri (VM'ler) ve/veya Bulut hizmetlerini (PaaS rolü örnekleri) başlatın. Ayrıca, sanal ağ mevcut bağlantı seçeneklerinden birini kullanarak şirket ağınıza bağlanabilir. Özetle, IP adres blokları üzerinde tam bir kontrol sahibi olarak ve Azure'ın sunduğu kurumsal ölçek avantajıyla, ağınızı Azure'a genişletebilirsiniz.

* [Sanal ağ genel bakış](../../virtual-network/virtual-networks-overview.md)

Azure CLI kullanarak bir VNet oluşturmak için burada ilerlemesi takibi gidin.

* [Azure CLI kullanarak VNet oluşturma](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

## <a name="network-security-groups"></a>Ağ Güvenlik Grupları
Ağ güvenlik grubu (NSG), bir Virtual Network üzerindeki VM örneklerinize ağ trafiğinin gitmesine izin veren veya reddeden Erişim Denetimi Listesi (ACL) kurallarının bir listesini içerir. NSG'ler alt ağlarla veya bu alt ağların içindeki tekil VM örnekleriyle ilişkili olabilir. Bir NSG bir alt ağ ile ilişkili olduğunda, ACL kuralları bu alt ağdaki tüm VM örnekleri için geçerli olur. Ayrıca, bir NSG doğrudan tekil bir VM ile ilişkilendirildiği zaman bu VM'ye giden trafik daha da kısıtlanabilir.

* [Ağ Güvenlik Grubu (NSG) Nedir?](../../virtual-network/virtual-networks-nsg.md)
* [Azure CLI içinde NSG’ler oluşturma](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

## <a name="user-defined-routes"></a>Kullanıcı Tanımlı Yollar
Azure'da bir sanal ağa (VNet) sanal makineler (VM'ler) eklediğiniz zaman, VM'lerin birbirleri ile ağ üzerinde otomatik olarak iletişim kurabildiklerini fark edersiniz. VM'ler farklı alt ağlarda bulunsa bile bir ağ geçidini belirtmenize gerek yoktur. Aynı şey VM'lerden genel İnternet'e giden iletişimlerde ve hatta Azure'dan kendi veri merkezinize karma bir bağlantı bulunduğunda şirket içi ağınıza giden iletişimlerde de geçerlidir.

* [Kullanıcı Tanımlı Yollar ve IP İletimi nedir?](../../virtual-network/virtual-networks-udr-overview.md)
* [Azure CLI bir UDR oluşturma](../../virtual-network/virtual-network-create-udr-arm-cli.md)

## <a name="associating-a-fqdn-to-your-linux-vm"></a>Linux VM için bir FQDN ilişkilendirme
Resource Manager dağıtım modelini kullanarak Azure portalında bir sanal makine (VM) oluşturduğunuzda, sanal makine için genel bir IP kaynağı otomatik olarak oluşturulur. VM uzaktan erişmek için bu IP adresi kullanın. Portalı varsayılan olarak bir tam etki alanı adını veya FQDN, oluşturmaz karşın, VM oluşturulduktan sonra bir tane ekleyebilirsiniz.

* [Azure portalında tam etki alanı adı oluşturma](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="network-interfaces"></a>Ağ arabirimleri
Ağ arabirimi (NIC), bir Sanal Makine (VM) ile onun yazılım altyapısı arasındaki çift yönlü bağlantıdır. Bu makalede bir ağ arabiriminin ne olduğu ve Azure Resource Manager dağıtım modelinde nasıl kullanıldığı açıklanmıştır.

* [Sanal ağ arabirimleri](../../virtual-network/virtual-network-network-interface.md)

## <a name="virtual-nics-and-dns-labeling"></a>Sanal NIC ve DNS etiketleme
Kalıcı olması gereken bir sunucu varsa, ancak sunucu cattle kabul edilir ve bozuk ve sık dağıtılan sanal ağ adına kalıcı hale getirmek için DNS NIC üzerinde etiketleme kullanmak istersiniz.  Aşağıdaki kılavuz ile bir statik IP kalıcı olarak adlandırılmış bir NIC Kurulum.

* [Azure CLI kullanarak eksiksiz bir Linux ortamı oluşturma](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="virtual-network-gateways"></a>Sanal Ağ Geçitleri
Sanal ağ geçidi, Azure sanal ağları ile şirket içi konumlar arasında ve Azure içindeki sanal ağlar arasında (Sanal Ağdan Sanal Ağa) ağ trafiği göndermek için kullanılır. Bir VPN ağ geçidini yapılandırdığınızda sanal bir ağ geçidi ve sanal ağ geçidi bağlantısı oluşturup yapılandırmanız gerekir.

* [VPN Gateway hakkında](../../vpn-gateway/vpn-gateway-about-vpngateways.md)

## <a name="internal-load-balancing"></a>İç Yük Dengeleme
Azure Load Balancer bir Katman 4 (TCP, UDP) yük dengeleyicidir. Yük dengeleyici, gelen trafiği bulut hizmetlerindeki sağlıklı hizmet örnekleri veya bir yük dengeleyici kümesindeki sanal makineler arasında dağıtarak yüksek kullanılabilirlik sağlar. Ayrıca, Azure Load Balancer bu hizmetleri birden çok bağlantı noktasında, birden çok IP adresinde ya da her ikisinde birden sağlayabilir.

* [Azure CLI kullanarak bir iç yük dengeleyici oluşturma](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)

