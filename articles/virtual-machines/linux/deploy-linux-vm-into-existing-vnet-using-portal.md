---
title: "Mevcut ağ Azure portal ile içine Linux VM'ler dağıtma | Microsoft Docs"
description: "Bir Linux VM mevcut bir Azure sanal Portalı'nı kullanarak ağa dağıtın."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 964c0fc41773b50a9fbe476df47460484c2ada66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-portal"></a>Mevcut Azure sanal ağda Azure portal ile Linux sanal makine dağıtma

Bu makalede, varolan bir sanal ağa (VNet) sanal makine (VM) dağıtma gösterilmektedir. Sanal ağlar ve ağ güvenlik grupları gibi Azure varlıklar statik olmalıdır ve nadiren dağıtılan kaynakları uzun ömürlü. Bir VNet dağıtıldıktan sonra hiçbir olumsuz etkiler altyapısı olmadan sabit redeployments tarafından yeniden. Geleneksel olarak VNet hakkında düşünüyorum donanım ağ anahtarı - değil gerekir yepyeni bir donanım anahtar her dağıtımı ile yapılandırın.  

Doğru yapılandırılmış bir VNet ile birlikte, yeni sunucuları bu Vnet'i tekrar tekrar VNet ömrü boyunca gereken birkaç varsa, değişikliklerle dağıtmak, devam edebilirsiniz.

## <a name="create-the-resource-group"></a>Kaynak grubunu oluşturma

İlk olarak, bu kılavuzda oluşturduğunuz her şeyi düzenlemek için bir kaynak grubu oluşturun. Azure kaynak grupları hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md)

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-the-vnet"></a>Sanal ağ oluşturma

Ardından, sanal makineleri içine başlatmak için bir VNet oluşturun. VNet ve bir sonraki adımda bu alt ağ güvenlik grubuyla ilişkilendirilmiş bir alt ağ içerir.

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-to-the-subnet"></a>Alt ağ için bir Vnıc'teki Ekle

Sanal ağ kartları (VNics) için farklı VM'ler bağlanabilir gibi önemlidir. Bu yaklaşım VM'ler geçici olarak olabileceği Vnıc statik bir kaynak olarak tutar. Bir Vnıc'teki oluşturun ve önceki adımda oluşturduğunuz alt ağ ile ilişkilendirin.

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-the-network-security-group"></a>Ağ güvenlik grubu oluşturun

Azure ağ güvenlik grupları, bir Güvenlik Duvarı'nı ağ katmanında eşdeğerdir. Azure ağ güvenlik grupları hakkında daha fazla bilgi için bkz: [bir ağ güvenlik grubu nedir](../../virtual-network/virtual-networks-nsg.md).

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a>Gelen bir SSH izin ver Kuralı Ekle

Gelen bağlantı noktası 22 trafiği ağ üzerinden bağlantı noktası 22 VM geçirilmesine izin veren bir kural oluşmasını VM Internet erişimi olmalıdır.

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-the-nsg-with-the-subnet"></a>NSG alt ağ ile ilişkilendirme

VNet ve oluşturulan alt ağ ile ağ güvenlik grubu alt ağı ile ilişkilendirin. Ağ güvenlik grupları, alt ağın tamamını veya bir tek tek Vnıc ile ilişkilendirilebilir. Alt ağ düzeyinde trafik filtreleme güvenlik duvarı ile tüm VNics ve alt ağ içindeki VM'ler ağ güvenlik grubu tarafından korunuyor. Diğer ağ güvenlik grubu sadece tek bir Vnıc'teki ve koruma yalnızca bir VM ile ilişkilendirilen bir yaklaşımdır.

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a>VNet ve NSG halinde VM dağıtma

Azure Portalı'nı kullanarak, var olan Azure kaynak grubu, sanal ağ, alt ağ ve Vnıc için Linux VM dağıtılır.

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

Var olan kaynakların seçmek için portalı kullanarak, varolan ağ içindeki VM dağıtmak için Azure isteyin. Bir VNet ve alt ağ dağıtıldıktan sonra Azure bölgesi içinde statik veya kalıcı kaynaklar olarak bırakılabilir.  

## <a name="next-steps"></a>Sonraki adımlar

* [Belirli bir dağıtımı oluşturmak için Azure Resource Manager şablonu kullanma](../windows/cli-deploy-templates.md)
* [Azure CLI'si komutlarını doğrudan kullanarak bir Linux VM'si için kendi özel ortamınızı oluşturun](create-cli-complete.md)
* [Şablonları kullanarak Azure'da bir Linux VM oluşturma](create-ssh-secured-vm-from-template.md)
