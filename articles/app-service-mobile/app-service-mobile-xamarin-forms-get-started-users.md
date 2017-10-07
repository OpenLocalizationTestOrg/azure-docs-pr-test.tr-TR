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
# <a name="add-authentication-tooyour-xamarin-forms-app"></a><span data-ttu-id="878bd-103">Kimlik doğrulama tooyour Xamarin Forms uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="878bd-103">Add authentication tooyour Xamarin Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a><span data-ttu-id="878bd-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="878bd-104">Overview</span></span>
<span data-ttu-id="878bd-105">Bu konu, nasıl gösterir bir mobil uygulama hizmeti, istemci uygulamasından tooauthenticate kullanıcıları.</span><span class="sxs-lookup"><span data-stu-id="878bd-105">This topic shows you how tooauthenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="878bd-106">Bu öğretici kapsamında, kimlik doğrulama App Service tarafından desteklenen bir kimlik sağlayıcısı kullanarak hello Xamarin Forms hızlı başlangıç projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="878bd-106">In this tutorial, you add authentication to hello Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="878bd-107">Mobil uygulamanız tarafından yetkili başarılı bir şekilde kimliği doğrulanmış ve sonra hello kullanıcı kimliği değeri görüntülenir ve kısıtlı mümkün tooaccess tablo verisi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="878bd-107">After being successfully authenticated and authorized by your Mobile App, hello user ID value is displayed, and you will be able tooaccess restricted table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="878bd-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="878bd-108">Prerequisites</span></span>
<span data-ttu-id="878bd-109">Merhaba en iyi sonuç almak için Bu öğretici ile Merhaba ilk tamamlamak olan öneririz [Xamarin Forms uygulaması oluşturma] [ 1] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="878bd-109">For hello best result with this tutorial, we recommend that you first complete hello [Create a Xamarin Forms app][1] tutorial.</span></span> <span data-ttu-id="878bd-110">Bu öğreticiyi tamamladıktan sonra bir çok platformlu Yapılacaklar listesi uygulamasıyla Xamarin Forms proje sahip olur.</span><span class="sxs-lookup"><span data-stu-id="878bd-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span></span>

<span data-ttu-id="878bd-111">Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, hello kimlik doğrulaması uzantı paketini tooyour projesi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="878bd-111">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="878bd-112">Server uzantısı paketleri hakkında daha fazla bilgi için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş][2].</span><span class="sxs-lookup"><span data-stu-id="878bd-112">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps][2].</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="878bd-113">Kimlik doğrulaması için uygulamanızı kaydetme ve uygulama hizmetlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="878bd-113">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="878bd-114"><a name="redirecturl"></a>Uygulama toohello izin verilen dış yönlendirme URL'lerini ekleme</span><span class="sxs-lookup"><span data-stu-id="878bd-114"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="878bd-115">Uygulamanız için yeni bir URL şemasını tanımlamak güvenli kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="878bd-115">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="878bd-116">Merhaba kimlik doğrulama işlemi tamamlandıktan sonra bu hello authentication sistem tooredirect geri tooyour uygulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="878bd-116">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="878bd-117">Bu öğreticide, kullandığımız hello URL şeması _appname_ boyunca.</span><span class="sxs-lookup"><span data-stu-id="878bd-117">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="878bd-118">Ancak, seçtiğiniz herhangi bir URL şeması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="878bd-118">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="878bd-119">Benzersiz tooyour mobil uygulama olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="878bd-119">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="878bd-120">Merhaba sunucu tarafı tooenable hello yönlendirme:</span><span class="sxs-lookup"><span data-stu-id="878bd-120">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="878bd-121">Hello [Azure portalı]'da, uygulama hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="878bd-121">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="878bd-122">Merhaba tıklatın **kimlik doğrulama / yetkilendirme** menü seçeneği.</span><span class="sxs-lookup"><span data-stu-id="878bd-122">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="878bd-123">Merhaba, **yeniden yönlendirme URL'lere izin**, girin `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="878bd-123">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="878bd-124">Merhaba **url_scheme_of_your_app** bu içinde hello URL şeması mobil uygulamanız için bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="878bd-124">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="878bd-125">Bir protokol (harf kullanın ve yalnızca sayı ve bir harf ile başlar) için normal URL belirtimi izlemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="878bd-125">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="878bd-126">Merhaba çeşitli yerlerde URL şeması ile mobil uygulama kodunuzu tooadjust gerekeceğinden, seçtiğiniz hello dize Not olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="878bd-126">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="878bd-127">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="878bd-127">Click **OK**.</span></span>

5. <span data-ttu-id="878bd-128">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="878bd-128">Click **Save**.</span></span>

## <a name="restrict-permissions-tooauthenticated-users"></a><span data-ttu-id="878bd-129">İzinleri tooauthenticated kullanıcılarını kısıtlayın</span><span class="sxs-lookup"><span data-stu-id="878bd-129">Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-toohello-portable-class-library"></a><span data-ttu-id="878bd-130">Kimlik doğrulama toohello taşınabilir sınıf kitaplığı ekleyin</span><span class="sxs-lookup"><span data-stu-id="878bd-130">Add authentication toohello portable class library</span></span>
<span data-ttu-id="878bd-131">Mobile Apps kullanan hello [LoginAsync] [ 3] genişletme yöntemi hello üzerinde [MobileServiceClient] [ 4] toosign bir kullanıcı için uygulama hizmeti ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="878bd-131">Mobile Apps uses hello [LoginAsync][3] extension method on hello [MobileServiceClient][4] toosign in a user with App Service authentication.</span></span> <span data-ttu-id="878bd-132">Bu örnek hello uygulamada oturum açma hello sağlayıcının arabirimi görüntüler bir sunucu yönetilen kimlik doğrulama akışı kullanır.</span><span class="sxs-lookup"><span data-stu-id="878bd-132">This sample uses a server-managed authentication flow that displays hello provider's sign-in interface in hello app.</span></span> <span data-ttu-id="878bd-133">Daha fazla bilgi için bkz: [kimlik doğrulama sunucusu yönetilen][5].</span><span class="sxs-lookup"><span data-stu-id="878bd-133">For more information, see [Server-managed authentication][5].</span></span> <span data-ttu-id="878bd-134">Üretim uygulamanızda daha iyi bir kullanıcı deneyimi sağlamak için dikkate almanız gereken kullanmayı [istemci yönetilen kimlik doğrulaması][6].</span><span class="sxs-lookup"><span data-stu-id="878bd-134">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span></span>

<span data-ttu-id="878bd-135">Xamarin Forms proje ile tooauthenticate tanımlayan bir **IAuthenticate** hello uygulaması için taşınabilir sınıf kitaplığı hello arabiriminde.</span><span class="sxs-lookup"><span data-stu-id="878bd-135">tooauthenticate with a Xamarin Forms project, define an **IAuthenticate** interface in hello Portable Class Library for hello app.</span></span> <span data-ttu-id="878bd-136">Ardından ekleyin bir **oturum açma** düğmesini toohello kullanıcı arabirimi başlangıç'ı taşınabilir sınıf kitaplığı tanımlanan toostart kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="878bd-136">Then add a **Sign-in** button toohello user interface defined in hello Portable Class Library, which you click toostart authentication.</span></span> <span data-ttu-id="878bd-137">Veriler başarılı kimlik doğrulamasından sonra hello mobil uygulama arka ucundan yüklenir.</span><span class="sxs-lookup"><span data-stu-id="878bd-137">Data is loaded from hello mobile app backend after successful authentication.</span></span>

<span data-ttu-id="878bd-138">Uygulama hello **IAuthenticate** uygulamanız tarafından desteklenen her platform için arabirim.</span><span class="sxs-lookup"><span data-stu-id="878bd-138">Implement hello **IAuthenticate** interface for each platform supported by your app.</span></span>

1. <span data-ttu-id="878bd-139">Visual Studio veya Xamarin Studio'da ile Merhaba projenizden App.cs açın **taşınabilir** taşınabilir sınıf kitaplığı proje olan hello ad sonra hello aşağıdakileri ekleyin `using` deyimi:</span><span class="sxs-lookup"><span data-stu-id="878bd-139">In Visual Studio or Xamarin Studio, open App.cs from hello project with **Portable** in hello name, which is Portable Class Library project, then  add hello following `using` statement:</span></span>

        using System.Threading.Tasks;
2. <span data-ttu-id="878bd-140">App.cs içinde hello aşağıdakileri ekleyin `IAuthenticate` arabirimi tanımından hemen önce hello `App` sınıf tanımının.</span><span class="sxs-lookup"><span data-stu-id="878bd-140">In App.cs, add hello following `IAuthenticate` interface definition immediately before hello `App` class definition.</span></span>

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. <span data-ttu-id="878bd-141">tooinitialize hello arabirimi platforma özgü bir uygulama eklemek statik üyeler toohello aşağıdaki hello **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="878bd-141">tooinitialize hello interface with a platform-specific implementation, add hello following static members toohello **App** class.</span></span>

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. <span data-ttu-id="878bd-142">Merhaba taşınabilir sınıf kitaplığı proje TodoList.xaml açın, hello aşağıdakileri ekleyin **düğmesini** hello öğesinde *buttonsPanel* hello varolan bir düğmeyi sonra Düzen öğesi:</span><span class="sxs-lookup"><span data-stu-id="878bd-142">Open TodoList.xaml from hello Portable Class Library project, add hello following **Button** element in hello *buttonsPanel* layout element, after hello existing button:</span></span>

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    <span data-ttu-id="878bd-143">Bu düğme, mobil uygulama arka ucu ile kimlik doğrulama sunucusu yönetilen tetikler.</span><span class="sxs-lookup"><span data-stu-id="878bd-143">This button triggers server-managed authentication with your mobile app backend.</span></span>
5. <span data-ttu-id="878bd-144">Merhaba taşınabilir sınıf kitaplığı proje TodoList.xaml.cs açın ve ardından alan toohello aşağıdaki hello eklemek `TodoList` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="878bd-144">Open TodoList.xaml.cs from hello Portable Class Library project, then add hello following field toohello `TodoList` class:</span></span>

        // Track whether hello user has authenticated.
        bool authenticated = false;
6. <span data-ttu-id="878bd-145">Hello yerine **OnAppearing** koddan hello yöntemiyle:</span><span class="sxs-lookup"><span data-stu-id="878bd-145">Replace hello **OnAppearing** method with hello following code:</span></span>

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

    <span data-ttu-id="878bd-146">Bu kod, doğrulanan sonra veriler yalnızca hello hizmetinden yenilenir emin olur.</span><span class="sxs-lookup"><span data-stu-id="878bd-146">This code makes sure that data is only refreshed from hello service after you have been authenticated.</span></span>
7. <span data-ttu-id="878bd-147">Hello için işleyici aşağıdaki hello eklemek **tıklama** olay toohello **TodoList** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="878bd-147">Add hello following handler for hello **Clicked** event toohello **TodoList** class:</span></span>

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems tootrue toosynchronize hello data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. <span data-ttu-id="878bd-148">Değişikliklerinizi kaydetmek ve hiçbir hata doğrulama hello taşınabilir sınıf kitaplığı proje derleyin.</span><span class="sxs-lookup"><span data-stu-id="878bd-148">Save your changes and rebuild hello Portable Class Library project verifying no errors.</span></span>

## <a name="add-authentication-toohello-android-app"></a><span data-ttu-id="878bd-149">Kimlik doğrulama toohello Android uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="878bd-149">Add authentication toohello Android app</span></span>
<span data-ttu-id="878bd-150">Bu bölümde gösterilmiştir nasıl tooimplement hello **IAuthenticate** hello Android uygulama projesi arabiriminde.</span><span class="sxs-lookup"><span data-stu-id="878bd-150">This section shows how tooimplement hello **IAuthenticate** interface in hello Android app project.</span></span> <span data-ttu-id="878bd-151">Android cihazları destekleme değil, bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="878bd-151">Skip this section if you are not supporting Android devices.</span></span>

1. <span data-ttu-id="878bd-152">Visual Studio veya Xamarin Studio'da hello sağ **droid** , sonra da proje **başlangıç projesi olarak ayarla**.</span><span class="sxs-lookup"><span data-stu-id="878bd-152">In Visual Studio or Xamarin Studio, right-click hello **droid** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="878bd-153">F5 toostart hello proje hello hata ayıklayıcıda tuşuna basın, sonra uygulama başladıktan sonra durum koduyla işlenmeyen bir özel durum 401 (yetkisiz) tetiklenir doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="878bd-153">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="878bd-154">Merhaba arka uç erişimi yalnızca sınırlı tooauthorized kullanıcılar olduğundan hello 401 kodu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="878bd-154">hello 401 code is produced because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="878bd-155">MainActivity.cs hello Android projeyi açın ve hello aşağıdakileri ekleyin `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="878bd-155">Open MainActivity.cs in hello Android project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="878bd-156">Güncelleştirme hello **MainActivity** sınıfı tooimplement hello **IAuthenticate** arabirimi, aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="878bd-156">Update hello **MainActivity** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. <span data-ttu-id="878bd-157">Güncelleştirme hello **MainActivity** ekleyerek sınıfı bir **MobileServiceUser** alan ve bir **kimlik doğrulama** hello tarafından gerekli yöntemi **IAuthenticate**  arabirimi, aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="878bd-157">Update hello **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

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

    <span data-ttu-id="878bd-158">Facebook dışında bir kimlik sağlayıcısı kullanıyorsanız, için farklı bir değer seçin [MobileServiceAuthenticationProvider][7].</span><span class="sxs-lookup"><span data-stu-id="878bd-158">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span></span>

6. <span data-ttu-id="878bd-159">Kod içinde aşağıdaki hello eklemek <application> AndroidManifest.xml düğümünün:</span><span class="sxs-lookup"><span data-stu-id="878bd-159">Add hello following code inside <application> node of AndroidManifest.xml:</span></span>

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

1. <span data-ttu-id="878bd-160">Aşağıdaki kodu toohello hello eklemek **OnCreate** hello yöntemi **MainActivity** hello çağrısından önce çok sınıf`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="878bd-160">Add hello following code toohello **OnCreate** method of hello **MainActivity** class before hello call too`LoadApplication()`:</span></span>

        // Initialize hello authenticator before loading hello app.
        App.Init((IAuthenticate)this);

    <span data-ttu-id="878bd-161">Bu kod hello Doğrulayıcı hello uygulama yükleri önce başlatılmış sağlar.</span><span class="sxs-lookup"><span data-stu-id="878bd-161">This code ensures hello authenticator is initialized before hello app loads.</span></span>
2. <span data-ttu-id="878bd-162">Merhaba uygulama yeniden, çalıştırın ve sonra seçtiğiniz ve kimliği doğrulanmış bir kullanıcı olarak mümkün tooaccess verileri doğrulayın hello kimlik doğrulama sağlayıcısının oturum açın.</span><span class="sxs-lookup"><span data-stu-id="878bd-162">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="add-authentication-toohello-ios-app"></a><span data-ttu-id="878bd-163">Kimlik doğrulama toohello iOS uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="878bd-163">Add authentication toohello iOS app</span></span>
<span data-ttu-id="878bd-164">Bu bölümde gösterilmiştir nasıl tooimplement hello **IAuthenticate** hello iOS uygulaması projesi arabiriminde.</span><span class="sxs-lookup"><span data-stu-id="878bd-164">This section shows how tooimplement hello **IAuthenticate** interface in hello iOS app project.</span></span> <span data-ttu-id="878bd-165">İOS cihazları destekleme değil, bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="878bd-165">Skip this section if you are not supporting iOS devices.</span></span>

1. <span data-ttu-id="878bd-166">Visual Studio veya Xamarin Studio'da hello sağ **iOS** , sonra da proje **başlangıç projesi olarak ayarla**.</span><span class="sxs-lookup"><span data-stu-id="878bd-166">In Visual Studio or Xamarin Studio, right-click hello **iOS** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="878bd-167">F5 toostart hello proje hello hata ayıklayıcıda tuşuna basın, sonra hello uygulama başladıktan sonra durum koduyla işlenmeyen bir özel durum 401 (yetkisiz) tetiklenir doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="878bd-167">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="878bd-168">Merhaba arka uç erişimi yalnızca sınırlı tooauthorized kullanıcılar olduğundan hello 401 yanıtı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="878bd-168">hello 401 response is produced because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="878bd-169">AppDelegate.cs hello iOS projeyi açın ve hello aşağıdakileri ekleyin `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="878bd-169">Open AppDelegate.cs in hello iOS project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="878bd-170">Güncelleştirme hello **AppDelegate** sınıfı tooimplement hello **IAuthenticate** arabirimi, aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="878bd-170">Update hello **AppDelegate** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. <span data-ttu-id="878bd-171">Güncelleştirme hello **AppDelegate** ekleyerek sınıfı bir **MobileServiceUser** alan ve bir **kimlik doğrulama** hello tarafından gerekli yöntemi **IAuthenticate**  arabirimi, aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="878bd-171">Update hello **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

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

    <span data-ttu-id="878bd-172">Facebook dışında bir kimlik sağlayıcısı kullanıyorsanız, [MobileServiceAuthenticationProvider] için farklı bir değer seçin.</span><span class="sxs-lookup"><span data-stu-id="878bd-172">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

6. <span data-ttu-id="878bd-173">OpenUrl (Uıapplication uygulama, NSUrl url NSDictionary seçenekleri) yöntemi aşırı yüklemesini ekleyerek Hello AppDelegate sınıfını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="878bd-173">Update hello AppDelegate class by adding OpenUrl(UIApplication app, NSUrl url, NSDictionary options) method overload</span></span>

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. <span data-ttu-id="878bd-174">Kod toohello satırının aşağıdaki hello eklemek **FinishedLaunching** hello önce yöntemini çağırın çok`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="878bd-174">Add hello following line of code toohello **FinishedLaunching** method before hello call too`LoadApplication()`:</span></span>

        App.Init(this);

    <span data-ttu-id="878bd-175">Bu kod hello Doğrulayıcı hello uygulama yüklenmeden önce başlatılmış sağlar.</span><span class="sxs-lookup"><span data-stu-id="878bd-175">This code ensures hello authenticator is initialized before hello app is loaded.</span></span>

6. <span data-ttu-id="878bd-176">Ekleme **{url_scheme_of_your_app}** Info.plist tooURL düzenleri.</span><span class="sxs-lookup"><span data-stu-id="878bd-176">Add **{url_scheme_of_your_app}** tooURL Schemes in Info.plist.</span></span>

7. <span data-ttu-id="878bd-177">Merhaba uygulama yeniden, çalıştırın ve sonra seçtiğiniz ve kimliği doğrulanmış bir kullanıcı olarak mümkün tooaccess verileri doğrulayın hello kimlik doğrulama sağlayıcısının oturum açın.</span><span class="sxs-lookup"><span data-stu-id="878bd-177">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="add-authentication-toowindows-10-including-phone-app-projects"></a><span data-ttu-id="878bd-178">Kimlik doğrulama tooWindows 10 (dahil olmak üzere telefon) eklemek uygulaması projeleri</span><span class="sxs-lookup"><span data-stu-id="878bd-178">Add authentication tooWindows 10 (including Phone) app projects</span></span>
<span data-ttu-id="878bd-179">Bu bölümde gösterilmiştir nasıl tooimplement hello **IAuthenticate** hello Windows 10 uygulaması projeleri arabiriminde.</span><span class="sxs-lookup"><span data-stu-id="878bd-179">This section shows how tooimplement hello **IAuthenticate** interface in hello Windows 10 app projects.</span></span> <span data-ttu-id="878bd-180">Evrensel Windows Platformu (UWP) projeleri, ancak hello kullanarak için aynı adımları uygulamak hello **UWP** projeyle (not ettiğiniz değişir).</span><span class="sxs-lookup"><span data-stu-id="878bd-180">hello same steps apply for Universal Windows Platform (UWP) projects, but using hello **UWP** project (with noted changes).</span></span> <span data-ttu-id="878bd-181">Windows cihazları destekleme değil, bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="878bd-181">Skip this section if you are not supporting Windows devices.</span></span>

1. <span data-ttu-id="878bd-182">"Visual Studio'da ya da hello sağ **UWP** , sonra da proje **başlangıç projesi olarak ayarla**.</span><span class="sxs-lookup"><span data-stu-id="878bd-182">"In Visual Studio, right-click either hello **UWP** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="878bd-183">F5 toostart hello proje hello hata ayıklayıcıda tuşuna basın, sonra hello uygulama başladıktan sonra durum koduyla işlenmeyen bir özel durum 401 (yetkisiz) tetiklenir doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="878bd-183">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="878bd-184">Merhaba arka uç erişimi yalnızca sınırlı tooauthorized kullanıcılar olduğundan hello 401 yanıt olur.</span><span class="sxs-lookup"><span data-stu-id="878bd-184">hello 401 response happens because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="878bd-185">MainPage.xaml.cs hello Windows uygulama projesi için açın ve hello aşağıdakileri ekleyin `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="878bd-185">Open MainPage.xaml.cs for hello Windows app project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    <span data-ttu-id="878bd-186">Değiştir `<your_Portable_Class_Library_namespace>` ile taşınabilir sınıf kitaplığı için hello ad alanı.</span><span class="sxs-lookup"><span data-stu-id="878bd-186">Replace `<your_Portable_Class_Library_namespace>` with hello namespace for your portable class library.</span></span>
4. <span data-ttu-id="878bd-187">Güncelleştirme hello **MainPage** sınıfı tooimplement hello **IAuthenticate** arabirimi, aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="878bd-187">Update hello **MainPage** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public sealed partial class MainPage : IAuthenticate
5. <span data-ttu-id="878bd-188">Güncelleştirme hello **MainPage** ekleyerek sınıfı bir **MobileServiceUser** alan ve bir **kimlik doğrulama** hello tarafından gerekli yöntemi **IAuthenticate** arabirimi, aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="878bd-188">Update hello **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

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

    <span data-ttu-id="878bd-189">Facebook dışında bir kimlik sağlayıcısı kullanıyorsanız, [MobileServiceAuthenticationProvider] için farklı bir değer seçin.</span><span class="sxs-lookup"><span data-stu-id="878bd-189">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

1. <span data-ttu-id="878bd-190">Aşağıdaki kod hello hello oluşturucuda hello eklemek **MainPage** hello çağrısından önce çok sınıf`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="878bd-190">Add hello following line of code in hello constructor for hello **MainPage** class before hello call too`LoadApplication()`:</span></span>

        // Initialize hello authenticator before loading hello app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    <span data-ttu-id="878bd-191">Değiştir `<your_Portable_Class_Library_namespace>` ile taşınabilir sınıf kitaplığı için hello ad alanı.</span><span class="sxs-lookup"><span data-stu-id="878bd-191">Replace `<your_Portable_Class_Library_namespace>` with hello namespace for your portable class library.</span></span>

3. <span data-ttu-id="878bd-192">Kullanıyorsanız **UWP**, hello aşağıdakileri ekleyin **OnActivated** yöntemini geçersiz kılın toohello **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="878bd-192">If you are using **UWP**, add hello following **OnActivated** method override toohello **App** class:</span></span>

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   <span data-ttu-id="878bd-193">Merhaba yöntemi geçersiz kılma zaten mevcut olduğunda hello koşullu kod parçacığını önceki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="878bd-193">When hello method override already exists, add hello conditional code from hello preceding snippet.</span></span>  <span data-ttu-id="878bd-194">Bu kod, Evrensel Windows projeleri için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="878bd-194">This code is not required for Universal Windows projects.</span></span>

3. <span data-ttu-id="878bd-195">Ekleme **{url_scheme_of_your_app}** Package.appxmanifest içinde.</span><span class="sxs-lookup"><span data-stu-id="878bd-195">Add **{url_scheme_of_your_app}** in Package.appxmanifest.</span></span> 

4. <span data-ttu-id="878bd-196">Merhaba uygulama yeniden, çalıştırın ve sonra seçtiğiniz ve kimliği doğrulanmış bir kullanıcı olarak mümkün tooaccess verileri doğrulayın hello kimlik doğrulama sağlayıcısının oturum açın.</span><span class="sxs-lookup"><span data-stu-id="878bd-196">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="878bd-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="878bd-197">Next steps</span></span>
<span data-ttu-id="878bd-198">Bu temel kimlik doğrulaması öğreticisini tamamladığınıza göre öğreticileri aşağıdaki hello tooone üzerinde etmeden göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="878bd-198">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="878bd-199">Anında iletme bildirimleri tooyour uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="878bd-199">Add push notifications tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)

  <span data-ttu-id="878bd-200">Mobil uygulama arka uç toouse Azure Notification Hubs toosend anında iletme bildirimleri yapılandırmak ve tooadd anında iletme bildirimleri tooyour uygulama'ı nasıl desteklediğini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="878bd-200">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="878bd-201">Uygulamanız için çevrimdışı eşitlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="878bd-201">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  <span data-ttu-id="878bd-202">Bir mobil uygulama arka ucu kullanarak uygulamanıza çevrimdışı tooadd destek nasıl bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="878bd-202">Learn how tooadd offline support your app using a Mobile App backend.</span></span> <span data-ttu-id="878bd-203">Çevrimdışı eşitleme son kullanıcıların toointeract ile mobil uygulama görüntüleme, ekleme veya ağ bağlantısı olduğunda bile veri - değiştirme - sağlar.</span><span class="sxs-lookup"><span data-stu-id="878bd-203">Offline sync allows end users toointeract with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
