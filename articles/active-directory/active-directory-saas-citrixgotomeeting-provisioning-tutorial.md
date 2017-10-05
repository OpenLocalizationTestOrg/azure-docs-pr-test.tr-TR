---
title: "Öğretici: Azure Active Directory Tümleştirme ile Citrix GoToMeeting | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve Citrix GoToMeeting arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1ddfcd991431a11e5c3e306bd5905003d094ac18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a><span data-ttu-id="19ceb-103">Öğretici: Citrix GoToMeeting otomatik kullanıcı sağlamayı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="19ceb-103">Tutorial: Configuring Citrix GoToMeeting for Automatic User Provisioning</span></span>

<span data-ttu-id="19ceb-104">Bu öğreticinin amacı Citrix GoToMeeting ve Azure AD otomatik olarak sağlamak ve kullanıcı hesaplarına Azure AD'den Citrix GoToMeeting sağlanmasını gerçekleştirmek için gereken adımları Göster sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="19ceb-104">The objective of this tutorial is to show you the steps you need to perform in Citrix GoToMeeting and Azure AD to automatically provision and de-provision user accounts from Azure AD to Citrix GoToMeeting.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19ceb-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="19ceb-105">Prerequisites</span></span>

<span data-ttu-id="19ceb-106">Bu öğreticide gösterilen senaryo, aşağıdaki öğeleri zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="19ceb-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="19ceb-107">Bir Azure Active directory kiracısı.</span><span class="sxs-lookup"><span data-stu-id="19ceb-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="19ceb-108">Bir Citrix GoToMeeting çoklu oturum açma etkin abonelik.</span><span class="sxs-lookup"><span data-stu-id="19ceb-108">A Citrix GoToMeeting single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="19ceb-109">Citrix GoToMeeting takım yönetici izinlerine sahip bir kullanıcı hesabının.</span><span class="sxs-lookup"><span data-stu-id="19ceb-109">A user account in Citrix GoToMeeting with Team Admin permissions.</span></span>

## <a name="assigning-users-to-citrix-gotomeeting"></a><span data-ttu-id="19ceb-110">Kullanıcılar için Citrix GoToMeeting atama</span><span class="sxs-lookup"><span data-stu-id="19ceb-110">Assigning users to Citrix GoToMeeting</span></span>

<span data-ttu-id="19ceb-111">Azure Active Directory "atamaları" adlı bir kavram hangi kullanıcıların seçili uygulamalara erişim alması belirlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="19ceb-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="19ceb-112">Otomatik olarak bir kullanıcı hesabı sağlama bağlamında, yalnızca kullanıcıların ve grupların "Azure AD uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="19ceb-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="19ceb-113">Yapılandırma ve sağlama hizmeti etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD grupları Citrix GoToMeeting uygulamanıza erişimi olması gereken kullanıcılar temsil eden karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="19ceb-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Citrix GoToMeeting app.</span></span> <span data-ttu-id="19ceb-114">Karar sonra buradaki yönergeleri izleyerek, bu kullanıcılar Citrix GoToMeeting uygulamanıza atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="19ceb-114">Once decided, you can assign these users to your Citrix GoToMeeting app by following the instructions here:</span></span>

[<span data-ttu-id="19ceb-115">Bir kullanıcı veya grup için bir kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="19ceb-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-citrix-gotomeeting"></a><span data-ttu-id="19ceb-116">Kullanıcılar için Citrix GoToMeeting atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="19ceb-116">Important tips for assigning users to Citrix GoToMeeting</span></span>

*   <span data-ttu-id="19ceb-117">Önerilir tek bir Azure AD kullanıcısının sağlama yapılandırmayı test etmek için Citrix GoToMeeting atanır.</span><span class="sxs-lookup"><span data-stu-id="19ceb-117">It is recommended that a single Azure AD user is assigned to Citrix GoToMeeting to test the provisioning configuration.</span></span> <span data-ttu-id="19ceb-118">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="19ceb-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="19ceb-119">Bir kullanıcı için Citrix GoToMeeting atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="19ceb-119">When assigning a user to Citrix GoToMeeting, you must select a valid user role.</span></span> <span data-ttu-id="19ceb-120">"Varsayılan erişim" rolü sağlama için çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="19ceb-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="19ceb-121">Otomatik kullanıcı sağlamayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="19ceb-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="19ceb-122">Bu bölümde Azure AD Citrix GoToMeeting'ın kullanıcı hesabına API sağlama konusunda size rehberlik eder ve oluşturmak için sağlama hizmeti yapılandırma güncelleştirin ve kullanıcı ve Grup Citrix GoToMeeting hesaplarında göre atanan kullanıcı devre dışı bırak Azure AD'de atama.</span><span class="sxs-lookup"><span data-stu-id="19ceb-122">This section guides you through connecting your Azure AD to Citrix GoToMeeting's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Citrix GoToMeeting based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="19ceb-123">Da tercih edebilirsiniz etkin SAML tabanlı çoklu oturum açma için Citrix GoToMeeting, yönergeleri izleyerek sağlanan [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="19ceb-123">You may also choose to enabled SAML-based Single Sign-On for Citrix GoToMeeting, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="19ceb-124">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="19ceb-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="19ceb-125">Otomatik olarak bir kullanıcı hesabı sağlama yapılandırmak için:</span><span class="sxs-lookup"><span data-stu-id="19ceb-125">To configure automatic user account provisioning:</span></span>

1. <span data-ttu-id="19ceb-126">İçinde [Azure portal](https://portal.azure.com), Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="19ceb-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="19ceb-127">Çoklu oturum açma için Citrix GoToMeeting zaten yapılandırdıysanız Citrix arama alanı kullanarak GoToMeeting Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="19ceb-127">If you have already configured Citrix GoToMeeting for single sign-on, search for your instance of Citrix GoToMeeting using the search field.</span></span> <span data-ttu-id="19ceb-128">Aksi takdirde seçin **Ekle** arayın ve **Citrix GoToMeeting** uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="19ceb-128">Otherwise, select **Add** and search for **Citrix GoToMeeting** in the application gallery.</span></span> <span data-ttu-id="19ceb-129">Arama sonuçlarından Citrix GoToMeeting seçin ve uygulamaları listenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="19ceb-129">Select Citrix GoToMeeting from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="19ceb-130">Citrix GoToMeeting örneğiniz seçin ve ardından **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="19ceb-130">Select your instance of Citrix GoToMeeting, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="19ceb-131">Ayarlama **sağlama** moduna **otomatik**.</span><span class="sxs-lookup"><span data-stu-id="19ceb-131">Set the **Provisioning** Mode to **Automatic**.</span></span> 

    ![Sağlama](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="19ceb-133">Yönetici kimlik bilgileri bölümü altında aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="19ceb-133">Under the Admin Credentials section, perform the following steps:</span></span>
   
    <span data-ttu-id="19ceb-134">a.</span><span class="sxs-lookup"><span data-stu-id="19ceb-134">a.</span></span> <span data-ttu-id="19ceb-135">İçinde **Citrix GoToMeeting yönetici kullanıcı adı** metin kutusuna, bir yönetici kullanıcı adını yazın.</span><span class="sxs-lookup"><span data-stu-id="19ceb-135">In the **Citrix GoToMeeting Admin User Name** textbox, type the user name of an administrator.</span></span>

    <span data-ttu-id="19ceb-136">b.</span><span class="sxs-lookup"><span data-stu-id="19ceb-136">b.</span></span> <span data-ttu-id="19ceb-137">İçinde **Citrix GoToMeeting yönetici parolası** metin kutusuna, yöneticinin parola.</span><span class="sxs-lookup"><span data-stu-id="19ceb-137">In the **Citrix GoToMeeting Admin Password** textbox, the administrator's password.</span></span>

6. <span data-ttu-id="19ceb-138">Azure portalında tıklatın **Bağlantıyı Sına** Azure emin olmak için AD Citrix GoToMeeting uygulamanıza bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="19ceb-138">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Citrix GoToMeeting app.</span></span> <span data-ttu-id="19ceb-139">Bağlantı başarısız olursa, Citrix GoToMeeting hesabınızın Team yönetici izinleri olduğundan emin olun ve deneyin **"Yönetici kimlik bilgileri"** adım yeniden uygulayın.</span><span class="sxs-lookup"><span data-stu-id="19ceb-139">If the connection fails, ensure your Citrix GoToMeeting account has Team Admin permissions and try the **"Admin Credentials"** step again.</span></span>

7. <span data-ttu-id="19ceb-140">Bir kişi veya sağlama hata bildirimleri alması gereken Grup e-posta adresini girin **bildirim e-posta** alan ve onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="19ceb-140">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

8. <span data-ttu-id="19ceb-141">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="19ceb-141">Click **Save.**</span></span>

9. <span data-ttu-id="19ceb-142">Eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları için Citrix GoToMeeting.**</span><span class="sxs-lookup"><span data-stu-id="19ceb-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to Citrix GoToMeeting.**</span></span>

10. <span data-ttu-id="19ceb-143">İçinde **öznitelik eşlemelerini** bölümünde, Citrix GoToMeeting Azure AD'den eşitlenen kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="19ceb-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Citrix GoToMeeting.</span></span> <span data-ttu-id="19ceb-144">Seçilen öznitelikler **eşleşen** özellikleri Citrix GoToMeeting kullanıcı hesaplarında güncelleştirme işlemleri için eşleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="19ceb-144">The attributes selected as **Matching** properties are used to match the user accounts in Citrix GoToMeeting for update operations.</span></span> <span data-ttu-id="19ceb-145">Değişiklikleri kaydetmek için Kaydet düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="19ceb-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="19ceb-146">Citrix GoToMeeting için hizmet sağlama Azure AD etkinleştirmek için değiştirmek **sağlama durumu** için **üzerinde** ayarları bölümünde</span><span class="sxs-lookup"><span data-stu-id="19ceb-146">To enable the Azure AD provisioning service for Citrix GoToMeeting, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="19ceb-147">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="19ceb-147">Click **Save.**</span></span>

<span data-ttu-id="19ceb-148">Herhangi bir kullanıcı ve/veya grupları kullanıcıları ve grupları bölümünde Citrix GoToMeeting atanan ilk eşitleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="19ceb-148">It starts the initial synchronization of any users and/or groups assigned to Citrix GoToMeeting in the Users and Groups section.</span></span> <span data-ttu-id="19ceb-149">İlk eşitleme gerçekleştirmek yaklaşık 20 dakikada çalıştığı sürece oluşan sonraki eşitlemeler uzun sürer.</span><span class="sxs-lookup"><span data-stu-id="19ceb-149">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="19ceb-150">Kullanabileceğiniz **eşitleme ayrıntıları** bölüm ilerlemeyi izlemek ve Citrix GoToMeeting uygulamanızı sağlama hizmeti tarafından gerçekleştirilen tüm eylemler açıklanmaktadır etkinlik raporları sağlamak için bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="19ceb-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Citrix GoToMeeting app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="19ceb-151">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="19ceb-151">Additional resources</span></span>

* [<span data-ttu-id="19ceb-152">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="19ceb-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="19ceb-153">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="19ceb-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="19ceb-154">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="19ceb-154">Configure Single Sign-on</span></span>](active-directory-saas-citrix-gotomeeting-tutorial.md)


