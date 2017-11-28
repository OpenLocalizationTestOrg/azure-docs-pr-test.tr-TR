---
title: Windows Azure PowerShell ile VM sorun giderme bir aaaUse | Microsoft Docs
description: "Merhaba işletim sistemi disk tooa kurtarma Azure PowerShell kullanarak bir VM bağlanarak tootroubleshoot Windows VM Azure'da nasıl sorunları öğrenin"
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 7a6a76f64824fe5d06dc4286cb1d87ab8bb794e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-azure-powershell"></a><span data-ttu-id="ac2e3-103">Bir Windows VM hello işletim sistemi disk tooa kurtarma Azure PowerShell kullanarak bir VM ekleyerek sorun giderme</span><span class="sxs-lookup"><span data-stu-id="ac2e3-103">Troubleshoot a Windows VM by attaching hello OS disk tooa recovery VM using Azure PowerShell</span></span>
<span data-ttu-id="ac2e3-104">Azure, Windows sanal makine (VM) önyükleme veya disk bir hatayla karşılaştığında, sorun giderme adımları hello sanal sabit diske kendisini tooperform gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="ac2e3-105">Yaygın bir örnek hello VM mümkün tooboot başarıyla engeller başarısız uygulama güncelleştirmesi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-105">A common example would be a failed application update that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="ac2e3-106">Bu makale ayrıntıları nasıl toouse Azure PowerShell tooconnect, sanal sabit disk tooanother Windows VM toofix herhangi bir hata sonra özgün VM'yi yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-106">This article details how toouse Azure PowerShell tooconnect your virtual hard disk tooanother Windows VM toofix any errors, then re-create your original VM.</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="ac2e3-107">Kurtarma işlemine genel bakış</span><span class="sxs-lookup"><span data-stu-id="ac2e3-107">Recovery process overview</span></span>
<span data-ttu-id="ac2e3-108">sorun giderme işlemi hello aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="ac2e3-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="ac2e3-109">Merhaba sanal sabit diskleri tutmak hello VM karşılaşmadan sorunları, silin.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="ac2e3-110">Ekleme ve sorun giderme amacıyla hello sanal sabit disk tooanother Windows VM bağlayın.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-110">Attach and mount hello virtual hard disk tooanother Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="ac2e3-111">VM sorun giderme toohello bağlayın.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="ac2e3-112">Dosyaları düzenleyin veya herhangi bir aracı toofix sorunları hello özgün sanal sabit disk üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="ac2e3-113">Çıkarın ve VM sorun giderme hello hello sanal sabit diski kullanımdan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="ac2e3-114">Merhaba özgün sanal sabit disk kullanan bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-114">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="ac2e3-115">Bilgisayarınızda yüklü olduğundan emin olun [en son Azure PowerShell hello](/powershell/azure/overview) yüklü ve tooyour abonelikte oturum:</span><span class="sxs-lookup"><span data-stu-id="ac2e3-115">Make sure that you have [hello latest Azure PowerShell](/powershell/azure/overview) installed and logged in tooyour subscription:</span></span>

```powershell
Login-AzureRMAccount
```

<span data-ttu-id="ac2e3-116">Hello aşağıdaki örneklerde, parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-116">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="ac2e3-117">Örnek parametre adlarında `myResourceGroup`, `mystorageaccount`, ve `myVM`.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-117">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="ac2e3-118">Önyükleme sorunlarını belirleme</span><span class="sxs-lookup"><span data-stu-id="ac2e3-118">Determine boot issues</span></span>
<span data-ttu-id="ac2e3-119">Azure üzerinde bir ekran görüntüsü, VM görüntüleyebilirsiniz toohelp önyükleme sorunlarını giderme.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-119">You can view a screenshot of your VM in Azure toohelp troubleshoot boot issues.</span></span> <span data-ttu-id="ac2e3-120">Bu ekran, bir VM tooboot başarısız neden tanımlamaya yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-120">This screenshot can help identify why a VM fails tooboot.</span></span> <span data-ttu-id="ac2e3-121">Merhaba aşağıdaki örnek hello ekran Windows adlı VM hello alır `myVM` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ac2e3-121">hello following example gets hello screenshot from hello Windows VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

<span data-ttu-id="ac2e3-122">Merhaba VM tooboot neden başarısız hello ekran toodetermine gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-122">Review hello screenshot toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="ac2e3-123">Herhangi bir özel hata iletileri veya sağlanan hata kodları unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-123">Note any specific error messages or error codes provided.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="ac2e3-124">Var olan sanal sabit disk ayrıntılarını görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="ac2e3-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="ac2e3-125">Sanal sabit disk tooanother VM ekleyebilmek için tooidentify hello adı hello sanal sabit disk (VHD) gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span>

<span data-ttu-id="ac2e3-126">Merhaba aşağıdaki örnek alır bilgi hello adlı VM için `myVM` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ac2e3-126">hello following example gets information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="ac2e3-127">Ara `Vhd URI` hello içinde `StorageProfile` komutu önceki hello hello çıktısından bölümü.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-127">Look for `Vhd URI` within hello `StorageProfile` section from hello output of hello preceding command.</span></span> <span data-ttu-id="ac2e3-128">Merhaba aşağıdaki kesilmiş örnek çıkış gösterir hello `Vhd URI` hello kod bloğu hello sonuna doğru:</span><span class="sxs-lookup"><span data-stu-id="ac2e3-128">hello following truncated example output shows hello `Vhd URI` towards hello end of hello code block:</span></span>

```powershell
RequestId                     : 8a134642-2f01-4e08-bb12-d89b5b81a0a0
StatusCode                    : OK
ResourceGroupName             : myResourceGroup
Id                            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM
Name                          : myVM
Type                          : Microsoft.Compute/virtualMachines
...
StorageProfile                :
  ImageReference              :
    Publisher                 : MicrosoftWindowsServer
    Offer                     : WindowsServer
    Sku                       : 2016-Datacenter
    Version                   : latest
  OsDisk                      :
    OsType                    : Windows
    Name                      : myVM
    Vhd                       :
      Uri                     : https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    Caching                   : ReadWrite
    CreateOption              : FromImage
```


## <a name="delete-existing-vm"></a><span data-ttu-id="ac2e3-129">Var olan VM silme</span><span class="sxs-lookup"><span data-stu-id="ac2e3-129">Delete existing VM</span></span>
<span data-ttu-id="ac2e3-130">Sanal sabit diskler ve sanal makineler Azure'da iki ayrı kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-130">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="ac2e3-131">Bir sanal sabit disk hello işletim sisteminin kendisi, uygulamalar ve yapılandırmalar depolandığı ' dir.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-131">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="ac2e3-132">Merhaba VM kendisini hello boyutunu veya konumunu tanımlar ve bir sanal sabit disk veya sanal ağ arabirim kartı (NIC) gibi kaynakları başvuran meta verilerdir.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-132">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="ac2e3-133">Her sanal sabit diske bağlı olduğunda atanmış bir kira sahip tooa VM.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-133">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="ac2e3-134">Veri diskleri bağlı ve hatta hello VM çalışırken ayrılmış olsa da, hello VM kaynak silinmedikçe hello işletim sistemi diski ayrılamıyor.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-134">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="ac2e3-135">Bu VM durduruldu ve deallocated durumda olduğunda bile hello kira tooassociate hello işletim sistemi diski bir VM ile devam eder.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-135">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="ac2e3-136">İlk adım toorecover hello VM toodelete hello VM kendisini kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-136">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="ac2e3-137">Silme hello VM hello sanal sabit diskleri depolama hesabınızdaki bırakır.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-137">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="ac2e3-138">Merhaba, VM silinmiş sonra hello sanal sabit disk tooanother VM tootroubleshoot ekleme ve hello hataları çözümleyin.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-138">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="ac2e3-139">Aşağıdaki örnek siler hello hello adlı VM `myVM` adlı hello kaynak grubundan `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ac2e3-139">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="ac2e3-140">Merhaba VM hello sanal sabit disk tooanother VM eklemeden önce silme tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-140">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="ac2e3-141">Merhaba kira hello sanal sabit diskte hello VM ile ilişkilendiren hello sanal sabit disk tooanother VM iliştirebilirsiniz önce yayınlanan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-141">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="ac2e3-142">Var olan sanal sabit disk tooanother VM ekleme</span><span class="sxs-lookup"><span data-stu-id="ac2e3-142">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="ac2e3-143">Sonraki birkaç adımda için Merhaba, sorun giderme amacıyla başka bir VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-143">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="ac2e3-144">VM toobrowse sorun giderme hello varolan sanal sabit disk toothis ekleme ve hello diskin içeriği düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-144">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="ac2e3-145">Bu işlem toocorrect sağlar herhangi bir yapılandırma hataları veya gözden geçirme ek uygulama veya sistem günlük dosyaları, örneğin.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-145">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="ac2e3-146">Seçin veya sorun giderme amacıyla başka bir VM toouse oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-146">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="ac2e3-147">Merhaba varolan bir sanal sabit diski taktığınızda hello URL toohello disk hello önceki elde belirtin `Get-AzureRmVM` komutu.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-147">When you attach hello existing virtual hard disk, specify hello URL toohello disk obtained in hello preceding `Get-AzureRmVM` command.</span></span> <span data-ttu-id="ac2e3-148">Merhaba aşağıdaki örnek iliştirir adlı VM sorun giderme var olan bir sanal sabit disk toohello `myVMRecovery` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ac2e3-148">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> <span data-ttu-id="ac2e3-149">Disk ekleme toospecify hello hello diskin boyutunu gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-149">Adding a disk requires you toospecify hello size of hello disk.</span></span> <span data-ttu-id="ac2e3-150">Biz varolan bir diski ekleme gibi hello `-DiskSizeInGB` olarak belirtilen `$null`.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-150">As we attach an existing disk, hello `-DiskSizeInGB` is specified as `$null`.</span></span> <span data-ttu-id="ac2e3-151">Bu değer hello veri diski düzgün bağlı ve hello toodetermine doğru veri diski boyutu hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-151">This value ensures hello data disk is correctly attached, and without hello need toodetermine hello true size of data disk.</span></span>


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="ac2e3-152">Merhaba bağlı veri diski bağlama</span><span class="sxs-lookup"><span data-stu-id="ac2e3-152">Mount hello attached data disk</span></span>

1. <span data-ttu-id="ac2e3-153">RDP tooyour VM Hello uygun kimlik bilgilerini kullanarak sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-153">RDP tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="ac2e3-154">Merhaba aşağıdaki örnek indirmeleri hello hello adlı VM için RDP bağlantı dosyası `myVMRecovery` adlı hello kaynak grubunda `myResourceGroup`ve çok indirir`C:\Users\ops\Documents`"</span><span class="sxs-lookup"><span data-stu-id="ac2e3-154">hello following example downloads hello RDP connection file for hello VM named `myVMRecovery` in hello resource group named `myResourceGroup`, and downloads it too`C:\Users\ops\Documents`"</span></span>

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. <span data-ttu-id="ac2e3-155">Merhaba veri diski otomatik olarak algılandı ve bağlı.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-155">hello data disk is automatically detected and attached.</span></span> <span data-ttu-id="ac2e3-156">Bağlı birimlerin toodetermine hello sürücü harfi Hello listesi gibi görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="ac2e3-156">View hello list of attached volumes toodetermine hello drive letter as follows:</span></span>

    ```powershell
    Get-Disk
    ```

    <span data-ttu-id="ac2e3-157">örnek çıktı aşağıdaki hello gösterir hello sanal sabit diske bağlı bir disk **2**.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-157">hello following example output shows hello virtual hard disk connected a disk **2**.</span></span> <span data-ttu-id="ac2e3-158">(Aynı zamanda `Get-Volume` tooview hello sürücü harfi):</span><span class="sxs-lookup"><span data-stu-id="ac2e3-158">(You can also use `Get-Volume` tooview hello drive letter):</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="ac2e3-159">Özgün sanal sabit diskinde ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="ac2e3-159">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="ac2e3-160">Merhaba varolan bir sanal sabit takılı diski ile tüm bakım ve sorun giderme adımları gereken şekilde artık gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-160">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="ac2e3-161">Merhaba sorunlar ele sonra aşağıdaki adımları hello ile devam edin.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-161">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="ac2e3-162">Çıkarın ve özgün sanal sabit disk ayırma</span><span class="sxs-lookup"><span data-stu-id="ac2e3-162">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="ac2e3-163">Hatalarınızı çözüldükten sonra çıkarın ve sorun giderme VM'den hello varolan sanal sabit disk ayırma.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-163">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="ac2e3-164">VM sorun giderme hello sanal sabit disk toohello ekleme hello kira serbest kadar herhangi bir VM ile sanal sabit disk kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-164">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="ac2e3-165">Gelen RDP oturumu içinde hello veri diski, Kurtarma VM çıkarın.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-165">From within your RDP session, unmount hello data disk on your recovery VM.</span></span> <span data-ttu-id="ac2e3-166">Merhaba disk hello numarasından önceki gereksinim `Get-Disk` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-166">You need hello disk number from hello previous `Get-Disk` cmdlet.</span></span> <span data-ttu-id="ac2e3-167">Ardından, `Set-Disk` tooset hello çevrimdışı olarak disk:</span><span class="sxs-lookup"><span data-stu-id="ac2e3-167">Then, use `Set-Disk` tooset hello disk as offline:</span></span>

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    <span data-ttu-id="ac2e3-168">Merhaba disk, çevrimdışı kullanılarak olarak şimdi ayarlanır onaylayın `Get-Disk` yeniden.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-168">Confirm hello disk is now set as offline using `Get-Disk` again.</span></span> <span data-ttu-id="ac2e3-169">Merhaba aşağıdaki örnek çıkış hello disk şimdi çevrimdışı olarak ayarlandı gösterir:</span><span class="sxs-lookup"><span data-stu-id="ac2e3-169">hello following example output shows hello disk is now set as offline:</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. <span data-ttu-id="ac2e3-170">RDP oturumunuzu kapatın.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-170">Exit your RDP session.</span></span> <span data-ttu-id="ac2e3-171">Azure PowerShell oturumunuzda VM sorun giderme hello hello sanal sabit diski kaldırın.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-171">From your Azure PowerShell session, remove hello virtual hard disk from hello troubleshooting VM.</span></span>

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="ac2e3-172">Özgün sabit diskten VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="ac2e3-172">Create VM from original hard disk</span></span>
<span data-ttu-id="ac2e3-173">bir VM, özgün sanal sabit diskten toocreate kullanmak [bu Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="ac2e3-173">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="ac2e3-174">Merhaba gerçek JSON şablon bağlantıyı izleyerek hello şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ac2e3-174">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="ac2e3-175">https://RAW.githubusercontent.com/Azure/Azure-QuickStart-Templates/master/201-VM-Specialized-VHD-Existing-vnet/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="ac2e3-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span></span>

<span data-ttu-id="ac2e3-176">Merhaba şablon hello VHD URL'si hello gelen kullanarak mevcut sanal ağda, bir VM dağıtır önceki komutu.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-176">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="ac2e3-177">Merhaba aşağıdaki örnek dağıtır hello şablon toohello kaynak grubu adında `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ac2e3-177">hello following example deploys hello template toohello resource group named `myResourceGroup`:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

<span data-ttu-id="ac2e3-178">VM adı, işletim sistemi türü ve VM boyutu gibi hello şablonu için yanıt hello ister.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-178">Answer hello prompts for hello template such as VM name, OS type, and VM size.</span></span> <span data-ttu-id="ac2e3-179">Merhaba `osDiskVhdUri` olduğundan, hello aynı VM sorun giderme hello varolan sanal sabit disk toohello eklerken daha önce kullanılan.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-179">hello `osDiskVhdUri` is hello same as previously used when attaching hello existing virtual hard disk toohello troubleshooting VM.</span></span>


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="ac2e3-180">Önyükleme tanılaması yeniden etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="ac2e3-180">Re-enable boot diagnostics</span></span>

<span data-ttu-id="ac2e3-181">Merhaba varolan sanal sabit diskten VM'nizi oluşturduğunuzda, önyükleme tanılaması otomatik olarak etkinleştirilmemiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="ac2e3-181">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="ac2e3-182">Merhaba aşağıdaki örnek hello tanılama uzantısını hello adlı VM üzerinde etkinleştirir `myVMDeployed` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ac2e3-182">hello following example enables hello diagnostic extension on hello VM named `myVMDeployed` in hello resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a><span data-ttu-id="ac2e3-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ac2e3-183">Next steps</span></span>
<span data-ttu-id="ac2e3-184">Tooyour VM bağlantı sorunları yaşıyorsanız, bkz: [sorun giderme RDP bağlantıları tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ac2e3-184">If you are having issues connecting tooyour VM, see [Troubleshoot RDP connections tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="ac2e3-185">VM üzerinde çalışan uygulamalara erişim sorunları için bkz: [Windows VM üzerinde uygulama bağlantı sorunlarını giderme](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ac2e3-185">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="ac2e3-186">Kaynak Yöneticisi'ni kullanma hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ac2e3-186">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
