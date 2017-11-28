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
# <a name="add-authentication-tooyour-xamarinandroid-app"></a><span data-ttu-id="569ea-103">Kimlik doğrulama tooyour Xamarin.Android uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="569ea-103">Add authentication tooyour Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="569ea-104">Bu konu, nasıl gösterir istemci uygulamanız mobil uygulamasından tooauthenticate kullanıcıları.</span><span class="sxs-lookup"><span data-stu-id="569ea-104">This topic shows you how tooauthenticate users of a Mobile App from your client application.</span></span> <span data-ttu-id="569ea-105">Bu öğreticide, Azure Mobile Apps tarafından desteklenen bir kimlik sağlayıcısı kullanarak kimlik doğrulaması toohello hızlı başlangıç projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="569ea-105">In this tutorial, you add authentication toohello quickstart project using an identity provider that is supported by Azure Mobile Apps.</span></span> <span data-ttu-id="569ea-106">Başarılı bir şekilde kimliği doğrulanmış ve hello mobil uygulama yetkili sonra hello kullanıcı kimliği değeri görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="569ea-106">After being successfully authenticated and authorized in hello Mobile App, hello user ID value is displayed.</span></span>

<span data-ttu-id="569ea-107">Bu öğretici hello mobil uygulama quickstart üzerinde temel alır.</span><span class="sxs-lookup"><span data-stu-id="569ea-107">This tutorial is based on hello Mobile App quickstart.</span></span> <span data-ttu-id="569ea-108">Ayrıca ilk hello öğreticiyi tamamlamanız gerekir [Xamarin.Android uygulaması oluşturma].</span><span class="sxs-lookup"><span data-stu-id="569ea-108">You must also first complete hello tutorial [Create a Xamarin.Android app].</span></span> <span data-ttu-id="569ea-109">Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, hello kimlik doğrulaması uzantı paketini tooyour projesi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="569ea-109">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="569ea-110">Server uzantısı paketleri hakkında daha fazla bilgi için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="569ea-110">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <span data-ttu-id="569ea-111"><a name="register"></a>Kimlik doğrulaması için uygulamanızı kaydetme ve uygulama hizmetlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="569ea-111"><a name="register"></a>Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="569ea-112"><a name="redirecturl"></a>Uygulama toohello izin verilen dış yönlendirme URL'lerini ekleme</span><span class="sxs-lookup"><span data-stu-id="569ea-112"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="569ea-113">Uygulamanız için yeni bir URL şemasını tanımlamak güvenli kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="569ea-113">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="569ea-114">Merhaba kimlik doğrulama işlemi tamamlandıktan sonra bu hello authentication sistem tooredirect geri tooyour uygulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="569ea-114">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="569ea-115">Bu öğreticide, kullandığımız hello URL şeması _appname_ boyunca.</span><span class="sxs-lookup"><span data-stu-id="569ea-115">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="569ea-116">Ancak, seçtiğiniz herhangi bir URL şeması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="569ea-116">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="569ea-117">Benzersiz tooyour mobil uygulama olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="569ea-117">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="569ea-118">Merhaba sunucu tarafı tooenable hello yönlendirme:</span><span class="sxs-lookup"><span data-stu-id="569ea-118">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="569ea-119">Hello [Azure portalı]'da, uygulama hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="569ea-119">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="569ea-120">Merhaba tıklatın **kimlik doğrulama / yetkilendirme** menü seçeneği.</span><span class="sxs-lookup"><span data-stu-id="569ea-120">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="569ea-121">Merhaba, **yeniden yönlendirme URL'lere izin**, girin `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="569ea-121">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="569ea-122">Merhaba **url_scheme_of_your_app** bu içinde hello URL şeması mobil uygulamanız için bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="569ea-122">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="569ea-123">Bir protokol (harf kullanın ve yalnızca sayı ve bir harf ile başlar) için normal URL belirtimi izlemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="569ea-123">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="569ea-124">Merhaba çeşitli yerlerde URL şeması ile mobil uygulama kodunuzu tooadjust gerekeceğinden, seçtiğiniz hello dize Not olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="569ea-124">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="569ea-125">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="569ea-125">Click **OK**.</span></span>

5. <span data-ttu-id="569ea-126">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="569ea-126">Click **Save**.</span></span>

## <span data-ttu-id="569ea-127"><a name="permissions"></a>İzinleri tooauthenticated kullanıcılarını kısıtlayın</span><span class="sxs-lookup"><span data-stu-id="569ea-127"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="569ea-128">Visual Studio veya Xamarin Studio'da hello istemci projesi bir cihaz veya öykünücü çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="569ea-128">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator.</span></span> <span data-ttu-id="569ea-129">Merhaba uygulama başladıktan sonra durum koduyla işlenmeyen bir özel durum 401 (yetkisiz) tetiklenir doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="569ea-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="569ea-130">Merhaba uygulama kimliği doğrulanmamış bir kullanıcı olarak, mobil uygulamanızın arka ucuna tooaccess çalıştığı meydana gelir.</span><span class="sxs-lookup"><span data-stu-id="569ea-130">This happens because hello app attempts tooaccess your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="569ea-131">Merhaba *Todoıtem* tablo artık kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="569ea-131">hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="569ea-132">Ardından, kimliği doğrulanmış bir kullanıcı ile Merhaba istemci uygulaması toorequest hello mobil uygulama arka ucu kaynaklardan güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="569ea-132">Next, you will update hello client app toorequest resources from hello Mobile App backend with an authenticated user.</span></span>

## <span data-ttu-id="569ea-133"><a name="add-authentication"></a>Kimlik doğrulama toohello uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="569ea-133"><a name="add-authentication"></a>Add authentication toohello app</span></span>
<span data-ttu-id="569ea-134">Merhaba uygulamadır güncelleştirilmiş toorequire kullanıcılar tootap hello **oturum** düğmesine tıklayın ve veri görüntülenmeden önce kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="569ea-134">hello app is updated toorequire users tootap hello **Sign in** button and authenticate before data is displayed.</span></span>

1. <span data-ttu-id="569ea-135">Aşağıdaki kodu toohello hello eklemek **TodoActivity** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="569ea-135">Add hello following code toohello **TodoActivity** class:</span></span>
   
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
   
    <span data-ttu-id="569ea-136">Bu yeni bir yöntem tooauthenticate bir kullanıcı bir yöntem işleyici yeni bir oluşturur ve **oturum** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="569ea-136">This creates a new method tooauthenticate a user and a method handler for a new **Sign in** button.</span></span> <span data-ttu-id="569ea-137">Yukarıdaki örnek kod hello Hello kullanıcı Facebook oturum açma kullanılarak doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="569ea-137">hello user in hello example code above is authenticated by using a Facebook login.</span></span> <span data-ttu-id="569ea-138">Bir iletişim kutusu bir kez kimlik doğrulaması kullanılan toodisplay hello kullanıcı kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="569ea-138">A dialog is used toodisplay hello user ID once authenticated.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="569ea-139">Facebook dışında bir kimlik sağlayıcısı kullanıyorsanız, çok geçirilen hello değeri değiştirmek**LoginAsync** tooone hello aşağıdaki yukarıda: *MicrosoftAccount*, *Twitter*, *Google*, veya *WindowsAzureActiveDirectory*.</span><span class="sxs-lookup"><span data-stu-id="569ea-139">If you are using an identity provider other than Facebook, change hello value passed too**LoginAsync** above tooone of hello following: *MicrosoftAccount*, *Twitter*, *Google*, or *WindowsAzureActiveDirectory*.</span></span>
   > 
   > 
2. <span data-ttu-id="569ea-140">Merhaba, **OnCreate** yöntemi, delete ya da aşağıdaki kod satırını açıklama kullanıma hello:</span><span class="sxs-lookup"><span data-stu-id="569ea-140">In hello **OnCreate** method, delete or comment-out hello following line of code:</span></span>
   
        OnRefreshItemsSelected ();
3. <span data-ttu-id="569ea-141">Merhaba Activity_To_Do.axml dosyasında hello aşağıdakileri ekleyin *LoginUser* düğmesini hello varolan önce tanımını *addItem* düğmesi:</span><span class="sxs-lookup"><span data-stu-id="569ea-141">In hello Activity_To_Do.axml file, add hello following *LoginUser* button definition before hello existing *AddItem* button:</span></span>
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. <span data-ttu-id="569ea-142">Aşağıdaki öğe toohello Strings.xml kaynaklar dosyasına hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="569ea-142">Add hello following element toohello Strings.xml resources file:</span></span>
   
        <string name="login_button_text">Sign in</string>
5. <span data-ttu-id="569ea-143">Merhaba AndroidManifest.xml dosyasını açın, hello kod içinde aşağıdaki ekleme `<application>` XML öğesi:</span><span class="sxs-lookup"><span data-stu-id="569ea-143">Open hello AndroidManifest.xml file, add hello following code inside `<application>` XML element:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. <span data-ttu-id="569ea-144">Visual Studio veya Xamarin Studio, bir cihaz veya öykünücü hello istemci projesi çalıştırın ve seçilen kimlik sağlayıcınız ile oturum açın.</span><span class="sxs-lookup"><span data-stu-id="569ea-144">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator and sign in with your chosen identity provider.</span></span> <span data-ttu-id="569ea-145">Başarıyla oturum açma zaman hello uygulama oturum açma Kimliğiniz görüntülenir ve hello listesi Yapılacaklar öğelerini ve güncelleştirmeleri toohello veri yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="569ea-145">When you are successfully logged-in, hello app will display your login ID and hello list of todo items, and you can make updates toohello data.</span></span>

<!-- URLs. -->
[Xamarin.Android uygulaması oluşturma]: app-service-mobile-xamarin-android-get-started.md