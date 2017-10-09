---
title: "aaaAssign bir kullanıcı Azure Active Directory'de tooadministrator rolü | Microsoft Docs"
description: "Açıklar nasıl toochange kullanıcı yönetim bilgilerinin Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a1ca1a53-50d8-4bf0-ae8f-73fa1253e2d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.openlocfilehash: 8bb6711c2570843962fe075b6026542a4bca525f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-tooadministrator-roles-in-azure-active-directory"></a><span data-ttu-id="c2b31-103">Bir kullanıcı Azure Active Directory'de tooadministrator Rolleri Ata</span><span class="sxs-lookup"><span data-stu-id="c2b31-103">Assign a user tooadministrator roles in Azure Active Directory</span></span>
<span data-ttu-id="c2b31-104">Bu makalede açıklanır nasıl tooassign Azure Active Directory (Azure AD) ortamında bir yönetici rolü tooa kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="c2b31-104">This article explains how tooassign an administrative role tooa user in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="c2b31-105">Kuruluşunuzdaki yeni kullanıcı ekleme hakkında daha fazla bilgi için bkz: [yeni kullanıcılar tooAzure Active Directory eklemek](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c2b31-105">For information about adding new users in your organization, see [Add new users tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="c2b31-106">Eklenen kullanıcılar varsayılan olarak yönetici izinlerine sahip olmayan, ancak herhangi bir zamanda roller toothem atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2b31-106">Added users don't have administrator permissions by default, but you can assign roles toothem at any time.</span></span>

## <a name="assign-a-role-tooa-user"></a><span data-ttu-id="c2b31-107">Rol tooa kullanıcı atama</span><span class="sxs-lookup"><span data-stu-id="c2b31-107">Assign a role tooa user</span></span>
1. <span data-ttu-id="c2b31-108">İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="c2b31-108">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="c2b31-109">Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** hello metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c2b31-109">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Açılış kullanıcı yönetimi](./media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="c2b31-111">Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c2b31-111">On hello **Users and groups** blade, select **All users**.</span></span>

   ![Açılış hello tüm kullanıcılar dikey penceresi](./media/active-directory-users-assign-role-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="c2b31-113">Merhaba üzerinde **kullanıcılar ve gruplar - tüm kullanıcılar** dikey penceresinde, kullanıcı hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="c2b31-113">On hello **Users and groups - All users** blade, select a user from hello list.</span></span>
5. <span data-ttu-id="c2b31-114">Merhaba dikey penceresinde hello seçilen kullanıcı, seçin **dizin rolünü**ve ardından hello hello kullanıcı tooa rolü atayın **dizin rolünü** listesi.</span><span class="sxs-lookup"><span data-stu-id="c2b31-114">On hello blade for hello selected user, select **Directory role**, and then assign hello user tooa role from hello **Directory role** list.</span></span> <span data-ttu-id="c2b31-115">Kullanıcı ve yönetici rolleri hakkında daha fazla bilgi için bkz. [Azure AD'de yönetici rolü atama](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="c2b31-115">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>

      ![Bir kullanıcı tooa rolü atama](./media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)
6. <span data-ttu-id="c2b31-117">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="c2b31-117">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2b31-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c2b31-118">Next steps</span></span>
* [<span data-ttu-id="c2b31-119">Kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="c2b31-119">Add a user</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="c2b31-120">Merhaba yeni Azure portalında bir kullanıcının parolasını sıfırlama</span><span class="sxs-lookup"><span data-stu-id="c2b31-120">Reset a user's password in hello new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="c2b31-121">Kullanıcının iş bilgilerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="c2b31-121">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="c2b31-122">Kullanıcı profillerini yönetme</span><span class="sxs-lookup"><span data-stu-id="c2b31-122">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="c2b31-123">Azure AD'de kullanıcı silme</span><span class="sxs-lookup"><span data-stu-id="c2b31-123">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
