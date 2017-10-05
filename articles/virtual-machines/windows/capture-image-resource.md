---
title: "Yönetilen bir görüntü oluşturma | Microsoft Docs"
description: "Genelleştirilmiş bir VM veya VHD yönetilen bir görüntüsünü oluşturma. Görüntüleri yönetilen diskler kullanan birden çok VM oluşturmak için kullanılabilir."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: f64b81489ab426b50ec89af369e1581ac71848be
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a>Yönetilen bir genelleştirilmiş bir VM görüntüsü oluşturma

Yönetilen görüntü kaynağı olarak yönetilen bir disk veya yönetilmeyen bir disk depolama hesabında depolanan genelleştirilmiş bir VM oluşturulabilir. Görüntü sonra birden çok VM oluşturmak için kullanılabilir. 


## <a name="generalize-the-windows-vm-using-sysprep"></a>Sysprep kullanarak Windows VM generalize

Sysprep tüm kişisel hesap bilgilerinize, başka şeylerin kaldırır ve bir görüntü olarak kullanılacak makine hazırlar. Sysprep hakkında daha fazla ayrıntı için bkz: [kullanım Sysprep nasıl: Giriş](http://technet.microsoft.com/library/bb457073.aspx).

Makinede çalışan sunucu rollerini Sysprep tarafından desteklendiğinden emin olun. Daha fazla bilgi için bkz: [sunucu rolleri için Sysprep desteği](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Sysprep, VHD Azure'a ilk kez karşıya yüklemeden önce çalıştırıyorsanız olduğundan emin olun [VM'nizi hazırlanmış](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Sysprep çalıştırılmadan önce. 
> 
> 

1. Windows sanal makinede oturum açın.
2. Bir yönetici olarak komut istemi penceresi açın. Dizinine değiştirin **%windir%\system32\sysprep**ve ardından çalıştırın `sysprep.exe`.
3. İçinde **Sistem Hazırlama aracı** iletişim kutusunda **girin sistem Out-of-Box deneyimi (OOBE)**, emin olun **Generalize** onay kutusu seçilidir.
4. İçinde **kapatma seçenekleri**seçin **kapatma**.
5. **Tamam** düğmesine tıklayın.
   
    ![Sysprep Başlat](./media/upload-generalized-managed/sysprepgeneral.png)
6. Sysprep tamamlandığında, sanal makineyi kapatır. VM yeniden başlatmayın.


## <a name="create-a-managed-image-in-the-portal"></a>Portalda yönetilen bir görüntü oluşturma 

1. Açık [portal](https://portal.azure.com).
2. Yeni bir kaynak oluşturmak için artı işaretine tıklayın.
3. Filtre Ara yazın **görüntü**.
4. Seçin **görüntü** sonuçlarından.
5. İçinde **görüntü** dikey penceresinde tıklatın **oluşturma**.
6. İçinde **adı**, görüntü için bir ad yazın.
7. Birden fazla aboneliğiniz varsa doğru makineden seçin **abonelik** açılır.
7. İçinde **kaynak grubu** ya da seçin **Yeni Oluştur** ve bir ad yazın veya seçin **varolan** ve aşağı açılan listeden kullanmak için bir kaynak grubu seçin.
8. İçinde **konumu**, kaynak grubu konumunu seçin.
9. İçinde **işletim sistemi türü** Windows ya da Linux işletim sistemi türünü seçin.
11. İçinde **depolama blobu**, tıklatın **Gözat** Azure depolama alanınızı VHD aramak için.
12. İçinde **hesap türü** Standard_LRS veya Premium_LRS seçin. Standart sabit disk sürücüleri ve Premium katı hal sürücüleri kullanır. Hem yerel olarak yedekli depolama kullanın.
13. İçinde **Disk önbelleği** seçeneği önbelleğe alma için uygun diski seçin. Seçenekler şunlardır: **hiçbiri**, **salt okunur** ve **sürücüsünde**.
14. İsteğe bağlı: Da varolan bir veri diski görüntüye tıklayarak ekleyebilirsiniz **+ Ekle veri diski**.  
15. İşiniz bittiğinde seçimlerinizi yaptıktan tıklatın **oluşturma**.
16. Görüntü oluşturulduktan sonra bunu olarak görür bir **görüntü** kaynak seçtiğiniz kaynak grubundaki kaynaklar listesinde.



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a>Yönetilen bir Powershell kullanarak bir VM görüntüsü oluşturma

Doğrudan sanal makineden bir görüntü oluşturma görüntünün işletim sistemi diski ve veri diskleri gibi VM ile ilişkili tüm diskleri içeren sağlar.


Başlamadan önce AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun. Yüklemek için aşağıdaki komutu çalıştırın.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).


1. Bazı değişkenler oluşturun.

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. VM serbest emin olun.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Sanal makine durumunu ayarlamak **Genelleştirmiş**. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. Sanal makine Al. 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. Görüntü yapılandırmasını oluşturun.

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. Görüntü oluşturma.

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a>PowerShell'de yönetilen bir VHD görüntüsü oluşturma

Genelleştirilmiş OS VHD kullanılarak yönetilen bir görüntü oluşturun.


1.  İlk olarak, ortak parametreleri ayarlayın:

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. Step\deallocate VM.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. VM genelleştirilmiş olarak işaretleyin.

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  Genelleştirilmiş OS VHD kullanarak görüntü oluşturma.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a>Powershell kullanarak bir anlık görüntüden yönetilen bir görüntü oluşturma

Genelleştirilmiş bir VM VHD'den görüntüsünü yönetilen resim de oluşturabilirsiniz.

    
1. Bazı değişkenler oluşturun. 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. Anlık görüntü alın.

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. Görüntü yapılandırmasını oluşturun.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. Görüntü oluşturma.

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a>Sonraki adımlar
- Artık [bir VM genelleştirilmiş yönetilen görüntüden oluşturma](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).  

