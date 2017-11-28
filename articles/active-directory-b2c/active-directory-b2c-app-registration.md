---
title: "Azure Active Directory B2C: Uygulama kaydı | Microsoft Belgeleri"
description: "Nasıl tooregister uygulamanız Azure Active Directory B2C ile"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: PatAltimore
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f69
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: parakhj
ms.openlocfilehash: bd58e123751db387d6c8f16bd010291ba698b1a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a><span data-ttu-id="ab1b5-103">Azure Active Directory B2C: Uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="ab1b5-103">Azure Active Directory B2C: Register your application</span></span>

<span data-ttu-id="ab1b5-104">Bu Hızlı Başlangıç, bir Microsoft Azure Active Directory (Azure AD) B2C Kiracısında bir uygulamayı birkaç dakika içinde kaydetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="ab1b5-105">İşiniz bittiğinde, uygulamanızı hello Azure B2C Kiracı kullanmak için kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-105">When you're finished, your application is registered for use in hello Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab1b5-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ab1b5-106">Prerequisites</span></span>

<span data-ttu-id="ab1b5-107">toobuild tüketicinin kaydolmasını ve oturum açma kabul eden bir uygulama, ilk Azure Active Directory B2C kiracısı ile tooregister Merhaba uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-107">toobuild an application that accepts consumer sign-up and sign-in, you first need tooregister hello application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="ab1b5-108">Kendi Kiracı özetlenen hello adımları kullanarak alma [bir Azure AD B2C kiracısı oluşturma](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ab1b5-108">Get your own tenant by using hello steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="ab1b5-109">Hello hello Azure AD B2C dikey penceresinde hello Azure portalında oluşturulan uygulamaları yönetilen aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-109">Applications created from hello Azure AD B2C blade in hello Azure portal must be managed from hello same location.</span></span> <span data-ttu-id="ab1b5-110">PowerShell veya başka bir portal kullanarak hello B2C uygulamaları düzenlerseniz, desteklenmeyen haline gelir ve Azure AD B2C ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-110">If you edit hello B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="ab1b5-111">Merhaba ayrıntıları görmek [hatalı uygulamaları](#faulted-apps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-111">See details in hello [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-toob2c-settings"></a><span data-ttu-id="ab1b5-112">TooB2C ayarları gidin</span><span class="sxs-lookup"><span data-stu-id="ab1b5-112">Navigate tooB2C settings</span></span>

<span data-ttu-id="ab1b5-113">İçinde toohello oturum [Azure portal](https://portal.azure.com/) hello B2C kiracısının genel Yöneticisi hello gibi.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-113">Log in toohello [Azure portal](https://portal.azure.com/) as hello Global Administrator of hello B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="ab1b5-114">Sonraki adımlar kaydettirmekte olduğunuz hello uygulama türüne göre seçin:</span><span class="sxs-lookup"><span data-stu-id="ab1b5-114">Choose next steps based on hello application type you are registering:</span></span>

* [<span data-ttu-id="ab1b5-115">Web uygulaması kaydetme</span><span class="sxs-lookup"><span data-stu-id="ab1b5-115">Register a web application</span></span>](#register-a-web-app)
* [<span data-ttu-id="ab1b5-116">Web API’si kaydetme</span><span class="sxs-lookup"><span data-stu-id="ab1b5-116">Register a web API</span></span>](#register-a-web-api)
* [<span data-ttu-id="ab1b5-117">Mobil veya yerel bir uygulamayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="ab1b5-117">Register a mobile or native application</span></span>](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a><span data-ttu-id="ab1b5-118">Web uygulaması kaydetme</span><span class="sxs-lookup"><span data-stu-id="ab1b5-118">Register a web app</span></span>

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

<span data-ttu-id="ab1b5-119">Web uygulamanız Azure AD B2C tarafından güvence altına alınmış bir web API'sini çağırıyorsa, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ab1b5-119">If your web application calls a web API secured by Azure AD B2C, perform these steps:</span></span>
   1. <span data-ttu-id="ab1b5-120">Giden toohello tarafından bir uygulama gizli anahtarı oluşturmak **anahtarları** dikey ve hello tıklayarak **anahtarı oluştur** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-120">Create an application secret by going toohello **Keys** blade and clicking hello **Generate Key** button.</span></span> <span data-ttu-id="ab1b5-121">Merhaba Not **uygulama anahtarı** değeri.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-121">Make note of hello **App key** value.</span></span> <span data-ttu-id="ab1b5-122">Uygulamanızın kodda hello uygulama gizli anahtarı olarak hello değerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-122">You use hello value as hello application secret in your application's code.</span></span>
   2. <span data-ttu-id="ab1b5-123">**API Erişimi**’ne ve **Ekle**’ye tıklayıp web API’si ve kapsamlarınızı (izinler) seçin.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-123">Click **API Access**, click **Add**, and select your web API and scopes (permissions).</span></span>

> [!NOTE]
> <span data-ttu-id="ab1b5-124">**Uygulama Gizli Anahtarı** önemli bir güvenlik kimlik bilgisidir ve güvenliği uygun şekilde sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-124">An **Application Secret** is an important security credential, and should be secured appropriately.</span></span>
> 

[<span data-ttu-id="ab1b5-125">Çok atlama**sonraki adımlar**</span><span class="sxs-lookup"><span data-stu-id="ab1b5-125">Jump too**next steps**</span></span>](#next-steps)

## <a name="register-a-web-api"></a><span data-ttu-id="ab1b5-126">Web API’si kaydetme</span><span class="sxs-lookup"><span data-stu-id="ab1b5-126">Register a web API</span></span>

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

<span data-ttu-id="ab1b5-127">Tıklatın **kapsamları yayımlanan** tooadd daha kapsamları gerektiğinde.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-127">Click **Published scopes** tooadd more scopes as necessary.</span></span> <span data-ttu-id="ab1b5-128">Varsayılan olarak, hello "user_impersonation" kapsam tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-128">By default, hello "user_impersonation" scope is defined.</span></span> <span data-ttu-id="ab1b5-129">Merhaba user_impersonation kapsam diğer uygulamaları hello özelliği tooaccess hello oturum açmış kullanıcı adına bu API sağlar.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-129">hello user_impersonation scope gives other applications hello ability tooaccess this api on behalf of hello signed-in user.</span></span> <span data-ttu-id="ab1b5-130">İsterseniz, hello user_impersonation kapsam kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-130">If you wish, hello user_impersonation scope can be removed.</span></span>

[<span data-ttu-id="ab1b5-131">Çok atlama**sonraki adımlar**</span><span class="sxs-lookup"><span data-stu-id="ab1b5-131">Jump too**next steps**</span></span>](#next-steps)

## <a name="register-a-mobile-or-native-app"></a><span data-ttu-id="ab1b5-132">Mobil veya yerel bir uygulamayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="ab1b5-132">Register a mobile or native app</span></span>

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[<span data-ttu-id="ab1b5-133">Çok atlama**sonraki adımlar**</span><span class="sxs-lookup"><span data-stu-id="ab1b5-133">Jump too**next steps**</span></span>](#next-steps)

## <a name="limitations"></a><span data-ttu-id="ab1b5-134">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="ab1b5-134">Limitations</span></span>

### <a name="choosing-a-web-app-or-api-reply-url"></a><span data-ttu-id="ab1b5-135">Bir web uygulaması veya api yanıt URL'si seçme</span><span class="sxs-lookup"><span data-stu-id="ab1b5-135">Choosing a web app or api reply URL</span></span>

<span data-ttu-id="ab1b5-136">Şu anda Azure AD B2C ile kayıtlı uygulamalar sınırlı kısıtlı tooa yanıt URL değerler kümesidir.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-136">Currently, apps that are registered with Azure AD B2C are restricted tooa limited set of reply URL values.</span></span> <span data-ttu-id="ab1b5-137">Merhaba web uygulamaları ve Hizmetleri için URL hello düzeniyle başlamalıdır yanıt `https`, ve URL değerler, tek bir DNS etki alanı paylaşması Tümünü Yanıtla.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-137">hello reply URL for web apps and services must begin with hello scheme `https`, and all reply URL values must share a single DNS domain.</span></span> <span data-ttu-id="ab1b5-138">Örneğin, şu yanıt URL'lerinden birine sahip bir web uygulamasını kaydedemezsiniz:</span><span class="sxs-lookup"><span data-stu-id="ab1b5-138">For example, you cannot register a web app that has one of these reply URLs:</span></span>

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="ab1b5-139">Merhaba kayıt sistem hello tam DNS adını hello varolan yanıt URL toohello DNS adını eklemekte olduğunuz hello yanıt URL'si karşılaştırır.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-139">hello registration system compares hello whole DNS name of hello existing reply URL toohello DNS name of hello reply URL that you are adding.</span></span> <span data-ttu-id="ab1b5-140">Aşağıdakilerden hello aşağıdaki koşullar doğruysa hello isteği tooadd hello DNS adı başarısız olur:</span><span class="sxs-lookup"><span data-stu-id="ab1b5-140">hello request tooadd hello DNS name fails if either of hello following conditions is true:</span></span>

* <span data-ttu-id="ab1b5-141">Merhaba tam DNS adını hello yeni yanıt URL'si hello varolan yanıt URL'si hello DNS adı eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-141">hello whole DNS name of hello new reply URL does not match hello DNS name of hello existing reply URL.</span></span>
* <span data-ttu-id="ab1b5-142">Merhaba yeni yanıt URL'si Hello tam DNS adı bir alt etki alanı hello varolan yanıt URL'si değil.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-142">hello whole DNS name of hello new reply URL is not a subdomain of hello existing reply URL.</span></span>

<span data-ttu-id="ab1b5-143">Örneğin, hello uygulama bu yanıt URL'si sahipse:</span><span class="sxs-lookup"><span data-stu-id="ab1b5-143">For example, if hello app has this reply URL:</span></span>

`https://login.contoso.com`

<span data-ttu-id="ab1b5-144">Bu gibi tooit ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ab1b5-144">You can add tooit, like this:</span></span>

`https://login.contoso.com/new`

<span data-ttu-id="ab1b5-145">Bu durumda, hello DNS adı tam olarak eşleşir.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-145">In this case, hello DNS name matches exactly.</span></span> <span data-ttu-id="ab1b5-146">Ya da şunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ab1b5-146">Or, you can do this:</span></span>

`https://new.login.contoso.com`

<span data-ttu-id="ab1b5-147">Bu durumda, login.contoso.com tooa DNS alt etki başvuran. Toohave east.contoso.com oturum açma ve oturum açma-west.contoso.com URL'leri yanıt olarak bir uygulama isterseniz bu sırada bu yanıt URL'leri eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="ab1b5-147">In this case, you're referring tooa DNS subdomain of login.contoso.com. If you want toohave an app that has login-east.contoso.com and login-west.contoso.com as reply URLs, you must add those reply URLs in this order:</span></span>

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="ab1b5-148">Yanıt URL'si ilk Merhaba, alt etki alanlarına olduklarından hello ikinci iki ekleyebilirsiniz contoso.com.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-148">You can add hello latter two because they are subdomains of hello first reply URL, contoso.com.</span></span>

### <a name="choosing-a-native-app-redirect-uri"></a><span data-ttu-id="ab1b5-149">Yerel uygulama yeniden yönlendirme URI'si seçme</span><span class="sxs-lookup"><span data-stu-id="ab1b5-149">Choosing a native app redirect URI</span></span>

<span data-ttu-id="ab1b5-150">Mobil/yerel uygulamalar için bir yeniden yönlendirme URI’si seçerken dikkat edilmesi gereken iki önemli nokta şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ab1b5-150">There are two important considerations when choosing a redirect URI for mobile/native applications:</span></span>

* <span data-ttu-id="ab1b5-151">**Benzersiz**: hello yeniden yönlendirme URI'si hello düzenini her uygulama için benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-151">**Unique**: hello scheme of hello redirect URI should be unique for every application.</span></span> <span data-ttu-id="ab1b5-152">Bizim örneğimizde (com.onmicrosoft.contoso.appname://redirect/path) hello şema olarak com.onmicrosoft.contoso.appname kullanırız.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-152">In our example (com.onmicrosoft.contoso.appname://redirect/path), we use com.onmicrosoft.contoso.appname as hello scheme.</span></span> <span data-ttu-id="ab1b5-153">Bu örneği izlemeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-153">We recommend following this pattern.</span></span> <span data-ttu-id="ab1b5-154">İki uygulama hello paylaşıyorsanız aynı, hello Düzen kullanıcı bir "uygulama Seç" iletişim kutusu görür.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-154">If two applications share hello same scheme, hello user sees a "choose app" dialog.</span></span> <span data-ttu-id="ab1b5-155">Merhaba kullanıcı yanlış bir seçim yaparsa hello oturum açma başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-155">If hello user makes an incorrect choice, hello login fails.</span></span>
* <span data-ttu-id="ab1b5-156">**Tam**: Yeniden yönlendirme URI’sinin bir şeması ve yolu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-156">**Complete**: Redirect URI must have a scheme and a path.</span></span> <span data-ttu-id="ab1b5-157">Merhaba yolunu en az bir eğik hello etki (örneğin, //contoso/ çalışır ve //contoso başarısız) içermelidir.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-157">hello path must contain at least one forward slash after hello domain (for example, //contoso/ works and //contoso fails).</span></span>

<span data-ttu-id="ab1b5-158">Yeniden yönlendirme URI'si Merhaba, alt çizgi gibi özel karakterler olmadığına olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-158">Ensure there are no special characters like underscores in hello redirect uri.</span></span>

### <a name="faulted-apps"></a><span data-ttu-id="ab1b5-159">Hatalı uygulamalar</span><span class="sxs-lookup"><span data-stu-id="ab1b5-159">Faulted apps</span></span>

<span data-ttu-id="ab1b5-160">B2C uygulamaları şu durumlarda DÜZENLENMEMELİDİR:</span><span class="sxs-lookup"><span data-stu-id="ab1b5-160">B2C applications should NOT be edited:</span></span>

* <span data-ttu-id="ab1b5-161">[Klasik Azure portalı](https://manage.windowsazure.com/) ve [Uygulama Kayıt Portalı](https://apps.dev.microsoft.com/) gibi diğer uygulama yanıt portallarında.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-161">On other application management portals such as the [Azure classic portal](https://manage.windowsazure.com/) & the [Application Registration Portal](https://apps.dev.microsoft.com/).</span></span>
* <span data-ttu-id="ab1b5-162">Grafik API'si veya PowerShell kullanılarak</span><span class="sxs-lookup"><span data-stu-id="ab1b5-162">Using Graph API or PowerShell</span></span>

<span data-ttu-id="ab1b5-163">Yukarıda açıklandığı gibi hello B2C uygulaması düzenleyin ve tooedit deneyin, bunu yeniden hello Azure AD B2C özellikleri dikey penceresinde hello Azure portal, hatalı bir uygulama olur ve uygulamanız artık Azure AD B2C ile kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-163">If you edit hello B2C application as described above and try tooedit it again in hello Azure AD B2C features blade on hello Azure portal, it becomes a faulted app, and your application is no longer usable with Azure AD B2C.</span></span> <span data-ttu-id="ab1b5-164">Toodelete hello uygulamasına sahip ve yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-164">You have toodelete hello application and create it again.</span></span>

<span data-ttu-id="ab1b5-165">toodelete hello uygulama, Git toohello [uygulama kayıt portalı](https://apps.dev.microsoft.com/) ve Merhaba uygulaması silin.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-165">toodelete hello app, go toohello [Application Registration Portal](https://apps.dev.microsoft.com/) and delete hello application there.</span></span> <span data-ttu-id="ab1b5-166">Merhaba uygulama toobe görünür için sırayla Merhaba uygulaması toobe hello sahibi (ve yalnızca hello Kiracı Yöneticisi) gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-166">In order for hello application toobe visible, you need toobe hello owner of hello application (and not just an admin of hello tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab1b5-167">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ab1b5-167">Next steps</span></span>

<span data-ttu-id="ab1b5-168">Azure AD B2C ile kayıtlı bir uygulamaya sahip olduğunuza göre aşağıdakilerden birini tamamlayabilirsiniz [hızlı başlangıç öğreticilerimizden](active-directory-b2c-overview.md#get-started) tooget çalışır.</span><span class="sxs-lookup"><span data-stu-id="ab1b5-168">Now that you have an application registered with Azure AD B2C, you can complete one of [our quick-start tutorials](active-directory-b2c-overview.md#get-started) tooget up and running.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ab1b5-169">Kaydolma, oturum açma ve parola sıfırlama seçenekleriyle bir ASP.NET web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ab1b5-169">Create an ASP.NET web app with sign-up, sign-in, and password reset</span></span>](active-directory-b2c-devquickstarts-web-dotnet-susi.md)