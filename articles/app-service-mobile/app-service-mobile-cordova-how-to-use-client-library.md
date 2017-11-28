---
title: "Apache Cordova eklentisi için Azure Mobile Apps kullanma"
description: "Apache Cordova eklentisi için Azure Mobile Apps kullanma"
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
ms.openlocfilehash: ebf0e911eeada0e529f908dd3e3430c94edae763
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-apache-cordova-client-library-for-azure-mobile-apps"></a><span data-ttu-id="4749d-103">Azure Mobile Apps için Apache Cordova istemci kitaplığını kullanma</span><span class="sxs-lookup"><span data-stu-id="4749d-103">How to use Apache Cordova client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="4749d-104">En son kullanılarak yaygın senaryolar gerçekleştirmek için bu kılavuzu öğretilmektedir [Azure Mobile Apps için Apache Cordova eklentisi].</span><span class="sxs-lookup"><span data-stu-id="4749d-104">This guide teaches you to perform common scenarios using the latest [Apache Cordova Plugin for Azure Mobile Apps].</span></span> <span data-ttu-id="4749d-105">Azure Mobile Apps yeniyseniz, ilk tamamlamak [Azure Mobile Apps Hızlı Başlangıç] bir arka uç oluşturmak için bir tablo oluşturun ve önceden oluşturulmuş bir Apache Cordova projenizi indirin.</span><span class="sxs-lookup"><span data-stu-id="4749d-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend, create a table, and download a pre-built Apache Cordova project.</span></span> <span data-ttu-id="4749d-106">Bu kılavuzda, istemci-tarafı Apache Cordova eklentisi üzerinde odaklanın.</span><span class="sxs-lookup"><span data-stu-id="4749d-106">In this guide, we focus on the client-side Apache Cordova Plugin.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="4749d-107">Desteklenen platformlar</span><span class="sxs-lookup"><span data-stu-id="4749d-107">Supported platforms</span></span>
<span data-ttu-id="4749d-108">Apache Cordova v6.0.0 ve daha sonra iOS, Android ve Windows bu SDK destekleyen cihazlar.</span><span class="sxs-lookup"><span data-stu-id="4749d-108">This SDK supports Apache Cordova v6.0.0 and later on iOS, Android, and Windows devices.</span></span>  <span data-ttu-id="4749d-109">Platform desteği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="4749d-109">The platform support is as follows:</span></span>

* <span data-ttu-id="4749d-110">Android API 19-24 (KitKat Nougat aracılığıyla).</span><span class="sxs-lookup"><span data-stu-id="4749d-110">Android API 19-24 (KitKat through Nougat).</span></span>
* <span data-ttu-id="4749d-111">iOS 8.0 ve sonraki sürümleri.</span><span class="sxs-lookup"><span data-stu-id="4749d-111">iOS versions 8.0 and later.</span></span>
* <span data-ttu-id="4749d-112">Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="4749d-112">Windows Phone 8.1.</span></span>
* <span data-ttu-id="4749d-113">Evrensel Windows platformu.</span><span class="sxs-lookup"><span data-stu-id="4749d-113">Universal Windows Platform.</span></span>

## <span data-ttu-id="4749d-114"><a name="Setup"></a>Kurulum ve Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="4749d-114"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="4749d-115">Bu kılavuz, bir tablo ile bir arka uç oluşturduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="4749d-115">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="4749d-116">Bu kılavuz tablo bu öğreticiler aynı şemaya tabloları sahip olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="4749d-116">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span> <span data-ttu-id="4749d-117">Bu kılavuz ayrıca kodunuz için Apache Cordova eklentisi eklediğiniz varsayar.</span><span class="sxs-lookup"><span data-stu-id="4749d-117">This guide also assumes that you have added the Apache Cordova Plugin to your code.</span></span>  <span data-ttu-id="4749d-118">Bunu yapmadıysanız komut satırında projenize Apache Cordova eklentisi ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4749d-118">If you have not done so, you may add the Apache Cordova plugin to your project on the command line:</span></span>

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="4749d-119">Oluşturma hakkında daha fazla bilgi için [ilk Apache Cordova uygulamanızı], kendi belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="4749d-119">For more information on creating [your first Apache Cordova app], see their documentation.</span></span>

## <span data-ttu-id="4749d-120"><a name="ionic"></a>Ionic v2 uygulama ayarlama</span><span class="sxs-lookup"><span data-stu-id="4749d-120"><a name="ionic"></a>Setting up an Ionic v2 app</span></span>

<span data-ttu-id="4749d-121">Ionic v2 projesinde düzgün bir şekilde yapılandırmak için önce temel bir uygulama oluşturun ve Cordova eklentisi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4749d-121">To properly configure an Ionic v2 project, first create a basic app and add the Cordova plugin:</span></span>

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="4749d-122">Aşağıdaki satırları ekleyin `app.component.ts` istemci nesnesi oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="4749d-122">Add the following lines to `app.component.ts` to create the client object:</span></span>

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

<span data-ttu-id="4749d-123">Şimdi oluşturun ve projeyi tarayıcıda çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4749d-123">You can now build and run the project in the browser:</span></span>

```
ionic platform add browser
ionic run browser
```

<span data-ttu-id="4749d-124">Azure Mobile Apps Cordova eklentisi her iki Ionic v1 ve v2 uygulamaları destekler.</span><span class="sxs-lookup"><span data-stu-id="4749d-124">The Azure Mobile Apps Cordova plugin supports both Ionic v1 and v2 apps.</span></span>  <span data-ttu-id="4749d-125">Ionic v2 uygulamalar için ek bildirim gerektiriyor yalnızca `WindowsAzure` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="4749d-125">Only the Ionic v2 apps require the additional declaration for the `WindowsAzure` object.</span></span>

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="4749d-126"><a name="auth"></a>Nasıl yapılır: kullanıcıların kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="4749d-126"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="4749d-127">Azure uygulama hizmeti, kimlik doğrulaması ve çeşitli dış kimlik sağlayıcılarını kullanarak uygulama kullanıcıları yetkilendirmek destekler: Facebook, Google, Microsoft Account ve Twitter.</span><span class="sxs-lookup"><span data-stu-id="4749d-127">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="4749d-128">Yalnızca kimliği doğrulanmış kullanıcılar için belirli işlemler için erişimi kısıtlamak için tablolarda izinlerini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4749d-128">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="4749d-129">Kimliği doğrulanmış kullanıcıların kimliğini, sunucu komut dosyalarında yetkilendirme kuralları uygulamak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4749d-129">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="4749d-130">Daha fazla bilgi için bkz: [kimlik doğrulamayı kullanmaya başlama] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="4749d-130">For more information, see the [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="4749d-131">Kimlik doğrulaması bir Apache Cordova uygulaması kullanırken, aşağıdaki Cordova eklenti kullanılabilir olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="4749d-131">When using authentication in an Apache Cordova app, the following Cordova plugins must be available:</span></span>

* <span data-ttu-id="4749d-132">[cordova-plugin-device]</span><span class="sxs-lookup"><span data-stu-id="4749d-132">[cordova-plugin-device]</span></span>
* <span data-ttu-id="4749d-133">[cordova eklentisi inappbrowser]</span><span class="sxs-lookup"><span data-stu-id="4749d-133">[cordova-plugin-inappbrowser]</span></span>

<span data-ttu-id="4749d-134">İki kimlik doğrulama akışı desteklenir: sunucu akışı ve bir istemci akışı.</span><span class="sxs-lookup"><span data-stu-id="4749d-134">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="4749d-135">Sağlayıcının web kimlik doğrulaması arabirimde alacağından sunucu akış Basit kimlik doğrulama deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="4749d-135">The server flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="4749d-136">Gibi istemci akışı aygıta özgü özellikleri ile daha derin tümleştirme sağlar çoklu oturum açma sağlayıcıya özgü aygıta özgü SDK'ları üzerinde alacağından.</span><span class="sxs-lookup"><span data-stu-id="4749d-136">The client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific device-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="4749d-137"><a name="configure-external-redirect-urls"></a>Nasıl yapılır: Mobil uygulama hizmetiniz için dış yönlendirme URL'lerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4749d-137"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="4749d-138">Apache Cordova uygulamaları çeşitli OAuth UI akışları işlemek için bir geri döngü özelliği kullanır.</span><span class="sxs-lookup"><span data-stu-id="4749d-138">Several types of Apache Cordova applications use a loopback capability to handle OAuth UI flows.</span></span>  <span data-ttu-id="4749d-139">Kimlik doğrulama hizmeti varsayılan olarak, hizmeti kullanmaya nasıl yalnızca bilir beri OAuth UI akışları localhost üzerinde sorunlara neden olur.</span><span class="sxs-lookup"><span data-stu-id="4749d-139">OAuth UI flows on localhost cause problems since the authentication service only knows how to utilize your service by default.</span></span>  <span data-ttu-id="4749d-140">Sorunlu OAuth UI akışları örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4749d-140">Examples of problematic OAuth UI flows include:</span></span>

* <span data-ttu-id="4749d-141">Ripple öykünücüsü.</span><span class="sxs-lookup"><span data-stu-id="4749d-141">The Ripple emulator.</span></span>
* <span data-ttu-id="4749d-142">Yeniden Ionic ile canlı.</span><span class="sxs-lookup"><span data-stu-id="4749d-142">Live Reload with Ionic.</span></span>
* <span data-ttu-id="4749d-143">Mobil arka uç yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="4749d-143">Running the mobile backend locally</span></span>
* <span data-ttu-id="4749d-144">Mobil arka uç bir sağlayan kimlik doğrulama'den farklı bir Azure uygulama hizmeti çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="4749d-144">Running the mobile backend in a different Azure App Service than the one providing authentication.</span></span>

<span data-ttu-id="4749d-145">Yerel ayarlarınızı yapılandırmaya eklemek için bu yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="4749d-145">Follow these instructions to add your local settings to the configuration:</span></span>

1. <span data-ttu-id="4749d-146">[Azure portalı]’nda oturum açın</span><span class="sxs-lookup"><span data-stu-id="4749d-146">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="4749d-147">Seçin **tüm kaynakları** veya **uygulama hizmetleri** mobil uygulamanızın adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4749d-147">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="4749d-148">Tıklatın **araçları**</span><span class="sxs-lookup"><span data-stu-id="4749d-148">Click **Tools**</span></span>
4. <span data-ttu-id="4749d-149">Tıklatın **kaynak Gezgini** GÖZLEMLE menüde ardından **Git**.</span><span class="sxs-lookup"><span data-stu-id="4749d-149">Click **Resource explorer** in the OBSERVE menu, then click **Go**.</span></span>  <span data-ttu-id="4749d-150">Yeni bir pencere veya sekmesinde açar.</span><span class="sxs-lookup"><span data-stu-id="4749d-150">A new window or tab opens.</span></span>
5. <span data-ttu-id="4749d-151">Genişletme **config**, **authsettings** düğümleri için sol gezinti sitenizdeki.</span><span class="sxs-lookup"><span data-stu-id="4749d-151">Expand the **config**, **authsettings** nodes for your site in the left-hand navigation.</span></span>
6. <span data-ttu-id="4749d-152">Tıklatın **Düzenle**</span><span class="sxs-lookup"><span data-stu-id="4749d-152">Click **Edit**</span></span>
7. <span data-ttu-id="4749d-153">"AllowedExternalRedirectUrls" öğesini arayın.</span><span class="sxs-lookup"><span data-stu-id="4749d-153">Look for the "allowedExternalRedirectUrls" element.</span></span>  <span data-ttu-id="4749d-154">Null ya da bir dizi değere ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="4749d-154">It may be set to null or an array of values.</span></span>  <span data-ttu-id="4749d-155">Değer şu değere değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4749d-155">Change the value to the following value:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="4749d-156">URL'leri hizmetinizi URL'ler ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4749d-156">Replace the URLs with the URLs of your service.</span></span>  <span data-ttu-id="4749d-157">(İçin Node.js örnek hizmeti) "http://localhost: 3000" veya "http://localhost:4400" (Ripple hizmeti için) örnek olarak verilebilir.</span><span class="sxs-lookup"><span data-stu-id="4749d-157">Examples include "http://localhost:3000" (for the Node.js sample service), or "http://localhost:4400" (for the Ripple service).</span></span>  <span data-ttu-id="4749d-158">Ancak, bu URL'ler örnekler - örneklerde, belirtilen Hizmetleri dahil olmak üzere durumunuz farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="4749d-158">However, these URLs are examples - your situation, including for the services mentioned in the examples, may be different.</span></span>
8. <span data-ttu-id="4749d-159">Tıklatın **okuma/yazma** ekranın sağ üst köşesindeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4749d-159">Click the **Read/Write** button in the top-right corner of the screen.</span></span>
9. <span data-ttu-id="4749d-160">Yeşil tıklatın **PUT** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4749d-160">Click the green **PUT** button.</span></span>

<span data-ttu-id="4749d-161">Bu noktada kaydedilmiş ayarları.</span><span class="sxs-lookup"><span data-stu-id="4749d-161">The settings are saved at this point.</span></span>  <span data-ttu-id="4749d-162">Ayarları bitinceye kadar tarayıcı penceresini kapatmayın kaydediliyor.</span><span class="sxs-lookup"><span data-stu-id="4749d-162">Do not close the browser window until the settings have finished saving.</span></span>
<span data-ttu-id="4749d-163">Ayrıca bu geri döngü URL'leri uygulama hizmetiniz için CORS ayarları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4749d-163">Also add these loopback URLs to the CORS settings for your App Service:</span></span>

1. <span data-ttu-id="4749d-164">[Azure portalı]’nda oturum açın</span><span class="sxs-lookup"><span data-stu-id="4749d-164">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="4749d-165">Seçin **tüm kaynakları** veya **uygulama hizmetleri** mobil uygulamanızın adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4749d-165">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="4749d-166">Ayarlar dikey penceresi otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="4749d-166">The Settings blade opens automatically.</span></span>  <span data-ttu-id="4749d-167">' I içermiyorsa tıklatırsanız **tüm ayarları**.</span><span class="sxs-lookup"><span data-stu-id="4749d-167">If it doesn't, click **All Settings**.</span></span>
4. <span data-ttu-id="4749d-168">Tıklatın **CORS** API menüsünün altında.</span><span class="sxs-lookup"><span data-stu-id="4749d-168">Click **CORS** under the API menu.</span></span>
5. <span data-ttu-id="4749d-169">Enter kutusunda eklemek istediğiniz URL sağlanan ve Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="4749d-169">Enter the URL that you wish to add in the box provided and press Enter.</span></span>
6. <span data-ttu-id="4749d-170">Gerektiğinde ek URL'leri girin.</span><span class="sxs-lookup"><span data-stu-id="4749d-170">Enter additional URLs as needed.</span></span>
7. <span data-ttu-id="4749d-171">Tıklatın **kaydetmek** ayarları kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="4749d-171">Click **Save** to save the settings.</span></span>

<span data-ttu-id="4749d-172">Yaklaşık olarak 10-15 etkili saniye yeni ayarları alır.</span><span class="sxs-lookup"><span data-stu-id="4749d-172">It takes approximately 10-15 seconds for the new settings to take effect.</span></span>

## <span data-ttu-id="4749d-173"><a name="register-for-push"></a>Nasıl yapılır: anında iletme bildirimleri için</span><span class="sxs-lookup"><span data-stu-id="4749d-173"><a name="register-for-push"></a>How to: Register for push notifications</span></span>
<span data-ttu-id="4749d-174">Yükleme [phonegap eklentiyi itme] anında iletme bildirimleri işlemek için.</span><span class="sxs-lookup"><span data-stu-id="4749d-174">Install the [phonegap-plugin-push] to handle push notifications.</span></span>  <span data-ttu-id="4749d-175">Bu eklenti kullanarak kolayca eklenebilen `cordova plugin add` komut satırında veya Visual Studio içinde Git eklentisi yükleyici aracılığıyla komutu.</span><span class="sxs-lookup"><span data-stu-id="4749d-175">This plugin can be easily added using the `cordova plugin add` command on the command line, or via the Git plugin installer within Visual Studio.</span></span>  <span data-ttu-id="4749d-176">Apache Cordova uygulamanızı aşağıdaki kodda Cihazınızı anında iletme bildirimleri için kaydeder:</span><span class="sxs-lookup"><span data-stu-id="4749d-176">The following code in your Apache Cordova app registers your device for push notifications:</span></span>

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
    // For cross-platform, you can use the device plugin to determine the device
    // Best is to use device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by the PNS - check the format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

<span data-ttu-id="4749d-177">Sunucudan anında iletme bildirimleri göndermek için Notification Hubs SDK'sı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4749d-177">Use the Notification Hubs SDK to send push notifications from the server.</span></span>  <span data-ttu-id="4749d-178">Hiçbir zaman doğrudan istemcilerden anında iletme bildirimleri gönderme.</span><span class="sxs-lookup"><span data-stu-id="4749d-178">Never send push notifications directly from clients.</span></span> <span data-ttu-id="4749d-179">Bunun yapılması bir hizmet reddi saldırısına karşı bildirim hub'ları veya PNS tetiklemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4749d-179">Doing so could be used to trigger a denial of service attack against Notification Hubs or the PNS.</span></span>  <span data-ttu-id="4749d-180">PNS trafiğinizi bu tür saldırıları sonucunda bSunucu.</span><span class="sxs-lookup"><span data-stu-id="4749d-180">The PNS could ban your traffic as a result of such attacks.</span></span>

## <a name="more-information"></a><span data-ttu-id="4749d-181">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="4749d-181">More information</span></span>

<span data-ttu-id="4749d-182">Ayrıntılı API ayrıntılarda bulabilirsiniz bizim [API belgelerine](http://azure.github.io/azure-mobile-apps-js-client/).</span><span class="sxs-lookup"><span data-stu-id="4749d-182">You can find detailed API details in our [API documentation](http://azure.github.io/azure-mobile-apps-js-client/).</span></span>

<!-- URLs. -->
<span data-ttu-id="4749d-183">[Azure portalı]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="4749d-183">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="4749d-184">[Azure Mobile Apps Hızlı Başlangıç]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="4749d-184">[Azure Mobile Apps Quick Start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="4749d-185">[kimlik doğrulamayı kullanmaya başlama]: app-service-mobile-cordova-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="4749d-185">[Get started with authentication]: app-service-mobile-cordova-get-started-users.md</span></span>
[Add authentication to your app]: app-service-mobile-cordova-get-started-users.md

<span data-ttu-id="4749d-186">[Azure Mobile Apps için Apache Cordova eklentisi]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps</span><span class="sxs-lookup"><span data-stu-id="4749d-186">[Apache Cordova Plugin for Azure Mobile Apps]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps</span></span>
<span data-ttu-id="4749d-187">[ilk Apache Cordova uygulamanızı]: http://cordova.apache.org/#getstarted</span><span class="sxs-lookup"><span data-stu-id="4749d-187">[your first Apache Cordova app]: http://cordova.apache.org/#getstarted</span></span>
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
<span data-ttu-id="4749d-188">[phonegap eklentiyi itme]: https://www.npmjs.com/package/phonegap-plugin-push</span><span class="sxs-lookup"><span data-stu-id="4749d-188">[phonegap-plugin-push]: https://www.npmjs.com/package/phonegap-plugin-push</span></span>
<span data-ttu-id="4749d-189">[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device</span><span class="sxs-lookup"><span data-stu-id="4749d-189">[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device</span></span>
<span data-ttu-id="4749d-190">[cordova eklentisi inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser</span><span class="sxs-lookup"><span data-stu-id="4749d-190">[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser</span></span>
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
