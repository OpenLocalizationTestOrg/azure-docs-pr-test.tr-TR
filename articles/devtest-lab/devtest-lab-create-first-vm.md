---
title: aaaCreate ilk VM'nizi Azure DevTest Labs laboratuvarda | Microsoft Docs
description: "Bilgi nasıl toocreate ilk sanal makinenizde bir laboratuar ortamında Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: fbc5a438-6e02-4952-b654-b8fa7322ae5f
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2017
ms.author: tarcher
ms.openlocfilehash: 4c3257efca9be6fdd190eaac1db731464e07fcfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a>Azure DevTest Labs laboratuvarda ilk VM oluşturma

Başlangıçta DevTest Labs erişmek ve ilk VM toocreate istediğiniz zaman, büyük olasılıkla bunu önceden yüklenmiş kullanarak yapacağınız [temel Market görüntüsü](devtest-lab-configure-marketplace-images.md). Daha sonra gelen mümkün toochoose de bir [özel görüntü ve bir formül](devtest-lab-add-vm.md) daha fazla sanal makineleri oluştururken. 

Bu öğreticide, Azure portal tooadd hello kullanılarak üzerinden ilk VM tooa laboratuvarınızda DevTest Labs açıklanmaktadır.

## <a name="steps-tooadd-your-first-vm-tooa-lab-in-azure-devtest-labs"></a>İlk VM tooa laboratuvarınızda Azure DevTest Labs tooadd adımları
1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.
1. Labs Hello listeden toocreate hello VM istediğiniz hello Laboratuvar seçin.  
1. Merhaba Laboratuvar'ın üzerinde **genel bakış** dikey penceresinde, select **+ Ekle**.  

    ![VM düğme ekleme](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. Merhaba üzerinde **bir temel seçin** bir Market görüntü dikey penceresinde, select hello VM.
1. Merhaba üzerinde **sanal makine** dikey penceresinde hello hello yeni bir sanal makine için bir ad girin **sanal makine adı** metin kutusu.

    ![Laboratuvar VM dikey penceresi](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. Girin bir **kullanıcı adı** hello sanal makinede yönetici ayrıcalıkları verilmiş.  
1. Etiketli hello metin alanına bir parola girin **bir değer yazın**.
1. Merhaba **sanal makine disk türü** hello laboratuarda hello sanal makineler için hangi depolama disk türüne izin belirler.
1. Seçin **sanal makine boyutu** ve hello birini seçin hello işlemci çekirdeği, RAM boyutu ve sabit sürücü boyutu hello VM toocreate hello belirtin öğeleri önceden tanımlanmış.
1. Seçin **yapıları** - - yapılarının hello listesinden seçin ve tooadd toohello temel görüntü istediğiniz hello yapıları yapılandırın.
    **Not:** yeni tooDevTest Labs olduğunuz ya da yapılar yapılandırma toohello başvurmak [var artifact tooa VM eklemek](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) bölümünde ve ardından bitirdikten sonra buraya dönün.
1. Seçin **oluşturma** tooadd hello belirtilen VM toohello Laboratuvar.

   Merhaba Laboratuvar dikey görüntüler hello VM'in oluşturma - hello durumunu ilk olarak **oluşturma**, ardından olarak **çalıştıran** VM başlatıldığında hello sonra.

## <a name="next-steps"></a>Sonraki adımlar
* Bir kez VM oluşturulan hello toohello VM seçerek bağlayabilirsiniz **Bağlan** hello VM'in dikey.
* Kullanıma [VM tooa Laboratuvar ekleme](devtest-lab-add-vm.md) sonraki VM'ler laboratuvarınızda ekleme hakkında daha ayrıntılı bilgi.
* Merhaba keşfedin [DevTest Labs Azure Resource Manager hızlı başlangıç Şablon Galerisi](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).
