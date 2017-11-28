---
title: "Öğretici: Azure Active Directory ile otomatik kullanıcı sağlamayı LucidChart yapılandırma | Microsoft Docs"
description: "Otomatik olarak sağlamak ve kullanıcı hesaplarına LucidChart sağlanmasını için Azure Active Directory yapılandırmayı öğrenin."
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
ms.openlocfilehash: 1f9344a5e750360e21ed7dc8e3ed013c2c2e1a45
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-lucidchart-for-automatic-user-provisioning"></a><span data-ttu-id="587f3-103">Öğretici: LucidChart otomatik kullanıcı sağlamayı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="587f3-103">Tutorial: Configuring LucidChart for Automatic User Provisioning</span></span>


<span data-ttu-id="587f3-104">Bu öğreticinin amacı LucidChart ve Azure AD otomatik olarak sağlamak ve kullanıcı hesaplarına Azure AD'den LucidChart sağlanmasını gerçekleştirmek için gereken adımları Göster sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="587f3-104">The objective of this tutorial is to show you the steps you need to perform in LucidChart and Azure AD to automatically provision and de-provision user accounts from Azure AD to LucidChart.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="587f3-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="587f3-105">Prerequisites</span></span>

<span data-ttu-id="587f3-106">Bu öğreticide gösterilen senaryo, aşağıdaki öğeleri zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="587f3-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="587f3-107">Bir Azure Active directory kiracısı</span><span class="sxs-lookup"><span data-stu-id="587f3-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="587f3-108">LucidChart Kiracı ile [Kurumsal planı](https://www.lucidchart.com/user/117598685#/subscriptionLevel) veya daha iyi etkin</span><span class="sxs-lookup"><span data-stu-id="587f3-108">A LucidChart tenant with the [Enterprise plan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) or better enabled</span></span> 
*   <span data-ttu-id="587f3-109">LucidChart yönetici izinlerine sahip bir kullanıcı hesabı</span><span class="sxs-lookup"><span data-stu-id="587f3-109">A user account in LucidChart with Admin permissions</span></span> 

## <a name="assigning-users-to-lucidchart"></a><span data-ttu-id="587f3-110">Kullanıcılar için LucidChart atama</span><span class="sxs-lookup"><span data-stu-id="587f3-110">Assigning users to LucidChart</span></span>

<span data-ttu-id="587f3-111">Azure Active Directory "atamaları" adlı bir kavram hangi kullanıcıların seçili uygulamalara erişim alması belirlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="587f3-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="587f3-112">Otomatik olarak bir kullanıcı hesabı sağlama bağlamında, yalnızca kullanıcıların ve grupların "Azure AD uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="587f3-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="587f3-113">Yapılandırma ve sağlama hizmeti etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD grupları LucidChart uygulamanıza erişimi olması gereken kullanıcılar temsil eden karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="587f3-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your LucidChart app.</span></span> <span data-ttu-id="587f3-114">Karar sonra buradaki yönergeleri izleyerek, bu kullanıcılar LucidChart uygulamanıza atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="587f3-114">Once decided, you can assign these users to your LucidChart app by following the instructions here:</span></span>

[<span data-ttu-id="587f3-115">Bir kullanıcı veya grup için bir kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="587f3-115">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-lucidchart"></a><span data-ttu-id="587f3-116">Kullanıcılar için LucidChart atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="587f3-116">Important tips for assigning users to LucidChart</span></span>

*   <span data-ttu-id="587f3-117">Önerilir tek bir Azure AD kullanıcısının sağlama yapılandırmayı test etmek için LucidChart atanır.</span><span class="sxs-lookup"><span data-stu-id="587f3-117">It is recommended that a single Azure AD user is assigned to LucidChart to test the provisioning configuration.</span></span> <span data-ttu-id="587f3-118">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="587f3-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="587f3-119">Bir kullanıcı için LucidChart atarken ya da seçmelisiniz **kullanıcı** rol ya da başka bir geçerli uygulamaya özgü rolü (varsa) atama iletişim.</span><span class="sxs-lookup"><span data-stu-id="587f3-119">When assigning a user to LucidChart, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="587f3-120">**Varsayılan erişim** rol sağlamak için çalışmaz ve bu kullanıcılar atlandı.</span><span class="sxs-lookup"><span data-stu-id="587f3-120">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-to-lucidchart"></a><span data-ttu-id="587f3-121">Kullanıcı için LucidChart sağlama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="587f3-121">Configuring user provisioning to LucidChart</span></span> 

<span data-ttu-id="587f3-122">Bu bölümde Azure AD LucidChart'ın kullanıcı hesabına API sağlama konusunda size rehberlik eder ve oluşturmak için sağlama hizmeti yapılandırma güncelleştirin ve Azure AD'de kullanıcı ve grup atama göre LucidChart atanan kullanıcı hesaplarında devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="587f3-122">This section guides you through connecting your Azure AD to LucidChart's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in LucidChart based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="587f3-123">Da tercih edebilirsiniz etkin SAML tabanlı çoklu oturum açma için LucidChart, yönergeleri izleyerek sağlanan [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="587f3-123">You may also choose to enabled SAML-based Single Sign-On for LucidChart, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="587f3-124">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="587f3-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-lucidchart-in-azure-ad"></a><span data-ttu-id="587f3-125">Otomatik olarak bir kullanıcı hesabı için LucidChart Azure AD'de sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="587f3-125">Configure automatic user account provisioning to LucidChart in Azure AD</span></span>


1. <span data-ttu-id="587f3-126">İçinde [Azure portal](https://portal.azure.com), Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="587f3-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="587f3-127">Çoklu oturum açma için LucidChart zaten yapılandırdıysanız arama alanı kullanarak LucidChart Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="587f3-127">If you have already configured LucidChart for single sign-on, search for your instance of LucidChart using the search field.</span></span> <span data-ttu-id="587f3-128">Aksi takdirde seçin **Ekle** arayın ve **LucidChart** uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="587f3-128">Otherwise, select **Add** and search for **LucidChart** in the application gallery.</span></span> <span data-ttu-id="587f3-129">Arama sonuçlarından LucidChart seçin ve uygulamaları listenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="587f3-129">Select LucidChart from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="587f3-130">LucidChart örneğiniz seçin ve ardından **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="587f3-130">Select your instance of LucidChart, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="587f3-131">Ayarlama **sağlama modunda** için **otomatik**.</span><span class="sxs-lookup"><span data-stu-id="587f3-131">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![LucidChart sağlama](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart1.png)

5. <span data-ttu-id="587f3-133">Altında **yönetici kimlik bilgileri** bölümü, giriş **gizli belirteci** LucidChart'ın hesap tarafından oluşturulan (belirteç hesabınızın altında bulabilirsiniz: **takım**  >  **Uygulama tümleştirmesi** > **SCIM'yi**).</span><span class="sxs-lookup"><span data-stu-id="587f3-133">Under the **Admin Credentials** section, input the **Secret Token** generated by your LucidChart's account (you can find the token under your account: **Team** > **App Integration** > **SCIM**).</span></span> 

    ![LucidChart sağlama](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart2.png)

6. <span data-ttu-id="587f3-135">Azure portalında tıklatın **Bağlantıyı Sına** Azure emin olmak için AD LucidChart uygulamanıza bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="587f3-135">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your LucidChart app.</span></span> <span data-ttu-id="587f3-136">Bağlantı başarısız olursa LucidChart hesabınız yönetici izinlerine sahip olduğundan emin olun ve 5. adım yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="587f3-136">If the connection fails, ensure your LucidChart account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="587f3-137">Bir kişi veya sağlama hata bildirimleri alması gereken Grup e-posta adresini girin **bildirim e-posta** alanına ve "bir hata oluştuğunda e-posta bildirimi gönder." onay kutusunu işaretleyin</span><span class="sxs-lookup"><span data-stu-id="587f3-137">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="587f3-138">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="587f3-138">Click **Save**.</span></span> 

9. <span data-ttu-id="587f3-139">Eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları LucidChart**.</span><span class="sxs-lookup"><span data-stu-id="587f3-139">Under the Mappings section, select **Synchronize Azure Active Directory Users to LucidChart**.</span></span>

10. <span data-ttu-id="587f3-140">İçinde **öznitelik eşlemelerini** bölümünde, LucidChart için Azure AD'den eşitlenen kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="587f3-140">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to LucidChart.</span></span> <span data-ttu-id="587f3-141">Seçilen öznitelikler **eşleşen** özellikleri LucidChart kullanıcı hesaplarında güncelleştirme işlemleri için eşleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="587f3-141">The attributes selected as **Matching** properties are used to match the user accounts in LucidChart for update operations.</span></span> <span data-ttu-id="587f3-142">Değişiklikleri kaydetmek için Kaydet düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="587f3-142">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="587f3-143">Azure AD hizmeti LucidChart için sağlama etkinleştirmek için değiştirmek **sağlama durumu** için **üzerinde** içinde **ayarları** bölümü</span><span class="sxs-lookup"><span data-stu-id="587f3-143">To enable the Azure AD provisioning service for LucidChart, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="587f3-144">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="587f3-144">Click **Save**.</span></span> 

<span data-ttu-id="587f3-145">Bu işlem, herhangi bir kullanıcı ve/veya grupları kullanıcıları ve grupları bölümünde LucidChart atanan ilk eşitleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="587f3-145">This operation starts the initial synchronization of any users and/or groups assigned to LucidChart in the Users and Groups section.</span></span> <span data-ttu-id="587f3-146">İlk eşitleme gerçekleştirmek yaklaşık 20 dakikada çalıştığı sürece oluşan sonraki eşitlemeler uzun sürer.</span><span class="sxs-lookup"><span data-stu-id="587f3-146">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="587f3-147">Kullanabileceğiniz **eşitleme ayrıntıları** bölüm ilerlemeyi izlemek ve sağlama hizmeti tarafından gerçekleştirilen tüm eylemler anlatılmaktadır etkinlik raporları sağlamak için bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="587f3-147">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="587f3-148">Günlükleri sağlama Azure AD okuma hakkında daha fazla bilgi için bkz: [otomatik olarak bir kullanıcı hesabı sağlama raporlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="587f3-148">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="587f3-149">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="587f3-149">Additional resources</span></span>

* [<span data-ttu-id="587f3-150">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="587f3-150">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="587f3-151">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="587f3-151">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="587f3-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="587f3-152">Next steps</span></span>

* [<span data-ttu-id="587f3-153">Günlüklerini gözden geçirin ve etkinlik sağlama raporları alma hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="587f3-153">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
