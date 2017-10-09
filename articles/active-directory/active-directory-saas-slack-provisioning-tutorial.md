---
title: "Öğretici: Azure Active Directory ile otomatik kullanıcı sağlamayı kayma yapılandırma | Microsoft Docs"
description: "Nasıl tooSlack tooconfigure, Azure Active Directory tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesapları öğrenin."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: d0a565bbe0bd7e229b9dd99b1ebbaf67d93a2206
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a><span data-ttu-id="27eb8-103">Öğretici: Kayma otomatik kullanıcı sağlamayı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="27eb8-103">Tutorial: Configuring Slack for Automatic User Provisioning</span></span>


<span data-ttu-id="27eb8-104">Merhaba Bu öğreticinin amacı olan kayma ve Azure tooperform gereken adımları hello tooshow AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooSlack.</span><span class="sxs-lookup"><span data-stu-id="27eb8-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Slack and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSlack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="27eb8-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="27eb8-105">Prerequisites</span></span>

<span data-ttu-id="27eb8-106">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="27eb8-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="27eb8-107">Bir Azure Active Active directory kiracısı</span><span class="sxs-lookup"><span data-stu-id="27eb8-107">An Azure Active Active directory tenant</span></span>
*   <span data-ttu-id="27eb8-108">Bir boşluk ile Merhaba Kiracı [planı artı](https://aadsyncfabric.slack.com/pricing) veya daha iyi etkin</span><span class="sxs-lookup"><span data-stu-id="27eb8-108">A Slack tenant with hello [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="27eb8-109">Kayma takım yönetici izinlerine sahip bir kullanıcı hesabı</span><span class="sxs-lookup"><span data-stu-id="27eb8-109">A user account in Slack with Team Admin permissions</span></span> 

<span data-ttu-id="27eb8-110">Not: Azure AD tümleştirme sağlama kullanır üzerinde hello hello [Slack'e SCIM'yi API](https://api.slack.com/scim) kullanılabilir tooSlack takımlar temelinde hello planı artı ya da daha iyi olduğu.</span><span class="sxs-lookup"><span data-stu-id="27eb8-110">Note: hello Azure AD provisioning integration relies on hello [Slack SCIM API](https://api.slack.com/scim) which is available tooSlack teams on hello Plus plan or better.</span></span>

## <a name="assigning-users-tooslack"></a><span data-ttu-id="27eb8-111">Kullanıcıların tooSlack atama</span><span class="sxs-lookup"><span data-stu-id="27eb8-111">Assigning users tooSlack</span></span>

<span data-ttu-id="27eb8-112">Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır.</span><span class="sxs-lookup"><span data-stu-id="27eb8-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="27eb8-113">Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="27eb8-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="27eb8-114">Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya tooyour Slack uygulamasına erişmesi Azure AD temsil hello kullanıcılar gruplarında toodecide gerekir.</span><span class="sxs-lookup"><span data-stu-id="27eb8-114">Before configuring and enabling hello provisioning service, you will need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Slack app.</span></span> <span data-ttu-id="27eb8-115">Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour Slack uygulama atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="27eb8-115">Once decided, you can assign these users tooyour Slack app by following hello instructions here:</span></span>

[<span data-ttu-id="27eb8-116">Bir kullanıcı veya grup tooan kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="27eb8-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-tooslack"></a><span data-ttu-id="27eb8-117">Kullanıcıların tooSlack atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="27eb8-117">Important tips for assigning users tooSlack</span></span>

*   <span data-ttu-id="27eb8-118">Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooSlack tootest hello atanabilir.</span><span class="sxs-lookup"><span data-stu-id="27eb8-118">It is recommended that a single Azure AD user be assigned tooSlack tootest hello provisioning configuration.</span></span> <span data-ttu-id="27eb8-119">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="27eb8-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="27eb8-120">Bir kullanıcı tooSlack atarken hello seçmelisiniz **kullanıcı** veya hello atama iletişim kutusunda "Grubu" rolü.</span><span class="sxs-lookup"><span data-stu-id="27eb8-120">When assigning a user tooSlack, you must select hello **User** or "Group" role in hello assignment dialog.</span></span> <span data-ttu-id="27eb8-121">Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="27eb8-121">hello "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-tooslack"></a><span data-ttu-id="27eb8-122">Kullanıcı tooSlack hazırlama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="27eb8-122">Configuring user provisioning tooSlack</span></span> 

<span data-ttu-id="27eb8-123">Bu bölümde, Azure AD tooSlack kullanıcının kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve Azure AD'de kullanıcı ve grup atama göre kayma atanan kullanıcı hesaplarında devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="27eb8-123">This section guides you through connecting your Azure AD tooSlack's user account provisioning API, and configuring hello provisioning service toocreate, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="27eb8-124">**İpucu:** tooenabled SAML tabanlı çoklu oturum açma (Azure Portalı'nda) sağlanan hello yönergeleri izleyerek kayma için tercih edebilirsiniz [https://portal.azure.com].</span><span class="sxs-lookup"><span data-stu-id="27eb8-124">**Tip:** You may also choose tooenabled SAML-based Single Sign-On for Slack, following hello instructions provided in (Azure portal)[https://portal.azure.com].</span></span> <span data-ttu-id="27eb8-125">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="27eb8-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-tooslack-in-azure-ad"></a><span data-ttu-id="27eb8-126">Azure AD'de tooSlack sağlama tooconfigure otomatik olarak bir kullanıcı hesabı:</span><span class="sxs-lookup"><span data-stu-id="27eb8-126">tooconfigure automatic user account provisioning tooSlack in Azure AD:</span></span>


1)  <span data-ttu-id="27eb8-127">Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="27eb8-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2) <span data-ttu-id="27eb8-128">Çoklu oturum açma için zaten kayma yapılandırdıysanız, hello arama alanı kullanarak kayma Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="27eb8-128">If you have already configured Slack for single sign-on, search for your instance of Slack using hello search field.</span></span> <span data-ttu-id="27eb8-129">Aksi takdirde seçin **Ekle** arayın ve **Slack'e** hello uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="27eb8-129">Otherwise, select **Add** and search for **Slack** in hello application gallery.</span></span> <span data-ttu-id="27eb8-130">Kayma hello Arama sonuçlarından seçin ve uygulamaların tooyour listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="27eb8-130">Select Slack from hello search results, and add it tooyour list of applications.</span></span>

3)  <span data-ttu-id="27eb8-131">Kayma örneğiniz seçin ve ardından hello **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="27eb8-131">Select your instance of Slack, then select hello **Provisioning** tab.</span></span>

4)  <span data-ttu-id="27eb8-132">Set hello **sağlama modu** çok**otomatik**.</span><span class="sxs-lookup"><span data-stu-id="27eb8-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

![Sağlama boşluk](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  <span data-ttu-id="27eb8-134">Merhaba altında **yönetici kimlik bilgileri** 'yi tıklatın **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="27eb8-134">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="27eb8-135">Bu, yeni bir tarayıcı penceresinde bir Slack yetkilendirme iletişim kutusunu açar.</span><span class="sxs-lookup"><span data-stu-id="27eb8-135">This opens a Slack authorization dialog in a new browser window.</span></span> 

6) <span data-ttu-id="27eb8-136">Merhaba yeni pencerede kayma takım yönetim hesabınızı kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="27eb8-136">In hello new window, sign into Slack using your Team Admin account.</span></span> <span data-ttu-id="27eb8-137">Hello elde edilen yetkilendirme iletişim kutusunda, select hello tooenable sağlamayı istiyor ve ardından Slack ekip **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="27eb8-137">in hello resulting authorization dialog, select hello Slack team that you want tooenable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="27eb8-138">Bir kez tamamlanan, dönüş toohello Azure portal toocomplete hello yapılandırma sağlama.</span><span class="sxs-lookup"><span data-stu-id="27eb8-138">Once completed, return toohello Azure portal toocomplete hello provisioning configuration.</span></span>

![Yetkilendirme iletişim](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) <span data-ttu-id="27eb8-140">Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour Slack uygulama bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="27eb8-140">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Slack app.</span></span> <span data-ttu-id="27eb8-141">Merhaba bağlantı başarısız olursa Slack hesabınızın Team yönetici izinlerine sahip olduğundan emin olun ve hello "Yetkilendir" adım yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="27eb8-141">If hello connection fails, ensure your Slack account has Team Admin permissions and try hello "Authorize" step again.</span></span>

8) <span data-ttu-id="27eb8-142">Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve aşağıdaki hello onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="27eb8-142">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

9) <span data-ttu-id="27eb8-143">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="27eb8-143">Click **Save**.</span></span> 

10) <span data-ttu-id="27eb8-144">Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooSlack**.</span><span class="sxs-lookup"><span data-stu-id="27eb8-144">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSlack**.</span></span>

11) <span data-ttu-id="27eb8-145">Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooSlack eşitleneceğini hello kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="27eb8-145">In hello **Attribute Mappings** section, review hello user attributes that will be synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="27eb8-146">Seçilen öznitelikler hello Not **eşleşen** özellikleri, Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları kayma içinde güncelleştirme işlemleri için olacaktır.</span><span class="sxs-lookup"><span data-stu-id="27eb8-146">Note that hello attributes selected as **Matching** properties will be used toomatch hello user accounts in Slack for update operations.</span></span> <span data-ttu-id="27eb8-147">Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.</span><span class="sxs-lookup"><span data-stu-id="27eb8-147">Select hello Save button toocommit any changes.</span></span>

12) <span data-ttu-id="27eb8-148">tooenable hello kayma, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello içinde **ayarları** bölümü</span><span class="sxs-lookup"><span data-stu-id="27eb8-148">tooenable hello Azure AD provisioning service for Slack, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

13) <span data-ttu-id="27eb8-149">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="27eb8-149">Click **Save**.</span></span> 

<span data-ttu-id="27eb8-150">Bu, herhangi bir kullanıcı ve/veya hello kullanıcılar tooSlack ve Gruplar bölümü atanan gruplarını hello ilk eşitleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="27eb8-150">This will start hello initial synchronization of any users and/or groups assigned tooSlack in hello Users and Groups section.</span></span> <span data-ttu-id="27eb8-151">Merhaba ilk eşitleme yaklaşık her 10 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform gerektiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="27eb8-151">Note that hello initial sync will take longer tooperform than subsequent syncs, which occur approximately every 10 minutes as long as hello service is running.</span></span> <span data-ttu-id="27eb8-152">Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve Slack uygulamanızdan hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.</span><span class="sxs-lookup"><span data-stu-id="27eb8-152">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Slack app.</span></span>

## <a name="optional-configuring-group-object-provisioning-tooslack"></a><span data-ttu-id="27eb8-153">[İsteğe bağlı] Grup nesnesi tooSlack sağlama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="27eb8-153">[Optional] Configuring group object provisioning tooSlack</span></span> 

<span data-ttu-id="27eb8-154">İsteğe bağlı olarak, Azure AD tooSlack Grup nesnelerle hello sağlamayı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27eb8-154">Optionally, you can enable hello provisioning of group objects from Azure AD tooSlack.</span></span> <span data-ttu-id="27eb8-155">Bu "kullanıcı gruplarını atamasını" farklıdır, bu hello gerçek Grup nesnesi ayrıca tooits üyeleri Azure AD tooSlack çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="27eb8-155">This is different from "assigning groups of users", in that hello actual group object in addition tooits members will be replicated from Azure AD tooSlack.</span></span> <span data-ttu-id="27eb8-156">Örneğin, Azure AD içinde "My grubu" adlı bir grup varsa, "My grubu" adlı bir identitical grubu kayma içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="27eb8-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span></span>

### <a name="tooenable-provisioning-of-group-objects"></a><span data-ttu-id="27eb8-157">tooenable group nesnelerini sağlama:</span><span class="sxs-lookup"><span data-stu-id="27eb8-157">tooenable provisioning of group objects:</span></span>

1) <span data-ttu-id="27eb8-158">Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory grupları tooSlack**.</span><span class="sxs-lookup"><span data-stu-id="27eb8-158">Under hello Mappings section, select **Synchronize Azure Active Directory Groups tooSlack**.</span></span>

2) <span data-ttu-id="27eb8-159">Merhaba eşleme özniteliği dikey penceresinde, etkin tooYes ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="27eb8-159">In hello Attribute Mapping blade, set Enabled tooYes.</span></span>

3) <span data-ttu-id="27eb8-160">Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooSlack eşitleneceğini hello grup öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="27eb8-160">In hello **Attribute Mappings** section, review hello group attributes that will be synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="27eb8-161">Seçilen öznitelikler hello Not **eşleşen** özellikler kullanılan toomatch hello gruplarında kayma güncelleştirme işlemleri için olacaktır.</span><span class="sxs-lookup"><span data-stu-id="27eb8-161">Note that hello attributes selected as **Matching** properties will be used toomatch hello groups in Slack for update operations.</span></span> 

4) <span data-ttu-id="27eb8-162">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="27eb8-162">Click **Save**.</span></span>

<span data-ttu-id="27eb8-163">Merhaba, tüm Grup atanmış nesneleri tooSlack bu sonucu **kullanıcılar ve gruplar** tam olarak Azure AD tooSlack eşitlenmekte olan bölüm.</span><span class="sxs-lookup"><span data-stu-id="27eb8-163">This result in any group objects assigned tooSlack in hello **Users and Groups** section being fully synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="27eb8-164">Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve Slack uygulamanızdan hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.</span><span class="sxs-lookup"><span data-stu-id="27eb8-164">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Slack app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="27eb8-165">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="27eb8-165">Additional Resources</span></span>

* [<span data-ttu-id="27eb8-166">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="27eb8-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="27eb8-167">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="27eb8-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
