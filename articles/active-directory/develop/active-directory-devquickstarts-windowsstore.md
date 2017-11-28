---
title: "Azure AD Windows Mağazası'nın Başlarken | Microsoft Docs"
description: "Oturum açma için Azure AD ile tümleştirme, Azure AD çağıran derleme Windows mağazası uygulamaları API'leri OAuth kullanan korumalı."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 3b96a6d1-270b-4ac1-b9b5-58070c896a68
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 09/16/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 6b5189dc06d7f8b0ed4426944948b904feba847e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a><span data-ttu-id="37e5e-103">Azure AD Windows mağazası uygulamaları ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="37e5e-103">Integrate Azure AD with Windows Store apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="37e5e-104">Windows mağazası 8.1 ve önceki sürümü projeleri Visual Studio 2017 desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="37e5e-104">Windows Store 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="37e5e-105">Daha fazla bilgi için bkz. [Visual Studio 2017 Platform Desteği ve Uyumluluk](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="37e5e-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="37e5e-106">Windows mağazası için uygulama geliştiriyorsanız, Azure Active Directory (Azure AD), basit ve kendi Active Directory hesaplarıyla, kullanıcıların kimliklerini doğrulamak kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="37e5e-106">If you're developing apps for the Windows Store, Azure Active Directory (Azure AD) makes it simple and straightforward to authenticate your users with their Active Directory accounts.</span></span> <span data-ttu-id="37e5e-107">Bir uygulama, Azure AD ile tümleştirerek, güvenli bir şekilde Office 365 API'leri veya Azure API'sini gibi Azure AD tarafından korunan tüm web API'si kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="37e5e-107">By integrating with Azure AD, an app can securely consume any web API that's protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="37e5e-108">Korunan kaynaklara erişim için gereken Windows mağazası Masaüstü uygulamaları için Active Directory Authentication Library (ADAL) Azure AD sağlar.</span><span class="sxs-lookup"><span data-stu-id="37e5e-108">For Windows Store desktop apps that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="37e5e-109">ADAL tek amacı, erişim belirteçleri almak uygulama için kolay hale getirmektir.</span><span class="sxs-lookup"><span data-stu-id="37e5e-109">The sole purpose of ADAL is to make it easy for the app to get access tokens.</span></span> <span data-ttu-id="37e5e-110">Ne kadar kolay olduğunu göstermek için bu makalede DirectorySearcher Windows mağazası uygulamasının nasıl oluşturulacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="37e5e-110">To demonstrate how easy it is, this article shows how to build a DirectorySearcher Windows Store app that:</span></span>

* <span data-ttu-id="37e5e-111">Alır erişim belirteçleri kullanarak Azure AD Graph API çağırma [OAuth 2.0 kimlik doğrulama protokolü](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="37e5e-111">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="37e5e-112">Sağlanan kullanıcı asıl adı (UPN) sahip kullanıcılar için bir dizin arar.</span><span class="sxs-lookup"><span data-stu-id="37e5e-112">Searches a directory for users with a given user principal name (UPN).</span></span>
* <span data-ttu-id="37e5e-113">İşaretlerini kullanıcıları.</span><span class="sxs-lookup"><span data-stu-id="37e5e-113">Signs users out.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="37e5e-114">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="37e5e-114">Before you get started</span></span>
* <span data-ttu-id="37e5e-115">Karşıdan [çatı projesini](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), veya indirme [tamamlanan örnek](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="37e5e-115">Download the [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), or download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span></span> <span data-ttu-id="37e5e-116">Her yükleme Visual Studio 2015 çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="37e5e-116">Each download is a Visual Studio 2015 solution.</span></span>
* <span data-ttu-id="37e5e-117">Ayrıca, kullanıcılar oluşturmak ve uygulamayı kaydetmek Azure AD kiracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="37e5e-117">You also need an Azure AD tenant in which to create users and register the app.</span></span> <span data-ttu-id="37e5e-118">Bir kiracı yoksa [edinebileceğinizi öğrenin](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="37e5e-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="37e5e-119">Hazır olduğunuzda, sonraki üç bölümde yordamları izleyin.</span><span class="sxs-lookup"><span data-stu-id="37e5e-119">When you are ready, follow the procedures in the next three sections.</span></span>

## <a name="step-1-register-the-directorysearcher-app"></a><span data-ttu-id="37e5e-120">1. adım: DirectorySearcher uygulamayı Kaydet</span><span class="sxs-lookup"><span data-stu-id="37e5e-120">Step 1: Register the DirectorySearcher app</span></span>
<span data-ttu-id="37e5e-121">Belirteçleri almak uygulamayı etkinleştirmek için önce Azure AD kiracınızda kaydetmek ve Azure AD grafik API'sine erişim izni vermek gerekir.</span><span class="sxs-lookup"><span data-stu-id="37e5e-121">To enable the app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API.</span></span> <span data-ttu-id="37e5e-122">Bunu yapmak için:</span><span class="sxs-lookup"><span data-stu-id="37e5e-122">Here's how:</span></span>

1. <span data-ttu-id="37e5e-123">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="37e5e-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="37e5e-124">Üst çubuğunda hesabınızı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="37e5e-124">On the top bar, click your account.</span></span> <span data-ttu-id="37e5e-125">Ardından, altında **Directory** listesinde, uygulama kaydetmek istediğiniz Active Directory Kiracı seçin.</span><span class="sxs-lookup"><span data-stu-id="37e5e-125">Then, under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="37e5e-126">Tıklatın **daha Hizmetleri** sol bölmesinde ve seçip **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="37e5e-126">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="37e5e-127">Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="37e5e-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="37e5e-128">Oluşturmak için istemleri izleyerek bir **yerel istemci uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="37e5e-128">Follow the prompts to create a **Native Client Application**.</span></span>
  * <span data-ttu-id="37e5e-129">**Ad** kullanıcılara uygulamasının açıklar.</span><span class="sxs-lookup"><span data-stu-id="37e5e-129">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="37e5e-130">**Yeniden yönlendirme URI'si** belirteci yanıtları döndürmek için Azure AD kullanır ve dize şeması bir birleşimidir.</span><span class="sxs-lookup"><span data-stu-id="37e5e-130">**Redirect URI** is a scheme and string combination that Azure AD uses to return token responses.</span></span> <span data-ttu-id="37e5e-131">Şu an için bir yer tutucu değerini girin (örneğin, **http://DirectorySearcher**).</span><span class="sxs-lookup"><span data-stu-id="37e5e-131">Enter a placeholder value for now (for example, **http://DirectorySearcher**).</span></span> <span data-ttu-id="37e5e-132">Değer daha sonra değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37e5e-132">You'll replace the value later.</span></span>
6. <span data-ttu-id="37e5e-133">Kayıt tamamladıktan sonra Azure AD uygulama benzersiz uygulama kimliği atar.</span><span class="sxs-lookup"><span data-stu-id="37e5e-133">After you’ve completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="37e5e-134">Değer kopyalayın **uygulama** sekmesinde, çünkü daha sonra ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="37e5e-134">Copy the value on the **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="37e5e-135">Üzerinde **ayarları** sayfasında, **gerekli izinler**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="37e5e-135">On the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="37e5e-136">İçin **Azure Active Directory** uygulama, select **Microsoft Graph** API olarak.</span><span class="sxs-lookup"><span data-stu-id="37e5e-136">For the **Azure Active Directory** app, select **Microsoft Graph** as the API.</span></span>
9. <span data-ttu-id="37e5e-137">Altında **izinlere temsilci**, ekleme **gibi oturum açan kullanıcının dizine erişim** izni.</span><span class="sxs-lookup"><span data-stu-id="37e5e-137">Under **Delegated Permissions**, add the **Access the directory as the signed-in user** permission.</span></span> <span data-ttu-id="37e5e-138">Bunun yapılması, kullanıcılar için grafik API'si sorgulamak uygulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="37e5e-138">Doing so enables the app to query the Graph API for users.</span></span>

## <a name="step-2-install-and-configure-adal"></a><span data-ttu-id="37e5e-139">2. adım: Yükleme ve ADAL yapılandırma</span><span class="sxs-lookup"><span data-stu-id="37e5e-139">Step 2: Install and configure ADAL</span></span>
<span data-ttu-id="37e5e-140">Azure AD'de bir uygulamaya sahip olduğunuza göre ADAL yükleyin ve kimlikle ilgili kodunuzu yazın.</span><span class="sxs-lookup"><span data-stu-id="37e5e-140">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="37e5e-141">Azure AD ile iletişim kurmak ADAL etkinleştirmek için uygulama kaydı hakkında bazı bilgileri verin.</span><span class="sxs-lookup"><span data-stu-id="37e5e-141">To enable ADAL to communicate with Azure AD, give it some information about the app registration.</span></span>

1. <span data-ttu-id="37e5e-142">ADAL Paket Yöneticisi konsolu kullanılarak DirectorySearcher projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="37e5e-142">Add ADAL to the DirectorySearcher project by using the Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. <span data-ttu-id="37e5e-143">DirectorySearcher projesinde MainPage.xaml.cs açın.</span><span class="sxs-lookup"><span data-stu-id="37e5e-143">In the DirectorySearcher project, open MainPage.xaml.cs.</span></span>
3. <span data-ttu-id="37e5e-144">Değerleri değiştirin **yapılandırma değerleri** Azure portalında girdiğiniz değerleri bölgesiyle.</span><span class="sxs-lookup"><span data-stu-id="37e5e-144">Replace the values in the **Config Values** region with the values that you entered in the Azure portal.</span></span> <span data-ttu-id="37e5e-145">ADAL kullandığında kodunuzu bu değerleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="37e5e-145">Your code refers to these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="37e5e-146">*Kiracı* Azure AD kiracınız (örneğin, contoso.onmicrosoft.com) etki alanıdır.</span><span class="sxs-lookup"><span data-stu-id="37e5e-146">The *tenant* is the domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="37e5e-147">*ClientID* portalından kopyalandığından uygulama istemci Kimliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="37e5e-147">The *clientId* is the client ID of the app, which you copied from the portal.</span></span>
4. <span data-ttu-id="37e5e-148">Artık Windows mağazası uygulamanız için geri çağırma URI bulmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="37e5e-148">You now need to discover the callback URI for your Windows Store app.</span></span> <span data-ttu-id="37e5e-149">Bu satırında bir kesme noktası belirleyerek `MainPage` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="37e5e-149">Set a breakpoint on this line in the `MainPage` method:</span></span>
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. <span data-ttu-id="37e5e-150">Çözüm derleme, tüm başvuruları paket emin olarak geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="37e5e-150">Build the solution, making sure that all package references are restored.</span></span> <span data-ttu-id="37e5e-151">Herhangi bir paket eksikse, NuGet Paket Yöneticisi'ni açın ve bunları geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="37e5e-151">If any packages are missing, open the NuGet Package Manager and restore them.</span></span>
6. <span data-ttu-id="37e5e-152">Uygulamayı çalıştırın ve değerini kopyalayın `redirectUri` zaman kesme noktası isabet.</span><span class="sxs-lookup"><span data-stu-id="37e5e-152">Run the app, and copy the value of `redirectUri` when the breakpoint is hit.</span></span> <span data-ttu-id="37e5e-153">Değer aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="37e5e-153">The value should look something like the following:</span></span>

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. <span data-ttu-id="37e5e-154">Geri **ayarları** sekmesi Azure portalında uygulama ekleme bir **RedirectUri** önceki değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="37e5e-154">Back on the **Settings** tab of the app in the Azure portal, add a **RedirectUri** with the preceding value.</span></span>  

## <a name="step-3-use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="37e5e-155">3. adım: Kullanım Azure AD'den belirteçleri almak için ADAL</span><span class="sxs-lookup"><span data-stu-id="37e5e-155">Step 3: Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="37e5e-156">Temel ADAL arkasında uygulamanın bir erişim belirteci ihtiyacı olduğunda, onu yalnızca çağırdığı ilkesidir `authContext.AcquireToken(…)`, ve ADAL rest yapar.</span><span class="sxs-lookup"><span data-stu-id="37e5e-156">The basic principle behind ADAL is that whenever the app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span></span>  

1. <span data-ttu-id="37e5e-157">Uygulamanın başlatma `AuthenticationContext`, ADAL birincil sınıfının olduğu.</span><span class="sxs-lookup"><span data-stu-id="37e5e-157">Initialize the app’s `AuthenticationContext`, which is the primary class of ADAL.</span></span> <span data-ttu-id="37e5e-158">Bu eylem ADAL geçirir gereken Azure AD ile iletişim kurmasını ve onu nasıl belirteçleri önbelleğe söyleyin koordinatları.</span><span class="sxs-lookup"><span data-stu-id="37e5e-158">This action passes ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. <span data-ttu-id="37e5e-159">Bulun `Search(...)` kullanıcılar'ı tıklattığınızda, çağrılan yöntem **arama** uygulamanın UI düğmesinde.</span><span class="sxs-lookup"><span data-stu-id="37e5e-159">Locate the `Search(...)` method, which is invoked when users click the **Search** button on the app's UI.</span></span> <span data-ttu-id="37e5e-160">Bu yöntem, UPN verilen arama terimiyle kullanıcıları için Azure AD Graph API sorgu için bir get isteği yapar.</span><span class="sxs-lookup"><span data-stu-id="37e5e-160">This method makes a get request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span> <span data-ttu-id="37e5e-161">Grafik API'si sorgulamak için bir erişim belirteci isteğin içinde dahil **yetkilendirme** üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="37e5e-161">To query the Graph API, include an access token in the request's **Authorization** header.</span></span> <span data-ttu-id="37e5e-162">ADAL nereden geldiğini budur.</span><span class="sxs-lookup"><span data-stu-id="37e5e-162">This is where ADAL comes in.</span></span>

    ```C#
    private async void Search(object sender, RoutedEventArgs e)
    {
        ...
        AuthenticationResult result = null;
        try
        {
            result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectURI, new PlatformParameters(PromptBehavior.Auto, false));
        }
        catch (AdalException ex)
        {
            if (ex.ErrorCode != "authentication_canceled")
            {
                ShowAuthError(string.Format("If the error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    <span data-ttu-id="37e5e-163">Uygulama isteğinde bulunduğunda bir belirteç çağırarak `AcquireTokenAsync(...)`, ADAL kullanıcı kimlik bilgilerinin sorulmasına olmadan bir simge döndürür dener.</span><span class="sxs-lookup"><span data-stu-id="37e5e-163">When the app requests a token by calling `AcquireTokenAsync(...)`, ADAL attempts to return a token without asking the user for credentials.</span></span> <span data-ttu-id="37e5e-164">ADAL kullanıcı bir belirteç almak üzere oturum açmak gerektiğini belirlerse, bir oturum açma iletişim kutusu görüntüler, kullanıcının kimlik bilgilerini toplar ve kimlik doğrulaması başarılı olduktan sonra bir belirteç döndürür.</span><span class="sxs-lookup"><span data-stu-id="37e5e-164">If ADAL determines that the user needs to sign in to get a token, it displays a sign-in dialog box, collects the user's credentials, and returns a token after authentication succeeds.</span></span> <span data-ttu-id="37e5e-165">ADAL herhangi bir nedenle bir belirteç döndüremedi ise *yazılımdan AuthenticationResult* bir hata durumudur.</span><span class="sxs-lookup"><span data-stu-id="37e5e-165">If ADAL is unable to return a token for any reason, the *AuthenticationResult* status is an error.</span></span>
3. <span data-ttu-id="37e5e-166">Artık yalnızca aldığınız erişim belirtecini kullanmak için zaman yapılır.</span><span class="sxs-lookup"><span data-stu-id="37e5e-166">Now it's time to use the access token you just acquired.</span></span> <span data-ttu-id="37e5e-167">Ayrıca, `Search(...)` yöntemi, grafik API'si get isteğine belirteç ekleme **yetkilendirme** üstbilgisi:</span><span class="sxs-lookup"><span data-stu-id="37e5e-167">Also in the `Search(...)` method, attach the token to the Graph API get request in the **Authorization** header:</span></span>

    ```C#
    // Add the access token to the Authorization header of the call to the Graph API, and call the Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. <span data-ttu-id="37e5e-168">Kullanabileceğiniz `AuthenticationResult` nesnesi kullanıcının kimliği gibi uygulama kullanıcı hakkındaki bilgileri görüntülemek için:</span><span class="sxs-lookup"><span data-stu-id="37e5e-168">You can use the `AuthenticationResult` object to display information about the user in the app, such as the user's ID:</span></span>

    ```C#
    // Update the page UI to represent the signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. <span data-ttu-id="37e5e-169">ADAL, kullanıcılar uygulama dışında imzalamak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37e5e-169">You can also use ADAL to sign users out of the app.</span></span> <span data-ttu-id="37e5e-170">Kullanıcı tıkladığında **oturum kapatma** düğmesini tıklatın, sonraki çağrısı emin `AcquireTokenAsync(...)` bir oturum açma görünümü gösterir.</span><span class="sxs-lookup"><span data-stu-id="37e5e-170">When the user clicks the **Sign Out** button, ensure that the next call to `AcquireTokenAsync(...)` shows a sign-in view.</span></span> <span data-ttu-id="37e5e-171">ADAL ile bu eylem belirteç önbelleği temizleme olarak kadar kolaydır:</span><span class="sxs-lookup"><span data-stu-id="37e5e-171">With ADAL, this action is as easy as clearing the token cache:</span></span>

    ```C#
    private void SignOut()
    {
        // Clear session state from the token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a><span data-ttu-id="37e5e-172">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="37e5e-172">What's next</span></span>
<span data-ttu-id="37e5e-173">Artık çalışan bir kullanıcıların kimlik doğrulaması, güvenli bir şekilde web OAuth 2.0 kullanan API'leri çağırmak ve kullanıcı hakkındaki temel bilgileri elde Windows mağazası uygulaması sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="37e5e-173">You now have a working Windows Store app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about the user.</span></span>

<span data-ttu-id="37e5e-174">Kiracı kullanıcılarla zaten doldurulmuş yapmadıysanız, bunu yapmak için gereken süre sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="37e5e-174">If you haven’t already populated your tenant with users, now is the time to do so.</span></span>
1. <span data-ttu-id="37e5e-175">DirectorySearcher uygulamanızı çalıştırın ve ardından kullanıcılardan birine oturum açın.</span><span class="sxs-lookup"><span data-stu-id="37e5e-175">Run your DirectorySearcher app, and then sign in with one of the users.</span></span>
2. <span data-ttu-id="37e5e-176">Diğer kullanıcıların UPN Değerlerinin üzerinde göre arayın.</span><span class="sxs-lookup"><span data-stu-id="37e5e-176">Search for other users based on their UPN.</span></span>
3. <span data-ttu-id="37e5e-177">Uygulamayı kapatın ve onu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="37e5e-177">Close the app, and rerun it.</span></span> <span data-ttu-id="37e5e-178">Kullanıcının oturumunu nasıl olduğu gibi kalır dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="37e5e-178">Notice how the user’s session remains intact.</span></span>
4. <span data-ttu-id="37e5e-179">Sağ tıklayarak alt çubukta görüntülemek için oturumu kapatın ve ardından başka bir kullanıcı olarak yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="37e5e-179">Sign out by right-clicking to display the bottom bar, and then sign back in as another user.</span></span>

<span data-ttu-id="37e5e-180">ADAL, bir uygulamaya bu ortak kimlik özelliklerin tümü eklemenizi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="37e5e-180">ADAL makes it easy to incorporate all these common identity features into the app.</span></span> <span data-ttu-id="37e5e-181">Bu tüm dirty iş sizin için önbellek yönetimi gibi OAuth protokol desteği, kullanıcı bir oturum açma kullanıcı Arabirimi, sunan mvc'deki ve yenileme belirteçleri süresi.</span><span class="sxs-lookup"><span data-stu-id="37e5e-181">It takes care of all the dirty work for you, such as cache management, OAuth protocol support, presenting the user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="37e5e-182">Tek bir API çağrısı yalnızca, bilmeniz gereken `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="37e5e-182">You need to know only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="37e5e-183">Başvuru için karşıdan [tamamlanan örnek](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (yapılandırma değerleriniz olmadan).</span><span class="sxs-lookup"><span data-stu-id="37e5e-183">For reference, download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="37e5e-184">Artık ek kimlik senaryolara geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37e5e-184">You can now move on to additional identity scenarios.</span></span> <span data-ttu-id="37e5e-185">Örneğin, [Azure AD ile .NET Web API'si güvenli](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="37e5e-185">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
