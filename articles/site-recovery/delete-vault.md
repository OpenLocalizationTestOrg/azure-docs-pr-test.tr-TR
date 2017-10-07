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
# <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="e603a-103">Site Recovery kasası Sil</span><span class="sxs-lookup"><span data-stu-id="e603a-103">Delete a Site Recovery vault</span></span>
<span data-ttu-id="e603a-104">Bağımlılıklar, bir Azure Site Recovery kasası silmesini engelleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e603a-104">Dependencies can prevent you from deleting an Azure Site Recovery vault.</span></span> <span data-ttu-id="e603a-105">Merhaba tootake gereken eylemler hello Site kurtarma senaryosunda göre farklılık gösterir: VMware tooAzure, Hyper-V (ile arama ve Sistem Merkezi Sanal Makine Yöneticisi olmadan) tooAzure ve Azure yedekleme.</span><span class="sxs-lookup"><span data-stu-id="e603a-105">hello actions you need tootake vary based on hello Site Recovery scenario: VMware tooAzure, Hyper-V (with and without System Center Virtual Machine Manager) tooAzure, and Azure Backup.</span></span> <span data-ttu-id="e603a-106">toodelete Azure yedeklemesinde kullanılan bir kasa bkz [Azure yedekleme kasasına silme](../backup/backup-azure-delete-vault.md).</span><span class="sxs-lookup"><span data-stu-id="e603a-106">toodelete a vault used in Azure Backup, see [Delete a Backup vault in Azure](../backup/backup-azure-delete-vault.md).</span></span>

>[!Important]
><span data-ttu-id="e603a-107">Merhaba ürün test ettiğiniz ve veri kaybı hakkında ilgili değil, kullanım hello zorla silme yöntemi toorapidly hello kasası ve tüm bağımlılıkları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e603a-107">If you're testing hello product and aren't concerned about data loss, use hello force delete method toorapidly remove hello vault and all its dependencies.</span></span>

> <span data-ttu-id="e603a-108">Merhaba PowerShell komutunu hello kasası tüm hello içeriğini siler ve geri alınamaz.</span><span class="sxs-lookup"><span data-stu-id="e603a-108">hello PowerShell command deletes all hello contents of hello vault and is not reversible.</span></span>

## <a name="use-powershell-tooforce-delete-hello-vault"></a><span data-ttu-id="e603a-109">Kullanım PowerShell tooforce hello kasa silme</span><span class="sxs-lookup"><span data-stu-id="e603a-109">Use PowerShell tooforce delete hello vault</span></span> 

<span data-ttu-id="e603a-110">Site Recovery kasası olsa bile toodelete hello korunan öğeleri, bu komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="e603a-110">toodelete hello Site Recovery vault even if there are protected items, use these commands:</span></span>

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="e603a-111">Site Recovery kasası Sil</span><span class="sxs-lookup"><span data-stu-id="e603a-111">Delete a Site Recovery vault</span></span> 
<span data-ttu-id="e603a-112">toodelete hello kasası izleyin hello adımları senaryonuz için önerilir.</span><span class="sxs-lookup"><span data-stu-id="e603a-112">toodelete hello vault, follow hello recommended steps for your scenario.</span></span>

### <a name="vmware-vms-tooazure"></a><span data-ttu-id="e603a-113">VMware Vm'leri tooAzure</span><span class="sxs-lookup"><span data-stu-id="e603a-113">VMware VMs tooAzure</span></span>

1. <span data-ttu-id="e603a-114">Delete tüm korumalı sanal makineleri hello adımları izleyerek [VMware için korumayı devre dışı bırakma](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="e603a-114">Delete all protected VMs by following hello steps in [Disable protection for a VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="e603a-115">Tüm çoğaltma ilkelerinin hello adımları izleyerek silme [çoğaltma ilkesini silmek](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="e603a-115">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="e603a-116">Aşağıdaki hello tarafından toovCenter adımları başvuruları silmek [bir vCenter silmek](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span><span class="sxs-lookup"><span data-stu-id="e603a-116">Delete references toovCenter by following hello steps in [Delete a vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span></span>

4. <span data-ttu-id="e603a-117">Merhaba adımları izleyerek Hello yapılandırma sunucusu silme [yapılandırma sunucusu yetkisini](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="e603a-117">Delete hello configuration server by following hello steps in [Decommission a configuration server](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span></span>

5. <span data-ttu-id="e603a-118">Merhaba kasayı silin.</span><span class="sxs-lookup"><span data-stu-id="e603a-118">Delete hello vault.</span></span>


### <a name="hyper-v-vms-with-virtual-machine-manager-tooazure"></a><span data-ttu-id="e603a-119">Hyper-V sanal makineleri (Sanal Makine Yöneticisi ile) tooAzure</span><span class="sxs-lookup"><span data-stu-id="e603a-119">Hyper-V VMs (with Virtual Machine Manager) tooAzure</span></span>
1. <span data-ttu-id="e603a-120">Delete tüm korumalı sanal makineleri hello adımları izleyerek [VMware VM veya fiziksel sunucu için koruma devre dışı bırakma](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="e603a-120">Delete all protected VMs by following hello steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="e603a-121">Tüm çoğaltma ilkelerinin hello adımları izleyerek silme [çoğaltma ilkesini silmek](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="e603a-121">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3.  <span data-ttu-id="e603a-122">Delete hello adımları izleyerek tooVirtual Machine Manager sunucuları başvuran [bağlı bir VMM sunucusunun kaydı](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span><span class="sxs-lookup"><span data-stu-id="e603a-122">Delete references tooVirtual Machine Manager servers by following hello steps in [Unregister a connected VMM server](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span></span>

4.  <span data-ttu-id="e603a-123">Merhaba kasayı silin.</span><span class="sxs-lookup"><span data-stu-id="e603a-123">Delete hello vault.</span></span>

### <a name="hyper-v-vms-without-virtual-machine-manager-tooazure"></a><span data-ttu-id="e603a-124">Hyper-V sanal makineleri (olmadan Sanal Makine Yöneticisi) tooAzure</span><span class="sxs-lookup"><span data-stu-id="e603a-124">Hyper-V VMs (without Virtual Machine Manager) tooAzure</span></span>
1. <span data-ttu-id="e603a-125">Delete tüm korumalı sanal makineleri hello adımları izleyerek [VMware VM veya fiziksel sunucu için koruma devre dışı bırakma](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="e603a-125">Delete all protected VMs by following hello steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="e603a-126">Tüm çoğaltma ilkelerinin hello adımları izleyerek silme [çoğaltma ilkesini silmek](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="e603a-126">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="e603a-127">Delete hello adımları izleyerek tooHyper-V sunucuları başvuran [bir Hyper-V ana bilgisayar kaydı](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span><span class="sxs-lookup"><span data-stu-id="e603a-127">Delete references tooHyper-V servers by following hello steps in [Unregister a Hyper-V host](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span></span>

4. <span data-ttu-id="e603a-128">Merhaba Hyper-V sitesi silin.</span><span class="sxs-lookup"><span data-stu-id="e603a-128">Delete hello Hyper-V site.</span></span>

5. <span data-ttu-id="e603a-129">Merhaba kasayı silin.</span><span class="sxs-lookup"><span data-stu-id="e603a-129">Delete hello vault.</span></span>
