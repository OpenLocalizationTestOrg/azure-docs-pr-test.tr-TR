---
title: "aaaUsing rol tabanlı erişim denetimi toomanage Azure Site Recovery | Microsoft Docs"
description: "Rol tabanlı erişim tooapply ve kullanım nasıl kontrol bu makalede (RBAC) toomanage Azure Site Recovery dağıtımlarınızı"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: manayar
ms.openlocfilehash: 7b721090351e561b28317ccdcf0ff283e0b146ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-azure-site-recovery-deployments"></a>Rol tabanlı erişim denetimi toomanage Azure Site Recovery dağıtımları kullanın

Azure Rol Tabanlı Erişim Denetimi (RBAC), Azure için ayrıntılı erişim yönetimi sağlar. RBAC kullanarak, ekibiniz içinde sorumlulukları kurabilmeleri ve yalnızca belirli erişim izinleri toousers gerekli tooperform belirli işler olarak verin.

Azure Site Recovery 3 yerleşik roller toocontrol Site Recovery yönetim işlemlerini sağlar. Daha fazla bilgi almak [Azure RBAC yerleşik rolleri](../active-directory/role-based-access-built-in-roles.md)

* [Site kurtarma katkıda bulunan](../active-directory/role-based-access-built-in-roles.md#site-recovery-contributor) -bu rol tüm izinleri gerekli toomanage Azure Site kurtarma işlemlerinin bir kurtarma Hizmetleri kasasına sahiptir. Bu role sahip bir kullanıcı ancak oluşturmak veya bir kurtarma Hizmetleri kasası silemez veya erişim hakları tooother kullanıcılar atayın. Merhaba durumda olabileceğinden bu rolü etkinleştirin ve olağanüstü durum kurtarma uygulamaları ya da tüm kuruluşlar için yönetmek olağanüstü durum kurtarma Yöneticiler için idealdir.
* [Site kurtarma işleci](../active-directory/role-based-access-built-in-roles.md#site-recovery-operator) -bu rol izinleri tooexecute ve manager yük devretme ve yeniden çalışma işlemlerini sahiptir. Bu rolüne sahip bir kullanıcı etkinleştirmek veya çoğaltma devre dışı bırakmak, oluşturmak veya kasalarını silmek, yeni altyapı kaydedilemiyor veya erişim hakları tooother kullanıcılar atayın. Bu rol kimin yük devretme sanal makinelerin olağanüstü durum kurtarma işleci için uygundur veya uygulama sahipleri ve gerçek veya sanal olağanüstü durumda bir DR gibi BT yöneticileri tarafından istendiğinde uygulamaları ayrıntıya gidin. POST hello olağanüstü durum çözümlemesi, hello DR işleci yeniden koruyabilir ve geri dönme hello sanal makineler.
* [Site kurtarma okuyucu](../active-directory/role-based-access-built-in-roles.md#site-recovery-reader) -bu rol izinleri tooview tüm Site Recovery yönetim işlemlerinin sahiptir. Bu rol kimin hello geçerli koruma durumunu izleyebilir ve Destek biletlerini gerekli olursa BT izleme yöneticinin için uygundur.

Daha fazla denetim için kendi rolleri toodefine arıyorsanız, bkz. nasıl çok[özel roller yapı](../active-directory/role-based-access-control-custom-roles.md) Azure.

## <a name="permissions-required-tooenable-replication-for-new-virtual-machines"></a>TooEnable çoğaltma yeni sanal makineler için gereken izinler
Yeni bir sanal makine Azure Site RECOVERY'yi kullanarak çoğaltılmış tooAzure olduğunda, kullanıcı hello doğrulanmış tooensure ilişkili hello kullanıcının erişim düzeyleri olan hello izinleri toouse hello sağlanan Azure kaynakları tooSite kurtarma istedi.

Yeni bir sanal makine için çoğaltma tooenable, bir kullanıcı olması gerekir:
* İzni toocreate hello seçili kaynak grubu içindeki bir sanal makineye
* İzni toocreate hello seçilen sanal ağ içindeki bir sanal makineye
* Depolama hesabı izni toowrite toohello seçili

Bir kullanıcının izinleri toocomplete yeni bir sanal makine çoğaltmasını aşağıdaki hello gerekir.

> [!IMPORTANT]
>İlgili izinleri hello dağıtım modeli eklendiğinden emin olun (Resource Manager / Klasik) kaynak dağıtımı için kullanılır.

| **Kaynak Türü** | **Dağıtım modeli** | **İzni** |
| --- | --- | --- |
| İşlem | Resource Manager | Microsoft.Compute/availabilitySets/read |
|  |  | Microsoft.Compute/virtualMachines/read |
|  |  | Microsoft.Compute/virtualMachines/write |
|  |  | Microsoft.Compute/virtualMachines/delete |
|  | Klasik | Microsoft.ClassicCompute/domainNames/read |
|  |  | Microsoft.ClassicCompute/domainNames/write |
|  |  | Microsoft.ClassicCompute/domainNames/delete |
|  |  | Microsoft.ClassicCompute/virtualMachines/read |
|  |  | Microsoft.ClassicCompute/virtualMachines/write |
|  |  | Microsoft.ClassicCompute/virtualMachines/delete |
| Ağ | Resource Manager | Microsoft.Network/networkInterfaces/read |
|  |  | Microsoft.Network/networkInterfaces/write |
|  |  | Microsoft.Network/networkInterfaces/delete |
|  |  | Microsoft.Network/networkInterfaces/join/action |
|  |  | Microsoft.Network/virtualNetworks/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/join/action |
|  | Klasik | Microsoft.ClassicNetwork/virtualNetworks/read |
|  |  | Microsoft.ClassicNetwork/virtualNetworks/join/action |
| Depolama | Resource Manager | Microsoft.Storage/storageAccounts/read |
|  |  | Microsoft.Storage/storageAccounts/listkeys/action |
|  | Klasik | Microsoft.ClassicStorage/storageAccounts/read |
|  |  | Microsoft.ClassicStorage/storageAccounts/listKeys/action |
| Kaynak Grubu | Resource Manager | Microsoft.Resources/deployments/* |
|  |  | Microsoft.Resources/subscriptions/resourceGroups/read |

Merhaba 'Sanal makine Katılımcısı' ve 'Klasik sanal makine Katılımcısı' kullanmayı düşünün [yerleşik roller](../active-directory/role-based-access-built-in-roles.md) için Resource Manager ve klasik dağıtım modelleri sırasıyla.

## <a name="next-steps"></a>Sonraki adımlar
* [Rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md): hello Azure portalında RBAC ile çalışmaya başlama.
* Toomanage nasıl erişim ile bilgi edinin:
  * [PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [REST API](../active-directory/role-based-access-control-manage-access-rest.md)
* [Rol tabanlı erişim denetimi sorun giderme](../active-directory/role-based-access-control-troubleshooting.md): sık karşılaşılan sorunları düzeltmek için öneriler alın.
