---
title: "Apache Cordova Mobile Apps ile kimlik doğrulaması ekleyin | Microsoft Docs"
description: "Apache Cordova uygulamanızı kimlik sağlayıcıları, Google, Facebook, Twitter ve Microsoft dahil olmak üzere çeşitli kullanıcıların kimliklerini doğrulamak için Azure App Service'de Mobile Apps kullanmayı öğrenin."
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
ms.openlocfilehash: b7362b7f26859de541f792e714502851d74c98e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-apache-cordova-app"></a><span data-ttu-id="b0f9d-103">Apache Cordova uygulamanıza kimlik doğrulaması ekleme</span><span class="sxs-lookup"><span data-stu-id="b0f9d-103">Add authentication to your Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="b0f9d-104">Özet</span><span class="sxs-lookup"><span data-stu-id="b0f9d-104">Summary</span></span>
<span data-ttu-id="b0f9d-105">Bu öğretici kapsamında, kimlik doğrulama desteklenen kimlik sağlayıcısı kullanarak Apache Cordova todolist hızlı başlangıç projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-105">In this tutorial, you add authentication to the todolist quickstart project on Apache Cordova using a supported identity provider.</span></span> <span data-ttu-id="b0f9d-106">Bu öğretici dayanır [Mobile Apps'i kullanmaya başlamak] önce tamamlamanız gereken öğretici.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-106">This tutorial is based on the [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="b0f9d-107"><a name="register"></a>Kimlik doğrulaması için uygulamanızı kaydetme ve uygulama hizmetini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b0f9d-107"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[<span data-ttu-id="b0f9d-108">Benzer adımları gösteren bir video izleyin</span><span class="sxs-lookup"><span data-stu-id="b0f9d-108">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <span data-ttu-id="b0f9d-109"><a name="permissions"></a>Kimliği doğrulanmış kullanıcılar için izinleri kısıtla</span><span class="sxs-lookup"><span data-stu-id="b0f9d-109"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="b0f9d-110">Şimdi, arka adsız erişim devre dışı olduğunu doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-110">Now, you can verify that anonymous access to your backend has been disabled.</span></span> <span data-ttu-id="b0f9d-111">Visual Studio'da:</span><span class="sxs-lookup"><span data-stu-id="b0f9d-111">In Visual Studio:</span></span>

* <span data-ttu-id="b0f9d-112">Öğretici tamamlandığında oluşturduğunuz projeyi açın [Mobile Apps'i kullanmaya başlamak].</span><span class="sxs-lookup"><span data-stu-id="b0f9d-112">Open the project that you created when you completed the tutorial [Get started with Mobile Apps].</span></span>
* <span data-ttu-id="b0f9d-113">Uygulamanızı çalıştırın **Google Android öykünücüsü**.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-113">Run your application in the **Google Android Emulator**.</span></span>
* <span data-ttu-id="b0f9d-114">Uygulama başlatıldıktan sonra beklenmeyen bir bağlantı hatası göründüğünü doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-114">Verify that an Unexpected Connection Failure is shown after the app starts.</span></span>

<span data-ttu-id="b0f9d-115">Ardından, mobil uygulama arka ucundan kaynakları istemeden önce kullanıcıların kimliklerini doğrulamak için uygulamayı güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-115">Next, update the app to authenticate users before requesting resources from the Mobile App backend.</span></span>

## <span data-ttu-id="b0f9d-116"><a name="add-authentication"></a>Kimlik doğrulaması için uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="b0f9d-116"><a name="add-authentication"></a>Add authentication to the app</span></span>
1. <span data-ttu-id="b0f9d-117">Projenizde açmak **Visual Studio**, ardından açık `www/index.html` dosyayı düzenlemek için.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-117">Open your project in **Visual Studio**, then open the `www/index.html` file for editing.</span></span>
2. <span data-ttu-id="b0f9d-118">Bulun `Content-Security-Policy` baş bölümünde meta etiketi.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-118">Locate the `Content-Security-Policy` meta tag in the head section.</span></span>  <span data-ttu-id="b0f9d-119">İzin verilen kaynaklar listesine OAuth konak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-119">Add the OAuth host to the list of allowed sources.</span></span>

   | <span data-ttu-id="b0f9d-120">Sağlayıcı</span><span class="sxs-lookup"><span data-stu-id="b0f9d-120">Provider</span></span> | <span data-ttu-id="b0f9d-121">SDK sağlayıcı adı</span><span class="sxs-lookup"><span data-stu-id="b0f9d-121">SDK Provider Name</span></span> | <span data-ttu-id="b0f9d-122">OAuth ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="b0f9d-122">OAuth Host</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="b0f9d-123">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0f9d-123">Azure Active Directory</span></span> | <span data-ttu-id="b0f9d-124">aad</span><span class="sxs-lookup"><span data-stu-id="b0f9d-124">aad</span></span> | <span data-ttu-id="b0f9d-125">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="b0f9d-125">https://login.microsoftonline.com</span></span> |
   | <span data-ttu-id="b0f9d-126">Facebook</span><span class="sxs-lookup"><span data-stu-id="b0f9d-126">Facebook</span></span> | <span data-ttu-id="b0f9d-127">Facebook</span><span class="sxs-lookup"><span data-stu-id="b0f9d-127">facebook</span></span> | <span data-ttu-id="b0f9d-128">https://www.facebook.com</span><span class="sxs-lookup"><span data-stu-id="b0f9d-128">https://www.facebook.com</span></span> |
   | <span data-ttu-id="b0f9d-129">Google</span><span class="sxs-lookup"><span data-stu-id="b0f9d-129">Google</span></span> | <span data-ttu-id="b0f9d-130">Google</span><span class="sxs-lookup"><span data-stu-id="b0f9d-130">google</span></span> | <span data-ttu-id="b0f9d-131">https://Accounts.Google.com</span><span class="sxs-lookup"><span data-stu-id="b0f9d-131">https://accounts.google.com</span></span> |
   | <span data-ttu-id="b0f9d-132">Microsoft</span><span class="sxs-lookup"><span data-stu-id="b0f9d-132">Microsoft</span></span> | <span data-ttu-id="b0f9d-133">MicrosoftAccount</span><span class="sxs-lookup"><span data-stu-id="b0f9d-133">microsoftaccount</span></span> | <span data-ttu-id="b0f9d-134">https://Login.live.com</span><span class="sxs-lookup"><span data-stu-id="b0f9d-134">https://login.live.com</span></span> |
   | <span data-ttu-id="b0f9d-135">Twitter</span><span class="sxs-lookup"><span data-stu-id="b0f9d-135">Twitter</span></span> | <span data-ttu-id="b0f9d-136">Twitter</span><span class="sxs-lookup"><span data-stu-id="b0f9d-136">twitter</span></span> | <span data-ttu-id="b0f9d-137">https://api.twitter.com</span><span class="sxs-lookup"><span data-stu-id="b0f9d-137">https://api.twitter.com</span></span> |

    <span data-ttu-id="b0f9d-138">İçerik güvenlik (Azure Active Directory için uygulanan) ilkeye örneği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="b0f9d-138">An example Content-Security-Policy (implemented for Azure Active Directory) is as follows:</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    <span data-ttu-id="b0f9d-139">Değiştir `https://login.microsoftonline.com` önceki tabloda OAuth host ile.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-139">Replace `https://login.microsoftonline.com` with the OAuth host from the preceding table.</span></span>  <span data-ttu-id="b0f9d-140">İçerik güvenlik ilkesi meta etiketi hakkında daha fazla bilgi için bkz: [içerik Güvenlik İlkesi belgeleri].</span><span class="sxs-lookup"><span data-stu-id="b0f9d-140">For more information about the content-security-policy meta tag, see the [Content-Security-Policy documentation].</span></span>

    <span data-ttu-id="b0f9d-141">Bazı kimlik doğrulama sağlayıcıları uygun mobil cihazlarda kullanıldığında içerik güvenlik ilkesi değişikliklerini gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-141">Some authentication providers do not require Content-Security-Policy changes when used on appropriate mobile devices.</span></span>  <span data-ttu-id="b0f9d-142">Örneğin, bir Android cihazında Google kimlik doğrulaması kullanırken, içerik güvenlik ilkesi değişiklik gerekmez.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-142">For example, no Content-Security-Policy changes are required when using Google authentication on an Android device.</span></span>

3. <span data-ttu-id="b0f9d-143">Açık `www/js/index.js` dosya düzenlemek için bulun `onDeviceReady()` yöntemi, ve istemci oluşturmanın altında kod aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b0f9d-143">Open the `www/js/index.js` file for editing, locate the `onDeviceReady()` method, and under the client  creation code add the following code:</span></span>

        // Login to the service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh the todoItems
                refreshDisplay();

                // Wire up the UI Event Handler for the Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    <span data-ttu-id="b0f9d-144">Bu kod, tablo başvurusu oluşturur ve kullanıcı arabirimini yeniler var olan kodu değiştirir.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-144">This code replaces the existing code that creates the table reference and refreshes the UI.</span></span>

    <span data-ttu-id="b0f9d-145">Tanımlar: login() yöntemi kimlik doğrulama sağlayıcı ile başlatır.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-145">The login() method starts authentication with the provider.</span></span> <span data-ttu-id="b0f9d-146">JavaScript Promise döndüren bir zaman uyumsuz işlev tanımlar: login() yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-146">The login() method is an async function that returns a JavaScript Promise.</span></span>  <span data-ttu-id="b0f9d-147">Böylece tanımlar: login() yöntemi tamamlanana kadar bu yürütülemiyor başlatma kalan içinde promise yanıt yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-147">The rest of the initialization is placed inside the promise response so that it is not executed until the login() method completes.</span></span>

4. <span data-ttu-id="b0f9d-148">Yeni eklediğiniz kodla, `SDK_Provider_Name` , oturum açma sağlayıcısı adı.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-148">In the code that you just added, replace `SDK_Provider_Name` with the name of your login provider.</span></span> <span data-ttu-id="b0f9d-149">Örneğin, Azure Active Directory kullanmak `client.login('aad')`.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-149">For example, for Azure Active Directory, use `client.login('aad')`.</span></span>
5. <span data-ttu-id="b0f9d-150">Projenizi çalıştırma.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-150">Run your project.</span></span>  <span data-ttu-id="b0f9d-151">Proje başlatma tamamlandığında, uygulamanız için seçilen kimlik doğrulama sağlayıcısı OAuth oturum açma sayfasına gösterir.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-151">When the project has finished initializing, your application shows the OAuth login page for the chosen authentication provider.</span></span>

## <span data-ttu-id="b0f9d-152"><a name="next-steps"></a>Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="b0f9d-152"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="b0f9d-153">Daha fazla bilgi edinin [kimlik doğrulama hakkında] Azure uygulama hizmeti ile.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-153">Learn more [About Authentication] with Azure App Service.</span></span>
* <span data-ttu-id="b0f9d-154">Öğretici ekleyerek devam [anında iletme bildirimleri] Apache Cordova uygulamanıza.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-154">Continue the tutorial by adding [Push Notifications] to your Apache Cordova app.</span></span>

<span data-ttu-id="b0f9d-155">SDK'ları kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="b0f9d-155">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="b0f9d-156">[Apache Cordova SDK]</span><span class="sxs-lookup"><span data-stu-id="b0f9d-156">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="b0f9d-157">[ASP.NET Sunucusu SDK]</span><span class="sxs-lookup"><span data-stu-id="b0f9d-157">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="b0f9d-158">[Node.js Sunucusu SDK]</span><span class="sxs-lookup"><span data-stu-id="b0f9d-158">[Node.js Server SDK]</span></span>

<!-- URLs. -->
<span data-ttu-id="b0f9d-159">[Mobile Apps'i kullanmaya başlamak]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="b0f9d-159">[Get started with Mobile Apps]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="b0f9d-160">[içerik Güvenlik İlkesi belgeleri]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html</span><span class="sxs-lookup"><span data-stu-id="b0f9d-160">[Content-Security-Policy documentation]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html</span></span>
<span data-ttu-id="b0f9d-161">[anında iletme bildirimleri]: app-service-mobile-cordova-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="b0f9d-161">[Push Notifications]: app-service-mobile-cordova-get-started-push.md</span></span>
<span data-ttu-id="b0f9d-162">[kimlik doğrulama hakkında]: app-service-mobile-auth.md</span><span class="sxs-lookup"><span data-stu-id="b0f9d-162">[About Authentication]: app-service-mobile-auth.md</span></span>
<span data-ttu-id="b0f9d-163">[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md</span><span class="sxs-lookup"><span data-stu-id="b0f9d-163">[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md</span></span>
<span data-ttu-id="b0f9d-164">[ASP.NET Sunucusu SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="b0f9d-164">[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span></span>
<span data-ttu-id="b0f9d-165">[Node.js Sunucusu SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="b0f9d-165">[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span></span>
