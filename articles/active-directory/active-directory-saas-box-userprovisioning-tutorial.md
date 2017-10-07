---
title: "Öğretici: Azure Active Directory Tümleştirme kutusuyla | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin kutusunu ve Azure Active Directory arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c959595-6e57-4954-9c0d-67ba03ee212b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: e92baabb174642c22c99e2a30bc9c71845b3b75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-box-for-automatic-user-provisioning"></a><span data-ttu-id="3bea8-103">Öğretici: Kutusunu otomatik kullanıcı sağlamayı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3bea8-103">Tutorial: Configuring Box for Automatic User Provisioning</span></span>

<span data-ttu-id="3bea8-104">Bu öğreticinin Hello hedefi kutusunu ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooBox tooperform gereken tooshow hello adımları ' dir.</span><span class="sxs-lookup"><span data-stu-id="3bea8-104">hello objective of this tutorial is tooshow hello steps you need tooperform in Box and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooBox.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3bea8-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3bea8-105">Prerequisites</span></span>

<span data-ttu-id="3bea8-106">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="3bea8-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="3bea8-107">Bir Azure Active directory kiracısı.</span><span class="sxs-lookup"><span data-stu-id="3bea8-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="3bea8-108">Bir kutusunu çoklu oturum açma etkin abonelik.</span><span class="sxs-lookup"><span data-stu-id="3bea8-108">A Box single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="3bea8-109">Takım yönetici izinlerine sahip bir kullanıcı hesabı kutusunda.</span><span class="sxs-lookup"><span data-stu-id="3bea8-109">A user account in Box with Team Admin permissions.</span></span>

## <a name="assigning-users-toobox"></a><span data-ttu-id="3bea8-110">Kullanıcıların tooBox atama</span><span class="sxs-lookup"><span data-stu-id="3bea8-110">Assigning users tooBox</span></span> 

<span data-ttu-id="3bea8-111">Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır.</span><span class="sxs-lookup"><span data-stu-id="3bea8-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="3bea8-112">Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="3bea8-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="3bea8-113">Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya tooyour kutusunu uygulamasına erişmesi Azure AD temsil hello kullanıcılar gruplarında toodecide gerekir.</span><span class="sxs-lookup"><span data-stu-id="3bea8-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Box app.</span></span> <span data-ttu-id="3bea8-114">Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooyour Box uygulamasına atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3bea8-114">Once decided, you can assign these users tooyour Box app by following hello instructions here:</span></span>

[<span data-ttu-id="3bea8-115">Bir kullanıcı veya grup tooan kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="3bea8-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

## <a name="assign-users-and-groups"></a><span data-ttu-id="3bea8-116">Kullanıcılar ve gruplar atayın</span><span class="sxs-lookup"><span data-stu-id="3bea8-116">Assign users and groups</span></span>
<span data-ttu-id="3bea8-117">Merhaba **kutusunu > Kullanıcılar ve gruplar** hello Azure portal sekmesinde hangi kullanıcıların ve grupların verilmesi erişim tooBox toospecify sağlar.</span><span class="sxs-lookup"><span data-stu-id="3bea8-117">hello **Box > Users and Groups** tab in hello Azure portal allows you toospecify which users and groups should be granted access tooBox.</span></span> <span data-ttu-id="3bea8-118">Bir kullanıcı veya grup ataması şeyler toooccur aşağıdaki hello neden olur:</span><span class="sxs-lookup"><span data-stu-id="3bea8-118">Assignment of a user or group causes hello following things toooccur:</span></span>

* <span data-ttu-id="3bea8-119">Azure AD hello atanan kullanıcı (da doğrudan atama veya grup üyeliği) tooauthenticate tooBox izin verir.</span><span class="sxs-lookup"><span data-stu-id="3bea8-119">Azure AD permits hello assigned user (either by direct assignment or group membership) tooauthenticate tooBox.</span></span> <span data-ttu-id="3bea8-120">Bir kullanıcı atanmamışsa, Azure AD bunları toosign tooBox içinde izin vermez ve hello Azure AD oturum açma sayfasında bir hata döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bea8-120">If a user is not assigned, then Azure AD does not permit them toosign in tooBox and returns an error on hello Azure AD sign-in page.</span></span>
* <span data-ttu-id="3bea8-121">Bir uygulama bölme kutusu için toohello kullanıcının eklenir [uygulama Başlatıcısı](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span><span class="sxs-lookup"><span data-stu-id="3bea8-121">An app tile for Box is added toohello user's [application launcher](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>
* <span data-ttu-id="3bea8-122">Otomatik sağlama etkinleştirildiğinde otomatik olarak sağlanan sıra toobe sağlama toohello hello atanan kullanıcılar ve/veya grupları eklenir.</span><span class="sxs-lookup"><span data-stu-id="3bea8-122">If automatic provisioning is enabled, then hello assigned users and/or groups are added toohello provisioning queue toobe automatically provisioned.</span></span>
  
  * <span data-ttu-id="3bea8-123">Yalnızca kullanıcı nesneleri sağlanan yapılandırılmış toobe bundan sonra tüm doğrudan atanan kullanıcılar hello sağlama kuyruğuna yerleştirilir ve hiçbir atanan gruplarının üyeleri olan tüm kullanıcıları sıra sağlama hello yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3bea8-123">If only user objects were configured toobe provisioned, then all directly assigned users are placed in hello provisioning queue, and all users that are members of any assigned groups are placed in hello provisioning queue.</span></span> 
  * <span data-ttu-id="3bea8-124">Grup nesneleri sağlanan yapılandırılmış toobe olsaydı, tüm atanmış olan Grup nesneleri sağlanan tooBox ve bu grupların üyeleri olan tüm kullanıcılar ' dir.</span><span class="sxs-lookup"><span data-stu-id="3bea8-124">If group objects were configured toobe provisioned, then all assigned group objects are provisioned tooBox, and all users that are members of those groups.</span></span> <span data-ttu-id="3bea8-125">Merhaba grup ve kullanıcı üyeliklerini tooBox üzerine yazılan korunur.</span><span class="sxs-lookup"><span data-stu-id="3bea8-125">hello group and user memberships are preserved upon being written tooBox.</span></span>

<span data-ttu-id="3bea8-126">Merhaba kullanabilirsiniz **öznitelikleri > çoklu oturum açma** hangi kullanıcı öznitelikleri (veya talep) sunulur tooBox SAML tabanlı kimlik doğrulaması ve hello sırasında tooconfigure sekmesinde **öznitelikleri > sağlama** Kullanıcı ve grup öznitelikleri işlemleri sağlama sırasında Azure AD tooBox nasıl gerçekleştiğini tooconfigure sekmesi.</span><span class="sxs-lookup"><span data-stu-id="3bea8-126">You can use hello **Attributes > Single Sign-On** tab tooconfigure which user attributes (or claims) are presented tooBox during SAML-based authentication, and hello **Attributes > Provisioning** tab tooconfigure how user and group attributes flow from Azure AD tooBox during provisioning operations.</span></span>

### <a name="important-tips-for-assigning-users-toobox"></a><span data-ttu-id="3bea8-127">Kullanıcıların tooBox atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="3bea8-127">Important tips for assigning users tooBox</span></span> 

*   <span data-ttu-id="3bea8-128">Önerilir tek bir Azure AD kullanıcı tarafından atanan tooBox tootest hello yapılandırma sağlama.</span><span class="sxs-lookup"><span data-stu-id="3bea8-128">It is recommended that a single Azure AD user assigned tooBox tootest hello provisioning configuration.</span></span> <span data-ttu-id="3bea8-129">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="3bea8-129">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="3bea8-130">Bir kullanıcı toobox atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3bea8-130">When assigning a user toobox, you must select a valid user role.</span></span> <span data-ttu-id="3bea8-131">Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="3bea8-131">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="3bea8-132">Otomatik kullanıcı sağlamayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="3bea8-132">Enable Automated User Provisioning</span></span>

<span data-ttu-id="3bea8-133">Bu bölümde Azure AD tooBox kullanıcının kullanıcı hesabı API sağlama konusunda size rehberlik eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve atanan kullanıcı hesapları Azure AD'de kullanıcı ve grup atama göre kutusundaki devre dışı bırak.</span><span class="sxs-lookup"><span data-stu-id="3bea8-133">This section guides through connecting your Azure AD tooBox's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Box based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="3bea8-134">Otomatik sağlama etkinleştirildiğinde otomatik olarak sağlanan sıra toobe sağlama toohello hello atanan kullanıcılar ve/veya grupları eklenir.</span><span class="sxs-lookup"><span data-stu-id="3bea8-134">If automatic provisioning is enabled, then hello assigned users and/or groups are added toohello provisioning queue toobe automatically provisioned.</span></span>
    
 * <span data-ttu-id="3bea8-135">Yalnızca, doğrudan atanan kullanıcılar hello sağlama kuyruğuna yerleştirilir ve hiçbir atanan gruplarının üyeleri olan tüm kullanıcıları sıra sağlama hello yerleştirilir sağlanan yapılandırılmış toobe kullanıcı nesneleridir.</span><span class="sxs-lookup"><span data-stu-id="3bea8-135">If only user objects are configured toobe provisioned, then directly assigned users are placed in hello provisioning queue, and all users that are members of any assigned groups are placed in hello provisioning queue.</span></span> 
    
 * <span data-ttu-id="3bea8-136">Grup nesneleri sağlanan yapılandırılmış toobe olsaydı, tüm atanmış olan Grup nesneleri sağlanan tooBox ve bu grupların üyeleri olan tüm kullanıcılar ' dir.</span><span class="sxs-lookup"><span data-stu-id="3bea8-136">If group objects were configured toobe provisioned, then all assigned group objects are provisioned tooBox, and all users that are members of those groups.</span></span> <span data-ttu-id="3bea8-137">Merhaba grup ve kullanıcı üyeliklerini tooBox üzerine yazılan korunur.</span><span class="sxs-lookup"><span data-stu-id="3bea8-137">hello group and user memberships are preserved upon being written tooBox.</span></span>

> [!TIP] 
> <span data-ttu-id="3bea8-138">SAML tabanlı çoklu oturum açma sağlanan hello yönergeleri izleyerek kutusunu tooenabled tercih edebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3bea8-138">You may also choose tooenabled SAML-based Single Sign-On for Box, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="3bea8-139">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="3bea8-139">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="3bea8-140">tooconfigure otomatik olarak bir kullanıcı hesabı sağlama:</span><span class="sxs-lookup"><span data-stu-id="3bea8-140">tooconfigure automatic user account provisioning:</span></span>

<span data-ttu-id="3bea8-141">Bu bölümde Hello amacı olan toooutline nasıl tooenable Active Directory kullanıcısı sağlama tooBox hesapları.</span><span class="sxs-lookup"><span data-stu-id="3bea8-141">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooBox.</span></span>

1. <span data-ttu-id="3bea8-142">Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="3bea8-142">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="3bea8-143">Çoklu oturum açma için kutusu zaten yapılandırdıysanız hello arama alanı kullanarak kutusunu Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="3bea8-143">If you have already configured Box for single sign-on, search for your instance of Box using hello search field.</span></span> <span data-ttu-id="3bea8-144">Aksi takdirde seçin **Ekle** arayın ve **kutusunu** hello uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="3bea8-144">Otherwise, select **Add** and search for **Box** in hello application gallery.</span></span> <span data-ttu-id="3bea8-145">Hello Arama sonuçlarından kutusunu seçin ve uygulamaların tooyour listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3bea8-145">Select Box from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="3bea8-146">Örneğiniz kutusunu seçin ve ardından hello **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="3bea8-146">Select your instance of Box, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="3bea8-147">Set hello **sağlama modu** çok**otomatik**.</span><span class="sxs-lookup"><span data-stu-id="3bea8-147">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Sağlama](./media/active-directory-saas-box-userprovisioning-tutorial/provisioning.png)

5. <span data-ttu-id="3bea8-149">Merhaba altında **yönetici kimlik bilgileri** 'yi tıklatın **Authorize** tooopen bir kutusunun oturum açma iletişim kutusunda yeni bir tarayıcı penceresi.</span><span class="sxs-lookup"><span data-stu-id="3bea8-149">Under hello **Admin Credentials** section, click **Authorize** tooopen a Box login dialog in a new browser window.</span></span>

6. <span data-ttu-id="3bea8-150">Merhaba üzerinde **oturum açma toogrant erişim tooBox** sayfasında, gerekli hello kimlik bilgilerini sağlayın ve ardından **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="3bea8-150">On hello **Login toogrant access tooBox** page, provide hello required credentials, and then click **Authorize**.</span></span> 
   
    <span data-ttu-id="3bea8-151">![Otomatik kullanıcı sağlamayı etkinleştirin](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "otomatik kullanıcı sağlamayı etkinleştirin")</span><span class="sxs-lookup"><span data-stu-id="3bea8-151">![Enable automatic user provisioning](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "Enable automatic user provisioning")</span></span>

7. <span data-ttu-id="3bea8-152">Tıklatın **Grant erişim tooBox** tooauthorize bu işlemi ve tooreturn toohello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="3bea8-152">Click **Grant access tooBox** tooauthorize this operation and tooreturn toohello Azure portal.</span></span> 
   
    <span data-ttu-id="3bea8-153">![Otomatik kullanıcı sağlamayı etkinleştirin](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "otomatik kullanıcı sağlamayı etkinleştirin")</span><span class="sxs-lookup"><span data-stu-id="3bea8-153">![Enable automatic user provisioning](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "Enable automatic user provisioning")</span></span>

8. <span data-ttu-id="3bea8-154">Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD tooyour Box uygulamasına bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="3bea8-154">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Box app.</span></span> <span data-ttu-id="3bea8-155">Merhaba bağlantı başarısız olursa kutusunu hesabınızın Team yönetici izinlerine sahip olduğundan emin olun ve hello deneyin **"Yetkilendir"** adım yeniden uygulayın.</span><span class="sxs-lookup"><span data-stu-id="3bea8-155">If hello connection fails, ensure your Box account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

9. <span data-ttu-id="3bea8-156">Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve hello onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="3bea8-156">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

10. <span data-ttu-id="3bea8-157">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="3bea8-157">Click **Save.**</span></span>

11. <span data-ttu-id="3bea8-158">Hello eşlemeleri bölümü altında seçin **eşitleme Azure Active Directory Kullanıcıları tooBox.**</span><span class="sxs-lookup"><span data-stu-id="3bea8-158">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooBox.**</span></span>

12. <span data-ttu-id="3bea8-159">Merhaba, **öznitelik eşlemelerini** bölümünde, Azure AD tooBox eşitlenir hello kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="3bea8-159">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooBox.</span></span> <span data-ttu-id="3bea8-160">Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları kutusunda güncelleştirme işlemleri için özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="3bea8-160">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Box for update operations.</span></span> <span data-ttu-id="3bea8-161">Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.</span><span class="sxs-lookup"><span data-stu-id="3bea8-161">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="3bea8-162">tooenable hello Azure AD sağlama hizmeti kutusunu değişiklik hello **sağlama durumu** çok**üzerinde** hello ayarları bölümünün içinde</span><span class="sxs-lookup"><span data-stu-id="3bea8-162">tooenable hello Azure AD provisioning service for Box, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

14. <span data-ttu-id="3bea8-163">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="3bea8-163">Click **Save.**</span></span>

<span data-ttu-id="3bea8-164">Herhangi bir kullanıcı ve/veya hello kullanıcılar tooBox ve Gruplar bölümü atanan gruplarını hello ilk eşitleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="3bea8-164">That starts hello initial synchronization of any users and/or groups assigned tooBox in hello Users and Groups section.</span></span> <span data-ttu-id="3bea8-165">Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır.</span><span class="sxs-lookup"><span data-stu-id="3bea8-165">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="3bea8-166">Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve hizmet kutusunu uygulamanızdan sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.</span><span class="sxs-lookup"><span data-stu-id="3bea8-166">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Box app.</span></span>

<span data-ttu-id="3bea8-167">Şimdi sınama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bea8-167">You can now create a test account.</span></span> <span data-ttu-id="3bea8-168">Toobox hello hesap tooverify eşitlenmiş too20 dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="3bea8-168">Wait for up too20 minutes tooverify that hello account has been synchronized toobox.</span></span>

<span data-ttu-id="3bea8-169">Altında listelenen kutusunu kiracınızda eşitlenmiş kullanıcıları **yönetilen kullanıcılara** hello içinde **Yönetici Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="3bea8-169">In your Box tenant, synchronized users are listed under **Managed Users** in hello **Admin Console**.</span></span>

<span data-ttu-id="3bea8-170">![Tümleştirme durumu](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "tümleştirme durumu")</span><span class="sxs-lookup"><span data-stu-id="3bea8-170">![Integration status](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "Integration status")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="3bea8-171">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="3bea8-171">Additional resources</span></span>

* [<span data-ttu-id="3bea8-172">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="3bea8-172">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3bea8-173">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="3bea8-173">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="3bea8-174">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="3bea8-174">Configure Single Sign-on</span></span>](active-directory-saas-box-tutorial.md)