---
title: "Azure Active Directory’de uygulamalar, izinler ve onay.| Microsoft Docs"
description: "Azure AD Connect, şirket içi dizinlerinizi Azure Active Directory ile tümleştirir. Bu, Office 365, Azure ve SaaS uygulamaları için ortak bir kimlik Azure AD ile tümleşik tooprovide sağlar."
keywords: "Azure AD Connect nedir giriş tooAzure AD, uygulamalar, active Directory'yi yükleyin"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 25897cc4-7687-49b6-b0d5-71f51302b6b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/31/2017
ms.author: billmath
ms.reviewer: jesakowi
ms.custom: oldportal;it-pro;
ms.openlocfilehash: af0c2669199736fdb41e85876a7e3a7064e80770
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a><span data-ttu-id="8fb9e-105">Azure Active Directory’de uygulamalar, izinler ve onay</span><span class="sxs-lookup"><span data-stu-id="8fb9e-105">Apps, permissions, and consent in Azure Active Directory</span></span>
<span data-ttu-id="8fb9e-106">Azure Active Directory içinde uygulamalar tooyour dizini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-106">Within Azure Active Directory, you can add applications tooyour directory.</span></span>  <span data-ttu-id="8fb9e-107">Merhaba uygulamaları uygulama hello türüne bağlı olarak değişebilir.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-107">hello applications can vary depending on hello type of application.</span></span>  <span data-ttu-id="8fb9e-108">tooview uygulamalar hello Klasik Portalı'nda bir dizin seçin ve uygulamaları seçin.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-108">tooview applications in hello classic portal, select a directory and choose applications.</span></span>

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> <span data-ttu-id="8fb9e-109">Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-109">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

## <a name="types-of-apps"></a><span data-ttu-id="8fb9e-110">Uygulama türleri</span><span class="sxs-lookup"><span data-stu-id="8fb9e-110">Types of apps</span></span>

1. <span data-ttu-id="8fb9e-111">**Tek kiracılı uygulamalar**</span><span class="sxs-lookup"><span data-stu-id="8fb9e-111">**Single-tenant apps**</span></span> </br>
    - <span data-ttu-id="8fb9e-112">**Tek Kiracı uygulamaları** -genellikle tooas iş kolu (LOB) uygulamaları adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-112">**Single-tenant apps** - Often referred tooas line-of-business (LOB) apps.</span></span> <span data-ttu-id="8fb9e-113">Burada birisi kuruluşunuz içinde kendi uygulama geliştirir ve hello kuruluş toobe mümkün toosign toohello uygulamasında kullanıcıların görmesini hello böyledir.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-113">This is hello case where someone within your organization develops their own app, and would like users in hello organization toobe able toosign in toohello app.</span></span>
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - <span data-ttu-id="8fb9e-114">**Uygulama proxy'si uygulamaları** - Azure AD uygulaması Proxy, şirket içi uygulamayla kullanıma tek Kiracı uygulama kiracınızda (toplama toohello uygulama Proxy Hizmeti) kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-114">**App Proxy apps** - When you expose an on-prem application with Azure AD App Proxy, a single-tenant app is registered in your tenant (in addition toohello App Proxy service).</span></span> <span data-ttu-id="8fb9e-115">Bu uygulama tüm bulut etkileşimleri (örneğin, kimlik doğrulaması) için şirket içi uygulamanızı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-115">This app is what represents your on-prem application for all cloud interactions (for example, authentication).</span></span> <span data-ttu-id="8fb9e-116">(Uygulama Ara Sunucusu, Azure AD Temel veya daha yüksek sürüm gerektirir.)</span><span class="sxs-lookup"><span data-stu-id="8fb9e-116">(App Proxy requires Azure AD Basic or higher.)</span></span>


2. <span data-ttu-id="8fb9e-117">**Çok kiracılı uygulamalar**</span><span class="sxs-lookup"><span data-stu-id="8fb9e-117">**Multi-tenant apps**</span></span>
    - <span data-ttu-id="8fb9e-118">**Diğerleri için onay çok kiracılı uygulamalar** - benzer çok "kuruluşunuzun geliştirdiği uygulamalarla tek Kiracı uygulamalar".</span><span class="sxs-lookup"><span data-stu-id="8fb9e-118">**Multi-tenant apps which others can consent to** - similar too“single-tenant apps that your organization develops”.</span></span> <span data-ttu-id="8fb9e-119">Merhaba ana (Merhaba uygulama mantığı hello) yanı sıra diğer kiracılar kullanıcılardan de toohello uygulamasında tooand oturum onay farktır.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-119">hello main difference (besides hello logic in hello app itself) is that users from other tenants can also consent tooand sign in toohello app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - <span data-ttu-id="8fb9e-120">**Başkalarının geliştirdiği ve Contoso’nun onay verebildiği çok kiracılı uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-120">**Multi-tenant apps others develop, which Contoso can consent to**.</span></span> <span data-ttu-id="8fb9e-121">(Veya kısaca “onaylanan uygulamalar”.) Bu, "çok kiracılı uygulamalar, kuruluşunuzun geliştirdiği uygulamalarla" Merhaba Çevir tarafında bulunur.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-121">(Or “consented apps”, for short.) This is hello flip side of “multi-tenant apps your organization develops”.</span></span> <span data-ttu-id="8fb9e-122">Başka bir kuruluştaki bir çok kiracılı uygulama geliştirir, kullanıcılar, kuruluşunuzun toohello uygulama onay ve tooit oturum açın.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-122">When another organization develops a multi-tenant app, users of your organization can consent toohello app and sign in tooit.</span></span>
    - <span data-ttu-id="8fb9e-123">**Microsoft birinci taraf uygulamaları** - Microsoft hizmetlerini temsil eden uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-123">**Microsoft first-party apps** - Apps that represent Microsoft services.</span></span> <span data-ttu-id="8fb9e-124">Onay hello Hizmeti'ne kaydolma hello olgu tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-124">Consent is driven by hello fact that you sign up for hello service.</span></span> <span data-ttu-id="8fb9e-125">Bazen özel UX ve yoktur belirli birinci taraf uygulamaları için genellikle ilkeleri erişim toohello uygulama etrafında kurarken kullanılan mantığı.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-125">There is sometimes special UX and logic for certain first-party apps that is often used when establishing policies around access toohello app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - <span data-ttu-id="8fb9e-126">**Önceden tümleştirilen uygulamalar** -Apps hello ekleyebileceğiniz Azure AD uygulama galerisinde kullanılabilir tooyour directory tooprovide tek oturum açma (ve sağlama bazı durumlarda) toopopular SaaS uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-126">**Pre-integrated apps** - Apps available in hello Azure AD App Gallery, which you can add tooyour directory tooprovide single sign-on (and in some cases, provisioning) toopopular SaaS apps.</span></span>
    - <span data-ttu-id="8fb9e-127">**Azure AD çoklu oturum açma**: SAML 2.0 veya OpenID Connect gibi desteklenen bir oturum açma protokolü aracılığıyla Azure AD ile tümleştirilebilen “Gerçek” SSO.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-127">**Azure AD single sign-on**: “Real” SSO, for apps that can be integrated with Azure AD, through a supported sign-in protocol such as SAML 2.0 or OpenID Connect.</span></span> <span data-ttu-id="8fb9e-128">Başlangıç Sihirbazı'nı ayarlama işlemleri size yol göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-128">hello wizard walks you through setting it up.</span></span>
    - <span data-ttu-id="8fb9e-129">**Parola çoklu oturum açma**: Azure AD güvenli bir şekilde hello uygulama hello kullanıcının kimlik bilgilerini depolar ve hello kimlik bilgileri "eklenen" oturum açma hello forma hello Azure AD uygulama erişim tarayıcı uzantısı tarafından.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-129">**Password single sign-on**: Azure AD securely stores hello user’s credentials for hello app, and hello credentials are “injected” into hello sign-in form by hello Azure AD App Access browser extension.</span></span> <span data-ttu-id="8fb9e-130">Bu işlem aynı zamanda “parola kasası oluşturma” olarak bilinir.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-130">Also known as “password vaulting”.</span></span>

## <a name="permissions"></a><span data-ttu-id="8fb9e-131">İzinler</span><span class="sxs-lookup"><span data-stu-id="8fb9e-131">Permissions</span></span>

<span data-ttu-id="8fb9e-132">Uygulama kaydedildikten sonra hello uygulama kaydı (diğer bir deyişle, hello Geliştirici) gerçekleştiren hello kullanıcısı hangi izinleri hello uygulamanın erişmesi ve hangi kaynaklara tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-132">When an app is registered, hello user performing hello app registration (that is, hello developer) defines which permissions hello app needs access to, and which resources.</span></span> <span data-ttu-id="8fb9e-133">(Merhaba kaynaklardır, kendilerini diğer uygulamaları olarak tanımlanmış.) Örneğin, birisi posta okuyucu uygulaması oluşturmaya durum, uygulama hello "Posta kutularına erişim hello oturum açmış kullanıcı olarak" hello "Office 365 Exchange Online" kaynak izin gerektirir:</span><span class="sxs-lookup"><span data-stu-id="8fb9e-133">(hello resources are, themselves, defined as other apps.) For example, someone building a mail reader app, would state that their app requires hello “Access mailboxes as hello signed-in user” permission in hello “Office 365 Exchange Online” resource:</span></span>
    
![](media/active-directory-apps-permissions-consent/apps6.png)

<span data-ttu-id="8fb9e-134">Bir uygulama (Merhaba istemci) toorequest başka bir uygulama (Merhaba kaynak) belirli bir izni için sırayla hello geliştiricisine hello kaynak mevcut hello izinleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-134">In order for one app (hello client) toorequest a certain permission from another app (hello resource), hello developer of hello resource app defines hello permissions that exist.</span></span> <span data-ttu-id="8fb9e-135">Bizim örneğimizde, Microsoft, kaynak uygulama "Office 365 Exchange Online" hello, hello sahibi "Posta kutularına erişim hello oturum açmış kullanıcı olarak" adlı bir izin tanımladınız.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-135">In our example, Microsoft, hello owner of hello “Office 365 Exchange Online” resource app, have defined a permission named “Access mailboxes as hello signed-in user”.</span></span>

<span data-ttu-id="8fb9e-136">İzinleri tanımlarken hello uygulama geliştiricisi izin hello izni verdiği veya yönetici onayı gerektirip gerektirmediğini tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-136">When defining permissions, hello app developer must define if hello permission can be consented to, or if it requires admin consent.</span></span> <span data-ttu-id="8fb9e-137">Bu geliştiriciler tooallow kullanıcılar tooconsent yalnızca düşük duyarlılık izinleri isteyen kendi tooapps sağlar, ancak admins tooconsent toomore hassas izinleri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-137">This allows developers tooallow users tooconsent on their own tooapps requesting only low-sensitivity permissions, but require admins tooconsent toomore sensitive permissions.</span></span> <span data-ttu-id="8fb9e-138">Örneğin, "Azure Active Directory" kaynak uygulama Merhaba, sınırlı salt okunur izinleri isteyen tooapps, kullanıcıların kabul şekilde, tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-138">For example, hello “Azure Active Directory” resource app, has been defined, so users can consent tooapps, requesting limited read-only permissions.</span></span>  <span data-ttu-id="8fb9e-139">Ancak, tam okuma izinleri ve tüm yazma izinleri için yönetici onayı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-139">However, admin consent is required for full read permissions, and all write permissions.</span></span>

<span data-ttu-id="8fb9e-140">Yerel istemcilerin kimliği doğrulanmadığı için, yerel istemci uygulaması olarak tanımlanmış bir uygulama yalnızca temsilci atanmış izinler isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-140">Because native clients are not authenticated, an app defined as a native client app can only request delegated permissions.</span></span> <span data-ttu-id="8fb9e-141">Bu durum, bir belirteç edinilirken her zaman gerçek bir kullanıcının rol alması gerektiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-141">This means that there must always be an actual user involved when obtaining a token.</span></span> <span data-ttu-id="8fb9e-142">Web uygulamaları ve web API’leri (gizli istemciler) için erişim belirteci alınırken mutlaka Azure AD ile kimlik doğrulaması yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-142">Web apps and web APIs (confidential clients), must always authenticate with Azure AD when getting an access token.</span></span> <span data-ttu-id="8fb9e-143">Ayrıca sahip oldukları yalnızca uygulama izinleri isteyen hello olasılığını anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-143">Meaning they also have hello possibility of requesting app-only permissions.</span></span> <span data-ttu-id="8fb9e-144">Örneğin, bir arka uç hizmetine tooauthenticate tooanother arka uç hizmetine gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-144">For example, if one back-end service needs tooauthenticate tooanother back-end service.</span></span> <span data-ttu-id="8fb9e-145">Yalnızca uygulama izinleri isteyen uygulamalar her zaman yönetici onayı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-145">Applications requesting app-only permissions always require administrator consent.</span></span>

<span data-ttu-id="8fb9e-146">Özetlemek gerekirse:</span><span class="sxs-lookup"><span data-stu-id="8fb9e-146">Summarizing:</span></span>



- <span data-ttu-id="8fb9e-147">Bir uygulama (istemci), diğer uygulamalar (kaynaklar) için gereken hello izinleri belirtir.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-147">An app (client) states hello permissions it needs for other apps (resources).</span></span>
- <span data-ttu-id="8fb9e-148">Bir uygulama (kaynak) hangi izinlerin gösterilen tooother uygulamaların (istemciler) olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-148">An app (resource) states what permissions are exposed tooother apps (clients).</span></span>
- <span data-ttu-id="8fb9e-149">Bir izin yalnızca uygulama izni ya da temsilci atanmış izin olabilir.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-149">A permission can be an app-only permission, or a delegated permission.</span></span>
- <span data-ttu-id="8fb9e-150">Temsilci atanmış izin, “kullanıcı onayına izin verir” veya “yönetici onayı gerektirir” olarak işaretlenebilir.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-150">A delegated permission can be marked as “allows user consent”, or “requires admin consent”.</span></span>
- <span data-ttu-id="8fb9e-151">Bir uygulamayı bir istemci olarak (izinleri tooa kaynak gerektiğini bildirerek), (Bu sunan hangi izinlerin bildirme tarafından) bir kaynak olarak ya da her ikisini de olarak davranabilir.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-151">An app can behave as a client (by declaring that it needs permissions tooa resource), as a resource (by declaring which permissions it exposes), or as both.</span></span>

## <a name="controls"></a><span data-ttu-id="8fb9e-152">Denetimler</span><span class="sxs-lookup"><span data-stu-id="8fb9e-152">Controls</span></span>

<span data-ttu-id="8fb9e-153">Merhaba, hello farklı yönetici denetimleri bu davranış için kullanılabilir listesi aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-153">hello following is a list of hello different admin controls available for all this behavior.</span></span> <span data-ttu-id="8fb9e-154">hello Yöneticisi denetimleri hello Klasik Portalı'ndan erişilebilen hello dizini altında yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-154">hello admin controls can be accessed in hello classic portal from configure under hello directory.</span></span>

![](media/active-directory-apps-permissions-consent/apps7.png)

<span data-ttu-id="8fb9e-155">Hello Azure'nın altında portal **yönetmek**, **kullanıcı ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-155">In hello Azure portal, under **manage**, **user settings**.</span></span>

![](media/active-directory-apps-permissions-consent/apps11.png)



- <span data-ttu-id="8fb9e-156">Kullanıcıların tooapps onayı olup olmadığını denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8fb9e-156">You can control whether users can consent tooapps:</span></span>

<span data-ttu-id="8fb9e-157">Merhaba Klasik portalında seçin **kullanıcıların kendi verilerini uygulamaları izinleri tooaccess verebileceği.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span><span class="sxs-lookup"><span data-stu-id="8fb9e-157">In hello classic portal, select **Users may give applications permissions tooaccess their data.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span></span>

<span data-ttu-id="8fb9e-158">Hello Azure portal, seçin **kullanıcıların kendi verilerini uygulamaları tooaccess izin verebilir**.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-158">In hello Azure portal, select **users can allow apps tooaccess their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps12.png)



- <span data-ttu-id="8fb9e-159">Kullanıcılar kendi tek Kiracı İş KOLU uygulamaları kaydolabilir olup olmadığını denetleyebilirsiniz: hello Klasik portal seçin **kullanıcıları tümleşik uygulamalar eklemek.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span><span class="sxs-lookup"><span data-stu-id="8fb9e-159">You can control whether users can register their own single-tenant LOB apps: In hello classic portal select **Users may add integrated applications.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span></span>

<span data-ttu-id="8fb9e-160">Hello Azure portal, seçin **kullanıcıların kendi verilerini uygulamaları tooaccess izin verebilir**.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-160">In hello Azure portal, select **users can allow apps tooaccess their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
><span data-ttu-id="8fb9e-161">Tooregister tek Kiracı İş KOLU uygulamaları kullanıcıların olsa bile toowhat kaydedilebilir sınırları vardır.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-161">Even if you do allow users tooregister single-tenant LOB apps, there are limits toowhat can be registered.</span></span>  
><span data-ttu-id="8fb9e-162">Örneğin, dizin yöneticisi olmayan geliştiriciler.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-162">For example, developers who are not directory admins.</span></span>
>
>- <span data-ttu-id="8fb9e-163">Kullanıcılar tek kiracılı bir uygulamayı çok kiracılı uygulama yapamaz.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-163">Users cannot make a single-tenant app a multi-tenant app.</span></span>
>- <span data-ttu-id="8fb9e-164">Tek Kiracı İş KOLU uygulamaları kaydederken, kullanıcılar yalnızca uygulama izinleri tooother uygulamaları isteğinde bulunamaz.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-164">When registering single-tenant LOB apps, users cannot request app-only permissions tooother apps.</span></span>
>- <span data-ttu-id="8fb9e-165">Bu izinleri yönetici onayı gerektiriyorsa tek Kiracı İş KOLU uygulamaları kaydederken izinlere temsilci tooother uygulamaları isteğinde bulunamaz.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-165">When registering single-tenant LOB apps, users cannot request delegated permissions tooother apps if those permissions require admin consent.</span></span>
>- <span data-ttu-id="8fb9e-166">Kullanıcıların sahipleri olmadıkları değişiklikleri tooapps yapamazsınız.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-166">Users cannot make changes tooapps that they are not owners of.</span></span>



- <span data-ttu-id="8fb9e-167">Kullanıcıların parola SSO (diğer adıyla “parola kasası oluşturma”) kullanan önceden tümleştirilmiş uygulamalar ekleyip ekleyemeyeceğini denetleyebilirsiniz ![](media/active-directory-apps-permissions-consent/apps10.png)</span><span class="sxs-lookup"><span data-stu-id="8fb9e-167">You can control whether users can themselves add pre-integrated apps that use password SSO (aka “password vaulting”) ![](media/active-directory-apps-permissions-consent/apps10.png)</span></span>



- <span data-ttu-id="8fb9e-168">Uygulamalara hangi koşullar altında erişilebileceğini denetleyebilirsiniz (koşullu erişim).</span><span class="sxs-lookup"><span data-stu-id="8fb9e-168">You can control under which conditions applications can be accessed (that is, conditional access).</span></span> <span data-ttu-id="8fb9e-169">Bu hem toohello istemci uygulaması hem de toohello kaynak uygulama geçerlidir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-169">Be aware this applies both toohello client app and toohello resource app.</span></span> <span data-ttu-id="8fb9e-170">Bu nedenle, bu hello "Office 365 Exchange Online" uygulama yalnızca uyumlu makinelerden erişilebilir bildiren bir koşullu erişim ilkesi ayarlayabilirsiniz söyleyin.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-170">So, say you set a conditional access policy that says that hello “Office 365 Exchange Online” app can only be accessed from machines, which are compliant.</span></span>  <span data-ttu-id="8fb9e-171">Bir kullanıcı toouse çevrimiçi izinleri tooExchange ister bir istemci uygulaması çalıştığında bu ilkeyi de ilkenin etkisini gösterip.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-171">This policy will also kick in when a user attempts toouse a client app which requests permissions tooExchange Online.</span></span>



- <span data-ttu-id="8fb9e-172">İçine razı tooand hangilerinin kullanılmakta olan uygulamaları silinmiş görünürlüğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-172">You have visibility into which apps have been consented tooand which ones are being used.</span></span>

1.  <span data-ttu-id="8fb9e-173">Bir kullanıcı tooan uygulama izin ServicePrincipal nesne hello Kiracı içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-173">When a user consents tooan app, a ServicePrincipal object is created in hello tenant.</span></span> <span data-ttu-id="8fb9e-174">ServicePrincipal oluşturma hello denetim raporuna dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-174">ServicePrincipal creation is included in hello audit report.</span></span>
2.  <span data-ttu-id="8fb9e-175">Kullanıcı oturum açma etkinliği raporları için hangi uygulama hello kullanıcı oturum söyleyin.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-175">User sign-in activity reports tell you which app hello user is signing in to.</span></span> 

## <a name="example"></a><span data-ttu-id="8fb9e-176">Örnek</span><span class="sxs-lookup"><span data-stu-id="8fb9e-176">Example</span></span>

<span data-ttu-id="8fb9e-177">Örnek olarak, Kiracı kullanıcılar için oturum açtığınız fark hello "FabrikamMail Office 365 için" uygulama atalım.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-177">As an example, let’s take hello “FabrikamMail for Office 365” app, which you’ve noticed users in your tenant are signing in to.</span></span> <span data-ttu-id="8fb9e-178">“FabrikamMail”, “Fabrikam, Inc.” tarafından yayımlanan Android’e yönelik bir posta okuma uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-178">“FabrikamMail” is a mail reader app for Android, published by “Fabrikam, Inc.”.</span></span> <span data-ttu-id="8fb9e-179">Bu hello döner "çok kiracılı uygulamalara Contoso onayı diğer geliştirme".</span><span class="sxs-lookup"><span data-stu-id="8fb9e-179">This falls into hello “multi-tenant apps other develop, which Contoso can consent to”.</span></span>

<span data-ttu-id="8fb9e-180">Kullanıcıların tooconsent izin verilirse, ilk kez oturum onay istemi hello alın:![](media/active-directory-apps-permissions-consent/apps14.png)</span><span class="sxs-lookup"><span data-stu-id="8fb9e-180">If users are allowed tooconsent, they get a consent prompt hello first time they sign in: ![](media/active-directory-apps-permissions-consent/apps14.png)</span></span>

<span data-ttu-id="8fb9e-181">", Posta kutularına erişebilmeleri" Merhaba kullanıcı dönük izin dizesi "Office 365 Exchange Online tarafından" (diğer bir deyişle, Exchange) kullanıma sunulan hello "Posta kutularına erişim hello oturum açmış kullanıcı olarak" izni olur.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-181">“Access your mailboxes” is hello user-facing consent string for hello “Access mailboxes as hello signed-in user” permission exposed by “Office 365 Exchange Online” (that is, Exchange).</span></span>

<span data-ttu-id="8fb9e-182">Office 365 için kaydolurken hangi eklendi Exchange (Merhaba kaynak) hello ServicePrincipal nesnesi arayarak hello izinleri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-182">You can see hello permissions by looking up hello ServicePrincipal object for Exchange (hello resource), which was added when you signed up for Office 365.</span></span> <span data-ttu-id="8fb9e-183">Farklı seçenekler ve yapılandırmaları kaydetmek için kullanılan kiracınızda bulunan hello ServicePrincipal nesnesinin örneği"" Merhaba uygulama düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-183">You can think of hello ServicePrincipal object of an “instance” of hello app in your tenant, which is used for recording different options and configurations.</span></span>  <span data-ttu-id="8fb9e-184">Bu hello kullanarak bkz `Get-AzureADServicePrincipal` PowerShell'de.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-184">You can see this by using hello `Get-AzureADServicePrincipal` in PowerShell.</span></span>

    PS C:\> Get-AzureADServicePrincipal -ObjectId 383f7b97-6754-4d3d-9474-3908ebcba1c6 | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : Office 365 Exchange Online
    AppId                     : 00000002-0000-0ff1-ce00-000000000000
    AppOwnerTenantId          : 
    AppRoleAssignmentRequired : False
    AppRoles                  : {...}
    DisplayName               : Microsoft.Exchange
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {...
                                , class OAuth2Permission {
                                  AdminConsentDescription : Allows hello app toohave hello same access toomailboxes as hello signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as hello signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows hello app full access tooyour mailboxes on your behalf.
                                  UserConsentDisplayName  : Access your mailboxes
                                  Value                   : full_access_as_user
                                },
                                ...}
    PasswordCredentials       : {}
    PublisherName             : 
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {00000002-0000-0ff1-ce00-000000000000/outlook.office365.com, 00000002-0000-0ff1-ce00-000000000000/mail.office365.com, 00000002-0000-0ff1-ce00-000000000000/outlook.com, 
                                00000002-0000-0ff1-ce00-000000000000/*.outlook.com...}
    Tags                      : {}

<span data-ttu-id="8fb9e-185">"Kabul et" Merhaba kullanıcı tıkladığında izin başlatılır.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-185">Consent is initiated when hello user clicks “Accept”.</span></span> <span data-ttu-id="8fb9e-186">İlk olarak, "Office 365 için FabrikamMail" için bir ServicePrincipal nesnesi hello Kiracı içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-186">First, a ServicePrincipal object for “FabrikamMail for Office 365” is created in hello tenant.</span></span> <span data-ttu-id="8fb9e-187">Merhaba ServicePrincipal şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="8fb9e-187">hello ServicePrincipal looks something like this:</span></span>

    PS C:\> Get-AzureADServicePrincipal -SearchString "FabrikamMail for Office 365" | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : a8b16333-851d-42e8-acd2-eac155849b37
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : FabrikamMail for Office 365
    AppId                     : aba7c072-2267-4031-8960-e7a2db6e0590
    AppOwnerTenantId          : 4a4076e0-a70f-41c6-b819-6f9c4a86df89
    AppRoleAssignmentRequired : False
    AppRoles                  : {}
    DisplayName               : FabrikamMail for Office 365
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {}
    PasswordCredentials       : {}
    PublisherName             : Fabrikam, Inc.
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {aba7c072-2267-4031-8960-e7a2db6e0590}
    Tags                      : {WindowsAzureActiveDirectoryIntegratedApp}

<span data-ttu-id="8fb9e-188">Onaylıyorsunuz tooan uygulamasını hello aşağıdaki arasında bir Oauth2PermissionGrant bağlantı oluşturur:</span><span class="sxs-lookup"><span data-stu-id="8fb9e-188">Consenting tooan app creates an Oauth2PermissionGrant link between hello following:</span></span>
  
- <span data-ttu-id="8fb9e-189">Merhaba kullanıcı nesnesi</span><span class="sxs-lookup"><span data-stu-id="8fb9e-189">hello user object</span></span>
- <span data-ttu-id="8fb9e-190">Merhaba istemci uygulamaları ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="8fb9e-190">hello client apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="8fb9e-191">Merhaba kaynak uygulamaları ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="8fb9e-191">hello resource apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="8fb9e-192">Merhaba kaynak uygulama izinleri.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-192">permissions in hello resource app.</span></span>  

<span data-ttu-id="8fb9e-193">FabrikamMail Hello durumda onu şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="8fb9e-193">In hello case of FabrikamMail, it looks something like this:</span></span>

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

<span data-ttu-id="8fb9e-194">(**ClientID** FabrikamMail'ın hizmet asıl nesne kimliği (Merhaba, yeni oluşturduğunuz), **Principalıd** hello kullanıcı nesne kimliği (Merhaba kullanıcının) rıza, **ResourceId**Exchange'in hizmet asıl nesne kimliği, kapsam olduğundan izin verdiği Exchange hello izni olan).</span><span class="sxs-lookup"><span data-stu-id="8fb9e-194">(**ClientId** is FabrikamMail’s service principal object ID (hello one that just got created), **PrincipalId** is hello user object ID (of hello user who consented), **ResourceId** is Exchange’s service principal object ID, Scope is hello permission in Exchange that was consented to).</span></span>

<span data-ttu-id="8fb9e-195">Kullanıcıların tooconsent izin verilmiyorsa, bu izni bildiren bir ekran gereklidir görürler.</span><span class="sxs-lookup"><span data-stu-id="8fb9e-195">If users are not allowed tooconsent, they will see a screen that says that permission is required.</span></span>

