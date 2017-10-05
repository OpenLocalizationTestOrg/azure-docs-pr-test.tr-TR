---
title: "İOS uygulaması ile Azure Mobile Apps için anında iletme bildirimleri ekleme"
description: "İOS uygulamanıza anında iletme bildirimleri göndermek için Azure Mobile Apps kullanmayı öğrenin."
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
ms.openlocfilehash: 08a8c35b89386bd0dbe7bba406a6985a5a0d7eb8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-ios-app"></a><span data-ttu-id="b3fac-103">İOS uygulamasına anında iletme bildirimleri ekleme</span><span class="sxs-lookup"><span data-stu-id="b3fac-103">Add Push Notifications to your iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="b3fac-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b3fac-104">Overview</span></span>
<span data-ttu-id="b3fac-105">Bu öğreticide, anında iletme bildirimleri ekleme [iOS Hızlı Başlat] proje böylece bir kayda eklenen her zaman bir anında iletme bildirimi cihaza gönderilir.</span><span class="sxs-lookup"><span data-stu-id="b3fac-105">In this tutorial, you add push notifications to the [iOS quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="b3fac-106">İndirilen hızlı başlangıç sunucu projesi kullanmazsanız, anında iletme bildirimi uzantısı paketi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3fac-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="b3fac-107">Bkz: [.NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="b3fac-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

<span data-ttu-id="b3fac-108">[İOS simülatörü anında iletme bildirimlerini desteklemiyor](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="b3fac-108">The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span> <span data-ttu-id="b3fac-109">Fiziksel bir iOS cihazına gerekir ve bir [Apple Developer Program üyeliği](https://developer.apple.com/programs/ios/).</span><span class="sxs-lookup"><span data-stu-id="b3fac-109">You need a physical iOS device and an [Apple Developer Program membership](https://developer.apple.com/programs/ios/).</span></span>

## <span data-ttu-id="b3fac-110"><a name="configure-hub"></a>Bildirim hub'ı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b3fac-110"><a name="configure-hub"></a>Configure Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="b3fac-111"><a id="register"></a>Anında iletme bildirimleri için uygulamanızı kaydetmeniz</span><span class="sxs-lookup"><span data-stu-id="b3fac-111"><a id="register"></a>Register app for push notifications</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="b3fac-112">Anında iletme bildirimleri göndermek için Azure yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b3fac-112">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <span data-ttu-id="b3fac-113"><a id="update-server"></a>Anında iletme bildirimleri göndermek için arka uç güncelleştir</span><span class="sxs-lookup"><span data-stu-id="b3fac-113"><a id="update-server"></a>Update backend to send push notifications</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <span data-ttu-id="b3fac-114"><a id="add-push"></a>Uygulamasına anında iletme bildirimleri ekleme</span><span class="sxs-lookup"><span data-stu-id="b3fac-114"><a id="add-push"></a>Add push notifications to app</span></span>
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <span data-ttu-id="b3fac-115"><a id="test"></a>Test anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="b3fac-115"><a id="test"></a>Test push notifications</span></span>
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <span data-ttu-id="b3fac-116"><a id="more"></a>Daha fazla</span><span class="sxs-lookup"><span data-stu-id="b3fac-116"><a id="more"></a>More</span></span>
* <span data-ttu-id="b3fac-117">Şablonları platformlar arası gönderim ve yerelleştirilmiş bildirim göndermek için esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="b3fac-117">Templates give you flexibility to send cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="b3fac-118">[Kullanım iOS için Azure Mobile Apps istemci kitaplığı nasıl](app-service-mobile-ios-how-to-use-client-library.md#templates) şablonlarını kaydetmek gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b3fac-118">[How to Use iOS Client Library for Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) shows you how to register templates.</span></span>

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
<span data-ttu-id="b3fac-119">[iOS Hızlı Başlat]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="b3fac-119">[iOS quick start]: app-service-mobile-ios-get-started.md</span></span>
