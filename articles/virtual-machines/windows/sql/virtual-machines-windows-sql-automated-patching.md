---
title: "Otomatik düzeltme eki uygulama SQL Server Vm'lerinin (Resource Manager) | Microsoft Docs"
description: "Otomatik düzeltme eki uygulama özelliği için SQL Server Kaynak Yöneticisi'ni kullanarak Azure'da çalışan sanal makineler açıklanmıştır."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 58232e92-318f-456b-8f0a-2201a541e08d
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 7d501ab45a85010a8dbfd6135d77f18f1743354e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a><span data-ttu-id="66a30-103">Azure Virtual Machines’de (Resource Manager) SQL Server için Otomatik Düzeltme Eki Uygulama</span><span class="sxs-lookup"><span data-stu-id="66a30-103">Automated Patching for SQL Server in Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="66a30-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="66a30-104">Resource Manager</span></span>](virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="66a30-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="66a30-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="66a30-106">Otomatik düzeltme eki bir Azure SQL Server çalıştıran sanal makine için bir bakım penceresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="66a30-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="66a30-107">Otomatik Güncelleştirmeler, yalnızca bu bakım penceresi sırasında yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="66a30-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="66a30-108">SQL Server için bu rescriction sistem güncelleştirmelerini ve ilişkili tüm yeniden başlatmalar veritabanı için olası en iyi zaman gerçekleşmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="66a30-108">For SQL Server, this rescriction ensures that system updates and any associated restarts occur at the best possible time for the database.</span></span> <span data-ttu-id="66a30-109">Otomatik düzeltme eki bağımlı [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="66a30-109">Automated Patching depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="66a30-110">Bu makalede klasik sürümünü görüntülemek için bkz: [otomatik düzeltme eki uygulama için Azure sanal makineleri Klasik SQL Server'da](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="66a30-110">To view the classic version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Classic](../classic/sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66a30-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="66a30-111">Prerequisites</span></span>
<span data-ttu-id="66a30-112">Otomatik düzeltme eki uygulama kullanmak için aşağıdaki önkoşulları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="66a30-112">To use Automated Patching, consider the following prerequisites:</span></span>

<span data-ttu-id="66a30-113">**İşletim sistemi**:</span><span class="sxs-lookup"><span data-stu-id="66a30-113">**Operating System**:</span></span>

* <span data-ttu-id="66a30-114">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="66a30-114">Windows Server 2012</span></span>
* <span data-ttu-id="66a30-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="66a30-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="66a30-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="66a30-116">Windows Server 2016</span></span>

<span data-ttu-id="66a30-117">**SQL Server sürümü**:</span><span class="sxs-lookup"><span data-stu-id="66a30-117">**SQL Server version**:</span></span>

* <span data-ttu-id="66a30-118">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="66a30-118">SQL Server 2012</span></span>
* <span data-ttu-id="66a30-119">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="66a30-119">SQL Server 2014</span></span>
* <span data-ttu-id="66a30-120">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="66a30-120">SQL Server 2016</span></span>

<span data-ttu-id="66a30-121">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="66a30-121">**Azure PowerShell**:</span></span>

* <span data-ttu-id="66a30-122">[En son Azure PowerShell komutlarını yüklemek](/powershell/azure/overview) otomatik düzeltme eki uygulama PowerShell ile yapılandırmayı planlıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="66a30-122">[Install the latest Azure PowerShell commands](/powershell/azure/overview) if you plan to configure Automated Patching with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="66a30-123">Otomatik düzeltme eki SQL Server Iaas Aracısı uzantısını kullanır.</span><span class="sxs-lookup"><span data-stu-id="66a30-123">Automated Patching relies on the SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="66a30-124">Geçerli SQL sanal makineye Galerisi görüntülerini varsayılan olarak bu uzantı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="66a30-124">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="66a30-125">Daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="66a30-125">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>
> 
> 

## <a name="settings"></a><span data-ttu-id="66a30-126">Ayarlar</span><span class="sxs-lookup"><span data-stu-id="66a30-126">Settings</span></span>
<span data-ttu-id="66a30-127">Aşağıdaki tabloda, otomatik düzeltme eki uygulama için yapılandırılabilir seçenekler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="66a30-127">The following table describes the options that can be configured for Automated Patching.</span></span> <span data-ttu-id="66a30-128">Gerçek yapılandırma adımları Azure portalında veya Azure Windows PowerShell komutlarını kullanmadığınıza bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="66a30-128">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="66a30-129">Ayar</span><span class="sxs-lookup"><span data-stu-id="66a30-129">Setting</span></span> | <span data-ttu-id="66a30-130">Olası değerler</span><span class="sxs-lookup"><span data-stu-id="66a30-130">Possible values</span></span> | <span data-ttu-id="66a30-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="66a30-131">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="66a30-132">**Otomatik Düzeltme Eki Uygulama**</span><span class="sxs-lookup"><span data-stu-id="66a30-132">**Automated Patching**</span></span> |<span data-ttu-id="66a30-133">Etkinleştir/devre dışı bırak (devre dışı)</span><span class="sxs-lookup"><span data-stu-id="66a30-133">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="66a30-134">Etkinleştirir veya bir Azure sanal makine için otomatik düzeltme eki uygulamayı devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="66a30-134">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="66a30-135">**Bakım zamanlaması**</span><span class="sxs-lookup"><span data-stu-id="66a30-135">**Maintenance schedule**</span></span> |<span data-ttu-id="66a30-136">Her gün, Pazartesi, Salı, Çarşamba, Perşembe, Cuma, Cumartesi Pazar</span><span class="sxs-lookup"><span data-stu-id="66a30-136">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="66a30-137">Sanal makineniz için Windows, SQL Server ve Microsoft güncelleştirmeler indiriliyor ve yükleniyor zamanlamasını.</span><span class="sxs-lookup"><span data-stu-id="66a30-137">The schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="66a30-138">**Bakım başlangıç saati**</span><span class="sxs-lookup"><span data-stu-id="66a30-138">**Maintenance start hour**</span></span> |<span data-ttu-id="66a30-139">0-24</span><span class="sxs-lookup"><span data-stu-id="66a30-139">0-24</span></span> |<span data-ttu-id="66a30-140">Sanal makineyi güncelleştirmek için yerel başlangıç saati.</span><span class="sxs-lookup"><span data-stu-id="66a30-140">The local start time to update the virtual machine.</span></span> |
| <span data-ttu-id="66a30-141">**Bakım penceresinin süresi**</span><span class="sxs-lookup"><span data-stu-id="66a30-141">**Maintenance window duration**</span></span> |<span data-ttu-id="66a30-142">30-180</span><span class="sxs-lookup"><span data-stu-id="66a30-142">30-180</span></span> |<span data-ttu-id="66a30-143">İndirme ve güncelleştirmeleri yüklemesini tamamlamak için izin verilen dakika sayısı.</span><span class="sxs-lookup"><span data-stu-id="66a30-143">The number of minutes permitted to complete the download and installation of updates.</span></span> |
| <span data-ttu-id="66a30-144">**Düzeltme eki kategorisi**</span><span class="sxs-lookup"><span data-stu-id="66a30-144">**Patch Category**</span></span> |<span data-ttu-id="66a30-145">Önemli</span><span class="sxs-lookup"><span data-stu-id="66a30-145">Important</span></span> |<span data-ttu-id="66a30-146">Güncelleştirmeleri indirmek ve yüklemek için kategorisi.</span><span class="sxs-lookup"><span data-stu-id="66a30-146">The category of updates to download and install.</span></span> |

## <a name="configuration-in-the-portal"></a><span data-ttu-id="66a30-147">Portal Yapılandırması</span><span class="sxs-lookup"><span data-stu-id="66a30-147">Configuration in the Portal</span></span>
<span data-ttu-id="66a30-148">Otomatik düzeltme eki uygulama sağlama sırasında veya var olan VM'ler için yapılandırmak için Azure portalını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66a30-148">You can use the Azure portal to configure Automated Patching during provisioning or for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="66a30-149">Yeni sanal makineleri</span><span class="sxs-lookup"><span data-stu-id="66a30-149">New VMs</span></span>
<span data-ttu-id="66a30-150">Resource Manager dağıtım modelinde yeni bir SQL Server sanal makine oluşturduğunuzda, otomatik düzeltme eki uygulama yapılandırmak için Azure Portalı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="66a30-150">Use the Azure portal to configure Automated Patching when you create a new SQL Server Virtual Machine in the Resource Manager deployment model.</span></span>

<span data-ttu-id="66a30-151">İçinde **SQL Server ayarları** dikey penceresinde, select **otomatik düzeltme eki uygulama**.</span><span class="sxs-lookup"><span data-stu-id="66a30-151">In the **SQL Server settings** blade, select **Automated patching**.</span></span> <span data-ttu-id="66a30-152">Aşağıdaki Azure portal ekran görüntüsü gösterildiği **SQL otomatik düzeltme eki uygulama** dikey.</span><span class="sxs-lookup"><span data-stu-id="66a30-152">The following Azure portal screenshot shows the **SQL Automated Patching** blade.</span></span>

![SQL otomatik düzeltme eki Azure portalında](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

<span data-ttu-id="66a30-154">Bağlam için tam üzerinde konusuna [azure'da bir SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="66a30-154">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="66a30-155">Var olan sanal makineleri</span><span class="sxs-lookup"><span data-stu-id="66a30-155">Existing VMs</span></span>
<span data-ttu-id="66a30-156">Var olan SQL Server sanal makineler için SQL Server sanal makine seçin.</span><span class="sxs-lookup"><span data-stu-id="66a30-156">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="66a30-157">Ardından **SQL Server yapılandırma** bölümünü **ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="66a30-157">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![SQL otomatik düzeltme eki uygulama var olan VM'ler için](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

<span data-ttu-id="66a30-159">İçinde **SQL Server yapılandırma** dikey penceresinde tıklatın **Düzenle** bölüm düzeltme eki uygulama otomatik düğmesini.</span><span class="sxs-lookup"><span data-stu-id="66a30-159">In the **SQL Server configuration** blade, click the **Edit** button in the Automated patching section.</span></span>

![SQL otomatik düzeltme eki uygulama var olan VM'ler için yapılandırma](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

<span data-ttu-id="66a30-161">Tamamlandığında, tıklatın **Tamam** alt düğmesinde **SQL Server yapılandırma** yaptığınız değişiklikleri kaydetmek için dikey.</span><span class="sxs-lookup"><span data-stu-id="66a30-161">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

<span data-ttu-id="66a30-162">Otomatik düzeltme eki uygulama ilk kez etkinleştiriyorsanız Azure SQL Server Iaas Aracısı arka planda yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="66a30-162">If you are enabling Automated Patching for the first time, Azure configures the SQL Server IaaS Agent in the background.</span></span> <span data-ttu-id="66a30-163">Bu süre boyunca, Azure portalında otomatik düzeltme eki uygulama yapılandırıldığını gösterilmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="66a30-163">During this time, the Azure portal might not show that Automated Patching is configured.</span></span> <span data-ttu-id="66a30-164">Aracının yüklü, yapılandırılmış birkaç dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="66a30-164">Wait several minutes for the agent to be installed, configured.</span></span> <span data-ttu-id="66a30-165">Bundan sonra Azure portalını yeni ayarlarını yansıtır.</span><span class="sxs-lookup"><span data-stu-id="66a30-165">After that the Azure portal reflects the new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="66a30-166">Bir şablon kullanarak otomatik düzeltme eki uygulama da yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66a30-166">You can also configure Automated Patching using a template.</span></span> <span data-ttu-id="66a30-167">Daha fazla bilgi için bkz: [otomatik düzeltme eki uygulama için Azure Hızlı Başlangıç şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span><span class="sxs-lookup"><span data-stu-id="66a30-167">For more information, see [Azure quickstart template for Automated Patching](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span></span>
> 
> 

## <a name="configuration-with-powershell"></a><span data-ttu-id="66a30-168">PowerShell ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="66a30-168">Configuration with PowerShell</span></span>
<span data-ttu-id="66a30-169">SQL VM'nizi sağladıktan sonra otomatik düzeltme eki uygulama yapılandırmak için PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="66a30-169">After provisioning your SQL VM, use PowerShell to configure Automated Patching.</span></span>

<span data-ttu-id="66a30-170">Aşağıdaki örnekte, PowerShell otomatik düzeltme eki uygulama üzerinde mevcut bir SQL Server VM'yi yapılandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="66a30-170">In the following example, PowerShell is used to configure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="66a30-171">**AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig** komut, otomatik güncelleştirmeler için yeni bir bakım penceresi yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="66a30-171">The **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

<span data-ttu-id="66a30-172">Aşağıdaki tabloda, bu örneği temel alarak, hedef Azure VM pratik etkisi açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="66a30-172">Based on this example, the following table describes the practical effect on the target Azure VM:</span></span>

| <span data-ttu-id="66a30-173">Parametre</span><span class="sxs-lookup"><span data-stu-id="66a30-173">Parameter</span></span> | <span data-ttu-id="66a30-174">Etki</span><span class="sxs-lookup"><span data-stu-id="66a30-174">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="66a30-175">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="66a30-175">**DayOfWeek**</span></span> |<span data-ttu-id="66a30-176">Her Perşembe düzeltme ekleri yüklenmemiş.</span><span class="sxs-lookup"><span data-stu-id="66a30-176">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="66a30-177">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="66a30-177">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="66a30-178">Begin 11: 00'da güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="66a30-178">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="66a30-179">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="66a30-179">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="66a30-180">Düzeltme ekleri 120 dakika içinde yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="66a30-180">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="66a30-181">Başlangıç zamanı temel alınarak, 1:00 pm tarafından tamamlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="66a30-181">Based on the start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="66a30-182">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="66a30-182">**PatchCategory**</span></span> |<span data-ttu-id="66a30-183">Bu parametre yalnızca olası ayarı **önemli**.</span><span class="sxs-lookup"><span data-stu-id="66a30-183">The only possible setting for this parameter is **Important**.</span></span> |

<span data-ttu-id="66a30-184">Yüklemek ve SQL Server Iaas aracısı yapılandırmak için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="66a30-184">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="66a30-185">Otomatik düzeltme eki uygulamayı devre dışı bırakmak için olmadan aynı komut dosyasını Çalıştır **-etkinleştirmek** parametresi **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig**.</span><span class="sxs-lookup"><span data-stu-id="66a30-185">To disable Automated Patching, run the same script without the **-Enable** parameter to the **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span></span> <span data-ttu-id="66a30-186">Yokluğu **-etkinleştirmek** parametresi sinyalleri özelliğini devre dışı bırakmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="66a30-186">The absence of the **-Enable** parameter signals the command to disable the feature.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66a30-187">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="66a30-187">Next steps</span></span>
<span data-ttu-id="66a30-188">Diğer kullanılabilir Otomasyon görevler hakkında daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="66a30-188">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="66a30-189">Azure Vm'lerinde SQL Server çalıştırma hakkında daha fazla bilgi için bkz: [Azure sanal makinelere genel bakış SQL Server'da](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="66a30-189">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

