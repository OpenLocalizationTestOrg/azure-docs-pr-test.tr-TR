---
title: "Öğretici: Salesforce korumalı alan Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve Salesforce korumalı alan arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bab73fda-6754-411d-9288-f73ecdaa486d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 7d3c655a754f83284c386d2007c604a731367814
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-salesforce-sandbox-for-automatic-user-provisioning"></a><span data-ttu-id="2f570-103">Öğretici: Salesforce korumalı alan otomatik kullanıcı sağlamayı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2f570-103">Tutorial: Configuring Salesforce Sandbox for Automatic User Provisioning</span></span>

<span data-ttu-id="2f570-104">Bu öğreticinin amacı Salesforce korumalı alan ve Azure AD otomatik olarak sağlamak ve kullanıcı hesaplarına Azure AD'den Salesforce korumalı alan sağlanmasını gerçekleştirmek için gereken adımları Göster sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="2f570-104">The objective of this tutorial is to show you the steps you need to perform in Salesforce Sandbox and Azure AD to automatically provision and de-provision user accounts from Azure AD to Salesforce Sandbox.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f570-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2f570-105">Prerequisites</span></span>

<span data-ttu-id="2f570-106">Bu öğreticide gösterilen senaryo, aşağıdaki öğeleri zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="2f570-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="2f570-107">Bir Azure Active directory kiracısı.</span><span class="sxs-lookup"><span data-stu-id="2f570-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="2f570-108">Salesforce korumalı alan için iş veya eğitim için Salesforce korumalı alan için geçerli bir kiracı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f570-108">You must have a valid tenant for Salesforce Sandbox for Work or Salesforce Sandbox for Education.</span></span> <span data-ttu-id="2f570-109">Ücretsiz bir deneme hesabı ya da hizmet için kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="2f570-109">You may use a free trial     account for either service.</span></span>
*   <span data-ttu-id="2f570-110">Salesforce korumalı alan takım yönetici izinlerine sahip bir kullanıcı hesabının.</span><span class="sxs-lookup"><span data-stu-id="2f570-110">A user account in Salesforce Sandbox with Team Admin permissions.</span></span>

## <a name="assigning-users-to-salesforce-sandbox"></a><span data-ttu-id="2f570-111">Salesforce korumalı alan kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="2f570-111">Assigning users to Salesforce Sandbox</span></span>

<span data-ttu-id="2f570-112">Azure Active Directory "atamaları" adlı bir kavram hangi kullanıcıların seçili uygulamalara erişim alması belirlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="2f570-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="2f570-113">Otomatik olarak bir kullanıcı hesabı sağlama bağlamında, yalnızca kullanıcıların ve grupların "Azure AD uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="2f570-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="2f570-114">Yapılandırma ve sağlama hizmeti etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD grupları Salesforce korumalı uygulamanıza erişmek isteyen kullanıcılar temsil eden karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f570-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Salesforce Sandbox app.</span></span> <span data-ttu-id="2f570-115">Karar sonra buradaki yönergeleri izleyerek, bu kullanıcılar Salesforce korumalı alan uygulamanıza atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2f570-115">Once decided, you can assign these users to your Salesforce Sandbox app by following the instructions here:</span></span>

[<span data-ttu-id="2f570-116">Bir kullanıcı veya grup için bir kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="2f570-116">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-salesforce-sandbox"></a><span data-ttu-id="2f570-117">Salesforce korumalı alan kullanıcılara atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="2f570-117">Important tips for assigning users to Salesforce Sandbox</span></span>

* <span data-ttu-id="2f570-118">Önerilir tek bir Azure AD kullanıcısının sağlama yapılandırmayı test etmek için Salesforce korumalı alan atanır.</span><span class="sxs-lookup"><span data-stu-id="2f570-118">It is recommended that a single Azure AD user is assigned to Salesforce Sandbox to test the provisioning configuration.</span></span> <span data-ttu-id="2f570-119">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="2f570-119">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="2f570-120">Bir kullanıcı için Salesforce korumalı alan atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f570-120">When assigning a user to Salesforce Sandbox, you must select a valid user role.</span></span> <span data-ttu-id="2f570-121">"Varsayılan erişim" rolü sağlama için çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="2f570-121">The "Default Access" role does not work for provisioning.</span></span>

> [!NOTE]
> <span data-ttu-id="2f570-122">Bu uygulama özel roller Salesforce korumalı alan müşteri kullanıcılar atarken seçmek isteyebilirsiniz sağlama işleminin bir parçası olarak alır.</span><span class="sxs-lookup"><span data-stu-id="2f570-122">This app imports custom roles from Salesforce Sandbox as part of the provisioning process, which the customer may want to select when assigning users.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="2f570-123">Otomatik kullanıcı sağlamayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="2f570-123">Enable Automated User Provisioning</span></span>

<span data-ttu-id="2f570-124">Bu bölümde Azure AD Salesforce korumalı alanın kullanıcı hesabına API sağlama konusunda size rehberlik eder ve oluşturmak için sağlama hizmeti yapılandırma güncelleştirmek ve Azure AD'de kullanıcı ve grup atama Salesforce korumalı alan hesaplarında dayalı atanan kullanıcı devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="2f570-124">This section guides you through connecting your Azure AD to Salesforce Sandbox's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Salesforce Sandbox based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="2f570-125">Da tercih edebilirsiniz etkin SAML tabanlı çoklu oturum açma için Salesforce korumalı alan, yönergeleri izleyerek sağlanan [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2f570-125">You may also choose to enabled SAML-based Single Sign-On for Salesforce Sandbox, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2f570-126">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="2f570-126">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="2f570-127">Otomatik olarak bir kullanıcı hesabı sağlama yapılandırmak için:</span><span class="sxs-lookup"><span data-stu-id="2f570-127">To configure automatic user account provisioning:</span></span>

<span data-ttu-id="2f570-128">Bu bölümün amacı Salesforce korumalı alan Active Directory kullanıcı hesaplarının kullanıcı sağlamayı etkinleştirme anahat sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="2f570-128">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce Sandbox.</span></span>

1. <span data-ttu-id="2f570-129">İçinde [Azure portal](https://portal.azure.com), Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="2f570-129">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="2f570-130">Çoklu oturum açma için Salesforce korumalı alan zaten yapılandırdıysanız arama alanı kullanarak Salesforce korumalı alan Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="2f570-130">If you have already configured Salesforce Sandbox for single sign-on, search for your instance of Salesforce Sandbox using the search field.</span></span> <span data-ttu-id="2f570-131">Aksi takdirde seçin **Ekle** arayın ve **Salesforce korumalı alan** uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="2f570-131">Otherwise, select **Add** and search for **Salesforce Sandbox** in the application gallery.</span></span> <span data-ttu-id="2f570-132">Arama sonuçlarından Salesforce korumalı alan seçin ve uygulamaları listenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2f570-132">Select Salesforce Sandbox from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="2f570-133">Salesforce korumalı alan örneğiniz seçin ve ardından **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="2f570-133">Select your instance of Salesforce Sandbox, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="2f570-134">Ayarlama **sağlama modunda** için **otomatik**.</span><span class="sxs-lookup"><span data-stu-id="2f570-134">Set the **Provisioning Mode** to **Automatic**.</span></span> 
    <span data-ttu-id="2f570-135">![sağlama](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/provisioning.png)</span><span class="sxs-lookup"><span data-stu-id="2f570-135">![provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/provisioning.png)</span></span>

5. <span data-ttu-id="2f570-136">Altında **yönetici kimlik bilgileri** bölümünde, aşağıdaki yapılandırma ayarları sağlar:</span><span class="sxs-lookup"><span data-stu-id="2f570-136">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="2f570-137">a.</span><span class="sxs-lookup"><span data-stu-id="2f570-137">a.</span></span> <span data-ttu-id="2f570-138">İçinde **yönetici kullanıcı adı** metin kutusuna, Salesforce korumalı alan adı hesap türü **Sistem Yöneticisi** atanan Salesforce.com profilinde.</span><span class="sxs-lookup"><span data-stu-id="2f570-138">In the **Admin User Name** textbox, type a Salesforce Sandbox account name that has the **System Administrator** profile in Salesforce.com assigned.</span></span>
   
    <span data-ttu-id="2f570-139">b.</span><span class="sxs-lookup"><span data-stu-id="2f570-139">b.</span></span> <span data-ttu-id="2f570-140">İçinde **yönetici parolası** metin kutusuna, bu hesabın parolasını yazın.</span><span class="sxs-lookup"><span data-stu-id="2f570-140">In the **Admin Password** textbox, type the password for this account.</span></span>

6. <span data-ttu-id="2f570-141">Salesforce korumalı alan güvenlik belirtecini almak için aynı Salesforce korumalı alan yönetici dikkate yeni sekmede ve oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2f570-141">To get your Salesforce Sandbox security token, open a new tab and sign into the same Salesforce Sandbox admin account.</span></span> <span data-ttu-id="2f570-142">Sayfanın sağ üst köşesinde adınıza tıklayın ve ardından **My ayarları**.</span><span class="sxs-lookup"><span data-stu-id="2f570-142">On the top right corner of the page, click your name, and then click **My Settings**.</span></span>

     <span data-ttu-id="2f570-143">![Otomatik kullanıcı sağlamayı etkinleştirin](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "otomatik kullanıcı sağlamayı etkinleştirin")</span><span class="sxs-lookup"><span data-stu-id="2f570-143">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span></span>
7. <span data-ttu-id="2f570-144">Sol gezinti bölmesinde tıklatın **kişisel** ilgili bölümü genişletin ve ardından **sıfırlama My güvenlik belirteci**.</span><span class="sxs-lookup"><span data-stu-id="2f570-144">On the left navigation pane, click **Personal** to expand the related section, and then click **Reset My Security Token**.</span></span>
  
    <span data-ttu-id="2f570-145">![Otomatik kullanıcı sağlamayı etkinleştirin](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "otomatik kullanıcı sağlamayı etkinleştirin")</span><span class="sxs-lookup"><span data-stu-id="2f570-145">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span></span>
8. <span data-ttu-id="2f570-146">Üzerinde **sıfırlama My güvenlik belirteci** sayfasında, **güvenlik belirteci sıfırlama** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2f570-146">On the **Reset My Security Token** page, click the **Reset Security Token** button.</span></span>

    <span data-ttu-id="2f570-147">![Otomatik kullanıcı sağlamayı etkinleştirin](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "otomatik kullanıcı sağlamayı etkinleştirin")</span><span class="sxs-lookup"><span data-stu-id="2f570-147">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span></span>
9. <span data-ttu-id="2f570-148">Bu Yönetici hesabınızla ilişkili e-posta gelen kutusunu kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="2f570-148">Check the email inbox associated with this admin account.</span></span> <span data-ttu-id="2f570-149">Salesforce Sandbox.com yeni güvenlik belirteci içeren bir e-posta için bakın.</span><span class="sxs-lookup"><span data-stu-id="2f570-149">Look for an email from Salesforce Sandbox.com that contains the new security token.</span></span>
10. <span data-ttu-id="2f570-150">Belirteç kopyalama, Azure AD penceresine gidin ve yapıştırın **yuva belirteci** alan.</span><span class="sxs-lookup"><span data-stu-id="2f570-150">Copy the token, go to your Azure AD window, and paste it into the **Socket Token** field.</span></span>

11. <span data-ttu-id="2f570-151">Azure portalında tıklatın **Bağlantıyı Sına** Azure emin olmak için AD Salesforce korumalı alan uygulamanıza bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="2f570-151">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Salesforce Sandbox app.</span></span>

12. <span data-ttu-id="2f570-152">İçinde **bildirim e-posta** alan, bir kişi veya grubun sağlama hata bildirimleri almak ve gerekir onay e-posta adresini girin.</span><span class="sxs-lookup"><span data-stu-id="2f570-152">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span></span>

13. <span data-ttu-id="2f570-153">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="2f570-153">Click **Save.**</span></span>  
    
14.  <span data-ttu-id="2f570-154">Eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları Salesforce korumalı alan için.**</span><span class="sxs-lookup"><span data-stu-id="2f570-154">Under the Mappings section, select **Synchronize Azure Active Directory Users to Salesforce Sandbox.**</span></span>

15. <span data-ttu-id="2f570-155">İçinde **öznitelik eşlemelerini** bölümünde, Salesforce korumalı alan için Azure AD'den eşitlenen kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="2f570-155">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Salesforce Sandbox.</span></span> <span data-ttu-id="2f570-156">Seçilen öznitelikler **eşleşen** özellikleri Salesforce korumalı alan kullanıcı hesaplarında güncelleştirme işlemleri için eşleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2f570-156">The attributes selected as **Matching** properties are used to match the user accounts in Salesforce Sandbox for update operations.</span></span> <span data-ttu-id="2f570-157">Değişiklikleri kaydetmek için Kaydet düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="2f570-157">Select the Save button to commit any changes.</span></span>

16. <span data-ttu-id="2f570-158">Salesforce korumalı alan için hizmet sağlama Azure AD etkinleştirmek için değiştirmek **sağlama durumu** için **üzerinde** ayarları bölümünde</span><span class="sxs-lookup"><span data-stu-id="2f570-158">To enable the Azure AD provisioning service for Salesforce Sandbox, change the **Provisioning Status** to **On** in the Settings section</span></span>

17. <span data-ttu-id="2f570-159">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="2f570-159">Click **Save.**</span></span>


<span data-ttu-id="2f570-160">Herhangi bir kullanıcı ve/veya Salesforce korumalı alan kullanıcılar ve Gruplar bölümünde atanan grupları ilk eşitleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="2f570-160">It starts the initial synchronization of any users and/or groups assigned to Salesforce Sandbox in the Users and Groups section.</span></span> <span data-ttu-id="2f570-161">İlk eşitleme gerçekleştirmek yaklaşık 20 dakikada çalıştığı sürece oluşan sonraki eşitlemeler uzun sürer.</span><span class="sxs-lookup"><span data-stu-id="2f570-161">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="2f570-162">Kullanabileceğiniz **eşitleme ayrıntıları** bölüm ilerlemeyi izlemek ve Salesforce korumalı alan uygulama sağlama hizmeti tarafından gerçekleştirilen tüm eylemler açıklanmaktadır etkinlik raporları sağlamak için bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="2f570-162">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on Salesforce Sandbox app.</span></span>

<span data-ttu-id="2f570-163">Şimdi sınama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f570-163">You can now create a test account.</span></span> <span data-ttu-id="2f570-164">Hesap salesforce eşitlendiğinden emin doğrulamak için en çok 20 dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="2f570-164">Wait for up to 20 minutes to verify that the account has been synchronized to salesforce.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2f570-165">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2f570-165">Additional resources</span></span>

* [<span data-ttu-id="2f570-166">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="2f570-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2f570-167">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="2f570-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="2f570-168">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="2f570-168">Configure Single Sign-on</span></span>](active-directory-saas-salesforcesandbox-tutorial.md)