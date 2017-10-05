---
title: "Belirteç tabanlı (HTTP/2) kimlik doğrulaması için Azure Notification Hubs APNS | Microsoft Docs"
description: "Bu konuda, yeni belirteç kimlik doğrulama APNS için yararlanacağınızı açıklanmaktadır"
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
ms.openlocfilehash: 5a21bcd9f12fc3f96b17a556ba15526c35ababe2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="token-based-http2-authentication-for-apns"></a><span data-ttu-id="f223d-103">APNS için belirteç tabanlı (HTTP/2) kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="f223d-103">Token-based (HTTP/2) Authentication for APNS</span></span>
## <a name="overview"></a><span data-ttu-id="f223d-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f223d-104">Overview</span></span>
<span data-ttu-id="f223d-105">Bu makalede yeni APNS HTTP/2 protokolü belirteç tabanlı kimlik doğrulaması ile kullanmak nasıl ayrıntılarını verir.</span><span class="sxs-lookup"><span data-stu-id="f223d-105">This article details how to use the new APNS HTTP/2 protocol with token based authentication.</span></span>

<span data-ttu-id="f223d-106">Yeni protokolünü kullanmanın avantajları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f223d-106">The key benefits of using the new protocol include:</span></span>
-   <span data-ttu-id="f223d-107">Belirteci oluşturma mücadele boş (sertifikaları karşılaştırıldığında) görece olduğu</span><span class="sxs-lookup"><span data-stu-id="f223d-107">Token generation is relatively hassle free (compared to certificates)</span></span>
-   <span data-ttu-id="f223d-108">Daha fazla hiçbir bitiş tarihlerini – kimlik doğrulama belirteçleri ve bunların iptal denetiminde olan</span><span class="sxs-lookup"><span data-stu-id="f223d-108">No more expiry dates – you are in control of your authentication tokens and their revocation</span></span>
-   <span data-ttu-id="f223d-109">Yükü artık en fazla 4 KB olabilir</span><span class="sxs-lookup"><span data-stu-id="f223d-109">Payloads can now be up to 4 KB</span></span>
- <span data-ttu-id="f223d-110">Eşzamanlı geri bildirim</span><span class="sxs-lookup"><span data-stu-id="f223d-110">Synchronous feedback</span></span>
-   <span data-ttu-id="f223d-111">Apple'nın en son protokolünü dileriz – sertifikaları kullanmaya devam kullanımdan kaldırma için işaretli ikili Protokolü</span><span class="sxs-lookup"><span data-stu-id="f223d-111">You’re on Apple’s latest protocol – certificates still use the binary protocol, which is marked for deprecation</span></span>

<span data-ttu-id="f223d-112">Bu yeni mekanizmayı kullanarak iki adımda birkaç dakika içinde yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="f223d-112">Using this new mechanism can be done in two steps in a few minutes:</span></span>
1.  <span data-ttu-id="f223d-113">Apple Geliştirici hesap portalından gerekli bilgileri edinmenize</span><span class="sxs-lookup"><span data-stu-id="f223d-113">Obtain the necessary information from the Apple Developer Account portal</span></span>
2.  <span data-ttu-id="f223d-114">Yeni bilgilerle bildirim hub'ınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f223d-114">Configure your notification hub with the new information</span></span>

<span data-ttu-id="f223d-115">Bildirim hub'ları olan şimdi APNS ile yeni kimlik doğrulama sistemi kullanmak için tüm kümesi.</span><span class="sxs-lookup"><span data-stu-id="f223d-115">Notification Hubs is now all set to use the new authentication system with APNS.</span></span> 

<span data-ttu-id="f223d-116">APNS için sertifika kimlik bilgilerini kullanarak geçirdiyseniz dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="f223d-116">Note that if you migrated from using certificate credentials for APNS:</span></span>
- <span data-ttu-id="f223d-117">belirteç özellikleri sertifikanızı sistemimizde üzerine yazma</span><span class="sxs-lookup"><span data-stu-id="f223d-117">the token properties overwrite your certificate in our system,</span></span>
- <span data-ttu-id="f223d-118">ancak sorunsuz bildirimleri almak uygulamanızı devam eder.</span><span class="sxs-lookup"><span data-stu-id="f223d-118">but your application continues to receive notifications seamlessly.</span></span>

## <a name="obtaining-authentication-information-from-apple"></a><span data-ttu-id="f223d-119">Apple'dan kimlik doğrulama bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="f223d-119">Obtaining authentication information from Apple</span></span>
<span data-ttu-id="f223d-120">Belirteç tabanlı kimlik doğrulamasını etkinleştirmek için aşağıdaki özellikleri Apple Developer hesabınızdan gerekir:</span><span class="sxs-lookup"><span data-stu-id="f223d-120">To enable token-based authentication, you need the following properties from your Apple Developer Account:</span></span>
### <a name="key-identifier"></a><span data-ttu-id="f223d-121">Anahtarı tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="f223d-121">Key Identifier</span></span>
<span data-ttu-id="f223d-122">Apple Geliştirici hesabınızda "Anahtarlar" sayfasından anahtarı tanımlayıcısı alınabilir</span><span class="sxs-lookup"><span data-stu-id="f223d-122">The key identifier can be obtained from the "Keys" page in your Apple Developer Account</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a><span data-ttu-id="f223d-123">Uygulama tanımlayıcısı & Uygulama adı</span><span class="sxs-lookup"><span data-stu-id="f223d-123">Application Identifier & Application Name</span></span>
<span data-ttu-id="f223d-124">Uygulama adı, geliştirici hesabını uygulama kimlikleri sayfasında aracılığıyla kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f223d-124">The application name is available via the App IDs page in the Developer Account.</span></span> 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

<span data-ttu-id="f223d-125">Uygulama tanımlayıcısı, geliştirici hesabını üyelik Ayrıntıları sayfasında aracılığıyla kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f223d-125">The application identifier is available via the membership details page in the Developer Account.</span></span>
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a><span data-ttu-id="f223d-126">Kimlik doğrulama belirteci</span><span class="sxs-lookup"><span data-stu-id="f223d-126">Authentication token</span></span>
<span data-ttu-id="f223d-127">Uygulamanız için bir belirteç oluşturmak sonra kimlik doğrulama belirteci indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="f223d-127">The authentication token can be downloaded after you generate a token for your application.</span></span> <span data-ttu-id="f223d-128">Bu belirteci üretmek nasıl hakkında daha fazla bilgi için başvurmak [Apple Geliştirici belgeleri](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span><span class="sxs-lookup"><span data-stu-id="f223d-128">For details on how to generate this token, refer to [Apple’s Developer documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span></span>

## <a name="configuring-your-notification-hub-to-use-token-based-authentication"></a><span data-ttu-id="f223d-129">Belirteç tabanlı kimlik doğrulaması kullanacak şekilde bildirim hub'ınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f223d-129">Configuring your notification hub to use token-based authentication</span></span>
### <a name="configure-via-the-azure-portal"></a><span data-ttu-id="f223d-130">Azure portalı üzerinden yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f223d-130">Configure via the Azure portal</span></span>
<span data-ttu-id="f223d-131">Portalda belirteç tabanlı kimlik doğrulamasını etkinleştirmek için Azure portalında oturum açın ve bildirim Hub'ına gidin > Bildirim Hizmetleri > APNS paneli.</span><span class="sxs-lookup"><span data-stu-id="f223d-131">To enable token based authentication in the portal, log in to the Azure portal and go to your Notification Hub > Notification Services > APNS panel.</span></span> 

<span data-ttu-id="f223d-132">Yeni bir özellik – yoktur *kimlik doğrulama modu*.</span><span class="sxs-lookup"><span data-stu-id="f223d-132">There is a new property – *Authentication Mode*.</span></span> <span data-ttu-id="f223d-133">Belirteç seçerek, tüm ilgili belirteci özellikleri ile hub'ınızı güncelleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="f223d-133">Selecting Token allows you to update your hub with all the relevant token properties.</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- <span data-ttu-id="f223d-134">Apple Geliştirici hesabınızdan alınan özelliklerini girin</span><span class="sxs-lookup"><span data-stu-id="f223d-134">Enter the properties you retrieved from your Apple developer account,</span></span> 
- <span data-ttu-id="f223d-135">uygulama modu (üretim veya korumalı alan) seçin</span><span class="sxs-lookup"><span data-stu-id="f223d-135">choose your application mode (Production or Sandbox)</span></span> 
- <span data-ttu-id="f223d-136">APNS kimlik bilgilerinizi güncelleştirmek için Kaydet'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f223d-136">click Save to update your APNS credentials.</span></span> 

### <a name="configure-via-management-api-rest"></a><span data-ttu-id="f223d-137">Yönetim API'si (REST) yapılandırın</span><span class="sxs-lookup"><span data-stu-id="f223d-137">Configure via Management API (REST)</span></span>

<span data-ttu-id="f223d-138">Kullanabileceğiniz bizim [Yönetimi API'leri](https://msdn.microsoft.com/library/azure/dn495827.aspx) belirteç tabanlı kimlik doğrulamasını kullanmak için bildirim hub'ı güncelleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f223d-138">You can use our [management APIs](https://msdn.microsoft.com/library/azure/dn495827.aspx) to update your notification hub to use token-based authentication.</span></span>
<span data-ttu-id="f223d-139">Yapılandırmakta uygulamanın (Apple Geliştirici hesabınızda belirtilen) bir korumalı alan veya üretim uygulaması olup bağlı olarak, karşılık gelen uç noktaları birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="f223d-139">Depending on whether the application you’re configuring is a Sandbox or Production app (specified in your Apple Developer Account), use one of the corresponding endpoints:</span></span>

- <span data-ttu-id="f223d-140">Korumalı alan uç noktası: [3/https://api.development.push.apple.com:443/aygıt](https://api.development.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="f223d-140">Sandbox Endpoint: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span></span>
- <span data-ttu-id="f223d-141">Üretim uç noktası: [3/https://api.push.apple.com:443/aygıt](https://api.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="f223d-141">Production Endpoint: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f223d-142">Belirteç tabanlı kimlik doğrulaması gerektiren bir API sürümü: **2017-04 ya da daha sonra**.</span><span class="sxs-lookup"><span data-stu-id="f223d-142">Token-based authentication requires an API version of: **2017-04 or later**.</span></span>
> 
> 

<span data-ttu-id="f223d-143">Belirteç tabanlı kimlik doğrulaması ile bir hub'ı güncelleştirmek için bir PUT İsteği bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f223d-143">Here’s an example of a PUT request to update a hub with token-based authentication:</span></span>


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
        

### <a name="configure-via-the-net-sdk"></a><span data-ttu-id="f223d-144">.NET SDK'sı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="f223d-144">Configure via the .NET SDK</span></span>
<span data-ttu-id="f223d-145">Hub'ınızı belirteç tabanlı kimlik doğrulamasını kullanmak için yapılandırabilirsiniz bizim [son istemci SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span><span class="sxs-lookup"><span data-stu-id="f223d-145">You can configure your hub to use token based authentication using our [latest client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span></span> 

<span data-ttu-id="f223d-146">Doğru kullanımını gösteren kod örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="f223d-146">Here’s a code sample illustrating the correct usage:</span></span>


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH TO YOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-to-using-certificate-based-authentication"></a><span data-ttu-id="f223d-147">Sertifika tabanlı kimlik doğrulaması kullanmaya geri alma</span><span class="sxs-lookup"><span data-stu-id="f223d-147">Reverting to using certificate-based authentication</span></span>
<span data-ttu-id="f223d-148">Herhangi bir zamanda herhangi bir önceki yöntemini kullanarak ve belirteç özellikleri yerine sertifikanın geçirme sertifika tabanlı kimlik doğrulaması kullanmaya geri dönebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f223d-148">You can revert at any time to using certificate-based authentication by using any preceding method and passing the certificate instead of the token properties.</span></span> <span data-ttu-id="f223d-149">Bu eylem, önceden depolanan kimlik bilgileri üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="f223d-149">That action overwrites the previously stored credentials.</span></span>
