---
title: "Öğretici: Azure Active Directory Tümleştirme ile DocuSign | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile DocuSign arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 294cd6b8-74d7-44bc-92bc-020ccd13ff12
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 8562a8f9e05fb72d3331507b7da5c6afee38f9b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-docusign-for-user-provisioning"></a><span data-ttu-id="70639-103">Öğretici: DocuSign kullanıcı sağlamak için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="70639-103">Tutorial: Configuring DocuSign for User Provisioning</span></span>

<span data-ttu-id="70639-104">Bu öğreticinin Hello hedefi DocuSign ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooDocuSign tooperform gereken adımları hello tooshow ' dir.</span><span class="sxs-lookup"><span data-stu-id="70639-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in DocuSign and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooDocuSign.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70639-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="70639-105">Prerequisites</span></span>

<span data-ttu-id="70639-106">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="70639-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="70639-107">Bir Azure Active directory kiracısı.</span><span class="sxs-lookup"><span data-stu-id="70639-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="70639-108">Bir DocuSign çoklu oturum açma abonelik etkin.</span><span class="sxs-lookup"><span data-stu-id="70639-108">A DocuSign single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="70639-109">Bir kullanıcı hesabında DocuSign takım yönetici izinlerine sahip.</span><span class="sxs-lookup"><span data-stu-id="70639-109">A user account in DocuSign with Team Admin permissions.</span></span>

## <a name="assigning-users-toodocusign"></a><span data-ttu-id="70639-110">Kullanıcıların tooDocuSign atama</span><span class="sxs-lookup"><span data-stu-id="70639-110">Assigning users tooDocuSign</span></span>

<span data-ttu-id="70639-111">Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır.</span><span class="sxs-lookup"><span data-stu-id="70639-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="70639-112">Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="70639-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="70639-113">Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya tooyour DocuSign uygulamasına erişmesi Azure AD temsil hello kullanıcılar gruplarında toodecide gerekir.</span><span class="sxs-lookup"><span data-stu-id="70639-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour DocuSign app.</span></span> <span data-ttu-id="70639-114">Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour DocuSign uygulama atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="70639-114">Once decided, you can assign these users tooyour DocuSign app by following hello instructions here:</span></span>

[<span data-ttu-id="70639-115">Bir kullanıcı veya grup tooan kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="70639-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodocusign"></a><span data-ttu-id="70639-116">Kullanıcıların tooDocuSign atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="70639-116">Important tips for assigning users tooDocuSign</span></span>

*   <span data-ttu-id="70639-117">Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooDocuSign tootest hello atanır.</span><span class="sxs-lookup"><span data-stu-id="70639-117">It is recommended that a single Azure AD user is assigned tooDocuSign tootest hello provisioning configuration.</span></span> <span data-ttu-id="70639-118">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="70639-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="70639-119">Bir kullanıcı tooDocuSign atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="70639-119">When assigning a user tooDocuSign, you must select a valid user role.</span></span> <span data-ttu-id="70639-120">Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="70639-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="70639-121">Kullanıcı sağlamayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="70639-121">Enable User Provisioning</span></span>

<span data-ttu-id="70639-122">Bu bölümde, Azure AD tooDocuSign kullanıcının kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve Azure AD'de kullanıcı ve grup atama göre DocuSign atanan kullanıcı hesaplarında devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="70639-122">This section guides you through connecting your Azure AD tooDocuSign's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in DocuSign based on user and group assignment in Azure AD.</span></span>

> [!Tip]
> <span data-ttu-id="70639-123">Sağlanan hello yönergeleri izleyerek DocuSign için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="70639-123">You may also choose tooenabled SAML-based Single Sign-On for DocuSign, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="70639-124">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="70639-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="70639-125">tooconfigure kullanıcı hesabı sağlama:</span><span class="sxs-lookup"><span data-stu-id="70639-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="70639-126">Bu bölümde Hello amacı olan toooutline tooDocuSign tooenable Active Directory kullanıcısı kullanıcı sağlamayı nasıl hesapları.</span><span class="sxs-lookup"><span data-stu-id="70639-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooDocuSign.</span></span>

1. <span data-ttu-id="70639-127">Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="70639-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="70639-128">Çoklu oturum açma için zaten DocuSign yapılandırdıysanız, hello arama alanı kullanarak DocuSign Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="70639-128">If you have already configured DocuSign for single sign-on, search for your instance of DocuSign using hello search field.</span></span> <span data-ttu-id="70639-129">Aksi takdirde seçin **Ekle** arayın ve **DocuSign** hello uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="70639-129">Otherwise, select **Add** and search for **DocuSign** in hello application gallery.</span></span> <span data-ttu-id="70639-130">Merhaba Arama sonuçlarından DocuSign seçin ve uygulamaların tooyour listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="70639-130">Select DocuSign from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="70639-131">DocuSign örneğiniz seçin ve ardından hello **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="70639-131">Select your instance of DocuSign, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="70639-132">Set hello **sağlama modu** çok**otomatik**.</span><span class="sxs-lookup"><span data-stu-id="70639-132">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Sağlama](./media/active-directory-saas-docusign-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="70639-134">Merhaba altında **yönetici kimlik bilgileri** bölümünde, yapılandırma ayarlarını aşağıdaki hello sağlayın:</span><span class="sxs-lookup"><span data-stu-id="70639-134">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="70639-135">a.</span><span class="sxs-lookup"><span data-stu-id="70639-135">a.</span></span> <span data-ttu-id="70639-136">Merhaba, **yönetici kullanıcı adı** metin kutusuna, bir DocuSign hesap hello sahip adı türü **Sistem Yöneticisi** atanan DocuSign.com profilinde.</span><span class="sxs-lookup"><span data-stu-id="70639-136">In hello **Admin User Name** textbox, type a DocuSign account name that has hello **System Administrator** profile in DocuSign.com assigned.</span></span>
   
    <span data-ttu-id="70639-137">b.</span><span class="sxs-lookup"><span data-stu-id="70639-137">b.</span></span> <span data-ttu-id="70639-138">Merhaba, **yönetici parolası** metin kutusuna, bu hesap için hello parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="70639-138">In hello **Admin Password** textbox, type hello password for this account.</span></span>

6. <span data-ttu-id="70639-139">Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour DocuSign uygulama bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="70639-139">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour DocuSign app.</span></span>

7. <span data-ttu-id="70639-140">Merhaba, **bildirim e-posta** alan, bir kişi veya grubun sağlama hata bildirimleri almak ve hello onay hello e-posta adresini girin.</span><span class="sxs-lookup"><span data-stu-id="70639-140">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox.</span></span>

8. <span data-ttu-id="70639-141">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="70639-141">Click **Save.**</span></span>

9. <span data-ttu-id="70639-142">Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooDocuSign.**</span><span class="sxs-lookup"><span data-stu-id="70639-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooDocuSign.**</span></span>

10. <span data-ttu-id="70639-143">Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooDocuSign eşitlenir hello kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="70639-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooDocuSign.</span></span> <span data-ttu-id="70639-144">Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları DocuSign içinde güncelleştirme işlemleri için özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="70639-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in DocuSign for update operations.</span></span> <span data-ttu-id="70639-145">Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.</span><span class="sxs-lookup"><span data-stu-id="70639-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="70639-146">tooenable hello DocuSign, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello ayarları bölümünün içinde</span><span class="sxs-lookup"><span data-stu-id="70639-146">tooenable hello Azure AD provisioning service for DocuSign, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="70639-147">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="70639-147">Click **Save.**</span></span>

<span data-ttu-id="70639-148">Herhangi bir kullanıcı ve/veya hello kullanıcılar tooDocuSign ve Gruplar bölümü atanan gruplarını hello ilk eşitleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="70639-148">It starts hello initial synchronization of any users and/or groups assigned tooDocuSign in hello Users and Groups section.</span></span> <span data-ttu-id="70639-149">Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır.</span><span class="sxs-lookup"><span data-stu-id="70639-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="70639-150">Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve hizmet DocuSign uygulamanızdan sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.</span><span class="sxs-lookup"><span data-stu-id="70639-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your DocuSign app.</span></span>

<span data-ttu-id="70639-151">Şimdi sınama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70639-151">You can now create a test account.</span></span> <span data-ttu-id="70639-152">TooDocuSign hello hesap tooverify eşitlenmiş too20 dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="70639-152">Wait for up too20 minutes tooverify that hello account has been synchronized tooDocuSign.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="70639-153">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="70639-153">Additional resources</span></span>

* [<span data-ttu-id="70639-154">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="70639-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="70639-155">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="70639-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="70639-156">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="70639-156">Configure Single Sign-on</span></span>](active-directory-saas-docusign-tutorial.md)