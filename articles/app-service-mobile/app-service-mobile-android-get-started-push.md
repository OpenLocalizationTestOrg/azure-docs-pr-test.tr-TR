---
title: "aaaAdd anında iletme bildirimleri tooyour Android uygulamanızı Mobile Apps | Microsoft Docs"
description: "Nasıl toouse Mobile Apps toosend anında bildirimler tooyour Android uygulaması hakkında bilgi edinin."
services: app-service\mobile
documentationcenter: android
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 9058ed6d-e871-4179-86af-0092d0ca09d3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: dcfb8463b395904b4bd0bf9bde2f71f259894066
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-android-app"></a><span data-ttu-id="041e9-103">Anında iletme bildirimleri tooyour Android uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="041e9-103">Add push notifications tooyour Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="041e9-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="041e9-104">Overview</span></span>
<span data-ttu-id="041e9-105">Bu öğreticide, eklediğiniz anında iletme bildirimleri toohello [Android Hızlı Başlangıç] bir kayda eklenen her zaman bir anında iletme bildirimi toohello aygıt gönderilen böylece proje.</span><span class="sxs-lookup"><span data-stu-id="041e9-105">In this tutorial, you add push notifications toohello [Android quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="041e9-106">Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, anında iletme bildirimi uzantısı paketi hello.</span><span class="sxs-lookup"><span data-stu-id="041e9-106">If you do not use hello downloaded quick start server project, you need hello push notification extension package.</span></span> <span data-ttu-id="041e9-107">Daha fazla bilgi için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="041e9-107">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="041e9-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="041e9-108">Prerequisites</span></span>
<span data-ttu-id="041e9-109">Merhaba aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="041e9-109">You need hello following:</span></span>

* <span data-ttu-id="041e9-110">Projenizin arka uç bağlı olarak bir IDE:</span><span class="sxs-lookup"><span data-stu-id="041e9-110">An IDE, depending on your project's back end:</span></span>

  * <span data-ttu-id="041e9-111">[Android Studio](https://developer.android.com/sdk/index.html) bu uygulamanın bir Node.js arka ucu varsa.</span><span class="sxs-lookup"><span data-stu-id="041e9-111">[Android Studio](https://developer.android.com/sdk/index.html) if this app has a Node.js back end.</span></span>
  * <span data-ttu-id="041e9-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) veya bu uygulamanın Microsoft .NET arka ucu varsa sonraki.</span><span class="sxs-lookup"><span data-stu-id="041e9-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) or later if this app has a Microsoft .NET back end.</span></span>
* <span data-ttu-id="041e9-113">Android 2.3 ve üzeri, Google depo düzeltme 27 veya daha yeni ve Google Play hizmetlerini 9.0.2 veya Firebase Cloud Messaging daha yeni.</span><span class="sxs-lookup"><span data-stu-id="041e9-113">Android 2.3 or later, Google Repository revision 27 or later, and Google Play Services 9.0.2 or later for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="041e9-114">Tam hello [Android Hızlı Başlangıç].</span><span class="sxs-lookup"><span data-stu-id="041e9-114">Complete hello [Android quick start].</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="041e9-115">Firebase Cloud Messaging'i destekleyen bir proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="041e9-115">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a><span data-ttu-id="041e9-116">Bildirim hub'ı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="041e9-116">Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="041e9-117">Azure toosend anında iletme bildirimleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="041e9-117">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-hello-server-project"></a><span data-ttu-id="041e9-118">Merhaba sunucu projesi için anında iletme bildirimlerini etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="041e9-118">Enable push notifications for hello server project</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-tooyour-app"></a><span data-ttu-id="041e9-119">Anında iletme bildirimleri tooyour uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="041e9-119">Add push notifications tooyour app</span></span>
<span data-ttu-id="041e9-120">Bu bölümde, istemci Android uygulaması toohandle anında iletme bildirimleri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="041e9-120">In this section, you update your client Android app toohandle push notifications.</span></span>

### <a name="verify-android-sdk-version"></a><span data-ttu-id="041e9-121">Android SDK sürümünü doğrula</span><span class="sxs-lookup"><span data-stu-id="041e9-121">Verify Android SDK version</span></span>
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

<span data-ttu-id="041e9-122">Sonraki adımınız tooinstall Google Play hizmetlerini olacaktır.</span><span class="sxs-lookup"><span data-stu-id="041e9-122">Your next step is tooinstall Google Play services.</span></span> <span data-ttu-id="041e9-123">Google Cloud Messaging sahip bazı en az API düzeyi gereksinimlerini geliştirme ve test etme, hangi hello **minSdkVersion** hello bildiriminde özellik için uygun olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="041e9-123">Google Cloud Messaging has some minimum API level requirements for development and testing, which hello **minSdkVersion** property in hello manifest must conform to.</span></span>

<span data-ttu-id="041e9-124">Eski bir aygıtla sınıyorsanız başvurun [ayarlayın yukarı Google Play Hizmetleri SDK] nasıl düşük toodetermine bu değeri ayarlayın ve uygun şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="041e9-124">If you are testing with an older device, consult [Set Up Google Play Services SDK] toodetermine how low you can set this value, and set it appropriately.</span></span>

### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="041e9-125">Google Play Hizmetleri toohello proje ekleyin</span><span class="sxs-lookup"><span data-stu-id="041e9-125">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a><span data-ttu-id="041e9-126">Kod ekleme</span><span class="sxs-lookup"><span data-stu-id="041e9-126">Add code</span></span>
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-hello-app-against-hello-published-mobile-service"></a><span data-ttu-id="041e9-127">Test hello uygulamayı hello karşı mobil hizmet yayımlandığına</span><span class="sxs-lookup"><span data-stu-id="041e9-127">Test hello app against hello published mobile service</span></span>
<span data-ttu-id="041e9-128">Merhaba uygulama doğrudan bir USB kablosu ile Android telefonla ekleme veya hello öykünücüsünde sanal cihazı kullanarak test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="041e9-128">You can test hello app by directly attaching an Android phone with a USB cable, or by using a virtual device in hello emulator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="041e9-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="041e9-129">Next steps</span></span>
<span data-ttu-id="041e9-130">Bu öğreticiyi tamamladığınıza göre öğreticileri aşağıdaki hello tooone üzerinde etmeden göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="041e9-130">Now that you completed this tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="041e9-131">[Kimlik doğrulama tooyour Android uygulaması eklemek](app-service-mobile-android-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="041e9-131">[Add authentication tooyour Android app](app-service-mobile-android-get-started-users.md).</span></span>
  <span data-ttu-id="041e9-132">Nasıl tooadd kimlik doğrulaması toohello todolist hızlı başlangıç projesi Android desteklenen kimlik sağlayıcısı kullanarak öğrenin.</span><span class="sxs-lookup"><span data-stu-id="041e9-132">Learn how tooadd authentication toohello todolist quickstart project on Android using a supported identity provider.</span></span>
* <span data-ttu-id="041e9-133">[Android uygulamanız için çevrimdışı eşitlemeyi etkinleştirme](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="041e9-133">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="041e9-134">Nasıl tooadd çevrimdışı destek tooyour uygulama Mobile Apps arka ucu kullanarak bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="041e9-134">Learn how tooadd offline support tooyour app by using a Mobile Apps back end.</span></span> <span data-ttu-id="041e9-135">Çevrimdışı Eşitleme ile kullanıcılar mobil uygulama ile etkileşim kurabilen&mdash;görüntüleme, ekleme veya değiştirme veri&mdash;hiçbir ağ bağlantısı olduğunda bile.</span><span class="sxs-lookup"><span data-stu-id="041e9-135">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs -->
[Android Hızlı Başlangıç]: app-service-mobile-android-get-started.md

[ayarlayın yukarı Google Play Hizmetleri SDK]:https://developers.google.com/android/guides/setup
