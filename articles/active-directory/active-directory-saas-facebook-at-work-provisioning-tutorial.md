---
title: "Öğretici: Kullanıcı sağlamak için çalışma alanına Facebook tarafından yapılandırma | Microsoft Docs"
description: "Azure AD tooWorkplace Facebook tarafından gelen nasıl tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesapları öğrenin."
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
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33d294dbc8f441b29138408b3c9ca41f2141f8af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="85c0d-103">Öğretici: Facebook ile çalışma alanına kullanıcı sağlamak için yapılandırın</span><span class="sxs-lookup"><span data-stu-id="85c0d-103">Tutorial: Configure Workplace by Facebook for user provisioning</span></span>

<span data-ttu-id="85c0d-104">Sağlamak ve Azure Active Directory (Azure AD) tooWorkplace Facebook tarafından kullanıcı hesaplarından sağlanmasını adımları gerekli tooautomatically hello Bu öğretici gösterir.</span><span class="sxs-lookup"><span data-stu-id="85c0d-104">This tutorial shows you hello steps necessary tooautomatically provision and de-provision user accounts from Azure Active Directory (Azure AD) tooWorkplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85c0d-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="85c0d-105">Prerequisites</span></span>

<span data-ttu-id="85c0d-106">Facebook ile çalışma alanına ile Azure AD tümleştirme tooconfigure, hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="85c0d-106">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following:</span></span>

- <span data-ttu-id="85c0d-107">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="85c0d-107">An Azure AD subscription</span></span>
- <span data-ttu-id="85c0d-108">Abonelik çalışma alanına Facebook çoklu oturum açma (SSO) tarafından etkin</span><span class="sxs-lookup"><span data-stu-id="85c0d-108">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="85c0d-109">Bu öğreticide tootest hello adımları bu önerileri izleyin:</span><span class="sxs-lookup"><span data-stu-id="85c0d-109">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="85c0d-110">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="85c0d-110">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="85c0d-111">Bir Azure AD deneme ortam yoksa, alabileceğiniz bir [bir aylık deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="85c0d-111">If you don't have an Azure AD trial environment, you can get a [one-month trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assign-users-tooworkplace-by-facebook"></a><span data-ttu-id="85c0d-112">Kullanıcıların tooWorkplace Facebook tarafından atayın</span><span class="sxs-lookup"><span data-stu-id="85c0d-112">Assign users tooWorkplace by Facebook</span></span>

<span data-ttu-id="85c0d-113">Azure AD hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır.</span><span class="sxs-lookup"><span data-stu-id="85c0d-113">Azure AD uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="85c0d-114">Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların Azure AD tooan uygulamada atanan eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="85c0d-114">In hello context of automatic user account provisioning, only hello users and groups that have been assigned tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="85c0d-115">Yapılandırma ve hizmet sağlama hello etkinleştirme karar vermeden önce hangi kullanıcıların ve grupların Azure AD içinde tooyour çalışma alanına Facebook uygulaması tarafından erişim hello kullanıcılar temsil eder.</span><span class="sxs-lookup"><span data-stu-id="85c0d-115">Before configuring and enabling hello provisioning service, decide what users and groups in Azure AD represent hello users who need access tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="85c0d-116">İzleyerek Facebook uygulaması tarafından bu kullanıcıların tooyour çalışma alanına daha sonra yeniden atayabilirsiniz hello yönergeleri [bir kullanıcı veya grup tooan kuruluş uygulama atama](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="85c0d-116">You can then assign these users tooyour Workplace by Facebook app by following hello instructions in [Assign a user or group tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span></span>

>[!IMPORTANT]
>*   <span data-ttu-id="85c0d-117">Tek bir atayarak yapılandırma sağlama test hello Azure AD kullanıcı tooWorkplace Facebook tarafından.</span><span class="sxs-lookup"><span data-stu-id="85c0d-117">Test hello provisioning configuration by assigning a single Azure AD user tooWorkplace by Facebook.</span></span> <span data-ttu-id="85c0d-118">Ek kullanıcılar ve gruplar daha sonra atayın.</span><span class="sxs-lookup"><span data-stu-id="85c0d-118">Assign additional users and groups later.</span></span>
>*   <span data-ttu-id="85c0d-119">Bir kullanıcı tooWorkplace Facebook tarafından atadığınızda, geçerli bir kullanıcı rolünün seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="85c0d-119">When you assign a user tooWorkplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="85c0d-120">Merhaba varsayılan erişim rolü sağlama için çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="85c0d-120">hello Default Access role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="85c0d-121">Otomatik kullanıcı sağlamayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="85c0d-121">Enable automated user provisioning</span></span>

<span data-ttu-id="85c0d-122">Bu bölümde, çalışma alanına API Facebook tarafından sağlama, Azure AD toohello kullanıcı hesabınızın konusunda size rehberlik eder.</span><span class="sxs-lookup"><span data-stu-id="85c0d-122">This section guides you through connecting your Azure AD toohello user account provisioning API of Workplace by Facebook.</span></span> <span data-ttu-id="85c0d-123">Ayrıca nasıl tooconfigure hello sağlama hizmeti toocreate, güncelleştirme ve çalışma Facebook tarafından atanan kullanıcı hesapları devre dışı bırak öğrenin.</span><span class="sxs-lookup"><span data-stu-id="85c0d-123">You also learn how tooconfigure hello provisioning service toocreate, update, and disable assigned user accounts in Workplace by Facebook.</span></span> <span data-ttu-id="85c0d-124">Bu kullanıcı ve grup atama Azure AD'de dayanır.</span><span class="sxs-lookup"><span data-stu-id="85c0d-124">This is based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="85c0d-125">Ayrıca tooenabled SAML tabanlı SSO için çalışma alanı, Facebook tarafından göre hello sağlanan hello yönergelerini izleyerek seçebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="85c0d-125">You can also choose tooenabled SAML-based SSO for Workplace by Facebook, by following hello instructions provided in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="85c0d-126">Bu iki özellik birbirine tamamlayan olsa SSO otomatik sağlamayı bağımsız olarak yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="85c0d-126">SSO can be configured independently of automatic provisioning, though these two features complement each other.</span></span>

### <a name="configure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a><span data-ttu-id="85c0d-127">Azure AD'de tooWorkplace Facebook tarafından sağlama kullanıcı hesabı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="85c0d-127">Configure user account provisioning tooWorkplace by Facebook in Azure AD</span></span>

<span data-ttu-id="85c0d-128">Azure AD destekler Hello özelliği tooautomatically hello hesap ayrıntılarını eşitlemek kullanıcılar tooWorkplace Facebook tarafından atanır.</span><span class="sxs-lookup"><span data-stu-id="85c0d-128">Azure AD supports hello ability tooautomatically synchronize hello account details of assigned users tooWorkplace by Facebook.</span></span> <span data-ttu-id="85c0d-129">Facebook tooget hello verileri, gereken tooauthorize kullanıcılar, erişimi için önce tarafından çalışma alanına bu otomatik eşitlenmesine olanak bunları içinde toosign hello için ilk kez çalışılıyor.</span><span class="sxs-lookup"><span data-stu-id="85c0d-129">This automatic synchronization enables Workplace by Facebook tooget hello data it needs tooauthorize users for access, before them attempting toosign in for hello first time.</span></span> <span data-ttu-id="85c0d-130">Erişim Azure AD'de iptal edilmiş durumda olduğunda, ayrıca çalışma alanına Facebook tarafından kullanıcılardan XML'deki sağlamasını yapar.</span><span class="sxs-lookup"><span data-stu-id="85c0d-130">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="85c0d-131">Merhaba, [Azure portal](https://portal.azure.com)seçin **Azure Active Directory** > **Kurumsal uygulamaları** > **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="85c0d-131">In hello [Azure portal](https://portal.azure.com), select **Azure Active Directory** > **Enterprise Apps** > **All applications**.</span></span>

2. <span data-ttu-id="85c0d-132">SSO için Facebook ile çalışma alanına zaten yapılandırdıysanız, çalışma alanına Facebook tarafından örneğiniz hello arama alanı kullanarak arayın.</span><span class="sxs-lookup"><span data-stu-id="85c0d-132">If you have already configured Workplace by Facebook for SSO, search for your instance of Workplace by Facebook by using hello search field.</span></span> <span data-ttu-id="85c0d-133">Aksi takdirde seçin **Ekle** arayın ve **Facebook ile çalışma alanına** hello uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="85c0d-133">Otherwise, select **Add** and search for **Workplace by Facebook** in hello application gallery.</span></span> <span data-ttu-id="85c0d-134">Seçin **Facebook ile çalışma alanına** hello gelen arama sonuçlarında ve uygulamaların tooyour listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="85c0d-134">Select **Workplace by Facebook** from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="85c0d-135">Facebook ile çalışma alanına örneğiniz seçin ve ardından hello seçin **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="85c0d-135">Select your instance of Workplace by Facebook, and then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="85c0d-136">Ayarlama **sağlama modu** çok**otomatik**.</span><span class="sxs-lookup"><span data-stu-id="85c0d-136">Set **Provisioning Mode** too**Automatic**.</span></span> 

    ![Çalışma alanına ekran görüntüsü tarafından Facebook sağlama seçenekleri](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="85c0d-138">Hello altında **yönetici kimlik bilgileri** bölümünde, hello girin **gizli belirteci** ve hello **Kiracı URL** Facebook yönetici tarafından çalışma alanı.</span><span class="sxs-lookup"><span data-stu-id="85c0d-138">Under hello **Admin Credentials** section, enter hello **Secret Token** and hello **Tenant URL** of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="85c0d-139">Hello Azure portal, seçin **Bağlantıyı Sına** tooensure Azure AD, Facebook uygulaması tarafından tooyour çalışma alanına bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="85c0d-139">In hello Azure portal, select **Test Connection** tooensure Azure AD can connect tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="85c0d-140">Merhaba bağlantı başarısız olursa işyeriniz Facebook hesabına göre takım yönetici izinleri olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="85c0d-140">If hello connection fails, ensure that your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="85c0d-141">Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve hello onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="85c0d-141">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello check box.</span></span>

8. <span data-ttu-id="85c0d-142">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="85c0d-142">Select **Save**.</span></span>

9. <span data-ttu-id="85c0d-143">Hello eşlemeleri bölümü altında seçin **Facebook tarafından Azure Active Directory Kullanıcıları Eşitle tooWorkplace**.</span><span class="sxs-lookup"><span data-stu-id="85c0d-143">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooWorkplace by Facebook**.</span></span>

10. <span data-ttu-id="85c0d-144">Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooWorkplace Facebook tarafından eşitlenen hello kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="85c0d-144">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooWorkplace by Facebook.</span></span> <span data-ttu-id="85c0d-145">Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları çalışma Facebook tarafından güncelleştirme işlemleri için özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="85c0d-145">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="85c0d-146">herhangi bir değişiklik toocommit seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="85c0d-146">toocommit any changes, select **Save**.</span></span>

11. <span data-ttu-id="85c0d-147">tooenable hello Azure AD sağlama hizmetinde tarafından Facebook, çalışma alanı için hello **ayarları** bölümünde, hello değiştirme **sağlama durumu** çok**üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="85c0d-147">tooenable hello Azure AD provisioning service for Workplace by Facebook, in hello **Settings** section, change hello **Provisioning Status** too**On**.</span></span>

12. <span data-ttu-id="85c0d-148">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="85c0d-148">Select **Save**.</span></span>

<span data-ttu-id="85c0d-149">Hakkında daha fazla bilgi için hazırlama, otomatik tooconfigure bkz [Facebook belgelerine hello](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span><span class="sxs-lookup"><span data-stu-id="85c0d-149">For more information on how tooconfigure automatic provisioning, see [hello Facebook documentation](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span></span>

<span data-ttu-id="85c0d-150">Şimdi sınama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85c0d-150">You can now create a test account.</span></span> <span data-ttu-id="85c0d-151">İçin Facebook tarafından tooWorkplace hello hesap tooverify eşitlenmiş too20 dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="85c0d-151">Wait for up too20 minutes tooverify that hello account has been synchronized tooWorkplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="85c0d-152">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="85c0d-152">Additional resources</span></span>

* [<span data-ttu-id="85c0d-153">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="85c0d-153">Managing user account provisioning for enterprise apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="85c0d-154">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="85c0d-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="85c0d-155">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="85c0d-155">Configure single sign-on</span></span>](active-directory-saas-facebook-at-work-tutorial.md)

