---
title: "Site Recovery kasası Sil"
description: "Site Recovery senaryoyu temel bir Azure Site Recovery kasası silme hakkında bilgi edinin."
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
ms.openlocfilehash: b95b9defa0a037f7d7d3ef36b99bc7c53c751050
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="02b41-103">Site Recovery kasası Sil</span><span class="sxs-lookup"><span data-stu-id="02b41-103">Delete a Site Recovery vault</span></span>
<span data-ttu-id="02b41-104">Bağımlılıklar, bir Azure Site Recovery kasası silmesini engelleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02b41-104">Dependencies can prevent you from deleting an Azure Site Recovery vault.</span></span> <span data-ttu-id="02b41-105">Size gereken eylemleri Site kurtarma senaryosunda göre farklılık gösterir: VMware azure'a, Hyper-V (ile arama ve Sistem Merkezi Sanal Makine Yöneticisi olmadan) Azure ve Azure yedekleme için.</span><span class="sxs-lookup"><span data-stu-id="02b41-105">The actions you need to take vary based on the Site Recovery scenario: VMware to Azure, Hyper-V (with and without System Center Virtual Machine Manager) to Azure, and Azure Backup.</span></span> <span data-ttu-id="02b41-106">Azure Backup ile kullanılan bir kasa silmek için bkz: [Azure yedekleme kasasına silme](../backup/backup-azure-delete-vault.md).</span><span class="sxs-lookup"><span data-stu-id="02b41-106">To delete a vault used in Azure Backup, see [Delete a Backup vault in Azure](../backup/backup-azure-delete-vault.md).</span></span>

>[!Important]
><span data-ttu-id="02b41-107">Ürün test ettiğiniz ve veri kaybı hakkında ilgili değil, kasaya ve tüm bağımlılıklarını daha kolay kaldırmaya zorla delete yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="02b41-107">If you're testing the product and aren't concerned about data loss, use the force delete method to rapidly remove the vault and all its dependencies.</span></span>

> <span data-ttu-id="02b41-108">PowerShell komut kasasının tüm içeriği siler ve geri alınamaz.</span><span class="sxs-lookup"><span data-stu-id="02b41-108">The PowerShell command deletes all the contents of the vault and is not reversible.</span></span>

## <a name="use-powershell-to-force-delete-the-vault"></a><span data-ttu-id="02b41-109">Zorlamak için kullanım PowerShell kasa silme</span><span class="sxs-lookup"><span data-stu-id="02b41-109">Use PowerShell to force delete the vault</span></span> 

<span data-ttu-id="02b41-110">Korunan öğelerin olsa bile Site Recovery kasası silmek için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="02b41-110">To delete the Site Recovery vault even if there are protected items, use these commands:</span></span>

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="02b41-111">Site Recovery kasası Sil</span><span class="sxs-lookup"><span data-stu-id="02b41-111">Delete a Site Recovery vault</span></span> 
<span data-ttu-id="02b41-112">Kasayı silmek için senaryonuz için önerilen adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="02b41-112">To delete the vault, follow the recommended steps for your scenario.</span></span>

### <a name="vmware-vms-to-azure"></a><span data-ttu-id="02b41-113">VMware VM'lerini Azure'a</span><span class="sxs-lookup"><span data-stu-id="02b41-113">VMware VMs to Azure</span></span>

1. <span data-ttu-id="02b41-114">İçindeki adımları izleyerek VM'ler korumalı Sil tüm [VMware için korumayı devre dışı bırakma](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="02b41-114">Delete all protected VMs by following the steps in [Disable protection for a VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="02b41-115">İçindeki adımları izleyerek tüm çoğaltma ilkelerinin silme [çoğaltma ilkesini silmek](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="02b41-115">Delete all replication policies by following the steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="02b41-116">İçindeki adımları izleyerek vCenter başvurular silme [bir vCenter silmek](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span><span class="sxs-lookup"><span data-stu-id="02b41-116">Delete references to vCenter by following the steps in [Delete a vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span></span>

4. <span data-ttu-id="02b41-117">İçindeki adımları izleyerek yapılandırma sunucusunu silmek [yapılandırma sunucusu yetkisini](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="02b41-117">Delete the configuration server by following the steps in [Decommission a configuration server](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span></span>

5. <span data-ttu-id="02b41-118">Kasayı silin.</span><span class="sxs-lookup"><span data-stu-id="02b41-118">Delete the vault.</span></span>


### <a name="hyper-v-vms-with-virtual-machine-manager-to-azure"></a><span data-ttu-id="02b41-119">Azure Hyper-V sanal makineleri (Sanal Makine Yöneticisi ile)</span><span class="sxs-lookup"><span data-stu-id="02b41-119">Hyper-V VMs (with Virtual Machine Manager) to Azure</span></span>
1. <span data-ttu-id="02b41-120">İçindeki adımları izleyerek VM'ler korumalı Sil tüm [VMware VM veya fiziksel sunucu için koruma devre dışı bırakma](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="02b41-120">Delete all protected VMs by following the steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="02b41-121">İçindeki adımları izleyerek tüm çoğaltma ilkelerinin silme [çoğaltma ilkesini silmek](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="02b41-121">Delete all replication policies by following the steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3.  <span data-ttu-id="02b41-122">Sanal Makine Yöneticisi sunucularına başvuruları içindeki adımları izleyerek silmek [bağlı bir VMM sunucusunun kaydı](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span><span class="sxs-lookup"><span data-stu-id="02b41-122">Delete references to Virtual Machine Manager servers by following the steps in [Unregister a connected VMM server](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span></span>

4.  <span data-ttu-id="02b41-123">Kasayı silin.</span><span class="sxs-lookup"><span data-stu-id="02b41-123">Delete the vault.</span></span>

### <a name="hyper-v-vms-without-virtual-machine-manager-to-azure"></a><span data-ttu-id="02b41-124">Azure için Hyper-V Vm'lerini (olmadan Sanal Makine Yöneticisi)</span><span class="sxs-lookup"><span data-stu-id="02b41-124">Hyper-V VMs (without Virtual Machine Manager) to Azure</span></span>
1. <span data-ttu-id="02b41-125">İçindeki adımları izleyerek VM'ler korumalı Sil tüm [VMware VM veya fiziksel sunucu için koruma devre dışı bırakma](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="02b41-125">Delete all protected VMs by following the steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="02b41-126">İçindeki adımları izleyerek tüm çoğaltma ilkelerinin silme [çoğaltma ilkesini silmek](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="02b41-126">Delete all replication policies by following the steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="02b41-127">Hyper-V sunucuları başvurular içindeki adımları izleyerek silme [bir Hyper-V ana bilgisayar kaydı](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span><span class="sxs-lookup"><span data-stu-id="02b41-127">Delete references to Hyper-V servers by following the steps in [Unregister a Hyper-V host](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span></span>

4. <span data-ttu-id="02b41-128">Hyper-V sitesi silin.</span><span class="sxs-lookup"><span data-stu-id="02b41-128">Delete the Hyper-V site.</span></span>

5. <span data-ttu-id="02b41-129">Kasayı silin.</span><span class="sxs-lookup"><span data-stu-id="02b41-129">Delete the vault.</span></span>
