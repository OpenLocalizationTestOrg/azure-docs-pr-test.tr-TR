---
title: "Bir Windows Azure PowerShell ile VM sorun giderme kullanın | Microsoft Docs"
description: "Kurtarma Azure PowerShell kullanarak bir VM için işletim sistemi diski bağlanarak Azure Windows VM sorunlarını giderme hakkında bilgi edinin"
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
ms.openlocfilehash: 8b7821b4285e73d461af426bfdfb3fdcc4454517
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-azure-powershell"></a><span data-ttu-id="ca6d2-103">Bir Windows VM kurtarma Azure PowerShell kullanarak bir VM için işletim sistemi diski ekleyerek sorun giderme</span><span class="sxs-lookup"><span data-stu-id="ca6d2-103">Troubleshoot a Windows VM by attaching the OS disk to a recovery VM using Azure PowerShell</span></span>
<span data-ttu-id="ca6d2-104">Azure, Windows sanal makine (VM) önyükleme veya disk bir hatayla karşılaştığında, sanal sabit diskin kendisinde sorun giderme adımları gerçekleştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="ca6d2-105">Yaygın bir örnek VM başarıyla önyükleme engeller başarısız uygulama güncelleştirmesi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-105">A common example would be a failed application update that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="ca6d2-106">Bu makale Azure PowerShell, sanal sabit diski başka bir Windows hataları düzeltin, sonra özgün VM'yi yeniden oluşturmak için VM'e bağlanmak için nasıl kullanılacağını ayrıntılarını verir.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-106">This article details how to use Azure PowerShell to connect your virtual hard disk to another Windows VM to fix any errors, then re-create your original VM.</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="ca6d2-107">Kurtarma işlemine genel bakış</span><span class="sxs-lookup"><span data-stu-id="ca6d2-107">Recovery process overview</span></span>
<span data-ttu-id="ca6d2-108">Sorun giderme işlemi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="ca6d2-108">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="ca6d2-109">Sorunlarla, sanal sabit diskleri tutmak VM silin.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-109">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="ca6d2-110">Ekleme ve sorun giderme amacıyla başka bir Windows VM için sanal sabit diski bağlama.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-110">Attach and mount the virtual hard disk to another Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="ca6d2-111">Sorun giderme işlemlerini yapacağınız VM'ye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-111">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="ca6d2-112">Dosyaları düzenleyin veya özgün sanal sabit diskte sorunlarını gidermek için herhangi bir aracı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-112">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="ca6d2-113">Sorun giderme işlemlerini yaptığınız VM’den sanal sabit diski çıkarın.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-113">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="ca6d2-114">Özgün sanal sabit disk kullanan bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-114">Create a VM using the original virtual hard disk.</span></span>

<span data-ttu-id="ca6d2-115">Bilgisayarınızda yüklü olduğundan emin olun [en son Azure PowerShell](/powershell/azure/overview) yüklü ve aboneliğinize oturum:</span><span class="sxs-lookup"><span data-stu-id="ca6d2-115">Make sure that you have [the latest Azure PowerShell](/powershell/azure/overview) installed and logged in to your subscription:</span></span>

```powershell
Login-AzureRMAccount
```

<span data-ttu-id="ca6d2-116">Aşağıdaki örneklerde, parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-116">In the following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="ca6d2-117">Örnek parametre adlarında `myResourceGroup`, `mystorageaccount`, ve `myVM`.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-117">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="ca6d2-118">Önyükleme sorunlarını belirleme</span><span class="sxs-lookup"><span data-stu-id="ca6d2-118">Determine boot issues</span></span>
<span data-ttu-id="ca6d2-119">Önyükleme sorunlarını gidermenize yardımcı olması için bir ekran görüntüsü, VM görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-119">You can view a screenshot of your VM in Azure to help troubleshoot boot issues.</span></span> <span data-ttu-id="ca6d2-120">Bu ekran, önyükleme bir VM başarısız neden tanımlamaya yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-120">This screenshot can help identify why a VM fails to boot.</span></span> <span data-ttu-id="ca6d2-121">Aşağıdaki örnek ekran görüntüsünde Windows adlı VM'den alır `myVM` kaynak grubunda adlı `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ca6d2-121">The following example gets the screenshot from the Windows VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

<span data-ttu-id="ca6d2-122">VM önyükleme neden başarısız olduğunu belirlemek için ekran görüntüsünü gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-122">Review the screenshot to determine why the VM is failing to boot.</span></span> <span data-ttu-id="ca6d2-123">Herhangi bir özel hata iletileri veya sağlanan hata kodları unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-123">Note any specific error messages or error codes provided.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="ca6d2-124">Var olan sanal sabit disk ayrıntılarını görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="ca6d2-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="ca6d2-125">Sanal sabit disk için başka bir VM iliştirebilirsiniz önce sanal sabit disk (VHD) adını tanımlamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-125">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span>

<span data-ttu-id="ca6d2-126">Aşağıdaki örnek adlı VM için bilgilerini alır `myVM` kaynak grubunda adlı `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ca6d2-126">The following example gets information for the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="ca6d2-127">Ara `Vhd URI` içinde `StorageProfile` önceki komutun çıktısından bölümü.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-127">Look for `Vhd URI` within the `StorageProfile` section from the output of the preceding command.</span></span> <span data-ttu-id="ca6d2-128">Aşağıdaki örnek çıktısında kesilmiş `Vhd URI` kod bloğunu sonuna:</span><span class="sxs-lookup"><span data-stu-id="ca6d2-128">The following truncated example output shows the `Vhd URI` towards the end of the code block:</span></span>

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


## <a name="delete-existing-vm"></a><span data-ttu-id="ca6d2-129">Var olan VM silme</span><span class="sxs-lookup"><span data-stu-id="ca6d2-129">Delete existing VM</span></span>
<span data-ttu-id="ca6d2-130">Sanal sabit diskler ve sanal makineler Azure'da iki ayrı kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-130">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="ca6d2-131">Bir sanal sabit disk, işletim sisteminin kendisi, uygulamalar ve yapılandırmalar depolandığı ' dir.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-131">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="ca6d2-132">VM boyutunu veya konumunu tanımlar ve bir sanal sabit disk veya sanal ağ arabirim kartı (NIC) gibi kaynakları başvuran meta verilerdir.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-132">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="ca6d2-133">Her sanal sabit disk için bir VM eklendiğinde atanmış bir kira var.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-133">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="ca6d2-134">Veri diskleri VM çalışırken bile eklenip çıkarılabilir, ancak VM kaynağı silinmedikçe işletim sistemi diski çıkarılamaz.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-134">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="ca6d2-135">Bu VM durduruldu ve deallocated durumda olduğunda bile işletim sistemi diski bir VM ile ilişkilendirilecek kira sürdürür.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-135">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="ca6d2-136">VM kurtarmak için ilk adım, VM kaynak silmektir.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-136">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="ca6d2-137">VM’yi sildiğinizde sanal sabit diskler depolama hesabınızda kalır.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-137">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="ca6d2-138">VM silindikten sonra sanal sabit diski ve hataları gidermek için başka bir VM'e ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-138">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="ca6d2-139">Aşağıdaki örnek adlı VM siler `myVM` kaynak grubundan adlı `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ca6d2-139">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span></span>

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="ca6d2-140">VM için başka bir VM sanal sabit disk eklemeden önce silme tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-140">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="ca6d2-141">VM ile ilişkilendirir sanal sabit disk üzerindeki kira süresini sanal sabit disk için başka bir VM eklemeden önce yayımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-141">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="ca6d2-142">Varolan bir sanal sabit diski başka bir VM'e ekleyin</span><span class="sxs-lookup"><span data-stu-id="ca6d2-142">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="ca6d2-143">Sonraki birkaç adımda için sorun giderme amacıyla başka bir VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-143">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="ca6d2-144">Varolan bir sanal sabit diski bulun ve diskin içeriği düzenlemek için sorun giderme bu VM'e ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-144">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span></span> <span data-ttu-id="ca6d2-145">Bu işlem, yapılandırma hataları düzeltin ya da ek uygulama veya sistem günlük dosyalarını, örneğin gözden olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-145">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="ca6d2-146">Seçin veya sorun giderme amacıyla kullanmak için başka bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-146">Choose or create another VM to use for troubleshooting purposes.</span></span>

<span data-ttu-id="ca6d2-147">Varolan bir sanal sabit diski taktığınızda, önceki elde disk URL'yi belirtmek `Get-AzureRmVM` komutu.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-147">When you attach the existing virtual hard disk, specify the URL to the disk obtained in the preceding `Get-AzureRmVM` command.</span></span> <span data-ttu-id="ca6d2-148">Aşağıdaki örnek sorun giderme VM adlı varolan bir sanal sabit diski iliştirir `myVMRecovery` kaynak grubunda adlı `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ca6d2-148">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> <span data-ttu-id="ca6d2-149">Disk ekleme diskin boyutunu belirtmenizi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-149">Adding a disk requires you to specify the size of the disk.</span></span> <span data-ttu-id="ca6d2-150">Biz varolan bir diski ilişti gibi `-DiskSizeInGB` olarak belirtilen `$null`.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-150">As we attach an existing disk, the `-DiskSizeInGB` is specified as `$null`.</span></span> <span data-ttu-id="ca6d2-151">Bu değer veri diski düzgün bağlı sağlar ve veri diski true boyutunu belirlemek için gerek kalmadan.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-151">This value ensures the data disk is correctly attached, and without the need to determine the true size of data disk.</span></span>


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="ca6d2-152">Bağlı veri diski bağlama</span><span class="sxs-lookup"><span data-stu-id="ca6d2-152">Mount the attached data disk</span></span>

1. <span data-ttu-id="ca6d2-153">Uygun kimlik bilgilerini kullanarak sorun giderme, VM için RDP.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-153">RDP to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="ca6d2-154">Aşağıdaki örnek adlı VM için RDP bağlantı dosyası karşıdan `myVMRecovery` kaynak grubunda adlı `myResourceGroup`ve kendisine indirir `C:\Users\ops\Documents`"</span><span class="sxs-lookup"><span data-stu-id="ca6d2-154">The following example downloads the RDP connection file for the VM named `myVMRecovery` in the resource group named `myResourceGroup`, and downloads it to `C:\Users\ops\Documents`"</span></span>

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. <span data-ttu-id="ca6d2-155">Veri diski otomatik olarak algılanır ve bağlı.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-155">The data disk is automatically detected and attached.</span></span> <span data-ttu-id="ca6d2-156">Sürücü harfi şu şekilde belirlemek için bağlı birimlerin listesini görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="ca6d2-156">View the list of attached volumes to determine the drive letter as follows:</span></span>

    ```powershell
    Get-Disk
    ```

    <span data-ttu-id="ca6d2-157">Aşağıdaki örnek çıkış sanal sabit diske bağlı bir disk gösterir **2**.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-157">The following example output shows the virtual hard disk connected a disk **2**.</span></span> <span data-ttu-id="ca6d2-158">(Aynı zamanda `Get-Volume` sürücü harfi görüntülemek için):</span><span class="sxs-lookup"><span data-stu-id="ca6d2-158">(You can also use `Get-Volume` to view the drive letter):</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="ca6d2-159">Özgün sanal sabit diskinde ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="ca6d2-159">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="ca6d2-160">Varolan bir sanal sabit takılı diski ile tüm bakım ve sorun giderme adımları gereken şekilde artık gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-160">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="ca6d2-161">Sorunları giderdikten sonra aşağıdaki adımlarla devam edin.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-161">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="ca6d2-162">Çıkarın ve özgün sanal sabit disk ayırma</span><span class="sxs-lookup"><span data-stu-id="ca6d2-162">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="ca6d2-163">Hatalarınızı çözüldükten sonra çıkarın ve varolan bir sanal sabit diski, sorun giderme sanal makineden ayırın.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-163">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="ca6d2-164">Sorun giderme VM için sanal sabit disk ekleme kira serbest kadar herhangi bir VM ile sanal sabit disk kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-164">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="ca6d2-165">Gelen RDP oturumu içinde veri diski, Kurtarma VM çıkarın.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-165">From within your RDP session, unmount the data disk on your recovery VM.</span></span> <span data-ttu-id="ca6d2-166">Disk numarası önceki gereksinim `Get-Disk` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-166">You need the disk number from the previous `Get-Disk` cmdlet.</span></span> <span data-ttu-id="ca6d2-167">Ardından, `Set-Disk` disk çevrimdışı olarak ayarlamak için:</span><span class="sxs-lookup"><span data-stu-id="ca6d2-167">Then, use `Set-Disk` to set the disk as offline:</span></span>

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    <span data-ttu-id="ca6d2-168">Disk, çevrimdışı kullanılarak olarak şimdi ayarlanır onaylayın `Get-Disk` yeniden.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-168">Confirm the disk is now set as offline using `Get-Disk` again.</span></span> <span data-ttu-id="ca6d2-169">Aşağıdaki örnek çıkış disk şimdi çevrimdışı olarak ayarlandı gösterir:</span><span class="sxs-lookup"><span data-stu-id="ca6d2-169">The following example output shows the disk is now set as offline:</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. <span data-ttu-id="ca6d2-170">RDP oturumunuzu kapatın.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-170">Exit your RDP session.</span></span> <span data-ttu-id="ca6d2-171">Azure PowerShell oturumunuzda, sorun giderme sanal makineden sanal sabit diski kaldırın.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-171">From your Azure PowerShell session, remove the virtual hard disk from the troubleshooting VM.</span></span>

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="ca6d2-172">Özgün sabit diskten VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="ca6d2-172">Create VM from original hard disk</span></span>
<span data-ttu-id="ca6d2-173">Özgün sanal sabit diskten bir VM oluşturmak için kullanmak [bu Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="ca6d2-173">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="ca6d2-174">Gerçek JSON şablon aşağıdaki bağlantıda şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ca6d2-174">The actual JSON template is at the following link:</span></span>

- <span data-ttu-id="ca6d2-175">https://RAW.githubusercontent.com/Azure/Azure-QuickStart-Templates/master/201-VM-Specialized-VHD-Existing-vnet/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="ca6d2-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span></span>

<span data-ttu-id="ca6d2-176">Önceki komutu VHD URL'yi kullanarak mevcut sanal ağda, bir VM şablonu dağıtır.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-176">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="ca6d2-177">Aşağıdaki örnek adlı kaynak grubunu şablon dağıtır `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ca6d2-177">The following example deploys the template to the resource group named `myResourceGroup`:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

<span data-ttu-id="ca6d2-178">VM adı, işletim sistemi türü ve VM boyutu gibi şablonu için istemleri yanıtlayın.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-178">Answer the prompts for the template such as VM name, OS type, and VM size.</span></span> <span data-ttu-id="ca6d2-179">`osDiskVhdUri` Daha önce kullanıldığında aynı varolan bir sanal sabit diski sorun giderme VM'ye ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-179">The `osDiskVhdUri` is the same as previously used when attaching the existing virtual hard disk to the troubleshooting VM.</span></span>


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="ca6d2-180">Önyükleme tanılaması yeniden etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="ca6d2-180">Re-enable boot diagnostics</span></span>

<span data-ttu-id="ca6d2-181">Var olan sanal sabit diskten VM'nizi oluşturduğunuzda, önyükleme tanılaması otomatik olarak etkinleştirilmemiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="ca6d2-181">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="ca6d2-182">Aşağıdaki örnek adlı VM'de tanılama uzantısını etkinleştirir `myVMDeployed` kaynak grubunda adlı `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ca6d2-182">The following example enables the diagnostic extension on the VM named `myVMDeployed` in the resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a><span data-ttu-id="ca6d2-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ca6d2-183">Next steps</span></span>
<span data-ttu-id="ca6d2-184">VM'nize bağlantı sorunları yaşıyorsanız, bkz: [bir Azure VM için RDP sorun giderme bağlantılarını](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ca6d2-184">If you are having issues connecting to your VM, see [Troubleshoot RDP connections to an Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="ca6d2-185">VM üzerinde çalışan uygulamalara erişim sorunları için bkz: [Windows VM üzerinde uygulama bağlantı sorunlarını giderme](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ca6d2-185">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="ca6d2-186">Kaynak Yöneticisi'ni kullanma hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ca6d2-186">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
