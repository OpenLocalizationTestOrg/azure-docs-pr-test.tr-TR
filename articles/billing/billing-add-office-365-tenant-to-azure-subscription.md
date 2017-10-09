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
# <a name="associate-an-office-365-tenant-tooan-azure-subscription"></a><span data-ttu-id="3a8cd-103">Office 365 Kiracı tooan Azure aboneliği ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="3a8cd-103">Associate an Office 365 tenant tooan Azure subscription</span></span>
<span data-ttu-id="3a8cd-104">Merhaba Office 365 Kiracı Azure aboneliğinizden erişebilmesi için ayrı Azure ve Office 365 abonelikleri bağlayın.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-104">Link your separate Azure and Office 365 subscriptions so that you can access hello Office 365 tenant from your Azure subscription.</span></span> <span data-ttu-id="3a8cd-105">hello Azure hizmeti yönetici hesabı ile tooAzure toolink oturum aboneliklerinizi, bir dizin ekleyin ve hello Office 365 Kurumsal hesaplar toohello Azure Active Directory Kiracı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-105">toolink your subscriptions, sign in tooAzure with hello Azure service administrator account, add a directory, and add hello Office 365 organizational accounts toohello Azure Active Directory tenant.</span></span>

<span data-ttu-id="3a8cd-106">Azure Active Directory örneğinizi kullanıcıları için Office 365 aboneliğiniz istediğiniz veya Office 365 hesabı ancak bir Azure hesabınız varsa, bkz: [kaydolmak için Azure ile Office 365 hesabı](billing-use-existing-office-365-account-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="3a8cd-106">If you want an Office 365 subscription for users in your Azure Active Directory instance or you have an Office 365 account but not an Azure account, see [Sign up for Azure with Office 365 account](billing-use-existing-office-365-account-azure-subscription.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="3a8cd-107">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="3a8cd-107">Before you begin</span></span>
* <span data-ttu-id="3a8cd-108">Merhaba hello Azure aboneliği Hizmet Yöneticisi kimlik bilgileri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-108">You must have hello credentials of hello Azure subscription service administrator.</span></span> <span data-ttu-id="3a8cd-109">Ortak yönetici hesapları, bu makaledeki adımları hello bazıları yapamazsınız.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-109">Co-administrator accounts can't do some of hello steps in this article.</span></span> <span data-ttu-id="3a8cd-110">toochange hizmet yöneticinize bkz [nasıl tooadd ya da değişiklik Azure yönetici rolleri](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span><span class="sxs-lookup"><span data-stu-id="3a8cd-110">toochange your service administrator, see [How tooadd or change Azure administrator roles](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span></span>
* <span data-ttu-id="3a8cd-111">Genel yöneticinin hello Office 365 Kiracı hello kimlik bilgileri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-111">You must have hello credentials of a global administrator of hello Office 365 tenant.</span></span>
* <span data-ttu-id="3a8cd-112">hello hizmet yöneticisinin Hello e-posta adresini hello Office 365 Kiracı içinde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-112">hello email address of hello service administrator must not be in hello Office 365 tenant.</span></span>
* <span data-ttu-id="3a8cd-113">hello hizmet yöneticisinin Hello e-posta adresini, herhangi bir genel yönetici hello Office 365 Kiracı eşleşmesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-113">hello email address of hello service administrator must not match that of any global administrator of hello Office 365 tenant.</span></span>
* <span data-ttu-id="3a8cd-114">Geçici olarak bir Microsoft hesabı ve bir kurumsal hesap bir e-posta adresi kullanıyorsanız, başka bir Microsoft hesabı hello hizmet yöneticisine, Azure aboneliği toouse değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-114">If you use an email address that is both a Microsoft account and an organizational account, temporarily change hello service administrator of your Azure subscription toouse another Microsoft account.</span></span> <span data-ttu-id="3a8cd-115">Merhaba bir Microsoft hesabı oluşturabilirsiniz [Microsoft hesabı kaydolma sayfası](https://signup.live.com/).</span><span class="sxs-lookup"><span data-stu-id="3a8cd-115">You can create a Microsoft account at hello [Microsoft account signup page](https://signup.live.com/).</span></span>

## <a name="link-office-365-tenant-tooazure-subscription"></a><span data-ttu-id="3a8cd-116">Office 365 Kiracı tooAzure aboneliği bağlama</span><span class="sxs-lookup"><span data-stu-id="3a8cd-116">Link Office 365 tenant tooAzure subscription</span></span>
<span data-ttu-id="3a8cd-117">tooassociate hello Office 365 Kiracı toohello Azure aboneliği, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="3a8cd-117">tooassociate hello Office 365 tenant toohello Azure subscription, follow these steps:</span></span>

### <a name="step-1-add-office-365-tenant-tooyour-azure-subscription"></a><span data-ttu-id="3a8cd-118">1. adım: Office 365 Kiracı tooyour Azure aboneliği ekleme</span><span class="sxs-lookup"><span data-stu-id="3a8cd-118">Step 1: Add Office 365 tenant tooyour Azure subscription</span></span>

1. <span data-ttu-id="3a8cd-119">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com/) hello hizmet yönetici kimlik bilgilerine sahip.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-119">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with hello service administrator credentials.</span></span>

    ![Ekran görüntüsü, Azure oturum açma](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. <span data-ttu-id="3a8cd-121">Merhaba sol bölmesinde seçin **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-121">In hello left pane, select **ACTIVE DIRECTORY**.</span></span> <span data-ttu-id="3a8cd-122">Merhaba Office 365 Kiracı görmemesi.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-122">You shouldn't see hello Office 365 tenant.</span></span> <span data-ttu-id="3a8cd-123">Görmüyorsanız, çok atla[2. adım: hello Azure aboneliği ile ilişkili değişiklik hello dizini](#Step2).</span><span class="sxs-lookup"><span data-stu-id="3a8cd-123">If you see it, skip too[Step 2: Change hello directory associated with hello Azure subscription](#Step2).</span></span>
   
   ![Active Directory ekran girişi](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. <span data-ttu-id="3a8cd-125">Seçin **yeni** > **DIRECTORY** > **özel Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-125">Select **NEW** > **DIRECTORY** > **CUSTOM CREATE**.</span></span>
   
    ![Ekran görüntüsü, Azure Active Directory özel oluştur](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. <span data-ttu-id="3a8cd-127">Merhaba üzerinde **Dizin Ekle** sayfasında **DIRECTORY**seçin **var olan dizini kullan**.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-127">On hello **Add directory** page, under **DIRECTORY**, select **Use existing directory**.</span></span> <span data-ttu-id="3a8cd-128">Ardından **şimdi oturumu kapattınız hazır toobe ben**seçip **tam** ![tamamlamak simgesi](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="3a8cd-128">Then select **I am ready toobe signed out now**, and select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    !["Var olan dizini kullan" ekran görüntüsü](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. <span data-ttu-id="3a8cd-130">Oturumu kapattınız sonra Office 365 kiracınız hello genel yönetici kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-130">After you are signed out, sign in with hello global administrator’s credentials of your Office 365 tenant.</span></span>
   
    ![Office 365 ekran genel yönetici oturum açma](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. <span data-ttu-id="3a8cd-132">Seçin **devam**.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-132">Select **Continue**.</span></span>
   
    ![Doğrulama ekran görüntüsü](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. <span data-ttu-id="3a8cd-134">Seçin **şimdi oturumu**.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-134">Select **Sign out now**.</span></span>
   
    ![Ekran görüntüsü oturum kapatma](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. <span data-ttu-id="3a8cd-136">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com/) hello hizmet yönetici kimlik bilgilerine sahip.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-136">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with hello service administrator credentials.</span></span>
   
    ![Ekran görüntüsü, Azure oturum açma](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. <span data-ttu-id="3a8cd-138">Office 365 kiracınız hello panosunda görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-138">You should see your Office 365 tenant in hello dashboard.</span></span>
   
    ![Panosunun ekran görüntüsü](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <span data-ttu-id="3a8cd-140"><a name="Step2"></a>2. adım: hello Azure aboneliği ile ilişkili değişiklik hello dizini</span><span class="sxs-lookup"><span data-stu-id="3a8cd-140"><a name="Step2"></a>Step 2: Change hello directory associated with hello Azure subscription</span></span>
   
1. <span data-ttu-id="3a8cd-141">Seçin **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-141">Select **Settings**.</span></span>
   
    ![Ekran görüntüsü, Azure Klasik Portalı Ayarları simgesi](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. <span data-ttu-id="3a8cd-143">Azure aboneliğinizi seçin ve ardından **dizini Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-143">Select your Azure subscription, and then select **EDIT DIRECTORY**.</span></span>

    ![Ekran görüntüsü, Azure abonelik düzenleme dizin](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. <span data-ttu-id="3a8cd-145">Seçin **sonraki** ![sonraki simgeyi](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span><span class="sxs-lookup"><span data-stu-id="3a8cd-145">Select **Next** ![Next icon](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span></span>
   
    !["Değişiklik hello ilişkili dizin" işleminin ekran görüntüsü](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. <span data-ttu-id="3a8cd-147">Etkilenen hello hesapları gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-147">Review hello affected accounts.</span></span> <span data-ttu-id="3a8cd-148">Tüm ortak Yöneticiler ve [rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-configure.md) hello mevcut kaynak gruplarındaki atanan erişimi olan kullanıcılar kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-148">All co-administrators and [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) users with assigned access in hello existing resource groups are removed.</span></span> <span data-ttu-id="3a8cd-149">Merhaba uyarı aldığınız yalnızca ortak Yöneticiler hello kaldırılmasını tanımlamıştır.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-149">hello warning you receive only mentions hello removal of co-administrators.</span></span>
      
    ![Ortak yönetici hesapları toobe kaldırılan hello gösteren ekran görüntüsü.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Bir örnek kullanıcı hesabı toobe gösteren ekran görüntüsü kaldırıldı.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. <span data-ttu-id="3a8cd-152">Seçin **tam** ![tamamlamak simgesi](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="3a8cd-152">Select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-toohello-azure-active-directory-tenant"></a><span data-ttu-id="3a8cd-153">3. adım: ortak Yöneticiler toohello Azure Active Directory Kiracı olarak, Office 365 Kurumsal hesapları ekleme</span><span class="sxs-lookup"><span data-stu-id="3a8cd-153">Step 3: Add your Office 365 organizational accounts as co-administrators toohello Azure Active Directory tenant</span></span>
   
1. <span data-ttu-id="3a8cd-154">Select hello **Yöneticiler** sekmesini tıklatın ve ardından **eklemek**.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-154">Select hello **ADMINISTRATORS** tab, and then select **ADD**.</span></span>
   
    ![Ekran görüntüsü, Azure Klasik portalı ayarlarını Yöneticiler sekmesi](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. <span data-ttu-id="3a8cd-156">Office 365 kiracınızın kurumsal bir hesap girin, hello Azure aboneliği seçin ve ardından **tam** ![tamamlamak simgesi](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="3a8cd-156">Enter an organizational account of your Office 365 tenant, select hello Azure subscription, and then select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Ekran görüntüsü, Azure ortak yönetici iletişim kutusu ekleme](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. <span data-ttu-id="3a8cd-158">Toohello dönün **Yöneticiler** sekmesi. Ortak yönetici olarak görüntülenen hello kuruluş hesabı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-158">Go back toohello **ADMINISTRATORS** tab. You should see hello organizational account displayed as co-administrator.</span></span>
   
    ![Yöneticiler sekmesi ekran görüntüsü](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  <span data-ttu-id="3a8cd-160">Test erişim tooAzure hello ortak yönetici hesabıyla.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-160">Test access tooAzure with hello co-administrator account.</span></span>
   
    <span data-ttu-id="3a8cd-161">a.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-161">a.</span></span> <span data-ttu-id="3a8cd-162">Merhaba dışında Klasik Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-162">Sign out of hello Azure classic portal.</span></span>
   
    <span data-ttu-id="3a8cd-163">b.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-163">b.</span></span> <span data-ttu-id="3a8cd-164">Açık hello [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3a8cd-164">Open hello [Azure portal](https://portal.azure.com/).</span></span>
   
    <span data-ttu-id="3a8cd-165">c.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-165">c.</span></span> <span data-ttu-id="3a8cd-166">Merhaba hello ortak yönetici kimlik bilgilerini girin ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-166">Enter hello credentials of hello co-administrator, and then select **Sign in**.</span></span>
   
    ![Ekran görüntüsü, Azure oturum açma sayfası](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a><span data-ttu-id="3a8cd-168">Yardım mı gerekiyor?</span><span class="sxs-lookup"><span data-stu-id="3a8cd-168">Need help?</span></span> <span data-ttu-id="3a8cd-169">Desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-169">Contact support.</span></span>
<span data-ttu-id="3a8cd-170">Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) sorunu Çözümlendi hızla tooget.</span><span class="sxs-lookup"><span data-stu-id="3a8cd-170">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>


