---
title: "Azure rol tabanlı erişim denetimi ile yedek yönetme | Microsoft Docs"
description: "Rol tabanlı erişim denetimi toomanage erişim toobackup yönetim işlemlerini kurtarma Hizmetleri kasasına kullanın."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 3bd46b97-4b29-47a5-b5ac-ac174dd36760
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/22/2017
ms.author: trinadhk;markgal
ms.openlocfilehash: 26d034d152f9b77fc6d5b2ffd5ef2648b1797f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-azure-backup-recovery-points"></a>Rol tabanlı erişim denetimi toomanage Azure yedekleme kurtarma noktalarını kullanma
Azure Rol Tabanlı Erişim Denetimi (RBAC), Azure için ayrıntılı erişim yönetimi sağlar. RBAC kullanarak, ekibiniz içinde görevleri kurabilmeleri ve tooperform işlerini gereksinim yalnızca hello miktarını erişim toousers verin.

> [!IMPORTANT]
> Azure yedekleme tarafından sağlanan Azure portalında gerçekleştirilebilir sınırlı tooactions rolleridir veya PowerShell cmdlet'leri kurtarma Hizmetleri kasası. Data Protection Manager kullanıcı Arabirimi veya Azure yedekleme sunucusu kullanıcı Arabirimi olan bu rolleri denetimi dışında Azure Yedekleme aracısı istemcisi kullanıcı arabirimini veya System center gerçekleştirilen eylemler.

Azure Backup 3 yerleşik roller toocontrol yedekleme yönetim işlemlerini sağlar. Daha fazla bilgi almak [Azure RBAC yerleşik rolleri](../active-directory/role-based-access-built-in-roles.md)

* [Yedekleme katkıda bulunan](../active-directory/role-based-access-built-in-roles.md#backup-contributor) -bu rol tüm izinleri toocreate sahiptir ve kurtarma Hizmetleri kasası oluşturma ve erişim tooothers vermiş dışında yedekleme yönetme. Bu rolü her yedekleme Yönetimi işlemi yapmak için Yedekleme yönetimi yönetici olarak düşünün.
* [Yedekleme işletmeni](../active-directory/role-based-access-built-in-roles.md#backup-operator) -bu rol izinleri tooeverything katılımcı dışında yedekleme ve yönetme yedekleme ilkeleri kaldırma sahiptir. Stop yedekleme verileri silmek ile gibi bozucu işlemler gerçekleştirmek veya şirket içi kaynakları kaydını kaldırma dışında bu eşdeğer toocontributor rolüdür.
* [Yedekleme okuyucu](../active-directory/role-based-access-built-in-roles.md#backup-reader) -bu rol izinleri tooview tüm yedekleme yönetim işlemlerinin sahiptir. Bu rol toobe izleme kişi düşünün.

Daha fazla denetim için kendi rolleri toodefine arıyorsanız, bkz. nasıl çok[özel roller yapı](../active-directory/role-based-access-control-custom-roles.md) Azure rbac'de.



## <a name="mapping-backup-built-in-roles-toobackup-management-actions"></a>Eşleme yedekleme yerleşik roller toobackup yönetimi eylemleri
Aşağıdaki tablonun hello hello yedekleme yönetimi eylemleri yakalar ve karşılık gelen minimum RBAC rolü tooperform bu işlem gerekli.

| Yönetim işlemi | Gereken en düşük RBAC rolü |
| --- | --- |
| Kurtarma Hizmetleri kasası oluşturma | Kasasının kaynak grubu üzerinde katılımcı |
| Azure sanal makinelerini yedeklemeyi etkinleştirme | Kasa, sanal makine Katılımcısı vm'lerde yedekleme işletmeni |
| Talep üzerine yedekleme VM | Yedekleme işletmeni |
| VM geri yükleme | Yedekleme işletmeni, VM ve sanal ağlar dağıtılan tooget kalacaklarını kaynak grubu katkıda bulunan |
| Diskler, tek tek dosyaların VM yedekten geri yükleme | Yedekleme işletmeni |
| Azure VM yedeklemesi için yedekleme ilkesi oluşturma | Yedekleme katkıda bulunan |
| Azure VM yedekleme, yedekleme ilkesini değiştirme | Yedekleme katkıda bulunan |
| Azure VM yedekleme, yedekleme ilkesi silme | Yedekleme katkıda bulunan |
| Stop yedekleme (verileri tut ile veya verileri Sil) VM yedekleme hakkında | Yedekleme katkıda bulunan |
| Şirket içi Windows Server/istemci/SCDPM veya Azure yedekleme sunucusu kaydetme | Yedekleme işletmeni |
| Kayıtlı şirket içi Windows Server/istemci/SCDPM veya Azure yedekleme sunucusu silme | Yedekleme katkıda bulunan |

## <a name="next-steps"></a>Sonraki adımlar
* [Rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md): hello Azure portalında RBAC ile çalışmaya başlama.
* Toomanage nasıl erişim ile bilgi edinin:
  * [PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [REST API](../active-directory/role-based-access-control-manage-access-rest.md)
* [Rol tabanlı erişim denetimi sorun giderme](../active-directory/role-based-access-control-troubleshooting.md): sık karşılaşılan sorunları düzeltmek için öneriler alın.
