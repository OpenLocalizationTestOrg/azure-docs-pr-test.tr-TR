---
title: "Öğretici: Azure Active Directory Tümleştirme ile Netsuite | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Netsuite arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 277c393536615fc8bfe8af0bc6d487115f04776c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a><span data-ttu-id="40cae-103">Öğretici: Netsuite otomatik kullanıcı sağlamayı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="40cae-103">Tutorial: Configuring Netsuite for Automatic User Provisioning</span></span>

<span data-ttu-id="40cae-104">Bu öğreticinin amacı Netsuite ve Azure AD otomatik olarak sağlamak ve kullanıcı hesaplarına Azure AD'den Netsuite sağlanmasını gerçekleştirmek için gereken adımları Göster sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="40cae-104">The objective of this tutorial is to show you the steps you need to perform in Netsuite and Azure AD to automatically provision and de-provision user accounts from Azure AD to Netsuite.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40cae-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="40cae-105">Prerequisites</span></span>

<span data-ttu-id="40cae-106">Bu öğreticide gösterilen senaryo, aşağıdaki öğeleri zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="40cae-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="40cae-107">Bir Azure Active directory kiracısı.</span><span class="sxs-lookup"><span data-stu-id="40cae-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="40cae-108">Bir Netsuite çoklu oturum açma etkin abonelik.</span><span class="sxs-lookup"><span data-stu-id="40cae-108">A Netsuite single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="40cae-109">Bir kullanıcı hesabında Netsuite takım yönetici izinlerine sahip.</span><span class="sxs-lookup"><span data-stu-id="40cae-109">A user account in Netsuite with Team Admin permissions.</span></span>

## <a name="assigning-users-to-netsuite"></a><span data-ttu-id="40cae-110">Kullanıcılar için Netsuite atama</span><span class="sxs-lookup"><span data-stu-id="40cae-110">Assigning users to Netsuite</span></span>

<span data-ttu-id="40cae-111">Azure Active Directory "atamaları" adlı bir kavram hangi kullanıcıların seçili uygulamalara erişim alması belirlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="40cae-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="40cae-112">Otomatik olarak bir kullanıcı hesabı sağlama bağlamında, yalnızca kullanıcıların ve grupların "Azure AD uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="40cae-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="40cae-113">Yapılandırma ve sağlama hizmeti etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD grupları Netsuite uygulamanıza erişimi olması gereken kullanıcılar temsil eden karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="40cae-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Netsuite app.</span></span> <span data-ttu-id="40cae-114">Karar sonra buradaki yönergeleri izleyerek, bu kullanıcılar Netsuite uygulamanıza atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="40cae-114">Once decided, you can assign these users to your Netsuite app by following the instructions here:</span></span>

[<span data-ttu-id="40cae-115">Bir kullanıcı veya grup için bir kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="40cae-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-netsuite"></a><span data-ttu-id="40cae-116">Kullanıcılar için Netsuite atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="40cae-116">Important tips for assigning users to Netsuite</span></span>

*   <span data-ttu-id="40cae-117">Önerilir tek bir Azure AD kullanıcısının sağlama yapılandırmayı test etmek için Netsuite atanır.</span><span class="sxs-lookup"><span data-stu-id="40cae-117">It is recommended that a single Azure AD user is assigned to Netsuite to test the provisioning configuration.</span></span> <span data-ttu-id="40cae-118">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="40cae-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="40cae-119">Bir kullanıcı için Netsuite atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="40cae-119">When assigning a user to Netsuite, you must select a valid user role.</span></span> <span data-ttu-id="40cae-120">"Varsayılan erişim" rolü sağlama için çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="40cae-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="40cae-121">Kullanıcı sağlamayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="40cae-121">Enable User Provisioning</span></span>

<span data-ttu-id="40cae-122">Bu bölümde Azure AD Netsuite'nın kullanıcı hesabına API sağlama konusunda size rehberlik eder ve oluşturmak için sağlama hizmeti yapılandırma güncelleştirin ve Azure AD'de kullanıcı ve grup atama göre Netsuite atanan kullanıcı hesaplarında devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="40cae-122">This section guides you through connecting your Azure AD to Netsuite's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Netsuite based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="40cae-123">Da tercih edebilirsiniz etkin SAML tabanlı çoklu oturum açma için Netsuite, yönergeleri izleyerek sağlanan [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="40cae-123">You may also choose to enabled SAML-based Single Sign-On for Netsuite, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="40cae-124">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="40cae-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="40cae-125">Kullanıcı hesabı sağlama yapılandırmak için:</span><span class="sxs-lookup"><span data-stu-id="40cae-125">To configure user account provisioning:</span></span>

<span data-ttu-id="40cae-126">Bu bölümün amacı, Active Directory kullanıcı hesaplarının Netsuite kullanıcı sağlamayı etkinleştirme anahat sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="40cae-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Netsuite.</span></span>

1. <span data-ttu-id="40cae-127">İçinde [Azure portal](https://portal.azure.com), Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="40cae-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="40cae-128">Çoklu oturum açma için Netsuite zaten yapılandırdıysanız arama alanı kullanarak Netsuite Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="40cae-128">If you have already configured Netsuite for single sign-on, search for your instance of Netsuite using the search field.</span></span> <span data-ttu-id="40cae-129">Aksi takdirde seçin **Ekle** arayın ve **Netsuite** uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="40cae-129">Otherwise, select **Add** and search for **Netsuite** in the application gallery.</span></span> <span data-ttu-id="40cae-130">Arama sonuçlarından Netsuite seçin ve uygulamaları listenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="40cae-130">Select Netsuite from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="40cae-131">Netsuite örneğiniz seçin ve ardından **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="40cae-131">Select your instance of Netsuite, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="40cae-132">Ayarlama **sağlama modunda** için **otomatik**.</span><span class="sxs-lookup"><span data-stu-id="40cae-132">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![Sağlama](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="40cae-134">Altında **yönetici kimlik bilgileri** bölümünde, aşağıdaki yapılandırma ayarları sağlar:</span><span class="sxs-lookup"><span data-stu-id="40cae-134">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="40cae-135">a.</span><span class="sxs-lookup"><span data-stu-id="40cae-135">a.</span></span> <span data-ttu-id="40cae-136">İçinde **yönetici kullanıcı adı** metin kutusuna, bir Netsuite hesap adı türü **Sistem Yöneticisi** atanan Netsuite.com profilinde.</span><span class="sxs-lookup"><span data-stu-id="40cae-136">In the **Admin User Name** textbox, type a Netsuite account name that has the **System Administrator** profile in Netsuite.com assigned.</span></span>
   
    <span data-ttu-id="40cae-137">b.</span><span class="sxs-lookup"><span data-stu-id="40cae-137">b.</span></span> <span data-ttu-id="40cae-138">İçinde **yönetici parolası** metin kutusuna, bu hesabın parolasını yazın.</span><span class="sxs-lookup"><span data-stu-id="40cae-138">In the **Admin Password** textbox, type the password for this account.</span></span>
      
6. <span data-ttu-id="40cae-139">Azure portalında tıklatın **Bağlantıyı Sına** Azure emin olmak için AD Netsuite uygulamanıza bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="40cae-139">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Netsuite app.</span></span>

7. <span data-ttu-id="40cae-140">İçinde **bildirim e-posta** alan, bir kişi veya grubun sağlama hata bildirimleri almak ve gerekir onay e-posta adresini girin.</span><span class="sxs-lookup"><span data-stu-id="40cae-140">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span></span>

8. <span data-ttu-id="40cae-141">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="40cae-141">Click **Save.**</span></span>

9. <span data-ttu-id="40cae-142">Eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları Netsuite.**</span><span class="sxs-lookup"><span data-stu-id="40cae-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to Netsuite.**</span></span>

10. <span data-ttu-id="40cae-143">İçinde **öznitelik eşlemelerini** bölümünde, Netsuite için Azure AD'den eşitlenen kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="40cae-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Netsuite.</span></span> <span data-ttu-id="40cae-144">Seçilen öznitelikler olarak Not **eşleşen** özellikleri Netsuite kullanıcı hesaplarında güncelleştirme işlemleri için eşleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="40cae-144">Note that the attributes selected as **Matching** properties are used to match the user accounts in Netsuite for update operations.</span></span> <span data-ttu-id="40cae-145">Değişiklikleri kaydetmek için Kaydet düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="40cae-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="40cae-146">Azure AD hizmeti Netsuite için sağlama etkinleştirmek için değiştirmek **sağlama durumu** için **üzerinde** ayarları bölümünde</span><span class="sxs-lookup"><span data-stu-id="40cae-146">To enable the Azure AD provisioning service for Netsuite, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="40cae-147">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="40cae-147">Click **Save.**</span></span>

<span data-ttu-id="40cae-148">Herhangi bir kullanıcı ve/veya grupları kullanıcıları ve grupları bölümünde Netsuite atanan ilk eşitleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="40cae-148">It starts the initial synchronization of any users and/or groups assigned to Netsuite in the Users and Groups section.</span></span> <span data-ttu-id="40cae-149">İlk eşitlemeyi gerçekleştirmek için yaklaşık 20 dakikada çalıştığı sürece oluşan sonraki eşitlemeler uzun sürer unutmayın.</span><span class="sxs-lookup"><span data-stu-id="40cae-149">Note that the initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="40cae-150">Kullanabileceğiniz **eşitleme ayrıntıları** bölüm ilerlemeyi izlemek ve Netsuite uygulamanızı sağlama hizmeti tarafından gerçekleştirilen tüm eylemler açıklanmaktadır etkinlik raporları sağlamak için bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="40cae-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Netsuite app.</span></span>

<span data-ttu-id="40cae-151">Şimdi sınama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40cae-151">You can now create a test account.</span></span> <span data-ttu-id="40cae-152">Hesap için Netsuite eşitlendiğinden emin doğrulamak için en çok 20 dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="40cae-152">Wait for up to 20 minutes to verify that the account has been synchronized to Netsuite.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="40cae-153">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="40cae-153">Additional resources</span></span>

* [<span data-ttu-id="40cae-154">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="40cae-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="40cae-155">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="40cae-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="40cae-156">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="40cae-156">Configure Single Sign-on</span></span>](active-directory-saas-netsuite-tutorial.md)