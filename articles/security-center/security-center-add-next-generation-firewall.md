---
title: "aaaAdd yeni nesil güvenlik duvarı Azure Güvenlik Merkezi'nde | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi önerilerini gösterir. ** bir sonraki nesil güvenlik duvarı ** ekleyin ve ** yalnızca rota traffice NGFW aracılığıyla **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 48b99015-4db8-4ce8-85e4-b544c0fa203e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9a80f12571ba08eadf3361728c6321388c863235
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a>Azure Güvenlik Merkezi'nde yeni nesil güvenlik duvarı ekleme
Azure Güvenlik Merkezi, yeni nesil Güvenlik Duvarı (NGFW) bir Microsoft iş ortağı tooincrease güvenlik korumaları eklemenizi öneririz. Bu belge, nasıl bir örnek üzerinden anlatan toodo bu.

> [!NOTE]
> Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.  Bu, adım adım ilerleyen bir kılavuz değildir.
>
>

## <a name="implement-hello-recommendation"></a>Merhaba öneriyi uygulamayı
1. Merhaba, **önerileri** dikey penceresinde, select **yeni nesil güvenlik duvarı ekleme**.
   ![Yeni Nesil Güvenlik Duvarı ekleme][1]
2. Merhaba, **yeni nesil güvenlik duvarı ekleme** dikey penceresinde, bir uç nokta seçin.
   ![Bir uç nokta seçin][2]
3. İkinci bir **yeni nesil güvenlik duvarı ekleme** dikey pencere açılır. Toouse varsa varolan bir çözümü seçebilir veya yeni bir tane oluşturabilirsiniz. Bu örnekte, yok varolan çözüm bir NGFW oluşturuyoruz şekilde.
   ![Yeni nesil güvenlik duvarı oluşturma][3]
4. toocreate bir NGFW hello tümleşik ortakları listesinden bir çözümü seçin. Bu örnekte, biz seçin **Check Point**.
   ![Yeni nesil güvenlik duvarı çözümü seçin][4]
5. Merhaba **Check Point** dikey pencere açılır hello iş ortağı çözümü hakkında bilgi sağlar. Seçin **oluşturma** hello bilgi dikey penceresinde.
   ![Güvenlik Duvarı bilgileri dikey penceresi][5]
6. Merhaba **sanal makine oluşturma** dikey pencere açılır. Buraya bir çalıştıran sanal makineyi (VM) ayarlama gerekli toospin hello NGFW bilgiler girebilirsiniz. Merhaba adımları ve gerekli hello NGFW bilgileri sağlayın. Tamam tooapply seçin.
   ![Sanal makine toorun NGFW oluşturma][6]

## <a name="route-traffic-through-ngfw-only"></a>Trafiği yalnızca NGFW aracılığıyla yönlendir
Toohello iade **önerileri** dikey. Güvenlik Merkezi, adlı aracılığıyla bir NGFW eklendikten sonra yeni bir giriş oluşturulan **rota yalnızca trafiği NGFW aracılığıyla**. Bu öneri, yalnızca Güvenlik Merkezi aracılığıyla, NGFW yüklediyseniz oluşturulur. Internet'e yönelik uç noktaları varsa, Güvenlik Merkezi gelen trafiği tooyour, NGFW aracılığıyla VM zorla ağ güvenlik grubu kurallarını yapılandırmak önerir.

1. Merhaba, **öneriler dikey**seçin **rota yalnızca trafiği NGFW aracılığıyla**.
   ![Trafiği yalnızca NGFW aracılığıyla yönlendirme][7]
2. Bu hello dikey pencere açılır **rota yalnızca trafiği NGFW aracılığıyla**, trafiği yönlendirebilir sanal makineleri listeler. Bir VM hello listeden seçin.
   ![Bir VM seçin][8]
3. Hello için dikey penceresinde seçili VM açar, ilgili gelen kuralları görüntüleme. Bir açıklama olası sonraki adımlar hakkında daha fazla bilgi sağlar. Seçin **gelen kuralları Düzenle** bir gelen kuralı düzenleme ile tooproceed. Merhaba beklenir, **kaynak** çok ayarlanmadı**herhangi** hello Internet'e yönelik uç noktalar ile bağlantılı için NGFW hello. toolearn hello gelen kuralı hello özellikleri hakkında daha fazla bilgi görmek [NSG kuralları](../virtual-network/virtual-networks-nsg.md#nsg-rules).
   ![Kuralları toolimit erişimi yapılandırma][9]
   ![düzenleme gelen kuralı][10]

## <a name="see-also"></a>Ayrıca bkz.
Bu belge size nasıl tooimplement hello Güvenlik Merkezi öneri "Ekleme yeni nesil güvenlik duvarı." gösterdi. toolearn NGFWs ve hello denetim noktası iş ortağı çözümü hakkında daha fazla hello aşağıdaki bakın:

* [Yeni nesil güvenlik duvarı](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [Denetim noktası vSEC](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) --nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.

<!--Image references-->
[1]: ./media/security-center-add-next-gen-firewall/add-next-gen-firewall.png
[2]: ./media/security-center-add-next-gen-firewall/select-an-endpoint.png
[3]: ./media/security-center-add-next-gen-firewall/create-new-next-gen-firewall.png
[4]: ./media/security-center-add-next-gen-firewall/select-next-gen-firewall.png
[5]: ./media/security-center-add-next-gen-firewall/firewall-solution-info-blade.png
[6]: ./media/security-center-add-next-gen-firewall/create-virtual-machine.png
[7]: ./media/security-center-add-next-gen-firewall/route-traffic-through-ngfw.png
[8]: ./media/security-center-add-next-gen-firewall/select-vm.png
[9]: ./media/security-center-add-next-gen-firewall/configure-rules-to-limit-access.png
[10]: ./media/security-center-add-next-gen-firewall/edit-inbound-rule.png
