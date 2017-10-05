---
title: "Xamarin.Android uygulamanıza anında iletme bildirimleri ekleme | Microsoft Docs"
description: "Xamarin.Android uygulamanıza anında iletme bildirimleri göndermek için Azure App Service ve Azure bildirim hub'ları kullanmayı öğrenin"
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6f7e8517-e532-4559-9b07-874115f4c65b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: c3757d56fb1792092710740dc5ffbd64f18730cf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinandroid-app"></a><span data-ttu-id="54706-103">Xamarin.Android uygulamanıza anında iletme bildirimleri ekleme</span><span class="sxs-lookup"><span data-stu-id="54706-103">Add push notifications to your Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="54706-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="54706-104">Overview</span></span>
<span data-ttu-id="54706-105">Bu öğreticide, anında iletme bildirimleri ekleme [Xamarin.Android Hızlı Başlangıç](app-service-mobile-windows-store-dotnet-get-started.md) proje böylece bir kayda eklenen her zaman bir anında iletme bildirimi cihaza gönderilir.</span><span class="sxs-lookup"><span data-stu-id="54706-105">In this tutorial, you add push notifications to the [Xamarin.Android quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="54706-106">İndirilen hızlı başlangıç sunucu projesi kullanmazsanız, anında iletme bildirimi uzantısı paketi gerekir.</span><span class="sxs-lookup"><span data-stu-id="54706-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="54706-107">Bkz: [.NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="54706-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54706-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="54706-108">Prerequisites</span></span>
<span data-ttu-id="54706-109">Bu öğretici için aşağıdakiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="54706-109">This tutorial requires the following:</span></span>

* <span data-ttu-id="54706-110">Etkin bir Google hesabı.</span><span class="sxs-lookup"><span data-stu-id="54706-110">An active Google account.</span></span> <span data-ttu-id="54706-111">Bir Google hesabı için kaydolabilirsiniz [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="54706-111">You can sign up for a Google account at [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>
* <span data-ttu-id="54706-112">[Google Cloud Messaging istemci bileşeni](http://components.xamarin.com/view/GCMClient/).</span><span class="sxs-lookup"><span data-stu-id="54706-112">[Google Cloud Messaging Client Component](http://components.xamarin.com/view/GCMClient/).</span></span>

## <span data-ttu-id="54706-113"><a name="configure-hub"></a>Bildirim hub'ı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="54706-113"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="54706-114"><a id="register"></a>Firebase etkinleştirmek bulut Mesajlaşma</span><span class="sxs-lookup"><span data-stu-id="54706-114"><a id="register"></a>Enable Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-to-send-push-requests"></a><span data-ttu-id="54706-115">Gönderme istekleri göndermek için Azure yapılandırma</span><span class="sxs-lookup"><span data-stu-id="54706-115">Configure Azure to send push requests</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <span data-ttu-id="54706-116"><a id="update-server"></a>Güncelleştirme anında iletme bildirimleri göndermek için sunucu projesi</span><span class="sxs-lookup"><span data-stu-id="54706-116"><a id="update-server"></a>Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="54706-117"><a id="configure-app"></a>İstemci projesi anında iletme bildirimleri için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="54706-117"><a id="configure-app"></a>Configure the client project for push notifications</span></span>
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <span data-ttu-id="54706-118"><a id="add-push"></a>Uygulamanıza anında iletme bildirimleri kod ekleme</span><span class="sxs-lookup"><span data-stu-id="54706-118"><a id="add-push"></a>Add push notifications code to your app</span></span>
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <span data-ttu-id="54706-119"><a name="test"></a>Test, uygulamanızda anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="54706-119"><a name="test"></a>Test push notifications in your app</span></span>
<span data-ttu-id="54706-120">Öykünücüde sanal cihazı kullanarak uygulamayı test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54706-120">You can test the app by using a virtual device in the emulator.</span></span> <span data-ttu-id="54706-121">Bir öykünücü üzerinde çalışırken gerekli ek yapılandırma adımları vardır.</span><span class="sxs-lookup"><span data-stu-id="54706-121">There are additional configuration steps required when running on an emulator.</span></span>

1. <span data-ttu-id="54706-122">Dağıtma ve Google API'leri hedef olarak ayarlanmış Android sanal cihazı (AVD) Yöneticisi'nde aşağıda gösterildiği gibi sanal cihaza hata ayıklama emin olun.</span><span class="sxs-lookup"><span data-stu-id="54706-122">Make sure that you are deploying to or debugging on a virtual device that has Google APIs set as the target, as shown below in the Android Virtual Device (AVD) manager.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. <span data-ttu-id="54706-123">Tıklayarak Android aygıtına bir Google hesabı ekleyin **uygulamaları** > **ayarları** > **hesabı eklemek**, ardından yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="54706-123">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**, then follow the prompts.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. <span data-ttu-id="54706-124">Önce Yapılacaklar listesi uygulaması gibi çalıştırabilir ve yeni bir Yapılacaklar öğesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="54706-124">Run the todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="54706-125">Bu süre, bildirim alanında bir bildirim simgesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="54706-125">This time, a notification icon is displayed in the notification area.</span></span> <span data-ttu-id="54706-126">Tam metin bildirimi görüntülemek için bildirim çekmecesini açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54706-126">You can open the notification drawer to view the full text of the notification.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
