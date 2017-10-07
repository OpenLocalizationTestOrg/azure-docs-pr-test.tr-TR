---
title: "aaaDelete Site Recovery kasası"
description: "Nasıl toodelete bir Azure Site Recovery kasası dayalı hello Site kurtarma senaryosunda öğrenin."
service: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: 36db202d8b790bb5d31d1348fb72f51acb5d559c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-site-recovery-vault"></a>Site Recovery kasası Sil
Bağımlılıklar, bir Azure Site Recovery kasası silmesini engelleyebilirsiniz. Merhaba tootake gereken eylemler hello Site kurtarma senaryosunda göre farklılık gösterir: VMware tooAzure, Hyper-V (ile arama ve Sistem Merkezi Sanal Makine Yöneticisi olmadan) tooAzure ve Azure yedekleme. toodelete Azure yedeklemesinde kullanılan bir kasa bkz [Azure yedekleme kasasına silme](../backup/backup-azure-delete-vault.md).

>[!Important]
>Merhaba ürün test ettiğiniz ve veri kaybı hakkında ilgili değil, kullanım hello zorla silme yöntemi toorapidly hello kasası ve tüm bağımlılıkları kaldırın.

> Merhaba PowerShell komutunu hello kasası tüm hello içeriğini siler ve geri alınamaz.

## <a name="use-powershell-tooforce-delete-hello-vault"></a>Kullanım PowerShell tooforce hello kasa silme 

Site Recovery kasası olsa bile toodelete hello korunan öğeleri, bu komutları kullanın:

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a>Site Recovery kasası Sil 
toodelete hello kasası izleyin hello adımları senaryonuz için önerilir.

### <a name="vmware-vms-tooazure"></a>VMware Vm'leri tooAzure

1. Delete tüm korumalı sanal makineleri hello adımları izleyerek [VMware için korumayı devre dışı bırakma](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Tüm çoğaltma ilkelerinin hello adımları izleyerek silme [çoğaltma ilkesini silmek](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3. Aşağıdaki hello tarafından toovCenter adımları başvuruları silmek [bir vCenter silmek](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).

4. Merhaba adımları izleyerek Hello yapılandırma sunucusu silme [yapılandırma sunucusu yetkisini](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).

5. Merhaba kasayı silin.


### <a name="hyper-v-vms-with-virtual-machine-manager-tooazure"></a>Hyper-V sanal makineleri (Sanal Makine Yöneticisi ile) tooAzure
1. Delete tüm korumalı sanal makineleri hello adımları izleyerek [VMware VM veya fiziksel sunucu için koruma devre dışı bırakma](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Tüm çoğaltma ilkelerinin hello adımları izleyerek silme [çoğaltma ilkesini silmek](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3.  Delete hello adımları izleyerek tooVirtual Machine Manager sunucuları başvuran [bağlı bir VMM sunucusunun kaydı](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).

4.  Merhaba kasayı silin.

### <a name="hyper-v-vms-without-virtual-machine-manager-tooazure"></a>Hyper-V sanal makineleri (olmadan Sanal Makine Yöneticisi) tooAzure
1. Delete tüm korumalı sanal makineleri hello adımları izleyerek [VMware VM veya fiziksel sunucu için koruma devre dışı bırakma](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Tüm çoğaltma ilkelerinin hello adımları izleyerek silme [çoğaltma ilkesini silmek](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3. Delete hello adımları izleyerek tooHyper-V sunucuları başvuran [bir Hyper-V ana bilgisayar kaydı](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).

4. Merhaba Hyper-V sitesi silin.

5. Merhaba kasayı silin.
