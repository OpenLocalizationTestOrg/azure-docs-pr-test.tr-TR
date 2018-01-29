---
title: "İOS uygulaması ile Azure Mobile Apps için anında iletme bildirimleri ekleme"
description: "İOS uygulamanıza anında iletme bildirimleri göndermek için Azure Mobile Apps kullanmayı öğrenin."
services: app-service\mobile
documentationcenter: ios
manager: crdun
editor: 
author: conceptdev
ms.assetid: fa503833-d23e-4925-8d93-341bb3fbab7d
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/10/2016
ms.author: crdun
ms.openlocfilehash: 063926a5a98aeab62e191d372831a00c29b9f6d7
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/04/2018
---
# <a name="add-push-notifications-to-your-ios-app"></a>İOS uygulamasına anında iletme bildirimleri ekleme
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Genel Bakış
Bu öğreticide, anında iletme bildirimleri ekleme [iOS Hızlı Başlat] proje böylece bir kayda eklenen her zaman bir anında iletme bildirimi cihaza gönderilir.

İndirilen hızlı başlangıç sunucu projesi kullanmazsanız, anında iletme bildirimi uzantısı paketi gerekir. Bkz: [.NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) daha fazla bilgi için.

[İOS simülatörü anında iletme bildirimlerini desteklemiyor](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html). Fiziksel bir iOS cihazına gerekir ve bir [Apple Developer Program üyeliği](https://developer.apple.com/programs/ios/).

## <a name="configure-hub"></a>Bildirim hub'ı yapılandırma
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a id="register"></a>Anında iletme bildirimleri için uygulamanızı kaydetmeniz
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-to-send-push-notifications"></a>Anında iletme bildirimleri göndermek için Azure yapılandırma
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a id="update-server"></a>Anında iletme bildirimleri göndermek için arka uç güncelleştir
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <a id="add-push"></a>Uygulamasına anında iletme bildirimleri ekleme
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <a id="test"></a>Test anında iletme bildirimleri
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <a id="more"></a>Daha fazla
* Şablonları platformlar arası gönderim ve yerelleştirilmiş bildirim göndermek için esneklik sağlar. [Kullanım iOS için Azure Mobile Apps istemci kitaplığı nasıl](app-service-mobile-ios-how-to-use-client-library.md#templates) şablonlarını kaydetmek gösterilmektedir.

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
[iOS Hızlı Başlat]: app-service-mobile-ios-get-started.md
