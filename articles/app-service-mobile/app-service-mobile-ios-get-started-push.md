---
title: "aaaAdd anında iletme bildirimleri tooiOS Azure Mobile Apps ile uygulama"
description: "Nasıl toouse Azure Mobile Apps toosend anında bildirimler tooyour iOS uygulaması hakkında bilgi edinin."
services: app-service\mobile
documentationcenter: ios
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: fa503833-d23e-4925-8d93-341bb3fbab7d
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/10/2016
ms.author: glenga
ms.openlocfilehash: 11588c56bc8987a71257dbad4fcdebf1b3209b1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-ios-app"></a>Anında iletme bildirimleri tooyour iOS uygulaması ekleyin
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Genel Bakış
Bu öğreticide, eklediğiniz anında iletme bildirimleri toohello [iOS Hızlı Başlat] bir kayda eklenen her zaman bir anında iletme bildirimi toohello aygıt gönderilen böylece proje.

Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, anında iletme bildirimi uzantısı paketi hello. Bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) daha fazla bilgi için.

Merhaba [iOS simülatörü anında iletme bildirimlerini desteklemiyor](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html). Fiziksel bir iOS cihazına gerekir ve bir [Apple Developer Program üyeliği](https://developer.apple.com/programs/ios/).

## <a name="configure-hub"></a>Bildirim hub'ı yapılandırma
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a id="register"></a>Anında iletme bildirimleri için uygulamanızı kaydetmeniz
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-toosend-push-notifications"></a>Azure toosend anında iletme bildirimleri yapılandırma
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a id="update-server"></a>Arka uç toosend anında iletme bildirimleri güncelleştir
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <a id="add-push"></a>Anında iletme bildirimleri tooapp Ekle
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <a id="test"></a>Test anında iletme bildirimleri
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <a id="more"></a>Daha fazla
* Şablonları esneklik toosend platformlar arası gönderim ve yerelleştirilmiş iter verin. [Nasıl tooUse iOS için Azure Mobile Apps istemci Kitaplığı](app-service-mobile-ios-how-to-use-client-library.md#templates) nasıl gösterir tooregister şablonları.

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
[iOS Hızlı Başlat]: app-service-mobile-ios-get-started.md
