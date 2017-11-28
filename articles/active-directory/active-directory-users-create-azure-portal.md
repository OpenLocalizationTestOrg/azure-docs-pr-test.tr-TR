---
title: "aaaAdd yeni kullanıcılar tooAzure Active Directory | Microsoft Docs"
description: "Açıklar nasıl tooadd yeni kullanıcılar veya Azure Active Directory'de kullanıcı bilgilerini değiştirebilirsiniz."
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
ms.openlocfilehash: c4a156ea31b81202bb0d0ac224afbfc3f1785532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-tooazure-active-directory"></a><span data-ttu-id="19c9f-103">Yeni kullanıcılar tooAzure Active Directory ekleme</span><span class="sxs-lookup"><span data-stu-id="19c9f-103">Add new users tooAzure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="19c9f-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="19c9f-104">Azure portal</span></span>](active-directory-users-create-azure-portal.md)
> * [<span data-ttu-id="19c9f-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="19c9f-105">Azure classic portal</span></span>](active-directory-create-users.md)
>
>

<span data-ttu-id="19c9f-106">Bu makalede, Azure Active Directory (Azure AD), kuruluşunuzdaki yeni kullanıcıların tooadd nasıl hello açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="19c9f-106">This article explains how tooadd new users in your organization in hello Azure Active Directory (Azure AD).</span></span> 

1. <span data-ttu-id="19c9f-107">İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="19c9f-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="19c9f-108">Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** hello metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="19c9f-108">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Açılış kullanıcılar ve gruplar](./media/active-directory-users-create-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="19c9f-110">Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **tüm kullanıcılar**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="19c9f-110">On hello **Users and groups** blade, select **All users**, and then select **Add**.</span></span>

   ![Merhaba Ekle komutu seçme](./media/active-directory-users-create-azure-portal/create-users-add-command.png)
4. <span data-ttu-id="19c9f-112">Ayrıntılar gibi hello kullanıcıdan girin **adı** ve **kullanıcı adı**.</span><span class="sxs-lookup"><span data-stu-id="19c9f-112">Enter details for hello user, such as **Name** and **User name**.</span></span> <span data-ttu-id="19c9f-113">Merhaba kullanıcı adının Hello etki alanı adı kısmını ya da hello ilk varsayılan etki alanı adı "foo.onmicrosoft.com" etki alanı adı ya da "contoso.com" gibi bir doğrulanmış, Federasyon olmayan etki alanı adı olması gerekir</span><span class="sxs-lookup"><span data-stu-id="19c9f-113">hello domain name portion of hello user name must either be hello initial default domain name "foo.onmicrosoft.com" domain name, or a verified, non-federated domain name such as "contoso.com."</span></span>
5. <span data-ttu-id="19c9f-114">Böylece bu işlem tamamlandıktan sonra toohello kullanıcı sağlayabilir kopyalama veya aksi Not hello tarafından oluşturulan kullanıcı parola.</span><span class="sxs-lookup"><span data-stu-id="19c9f-114">Copy or otherwise note hello generated user password so that you can provide it toohello user after this process is complete.</span></span>
6. <span data-ttu-id="19c9f-115">İsteğe bağlı olarak, açın ve hello hello bilgileri doldurun **profil** dikey penceresinde, hello **grupları** dikey ya da hello **dizin rolünü** dikey penceresinde hello kullanıcı için.</span><span class="sxs-lookup"><span data-stu-id="19c9f-115">Optionally, you can open and fill out hello information in hello **Profile** blade, hello **Groups** blade, or hello **Directory role** blade for hello user.</span></span> <span data-ttu-id="19c9f-116">Kullanıcı ve yönetici rolleri hakkında daha fazla bilgi için bkz. [Azure AD'de yönetici rolü atama](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="19c9f-116">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="19c9f-117">Merhaba üzerinde **kullanıcı** dikey penceresinde, select **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="19c9f-117">On hello **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="19c9f-118">Böylece Hello kullanıcı oturum açabilir hello oluşturulan parola toohello yeni kullanıcı güvenli bir şekilde dağıtın.</span><span class="sxs-lookup"><span data-stu-id="19c9f-118">Securely distribute hello generated password toohello new user so that hello user can sign in.</span></span>

### <a name="next-steps"></a><span data-ttu-id="19c9f-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="19c9f-119">Next steps</span></span>
* [<span data-ttu-id="19c9f-120">Bir dış kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="19c9f-120">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)
* [<span data-ttu-id="19c9f-121">Merhaba yeni Azure portalında bir kullanıcının parolasını sıfırlama</span><span class="sxs-lookup"><span data-stu-id="19c9f-121">Reset a user's password in hello new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="19c9f-122">Kullanıcının iş bilgilerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="19c9f-122">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="19c9f-123">Kullanıcı profillerini yönetme</span><span class="sxs-lookup"><span data-stu-id="19c9f-123">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="19c9f-124">Azure AD'de kullanıcı silme</span><span class="sxs-lookup"><span data-stu-id="19c9f-124">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
* [<span data-ttu-id="19c9f-125">Azure AD'de kullanıcı tooa rol atama</span><span class="sxs-lookup"><span data-stu-id="19c9f-125">Assign a user tooa role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)
