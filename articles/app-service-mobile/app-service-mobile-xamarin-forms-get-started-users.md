---
title: "Mobil uygulamaları için Xamarin Forms uygulamasında kimlik doğrulamasını kullanmaya başlama | Microsoft Docs"
description: "Mobile Apps kimlik sağlayıcıları, AAD, Google, Facebook, Twitter ve Microsoft dahil olmak üzere çeşitli Xamarin Forms uygulamanızdaki kullanıcıların kimliklerini doğrulamak için nasıl kullanılacağını öğrenin."
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
ms.openlocfilehash: 9e14e95793bcc81ad46783fd50ba223eec4ea360
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="add-authentication-to-your-xamarin-forms-app"></a><span data-ttu-id="4f22f-103">Xamarin Forms kimlik doğrulaması ekleme</span><span class="sxs-lookup"><span data-stu-id="4f22f-103">Add authentication to your Xamarin Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a><span data-ttu-id="4f22f-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="4f22f-104">Overview</span></span>
<span data-ttu-id="4f22f-105">Bu konuda bir mobil uygulama hizmeti istemci uygulamanızdan kullanıcıların kimliklerini gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4f22f-105">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="4f22f-106">Bu öğretici kapsamında, kimlik doğrulama App Service tarafından desteklenen bir kimlik sağlayıcısı kullanarak Xamarin Forms hızlı başlangıç projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4f22f-106">In this tutorial, you add authentication to the Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="4f22f-107">Mobil uygulamanız tarafından yetkili başarılı bir şekilde kimliği doğrulanmış ve sonra kullanıcı kimliği değeri görüntülenir ve kısıtlı tablo veri erişimi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4f22f-107">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed, and you will be able to access restricted table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f22f-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4f22f-108">Prerequisites</span></span>
<span data-ttu-id="4f22f-109">Bu öğretici ile en iyi sonuç için önce tamamlamanızı öneririz [Xamarin Forms uygulaması oluşturma] [ 1] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="4f22f-109">For the best result with this tutorial, we recommend that you first complete the [Create a Xamarin Forms app][1] tutorial.</span></span> <span data-ttu-id="4f22f-110">Bu öğreticiyi tamamladıktan sonra bir çok platformlu Yapılacaklar listesi uygulamasıyla Xamarin Forms proje sahip olur.</span><span class="sxs-lookup"><span data-stu-id="4f22f-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span></span>

<span data-ttu-id="4f22f-111">İndirilen hızlı başlangıç sunucu projesi kullanmazsanız, kimlik doğrulaması uzantısı paketini projenize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f22f-111">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="4f22f-112">Server uzantısı paketleri hakkında daha fazla bilgi için bkz: [.NET arka uç sunucusu SDK ile Azure Mobile Apps için iş][2].</span><span class="sxs-lookup"><span data-stu-id="4f22f-112">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps][2].</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="4f22f-113">Kimlik doğrulaması için uygulamanızı kaydetme ve uygulama hizmetlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4f22f-113">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="4f22f-114"><a name="redirecturl"></a>Uygulamanız için izin verilen dış yönlendirme URL'leri ekleme</span><span class="sxs-lookup"><span data-stu-id="4f22f-114"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="4f22f-115">Uygulamanız için yeni bir URL şemasını tanımlamak güvenli kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4f22f-115">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="4f22f-116">Bu kimlik doğrulama işlemi tamamlandıktan sonra uygulamanıza geri yönlendirmek bir kimlik doğrulama sistemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="4f22f-116">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="4f22f-117">Bu öğreticide, URL şemasının kullanırız _appname_ boyunca.</span><span class="sxs-lookup"><span data-stu-id="4f22f-117">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="4f22f-118">Ancak, seçtiğiniz herhangi bir URL şeması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f22f-118">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="4f22f-119">Mobil uygulamanız için benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4f22f-119">It should be unique to your mobile application.</span></span> <span data-ttu-id="4f22f-120">Sunucu tarafında yeniden yönlendirmeyi etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="4f22f-120">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="4f22f-121">[Azure portalında] uygulama hizmetinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="4f22f-121">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="4f22f-122">Tıklatın **kimlik doğrulama / yetkilendirme** menü seçeneği.</span><span class="sxs-lookup"><span data-stu-id="4f22f-122">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="4f22f-123">İçinde **yeniden yönlendirme URL'lere izin**, girin `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="4f22f-123">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="4f22f-124">**Url_scheme_of_your_app** Bu dize, mobil uygulamanız için URL düzenidir.</span><span class="sxs-lookup"><span data-stu-id="4f22f-124">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="4f22f-125">Bir protokol (harf kullanın ve yalnızca sayı ve bir harf ile başlar) için normal URL belirtimi izlemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="4f22f-125">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="4f22f-126">Çeşitli yerlerde URL şeması ile mobil uygulama kodunuzu ayarlamak ihtiyaç duyacağınız seçtiğiniz dizeyi Not olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f22f-126">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="4f22f-127">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4f22f-127">Click **OK**.</span></span>

5. <span data-ttu-id="4f22f-128">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4f22f-128">Click **Save**.</span></span>

## <a name="restrict-permissions-to-authenticated-users"></a><span data-ttu-id="4f22f-129">Kimliği doğrulanmış kullanıcılar için izinleri kısıtla</span><span class="sxs-lookup"><span data-stu-id="4f22f-129">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-to-the-portable-class-library"></a><span data-ttu-id="4f22f-130">Taşınabilir Sınıf Kitaplığı'na kimlik doğrulaması ekleme</span><span class="sxs-lookup"><span data-stu-id="4f22f-130">Add authentication to the portable class library</span></span>
<span data-ttu-id="4f22f-131">Mobile Apps kullanan [LoginAsync] [ 3] genişletme yöntemi [MobileServiceClient] [ 4] uygulama hizmeti ile bir kullanıcıyla oturum açmak için kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="4f22f-131">Mobile Apps uses the [LoginAsync][3] extension method on the [MobileServiceClient][4] to sign in a user with App Service authentication.</span></span> <span data-ttu-id="4f22f-132">Bu örnek uygulamada oturum açma sağlayıcısı'nın arabirimi görüntüleyen bir sunucu yönetilen kimlik doğrulama akışı kullanır.</span><span class="sxs-lookup"><span data-stu-id="4f22f-132">This sample uses a server-managed authentication flow that displays the provider's sign-in interface in the app.</span></span> <span data-ttu-id="4f22f-133">Daha fazla bilgi için bkz: [kimlik doğrulama sunucusu yönetilen][5].</span><span class="sxs-lookup"><span data-stu-id="4f22f-133">For more information, see [Server-managed authentication][5].</span></span> <span data-ttu-id="4f22f-134">Üretim uygulamanızda daha iyi bir kullanıcı deneyimi sağlamak için dikkate almanız gereken kullanmayı [istemci yönetilen kimlik doğrulaması][6].</span><span class="sxs-lookup"><span data-stu-id="4f22f-134">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span></span>

<span data-ttu-id="4f22f-135">Xamarin Forms projesi ile kimlik doğrulaması için tanımlama bir **IAuthenticate** uygulama için taşınabilir Sınıf Kitaplığı'nda arabirimi.</span><span class="sxs-lookup"><span data-stu-id="4f22f-135">To authenticate with a Xamarin Forms project, define an **IAuthenticate** interface in the Portable Class Library for the app.</span></span> <span data-ttu-id="4f22f-136">Ardından ekleyin bir **oturum açma** taşınabilir sınıf hangi kimlik doğrulama başlatmak için tıklatın Kitaplığı'nda tanımlanan kullanıcı arabirimi düğme.</span><span class="sxs-lookup"><span data-stu-id="4f22f-136">Then add a **Sign-in** button to the user interface defined in the Portable Class Library, which you click to start authentication.</span></span> <span data-ttu-id="4f22f-137">Veriler mobil uygulama arka ucundan başarılı kimlik doğrulamasından sonra yüklenir.</span><span class="sxs-lookup"><span data-stu-id="4f22f-137">Data is loaded from the mobile app backend after successful authentication.</span></span>

<span data-ttu-id="4f22f-138">Uygulama **IAuthenticate** uygulamanız tarafından desteklenen her platform için arabirim.</span><span class="sxs-lookup"><span data-stu-id="4f22f-138">Implement the **IAuthenticate** interface for each platform supported by your app.</span></span>

1. <span data-ttu-id="4f22f-139">Visual Studio veya Xamarin Studio'da ile projenizden App.cs açın **taşınabilir** taşınabilir sınıf kitaplığı proje olan adlarında sonra aşağıdakileri ekleyin `using` deyimi:</span><span class="sxs-lookup"><span data-stu-id="4f22f-139">In Visual Studio or Xamarin Studio, open App.cs from the project with **Portable** in the name, which is Portable Class Library project, then  add the following `using` statement:</span></span>

        using System.Threading.Tasks;
2. <span data-ttu-id="4f22f-140">App.cs içinde aşağıdaki ekleme `IAuthenticate` tanımı hemen önce arabirim `App` sınıf tanımının.</span><span class="sxs-lookup"><span data-stu-id="4f22f-140">In App.cs, add the following `IAuthenticate` interface definition immediately before the `App` class definition.</span></span>

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. <span data-ttu-id="4f22f-141">Platforma özgü bir uygulama arabirimi başlatmak için aşağıdaki statik üyeleri Ekle **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="4f22f-141">To initialize the interface with a platform-specific implementation, add the following static members to the **App** class.</span></span>

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. <span data-ttu-id="4f22f-142">Taşınabilir sınıf kitaplığı projesinden TodoList.xaml açın, aşağıdakileri ekleyin **düğmesini** öğesinde *buttonsPanel* varolan bir düğmeyi sonra Düzen öğesi:</span><span class="sxs-lookup"><span data-stu-id="4f22f-142">Open TodoList.xaml from the Portable Class Library project, add the following **Button** element in the *buttonsPanel* layout element, after the existing button:</span></span>

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    <span data-ttu-id="4f22f-143">Bu düğme, mobil uygulama arka ucu ile kimlik doğrulama sunucusu yönetilen tetikler.</span><span class="sxs-lookup"><span data-stu-id="4f22f-143">This button triggers server-managed authentication with your mobile app backend.</span></span>
5. <span data-ttu-id="4f22f-144">Taşınabilir sınıf kitaplığı projesinden TodoList.xaml.cs açın, ardından aşağıdaki alana ekleyin `TodoList` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="4f22f-144">Open TodoList.xaml.cs from the Portable Class Library project, then add the following field to the `TodoList` class:</span></span>

        // Track whether the user has authenticated.
        bool authenticated = false;
6. <span data-ttu-id="4f22f-145">Değiştir **OnAppearing** aşağıdaki kod ile yöntemi:</span><span class="sxs-lookup"><span data-stu-id="4f22f-145">Replace the **OnAppearing** method with the following code:</span></span>

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems to true in order to synchronize the data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide the Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    <span data-ttu-id="4f22f-146">Bu kod, doğrulanan sonra veriler yalnızca hizmetinden yenilenir emin olur.</span><span class="sxs-lookup"><span data-stu-id="4f22f-146">This code makes sure that data is only refreshed from the service after you have been authenticated.</span></span>
7. <span data-ttu-id="4f22f-147">Aşağıdaki işleyicisi ekleme **tıklama** olaya **TodoList** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="4f22f-147">Add the following handler for the **Clicked** event to the **TodoList** class:</span></span>

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems to true to synchronize the data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. <span data-ttu-id="4f22f-148">Değişikliklerinizi kaydetmek ve hiçbir hata doğrulama taşınabilir sınıf kitaplığı proje derleyin.</span><span class="sxs-lookup"><span data-stu-id="4f22f-148">Save your changes and rebuild the Portable Class Library project verifying no errors.</span></span>

## <a name="add-authentication-to-the-android-app"></a><span data-ttu-id="4f22f-149">Android uygulaması için kimlik doğrulaması ekleme</span><span class="sxs-lookup"><span data-stu-id="4f22f-149">Add authentication to the Android app</span></span>
<span data-ttu-id="4f22f-150">Bu bölümde nasıl uygulandığını gösterir **IAuthenticate** Android uygulama projesi arabiriminde.</span><span class="sxs-lookup"><span data-stu-id="4f22f-150">This section shows how to implement the **IAuthenticate** interface in the Android app project.</span></span> <span data-ttu-id="4f22f-151">Android cihazları destekleme değil, bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f22f-151">Skip this section if you are not supporting Android devices.</span></span>

1. <span data-ttu-id="4f22f-152">Visual Studio veya Xamarin Studio'da sağ **droid** , sonra da proje **başlangıç projesi olarak ayarla**.</span><span class="sxs-lookup"><span data-stu-id="4f22f-152">In Visual Studio or Xamarin Studio, right-click the **droid** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="4f22f-153">Projeyi Hata Ayıklayıcısı'ndaki başlayın, ardından uygulama başladıktan sonra durum koduyla işlenmeyen bir özel durum 401 (yetkisiz) tetiklenir doğrulamak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="4f22f-153">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="4f22f-154">Arka uç erişimi yalnızca yetkili kullanıcılar ile sınırlı olduğundan 401 kodu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4f22f-154">The 401 code is produced because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="4f22f-155">MainActivity.cs Android projeyi açın ve aşağıdakileri ekleyin `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="4f22f-155">Open MainActivity.cs in the Android project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="4f22f-156">Güncelleştirme **MainActivity** uygulamak için sınıf **IAuthenticate** arabirimi, aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="4f22f-156">Update the **MainActivity** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. <span data-ttu-id="4f22f-157">Güncelleştirme **MainActivity** ekleyerek sınıfı bir **MobileServiceUser** alan ve bir **kimlik doğrulama** gerekli yöntemi **IAuthenticate** arabirimi, aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="4f22f-157">Update the **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

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

            // Display the success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    <span data-ttu-id="4f22f-158">Facebook dışında bir kimlik sağlayıcısı kullanıyorsanız, için farklı bir değer seçin [MobileServiceAuthenticationProvider][7].</span><span class="sxs-lookup"><span data-stu-id="4f22f-158">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span></span>

6. <span data-ttu-id="4f22f-159">Aşağıdaki kodu ekleyin <application> AndroidManifest.xml düğümünün:</span><span class="sxs-lookup"><span data-stu-id="4f22f-159">Add the following code inside <application> node of AndroidManifest.xml:</span></span>

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

1. <span data-ttu-id="4f22f-160">Aşağıdaki kodu ekleyin **OnCreate** yöntemi **MainActivity** çağırmadan önce sınıfın `LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="4f22f-160">Add the following code to the **OnCreate** method of the **MainActivity** class before the call to `LoadApplication()`:</span></span>

        // Initialize the authenticator before loading the app.
        App.Init((IAuthenticate)this);

    <span data-ttu-id="4f22f-161">Bu kod, Doğrulayıcı uygulama yükleri önce başlatılmış sağlar.</span><span class="sxs-lookup"><span data-stu-id="4f22f-161">This code ensures the authenticator is initialized before the app loads.</span></span>
2. <span data-ttu-id="4f22f-162">Uygulama yeniden, çalıştırın, ardından seçtiğiniz ve kimliği doğrulanmış bir kullanıcı olarak verilerine erişebilir doğrulayın kimlik doğrulama sağlayıcısının oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4f22f-162">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="add-authentication-to-the-ios-app"></a><span data-ttu-id="4f22f-163">İOS uygulaması için kimlik doğrulaması ekleme</span><span class="sxs-lookup"><span data-stu-id="4f22f-163">Add authentication to the iOS app</span></span>
<span data-ttu-id="4f22f-164">Bu bölümde nasıl uygulandığını gösterir **IAuthenticate** iOS uygulaması projesi arabiriminde.</span><span class="sxs-lookup"><span data-stu-id="4f22f-164">This section shows how to implement the **IAuthenticate** interface in the iOS app project.</span></span> <span data-ttu-id="4f22f-165">İOS cihazları destekleme değil, bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f22f-165">Skip this section if you are not supporting iOS devices.</span></span>

1. <span data-ttu-id="4f22f-166">Visual Studio veya Xamarin Studio'da sağ **iOS** , sonra da proje **başlangıç projesi olarak ayarla**.</span><span class="sxs-lookup"><span data-stu-id="4f22f-166">In Visual Studio or Xamarin Studio, right-click the **iOS** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="4f22f-167">Projeyi Hata Ayıklayıcısı'ndaki başlayın, ardından uygulama başladıktan sonra durum koduyla işlenmeyen bir özel durum 401 (yetkisiz) tetiklenir doğrulamak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="4f22f-167">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="4f22f-168">Arka uç erişimi yalnızca yetkili kullanıcılar ile sınırlı olduğundan 401 yanıtı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4f22f-168">The 401 response is produced because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="4f22f-169">AppDelegate.cs iOS projeyi açın ve aşağıdakileri ekleyin `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="4f22f-169">Open AppDelegate.cs in the iOS project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="4f22f-170">Güncelleştirme **AppDelegate** uygulamak için sınıf **IAuthenticate** arabirimi, aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="4f22f-170">Update the **AppDelegate** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. <span data-ttu-id="4f22f-171">Güncelleştirme **AppDelegate** ekleyerek sınıfı bir **MobileServiceUser** alan ve bir **kimlik doğrulama** gerekli yöntemi **IAuthenticate** arabirimi, aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="4f22f-171">Update the **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

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

            // Display the success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    <span data-ttu-id="4f22f-172">Facebook dışında bir kimlik sağlayıcısı kullanıyorsanız, [MobileServiceAuthenticationProvider] için farklı bir değer seçin.</span><span class="sxs-lookup"><span data-stu-id="4f22f-172">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

6. <span data-ttu-id="4f22f-173">OpenUrl (Uıapplication uygulama, NSUrl url NSDictionary seçenekleri) yöntemi aşırı yüklemesini ekleyerek AppDelegate sınıfını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="4f22f-173">Update the AppDelegate class by adding OpenUrl(UIApplication app, NSUrl url, NSDictionary options) method overload</span></span>

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. <span data-ttu-id="4f22f-174">Aşağıdaki kod satırını ekleyin **FinishedLaunching** yöntemi çağırmadan önce `LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="4f22f-174">Add the following line of code to the **FinishedLaunching** method before the call to `LoadApplication()`:</span></span>

        App.Init(this);

    <span data-ttu-id="4f22f-175">Bu kod, Doğrulayıcı uygulama yüklenmeden önce başlatılmış sağlar.</span><span class="sxs-lookup"><span data-stu-id="4f22f-175">This code ensures the authenticator is initialized before the app is loaded.</span></span>

6. <span data-ttu-id="4f22f-176">Ekleme **{url_scheme_of_your_app}** Info.plist URL şemalarını için.</span><span class="sxs-lookup"><span data-stu-id="4f22f-176">Add **{url_scheme_of_your_app}** to URL Schemes in Info.plist.</span></span>

7. <span data-ttu-id="4f22f-177">Uygulama yeniden, çalıştırın, ardından seçtiğiniz ve kimliği doğrulanmış bir kullanıcı olarak verilerine erişebilir doğrulayın kimlik doğrulama sağlayıcısının oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4f22f-177">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="add-authentication-to-windows-10-including-phone-app-projects"></a><span data-ttu-id="4f22f-178">Windows 10 (Phone dahil) uygulaması projeleri için kimlik doğrulaması ekleme</span><span class="sxs-lookup"><span data-stu-id="4f22f-178">Add authentication to Windows 10 (including Phone) app projects</span></span>
<span data-ttu-id="4f22f-179">Bu bölümde nasıl uygulandığını gösterir **IAuthenticate** Windows 10 uygulaması projeleri arabiriminde.</span><span class="sxs-lookup"><span data-stu-id="4f22f-179">This section shows how to implement the **IAuthenticate** interface in the Windows 10 app projects.</span></span> <span data-ttu-id="4f22f-180">Evrensel Windows Platformu (UWP) projeleri, ancak kullanarak için aynı adımları uygulamak **UWP** projeyle (not ettiğiniz değişir).</span><span class="sxs-lookup"><span data-stu-id="4f22f-180">The same steps apply for Universal Windows Platform (UWP) projects, but using the **UWP** project (with noted changes).</span></span> <span data-ttu-id="4f22f-181">Windows cihazları destekleme değil, bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f22f-181">Skip this section if you are not supporting Windows devices.</span></span>

1. <span data-ttu-id="4f22f-182">"Visual Studio'da sağ **UWP** , sonra da proje **başlangıç projesi olarak ayarla**.</span><span class="sxs-lookup"><span data-stu-id="4f22f-182">"In Visual Studio, right-click either the **UWP** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="4f22f-183">Projeyi Hata Ayıklayıcısı'ndaki başlayın, ardından uygulama başladıktan sonra durum koduyla işlenmeyen bir özel durum 401 (yetkisiz) tetiklenir doğrulamak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="4f22f-183">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="4f22f-184">Arka uç erişimi yalnızca yetkili kullanıcılar ile sınırlı olduğundan 401 yanıt olur.</span><span class="sxs-lookup"><span data-stu-id="4f22f-184">The 401 response happens because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="4f22f-185">Windows uygulama projesi için MainPage.xaml.cs açın ve aşağıdakileri ekleyin `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="4f22f-185">Open MainPage.xaml.cs for the Windows app project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    <span data-ttu-id="4f22f-186">Değiştir `<your_Portable_Class_Library_namespace>` ile taşınabilir sınıf kitaplığı için ad alanı.</span><span class="sxs-lookup"><span data-stu-id="4f22f-186">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span></span>
4. <span data-ttu-id="4f22f-187">Güncelleştirme **MainPage** uygulamak için sınıf **IAuthenticate** arabirimi, aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="4f22f-187">Update the **MainPage** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public sealed partial class MainPage : IAuthenticate
5. <span data-ttu-id="4f22f-188">Güncelleştirme **MainPage** ekleyerek sınıfı bir **MobileServiceUser** alan ve bir **kimlik doğrulama** gerekli yöntemi **IAuthenticate**arabirimi, aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="4f22f-188">Update the **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

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

            // Display the success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    <span data-ttu-id="4f22f-189">Facebook dışında bir kimlik sağlayıcısı kullanıyorsanız, [MobileServiceAuthenticationProvider] için farklı bir değer seçin.</span><span class="sxs-lookup"><span data-stu-id="4f22f-189">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

1. <span data-ttu-id="4f22f-190">Aşağıdaki kod satırını Oluşturucusu eklemek **MainPage** çağırmadan önce sınıfın `LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="4f22f-190">Add the following line of code in the constructor for the **MainPage** class before the call to `LoadApplication()`:</span></span>

        // Initialize the authenticator before loading the app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    <span data-ttu-id="4f22f-191">Değiştir `<your_Portable_Class_Library_namespace>` ile taşınabilir sınıf kitaplığı için ad alanı.</span><span class="sxs-lookup"><span data-stu-id="4f22f-191">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span></span>

3. <span data-ttu-id="4f22f-192">Kullanıyorsanız **UWP**, aşağıdakileri ekleyin **OnActivated** yöntemi geçersiz kılma **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="4f22f-192">If you are using **UWP**, add the following **OnActivated** method override to the **App** class:</span></span>

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   <span data-ttu-id="4f22f-193">Yöntemini geçersiz kılma zaten mevcut olduğunda koşullu kodu önceki kod parçacığını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4f22f-193">When the method override already exists, add the conditional code from the preceding snippet.</span></span>  <span data-ttu-id="4f22f-194">Bu kod, Evrensel Windows projeleri için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="4f22f-194">This code is not required for Universal Windows projects.</span></span>

3. <span data-ttu-id="4f22f-195">Ekleme **{url_scheme_of_your_app}** Package.appxmanifest içinde.</span><span class="sxs-lookup"><span data-stu-id="4f22f-195">Add **{url_scheme_of_your_app}** in Package.appxmanifest.</span></span> 

4. <span data-ttu-id="4f22f-196">Uygulama yeniden, çalıştırın, ardından seçtiğiniz ve kimliği doğrulanmış bir kullanıcı olarak verilerine erişebilir doğrulayın kimlik doğrulama sağlayıcısının oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4f22f-196">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f22f-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4f22f-197">Next steps</span></span>
<span data-ttu-id="4f22f-198">Bu temel kimlik doğrulaması öğreticisini tamamladığınıza göre aşağıdaki öğreticiler birini açın etmeden göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="4f22f-198">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="4f22f-199">Uygulamanıza anında iletme bildirimleri ekleme</span><span class="sxs-lookup"><span data-stu-id="4f22f-199">Add push notifications to your app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)

  <span data-ttu-id="4f22f-200">Uygulamanıza anında iletme bildirimleri desteği eklemeyi ve anında iletme bildirimleri göndermek için Azure Notification Hubs’ı kullanmak üzere Mobile App arka ucunuzu yapılandırmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4f22f-200">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="4f22f-201">Uygulamanız için çevrimdışı eşitlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="4f22f-201">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  <span data-ttu-id="4f22f-202">Bir mobil uygulama arka ucu kullanarak uygulamanıza çevrimdışı destek eklemeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4f22f-202">Learn how to add offline support your app using a Mobile App backend.</span></span> <span data-ttu-id="4f22f-203">Çevrimdışı eşitleme son kullanıcıların görüntüleme, ekleme veya ağ bağlantısı olduğunda bile veri - değiştirme bir mobil uygulamayla - etkileşime olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="4f22f-203">Offline sync allows end users to interact with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
