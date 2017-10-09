---
title: "Azure Güvenlik Merkezi'nde Internet'e yönelik uç noktalar aracılığıyla aaaRestrict erişimi | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi öneri gösterir. ** Internet'e yönelik uç nokta ** aracılığıyla erişimi kısıtlayın."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 727d88c9-163b-4ea0-a4ce-3be43686599f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: ee72497088618d4db29b5ae4183f4fe77b498423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a>Azure Güvenlik Merkezi'nde Internet'e yönelik uç noktalar aracılığıyla erişimi kısıtlama
Azure Güvenlik Merkezi, herhangi bir ağ güvenlik grupları (Nsg'ler) varsa, "tüm" kaynak IP adresleri erişime izin verecek bir veya daha fazla gelen kuralları Internet'e yönelik uç noktalar aracılığıyla erişimi kısıtlamak önerir. Erişim çok "herhangi" açma saldırganlar tooaccess kaynaklarınızı sağlayabilir. Güvenlik Merkezi, erişim gerektiren bu gelen kuralları toorestrict erişim toosource IP adreslerini Düzenle önerir.

Bu öneri, "" kaynağı olarak içeren herhangi bir web dışı bağlantı için oluşturulur.

> [!NOTE]
> Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar. Bu, adım adım ilerleyen bir kılavuz değildir.
>
>

## <a name="implement-hello-recommendation"></a>Merhaba öneriyi uygulamayı
1. Merhaba, **öneriler dikey**seçin **Internet'e yönelik uç noktası aracılığıyla erişimi kısıtlamak**.

   ![İnternet'e yönelik uç nokta ile erişimi kısıtlama][1]
2. Bu hello dikey pencere açılır **Internet'e yönelik uç noktası aracılığıyla erişimi kısıtlamak**. Bu dikey potansiyel bir güvenlik sorunu oluşturmak gelen kuralları ile Merhaba sanal makineleri (VM'ler) listeler. Bir VM'yi seçin.

   ![Bir VM seçin][2]
3. Merhaba **NSG** dikey ağ güvenlik grubu bilgileri, ilgili gelen kuralları, görüntüler ve hello ilişkili VM. Seçin **gelen kuralları Düzenle** bir gelen kuralı düzenleme ile tooproceed.

   ![Ağ güvenlik grubu dikey penceresi][3]
4. Merhaba üzerinde **gelen güvenlik kuralları** hello gelen kuralı tooedit dikey seçin. Bu örnekte, şimdi seçin **AllowWeb**.

   ![Gelen güvenlik kuralları][4]

   Not, ayrıca seçebilirsiniz **varsayılan kuralları** toosee hello tüm Nsg'ler tarafından bulunan varsayılan kuralları kümesi. Merhaba varsayılan kurallar silinemez ancak daha düşük bir öncelik atandığı için oluşturduğunuz hello kurallarıyla kılınabilir. Daha fazla bilgi edinmek [varsayılan kuralları](../virtual-network/virtual-networks-nsg.md#default-rules).

   ![Varsayılan kurallar][5]
5. Merhaba üzerinde **AllowWeb** dikey penceresinde, hello şekilde hello gelen kuralı düzenleme hello özelliklerini **kaynak** bir IP adresi veya IP adresleri bloğu. toolearn hello gelen kuralı hello özellikleri hakkında daha fazla bilgi görmek [NSG kuralları](../virtual-network/virtual-networks-nsg.md#nsg-rules).

   ![Gelen kuralını Düzenle][6]

## <a name="see-also"></a>Ayrıca bkz.
Bu makalede, nasıl tooimplement hello Güvenlik Merkezi öneri "erişimi kısıtlama Internet'e yönelik uç noktası aracılığıyla." gösterdi. Nsg'ler ve kurallarını etkinleştirme hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Ağ Güvenlik Grubu (NSG) Nedir?](../virtual-network/virtual-networks-nsg.md)
* [Azure portal kullanarak toomanage Nsg'ler nasıl hello](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md)--öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) - Önerilerin Azure kaynaklarınızı korumanıza nasıl yardım edeceği hakkında bilgi edinin.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md)--nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md)--öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) --nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md)--hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/)--hello en son Azure güvenlik haberlerini ve bilgilerini alın.

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
