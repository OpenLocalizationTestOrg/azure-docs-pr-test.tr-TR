---
title: "aaaUsing sistemi etki alanları arası kimlik yönetimi için otomatik olarak sağlamak kullanıcıların ve grupların Azure Active Directory tooapplications | Microsoft Docs"
description: "Azure Active Directory Kullanıcıları ve bir web hizmeti tarafından hello SCIM'yi protokolü belirtimi tanımlanan hello arabirimiyle fronted grupları tooany uygulama ya da kimlik deposunu otomatik olarak sağlayabilirsiniz"
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 4d86f3dc-e2d3-4bde-81a3-4a0e092551c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.custom: aaddev;it-pro;oldportal
ms.openlocfilehash: 43045c97e68d0d22db598dcb5ec23481c4e97718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-system-for-cross-domain-identity-management-tooautomatically-provision-users-and-groups-from-azure-active-directory-tooapplications"></a><span data-ttu-id="d04da-103">Etki alanları arası Kimlik Yönetimi tooautomatically sağlama kullanıcılar ve grupların Azure Active Directory tooapplications için sistem kullanma</span><span class="sxs-lookup"><span data-stu-id="d04da-103">Using System for Cross-Domain Identity Management tooautomatically provision users and groups from Azure Active Directory tooapplications</span></span>

## <a name="overview"></a><span data-ttu-id="d04da-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d04da-104">Overview</span></span>
<span data-ttu-id="d04da-105">Azure Active Directory (Azure AD) kullanıcı ve bir web hizmeti tarafından hello tanımlanan hello arabirimiyle fronted grupları tooany uygulama ya da kimlik deposunu otomatik olarak sağlayabilirler [sistem etki alanları arası Kimlik Yönetimi (SCIM'yi) 2.0 protokol belirtimi](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span><span class="sxs-lookup"><span data-stu-id="d04da-105">Azure Active Directory (Azure AD) can automatically provision users and groups tooany application or identity store that is fronted by a web service with hello interface defined in hello [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span></span> <span data-ttu-id="d04da-106">Azure Active Directory istekleri toocreate göndermek, değiştirmek veya atanan kullanıcılar ve gruplar toohello web hizmetini silin.</span><span class="sxs-lookup"><span data-stu-id="d04da-106">Azure Active Directory can send requests toocreate, modify, or delete assigned users and groups toohello web service.</span></span> <span data-ttu-id="d04da-107">Merhaba web hizmeti işlemlere hello hedef kimlik deposu bu istekleri sonra çevirebilir.</span><span class="sxs-lookup"><span data-stu-id="d04da-107">hello web service can then translate those requests into operations on hello target identity store.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d04da-108">Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="d04da-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 



<span data-ttu-id="d04da-109">![][0]
*Şekil 1: bir web hizmeti aracılığıyla Azure Active Directory tooan kimlik deposu sağlama*</span><span class="sxs-lookup"><span data-stu-id="d04da-109">![][0]
*Figure 1: Provisioning from Azure Active Directory tooan identity store via a web service*</span></span>

<span data-ttu-id="d04da-110">Bu özellik "kendi uygulamanızı getir" Merhaba yeteneğine Azure AD tooenable çoklu oturum açma ve otomatik kullanıcı sağlayan veya SCIM'yi web hizmeti tarafından fronted uygulamalar için hazırlama birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d04da-110">This capability can be used in conjunction with hello “bring your own app” capability in Azure AD tooenable single sign-on and automatic user provisioning for applications that provide or are fronted by a SCIM web service.</span></span>

<span data-ttu-id="d04da-111">Azure Active Directory'de SCIM'yi kullanma iki kullanım örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d04da-111">There are two use cases for using SCIM in Azure Active Directory:</span></span>

* <span data-ttu-id="d04da-112">**SCIM'yi destek kullanıcılar ve gruplar tooapplications sağlama** SCIM'yi 2.0 desteği ve yapılandırma olmadan Azure AD ile kimlik doğrulaması çalışır OAuth taşıyıcı belirteçlerini kullanmak uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="d04da-112">**Provisioning users and groups tooapplications that support SCIM** Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication works with Azure AD without configuration.</span></span>
* <span data-ttu-id="d04da-113">**Diğer API tabanlı sağlama destekleyen uygulamalar için kendi sağlama çözümü derleme** SCIM'yi olmayan uygulamalar için SCIM'yi uç nokta tootranslate hello Azure AD SCIM'yi endpoint herhangi API hello uygulamanızın desteklediği arasındaki oluşturabilirsiniz. Kullanıcı sağlama için.</span><span class="sxs-lookup"><span data-stu-id="d04da-113">**Build your own provisioning solution for applications that support other API-based provisioning** For non-SCIM applications, you can create a SCIM endpoint tootranslate between hello Azure AD SCIM endpoint and any API hello application supports for user provisioning.</span></span> <span data-ttu-id="d04da-114">toohelp SCIM'yi endpoint geliştirme, ortak dil altyapısı (CLI) kitaplıkları ile birlikte nasıl toodo SCIM'yi uç nokta sağlar ve SCIM'yi iletileri Çevir Göster kod örnekleri sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="d04da-114">toohelp you develop a SCIM endpoint, we provide Common Language Infrastructure (CLI) libraries along with code samples that show you how toodo provide a SCIM endpoint and translate SCIM messages.</span></span>  

## <a name="provisioning-users-and-groups-tooapplications-that-support-scim"></a><span data-ttu-id="d04da-115">Kullanıcılar ve SCIM'yi destek grupları tooapplications sağlama</span><span class="sxs-lookup"><span data-stu-id="d04da-115">Provisioning users and groups tooapplications that support SCIM</span></span>
<span data-ttu-id="d04da-116">Azure AD uygulayan yapılandırılmış tooautomatically sağlama atanan kullanıcılar ve gruplar tooapplications olabilir bir [sistemi için etki alanları arası Kimlik Yönetimi 2 (SCIM'yi)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web hizmeti ve kimlik doğrulaması için OAuth taşıyıcı belirteçlerini kabul edin .</span><span class="sxs-lookup"><span data-stu-id="d04da-116">Azure AD can be configured tooautomatically provision assigned users and groups tooapplications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web service and accept OAuth bearer tokens for authentication.</span></span> <span data-ttu-id="d04da-117">Merhaba SCIM'yi 2.0 belirtimi içinde uygulamalar bu gereksinimleri karşılamalıdır:</span><span class="sxs-lookup"><span data-stu-id="d04da-117">Within hello SCIM 2.0 specification, applications must meet these requirements:</span></span>

* <span data-ttu-id="d04da-118">Kullanıcılara ve/veya hello SCIM'yi Protokolü 3.3 bölümünü göredir grupları oluşturmayı destekler.</span><span class="sxs-lookup"><span data-stu-id="d04da-118">Supports creating users and/or groups, as per section 3.3 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="d04da-119">Kullanıcılara ve/veya patch isteklerinde hello SCIM'yi Protokolü 3.5.2'de bölümünü göredir gruplarla değiştirerek destekler.</span><span class="sxs-lookup"><span data-stu-id="d04da-119">Supports modifying users and/or groups with patch requests as per section 3.5.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="d04da-120">Bilinen kaynak hello SCIM'yi Protokolü 3.4.1 bölümünü göredir alma destekler.</span><span class="sxs-lookup"><span data-stu-id="d04da-120">Supports retrieving a known resource as per section 3.4.1 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="d04da-121">Kullanıcılara ve/veya grupları hello SCIM'yi Protokolü 3.4.2 bölümünü göredir sorgulama destekler.</span><span class="sxs-lookup"><span data-stu-id="d04da-121">Supports querying users and/or groups, as per section 3.4.2 of hello SCIM protocol.</span></span>  <span data-ttu-id="d04da-122">Varsayılan olarak, kullanıcılar tarafından externalID seçmeleri istenir ve grupları displayName tarafından sorgulanır.</span><span class="sxs-lookup"><span data-stu-id="d04da-122">By default, users are queried by externalId and groups are queried by displayName.</span></span>  
* <span data-ttu-id="d04da-123">Kullanıcı kimliği ve hello SCIM'yi Protokolü 3.4.2 bölümünü göredir Yöneticisi tarafından sorgulama destekler.</span><span class="sxs-lookup"><span data-stu-id="d04da-123">Supports querying user by ID and by manager as per section 3.4.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="d04da-124">Gruplar ve üye hello SCIM'yi Protokolü 3.4.2 bölümünü göredir kimliği tarafından sorgulama destekler.</span><span class="sxs-lookup"><span data-stu-id="d04da-124">Supports querying groups by ID and by member as per section 3.4.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="d04da-125">Merhaba SCIM'yi Protokolü bölüm 2.1 göredir yetkilendirme için OAuth taşıyıcı belirteçleri kabul eder.</span><span class="sxs-lookup"><span data-stu-id="d04da-125">Accepts OAuth bearer tokens for authorization as per section 2.1 of hello SCIM protocol.</span></span>

<span data-ttu-id="d04da-126">Uygulama sağlayıcınıza veya bu gereksinimleri ile uyumluluk bilgilerinin uygulama sağlayıcınızın belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="d04da-126">Check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span></span>

### <a name="getting-started"></a><span data-ttu-id="d04da-127">Başlarken</span><span class="sxs-lookup"><span data-stu-id="d04da-127">Getting started</span></span>
<span data-ttu-id="d04da-128">Bu makalede açıklanan hello SCIM'yi profili destekleyen uygulamalar bağlı tooAzure Active Directory olabilir hello Azure AD uygulama galerisinde galeri olmayan hello "uygulama" özelliğini kullanma.</span><span class="sxs-lookup"><span data-stu-id="d04da-128">Applications that support hello SCIM profile described in this article can be connected tooAzure Active Directory using hello "non-gallery application" feature in hello Azure AD application gallery.</span></span> <span data-ttu-id="d04da-129">Bağlı, Azure AD çalıştıran sonra eşitleme işlemi burada hello uygulamanın SCIM'yi uç noktası için sorgular 20 dakikada kullanıcılar ve gruplar, atanan ve oluşturur veya bunları toohello atama ayrıntıları göre değiştirir.</span><span class="sxs-lookup"><span data-stu-id="d04da-129">Once connected, Azure AD runs a synchronization process every 20 minutes where it queries hello application's SCIM endpoint for assigned users and groups, and creates or modifies them according toohello assignment details.</span></span>

<span data-ttu-id="d04da-130">**tooconnect SCIM'yi destekleyen bir uygulama:**</span><span class="sxs-lookup"><span data-stu-id="d04da-130">**tooconnect an application that supports SCIM:**</span></span>

1. <span data-ttu-id="d04da-131">Çok oturum[Azure portal hello](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d04da-131">Sign in too[hello Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="d04da-132">Çok Gözat ** Azure Active Directory > Kurumsal uygulamaları ve select **yeni uygulama > tüm > olmayan galeri uygulama**.</span><span class="sxs-lookup"><span data-stu-id="d04da-132">Browse too**Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="d04da-133">Uygulamanız için bir ad girin ve tıklayın **Ekle** simgesi toocreate bir uygulama nesnesi.</span><span class="sxs-lookup"><span data-stu-id="d04da-133">Enter a name for your application, and click **Add** icon toocreate an app object.</span></span>
    
  <span data-ttu-id="d04da-134">![][1]
  *Şekil 2: Azure AD uygulama galerisinde*</span><span class="sxs-lookup"><span data-stu-id="d04da-134">![][1]
*Figure 2: Azure AD application gallery*</span></span>
    
4. <span data-ttu-id="d04da-135">Merhaba Hello elde edilen ekranında şunları seçin **sağlama** hello sol sütunda sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d04da-135">In hello resulting screen, select hello **Provisioning** tab in hello left column.</span></span>
5. <span data-ttu-id="d04da-136">Merhaba, **sağlama modu** menüsünde, select **otomatik**.</span><span class="sxs-lookup"><span data-stu-id="d04da-136">In hello **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="d04da-137">![][2]
  *Şekil 3: hello Azure portal sağlama yapılandırma*</span><span class="sxs-lookup"><span data-stu-id="d04da-137">![][2]
*Figure 3: Configuring provisioning in hello Azure portal*</span></span>
    
6. <span data-ttu-id="d04da-138">Merhaba, **Kiracı URL** alanında, hello hello uygulamanın SCIM'yi uç nokta URL'sini girin.</span><span class="sxs-lookup"><span data-stu-id="d04da-138">In hello **Tenant URL** field, enter hello URL of hello application's SCIM endpoint.</span></span> <span data-ttu-id="d04da-139">Örnek: https://api.contoso.com/scim/v2/</span><span class="sxs-lookup"><span data-stu-id="d04da-139">Example: https://api.contoso.com/scim/v2/</span></span>
7. <span data-ttu-id="d04da-140">Merhaba SCIM'yi uç nokta gerektiriyor Azure AD dışında bir veren bir OAuth taşıyıcı belirtecinden sonra kopyalama hello gerekli OAuth taşıyıcı belirteci hello isteğe bağlı **gizli belirteci** alan.</span><span class="sxs-lookup"><span data-stu-id="d04da-140">If hello SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy hello required OAuth bearer token into hello optional **Secret Token** field.</span></span> <span data-ttu-id="d04da-141">Bu alan boş bırakılırsa, Azure AD her istek ile Azure AD tarafından verilen bir OAuth taşıyıcı belirteci dahil.</span><span class="sxs-lookup"><span data-stu-id="d04da-141">If this field is left blank, then Azure AD included an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="d04da-142">Azure AD kimlik sağlayıcısı bu Azure AD doğrulayabilirsiniz olarak kullanan uygulamaları-belirteç.</span><span class="sxs-lookup"><span data-stu-id="d04da-142">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="d04da-143">Merhaba tıklatın **Bağlantıyı Sına** düğmesi toohave Azure Active Directory girişimi tooconnect toohello SCIM'yi uç noktası.</span><span class="sxs-lookup"><span data-stu-id="d04da-143">Click hello **Test Connection** button toohave Azure Active Directory attempt tooconnect toohello SCIM endpoint.</span></span> <span data-ttu-id="d04da-144">Merhaba deneme başarısız olursa hata bilgileri görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d04da-144">If hello attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="d04da-145">Merhaba denemeleri tooconnect toohello uygulaması başarılı olursa, ardından **kaydetmek** toosave hello yönetici kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="d04da-145">If hello attempts tooconnect toohello application succeed, then click **Save** toosave hello admin credentials.</span></span>
10. <span data-ttu-id="d04da-146">Merhaba, **eşlemeleri** bölümünde, iki seçilebilir öznitelik eşlemelerini kümesi vardır: biri kullanıcı nesneleri ve Grup nesneleri için bir tane.</span><span class="sxs-lookup"><span data-stu-id="d04da-146">In hello **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="d04da-147">Eşitlenen her bir tooreview hello öznitelikleri, Azure Active Directory tooyour uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="d04da-147">Select each one tooreview hello attributes that are synchronized from Azure Active Directory tooyour app.</span></span> <span data-ttu-id="d04da-148">Merhaba olarak seçilen öznitelikler **eşleşen** kullanılan toomatch hello kullanıcılar ve gruplar güncelleştirme işlemleri için uygulamanızda özellikleridir.</span><span class="sxs-lookup"><span data-stu-id="d04da-148">hello attributes selected as **Matching** properties are used toomatch hello users and groups in your app for update operations.</span></span> <span data-ttu-id="d04da-149">Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.</span><span class="sxs-lookup"><span data-stu-id="d04da-149">Select hello Save button toocommit any changes.</span></span>

    >[!NOTE]
    ><span data-ttu-id="d04da-150">İsteğe bağlı olarak, "Merhaba grupları eşleme" devre dışı bırakarak group nesnelerini eşitlemeyi devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="d04da-150">You can optionally disable syncing of group objects by disabling hello "groups" mapping.</span></span> 

11. <span data-ttu-id="d04da-151">Altında **ayarları**, hello **kapsam** alanı tanımlar hangi kullanıcı ve grup veya eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="d04da-151">Under **Settings**, hello **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="d04da-152">"Eşitleme yalnızca kullanıcılar ve gruplar (önerilen) atanan" seçerek yalnızca eşitlendiğini kullanıcılar ve gruplar hello atanan **kullanıcılar ve gruplar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d04da-152">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in hello **Users and groups** tab.</span></span>
12. <span data-ttu-id="d04da-153">Merhaba, yapılandırma tamamlandıktan sonra değiştirmek **sağlama durumu** çok**üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="d04da-153">Once your configuration is complete, change hello **Provisioning Status** too**On**.</span></span>
13. <span data-ttu-id="d04da-154">Tıklatın **kaydetmek** toostart hello Azure AD sağlama hizmeti.</span><span class="sxs-lookup"><span data-stu-id="d04da-154">Click **Save** toostart hello Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="d04da-155">Kullanıcılar ve gruplar (önerilen) yalnızca eşitleniyor atanan emin tooselect hello olması **kullanıcılar ve gruplar** sekmesinde ve hello kullanıcılara ve/veya toosync istediğiniz grupları atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d04da-155">If syncing only assigned users and groups (recommended), be sure tooselect hello **Users and groups** tab and assign hello users and/or groups you wish toosync.</span></span>

<span data-ttu-id="d04da-156">Merhaba ilk eşitleme başladıktan sonra hello kullanabilirsiniz **denetim günlüklerini** sekmesinde uygulamanızdan hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler gösterir toomonitor devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="d04da-156">Once hello initial synchronization has started, you can use hello **Audit logs** tab toomonitor progress, which shows all actions performed by hello provisioning service on your app.</span></span> <span data-ttu-id="d04da-157">Hello Azure AD tooread sağlama nasıl oturum ile ilgili daha fazla bilgi için bkz: [otomatik olarak bir kullanıcı hesabı sağlama raporlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="d04da-157">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

>[!NOTE]
><span data-ttu-id="d04da-158">Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır.</span><span class="sxs-lookup"><span data-stu-id="d04da-158">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> 


## <a name="building-your-own-provisioning-solution-for-any-application"></a><span data-ttu-id="d04da-159">Herhangi bir uygulama için kendi sağlama çözümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="d04da-159">Building your own provisioning solution for any application</span></span>
<span data-ttu-id="d04da-160">Azure Active Directory ile arabirimleri SCIM'yi web hizmeti oluşturarak, bir REST veya SOAP kullanıcı API hazırlama sağlar neredeyse her uygulama için tek oturum açma ve otomatik kullanıcı sağlamayı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d04da-160">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span></span>

<span data-ttu-id="d04da-161">İşte nasıl çalışır:</span><span class="sxs-lookup"><span data-stu-id="d04da-161">Here’s how it works:</span></span>

1. <span data-ttu-id="d04da-162">Azure AD sağlar adlı ortak dil altyapısı kitaplık [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span><span class="sxs-lookup"><span data-stu-id="d04da-162">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span></span> <span data-ttu-id="d04da-163">Sistem tümleştiricileri ve geliştiriciler, bu kitaplık toocreate kullanabilir ve bir SCIM'yi tabanlı web hizmeti uç noktası Azure AD tooany uygulamanın kimlik deposu bağlanıp bağlanamayacağını dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d04da-163">System integrators and developers can use this library toocreate and deploy a SCIM-based web service endpoint capable of connecting Azure AD tooany application’s identity store.</span></span>
2. <span data-ttu-id="d04da-164">Eşlemeleri hello web hizmeti toomap hello standartlaştırılmış kullanıcı şema toohello kullanıcı şeması ve hello uygulama tarafından istenen Protokolü uygulanır.</span><span class="sxs-lookup"><span data-stu-id="d04da-164">Mappings are implemented in hello web service toomap hello standardized user schema toohello user schema and protocol required by hello application.</span></span>
3. <span data-ttu-id="d04da-165">Merhaba uç nokta URL'si hello uygulama galerisinde özel bir uygulama bir parçası olarak Azure AD'de kayıtlı değil.</span><span class="sxs-lookup"><span data-stu-id="d04da-165">hello endpoint URL is registered in Azure AD as part of a custom application in hello application gallery.</span></span>
4. <span data-ttu-id="d04da-166">Kullanıcıların ve grupların Azure AD toothis uygulamada atanır.</span><span class="sxs-lookup"><span data-stu-id="d04da-166">Users and groups are assigned toothis application in Azure AD.</span></span> <span data-ttu-id="d04da-167">Atama oldukları bir sıra eşitlenen toobe toohello hedef uygulamasına yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d04da-167">Upon assignment, they are put into a queue toobe synchronized toohello target application.</span></span> <span data-ttu-id="d04da-168">Hello sıra işleme hello eşitleme işlemi 20 dakikada bir çalışır.</span><span class="sxs-lookup"><span data-stu-id="d04da-168">hello synchronization process handling hello queue runs every 20 minutes.</span></span>

### <a name="code-samples"></a><span data-ttu-id="d04da-169">Kod Örnekleri</span><span class="sxs-lookup"><span data-stu-id="d04da-169">Code Samples</span></span>
<span data-ttu-id="d04da-170">toomake bu işlem daha kolay bir dizi [kod örnekleri](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) SCIM'yi web hizmeti uç noktası oluşturun ve otomatik sağlamayı göstermek sağlanır.</span><span class="sxs-lookup"><span data-stu-id="d04da-170">toomake this process easier, a set of [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span></span> <span data-ttu-id="d04da-171">Kullanıcılar ve gruplar temsil eden virgülle ayrılmış değerler satırlarla bir dosyayı korur bir sağlayıcının bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d04da-171">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span></span>  <span data-ttu-id="d04da-172">Merhaba diğer hello Amazon Web Hizmetleri kimlik ve erişim yönetimi hizmetini çalışır bir sağlayıcı değil.</span><span class="sxs-lookup"><span data-stu-id="d04da-172">hello other is of a provider that operates on hello Amazon Web Services Identity and Access Management service.</span></span>  

<span data-ttu-id="d04da-173">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="d04da-173">**Prerequisites**</span></span>

* <span data-ttu-id="d04da-174">Visual Studio 2013 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="d04da-174">Visual Studio 2013 or later</span></span>
* [<span data-ttu-id="d04da-175">.NET için Azure SDK</span><span class="sxs-lookup"><span data-stu-id="d04da-175">Azure SDK for .NET</span></span>](https://azure.microsoft.com/downloads/)
* <span data-ttu-id="d04da-176">Merhaba ASP.NET framework 4.5 toobe destekleyen Windows makine SCIM'yi endpoint hello kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d04da-176">Windows machine that supports hello ASP.NET framework 4.5 toobe used as hello SCIM endpoint.</span></span> <span data-ttu-id="d04da-177">Bu makinenin hello buluttan erişilebilir olması gerekir</span><span class="sxs-lookup"><span data-stu-id="d04da-177">This machine must be accessible from hello cloud</span></span>
* [<span data-ttu-id="d04da-178">Bir Azure aboneliği ile Azure AD Premium deneme veya lisanslı bir sürümü</span><span class="sxs-lookup"><span data-stu-id="d04da-178">An Azure subscription with a trial or licensed version of Azure AD Premium</span></span>](https://azure.microsoft.com/services/active-directory/)
* <span data-ttu-id="d04da-179">Merhaba Amazon AWS örneği gerektirir hello kitaplıklarından [Visual Studio için AWS Araç Seti](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span><span class="sxs-lookup"><span data-stu-id="d04da-179">hello Amazon AWS sample requires libraries from hello [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span></span> <span data-ttu-id="d04da-180">Daha fazla bilgi için bkz: hello Benioku hello örnekle dahil dosya.</span><span class="sxs-lookup"><span data-stu-id="d04da-180">For more information, see hello README file included with hello sample.</span></span>

### <a name="getting-started"></a><span data-ttu-id="d04da-181">Başlarken</span><span class="sxs-lookup"><span data-stu-id="d04da-181">Getting Started</span></span>
<span data-ttu-id="d04da-182">Azure AD'den sağlama kabul edebileceği bir SCIM'yi uç noktası istekleri hello en kolay yolu tooimplement toobuild olan ve hello sağlanan kullanıcılar tooa virgülle ayrılmış değer (CSV) dosyası çıkarır hello kod örneği dağıtın.</span><span class="sxs-lookup"><span data-stu-id="d04da-182">hello easiest way tooimplement a SCIM endpoint that can accept provisioning requests from Azure AD is toobuild and deploy hello code sample that outputs hello provisioned users tooa comma-separated value (CSV) file.</span></span>

<span data-ttu-id="d04da-183">**toocreate bir örnek SCIM'yi uç noktası:**</span><span class="sxs-lookup"><span data-stu-id="d04da-183">**toocreate a sample SCIM endpoint:**</span></span>

1. <span data-ttu-id="d04da-184">Merhaba kod örnek paketin karşıdan [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span><span class="sxs-lookup"><span data-stu-id="d04da-184">Download hello code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span></span>
2. <span data-ttu-id="d04da-185">Merhaba paketin sıkıştırmasını açın ve Windows makinenizdeki C:\AzureAD-BYOA-Provisioning-Samples\ gibi bir konuma yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="d04da-185">Unzip hello package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span></span>
3. <span data-ttu-id="d04da-186">Bu klasörde, Visual Studio'da hello FileProvisioningAgent çözüm başlatın.</span><span class="sxs-lookup"><span data-stu-id="d04da-186">In this folder, launch hello FileProvisioningAgent solution in Visual Studio.</span></span>
4. <span data-ttu-id="d04da-187">Seçin **Araçlar > Kitaplık Paket Yöneticisi > Paket Yöneticisi Konsolu**ve komutları hello FileProvisioningAgent proje tooresolve hello çözüm başvuruları için aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="d04da-187">Select **Tools > Library Package Manager > Package Manager Console**, and execute hello following commands for hello FileProvisioningAgent project tooresolve hello solution references:</span></span>
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. <span data-ttu-id="d04da-188">Merhaba FileProvisioningAgent projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d04da-188">Build hello FileProvisioningAgent project.</span></span>
6. <span data-ttu-id="d04da-189">(Yönetici) olarak Windows Hello komut istemi uygulamasını başlatma ve hello kullan **cd** komutu toochange hello dizin tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** klasör.</span><span class="sxs-lookup"><span data-stu-id="d04da-189">Launch hello Command Prompt application in Windows (as an Administrator), and use hello **cd** command toochange hello directory tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span></span>
7. <span data-ttu-id="d04da-190">Aşağıdaki komut, < IP adresi > merhaba IP adresine veya etki alanı adıyla hello Windows makinenin değiştirerek hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d04da-190">Run hello following command, replacing <ip-address> with hello IP address or domain name of hello Windows machine:</span></span>
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. <span data-ttu-id="d04da-191">Windows altında **Windows Ayarları > Ağ ve Internet ayarlarını**seçin hello **Windows Güvenlik Duvarı > Gelişmiş ayarları**ve oluşturma bir **gelen kuralı** , gelen erişim tooport 9000 sağlar.</span><span class="sxs-lookup"><span data-stu-id="d04da-191">In Windows under **Windows Settings > Network & Internet Settings**, select hello **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access tooport 9000.</span></span>
9. <span data-ttu-id="d04da-192">Merhaba Windows makine yönlendiricisi arkasında ise, sunulan toohello olan yönlendirici gereksinimlerini yapılandırılmış toobe tooperform ağ erişim çevirisi, bağlantı noktası 9000 arasında hello Internet ve bağlantı noktası 9000 hello Windows makinede.</span><span class="sxs-lookup"><span data-stu-id="d04da-192">If hello Windows machine is behind a router, hello router needs toobe configured tooperform Network Access Translation between its port 9000 that is exposed toohello internet, and port 9000 on hello Windows machine.</span></span> <span data-ttu-id="d04da-193">Bu Azure AD toobe mümkün tooaccess gereklidir hello bulutta Bu uç nokta.</span><span class="sxs-lookup"><span data-stu-id="d04da-193">This is required for Azure AD toobe able tooaccess this endpoint in hello cloud.</span></span>

<span data-ttu-id="d04da-194">**tooregister hello örnek SCIM'yi uç noktası Azure AD'de:**</span><span class="sxs-lookup"><span data-stu-id="d04da-194">**tooregister hello sample SCIM endpoint in Azure AD:**</span></span>

1. <span data-ttu-id="d04da-195">Çok oturum[Azure portal hello](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d04da-195">Sign in too[hello Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="d04da-196">Çok Gözat ** Azure Active Directory > Kurumsal uygulamaları ve select **yeni uygulama > tüm > olmayan galeri uygulama**.</span><span class="sxs-lookup"><span data-stu-id="d04da-196">Browse too**Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="d04da-197">Uygulamanız için bir ad girin ve tıklayın **Ekle** simgesi toocreate bir uygulama nesnesi.</span><span class="sxs-lookup"><span data-stu-id="d04da-197">Enter a name for your application, and click **Add** icon toocreate an app object.</span></span> <span data-ttu-id="d04da-198">oluşturulan hello uygulama hedeflenen toorepresent hello hedef uygulama tek oturum açma için ve yalnızca hello SCIM'yi endpoint uygulama tooand sağlama nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="d04da-198">hello application object created is intended toorepresent hello target app you would be provisioning tooand implementing single sign-on for, and not just hello SCIM endpoint.</span></span>
4. <span data-ttu-id="d04da-199">Merhaba Hello elde edilen ekranında şunları seçin **sağlama** hello sol sütunda sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d04da-199">In hello resulting screen, select hello **Provisioning** tab in hello left column.</span></span>
5. <span data-ttu-id="d04da-200">Merhaba, **sağlama modu** menüsünde, select **otomatik**.</span><span class="sxs-lookup"><span data-stu-id="d04da-200">In hello **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="d04da-201">![][2]
  *Şekil 4: hello Azure portal sağlama yapılandırma*</span><span class="sxs-lookup"><span data-stu-id="d04da-201">![][2]
*Figure 4: Configuring provisioning in hello Azure portal*</span></span>
    
6. <span data-ttu-id="d04da-202">Merhaba, **Kiracı URL** alanında, hello Internet kullanıma sunulan URL ve SCIM'yi bitiş bağlantı noktası girin.</span><span class="sxs-lookup"><span data-stu-id="d04da-202">In hello **Tenant URL** field, enter hello internet-exposed URL and port of your SCIM endpoint.</span></span> <span data-ttu-id="d04da-203">Http://testmachine.contoso.com:9000 veya http://<ip-address>:9000/, burada < IP adresi > olan hello internet IP kullanıma sunulan gibi bu bir şey olacaktır adresi.</span><span class="sxs-lookup"><span data-stu-id="d04da-203">This would be something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is hello internet exposed IP address.</span></span>  
7. <span data-ttu-id="d04da-204">Merhaba SCIM'yi uç nokta gerektiriyor Azure AD dışında bir veren bir OAuth taşıyıcı belirtecinden sonra kopyalama hello gerekli OAuth taşıyıcı belirteci hello isteğe bağlı **gizli belirteci** alan.</span><span class="sxs-lookup"><span data-stu-id="d04da-204">If hello SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy hello required OAuth bearer token into hello optional **Secret Token** field.</span></span> <span data-ttu-id="d04da-205">Bu alan boş bırakılırsa, Azure AD her istek ile Azure AD tarafından verilen bir OAuth taşıyıcı belirteci dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="d04da-205">If this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="d04da-206">Azure AD kimlik sağlayıcısı bu Azure AD doğrulayabilirsiniz olarak kullanan uygulamaları-belirteç.</span><span class="sxs-lookup"><span data-stu-id="d04da-206">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="d04da-207">Merhaba tıklatın **Bağlantıyı Sına** düğmesi toohave Azure Active Directory girişimi tooconnect toohello SCIM'yi uç noktası.</span><span class="sxs-lookup"><span data-stu-id="d04da-207">Click hello **Test Connection** button toohave Azure Active Directory attempt tooconnect toohello SCIM endpoint.</span></span> <span data-ttu-id="d04da-208">Merhaba deneme başarısız olursa hata bilgileri görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d04da-208">If hello attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="d04da-209">Merhaba denemeleri tooconnect toohello uygulaması başarılı olursa, ardından **kaydetmek** toosave hello yönetici kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="d04da-209">If hello attempts tooconnect toohello application succeed, then click **Save** toosave hello admin credentials.</span></span>
10. <span data-ttu-id="d04da-210">Merhaba, **eşlemeleri** bölümünde, iki seçilebilir öznitelik eşlemelerini kümesi vardır: biri kullanıcı nesneleri ve Grup nesneleri için bir tane.</span><span class="sxs-lookup"><span data-stu-id="d04da-210">In hello **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="d04da-211">Eşitlenen her bir tooreview hello öznitelikleri, Azure Active Directory tooyour uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="d04da-211">Select each one tooreview hello attributes that are synchronized from Azure Active Directory tooyour app.</span></span> <span data-ttu-id="d04da-212">Merhaba olarak seçilen öznitelikler **eşleşen** kullanılan toomatch hello kullanıcılar ve gruplar güncelleştirme işlemleri için uygulamanızda özellikleridir.</span><span class="sxs-lookup"><span data-stu-id="d04da-212">hello attributes selected as **Matching** properties are used toomatch hello users and groups in your app for update operations.</span></span> <span data-ttu-id="d04da-213">Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.</span><span class="sxs-lookup"><span data-stu-id="d04da-213">Select hello Save button toocommit any changes.</span></span>
11. <span data-ttu-id="d04da-214">Altında **ayarları**, hello **kapsam** alanı tanımlar hangi kullanıcı ve grup veya eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="d04da-214">Under **Settings**, hello **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="d04da-215">"Eşitleme yalnızca kullanıcılar ve gruplar (önerilen) atanan" seçerek yalnızca eşitlendiğini kullanıcılar ve gruplar hello atanan **kullanıcılar ve gruplar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d04da-215">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in hello **Users and groups** tab.</span></span>
12. <span data-ttu-id="d04da-216">Merhaba, yapılandırma tamamlandıktan sonra değiştirmek **sağlama durumu** çok**üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="d04da-216">Once your configuration is complete, change hello **Provisioning Status** too**On**.</span></span>
13. <span data-ttu-id="d04da-217">Tıklatın **kaydetmek** toostart hello Azure AD sağlama hizmeti.</span><span class="sxs-lookup"><span data-stu-id="d04da-217">Click **Save** toostart hello Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="d04da-218">Kullanıcılar ve gruplar (önerilen) yalnızca eşitleniyor atanan emin tooselect hello olması **kullanıcılar ve gruplar** sekmesinde ve hello kullanıcılara ve/veya toosync istediğiniz grupları atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d04da-218">If syncing only assigned users and groups (recommended), be sure tooselect hello **Users and groups** tab and assign hello users and/or groups you wish toosync.</span></span>

<span data-ttu-id="d04da-219">Merhaba ilk eşitleme başladıktan sonra hello kullanabilirsiniz **denetim günlüklerini** sekmesinde uygulamanızdan hizmet sağlama hello tarafından gerçekleştirilen tüm eylemler gösterir toomonitor devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="d04da-219">Once hello initial synchronization has started, you can use hello **Audit logs** tab toomonitor progress, which shows all actions performed by hello provisioning service on your app.</span></span> <span data-ttu-id="d04da-220">Hello Azure AD tooread sağlama nasıl oturum ile ilgili daha fazla bilgi için bkz: [otomatik olarak bir kullanıcı hesabı sağlama raporlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="d04da-220">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

<span data-ttu-id="d04da-221">Merhaba örnek doğrulama hello son adımı tooopen hello Windows makinenizde hello \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug klasöründeki TargetFile.csv dosyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d04da-221">hello final step in verifying hello sample is tooopen hello TargetFile.csv file in hello \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span></span> <span data-ttu-id="d04da-222">Sağlama işlemi hello çalıştırdıktan sonra bu dosyayı tüm hello ayrıntılarını atanan ve kullanıcılar ve gruplar sağlanan gösterir.</span><span class="sxs-lookup"><span data-stu-id="d04da-222">Once hello provisioning process is run, this file shows hello details of all assigned and provisioned users and groups.</span></span>

### <a name="development-libraries"></a><span data-ttu-id="d04da-223">Geliştirme kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="d04da-223">Development libraries</span></span>
<span data-ttu-id="d04da-224">toodevelop toohello SCIM'yi belirtimine uygun kendi web hizmeti ilk tanıyın kendinizi Microsoft tarafından toohelp hızlandırmak sağlanan hello geliştirme sürecinin kitaplıkları aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="d04da-224">toodevelop your own web service that conforms toohello SCIM specification, first familiarize yourself with hello following libraries provided by Microsoft toohelp accelerate hello development process:</span></span> 

1. <span data-ttu-id="d04da-225">Ortak dil altyapısı (CLI) kitaplıklar gibi C#, altyapı göre dilleri ile kullanıma sunulur.</span><span class="sxs-lookup"><span data-stu-id="d04da-225">Common Language Infrastructure (CLI) libraries are offered for use with languages based on that infrastructure, such as C#.</span></span> <span data-ttu-id="d04da-226">Bu kitaplıklar birini [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), hello aşağıdaki çizimde gösterilen bir arabirim Microsoft.SystemForCrossDomainIdentityManagement.IProvider, bildirir: A Merhaba kitaplıkları kullanarak geliştirici için genel sağlayıcısı olarak adlandırılabilir bir sınıf ile bu arabirimini uygulaması.</span><span class="sxs-lookup"><span data-stu-id="d04da-226">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in hello following illustration:  A developer using hello libraries would implement that interface with a class that may be referred to, generically, as a provider.</span></span> <span data-ttu-id="d04da-227">Merhaba kitaplıkları hello Geliştirici toodeploy toohello SCIM'yi belirtimi uyumlu bir web hizmeti etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d04da-227">hello libraries enable hello developer toodeploy a web service that conforms toohello SCIM specification.</span></span> <span data-ttu-id="d04da-228">Merhaba web hizmeti ya da Internet Information Services veya yürütülebilir bir ortak dil altyapısı derlemesi içinde barındırılabilir.</span><span class="sxs-lookup"><span data-stu-id="d04da-228">hello web service can be either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span></span> <span data-ttu-id="d04da-229">İstek hello Geliştirici toooperate bazı kimlik deposu olarak programlanmış çağrıları toohello sağlayıcının yöntemlerde çevrilir.</span><span class="sxs-lookup"><span data-stu-id="d04da-229">Request is translated into calls toohello provider’s methods, which would be programmed by hello developer toooperate on some identity store.</span></span>
  
  ![][3]
  
2. <span data-ttu-id="d04da-230">[Rota işleyicileri express](http://expressjs.com/guide/routing.html) tooa node.js web hizmetine yapılan çağrılar (tarafından tanımlanan hello SCIM'yi belirtimi), temsil eden bir node.js isteği nesneleri ayrıştırmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d04da-230">[Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by hello SCIM specification), made tooa node.js web service.</span></span>   

### <a name="building-a-custom-scim-endpoint"></a><span data-ttu-id="d04da-231">Bir özel SCIM'yi uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="d04da-231">Building a Custom SCIM Endpoint</span></span>
<span data-ttu-id="d04da-232">Merhaba CLI kitaplıkları kullanarak, bu kitaplığı kullanan geliştiriciler kendi Hizmetleri veya Internet Information Services yürütülebilir ortak dil altyapısı derlemeler içinde barındırabilir.</span><span class="sxs-lookup"><span data-stu-id="d04da-232">Using hello CLI libraries, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span></span> <span data-ttu-id="d04da-233">Merhaba adresinde http://localhost:9000 yürütülebilir bütünleştirilmiş kod içinde bir hizmet barındırma için örnek kod aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d04da-233">Here is sample code for hosting a service within an executable assembly, at hello address http://localhost:9000:</span></span> 

    private static void Main(string[] arguments)
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IProvider and 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
      new DevelopersMonitor();
    Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
      new DevelopersProvider(arguments[1]);
    Microsoft.SystemForCrossDomainIdentityManagement.Service webService = null;
    try
    {
        webService = new WebService(monitor, provider);
        webService.Start("http://localhost:9000");

        Console.ReadKey(true);
    }
    finally
    {
        if (webService != null)
        {
            webService.Dispose();
            webService = null;
        }
    }
    }

    public class WebService : Microsoft.SystemForCrossDomainIdentityManagement.Service
    {
    private Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor;
    private Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider;

    public WebService(
      Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitoringBehavior, 
      Microsoft.SystemForCrossDomainIdentityManagement.IProvider providerBehavior)
    {
        this.monitor = monitoringBehavior;
        this.provider = providerBehavior;
    }

    public override IMonitor MonitoringBehavior
    {
        get
        {
            return this.monitor;
        }

        set
        {
            this.monitor = value;
        }
    }

    public override IProvider ProviderBehavior
    {
        get
        {
            return this.provider;
        }

        set
        {
            this.provider = value;
        }
    }
    }

<span data-ttu-id="d04da-234">Bu hizmet hangi hello kök sertifika yetkilisi hello aşağıdakilerden biri olan bir HTTP adresi ve bir sunucu kimlik doğrulama sertifikası olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="d04da-234">This service must have an HTTP address and server authentication certificate of which hello root certification authority is one of hello following:</span></span> 

* <span data-ttu-id="d04da-235">CNNIC</span><span class="sxs-lookup"><span data-stu-id="d04da-235">CNNIC</span></span>
* <span data-ttu-id="d04da-236">Comodo</span><span class="sxs-lookup"><span data-stu-id="d04da-236">Comodo</span></span>
* <span data-ttu-id="d04da-237">CyberTrust</span><span class="sxs-lookup"><span data-stu-id="d04da-237">CyberTrust</span></span>
* <span data-ttu-id="d04da-238">DigiCert</span><span class="sxs-lookup"><span data-stu-id="d04da-238">DigiCert</span></span>
* <span data-ttu-id="d04da-239">GeoTrust</span><span class="sxs-lookup"><span data-stu-id="d04da-239">GeoTrust</span></span>
* <span data-ttu-id="d04da-240">GlobalSign</span><span class="sxs-lookup"><span data-stu-id="d04da-240">GlobalSign</span></span>
* <span data-ttu-id="d04da-241">Daddy gidin</span><span class="sxs-lookup"><span data-stu-id="d04da-241">Go Daddy</span></span>
* <span data-ttu-id="d04da-242">VeriSign</span><span class="sxs-lookup"><span data-stu-id="d04da-242">Verisign</span></span>
* <span data-ttu-id="d04da-243">WoSign</span><span class="sxs-lookup"><span data-stu-id="d04da-243">WoSign</span></span>

<span data-ttu-id="d04da-244">Bir sunucu kimlik doğrulama sertifikası hello ağ Kabuğu yardımcı programını kullanarak bir Windows ana bilgisayardaki ilişkili tooa bağlantı noktası olabilir:</span><span class="sxs-lookup"><span data-stu-id="d04da-244">A server authentication certificate can be bound tooa port on a Windows host using hello network shell utility:</span></span> 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

<span data-ttu-id="d04da-245">Merhaba AppID bağımsız değişkeni için sağlanan hello değeri rastgele bir genel benzersiz tanımlayıcı olsa da burada hello certhash bağımsız değişkeni için sağlanan hello hello sertifikanın parmak izini Merhaba, değerdir.</span><span class="sxs-lookup"><span data-stu-id="d04da-245">Here, hello value provided for hello certhash argument is hello thumbprint of hello certificate, while hello value provided for hello appid argument is an arbitrary globally unique identifier.</span></span>  

<span data-ttu-id="d04da-246">toohost hello hizmet Internet Information Services içinde bir geliştirici, başlangıç hello derlemenin hello varsayılan ad alanında adlı bir sınıf ile CLA kod kitaplığı derleme oluşturma.</span><span class="sxs-lookup"><span data-stu-id="d04da-246">toohost hello service within Internet Information Services, a developer would build a CLA code library assembly with a class named Startup in hello default namespace of hello assembly.</span></span>  <span data-ttu-id="d04da-247">Böyle bir sınıfın bir örneği aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d04da-247">Here is a sample of such a class:</span></span> 

    public class Startup
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor and  
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter starter;

    public Startup()
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
          new DevelopersMonitor();
        Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
          new DevelopersProvider();
        this.starter = 
          new Microsoft.SystemForCrossDomainIdentityManagement.WebApplicationStarter(
            provider, 
            monitor);
    }

    public void Configuration(
      Owin.IAppBuilder builder) // Defined in in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a><span data-ttu-id="d04da-248">İşleme uç noktası kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d04da-248">Handling endpoint authentication</span></span>
<span data-ttu-id="d04da-249">Azure Active Directory gelen istekleri bir OAuth 2.0 taşıyıcı belirteci içerir.</span><span class="sxs-lookup"><span data-stu-id="d04da-249">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span></span>   <span data-ttu-id="d04da-250">Herhangi bir hizmet alıcı hello isteği hello veren erişim toohello Azure Active Directory Graph web hizmeti için beklenen hello Azure Active Directory Kiracı adına Azure Active Directory olarak kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="d04da-250">Any service receiving hello request should authenticate hello issuer as being Azure Active Directory on behalf of hello expected Azure Active Directory tenant, for access toohello Azure Active Directory Graph web service.</span></span>  <span data-ttu-id="d04da-251">Merhaba belirteçte hello veren "ISS" gibi bir ISS talep tanımlanır: "https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span><span class="sxs-lookup"><span data-stu-id="d04da-251">In hello token, hello issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span></span>  <span data-ttu-id="d04da-252">Bu örnekte, hello talep değeri, taban adresini hello https://sts.windows.net, veren hello gibi Azure Active Directory tanımlar, hello göreli adresi segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, benzersiz tanıtıcısının olsa da Azure Active hello Dizin Kiracı adına hangi hello belirteci verilmiş.</span><span class="sxs-lookup"><span data-stu-id="d04da-252">In this example, hello base address of hello claim value, https://sts.windows.net, identifies Azure Active Directory as hello issuer, while hello relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of hello Azure Active Directory tenant on behalf of which hello token was issued.</span></span>  <span data-ttu-id="d04da-253">Merhaba belirteci hello Azure Active Directory Graph web hizmeti, bu hizmeti sonra hello tanıtıcısı erişmek için verilmişse 00000002-0000-0000-c000-000000000000, olması hello belirtecin aud hello değerinin talep.</span><span class="sxs-lookup"><span data-stu-id="d04da-253">If hello token was issued for accessing hello Azure Active Directory Graph web service, then hello identifier of that service, 00000002-0000-0000-c000-000000000000, should be in hello value of hello token’s aud claim.</span></span>  

<span data-ttu-id="d04da-254">Geliştiriciler SCIM'yi hizmet oluşturmak için Microsoft tarafından sağlanan hello CLA kitaplıkları kullanarak aşağıdaki adımları izleyerek hello Microsoft.Owin.Security.ActiveDirectory paketi kullanılarak Azure Active Directory'ye gelen istekleri doğrulayabilir:</span><span class="sxs-lookup"><span data-stu-id="d04da-254">Developers using hello CLA libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using hello Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span></span> 

1. <span data-ttu-id="d04da-255">Sağlayıcı, bu hello hizmeti başlatıldığında adlı bir yöntem toobe dönüş sağlayarak hello Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior özelliği uygulayın:</span><span class="sxs-lookup"><span data-stu-id="d04da-255">In a provider, implement hello Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method toobe called whenever hello service is started:</span></span> 

  ````
    public override Action\<Owin.IAppBuilder, System.Web.Http.HttpConfiguration.HttpConfiguration\> StartupBehavior
    {
      get
      {
        return this.OnServiceStartup;
      }
    }

    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder,  // Defined in Owin.dll.  
      System.Web.Http.HttpConfiguration configuration)  // Defined in System.Web.Http.dll.  
    {
    }
  ````

2. <span data-ttu-id="d04da-256">Aşağıdaki kod toothat yöntemi toohave hello hello hizmetin uç noktaları erişim toohello Azure AD grafik web hizmeti için belirtilen bir kiracı adına Azure Active Directory tarafından verilmiş bir belirteç pul olarak kimliği doğrulanmış tüm istek tooany ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d04da-256">Add hello following code toothat method toohave any request tooany of hello service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access toohello Azure AD Graph web service:</span></span> 

  ````
    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder IAppBuilder applicationBuilder, 
      System.Web.Http.HttpConfiguration HttpConfiguration configuration)
    {
      // IFilter is defined in System.Web.Http.dll.  
      System.Web.Http.Filters.IFilter authorizationFilter = 
        new System.Web.Http.AuthorizeAttribute(); // Defined in System.Web.Http.dll.configuration.Filters.Add(authorizationFilter);

      // SystemIdentityModel.Tokens.TokenValidationParameters is defined in    
      // System.IdentityModel.Token.Jwt.dll.
      SystemIdentityModel.Tokens.TokenValidationParameters tokenValidationParameters =     
        new TokenValidationParameters()
        {
          ValidAudience = "00000002-0000-0000-c000-000000000000"
        };

      // WindowsAzureActiveDirectoryBearerAuthenticationOptions is defined in 
      // Microsoft.Owin.Security.ActiveDirectory.dll
      Microsoft.Owin.Security.ActiveDirectory.
      WindowsAzureActiveDirectoryBearerAuthenticationOptions authenticationOptions =
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions()    {
        TokenValidationParameters = tokenValidationParameters,
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute hello appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a><span data-ttu-id="d04da-257">Kullanıcı ve Grup şeması</span><span class="sxs-lookup"><span data-stu-id="d04da-257">User and group schema</span></span>
<span data-ttu-id="d04da-258">Azure Active Directory kaynakları tooSCIM web hizmetleri iki tür sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d04da-258">Azure Active Directory can provision two types of resources tooSCIM web services.</span></span>  <span data-ttu-id="d04da-259">Bu kaynakların kullanıcılar ve gruplar türleridir.</span><span class="sxs-lookup"><span data-stu-id="d04da-259">Those types of resources are users and groups.</span></span>  

<span data-ttu-id="d04da-260">Kullanıcı kaynakları hello şema tanımlayıcısı, bu protokolü belirtimi içinde bulunan urn: ietf:params:scim:schemas:extension:enterprise:2.0:User tanımlanır: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span><span class="sxs-lookup"><span data-stu-id="d04da-260">User resources are identified by hello schema identifier, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span></span>  <span data-ttu-id="d04da-261">Kullanıcıların Azure Active Directory toohello özniteliklerinde urn: ietf:params:scim:schemas:extension:enterprise:2.0:User kaynakların hello özniteliklerin Hello Varsayılan eşleme Tablo 1, aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d04da-261">hello default mapping of hello attributes of users in Azure Active Directory toohello attributes of urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resources is provided in table 1, below.</span></span>  

<span data-ttu-id="d04da-262">Grup kaynaklarının hello şema tanımlayıcılarına göre tanımlanır http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="d04da-262">Group resources are identified by hello schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  <span data-ttu-id="d04da-263">Aşağıda, gösterir hello Varsayılan eşleme gruplarının Azure Active Directory toohello öznitelikleri http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group kaynakların hello özniteliklerin Tablo 2.</span><span class="sxs-lookup"><span data-stu-id="d04da-263">Table 2, below, shows hello default mapping of hello attributes of groups in Azure Active Directory toohello attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span></span>  

### <a name="table-1-default-user-attribute-mapping"></a><span data-ttu-id="d04da-264">Tablo 1: Varsayılan kullanıcı özniteliği eşlemesi</span><span class="sxs-lookup"><span data-stu-id="d04da-264">Table 1: Default user attribute mapping</span></span>
| <span data-ttu-id="d04da-265">Azure Active Directory kullanıcısı</span><span class="sxs-lookup"><span data-stu-id="d04da-265">Azure Active Directory user</span></span> | <span data-ttu-id="d04da-266">urn: ietf:params:scim:schemas:extension:enterprise:2.0:User</span><span class="sxs-lookup"><span data-stu-id="d04da-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span></span> |
| --- | --- |
| <span data-ttu-id="d04da-267">IsSoftDeleted</span><span class="sxs-lookup"><span data-stu-id="d04da-267">IsSoftDeleted</span></span> |<span data-ttu-id="d04da-268">Etkin</span><span class="sxs-lookup"><span data-stu-id="d04da-268">active</span></span> |
| <span data-ttu-id="d04da-269">Görünen adı</span><span class="sxs-lookup"><span data-stu-id="d04da-269">displayName</span></span> |<span data-ttu-id="d04da-270">Görünen adı</span><span class="sxs-lookup"><span data-stu-id="d04da-270">displayName</span></span> |
| <span data-ttu-id="d04da-271">Faks TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="d04da-271">Facsimile-TelephoneNumber</span></span> |<span data-ttu-id="d04da-272">PhoneNumber [türü eq "faks"] .value</span><span class="sxs-lookup"><span data-stu-id="d04da-272">phoneNumbers[type eq "fax"].value</span></span> |
| <span data-ttu-id="d04da-273">givenName</span><span class="sxs-lookup"><span data-stu-id="d04da-273">givenName</span></span> |<span data-ttu-id="d04da-274">name.givenName</span><span class="sxs-lookup"><span data-stu-id="d04da-274">name.givenName</span></span> |
| <span data-ttu-id="d04da-275">İş Unvanı</span><span class="sxs-lookup"><span data-stu-id="d04da-275">jobTitle</span></span> |<span data-ttu-id="d04da-276">Başlık</span><span class="sxs-lookup"><span data-stu-id="d04da-276">title</span></span> |
| <span data-ttu-id="d04da-277">Posta</span><span class="sxs-lookup"><span data-stu-id="d04da-277">mail</span></span> |<span data-ttu-id="d04da-278">e-postaları [türü eq "İş"] .value</span><span class="sxs-lookup"><span data-stu-id="d04da-278">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="d04da-279">mailNickname</span><span class="sxs-lookup"><span data-stu-id="d04da-279">mailNickname</span></span> |<span data-ttu-id="d04da-280">externalID</span><span class="sxs-lookup"><span data-stu-id="d04da-280">externalId</span></span> |
| <span data-ttu-id="d04da-281">Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="d04da-281">manager</span></span> |<span data-ttu-id="d04da-282">Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="d04da-282">manager</span></span> |
| <span data-ttu-id="d04da-283">Mobil</span><span class="sxs-lookup"><span data-stu-id="d04da-283">mobile</span></span> |<span data-ttu-id="d04da-284">PhoneNumber [türü eq "mobile"] .value</span><span class="sxs-lookup"><span data-stu-id="d04da-284">phoneNumbers[type eq "mobile"].value</span></span> |
| <span data-ttu-id="d04da-285">objectID</span><span class="sxs-lookup"><span data-stu-id="d04da-285">objectId</span></span> |<span data-ttu-id="d04da-286">id</span><span class="sxs-lookup"><span data-stu-id="d04da-286">id</span></span> |
| <span data-ttu-id="d04da-287">posta kodu</span><span class="sxs-lookup"><span data-stu-id="d04da-287">postalCode</span></span> |<span data-ttu-id="d04da-288">adresler [türü eq "İş"] .postalCode</span><span class="sxs-lookup"><span data-stu-id="d04da-288">addresses[type eq "work"].postalCode</span></span> |
| <span data-ttu-id="d04da-289">Proxy adresleri</span><span class="sxs-lookup"><span data-stu-id="d04da-289">proxy-Addresses</span></span> |<span data-ttu-id="d04da-290">e-postaları [eq "diğer" yazın]. Değer</span><span class="sxs-lookup"><span data-stu-id="d04da-290">emails[type eq "other"].Value</span></span> |
| <span data-ttu-id="d04da-291">fiziksel teslim OfficeName</span><span class="sxs-lookup"><span data-stu-id="d04da-291">physical-Delivery-OfficeName</span></span> |<span data-ttu-id="d04da-292">adresler [eq "diğer" yazın]. Biçimlendirilmiş</span><span class="sxs-lookup"><span data-stu-id="d04da-292">addresses[type eq "other"].Formatted</span></span> |
| <span data-ttu-id="d04da-293">StreetAddress</span><span class="sxs-lookup"><span data-stu-id="d04da-293">streetAddress</span></span> |<span data-ttu-id="d04da-294">adresler [türü eq "İş"] .streetAddress</span><span class="sxs-lookup"><span data-stu-id="d04da-294">addresses[type eq "work"].streetAddress</span></span> |
| <span data-ttu-id="d04da-295">Soyadı</span><span class="sxs-lookup"><span data-stu-id="d04da-295">surname</span></span> |<span data-ttu-id="d04da-296">name.familyName</span><span class="sxs-lookup"><span data-stu-id="d04da-296">name.familyName</span></span> |
| <span data-ttu-id="d04da-297">telefon numarası</span><span class="sxs-lookup"><span data-stu-id="d04da-297">telephone-Number</span></span> |<span data-ttu-id="d04da-298">PhoneNumber [türü eq "İş"] .value</span><span class="sxs-lookup"><span data-stu-id="d04da-298">phoneNumbers[type eq "work"].value</span></span> |
| <span data-ttu-id="d04da-299">Kullanıcı PrincipalName</span><span class="sxs-lookup"><span data-stu-id="d04da-299">user-PrincipalName</span></span> |<span data-ttu-id="d04da-300">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="d04da-300">userName</span></span> |

### <a name="table-2-default-group-attribute-mapping"></a><span data-ttu-id="d04da-301">Tablo 2: Varsayılan grup özellik eşlemesi</span><span class="sxs-lookup"><span data-stu-id="d04da-301">Table 2: Default group attribute mapping</span></span>
| <span data-ttu-id="d04da-302">Azure Active Directory grubu</span><span class="sxs-lookup"><span data-stu-id="d04da-302">Azure Active Directory group</span></span> | <span data-ttu-id="d04da-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span><span class="sxs-lookup"><span data-stu-id="d04da-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span></span> |
| --- | --- |
| <span data-ttu-id="d04da-304">Görünen adı</span><span class="sxs-lookup"><span data-stu-id="d04da-304">displayName</span></span> |<span data-ttu-id="d04da-305">externalID</span><span class="sxs-lookup"><span data-stu-id="d04da-305">externalId</span></span> |
| <span data-ttu-id="d04da-306">Posta</span><span class="sxs-lookup"><span data-stu-id="d04da-306">mail</span></span> |<span data-ttu-id="d04da-307">e-postaları [türü eq "İş"] .value</span><span class="sxs-lookup"><span data-stu-id="d04da-307">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="d04da-308">mailNickname</span><span class="sxs-lookup"><span data-stu-id="d04da-308">mailNickname</span></span> |<span data-ttu-id="d04da-309">Görünen adı</span><span class="sxs-lookup"><span data-stu-id="d04da-309">displayName</span></span> |
| <span data-ttu-id="d04da-310">Üyeleri</span><span class="sxs-lookup"><span data-stu-id="d04da-310">members</span></span> |<span data-ttu-id="d04da-311">Üyeleri</span><span class="sxs-lookup"><span data-stu-id="d04da-311">members</span></span> |
| <span data-ttu-id="d04da-312">objectID</span><span class="sxs-lookup"><span data-stu-id="d04da-312">objectId</span></span> |<span data-ttu-id="d04da-313">id</span><span class="sxs-lookup"><span data-stu-id="d04da-313">id</span></span> |
| <span data-ttu-id="d04da-314">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="d04da-314">proxyAddresses</span></span> |<span data-ttu-id="d04da-315">e-postaları [eq "diğer" yazın]. Değer</span><span class="sxs-lookup"><span data-stu-id="d04da-315">emails[type eq "other"].Value</span></span> |

## <a name="user-provisioning-and-de-provisioning"></a><span data-ttu-id="d04da-316">Kullanıcı hazırlama ve sağlamayı kaldırma özelliklerini</span><span class="sxs-lookup"><span data-stu-id="d04da-316">User provisioning and de-provisioning</span></span>
<span data-ttu-id="d04da-317">Merhaba, aşağıdaki çizimde gösterilmektedir Merhaba iletileri Azure Active Directory tooa SCIM'yi hizmet toomanage hello kullanım ömrü boyunca bir kullanıcı başka bir kimlik deposu gönderir.</span><span class="sxs-lookup"><span data-stu-id="d04da-317">hello following illustration shows hello messages that Azure Active Directory sends tooa SCIM service toomanage hello lifecycle of a user in another identity store.</span></span> <span data-ttu-id="d04da-318">Merhaba diyagramı de nasıl hello CLI kitaplıkları kullanılarak uygulanan SCIM'yi sağlanan bir hizmeti Microsoft tarafından yapı için bu tür hizmetlerin bu istekleri bir sağlayıcısının çağrıları toohello yöntemlerin içine Çevir gösterir.</span><span class="sxs-lookup"><span data-stu-id="d04da-318">hello diagram also shows how a SCIM service implemented using hello CLI libraries provided by Microsoft for building such services translate those requests into calls toohello methods of a provider.</span></span>  

<span data-ttu-id="d04da-319">![][4]
*Şekil 5: Kullanıcı sağlama ve sağlamayı kaldırma özelliklerini sırası*</span><span class="sxs-lookup"><span data-stu-id="d04da-319">![][4]
*Figure 5: User provisioning and de-provisioning sequence*</span></span>

1. <span data-ttu-id="d04da-320">Azure Active Directory sorgularını hello mailNickname öznitelik değeri, bir kullanıcının Azure AD içinde eşleşen bir externalID öznitelik değeri olan bir kullanıcı için hizmet hello.</span><span class="sxs-lookup"><span data-stu-id="d04da-320">Azure Active Directory queries hello service for a user with an externalId attribute value matching hello mailNickname attribute value of a user in Azure AD.</span></span> <span data-ttu-id="d04da-321">Merhaba sorgu; burada görüntülerle jyoung mailNickname bir kullanıcının Azure Active Directory'de örneğidir Bu örnekte gibi bir Köprü Metni Aktarım Protokolü (HTTP) istek olarak ifade edilir:</span><span class="sxs-lookup"><span data-stu-id="d04da-321">hello query is expressed as a Hypertext Transfer Protocol (HTTP) request such as this example, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span></span> 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="d04da-322">Merhaba hizmet SCIM'yi Hizmetleri uygulamak için Microsoft tarafından sağlanan Merhaba ortak dil altyapısı kitaplıkları kullanılarak oluşturuldu, hello isteği çağrısı toohello hello hizmetin sağlayıcısının sorgu yöntemini çevrilir.</span><span class="sxs-lookup"><span data-stu-id="d04da-322">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Query method of hello service’s provider.</span></span>  <span data-ttu-id="d04da-323">Bu yöntem hello imzası şöyledir:</span><span class="sxs-lookup"><span data-stu-id="d04da-323">Here is hello signature of that method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="d04da-324">Merhaba Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters arabirimi hello tanımı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d04da-324">Here is hello definition of hello Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span></span> 
  ````
    public interface IQueryParameters: 
      Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
        System.Collections.Generic.IReadOnlyCollection <Microsoft.SystemForCrossDomainIdentityManagement.IFilter> AlternateFilters 
        { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
      system.Collections.Generic.IReadOnlyCollection<string> ExcludedAttributePaths 
      { get; }
      System.Collections.Generic.IReadOnlyCollection<string> RequestedAttributePaths 
      { get; }
      string SchemaIdentifier 
      { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IFilter
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IFilter AdditionalFilter 
          { get; set; }
        string AttributePath 
          { get; } 
        Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator FilterOperator 
          { get; }
        string ComparisonValue 
          { get; }
    }

    public enum Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator
    {
        Equals
    }
  ````
  <span data-ttu-id="d04da-325">Bir kullanıcı için bir sorgu hello externalID özniteliği için belirtilen bir değerle örneği aşağıdaki hello toohello sorgu yöntemi hello değişkenlerin değerleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d04da-325">In hello following sample of a query for a user with a given value for hello externalId attribute, values of hello arguments passed toohello Query method are:</span></span> 
  * <span data-ttu-id="d04da-326">parametreleri. AlternateFilters.Count: 1</span><span class="sxs-lookup"><span data-stu-id="d04da-326">parameters.AlternateFilters.Count: 1</span></span>
  * <span data-ttu-id="d04da-327">parametreleri. AlternateFilters.ElementAt(0). AttributePath: "externalID"</span><span class="sxs-lookup"><span data-stu-id="d04da-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span></span>
  * <span data-ttu-id="d04da-328">parametreleri. AlternateFilters.ElementAt(0). Karşılaştırmaİşleci: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="d04da-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="d04da-329">parametreleri. AlternateFilter.ElementAt(0). ComparisonValue: "jyoung"</span><span class="sxs-lookup"><span data-stu-id="d04da-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span></span>
  * <span data-ttu-id="d04da-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin. RequestId"]</span><span class="sxs-lookup"><span data-stu-id="d04da-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span></span> 

2. <span data-ttu-id="d04da-331">Merhaba yanıt tooa sorgu toohello web hizmeti, bir kullanıcının hello mailNickname öznitelik değeri ile eşleşen bir externalID öznitelik değeri olan bir kullanıcı için tüm kullanıcıların döndürmezse, Azure Active Directory bu hello hizmet sağlama kullanıcı istekleri karşılık gelen toohello bir Azure Active Directory'de.</span><span class="sxs-lookup"><span data-stu-id="d04da-331">If hello response tooa query toohello web service for a user with an externalId attribute value that matches hello mailNickname attribute value of a user does not return any users, then Azure Active Directory requests that hello service provision a user corresponding toohello one in Azure Active Directory.</span></span>  <span data-ttu-id="d04da-332">Böyle bir istek bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d04da-332">Here is an example of such a request:</span></span> 
  ````
    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas":
      [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0User"],
      "externalId":"jyoung",
      "userName":"jyoung",
      "active":true,
      "addresses":null,
      "displayName":"Joy Young",
      "emails": [
        {
          "type":"work",
          "value":"jyoung@Contoso.com",
          "primary":true}],
      "meta": {
        "resourceType":"User"},
       "name":{
        "familyName":"Young",
        "givenName":"Joy"},
      "phoneNumbers":null,
      "preferredLanguage":null,
      "title":null,
      "department":null,
      "manager":null}
  ````
  <span data-ttu-id="d04da-333">Merhaba ortak dil altyapısı kitaplıkları SCIM'yi Hizmetleri uygulamak için Microsoft tarafından sağlanan bu isteği bir çağrı toohello hello hizmetin sağlayıcısının oluşturma yöntemini çevirir.</span><span class="sxs-lookup"><span data-stu-id="d04da-333">hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call toohello Create method of hello service’s provider.</span></span>  <span data-ttu-id="d04da-334">Merhaba Create yönteminin bu imzaya sahip:</span><span class="sxs-lookup"><span data-stu-id="d04da-334">hello Create method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="d04da-335">Bir istek tooprovision bir kullanıcı hello hello kaynak bağımsız değişkeni hello Microsoft.SystemForCrossDomainIdentityManagement örneği değeridir.</span><span class="sxs-lookup"><span data-stu-id="d04da-335">In a request tooprovision a user, hello value of hello resource argument is an instance of hello Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="d04da-336">Merhaba Microsoft.SystemForCrossDomainIdentityManagement.Schemas Kitaplığı'nda tanımlanan Core2EnterpriseUser sınıfı.</span><span class="sxs-lookup"><span data-stu-id="d04da-336">Core2EnterpriseUser class, defined in hello Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span></span>  <span data-ttu-id="d04da-337">Merhaba isteği tooprovision hello kullanıcı başarılı olursa, ardından hello hello yöntemi beklenen tooreturn hello Microsoft.SystemForCrossDomainIdentityManagement örneği uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="d04da-337">If hello request tooprovision hello user succeeds, then hello implementation of hello method is expected tooreturn an instance of hello Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="d04da-338">Merhaba tanımlayıcısı özelliği hello değeriyle Core2EnterpriseUser sınıfı hello yeni sağlanan kullanıcının benzersiz tanıtıcısı toohello ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d04da-338">Core2EnterpriseUser class, with hello value of hello Identifier property set toohello unique identifier of hello newly provisioned user.</span></span>  

3. <span data-ttu-id="d04da-339">tooupdate tooexist bir kimlik deposu olarak bilinen bir kullanıcı tarafından bir SCIM'yi, kullanıcının geçerli durumunu hello gibi bir istekle hello Hizmeti'nden istiyor tarafından Azure Active Directory kazançlar fronted:</span><span class="sxs-lookup"><span data-stu-id="d04da-339">tooupdate a user known tooexist in an identity store fronted by an SCIM, Azure Active Directory proceeds by requesting hello current state of that user from hello service with a request such as:</span></span> 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="d04da-340">Merhaba ortak dil altyapısı kitaplıkları SCIM'yi Hizmetleri uygulamak için Microsoft tarafından sağlanan kullanılarak oluşturulmuş bir hizmetinde hello isteği çağrısı toohello hello hizmetin sağlayıcısının alma yöntemini çevrilir.</span><span class="sxs-lookup"><span data-stu-id="d04da-340">In a service built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, hello request is translated into a call toohello Retrieve method of hello service’s provider.</span></span>  <span data-ttu-id="d04da-341">Merhaba alma yöntemini hello imzası şöyledir:</span><span class="sxs-lookup"><span data-stu-id="d04da-341">Here is hello signature of hello Retrieve method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource and 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
    // are defined in Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> 
       Retrieve(
         Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
           parameters, 
           string correlationIdentifier);

    public interface 
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters:   
        IRetrievalParameters
        {
          Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
            ResourceIdentifier 
              { get; }
    }
    public interface Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier
    {
        string Identifier 
          { get; set; }
        string Microsoft.SystemForCrossDomainIdentityManagement.SchemaIdentifier 
          { get; set; }
    }
  ````
  <span data-ttu-id="d04da-342">Bir kullanıcı bir istek tooretrieve hello geçerli durumu Hello örnekte hello'hello parametreleri bağımsız değişkenin değeri sağlanan hello nesne hello özelliklerinin hello değerleri aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="d04da-342">In hello example of a request tooretrieve hello current state of a user, hello values of hello properties of hello object provided as hello value of hello parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="d04da-343">Tanımlayıcı: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="d04da-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="d04da-344">SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="d04da-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

4. <span data-ttu-id="d04da-345">Hello hello başvuru özniteliği hello kimlik deposundaki geçerli değeri tarafından fronted olup olmadığına bakılmaksızın bir başvuru özniteliği güncelleştirilmiş, toobe sonra Azure Active Directory sorgularını hello hizmet toodetermine ise hello hizmeti zaten bu özniteliğin değerini hello eşleşir Azure Active Directory'de.</span><span class="sxs-lookup"><span data-stu-id="d04da-345">If a reference attribute is toobe updated, then Azure Active Directory queries hello service toodetermine whether or not hello current value of hello reference attribute in hello identity store fronted by hello service already matches hello value of that attribute in Azure Active Directory.</span></span> <span data-ttu-id="d04da-346">Kullanıcılar için hangi hello geçerli değeri bu şekilde sorgulanır hello yalnızca öznitelik hello Yöneticisi özniteliğidir.</span><span class="sxs-lookup"><span data-stu-id="d04da-346">For users, hello only attribute of which hello current value is queried in this way is hello manager attribute.</span></span> <span data-ttu-id="d04da-347">Burada, belirli bir kullanıcı nesnesinin hello Yöneticisi özniteliği şu anda belirli bir değere sahip olup olmadığını isteği toodetermine örneği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d04da-347">Here is an example of a request toodetermine whether hello manager attribute of a particular user object currently has a certain value:</span></span> 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="d04da-348">Merhaba değeri hello öznitelikleri sorgu parametresinin kimliği güveninin bir kullanıcı nesnesi varsa hello hello filtre sorgu parametresi değeri olarak sağlanan hello ifadeyi karşılayan sonra hello hizmetidir beklenen toorespond urn: ietf:params:scim:schemas ile: yalnızca bu kaynağın ID özniteliği hello değeri de dahil olmak üzere çekirdek: 2.0:User veya urn: ietf:params:scim:schemas:extension:enterprise:2.0:User kaynak.</span><span class="sxs-lookup"><span data-stu-id="d04da-348">hello value of hello attributes query parameter, id, signifies that if a user object exists that satisfies hello expression provided as hello value of hello filter query parameter, then hello service is expected toorespond with a urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, including only hello value of that resource’s id attribute.</span></span>  <span data-ttu-id="d04da-349">Merhaba hello değerini **kimliği** toohello istek sahibi bilinen öznitelik.</span><span class="sxs-lookup"><span data-stu-id="d04da-349">hello value of hello **id** attribute is known toohello requestor.</span></span> <span data-ttu-id="d04da-350">Merhaba filtre sorgu parametresi hello değerinde bulunur; Merhaba amacı söylemelisiniz gerçekten toorequest hello filtre ifadesinin olup olmadığına böyle nesne bir gösterge olarak çağıran mevcut bir kaynak en az bir gösterimi ' dir.</span><span class="sxs-lookup"><span data-stu-id="d04da-350">It is included in hello value of hello filter query parameter; hello purpose of asking for it is actually toorequest a minimal representation of a resource that satisfying hello filter expression as an indication of whether or not any such object exists.</span></span>   

  <span data-ttu-id="d04da-351">Merhaba hizmet SCIM'yi Hizmetleri uygulamak için Microsoft tarafından sağlanan Merhaba ortak dil altyapısı kitaplıkları kullanılarak oluşturuldu, hello isteği çağrısı toohello hello hizmetin sağlayıcısının sorgu yöntemini çevrilir.</span><span class="sxs-lookup"><span data-stu-id="d04da-351">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Query method of hello service’s provider.</span></span> <span data-ttu-id="d04da-352">hello'hello parametreleri bağımsız değişkenin değeri sağlanan hello nesnesinin hello özelliklerini Hello değeri aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="d04da-352">hello value of hello properties of hello object provided as hello value of hello parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="d04da-353">parametreleri. AlternateFilters.Count: 2</span><span class="sxs-lookup"><span data-stu-id="d04da-353">parameters.AlternateFilters.Count: 2</span></span>
  * <span data-ttu-id="d04da-354">parametreleri. AlternateFilters.ElementAt(x). AttributePath: "id"</span><span class="sxs-lookup"><span data-stu-id="d04da-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span></span>
  * <span data-ttu-id="d04da-355">parametreleri. AlternateFilters.ElementAt(x). Karşılaştırmaİşleci: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="d04da-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="d04da-356">parametreleri. AlternateFilter.ElementAt(x). ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="d04da-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="d04da-357">parametreleri. AlternateFilters.ElementAt(y). AttributePath: "Yönetici"</span><span class="sxs-lookup"><span data-stu-id="d04da-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span></span>
  * <span data-ttu-id="d04da-358">parametreleri. AlternateFilters.ElementAt(y). Karşılaştırmaİşleci: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="d04da-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="d04da-359">parametreleri. AlternateFilter.ElementAt(y). ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span><span class="sxs-lookup"><span data-stu-id="d04da-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span></span>
  * <span data-ttu-id="d04da-360">parametreleri. RequestedAttributePaths.ElementAt(0): "id"</span><span class="sxs-lookup"><span data-stu-id="d04da-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span></span>
  * <span data-ttu-id="d04da-361">parametreleri. SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="d04da-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

  <span data-ttu-id="d04da-362">Burada, hello dizinin x hello değeri 0 olabilir ve hello hello dizin y değerini 1, olabilir ya da x hello değeri 1 olabilir ve hello y değerini hello filtre sorgu parametresi hello ifadelerin hello sırasını bağlı olarak 0 olabilir.</span><span class="sxs-lookup"><span data-stu-id="d04da-362">Here, hello value of hello index x may be 0 and hello value of hello index y may be 1, or hello value of x may be 1 and hello value of y may be 0, depending on hello order of hello expressions of hello filter query parameter.</span></span>   

5. <span data-ttu-id="d04da-363">Azure Active Directory tooan SCIM'yi hizmet tooupdate bir kullanıcı bir isteğin bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d04da-363">Here is an example of a request from Azure Active Directory tooan SCIM service tooupdate a user:</span></span> 
  ````
    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas": 
      [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"],
      "Operations":
      [
        {
          "op":"Add",
          "path":"manager",
          "value":
            [
              {
                "$ref":"http://.../scim/Users/2819c223-7f76-453a-919d-413861904646",
                "value":"2819c223-7f76-453a-919d-413861904646"}]}]}
  ````
  <span data-ttu-id="d04da-364">hello Microsoft ortak dil altyapısı kitaplıkları SCIM'yi Hizmetleri uygulamak için bir çağrı toohello hello hizmetin sağlayıcısının güncelleştirme yöntemini hello isteği çevirir.</span><span class="sxs-lookup"><span data-stu-id="d04da-364">hello Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate hello request into a call toohello Update method of hello service’s provider.</span></span> <span data-ttu-id="d04da-365">Merhaba güncelleştirme yöntemi hello imzası şöyledir:</span><span class="sxs-lookup"><span data-stu-id="d04da-365">Here is hello signature of hello Update method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks and 
    // System.Collections.Generic.IReadOnlyCollection<T>
    // are defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IPatch, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation, 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationName, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IPath and 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationValue 
    // are all defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 

    System.Threading.Tasks.Task Update(
      Microsoft.SystemForCrossDomainIdentityManagement.IPatch patch, 
      string correlationIdentifier);

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IPatch
    {
    Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase 
      PatchRequest 
        { get; set; }
    Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
      ResourceIdentifier 
        { get; set; }        
    }

    public class PatchRequest2: 
      Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase
    {
    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation> 
        Operations
        { get;}

    public void AddOperation(
      Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation operation);
    }

    public class PatchOperation
    {
    public Microsoft.SystemForCrossDomainIdentityManagement.OperationName 
      Name
      { get; set; }

    public Microsoft.SystemForCrossDomainIdentityManagement.IPath 
      Path
      { get; set; }

    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.OperationValue> Value
      { get; }

    public void AddValue(
      Microsoft.SystemForCrossDomainIdentityManagement.OperationValue value);
    }

    public enum OperationName
    {
      Add,
      Remove,
      Replace
    }

    public interface IPath
    {
      string AttributePath { get; }
      System.Collections.Generic.IReadOnlyCollection<IFilter> SubAttributes { get; }
      Microsoft.SystemForCrossDomainIdentityManagement.IPath ValuePath { get; }
    }

    public class OperationValue
    {
      public string Reference
      { get; set; }

      public string Value
      { get; set; }
    }
  ````
    <span data-ttu-id="d04da-366">İstek tooupdate kullanıcı Hello örnekte hello'hello düzeltme eki bağımsız değişkenin değeri sağlanan hello nesnesi bu özellik değerlerini içerir:</span><span class="sxs-lookup"><span data-stu-id="d04da-366">In hello example of a request tooupdate a user, hello object provided as hello value of hello patch argument has these property values:</span></span> 
  
  * <span data-ttu-id="d04da-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="d04da-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="d04da-368">ResourceIdentifier.SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="d04da-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>
  * <span data-ttu-id="d04da-369">(PatchRequest PatchRequest2 olarak). Operations.Count: 1</span><span class="sxs-lookup"><span data-stu-id="d04da-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span></span>
  * <span data-ttu-id="d04da-370">(PatchRequest PatchRequest2 olarak). Operations.ElementAt(0). OperationName: OperationName.Add</span><span class="sxs-lookup"><span data-stu-id="d04da-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span></span>
  * <span data-ttu-id="d04da-371">(PatchRequest PatchRequest2 olarak). Operations.ElementAt(0). Path.AttributePath: "Yönetici"</span><span class="sxs-lookup"><span data-stu-id="d04da-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span></span>
  * <span data-ttu-id="d04da-372">(PatchRequest PatchRequest2 olarak). Operations.ElementAt(0). Value.Count: 1</span><span class="sxs-lookup"><span data-stu-id="d04da-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span></span>
  * <span data-ttu-id="d04da-373">(PatchRequest PatchRequest2 olarak). Operations.ElementAt(0). Value.ElementAt(0). Başvuru: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="d04da-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span></span>
  * <span data-ttu-id="d04da-374">(PatchRequest PatchRequest2 olarak). Operations.ElementAt(0). Value.ElementAt(0). Değer: 2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="d04da-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span></span>

6. <span data-ttu-id="d04da-375">toode sağlama SCIM'yi hizmeti tarafından bir kimlik deposu kullanıcıdan fronted, Azure AD gibi bir isteği gönderir:</span><span class="sxs-lookup"><span data-stu-id="d04da-375">toode-provision a user from an identity store fronted by an SCIM service, Azure AD sends a request such as:</span></span> 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="d04da-376">Merhaba hizmet SCIM'yi Hizmetleri uygulamak için Microsoft tarafından sağlanan Merhaba ortak dil altyapısı kitaplıkları kullanılarak oluşturuldu, hello isteği çağrısı toohello hello hizmetin sağlayıcısının Delete yöntemini çevrilir.</span><span class="sxs-lookup"><span data-stu-id="d04da-376">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Delete method of hello service’s provider.</span></span>   <span data-ttu-id="d04da-377">Bu yöntem, bu imza sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d04da-377">That method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="d04da-378">Hello'hello resourceIdentifier bağımsız değişkenin değeri sağlanan hello nesnesi istek toode-provizyon kullanıcı hello örnekte bu özellik değerlerini içerir:</span><span class="sxs-lookup"><span data-stu-id="d04da-378">hello object provided as hello value of hello resourceIdentifier argument has these property values in hello example of a request toode-provision a user:</span></span> 
  
  * <span data-ttu-id="d04da-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="d04da-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="d04da-380">ResourceIdentifier.SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="d04da-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

## <a name="group-provisioning-and-de-provisioning"></a><span data-ttu-id="d04da-381">Grup sağlama ve sağlamayı kaldırma özelliklerini</span><span class="sxs-lookup"><span data-stu-id="d04da-381">Group provisioning and de-provisioning</span></span>
<span data-ttu-id="d04da-382">Merhaba, aşağıdaki çizimde gösterilmektedir Merhaba iletileri Azure AcD tooa SCIM'yi hizmet toomanage hello kullanım ömrü boyunca bir grubu başka bir kimlik deposu gönderir.</span><span class="sxs-lookup"><span data-stu-id="d04da-382">hello following illustration shows hello messages that Azure AcD sends tooa SCIM service toomanage hello lifecycle of a group in another identity store.</span></span>  <span data-ttu-id="d04da-383">Bu iletiler toousers üç yolla ilgili Merhaba iletileri farklıdır:</span><span class="sxs-lookup"><span data-stu-id="d04da-383">Those messages differ from hello messages pertaining toousers in three ways:</span></span> 

* <span data-ttu-id="d04da-384">bir grup kaynak Hello şeması http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="d04da-384">hello schema of a group resource is identified as http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  
* <span data-ttu-id="d04da-385">Bu hello üyeleri öznitelik tooretrieve grupları iznine isteği yanıt toohello isteğinde sağlanan herhangi bir kaynağa dışında toobe sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="d04da-385">Requests tooretrieve groups stipulate that hello members attribute is toobe excluded from any resource provided in response toohello request.</span></span>  
* <span data-ttu-id="d04da-386">İstekleri toodetermine olan istekleri hello üyeleri özniteliği hakkında bir başvuru özniteliği belirli bir değere sahip olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="d04da-386">Requests toodetermine whether a reference attribute has a certain value are requests about hello members attribute.</span></span>  

<span data-ttu-id="d04da-387">![][5]
*Şekil 6: Grup sağlama ve sağlamayı kaldırma özelliklerini sırası*</span><span class="sxs-lookup"><span data-stu-id="d04da-387">![][5]
*Figure 6: Group provisioning and de-provisioning sequence*</span></span>

## <a name="related-articles"></a><span data-ttu-id="d04da-388">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="d04da-388">Related articles</span></span>
* [<span data-ttu-id="d04da-389">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="d04da-389">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="d04da-390">Kullanıcı hazırlama/sağlama kaldırmayı tooSaaS uygulamaları otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="d04da-390">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="d04da-391">Kullanıcı sağlama öznitelik eşlemelerini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="d04da-391">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="d04da-392">Özellik eşlemeleri için ifade yazma</span><span class="sxs-lookup"><span data-stu-id="d04da-392">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="d04da-393">Kapsam belirleme filtreleri kullanıcı sağlama</span><span class="sxs-lookup"><span data-stu-id="d04da-393">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="d04da-394">Hesap sağlama bildirimleri</span><span class="sxs-lookup"><span data-stu-id="d04da-394">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="d04da-395">İlgili nasıl öğreticiler listesi tooIntegrate SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="d04da-395">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
