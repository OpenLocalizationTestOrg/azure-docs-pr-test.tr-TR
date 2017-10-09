---
title: "Öğretici: Azure Active Directory ile otomatik kullanıcı sağlamayı Samanage yapılandırma | Microsoft Docs"
description: "Nasıl tooSamanage tooconfigure, Azure Active Directory tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesapları öğrenin."
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
ms.openlocfilehash: 6cb36d2cc6ce33da4f8ebba65d138bfd4f2aca9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-samanage-for-automatic-user-provisioning"></a><span data-ttu-id="05cc0-103">Öğretici: Samanage otomatik kullanıcı sağlamayı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="05cc0-103">Tutorial: Configuring Samanage for Automatic User Provisioning</span></span>


<span data-ttu-id="05cc0-104">Bu öğreticinin Hello hedefi Samanage ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooSamanage tooperform gereken adımları hello tooshow ' dir.</span><span class="sxs-lookup"><span data-stu-id="05cc0-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Samanage and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSamanage.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="05cc0-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="05cc0-105">Prerequisites</span></span>

<span data-ttu-id="05cc0-106">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="05cc0-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="05cc0-107">Bir Azure Active directory kiracısı</span><span class="sxs-lookup"><span data-stu-id="05cc0-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="05cc0-108">Merhaba Samanage kiracıyla [profesyonel planı](https://www.samanage.com/pricing/) veya daha iyi etkin</span><span class="sxs-lookup"><span data-stu-id="05cc0-108">A Samanage tenant with hello [Professional plan](https://www.samanage.com/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="05cc0-109">Samanage yönetici izinlerine sahip bir kullanıcı hesabı</span><span class="sxs-lookup"><span data-stu-id="05cc0-109">A user account in Samanage with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="05cc0-110">Merhaba tümleştirme sağlama Azure AD kullanır hello üzerinde [Samanage REST API](https://www.samanage.com/api/), kullanılabilir tooSamanage takımlar hello Professional üzerinde olduğu planlayabilir ya da daha iyi.</span><span class="sxs-lookup"><span data-stu-id="05cc0-110">hello Azure AD provisioning integration relies on hello [Samanage REST API](https://www.samanage.com/api/), which is available tooSamanage teams on hello Professional plan or better.</span></span>

## <a name="assigning-users-toosamanage"></a><span data-ttu-id="05cc0-111">Kullanıcıların tooSamanage atama</span><span class="sxs-lookup"><span data-stu-id="05cc0-111">Assigning users tooSamanage</span></span>

<span data-ttu-id="05cc0-112">Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır.</span><span class="sxs-lookup"><span data-stu-id="05cc0-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="05cc0-113">Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="05cc0-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="05cc0-114">Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya tooyour Samanage uygulamasına erişmesi Azure AD temsil hello kullanıcılar gruplarında toodecide gerekir.</span><span class="sxs-lookup"><span data-stu-id="05cc0-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Samanage app.</span></span> <span data-ttu-id="05cc0-115">Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour Samanage uygulama atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="05cc0-115">Once decided, you can assign these users tooyour Samanage app by following hello instructions here:</span></span>

[<span data-ttu-id="05cc0-116">Bir kullanıcı veya grup tooan kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="05cc0-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toosamanage"></a><span data-ttu-id="05cc0-117">Kullanıcıların tooSamanage atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="05cc0-117">Important tips for assigning users tooSamanage</span></span>

*   <span data-ttu-id="05cc0-118">Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooSamanage tootest hello atanır.</span><span class="sxs-lookup"><span data-stu-id="05cc0-118">It is recommended that a single Azure AD user is assigned tooSamanage tootest hello provisioning configuration.</span></span> <span data-ttu-id="05cc0-119">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="05cc0-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="05cc0-120">Bir kullanıcı tooSamanage atarken ya da hello seçmelisiniz **kullanıcı** rol ya da başka bir geçerli uygulamaya özgü rolü (varsa) hello atama iletişim.</span><span class="sxs-lookup"><span data-stu-id="05cc0-120">When assigning a user tooSamanage, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="05cc0-121">Merhaba **varsayılan erişim** rol sağlamak için çalışmaz ve bu kullanıcılar atlandı.</span><span class="sxs-lookup"><span data-stu-id="05cc0-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="05cc0-122">Eklenen bir özellik olarak hizmet sağlama hello Samanage içinde tanımlanan herhangi bir özel rolü okur ve bunları Azure AD hello rolü Seç iletişim kutusunda bunlar burada seçilebilir aktarır.</span><span class="sxs-lookup"><span data-stu-id="05cc0-122">As an added feature, hello provisioning service reads any custom roles defined in Samanage, and imports them into Azure AD where they can be selected in hello Select Role dialog.</span></span> <span data-ttu-id="05cc0-123">Bu rolleri hizmet sağlama hello etkinleştirilir ve bir eşitleme döngüsü tamamlandıktan sonra hello Azure portalında görünür.</span><span class="sxs-lookup"><span data-stu-id="05cc0-123">These roles will be visible in hello Azure portal after hello provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-toosamanage"></a><span data-ttu-id="05cc0-124">Kullanıcı tooSamanage hazırlama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="05cc0-124">Configuring user provisioning tooSamanage</span></span> 

<span data-ttu-id="05cc0-125">Bu bölümde, Azure AD tooSamanage kullanıcının kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve Azure AD'de kullanıcı ve grup atama göre Samanage atanan kullanıcı hesaplarında devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="05cc0-125">This section guides you through connecting your Azure AD tooSamanage's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Samanage based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="05cc0-126">Sağlanan hello yönergeleri izleyerek Samanage için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="05cc0-126">You may also choose tooenabled SAML-based Single Sign-On for Samanage, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="05cc0-127">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="05cc0-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toosamanage-in-azure-ad"></a><span data-ttu-id="05cc0-128">Azure AD'de tooSamanage sağlama otomatik olarak bir kullanıcı hesabı yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="05cc0-128">Configure automatic user account provisioning tooSamanage in Azure AD:</span></span>


1. <span data-ttu-id="05cc0-129">Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="05cc0-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="05cc0-130">Çoklu oturum açma için zaten Samanage yapılandırdıysanız, hello arama alanı kullanarak Samanage Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="05cc0-130">If you have already configured Samanage for single sign-on, search for your instance of Samanage using hello search field.</span></span> <span data-ttu-id="05cc0-131">Aksi takdirde seçin **Ekle** arayın ve **Samanage** hello uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="05cc0-131">Otherwise, select **Add** and search for **Samanage** in hello application gallery.</span></span> <span data-ttu-id="05cc0-132">Merhaba Arama sonuçlarından Samanage seçin ve uygulamaların tooyour listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="05cc0-132">Select Samanage from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="05cc0-133">Samanage örneğiniz seçin ve ardından hello **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="05cc0-133">Select your instance of Samanage, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="05cc0-134">Set hello **sağlama modu** çok**otomatik**.</span><span class="sxs-lookup"><span data-stu-id="05cc0-134">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Samanage sağlama](./media/active-directory-saas-samanage-provisioning-tutorial/Samanage1.png)

5. <span data-ttu-id="05cc0-136">Merhaba altında **yönetici kimlik bilgileri** bölümü, giriş hello **yönetici kullanıcı adı ve yönetici parolası** Samanage'nın hesap.</span><span class="sxs-lookup"><span data-stu-id="05cc0-136">Under hello **Admin Credentials** section, input hello **Admin Username&Admin Password** of your Samanage's account.</span></span> 

6. <span data-ttu-id="05cc0-137">Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour Samanage uygulama bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="05cc0-137">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Samanage app.</span></span> <span data-ttu-id="05cc0-138">Merhaba bağlantı başarısız olursa Samanage hesabınız yönetici izinlerine sahip olduğundan emin olun ve 5. adım yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="05cc0-138">If hello connection fails, ensure your Samanage account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="05cc0-139">Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve onay hello onay kutusu "bir e-posta bildirim gönder bir hata oluştuğunda."</span><span class="sxs-lookup"><span data-stu-id="05cc0-139">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="05cc0-140">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="05cc0-140">Click **Save**.</span></span> 

9. <span data-ttu-id="05cc0-141">Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooSamanage**.</span><span class="sxs-lookup"><span data-stu-id="05cc0-141">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSamanage**.</span></span>

10. <span data-ttu-id="05cc0-142">Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooSamanage eşitlenir hello kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="05cc0-142">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooSamanage.</span></span> <span data-ttu-id="05cc0-143">Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları Samanage içinde güncelleştirme işlemleri için özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="05cc0-143">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Samanage for update operations.</span></span> <span data-ttu-id="05cc0-144">Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.</span><span class="sxs-lookup"><span data-stu-id="05cc0-144">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="05cc0-145">tooenable hello Samanage, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello içinde **ayarları** bölümü</span><span class="sxs-lookup"><span data-stu-id="05cc0-145">tooenable hello Azure AD provisioning service for Samanage, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="05cc0-146">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="05cc0-146">Click **Save**.</span></span> 

<span data-ttu-id="05cc0-147">Bu işlem, herhangi bir kullanıcı ve/veya hello kullanıcılar tooSamanage ve Gruplar bölümü atanan gruplarını hello ilk eşitleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="05cc0-147">This operation starts hello initial synchronization of any users and/or groups assigned tooSamanage in hello Users and Groups section.</span></span> <span data-ttu-id="05cc0-148">Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır.</span><span class="sxs-lookup"><span data-stu-id="05cc0-148">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="05cc0-149">Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler açıklanmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.</span><span class="sxs-lookup"><span data-stu-id="05cc0-149">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="05cc0-150">Hello Azure AD tooread sağlama nasıl oturum ile ilgili daha fazla bilgi için bkz: [otomatik olarak bir kullanıcı hesabı sağlama raporlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="05cc0-150">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="05cc0-151">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="05cc0-151">Additional resources</span></span>

* [<span data-ttu-id="05cc0-152">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="05cc0-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="05cc0-153">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="05cc0-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="05cc0-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="05cc0-154">Next steps</span></span>

* [<span data-ttu-id="05cc0-155">Tooreview nasıl günlüğe yazacağını öğrenin ve etkinlik sağlama raporları alın</span><span class="sxs-lookup"><span data-stu-id="05cc0-155">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
