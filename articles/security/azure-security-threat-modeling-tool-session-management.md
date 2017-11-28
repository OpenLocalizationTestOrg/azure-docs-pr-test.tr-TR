---
title: "Oturum yönetimi - Microsoft tehdit modelleme aracı - Azure | Microsoft Docs"
description: "Azaltıcı Etkenler tehdit modelleme Aracı kullanıma sunulan tehditleri"
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
ms.openlocfilehash: 56471d8ef68eacacb3ecebad5056d7e7a9f3ca40
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="security-frame-session-management--articles"></a><span data-ttu-id="ecf0c-103">Güvenlik çerçevesi: Oturum yönetimi | Makaleler</span><span class="sxs-lookup"><span data-stu-id="ecf0c-103">Security Frame: Session Management | Articles</span></span> 
| <span data-ttu-id="ecf0c-104">Ürün/hizmet</span><span class="sxs-lookup"><span data-stu-id="ecf0c-104">Product/Service</span></span> | <span data-ttu-id="ecf0c-105">Makale</span><span class="sxs-lookup"><span data-stu-id="ecf0c-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="ecf0c-106">**Azure AD**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-106">**Azure AD**</span></span>    | <ul><li>[<span data-ttu-id="ecf0c-107">Azure AD kullanırken ADAL yöntemleri kullanarak uygulama uygun oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-107">Implement proper logout using ADAL methods when using Azure AD</span></span>](#logout-adal)</li></ul> |
| <span data-ttu-id="ecf0c-108">IOT cihaz</span><span class="sxs-lookup"><span data-stu-id="ecf0c-108">IoT Device</span></span> | <ul><li>[<span data-ttu-id="ecf0c-109">Sonlu yaşam süreleri için oluşturulan SaS belirteci kullanın</span><span class="sxs-lookup"><span data-stu-id="ecf0c-109">Use finite lifetimes for generated SaS tokens</span></span>](#finite-tokens)</li></ul> |
| <span data-ttu-id="ecf0c-110">**Azure belge DB**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-110">**Azure Document DB**</span></span> | <ul><li>[<span data-ttu-id="ecf0c-111">Minimum belirteci yaşam süreleri için oluşturulan kaynak belirteçleri kullanın</span><span class="sxs-lookup"><span data-stu-id="ecf0c-111">Use minimum token lifetimes for generated Resource tokens</span></span>](#resource-tokens)</li></ul> |
| <span data-ttu-id="ecf0c-112">**ADFS**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-112">**ADFS**</span></span> | <ul><li>[<span data-ttu-id="ecf0c-113">ADFS kullanırken WsFederation yöntemleri kullanarak uygulama uygun oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-113">Implement proper logout using WsFederation methods when using ADFS</span></span>](#wsfederation-logout)</li></ul> |
| <span data-ttu-id="ecf0c-114">**Kimlik sunucusu**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-114">**Identity Server**</span></span> | <ul><li>[<span data-ttu-id="ecf0c-115">Kimlik sunucusu kullanılırken uygulama uygun oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-115">Implement proper logout when using Identity Server</span></span>](#proper-logout)</li></ul> |
| <span data-ttu-id="ecf0c-116">**Web uygulaması**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-116">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="ecf0c-117">HTTPS üzerinden kullanılabilir uygulamaları güvenli tanımlama bilgileri kullanmalıdır</span><span class="sxs-lookup"><span data-stu-id="ecf0c-117">Applications available over HTTPS must use secure cookies</span></span>](#https-secure-cookies)</li><li>[<span data-ttu-id="ecf0c-118">Tüm http tabanlı uygulama http tanımlama bilgisi tanımı için yalnızca belirtmeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="ecf0c-118">All http based application should specify http only for cookie definition</span></span>](#cookie-definition)</li><li>[<span data-ttu-id="ecf0c-119">ASP.NET web sayfaları siteler arası istek sahteciliği (CSRF) saldırılarını karşı azaltmak</span><span class="sxs-lookup"><span data-stu-id="ecf0c-119">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>](#csrf-asp)</li><li>[<span data-ttu-id="ecf0c-120">Oturum etkin olmama ömrü için ayarlama</span><span class="sxs-lookup"><span data-stu-id="ecf0c-120">Set up session for inactivity lifetime</span></span>](#inactivity-lifetime)</li><li>[<span data-ttu-id="ecf0c-121">Uygulama uygulamadan uygun oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-121">Implement proper logout from the application</span></span>](#proper-app-logout)</li></ul> |
| <span data-ttu-id="ecf0c-122">**Web API**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-122">**Web API**</span></span> | <ul><li>[<span data-ttu-id="ecf0c-123">ASP.NET Web API siteler arası istek sahteciliği (CSRF) saldırılarını karşı azaltmak</span><span class="sxs-lookup"><span data-stu-id="ecf0c-123">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>](#csrf-api)</li></ul> |

## <span data-ttu-id="ecf0c-124"><a id="logout-adal"></a>Azure AD kullanırken ADAL yöntemleri kullanarak uygulama uygun oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-124"><a id="logout-adal"></a>Implement proper logout using ADAL methods when using Azure AD</span></span>

| <span data-ttu-id="ecf0c-125">Başlık</span><span class="sxs-lookup"><span data-stu-id="ecf0c-125">Title</span></span>                   | <span data-ttu-id="ecf0c-126">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="ecf0c-126">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ecf0c-127">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-127">**Component**</span></span>               | <span data-ttu-id="ecf0c-128">Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecf0c-128">Azure AD</span></span> | 
| <span data-ttu-id="ecf0c-129">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-129">**SDL Phase**</span></span>               | <span data-ttu-id="ecf0c-130">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-130">Build</span></span> |  
| <span data-ttu-id="ecf0c-131">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-131">**Applicable Technologies**</span></span> | <span data-ttu-id="ecf0c-132">Genel</span><span class="sxs-lookup"><span data-stu-id="ecf0c-132">Generic</span></span> |
| <span data-ttu-id="ecf0c-133">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-133">**Attributes**</span></span>              | <span data-ttu-id="ecf0c-134">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-134">N/A</span></span>  |
| <span data-ttu-id="ecf0c-135">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-135">**References**</span></span>              | <span data-ttu-id="ecf0c-136">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-136">N/A</span></span>  |
| <span data-ttu-id="ecf0c-137">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-137">**Steps**</span></span> | <span data-ttu-id="ecf0c-138">Uygulama Azure AD tarafından verilen erişim belirtecini kullanır, oturum kapatma olay işleyicisi çağırmalıdır</span><span class="sxs-lookup"><span data-stu-id="ecf0c-138">If the application relies on access token issued by Azure AD, the logout event handler should call</span></span> |

### <a name="example"></a><span data-ttu-id="ecf0c-139">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-139">Example</span></span>
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a><span data-ttu-id="ecf0c-140">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-140">Example</span></span>
<span data-ttu-id="ecf0c-141">Session.Abandon() yöntemini çağırarak, kullanıcının oturumunu destroy.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-141">It should also destroy user's session by calling Session.Abandon() method.</span></span> <span data-ttu-id="ecf0c-142">Yöntemini aşağıdaki kullanıcı oturum kapatma güvenli uygulamasını gösterir:</span><span class="sxs-lookup"><span data-stu-id="ecf0c-142">Following method shows secure implementation of user logout:</span></span>
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

## <span data-ttu-id="ecf0c-143"><a id="finite-tokens"></a>Sonlu yaşam süreleri için oluşturulan SaS belirteci kullanın</span><span class="sxs-lookup"><span data-stu-id="ecf0c-143"><a id="finite-tokens"></a>Use finite lifetimes for generated SaS tokens</span></span>

| <span data-ttu-id="ecf0c-144">Başlık</span><span class="sxs-lookup"><span data-stu-id="ecf0c-144">Title</span></span>                   | <span data-ttu-id="ecf0c-145">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="ecf0c-145">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ecf0c-146">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-146">**Component**</span></span>               | <span data-ttu-id="ecf0c-147">IOT cihaz</span><span class="sxs-lookup"><span data-stu-id="ecf0c-147">IoT Device</span></span> | 
| <span data-ttu-id="ecf0c-148">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-148">**SDL Phase**</span></span>               | <span data-ttu-id="ecf0c-149">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-149">Build</span></span> |  
| <span data-ttu-id="ecf0c-150">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-150">**Applicable Technologies**</span></span> | <span data-ttu-id="ecf0c-151">Genel</span><span class="sxs-lookup"><span data-stu-id="ecf0c-151">Generic</span></span> |
| <span data-ttu-id="ecf0c-152">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-152">**Attributes**</span></span>              | <span data-ttu-id="ecf0c-153">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-153">N/A</span></span>  |
| <span data-ttu-id="ecf0c-154">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-154">**References**</span></span>              | <span data-ttu-id="ecf0c-155">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-155">N/A</span></span>  |
| <span data-ttu-id="ecf0c-156">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-156">**Steps**</span></span> | <span data-ttu-id="ecf0c-157">Azure IOT Hub'ına kimlik doğrulaması için oluşturulan SaS belirteçleri sınırlı süre sonu dönemi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-157">SaS tokens generated for authenticating to Azure IoT Hub should have a finite expiry period.</span></span> <span data-ttu-id="ecf0c-158">SaS belirteci yaşam süreleri belirteçleri güvenliğinin ihlal edilmesi durumunda bunlar çalınabilir süre miktarını sınırlamak için en düşük tutun.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-158">Keep the SaS token lifetimes to a minimum to limit the amount of time they can be replayed in case the tokens are compromised.</span></span>|

## <span data-ttu-id="ecf0c-159"><a id="resource-tokens"></a>Minimum belirteci yaşam süreleri için oluşturulan kaynak belirteçleri kullanın</span><span class="sxs-lookup"><span data-stu-id="ecf0c-159"><a id="resource-tokens"></a>Use minimum token lifetimes for generated Resource tokens</span></span>

| <span data-ttu-id="ecf0c-160">Başlık</span><span class="sxs-lookup"><span data-stu-id="ecf0c-160">Title</span></span>                   | <span data-ttu-id="ecf0c-161">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="ecf0c-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ecf0c-162">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-162">**Component**</span></span>               | <span data-ttu-id="ecf0c-163">Azure belge DB</span><span class="sxs-lookup"><span data-stu-id="ecf0c-163">Azure Document DB</span></span> | 
| <span data-ttu-id="ecf0c-164">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-164">**SDL Phase**</span></span>               | <span data-ttu-id="ecf0c-165">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-165">Build</span></span> |  
| <span data-ttu-id="ecf0c-166">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-166">**Applicable Technologies**</span></span> | <span data-ttu-id="ecf0c-167">Genel</span><span class="sxs-lookup"><span data-stu-id="ecf0c-167">Generic</span></span> |
| <span data-ttu-id="ecf0c-168">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-168">**Attributes**</span></span>              | <span data-ttu-id="ecf0c-169">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-169">N/A</span></span>  |
| <span data-ttu-id="ecf0c-170">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-170">**References**</span></span>              | <span data-ttu-id="ecf0c-171">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-171">N/A</span></span>  |
| <span data-ttu-id="ecf0c-172">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-172">**Steps**</span></span> | <span data-ttu-id="ecf0c-173">Kaynak belirteci timespan gerekli en düşük değer azaltın.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-173">Reduce the timespan of resource token to a minimum value required.</span></span> <span data-ttu-id="ecf0c-174">Kaynak belirteçleri 1 saatlik varsayılan geçerli timespan vardır.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-174">Resource tokens have a default valid timespan of 1 hour.</span></span>|

## <span data-ttu-id="ecf0c-175"><a id="wsfederation-logout"></a>ADFS kullanırken WsFederation yöntemleri kullanarak uygulama uygun oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-175"><a id="wsfederation-logout"></a>Implement proper logout using WsFederation methods when using ADFS</span></span>

| <span data-ttu-id="ecf0c-176">Başlık</span><span class="sxs-lookup"><span data-stu-id="ecf0c-176">Title</span></span>                   | <span data-ttu-id="ecf0c-177">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="ecf0c-177">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ecf0c-178">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-178">**Component**</span></span>               | <span data-ttu-id="ecf0c-179">ADFS</span><span class="sxs-lookup"><span data-stu-id="ecf0c-179">ADFS</span></span> | 
| <span data-ttu-id="ecf0c-180">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-180">**SDL Phase**</span></span>               | <span data-ttu-id="ecf0c-181">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-181">Build</span></span> |  
| <span data-ttu-id="ecf0c-182">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-182">**Applicable Technologies**</span></span> | <span data-ttu-id="ecf0c-183">Genel</span><span class="sxs-lookup"><span data-stu-id="ecf0c-183">Generic</span></span> |
| <span data-ttu-id="ecf0c-184">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-184">**Attributes**</span></span>              | <span data-ttu-id="ecf0c-185">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-185">N/A</span></span>  |
| <span data-ttu-id="ecf0c-186">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-186">**References**</span></span>              | <span data-ttu-id="ecf0c-187">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-187">N/A</span></span>  |
| <span data-ttu-id="ecf0c-188">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-188">**Steps**</span></span> | <span data-ttu-id="ecf0c-189">Uygulama tarafından ADFS STS belirteç dayalıysa, oturum kapatma olay işleyicisi için kullanıcının oturum açması için WSFederationAuthenticationModule.FederatedSignOut() yöntemini çağırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-189">If the application relies on STS token issued by ADFS, the logout event handler should call WSFederationAuthenticationModule.FederatedSignOut() method to log out the user.</span></span> <span data-ttu-id="ecf0c-190">Geçerli oturumu de yok edilmesi ve oturum belirteç değeri sıfırlamak ve nullified.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-190">Also the current session should be destroyed, and the session token value should be reset and nullified.</span></span>|

### <a name="example"></a><span data-ttu-id="ecf0c-191">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-191">Example</span></span>
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes the user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at the specified security token service (STS) by using the WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of the current session and raises the appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at the specified security token service (STS) by using the WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <span data-ttu-id="ecf0c-192"><a id="proper-logout"></a>Kimlik sunucusu kullanılırken uygulama uygun oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-192"><a id="proper-logout"></a>Implement proper logout when using Identity Server</span></span>

| <span data-ttu-id="ecf0c-193">Başlık</span><span class="sxs-lookup"><span data-stu-id="ecf0c-193">Title</span></span>                   | <span data-ttu-id="ecf0c-194">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="ecf0c-194">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ecf0c-195">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-195">**Component**</span></span>               | <span data-ttu-id="ecf0c-196">Kimlik sunucusu</span><span class="sxs-lookup"><span data-stu-id="ecf0c-196">Identity Server</span></span> | 
| <span data-ttu-id="ecf0c-197">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-197">**SDL Phase**</span></span>               | <span data-ttu-id="ecf0c-198">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-198">Build</span></span> |  
| <span data-ttu-id="ecf0c-199">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-199">**Applicable Technologies**</span></span> | <span data-ttu-id="ecf0c-200">Genel</span><span class="sxs-lookup"><span data-stu-id="ecf0c-200">Generic</span></span> |
| <span data-ttu-id="ecf0c-201">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-201">**Attributes**</span></span>              | <span data-ttu-id="ecf0c-202">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-202">N/A</span></span>  |
| <span data-ttu-id="ecf0c-203">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-203">**References**</span></span>              | [<span data-ttu-id="ecf0c-204">IdentityServer3 federe oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-204">IdentityServer3-Federated sign out</span></span>](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| <span data-ttu-id="ecf0c-205">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-205">**Steps**</span></span> | <span data-ttu-id="ecf0c-206">IdentityServer Dış kimlik sağlayıcıları ile birleştirmek özelliğini destekler.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-206">IdentityServer supports the ability to federate with external identity providers.</span></span> <span data-ttu-id="ecf0c-207">Bir Yukarı Akış kimlik sağlayıcısı dışında bir kullanıcı oturum açtığında kullanılan, protokol bağlı olarak kullanıcı oturumu kapattığında bir bildirim almak mümkün olabilir. Bunlar daha da kullanıcı oturumu şekilde istemcilerine bildirmek IdentityServer sağlar. Uygulama ayrıntıları için başvurular bölümdeki belgelere bakın.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-207">When a user signs out of an upstream identity provider, depending upon the protocol used, it might be possible to receive a notification when the user signs out. It allows IdentityServer to notify its clients so they can also sign the user out. Check the documentation in the references section for the implementation details.</span></span>|

## <span data-ttu-id="ecf0c-208"><a id="https-secure-cookies"></a>HTTPS üzerinden kullanılabilir uygulamaları güvenli tanımlama bilgileri kullanmalıdır</span><span class="sxs-lookup"><span data-stu-id="ecf0c-208"><a id="https-secure-cookies"></a>Applications available over HTTPS must use secure cookies</span></span>

| <span data-ttu-id="ecf0c-209">Başlık</span><span class="sxs-lookup"><span data-stu-id="ecf0c-209">Title</span></span>                   | <span data-ttu-id="ecf0c-210">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="ecf0c-210">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ecf0c-211">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-211">**Component**</span></span>               | <span data-ttu-id="ecf0c-212">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="ecf0c-212">Web Application</span></span> | 
| <span data-ttu-id="ecf0c-213">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-213">**SDL Phase**</span></span>               | <span data-ttu-id="ecf0c-214">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-214">Build</span></span> |  
| <span data-ttu-id="ecf0c-215">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-215">**Applicable Technologies**</span></span> | <span data-ttu-id="ecf0c-216">Genel</span><span class="sxs-lookup"><span data-stu-id="ecf0c-216">Generic</span></span> |
| <span data-ttu-id="ecf0c-217">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-217">**Attributes**</span></span>              | <span data-ttu-id="ecf0c-218">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="ecf0c-218">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="ecf0c-219">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-219">**References**</span></span>              | <span data-ttu-id="ecf0c-220">[httpCookies Ögesi (ASP.NET Ayarlar Şeması)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure özelliği](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span><span class="sxs-lookup"><span data-stu-id="ecf0c-220">[httpCookies Element (ASP.NET Settings Schema)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure Property](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span></span> |
| <span data-ttu-id="ecf0c-221">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-221">**Steps**</span></span> | <span data-ttu-id="ecf0c-222">Tanımlama bilgileri normal olarak yalnızca, bunlar kapsamlı etki alanı için erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-222">Cookies are normally only accessible to the domain for which they were scoped.</span></span> <span data-ttu-id="ecf0c-223">Ne yazık ki, HTTPS üzerinden oluşturulan tanımlama bilgilerini HTTP üzerinden erişilebilir olması için "etki alanı" tanımını Protokolü içermez.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-223">Unfortunately, the definition of "domain" does not include the protocol so cookies that are created over HTTPS are accessible over HTTP.</span></span> <span data-ttu-id="ecf0c-224">"Güvenli" özniteliği, tarayıcıda tanımlama bilgisinin yalnızca HTTPS üzerinden kullanılabilir olması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-224">The "secure" attribute indicates to the browser that the cookie should only be made available over HTTPS.</span></span> <span data-ttu-id="ecf0c-225">Tüm tanımlama bilgilerini üzerinden HTTPS kullanımı ayarlandığından emin olun **güvenli** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-225">Ensure that all cookies set over HTTPS use the **secure** attribute.</span></span> <span data-ttu-id="ecf0c-226">Gereksinim requireSSL özniteliği true olarak ayarlayarak web.config dosyasında uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-226">The requirement can be enforced in the web.config file by setting the requireSSL attribute to true.</span></span> <span data-ttu-id="ecf0c-227">Zorunlu kılacak tercih edilen yaklaşım demektir **güvenli** özniteliği için ek kod değişiklikleri yapmak zorunda kalmadan tüm geçerli ve gelecekteki olan tanımlama bilgileri.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-227">It is the preferred approach because it will enforce the **secure** attribute for all current and future cookies without the need to make any additional code changes.</span></span>|

### <a name="example"></a><span data-ttu-id="ecf0c-228">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-228">Example</span></span>
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
<span data-ttu-id="ecf0c-229">HTTP uygulamaya erişmek için kullanılsa bile ayarı zorunlu kılınır.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-229">The setting is enforced even if HTTP is used to access the application.</span></span> <span data-ttu-id="ecf0c-230">Uygulamaya erişmek için HTTP kullandıysanız, çünkü tanımlama bilgileri güvenli özniteliği ile ayarlanır ve tarayıcı bunları geri uygulamaya göndermez ayarı uygulama keser.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-230">If HTTP is used to access the application, the setting breaks the application because the cookies are set with the secure attribute and the browser will not send them back to the application.</span></span>

| <span data-ttu-id="ecf0c-231">Başlık</span><span class="sxs-lookup"><span data-stu-id="ecf0c-231">Title</span></span>                   | <span data-ttu-id="ecf0c-232">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="ecf0c-232">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ecf0c-233">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-233">**Component**</span></span>               | <span data-ttu-id="ecf0c-234">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="ecf0c-234">Web Application</span></span> | 
| <span data-ttu-id="ecf0c-235">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-235">**SDL Phase**</span></span>               | <span data-ttu-id="ecf0c-236">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-236">Build</span></span> |  
| <span data-ttu-id="ecf0c-237">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-237">**Applicable Technologies**</span></span> | <span data-ttu-id="ecf0c-238">Web Forms, MVC5</span><span class="sxs-lookup"><span data-stu-id="ecf0c-238">Web Forms, MVC5</span></span> |
| <span data-ttu-id="ecf0c-239">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-239">**Attributes**</span></span>              | <span data-ttu-id="ecf0c-240">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="ecf0c-240">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="ecf0c-241">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-241">**References**</span></span>              | <span data-ttu-id="ecf0c-242">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-242">N/A</span></span>  |
| <span data-ttu-id="ecf0c-243">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-243">**Steps**</span></span> | <span data-ttu-id="ecf0c-244">Bağlı olan taraf web uygulamasıdır ve IDP ADFS sunucusu olduğunda FedAuth belirtecin güvenli özniteliği requireSSL True olarak ayarlanarak yapılandırılabilir `system.identityModel.services` web.config bölümünü:</span><span class="sxs-lookup"><span data-stu-id="ecf0c-244">When the web application is the Relying Party, and the IdP is ADFS server, the FedAuth token's secure attribute can be configured by setting requireSSL to True in `system.identityModel.services` section of web.config:</span></span>|

### <a name="example"></a><span data-ttu-id="ecf0c-245">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-245">Example</span></span>
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <span data-ttu-id="ecf0c-246"><a id="cookie-definition"></a>Tüm http tabanlı uygulama http tanımlama bilgisi tanımı için yalnızca belirtmeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="ecf0c-246"><a id="cookie-definition"></a>All http based application should specify http only for cookie definition</span></span>

| <span data-ttu-id="ecf0c-247">Başlık</span><span class="sxs-lookup"><span data-stu-id="ecf0c-247">Title</span></span>                   | <span data-ttu-id="ecf0c-248">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="ecf0c-248">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ecf0c-249">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-249">**Component**</span></span>               | <span data-ttu-id="ecf0c-250">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="ecf0c-250">Web Application</span></span> | 
| <span data-ttu-id="ecf0c-251">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-251">**SDL Phase**</span></span>               | <span data-ttu-id="ecf0c-252">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-252">Build</span></span> |  
| <span data-ttu-id="ecf0c-253">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-253">**Applicable Technologies**</span></span> | <span data-ttu-id="ecf0c-254">Genel</span><span class="sxs-lookup"><span data-stu-id="ecf0c-254">Generic</span></span> |
| <span data-ttu-id="ecf0c-255">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-255">**Attributes**</span></span>              | <span data-ttu-id="ecf0c-256">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-256">N/A</span></span>  |
| <span data-ttu-id="ecf0c-257">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-257">**References**</span></span>              | [<span data-ttu-id="ecf0c-258">Güvenli tanımlama bilgisi özniteliği</span><span class="sxs-lookup"><span data-stu-id="ecf0c-258">Secure Cookie Attribute</span></span>](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| <span data-ttu-id="ecf0c-259">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-259">**Steps**</span></span> | <span data-ttu-id="ecf0c-260">Siteler arası (XSS) saldırısı ile bilgi ifşaatı riskini azaltmak için yeni bir öznitelik - httpOnly - tanımlama bilgileri için sunulmuştur ve önde gelen tüm tarayıcılar tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-260">To mitigate the risk of information disclosure with a cross-site scripting (XSS) attack, a new attribute - httpOnly - was introduced to cookies and is supported by all major browsers.</span></span> <span data-ttu-id="ecf0c-261">Öznitelik, bir tanımlama bilgisi komut dosyası aracılığıyla erişilebilir değil belirtir.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-261">The attribute specifies that a cookie is not accessible through script.</span></span> <span data-ttu-id="ecf0c-262">HttpOnly tanımlama bilgilerini kullanarak bir web uygulaması tanımlama bilgisine dahil hassas bilgileri komut dosyası çalınması ve bir saldırganın Web sitesine gönderilen olduğunu olasılığını azaltır.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-262">By using HttpOnly cookies, a web application reduces the possibility that sensitive information contained in the cookie can be stolen via script and sent to an attacker's website.</span></span> |

### <a name="example"></a><span data-ttu-id="ecf0c-263">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-263">Example</span></span>
<span data-ttu-id="ecf0c-264">Tanımlama bilgileri kullanan tüm HTTP tabanlı uygulamalar HttpOnly yapılandırma web.config dosyasında aşağıdaki uygulayarak tanımlama bilgisi tanımında belirtmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="ecf0c-264">All HTTP-based applications that use cookies should specify HttpOnly in the cookie definition, by implementing following configuration in web.config:</span></span>
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| <span data-ttu-id="ecf0c-265">Başlık</span><span class="sxs-lookup"><span data-stu-id="ecf0c-265">Title</span></span>                   | <span data-ttu-id="ecf0c-266">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="ecf0c-266">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ecf0c-267">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-267">**Component**</span></span>               | <span data-ttu-id="ecf0c-268">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="ecf0c-268">Web Application</span></span> | 
| <span data-ttu-id="ecf0c-269">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-269">**SDL Phase**</span></span>               | <span data-ttu-id="ecf0c-270">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-270">Build</span></span> |  
| <span data-ttu-id="ecf0c-271">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-271">**Applicable Technologies**</span></span> | <span data-ttu-id="ecf0c-272">Web formları</span><span class="sxs-lookup"><span data-stu-id="ecf0c-272">Web Forms</span></span> |
| <span data-ttu-id="ecf0c-273">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-273">**Attributes**</span></span>              | <span data-ttu-id="ecf0c-274">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-274">N/A</span></span>  |
| <span data-ttu-id="ecf0c-275">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-275">**References**</span></span>              | [<span data-ttu-id="ecf0c-276">FormsAuthentication.RequireSSL özelliği</span><span class="sxs-lookup"><span data-stu-id="ecf0c-276">FormsAuthentication.RequireSSL Property</span></span>](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| <span data-ttu-id="ecf0c-277">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-277">**Steps**</span></span> | <span data-ttu-id="ecf0c-278">RequireSSL özellik değeri, yapılandırma öğesinin requireSSL özniteliğini kullanarak bir ASP.NET uygulaması için yapılandırma dosyasında ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-278">The RequireSSL property value is set in the configuration file for an ASP.NET application by using the requireSSL attribute of the configuration element.</span></span> <span data-ttu-id="ecf0c-279">ASP.NET uygulamanız için SSL (Güvenli Yuva Katmanı) requireSSL özniteliğini ayarlayarak form kimlik doğrulaması tanımlama bilgisinin sunucuya döndürülmesi gerekip gerekmediğini, Web.config dosyasında belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-279">You can specify in the Web.config file for your ASP.NET application whether SSL (Secure Sockets Layer) is required to return the forms-authentication cookie to the server by setting the requireSSL attribute.</span></span>|

### <a name="example"></a><span data-ttu-id="ecf0c-280">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-280">Example</span></span> 
<span data-ttu-id="ecf0c-281">Aşağıdaki kod örneğinde requireSSL özniteliği Web.config dosyasında ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-281">The following code example sets the requireSSL attribute in the Web.config file.</span></span>
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| <span data-ttu-id="ecf0c-282">Başlık</span><span class="sxs-lookup"><span data-stu-id="ecf0c-282">Title</span></span>                   | <span data-ttu-id="ecf0c-283">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="ecf0c-283">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ecf0c-284">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-284">**Component**</span></span>               | <span data-ttu-id="ecf0c-285">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="ecf0c-285">Web Application</span></span> | 
| <span data-ttu-id="ecf0c-286">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-286">**SDL Phase**</span></span>               | <span data-ttu-id="ecf0c-287">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-287">Build</span></span> |  
| <span data-ttu-id="ecf0c-288">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-288">**Applicable Technologies**</span></span> | <span data-ttu-id="ecf0c-289">MVC5</span><span class="sxs-lookup"><span data-stu-id="ecf0c-289">MVC5</span></span> |
| <span data-ttu-id="ecf0c-290">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-290">**Attributes**</span></span>              | <span data-ttu-id="ecf0c-291">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="ecf0c-291">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="ecf0c-292">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-292">**References**</span></span>              | [<span data-ttu-id="ecf0c-293">Windows Identity Foundation (WIF) yapılandırması – Bölüm II</span><span class="sxs-lookup"><span data-stu-id="ecf0c-293">Windows Identity Foundation (WIF) Configuration – Part II</span></span>](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| <span data-ttu-id="ecf0c-294">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-294">**Steps**</span></span> | <span data-ttu-id="ecf0c-295">FedAuth tanımlama bilgilerini httpOnly özniteliğini ayarlamak için hideFromCsript öznitelik değeri True olarak ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-295">To set httpOnly attribute for FedAuth cookies, hideFromCsript attribute value should be set to True.</span></span> |

### <a name="example"></a><span data-ttu-id="ecf0c-296">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-296">Example</span></span>
<span data-ttu-id="ecf0c-297">Aşağıdaki yapılandırma doğru yapılandırması gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="ecf0c-297">Following configuration shows the correct configuration:</span></span>
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

## <span data-ttu-id="ecf0c-298"><a id="csrf-asp"></a>ASP.NET web sayfaları siteler arası istek sahteciliği (CSRF) saldırılarını karşı azaltmak</span><span class="sxs-lookup"><span data-stu-id="ecf0c-298"><a id="csrf-asp"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>

| <span data-ttu-id="ecf0c-299">Başlık</span><span class="sxs-lookup"><span data-stu-id="ecf0c-299">Title</span></span>                   | <span data-ttu-id="ecf0c-300">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="ecf0c-300">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ecf0c-301">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-301">**Component**</span></span>               | <span data-ttu-id="ecf0c-302">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="ecf0c-302">Web Application</span></span> | 
| <span data-ttu-id="ecf0c-303">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-303">**SDL Phase**</span></span>               | <span data-ttu-id="ecf0c-304">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-304">Build</span></span> |  
| <span data-ttu-id="ecf0c-305">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-305">**Applicable Technologies**</span></span> | <span data-ttu-id="ecf0c-306">Genel</span><span class="sxs-lookup"><span data-stu-id="ecf0c-306">Generic</span></span> |
| <span data-ttu-id="ecf0c-307">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-307">**Attributes**</span></span>              | <span data-ttu-id="ecf0c-308">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-308">N/A</span></span>  |
| <span data-ttu-id="ecf0c-309">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-309">**References**</span></span>              | <span data-ttu-id="ecf0c-310">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-310">N/A</span></span>  |
| <span data-ttu-id="ecf0c-311">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-311">**Steps**</span></span> | <span data-ttu-id="ecf0c-312">Siteler arası istek sahtekarlığı (CSRF veya XSRF), bir saldırganın bir web sitesi kurulan oturum farklı bir kullanıcının güvenlik bağlamında eylemleri gerçekleştirebilirsiniz saldırı türüdür.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-312">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in the security context of a different user's established session on a web site.</span></span> <span data-ttu-id="ecf0c-313">Hedeflenen web sitesi alınan istek kimliğini doğrulamak için özel olarak oturum tanımlama dayalıysa değiştirmek veya içerik silmek için belirtilir.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-313">The goal is to modify or delete content, if the targeted web site relies exclusively on session cookies to authenticate received request.</span></span> <span data-ttu-id="ecf0c-314">Bir saldırgan, üzerinde kullanıcı zaten oturum açık bir siteden bir komutla bir URL yüklemek için farklı bir kullanıcının tarayıcı alarak bu güvenlik açığından yararlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-314">An attacker could exploit this vulnerability by getting a different user's browser to load a URL with a command from a vulnerable site on which the user is already logged in.</span></span> <span data-ttu-id="ecf0c-315">Bir bağlantıyı, gibi bir kaynak savunmasız sunucusundan yükler farklı bir web sitesi barındırma veya kullanıcı alma Bunu yapmak bir saldırganın birçok yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-315">There are many ways for an attacker to do that, such as by hosting a different web site that loads a resource from the vulnerable server, or getting the user to click a link.</span></span> <span data-ttu-id="ecf0c-316">Sunucu istemciye bir ek belirteç, belirtecini de gelecekteki tüm istekler dahil etmek istemcinin gerektiriyorsa ve tüm gelecekteki isteklerin ASP.NET kullanılarak gibi geçerli oturum için ilgili bir belirteç dahil olduğunu doğrular, saldırı önlenebilir AntiForgeryToken veya Görünüm durumu.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-316">The attack can be prevented if the server sends an additional token to the client, requires the client to include that token in all future requests, and verifies that all future requests include a token that pertains to the current session, such as by using the ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="ecf0c-317">Başlık</span><span class="sxs-lookup"><span data-stu-id="ecf0c-317">Title</span></span>                   | <span data-ttu-id="ecf0c-318">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="ecf0c-318">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ecf0c-319">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-319">**Component**</span></span>               | <span data-ttu-id="ecf0c-320">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="ecf0c-320">Web Application</span></span> | 
| <span data-ttu-id="ecf0c-321">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-321">**SDL Phase**</span></span>               | <span data-ttu-id="ecf0c-322">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-322">Build</span></span> |  
| <span data-ttu-id="ecf0c-323">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-323">**Applicable Technologies**</span></span> | <span data-ttu-id="ecf0c-324">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="ecf0c-324">MVC5, MVC6</span></span> |
| <span data-ttu-id="ecf0c-325">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-325">**Attributes**</span></span>              | <span data-ttu-id="ecf0c-326">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-326">N/A</span></span>  |
| <span data-ttu-id="ecf0c-327">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-327">**References**</span></span>              | [<span data-ttu-id="ecf0c-328">ASP.NET MVC ve Web sayfaları XSRF/CSRF önleme</span><span class="sxs-lookup"><span data-stu-id="ecf0c-328">XSRF/CSRF Prevention in ASP.NET MVC and Web Pages</span></span>](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| <span data-ttu-id="ecf0c-329">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-329">**Steps**</span></span> | <span data-ttu-id="ecf0c-330">Anti-CSRF ve ASP.NET MVC formları - kullanma `AntiForgeryToken` yardımcı yöntemi görünümleri; put bir `Html.AntiForgeryToken()` forma, örneğin,</span><span class="sxs-lookup"><span data-stu-id="ecf0c-330">Anti-CSRF and ASP.NET MVC forms - Use the `AntiForgeryToken` helper method on Views; put an `Html.AntiForgeryToken()` into the form, for example,</span></span>|

### <a name="example"></a><span data-ttu-id="ecf0c-331">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-331">Example</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a><span data-ttu-id="ecf0c-332">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-332">Example</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="ecf0c-333">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-333">Example</span></span>
<span data-ttu-id="ecf0c-334">Aynı anda Html.AntiForgeryToken() ziyaretçi yukarıda gösterilen rastgele gizli değer ile aynı değere sahip __RequestVerificationToken adlı bir tanımlama bilgisi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-334">At the same time, Html.AntiForgeryToken() gives the visitor a cookie called __RequestVerificationToken, with the same value as the random hidden value shown above.</span></span> <span data-ttu-id="ecf0c-335">Ardından, gelen bir form post doğrulamak için hedef eylem yöntemine [ValidateAntiForgeryToken] filtresini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-335">Next, to validate an incoming form post, add the [ValidateAntiForgeryToken] filter to the target action method.</span></span> <span data-ttu-id="ecf0c-336">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ecf0c-336">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="ecf0c-337">Denetleyen yetkilendirme Filtresi:</span><span class="sxs-lookup"><span data-stu-id="ecf0c-337">Authorization filter that checks that:</span></span>
* <span data-ttu-id="ecf0c-338">Gelen istek __RequestVerificationToken adlı bir tanımlama bilgisi içeriyor</span><span class="sxs-lookup"><span data-stu-id="ecf0c-338">The incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="ecf0c-339">Gelen istek sahip bir `Request.Form` __RequestVerificationToken adlı giriş</span><span class="sxs-lookup"><span data-stu-id="ecf0c-339">The incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="ecf0c-340">Bu tanımlama bilgisi ve `Request.Form` varsayılarak tüm değerleri Eşleştir iyi, istek geçtiği normal olarak.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-340">These cookie and `Request.Form` values match Assuming all is well, the request goes through as normal.</span></span> <span data-ttu-id="ecf0c-341">Ancak değilse, ardından bir Yetkilendirme hatası iletisi "gerekli sahteciliğe karşı koruma belirteci belirtilmedi veya geçersiz".</span><span class="sxs-lookup"><span data-stu-id="ecf0c-341">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span> 

### <a name="example"></a><span data-ttu-id="ecf0c-342">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-342">Example</span></span>
<span data-ttu-id="ecf0c-343">Anti-CSRF ve AJAX: JSON verilerini, HTML form verilerini bir AJAX İsteği Gönder çünkü form simgesi AJAX istekleri için bir sorun olabilir.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-343">Anti-CSRF and AJAX: The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="ecf0c-344">Bir çözüm, özel bir HTTP üstbilgisi belirteçleri göndermektir.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-344">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="ecf0c-345">Aşağıdaki kod belirteçleri oluşturmak için Razor sözdizimini kullanır ve ardından bir AJAX isteği belirteçleri ekler.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-345">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> 
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

### <a name="example"></a><span data-ttu-id="ecf0c-346">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-346">Example</span></span>
<span data-ttu-id="ecf0c-347">İsteği işlerken, istek üstbilgisi belirteçleri ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-347">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="ecf0c-348">Ardından belirteçleri doğrulamak için AntiForgery.Validate yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-348">Then call the AntiForgery.Validate method to validate the tokens.</span></span> <span data-ttu-id="ecf0c-349">Belirteçleri geçerli değilse doğrulama yöntemi bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-349">The Validate method throws an exception if the tokens are not valid.</span></span>
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

| <span data-ttu-id="ecf0c-350">Başlık</span><span class="sxs-lookup"><span data-stu-id="ecf0c-350">Title</span></span>                   | <span data-ttu-id="ecf0c-351">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="ecf0c-351">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ecf0c-352">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-352">**Component**</span></span>               | <span data-ttu-id="ecf0c-353">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="ecf0c-353">Web Application</span></span> | 
| <span data-ttu-id="ecf0c-354">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-354">**SDL Phase**</span></span>               | <span data-ttu-id="ecf0c-355">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-355">Build</span></span> |  
| <span data-ttu-id="ecf0c-356">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-356">**Applicable Technologies**</span></span> | <span data-ttu-id="ecf0c-357">Web formları</span><span class="sxs-lookup"><span data-stu-id="ecf0c-357">Web Forms</span></span> |
| <span data-ttu-id="ecf0c-358">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-358">**Attributes**</span></span>              | <span data-ttu-id="ecf0c-359">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-359">N/A</span></span>  |
| <span data-ttu-id="ecf0c-360">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-360">**References**</span></span>              | [<span data-ttu-id="ecf0c-361">Web saldırıları Fend için ASP.NET yerleşik özelliklerden yararlanabilir</span><span class="sxs-lookup"><span data-stu-id="ecf0c-361">Take Advantage of ASP.NET Built-in Features to Fend Off Web Attacks</span></span>](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| <span data-ttu-id="ecf0c-362">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-362">**Steps**</span></span> | <span data-ttu-id="ecf0c-363">CSRF saldırılarını WebForm tabanlı uygulamalarda - her kullanıcı için kullanıcı kimliği değişen rastgele bir dize ViewStateUserKey ayarlayarak azaltılabilir veya, henüz, oturum kimliği daha iyi</span><span class="sxs-lookup"><span data-stu-id="ecf0c-363">CSRF attacks in WebForm based applications can be mitigated by setting ViewStateUserKey to a random string that varies for each user - user ID or, better yet, session ID.</span></span> <span data-ttu-id="ecf0c-364">Kimliktir öngörülemeyen, oturum zaman aşımına uğradı ve bir kullanıcı başına temelinde değişir olduğundan bir teknik ve sosyal nedeniyle için oturum kimliği daha iyi bir uyum sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-364">For a number of technical and social reasons, session ID is a much better fit because a session ID is unpredictable, times out, and varies on a per-user basis.</span></span>|

### <a name="example"></a><span data-ttu-id="ecf0c-365">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-365">Example</span></span>
<span data-ttu-id="ecf0c-366">Sayfalarınızın tümünü gerek kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="ecf0c-366">Here's the code you need to have in all of your pages:</span></span>
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <span data-ttu-id="ecf0c-367"><a id="inactivity-lifetime"></a>Oturum etkin olmama ömrü için ayarlama</span><span class="sxs-lookup"><span data-stu-id="ecf0c-367"><a id="inactivity-lifetime"></a>Set up session for inactivity lifetime</span></span>

| <span data-ttu-id="ecf0c-368">Başlık</span><span class="sxs-lookup"><span data-stu-id="ecf0c-368">Title</span></span>                   | <span data-ttu-id="ecf0c-369">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="ecf0c-369">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ecf0c-370">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-370">**Component**</span></span>               | <span data-ttu-id="ecf0c-371">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="ecf0c-371">Web Application</span></span> | 
| <span data-ttu-id="ecf0c-372">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-372">**SDL Phase**</span></span>               | <span data-ttu-id="ecf0c-373">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-373">Build</span></span> |  
| <span data-ttu-id="ecf0c-374">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-374">**Applicable Technologies**</span></span> | <span data-ttu-id="ecf0c-375">Genel</span><span class="sxs-lookup"><span data-stu-id="ecf0c-375">Generic</span></span> |
| <span data-ttu-id="ecf0c-376">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-376">**Attributes**</span></span>              | <span data-ttu-id="ecf0c-377">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-377">N/A</span></span>  |
| <span data-ttu-id="ecf0c-378">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-378">**References**</span></span>              | <span data-ttu-id="ecf0c-379">[HttpSessionState.Timeout özelliği](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="ecf0c-379">[HttpSessionState.Timeout Property](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span></span> |
| <span data-ttu-id="ecf0c-380">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-380">**Steps**</span></span> | <span data-ttu-id="ecf0c-381">Oturum zaman aşımı, kullanıcı herhangi bir eylem bir web sitesinde (web sunucusu tarafından tanımlanan) bir aralık boyunca gerçekleştirmez zaman gerçekleşen olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-381">Session timeout represents the event occurring when a user does not perform any action on a web site during a interval (defined by web server).</span></span> <span data-ttu-id="ecf0c-382">Sunucu tarafında olay (örneğin "artık kullanılmıyor") kullanıcı oturumunun durumu 'için geçersiz' değiştirebilir ve bunu (içine bulunan tüm verileri silme) yok etmek için web sunucusu isteyin.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-382">The event, on server side, change the status of the user session to 'invalid' (for example  "not used anymore") and instruct the web server to destroy it (deleting all data contained into it).</span></span> <span data-ttu-id="ecf0c-383">Aşağıdaki kod örneğinde zaman aşımı oturum özniteliği Web.config dosyasında 15 dakika olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-383">The following code example sets the timeout session attribute to 15 minutes in the Web.config file.</span></span>|

### <a name="example"></a><span data-ttu-id="ecf0c-384">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-384">Example</span></span>
<span data-ttu-id="ecf0c-385">'''XML kodunu <configuration> < system.web > <sessionState mode="InProc" cookieless="true" timeout="15" /> < /system.web ></configuration></span><span class="sxs-lookup"><span data-stu-id="ecf0c-385">``\`XML code <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span></span>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| <span data-ttu-id="ecf0c-386">Başlık</span><span class="sxs-lookup"><span data-stu-id="ecf0c-386">Title</span></span>                   | <span data-ttu-id="ecf0c-387">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="ecf0c-387">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ecf0c-388">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-388">**Component**</span></span>               | <span data-ttu-id="ecf0c-389">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="ecf0c-389">Web Application</span></span> | 
| <span data-ttu-id="ecf0c-390">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-390">**SDL Phase**</span></span>               | <span data-ttu-id="ecf0c-391">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-391">Build</span></span> |  
| <span data-ttu-id="ecf0c-392">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-392">**Applicable Technologies**</span></span> | <span data-ttu-id="ecf0c-393">Web formları</span><span class="sxs-lookup"><span data-stu-id="ecf0c-393">Web Forms</span></span> |
| <span data-ttu-id="ecf0c-394">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-394">**Attributes**</span></span>              | <span data-ttu-id="ecf0c-395">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-395">N/A</span></span>  |
| <span data-ttu-id="ecf0c-396">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-396">**References**</span></span>              | <span data-ttu-id="ecf0c-397">[Öğe forms kimlik doğrulaması için (ASP.NET Ayarlar Şeması)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="ecf0c-397">[forms Element for authentication (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span></span> |
| <span data-ttu-id="ecf0c-398">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-398">**Steps**</span></span> | <span data-ttu-id="ecf0c-399">Forms kimlik doğrulaması bileti tanımlama bilgisi zaman aşımı 15 dakika olarak ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ecf0c-399">Set the Forms Authentication Ticket cookie timeout to 15 minutes</span></span>|

### <a name="example"></a><span data-ttu-id="ecf0c-400">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-400">Example</span></span>
<span data-ttu-id="ecf0c-401">'''XML kodu<forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span><span class="sxs-lookup"><span data-stu-id="ecf0c-401">``\`XML code <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span></span>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When the web application is Relying Party and ADFS is the STS, the lifetime of the authentication cookies - FedAuth tokens - can be set by the following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use the code below to enable encryption-decryption of claims received from ADFS. Thumbprint value varies based on the certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a><span data-ttu-id="ecf0c-402">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-402">Example</span></span>
<span data-ttu-id="ecf0c-403">Ayrıca belirtecin yaşam süresi 15 dakika, ADFS sunucusunda aşağıdaki powershell komutunu yürüterek ayarlamanız gerekir SAML verilen ADFS talep:</span><span class="sxs-lookup"><span data-stu-id="ecf0c-403">Also the ADFS issued SAML claim token's lifetime should be set to 15 minutes, by executing the following powershell command on the ADFS server:</span></span>
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <span data-ttu-id="ecf0c-404"><a id="proper-app-logout"></a>Uygulama uygulamadan uygun oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-404"><a id="proper-app-logout"></a>Implement proper logout from the application</span></span>

| <span data-ttu-id="ecf0c-405">Başlık</span><span class="sxs-lookup"><span data-stu-id="ecf0c-405">Title</span></span>                   | <span data-ttu-id="ecf0c-406">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="ecf0c-406">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ecf0c-407">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-407">**Component**</span></span>               | <span data-ttu-id="ecf0c-408">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="ecf0c-408">Web Application</span></span> | 
| <span data-ttu-id="ecf0c-409">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-409">**SDL Phase**</span></span>               | <span data-ttu-id="ecf0c-410">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-410">Build</span></span> |  
| <span data-ttu-id="ecf0c-411">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-411">**Applicable Technologies**</span></span> | <span data-ttu-id="ecf0c-412">Genel</span><span class="sxs-lookup"><span data-stu-id="ecf0c-412">Generic</span></span> |
| <span data-ttu-id="ecf0c-413">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-413">**Attributes**</span></span>              | <span data-ttu-id="ecf0c-414">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-414">N/A</span></span>  |
| <span data-ttu-id="ecf0c-415">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-415">**References**</span></span>              | <span data-ttu-id="ecf0c-416">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-416">N/A</span></span>  |
| <span data-ttu-id="ecf0c-417">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-417">**Steps**</span></span> | <span data-ttu-id="ecf0c-418">Doğru oturum kapatma düğmesi kullanıcı basarsa oturum açtığınızda uygulamadan gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-418">Perform proper Sign Out from the application, when user presses log out button.</span></span> <span data-ttu-id="ecf0c-419">Oturum kapatma sırasında uygulama kullanıcının oturumunu destroy de sıfırlama ve sıfırlama ve kimlik doğrulama tanımlama bilgisi değeri nullifying yanı sıra oturum tanımlama bilgisi değerini iptal edilmez.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-419">Upon logout, application should destroy user's session, and also reset and nullify session cookie value, along with resetting and nullifying authentication cookie value.</span></span> <span data-ttu-id="ecf0c-420">Birden çok oturumu tek bir kullanıcı kimliğine bağlıdır, ayrıca, bunlar topluca sunucu tarafındaki zaman aşımı veya oturum kapatma ile bitmelidir.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-420">Also, when multiple sessions are tied to a single user identity, they must be collectively terminated on the server side at timeout or logout.</span></span> <span data-ttu-id="ecf0c-421">Son olarak, her sayfada oturum kapatma işlevselliği kullanılabilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-421">Lastly, ensure that Logout functionality is available on every page.</span></span> |

## <span data-ttu-id="ecf0c-422"><a id="csrf-api"></a>ASP.NET Web API siteler arası istek sahteciliği (CSRF) saldırılarını karşı azaltmak</span><span class="sxs-lookup"><span data-stu-id="ecf0c-422"><a id="csrf-api"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>

| <span data-ttu-id="ecf0c-423">Başlık</span><span class="sxs-lookup"><span data-stu-id="ecf0c-423">Title</span></span>                   | <span data-ttu-id="ecf0c-424">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="ecf0c-424">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ecf0c-425">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-425">**Component**</span></span>               | <span data-ttu-id="ecf0c-426">Web API</span><span class="sxs-lookup"><span data-stu-id="ecf0c-426">Web API</span></span> | 
| <span data-ttu-id="ecf0c-427">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-427">**SDL Phase**</span></span>               | <span data-ttu-id="ecf0c-428">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-428">Build</span></span> |  
| <span data-ttu-id="ecf0c-429">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-429">**Applicable Technologies**</span></span> | <span data-ttu-id="ecf0c-430">Genel</span><span class="sxs-lookup"><span data-stu-id="ecf0c-430">Generic</span></span> |
| <span data-ttu-id="ecf0c-431">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-431">**Attributes**</span></span>              | <span data-ttu-id="ecf0c-432">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-432">N/A</span></span>  |
| <span data-ttu-id="ecf0c-433">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-433">**References**</span></span>              | <span data-ttu-id="ecf0c-434">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-434">N/A</span></span>  |
| <span data-ttu-id="ecf0c-435">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-435">**Steps**</span></span> | <span data-ttu-id="ecf0c-436">Siteler arası istek sahtekarlığı (CSRF veya XSRF), bir saldırganın bir web sitesi kurulan oturum farklı bir kullanıcının güvenlik bağlamında eylemleri gerçekleştirebilirsiniz saldırı türüdür.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-436">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in the security context of a different user's established session on a web site.</span></span> <span data-ttu-id="ecf0c-437">Hedeflenen web sitesi alınan istek kimliğini doğrulamak için özel olarak oturum tanımlama dayalıysa değiştirmek veya içerik silmek için belirtilir.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-437">The goal is to modify or delete content, if the targeted web site relies exclusively on session cookies to authenticate received request.</span></span> <span data-ttu-id="ecf0c-438">Bir saldırgan, üzerinde kullanıcı zaten oturum açık bir siteden bir komutla bir URL yüklemek için farklı bir kullanıcının tarayıcı alarak bu güvenlik açığından yararlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-438">An attacker could exploit this vulnerability by getting a different user's browser to load a URL with a command from a vulnerable site on which the user is already logged in.</span></span> <span data-ttu-id="ecf0c-439">Bir bağlantıyı, gibi bir kaynak savunmasız sunucusundan yükler farklı bir web sitesi barındırma veya kullanıcı alma Bunu yapmak bir saldırganın birçok yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-439">There are many ways for an attacker to do that, such as by hosting a different web site that loads a resource from the vulnerable server, or getting the user to click a link.</span></span> <span data-ttu-id="ecf0c-440">Sunucu istemciye bir ek belirteç, belirtecini de gelecekteki tüm istekler dahil etmek istemcinin gerektiriyorsa ve tüm gelecekteki isteklerin ASP.NET kullanılarak gibi geçerli oturum için ilgili bir belirteç dahil olduğunu doğrular, saldırı önlenebilir AntiForgeryToken veya Görünüm durumu.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-440">The attack can be prevented if the server sends an additional token to the client, requires the client to include that token in all future requests, and verifies that all future requests include a token that pertains to the current session, such as by using the ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="ecf0c-441">Başlık</span><span class="sxs-lookup"><span data-stu-id="ecf0c-441">Title</span></span>                   | <span data-ttu-id="ecf0c-442">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="ecf0c-442">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ecf0c-443">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-443">**Component**</span></span>               | <span data-ttu-id="ecf0c-444">Web API</span><span class="sxs-lookup"><span data-stu-id="ecf0c-444">Web API</span></span> | 
| <span data-ttu-id="ecf0c-445">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-445">**SDL Phase**</span></span>               | <span data-ttu-id="ecf0c-446">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-446">Build</span></span> |  
| <span data-ttu-id="ecf0c-447">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-447">**Applicable Technologies**</span></span> | <span data-ttu-id="ecf0c-448">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="ecf0c-448">MVC5, MVC6</span></span> |
| <span data-ttu-id="ecf0c-449">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-449">**Attributes**</span></span>              | <span data-ttu-id="ecf0c-450">Yok</span><span class="sxs-lookup"><span data-stu-id="ecf0c-450">N/A</span></span>  |
| <span data-ttu-id="ecf0c-451">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-451">**References**</span></span>              | [<span data-ttu-id="ecf0c-452">ASP.NET Web API'de siteler arası istek sahtekarlığı (CSRF) saldırılarını önleme</span><span class="sxs-lookup"><span data-stu-id="ecf0c-452">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| <span data-ttu-id="ecf0c-453">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-453">**Steps**</span></span> | <span data-ttu-id="ecf0c-454">Anti-CSRF ve AJAX: JSON verilerini, HTML form verilerini bir AJAX İsteği Gönder çünkü form simgesi AJAX istekleri için bir sorun olabilir.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-454">Anti-CSRF and AJAX: The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="ecf0c-455">Bir çözüm, özel bir HTTP üstbilgisi belirteçleri göndermektir.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-455">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="ecf0c-456">Aşağıdaki kod belirteçleri oluşturmak için Razor sözdizimini kullanır ve ardından bir AJAX isteği belirteçleri ekler.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-456">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> |

### <a name="example"></a><span data-ttu-id="ecf0c-457">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-457">Example</span></span>
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

### <a name="example"></a><span data-ttu-id="ecf0c-458">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-458">Example</span></span>
<span data-ttu-id="ecf0c-459">İsteği işlerken, istek üstbilgisi belirteçleri ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-459">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="ecf0c-460">Ardından belirteçleri doğrulamak için AntiForgery.Validate yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-460">Then call the AntiForgery.Validate method to validate the tokens.</span></span> <span data-ttu-id="ecf0c-461">Belirteçleri geçerli değilse doğrulama yöntemi bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-461">The Validate method throws an exception if the tokens are not valid.</span></span>
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

### <a name="example"></a><span data-ttu-id="ecf0c-462">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-462">Example</span></span>
<span data-ttu-id="ecf0c-463">Anti-CSRF ve ASP.NET MVC formları - AntiForgeryToken yardımcı yöntemi görünümleri kullanma; Örneğin, bir Html.AntiForgeryToken() forma, put,</span><span class="sxs-lookup"><span data-stu-id="ecf0c-463">Anti-CSRF and ASP.NET MVC forms - Use the AntiForgeryToken helper method on Views; put an Html.AntiForgeryToken() into the form, for example,</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a><span data-ttu-id="ecf0c-464">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-464">Example</span></span>
<span data-ttu-id="ecf0c-465">Yukarıdaki örnekte, aşağıdakine benzer çıktı:</span><span class="sxs-lookup"><span data-stu-id="ecf0c-465">The example above will output something like the following:</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="ecf0c-466">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-466">Example</span></span>
<span data-ttu-id="ecf0c-467">Aynı anda Html.AntiForgeryToken() ziyaretçi yukarıda gösterilen rastgele gizli değer ile aynı değere sahip __RequestVerificationToken adlı bir tanımlama bilgisi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-467">At the same time, Html.AntiForgeryToken() gives the visitor a cookie called __RequestVerificationToken, with the same value as the random hidden value shown above.</span></span> <span data-ttu-id="ecf0c-468">Ardından, gelen bir form post doğrulamak için hedef eylem yöntemine [ValidateAntiForgeryToken] filtresini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-468">Next, to validate an incoming form post, add the [ValidateAntiForgeryToken] filter to the target action method.</span></span> <span data-ttu-id="ecf0c-469">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ecf0c-469">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="ecf0c-470">Denetleyen yetkilendirme Filtresi:</span><span class="sxs-lookup"><span data-stu-id="ecf0c-470">Authorization filter that checks that:</span></span>
* <span data-ttu-id="ecf0c-471">Gelen istek __RequestVerificationToken adlı bir tanımlama bilgisi içeriyor</span><span class="sxs-lookup"><span data-stu-id="ecf0c-471">The incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="ecf0c-472">Gelen istek sahip bir `Request.Form` __RequestVerificationToken adlı giriş</span><span class="sxs-lookup"><span data-stu-id="ecf0c-472">The incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="ecf0c-473">Bu tanımlama bilgisi ve `Request.Form` varsayılarak tüm değerleri Eşleştir iyi, istek geçtiği normal olarak.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-473">These cookie and `Request.Form` values match Assuming all is well, the request goes through as normal.</span></span> <span data-ttu-id="ecf0c-474">Ancak değilse, ardından bir Yetkilendirme hatası iletisi "gerekli sahteciliğe karşı koruma belirteci belirtilmedi veya geçersiz".</span><span class="sxs-lookup"><span data-stu-id="ecf0c-474">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span>

| <span data-ttu-id="ecf0c-475">Başlık</span><span class="sxs-lookup"><span data-stu-id="ecf0c-475">Title</span></span>                   | <span data-ttu-id="ecf0c-476">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="ecf0c-476">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ecf0c-477">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-477">**Component**</span></span>               | <span data-ttu-id="ecf0c-478">Web API</span><span class="sxs-lookup"><span data-stu-id="ecf0c-478">Web API</span></span> | 
| <span data-ttu-id="ecf0c-479">**SDL aşaması**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-479">**SDL Phase**</span></span>               | <span data-ttu-id="ecf0c-480">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf0c-480">Build</span></span> |  
| <span data-ttu-id="ecf0c-481">**İlgili teknolojiler**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-481">**Applicable Technologies**</span></span> | <span data-ttu-id="ecf0c-482">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="ecf0c-482">MVC5, MVC6</span></span> |
| <span data-ttu-id="ecf0c-483">**Öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-483">**Attributes**</span></span>              | <span data-ttu-id="ecf0c-484">Kimlik sağlayıcısı - ADFS, kimlik sağlayıcısı - Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecf0c-484">Identity Provider - ADFS, Identity Provider - Azure AD</span></span> |
| <span data-ttu-id="ecf0c-485">**Başvuruları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-485">**References**</span></span>              | [<span data-ttu-id="ecf0c-486">Bireysel hesaplar ve ASP.NET Web API 2.2 yerel oturum açma ile Web API güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="ecf0c-486">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2</span></span>](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| <span data-ttu-id="ecf0c-487">**Adımları**</span><span class="sxs-lookup"><span data-stu-id="ecf0c-487">**Steps**</span></span> | <span data-ttu-id="ecf0c-488">Web API ise OAuth 2.0 kullanan güvenli sonra bir taşıyıcı belirteci yetkilendirme istek üstbilgisinde bekler ve yalnızca belirteç geçerliyse istek erişim verir.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-488">If the Web API is secured using OAuth 2.0, then it expects a bearer token in Authorization request header and grants access to the request only if the token is valid.</span></span> <span data-ttu-id="ecf0c-489">Tanımlama bilgisi tabanlı kimlik doğrulaması, tarayıcılar isteklerine taşıyıcı belirteçlerini eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-489">Unlike cookie based authentication, browsers do not attach the bearer tokens to requests.</span></span> <span data-ttu-id="ecf0c-490">İstek üstbilgisinde taşıyıcı belirteci açıkça eklemek istekte bulunan istemci gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-490">The requesting client needs to explicitly attach the bearer token in the request header.</span></span> <span data-ttu-id="ecf0c-491">Bu nedenle, OAuth 2.0 kullanan korumalı ASP.NET Web API için taşıyıcı belirteçlerini CSRF saldırılarına karşı savunma hattı olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-491">Therefore, for ASP.NET Web APIs protected using OAuth 2.0, bearer tokens are considered as a defense against CSRF attacks.</span></span> <span data-ttu-id="ecf0c-492">Lütfen uygulama MVC kısmı form kimlik doğrulaması (yani, tanımlama bilgileri kullanır) kullanıyorsa, sahteciliğe karşı koruma belirteçleri MVC web uygulaması tarafından kullanılması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-492">Please note that if the MVC portion of the application uses forms authentication (i.e., uses cookies), anti-forgery tokens have to be used by the MVC web app.</span></span> |

### <a name="example"></a><span data-ttu-id="ecf0c-493">Örnek</span><span class="sxs-lookup"><span data-stu-id="ecf0c-493">Example</span></span>
<span data-ttu-id="ecf0c-494">Yalnızca üzerinde taşıyıcı belirteçlerini ve çalıştırılmadı tanımlama bilgilerini yararlanmayı bilgi sahibi olmak Web API vardır.</span><span class="sxs-lookup"><span data-stu-id="ecf0c-494">The Web API has to be informed to rely ONLY on bearer tokens and not on cookies.</span></span> <span data-ttu-id="ecf0c-495">Aşağıdaki yapılandırmada tarafından yapılabilir `WebApiConfig.Register` yöntemi: '''C-Sharp kod yapılandırma. SuppressDefaultHostAuthentication(); Config. Filters.Add (yeni HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span><span class="sxs-lookup"><span data-stu-id="ecf0c-495">It can be done by the following configuration in `WebApiConfig.Register` method: ``\`C-Sharp code config.SuppressDefaultHostAuthentication(); config.Filters.Add(new HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span></span>
```
The SuppressDefaultHostAuthentication method tells Web API to ignore any authentication that happens before the request reaches the Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API to authenticate only using bearer tokens.