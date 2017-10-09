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
# <a name="add-push-notifications-tooyour-android-app"></a>Anında iletme bildirimleri tooyour Android uygulaması ekleyin
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Genel Bakış
Bu öğreticide, eklediğiniz anında iletme bildirimleri toohello [Android Hızlı Başlangıç] bir kayda eklenen her zaman bir anında iletme bildirimi toohello aygıt gönderilen böylece proje.

Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, anında iletme bildirimi uzantısı paketi hello. Daha fazla bilgi için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="prerequisites"></a>Ön koşullar
Merhaba aşağıdaki gerekir:

* Projenizin arka uç bağlı olarak bir IDE:

  * [Android Studio](https://developer.android.com/sdk/index.html) bu uygulamanın bir Node.js arka ucu varsa.
  * [Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) veya bu uygulamanın Microsoft .NET arka ucu varsa sonraki.
* Android 2.3 ve üzeri, Google depo düzeltme 27 veya daha yeni ve Google Play hizmetlerini 9.0.2 veya Firebase Cloud Messaging daha yeni.
* Tam hello [Android Hızlı Başlangıç].

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a>Firebase Cloud Messaging'i destekleyen bir proje oluşturma
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a>Bildirim hub'ı yapılandırma
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-toosend-push-notifications"></a>Azure toosend anında iletme bildirimleri yapılandırma
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-hello-server-project"></a>Merhaba sunucu projesi için anında iletme bildirimlerini etkinleştirin
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-tooyour-app"></a>Anında iletme bildirimleri tooyour uygulama Ekle
Bu bölümde, istemci Android uygulaması toohandle anında iletme bildirimleri güncelleştirin.

### <a name="verify-android-sdk-version"></a>Android SDK sürümünü doğrula
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

Sonraki adımınız tooinstall Google Play hizmetlerini olacaktır. Google Cloud Messaging sahip bazı en az API düzeyi gereksinimlerini geliştirme ve test etme, hangi hello **minSdkVersion** hello bildiriminde özellik için uygun olmalıdır.

Eski bir aygıtla sınıyorsanız başvurun [ayarlayın yukarı Google Play Hizmetleri SDK] nasıl düşük toodetermine bu değeri ayarlayın ve uygun şekilde ayarlayın.

### <a name="add-google-play-services-toohello-project"></a>Google Play Hizmetleri toohello proje ekleyin
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a>Kod ekleme
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-hello-app-against-hello-published-mobile-service"></a>Test hello uygulamayı hello karşı mobil hizmet yayımlandığına
Merhaba uygulama doğrudan bir USB kablosu ile Android telefonla ekleme veya hello öykünücüsünde sanal cihazı kullanarak test edebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticiyi tamamladığınıza göre öğreticileri aşağıdaki hello tooone üzerinde etmeden göz önünde bulundurun:

* [Kimlik doğrulama tooyour Android uygulaması eklemek](app-service-mobile-android-get-started-users.md).
  Nasıl tooadd kimlik doğrulaması toohello todolist hızlı başlangıç projesi Android desteklenen kimlik sağlayıcısı kullanarak öğrenin.
* [Android uygulamanız için çevrimdışı eşitlemeyi etkinleştirme](app-service-mobile-android-get-started-offline-data.md).
  Nasıl tooadd çevrimdışı destek tooyour uygulama Mobile Apps arka ucu kullanarak bilgi edinin. Çevrimdışı Eşitleme ile kullanıcılar mobil uygulama ile etkileşim kurabilen&mdash;görüntüleme, ekleme veya değiştirme veri&mdash;hiçbir ağ bağlantısı olduğunda bile.

<!-- URLs -->
[Android Hızlı Başlangıç]: app-service-mobile-android-get-started.md

[ayarlayın yukarı Google Play Hizmetleri SDK]:https://developers.google.com/android/guides/setup
