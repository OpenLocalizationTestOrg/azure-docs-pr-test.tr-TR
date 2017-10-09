---
title: "Azure DevTest Labs toocreate VM'ler aaaManage formüller | Microsoft Docs"
description: "Bilgi nasıl tooupdate ekleme ve kaldırma Azure DevTest Labs formüller"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 855debe46f3b70cc45ea5d55869663b64e225124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a>Azure DevTest Labs formüller yönetme

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

Bu makalede gösterilmektedir nasıl toocreate temel (özel görüntü, Market görüntüsü veya başka bir formül) veya mevcut bir VM'yi bir formül. Bu makalede ayrıca, varolan formüller yönetme aracılığıyla size yol gösterir.

## <a name="create-a-formula"></a>Formül oluşturma
DevTest Labs kimseyle *kullanıcıların* izinleri olan bir formül temel olarak kullanarak mümkün toocreate VM'ler. Toocreate formüller iki yolu vardır: 

* Merhaba formülü tüm hello özelliklerini toodefine istediğinizde bir taban - kullanın.
* Var olan Laboratuvar VM - formül mevcut bir VM'yi hello ayarlarınızı temel alan toocreate istediğinizde kullanın

Kullanıcılar ve izinler ekleme hakkında daha fazla bilgi için bkz: [Azure DevTest Labs'de sahipleri ve kullanıcılar ekleme](./devtest-lab-add-devtest-user.md).

### <a name="create-a-formula-from-a-base"></a>Formül bir taban oluşturma
Aşağıdaki adımları hello formül özel bir görüntü, Market görüntüsü ya da başka bir formül oluşturma hello işleminde size kılavuzluk eder.

1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).

2. Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.

3. Merhaba istenen Laboratuvar labs Hello listeden seçin.  

4. Merhaba Laboratuvar'ın dikey penceresinde, seçin **formüller (yeniden kullanılabilir tabanları)**.
   
    ![Formül menüsü](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. Merhaba üzerinde **formüller** dikey penceresinde, select **+ Ekle**.
   
    ![Formül ekleme](./media/devtest-lab-create-formulas/add-formula.png)

6. Merhaba üzerinde **bir temel seçin** dikey penceresinde, toocreate hello formülü istediğiniz select hello temel (özel görüntü, Market görüntüsünü veya formülü).
   
    ![Temel listesi](./media/devtest-lab-create-formulas/base-list.png)

7. Merhaba üzerinde **formül oluşturma** dikey penceresinde hello aşağıdaki değerleri belirtin:
   
    * **Formül adı** -formül için bir ad girin. Bu değer bir VM oluşturma hello temel görüntü listesinde görüntülenir. Merhaba adı yazdığınız ve geçerli değil, bir ileti için geçerli bir ad hello gereksinimleri gösterir doğrulanır.
    * **Açıklama** -formül için anlamlı bir açıklama girin. Bir VM oluştururken bu değeri hello formülün bağlam menüsünden kullanılabilir.
    * **Kullanıcı adı** -yönetici ayrıcalıkları verilmiş bir kullanıcı adı girin.
    * **Parola** - girin - veya hello aşağı açılır listeden seçin - toouse hello belirtilen kullanıcı için istediğiniz hello gizliliği (parola) ile ilişkili olan bir değer. Merhaba gizli anahtarları hakkında daha fazla bilgi için bkz: [Azure DevTest Labs: Kişisel gizli depolama](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).
    * **Sanal makine disk türü** - iki HDD (sabit disk sürücüsü) belirtin veya bu temel görüntü kullanılarak sağlanan hello sanal makineler için hangi depolama disk türü SSD (katı hal sürücüsü) tooindicate izin verilir.
    * ** Sanal makine boyutu ** - hello işlemci çekirdeği, RAM boyutu ve sabit sürücü boyutu hello VM toocreate hello belirtin önceden tanımlanmış hello öğeleri birini seçin. 
    * **Yapıları** -Select tooopen hello **yapıları eklemek** dikey penceresinde, seçin ve tooadd toohello temel görüntü istediğiniz hello yapıları yapılandırın. Yapılar hakkında daha fazla bilgi için bkz: [Azure DevTest Labs yönetmek VM yapıları](./devtest-lab-add-vm-with-artifacts.md).
    * **Gelişmiş ayarlar** -Select tooopen hello **Gelişmiş** hello ayarları aşağıdaki yapılandırdığınız dikey penceresinde:
        * **Sanal ağ** -hello istenen sanal ağ belirtin.
        * **Alt ağ** -hello istenen alt ağ belirtin.    
        * **IP adresi yapılandırması** -hello genel, özel veya paylaşılan IP adreslerini isteyip istemediğinizi belirtin. Paylaşılan IP adresleri hakkında daha fazla bilgi için bkz: [anlayın paylaşılan Azure DevTest Labs IP adresleri](./devtest-lab-shared-ip.md).
        * **Bu makineyi claimable hale** -bir makine "claimable" yapmadan anlamına gelir, sahipliği hello oluşturma sırasında atanması değil. Bunun yerine Laboratuvar kullanıcılar mümkün tootake sahipliği ("talep") hello makine hello Laboratuvar'ın dikey penceresinde olacaktır.     
    * **Görüntü** -Bu alan hello önceki dikey penceresinde hello temel görüntü seçtiğiniz adını görüntüler. 
     
       ![Formül oluşturma](./media/devtest-lab-create-formulas/create-formula.png)

8. Seçin **oluşturma** toocreate hello formül.

9. Merhaba formülü oluşturduğunuzda hello hello listesinde görüntüler **formüller** dikey.

### <a name="create-a-formula-from-a-vm"></a>Bir sanal makineden bir formül oluşturma
Merhaba aşağıdaki adımları var olan bir VM temelinde bir formül oluşturma hello işleminde size kılavuzluk. 

> [!NOTE]
> bir VM formülünden toocreate hello VM 30 Mart 2016'dan sonra oluşturulmuş olması gerekir. 
> 
> 

1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.
3. Merhaba istenen Laboratuvar labs Hello listeden seçin.  
4. Merhaba Laboratuvar'ın üzerinde **genel bakış** dikey penceresinde, select hello VM içinden istediğiniz toocreate hello formül.
   
    ![Labs VM'ler](./media/devtest-lab-create-formulas/my-vms.png)
5. Merhaba VM'in dikey penceresinde, seçin **formül (yeniden kullanılabilir temel) oluşturma**.
   
    ![Formül oluşturma](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. Merhaba üzerinde **formül oluşturma** dikey penceresinde girin bir **adı** ve **açıklama** için yeni formül.
   
    ![Formül dikey penceresi oluşturma](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. Seçin **Tamam** toocreate hello formül.

## <a name="modify-a-formula"></a>Bir formülü değiştirme
toomodify bir formül şu adımları izleyin:

1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.
3. Merhaba istenen Laboratuvar labs Hello listeden seçin.  
4. Merhaba Laboratuvar'ın dikey penceresinde, seçin **formüller (yeniden kullanılabilir tabanları)**.
   
    ![Formül menüsü](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. Merhaba üzerinde **Laboratuvar formüller** dikey penceresinde, select hello formül toomodify istiyor.
6. Merhaba üzerinde **güncelleştirme formülü** dikey penceresinde, istenen hello düzenlemeleri yapın ve seçin **güncelleştirme**.

## <a name="delete-a-formula"></a>Formül silme
toodelete bir formül şu adımları izleyin:

1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.
3. Merhaba istenen Laboratuvar labs Hello listeden seçin.  
4. Merhaba Laboratuvar üzerinde **ayarları** dikey penceresinde, select **formüller**.
   
    ![Formül menüsü](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. Merhaba üzerinde **Laboratuvar formüller** , dikey penceresinde, select hello üç nokta toohello hello formülü sağında toodelete istiyor.
   
    ![Formül menüsü](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. Merhaba formülün bağlam menüsünde seçin **silmek**.
   
    ![Formül bağlam menüsü](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. Seçin **Evet** toohello silme onayı iletişim.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>İlgili blog gönderileri
* [Özel resimler veya formüller?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a>Sonraki adımlar
Bir VM oluştururken kullanmak için bir formül oluşturduktan sonra hello sonraki çok adımdır[VM tooyour Laboratuvar ekleme](devtest-lab-add-vm-with-artifacts.md).

