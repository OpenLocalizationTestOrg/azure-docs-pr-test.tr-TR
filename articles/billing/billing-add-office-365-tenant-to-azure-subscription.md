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
# <a name="associate-an-office-365-tenant-to-an-azure-subscription"></a><span data-ttu-id="d3bee-103">Bir Azure aboneliği için bir Office 365 Kiracı ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="d3bee-103">Associate an Office 365 tenant to an Azure subscription</span></span>
<span data-ttu-id="d3bee-104">Office 365 Kiracı Azure aboneliğinizden erişebilmesi için ayrı Azure ve Office 365 abonelikleri bağlayın.</span><span class="sxs-lookup"><span data-stu-id="d3bee-104">Link your separate Azure and Office 365 subscriptions so that you can access the Office 365 tenant from your Azure subscription.</span></span> <span data-ttu-id="d3bee-105">Aboneliklerinizi bağlamak için Azure'da Azure Hizmet yöneticisi hesabı ile oturum açın, bir dizin ekleyin ve Office 365 Kurumsal hesaplar için Azure Active Directory Kiracı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d3bee-105">To link your subscriptions, sign in to Azure with the Azure service administrator account, add a directory, and add the Office 365 organizational accounts to the Azure Active Directory tenant.</span></span>

<span data-ttu-id="d3bee-106">Azure Active Directory örneğinizi kullanıcıları için Office 365 aboneliğiniz istediğiniz veya Office 365 hesabı ancak bir Azure hesabınız varsa, bkz: [kaydolmak için Azure ile Office 365 hesabı](billing-use-existing-office-365-account-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="d3bee-106">If you want an Office 365 subscription for users in your Azure Active Directory instance or you have an Office 365 account but not an Azure account, see [Sign up for Azure with Office 365 account](billing-use-existing-office-365-account-azure-subscription.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="d3bee-107">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="d3bee-107">Before you begin</span></span>
* <span data-ttu-id="d3bee-108">Azure aboneliği Hizmet Yöneticisi kimlik bilgileri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3bee-108">You must have the credentials of the Azure subscription service administrator.</span></span> <span data-ttu-id="d3bee-109">Ortak yönetici hesapları, bu makaledeki adımları bazıları yapamazsınız.</span><span class="sxs-lookup"><span data-stu-id="d3bee-109">Co-administrator accounts can't do some of the steps in this article.</span></span> <span data-ttu-id="d3bee-110">Hizmet yöneticiniz değiştirmek için bkz: [eklemek veya Azure yönetici rollerini değiştirmek nasıl](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span><span class="sxs-lookup"><span data-stu-id="d3bee-110">To change your service administrator, see [How to add or change Azure administrator roles](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span></span>
* <span data-ttu-id="d3bee-111">Office 365 Kiracı genel yönetici kimlik bilgileri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3bee-111">You must have the credentials of a global administrator of the Office 365 tenant.</span></span>
* <span data-ttu-id="d3bee-112">Hizmet yöneticisinin e-posta adresini Office 365 Kiracı olmaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3bee-112">The email address of the service administrator must not be in the Office 365 tenant.</span></span>
* <span data-ttu-id="d3bee-113">Hizmet yöneticisinin e-posta adresini, herhangi bir genel yönetici Office 365 Kiracı eşleşmesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d3bee-113">The email address of the service administrator must not match that of any global administrator of the Office 365 tenant.</span></span>
* <span data-ttu-id="d3bee-114">Bir Microsoft hesabı ve bir kurumsal hesap bir e-posta adresi kullanırsanız, geçici olarak başka bir Microsoft hesabı kullanmak için Hizmet Yöneticisi Azure aboneliğinizin değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d3bee-114">If you use an email address that is both a Microsoft account and an organizational account, temporarily change the service administrator of your Azure subscription to use another Microsoft account.</span></span> <span data-ttu-id="d3bee-115">Bir Microsoft hesabı oluşturabilirsiniz [Microsoft hesabı kaydolma sayfası](https://signup.live.com/).</span><span class="sxs-lookup"><span data-stu-id="d3bee-115">You can create a Microsoft account at the [Microsoft account signup page](https://signup.live.com/).</span></span>

## <a name="link-office-365-tenant-to-azure-subscription"></a><span data-ttu-id="d3bee-116">Azure aboneliğine bağlantı Office 365 Kiracı</span><span class="sxs-lookup"><span data-stu-id="d3bee-116">Link Office 365 tenant to Azure subscription</span></span>
<span data-ttu-id="d3bee-117">Azure aboneliği için Office 365 Kiracı ilişkilendirmek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d3bee-117">To associate the Office 365 tenant to the Azure subscription, follow these steps:</span></span>

### <a name="step-1-add-office-365-tenant-to-your-azure-subscription"></a><span data-ttu-id="d3bee-118">1. adım: Office 365 Kiracı Azure aboneliğinize ekleme</span><span class="sxs-lookup"><span data-stu-id="d3bee-118">Step 1: Add Office 365 tenant to your Azure subscription</span></span>

1. <span data-ttu-id="d3bee-119">Oturum [Klasik Azure portalı](https://manage.windowsazure.com/) hizmet yönetici kimlik bilgilerine sahip.</span><span class="sxs-lookup"><span data-stu-id="d3bee-119">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with the service administrator credentials.</span></span>

    ![Ekran görüntüsü, Azure oturum açma](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. <span data-ttu-id="d3bee-121">Sol bölmede seçin **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="d3bee-121">In the left pane, select **ACTIVE DIRECTORY**.</span></span> <span data-ttu-id="d3bee-122">Office 365 Kiracı görmemesi.</span><span class="sxs-lookup"><span data-stu-id="d3bee-122">You shouldn't see the Office 365 tenant.</span></span> <span data-ttu-id="d3bee-123">Görmüyorsanız, geçin [2. adım: Azure aboneliği ile ilişkili dizine](#Step2).</span><span class="sxs-lookup"><span data-stu-id="d3bee-123">If you see it, skip to [Step 2: Change the directory associated with the Azure subscription](#Step2).</span></span>
   
   ![Active Directory ekran girişi](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. <span data-ttu-id="d3bee-125">Seçin **yeni** > **DIRECTORY** > **özel Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="d3bee-125">Select **NEW** > **DIRECTORY** > **CUSTOM CREATE**.</span></span>
   
    ![Ekran görüntüsü, Azure Active Directory özel oluştur](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. <span data-ttu-id="d3bee-127">Üzerinde **Dizin Ekle** sayfasında **DIRECTORY**seçin **var olan dizini kullan**.</span><span class="sxs-lookup"><span data-stu-id="d3bee-127">On the **Add directory** page, under **DIRECTORY**, select **Use existing directory**.</span></span> <span data-ttu-id="d3bee-128">Ardından **şimdi oturumunuz için hazır ben**seçip **tam** ![tamamlamak simgesi](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="d3bee-128">Then select **I am ready to be signed out now**, and select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    !["Var olan dizini kullan" ekran görüntüsü](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. <span data-ttu-id="d3bee-130">Oturumu kapattınız sonra Office 365 kiracınızın genel yönetici kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d3bee-130">After you are signed out, sign in with the global administrator’s credentials of your Office 365 tenant.</span></span>
   
    ![Office 365 ekran genel yönetici oturum açma](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. <span data-ttu-id="d3bee-132">Seçin **devam**.</span><span class="sxs-lookup"><span data-stu-id="d3bee-132">Select **Continue**.</span></span>
   
    ![Doğrulama ekran görüntüsü](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. <span data-ttu-id="d3bee-134">Seçin **şimdi oturumu**.</span><span class="sxs-lookup"><span data-stu-id="d3bee-134">Select **Sign out now**.</span></span>
   
    ![Ekran görüntüsü oturum kapatma](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. <span data-ttu-id="d3bee-136">Oturum [Klasik Azure portalı](https://manage.windowsazure.com/) hizmet yönetici kimlik bilgilerine sahip.</span><span class="sxs-lookup"><span data-stu-id="d3bee-136">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with the service administrator credentials.</span></span>
   
    ![Ekran görüntüsü, Azure oturum açma](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. <span data-ttu-id="d3bee-138">Office 365 kiracınız panosunda görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3bee-138">You should see your Office 365 tenant in the dashboard.</span></span>
   
    ![Panosunun ekran görüntüsü](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <span data-ttu-id="d3bee-140"><a name="Step2"></a>2. adım: Azure aboneliği ile ilişkili dizini değiştirin</span><span class="sxs-lookup"><span data-stu-id="d3bee-140"><a name="Step2"></a>Step 2: Change the directory associated with the Azure subscription</span></span>
   
1. <span data-ttu-id="d3bee-141">Seçin **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="d3bee-141">Select **Settings**.</span></span>
   
    ![Ekran görüntüsü, Azure Klasik Portalı Ayarları simgesi](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. <span data-ttu-id="d3bee-143">Azure aboneliğinizi seçin ve ardından **dizini Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="d3bee-143">Select your Azure subscription, and then select **EDIT DIRECTORY**.</span></span>

    ![Ekran görüntüsü, Azure abonelik düzenleme dizin](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. <span data-ttu-id="d3bee-145">Seçin **sonraki** ![sonraki simgeyi](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span><span class="sxs-lookup"><span data-stu-id="d3bee-145">Select **Next** ![Next icon](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span></span>
   
    !["Değişiklik ilişkili dizin" ekran görüntüsü](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. <span data-ttu-id="d3bee-147">Etkilenen hesapların gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="d3bee-147">Review the affected accounts.</span></span> <span data-ttu-id="d3bee-148">Tüm ortak Yöneticiler ve [rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-configure.md) mevcut kaynak gruplarındaki atanan erişimi olan kullanıcılar kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="d3bee-148">All co-administrators and [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) users with assigned access in the existing resource groups are removed.</span></span> <span data-ttu-id="d3bee-149">Aldığınız uyarı yalnızca ortak Yöneticiler kaldırılmasını tanımlamıştır.</span><span class="sxs-lookup"><span data-stu-id="d3bee-149">The warning you receive only mentions the removal of co-administrators.</span></span>
      
    ![Kaldırılacak ortak yönetici hesapları gösteren ekran görüntüsü.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Kaldırılacak bir örnek kullanıcı hesabı gösteren ekran görüntüsü.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. <span data-ttu-id="d3bee-152">Seçin **tam** ![tamamlamak simgesi](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="d3bee-152">Select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-to-the-azure-active-directory-tenant"></a><span data-ttu-id="d3bee-153">3. adım: Office 365 Kurumsal hesaplarınızı Azure Active Directory Kiracı ortak yönetici olarak ekleyin</span><span class="sxs-lookup"><span data-stu-id="d3bee-153">Step 3: Add your Office 365 organizational accounts as co-administrators to the Azure Active Directory tenant</span></span>
   
1. <span data-ttu-id="d3bee-154">Seçin **Yöneticiler** sekmesini tıklatın ve ardından **eklemek**.</span><span class="sxs-lookup"><span data-stu-id="d3bee-154">Select the **ADMINISTRATORS** tab, and then select **ADD**.</span></span>
   
    ![Ekran görüntüsü, Azure Klasik portalı ayarlarını Yöneticiler sekmesi](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. <span data-ttu-id="d3bee-156">Office 365 kiracınızın kurumsal bir hesap girin, Azure aboneliğini seçin ve ardından **tam** ![tamamlamak simgesi](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="d3bee-156">Enter an organizational account of your Office 365 tenant, select the Azure subscription, and then select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Ekran görüntüsü, Azure ortak yönetici iletişim kutusu ekleme](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. <span data-ttu-id="d3bee-158">Geri dönerek **Yöneticiler** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d3bee-158">Go back to the **ADMINISTRATORS** tab.</span></span> <span data-ttu-id="d3bee-159">Ortak yönetici olarak görüntülenen kuruluş hesabı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3bee-159">You should see the organizational account displayed as co-administrator.</span></span>
   
    ![Yöneticiler sekmesi ekran görüntüsü](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  <span data-ttu-id="d3bee-161">Azure ortak yönetici hesabıyla erişimi test edin.</span><span class="sxs-lookup"><span data-stu-id="d3bee-161">Test access to Azure with the co-administrator account.</span></span>
   
    <span data-ttu-id="d3bee-162">a.</span><span class="sxs-lookup"><span data-stu-id="d3bee-162">a.</span></span> <span data-ttu-id="d3bee-163">Dışında Klasik Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d3bee-163">Sign out of the Azure classic portal.</span></span>
   
    <span data-ttu-id="d3bee-164">b.</span><span class="sxs-lookup"><span data-stu-id="d3bee-164">b.</span></span> <span data-ttu-id="d3bee-165">[Azure portalı](https://portal.azure.com/) açın.</span><span class="sxs-lookup"><span data-stu-id="d3bee-165">Open the [Azure portal](https://portal.azure.com/).</span></span>
   
    <span data-ttu-id="d3bee-166">c.</span><span class="sxs-lookup"><span data-stu-id="d3bee-166">c.</span></span> <span data-ttu-id="d3bee-167">Ortak yönetici kimlik bilgilerini girin ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="d3bee-167">Enter the credentials of the co-administrator, and then select **Sign in**.</span></span>
   
    ![Ekran görüntüsü, Azure oturum açma sayfası](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a><span data-ttu-id="d3bee-169">Yardım mı gerekiyor?</span><span class="sxs-lookup"><span data-stu-id="d3bee-169">Need help?</span></span> <span data-ttu-id="d3bee-170">Desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="d3bee-170">Contact support.</span></span>
<span data-ttu-id="d3bee-171">Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) hızla çözümlenen sorunu almak için.</span><span class="sxs-lookup"><span data-stu-id="d3bee-171">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>


