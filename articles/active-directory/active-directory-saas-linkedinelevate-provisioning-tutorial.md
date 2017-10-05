---
title: "Öğretici: Azure Active Directory ile otomatik kullanıcı sağlamayı LinkedIn yükseltmesine yapılandırma | Microsoft Docs"
description: "Otomatik olarak sağlamak ve LinkedIn yükseltmesine kullanıcı hesaplarına sağlanmasını için Azure Active Directory yapılandırmayı öğrenin."
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
ms.openlocfilehash: 526666301aad1e5284c621024649d9cd52c92d18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-linkedin-elevate-for-automatic-user-provisioning"></a><span data-ttu-id="fd2c9-103">Öğretici: Yapılandırma LinkedIn yükseltmesine otomatik kullanıcı hazırlama</span><span class="sxs-lookup"><span data-stu-id="fd2c9-103">Tutorial: Configuring LinkedIn Elevate for Automatic User Provisioning</span></span>


<span data-ttu-id="fd2c9-104">Bu öğreticinin amacı LinkedIn yükseltmesine ve Azure AD otomatik olarak sağlamak ve kullanıcı hesaplarına Azure AD'den LinkedIn yükseltmesine sağlanmasını gerçekleştirmek için gereken adımları Göster sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-104">The objective of this tutorial is to show you the steps you need to perform in LinkedIn Elevate and Azure AD to automatically provision and de-provision user accounts from Azure AD to LinkedIn Elevate.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fd2c9-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fd2c9-105">Prerequisites</span></span>

<span data-ttu-id="fd2c9-106">Bu öğreticide gösterilen senaryo, aşağıdaki öğeleri zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="fd2c9-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="fd2c9-107">Azure Active Directory kiracısı</span><span class="sxs-lookup"><span data-stu-id="fd2c9-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="fd2c9-108">Bir LinkedIn yükseltmesine Kiracı</span><span class="sxs-lookup"><span data-stu-id="fd2c9-108">A LinkedIn Elevate tenant</span></span> 
*   <span data-ttu-id="fd2c9-109">Bir yönetici hesabında LinkedIn yükseltmesine LinkedIn hesap Merkezi erişim</span><span class="sxs-lookup"><span data-stu-id="fd2c9-109">An administrator account in LinkedIn Elevate with access to the LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="fd2c9-110">Azure Active Directory tümleştirir LinkedIn Yükselt'i kullanmaya [SCIM'yi](http://www.simplecloud.info/) protokolü.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-110">Azure Active Directory integrates with LinkedIn Elevate using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-linkedin-elevate"></a><span data-ttu-id="fd2c9-111">LinkedIn yükseltmek için kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="fd2c9-111">Assigning users to LinkedIn Elevate</span></span>

<span data-ttu-id="fd2c9-112">Azure Active Directory "atamaları" adlı bir kavram hangi kullanıcıların seçili uygulamalara erişim alması belirlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="fd2c9-113">Otomatik olarak bir kullanıcı hesabı sağlama bağlamında, yalnızca kullanıcıların ve grupların "Azure AD uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="fd2c9-114">Yapılandırma ve sağlama hizmeti etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD grupları LinkedIn yükseltmesine erişmek isteyen kullanıcıların temsil eden karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to LinkedIn Elevate.</span></span> <span data-ttu-id="fd2c9-115">Karar sonra bu kullanıcılar LinkedIn yükseltmek için buradaki yönergeleri izleyerek atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fd2c9-115">Once decided, you can assign these users to LinkedIn Elevate by following the instructions here:</span></span>

[<span data-ttu-id="fd2c9-116">Bir kullanıcı veya grup için bir kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="fd2c9-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-linkedin-elevate"></a><span data-ttu-id="fd2c9-117">LinkedIn yükseltmek için kullanıcılara atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="fd2c9-117">Important tips for assigning users to LinkedIn Elevate</span></span>

*   <span data-ttu-id="fd2c9-118">Önerilir tek bir Azure AD kullanıcısının atanabilir LinkedIn yükseltmek için sağlama yapılandırmayı test etmek.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-118">It is recommended that a single Azure AD user be assigned to LinkedIn Elevate to test the provisioning configuration.</span></span> <span data-ttu-id="fd2c9-119">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="fd2c9-120">Bir kullanıcı LinkedIn yükseltmek için atarken seçmelisiniz **kullanıcı** rol ataması iletişim.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-120">When assigning a user to LinkedIn Elevate, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="fd2c9-121">"Varsayılan erişim" rolü sağlama için çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-linkedin-elevate"></a><span data-ttu-id="fd2c9-122">LinkedIn yükseltmek kullanıcı hazırlama işleminin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="fd2c9-122">Configuring user provisioning to LinkedIn Elevate</span></span>

<span data-ttu-id="fd2c9-123">Bu bölümde, Azure AD API sağlama LinkedIn Yükselt'ın SCIM'yi kullanıcı hesabına bağlanma yoluyla size rehberlik eder ve kullanıcı ve grup atama Azure AD'de göre LinkedIn yükseltmesine kullanıcı hesapları oluşturma, güncelleştirme ve devre dışı bırakmak için sağlama hizmeti yapılandırma atanır.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-123">This section guides you through connecting your Azure AD to LinkedIn Elevate's SCIM user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in LinkedIn Elevate based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="fd2c9-124">**İpucu:** için etkin şeklinde SAML tabanlı çoklu oturum açma LinkedIn sağlanan yönergeleri izleyerek yükseltmesine, tercih edebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fd2c9-124">**Tip:** You may also choose to enabled SAML-based Single Sign-On for LinkedIn Elevate, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fd2c9-125">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-linkedin-elevate-in-azure-ad"></a><span data-ttu-id="fd2c9-126">Otomatik olarak bir kullanıcı hesabı LinkedIn yükseltmek için Azure AD'de sağlama yapılandırmak için:</span><span class="sxs-lookup"><span data-stu-id="fd2c9-126">To configure automatic user account provisioning to LinkedIn Elevate in Azure AD:</span></span>


<span data-ttu-id="fd2c9-127">LinkedIn erişim belirteci almak için ilk adımdır bakın.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-127">The first step is to retrieve your LinkedIn access token.</span></span> <span data-ttu-id="fd2c9-128">Bir kuruluş yöneticisi iseniz, bir erişim belirteci otomatik olarak sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="fd2c9-129">Hesap Merkezinize gidin **ayarları &gt; genel ayarları** açarak **SCIM'yi Kurulum** paneli.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-129">In your account center, go to **Settings &gt; Global Settings** and open the **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="fd2c9-130">Hesap Merkezi'nde yerine doğrudan bir bağlantı aracılığıyla erişiyorsanız aşağıdaki adımları kullanarak ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-130">If you are accessing the account center directly rather than through a link, you can reach it using the following steps.</span></span>

1)  <span data-ttu-id="fd2c9-131">Merkezi hesap için oturum açın.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-131">Sign in to Account Center.</span></span>

2)  <span data-ttu-id="fd2c9-132">Seçin **yönetici &gt; yönetici ayarları** .</span><span class="sxs-lookup"><span data-stu-id="fd2c9-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="fd2c9-133">Tıklatın **Gelişmiş tümleştirmeler** sol kenar çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-133">Click **Advanced Integrations** on the left sidebar.</span></span> <span data-ttu-id="fd2c9-134">Hesap Merkezi'nde yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-134">You are directed to the account center.</span></span>

4)  <span data-ttu-id="fd2c9-135">Tıklatın **+ Ekle yeni SCIM'yi yapılandırma** ve her alanı doldurarak yordamı izleyin.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-135">Click **+ Add new SCIM configuration** and follow the procedure by filling in each field.</span></span>

> <span data-ttu-id="fd2c9-136">Autoassign lisansları etkin değil, yalnızca kullanıcı verilerini eşitlenip anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![LinkedIn yükseltmesine sağlama](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate1.PNG)

> <span data-ttu-id="fd2c9-138">Autolicense atama etkinleştirildiğinde, uygulama örneği ve lisans türü Not gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-138">When auto­license assignment is enabled, you need to note the application instance and license type.</span></span> <span data-ttu-id="fd2c9-139">İlk gelen üzerinde atanmış lisansların, tüm lisanslar duruma kadar temel ilk hizmet.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-139">Licenses are assigned on a first come, first serve basis until all the licenses are taken.</span></span>

![LinkedIn yükseltmesine sağlama](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate2.PNG)

5)  <span data-ttu-id="fd2c9-141">Tıklatın **belirteç Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-141">Click **Generate token**.</span></span> <span data-ttu-id="fd2c9-142">Erişim belirteci görüntü altında görmelisiniz **erişim belirteci** alan.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-142">You should see your access token display under the **Access token** field.</span></span>

6)  <span data-ttu-id="fd2c9-143">Erişim belirteci sayfadan ayrılmadan önce Pano veya bilgisayara kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-143">Save your access token to your clipboard or computer before leaving the page.</span></span>

7) <span data-ttu-id="fd2c9-144">Ardından, oturum [Azure portal](https://portal.azure.com)ve **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-144">Next, sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="fd2c9-145">Zaten LinkedIn yükseltmek için çoklu oturum açmayı yapılandırdıysanız, örneğiniz LinkedIn arama alanı kullanımı ile yükseltme için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-145">If you have already configured LinkedIn Elevate for single sign-on, search for your instance of LinkedIn Elevate using the search field.</span></span> <span data-ttu-id="fd2c9-146">Aksi takdirde seçin **Ekle** arayın ve **LinkedIn yükseltmesine** uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-146">Otherwise, select **Add** and search for **LinkedIn Elevate** in the application gallery.</span></span> <span data-ttu-id="fd2c9-147">Arama sonuçlarından LinkedIn Yükselt'i seçin ve uygulamaları listenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-147">Select LinkedIn Elevate from the search results, and add it to your list of applications.</span></span>

9)  <span data-ttu-id="fd2c9-148">LinkedIn yükseltmesine örneğiniz seçin ve ardından **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-148">Select your instance of LinkedIn Elevate, then select the **Provisioning** tab.</span></span>

10) <span data-ttu-id="fd2c9-149">Ayarlama **sağlama modunda** için **otomatik**.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-149">Set the **Provisioning Mode** to **Automatic**.</span></span>

![LinkedIn yükseltmesine sağlama](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate3.PNG)

11)  <span data-ttu-id="fd2c9-151">Altında aşağıdaki alanları doldurun **yönetici kimlik bilgileri** :</span><span class="sxs-lookup"><span data-stu-id="fd2c9-151">Fill in the following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="fd2c9-152">İçinde **Kiracı URL** alanında, https://api.linkedin.com girin.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-152">In the **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="fd2c9-153">İçinde **gizli belirteci** alan, 1. adımda oluşturulan erişim belirteci girin ve tıklayın **Bağlantıyı Sına** .</span><span class="sxs-lookup"><span data-stu-id="fd2c9-153">In the **Secret Token** field, enter the access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="fd2c9-154">Portalınızı upperright tarafında bir başarı bildirimi görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-154">You should see a success notification on the upper­right side of   your portal.</span></span>

12) <span data-ttu-id="fd2c9-155">Bir kişi veya sağlama hata bildirimleri alması gereken Grup e-posta adresini girin **bildirim e-posta** alan ve aşağıdaki onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-155">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

13) <span data-ttu-id="fd2c9-156">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-156">Click **Save**.</span></span> 

14) <span data-ttu-id="fd2c9-157">İçinde **öznitelik eşlemelerini** bölümünde, Azure AD'den LinkedIn yükseltmek için eşitlenecek kullanıcı ve grup öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-157">In the **Attribute Mappings** section, review the user and group attributes that will be synchronized from Azure AD to LinkedIn Elevate.</span></span> <span data-ttu-id="fd2c9-158">Seçilen öznitelikler olarak Not **eşleşen** özellikleri, kullanıcı hesapları ve grupları LinkedIn yükseltmesine güncelleştirme işlemleri için eşleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-158">Note that the attributes selected as **Matching** properties will be used to match the user accounts and groups in LinkedIn Elevate for update operations.</span></span> <span data-ttu-id="fd2c9-159">Değişiklikleri kaydetmek için Kaydet düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-159">Select the Save button to commit any changes.</span></span>

![LinkedIn yükseltmesine sağlama](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate4.PNG)

15) <span data-ttu-id="fd2c9-161">Azure AD hizmeti LinkedIn yükseltmek için sağlama etkinleştirmek için değiştirmek **sağlama durumu** için **üzerinde** içinde **ayarları** bölümü</span><span class="sxs-lookup"><span data-stu-id="fd2c9-161">To enable the Azure AD provisioning service for LinkedIn Elevate, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

16) <span data-ttu-id="fd2c9-162">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-162">Click **Save**.</span></span> 

<span data-ttu-id="fd2c9-163">Bu, herhangi bir kullanıcı ve/veya LinkedIn yükseltmesine kullanıcılar ve Gruplar bölümünde atanan grupları ilk eşitleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-163">This will start the initial synchronization of any users and/or groups assigned to LinkedIn Elevate in the Users and Groups section.</span></span> <span data-ttu-id="fd2c9-164">İlk eşitlemeyi gerçekleştirmek için yaklaşık 20 dakikada çalıştığı sürece oluşan sonraki eşitlemeler uzun sürer unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-164">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="fd2c9-165">Kullanabileceğiniz **eşitleme ayrıntıları** bölüm ilerlemeyi izlemek ve LinkedIn yükseltmesine uygulamanızı sağlama hizmeti tarafından gerçekleştirilen tüm eylemler açıklanmaktadır etkinlik raporları sağlamak için bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="fd2c9-165">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your LinkedIn Elevate app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="fd2c9-166">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="fd2c9-166">Additional Resources</span></span>

* [<span data-ttu-id="fd2c9-167">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="fd2c9-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="fd2c9-168">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="fd2c9-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
