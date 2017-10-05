---
title: "Azure Active Directory'ye yeni kullanıcı ekleme | Microsoft Belgeleri"
description: "Azure Active Directory'de yeni kullanıcıların eklenmesini veya kullanıcı bilgilerinin değiştirilmesini açıklar."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand;jeffsta
ms.reviewer: jeffsta
ms.openlocfilehash: bfe0c556d94d50207a23d2e3984371fb602e9406
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-new-users-to-azure-active-directory"></a><span data-ttu-id="65786-103">Azure Active Directory'ye yeni kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="65786-103">Add new users to Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="65786-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="65786-104">Azure portal</span></span>](active-directory-users-create-azure-portal.md)
> * [<span data-ttu-id="65786-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="65786-105">Azure classic portal</span></span>](active-directory-create-users.md)
>
>

<span data-ttu-id="65786-106">Bu makalede, Azure Active Directory'de (Azure AD), kuruluşunuzdaki yeni kullanıcı ekleme açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="65786-106">This article explains how to add new users in your organization in the Azure Active Directory (Azure AD).</span></span> 

1. <span data-ttu-id="65786-107">Oturum [Azure portal](https://portal.azure.com) dizini için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="65786-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="65786-108">Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="65786-108">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Açılış kullanıcılar ve gruplar](./media/active-directory-users-create-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="65786-110">Üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **tüm kullanıcılar**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="65786-110">On the **Users and groups** blade, select **All users**, and then select **Add**.</span></span>

   ![Ekle komutu seçme](./media/active-directory-users-create-azure-portal/create-users-add-command.png)
4. <span data-ttu-id="65786-112">Kullanıcı için Ayrıntılar gibi girin **adı** ve **kullanıcı adı**.</span><span class="sxs-lookup"><span data-stu-id="65786-112">Enter details for the user, such as **Name** and **User name**.</span></span> <span data-ttu-id="65786-113">Kullanıcı adı etki alanı adı kısmını ya da ilk varsayılan etki alanı adı "foo.onmicrosoft.com" etki alanı adı ya da "contoso.com" gibi bir doğrulanmış, Federasyon olmayan etki alanı adı olması gerekir</span><span class="sxs-lookup"><span data-stu-id="65786-113">The domain name portion of the user name must either be the initial default domain name "foo.onmicrosoft.com" domain name, or a verified, non-federated domain name such as "contoso.com."</span></span>
5. <span data-ttu-id="65786-114">Kopyalama veya aksi takdirde bu işlem tamamlandıktan sonra kullanıcıya sağlayabilir böylece oluşturulmuş kullanıcı parolası not edin.</span><span class="sxs-lookup"><span data-stu-id="65786-114">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span></span>
6. <span data-ttu-id="65786-115">İsteğe bağlı olarak, açın ve bilgileri doldurun **profil** dikey penceresinde **grupları** dikey penceresinde veya **dizin rolünü** dikey penceresinde kullanıcı için.</span><span class="sxs-lookup"><span data-stu-id="65786-115">Optionally, you can open and fill out the information in the **Profile** blade, the **Groups** blade, or the **Directory role** blade for the user.</span></span> <span data-ttu-id="65786-116">Kullanıcı ve yönetici rolleri hakkında daha fazla bilgi için bkz. [Azure AD'de yönetici rolü atama](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="65786-116">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="65786-117">Üzerinde **kullanıcı** dikey penceresinde, select **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="65786-117">On the **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="65786-118">Böylece kullanıcı oturum açarak yeni kullanıcı için oluşturulmuş bir parola güvenli bir şekilde dağıtın.</span><span class="sxs-lookup"><span data-stu-id="65786-118">Securely distribute the generated password to the new user so that the user can sign in.</span></span>

### <a name="next-steps"></a><span data-ttu-id="65786-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="65786-119">Next steps</span></span>
* [<span data-ttu-id="65786-120">Bir dış kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="65786-120">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)
* [<span data-ttu-id="65786-121">Yeni Azure portalında bir kullanıcının parolasını sıfırlama</span><span class="sxs-lookup"><span data-stu-id="65786-121">Reset a user's password in the new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="65786-122">Kullanıcının iş bilgilerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="65786-122">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="65786-123">Kullanıcı profillerini yönetme</span><span class="sxs-lookup"><span data-stu-id="65786-123">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="65786-124">Azure AD'de kullanıcı silme</span><span class="sxs-lookup"><span data-stu-id="65786-124">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
* [<span data-ttu-id="65786-125">Bir kullanıcı, Azure AD'de rol atama</span><span class="sxs-lookup"><span data-stu-id="65786-125">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)
