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
# <a name="add-push-notifications-tooyour-ios-app"></a><span data-ttu-id="d7420-103">Anında iletme bildirimleri tooyour iOS uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="d7420-103">Add Push Notifications tooyour iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="d7420-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d7420-104">Overview</span></span>
<span data-ttu-id="d7420-105">Bu öğreticide, eklediğiniz anında iletme bildirimleri toohello [iOS Hızlı Başlat] bir kayda eklenen her zaman bir anında iletme bildirimi toohello aygıt gönderilen böylece proje.</span><span class="sxs-lookup"><span data-stu-id="d7420-105">In this tutorial, you add push notifications toohello [iOS quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="d7420-106">Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, anında iletme bildirimi uzantısı paketi hello.</span><span class="sxs-lookup"><span data-stu-id="d7420-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="d7420-107">Bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="d7420-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

<span data-ttu-id="d7420-108">Merhaba [iOS simülatörü anında iletme bildirimlerini desteklemiyor](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="d7420-108">hello [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span> <span data-ttu-id="d7420-109">Fiziksel bir iOS cihazına gerekir ve bir [Apple Developer Program üyeliği](https://developer.apple.com/programs/ios/).</span><span class="sxs-lookup"><span data-stu-id="d7420-109">You need a physical iOS device and an [Apple Developer Program membership](https://developer.apple.com/programs/ios/).</span></span>

## <span data-ttu-id="d7420-110"><a name="configure-hub"></a>Bildirim hub'ı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d7420-110"><a name="configure-hub"></a>Configure Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="d7420-111"><a id="register"></a>Anında iletme bildirimleri için uygulamanızı kaydetmeniz</span><span class="sxs-lookup"><span data-stu-id="d7420-111"><a id="register"></a>Register app for push notifications</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="d7420-112">Azure toosend anında iletme bildirimleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d7420-112">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <span data-ttu-id="d7420-113"><a id="update-server"></a>Arka uç toosend anında iletme bildirimleri güncelleştir</span><span class="sxs-lookup"><span data-stu-id="d7420-113"><a id="update-server"></a>Update backend toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <span data-ttu-id="d7420-114"><a id="add-push"></a>Anında iletme bildirimleri tooapp Ekle</span><span class="sxs-lookup"><span data-stu-id="d7420-114"><a id="add-push"></a>Add push notifications tooapp</span></span>
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <span data-ttu-id="d7420-115"><a id="test"></a>Test anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="d7420-115"><a id="test"></a>Test push notifications</span></span>
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <span data-ttu-id="d7420-116"><a id="more"></a>Daha fazla</span><span class="sxs-lookup"><span data-stu-id="d7420-116"><a id="more"></a>More</span></span>
* <span data-ttu-id="d7420-117">Şablonları esneklik toosend platformlar arası gönderim ve yerelleştirilmiş iter verin.</span><span class="sxs-lookup"><span data-stu-id="d7420-117">Templates give you flexibility toosend cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="d7420-118">[Nasıl tooUse iOS için Azure Mobile Apps istemci Kitaplığı](app-service-mobile-ios-how-to-use-client-library.md#templates) nasıl gösterir tooregister şablonları.</span><span class="sxs-lookup"><span data-stu-id="d7420-118">[How tooUse iOS Client Library for Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) shows you how tooregister templates.</span></span>

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
[iOS Hızlı Başlat]: app-service-mobile-ios-get-started.md
