---
title: "aaaAdd yeni kullanıcılar tooAzure Active Directory | Microsoft Docs"
description: "Açıklar nasıl tooadd yeni kullanıcılar Azure Active Directory'de."
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
ms.openlocfilehash: 6ca413c84a7a5238a30fd26fc751d687d827b24a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-new-users-tooazure-active-directory"></a><span data-ttu-id="cab66-103">Hızlı Başlangıç: yeni kullanıcılar tooAzure Active Directory ekleme</span><span class="sxs-lookup"><span data-stu-id="cab66-103">Quickstart: Add new users tooAzure Active Directory</span></span>
<span data-ttu-id="cab66-104">Bu makalede nasıl hello Azure Active Directory (Azure AD), kuruluşunuzdaki yeni kullanıcıların tooadd hello Azure portal kullanarak bir zamanda ya da şirket içi Windows Server AD kullanıcı eşitleme hesabı veri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cab66-104">This article explains how tooadd new users in your organization in hello Azure Active Directory (Azure AD) one at a time using hello Azure portal or by synchronizing your on-premises Windows Server AD user account data.</span></span> 

## <a name="add-cloud-based-users"></a><span data-ttu-id="cab66-105">Bulut tabanlı kullanıcıları ekleme</span><span class="sxs-lookup"><span data-stu-id="cab66-105">Add cloud-based users</span></span>
1. <span data-ttu-id="cab66-106">İçinde toohello oturum [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com) hello dizin için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="cab66-106">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="cab66-107">Seçin **Azure Active Directory** ve ardından **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="cab66-107">Select **Azure Active Directory** and then **Users and groups**.</span></span>
3. <span data-ttu-id="cab66-108">Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **tüm kullanıcılar**ve ardından **yeni kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="cab66-108">On hello **Users and groups** blade, select **All users**, and then select **New user**.</span></span>
   <span data-ttu-id="cab66-109">![Merhaba Ekle komutu seçme](./media/add-users-azure-active-directory/add-user.png)</span><span class="sxs-lookup"><span data-stu-id="cab66-109">![Selecting hello Add command](./media/add-users-azure-active-directory/add-user.png)</span></span>
4. <span data-ttu-id="cab66-110">Ayrıntılar gibi hello kullanıcıdan girin **adı** ve **kullanıcı adı**.</span><span class="sxs-lookup"><span data-stu-id="cab66-110">Enter details for hello user, such as **Name** and **User name**.</span></span> <span data-ttu-id="cab66-111">Merhaba hello kullanıcı adının etki alanı adı kısmını hello ilk varsayılan etki alanı adı "[etki alanı adı].onmicrosoft.com" ya da doğrulanmış, Federasyon olmayan olmalıdır [özel etki alanı adı](add-custom-domain.md) "contoso.com" gibi</span><span class="sxs-lookup"><span data-stu-id="cab66-111">hello domain name portion of hello user name must either be hello initial default domain name "[domain name].onmicrosoft.com" or a verified, non-federated [custom domain name](add-custom-domain.md) such as "contoso.com."</span></span>
5. <span data-ttu-id="cab66-112">Böylece bu işlem tamamlandıktan sonra toohello kullanıcı sağlayabilir kopyalama veya aksi Not hello tarafından oluşturulan kullanıcı parola.</span><span class="sxs-lookup"><span data-stu-id="cab66-112">Copy or otherwise note hello generated user password so that you can provide it toohello user after this process is complete.</span></span>
6. <span data-ttu-id="cab66-113">İsteğe bağlı olarak, açın ve hello hello bilgileri doldurun **profil** dikey penceresinde, hello **grupları** dikey ya da hello **dizin rolünü** dikey penceresinde hello kullanıcı için.</span><span class="sxs-lookup"><span data-stu-id="cab66-113">Optionally, you can open and fill out hello information in hello **Profile** blade, hello **Groups** blade, or hello **Directory role** blade for hello user.</span></span> <span data-ttu-id="cab66-114">Kullanıcı ve yönetici rolleri hakkında daha fazla bilgi için bkz. [Azure AD'de yönetici rolü atama](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="cab66-114">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="cab66-115">Merhaba üzerinde **kullanıcı** dikey penceresinde, select **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="cab66-115">On hello **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="cab66-116">Böylece Hello kullanıcı oturum açabilir hello oluşturulan parola toohello yeni kullanıcı güvenli bir şekilde dağıtın.</span><span class="sxs-lookup"><span data-stu-id="cab66-116">Securely distribute hello generated password toohello new user so that hello user can sign in.</span></span>

> [!TIP]
> <span data-ttu-id="cab66-117">Ayrıca şirket içi Windows Server AD kullanıcı hesabı verileri eşitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cab66-117">You can also synchronize user account data from on-premises Windows Server AD.</span></span> <span data-ttu-id="cab66-118">Microsoft'un kimlik çözümleri şirket içi ve bulut tabanlı özellikleri, tek bir kullanıcı kimliği kimlik doğrulama ve yetkilendirme için konum bağımsız olarak tooall kaynakları oluşturma span.</span><span class="sxs-lookup"><span data-stu-id="cab66-118">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization tooall resources, regardless of location.</span></span> <span data-ttu-id="cab66-119">Bu karma kimlik diyoruz.</span><span class="sxs-lookup"><span data-stu-id="cab66-119">We call this Hybrid Identity.</span></span> <span data-ttu-id="cab66-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) şirket içi dizinlerinizi Azure Active Directory ile karma kimlik senaryosunda kullanılan toointegrate olabilir.</span><span class="sxs-lookup"><span data-stu-id="cab66-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) can be used toointegrate your on-premises directories with Azure Active Directory for hybrid identity scenarios.</span></span> <span data-ttu-id="cab66-121">Bu, kullanıcıların Office 365, Azure ve SaaS uygulamaları için ortak bir kimlik Azure AD ile tümleşik tooprovide sağlar.</span><span class="sxs-lookup"><span data-stu-id="cab66-121">This allows you tooprovide a common identity for your users for Office 365, Azure, and SaaS applications integrated with Azure AD.</span></span> 

## <a name="delete-users-from-azure-ad"></a><span data-ttu-id="cab66-122">Azure AD kullanıcıları Sil</span><span class="sxs-lookup"><span data-stu-id="cab66-122">Delete users from Azure AD</span></span>
1. <span data-ttu-id="cab66-123">İçinde toohello oturum [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com) hello dizin için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="cab66-123">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="cab66-124">Seçin **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="cab66-124">Select **Users and groups**.</span></span>
3. <span data-ttu-id="cab66-125">Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select hello kullanıcı toodelete hello listeden.</span><span class="sxs-lookup"><span data-stu-id="cab66-125">On hello **Users and groups** blade, select hello user toodelete from hello list.</span></span> 
4. <span data-ttu-id="cab66-126">Merhaba dikey penceresinde hello seçilen kullanıcı, seçin **genel bakış**ve hello komut çubuğunda, ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="cab66-126">On hello blade for hello selected user, select **Overview**, and then in hello command bar, select **Delete**.</span></span>
   <span data-ttu-id="cab66-127">![Merhaba Ekle komutu seçme](./media/add-users-azure-active-directory/delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="cab66-127">![Selecting hello Add command](./media/add-users-azure-active-directory/delete-user.png)</span></span>


### <a name="learn-more"></a><span data-ttu-id="cab66-128">Daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="cab66-128">Learn more</span></span> 
* [<span data-ttu-id="cab66-129">Bir dış kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="cab66-129">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)

* [<span data-ttu-id="cab66-130">Azure AD'de kullanıcı tooa rol atama</span><span class="sxs-lookup"><span data-stu-id="cab66-130">Assign a user tooa role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a><span data-ttu-id="cab66-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cab66-131">Next steps</span></span>
<span data-ttu-id="cab66-132">Bu Hızlı Başlangıç, öğrendiğinize nasıl tooadd yeni kullanıcılar tooAzure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="cab66-132">In this quickstart, you’ve learned how tooadd new users tooAzure AD Premium.</span></span> 

<span data-ttu-id="cab66-133">Bağlantı toocreate yeni bir kullanıcı Azure AD'de hello Azure portal ' aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cab66-133">You can use hello following link toocreate a new user in Azure AD from hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cab66-134">Kullanıcıların tooAzure AD ekleyin</span><span class="sxs-lookup"><span data-stu-id="cab66-134">Add users tooAzure AD</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 
