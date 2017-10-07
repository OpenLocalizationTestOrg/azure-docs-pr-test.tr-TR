---
title: "Azure B2C için aaaAdd oturum açma tooa Node.js web uygulaması | Microsoft Docs"
description: "Nasıl toobuild bir Node.js web uygulaması, kullanıcıların bir B2C kiracısı kullanarak imzalar."
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: db97f84a-1f24-447b-b6d2-0265c6896b27
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 03/10/2017
ms.author: xerners
ms.openlocfilehash: b4c334b1f7a0669df2d0864140603dc55bbb5408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-add-sign-in-tooa-nodejs-web-app"></a><span data-ttu-id="33e85-103">Azure AD B2C: oturum açma tooa Node.js web uygulaması Ekle</span><span class="sxs-lookup"><span data-stu-id="33e85-103">Azure AD B2C: Add sign-in tooa Node.js web app</span></span>

<span data-ttu-id="33e85-104">**Passport**, Node.js için kimlik doğrulama ara yazılımıdır.</span><span class="sxs-lookup"><span data-stu-id="33e85-104">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="33e85-105">Son derece esnek ve modüler olan Passport, Express tabanlı veya Restify web uygulamasına sorunsuz bir şekilde yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="33e85-105">Extremely flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="33e85-106">Bir dizi kapsamlı strateji; bir kullanıcı adı ve parola, Facebook, Twitter ve daha fazlası ile kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="33e85-106">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="33e85-107">Azure Active Directory (Azure AD) için bir strateji geliştirdik.</span><span class="sxs-lookup"><span data-stu-id="33e85-107">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="33e85-108">Bu modülü yükleyin ve ardından hello Azure AD ekleyin `passport-azure-ad` eklentisi.</span><span class="sxs-lookup"><span data-stu-id="33e85-108">You will install this module and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="33e85-109">toodo bunu yapmanız:</span><span class="sxs-lookup"><span data-stu-id="33e85-109">toodo this, you need to:</span></span>

1. <span data-ttu-id="33e85-110">Bir uygulamayı Azure AD kullanarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="33e85-110">Register an application by using Azure AD.</span></span>
2. <span data-ttu-id="33e85-111">Uygulama toouse hello ayarlamak `passport-azure-ad` eklentisi.</span><span class="sxs-lookup"><span data-stu-id="33e85-111">Set up your app toouse hello `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="33e85-112">Passport tooissue oturum açma ve oturum kapatma isteklerini tooAzure AD kullanın.</span><span class="sxs-lookup"><span data-stu-id="33e85-112">Use Passport tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="33e85-113">Kullanıcı verilerini yazdırın.</span><span class="sxs-lookup"><span data-stu-id="33e85-113">Print user data.</span></span>

<span data-ttu-id="33e85-114">Bu öğretici için kod Hello [Github'da korunur](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="33e85-114">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span></span> <span data-ttu-id="33e85-115">yapabilecekleriniz toofollow boyunca [hello uygulamanın çatısını bir .zip dosyası karşıdan](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="33e85-115">toofollow along, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="33e85-116">Ayrıca hello çatıyı kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="33e85-116">You can also clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="33e85-117">Tamamlanan Merhaba uygulaması hello Bu öğreticinin sonunda sağlanır.</span><span class="sxs-lookup"><span data-stu-id="33e85-117">hello completed application is provided at hello end of this tutorial.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="33e85-118">Azure AD B2C dizini alma</span><span class="sxs-lookup"><span data-stu-id="33e85-118">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="33e85-119">Azure AD B2C'yi kullanabilmek için önce dizin veya kiracı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="33e85-119">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="33e85-120">Dizin; tüm kullanıcılarınız, uygulamalarınız, gruplarınız ve daha fazlası için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="33e85-120">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="33e85-121">Henüz yoksa devam etmeden önce bu kılavuzda [bir B2C dizini oluşturun](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="33e85-121">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="33e85-122">Uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="33e85-122">Create an application</span></span>

<span data-ttu-id="33e85-123">Ardından B2C dizininizde uygulama toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="33e85-123">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="33e85-124">Bu, uygulamanız ile güvenli toocommunicate gereken bilgileri Azure AD'ye verir.</span><span class="sxs-lookup"><span data-stu-id="33e85-124">This gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="33e85-125">Hem istemci uygulaması hello ve web API tarafından tek bir temsil **uygulama kimliği**, bir mantıksal uygulama içerdikleri için.</span><span class="sxs-lookup"><span data-stu-id="33e85-125">Both hello client app and web API will be represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="33e85-126">Uygulama, bir toocreate izleyin [bu yönergeleri](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="33e85-126">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="33e85-127">Şunları yaptığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="33e85-127">Be sure to:</span></span>

- <span data-ttu-id="33e85-128">Dahil bir **web uygulaması**/**web API'si** hello uygulamada.</span><span class="sxs-lookup"><span data-stu-id="33e85-128">Include a **web app**/**web API** in hello application.</span></span>
- <span data-ttu-id="33e85-129">**Yanıt URL'si** olarak `http://localhost:3000/auth/openid/return` adresini girin.</span><span class="sxs-lookup"><span data-stu-id="33e85-129">Enter `http://localhost:3000/auth/openid/return` as a **Reply URL**.</span></span> <span data-ttu-id="33e85-130">Bu kod örneği için hello varsayılan URL değil.</span><span class="sxs-lookup"><span data-stu-id="33e85-130">It is hello default URL for this code sample.</span></span>
- <span data-ttu-id="33e85-131">Uygulamanız için bir **Uygulama gizli anahtarı** oluşturun ve bunu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="33e85-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="33e85-132">Buna daha sonra ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="33e85-132">You will need it later.</span></span> <span data-ttu-id="33e85-133">Bu değer toobe gerektiğini Not [XML kaçışlı](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) kullanmadan önce.</span><span class="sxs-lookup"><span data-stu-id="33e85-133">Note that this value needs toobe [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
- <span data-ttu-id="33e85-134">Kopya hello **uygulama kimliği** diğer bir deyişle atanan tooyour uygulama.</span><span class="sxs-lookup"><span data-stu-id="33e85-134">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="33e85-135">Buna da daha sonra ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="33e85-135">You'll also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="33e85-136">İlkelerinizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="33e85-136">Create your policies</span></span>

<span data-ttu-id="33e85-137">Azure AD B2C'de her kullanıcı deneyimi, bir [ilke](active-directory-b2c-reference-policies.md) ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="33e85-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="33e85-138">Bu uygulama üç kimlik deneyimi içerir: Kaydolma, oturum açma ve Facebook ile oturum açma.</span><span class="sxs-lookup"><span data-stu-id="33e85-138">This app contains three identity experiences: sign up, sign in, and sign in by using Facebook.</span></span> <span data-ttu-id="33e85-139">Toocreate açıklandığı gibi her tür Bu ilkeyi gereken [ilke başvurusu makalesinde](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="33e85-139">You need toocreate this policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="33e85-140">Üç ilkenizi oluştururken şunları yaptığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="33e85-140">When you create your three policies, be sure to:</span></span>

- <span data-ttu-id="33e85-141">Merhaba seçin **görünen adı** ve diğer kaydolma özniteliklerini kaydolma ilkenizde.</span><span class="sxs-lookup"><span data-stu-id="33e85-141">Choose hello **Display name** and other sign-up attributes in your sign-up policy.</span></span>
- <span data-ttu-id="33e85-142">Merhaba seçin **görünen adı** ve **nesne kimliği** her ilkede uygulamanın talep.</span><span class="sxs-lookup"><span data-stu-id="33e85-142">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="33e85-143">Diğer talepleri de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33e85-143">You can choose other claims as well.</span></span>
- <span data-ttu-id="33e85-144">Kopya hello **adı** oluşturduktan sonra her ilkenin.</span><span class="sxs-lookup"><span data-stu-id="33e85-144">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="33e85-145">Merhaba önekine sahip olmalıdır `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="33e85-145">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="33e85-146">Bu ilke adlarına daha sonra ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="33e85-146">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="33e85-147">Üç ilkenizi oluşturduktan sonra hazır toobuild olduğunuz uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="33e85-147">After you create your three policies, you're ready toobuild your app.</span></span>

<span data-ttu-id="33e85-148">Bu makalenin nasıl toouse hello ilkeleri oluşturduğunuz kapsamadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="33e85-148">Note that this article does not cover how toouse hello policies you just created.</span></span> <span data-ttu-id="33e85-149">toolearn ile Merhaba ilkelerinin Azure AD B2C'de nasıl çalıştığı hakkında başlangıç [.NET web uygulamasıyla çalışmaya başlama Öğreticisi](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="33e85-149">toolearn about how policies work in Azure AD B2C, start with hello [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="add-prerequisites-tooyour-directory"></a><span data-ttu-id="33e85-150">Önkoşullar tooyour Dizin Ekle</span><span class="sxs-lookup"><span data-stu-id="33e85-150">Add prerequisites tooyour directory</span></span>

<span data-ttu-id="33e85-151">Zaten orada değilseniz hello komut satırında, dizinleri tooyour kök klasörü değiştirin.</span><span class="sxs-lookup"><span data-stu-id="33e85-151">From hello command line, change directories tooyour root folder, if you're not already there.</span></span> <span data-ttu-id="33e85-152">Merhaba aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="33e85-152">Run hello following commands:</span></span>

- `npm install express`
- `npm install ejs`
- `npm install ejs-locals`
- `npm install restify`
- `npm install mongoose`
- `npm install bunyan`
- `npm install assert-plus`
- `npm install passport`
- `npm install webfinger`
- `npm install body-parser`
- `npm install express-session`
- `npm install cookie-parser`

<span data-ttu-id="33e85-153">Ayrıca, kullandık `passport-azure-ad` bizim önizlemede hello hello hızlı başlangıç çatısında önizlememiz için.</span><span class="sxs-lookup"><span data-stu-id="33e85-153">In addition, we used `passport-azure-ad` for our preview in hello skeleton of hello Quickstart.</span></span>

- `npm install passport-azure-ad`

<span data-ttu-id="33e85-154">Bu hello kitaplıkları yükleyecek, `passport-azure-ad` bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="33e85-154">This will install hello libraries that `passport-azure-ad` depends on.</span></span>

## <a name="set-up-your-app-toouse-hello-passport-nodejs-strategy"></a><span data-ttu-id="33e85-155">Uygulama toouse hello Passport Node.js stratejisi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="33e85-155">Set up your app toouse hello Passport-Node.js strategy</span></span>
<span data-ttu-id="33e85-156">Merhaba Express ara yazılım toouse hello Openıd Connect kimlik doğrulama protokolü yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="33e85-156">Configure hello Express middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="33e85-157">Passport oturum açma ve oturum kapatma isteklerini kullanılan tooissue olması, kullanıcı oturumlarını yönetmek ve diğer eylemler boyunca kullanıcılar hakkında bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="33e85-157">Passport will be used tooissue sign-in and sign-out requests, manage user sessions, and get information about users, among other actions.</span></span>

<span data-ttu-id="33e85-158">Açık hello `config.js` hello proje hello kökünde bulunan dosya ve hello uygulamanızın yapılandırma değerlerini girin `exports.creds` bölümü.</span><span class="sxs-lookup"><span data-stu-id="33e85-158">Open hello `config.js` file in hello root of hello project and enter your app's configuration values in hello `exports.creds` section.</span></span>
- <span data-ttu-id="33e85-159">`clientID`: Merhaba **uygulama kimliği** tooyour uygulama hello kayıt Portalı'nda atanmış.</span><span class="sxs-lookup"><span data-stu-id="33e85-159">`clientID`: hello **Application ID** assigned tooyour app in hello registration portal.</span></span>
- <span data-ttu-id="33e85-160">`returnURL`: Merhaba **yeniden yönlendirme URI'si** hello portalda girdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="33e85-160">`returnURL`: hello **Redirect URI** you entered in hello portal.</span></span>
- <span data-ttu-id="33e85-161">`tenantName`: hello Kiracı adı, bu gibi bir durumda uygulamanızın **contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="33e85-161">`tenantName`: hello tenant name of your app, for example, **contoso.onmicrosoft.com**.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="33e85-162">Açık hello `app.js` hello hello proje kökündeki dosyasında.</span><span class="sxs-lookup"><span data-stu-id="33e85-162">Open hello `app.js` file in hello root of hello project.</span></span> <span data-ttu-id="33e85-163">Çağrı tooinvoke hello aşağıdaki hello eklemek `OIDCStrategy` birlikte stratejisi `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="33e85-163">Add hello following call tooinvoke hello `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

<span data-ttu-id="33e85-164">Yalnızca toohandle oturum açma isteklerini başvurulan hello stratejiyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="33e85-164">Use hello strategy you just referenced toohandle sign-in requests.</span></span>

```JavaScript
// Use hello OIDCStrategy in Passport (Section 2).
//
//   Strategies in Passport require a "validate" function that accepts
//   credentials (in this case, an OpenID identifier), and invokes a callback
//   by using a user object.
passport.use(new OIDCStrategy({
    callbackURL: config.creds.returnURL,
    realm: config.creds.realm,
    clientID: config.creds.clientID,
    oidcIssuer: config.creds.issuer,
    identityMetadata: config.creds.identityMetadata,
    skipUserProfile: config.creds.skipUserProfile,
    responseType: config.creds.responseType,
    responseMode: config.creds.responseMode,
    tenantName: config.creds.tenantName
  },
  function(iss, sub, profile, accessToken, refreshToken, done) {
    log.info('Example: Email address we received was: ', profile.email);
    // asynchronous verification, for effect...
    process.nextTick(function () {
      findByEmail(profile.email, function(err, user) {
        if (err) {
          return done(err);
        }
        if (!user) {
          // "Auto-registration"
          users.push(profile);
          return done(null, profile);
        }
        return done(null, user);
      });
    });
  }
));
```
<span data-ttu-id="33e85-165">Passport, tüm stratejileri (Twitter ve Facebook dahil) için benzer bir desen kullanır.</span><span class="sxs-lookup"><span data-stu-id="33e85-165">Passport uses a similar pattern for all of its strategies (including Twitter and Facebook).</span></span> <span data-ttu-id="33e85-166">Tüm strateji yazıcıları toothis düzeni uyması.</span><span class="sxs-lookup"><span data-stu-id="33e85-166">All strategy writers adhere toothis pattern.</span></span> <span data-ttu-id="33e85-167">Merhaba stratejisi baktığınızda geçirdiğinizi görebilirsiniz bir `function()` belirtece sahip ve bir `done` hello parametre olarak.</span><span class="sxs-lookup"><span data-stu-id="33e85-167">When you look at hello strategy, you can see that you pass it a `function()` that has a token and a `done` as hello parameters.</span></span> <span data-ttu-id="33e85-168">tüm işlemlerini tamamladıktan sonra hello stratejisi tooyou gelir.</span><span class="sxs-lookup"><span data-stu-id="33e85-168">hello strategy comes back tooyou after it has done all of its work.</span></span> <span data-ttu-id="33e85-169">Merhaba kullanıcı saklayabilir ve böylece için yeniden tooask gerekmeyen hello belirteci kaydedin;.</span><span class="sxs-lookup"><span data-stu-id="33e85-169">Store hello user and stash hello token so that you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="33e85-170">Merhaba önceki kod hello kimlik doğrulamasını tüm kullanıcıları alır.</span><span class="sxs-lookup"><span data-stu-id="33e85-170">hello preceding code takes all users whom hello server authenticates.</span></span> <span data-ttu-id="33e85-171">Bu otomatik kayıttır.</span><span class="sxs-lookup"><span data-stu-id="33e85-171">This is autoregistration.</span></span> <span data-ttu-id="33e85-172">Üretim sunucularını kullandığınızda, ayarladığınız kayıt işlemiyle ilerlemiş sürece kullanıcılar toolet istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="33e85-172">When you use production servers, you don’t want toolet in users unless they have gone through a registration process that you have set up.</span></span> <span data-ttu-id="33e85-173">Tüketici uygulamalarında bu deseni sıkça görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33e85-173">You can often see this pattern in consumer apps.</span></span> <span data-ttu-id="33e85-174">Bunlar, tooregister Facebook kullanarak izin verir, ancak ek bilgiler toofill bunlar isteyin sonra.</span><span class="sxs-lookup"><span data-stu-id="33e85-174">These allow you tooregister by using Facebook, but then they ask you toofill out additional information.</span></span> <span data-ttu-id="33e85-175">Uygulamamız bir örnek olmasaydı, biz döndürülen hello belirteç nesnesinden bir e-posta adresi ayıklayın ve ardından ek bilgi hello kullanıcı toofill isteyin.</span><span class="sxs-lookup"><span data-stu-id="33e85-175">If our application wasn’t a sample, we could extract an email address from hello token object that is returned, and then ask hello user toofill out additional information.</span></span> <span data-ttu-id="33e85-176">Bu bir test sunucusu olduğundan, biz kullanıcıların toohello bellek içi veritabanına eklemeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="33e85-176">Because this is a test server, we simply add users toohello in-memory database.</span></span>

<span data-ttu-id="33e85-177">Tookeep izleme, oturum açmış kullanıcıların izin hello yöntemler ekleyen Passport'un gerektirdiği gibi.</span><span class="sxs-lookup"><span data-stu-id="33e85-177">Add hello methods that allow you tookeep track of users who have signed in, as required by Passport.</span></span> <span data-ttu-id="33e85-178">Bu, kullanıcı bilgilerini serileştirmeyi ve seri durumdan çıkarmayı kapsar:</span><span class="sxs-lookup"><span data-stu-id="33e85-178">This includes serializing and deserializing user information:</span></span>

```JavaScript

// Passport session setup. (Section 2)

//   toosupport persistent sign-in sessions, Passport needs toobe able to
//   serialize users into and deserialize users out of sessions. Typically,
//   this is as simple as storing hello user ID when Passport serializes a user
//   and finding hello user by ID when Passport deserializes that user.
passport.serializeUser(function(user, done) {
  done(null, user.email);
});

passport.deserializeUser(function(id, done) {
  findByEmail(id, function (err, user) {
    done(err, user);
  });
});

// Array toohold users who have signed in
var users = [];

var findByEmail = function(email, fn) {
  for (var i = 0, len = users.length; i < len; i++) {
    var user = users[i];
    log.info('we are using user: ', user);
    if (user.email === email) {
      return fn(null, user);
    }
  }
  return fn(null, null);
};

```

<span data-ttu-id="33e85-179">Merhaba kod tooload hello Express altyapısını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="33e85-179">Add hello code tooload hello Express engine.</span></span> <span data-ttu-id="33e85-180">Merhaba aşağıdakileri hello varsayılan kullandığımızı görebilirsiniz `/views` ve `/routes` Express'in sağladığı düzeni.</span><span class="sxs-lookup"><span data-stu-id="33e85-180">In hello following, you can see that we use hello default `/views` and `/routes` pattern that Express provides.</span></span>

```JavaScript

// configure Express (Section 2)

var app = express();


app.configure(function() {
  app.set('views', __dirname + '/views');
  app.set('view engine', 'ejs');
  app.use(express.logger());
  app.use(express.methodOverride());
  app.use(cookieParser());
  app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
  app.use(bodyParser.urlencoded({ extended : true }));
  // Initialize Passport!  Also use passport.session() middleware toosupport
  // persistent sign-in sessions (recommended).
  app.use(passport.initialize());
  app.use(passport.session());
  app.use(app.router);
  app.use(express.static(__dirname + '/../../public'));
});

```

<span data-ttu-id="33e85-181">Merhaba eklemek `POST` kapalı el yollar hello gerçek oturum açma isteklerini toohello `passport-azure-ad` altyapısı:</span><span class="sxs-lookup"><span data-stu-id="33e85-181">Add hello `POST` routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>

```JavaScript

// Our Auth routes (Section 3)

// GET /auth/openid
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. hello first step in OpenID authentication involves redirecting
//   hello user tooan OpenID provider. After hello user is authenticated,
//   hello OpenID provider redirects hello user back toothis application at
//   /auth/openid/return

app.get('/auth/openid',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Authentication was called in hello Sample');
    res.redirect('/');
  });

// GET /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it redirects hello user toohello home page.
app.get('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });

// POST /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it will redirect hello user toohello home page.

app.post('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });
```

## <a name="use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="33e85-182">Passport tooissue oturum açma ve oturum kapatma isteklerini tooAzure AD kullanın</span><span class="sxs-lookup"><span data-stu-id="33e85-182">Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>

<span data-ttu-id="33e85-183">Uygulamanızı hello v2.0 uç noktası ile düzgün şekilde yapılandırılmış toocommunicate hello Openıd Connect kimlik doğrulama protokolü kullanarak sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="33e85-183">Your app is now properly configured toocommunicate with hello v2.0 endpoint by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="33e85-184">`passport-azure-ad`alınan kimlik doğrulama iletileri hazırlayın, Azure AD'den belirteçleri doğrulamak ve kullanıcı oturumu koruma hello ayrıntılarını önemli.</span><span class="sxs-lookup"><span data-stu-id="33e85-184">`passport-azure-ad` has taken care of hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span> <span data-ttu-id="33e85-185">Tüm bu kalır, kullanıcılarınızın toogive olan bir şekilde toosign ve oturum out ve toogather açan kullanıcılar hakkında ek bilgi.</span><span class="sxs-lookup"><span data-stu-id="33e85-185">All that remains is toogive your users a way toosign in and sign out, and toogather additional information on users who have signed in.</span></span>

<span data-ttu-id="33e85-186">İlk olarak, hello varsayılan, oturum açma, hesap ve oturum kapatma yöntemlerini tooyour ekleyin `app.js` dosyası:</span><span class="sxs-lookup"><span data-stu-id="33e85-186">First, add hello default, sign-in, account, and sign-out methods tooyour `app.js` file:</span></span>

```JavaScript

//Routes (Section 4)

app.get('/', function(req, res){
  res.render('index', { user: req.user });
});

app.get('/account', ensureAuthenticated, function(req, res){
  res.render('account', { user: req.user });
});

app.get('/login',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Login was called in hello Sample');
    res.redirect('/');
});

app.get('/logout', function(req, res){
  req.logout();
  res.redirect('/');
});

```

<span data-ttu-id="33e85-187">tooreview bu yöntemleri ayrıntılı:</span><span class="sxs-lookup"><span data-stu-id="33e85-187">tooreview these methods in detail:</span></span>
- <span data-ttu-id="33e85-188">Merhaba `/` rota yönlendiren toohello `index.ejs` (varsa) geçirerek hello kullanıcı hello istekte görünümü.</span><span class="sxs-lookup"><span data-stu-id="33e85-188">hello `/` route redirects toohello `index.ejs` view by passing hello user in hello request (if it exists).</span></span>
- <span data-ttu-id="33e85-189">Merhaba `/account` rota ilk doğrular, doğrulanır (Bu aşağıda için uygulama hello).</span><span class="sxs-lookup"><span data-stu-id="33e85-189">hello `/account` route first verifies that you are authenticated (hello implementation for this is below).</span></span> <span data-ttu-id="33e85-190">Böylece hello kullanıcı hakkında ek bilgi alabilir hello istekte sonra hello kullanıcı geçirir.</span><span class="sxs-lookup"><span data-stu-id="33e85-190">It then passes hello user in hello request so that you can get additional information about hello user.</span></span>
- <span data-ttu-id="33e85-191">Merhaba `/login` rota çağrıları hello `azuread-openidconnect` doğrulayıcıdan `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="33e85-191">hello `/login` route calls hello `azuread-openidconnect` authenticator from `passport-azure-ad`.</span></span> <span data-ttu-id="33e85-192">İşlemi başarılı değil, hello rota hello kullanıcı geri çok yönlendiren`/login`.</span><span class="sxs-lookup"><span data-stu-id="33e85-192">If it doesn't succeed, hello route redirects hello user back too`/login`.</span></span>
- <span data-ttu-id="33e85-193">`/logout` yalnızca `logout.ejs` öğesini (ve yolunu) çağırır.</span><span class="sxs-lookup"><span data-stu-id="33e85-193">`/logout` simply calls `logout.ejs` (and its route).</span></span> <span data-ttu-id="33e85-194">Bu tanımlama bilgilerini temizler ve ardından döndürür kullanıcı geri çok hello`index.ejs`.</span><span class="sxs-lookup"><span data-stu-id="33e85-194">This clears cookies and then returns hello user back too`index.ejs`.</span></span>


<span data-ttu-id="33e85-195">Merhaba son kısmı için `app.js`, hello eklemek `EnsureAuthenticated` hello yöntemi `/account` rota.</span><span class="sxs-lookup"><span data-stu-id="33e85-195">For hello last part of `app.js`, add hello `EnsureAuthenticated` method that is used in hello `/account` route.</span></span>

```JavaScript

// Simple route middleware tooensure that hello user is authenticated. (Section 4)

//   Use this route middleware on any resource that needs toobe protected. If
//   hello request is authenticated (typically via a persistent sign-in session),
//   then hello request will proceed. Otherwise, hello user will be redirected toothe
//   sign-in page.
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/login')
}

```

<span data-ttu-id="33e85-196">Son olarak, hello sunucusu kendisini oluşturmak içinde `app.js`.</span><span class="sxs-lookup"><span data-stu-id="33e85-196">Finally, create hello server itself in `app.js`.</span></span>

```JavaScript

app.listen(3000);

```


## <a name="create-hello-views-and-routes-in-express-toocall-your-policies"></a><span data-ttu-id="33e85-197">Merhaba görünümler oluşturabilir ve hızlı toocall ilkelerinizi yönlendirir</span><span class="sxs-lookup"><span data-stu-id="33e85-197">Create hello views and routes in Express toocall your policies</span></span>

<span data-ttu-id="33e85-198">Şimdi `app.js` öğeniz tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="33e85-198">Your `app.js` is now complete.</span></span> <span data-ttu-id="33e85-199">Tooadd hello yollar ve toocall hello oturum açma ve kaydolma ilkeler izin görünümleri yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="33e85-199">You just need tooadd hello routes and views that allow you toocall hello sign-in and sign-up policies.</span></span> <span data-ttu-id="33e85-200">Bunlar ayrıca hello işlemek `/logout` ve `/login` oluşturduğunuz yollar.</span><span class="sxs-lookup"><span data-stu-id="33e85-200">These also handle hello `/logout` and `/login` routes you created.</span></span>

<span data-ttu-id="33e85-201">Merhaba oluşturmak `/routes/index.js` hello kök dizininin altındaki yol.</span><span class="sxs-lookup"><span data-stu-id="33e85-201">Create hello `/routes/index.js` route under hello root directory.</span></span>

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

<span data-ttu-id="33e85-202">Merhaba oluşturmak `/routes/user.js` hello kök dizininin altındaki yol.</span><span class="sxs-lookup"><span data-stu-id="33e85-202">Create hello `/routes/user.js` route under hello root directory.</span></span>

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

<span data-ttu-id="33e85-203">Bu basit yollar istekleri tooyour görünümleri geçirin.</span><span class="sxs-lookup"><span data-stu-id="33e85-203">These simple routes pass along requests tooyour views.</span></span> <span data-ttu-id="33e85-204">Var olan hello kullanıcı içerirler.</span><span class="sxs-lookup"><span data-stu-id="33e85-204">They include hello user, if one is present.</span></span>

<span data-ttu-id="33e85-205">Merhaba oluşturmak `/views/index.ejs` hello kök dizininin altında görünümü.</span><span class="sxs-lookup"><span data-stu-id="33e85-205">Create hello `/views/index.ejs` view under hello root directory.</span></span> <span data-ttu-id="33e85-206">Bu, oturum açma ve oturum kapatma için ilkeleri çağıran basit bir sayfadır. Ayrıca toograb hesap bilgileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33e85-206">This is a simple page that calls policies for sign-in and sign-out. You can also use it toograb account information.</span></span> <span data-ttu-id="33e85-207">Merhaba koşullu kullanabileceğinizi unutmayın `if (!user)` içinde hello kullanıcı geçirilir gibi hello isteği tooprovide kanıtlayan bilgiler hello kullanıcının oturum.</span><span class="sxs-lookup"><span data-stu-id="33e85-207">Note that you can use hello conditional `if (!user)` as hello user is passed through in hello request tooprovide evidence that hello user is signed in.</span></span>

```JavaScript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login/?p=your facebook policy">Sign in with Facebook</a>
    <a href="/login/?p=your email sign-in policy">Sign in with email</a>
    <a href="/login/?p=your email sign-up policy">Sign up with email</a>
<% } else { %>
    <h2>Hello, <%= user.displayName %>.</h2>
    <a href="/account">Account info</a></br>
    <a href="/logout">Log out</a>
<% } %>
```

<span data-ttu-id="33e85-208">Merhaba oluşturma `/views/account.ejs` ek bilgileri görüntüleyebilmek hello kök dizininin altındaki görüntülemek, `passport-azure-ad` hello kullanıcı isteğine koyulan.</span><span class="sxs-lookup"><span data-stu-id="33e85-208">Create hello `/views/account.ejs` view under hello root directory so that you can view additional information that `passport-azure-ad` put in hello user request.</span></span>

```Javascript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login">Sign in</a>
<% } else { %>
<p>displayName: <%= user.displayName %></p>
<p>givenName: <%= user.name.givenName %></p>
<p>familyName: <%= user.name.familyName %></p>
<p>UPN: <%= user._json.upn %></p>
<p>Profile ID: <%= user.id %></p>
<p>Full Claims</p>
<%- JSON.stringify(user) %>
<p></p>
<a href="/logout">Log Out</a>
<% } %>
```

<span data-ttu-id="33e85-209">Artık uygulamanızı oluşturabilir ve çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33e85-209">You can now build and run your app.</span></span>

<span data-ttu-id="33e85-210">Çalıştırma `node app.js` ve çok gidin`http://localhost:3000`</span><span class="sxs-lookup"><span data-stu-id="33e85-210">Run `node app.js` and navigate too`http://localhost:3000`</span></span>


<span data-ttu-id="33e85-211">Kaydolma veya e-posta veya Facebook kullanarak toohello uygulamada oturum açın.</span><span class="sxs-lookup"><span data-stu-id="33e85-211">Sign up or sign in toohello app by using email or Facebook.</span></span> <span data-ttu-id="33e85-212">Oturumu kapatın ve farklı kullanıcı olarak tekrar oturum açın.</span><span class="sxs-lookup"><span data-stu-id="33e85-212">Sign out and sign back in as a different user.</span></span>

##<a name="next-steps"></a><span data-ttu-id="33e85-213">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="33e85-213">Next steps</span></span>

<span data-ttu-id="33e85-214">Başvuru için hello tamamlandı (yapılandırma değerleriniz olmadan) örnek [bir .zip dosyası olarak sağlanan](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="33e85-214">For reference, hello completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="33e85-215">Aynı zamanda GitHub'dan kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="33e85-215">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="33e85-216">Gelişmiş konular toomore üzerinde şimdi taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33e85-216">You can now move on toomore advanced topics.</span></span> <span data-ttu-id="33e85-217">Deneyebilecekleriniz:</span><span class="sxs-lookup"><span data-stu-id="33e85-217">You might try:</span></span>

[<span data-ttu-id="33e85-218">Node.js içinde hello B2C modeli kullanarak bir web API güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="33e85-218">Secure a web API by using hello B2C model in Node.js</span></span>](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on toomore advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing hello your B2C App's UX >>]()

-->
