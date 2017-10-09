---
title: "Öğretici: Azure Active Directory Tümleştirme ile Jive | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Jive arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: b1c0d0bc2d79427c055f577fe5f9d30d10f1bbdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a><span data-ttu-id="e70c7-103">Öğretici: Jive kullanıcı sağlamak için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e70c7-103">Tutorial: Configuring Jive for User Provisioning</span></span>

<span data-ttu-id="e70c7-104">Bu öğreticinin Hello hedefi Jive ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooJive tooperform gereken adımları hello tooshow ' dir.</span><span class="sxs-lookup"><span data-stu-id="e70c7-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Jive and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooJive.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e70c7-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e70c7-105">Prerequisites</span></span>

<span data-ttu-id="e70c7-106">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="e70c7-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="e70c7-107">Bir Azure Active directory kiracısı.</span><span class="sxs-lookup"><span data-stu-id="e70c7-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="e70c7-108">Bir Jive çoklu oturum açma etkin abonelik.</span><span class="sxs-lookup"><span data-stu-id="e70c7-108">A Jive single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="e70c7-109">Bir kullanıcı hesabında Jive takım yönetici izinlerine sahip.</span><span class="sxs-lookup"><span data-stu-id="e70c7-109">A user account in Jive with Team Admin permissions.</span></span>

## <a name="assigning-users-toojive"></a><span data-ttu-id="e70c7-110">Kullanıcıların tooJive atama</span><span class="sxs-lookup"><span data-stu-id="e70c7-110">Assigning users tooJive</span></span>

<span data-ttu-id="e70c7-111">Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır.</span><span class="sxs-lookup"><span data-stu-id="e70c7-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="e70c7-112">Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="e70c7-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="e70c7-113">Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD tooyour Jive uygulamasına erişmesi hello kullanıcıları temsil gruplarında toodecide gerekir.</span><span class="sxs-lookup"><span data-stu-id="e70c7-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Jive app.</span></span> <span data-ttu-id="e70c7-114">Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour Jive uygulama atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e70c7-114">Once decided, you can assign these users tooyour Jive app by following hello instructions here:</span></span>

[<span data-ttu-id="e70c7-115">Bir kullanıcı veya grup tooan kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="e70c7-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toojive"></a><span data-ttu-id="e70c7-116">Kullanıcıların tooJive atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="e70c7-116">Important tips for assigning users tooJive</span></span>

*   <span data-ttu-id="e70c7-117">Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooJive tootest hello atanabilir.</span><span class="sxs-lookup"><span data-stu-id="e70c7-117">It is recommended that a single Azure AD user be assigned tooJive tootest hello provisioning configuration.</span></span> <span data-ttu-id="e70c7-118">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="e70c7-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="e70c7-119">Bir kullanıcı tooJive atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e70c7-119">When assigning a user tooJive, you must select a valid user role.</span></span> <span data-ttu-id="e70c7-120">Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="e70c7-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="e70c7-121">Kullanıcı sağlamayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="e70c7-121">Enable User Provisioning</span></span>

<span data-ttu-id="e70c7-122">Bu bölümde, Azure AD tooJive kullanıcının kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve Azure AD'de kullanıcı ve grup atama göre Jive atanan kullanıcı hesaplarında devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="e70c7-122">This section guides you through connecting your Azure AD tooJive's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Jive based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="e70c7-123">SAML tabanlı tek oturum açma için sağlanan hello yönergeleri izleyerek Jive tooenabled tercih edebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e70c7-123">You may also choose tooenabled SAML-based Single Sign-On for Jive, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e70c7-124">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="e70c7-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="e70c7-125">tooconfigure kullanıcı hesabı sağlama:</span><span class="sxs-lookup"><span data-stu-id="e70c7-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="e70c7-126">Bu bölümde Hello amacı olan toooutline tooJive tooenable Active Directory kullanıcısı kullanıcı sağlamayı nasıl hesapları.</span><span class="sxs-lookup"><span data-stu-id="e70c7-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooJive.</span></span>
<span data-ttu-id="e70c7-127">Bu yordam bir parçası, gerekli tooprovide toorequest Jive.com gelen gereken kullanıcı güvenlik belirteci olur.</span><span class="sxs-lookup"><span data-stu-id="e70c7-127">As part of this procedure, you are required tooprovide a user security token you need toorequest from Jive.com.</span></span>

1. <span data-ttu-id="e70c7-128">Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="e70c7-128">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="e70c7-129">Çoklu oturum açma için zaten Jive yapılandırdıysanız, hello arama alanı kullanarak Jive Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="e70c7-129">If you have already configured Jive for single sign-on, search for your instance of Jive using hello search field.</span></span> <span data-ttu-id="e70c7-130">Aksi takdirde seçin **Ekle** arayın ve **Jive** hello uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="e70c7-130">Otherwise, select **Add** and search for **Jive** in hello application gallery.</span></span> <span data-ttu-id="e70c7-131">Merhaba Arama sonuçlarından Jive seçin ve uygulamaların tooyour listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e70c7-131">Select Jive from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="e70c7-132">Jive örneğiniz seçin ve ardından hello **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="e70c7-132">Select your instance of Jive, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="e70c7-133">Set hello **sağlama modu** çok**otomatik**.</span><span class="sxs-lookup"><span data-stu-id="e70c7-133">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Sağlama](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="e70c7-135">Merhaba altında **yönetici kimlik bilgileri** bölümünde, yapılandırma ayarlarını aşağıdaki hello sağlayın:</span><span class="sxs-lookup"><span data-stu-id="e70c7-135">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="e70c7-136">a.</span><span class="sxs-lookup"><span data-stu-id="e70c7-136">a.</span></span> <span data-ttu-id="e70c7-137">Merhaba, **Jive yönetici kullanıcı adı** metin kutusuna, bir Jive hesap hello sahip adı türü **Sistem Yöneticisi** atanan Jive.com profilinde.</span><span class="sxs-lookup"><span data-stu-id="e70c7-137">In hello **Jive Admin User Name** textbox, type a Jive account name that has hello **System Administrator** profile in Jive.com assigned.</span></span>
   
    <span data-ttu-id="e70c7-138">b.</span><span class="sxs-lookup"><span data-stu-id="e70c7-138">b.</span></span> <span data-ttu-id="e70c7-139">Merhaba, **Jive yönetici parolası** metin kutusuna, bu hesap için hello parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="e70c7-139">In hello **Jive Admin Password** textbox, type hello password for this account.</span></span>
   
    <span data-ttu-id="e70c7-140">c.</span><span class="sxs-lookup"><span data-stu-id="e70c7-140">c.</span></span> <span data-ttu-id="e70c7-141">Merhaba, **Jive Kiracı URL** metin kutusuna, türü hello Jive Kiracı URL.</span><span class="sxs-lookup"><span data-stu-id="e70c7-141">In hello **Jive Tenant URL** textbox, type hello Jive tenant URL.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="e70c7-142">Merhaba Jive Kiracı tooJive içinde kuruluş toolog tarafından kullanılan URL'dir.</span><span class="sxs-lookup"><span data-stu-id="e70c7-142">hello Jive tenant URL is URL that is used by your organization toolog in tooJive.</span></span>  
      > <span data-ttu-id="e70c7-143">Genellikle, hello URL biçimi aşağıdaki hello sahiptir: **www.\< Kuruluş\>. jive.com**.</span><span class="sxs-lookup"><span data-stu-id="e70c7-143">Typically, hello URL has hello following format: **www.\<organization\>.jive.com**.</span></span>          

6. <span data-ttu-id="e70c7-144">Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour Jive uygulama bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="e70c7-144">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Jive app.</span></span>

7. <span data-ttu-id="e70c7-145">Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve aşağıdaki hello onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="e70c7-145">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

8. <span data-ttu-id="e70c7-146">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="e70c7-146">Click **Save.**</span></span>

9. <span data-ttu-id="e70c7-147">Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooJive.**</span><span class="sxs-lookup"><span data-stu-id="e70c7-147">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooJive.**</span></span>

10. <span data-ttu-id="e70c7-148">Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooJive eşitlenir hello kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="e70c7-148">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooJive.</span></span> <span data-ttu-id="e70c7-149">Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları Jive içinde güncelleştirme işlemleri için özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="e70c7-149">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Jive for update operations.</span></span> <span data-ttu-id="e70c7-150">Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.</span><span class="sxs-lookup"><span data-stu-id="e70c7-150">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="e70c7-151">tooenable hello Jive, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello ayarları bölümünün içinde</span><span class="sxs-lookup"><span data-stu-id="e70c7-151">tooenable hello Azure AD provisioning service for Jive, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="e70c7-152">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="e70c7-152">Click **Save.**</span></span>

<span data-ttu-id="e70c7-153">Herhangi bir kullanıcı ve/veya hello kullanıcılar tooJive ve Gruplar bölümü atanan gruplarını hello ilk eşitleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="e70c7-153">It starts hello initial synchronization of any users and/or groups assigned tooJive in hello Users and Groups section.</span></span> <span data-ttu-id="e70c7-154">Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır.</span><span class="sxs-lookup"><span data-stu-id="e70c7-154">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="e70c7-155">Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve hizmet Jive uygulamanızdan sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.</span><span class="sxs-lookup"><span data-stu-id="e70c7-155">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Jive app.</span></span>

<span data-ttu-id="e70c7-156">Şimdi sınama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e70c7-156">You can now create a test account.</span></span> <span data-ttu-id="e70c7-157">TooJive hello hesap tooverify eşitlenmiş too20 dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="e70c7-157">Wait for up too20 minutes tooverify that hello account has been synchronized tooJive.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e70c7-158">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e70c7-158">Additional resources</span></span>

* [<span data-ttu-id="e70c7-159">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="e70c7-159">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e70c7-160">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e70c7-160">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="e70c7-161">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e70c7-161">Configure Single Sign-on</span></span>](active-directory-saas-jive-tutorial.md)