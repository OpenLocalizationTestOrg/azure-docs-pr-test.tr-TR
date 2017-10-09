---
title: "Xamarin iOS mobil uygulamalar için kimlik doğrulaması ile aaaGet başlatıldı"
description: "Bilgi nasıl toouse Mobile Apps tooauthenticate Xamarin iOS uygulamanızı kimlik sağlayıcıları, AAD, Google, Facebook, Twitter ve Microsoft dahil olmak üzere çeşitli kullanıcılarının."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 180cc61b-19c5-48bf-a16c-7181aef3eacc
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: glenga
ms.openlocfilehash: 6458e9651b03df61c86b88b11953792e04bfa5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinios-app"></a>Kimlik doğrulama tooyour Xamarin.iOS uygulaması ekleyin
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

Bu konu, nasıl gösterir bir mobil uygulama hizmeti, istemci uygulamasından tooauthenticate kullanıcıları. Bu öğreticide, App Service tarafından desteklenen bir kimlik sağlayıcısı kullanarak kimlik doğrulaması toohello Xamarin.iOS hızlı başlangıç projesi ekleyin. Mobil uygulamanız tarafından yetkili başarılı bir şekilde kimliği doğrulanmış ve sonra hello kullanıcı kimliği değeri görüntülenir ve kısıtlı mümkün tooaccess tablo verisi olacaktır.

Merhaba öğretici ilk tamamlamalısınız [bir Xamarin.iOS uygulaması oluşturma]. Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, hello kimlik doğrulaması uzantı paketini tooyour projesi eklemeniz gerekir. Server uzantısı paketleri hakkında daha fazla bilgi için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="register-your-app-for-authentication-and-configure-app-services"></a>Kimlik doğrulaması için uygulamanızı kaydetme ve uygulama hizmetlerini yapılandırma
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-toohello-allowed-external-redirect-urls"></a>Uygulama toohello izin verilen dış yönlendirme URL'lerini ekleme

Uygulamanız için yeni bir URL şemasını tanımlamak güvenli kimlik doğrulaması gerektirir. Merhaba kimlik doğrulama işlemi tamamlandıktan sonra bu hello authentication sistem tooredirect geri tooyour uygulamasını sağlar. Bu öğreticide, kullandığımız hello URL şeması _appname_ boyunca. Ancak, seçtiğiniz herhangi bir URL şeması kullanabilirsiniz. Benzersiz tooyour mobil uygulama olmalıdır. Merhaba sunucu tarafı tooenable hello yönlendirme:

1. Hello [Azure portalı]'da, uygulama hizmeti seçin.

2. Merhaba tıklatın **kimlik doğrulama / yetkilendirme** menü seçeneği.

3. Merhaba, **yeniden yönlendirme URL'lere izin**, girin `url_scheme_of_your_app://easyauth.callback`.  Merhaba **url_scheme_of_your_app** bu içinde hello URL şeması mobil uygulamanız için bir dizedir.  Bir protokol (harf kullanın ve yalnızca sayı ve bir harf ile başlar) için normal URL belirtimi izlemelisiniz.  Merhaba çeşitli yerlerde URL şeması ile mobil uygulama kodunuzu tooadjust gerekeceğinden, seçtiğiniz hello dize Not olmanız gerekir.

4. **Tamam** düğmesine tıklayın.

5. **Kaydet** düğmesine tıklayın.

## <a name="restrict-permissions-tooauthenticated-users"></a>İzinleri tooauthenticated kullanıcılarını kısıtlayın
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

&nbsp;&nbsp;4. Visual Studio veya Xamarin Studio'da hello istemci projesi bir cihaz veya öykünücü çalıştırın. Merhaba uygulama başladıktan sonra durum koduyla işlenmeyen bir özel durum 401 (yetkisiz) tetiklenir doğrulayın. Merhaba, günlüğe kaydedilen toohello konsol hello hata ayıklayıcısının hatasıdır. Bu nedenle Visual Studio'da hello çıktı penceresinde hello hatası görmeniz gerekir.

&nbsp;&nbsp;Merhaba uygulama kimliği doğrulanmamış bir kullanıcı olarak, mobil uygulamanızın arka ucuna tooaccess çalıştığı yetkisiz bu hata gerçekleşir. Merhaba *Todoıtem* tablo artık kimlik doğrulaması gerektirir.

Ardından, kimliği doğrulanmış bir kullanıcı ile Merhaba istemci uygulaması toorequest hello mobil uygulama arka ucu kaynaklardan güncelleştirir.

## <a name="add-authentication-toohello-app"></a>Kimlik doğrulama toohello uygulama Ekle
Bu bölümde, veri görüntülemeden önce hello uygulama toodisplay bir oturum açma ekranı değiştirecektir. Merhaba uygulama başlatıldığında değil tooyour uygulama hizmeti bağlanmaz ve herhangi bir veri görüntülenmez. İlk kez Hello sonra hello oturum açma ekranı görünür hello kullanıcı hello yenileme hareketi gerçekleştirir; başarılı oturum açma işleminden sonra hello Yapılacaklar öğelerini listesi görüntülenir.

1. Merhaba istemci projesinde hello dosyasını açın **QSTodoService.cs** ve hello aşağıdakileri ekleyin deyimiyle ve `MobileServiceUser` erişimci toohello QSTodoService sınıfı ile:
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. Adlı yeni bir yöntem ekleyin **kimlik doğrulama** çok**QSTodoService** tanımı aşağıdaki hello ile:

        public async Task Authenticate(UIViewController view)
        {
            try
            {
                AppDelegate.ResumeWithURL = url => url.Scheme == "zumoe2etestapp" && client.ResumeWithURL(url);
                user = await client.LoginAsync(view, MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine (@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
            }
        }

    >[AZURE.NOTE] Bir Facebook dışında bir kimlik sağlayıcısı kullanıyorsanız, çok geçirilen hello değeri değiştirmek**LoginAsync** tooone hello aşağıdaki yukarıda: _MicrosoftAccount_, _Twitter_, _Google_, veya _WindowsAzureActiveDirectory_.

3. Açık **QSTodoListViewController.cs**. Merhaba yöntemi tanımını değiştirme **ViewDidLoad** hello çağrısı çok kaldırma**RefreshAsync()** hello sona:
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out hello call tooRefreshAsync
            // await RefreshAsync();
        }
4. Merhaba yöntemi Değiştir **RefreshAsync** tooauthenticate hello varsa **kullanıcı** özelliği null. Merhaba yöntemi tanımı hello üstündeki koddan hello ekleyin:
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. Açık **AppDelegate.cs**, yöntem aşağıdaki hello ekleyin:

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. Açık **Info.plist** dosya, çok gidin**URL türleri** hello içinde **Gelişmiş** bölümü. Şimdi hello yapılandırmak **tanımlayıcısı** ve hello **URL şemalarını** URL türü ve tıklatın **URL türü Ekle**. **URL şemalarını** {url_scheme_of_your_app} hello aynı olmalıdır.
7. Visual Studio veya Xamarin Studio'da tooyour Xamarin yapı konağı bir cihaz veya öykünücü hedefleme hello istemci projesi çalıştırma Mac, bağlı. Hiçbir veri bu hello uygulama görüntüler doğrulayın.
   
    Merhaba yenileme hareketi hello oturum açma ekranı tooappear neden olacak öğeleri hello listede aşağı çekerek gerçekleştirin. Geçerli kimlik bilgileri başarıyla girdikten sonra hello uygulama Yapılacaklar öğelerini hello listesini görüntüler ve güncelleştirmeler toohello veri yapabilirsiniz.

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[bir Xamarin.iOS uygulaması oluşturma]: app-service-mobile-xamarin-ios-get-started.md