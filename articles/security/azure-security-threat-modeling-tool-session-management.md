---
title: "aaaSession Yönetimi - Microsoft tehdit modelleme aracı - Azure | Microsoft Docs"
description: "Azaltıcı Etkenler hello tehdit modelleme Aracı kullanıma sunulan tehditleri"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 915ffae3f775ca6902fcfb93e7e1952ce85612f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-session-management--articles"></a><span data-ttu-id="d52ad-103">Güvenlik çerçevesi: Oturum yönetimi | Makaleler</span><span class="sxs-lookup"><span data-stu-id="d52ad-103">Security Frame: Session Management | Articles</span></span> 
| <span data-ttu-id="d52ad-104">Ürün/hizmet</span><span class="sxs-lookup"><span data-stu-id="d52ad-104">Product/Service</span></span> | <span data-ttu-id="d52ad-105">Makale</span><span class="sxs-lookup"><span data-stu-id="d52ad-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="d52ad-106">**Azure AD**</span><span class="sxs-lookup"><span data-stu-id="d52ad-106">**Azure AD**</span></span>    | <ul><li>[<span data-ttu-id="d52ad-107">Azure AD kullanırken ADAL yöntemleri kullanarak uygulama uygun oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="d52ad-107">Implement proper logout using ADAL methods when using Azure AD</span></span>](#logout-adal)</li></ul> |
| <span data-ttu-id="d52ad-108">IOT cihaz</span><span class="sxs-lookup"><span data-stu-id="d52ad-108">IoT Device</span></span> | <ul><li>[<span data-ttu-id="d52ad-109">Sonlu yaşam süreleri için oluşturulan SaS belirteci kullanın</span><span class="sxs-lookup"><span data-stu-id="d52ad-109">Use finite lifetimes for generated SaS tokens</span></span>](#finite-tokens)</li></ul> |
| <span data-ttu-id="d52ad-110">**Azure belge DB**</span><span class="sxs-lookup"><span data-stu-id="d52ad-110">**Azure Document DB**</span></span> | <ul><li>[<span data-ttu-id="d52ad-111">Minimum belirteci yaşam süreleri için oluşturulan kaynak belirteçleri kullanın</span><span class="sxs-lookup"><span data-stu-id="d52ad-111">Use minimum token lifetimes for generated Resource tokens</span></span>](#resource-tokens)</li></ul> |
| <span data-ttu-id="d52ad-112">**ADFS**</span><span class="sxs-lookup"><span data-stu-id="d52ad-112">**ADFS**</span></span> | <ul><li>[<span data-ttu-id="d52ad-113">ADFS kullanırken WsFederation yöntemleri kullanarak uygulama uygun oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="d52ad-113">Implement proper logout using WsFederation methods when using ADFS</span></span>](#wsfederation-logout)</li></ul> |
| <span data-ttu-id="d52ad-114">**Kimlik sunucusu**</span><span class="sxs-lookup"><span data-stu-id="d52ad-114">**Identity Server**</span></span> | <ul><li>[<span data-ttu-id="d52ad-115">Kimlik sunucusu kullanılırken uygulama uygun oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="d52ad-115">Implement proper logout when using Identity Server</span></span>](#proper-logout)</li></ul> |
| <span data-ttu-id="d52ad-116">**Web uygulaması**</span><span class="sxs-lookup"><span data-stu-id="d52ad-116">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="d52ad-117">HTTPS üzerinden kullanılabilir uygulamaları güvenli tanımlama bilgileri kullanmalıdır</span><span class="sxs-lookup"><span data-stu-id="d52ad-117">Applications available over HTTPS must use secure cookies</span></span>](#https-secure-cookies)</li><li>[<span data-ttu-id="d52ad-118">Tüm http tabanlı uygulama http tanımlama bilgisi tanımı için yalnızca belirtmeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="d52ad-118">All http based application should specify http only for cookie definition</span></span>](#cookie-definition)</li><li>[<span data-ttu-id="d52ad-119">ASP.NET web sayfaları siteler arası istek sahteciliği (CSRF) saldırılarını karşı azaltmak</span><span class="sxs-lookup"><span data-stu-id="d52ad-119">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>](#csrf-asp)</li><li>[<span data-ttu-id="d52ad-120">Oturum etkin olmama ömrü için ayarlama</span><span class="sxs-lookup"><span data-stu-id="d52ad-120">Set up session for inactivity lifetime</span></span>](#inactivity-lifetime)</li><li>[<span data-ttu-id="d52ad-121">Uygulama hello uygulamasından uygun oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="d52ad-121">Implement proper logout from hello application</span></span>](#proper-app-logout)</li></ul> |
| <span data-ttu-id="d52ad-122">**Web API**</span><span class="sxs-lookup"><span data-stu-id="d52ad-122">**Web API**</span></span> | <ul><li>[<span data-ttu-id="d52ad-123">ASP.NET Web API siteler arası istek sahteciliği (CSRF) saldırılarını karşı azaltmak</span><span class="sxs-lookup"><span data-stu-id="d52ad-123">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>](#csrf-api)</li></ul> |

## <span data-ttu-id="d52ad-124"><a id="logout-adal"></a>Azure AD kullanırken ADAL yöntemleri kullanarak uygulama uygun oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="d52ad-124"><a id="logout-adal"></a>Implement proper logout using ADAL methods when using Azure AD</span></span>

| <span data-ttu-id="d52ad-125">Başlık</span><span class="sxs-lookup"><span data-stu-id="d52ad-125">Title</span></span>                   | <span data-ttu-id="d52ad-126">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="d52ad-126">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d52ad-127">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="d52ad-127">**Component**</span></span>               | <span data-ttu-id="d52ad-128">Azure AD</span><span class="sxs-lookup"><span data-stu-id="d52ad-128">Azure AD</span></span> | 
| <span data-ttu-id="d52ad-129">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="d52ad-129">**SDL Phase**</span></span>               | <span data-ttu-id="d52ad-130">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d52ad-130">Build</span></span> |  
| <span data-ttu-id="d52ad-131">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="d52ad-131">**Applicable Technologies**</span></span> | <span data-ttu-id="d52ad-132">Genel</span><span class="sxs-lookup"><span data-stu-id="d52ad-132">Generic</span></span> |
| <span data-ttu-id="d52ad-133">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="d52ad-133">**Attributes**</span></span>              | <span data-ttu-id="d52ad-134">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-134">N/A</span></span>  |
| <span data-ttu-id="d52ad-135">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-135">**References**</span></span>              | <span data-ttu-id="d52ad-136">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-136">N/A</span></span>  |
| <span data-ttu-id="d52ad-137">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-137">**Steps**</span></span> | <span data-ttu-id="d52ad-138">Merhaba uygulaması Azure AD tarafından verilen erişim belirtecini kullanır, hello oturum kapatma olay işleyicisi çağırmalıdır</span><span class="sxs-lookup"><span data-stu-id="d52ad-138">If hello application relies on access token issued by Azure AD, hello logout event handler should call</span></span> |

### <a name="example"></a><span data-ttu-id="d52ad-139">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-139">Example</span></span>
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a><span data-ttu-id="d52ad-140">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-140">Example</span></span>
<span data-ttu-id="d52ad-141">Session.Abandon() yöntemini çağırarak, kullanıcının oturumunu destroy.</span><span class="sxs-lookup"><span data-stu-id="d52ad-141">It should also destroy user's session by calling Session.Abandon() method.</span></span> <span data-ttu-id="d52ad-142">Yöntemini aşağıdaki kullanıcı oturum kapatma güvenli uygulamasını gösterir:</span><span class="sxs-lookup"><span data-stu-id="d52ad-142">Following method shows secure implementation of user logout:</span></span>
```C#
    [HttpPost]
        [ValidateAntiForgeryToken]
        public void LogOff()
        {
            string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            AuthenticationContext authContext = new AuthenticationContext(Authority + TenantId, new NaiveSessionCache(userObjectID));
            authContext.TokenCache.Clear();
            Session.Clear();
            Session.Abandon();
            Response.SetCookie(new HttpCookie("ASP.NET_SessionId", string.Empty));
            HttpContext.GetOwinContext().Authentication.SignOut(
                OpenIdConnectAuthenticationDefaults.AuthenticationType,
                CookieAuthenticationDefaults.AuthenticationType);
        } 
```

## <span data-ttu-id="d52ad-143"><a id="finite-tokens"></a>Sonlu yaşam süreleri için oluşturulan SaS belirteci kullanın</span><span class="sxs-lookup"><span data-stu-id="d52ad-143"><a id="finite-tokens"></a>Use finite lifetimes for generated SaS tokens</span></span>

| <span data-ttu-id="d52ad-144">Başlık</span><span class="sxs-lookup"><span data-stu-id="d52ad-144">Title</span></span>                   | <span data-ttu-id="d52ad-145">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="d52ad-145">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d52ad-146">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="d52ad-146">**Component**</span></span>               | <span data-ttu-id="d52ad-147">IOT cihaz</span><span class="sxs-lookup"><span data-stu-id="d52ad-147">IoT Device</span></span> | 
| <span data-ttu-id="d52ad-148">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="d52ad-148">**SDL Phase**</span></span>               | <span data-ttu-id="d52ad-149">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d52ad-149">Build</span></span> |  
| <span data-ttu-id="d52ad-150">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="d52ad-150">**Applicable Technologies**</span></span> | <span data-ttu-id="d52ad-151">Genel</span><span class="sxs-lookup"><span data-stu-id="d52ad-151">Generic</span></span> |
| <span data-ttu-id="d52ad-152">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="d52ad-152">**Attributes**</span></span>              | <span data-ttu-id="d52ad-153">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-153">N/A</span></span>  |
| <span data-ttu-id="d52ad-154">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-154">**References**</span></span>              | <span data-ttu-id="d52ad-155">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-155">N/A</span></span>  |
| <span data-ttu-id="d52ad-156">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-156">**Steps**</span></span> | <span data-ttu-id="d52ad-157">SaS belirteci tooAzure IOT Hub kimlik doğrulaması için oluşturulan sınırlı süre sonu dönemi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d52ad-157">SaS tokens generated for authenticating tooAzure IoT Hub should have a finite expiry period.</span></span> <span data-ttu-id="d52ad-158">Merhaba SaS belirteci yaşam süreleri tooa minimum toolimit hello süreyi hello belirteçleri güvenliğinin ihlal edilmesi durumunda bunlar çalınabilir tutun.</span><span class="sxs-lookup"><span data-stu-id="d52ad-158">Keep hello SaS token lifetimes tooa minimum toolimit hello amount of time they can be replayed in case hello tokens are compromised.</span></span>|

## <span data-ttu-id="d52ad-159"><a id="resource-tokens"></a>Minimum belirteci yaşam süreleri için oluşturulan kaynak belirteçleri kullanın</span><span class="sxs-lookup"><span data-stu-id="d52ad-159"><a id="resource-tokens"></a>Use minimum token lifetimes for generated Resource tokens</span></span>

| <span data-ttu-id="d52ad-160">Başlık</span><span class="sxs-lookup"><span data-stu-id="d52ad-160">Title</span></span>                   | <span data-ttu-id="d52ad-161">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="d52ad-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d52ad-162">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="d52ad-162">**Component**</span></span>               | <span data-ttu-id="d52ad-163">Azure belge DB</span><span class="sxs-lookup"><span data-stu-id="d52ad-163">Azure Document DB</span></span> | 
| <span data-ttu-id="d52ad-164">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="d52ad-164">**SDL Phase**</span></span>               | <span data-ttu-id="d52ad-165">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d52ad-165">Build</span></span> |  
| <span data-ttu-id="d52ad-166">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="d52ad-166">**Applicable Technologies**</span></span> | <span data-ttu-id="d52ad-167">Genel</span><span class="sxs-lookup"><span data-stu-id="d52ad-167">Generic</span></span> |
| <span data-ttu-id="d52ad-168">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="d52ad-168">**Attributes**</span></span>              | <span data-ttu-id="d52ad-169">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-169">N/A</span></span>  |
| <span data-ttu-id="d52ad-170">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-170">**References**</span></span>              | <span data-ttu-id="d52ad-171">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-171">N/A</span></span>  |
| <span data-ttu-id="d52ad-172">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-172">**Steps**</span></span> | <span data-ttu-id="d52ad-173">Kaynak belirteci tooa en düşük değer, Hello timespan azaltın.</span><span class="sxs-lookup"><span data-stu-id="d52ad-173">Reduce hello timespan of resource token tooa minimum value required.</span></span> <span data-ttu-id="d52ad-174">Kaynak belirteçleri 1 saatlik varsayılan geçerli timespan vardır.</span><span class="sxs-lookup"><span data-stu-id="d52ad-174">Resource tokens have a default valid timespan of 1 hour.</span></span>|

## <span data-ttu-id="d52ad-175"><a id="wsfederation-logout"></a>ADFS kullanırken WsFederation yöntemleri kullanarak uygulama uygun oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="d52ad-175"><a id="wsfederation-logout"></a>Implement proper logout using WsFederation methods when using ADFS</span></span>

| <span data-ttu-id="d52ad-176">Başlık</span><span class="sxs-lookup"><span data-stu-id="d52ad-176">Title</span></span>                   | <span data-ttu-id="d52ad-177">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="d52ad-177">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d52ad-178">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="d52ad-178">**Component**</span></span>               | <span data-ttu-id="d52ad-179">ADFS</span><span class="sxs-lookup"><span data-stu-id="d52ad-179">ADFS</span></span> | 
| <span data-ttu-id="d52ad-180">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="d52ad-180">**SDL Phase**</span></span>               | <span data-ttu-id="d52ad-181">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d52ad-181">Build</span></span> |  
| <span data-ttu-id="d52ad-182">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="d52ad-182">**Applicable Technologies**</span></span> | <span data-ttu-id="d52ad-183">Genel</span><span class="sxs-lookup"><span data-stu-id="d52ad-183">Generic</span></span> |
| <span data-ttu-id="d52ad-184">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="d52ad-184">**Attributes**</span></span>              | <span data-ttu-id="d52ad-185">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-185">N/A</span></span>  |
| <span data-ttu-id="d52ad-186">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-186">**References**</span></span>              | <span data-ttu-id="d52ad-187">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-187">N/A</span></span>  |
| <span data-ttu-id="d52ad-188">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-188">**Steps**</span></span> | <span data-ttu-id="d52ad-189">Merhaba uygulaması tarafından ADFS STS belirteç dayalıysa, hello oturum kapatma olay işleyicisi WSFederationAuthenticationModule.FederatedSignOut() yöntemi toolog hello kullanıcı çıkışı çağırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d52ad-189">If hello application relies on STS token issued by ADFS, hello logout event handler should call WSFederationAuthenticationModule.FederatedSignOut() method toolog out hello user.</span></span> <span data-ttu-id="d52ad-190">Ayrıca hello geçerli oturum yok edilmesi ve hello oturum belirteç değeri sıfırlayın ve nullified.</span><span class="sxs-lookup"><span data-stu-id="d52ad-190">Also hello current session should be destroyed, and hello session token value should be reset and nullified.</span></span>|

### <a name="example"></a><span data-ttu-id="d52ad-191">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-191">Example</span></span>
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes hello user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at hello specified security token service (STS) by using hello WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of hello current session and raises hello appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at hello specified security token service (STS) by using hello WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <span data-ttu-id="d52ad-192"><a id="proper-logout"></a>Kimlik sunucusu kullanılırken uygulama uygun oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="d52ad-192"><a id="proper-logout"></a>Implement proper logout when using Identity Server</span></span>

| <span data-ttu-id="d52ad-193">Başlık</span><span class="sxs-lookup"><span data-stu-id="d52ad-193">Title</span></span>                   | <span data-ttu-id="d52ad-194">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="d52ad-194">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d52ad-195">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="d52ad-195">**Component**</span></span>               | <span data-ttu-id="d52ad-196">Kimlik sunucusu</span><span class="sxs-lookup"><span data-stu-id="d52ad-196">Identity Server</span></span> | 
| <span data-ttu-id="d52ad-197">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="d52ad-197">**SDL Phase**</span></span>               | <span data-ttu-id="d52ad-198">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d52ad-198">Build</span></span> |  
| <span data-ttu-id="d52ad-199">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="d52ad-199">**Applicable Technologies**</span></span> | <span data-ttu-id="d52ad-200">Genel</span><span class="sxs-lookup"><span data-stu-id="d52ad-200">Generic</span></span> |
| <span data-ttu-id="d52ad-201">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="d52ad-201">**Attributes**</span></span>              | <span data-ttu-id="d52ad-202">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-202">N/A</span></span>  |
| <span data-ttu-id="d52ad-203">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-203">**References**</span></span>              | [<span data-ttu-id="d52ad-204">IdentityServer3 federe oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="d52ad-204">IdentityServer3-Federated sign out</span></span>](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| <span data-ttu-id="d52ad-205">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-205">**Steps**</span></span> | <span data-ttu-id="d52ad-206">Dış kimlik sağlayıcıları ile Merhaba özelliği toofederate IdentityServer destekler.</span><span class="sxs-lookup"><span data-stu-id="d52ad-206">IdentityServer supports hello ability toofederate with external identity providers.</span></span> <span data-ttu-id="d52ad-207">Bir Yukarı Akış kimlik sağlayıcısı dışında bir kullanıcı oturum açtığında hello kullanıcı oturumu kapattığında hello Protokolü kullanıldığında, bağlı olarak bunun olası tooreceive bir bildirim olabilir. Kullanıcı çıkışı istemcilerine de kaydolabilirsiniz şekilde hello IdentityServer toonotify sağlar. Merhaba başvurular bölümündeki hello uygulama ayrıntılarını Hello belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="d52ad-207">When a user signs out of an upstream identity provider, depending upon hello protocol used, it might be possible tooreceive a notification when hello user signs out. It allows IdentityServer toonotify its clients so they can also sign hello user out. Check hello documentation in hello references section for hello implementation details.</span></span>|

## <span data-ttu-id="d52ad-208"><a id="https-secure-cookies"></a>HTTPS üzerinden kullanılabilir uygulamaları güvenli tanımlama bilgileri kullanmalıdır</span><span class="sxs-lookup"><span data-stu-id="d52ad-208"><a id="https-secure-cookies"></a>Applications available over HTTPS must use secure cookies</span></span>

| <span data-ttu-id="d52ad-209">Başlık</span><span class="sxs-lookup"><span data-stu-id="d52ad-209">Title</span></span>                   | <span data-ttu-id="d52ad-210">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="d52ad-210">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d52ad-211">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="d52ad-211">**Component**</span></span>               | <span data-ttu-id="d52ad-212">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="d52ad-212">Web Application</span></span> | 
| <span data-ttu-id="d52ad-213">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="d52ad-213">**SDL Phase**</span></span>               | <span data-ttu-id="d52ad-214">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d52ad-214">Build</span></span> |  
| <span data-ttu-id="d52ad-215">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="d52ad-215">**Applicable Technologies**</span></span> | <span data-ttu-id="d52ad-216">Genel</span><span class="sxs-lookup"><span data-stu-id="d52ad-216">Generic</span></span> |
| <span data-ttu-id="d52ad-217">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="d52ad-217">**Attributes**</span></span>              | <span data-ttu-id="d52ad-218">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="d52ad-218">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="d52ad-219">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-219">**References**</span></span>              | <span data-ttu-id="d52ad-220">[httpCookies Ögesi (ASP.NET Ayarlar Şeması)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure özelliği](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span><span class="sxs-lookup"><span data-stu-id="d52ad-220">[httpCookies Element (ASP.NET Settings Schema)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure Property](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span></span> |
| <span data-ttu-id="d52ad-221">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-221">**Steps**</span></span> | <span data-ttu-id="d52ad-222">Tanımlama bilgileri, yalnızca erişilebilir toohello etki alanı için bunlar kapsamlı normalde bilgileridir.</span><span class="sxs-lookup"><span data-stu-id="d52ad-222">Cookies are normally only accessible toohello domain for which they were scoped.</span></span> <span data-ttu-id="d52ad-223">Ne yazık ki, HTTPS üzerinden oluşturulan tanımlama bilgilerini HTTP üzerinden erişilebilir olması için "etki alanı" Merhaba tanımını hello Protokolü içermez.</span><span class="sxs-lookup"><span data-stu-id="d52ad-223">Unfortunately, hello definition of "domain" does not include hello protocol so cookies that are created over HTTPS are accessible over HTTP.</span></span> <span data-ttu-id="d52ad-224">tanımlama bilgisi hello toohello tarayıcı yalnızca HTTPS üzerinden kullanılabilir olması Hello "güvenli" özniteliği belirtir.</span><span class="sxs-lookup"><span data-stu-id="d52ad-224">hello "secure" attribute indicates toohello browser that hello cookie should only be made available over HTTPS.</span></span> <span data-ttu-id="d52ad-225">HTTPS üzerinden ayarlamak tüm tanımlama bilgilerini hello kullandığınızdan emin olun **güvenli** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="d52ad-225">Ensure that all cookies set over HTTPS use hello **secure** attribute.</span></span> <span data-ttu-id="d52ad-226">Merhaba gereksinim hello requireSSL özniteliği tootrue ayarlayarak hello web.config dosyasında uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="d52ad-226">hello requirement can be enforced in hello web.config file by setting hello requireSSL attribute tootrue.</span></span> <span data-ttu-id="d52ad-227">Merhaba tercih edilen yaklaşım hello zorunlu kılacak çünkü olan **güvenli** ek kod değişikliklerini özniteliği hello gerek toomake olmadan tüm geçerli ve gelecekteki olan tanımlama bilgileri.</span><span class="sxs-lookup"><span data-stu-id="d52ad-227">It is hello preferred approach because it will enforce hello **secure** attribute for all current and future cookies without hello need toomake any additional code changes.</span></span>|

### <a name="example"></a><span data-ttu-id="d52ad-228">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-228">Example</span></span>
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
<span data-ttu-id="d52ad-229">HTTP kullanılan tooaccess Merhaba uygulaması olsa bile hello ayarı zorunlu kılınır.</span><span class="sxs-lookup"><span data-stu-id="d52ad-229">hello setting is enforced even if HTTP is used tooaccess hello application.</span></span> <span data-ttu-id="d52ad-230">HTTP kullanılıyorsa, uygulama tooaccess Merhaba, hello hello tanımlama bilgilerini hello güvenli özniteliği ve hello tarayıcı ile ayarlandığından Merhaba uygulaması bunları göndermez ayarı sonları geri toohello uygulama.</span><span class="sxs-lookup"><span data-stu-id="d52ad-230">If HTTP is used tooaccess hello application, hello setting breaks hello application because hello cookies are set with hello secure attribute and hello browser will not send them back toohello application.</span></span>

| <span data-ttu-id="d52ad-231">Başlık</span><span class="sxs-lookup"><span data-stu-id="d52ad-231">Title</span></span>                   | <span data-ttu-id="d52ad-232">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="d52ad-232">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d52ad-233">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="d52ad-233">**Component**</span></span>               | <span data-ttu-id="d52ad-234">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="d52ad-234">Web Application</span></span> | 
| <span data-ttu-id="d52ad-235">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="d52ad-235">**SDL Phase**</span></span>               | <span data-ttu-id="d52ad-236">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d52ad-236">Build</span></span> |  
| <span data-ttu-id="d52ad-237">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="d52ad-237">**Applicable Technologies**</span></span> | <span data-ttu-id="d52ad-238">Web Forms, MVC5</span><span class="sxs-lookup"><span data-stu-id="d52ad-238">Web Forms, MVC5</span></span> |
| <span data-ttu-id="d52ad-239">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="d52ad-239">**Attributes**</span></span>              | <span data-ttu-id="d52ad-240">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="d52ad-240">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="d52ad-241">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-241">**References**</span></span>              | <span data-ttu-id="d52ad-242">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-242">N/A</span></span>  |
| <span data-ttu-id="d52ad-243">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-243">**Steps**</span></span> | <span data-ttu-id="d52ad-244">RequireSSL tooTrue ayarı tarafından Hello web uygulamasıdır bağlı olan taraf hello ve hello IDP ADFS sunucusu olduğunda hello FedAuth belirtecin güvenli özniteliği yapılandırılabilir `system.identityModel.services` web.config bölümünü:</span><span class="sxs-lookup"><span data-stu-id="d52ad-244">When hello web application is hello Relying Party, and hello IdP is ADFS server, hello FedAuth token's secure attribute can be configured by setting requireSSL tooTrue in `system.identityModel.services` section of web.config:</span></span>|

### <a name="example"></a><span data-ttu-id="d52ad-245">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-245">Example</span></span>
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <span data-ttu-id="d52ad-246"><a id="cookie-definition"></a>Tüm http tabanlı uygulama http tanımlama bilgisi tanımı için yalnızca belirtmeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="d52ad-246"><a id="cookie-definition"></a>All http based application should specify http only for cookie definition</span></span>

| <span data-ttu-id="d52ad-247">Başlık</span><span class="sxs-lookup"><span data-stu-id="d52ad-247">Title</span></span>                   | <span data-ttu-id="d52ad-248">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="d52ad-248">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d52ad-249">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="d52ad-249">**Component**</span></span>               | <span data-ttu-id="d52ad-250">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="d52ad-250">Web Application</span></span> | 
| <span data-ttu-id="d52ad-251">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="d52ad-251">**SDL Phase**</span></span>               | <span data-ttu-id="d52ad-252">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d52ad-252">Build</span></span> |  
| <span data-ttu-id="d52ad-253">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="d52ad-253">**Applicable Technologies**</span></span> | <span data-ttu-id="d52ad-254">Genel</span><span class="sxs-lookup"><span data-stu-id="d52ad-254">Generic</span></span> |
| <span data-ttu-id="d52ad-255">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="d52ad-255">**Attributes**</span></span>              | <span data-ttu-id="d52ad-256">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-256">N/A</span></span>  |
| <span data-ttu-id="d52ad-257">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-257">**References**</span></span>              | [<span data-ttu-id="d52ad-258">Güvenli tanımlama bilgisi özniteliği</span><span class="sxs-lookup"><span data-stu-id="d52ad-258">Secure Cookie Attribute</span></span>](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| <span data-ttu-id="d52ad-259">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-259">**Steps**</span></span> | <span data-ttu-id="d52ad-260">siteler arası (XSS) saldırısı ile bilgilerin açığa çıkmasına hello riskini toomitigate, yeni bir öznitelik - httpOnly - sunulan toocookies oluştu ve önde gelen tüm tarayıcılar tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="d52ad-260">toomitigate hello risk of information disclosure with a cross-site scripting (XSS) attack, a new attribute - httpOnly - was introduced toocookies and is supported by all major browsers.</span></span> <span data-ttu-id="d52ad-261">bir tanımlama bilgisi komut dosyası aracılığıyla erişilebilir değil Hello özniteliği belirtir.</span><span class="sxs-lookup"><span data-stu-id="d52ad-261">hello attribute specifies that a cookie is not accessible through script.</span></span> <span data-ttu-id="d52ad-262">HttpOnly tanımlama bilgilerini kullanarak bir web uygulaması hello tanımlama bilgisine dahil hassas bilgileri komut dosyası çalınması ve tooan saldırganın Web gönderilen olduğunu hello olasılığını azaltır.</span><span class="sxs-lookup"><span data-stu-id="d52ad-262">By using HttpOnly cookies, a web application reduces hello possibility that sensitive information contained in hello cookie can be stolen via script and sent tooan attacker's website.</span></span> |

### <a name="example"></a><span data-ttu-id="d52ad-263">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-263">Example</span></span>
<span data-ttu-id="d52ad-264">Tanımlama bilgileri kullanan tüm HTTP tabanlı uygulamalar HttpOnly yapılandırma web.config dosyasında aşağıdaki uygulayarak hello tanımlama bilgisi tanımında belirtmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="d52ad-264">All HTTP-based applications that use cookies should specify HttpOnly in hello cookie definition, by implementing following configuration in web.config:</span></span>
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| <span data-ttu-id="d52ad-265">Başlık</span><span class="sxs-lookup"><span data-stu-id="d52ad-265">Title</span></span>                   | <span data-ttu-id="d52ad-266">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="d52ad-266">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d52ad-267">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="d52ad-267">**Component**</span></span>               | <span data-ttu-id="d52ad-268">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="d52ad-268">Web Application</span></span> | 
| <span data-ttu-id="d52ad-269">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="d52ad-269">**SDL Phase**</span></span>               | <span data-ttu-id="d52ad-270">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d52ad-270">Build</span></span> |  
| <span data-ttu-id="d52ad-271">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="d52ad-271">**Applicable Technologies**</span></span> | <span data-ttu-id="d52ad-272">Web formları</span><span class="sxs-lookup"><span data-stu-id="d52ad-272">Web Forms</span></span> |
| <span data-ttu-id="d52ad-273">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="d52ad-273">**Attributes**</span></span>              | <span data-ttu-id="d52ad-274">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-274">N/A</span></span>  |
| <span data-ttu-id="d52ad-275">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-275">**References**</span></span>              | [<span data-ttu-id="d52ad-276">FormsAuthentication.RequireSSL özelliği</span><span class="sxs-lookup"><span data-stu-id="d52ad-276">FormsAuthentication.RequireSSL Property</span></span>](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| <span data-ttu-id="d52ad-277">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-277">**Steps**</span></span> | <span data-ttu-id="d52ad-278">Merhaba RequireSSL özellik değeri, hello yapılandırma öğesinin hello requireSSL özniteliğini kullanarak bir ASP.NET uygulaması için hello yapılandırma dosyasında ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="d52ad-278">hello RequireSSL property value is set in hello configuration file for an ASP.NET application by using hello requireSSL attribute of hello configuration element.</span></span> <span data-ttu-id="d52ad-279">SSL (Güvenli Yuva Katmanı) ayarı hello requireSSL özniteliği tarafından gerekli tooreturn hello form kimlik doğrulaması tanımlama bilgisi toohello sunucusu olup olmadığını, ASP.NET uygulamanız için hello Web.config dosyasında belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d52ad-279">You can specify in hello Web.config file for your ASP.NET application whether SSL (Secure Sockets Layer) is required tooreturn hello forms-authentication cookie toohello server by setting hello requireSSL attribute.</span></span>|

### <a name="example"></a><span data-ttu-id="d52ad-280">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-280">Example</span></span> 
<span data-ttu-id="d52ad-281">Merhaba aşağıdaki kod örneğinde hello requireSSL öznitelik hello Web.config dosyasında ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d52ad-281">hello following code example sets hello requireSSL attribute in hello Web.config file.</span></span>
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| <span data-ttu-id="d52ad-282">Başlık</span><span class="sxs-lookup"><span data-stu-id="d52ad-282">Title</span></span>                   | <span data-ttu-id="d52ad-283">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="d52ad-283">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d52ad-284">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="d52ad-284">**Component**</span></span>               | <span data-ttu-id="d52ad-285">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="d52ad-285">Web Application</span></span> | 
| <span data-ttu-id="d52ad-286">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="d52ad-286">**SDL Phase**</span></span>               | <span data-ttu-id="d52ad-287">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d52ad-287">Build</span></span> |  
| <span data-ttu-id="d52ad-288">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="d52ad-288">**Applicable Technologies**</span></span> | <span data-ttu-id="d52ad-289">MVC5</span><span class="sxs-lookup"><span data-stu-id="d52ad-289">MVC5</span></span> |
| <span data-ttu-id="d52ad-290">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="d52ad-290">**Attributes**</span></span>              | <span data-ttu-id="d52ad-291">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="d52ad-291">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="d52ad-292">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-292">**References**</span></span>              | [<span data-ttu-id="d52ad-293">Windows Identity Foundation (WIF) yapılandırması – Bölüm II</span><span class="sxs-lookup"><span data-stu-id="d52ad-293">Windows Identity Foundation (WIF) Configuration – Part II</span></span>](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| <span data-ttu-id="d52ad-294">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-294">**Steps**</span></span> | <span data-ttu-id="d52ad-295">tooset httpOnly özniteliği FedAuth tanımlama bilgilerinin hideFromCsript öznitelik değeri tooTrue ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d52ad-295">tooset httpOnly attribute for FedAuth cookies, hideFromCsript attribute value should be set tooTrue.</span></span> |

### <a name="example"></a><span data-ttu-id="d52ad-296">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-296">Example</span></span>
<span data-ttu-id="d52ad-297">Aşağıdaki yapılandırma hello doğru yapılandırması gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="d52ad-297">Following configuration shows hello correct configuration:</span></span>
```XML
<federatedAuthentication>
<cookieHandler mode="Custom"
                       hideFromScript="true"
                       name="FedAuth"
                       path="/"
                       requireSsl="true"
                       persistentSessionLifetime="25">
</cookieHandler>
</federatedAuthentication>
```

## <span data-ttu-id="d52ad-298"><a id="csrf-asp"></a>ASP.NET web sayfaları siteler arası istek sahteciliği (CSRF) saldırılarını karşı azaltmak</span><span class="sxs-lookup"><span data-stu-id="d52ad-298"><a id="csrf-asp"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>

| <span data-ttu-id="d52ad-299">Başlık</span><span class="sxs-lookup"><span data-stu-id="d52ad-299">Title</span></span>                   | <span data-ttu-id="d52ad-300">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="d52ad-300">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d52ad-301">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="d52ad-301">**Component**</span></span>               | <span data-ttu-id="d52ad-302">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="d52ad-302">Web Application</span></span> | 
| <span data-ttu-id="d52ad-303">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="d52ad-303">**SDL Phase**</span></span>               | <span data-ttu-id="d52ad-304">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d52ad-304">Build</span></span> |  
| <span data-ttu-id="d52ad-305">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="d52ad-305">**Applicable Technologies**</span></span> | <span data-ttu-id="d52ad-306">Genel</span><span class="sxs-lookup"><span data-stu-id="d52ad-306">Generic</span></span> |
| <span data-ttu-id="d52ad-307">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="d52ad-307">**Attributes**</span></span>              | <span data-ttu-id="d52ad-308">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-308">N/A</span></span>  |
| <span data-ttu-id="d52ad-309">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-309">**References**</span></span>              | <span data-ttu-id="d52ad-310">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-310">N/A</span></span>  |
| <span data-ttu-id="d52ad-311">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-311">**Steps**</span></span> | <span data-ttu-id="d52ad-312">Siteler arası istek sahtekarlığı (CSRF veya XSRF), bir saldırgan, farklı bir kullanıcının bir web sitesi kurulan oturum hello güvenlik bağlamında eylemleri gerçekleştirebilirsiniz saldırı türüdür.</span><span class="sxs-lookup"><span data-stu-id="d52ad-312">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in hello security context of a different user's established session on a web site.</span></span> <span data-ttu-id="d52ad-313">Merhaba hedef toomodify ya da hello hedeflenen web sitesi yalnızca oturum tanımlama bilgileri tooauthenticate alınan isteği dayalıysa içeriği silin.</span><span class="sxs-lookup"><span data-stu-id="d52ad-313">hello goal is toomodify or delete content, if hello targeted web site relies exclusively on session cookies tooauthenticate received request.</span></span> <span data-ttu-id="d52ad-314">Bir saldırgan, üzerinde hello kullanıcı zaten oturum açık bir siteden bir URL bir komut ile farklı bir kullanıcının tarayıcı tooload alarak bu güvenlik açığından yararlanabilir.</span><span class="sxs-lookup"><span data-stu-id="d52ad-314">An attacker could exploit this vulnerability by getting a different user's browser tooload a URL with a command from a vulnerable site on which hello user is already logged in.</span></span> <span data-ttu-id="d52ad-315">Gibi farklı bir web sitesi barındırma tarafından bir kaynak hello savunmasız sunucu veya alınırken hello kullanıcı tooclick bağlantı yükler, bir saldırganın toodo için birçok yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="d52ad-315">There are many ways for an attacker toodo that, such as by hosting a different web site that loads a resource from hello vulnerable server, or getting hello user tooclick a link.</span></span> <span data-ttu-id="d52ad-316">Merhaba sunucu bir ek belirteç toohello istemci gönderir, bu tüm gelecekteki isteklerin belirteçte istemci tooinclude hello ve tüm gelecekteki isteklerin toohello geçerli oturum gibi ile ilgili bir belirteç içerdiğini doğrular gerektirir hello saldırı önlenebilir Merhaba ASP.NET AntiForgeryToken ya da ViewState kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="d52ad-316">hello attack can be prevented if hello server sends an additional token toohello client, requires hello client tooinclude that token in all future requests, and verifies that all future requests include a token that pertains toohello current session, such as by using hello ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="d52ad-317">Başlık</span><span class="sxs-lookup"><span data-stu-id="d52ad-317">Title</span></span>                   | <span data-ttu-id="d52ad-318">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="d52ad-318">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d52ad-319">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="d52ad-319">**Component**</span></span>               | <span data-ttu-id="d52ad-320">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="d52ad-320">Web Application</span></span> | 
| <span data-ttu-id="d52ad-321">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="d52ad-321">**SDL Phase**</span></span>               | <span data-ttu-id="d52ad-322">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d52ad-322">Build</span></span> |  
| <span data-ttu-id="d52ad-323">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="d52ad-323">**Applicable Technologies**</span></span> | <span data-ttu-id="d52ad-324">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="d52ad-324">MVC5, MVC6</span></span> |
| <span data-ttu-id="d52ad-325">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="d52ad-325">**Attributes**</span></span>              | <span data-ttu-id="d52ad-326">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-326">N/A</span></span>  |
| <span data-ttu-id="d52ad-327">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-327">**References**</span></span>              | [<span data-ttu-id="d52ad-328">ASP.NET MVC ve Web sayfaları XSRF/CSRF önleme</span><span class="sxs-lookup"><span data-stu-id="d52ad-328">XSRF/CSRF Prevention in ASP.NET MVC and Web Pages</span></span>](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| <span data-ttu-id="d52ad-329">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-329">**Steps**</span></span> | <span data-ttu-id="d52ad-330">Anti-CSRF ve ASP.NET MVC forms - kullanım hello `AntiForgeryToken` yardımcı yöntemi görünümleri; put bir `Html.AntiForgeryToken()` forma Merhaba, örneğin,</span><span class="sxs-lookup"><span data-stu-id="d52ad-330">Anti-CSRF and ASP.NET MVC forms - Use hello `AntiForgeryToken` helper method on Views; put an `Html.AntiForgeryToken()` into hello form, for example,</span></span>|

### <a name="example"></a><span data-ttu-id="d52ad-331">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-331">Example</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a><span data-ttu-id="d52ad-332">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-332">Example</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="d52ad-333">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-333">Example</span></span>
<span data-ttu-id="d52ad-334">Merhaba aynı zaman, bir tanımlama bilgisi ile aynı hello rastgele gizli değer yukarıda gösterilen olarak değeri hello __RequestVerificationToken olarak adlandırılan Html.AntiForgeryToken() verir hello ziyaretçi.</span><span class="sxs-lookup"><span data-stu-id="d52ad-334">At hello same time, Html.AntiForgeryToken() gives hello visitor a cookie called __RequestVerificationToken, with hello same value as hello random hidden value shown above.</span></span> <span data-ttu-id="d52ad-335">Ardından, toovalidate gelen bir form post hello [ValidateAntiForgeryToken] filtre toohello hedef eylem yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d52ad-335">Next, toovalidate an incoming form post, add hello [ValidateAntiForgeryToken] filter toohello target action method.</span></span> <span data-ttu-id="d52ad-336">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d52ad-336">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="d52ad-337">Denetleyen yetkilendirme Filtresi:</span><span class="sxs-lookup"><span data-stu-id="d52ad-337">Authorization filter that checks that:</span></span>
* <span data-ttu-id="d52ad-338">Merhaba gelen istek __RequestVerificationToken adlı bir tanımlama bilgisi içeriyor</span><span class="sxs-lookup"><span data-stu-id="d52ad-338">hello incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="d52ad-339">Merhaba gelen istek sahip bir `Request.Form` __RequestVerificationToken adlı giriş</span><span class="sxs-lookup"><span data-stu-id="d52ad-339">hello incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="d52ad-340">Bu tanımlama bilgisi ve `Request.Form` varsayılarak tüm değerleri Eşleştir iyi, hello isteği geçtiği normal olarak.</span><span class="sxs-lookup"><span data-stu-id="d52ad-340">These cookie and `Request.Form` values match Assuming all is well, hello request goes through as normal.</span></span> <span data-ttu-id="d52ad-341">Ancak değilse, ardından bir Yetkilendirme hatası iletisi "gerekli sahteciliğe karşı koruma belirteci belirtilmedi veya geçersiz".</span><span class="sxs-lookup"><span data-stu-id="d52ad-341">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span> 

### <a name="example"></a><span data-ttu-id="d52ad-342">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-342">Example</span></span>
<span data-ttu-id="d52ad-343">Anti-CSRF ve AJAX: JSON verilerini, HTML form verilerini bir AJAX İsteği Gönder çünkü hello form simgesi AJAX istekleri için bir sorun olabilir.</span><span class="sxs-lookup"><span data-stu-id="d52ad-343">Anti-CSRF and AJAX: hello form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="d52ad-344">Özel bir HTTP üstbilgisi toosend hello belirteçleri bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="d52ad-344">One solution is toosend hello tokens in a custom HTTP header.</span></span> <span data-ttu-id="d52ad-345">Merhaba aşağıdaki kodu Razor sözdizimi toogenerate hello belirteçleri kullanır ve ardından hello belirteçleri tooan AJAX isteği ekler.</span><span class="sxs-lookup"><span data-stu-id="d52ad-345">hello following code uses Razor syntax toogenerate hello tokens, and then adds hello tokens tooan AJAX request.</span></span> 
```C#
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }

    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="d52ad-346">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-346">Example</span></span>
<span data-ttu-id="d52ad-347">Merhaba isteği işlerken hello belirteçleri hello isteği başlığından ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="d52ad-347">When you process hello request, extract hello tokens from hello request header.</span></span> <span data-ttu-id="d52ad-348">Ardından toovalidate hello belirteçleri hello AntiForgery.Validate yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="d52ad-348">Then call hello AntiForgery.Validate method toovalidate hello tokens.</span></span> <span data-ttu-id="d52ad-349">Merhaba belirteçleri geçerli değilse hello doğrulama yöntemi bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d52ad-349">hello Validate method throws an exception if hello tokens are not valid.</span></span>
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

| <span data-ttu-id="d52ad-350">Başlık</span><span class="sxs-lookup"><span data-stu-id="d52ad-350">Title</span></span>                   | <span data-ttu-id="d52ad-351">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="d52ad-351">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d52ad-352">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="d52ad-352">**Component**</span></span>               | <span data-ttu-id="d52ad-353">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="d52ad-353">Web Application</span></span> | 
| <span data-ttu-id="d52ad-354">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="d52ad-354">**SDL Phase**</span></span>               | <span data-ttu-id="d52ad-355">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d52ad-355">Build</span></span> |  
| <span data-ttu-id="d52ad-356">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="d52ad-356">**Applicable Technologies**</span></span> | <span data-ttu-id="d52ad-357">Web formları</span><span class="sxs-lookup"><span data-stu-id="d52ad-357">Web Forms</span></span> |
| <span data-ttu-id="d52ad-358">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="d52ad-358">**Attributes**</span></span>              | <span data-ttu-id="d52ad-359">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-359">N/A</span></span>  |
| <span data-ttu-id="d52ad-360">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-360">**References**</span></span>              | [<span data-ttu-id="d52ad-361">Take avantajı, ASP.NET yerleşik özellikleri tooFend Kapalı Web saldırıları</span><span class="sxs-lookup"><span data-stu-id="d52ad-361">Take Advantage of ASP.NET Built-in Features tooFend Off Web Attacks</span></span>](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| <span data-ttu-id="d52ad-362">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-362">**Steps**</span></span> | <span data-ttu-id="d52ad-363">Her kullanıcı - kullanıcı kimliği için değişir ViewStateUserKey tooa rasgele dize ayarlayarak WebForm tabanlı uygulamalarda CSRF saldırıları azaltmak için veya daha iyi henüz, oturum kimliği</span><span class="sxs-lookup"><span data-stu-id="d52ad-363">CSRF attacks in WebForm based applications can be mitigated by setting ViewStateUserKey tooa random string that varies for each user - user ID or, better yet, session ID.</span></span> <span data-ttu-id="d52ad-364">Kimliktir öngörülemeyen, oturum zaman aşımına uğradı ve bir kullanıcı başına temelinde değişir olduğundan bir teknik ve sosyal nedeniyle için oturum kimliği daha iyi bir uyum sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="d52ad-364">For a number of technical and social reasons, session ID is a much better fit because a session ID is unpredictable, times out, and varies on a per-user basis.</span></span>|

### <a name="example"></a><span data-ttu-id="d52ad-365">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-365">Example</span></span>
<span data-ttu-id="d52ad-366">Sayfalarınızın tümünü toohave gereksinim hello kod aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="d52ad-366">Here's hello code you need toohave in all of your pages:</span></span>
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <span data-ttu-id="d52ad-367"><a id="inactivity-lifetime"></a>Oturum etkin olmama ömrü için ayarlama</span><span class="sxs-lookup"><span data-stu-id="d52ad-367"><a id="inactivity-lifetime"></a>Set up session for inactivity lifetime</span></span>

| <span data-ttu-id="d52ad-368">Başlık</span><span class="sxs-lookup"><span data-stu-id="d52ad-368">Title</span></span>                   | <span data-ttu-id="d52ad-369">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="d52ad-369">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d52ad-370">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="d52ad-370">**Component**</span></span>               | <span data-ttu-id="d52ad-371">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="d52ad-371">Web Application</span></span> | 
| <span data-ttu-id="d52ad-372">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="d52ad-372">**SDL Phase**</span></span>               | <span data-ttu-id="d52ad-373">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d52ad-373">Build</span></span> |  
| <span data-ttu-id="d52ad-374">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="d52ad-374">**Applicable Technologies**</span></span> | <span data-ttu-id="d52ad-375">Genel</span><span class="sxs-lookup"><span data-stu-id="d52ad-375">Generic</span></span> |
| <span data-ttu-id="d52ad-376">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="d52ad-376">**Attributes**</span></span>              | <span data-ttu-id="d52ad-377">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-377">N/A</span></span>  |
| <span data-ttu-id="d52ad-378">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-378">**References**</span></span>              | <span data-ttu-id="d52ad-379">[HttpSessionState.Timeout özelliği](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="d52ad-379">[HttpSessionState.Timeout Property](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span></span> |
| <span data-ttu-id="d52ad-380">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-380">**Steps**</span></span> | <span data-ttu-id="d52ad-381">Oturum zaman aşımı, kullanıcı herhangi bir eylem bir web sitesinde (web sunucusu tarafından tanımlanan) bir aralık boyunca gerçekleştirmez olduğunda olay hello gerçekleşen temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d52ad-381">Session timeout represents hello event occurring when a user does not perform any action on a web site during a interval (defined by web server).</span></span> <span data-ttu-id="d52ad-382">Sunucu tarafında olay Merhaba, hello kullanıcı oturumu too'invalid hello durumunu değiştir ' (örneğin "artık kullanılmıyor") ve (içine bulunan tüm verileri silme) hello web sunucusu toodestroy talimatını.</span><span class="sxs-lookup"><span data-stu-id="d52ad-382">hello event, on server side, change hello status of hello user session too'invalid' (for example  "not used anymore") and instruct hello web server toodestroy it (deleting all data contained into it).</span></span> <span data-ttu-id="d52ad-383">Merhaba aşağıdaki kod örneğinde hello zaman aşımı oturum özniteliği too15 dakika hello Web.config dosyasında ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d52ad-383">hello following code example sets hello timeout session attribute too15 minutes in hello Web.config file.</span></span>|

### <a name="example"></a><span data-ttu-id="d52ad-384">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-384">Example</span></span>
<span data-ttu-id="d52ad-385">'''XML kodunu <configuration> < system.web > <sessionState mode="InProc" cookieless="true" timeout="15" /> < /system.web ></configuration></span><span class="sxs-lookup"><span data-stu-id="d52ad-385">``\`XML code <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span></span>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| <span data-ttu-id="d52ad-386">Başlık</span><span class="sxs-lookup"><span data-stu-id="d52ad-386">Title</span></span>                   | <span data-ttu-id="d52ad-387">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="d52ad-387">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d52ad-388">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="d52ad-388">**Component**</span></span>               | <span data-ttu-id="d52ad-389">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="d52ad-389">Web Application</span></span> | 
| <span data-ttu-id="d52ad-390">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="d52ad-390">**SDL Phase**</span></span>               | <span data-ttu-id="d52ad-391">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d52ad-391">Build</span></span> |  
| <span data-ttu-id="d52ad-392">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="d52ad-392">**Applicable Technologies**</span></span> | <span data-ttu-id="d52ad-393">Web formları</span><span class="sxs-lookup"><span data-stu-id="d52ad-393">Web Forms</span></span> |
| <span data-ttu-id="d52ad-394">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="d52ad-394">**Attributes**</span></span>              | <span data-ttu-id="d52ad-395">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-395">N/A</span></span>  |
| <span data-ttu-id="d52ad-396">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-396">**References**</span></span>              | <span data-ttu-id="d52ad-397">[Öğe forms kimlik doğrulaması için (ASP.NET Ayarlar Şeması)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="d52ad-397">[forms Element for authentication (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span></span> |
| <span data-ttu-id="d52ad-398">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-398">**Steps**</span></span> | <span data-ttu-id="d52ad-399">Merhaba Forms kimlik doğrulaması bileti tanımlama bilgisi zaman aşımı too15 dakika ayarlayın</span><span class="sxs-lookup"><span data-stu-id="d52ad-399">Set hello Forms Authentication Ticket cookie timeout too15 minutes</span></span>|

### <a name="example"></a><span data-ttu-id="d52ad-400">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-400">Example</span></span>
<span data-ttu-id="d52ad-401">'''XML kodu<forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span><span class="sxs-lookup"><span data-stu-id="d52ad-401">``\`XML code <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span></span>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When hello web application is Relying Party and ADFS is hello STS, hello lifetime of hello authentication cookies - FedAuth tokens - can be set by hello following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use hello code below tooenable encryption-decryption of claims received from ADFS. Thumbprint value varies based on hello certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a><span data-ttu-id="d52ad-402">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-402">Example</span></span>
<span data-ttu-id="d52ad-403">Ayrıca hello ADFS sunucusunda powershell komutunu aşağıdaki hello yürüterek bir SAML talep belirtecinin ömrü verilen ADFS too15 ayarlanmalıdır hello dakika:</span><span class="sxs-lookup"><span data-stu-id="d52ad-403">Also hello ADFS issued SAML claim token's lifetime should be set too15 minutes, by executing hello following powershell command on hello ADFS server:</span></span>
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <span data-ttu-id="d52ad-404"><a id="proper-app-logout"></a>Uygulama hello uygulamasından uygun oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="d52ad-404"><a id="proper-app-logout"></a>Implement proper logout from hello application</span></span>

| <span data-ttu-id="d52ad-405">Başlık</span><span class="sxs-lookup"><span data-stu-id="d52ad-405">Title</span></span>                   | <span data-ttu-id="d52ad-406">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="d52ad-406">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d52ad-407">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="d52ad-407">**Component**</span></span>               | <span data-ttu-id="d52ad-408">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="d52ad-408">Web Application</span></span> | 
| <span data-ttu-id="d52ad-409">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="d52ad-409">**SDL Phase**</span></span>               | <span data-ttu-id="d52ad-410">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d52ad-410">Build</span></span> |  
| <span data-ttu-id="d52ad-411">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="d52ad-411">**Applicable Technologies**</span></span> | <span data-ttu-id="d52ad-412">Genel</span><span class="sxs-lookup"><span data-stu-id="d52ad-412">Generic</span></span> |
| <span data-ttu-id="d52ad-413">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="d52ad-413">**Attributes**</span></span>              | <span data-ttu-id="d52ad-414">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-414">N/A</span></span>  |
| <span data-ttu-id="d52ad-415">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-415">**References**</span></span>              | <span data-ttu-id="d52ad-416">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-416">N/A</span></span>  |
| <span data-ttu-id="d52ad-417">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-417">**Steps**</span></span> | <span data-ttu-id="d52ad-418">Doğru oturum kapatma düğmesi kullanıcı basarsa oturum açtığınızda hello uygulamadan gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="d52ad-418">Perform proper Sign Out from hello application, when user presses log out button.</span></span> <span data-ttu-id="d52ad-419">Oturum kapatma sırasında uygulama kullanıcının oturumunu destroy de sıfırlama ve sıfırlama ve kimlik doğrulama tanımlama bilgisi değeri nullifying yanı sıra oturum tanımlama bilgisi değerini iptal edilmez.</span><span class="sxs-lookup"><span data-stu-id="d52ad-419">Upon logout, application should destroy user's session, and also reset and nullify session cookie value, along with resetting and nullifying authentication cookie value.</span></span> <span data-ttu-id="d52ad-420">Birden çok oturumu bağlı tooa tek kullanıcı kimliği olduğunda, ayrıca, bunlar topluca hello sunucu tarafındaki zaman aşımı veya oturum kapatma ile bitmelidir.</span><span class="sxs-lookup"><span data-stu-id="d52ad-420">Also, when multiple sessions are tied tooa single user identity, they must be collectively terminated on hello server side at timeout or logout.</span></span> <span data-ttu-id="d52ad-421">Son olarak, her sayfada oturum kapatma işlevselliği kullanılabilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d52ad-421">Lastly, ensure that Logout functionality is available on every page.</span></span> |

## <span data-ttu-id="d52ad-422"><a id="csrf-api"></a>ASP.NET Web API siteler arası istek sahteciliği (CSRF) saldırılarını karşı azaltmak</span><span class="sxs-lookup"><span data-stu-id="d52ad-422"><a id="csrf-api"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>

| <span data-ttu-id="d52ad-423">Başlık</span><span class="sxs-lookup"><span data-stu-id="d52ad-423">Title</span></span>                   | <span data-ttu-id="d52ad-424">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="d52ad-424">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d52ad-425">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="d52ad-425">**Component**</span></span>               | <span data-ttu-id="d52ad-426">Web API</span><span class="sxs-lookup"><span data-stu-id="d52ad-426">Web API</span></span> | 
| <span data-ttu-id="d52ad-427">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="d52ad-427">**SDL Phase**</span></span>               | <span data-ttu-id="d52ad-428">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d52ad-428">Build</span></span> |  
| <span data-ttu-id="d52ad-429">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="d52ad-429">**Applicable Technologies**</span></span> | <span data-ttu-id="d52ad-430">Genel</span><span class="sxs-lookup"><span data-stu-id="d52ad-430">Generic</span></span> |
| <span data-ttu-id="d52ad-431">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="d52ad-431">**Attributes**</span></span>              | <span data-ttu-id="d52ad-432">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-432">N/A</span></span>  |
| <span data-ttu-id="d52ad-433">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-433">**References**</span></span>              | <span data-ttu-id="d52ad-434">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-434">N/A</span></span>  |
| <span data-ttu-id="d52ad-435">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-435">**Steps**</span></span> | <span data-ttu-id="d52ad-436">Siteler arası istek sahtekarlığı (CSRF veya XSRF), bir saldırgan, farklı bir kullanıcının bir web sitesi kurulan oturum hello güvenlik bağlamında eylemleri gerçekleştirebilirsiniz saldırı türüdür.</span><span class="sxs-lookup"><span data-stu-id="d52ad-436">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in hello security context of a different user's established session on a web site.</span></span> <span data-ttu-id="d52ad-437">Merhaba hedef toomodify ya da hello hedeflenen web sitesi yalnızca oturum tanımlama bilgileri tooauthenticate alınan isteği dayalıysa içeriği silin.</span><span class="sxs-lookup"><span data-stu-id="d52ad-437">hello goal is toomodify or delete content, if hello targeted web site relies exclusively on session cookies tooauthenticate received request.</span></span> <span data-ttu-id="d52ad-438">Bir saldırgan, üzerinde hello kullanıcı zaten oturum açık bir siteden bir URL bir komut ile farklı bir kullanıcının tarayıcı tooload alarak bu güvenlik açığından yararlanabilir.</span><span class="sxs-lookup"><span data-stu-id="d52ad-438">An attacker could exploit this vulnerability by getting a different user's browser tooload a URL with a command from a vulnerable site on which hello user is already logged in.</span></span> <span data-ttu-id="d52ad-439">Gibi farklı bir web sitesi barındırma tarafından bir kaynak hello savunmasız sunucu veya alınırken hello kullanıcı tooclick bağlantı yükler, bir saldırganın toodo için birçok yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="d52ad-439">There are many ways for an attacker toodo that, such as by hosting a different web site that loads a resource from hello vulnerable server, or getting hello user tooclick a link.</span></span> <span data-ttu-id="d52ad-440">Merhaba sunucu bir ek belirteç toohello istemci gönderir, bu tüm gelecekteki isteklerin belirteçte istemci tooinclude hello ve tüm gelecekteki isteklerin toohello geçerli oturum gibi ile ilgili bir belirteç içerdiğini doğrular gerektirir hello saldırı önlenebilir Merhaba ASP.NET AntiForgeryToken ya da ViewState kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="d52ad-440">hello attack can be prevented if hello server sends an additional token toohello client, requires hello client tooinclude that token in all future requests, and verifies that all future requests include a token that pertains toohello current session, such as by using hello ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="d52ad-441">Başlık</span><span class="sxs-lookup"><span data-stu-id="d52ad-441">Title</span></span>                   | <span data-ttu-id="d52ad-442">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="d52ad-442">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d52ad-443">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="d52ad-443">**Component**</span></span>               | <span data-ttu-id="d52ad-444">Web API</span><span class="sxs-lookup"><span data-stu-id="d52ad-444">Web API</span></span> | 
| <span data-ttu-id="d52ad-445">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="d52ad-445">**SDL Phase**</span></span>               | <span data-ttu-id="d52ad-446">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d52ad-446">Build</span></span> |  
| <span data-ttu-id="d52ad-447">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="d52ad-447">**Applicable Technologies**</span></span> | <span data-ttu-id="d52ad-448">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="d52ad-448">MVC5, MVC6</span></span> |
| <span data-ttu-id="d52ad-449">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="d52ad-449">**Attributes**</span></span>              | <span data-ttu-id="d52ad-450">Yok</span><span class="sxs-lookup"><span data-stu-id="d52ad-450">N/A</span></span>  |
| <span data-ttu-id="d52ad-451">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-451">**References**</span></span>              | [<span data-ttu-id="d52ad-452">ASP.NET Web API'de siteler arası istek sahtekarlığı (CSRF) saldırılarını önleme</span><span class="sxs-lookup"><span data-stu-id="d52ad-452">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| <span data-ttu-id="d52ad-453">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-453">**Steps**</span></span> | <span data-ttu-id="d52ad-454">Anti-CSRF ve AJAX: JSON verilerini, HTML form verilerini bir AJAX İsteği Gönder çünkü hello form simgesi AJAX istekleri için bir sorun olabilir.</span><span class="sxs-lookup"><span data-stu-id="d52ad-454">Anti-CSRF and AJAX: hello form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="d52ad-455">Özel bir HTTP üstbilgisi toosend hello belirteçleri bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="d52ad-455">One solution is toosend hello tokens in a custom HTTP header.</span></span> <span data-ttu-id="d52ad-456">Merhaba aşağıdaki kodu Razor sözdizimi toogenerate hello belirteçleri kullanır ve ardından hello belirteçleri tooan AJAX isteği ekler.</span><span class="sxs-lookup"><span data-stu-id="d52ad-456">hello following code uses Razor syntax toogenerate hello tokens, and then adds hello tokens tooan AJAX request.</span></span> |

### <a name="example"></a><span data-ttu-id="d52ad-457">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-457">Example</span></span>
```Javascript
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }
    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="d52ad-458">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-458">Example</span></span>
<span data-ttu-id="d52ad-459">Merhaba isteği işlerken hello belirteçleri hello isteği başlığından ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="d52ad-459">When you process hello request, extract hello tokens from hello request header.</span></span> <span data-ttu-id="d52ad-460">Ardından toovalidate hello belirteçleri hello AntiForgery.Validate yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="d52ad-460">Then call hello AntiForgery.Validate method toovalidate hello tokens.</span></span> <span data-ttu-id="d52ad-461">Merhaba belirteçleri geçerli değilse hello doğrulama yöntemi bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d52ad-461">hello Validate method throws an exception if hello tokens are not valid.</span></span>
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

### <a name="example"></a><span data-ttu-id="d52ad-462">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-462">Example</span></span>
<span data-ttu-id="d52ad-463">Anti-CSRF ve ASP.NET MVC forms - kullanım hello AntiForgeryToken yardımcı yöntemi görünümleri; Örneğin, bir Html.AntiForgeryToken() hello forma koyun,</span><span class="sxs-lookup"><span data-stu-id="d52ad-463">Anti-CSRF and ASP.NET MVC forms - Use hello AntiForgeryToken helper method on Views; put an Html.AntiForgeryToken() into hello form, for example,</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a><span data-ttu-id="d52ad-464">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-464">Example</span></span>
<span data-ttu-id="d52ad-465">Yukarıdaki örnekte Hello hello aşağıdaki gibi bir şey çıkarır:</span><span class="sxs-lookup"><span data-stu-id="d52ad-465">hello example above will output something like hello following:</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="d52ad-466">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-466">Example</span></span>
<span data-ttu-id="d52ad-467">Merhaba aynı zaman, bir tanımlama bilgisi ile aynı hello rastgele gizli değer yukarıda gösterilen olarak değeri hello __RequestVerificationToken olarak adlandırılan Html.AntiForgeryToken() verir hello ziyaretçi.</span><span class="sxs-lookup"><span data-stu-id="d52ad-467">At hello same time, Html.AntiForgeryToken() gives hello visitor a cookie called __RequestVerificationToken, with hello same value as hello random hidden value shown above.</span></span> <span data-ttu-id="d52ad-468">Ardından, toovalidate gelen bir form post hello [ValidateAntiForgeryToken] filtre toohello hedef eylem yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d52ad-468">Next, toovalidate an incoming form post, add hello [ValidateAntiForgeryToken] filter toohello target action method.</span></span> <span data-ttu-id="d52ad-469">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d52ad-469">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="d52ad-470">Denetleyen yetkilendirme Filtresi:</span><span class="sxs-lookup"><span data-stu-id="d52ad-470">Authorization filter that checks that:</span></span>
* <span data-ttu-id="d52ad-471">Merhaba gelen istek __RequestVerificationToken adlı bir tanımlama bilgisi içeriyor</span><span class="sxs-lookup"><span data-stu-id="d52ad-471">hello incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="d52ad-472">Merhaba gelen istek sahip bir `Request.Form` __RequestVerificationToken adlı giriş</span><span class="sxs-lookup"><span data-stu-id="d52ad-472">hello incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="d52ad-473">Bu tanımlama bilgisi ve `Request.Form` varsayılarak tüm değerleri Eşleştir iyi, hello isteği geçtiği normal olarak.</span><span class="sxs-lookup"><span data-stu-id="d52ad-473">These cookie and `Request.Form` values match Assuming all is well, hello request goes through as normal.</span></span> <span data-ttu-id="d52ad-474">Ancak değilse, ardından bir Yetkilendirme hatası iletisi "gerekli sahteciliğe karşı koruma belirteci belirtilmedi veya geçersiz".</span><span class="sxs-lookup"><span data-stu-id="d52ad-474">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span>

| <span data-ttu-id="d52ad-475">Başlık</span><span class="sxs-lookup"><span data-stu-id="d52ad-475">Title</span></span>                   | <span data-ttu-id="d52ad-476">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="d52ad-476">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d52ad-477">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="d52ad-477">**Component**</span></span>               | <span data-ttu-id="d52ad-478">Web API</span><span class="sxs-lookup"><span data-stu-id="d52ad-478">Web API</span></span> | 
| <span data-ttu-id="d52ad-479">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="d52ad-479">**SDL Phase**</span></span>               | <span data-ttu-id="d52ad-480">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d52ad-480">Build</span></span> |  
| <span data-ttu-id="d52ad-481">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="d52ad-481">**Applicable Technologies**</span></span> | <span data-ttu-id="d52ad-482">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="d52ad-482">MVC5, MVC6</span></span> |
| <span data-ttu-id="d52ad-483">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="d52ad-483">**Attributes**</span></span>              | <span data-ttu-id="d52ad-484">Kimlik sağlayıcısı - ADFS, kimlik sağlayıcısı - Azure AD</span><span class="sxs-lookup"><span data-stu-id="d52ad-484">Identity Provider - ADFS, Identity Provider - Azure AD</span></span> |
| <span data-ttu-id="d52ad-485">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-485">**References**</span></span>              | [<span data-ttu-id="d52ad-486">Bireysel hesaplar ve ASP.NET Web API 2.2 yerel oturum açma ile Web API güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="d52ad-486">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2</span></span>](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| <span data-ttu-id="d52ad-487">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="d52ad-487">**Steps**</span></span> | <span data-ttu-id="d52ad-488">OAuth 2.0 kullanarak Hello Web API güvenliği, yalnızca hello belirteci geçerliyse sonra bir taşıyıcı belirteci yetkilendirme isteği üstbilgisi ve verir erişim toohello istekte bekler.</span><span class="sxs-lookup"><span data-stu-id="d52ad-488">If hello Web API is secured using OAuth 2.0, then it expects a bearer token in Authorization request header and grants access toohello request only if hello token is valid.</span></span> <span data-ttu-id="d52ad-489">Tanımlama bilgisi tabanlı kimlik doğrulaması, tarayıcılar hello taşıyıcı belirteçleri toorequests eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="d52ad-489">Unlike cookie based authentication, browsers do not attach hello bearer tokens toorequests.</span></span> <span data-ttu-id="d52ad-490">İstemci tooexplicitly gereken Hello isteyen hello taşıyıcı belirteci hello istek üstbilgisi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d52ad-490">hello requesting client needs tooexplicitly attach hello bearer token in hello request header.</span></span> <span data-ttu-id="d52ad-491">Bu nedenle, OAuth 2.0 kullanan korumalı ASP.NET Web API için taşıyıcı belirteçlerini CSRF saldırılarına karşı savunma hattı olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="d52ad-491">Therefore, for ASP.NET Web APIs protected using OAuth 2.0, bearer tokens are considered as a defense against CSRF attacks.</span></span> <span data-ttu-id="d52ad-492">Merhaba MVC hello uygulama kısmı form kimlik doğrulaması (yani, tanımlama bilgileri kullanır) kullanıyorsa, sahteciliğe karşı koruma belirteçleri hello MVC web uygulaması tarafından kullanılan toobe gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d52ad-492">Please note that if hello MVC portion of hello application uses forms authentication (i.e., uses cookies), anti-forgery tokens have toobe used by hello MVC web app.</span></span> |

### <a name="example"></a><span data-ttu-id="d52ad-493">Örnek</span><span class="sxs-lookup"><span data-stu-id="d52ad-493">Example</span></span>
<span data-ttu-id="d52ad-494">Merhaba Web API sahip toobe haberdar toorely yalnızca taşıyıcı belirteçlerini ve tanımlama bilgileri üzerinde değil.</span><span class="sxs-lookup"><span data-stu-id="d52ad-494">hello Web API has toobe informed toorely ONLY on bearer tokens and not on cookies.</span></span> <span data-ttu-id="d52ad-495">Yapılandırmada aşağıdaki hello tarafından yapılabilir `WebApiConfig.Register` yöntemi: '''C-Sharp kod yapılandırma. SuppressDefaultHostAuthentication(); Config. Filters.Add (yeni HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span><span class="sxs-lookup"><span data-stu-id="d52ad-495">It can be done by hello following configuration in `WebApiConfig.Register` method: ``\`C-Sharp code config.SuppressDefaultHostAuthentication(); config.Filters.Add(new HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span></span>
```
hello SuppressDefaultHostAuthentication method tells Web API tooignore any authentication that happens before hello request reaches hello Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API tooauthenticate only using bearer tokens.
