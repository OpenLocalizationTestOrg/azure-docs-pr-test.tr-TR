---
title: "Öğretici: Azure Active Directory Tümleştirme ile Concur | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Concur arasında."
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
ms.openlocfilehash: 13ba364af26a5ce0f1d2b51aaa0f84a4c353b107
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a><span data-ttu-id="ed1a8-103">Öğretici: Yapılandırma Concur kullanıcı sağlamak için</span><span class="sxs-lookup"><span data-stu-id="ed1a8-103">Tutorial: Configuring Concur for User Provisioning</span></span>

<span data-ttu-id="ed1a8-104">Bu öğreticinin Hello hedefi Concur ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooConcur tooperform gereken adımları hello tooshow ' dir.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Concur and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooConcur.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed1a8-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ed1a8-105">Prerequisites</span></span>

<span data-ttu-id="ed1a8-106">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="ed1a8-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="ed1a8-107">Bir Azure Active directory kiracısı.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="ed1a8-108">Bir Concur çoklu oturum açma abonelik etkin.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-108">A Concur single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="ed1a8-109">Concur takım yönetici izinlerine sahip bir kullanıcı hesabının.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-109">A user account in Concur with Team Admin permissions.</span></span>

## <a name="assigning-users-tooconcur"></a><span data-ttu-id="ed1a8-110">Kullanıcıların tooConcur atama</span><span class="sxs-lookup"><span data-stu-id="ed1a8-110">Assigning users tooConcur</span></span>

<span data-ttu-id="ed1a8-111">Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="ed1a8-112">Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="ed1a8-113">Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya tooyour Concur uygulamasına erişmesi Azure AD temsil hello kullanıcılar gruplarında toodecide gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Concur app.</span></span> <span data-ttu-id="ed1a8-114">Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour Concur uygulama atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ed1a8-114">Once decided, you can assign these users tooyour Concur app by following hello instructions here:</span></span>

[<span data-ttu-id="ed1a8-115">Bir kullanıcı veya grup tooan kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="ed1a8-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooconcur"></a><span data-ttu-id="ed1a8-116">Kullanıcıların tooConcur atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="ed1a8-116">Important tips for assigning users tooConcur</span></span>

*   <span data-ttu-id="ed1a8-117">Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooConcur tootest hello atanabilir.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-117">It is recommended that a single Azure AD user be assigned tooConcur tootest hello provisioning configuration.</span></span> <span data-ttu-id="ed1a8-118">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="ed1a8-119">Bir kullanıcı tooConcur atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-119">When assigning a user tooConcur, you must select a valid user role.</span></span> <span data-ttu-id="ed1a8-120">Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="ed1a8-121">Kullanıcı sağlamayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="ed1a8-121">Enable user provisioning</span></span>

<span data-ttu-id="ed1a8-122">Bu bölümde, Azure AD tooConcur kullanıcının kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve Azure AD'de kullanıcı ve grup atama göre Concur atanan kullanıcı hesaplarında devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-122">This section guides you through connecting your Azure AD tooConcur's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span></span>

> [!Tip] 
> <span data-ttu-id="ed1a8-123">Sağlanan hello yönergeleri izleyerek Concur için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ed1a8-123">You may also choose tooenabled SAML-based Single Sign-On for Concur, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ed1a8-124">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="ed1a8-125">tooconfigure kullanıcı hesabı sağlama:</span><span class="sxs-lookup"><span data-stu-id="ed1a8-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="ed1a8-126">Bu bölümde Hello amacı olan toooutline nasıl tooenable Active Directory kullanıcısı sağlama tooConcur hesapları.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-126">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooConcur.</span></span>

<span data-ttu-id="ed1a8-127">tooenable uygulamalarında gider hizmet Merhaba, toobe uygun Kurulum ve kullanım Web Hizmeti Yönetim profili var olan.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-127">tooenable apps in hello Expense Service, there has toobe proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="ed1a8-128">Merhaba, T & E yönetim işlevleri için kullandığınız WS yönetim rolü tooyour mevcut yönetici profili eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-128">Don't add hello WS Admin role tooyour existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="ed1a8-129">Danışmanlar concur veya hello İstemci Yöneticisi ayrı bir Web hizmeti yönetici profili oluşturmanız gerekir ve hello İstemci Yöneticisi bu profili hello Web Services Yöneticisi işlevleri (örneğin, etkinleştirme uygulamalar) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-129">Concur Consultants or hello client administrator must create a distinct Web Service Administrator profile and hello Client administrator must use this profile for hello Web Services Administrator functions (for example, enabling apps).</span></span> <span data-ttu-id="ed1a8-130">Bu profiller hello istemci yöneticinin günlük T & E yönetici profilinden ayrı tutulmalıdır (Merhaba T & E yönetim profili olmamalıdır atanan hello WSAdmin rolü).</span><span class="sxs-lookup"><span data-stu-id="ed1a8-130">These profiles must be kept separate from hello client administrator's daily T&E admin profile (hello T&E admin profile should not have hello WSAdmin role assigned).</span></span>

<span data-ttu-id="ed1a8-131">Merhaba uygulama etkinleştirmek için kullanılan hello profil toobe oluşturduğunuzda, hello kullanıcı profili alanlarına hello istemci yöneticinin adı girin.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-131">When you create hello profile toobe used for enabling hello app, enter hello client administrator's name into hello user profile fields.</span></span> <span data-ttu-id="ed1a8-132">Sahipliği toohello profil atar.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-132">This assigns ownership toohello profile.</span></span> <span data-ttu-id="ed1a8-133">Bir veya daha fazla profil oluşturulduktan sonra hello istemci bu profili tooclick hello oturum açmanız gerekir "*etkinleştirmek*" bir iş ortağı uygulamanın içinden hello Web Hizmetleri menü düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-133">Once one or more profiles is created, hello client must log in with this profile tooclick hello "*Enable*" button for a Partner App within hello Web Services menu.</span></span>

<span data-ttu-id="ed1a8-134">Aşağıdaki nedenlerden hello için bu eylem normal T & E Yönetim için kullandıkları hello profiliyle yapılmalıdır değil.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-134">For hello following reasons, this action should not be done with hello profile they use for normal T&E administration.</span></span>

* <span data-ttu-id="ed1a8-135">Merhaba istemci sahip tıklattığında bir hello toobe "*Evet*" uygulama etkinleştirildikten sonra görüntülenen hello iletişim penceresinde.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-135">hello client has toobe hello one that clicks "*Yes*" on hello dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="ed1a8-136">Bunu siz veya hello iş ortağı Evet düğmesini tıklattıktan olamaz şekilde hello istemci hello iş ortağı uygulama tooaccess için kendi veri istekli bildirir.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-136">This click acknowledges hello client is willing for hello Partner application tooaccess their data, so you or hello Partner cannot click that Yes button.</span></span>

* <span data-ttu-id="ed1a8-137">Merhaba T & E yönetim profili kullanarak bir uygulama etkinleştirilmiş bir istemci Yöneticisi (hello profiline devre kaynaklanan) hello şirketten ayrılırsa, bu profili kullanan etkinleştirilmiş uygulamalardan çalışmaz hello uygulama ile başka bir etkin WS yönetim etkinleştirilene kadar profili.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-137">If a client administrator that has enabled an app using hello T&E admin profile leaves hello company (resulting in hello profile being inactivated), any apps enabled using that profile does not function until hello app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="ed1a8-138">Toocreate ayrı WS yönetim profilleri beklenen nedeni budur.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-138">This is why you are supposed toocreate distinct WS Admin profiles.</span></span>

* <span data-ttu-id="ed1a8-139">Yönetici hello şirketten ayrılması durumunda WS yönetim profili değiştirilen toohello değiştirme yönetici etkin hello etkilemeden bu profili gerek yoktur çünkü uygulama devre isterseniz olabilir toohello ilişkili hello adı.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-139">If an administrator leaves hello company, hello name associated toohello WS Admin profile can be changed toohello replacement administrator if desired without impacting hello enabled app because that profile does not need inactivated.</span></span>

<span data-ttu-id="ed1a8-140">**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ed1a8-140">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed1a8-141">Tooyour üzerinde oturum **Concur** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-141">Log on tooyour **Concur** tenant.</span></span>

2. <span data-ttu-id="ed1a8-142">Merhaba gelen **Yönetim** menüsünde, select **Web Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-142">From hello **Administration** menu, select **Web Services**.</span></span>
   
    <span data-ttu-id="ed1a8-143">![Concur kiracısı](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur kiracısı")</span><span class="sxs-lookup"><span data-stu-id="ed1a8-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span></span>

3. <span data-ttu-id="ed1a8-144">Hello tarafı, sol hello üzerinde **Web Hizmetleri** bölmesinde, **iş ortağı uygulamasını etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-144">On hello left side, from hello **Web Services** pane, select **Enable Partner Application**.</span></span>
   
    <span data-ttu-id="ed1a8-145">![İş ortağı uygulamasını etkinleştir](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "iş ortağı uygulamasını etkinleştir")</span><span class="sxs-lookup"><span data-stu-id="ed1a8-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span></span>

4. <span data-ttu-id="ed1a8-146">Merhaba gelen **etkinleştirmek uygulama** listesinde **Azure Active Directory**ve ardından **etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-146">From hello **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
    <span data-ttu-id="ed1a8-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="ed1a8-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span></span>

5. <span data-ttu-id="ed1a8-148">Tıklatın **Evet** tooclose hello **eylemi onaylayın** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-148">Click **Yes** tooclose hello **Confirm Action** dialog.</span></span>
   
    <span data-ttu-id="ed1a8-149">![Eylemi onaylamak](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "eylemi onaylayın")</span><span class="sxs-lookup"><span data-stu-id="ed1a8-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span></span>

6. <span data-ttu-id="ed1a8-150">Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-150">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

7. <span data-ttu-id="ed1a8-151">Çoklu oturum açma için zaten Concur yapılandırdıysanız, hello arama alanı kullanarak Concur Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-151">If you have already configured Concur for single sign-on, search for your instance of Concur using hello search field.</span></span> <span data-ttu-id="ed1a8-152">Aksi takdirde seçin **Ekle** arayın ve **Concur** hello uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-152">Otherwise, select **Add** and search for **Concur** in hello application gallery.</span></span> <span data-ttu-id="ed1a8-153">Concur hello Arama sonuçlarından seçin ve uygulamaların tooyour listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-153">Select Concur from hello search results, and add it tooyour list of applications.</span></span>

8. <span data-ttu-id="ed1a8-154">Concur örneğiniz seçin ve ardından hello **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-154">Select your instance of Concur, then select hello **Provisioning** tab.</span></span>

9. <span data-ttu-id="ed1a8-155">Set hello **sağlama modu** çok**otomatik**.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-155">Set hello **Provisioning Mode** too**Automatic**.</span></span> 
 
    ![Sağlama](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. <span data-ttu-id="ed1a8-157">Merhaba altında **yönetici kimlik bilgileri** bölümünde, hello girin **kullanıcı adı** ve hello **parola** Concur yöneticinizin.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-157">Under hello **Admin Credentials** section, enter hello **user name** and hello **password** of your Concur administrator.</span></span>

11. <span data-ttu-id="ed1a8-158">Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour Concur uygulama bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-158">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Concur app.</span></span> <span data-ttu-id="ed1a8-159">Merhaba bağlantı başarısız olursa Concur hesabınızın Team yönetici izinleri olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-159">If hello connection fails, ensure your Concur account has Team Admin permissions.</span></span>

12. <span data-ttu-id="ed1a8-160">Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve hello onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-160">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

13. <span data-ttu-id="ed1a8-161">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="ed1a8-161">Click **Save.**</span></span>

14. <span data-ttu-id="ed1a8-162">Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooConcur.**</span><span class="sxs-lookup"><span data-stu-id="ed1a8-162">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooConcur.**</span></span>

15. <span data-ttu-id="ed1a8-163">Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooConcur eşitlenir hello kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-163">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooConcur.</span></span> <span data-ttu-id="ed1a8-164">Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları Concur içinde güncelleştirme işlemleri için özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-164">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Concur for update operations.</span></span> <span data-ttu-id="ed1a8-165">Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-165">Select hello Save button toocommit any changes.</span></span>

16. <span data-ttu-id="ed1a8-166">tooenable hello Concur, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello içinde **ayarları** bölümü</span><span class="sxs-lookup"><span data-stu-id="ed1a8-166">tooenable hello Azure AD provisioning service for Concur, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

17. <span data-ttu-id="ed1a8-167">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="ed1a8-167">Click **Save.**</span></span>

<span data-ttu-id="ed1a8-168">Şimdi sınama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-168">You can now create a test account.</span></span> <span data-ttu-id="ed1a8-169">TooConcur hello hesap tooverify eşitlenmiş too20 dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="ed1a8-169">Wait for up too20 minutes tooverify that hello account has been synchronized tooConcur.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ed1a8-170">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ed1a8-170">Additional resources</span></span>

* [<span data-ttu-id="ed1a8-171">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="ed1a8-171">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ed1a8-172">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="ed1a8-172">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ed1a8-173">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="ed1a8-173">Configure Single Sign-on</span></span>](active-directory-saas-concur-tutorial.md)

