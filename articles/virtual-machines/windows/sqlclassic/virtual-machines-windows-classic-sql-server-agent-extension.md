---
title: "SQL vm'lerde (Klasik) yönetim görevlerini otomatikleştiren | Microsoft Docs"
description: "Bu konuda, belirli SQL Server yönetim görevlerini otomatikleştirir SQL Server Aracısı uzantısı yönetmek açıklar. Bunlar otomatik yedekleme, otomatik düzeltme eki uygulama ve Azure anahtar kasası tümleştirmeyi içerir. Bu konu, Klasik dağıtım modunu kullanır."
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
ms.openlocfilehash: 30fa9128cd51a7498449c991b58500ad9acdd3d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-the-sql-server-agent-extension-classic"></a><span data-ttu-id="bc94e-105">SQL Server Aracısı uzantısı (Klasik) ile Azure sanal makineler üzerinde yönetim görevlerini otomatik hale getirme</span><span class="sxs-lookup"><span data-stu-id="bc94e-105">Automate management tasks on Azure Virtual Machines with the SQL Server Agent Extension (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bc94e-106">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bc94e-106">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="bc94e-107">Klasik</span><span class="sxs-lookup"><span data-stu-id="bc94e-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
>
 
<span data-ttu-id="bc94e-108">SQL Server Iaas Aracısı uzantısı (Sqlıaasagent) Azure yönetim görevlerini otomatikleştirmek için sanal makinelerde çalışır.</span><span class="sxs-lookup"><span data-stu-id="bc94e-108">The SQL Server IaaS Agent Extension (SQLIaaSAgent) runs on Azure virtual machines to automate administration tasks.</span></span> <span data-ttu-id="bc94e-109">Bu konu, yükleme, durum ve kaldırma yönergeleri yanı sıra uzantısı tarafından desteklenen hizmetlerine genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc94e-109">This topic provides an overview of the services supported by the extension as well as instructions for installation, status, and removal.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="bc94e-110">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bc94e-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bc94e-111">Bu makalede, Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="bc94e-111">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="bc94e-112">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="bc94e-112">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="bc94e-113">Bu makalede Resource Manager sürümünü görüntülemek için bkz: [SQL Server Aracısı uzantısı için SQL Server VM'ler Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="bc94e-113">To view the Resource Manager version of this article, see [SQL Server Agent Extension for SQL Server VMs Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="bc94e-114">Desteklenen hizmetler</span><span class="sxs-lookup"><span data-stu-id="bc94e-114">Supported services</span></span>
<span data-ttu-id="bc94e-115">SQL Server Iaas Aracısı uzantısı aşağıdaki yönetim görevlerini destekler:</span><span class="sxs-lookup"><span data-stu-id="bc94e-115">The SQL Server IaaS Agent Extension supports the following administration tasks:</span></span>

| <span data-ttu-id="bc94e-116">Yönetim özelliği</span><span class="sxs-lookup"><span data-stu-id="bc94e-116">Administration feature</span></span> | <span data-ttu-id="bc94e-117">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bc94e-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bc94e-118">**SQL otomatik yedekleme**</span><span class="sxs-lookup"><span data-stu-id="bc94e-118">**SQL Automated Backup**</span></span> |<span data-ttu-id="bc94e-119">Tüm veritabanları için yedekleme VM'de SQL Server'ın varsayılan örneğinin zamanlama otomatikleştirir.</span><span class="sxs-lookup"><span data-stu-id="bc94e-119">Automates the scheduling of backups for all databases for the default instance of SQL Server in the VM.</span></span> <span data-ttu-id="bc94e-120">Daha fazla bilgi için bkz: [Azure Virtual Machines'de (Klasik) SQL Server için otomatik yedeklemeyi](../classic/sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="bc94e-120">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-backup.md).</span></span> |
| <span data-ttu-id="bc94e-121">**SQL otomatik düzeltme eki uygulama**</span><span class="sxs-lookup"><span data-stu-id="bc94e-121">**SQL Automated Patching**</span></span> |<span data-ttu-id="bc94e-122">Güncelleştirmeleri, iş yükü için yoğun saatlerde kaçınmak için güncelleştirme, VM, gerçekleştirilebildiği bir bakım penceresi yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="bc94e-122">Configures a maintenance window during which updates to your VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="bc94e-123">Daha fazla bilgi için bkz: [otomatik Azure Virtual Machines'de (Klasik) SQL Server için düzeltme eki uygulama](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="bc94e-123">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-patching.md).</span></span> |
| <span data-ttu-id="bc94e-124">**Azure Anahtar Kasası Tümleştirmesi**</span><span class="sxs-lookup"><span data-stu-id="bc94e-124">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="bc94e-125">Otomatik olarak yüklemek ve SQL Server VM'nize üzerinde Azure anahtar kasası yapılandırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc94e-125">Enables you to automatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="bc94e-126">Daha fazla bilgi için bkz: [(Klasik) Azure vm'lerinde SQL Server için Azure anahtar kasası tümleştirmeyi yapılandırmak](../classic/ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="bc94e-126">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Classic)](../classic/ps-sql-keyvault.md).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="bc94e-127">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bc94e-127">Prerequisites</span></span>
<span data-ttu-id="bc94e-128">VM üzerinde SQL Server Iaas Aracısı uzantısı kullanmak için gereksinimler:</span><span class="sxs-lookup"><span data-stu-id="bc94e-128">Requirements to use the SQL Server IaaS Agent Extension on your VM:</span></span>

### <a name="operating-system"></a><span data-ttu-id="bc94e-129">İşletim Sistemi:</span><span class="sxs-lookup"><span data-stu-id="bc94e-129">Operating System:</span></span>
* <span data-ttu-id="bc94e-130">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="bc94e-130">Windows Server 2012</span></span>
* <span data-ttu-id="bc94e-131">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="bc94e-131">Windows Server 2012 R2</span></span>
* <span data-ttu-id="bc94e-132">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="bc94e-132">Windows Server 2016</span></span>

### <a name="sql-server-versions"></a><span data-ttu-id="bc94e-133">SQL Server sürümleri:</span><span class="sxs-lookup"><span data-stu-id="bc94e-133">SQL Server versions:</span></span>
* <span data-ttu-id="bc94e-134">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="bc94e-134">SQL Server 2012</span></span>
* <span data-ttu-id="bc94e-135">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="bc94e-135">SQL Server 2014</span></span>
* <span data-ttu-id="bc94e-136">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="bc94e-136">SQL Server 2016</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="bc94e-137">Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bc94e-137">Azure PowerShell:</span></span>
<span data-ttu-id="bc94e-138">[İndirme ve en son Azure PowerShell komutlarının yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bc94e-138">[Download and configure the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="bc94e-139">Windows PowerShell'i başlatın ve Azure aboneliğinizle bağlanmak **Add-AzureAccount** komutu.</span><span class="sxs-lookup"><span data-stu-id="bc94e-139">Start Windows PowerShell, and connect it to your Azure subscription with the **Add-AzureAccount** command.</span></span>

    Add-AzureAccount

<span data-ttu-id="bc94e-140">Birden çok aboneliğiniz varsa, kullanmak **Select-AzureSubscription** hedef içeren aboneliği seçmek için Klasik VM.</span><span class="sxs-lookup"><span data-stu-id="bc94e-140">If you have multiple subscriptions, use **Select-AzureSubscription** to select the subscription that contains your target classic VM.</span></span>

    Select-AzureSubscription -SubscriptionName <subscriptionname>

<span data-ttu-id="bc94e-141">Bu noktada, Klasik sanal makineleri ve ilişkili hizmet adlarını listesini almak **Get-AzureVM** komutu.</span><span class="sxs-lookup"><span data-stu-id="bc94e-141">At this point, you can get a list of the classic virtual machines and their associated service names with the **Get-AzureVM** command.</span></span>

    Get-AzureVM

## <a name="installation"></a><span data-ttu-id="bc94e-142">Yükleme</span><span class="sxs-lookup"><span data-stu-id="bc94e-142">Installation</span></span>
<span data-ttu-id="bc94e-143">Klasik VM'ler için SQL Server Iaas Aracısı uzantısını yükleyin ve ilişkili hizmetlerini yapılandırmak için PowerShell kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc94e-143">For classic VMs, you must use PowerShell to install the SQL Server IaaS Agent Extension and configure its associated services.</span></span> <span data-ttu-id="bc94e-144">Kullanım **kümesi AzureVMSqlServerExtension** uzantıyı yüklemek için PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bc94e-144">Use the **Set-AzureVMSqlServerExtension** PowerShell cmdlet to install the extension.</span></span> <span data-ttu-id="bc94e-145">Örneğin, aşağıdaki komutu bir Windows Server VM'ye (Klasik) uzantıyı yükleyen ve "SQLIaaSExtension" adları.</span><span class="sxs-lookup"><span data-stu-id="bc94e-145">For example, the following command installs the extension on a Windows Server VM (classic) and names it "SQLIaaSExtension".</span></span>

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

<span data-ttu-id="bc94e-146">SQL Iaas Aracısı uzantısı'nın en son sürüm güncelleştirirseniz, uzantı güncelleştirdikten sonra sanal makinenizi yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc94e-146">If you update to the latest version of the SQL IaaS Agent Extension, you must restart your virtual machine after updating the extension.</span></span>

> [!NOTE]
> <span data-ttu-id="bc94e-147">Klasik sanal makineleri yükleme ve portal üzerinden SQL Iaas Aracısı uzantısı yapılandırma seçeneği yok.</span><span class="sxs-lookup"><span data-stu-id="bc94e-147">Classic virtual machines do not have an option to install and configure the SQL IaaS Agent Extension through the portal.</span></span>
> 
> 

## <a name="status"></a><span data-ttu-id="bc94e-148">Durum</span><span class="sxs-lookup"><span data-stu-id="bc94e-148">Status</span></span>
<span data-ttu-id="bc94e-149">Uzantı'nin yüklü olduğunu doğrulamak için bir Azure Portalı'nda aracı durumunu görüntülemek için yoludur.</span><span class="sxs-lookup"><span data-stu-id="bc94e-149">One way to verify that the extension is installed is to view the agent status in the Azure Portal.</span></span> <span data-ttu-id="bc94e-150">Sanal makine dikey penceresinde listelenen bir sanal makineyi seçin ve ardından tıklatın **uzantıları**.</span><span class="sxs-lookup"><span data-stu-id="bc94e-150">Select a virtual machine listed in the virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="bc94e-151">Görmeniz gerekir **Sqlıaasagent** listelenen uzantısı.</span><span class="sxs-lookup"><span data-stu-id="bc94e-151">You should see the **SQLIaaSAgent** extension listed.</span></span>

![SQL Server Iaas Aracısı uzantısı Azure portalında](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

<span data-ttu-id="bc94e-153">Aynı zamanda **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bc94e-153">You can also use the **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a><span data-ttu-id="bc94e-154">Temizleme</span><span class="sxs-lookup"><span data-stu-id="bc94e-154">Removal</span></span>
<span data-ttu-id="bc94e-155">Azure Portalı'nda üç nokta işaretine tıklayarak uzantısını kaldırabilirsiniz **uzantıları** dikey penceresinde, sanal makine özellikleri.</span><span class="sxs-lookup"><span data-stu-id="bc94e-155">In the Azure Portal, you can uninstall the extension by clicking the ellipsis on the **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="bc94e-156">Ardından **kaldırma**.</span><span class="sxs-lookup"><span data-stu-id="bc94e-156">Then click **Uninstall**.</span></span>

![Azure Portal'ın SQL Server Iaas Aracısı uzantısını Kaldır](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="bc94e-158">Aynı zamanda **Kaldır AzureVMSqlServerExtension** Powershell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bc94e-158">You can also use the **Remove-AzureVMSqlServerExtension** Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="bc94e-159">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="bc94e-159">Next Steps</span></span>
<span data-ttu-id="bc94e-160">Genişletme tarafından desteklenen hizmetlerinden birini kullanarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="bc94e-160">Begin using one of the services supported by the extension.</span></span> <span data-ttu-id="bc94e-161">Daha fazla ayrıntı için bkz: başvuru konular [desteklenen Hizmetleri](#supported-services) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="bc94e-161">For more details, see the topics referenced in the [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="bc94e-162">SQL Server Azure sanal makinelerde çalıştırma hakkında daha fazla bilgi için bkz: [Azure sanal makinelere genel bakış SQL Server'da](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bc94e-162">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

