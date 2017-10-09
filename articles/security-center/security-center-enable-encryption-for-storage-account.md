---
title: "Azure Güvenlik Merkezi'nde depolama hesabı için aaaEnable şifreleme | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi önerilerini gösterir. ** şifreleme için Azure depolama hesabı ** etkinleştirin."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2016
ms.author: terrylan
ms.openlocfilehash: c5cbafbf3a8be86f213dcf1c0c0ddcc0222b3d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a>Azure Güvenlik Merkezi'nde Azure depolama hesabı için şifrelemeyi etkinleştir
Azure Güvenlik Merkezi, Azure depolama hizmeti şifrelemesi bekleyen veri için etkinleştirmenizi öneririz.

Depolama hizmeti şifreleme (SSE) tooAzure depolama yazıldığında hello verileri şifrelemek ve alma önce hello verilerin şifresini çözmek çalışır.  SSE yalnızca hello Azure Blob hizmeti şu anda kullanılabilir değil ve blok blobları, sayfa bloblarını kullanılabilir ve ekleme blobları.  toolearn daha, fazla [bekleyen veri için depolama hizmeti şifrelemesi](../storage/common/storage-service-encryption.md).


> [!Note]
> Şifreleme etkinleştirdikten sonra yalnızca yeni veri şifrelenir. Varolan BLOB storage hesabınızdaki şifrelenmemiş kalır. tooencrypt varolan BLOB'lar, bkz: Merhaba [depolama hizmeti şifrelemesi SSS](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).
>
>

Depolama hizmeti şifreleme yalnızca Resource Manager depolama hesaplarında desteklenir. Klasik depolama hesapları şu anda desteklenmemektedir. toounderstand hello Klasik ve Resource Manager dağıtım modellerinde bkz [Azure dağıtım modelleri](../azure-classic-rm.md).

> [!NOTE]
> Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.  Bu belge hakkında adım adım kılavuz değildir.
>
>

## <a name="implement-hello-recommendation"></a>Merhaba öneriyi uygulamayı
1. Merhaba, **önerileri** dikey penceresinde, select **etkinleştirmek Azure depolama hesabı için şifreleme**.
   ![Depolama hesabı için şifrelemeyi etkinleştirme][1]
2. Merhaba **etkinleştirmek depolama şifreleme** dikey pencere açılır. Bu dikey burada depolama şifreleme devre dışı hello Azure depolama hesaplarını listeler. Bu örnekte, şimdi seçin **storageacct1**.
   ![Depolama şifrelemeyi etkinleştir][2]
3. Merhaba **şifreleme** dikey **storageacct1** açar. Seçin **etkin**.
   ![Şifreleme dikey penceresi][3]
4. **Kaydet**’i seçin.

Depolama şifrelemesi için şimdi etkinleştirdiğiniz **storageacct1**.


## <a name="see-also"></a>Ayrıca bkz.
Bu belge size nasıl tooimplement hello Güvenlik Merkezi öneri "etkinleştirmek için şifreleme Azure depolama hesabı." gösterdi. Azure depolama hizmeti şifrelemesi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Rest verileri için Azure Storage hizmeti şifreleme](../storage/common/storage-service-encryption.md)

Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) -öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) -nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) -öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) -önerilerin Azure kaynaklarınızı korumanıza nasıl yardımcı öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) -hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) -Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
