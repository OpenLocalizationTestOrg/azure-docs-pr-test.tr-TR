---
title: "aaaHow tooadd veya bir kullanıcı rolünü kaldırmak | Microsoft Docs"
description: "Azure Active Directory Privileged Identity Management uygulaması tooadd rolleri tooprivileged kimliklerle nasıl hello öğrenin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 6a47ced8-cf34-4ce8-bea2-e4fc548cfe22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim;oldportal;it-pro;
ms.openlocfilehash: f84639757dd76061ea12ed6ea7ec9e62ad942109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-privileged-identity-management-how-tooadd-or-remove-a-user-role"></a><span data-ttu-id="cea44-103">Azure AD Privileged Identity Management: Nasıl tooadd veya bir kullanıcı rolünü kaldır</span><span class="sxs-lookup"><span data-stu-id="cea44-103">Azure AD Privileged Identity Management: How tooadd or remove a user role</span></span>
<span data-ttu-id="cea44-104">Azure Active Directory (AD ile), bir genel yönetici (veya şirket Yöneticisi) kullanıcıları olan güncelleştirebilirsiniz **kalıcı olarak** tooroles Azure AD'de atanmış.</span><span class="sxs-lookup"><span data-stu-id="cea44-104">With Azure Active Directory (AD), a global administrator (or company administrator) can update which users are **permanently** assigned tooroles in Azure AD.</span></span> <span data-ttu-id="cea44-105">Bu PowerShell cmdlet'leri gibi gerçekleştirilir `Add-MsolRoleMember` ve `Remove-MsolRoleMember`.</span><span class="sxs-lookup"><span data-stu-id="cea44-105">This is done with PowerShell cmdlets like `Add-MsolRoleMember` and `Remove-MsolRoleMember`.</span></span> <span data-ttu-id="cea44-106">Ya da açıklandığı gibi hello Klasik Azure portalını kullanabilirsiniz [Azure Active Directory'de yönetici rolleri atama](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="cea44-106">Or they can use hello Azure classic portal as described in [assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="cea44-107">Hello Azure AD Privileged Identity Management uygulaması ayrıcalıklı rol yöneticilerinin toomake kalıcı rol atamaları de sağlar.</span><span class="sxs-lookup"><span data-stu-id="cea44-107">hello Azure AD Privileged Identity Management application allows privileged role administrators toomake permanent role assignments, as well.</span></span> <span data-ttu-id="cea44-108">Ayrıca, ayrıcalıklı rol Yöneticiler kullanıcılar yapabilir **uygun** yönetici rolleri.</span><span class="sxs-lookup"><span data-stu-id="cea44-108">Additionally, privileged role administrators can make users **eligible** for admin roles.</span></span> <span data-ttu-id="cea44-109">Uygun bir yönetici hello rol ihtiyaç duydukları ve bunlar bitirdiğinizde izinlerini sona etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cea44-109">An eligible admin can activate hello role when they need it, and then their permissions expire once they're done.</span></span>

## <a name="manage-roles-with-pim-in-hello-azure-portal"></a><span data-ttu-id="cea44-110">Hello Azure portal ile PIM rolleri yönetme</span><span class="sxs-lookup"><span data-stu-id="cea44-110">Manage roles with PIM in hello Azure portal</span></span>
<span data-ttu-id="cea44-111">Kuruluşunuzdaki kullanıcılar Azure AD'de Office 365 ve diğer Microsoft Hizmetleri ve uygulamaları toodifferent yönetici rollerini atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cea44-111">In your organization, you can assign users toodifferent administrative roles in Azure AD, Office 365, and other Microsoft services and applications.</span></span>  <span data-ttu-id="cea44-112">Merhaba kullanılabilir rolleri hakkında daha fazla ayrıntı bulunabilir [Azure AD PIM rolleri](active-directory-privileged-identity-management-roles.md).</span><span class="sxs-lookup"><span data-stu-id="cea44-112">More details on hello available roles can be found at [Roles in Azure AD PIM](active-directory-privileged-identity-management-roles.md).</span></span>

<span data-ttu-id="cea44-113">tooadd veya Kaldır ayrıcalıklı Kimlik Yönetimi'ni kullanarak bir roldeki kullanıcı hello PIM Pano çıkarır.</span><span class="sxs-lookup"><span data-stu-id="cea44-113">tooadd or remove a user in a role using Privileged Identity Management, bring up hello PIM dashboard.</span></span> <span data-ttu-id="cea44-114">Ya da hello tıklatın ardından **yönetici rolleri** düğmesini veya hello rolleri tablosundan (örneğin, genel yönetici) belirli bir rol seçin.</span><span class="sxs-lookup"><span data-stu-id="cea44-114">Then either click hello **Users in Admin Roles** button, or select a specific role (such as Global Administrator) from hello roles table.</span></span>

> [!NOTE]
> <span data-ttu-id="cea44-115">PIM hello Azure portal henüz etkinleştirmediyseniz, çok Git[Azure AD PIM ile çalışmaya başlama](active-directory-privileged-identity-management-getting-started.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="cea44-115">If you haven't enabled PIM in hello Azure portal yet, go too[Get started with Azure AD PIM](active-directory-privileged-identity-management-getting-started.md) for details.</span></span>

<span data-ttu-id="cea44-116">Başka bir kullanıcı erişimi tooPIM kendisini hello kullanıcı toohave daha ayrıntılı açıklanır PIM gerektiren hello rolleri toogive istiyorsanız [nasıl toogive erişim tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="cea44-116">If you want toogive another user access tooPIM itself, hello roles which PIM requires hello user toohave are described further in [how toogive access tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="add-a-user-tooa-role"></a><span data-ttu-id="cea44-117">Kullanıcı tooa rolü ekleme</span><span class="sxs-lookup"><span data-stu-id="cea44-117">Add a user tooa role</span></span>
1. <span data-ttu-id="cea44-118">Merhaba, [Azure portal](https://portal.azure.com/)seçin hello **Azure AD Privileged Identity Management** döşeme hello Panoda.</span><span class="sxs-lookup"><span data-stu-id="cea44-118">In hello [Azure portal](https://portal.azure.com/), select hello **Azure AD Privileged Identity Management** tile on hello dashboard.</span></span>
2. <span data-ttu-id="cea44-119">Seçin **yönetmek ayrıcalıklı rolleri**.</span><span class="sxs-lookup"><span data-stu-id="cea44-119">Select **Manage privileged roles**.</span></span>
3. <span data-ttu-id="cea44-120">Merhaba, **Rol Özeti** tablo, select hello rol toomanage istiyor.</span><span class="sxs-lookup"><span data-stu-id="cea44-120">In hello **Role summary** table, select hello role you want toomanage.</span></span>
4. <span data-ttu-id="cea44-121">Merhaba rol dikey penceresinde, seçin **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="cea44-121">In hello role blade, select **Add**.</span></span>
5. <span data-ttu-id="cea44-122">Tıklatın **kullanıcı seçin** ve hello hello kullanıcı Ara **kullanıcı seçin** dikey.</span><span class="sxs-lookup"><span data-stu-id="cea44-122">Click **Select users** and search for hello user on hello **Select users** blade.</span></span>  
6. <span data-ttu-id="cea44-123">Merhaba kullanıcı hello arama sonuçları listesinden seçip'ı tıklatın **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="cea44-123">Select hello user from hello search results list, and click **Done**.</span></span>
7. <span data-ttu-id="cea44-124">Tıklatın **Tamam** toosave seçiminizi.</span><span class="sxs-lookup"><span data-stu-id="cea44-124">Click **OK** toosave your selection.</span></span> <span data-ttu-id="cea44-125">Seçtiğiniz hello kullanıcı hello listesinde hello rol için uygun olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="cea44-125">hello user you have selected will appear in hello list as eligible for hello role.</span></span>

> [!NOTE]
> <span data-ttu-id="cea44-126">Bir rolü yeni kullanıcılar yalnızca varsayılan hello rolü için uygundur.</span><span class="sxs-lookup"><span data-stu-id="cea44-126">New users in a role are only eligible for hello role by default.</span></span> <span data-ttu-id="cea44-127">Toomake hello rol kalıcı istiyorsanız hello kullanıcı hello listesinde tıklatın.</span><span class="sxs-lookup"><span data-stu-id="cea44-127">If you want toomake hello role permanent, click hello user in hello list.</span></span> <span data-ttu-id="cea44-128">Merhaba kullanıcının bilgileri yeni bir dikey pencerede görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="cea44-128">hello user's information will appear in a new blade.</span></span> <span data-ttu-id="cea44-129">Seçin **yapma izni** hello kullanıcı bilgileri menüsünde.</span><span class="sxs-lookup"><span data-stu-id="cea44-129">Select **Make perm** in hello user information menu.</span></span>  
> <span data-ttu-id="cea44-130">Bir kullanıcı Azure çok faktörlü kimlik doğrulama (MFA) kaydedilemiyor veya bir Microsoft hesabı kullanıyorsanız (genellikle @outlook.com), toomake ihtiyacınız bunları kendi tüm rollerde kalıcı.</span><span class="sxs-lookup"><span data-stu-id="cea44-130">If a user cannot register for Azure Multi-Factor Authentication (MFA), or is using a Microsoft account (usually @outlook.com), you need toomake them permanent in all their roles.</span></span> <span data-ttu-id="cea44-131">Uygun admins tooregister etkinleştirme sırasında MFA için istenir.</span><span class="sxs-lookup"><span data-stu-id="cea44-131">Eligible admins are asked tooregister for MFA during activation.</span></span>

<span data-ttu-id="cea44-132">Merhaba kullanıcı rolü için uygun olup, bunu toohello yönergelerinde göre etkinleştirme olduğunu bildirmek [nasıl tooactivate veya bir rolü devre dışı bırakma](active-directory-privileged-identity-management-how-to-activate-role.md).</span><span class="sxs-lookup"><span data-stu-id="cea44-132">Now that hello user is eligible for a role, let them know that they can activate it according toohello instructions in [How tooactivate or deactivate a role](active-directory-privileged-identity-management-how-to-activate-role.md).</span></span>

## <a name="remove-a-user-from-a-role"></a><span data-ttu-id="cea44-133">Bir kullanıcıyı rolden kaldırır</span><span class="sxs-lookup"><span data-stu-id="cea44-133">Remove a user from a role</span></span>
<span data-ttu-id="cea44-134">Uygun rol atamaları Kullanıcıları Kaldır, ancak her zaman kalıcı genel yönetici olan en az bir kullanıcı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="cea44-134">You can remove users from eligible role assignments, but make sure there is always at least one user who is a permanent global administrator.</span></span>

<span data-ttu-id="cea44-135">Bu adımları tooremove belirli bir kullanıcıyı rolden izleyin:</span><span class="sxs-lookup"><span data-stu-id="cea44-135">Follow these steps tooremove a specific user from a role:</span></span>

1. <span data-ttu-id="cea44-136">Merhaba rolü listesinde toohello rol hello Azure AD PIM panosunda bir rolü seçerek veya üzerinde hello tıklatarak gidin **yönetici rolleri** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cea44-136">Navigate toohello role in hello role list either by selecting a role in hello Azure AD PIM dashboard or by clicking on hello **Users in Admin Roles** button.</span></span>
2. <span data-ttu-id="cea44-137">Merhaba kullanıcı hello kullanıcı listesinde tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cea44-137">Click on hello user in hello user list.</span></span>
3. <span data-ttu-id="cea44-138">Tıklatın **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="cea44-138">Click **Remove**.</span></span> <span data-ttu-id="cea44-139">Bir ileti tooconfirm isteyecektir.</span><span class="sxs-lookup"><span data-stu-id="cea44-139">A message will ask you tooconfirm.</span></span>
4. <span data-ttu-id="cea44-140">Tıklatın **Evet** tooremove hello hello kullanıcı rolünden.</span><span class="sxs-lookup"><span data-stu-id="cea44-140">Click **Yes** tooremove hello role from hello user.</span></span>

<span data-ttu-id="cea44-141">Hangi kullanıcıların yine rol atamalarını gerekir emin değilseniz sonra şunları yapabilirsiniz [hello rol için erişim incelemesi başlatma](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="cea44-141">If you're not sure which users still need their role assignments, then you can [start an access review for hello role](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cea44-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cea44-142">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

