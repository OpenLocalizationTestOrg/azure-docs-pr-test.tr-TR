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
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-azure-powershell"></a>Bir Windows VM hello işletim sistemi disk tooa kurtarma Azure PowerShell kullanarak bir VM ekleyerek sorun giderme
Azure, Windows sanal makine (VM) önyükleme veya disk bir hatayla karşılaştığında, sorun giderme adımları hello sanal sabit diske kendisini tooperform gerekebilir. Yaygın bir örnek hello VM mümkün tooboot başarıyla engeller başarısız uygulama güncelleştirmesi olacaktır. Bu makale ayrıntıları nasıl toouse Azure PowerShell tooconnect, sanal sabit disk tooanother Windows VM toofix herhangi bir hata sonra özgün VM'yi yeniden oluşturun.


## <a name="recovery-process-overview"></a>Kurtarma işlemine genel bakış
sorun giderme işlemi hello aşağıdaki gibidir:

1. Merhaba sanal sabit diskleri tutmak hello VM karşılaşmadan sorunları, silin.
2. Ekleme ve sorun giderme amacıyla hello sanal sabit disk tooanother Windows VM bağlayın.
3. VM sorun giderme toohello bağlayın. Dosyaları düzenleyin veya herhangi bir aracı toofix sorunları hello özgün sanal sabit disk üzerinde çalıştırın.
4. Çıkarın ve VM sorun giderme hello hello sanal sabit diski kullanımdan çıkarın.
5. Merhaba özgün sanal sabit disk kullanan bir VM oluşturun.

Bilgisayarınızda yüklü olduğundan emin olun [en son Azure PowerShell hello](/powershell/azure/overview) yüklü ve tooyour abonelikte oturum:

```powershell
Login-AzureRMAccount
```

Hello aşağıdaki örneklerde, parametre adları kendi değerlerinizle değiştirin. Örnek parametre adlarında `myResourceGroup`, `mystorageaccount`, ve `myVM`.


## <a name="determine-boot-issues"></a>Önyükleme sorunlarını belirleme
Azure üzerinde bir ekran görüntüsü, VM görüntüleyebilirsiniz toohelp önyükleme sorunlarını giderme. Bu ekran, bir VM tooboot başarısız neden tanımlamaya yardımcı olabilir. Merhaba aşağıdaki örnek hello ekran Windows adlı VM hello alır `myVM` adlı hello kaynak grubunda `myResourceGroup`:

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

Merhaba VM tooboot neden başarısız hello ekran toodetermine gözden geçirin. Herhangi bir özel hata iletileri veya sağlanan hata kodları unutmayın.


## <a name="view-existing-virtual-hard-disk-details"></a>Var olan sanal sabit disk ayrıntılarını görüntüleyin
Sanal sabit disk tooanother VM ekleyebilmek için tooidentify hello adı hello sanal sabit disk (VHD) gerekir.

Merhaba aşağıdaki örnek alır bilgi hello adlı VM için `myVM` adlı hello kaynak grubunda `myResourceGroup`:

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

Ara `Vhd URI` hello içinde `StorageProfile` komutu önceki hello hello çıktısından bölümü. Merhaba aşağıdaki kesilmiş örnek çıkış gösterir hello `Vhd URI` hello kod bloğu hello sonuna doğru:

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


## <a name="delete-existing-vm"></a>Var olan VM silme
Sanal sabit diskler ve sanal makineler Azure'da iki ayrı kaynaktır. Bir sanal sabit disk hello işletim sisteminin kendisi, uygulamalar ve yapılandırmalar depolandığı ' dir. Merhaba VM kendisini hello boyutunu veya konumunu tanımlar ve bir sanal sabit disk veya sanal ağ arabirim kartı (NIC) gibi kaynakları başvuran meta verilerdir. Her sanal sabit diske bağlı olduğunda atanmış bir kira sahip tooa VM. Veri diskleri bağlı ve hatta hello VM çalışırken ayrılmış olsa da, hello VM kaynak silinmedikçe hello işletim sistemi diski ayrılamıyor. Bu VM durduruldu ve deallocated durumda olduğunda bile hello kira tooassociate hello işletim sistemi diski bir VM ile devam eder.

İlk adım toorecover hello VM toodelete hello VM kendisini kaynaktır. Silme hello VM hello sanal sabit diskleri depolama hesabınızdaki bırakır. Merhaba, VM silinmiş sonra hello sanal sabit disk tooanother VM tootroubleshoot ekleme ve hello hataları çözümleyin.

Aşağıdaki örnek siler hello hello adlı VM `myVM` adlı hello kaynak grubundan `myResourceGroup`:

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

Merhaba VM hello sanal sabit disk tooanother VM eklemeden önce silme tamamlanana kadar bekleyin. Merhaba kira hello sanal sabit diskte hello VM ile ilişkilendiren hello sanal sabit disk tooanother VM iliştirebilirsiniz önce yayınlanan toobe gerekir.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Var olan sanal sabit disk tooanother VM ekleme
Sonraki birkaç adımda için Merhaba, sorun giderme amacıyla başka bir VM kullanın. VM toobrowse sorun giderme hello varolan sanal sabit disk toothis ekleme ve hello diskin içeriği düzenleyin. Bu işlem toocorrect sağlar herhangi bir yapılandırma hataları veya gözden geçirme ek uygulama veya sistem günlük dosyaları, örneğin. Seçin veya sorun giderme amacıyla başka bir VM toouse oluşturun.

Merhaba varolan bir sanal sabit diski taktığınızda hello URL toohello disk hello önceki elde belirtin `Get-AzureRmVM` komutu. Merhaba aşağıdaki örnek iliştirir adlı VM sorun giderme var olan bir sanal sabit disk toohello `myVMRecovery` adlı hello kaynak grubunda `myResourceGroup`:

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> Disk ekleme toospecify hello hello diskin boyutunu gerektirir. Biz varolan bir diski ekleme gibi hello `-DiskSizeInGB` olarak belirtilen `$null`. Bu değer hello veri diski düzgün bağlı ve hello toodetermine doğru veri diski boyutu hello sağlar.


## <a name="mount-hello-attached-data-disk"></a>Merhaba bağlı veri diski bağlama

1. RDP tooyour VM Hello uygun kimlik bilgilerini kullanarak sorun giderme. Merhaba aşağıdaki örnek indirmeleri hello hello adlı VM için RDP bağlantı dosyası `myVMRecovery` adlı hello kaynak grubunda `myResourceGroup`ve çok indirir`C:\Users\ops\Documents`"

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. Merhaba veri diski otomatik olarak algılandı ve bağlı. Bağlı birimlerin toodetermine hello sürücü harfi Hello listesi gibi görüntüleyin:

    ```powershell
    Get-Disk
    ```

    örnek çıktı aşağıdaki hello gösterir hello sanal sabit diske bağlı bir disk **2**. (Aynı zamanda `Get-Volume` tooview hello sürücü harfi):

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a>Özgün sanal sabit diskinde ilgili sorunları giderme
Merhaba varolan bir sanal sabit takılı diski ile tüm bakım ve sorun giderme adımları gereken şekilde artık gerçekleştirebilirsiniz. Merhaba sorunlar ele sonra aşağıdaki adımları hello ile devam edin.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Çıkarın ve özgün sanal sabit disk ayırma
Hatalarınızı çözüldükten sonra çıkarın ve sorun giderme VM'den hello varolan sanal sabit disk ayırma. VM sorun giderme hello sanal sabit disk toohello ekleme hello kira serbest kadar herhangi bir VM ile sanal sabit disk kullanamazsınız.

1. Gelen RDP oturumu içinde hello veri diski, Kurtarma VM çıkarın. Merhaba disk hello numarasından önceki gereksinim `Get-Disk` cmdlet'i. Ardından, `Set-Disk` tooset hello çevrimdışı olarak disk:

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    Merhaba disk, çevrimdışı kullanılarak olarak şimdi ayarlanır onaylayın `Get-Disk` yeniden. Merhaba aşağıdaki örnek çıkış hello disk şimdi çevrimdışı olarak ayarlandı gösterir:

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. RDP oturumunuzu kapatın. Azure PowerShell oturumunuzda VM sorun giderme hello hello sanal sabit diski kaldırın.

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a>Özgün sabit diskten VM oluşturma
bir VM, özgün sanal sabit diskten toocreate kullanmak [bu Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet). Merhaba gerçek JSON şablon bağlantıyı izleyerek hello şöyledir:

- https://RAW.githubusercontent.com/Azure/Azure-QuickStart-Templates/master/201-VM-Specialized-VHD-Existing-vnet/azuredeploy.JSON

Merhaba şablon hello VHD URL'si hello gelen kullanarak mevcut sanal ağda, bir VM dağıtır önceki komutu. Merhaba aşağıdaki örnek dağıtır hello şablon toohello kaynak grubu adında `myResourceGroup`:

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

VM adı, işletim sistemi türü ve VM boyutu gibi hello şablonu için yanıt hello ister. Merhaba `osDiskVhdUri` olduğundan, hello aynı VM sorun giderme hello varolan sanal sabit disk toohello eklerken daha önce kullanılan.


## <a name="re-enable-boot-diagnostics"></a>Önyükleme tanılaması yeniden etkinleştirin

Merhaba varolan sanal sabit diskten VM'nizi oluşturduğunuzda, önyükleme tanılaması otomatik olarak etkinleştirilmemiş olabilir. Merhaba aşağıdaki örnek hello tanılama uzantısını hello adlı VM üzerinde etkinleştirir `myVMDeployed` adlı hello kaynak grubunda `myResourceGroup`:

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a>Sonraki adımlar
Tooyour VM bağlantı sorunları yaşıyorsanız, bkz: [sorun giderme RDP bağlantıları tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). VM üzerinde çalışan uygulamalara erişim sorunları için bkz: [Windows VM üzerinde uygulama bağlantı sorunlarını giderme](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Kaynak Yöneticisi'ni kullanma hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
