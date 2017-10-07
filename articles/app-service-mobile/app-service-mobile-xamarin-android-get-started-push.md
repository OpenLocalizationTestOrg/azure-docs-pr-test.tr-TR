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
# <a name="add-push-notifications-tooyour-xamarinandroid-app"></a>Anında iletme bildirimleri tooyour Xamarin.Android uygulaması ekleyin
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Genel Bakış
Bu öğreticide, eklediğiniz anında iletme bildirimleri toohello [Xamarin.Android Hızlı Başlangıç](app-service-mobile-windows-store-dotnet-get-started.md) bir kayda eklenen her zaman bir anında iletme bildirimi toohello aygıt gönderilen böylece proje.

Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, anında iletme bildirimi uzantısı paketi hello. Bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) daha fazla bilgi için.

## <a name="prerequisites"></a>Ön koşullar
Bu öğretici hello aşağıdakileri gerektirir:

* Etkin bir Google hesabı. Bir Google hesabı için kaydolabilirsiniz [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).
* [Google Cloud Messaging istemci bileşeni](http://components.xamarin.com/view/GCMClient/).

## <a name="configure-hub"></a>Bildirim hub'ı yapılandırma
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a id="register"></a>Firebase etkinleştirmek bulut Mesajlaşma
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-toosend-push-requests"></a>Azure toosend gönderme istekleri yapılandırın
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a id="update-server"></a>Güncelleştirme Hello sunucu projesi toosend anında iletme bildirimleri
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a id="configure-app"></a>Merhaba istemci projesi anında iletme bildirimleri için yapılandırma
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <a id="add-push"></a>Anında iletme bildirimleri kodu tooyour uygulama Ekle
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <a name="test"></a>Test, uygulamanızda anında iletme bildirimleri
Merhaba öykünücüsünde sanal cihazı kullanarak hello uygulama test edebilirsiniz. Bir öykünücü üzerinde çalışırken gerekli ek yapılandırma adımları vardır.

1. Aşağıda hello Android sanal cihazı (AVD) Yöneticisi'nde gösterildiği gibi Google API'leri hello hedef olarak ayarlanmış olan bir sanal cihazdaki tooor hata ayıklama dağıtıyorsanız emin olun.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. Bir Google hesabı toohello Android cihazı tıklayarak ekleyin **uygulamaları** > **ayarları** > **hesabı eklemek**, hello istemleri izleyin.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. Önce Hello Yapılacaklar listesi uygulaması gibi çalıştırabilir ve yeni bir Yapılacaklar öğesi ekleyin. Bu süre, hello bildirim alanında bir bildirim simgesi görüntülenir. Merhaba bildirim çekmecesini tooview hello tam metin hello bildirim açabilirsiniz.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
