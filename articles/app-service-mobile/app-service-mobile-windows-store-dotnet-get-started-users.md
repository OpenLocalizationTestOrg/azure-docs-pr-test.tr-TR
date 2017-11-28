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
# <a name="add-authentication-tooyour-windows-app"></a><span data-ttu-id="c9197-103">Kimlik doğrulaması tooyour Windows uygulaması Ekle</span><span class="sxs-lookup"><span data-stu-id="c9197-103">Add authentication tooyour Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="c9197-104">Bu konu, nasıl gösterir tooadd bulut tabanlı kimlik doğrulaması tooyour mobil uygulama.</span><span class="sxs-lookup"><span data-stu-id="c9197-104">This topic shows you how tooadd cloud-based authentication tooyour mobile app.</span></span> <span data-ttu-id="c9197-105">Bu öğreticide, Azure App Service tarafından desteklenen bir kimlik sağlayıcısı kullanarak mobil uygulamalar için kimlik doğrulama toohello Evrensel Windows Platformu (UWP) hızlı başlangıç projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c9197-105">In this tutorial, you add authentication toohello Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span></span> <span data-ttu-id="c9197-106">Başarılı bir şekilde kimliği doğrulanmış ve, mobil uygulama arka ucu tarafından yetkili sonra hello kullanıcı kimliği değeri görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c9197-106">After being successfully authenticated and authorized by your Mobile App backend, hello user ID value is displayed.</span></span>

<span data-ttu-id="c9197-107">Bu öğretici hello Mobile Apps quickstart üzerinde temel alır.</span><span class="sxs-lookup"><span data-stu-id="c9197-107">This tutorial is based on hello Mobile Apps quickstart.</span></span> <span data-ttu-id="c9197-108">Merhaba öğretici ilk tamamlamalısınız [Mobile Apps'i kullanmaya başlamak](app-service-mobile-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c9197-108">You must first complete hello tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span></span>

## <span data-ttu-id="c9197-109"><a name="register"></a>Kimlik doğrulaması için uygulamanızı kaydetmenizi ve hello uygulama hizmetini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c9197-109"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="c9197-110"><a name="redirecturl"></a>Uygulama toohello izin verilen dış yönlendirme URL'lerini ekleme</span><span class="sxs-lookup"><span data-stu-id="c9197-110"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="c9197-111">Uygulamanız için yeni bir URL şemasını tanımlamak güvenli kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c9197-111">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="c9197-112">Merhaba kimlik doğrulama işlemi tamamlandıktan sonra bu hello authentication sistem tooredirect geri tooyour uygulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="c9197-112">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="c9197-113">Bu öğreticide, kullandığımız hello URL şeması _appname_ boyunca.</span><span class="sxs-lookup"><span data-stu-id="c9197-113">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="c9197-114">Ancak, seçtiğiniz herhangi bir URL şeması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9197-114">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="c9197-115">Benzersiz tooyour mobil uygulama olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c9197-115">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="c9197-116">Merhaba sunucu tarafı tooenable hello yönlendirme:</span><span class="sxs-lookup"><span data-stu-id="c9197-116">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="c9197-117">Hello [Azure portalı]'da, uygulama hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="c9197-117">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="c9197-118">Merhaba tıklatın **kimlik doğrulama / yetkilendirme** menü seçeneği.</span><span class="sxs-lookup"><span data-stu-id="c9197-118">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="c9197-119">Merhaba, **yeniden yönlendirme URL'lere izin**, girin `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="c9197-119">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="c9197-120">Merhaba **url_scheme_of_your_app** bu içinde hello URL şeması mobil uygulamanız için bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="c9197-120">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="c9197-121">Bir protokol (harf kullanın ve yalnızca sayı ve bir harf ile başlar) için normal URL belirtimi izlemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="c9197-121">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="c9197-122">Merhaba çeşitli yerlerde URL şeması ile mobil uygulama kodunuzu tooadjust gerekeceğinden, seçtiğiniz hello dize Not olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9197-122">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="c9197-123">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9197-123">Click **OK**.</span></span>

5. <span data-ttu-id="c9197-124">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9197-124">Click **Save**.</span></span>

## <span data-ttu-id="c9197-125"><a name="permissions"></a>İzinleri tooauthenticated kullanıcılarını kısıtlayın</span><span class="sxs-lookup"><span data-stu-id="c9197-125"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="c9197-126">Şimdi, bu anonim erişim tooyour arka uç devre dışı doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9197-126">Now, you can verify that anonymous access tooyour backend has been disabled.</span></span> <span data-ttu-id="c9197-127">Merhaba UWP uygulaması projesi hello başlangıç projesi olarak ayarla, dağıtmak ve hello uygulamayı çalıştırın; Merhaba uygulama başladıktan sonra durum koduyla işlenmeyen bir özel durum 401 (yetkisiz) tetiklenir doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c9197-127">With hello UWP app project set as hello start-up project, deploy and run hello app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="c9197-128">Merhaba uygulama tooaccess mobil uygulama kodunuzu kimliği doğrulanmamış bir kullanıcı olarak çalışır. Bunun nedeni, ancak hello *Todoıtem* tablo artık kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c9197-128">This happens because hello app attempts tooaccess your Mobile App Code as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="c9197-129">Ardından, uygulama hizmetinizden kaynakları istemeden önce hello uygulama tooauthenticate kullanıcılar güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="c9197-129">Next, you will update hello app tooauthenticate users before requesting resources from your App Service.</span></span>

## <span data-ttu-id="c9197-130"><a name="add-authentication"></a>Kimlik doğrulama toohello uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="c9197-130"><a name="add-authentication"></a>Add authentication toohello app</span></span>
1. <span data-ttu-id="c9197-131">MainPage.xaml.cs Hello UWP uygulaması projesi dosyasını ve kod parçacığını aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c9197-131">In hello UWP app project file MainPage.xaml.cs and add hello following code snippet:</span></span>
   
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
   
    <span data-ttu-id="c9197-132">Bu kod bir Facebook oturum açma ile Merhaba kullanıcının kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="c9197-132">This code authenticates hello user with a Facebook login.</span></span> <span data-ttu-id="c9197-133">Facebook dışında bir kimlik sağlayıcısı kullanıyorsanız, hello değerini değiştirme **MobileServiceAuthenticationProvider** sağlayıcınız toohello değerin üzerinde.</span><span class="sxs-lookup"><span data-stu-id="c9197-133">If you are using an identity provider other than Facebook, change hello value of **MobileServiceAuthenticationProvider** above toohello value for your provider.</span></span>
2. <span data-ttu-id="c9197-134">Hello yerine **OnNavigatedTo()** MainPage.xaml.cs yöntemi.</span><span class="sxs-lookup"><span data-stu-id="c9197-134">Replace hello **OnNavigatedTo()** method in MainPage.xaml.cs.</span></span> <span data-ttu-id="c9197-135">Sonra ekleyeceksiniz bir **oturum** kimlik doğrulamasını tetikler düğmesi toohello uygulama.</span><span class="sxs-lookup"><span data-stu-id="c9197-135">Next, you will add a **Sign in** button toohello app that triggers authentication.</span></span>

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. <span data-ttu-id="c9197-136">Aşağıdaki kod parçacığını toohello MainPage.xaml.cs hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c9197-136">Add hello following code snippet toohello MainPage.xaml.cs:</span></span>
   
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
4. <span data-ttu-id="c9197-137">Merhaba MainPage.xaml proje dosyasını açın, hello tanımlar hello öğesini bulun **kaydetmek** düğmesine tıklayın ve kodu aşağıdaki hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="c9197-137">Open hello MainPage.xaml project file, locate hello element that defines hello **Save** button and replace it with hello following code:</span></span>
   
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
5. <span data-ttu-id="c9197-138">Aşağıdaki kod parçacığını toohello App.xaml.cs hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c9197-138">Add hello following code snippet toohello App.xaml.cs:</span></span>

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
6. <span data-ttu-id="c9197-139">Package.appxmanifest dosyasını açın, çok gidin**bildirimleri**, **kullanılabilir bildirimleri** açılır listesinden, **Protokolü** tıklatıp **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c9197-139">Open Package.appxmanifest file, navigate too**Declarations**, in **Available Declarations** dropdown list, select **Protocol** and click **Add** button.</span></span> <span data-ttu-id="c9197-140">Şimdi hello yapılandırmak **özellikleri** Merhaba, **Protokolü** bildirimi.</span><span class="sxs-lookup"><span data-stu-id="c9197-140">Now configure hello **Properties** of hello **Protocol** declaration.</span></span> <span data-ttu-id="c9197-141">İçinde **görünen adı**, uygulamanızın toodisplay toousers istediğiniz hello adını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c9197-141">In **Display name**, add hello name you wish toodisplay toousers of your application.</span></span> <span data-ttu-id="c9197-142">İçinde **adı**, {url_scheme_of_your_app} ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c9197-142">In **Name**, add your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="c9197-143">Merhaba Hello F5 anahtar toorun hello uygulama tuşlarına basın, **oturum** düğmesi ve seçilen kimlik sağlayıcınızı hello uygulamada oturum.</span><span class="sxs-lookup"><span data-stu-id="c9197-143">Press hello F5 key toorun hello app, click hello **Sign in** button, and sign into hello app with your chosen identity provider.</span></span> <span data-ttu-id="c9197-144">Oturum açma işleminiz başarılı olduktan sonra hello uygulama hatasız çalışır ve arka mümkün tooquery olan ve güncelleştirmeleri toodata yapın.</span><span class="sxs-lookup"><span data-stu-id="c9197-144">After your sign-in is successful, hello app runs without errors and you are able tooquery your backend and make updates toodata.</span></span>

## <span data-ttu-id="c9197-145"><a name="tokens"></a>Merhaba istemcide deposu hello kimlik doğrulama belirteci</span><span class="sxs-lookup"><span data-stu-id="c9197-145"><a name="tokens"></a>Store hello authentication token on hello client</span></span>
<span data-ttu-id="c9197-146">Merhaba önceki örnek bir standart oturum hello istemci toocontact gerektiren açma, her iki hello kimlik sağlayıcısı gösterdi ve bu hello uygulama her başlatıldığında uygulama hizmeti hello.</span><span class="sxs-lookup"><span data-stu-id="c9197-146">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello App Service every time that hello app starts.</span></span> <span data-ttu-id="c9197-147">Bu yöntemi yalnızca çalıştırabilirsiniz verimsiz olduğu halinde kullanım-sorunları birçok müşteri deneyin toostart ilişkili Merhaba, uygulamaya aynı anda.</span><span class="sxs-lookup"><span data-stu-id="c9197-147">Not only is this method inefficient, you can run into usage-relates issues should many customers try toostart you app at hello same time.</span></span> <span data-ttu-id="c9197-148">Daha iyi bir toocache hello yetkilendirme belirtecini try toouse ve uygulama hizmeti bu ilk önce bir sağlayıcı tabanlı oturum açma kullanarak döndürülen yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="c9197-148">A better approach is toocache hello authorization token returned by your App Service and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="c9197-149">Uygulama Hizmetleri tarafından yönetilen istemci veya hizmet tarafından yönetilen kimlik doğrulaması kullanıp bağımsız olarak hello belirteç önbelleğe alabilir.</span><span class="sxs-lookup"><span data-stu-id="c9197-149">You can cache hello token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="c9197-150">Bu öğretici, kimlik doğrulama hizmeti tarafından yönetilen kullanır.</span><span class="sxs-lookup"><span data-stu-id="c9197-150">This tutorial uses service-managed authentication.</span></span>
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="c9197-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c9197-151">Next steps</span></span>
<span data-ttu-id="c9197-152">Bu temel kimlik doğrulaması öğreticisini tamamladığınıza göre öğreticileri aşağıdaki hello tooone üzerinde etmeden göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="c9197-152">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="c9197-153">Anında iletme bildirimleri tooyour uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="c9197-153">Add push notifications tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="c9197-154">Mobil uygulama arka uç toouse Azure Notification Hubs toosend anında iletme bildirimleri yapılandırmak ve tooadd anında iletme bildirimleri tooyour uygulama'ı nasıl desteklediğini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c9197-154">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="c9197-155">Uygulamanız için çevrimdışı eşitlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c9197-155">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="c9197-156">Bir mobil uygulama arka ucu kullanarak uygulamanıza çevrimdışı tooadd destek nasıl bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="c9197-156">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="c9197-157">Çevrimdışı eşitleme sağlayan bir mobil uygulama ile son kullanıcılar toointeract&mdash;görüntüleme, ekleme veya değiştirme veri&mdash;hiçbir ağ bağlantısı olduğunda bile.</span><span class="sxs-lookup"><span data-stu-id="c9197-157">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
