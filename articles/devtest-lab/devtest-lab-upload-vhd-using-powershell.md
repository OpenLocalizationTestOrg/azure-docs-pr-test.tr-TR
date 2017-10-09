---
title: aaaUpload VHD tooAzure DevTest Labs PowerShell kullanarak dosya | Microsoft Docs
description: "PowerShell kullanarak VHD dosyasını toolab ait depolama hesabı karşıya yükle"
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
ms.openlocfilehash: 9c3ee96e212457b0ef8203714b419350cb97f895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-powershell"></a>PowerShell kullanarak VHD dosyasını toolab ait depolama hesabı karşıya yükle

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

Azure DevTest Labs'de VHD dosyaları kullanılan tooprovision sanal makinelerdir kullanılan toocreate özel resimler olabilir. Merhaba aşağıdaki adımlar, PowerShell tooupload kullanılarak üzerinden bir VHD dosyası tooa Laboratuvar ait depolama hesabı yol. VHD dosyasını yüklediğiniz sonra hello [bölüm'sonraki adımlar](#next-steps) nasıl toocreate hello özel bir görüntüden VHD dosyasını karşıya göstermeye bazı makaleleri listeler. Diskleri ve Azure içinde VHD'leri hakkında daha fazla bilgi için bkz: [diskler ve sanal makineler için VHD'ler hakkında](../virtual-machines/linux/about-disks-and-vhds.md)

## <a name="step-by-step-instructions"></a>Adım adım yönergeler

Merhaba aşağıdaki tooAzure DevTest Labs PowerShell kullanarak bir VHD'yi karşıya aracılığıyla dosyası ilerlemesi adımları. 

1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Seçin **daha fazla hizmet**ve ardından **DevTest Labs** hello listeden.

1. Merhaba istenen Laboratuvar labs Hello listeden seçin.  

1. Merhaba Laboratuvar'ın dikey penceresinde, seçin **yapılandırma**. 

1. Merhaba Laboratuvar üzerinde **yapılandırma** dikey penceresinde, select **özel görüntülerini (VHD)**.

1. Merhaba üzerinde **özel görüntüleri** dikey penceresinde, seçin **+ Ekle**. 

1. Merhaba üzerinde **özel görüntü** dikey penceresinde, select **VHD**.

1. Merhaba üzerinde **VHD** dikey penceresinde, select **PowerShell kullanarak bir VHD'yi karşıya**.

    ![PowerShell kullanarak VHD karşıya yükle](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. Merhaba üzerinde **PowerShell kullanarak bir görüntüyü karşıya yüklemeden** dikey penceresinde, kopya oluşturulan hello PowerShell komut dosyası tooa metin düzenleyici.

1. Merhaba değiştirme **LocalFilePath** hello parametresinin **Ekle AzureVhd** cmdlet toopoint toohello hello tooupload istediğiniz VHD dosyasının konumunu.

1. Merhaba bir PowerShell isteminde çalıştırın **Ekle AzureVhd** cmdlet (değiştiren hello ile **LocalFilePath** parametresi).

> [!WARNING] 
> 
> VHD dosyasını karşıya yükleme işleminin hello hello hello VHD dosyasının boyutunu ve bağlantı hızınıza bağlı olarak uzun olabilir.

## <a name="next-steps"></a>Sonraki adımlar

- [Azure DevTest Labs hello Azure portal kullanarak bir VHD dosyasında özel bir görüntü oluşturun](devtest-lab-create-template.md)
- [Azure DevTest Labs PowerShell kullanarak bir VHD dosyasında özel bir görüntü oluşturun](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
