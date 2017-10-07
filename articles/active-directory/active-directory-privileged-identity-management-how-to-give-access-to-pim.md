---
title: "aaaHow toogive erişim tooPrivileged Kimlik Yönetimi - Azure | Microsoft Docs"
description: "PIM yönetilebilir tooadd rolleri toousers ile Azure Active Directory Privileged Identity Management uzantısı nasıl hello öğrenin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: d4c53b53-2b37-41e6-813c-96ec08a1c897
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 5d99589af4af766e430d7cecd743ace752f63768
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="giving-access-toomanage-azure-ad-privileged-identity-management"></a><span data-ttu-id="9c91e-103">Erişim toomanage Azure AD Privileged Identity Management vermiş</span><span class="sxs-lookup"><span data-stu-id="9c91e-103">Giving access toomanage Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="9c91e-104">Azure AD Privileged Identity Management (PIM) bir kuruluş için otomatik olarak etkinleştirir hello genel yönetici rol atamalarını almak ve tooPIM erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c91e-104">hello global administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access tooPIM.</span></span> <span data-ttu-id="9c91e-105">Hiç kimsenin yazma erişimi varsayılan olarak, ancak başka genel yöneticiler de dahil olmak üzere alır.</span><span class="sxs-lookup"><span data-stu-id="9c91e-105">No one else gets write access by default, though, including other global administrators.</span></span> <span data-ttu-id="9c91e-106">Diğer genel yöneticileri, güvenlik yöneticileri ve güvenlik okuyucular salt okunur erişim tooAzure AD PIM sahiptir.</span><span class="sxs-lookup"><span data-stu-id="9c91e-106">Other global adminstrators, security administrators, and security readers have read-only access tooAzure AD PIM.</span></span> <span data-ttu-id="9c91e-107">toogive erişim tooPIM hello ilk kullanıcı atayabilirsiniz başkalarının toohello **ayrıcalıklı Rol Yöneticisi** rol.</span><span class="sxs-lookup"><span data-stu-id="9c91e-107">toogive access tooPIM, hello first user can assign others toohello **Privileged role administrator** role.</span></span> <span data-ttu-id="9c91e-108">Bu atama gelen PIM içinde yapılmalıdır ve PowerShell veya diğer portallar değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="9c91e-108">This assignment must be done from within PIM itself, and cannot be changed via PowerShell or other portals.</span></span>

> [!NOTE]
> <span data-ttu-id="9c91e-109">Azure AD PIM yönetme Azure MFA gerektirir.</span><span class="sxs-lookup"><span data-stu-id="9c91e-109">Managing Azure AD PIM requires Azure MFA.</span></span> <span data-ttu-id="9c91e-110">Microsoft hesapları için Azure MFA kaydedilemiyor olduğundan, bir Microsoft hesabıyla oturum açan bir kullanıcı Azure AD PIM erişemiyor.</span><span class="sxs-lookup"><span data-stu-id="9c91e-110">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access Azure AD PIM.</span></span>
> 
> 

<span data-ttu-id="9c91e-111">Her zaman en az iki kullanıcılar ayrıcalıklı Rol Yöneticisi rolünde bir kullanıcı kilitli durumda veya kullanıcıların hesap silindi emin olun.</span><span class="sxs-lookup"><span data-stu-id="9c91e-111">Make sure there are always at least two users in a privileged role administrator role, in case one user is locked out or their account is deleted.</span></span>

## <a name="give-another-user-access-toomanage-pim"></a><span data-ttu-id="9c91e-112">Başka bir kullanıcı erişimi toomanage PIM verin</span><span class="sxs-lookup"><span data-stu-id="9c91e-112">Give another user access toomanage PIM</span></span>
1. <span data-ttu-id="9c91e-113">İçinde toohello oturum [Azure portal](https://portal.azure.com/) ve select hello **Azure AD Privileged Identity Management** hello Pano uygulaması.</span><span class="sxs-lookup"><span data-stu-id="9c91e-113">Sign in toohello [Azure portal](https://portal.azure.com/) and select hello **Azure AD Privileged Identity Management** app on hello dashboard.</span></span>
2. <span data-ttu-id="9c91e-114">Seçin **yönetmek ayrıcalıklı rolleri** > **ayrıcalıklı Rol Yöneticisi** > **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="9c91e-114">Select **Manage privileged roles** > **Privileged role administrator** > **Add**.</span></span>
   
    ![Ayrıcalıklı rol yöneticileri - ekran görüntüsü ekleme][1]
3. <span data-ttu-id="9c91e-116">Merhaba yönetilen Kullanıcı Ekle dikey, 1. adım zaten tamamlanmış olur.</span><span class="sxs-lookup"><span data-stu-id="9c91e-116">On hello Add managed users blade, step 1 is already complete.</span></span> <span data-ttu-id="9c91e-117">2. adımı seçin **kullanıcı seçin** ve arama hello kullanıcıdan tooadd istiyor.</span><span class="sxs-lookup"><span data-stu-id="9c91e-117">Select step 2, **Select users** and search for hello user you want tooadd.</span></span>
   
    ![Kullanıcılar - ekran görüntüsü seçin][2]
4. <span data-ttu-id="9c91e-119">Merhaba Arama sonuçlarından Hello kullanıcı seçin ve tıklatın **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="9c91e-119">Select hello user from hello search results, and click **Done**.</span></span>
5. <span data-ttu-id="9c91e-120">Tıklatın **Tamam** toosave seçiminizi.</span><span class="sxs-lookup"><span data-stu-id="9c91e-120">Click **OK** toosave your selection.</span></span> <span data-ttu-id="9c91e-121">Seçtiğiniz hello kullanıcı hello ayrıcalıklı rol Yöneticiler listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="9c91e-121">hello user you have selected will appear in hello list of Privileged role administrators.</span></span>
   
   * <span data-ttu-id="9c91e-122">Yeni bir rol toosomeone atadığınız zaman, bunlar otomatik olarak uygun tooactivate hello rolü olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="9c91e-122">Whenever you assign a new role toosomeone, they are automatically set up as eligible tooactivate hello role.</span></span> <span data-ttu-id="9c91e-123">Toomake istiyorsanız, bunları hello rolü'nde, kalıcı hello kullanıcı hello listesinde tıklatın.</span><span class="sxs-lookup"><span data-stu-id="9c91e-123">If you want toomake them permanent in hello role, click hello user in hello list.</span></span> <span data-ttu-id="9c91e-124">Seçin **izin olun** hello kullanıcı bilgileri menüsünde.</span><span class="sxs-lookup"><span data-stu-id="9c91e-124">Select **make perm** in hello user information menu.</span></span>
6. <span data-ttu-id="9c91e-125">Merhaba kullanıcı bağlantısı çok Gönder[Azure AD Privileged Identity Management ile çalışmaya başlama](active-directory-privileged-identity-management-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="9c91e-125">Send hello user a link too[Getting started with Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span></span>

## <a name="remove-another-users-access-rights-for-managing-pim"></a><span data-ttu-id="9c91e-126">PIM yönetmek için başka bir kullanıcının erişim haklarını kaldır</span><span class="sxs-lookup"><span data-stu-id="9c91e-126">Remove another user's access rights for managing PIM</span></span>
<span data-ttu-id="9c91e-127">Birisi hello ayrıcalıklı rol yöneticisi rolünden kaldırmadan önce her zaman tooit atanan iki kullanıcılar çıkarılsın emin olun.</span><span class="sxs-lookup"><span data-stu-id="9c91e-127">Before you remove someone from hello privileged role administrator role, always make sure there will still be two users assigned tooit.</span></span>

1. <span data-ttu-id="9c91e-128">Merhaba rolü'nde Hello PIM panosunda tıklatın **ayrıcalıklı Rol Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="9c91e-128">In hello PIM dashboard, click on hello role **Privileged role administrator**.</span></span>  <span data-ttu-id="9c91e-129">şu anda bu roldeki kullanıcılar Hello listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9c91e-129">hello list of users currently in that role will be displayed.</span></span>
2. <span data-ttu-id="9c91e-130">Merhaba kullanıcı hello kullanıcı listesinde tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9c91e-130">Click on hello user in hello user list.</span></span>
3. <span data-ttu-id="9c91e-131">Tıklayın **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="9c91e-131">Click on **Remove**.</span></span>  <span data-ttu-id="9c91e-132">Bir onay iletisi ile sunulur.</span><span class="sxs-lookup"><span data-stu-id="9c91e-132">You are presented with a confirmation message.</span></span>
4. <span data-ttu-id="9c91e-133">Tıklatın **Evet** hello rolünden tooremove hello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="9c91e-133">Click **Yes** tooremove hello user from hello role.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="9c91e-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9c91e-134">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
