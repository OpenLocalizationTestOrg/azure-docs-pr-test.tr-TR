---
title: "aaaAdd anında iletme bildirimleri tooyour Xamarin.Android uygulaması | Microsoft Docs"
description: "Nasıl toouse Azure App Service ve Azure Notification Hubs toosend bildirimleri tooyour Xamarin.Android uygulaması anında bilgi edinin"
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
ms.openlocfilehash: c93d1d0cae06ab15e3e3e5c4b342808b2cd49113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinandroid-app"></a><span data-ttu-id="a1853-103">Anında iletme bildirimleri tooyour Xamarin.Android uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="a1853-103">Add push notifications tooyour Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="a1853-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="a1853-104">Overview</span></span>
<span data-ttu-id="a1853-105">Bu öğreticide, eklediğiniz anında iletme bildirimleri toohello [Xamarin.Android Hızlı Başlangıç](app-service-mobile-windows-store-dotnet-get-started.md) bir kayda eklenen her zaman bir anında iletme bildirimi toohello aygıt gönderilen böylece proje.</span><span class="sxs-lookup"><span data-stu-id="a1853-105">In this tutorial, you add push notifications toohello [Xamarin.Android quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="a1853-106">Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, anında iletme bildirimi uzantısı paketi hello.</span><span class="sxs-lookup"><span data-stu-id="a1853-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="a1853-107">Bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="a1853-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1853-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a1853-108">Prerequisites</span></span>
<span data-ttu-id="a1853-109">Bu öğretici hello aşağıdakileri gerektirir:</span><span class="sxs-lookup"><span data-stu-id="a1853-109">This tutorial requires hello following:</span></span>

* <span data-ttu-id="a1853-110">Etkin bir Google hesabı.</span><span class="sxs-lookup"><span data-stu-id="a1853-110">An active Google account.</span></span> <span data-ttu-id="a1853-111">Bir Google hesabı için kaydolabilirsiniz [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="a1853-111">You can sign up for a Google account at [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>
* <span data-ttu-id="a1853-112">[Google Cloud Messaging istemci bileşeni](http://components.xamarin.com/view/GCMClient/).</span><span class="sxs-lookup"><span data-stu-id="a1853-112">[Google Cloud Messaging Client Component](http://components.xamarin.com/view/GCMClient/).</span></span>

## <span data-ttu-id="a1853-113"><a name="configure-hub"></a>Bildirim hub'ı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a1853-113"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="a1853-114"><a id="register"></a>Firebase etkinleştirmek bulut Mesajlaşma</span><span class="sxs-lookup"><span data-stu-id="a1853-114"><a id="register"></a>Enable Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-toosend-push-requests"></a><span data-ttu-id="a1853-115">Azure toosend gönderme istekleri yapılandırın</span><span class="sxs-lookup"><span data-stu-id="a1853-115">Configure Azure toosend push requests</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <span data-ttu-id="a1853-116"><a id="update-server"></a>Güncelleştirme Hello sunucu projesi toosend anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="a1853-116"><a id="update-server"></a>Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="a1853-117"><a id="configure-app"></a>Merhaba istemci projesi anında iletme bildirimleri için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a1853-117"><a id="configure-app"></a>Configure hello client project for push notifications</span></span>
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <span data-ttu-id="a1853-118"><a id="add-push"></a>Anında iletme bildirimleri kodu tooyour uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="a1853-118"><a id="add-push"></a>Add push notifications code tooyour app</span></span>
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <span data-ttu-id="a1853-119"><a name="test"></a>Test, uygulamanızda anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="a1853-119"><a name="test"></a>Test push notifications in your app</span></span>
<span data-ttu-id="a1853-120">Merhaba öykünücüsünde sanal cihazı kullanarak hello uygulama test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1853-120">You can test hello app by using a virtual device in hello emulator.</span></span> <span data-ttu-id="a1853-121">Bir öykünücü üzerinde çalışırken gerekli ek yapılandırma adımları vardır.</span><span class="sxs-lookup"><span data-stu-id="a1853-121">There are additional configuration steps required when running on an emulator.</span></span>

1. <span data-ttu-id="a1853-122">Aşağıda hello Android sanal cihazı (AVD) Yöneticisi'nde gösterildiği gibi Google API'leri hello hedef olarak ayarlanmış olan bir sanal cihazdaki tooor hata ayıklama dağıtıyorsanız emin olun.</span><span class="sxs-lookup"><span data-stu-id="a1853-122">Make sure that you are deploying tooor debugging on a virtual device that has Google APIs set as hello target, as shown below in hello Android Virtual Device (AVD) manager.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. <span data-ttu-id="a1853-123">Bir Google hesabı toohello Android cihazı tıklayarak ekleyin **uygulamaları** > **ayarları** > **hesabı eklemek**, hello istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="a1853-123">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**, then follow hello prompts.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. <span data-ttu-id="a1853-124">Önce Hello Yapılacaklar listesi uygulaması gibi çalıştırabilir ve yeni bir Yapılacaklar öğesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a1853-124">Run hello todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="a1853-125">Bu süre, hello bildirim alanında bir bildirim simgesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a1853-125">This time, a notification icon is displayed in hello notification area.</span></span> <span data-ttu-id="a1853-126">Merhaba bildirim çekmecesini tooview hello tam metin hello bildirim açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1853-126">You can open hello notification drawer tooview hello full text of hello notification.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
