---
title: "aaaCreate ve karşıya yükleme VM görüntü Powershell kullanarak | Microsoft Docs"
description: "Toocreate öğrenin ve hello Klasik dağıtım modeli ve Azure Powershell kullanılarak genelleştirilmiş bir Windows Server yansıma (VHD) yükleyin."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8c4a08fe-7714-4bf0-be87-c728a7806d3f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: 093b57c9157cea5f348c8ba02b5700c917adbcdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-windows-server-vhd-tooazure"></a>Oluşturma ve Windows Server VHD tooAzure yükleme
Bu makalede nasıl tooupload genelleştirilmiş VM görüntü sanal sabit disk (VHD) toocreate sanal makineleri kullanabilmesi için gösterilmektedir. Diskleri ve Microsoft Azure içinde VHD'leri hakkında daha fazla ayrıntı için [hakkında diskleri ve sanal makineler için VHD'ler](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Ayrıca [karşıya](../upload-generalized-managed.md) hello Resource Manager modelini kullanarak bir sanal makine.

## <a name="prerequisites"></a>Ön koşullar
Bu makalede, sahip olduğunuz varsayılmaktadır:

* **Bir Azure aboneliği** -yoksa, şunları yapabilirsiniz [ücretsiz bir Azure hesabı açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
* **[Microsoft Azure PowerShell](/powershell/azure/overview)**  -hello Microsoft Azure PowerShell sahip modülü yüklenir ve aboneliğinizi toouse yapılandırılır.
* **A. VHD dosyasını** - desteklenen Windows işletim sistemi bir .vhd dosyası ekli tooa sanal makine depolanır. VHD Hello üzerinde çalışan hello sunucu rolleri Sysprep tarafından destekleniyorsa toosee denetleyin. Daha fazla bilgi için bkz: [sunucu rolleri için Sysprep desteği](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).

    > [!IMPORTANT]
    > Microsoft Azure'da Hello VHDX biçimi desteklenmiyor. Hyper-V Yöneticisi'ni veya hello kullanarak hello disk tooVHD biçimine dönüştürebilirsiniz [Convert-VHD cmdlet](http://technet.microsoft.com/library/hh848454.aspx). Ayrıntılar için bu bkz [blog gönderisi](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).

## <a name="step-1-prep-hello-vhd"></a>1. adım: Hazırlığı hello VHD
Merhaba VHD tooAzure karşıya yüklemeden önce hello Sysprep aracını kullanılarak genelleştirilmiş toobe gerekir. Bir görüntü olarak kullanılan hello VHD toobe hazırlar. Sysprep hakkında daha fazla ayrıntı için bkz: [nasıl tooUse Sysprep: Giriş](http://technet.microsoft.com/library/bb457073.aspx). VM Hello, Sysprep çalıştırılmadan önce yedekleyin.

Merhaba sanal makineden işletim sistemi hello hello aşağıdaki yordamı tamamlamak için yüklendi:

1. Toohello işletim sisteminde oturum açın.
2. Yönetici olarak bir komut istemi penceresi açın. Merhaba dizini çok değiştirmek**%windir%\system32\sysprep**ve ardından çalıştırın `sysprep.exe`.

    ![Bir komut istemi penceresi açın](./media/createupload-vhd/sysprep_commandprompt.png)
3. Merhaba **Sistem Hazırlama aracı** iletişim kutusu görüntülenir.

   ![Sysprep Başlat](./media/createupload-vhd/sysprepgeneral.png)
4. Merhaba, **Sistem Hazırlama aracı**seçin **girin sistem ilk çalıştırma deneyimi (OOBE)** emin olun **Generalize** denetlenir.
5. İçinde **kapatma seçenekleri**seçin **kapatma**.
6. **Tamam** düğmesine tıklayın.

## <a name="step-2-create-a-storage-account-and-a-container"></a>2. adım: bir depolama hesabı ve kapsayıcı oluşturma
Bir yerde tooupload hello .vhd dosyası için bir Azure depolama hesabında olması gerekir. Bu adım nasıl toocreate bir hesap veya get hello bilgileri gösterir, var olan bir hesaptan gerekir. Merhaba değişkenleri değiştirin &lsaquo; köşeli &rsaquo; kendi bilgilerle.

1. Oturum Aç

    ```powershell
    Add-AzureAccount
    ```

2. Azure aboneliğiniz ayarlayın.

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. Yeni bir depolama hesabı oluşturun. Merhaba hello depolama hesabı adının benzersiz olması 3-24 karakter. Merhaba adı harfler ve sayıların birleşiminden oluşabilir. Ayrıca toospecify "Doğu ABD" gibi bir yerde gerekir

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. Merhaba yeni depolama hesabı hello varsayılan olarak ayarlayın.

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. Yeni bir kapsayıcı oluşturun.

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-hello-vhd-file"></a>3. adım: hello .vhd dosyasını karşıya yükle
Kullanım hello [Ekle AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) tooupload hello VHD.

Merhaba önceki adımda kullanılan hello Azure PowerShell penceresi türü hello aşağıdaki komut ve hello değişkenleri değiştirin &lsaquo; köşeli &rsaquo; kendi bilgilerle.

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-hello-image-tooyour-list-of-custom-images"></a>4. adım: hello görüntü tooyour özel resimler listesi ekleme
Kullanım hello [Ekle AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet tooadd hello görüntü toohello listesi özel görüntüler.

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a>Sonraki adımlar
Artık [özel bir VM oluşturma](createportal.md) hello kullanarak karşıya görüntü.
