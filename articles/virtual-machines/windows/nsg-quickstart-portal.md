---
title: "Azure Portalı'nı kullanarak bir VM için bağlantı noktalarını açmak | Microsoft Docs"
description: "Bir bağlantı noktasını açmak bir uç noktası, Windows Azure Portalı'nda resource manager dağıtım modelini kullanarak VM oluşturma hakkında bilgi edinin"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: f7cf0319-5ee7-435e-8f94-c484bf5ee6f1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 33bc0be0aeae6d0276fd8999b9ac0a010e3067ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-open-ports-to-a-virtual-machine-with-the-azure-portal"></a>Azure portal ile bir sanal makineye bağlantı noktalarının nasıl
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a>Hızlı komutlar
Ayrıca [Azure PowerShell kullanarak bu adımları uygulamadan](nsg-quickstart-powershell.md).

İlk olarak, ağ güvenlik grubu oluşturun. Portalda bir kaynak grubu seçin, **Ekle**, ardından aramak ve seçmek **ağ güvenlik grubu**:

![Ağ güvenlik grubu Ekle](./media/nsg-quickstart-portal/add-nsg.png)

Ağ güvenlik grubu için bir ad girin, seçin veya bir kaynak grubu oluşturmak ve bir konum seçin. Seçin **oluşturma** bitirdikten sonra:

![Bir ağ güvenlik grubu oluşturun](./media/nsg-quickstart-portal/create-nsg.png)

Yeni bir ağ güvenlik grubu seçin. 'Gelen güvenlik kuralları' seçin ve ardından **Ekle** düğmesine bir kural oluşturmak için:

![Bir gelen kuralı Ekle](./media/nsg-quickstart-portal/add-inbound-rule.png)

Bir ortak seçin **hizmet** açılır menüsünden gibi *HTTP*. Öğesini de seçebilirsiniz *özel* kullanmak için belirli bir bağlantı sağlamak için. İsterseniz, öncelik veya adını değiştirin. Öncelik, kuralları uygulanır - sırasını düşük sayısal değer etkiler, kural önce uygulanır. Öğesini de seçebilirsiniz **Gelişmiş** belirli bir kaynak IP Blok veya bağlantı noktası aralığı, örneğin girmek için bu ekranın üstünde. Hazır olduğunuzda seçin **Tamam** kuralı oluşturmak için:

![Bir gelen kuralı oluşturun](./media/nsg-quickstart-portal/create-inbound-rule.png)

Ağ güvenlik grubunun bir alt ağ veya belirli ağ arabirimi ile ilişkilendirmek için son adımınız olacaktır. Şimdi ağ güvenlik grubu bir alt ağı ile ilişkilendirin. Seçin **alt ağlar**, ardından **ilişkilendirmek**:

![Ağ güvenlik grubunun bir alt ağ ile ilişkilendirme](./media/nsg-quickstart-portal/associate-subnet.png)

Sanal ağınızı seçin ve ardından uygun alt ağ seçin:

![Bir ağ güvenlik grubu sanal ağ ile ilişkilendirme](./media/nsg-quickstart-portal/select-vnet-subnet.png)

Bağlantı noktası 80 üzerinde trafiğe izin verir ve bir alt ağ ile ilişkilendirilmiş bir gelen kuralı oluşturulan bir ağ güvenlik grubu oluşturdunuz. Bu alt ağa bağlanma herhangi bir VM bağlantı noktası 80 üzerinde erişilebilir.

## <a name="more-information-on-network-security-groups"></a>Ağ güvenlik grupları hakkında daha fazla bilgi
Burada hızlı komutlar VM'nize akan trafikle başlamak ve çalıştırmak için olanak sağlar. Ağ güvenlik grupları birçok harika özellikler ve kaynaklarınıza erişimi denetlemek için ayrıntı düzeyi sağlar. Daha fazla bilgi edinebilirsiniz [bir ağ güvenlik grubu ve ACL oluşturma kuralları burada](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).

Yüksek oranda kullanılabilir web uygulamaları için Azure yük dengeleyici arkasında Vm'leriniz yerleştirmeniz gerekir. Yük Dengeleyici trafik filtreleme sağlar bir ağ güvenlik grubu olan VM'ler için trafiği dağıtır. Daha fazla bilgi için bkz: [nasıl yükleneceğini Linux sanal makineleri yüksek oranda kullanılabilir bir uygulama oluşturmak için Azure Bakiye](tutorial-load-balancer.md).

## <a name="next-steps"></a>Sonraki adımlar
Bu örnekte, HTTP trafiğine izin veren basit bir kural oluşturuldu. Aşağıdaki makalelerde ayrıntılı ortamları oluşturma hakkında bilgi bulabilirsiniz:

* [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md)
* [Ağ Güvenlik Grubu (NSG) Nedir?](../../virtual-network/virtual-networks-nsg.md)