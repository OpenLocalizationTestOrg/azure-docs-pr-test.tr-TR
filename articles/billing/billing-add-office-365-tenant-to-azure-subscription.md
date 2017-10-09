---
title: "Azure aboneliği ile aaaUse bir Office 365 Kiracı | Microsoft Docs"
description: "Bilgi nasıl tooadd bir Office 365 dizin (Kiracı) tooan Azure aboneliği."
services: 
documentationcenter: 
author: JiangChen79
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: cc9c57c6-7bfd-4dea-9027-c75ef3737589
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: cjiang
ms.openlocfilehash: e560370417bd074a7e37ceb7c60da45dbbbcf775
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="associate-an-office-365-tenant-tooan-azure-subscription"></a>Office 365 Kiracı tooan Azure aboneliği ilişkilendirme
Merhaba Office 365 Kiracı Azure aboneliğinizden erişebilmesi için ayrı Azure ve Office 365 abonelikleri bağlayın. hello Azure hizmeti yönetici hesabı ile tooAzure toolink oturum aboneliklerinizi, bir dizin ekleyin ve hello Office 365 Kurumsal hesaplar toohello Azure Active Directory Kiracı ekleyin.

Azure Active Directory örneğinizi kullanıcıları için Office 365 aboneliğiniz istediğiniz veya Office 365 hesabı ancak bir Azure hesabınız varsa, bkz: [kaydolmak için Azure ile Office 365 hesabı](billing-use-existing-office-365-account-azure-subscription.md). 

## <a name="before-you-begin"></a>Başlamadan önce
* Merhaba hello Azure aboneliği Hizmet Yöneticisi kimlik bilgileri olması gerekir. Ortak yönetici hesapları, bu makaledeki adımları hello bazıları yapamazsınız. toochange hizmet yöneticinize bkz [nasıl tooadd ya da değişiklik Azure yönetici rolleri](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).
* Genel yöneticinin hello Office 365 Kiracı hello kimlik bilgileri olması gerekir.
* hello hizmet yöneticisinin Hello e-posta adresini hello Office 365 Kiracı içinde olması gerekir.
* hello hizmet yöneticisinin Hello e-posta adresini, herhangi bir genel yönetici hello Office 365 Kiracı eşleşmesi gerekmez.
* Geçici olarak bir Microsoft hesabı ve bir kurumsal hesap bir e-posta adresi kullanıyorsanız, başka bir Microsoft hesabı hello hizmet yöneticisine, Azure aboneliği toouse değiştirin. Merhaba bir Microsoft hesabı oluşturabilirsiniz [Microsoft hesabı kaydolma sayfası](https://signup.live.com/).

## <a name="link-office-365-tenant-tooazure-subscription"></a>Office 365 Kiracı tooAzure aboneliği bağlama
tooassociate hello Office 365 Kiracı toohello Azure aboneliği, şu adımları izleyin:

### <a name="step-1-add-office-365-tenant-tooyour-azure-subscription"></a>1. adım: Office 365 Kiracı tooyour Azure aboneliği ekleme

1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com/) hello hizmet yönetici kimlik bilgilerine sahip.

    ![Ekran görüntüsü, Azure oturum açma](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. Merhaba sol bölmesinde seçin **ACTIVE DIRECTORY**. Merhaba Office 365 Kiracı görmemesi. Görmüyorsanız, çok atla[2. adım: hello Azure aboneliği ile ilişkili değişiklik hello dizini](#Step2).
   
   ![Active Directory ekran girişi](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. Seçin **yeni** > **DIRECTORY** > **özel Oluştur**.
   
    ![Ekran görüntüsü, Azure Active Directory özel oluştur](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. Merhaba üzerinde **Dizin Ekle** sayfasında **DIRECTORY**seçin **var olan dizini kullan**. Ardından **şimdi oturumu kapattınız hazır toobe ben**seçip **tam** ![tamamlamak simgesi](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).
   
    !["Var olan dizini kullan" ekran görüntüsü](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. Oturumu kapattınız sonra Office 365 kiracınız hello genel yönetici kimlik bilgilerinizle oturum açın.
   
    ![Office 365 ekran genel yönetici oturum açma](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. Seçin **devam**.
   
    ![Doğrulama ekran görüntüsü](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. Seçin **şimdi oturumu**.
   
    ![Ekran görüntüsü oturum kapatma](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com/) hello hizmet yönetici kimlik bilgilerine sahip.
   
    ![Ekran görüntüsü, Azure oturum açma](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. Office 365 kiracınız hello panosunda görmeniz gerekir.
   
    ![Panosunun ekran görüntüsü](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <a name="Step2"></a>2. adım: hello Azure aboneliği ile ilişkili değişiklik hello dizini
   
1. Seçin **ayarları**.
   
    ![Ekran görüntüsü, Azure Klasik Portalı Ayarları simgesi](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. Azure aboneliğinizi seçin ve ardından **dizini Düzenle**.

    ![Ekran görüntüsü, Azure abonelik düzenleme dizin](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. Seçin **sonraki** ![sonraki simgeyi](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).
   
    !["Değişiklik hello ilişkili dizin" işleminin ekran görüntüsü](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. Etkilenen hello hesapları gözden geçirin. Tüm ortak Yöneticiler ve [rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-configure.md) hello mevcut kaynak gruplarındaki atanan erişimi olan kullanıcılar kaldırılır. Merhaba uyarı aldığınız yalnızca ortak Yöneticiler hello kaldırılmasını tanımlamıştır.
      
    ![Ortak yönetici hesapları toobe kaldırılan hello gösteren ekran görüntüsü.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Bir örnek kullanıcı hesabı toobe gösteren ekran görüntüsü kaldırıldı.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. Seçin **tam** ![tamamlamak simgesi](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-toohello-azure-active-directory-tenant"></a>3. adım: ortak Yöneticiler toohello Azure Active Directory Kiracı olarak, Office 365 Kurumsal hesapları ekleme
   
1. Select hello **Yöneticiler** sekmesini tıklatın ve ardından **eklemek**.
   
    ![Ekran görüntüsü, Azure Klasik portalı ayarlarını Yöneticiler sekmesi](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. Office 365 kiracınızın kurumsal bir hesap girin, hello Azure aboneliği seçin ve ardından **tam** ![tamamlamak simgesi](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).
   
    ![Ekran görüntüsü, Azure ortak yönetici iletişim kutusu ekleme](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. Toohello dönün **Yöneticiler** sekmesi. Ortak yönetici olarak görüntülenen hello kuruluş hesabı görmeniz gerekir.
   
    ![Yöneticiler sekmesi ekran görüntüsü](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  Test erişim tooAzure hello ortak yönetici hesabıyla.
   
    a. Merhaba dışında Klasik Azure portalında oturum açın.
   
    b. Açık hello [Azure portal](https://portal.azure.com/).
   
    c. Merhaba hello ortak yönetici kimlik bilgilerini girin ve ardından **oturum**.
   
    ![Ekran görüntüsü, Azure oturum açma sayfası](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a>Yardım mı gerekiyor? Desteğe başvurun.
Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) sorunu Çözümlendi hızla tooget.


