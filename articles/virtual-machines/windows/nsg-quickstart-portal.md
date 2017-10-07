---
title: "aaaOpen bağlantı noktalarını tooa VM kullanarak hello Azure portalı | Microsoft Docs"
description: "Bilgi nasıl tooopen bir bağlantı noktası / bir uç nokta tooyour Windows VM oluşturma hello resource manager dağıtım modeline hello Azure Portal kullanarak"
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
ms.openlocfilehash: aba789c65254651899aa688f256fe616c3d0126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-tooa-virtual-machine-with-hello-azure-portal"></a>Tooopen hello Azure portalı ile yeni bir sanal makine tooa nasıl bağlantı noktaları
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a>Hızlı komutlar
Ayrıca [Azure PowerShell kullanarak bu adımları uygulamadan](nsg-quickstart-powershell.md).

İlk olarak, ağ güvenlik grubu oluşturun. Merhaba Portalı'nda bir kaynak grubu seçin, **Ekle**, ardından aramak ve seçmek **ağ güvenlik grubu**:

![Ağ güvenlik grubu Ekle](./media/nsg-quickstart-portal/add-nsg.png)

Ağ güvenlik grubu için bir ad girin, seçin veya bir kaynak grubu oluşturmak ve bir konum seçin. Seçin **oluşturma** bitirdikten sonra:

![Bir ağ güvenlik grubu oluşturun](./media/nsg-quickstart-portal/create-nsg.png)

Yeni bir ağ güvenlik grubu seçin. 'Gelen güvenlik kuralları' seçin ve ardından hello **Ekle** düğmesini toocreate bir kural:

![Bir gelen kuralı Ekle](./media/nsg-quickstart-portal/add-inbound-rule.png)

Bir ortak seçin **hizmet** hello açılan menüsünden gibi *HTTP*. Öğesini de seçebilirsiniz *özel* tooprovide belirli bir bağlantı noktası toouse. İsterseniz, hello öncelik veya adını değiştirin. Merhaba öncelik içinde kuralları uygulanır - hello sırasını hello alt hello sayısal değer etkiler, hello önceki hello kuralı uygulanır. Öğesini de seçebilirsiniz **Gelişmiş** hello bu ekran tooenter üstündeki belirli bir kaynak IP Blok veya bağlantı noktası aralığı, örneğin. Hazır olduğunuzda seçin **Tamam** toocreate hello kural:

![Bir gelen kuralı oluşturun](./media/nsg-quickstart-portal/create-inbound-rule.png)

Ağınızda güvenlik grubunun bir alt ağ veya belirli bir ağ arabiriminde tooassociate, son adımdır. Şimdi hello ağ güvenlik grubunun bir alt ağı ile ilişkilendirin. Seçin **alt ağlar**, ardından **ilişkilendirmek**:

![Ağ güvenlik grubunun bir alt ağ ile ilişkilendirme](./media/nsg-quickstart-portal/associate-subnet.png)

Sanal ağınızı seçin ve ardından hello uygun alt ağ seçin:

![Bir ağ güvenlik grubu sanal ağ ile ilişkilendirme](./media/nsg-quickstart-portal/select-vnet-subnet.png)

Bağlantı noktası 80 üzerinde trafiğe izin verir ve bir alt ağ ile ilişkilendirilmiş bir gelen kuralı oluşturulan bir ağ güvenlik grubu oluşturdunuz. Toothat alt bağlanmak herhangi bir VM bağlantı noktası 80 üzerinde erişilebilir.

## <a name="more-information-on-network-security-groups"></a>Ağ güvenlik grupları hakkında daha fazla bilgi
Burada hızlı komutları Hello tooget yukarı ve trafik boyunca tooyour VM ile çalışmaya izin verir. Ağ güvenlik grupları, birçok harika özellikler ve denetleme tooyour kaynaklara erişmek için ayrıntı düzeyi sağlar. Daha fazla bilgi edinebilirsiniz [bir ağ güvenlik grubu ve ACL oluşturma kuralları burada](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).

Yüksek oranda kullanılabilir web uygulamaları için Azure yük dengeleyici arkasında Vm'leriniz yerleştirmeniz gerekir. Merhaba yük dengeleyici trafik filtreleme sağlar bir ağ güvenlik grubuyla trafiği tooVMs dağıtır. Daha fazla bilgi için bkz: [nasıl tooload Bakiye Linux sanal yüksek oranda kullanılabilir bir uygulama içinde Azure toocreate makineleri](tutorial-load-balancer.md).

## <a name="next-steps"></a>Sonraki adımlar
Bu örnekte, bir basit kural tooallow HTTP trafiği oluşturuldu. Aşağıdaki makaleleri hello ayrıntılı ortamları oluşturma hakkında bilgi bulabilirsiniz:

* [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md)
* [Ağ Güvenlik Grubu (NSG) Nedir?](../../virtual-network/virtual-networks-nsg.md)