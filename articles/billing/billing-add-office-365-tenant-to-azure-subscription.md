---
title: "Bir Office 365 Kiracı bir Azure aboneliği ile kullanma | Microsoft Docs"
description: "Bir Office 365 dizini (Kiracı) bir Azure aboneliğine eklemeyi öğrenin."
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
ms.openlocfilehash: 7affb4a83cdb8ababef60e786a3c824e7477ed68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="associate-an-office-365-tenant-to-an-azure-subscription"></a>Bir Azure aboneliği için bir Office 365 Kiracı ilişkilendirme
Office 365 Kiracı Azure aboneliğinizden erişebilmesi için ayrı Azure ve Office 365 abonelikleri bağlayın. Aboneliklerinizi bağlamak için Azure'da Azure Hizmet yöneticisi hesabı ile oturum açın, bir dizin ekleyin ve Office 365 Kurumsal hesaplar için Azure Active Directory Kiracı ekleyin.

Azure Active Directory örneğinizi kullanıcıları için Office 365 aboneliğiniz istediğiniz veya Office 365 hesabı ancak bir Azure hesabınız varsa, bkz: [kaydolmak için Azure ile Office 365 hesabı](billing-use-existing-office-365-account-azure-subscription.md). 

## <a name="before-you-begin"></a>Başlamadan önce
* Azure aboneliği Hizmet Yöneticisi kimlik bilgileri olması gerekir. Ortak yönetici hesapları, bu makaledeki adımları bazıları yapamazsınız. Hizmet yöneticiniz değiştirmek için bkz: [eklemek veya Azure yönetici rollerini değiştirmek nasıl](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).
* Office 365 Kiracı genel yönetici kimlik bilgileri olması gerekir.
* Hizmet yöneticisinin e-posta adresini Office 365 Kiracı olmaması gerekir.
* Hizmet yöneticisinin e-posta adresini, herhangi bir genel yönetici Office 365 Kiracı eşleşmesi gerekmez.
* Bir Microsoft hesabı ve bir kurumsal hesap bir e-posta adresi kullanırsanız, geçici olarak başka bir Microsoft hesabı kullanmak için Hizmet Yöneticisi Azure aboneliğinizin değiştirin. Bir Microsoft hesabı oluşturabilirsiniz [Microsoft hesabı kaydolma sayfası](https://signup.live.com/).

## <a name="link-office-365-tenant-to-azure-subscription"></a>Azure aboneliğine bağlantı Office 365 Kiracı
Azure aboneliği için Office 365 Kiracı ilişkilendirmek için aşağıdaki adımları izleyin:

### <a name="step-1-add-office-365-tenant-to-your-azure-subscription"></a>1. adım: Office 365 Kiracı Azure aboneliğinize ekleme

1. Oturum [Klasik Azure portalı](https://manage.windowsazure.com/) hizmet yönetici kimlik bilgilerine sahip.

    ![Ekran görüntüsü, Azure oturum açma](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. Sol bölmede seçin **ACTIVE DIRECTORY**. Office 365 Kiracı görmemesi. Görmüyorsanız, geçin [2. adım: Azure aboneliği ile ilişkili dizine](#Step2).
   
   ![Active Directory ekran girişi](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. Seçin **yeni** > **DIRECTORY** > **özel Oluştur**.
   
    ![Ekran görüntüsü, Azure Active Directory özel oluştur](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. Üzerinde **Dizin Ekle** sayfasında **DIRECTORY**seçin **var olan dizini kullan**. Ardından **şimdi oturumunuz için hazır ben**seçip **tam** ![tamamlamak simgesi](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).
   
    !["Var olan dizini kullan" ekran görüntüsü](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. Oturumu kapattınız sonra Office 365 kiracınızın genel yönetici kimlik bilgilerinizle oturum açın.
   
    ![Office 365 ekran genel yönetici oturum açma](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. Seçin **devam**.
   
    ![Doğrulama ekran görüntüsü](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. Seçin **şimdi oturumu**.
   
    ![Ekran görüntüsü oturum kapatma](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. Oturum [Klasik Azure portalı](https://manage.windowsazure.com/) hizmet yönetici kimlik bilgilerine sahip.
   
    ![Ekran görüntüsü, Azure oturum açma](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. Office 365 kiracınız panosunda görmeniz gerekir.
   
    ![Panosunun ekran görüntüsü](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <a name="Step2"></a>2. adım: Azure aboneliği ile ilişkili dizini değiştirin
   
1. Seçin **ayarları**.
   
    ![Ekran görüntüsü, Azure Klasik Portalı Ayarları simgesi](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. Azure aboneliğinizi seçin ve ardından **dizini Düzenle**.

    ![Ekran görüntüsü, Azure abonelik düzenleme dizin](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. Seçin **sonraki** ![sonraki simgeyi](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).
   
    !["Değişiklik ilişkili dizin" ekran görüntüsü](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. Etkilenen hesapların gözden geçirin. Tüm ortak Yöneticiler ve [rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-configure.md) mevcut kaynak gruplarındaki atanan erişimi olan kullanıcılar kaldırılır. Aldığınız uyarı yalnızca ortak Yöneticiler kaldırılmasını tanımlamıştır.
      
    ![Kaldırılacak ortak yönetici hesapları gösteren ekran görüntüsü.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Kaldırılacak bir örnek kullanıcı hesabı gösteren ekran görüntüsü.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. Seçin **tam** ![tamamlamak simgesi](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-to-the-azure-active-directory-tenant"></a>3. adım: Office 365 Kurumsal hesaplarınızı Azure Active Directory Kiracı ortak yönetici olarak ekleyin
   
1. Seçin **Yöneticiler** sekmesini tıklatın ve ardından **eklemek**.
   
    ![Ekran görüntüsü, Azure Klasik portalı ayarlarını Yöneticiler sekmesi](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. Office 365 kiracınızın kurumsal bir hesap girin, Azure aboneliğini seçin ve ardından **tam** ![tamamlamak simgesi](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).
   
    ![Ekran görüntüsü, Azure ortak yönetici iletişim kutusu ekleme](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. Geri dönerek **Yöneticiler** sekmesi. Ortak yönetici olarak görüntülenen kuruluş hesabı görmeniz gerekir.
   
    ![Yöneticiler sekmesi ekran görüntüsü](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  Azure ortak yönetici hesabıyla erişimi test edin.
   
    a. Dışında Klasik Azure portalında oturum açın.
   
    b. [Azure portalı](https://portal.azure.com/) açın.
   
    c. Ortak yönetici kimlik bilgilerini girin ve ardından **oturum**.
   
    ![Ekran görüntüsü, Azure oturum açma sayfası](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a>Yardım mı gerekiyor? Desteğe başvurun.
Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) hızla çözümlenen sorunu almak için.


