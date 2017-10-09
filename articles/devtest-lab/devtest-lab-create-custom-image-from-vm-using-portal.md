---
title: "Azure DevTest Labs özel görüntüyü bir VM'den aaaCreate | Microsoft Docs"
description: "Nasıl toocreate sağlanan bir VM kullanarak Azure DevTest Labs özel bir görüntü hello Azure portal öğrenin"
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
ms.openlocfilehash: 7dccb79d3db4aae676c7bd2f6b800301210491e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vm"></a>Bir sanal makineden özel bir görüntü oluşturun

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a>Adım adım yönergeler

Sağlanan bir sanal makineden özel bir görüntü oluşturun ve daha sonra bu özel görüntü toocreate kullanın aynı VM'ler. Aşağıdaki adımları hello nasıl toocreate özel bir görüntü bir VM'den gösterilmiştir:

1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Seçin **daha fazla hizmet**ve ardından **DevTest Labs** hello listeden.

1. Merhaba istenen Laboratuvar labs Hello listeden seçin.  

1. Merhaba Laboratuvar'ın dikey penceresinde, seçin **My sanal makineleri**.
 
1. Merhaba üzerinde **My sanal makineleri** dikey penceresinde, toocreate hello özel görüntü istediğiniz select hello VM.

1. Merhaba VM'in dikey penceresinde, seçin **oluşturma özel görüntü (VHD)**.

    ![Özel görüntü menü öğesi oluşturma](./media/devtest-lab-create-template/create-custom-image.png)

1. Merhaba üzerinde **oluşturma görüntü** dikey penceresinde, bir ad ve özel görüntünüzü açıklamasını girin. Bir VM oluşturduğunuzda, bu bilgileri hello tabanları listesinde görüntülenir.

    ![Özel görüntü dikey penceresi oluşturma](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. Sysprep hello VM üzerinde çalıştırıldığı olup olmadığını seçin. Merhaba sysprep hello VM üzerinde çalıştırılmadı, sysprep bu özel görüntüsünü bir VM oluşturulduğunda çalıştırmak isteyip istemediğinizi belirtin.

1. Seçin **Tamam** ne zaman sona toocreate hello özel görüntü.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>İlgili blog gönderileri

- [Özel resimler veya formüller?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Azure DevTest Labs arasında özel resimler kopyalama](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Sonraki adımlar

- [VM tooyour Laboratuvar ekleme](./devtest-lab-add-vm-with-artifacts.md)
