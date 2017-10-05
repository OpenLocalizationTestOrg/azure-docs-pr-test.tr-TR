---
title: "Öğretici: Azure Active Directory Tümleştirme ile çalışma alanına Facebook tarafından | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve Facebook ile çalışma alanına arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 9b22679c304248ed7ba7a6bd9eaf82b64f7143cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="ee0a3-103">Öğretici: Kullanıcı sağlamak için çalışma alanına Facebook ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ee0a3-103">Tutorial: Configuring Workplace by Facebook for User Provisioning</span></span>

<span data-ttu-id="ee0a3-104">Bu öğreticinin amacı, Facebook ve Azure AD otomatik olarak sağlamak ve Azure AD kullanıcı hesaplarından çalışma Facebook tarafından sağlanmasını tarafından çalışma gerçekleştirmek için gereken adımları Göster sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-104">The objective of this tutorial is to show you the steps you need to perform in Workplace by Facebook and Azure AD to automatically provision and de-provision user accounts from Azure AD to Workplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee0a3-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ee0a3-105">Prerequisites</span></span>

<span data-ttu-id="ee0a3-106">Facebook ile çalışma alanına ile Azure AD tümleştirme yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="ee0a3-106">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="ee0a3-107">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="ee0a3-107">An Azure AD subscription</span></span>
- <span data-ttu-id="ee0a3-108">Facebook çoklu oturum açma etkin abonelik tarafından bir çalışma alanı</span><span class="sxs-lookup"><span data-stu-id="ee0a3-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ee0a3-109">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-109">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ee0a3-110">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ee0a3-110">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ee0a3-111">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ee0a3-112">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ee0a3-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="ee0a3-113">Kullanıcıların Facebook ile çalışma alanına atama</span><span class="sxs-lookup"><span data-stu-id="ee0a3-113">Assigning users to Workplace by Facebook</span></span>

<span data-ttu-id="ee0a3-114">Azure Active Directory "atamaları" adlı bir kavram hangi kullanıcıların seçili uygulamalara erişim alması belirlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-114">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="ee0a3-115">Otomatik olarak bir kullanıcı hesabı sağlama bağlamında, yalnızca kullanıcıların ve grupların "Azure AD uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-115">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="ee0a3-116">Yapılandırma ve sağlama hizmeti etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD grupları Facebook uygulama tarafından işyeriniz erişmek isteyen kullanıcıların temsil eden karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-116">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Workplace by Facebook app.</span></span> <span data-ttu-id="ee0a3-117">Karar sonra bu kullanıcılar çalışma alanınıza Facebook uygulama tarafından Buradaki yönergeleri izleyerek atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ee0a3-117">Once decided, you can assign these users to your Workplace by Facebook app by following the instructions here:</span></span>

[<span data-ttu-id="ee0a3-118">Bir kullanıcı veya grup için bir kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="ee0a3-118">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="ee0a3-119">Facebook ile çalışma alanına kullanıcılara atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="ee0a3-119">Important tips for assigning users to Workplace by Facebook</span></span>

*   <span data-ttu-id="ee0a3-120">Önerilir tek bir Azure AD kullanıcısının atanması çalışma alanına Facebook tarafından sağlama yapılandırmayı test etme.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-120">It is recommended that a single Azure AD user is assigned to Workplace by Facebook to test the provisioning configuration.</span></span> <span data-ttu-id="ee0a3-121">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="ee0a3-122">Bir kullanıcı için çalışma alanına Facebook tarafından atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-122">When assigning a user to Workplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="ee0a3-123">"Varsayılan erişim" rolü sağlama için çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-123">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="ee0a3-124">Kullanıcı sağlamayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="ee0a3-124">Enable User Provisioning</span></span>

<span data-ttu-id="ee0a3-125">Bu bölümde API sağlama Facebook'ın kullanıcı hesabı tarafından Azure AD çalışma alanına konusunda size rehberlik eder ve oluşturmak için sağlama hizmeti yapılandırma güncelleştirin ve çalışma Azure AD'de kullanıcı ve grup atama göre Facebook tarafından atanan kullanıcı hesapları devre dışı bırak.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-125">This section guides you through connecting your Azure AD to Workplace by Facebook's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="ee0a3-126">Da tercih edebilirsiniz etkin SAML tabanlı çoklu oturum açma Facebook tarafından çalışma alanı için yönergeleri izleyerek sağlanan [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ee0a3-126">You may also choose to enabled SAML-based Single Sign-On for Workplace by Facebook, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ee0a3-127">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning-to-workplace-by-facebook-in-azure-ad"></a><span data-ttu-id="ee0a3-128">Kullanıcı hesap için çalışma alanına Facebook tarafından Azure AD'de sağlama yapılandırmak için:</span><span class="sxs-lookup"><span data-stu-id="ee0a3-128">To configure user account provisioning to Workplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="ee0a3-129">Bu bölümün amacı, Active Directory kullanıcı hesapları için çalışma alanına Facebook tarafından sağlanmasını etkinleştirme anahat sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-129">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Workplace by Facebook.</span></span>

<span data-ttu-id="ee0a3-130">Azure AD çalışma alanına Facebook tarafından atanan kullanıcı hesabı ayrıntıları otomatik olarak eşitleme özelliği destekler.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-130">Azure AD supports the ability to automatically synchronize the account details of assigned users to Workplace by Facebook.</span></span> <span data-ttu-id="ee0a3-131">Bu otomatik eşitleme ilk kez oturum açmaya önlerinde erişim için Kullanıcıları yetkilendirmek için gereken verileri almak için Facebook ile çalışma alanına sağlar.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-131">This automatic synchronization enables Workplace by Facebook to get the data it needs to authorize users for access, before them attempting to sign in for the first time.</span></span> <span data-ttu-id="ee0a3-132">Erişim Azure AD'de iptal edilmiş durumda olduğunda, ayrıca çalışma alanına Facebook tarafından kullanıcılardan XML'deki sağlamasını yapar.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="ee0a3-133">İçinde [Azure portal](https://portal.azure.com), Gözat **Azure Active Directory** > **Kurumsal uygulamaları** > **tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-133">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="ee0a3-134">Çoklu oturum açma için Facebook ile çalışma alanına zaten yapılandırdıysanız arama alanı kullanarak Facebook ile çalışma alanına örneğiniz arayın.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using the search field.</span></span> <span data-ttu-id="ee0a3-135">Aksi takdirde seçin **Ekle** arayın ve **Facebook ile çalışma alanına** uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-135">Otherwise, select **Add** and search for **Workplace by Facebook** in the application gallery.</span></span> <span data-ttu-id="ee0a3-136">Arama sonuçlarından Facebook tarafından çalışma alanı seçin ve uygulamaları listenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-136">Select Workplace by Facebook from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="ee0a3-137">Facebook ile çalışma alanına örneğiniz seçin, sonra seçin **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-137">Select your instance of Workplace by Facebook, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="ee0a3-138">Ayarlama **sağlama modunda** için **otomatik**.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-138">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![Sağlama](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="ee0a3-140">Altında **yönetici kimlik bilgileri** bölümünde, gizli belirteci ve işyeriniz Facebook yönetici tarafından Kiracı URL'sini girin.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-140">Under the **Admin Credentials** section, enter the Secret Token and the Tenant URL of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="ee0a3-141">Azure portalında tıklatın **Bağlantıyı Sına** Azure emin olmak için AD çalışma alanına Facebook uygulaması tarafından bağlanabilirler.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-141">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Workplace by Facebook app.</span></span> <span data-ttu-id="ee0a3-142">Bağlantı başarısız olursa işyeriniz Facebook hesabına göre takım yönetici izinleri olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-142">If the connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="ee0a3-143">Bir kişi veya sağlama hata bildirimleri alması gereken Grup e-posta adresini girin **bildirim e-posta** alan ve onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-143">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

8. <span data-ttu-id="ee0a3-144">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="ee0a3-144">Click **Save.**</span></span>

9. <span data-ttu-id="ee0a3-145">Eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları Facebook ile çalışma.**</span><span class="sxs-lookup"><span data-stu-id="ee0a3-145">Under the Mappings section, select **Synchronize Azure Active Directory Users to Workplace by Facebook.**</span></span>

10. <span data-ttu-id="ee0a3-146">İçinde **öznitelik eşlemelerini** bölümünde, Facebook ile eşitlenmiş Azure AD çalışma alanına kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-146">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Workplace by Facebook.</span></span> <span data-ttu-id="ee0a3-147">Seçilen öznitelikler **eşleşen** özellikler kullanılan çalışma alanına kullanıcı hesaplarında eşleştirmek için Facebook tarafından güncelleştirme işlemleri için.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-147">The attributes selected as **Matching** properties are used to match the user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="ee0a3-148">Değişiklikleri kaydetmek için Kaydet düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-148">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="ee0a3-149">Azure AD çalışma alanına Facebook tarafından hizmet sağlama etkinleştirmek için değiştirmek **sağlama durumu** için **üzerinde** içinde **ayarları** bölümü</span><span class="sxs-lookup"><span data-stu-id="ee0a3-149">To enable the Azure AD provisioning service for Workplace by Facebook, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="ee0a3-150">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="ee0a3-150">Click **Save.**</span></span>

<span data-ttu-id="ee0a3-151">Otomatik sağlama yapılandırma hakkında daha fazla bilgi için bkz: [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span><span class="sxs-lookup"><span data-stu-id="ee0a3-151">For more information on how to configure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="ee0a3-152">Şimdi sınama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-152">You can now create a test account.</span></span> <span data-ttu-id="ee0a3-153">Hesap çalışma alanına Facebook ile eşitlendiğinden emin doğrulamak için en çok 20 dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="ee0a3-153">Wait for up to 20 minutes to verify that the account has been synchronized to Workplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ee0a3-154">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ee0a3-154">Additional resources</span></span>

* [<span data-ttu-id="ee0a3-155">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="ee0a3-155">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ee0a3-156">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="ee0a3-156">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ee0a3-157">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="ee0a3-157">Configure Single Sign-on</span></span>](active-directory-saas-workplacebyfacebook-tutorial.md)

