---
title: "Azure AD v2 ASP.NET Web sunucusu başlamak - kullanın | Microsoft Docs"
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
ms.openlocfilehash: 3b7d29e48c91f40e8782a5e32a52998b815fe331
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
## <a name="add-a-controller-to-handle-sign-in-and-sign-out-requests"></a><span data-ttu-id="80cab-103">Oturum açma ve oturum kapatma isteklerini işlemek için bir denetleyici ekleyin</span><span class="sxs-lookup"><span data-stu-id="80cab-103">Add a controller to handle sign-in and sign-out requests</span></span>

<span data-ttu-id="80cab-104">Bu adım, oturum açma ve oturum kapatma yöntemlerini kullanıma sunmak için yeni bir denetleyici oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="80cab-104">This step shows how to create a new controller to expose sign-in and sign-out methods.</span></span>

1.  <span data-ttu-id="80cab-105">Sağ tıklayın `Controllers` klasörü ve seçin`Add` > `Controller`</span><span class="sxs-lookup"><span data-stu-id="80cab-105">Right click the `Controllers` folder and select `Add` > `Controller`</span></span>
2.  <span data-ttu-id="80cab-106">Seçin `MVC (.NET version) Controller – Empty`.</span><span class="sxs-lookup"><span data-stu-id="80cab-106">Select `MVC (.NET version) Controller – Empty`.</span></span>
3.  <span data-ttu-id="80cab-107">Tıklatın *Ekle*</span><span class="sxs-lookup"><span data-stu-id="80cab-107">Click *Add*</span></span>
4.  <span data-ttu-id="80cab-108">Bu ad `HomeController` tıklatıp *Ekle*</span><span class="sxs-lookup"><span data-stu-id="80cab-108">Name it `HomeController` and click *Add*</span></span>
5.  <span data-ttu-id="80cab-109">Ekleme *OWIN* sınıfına başvuruyor:</span><span class="sxs-lookup"><span data-stu-id="80cab-109">Add *OWIN* references to the class:</span></span>

```csharp
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
```
<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="80cab-110">Oturum kapatma ve oturum açma işlemek için aşağıdaki iki yöntem, bir kimlik doğrulaması sınaması kodu aracılığıyla başlatarak denetleyicinize ekleyin:</span><span class="sxs-lookup"><span data-stu-id="80cab-110">Add the two methods below to handle sign-in and sign-out to your controller by initiating an authentication challenge via code:</span></span>
</li>
</ol>

```csharp
/// <summary>
/// Send an OpenID Connect sign-in request.
/// Alternatively, you can just decorate the SignIn method with the [Authorize] attribute
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

## <a name="create-the-apps-home-page-to-sign-in-users-via-a-sign-in-button"></a><span data-ttu-id="80cab-111">Kullanıcılar bir oturum açma düğmesi aracılığıyla imzalamak için uygulamanın giriş sayfası oluşturun</span><span class="sxs-lookup"><span data-stu-id="80cab-111">Create the app's home page to sign in users via a sign-in button</span></span>

<span data-ttu-id="80cab-112">Visual Studio'da Oturum Aç düğmesini ekleyin ve kimlik doğrulamasından sonra kullanıcı bilgilerini görüntülemek için yeni bir görünüm oluşturun:</span><span class="sxs-lookup"><span data-stu-id="80cab-112">In Visual Studio, create a new view to add the sign-in button and display user information after authentication:</span></span>

1.  <span data-ttu-id="80cab-113">Sağ tıklayın `Views\Home` klasörü ve seçin`Add View`</span><span class="sxs-lookup"><span data-stu-id="80cab-113">Right click the `Views\Home` folder and select `Add View`</span></span>
2.  <span data-ttu-id="80cab-114">Bunu, `Index` olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="80cab-114">Name it `Index`.</span></span>
3.  <span data-ttu-id="80cab-115">Oturum açma düğmesi içerir, aşağıdaki HTML dosyaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="80cab-115">Add the following HTML, which includes the sign-in button, to the file:</span></span>

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Guide</title>
</head>
<body>
@if (!Request.IsAuthenticated)
{
    <!-- If the user is not authenticated, display the sign-in button -->
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
### <a name="more-information"></a><span data-ttu-id="80cab-116">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="80cab-116">More Information</span></span>
> <span data-ttu-id="80cab-117">Bu sayfa bir oturum açma düğmesi siyah bir arka plan ile SVG biçiminde ekler:</span><span class="sxs-lookup"><span data-stu-id="80cab-117">This page adds a sign-in button in SVG format with a black background:</span></span><br/><span data-ttu-id="80cab-118">![Microsoft ile oturum aç](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)</span><span class="sxs-lookup"><span data-stu-id="80cab-118">![Sign-in with Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)</span></span><br/> <span data-ttu-id="80cab-119">Daha fazla düğme'nın oturum açma Lütfen gidin [bu sayfayı](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "Branding guidelines").</span><span class="sxs-lookup"><span data-stu-id="80cab-119">For more sign-in buttons, please go to the [this page](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "Branding guidelines").</span></span>
<!--end-collapse-->

## <a name="add-a-controller-to-display-users-claims"></a><span data-ttu-id="80cab-120">Kullanıcının talepleri görüntülemek için bir denetleyici ekleyin</span><span class="sxs-lookup"><span data-stu-id="80cab-120">Add a controller to display user's claims</span></span>
<span data-ttu-id="80cab-121">Bu denetleyici kullanımını gösteren `[Authorize]` bir denetleyici korumak için öznitelik.</span><span class="sxs-lookup"><span data-stu-id="80cab-121">This controller demonstrates the uses of the `[Authorize]` attribute to protect a controller.</span></span> <span data-ttu-id="80cab-122">Bu öznitelik, yalnızca kimliği doğrulanan kullanıcılar vererek, denetleyiciye erişimi sınırlandırır.</span><span class="sxs-lookup"><span data-stu-id="80cab-122">This attribute restricts access to the controller by only allowing authenticated users.</span></span> <span data-ttu-id="80cab-123">Aşağıdaki kodu yapar alındı kullanıcı talepleri, oturum açma parçası olarak görüntülemek için özniteliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="80cab-123">The code below makes use of the attribute to display user claims that were retrieved as part of the sign-in.</span></span>

1.  <span data-ttu-id="80cab-124">Sağ tıklayın `Controllers` klasörü:`Add` > `Controller`</span><span class="sxs-lookup"><span data-stu-id="80cab-124">Right click the `Controllers` folder: `Add` > `Controller`</span></span>
2.  <span data-ttu-id="80cab-125">Seçin `MVC {version} Controller – Empty`.</span><span class="sxs-lookup"><span data-stu-id="80cab-125">Select `MVC {version} Controller – Empty`.</span></span>
3.  <span data-ttu-id="80cab-126">Tıklatın *Ekle*</span><span class="sxs-lookup"><span data-stu-id="80cab-126">Click *Add*</span></span>
4.  <span data-ttu-id="80cab-127">Adlandırın`ClaimsController`</span><span class="sxs-lookup"><span data-stu-id="80cab-127">Name it `ClaimsController`</span></span>
5.  <span data-ttu-id="80cab-128">Denetleyici sınıfının kodu aşağıdaki - bu ekler değiştirin `[Authorize]` öznitelik sınıfı:</span><span class="sxs-lookup"><span data-stu-id="80cab-128">Replace the code of your controller class with the code below - this adds the `[Authorize]` attribute to the class:</span></span>

```csharp
[Authorize]
public class ClaimsController : Controller
{
    /// <summary>
    /// Add user's claims to viewbag
    /// </summary>
    /// <returns></returns>
    public ActionResult Index()
    {
        var claimsPrincipalCurrent = System.Security.Claims.ClaimsPrincipal.Current;
        //You get the user’s first and last name below:
        ViewBag.Name = claimsPrincipalCurrent.FindFirst("name").Value;

        // The 'preferred_username' claim can be used for showing the username
        ViewBag.Username = claimsPrincipalCurrent.FindFirst("preferred_username").Value;

        // The subject claim can be used to uniquely identify the user across the web
        ViewBag.Subject = claimsPrincipalCurrent.FindFirst(System.Security.Claims.ClaimTypes.NameIdentifier).Value;

        // TenantId is the unique Tenant Id - which represents an organization in Azure AD
        ViewBag.TenantId = claimsPrincipalCurrent.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;

        return View();
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="80cab-129">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="80cab-129">More Information</span></span>
> <span data-ttu-id="80cab-130">Kullanımı nedeniyle `[Authorize]` özniteliği, bu denetleyicinin tüm yöntemleri, yalnızca kullanıcının kimliği doğrulanırsa çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="80cab-130">Because of the use of the `[Authorize]` attribute, all methods of this controller can only be executed if the user is authenticated.</span></span> <span data-ttu-id="80cab-131">Kullanıcı kimliği doğrulanmamış ve denetleyici erişmeye çalışırsa, OWIN kimlik doğrulaması sınaması başlatabilir ve kullanıcının kimlik doğrulamasını zorla.</span><span class="sxs-lookup"><span data-stu-id="80cab-131">If the user is not authenticated and tries to access the controller, OWIN will initiate an authentication challenge and force the user to authenticate.</span></span> <span data-ttu-id="80cab-132">Yukarıdaki kod talep koleksiyonu görünür `ClaimsPrincipal.Current` kullanıcının belirteçte dahil belirli kullanıcı öznitelikleri için örneği.</span><span class="sxs-lookup"><span data-stu-id="80cab-132">The code above looks at the claims collection of the `ClaimsPrincipal.Current` instance for specific user attributes included in the user’s token.</span></span> <span data-ttu-id="80cab-133">Bu öznitelikler, kullanıcının tam adını ve kullanıcı adı yanı sıra, genel kullanıcı tanımlayıcısı konu içerir.</span><span class="sxs-lookup"><span data-stu-id="80cab-133">These attributes include the user’s full name and username, as well as the global user identifier subject.</span></span> <span data-ttu-id="80cab-134">Ayrıca içerdiği *Kiracı kimliği*, kullanıcının kuruluş Kimliğini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="80cab-134">It also contains the *Tenant ID*, which represents the ID for the user’s organization.</span></span> 
<!--end-collapse-->

## <a name="create-a-view-to-display-the-users-claims"></a><span data-ttu-id="80cab-135">Kullanıcının talepleri görüntülemek için bir görünüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="80cab-135">Create a view to display the user's claims</span></span>

<span data-ttu-id="80cab-136">Visual Studio'da bir web sayfasında kullanıcının talepleri görüntülemek için yeni bir görünüm oluşturun:</span><span class="sxs-lookup"><span data-stu-id="80cab-136">In Visual Studio, create a new view to display the user's claims in a web page:</span></span>

1.  <span data-ttu-id="80cab-137">Sağ tıklayın `Views\Claims` klasörü ve:`Add View`</span><span class="sxs-lookup"><span data-stu-id="80cab-137">Right click the `Views\Claims` folder and: `Add View`</span></span>
2.  <span data-ttu-id="80cab-138">Bunu, `Index` olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="80cab-138">Name it `Index`.</span></span>
3.  <span data-ttu-id="80cab-139">Aşağıdaki HTML dosyaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="80cab-139">Add the following HTML to the file:</span></span>

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
