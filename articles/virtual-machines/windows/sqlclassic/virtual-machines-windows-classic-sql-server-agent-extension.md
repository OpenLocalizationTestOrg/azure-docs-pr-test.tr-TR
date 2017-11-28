---
title: "SQL VM'ler (Klasik) aaaAutomate yönetim görevleri | Microsoft Docs"
description: "Bu konuda nasıl toomanage hello belirli SQL Server yönetim görevlerini otomatikleştirir SQL Server Aracısı uzantısı açıklanmaktadır. Bunlar otomatik yedekleme, otomatik düzeltme eki uygulama ve Azure anahtar kasası tümleştirmeyi içerir. Bu konuda hello Klasik dağıtım modunu kullanır."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a9bda2e7-cdba-427c-bc30-77cde4376f3a
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1dc011e0526845701eaf0c365007938f9ee32ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a><span data-ttu-id="bf756-105">Merhaba SQL Server Aracısı uzantısı (Klasik) ile Azure sanal makineler üzerinde yönetim görevleri otomatik hale getirme</span><span class="sxs-lookup"><span data-stu-id="bf756-105">Automate management tasks on Azure Virtual Machines with hello SQL Server Agent Extension (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bf756-106">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bf756-106">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="bf756-107">Klasik</span><span class="sxs-lookup"><span data-stu-id="bf756-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
>
 
<span data-ttu-id="bf756-108">SQL Server Iaas Aracısı uzantısı (Sqlıaasagent) Hello Azure sanal makineleri tooautomate yönetim görevlerini üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="bf756-108">hello SQL Server IaaS Agent Extension (SQLIaaSAgent) runs on Azure virtual machines tooautomate administration tasks.</span></span> <span data-ttu-id="bf756-109">Bu konu, yükleme, durum ve kaldırma yönergeleri yanı sıra hello uzantısı tarafından desteklenen hello hizmetlerine genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="bf756-109">This topic provides an overview of hello services supported by hello extension as well as instructions for installation, status, and removal.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="bf756-110">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bf756-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bf756-111">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="bf756-111">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="bf756-112">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="bf756-112">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="bf756-113">Bu makalenin tooview hello Resource Manager sürümü bkz [SQL Server Aracısı uzantısı için SQL Server VM'ler Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="bf756-113">tooview hello Resource Manager version of this article, see [SQL Server Agent Extension for SQL Server VMs Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="bf756-114">Desteklenen hizmetler</span><span class="sxs-lookup"><span data-stu-id="bf756-114">Supported services</span></span>
<span data-ttu-id="bf756-115">SQL Server Iaas Aracısı uzantısı Hello hello aşağıdaki yönetim görevlerini destekler:</span><span class="sxs-lookup"><span data-stu-id="bf756-115">hello SQL Server IaaS Agent Extension supports hello following administration tasks:</span></span>

| <span data-ttu-id="bf756-116">Yönetim özelliği</span><span class="sxs-lookup"><span data-stu-id="bf756-116">Administration feature</span></span> | <span data-ttu-id="bf756-117">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bf756-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bf756-118">**SQL otomatik yedekleme**</span><span class="sxs-lookup"><span data-stu-id="bf756-118">**SQL Automated Backup**</span></span> |<span data-ttu-id="bf756-119">Merhaba hello varsayılan SQL Server'ın örneğinde hello VM tüm veritabanları için yedekleme zamanlaması otomatikleştirir.</span><span class="sxs-lookup"><span data-stu-id="bf756-119">Automates hello scheduling of backups for all databases for hello default instance of SQL Server in hello VM.</span></span> <span data-ttu-id="bf756-120">Daha fazla bilgi için bkz: [Azure Virtual Machines'de (Klasik) SQL Server için otomatik yedeklemeyi](../classic/sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="bf756-120">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-backup.md).</span></span> |
| <span data-ttu-id="bf756-121">**SQL otomatik düzeltme eki uygulama**</span><span class="sxs-lookup"><span data-stu-id="bf756-121">**SQL Automated Patching**</span></span> |<span data-ttu-id="bf756-122">Güncelleştirmeleri, iş yükü için yoğun saatlerde kaçınmak için bir bakım penceresi sırasında hangi güncelleştirmelerin VM sürebilir tooyour yerleştirin, yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="bf756-122">Configures a maintenance window during which updates tooyour VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="bf756-123">Daha fazla bilgi için bkz: [otomatik Azure Virtual Machines'de (Klasik) SQL Server için düzeltme eki uygulama](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="bf756-123">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-patching.md).</span></span> |
| <span data-ttu-id="bf756-124">**Azure Anahtar Kasası Tümleştirmesi**</span><span class="sxs-lookup"><span data-stu-id="bf756-124">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="bf756-125">Tooautomatically yükleme ve SQL Server VM'nize üzerinde Azure anahtar kasası yapılandırma sağlar.</span><span class="sxs-lookup"><span data-stu-id="bf756-125">Enables you tooautomatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="bf756-126">Daha fazla bilgi için bkz: [(Klasik) Azure vm'lerinde SQL Server için Azure anahtar kasası tümleştirmeyi yapılandırmak](../classic/ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="bf756-126">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Classic)](../classic/ps-sql-keyvault.md).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="bf756-127">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bf756-127">Prerequisites</span></span>
<span data-ttu-id="bf756-128">SQL Server Iaas Aracısı uzantısını VM toouse hello gereksinimleri:</span><span class="sxs-lookup"><span data-stu-id="bf756-128">Requirements toouse hello SQL Server IaaS Agent Extension on your VM:</span></span>

### <a name="operating-system"></a><span data-ttu-id="bf756-129">İşletim Sistemi:</span><span class="sxs-lookup"><span data-stu-id="bf756-129">Operating System:</span></span>
* <span data-ttu-id="bf756-130">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="bf756-130">Windows Server 2012</span></span>
* <span data-ttu-id="bf756-131">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="bf756-131">Windows Server 2012 R2</span></span>
* <span data-ttu-id="bf756-132">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="bf756-132">Windows Server 2016</span></span>

### <a name="sql-server-versions"></a><span data-ttu-id="bf756-133">SQL Server sürümleri:</span><span class="sxs-lookup"><span data-stu-id="bf756-133">SQL Server versions:</span></span>
* <span data-ttu-id="bf756-134">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="bf756-134">SQL Server 2012</span></span>
* <span data-ttu-id="bf756-135">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="bf756-135">SQL Server 2014</span></span>
* <span data-ttu-id="bf756-136">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="bf756-136">SQL Server 2016</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="bf756-137">Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bf756-137">Azure PowerShell:</span></span>
<span data-ttu-id="bf756-138">[İndirme ve hello en son Azure PowerShell komutlarının yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bf756-138">[Download and configure hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="bf756-139">Windows PowerShell'i başlatın ve tooyour Azure aboneliği ile Merhaba bağlamak **Add-AzureAccount** komutu.</span><span class="sxs-lookup"><span data-stu-id="bf756-139">Start Windows PowerShell, and connect it tooyour Azure subscription with hello **Add-AzureAccount** command.</span></span>

    Add-AzureAccount

<span data-ttu-id="bf756-140">Birden çok aboneliğiniz varsa, kullanmak **Select-AzureSubscription** hedef içeren tooselect hello abonelik Klasik VM.</span><span class="sxs-lookup"><span data-stu-id="bf756-140">If you have multiple subscriptions, use **Select-AzureSubscription** tooselect hello subscription that contains your target classic VM.</span></span>

    Select-AzureSubscription -SubscriptionName <subscriptionname>

<span data-ttu-id="bf756-141">Bu noktada, hello Klasik sanal makineleri ve ilişkili hizmet adlarını hello listesini almak **Get-AzureVM** komutu.</span><span class="sxs-lookup"><span data-stu-id="bf756-141">At this point, you can get a list of hello classic virtual machines and their associated service names with hello **Get-AzureVM** command.</span></span>

    Get-AzureVM

## <a name="installation"></a><span data-ttu-id="bf756-142">Yükleme</span><span class="sxs-lookup"><span data-stu-id="bf756-142">Installation</span></span>
<span data-ttu-id="bf756-143">Klasik VM'ler için PowerShell tooinstall hello SQL Server Iaas Aracısı uzantısı kullanın ve ilişkili hizmetlerini yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bf756-143">For classic VMs, you must use PowerShell tooinstall hello SQL Server IaaS Agent Extension and configure its associated services.</span></span> <span data-ttu-id="bf756-144">Kullanım hello **kümesi AzureVMSqlServerExtension** PowerShell cmdlet tooinstall hello uzantısı.</span><span class="sxs-lookup"><span data-stu-id="bf756-144">Use hello **Set-AzureVMSqlServerExtension** PowerShell cmdlet tooinstall hello extension.</span></span> <span data-ttu-id="bf756-145">Örneğin, komutu aşağıdaki hello hello uzantısı bir Windows Server VM'ye (Klasik) yükler ve bunu "SQLIaaSExtension" adları.</span><span class="sxs-lookup"><span data-stu-id="bf756-145">For example, hello following command installs hello extension on a Windows Server VM (classic) and names it "SQLIaaSExtension".</span></span>

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

<span data-ttu-id="bf756-146">Merhaba SQL Iaas Aracısı uzantısı en son sürümünü toohello güncelleştirirseniz, hello uzantısı güncelleştirdikten sonra sanal makinenizi yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bf756-146">If you update toohello latest version of hello SQL IaaS Agent Extension, you must restart your virtual machine after updating hello extension.</span></span>

> [!NOTE]
> <span data-ttu-id="bf756-147">Klasik sanal makineleri olmayan bir seçenek tooinstall sahip ve hello SQL Iaas Aracısı uzantısı hello portal üzerinden yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bf756-147">Classic virtual machines do not have an option tooinstall and configure hello SQL IaaS Agent Extension through hello portal.</span></span>
> 
> 

## <a name="status"></a><span data-ttu-id="bf756-148">Durum</span><span class="sxs-lookup"><span data-stu-id="bf756-148">Status</span></span>
<span data-ttu-id="bf756-149">Tek yönlü tooverify Hello uzantısı yüklenir tooview hello aracı durumunu hello Azure Portal ' dir.</span><span class="sxs-lookup"><span data-stu-id="bf756-149">One way tooverify that hello extension is installed is tooview hello agent status in hello Azure Portal.</span></span> <span data-ttu-id="bf756-150">Merhaba sanal makine dikey penceresinde listelenen bir sanal makineyi seçin ve ardından tıklatın **uzantıları**.</span><span class="sxs-lookup"><span data-stu-id="bf756-150">Select a virtual machine listed in hello virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="bf756-151">Merhaba görmelisiniz **Sqlıaasagent** listelenen uzantısı.</span><span class="sxs-lookup"><span data-stu-id="bf756-151">You should see hello **SQLIaaSAgent** extension listed.</span></span>

![SQL Server Iaas Aracısı uzantısı Azure portalında](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

<span data-ttu-id="bf756-153">Merhaba de kullanabilirsiniz **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bf756-153">You can also use hello **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a><span data-ttu-id="bf756-154">Temizleme</span><span class="sxs-lookup"><span data-stu-id="bf756-154">Removal</span></span>
<span data-ttu-id="bf756-155">Hello Azure Portal, hello üzerindeki hello üç nokta düğmesine tıklayarak hello uzantısını kaldırabilirsiniz **uzantıları** dikey penceresinde, sanal makine özellikleri.</span><span class="sxs-lookup"><span data-stu-id="bf756-155">In hello Azure Portal, you can uninstall hello extension by clicking hello ellipsis on hello **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="bf756-156">Ardından **kaldırma**.</span><span class="sxs-lookup"><span data-stu-id="bf756-156">Then click **Uninstall**.</span></span>

![Hello Azure Portalı'nda SQL Server Iaas Aracısı uzantısı kaldırma](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="bf756-158">Merhaba de kullanabilirsiniz **Kaldır AzureVMSqlServerExtension** Powershell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bf756-158">You can also use hello **Remove-AzureVMSqlServerExtension** Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="bf756-159">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="bf756-159">Next Steps</span></span>
<span data-ttu-id="bf756-160">Merhaba uzantısı tarafından desteklenen hello hizmetlerini birini kullanarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="bf756-160">Begin using one of hello services supported by hello extension.</span></span> <span data-ttu-id="bf756-161">Daha fazla ayrıntı için bkz: hello başvurulan hello konular [desteklenen Hizmetleri](#supported-services) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="bf756-161">For more details, see hello topics referenced in hello [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="bf756-162">SQL Server Azure sanal makinelerde çalıştırma hakkında daha fazla bilgi için bkz: [Azure sanal makinelere genel bakış SQL Server'da](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bf756-162">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

