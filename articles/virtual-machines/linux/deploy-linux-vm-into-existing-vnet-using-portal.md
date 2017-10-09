---
title: "mevcut ağ Azure portal ile içine aaaDeploy Linux VM'ler | Microsoft Docs"
description: "Bir Linux VM mevcut bir Azure sanal hello portal kullanarak ağa dağıtın."
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
ms.openlocfilehash: 51272b8cdb1dc7f3fe768d2ebbf4ebe0d754cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-portal"></a>Nasıl toodeploy mevcut Azure sanal ağda hello Azure portal ile Linux sanal makine

Bu makale size nasıl gösterir toodeploy mevcut sanal ağda (VNet) sanal makine (VM). Sanal ağlar ve ağ güvenlik grupları gibi Azure varlıklar statik olmalıdır ve nadiren dağıtılan kaynakları uzun ömürlü. Bir VNet dağıtıldıktan sonra herhangi bir olumsuz etkiler toohello altyapı olmadan sabit redeployments tarafından yeniden. Geleneksel olarak VNet hakkında düşünüyorum donanım ağ anahtarı - ihtiyacınız olmayan yepyeni bir donanım her dağıtımı ile geçiş tooconfigure.  

Doğru yapılandırılmış bir VNet ile birlikte toodeploy yeni sunucuları bu sanal ağ içinde tekrar tekrar hello VNet hello ömrü boyunca gereken birkaç varsa, değişikliklerle devam edebilirsiniz.

## <a name="create-hello-resource-group"></a>Merhaba kaynak grubu oluştur

İlk olarak, bir kaynak grubu tooorganize bu kılavuzda oluşturduğunuz her şeyi oluşturun. Azure kaynak grupları hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md)

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-hello-vnet"></a>Merhaba VNet oluşturma

Ardından, bir VNet toolaunch hello içine VM'ler oluşturun. Merhaba VNet ve hello ağ güvenlik grubu sonraki adımda bu alt ağ ile ilişkilendirilmiş bir alt ağ içerir.

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-toohello-subnet"></a>Vnıc toohello alt ağ Ekle

Sanal ağ kartları (VNics) toodifferent VM'ler bağlanabilir gibi önemlidir. Bu yaklaşım Hello VM'ler geçici olarak olabileceği hello Vnıc statik bir kaynak olarak tutar. Bir Vnıc'teki oluşturup hello önceki adımda oluşturduğunuz hello alt ağı ile ilişkilendirin.

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-hello-network-security-group"></a>Merhaba ağ güvenlik grubu oluşturun

Azure ağ güvenlik grupları hello ağ katmanı eşdeğer tooa güvenlik duvarında değildir. Azure ağ güvenlik grupları hakkında daha fazla bilgi için bkz: [bir ağ güvenlik grubu nedir](../../virtual-network/virtual-networks-nsg.md).

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a>Gelen bir SSH izin ver Kuralı Ekle

Merhaba VM hello erişimden gereken gelen bağlantı noktası 22 trafiği toobe veren bir kural, VM oluşturulduğunda hello üzerinde hello ağ tooport 22 geçirilen şekilde Internet.

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-hello-nsg-with-hello-subnet"></a>Merhaba NSG hello alt ağı ile ilişkilendirin

Merhaba VNet ve oluşturulan hello alt ağ ile Merhaba ağ güvenlik grubu hello alt ağı ile ilişkilendirin. Ağ güvenlik grupları, alt ağın tamamını veya bir tek tek Vnıc ile ilişkilendirilebilir. Merhaba alt ağ düzeyindeki trafiği filtreleme hello güvenlik duvarı ile tüm VNics ve hello alt ağ içindeki VM'ler hello hello ağ güvenlik grubu tarafından korunuyor. Merhaba diğer yaklaşım olduğu hello ağ güvenlik grubu olması yalnızca tek bir Vnıc'teki ile ilişkili olan ve tek bir VM koruma.

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Merhaba VM hello VNet içine ve NSG dağıtma

Hello Azure portal kullanarak hello Linux VM dağıtılan toohello Azure kaynak grubu, sanal ağ, alt ağ ve Vnıc mevcut değildir.

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

Merhaba portal toochoose var olan kaynakları kullanarak hello mevcut ağ içinde Azure toodeploy hello VM isteyin. Bir VNet ve alt ağ dağıtıldıktan sonra Azure bölgesi içinde statik veya kalıcı kaynaklar olarak bırakılabilir.  

## <a name="next-steps"></a>Sonraki adımlar

* [Azure Resource Manager şablonu toocreate belirli bir dağıtım kullanın](../windows/cli-deploy-templates.md)
* [Azure CLI'si komutlarını doğrudan kullanarak bir Linux VM'si için kendi özel ortamınızı oluşturun](create-cli-complete.md)
* [Şablonları kullanarak Azure'da bir Linux VM oluşturma](create-ssh-secured-vm-from-template.md)
