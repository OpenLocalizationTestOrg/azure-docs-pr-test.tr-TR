---
title: "Xamarin iOS mobil uygulamalar için kimlik doğrulaması kullanmaya başlama"
description: "Xamarin iOS uygulamanızın kimlik sağlayıcıları, AAD, Google, Facebook, Twitter ve Microsoft dahil olmak üzere çeşitli kullanıcıların kimliklerini doğrulamak için Mobile Apps kullanmayı öğrenin."
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
ms.openlocfilehash: 454b2df5a9bf8cfba93befea54370957ab044d95
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-xamarinios-app"></a><span data-ttu-id="64eed-103">Xamarin.iOS uygulamanıza kimlik doğrulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="64eed-103">Add authentication to your Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="64eed-104">Bu konuda bir mobil uygulama hizmeti istemci uygulamanızdan kullanıcıların kimliklerini gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="64eed-104">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="64eed-105">Bu öğretici kapsamında, kimlik doğrulama App Service tarafından desteklenen bir kimlik sağlayıcısı kullanarak Xamarin.iOS hızlı başlangıç projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="64eed-105">In this tutorial, you add authentication to the Xamarin.iOS quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="64eed-106">Mobil uygulamanız tarafından yetkili başarılı bir şekilde kimliği doğrulanmış ve sonra kullanıcı kimliği değeri görüntülenir ve kısıtlı tablo veri erişimi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="64eed-106">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed and you will be able to access restricted table data.</span></span>

<span data-ttu-id="64eed-107">Öğreticiyi tamamlamak [bir Xamarin.iOS uygulaması oluşturma].</span><span class="sxs-lookup"><span data-stu-id="64eed-107">You must first complete the tutorial [Create a Xamarin.iOS app].</span></span> <span data-ttu-id="64eed-108">İndirilen hızlı başlangıç sunucu projesi kullanmazsanız, kimlik doğrulaması uzantısı paketini projenize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="64eed-108">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="64eed-109">Server uzantısı paketleri hakkında daha fazla bilgi için bkz: [.NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="64eed-109">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="64eed-110">Kimlik doğrulaması için uygulamanızı kaydetme ve uygulama hizmetlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="64eed-110">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-to-the-allowed-external-redirect-urls"></a><span data-ttu-id="64eed-111">Uygulamanız için izin verilen dış yönlendirme URL'leri ekleme</span><span class="sxs-lookup"><span data-stu-id="64eed-111">Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="64eed-112">Uygulamanız için yeni bir URL şemasını tanımlamak güvenli kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="64eed-112">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="64eed-113">Bu kimlik doğrulama işlemi tamamlandıktan sonra uygulamanıza geri yönlendirmek bir kimlik doğrulama sistemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="64eed-113">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="64eed-114">Bu öğreticide, URL şemasının kullanırız _appname_ boyunca.</span><span class="sxs-lookup"><span data-stu-id="64eed-114">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="64eed-115">Ancak, seçtiğiniz herhangi bir URL şeması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64eed-115">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="64eed-116">Mobil uygulamanız için benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="64eed-116">It should be unique to your mobile application.</span></span> <span data-ttu-id="64eed-117">Sunucu tarafında yeniden yönlendirmeyi etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="64eed-117">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="64eed-118">[Azure portalında] uygulama hizmetinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="64eed-118">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="64eed-119">Tıklatın **kimlik doğrulama / yetkilendirme** menü seçeneği.</span><span class="sxs-lookup"><span data-stu-id="64eed-119">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="64eed-120">İçinde **yeniden yönlendirme URL'lere izin**, girin `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="64eed-120">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="64eed-121">**Url_scheme_of_your_app** Bu dize, mobil uygulamanız için URL düzenidir.</span><span class="sxs-lookup"><span data-stu-id="64eed-121">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="64eed-122">Bir protokol (harf kullanın ve yalnızca sayı ve bir harf ile başlar) için normal URL belirtimi izlemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="64eed-122">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="64eed-123">Çeşitli yerlerde URL şeması ile mobil uygulama kodunuzu ayarlamak ihtiyaç duyacağınız seçtiğiniz dizeyi Not olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="64eed-123">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="64eed-124">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="64eed-124">Click **OK**.</span></span>

5. <span data-ttu-id="64eed-125">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="64eed-125">Click **Save**.</span></span>

## <a name="restrict-permissions-to-authenticated-users"></a><span data-ttu-id="64eed-126">Kimliği doğrulanmış kullanıcılar için izinleri kısıtla</span><span class="sxs-lookup"><span data-stu-id="64eed-126">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="64eed-127">&nbsp;&nbsp;4.</span><span class="sxs-lookup"><span data-stu-id="64eed-127">&nbsp;&nbsp;4.</span></span> <span data-ttu-id="64eed-128">Visual Studio veya Xamarin Studio'da istemci projesi bir cihaz veya öykünücü çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="64eed-128">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span></span> <span data-ttu-id="64eed-129">Uygulama başlatıldıktan sonra bir durum koduyla işlenmeyen bir özel durum 401 (yetkisiz) tetiklenir doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="64eed-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="64eed-130">Hata ayıklayıcı konsola hata günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="64eed-130">The failure is logged to the console of the debugger.</span></span> <span data-ttu-id="64eed-131">Bu nedenle Visual Studio'da hata çıktı penceresinde görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="64eed-131">So in Visual Studio, you should see the failure in the output window.</span></span>

<span data-ttu-id="64eed-132">&nbsp;&nbsp;Uygulama Kimliği doğrulanmamış bir kullanıcı olarak, mobil uygulamanızın arka ucuna erişmeye çünkü bu yetkisiz hatası gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="64eed-132">&nbsp;&nbsp;This unauthorized failure happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="64eed-133">*Todoıtem* tablo artık kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="64eed-133">The *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="64eed-134">Ardından, istemci uygulaması isteği kaynaklarına mobil uygulama arka ucundan kimliği doğrulanmış bir kullanıcı ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="64eed-134">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication-to-the-app"></a><span data-ttu-id="64eed-135">Kimlik doğrulaması için uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="64eed-135">Add authentication to the app</span></span>
<span data-ttu-id="64eed-136">Bu bölümde, uygulama veri görüntülenmeden önce bir oturum açma ekranı değiştirecektir.</span><span class="sxs-lookup"><span data-stu-id="64eed-136">In this section, you will modify the app to display a login screen before displaying data.</span></span> <span data-ttu-id="64eed-137">Uygulama başlatıldığında değil, App Service'e bağlanmaz ve herhangi bir veri görüntülenmez.</span><span class="sxs-lookup"><span data-stu-id="64eed-137">When the app starts, it will not not connect to your App Service and will not display any data.</span></span> <span data-ttu-id="64eed-138">İlk kez sonra kullanıcı oturum açma ekranı görünür yenileme hareketi gerçekleştirir; başarılı oturum açma işleminden sonra Yapılacaklar öğelerini listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="64eed-138">After the first time that the user performs the refresh gesture, the login screen will appear; after successful login the list of todo items will be displayed.</span></span>

1. <span data-ttu-id="64eed-139">İstemci proje dosyasını açın **QSTodoService.cs** ve aşağıdakileri ekleyin deyimiyle ve `MobileServiceUser` QSTodoService sınıfına erişimcisi ile:</span><span class="sxs-lookup"><span data-stu-id="64eed-139">In the client project, open the file **QSTodoService.cs** and add the following using statement and `MobileServiceUser` with accessor to the QSTodoService class:</span></span>
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. <span data-ttu-id="64eed-140">Adlı yeni bir yöntem ekleyin **kimlik doğrulama** için **QSTodoService** aşağıdaki tanımıyla:</span><span class="sxs-lookup"><span data-stu-id="64eed-140">Add new method named **Authenticate** to **QSTodoService** with the following definition:</span></span>

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

    >[AZURE.NOTE] <span data-ttu-id="64eed-141">Bir Facebook dışında bir kimlik sağlayıcısı kullanıyorsanız, geçirilen değerini değiştirmek **LoginAsync** yukarıda aşağıdakilerden birine: _MicrosoftAccount_, _Twitter_,  _Google_, veya _WindowsAzureActiveDirectory_.</span><span class="sxs-lookup"><span data-stu-id="64eed-141">If you are using an identity provider other than a Facebook, change the value passed to **LoginAsync** above to one of the following: _MicrosoftAccount_, _Twitter_, _Google_, or _WindowsAzureActiveDirectory_.</span></span>

3. <span data-ttu-id="64eed-142">Açık **QSTodoListViewController.cs**.</span><span class="sxs-lookup"><span data-stu-id="64eed-142">Open **QSTodoListViewController.cs**.</span></span> <span data-ttu-id="64eed-143">Yöntem tanımını değiştirme **ViewDidLoad** çağrısı kaldırma **RefreshAsync()** yakınında bitiş:</span><span class="sxs-lookup"><span data-stu-id="64eed-143">Modify the method definition of **ViewDidLoad** removing the call to **RefreshAsync()** near the end:</span></span>
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out the call to RefreshAsync
            // await RefreshAsync();
        }
4. <span data-ttu-id="64eed-144">Yöntemi Değiştir **RefreshAsync** , kimlik doğrulaması için **kullanıcı** özelliği null.</span><span class="sxs-lookup"><span data-stu-id="64eed-144">Modify the method **RefreshAsync** to authenticate if the **User** property is null.</span></span> <span data-ttu-id="64eed-145">Yöntem tanımı üstünde aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="64eed-145">Add the following code at the top of the method definition:</span></span>
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. <span data-ttu-id="64eed-146">Açık **AppDelegate.cs**, aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="64eed-146">Open **AppDelegate.cs**, add the following method:</span></span>

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. <span data-ttu-id="64eed-147">Açık **Info.plist** dosya, gitmek **URL türleri** içinde **Gelişmiş** bölümü.</span><span class="sxs-lookup"><span data-stu-id="64eed-147">Open **Info.plist** file, navigate to **URL Types** in the **Advanced** section.</span></span> <span data-ttu-id="64eed-148">Şimdi yapılandırmak **tanımlayıcısı** ve **URL şemalarını** URL türü ve tıklatın **URL türü Ekle**.</span><span class="sxs-lookup"><span data-stu-id="64eed-148">Now configure the **Identifier** and the **URL Schemes** of your URL Type and click **Add URL Type**.</span></span> <span data-ttu-id="64eed-149">**URL şemalarını** , {url_scheme_of_your_app} aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="64eed-149">**URL Schemes** should be the same as your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="64eed-150">Visual Studio veya Xamarin Studio'da, Xamarin derleme konaktaki bir cihaz veya öykünücü hedefleme istemci projesi çalıştırma Mac'iniz bağlı.</span><span class="sxs-lookup"><span data-stu-id="64eed-150">In Visual Studio or Xamarin Studio connected to your Xamarin Build Host on your Mac, run the client project targeting a device or emulator.</span></span> <span data-ttu-id="64eed-151">Uygulama veri görüntülendiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="64eed-151">Verify that the app displays no data.</span></span>
   
    <span data-ttu-id="64eed-152">Görüntülenecek oturum açma ekranı neden olacak öğeleri listede aşağı çekerek yenileme hareketi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="64eed-152">Perform the refresh gesture by pulling down the list of items, which will cause the login screen to appear.</span></span> <span data-ttu-id="64eed-153">Geçerli kimlik bilgileri başarıyla girdikten sonra uygulama Yapılacaklar öğelerini listesi görüntülenir ve veri güncelleştirmeleri yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64eed-153">Once you have successfully entered valid credentials, the app will display the list of todo items, and you can make updates to the data.</span></span>

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
<span data-ttu-id="64eed-154">[bir Xamarin.iOS uygulaması oluşturma]: app-service-mobile-xamarin-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="64eed-154">[Create a Xamarin.iOS app]: app-service-mobile-xamarin-ios-get-started.md</span></span>