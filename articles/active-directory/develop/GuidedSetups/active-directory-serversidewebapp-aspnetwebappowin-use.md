---
title: "aaaAzure AD v2 ASP.NET Web sunucusu Getting Started - kullanım | Microsoft Docs"
description: "Microsoft oturum açma Openıd Connect standardını kullanan geleneksel web tarayıcı tabanlı bir uygulama ile ASP.NET çözümünü uygulama"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 03afce6fa6598215e8c4af841c00762c143a0cd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="add-a-controller-toohandle-sign-in-and-sign-out-requests"></a>Denetleyici toohandle oturum açma ve oturum kapatma isteklerini ekleyin

Bu adım programlarını nasıl toocreate yeni bir denetleyici tooexpose oturum açma ve oturum kapatma yöntemlerini.

1.  Merhaba sağ tıklayın `Controllers` klasörü ve seçin`Add` > `Controller`
2.  `MVC (.NET version) Controller – Empty` öğesini seçin.
3.  Tıklatın *Ekle*
4.  Bu ad `HomeController` tıklatıp *Ekle*
5.  Ekleme *OWIN* toohello sınıfı başvuruyor:

```csharp
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
```
<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
Bir kimlik doğrulaması sınaması kodu aracılığıyla başlatarak Hello iki yöntem aşağıda toohandle oturum açma ve oturum kapatma tooyour denetleyici ekleyin:
</li>
</ol>

```csharp
/// <summary>
/// Send an OpenID Connect sign-in request.
/// Alternatively, you can just decorate hello SignIn method with hello [Authorize] attribute
/// </summary>
public void SignIn()
{
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge(
            new AuthenticationProperties{ RedirectUri = "/" },
            OpenIdConnectAuthenticationDefaults.AuthenticationType);
    }
}

/// <summary>
/// Send an OpenID Connect sign-out request.
/// </summary>
public void SignOut()
{
    HttpContext.GetOwinContext().Authentication.SignOut(
            OpenIdConnectAuthenticationDefaults.AuthenticationType,
            CookieAuthenticationDefaults.AuthenticationType);
}
```

## <a name="create-hello-apps-home-page-toosign-in-users-via-a-sign-in-button"></a>Kullanıcılar bir oturum açma düğmesiyle Hello uygulamanın giriş sayfası toosign oluşturma

Visual Studio'da oturum açma yeni bir görünüm tooadd hello düğmesini oluşturun ve kimlik doğrulamasından sonra kullanıcı bilgilerini görüntüleyin:

1.  Merhaba sağ tıklayın `Views\Home` klasörü ve seçin`Add View`
2.  Bunu, `Index` olarak adlandırın.
3.  Merhaba oturum açma düğmesi, toohello dosyasını içeren HTML aşağıdaki hello ekleyin:

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Guide</title>
</head>
<body>
@if (!Request.IsAuthenticated)
{
    <!-- If hello user is not authenticated, display hello sign-in button -->
    <a href="@Url.Action("SignIn", "Home")" style="text-decoration: none;">
        <svg xmlns="http://www.w3.org/2000/svg" xml:space="preserve" width="300px" height="50px" viewBox="0 0 3278 522" class="SignInButton">
        <style type="text/css">.fil0:hover {fill: #4B4B4B;} .fnt0 {font-size: 260px;font-family: 'Segoe UI Semibold', 'Segoe UI'; text-decoration: none;}</style>
        <rect class="fil0" x="2" y="2" width="3174" height="517" fill="black" />
        <rect x="150" y="129" width="122" height="122" fill="#F35325" />
        <rect x="284" y="129" width="122" height="122" fill="#81BC06" />
        <rect x="150" y="263" width="122" height="122" fill="#05A6F0" />
        <rect x="284" y="263" width="122" height="122" fill="#FFBA08" />
        <text x="470" y="357" fill="white" class="fnt0">Sign in with Microsoft</text>
        </svg>
    </a>
}
else
{
    <span><br/>Hello @System.Security.Claims.ClaimsPrincipal.Current.FindFirst("name").Value;</span>
    <br /><br />
    @Html.ActionLink("See Your Claims", "Index", "Claims")
    <br /><br />
    @Html.ActionLink("Sign out", "SignOut", "Home")
}
@if (!string.IsNullOrWhiteSpace(Request.QueryString["errormessage"]))
{
    <div style="background-color:red;color:white;font-weight: bold;">Error: @Request.QueryString["errormessage"]</div>
}
</body>
</html>
```
<!--start-collapse-->
### <a name="more-information"></a>Daha Fazla Bilgi
> Bu sayfa bir oturum açma düğmesi siyah bir arka plan ile SVG biçiminde ekler:<br/>![Microsoft ile oturum aç](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)<br/> Daha fazla oturum açma için lütfen toohello gitme düğmeleri [bu sayfayı](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "yönergeleri marka").
<!--end-collapse-->

## <a name="add-a-controller-toodisplay-users-claims"></a>Bir denetleyici toodisplay kullanıcının talep ekleme
Bu denetleyici hello kullanır hello gösterir `[Authorize]` tooprotect bir denetleyici özniteliği. Bu öznitelik, yalnızca kimliği doğrulanan kullanıcılar vererek erişimi toohello denetleyicisi kısıtlar. Aşağıdaki kodu Hello kapsamında hello oturum açma alındı hello özniteliği toodisplay kullanıcı talepleri kullanır.

1.  Merhaba sağ tıklayın `Controllers` klasörü:`Add` > `Controller`
2.  `MVC {version} Controller – Empty` öğesini seçin.
3.  Tıklatın *Ekle*
4.  Adlandırın`ClaimsController`
5.  Merhaba kod değiştirin bu hello ekler aşağıdaki - hello koduyla denetleyici sınıfının `[Authorize]` özniteliği toohello sınıfı:

```csharp
[Authorize]
public class ClaimsController : Controller
{
    /// <summary>
    /// Add user's claims tooviewbag
    /// </summary>
    /// <returns></returns>
    public ActionResult Index()
    {
        var claimsPrincipalCurrent = System.Security.Claims.ClaimsPrincipal.Current;
        //You get hello user’s first and last name below:
        ViewBag.Name = claimsPrincipalCurrent.FindFirst("name").Value;

        // hello 'preferred_username' claim can be used for showing hello username
        ViewBag.Username = claimsPrincipalCurrent.FindFirst("preferred_username").Value;

        // hello subject claim can be used toouniquely identify hello user across hello web
        ViewBag.Subject = claimsPrincipalCurrent.FindFirst(System.Security.Claims.ClaimTypes.NameIdentifier).Value;

        // TenantId is hello unique Tenant Id - which represents an organization in Azure AD
        ViewBag.TenantId = claimsPrincipalCurrent.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;

        return View();
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a>Daha Fazla Bilgi
> Merhaba hello kullanımı nedeniyle `[Authorize]` özniteliği, bu denetleyicinin tüm yöntemleri, yalnızca hello kullanıcı kimliği doğrulanırsa çalıştırılabilir. Merhaba kullanıcı kimliği doğrulanmamış ve tooaccess hello denetleyicisi çalışırsa, OWIN kimlik doğrulaması sınaması başlatabilir ve hello kullanıcı tooauthenticate zorla. bakar Merhaba, yukarıdaki Hello kodu talep hello koleksiyonunu `ClaimsPrincipal.Current` hello kullanıcının belirteçte dahil belirli kullanıcı öznitelikleri için örneği. Bu öznitelikler hello genel kullanıcı tanımlayıcısı konu yanı sıra hello kullanıcının tam adını ve kullanıcı adını içerir. Ayrıca hello içerdiği *Kiracı kimliği*, hello kullanıcının kuruluş için hello Kimliğini temsil eder. 
<!--end-collapse-->

## <a name="create-a-view-toodisplay-hello-users-claims"></a>Toodisplay hello kullanıcının talepleri bir görünüm oluşturma

Visual Studio'da bir web sayfasında toodisplay hello kullanıcının talepleri yeni bir görünüm oluşturun:

1.  Merhaba sağ tıklayın `Views\Claims` klasörü ve:`Add View`
2.  Bunu, `Index` olarak adlandırın.
3.  Aşağıdaki HTML toohello dosyasına hello ekleyin:

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Sample</title>
    <link href="@Url.Content("~/Content/bootstrap.min.css")" rel="stylesheet" type="text/css" />
</head>
<body style="padding:50px">
    <h3>Main Claims:</h3>
    <table class="table table-striped table-bordered table-hover">
        <tr><td>Name</td><td>@ViewBag.Name</td></tr>
        <tr><td>Username</td><td>@ViewBag.Username</td></tr>
        <tr><td>Subject</td><td>@ViewBag.Subject</td></tr>
        <tr><td>TenantId</td><td>@ViewBag.TenantId</td></tr>
    </table>
    <br />
    <h3>All Claims:</h3>
    <table class="table table-striped table-bordered table-hover table-condensed">
    @foreach (var claim in System.Security.Claims.ClaimsPrincipal.Current.Claims)
    {
        <tr><td>@claim.Type</td><td>@claim.Value</td></tr>
    }
</table>
    <br />
    <br />
    @Html.ActionLink("Sign out", "SignOut", "Home", null, new { @class = "btn btn-primary" })
</body>
</html>
```
