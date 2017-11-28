---
title: "Otomatik düzeltme eki uygulama SQL Server Vm'lerinin (Klasik) | Microsoft Docs"
description: "Otomatik düzeltme eki uygulama özelliği için SQL Server Klasik dağıtım modunu kullanarak Azure'da çalışan sanal makineler açıklanmıştır."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 737b2f65-08b9-4f54-b867-e987730265a8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 1959871141f196ba80ffd7b37e62e5ea5b42dba3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="761b7-103">Otomatik Azure sanal makinelerde (Klasik) SQL Server için düzeltme eki uygulama</span><span class="sxs-lookup"><span data-stu-id="761b7-103">Automated Patching for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="761b7-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="761b7-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="761b7-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="761b7-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="761b7-106">Otomatik düzeltme eki bir Azure SQL Server çalıştıran sanal makine için bir bakım penceresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="761b7-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="761b7-107">Otomatik Güncelleştirmeler, yalnızca bu bakım penceresi sırasında yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="761b7-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="761b7-108">SQL Server için bu sistem güncelleştirmelerini ve ilişkili tüm yeniden başlatmalar veritabanı için olası en iyi zaman gerçekleşmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="761b7-108">For SQL Server, this ensures that system updates and any associated restarts occur at the best possible time for the database.</span></span> <span data-ttu-id="761b7-109">Otomatik düzeltme eki bağımlı [SQL Server Iaas Aracısı uzantısı](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="761b7-109">Automated Patching depends on the [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="761b7-110">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="761b7-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="761b7-111">Bu makalede, Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="761b7-111">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="761b7-112">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="761b7-112">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="761b7-113">Bu makalede Resource Manager sürümünü görüntülemek için bkz: [otomatik düzeltme eki uygulama SQL Server Azure sanal makineleri Kaynak Yöneticisi'nde](../sql/virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="761b7-113">To view the Resource Manager version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="761b7-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="761b7-114">Prerequisites</span></span>
<span data-ttu-id="761b7-115">Otomatik düzeltme eki uygulama kullanmak için aşağıdaki önkoşulları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="761b7-115">To use Automated Patching, consider the following prerequisites:</span></span>

<span data-ttu-id="761b7-116">**İşletim sistemi**:</span><span class="sxs-lookup"><span data-stu-id="761b7-116">**Operating System**:</span></span>

* <span data-ttu-id="761b7-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="761b7-117">Windows Server 2012</span></span>
* <span data-ttu-id="761b7-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="761b7-118">Windows Server 2012 R2</span></span>
* <span data-ttu-id="761b7-119">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="761b7-119">Windows Server 2016</span></span>

<span data-ttu-id="761b7-120">**SQL Server sürümü**:</span><span class="sxs-lookup"><span data-stu-id="761b7-120">**SQL Server version**:</span></span>

* <span data-ttu-id="761b7-121">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="761b7-121">SQL Server 2012</span></span>
* <span data-ttu-id="761b7-122">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="761b7-122">SQL Server 2014</span></span>
* <span data-ttu-id="761b7-123">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="761b7-123">SQL Server 2016</span></span>

<span data-ttu-id="761b7-124">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="761b7-124">**Azure PowerShell**:</span></span>

* <span data-ttu-id="761b7-125">[En son Azure PowerShell komutlarını yüklemek](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="761b7-125">[Install the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="761b7-126">**SQL Server Iaas uzantısı**:</span><span class="sxs-lookup"><span data-stu-id="761b7-126">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="761b7-127">[SQL Server Iaas uzantısını yükleyin](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="761b7-127">[Install the SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="761b7-128">Ayarlar</span><span class="sxs-lookup"><span data-stu-id="761b7-128">Settings</span></span>
<span data-ttu-id="761b7-129">Aşağıdaki tabloda, otomatik düzeltme eki uygulama için yapılandırılabilir seçenekler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="761b7-129">The following table describes the options that can be configured for Automated Patching.</span></span> <span data-ttu-id="761b7-130">Klasik VM'ler için bu ayarları yapılandırmak için PowerShell kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="761b7-130">For classic VMs, you must use PowerShell to configure these settings.</span></span>

| <span data-ttu-id="761b7-131">Ayar</span><span class="sxs-lookup"><span data-stu-id="761b7-131">Setting</span></span> | <span data-ttu-id="761b7-132">Olası değerler</span><span class="sxs-lookup"><span data-stu-id="761b7-132">Possible values</span></span> | <span data-ttu-id="761b7-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="761b7-133">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="761b7-134">**Otomatik Düzeltme Eki Uygulama**</span><span class="sxs-lookup"><span data-stu-id="761b7-134">**Automated Patching**</span></span> |<span data-ttu-id="761b7-135">Etkinleştir/devre dışı bırak (devre dışı)</span><span class="sxs-lookup"><span data-stu-id="761b7-135">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="761b7-136">Etkinleştirir veya bir Azure sanal makine için otomatik düzeltme eki uygulamayı devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="761b7-136">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="761b7-137">**Bakım zamanlaması**</span><span class="sxs-lookup"><span data-stu-id="761b7-137">**Maintenance schedule**</span></span> |<span data-ttu-id="761b7-138">Her gün, Pazartesi, Salı, Çarşamba, Perşembe, Cuma, Cumartesi Pazar</span><span class="sxs-lookup"><span data-stu-id="761b7-138">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="761b7-139">Sanal makineniz için Windows, SQL Server ve Microsoft güncelleştirmeler indiriliyor ve yükleniyor zamanlamasını.</span><span class="sxs-lookup"><span data-stu-id="761b7-139">The schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="761b7-140">**Bakım başlangıç saati**</span><span class="sxs-lookup"><span data-stu-id="761b7-140">**Maintenance start hour**</span></span> |<span data-ttu-id="761b7-141">0-24</span><span class="sxs-lookup"><span data-stu-id="761b7-141">0-24</span></span> |<span data-ttu-id="761b7-142">Sanal makineyi güncelleştirmek için yerel başlangıç saati.</span><span class="sxs-lookup"><span data-stu-id="761b7-142">The local start time to update the virtual machine.</span></span> |
| <span data-ttu-id="761b7-143">**Bakım penceresinin süresi**</span><span class="sxs-lookup"><span data-stu-id="761b7-143">**Maintenance window duration**</span></span> |<span data-ttu-id="761b7-144">30-180</span><span class="sxs-lookup"><span data-stu-id="761b7-144">30-180</span></span> |<span data-ttu-id="761b7-145">İndirme ve güncelleştirmeleri yüklemesini tamamlamak için izin verilen dakika sayısı.</span><span class="sxs-lookup"><span data-stu-id="761b7-145">The number of minutes permitted to complete the download and installation of updates.</span></span> |
| <span data-ttu-id="761b7-146">**Düzeltme eki kategorisi**</span><span class="sxs-lookup"><span data-stu-id="761b7-146">**Patch Category**</span></span> |<span data-ttu-id="761b7-147">Önemli</span><span class="sxs-lookup"><span data-stu-id="761b7-147">Important</span></span> |<span data-ttu-id="761b7-148">Güncelleştirmeleri indirmek ve yüklemek için kategorisi.</span><span class="sxs-lookup"><span data-stu-id="761b7-148">The category of updates to download and install.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="761b7-149">PowerShell ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="761b7-149">Configuration with PowerShell</span></span>
<span data-ttu-id="761b7-150">Aşağıdaki örnekte, PowerShell otomatik düzeltme eki uygulama üzerinde mevcut bir SQL Server VM'yi yapılandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="761b7-150">In the following example, PowerShell is used to configure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="761b7-151">**Yeni AzureVMSqlServerAutoPatchingConfig** komut, otomatik güncelleştirmeler için yeni bir bakım penceresi yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="761b7-151">The **New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

<span data-ttu-id="761b7-152">Aşağıdaki tabloda, bu örneği temel alarak, hedef Azure VM pratik etkisi açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="761b7-152">Based on this example, the following table describes the practical effect on the target Azure VM:</span></span>

| <span data-ttu-id="761b7-153">Parametre</span><span class="sxs-lookup"><span data-stu-id="761b7-153">Parameter</span></span> | <span data-ttu-id="761b7-154">Etki</span><span class="sxs-lookup"><span data-stu-id="761b7-154">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="761b7-155">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="761b7-155">**DayOfWeek**</span></span> |<span data-ttu-id="761b7-156">Her Perşembe düzeltme ekleri yüklenmemiş.</span><span class="sxs-lookup"><span data-stu-id="761b7-156">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="761b7-157">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="761b7-157">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="761b7-158">Begin 11: 00'da güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="761b7-158">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="761b7-159">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="761b7-159">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="761b7-160">Düzeltme ekleri 120 dakika içinde yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="761b7-160">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="761b7-161">Başlangıç zamanı temel alınarak, 1:00 pm tarafından tamamlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="761b7-161">Based on the start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="761b7-162">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="761b7-162">**PatchCategory**</span></span> |<span data-ttu-id="761b7-163">Bu parametre için yalnızca olası ayar "Önemli" dir.</span><span class="sxs-lookup"><span data-stu-id="761b7-163">The only possible setting for this parameter is “Important”.</span></span> |

<span data-ttu-id="761b7-164">Yüklemek ve SQL Server Iaas aracısı yapılandırmak için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="761b7-164">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="761b7-165">Otomatik düzeltme eki uygulamayı devre dışı bırakmak için aynı Çalıştır komut dosyası yeni AzureVMSqlServerAutoPatchingConfig Enable parametresi olmadan.</span><span class="sxs-lookup"><span data-stu-id="761b7-165">To disable Automated Patching, run the same script without the -Enable parameter to the New-AzureVMSqlServerAutoPatchingConfig.</span></span> <span data-ttu-id="761b7-166">Yüklemesiyle olduğu gibi otomatik düzeltme eki uygulamayı devre dışı bırakmak için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="761b7-166">As with installation, it can take several minutes to disable Automated Patching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="761b7-167">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="761b7-167">Next steps</span></span>
<span data-ttu-id="761b7-168">Diğer kullanılabilir Otomasyon görevler hakkında daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="761b7-168">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="761b7-169">Azure Vm'lerinde SQL Server çalıştırma hakkında daha fazla bilgi için bkz: [Azure sanal makinelere genel bakış SQL Server'da](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="761b7-169">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

