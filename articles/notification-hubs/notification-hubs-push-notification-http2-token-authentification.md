---
title: "aaaToken tabanlı (HTTP/2) kimlik doğrulaması için Azure Notification Hubs APNS | Microsoft Docs"
description: "Bu konuda, nasıl tooleverage hello APNS için yeni belirteç kimlik doğrulama açıklanmıştır."
services: notification-hubs
documentationcenter: .net
author: kpiteira
manager: erikre
editor: 
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 05/17/2017
ms.author: kapiteir
ms.openlocfilehash: 3353d7f16033ce0b68edec9ee9aeb98f47faa1fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="token-based-http2-authentication-for-apns"></a><span data-ttu-id="349e3-103">APNS için belirteç tabanlı (HTTP/2) kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="349e3-103">Token-based (HTTP/2) Authentication for APNS</span></span>
## <a name="overview"></a><span data-ttu-id="349e3-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="349e3-104">Overview</span></span>
<span data-ttu-id="349e3-105">Bu makalede nasıl toouse hello yeni APNS HTTP/2 protokolüyle belirteç tabanlı kimlik doğrulaması ayrıntıları verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="349e3-105">This article details how toouse hello new APNS HTTP/2 protocol with token based authentication.</span></span>

<span data-ttu-id="349e3-106">Merhaba yeni protokolünü kullanarak hello avantajları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="349e3-106">hello key benefits of using hello new protocol include:</span></span>
-   <span data-ttu-id="349e3-107">Belirteci oluşturma görece mücadele boş (karşılaştırılan toocertificates) değil</span><span class="sxs-lookup"><span data-stu-id="349e3-107">Token generation is relatively hassle free (compared toocertificates)</span></span>
-   <span data-ttu-id="349e3-108">Daha fazla hiçbir bitiş tarihlerini – kimlik doğrulama belirteçleri ve bunların iptal denetiminde olan</span><span class="sxs-lookup"><span data-stu-id="349e3-108">No more expiry dates – you are in control of your authentication tokens and their revocation</span></span>
-   <span data-ttu-id="349e3-109">Yükü artık too4 KB olabilir</span><span class="sxs-lookup"><span data-stu-id="349e3-109">Payloads can now be up too4 KB</span></span>
- <span data-ttu-id="349e3-110">Eşzamanlı geri bildirim</span><span class="sxs-lookup"><span data-stu-id="349e3-110">Synchronous feedback</span></span>
-   <span data-ttu-id="349e3-111">Apple'nın en son protokolünü dileriz – sertifikaları kullanmaya devam kullanımdan kaldırma için işaretli hello ikili Protokolü</span><span class="sxs-lookup"><span data-stu-id="349e3-111">You’re on Apple’s latest protocol – certificates still use hello binary protocol, which is marked for deprecation</span></span>

<span data-ttu-id="349e3-112">Bu yeni mekanizmayı kullanarak iki adımda birkaç dakika içinde yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="349e3-112">Using this new mechanism can be done in two steps in a few minutes:</span></span>
1.  <span data-ttu-id="349e3-113">Merhaba gerekli bilgileri hello Apple Developer hesabı portaldan alın</span><span class="sxs-lookup"><span data-stu-id="349e3-113">Obtain hello necessary information from hello Apple Developer Account portal</span></span>
2.  <span data-ttu-id="349e3-114">Merhaba yeni bilgilerle bildirim hub'ınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="349e3-114">Configure your notification hub with hello new information</span></span>

<span data-ttu-id="349e3-115">Bildirim hub'ları sistemidir şimdi tüm kümesi toouse hello yeni kimlik doğrulama APNS ile.</span><span class="sxs-lookup"><span data-stu-id="349e3-115">Notification Hubs is now all set toouse hello new authentication system with APNS.</span></span> 

<span data-ttu-id="349e3-116">APNS için sertifika kimlik bilgilerini kullanarak geçirdiyseniz dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="349e3-116">Note that if you migrated from using certificate credentials for APNS:</span></span>
- <span data-ttu-id="349e3-117">Merhaba belirteci özellikleri sertifikanızı sistemimizde üzerine yazma</span><span class="sxs-lookup"><span data-stu-id="349e3-117">hello token properties overwrite your certificate in our system,</span></span>
- <span data-ttu-id="349e3-118">Ancak, uygulamanızın tooreceive bildirimleri sorunsuz bir şekilde devam eder.</span><span class="sxs-lookup"><span data-stu-id="349e3-118">but your application continues tooreceive notifications seamlessly.</span></span>

## <a name="obtaining-authentication-information-from-apple"></a><span data-ttu-id="349e3-119">Apple'dan kimlik doğrulama bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="349e3-119">Obtaining authentication information from Apple</span></span>
<span data-ttu-id="349e3-120">tooenable belirteç tabanlı kimlik doğrulaması, aşağıdaki özelliklere Apple Developer hesabınızdan hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="349e3-120">tooenable token-based authentication, you need hello following properties from your Apple Developer Account:</span></span>
### <a name="key-identifier"></a><span data-ttu-id="349e3-121">Anahtarı tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="349e3-121">Key Identifier</span></span>
<span data-ttu-id="349e3-122">başlangıç anahtarı tanımlayıcısı Apple Geliştirici hesabınızda hello "Anahtarlar" sayfasından elde edilebilir</span><span class="sxs-lookup"><span data-stu-id="349e3-122">hello key identifier can be obtained from hello "Keys" page in your Apple Developer Account</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a><span data-ttu-id="349e3-123">Uygulama tanımlayıcısı & Uygulama adı</span><span class="sxs-lookup"><span data-stu-id="349e3-123">Application Identifier & Application Name</span></span>
<span data-ttu-id="349e3-124">Merhaba uygulama adı, hello uygulama kimlikleri hello Geliştirici hesabını sayfasında aracılığıyla kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="349e3-124">hello application name is available via hello App IDs page in hello Developer Account.</span></span> 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

<span data-ttu-id="349e3-125">Merhaba uygulama tanımlayıcısı hello üyelik Ayrıntıları sayfasında hello Geliştirici hesabını aracılığıyla kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="349e3-125">hello application identifier is available via hello membership details page in hello Developer Account.</span></span>
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a><span data-ttu-id="349e3-126">Kimlik doğrulama belirteci</span><span class="sxs-lookup"><span data-stu-id="349e3-126">Authentication token</span></span>
<span data-ttu-id="349e3-127">Uygulamanız için bir belirteç oluşturmak sonra hello kimlik doğrulama belirteci indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="349e3-127">hello authentication token can be downloaded after you generate a token for your application.</span></span> <span data-ttu-id="349e3-128">Nasıl toogenerate bu simge, Ayrıntılar başvurmak için çok[Apple Geliştirici belgeleri](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span><span class="sxs-lookup"><span data-stu-id="349e3-128">For details on how toogenerate this token, refer too[Apple’s Developer documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span></span>

## <a name="configuring-your-notification-hub-toouse-token-based-authentication"></a><span data-ttu-id="349e3-129">Bildirim hub'ı toouse belirteç tabanlı kimlik doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="349e3-129">Configuring your notification hub toouse token-based authentication</span></span>
### <a name="configure-via-hello-azure-portal"></a><span data-ttu-id="349e3-130">Hello Azure portal yapılandırın</span><span class="sxs-lookup"><span data-stu-id="349e3-130">Configure via hello Azure portal</span></span>
<span data-ttu-id="349e3-131">tooenable belirteç tabanlı kimlik doğrulaması hello portalında toohello Azure portal günlüğüne ve tooyour bildirim hub'ı Git > Bildirim Hizmetleri > APNS paneli.</span><span class="sxs-lookup"><span data-stu-id="349e3-131">tooenable token based authentication in hello portal, log in toohello Azure portal and go tooyour Notification Hub > Notification Services > APNS panel.</span></span> 

<span data-ttu-id="349e3-132">Yeni bir özellik – yoktur *kimlik doğrulama modu*.</span><span class="sxs-lookup"><span data-stu-id="349e3-132">There is a new property – *Authentication Mode*.</span></span> <span data-ttu-id="349e3-133">Belirteç seçilmesine olanak sağlar, tooupdate hub'ınızı tüm hello ilgili belirteci özelliklere sahip.</span><span class="sxs-lookup"><span data-stu-id="349e3-133">Selecting Token allows you tooupdate your hub with all hello relevant token properties.</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- <span data-ttu-id="349e3-134">Apple Geliştirici hesabınızdan alınan hello özelliklerini girin</span><span class="sxs-lookup"><span data-stu-id="349e3-134">Enter hello properties you retrieved from your Apple developer account,</span></span> 
- <span data-ttu-id="349e3-135">uygulama modu (üretim veya korumalı alan) seçin</span><span class="sxs-lookup"><span data-stu-id="349e3-135">choose your application mode (Production or Sandbox)</span></span> 
- <span data-ttu-id="349e3-136">APNS kimlik bilgilerinizi tooupdate Kaydet'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="349e3-136">click Save tooupdate your APNS credentials.</span></span> 

### <a name="configure-via-management-api-rest"></a><span data-ttu-id="349e3-137">Yönetim API'si (REST) yapılandırın</span><span class="sxs-lookup"><span data-stu-id="349e3-137">Configure via Management API (REST)</span></span>

<span data-ttu-id="349e3-138">Kullanabileceğiniz bizim [Yönetimi API'leri](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate, bildirim hub'ı toouse belirteç tabanlı kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="349e3-138">You can use our [management APIs](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate your notification hub toouse token-based authentication.</span></span>
<span data-ttu-id="349e3-139">Yapılandırmakta Merhaba uygulaması (Apple Geliştirici hesabınızda belirtilen) bir korumalı alan veya üretim uygulaması olup bağlı olarak, karşılık gelen uç noktaları hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="349e3-139">Depending on whether hello application you’re configuring is a Sandbox or Production app (specified in your Apple Developer Account), use one of hello corresponding endpoints:</span></span>

- <span data-ttu-id="349e3-140">Korumalı alan uç noktası: [3/https://api.development.push.apple.com:443/aygıt](https://api.development.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="349e3-140">Sandbox Endpoint: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span></span>
- <span data-ttu-id="349e3-141">Üretim uç noktası: [3/https://api.push.apple.com:443/aygıt](https://api.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="349e3-141">Production Endpoint: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="349e3-142">Belirteç tabanlı kimlik doğrulaması gerektiren bir API sürümü: **2017-04 ya da daha sonra**.</span><span class="sxs-lookup"><span data-stu-id="349e3-142">Token-based authentication requires an API version of: **2017-04 or later**.</span></span>
> 
> 

<span data-ttu-id="349e3-143">PUT istek tooupdate belirteç tabanlı kimlik doğrulaması olan bir hub örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="349e3-143">Here’s an example of a PUT request tooupdate a hub with token-based authentication:</span></span>


        PUT https://{namespace}.servicebus.windows.net/{Notification Hub}?api-version=2017-04
          "Properties": {
            "ApnsCredential": {
              "Properties": {
                "KeyId": "<Your Key Id>",
                "Token": "<Your Authentication Token>",
                "AppName": "<Your Application Name>",
                "AppId": "<Your Application Id>",
                "Endpoint":"<Sandbox/Production Endpoint>"
              }
            }
          }
        

### <a name="configure-via-hello-net-sdk"></a><span data-ttu-id="349e3-144">.NET SDK'sı Hello yapılandırın</span><span class="sxs-lookup"><span data-stu-id="349e3-144">Configure via hello .NET SDK</span></span>
<span data-ttu-id="349e3-145">Hub toouse belirteç tabanlı kimlik doğrulamasını kullanarak yapılandırabilirsiniz bizim [son istemci SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span><span class="sxs-lookup"><span data-stu-id="349e3-145">You can configure your hub toouse token based authentication using our [latest client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span></span> 

<span data-ttu-id="349e3-146">Merhaba doğru kullanımını gösteren kod örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="349e3-146">Here’s a code sample illustrating hello correct usage:</span></span>


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH tooYOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-toousing-certificate-based-authentication"></a><span data-ttu-id="349e3-147">Geri alma toousing sertifika tabanlı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="349e3-147">Reverting toousing certificate-based authentication</span></span>
<span data-ttu-id="349e3-148">Merhaba belirteci özellikleri yerine önceki yöntemi ve geçirerek hello sertifika kullanarak her zaman toousing sertifika tabanlı kimlik doğrulaması sırasında geri dönebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="349e3-148">You can revert at any time toousing certificate-based authentication by using any preceding method and passing hello certificate instead of hello token properties.</span></span> <span data-ttu-id="349e3-149">Eylemin hello üzerine yazar daha önce depolanan kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="349e3-149">That action overwrites hello previously stored credentials.</span></span>
