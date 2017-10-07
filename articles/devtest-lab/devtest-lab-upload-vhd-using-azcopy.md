---
title: aaaUpload VHD tooAzure DevTest Labs AzCopy kullanarak dosya | Microsoft Docs
description: "AzCopy kullanarak VHD dosyasını toolab ait depolama hesabı karşıya yükle"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 14f9e933b0bd27451f6bcb94841ecc381213e578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-azcopy"></a>AzCopy kullanarak VHD dosyasını toolab ait depolama hesabı karşıya yükle

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

Azure DevTest Labs'de VHD dosyaları kullanılan tooprovision sanal makinelerdir kullanılan toocreate özel resimler olabilir. Aşağıdaki adımları Merhaba, hello AzCopy komut satırı yardımcı programını tooupload kullanılarak üzerinden bir VHD dosyası tooa Laboratuvar ait depolama hesabı yol. VHD dosyasını yüklediğiniz sonra hello [bölüm'sonraki adımlar](#next-steps) nasıl toocreate hello özel bir görüntüden VHD dosyasını karşıya göstermeye bazı makaleleri listeler. Diskleri ve Azure içinde VHD'leri hakkında daha fazla bilgi için bkz: [diskler ve sanal makineler için VHD'ler hakkında](../virtual-machines/linux/about-disks-and-vhds.md)

> [!NOTE] 
>  
> AzCopy yalnızca Windows bir komut satırı yardımcı programıdır.

## <a name="step-by-step-instructions"></a>Adım adım yönergeler

Merhaba adımları ilerlemesi tooAzure DevTest Labs kullanarak bir VHD'yi karşıya size dosya [AzCopy](http://aka.ms/downloadazcopy). 

1. Merhaba hello Azure portal kullanarak hello Laboratuvar ait depolama hesabı adını alın:

1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Seçin **daha fazla hizmet**ve ardından **DevTest Labs** hello listeden.

1. Merhaba istenen Laboratuvar labs Hello listeden seçin.  

1. Merhaba Laboratuvar'ın dikey penceresinde, seçin **yapılandırma**. 

1. Merhaba Laboratuvar üzerinde **yapılandırma** dikey penceresinde, select **özel görüntülerini (VHD)**.

1. Merhaba üzerinde **özel görüntüleri** dikey penceresinde, seçin **+ Ekle**. 

1. Merhaba üzerinde **özel görüntü** dikey penceresinde, select **VHD**.

1. Merhaba üzerinde **VHD** dikey penceresinde, select **PowerShell kullanarak bir VHD'yi karşıya**.

    ![PowerShell kullanarak VHD karşıya yükle](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. Merhaba **PowerShell kullanarak bir görüntüyü karşıya yüklemeden** dikey penceresinde görüntüler çağrısı toohello **Ekle AzureVhd** cmdlet'i. İlk parametre hello (*hedef*) blob kapsayıcısı için URI hello içerir (*yükler*) biçimi aşağıdaki hello içinde:

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. Merhaba Not daha sonraki adımlarda kullanılmak üzere tam URI.

1. AzCopy kullanarak hello VHD dosyasını karşıya yükle:
 
1. [Merhaba en güncel AzCopy sürümünü karşıdan yükleyip](http://aka.ms/downloadazcopy).

1. Bir komut penceresi açın ve toohello AzCopy yükleme dizinine gidin. İsteğe bağlı olarak, hello AzCopy yükleme konumu tooyour sistem yolu ekleyebilirsiniz. Varsayılan olarak, AzCopy yüklü toohello directory aşağıdaki gibidir:

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. Merhaba depolama hesabı anahtarı ve blob kapsayıcısı URI kullanarak, komut hello komut isteminde aşağıdaki hello çalıştırın. Merhaba *vhdFileName* değeri tırnak toobe gerekiyor. VHD dosyasını karşıya yükleme işleminin hello hello hello VHD dosyasının boyutunu ve bağlantı hızınıza bağlı olarak uzun olabilir.   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a>Sonraki adımlar

- [Azure DevTest Labs hello Azure portal kullanarak bir VHD dosyasında özel bir görüntü oluşturun](devtest-lab-create-template.md)
- [Azure DevTest Labs PowerShell kullanarak bir VHD dosyasında özel bir görüntü oluşturun](devtest-lab-create-custom-image-from-vhd-using-powershell.md)