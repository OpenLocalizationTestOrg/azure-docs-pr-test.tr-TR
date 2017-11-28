---
title: "Bir kullanıcı Azure Active Directory'de yönetici rolleri atamak | Microsoft Docs"
description: "Azure Active Directory'de kullanıcı yönetim bilgilerini değiştirmek açıklanmaktadır"
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
ms.openlocfilehash: bfadf133154488f9827cfbeaa98ddb0eb84b52f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-a-user-to-administrator-roles-in-azure-active-directory"></a><span data-ttu-id="7fbcc-103">Kullanıcı Azure Active Directory'de yönetici rolleri atama</span><span class="sxs-lookup"><span data-stu-id="7fbcc-103">Assign a user to administrator roles in Azure Active Directory</span></span>
<span data-ttu-id="7fbcc-104">Bu makalede, Azure Active Directory'de (Azure AD) kullanıcıya bir yönetici rolü atama açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7fbcc-104">This article explains how to assign an administrative role to a user in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="7fbcc-105">Kuruluşunuzdaki yeni kullanıcı ekleme hakkında daha fazla bilgi için bkz: [Azure Active Directory'ye yeni kullanıcı ekleme](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7fbcc-105">For information about adding new users in your organization, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="7fbcc-106">Eklenen kullanıcılar varsayılan olarak yönetici izinlerine sahip olmaz ancak bu kullanıcılara herhangi bir zamanda roller atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7fbcc-106">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

## <a name="assign-a-role-to-a-user"></a><span data-ttu-id="7fbcc-107">Bir kullanıcıya rol atama</span><span class="sxs-lookup"><span data-stu-id="7fbcc-107">Assign a role to a user</span></span>
1. <span data-ttu-id="7fbcc-108">Oturum [Azure portal](https://portal.azure.com) dizini için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="7fbcc-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="7fbcc-109">Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="7fbcc-109">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Açılış kullanıcı yönetimi](./media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="7fbcc-111">Üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="7fbcc-111">On the **Users and groups** blade, select **All users**.</span></span>

   ![Tüm kullanıcılar dikey penceresini açma](./media/active-directory-users-assign-role-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="7fbcc-113">Üzerinde **kullanıcılar ve gruplar - tüm kullanıcılar** dikey penceresinde, listeden kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="7fbcc-113">On the **Users and groups - All users** blade, select a user from the list.</span></span>
5. <span data-ttu-id="7fbcc-114">Dikey penceresinde seçili kullanıcı, seçin **dizin rolünü**ve ardından kullanıcının bir rol atayın **dizin rolünü** listesi.</span><span class="sxs-lookup"><span data-stu-id="7fbcc-114">On the blade for the selected user, select **Directory role**, and then assign the user to a role from the **Directory role** list.</span></span> <span data-ttu-id="7fbcc-115">Kullanıcı ve yönetici rolleri hakkında daha fazla bilgi için bkz. [Azure AD'de yönetici rolü atama](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="7fbcc-115">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>

      ![Bir kullanıcı rol atama](./media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)
6. <span data-ttu-id="7fbcc-117">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="7fbcc-117">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fbcc-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7fbcc-118">Next steps</span></span>
* [<span data-ttu-id="7fbcc-119">Kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="7fbcc-119">Add a user</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="7fbcc-120">Yeni Azure portalında bir kullanıcının parolasını sıfırlama</span><span class="sxs-lookup"><span data-stu-id="7fbcc-120">Reset a user's password in the new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="7fbcc-121">Kullanıcının iş bilgilerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="7fbcc-121">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="7fbcc-122">Kullanıcı profillerini yönetme</span><span class="sxs-lookup"><span data-stu-id="7fbcc-122">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="7fbcc-123">Azure AD'de kullanıcı silme</span><span class="sxs-lookup"><span data-stu-id="7fbcc-123">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
