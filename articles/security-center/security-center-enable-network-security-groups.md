---
title: "Ağ güvenlik grupları Azure Güvenlik Merkezi'nde aaaEnable | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi öneri gösterir. ** etkinleştirmek ağ güvenlik grupları **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f53ed853-ffaf-4530-a019-1906ba6f341b
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 2f70fe432aa452f833a5c322d13102ebbd6dbb69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a>Ağ güvenlik grupları Azure Güvenlik Merkezi'nde etkinleştir
Azure Güvenlik Merkezi bir zaten etkin değilse, bir ağ güvenlik grubu (NSG) etkinleştirmenizi önerir. Nsg'ler izin veren veya bir sanal ağ tooyour VM örnekleri ağ trafiği reddeden erişim denetimi listesi (ACL) kurallarının bir listesini içerir. NSG'ler alt ağlarla veya bu alt ağların içindeki tekil VM örnekleriyle ilişkili olabilir. Bir NSG'yi bir alt ağ ile ilişkili olduğunda hello ACL kuralları bu alt ağdaki tooall hello VM örnekleri uygulayın. Buna ek olarak, trafiği tooan tek tek VM kısıtlanabilir başka bir NSG ilişkilendirerek doğrudan toothat VM. toolearn daha fazla [bir ağ güvenlik grubu (NSG) nedir?](../virtual-network/virtual-networks-nsg.md)

Nsg'ler etkin yoksa Güvenlik Merkezi iki önerileri tooyou sunar: alt ağları ve ağ güvenlik grupları sanal makinelerde etkinleştir üzerinde ağ güvenlik grupları etkinleştirin. Hangi düzeyinde, alt ağ veya VM, tooapply Nsg'ler seçin.

> [!NOTE]
> Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.  Bu, adım adım ilerleyen bir kılavuz değildir.
>
>

## <a name="implement-hello-recommendation"></a>Merhaba öneriyi uygulamayı
1. Merhaba, **önerileri** dikey penceresinde, select **etkinleştirmek ağ güvenlik grupları** alt ağlarda veya sanal makinelerde.
   ![Ağ Güvenlik Gruplarını Etkinleştirme][1]
2. Bu hello dikey pencere açılır **eksik ağ güvenlik gruplarını yapılandırma** alt ağlar için veya seçtiğiniz hello öneri bağlı olarak sanal makineler için. Bir alt ağ veya sanal makine tooconfigure bir NSG seçin.

   ![Alt ağı için NSG yapılandırma][2]

   ![VM için NSG yapılandırma][3]
3. Merhaba üzerinde **ağ güvenlik grubunu seçme** dikey penceresinde, varolan bir NSG veya seçin **Yeni Oluştur** toocreate bir NSG.

   ![Ağ güvenlik grubu seç][4]

Bir NSG oluşturursanız, hello adımları [nasıl Azure portal kullanarak toomanage Nsg'ler hello](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate bir NSG ve güvenlik kuralları ayarlayın.

## <a name="see-also"></a>Ayrıca bkz.
Bu makalede nasıl tooimplement hello Güvenlik Merkezi öneri "etkinleştirmek ağ güvenlik grupları" alt ağ veya sanal makineleri için gösterdi. Nsg'ler, etkinleştirme hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Ağ Güvenlik Grubu (NSG) Nedir?](../virtual-network/virtual-networks-nsg.md)
* [Azure portal kullanarak toomanage Nsg'ler nasıl hello](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) --nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --hello en son Azure güvenlik haberlerini ve bilgilerini alın.

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
