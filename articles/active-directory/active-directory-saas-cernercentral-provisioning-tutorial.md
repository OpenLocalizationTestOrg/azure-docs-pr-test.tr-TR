---
title: "Öğretici: Azure Active Directory ile otomatik kullanıcı sağlamayı Cerner Orta yapılandırma | Microsoft Docs"
description: "Nasıl tooconfigure Azure Active Directory tooautomatically sağlamak kullanıcılar tooa kadrosu Cerner Orta öğrenin."
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
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: e96da98e783d24e7f34ae924824f909eead75f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a><span data-ttu-id="486f3-103">Öğretici: Cerner Orta otomatik kullanıcı sağlamayı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="486f3-103">Tutorial: Configuring Cerner Central for Automatic User Provisioning</span></span>

<span data-ttu-id="486f3-104">Bu öğreticinin Hello hedefi Cerner Orta ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooa kullanıcı kadrosu Cerner Orta tooperform gereken adımları hello tooshow ' dir.</span><span class="sxs-lookup"><span data-stu-id="486f3-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Cerner Central and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooa user roster in Cerner Central.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="486f3-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="486f3-105">Prerequisites</span></span>

<span data-ttu-id="486f3-106">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="486f3-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="486f3-107">Azure Active Directory kiracısı</span><span class="sxs-lookup"><span data-stu-id="486f3-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="486f3-108">Cerner Orta Kiracı</span><span class="sxs-lookup"><span data-stu-id="486f3-108">A Cerner Central tenant</span></span> 

> [!NOTE]
> <span data-ttu-id="486f3-109">Azure Active Directory Cerner hello kullanarak orta ile tümleşen [SCIM'yi](http://www.simplecloud.info/) protokolü.</span><span class="sxs-lookup"><span data-stu-id="486f3-109">Azure Active Directory integrates with Cerner Central using hello [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-toocerner-central"></a><span data-ttu-id="486f3-110">Kullanıcıların tooCerner Orta atama</span><span class="sxs-lookup"><span data-stu-id="486f3-110">Assigning users tooCerner Central</span></span>

<span data-ttu-id="486f3-111">Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır.</span><span class="sxs-lookup"><span data-stu-id="486f3-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="486f3-112">Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="486f3-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="486f3-113">Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD grupları tooCerner Orta erişmesi hello kullanıcıları temsil karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="486f3-113">Before configuring and enabling hello provisioning service, you should decide what users and/or groups in Azure AD represent hello users who need access tooCerner Central.</span></span> <span data-ttu-id="486f3-114">Karar sonra buraya hello yönergeleri izleyerek bu kullanıcıların tooCerner Orta atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="486f3-114">Once decided, you can assign these users tooCerner Central by following hello instructions here:</span></span>

[<span data-ttu-id="486f3-115">Bir kullanıcı veya grup tooan kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="486f3-115">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toocerner-central"></a><span data-ttu-id="486f3-116">Kullanıcıların tooCerner Orta atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="486f3-116">Important tips for assigning users tooCerner Central</span></span>

*   <span data-ttu-id="486f3-117">Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama tooCerner merkezi tootest hello atanabilir.</span><span class="sxs-lookup"><span data-stu-id="486f3-117">It is recommended that a single Azure AD user be assigned tooCerner Central tootest hello provisioning configuration.</span></span> <span data-ttu-id="486f3-118">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="486f3-118">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="486f3-119">Tek bir kullanıcı için ilk test tamamlandıktan sonra amaçlanan kullanıcılar tooaccess tam listesini hello herhangi Cerner çözüm (yalnızca Cerner Merkezi) sağlanan toobe tooCerner ait kullanıcı ad listesi atama Cerner Orta önerir.</span><span class="sxs-lookup"><span data-stu-id="486f3-119">Once initial testing is complete for a single user, Cerner Central recommends assigning hello entire list of users intended tooaccess any Cerner solution (not just Cerner Central) toobe provisioned tooCerner’s user roster.</span></span>  <span data-ttu-id="486f3-120">Diğer Cerner çözümleri hello kullanıcı ad listesi kullanıcılar bu listesi yararlanın.</span><span class="sxs-lookup"><span data-stu-id="486f3-120">Other Cerner solutions leverage this list of users in hello user roster.</span></span>

*   <span data-ttu-id="486f3-121">Bir kullanıcı tooCerner Orta atarken hello seçmelisiniz **kullanıcı** hello atama iletişim rolü.</span><span class="sxs-lookup"><span data-stu-id="486f3-121">When assigning a user tooCerner Central, you must select hello **User** role in hello assignment dialog.</span></span> <span data-ttu-id="486f3-122">Merhaba "Varsayılan erişim" rolüne sahip kullanıcılar sağlamasından hariç tutulur.</span><span class="sxs-lookup"><span data-stu-id="486f3-122">Users with hello "Default Access" role are excluded from provisioning.</span></span>


## <a name="configuring-user-provisioning-toocerner-central"></a><span data-ttu-id="486f3-123">Kullanıcı tooCerner Orta hazırlama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="486f3-123">Configuring user provisioning tooCerner Central</span></span>

<span data-ttu-id="486f3-124">Bu bölümde, Azure AD tooCerner Orta ait kullanıcı API sağlama Cerner'ın SCIM'yi kullanıcı hesabını kullanarak ad listesi bağlanma yoluyla sırasında size kılavuzluk eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve atanan kullanıcı hesapları Cerner Orta tabanlı devre dışı bırak Azure AD'de kullanıcı ve grup atama üzerinde.</span><span class="sxs-lookup"><span data-stu-id="486f3-124">This section guides you through connecting your Azure AD tooCerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="486f3-125">[Azure Portalı'nda (https://portal.azure.com). sağlanan hello yönergeleri izleyerek Cerner Orta için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="486f3-125">You may also choose tooenabled SAML-based Single Sign-On for Cerner Central, following hello instructions provided in [Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="486f3-126">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="486f3-126">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span> <span data-ttu-id="486f3-127">Daha fazla bilgi için bkz: Merhaba [oturum açma Cerner Orta tek Öğreticisi](active-directory-saas-cernercentral-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="486f3-127">For more information, see hello [Cerner Central single sign-on tutorial](active-directory-saas-cernercentral-tutorial.md).</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-toocerner-central-in-azure-ad"></a><span data-ttu-id="486f3-128">Azure AD'de tooCerner Orta sağlama tooconfigure otomatik olarak bir kullanıcı hesabı:</span><span class="sxs-lookup"><span data-stu-id="486f3-128">tooconfigure automatic user account provisioning tooCerner Central in Azure AD:</span></span>


<span data-ttu-id="486f3-129">Sipariş tooprovision kullanıcı hesapları tooCerner Orta, toorequest Cerner Cerner Orta system hesabından gerekir ve Azure AD'nin tooconnect tooCerner'ın SCIM'yi endpoint kullanabileceği bir OAuth taşıyıcı belirteci oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="486f3-129">In order tooprovision user accounts tooCerner Central, you’ll need toorequest a Cerner Central system account from Cerner, and generate an OAuth bearer token that Azure AD can use tooconnect tooCerner's SCIM endpoint.</span></span> <span data-ttu-id="486f3-130">Merhaba tümleştirme tooproduction dağıtmadan önce bir Cerner sanal ortamda gerçekleştirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="486f3-130">It is also recommended that hello integration be performed in a Cerner sandbox environment before deploying tooproduction.</span></span>

1.  <span data-ttu-id="486f3-131">Merhaba ilk adımı hello Cerner yönetme tooensure hello kişiler ve Azure AD tümleştirme sahip gerekli tooaccess hello belgelerine gerekli toocomplete hello yönergeleri olan CernerCare hesap.</span><span class="sxs-lookup"><span data-stu-id="486f3-131">hello first step is tooensure hello people managing hello Cerner and Azure AD integration have a CernerCare account, which is required tooaccess hello documentation necessary toocomplete hello instructions.</span></span> <span data-ttu-id="486f3-132">Gerekirse, her bir geçerli ortamda hello URL'ler toocreate CernerCare hesapları aşağıda kullanın.</span><span class="sxs-lookup"><span data-stu-id="486f3-132">If necessary, use hello URLs below toocreate CernerCare accounts in each applicable environment.</span></span>

   * <span data-ttu-id="486f3-133">Korumalı alan: https://sandboxcernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="486f3-133">Sandbox:  https://sandboxcernercare.com/accounts/create</span></span>

   * <span data-ttu-id="486f3-134">Üretim: https://cernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="486f3-134">Production:  https://cernercare.com/accounts/create</span></span>  

2.  <span data-ttu-id="486f3-135">Ardından, bir sistem hesabı için Azure AD oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="486f3-135">Next, a system account must be created for Azure AD.</span></span> <span data-ttu-id="486f3-136">Merhaba yönergeleri toorequest bir sistem hesabı altında korumalı alan ve üretim ortamları için kullanın.</span><span class="sxs-lookup"><span data-stu-id="486f3-136">Use hello instructions below toorequest a System Account for your sandbox and production environments.</span></span>

   * <span data-ttu-id="486f3-137">Yönergeler: https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span><span class="sxs-lookup"><span data-stu-id="486f3-137">Instructions:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span></span>

   * <span data-ttu-id="486f3-138">Korumalı alan: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="486f3-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="486f3-139">Üretim: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="486f3-139">Production:  https://cernercentral.com/system-accounts/</span></span>

3.  <span data-ttu-id="486f3-140">Ardından, OAuth taşıyıcı belirteci her sistem hesapları için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="486f3-140">Next, generate an OAuth bearer token for each of your system accounts.</span></span> <span data-ttu-id="486f3-141">toodo Bu, aşağıdaki izleme hello yönergeleri.</span><span class="sxs-lookup"><span data-stu-id="486f3-141">toodo this, follow hello instructions below.</span></span>

   * <span data-ttu-id="486f3-142">Yönergeler: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span><span class="sxs-lookup"><span data-stu-id="486f3-142">Instructions:  https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span></span>

   * <span data-ttu-id="486f3-143">Korumalı alan: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="486f3-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="486f3-144">Üretim: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="486f3-144">Production:  https://cernercentral.com/system-accounts/</span></span>

4. <span data-ttu-id="486f3-145">Son olarak, her iki Cerner toocomplete hello yapılandırmasında hello korumalı alan ve üretim ortamları için tooacquire kullanıcı ad listesi bölge kimlikleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="486f3-145">Finally, you need tooacquire User Roster Realm IDs for both hello sandbox and production environments in Cerner toocomplete hello configuration.</span></span> <span data-ttu-id="486f3-146">Hakkında bilgi için tooacquire buna ek olarak, bkz: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span><span class="sxs-lookup"><span data-stu-id="486f3-146">For information on how tooacquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span></span> 

5. <span data-ttu-id="486f3-147">Artık Azure AD tooprovision kullanıcı hesapları tooCerner yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="486f3-147">Now you can configure Azure AD tooprovision user accounts tooCerner.</span></span> <span data-ttu-id="486f3-148">İçinde toohello oturum [Azure portal](https://portal.azure.com)ve toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölüm.</span><span class="sxs-lookup"><span data-stu-id="486f3-148">Sign in toohello [Azure portal](https://portal.azure.com), and browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

6. <span data-ttu-id="486f3-149">Çoklu oturum açma için zaten Cerner Orta yapılandırdıysanız, Cerner hello arama alanı kullanarak orta Örneğiniz için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="486f3-149">If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using hello search field.</span></span> <span data-ttu-id="486f3-150">Aksi takdirde seçin **Ekle** arayın ve **Cerner orta** hello uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="486f3-150">Otherwise, select **Add** and search for **Cerner Central** in hello application gallery.</span></span> <span data-ttu-id="486f3-151">Merhaba Arama sonuçlarından Cerner Orta seçin ve uygulamaların tooyour listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="486f3-151">Select Cerner Central from hello search results, and add it tooyour list of applications.</span></span>

7.  <span data-ttu-id="486f3-152">Cerner Orta örneğiniz seçin ve ardından hello **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="486f3-152">Select your instance of Cerner Central, then select hello **Provisioning** tab.</span></span>

8.  <span data-ttu-id="486f3-153">Set hello **sağlama modu** çok**otomatik**.</span><span class="sxs-lookup"><span data-stu-id="486f3-153">Set hello **Provisioning Mode** too**Automatic**.</span></span>

   ![Cerner sağlama Orta](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  <span data-ttu-id="486f3-155">Alanlar'ın altında aşağıdaki hello doldurun **yönetici kimlik bilgileri**:</span><span class="sxs-lookup"><span data-stu-id="486f3-155">Fill in hello following fields under **Admin Credentials**:</span></span>

   * <span data-ttu-id="486f3-156">Merhaba, **Kiracı URL** alan, "Kullanıcı-ad listesi-bölge-ID" Merhaba bölge kimliği #4. adımda aldığınız değiştirerek bir URL aşağıda hello biçiminde girin.</span><span class="sxs-lookup"><span data-stu-id="486f3-156">In hello **Tenant URL** field, enter a URL in hello format below, replacing "User-Roster-Realm-ID" with hello realm ID you acquired in step #4.</span></span>

> <span data-ttu-id="486f3-157">Korumalı alan: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="486f3-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

> <span data-ttu-id="486f3-158">Üretim: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="486f3-158">Production: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

   * <span data-ttu-id="486f3-159">Merhaba, **gizli belirteci** alanına #3. adımda oluşturulan hello OAuth taşıyıcı belirteci girin ve tıklatın **Bağlantıyı Sına**.</span><span class="sxs-lookup"><span data-stu-id="486f3-159">In hello **Secret Token** field, enter hello OAuth bearer token you generated in step #3 and click **Test Connection**.</span></span>

   * <span data-ttu-id="486f3-160">Merhaba upperright tarafında portalınızı başarı bildirim görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="486f3-160">You should see a success notification on hello upper­right side of your portal.</span></span>

10. <span data-ttu-id="486f3-161">Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve aşağıdaki hello onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="486f3-161">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

11. <span data-ttu-id="486f3-162">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="486f3-162">Click **Save**.</span></span> 

12. <span data-ttu-id="486f3-163">Merhaba, **öznitelik eşlemelerini** bölümünde, hello kullanıcı ve grup öznitelikleri toobe eşitlenmiş Azure AD tooCerner Orta gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="486f3-163">In hello **Attribute Mappings** section, review hello user and group attributes toobe synchronized from Azure AD tooCerner Central.</span></span> <span data-ttu-id="486f3-164">Merhaba olarak seçilen öznitelikler **eşleşen** kullanılan toomatch hello kullanıcı hesapları ve grupları Cerner Orta güncelleştirme işlemleri için özellikleridir.</span><span class="sxs-lookup"><span data-stu-id="486f3-164">hello attributes selected as **Matching** properties are used toomatch hello user accounts and groups in Cerner Central for update operations.</span></span> <span data-ttu-id="486f3-165">Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.</span><span class="sxs-lookup"><span data-stu-id="486f3-165">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="486f3-166">tooenable hello Cerner Orta, değişiklik hello için Azure AD sağlama hizmeti **sağlama durumu** çok**üzerinde** hello içinde **ayarları** bölümü</span><span class="sxs-lookup"><span data-stu-id="486f3-166">tooenable hello Azure AD provisioning service for Cerner Central, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

14. <span data-ttu-id="486f3-167">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="486f3-167">Click **Save**.</span></span> 

<span data-ttu-id="486f3-168">Bu, tüm kullanıcıların hello ilk eşitleme başlatır ve/veya gruplarının tooCerner Orta hello kullanıcılar ve Gruplar bölümünde atanmış.</span><span class="sxs-lookup"><span data-stu-id="486f3-168">This starts hello initial synchronization of any users and/or groups assigned tooCerner Central in hello Users and Groups section.</span></span> <span data-ttu-id="486f3-169">Merhaba ilk eşitleme yaklaşık 20 dakikada hello Azure AD sağlama hizmeti çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır.</span><span class="sxs-lookup"><span data-stu-id="486f3-169">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello Azure AD provisioning service is running.</span></span> <span data-ttu-id="486f3-170">Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve Cerner Orta uygulama hizmeti sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.</span><span class="sxs-lookup"><span data-stu-id="486f3-170">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Cerner Central app.</span></span>

<span data-ttu-id="486f3-171">Hello Azure AD tooread sağlama nasıl oturum ile ilgili daha fazla bilgi için bkz: [otomatik olarak bir kullanıcı hesabı sağlama raporlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="486f3-171">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="486f3-172">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="486f3-172">Additional resources</span></span>

* [<span data-ttu-id="486f3-173">Cerner Orta: Azure AD kullanarak kimlik verilerini yayımlama</span><span class="sxs-lookup"><span data-stu-id="486f3-173">Cerner Central: Publishing identity data using Azure AD</span></span>](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [<span data-ttu-id="486f3-174">Öğretici: Azure Active Directory ile çoklu oturum açma Cerner Orta yapılandırma</span><span class="sxs-lookup"><span data-stu-id="486f3-174">Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory</span></span>](active-directory-saas-cernercentral-tutorial.md)
* [<span data-ttu-id="486f3-175">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="486f3-175">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="486f3-176">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="486f3-176">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="486f3-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="486f3-177">Next steps</span></span>
* <span data-ttu-id="486f3-178">[Tooreview nasıl günlüğe yazacağını öğrenin ve get raporlar etkinlik sağlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="486f3-178">[Learn how tooreview logs and get reports on provisioning activity](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>
