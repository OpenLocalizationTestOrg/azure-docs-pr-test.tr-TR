---
title: "Apache Cordova Mobile Apps ile kimlik doğrulamasını aaaAdd | Microsoft Docs"
description: "Bilgi nasıl toouse Mobile Apps tooauthenticate kullanıcıları kimlik sağlayıcıları, Google, Facebook, Twitter ve Microsoft dahil olmak üzere çeşitli Apache Cordova uygulamanızı Azure App Service içinde."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 10dd6dc9-ddf5-423d-8205-00ad74929f0d
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 61a05c5ac67fd0f0bc4c9d6920954a9b464a0a8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-apache-cordova-app"></a><span data-ttu-id="1e1e6-103">Kimlik doğrulama tooyour Apache Cordova uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="1e1e6-103">Add authentication tooyour Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="1e1e6-104">Özet</span><span class="sxs-lookup"><span data-stu-id="1e1e6-104">Summary</span></span>
<span data-ttu-id="1e1e6-105">Bu öğreticide, Apache Cordova desteklenen kimlik sağlayıcısı kullanarak kimlik doğrulaması toohello todolist hızlı başlangıç projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-105">In this tutorial, you add authentication toohello todolist quickstart project on Apache Cordova using a supported identity provider.</span></span> <span data-ttu-id="1e1e6-106">Bu öğretici hello üzerinde temel [Mobile Apps'i kullanmaya başlamak] önce tamamlamanız gereken öğretici.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-106">This tutorial is based on hello [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="1e1e6-107"><a name="register"></a>Kimlik doğrulaması için uygulamanızı kaydetmenizi ve hello uygulama hizmetini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1e1e6-107"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[<span data-ttu-id="1e1e6-108">Benzer adımları gösteren bir video izleyin</span><span class="sxs-lookup"><span data-stu-id="1e1e6-108">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <span data-ttu-id="1e1e6-109"><a name="permissions"></a>İzinleri tooauthenticated kullanıcılarını kısıtlayın</span><span class="sxs-lookup"><span data-stu-id="1e1e6-109"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="1e1e6-110">Şimdi, bu anonim erişim tooyour arka uç devre dışı doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-110">Now, you can verify that anonymous access tooyour backend has been disabled.</span></span> <span data-ttu-id="1e1e6-111">Visual Studio'da:</span><span class="sxs-lookup"><span data-stu-id="1e1e6-111">In Visual Studio:</span></span>

* <span data-ttu-id="1e1e6-112">Başlangıç Öğreticisi tamamlandığında oluşturduğunuz açık hello proje [Mobile Apps'i kullanmaya başlamak].</span><span class="sxs-lookup"><span data-stu-id="1e1e6-112">Open hello project that you created when you completed hello tutorial [Get started with Mobile Apps].</span></span>
* <span data-ttu-id="1e1e6-113">Hello uygulamanızı çalıştırın **Google Android öykünücüsü**.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-113">Run your application in hello **Google Android Emulator**.</span></span>
* <span data-ttu-id="1e1e6-114">Merhaba uygulama başladıktan sonra beklenmeyen bir bağlantı hatası göründüğünü doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-114">Verify that an Unexpected Connection Failure is shown after hello app starts.</span></span>

<span data-ttu-id="1e1e6-115">Ardından, hello uygulama tooauthenticate kullanıcılar kaynakları hello mobil uygulama arka ucundan istemeden önce güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-115">Next, update hello app tooauthenticate users before requesting resources from hello Mobile App backend.</span></span>

## <span data-ttu-id="1e1e6-116"><a name="add-authentication"></a>Kimlik doğrulama toohello uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="1e1e6-116"><a name="add-authentication"></a>Add authentication toohello app</span></span>
1. <span data-ttu-id="1e1e6-117">Projenizde açmak **Visual Studio**, ardından açık hello `www/index.html` dosyayı düzenlemek için.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-117">Open your project in **Visual Studio**, then open hello `www/index.html` file for editing.</span></span>
2. <span data-ttu-id="1e1e6-118">Merhaba bulun `Content-Security-Policy` hello baş bölümünde meta etiketi.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-118">Locate hello `Content-Security-Policy` meta tag in hello head section.</span></span>  <span data-ttu-id="1e1e6-119">Merhaba OAuth konak toohello izin verilen kaynaklar listesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-119">Add hello OAuth host toohello list of allowed sources.</span></span>

   | <span data-ttu-id="1e1e6-120">Sağlayıcı</span><span class="sxs-lookup"><span data-stu-id="1e1e6-120">Provider</span></span> | <span data-ttu-id="1e1e6-121">SDK sağlayıcı adı</span><span class="sxs-lookup"><span data-stu-id="1e1e6-121">SDK Provider Name</span></span> | <span data-ttu-id="1e1e6-122">OAuth ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="1e1e6-122">OAuth Host</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="1e1e6-123">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e1e6-123">Azure Active Directory</span></span> | <span data-ttu-id="1e1e6-124">aad</span><span class="sxs-lookup"><span data-stu-id="1e1e6-124">aad</span></span> | <span data-ttu-id="1e1e6-125">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="1e1e6-125">https://login.microsoftonline.com</span></span> |
   | <span data-ttu-id="1e1e6-126">Facebook</span><span class="sxs-lookup"><span data-stu-id="1e1e6-126">Facebook</span></span> | <span data-ttu-id="1e1e6-127">Facebook</span><span class="sxs-lookup"><span data-stu-id="1e1e6-127">facebook</span></span> | <span data-ttu-id="1e1e6-128">https://www.facebook.com</span><span class="sxs-lookup"><span data-stu-id="1e1e6-128">https://www.facebook.com</span></span> |
   | <span data-ttu-id="1e1e6-129">Google</span><span class="sxs-lookup"><span data-stu-id="1e1e6-129">Google</span></span> | <span data-ttu-id="1e1e6-130">Google</span><span class="sxs-lookup"><span data-stu-id="1e1e6-130">google</span></span> | <span data-ttu-id="1e1e6-131">https://Accounts.Google.com</span><span class="sxs-lookup"><span data-stu-id="1e1e6-131">https://accounts.google.com</span></span> |
   | <span data-ttu-id="1e1e6-132">Microsoft</span><span class="sxs-lookup"><span data-stu-id="1e1e6-132">Microsoft</span></span> | <span data-ttu-id="1e1e6-133">MicrosoftAccount</span><span class="sxs-lookup"><span data-stu-id="1e1e6-133">microsoftaccount</span></span> | <span data-ttu-id="1e1e6-134">https://Login.live.com</span><span class="sxs-lookup"><span data-stu-id="1e1e6-134">https://login.live.com</span></span> |
   | <span data-ttu-id="1e1e6-135">Twitter</span><span class="sxs-lookup"><span data-stu-id="1e1e6-135">Twitter</span></span> | <span data-ttu-id="1e1e6-136">Twitter</span><span class="sxs-lookup"><span data-stu-id="1e1e6-136">twitter</span></span> | <span data-ttu-id="1e1e6-137">https://api.twitter.com</span><span class="sxs-lookup"><span data-stu-id="1e1e6-137">https://api.twitter.com</span></span> |

    <span data-ttu-id="1e1e6-138">İçerik güvenlik (Azure Active Directory için uygulanan) ilkeye örneği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="1e1e6-138">An example Content-Security-Policy (implemented for Azure Active Directory) is as follows:</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    <span data-ttu-id="1e1e6-139">Değiştir `https://login.microsoftonline.com` tablo önceki hello hello OAuth host ile.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-139">Replace `https://login.microsoftonline.com` with hello OAuth host from hello preceding table.</span></span>  <span data-ttu-id="1e1e6-140">Merhaba hello içerik güvenlik ilkesi meta etiketi hakkında daha fazla bilgi için bkz: [içerik Güvenlik İlkesi belgeleri].</span><span class="sxs-lookup"><span data-stu-id="1e1e6-140">For more information about hello content-security-policy meta tag, see hello [Content-Security-Policy documentation].</span></span>

    <span data-ttu-id="1e1e6-141">Bazı kimlik doğrulama sağlayıcıları uygun mobil cihazlarda kullanıldığında içerik güvenlik ilkesi değişikliklerini gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-141">Some authentication providers do not require Content-Security-Policy changes when used on appropriate mobile devices.</span></span>  <span data-ttu-id="1e1e6-142">Örneğin, bir Android cihazında Google kimlik doğrulaması kullanırken, içerik güvenlik ilkesi değişiklik gerekmez.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-142">For example, no Content-Security-Policy changes are required when using Google authentication on an Android device.</span></span>

3. <span data-ttu-id="1e1e6-143">Açık hello `www/js/index.js` dosya düzenlemek için hello bulun `onDeviceReady()` yöntemini ve hello istemci oluşturmanın altında koddan hello kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1e1e6-143">Open hello `www/js/index.js` file for editing, locate hello `onDeviceReady()` method, and under hello client  creation code add hello following code:</span></span>

        // Login toohello service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    <span data-ttu-id="1e1e6-144">Bu kod hello tablo başvurusu oluşturan ve hello UI yeniler hello var olan kodu değiştirir.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-144">This code replaces hello existing code that creates hello table reference and refreshes hello UI.</span></span>

    <span data-ttu-id="1e1e6-145">Merhaba tanımlar: login() yöntemi hello sağlayıcı ile kimlik doğrulamasını başlatır.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-145">hello login() method starts authentication with hello provider.</span></span> <span data-ttu-id="1e1e6-146">JavaScript Promise döndüren bir zaman uyumsuz işlev Hello tanımlar: login() yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-146">hello login() method is an async function that returns a JavaScript Promise.</span></span>  <span data-ttu-id="1e1e6-147">Böylece Hello tanımlar: login() yöntemi tamamlanana kadar bu yürütülemiyor hello rest hello başlatma hello promise yanıt içinde yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-147">hello rest of hello initialization is placed inside hello promise response so that it is not executed until hello login() method completes.</span></span>

4. <span data-ttu-id="1e1e6-148">Yeni eklediğiniz hello kodda Değiştir `SDK_Provider_Name` hello adıyla oturum açma sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-148">In hello code that you just added, replace `SDK_Provider_Name` with hello name of your login provider.</span></span> <span data-ttu-id="1e1e6-149">Örneğin, Azure Active Directory kullanmak `client.login('aad')`.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-149">For example, for Azure Active Directory, use `client.login('aad')`.</span></span>
5. <span data-ttu-id="1e1e6-150">Projenizi çalıştırma.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-150">Run your project.</span></span>  <span data-ttu-id="1e1e6-151">Merhaba proje başlatma tamamlandığında, uygulamanızı hello OAuth oturum açma sayfasına kimlik doğrulama sağlayıcısı seçilen hello için gösterir.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-151">When hello project has finished initializing, your application shows hello OAuth login page for hello chosen authentication provider.</span></span>

## <span data-ttu-id="1e1e6-152"><a name="next-steps"></a>Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="1e1e6-152"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="1e1e6-153">Daha fazla bilgi edinin [kimlik doğrulama hakkında] Azure uygulama hizmeti ile.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-153">Learn more [About Authentication] with Azure App Service.</span></span>
* <span data-ttu-id="1e1e6-154">Başlangıç Öğreticisi ekleyerek devam [anında iletme bildirimleri] tooyour Apache Cordova uygulaması.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-154">Continue hello tutorial by adding [Push Notifications] tooyour Apache Cordova app.</span></span>

<span data-ttu-id="1e1e6-155">Nasıl toouse hello SDK'ları hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="1e1e6-155">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="1e1e6-156">[Apache Cordova SDK]</span><span class="sxs-lookup"><span data-stu-id="1e1e6-156">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="1e1e6-157">[ASP.NET Sunucusu SDK]</span><span class="sxs-lookup"><span data-stu-id="1e1e6-157">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="1e1e6-158">[Node.js Sunucusu SDK]</span><span class="sxs-lookup"><span data-stu-id="1e1e6-158">[Node.js Server SDK]</span></span>

<!-- URLs. -->
[Mobile Apps'i kullanmaya başlamak]: app-service-mobile-cordova-get-started.md
[içerik Güvenlik İlkesi belgeleri]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html
[anında iletme bildirimleri]: app-service-mobile-cordova-get-started-push.md
[kimlik doğrulama hakkında]: app-service-mobile-auth.md
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Sunucusu SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Sunucusu SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
