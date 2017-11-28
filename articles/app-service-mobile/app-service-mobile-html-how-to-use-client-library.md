---
title: "aaaHow tooUse hello Azure Mobile Apps için JavaScript SDK'sı"
description: "Nasıl Azure Mobile Apps için tooUse v"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 53b78965-caa3-4b22-bb67-5bd5c19d03c4
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 3fcbb0c5bd6918a285bdafa1946ba0bd47bb21b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a><span data-ttu-id="7bdcf-103">Nasıl tooUse hello JavaScript istemci kitaplığı Azure Mobile Apps için</span><span class="sxs-lookup"><span data-stu-id="7bdcf-103">How tooUse hello JavaScript client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="7bdcf-104">Bu kılavuz hello son kullanarak tooperform genel senaryolar öğretilmektedir [JavaScript SDK'sı Azure Mobile Apps için].</span><span class="sxs-lookup"><span data-stu-id="7bdcf-104">This guide teaches you tooperform common scenarios using hello latest [JavaScript SDK for Azure Mobile Apps].</span></span> <span data-ttu-id="7bdcf-105">Yeni tooAzure mobil uygulamalar varsa, ilk tamamlamak [Azure Mobile Apps Hızlı Başlangıç] toocreate bir arka uç ve bir tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend and create a table.</span></span> <span data-ttu-id="7bdcf-106">Bu kılavuzda, HTML/JavaScript Web uygulamaları kullanarak hello mobil arka uç odaklanın.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-106">In this guide, we focus on using hello mobile backend in HTML/JavaScript Web applications.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="7bdcf-107">Desteklenen platformlar</span><span class="sxs-lookup"><span data-stu-id="7bdcf-107">Supported platforms</span></span>
<span data-ttu-id="7bdcf-108">Tarayıcı desteği toohello geçerli sınırlamak ve önde gelen tarayıcılar hello sürümleri son: Google Chrome, Microsoft Edge, Microsoft Internet Explorer ve Mozilla Firefox.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-108">We limit browser support toohello current and last versions of hello major browsers:  Google Chrome, Microsoft Edge, Microsoft Internet Explorer, and Mozilla Firefox.</span></span>  <span data-ttu-id="7bdcf-109">Görece modern bir tarayıcı ile Merhaba SDK toofunction bekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-109">We expect hello SDK toofunction with any relatively modern browser.</span></span>

<span data-ttu-id="7bdcf-110">Merhaba paket Evrensel JavaScript modülü olarak CommonJS biçimleri ve genel öğeleri, AMD, destekler şekilde dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-110">hello package is distributed as a Universal JavaScript Module, so it supports globals, AMD, and CommonJS formats.</span></span>

## <span data-ttu-id="7bdcf-111"><a name="Setup"></a>Kurulum ve Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7bdcf-111"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="7bdcf-112">Bu kılavuz, bir tablo ile bir arka uç oluşturduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-112">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="7bdcf-113">Bu kılavuz o hello tablolu hello varsayar bu öğreticiler hello tablolarla aynı şema.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-113">This guide assumes that hello table has hello same schema as hello tables in those tutorials.</span></span>

<span data-ttu-id="7bdcf-114">Hello Azure Mobile Apps JavaScript SDK'sı yükleme hello yapılabilir `npm` komutu:</span><span class="sxs-lookup"><span data-stu-id="7bdcf-114">Installing hello Azure Mobile Apps JavaScript SDK can be done via hello `npm` command:</span></span>

```
npm install azure-mobile-apps-client --save
```

<span data-ttu-id="7bdcf-115">Merhaba kitaplığı CommonJS ortamlarda AMD kitaplığı olarak ve Browserify ve Webpack gibi bir ES2015 modül olarak da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-115">hello library can also be used as an ES2015 module, within CommonJS environments such as Browserify and Webpack and as an AMD library.</span></span>  <span data-ttu-id="7bdcf-116">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="7bdcf-116">For example:</span></span>

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

<span data-ttu-id="7bdcf-117">Doğrudan sunduğumuz CDN yükleyerek hello SDK önceden oluşturulmuş bir sürümünü de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7bdcf-117">You can also use a pre-built version of hello SDK by downloading directly from our CDN:</span></span>

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="7bdcf-118"><a name="auth"></a>Nasıl yapılır: kullanıcıların kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="7bdcf-118"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="7bdcf-119">Azure uygulama hizmeti, kimlik doğrulaması ve çeşitli dış kimlik sağlayıcılarını kullanarak uygulama kullanıcıları yetkilendirmek destekler: Facebook, Google, Microsoft Account ve Twitter.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-119">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="7bdcf-120">Tooonly kimliği doğrulanmış kullanıcıların belirli işlemler için tabloları toorestrict erişim izinlerini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-120">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="7bdcf-121">Sunucu komut dosyalarında kimliği doğrulanmış kullanıcılar tooimplement yetkilendirme kuralları hello kimliğini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-121">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="7bdcf-122">Daha fazla bilgi için bkz: Merhaba [kimlik doğrulamayı kullanmaya başlama] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-122">For more information, see hello [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="7bdcf-123">İki kimlik doğrulama akışı desteklenir: sunucu akışı ve bir istemci akışı.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-123">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="7bdcf-124">Merhaba sağlayıcının web kimlik doğrulaması arabirimde alacağından hello sunucu akış hello Basit kimlik doğrulama deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-124">hello server flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="7bdcf-125">Merhaba istemci akışı aygıta özgü özellikleri ile daha derin tümleştirme gibi izin verir çoklu oturum açma sağlayıcıya özgü SDK'ları üzerinde alacağından.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-125">hello client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="7bdcf-126"><a name="configure-external-redirect-urls"></a>Nasıl yapılır: Mobil uygulama hizmetiniz için dış yönlendirme URL'lerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-126"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="7bdcf-127">JavaScript uygulamaları çeşitli OAuth UI akar geri döngü yetenek toohandle kullanın.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-127">Several types of JavaScript applications use a loopback capability toohandle OAuth UI flows.</span></span>  <span data-ttu-id="7bdcf-128">Bu özellikler şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="7bdcf-128">These capabilities include:</span></span>

* <span data-ttu-id="7bdcf-129">Hizmetinizi yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7bdcf-129">Running your service locally</span></span>
* <span data-ttu-id="7bdcf-130">Dinamik yeniden hello Ionic Framework ile kullanma</span><span class="sxs-lookup"><span data-stu-id="7bdcf-130">Using Live Reload with hello Ionic Framework</span></span>
* <span data-ttu-id="7bdcf-131">TooApp hizmet kimlik doğrulaması için yönlendirme.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-131">Redirecting tooApp Service for authentication.</span></span>

<span data-ttu-id="7bdcf-132">Varsayılan olarak, uygulama hizmet kimlik doğrulaması yalnızca olduğundan, mobil uygulamanızın arka ucuna tooallow erişimden yapılandırılmış olduğundan, yerel olarak çalışan sorunlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-132">Running locally can cause problems because, by default, App Service authentication is only configured tooallow access from your Mobile App backend.</span></span> <span data-ttu-id="7bdcf-133">Adımları toochange hello App Service ayarlarını tooenable kimlik doğrulaması hello sunucu yerel olarak çalıştırırken aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="7bdcf-133">Use hello following steps toochange hello App Service settings tooenable authentication when running hello server locally:</span></span>

1. <span data-ttu-id="7bdcf-134">İçinde toohello oturum [Azure portalı]</span><span class="sxs-lookup"><span data-stu-id="7bdcf-134">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="7bdcf-135">Tooyour mobil uygulama arka ucu gidin.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-135">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="7bdcf-136">Seçin **kaynak Gezgini** hello içinde **geliştirme araçları** menüsü.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-136">Select **Resource explorer** in hello **DEVELOPMENT TOOLS** menu.</span></span>
4. <span data-ttu-id="7bdcf-137">Tıklatın **Git** tooopen hello kaynak Gezgini, mobil uygulamanızın arka ucuna yeni sekmesinde veya penceresinde için.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-137">Click **Go** tooopen hello resource explorer for your Mobile App backend in a new tab or window.</span></span>
5. <span data-ttu-id="7bdcf-138">Merhaba genişletin **config** > **authsettings** düğümü, uygulamanız için.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-138">Expand hello **config** > **authsettings** node for your app.</span></span>
6. <span data-ttu-id="7bdcf-139">Merhaba tıklatın **Düzenle** düğmesini tooenable hello kaynak düzenleme.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-139">Click hello **Edit** button tooenable editing of hello resource.</span></span>
7. <span data-ttu-id="7bdcf-140">Hello bulur **allowedExternalRedirectUrls** öğesi null olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-140">Find hello **allowedExternalRedirectUrls** element, which should be null.</span></span> <span data-ttu-id="7bdcf-141">URL'nizde bir dizide ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7bdcf-141">Add your URLs in an array:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="7bdcf-142">Merhaba URL'leri hello dizisinde olan bu örnekte hizmetinizi hello URL'ler ile Değiştir `http://localhost:3000` hello yerel Node.js örnek hizmetinin.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-142">Replace hello URLs in hello array with hello URLs of your service, which in this example is `http://localhost:3000` for hello local Node.js sample service.</span></span> <span data-ttu-id="7bdcf-143">De kullanabilirsiniz `http://localhost:4400` hello Ripple hizmet veya uygulamanızı nasıl yapılandırıldığına bağlı olarak bazı diğer URL.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-143">You could also use `http://localhost:4400` for hello Ripple service or some other URL, depending on how your app is configured.</span></span>
8. <span data-ttu-id="7bdcf-144">Merhaba hello sayfanın en üstünde, tıklatın **okuma/yazma**, ardından **PUT** toosave yaptığınız güncelleştirmeler.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-144">At hello top of hello page, click **Read/Write**, then click **PUT** toosave your updates.</span></span>

<span data-ttu-id="7bdcf-145">Tooadd etmeniz aynı geri döngü URL'leri toohello CORS beyaz liste ayarları hello:</span><span class="sxs-lookup"><span data-stu-id="7bdcf-145">You also need tooadd hello same loopback URLs toohello CORS whitelist settings:</span></span>

1. <span data-ttu-id="7bdcf-146">Geri toohello gidin [Azure portalı].</span><span class="sxs-lookup"><span data-stu-id="7bdcf-146">Navigate back toohello [Azure portal].</span></span>
2. <span data-ttu-id="7bdcf-147">Tooyour mobil uygulama arka ucu gidin.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-147">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="7bdcf-148">Tıklatın **CORS** hello içinde **API** menüsü.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-148">Click **CORS** in hello **API** menu.</span></span>
4. <span data-ttu-id="7bdcf-149">Merhaba boş her URL girin **izin verilen çıkış noktası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-149">Enter each URL in hello empty **Allowed Origins** text box.</span></span>  <span data-ttu-id="7bdcf-150">Yeni bir metin kutusu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-150">A new text box is created.</span></span>
5. <span data-ttu-id="7bdcf-151">Tıklatın **Kaydet**</span><span class="sxs-lookup"><span data-stu-id="7bdcf-151">Click **SAVE**</span></span>

<span data-ttu-id="7bdcf-152">Merhaba arka uç güncelleştirildikten sonra uygulamanızda mümkün toouse hello yeni geri döngü URL'ler olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7bdcf-152">After hello backend updates, you will be able toouse hello new loopback URLs in your app.</span></span>

<!-- URLs. -->
[Azure Mobile Apps Hızlı Başlangıç]: app-service-mobile-cordova-get-started.md
[kimlik doğrulamayı kullanmaya başlama]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[Azure portalı]: https://portal.azure.com/
[JavaScript SDK'sı Azure Mobile Apps için]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
