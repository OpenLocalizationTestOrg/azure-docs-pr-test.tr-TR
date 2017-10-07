---
title: "Xamarin Android mobil uygulamalar için kimlik doğrulaması ile aaaGet başlatıldı"
description: "Bilgi nasıl toouse Mobile Apps tooauthenticate kullanıcıların kimlik sağlayıcıları, AAD, Google, Facebook, Twitter ve Microsoft dahil olmak üzere çeşitli Xamarin Android uygulamanızın."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 570fc12b-46a9-4722-b2e0-0d1c45fb2152
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: 500a4efa816e4f6d75d359e31d6357da56a72f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinandroid-app"></a>Kimlik doğrulama tooyour Xamarin.Android uygulaması ekleyin
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

Bu konu, nasıl gösterir istemci uygulamanız mobil uygulamasından tooauthenticate kullanıcıları. Bu öğreticide, Azure Mobile Apps tarafından desteklenen bir kimlik sağlayıcısı kullanarak kimlik doğrulaması toohello hızlı başlangıç projesi ekleyin. Başarılı bir şekilde kimliği doğrulanmış ve hello mobil uygulama yetkili sonra hello kullanıcı kimliği değeri görüntülenir.

Bu öğretici hello mobil uygulama quickstart üzerinde temel alır. Ayrıca ilk hello öğreticiyi tamamlamanız gerekir [Xamarin.Android uygulaması oluşturma]. Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, hello kimlik doğrulaması uzantı paketini tooyour projesi eklemeniz gerekir. Server uzantısı paketleri hakkında daha fazla bilgi için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="register"></a>Kimlik doğrulaması için uygulamanızı kaydetme ve uygulama hizmetlerini yapılandırma
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Uygulama toohello izin verilen dış yönlendirme URL'lerini ekleme

Uygulamanız için yeni bir URL şemasını tanımlamak güvenli kimlik doğrulaması gerektirir. Merhaba kimlik doğrulama işlemi tamamlandıktan sonra bu hello authentication sistem tooredirect geri tooyour uygulamasını sağlar. Bu öğreticide, kullandığımız hello URL şeması _appname_ boyunca. Ancak, seçtiğiniz herhangi bir URL şeması kullanabilirsiniz. Benzersiz tooyour mobil uygulama olmalıdır. Merhaba sunucu tarafı tooenable hello yönlendirme:

1. Hello [Azure portalı]'da, uygulama hizmeti seçin.

2. Merhaba tıklatın **kimlik doğrulama / yetkilendirme** menü seçeneği.

3. Merhaba, **yeniden yönlendirme URL'lere izin**, girin `url_scheme_of_your_app://easyauth.callback`.  Merhaba **url_scheme_of_your_app** bu içinde hello URL şeması mobil uygulamanız için bir dizedir.  Bir protokol (harf kullanın ve yalnızca sayı ve bir harf ile başlar) için normal URL belirtimi izlemelisiniz.  Merhaba çeşitli yerlerde URL şeması ile mobil uygulama kodunuzu tooadjust gerekeceğinden, seçtiğiniz hello dize Not olmanız gerekir.

4. **Tamam** düğmesine tıklayın.

5. **Kaydet** düğmesine tıklayın.

## <a name="permissions"></a>İzinleri tooauthenticated kullanıcılarını kısıtlayın
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

Visual Studio veya Xamarin Studio'da hello istemci projesi bir cihaz veya öykünücü çalıştırın. Merhaba uygulama başladıktan sonra durum koduyla işlenmeyen bir özel durum 401 (yetkisiz) tetiklenir doğrulayın. Merhaba uygulama kimliği doğrulanmamış bir kullanıcı olarak, mobil uygulamanızın arka ucuna tooaccess çalıştığı meydana gelir. Merhaba *Todoıtem* tablo artık kimlik doğrulaması gerektirir.

Ardından, kimliği doğrulanmış bir kullanıcı ile Merhaba istemci uygulaması toorequest hello mobil uygulama arka ucu kaynaklardan güncelleştirir.

## <a name="add-authentication"></a>Kimlik doğrulama toohello uygulama Ekle
Merhaba uygulamadır güncelleştirilmiş toorequire kullanıcılar tootap hello **oturum** düğmesine tıklayın ve veri görüntülenmeden önce kimlik doğrulaması.

1. Aşağıdaki kodu toohello hello eklemek **TodoActivity** sınıfı:
   
        // Define a authenticated user.
        private MobileServiceUser user;
        private async Task<bool> Authenticate()
        {
                var success = false;
                try
                {
                    // Sign in with Facebook login using a server-managed flow.
                    user = await client.LoginAsync(this,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    CreateAndShowDialog(string.Format("you are now logged in - {0}",
                        user.UserId), "Logged in!");
   
                    success = true;
                }
                catch (Exception ex)
                {
                    CreateAndShowDialog(ex, "Authentication failed");
                }
                return success;
        }
   
        [Java.Interop.Export()]
        public async void LoginUser(View view)
        {
            // Load data only after authentication succeeds.
            if (await Authenticate())
            {
                //Hide hello button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load hello data.
                OnRefreshItemsSelected();
            }
        }
   
    Bu yeni bir yöntem tooauthenticate bir kullanıcı bir yöntem işleyici yeni bir oluşturur ve **oturum** düğmesi. Yukarıdaki örnek kod hello Hello kullanıcı Facebook oturum açma kullanılarak doğrulanır. Bir iletişim kutusu bir kez kimlik doğrulaması kullanılan toodisplay hello kullanıcı kimliğidir.
   
   > [!NOTE]
   > Facebook dışında bir kimlik sağlayıcısı kullanıyorsanız, çok geçirilen hello değeri değiştirmek**LoginAsync** tooone hello aşağıdaki yukarıda: *MicrosoftAccount*, *Twitter*, *Google*, veya *WindowsAzureActiveDirectory*.
   > 
   > 
2. Merhaba, **OnCreate** yöntemi, delete ya da aşağıdaki kod satırını açıklama kullanıma hello:
   
        OnRefreshItemsSelected ();
3. Merhaba Activity_To_Do.axml dosyasında hello aşağıdakileri ekleyin *LoginUser* düğmesini hello varolan önce tanımını *addItem* düğmesi:
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. Aşağıdaki öğe toohello Strings.xml kaynaklar dosyasına hello ekleyin:
   
        <string name="login_button_text">Sign in</string>
5. Merhaba AndroidManifest.xml dosyasını açın, hello kod içinde aşağıdaki ekleme `<application>` XML öğesi:

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. Visual Studio veya Xamarin Studio, bir cihaz veya öykünücü hello istemci projesi çalıştırın ve seçilen kimlik sağlayıcınız ile oturum açın. Başarıyla oturum açma zaman hello uygulama oturum açma Kimliğiniz görüntülenir ve hello listesi Yapılacaklar öğelerini ve güncelleştirmeleri toohello veri yapabilirsiniz.

<!-- URLs. -->
[Xamarin.Android uygulaması oluşturma]: app-service-mobile-xamarin-android-get-started.md