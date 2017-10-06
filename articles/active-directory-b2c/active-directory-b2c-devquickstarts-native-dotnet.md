---
title: Active Directory B2C aaaAzure | Microsoft Docs
description: "Nasıl toobuild bir Windows masaüstü uygulaması, oturum açma, kaydolma içerir ve Azure Active Directory B2C kullanarak yönetim profili."
services: active-directory-b2c
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9da14362-8216-4485-960e-af17cd5ba3bd
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: f22b0299ff74bfba2f3fea88f006da609859dda5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a><span data-ttu-id="da2e8-103">Azure AD B2C: bir Windows masaüstü uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="da2e8-103">Azure AD B2C: Build a Windows desktop app</span></span>
<span data-ttu-id="da2e8-104">Azure Active Directory (Azure AD) B2C kullanarak kısa birkaç adımda güçlü Self Servis kimlik yönetimi özelliklerini tooyour masaüstü uygulaması ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da2e8-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features tooyour desktop app in a few short steps.</span></span> <span data-ttu-id="da2e8-105">Bu makale size nasıl gösterir toocreate kullanıcı kaydolma, oturum açma ve profil yönetimini kapsayan .NET Windows Presentation Foundation (WPF) "Yapılacaklar listesi" uygulama.</span><span class="sxs-lookup"><span data-stu-id="da2e8-105">This article will show you how toocreate a .NET Windows Presentation Foundation (WPF) "to-do list" app that includes user sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="da2e8-106">Merhaba uygulama bir kullanıcı adı veya e-posta kullanarak kaydolma ve oturum açma için destek içerir.</span><span class="sxs-lookup"><span data-stu-id="da2e8-106">hello app will include support for sign-up and sign-in by using a user name or email.</span></span> <span data-ttu-id="da2e8-107">Facebook ve Google gibi sosyal hesaplarını kullanarak, kaydolma ve oturum açma için destek yer alacaktır.</span><span class="sxs-lookup"><span data-stu-id="da2e8-107">It will also include support for sign-up and sign-in by using social accounts such as Facebook and Google.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="da2e8-108">Azure AD B2C dizini alma</span><span class="sxs-lookup"><span data-stu-id="da2e8-108">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="da2e8-109">Azure AD B2C'yi kullanabilmek için önce dizin veya kiracı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="da2e8-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="da2e8-110">Dizin; tüm kullanıcılarınız, uygulamalarınız, gruplarınız ve daha fazlası için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="da2e8-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="da2e8-111">Henüz yoksa devam etmeden önce bu kılavuzda [bir B2C dizini oluşturun](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="da2e8-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="da2e8-112">Uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="da2e8-112">Create an application</span></span>
<span data-ttu-id="da2e8-113">Ardından B2C dizininizde uygulama toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="da2e8-113">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="da2e8-114">Bu ihtiyaçlarını uygulamanızla toosecurely, iletişim bilgileri Azure AD'ye verir.</span><span class="sxs-lookup"><span data-stu-id="da2e8-114">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="da2e8-115">Uygulama, bir toocreate izleyin [bu yönergeleri](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="da2e8-115">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span>  <span data-ttu-id="da2e8-116">Şunları yaptığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="da2e8-116">Be sure to:</span></span>

* <span data-ttu-id="da2e8-117">Dahil bir **yerel istemci** hello uygulamada.</span><span class="sxs-lookup"><span data-stu-id="da2e8-117">Include a **native client** in hello application.</span></span>
* <span data-ttu-id="da2e8-118">Kopya hello **yeniden yönlendirme URI'si** `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="da2e8-118">Copy hello **Redirect URI** `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="da2e8-119">Bu kod örneği için hello varsayılan URL değil.</span><span class="sxs-lookup"><span data-stu-id="da2e8-119">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="da2e8-120">Kopya hello **uygulama kimliği** diğer bir deyişle atanan tooyour uygulama.</span><span class="sxs-lookup"><span data-stu-id="da2e8-120">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="da2e8-121">Buna daha sonra ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="da2e8-121">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="da2e8-122">İlkelerinizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="da2e8-122">Create your policies</span></span>
<span data-ttu-id="da2e8-123">Azure AD B2C'de her kullanıcı deneyimi, bir [ilke](active-directory-b2c-reference-policies.md) ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="da2e8-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="da2e8-124">Bu kod örneği üç kimlik deneyimi içerir: kaydolma, oturum açın ve profil düzenleme.</span><span class="sxs-lookup"><span data-stu-id="da2e8-124">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span></span> <span data-ttu-id="da2e8-125">Toocreate bir ilke açıklandığı gibi her tür için gereken [ilke başvurusu makalesinde](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="da2e8-125">You need toocreate a policy for each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="da2e8-126">Merhaba üç ilke oluşturduğunuzda, emin olun:</span><span class="sxs-lookup"><span data-stu-id="da2e8-126">When you create hello three policies, be sure to:</span></span>

* <span data-ttu-id="da2e8-127">Ya da seçin **kullanıcı kimliği kaydolma** veya **kayıt e-posta** hello kimlik sağlayıcılar dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="da2e8-127">Choose either **User ID sign-up** or **Email sign-up** in hello identity providers blade.</span></span>
* <span data-ttu-id="da2e8-128">Kaydolma ilkenizde, **Görünen ad** ve diğer kaydolma özniteliklerini seçin.</span><span class="sxs-lookup"><span data-stu-id="da2e8-128">Choose **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="da2e8-129">Her ilke için uygulamanın talep ettiği gibi **Görünen ad** ve **Nesne Kimliği** öğelerini seçin.</span><span class="sxs-lookup"><span data-stu-id="da2e8-129">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="da2e8-130">Diğer talepleri de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da2e8-130">You can choose other claims as well.</span></span>
* <span data-ttu-id="da2e8-131">Kopya hello **adı** oluşturduktan sonra her ilkenin.</span><span class="sxs-lookup"><span data-stu-id="da2e8-131">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="da2e8-132">Merhaba önekine sahip olmalıdır `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="da2e8-132">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="da2e8-133">Bu ilke adlarına daha sonra ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="da2e8-133">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="da2e8-134">Üç ilke hello başarıyla oluşturduktan sonra hazır toobuild olduğunuz uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="da2e8-134">After you have successfully created hello three policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="da2e8-135">Merhaba kodu indirme</span><span class="sxs-lookup"><span data-stu-id="da2e8-135">Download hello code</span></span>
<span data-ttu-id="da2e8-136">Bu öğretici için kod Hello [Github'da korunur](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="da2e8-136">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span></span> <span data-ttu-id="da2e8-137">toobuild hello örnek olarak, Git, yapabilecekleriniz [çatı projesini .zip dosyası olarak indirebilirsiniz](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="da2e8-137">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span></span> <span data-ttu-id="da2e8-138">Ayrıca hello çatıyı kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="da2e8-138">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

<span data-ttu-id="da2e8-139">Tamamlanan hello uygulamadır de [.zip dosyası olarak kullanılabilir](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) veya hello `complete` hello dalı aynı deposu.</span><span class="sxs-lookup"><span data-stu-id="da2e8-139">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

<span data-ttu-id="da2e8-140">Merhaba örnek kodu indirdikten sonra açık hello Visual Studio .sln dosyasını tooget başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="da2e8-140">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="da2e8-141">Merhaba `TaskClient` projedir hello kullanıcı hello WPF masaüstü uygulaması ile etkileşim kurar.</span><span class="sxs-lookup"><span data-stu-id="da2e8-141">hello `TaskClient` project is hello WPF desktop application that hello user interacts with.</span></span> <span data-ttu-id="da2e8-142">Bu öğreticinin Hello amaçları doğrultusunda, arka uç görev web API'si, her kullanıcının yapılacaklar listesini depolayan Azure üzerinde barındırılan çağırır.</span><span class="sxs-lookup"><span data-stu-id="da2e8-142">For hello purposes of this tutorial, it calls a back-end task web API, hosted in Azure, that stores each user's to-do list.</span></span>  <span data-ttu-id="da2e8-143">Toobuild hello web API gerekmez, biz zaten çalışıyor olması.</span><span class="sxs-lookup"><span data-stu-id="da2e8-143">You do not need toobuild hello web API, we already have it running for you.</span></span>

<span data-ttu-id="da2e8-144">güvenli bir şekilde web API'si Azure AD B2C kullanarak istekleri doğrular nasıl toolearn kullanıma [web API Başlarken makale](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="da2e8-144">toolearn how a web API securely authenticates requests by using Azure AD B2C, check out the [web API getting started article](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="execute-policies"></a><span data-ttu-id="da2e8-145">İlkeleri yürütme</span><span class="sxs-lookup"><span data-stu-id="da2e8-145">Execute policies</span></span>
<span data-ttu-id="da2e8-146">Uygulamanızı hello HTTP isteğinin bir parçası olarak tooexecute istedikleri hello İlkesi belirtin kimlik doğrulama iletileri göndererek Azure AD B2C ile iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="da2e8-146">Your app communicates with Azure AD B2C by sending authentication messages that specify hello policy they want tooexecute as part of hello HTTP request.</span></span> <span data-ttu-id="da2e8-147">Merhaba kullanabileceğiniz .NET Masaüstü uygulamaları için Microsoft kimlik doğrulama kitaplığı (MSAL) toosend OAuth 2.0 kimlik doğrulama iletileri önizleme, ilkeleri yürütün ve bu çağrı web API'leri belirteçleri almak.</span><span class="sxs-lookup"><span data-stu-id="da2e8-147">For .NET desktop applications, you can use hello preview Microsoft Authentication Library (MSAL) toosend OAuth 2.0 authentication messages, execute policies, and get tokens that call web APIs.</span></span>

### <a name="install-msal"></a><span data-ttu-id="da2e8-148">MSAL yükleyin</span><span class="sxs-lookup"><span data-stu-id="da2e8-148">Install MSAL</span></span>
<span data-ttu-id="da2e8-149">MSAL toohello ekleme `TaskClient` hello Visual Studio Paket Yöneticisi konsolu kullanarak proje.</span><span class="sxs-lookup"><span data-stu-id="da2e8-149">Add MSAL toohello `TaskClient` project by using hello Visual Studio Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a><span data-ttu-id="da2e8-150">B2C bilgilerinizi girme</span><span class="sxs-lookup"><span data-stu-id="da2e8-150">Enter your B2C details</span></span>
<span data-ttu-id="da2e8-151">Açık hello dosya `Globals.cs` ve her hello özellik değerleri kendinizinkilerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="da2e8-151">Open hello file `Globals.cs` and replace each of hello property values with your own.</span></span> <span data-ttu-id="da2e8-152">Bu sınıf genelinde kullanılan `TaskClient` tooreference yaygın olarak kullanılan değerler.</span><span class="sxs-lookup"><span data-stu-id="da2e8-152">This class is used throughout `TaskClient` tooreference commonly used values.</span></span>

```C#
public static class Globals
{
    ...

    // TODO: Replace these five default with your own configuration values
    public static string tenant = "fabrikamb2c.onmicrosoft.com";
    public static string clientId = "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6";
    public static string signInPolicy = "b2c_1_sign_in";
    public static string signUpPolicy = "b2c_1_sign_up";
    public static string editProfilePolicy = "b2c_1_edit_profile";

    ...
}
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="create-hello-publicclientapplication"></a><span data-ttu-id="da2e8-153">Merhaba PublicClientApplication oluşturma</span><span class="sxs-lookup"><span data-stu-id="da2e8-153">Create hello PublicClientApplication</span></span>
<span data-ttu-id="da2e8-154">Merhaba birincil sınıf MSAL `PublicClientApplication`.</span><span class="sxs-lookup"><span data-stu-id="da2e8-154">hello primary class of MSAL is `PublicClientApplication`.</span></span> <span data-ttu-id="da2e8-155">Bu sınıf, uygulamanızın hello Azure AD B2C sistemde temsil eder.</span><span class="sxs-lookup"><span data-stu-id="da2e8-155">This class represents your application in hello Azure AD B2C system.</span></span> <span data-ttu-id="da2e8-156">Merhaba uygulama initalizes oluşturduğunuzda örneği `PublicClientApplication` içinde `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="da2e8-156">When hello app initalizes, create an instance of `PublicClientApplication` in `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="da2e8-157">Bu hello penceresi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="da2e8-157">This can be used throughout hello window.</span></span>

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens toopersist when hello user closes hello app,
        // we've extended hello MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a><span data-ttu-id="da2e8-158">Kaydolma akışı başlatma</span><span class="sxs-lookup"><span data-stu-id="da2e8-158">Initiate a sign-up flow</span></span>
<span data-ttu-id="da2e8-159">Bir kullanıcı yukarı toosigns seçtiğinde tooinitiate oluşturduğunuz hello kaydolma ilkeyi kullanan bir kaydolma akışı istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="da2e8-159">When a user opts toosigns up, you want tooinitiate a sign-up flow that uses hello sign-up policy you created.</span></span> <span data-ttu-id="da2e8-160">MSAL kullanarak, yalnızca çağırmanız `pca.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="da2e8-160">By using MSAL, you just call `pca.AcquireTokenAsync(...)`.</span></span> <span data-ttu-id="da2e8-161">Merhaba çok geçirdiğiniz parametreler`AcquireTokenAsync(...)` hangi belirteci, aldığınız hello kimlik doğrulama isteği ve daha fazlasını kullanılan hello ilkesi belirleyin.</span><span class="sxs-lookup"><span data-stu-id="da2e8-161">hello parameters you pass too`AcquireTokenAsync(...)` determine which token you receive, hello policy used in hello authentication request, and more.</span></span>

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use hello app's clientId here as hello scope parameter, indicating that
        // you want a token toohello your app's backend web API (represented by
        // hello cloud hosted task API).  Use hello UiOptions.ForceLogin flag to
        // indicate tooMSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in hello app that hello user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When hello request completes successfully, you can get user
        // information from hello AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After hello sign up successfully completes, display hello user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of hello policy.
    catch (MsalException ex)
    {
        if (ex.ErrorCode != "authentication_canceled")
        {
            // An unexpected error occurred.
            string message = ex.Message;
            if (ex.InnerException != null)
            {
                message += "Inner Exception : " + ex.InnerException.Message;
            }

            MessageBox.Show(message);
        }

        return;
    }
}
```

### <a name="initiate-a-sign-in-flow"></a><span data-ttu-id="da2e8-162">Oturum açma akışını başlatmak</span><span class="sxs-lookup"><span data-stu-id="da2e8-162">Initiate a sign-in flow</span></span>
<span data-ttu-id="da2e8-163">Merhaba bir oturum açma akışını başlatabilirsiniz aynı şekilde kaydolma akış başlatmak.</span><span class="sxs-lookup"><span data-stu-id="da2e8-163">You can initiate a sign-in flow in hello same way that you initiate a sign-up flow.</span></span> <span data-ttu-id="da2e8-164">Bir kullanıcı oturum açtığında aynı hello olun tooMSAL, arama, oturum açma ilkesini kullanarak bu saati:</span><span class="sxs-lookup"><span data-stu-id="da2e8-164">When a user signs in, make hello same call tooMSAL, this time by using your sign-in policy:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.signInPolicy);
        ...
```

### <a name="initiate-an-edit-profile-flow"></a><span data-ttu-id="da2e8-165">Bir profili Düzenle akışı başlatma</span><span class="sxs-lookup"><span data-stu-id="da2e8-165">Initiate an edit-profile flow</span></span>
<span data-ttu-id="da2e8-166">Yeniden hello profili Düzenle İlkesi yürütebilir aynı şekilde:</span><span class="sxs-lookup"><span data-stu-id="da2e8-166">Again, you can execute an edit-profile policy in hello same fashion:</span></span>

```C#
private async void EditProfile(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.editProfilePolicy);
```

<span data-ttu-id="da2e8-167">Bu durumların tümünde, MSAL bir belirteç içine ya da döndürür `AuthenticationResult` veya bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="da2e8-167">In all of these cases, MSAL either returns a token in `AuthenticationResult` or throws an exception.</span></span> <span data-ttu-id="da2e8-168">MSAL belirteci Al her zaman hello kullanabilirsiniz `AuthenticationResult.User` tooupdate hello kullanıcı verilerini hello UI gibi hello uygulama nesnesi.</span><span class="sxs-lookup"><span data-stu-id="da2e8-168">Each time you get a token from MSAL, you can use hello `AuthenticationResult.User` object tooupdate hello user data in hello app, such as hello UI.</span></span> <span data-ttu-id="da2e8-169">ADAL de önbellekleri hello uygulama diğer bölümleri kullanmak için belirteç hello.</span><span class="sxs-lookup"><span data-stu-id="da2e8-169">ADAL also caches hello token for use in other parts of hello application.</span></span>

### <a name="check-for-tokens-on-app-start"></a><span data-ttu-id="da2e8-170">Uygulama başlangıç belirteçleri denetleyin</span><span class="sxs-lookup"><span data-stu-id="da2e8-170">Check for tokens on app start</span></span>
<span data-ttu-id="da2e8-171">Merhaba kullanıcının oturum açma durumu MSAL tookeep izleme de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da2e8-171">You can also use MSAL tookeep track of hello user's sign-in state.</span></span>  <span data-ttu-id="da2e8-172">Bu uygulamada hello kullanıcı tooremain bile bunlar hello uygulamasını kapatın ve yeniden açın sonra oturum istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="da2e8-172">In this app, we want hello user tooremain signed in even after they close hello app & re-open it.</span></span>  <span data-ttu-id="da2e8-173">Merhaba içinde geri `OnInitialized` geçersiz kılma, MSAL'ın kullanmak `AcquireTokenSilent` yöntemi toocheck önbelleğe alınmış belirteçler için:</span><span class="sxs-lookup"><span data-stu-id="da2e8-173">Back inside hello `OnInitialized` override, use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

```C#
AuthenticationResult result = null;
try
{
    // If hello user has has a token cached with any policy, we'll display them as signed-in.
    TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
    string existingPolicy = tci == null ? null : tci.Policy;
    result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    SignInButton.Visibility = Visibility.Collapsed;
    SignUpButton.Visibility = Visibility.Collapsed;
    EditProfileButton.Visibility = Visibility.Visible;
    SignOutButton.Visibility = Visibility.Visible;
    UsernameLabel.Content = result.User.Name;
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "failed_to_acquire_token_silently")
    {
        // There are no tokens in hello cache.  Proceed without calling hello tooDo list service.
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
    return;
}
```

## <a name="call-hello-task-api"></a><span data-ttu-id="da2e8-174">Merhaba görev API çağrısı</span><span class="sxs-lookup"><span data-stu-id="da2e8-174">Call hello task API</span></span>
<span data-ttu-id="da2e8-175">Şimdi MSAL tooexecute ilkeleri kullanmış ve belirteçleri almak.</span><span class="sxs-lookup"><span data-stu-id="da2e8-175">You have now used MSAL tooexecute policies and get tokens.</span></span>  <span data-ttu-id="da2e8-176">Toouse biri bu belirteçleri toocall hello görev API istediğinizde MSAL'ın yeniden kullanabilirsiniz `AcquireTokenSilent` yöntemi toocheck önbelleğe alınmış belirteçler için:</span><span class="sxs-lookup"><span data-stu-id="da2e8-176">When you want toouse one these tokens toocall hello task API, you can again use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want toocheck for a cached token, independent of whatever policy was used tooacquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent tooindicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch hello exception and show hello user a message.
    catch (MsalException ex)
    {
        // There is no access token in hello cache, so prompt hello user toosign-in.
        if (ex.ErrorCode == "failed_to_acquire_token_silently")
        {
            MessageBox.Show("Please sign up or sign in first");
            SignInButton.Visibility = Visibility.Visible;
            SignUpButton.Visibility = Visibility.Visible;
            EditProfileButton.Visibility = Visibility.Collapsed;
            SignOutButton.Visibility = Visibility.Collapsed;
            UsernameLabel.Content = string.Empty;
        }
        else
        {
            // An unexpected error occurred.
            string message = ex.Message;
            if (ex.InnerException != null)
            {
                message += "Inner Exception : " + ex.InnerException.Message;
            }
            MessageBox.Show(message);
        }

        return;
    }
    ...
```

<span data-ttu-id="da2e8-177">Ne zaman hello çağrısı çok`AcquireTokenSilentAsync(...)` başarılı olur ve bir belirteç bulundu hello Önbelleği'nde hello belirteci toohello ekleyebilirsiniz `Authorization` hello HTTP isteği üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="da2e8-177">When hello call too`AcquireTokenSilentAsync(...)` succeeds and a token is found in hello cache, you can add hello token toohello `Authorization` header of hello HTTP request.</span></span> <span data-ttu-id="da2e8-178">Merhaba görev web API bu başlığı tooauthenticate hello isteği tooread hello kullanıcının yapılacaklar listesi kullanır:</span><span class="sxs-lookup"><span data-stu-id="da2e8-178">hello task web API will use this header tooauthenticate hello request tooread hello user's to-do list:</span></span>

```C#
    ...
    // Once hello token has been returned by MSAL, add it toohello http authorization header, before making hello call tooaccess hello tooDo list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call hello tooDo list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-hello-user-out"></a><span data-ttu-id="da2e8-179">Out hello kullanıcı oturum açın</span><span class="sxs-lookup"><span data-stu-id="da2e8-179">Sign hello user out</span></span>
<span data-ttu-id="da2e8-180">Son olarak, MSAL kullanabilirsiniz bir kullanıcının oturumunu hello kullanıcı seçtiğinde hello uygulamayla tooend **oturumu**.  MSAL kullanırken, bu tüm hello belirteç önbelleği hello belirteçlerinden temizleyerek gerçekleştirilir:</span><span class="sxs-lookup"><span data-stu-id="da2e8-180">Finally, you can use MSAL tooend a user's session with hello app when hello user selects **Sign out**.  When using MSAL, this is accomplished by clearing all of hello tokens from hello token cache:</span></span>

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of hello user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in hello browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update hello UI tooshow hello user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-hello-sample-app"></a><span data-ttu-id="da2e8-181">Merhaba örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="da2e8-181">Run hello sample app</span></span>
<span data-ttu-id="da2e8-182">Son olarak, yapı ve hello örnek çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="da2e8-182">Finally, build and run hello sample.</span></span>  <span data-ttu-id="da2e8-183">Bir e-posta adresi veya kullanıcı adı kullanarak Hello uygulaması için kaydolun.</span><span class="sxs-lookup"><span data-stu-id="da2e8-183">Sign up for hello app by using an email address or user name.</span></span> <span data-ttu-id="da2e8-184">Oturumu kapatın ve tekrar oturum içinde hello aynı kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="da2e8-184">Sign out and sign back in as hello same user.</span></span> <span data-ttu-id="da2e8-185">Bu kullanıcının profilini düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="da2e8-185">Edit that user's profile.</span></span> <span data-ttu-id="da2e8-186">Oturumu kapatın ve farklı bir kullanıcı kullanarak kaydolun.</span><span class="sxs-lookup"><span data-stu-id="da2e8-186">Sign out and sign up by using a different user.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="da2e8-187">Sosyal IDPs Ekle</span><span class="sxs-lookup"><span data-stu-id="da2e8-187">Add social IDPs</span></span>
<span data-ttu-id="da2e8-188">Şu anda hello uygulama yalnızca kullanıcı kaydolma ve oturum kullanan açma destekler **yerel hesaplar**.</span><span class="sxs-lookup"><span data-stu-id="da2e8-188">Currently, hello app supports only user sign-up and sign-in that use **local accounts**.</span></span> <span data-ttu-id="da2e8-189">Bunlar, bir kullanıcı adı ve parola kullanan B2C dizininizde depolanan hesaplarıdır.</span><span class="sxs-lookup"><span data-stu-id="da2e8-189">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="da2e8-190">Azure AD B2C kullanarak kodunuzu değiştirmeden diğer kimlik sağlayıcılardan (IDPs) için destek ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da2e8-190">By using Azure AD B2C, you can add support for other identity providers (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="da2e8-191">tooadd sosyal IDPs tooyour uygulama, izleyerek başlamak hello ayrıntılı yönergeler bu makalelerde.</span><span class="sxs-lookup"><span data-stu-id="da2e8-191">tooadd social IDPs tooyour app, begin by following hello detailed instructions in these articles.</span></span> <span data-ttu-id="da2e8-192">Her IDP için toosupport istediğiniz, bu sistemde tooregister uygulamanın gerekir ve bir istemci kimliği alın</span><span class="sxs-lookup"><span data-stu-id="da2e8-192">For each IDP you want toosupport, you need tooregister an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="da2e8-193">Facebook bir IDP ayarlayın</span><span class="sxs-lookup"><span data-stu-id="da2e8-193">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="da2e8-194">Google bir IDP ayarlayın</span><span class="sxs-lookup"><span data-stu-id="da2e8-194">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="da2e8-195">Amazon bir IDP ayarlayın</span><span class="sxs-lookup"><span data-stu-id="da2e8-195">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="da2e8-196">LinkedIn bir IDP ayarlayın</span><span class="sxs-lookup"><span data-stu-id="da2e8-196">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="da2e8-197">Merhaba kimlik sağlayıcıları tooyour B2C dizini ekledikten sonra her üç ilkenizi tooinclude olarak yeni IDPs hello açıklanan hello tooedit gerek [ilke başvurusu makalesinde](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="da2e8-197">After you add hello identity providers tooyour B2C directory, you need tooedit each of your three policies tooinclude hello new IDPs, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="da2e8-198">İlkelerinizi kaydettikten sonra hello uygulamayı yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="da2e8-198">After you save your policies, run hello app again.</span></span> <span data-ttu-id="da2e8-199">Oturum açma ve kaydolma seçenekleri her kimlik deneyimlerinizi yeni IDPs eklenen hello görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="da2e8-199">You should see hello new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="da2e8-200">İlkelerinizle denemeler ve örnek uygulamanızı hello etkileri gözlemleyin.</span><span class="sxs-lookup"><span data-stu-id="da2e8-200">You can experiment with your policies and observe hello effects on your sample app.</span></span> <span data-ttu-id="da2e8-201">Ekleyebilir veya IDPs kaldırmak, uygulamanın talep değiştirmek veya kaydolma özniteliklerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da2e8-201">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="da2e8-202">İlkeleri, kimlik doğrulama isteklerini ve MSAL nasıl birbirine bağlayan görene kadar deneyin.</span><span class="sxs-lookup"><span data-stu-id="da2e8-202">Experiment until you can see how policies, authentication requests, and MSAL tie together.</span></span>

<span data-ttu-id="da2e8-203">Başvuru için hello tamamlandı örnek [bir .zip dosyası olarak sağlanan](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="da2e8-203">For reference, hello completed sample [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="da2e8-204">Aynı zamanda GitHub'dan kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="da2e8-204">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
