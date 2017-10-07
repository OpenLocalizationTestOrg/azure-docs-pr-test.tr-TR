---
title: "aaaAdd authentication tooyour Evrensel Windows Platformu (UWP) uygulamasını | Microsoft Docs"
description: "Bilgi nasıl toouse Azure App Service Mobile Apps tooauthenticate kullanıcıların kimlik sağlayıcıları dahil olmak üzere, çeşitli kullanarak, Evrensel Windows Platformu (UWP) uygulamanızın: AAD, Google, Facebook, Twitter ve Microsoft."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 6cffd951-893e-4ce5-97ac-86e3f5ad9466
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: ad4477e9509f1c40c33e71818e268f6857fe1e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-windows-app"></a>Kimlik doğrulaması tooyour Windows uygulaması Ekle
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

Bu konu, nasıl gösterir tooadd bulut tabanlı kimlik doğrulaması tooyour mobil uygulama. Bu öğreticide, Azure App Service tarafından desteklenen bir kimlik sağlayıcısı kullanarak mobil uygulamalar için kimlik doğrulama toohello Evrensel Windows Platformu (UWP) hızlı başlangıç projesi ekleyin. Başarılı bir şekilde kimliği doğrulanmış ve, mobil uygulama arka ucu tarafından yetkili sonra hello kullanıcı kimliği değeri görüntülenir.

Bu öğretici hello Mobile Apps quickstart üzerinde temel alır. Merhaba öğretici ilk tamamlamalısınız [Mobile Apps'i kullanmaya başlamak](app-service-mobile-windows-store-dotnet-get-started.md).

## <a name="register"></a>Kimlik doğrulaması için uygulamanızı kaydetmenizi ve hello uygulama hizmetini yapılandırma
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

Şimdi, bu anonim erişim tooyour arka uç devre dışı doğrulayabilirsiniz. Merhaba UWP uygulaması projesi hello başlangıç projesi olarak ayarla, dağıtmak ve hello uygulamayı çalıştırın; Merhaba uygulama başladıktan sonra durum koduyla işlenmeyen bir özel durum 401 (yetkisiz) tetiklenir doğrulayın. Merhaba uygulama tooaccess mobil uygulama kodunuzu kimliği doğrulanmamış bir kullanıcı olarak çalışır. Bunun nedeni, ancak hello *Todoıtem* tablo artık kimlik doğrulaması gerektirir.

Ardından, uygulama hizmetinizden kaynakları istemeden önce hello uygulama tooauthenticate kullanıcılar güncelleştirir.

## <a name="add-authentication"></a>Kimlik doğrulama toohello uygulama Ekle
1. MainPage.xaml.cs Hello UWP uygulaması projesi dosyasını ve kod parçacığını aşağıdaki hello ekleyin:
   
        // Define a member variable for storing hello signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs hello authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' toohello name of your MobileServiceClient instance.
                // Sign-in using Facebook authentication.
                user = await App.MobileService
                    .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                message =
                    string.Format("You are now signed in - {0}", user.UserId);
   
                success = true;
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
            return success;
        }
   
    Bu kod bir Facebook oturum açma ile Merhaba kullanıcının kimliğini doğrular. Facebook dışında bir kimlik sağlayıcısı kullanıyorsanız, hello değerini değiştirme **MobileServiceAuthenticationProvider** sağlayıcınız toohello değerin üzerinde.
2. Hello yerine **OnNavigatedTo()** MainPage.xaml.cs yöntemi. Sonra ekleyeceksiniz bir **oturum** kimlik doğrulamasını tetikler düğmesi toohello uygulama.

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. Aşağıdaki kod parçacığını toohello MainPage.xaml.cs hello ekleyin:
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login hello user and then load data from hello mobile app.
            if (await AuthenticateAsync())
            {
                // Switch hello buttons and load items from hello mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. Merhaba MainPage.xaml proje dosyasını açın, hello tanımlar hello öğesini bulun **kaydetmek** düğmesine tıklayın ve kodu aşağıdaki hello ile değiştirin:
   
        <Button Name="ButtonSave" Visibility="Collapsed" Margin="0,8,8,0" 
                Click="ButtonSave_Click">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Add"/>
                <TextBlock Margin="5">Save</TextBlock>
            </StackPanel>
        </Button>
        <Button Name="ButtonLogin" Visibility="Visible" Margin="0,8,8,0" 
                Click="ButtonLogin_Click" TabIndex="0">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Permissions"/>
                <TextBlock Margin="5">Sign in</TextBlock> 
            </StackPanel>
        </Button>
5. Aşağıdaki kod parçacığını toohello App.xaml.cs hello ekleyin:

        protected override void OnActivated(IActivatedEventArgs args)
        {
            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                Frame content = Window.Current.Content as Frame;
                if (content.Content.GetType() == typeof(MainPage))
                {
                    content.Navigate(typeof(MainPage), protocolArgs.Uri);
                }
            }
            Window.Current.Activate();
            base.OnActivated(args);
        }
6. Package.appxmanifest dosyasını açın, çok gidin**bildirimleri**, **kullanılabilir bildirimleri** açılır listesinden, **Protokolü** tıklatıp **Ekle** düğmesi. Şimdi hello yapılandırmak **özellikleri** Merhaba, **Protokolü** bildirimi. İçinde **görünen adı**, uygulamanızın toodisplay toousers istediğiniz hello adını ekleyin. İçinde **adı**, {url_scheme_of_your_app} ekleyin.
7. Merhaba Hello F5 anahtar toorun hello uygulama tuşlarına basın, **oturum** düğmesi ve seçilen kimlik sağlayıcınızı hello uygulamada oturum. Oturum açma işleminiz başarılı olduktan sonra hello uygulama hatasız çalışır ve arka mümkün tooquery olan ve güncelleştirmeleri toodata yapın.

## <a name="tokens"></a>Merhaba istemcide deposu hello kimlik doğrulama belirteci
Merhaba önceki örnek bir standart oturum hello istemci toocontact gerektiren açma, her iki hello kimlik sağlayıcısı gösterdi ve bu hello uygulama her başlatıldığında uygulama hizmeti hello. Bu yöntemi yalnızca çalıştırabilirsiniz verimsiz olduğu halinde kullanım-sorunları birçok müşteri deneyin toostart ilişkili Merhaba, uygulamaya aynı anda. Daha iyi bir toocache hello yetkilendirme belirtecini try toouse ve uygulama hizmeti bu ilk önce bir sağlayıcı tabanlı oturum açma kullanarak döndürülen yaklaşımdır.

> [!NOTE]
> Uygulama Hizmetleri tarafından yönetilen istemci veya hizmet tarafından yönetilen kimlik doğrulaması kullanıp bağımsız olarak hello belirteç önbelleğe alabilir. Bu öğretici, kimlik doğrulama hizmeti tarafından yönetilen kullanır.
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a>Sonraki adımlar
Bu temel kimlik doğrulaması öğreticisini tamamladığınıza göre öğreticileri aşağıdaki hello tooone üzerinde etmeden göz önünde bulundurun:

* [Anında iletme bildirimleri tooyour uygulama Ekle](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  Mobil uygulama arka uç toouse Azure Notification Hubs toosend anında iletme bildirimleri yapılandırmak ve tooadd anında iletme bildirimleri tooyour uygulama'ı nasıl desteklediğini öğrenin.
* [Uygulamanız için çevrimdışı eşitlemeyi etkinleştirme](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Bir mobil uygulama arka ucu kullanarak uygulamanıza çevrimdışı tooadd destek nasıl bilgi edinin. Çevrimdışı eşitleme sağlayan bir mobil uygulama ile son kullanıcılar toointeract&mdash;görüntüleme, ekleme veya değiştirme veri&mdash;hiçbir ağ bağlantısı olduğunda bile.

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
