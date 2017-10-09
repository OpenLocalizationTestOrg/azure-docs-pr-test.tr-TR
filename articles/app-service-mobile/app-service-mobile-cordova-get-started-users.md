---
title: "Apache Cordova Mobile Apps ile kimlik doğrulamasını aaaAdd | Microsoft Docs"
description: "Bilgi nasıl toouse Mobile Apps tooauthenticate kullanıcıları kimlik sağlayıcıları, Google, Facebook, Twitter ve Microsoft dahil olmak üzere çeşitli Apache Cordova uygulamanızı Azure App Service içinde."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 10dd6dc9-ddf5-423d-8205-00ad74929f0d
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 61a05c5ac67fd0f0bc4c9d6920954a9b464a0a8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-apache-cordova-app"></a>Kimlik doğrulama tooyour Apache Cordova uygulaması ekleyin
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a>Özet
Bu öğreticide, Apache Cordova desteklenen kimlik sağlayıcısı kullanarak kimlik doğrulaması toohello todolist hızlı başlangıç projesi ekleyin. Bu öğretici hello üzerinde temel [Mobile Apps'i kullanmaya başlamak] önce tamamlamanız gereken öğretici.

## <a name="register"></a>Kimlik doğrulaması için uygulamanızı kaydetmenizi ve hello uygulama hizmetini yapılandırma
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[Benzer adımları gösteren bir video izleyin](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <a name="permissions"></a>İzinleri tooauthenticated kullanıcılarını kısıtlayın
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

Şimdi, bu anonim erişim tooyour arka uç devre dışı doğrulayabilirsiniz. Visual Studio'da:

* Başlangıç Öğreticisi tamamlandığında oluşturduğunuz açık hello proje [Mobile Apps'i kullanmaya başlamak].
* Hello uygulamanızı çalıştırın **Google Android öykünücüsü**.
* Merhaba uygulama başladıktan sonra beklenmeyen bir bağlantı hatası göründüğünü doğrulayın.

Ardından, hello uygulama tooauthenticate kullanıcılar kaynakları hello mobil uygulama arka ucundan istemeden önce güncelleştirin.

## <a name="add-authentication"></a>Kimlik doğrulama toohello uygulama Ekle
1. Projenizde açmak **Visual Studio**, ardından açık hello `www/index.html` dosyayı düzenlemek için.
2. Merhaba bulun `Content-Security-Policy` hello baş bölümünde meta etiketi.  Merhaba OAuth konak toohello izin verilen kaynaklar listesi ekleyin.

   | Sağlayıcı | SDK sağlayıcı adı | OAuth ana bilgisayar |
   |:--- |:--- |:--- |
   | Azure Active Directory | aad | https://login.microsoftonline.com |
   | Facebook | Facebook | https://www.facebook.com |
   | Google | Google | https://Accounts.Google.com |
   | Microsoft | MicrosoftAccount | https://Login.live.com |
   | Twitter | Twitter | https://api.twitter.com |

    İçerik güvenlik (Azure Active Directory için uygulanan) ilkeye örneği aşağıdaki gibidir:

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    Değiştir `https://login.microsoftonline.com` tablo önceki hello hello OAuth host ile.  Merhaba hello içerik güvenlik ilkesi meta etiketi hakkında daha fazla bilgi için bkz: [içerik Güvenlik İlkesi belgeleri].

    Bazı kimlik doğrulama sağlayıcıları uygun mobil cihazlarda kullanıldığında içerik güvenlik ilkesi değişikliklerini gerektirmez.  Örneğin, bir Android cihazında Google kimlik doğrulaması kullanırken, içerik güvenlik ilkesi değişiklik gerekmez.

3. Açık hello `www/js/index.js` dosya düzenlemek için hello bulun `onDeviceReady()` yöntemini ve hello istemci oluşturmanın altında koddan hello kodu ekleyin:

        // Login toohello service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    Bu kod hello tablo başvurusu oluşturan ve hello UI yeniler hello var olan kodu değiştirir.

    Merhaba tanımlar: login() yöntemi hello sağlayıcı ile kimlik doğrulamasını başlatır. JavaScript Promise döndüren bir zaman uyumsuz işlev Hello tanımlar: login() yöntemidir.  Böylece Hello tanımlar: login() yöntemi tamamlanana kadar bu yürütülemiyor hello rest hello başlatma hello promise yanıt içinde yerleştirilir.

4. Yeni eklediğiniz hello kodda Değiştir `SDK_Provider_Name` hello adıyla oturum açma sağlayıcısı. Örneğin, Azure Active Directory kullanmak `client.login('aad')`.
5. Projenizi çalıştırma.  Merhaba proje başlatma tamamlandığında, uygulamanızı hello OAuth oturum açma sayfasına kimlik doğrulama sağlayıcısı seçilen hello için gösterir.

## <a name="next-steps"></a>Sonraki Adımlar
* Daha fazla bilgi edinin [kimlik doğrulama hakkında] Azure uygulama hizmeti ile.
* Başlangıç Öğreticisi ekleyerek devam [anında iletme bildirimleri] tooyour Apache Cordova uygulaması.

Nasıl toouse hello SDK'ları hakkında bilgi edinin.

* [Apache Cordova SDK]
* [ASP.NET Sunucusu SDK]
* [Node.js Sunucusu SDK]

<!-- URLs. -->
[Mobile Apps'i kullanmaya başlamak]: app-service-mobile-cordova-get-started.md
[içerik Güvenlik İlkesi belgeleri]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html
[anında iletme bildirimleri]: app-service-mobile-cordova-get-started-push.md
[kimlik doğrulama hakkında]: app-service-mobile-auth.md
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Sunucusu SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Sunucusu SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
