---
title: "SQL VM'ler (Resource Manager) aaaAutomate yönetim görevleri | Microsoft Docs"
description: "Bu konuda nasıl toomanage hello belirli SQL Server yönetim görevlerini otomatikleştirir SQL Server Aracısı uzantısı açıklanmaktadır. Bunlar otomatik yedekleme, otomatik düzeltme eki uygulama ve Azure anahtar kasası tümleştirmeyi içerir. Bu konuda hello Resource Manager dağıtım modunu kullanır."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: effe4e2f-35b5-490a-b5ef-b06746083da4
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ae917612c4af59f12c0b083440673bdc555e9d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-resource-manager"></a><span data-ttu-id="fe2f7-105">Merhaba SQL Server Aracısı uzantısı (Resource Manager) ile Azure sanal makineler üzerinde yönetim görevleri otomatik hale getirme</span><span class="sxs-lookup"><span data-stu-id="fe2f7-105">Automate management tasks on Azure Virtual Machines with hello SQL Server Agent Extension (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe2f7-106">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fe2f7-106">Resource Manager</span></span>](virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="fe2f7-107">Klasik</span><span class="sxs-lookup"><span data-stu-id="fe2f7-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
> 

<span data-ttu-id="fe2f7-108">SQL Server Iaas Aracısı uzantısı (SQLIaaSExtension) Hello Azure sanal makineleri tooautomate yönetim görevlerini üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-108">hello SQL Server IaaS Agent Extension (SQLIaaSExtension) runs on Azure virtual machines tooautomate administration tasks.</span></span> <span data-ttu-id="fe2f7-109">Bu konu, yükleme, durum ve kaldırma yönergeleri yanı sıra hello uzantısı tarafından desteklenen hello hizmetlerine genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-109">This topic provides an overview of hello services supported by hello extension as well as instructions for installation, status, and removal.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="fe2f7-110">Bu makalenin tooview hello Klasik sürümü bkz [SQL Server Aracısı uzantısı için SQL Server sanal makineleri Klasik](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="fe2f7-110">tooview hello classic version of this article, see [SQL Server Agent Extension for SQL Server VMs Classic](../classic/sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="fe2f7-111">Desteklenen hizmetler</span><span class="sxs-lookup"><span data-stu-id="fe2f7-111">Supported services</span></span>
<span data-ttu-id="fe2f7-112">SQL Server Iaas Aracısı uzantısı Hello hello aşağıdaki yönetim görevlerini destekler:</span><span class="sxs-lookup"><span data-stu-id="fe2f7-112">hello SQL Server IaaS Agent Extension supports hello following administration tasks:</span></span>

| <span data-ttu-id="fe2f7-113">Yönetim özelliği</span><span class="sxs-lookup"><span data-stu-id="fe2f7-113">Administration feature</span></span> | <span data-ttu-id="fe2f7-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fe2f7-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fe2f7-115">**SQL otomatik yedekleme**</span><span class="sxs-lookup"><span data-stu-id="fe2f7-115">**SQL Automated Backup**</span></span> |<span data-ttu-id="fe2f7-116">Merhaba hello varsayılan SQL Server'ın örneğinde hello VM tüm veritabanları için yedekleme zamanlaması otomatikleştirir.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-116">Automates hello scheduling of backups for all databases for hello default instance of SQL Server in hello VM.</span></span> <span data-ttu-id="fe2f7-117">Daha fazla bilgi için bkz: [Azure Virtual Machines'de (Resource Manager) SQL Server için otomatik yedeklemeyi](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="fe2f7-117">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span></span> |
| <span data-ttu-id="fe2f7-118">**SQL otomatik düzeltme eki uygulama**</span><span class="sxs-lookup"><span data-stu-id="fe2f7-118">**SQL Automated Patching**</span></span> |<span data-ttu-id="fe2f7-119">Güncelleştirmeleri, iş yükü için yoğun saatlerde kaçınmak için bir bakım penceresi sırasında hangi güncelleştirmelerin VM sürebilir tooyour yerleştirin, yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-119">Configures a maintenance window during which updates tooyour VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="fe2f7-120">Daha fazla bilgi için bkz: [otomatik Azure Virtual Machines'de (Resource Manager) SQL Server için düzeltme eki uygulama](virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="fe2f7-120">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span></span> |
| <span data-ttu-id="fe2f7-121">**Azure Anahtar Kasası Tümleştirmesi**</span><span class="sxs-lookup"><span data-stu-id="fe2f7-121">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="fe2f7-122">Tooautomatically yükleme ve SQL Server VM'nize üzerinde Azure anahtar kasası yapılandırma sağlar.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-122">Enables you tooautomatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="fe2f7-123">Daha fazla bilgi için bkz: [(Resource Manager) Azure vm'lerinde SQL Server için Azure anahtar kasası tümleştirmeyi yapılandırmak](virtual-machines-windows-ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="fe2f7-123">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span></span> |

<span data-ttu-id="fe2f7-124">Yüklü ve çalışan sonra hello SQL Server Iaas Aracısı uzantısı bu yönetim özellikleri hello SQL Server panosunda hello sanal makinenin hello Azure portalı ve Azure PowerShell aracılığıyla ve SQL Server Market görüntülerini için kullanılabilmesini sağlar Azure PowerShell hello uzantısı el ile yüklemeleri için.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-124">Once installed and running, hello SQL Server IaaS Agent Extension makes these administration features available on hello SQL Server panel of hello virtual machine in hello Azure Portal and through Azure PowerShell for SQL Server marketplace images, and through Azure PowerShell for manual installations of hello extension.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fe2f7-125">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fe2f7-125">Prerequisites</span></span>
<span data-ttu-id="fe2f7-126">SQL Server Iaas Aracısı uzantısını VM toouse hello gereksinimleri:</span><span class="sxs-lookup"><span data-stu-id="fe2f7-126">Requirements toouse hello SQL Server IaaS Agent Extension on your VM:</span></span>

<span data-ttu-id="fe2f7-127">**İşletim sistemi**:</span><span class="sxs-lookup"><span data-stu-id="fe2f7-127">**Operating System**:</span></span>

* <span data-ttu-id="fe2f7-128">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="fe2f7-128">Windows Server 2012</span></span>
* <span data-ttu-id="fe2f7-129">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="fe2f7-129">Windows Server 2012 R2</span></span>
* <span data-ttu-id="fe2f7-130">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="fe2f7-130">Windows Server 2016</span></span>

<span data-ttu-id="fe2f7-131">**SQL Server sürümleri**:</span><span class="sxs-lookup"><span data-stu-id="fe2f7-131">**SQL Server versions**:</span></span>

* <span data-ttu-id="fe2f7-132">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="fe2f7-132">SQL Server 2012</span></span>
* <span data-ttu-id="fe2f7-133">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="fe2f7-133">SQL Server 2014</span></span>
* <span data-ttu-id="fe2f7-134">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="fe2f7-134">SQL Server 2016</span></span>

<span data-ttu-id="fe2f7-135">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="fe2f7-135">**Azure PowerShell**:</span></span>

* [<span data-ttu-id="fe2f7-136">İndirme ve hello en son Azure PowerShell komutlarının yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fe2f7-136">Download and configure hello latest Azure PowerShell commands</span></span>](/powershell/azure/overview)

## <a name="installation"></a><span data-ttu-id="fe2f7-137">Yükleme</span><span class="sxs-lookup"><span data-stu-id="fe2f7-137">Installation</span></span>
<span data-ttu-id="fe2f7-138">Merhaba SQL Server sanal makineye Galerisi görüntülerden birini sağladığınızda hello SQL Server Iaas Aracısı uzantısı otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-138">hello SQL Server IaaS Agent Extension is automatically installed when you provision one of hello SQL Server virtual machine gallery images.</span></span> <span data-ttu-id="fe2f7-139">Bu SQL Server Vm'lerinin birinde el ile tooreinstall hello uzantısı gerekiyorsa, hello aşağıdaki PowerShell komutunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="fe2f7-139">If you need tooreinstall hello extension manually on one of these SQL Server VMs, use hello following PowerShell command:</span></span>

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

<span data-ttu-id="fe2f7-140">Ayrıca, yalnızca işletim sistemi Windows Server sanal makinede SQL Server Iaas Aracısı uzantısı olası tooinstall hello olur.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-140">It is also possible tooinstall hello SQL Server IaaS Agent Extension on an OS-only Windows Server virtual machine.</span></span> <span data-ttu-id="fe2f7-141">Bu, yalnızca bu makinede de el ile SQL Server yüklediyseniz desteklenir.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-141">This is only supported if you have also manually installed SQL Server on that machine.</span></span> <span data-ttu-id="fe2f7-142">Kullanarak el ile yükleme hello uzantısı hello sonra aynı **kümesi AzureVMSqlServerExtension** PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-142">Then install hello extension manually by using hello same **Set-AzureVMSqlServerExtension** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="fe2f7-143">Bir yalnızca işletim sistemi Windows Server VM üzerinde SQL Server Iaas Aracısı uzantısı hello el ile yüklerseniz, hello SQL Server yapılandırma ayarları hello Azure portal aracılığıyla yönetebilirsiniz değil.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-143">If you manually install hello SQL Server IaaS Agent Extension on an OS-only Windows Server VM, you can not manage hello SQL Server configuration settings through hello Azure portal.</span></span> <span data-ttu-id="fe2f7-144">Bu senaryoda, PowerShell ile tüm değişiklikler yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-144">In this scenario, you must make all changes with PowerShell.</span></span>

## <a name="status"></a><span data-ttu-id="fe2f7-145">Durum</span><span class="sxs-lookup"><span data-stu-id="fe2f7-145">Status</span></span>
<span data-ttu-id="fe2f7-146">Tek yönlü tooverify Hello uzantısı yüklenir tooview hello aracı durumunu hello Azure Portal ' dir.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-146">One way tooverify that hello extension is installed is tooview hello agent status in hello Azure Portal.</span></span> <span data-ttu-id="fe2f7-147">Seçin **tüm ayarları** hello sanal makine dikey ve tıklayın **uzantıları**.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-147">Select **All settings** in hello virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="fe2f7-148">Merhaba görmelisiniz **SQLIaaSExtension** listelenen uzantısı.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-148">You should see hello **SQLIaaSExtension** extension listed.</span></span>

![SQL Server Iaas Aracısı uzantısı Azure portalında](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

<span data-ttu-id="fe2f7-150">Merhaba de kullanabilirsiniz **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-150">You can also use hello **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

<span data-ttu-id="fe2f7-151">Merhaba önceki komutu hello aracısı yüklü olduğundan ve genel durum bilgilerini sağlar onaylar.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-151">hello previous command confirms hello agent is installed and provides general status information.</span></span> <span data-ttu-id="fe2f7-152">Aşağıdaki komutları hello ile otomatik yedekleme ve düzeltme eki ilgili özel durum bilgilerini de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-152">You can also get specific status information about Automated Backup and Patching with hello following commands.</span></span>

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a><span data-ttu-id="fe2f7-153">Temizleme</span><span class="sxs-lookup"><span data-stu-id="fe2f7-153">Removal</span></span>
<span data-ttu-id="fe2f7-154">Hello Azure Portal, hello üzerindeki hello üç nokta düğmesine tıklayarak hello uzantısını kaldırabilirsiniz **uzantıları** dikey penceresinde, sanal makine özellikleri.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-154">In hello Azure Portal, you can uninstall hello extension by clicking hello ellipsis on hello **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="fe2f7-155">Ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-155">Then click **Delete**.</span></span>

![Hello Azure Portalı'nda SQL Server Iaas Aracısı uzantısı kaldırma](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="fe2f7-157">Merhaba de kullanabilirsiniz **Kaldır AzureRmVMSqlServerExtension** Powershell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-157">You can also use hello **Remove-AzureRmVMSqlServerExtension** Powershell cmdlet.</span></span>

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a><span data-ttu-id="fe2f7-158">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="fe2f7-158">Next Steps</span></span>
<span data-ttu-id="fe2f7-159">Merhaba uzantısı tarafından desteklenen hello hizmetlerini birini kullanarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-159">Begin using one of hello services supported by hello extension.</span></span> <span data-ttu-id="fe2f7-160">Daha fazla ayrıntı için bkz: hello başvurulan hello konular [desteklenen Hizmetleri](#supported-services) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="fe2f7-160">For more details, see hello topics referenced in hello [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="fe2f7-161">SQL Server Azure sanal makinelerde çalıştırma hakkında daha fazla bilgi için bkz: [Azure sanal makinelere genel bakış SQL Server'da](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fe2f7-161">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

