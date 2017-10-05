---
title: "Azure Active Directory'ye yeni kullanıcı ekleme | Microsoft Belgeleri"
description: "Azure Active Directory'ye yeni kullanıcı ekleme açıklanmaktadır."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 13a7d2d3b991206c45e66872b590bc27a224eead
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="quickstart-add-new-users-to-azure-active-directory"></a><span data-ttu-id="a7db3-103">Hızlı Başlangıç: Azure Active Directory'ye yeni kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="a7db3-103">Quickstart: Add new users to Azure Active Directory</span></span>
<span data-ttu-id="a7db3-104">Bu makalede Azure Active Directory'de (Azure AD), kuruluşunuzdaki yeni kullanıcı ekleme açıklayan bir Azure portalını kullanarak bir zamanda veya şirket içi Windows Server AD kullanıcı hesabı verilerinizi eşitleyerek.</span><span class="sxs-lookup"><span data-stu-id="a7db3-104">This article explains how to add new users in your organization in the Azure Active Directory (Azure AD) one at a time using the Azure portal or by synchronizing your on-premises Windows Server AD user account data.</span></span> 

## <a name="add-cloud-based-users"></a><span data-ttu-id="a7db3-105">Bulut tabanlı kullanıcıları ekleme</span><span class="sxs-lookup"><span data-stu-id="a7db3-105">Add cloud-based users</span></span>
1. <span data-ttu-id="a7db3-106">Oturum [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com) dizini için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="a7db3-106">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="a7db3-107">Seçin **Azure Active Directory** ve ardından **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="a7db3-107">Select **Azure Active Directory** and then **Users and groups**.</span></span>
3. <span data-ttu-id="a7db3-108">Üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **tüm kullanıcılar**ve ardından **yeni kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="a7db3-108">On the **Users and groups** blade, select **All users**, and then select **New user**.</span></span>
   <span data-ttu-id="a7db3-109">![Ekle komutu seçme](./media/add-users-azure-active-directory/add-user.png)</span><span class="sxs-lookup"><span data-stu-id="a7db3-109">![Selecting the Add command](./media/add-users-azure-active-directory/add-user.png)</span></span>
4. <span data-ttu-id="a7db3-110">Kullanıcı için Ayrıntılar gibi girin **adı** ve **kullanıcı adı**.</span><span class="sxs-lookup"><span data-stu-id="a7db3-110">Enter details for the user, such as **Name** and **User name**.</span></span> <span data-ttu-id="a7db3-111">Kullanıcı adı etki alanı adı kısmını ya da gereken ilk varsayılan etki alanı adı "[etki alanı adı].onmicrosoft.com" veya doğrulanmış, Federasyon olmayan olması [özel etki alanı adı](add-custom-domain.md) "contoso.com" gibi</span><span class="sxs-lookup"><span data-stu-id="a7db3-111">The domain name portion of the user name must either be the initial default domain name "[domain name].onmicrosoft.com" or a verified, non-federated [custom domain name](add-custom-domain.md) such as "contoso.com."</span></span>
5. <span data-ttu-id="a7db3-112">Kopyalama veya aksi takdirde bu işlem tamamlandıktan sonra kullanıcıya sağlayabilir böylece oluşturulmuş kullanıcı parolası not edin.</span><span class="sxs-lookup"><span data-stu-id="a7db3-112">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span></span>
6. <span data-ttu-id="a7db3-113">İsteğe bağlı olarak, açın ve bilgileri doldurun **profil** dikey penceresinde **grupları** dikey penceresinde veya **dizin rolünü** dikey penceresinde kullanıcı için.</span><span class="sxs-lookup"><span data-stu-id="a7db3-113">Optionally, you can open and fill out the information in the **Profile** blade, the **Groups** blade, or the **Directory role** blade for the user.</span></span> <span data-ttu-id="a7db3-114">Kullanıcı ve yönetici rolleri hakkında daha fazla bilgi için bkz. [Azure AD'de yönetici rolü atama](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="a7db3-114">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="a7db3-115">Üzerinde **kullanıcı** dikey penceresinde, select **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="a7db3-115">On the **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="a7db3-116">Böylece kullanıcı oturum açarak yeni kullanıcı için oluşturulmuş bir parola güvenli bir şekilde dağıtın.</span><span class="sxs-lookup"><span data-stu-id="a7db3-116">Securely distribute the generated password to the new user so that the user can sign in.</span></span>

> [!TIP]
> <span data-ttu-id="a7db3-117">Ayrıca şirket içi Windows Server AD kullanıcı hesabı verileri eşitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7db3-117">You can also synchronize user account data from on-premises Windows Server AD.</span></span> <span data-ttu-id="a7db3-118">Microsoft'un kimlik çözümleri şirket içi ve bulut tabanlı özellikleri, kimlik doğrulama ve yetkilendirme konum bağımsız olarak tüm kaynaklar için tek bir kullanıcı kimliğini oluşturma span.</span><span class="sxs-lookup"><span data-stu-id="a7db3-118">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization to all resources, regardless of location.</span></span> <span data-ttu-id="a7db3-119">Bu karma kimlik diyoruz.</span><span class="sxs-lookup"><span data-stu-id="a7db3-119">We call this Hybrid Identity.</span></span> <span data-ttu-id="a7db3-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) şirket içi dizinlerinizi Azure Active Directory ile karma kimlik senaryoları için tümleştirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a7db3-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) can be used to integrate your on-premises directories with Azure Active Directory for hybrid identity scenarios.</span></span> <span data-ttu-id="a7db3-121">Bu sayede kullanıcılarınıza Azure AD ile tümleşik Office 365, Azure ve SaaS uygulamaları için ortak bir kimlik sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7db3-121">This allows you to provide a common identity for your users for Office 365, Azure, and SaaS applications integrated with Azure AD.</span></span> 

## <a name="delete-users-from-azure-ad"></a><span data-ttu-id="a7db3-122">Azure AD kullanıcıları Sil</span><span class="sxs-lookup"><span data-stu-id="a7db3-122">Delete users from Azure AD</span></span>
1. <span data-ttu-id="a7db3-123">Oturum [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com) dizini için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="a7db3-123">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="a7db3-124">Seçin **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="a7db3-124">Select **Users and groups**.</span></span>
3. <span data-ttu-id="a7db3-125">Üzerinde **kullanıcılar ve gruplar** dikey penceresinde, listeden silmek istediğiniz kullanıcıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="a7db3-125">On the **Users and groups** blade, select the user to delete from the list.</span></span> 
4. <span data-ttu-id="a7db3-126">Seçilen kullanıcı için dikey seçin **genel bakış**ve ardından komut çubuğunda **silmek**.</span><span class="sxs-lookup"><span data-stu-id="a7db3-126">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span></span>
   <span data-ttu-id="a7db3-127">![Ekle komutu seçme](./media/add-users-azure-active-directory/delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="a7db3-127">![Selecting the Add command](./media/add-users-azure-active-directory/delete-user.png)</span></span>


### <a name="learn-more"></a><span data-ttu-id="a7db3-128">Daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="a7db3-128">Learn more</span></span> 
* [<span data-ttu-id="a7db3-129">Bir dış kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="a7db3-129">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)

* [<span data-ttu-id="a7db3-130">Bir kullanıcı, Azure AD'de rol atama</span><span class="sxs-lookup"><span data-stu-id="a7db3-130">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a><span data-ttu-id="a7db3-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a7db3-131">Next steps</span></span>
<span data-ttu-id="a7db3-132">Bu hızlı başlangıç Azure AD Premium için yeni kullanıcı ekleme öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="a7db3-132">In this quickstart, you’ve learned how to add new users to Azure AD Premium.</span></span> 

<span data-ttu-id="a7db3-133">Azure portalından Azure AD'de yeni bir kullanıcı oluşturmak için aşağıdaki bağlantıyı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a7db3-133">You can use the following link to create a new user in Azure AD from the Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a7db3-134">Kullanıcıları Azure AD’ye ekleme</span><span class="sxs-lookup"><span data-stu-id="a7db3-134">Add users to Azure AD</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 