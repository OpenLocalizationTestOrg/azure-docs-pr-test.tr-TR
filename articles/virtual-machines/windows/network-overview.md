---
title: "aaaVirtual ağlar ve azure'da Windows sanal makineler | Microsoft Docs"
description: "Azure'da Windows sanal makineler oluşturma temelleri toohello ilgili olarak ağ hakkında bilgi edinin."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5493e9f7-7d45-4e98-be9a-657a53708746
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: e28a4782f9f6c69f6101e45dbb560ccd694a1e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-networks-and-windows-virtual-machines-in-azure"></a>Azure’da sanal ağlar ve Windows sanal makineleri 

Azure sanal makinesi (VM) oluştururken bir [sanal ağ](../../virtual-network/virtual-networks-overview.md) (VNet) oluşturmanız ya da mevcut bir VNet’i kullanmanız gerekir. Ayrıca Vm'lerinizi hello VNet üzerinde erişilen hedeflenen toobe şeklini toodecide gerekir. Çok önemlidir[kaynaklar oluşturmadan önce plan](../../virtual-network/virtual-network-vnet-plan-design-arm.md) ve hello anladığınızdan emin olun [kaynakları ağ sınırları](../../azure-subscription-service-limits.md#networking-limits).

Aşağıdaki şekilde hello VM'ler web sunucusu ve veritabanı sunucusu temsil edilir. VM'ler her kümesi hello VNet tooseparate alt ağların atanır.

![Azure sanal ağı](./media/network-overview/vnetoverview.png)

Bir sanal ağ, bir VM oluşturun veya bir VM oluşturulurken hello VNet oluşturabilirsiniz önce ya da oluşturabilirsiniz. Kendiniz bir VNet oluşturmalısınız veya VM oluşturduğunuz sırada sizin için bir VNet oluşturulur.

Bir VM ile bu kaynakları toosupport iletişimi oluşturun:

- Ağ arabirimleri
- IP adresleri
- Sanal ağ ve alt ağlar

Ayrıca toothose temel kaynakları, aynı zamanda bu isteğe bağlı kaynakları dikkate almanız gerekenler:

- Ağ güvenlik grupları
- Yük dengeleyiciler 

## <a name="network-interfaces"></a>Ağ arabirimleri

A [ağ arabirimi (NIC)](../../virtual-network/virtual-network-network-interface.md) bir VM sanal ağ (VNet) arasındaki hello bağlantısı olduğundan. Bir VM en az bir NIC olmalıdır, ancak birden çok hello hello oluşturduğunuz VM boyutuna bağlı olarak sağlayabilirsiniz. [Azure’da sanal makine boyutları](sizes.md) konusundan her VM boyutunun kaç NIC desteklediğini öğrenebilirsiniz. 

Toocreate birden çok NIC ile VM istiyorsanız, en az iki hello VM oluşturmanız gerekir.  Oluşturulduktan sonra ek NIC'lerin hello VM boyutu tarafından desteklenen toohello numarasını ekleyebilirsiniz, ancak ek NIC tooa yalnızca biri ile oluşturulan VM eklenemiyor, bağımsız olarak kaç NIC hello VM boyutunu destekler. 

Merhaba VM tooan kullanılabilirlik kümesi eklenirse, tüm VM'ler hello kullanılabilirlik kümesi içinde bir veya birden çok NIC olması gerekir. Birden çok NIC olmayan olan VM'ler gerekli toohave hello aynı sayıda NIC, ancak bunlar en az iki sahip olmalıdır.

VM bulunmalıdır her bağlı NIC tooa hello aynı konumu ve abonelik VM hello gibi. Her NIC'nin bağlı tooa hello aynı mevcut VNet olmalıdır Azure konumu ve NIC hello gibi abonelik Bir NIC oluşturulduktan sonra bağlı hello alt değiştirebilirsiniz, ancak hello bağlı VNet değiştiremezsiniz.  Her NIC'nin VM hello VM silinene kadar değişmeyen bir MAC adresi atanır tooa bağlı.

Bu tabloda toocreate bir ağ arabirimi kullanabileceğiniz hello yöntemler listelenmiştir.

| Yöntem | Açıklama |
| ------ | ----------- |
| Azure portalına | Bir VM hello Azure portal oluşturduğunuzda, bir ağ arabirimi (ayrı olarak oluşturduğunuz bir NIC kullanamazsınız) sizin için otomatik olarak oluşturulur. tek bir NIC ile VM Hello portal oluşturur Birden çok NIC ile VM toocreate isterseniz, farklı bir yöntemle oluşturmanız gerekir. |
| [Azure PowerShell](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) | Kullanım [yeni AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) hello ile **- PublicIpAddressId** daha önce oluşturduğunuz hello ortak IP adresinin parametresi tooprovide hello tanımlayıcı. |
| [Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md) | tooprovide hello tanımlayıcı hello ortak IP adresi, önceden oluşturulmuş kullanım [az ağ NIC oluşturma](https://docs.microsoft.com/cli/azure/network/nic#create) hello ile **--ortak IP adresi** parametresi. |
| [Şablon](../../virtual-network/virtual-network-deploy-multinic-arm-template.md) | Bir şablon kullanarak ağ arabirimi dağıtmak için [Genel IP Adresli bir Sanal Ağda Ağ Arabirimi](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet) konusunu bir kılavuz olarak kullanın. |

## <a name="ip-addresses"></a>IP adresleri 

Bu tür atayabilirsiniz [IP adreslerini](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) tooa azure'da NIC:

- **Genel IP adresleri** -toocommunicate gelen ve giden (olmadan ağ adresi çevirisi (NAT)) kullanılan ile Merhaba Internet ve diğer Azure kaynaklarına tooa VNet bağlı değil. Bir ortak IP adresi tooa atama NIC isteğe bağlıdır. Genel IP adreslerinin nominal bir ücreti vardır ve abonelik başına kullanılabilecek en fazla sayı sınırlaması vardır.
- **Özel IP adresleri** - VNet, şirket içi ağınız ve hello Internet (NAT ile) iletişim için kullanılır. En az bir özel IP adresi tooa VM atamanız gerekir. NAT, azure'da hakkında daha fazla toolearn okuma [azure'da giden bağlantılar anlama](../../load-balancer/load-balancer-outbound-connections.md).

Ortak IP adresleri tooVMs veya internet'e yönelik Yük Dengeleyici atayabilirsiniz. Özel IP adresleri tooVMs ve iç yük dengeleyicileri atayabilirsiniz. IP adreslerini tooa bir ağ arabirimi kullanarak VM atayın.

Tooa kaynak - dinamik veya statik bir IP adresi ayrıldığı iki yöntem vardır. oluşturulduğunda bir IP adresi ayrılmamış burada hello varsayılan ayırma yöntemi dinamik. Bunun yerine, bir VM oluşturun veya durmuş bir VM'yi başlattığınızda başlangıç IP adresi ayrılır. Başlangıç IP adresi, durdurmak veya hello VM sildiğinizde yayımlanır. 

VM kalır hello için tooensure başlangıç IP adresi aynı Merhaba, hello ayırma yöntemi açık olarak ayarlanıp toostatic. Bu durumda, anında bir IP adresi atanır. Yalnızca hello VM silme veya kendi ayırma yöntemi toodynamic değiştirdiğinizde yayımlanır.
    
Bu tabloda toocreate bir IP adresi kullanabileceğiniz hello yöntemler listelenmiştir.

| Yöntem | Açıklama |
| ------ | ----------- |
| [Azure portal](../../virtual-network/virtual-network-deploy-static-pip-arm-portal.md) | Varsayılan olarak, dinamik genel IP adresleri ve hello VM durduruldu veya silindiğinde hello ilişkili adresi toothem değişebilir. VM her zaman hello tooguarantee kullanan Merhaba aynı genel IP adresi, bir statik genel IP adresi oluşturun. Varsayılan olarak, bir VM oluştururken, bir dinamik özel IP adresi tooa NIC hello portal atar. Bu toostatic hello VM oluşturulduktan sonra değiştirebilirsiniz.|
| [Azure PowerShell](../../virtual-network/virtual-network-deploy-static-pip-arm-ps.md) | Kullandığınız [yeni AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) hello ile **- AllocationMethod** parametre dinamik veya statik olarak. |
| [Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md) | Kullandığınız [az ağ genel IP oluşturun](https://docs.microsoft.com/cli/azure/network/public-ip#create) hello ile **--ayırma yöntemi** parametre dinamik veya statik olarak. |
| [Şablon](../../virtual-network/virtual-network-deploy-static-pip-arm-template.md) | Bir şablon kullanarak genel IP adresi dağıtmak için [Genel IP Adresli bir Sanal Ağda Ağ Arabirimi](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet) konusunu bir kılavuz olarak kullanın. |

Bir ortak IP adresi oluşturduktan sonra bir VM ile tooa NIC atayarak ilişkilendirebilir

## <a name="virtual-network-and-subnets"></a>Sanal ağ ve alt ağlar

Bir IP adresi aralığı hello VNet içindeki bir alt ağıdır. Bir sanal ağı organizasyon ve güvenlik için birden çok alt ağa bölebilirsiniz. Her NIC'nin bir VM'de bağlı tooone alt bir VNet içinde değil. NIC bağlı toosubnets (aynı veya farklı) bir sanal ağ içindeki ek bir yapılandırma gerektirmeden birbirleriyle iletişim kurabilir.

Bir VNet ayarladığınızda, hello kullanılabilir adres alanları ve alt ağlar da dahil olmak üzere, hello topolojisini belirtin. Merhaba VNet bağlı toobe tooother sanal ağlar veya şirket içi ağlar ise, çakışmadığından adres aralıklarını seçmeniz gerekir. Merhaba IP adresleri özel olan ve hello yalnızca hello routeable olmayan IP adreslerini 10.0.0.0/8, 172.16.0.0/12 veya 192.168.0.0/16 gibi true Internet erişilemiyor. Şimdi, Azure herhangi bir adres aralığı hello VNet, birbirine bağlı sanal ağlar içinde ve şirket içi konumunuz içinde yalnızca erişilebilen hello özel sanal ağ IP adresi alanı bir parçası olarak değerlendirir. 

Başka birinin hello iç ağlar için sorumlu olduğu bir kuruluştaki çalışıyorsanız, adres alanınızı seçmeden önce toothat kişi konuşun. Bir çakışma olduğundan emin olun ve toouse istediğiniz hello boşluk bildirmek deneyin olmayan şekilde toouse hello aynı IP adresi aralığı. 

Varsayılan olarak, bu alt ağın her biri Vm'lerde tooone iletişim kurabilirsiniz alt ağlar arasında hiçbir güvenlik sınırı olduğundan başka bir. Ancak, toocontrol hello trafik akışı tooand alt ağlar gelen ve vm'lerden tooand izin veren ağ güvenlik grupları (Nsg'ler) ayarlayabilirsiniz. 

Bu tabloda toocreate VNet ve alt ağları kullanabileceğiniz hello yöntemler listelenmiştir.   

| Yöntem | Açıklama |
| ------ | ----------- |
| [Azure portal](../../virtual-network/virtual-networks-create-vnet-arm-pportal.md) | Azure VM oluşturduğunuzda, bir VNet oluşturma izin vermek istiyorsanız, hello adı bir hello VNet içeren hello kaynak grubu adı birleşimidir ve **- vnet**. Merhaba adres alanı 10.0.0.0/24, hello gereken alt ağ adı **varsayılan**, ve hello alt ağ adresi aralığı 10.0.0.0/24. |
| [Azure PowerShell](../../virtual-network/virtual-networks-create-vnet-arm-ps.md) | Kullandığınız [yeni AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetworkSubnetConfig) ve [New-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetwork) toocreate bir alt ağ ve sanal ağ bir. De kullanabilirsiniz [Ekle AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) tooadd bir alt ağ tooan mevcut VNet. |
| [Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md) | Hello alt hello VNet hello aynı oluşturulduğunu ve saat. Sağlayan bir **--alt ağ adı** parametresi çok[az ağ vnet oluşturma](https://docs.microsoft.com/cli/azure/network/vnet#create) hello alt ağ adı ile. |
| [Şablon](../../virtual-network/virtual-networks-create-vnet-arm-template-click.md) | Merhaba en kolay yolu toocreate VNet ve alt ağıdır toodownload var olan bir şablonu gibi [iki alt ağ ile sanal ağ](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets)ve gereksinimlerinize göre değiştirin. |

## <a name="network-security-groups"></a>Ağ güvenlik grupları

A [ağ güvenlik grubu (NSG)](../../virtual-network/virtual-networks-nsg.md) izin veren veya ağ trafiğini toosubnets, NIC ya da her ikisini de reddeden erişim denetimi listesi (ACL) kurallarının bir listesini içerir. Nsg'ler alt ağları veya tek tek NIC bağlı tooa alt ağ ile ilişkili olabilir. Bir NSG'yi bir alt ağ ile ilişkili olduğunda hello ACL kuralları bu alt ağdaki tooall hello VM'ler uygulayın. Ayrıca, tek tek NIC, bir NSG ilişkilendirerek kısıtlanabilir tooan trafiği doğrudan tooa NIC

NSG'ler iki kural kümesi içerir: gelen ve giden. bir kural için Hello öncelik her küme içinde benzersiz olmalıdır. Her kuralın protokol, kaynak ve hedef bağlantı noktası aralıkları, adres ön ekleri, trafik yönü, öncelik ve erişim türü özellikleri vardır. 

Tüm NSG'ler bir varsayılan kurallar kümesini içerir. Merhaba varsayılan kurallar silinemez ancak hello en düşük öncelik atandığı için oluşturduğunuz hello kurallarıyla kılınabilir. 

Bir NSG tooa NIC ile ilişkilendirdiğinizde, hello ağ erişim kuralları hello NSG içinde uygulanan yalnızca toothat NIC olan Bir NSG'yi uygulanan tooa ise tek NIC multi-NIC VM bu trafiği toohello diğer NIC'ler etkilemez. Farklı Nsg'leri tooa NIC (veya hello dağıtım modeline bağlı olarak VM) ilişkilendirin ve NIC'nin veya VM'nin bağlı olduğu alt ağ hello. Öncelik trafiği hello yönünü verilir.

Mutlaka çok[planı](../../virtual-network/virtual-networks-nsg.md#planning) VM'ler ve sanal ağ planlarken Nsg'lerinizi.

Bu tabloda toocreate bir ağ güvenlik grubu kullanabileceğiniz hello yöntemler listelenmiştir.

| Yöntem | Açıklama |
| ------ | ----------- |
| [Azure portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md) | Bir VM hello Azure portal oluşturduğunuzda, bir NSG otomatik olarak oluşturulur ve ilişkili toohello NIC hello portal oluşturur. Merhaba NSG Hello adını hello VM hello adını birleşimidir ve **- nsg**. Bu NSG bir gelen kuralı içeren bir önceliği 1000, hizmet kümesi tooRDP, hello Protokolü kümesi tooTCP, bağlantı noktası too3389 ayarlamak ve eylem tooAllow ayarlayın. Tüm diğer gelen trafiği toohello VM tooallow istiyorsanız, ek kurallar toohello NSG eklemeniz gerekir. |
| [Azure PowerShell](../../virtual-network/virtual-networks-create-nsg-arm-ps.md) | Kullanım [yeni AzureRmNetworkSecurityRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityRuleConfig) ve gerekli hello kural bilgileri sağlayın. Kullanım [yeni AzureRmNetworkSecurityGroup](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityGroup) toocreate hello NSG. Kullanım [kümesi AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/Set-AzureRmVirtualNetworkSubnetConfig) hello alt ağı için NSG tooconfigure hello. Kullanım [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) tooadd hello NSG toohello VNet. |
| [Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md) | Kullanım [az ağ nsg oluşturma](https://docs.microsoft.com/cli/azure/network/nsg#create) tooinitially hello NSG oluşturun. Kullanım [az ağ nsg kuralını](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) tooadd toohello NSG kuralları. Kullanım [az ağ sanal ağ alt ağı güncelleştirme](https://docs.microsoft.com/en-us/cli/azure/network/vnet/subnet#update) tooadd hello NSG toohello alt ağ. |
| [Şablon](../../virtual-network/virtual-networks-create-nsg-arm-template.md) | Bir şablon kullanarak ağ güvenlik grubu dağıtmak için [Ağ Güvenlik Grubu Oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/101-security-group-create) konusunu kılavuz olarak kullanın. |

## <a name="load-balancers"></a>Yük dengeleyiciler

[Azure yük dengeleyici](../../load-balancer/load-balancer-overview.md) tooyour uygulamaları yüksek kullanılabilirlik ve ağ performansı sunar. Bir yük dengeleyici çok yapılandırılabilir[gelen Internet trafiği dengelemek](../../load-balancer/load-balancer-internet-overview.md) tooVMs veya [bir VNet içindeki VM'ler arasındaki trafiği dengelemek](../../load-balancer/load-balancer-internal-overview.md). Bir yük dengeleyici ayrıca şirket içi bilgisayarları ve VM'ler arasındaki trafiği bir şirket içi ağ ya da dış trafiği tooa dengeleyebilirsiniz belirli VM.

Merhaba yük dengeleyici eşlemeleri gelen ve giden trafiği arasında ortak IP adresi ve bağlantı noktası hello yük dengeleyici ve hello özel IP adresi ve bağlantı noktası hello VM hello.

Bir yük dengeleyici oluştururken şu yapılandırma öğelerini de dikkate almanız gerekir:

- **Ön uç IP yapılandırması**: Bir yük dengeleyici, sanal IP’ler (VIP) olarak da bilinen bir veya daha fazla ön uç IP adresi içerebilir. Bu IP adreslerine hello trafiği için giriş işlevini görür.
- **Arka uç adres havuzu** – hello NIC toowhich yük ile ilişkili IP adreslerinin dağıtılır.
- **NAT kuralları** -nasıl gelen trafiği tanımlar hello ön uç IP ve dağıtılmış toohello arka uç IP aracılığıyla akar.
- **Yük Dengeleyici kuralları** -verilen ön uç IP ve bağlantı noktası bileşimi tooa kümesi arka uç IP adresleri ve bağlantı noktası bileşimi eşler. Tek bir yük dengeleyici birden çok dengeleme kuralına sahip olabilir. Her kural, bir ön uç IP’si ile bağlantı noktasının ve arka uç IP’si ile VM’lerle ilişkilendirilmiş bağlantı noktasının birleşiminden oluşur.
- **[Yoklamaları](../../load-balancer/load-balancer-custom-probe-overview.md)**  -izleyiciler hello VM'ler durumunu. Bir araştırma toorespond başarısız olduğunda, hello yük dengeleyici durdurur yeni bağlantıları toohello gönderme sağlıksız VM. Merhaba varolan bağlantılar etkilenmez ve yeni bağlantılar toohealthy VM'ler gönderilir.

Bu tabloda hello yöntemleri toocreate bir internet'e yönelik Yük Dengeleyici kullanabilirsiniz.

| Yöntem | Açıklama |
| ------ | ----------- |
| Azure portalına | Hello Azure portal kullanarak bir internet'e yönelik Yük Dengeleyici şu anda oluşturulamıyor. |
| [Azure PowerShell](../../load-balancer/load-balancer-get-started-internet-arm-ps.md) | tooprovide hello tanımlayıcı hello ortak IP adresi, önceden oluşturulmuş kullanım [yeni AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) hello ile **- Publicıpaddress** parametresi. Kullanım [yeni AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) toocreate hello yapılandırmasını hello arka uç adres havuzu. Kullanım [yeni AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) toocreate gelen NAT kuralları, oluşturduğunuz hello ön uç IP yapılandırması ile ilişkilendirilmiş. Kullanım [yeni AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) toocreate hello araştırmaları, gerekir. Kullanım [yeni AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) toocreate hello yük dengeleyici yapılandırması. Kullanım [yeni AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer) toocreate hello yük dengeleyici.|
| [Azure CLI](../../load-balancer/load-balancer-get-started-internet-arm-cli.md) | Kullanım [az ağ lb oluşturma](https://docs.microsoft.com/cli/azure/network/lb#create) toocreate hello ilk yük dengeleyici yapılandırması. Kullanım [az ağ lb ön uç-IP oluşturmak](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) daha önce oluşturduğunuz tooadd hello genel IP adresi. Kullanım [az ağ lb adres havuzu oluşturma](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) hello arka uç adres havuzu tooadd hello yapılandırması. Kullanım [az ağ lb gelen nat-kuralı oluşturma](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) tooadd NAT kuralları. Kullanım [az ağ lb kuralını](https://docs.microsoft.com/cli/azure/network/lb/rule#create) tooadd hello yük dengeleyici kuralları. Kullanım [az ağ lb araştırma oluşturmak](https://docs.microsoft.com/cli/azure/network/lb/probe#create) tooadd hello araştırmaları. |
| [Şablon](../../load-balancer/load-balancer-get-started-internet-arm-template.md) | Kullanım [bir yük dengeleyici içinde 2 VM ve NAT kurallarını LB hello üzerinde yapılandırma](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-natrules) bir şablonu kullanarak bir yük dengeleyici dağıtmak için bir kılavuz olarak. |
    
Bu tabloda hello yöntemleri toocreate bir iç yük dengeleyici kullanabilirsiniz.

| Yöntem | Açıklama |
| ------ | ----------- |
| Azure portalına | Hello Azure portal kullanarak bir iç yük dengeleyici şu anda oluşturulamıyor. |
| [Azure PowerShell](../../load-balancer/load-balancer-get-started-ilb-arm-ps.md) | özel bir IP adresi hello ağ alt ağındaki, kullanım tooprovide [yeni AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) hello ile **- PrivateIpAddress** parametresi. Kullanım [yeni AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) toocreate hello yapılandırmasını hello arka uç adres havuzu. Kullanım [yeni AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) toocreate gelen NAT kuralları, oluşturduğunuz hello ön uç IP yapılandırması ile ilişkilendirilmiş. Kullanım [yeni AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) toocreate hello araştırmaları, gerekir. Kullanım [yeni AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) toocreate hello yük dengeleyici yapılandırması. Kullanım [yeni AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer) toocreate hello yük dengeleyici.|
| [Azure CLI](../../load-balancer/load-balancer-get-started-ilb-arm-cli.md) | Kullanım hello [az ağ lb oluşturmak](https://docs.microsoft.com/cli/azure/network/lb#create) komut toocreate hello ilk yük dengeleyici yapılandırması. toodefine hello özel IP adresi, kullanım [az ağ lb ön uç-IP oluşturma](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) hello ile **--özel IP adresi** parametresi. Kullanım [az ağ lb adres havuzu oluşturma](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) hello arka uç adres havuzu tooadd hello yapılandırması. Kullanım [az ağ lb gelen nat-kuralı oluşturma](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) tooadd NAT kuralları. Kullanım [az ağ lb kuralını](https://docs.microsoft.com/cli/azure/network/lb/rule#create) tooadd hello yük dengeleyici kuralları. Kullanım [az ağ lb araştırma oluşturmak](https://docs.microsoft.com/cli/azure/network/lb/probe#create) tooadd hello araştırmaları.|
| [Şablon](../../load-balancer/load-balancer-get-started-ilb-arm-template.md) | Kullanım [bir yük dengeleyici içinde 2 VM ve NAT kurallarını LB hello üzerinde yapılandırma](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer) bir şablonu kullanarak bir yük dengeleyici dağıtmak için bir kılavuz olarak. |

## <a name="vms"></a>VM'ler

Sanal makineleri oluşturulabilir hello aynı sanal ağ ve bunlar tooeach diğer bağlanabilir özel IP adresleri. Bunlar hello gerek tooconfigure olmadan farklı alt ağlarda bir ağ geçidi veya genel IP adresleri bile kullanıyorsanız bağlanabilir. tooput bir VNet içine VM'ler, hello VNet oluşturmak ve her bir VM oluştururken, onu toohello VNet ve alt ağ atayın. VM’ler ağ ayarlarını dağıtım veya başlatma sırasında alır.  

VM’ler dağıtıldığı sırada VM’lere bir IP adresi atanır. Bir VNet veya alt ağa birden çok VM dağıtırsanız, bunlara başlatıldıkları sırada IP adresleri atanır. Dinamik bir IP adresi (DIP) bir VM ile ilişkili hello iç IP adresidir. Statik DIP tooa VM ayırabilirsiniz. Statik DIP tahsis yanlışlıkla başka bir VM için bir statik DIP yeniden belirli alt tooavoid kullanmayı düşünmelisiniz.  

Bir VM oluşturun ve daha sonra toomigrate istiyorsanız, bir sanal ağ içinde bir basit yapılandırma değişikliği değil. Merhaba VM hello VNet uygulamasına dağıtmanız gerekir. Hello en kolay yolu tooredeploy toodelete hello VM, ancak hiçbir diskleri tooit bağlı; yeniden oluşturmanız hello VM kullanarak hello hello VNet özgün diskleri 

Bu tabloda toocreate bir VM sanal ağ içinde kullanabileceğiniz hello yöntemler listelenmiştir.

| Yöntem | Açıklama |
| ------ | ----------- |
| [Azure portal](../virtual-machines-windows-hero-tutorial.md) | Daha önce kullandığı hello varsayılan ağ ayarların toocreate tek bir NIC ile VM belirtilen birden çok NIC ile VM toocreate, farklı bir yöntem kullanmanız gerekir. |
| [Azure PowerShell](../virtual-machines-windows-ps-create.md) | Merhaba kullanımını içerir [Ekle AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) tooadd hello toohello VM yapılandırması daha önce oluşturduğunuz NIC. |
| [Şablon](ps-template.md) | Bir şablon kullanarak VM dağıtmak için [Çok basit Windows VM dağıtımı](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) konusunu kılavuz olarak kullanın. |

## <a name="next-steps"></a>Sonraki adımlar

- Bilgi nasıl tooconfigure [kullanıcı tanımlı yollar ve IP iletimini](../../virtual-network/virtual-networks-udr-overview.md). 
- Bilgi nasıl tooconfigure [VNet tooVNet bağlantıları](../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).
- Nasıl çok öğrenin[sorun giderme yolları](../../virtual-network/virtual-network-routes-troubleshoot-portal.md).
