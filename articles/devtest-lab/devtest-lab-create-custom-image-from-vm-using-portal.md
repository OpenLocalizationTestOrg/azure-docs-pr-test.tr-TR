---
title: "Bir sanal makineden Azure DevTest Labs özel görüntü oluşturma | Microsoft Docs"
description: "Azure DevTest Labs Azure portalını kullanarak sağlanan bir VM'den içinde özel bir görüntü oluşturmayı öğrenin"
services: devtest-lab,virtual-machines
documentationcenter: na
author: craigcaseyMSFT
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2018
ms.author: v-craic
ms.openlocfilehash: dc315bcc625ea98244bb5804ce6ff1c13d0ec7b1
ms.sourcegitcommit: 562a537ed9b96c9116c504738414e5d8c0fd53b1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/12/2018
---
# <a name="create-a-custom-image-from-a-vm"></a>Bir sanal makineden özel bir görüntü oluşturun

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a>Adım adım yönergeler

Sağlanan bir sanal makineden özel bir görüntü oluşturun ve daha sonra aynı VM'ler oluşturmak için özel görüntü kullanın. Aşağıdaki adımlar, bir VM'den özel bir görüntü oluşturmak nasıl çalışılacağını:

1. [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) oturum açın.

1. Seçin **tüm hizmetleri**ve ardından **DevTest Labs** listeden.

1. İstenen Laboratuvar labs listesinden seçin.  

1. Laboratuvar ait ana bölmede, seçin **My sanal makineleri**.
 
1. Üzerinde **My sanal makineleri** bölmesinde istediğiniz özel görüntü oluşturmak VM seçin.

1. VM'ın yönetim bölmesinde seçin **oluşturma özel görüntü (VHD)**.

    ![Özel görüntü menü öğesi oluşturma](./media/devtest-lab-create-template/create-custom-image.png)

1. Üzerinde **özel görüntü** bölmesinde, bir ad ve özel görüntünüzü açıklamasını girin. Bir VM oluşturduğunuzda, bu bilgileri tabanları listesinde görüntülenir.

    ![Özel görüntü bölmesi oluşturun](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. Sysprep VM üzerinde çalışan olup olmadığını seçin. Sysprep VM çalıştırılmadı, sysprep bu özel görüntüsünü bir VM oluşturulduğunda çalıştırmak isteyip istemediğinizi belirtin.

1. Seçin **Tamam** özel görüntü oluşturmak için bitirdikten sonra.

Birkaç dakika sonra özel görüntü oluşturulur ve Laboratuvar ait depolama hesabı içinde depolanır. Yeni bir VM oluşturmak bir laboratuvar kullanıcı istediği zaman, görüntü temel görüntü listesinde tarafından kullanılabilir.

![Özel görüntü temel görüntü listesinde kullanılabilir](./media/devtest-lab-create-template/custom-image-available-as-base.png)


[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>İlgili blog gönderileri

- [Özel resimler veya formüller?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Azure DevTest Labs arasında özel resimler kopyalama](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

## <a name="next-steps"></a>Sonraki adımlar

- [Laboratuvarınızı için bir VM ekleme](devtest-lab-add-vm.md)
