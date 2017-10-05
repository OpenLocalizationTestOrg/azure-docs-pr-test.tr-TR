---
title: "Öğretici: Azure Active Directory ile otomatik kullanıcı sağlamayı ThousandEyes yapılandırma | Microsoft Docs"
description: "Otomatik olarak sağlamak ve kullanıcı hesaplarına ThousandEyes sağlanmasını için Azure Active Directory yapılandırmayı öğrenin."
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
ms.openlocfilehash: e6bc2eab3cc1adcf26857ed98d920177a51455ea
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-thousandeyes-for-automatic-user-provisioning"></a><span data-ttu-id="a3781-103">Öğretici: ThousandEyes otomatik kullanıcı sağlamayı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a3781-103">Tutorial: Configuring ThousandEyes for Automatic User Provisioning</span></span>


<span data-ttu-id="a3781-104">Bu öğreticinin amacı ThousandEyes ve Azure AD otomatik olarak sağlamak ve kullanıcı hesaplarına Azure AD'den ThousandEyes sağlanmasını gerçekleştirmek için gereken adımları Göster sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="a3781-104">The objective of this tutorial is to show you the steps you need to perform in ThousandEyes and Azure AD to automatically provision and de-provision user accounts from Azure AD to ThousandEyes.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a3781-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a3781-105">Prerequisites</span></span>

<span data-ttu-id="a3781-106">Bu öğreticide gösterilen senaryo, aşağıdaki öğeleri zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="a3781-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="a3781-107">Bir Azure Active directory kiracısı</span><span class="sxs-lookup"><span data-stu-id="a3781-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="a3781-108">ThousandEyes Kiracı ile [standart planı](https://www.thousandeyes.com/pricing) veya daha iyi etkin</span><span class="sxs-lookup"><span data-stu-id="a3781-108">A ThousandEyes tenant with the [Standard plan](https://www.thousandeyes.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="a3781-109">ThousandEyes yönetici izinlerine sahip bir kullanıcı hesabı</span><span class="sxs-lookup"><span data-stu-id="a3781-109">A user account in ThousandEyes with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="a3781-110">Tümleştirme sağlama Azure AD dayanan [ThousandEyes SCIM'yi API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), standart plan üzerinde ThousandEyes ekipleri için kullanılabilir ya da daha iyi olduğu.</span><span class="sxs-lookup"><span data-stu-id="a3781-110">The Azure AD provisioning integration relies on the [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), which is available to ThousandEyes teams on the Standard plan or better.</span></span>

## <a name="assigning-users-to-thousandeyes"></a><span data-ttu-id="a3781-111">Kullanıcılar için ThousandEyes atama</span><span class="sxs-lookup"><span data-stu-id="a3781-111">Assigning users to ThousandEyes</span></span>

<span data-ttu-id="a3781-112">Azure Active Directory "atamaları" adlı bir kavram hangi kullanıcıların seçili uygulamalara erişim alması belirlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="a3781-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="a3781-113">Otomatik olarak bir kullanıcı hesabı sağlama bağlamında, yalnızca kullanıcıların ve grupların "Azure AD uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="a3781-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="a3781-114">Yapılandırma ve sağlama hizmeti etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD grupları ThousandEyes uygulamanıza erişimi olması gereken kullanıcılar temsil eden karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a3781-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your ThousandEyes app.</span></span> <span data-ttu-id="a3781-115">Karar sonra buradaki yönergeleri izleyerek, bu kullanıcılar ThousandEyes uygulamanıza atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a3781-115">Once decided, you can assign these users to your ThousandEyes app by following the instructions here:</span></span>

[<span data-ttu-id="a3781-116">Bir kullanıcı veya grup için bir kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="a3781-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-thousandeyes"></a><span data-ttu-id="a3781-117">Kullanıcılar için ThousandEyes atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="a3781-117">Important tips for assigning users to ThousandEyes</span></span>

*   <span data-ttu-id="a3781-118">Önerilir tek bir Azure AD kullanıcısının sağlama yapılandırmayı test etmek için ThousandEyes atanır.</span><span class="sxs-lookup"><span data-stu-id="a3781-118">It is recommended that a single Azure AD user is assigned to ThousandEyes to test the provisioning configuration.</span></span> <span data-ttu-id="a3781-119">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="a3781-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="a3781-120">Bir kullanıcı için ThousandEyes atarken ya da seçmelisiniz **kullanıcı** rol ya da başka bir geçerli uygulamaya özgü rolü (varsa) atama iletişim.</span><span class="sxs-lookup"><span data-stu-id="a3781-120">When assigning a user to ThousandEyes, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="a3781-121">**Varsayılan erişim** rol sağlamak için çalışmaz ve bu kullanıcılar atlandı.</span><span class="sxs-lookup"><span data-stu-id="a3781-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-to-thousandeyes"></a><span data-ttu-id="a3781-122">Kullanıcı için ThousandEyes sağlama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a3781-122">Configuring user provisioning to ThousandEyes</span></span> 

<span data-ttu-id="a3781-123">Bu bölümde Azure AD ThousandEyes'ın kullanıcı hesabına API sağlama konusunda size rehberlik eder ve oluşturmak için sağlama hizmeti yapılandırma güncelleştirin ve Azure AD'de kullanıcı ve grup atama göre ThousandEyes atanan kullanıcı hesaplarında devre dışı bırak .</span><span class="sxs-lookup"><span data-stu-id="a3781-123">This section guides you through connecting your Azure AD to ThousandEyes's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in ThousandEyes based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="a3781-124">Da tercih edebilirsiniz etkin SAML tabanlı çoklu oturum açma için ThousandEyes, yönergeleri izleyerek sağlanan [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a3781-124">You may also choose to enabled SAML-based Single Sign-On for ThousandEyes, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a3781-125">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="a3781-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-thousandeyes-in-azure-ad"></a><span data-ttu-id="a3781-126">Otomatik olarak bir kullanıcı hesabı için ThousandEyes Azure AD'de sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="a3781-126">Configure automatic user account provisioning to ThousandEyes in Azure AD</span></span>


1. <span data-ttu-id="a3781-127">İçinde [Azure portal](https://portal.azure.com), Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="a3781-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="a3781-128">Çoklu oturum açma için ThousandEyes zaten yapılandırdıysanız arama alanı kullanarak ThousandEyes Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="a3781-128">If you have already configured ThousandEyes for single sign-on, search for your instance of ThousandEyes using the search field.</span></span> <span data-ttu-id="a3781-129">Aksi takdirde seçin **Ekle** arayın ve **ThousandEyes** uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="a3781-129">Otherwise, select **Add** and search for **ThousandEyes** in the application gallery.</span></span> <span data-ttu-id="a3781-130">Arama sonuçlarından ThousandEyes seçin ve uygulamaları listenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a3781-130">Select ThousandEyes from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="a3781-131">ThousandEyes örneğiniz seçin ve ardından **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="a3781-131">Select your instance of ThousandEyes, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="a3781-132">Ayarlama **sağlama modunda** için **otomatik**.</span><span class="sxs-lookup"><span data-stu-id="a3781-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![ThousandEyes sağlama](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes1.png)

5. <span data-ttu-id="a3781-134">Altında **yönetici kimlik bilgileri** bölümü, giriş **gizli belirteci** ThousandEyes'ın hesap tarafından oluşturulan (belirteç ThousandEyes hesabınızın altında bulabilirsiniz: **güvenlik & Kimlik doğrulama**).</span><span class="sxs-lookup"><span data-stu-id="a3781-134">Under the **Admin Credentials** section, input the **Secret Token** generated by your ThousandEyes's account (you can find the token under your ThousandEyes account: **Security & Authentication**).</span></span> 

    ![ThousandEyes sağlama](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes2.png)

6. <span data-ttu-id="a3781-136">Azure portalında tıklatın **Bağlantıyı Sına** Azure emin olmak için AD ThousandEyes uygulamanıza bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="a3781-136">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your ThousandEyes app.</span></span> <span data-ttu-id="a3781-137">Bağlantı başarısız olursa ThousandEyes hesabınız yönetici izinlerine sahip olduğundan emin olun ve 5. adım yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="a3781-137">If the connection fails, ensure your ThousandEyes account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="a3781-138">Bir kişi veya sağlama hata bildirimleri alması gereken Grup e-posta adresini girin **bildirim e-posta** alanına ve "bir hata oluştuğunda e-posta bildirimi gönder." onay kutusunu işaretleyin</span><span class="sxs-lookup"><span data-stu-id="a3781-138">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="a3781-139">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a3781-139">Click **Save**.</span></span> 

9. <span data-ttu-id="a3781-140">Eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="a3781-140">Under the Mappings section, select **Synchronize Azure Active Directory Users to ThousandEyes**.</span></span>

10. <span data-ttu-id="a3781-141">İçinde **öznitelik eşlemelerini** bölümünde, ThousandEyes için Azure AD'den eşitlenen kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="a3781-141">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to ThousandEyes.</span></span> <span data-ttu-id="a3781-142">Seçilen öznitelikler **eşleşen** özellikleri ThousandEyes kullanıcı hesaplarında güncelleştirme işlemleri için eşleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a3781-142">The attributes selected as **Matching** properties are used to match the user accounts in ThousandEyes for update operations.</span></span> <span data-ttu-id="a3781-143">Değişiklikleri kaydetmek için Kaydet düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="a3781-143">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="a3781-144">Azure AD hizmeti ThousandEyes için sağlama etkinleştirmek için değiştirmek **sağlama durumu** için **üzerinde** içinde **ayarları** bölümü</span><span class="sxs-lookup"><span data-stu-id="a3781-144">To enable the Azure AD provisioning service for ThousandEyes, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="a3781-145">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a3781-145">Click **Save**.</span></span> 

<span data-ttu-id="a3781-146">Bu işlem, herhangi bir kullanıcı ve/veya grupları kullanıcıları ve grupları bölümünde ThousandEyes atanan ilk eşitleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="a3781-146">This operation starts the initial synchronization of any users and/or groups assigned to ThousandEyes in the Users and Groups section.</span></span> <span data-ttu-id="a3781-147">İlk eşitleme gerçekleştirmek yaklaşık 20 dakikada çalıştığı sürece oluşan sonraki eşitlemeler uzun sürer.</span><span class="sxs-lookup"><span data-stu-id="a3781-147">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="a3781-148">Kullanabileceğiniz **eşitleme ayrıntıları** bölüm ilerlemeyi izlemek ve sağlama hizmeti tarafından gerçekleştirilen tüm eylemler anlatılmaktadır etkinlik raporları sağlamak için bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="a3781-148">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="a3781-149">Günlükleri sağlama Azure AD okuma hakkında daha fazla bilgi için bkz: [otomatik olarak bir kullanıcı hesabı sağlama raporlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="a3781-149">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a3781-150">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a3781-150">Additional resources</span></span>

* [<span data-ttu-id="a3781-151">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="a3781-151">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="a3781-152">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="a3781-152">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="a3781-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a3781-153">Next steps</span></span>

* [<span data-ttu-id="a3781-154">Günlüklerini gözden geçirin ve etkinlik sağlama raporları alma hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="a3781-154">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
