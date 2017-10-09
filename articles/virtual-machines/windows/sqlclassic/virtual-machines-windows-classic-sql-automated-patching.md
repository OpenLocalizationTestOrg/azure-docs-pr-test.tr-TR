---
title: "aaaAutomated SQL Server Vm'lerinin (Klasik) için düzeltme eki uygulama | Microsoft Docs"
description: "Merhaba otomatik düzeltme eki uygulama özelliği için SQL Server hello Klasik dağıtım modunu kullanarak Azure'da çalışan sanal makineler açıklanmıştır."
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
ms.openlocfilehash: 2ef06b95705fc457605d6eb2fbc0afd490321843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="66171-103">Otomatik Azure sanal makinelerde (Klasik) SQL Server için düzeltme eki uygulama</span><span class="sxs-lookup"><span data-stu-id="66171-103">Automated Patching for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="66171-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="66171-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="66171-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="66171-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="66171-106">Otomatik düzeltme eki bir Azure SQL Server çalıştıran sanal makine için bir bakım penceresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="66171-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="66171-107">Otomatik Güncelleştirmeler, yalnızca bu bakım penceresi sırasında yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="66171-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="66171-108">SQL Server için bu sistem güncelleştirmelerini ve ilişkili tüm yeniden başlatmalar hello veritabanı için en iyi olası zaman hello gerçekleşmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="66171-108">For SQL Server, this ensures that system updates and any associated restarts occur at hello best possible time for hello database.</span></span> <span data-ttu-id="66171-109">Otomatik düzeltme eki bağlıdır hello üzerinde [SQL Server Iaas Aracısı uzantısı](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="66171-109">Automated Patching depends on hello [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="66171-110">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="66171-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="66171-111">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="66171-111">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="66171-112">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="66171-112">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="66171-113">Bu makalenin tooview hello Resource Manager sürümü bkz [otomatik düzeltme eki uygulama SQL Server Azure sanal makineleri Kaynak Yöneticisi'nde](../sql/virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="66171-113">tooview hello Resource Manager version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66171-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="66171-114">Prerequisites</span></span>
<span data-ttu-id="66171-115">toouse Önkoşullar aşağıdaki hello otomatik düzeltme eki uygulama, göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="66171-115">toouse Automated Patching, consider hello following prerequisites:</span></span>

<span data-ttu-id="66171-116">**İşletim sistemi**:</span><span class="sxs-lookup"><span data-stu-id="66171-116">**Operating System**:</span></span>

* <span data-ttu-id="66171-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="66171-117">Windows Server 2012</span></span>
* <span data-ttu-id="66171-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="66171-118">Windows Server 2012 R2</span></span>
* <span data-ttu-id="66171-119">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="66171-119">Windows Server 2016</span></span>

<span data-ttu-id="66171-120">**SQL Server sürümü**:</span><span class="sxs-lookup"><span data-stu-id="66171-120">**SQL Server version**:</span></span>

* <span data-ttu-id="66171-121">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="66171-121">SQL Server 2012</span></span>
* <span data-ttu-id="66171-122">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="66171-122">SQL Server 2014</span></span>
* <span data-ttu-id="66171-123">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="66171-123">SQL Server 2016</span></span>

<span data-ttu-id="66171-124">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="66171-124">**Azure PowerShell**:</span></span>

* <span data-ttu-id="66171-125">[Merhaba en son Azure PowerShell komutlarını yüklemek](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="66171-125">[Install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="66171-126">**SQL Server Iaas uzantısı**:</span><span class="sxs-lookup"><span data-stu-id="66171-126">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="66171-127">[SQL Server Iaas uzantısı Hello yüklemek](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="66171-127">[Install hello SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="66171-128">Ayarlar</span><span class="sxs-lookup"><span data-stu-id="66171-128">Settings</span></span>
<span data-ttu-id="66171-129">Merhaba aşağıdaki tabloda otomatik düzeltme eki uygulama için yapılandırılabilir hello seçenekleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="66171-129">hello following table describes hello options that can be configured for Automated Patching.</span></span> <span data-ttu-id="66171-130">Klasik VM'ler için bu ayarları PowerShell tooconfigure kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="66171-130">For classic VMs, you must use PowerShell tooconfigure these settings.</span></span>

| <span data-ttu-id="66171-131">Ayar</span><span class="sxs-lookup"><span data-stu-id="66171-131">Setting</span></span> | <span data-ttu-id="66171-132">Olası değerler</span><span class="sxs-lookup"><span data-stu-id="66171-132">Possible values</span></span> | <span data-ttu-id="66171-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="66171-133">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="66171-134">**Otomatik Düzeltme Eki Uygulama**</span><span class="sxs-lookup"><span data-stu-id="66171-134">**Automated Patching**</span></span> |<span data-ttu-id="66171-135">Etkinleştir/devre dışı bırak (devre dışı)</span><span class="sxs-lookup"><span data-stu-id="66171-135">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="66171-136">Etkinleştirir veya bir Azure sanal makine için otomatik düzeltme eki uygulamayı devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="66171-136">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="66171-137">**Bakım zamanlaması**</span><span class="sxs-lookup"><span data-stu-id="66171-137">**Maintenance schedule**</span></span> |<span data-ttu-id="66171-138">Her gün, Pazartesi, Salı, Çarşamba, Perşembe, Cuma, Cumartesi Pazar</span><span class="sxs-lookup"><span data-stu-id="66171-138">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="66171-139">Sanal makineniz için Windows, SQL Server ve Microsoft güncelleştirmeler indiriliyor ve yükleniyor için hello zamanlama.</span><span class="sxs-lookup"><span data-stu-id="66171-139">hello schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="66171-140">**Bakım başlangıç saati**</span><span class="sxs-lookup"><span data-stu-id="66171-140">**Maintenance start hour**</span></span> |<span data-ttu-id="66171-141">0-24</span><span class="sxs-lookup"><span data-stu-id="66171-141">0-24</span></span> |<span data-ttu-id="66171-142">Merhaba yerel başlatma zamanı tooupdate hello sanal makine.</span><span class="sxs-lookup"><span data-stu-id="66171-142">hello local start time tooupdate hello virtual machine.</span></span> |
| <span data-ttu-id="66171-143">**Bakım penceresinin süresi**</span><span class="sxs-lookup"><span data-stu-id="66171-143">**Maintenance window duration**</span></span> |<span data-ttu-id="66171-144">30-180</span><span class="sxs-lookup"><span data-stu-id="66171-144">30-180</span></span> |<span data-ttu-id="66171-145">Merhaba süreyi dakika cinsinden izin verilen toocomplete hello indirme ve güncelleştirmeleri yükleme.</span><span class="sxs-lookup"><span data-stu-id="66171-145">hello number of minutes permitted toocomplete hello download and installation of updates.</span></span> |
| <span data-ttu-id="66171-146">**Düzeltme eki kategorisi**</span><span class="sxs-lookup"><span data-stu-id="66171-146">**Patch Category**</span></span> |<span data-ttu-id="66171-147">Önemli</span><span class="sxs-lookup"><span data-stu-id="66171-147">Important</span></span> |<span data-ttu-id="66171-148">güncelleştirmeleri toodownload ve yükleme Hello kategorisi.</span><span class="sxs-lookup"><span data-stu-id="66171-148">hello category of updates toodownload and install.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="66171-149">PowerShell ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="66171-149">Configuration with PowerShell</span></span>
<span data-ttu-id="66171-150">Aşağıdaki örneğine hello kullanılan tooconfigure powershell'dir otomatik düzeltme eki uygulama mevcut bir SQL Server VM üzerinde.</span><span class="sxs-lookup"><span data-stu-id="66171-150">In hello following example, PowerShell is used tooconfigure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="66171-151">Merhaba **yeni AzureVMSqlServerAutoPatchingConfig** komut, otomatik güncelleştirmeler için yeni bir bakım penceresi yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="66171-151">hello **New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

<span data-ttu-id="66171-152">Bu örneği temel alarak, hello aşağıdaki tabloda hello pratik hello hedef Azure VM etkisi açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="66171-152">Based on this example, hello following table describes hello practical effect on hello target Azure VM:</span></span>

| <span data-ttu-id="66171-153">Parametre</span><span class="sxs-lookup"><span data-stu-id="66171-153">Parameter</span></span> | <span data-ttu-id="66171-154">Etki</span><span class="sxs-lookup"><span data-stu-id="66171-154">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="66171-155">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="66171-155">**DayOfWeek**</span></span> |<span data-ttu-id="66171-156">Her Perşembe düzeltme ekleri yüklenmemiş.</span><span class="sxs-lookup"><span data-stu-id="66171-156">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="66171-157">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="66171-157">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="66171-158">Begin 11: 00'da güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="66171-158">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="66171-159">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="66171-159">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="66171-160">Düzeltme ekleri 120 dakika içinde yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="66171-160">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="66171-161">Merhaba başlangıç zamanı temel alınarak, 1:00 pm tarafından tamamlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="66171-161">Based on hello start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="66171-162">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="66171-162">**PatchCategory**</span></span> |<span data-ttu-id="66171-163">Merhaba yalnızca olası için bu parametreyi "Önemli" ayardır.</span><span class="sxs-lookup"><span data-stu-id="66171-163">hello only possible setting for this parameter is “Important”.</span></span> |

<span data-ttu-id="66171-164">Birkaç dakika tooinstall alın ve hello SQL Server Iaas Aracısı Yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="66171-164">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="66171-165">toodisable otomatik düzeltme eki uygulama, aynı komut dosyası olmadan çalıştırma hello hello - Enable parametresini toohello yeni AzureVMSqlServerAutoPatchingConfig.</span><span class="sxs-lookup"><span data-stu-id="66171-165">toodisable Automated Patching, run hello same script without hello -Enable parameter toohello New-AzureVMSqlServerAutoPatchingConfig.</span></span> <span data-ttu-id="66171-166">Yükleme ile birkaç dakika toodisable sürebilir gibi otomatik düzeltme eki uygulama.</span><span class="sxs-lookup"><span data-stu-id="66171-166">As with installation, it can take several minutes toodisable Automated Patching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66171-167">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="66171-167">Next steps</span></span>
<span data-ttu-id="66171-168">Diğer kullanılabilir Otomasyon görevler hakkında daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="66171-168">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="66171-169">Azure Vm'lerinde SQL Server çalıştırma hakkında daha fazla bilgi için bkz: [Azure sanal makinelere genel bakış SQL Server'da](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="66171-169">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

