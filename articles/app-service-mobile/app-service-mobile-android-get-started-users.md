---
title: "Android Mobile Apps ile kimlik doğrulamasını aaaAdd | Microsoft Docs"
description: "Nasıl toouse hello tooauthenticate kullanıcılarının Android uygulamanızın kimlik sağlayıcıları, Google, Facebook, Twitter ve Microsoft dahil olmak üzere çeşitli Azure App Service Mobile Apps özelliğini öğrenin."
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 1fc8e7c1-6c3c-40f4-9967-9cf5e21fc4e1
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 01f608f996c931c643790ed2778df11cf590c903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-android-app"></a>Kimlik doğrulama tooyour Android uygulaması ekleyin
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a>Özet
Bu öğreticide, desteklenen kimlik sağlayıcısı kullanarak Android kimlik doğrulama toohello todolist hızlı başlangıç projesi ekleyin. Bu öğretici hello üzerinde temel [Mobile Apps'i kullanmaya başlamak] önce tamamlamanız gereken öğretici.

## <a name="register"></a>Kimlik doğrulaması için uygulamanızı kaydetmenizi ve Azure uygulama hizmeti yapılandırın
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Uygulama toohello izin verilen dış yönlendirme URL'lerini ekleme

Uygulamanız için yeni bir URL şemasını tanımlamak güvenli kimlik doğrulaması gerektirir. Merhaba kimlik doğrulama işlemi tamamlandıktan sonra bu hello authentication sistem tooredirect geri tooyour uygulamasını sağlar. Bu öğreticide, kullandığımız hello URL şeması _appname_ boyunca. Ancak, seçtiğiniz herhangi bir URL şeması kullanabilirsiniz. Benzersiz tooyour mobil uygulama olmalıdır. Merhaba sunucu tarafı tooenable hello yönlendirme:

1. Hello [Azure portalı]'da, uygulama hizmeti seçin.

2. Merhaba tıklatın **kimlik doğrulama / yetkilendirme** menü seçeneği.

3. Merhaba, **yeniden yönlendirme URL'lere izin**, girin `appname://easyauth.callback`.  Merhaba _appname_ bu içinde hello URL şeması mobil uygulamanız için bir dizedir.  Bir protokol (harf kullanın ve yalnızca sayı ve bir harf ile başlar) için normal URL belirtimi izlemelisiniz.  Merhaba çeşitli yerlerde URL şeması ile mobil uygulama kodunuzu tooadjust gerekeceğinden, seçtiğiniz hello dize Not olmanız gerekir.

4. **Tamam** düğmesine tıklayın.

5. **Kaydet** düğmesine tıklayın.

## <a name="permissions"></a>İzinleri tooauthenticated kullanıcılarını kısıtlayın
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* Android Studio'da hello eğitici, tamamlandı hello proje açmak [Mobile Apps'i kullanmaya başlamak]. Hello gelen **çalıştırmak** menüsünde tıklatın **uygulama çalıştırma**ve hello uygulama başladıktan sonra durum koduyla işlenmeyen bir özel durum 401 (yetkisiz) tetiklenir doğrulayın.

     Merhaba uygulama denemeleri tooaccess hello geri bitiş kimliği doğrulanmamış bir kullanıcı olarak, ancak hello için bu özel durum *Todoıtem* tablo artık kimlik doğrulaması gerektirir.

Ardından, hello uygulama tooauthenticate kullanıcılar kaynakları Mobile Apps bitiş hello istemeden önce güncelleştirin. 

## <a name="add-authentication-toohello-app"></a>Kimlik doğrulama toohello uygulama Ekle
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <a name="cache-tokens"></a>Kimlik doğrulama belirteçleri hello istemcide önbelleğe alma
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a>Sonraki adımlar
Bu temel kimlik doğrulaması öğreticisini tamamladığınıza göre öğreticileri aşağıdaki hello tooone üzerinde etmeden göz önünde bulundurun:

* [Anında iletme bildirimleri tooyour Android uygulaması eklemek](app-service-mobile-android-get-started-push.md).
  Mobile Apps geri tooconfigure toouse Azure bildirim hub'ları toosend anında iletme bildirimleri nasıl sona erdirmek öğrenin.
* [Android uygulamanız için çevrimdışı eşitlemeyi etkinleştirme](app-service-mobile-android-get-started-offline-data.md).
  Nasıl tooadd çevrimdışı destek tooyour uygulama Mobile Apps arka ucu kullanarak bilgi edinin. Çevrimdışı Eşitleme ile kullanıcılar mobil uygulama ile etkileşim kurabilen&mdash;görüntüleme, ekleme veya değiştirme veri&mdash;hiçbir ağ bağlantısı olduğunda bile.

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions tooauthenticated users]: #permissions
[Add authentication toohello app]: #add-authentication
[Store authentication tokens on hello client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
[Mobile Apps'i kullanmaya başlamak]: app-service-mobile-android-get-started.md
