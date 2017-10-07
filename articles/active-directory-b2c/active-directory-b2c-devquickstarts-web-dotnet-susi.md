---
title: Active Directory B2C aaaAzure | Microsoft Docs
description: "Nasıl toobuild oturumu-up/oturum açma, sahip bir web uygulaması düzenleme ve parola sıfırlama ve Azure Active Directory B2C kullanarak profil."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: barbaraselden
ms.assetid: 30261336-d7a5-4a6d-8c1a-7943ad76ed25
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 187f99a8dd50d212de4f0517f552cdbbe5a8edf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a><span data-ttu-id="4d074-103">Azure Active Directory B2C kaydolma, oturum açma profili düzenleme ve parola sıfırlama ile bir ASP.NET web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="4d074-103">Create an ASP.NET web app with Azure Active Directory B2C sign-up, sign-in, profile edit, and password reset</span></span>

<span data-ttu-id="4d074-104">Bu öğretici şunların nasıl yapıldığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="4d074-104">This tutorial shows you how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4d074-105">Azure AD B2C kimlik özellikleri tooyour web uygulaması Ekle</span><span class="sxs-lookup"><span data-stu-id="4d074-105">Add Azure AD B2C identity features tooyour web app</span></span>
> * <span data-ttu-id="4d074-106">Azure AD B2C dizininizde web uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="4d074-106">Register your web app in your Azure AD B2C directory</span></span>
> * <span data-ttu-id="4d074-107">Kullanıcı oturumu-up/oturum açma, profil düzenleme ve web uygulamanız için parola sıfırlama ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4d074-107">Create a user sign-up/sign-in, profile edit, and password reset policy for your web app</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d074-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4d074-108">Prerequisites</span></span>

- <span data-ttu-id="4d074-109">Azure hesabı, B2C Kiracı tooan bağlanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d074-109">You must connect your B2C Tenant tooan Azure account.</span></span> <span data-ttu-id="4d074-110">Ücretsiz bir Azure hesabı oluşturabilirsiniz [burada](https://azure.microsoft.com/en-us/).</span><span class="sxs-lookup"><span data-stu-id="4d074-110">You can create a free Azure account [here](https://azure.microsoft.com/en-us/).</span></span>
- <span data-ttu-id="4d074-111">Gereksinim duyduğunuz [Microsoft Visual Studio](https://www.visualstudio.com/) veya benzeri program tooview ve hello örnek kodu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4d074-111">You need [Microsoft Visual Studio](https://www.visualstudio.com/) or a similar program tooview and modify hello sample code.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="4d074-112">Azure AD B2C dizini oluşturma</span><span class="sxs-lookup"><span data-stu-id="4d074-112">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="4d074-113">Azure AD B2C'yi kullanabilmek için önce dizin veya kiracı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d074-113">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="4d074-114">Bir dizin, tüm kullanıcıların, uygulamaları, grupları ve daha fazlası için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="4d074-114">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="4d074-115">Zaten yoksa, bu kılavuza devam etmeden önce bir B2C dizini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4d074-115">If you don't have one already, create a B2C directory before you continue in this guide.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> <span data-ttu-id="4d074-116">Tooconnect hello B2C Kiracı tooyour Azure aboneliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d074-116">You need tooconnect hello B2C Tenant tooyour Azure subscription.</span></span> <span data-ttu-id="4d074-117">Seçtikten sonra **oluşturma**seçin hello **bağlantı var olan bir Azure AD B2C Kiracı toomy Azure aboneliği** seçeneğini ve ardından hello **Azure AD B2C Kiracısı** açılan, seçin Merhaba Kiracı tooassociate istiyor.</span><span class="sxs-lookup"><span data-stu-id="4d074-117">After selecting **Create**, select hello **Link an existing Azure AD B2C Tenant toomy Azure subscription** option, and then in hello **Azure AD B2C Tenant** drop down, select hello tenant you want tooassociate.</span></span>

## <a name="create-and-register-an-application"></a><span data-ttu-id="4d074-118">Oluşturma ve bir uygulamayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="4d074-118">Create and register an application</span></span>

<span data-ttu-id="4d074-119">Ardından, toocreate gerekir ve B2C dizininizde hello uygulama kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4d074-119">Next, you need toocreate and register hello app in your B2C directory.</span></span> <span data-ttu-id="4d074-120">Bu Azure AD B2C toosecurely gereken bilgileri sağlar uygulamanız ile iletişim kurması.</span><span class="sxs-lookup"><span data-stu-id="4d074-120">This provides information that Azure AD B2C needs toosecurely communicate with your app.</span></span> 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

<span data-ttu-id="4d074-121">İşiniz bittiğinde, uygulamanızın ayarlarını bir API ve yerel bir uygulamaya gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d074-121">When you are done, you will have both an API and a native application in your application settings.</span></span>

## <a name="create-policies-on-your-b2c-tenant"></a><span data-ttu-id="4d074-122">B2C kiracınızın ilkeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="4d074-122">Create policies on your B2C tenant</span></span>

<span data-ttu-id="4d074-123">Azure AD B2C'de her kullanıcı deneyimi, bir [ilke](active-directory-b2c-reference-policies.md) ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="4d074-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="4d074-124">Bu kod örneği üç kimlik deneyimi içerir: **kaydolma ve oturum açma**, **düzenleme profil**, ve **parola sıfırlama**.</span><span class="sxs-lookup"><span data-stu-id="4d074-124">This code sample contains three identity experiences: **sign-up & sign-in**, **profile edit**, and **password reset**.</span></span>  <span data-ttu-id="4d074-125">Hello açıklandığı gibi her tür bir ilke toocreate gerek [ilke başvurusu makalesinde](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="4d074-125">You need toocreate one policy of each type, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="4d074-126">Her ilke için tooselect hello görünen adı özniteliği veya talep ve daha sonra kullanmak için hello ad ilkenizin aşağı toocopy emin olun.</span><span class="sxs-lookup"><span data-stu-id="4d074-126">For each policy, be sure tooselect hello Display name attribute or claim, and toocopy down hello name of your policy for later use.</span></span>

### <a name="add-your-identity-providers"></a><span data-ttu-id="4d074-127">Kimlik sağlayıcısı ekleyin</span><span class="sxs-lookup"><span data-stu-id="4d074-127">Add your identity providers</span></span>

<span data-ttu-id="4d074-128">Ayarlarınızı seçin **kimlik sağlayıcıları** ve kullanıcı adı kayıt ya da e-posta'i seçin.</span><span class="sxs-lookup"><span data-stu-id="4d074-128">From your settings, select **Identity Providers** and choose Username signup or Email signup.</span></span>

### <a name="create-a-sign-up-and-sign-in-policy"></a><span data-ttu-id="4d074-129">Kaydolma ve oturum açma ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4d074-129">Create a sign-up and sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a><span data-ttu-id="4d074-130">İlke düzenleme profil oluşturma</span><span class="sxs-lookup"><span data-stu-id="4d074-130">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a><span data-ttu-id="4d074-131">Bir parola sıfırlama ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4d074-131">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

<span data-ttu-id="4d074-132">İlkelerinizi oluşturduktan sonra hazır toobuild olduğunuz uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="4d074-132">After you create your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="4d074-133">Merhaba örnek kodu indirin</span><span class="sxs-lookup"><span data-stu-id="4d074-133">Download hello sample code</span></span>

<span data-ttu-id="4d074-134">Bu öğretici için kod Hello korunduğu [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="4d074-134">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="4d074-135">Çalıştırarak hello örnek kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4d074-135">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="4d074-136">Merhaba örnek kodu indirdikten sonra açık hello Visual Studio .sln dosyasını tooget başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="4d074-136">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="4d074-137">Merhaba çözüm dosyası iki proje içerir: `TaskWebApp` ve `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="4d074-137">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="4d074-138">`TaskWebApp`Merhaba kullanıcı hello MVC web uygulaması ile etkileşime giren olur.</span><span class="sxs-lookup"><span data-stu-id="4d074-138">`TaskWebApp` is hello MVC web application that hello user interacts with.</span></span> <span data-ttu-id="4d074-139">`TaskService`her kullanıcının yapılacaklar listesini depolayan hello uygulamanızın arka uç web API'dır.</span><span class="sxs-lookup"><span data-stu-id="4d074-139">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="4d074-140">Bu makalede yalnızca hello ele alınacaktır `TaskWebApp` uygulama.</span><span class="sxs-lookup"><span data-stu-id="4d074-140">This article will only discuss hello `TaskWebApp` application.</span></span> <span data-ttu-id="4d074-141">toolearn nasıl toobuild `TaskService` Azure AD B2C kullanarak bkz [.NET web API'si öğreticimizi](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="4d074-141">toolearn how toobuild `TaskService` using Azure AD B2C, see [our .NET web api tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="update-code-toouse-your-tenant-and-policies"></a><span data-ttu-id="4d074-142">Kiracı ve ilkeleri kod toouse güncelleştir</span><span class="sxs-lookup"><span data-stu-id="4d074-142">Update code toouse your tenant and policies</span></span>

<span data-ttu-id="4d074-143">Bizim örnek yapılandırılmış toouse hello ilkeleri ve istemci bizim demo Kiracı kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="4d074-143">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="4d074-144">tooconnect, tooyour kendi Kiracı tooopen gerek `web.config` hello içinde `TaskWebApp` proje ve değerleri aşağıdaki hello değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4d074-144">tooconnect it tooyour own tenant, you need tooopen `web.config` in hello `TaskWebApp` project and replace hello following values:</span></span>

* <span data-ttu-id="4d074-145">kiracı adınızla `ida:Tenant`</span><span class="sxs-lookup"><span data-stu-id="4d074-145">`ida:Tenant` with your tenant name</span></span>
* <span data-ttu-id="4d074-146">Web uygulamanızın kimliği ile `ida:ClientId`</span><span class="sxs-lookup"><span data-stu-id="4d074-146">`ida:ClientId` with your web app application ID</span></span>
* <span data-ttu-id="4d074-147">Web uygulamanızın gizli anahtarı ile `ida:ClientSecret`</span><span class="sxs-lookup"><span data-stu-id="4d074-147">`ida:ClientSecret` with your web app secret key</span></span>
* <span data-ttu-id="4d074-148">"Kaydolma veya Oturum açma" ilkenizin adıyla `ida:SignUpSignInPolicyId`</span><span class="sxs-lookup"><span data-stu-id="4d074-148">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
* <span data-ttu-id="4d074-149">"Profil Düzenleme" ilkenizin adıyla `ida:EditProfilePolicyId`</span><span class="sxs-lookup"><span data-stu-id="4d074-149">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
* <span data-ttu-id="4d074-150">"Parola Sıfırlama" ilkenizin adıyla `ida:ResetPasswordPolicyId`</span><span class="sxs-lookup"><span data-stu-id="4d074-150">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>

## <a name="launch-hello-app"></a><span data-ttu-id="4d074-151">Merhaba uygulamasını başlatın</span><span class="sxs-lookup"><span data-stu-id="4d074-151">Launch hello app</span></span>
<span data-ttu-id="4d074-152">Gelen Visual Studio içinde hello uygulamasını başlatın.</span><span class="sxs-lookup"><span data-stu-id="4d074-152">From within Visual Studio, launch hello app.</span></span> <span data-ttu-id="4d074-153">Toohello Yapılacaklar listesi sekmesi ve URL Not hello gidin: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*& client_id = *YourclientID*...</span><span class="sxs-lookup"><span data-stu-id="4d074-153">Navigate toohello To-Do List tab, and note hello URl is: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.....</span></span>

<span data-ttu-id="4d074-154">E-posta adresi veya kullanıcı adı kullanarak Hello uygulaması için kaydolun.</span><span class="sxs-lookup"><span data-stu-id="4d074-154">Sign up for hello app by using your email address or user name.</span></span> <span data-ttu-id="4d074-155">Çıkışı, oturum daha sonra yeniden oturum açın ve hello profili düzenlemek veya hello parola sıfırlama.</span><span class="sxs-lookup"><span data-stu-id="4d074-155">Sign out, then sign in again and edit hello profile or reset hello password.</span></span> <span data-ttu-id="4d074-156">Oturumu kapatın ve farklı bir kullanıcı olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4d074-156">Sign out and sign in as a different user.</span></span> 

## <a name="add-social-idps"></a><span data-ttu-id="4d074-157">Sosyal IDPs Ekle</span><span class="sxs-lookup"><span data-stu-id="4d074-157">Add social IDPs</span></span>

<span data-ttu-id="4d074-158">Şu anda kullanarak yalnızca kullanıcı kaydolma ve oturum açma'de hello uygulama'yı destekler **yerel hesaplar**; B2C dizininizde depolanan hesapları, bir kullanıcı adı ve parola kullanın.</span><span class="sxs-lookup"><span data-stu-id="4d074-158">Currently, hello app supports only user sign-up and sign-in by using **local accounts**; accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="4d074-159">Azure AD B2C kullanarak diğer için destek ekleyebilmesi **kimlik sağlayıcıları** (IDPs) herhangi birini kodunuzu değiştirmeden.</span><span class="sxs-lookup"><span data-stu-id="4d074-159">By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="4d074-160">tooadd sosyal IDPs tooyour uygulama, izleyerek başlamak hello ayrıntılı yönergeler bu makalelerde.</span><span class="sxs-lookup"><span data-stu-id="4d074-160">tooadd social IDPs tooyour app, begin by following hello detailed instructions in these articles.</span></span> <span data-ttu-id="4d074-161">Her IDP için toosupport istediğiniz, bu sistemde tooregister uygulamanın gerekir ve bir istemci kimliği alın</span><span class="sxs-lookup"><span data-stu-id="4d074-161">For each IDP you want toosupport, you need tooregister an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="4d074-162">Facebook bir IDP ayarlayın</span><span class="sxs-lookup"><span data-stu-id="4d074-162">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="4d074-163">Google bir IDP ayarlayın</span><span class="sxs-lookup"><span data-stu-id="4d074-163">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="4d074-164">Amazon bir IDP ayarlayın</span><span class="sxs-lookup"><span data-stu-id="4d074-164">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="4d074-165">LinkedIn bir IDP ayarlayın</span><span class="sxs-lookup"><span data-stu-id="4d074-165">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="4d074-166">Eklediğiniz sonra hello kimlik sağlayıcıları tooyour B2C dizini, düzenlemesini her üç ilke tooinclude hello açıklandığı gibi yeni IDPs hello [ilke başvurusu makalesinde](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="4d074-166">After you add hello identity providers tooyour B2C directory, edit each of your three policies tooinclude hello new IDPs, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="4d074-167">İlkelerinizi kaydettikten sonra hello uygulamayı yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4d074-167">After you save your policies, run hello app again.</span></span>  <span data-ttu-id="4d074-168">Oturum açma ve kaydolma seçenekleri her kimlik deneyimlerinizi yeni IDPs eklenen hello görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d074-168">You should see hello new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="4d074-169">İlkelerinizle denemeler ve örnek uygulamanızı hello etkisi gözlemleyin.</span><span class="sxs-lookup"><span data-stu-id="4d074-169">You can experiment with your policies and observe hello effect on your sample app.</span></span> <span data-ttu-id="4d074-170">Ekleyebilir veya IDPs kaldırmak, uygulamanın talep değiştirmek veya kaydolma özniteliklerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d074-170">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="4d074-171">İlkeleri ve kimlik doğrulama isteklerini OWIN nasıl birbirine bağlayan görene kadar deneyin.</span><span class="sxs-lookup"><span data-stu-id="4d074-171">Experiment until you can see how policies, authentication requests, and OWIN tie together.</span></span>

## <a name="sample-code-walkthrough"></a><span data-ttu-id="4d074-172">Örnek kod gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="4d074-172">Sample code walkthrough</span></span>
<span data-ttu-id="4d074-173">Aşağıdaki bölümlerde hello hello örnek uygulama kodu nasıl yapılandırıldığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="4d074-173">hello following sections show you how hello sample application code is configured.</span></span> <span data-ttu-id="4d074-174">Bu kılavuz olarak gelecekte uygulama geliştirmede kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="4d074-174">You may use this as a guide in your future app development.</span></span>

### <a name="add-authentication-support"></a><span data-ttu-id="4d074-175">Kimlik doğrulama desteği ekleme</span><span class="sxs-lookup"><span data-stu-id="4d074-175">Add authentication support</span></span>

<span data-ttu-id="4d074-176">Artık, uygulama toouse Azure AD B2C yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d074-176">You can now configure your app toouse Azure AD B2C.</span></span> <span data-ttu-id="4d074-177">Uygulamanız, Openıd Connect kimlik doğrulama istekleri göndererek Azure AD B2C ile iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="4d074-177">Your app communicates with Azure AD B2C by sending OpenID Connect authentication requests.</span></span> <span data-ttu-id="4d074-178">Merhaba istekleri dikte hello kullanıcı deneyimi hello İlkesi belirterek tooexecute uygulamanızı istemektedir.</span><span class="sxs-lookup"><span data-stu-id="4d074-178">hello requests dictate hello user experience your app wants tooexecute by specifying hello policy.</span></span> <span data-ttu-id="4d074-179">Bu istekleri Microsoft'un OWIN kitaplığı toosend kullanın, ilkeleri yürütmek, kullanıcı oturumları ve daha fazlasını yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d074-179">You can use Microsoft's OWIN library toosend these requests, execute policies, manage user sessions, and more.</span></span>

#### <a name="install-owin"></a><span data-ttu-id="4d074-180">OWIN yükleme</span><span class="sxs-lookup"><span data-stu-id="4d074-180">Install OWIN</span></span>

<span data-ttu-id="4d074-181">toobegin, hello Visual Studio Paket Yöneticisi konsolu kullanarak hello OWIN ara yazılımı NuGet paketleri toohello projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4d074-181">toobegin, add hello OWIN middleware NuGet packages toohello project by using hello Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a><span data-ttu-id="4d074-182">OWIN başlangıç sınıfı ekleme</span><span class="sxs-lookup"><span data-stu-id="4d074-182">Add an OWIN startup class</span></span>

<span data-ttu-id="4d074-183">Bir OWIN başlangıç sınıfı toohello API adlı eklemek `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="4d074-183">Add an OWIN startup class toohello API called `Startup.cs`.</span></span>  <span data-ttu-id="4d074-184">Merhaba projede, select sağ **Ekle** ve **yeni öğe**ve ardından OWIN'i aratın.</span><span class="sxs-lookup"><span data-stu-id="4d074-184">Right-click on hello project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="4d074-185">Merhaba OWIN ara yazılımı hello çağırılır `Configuration(…)` uygulamanız başladığında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="4d074-185">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="4d074-186">Örneğimizde, biz hello sınıf bildirimi çok değiştirilen`public partial class Startup` ve uygulanan diğer hello sınıfında parçası hello `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="4d074-186">In our sample, we changed hello class declaration too`public partial class Startup` and implemented hello other part of hello class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="4d074-187">İç hello `Configuration` yöntemi, bir çağrı çok eklediğimiz`ConfigureAuth`, içinde tanımlanan `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="4d074-187">Inside hello `Configuration` method, we added a call too`ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="4d074-188">Merhaba değişiklikler sonra `Startup.cs` hello aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="4d074-188">After hello modifications, `Startup.cs` looks like hello following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-hello-authentication-middleware"></a><span data-ttu-id="4d074-189">Merhaba kimlik doğrulaması ara yazılımını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4d074-189">Configure hello authentication middleware</span></span>

<span data-ttu-id="4d074-190">Açık hello dosya `App_Start\Startup.Auth.cs` ve hello uygulamak `ConfigureAuth(...)` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="4d074-190">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="4d074-191">Merhaba, sağladığınız parametreler `OpenIdConnectAuthenticationOptions` , uygulama toocommunicate Azure AD B2C ile koordinatları olarak hizmet.</span><span class="sxs-lookup"><span data-stu-id="4d074-191">hello parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="4d074-192">Belirli parametreleri belirtmezseniz hello varsayılan değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="4d074-192">If you do not specify certain parameters, it will use hello default value.</span></span> <span data-ttu-id="4d074-193">Örneğin, biz hello belirtmeyin `ResponseType` hello örneğinde, böylece varsayılan değer hello `code id_token` her giden istek tooAzure AD B2C kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="4d074-193">For example, we do not specify hello `ResponseType` in hello sample, so hello default value `code id_token` will be used in each outgoing request tooAzure AD B2C.</span></span>

<span data-ttu-id="4d074-194">Tanımlama bilgisi kimlik doğrulamasını oluşturan tooset de gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d074-194">You also need tooset up cookie authentication.</span></span> <span data-ttu-id="4d074-195">Merhaba Openıd Connect ara yazılım tanımlama bilgilerini toomaintain kullanıcı oturumları, başka şeylerin kullanır.</span><span class="sxs-lookup"><span data-stu-id="4d074-195">hello OpenID Connect middleware uses cookies toomaintain user sessions, among other things.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure hello OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate hello metadata address using hello tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify hello callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify hello claims toovalidate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement hello "Notification" methods...
}
```

<span data-ttu-id="4d074-196">İçinde `OpenIdConnectAuthenticationOptions` geri çağırma işlevleri hello ara yazılımı Openıd Connect tarafından alınan belirli bildirimleri için bir dizi yukarıdaki tanımlarız.</span><span class="sxs-lookup"><span data-stu-id="4d074-196">In `OpenIdConnectAuthenticationOptions` above, we define a set of callback functions for specific notifications that are received by hello OpenID Connect middleware.</span></span> <span data-ttu-id="4d074-197">Bu davranışların kullanarak tanımlanan bir `OpenIdConnectAuthenticationNotifications` nesne ve hello depolanmış `Notifications` değişkeni.</span><span class="sxs-lookup"><span data-stu-id="4d074-197">These behaviors are defined using a `OpenIdConnectAuthenticationNotifications` object and stored into hello `Notifications` variable.</span></span> <span data-ttu-id="4d074-198">Örneğimizde, biz hello olay bağlı olarak üç farklı geri aramalar tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="4d074-198">In our sample, we define three different callbacks depending on hello event.</span></span>

### <a name="using-different-policies"></a><span data-ttu-id="4d074-199">Farklı ilkelerini kullanma</span><span class="sxs-lookup"><span data-stu-id="4d074-199">Using different policies</span></span>

<span data-ttu-id="4d074-200">Merhaba `RedirectToIdentityProvider` bildirim tooAzure AD B2C bir istek yapıldığında tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="4d074-200">hello `RedirectToIdentityProvider` notification is triggered whenever a request is made tooAzure AD B2C.</span></span> <span data-ttu-id="4d074-201">Merhaba geri arama işlevinde `OnRedirectToIdentityProvider`, biz toouse istiyoruz, çağrı giden hello başka bir ilke kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="4d074-201">In hello callback function `OnRedirectToIdentityProvider`, we check in hello outgoing call if we want toouse a different policy.</span></span> <span data-ttu-id="4d074-202">İlke hello varsayılan "Kaydolma veya oturum açma" ilke yerine Hello parola sıfırlama gibi bir parola sıfırlama veya bir profili düzenlemek sipariş toodo içinde toouse hello ilgili ilkeyi gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d074-202">In order toodo a password reset or edit a profile, you need toouse hello corresponding policy such as hello password reset policy instead of hello default "Sign-up or Sign-in" policy.</span></span>

<span data-ttu-id="4d074-203">Bir kullanıcı tooreset hello parola istediği veya hello profili düzenlediğinizde Örneğimizde, biz biz toouse hello OWIN bağlamına tercih hello ilkesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4d074-203">In our sample, when a user wants tooreset hello password or edit hello profile, we add hello policy we prefer toouse into hello OWIN context.</span></span> <span data-ttu-id="4d074-204">Hello aşağıdakileri yaparak yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="4d074-204">That can be done by doing hello following:</span></span>

```CSharp
    // Let hello middleware know you are trying toouse hello edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

<span data-ttu-id="4d074-205">Ve hello geri çağırma işlevi uygulayabilirsiniz `OnRedirectToIdentityProvider` hello aşağıdakileri yaparak:</span><span class="sxs-lookup"><span data-stu-id="4d074-205">And you can implement hello callback function `OnRedirectToIdentityProvider` by doing hello following:</span></span>

```CSharp
/*
*  On each call tooAzure AD B2C, check if a policy (e.g. hello profile edit or password reset policy) has been specified in hello OWIN context.
*  If so, use that policy when making hello call. Also, don't request a code (since it won't be needed).
*/
private Task OnRedirectToIdentityProvider(RedirectToIdentityProviderNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    var policy = notification.OwinContext.Get<string>("Policy");

    if (!string.IsNullOrEmpty(policy) && !policy.Equals(DefaultPolicy))
    {
        notification.ProtocolMessage.Scope = OpenIdConnectScopes.OpenId;
        notification.ProtocolMessage.ResponseType = OpenIdConnectResponseTypes.IdToken;
        notification.ProtocolMessage.IssuerAddress = notification.ProtocolMessage.IssuerAddress.Replace(DefaultPolicy, policy);
    }

    return Task.FromResult(0);
}
```

### <a name="handling-authorization-codes"></a><span data-ttu-id="4d074-206">Yetkilendirme kodları işleme</span><span class="sxs-lookup"><span data-stu-id="4d074-206">Handling authorization codes</span></span>

<span data-ttu-id="4d074-207">Merhaba `AuthorizationCodeReceived` bildirim bir yetkilendirme kodu alındığında tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="4d074-207">hello `AuthorizationCodeReceived` notification is triggered when an authorization code is received.</span></span> <span data-ttu-id="4d074-208">Merhaba Openıd Connect Ara değiş tokuşu kodları için erişim belirteçleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="4d074-208">hello OpenID Connect middleware does not support exchanging codes for access tokens.</span></span> <span data-ttu-id="4d074-209">Bir geri çağırma işlevini hello belirteçte hello kodunu el ile değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="4d074-209">You can manually exchange hello code for hello token in a callback function.</span></span> <span data-ttu-id="4d074-210">Daha fazla bilgi için lütfen hello bakın [belgelerine](active-directory-b2c-devquickstarts-web-api-dotnet.md) , açıklar nasıl.</span><span class="sxs-lookup"><span data-stu-id="4d074-210">For more information, please look at hello [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) that explains how.</span></span>

### <a name="handling-errors"></a><span data-ttu-id="4d074-211">Hataları işleme</span><span class="sxs-lookup"><span data-stu-id="4d074-211">Handling errors</span></span>

<span data-ttu-id="4d074-212">Merhaba `AuthenticationFailed` bildirim kimlik doğrulama başarısız olduğunda tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="4d074-212">hello `AuthenticationFailed` notification is triggered when authentication fails.</span></span> <span data-ttu-id="4d074-213">İstediğiniz gibi kendi geri çağırma yönteminde hello hataları işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="4d074-213">In its callback method, you can handle hello errors as you wish.</span></span> <span data-ttu-id="4d074-214">Merhaba hata kodunu denetle ancak eklemelisiniz `AADB2C90118`.</span><span class="sxs-lookup"><span data-stu-id="4d074-214">You should however add a check for hello error code `AADB2C90118`.</span></span> <span data-ttu-id="4d074-215">Merhaba "Kaydolma veya oturum açma" ilke Hello yürütülmesi sırasında hello kullanıcının hello fırsat tooselect sahip bir **parolanızı mı unuttunuz?** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="4d074-215">During hello execution of hello "Sign-up or Sign-in" policy, hello user has hello opportunity tooselect a **Forgot your password?** link.</span></span> <span data-ttu-id="4d074-216">Bu durumda, uygulamanızı hello parolası sıfırlama ilkesini kullanmayı bir istek olmalısınız belirten bu hata kodu, uygulamanızı Azure AD B2C gönderir.</span><span class="sxs-lookup"><span data-stu-id="4d074-216">In this event, Azure AD B2C sends your app that error code indicating that your app should make a request using hello password reset policy instead.</span></span>

```CSharp
/*
* Catch any failures received by hello authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle hello error code that Azure AD B2C throws when trying tooreset a password from hello login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If hello user clicked hello reset password link, redirect toohello reset password route
        notification.Response.Redirect("/Account/ResetPassword");
    }
    else if (notification.Exception.Message == "access_denied")
    {
        notification.Response.Redirect("/");
    }
    else
    {
        notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
    }

    return Task.FromResult(0);
}
```

### <a name="send-authentication-requests-tooazure-ad"></a><span data-ttu-id="4d074-217">Kimlik doğrulama isteklerini tooAzure AD Gönder</span><span class="sxs-lookup"><span data-stu-id="4d074-217">Send authentication requests tooAzure AD</span></span>

<span data-ttu-id="4d074-218">Uygulamanızı Azure AD B2C ile düzgün şekilde yapılandırılmış toocommunicate hello Openıd Connect kimlik doğrulama protokolü kullanarak sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="4d074-218">Your app is now properly configured toocommunicate with Azure AD B2C by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="4d074-219">OWIN kimlik doğrulama iletileri hazırlayın, Azure AD B2C gelen belirteçleri doğrulamak ve kullanıcı oturumu koruyarak hello ayrıntılarını yönetir.</span><span class="sxs-lookup"><span data-stu-id="4d074-219">OWIN manages hello details of crafting authentication messages, validating tokens from Azure AD B2C, and maintaining user session.</span></span> <span data-ttu-id="4d074-220">Tüm bu kalır tooinitiate her kullanıcının akışıdır.</span><span class="sxs-lookup"><span data-stu-id="4d074-220">All that remains is tooinitiate each user's flow.</span></span>

<span data-ttu-id="4d074-221">Bir kullanıcı seçtiğinde **oturum yukarı/oturum açma**, **Düzenle profili**, veya **parola sıfırlama** hello web uygulamasında hello ilişkili eylemin çağrılması `Controllers\AccountController.cs`:</span><span class="sxs-lookup"><span data-stu-id="4d074-221">When a user selects **Sign up/Sign in**, **Edit profile**, or **Reset password** in hello web app, hello associated action is invoked in `Controllers\AccountController.cs`:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign up or sign in
*/
public void SignUpSignIn()
{
    // Use hello default policy tooprocess hello sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting tooedit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let hello middleware know you are trying toouse hello edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set hello page tooredirect tooafter editing hello profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting tooreset a password
*/
public void ResetPassword()
{
    // Let hello middleware know you are trying toouse hello reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set hello page tooredirect tooafter changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

<span data-ttu-id="4d074-222">OWIN toosign hello kullanıcının hello uygulama çıkışı de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d074-222">You can also use OWIN toosign out hello user from hello app.</span></span> <span data-ttu-id="4d074-223">İçinde `Controllers\AccountController.cs` sunuyoruz:</span><span class="sxs-lookup"><span data-stu-id="4d074-223">In `Controllers\AccountController.cs` we have:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign out
*/
public void SignOut()
{
    // toosign out hello user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

<span data-ttu-id="4d074-224">Bir ilke çağırma toplama tooexplicitly kullanabileceğiniz bir `[Authorize]` hello kullanıcı imzalı değilse bir ilke yürütür etiketinde denetleyicilerinizi.</span><span class="sxs-lookup"><span data-stu-id="4d074-224">In addition tooexplicitly invoking a policy, you can use a `[Authorize]` tag in your controllers that executes a policy if hello user is not signed in.</span></span> <span data-ttu-id="4d074-225">Açık `Controllers\HomeController.cs` ve hello ekleyin `[Authorize]` etiketi toohello talep denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="4d074-225">Open `Controllers\HomeController.cs` and add hello `[Authorize]` tag toohello claims controller.</span></span>  <span data-ttu-id="4d074-226">OWIN seçer hello son ilke hello yapılandırılmış `[Authorize]` etiketi isabet.</span><span class="sxs-lookup"><span data-stu-id="4d074-226">OWIN selects hello last policy configured when hello `[Authorize]` tag is hit.</span></span>

```CSharp
// Controllers\HomeController.cs

// You can use hello Authorize decorator tooexecute a certain policy if hello user is not already signed into hello app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a><span data-ttu-id="4d074-227">Kullanıcı bilgilerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="4d074-227">Display user information</span></span>

<span data-ttu-id="4d074-228">Openıd Connect kullanarak kullanıcıların kimlik doğrulaması sırasında Azure AD B2C içeren kimliği belirteci toohello uygulama döndürür **talep**.</span><span class="sxs-lookup"><span data-stu-id="4d074-228">When you authenticate users by using OpenID Connect, Azure AD B2C returns an ID token toohello app that contains **claims**.</span></span> <span data-ttu-id="4d074-229">Bunlar, hello kullanıcı hakkında onaylamalardır.</span><span class="sxs-lookup"><span data-stu-id="4d074-229">These are assertions about hello user.</span></span> <span data-ttu-id="4d074-230">Uygulamanızı talep toopersonalize kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d074-230">You can use claims toopersonalize your app.</span></span>

<span data-ttu-id="4d074-231">Açık hello `Controllers\HomeController.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="4d074-231">Open hello `Controllers\HomeController.cs` file.</span></span> <span data-ttu-id="4d074-232">Denetleyicilerinizi hello aracılığıyla, kullanıcı talepleri erişim `ClaimsPrincipal.Current` güvenlik sorumlusu nesnesi.</span><span class="sxs-lookup"><span data-stu-id="4d074-232">You can access user claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

```CSharp
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

<span data-ttu-id="4d074-233">Uygulamanızı hello aynı aldığını talep erişebileceği şekilde.</span><span class="sxs-lookup"><span data-stu-id="4d074-233">You can access any claim that your application receives in hello same way.</span></span>  <span data-ttu-id="4d074-234">Merhaba uygulama aldığı tüm hello talepler listesinin hello üzerinde sizin için kullanılabilir **talep** sayfası.</span><span class="sxs-lookup"><span data-stu-id="4d074-234">A list of all hello claims hello app receives is available for you on hello **Claims** page.</span></span>
