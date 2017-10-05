---
title: "Etki alanları arası Identity Management otomatik olarak sağlamak için kullanıcıları ve grupları Azure Active Directory'den uygulamalara sistemiyle | Microsoft Docs"
description: "Azure Active Directory Kullanıcıları ve grupları SCIM'yi protokolü belirtimi içinde tanımlı arabirimi ile bir web hizmeti tarafından fronted uygulama ya da kimliği deposuna otomatik olarak sağlayabilirsiniz"
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
ms.openlocfilehash: 91978cee88d55c99bcb63c63cdaf01581ae84668
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="using-system-for-cross-domain-identity-management-to-automatically-provision-users-and-groups-from-azure-active-directory-to-applications"></a><span data-ttu-id="65d04-103">Kullanıcıları ve grupları Azure Active Directory'den uygulamalara otomatik olarak sağlamak için etki alanları arası kimlik yönetimi sistemi kullanarak</span><span class="sxs-lookup"><span data-stu-id="65d04-103">Using System for Cross-Domain Identity Management to automatically provision users and groups from Azure Active Directory to applications</span></span>

## <a name="overview"></a><span data-ttu-id="65d04-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="65d04-104">Overview</span></span>
<span data-ttu-id="65d04-105">Azure Active Directory (Azure AD) otomatik olarak kullanıcı sağlama ve tanımlanan gruplar arabirimi ile bir web hizmeti tarafından fronted uygulama ya da kimliği deposuna [sistemi etki alanları arası Kimlik Yönetimi (SCIM'yi) 2.0 protokolü belirtimi için](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span><span class="sxs-lookup"><span data-stu-id="65d04-105">Azure Active Directory (Azure AD) can automatically provision users and groups to any application or identity store that is fronted by a web service with the interface defined in the [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span></span> <span data-ttu-id="65d04-106">Delete kullanıcılar ve gruplar web hizmetine atanan veya Azure Active Directory oluşturmak, değiştirmek için istek gönderemez.</span><span class="sxs-lookup"><span data-stu-id="65d04-106">Azure Active Directory can send requests to create, modify, or delete assigned users and groups to the web service.</span></span> <span data-ttu-id="65d04-107">Web hizmeti, hedef kimlik deposu işlemlere bu istekleri sonra anlamına gelebilir.</span><span class="sxs-lookup"><span data-stu-id="65d04-107">The web service can then translate those requests into operations on the target identity store.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="65d04-108">Microsoft, Azure AD’yi bu makalede bahsedilen Klasik Azure Portalı yerine Azure portalındaki [Azure AD yönetim merkezini](https://aad.portal.azure.com) kullanarak yönetmenizi öneriyor.</span><span class="sxs-lookup"><span data-stu-id="65d04-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 



<span data-ttu-id="65d04-109">![][0]
*Şekil 1: Bir web hizmeti aracılığıyla bir kimlik deposu için Azure Active Directory'den sağlama*</span><span class="sxs-lookup"><span data-stu-id="65d04-109">![][0]
*Figure 1: Provisioning from Azure Active Directory to an identity store via a web service*</span></span>

<span data-ttu-id="65d04-110">Bu özellik birlikte "kendi uygulamanızı getir" özelliğine sahip Azure AD çoklu oturum açma ve otomatik kullanıcı sağlayan veya SCIM'yi web hizmeti tarafından fronted uygulamalar için hazırlama etkinleştirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="65d04-110">This capability can be used in conjunction with the “bring your own app” capability in Azure AD to enable single sign-on and automatic user provisioning for applications that provide or are fronted by a SCIM web service.</span></span>

<span data-ttu-id="65d04-111">Azure Active Directory'de SCIM'yi kullanma iki kullanım örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="65d04-111">There are two use cases for using SCIM in Azure Active Directory:</span></span>

* <span data-ttu-id="65d04-112">**Kullanıcılar ve gruplar SCIM'yi destekleyen uygulamalar için sağlama** SCIM'yi 2.0 desteği ve yapılandırma olmadan Azure AD ile kimlik doğrulaması çalışır OAuth taşıyıcı belirteçlerini kullanmak uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="65d04-112">**Provisioning users and groups to applications that support SCIM** Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication works with Azure AD without configuration.</span></span>
* <span data-ttu-id="65d04-113">**Diğer API tabanlı sağlama destekleyen uygulamalar için kendi sağlama çözümü derleme** SCIM'yi olmayan uygulamalar için Azure AD SCIM'yi uç noktası ve uygulama destekleyen kullanıcı sağlama için herhangi bir API'yi arasında çevirmek için SCIM'yi uç noktası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65d04-113">**Build your own provisioning solution for applications that support other API-based provisioning** For non-SCIM applications, you can create a SCIM endpoint to translate between the Azure AD SCIM endpoint and any API the application supports for user provisioning.</span></span> <span data-ttu-id="65d04-114">Bir SCIM'yi uç noktası geliştirmenize yardımcı olması için SCIM'yi uç noktası sağlamak ve SCIM'yi iletileri çevirmek nasıl Göster kod örnekleri birlikte ortak dil altyapısı (CLI) kitaplıkları sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="65d04-114">To help you develop a SCIM endpoint, we provide Common Language Infrastructure (CLI) libraries along with code samples that show you how to do provide a SCIM endpoint and translate SCIM messages.</span></span>  

## <a name="provisioning-users-and-groups-to-applications-that-support-scim"></a><span data-ttu-id="65d04-115">Kullanıcılar ve gruplar SCIM'yi destekleyen uygulamalar için hazırlama</span><span class="sxs-lookup"><span data-stu-id="65d04-115">Provisioning users and groups to applications that support SCIM</span></span>
<span data-ttu-id="65d04-116">Azure AD, otomatik olarak sağlama atanan kullanıcılar ve gruplar kullanan uygulamalar için yapılandırılabilir bir [sistemi için etki alanları arası Kimlik Yönetimi 2 (SCIM'yi)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web hizmeti ve kimlik doğrulaması için OAuth taşıyıcı belirteçlerini kabul edin.</span><span class="sxs-lookup"><span data-stu-id="65d04-116">Azure AD can be configured to automatically provision assigned users and groups to applications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web service and accept OAuth bearer tokens for authentication.</span></span> <span data-ttu-id="65d04-117">SCIM'yi 2.0 belirtimi içinde uygulamalar bu gereksinimleri karşılamalıdır:</span><span class="sxs-lookup"><span data-stu-id="65d04-117">Within the SCIM 2.0 specification, applications must meet these requirements:</span></span>

* <span data-ttu-id="65d04-118">Kullanıcılara ve/veya bölüm 3.3 SCIM'yi Protokolü göredir grupları oluşturmayı destekler.</span><span class="sxs-lookup"><span data-stu-id="65d04-118">Supports creating users and/or groups, as per section 3.3 of the SCIM protocol.</span></span>  
* <span data-ttu-id="65d04-119">Kullanıcılara ve/veya SCIM'yi Protokolü 3.5.2'de bölümünü göredir patch isteklerinde gruplarla değiştirerek destekler.</span><span class="sxs-lookup"><span data-stu-id="65d04-119">Supports modifying users and/or groups with patch requests as per section 3.5.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="65d04-120">Bilinen kaynak SCIM'yi Protokolü 3.4.1 bölümünü göredir alma destekler.</span><span class="sxs-lookup"><span data-stu-id="65d04-120">Supports retrieving a known resource as per section 3.4.1 of the SCIM protocol.</span></span>  
* <span data-ttu-id="65d04-121">Kullanıcılara ve/veya SCIM'yi Protokolü 3.4.2 bölümünü göredir grupları sorgulama destekler.</span><span class="sxs-lookup"><span data-stu-id="65d04-121">Supports querying users and/or groups, as per section 3.4.2 of the SCIM protocol.</span></span>  <span data-ttu-id="65d04-122">Varsayılan olarak, kullanıcılar tarafından externalID seçmeleri istenir ve grupları displayName tarafından sorgulanır.</span><span class="sxs-lookup"><span data-stu-id="65d04-122">By default, users are queried by externalId and groups are queried by displayName.</span></span>  
* <span data-ttu-id="65d04-123">Kullanıcı kimliği ve bölüm 3.4.2 SCIM'yi Protokolü göredir Yöneticisi tarafından sorgulama destekler.</span><span class="sxs-lookup"><span data-stu-id="65d04-123">Supports querying user by ID and by manager as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="65d04-124">Grup Kimliği ve bölüm 3.4.2 SCIM'yi Protokolü göredir üye tarafından sorgulama destekler.</span><span class="sxs-lookup"><span data-stu-id="65d04-124">Supports querying groups by ID and by member as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="65d04-125">Bölüm 2.1 göredir yetkilendirme SCIM'yi protokolü için OAuth taşıyıcı belirteçleri kabul eder.</span><span class="sxs-lookup"><span data-stu-id="65d04-125">Accepts OAuth bearer tokens for authorization as per section 2.1 of the SCIM protocol.</span></span>

<span data-ttu-id="65d04-126">Uygulama sağlayıcınıza veya bu gereksinimleri ile uyumluluk bilgilerinin uygulama sağlayıcınızın belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="65d04-126">Check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span></span>

### <a name="getting-started"></a><span data-ttu-id="65d04-127">Başlarken</span><span class="sxs-lookup"><span data-stu-id="65d04-127">Getting started</span></span>
<span data-ttu-id="65d04-128">Bu makalede açıklanan SCIM'yi profili destekleyen uygulamalar Azure AD uygulama galerisinde "galeri olmayan uygulama" özelliği kullanılarak Azure Active Directory'ye bağlı.</span><span class="sxs-lookup"><span data-stu-id="65d04-128">Applications that support the SCIM profile described in this article can be connected to Azure Active Directory using the "non-gallery application" feature in the Azure AD application gallery.</span></span> <span data-ttu-id="65d04-129">Bağlandıktan sonra Azure AD eşitleme işlemi burada uygulamanın SCIM'yi endpoint atanan kullanıcılar ve gruplar için sorgular ve oluşturur veya göre atama ayrıntıları değiştirir 20 dakikada bir çalışır.</span><span class="sxs-lookup"><span data-stu-id="65d04-129">Once connected, Azure AD runs a synchronization process every 20 minutes where it queries the application's SCIM endpoint for assigned users and groups, and creates or modifies them according to the assignment details.</span></span>

<span data-ttu-id="65d04-130">**SCIM'yi destekleyen bir uygulama bağlanmak için:**</span><span class="sxs-lookup"><span data-stu-id="65d04-130">**To connect an application that supports SCIM:**</span></span>

1. <span data-ttu-id="65d04-131">Oturum [Azure portalı](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="65d04-131">Sign in to [the Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="65d04-132">Gözat ** Azure Active Directory > Kurumsal uygulamaları ve select **yeni uygulama > tüm > olmayan galeri uygulama**.</span><span class="sxs-lookup"><span data-stu-id="65d04-132">Browse to **Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="65d04-133">Uygulamanız için bir ad girin ve tıklayın **Ekle** uygulama nesne oluşturmak için simge.</span><span class="sxs-lookup"><span data-stu-id="65d04-133">Enter a name for your application, and click **Add** icon to create an app object.</span></span>
    
  <span data-ttu-id="65d04-134">![][1]
  *Şekil 2: Azure AD uygulama galerisinde*</span><span class="sxs-lookup"><span data-stu-id="65d04-134">![][1]
*Figure 2: Azure AD application gallery*</span></span>
    
4. <span data-ttu-id="65d04-135">Sonuçta elde edilen ekranında şunları seçin **sağlama** sol sütunda sekmesi.</span><span class="sxs-lookup"><span data-stu-id="65d04-135">In the resulting screen, select the **Provisioning** tab in the left column.</span></span>
5. <span data-ttu-id="65d04-136">İçinde **sağlama modu** menüsünde, select **otomatik**.</span><span class="sxs-lookup"><span data-stu-id="65d04-136">In the **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="65d04-137">![][2]
  *Şekil 3: Azure portalında sağlama yapılandırma*</span><span class="sxs-lookup"><span data-stu-id="65d04-137">![][2]
*Figure 3: Configuring provisioning in the Azure portal*</span></span>
    
6. <span data-ttu-id="65d04-138">İçinde **Kiracı URL** alanında, uygulamanın SCIM'yi uç nokta URL'sini girin.</span><span class="sxs-lookup"><span data-stu-id="65d04-138">In the **Tenant URL** field, enter the URL of the application's SCIM endpoint.</span></span> <span data-ttu-id="65d04-139">Örnek: https://api.contoso.com/scim/v2/</span><span class="sxs-lookup"><span data-stu-id="65d04-139">Example: https://api.contoso.com/scim/v2/</span></span>
7. <span data-ttu-id="65d04-140">Ardından SCIM'yi uç noktanın bir OAuth taşıyıcı belirtecinden Azure AD dışında bir veren gerektiriyorsa, gerekli OAuth taşıyıcı belirteci isteğe bağlı kopyalamak **gizli belirteci** alan.</span><span class="sxs-lookup"><span data-stu-id="65d04-140">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span></span> <span data-ttu-id="65d04-141">Bu alan boş bırakılırsa, Azure AD her istek ile Azure AD tarafından verilen bir OAuth taşıyıcı belirteci dahil.</span><span class="sxs-lookup"><span data-stu-id="65d04-141">If this field is left blank, then Azure AD included an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="65d04-142">Azure AD kimlik sağlayıcısı bu Azure AD doğrulayabilirsiniz olarak kullanan uygulamaları-belirteç.</span><span class="sxs-lookup"><span data-stu-id="65d04-142">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="65d04-143">Tıklatın **Bağlantıyı Sına** SCIM'yi bitiş noktasına bağlanmaya Azure Active Directory için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="65d04-143">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="65d04-144">Deneme başarısız olursa hata bilgileri görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="65d04-144">If the attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="65d04-145">Uygulama başarılı için bağlanmaya çalışırsa sonra tıklatırsanız **kaydetmek** yönetici kimlik bilgilerini kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="65d04-145">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span></span>
10. <span data-ttu-id="65d04-146">İçinde **eşlemeleri** bölümünde, iki seçilebilir öznitelik eşlemelerini kümesi vardır: biri kullanıcı nesneleri ve Grup nesneleri için bir tane.</span><span class="sxs-lookup"><span data-stu-id="65d04-146">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="65d04-147">Uygulamanız için Azure Active Directory'den eşitlenen öznitelikler gözden geçirmek için her birini seçin.</span><span class="sxs-lookup"><span data-stu-id="65d04-147">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span></span> <span data-ttu-id="65d04-148">Seçilen öznitelikler **eşleşen** özellikleri, kullanıcıları ve grupları güncelleştirme işlemleri için uygulamanızda eşleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="65d04-148">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span></span> <span data-ttu-id="65d04-149">Değişiklikleri kaydetmek için Kaydet düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="65d04-149">Select the Save button to commit any changes.</span></span>

    >[!NOTE]
    ><span data-ttu-id="65d04-150">İsteğe bağlı olarak, "eşleme grupları" devre dışı bırakarak group nesnelerini eşitlemeyi devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="65d04-150">You can optionally disable syncing of group objects by disabling the "groups" mapping.</span></span> 

11. <span data-ttu-id="65d04-151">Altında **ayarları**, **kapsam** alanı tanımlar hangi kullanıcı ve grup veya eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="65d04-151">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="65d04-152">"Eşitleme yalnızca kullanıcılar ve gruplar (önerilen) atanan" seçerek yalnızca eşitleme kullanıcılar ve gruplar atanan **kullanıcılar ve gruplar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="65d04-152">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span></span>
12. <span data-ttu-id="65d04-153">Yapılandırma tamamlandıktan sonra değiştirmek **sağlama durumu** için **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="65d04-153">Once your configuration is complete, change the **Provisioning Status** to **On**.</span></span>
13. <span data-ttu-id="65d04-154">Tıklatın **kaydetmek** hizmet sağlama Azure AD başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="65d04-154">Click **Save** to start the Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="65d04-155">Eşitlemeyi yalnızca kullanıcılar ve gruplar (önerilen) atanmışsa, seçtiğinizden emin olun **kullanıcılar ve gruplar** sekmesinde ve kullanıcılara ve/veya eşitlemek istediğiniz grupları atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65d04-155">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span></span>

<span data-ttu-id="65d04-156">İlk eşitleme başladıktan sonra kullanabileceğiniz **denetim günlüklerini** uygulamanızı sağlama hizmeti tarafından gerçekleştirilen tüm eylemler gösterir İzleyici ilerleme sekmesine.</span><span class="sxs-lookup"><span data-stu-id="65d04-156">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span></span> <span data-ttu-id="65d04-157">Günlükleri sağlama Azure AD okuma hakkında daha fazla bilgi için bkz: [otomatik olarak bir kullanıcı hesabı sağlama raporlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="65d04-157">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

>[!NOTE]
><span data-ttu-id="65d04-158">İlk eşitleme gerçekleştirmek yaklaşık 20 dakikada çalıştığı sürece oluşan sonraki eşitlemeler uzun sürer.</span><span class="sxs-lookup"><span data-stu-id="65d04-158">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> 


## <a name="building-your-own-provisioning-solution-for-any-application"></a><span data-ttu-id="65d04-159">Herhangi bir uygulama için kendi sağlama çözümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="65d04-159">Building your own provisioning solution for any application</span></span>
<span data-ttu-id="65d04-160">Azure Active Directory ile arabirimleri SCIM'yi web hizmeti oluşturarak, bir REST veya SOAP kullanıcı API hazırlama sağlar neredeyse her uygulama için tek oturum açma ve otomatik kullanıcı sağlamayı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65d04-160">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span></span>

<span data-ttu-id="65d04-161">İşte nasıl çalışır:</span><span class="sxs-lookup"><span data-stu-id="65d04-161">Here’s how it works:</span></span>

1. <span data-ttu-id="65d04-162">Azure AD sağlar adlı ortak dil altyapısı kitaplık [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span><span class="sxs-lookup"><span data-stu-id="65d04-162">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span></span> <span data-ttu-id="65d04-163">Sistem tümleştiricileri ve geliştiriciler bu kitaplığı oluşturmak ve bir SCIM'yi tabanlı web hizmeti uç noktası için herhangi bir uygulamanın kimlik deposu Azure AD bağlanıp bağlanamayacağını dağıtmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65d04-163">System integrators and developers can use this library to create and deploy a SCIM-based web service endpoint capable of connecting Azure AD to any application’s identity store.</span></span>
2. <span data-ttu-id="65d04-164">Eşlemeleri kullanıcı şema ve uygulama tarafından istenen Protokolü standartlaştırılmış kullanıcı şemasını eşleştirmek için web hizmeti uygulanır.</span><span class="sxs-lookup"><span data-stu-id="65d04-164">Mappings are implemented in the web service to map the standardized user schema to the user schema and protocol required by the application.</span></span>
3. <span data-ttu-id="65d04-165">Uç nokta URL'sini Azure AD uygulama galerisinde özel bir uygulama bir parçası olarak kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="65d04-165">The endpoint URL is registered in Azure AD as part of a custom application in the application gallery.</span></span>
4. <span data-ttu-id="65d04-166">Kullanıcıları ve grupları, Azure AD'de bu uygulama atanır.</span><span class="sxs-lookup"><span data-stu-id="65d04-166">Users and groups are assigned to this application in Azure AD.</span></span> <span data-ttu-id="65d04-167">Atama sırasında bunlar hedef uygulama için eşitlenecek kuyruğuna yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="65d04-167">Upon assignment, they are put into a queue to be synchronized to the target application.</span></span> <span data-ttu-id="65d04-168">Sıranın işleme eşitleme işlemi 20 dakikada bir çalışır.</span><span class="sxs-lookup"><span data-stu-id="65d04-168">The synchronization process handling the queue runs every 20 minutes.</span></span>

### <a name="code-samples"></a><span data-ttu-id="65d04-169">Kod Örnekleri</span><span class="sxs-lookup"><span data-stu-id="65d04-169">Code Samples</span></span>
<span data-ttu-id="65d04-170">Bu işlem daha kolay, bir dizi yapmak için [kod örnekleri](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) SCIM'yi web hizmeti uç noktası oluşturun ve otomatik sağlamayı göstermek sağlanır.</span><span class="sxs-lookup"><span data-stu-id="65d04-170">To make this process easier, a set of [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span></span> <span data-ttu-id="65d04-171">Kullanıcılar ve gruplar temsil eden virgülle ayrılmış değerler satırlarla bir dosyayı korur bir sağlayıcının bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="65d04-171">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span></span>  <span data-ttu-id="65d04-172">Diğer Amazon Web Hizmetleri kimlik ve erişim yönetimi hizmetini çalışır bir sağlayıcı değil.</span><span class="sxs-lookup"><span data-stu-id="65d04-172">The other is of a provider that operates on the Amazon Web Services Identity and Access Management service.</span></span>  

<span data-ttu-id="65d04-173">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="65d04-173">**Prerequisites**</span></span>

* <span data-ttu-id="65d04-174">Visual Studio 2013 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="65d04-174">Visual Studio 2013 or later</span></span>
* [<span data-ttu-id="65d04-175">.NET için Azure SDK</span><span class="sxs-lookup"><span data-stu-id="65d04-175">Azure SDK for .NET</span></span>](https://azure.microsoft.com/downloads/)
* <span data-ttu-id="65d04-176">SCIM'yi uç noktası olarak kullanılacak ASP.NET framework 4.5 destekleyen Windows makine.</span><span class="sxs-lookup"><span data-stu-id="65d04-176">Windows machine that supports the ASP.NET framework 4.5 to be used as the SCIM endpoint.</span></span> <span data-ttu-id="65d04-177">Bu makinenin buluttan erişilebilir olması gerekir</span><span class="sxs-lookup"><span data-stu-id="65d04-177">This machine must be accessible from the cloud</span></span>
* [<span data-ttu-id="65d04-178">Bir Azure aboneliği ile Azure AD Premium deneme veya lisanslı bir sürümü</span><span class="sxs-lookup"><span data-stu-id="65d04-178">An Azure subscription with a trial or licensed version of Azure AD Premium</span></span>](https://azure.microsoft.com/services/active-directory/)
* <span data-ttu-id="65d04-179">Amazon AWS örneği kitaplıklarından gerektirir [Visual Studio için AWS Araç Seti](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span><span class="sxs-lookup"><span data-stu-id="65d04-179">The Amazon AWS sample requires libraries from the [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span></span> <span data-ttu-id="65d04-180">Daha fazla bilgi için örnekle dahil Benioku dosyasına bakın.</span><span class="sxs-lookup"><span data-stu-id="65d04-180">For more information, see the README file included with the sample.</span></span>

### <a name="getting-started"></a><span data-ttu-id="65d04-181">Başlarken</span><span class="sxs-lookup"><span data-stu-id="65d04-181">Getting Started</span></span>
<span data-ttu-id="65d04-182">Azure AD'den sağlama isteklerini kabul edebilir bir SCIM'yi uç noktası uygulamak için kolay derleme ve sağlanan kullanıcılar bir virgülle ayrılmış değer (CSV) dosyasına çıkarır kod örneği dağıtma yoludur.</span><span class="sxs-lookup"><span data-stu-id="65d04-182">The easiest way to implement a SCIM endpoint that can accept provisioning requests from Azure AD is to build and deploy the code sample that outputs the provisioned users to a comma-separated value (CSV) file.</span></span>

<span data-ttu-id="65d04-183">**Bir örnek SCIM'yi uç noktası oluşturmak için:**</span><span class="sxs-lookup"><span data-stu-id="65d04-183">**To create a sample SCIM endpoint:**</span></span>

1. <span data-ttu-id="65d04-184">Kod örnek paketin karşıdan [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span><span class="sxs-lookup"><span data-stu-id="65d04-184">Download the code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span></span>
2. <span data-ttu-id="65d04-185">Paketin sıkıştırmasını açın ve Windows makinenizdeki C:\AzureAD-BYOA-Provisioning-Samples\ gibi bir konuma yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="65d04-185">Unzip the package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span></span>
3. <span data-ttu-id="65d04-186">Bu klasörde, Visual Studio FileProvisioningAgent çözümde başlatın.</span><span class="sxs-lookup"><span data-stu-id="65d04-186">In this folder, launch the FileProvisioningAgent solution in Visual Studio.</span></span>
4. <span data-ttu-id="65d04-187">Seçin **Araçlar > Kitaplık Paket Yöneticisi > Paket Yöneticisi Konsolu**ve çözüm başvuruları çözümlemek FileProvisioningAgent projesi için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="65d04-187">Select **Tools > Library Package Manager > Package Manager Console**, and execute the following commands for the FileProvisioningAgent project to resolve the solution references:</span></span>
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. <span data-ttu-id="65d04-188">FileProvisioningAgent projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="65d04-188">Build the FileProvisioningAgent project.</span></span>
6. <span data-ttu-id="65d04-189">Windows komut istemi uygulamada (Yönetici) olarak başlatın ve kullanmak **cd** dizine değiştirmek için komutu, **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** klasör.</span><span class="sxs-lookup"><span data-stu-id="65d04-189">Launch the Command Prompt application in Windows (as an Administrator), and use the **cd** command to change the directory to your **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span></span>
7. <span data-ttu-id="65d04-190">< IP adresi > IP adresine veya etki alanı adıyla Windows makinenin değiştirerek aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="65d04-190">Run the following command, replacing <ip-address> with the IP address or domain name of the Windows machine:</span></span>
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. <span data-ttu-id="65d04-191">Altında Windows'ta **Windows Ayarları > Ağ ve Internet ayarlarını**seçin **Windows Güvenlik Duvarı > Gelişmiş ayarları**ve oluşturma bir **gelen kuralı** 9000 numaralı bağlantı noktasına gelen erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="65d04-191">In Windows under **Windows Settings > Network & Internet Settings**, select the **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access to port 9000.</span></span>
9. <span data-ttu-id="65d04-192">Windows makine yönlendiricisi arkasında ise, yönlendirici, bağlantı noktası Internet'e açık 9000 ve bağlantı noktası 9000 Windows makinede arasındaki ağ erişim çevirisi gerçekleştirecek şekilde yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="65d04-192">If the Windows machine is behind a router, the router needs to be configured to perform Network Access Translation between its port 9000 that is exposed to the internet, and port 9000 on the Windows machine.</span></span> <span data-ttu-id="65d04-193">Bu bulutta Bu uç noktasına erişmek Azure AD için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="65d04-193">This is required for Azure AD to be able to access this endpoint in the cloud.</span></span>

<span data-ttu-id="65d04-194">**Azure AD'de örnek SCIM'yi uç noktasını kaydetmek için:**</span><span class="sxs-lookup"><span data-stu-id="65d04-194">**To register the sample SCIM endpoint in Azure AD:**</span></span>

1. <span data-ttu-id="65d04-195">Oturum [Azure portalı](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="65d04-195">Sign in to [the Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="65d04-196">Gözat ** Azure Active Directory > Kurumsal uygulamaları ve select **yeni uygulama > tüm > olmayan galeri uygulama**.</span><span class="sxs-lookup"><span data-stu-id="65d04-196">Browse to **Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="65d04-197">Uygulamanız için bir ad girin ve tıklayın **Ekle** uygulama nesne oluşturmak için simge.</span><span class="sxs-lookup"><span data-stu-id="65d04-197">Enter a name for your application, and click **Add** icon to create an app object.</span></span> <span data-ttu-id="65d04-198">Oluşturulan uygulama nesnesi olmaları için sağlama ve çoklu oturum açma için ve yalnızca SCIM'yi uç uygulama hedef uygulama temsil etmek üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="65d04-198">The application object created is intended to represent the target app you would be provisioning to and implementing single sign-on for, and not just the SCIM endpoint.</span></span>
4. <span data-ttu-id="65d04-199">Sonuçta elde edilen ekranında şunları seçin **sağlama** sol sütunda sekmesi.</span><span class="sxs-lookup"><span data-stu-id="65d04-199">In the resulting screen, select the **Provisioning** tab in the left column.</span></span>
5. <span data-ttu-id="65d04-200">İçinde **sağlama modu** menüsünde, select **otomatik**.</span><span class="sxs-lookup"><span data-stu-id="65d04-200">In the **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="65d04-201">![][2]
  *Şekil 4: Azure portalında sağlama yapılandırma*</span><span class="sxs-lookup"><span data-stu-id="65d04-201">![][2]
*Figure 4: Configuring provisioning in the Azure portal*</span></span>
    
6. <span data-ttu-id="65d04-202">İçinde **Kiracı URL** alanında, Internet kullanıma sunulan URL ve bağlantı noktası SCIM'yi uç noktanızı girin.</span><span class="sxs-lookup"><span data-stu-id="65d04-202">In the **Tenant URL** field, enter the internet-exposed URL and port of your SCIM endpoint.</span></span> <span data-ttu-id="65d04-203">Http://testmachine.contoso.com:9000 veya http://<ip-address>:9000/, burada < IP adresi >, internet IP kullanıma sunulan gibi bu bir şey olacaktır adresi.</span><span class="sxs-lookup"><span data-stu-id="65d04-203">This would be something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is the internet exposed IP address.</span></span>  
7. <span data-ttu-id="65d04-204">Ardından SCIM'yi uç noktanın bir OAuth taşıyıcı belirtecinden Azure AD dışında bir veren gerektiriyorsa, gerekli OAuth taşıyıcı belirteci isteğe bağlı kopyalamak **gizli belirteci** alan.</span><span class="sxs-lookup"><span data-stu-id="65d04-204">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span></span> <span data-ttu-id="65d04-205">Bu alan boş bırakılırsa, Azure AD her istek ile Azure AD tarafından verilen bir OAuth taşıyıcı belirteci dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="65d04-205">If this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="65d04-206">Azure AD kimlik sağlayıcısı bu Azure AD doğrulayabilirsiniz olarak kullanan uygulamaları-belirteç.</span><span class="sxs-lookup"><span data-stu-id="65d04-206">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="65d04-207">Tıklatın **Bağlantıyı Sına** SCIM'yi bitiş noktasına bağlanmaya Azure Active Directory için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="65d04-207">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="65d04-208">Deneme başarısız olursa hata bilgileri görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="65d04-208">If the attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="65d04-209">Uygulama başarılı için bağlanmaya çalışırsa sonra tıklatırsanız **kaydetmek** yönetici kimlik bilgilerini kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="65d04-209">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span></span>
10. <span data-ttu-id="65d04-210">İçinde **eşlemeleri** bölümünde, iki seçilebilir öznitelik eşlemelerini kümesi vardır: biri kullanıcı nesneleri ve Grup nesneleri için bir tane.</span><span class="sxs-lookup"><span data-stu-id="65d04-210">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="65d04-211">Uygulamanız için Azure Active Directory'den eşitlenen öznitelikler gözden geçirmek için her birini seçin.</span><span class="sxs-lookup"><span data-stu-id="65d04-211">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span></span> <span data-ttu-id="65d04-212">Seçilen öznitelikler **eşleşen** özellikleri, kullanıcıları ve grupları güncelleştirme işlemleri için uygulamanızda eşleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="65d04-212">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span></span> <span data-ttu-id="65d04-213">Değişiklikleri kaydetmek için Kaydet düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="65d04-213">Select the Save button to commit any changes.</span></span>
11. <span data-ttu-id="65d04-214">Altında **ayarları**, **kapsam** alanı tanımlar hangi kullanıcı ve grup veya eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="65d04-214">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="65d04-215">"Eşitleme yalnızca kullanıcılar ve gruplar (önerilen) atanan" seçerek yalnızca eşitleme kullanıcılar ve gruplar atanan **kullanıcılar ve gruplar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="65d04-215">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span></span>
12. <span data-ttu-id="65d04-216">Yapılandırma tamamlandıktan sonra değiştirmek **sağlama durumu** için **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="65d04-216">Once your configuration is complete, change the **Provisioning Status** to **On**.</span></span>
13. <span data-ttu-id="65d04-217">Tıklatın **kaydetmek** hizmet sağlama Azure AD başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="65d04-217">Click **Save** to start the Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="65d04-218">Eşitlemeyi yalnızca kullanıcılar ve gruplar (önerilen) atanmışsa, seçtiğinizden emin olun **kullanıcılar ve gruplar** sekmesinde ve kullanıcılara ve/veya eşitlemek istediğiniz grupları atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65d04-218">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span></span>

<span data-ttu-id="65d04-219">İlk eşitleme başladıktan sonra kullanabileceğiniz **denetim günlüklerini** uygulamanızı sağlama hizmeti tarafından gerçekleştirilen tüm eylemler gösterir İzleyici ilerleme sekmesine.</span><span class="sxs-lookup"><span data-stu-id="65d04-219">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span></span> <span data-ttu-id="65d04-220">Günlükleri sağlama Azure AD okuma hakkında daha fazla bilgi için bkz: [otomatik olarak bir kullanıcı hesabı sağlama raporlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="65d04-220">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

<span data-ttu-id="65d04-221">Windows makinenizi \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug klasöründe TargetFile.csv dosyayı açmak için örnek doğrulama son adım var.</span><span class="sxs-lookup"><span data-stu-id="65d04-221">The final step in verifying the sample is to open the TargetFile.csv file in the \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span></span> <span data-ttu-id="65d04-222">Sağlama işlemini çalıştırdıktan sonra bu dosyayı tüm ayrıntılarını atanan ve kullanıcılar ve gruplar sağlanan gösterir.</span><span class="sxs-lookup"><span data-stu-id="65d04-222">Once the provisioning process is run, this file shows the details of all assigned and provisioned users and groups.</span></span>

### <a name="development-libraries"></a><span data-ttu-id="65d04-223">Geliştirme kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="65d04-223">Development libraries</span></span>
<span data-ttu-id="65d04-224">SCIM'yi belirtimine uygun kendi web hizmeti geliştirmek için öncelikle geliştirme sürecinin artırmanıza yardımcı olmak üzere Microsoft tarafından sağlanan aşağıdaki kitaplıkları tanıyın:</span><span class="sxs-lookup"><span data-stu-id="65d04-224">To develop your own web service that conforms to the SCIM specification, first familiarize yourself with the following libraries provided by Microsoft to help accelerate the development process:</span></span> 

1. <span data-ttu-id="65d04-225">Ortak dil altyapısı (CLI) kitaplıklar gibi C#, altyapı göre dilleri ile kullanıma sunulur.</span><span class="sxs-lookup"><span data-stu-id="65d04-225">Common Language Infrastructure (CLI) libraries are offered for use with languages based on that infrastructure, such as C#.</span></span> <span data-ttu-id="65d04-226">Bu kitaplıklar birini [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), aşağıdaki çizimde gösterilen bir arabirim Microsoft.SystemForCrossDomainIdentityManagement.IProvider, bildirir: kitaplıkları kullanarak bir geliştirici bu arabirim için genel olarak, bir sağlayıcısı olarak adlandırılabilir sınıfıyla uygulamak.</span><span class="sxs-lookup"><span data-stu-id="65d04-226">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in the following illustration:  A developer using the libraries would implement that interface with a class that may be referred to, generically, as a provider.</span></span> <span data-ttu-id="65d04-227">Kitaplıklar için SCIM'yi belirtimi uyumlu bir web hizmeti dağıtmak Geliştirici etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="65d04-227">The libraries enable the developer to deploy a web service that conforms to the SCIM specification.</span></span> <span data-ttu-id="65d04-228">Web hizmeti ya da Internet Information Services veya yürütülebilir bir ortak dil altyapısı derlemesi içinde barındırılabilir.</span><span class="sxs-lookup"><span data-stu-id="65d04-228">The web service can be either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span></span> <span data-ttu-id="65d04-229">İstek, bazı kimlik deposu üzerinde çalışması için geliştirici tarafından programlanmış sağlayıcının yöntem çağrıları veri dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="65d04-229">Request is translated into calls to the provider’s methods, which would be programmed by the developer to operate on some identity store.</span></span>
  
  ![][3]
  
2. <span data-ttu-id="65d04-230">[Rota işleyicileri express](http://expressjs.com/guide/routing.html) bir node.js web hizmeti çağrıları (SCIM'yi belirtimi tarafından tanımlandığı gibi) temsil eden bir node.js isteği nesneleri ayrıştırma için kullanılabilir yapılır.</span><span class="sxs-lookup"><span data-stu-id="65d04-230">[Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by the SCIM specification), made to a node.js web service.</span></span>   

### <a name="building-a-custom-scim-endpoint"></a><span data-ttu-id="65d04-231">Bir özel SCIM'yi uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="65d04-231">Building a Custom SCIM Endpoint</span></span>
<span data-ttu-id="65d04-232">CLI kitaplıkları kullanarak, bu kitaplığı kullanan geliştiriciler kendi Hizmetleri veya Internet Information Services yürütülebilir ortak dil altyapısı derlemeler içinde barındırabilir.</span><span class="sxs-lookup"><span data-stu-id="65d04-232">Using the CLI libraries, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span></span> <span data-ttu-id="65d04-233">Http://localhost:9000 adresindeki yürütülebilir bütünleştirilmiş kod içinde bir hizmet barındırma için örnek kod aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="65d04-233">Here is sample code for hosting a service within an executable assembly, at the address http://localhost:9000:</span></span> 

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

<span data-ttu-id="65d04-234">Bu hizmet kök sertifika yetkilisi aşağıdakilerden biri olduğu bir HTTP adresi ve bir sunucu kimlik doğrulama sertifikası olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="65d04-234">This service must have an HTTP address and server authentication certificate of which the root certification authority is one of the following:</span></span> 

* <span data-ttu-id="65d04-235">CNNIC</span><span class="sxs-lookup"><span data-stu-id="65d04-235">CNNIC</span></span>
* <span data-ttu-id="65d04-236">Comodo</span><span class="sxs-lookup"><span data-stu-id="65d04-236">Comodo</span></span>
* <span data-ttu-id="65d04-237">CyberTrust</span><span class="sxs-lookup"><span data-stu-id="65d04-237">CyberTrust</span></span>
* <span data-ttu-id="65d04-238">DigiCert</span><span class="sxs-lookup"><span data-stu-id="65d04-238">DigiCert</span></span>
* <span data-ttu-id="65d04-239">GeoTrust</span><span class="sxs-lookup"><span data-stu-id="65d04-239">GeoTrust</span></span>
* <span data-ttu-id="65d04-240">GlobalSign</span><span class="sxs-lookup"><span data-stu-id="65d04-240">GlobalSign</span></span>
* <span data-ttu-id="65d04-241">Daddy gidin</span><span class="sxs-lookup"><span data-stu-id="65d04-241">Go Daddy</span></span>
* <span data-ttu-id="65d04-242">VeriSign</span><span class="sxs-lookup"><span data-stu-id="65d04-242">Verisign</span></span>
* <span data-ttu-id="65d04-243">WoSign</span><span class="sxs-lookup"><span data-stu-id="65d04-243">WoSign</span></span>

<span data-ttu-id="65d04-244">Bir sunucu kimlik doğrulama sertifikası ağ Kabuğu yardımcı programını kullanarak bir Windows ana bilgisayarda bir bağlantı noktasına bağlı olabilir:</span><span class="sxs-lookup"><span data-stu-id="65d04-244">A server authentication certificate can be bound to a port on a Windows host using the network shell utility:</span></span> 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

<span data-ttu-id="65d04-245">Burada, rastgele bir genel benzersiz tanımlayıcı olsa da AppID bağımsız değişkeni için sağlanan değer certhash bağımsız değişkeni için sağlanan değer sertifikanın parmak izini ' dir.</span><span class="sxs-lookup"><span data-stu-id="65d04-245">Here, the value provided for the certhash argument is the thumbprint of the certificate, while the value provided for the appid argument is an arbitrary globally unique identifier.</span></span>  

<span data-ttu-id="65d04-246">Internet Information Services hizmetinde barındırmak için bir geliştirici bir CLA kod kitaplığı başlangıç derleme varsayılan ad alanı adlı bir sınıf ile derleme.</span><span class="sxs-lookup"><span data-stu-id="65d04-246">To host the service within Internet Information Services, a developer would build a CLA code library assembly with a class named Startup in the default namespace of the assembly.</span></span>  <span data-ttu-id="65d04-247">Böyle bir sınıfın bir örneği aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="65d04-247">Here is a sample of such a class:</span></span> 

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

### <a name="handling-endpoint-authentication"></a><span data-ttu-id="65d04-248">İşleme uç noktası kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="65d04-248">Handling endpoint authentication</span></span>
<span data-ttu-id="65d04-249">Azure Active Directory gelen istekleri bir OAuth 2.0 taşıyıcı belirteci içerir.</span><span class="sxs-lookup"><span data-stu-id="65d04-249">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span></span>   <span data-ttu-id="65d04-250">İsteği alma herhangi bir hizmet olarak Azure Active Directory Azure Active Directory Graph web hizmetine erişim için beklenen Azure Active Directory Kiracı adına veren kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="65d04-250">Any service receiving the request should authenticate the issuer as being Azure Active Directory on behalf of the expected Azure Active Directory tenant, for access to the Azure Active Directory Graph web service.</span></span>  <span data-ttu-id="65d04-251">Belirteç veren "ISS" gibi bir ISS talep tanımlanır: "https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span><span class="sxs-lookup"><span data-stu-id="65d04-251">In the token, the issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span></span>  <span data-ttu-id="65d04-252">Bu örnekte, talep değeri, taban adresini https://sts.windows.net, göreli adres segment cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, hangi adına belirteç verildiği Azure Active Directory Kiracı benzersiz bir tanımlayıcı olsa da bu Azure Active Directory, veren tanımlar.</span><span class="sxs-lookup"><span data-stu-id="65d04-252">In this example, the base address of the claim value, https://sts.windows.net, identifies Azure Active Directory as the issuer, while the relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of the Azure Active Directory tenant on behalf of which the token was issued.</span></span>  <span data-ttu-id="65d04-253">Azure Active Directory Graph web hizmetine erişmek için belirteç verilmişse, 00000002-0000-0000-c000-000000000000, bu hizmeti tanıtıcısı belirtecin aud talebin değeri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="65d04-253">If the token was issued for accessing the Azure Active Directory Graph web service, then the identifier of that service, 00000002-0000-0000-c000-000000000000, should be in the value of the token’s aud claim.</span></span>  

<span data-ttu-id="65d04-254">Geliştiriciler SCIM'yi hizmet oluşturmak için Microsoft tarafından sağlanan CLA kitaplıkları kullanarak aşağıdaki adımları izleyerek Microsoft.Owin.Security.ActiveDirectory paketi kullanılarak Azure Active Directory'ye gelen istekleri doğrulayabilir:</span><span class="sxs-lookup"><span data-stu-id="65d04-254">Developers using the CLA libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using the Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span></span> 

1. <span data-ttu-id="65d04-255">Sağlayıcı, bu hizmeti başlatıldığında çağrılacak döndürme sağlayarak Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior özelliği uygulayın:</span><span class="sxs-lookup"><span data-stu-id="65d04-255">In a provider, implement the Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method to be called whenever the service is started:</span></span> 

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

2. <span data-ttu-id="65d04-256">Bu yöntem herhangi bir hizmetin uç noktaları erişim Azure AD grafik web hizmeti için belirtilen bir kiracı adına Azure Active Directory tarafından verilmiş bir belirteç pul olarak kimlik doğrulaması için herhangi bir istek olması için aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="65d04-256">Add the following code to that method to have any request to any of the service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access to the Azure AD Graph web service:</span></span> 

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
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute the appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a><span data-ttu-id="65d04-257">Kullanıcı ve Grup şeması</span><span class="sxs-lookup"><span data-stu-id="65d04-257">User and group schema</span></span>
<span data-ttu-id="65d04-258">Azure Active Directory iki tür kaynak SCIM'yi web hizmetlerine sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65d04-258">Azure Active Directory can provision two types of resources to SCIM web services.</span></span>  <span data-ttu-id="65d04-259">Bu kaynakların kullanıcılar ve gruplar türleridir.</span><span class="sxs-lookup"><span data-stu-id="65d04-259">Those types of resources are users and groups.</span></span>  

<span data-ttu-id="65d04-260">Kullanıcı kaynakları şema tanımlayıcısı, bu protokolü belirtimi içinde bulunan urn: ietf:params:scim:schemas:extension:enterprise:2.0:User tanımlanır: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span><span class="sxs-lookup"><span data-stu-id="65d04-260">User resources are identified by the schema identifier, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span></span>  <span data-ttu-id="65d04-261">Azure Active Directory'de kullanıcıları urn: ietf:params:scim:schemas:extension:enterprise:2.0:User kaynakları özniteliklerinin özniteliklerinin varsayılan eşleme Tablo 1, aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="65d04-261">The default mapping of the attributes of users in Azure Active Directory to the attributes of urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resources is provided in table 1, below.</span></span>  

<span data-ttu-id="65d04-262">Grup kaynaklarının şema tanımlayıcısı tarafından tanımlanan http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="65d04-262">Group resources are identified by the schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  <span data-ttu-id="65d04-263">Azure Active Directory'deki öznitelikleri için http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group kaynak grupları özniteliklerinin varsayılan eşleme Tablo 2, aşağıda gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="65d04-263">Table 2, below, shows the default mapping of the attributes of groups in Azure Active Directory to the attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span></span>  

### <a name="table-1-default-user-attribute-mapping"></a><span data-ttu-id="65d04-264">Tablo 1: Varsayılan kullanıcı özniteliği eşlemesi</span><span class="sxs-lookup"><span data-stu-id="65d04-264">Table 1: Default user attribute mapping</span></span>
| <span data-ttu-id="65d04-265">Azure Active Directory kullanıcısı</span><span class="sxs-lookup"><span data-stu-id="65d04-265">Azure Active Directory user</span></span> | <span data-ttu-id="65d04-266">urn: ietf:params:scim:schemas:extension:enterprise:2.0:User</span><span class="sxs-lookup"><span data-stu-id="65d04-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span></span> |
| --- | --- |
| <span data-ttu-id="65d04-267">IsSoftDeleted</span><span class="sxs-lookup"><span data-stu-id="65d04-267">IsSoftDeleted</span></span> |<span data-ttu-id="65d04-268">Etkin</span><span class="sxs-lookup"><span data-stu-id="65d04-268">active</span></span> |
| <span data-ttu-id="65d04-269">Görünen adı</span><span class="sxs-lookup"><span data-stu-id="65d04-269">displayName</span></span> |<span data-ttu-id="65d04-270">Görünen adı</span><span class="sxs-lookup"><span data-stu-id="65d04-270">displayName</span></span> |
| <span data-ttu-id="65d04-271">Faks TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="65d04-271">Facsimile-TelephoneNumber</span></span> |<span data-ttu-id="65d04-272">PhoneNumber [türü eq "faks"] .value</span><span class="sxs-lookup"><span data-stu-id="65d04-272">phoneNumbers[type eq "fax"].value</span></span> |
| <span data-ttu-id="65d04-273">givenName</span><span class="sxs-lookup"><span data-stu-id="65d04-273">givenName</span></span> |<span data-ttu-id="65d04-274">name.givenName</span><span class="sxs-lookup"><span data-stu-id="65d04-274">name.givenName</span></span> |
| <span data-ttu-id="65d04-275">İş Unvanı</span><span class="sxs-lookup"><span data-stu-id="65d04-275">jobTitle</span></span> |<span data-ttu-id="65d04-276">Başlık</span><span class="sxs-lookup"><span data-stu-id="65d04-276">title</span></span> |
| <span data-ttu-id="65d04-277">Posta</span><span class="sxs-lookup"><span data-stu-id="65d04-277">mail</span></span> |<span data-ttu-id="65d04-278">e-postaları [türü eq "İş"] .value</span><span class="sxs-lookup"><span data-stu-id="65d04-278">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="65d04-279">mailNickname</span><span class="sxs-lookup"><span data-stu-id="65d04-279">mailNickname</span></span> |<span data-ttu-id="65d04-280">externalID</span><span class="sxs-lookup"><span data-stu-id="65d04-280">externalId</span></span> |
| <span data-ttu-id="65d04-281">Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="65d04-281">manager</span></span> |<span data-ttu-id="65d04-282">Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="65d04-282">manager</span></span> |
| <span data-ttu-id="65d04-283">Mobil</span><span class="sxs-lookup"><span data-stu-id="65d04-283">mobile</span></span> |<span data-ttu-id="65d04-284">PhoneNumber [türü eq "mobile"] .value</span><span class="sxs-lookup"><span data-stu-id="65d04-284">phoneNumbers[type eq "mobile"].value</span></span> |
| <span data-ttu-id="65d04-285">objectID</span><span class="sxs-lookup"><span data-stu-id="65d04-285">objectId</span></span> |<span data-ttu-id="65d04-286">id</span><span class="sxs-lookup"><span data-stu-id="65d04-286">id</span></span> |
| <span data-ttu-id="65d04-287">posta kodu</span><span class="sxs-lookup"><span data-stu-id="65d04-287">postalCode</span></span> |<span data-ttu-id="65d04-288">adresler [türü eq "İş"] .postalCode</span><span class="sxs-lookup"><span data-stu-id="65d04-288">addresses[type eq "work"].postalCode</span></span> |
| <span data-ttu-id="65d04-289">Proxy adresleri</span><span class="sxs-lookup"><span data-stu-id="65d04-289">proxy-Addresses</span></span> |<span data-ttu-id="65d04-290">e-postaları [eq "diğer" yazın]. Değer</span><span class="sxs-lookup"><span data-stu-id="65d04-290">emails[type eq "other"].Value</span></span> |
| <span data-ttu-id="65d04-291">fiziksel teslim OfficeName</span><span class="sxs-lookup"><span data-stu-id="65d04-291">physical-Delivery-OfficeName</span></span> |<span data-ttu-id="65d04-292">adresler [eq "diğer" yazın]. Biçimlendirilmiş</span><span class="sxs-lookup"><span data-stu-id="65d04-292">addresses[type eq "other"].Formatted</span></span> |
| <span data-ttu-id="65d04-293">StreetAddress</span><span class="sxs-lookup"><span data-stu-id="65d04-293">streetAddress</span></span> |<span data-ttu-id="65d04-294">adresler [türü eq "İş"] .streetAddress</span><span class="sxs-lookup"><span data-stu-id="65d04-294">addresses[type eq "work"].streetAddress</span></span> |
| <span data-ttu-id="65d04-295">Soyadı</span><span class="sxs-lookup"><span data-stu-id="65d04-295">surname</span></span> |<span data-ttu-id="65d04-296">name.familyName</span><span class="sxs-lookup"><span data-stu-id="65d04-296">name.familyName</span></span> |
| <span data-ttu-id="65d04-297">telefon numarası</span><span class="sxs-lookup"><span data-stu-id="65d04-297">telephone-Number</span></span> |<span data-ttu-id="65d04-298">PhoneNumber [türü eq "İş"] .value</span><span class="sxs-lookup"><span data-stu-id="65d04-298">phoneNumbers[type eq "work"].value</span></span> |
| <span data-ttu-id="65d04-299">Kullanıcı PrincipalName</span><span class="sxs-lookup"><span data-stu-id="65d04-299">user-PrincipalName</span></span> |<span data-ttu-id="65d04-300">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="65d04-300">userName</span></span> |

### <a name="table-2-default-group-attribute-mapping"></a><span data-ttu-id="65d04-301">Tablo 2: Varsayılan grup özellik eşlemesi</span><span class="sxs-lookup"><span data-stu-id="65d04-301">Table 2: Default group attribute mapping</span></span>
| <span data-ttu-id="65d04-302">Azure Active Directory grubu</span><span class="sxs-lookup"><span data-stu-id="65d04-302">Azure Active Directory group</span></span> | <span data-ttu-id="65d04-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span><span class="sxs-lookup"><span data-stu-id="65d04-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span></span> |
| --- | --- |
| <span data-ttu-id="65d04-304">Görünen adı</span><span class="sxs-lookup"><span data-stu-id="65d04-304">displayName</span></span> |<span data-ttu-id="65d04-305">externalID</span><span class="sxs-lookup"><span data-stu-id="65d04-305">externalId</span></span> |
| <span data-ttu-id="65d04-306">Posta</span><span class="sxs-lookup"><span data-stu-id="65d04-306">mail</span></span> |<span data-ttu-id="65d04-307">e-postaları [türü eq "İş"] .value</span><span class="sxs-lookup"><span data-stu-id="65d04-307">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="65d04-308">mailNickname</span><span class="sxs-lookup"><span data-stu-id="65d04-308">mailNickname</span></span> |<span data-ttu-id="65d04-309">Görünen adı</span><span class="sxs-lookup"><span data-stu-id="65d04-309">displayName</span></span> |
| <span data-ttu-id="65d04-310">Üyeleri</span><span class="sxs-lookup"><span data-stu-id="65d04-310">members</span></span> |<span data-ttu-id="65d04-311">Üyeleri</span><span class="sxs-lookup"><span data-stu-id="65d04-311">members</span></span> |
| <span data-ttu-id="65d04-312">objectID</span><span class="sxs-lookup"><span data-stu-id="65d04-312">objectId</span></span> |<span data-ttu-id="65d04-313">id</span><span class="sxs-lookup"><span data-stu-id="65d04-313">id</span></span> |
| <span data-ttu-id="65d04-314">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="65d04-314">proxyAddresses</span></span> |<span data-ttu-id="65d04-315">e-postaları [eq "diğer" yazın]. Değer</span><span class="sxs-lookup"><span data-stu-id="65d04-315">emails[type eq "other"].Value</span></span> |

## <a name="user-provisioning-and-de-provisioning"></a><span data-ttu-id="65d04-316">Kullanıcı hazırlama ve sağlamayı kaldırma özelliklerini</span><span class="sxs-lookup"><span data-stu-id="65d04-316">User provisioning and de-provisioning</span></span>
<span data-ttu-id="65d04-317">Aşağıdaki çizimde gösterildiği Azure Active Directory kullanıcı başka bir kimlik deposu olarak ömrünü yönetmek için SCIM'yi Hizmeti'ne gönderilen iletileri.</span><span class="sxs-lookup"><span data-stu-id="65d04-317">The following illustration shows the messages that Azure Active Directory sends to a SCIM service to manage the lifecycle of a user in another identity store.</span></span> <span data-ttu-id="65d04-318">Diyagram ayrıca nasıl CLI kitaplıkları kullanılarak uygulanan SCIM'yi sağlanan bir hizmeti Microsoft tarafından yapı için bir sağlayıcı yöntem çağrıları içine bu istekleri gibi hizmetleri Çevir gösterir.</span><span class="sxs-lookup"><span data-stu-id="65d04-318">The diagram also shows how a SCIM service implemented using the CLI libraries provided by Microsoft for building such services translate those requests into calls to the methods of a provider.</span></span>  

<span data-ttu-id="65d04-319">![][4]
*Şekil 5: Kullanıcı sağlama ve sağlamayı kaldırma özelliklerini sırası*</span><span class="sxs-lookup"><span data-stu-id="65d04-319">![][4]
*Figure 5: User provisioning and de-provisioning sequence*</span></span>

1. <span data-ttu-id="65d04-320">Azure AD'de kullanıcı mailNickname öznitelik değerini eşleşen bir externalID öznitelik değeri olan bir kullanıcı için hizmet Azure Active Directory'yi sorgular.</span><span class="sxs-lookup"><span data-stu-id="65d04-320">Azure Active Directory queries the service for a user with an externalId attribute value matching the mailNickname attribute value of a user in Azure AD.</span></span> <span data-ttu-id="65d04-321">Sorgu; burada görüntülerle jyoung mailNickname bir kullanıcının Azure Active Directory'de örneğidir Bu örnekte gibi bir Köprü Metni Aktarım Protokolü (HTTP) istek olarak ifade edilir:</span><span class="sxs-lookup"><span data-stu-id="65d04-321">The query is expressed as a Hypertext Transfer Protocol (HTTP) request such as this example, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span></span> 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="65d04-322">Hizmet SCIM'yi Hizmetleri uygulamak için Microsoft tarafından sağlanan ortak dil altyapısı kitaplıkları kullanılarak oluşturuldu, istek sorgu yöntemi hizmet sağlayıcı için bir çağrı çevrilir.</span><span class="sxs-lookup"><span data-stu-id="65d04-322">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span></span>  <span data-ttu-id="65d04-323">Bu yöntem imzası şöyledir:</span><span class="sxs-lookup"><span data-stu-id="65d04-323">Here is the signature of that method:</span></span> 
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
  <span data-ttu-id="65d04-324">Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters arabirim tanımı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="65d04-324">Here is the definition of the Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span></span> 
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
  <span data-ttu-id="65d04-325">Bir kullanıcı için bir sorgu externalID özniteliği için belirtilen bir değerle aşağıdaki örnekte sorgu yönteme geçirilen bağımsız değişkenlerin değerleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="65d04-325">In the following sample of a query for a user with a given value for the externalId attribute, values of the arguments passed to the Query method are:</span></span> 
  * <span data-ttu-id="65d04-326">parametreleri. AlternateFilters.Count: 1</span><span class="sxs-lookup"><span data-stu-id="65d04-326">parameters.AlternateFilters.Count: 1</span></span>
  * <span data-ttu-id="65d04-327">parametreleri. AlternateFilters.ElementAt(0). AttributePath: "externalID"</span><span class="sxs-lookup"><span data-stu-id="65d04-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span></span>
  * <span data-ttu-id="65d04-328">parametreleri. AlternateFilters.ElementAt(0). Karşılaştırmaİşleci: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="65d04-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="65d04-329">parametreleri. AlternateFilter.ElementAt(0). ComparisonValue: "jyoung"</span><span class="sxs-lookup"><span data-stu-id="65d04-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span></span>
  * <span data-ttu-id="65d04-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin. RequestId"]</span><span class="sxs-lookup"><span data-stu-id="65d04-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span></span> 

2. <span data-ttu-id="65d04-331">Web hizmeti, bir kullanıcının mailNickname öznitelik değeri ile eşleşen bir externalID öznitelik değeri olan bir kullanıcı için bir sorguya yanıt herhangi bir kullanıcının döndürmezse, Azure Active Directory hizmeti bir Azure Active Directory'de karşılık gelen bir kullanıcı sağlamak ister.</span><span class="sxs-lookup"><span data-stu-id="65d04-331">If the response to a query to the web service for a user with an externalId attribute value that matches the mailNickname attribute value of a user does not return any users, then Azure Active Directory requests that the service provision a user corresponding to the one in Azure Active Directory.</span></span>  <span data-ttu-id="65d04-332">Böyle bir istek bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="65d04-332">Here is an example of such a request:</span></span> 
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
  <span data-ttu-id="65d04-333">SCIM'yi Hizmetleri uygulamak için Microsoft tarafından sağlanan ortak dil altyapısı kitaplıkları bu isteği oluşturma yöntemi hizmet sağlayıcı için bir çağrı çevirir.</span><span class="sxs-lookup"><span data-stu-id="65d04-333">The Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call to the Create method of the service’s provider.</span></span>  <span data-ttu-id="65d04-334">Create yönteminin bu imzaya sahip:</span><span class="sxs-lookup"><span data-stu-id="65d04-334">The Create method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="65d04-335">Bir kullanıcı sağlamak için istekte kaynak bağımsız değişkeninin değeri Microsoft.SystemForCrossDomainIdentityManagement örneğidir.</span><span class="sxs-lookup"><span data-stu-id="65d04-335">In a request to provision a user, the value of the resource argument is an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="65d04-336">Microsoft.SystemForCrossDomainIdentityManagement.Schemas Kitaplığı'nda tanımlanan Core2EnterpriseUser sınıfı.</span><span class="sxs-lookup"><span data-stu-id="65d04-336">Core2EnterpriseUser class, defined in the Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span></span>  <span data-ttu-id="65d04-337">Kullanıcı sağlama isteği başarılı olursa, yöntemin kullanımı Microsoft.SystemForCrossDomainIdentityManagement örneği döndürmesi beklenir.</span><span class="sxs-lookup"><span data-stu-id="65d04-337">If the request to provision the user succeeds, then the implementation of the method is expected to return an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="65d04-338">Yeni sağlanan kullanıcının benzersiz tanımlayıcıya ayarlamak tanımlayıcı özelliğinin değeri ile Core2EnterpriseUser sınıfı.</span><span class="sxs-lookup"><span data-stu-id="65d04-338">Core2EnterpriseUser class, with the value of the Identifier property set to the unique identifier of the newly provisioned user.</span></span>  

3. <span data-ttu-id="65d04-339">Bir kullanıcı tarafından bir SCIM'yi fronted kimlik deposunda bilinmektedir güncelleştirmek için Azure Active Directory gibi bir istekle hizmetinden kullanıcı geçerli durumunu isteyerek çalışır:</span><span class="sxs-lookup"><span data-stu-id="65d04-339">To update a user known to exist in an identity store fronted by an SCIM, Azure Active Directory proceeds by requesting the current state of that user from the service with a request such as:</span></span> 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="65d04-340">SCIM'yi Hizmetleri uygulamak için Microsoft tarafından sağlanan ortak dil altyapısı kitaplıkları kullanılarak oluşturulmuş bir hizmeti, hizmet sağlayıcısının alma yöntemine bir çağrı isteği çevrilir.</span><span class="sxs-lookup"><span data-stu-id="65d04-340">In a service built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, the request is translated into a call to the Retrieve method of the service’s provider.</span></span>  <span data-ttu-id="65d04-341">Alma yöntemi imzası şöyledir:</span><span class="sxs-lookup"><span data-stu-id="65d04-341">Here is the signature of the Retrieve method:</span></span> 
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
  <span data-ttu-id="65d04-342">Kullanıcının geçerli durumunu almak için bir istek örnekte parametreleri bağımsız değişkenin değeri sağlanan nesne özelliklerinin değerleri aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="65d04-342">In the example of a request to retrieve the current state of a user, the values of the properties of the object provided as the value of the parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="65d04-343">Tanımlayıcı: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="65d04-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="65d04-344">SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="65d04-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

4. <span data-ttu-id="65d04-345">Azure Active Directory kimlik deposu olarak başvuru özniteliği geçerli değeri hizmeti tarafından zaten fronted olup olmadığını belirlemek üzere hizmetini sorgular ardından güncelleştirilmesi için bir başvuru özniteliği ise Azure Active Directory'de bu özniteliğin değeri ile eşleşir.</span><span class="sxs-lookup"><span data-stu-id="65d04-345">If a reference attribute is to be updated, then Azure Active Directory queries the service to determine whether or not the current value of the reference attribute in the identity store fronted by the service already matches the value of that attribute in Azure Active Directory.</span></span> <span data-ttu-id="65d04-346">Kullanıcılar için bu şekilde sorgulanan geçerli değeri yalnızca öznitelik Yöneticisi özniteliğidir.</span><span class="sxs-lookup"><span data-stu-id="65d04-346">For users, the only attribute of which the current value is queried in this way is the manager attribute.</span></span> <span data-ttu-id="65d04-347">Belirli bir kullanıcı nesnesinin Yöneticisi özniteliği şu anda belirli bir değere sahip olup olmadığını belirlemek için bir istek bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="65d04-347">Here is an example of a request to determine whether the manager attribute of a particular user object currently has a certain value:</span></span> 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="65d04-348">Değer öznitelikleri sorgu parametresinin kimliği güveninin, bir kullanıcı nesnesi filtre sorgu parametresi değeri olarak sağlanan ifade karşılayan varsa, ardından hizmeti yalnızca o kaynağın Kimliği özniteliğinin değeri de dahil olmak üzere urn: ietf:params:scim:schemas:core:2.0:User veya urn: ietf:params:scim:schemas:extension:enterprise:2.0:User sahip bir kaynak, yanıt vermesi bekleniyor.</span><span class="sxs-lookup"><span data-stu-id="65d04-348">The value of the attributes query parameter, id, signifies that if a user object exists that satisfies the expression provided as the value of the filter query parameter, then the service is expected to respond with a urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, including only the value of that resource’s id attribute.</span></span>  <span data-ttu-id="65d04-349">Değeri **kimliği** istek sahibine bilinen öznitelik.</span><span class="sxs-lookup"><span data-stu-id="65d04-349">The value of the **id** attribute is known to the requestor.</span></span> <span data-ttu-id="65d04-350">Filtre sorgu parametresi değeri içinde bulunur; Filtre ifadesinin olup olmadığına böyle bir nesne var olan bir göstergesi olarak çağıran bir kaynak en az bir gösterimini istemek üzere söylemelisiniz amacı gerçekte var.</span><span class="sxs-lookup"><span data-stu-id="65d04-350">It is included in the value of the filter query parameter; the purpose of asking for it is actually to request a minimal representation of a resource that satisfying the filter expression as an indication of whether or not any such object exists.</span></span>   

  <span data-ttu-id="65d04-351">Hizmet SCIM'yi Hizmetleri uygulamak için Microsoft tarafından sağlanan ortak dil altyapısı kitaplıkları kullanılarak oluşturuldu, istek sorgu yöntemi hizmet sağlayıcı için bir çağrı çevrilir.</span><span class="sxs-lookup"><span data-stu-id="65d04-351">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span></span> <span data-ttu-id="65d04-352">Parametre bağımsız değişkenin değeri sağlanan nesne özelliklerini değeri aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="65d04-352">The value of the properties of the object provided as the value of the parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="65d04-353">parametreleri. AlternateFilters.Count: 2</span><span class="sxs-lookup"><span data-stu-id="65d04-353">parameters.AlternateFilters.Count: 2</span></span>
  * <span data-ttu-id="65d04-354">parametreleri. AlternateFilters.ElementAt(x). AttributePath: "id"</span><span class="sxs-lookup"><span data-stu-id="65d04-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span></span>
  * <span data-ttu-id="65d04-355">parametreleri. AlternateFilters.ElementAt(x). Karşılaştırmaİşleci: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="65d04-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="65d04-356">parametreleri. AlternateFilter.ElementAt(x). ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="65d04-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="65d04-357">parametreleri. AlternateFilters.ElementAt(y). AttributePath: "Yönetici"</span><span class="sxs-lookup"><span data-stu-id="65d04-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span></span>
  * <span data-ttu-id="65d04-358">parametreleri. AlternateFilters.ElementAt(y). Karşılaştırmaİşleci: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="65d04-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="65d04-359">parametreleri. AlternateFilter.ElementAt(y). ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span><span class="sxs-lookup"><span data-stu-id="65d04-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span></span>
  * <span data-ttu-id="65d04-360">parametreleri. RequestedAttributePaths.ElementAt(0): "id"</span><span class="sxs-lookup"><span data-stu-id="65d04-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span></span>
  * <span data-ttu-id="65d04-361">parametreleri. SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="65d04-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

  <span data-ttu-id="65d04-362">Burada, dizinin x değeri 0 olabilir ve dizin y değeri 1, olabilir ya da x değerini 1 olabilir ve y değeri filtre sorgu parametresi ifadelerin sırasını bağlı olarak 0 olabilir.</span><span class="sxs-lookup"><span data-stu-id="65d04-362">Here, the value of the index x may be 0 and the value of the index y may be 1, or the value of x may be 1 and the value of y may be 0, depending on the order of the expressions of the filter query parameter.</span></span>   

5. <span data-ttu-id="65d04-363">Bir isteğin bir kullanıcıyı güncelleştirmek için SCIM'yi hizmetine örnek Azure Active Directory'den verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="65d04-363">Here is an example of a request from Azure Active Directory to an SCIM service to update a user:</span></span> 
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
  <span data-ttu-id="65d04-364">Microsoft ortak dil altyapısı kitaplıkları SCIM'yi Hizmetleri uygulamak için hizmet sağlayıcısı'nın güncelleştirme yöntemine bir çağrı isteği çevirir.</span><span class="sxs-lookup"><span data-stu-id="65d04-364">The Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate the request into a call to the Update method of the service’s provider.</span></span> <span data-ttu-id="65d04-365">Update yöntemi imzası şöyledir:</span><span class="sxs-lookup"><span data-stu-id="65d04-365">Here is the signature of the Update method:</span></span> 
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
    <span data-ttu-id="65d04-366">Kullanıcıyı güncelleştirmek için bir istek örnekte, bu özellik değerlerini düzeltme eki bağımsız değişkenin değeri sağlanan nesne vardır:</span><span class="sxs-lookup"><span data-stu-id="65d04-366">In the example of a request to update a user, the object provided as the value of the patch argument has these property values:</span></span> 
  
  * <span data-ttu-id="65d04-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="65d04-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="65d04-368">ResourceIdentifier.SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="65d04-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>
  * <span data-ttu-id="65d04-369">(PatchRequest PatchRequest2 olarak). Operations.Count: 1</span><span class="sxs-lookup"><span data-stu-id="65d04-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span></span>
  * <span data-ttu-id="65d04-370">(PatchRequest PatchRequest2 olarak). Operations.ElementAt(0). OperationName: OperationName.Add</span><span class="sxs-lookup"><span data-stu-id="65d04-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span></span>
  * <span data-ttu-id="65d04-371">(PatchRequest PatchRequest2 olarak). Operations.ElementAt(0). Path.AttributePath: "Yönetici"</span><span class="sxs-lookup"><span data-stu-id="65d04-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span></span>
  * <span data-ttu-id="65d04-372">(PatchRequest PatchRequest2 olarak). Operations.ElementAt(0). Value.Count: 1</span><span class="sxs-lookup"><span data-stu-id="65d04-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span></span>
  * <span data-ttu-id="65d04-373">(PatchRequest PatchRequest2 olarak). Operations.ElementAt(0). Value.ElementAt(0). Başvuru: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="65d04-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span></span>
  * <span data-ttu-id="65d04-374">(PatchRequest PatchRequest2 olarak). Operations.ElementAt(0). Value.ElementAt(0). Değer: 2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="65d04-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span></span>

6. <span data-ttu-id="65d04-375">Bir kullanıcı bir SCIM'yi hizmeti tarafından fronted kimlik mağazadan sağlanmasını için Azure AD gibi bir isteği gönderir:</span><span class="sxs-lookup"><span data-stu-id="65d04-375">To de-provision a user from an identity store fronted by an SCIM service, Azure AD sends a request such as:</span></span> 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="65d04-376">Hizmet SCIM'yi Hizmetleri uygulamak için Microsoft tarafından sağlanan ortak dil altyapısı kitaplıkları kullanılarak oluşturuldu, istek hizmet sağlayıcısının Delete yöntemine bir çağrı çevrilir.</span><span class="sxs-lookup"><span data-stu-id="65d04-376">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Delete method of the service’s provider.</span></span>   <span data-ttu-id="65d04-377">Bu yöntem, bu imza sahiptir:</span><span class="sxs-lookup"><span data-stu-id="65d04-377">That method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="65d04-378">Bu özellik değerlerini resourceIdentifier bağımsız değişkenin değeri sağlanan nesne kullanıcı sağlanmasını isteği örnekte vardır:</span><span class="sxs-lookup"><span data-stu-id="65d04-378">The object provided as the value of the resourceIdentifier argument has these property values in the example of a request to de-provision a user:</span></span> 
  
  * <span data-ttu-id="65d04-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="65d04-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="65d04-380">ResourceIdentifier.SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="65d04-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

## <a name="group-provisioning-and-de-provisioning"></a><span data-ttu-id="65d04-381">Grup sağlama ve sağlamayı kaldırma özelliklerini</span><span class="sxs-lookup"><span data-stu-id="65d04-381">Group provisioning and de-provisioning</span></span>
<span data-ttu-id="65d04-382">Aşağıdaki çizimde gösterildiği Azure AcD bir grubu başka bir kimlik deposu içinde yaşam döngüsü yönetmek için SCIM'yi Hizmeti'ne gönderilen iletileri.</span><span class="sxs-lookup"><span data-stu-id="65d04-382">The following illustration shows the messages that Azure AcD sends to a SCIM service to manage the lifecycle of a group in another identity store.</span></span>  <span data-ttu-id="65d04-383">Bu iletiler, kullanıcılara üç yolla ilgili iletiler farklıdır:</span><span class="sxs-lookup"><span data-stu-id="65d04-383">Those messages differ from the messages pertaining to users in three ways:</span></span> 

* <span data-ttu-id="65d04-384">Bir grup kaynağına şema http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="65d04-384">The schema of a group resource is identified as http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  
* <span data-ttu-id="65d04-385">Grupları almak için yapılan isteklerinin üyeleri öznitelik isteğine yanıt olarak sağlanan herhangi bir kaynağa dışında tutulması olduğunu iznine.</span><span class="sxs-lookup"><span data-stu-id="65d04-385">Requests to retrieve groups stipulate that the members attribute is to be excluded from any resource provided in response to the request.</span></span>  
* <span data-ttu-id="65d04-386">Bir başvuru özniteliği belirli bir değere sahip olup olmadığını belirlemek üzere istekleri üyeleri özniteliği hakkında isteklerdir.</span><span class="sxs-lookup"><span data-stu-id="65d04-386">Requests to determine whether a reference attribute has a certain value are requests about the members attribute.</span></span>  

<span data-ttu-id="65d04-387">![][5]
*Şekil 6: Grup sağlama ve sağlamayı kaldırma özelliklerini sırası*</span><span class="sxs-lookup"><span data-stu-id="65d04-387">![][5]
*Figure 6: Group provisioning and de-provisioning sequence*</span></span>

## <a name="related-articles"></a><span data-ttu-id="65d04-388">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="65d04-388">Related articles</span></span>
* [<span data-ttu-id="65d04-389">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="65d04-389">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="65d04-390">Kullanıcı sağlama/sağlamayı SaaS uygulamaları için otomatik hale getirme</span><span class="sxs-lookup"><span data-stu-id="65d04-390">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="65d04-391">Kullanıcı sağlama öznitelik eşlemelerini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="65d04-391">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="65d04-392">Özellik eşlemeleri için ifade yazma</span><span class="sxs-lookup"><span data-stu-id="65d04-392">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="65d04-393">Kapsam belirleme filtreleri kullanıcı sağlama</span><span class="sxs-lookup"><span data-stu-id="65d04-393">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="65d04-394">Hesap sağlama bildirimleri</span><span class="sxs-lookup"><span data-stu-id="65d04-394">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="65d04-395">SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="65d04-395">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
