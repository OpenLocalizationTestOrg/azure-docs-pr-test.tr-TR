---
title: "Öğretici: Azure Active Directory ile otomatik olarak bir kullanıcı sağlamak için GitHub yapılandırma | Microsoft Docs"
description: "Otomatik olarak sağlamak ve GitHub kullanıcı hesaplarına sağlanmasını için Azure Active Directory yapılandırmayı öğrenin."
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
ms.openlocfilehash: 3cc70273e95dbf4913e7bbcd8a37bd9a52987b60
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a><span data-ttu-id="31e32-103">Öğretici: Otomatik kullanıcı sağlamak için GitHub yapılandırma</span><span class="sxs-lookup"><span data-stu-id="31e32-103">Tutorial: Configuring GitHub for Automatic User Provisioning</span></span>


<span data-ttu-id="31e32-104">Bu öğreticinin amacı, GitHub ve Azure AD otomatik olarak sağlamak ve kullanıcı hesaplarına Azure AD'den GitHub sağlanmasını gerçekleştirmek için gereken adımları Göster sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="31e32-104">The objective of this tutorial is to show you the steps you need to perform in GitHub and Azure AD to automatically provision and de-provision user accounts from Azure AD to GitHub.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="31e32-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="31e32-105">Prerequisites</span></span>

<span data-ttu-id="31e32-106">Bu öğreticide gösterilen senaryo, aşağıdaki öğeleri zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="31e32-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="31e32-107">Bir Azure Active directory kiracısı</span><span class="sxs-lookup"><span data-stu-id="31e32-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="31e32-108">Github Kiracı ile [iş planı](https://help.github.com/articles/organization-billing-plans/#business-plan) veya daha iyi etkin</span><span class="sxs-lookup"><span data-stu-id="31e32-108">A Github tenant with the [Business plan](https://help.github.com/articles/organization-billing-plans/#business-plan) or better enabled</span></span> 
*   <span data-ttu-id="31e32-109">GitHub yönetici izinlerine sahip bir kullanıcı hesabı</span><span class="sxs-lookup"><span data-stu-id="31e32-109">A user account in GitHub with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="31e32-110">Azure AD tümleştirme sağlama dayanan [GitHub SCIM'yi API](https://developer.github.com/v3/scim/), Github takımlara iş plan üzerinde kullanılabilir veya daha iyi.</span><span class="sxs-lookup"><span data-stu-id="31e32-110">The Azure AD provisioning integration relies on the [GitHub SCIM API](https://developer.github.com/v3/scim/), which is available to Github teams on the Business plan or better.</span></span>

## <a name="assigning-users-to-github"></a><span data-ttu-id="31e32-111">Kullanıcılar için GitHub atama</span><span class="sxs-lookup"><span data-stu-id="31e32-111">Assigning users to GitHub</span></span>

<span data-ttu-id="31e32-112">Azure Active Directory "atamaları" adlı bir kavram hangi kullanıcıların seçili uygulamalara erişim alması belirlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="31e32-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="31e32-113">Otomatik olarak bir kullanıcı hesabı sağlama bağlamında, yalnızca kullanıcıların ve grupların "Azure AD uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="31e32-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="31e32-114">Yapılandırma ve sağlama hizmeti etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD grupları GitHub uygulamanıza erişimi olması gereken kullanıcılar temsil eden karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="31e32-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your GitHub app.</span></span> <span data-ttu-id="31e32-115">Karar sonra buradaki yönergeleri izleyerek, bu kullanıcılar GitHub uygulamanıza atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="31e32-115">Once decided, you can assign these users to your GitHub app by following the instructions here:</span></span>

[<span data-ttu-id="31e32-116">Bir kullanıcı veya grup için bir kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="31e32-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-github"></a><span data-ttu-id="31e32-117">Kullanıcılar için GitHub atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="31e32-117">Important tips for assigning users to GitHub</span></span>

*   <span data-ttu-id="31e32-118">Önerilir tek bir Azure AD kullanıcısının sağlama yapılandırmayı test etmek için GitHub atanır.</span><span class="sxs-lookup"><span data-stu-id="31e32-118">It is recommended that a single Azure AD user is assigned to GitHub to test the provisioning configuration.</span></span> <span data-ttu-id="31e32-119">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="31e32-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="31e32-120">Bir kullanıcı için GitHub atarken ya da seçmelisiniz **kullanıcı** rol ya da başka bir geçerli uygulamaya özgü rolü (varsa) atama iletişim.</span><span class="sxs-lookup"><span data-stu-id="31e32-120">When assigning a user to GitHub, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="31e32-121">**Varsayılan erişim** rol sağlamak için çalışmaz ve bu kullanıcılar atlandı.</span><span class="sxs-lookup"><span data-stu-id="31e32-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-to-github"></a><span data-ttu-id="31e32-122">Kullanıcı için GitHub sağlama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="31e32-122">Configuring user provisioning to GitHub</span></span> 

<span data-ttu-id="31e32-123">Bu bölümde Azure AD GitHub'ın kullanıcı hesabına API sağlama konusunda size rehberlik eder ve oluşturmak için sağlama hizmeti yapılandırma güncelleştirin ve Azure AD'de kullanıcı ve grup atama göre github'da atanan kullanıcı hesapları devre dışı bırak.</span><span class="sxs-lookup"><span data-stu-id="31e32-123">This section guides you through connecting your Azure AD to GitHub's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in GitHub based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="31e32-124">Da tercih edebilirsiniz etkin SAML tabanlı çoklu oturum açma için GitHub, yönergeleri izleyerek sağlanan [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="31e32-124">You may also choose to enabled SAML-based Single Sign-On for GitHub, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="31e32-125">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="31e32-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-github-in-azure-ad"></a><span data-ttu-id="31e32-126">Otomatik olarak bir kullanıcı hesabı için GitHub Azure AD'de sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="31e32-126">Configure automatic user account provisioning to GitHub in Azure AD</span></span>


1. <span data-ttu-id="31e32-127">İçinde [Azure portal](https://portal.azure.com), Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="31e32-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="31e32-128">Çoklu oturum açma için GitHub zaten yapılandırdıysanız arama alanı kullanarak GitHub Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="31e32-128">If you have already configured GitHub for single sign-on, search for your instance of GitHub using the search field.</span></span> <span data-ttu-id="31e32-129">Aksi takdirde seçin **Ekle** arayın ve **GitHub** uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="31e32-129">Otherwise, select **Add** and search for **GitHub** in the application gallery.</span></span> <span data-ttu-id="31e32-130">Arama sonuçlarından GitHub seçin ve uygulamaları listenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="31e32-130">Select GitHub from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="31e32-131">GitHub örneğiniz seçin ve ardından **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="31e32-131">Select your instance of GitHub, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="31e32-132">Ayarlama **sağlama modunda** için **otomatik**.</span><span class="sxs-lookup"><span data-stu-id="31e32-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![GitHub sağlama](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. <span data-ttu-id="31e32-134">Altında **yönetici kimlik bilgileri** 'yi tıklatın **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="31e32-134">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="31e32-135">Bu işlem, yeni bir tarayıcı penceresinde bir GitHub yetkilendirme iletişim kutusunu açar.</span><span class="sxs-lookup"><span data-stu-id="31e32-135">This operation opens a GitHub authorization dialog in a new browser window.</span></span> 

6. <span data-ttu-id="31e32-136">Yeni pencerede GitHub yönetici hesabınızı kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="31e32-136">In the new window, sign into GitHub using your Admin account.</span></span> <span data-ttu-id="31e32-137">Elde edilen yetkilendirme iletişim kutusunda sağlamayı etkinleştirmek istediğiniz GitHub ekibi seçin ve ardından **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="31e32-137">In the resulting authorization dialog, select the GitHub team that you want to enable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="31e32-138">Tamamlandığında, sağlama yapılandırmasını tamamlamak için Azure portalına geri dönün.</span><span class="sxs-lookup"><span data-stu-id="31e32-138">Once completed, return to the Azure portal to complete the provisioning configuration.</span></span>

    ![Yetkilendirme iletişim](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. <span data-ttu-id="31e32-140">Azure portalında giriş **Kiracı URL** tıklatıp **Bağlantıyı Sına** Azure emin olmak için AD GitHub uygulamanıza bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="31e32-140">In the Azure portal, input **Tenant URL** and click **Test Connection** to ensure Azure AD can connect to your GitHub app.</span></span> <span data-ttu-id="31e32-141">Bağlantı başarısız olursa, GitHub hesabınızda yönetici izinleri olduğundan emin olun ve **Kiracı URl** doğru girilen ve "Yetkilendir" adımı yeniden deneyin (size oluşturabilecek **Kiracı URL** kuralı tarafından: "https:// api.github.com/scim/v2/organizations/ + < Organizations_name > ", kuruluşlar, GitHub hesabınızda altında bulabilirsiniz: **ayarları** > **kuruluşların**).</span><span class="sxs-lookup"><span data-stu-id="31e32-141">If the connection fails, ensure your GitHub account has Admin permissions and **Tenant URl** is inputted correctly, then try the "Authorize" step again (you can constitute **Tenant URL** by rule: "https://api.github.com/scim/v2/organizations/ + <Organizations_name>", you can find your organizations under your GitHub account: **Settings** > **Organizations**).</span></span>

    ![Yetkilendirme iletişim](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. <span data-ttu-id="31e32-143">Bir kişi veya sağlama hata bildirimleri alması gereken Grup e-posta adresini girin **bildirim e-posta** alanına ve "bir hata oluştuğunda e-posta bildirimi gönder." onay kutusunu işaretleyin</span><span class="sxs-lookup"><span data-stu-id="31e32-143">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

9. <span data-ttu-id="31e32-144">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="31e32-144">Click **Save**.</span></span> 

10. <span data-ttu-id="31e32-145">Eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları GitHub için**.</span><span class="sxs-lookup"><span data-stu-id="31e32-145">Under the Mappings section, select **Synchronize Azure Active Directory Users to GitHub**.</span></span>

11. <span data-ttu-id="31e32-146">İçinde **öznitelik eşlemelerini** bölümünde, GitHub için Azure AD'den eşitlenen kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="31e32-146">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to GitHub.</span></span> <span data-ttu-id="31e32-147">Seçilen öznitelikler **eşleşen** özellikleri güncelleştirme işlemleri için github kullanıcı hesapları eşleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="31e32-147">The attributes selected as **Matching** properties are used to match the user accounts in GitHub for update operations.</span></span> <span data-ttu-id="31e32-148">Değişiklikleri kaydetmek için Kaydet düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="31e32-148">Select the Save button to commit any changes.</span></span>

12. <span data-ttu-id="31e32-149">GitHub için hizmet sağlama Azure AD etkinleştirmek için değiştirmek **sağlama durumu** için **üzerinde** içinde **ayarları** bölümü</span><span class="sxs-lookup"><span data-stu-id="31e32-149">To enable the Azure AD provisioning service for GitHub, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

13. <span data-ttu-id="31e32-150">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="31e32-150">Click **Save**.</span></span> 

<span data-ttu-id="31e32-151">Bu işlem, herhangi bir kullanıcı ve/veya grupları kullanıcıları ve grupları bölümünde GitHub atanan ilk eşitleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="31e32-151">This operation starts the initial synchronization of any users and/or groups assigned to GitHub in the Users and Groups section.</span></span> <span data-ttu-id="31e32-152">İlk eşitleme gerçekleştirmek yaklaşık 20 dakikada çalıştığı sürece oluşan sonraki eşitlemeler uzun sürer.</span><span class="sxs-lookup"><span data-stu-id="31e32-152">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="31e32-153">Kullanabileceğiniz **eşitleme ayrıntıları** bölüm ilerlemeyi izlemek ve sağlama hizmeti tarafından gerçekleştirilen tüm eylemler anlatılmaktadır etkinlik raporları sağlamak için bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="31e32-153">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="31e32-154">Günlükleri sağlama Azure AD okuma hakkında daha fazla bilgi için bkz: [otomatik olarak bir kullanıcı hesabı sağlama raporlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="31e32-154">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="31e32-155">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="31e32-155">Additional resources</span></span>

* [<span data-ttu-id="31e32-156">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="31e32-156">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="31e32-157">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="31e32-157">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="31e32-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="31e32-158">Next steps</span></span>

* [<span data-ttu-id="31e32-159">Günlüklerini gözden geçirin ve etkinlik sağlama raporları alma hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="31e32-159">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
