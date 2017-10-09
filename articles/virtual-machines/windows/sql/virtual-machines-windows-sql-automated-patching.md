---
title: "aaaAutomated SQL Server Vm'lerinin (Resource Manager) için düzeltme eki uygulama | Microsoft Docs"
description: "Merhaba otomatik düzeltme eki uygulama özelliği için SQL Server Kaynak Yöneticisi'ni kullanarak Azure'da çalışan sanal makineler açıklanmıştır."
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
ms.openlocfilehash: 8bb8d0fb265e69d7bbf1fa047f5ceef02e7c56fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a><span data-ttu-id="8a2a6-103">Azure Virtual Machines’de (Resource Manager) SQL Server için Otomatik Düzeltme Eki Uygulama</span><span class="sxs-lookup"><span data-stu-id="8a2a6-103">Automated Patching for SQL Server in Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8a2a6-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8a2a6-104">Resource Manager</span></span>](virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="8a2a6-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="8a2a6-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="8a2a6-106">Otomatik düzeltme eki bir Azure SQL Server çalıştıran sanal makine için bir bakım penceresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="8a2a6-107">Otomatik Güncelleştirmeler, yalnızca bu bakım penceresi sırasında yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="8a2a6-108">SQL Server için bu rescriction sistem güncelleştirmelerini ve ilişkili tüm yeniden başlatmalar hello veritabanı için en iyi olası zaman hello gerçekleşmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-108">For SQL Server, this rescriction ensures that system updates and any associated restarts occur at hello best possible time for hello database.</span></span> <span data-ttu-id="8a2a6-109">Otomatik düzeltme eki bağlıdır hello üzerinde [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="8a2a6-109">Automated Patching depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="8a2a6-110">Bu makalenin tooview hello Klasik sürümü bkz [otomatik düzeltme eki uygulama için Azure sanal makineleri Klasik SQL Server'da](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="8a2a6-110">tooview hello classic version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Classic](../classic/sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a2a6-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8a2a6-111">Prerequisites</span></span>
<span data-ttu-id="8a2a6-112">toouse Önkoşullar aşağıdaki hello otomatik düzeltme eki uygulama, göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="8a2a6-112">toouse Automated Patching, consider hello following prerequisites:</span></span>

<span data-ttu-id="8a2a6-113">**İşletim sistemi**:</span><span class="sxs-lookup"><span data-stu-id="8a2a6-113">**Operating System**:</span></span>

* <span data-ttu-id="8a2a6-114">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="8a2a6-114">Windows Server 2012</span></span>
* <span data-ttu-id="8a2a6-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="8a2a6-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="8a2a6-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="8a2a6-116">Windows Server 2016</span></span>

<span data-ttu-id="8a2a6-117">**SQL Server sürümü**:</span><span class="sxs-lookup"><span data-stu-id="8a2a6-117">**SQL Server version**:</span></span>

* <span data-ttu-id="8a2a6-118">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="8a2a6-118">SQL Server 2012</span></span>
* <span data-ttu-id="8a2a6-119">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="8a2a6-119">SQL Server 2014</span></span>
* <span data-ttu-id="8a2a6-120">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="8a2a6-120">SQL Server 2016</span></span>

<span data-ttu-id="8a2a6-121">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="8a2a6-121">**Azure PowerShell**:</span></span>

* <span data-ttu-id="8a2a6-122">[Merhaba en son Azure PowerShell komutlarını yüklemek](/powershell/azure/overview) tooconfigure düşünüyorsanız, otomatik düzeltme eki uygulama PowerShell ile.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-122">[Install hello latest Azure PowerShell commands](/powershell/azure/overview) if you plan tooconfigure Automated Patching with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="8a2a6-123">Otomatik düzeltme eki hello üzerinde SQL Server Iaas Aracısı uzantısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-123">Automated Patching relies on hello SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="8a2a6-124">Geçerli SQL sanal makineye Galerisi görüntülerini varsayılan olarak bu uzantı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-124">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="8a2a6-125">Daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="8a2a6-125">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>
> 
> 

## <a name="settings"></a><span data-ttu-id="8a2a6-126">Ayarlar</span><span class="sxs-lookup"><span data-stu-id="8a2a6-126">Settings</span></span>
<span data-ttu-id="8a2a6-127">Merhaba aşağıdaki tabloda otomatik düzeltme eki uygulama için yapılandırılabilir hello seçenekleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-127">hello following table describes hello options that can be configured for Automated Patching.</span></span> <span data-ttu-id="8a2a6-128">Merhaba gerçek yapılandırma adımlarını hello Azure portalında veya Azure Windows PowerShell komutlarını kullanmadığınıza bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-128">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="8a2a6-129">Ayar</span><span class="sxs-lookup"><span data-stu-id="8a2a6-129">Setting</span></span> | <span data-ttu-id="8a2a6-130">Olası değerler</span><span class="sxs-lookup"><span data-stu-id="8a2a6-130">Possible values</span></span> | <span data-ttu-id="8a2a6-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8a2a6-131">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8a2a6-132">**Otomatik Düzeltme Eki Uygulama**</span><span class="sxs-lookup"><span data-stu-id="8a2a6-132">**Automated Patching**</span></span> |<span data-ttu-id="8a2a6-133">Etkinleştir/devre dışı bırak (devre dışı)</span><span class="sxs-lookup"><span data-stu-id="8a2a6-133">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="8a2a6-134">Etkinleştirir veya bir Azure sanal makine için otomatik düzeltme eki uygulamayı devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-134">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="8a2a6-135">**Bakım zamanlaması**</span><span class="sxs-lookup"><span data-stu-id="8a2a6-135">**Maintenance schedule**</span></span> |<span data-ttu-id="8a2a6-136">Her gün, Pazartesi, Salı, Çarşamba, Perşembe, Cuma, Cumartesi Pazar</span><span class="sxs-lookup"><span data-stu-id="8a2a6-136">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="8a2a6-137">Sanal makineniz için Windows, SQL Server ve Microsoft güncelleştirmeler indiriliyor ve yükleniyor için hello zamanlama.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-137">hello schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="8a2a6-138">**Bakım başlangıç saati**</span><span class="sxs-lookup"><span data-stu-id="8a2a6-138">**Maintenance start hour**</span></span> |<span data-ttu-id="8a2a6-139">0-24</span><span class="sxs-lookup"><span data-stu-id="8a2a6-139">0-24</span></span> |<span data-ttu-id="8a2a6-140">Merhaba yerel başlatma zamanı tooupdate hello sanal makine.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-140">hello local start time tooupdate hello virtual machine.</span></span> |
| <span data-ttu-id="8a2a6-141">**Bakım penceresinin süresi**</span><span class="sxs-lookup"><span data-stu-id="8a2a6-141">**Maintenance window duration**</span></span> |<span data-ttu-id="8a2a6-142">30-180</span><span class="sxs-lookup"><span data-stu-id="8a2a6-142">30-180</span></span> |<span data-ttu-id="8a2a6-143">Merhaba süreyi dakika cinsinden izin verilen toocomplete hello indirme ve güncelleştirmeleri yükleme.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-143">hello number of minutes permitted toocomplete hello download and installation of updates.</span></span> |
| <span data-ttu-id="8a2a6-144">**Düzeltme eki kategorisi**</span><span class="sxs-lookup"><span data-stu-id="8a2a6-144">**Patch Category**</span></span> |<span data-ttu-id="8a2a6-145">Önemli</span><span class="sxs-lookup"><span data-stu-id="8a2a6-145">Important</span></span> |<span data-ttu-id="8a2a6-146">güncelleştirmeleri toodownload ve yükleme Hello kategorisi.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-146">hello category of updates toodownload and install.</span></span> |

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="8a2a6-147">Merhaba Portal Yapılandırması</span><span class="sxs-lookup"><span data-stu-id="8a2a6-147">Configuration in hello Portal</span></span>
<span data-ttu-id="8a2a6-148">Hello Azure portal tooconfigure kullanabileceğiniz otomatik düzeltme eki uygulama sağlama sırasında veya var olan VM'ler için.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-148">You can use hello Azure portal tooconfigure Automated Patching during provisioning or for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="8a2a6-149">Yeni sanal makineleri</span><span class="sxs-lookup"><span data-stu-id="8a2a6-149">New VMs</span></span>
<span data-ttu-id="8a2a6-150">Kullanım hello Azure portal tooconfigure otomatik hello Resource Manager dağıtım modelinde yeni bir SQL Server sanal makine oluşturduğunuzda, düzeltme eki uygulama.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-150">Use hello Azure portal tooconfigure Automated Patching when you create a new SQL Server Virtual Machine in hello Resource Manager deployment model.</span></span>

<span data-ttu-id="8a2a6-151">Merhaba, **SQL Server ayarları** dikey penceresinde, select **otomatik düzeltme eki uygulama**.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-151">In hello **SQL Server settings** blade, select **Automated patching**.</span></span> <span data-ttu-id="8a2a6-152">Merhaba aşağıdaki Azure portal ekran görüntüsü gösterir hello **SQL otomatik düzeltme eki uygulama** dikey.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-152">hello following Azure portal screenshot shows hello **SQL Automated Patching** blade.</span></span>

![SQL otomatik düzeltme eki Azure portalında](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

<span data-ttu-id="8a2a6-154">Bağlam için hello tam üzerinde konusuna [azure'da bir SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="8a2a6-154">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="8a2a6-155">Var olan sanal makineleri</span><span class="sxs-lookup"><span data-stu-id="8a2a6-155">Existing VMs</span></span>
<span data-ttu-id="8a2a6-156">Var olan SQL Server sanal makineler için SQL Server sanal makine seçin.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-156">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="8a2a6-157">Merhaba seçip **SQL Server yapılandırma** hello bölümünü **ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-157">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![SQL otomatik düzeltme eki uygulama var olan VM'ler için](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

<span data-ttu-id="8a2a6-159">Merhaba, **SQL Server yapılandırma** dikey penceresinde hello tıklatın **Düzenle** hello düğmesini otomatik düzeltme eki uygulama bölümü.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-159">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated patching section.</span></span>

![SQL otomatik düzeltme eki uygulama var olan VM'ler için yapılandırma](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

<span data-ttu-id="8a2a6-161">Tamamlandığında, hello tıklatın **Tamam** hello hello alt düğmesinde **SQL Server yapılandırma** dikey toosave değişikliklerinizi.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-161">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="8a2a6-162">Otomatik düzeltme eki uygulama hello için ilk kez etkinleştiriyorsanız, Azure SQL Server Iaas Aracısı hello hello arka planda yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-162">If you are enabling Automated Patching for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="8a2a6-163">Bu süre boyunca, otomatik düzeltme eki uygulama yapılandırıldığını hello Azure portal gösterilmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-163">During this time, hello Azure portal might not show that Automated Patching is configured.</span></span> <span data-ttu-id="8a2a6-164">Merhaba Aracısı toobe yüklü, birkaç dakika bekleyin yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-164">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="8a2a6-165">Bu hello sonra Azure portalı hello yeni ayarlarını yansıtır.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-165">After that hello Azure portal reflects hello new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="8a2a6-166">Bir şablon kullanarak otomatik düzeltme eki uygulama da yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-166">You can also configure Automated Patching using a template.</span></span> <span data-ttu-id="8a2a6-167">Daha fazla bilgi için bkz: [otomatik düzeltme eki uygulama için Azure Hızlı Başlangıç şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span><span class="sxs-lookup"><span data-stu-id="8a2a6-167">For more information, see [Azure quickstart template for Automated Patching](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span></span>
> 
> 

## <a name="configuration-with-powershell"></a><span data-ttu-id="8a2a6-168">PowerShell ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8a2a6-168">Configuration with PowerShell</span></span>
<span data-ttu-id="8a2a6-169">SQL VM'nizi sağladıktan sonra PowerShell tooconfigure kullanın otomatik düzeltme eki uygulama.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-169">After provisioning your SQL VM, use PowerShell tooconfigure Automated Patching.</span></span>

<span data-ttu-id="8a2a6-170">Aşağıdaki örneğine hello kullanılan tooconfigure powershell'dir otomatik düzeltme eki uygulama mevcut bir SQL Server VM üzerinde.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-170">In hello following example, PowerShell is used tooconfigure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="8a2a6-171">Merhaba **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig** komut, otomatik güncelleştirmeler için yeni bir bakım penceresi yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-171">hello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

<span data-ttu-id="8a2a6-172">Bu örneği temel alarak, hello aşağıdaki tabloda hello pratik hello hedef Azure VM etkisi açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="8a2a6-172">Based on this example, hello following table describes hello practical effect on hello target Azure VM:</span></span>

| <span data-ttu-id="8a2a6-173">Parametre</span><span class="sxs-lookup"><span data-stu-id="8a2a6-173">Parameter</span></span> | <span data-ttu-id="8a2a6-174">Etki</span><span class="sxs-lookup"><span data-stu-id="8a2a6-174">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="8a2a6-175">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="8a2a6-175">**DayOfWeek**</span></span> |<span data-ttu-id="8a2a6-176">Her Perşembe düzeltme ekleri yüklenmemiş.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-176">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="8a2a6-177">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="8a2a6-177">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="8a2a6-178">Begin 11: 00'da güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-178">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="8a2a6-179">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="8a2a6-179">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="8a2a6-180">Düzeltme ekleri 120 dakika içinde yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-180">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="8a2a6-181">Merhaba başlangıç zamanı temel alınarak, 1:00 pm tarafından tamamlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-181">Based on hello start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="8a2a6-182">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="8a2a6-182">**PatchCategory**</span></span> |<span data-ttu-id="8a2a6-183">Bu parametre yalnızca olası ayarı hello **önemli**.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-183">hello only possible setting for this parameter is **Important**.</span></span> |

<span data-ttu-id="8a2a6-184">Birkaç dakika tooinstall alın ve hello SQL Server Iaas Aracısı Yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-184">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="8a2a6-185">toodisable otomatik düzeltme eki uygulama, hello aynı komut dosyası çalıştırma hello **-etkinleştirmek** parametresi toohello **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig**.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-185">toodisable Automated Patching, run hello same script without hello **-Enable** parameter toohello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span></span> <span data-ttu-id="8a2a6-186">Merhaba hello yokluğu **-etkinleştirmek** parametresi sinyalleri hello komutu toodisable hello özelliği.</span><span class="sxs-lookup"><span data-stu-id="8a2a6-186">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a2a6-187">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8a2a6-187">Next steps</span></span>
<span data-ttu-id="8a2a6-188">Diğer kullanılabilir Otomasyon görevler hakkında daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="8a2a6-188">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="8a2a6-189">Azure Vm'lerinde SQL Server çalıştırma hakkında daha fazla bilgi için bkz: [Azure sanal makinelere genel bakış SQL Server'da](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8a2a6-189">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

