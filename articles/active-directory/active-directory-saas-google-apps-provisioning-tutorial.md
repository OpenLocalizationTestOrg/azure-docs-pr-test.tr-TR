---
title: "Öğretici: Azure otomatik kullanıcı sağlamayı Google uygulamaları yapılandırma | Microsoft Docs"
description: "Otomatik olarak sağlamak ve Google Apps için kullanıcı hesapları Azure AD'den sağlanmasını öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: b061f0ddad70be4a5ca48d48d1a737d6af8afa8d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a><span data-ttu-id="e2c07-103">Öğretici: Otomatik kullanıcı sağlamayı için Google uygulamaları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e2c07-103">Tutorial: Configuring Google Apps for automatic user provisioning</span></span>

<span data-ttu-id="e2c07-104">Bu öğreticinin amacı, Google Apps ve Azure AD otomatik olarak sağlamak ve Google Apps için kullanıcı hesapları Azure AD'den sağlanmasını gerçekleştirmek için gereken adımları Göster sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="e2c07-104">The objective of this tutorial is to show you the steps you need to perform in Google Apps and Azure AD to automatically provision and de-provision user accounts from Azure AD to Google Apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2c07-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e2c07-105">Prerequisites</span></span>

<span data-ttu-id="e2c07-106">Bu öğreticide gösterilen senaryo, aşağıdaki öğeleri zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="e2c07-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="e2c07-107">Bir Azure Active directory kiracısı.</span><span class="sxs-lookup"><span data-stu-id="e2c07-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="e2c07-108">İş veya eğitim için Google Apps için Google Apps için geçerli bir kiracı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e2c07-108">You must have a valid tenant for Google Apps for Work or Google Apps for Education.</span></span> <span data-ttu-id="e2c07-109">Ücretsiz bir deneme hesabı ya da hizmet için kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="e2c07-109">You may use a free trial account for either service.</span></span>
*   <span data-ttu-id="e2c07-110">Google Apps takım yönetici izinlerine sahip bir kullanıcı hesabının.</span><span class="sxs-lookup"><span data-stu-id="e2c07-110">A user account in Google Apps with Team Admin permissions.</span></span>

## <a name="assigning-users-to-google-apps"></a><span data-ttu-id="e2c07-111">Google Apps kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="e2c07-111">Assigning users to Google Apps</span></span>

<span data-ttu-id="e2c07-112">Azure Active Directory "atamaları" adlı bir kavram hangi kullanıcıların seçili uygulamalara erişim alması belirlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="e2c07-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="e2c07-113">Otomatik olarak bir kullanıcı hesabı sağlama bağlamında, yalnızca kullanıcıların ve grupların "Azure AD uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="e2c07-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="e2c07-114">Yapılandırma ve sağlama hizmeti etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD grupları Google Apps uygulamanıza erişimi olması gereken kullanıcılar temsil eden karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e2c07-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Google Apps app.</span></span> <span data-ttu-id="e2c07-115">Karar sonra bu kullanıcılar, Google Apps uygulamanızın Buradaki yönergeleri izleyerek atayabilirsiniz: [bir kullanıcı veya grup için bir kuruluş uygulama atama](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="e2c07-115">Once decided, you can assign these users to your Google Apps app by following the instructions here: [Assign a user or group to an enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span></span>

> [!IMPORTANT]
>*   <span data-ttu-id="e2c07-116">Önerilir tek bir Azure AD kullanıcısının sağlama yapılandırmayı test etmek için Google Apps atanabilir.</span><span class="sxs-lookup"><span data-stu-id="e2c07-116">It is recommended that a single Azure AD user be assigned to Google Apps to test the provisioning configuration.</span></span> <span data-ttu-id="e2c07-117">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="e2c07-117">Additional users and/or groups may be assigned later.</span></span>
>*   <span data-ttu-id="e2c07-118">Bir kullanıcı için Google Apps atarken, kullanıcı ya da "Grup" rol ataması iletişim kutusunda seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e2c07-118">When assigning a user to Google Apps, you must select the User or "Group" role in the assignment dialog.</span></span> <span data-ttu-id="e2c07-119">"Varsayılan erişim" rolü sağlama için çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="e2c07-119">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="e2c07-120">Otomatik kullanıcı sağlamayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="e2c07-120">Enable automated user provisioning</span></span>

<span data-ttu-id="e2c07-121">Azure AD Google Apps'ın kullanıcı hesabı sağlama API'sine bağlanma ve sağlama hizmeti oluşturmak için yapılandırma güncelleştirmesi ve Google Apps atanan kullanıcı hesaplarında devre dışı bu bölümü kılavuzları kullanıcı ve grup atama Azure AD'de temel.</span><span class="sxs-lookup"><span data-stu-id="e2c07-121">This section guides you through connecting your Azure AD to Google Apps's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Google Apps based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="e2c07-122">Da tercih edebilirsiniz etkin SAML tabanlı çoklu oturum açma için Google Apps, yönergeleri izleyerek sağlanan [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e2c07-122">You may also choose to enabled SAML-based Single Sign-On for Google Apps, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e2c07-123">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="e2c07-123">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="configure-automatic-user-account-provisioning"></a><span data-ttu-id="e2c07-124">Hesap otomatik kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="e2c07-124">Configure automatic user account provisioning</span></span>

> [!NOTE]
> <span data-ttu-id="e2c07-125">Google Apps kullanıcı sağlamayı otomatikleştirmek için başka bir uygulanabilir seçenek kullanmaktır [Google Apps dizin eşitleme (GADS)](https://support.google.com/a/answer/106368?hl=en) Google Apps, şirket içi Active Directory kimlikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="e2c07-125">Another viable option for automating user provisioning to Google Apps is to use [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) which provisions your on-premises Active Directory identities to Google Apps.</span></span> <span data-ttu-id="e2c07-126">Buna karşılık, çözüm Bu öğreticide, Azure Active Directory (bulut) kullanıcıları ve Google Apps için posta özellikli gruplar sağlamasını yapar.</span><span class="sxs-lookup"><span data-stu-id="e2c07-126">In contrast, the solution in this tutorial provisions your Azure Active Directory (cloud) users and mail-enabled groups to Google Apps.</span></span> 

1. <span data-ttu-id="e2c07-127">Oturum [Google Apps Yönetici Konsolu](http://admin.google.com/) yönetici hesabı kullanarak ve tıklayın **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="e2c07-127">Sign into the [Google Apps Admin Console](http://admin.google.com/) using your administrator account, and click **Security**.</span></span> <span data-ttu-id="e2c07-128">Bağlantıyı görmüyorsanız, altında gizli olabilir **daha fazla denetim** ekranın altındaki menüsü.</span><span class="sxs-lookup"><span data-stu-id="e2c07-128">If you don't see the link, it may be hidden under the **More Controls** menu at the bottom of the screen.</span></span>
   
    ![Güvenlik'e tıklayın.][10]

2. <span data-ttu-id="e2c07-130">Üzerinde **güvenlik** sayfasında, **API Başvurusu**.</span><span class="sxs-lookup"><span data-stu-id="e2c07-130">On the **Security** page, click **API Reference**.</span></span>
   
    ![API Başvurusu'ı tıklatın.][15]

3. <span data-ttu-id="e2c07-132">Seçin **etkinleştirmek API erişimini**.</span><span class="sxs-lookup"><span data-stu-id="e2c07-132">Select **Enable API access**.</span></span>
   
    ![API Başvurusu'ı tıklatın.][16]

    > [!IMPORTANT]
    > <span data-ttu-id="e2c07-134">Google Apps, Azure Active Directory'de kullanıcı adlarını sağlamak istediğiniz her kullanıcı için *gerekir* özel bir etki alanına bağlı.</span><span class="sxs-lookup"><span data-stu-id="e2c07-134">For every user that you intend to provision to Google Apps, their username in Azure Active Directory *must* be tied to a custom domain.</span></span> <span data-ttu-id="e2c07-135">Örneğin, neye benzediğini gösteren kullanıcı adları bob@contoso.onmicrosoft.com ancak Google Apps tarafından kabul edilmiyor bob@contoso.com kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="e2c07-135">For example, usernames that look like bob@contoso.onmicrosoft.com is not accepted by Google Apps, whereas bob@contoso.com is accepted.</span></span> <span data-ttu-id="e2c07-136">Mevcut bir kullanıcının etki alanı Azure AD'de özelliklerini düzenleyerek değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2c07-136">You can change an existing user's domain by editing their properties in Azure AD.</span></span> <span data-ttu-id="e2c07-137">Yönergeler için Azure Active Directory ve Google Apps için özel bir etki alanı ayarlama adımları izleyerek dahil edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e2c07-137">Instructions for how to set a custom domain for both Azure Active Directory and Google Apps are included in following steps.</span></span>
      
4. <span data-ttu-id="e2c07-138">Ardından, bir özel etki alanı adı, Azure Active Directory'ye henüz eklemediyseniz, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="e2c07-138">If you haven't added a custom domain name to your Azure Active Directory yet, then follow the following steps:</span></span>
  
    <span data-ttu-id="e2c07-139">a.</span><span class="sxs-lookup"><span data-stu-id="e2c07-139">a.</span></span> <span data-ttu-id="e2c07-140">İçinde [Azure portal](https://portal.azure.com), sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e2c07-140">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span> <span data-ttu-id="e2c07-141">Dizin listesinde dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="e2c07-141">In the directory list, select your directory.</span></span> 

    <span data-ttu-id="e2c07-142">b.</span><span class="sxs-lookup"><span data-stu-id="e2c07-142">b.</span></span> <span data-ttu-id="e2c07-143">Tıklatın **etki alanı adı** sol gezinti bölmesinde ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e2c07-143">Click **Domains name** on the left navigation pane, and then click **Add**.</span></span>
     
     ![Etki alanı](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![etki alanı ekleme](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    <span data-ttu-id="e2c07-146">c.</span><span class="sxs-lookup"><span data-stu-id="e2c07-146">c.</span></span> <span data-ttu-id="e2c07-147">Etki alanı adınızı yazın **etki alanı adı** alan.</span><span class="sxs-lookup"><span data-stu-id="e2c07-147">Type your domain name into the **Domain name** field.</span></span> <span data-ttu-id="e2c07-148">Bu etki alanı adı, Google uygulamaları için kullanmak istediğiniz aynı etki alanı adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e2c07-148">This domain name should be the same domain name that you intend to use for Google Apps.</span></span> <span data-ttu-id="e2c07-149">Hazır olduğunuzda tıklatın **etki alanı Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e2c07-149">When ready, click the **Add Domain** button.</span></span>
     
     ![Etki alanı adı](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    <span data-ttu-id="e2c07-151">d.</span><span class="sxs-lookup"><span data-stu-id="e2c07-151">d.</span></span> <span data-ttu-id="e2c07-152">Tıklatın **sonraki** doğrulama sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="e2c07-152">Click **Next** to go to the verification page.</span></span> <span data-ttu-id="e2c07-153">Bu etki alanına ait olduğunu doğrulamak için etki alanının DNS kayıtlarını bu sayfada sağlanan değerlere göre düzenlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e2c07-153">To verify that you own this domain, you must edit the domain's DNS records according to the values provided on this page.</span></span> <span data-ttu-id="e2c07-154">Kullanarak doğrulamak seçebilirsiniz **MX kayıtları** veya **TXT kayıtlarının**için seçtiğiniz bağlı olarak **kayıt türü** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="e2c07-154">You may choose to verify using either **MX records** or **TXT records**, depending on what you select for the **Record Type** option.</span></span> <span data-ttu-id="e2c07-155">Azure AD etki alanı adıyla doğrulamak nasıl daha kapsamlı yönergeler için bkz [kendi etki alanı adını Azure AD'ye ekleme](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="e2c07-155">For more comprehensive instructions on how to verify domain name with Azure AD, refer [Add your own domain name to Azure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span></span>
     
     ![Etki alanı](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    <span data-ttu-id="e2c07-157">e.</span><span class="sxs-lookup"><span data-stu-id="e2c07-157">e.</span></span> <span data-ttu-id="e2c07-158">Dizininize eklemek istediğiniz tüm etki alanları için önceki adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="e2c07-158">Repeat the preceding steps for all the domains that you intend to add to your directory.</span></span>

5. <span data-ttu-id="e2c07-159">Azure AD ile etki alanları doğruladıktan, artık bunları yeniden Google Apps ile doğrulamanız gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="e2c07-159">Now that you have verified all your domains with Azure AD, you must now verify them again with Google Apps.</span></span> <span data-ttu-id="e2c07-160">Google Apps ile zaten kayıtlı değil her etki alanı için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e2c07-160">For each domain that isn't already registered with Google Apps, perform the following steps:</span></span>
   
    <span data-ttu-id="e2c07-161">a.</span><span class="sxs-lookup"><span data-stu-id="e2c07-161">a.</span></span> <span data-ttu-id="e2c07-162">İçinde [Google Apps Yönetici Konsolu](http://admin.google.com/), tıklatın **etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="e2c07-162">In the [Google Apps Admin Console](http://admin.google.com/), click **Domains**.</span></span>
     
     ![Etki alanlarında tıklatın][20]

    <span data-ttu-id="e2c07-164">b.</span><span class="sxs-lookup"><span data-stu-id="e2c07-164">b.</span></span> <span data-ttu-id="e2c07-165">Tıklatın **bir etki alanı veya bir etki alanı diğer adı eklemek**.</span><span class="sxs-lookup"><span data-stu-id="e2c07-165">Click **Add a domain or a domain alias**.</span></span>
     
     ![Yeni bir etki alanı Ekle][21]

    <span data-ttu-id="e2c07-167">c.</span><span class="sxs-lookup"><span data-stu-id="e2c07-167">c.</span></span> <span data-ttu-id="e2c07-168">Seçin **başka bir etki alanı ekleme**ve eklemek istediğiniz etki alanı adını yazın.</span><span class="sxs-lookup"><span data-stu-id="e2c07-168">Select **Add another domain**, and type in the name of the domain that you would like to add.</span></span>
     
     ![Etki alanı adınızı yazın][22]

    <span data-ttu-id="e2c07-170">d.</span><span class="sxs-lookup"><span data-stu-id="e2c07-170">d.</span></span> <span data-ttu-id="e2c07-171">Tıklatın **devam ve etki alanı sahipliği doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="e2c07-171">Click **Continue and verify domain ownership**.</span></span> <span data-ttu-id="e2c07-172">Sonra etki alanı adının size ait olduğunu doğrulamak için adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="e2c07-172">Then follow the steps to verify that you own the domain name.</span></span> <span data-ttu-id="e2c07-173">Google Apps etki alanınızı doğrulayın konusunda kapsamlı yönergeler için bkz.</span><span class="sxs-lookup"><span data-stu-id="e2c07-173">For comprehensive instructions on how to verify your domain with Google Apps, see.</span></span> <span data-ttu-id="e2c07-174">[Google Apps ile site sahipliği doğrulamak](https://support.google.com/webmasters/answer/35179).</span><span class="sxs-lookup"><span data-stu-id="e2c07-174">[Verify your site ownership with Google Apps](https://support.google.com/webmasters/answer/35179).</span></span>

    <span data-ttu-id="e2c07-175">e.</span><span class="sxs-lookup"><span data-stu-id="e2c07-175">e.</span></span> <span data-ttu-id="e2c07-176">Google Apps için eklemek istediğiniz her ek etki alanları için önceki adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="e2c07-176">Repeat the preceding steps for any additional domains that you intend to add to Google Apps.</span></span>
     
     > [!WARNING]
     > <span data-ttu-id="e2c07-177">Google Apps kiracınız için birincil etki alanı değiştirmek ve zaten var, yapılandırılan çoklu oturum açma Azure AD ile durumunda #3. adım altında yinelemek zorunda [adım iki: etkinleştirmek çoklu oturum açma](#step-two-enable-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="e2c07-177">If you change the primary domain for your Google Apps tenant, and if you have already configured single sign-on with Azure AD, then you have to repeat step #3 under [Step Two: Enable Single Sign-On](#step-two-enable-single-sign-on).</span></span>
       
6. <span data-ttu-id="e2c07-178">İçinde [Google Apps Yönetici Konsolu](http://admin.google.com/), tıklatın **yönetici rollerine**.</span><span class="sxs-lookup"><span data-stu-id="e2c07-178">In the [Google Apps Admin Console](http://admin.google.com/), click **Admin Roles**.</span></span>
   
     ![Google Apps'ı tıklatın][26]

7. <span data-ttu-id="e2c07-180">Kullanıcı sağlamayı yönetmek için kullanmak istediğiniz yönetici hesabı belirleyin.</span><span class="sxs-lookup"><span data-stu-id="e2c07-180">Determine which admin account you would like to use to manage user provisioning.</span></span> <span data-ttu-id="e2c07-181">İçin **Yönetici rolü** bu hesabı, düzenleme **ayrıcalıkları** bu rol için.</span><span class="sxs-lookup"><span data-stu-id="e2c07-181">For the **admin role** of that account, edit the **Privileges** for that role.</span></span> <span data-ttu-id="e2c07-182">Tüm olduğundan emin olun **yönetici API ayrıcalıkları** sağlamak için bu hesabı kullanılabilir böylece etkin.</span><span class="sxs-lookup"><span data-stu-id="e2c07-182">Make sure it has all the **Admin API Privileges** enabled so that this account can be used for provisioning.</span></span>
   
     ![Google Apps'ı tıklatın][27]
   
    > [!NOTE]
    > <span data-ttu-id="e2c07-184">Bir üretim ortamında yapılandırıyorsanız, en iyi uygulama olarak bir yönetici hesabı Google Apps özellikle bu adım için oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="e2c07-184">If you are configuring a production environment, the best practice is to create an admin account in Google Apps specifically for this step.</span></span> <span data-ttu-id="e2c07-185">Bu hesaplar gerekli API ayrıcalıklara sahip bir yönetici rolü kendisiyle ilişkilendirilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e2c07-185">These accounts must have an admin role associated with it that has the necessary API privileges.</span></span>
     
8. <span data-ttu-id="e2c07-186">İçinde [Azure portal](https://portal.azure.com), Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="e2c07-186">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

9. <span data-ttu-id="e2c07-187">Çoklu oturum açma için Google Apps zaten yapılandırdıysanız arama alanı kullanarak Google Apps Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="e2c07-187">If you have already configured Google Apps for single sign-on, search for your instance of Google Apps using the search field.</span></span> <span data-ttu-id="e2c07-188">Aksi takdirde seçin **Ekle** arayın ve **Google Apps** uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="e2c07-188">Otherwise, select **Add** and search for **Google Apps** in the application gallery.</span></span> <span data-ttu-id="e2c07-189">Arama sonuçlarından Google Apps seçin ve uygulamaları listenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e2c07-189">Select Google Apps from the search results, and add it to your list of applications.</span></span>

10. <span data-ttu-id="e2c07-190">Google Apps örneğiniz seçin ve ardından **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="e2c07-190">Select your instance of Google Apps, then select the **Provisioning** tab.</span></span>

11. <span data-ttu-id="e2c07-191">Ayarlama **sağlama modunda** için **otomatik**.</span><span class="sxs-lookup"><span data-stu-id="e2c07-191">Set the **Provisioning Mode** to **Automatic**.</span></span> 

     ![Sağlama](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. <span data-ttu-id="e2c07-193">Altında **yönetici kimlik bilgileri** 'yi tıklatın **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="e2c07-193">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="e2c07-194">Yeni bir tarayıcı penceresinde bir Google Apps yetkilendirme iletişim kutusunu açar.</span><span class="sxs-lookup"><span data-stu-id="e2c07-194">It opens a Google Apps authorization dialog in a new browser window.</span></span>

13. <span data-ttu-id="e2c07-195">Google Apps kiracınız değişiklik yapmak için Azure Active Directory izni vermek istediğiniz onaylayın.</span><span class="sxs-lookup"><span data-stu-id="e2c07-195">Confirm that you would like to give Azure Active Directory permission to make changes to your Google Apps tenant.</span></span> <span data-ttu-id="e2c07-196">Tıklatın **kabul**.</span><span class="sxs-lookup"><span data-stu-id="e2c07-196">Click **Accept**.</span></span>
    
     ![İzinleri doğrulayın.][28]

14. <span data-ttu-id="e2c07-198">Azure portalında tıklatın **Bağlantıyı Sına** Azure emin olmak için AD, Google Apps uygulamanızın bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="e2c07-198">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Google Apps app.</span></span> <span data-ttu-id="e2c07-199">Bağlantı başarısız olursa, Google Apps hesabınız takım yönetici izinlerine sahip olduğundan emin olun ve deneyin **"Yetkilendir"** adım yeniden uygulayın.</span><span class="sxs-lookup"><span data-stu-id="e2c07-199">If the connection fails, ensure your Google Apps account has Team Admin permissions and try the **"Authorize"** step again.</span></span>

15. <span data-ttu-id="e2c07-200">Bir kişi veya sağlama hata bildirimleri alması gereken Grup e-posta adresini girin **bildirim e-posta** alan ve onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="e2c07-200">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

16. <span data-ttu-id="e2c07-201">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="e2c07-201">Click **Save.**</span></span>

17. <span data-ttu-id="e2c07-202">Eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları Google Apps için.**</span><span class="sxs-lookup"><span data-stu-id="e2c07-202">Under the Mappings section, select **Synchronize Azure Active Directory Users to Google Apps.**</span></span>

18. <span data-ttu-id="e2c07-203">İçinde **öznitelik eşlemelerini** bölümünde, Google Apps Azure AD'den eşitlenen kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="e2c07-203">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Google Apps.</span></span> <span data-ttu-id="e2c07-204">Seçilen öznitelikler **eşleşen** özellikleri, Google Apps kullanıcı hesaplarında güncelleştirme işlemleri için eşleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e2c07-204">The attributes selected as **Matching** properties are used to match the user accounts in Google Apps for update operations.</span></span> <span data-ttu-id="e2c07-205">Değişiklikleri kaydetmek için Kaydet düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="e2c07-205">Select the Save button to commit any changes.</span></span>

19. <span data-ttu-id="e2c07-206">Google Apps için hizmet sağlama Azure AD etkinleştirmek için değiştirmek **sağlama durumu** için **üzerinde** ayarları bölümünde</span><span class="sxs-lookup"><span data-stu-id="e2c07-206">To enable the Azure AD provisioning service for Google Apps, change the **Provisioning Status** to **On** in the Settings section</span></span>

20. <span data-ttu-id="e2c07-207">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="e2c07-207">Click **Save.**</span></span>

<span data-ttu-id="e2c07-208">Herhangi bir kullanıcı ve/veya grupları kullanıcıları ve grupları bölümünde Google Apps atanan ilk eşitleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="e2c07-208">It starts the initial synchronization of any users and/or groups assigned to Google Apps in the Users and Groups section.</span></span> <span data-ttu-id="e2c07-209">İlk eşitleme gerçekleştirmek yaklaşık 20 dakikada çalıştığı sürece oluşan sonraki eşitlemeler uzun sürer.</span><span class="sxs-lookup"><span data-stu-id="e2c07-209">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="e2c07-210">Kullanabileceğiniz **eşitleme ayrıntıları** bölüm ilerlemeyi izlemek ve Google Apps uygulamanızı sağlama hizmeti tarafından gerçekleştirilen tüm eylemler açıklanmaktadır etkinlik raporları sağlamak için bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="e2c07-210">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Google Apps app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e2c07-211">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e2c07-211">Additional resources</span></span>

* [<span data-ttu-id="e2c07-212">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="e2c07-212">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e2c07-213">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e2c07-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="e2c07-214">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e2c07-214">Configure Single Sign-on</span></span>](active-directory-saas-google-apps-tutorial.md)



<!--Image references-->

[10]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-security.png
[15]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api-enabled.png
[20]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-another.png
[24]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-auth.png