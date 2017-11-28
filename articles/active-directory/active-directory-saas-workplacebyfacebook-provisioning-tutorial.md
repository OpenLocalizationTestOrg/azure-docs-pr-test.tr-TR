---
title: "Öğretici: Azure Active Directory Tümleştirme ile çalışma alanına Facebook tarafından | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Facebook ile çalışma alanına arasında."
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
ms.openlocfilehash: 551ec353a5ec1da936373587688c299a6f4acca7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="cc02a-103">Öğretici: Kullanıcı sağlamak için çalışma alanına Facebook ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cc02a-103">Tutorial: Configuring Workplace by Facebook for User Provisioning</span></span>

<span data-ttu-id="cc02a-104">Bu öğreticinin Hello hedefi çalışma tooperform Facebook ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooWorkplace Facebook tarafından tarafından gereken adımları hello tooshow ' dir.</span><span class="sxs-lookup"><span data-stu-id="cc02a-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Workplace by Facebook and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooWorkplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc02a-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cc02a-105">Prerequisites</span></span>

<span data-ttu-id="cc02a-106">Facebook ile çalışma alanına ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="cc02a-106">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="cc02a-107">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="cc02a-107">An Azure AD subscription</span></span>
- <span data-ttu-id="cc02a-108">Facebook çoklu oturum açma etkin abonelik tarafından bir çalışma alanı</span><span class="sxs-lookup"><span data-stu-id="cc02a-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc02a-109">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="cc02a-109">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc02a-110">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="cc02a-110">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc02a-111">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="cc02a-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc02a-112">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc02a-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="cc02a-113">Kullanıcıların tooWorkplace Facebook tarafından atama</span><span class="sxs-lookup"><span data-stu-id="cc02a-113">Assigning users tooWorkplace by Facebook</span></span>

<span data-ttu-id="cc02a-114">Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır.</span><span class="sxs-lookup"><span data-stu-id="cc02a-114">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="cc02a-115">Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="cc02a-115">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="cc02a-116">Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD tooyour çalışma alanına Facebook uygulaması tarafından erişim hello kullanıcıları temsil gruplarında toodecide gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc02a-116">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="cc02a-117">Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour çalışma alanına Facebook uygulaması tarafından atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cc02a-117">Once decided, you can assign these users tooyour Workplace by Facebook app by following hello instructions here:</span></span>

[<span data-ttu-id="cc02a-118">Bir kullanıcı veya grup tooan kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="cc02a-118">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="cc02a-119">Kullanıcıların tooWorkplace Facebook tarafından atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="cc02a-119">Important tips for assigning users tooWorkplace by Facebook</span></span>

*   <span data-ttu-id="cc02a-120">Önerilir tek bir Azure AD kullanıcısının tooWorkplace yapılandırma sağlama Facebook tootest hello tarafından atanır.</span><span class="sxs-lookup"><span data-stu-id="cc02a-120">It is recommended that a single Azure AD user is assigned tooWorkplace by Facebook tootest hello provisioning configuration.</span></span> <span data-ttu-id="cc02a-121">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="cc02a-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="cc02a-122">Bir kullanıcı tooWorkplace Facebook tarafından atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc02a-122">When assigning a user tooWorkplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="cc02a-123">Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="cc02a-123">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="cc02a-124">Kullanıcı sağlamayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="cc02a-124">Enable User Provisioning</span></span>

<span data-ttu-id="cc02a-125">Bu bölümde, Azure AD tooWorkplace Facebook'ın kullanıcı hesabı tarafından API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve çalışma Facebook kullanıcı ve Grup göre tarafından atanan kullanıcı hesapları devre dışı bırak Azure AD'de atama.</span><span class="sxs-lookup"><span data-stu-id="cc02a-125">This section guides you through connecting your Azure AD tooWorkplace by Facebook's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="cc02a-126">İş yeri tarafından sağlanan hello yönergeleri izleyerek Facebook için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cc02a-126">You may also choose tooenabled SAML-based Single Sign-On for Workplace by Facebook, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="cc02a-127">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="cc02a-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a><span data-ttu-id="cc02a-128">Azure AD'de tooWorkplace Facebook tarafından sağlama tooconfigure kullanıcı hesabı:</span><span class="sxs-lookup"><span data-stu-id="cc02a-128">tooconfigure user account provisioning tooWorkplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="cc02a-129">Bu bölümde Hello amacı olan toooutline tooWorkplace Facebook tarafından Active Directory kullanıcısı tooenable sağlama nasıl hesapları.</span><span class="sxs-lookup"><span data-stu-id="cc02a-129">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooWorkplace by Facebook.</span></span>

<span data-ttu-id="cc02a-130">Azure AD destekler Hello özelliği tooautomatically hello hesap ayrıntılarını eşitlemek kullanıcılar tooWorkplace Facebook tarafından atanır.</span><span class="sxs-lookup"><span data-stu-id="cc02a-130">Azure AD supports hello ability tooautomatically synchronize hello account details of assigned users tooWorkplace by Facebook.</span></span> <span data-ttu-id="cc02a-131">Facebook tooget hello verileri, gereken tooauthorize kullanıcılar, erişimi için önce tarafından çalışma alanına bu otomatik eşitlenmesine olanak bunları içinde toosign hello için ilk kez çalışılıyor.</span><span class="sxs-lookup"><span data-stu-id="cc02a-131">This automatic synchronization enables Workplace by Facebook tooget hello data it needs tooauthorize users for access, before them attempting toosign in for hello first time.</span></span> <span data-ttu-id="cc02a-132">Erişim Azure AD'de iptal edilmiş durumda olduğunda, ayrıca çalışma alanına Facebook tarafından kullanıcılardan XML'deki sağlamasını yapar.</span><span class="sxs-lookup"><span data-stu-id="cc02a-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="cc02a-133">Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory** > **Kurumsal uygulamaları** > **tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="cc02a-133">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="cc02a-134">Çoklu oturum açma için zaten çalışma alanına Facebook tarafından yapılandırdıysanız, çalışma alanına hello arama alanı kullanarak Facebook tarafından örneğiniz arayın.</span><span class="sxs-lookup"><span data-stu-id="cc02a-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using hello search field.</span></span> <span data-ttu-id="cc02a-135">Aksi takdirde seçin **Ekle** arayın ve **Facebook ile çalışma alanına** hello uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="cc02a-135">Otherwise, select **Add** and search for **Workplace by Facebook** in hello application gallery.</span></span> <span data-ttu-id="cc02a-136">Merhaba Arama sonuçlarından Facebook tarafından çalışma alanı seçin ve uygulamaların tooyour listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cc02a-136">Select Workplace by Facebook from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="cc02a-137">Facebook ile çalışma alanına örneğiniz seçin, sonra seçin hello **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="cc02a-137">Select your instance of Workplace by Facebook, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="cc02a-138">Set hello **sağlama modu** çok**otomatik**.</span><span class="sxs-lookup"><span data-stu-id="cc02a-138">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Sağlama](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="cc02a-140">Merhaba altında **yönetici kimlik bilgileri** bölümünde hello gizli belirteci girin ve Kiracı URL'si işyeriniz Facebook yönetici tarafından hello.</span><span class="sxs-lookup"><span data-stu-id="cc02a-140">Under hello **Admin Credentials** section, enter hello Secret Token and hello Tenant URL of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="cc02a-141">Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD, Facebook uygulaması tarafından tooyour çalışma alanına bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="cc02a-141">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="cc02a-142">Merhaba bağlantı başarısız olursa işyeriniz Facebook hesabına göre takım yönetici izinleri olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="cc02a-142">If hello connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="cc02a-143">Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve hello onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="cc02a-143">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

8. <span data-ttu-id="cc02a-144">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="cc02a-144">Click **Save.**</span></span>

9. <span data-ttu-id="cc02a-145">Hello eşlemeleri bölümü altında seçin **Facebook tarafından Azure Active Directory Kullanıcıları Eşitle tooWorkplace.**</span><span class="sxs-lookup"><span data-stu-id="cc02a-145">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooWorkplace by Facebook.**</span></span>

10. <span data-ttu-id="cc02a-146">Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooWorkplace Facebook tarafından eşitlenen hello kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="cc02a-146">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooWorkplace by Facebook.</span></span> <span data-ttu-id="cc02a-147">Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları çalışma Facebook tarafından güncelleştirme işlemleri için özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="cc02a-147">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="cc02a-148">Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.</span><span class="sxs-lookup"><span data-stu-id="cc02a-148">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="cc02a-149">tooenable hello Facebook, değişiklik hello tarafından çalışma alanı için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello içinde **ayarları** bölümü</span><span class="sxs-lookup"><span data-stu-id="cc02a-149">tooenable hello Azure AD provisioning service for Workplace by Facebook, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="cc02a-150">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="cc02a-150">Click **Save.**</span></span>

<span data-ttu-id="cc02a-151">Hakkında daha fazla bilgi için hazırlama, otomatik tooconfigure bkz [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span><span class="sxs-lookup"><span data-stu-id="cc02a-151">For more information on how tooconfigure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="cc02a-152">Şimdi sınama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc02a-152">You can now create a test account.</span></span> <span data-ttu-id="cc02a-153">İçin Facebook tarafından tooWorkplace hello hesap tooverify eşitlenmiş too20 dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="cc02a-153">Wait for up too20 minutes tooverify that hello account has been synchronized tooWorkplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cc02a-154">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="cc02a-154">Additional resources</span></span>

* [<span data-ttu-id="cc02a-155">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="cc02a-155">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cc02a-156">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="cc02a-156">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="cc02a-157">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="cc02a-157">Configure Single Sign-on</span></span>](active-directory-saas-workplacebyfacebook-tutorial.md)

