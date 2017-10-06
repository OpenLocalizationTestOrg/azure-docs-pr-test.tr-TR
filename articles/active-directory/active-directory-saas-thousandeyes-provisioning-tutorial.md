---
title: "Öğretici: Azure Active Directory ile otomatik kullanıcı sağlamayı ThousandEyes yapılandırma | Microsoft Docs"
description: "Nasıl tooThousandEyes tooconfigure, Azure Active Directory tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesapları öğrenin."
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
ms.openlocfilehash: f31883ab685d0ffcd9a830aa4a7d43c056f5f4cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-thousandeyes-for-automatic-user-provisioning"></a><span data-ttu-id="ee93b-103">Öğretici: ThousandEyes otomatik kullanıcı sağlamayı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ee93b-103">Tutorial: Configuring ThousandEyes for Automatic User Provisioning</span></span>


<span data-ttu-id="ee93b-104">Bu öğreticinin Hello hedefi ThousandEyes ve Azure AD tooautomatically sağlama tooperform gerekir ve Azure AD tooThousandEyes kullanıcı hesaplarından sağlanmasını adımları hello tooshow ' dir.</span><span class="sxs-lookup"><span data-stu-id="ee93b-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in ThousandEyes and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooThousandEyes.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ee93b-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ee93b-105">Prerequisites</span></span>

<span data-ttu-id="ee93b-106">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="ee93b-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="ee93b-107">Bir Azure Active directory kiracısı</span><span class="sxs-lookup"><span data-stu-id="ee93b-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="ee93b-108">Merhaba ThousandEyes kiracıyla [standart planı](https://www.thousandeyes.com/pricing) veya daha iyi etkin</span><span class="sxs-lookup"><span data-stu-id="ee93b-108">A ThousandEyes tenant with hello [Standard plan](https://www.thousandeyes.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="ee93b-109">ThousandEyes yönetici izinlerine sahip bir kullanıcı hesabı</span><span class="sxs-lookup"><span data-stu-id="ee93b-109">A user account in ThousandEyes with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="ee93b-110">Merhaba tümleştirme sağlama Azure AD kullanır hello üzerinde [ThousandEyes SCIM'yi API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), kullanılabilir tooThousandEyes takımlar hello standart plan üzerinde ya da daha iyi olduğu.</span><span class="sxs-lookup"><span data-stu-id="ee93b-110">hello Azure AD provisioning integration relies on hello [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), which is available tooThousandEyes teams on hello Standard plan or better.</span></span>

## <a name="assigning-users-toothousandeyes"></a><span data-ttu-id="ee93b-111">Kullanıcıların tooThousandEyes atama</span><span class="sxs-lookup"><span data-stu-id="ee93b-111">Assigning users tooThousandEyes</span></span>

<span data-ttu-id="ee93b-112">Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır.</span><span class="sxs-lookup"><span data-stu-id="ee93b-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="ee93b-113">Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="ee93b-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="ee93b-114">Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya tooyour ThousandEyes uygulamasına erişmesi Azure AD temsil hello kullanıcılar gruplarında toodecide gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee93b-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour ThousandEyes app.</span></span> <span data-ttu-id="ee93b-115">Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour ThousandEyes uygulama atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ee93b-115">Once decided, you can assign these users tooyour ThousandEyes app by following hello instructions here:</span></span>

[<span data-ttu-id="ee93b-116">Bir kullanıcı veya grup tooan kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="ee93b-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toothousandeyes"></a><span data-ttu-id="ee93b-117">Kullanıcıların tooThousandEyes atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="ee93b-117">Important tips for assigning users tooThousandEyes</span></span>

*   <span data-ttu-id="ee93b-118">Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooThousandEyes tootest hello atanır.</span><span class="sxs-lookup"><span data-stu-id="ee93b-118">It is recommended that a single Azure AD user is assigned tooThousandEyes tootest hello provisioning configuration.</span></span> <span data-ttu-id="ee93b-119">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="ee93b-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="ee93b-120">Bir kullanıcı tooThousandEyes atarken ya da hello seçmelisiniz **kullanıcı** rol ya da başka bir geçerli uygulamaya özgü rolü (varsa) hello atama iletişim.</span><span class="sxs-lookup"><span data-stu-id="ee93b-120">When assigning a user tooThousandEyes, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="ee93b-121">Merhaba **varsayılan erişim** rol sağlamak için çalışmaz ve bu kullanıcılar atlandı.</span><span class="sxs-lookup"><span data-stu-id="ee93b-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toothousandeyes"></a><span data-ttu-id="ee93b-122">Kullanıcı tooThousandEyes hazırlama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ee93b-122">Configuring user provisioning tooThousandEyes</span></span> 

<span data-ttu-id="ee93b-123">Bu bölümde, Azure AD tooThousandEyes kullanıcının kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve kullanıcı ve grup atama göre ThousandEyes atanan kullanıcı hesaplarında devre dışı bırak Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ee93b-123">This section guides you through connecting your Azure AD tooThousandEyes's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in ThousandEyes based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="ee93b-124">Sağlanan hello yönergeleri izleyerek ThousandEyes için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ee93b-124">You may also choose tooenabled SAML-based Single Sign-On for ThousandEyes, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ee93b-125">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="ee93b-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toothousandeyes-in-azure-ad"></a><span data-ttu-id="ee93b-126">Azure AD'de tooThousandEyes sağlama otomatik olarak bir kullanıcı hesabı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="ee93b-126">Configure automatic user account provisioning tooThousandEyes in Azure AD</span></span>


1. <span data-ttu-id="ee93b-127">Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="ee93b-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="ee93b-128">Çoklu oturum açma için zaten ThousandEyes yapılandırdıysanız, hello arama alanı kullanarak ThousandEyes Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="ee93b-128">If you have already configured ThousandEyes for single sign-on, search for your instance of ThousandEyes using hello search field.</span></span> <span data-ttu-id="ee93b-129">Aksi takdirde seçin **Ekle** arayın ve **ThousandEyes** hello uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="ee93b-129">Otherwise, select **Add** and search for **ThousandEyes** in hello application gallery.</span></span> <span data-ttu-id="ee93b-130">Merhaba Arama sonuçlarından ThousandEyes seçin ve uygulamaların tooyour listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ee93b-130">Select ThousandEyes from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="ee93b-131">ThousandEyes örneğiniz seçin ve ardından hello **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ee93b-131">Select your instance of ThousandEyes, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="ee93b-132">Set hello **sağlama modu** çok**otomatik**.</span><span class="sxs-lookup"><span data-stu-id="ee93b-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![ThousandEyes sağlama](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes1.png)

5. <span data-ttu-id="ee93b-134">Merhaba altında **yönetici kimlik bilgileri** bölümü, giriş hello **gizli belirteci** ThousandEyes'ın hesap tarafından oluşturulan (Merhaba belirteci ThousandEyes hesabınızın altında bulabilirsiniz: **güvenlik & Kimlik doğrulama**).</span><span class="sxs-lookup"><span data-stu-id="ee93b-134">Under hello **Admin Credentials** section, input hello **Secret Token** generated by your ThousandEyes's account (you can find hello token under your ThousandEyes account: **Security & Authentication**).</span></span> 

    ![ThousandEyes sağlama](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes2.png)

6. <span data-ttu-id="ee93b-136">Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour ThousandEyes uygulama bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ee93b-136">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour ThousandEyes app.</span></span> <span data-ttu-id="ee93b-137">Merhaba bağlantı başarısız olursa ThousandEyes hesabınız yönetici izinlerine sahip olduğundan emin olun ve 5. adım yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="ee93b-137">If hello connection fails, ensure your ThousandEyes account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="ee93b-138">Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve onay hello onay kutusu "bir e-posta bildirim gönder bir hata oluştuğunda."</span><span class="sxs-lookup"><span data-stu-id="ee93b-138">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="ee93b-139">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ee93b-139">Click **Save**.</span></span> 

9. <span data-ttu-id="ee93b-140">Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="ee93b-140">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooThousandEyes**.</span></span>

10. <span data-ttu-id="ee93b-141">Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooThousandEyes eşitlenir hello kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="ee93b-141">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooThousandEyes.</span></span> <span data-ttu-id="ee93b-142">Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları ThousandEyes içinde güncelleştirme işlemleri için özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="ee93b-142">hello attributes selected as **Matching** properties are used toomatch hello user accounts in ThousandEyes for update operations.</span></span> <span data-ttu-id="ee93b-143">Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.</span><span class="sxs-lookup"><span data-stu-id="ee93b-143">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="ee93b-144">tooenable hello ThousandEyes, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello içinde **ayarları** bölümü</span><span class="sxs-lookup"><span data-stu-id="ee93b-144">tooenable hello Azure AD provisioning service for ThousandEyes, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="ee93b-145">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ee93b-145">Click **Save**.</span></span> 

<span data-ttu-id="ee93b-146">Bu işlem, herhangi bir kullanıcı ve/veya hello kullanıcılar tooThousandEyes ve Gruplar bölümü atanan gruplarını hello ilk eşitleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="ee93b-146">This operation starts hello initial synchronization of any users and/or groups assigned tooThousandEyes in hello Users and Groups section.</span></span> <span data-ttu-id="ee93b-147">Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır.</span><span class="sxs-lookup"><span data-stu-id="ee93b-147">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="ee93b-148">Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler açıklanmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.</span><span class="sxs-lookup"><span data-stu-id="ee93b-148">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="ee93b-149">Hello Azure AD tooread sağlama nasıl oturum ile ilgili daha fazla bilgi için bkz: [otomatik olarak bir kullanıcı hesabı sağlama raporlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="ee93b-149">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="ee93b-150">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ee93b-150">Additional resources</span></span>

* [<span data-ttu-id="ee93b-151">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="ee93b-151">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="ee93b-152">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="ee93b-152">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="ee93b-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ee93b-153">Next steps</span></span>

* [<span data-ttu-id="ee93b-154">Tooreview nasıl günlüğe yazacağını öğrenin ve etkinlik sağlama raporları alın</span><span class="sxs-lookup"><span data-stu-id="ee93b-154">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
