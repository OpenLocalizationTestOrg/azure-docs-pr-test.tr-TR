---
title: "Azure yönetilen görüntüde aaaCreate | Microsoft Docs"
description: "Genelleştirilmiş bir VM veya VHD yönetilen bir görüntüsünü oluşturma. Görüntüleri kullanılan toocreate yönetilen diskler kullanan birden çok VM olabilir."
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
ms.openlocfilehash: d8cd6c2ce8c5d704de2c845abced85139944d682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a>Yönetilen bir genelleştirilmiş bir VM görüntüsü oluşturma

Yönetilen görüntü kaynağı olarak yönetilen bir disk veya yönetilmeyen bir disk depolama hesabında depolanan genelleştirilmiş bir VM oluşturulabilir. Görüntü can hello sonra birden çok VM kullanılan toocreate olabilir. 


## <a name="generalize-hello-windows-vm-using-sysprep"></a>Generalize Sysprep kullanarak Windows VM hello

Sysprep tüm kişisel hesap bilgilerinize, başka şeylerin kaldırır ve bir görüntü olarak kullanılan hello makine toobe hazırlar. Sysprep hakkında daha fazla ayrıntı için bkz: [nasıl tooUse Sysprep: Giriş](http://technet.microsoft.com/library/bb457073.aspx).

Merhaba makine üzerinde çalışan hello sunucu rolleri Sysprep tarafından desteklendiğinden emin olun. Daha fazla bilgi için bkz: [sunucu rolleri için Sysprep desteği](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Sysprep, VHD tooAzure hello için karşıya yüklemeden önce ilk kez çalıştırıyorsanız olduğundan emin olun [VM'nizi hazırlanmış](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Sysprep çalıştırılmadan önce. 
> 
> 

1. Windows sanal makine içinde toohello imzalayın.
2. Merhaba komut istemi penceresi bir yönetici olarak açın. Merhaba dizini çok değiştirmek**%windir%\system32\sysprep**ve ardından çalıştırın `sysprep.exe`.
3. Merhaba, **Sistem Hazırlama aracı** iletişim kutusunda **girin sistem Out-of-Box deneyimi (OOBE)**ve bu hello emin olun **Generalize** onay kutusu seçilidir.
4. İçinde **kapatma seçenekleri**seçin **kapatma**.
5. **Tamam** düğmesine tıklayın.
   
    ![Sysprep Başlat](./media/upload-generalized-managed/sysprepgeneral.png)
6. Sysprep tamamlandığında hello sanal makineyi kapatır. Merhaba VM yeniden başlatmayın.


## <a name="create-a-managed-image-in-hello-portal"></a>Merhaba Portalı'nda yönetilen bir görüntü oluşturma 

1. Açık hello [portal](https://portal.azure.com).
2. Yeni bir kaynak artı toocreate hello'ı tıklatın.
3. Merhaba filtre ara yazın **görüntü**.
4. Seçin **görüntü** hello sonuçlarından.
5. Merhaba, **görüntü** dikey penceresinde tıklatın **oluşturma**.
6. İçinde **adı**, hello görüntü için bir ad yazın.
7. Birden fazla aboneliğiniz varsa, select hello doğru bir hello **abonelik** açılır.
7. İçinde **kaynak grubu** ya da seçin **Yeni Oluştur** ve bir ad yazın veya seçin **varolan** ve kaynak grubu toouse hello aşağı açılan listeden seçin.
8. İçinde **konumu**, kaynak grubunuz hello konumunu seçin.
9. İçinde **işletim sistemi türü** işletim sistemi, Windows veya Linux hello türünü seçin.
11. İçinde **depolama blobu**, tıklatın **Gözat** toolook Azure depolama alanınızı hello VHD için.
12. İçinde **hesap türü** Standard_LRS veya Premium_LRS seçin. Standart sabit disk sürücüleri ve Premium katı hal sürücüleri kullanır. Hem yerel olarak yedekli depolama kullanın.
13. İçinde **Disk önbelleği** hello önbelleğe uygun diski seçin. Başlangıç Seçenekleri **hiçbiri**, **salt okunur** ve **sürücüsünde**.
14. İsteğe bağlı: Da var olan bir veri diski toohello görüntüsünü tıklayarak ekleyebilirsiniz **+ Ekle veri diski**.  
15. İşiniz bittiğinde seçimlerinizi yaptıktan tıklatın **oluşturma**.
16. Merhaba görüntü oluşturulduktan sonra bunu olarak görür bir **görüntü** kaynak hello Seçtiğiniz hello kaynak grubundaki kaynaklar listesinde.



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a>Yönetilen bir Powershell kullanarak bir VM görüntüsü oluşturma

Doğrudan VM, hello görüntü sağlar hello bir görüntü oluşturmayı hello hello işletim sistemi diski ve veri diskleri gibi VM ile ilişkili hello disklerin tümünü içerir.


Başlamadan önce hello hello AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun. Çalıştırma hello komut tooinstall onu.

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
2. VM serbest emin hello olun.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Hello sanal makinenin başlangıç durumu çok Ayarla**Genelleştirmiş**. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. Merhaba sanal makine alın. 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. Merhaba görüntü yapılandırmasını oluşturun.

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. Merhaba görüntü oluşturma.

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a>PowerShell'de yönetilen bir VHD görüntüsü oluşturma

Genelleştirilmiş OS VHD kullanılarak yönetilen bir görüntü oluşturun.


1.  İlk olarak, hello ortak parametreleri ayarlayın:

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. Step\deallocate hello VM.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Merhaba VM genelleştirilmiş olarak işaretleyin.

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  Genelleştirilmiş OS VHD kullanarak hello görüntüsü oluşturun.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a>Powershell kullanarak bir anlık görüntüden yönetilen bir görüntü oluşturma

Bir anlık görüntüsünü hello genelleştirilmiş VM VHD'den yönetilen resim de oluşturabilirsiniz.

    
1. Bazı değişkenler oluşturun. 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. Başlangıç anlık görüntü alın.

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. Merhaba görüntü yapılandırmasını oluşturun.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. Merhaba görüntü oluşturma.

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a>Sonraki adımlar
- Artık [genelleştirilmiş hello yönetilen görüntüsünden bir VM oluşturma](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).    

