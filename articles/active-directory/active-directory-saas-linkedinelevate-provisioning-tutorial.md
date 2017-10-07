---
title: "Öğretici: Azure Active Directory ile otomatik kullanıcı sağlamayı LinkedIn yükseltmesine yapılandırma | Microsoft Docs"
description: "Nasıl tooLinkedIn yükseltme tooconfigure, Azure Active Directory tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesapları öğrenin."
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
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 08201c078ece0054e75ec0c004840e5186e0e704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-elevate-for-automatic-user-provisioning"></a><span data-ttu-id="5c15e-103">Öğretici: Yapılandırma LinkedIn yükseltmesine otomatik kullanıcı hazırlama</span><span class="sxs-lookup"><span data-stu-id="5c15e-103">Tutorial: Configuring LinkedIn Elevate for Automatic User Provisioning</span></span>


<span data-ttu-id="5c15e-104">Bu öğreticinin Hello hedefi LinkedIn yükseltmesine ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooLinkedIn yükseltme tooperform gereken adımları hello tooshow ' dir.</span><span class="sxs-lookup"><span data-stu-id="5c15e-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in LinkedIn Elevate and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooLinkedIn Elevate.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5c15e-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5c15e-105">Prerequisites</span></span>

<span data-ttu-id="5c15e-106">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="5c15e-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="5c15e-107">Azure Active Directory kiracısı</span><span class="sxs-lookup"><span data-stu-id="5c15e-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="5c15e-108">Bir LinkedIn yükseltmesine Kiracı</span><span class="sxs-lookup"><span data-stu-id="5c15e-108">A LinkedIn Elevate tenant</span></span> 
*   <span data-ttu-id="5c15e-109">Bir yönetici hesabıyla LinkedIn yükseltmesine de erişim toohello LinkedIn hesap Merkezi</span><span class="sxs-lookup"><span data-stu-id="5c15e-109">An administrator account in LinkedIn Elevate with access toohello LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="5c15e-110">Azure Active Directory tümleştirir LinkedIn hello kullanımı ile yükseltme ile [SCIM'yi](http://www.simplecloud.info/) protokolü.</span><span class="sxs-lookup"><span data-stu-id="5c15e-110">Azure Active Directory integrates with LinkedIn Elevate using hello [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-toolinkedin-elevate"></a><span data-ttu-id="5c15e-111">Kullanıcıların tooLinkedIn yükseltme atama</span><span class="sxs-lookup"><span data-stu-id="5c15e-111">Assigning users tooLinkedIn Elevate</span></span>

<span data-ttu-id="5c15e-112">Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır.</span><span class="sxs-lookup"><span data-stu-id="5c15e-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="5c15e-113">Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="5c15e-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="5c15e-114">Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD tooLinkedIn yükseltme erişmesi hello kullanıcıları temsil gruplarında toodecide gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c15e-114">Before configuring and enabling hello provisioning service, you will need toodecide what users and/or groups in Azure AD represent hello users who need access tooLinkedIn Elevate.</span></span> <span data-ttu-id="5c15e-115">Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooLinkedIn yükseltme atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5c15e-115">Once decided, you can assign these users tooLinkedIn Elevate by following hello instructions here:</span></span>

[<span data-ttu-id="5c15e-116">Bir kullanıcı veya grup tooan kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="5c15e-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-elevate"></a><span data-ttu-id="5c15e-117">Kullanıcıların tooLinkedIn yükseltme atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="5c15e-117">Important tips for assigning users tooLinkedIn Elevate</span></span>

*   <span data-ttu-id="5c15e-118">Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooLinkedIn yükseltme tootest hello atanabilir.</span><span class="sxs-lookup"><span data-stu-id="5c15e-118">It is recommended that a single Azure AD user be assigned tooLinkedIn Elevate tootest hello provisioning configuration.</span></span> <span data-ttu-id="5c15e-119">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="5c15e-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="5c15e-120">Bir kullanıcı tooLinkedIn yükseltme atarken hello seçmelisiniz **kullanıcı** hello atama iletişim rolü.</span><span class="sxs-lookup"><span data-stu-id="5c15e-120">When assigning a user tooLinkedIn Elevate, you must select hello **User** role in hello assignment dialog.</span></span> <span data-ttu-id="5c15e-121">Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="5c15e-121">hello "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-toolinkedin-elevate"></a><span data-ttu-id="5c15e-122">Kullanıcı tooLinkedIn yükseltme hazırlama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5c15e-122">Configuring user provisioning tooLinkedIn Elevate</span></span>

<span data-ttu-id="5c15e-123">Bu bölümde, API sağlama, Azure AD tooLinkedIn yükseltme'nın SCIM'yi kullanıcı hesabı konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve kullanıcı ve Grup göre LinkedIn yükseltmesine atanan kullanıcı hesaplarında devre dışı bırak Azure AD'de atama.</span><span class="sxs-lookup"><span data-stu-id="5c15e-123">This section guides you through connecting your Azure AD tooLinkedIn Elevate's SCIM user account provisioning API, and configuring hello provisioning service toocreate, update and disable assigned user accounts in LinkedIn Elevate based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="5c15e-124">**İpucu:** LinkedIn sağlanan hello yönergeleri izleyerek yükseltmesine için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5c15e-124">**Tip:** You may also choose tooenabled SAML-based Single Sign-On for LinkedIn Elevate, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5c15e-125">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="5c15e-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-elevate-in-azure-ad"></a><span data-ttu-id="5c15e-126">Azure AD'de tooLinkedIn yükseltme sağlama tooconfigure otomatik olarak bir kullanıcı hesabı:</span><span class="sxs-lookup"><span data-stu-id="5c15e-126">tooconfigure automatic user account provisioning tooLinkedIn Elevate in Azure AD:</span></span>


<span data-ttu-id="5c15e-127">Merhaba ilk adımı tooretrieve LinkedIn erişim belirteci değil.</span><span class="sxs-lookup"><span data-stu-id="5c15e-127">hello first step is tooretrieve your LinkedIn access token.</span></span> <span data-ttu-id="5c15e-128">Bir kuruluş yöneticisi iseniz, bir erişim belirteci otomatik olarak sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c15e-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="5c15e-129">Hesap Merkezinize çok Git**ayarları &gt; genel ayarları** ve açık hello **SCIM'yi Kurulum** paneli.</span><span class="sxs-lookup"><span data-stu-id="5c15e-129">In your account center, go too**Settings &gt; Global Settings** and open hello **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="5c15e-130">Merhaba hesap Merkezi'nde yerine doğrudan bir bağlantı aracılığıyla erişiyorsanız aşağıdaki adımları hello kullanarak ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c15e-130">If you are accessing hello account center directly rather than through a link, you can reach it using hello following steps.</span></span>

1)  <span data-ttu-id="5c15e-131">TooAccount Merkezi'nde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5c15e-131">Sign in tooAccount Center.</span></span>

2)  <span data-ttu-id="5c15e-132">Seçin **yönetici &gt; yönetici ayarları** .</span><span class="sxs-lookup"><span data-stu-id="5c15e-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="5c15e-133">Tıklatın **Gelişmiş tümleştirmeler** hello sol kenar üzerinde.</span><span class="sxs-lookup"><span data-stu-id="5c15e-133">Click **Advanced Integrations** on hello left sidebar.</span></span> <span data-ttu-id="5c15e-134">Yönlendirilmiş toohello hesap Merkezi'nde var.</span><span class="sxs-lookup"><span data-stu-id="5c15e-134">You are directed toohello account center.</span></span>

4)  <span data-ttu-id="5c15e-135">Tıklatın **+ Ekle yeni SCIM'yi yapılandırma** ve her alanı doldurarak hello yordamı izleyin.</span><span class="sxs-lookup"><span data-stu-id="5c15e-135">Click **+ Add new SCIM configuration** and follow hello procedure by filling in each field.</span></span>

> <span data-ttu-id="5c15e-136">Autoassign lisansları etkin değil, yalnızca kullanıcı verilerini eşitlenip anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="5c15e-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![LinkedIn yükseltmesine sağlama](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate1.PNG)

> <span data-ttu-id="5c15e-138">Autolicense atama etkinleştirildiğinde, toonote uygulama örneği ve lisans türü gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c15e-138">When auto­license assignment is enabled, you need toonote the application instance and license type.</span></span> <span data-ttu-id="5c15e-139">İlk gelen üzerinde atanmış lisansların, tüm hello lisansları duruma kadar temel ilk hizmet.</span><span class="sxs-lookup"><span data-stu-id="5c15e-139">Licenses are assigned on a first come, first serve basis until all hello licenses are taken.</span></span>

![LinkedIn yükseltmesine sağlama](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate2.PNG)

5)  <span data-ttu-id="5c15e-141">Tıklatın **belirteç Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="5c15e-141">Click **Generate token**.</span></span> <span data-ttu-id="5c15e-142">Erişim belirteci ekranınıza hello altında görmelisiniz **erişim belirteci** alan.</span><span class="sxs-lookup"><span data-stu-id="5c15e-142">You should see your access token display under hello **Access token** field.</span></span>

6)  <span data-ttu-id="5c15e-143">Erişim belirteci tooyour Pano veya bilgisayar hello sayfadan ayrılmadan önce kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5c15e-143">Save your access token tooyour clipboard or computer before leaving hello page.</span></span>

7) <span data-ttu-id="5c15e-144">Ardından, toohello içinde oturum [Azure portal](https://portal.azure.com)ve toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölüm.</span><span class="sxs-lookup"><span data-stu-id="5c15e-144">Next, sign in toohello [Azure portal](https://portal.azure.com), and browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="5c15e-145">Zaten LinkedIn yükseltmek için çoklu oturum açmayı yapılandırdıysanız, örneğiniz LinkedIn hello arama alanı kullanımı ile yükseltme için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="5c15e-145">If you have already configured LinkedIn Elevate for single sign-on, search for your instance of LinkedIn Elevate using hello search field.</span></span> <span data-ttu-id="5c15e-146">Aksi takdirde seçin **Ekle** arayın ve **LinkedIn yükseltmesine** hello uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="5c15e-146">Otherwise, select **Add** and search for **LinkedIn Elevate** in hello application gallery.</span></span> <span data-ttu-id="5c15e-147">Merhaba Arama sonuçlarından LinkedIn Yükselt'i seçin ve uygulamaların tooyour listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5c15e-147">Select LinkedIn Elevate from hello search results, and add it tooyour list of applications.</span></span>

9)  <span data-ttu-id="5c15e-148">LinkedIn yükseltmesine örneğiniz seçin ve ardından hello **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5c15e-148">Select your instance of LinkedIn Elevate, then select hello **Provisioning** tab.</span></span>

10) <span data-ttu-id="5c15e-149">Set hello **sağlama modu** çok**otomatik**.</span><span class="sxs-lookup"><span data-stu-id="5c15e-149">Set hello **Provisioning Mode** too**Automatic**.</span></span>

![LinkedIn yükseltmesine sağlama](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate3.PNG)

11)  <span data-ttu-id="5c15e-151">Alanlar'ın altında aşağıdaki hello doldurun **yönetici kimlik bilgileri** :</span><span class="sxs-lookup"><span data-stu-id="5c15e-151">Fill in hello following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="5c15e-152">Merhaba, **Kiracı URL** alanında, https://api.linkedin.com girin.</span><span class="sxs-lookup"><span data-stu-id="5c15e-152">In hello **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="5c15e-153">Merhaba, **gizli belirteci** alan, 1. adımda oluşturulan hello erişim belirtecini girin ve tıklatın **Bağlantıyı Sına** .</span><span class="sxs-lookup"><span data-stu-id="5c15e-153">In hello **Secret Token** field, enter hello access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="5c15e-154">Merhaba upperright tarafında portalınızı başarı bildirim görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c15e-154">You should see a success notification on hello upper­right side of   your portal.</span></span>

12) <span data-ttu-id="5c15e-155">Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve aşağıdaki hello onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="5c15e-155">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

13) <span data-ttu-id="5c15e-156">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5c15e-156">Click **Save**.</span></span> 

14) <span data-ttu-id="5c15e-157">Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooLinkedIn ' yükseltme eşitleneceğini hello kullanıcı ve grup öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="5c15e-157">In hello **Attribute Mappings** section, review hello user and group attributes that will be synchronized from Azure AD tooLinkedIn Elevate.</span></span> <span data-ttu-id="5c15e-158">Seçilen öznitelikler hello Not **eşleşen** özellikler kullanılan toomatch hello kullanıcı hesapları ve grupları LinkedIn yükseltmesine güncelleştirme işlemleri için olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5c15e-158">Note that hello attributes selected as **Matching** properties will be used toomatch hello user accounts and groups in LinkedIn Elevate for update operations.</span></span> <span data-ttu-id="5c15e-159">Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.</span><span class="sxs-lookup"><span data-stu-id="5c15e-159">Select hello Save button toocommit any changes.</span></span>

![LinkedIn yükseltmesine sağlama](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate4.PNG)

15) <span data-ttu-id="5c15e-161">tooenable hello LinkedIn yükseltme, değiştirme hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello içinde **ayarları** bölümü</span><span class="sxs-lookup"><span data-stu-id="5c15e-161">tooenable hello Azure AD provisioning service for LinkedIn Elevate, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

16) <span data-ttu-id="5c15e-162">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5c15e-162">Click **Save**.</span></span> 

<span data-ttu-id="5c15e-163">Bu herhangi bir kullanıcı ilk eşitleme hello başlatır ve/veya gruplarının tooLinkedIn hello kullanıcılar ve Gruplar bölümünde yükseltme atanmış.</span><span class="sxs-lookup"><span data-stu-id="5c15e-163">This will start hello initial synchronization of any users and/or groups assigned tooLinkedIn Elevate in hello Users and Groups section.</span></span> <span data-ttu-id="5c15e-164">Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform gerektiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="5c15e-164">Note that hello initial sync will take longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="5c15e-165">Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve LinkedIn yükseltmesine uygulamanızdan hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.</span><span class="sxs-lookup"><span data-stu-id="5c15e-165">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your LinkedIn Elevate app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="5c15e-166">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="5c15e-166">Additional Resources</span></span>

* [<span data-ttu-id="5c15e-167">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="5c15e-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="5c15e-168">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="5c15e-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
