---
title: "Öğretici: Azure Active Directory Tümleştirme ile Concur | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Concur arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: cd35b6e2dc3171e9cffdb820bbc5b0d45ff58e07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a><span data-ttu-id="37243-103">Öğretici: Yapılandırma Concur kullanıcı sağlamak için</span><span class="sxs-lookup"><span data-stu-id="37243-103">Tutorial: Configuring Concur for User Provisioning</span></span>

<span data-ttu-id="37243-104">Bu öğreticinin amacı Concur ve Azure AD otomatik olarak sağlamak ve kullanıcı hesaplarına Azure AD'den Concur sağlanmasını gerçekleştirmek için gereken adımları Göster sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="37243-104">The objective of this tutorial is to show you the steps you need to perform in Concur and Azure AD to automatically provision and de-provision user accounts from Azure AD to Concur.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37243-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="37243-105">Prerequisites</span></span>

<span data-ttu-id="37243-106">Bu öğreticide gösterilen senaryo, aşağıdaki öğeleri zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="37243-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="37243-107">Bir Azure Active directory kiracısı.</span><span class="sxs-lookup"><span data-stu-id="37243-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="37243-108">Bir Concur çoklu oturum açma abonelik etkin.</span><span class="sxs-lookup"><span data-stu-id="37243-108">A Concur single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="37243-109">Concur takım yönetici izinlerine sahip bir kullanıcı hesabının.</span><span class="sxs-lookup"><span data-stu-id="37243-109">A user account in Concur with Team Admin permissions.</span></span>

## <a name="assigning-users-to-concur"></a><span data-ttu-id="37243-110">Kullanıcılar için Concur atama</span><span class="sxs-lookup"><span data-stu-id="37243-110">Assigning users to Concur</span></span>

<span data-ttu-id="37243-111">Azure Active Directory "atamaları" adlı bir kavram hangi kullanıcıların seçili uygulamalara erişim alması belirlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="37243-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="37243-112">Otomatik olarak bir kullanıcı hesabı sağlama bağlamında, yalnızca kullanıcıların ve grupların "Azure AD uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="37243-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="37243-113">Yapılandırma ve sağlama hizmeti etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD grupları Concur uygulamanıza erişimi olması gereken kullanıcılar temsil eden karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="37243-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Concur app.</span></span> <span data-ttu-id="37243-114">Karar sonra buradaki yönergeleri izleyerek, bu kullanıcılar Concur uygulamanıza atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="37243-114">Once decided, you can assign these users to your Concur app by following the instructions here:</span></span>

[<span data-ttu-id="37243-115">Bir kullanıcı veya grup için bir kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="37243-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-concur"></a><span data-ttu-id="37243-116">Kullanıcılar için Concur atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="37243-116">Important tips for assigning users to Concur</span></span>

*   <span data-ttu-id="37243-117">Önerilir tek bir Azure AD kullanıcısının sağlama yapılandırmayı test etmek için Concur atanabilir.</span><span class="sxs-lookup"><span data-stu-id="37243-117">It is recommended that a single Azure AD user be assigned to Concur to test the provisioning configuration.</span></span> <span data-ttu-id="37243-118">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="37243-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="37243-119">Bir kullanıcı için Concur atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="37243-119">When assigning a user to Concur, you must select a valid user role.</span></span> <span data-ttu-id="37243-120">"Varsayılan erişim" rolü sağlama için çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="37243-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="37243-121">Kullanıcı sağlamayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="37243-121">Enable user provisioning</span></span>

<span data-ttu-id="37243-122">Bu bölümde Azure AD Concur'ın kullanıcı hesabına API sağlama konusunda size rehberlik eder ve oluşturmak için sağlama hizmeti yapılandırma güncelleştirin ve Azure AD'de kullanıcı ve grup atama göre Concur atanan kullanıcı hesaplarında devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="37243-122">This section guides you through connecting your Azure AD to Concur's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span></span>

> [!Tip] 
> <span data-ttu-id="37243-123">Da tercih edebilirsiniz etkin SAML tabanlı çoklu oturum açma için Concur, yönergeleri izleyerek sağlanan [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="37243-123">You may also choose to enabled SAML-based Single Sign-On for Concur, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="37243-124">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="37243-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="37243-125">Kullanıcı hesabı sağlama yapılandırmak için:</span><span class="sxs-lookup"><span data-stu-id="37243-125">To configure user account provisioning:</span></span>

<span data-ttu-id="37243-126">Bu bölümün amacı, Active Directory kullanıcı hesaplarının Concur sağlama etkinleştirme anahat sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="37243-126">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Concur.</span></span>

<span data-ttu-id="37243-127">Var. harcama hizmet uygulamalarda etkinleştirmek için uygun Kurulum ve kullanım Web Hizmeti Yönetim profilinin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="37243-127">To enable apps in the Expense Service, there has to be proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="37243-128">WS yönetici rolünü, T & E yönetim işlevleri için kullandığınız varolan yönetici profilinizin eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="37243-128">Don't add the WS Admin role to your existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="37243-129">Danışmanlar concur veya istemci Yöneticisi ayrı bir Web hizmeti yönetici profili oluşturmanız gerekir ve istemci Yöneticisi bu profil için Web Services Yöneticisi işlevleri (örneğin, etkinleştirme uygulamalar) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="37243-129">Concur Consultants or the client administrator must create a distinct Web Service Administrator profile and the Client administrator must use this profile for the Web Services Administrator functions (for example, enabling apps).</span></span> <span data-ttu-id="37243-130">Bu profiller (T & E yönetim profili atanan WSAdmin rolü olmamalıdır) istemci yöneticinin günlük T & E yönetici profilinden ayrı tutulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="37243-130">These profiles must be kept separate from the client administrator's daily T&E admin profile (the T&E admin profile should not have the WSAdmin role assigned).</span></span>

<span data-ttu-id="37243-131">Uygulama etkinleştirmek için kullanılacak profili oluşturduğunuzda, istemci yöneticinin adı kullanıcı profili alanlarına girin.</span><span class="sxs-lookup"><span data-stu-id="37243-131">When you create the profile to be used for enabling the app, enter the client administrator's name into the user profile fields.</span></span> <span data-ttu-id="37243-132">Bu profile sahipliği atar.</span><span class="sxs-lookup"><span data-stu-id="37243-132">This assigns ownership to the profile.</span></span> <span data-ttu-id="37243-133">Bir veya daha fazla profil oluşturulur sonra istemci tıklatın için bu profili ile oturum açmanız gerekir "*etkinleştirmek*" düğmesi için bir iş ortağı uygulama Web Hizmetleri menü içinde.</span><span class="sxs-lookup"><span data-stu-id="37243-133">Once one or more profiles is created, the client must log in with this profile to click the "*Enable*" button for a Partner App within the Web Services menu.</span></span>

<span data-ttu-id="37243-134">Aşağıdaki nedenlerle Bu eylem normal T & E Yönetim için kullandıkları profille yapılmalıdır değil.</span><span class="sxs-lookup"><span data-stu-id="37243-134">For the following reasons, this action should not be done with the profile they use for normal T&E administration.</span></span>

* <span data-ttu-id="37243-135">İstemci tıklar biri olması gerekir "*Evet*" uygulama etkinleştirildikten sonra görüntülenen iletişim penceresinde.</span><span class="sxs-lookup"><span data-stu-id="37243-135">The client has to be the one that clicks "*Yes*" on the dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="37243-136">Bu, istemci, veya iş ortağı bu Evet düğmesini tıklatın edilemez şekilde kendi verilere erişmek iş ortağı uygulamasını için istekli olup bildirir.</span><span class="sxs-lookup"><span data-stu-id="37243-136">This click acknowledges the client is willing for the Partner application to access their data, so you or the Partner cannot click that Yes button.</span></span>

* <span data-ttu-id="37243-137">Bir uygulama etkinleştirilmiş bir istemci yönetici T & E yönetici profili (devre profilinde kaynaklanan) şirket olan, uygulama ile başka bir etkin WS yönetim profili etkinleştirilene kadar profili çalışmaz etkinleştirilmiş uygulamalardan bırakır.</span><span class="sxs-lookup"><span data-stu-id="37243-137">If a client administrator that has enabled an app using the T&E admin profile leaves the company (resulting in the profile being inactivated), any apps enabled using that profile does not function until the app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="37243-138">Ayrı WS yönetim profilleri oluşturmak için beklenen nedeni budur.</span><span class="sxs-lookup"><span data-stu-id="37243-138">This is why you are supposed to create distinct WS Admin profiles.</span></span>

* <span data-ttu-id="37243-139">Bir yönetici şirketten ayrılması durumunda WS yönetim profiline ilişkili adı etkilemeden bu profili gerek yoktur çünkü etkin uygulama devre isterseniz değiştirme yönetici değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="37243-139">If an administrator leaves the company, the name associated to the WS Admin profile can be changed to the replacement administrator if desired without impacting the enabled app because that profile does not need inactivated.</span></span>

<span data-ttu-id="37243-140">**Kullanıcı sağlamayı yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="37243-140">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="37243-141">Oturum, **Concur** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="37243-141">Log on to your **Concur** tenant.</span></span>

2. <span data-ttu-id="37243-142">Gelen **Yönetim** menüsünde, select **Web Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="37243-142">From the **Administration** menu, select **Web Services**.</span></span>
   
    <span data-ttu-id="37243-143">![Concur kiracısı](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur kiracısı")</span><span class="sxs-lookup"><span data-stu-id="37243-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span></span>

3. <span data-ttu-id="37243-144">Sol taraftaki gelen **Web Hizmetleri** bölmesinde, **iş ortağı uygulamasını etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="37243-144">On the left side, from the **Web Services** pane, select **Enable Partner Application**.</span></span>
   
    <span data-ttu-id="37243-145">![İş ortağı uygulamasını etkinleştir](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "iş ortağı uygulamasını etkinleştir")</span><span class="sxs-lookup"><span data-stu-id="37243-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span></span>

4. <span data-ttu-id="37243-146">Gelen **etkinleştirmek uygulama** listesinde **Azure Active Directory**ve ardından **etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="37243-146">From the **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
    <span data-ttu-id="37243-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="37243-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span></span>

5. <span data-ttu-id="37243-148">Tıklatın **Evet** kapatmak için **eylemi onaylayın** iletişim.</span><span class="sxs-lookup"><span data-stu-id="37243-148">Click **Yes** to close the **Confirm Action** dialog.</span></span>
   
    <span data-ttu-id="37243-149">![Eylemi onaylamak](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "eylemi onaylayın")</span><span class="sxs-lookup"><span data-stu-id="37243-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span></span>

6. <span data-ttu-id="37243-150">İçinde [Azure portal](https://portal.azure.com), Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="37243-150">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

7. <span data-ttu-id="37243-151">Çoklu oturum açma için Concur zaten yapılandırdıysanız arama alanı kullanarak Concur Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="37243-151">If you have already configured Concur for single sign-on, search for your instance of Concur using the search field.</span></span> <span data-ttu-id="37243-152">Aksi takdirde seçin **Ekle** arayın ve **Concur** uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="37243-152">Otherwise, select **Add** and search for **Concur** in the application gallery.</span></span> <span data-ttu-id="37243-153">Arama sonuçlarından Concur seçin ve uygulamaları listenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="37243-153">Select Concur from the search results, and add it to your list of applications.</span></span>

8. <span data-ttu-id="37243-154">Concur örneğiniz seçin ve ardından **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="37243-154">Select your instance of Concur, then select the **Provisioning** tab.</span></span>

9. <span data-ttu-id="37243-155">Ayarlama **sağlama modunda** için **otomatik**.</span><span class="sxs-lookup"><span data-stu-id="37243-155">Set the **Provisioning Mode** to **Automatic**.</span></span> 
 
    ![Sağlama](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. <span data-ttu-id="37243-157">Altında **yönetici kimlik bilgileri** bölümünde, girin **kullanıcı adı** ve **parola** Concur yöneticinizin.</span><span class="sxs-lookup"><span data-stu-id="37243-157">Under the **Admin Credentials** section, enter the **user name** and the **password** of your Concur administrator.</span></span>

11. <span data-ttu-id="37243-158">Azure portalında tıklatın **Bağlantıyı Sına** Azure emin olmak için AD Concur uygulamanıza bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="37243-158">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Concur app.</span></span> <span data-ttu-id="37243-159">Bağlantı başarısız olursa Concur hesabınızın Team yönetici izinleri olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="37243-159">If the connection fails, ensure your Concur account has Team Admin permissions.</span></span>

12. <span data-ttu-id="37243-160">Bir kişi veya sağlama hata bildirimleri alması gereken Grup e-posta adresini girin **bildirim e-posta** alan ve onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="37243-160">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

13. <span data-ttu-id="37243-161">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="37243-161">Click **Save.**</span></span>

14. <span data-ttu-id="37243-162">Eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları Concur.**</span><span class="sxs-lookup"><span data-stu-id="37243-162">Under the Mappings section, select **Synchronize Azure Active Directory Users to Concur.**</span></span>

15. <span data-ttu-id="37243-163">İçinde **öznitelik eşlemelerini** bölümünde, Concur için Azure AD'den eşitlenen kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="37243-163">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Concur.</span></span> <span data-ttu-id="37243-164">Seçilen öznitelikler **eşleşen** özellikleri Concur kullanıcı hesaplarında güncelleştirme işlemleri için eşleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="37243-164">The attributes selected as **Matching** properties are used to match the user accounts in Concur for update operations.</span></span> <span data-ttu-id="37243-165">Değişiklikleri kaydetmek için Kaydet düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="37243-165">Select the Save button to commit any changes.</span></span>

16. <span data-ttu-id="37243-166">Azure AD hizmeti Concur için sağlama etkinleştirmek için değiştirmek **sağlama durumu** için **üzerinde** içinde **ayarları** bölümü</span><span class="sxs-lookup"><span data-stu-id="37243-166">To enable the Azure AD provisioning service for Concur, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

17. <span data-ttu-id="37243-167">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="37243-167">Click **Save.**</span></span>

<span data-ttu-id="37243-168">Şimdi sınama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37243-168">You can now create a test account.</span></span> <span data-ttu-id="37243-169">Hesap için Concur eşitlendiğinden emin doğrulamak için en çok 20 dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="37243-169">Wait for up to 20 minutes to verify that the account has been synchronized to Concur.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37243-170">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="37243-170">Additional resources</span></span>

* [<span data-ttu-id="37243-171">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="37243-171">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="37243-172">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="37243-172">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="37243-173">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="37243-173">Configure Single Sign-on</span></span>](active-directory-saas-concur-tutorial.md)

