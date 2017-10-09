---
title: "aaaHow tooUse Azure Mobile Apps için Apache Cordova eklentisi"
description: "Nasıl tooUse Azure Mobile Apps için Apache Cordova eklentisi"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: a56a1ce4-de0c-4f3c-8763-66252c52aa59
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: d3e0639e6478c409132af25304a2fb0f28401e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-apache-cordova-client-library-for-azure-mobile-apps"></a><span data-ttu-id="cab45-103">Nasıl Azure Mobile Apps için toouse Apache Cordova istemci kitaplığı</span><span class="sxs-lookup"><span data-stu-id="cab45-103">How toouse Apache Cordova client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="cab45-104">Bu kılavuz hello son kullanarak tooperform genel senaryolar öğretilmektedir [Azure Mobile Apps için Apache Cordova eklentisi].</span><span class="sxs-lookup"><span data-stu-id="cab45-104">This guide teaches you tooperform common scenarios using hello latest [Apache Cordova Plugin for Azure Mobile Apps].</span></span> <span data-ttu-id="cab45-105">Yeni tooAzure mobil uygulamalar varsa, ilk tamamlamak [Azure Mobile Apps Hızlı Başlangıç] toocreate bir arka uç bir tablo oluşturun ve önceden oluşturulmuş bir Apache Cordova projenizi indirin.</span><span class="sxs-lookup"><span data-stu-id="cab45-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend, create a table, and download a pre-built Apache Cordova project.</span></span> <span data-ttu-id="cab45-106">Bu kılavuzda, biz hello istemci tarafında odaklanmak Apache Cordova eklentisi.</span><span class="sxs-lookup"><span data-stu-id="cab45-106">In this guide, we focus on hello client-side Apache Cordova Plugin.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="cab45-107">Desteklenen platformlar</span><span class="sxs-lookup"><span data-stu-id="cab45-107">Supported platforms</span></span>
<span data-ttu-id="cab45-108">Apache Cordova v6.0.0 ve daha sonra iOS, Android ve Windows bu SDK destekleyen cihazlar.</span><span class="sxs-lookup"><span data-stu-id="cab45-108">This SDK supports Apache Cordova v6.0.0 and later on iOS, Android, and Windows devices.</span></span>  <span data-ttu-id="cab45-109">Merhaba platform desteği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="cab45-109">hello platform support is as follows:</span></span>

* <span data-ttu-id="cab45-110">Android API 19-24 (KitKat Nougat aracılığıyla).</span><span class="sxs-lookup"><span data-stu-id="cab45-110">Android API 19-24 (KitKat through Nougat).</span></span>
* <span data-ttu-id="cab45-111">iOS 8.0 ve sonraki sürümleri.</span><span class="sxs-lookup"><span data-stu-id="cab45-111">iOS versions 8.0 and later.</span></span>
* <span data-ttu-id="cab45-112">Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="cab45-112">Windows Phone 8.1.</span></span>
* <span data-ttu-id="cab45-113">Evrensel Windows platformu.</span><span class="sxs-lookup"><span data-stu-id="cab45-113">Universal Windows Platform.</span></span>

## <span data-ttu-id="cab45-114"><a name="Setup"></a>Kurulum ve Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="cab45-114"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="cab45-115">Bu kılavuz, bir tablo ile bir arka uç oluşturduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="cab45-115">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="cab45-116">Bu kılavuz o hello tablolu hello varsayar bu öğreticiler hello tablolarla aynı şema.</span><span class="sxs-lookup"><span data-stu-id="cab45-116">This guide assumes that hello table has hello same schema as hello tables in those tutorials.</span></span> <span data-ttu-id="cab45-117">Bu kılavuz, ayrıca hello Apache Cordova eklentisi tooyour kodu eklemiştir varsayar.</span><span class="sxs-lookup"><span data-stu-id="cab45-117">This guide also assumes that you have added hello Apache Cordova Plugin tooyour code.</span></span>  <span data-ttu-id="cab45-118">Bunu yapmadıysanız hello komut satırında hello Apache Cordova eklentisi tooyour proje ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cab45-118">If you have not done so, you may add hello Apache Cordova plugin tooyour project on hello command line:</span></span>

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="cab45-119">Oluşturma hakkında daha fazla bilgi için [ilk Apache Cordova uygulamanızı], kendi belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="cab45-119">For more information on creating [your first Apache Cordova app], see their documentation.</span></span>

## <span data-ttu-id="cab45-120"><a name="ionic"></a>Ionic v2 uygulama ayarlama</span><span class="sxs-lookup"><span data-stu-id="cab45-120"><a name="ionic"></a>Setting up an Ionic v2 app</span></span>

<span data-ttu-id="cab45-121">tooproperly Ionic v2 projesinde yapılandırmak, ilk temel bir uygulama oluşturun ve hello Cordova eklentisi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="cab45-121">tooproperly configure an Ionic v2 project, first create a basic app and add hello Cordova plugin:</span></span>

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="cab45-122">Çok satırlardan hello eklemek`app.component.ts` toocreate hello istemci nesnesi:</span><span class="sxs-lookup"><span data-stu-id="cab45-122">Add hello following lines too`app.component.ts` toocreate hello client object:</span></span>

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

<span data-ttu-id="cab45-123">Şimdi, yapı ve başlangıç projesi hello tarayıcıda çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="cab45-123">You can now build and run hello project in hello browser:</span></span>

```
ionic platform add browser
ionic run browser
```

<span data-ttu-id="cab45-124">Hello Azure Mobile Apps Cordova eklentisi her iki Ionic v1 ve v2 uygulamaları destekler.</span><span class="sxs-lookup"><span data-stu-id="cab45-124">hello Azure Mobile Apps Cordova plugin supports both Ionic v1 and v2 apps.</span></span>  <span data-ttu-id="cab45-125">Merhaba Ionic v2 uygulamaları ek bildirimi Merhaba gerekir. yalnızca `WindowsAzure` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="cab45-125">Only hello Ionic v2 apps require the additional declaration for hello `WindowsAzure` object.</span></span>

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="cab45-126"><a name="auth"></a>Nasıl yapılır: kullanıcıların kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="cab45-126"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="cab45-127">Azure uygulama hizmeti, kimlik doğrulaması ve çeşitli dış kimlik sağlayıcılarını kullanarak uygulama kullanıcıları yetkilendirmek destekler: Facebook, Google, Microsoft Account ve Twitter.</span><span class="sxs-lookup"><span data-stu-id="cab45-127">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="cab45-128">Tooonly kimliği doğrulanmış kullanıcıların belirli işlemler için tabloları toorestrict erişim izinlerini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cab45-128">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="cab45-129">Sunucu komut dosyalarında kimliği doğrulanmış kullanıcılar tooimplement yetkilendirme kuralları hello kimliğini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cab45-129">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="cab45-130">Daha fazla bilgi için bkz: Merhaba [kimlik doğrulamayı kullanmaya başlama] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="cab45-130">For more information, see hello [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="cab45-131">Kimlik doğrulaması bir Apache Cordova uygulaması kullanırken, Cordova eklenti aşağıdaki hello kullanılabilir olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="cab45-131">When using authentication in an Apache Cordova app, hello following Cordova plugins must be available:</span></span>

* <span data-ttu-id="cab45-132">[cordova-plugin-device]</span><span class="sxs-lookup"><span data-stu-id="cab45-132">[cordova-plugin-device]</span></span>
* <span data-ttu-id="cab45-133">[cordova eklentisi inappbrowser]</span><span class="sxs-lookup"><span data-stu-id="cab45-133">[cordova-plugin-inappbrowser]</span></span>

<span data-ttu-id="cab45-134">İki kimlik doğrulama akışı desteklenir: sunucu akışı ve bir istemci akışı.</span><span class="sxs-lookup"><span data-stu-id="cab45-134">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="cab45-135">Merhaba sağlayıcının web kimlik doğrulaması arabirimde alacağından hello sunucu akış hello Basit kimlik doğrulama deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="cab45-135">hello server flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="cab45-136">Merhaba istemci akışı aygıta özgü özellikleri ile daha derin tümleştirme gibi izin verir çoklu oturum açma sağlayıcıya özgü aygıta özgü SDK'ları üzerinde alacağından.</span><span class="sxs-lookup"><span data-stu-id="cab45-136">hello client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific device-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="cab45-137"><a name="configure-external-redirect-urls"></a>Nasıl yapılır: Mobil uygulama hizmetiniz için dış yönlendirme URL'lerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cab45-137"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="cab45-138">Apache Cordova uygulamaları çeşitli OAuth UI akar geri döngü yetenek toohandle kullanın.</span><span class="sxs-lookup"><span data-stu-id="cab45-138">Several types of Apache Cordova applications use a loopback capability toohandle OAuth UI flows.</span></span>  <span data-ttu-id="cab45-139">Localhost üzerinde OAuth UI akışları hello kimlik doğrulama hizmeti yalnızca bilir beri sorunlara neden nasıl tooutilize varsayılan olarak, hizmet.</span><span class="sxs-lookup"><span data-stu-id="cab45-139">OAuth UI flows on localhost cause problems since hello authentication service only knows how tooutilize your service by default.</span></span>  <span data-ttu-id="cab45-140">Sorunlu OAuth UI akışları örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="cab45-140">Examples of problematic OAuth UI flows include:</span></span>

* <span data-ttu-id="cab45-141">Merhaba Ripple öykünücüsü.</span><span class="sxs-lookup"><span data-stu-id="cab45-141">hello Ripple emulator.</span></span>
* <span data-ttu-id="cab45-142">Yeniden Ionic ile canlı.</span><span class="sxs-lookup"><span data-stu-id="cab45-142">Live Reload with Ionic.</span></span>
* <span data-ttu-id="cab45-143">Merhaba mobil arka uç yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="cab45-143">Running hello mobile backend locally</span></span>
* <span data-ttu-id="cab45-144">Merhaba mobil arka uç hello bir sağlayan kimlik doğrulama'den farklı bir Azure uygulama hizmeti çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="cab45-144">Running hello mobile backend in a different Azure App Service than hello one providing authentication.</span></span>

<span data-ttu-id="cab45-145">Bu yönergeler tooadd yerel ayarları toohello yapılandırmanızı izleyin:</span><span class="sxs-lookup"><span data-stu-id="cab45-145">Follow these instructions tooadd your local settings toohello configuration:</span></span>

1. <span data-ttu-id="cab45-146">İçinde toohello oturum [Azure portalı]</span><span class="sxs-lookup"><span data-stu-id="cab45-146">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="cab45-147">Seçin **tüm kaynakları** veya **uygulama hizmetleri** mobil uygulamanızın hello adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="cab45-147">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="cab45-148">Tıklatın **araçları**</span><span class="sxs-lookup"><span data-stu-id="cab45-148">Click **Tools**</span></span>
4. <span data-ttu-id="cab45-149">Tıklatın **kaynak Gezgini** hello GÖZLEMLE menüde, ardından **Git**.</span><span class="sxs-lookup"><span data-stu-id="cab45-149">Click **Resource explorer** in hello OBSERVE menu, then click **Go**.</span></span>  <span data-ttu-id="cab45-150">Yeni bir pencere veya sekmesinde açar.</span><span class="sxs-lookup"><span data-stu-id="cab45-150">A new window or tab opens.</span></span>
5. <span data-ttu-id="cab45-151">Merhaba genişletin **config**, **authsettings** hello sol gezinti sitenizdeki düğümlerin.</span><span class="sxs-lookup"><span data-stu-id="cab45-151">Expand hello **config**, **authsettings** nodes for your site in hello left-hand navigation.</span></span>
6. <span data-ttu-id="cab45-152">Tıklatın **Düzenle**</span><span class="sxs-lookup"><span data-stu-id="cab45-152">Click **Edit**</span></span>
7. <span data-ttu-id="cab45-153">Merhaba "allowedExternalRedirectUrls" öğesini arayın.</span><span class="sxs-lookup"><span data-stu-id="cab45-153">Look for hello "allowedExternalRedirectUrls" element.</span></span>  <span data-ttu-id="cab45-154">Toonull veya bir dizi değere ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="cab45-154">It may be set toonull or an array of values.</span></span>  <span data-ttu-id="cab45-155">Aşağıdaki değeri hello değeri toohello değiştirin:</span><span class="sxs-lookup"><span data-stu-id="cab45-155">Change hello value toohello following value:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="cab45-156">Merhaba URL'leri hizmetinizi hello URL'ler ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="cab45-156">Replace hello URLs with hello URLs of your service.</span></span>  <span data-ttu-id="cab45-157">Örnekler (Merhaba Node.js örnek hizmeti için) "http://localhost: 3000" veya "http://localhost:4400" (Merhaba Ripple hizmeti) içerir.</span><span class="sxs-lookup"><span data-stu-id="cab45-157">Examples include "http://localhost:3000" (for hello Node.js sample service), or "http://localhost:4400" (for hello Ripple service).</span></span>  <span data-ttu-id="cab45-158">Ancak, bu URL'ler örnekler - hello örneklerde, belirtilen hello Hizmetleri dahil olmak üzere durumunuz farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="cab45-158">However, these URLs are examples - your situation, including for hello services mentioned in hello examples, may be different.</span></span>
8. <span data-ttu-id="cab45-159">Merhaba tıklatın **okuma/yazma** Merhaba ekranında sağ üst köşesindeki hello düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cab45-159">Click hello **Read/Write** button in hello top-right corner of hello screen.</span></span>
9. <span data-ttu-id="cab45-160">Merhaba yeşil tıklatın **PUT** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cab45-160">Click hello green **PUT** button.</span></span>

<span data-ttu-id="cab45-161">Bu noktada kaydedilmiş Hello ayarları.</span><span class="sxs-lookup"><span data-stu-id="cab45-161">hello settings are saved at this point.</span></span>  <span data-ttu-id="cab45-162">Hello ayarları bitinceye kadar hello tarayıcı penceresini kapatmayın kaydediliyor.</span><span class="sxs-lookup"><span data-stu-id="cab45-162">Do not close hello browser window until hello settings have finished saving.</span></span>
<span data-ttu-id="cab45-163">Ayrıca uygulama hizmetiniz için bu geri döngü URL'leri toohello CORS ayarları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="cab45-163">Also add these loopback URLs toohello CORS settings for your App Service:</span></span>

1. <span data-ttu-id="cab45-164">İçinde toohello oturum [Azure portalı]</span><span class="sxs-lookup"><span data-stu-id="cab45-164">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="cab45-165">Seçin **tüm kaynakları** veya **uygulama hizmetleri** mobil uygulamanızın hello adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="cab45-165">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="cab45-166">Merhaba ayarlar dikey penceresi otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="cab45-166">hello Settings blade opens automatically.</span></span>  <span data-ttu-id="cab45-167">' I içermiyorsa tıklatırsanız **tüm ayarları**.</span><span class="sxs-lookup"><span data-stu-id="cab45-167">If it doesn't, click **All Settings**.</span></span>
4. <span data-ttu-id="cab45-168">Tıklatın **CORS** hello API menüsü altında.</span><span class="sxs-lookup"><span data-stu-id="cab45-168">Click **CORS** under hello API menu.</span></span>
5. <span data-ttu-id="cab45-169">Sağlanan hello kutusunda tooadd istediğiniz hello URL'sini girin ve Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="cab45-169">Enter hello URL that you wish tooadd in hello box provided and press Enter.</span></span>
6. <span data-ttu-id="cab45-170">Gerektiğinde ek URL'leri girin.</span><span class="sxs-lookup"><span data-stu-id="cab45-170">Enter additional URLs as needed.</span></span>
7. <span data-ttu-id="cab45-171">Tıklatın **kaydetmek** toosave hello ayarları.</span><span class="sxs-lookup"><span data-stu-id="cab45-171">Click **Save** toosave hello settings.</span></span>

<span data-ttu-id="cab45-172">Merhaba yeni ayarları tootake etkisi yaklaşık olarak 10-15 saniye sürer.</span><span class="sxs-lookup"><span data-stu-id="cab45-172">It takes approximately 10-15 seconds for hello new settings tootake effect.</span></span>

## <span data-ttu-id="cab45-173"><a name="register-for-push"></a>Nasıl yapılır: anında iletme bildirimleri için</span><span class="sxs-lookup"><span data-stu-id="cab45-173"><a name="register-for-push"></a>How to: Register for push notifications</span></span>
<span data-ttu-id="cab45-174">Merhaba yüklemek [phonegap eklentiyi itme] toohandle anında iletme bildirimleri.</span><span class="sxs-lookup"><span data-stu-id="cab45-174">Install hello [phonegap-plugin-push] toohandle push notifications.</span></span>  <span data-ttu-id="cab45-175">Bu eklenti kullanarak kolayca eklenebilen `cordova plugin add` hello komut satırında veya Visual Studio içinde hello Git eklentisi yükleyici aracılığıyla komutu.</span><span class="sxs-lookup"><span data-stu-id="cab45-175">This plugin can be easily added using the `cordova plugin add` command on hello command line, or via hello Git plugin installer within Visual Studio.</span></span>  <span data-ttu-id="cab45-176">Apache Cordova uygulamanızı aşağıdaki kodda Cihazınızı anında iletme bildirimleri için kaydeder:</span><span class="sxs-lookup"><span data-stu-id="cab45-176">The following code in your Apache Cordova app registers your device for push notifications:</span></span>

```
var pushOptions = {
    android: {
        senderId: '<from-gcm-console>'
    },
    ios: {
        alert: true,
        badge: true,
        sound: true
    },
    windows: {
    }
};
pushHandler = PushNotification.init(pushOptions);

pushHandler.on('registration', function (data) {
    registrationId = data.registrationId;
    // For cross-platform, you can use hello device plugin toodetermine hello device
    // Best is toouse device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by hello PNS - check hello format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

<span data-ttu-id="cab45-177">Merhaba Notification Hubs SDK'sı toosend anında iletme bildirimleri hello sunucusundan kullanın.</span><span class="sxs-lookup"><span data-stu-id="cab45-177">Use hello Notification Hubs SDK toosend push notifications from hello server.</span></span>  <span data-ttu-id="cab45-178">Hiçbir zaman doğrudan istemcilerden anında iletme bildirimleri gönderme.</span><span class="sxs-lookup"><span data-stu-id="cab45-178">Never send push notifications directly from clients.</span></span> <span data-ttu-id="cab45-179">Bunu yapmak nedenle oluşturulamadı kullanılan tootrigger bir hizmet reddi saldırısına karşı bildirim hub'ları olması veya PNS hello.</span><span class="sxs-lookup"><span data-stu-id="cab45-179">Doing so could be used tootrigger a denial of service attack against Notification Hubs or hello PNS.</span></span>  <span data-ttu-id="cab45-180">Merhaba PNS trafiğinizi bu tür saldırıları sonucunda bSunucu.</span><span class="sxs-lookup"><span data-stu-id="cab45-180">hello PNS could ban your traffic as a result of such attacks.</span></span>

## <a name="more-information"></a><span data-ttu-id="cab45-181">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="cab45-181">More information</span></span>

<span data-ttu-id="cab45-182">Ayrıntılı API ayrıntılarda bulabilirsiniz bizim [API belgelerine](http://azure.github.io/azure-mobile-apps-js-client/).</span><span class="sxs-lookup"><span data-stu-id="cab45-182">You can find detailed API details in our [API documentation](http://azure.github.io/azure-mobile-apps-js-client/).</span></span>

<!-- URLs. -->
[Azure portalı]: https://portal.azure.com
[Azure Mobile Apps Hızlı Başlangıç]: app-service-mobile-cordova-get-started.md
[kimlik doğrulamayı kullanmaya başlama]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[Azure Mobile Apps için Apache Cordova eklentisi]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps
[ilk Apache Cordova uygulamanızı]: http://cordova.apache.org/#getstarted
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
[phonegap eklentiyi itme]: https://www.npmjs.com/package/phonegap-plugin-push
[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device
[cordova eklentisi inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
