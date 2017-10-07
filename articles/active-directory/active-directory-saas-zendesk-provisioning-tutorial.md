---
title: "Öğretici: Azure Active Directory ile otomatik kullanıcı sağlamayı ZenDesk yapılandırma | Microsoft Docs"
description: "Nasıl tooZenDesk tooconfigure, Azure Active Directory tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesapları öğrenin."
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
ms.openlocfilehash: 200e8790ec1755f5cf927274ceb38527dd993f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-zendesk-for-automatic-user-provisioning"></a><span data-ttu-id="01e96-103">Öğretici: ZenDesk otomatik kullanıcı sağlamayı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="01e96-103">Tutorial: Configuring ZenDesk for Automatic User Provisioning</span></span>


<span data-ttu-id="01e96-104">Bu öğreticinin Hello hedefi ZenDesk ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooZenDesk tooperform gereken adımları hello tooshow ' dir.</span><span class="sxs-lookup"><span data-stu-id="01e96-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in ZenDesk and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooZenDesk.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="01e96-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="01e96-105">Prerequisites</span></span>

<span data-ttu-id="01e96-106">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="01e96-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="01e96-107">Bir Azure Active directory kiracısı</span><span class="sxs-lookup"><span data-stu-id="01e96-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="01e96-108">ZenDesk Kiracı hello ile [Kurumsal planı](https://www.zendesk.com/product/pricing/) veya daha iyi etkin</span><span class="sxs-lookup"><span data-stu-id="01e96-108">A ZenDesk tenant with hello [Enterprise plan](https://www.zendesk.com/product/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="01e96-109">ZenDesk yönetici izinlerine sahip bir kullanıcı hesabı</span><span class="sxs-lookup"><span data-stu-id="01e96-109">A user account in ZenDesk with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="01e96-110">Merhaba tümleştirme sağlama Azure AD kullanır hello üzerinde [ZenDesk REST API](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), kullanılabilir tooZenDesk takımlar hello temel plan üzerinde ya da daha iyi olduğu.</span><span class="sxs-lookup"><span data-stu-id="01e96-110">hello Azure AD provisioning integration relies on hello [ZenDesk REST API](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), which is available tooZenDesk teams on hello Essential plan or better.</span></span>

## <a name="assigning-users-toozendesk"></a><span data-ttu-id="01e96-111">Kullanıcıların tooZenDesk atama</span><span class="sxs-lookup"><span data-stu-id="01e96-111">Assigning users tooZenDesk</span></span>

<span data-ttu-id="01e96-112">Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır.</span><span class="sxs-lookup"><span data-stu-id="01e96-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="01e96-113">Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="01e96-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="01e96-114">Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya tooyour ZenDesk uygulamasına erişmesi Azure AD temsil hello kullanıcılar gruplarında toodecide gerekir.</span><span class="sxs-lookup"><span data-stu-id="01e96-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour ZenDesk app.</span></span> <span data-ttu-id="01e96-115">Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour ZenDesk uygulama atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="01e96-115">Once decided, you can assign these users tooyour ZenDesk app by following hello instructions here:</span></span>

[<span data-ttu-id="01e96-116">Bir kullanıcı veya grup tooan kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="01e96-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toozendesk"></a><span data-ttu-id="01e96-117">Kullanıcıların tooZenDesk atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="01e96-117">Important tips for assigning users tooZenDesk</span></span>

*   <span data-ttu-id="01e96-118">Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooZenDesk tootest hello atanır.</span><span class="sxs-lookup"><span data-stu-id="01e96-118">It is recommended that a single Azure AD user is assigned tooZenDesk tootest hello provisioning configuration.</span></span> <span data-ttu-id="01e96-119">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="01e96-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="01e96-120">Bir kullanıcı tooZenDesk atarken ya da hello seçmelisiniz **kullanıcı** rol ya da başka bir geçerli uygulamaya özgü rolü (varsa) hello atama iletişim.</span><span class="sxs-lookup"><span data-stu-id="01e96-120">When assigning a user tooZenDesk, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="01e96-121">Merhaba **varsayılan erişim** rol sağlamak için çalışmaz ve bu kullanıcılar atlandı.</span><span class="sxs-lookup"><span data-stu-id="01e96-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="01e96-122">Eklenen bir özellik olarak hizmet sağlama hello Zendesk içinde tanımlanan herhangi bir özel rolü okur ve bunları Azure AD hello rolü Seç iletişim kutusunda bunlar burada seçilebilir aktarır.</span><span class="sxs-lookup"><span data-stu-id="01e96-122">As an added feature, hello provisioning service reads any custom roles defined in Zendesk, and imports them into Azure AD where they can be selected in hello Select Role dialog.</span></span> <span data-ttu-id="01e96-123">Bu rolleri hizmet sağlama hello etkinleştirilir ve bir eşitleme döngüsü tamamlandıktan sonra hello Azure portalında görünür.</span><span class="sxs-lookup"><span data-stu-id="01e96-123">These roles will be visible in hello Azure portal after hello provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-toozendesk"></a><span data-ttu-id="01e96-124">Kullanıcı tooZenDesk hazırlama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="01e96-124">Configuring user provisioning tooZenDesk</span></span> 

<span data-ttu-id="01e96-125">Bu bölümde, Azure AD tooZenDesk kullanıcının kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve Azure AD'de kullanıcı ve grup atama göre ZenDesk atanan kullanıcı hesaplarında devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="01e96-125">This section guides you through connecting your Azure AD tooZenDesk's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in ZenDesk based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="01e96-126">Sağlanan hello yönergeleri izleyerek ZenDesk için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="01e96-126">You may also choose tooenabled SAML-based Single Sign-On for ZenDesk, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="01e96-127">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="01e96-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toozendesk-in-azure-ad"></a><span data-ttu-id="01e96-128">Azure AD'de tooZenDesk sağlama otomatik olarak bir kullanıcı hesabı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="01e96-128">Configure automatic user account provisioning tooZenDesk in Azure AD</span></span>


1. <span data-ttu-id="01e96-129">Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="01e96-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="01e96-130">Çoklu oturum açma için zaten ZenDesk yapılandırdıysanız, hello arama alanı kullanarak ZenDesk Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="01e96-130">If you have already configured ZenDesk for single sign-on, search for your instance of ZenDesk using hello search field.</span></span> <span data-ttu-id="01e96-131">Aksi takdirde seçin **Ekle** arayın ve **ZenDesk** hello uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="01e96-131">Otherwise, select **Add** and search for **ZenDesk** in hello application gallery.</span></span> <span data-ttu-id="01e96-132">ZenDesk hello Arama sonuçlarından seçin ve uygulamaların tooyour listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="01e96-132">Select ZenDesk from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="01e96-133">ZenDesk örneğiniz seçin ve ardından hello **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="01e96-133">Select your instance of ZenDesk, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="01e96-134">Set hello **sağlama modu** çok**otomatik**.</span><span class="sxs-lookup"><span data-stu-id="01e96-134">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![ZenDesk sağlama](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk1.png)

5. <span data-ttu-id="01e96-136">Merhaba altında **yönetici kimlik bilgileri** bölümü, giriş hello **yönetici kullanıcı adı, tokenkey & etki alanı** ZenDesk'ın hesap tarafından oluşturulan (Merhaba belirteci hesabınızın altında bulabilirsiniz: **yönetici**   >  **API** > **ayarları**).</span><span class="sxs-lookup"><span data-stu-id="01e96-136">Under hello **Admin Credentials** section, input hello **Admin Username&tokenkey&Domain** generated by your ZenDesk's account (you can find hello token under your account: **Admin** > **API** > **Settings**).</span></span> 

    ![ZenDesk sağlama](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk2.png)

6. <span data-ttu-id="01e96-138">Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour ZenDesk uygulama bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="01e96-138">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour ZenDesk app.</span></span> <span data-ttu-id="01e96-139">Merhaba bağlantı başarısız olursa ZenDesk hesabınıza yönetici izinlerine sahip olduğundan emin olun ve 5. adım yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="01e96-139">If hello connection fails, ensure your ZenDesk account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="01e96-140">Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve onay hello onay kutusu "bir e-posta bildirim gönder bir hata oluştuğunda."</span><span class="sxs-lookup"><span data-stu-id="01e96-140">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="01e96-141">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01e96-141">Click **Save**.</span></span> 

9. <span data-ttu-id="01e96-142">Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooZenDesk**.</span><span class="sxs-lookup"><span data-stu-id="01e96-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooZenDesk**.</span></span>

10. <span data-ttu-id="01e96-143">Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooZenDesk eşitlenir hello kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="01e96-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooZenDesk.</span></span> <span data-ttu-id="01e96-144">Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları ZenDesk içinde güncelleştirme işlemleri için özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="01e96-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in ZenDesk for update operations.</span></span> <span data-ttu-id="01e96-145">Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.</span><span class="sxs-lookup"><span data-stu-id="01e96-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="01e96-146">tooenable hello ZenDesk, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello içinde **ayarları** bölümü</span><span class="sxs-lookup"><span data-stu-id="01e96-146">tooenable hello Azure AD provisioning service for ZenDesk, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="01e96-147">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01e96-147">Click **Save**.</span></span> 

<span data-ttu-id="01e96-148">Bu işlem, herhangi bir kullanıcı ve/veya hello kullanıcılar tooZenDesk ve Gruplar bölümü atanan gruplarını hello ilk eşitleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="01e96-148">This operation starts hello initial synchronization of any users and/or groups assigned tooZenDesk in hello Users and Groups section.</span></span> <span data-ttu-id="01e96-149">Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır.</span><span class="sxs-lookup"><span data-stu-id="01e96-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="01e96-150">Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler açıklanmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.</span><span class="sxs-lookup"><span data-stu-id="01e96-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="01e96-151">Hello Azure AD tooread sağlama nasıl oturum ile ilgili daha fazla bilgi için bkz: [otomatik olarak bir kullanıcı hesabı sağlama raporlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="01e96-151">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="01e96-152">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="01e96-152">Additional resources</span></span>

* [<span data-ttu-id="01e96-153">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="01e96-153">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="01e96-154">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="01e96-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="01e96-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="01e96-155">Next steps</span></span>

* [<span data-ttu-id="01e96-156">Tooreview nasıl günlüğe yazacağını öğrenin ve etkinlik sağlama raporları alın</span><span class="sxs-lookup"><span data-stu-id="01e96-156">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
