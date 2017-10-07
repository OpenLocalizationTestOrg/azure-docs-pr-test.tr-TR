---
title: "aaaAdd sahipleri ve Azure DevTest Labs kullanıcılar | Microsoft Docs"
description: "Hello Azure portal veya PowerShell kullanarak Azure DevTest Labs içinde sahipleri ve kullanıcılar ekleme"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a>Azure DevTest Labs'de sahipleri ve kullanıcılar ekleme
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

Azure DevTest Labs Access'te tarafından denetlenir [Azure rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-what-is.md). RBAC kullanarak, ekibiniz içinde içinde görevlerini ayırabilirsiniz *rolleri* burada verdiğiniz yalnızca hello miktarını erişim gerekli toousers tooperform işlerini. Üç RBAC rolde olan *sahibi*, *DevTest Labs kullanıcı*, ve *katkıda bulunan*. Bu makalede, hangi eylemlerin her hello üç ana RBAC rolü gerçekleştirilebilir öğrenin. Buradan, nasıl tooadd kullanıcılar tooa Laboratuvar - aracılığıyla her ikisi de hello öğrenin portal ve farklı bir PowerShell Betiği ve nasıl tooadd kullanıcılar abonelik düzeyinde hello aracılığıyla.

## <a name="actions-that-can-be-performed-in-each-role"></a>Her rol gerçekleştirilen eylemler
Bir kullanıcı atayabilirsiniz üç ana rol vardır:

* Sahip
* DevTest Labs kullanıcı
* Katılımcı

Merhaba aşağıdaki tabloda bu rollerin her biri bulunan kullanıcılar tarafından gerçekleştirilen hello Eylemler gösterilmektedir:

| **Bu roldeki kullanıcılar eylemleri gerçekleştirebilirsiniz** | **DevTest Labs kullanıcı** | **Sahibi** | **Katkıda bulunan** |
| --- | --- | --- | --- |
| **Laboratuvar görevleri** | | | |
| Kullanıcıların tooa Laboratuvar ekleme |Hayır |Yes |Hayır |
| Maliyet ayarlarını güncelleştirme |Hayır |Evet |Evet |
| **VM temel görevleri** | | | |
| Özel resimler ekleyip |Hayır |Evet |Evet |
| Ekleme, güncelleştirme ve formülleri silme |Evet |Evet |Evet |
| Beyaz liste Azure Marketi görüntüleri |Hayır |Evet |Evet |
| **VM görevleri** | | | |
| VM oluşturma |Evet |Evet |Evet |
| Başlatma, durdurma ve sanal makineleri silin |Yalnızca Hello kullanıcı tarafından oluşturulan sanal makineleri |Evet |Evet |
| VM ilkelerini güncelleştirme |Hayır |Evet |Evet |
| Veri diskleri için/VMs Ekle/Kaldır |Yalnızca Hello kullanıcı tarafından oluşturulan sanal makineleri |Evet |Evet |
| **Yapı görevleri** | | | |
| Ekleme ve yapı depoları kaldırma |Hayır |Evet |Evet |
| Yapıları Uygula |Evet |Evet |Evet |

> [!NOTE]
> Bir kullanıcı bir VM oluşturduğunda, bu kullanıcının toohello otomatik olarak atanır **sahibi** VM oluşturulan hello rolü.
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a>Merhaba Laboratuvar düzeyinde sahibi veya kullanıcı ekleyin
Sahipleri ve kullanıcıların hello Laboratuvar düzeyinde hello Azure portal aracılığıyla eklenebilir. Bu geçerli bir dış kullanıcılarla içerir [Microsoft hesabı (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).
Aşağıdaki adımları hello Azure DevTest Labs'de bir sahibi veya kullanıcı tooa Laboratuvar ekleme hello işleminde size kılavuzluk eder:

1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Seçin **daha fazla hizmet**ve ardından **DevTest Labs** hello listeden.
3. Merhaba istenen Laboratuvar labs Hello listeden seçin.
4. Merhaba Laboratuvar'ın dikey penceresinde, seçin **yapılandırma**. 
5. Merhaba üzerinde **yapılandırma** dikey penceresinde, select **kullanıcılar**.
6. Merhaba üzerinde **kullanıcılar** dikey penceresinde, select **+ Ekle**.
   
    ![Kullanıcı ekle](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. Merhaba üzerinde **bir rol seçin** dikey penceresinde, select hello istenen rol. Merhaba bölüm [her rolünde gerçekleştirilen eylemler](#actions-that-can-be-performed-in-each-role) listeleri hello hello sahibi, DevTest kullanıcı ve katkıda bulunan rollerinin bulunan kullanıcılar tarafından gerçekleştirilen çeşitli eylemler.
8. Merhaba üzerinde **kullanıcıları eklemek** dikey penceresinde hello e-posta adresi veya belirttiğiniz hello rolündeki tooadd istediğiniz hello kullanıcı adı girin. Merhaba kullanıcı bulunamazsa, bir hata iletisi hello sorun açıklanmaktadır. Merhaba kullanıcı bulunursa, o kullanıcı listelenen ve seçili. 
9. Seçin **seçin**.
10. Seçin **Tamam** tooclose hello **erişim Ekle** dikey.
11. Toohello döndüğünüzde **kullanıcılar** dikey penceresinde hello kullanıcı eklendi.  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a>PowerShell kullanarak bir dış kullanıcı tooa Laboratuvar ekleme
Ayrıca tooadding kullanıcılar'hello Azure portal'ın bir PowerShell komut dosyası kullanarak bir dış kullanıcı tooyour laboratuvarı ekleyebilirsiniz. Hello hello altında hello parametre değerleri yalnızca değiştirme örneği, aşağıdaki **değerleri toochange** açıklama.
Merhaba alabilir `subscriptionId`, `labResourceGroup`, ve `labName` hello Laboratuvar dikey penceresinde hello Azure portal değerleri.

> [!NOTE]
> Kullanıcı Konuk toohello Active Directory eklendi ve hello durumda değilse, başarısız olur, hello belirtilen Hello örnek betik varsayar. tooadd hello Active Directory tooa Laboratuvar olmayan bir kullanıcı hello bölümünde gösterildiği gibi hello Azure portal tooassign hello kullanıcı tooa rolü kullanmak [sahibi veya kullanıcı hello Laboratuvar düzeyinde ekleme](#add-an-owner-or-user-at-the-lab-level).   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a>Merhaba abonelik düzeyinde sahibi veya kullanıcı ekleyin
Azure izinleri üst kapsam toochild kapsamdan Azure yayılır. Dolayısıyla, labs içeren Azure aboneliği sahipleri, otomatik olarak bu labs sahipleri altındadır. Ayrıca hello VM'ler ve hello Laboratuvar'ın kullanıcılar hello Azure DevTest Labs hizmeti tarafından oluşturulan ve diğer kaynaklara sahip. 

Hello hello Laboratuvar'ın dikey penceresi aracılığıyla ek sahipleri tooa Laboratuvar ekleyebilirsiniz [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040). Ancak, hello sahibinin yönetim kapsamını hello abonelik sahibinin kapsamı daha dar eklenir. Örneğin, hello sahipleri hello abonelikte hello DevTest Labs hizmeti tarafından oluşturulan hello kaynakların tam erişim toosome yok eklendi. 

tooadd sahibi tooan Azure aboneliği, şu adımları izleyin:

1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Seçin **daha Hizmetleri**ve ardından **abonelikleri** hello listeden.
3. İstenen hello aboneliği seçin.
4. Seçin **erişim** simgesi. 
   
    ![Erişim kullanıcıları](./media/devtest-lab-add-devtest-user/access-users.png)
5. Merhaba üzerinde **kullanıcılar** dikey penceresinde, select **Ekle**.
   
    ![Kullanıcı ekle](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. Merhaba üzerinde **bir rol seçin** dikey penceresinde, seçin **sahibi**.
7. Merhaba üzerinde **kullanıcıları eklemek** dikey penceresinde hello e-posta adresi veya adı girin hello kullanıcısı sahibi olarak tooadd istiyor. Merhaba kullanıcı bulunamazsa, hello sorunu açıklayan bir hata iletisi alırsınız. Merhaba kullanıcı bulunursa, o kullanıcı hello altında listelenen **kullanıcı** metin kutusu.
8. Merhaba bulunduğu kullanıcı adını seçin.
9. Seçin **seçin**.
10. Seçin **Tamam** tooclose hello **erişim Ekle** dikey.
11. Toohello döndüğünüzde **kullanıcılar** dikey penceresinde hello kullanıcı sahibi olarak eklendi. Bu kullanıcı artık bu abonelik altında oluşturulan labs sahibi ve böylece mümkün tooperform sahibi görevler. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

