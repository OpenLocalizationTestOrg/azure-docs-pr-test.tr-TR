---
title: "Öğretici: Azure Active Directory ile otomatik olarak bir kullanıcı sağlamak için GitHub yapılandırma | Microsoft Docs"
description: "Nasıl tooGitHub tooconfigure, Azure Active Directory tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesapları öğrenin."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: c1f0f7a42e4f8a94db3f409cd463e13bb1bc13bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a><span data-ttu-id="43717-103">Öğretici: Otomatik kullanıcı sağlamak için GitHub yapılandırma</span><span class="sxs-lookup"><span data-stu-id="43717-103">Tutorial: Configuring GitHub for Automatic User Provisioning</span></span>


<span data-ttu-id="43717-104">Bu öğreticinin Hello hedefi GitHub ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooGitHub tooperform gereken adımları hello tooshow ' dir.</span><span class="sxs-lookup"><span data-stu-id="43717-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in GitHub and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooGitHub.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="43717-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="43717-105">Prerequisites</span></span>

<span data-ttu-id="43717-106">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="43717-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="43717-107">Bir Azure Active directory kiracısı</span><span class="sxs-lookup"><span data-stu-id="43717-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="43717-108">Merhaba Github kiracıyla [iş planı](https://help.github.com/articles/organization-billing-plans/#business-plan) veya daha iyi etkin</span><span class="sxs-lookup"><span data-stu-id="43717-108">A Github tenant with hello [Business plan](https://help.github.com/articles/organization-billing-plans/#business-plan) or better enabled</span></span> 
*   <span data-ttu-id="43717-109">GitHub yönetici izinlerine sahip bir kullanıcı hesabı</span><span class="sxs-lookup"><span data-stu-id="43717-109">A user account in GitHub with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="43717-110">Merhaba tümleştirme sağlama Azure AD kullanır hello üzerinde [GitHub SCIM'yi API](https://developer.github.com/v3/scim/), kullanılabilir tooGithub takımlar hello iş planı veya daha iyi olduğu.</span><span class="sxs-lookup"><span data-stu-id="43717-110">hello Azure AD provisioning integration relies on hello [GitHub SCIM API](https://developer.github.com/v3/scim/), which is available tooGithub teams on hello Business plan or better.</span></span>

## <a name="assigning-users-toogithub"></a><span data-ttu-id="43717-111">Kullanıcıların tooGitHub atama</span><span class="sxs-lookup"><span data-stu-id="43717-111">Assigning users tooGitHub</span></span>

<span data-ttu-id="43717-112">Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır.</span><span class="sxs-lookup"><span data-stu-id="43717-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="43717-113">Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="43717-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="43717-114">Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya tooyour GitHub uygulamasına erişmesi Azure AD temsil hello kullanıcılar gruplarında toodecide gerekir.</span><span class="sxs-lookup"><span data-stu-id="43717-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour GitHub app.</span></span> <span data-ttu-id="43717-115">Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour GitHub uygulama atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="43717-115">Once decided, you can assign these users tooyour GitHub app by following hello instructions here:</span></span>

[<span data-ttu-id="43717-116">Bir kullanıcı veya grup tooan kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="43717-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toogithub"></a><span data-ttu-id="43717-117">Kullanıcıların tooGitHub atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="43717-117">Important tips for assigning users tooGitHub</span></span>

*   <span data-ttu-id="43717-118">Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooGitHub tootest hello atanır.</span><span class="sxs-lookup"><span data-stu-id="43717-118">It is recommended that a single Azure AD user is assigned tooGitHub tootest hello provisioning configuration.</span></span> <span data-ttu-id="43717-119">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="43717-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="43717-120">Bir kullanıcı tooGitHub atarken ya da hello seçmelisiniz **kullanıcı** rol ya da başka bir geçerli uygulamaya özgü rolü (varsa) hello atama iletişim.</span><span class="sxs-lookup"><span data-stu-id="43717-120">When assigning a user tooGitHub, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="43717-121">Merhaba **varsayılan erişim** rol sağlamak için çalışmaz ve bu kullanıcılar atlandı.</span><span class="sxs-lookup"><span data-stu-id="43717-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toogithub"></a><span data-ttu-id="43717-122">Kullanıcı tooGitHub hazırlama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="43717-122">Configuring user provisioning tooGitHub</span></span> 

<span data-ttu-id="43717-123">Bu bölümde, Azure AD tooGitHub kullanıcının kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve Azure AD'de kullanıcı ve grup atama göre github'da atanan kullanıcı hesapları devre dışı bırak.</span><span class="sxs-lookup"><span data-stu-id="43717-123">This section guides you through connecting your Azure AD tooGitHub's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in GitHub based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="43717-124">Sağlanan hello yönergeleri izleyerek GitHub için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="43717-124">You may also choose tooenabled SAML-based Single Sign-On for GitHub, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="43717-125">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="43717-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toogithub-in-azure-ad"></a><span data-ttu-id="43717-126">Azure AD'de tooGitHub sağlama otomatik olarak bir kullanıcı hesabı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="43717-126">Configure automatic user account provisioning tooGitHub in Azure AD</span></span>


1. <span data-ttu-id="43717-127">Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="43717-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="43717-128">Çoklu oturum açma için GitHub zaten yapılandırdıysanız hello arama alanı kullanarak GitHub Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="43717-128">If you have already configured GitHub for single sign-on, search for your instance of GitHub using hello search field.</span></span> <span data-ttu-id="43717-129">Aksi takdirde seçin **Ekle** arayın ve **GitHub** hello uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="43717-129">Otherwise, select **Add** and search for **GitHub** in hello application gallery.</span></span> <span data-ttu-id="43717-130">GitHub hello Arama sonuçlarından seçin ve uygulamaların tooyour listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="43717-130">Select GitHub from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="43717-131">GitHub örneğiniz seçin ve ardından hello **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="43717-131">Select your instance of GitHub, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="43717-132">Set hello **sağlama modu** çok**otomatik**.</span><span class="sxs-lookup"><span data-stu-id="43717-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![GitHub sağlama](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. <span data-ttu-id="43717-134">Merhaba altında **yönetici kimlik bilgileri** 'yi tıklatın **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="43717-134">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="43717-135">Bu işlem, yeni bir tarayıcı penceresinde bir GitHub yetkilendirme iletişim kutusunu açar.</span><span class="sxs-lookup"><span data-stu-id="43717-135">This operation opens a GitHub authorization dialog in a new browser window.</span></span> 

6. <span data-ttu-id="43717-136">Merhaba yeni pencerede GitHub yönetici hesabınızı kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="43717-136">In hello new window, sign into GitHub using your Admin account.</span></span> <span data-ttu-id="43717-137">Hello elde edilen yetkilendirme iletişim kutusunda, tooenable sağlamayı istiyor ve ardından hello GitHub ekibi seçin **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="43717-137">In hello resulting authorization dialog, select hello GitHub team that you want tooenable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="43717-138">Bir kez tamamlanan, dönüş toohello Azure portal toocomplete hello yapılandırma sağlama.</span><span class="sxs-lookup"><span data-stu-id="43717-138">Once completed, return toohello Azure portal toocomplete hello provisioning configuration.</span></span>

    ![Yetkilendirme iletişim](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. <span data-ttu-id="43717-140">Hello Azure portal, giriş **Kiracı URL** tıklatıp **Bağlantıyı Sına** tooensure Azure AD tooyour GitHub uygulama bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="43717-140">In hello Azure portal, input **Tenant URL** and click **Test Connection** tooensure Azure AD can connect tooyour GitHub app.</span></span> <span data-ttu-id="43717-141">Merhaba bağlantı başarısız olursa, GitHub hesabınızda yönetici izinleri olduğundan emin olun ve **Kiracı URl** doğru girilen sonra hello "Yetkilendir" adımı yeniden deneyin (size oluşturabilecek **Kiracı URL** kuralı tarafından: "https : //api.github.com/scim/v2/organizations/ + < Organizations_name > ", kuruluşlar, GitHub hesabınızda altında bulabilirsiniz: **ayarları** > **kuruluşların**).</span><span class="sxs-lookup"><span data-stu-id="43717-141">If hello connection fails, ensure your GitHub account has Admin permissions and **Tenant URl** is inputted correctly, then try hello "Authorize" step again (you can constitute **Tenant URL** by rule: "https://api.github.com/scim/v2/organizations/ + <Organizations_name>", you can find your organizations under your GitHub account: **Settings** > **Organizations**).</span></span>

    ![Yetkilendirme iletişim](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. <span data-ttu-id="43717-143">Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve onay hello onay kutusu "bir e-posta bildirim gönder bir hata oluştuğunda."</span><span class="sxs-lookup"><span data-stu-id="43717-143">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

9. <span data-ttu-id="43717-144">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="43717-144">Click **Save**.</span></span> 

10. <span data-ttu-id="43717-145">Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooGitHub**.</span><span class="sxs-lookup"><span data-stu-id="43717-145">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooGitHub**.</span></span>

11. <span data-ttu-id="43717-146">Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooGitHub eşitlenir hello kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="43717-146">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooGitHub.</span></span> <span data-ttu-id="43717-147">Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları github'da güncelleştirme işlemleri için özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="43717-147">hello attributes selected as **Matching** properties are used toomatch hello user accounts in GitHub for update operations.</span></span> <span data-ttu-id="43717-148">Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.</span><span class="sxs-lookup"><span data-stu-id="43717-148">Select hello Save button toocommit any changes.</span></span>

12. <span data-ttu-id="43717-149">tooenable hello GitHub, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello içinde **ayarları** bölümü</span><span class="sxs-lookup"><span data-stu-id="43717-149">tooenable hello Azure AD provisioning service for GitHub, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

13. <span data-ttu-id="43717-150">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="43717-150">Click **Save**.</span></span> 

<span data-ttu-id="43717-151">Bu işlem, herhangi bir kullanıcı ve/veya hello kullanıcılar tooGitHub ve Gruplar bölümü atanan gruplarını hello ilk eşitleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="43717-151">This operation starts hello initial synchronization of any users and/or groups assigned tooGitHub in hello Users and Groups section.</span></span> <span data-ttu-id="43717-152">Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır.</span><span class="sxs-lookup"><span data-stu-id="43717-152">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="43717-153">Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler açıklanmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.</span><span class="sxs-lookup"><span data-stu-id="43717-153">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="43717-154">Hello Azure AD tooread sağlama nasıl oturum ile ilgili daha fazla bilgi için bkz: [otomatik olarak bir kullanıcı hesabı sağlama raporlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="43717-154">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="43717-155">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="43717-155">Additional resources</span></span>

* [<span data-ttu-id="43717-156">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="43717-156">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="43717-157">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="43717-157">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="43717-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="43717-158">Next steps</span></span>

* [<span data-ttu-id="43717-159">Tooreview nasıl günlüğe yazacağını öğrenin ve etkinlik sağlama raporları alın</span><span class="sxs-lookup"><span data-stu-id="43717-159">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
