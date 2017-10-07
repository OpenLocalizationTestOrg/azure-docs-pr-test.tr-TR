---
title: "aaaAdd yeni kullanıcılar tooAzure Active Directory | Microsoft Docs"
description: "Açıklar nasıl tooadd yeni kullanıcılar veya Azure Active Directory'de kullanıcı bilgilerini değiştirebilirsiniz."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e3673727-6bec-4fdc-87a4-d65b213c4c3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 72f67ad41022fd19fd94c8e1301943b0db1e57bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-tooazure-active-directory"></a><span data-ttu-id="293e1-103">Yeni kullanıcı veya kullanıcıların Microsoft hesaplarını tooAzure Active Directory ile ekleme</span><span class="sxs-lookup"><span data-stu-id="293e1-103">Add new users or users with Microsoft accounts tooAzure Active Directory</span></span>
<span data-ttu-id="293e1-104">Kullanıcıların toopopulate dizininize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="293e1-104">Add users toopopulate your directory.</span></span> <span data-ttu-id="293e1-105">Bu makalede açıklanır nasıl tooadd yeni kullanıcılar, kuruluşunuzda nasıl ve ne Microsoft hesabına sahip tooadd kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="293e1-105">This article explains how tooadd new users in your organization, and how tooadd users who have Microsoft accounts.</span></span> <span data-ttu-id="293e1-106">Azure Active Directory'de diğer dizinlerden kullanıcı ekleme veya iş ortağı şirketlerden kullanıcı ekleme hakkında daha fazla bilgi için bkz. [Azure Active Directory'de diğer dizinlerden veya iş ortağı şirketlerden kullanıcılar ekleme](active-directory-create-users-external.md).</span><span class="sxs-lookup"><span data-stu-id="293e1-106">For more information about adding users from other directories in Azure Active Directory or adding users from partner companies, see [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md).</span></span> <span data-ttu-id="293e1-107">Eklenen kullanıcılar varsayılan olarak yönetici izinlerine sahip olmayan, ancak herhangi bir zamanda roller toothem atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="293e1-107">Added users don't have administrator permissions by default, but you can assign roles toothem at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="293e1-108">Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="293e1-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="293e1-109">Nasıl tooadd hello Azure AD Yönetim Merkezi'nden bir kullanıcı görmek için [yeni kullanıcılar tooAzure Active Directory eklemek](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="293e1-109">For how tooadd a user in hello Azure AD admin center, see [Add new users tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="add-a-user"></a><span data-ttu-id="293e1-110">Kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="293e1-110">Add a user</span></span>
1. <span data-ttu-id="293e1-111">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com) hello dizin için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="293e1-111">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="293e1-112">Seçin **Active Directory**ve ardından kuruluş dizininizin hello adını seçin.</span><span class="sxs-lookup"><span data-stu-id="293e1-112">Select **Active Directory**, and then select hello name of your organization directory.</span></span>
3. <span data-ttu-id="293e1-113">Select hello **kullanıcılar** sekmesini tıklatın ve ardından hello komut çubuğunda seçin **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="293e1-113">Select hello **Users** tab, and then, in hello command bar, select **Add User**.</span></span>
4. <span data-ttu-id="293e1-114">Merhaba üzerinde **bu kullanıcı hakkında bize** sayfasında **kullanıcı türünü**, şunlardan birini seçin:</span><span class="sxs-lookup"><span data-stu-id="293e1-114">On hello **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="293e1-115">**New user in your organization (Kuruluşunuzdaki yeni kullanıcı)** - dizininize yeni bir kullanıcı hesabı ekler.</span><span class="sxs-lookup"><span data-stu-id="293e1-115">**New user in your organization** – adds a new user account in your directory.</span></span>
   * <span data-ttu-id="293e1-116">**Var olan bir Microsoft hesabı olan kullanıcı** – mevcut bir Microsoft tüketici hesabını tooyour dizin (örneğin, bir Outlook hesabı) ekler</span><span class="sxs-lookup"><span data-stu-id="293e1-116">**User with an existing Microsoft account** – adds an existing Microsoft consumer account tooyour directory (for example, an Outlook account)</span></span>
5. <span data-ttu-id="293e1-117">**Type of User (Kullanıcı Türü)** seçeneğine bağlı olarak, bir kullanıcı adı (yeni kullanıcı için) veya bir e-posta adresi (Microsoft hesabı olan bir kullanıcı için) girin.</span><span class="sxs-lookup"><span data-stu-id="293e1-117">Depending on **Type of user**, enter a user name (for new user) or an email address (for a user with a Microsoft account).</span></span>
6. <span data-ttu-id="293e1-118">Merhaba kullanıcı **profil** sayfasında, adı ve Soyadı, kullanıcı dostu bir ad ve bir kullanıcı rolüyle hello sağlayın **rolleri** listesi.</span><span class="sxs-lookup"><span data-stu-id="293e1-118">On hello user **Profile** page, provide a first and last name, a user-friendly name, and a user role from hello **Roles** list.</span></span> <span data-ttu-id="293e1-119">Kullanıcı ve yönetici rolleri hakkında daha fazla bilgi için bkz. [Azure AD'de yönetici rolü atama](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="293e1-119">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="293e1-120">Belirtin çok olup olmadığını**çok faktörlü kimlik doğrulamasını etkinleştir** hello kullanıcı için.</span><span class="sxs-lookup"><span data-stu-id="293e1-120">Specify whether too**Enable Multi-Factor Authentication** for hello user.</span></span>
7. <span data-ttu-id="293e1-121">Merhaba üzerinde **Get geçici parola** sayfasında, **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="293e1-121">On hello **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="293e1-122">Kuruluşunuz birden fazla etki alanı kullanıyorsa bir kullanıcı hesabı eklediğinizde, sorunları aşağıdaki hello hakkında bilmeniz gerekenler:</span><span class="sxs-lookup"><span data-stu-id="293e1-122">If your organization uses more than one domain, you should know about hello following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="293e1-123">tooadd kullanıcı hesapları ile etki alanları arasında aynı kullanıcı asıl adı (UPN) hello **ilk** ekleme, örneğin, geoffgrisso@contoso.onmicrosoft.com, **arkasından** geoffgrisso@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="293e1-123">tooadd user accounts with hello same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="293e1-124">geoffgrisso@contoso.onmicrosoft.com eklemeden önce geoffgrisso@contoso.com **eklemeyin**. Bu sıra önemlidir ve sıkıcı tooundo olabilir.</span><span class="sxs-lookup"><span data-stu-id="293e1-124">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com. This order is important, and can be cumbersome tooundo.</span></span>
>
>

## <a name="change-user-information"></a><span data-ttu-id="293e1-125">Kullanıcı bilgilerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="293e1-125">Change user information</span></span>
<span data-ttu-id="293e1-126">Merhaba nesne kimliği dışındaki tüm kullanıcı özniteliklerini değiştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="293e1-126">You can change any user attribute except for hello object ID.</span></span>

1. <span data-ttu-id="293e1-127">Dizininizi açın.</span><span class="sxs-lookup"><span data-stu-id="293e1-127">Open your directory.</span></span>
2. <span data-ttu-id="293e1-128">Select hello **kullanıcılar** sekmesini ve ardından hello görünen adını hello toochange istediğiniz kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="293e1-128">Select hello **Users** tab, and then select hello display name of hello user you want toochange.</span></span>
3. <span data-ttu-id="293e1-129">Değişikliklerinizi tamamlayın ve ardından **Save (Kaydet)** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="293e1-129">Complete your changes, and then click **Save**.</span></span>

<span data-ttu-id="293e1-130">Değiştirdiğiniz hello kullanıcı şirket içi Active Directory hizmetinizle eşitlenmişse bu yordamı kullanarak hello kullanıcı bilgilerini değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="293e1-130">If hello user that you're changing is synchronized with your on-premises Active Directory service, you can't change hello user information using this procedure.</span></span> <span data-ttu-id="293e1-131">toochange hello kullanıcı, şirket içi Active Directory Yönetim araçlarınızı kullanın.</span><span class="sxs-lookup"><span data-stu-id="293e1-131">toochange hello user, use your on-premises Active Directory management tools.</span></span>

## <a name="guest-user-management-and-limitations"></a><span data-ttu-id="293e1-132">Konuk kullanıcı yönetimi ve sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="293e1-132">Guest user management and limitations</span></span>
<span data-ttu-id="293e1-133">Konuk, davet edilen tooyour directory tooaccess SharePoint belgeleri, uygulamaları ya da diğer Azure kaynaklarına diğer dizinlerden kullanıcı hesaplarıdır.</span><span class="sxs-lookup"><span data-stu-id="293e1-133">Guest accounts are users from other directories who were invited tooyour directory tooaccess SharePoint documents, applications, or other Azure resources.</span></span> <span data-ttu-id="293e1-134">Bir Konuk hesabı dizininizde çok "konuk." ayarlamak temel alınan UserType özniteliği var</span><span class="sxs-lookup"><span data-stu-id="293e1-134">A guest account in your directory has its underlying UserType attribute set too"Guest."</span></span> <span data-ttu-id="293e1-135">Normal kullanıcıların (özellikle de dizininizin üyelerinin) hello UserType özniteliği "Üye" sahip</span><span class="sxs-lookup"><span data-stu-id="293e1-135">Regular users (specifically, members of your directory) have hello UserType attribute "Member."</span></span>

<span data-ttu-id="293e1-136">Konuklar hello dizinde sınırlı bir haklar kümesine sahip.</span><span class="sxs-lookup"><span data-stu-id="293e1-136">Guests have a limited set of rights in hello directory.</span></span> <span data-ttu-id="293e1-137">Bu haklar hello özelliği konuklar toodiscover hello dizin diğer kullanıcılar hakkında bilgi edinmek için sınırlar.</span><span class="sxs-lookup"><span data-stu-id="293e1-137">These rights limit hello ability for Guests toodiscover information about other users in hello directory.</span></span> <span data-ttu-id="293e1-138">Ancak, Konuk kullanıcılar hello kullanıcılar ve gruplar üzerinde çalıştığınız hello kaynaklarla ilişkili ile etkileşebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="293e1-138">However, guest users can still interact with hello users and groups associated with hello resources they're working on.</span></span> <span data-ttu-id="293e1-139">Konuk kullanıcılar şunları yapabilir:</span><span class="sxs-lookup"><span data-stu-id="293e1-139">Guest users can:</span></span>

* <span data-ttu-id="293e1-140">Diğer kullanıcılar ve gruplar atanmış oldukları bir Azure aboneliği toowhich ile ilişkili bakın</span><span class="sxs-lookup"><span data-stu-id="293e1-140">See other users and groups associated with an Azure subscription toowhich they're assigned</span></span>
* <span data-ttu-id="293e1-141">Ait oldukları gruplar toowhich Hello üyeleri bakın</span><span class="sxs-lookup"><span data-stu-id="293e1-141">See hello members of groups toowhich they belong</span></span>
* <span data-ttu-id="293e1-142">Başlangıç dizini, diğer kullanıcıları hello kullanıcı hello tam e-posta adresini biliyorsanız arayın</span><span class="sxs-lookup"><span data-stu-id="293e1-142">Look up other users in hello directory, if they know hello full email address of hello user</span></span>
* <span data-ttu-id="293e1-143">Yalnızca sınırlı sayıda sınırlı toodisplay adı, e-posta adresi, kullanıcı asıl adı (UPN) ve küçük resim fotoğrafı yukarı--göründükleri hello kullanıcılar özniteliklerini bakın</span><span class="sxs-lookup"><span data-stu-id="293e1-143">See only a limited set of attributes of hello users they look up--limited toodisplay name, email address, user principal name (UPN), and thumbnail photo</span></span>
* <span data-ttu-id="293e1-144">Merhaba dizinde doğrulanan etki alanlarının bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="293e1-144">Get a list of verified domains in hello directory</span></span>
* <span data-ttu-id="293e1-145">Dizininizde üyelere sahip aynı erişim izni tooapplications, bunları verme hello</span><span class="sxs-lookup"><span data-stu-id="293e1-145">Consent tooapplications, granting them hello same access that Members have in your directory</span></span>

## <a name="set-guest-user-access-policies"></a><span data-ttu-id="293e1-146">Konuk kullanıcı erişim ilkeleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="293e1-146">Set guest user access policies</span></span>
<span data-ttu-id="293e1-147">Merhaba **yapılandırma** bir dizinin sekmesi seçenekleri toocontrol konuk kullanıcıların erişimini içerir.</span><span class="sxs-lookup"><span data-stu-id="293e1-147">hello **Configure** tab of a directory includes options toocontrol access for guest users.</span></span> <span data-ttu-id="293e1-148">Bu seçenekler yalnızca klasik Azure portalında bir dizin genel yöneticisi tarafından değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="293e1-148">These options can be changed only in Azure classic portal by a directory global administrator.</span></span> <span data-ttu-id="293e1-149">Şu anda bir PowerShell veya API yöntemi bulunmamaktadır.</span><span class="sxs-lookup"><span data-stu-id="293e1-149">Currently, there's no PowerShell or API method.</span></span>

<span data-ttu-id="293e1-150">tooopen hello **yapılandırma** hello Azure Klasik portalı, select sekmesinde **Active Directory**ve ardından hello hello dizin adını seçin.</span><span class="sxs-lookup"><span data-stu-id="293e1-150">tooopen hello **Configure** tab in hello Azure classic portal, select **Active Directory**, and then select hello name of hello directory.</span></span>

![Azure Active Directory'deki Configure (Yapılandır) sekmesi][1]

<span data-ttu-id="293e1-152">Ardından konuk kullanıcıların erişimini hello seçenekleri toocontrol düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="293e1-152">Then you can edit hello options toocontrol access for guest users.</span></span>

![konuk kullanıcılara yönelik erişim denetimi seçenekleri][2]

## <a name="whats-next"></a><span data-ttu-id="293e1-154">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="293e1-154">What's next</span></span>
* [<span data-ttu-id="293e1-155">Azure Active Directory'de diğer dizinlerden veya iş ortağı şirketlerden kullanıcılar ekleme</span><span class="sxs-lookup"><span data-stu-id="293e1-155">Add users from other directories or partner companies in Azure Active Directory</span></span>](active-directory-create-users-external.md)
* [<span data-ttu-id="293e1-156">Azure AD'yi yönetme</span><span class="sxs-lookup"><span data-stu-id="293e1-156">Administering Azure AD</span></span>](active-directory-administer.md)
* [<span data-ttu-id="293e1-157">Azure AD'de parolaları yönetme</span><span class="sxs-lookup"><span data-stu-id="293e1-157">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="293e1-158">Azure AD'de grupları yönetme</span><span class="sxs-lookup"><span data-stu-id="293e1-158">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
