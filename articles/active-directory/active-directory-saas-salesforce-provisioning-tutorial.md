---
title: "Öğretici: Azure Active Directory Tümleştirme Salesforce ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Salesforce arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: a916be8dbf0b4c6173cda873936a53cd1f3ff12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a><span data-ttu-id="b50f0-103">Öğretici: Salesforce otomatik kullanıcı sağlamayı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b50f0-103">Tutorial: Configuring Salesforce for Automatic User Provisioning</span></span>

<span data-ttu-id="b50f0-104">Bu öğreticinin Hello hedefi tooshow hello adımları gerekli tooperform Salesforce ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarında bulunan Azure AD tooSalesforce ' dir.</span><span class="sxs-lookup"><span data-stu-id="b50f0-104">hello objective of this tutorial is tooshow hello steps required tooperform in Salesforce and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSalesforce.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b50f0-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b50f0-105">Prerequisites</span></span>

<span data-ttu-id="b50f0-106">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="b50f0-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="b50f0-107">Bir Azure Active directory kiracısı.</span><span class="sxs-lookup"><span data-stu-id="b50f0-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="b50f0-108">İş veya eğitim için Salesforce Salesforce için geçerli bir kiracı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b50f0-108">You must have a valid tenant for Salesforce for Work or Salesforce for Education.</span></span> <span data-ttu-id="b50f0-109">Ücretsiz bir deneme hesabı ya da hizmet için kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="b50f0-109">You may use a free trial     account for either service.</span></span>
*   <span data-ttu-id="b50f0-110">Salesforce takım yönetici izinlerine sahip bir kullanıcı hesabının.</span><span class="sxs-lookup"><span data-stu-id="b50f0-110">A user account in Salesforce with Team Admin permissions.</span></span>

## <a name="assigning-users-toosalesforce"></a><span data-ttu-id="b50f0-111">Kullanıcıların tooSalesforce atama</span><span class="sxs-lookup"><span data-stu-id="b50f0-111">Assigning users tooSalesforce</span></span>

<span data-ttu-id="b50f0-112">Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır.</span><span class="sxs-lookup"><span data-stu-id="b50f0-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="b50f0-113">Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="b50f0-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="b50f0-114">Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya tooyour Salesforce uygulamasına erişmesi Azure AD temsil hello kullanıcılar gruplarında toodecide gerekir.</span><span class="sxs-lookup"><span data-stu-id="b50f0-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Salesforce app.</span></span> <span data-ttu-id="b50f0-115">Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour Salesforce uygulamasına atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b50f0-115">Once decided, you can assign these users tooyour Salesforce app by following hello instructions here:</span></span>

[<span data-ttu-id="b50f0-116">Bir kullanıcı veya grup tooan kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="b50f0-116">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce"></a><span data-ttu-id="b50f0-117">Kullanıcıların tooSalesforce atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="b50f0-117">Important tips for assigning users tooSalesforce</span></span>

*   <span data-ttu-id="b50f0-118">Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooSalesforce tootest hello atanır.</span><span class="sxs-lookup"><span data-stu-id="b50f0-118">It is recommended that a single Azure AD user is assigned tooSalesforce tootest hello provisioning configuration.</span></span> <span data-ttu-id="b50f0-119">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="b50f0-119">Additional users and/or groups may be assigned later.</span></span>

*  <span data-ttu-id="b50f0-120">Bir kullanıcı tooSalesforce atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b50f0-120">When assigning a user tooSalesforce, you must select a valid user role.</span></span> <span data-ttu-id="b50f0-121">Merhaba "Varsayılan erişim" rolü sağlama için çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="b50f0-121">hello "Default Access" role does not work for provisioning</span></span>

    > [!NOTE]
    > <span data-ttu-id="b50f0-122">Bu uygulamayı Salesforce sağlama işlemi, hangi hello müşteri tooselect kullanıcılar atarken isteyebilirsiniz hello bir parçası olarak özel roller alır</span><span class="sxs-lookup"><span data-stu-id="b50f0-122">This app imports custom roles from Salesforce as part of hello provisioning process, which hello customer may want tooselect when assigning users</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="b50f0-123">Otomatik kullanıcı sağlamayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="b50f0-123">Enable Automated User Provisioning</span></span>

<span data-ttu-id="b50f0-124">Bu bölümde, Azure AD tooSalesforce kullanıcının kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve Azure AD'de kullanıcı ve grup atama göre Salesforce atanan kullanıcı hesaplarında devre dışı bırak .</span><span class="sxs-lookup"><span data-stu-id="b50f0-124">This section guides you through connecting your Azure AD tooSalesforce's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Salesforce based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="b50f0-125">Sağlanan hello yönergeleri izleyerek Salesforce için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b50f0-125">You may also choose tooenabled SAML-based Single Sign-On for Salesforce, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b50f0-126">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="b50f0-126">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="b50f0-127">tooconfigure otomatik olarak bir kullanıcı hesabı sağlama:</span><span class="sxs-lookup"><span data-stu-id="b50f0-127">tooconfigure automatic user account provisioning:</span></span>

<span data-ttu-id="b50f0-128">Bu bölümde Hello amacı olan toooutline tooSalesforce tooenable Active Directory kullanıcısı kullanıcı sağlamayı nasıl hesapları.</span><span class="sxs-lookup"><span data-stu-id="b50f0-128">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooSalesforce.</span></span>

1. <span data-ttu-id="b50f0-129">Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="b50f0-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="b50f0-130">Çoklu oturum açma için zaten Salesforce yapılandırdıysanız, hello arama alanı kullanarak Salesforce Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="b50f0-130">If you have already configured Salesforce for single sign-on, search for your instance of Salesforce using hello search field.</span></span> <span data-ttu-id="b50f0-131">Aksi takdirde seçin **Ekle** arayın ve **Salesforce** hello uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="b50f0-131">Otherwise, select **Add** and search for **Salesforce** in hello application gallery.</span></span> <span data-ttu-id="b50f0-132">Salesforce hello Arama sonuçlarından seçin ve uygulamaların tooyour listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b50f0-132">Select Salesforce from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="b50f0-133">Salesforce örneğiniz seçin ve ardından hello **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="b50f0-133">Select your instance of Salesforce, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="b50f0-134">Set hello **sağlama modu** çok**otomatik**.</span><span class="sxs-lookup"><span data-stu-id="b50f0-134">Set hello **Provisioning Mode** too**Automatic**.</span></span> 
<span data-ttu-id="b50f0-135">![sağlama](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span><span class="sxs-lookup"><span data-stu-id="b50f0-135">![provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span></span>

5. <span data-ttu-id="b50f0-136">Merhaba altında **yönetici kimlik bilgileri** bölümünde, yapılandırma ayarlarını aşağıdaki hello sağlayın:</span><span class="sxs-lookup"><span data-stu-id="b50f0-136">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="b50f0-137">a.</span><span class="sxs-lookup"><span data-stu-id="b50f0-137">a.</span></span> <span data-ttu-id="b50f0-138">Merhaba, **yönetici kullanıcı adı** metin kutusuna, bir Salesforce hesap hello sahip adı türü **Sistem Yöneticisi** atanan Salesforce.com profilinde.</span><span class="sxs-lookup"><span data-stu-id="b50f0-138">In hello **Admin User Name** textbox, type a Salesforce account name that has hello **System Administrator** profile in Salesforce.com assigned.</span></span>
   
    <span data-ttu-id="b50f0-139">b.</span><span class="sxs-lookup"><span data-stu-id="b50f0-139">b.</span></span> <span data-ttu-id="b50f0-140">Merhaba, **yönetici parolası** metin kutusuna, bu hesap için hello parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="b50f0-140">In hello **Admin Password** textbox, type hello password for this account.</span></span>

6. <span data-ttu-id="b50f0-141">tooget, Salesforce güvenlik belirtecinizdeki yeni bir sekme açın ve hello aynı oturum Salesforce yönetici hesabı.</span><span class="sxs-lookup"><span data-stu-id="b50f0-141">tooget your Salesforce security token, open a new tab and sign into hello same Salesforce admin account.</span></span> <span data-ttu-id="b50f0-142">Merhaba sağ üst köşesinde başlangıç sayfası, adınıza tıklayın ve ardından **My ayarları**.</span><span class="sxs-lookup"><span data-stu-id="b50f0-142">On hello top right corner of hello page, click your name, and then click **My Settings**.</span></span>

     <span data-ttu-id="b50f0-143">![Otomatik kullanıcı sağlamayı etkinleştirin](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "otomatik kullanıcı sağlamayı etkinleştirin")</span><span class="sxs-lookup"><span data-stu-id="b50f0-143">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span></span>
7. <span data-ttu-id="b50f0-144">Merhaba sol gezinti bölmesinde tıklatın **kişisel** tooexpand hello ilgili bölümü ve ardından **sıfırlama My güvenlik belirteci**.</span><span class="sxs-lookup"><span data-stu-id="b50f0-144">On hello left navigation pane, click **Personal** tooexpand hello related section, and then click **Reset My Security Token**.</span></span>
  
    <span data-ttu-id="b50f0-145">![Otomatik kullanıcı sağlamayı etkinleştirin](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "otomatik kullanıcı sağlamayı etkinleştirin")</span><span class="sxs-lookup"><span data-stu-id="b50f0-145">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span></span>
8. <span data-ttu-id="b50f0-146">Merhaba üzerinde **sıfırlama My güvenlik belirteci** sayfasında, **güvenlik belirteci sıfırlama** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b50f0-146">On hello **Reset My Security Token** page, click **Reset Security Token** button.</span></span>

    <span data-ttu-id="b50f0-147">![Otomatik kullanıcı sağlamayı etkinleştirin](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "otomatik kullanıcı sağlamayı etkinleştirin")</span><span class="sxs-lookup"><span data-stu-id="b50f0-147">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span></span>
9. <span data-ttu-id="b50f0-148">Bu yönetici hesabıyla ilişkili hello e-posta gelen kutusunu kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="b50f0-148">Check hello email inbox associated with this admin account.</span></span> <span data-ttu-id="b50f0-149">Bir e-postadan hello yeni güvenlik belirteci içeriyor Salesforce.com arayın.</span><span class="sxs-lookup"><span data-stu-id="b50f0-149">Look for an email from Salesforce.com that contains hello new security token.</span></span>
10. <span data-ttu-id="b50f0-150">Hello belirteci, Git tooyour Azure AD penceresi kopyalama ve hello yapıştırma **yuva belirteci** alan.</span><span class="sxs-lookup"><span data-stu-id="b50f0-150">Copy hello token, go tooyour Azure AD window, and paste it into hello **Socket Token** field.</span></span>

11. <span data-ttu-id="b50f0-151">Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour Salesforce uygulamasına bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="b50f0-151">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Salesforce app.</span></span>

12. <span data-ttu-id="b50f0-152">Merhaba, **bildirim e-posta** alan, bir kişi veya grubun sağlama hata bildirimleri almak ve hello aşağıdaki onay hello e-posta adresini girin.</span><span class="sxs-lookup"><span data-stu-id="b50f0-152">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox below.</span></span>

13. <span data-ttu-id="b50f0-153">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="b50f0-153">Click **Save.**</span></span>  
    
14.  <span data-ttu-id="b50f0-154">Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooSalesforce.**</span><span class="sxs-lookup"><span data-stu-id="b50f0-154">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSalesforce.**</span></span>

15. <span data-ttu-id="b50f0-155">Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooSalesforce eşitlenir hello kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="b50f0-155">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooSalesforce.</span></span> <span data-ttu-id="b50f0-156">Seçilen öznitelikler hello Not **eşleşen** özelliklerdir Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları Salesforce içinde güncelleştirme işlemleri için.</span><span class="sxs-lookup"><span data-stu-id="b50f0-156">Note that hello attributes selected as **Matching** properties are used toomatch hello user accounts in Salesforce for update operations.</span></span> <span data-ttu-id="b50f0-157">Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.</span><span class="sxs-lookup"><span data-stu-id="b50f0-157">Select hello Save button toocommit any changes.</span></span>

16. <span data-ttu-id="b50f0-158">tooenable hello Salesforce, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello ayarları bölümünün içinde</span><span class="sxs-lookup"><span data-stu-id="b50f0-158">tooenable hello Azure AD provisioning service for Salesforce, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

17. <span data-ttu-id="b50f0-159">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="b50f0-159">Click **Save.**</span></span>

<span data-ttu-id="b50f0-160">Bu, herhangi bir kullanıcı ve/veya hello kullanıcılar tooSalesforce ve Gruplar bölümü atanan gruplarını hello ilk eşitleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="b50f0-160">This starts hello initial synchronization of any users and/or groups assigned tooSalesforce in hello Users and Groups section.</span></span> <span data-ttu-id="b50f0-161">Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform öncelikli olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="b50f0-161">Note that hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="b50f0-162">Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve Salesforce uygulama hizmeti sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.</span><span class="sxs-lookup"><span data-stu-id="b50f0-162">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Salesforce app.</span></span>

<span data-ttu-id="b50f0-163">Şimdi sınama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b50f0-163">You can now create a test account.</span></span> <span data-ttu-id="b50f0-164">TooSalesforce hello hesap tooverify eşitlenmiş too20 dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="b50f0-164">Wait for up too20 minutes tooverify that hello account has been synchronized tooSalesforce.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b50f0-165">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b50f0-165">Additional resources</span></span>

* [<span data-ttu-id="b50f0-166">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="b50f0-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b50f0-167">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="b50f0-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b50f0-168">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="b50f0-168">Configure Single Sign-on</span></span>](active-directory-saas-salesforce-tutorial.md)