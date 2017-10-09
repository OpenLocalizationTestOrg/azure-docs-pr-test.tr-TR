---
title: "Azure Güvenlik Merkezi'nde VM Aracısı aaaEnable | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi öneri gösterir. ** etkinleştirmek VM Aracısı **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 5b431c25-4241-45b7-9556-cf2a1956f3da
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9bd71e638b020780537da25fd4cf7baf34d3e11a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a>Azure Güvenlik Merkezi'nde VM aracısını etkinleştir
Merhaba VM Aracısı sanal makineleri (VM'ler) sırayla çok yüklenmelidir[veri toplamayı etkinleştirmek](security-center-enable-data-collection.md).  Sanal makineleri gerektiren, toosee VM Aracısı hello ve işlem etkinleştirmenizi öneririz azure Güvenlik Merkezi sağlar, bu vm'lerde VM Aracısı hello.

Merhaba VM Aracısı, Azure Marketi hello dağıtılan VM'ler için varsayılan olarak yüklenir. Merhaba makale [VM aracısı ve uzantılar – Kısım 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) nasıl tooinstall hello üzerinde VM aracısı bilgi sağlar.

> [!NOTE]
> Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar. Bu, adım adım ilerleyen bir kılavuz değildir.
>
>

## <a name="implement-hello-recommendation"></a>Merhaba öneriyi uygulamayı
1. Merhaba, **öneriler dikey**seçin **etkinleştirmek VM Aracısı**.
   ![VM Aracısını etkinleştirin][1]
2. Bu hello dikey pencere açılır **VM Aracısı eksik veya yanıt vermiyor**. Bu dikey penceresinde hello VM Aracısı gerektiren hello sanal makineleri listeler. Merhaba dikey tooinstall hello VM Aracısı'nı Hello yönergeleri izleyin.
   ![VM Aracısı eksik.][2]

## <a name="see-also"></a>Ayrıca bkz.
Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md)--öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) - Önerilerin Azure kaynaklarınızı korumanıza nasıl yardım edeceği hakkında bilgi edinin.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md)--nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md)--öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) --nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md)--hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/)--hello en son Azure güvenlik haberlerini ve bilgilerini alın.

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
