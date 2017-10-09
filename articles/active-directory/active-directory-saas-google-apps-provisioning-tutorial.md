---
title: "Öğretici: Azure otomatik kullanıcı sağlamayı Google uygulamaları yapılandırma | Microsoft Docs"
description: "Azure AD tooGoogle uygulamaları ' nasıl tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesapları öğrenin."
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
ms.openlocfilehash: d1fa8449bd6013d1627b3552aaa19db1c0f4f46f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a><span data-ttu-id="eab36-103">Öğretici: Otomatik kullanıcı sağlamayı için Google uygulamaları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="eab36-103">Tutorial: Configuring Google Apps for automatic user provisioning</span></span>

<span data-ttu-id="eab36-104">Bu öğreticinin Hello hedefi Google Apps ve Azure AD tooautomatically sağlama tooperform gerekir ve Azure AD tooGoogle uygulamalar kullanıcı hesaplarından sağlanmasını adımları hello tooshow ' dir.</span><span class="sxs-lookup"><span data-stu-id="eab36-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Google Apps and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooGoogle Apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eab36-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="eab36-105">Prerequisites</span></span>

<span data-ttu-id="eab36-106">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="eab36-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="eab36-107">Bir Azure Active directory kiracısı.</span><span class="sxs-lookup"><span data-stu-id="eab36-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="eab36-108">İş veya eğitim için Google Apps için Google Apps için geçerli bir kiracı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eab36-108">You must have a valid tenant for Google Apps for Work or Google Apps for Education.</span></span> <span data-ttu-id="eab36-109">Ücretsiz bir deneme hesabı ya da hizmet için kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="eab36-109">You may use a free trial account for either service.</span></span>
*   <span data-ttu-id="eab36-110">Google Apps takım yönetici izinlerine sahip bir kullanıcı hesabının.</span><span class="sxs-lookup"><span data-stu-id="eab36-110">A user account in Google Apps with Team Admin permissions.</span></span>

## <a name="assigning-users-toogoogle-apps"></a><span data-ttu-id="eab36-111">Kullanıcıları tooGoogle uygulamalar atama</span><span class="sxs-lookup"><span data-stu-id="eab36-111">Assigning users tooGoogle Apps</span></span>

<span data-ttu-id="eab36-112">Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır.</span><span class="sxs-lookup"><span data-stu-id="eab36-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="eab36-113">Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="eab36-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="eab36-114">Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD tooyour Google Apps uygulamasına erişmesi hello kullanıcıları temsil gruplarında toodecide gerekir.</span><span class="sxs-lookup"><span data-stu-id="eab36-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Google Apps app.</span></span> <span data-ttu-id="eab36-115">Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour Google Apps uygulama atayabilirsiniz: [bir kullanıcı veya grup tooan kuruluş uygulama atama](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="eab36-115">Once decided, you can assign these users tooyour Google Apps app by following hello instructions here: [Assign a user or group tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span></span>

> [!IMPORTANT]
>*   <span data-ttu-id="eab36-116">Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooGoogle uygulamaları tootest hello atanabilir.</span><span class="sxs-lookup"><span data-stu-id="eab36-116">It is recommended that a single Azure AD user be assigned tooGoogle Apps tootest hello provisioning configuration.</span></span> <span data-ttu-id="eab36-117">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="eab36-117">Additional users and/or groups may be assigned later.</span></span>
>*   <span data-ttu-id="eab36-118">Bir kullanıcı tooGoogle uygulamaları atarken hello atama iletişim kutusunda hello kullanıcı ya da "Grup" rolünü seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="eab36-118">When assigning a user tooGoogle Apps, you must select hello User or "Group" role in hello assignment dialog.</span></span> <span data-ttu-id="eab36-119">Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="eab36-119">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="eab36-120">Otomatik kullanıcı sağlamayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="eab36-120">Enable automated user provisioning</span></span>

<span data-ttu-id="eab36-121">Bu bölümde, Azure AD tooGoogle uygulamalarınızı'nın kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve Google Apps Azure AD'de kullanıcı ve grup atama göre atanan kullanıcı hesaplarında devre dışı bırak .</span><span class="sxs-lookup"><span data-stu-id="eab36-121">This section guides you through connecting your Azure AD tooGoogle Apps's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Google Apps based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="eab36-122">Sağlanan hello yönergeleri izleyerek Google Apps için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="eab36-122">You may also choose tooenabled SAML-based Single Sign-On for Google Apps, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="eab36-123">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="eab36-123">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="configure-automatic-user-account-provisioning"></a><span data-ttu-id="eab36-124">Hesap otomatik kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="eab36-124">Configure automatic user account provisioning</span></span>

> [!NOTE]
> <span data-ttu-id="eab36-125">Kullanıcı tooGoogle uygulamaları hazırlama otomatikleştirmek için başka bir uygun toouse seçenektir [Google Apps dizin eşitleme (GADS)](https://support.google.com/a/answer/106368?hl=en) , şirket içi Active Directory kimlikleri tooGoogle uygulamaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="eab36-125">Another viable option for automating user provisioning tooGoogle Apps is toouse [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) which provisions your on-premises Active Directory identities tooGoogle Apps.</span></span> <span data-ttu-id="eab36-126">Buna karşılık, hello çözümü Bu öğreticide, Azure Active Directory (bulut) kullanıcıları ve posta özellikli gruplar tooGoogle uygulamaları sağlamasını yapar.</span><span class="sxs-lookup"><span data-stu-id="eab36-126">In contrast, hello solution in this tutorial provisions your Azure Active Directory (cloud) users and mail-enabled groups tooGoogle Apps.</span></span> 

1. <span data-ttu-id="eab36-127">Merhaba içine oturum [Google Apps Yönetici Konsolu](http://admin.google.com/) yönetici hesabı kullanarak ve tıklayın **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="eab36-127">Sign into hello [Google Apps Admin Console](http://admin.google.com/) using your administrator account, and click **Security**.</span></span> <span data-ttu-id="eab36-128">Merhaba bağlantısını görmüyorsanız, hello altında gizli olabilir **daha fazla denetim** hello ekranın hello menüsünde.</span><span class="sxs-lookup"><span data-stu-id="eab36-128">If you don't see hello link, it may be hidden under hello **More Controls** menu at hello bottom of hello screen.</span></span>
   
    ![Güvenlik'e tıklayın.][10]

2. <span data-ttu-id="eab36-130">Merhaba üzerinde **güvenlik** sayfasında, **API Başvurusu**.</span><span class="sxs-lookup"><span data-stu-id="eab36-130">On hello **Security** page, click **API Reference**.</span></span>
   
    ![API Başvurusu'ı tıklatın.][15]

3. <span data-ttu-id="eab36-132">Seçin **etkinleştirmek API erişimini**.</span><span class="sxs-lookup"><span data-stu-id="eab36-132">Select **Enable API access**.</span></span>
   
    ![API Başvurusu'ı tıklatın.][16]

    > [!IMPORTANT]
    > <span data-ttu-id="eab36-134">Tooprovision tooGoogle uygulamaları, Azure Active Directory'de kullanıcı adlarını düşündüğünüz her kullanıcı için *gerekir* bağlı tooa özel etki alanı olması.</span><span class="sxs-lookup"><span data-stu-id="eab36-134">For every user that you intend tooprovision tooGoogle Apps, their username in Azure Active Directory *must* be tied tooa custom domain.</span></span> <span data-ttu-id="eab36-135">Örneğin, neye benzediğini gösteren kullanıcı adları bob@contoso.onmicrosoft.com ancak Google Apps tarafından kabul edilmiyor bob@contoso.com kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="eab36-135">For example, usernames that look like bob@contoso.onmicrosoft.com is not accepted by Google Apps, whereas bob@contoso.com is accepted.</span></span> <span data-ttu-id="eab36-136">Mevcut bir kullanıcının etki alanı Azure AD'de özelliklerini düzenleyerek değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eab36-136">You can change an existing user's domain by editing their properties in Azure AD.</span></span> <span data-ttu-id="eab36-137">Yönergeler nasıl tooset Azure Active Directory ve Google Apps için özel bir etki alanı dahil edilmiştir için adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="eab36-137">Instructions for how tooset a custom domain for both Azure Active Directory and Google Apps are included in following steps.</span></span>
      
4. <span data-ttu-id="eab36-138">Özel etki alanı adı tooyour Azure Active Directory henüz eklemediyseniz, hello aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="eab36-138">If you haven't added a custom domain name tooyour Azure Active Directory yet, then follow hello following steps:</span></span>
  
    <span data-ttu-id="eab36-139">a.</span><span class="sxs-lookup"><span data-stu-id="eab36-139">a.</span></span> <span data-ttu-id="eab36-140">Merhaba, [Azure portal](https://portal.azure.com), üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="eab36-140">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span> <span data-ttu-id="eab36-141">Merhaba dizin listesinde dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="eab36-141">In hello directory list, select your directory.</span></span> 

    <span data-ttu-id="eab36-142">b.</span><span class="sxs-lookup"><span data-stu-id="eab36-142">b.</span></span> <span data-ttu-id="eab36-143">Tıklatın **etki alanı adı** üzerinde sol gezinti bölmesinde hello ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="eab36-143">Click **Domains name** on hello left navigation pane, and then click **Add**.</span></span>
     
     ![Etki alanı](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![etki alanı ekleme](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    <span data-ttu-id="eab36-146">c.</span><span class="sxs-lookup"><span data-stu-id="eab36-146">c.</span></span> <span data-ttu-id="eab36-147">Etki alanı adınızı hello yazın **etki alanı adı** alan.</span><span class="sxs-lookup"><span data-stu-id="eab36-147">Type your domain name into hello **Domain name** field.</span></span> <span data-ttu-id="eab36-148">Bu etki alanı adı hello olmalıdır Google Apps için toouse düşündüğünüz aynı etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="eab36-148">This domain name should be hello same domain name that you intend toouse for Google Apps.</span></span> <span data-ttu-id="eab36-149">Hazır olduğunuzda hello tıklatın **etki alanı Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eab36-149">When ready, click hello **Add Domain** button.</span></span>
     
     ![Etki alanı adı](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    <span data-ttu-id="eab36-151">d.</span><span class="sxs-lookup"><span data-stu-id="eab36-151">d.</span></span> <span data-ttu-id="eab36-152">Tıklatın **sonraki** toogo toohello doğrulama sayfasında.</span><span class="sxs-lookup"><span data-stu-id="eab36-152">Click **Next** toogo toohello verification page.</span></span> <span data-ttu-id="eab36-153">Bu etki alanı kendi tooverify, bu sayfada sağlanan toohello değerleri göre hello etki alanının DNS kayıtlarını düzenlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="eab36-153">tooverify that you own this domain, you must edit hello domain's DNS records according toohello values provided on this page.</span></span> <span data-ttu-id="eab36-154">Kullanarak tooverify seçebilirsiniz **MX kayıtları** veya **TXT kayıtlarının**Merhaba seçin bağlı olarak **kayıt türü** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="eab36-154">You may choose tooverify using either **MX records** or **TXT records**, depending on what you select for hello **Record Type** option.</span></span> <span data-ttu-id="eab36-155">Nasıl tooverify etki alanı adı Azure AD ile daha kapsamlı yönergeler için bkz [kendi etki alanı adı tooAzure AD eklemek](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="eab36-155">For more comprehensive instructions on how tooverify domain name with Azure AD, refer [Add your own domain name tooAzure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span></span>
     
     ![Etki alanı](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    <span data-ttu-id="eab36-157">e.</span><span class="sxs-lookup"><span data-stu-id="eab36-157">e.</span></span> <span data-ttu-id="eab36-158">Merhaba önceki adımları tooadd tooyour directory düşündüğünüz tüm hello etki alanları için yineleyin.</span><span class="sxs-lookup"><span data-stu-id="eab36-158">Repeat hello preceding steps for all hello domains that you intend tooadd tooyour directory.</span></span>

5. <span data-ttu-id="eab36-159">Azure AD ile etki alanları doğruladıktan, artık bunları yeniden Google Apps ile doğrulamanız gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="eab36-159">Now that you have verified all your domains with Azure AD, you must now verify them again with Google Apps.</span></span> <span data-ttu-id="eab36-160">Google Apps ile zaten kayıtlı değil her etki alanı için hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="eab36-160">For each domain that isn't already registered with Google Apps, perform hello following steps:</span></span>
   
    <span data-ttu-id="eab36-161">a.</span><span class="sxs-lookup"><span data-stu-id="eab36-161">a.</span></span> <span data-ttu-id="eab36-162">Merhaba, [Google Apps Yönetici Konsolu](http://admin.google.com/), tıklatın **etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="eab36-162">In hello [Google Apps Admin Console](http://admin.google.com/), click **Domains**.</span></span>
     
     ![Etki alanlarında tıklatın][20]

    <span data-ttu-id="eab36-164">b.</span><span class="sxs-lookup"><span data-stu-id="eab36-164">b.</span></span> <span data-ttu-id="eab36-165">Tıklatın **bir etki alanı veya bir etki alanı diğer adı eklemek**.</span><span class="sxs-lookup"><span data-stu-id="eab36-165">Click **Add a domain or a domain alias**.</span></span>
     
     ![Yeni bir etki alanı Ekle][21]

    <span data-ttu-id="eab36-167">c.</span><span class="sxs-lookup"><span data-stu-id="eab36-167">c.</span></span> <span data-ttu-id="eab36-168">Seçin **başka bir etki alanı ekleme**, tooadd istediğiniz hello etki alanının hello adı yazın.</span><span class="sxs-lookup"><span data-stu-id="eab36-168">Select **Add another domain**, and type in hello name of hello domain that you would like tooadd.</span></span>
     
     ![Etki alanı adınızı yazın][22]

    <span data-ttu-id="eab36-170">d.</span><span class="sxs-lookup"><span data-stu-id="eab36-170">d.</span></span> <span data-ttu-id="eab36-171">Tıklatın **devam ve etki alanı sahipliği doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="eab36-171">Click **Continue and verify domain ownership**.</span></span> <span data-ttu-id="eab36-172">Daha sonra hello etki alanı adını kendi hello adımları tooverify izleyin.</span><span class="sxs-lookup"><span data-stu-id="eab36-172">Then follow hello steps tooverify that you own hello domain name.</span></span> <span data-ttu-id="eab36-173">Kapsamlı yönergeler nasıl tooverify Google Apps etki alanınızı bakın.</span><span class="sxs-lookup"><span data-stu-id="eab36-173">For comprehensive instructions on how tooverify your domain with Google Apps, see.</span></span> <span data-ttu-id="eab36-174">[Google Apps ile site sahipliği doğrulamak](https://support.google.com/webmasters/answer/35179).</span><span class="sxs-lookup"><span data-stu-id="eab36-174">[Verify your site ownership with Google Apps](https://support.google.com/webmasters/answer/35179).</span></span>

    <span data-ttu-id="eab36-175">e.</span><span class="sxs-lookup"><span data-stu-id="eab36-175">e.</span></span> <span data-ttu-id="eab36-176">Adımları tooadd tooGoogle uygulamaları düşündüğünüz diğer etki alanlarını için önceki hello yineleyin.</span><span class="sxs-lookup"><span data-stu-id="eab36-176">Repeat hello preceding steps for any additional domains that you intend tooadd tooGoogle Apps.</span></span>
     
     > [!WARNING]
     > <span data-ttu-id="eab36-177">Google Apps kiracınız için hello birincil etki alanı değiştirmek ve zaten var, yapılandırılan çoklu oturum açma Azure AD ile durumunda toorepeat adımı #3 altında sahip [adım iki: etkinleştirmek çoklu oturum açma](#step-two-enable-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="eab36-177">If you change hello primary domain for your Google Apps tenant, and if you have already configured single sign-on with Azure AD, then you have toorepeat step #3 under [Step Two: Enable Single Sign-On](#step-two-enable-single-sign-on).</span></span>
       
6. <span data-ttu-id="eab36-178">Merhaba, [Google Apps Yönetici Konsolu](http://admin.google.com/), tıklatın **yönetici rollerine**.</span><span class="sxs-lookup"><span data-stu-id="eab36-178">In hello [Google Apps Admin Console](http://admin.google.com/), click **Admin Roles**.</span></span>
   
     ![Google Apps'ı tıklatın][26]

7. <span data-ttu-id="eab36-180">Hangi yönetim belirlemek istediğinizi toouse toomanage kullanıcı sağlamayı hesabı.</span><span class="sxs-lookup"><span data-stu-id="eab36-180">Determine which admin account you would like toouse toomanage user provisioning.</span></span> <span data-ttu-id="eab36-181">Hello için **Yönetici rolü** bu hesabı, hello Düzenle **ayrıcalıkları** bu rol için.</span><span class="sxs-lookup"><span data-stu-id="eab36-181">For hello **admin role** of that account, edit hello **Privileges** for that role.</span></span> <span data-ttu-id="eab36-182">Tüm hello olduğundan emin olun **yönetici API ayrıcalıkları** sağlamak için bu hesabı kullanılabilir böylece etkin.</span><span class="sxs-lookup"><span data-stu-id="eab36-182">Make sure it has all hello **Admin API Privileges** enabled so that this account can be used for provisioning.</span></span>
   
     ![Google Apps'ı tıklatın][27]
   
    > [!NOTE]
    > <span data-ttu-id="eab36-184">Bir üretim ortamında yapılandırıyorsanız, hello en iyi toocreate Google Apps özellikle bu adım için bir yönetici hesabı uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="eab36-184">If you are configuring a production environment, hello best practice is toocreate an admin account in Google Apps specifically for this step.</span></span> <span data-ttu-id="eab36-185">Bu hesapları hello gerekli API ayrıcalıklara sahip bir yönetici rolü kendisiyle ilişkilendirilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eab36-185">These accounts must have an admin role associated with it that has hello necessary API privileges.</span></span>
     
8. <span data-ttu-id="eab36-186">Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="eab36-186">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

9. <span data-ttu-id="eab36-187">Çoklu oturum açma için zaten Google Apps yapılandırdıysanız, Google hello arama alanı kullanarak uygulamaları Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="eab36-187">If you have already configured Google Apps for single sign-on, search for your instance of Google Apps using hello search field.</span></span> <span data-ttu-id="eab36-188">Aksi takdirde seçin **Ekle** arayın ve **Google Apps** hello uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="eab36-188">Otherwise, select **Add** and search for **Google Apps** in hello application gallery.</span></span> <span data-ttu-id="eab36-189">Google Apps hello Arama sonuçlarından seçin ve uygulamaların tooyour listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="eab36-189">Select Google Apps from hello search results, and add it tooyour list of applications.</span></span>

10. <span data-ttu-id="eab36-190">Google Apps örneğiniz seçin ve ardından hello **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="eab36-190">Select your instance of Google Apps, then select hello **Provisioning** tab.</span></span>

11. <span data-ttu-id="eab36-191">Set hello **sağlama modu** çok**otomatik**.</span><span class="sxs-lookup"><span data-stu-id="eab36-191">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

     ![Sağlama](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. <span data-ttu-id="eab36-193">Merhaba altında **yönetici kimlik bilgileri** 'yi tıklatın **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="eab36-193">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="eab36-194">Yeni bir tarayıcı penceresinde bir Google Apps yetkilendirme iletişim kutusunu açar.</span><span class="sxs-lookup"><span data-stu-id="eab36-194">It opens a Google Apps authorization dialog in a new browser window.</span></span>

13. <span data-ttu-id="eab36-195">Toogive Azure Active Directory izin toomake değişiklikleri tooyour Google Apps Kiracı istediğinizi onaylayın.</span><span class="sxs-lookup"><span data-stu-id="eab36-195">Confirm that you would like toogive Azure Active Directory permission toomake changes tooyour Google Apps tenant.</span></span> <span data-ttu-id="eab36-196">Tıklatın **kabul**.</span><span class="sxs-lookup"><span data-stu-id="eab36-196">Click **Accept**.</span></span>
    
     ![İzinleri doğrulayın.][28]

14. <span data-ttu-id="eab36-198">Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour Google Apps uygulama bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="eab36-198">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Google Apps app.</span></span> <span data-ttu-id="eab36-199">Merhaba bağlantı başarısız olursa, Google Apps hesabınız takım yönetici izinlerine sahip olduğundan emin olun ve hello deneyin **"Yetkilendir"** adım yeniden uygulayın.</span><span class="sxs-lookup"><span data-stu-id="eab36-199">If hello connection fails, ensure your Google Apps account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

15. <span data-ttu-id="eab36-200">Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve hello onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="eab36-200">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

16. <span data-ttu-id="eab36-201">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="eab36-201">Click **Save.**</span></span>

17. <span data-ttu-id="eab36-202">Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooGoogle uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="eab36-202">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooGoogle Apps.**</span></span>

18. <span data-ttu-id="eab36-203">Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooGoogle uygulamaları eşitlenir hello kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="eab36-203">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooGoogle Apps.</span></span> <span data-ttu-id="eab36-204">Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları Google Apps içinde güncelleştirme işlemleri için özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="eab36-204">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Google Apps for update operations.</span></span> <span data-ttu-id="eab36-205">Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.</span><span class="sxs-lookup"><span data-stu-id="eab36-205">Select hello Save button toocommit any changes.</span></span>

19. <span data-ttu-id="eab36-206">tooenable hello Google Apps, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello ayarları bölümünün içinde</span><span class="sxs-lookup"><span data-stu-id="eab36-206">tooenable hello Azure AD provisioning service for Google Apps, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

20. <span data-ttu-id="eab36-207">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="eab36-207">Click **Save.**</span></span>

<span data-ttu-id="eab36-208">Tüm kullanıcıların hello ilk eşitleme başlar ve/veya gruplarının tooGoogle uygulamaları hello kullanıcılar ve Gruplar bölümünde atanmış.</span><span class="sxs-lookup"><span data-stu-id="eab36-208">It starts hello initial synchronization of any users and/or groups assigned tooGoogle Apps in hello Users and Groups section.</span></span> <span data-ttu-id="eab36-209">Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır.</span><span class="sxs-lookup"><span data-stu-id="eab36-209">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="eab36-210">Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve Google Apps uygulamanızdan hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.</span><span class="sxs-lookup"><span data-stu-id="eab36-210">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Google Apps app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eab36-211">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="eab36-211">Additional resources</span></span>

* [<span data-ttu-id="eab36-212">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="eab36-212">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eab36-213">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="eab36-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="eab36-214">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="eab36-214">Configure Single Sign-on</span></span>](active-directory-saas-google-apps-tutorial.md)



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