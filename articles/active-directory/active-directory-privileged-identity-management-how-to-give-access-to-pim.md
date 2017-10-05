---
title: "Privileged Identity Management - Azure için erişim vermek nasıl | Microsoft Docs"
description: "Azure Active Directory Privileged Identity Management uzantısı ile kullanıcıları için roller PIM yönetilebilir eklemeyi öğrenin."
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
ms.openlocfilehash: aeaefb484b29da6e89c2c3c650a79a881b3fa5b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="giving-access-to-manage-azure-ad-privileged-identity-management"></a><span data-ttu-id="bdb6c-103">Azure AD Privileged Identity Management yönetmek için erişim verme</span><span class="sxs-lookup"><span data-stu-id="bdb6c-103">Giving access to manage Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="bdb6c-104">Azure AD Privileged Identity Management (PIM) bir kuruluş için otomatik olarak etkinleştirir genel yönetici rol atamalarını ve PIM erişimi alın.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-104">The global administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access to PIM.</span></span> <span data-ttu-id="bdb6c-105">Hiç kimsenin yazma erişimi varsayılan olarak, ancak başka genel yöneticiler de dahil olmak üzere alır.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-105">No one else gets write access by default, though, including other global administrators.</span></span> <span data-ttu-id="bdb6c-106">Diğer genel yöneticileri, güvenlik yöneticileri ve güvenlik okuyucuları Azure AD PIM salt okunur erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-106">Other global adminstrators, security administrators, and security readers have read-only access to Azure AD PIM.</span></span> <span data-ttu-id="bdb6c-107">PIM için erişim vermek için ilk kullanıcı başkalarına atayabilirsiniz **ayrıcalıklı Rol Yöneticisi** rol.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-107">To give access to PIM, the first user can assign others to the **Privileged role administrator** role.</span></span> <span data-ttu-id="bdb6c-108">Bu atama gelen PIM içinde yapılmalıdır ve PowerShell veya diğer portallar değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-108">This assignment must be done from within PIM itself, and cannot be changed via PowerShell or other portals.</span></span>

> [!NOTE]
> <span data-ttu-id="bdb6c-109">Azure AD PIM yönetme Azure MFA gerektirir.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-109">Managing Azure AD PIM requires Azure MFA.</span></span> <span data-ttu-id="bdb6c-110">Microsoft hesapları için Azure MFA kaydedilemiyor olduğundan, bir Microsoft hesabıyla oturum açan bir kullanıcı Azure AD PIM erişemiyor.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-110">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access Azure AD PIM.</span></span>
> 
> 

<span data-ttu-id="bdb6c-111">Her zaman en az iki kullanıcılar ayrıcalıklı Rol Yöneticisi rolünde bir kullanıcı kilitli durumda veya kullanıcıların hesap silindi emin olun.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-111">Make sure there are always at least two users in a privileged role administrator role, in case one user is locked out or their account is deleted.</span></span>

## <a name="give-another-user-access-to-manage-pim"></a><span data-ttu-id="bdb6c-112">PIM yönetmek için başka bir kullanıcı erişimi verin</span><span class="sxs-lookup"><span data-stu-id="bdb6c-112">Give another user access to manage PIM</span></span>
1. <span data-ttu-id="bdb6c-113">Oturum [Azure portal](https://portal.azure.com/) seçip **Azure AD Privileged Identity Management** Panoda uygulama.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-113">Sign in to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** app on the dashboard.</span></span>
2. <span data-ttu-id="bdb6c-114">Seçin **yönetmek ayrıcalıklı rolleri** > **ayrıcalıklı Rol Yöneticisi** > **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-114">Select **Manage privileged roles** > **Privileged role administrator** > **Add**.</span></span>
   
    ![Ayrıcalıklı rol yöneticileri - ekran görüntüsü ekleme][1]
3. <span data-ttu-id="bdb6c-116">Yönetilen Kullanıcı Ekle dikey, 1. adım zaten tamamlanmış olur.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-116">On the Add managed users blade, step 1 is already complete.</span></span> <span data-ttu-id="bdb6c-117">2. adımı seçin **kullanıcı seçin** eklemek istediğiniz kullanıcıyı arayın.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-117">Select step 2, **Select users** and search for the user you want to add.</span></span>
   
    ![Kullanıcılar - ekran görüntüsü seçin][2]
4. <span data-ttu-id="bdb6c-119">Arama sonuçlarından kullanıcıyı seçin ve'ı tıklatın **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-119">Select the user from the search results, and click **Done**.</span></span>
5. <span data-ttu-id="bdb6c-120">Tıklatın **Tamam** seçiminizi kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-120">Click **OK** to save your selection.</span></span> <span data-ttu-id="bdb6c-121">Seçtiğiniz kullanıcı ayrıcalıklı rol Yöneticiler listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-121">The user you have selected will appear in the list of Privileged role administrators.</span></span>
   
   * <span data-ttu-id="bdb6c-122">Yeni bir rol birine atamak olduğunda, bunlar otomatik olarak uygun rolünü etkinleştirmek için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-122">Whenever you assign a new role to someone, they are automatically set up as eligible to activate the role.</span></span> <span data-ttu-id="bdb6c-123">Roldeki kalıcı hale getirmek istiyorsanız, kullanıcı listesinde'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-123">If you want to make them permanent in the role, click the user in the list.</span></span> <span data-ttu-id="bdb6c-124">Seçin **izin olun** kullanıcı bilgileri menüsünde.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-124">Select **make perm** in the user information menu.</span></span>
6. <span data-ttu-id="bdb6c-125">Kullanıcı bağlantı gönderme [Azure AD Privileged Identity Management ile çalışmaya başlama](active-directory-privileged-identity-management-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="bdb6c-125">Send the user a link to [Getting started with Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span></span>

## <a name="remove-another-users-access-rights-for-managing-pim"></a><span data-ttu-id="bdb6c-126">PIM yönetmek için başka bir kullanıcının erişim haklarını kaldır</span><span class="sxs-lookup"><span data-stu-id="bdb6c-126">Remove another user's access rights for managing PIM</span></span>
<span data-ttu-id="bdb6c-127">Biri ayrıcalıklı rol yöneticisi rolünden kaldırmadan önce her zaman atanmış iki kullanıcı çıkarılsın emin olun.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-127">Before you remove someone from the privileged role administrator role, always make sure there will still be two users assigned to it.</span></span>

1. <span data-ttu-id="bdb6c-128">PIM panosunda rolüne tıklayın **ayrıcalıklı Rol Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-128">In the PIM dashboard, click on the role **Privileged role administrator**.</span></span>  <span data-ttu-id="bdb6c-129">Şu anda bu roldeki kullanıcılar listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-129">The list of users currently in that role will be displayed.</span></span>
2. <span data-ttu-id="bdb6c-130">Kullanıcı listesinde kullanıcı tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-130">Click on the user in the user list.</span></span>
3. <span data-ttu-id="bdb6c-131">Tıklayın **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-131">Click on **Remove**.</span></span>  <span data-ttu-id="bdb6c-132">Bir onay iletisi ile sunulur.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-132">You are presented with a confirmation message.</span></span>
4. <span data-ttu-id="bdb6c-133">Tıklatın **Evet** kullanıcı rolünden kaldırmak için.</span><span class="sxs-lookup"><span data-stu-id="bdb6c-133">Click **Yes** to remove the user from the role.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="bdb6c-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bdb6c-134">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
