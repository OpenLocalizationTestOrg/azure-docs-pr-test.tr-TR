---
title: aaaManage Azure PowerShell kullanarak sanal makinelerinizin | Microsoft Docs
description: "Sanal makinelerinizi yönetme tooautomate görevleri kullanabileceğiniz komutlar hakkında bilgi edinin."
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: e4ca6f098519243a321eac98b6692790fe18c22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a><span data-ttu-id="dd15c-103">Azure PowerShell kullanarak sanal makinelerinizi yönetme</span><span class="sxs-lookup"><span data-stu-id="dd15c-103">Manage your virtual machines by using Azure PowerShell</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="dd15c-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="dd15c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="dd15c-105">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="dd15c-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="dd15c-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="dd15c-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="dd15c-107">Merhaba Resource Manager modelini kullanarak ortak PowerShell komutları için bkz: [burada](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd15c-107">For common PowerShell commands using hello Resource Manager model, see [here](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="dd15c-108">Birçok görevi her gün toomanage Vm'leriniz bunu Azure PowerShell cmdlet'lerini kullanarak otomatik olarak.</span><span class="sxs-lookup"><span data-stu-id="dd15c-108">Many tasks you do each day toomanage your VMs can be automated by using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="dd15c-109">Bu makalede daha basit görevler ve daha karmaşık görevleri için hello komutları göster bağlantılar tooarticles için örnek komutlar verir.</span><span class="sxs-lookup"><span data-stu-id="dd15c-109">This article gives you example commands for simpler tasks, and links tooarticles that show hello commands for more complex tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="dd15c-110">Azure PowerShell'i yükleyip henüz henüz hello makaledeki yönergeleri alabilir, [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dd15c-110">If you haven't installed and configured Azure PowerShell yet, you can get instructions in hello article [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
> 
> 

## <a name="how-toouse-hello-example-commands"></a><span data-ttu-id="dd15c-111">Nasıl toouse hello örnek komutları</span><span class="sxs-lookup"><span data-stu-id="dd15c-111">How toouse hello example commands</span></span>
<span data-ttu-id="dd15c-112">Merhaba hello metinde bazıları komutları ortamınız için uygun metinle tooreplace gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd15c-112">You'll need tooreplace some of hello text in hello commands with text that's appropriate for your environment.</span></span> <span data-ttu-id="dd15c-113">Merhaba < ve > sembolleri tooreplace gereksinim metin gösterir.</span><span class="sxs-lookup"><span data-stu-id="dd15c-113">hello < and > symbols indicate text you need tooreplace.</span></span> <span data-ttu-id="dd15c-114">Merhaba metin değiştirdiğinizde hello simgeleri Kaldır ancak hello tırnak işaretleri bırakın.</span><span class="sxs-lookup"><span data-stu-id="dd15c-114">When you replace hello text, remove hello symbols but leave hello quote marks in place.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="dd15c-115">VM Al</span><span class="sxs-lookup"><span data-stu-id="dd15c-115">Get a VM</span></span>
<span data-ttu-id="dd15c-116">Bu, genellikle kullanacağınız temel bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="dd15c-116">This is a basic task you'll use often.</span></span> <span data-ttu-id="dd15c-117">VM tooget bilgilerini kullanmak, bir VM görevler gerçekleştiren veya çıktı toostore bir değişkende alın.</span><span class="sxs-lookup"><span data-stu-id="dd15c-117">Use it tooget information about a VM, perform tasks on a VM, or get output toostore in a variable.</span></span>

<span data-ttu-id="dd15c-118">Merhaba VM tooget bilgilerini hello tırnak merhaba < ve > karakterleri dahil olmak üzere, her şeyi değiştirerek bu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="dd15c-118">tooget information about hello VM, run this command, replacing everything in hello quotes, including hello < and > characters:</span></span>

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

<span data-ttu-id="dd15c-119">bir $vm değişkende çıktı toostore hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="dd15c-119">toostore hello output in a $vm variable, run:</span></span>

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a><span data-ttu-id="dd15c-120">Windows tabanlı VM üzerinde tooa oturum</span><span class="sxs-lookup"><span data-stu-id="dd15c-120">Log on tooa Windows-based VM</span></span>
<span data-ttu-id="dd15c-121">Şu komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="dd15c-121">Run these commands:</span></span>

> [!NOTE]
> <span data-ttu-id="dd15c-122">Merhaba hello görüntüden hello sanal makine ve bulut hizmeti adı alabilirsiniz **Get-AzureVM** komutu.</span><span class="sxs-lookup"><span data-stu-id="dd15c-122">You can get hello virtual machine and cloud service name from hello display of hello **Get-AzureVM** command.</span></span>
> 
> <span data-ttu-id="dd15c-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "< sürücü ve klasör konumu toostore indirilen hello RDP dosyası, örneğin: c:\temp >" $localFile $localPath = + "\" $vmname +".rdp"Get-AzureRemoteDesktopFile - ServiceName $svcName-$vmName - LocalPath $localFile ad-Başlat</span><span class="sxs-lookup"><span data-stu-id="dd15c-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<drive and folder location toostore hello downloaded RDP file, example: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span></span>
> 
> 

## <a name="stop-a-vm"></a><span data-ttu-id="dd15c-124">VM durdurma</span><span class="sxs-lookup"><span data-stu-id="dd15c-124">Stop a VM</span></span>
<span data-ttu-id="dd15c-125">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="dd15c-125">Run this command:</span></span>

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> <span data-ttu-id="dd15c-126">Sanal IP (VIP) hello bulut hizmeti olduğu durumda bu parametre tookeep hello kullanmak son VM bu bulut hizmeti ile Merhaba.</span><span class="sxs-lookup"><span data-stu-id="dd15c-126">Use this parameter tookeep hello virtual IP (VIP) of hello cloud service in case it's hello last VM in that cloud service.</span></span> <br><br> <span data-ttu-id="dd15c-127">Merhaba StayProvisioned parametreyi kullanırsanız, VM hello için fatura.</span><span class="sxs-lookup"><span data-stu-id="dd15c-127">If you use hello StayProvisioned parameter, you'll still be billed for hello VM.</span></span>
> 
> 

## <a name="start-a-vm"></a><span data-ttu-id="dd15c-128">VM başlatma</span><span class="sxs-lookup"><span data-stu-id="dd15c-128">Start a VM</span></span>
<span data-ttu-id="dd15c-129">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="dd15c-129">Run this command:</span></span>

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a><span data-ttu-id="dd15c-130">Veri diski ekleme</span><span class="sxs-lookup"><span data-stu-id="dd15c-130">Attach a data disk</span></span>
<span data-ttu-id="dd15c-131">Bu görev birkaç adımı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="dd15c-131">This task requires a few steps.</span></span> <span data-ttu-id="dd15c-132">Merhaba ilk olarak, kullandığınız *** Ekle-AzureDataDisk *** cmdlet tooadd hello disk toohello $vm nesnesi.</span><span class="sxs-lookup"><span data-stu-id="dd15c-132">First, you use hello ****Add-AzureDataDisk**** cmdlet tooadd hello disk toohello $vm object.</span></span> <span data-ttu-id="dd15c-133">Ardından, kullandığınız **güncelleştirme-AzureVM** hello VM cmdlet tooupdate hello yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="dd15c-133">Then, you use **Update-AzureVM** cmdlet tooupdate hello configuration of hello VM.</span></span>

<span data-ttu-id="dd15c-134">Ayrıca tooattach yeni bir disk veya bir içeren olup olmadığını toodecide gerekir veri.</span><span class="sxs-lookup"><span data-stu-id="dd15c-134">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="dd15c-135">Yeni bir disk için hello komut hello .vhd dosyası oluşturur ve bunları ekler.</span><span class="sxs-lookup"><span data-stu-id="dd15c-135">For a new disk, hello command creates hello .vhd file and attaches it.</span></span>

<span data-ttu-id="dd15c-136">Yeni bir disk tooattach bu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="dd15c-136">tooattach a new disk, run this command:</span></span>

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

<span data-ttu-id="dd15c-137">Varolan bir veri diski tooattach bu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="dd15c-137">tooattach an existing data disk, run this command:</span></span>

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

<span data-ttu-id="dd15c-138">var olan .vhd dosyasına blob storage'da tooattach veri disklerinden bu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="dd15c-138">tooattach data disks from an existing .vhd file in blob storage, run this command:</span></span>

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a><span data-ttu-id="dd15c-139">Windows tabanlı bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd15c-139">Create a Windows-based VM</span></span>
<span data-ttu-id="dd15c-140">toocreate yeni bir Windows tabanlı sanal makine azure'da kullanım hello yönergeleri [Azure PowerShell kullanma toocreate ve Windows tabanlı sanal makineleri önceden](create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="dd15c-140">toocreate a new Windows-based virtual machine in Azure, use hello instructions in [Use Azure PowerShell toocreate and preconfigure Windows-based virtual machines](create-powershell.md).</span></span> <span data-ttu-id="dd15c-141">Bu konuda adım adım komut kümesi bir Azure PowerShell hello oluşturulmasını size önceden yapılandırılabilir Windows tabanlı bir VM oluşturur:</span><span class="sxs-lookup"><span data-stu-id="dd15c-141">This topic steps you through hello creation of an Azure PowerShell command set that creates a Windows-based VM that can be preconfigured:</span></span>

* <span data-ttu-id="dd15c-142">Active Directory etki alanı üyeliği ile.</span><span class="sxs-lookup"><span data-stu-id="dd15c-142">With Active Directory domain membership.</span></span>
* <span data-ttu-id="dd15c-143">Ek disklerle.</span><span class="sxs-lookup"><span data-stu-id="dd15c-143">With additional disks.</span></span>
* <span data-ttu-id="dd15c-144">Varolan yük dengeli bir üye olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="dd15c-144">As a member of an existing load-balanced set.</span></span>
* <span data-ttu-id="dd15c-145">Statik bir IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="dd15c-145">With a static IP address.</span></span>

