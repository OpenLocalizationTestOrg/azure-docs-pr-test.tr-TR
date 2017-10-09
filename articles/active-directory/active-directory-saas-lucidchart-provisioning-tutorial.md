---
title: "Öğretici: Azure Active Directory ile otomatik kullanıcı sağlamayı LucidChart yapılandırma | Microsoft Docs"
description: "Nasıl tooLucidChart tooconfigure, Azure Active Directory tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesapları öğrenin."
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
ms.openlocfilehash: d3af45141731215f2edc8942ad21b016468c1e38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-lucidchart-for-automatic-user-provisioning"></a><span data-ttu-id="4c85d-103">Öğretici: LucidChart otomatik kullanıcı sağlamayı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4c85d-103">Tutorial: Configuring LucidChart for Automatic User Provisioning</span></span>


<span data-ttu-id="4c85d-104">Bu öğreticinin Hello hedefi LucidChart ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooLucidChart tooperform gereken adımları hello tooshow ' dir.</span><span class="sxs-lookup"><span data-stu-id="4c85d-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in LucidChart and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooLucidChart.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4c85d-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4c85d-105">Prerequisites</span></span>

<span data-ttu-id="4c85d-106">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="4c85d-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="4c85d-107">Bir Azure Active directory kiracısı</span><span class="sxs-lookup"><span data-stu-id="4c85d-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="4c85d-108">Merhaba LucidChart kiracıyla [Kurumsal planı](https://www.lucidchart.com/user/117598685#/subscriptionLevel) veya daha iyi etkin</span><span class="sxs-lookup"><span data-stu-id="4c85d-108">A LucidChart tenant with hello [Enterprise plan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) or better enabled</span></span> 
*   <span data-ttu-id="4c85d-109">LucidChart yönetici izinlerine sahip bir kullanıcı hesabı</span><span class="sxs-lookup"><span data-stu-id="4c85d-109">A user account in LucidChart with Admin permissions</span></span> 

## <a name="assigning-users-toolucidchart"></a><span data-ttu-id="4c85d-110">Kullanıcıların tooLucidChart atama</span><span class="sxs-lookup"><span data-stu-id="4c85d-110">Assigning users tooLucidChart</span></span>

<span data-ttu-id="4c85d-111">Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır.</span><span class="sxs-lookup"><span data-stu-id="4c85d-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="4c85d-112">Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="4c85d-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="4c85d-113">Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya tooyour LucidChart uygulamasına erişmesi Azure AD temsil hello kullanıcılar gruplarında toodecide gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c85d-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour LucidChart app.</span></span> <span data-ttu-id="4c85d-114">Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour LucidChart uygulama atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4c85d-114">Once decided, you can assign these users tooyour LucidChart app by following hello instructions here:</span></span>

[<span data-ttu-id="4c85d-115">Bir kullanıcı veya grup tooan kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="4c85d-115">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolucidchart"></a><span data-ttu-id="4c85d-116">Kullanıcıların tooLucidChart atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="4c85d-116">Important tips for assigning users tooLucidChart</span></span>

*   <span data-ttu-id="4c85d-117">Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooLucidChart tootest hello atanır.</span><span class="sxs-lookup"><span data-stu-id="4c85d-117">It is recommended that a single Azure AD user is assigned tooLucidChart tootest hello provisioning configuration.</span></span> <span data-ttu-id="4c85d-118">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="4c85d-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="4c85d-119">Bir kullanıcı tooLucidChart atarken ya da hello seçmelisiniz **kullanıcı** rol ya da başka bir geçerli uygulamaya özgü rolü (varsa) hello atama iletişim.</span><span class="sxs-lookup"><span data-stu-id="4c85d-119">When assigning a user tooLucidChart, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="4c85d-120">Merhaba **varsayılan erişim** rol sağlamak için çalışmaz ve bu kullanıcılar atlandı.</span><span class="sxs-lookup"><span data-stu-id="4c85d-120">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toolucidchart"></a><span data-ttu-id="4c85d-121">Kullanıcı tooLucidChart hazırlama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4c85d-121">Configuring user provisioning tooLucidChart</span></span> 

<span data-ttu-id="4c85d-122">Bu bölümde, Azure AD tooLucidChart kullanıcının kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve Azure AD'de kullanıcı ve grup atama göre LucidChart atanan kullanıcı hesaplarında devre dışı bırak .</span><span class="sxs-lookup"><span data-stu-id="4c85d-122">This section guides you through connecting your Azure AD tooLucidChart's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in LucidChart based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="4c85d-123">Sağlanan hello yönergeleri izleyerek LucidChart için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4c85d-123">You may also choose tooenabled SAML-based Single Sign-On for LucidChart, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4c85d-124">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="4c85d-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toolucidchart-in-azure-ad"></a><span data-ttu-id="4c85d-125">Azure AD'de tooLucidChart sağlama otomatik olarak bir kullanıcı hesabı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4c85d-125">Configure automatic user account provisioning tooLucidChart in Azure AD</span></span>


1. <span data-ttu-id="4c85d-126">Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="4c85d-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="4c85d-127">Çoklu oturum açma için zaten LucidChart yapılandırdıysanız, hello arama alanı kullanarak LucidChart Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="4c85d-127">If you have already configured LucidChart for single sign-on, search for your instance of LucidChart using hello search field.</span></span> <span data-ttu-id="4c85d-128">Aksi takdirde seçin **Ekle** arayın ve **LucidChart** hello uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="4c85d-128">Otherwise, select **Add** and search for **LucidChart** in hello application gallery.</span></span> <span data-ttu-id="4c85d-129">Merhaba Arama sonuçlarından LucidChart seçin ve uygulamaların tooyour listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4c85d-129">Select LucidChart from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="4c85d-130">LucidChart örneğiniz seçin ve ardından hello **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="4c85d-130">Select your instance of LucidChart, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="4c85d-131">Set hello **sağlama modu** çok**otomatik**.</span><span class="sxs-lookup"><span data-stu-id="4c85d-131">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![LucidChart sağlama](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart1.png)

5. <span data-ttu-id="4c85d-133">Merhaba altında **yönetici kimlik bilgileri** bölümü, giriş hello **gizli belirteci** LucidChart'ın hesap tarafından oluşturulan (Merhaba belirteci hesabınızın altında bulabilirsiniz: **takım**  >  **Uygulama tümleştirmesi** > **SCIM'yi**).</span><span class="sxs-lookup"><span data-stu-id="4c85d-133">Under hello **Admin Credentials** section, input hello **Secret Token** generated by your LucidChart's account (you can find hello token under your account: **Team** > **App Integration** > **SCIM**).</span></span> 

    ![LucidChart sağlama](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart2.png)

6. <span data-ttu-id="4c85d-135">Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour LucidChart uygulama bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="4c85d-135">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour LucidChart app.</span></span> <span data-ttu-id="4c85d-136">Merhaba bağlantı başarısız olursa LucidChart hesabınız yönetici izinlerine sahip olduğundan emin olun ve 5. adım yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="4c85d-136">If hello connection fails, ensure your LucidChart account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="4c85d-137">Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve onay hello onay kutusu "bir e-posta bildirim gönder bir hata oluştuğunda."</span><span class="sxs-lookup"><span data-stu-id="4c85d-137">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="4c85d-138">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c85d-138">Click **Save**.</span></span> 

9. <span data-ttu-id="4c85d-139">Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooLucidChart**.</span><span class="sxs-lookup"><span data-stu-id="4c85d-139">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooLucidChart**.</span></span>

10. <span data-ttu-id="4c85d-140">Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooLucidChart eşitlenir hello kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="4c85d-140">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooLucidChart.</span></span> <span data-ttu-id="4c85d-141">Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları LucidChart içinde güncelleştirme işlemleri için özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="4c85d-141">hello attributes selected as **Matching** properties are used toomatch hello user accounts in LucidChart for update operations.</span></span> <span data-ttu-id="4c85d-142">Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.</span><span class="sxs-lookup"><span data-stu-id="4c85d-142">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="4c85d-143">tooenable hello LucidChart, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello içinde **ayarları** bölümü</span><span class="sxs-lookup"><span data-stu-id="4c85d-143">tooenable hello Azure AD provisioning service for LucidChart, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="4c85d-144">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c85d-144">Click **Save**.</span></span> 

<span data-ttu-id="4c85d-145">Bu işlem, herhangi bir kullanıcı ve/veya hello kullanıcılar tooLucidChart ve Gruplar bölümü atanan gruplarını hello ilk eşitleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="4c85d-145">This operation starts hello initial synchronization of any users and/or groups assigned tooLucidChart in hello Users and Groups section.</span></span> <span data-ttu-id="4c85d-146">Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır.</span><span class="sxs-lookup"><span data-stu-id="4c85d-146">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="4c85d-147">Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler açıklanmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.</span><span class="sxs-lookup"><span data-stu-id="4c85d-147">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="4c85d-148">Hello Azure AD tooread sağlama nasıl oturum ile ilgili daha fazla bilgi için bkz: [otomatik olarak bir kullanıcı hesabı sağlama raporlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="4c85d-148">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="4c85d-149">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4c85d-149">Additional resources</span></span>

* [<span data-ttu-id="4c85d-150">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="4c85d-150">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="4c85d-151">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="4c85d-151">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="4c85d-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4c85d-152">Next steps</span></span>

* [<span data-ttu-id="4c85d-153">Tooreview nasıl günlüğe yazacağını öğrenin ve etkinlik sağlama raporları alın</span><span class="sxs-lookup"><span data-stu-id="4c85d-153">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
