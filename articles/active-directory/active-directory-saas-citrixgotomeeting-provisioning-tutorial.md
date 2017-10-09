---
title: "Öğretici: Azure Active Directory Tümleştirme ile Citrix GoToMeeting | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Citrix GoToMeeting arasında."
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
ms.openlocfilehash: 3c6eed5309dfa384c292b0cf63f8aa58988add81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a><span data-ttu-id="0aea7-103">Öğretici: Citrix GoToMeeting otomatik kullanıcı sağlamayı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0aea7-103">Tutorial: Configuring Citrix GoToMeeting for Automatic User Provisioning</span></span>

<span data-ttu-id="0aea7-104">Bu öğreticinin Hello hedefi Citrix GoToMeeting ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooCitrix GoToMeeting tooperform gereken adımları hello tooshow ' dir.</span><span class="sxs-lookup"><span data-stu-id="0aea7-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Citrix GoToMeeting and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooCitrix GoToMeeting.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0aea7-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0aea7-105">Prerequisites</span></span>

<span data-ttu-id="0aea7-106">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="0aea7-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="0aea7-107">Bir Azure Active directory kiracısı.</span><span class="sxs-lookup"><span data-stu-id="0aea7-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="0aea7-108">Bir Citrix GoToMeeting çoklu oturum açma etkin abonelik.</span><span class="sxs-lookup"><span data-stu-id="0aea7-108">A Citrix GoToMeeting single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="0aea7-109">Citrix GoToMeeting takım yönetici izinlerine sahip bir kullanıcı hesabının.</span><span class="sxs-lookup"><span data-stu-id="0aea7-109">A user account in Citrix GoToMeeting with Team Admin permissions.</span></span>

## <a name="assigning-users-toocitrix-gotomeeting"></a><span data-ttu-id="0aea7-110">Kullanıcıların tooCitrix GoToMeeting atama</span><span class="sxs-lookup"><span data-stu-id="0aea7-110">Assigning users tooCitrix GoToMeeting</span></span>

<span data-ttu-id="0aea7-111">Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır.</span><span class="sxs-lookup"><span data-stu-id="0aea7-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="0aea7-112">Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="0aea7-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="0aea7-113">Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD tooyour Citrix GoToMeeting uygulama erişim hello kullanıcıları temsil gruplarında toodecide gerekir.</span><span class="sxs-lookup"><span data-stu-id="0aea7-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Citrix GoToMeeting app.</span></span> <span data-ttu-id="0aea7-114">Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour Citrix GoToMeeting uygulama atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0aea7-114">Once decided, you can assign these users tooyour Citrix GoToMeeting app by following hello instructions here:</span></span>

[<span data-ttu-id="0aea7-115">Bir kullanıcı veya grup tooan kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="0aea7-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toocitrix-gotomeeting"></a><span data-ttu-id="0aea7-116">Kullanıcıların tooCitrix GoToMeeting atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="0aea7-116">Important tips for assigning users tooCitrix GoToMeeting</span></span>

*   <span data-ttu-id="0aea7-117">Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooCitrix GoToMeeting tootest hello atanır.</span><span class="sxs-lookup"><span data-stu-id="0aea7-117">It is recommended that a single Azure AD user is assigned tooCitrix GoToMeeting tootest hello provisioning configuration.</span></span> <span data-ttu-id="0aea7-118">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="0aea7-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="0aea7-119">Bir kullanıcı tooCitrix GoToMeeting atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0aea7-119">When assigning a user tooCitrix GoToMeeting, you must select a valid user role.</span></span> <span data-ttu-id="0aea7-120">Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="0aea7-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="0aea7-121">Otomatik kullanıcı sağlamayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="0aea7-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="0aea7-122">Bu bölümde, API sağlama, Azure AD tooCitrix GoToMeeting'ın kullanıcı hesabı konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve kullanıcı ve Grup Citrix GoToMeeting hesaplarında göre atanan kullanıcı devre dışı bırak Azure AD'de atama.</span><span class="sxs-lookup"><span data-stu-id="0aea7-122">This section guides you through connecting your Azure AD tooCitrix GoToMeeting's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Citrix GoToMeeting based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="0aea7-123">Sağlanan hello yönergeleri izleyerek Citrix GoToMeeting için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0aea7-123">You may also choose tooenabled SAML-based Single Sign-On for Citrix GoToMeeting, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0aea7-124">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="0aea7-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="0aea7-125">tooconfigure otomatik olarak bir kullanıcı hesabı sağlama:</span><span class="sxs-lookup"><span data-stu-id="0aea7-125">tooconfigure automatic user account provisioning:</span></span>

1. <span data-ttu-id="0aea7-126">Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="0aea7-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="0aea7-127">Çoklu oturum açma için Citrix GoToMeeting zaten yapılandırdıysanız Citrix hello arama alanı kullanarak GoToMeeting Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="0aea7-127">If you have already configured Citrix GoToMeeting for single sign-on, search for your instance of Citrix GoToMeeting using hello search field.</span></span> <span data-ttu-id="0aea7-128">Aksi takdirde seçin **Ekle** arayın ve **Citrix GoToMeeting** hello uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="0aea7-128">Otherwise, select **Add** and search for **Citrix GoToMeeting** in hello application gallery.</span></span> <span data-ttu-id="0aea7-129">Citrix GoToMeeting hello Arama sonuçlarından seçin ve uygulamaların tooyour listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0aea7-129">Select Citrix GoToMeeting from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="0aea7-130">Citrix GoToMeeting örneğiniz seçin ve ardından hello **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="0aea7-130">Select your instance of Citrix GoToMeeting, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="0aea7-131">Set hello **sağlama** modu çok**otomatik**.</span><span class="sxs-lookup"><span data-stu-id="0aea7-131">Set hello **Provisioning** Mode too**Automatic**.</span></span> 

    ![Sağlama](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="0aea7-133">Merhaba yönetici kimlik bilgileri bölümü altında hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0aea7-133">Under hello Admin Credentials section, perform hello following steps:</span></span>
   
    <span data-ttu-id="0aea7-134">a.</span><span class="sxs-lookup"><span data-stu-id="0aea7-134">a.</span></span> <span data-ttu-id="0aea7-135">Merhaba, **Citrix GoToMeeting yönetici kullanıcı adı** metin kutusuna, bir yöneticinin türü hello kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="0aea7-135">In hello **Citrix GoToMeeting Admin User Name** textbox, type hello user name of an administrator.</span></span>

    <span data-ttu-id="0aea7-136">b.</span><span class="sxs-lookup"><span data-stu-id="0aea7-136">b.</span></span> <span data-ttu-id="0aea7-137">Merhaba, **Citrix GoToMeeting yönetici parolası** metin kutusuna, hello yöneticinin parola.</span><span class="sxs-lookup"><span data-stu-id="0aea7-137">In hello **Citrix GoToMeeting Admin Password** textbox, hello administrator's password.</span></span>

6. <span data-ttu-id="0aea7-138">Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour Citrix GoToMeeting uygulama bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="0aea7-138">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Citrix GoToMeeting app.</span></span> <span data-ttu-id="0aea7-139">Merhaba bağlantı başarısız olursa, Citrix GoToMeeting hesabınızın Team yönetici izinleri olduğundan emin olun ve hello deneyin **"Yönetici kimlik bilgileri"** adım yeniden uygulayın.</span><span class="sxs-lookup"><span data-stu-id="0aea7-139">If hello connection fails, ensure your Citrix GoToMeeting account has Team Admin permissions and try hello **"Admin Credentials"** step again.</span></span>

7. <span data-ttu-id="0aea7-140">Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve hello onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="0aea7-140">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

8. <span data-ttu-id="0aea7-141">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="0aea7-141">Click **Save.**</span></span>

9. <span data-ttu-id="0aea7-142">Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooCitrix GoToMeeting.**</span><span class="sxs-lookup"><span data-stu-id="0aea7-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooCitrix GoToMeeting.**</span></span>

10. <span data-ttu-id="0aea7-143">Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooCitrix GoToMeeting eşitlenir hello kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="0aea7-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooCitrix GoToMeeting.</span></span> <span data-ttu-id="0aea7-144">Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları Citrix GoToMeeting içinde güncelleştirme işlemleri için özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="0aea7-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Citrix GoToMeeting for update operations.</span></span> <span data-ttu-id="0aea7-145">Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.</span><span class="sxs-lookup"><span data-stu-id="0aea7-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="0aea7-146">tooenable hello Citrix GoToMeeting, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello ayarları bölümünün içinde</span><span class="sxs-lookup"><span data-stu-id="0aea7-146">tooenable hello Azure AD provisioning service for Citrix GoToMeeting, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="0aea7-147">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="0aea7-147">Click **Save.**</span></span>

<span data-ttu-id="0aea7-148">Tüm kullanıcıların hello ilk eşitleme başlar ve/veya gruplarının tooCitrix GoToMeeting hello kullanıcılar ve Gruplar bölümünde atanmış.</span><span class="sxs-lookup"><span data-stu-id="0aea7-148">It starts hello initial synchronization of any users and/or groups assigned tooCitrix GoToMeeting in hello Users and Groups section.</span></span> <span data-ttu-id="0aea7-149">Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır.</span><span class="sxs-lookup"><span data-stu-id="0aea7-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="0aea7-150">Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve Citrix GoToMeeting uygulamanızdan hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.</span><span class="sxs-lookup"><span data-stu-id="0aea7-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Citrix GoToMeeting app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0aea7-151">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="0aea7-151">Additional resources</span></span>

* [<span data-ttu-id="0aea7-152">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="0aea7-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0aea7-153">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="0aea7-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="0aea7-154">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0aea7-154">Configure Single Sign-on</span></span>](active-directory-saas-citrix-gotomeeting-tutorial.md)


