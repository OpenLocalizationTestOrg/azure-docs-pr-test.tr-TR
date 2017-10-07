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
# <a name="token-based-http2-authentication-for-apns"></a>APNS için belirteç tabanlı (HTTP/2) kimlik doğrulaması
## <a name="overview"></a>Genel Bakış
Bu makalede nasıl toouse hello yeni APNS HTTP/2 protokolüyle belirteç tabanlı kimlik doğrulaması ayrıntıları verilmektedir.

Merhaba yeni protokolünü kullanarak hello avantajları şunlardır:
-   Belirteci oluşturma görece mücadele boş (karşılaştırılan toocertificates) değil
-   Daha fazla hiçbir bitiş tarihlerini – kimlik doğrulama belirteçleri ve bunların iptal denetiminde olan
-   Yükü artık too4 KB olabilir
- Eşzamanlı geri bildirim
-   Apple'nın en son protokolünü dileriz – sertifikaları kullanmaya devam kullanımdan kaldırma için işaretli hello ikili Protokolü

Bu yeni mekanizmayı kullanarak iki adımda birkaç dakika içinde yapılabilir:
1.  Merhaba gerekli bilgileri hello Apple Developer hesabı portaldan alın
2.  Merhaba yeni bilgilerle bildirim hub'ınızı yapılandırma

Bildirim hub'ları sistemidir şimdi tüm kümesi toouse hello yeni kimlik doğrulama APNS ile. 

APNS için sertifika kimlik bilgilerini kullanarak geçirdiyseniz dikkat edin:
- Merhaba belirteci özellikleri sertifikanızı sistemimizde üzerine yazma
- Ancak, uygulamanızın tooreceive bildirimleri sorunsuz bir şekilde devam eder.

## <a name="obtaining-authentication-information-from-apple"></a>Apple'dan kimlik doğrulama bilgilerini alma
tooenable belirteç tabanlı kimlik doğrulaması, aşağıdaki özelliklere Apple Developer hesabınızdan hello gerekir:
### <a name="key-identifier"></a>Anahtarı tanımlayıcısı
başlangıç anahtarı tanımlayıcısı Apple Geliştirici hesabınızda hello "Anahtarlar" sayfasından elde edilebilir

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a>Uygulama tanımlayıcısı & Uygulama adı
Merhaba uygulama adı, hello uygulama kimlikleri hello Geliştirici hesabını sayfasında aracılığıyla kullanılabilir. 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

Merhaba uygulama tanımlayıcısı hello üyelik Ayrıntıları sayfasında hello Geliştirici hesabını aracılığıyla kullanılabilir.
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a>Kimlik doğrulama belirteci
Uygulamanız için bir belirteç oluşturmak sonra hello kimlik doğrulama belirteci indirilebilir. Nasıl toogenerate bu simge, Ayrıntılar başvurmak için çok[Apple Geliştirici belgeleri](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).

## <a name="configuring-your-notification-hub-toouse-token-based-authentication"></a>Bildirim hub'ı toouse belirteç tabanlı kimlik doğrulamasını yapılandırma
### <a name="configure-via-hello-azure-portal"></a>Hello Azure portal yapılandırın
tooenable belirteç tabanlı kimlik doğrulaması hello portalında toohello Azure portal günlüğüne ve tooyour bildirim hub'ı Git > Bildirim Hizmetleri > APNS paneli. 

Yeni bir özellik – yoktur *kimlik doğrulama modu*. Belirteç seçilmesine olanak sağlar, tooupdate hub'ınızı tüm hello ilgili belirteci özelliklere sahip.

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- Apple Geliştirici hesabınızdan alınan hello özelliklerini girin 
- uygulama modu (üretim veya korumalı alan) seçin 
- APNS kimlik bilgilerinizi tooupdate Kaydet'i tıklatın. 

### <a name="configure-via-management-api-rest"></a>Yönetim API'si (REST) yapılandırın

Kullanabileceğiniz bizim [Yönetimi API'leri](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate, bildirim hub'ı toouse belirteç tabanlı kimlik doğrulaması.
Yapılandırmakta Merhaba uygulaması (Apple Geliştirici hesabınızda belirtilen) bir korumalı alan veya üretim uygulaması olup bağlı olarak, karşılık gelen uç noktaları hello birini kullanın:

- Korumalı alan uç noktası: [3/https://api.development.push.apple.com:443/aygıt](https://api.development.push.apple.com:443/3/device)
- Üretim uç noktası: [3/https://api.push.apple.com:443/aygıt](https://api.push.apple.com:443/3/device)

> [!IMPORTANT]
> Belirteç tabanlı kimlik doğrulaması gerektiren bir API sürümü: **2017-04 ya da daha sonra**.
> 
> 

PUT istek tooupdate belirteç tabanlı kimlik doğrulaması olan bir hub örneği şöyledir:


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
        

### <a name="configure-via-hello-net-sdk"></a>.NET SDK'sı Hello yapılandırın
Hub toouse belirteç tabanlı kimlik doğrulamasını kullanarak yapılandırabilirsiniz bizim [son istemci SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8). 

Merhaba doğru kullanımını gösteren kod örneği şöyledir:


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH tooYOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-toousing-certificate-based-authentication"></a>Geri alma toousing sertifika tabanlı kimlik doğrulaması
Merhaba belirteci özellikleri yerine önceki yöntemi ve geçirerek hello sertifika kullanarak her zaman toousing sertifika tabanlı kimlik doğrulaması sırasında geri dönebilirsiniz. Eylemin hello üzerine yazar daha önce depolanan kimlik bilgileri.
