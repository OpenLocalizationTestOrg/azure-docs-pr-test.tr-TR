---
title: "Xamarin Forms uygulamasında mobil uygulamalar için kimlik doğrulaması ile başlatıldı aaaGet | Microsoft Docs"
description: "Bilgi nasıl toouse Mobile Apps tooauthenticate kullanıcıların kimlik sağlayıcıları, AAD, Google, Facebook, Twitter ve Microsoft dahil olmak üzere çeşitli Xamarin Forms uygulamanızın."
services: app-service\mobile
documentationcenter: xamarin
author: panarasi
manager: syntaxc4
editor: 
ms.assetid: 9c55e192-c761-4ff2-8d88-72260e9f6179
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: panarasi
ms.openlocfilehash: 7f6716619f33d9cc4f866c41effba8f048dc49fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarin-forms-app"></a>Kimlik doğrulama tooyour Xamarin Forms uygulama Ekle
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a>Genel Bakış
Bu konu, nasıl gösterir bir mobil uygulama hizmeti, istemci uygulamasından tooauthenticate kullanıcıları. Bu öğretici kapsamında, kimlik doğrulama App Service tarafından desteklenen bir kimlik sağlayıcısı kullanarak hello Xamarin Forms hızlı başlangıç projesi ekleyin. Mobil uygulamanız tarafından yetkili başarılı bir şekilde kimliği doğrulanmış ve sonra hello kullanıcı kimliği değeri görüntülenir ve kısıtlı mümkün tooaccess tablo verisi olacaktır.

## <a name="prerequisites"></a>Ön koşullar
Merhaba en iyi sonuç almak için Bu öğretici ile Merhaba ilk tamamlamak olan öneririz [Xamarin Forms uygulaması oluşturma] [ 1] Öğreticisi. Bu öğreticiyi tamamladıktan sonra bir çok platformlu Yapılacaklar listesi uygulamasıyla Xamarin Forms proje sahip olur.

Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, hello kimlik doğrulaması uzantı paketini tooyour projesi eklemeniz gerekir. Server uzantısı paketleri hakkında daha fazla bilgi için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş][2].

## <a name="register-your-app-for-authentication-and-configure-app-services"></a>Kimlik doğrulaması için uygulamanızı kaydetme ve uygulama hizmetlerini yapılandırma
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Uygulama toohello izin verilen dış yönlendirme URL'lerini ekleme

Uygulamanız için yeni bir URL şemasını tanımlamak güvenli kimlik doğrulaması gerektirir. Merhaba kimlik doğrulama işlemi tamamlandıktan sonra bu hello authentication sistem tooredirect geri tooyour uygulamasını sağlar. Bu öğreticide, kullandığımız hello URL şeması _appname_ boyunca. Ancak, seçtiğiniz herhangi bir URL şeması kullanabilirsiniz. Benzersiz tooyour mobil uygulama olmalıdır. Merhaba sunucu tarafı tooenable hello yönlendirme:

1. Hello [Azure portalı]'da, uygulama hizmeti seçin.

2. Merhaba tıklatın **kimlik doğrulama / yetkilendirme** menü seçeneği.

3. Merhaba, **yeniden yönlendirme URL'lere izin**, girin `url_scheme_of_your_app://easyauth.callback`.  Merhaba **url_scheme_of_your_app** bu içinde hello URL şeması mobil uygulamanız için bir dizedir.  Bir protokol (harf kullanın ve yalnızca sayı ve bir harf ile başlar) için normal URL belirtimi izlemelisiniz.  Merhaba çeşitli yerlerde URL şeması ile mobil uygulama kodunuzu tooadjust gerekeceğinden, seçtiğiniz hello dize Not olmanız gerekir.

4. **Tamam** düğmesine tıklayın.

5. **Kaydet** düğmesine tıklayın.

## <a name="restrict-permissions-tooauthenticated-users"></a>İzinleri tooauthenticated kullanıcılarını kısıtlayın
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-toohello-portable-class-library"></a>Kimlik doğrulama toohello taşınabilir sınıf kitaplığı ekleyin
Mobile Apps kullanan hello [LoginAsync] [ 3] genişletme yöntemi hello üzerinde [MobileServiceClient] [ 4] toosign bir kullanıcı için uygulama hizmeti ile kimlik doğrulaması. Bu örnek hello uygulamada oturum açma hello sağlayıcının arabirimi görüntüler bir sunucu yönetilen kimlik doğrulama akışı kullanır. Daha fazla bilgi için bkz: [kimlik doğrulama sunucusu yönetilen][5]. Üretim uygulamanızda daha iyi bir kullanıcı deneyimi sağlamak için dikkate almanız gereken kullanmayı [istemci yönetilen kimlik doğrulaması][6].

Xamarin Forms proje ile tooauthenticate tanımlayan bir **IAuthenticate** hello uygulaması için taşınabilir sınıf kitaplığı hello arabiriminde. Ardından ekleyin bir **oturum açma** düğmesini toohello kullanıcı arabirimi başlangıç'ı taşınabilir sınıf kitaplığı tanımlanan toostart kimlik doğrulaması. Veriler başarılı kimlik doğrulamasından sonra hello mobil uygulama arka ucundan yüklenir.

Uygulama hello **IAuthenticate** uygulamanız tarafından desteklenen her platform için arabirim.

1. Visual Studio veya Xamarin Studio'da ile Merhaba projenizden App.cs açın **taşınabilir** taşınabilir sınıf kitaplığı proje olan hello ad sonra hello aşağıdakileri ekleyin `using` deyimi:

        using System.Threading.Tasks;
2. App.cs içinde hello aşağıdakileri ekleyin `IAuthenticate` arabirimi tanımından hemen önce hello `App` sınıf tanımının.

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. tooinitialize hello arabirimi platforma özgü bir uygulama eklemek statik üyeler toohello aşağıdaki hello **uygulama** sınıfı.

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. Merhaba taşınabilir sınıf kitaplığı proje TodoList.xaml açın, hello aşağıdakileri ekleyin **düğmesini** hello öğesinde *buttonsPanel* hello varolan bir düğmeyi sonra Düzen öğesi:

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    Bu düğme, mobil uygulama arka ucu ile kimlik doğrulama sunucusu yönetilen tetikler.
5. Merhaba taşınabilir sınıf kitaplığı proje TodoList.xaml.cs açın ve ardından alan toohello aşağıdaki hello eklemek `TodoList` sınıfı:

        // Track whether hello user has authenticated.
        bool authenticated = false;
6. Hello yerine **OnAppearing** koddan hello yöntemiyle:

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems tootrue in order toosynchronize hello data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide hello Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    Bu kod, doğrulanan sonra veriler yalnızca hello hizmetinden yenilenir emin olur.
7. Hello için işleyici aşağıdaki hello eklemek **tıklama** olay toohello **TodoList** sınıfı:

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems tootrue toosynchronize hello data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. Değişikliklerinizi kaydetmek ve hiçbir hata doğrulama hello taşınabilir sınıf kitaplığı proje derleyin.

## <a name="add-authentication-toohello-android-app"></a>Kimlik doğrulama toohello Android uygulaması ekleyin
Bu bölümde gösterilmiştir nasıl tooimplement hello **IAuthenticate** hello Android uygulama projesi arabiriminde. Android cihazları destekleme değil, bu bölümü atlayabilirsiniz.

1. Visual Studio veya Xamarin Studio'da hello sağ **droid** , sonra da proje **başlangıç projesi olarak ayarla**.
2. F5 toostart hello proje hello hata ayıklayıcıda tuşuna basın, sonra uygulama başladıktan sonra durum koduyla işlenmeyen bir özel durum 401 (yetkisiz) tetiklenir doğrulayın. Merhaba arka uç erişimi yalnızca sınırlı tooauthorized kullanıcılar olduğundan hello 401 kodu oluşturulur.
3. MainActivity.cs hello Android projeyi açın ve hello aşağıdakileri ekleyin `using` deyimleri:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. Güncelleştirme hello **MainActivity** sınıfı tooimplement hello **IAuthenticate** arabirimi, aşağıdaki gibi:

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. Güncelleştirme hello **MainActivity** ekleyerek sınıfı bir **MobileServiceUser** alan ve bir **kimlik doğrulama** hello tarafından gerekli yöntemi **IAuthenticate**  arabirimi, aşağıdaki gibi:

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                user = await TodoItemManager.DefaultManager.CurrentClient.LoginAsync(this, 
                    MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                if (user != null)
                {
                    message = string.Format("you are now signed-in as {0}.",
                        user.UserId);
                    success = true;
                }
            }
            catch (Exception ex)
            {
                message = ex.Message;
            }

            // Display hello success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    Facebook dışında bir kimlik sağlayıcısı kullanıyorsanız, için farklı bir değer seçin [MobileServiceAuthenticationProvider][7].

6. Kod içinde aşağıdaki hello eklemek <application> AndroidManifest.xml düğümünün:

```xml
    <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
      <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
      </intent-filter>
    </activity>
```

1. Aşağıdaki kodu toohello hello eklemek **OnCreate** hello yöntemi **MainActivity** hello çağrısından önce çok sınıf`LoadApplication()`:

        // Initialize hello authenticator before loading hello app.
        App.Init((IAuthenticate)this);

    Bu kod hello Doğrulayıcı hello uygulama yükleri önce başlatılmış sağlar.
2. Merhaba uygulama yeniden, çalıştırın ve sonra seçtiğiniz ve kimliği doğrulanmış bir kullanıcı olarak mümkün tooaccess verileri doğrulayın hello kimlik doğrulama sağlayıcısının oturum açın.

## <a name="add-authentication-toohello-ios-app"></a>Kimlik doğrulama toohello iOS uygulaması ekleyin
Bu bölümde gösterilmiştir nasıl tooimplement hello **IAuthenticate** hello iOS uygulaması projesi arabiriminde. İOS cihazları destekleme değil, bu bölümü atlayabilirsiniz.

1. Visual Studio veya Xamarin Studio'da hello sağ **iOS** , sonra da proje **başlangıç projesi olarak ayarla**.
2. F5 toostart hello proje hello hata ayıklayıcıda tuşuna basın, sonra hello uygulama başladıktan sonra durum koduyla işlenmeyen bir özel durum 401 (yetkisiz) tetiklenir doğrulayın. Merhaba arka uç erişimi yalnızca sınırlı tooauthorized kullanıcılar olduğundan hello 401 yanıtı oluşturulur.
3. AppDelegate.cs hello iOS projeyi açın ve hello aşağıdakileri ekleyin `using` deyimleri:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. Güncelleştirme hello **AppDelegate** sınıfı tooimplement hello **IAuthenticate** arabirimi, aşağıdaki gibi:

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. Güncelleştirme hello **AppDelegate** ekleyerek sınıfı bir **MobileServiceUser** alan ve bir **kimlik doğrulama** hello tarafından gerekli yöntemi **IAuthenticate**  arabirimi, aşağıdaki gibi:

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(UIApplication.SharedApplication.KeyWindow.RootViewController,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                        success = true;
                    }
                }
            }
            catch (Exception ex)
            {
               message = ex.Message;
            }

            // Display hello success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    Facebook dışında bir kimlik sağlayıcısı kullanıyorsanız, [MobileServiceAuthenticationProvider] için farklı bir değer seçin.

6. OpenUrl (Uıapplication uygulama, NSUrl url NSDictionary seçenekleri) yöntemi aşırı yüklemesini ekleyerek Hello AppDelegate sınıfını güncelleştirme

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. Kod toohello satırının aşağıdaki hello eklemek **FinishedLaunching** hello önce yöntemini çağırın çok`LoadApplication()`:

        App.Init(this);

    Bu kod hello Doğrulayıcı hello uygulama yüklenmeden önce başlatılmış sağlar.

6. Ekleme **{url_scheme_of_your_app}** Info.plist tooURL düzenleri.

7. Merhaba uygulama yeniden, çalıştırın ve sonra seçtiğiniz ve kimliği doğrulanmış bir kullanıcı olarak mümkün tooaccess verileri doğrulayın hello kimlik doğrulama sağlayıcısının oturum açın.

## <a name="add-authentication-toowindows-10-including-phone-app-projects"></a>Kimlik doğrulama tooWindows 10 (dahil olmak üzere telefon) eklemek uygulaması projeleri
Bu bölümde gösterilmiştir nasıl tooimplement hello **IAuthenticate** hello Windows 10 uygulaması projeleri arabiriminde. Evrensel Windows Platformu (UWP) projeleri, ancak hello kullanarak için aynı adımları uygulamak hello **UWP** projeyle (not ettiğiniz değişir). Windows cihazları destekleme değil, bu bölümü atlayabilirsiniz.

1. "Visual Studio'da ya da hello sağ **UWP** , sonra da proje **başlangıç projesi olarak ayarla**.
2. F5 toostart hello proje hello hata ayıklayıcıda tuşuna basın, sonra hello uygulama başladıktan sonra durum koduyla işlenmeyen bir özel durum 401 (yetkisiz) tetiklenir doğrulayın. Merhaba arka uç erişimi yalnızca sınırlı tooauthorized kullanıcılar olduğundan hello 401 yanıt olur.
3. MainPage.xaml.cs hello Windows uygulama projesi için açın ve hello aşağıdakileri ekleyin `using` deyimleri:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    Değiştir `<your_Portable_Class_Library_namespace>` ile taşınabilir sınıf kitaplığı için hello ad alanı.
4. Güncelleştirme hello **MainPage** sınıfı tooimplement hello **IAuthenticate** arabirimi, aşağıdaki gibi:

        public sealed partial class MainPage : IAuthenticate
5. Güncelleştirme hello **MainPage** ekleyerek sınıfı bir **MobileServiceUser** alan ve bir **kimlik doğrulama** hello tarafından gerekli yöntemi **IAuthenticate** arabirimi, aşağıdaki gibi:

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            string message = string.Empty;
            var success = false;

            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        success = true;
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                    }
                }

            }
            catch (Exception ex)
            {
                message = string.Format("Authentication Failed: {0}", ex.Message);
            }

            // Display hello success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    Facebook dışında bir kimlik sağlayıcısı kullanıyorsanız, [MobileServiceAuthenticationProvider] için farklı bir değer seçin.

1. Aşağıdaki kod hello hello oluşturucuda hello eklemek **MainPage** hello çağrısından önce çok sınıf`LoadApplication()`:

        // Initialize hello authenticator before loading hello app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    Değiştir `<your_Portable_Class_Library_namespace>` ile taşınabilir sınıf kitaplığı için hello ad alanı.

3. Kullanıyorsanız **UWP**, hello aşağıdakileri ekleyin **OnActivated** yöntemini geçersiz kılın toohello **uygulama** sınıfı:

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   Merhaba yöntemi geçersiz kılma zaten mevcut olduğunda hello koşullu kod parçacığını önceki hello ekleyin.  Bu kod, Evrensel Windows projeleri için gerekli değildir.

3. Ekleme **{url_scheme_of_your_app}** Package.appxmanifest içinde. 

4. Merhaba uygulama yeniden, çalıştırın ve sonra seçtiğiniz ve kimliği doğrulanmış bir kullanıcı olarak mümkün tooaccess verileri doğrulayın hello kimlik doğrulama sağlayıcısının oturum açın.

## <a name="next-steps"></a>Sonraki adımlar
Bu temel kimlik doğrulaması öğreticisini tamamladığınıza göre öğreticileri aşağıdaki hello tooone üzerinde etmeden göz önünde bulundurun:

* [Anında iletme bildirimleri tooyour uygulama Ekle](app-service-mobile-xamarin-forms-get-started-push.md)

  Mobil uygulama arka uç toouse Azure Notification Hubs toosend anında iletme bildirimleri yapılandırmak ve tooadd anında iletme bildirimleri tooyour uygulama'ı nasıl desteklediğini öğrenin.
* [Uygulamanız için çevrimdışı eşitlemeyi etkinleştirme](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  Bir mobil uygulama arka ucu kullanarak uygulamanıza çevrimdışı tooadd destek nasıl bilgi edinin. Çevrimdışı eşitleme son kullanıcıların toointeract ile mobil uygulama görüntüleme, ekleme veya ağ bağlantısı olduğunda bile veri - değiştirme - sağlar.

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
