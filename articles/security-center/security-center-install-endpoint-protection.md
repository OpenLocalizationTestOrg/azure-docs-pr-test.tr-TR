---
title: "aaaInstall Azure Güvenlik Merkezi'nde Endpoint Protection | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi öneri gösterir. ** yüklemek Endpoint Protection **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: fea891810e042e4d4f6e55094c0cd4de013ba68a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a>Azure Güvenlik Merkezi'nde Endpoint Protection yükle
Azure Güvenlik Merkezi, uç nokta koruma zaten etkin değilse uç nokta koruma Azure sanal makinelerde (VM'ler) yüklemenizi önerir. Bu öneri tooWindows VM'ler yalnızca geçerlidir.

> [!NOTE]
> Bu örnek dağıtım Microsoft Antimalware kullanır. Bkz: [Azure Güvenlik Merkezi'nde iş ortağı tümleştirme](security-center-partner-integration.md#partners-that-integrate-with-security-center) iş ortaklarının listesi için Güvenlik Merkezi ile tümleşiktir.  
>
>

## <a name="implement-hello-recommendation"></a>Merhaba öneriyi uygulamayı

> [!NOTE]
> Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.  Bu belge hakkında adım adım kılavuz değildir.
>
>

1. Merhaba, **önerileri** dikey penceresinde, select **Endpoint Protection Yükle**.
   ![Endpoint Protection yükle seçin][1]
2. Merhaba **Endpoint Protection Yükle** uç nokta koruması olmadan VM'ler listesini görüntüleyen dikey pencere açılır. Merhaba listesi hello üzerinde tooinstall endpoint protection istediğiniz VM'ler seçim **Vm'lerinde yükleme**.
   ![Sanal makineleri tooinstall Endpoint Protection'ı seçin][2]
3. Merhaba **işaretleyin Endpoint Protection** dikey pencere açılır tooallow toouse istediğiniz, tooselect hello uç nokta koruma çözümü. Bu örnekte, şimdi seçin **Microsoft Antimalware**.
   ![Endpoint Protection seçin][3]
4. Merhaba uç nokta koruma çözümü hakkında ek bilgi görüntülenir. **Oluştur**’u seçin.
   ![Kötü amaçlı yazılımdan koruma çözümü oluşturun][4]
5. Merhaba üzerinde hello gerekli yapılandırma ayarlarını girin **eklemek uzantısı** dikey ve ardından **Tamam**. toolearn hello yapılandırma ayarları hakkında daha fazla bilgi görmek [varsayılan ve özel kötü amaçlı yazılımdan koruma yapılandırma](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).

[Microsoft Antimalware](../security/azure-security-antimalware.md) hello etkin VM'ler seçili artık.

## <a name="see-also"></a>Ayrıca bkz.
Bu makalede, nasıl tooimplement hello Güvenlik Merkezi öneri "Endpoint Protection yükle." gösterdi. Azure, Microsoft Antimalware etkinleştirme hakkında daha fazla toolearn belge aşağıdaki hello bakın:

* [Bulut Hizmetleri ve sanal makineleri için Microsoft Antimalware](../security/azure-security-antimalware.md) --öğrenin nasıl toodeploy Microsoft Antimalware.

Güvenlik Merkezi hakkında daha fazla toolearn belgeleri aşağıdaki hello bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) --nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
