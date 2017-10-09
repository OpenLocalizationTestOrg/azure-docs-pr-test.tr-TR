---
title: "Azure DevTest Labs özel görüntüyü bir VHD dosyasından aaaCreate | Microsoft Docs"
description: "Nasıl toocreate VHD dosyasını kullanarak Azure DevTest Labs özel bir görüntü hello Azure portal öğrenin"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: b795bc61-7c28-40e6-82fc-96d629ee0568
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 80af8ea1cb72380f868df0a76c4a0dcd92e63cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a>Bir VHD dosyasındaki özel bir görüntü oluşturun

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a>Adım adım yönergeler

Merhaba aşağıdaki adımlar, özel bir görüntü hello Azure portal kullanarak bir VHD'yi dosyasından oluşturmada size yol:

1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Seçin **daha fazla hizmet**ve ardından **DevTest Labs** hello listeden.

1. Merhaba istenen Laboratuvar labs Hello listeden seçin.  

1. Merhaba Laboratuvar'ın dikey penceresinde, seçin **yapılandırma**. 

1. Merhaba Laboratuvar üzerinde **yapılandırma** dikey penceresinde, select **özel görüntülerini (VHD)**.

1. Merhaba üzerinde **özel görüntüleri** dikey penceresinde, select **+ Ekle**.

    ![Özel görüntü ekleme](./media/devtest-lab-create-template/add-custom-image.png)

1. Merhaba özel görüntü Hello adını girin. Bu ad, bir VM oluşturulurken hello temel görüntü listesinde görüntülenir.

1. Merhaba özel görüntü Hello açıklamasını girin. Bu açıklama, bir VM oluşturulurken hello temel görüntü listesinde görüntülenir.

1. Seçin **VHD**.

1. Merhaba gelen **VHD** dikey penceresinde, istenen select hello VHD dosyası.

1. Seçin **Tamam** tooclose hello **VHD** dikey.

1. Seçin **işletim sistemi yapılandırması**.

1. Merhaba üzerinde **işletim sistemi yapılandırması** sekmesinde, ya da seçin **Windows** veya **Linux**.

1. Varsa **Windows** olan hello onay kutusu seçildiyse olup olmadığını *Sysprep* hello makinede çalıştırın. 

1. Seçin **Tamam** tooclose hello **işletim sistemi yapılandırması** dikey.

1. Seçin **Tamam** toocreate hello özel görüntü.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>İlgili blog gönderileri

- [Özel resimler veya formüller?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Azure DevTest Labs arasında özel resimler kopyalama](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Sonraki adımlar

- [VM tooyour Laboratuvar ekleme](./devtest-lab-add-vm-with-artifacts.md)
