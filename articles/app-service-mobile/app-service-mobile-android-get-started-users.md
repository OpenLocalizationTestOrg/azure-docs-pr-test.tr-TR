---
title: "Android Mobile Apps ile kimlik doğrulamasını aaaAdd | Microsoft Docs"
description: "Nasıl toouse hello tooauthenticate kullanıcılarının Android uygulamanızın kimlik sağlayıcıları, Google, Facebook, Twitter ve Microsoft dahil olmak üzere çeşitli Azure App Service Mobile Apps özelliğini öğrenin."
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 1fc8e7c1-6c3c-40f4-9967-9cf5e21fc4e1
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 01f608f996c931c643790ed2778df11cf590c903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-android-app"></a><span data-ttu-id="19e46-103">Kimlik doğrulama tooyour Android uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="19e46-103">Add authentication tooyour Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="19e46-104">Özet</span><span class="sxs-lookup"><span data-stu-id="19e46-104">Summary</span></span>
<span data-ttu-id="19e46-105">Bu öğreticide, desteklenen kimlik sağlayıcısı kullanarak Android kimlik doğrulama toohello todolist hızlı başlangıç projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="19e46-105">In this tutorial, you add authentication toohello todolist quickstart project on Android by using a supported identity provider.</span></span> <span data-ttu-id="19e46-106">Bu öğretici hello üzerinde temel [Mobile Apps'i kullanmaya başlamak] önce tamamlamanız gereken öğretici.</span><span class="sxs-lookup"><span data-stu-id="19e46-106">This tutorial is based on hello [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="19e46-107"><a name="register"></a>Kimlik doğrulaması için uygulamanızı kaydetmenizi ve Azure uygulama hizmeti yapılandırın</span><span class="sxs-lookup"><span data-stu-id="19e46-107"><a name="register"></a>Register your app for authentication and configure Azure App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="19e46-108"><a name="redirecturl"></a>Uygulama toohello izin verilen dış yönlendirme URL'lerini ekleme</span><span class="sxs-lookup"><span data-stu-id="19e46-108"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="19e46-109">Uygulamanız için yeni bir URL şemasını tanımlamak güvenli kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="19e46-109">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="19e46-110">Merhaba kimlik doğrulama işlemi tamamlandıktan sonra bu hello authentication sistem tooredirect geri tooyour uygulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="19e46-110">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="19e46-111">Bu öğreticide, kullandığımız hello URL şeması _appname_ boyunca.</span><span class="sxs-lookup"><span data-stu-id="19e46-111">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="19e46-112">Ancak, seçtiğiniz herhangi bir URL şeması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19e46-112">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="19e46-113">Benzersiz tooyour mobil uygulama olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="19e46-113">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="19e46-114">Merhaba sunucu tarafı tooenable hello yönlendirme:</span><span class="sxs-lookup"><span data-stu-id="19e46-114">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="19e46-115">Hello [Azure portalı]'da, uygulama hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="19e46-115">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="19e46-116">Merhaba tıklatın **kimlik doğrulama / yetkilendirme** menü seçeneği.</span><span class="sxs-lookup"><span data-stu-id="19e46-116">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="19e46-117">Merhaba, **yeniden yönlendirme URL'lere izin**, girin `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="19e46-117">In hello **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="19e46-118">Merhaba _appname_ bu içinde hello URL şeması mobil uygulamanız için bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="19e46-118">hello _appname_ in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="19e46-119">Bir protokol (harf kullanın ve yalnızca sayı ve bir harf ile başlar) için normal URL belirtimi izlemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="19e46-119">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="19e46-120">Merhaba çeşitli yerlerde URL şeması ile mobil uygulama kodunuzu tooadjust gerekeceğinden, seçtiğiniz hello dize Not olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="19e46-120">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="19e46-121">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="19e46-121">Click **OK**.</span></span>

5. <span data-ttu-id="19e46-122">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="19e46-122">Click **Save**.</span></span>

## <span data-ttu-id="19e46-123"><a name="permissions"></a>İzinleri tooauthenticated kullanıcılarını kısıtlayın</span><span class="sxs-lookup"><span data-stu-id="19e46-123"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* <span data-ttu-id="19e46-124">Android Studio'da hello eğitici, tamamlandı hello proje açmak [Mobile Apps'i kullanmaya başlamak].</span><span class="sxs-lookup"><span data-stu-id="19e46-124">In Android Studio, open hello project you completed with hello tutorial [Get started with Mobile Apps].</span></span> <span data-ttu-id="19e46-125">Hello gelen **çalıştırmak** menüsünde tıklatın **uygulama çalıştırma**ve hello uygulama başladıktan sonra durum koduyla işlenmeyen bir özel durum 401 (yetkisiz) tetiklenir doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="19e46-125">From hello **Run** menu, click **Run app**, and verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span>

     <span data-ttu-id="19e46-126">Merhaba uygulama denemeleri tooaccess hello geri bitiş kimliği doğrulanmamış bir kullanıcı olarak, ancak hello için bu özel durum *Todoıtem* tablo artık kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="19e46-126">This exception happens because hello app attempts tooaccess hello back end as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="19e46-127">Ardından, hello uygulama tooauthenticate kullanıcılar kaynakları Mobile Apps bitiş hello istemeden önce güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="19e46-127">Next, you update hello app tooauthenticate users before requesting resources from hello Mobile Apps back end.</span></span> 

## <a name="add-authentication-toohello-app"></a><span data-ttu-id="19e46-128">Kimlik doğrulama toohello uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="19e46-128">Add authentication toohello app</span></span>
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <span data-ttu-id="19e46-129"><a name="cache-tokens"></a>Kimlik doğrulama belirteçleri hello istemcide önbelleğe alma</span><span class="sxs-lookup"><span data-stu-id="19e46-129"><a name="cache-tokens"></a>Cache authentication tokens on hello client</span></span>
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="19e46-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="19e46-130">Next steps</span></span>
<span data-ttu-id="19e46-131">Bu temel kimlik doğrulaması öğreticisini tamamladığınıza göre öğreticileri aşağıdaki hello tooone üzerinde etmeden göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="19e46-131">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="19e46-132">[Anında iletme bildirimleri tooyour Android uygulaması eklemek](app-service-mobile-android-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="19e46-132">[Add push notifications tooyour Android app](app-service-mobile-android-get-started-push.md).</span></span>
  <span data-ttu-id="19e46-133">Mobile Apps geri tooconfigure toouse Azure bildirim hub'ları toosend anında iletme bildirimleri nasıl sona erdirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="19e46-133">Learn how tooconfigure your Mobile Apps back end toouse Azure notification hubs toosend push notifications.</span></span>
* <span data-ttu-id="19e46-134">[Android uygulamanız için çevrimdışı eşitlemeyi etkinleştirme](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="19e46-134">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="19e46-135">Nasıl tooadd çevrimdışı destek tooyour uygulama Mobile Apps arka ucu kullanarak bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="19e46-135">Learn how tooadd offline support tooyour app by using a Mobile Apps back end.</span></span> <span data-ttu-id="19e46-136">Çevrimdışı Eşitleme ile kullanıcılar mobil uygulama ile etkileşim kurabilen&mdash;görüntüleme, ekleme veya değiştirme veri&mdash;hiçbir ağ bağlantısı olduğunda bile.</span><span class="sxs-lookup"><span data-stu-id="19e46-136">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions tooauthenticated users]: #permissions
[Add authentication toohello app]: #add-authentication
[Store authentication tokens on hello client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
[Mobile Apps'i kullanmaya başlamak]: app-service-mobile-android-get-started.md
