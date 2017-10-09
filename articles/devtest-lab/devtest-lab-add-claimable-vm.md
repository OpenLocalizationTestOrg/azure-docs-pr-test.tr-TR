---
title: Azure DevTest Labs claimable bir VM tooa laboratuvarda aaaAdd | Microsoft Docs
description: "Bilgi nasıl tooadd Azure DevTest Labs claimable sanal makine tooa laboratuvarda"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: tarcher
ms.openlocfilehash: fe6385ae2e59b9636b82aec250dc3a1f8a40ba5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a>Azure DevTest Labs'de claimable VM tooa Laboratuvar ekleme
Bir benzer şekilde toohow claimable VM tooa Laboratuvar ekleme, [standart VM eklemek](devtest-lab-add-vm.md) – bir *temel* ya da başka bir deyişle bir [özel görüntü](devtest-lab-create-template.md), [formülü](devtest-lab-manage-formulas.md), veya [Market görüntüsü](devtest-lab-configure-marketplace-images.md). Bu öğretici DevTest Labs claimable bir VM tooa laboratuvarda hello Azure portal tooadd kullanılarak üzerinden anlatılmaktadır ve bir kullanıcının tooclaim hello VM izlediği hello işlemi gösterir.

> [!NOTE]
> Laboratuvar VM'ler aracılığıyla dağıtırsanız [Azure Resource Manager şablonları](devtest-lab-create-environment-from-arm.md), ayarı hello tarafından claimable VM'ler oluşturabilirsiniz **allowClaim** özelliği tootrue hello özellikler bölümünde.
>
>

## <a name="steps-tooadd-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a>Adımları tooadd Azure DevTest Labs claimable bir VM tooa laboratuvarda
1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.
1. Merhaba Laboratuvar labs Hello listeden seçin, istediğiniz toocreate hello claimable VM.  
1. Merhaba Laboratuvar'ın üzerinde **genel bakış** dikey penceresinde, select **+ Ekle**.  

    ![VM düğme ekleme](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. Merhaba üzerinde **bir temel seçin** dikey penceresinde hello VM için temel bir seçin.
1. Merhaba üzerinde **sanal makine** dikey penceresinde hello hello yeni bir sanal makine için bir ad girin **sanal makine adı** metin kutusu.

    ![Laboratuvar VM dikey penceresi](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. Girin bir **kullanıcı adı** hello sanal makinede yönetici ayrıcalıkları verilmiş.  
1. Toouse istiyorsanız bir parola depolanır, [gizli deposu](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)seçin **kaydedilmiş gizliliği kullanın**ve tooyour gizliliği (parola) karşılık gelen bir anahtar değeri belirtin. Aksi halde, bir parola etiketli hello metin alanına **bir değer yazın**.
1. Merhaba **sanal makine disk türü** hello laboratuarda hello sanal makineler için hangi depolama disk türüne izin belirler.
1. Seçin **sanal makine boyutu** ve hello birini seçin hello işlemci çekirdeği, RAM boyutu ve sabit sürücü boyutu hello VM toocreate hello belirtin öğeleri önceden tanımlanmış.
1. Seçin **yapıları** hello yapılarının, listeden seçin ve tooadd toohello temel görüntü istediğiniz hello yapıları yapılandırın. Yeni tooDevTest Labs olduğunuz ya da yapılar yapılandırma toohello başvurmak [var artifact tooa VM eklemek](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) bölümünde ve ardından bitirdikten sonra buraya dönün.
1. Seçin **Gelişmiş ayarları** tooconfigure hello VM'in ağ seçenekleri ve sona erme tarihi seçenekleri. Altında **talep seçenekleri**, seçin **Evet** toomake hello makine claimable.

  ![Toomake hello VM claimable seçin.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. Tooview istediğiniz veya kopyalarsanız hello Azure Resource Manager şablonu toohello başvuran [Kaydet Azure Resource Manager şablonu](devtest-lab-add-vm.md#save-azure-resource-manager-template) bölümünde ve bittiğinde buraya dönün.
1. Seçin **oluşturma** tooadd hello belirtilen VM toohello Laboratuvar.
1. Merhaba Laboratuvar dikey görüntüler hello VM'in oluşturma - hello durumunu ilk olarak **oluşturma**, ardından olarak **çalıştıran** VM başlatıldığında hello sonra.


## <a name="using-a-claimable-vm"></a>Claimable VM kullanma

Bir kullanıcı, aşağıdaki adımlardan birini yaparak "Claimable sanal makineler" Merhaba listesinden herhangi bir VM talep:

* Hello listesinde "Claimable sanal makinelerin" Merhaba Laboratuvar'ın genel bakış dikey penceresinde hello sonundaki hello VM'ler hello listesinde birine sağ tıklayın ve seçin **talep makine**.

 ![Belirli bir claimable VM'yi isteyin.](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* Merhaba hello üstündeki **genel bakış** dikey penceresinde, seçin **herhangi bir talep**. Rastgele bir sanal makine hello claimable VM'ler listesinden atanır.

 ![Tüm claimable VM isteyin.](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


Bir kullanıcı bir VM talep sonra kendi "Benim sanal makineler" listesine taşınır ve artık herhangi bir kullanıcı tarafından claimable değil.

## <a name="next-steps"></a>Sonraki adımlar
* Bir kez VM oluşturulan hello toohello VM seçerek bağlayabilirsiniz **Bağlan** hello VM'in dikey.
* Merhaba keşfedin [DevTest Labs Azure Resource Manager hızlı başlangıç Şablon Galerisi](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)
