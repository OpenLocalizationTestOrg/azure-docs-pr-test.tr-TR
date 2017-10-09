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
# <a name="add-authentication-tooyour-xamarinios-app"></a><span data-ttu-id="c4e68-103">Kimlik doğrulama tooyour Xamarin.iOS uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="c4e68-103">Add authentication tooyour Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="c4e68-104">Bu konu, nasıl gösterir bir mobil uygulama hizmeti, istemci uygulamasından tooauthenticate kullanıcıları.</span><span class="sxs-lookup"><span data-stu-id="c4e68-104">This topic shows you how tooauthenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="c4e68-105">Bu öğreticide, App Service tarafından desteklenen bir kimlik sağlayıcısı kullanarak kimlik doğrulaması toohello Xamarin.iOS hızlı başlangıç projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c4e68-105">In this tutorial, you add authentication toohello Xamarin.iOS quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="c4e68-106">Mobil uygulamanız tarafından yetkili başarılı bir şekilde kimliği doğrulanmış ve sonra hello kullanıcı kimliği değeri görüntülenir ve kısıtlı mümkün tooaccess tablo verisi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c4e68-106">After being successfully authenticated and authorized by your Mobile App, hello user ID value is displayed and you will be able tooaccess restricted table data.</span></span>

<span data-ttu-id="c4e68-107">Merhaba öğretici ilk tamamlamalısınız [bir Xamarin.iOS uygulaması oluşturma].</span><span class="sxs-lookup"><span data-stu-id="c4e68-107">You must first complete hello tutorial [Create a Xamarin.iOS app].</span></span> <span data-ttu-id="c4e68-108">Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, hello kimlik doğrulaması uzantı paketini tooyour projesi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4e68-108">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="c4e68-109">Server uzantısı paketleri hakkında daha fazla bilgi için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="c4e68-109">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="c4e68-110">Kimlik doğrulaması için uygulamanızı kaydetme ve uygulama hizmetlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c4e68-110">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-toohello-allowed-external-redirect-urls"></a><span data-ttu-id="c4e68-111">Uygulama toohello izin verilen dış yönlendirme URL'lerini ekleme</span><span class="sxs-lookup"><span data-stu-id="c4e68-111">Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="c4e68-112">Uygulamanız için yeni bir URL şemasını tanımlamak güvenli kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c4e68-112">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="c4e68-113">Merhaba kimlik doğrulama işlemi tamamlandıktan sonra bu hello authentication sistem tooredirect geri tooyour uygulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="c4e68-113">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="c4e68-114">Bu öğreticide, kullandığımız hello URL şeması _appname_ boyunca.</span><span class="sxs-lookup"><span data-stu-id="c4e68-114">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="c4e68-115">Ancak, seçtiğiniz herhangi bir URL şeması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4e68-115">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="c4e68-116">Benzersiz tooyour mobil uygulama olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c4e68-116">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="c4e68-117">Merhaba sunucu tarafı tooenable hello yönlendirme:</span><span class="sxs-lookup"><span data-stu-id="c4e68-117">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="c4e68-118">Hello [Azure portalı]'da, uygulama hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="c4e68-118">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="c4e68-119">Merhaba tıklatın **kimlik doğrulama / yetkilendirme** menü seçeneği.</span><span class="sxs-lookup"><span data-stu-id="c4e68-119">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="c4e68-120">Merhaba, **yeniden yönlendirme URL'lere izin**, girin `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="c4e68-120">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="c4e68-121">Merhaba **url_scheme_of_your_app** bu içinde hello URL şeması mobil uygulamanız için bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="c4e68-121">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="c4e68-122">Bir protokol (harf kullanın ve yalnızca sayı ve bir harf ile başlar) için normal URL belirtimi izlemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="c4e68-122">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="c4e68-123">Merhaba çeşitli yerlerde URL şeması ile mobil uygulama kodunuzu tooadjust gerekeceğinden, seçtiğiniz hello dize Not olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4e68-123">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="c4e68-124">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c4e68-124">Click **OK**.</span></span>

5. <span data-ttu-id="c4e68-125">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c4e68-125">Click **Save**.</span></span>

## <a name="restrict-permissions-tooauthenticated-users"></a><span data-ttu-id="c4e68-126">İzinleri tooauthenticated kullanıcılarını kısıtlayın</span><span class="sxs-lookup"><span data-stu-id="c4e68-126">Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="c4e68-127">&nbsp;&nbsp;4.</span><span class="sxs-lookup"><span data-stu-id="c4e68-127">&nbsp;&nbsp;4.</span></span> <span data-ttu-id="c4e68-128">Visual Studio veya Xamarin Studio'da hello istemci projesi bir cihaz veya öykünücü çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c4e68-128">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator.</span></span> <span data-ttu-id="c4e68-129">Merhaba uygulama başladıktan sonra durum koduyla işlenmeyen bir özel durum 401 (yetkisiz) tetiklenir doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c4e68-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="c4e68-130">Merhaba, günlüğe kaydedilen toohello konsol hello hata ayıklayıcısının hatasıdır.</span><span class="sxs-lookup"><span data-stu-id="c4e68-130">hello failure is logged toohello console of hello debugger.</span></span> <span data-ttu-id="c4e68-131">Bu nedenle Visual Studio'da hello çıktı penceresinde hello hatası görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4e68-131">So in Visual Studio, you should see hello failure in hello output window.</span></span>

<span data-ttu-id="c4e68-132">&nbsp;&nbsp;Merhaba uygulama kimliği doğrulanmamış bir kullanıcı olarak, mobil uygulamanızın arka ucuna tooaccess çalıştığı yetkisiz bu hata gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="c4e68-132">&nbsp;&nbsp;This unauthorized failure happens because hello app attempts tooaccess your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="c4e68-133">Merhaba *Todoıtem* tablo artık kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c4e68-133">hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="c4e68-134">Ardından, kimliği doğrulanmış bir kullanıcı ile Merhaba istemci uygulaması toorequest hello mobil uygulama arka ucu kaynaklardan güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="c4e68-134">Next, you will update hello client app toorequest resources from hello Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication-toohello-app"></a><span data-ttu-id="c4e68-135">Kimlik doğrulama toohello uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="c4e68-135">Add authentication toohello app</span></span>
<span data-ttu-id="c4e68-136">Bu bölümde, veri görüntülemeden önce hello uygulama toodisplay bir oturum açma ekranı değiştirecektir.</span><span class="sxs-lookup"><span data-stu-id="c4e68-136">In this section, you will modify hello app toodisplay a login screen before displaying data.</span></span> <span data-ttu-id="c4e68-137">Merhaba uygulama başlatıldığında değil tooyour uygulama hizmeti bağlanmaz ve herhangi bir veri görüntülenmez.</span><span class="sxs-lookup"><span data-stu-id="c4e68-137">When hello app starts, it will not not connect tooyour App Service and will not display any data.</span></span> <span data-ttu-id="c4e68-138">İlk kez Hello sonra hello oturum açma ekranı görünür hello kullanıcı hello yenileme hareketi gerçekleştirir; başarılı oturum açma işleminden sonra hello Yapılacaklar öğelerini listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c4e68-138">After hello first time that hello user performs hello refresh gesture, hello login screen will appear; after successful login hello list of todo items will be displayed.</span></span>

1. <span data-ttu-id="c4e68-139">Merhaba istemci projesinde hello dosyasını açın **QSTodoService.cs** ve hello aşağıdakileri ekleyin deyimiyle ve `MobileServiceUser` erişimci toohello QSTodoService sınıfı ile:</span><span class="sxs-lookup"><span data-stu-id="c4e68-139">In hello client project, open hello file **QSTodoService.cs** and add hello following using statement and `MobileServiceUser` with accessor toohello QSTodoService class:</span></span>
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. <span data-ttu-id="c4e68-140">Adlı yeni bir yöntem ekleyin **kimlik doğrulama** çok**QSTodoService** tanımı aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="c4e68-140">Add new method named **Authenticate** too**QSTodoService** with hello following definition:</span></span>

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

    >[AZURE.NOTE] <span data-ttu-id="c4e68-141">Bir Facebook dışında bir kimlik sağlayıcısı kullanıyorsanız, çok geçirilen hello değeri değiştirmek**LoginAsync** tooone hello aşağıdaki yukarıda: _MicrosoftAccount_, _Twitter_, _Google_, veya _WindowsAzureActiveDirectory_.</span><span class="sxs-lookup"><span data-stu-id="c4e68-141">If you are using an identity provider other than a Facebook, change hello value passed too**LoginAsync** above tooone of hello following: _MicrosoftAccount_, _Twitter_, _Google_, or _WindowsAzureActiveDirectory_.</span></span>

3. <span data-ttu-id="c4e68-142">Açık **QSTodoListViewController.cs**.</span><span class="sxs-lookup"><span data-stu-id="c4e68-142">Open **QSTodoListViewController.cs**.</span></span> <span data-ttu-id="c4e68-143">Merhaba yöntemi tanımını değiştirme **ViewDidLoad** hello çağrısı çok kaldırma**RefreshAsync()** hello sona:</span><span class="sxs-lookup"><span data-stu-id="c4e68-143">Modify hello method definition of **ViewDidLoad** removing hello call too**RefreshAsync()** near hello end:</span></span>
   
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
4. <span data-ttu-id="c4e68-144">Merhaba yöntemi Değiştir **RefreshAsync** tooauthenticate hello varsa **kullanıcı** özelliği null.</span><span class="sxs-lookup"><span data-stu-id="c4e68-144">Modify hello method **RefreshAsync** tooauthenticate if hello **User** property is null.</span></span> <span data-ttu-id="c4e68-145">Merhaba yöntemi tanımı hello üstündeki koddan hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c4e68-145">Add hello following code at hello top of hello method definition:</span></span>
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. <span data-ttu-id="c4e68-146">Açık **AppDelegate.cs**, yöntem aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c4e68-146">Open **AppDelegate.cs**, add hello following method:</span></span>

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. <span data-ttu-id="c4e68-147">Açık **Info.plist** dosya, çok gidin**URL türleri** hello içinde **Gelişmiş** bölümü.</span><span class="sxs-lookup"><span data-stu-id="c4e68-147">Open **Info.plist** file, navigate too**URL Types** in hello **Advanced** section.</span></span> <span data-ttu-id="c4e68-148">Şimdi hello yapılandırmak **tanımlayıcısı** ve hello **URL şemalarını** URL türü ve tıklatın **URL türü Ekle**.</span><span class="sxs-lookup"><span data-stu-id="c4e68-148">Now configure hello **Identifier** and hello **URL Schemes** of your URL Type and click **Add URL Type**.</span></span> <span data-ttu-id="c4e68-149">**URL şemalarını** {url_scheme_of_your_app} hello aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c4e68-149">**URL Schemes** should be hello same as your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="c4e68-150">Visual Studio veya Xamarin Studio'da tooyour Xamarin yapı konağı bir cihaz veya öykünücü hedefleme hello istemci projesi çalıştırma Mac, bağlı.</span><span class="sxs-lookup"><span data-stu-id="c4e68-150">In Visual Studio or Xamarin Studio connected tooyour Xamarin Build Host on your Mac, run hello client project targeting a device or emulator.</span></span> <span data-ttu-id="c4e68-151">Hiçbir veri bu hello uygulama görüntüler doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c4e68-151">Verify that hello app displays no data.</span></span>
   
    <span data-ttu-id="c4e68-152">Merhaba yenileme hareketi hello oturum açma ekranı tooappear neden olacak öğeleri hello listede aşağı çekerek gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="c4e68-152">Perform hello refresh gesture by pulling down hello list of items, which will cause hello login screen tooappear.</span></span> <span data-ttu-id="c4e68-153">Geçerli kimlik bilgileri başarıyla girdikten sonra hello uygulama Yapılacaklar öğelerini hello listesini görüntüler ve güncelleştirmeler toohello veri yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4e68-153">Once you have successfully entered valid credentials, hello app will display hello list of todo items, and you can make updates toohello data.</span></span>

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[bir Xamarin.iOS uygulaması oluşturma]: app-service-mobile-xamarin-ios-get-started.md