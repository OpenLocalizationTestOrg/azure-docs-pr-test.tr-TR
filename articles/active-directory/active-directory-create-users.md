---
title: "Azure Active Directory'ye yeni kullanıcı ekleme | Microsoft Belgeleri"
description: "Azure Active Directory'de yeni kullanıcıların eklenmesini veya kullanıcı bilgilerinin değiştirilmesini açıklar."
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
ms.openlocfilehash: ff4b742e772a6062885313e9bb49e55907fe125a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-to-azure-active-directory"></a><span data-ttu-id="32bb1-103">Yeni kullanıcılar ya da Microsoft hesabı olan kullanıcıların Azure Active Directory'ye ekleme</span><span class="sxs-lookup"><span data-stu-id="32bb1-103">Add new users or users with Microsoft accounts to Azure Active Directory</span></span>
<span data-ttu-id="32bb1-104">Dizininizi doldurmak için kullanıcılar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="32bb1-104">Add users to populate your directory.</span></span> <span data-ttu-id="32bb1-105">Bu makalede kuruluşunuzdaki yeni kullanıcıların ve Microsoft hesabına sahip kullanıcıların nasıl ekleneceği açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="32bb1-105">This article explains how to add new users in your organization, and how to add users who have Microsoft accounts.</span></span> <span data-ttu-id="32bb1-106">Azure Active Directory'de diğer dizinlerden kullanıcı ekleme veya iş ortağı şirketlerden kullanıcı ekleme hakkında daha fazla bilgi için bkz. [Azure Active Directory'de diğer dizinlerden veya iş ortağı şirketlerden kullanıcılar ekleme](active-directory-create-users-external.md).</span><span class="sxs-lookup"><span data-stu-id="32bb1-106">For more information about adding users from other directories in Azure Active Directory or adding users from partner companies, see [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md).</span></span> <span data-ttu-id="32bb1-107">Eklenen kullanıcılar varsayılan olarak yönetici izinlerine sahip olmaz ancak bu kullanıcılara herhangi bir zamanda roller atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32bb1-107">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32bb1-108">Microsoft, Azure AD’yi bu makalede bahsedilen Klasik Azure Portalı yerine Azure portalındaki [Azure AD yönetim merkezini](https://aad.portal.azure.com) kullanarak yönetmenizi öneriyor.</span><span class="sxs-lookup"><span data-stu-id="32bb1-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="32bb1-109">Azure AD Yönetim Merkezi'nde bir kullanıcı eklemek için bkz: nasıl [Azure Active Directory'ye yeni kullanıcı ekleme](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="32bb1-109">For how to add a user in the Azure AD admin center, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="add-a-user"></a><span data-ttu-id="32bb1-110">Kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="32bb1-110">Add a user</span></span>
1. <span data-ttu-id="32bb1-111">Dizin için genel yönetici olan bir hesapla [klasik Azure portalında](https://manage.windowsazure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="32bb1-111">Sign in to the [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="32bb1-112">**Active Directory**'yi seçin ve ardından kuruluş dizininizin adını seçin.</span><span class="sxs-lookup"><span data-stu-id="32bb1-112">Select **Active Directory**, and then select the name of your organization directory.</span></span>
3. <span data-ttu-id="32bb1-113">**Users (Kullanıcılar)** sekmesini seçin ve ardından komut çubuğunda **Add User (Kullanıcı Ekle)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="32bb1-113">Select the **Users** tab, and then, in the command bar, select **Add User**.</span></span>
4. <span data-ttu-id="32bb1-114">**Tell us about this user (Bu kullanıcı hakkındaki görüşlerinizi bize bildirin)** sayfasında, **Type of user (Kullanıcı türü)** kısmında aşağıdaki seçeneklerden birini belirleyin:</span><span class="sxs-lookup"><span data-stu-id="32bb1-114">On the **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="32bb1-115">**New user in your organization (Kuruluşunuzdaki yeni kullanıcı)** - dizininize yeni bir kullanıcı hesabı ekler.</span><span class="sxs-lookup"><span data-stu-id="32bb1-115">**New user in your organization** – adds a new user account in your directory.</span></span>
   * <span data-ttu-id="32bb1-116">**User with an existing Microsoft account (Var olan bir Microsoft hesabı olan kullanıcı)** - Var olan bir Microsoft tüketici hesabını dizininize ekler (örneğin, bir Outlook hesabı)</span><span class="sxs-lookup"><span data-stu-id="32bb1-116">**User with an existing Microsoft account** – adds an existing Microsoft consumer account to your directory (for example, an Outlook account)</span></span>
5. <span data-ttu-id="32bb1-117">**Type of User (Kullanıcı Türü)** seçeneğine bağlı olarak, bir kullanıcı adı (yeni kullanıcı için) veya bir e-posta adresi (Microsoft hesabı olan bir kullanıcı için) girin.</span><span class="sxs-lookup"><span data-stu-id="32bb1-117">Depending on **Type of user**, enter a user name (for new user) or an email address (for a user with a Microsoft account).</span></span>
6. <span data-ttu-id="32bb1-118">**Profile (Profil)** sayfasında bir ad ve soyad, kolay ad ve **Roles (Roller)** listesinden bir kullanıcı rolü sağlayın.</span><span class="sxs-lookup"><span data-stu-id="32bb1-118">On the user **Profile** page, provide a first and last name, a user-friendly name, and a user role from the **Roles** list.</span></span> <span data-ttu-id="32bb1-119">Kullanıcı ve yönetici rolleri hakkında daha fazla bilgi için bkz. [Azure AD'de yönetici rolü atama](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="32bb1-119">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="32bb1-120">Kullanıcı için **Enable Multi-Factor Authentication (Multi-Factor Authentication'ı Etkinleştir)** seçeneğinin belirlenip belirlenmeyeceğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="32bb1-120">Specify whether to **Enable Multi-Factor Authentication** for the user.</span></span>
7. <span data-ttu-id="32bb1-121">**Get temporary password (Geçici parola alma)** sayfasında, **Create (Oluştur)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="32bb1-121">On the **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32bb1-122">Kuruluşunuz birden fazla etki alanı kullanıyorsa bir kullanıcı hesabını eklerken aşağıdakileri bilmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="32bb1-122">If your organization uses more than one domain, you should know about the following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="32bb1-123">Etki alanlarında aynı kullanıcı asıl adına (UPN) sahip kullanıcı hesaplarını eklemek için, örneğin, **önce** geoffgrisso@contoso.onmicrosoft.com hesabını ve **ardından** geoffgrisso@contoso.com hesabını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="32bb1-123">TO add user accounts with the same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="32bb1-124">geoffgrisso@contoso.onmicrosoft.com eklemeden önce geoffgrisso@contoso.com **eklemeyin**.</span><span class="sxs-lookup"><span data-stu-id="32bb1-124">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com.</span></span> <span data-ttu-id="32bb1-125">Bu sıra önemlidir, sıralamanın geri alınması ise çok uğraşmayı gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="32bb1-125">This order is important, and can be cumbersome to undo.</span></span>
>
>

## <a name="change-user-information"></a><span data-ttu-id="32bb1-126">Kullanıcı bilgilerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="32bb1-126">Change user information</span></span>
<span data-ttu-id="32bb1-127">Nesne kimliği dışındaki tüm kullanıcı özniteliklerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32bb1-127">You can change any user attribute except for the object ID.</span></span>

1. <span data-ttu-id="32bb1-128">Dizininizi açın.</span><span class="sxs-lookup"><span data-stu-id="32bb1-128">Open your directory.</span></span>
2. <span data-ttu-id="32bb1-129">**Users (Kullanıcılar)** sekmesini ve ardından değiştirmek istediğiniz kullanıcının görünen adını seçin.</span><span class="sxs-lookup"><span data-stu-id="32bb1-129">Select the **Users** tab, and then select the display name of the user you want to change.</span></span>
3. <span data-ttu-id="32bb1-130">Değişikliklerinizi tamamlayın ve ardından **Save (Kaydet)** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="32bb1-130">Complete your changes, and then click **Save**.</span></span>

<span data-ttu-id="32bb1-131">Değiştirdiğiniz kullanıcı şirket içi Active Directory hizmetinizle eşitlenmişse bu yordamı kullanarak kullanıcı bilgilerini değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="32bb1-131">If the user that you're changing is synchronized with your on-premises Active Directory service, you can't change the user information using this procedure.</span></span> <span data-ttu-id="32bb1-132">Kullanıcıyı değiştirmek için şirket içi Active Directory yönetim araçlarınızı kullanın.</span><span class="sxs-lookup"><span data-stu-id="32bb1-132">To change the user, use your on-premises Active Directory management tools.</span></span>

## <a name="guest-user-management-and-limitations"></a><span data-ttu-id="32bb1-133">Konuk kullanıcı yönetimi ve sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="32bb1-133">Guest user management and limitations</span></span>
<span data-ttu-id="32bb1-134">Konuk hesapları; SharePoint belgeleri, uygulamaları veya diğer Azure kaynaklarına erişmek için dizininize davet edilen, diğer dizinlerdeki kullanıcılardır.</span><span class="sxs-lookup"><span data-stu-id="32bb1-134">Guest accounts are users from other directories who were invited to your directory to access SharePoint documents, applications, or other Azure resources.</span></span> <span data-ttu-id="32bb1-135">Dizininizdeki bir kullanıcı hesabının temel alınan UserType özniteliği "Konuk" olarak ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="32bb1-135">A guest account in your directory has its underlying UserType attribute set to "Guest."</span></span> <span data-ttu-id="32bb1-136">Normal kullanıcıların (özellikle de dizininizin üyelerinin) temel alınan UserType özniteliği "Üye"dir.</span><span class="sxs-lookup"><span data-stu-id="32bb1-136">Regular users (specifically, members of your directory) have the UserType attribute "Member."</span></span>

<span data-ttu-id="32bb1-137">Konuklar, dizinde sınırlı bir haklar kümesine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="32bb1-137">Guests have a limited set of rights in the directory.</span></span> <span data-ttu-id="32bb1-138">Bu haklar, Konukların dizindeki diğer kullanıcılara ait bilgileri keşfetme becerisini sınırlandırır.</span><span class="sxs-lookup"><span data-stu-id="32bb1-138">These rights limit the ability for Guests to discover information about other users in the directory.</span></span> <span data-ttu-id="32bb1-139">Ancak konuk kullanıcılar çalışmakta oldukları kaynaklarla ilişkili olan kullanıcılarla ve gruplarla etkileşim kurmaya devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="32bb1-139">However, guest users can still interact with the users and groups associated with the resources they're working on.</span></span> <span data-ttu-id="32bb1-140">Konuk kullanıcılar şunları yapabilir:</span><span class="sxs-lookup"><span data-stu-id="32bb1-140">Guest users can:</span></span>

* <span data-ttu-id="32bb1-141">Atanmış oldukları bir Azure aboneliği ile ilişkili diğer kullanıcıları ve grupları görme</span><span class="sxs-lookup"><span data-stu-id="32bb1-141">See other users and groups associated with an Azure subscription to which they're assigned</span></span>
* <span data-ttu-id="32bb1-142">Ait oldukları grupların üyelerini görme</span><span class="sxs-lookup"><span data-stu-id="32bb1-142">See the members of groups to which they belong</span></span>
* <span data-ttu-id="32bb1-143">Dizinde bulunan tam e-posta adresini bildikleri diğer kullanıcıları arama</span><span class="sxs-lookup"><span data-stu-id="32bb1-143">Look up other users in the directory, if they know the full email address of the user</span></span>
* <span data-ttu-id="32bb1-144">Aradıkları kullanıcılara ait yalnızca sınırlı bir öznitelik kümesini görme; bu öznitelikler görünen ad, e-posta adresi, kullanıcı asıl adı (UPN) ve küçük resim fotoğrafı ile sınırlıdır</span><span class="sxs-lookup"><span data-stu-id="32bb1-144">See only a limited set of attributes of the users they look up--limited to display name, email address, user principal name (UPN), and thumbnail photo</span></span>
* <span data-ttu-id="32bb1-145">Dizinde doğrulanan etki alanlarının bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="32bb1-145">Get a list of verified domains in the directory</span></span>
* <span data-ttu-id="32bb1-146">Uygulamalara onay verme, bu uygulamalara dizininizdeki Üyelerin sahip olduklarıyla aynı erişimi sağlama</span><span class="sxs-lookup"><span data-stu-id="32bb1-146">Consent to applications, granting them the same access that Members have in your directory</span></span>

## <a name="set-guest-user-access-policies"></a><span data-ttu-id="32bb1-147">Konuk kullanıcı erişim ilkeleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="32bb1-147">Set guest user access policies</span></span>
<span data-ttu-id="32bb1-148">Bir dizinin **Configure (Yapılandır)** sekmesinde, konuk kullanıcıların erişimini denetlemeyi sağlayan seçenekler bulunur.</span><span class="sxs-lookup"><span data-stu-id="32bb1-148">The **Configure** tab of a directory includes options to control access for guest users.</span></span> <span data-ttu-id="32bb1-149">Bu seçenekler yalnızca klasik Azure portalında bir dizin genel yöneticisi tarafından değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="32bb1-149">These options can be changed only in Azure classic portal by a directory global administrator.</span></span> <span data-ttu-id="32bb1-150">Şu anda bir PowerShell veya API yöntemi bulunmamaktadır.</span><span class="sxs-lookup"><span data-stu-id="32bb1-150">Currently, there's no PowerShell or API method.</span></span>

<span data-ttu-id="32bb1-151">Klasik Azure portalında **Configure (Yapılandır)** sekmesini açmak için **Active Directory**'yi seçin ve ardından dizinin adını seçin.</span><span class="sxs-lookup"><span data-stu-id="32bb1-151">To open the **Configure** tab in the Azure classic portal, select **Active Directory**, and then select the name of the directory.</span></span>

![Azure Active Directory'deki Configure (Yapılandır) sekmesi][1]

<span data-ttu-id="32bb1-153">Ardından konuk kullanıcıların erişimini denetleme seçeneklerini düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32bb1-153">Then you can edit the options to control access for guest users.</span></span>

![konuk kullanıcılara yönelik erişim denetimi seçenekleri][2]

## <a name="whats-next"></a><span data-ttu-id="32bb1-155">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="32bb1-155">What's next</span></span>
* [<span data-ttu-id="32bb1-156">Azure Active Directory'de diğer dizinlerden veya iş ortağı şirketlerden kullanıcılar ekleme</span><span class="sxs-lookup"><span data-stu-id="32bb1-156">Add users from other directories or partner companies in Azure Active Directory</span></span>](active-directory-create-users-external.md)
* [<span data-ttu-id="32bb1-157">Azure AD'yi yönetme</span><span class="sxs-lookup"><span data-stu-id="32bb1-157">Administering Azure AD</span></span>](active-directory-administer.md)
* [<span data-ttu-id="32bb1-158">Azure AD'de parolaları yönetme</span><span class="sxs-lookup"><span data-stu-id="32bb1-158">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="32bb1-159">Azure AD'de grupları yönetme</span><span class="sxs-lookup"><span data-stu-id="32bb1-159">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
