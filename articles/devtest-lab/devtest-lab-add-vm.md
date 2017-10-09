---
title: Azure DevTest Labs VM tooa laboratuvarda aaaAdd | Microsoft Docs
description: "Bilgi nasıl tooadd Azure DevTest Labs bir sanal makine tooa laboratuvarda"
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
ms.date: 02/24/2017
ms.author: tarcher
ms.openlocfilehash: 82838e4349550db56de311264c188140b9556b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-vm-tooa-lab-in-azure-devtest-labs"></a>Azure DevTest Labs'de VM tooa Laboratuvar ekleme
Zaten varsa [ilk VM oluşturulan](devtest-lab-create-first-vm.md), büyük olasılıkla bunu bir önceden yüklenmiş yaptığınız [Market görüntüsü](devtest-lab-configure-marketplace-images.md). Şimdi, tooadd sonraki VM'ler tooyour Laboratuvar isterseniz, ayrıca seçebileceğiniz bir *temel* ya da başka bir deyişle bir [özel görüntü](devtest-lab-create-template.md) veya [formülü](devtest-lab-manage-formulas.md). Bu öğreticide Azure portal tooadd VM tooa Laboratuvar hello DevTest Labs'de kullanılarak üzerinden açıklanmaktadır.

Bu makalede ayrıca nasıl toomanage hello yapıları laboratuvarınızda bir VM için gösterilmektedir.

## <a name="steps-tooadd-a-vm-tooa-lab-in-azure-devtest-labs"></a>Adımları tooadd Azure DevTest Labs VM tooa laboratuvarda
1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.
1. Labs Hello listeden toocreate hello VM istediğiniz hello Laboratuvar seçin.  
1. Merhaba Laboratuvar'ın üzerinde **genel bakış** dikey penceresinde, select **+ Ekle**.  

    ![VM düğme ekleme](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. Merhaba üzerinde **bir temel seçin** dikey penceresinde hello VM için temel bir seçin.
1. Merhaba üzerinde **sanal makine** dikey penceresinde hello hello yeni bir sanal makine için bir ad girin **sanal makine adı** metin kutusu.

    ![Laboratuvar VM dikey penceresi](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. Girin bir **kullanıcı adı** hello sanal makinede yönetici ayrıcalıkları verilmiş.  
1. Toouse istiyorsanız bir parola depolanır, [gizli deposu](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)seçin **kaydedilmiş gizliliği kullanın**ve tooyour gizliliği (parola) karşılık gelen bir anahtar değeri belirtin. Aksi halde, bir parola etiketli hello metin alanına **bir değer yazın**.
1. Merhaba **sanal makine disk türü** hello laboratuarda hello sanal makineler için hangi depolama disk türüne izin belirler.
1. Seçin **sanal makine boyutu** ve hello birini seçin hello işlemci çekirdeği, RAM boyutu ve sabit sürücü boyutu hello VM toocreate hello belirtin öğeleri önceden tanımlanmış.
1. Seçin **yapıları** - - yapılarının hello listesinden seçin ve tooadd toohello temel görüntü istediğiniz hello yapıları yapılandırın.
    **Not:** yeni tooDevTest Labs olduğunuz ya da yapılar yapılandırma toohello başvurmak [var artifact tooa VM eklemek](#add-an-existing-artifact-to-a-vm) bölümünde ve ardından bitirdikten sonra buraya dönün.
1. Seçin **Gelişmiş ayarları** tooconfigure hello VM'in ağ seçenekleri ve sona erme tarihi seçenekleri. 

   tooset bir sona erme seçenek üzerinde VM hello tarih otomatik olarak silinir hello Takvim simgesi toospecify seçin.  Varsayılan olarak, hello VM asla sona erecek. 
1. Tooview istediğiniz veya kopyalarsanız hello Azure Resource Manager şablonu toohello başvuran [Kaydet Azure Resource Manager şablonu](#save-azure-resource-manager-template) bölümünde ve bittiğinde buraya dönün.
1. Seçin **oluşturma** tooadd hello belirtilen VM toohello Laboratuvar.
1. Merhaba Laboratuvar dikey görüntüler hello VM'in oluşturma - hello durumunu ilk olarak **oluşturma**, ardından olarak **çalıştıran** VM başlatıldığında hello sonra.

> [!NOTE]
> [Claimable VM eklemek](devtest-lab-add-claimable-vm.md) nasıl toomake hello VM claimable hello laboratuarda herhangi bir kullanıcı tarafından kullanılmak üzere kullanılabilir olduğunu gösterir.
>
>

## <a name="add-an-existing-artifact-tooa-vm"></a>Varolan bir yapı tooa VM ekleme
Bir VM oluştururken, varolan yapıları ekleyebilirsiniz. Her Laboratuvar hello ortak DevTest Labs Yapıt deposu yapılardan yanı sıra, oluşturduğunuz ve eklenen tooyour kendi Yapıt deposu yapıları içerir.

* Azure DevTest Labs *yapıları* belirlemenize olanak *Eylemler* hello VM Windows PowerShell komut dosyası çalıştırarak, Bash komutlarını çalıştırarak ve yazılım yükleme gibi sağlandığında gerçekleştirilir.
* Yapı *parametreleri* hello yapı belirli senaryonuz için özelleştirmenize olanak tanır

nasıl toocreate yapıları görmek toodiscover hello makalenin [tooauthor kendi yapıtlar için DevTest Labs ile kullanma hakkında bilgi edinin](devtest-lab-artifact-author.md).

1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.
1. Labs Hello listeden toowork istediğiniz hello VM'yi içeren hello Laboratuvar seçin.  
1. Seçin **My sanal makineleri**.
1. Select hello VM istenen.
1. Seçin **yapıları**. 
1. Seçin **yapıları uygulamak**.
1. Merhaba üzerinde **yapıları uygulamak** dikey penceresinde, select hello yapı tooadd toohello VM istiyor.
1. Merhaba üzerinde **ekleyin yapıt** dikey penceresinde hello gerekli parametre değerlerini ve gereken isteğe bağlı parametreleri girin.  
1. Seçin **Ekle** tooadd hello yapı ve return toohello **yapıları uygulamak** dikey.
1. Yapılar, VM için gerektiği şekilde ekleme devam edin.
1. Yapıtları ekledikten sonra [hangi hello yapıları çalıştırılır hello sırasını değiştirmek](#change-the-order-in-which-artifacts-are-run). Ayrıca çok dönebilirsiniz[görüntülemek veya bir yapı değiştirmek](#view-or-modify-an-artifact).
1. Ekleme yapıları bittiğinde, seçin **Uygula**

## <a name="change-hello-order-in-which-artifacts-are-run"></a>Yapıları çalıştırdığınız hello sırasını değiştirme
Varsayılan olarak, hello Eylemler hello yapılarının toohello VM eklenen hello sırada yürütülür. Merhaba aşağıdaki adımları nasıl toochange hello hangi hello yapıları çalıştırılan sipariş gösterilmektedir.

1. Merhaba hello üstündeki **yapıları uygulamak** dikey penceresinde, toohello VM eklenen yapıları hello sayısını gösteren select hello bağlantı.
   
    ![Yapıları eklenen tooVM sayısı](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. Merhaba üzerinde **seçili yapıları** dikey penceresinde, sürükle ve bırak hello yapıları hello içine istenen sırası. **Not:** hello yapı sürükleyerek sorun yaşıyorsanız, sol hello yapı tarafı hello sürükleyerek emin olun. 
1. Tamamladığınızda **Tamam**’ı seçin.  

## <a name="view-or-modify-an-artifact"></a>Görüntüleme veya bir yapı değiştirme
Merhaba aşağıdaki adımları göstermek nasıl tooview veya bir yapının hello parametreleri değiştirin:

1. Merhaba hello üstündeki **yapıları uygulamak** dikey penceresinde, toohello VM eklenen yapıları hello sayısını gösteren select hello bağlantı.
   
    ![Yapıları eklenen tooVM sayısı](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. Merhaba üzerinde **seçili yapıları** dikey penceresinde, tooview istediğiniz veya düzenleme select hello yapı.  
1. Merhaba üzerinde **ekleyin yapıt** dikey penceresinde, tüm değişikliklerin gerekli ve seçin yapma **Tamam** tooclose hello **ekleyin yapıt** dikey.
1. Seçin **Tamam** tooclose hello **seçili yapıları** dikey.

## <a name="save-azure-resource-manager-template"></a>Azure Resource Manager şablonunu Kaydet
Bir Azure Resource Manager şablonu tekrarlanabilir bir dağıtım bir bildirim temelli şekilde toodefine sağlar. Aşağıdaki adımları hello nasıl toosave hello hello oluşturulan VM için Azure Resource Manager şablonu açıklanmaktadır.
Kaydedildikten sonra hello Azure Resource Manager şablonu kullanabileceğine[Azure PowerShell ile yeni VM'ler dağıtmak](../azure-resource-manager/resource-group-overview.md#template-deployment).

1. Merhaba üzerinde **sanal makine** dikey penceresinde, select **ARM şablonu görüntüleme**.
2. Merhaba üzerinde **görünüm Azure Resource Manager şablonu** dikey penceresinde, select hello şablon metni.
3. Merhaba seçili metni toohello panoya kopyalayın.
4. Seçin **Tamam** tooclose hello **görünüm Azure Resource Manager şablonu dikey**.
5. Bir metin düzenleyicisinde açın.
6. Hello Pano'dan hello şablon metni yapıştırın.
7. Daha sonra kullanmak için Hello dosyasını kaydedin.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>Sonraki adımlar
* Bir kez VM oluşturulan hello toohello VM seçerek bağlayabilirsiniz **Bağlan** hello VM'in dikey.
* Nasıl çok öğrenin[DevTest Labs VM için özel yapılar oluşturma](devtest-lab-artifact-author.md).
* Merhaba keşfedin [DevTest Labs Azure Resource Manager hızlı başlangıç Şablon Galerisi](https://github.com/Azure/azure-devtestlab/tree/master/Samples).
