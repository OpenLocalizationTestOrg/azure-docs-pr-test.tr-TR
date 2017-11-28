---
title: "aaaOpen kaynak teknolojileri SSS Azure web uygulamaları | Microsoft Docs"
description: "Azure App Service Web Apps özelliğini hello açık kaynak teknolojileri hakkında sorular yanıtlar toofrequently alın."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 35cff4f322859d25972747cf55aa7c4316381a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a><span data-ttu-id="3629a-103">Açık kaynak teknolojileri Azure Web uygulamaları için sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="3629a-103">Open-source technologies FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="3629a-104">Bu makalede hello için açık kaynak teknolojileri ile ilgili sorunlar hakkında sorulan sorular (SSS) yanıtlar toofrequently sahip [Azure App Service Web Apps özelliğini](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="3629a-104">This article has answers toofrequently asked questions (FAQs) about issues with open-source technologies for hello [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a><span data-ttu-id="3629a-105">ClearDB veritabanı kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="3629a-105">My ClearDB database is down.</span></span> <span data-ttu-id="3629a-106">Bu nasıl giderebilirim?</span><span class="sxs-lookup"><span data-stu-id="3629a-106">How do I resolve this?</span></span>

<span data-ttu-id="3629a-107">Veritabanı ile ilgili sorunlar için başvurun [ClearDB Destek](https://www.cleardb.com/developers/help/support).</span><span class="sxs-lookup"><span data-stu-id="3629a-107">For database-related issues, contact [ClearDB support](https://www.cleardb.com/developers/help/support).</span></span> 

<span data-ttu-id="3629a-108">ClearDB ilgili yanıtlar toocommon sorular için bkz: [ClearDB SSS](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="3629a-108">For answers toocommon questions about ClearDB, see [ClearDB FAQs](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-isnt-my-cleardb-database-listed-in-hello-portal"></a><span data-ttu-id="3629a-109">ClearDB veritabanı hello Portalı'nda neden listede yok?</span><span class="sxs-lookup"><span data-stu-id="3629a-109">Why isn't my ClearDB database listed in hello portal?</span></span>

<span data-ttu-id="3629a-110">Hello bir ClearDB veritabanı oluşturursanız [Azure portal](http://portal.azure.com/), hello veritabanı hello görünmüyor [Klasik Azure portalı](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="3629a-110">If you create a ClearDB database in hello [Azure portal](http://portal.azure.com/), hello database doesn't appear in hello [Azure classic portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="3629a-111">toowork bu geçici veritabanı toohello web uygulamanızı elle bağlantı kurabilir.</span><span class="sxs-lookup"><span data-stu-id="3629a-111">toowork around this, you can manually link your database toohello web app.</span></span>

<span data-ttu-id="3629a-112">Benzer şekilde, bir ClearDB veritabanı hello oluşturursanız [Klasik Azure portalı](http://manage.windowsazure.com/), hello veritabanınızda görmezsiniz [Azure portal](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3629a-112">Similarly, if you create a ClearDB database in hello [Azure classic portal](http://manage.windowsazure.com/),  you won't see your database in hello [Azure portal](http://portal.azure.com/).</span></span> <span data-ttu-id="3629a-113">Bu durumda, geçici bir çözüm kullanılabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="3629a-113">In this case, no workaround is available.</span></span> 

<span data-ttu-id="3629a-114">Daha fazla bilgi için bkz: [ClearDB MySQL veritabanları için SSS Azure uygulama hizmeti ile](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="3629a-114">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a><span data-ttu-id="3629a-115">Neden ClearDB veritabanı my abonelik geçişi sırasında geçirilen değildi?</span><span class="sxs-lookup"><span data-stu-id="3629a-115">Why wasn't my ClearDB database migrated during my subscription migration?</span></span>

<span data-ttu-id="3629a-116">Abonelikler arasında kaynak geçiş gerçekleştirdiğinizde, bazı sınırlamalar uygulanır.</span><span class="sxs-lookup"><span data-stu-id="3629a-116">When you perform resource migration across subscriptions, some limitations apply.</span></span> <span data-ttu-id="3629a-117">ClearDB MySQL veritabanı bir üçüncü taraf hizmeti ve Azure abonelik geçişi sırasında geçirilmez.</span><span class="sxs-lookup"><span data-stu-id="3629a-117">A ClearDB MySQL database is a third-party service and is not migrated during an Azure subscription migration.</span></span>

<span data-ttu-id="3629a-118">Azure kaynaklarınızı geçirmeden önce MySQL veritabanınızı hello geçişini yönetmiyorsanız ClearDB MySQL veritabanı kullanılamıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="3629a-118">If you don't manage hello migration of your MySQL database before you migrate your Azure resources, your ClearDB MySQL database might be unavailable.</span></span> <span data-ttu-id="3629a-119">tooavoid Bu, ilk olarak, el ile ClearDB veritabanınızı geçirin ve ardından hello web uygulamanız için Azure aboneliği geçirin.</span><span class="sxs-lookup"><span data-stu-id="3629a-119">tooavoid this, first, manually migrate your ClearDB database, and then migrate hello Azure subscription for your web app.</span></span>

<span data-ttu-id="3629a-120">Daha fazla bilgi için bkz: [ClearDB MySQL veritabanları için SSS Azure uygulama hizmeti ile](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="3629a-120">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="how-do-i-turn-on-php-logging-tootroubleshoot-php-issues"></a><span data-ttu-id="3629a-121">Üzerinde PHP tootroubleshoot PHP sorunları günlüğü nasıl kapatırım?</span><span class="sxs-lookup"><span data-stu-id="3629a-121">How do I turn on PHP logging tootroubleshoot PHP issues?</span></span>

<span data-ttu-id="3629a-122">PHP günlüğünü tooturn:</span><span class="sxs-lookup"><span data-stu-id="3629a-122">tooturn on PHP logging:</span></span>

1. <span data-ttu-id="3629a-123">İçinde tooyour oturum [Kudu Web sitesi](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="3629a-123">Sign in tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="3629a-124">Merhaba üst menüde seçin **hata ayıklama Konsolu'nda** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="3629a-124">In hello top menu, select **Debug Console** > **CMD**.</span></span>
3. <span data-ttu-id="3629a-125">Select hello **Site** klasör.</span><span class="sxs-lookup"><span data-stu-id="3629a-125">Select hello **Site** folder.</span></span>
4. <span data-ttu-id="3629a-126">Select hello **wwwroot** klasör.</span><span class="sxs-lookup"><span data-stu-id="3629a-126">Select hello **wwwroot** folder.</span></span>
5. <span data-ttu-id="3629a-127">Select hello  **+**  simgesine ve ardından **yeni dosya**.</span><span class="sxs-lookup"><span data-stu-id="3629a-127">Select hello **+** icon, and then select **New File**.</span></span>
6. <span data-ttu-id="3629a-128">Merhaba dosya adı çok ayarlamak**. user.ini**.</span><span class="sxs-lookup"><span data-stu-id="3629a-128">Set hello file name too**.user.ini**.</span></span>
7. <span data-ttu-id="3629a-129">Merhaba Kurşun Kalem simgesini seçin sonraki çok**. user.ini**.</span><span class="sxs-lookup"><span data-stu-id="3629a-129">Select hello pencil icon next too**.user.ini**.</span></span>
8. <span data-ttu-id="3629a-130">Merhaba dosyasında bu kodu ekleyin:`log_errors=on`</span><span class="sxs-lookup"><span data-stu-id="3629a-130">In hello file, add this code: `log_errors=on`</span></span>
9. <span data-ttu-id="3629a-131">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="3629a-131">Select **Save**.</span></span>
10. <span data-ttu-id="3629a-132">Merhaba Kurşun Kalem simgesini seçin sonraki çok**wp-config.php**.</span><span class="sxs-lookup"><span data-stu-id="3629a-132">Select hello pencil icon next too**wp-config.php**.</span></span>
11. <span data-ttu-id="3629a-133">Merhaba metin toohello kod aşağıdaki gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="3629a-133">Change hello text toohello following code:</span></span>
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging too/wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings tooscreendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors tooscreenini_set('display_errors', 0);
   ```
12. <span data-ttu-id="3629a-134">Hello hello web uygulama menüsünde, Azure portal, web uygulamanızı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="3629a-134">In hello Azure portal, in hello web app menu, restart your web app.</span></span>

<span data-ttu-id="3629a-135">Daha fazla bilgi için bkz: [etkinleştirmek WordPress Hata günlüklerini](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span><span class="sxs-lookup"><span data-stu-id="3629a-135">For more information, see [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a><span data-ttu-id="3629a-136">App Service içinde barındırılan uygulamalar, Python uygulama hatalarını nasıl oturum?</span><span class="sxs-lookup"><span data-stu-id="3629a-136">How do I log Python application errors in apps that are hosted in App Service?</span></span>

<span data-ttu-id="3629a-137">toocapture Python uygulama hatalarını:</span><span class="sxs-lookup"><span data-stu-id="3629a-137">toocapture Python application errors:</span></span>

1. <span data-ttu-id="3629a-138">Hello Azure portalında, web uygulamanızı seçin **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="3629a-138">In hello Azure portal, in your web app, select **Settings**.</span></span>
2. <span data-ttu-id="3629a-139">Merhaba üzerinde **ayarları** sekmesine **uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="3629a-139">On hello **Settings** tab, select **Application settings**.</span></span>
3. <span data-ttu-id="3629a-140">Altında **uygulama ayarları**, anahtar/değer çifti aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="3629a-140">Under **App settings**, enter hello following key/value pair:</span></span>
    * <span data-ttu-id="3629a-141">Anahtar: WSGI_LOG</span><span class="sxs-lookup"><span data-stu-id="3629a-141">Key : WSGI_LOG</span></span>
    * <span data-ttu-id="3629a-142">Değer: D:\home\site\wwwroot\logs.txt (dosya adı seçiminizi girin)</span><span class="sxs-lookup"><span data-stu-id="3629a-142">Value : D:\home\site\wwwroot\logs.txt (enter your choice of file name)</span></span>

<span data-ttu-id="3629a-143">Şimdi hello wwwroot klasöründe hello logs.txt dosyasındaki hatalar görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3629a-143">You should now see errors in hello logs.txt file in hello wwwroot folder.</span></span>

## <a name="how-do-i-change-hello-version-of-hello-nodejs-application-that-is-hosted-in-app-service"></a><span data-ttu-id="3629a-144">Merhaba App Service içinde barındırılan bir Node.js uygulaması hello sürümünü nasıl değişiyor?</span><span class="sxs-lookup"><span data-stu-id="3629a-144">How do I change hello version of hello Node.js application that is hosted in App Service?</span></span>

<span data-ttu-id="3629a-145">Merhaba Node.js uygulaması toochange hello sürümü, aşağıdaki seçenekleri şu hello birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3629a-145">toochange hello version of hello Node.js application, you can use one of hello following options:</span></span>

*   <span data-ttu-id="3629a-146">Hello Azure portal, kullanın **uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="3629a-146">In hello Azure portal, use **App settings**.</span></span>
    1. <span data-ttu-id="3629a-147">Hello Azure portal, tooyour web uygulamasına gidin.</span><span class="sxs-lookup"><span data-stu-id="3629a-147">In hello Azure portal, go tooyour web app.</span></span>
    2. <span data-ttu-id="3629a-148">Merhaba üzerinde **ayarları** dikey penceresinde, select **uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="3629a-148">On hello **Settings** blade, select **Application settings**.</span></span>
    3. <span data-ttu-id="3629a-149">İçinde **uygulama ayarları**WEBSITE_NODE_DEFAULT_VERSION başlangıç anahtarı olarak içerebilir ve hello Node.js sürümünü hello değeri olarak istiyor.</span><span class="sxs-lookup"><span data-stu-id="3629a-149">In **App settings**, you can include WEBSITE_NODE_DEFAULT_VERSION as hello key, and hello version of Node.js you want as hello value.</span></span>
    4. <span data-ttu-id="3629a-150">Tooyour Git [Kudu konsol](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="3629a-150">Go tooyour [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
    5. <span data-ttu-id="3629a-151">toocheck Node.js sürümünü Merhaba, komutu aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="3629a-151">toocheck hello Node.js version, enter hello following command:</span></span>  
   ```
   node -v
   ```
*   <span data-ttu-id="3629a-152">Merhaba iisnode.yml dosyasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3629a-152">Modify hello iisnode.yml file.</span></span> <span data-ttu-id="3629a-153">Merhaba iisnode.yml dosyasını değişen hello Node.js sürümünde yalnızca o iisnode hello çalışma zamanı ortamı ayarlar kullanır.</span><span class="sxs-lookup"><span data-stu-id="3629a-153">Changing hello Node.js version in hello iisnode.yml file only sets hello runtime environment that iisnode uses.</span></span> <span data-ttu-id="3629a-154">Kudu cmd ve diğerleri kümesinde hello Node.js sürümünü kullanmaya devam **uygulama ayarları** hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="3629a-154">Your Kudu cmd and others still use hello Node.js version that is set in **App settings** in hello Azure portal.</span></span>

    <span data-ttu-id="3629a-155">tooset hello iisnode.yml uygulama kök klasörünüzde el ile bir iisnode.yml dosyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3629a-155">tooset hello iisnode.yml manually, create an iisnode.yml file in your app root folder.</span></span> <span data-ttu-id="3629a-156">Merhaba dosyasında aşağıdaki satırı hello şunlardır:</span><span class="sxs-lookup"><span data-stu-id="3629a-156">In hello file, include hello following line:</span></span>
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   <span data-ttu-id="3629a-157">Merhaba iisnode.yml dosyasını kaynak denetimi dağıtımı sırasında package.json kullanarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3629a-157">Set hello iisnode.yml file by using package.json during source control deployment.</span></span>
    <span data-ttu-id="3629a-158">Hello Azure kaynak denetimi dağıtım işlemi hello aşağıdaki adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="3629a-158">hello Azure source control deployment process involves hello following steps:</span></span>
    1. <span data-ttu-id="3629a-159">İçerik toohello Azure web uygulaması taşır.</span><span class="sxs-lookup"><span data-stu-id="3629a-159">Moves content toohello Azure web app.</span></span>
    2. <span data-ttu-id="3629a-160">Hiç yoksa (deploy.cmd, .deployment dosyaları) hello web uygulaması kök klasöründe bir varsayılan dağıtım betiğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3629a-160">Creates a default deployment script, if there isn’t one (deploy.cmd, .deployment files) in hello web app root folder.</span></span>
    3. <span data-ttu-id="3629a-161">Hangi oluşturduğu bir iisnode.yml dosyasını hello Node.js sürümünü hello package.json dosyasında Bahsediyor, bir dağıtım betiği çalıştıran > altyapısı`"engines": {"node": "5.9.1","npm": "3.7.3"}`</span><span class="sxs-lookup"><span data-stu-id="3629a-161">Runs a deployment script in which it creates an iisnode.yml file if you mention hello Node.js version in hello package.json file > engine `"engines": {"node": "5.9.1","npm": "3.7.3"}`</span></span>
    4. <span data-ttu-id="3629a-162">Merhaba iisnode.yml dosyasını aşağıdaki kod hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="3629a-162">hello iisnode.yml file has hello following line of code:</span></span>
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-hello-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a><span data-ttu-id="3629a-163">App Service içinde barındırılan my WordPress uygulamasında selamlama iletisine "veritabanı bağlantısı kurma hatası" görüyorum.</span><span class="sxs-lookup"><span data-stu-id="3629a-163">I see hello message "Error establishing a database connection" in my WordPress app that's hosted in App Service.</span></span> <span data-ttu-id="3629a-164">Bu nasıl giderebilirim?</span><span class="sxs-lookup"><span data-stu-id="3629a-164">How do I troubleshoot this?</span></span>

<span data-ttu-id="3629a-165">Tam hello adımları Azure WordPress uygulaması, tooenable php_errors.log ve debug.log bu hatayı görürseniz, ayrıntılı [etkinleştirmek WordPress Hata günlüklerini](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span><span class="sxs-lookup"><span data-stu-id="3629a-165">If you see this error in your Azure WordPress app, tooenable php_errors.log and debug.log, complete hello steps detailed in [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

<span data-ttu-id="3629a-166">Merhaba günlükleri etkinleştirildiğinde, hello hatayı yeniden oluşturmaya ve bağlantıları dışında çalıştırıyorsanız hello günlükleri toosee kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="3629a-166">When hello logs are enabled, reproduce hello error, and then check hello logs toosee if you are running out of connections:</span></span>
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded hello ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

<span data-ttu-id="3629a-167">Debug.log veya php_errors.log dosyalarınızı bu hatayı görürseniz, uygulamanızı bağlantı hello sayısını aşıyor.</span><span class="sxs-lookup"><span data-stu-id="3629a-167">If you see this error in your debug.log or php_errors.log files, your app is exceeding hello number of connections.</span></span> <span data-ttu-id="3629a-168">ClearDB üzerinde koyduysanız hello kullanılabilir olan bağlantı sayısı doğrulayın, [hizmet planı](https://www.cleardb.com/pricing.view).</span><span class="sxs-lookup"><span data-stu-id="3629a-168">If you’re hosting on ClearDB, verify hello number of connections that are available in your [service plan](https://www.cleardb.com/pricing.view).</span></span>

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a><span data-ttu-id="3629a-169">App Service içinde barındırılan bir Node.js uygulaması nasıl hata?</span><span class="sxs-lookup"><span data-stu-id="3629a-169">How do I debug a Node.js app that's hosted in App Service?</span></span>

1.  <span data-ttu-id="3629a-170">Tooyour Git [Kudu konsol](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span><span class="sxs-lookup"><span data-stu-id="3629a-170">Go tooyour [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span></span>
2.  <span data-ttu-id="3629a-171">Git tooyour uygulama günlükleri klasöründe (D:\home\LogFiles\Application).</span><span class="sxs-lookup"><span data-stu-id="3629a-171">Go tooyour application logs folder (D:\home\LogFiles\Application).</span></span>
3.  <span data-ttu-id="3629a-172">Merhaba logging_errors.txt dosyasında içerik için denetleyin.</span><span class="sxs-lookup"><span data-stu-id="3629a-172">In hello logging_errors.txt file, check for content.</span></span>

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a><span data-ttu-id="3629a-173">Yerel Python modüllerini nasıl bir App Service web uygulaması veya API uygulaması yükleme?</span><span class="sxs-lookup"><span data-stu-id="3629a-173">How do I install native Python modules in an App Service web app or API app?</span></span>

<span data-ttu-id="3629a-174">Bazı paketler, Azure'da PIP kullanarak yüklemeyebilir.</span><span class="sxs-lookup"><span data-stu-id="3629a-174">Some packages might not install by using pip in Azure.</span></span> <span data-ttu-id="3629a-175">Merhaba paket Python paket dizinini hello üzerinde kullanılabilir olabilir ya da bir derleyici gerekli olabilir (derleyici hello web uygulaması App Service içinde çalışan hello bilgisayarda kullanılabilir değildir).</span><span class="sxs-lookup"><span data-stu-id="3629a-175">hello package might not be available on hello Python Package Index, or a compiler might be required (a compiler is not available on hello computer that is running hello web app in App Service).</span></span> <span data-ttu-id="3629a-176">App Service web apps ve API apps yerel modülleri yükleme hakkında daha fazla bilgi için bkz: [uygulama hizmeti yükleme Python modülleri](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span><span class="sxs-lookup"><span data-stu-id="3629a-176">For information about installing native modules in App Service web apps and API apps, see [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span></span>

## <a name="how-do-i-deploy-a-django-app-tooapp-service-by-using-git-and-hello-new-version-of-python"></a><span data-ttu-id="3629a-177">Django uygulama tooApp hizmet Python Git ve hello yeni sürümünü kullanarak nasıl dağıtıldığına?</span><span class="sxs-lookup"><span data-stu-id="3629a-177">How do I deploy a Django app tooApp Service by using Git and hello new version of Python?</span></span>

<span data-ttu-id="3629a-178">Django yükleme hakkında daha fazla bilgi için bkz: [Django uygulama tooApp hizmet dağıtma](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span><span class="sxs-lookup"><span data-stu-id="3629a-178">For information about installing Django, see [Deploying a Django app tooApp Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span></span>

## <a name="where-are-hello-tomcat-log-files-located"></a><span data-ttu-id="3629a-179">Bulunan hello Tomcat günlük dosyalarının nerede?</span><span class="sxs-lookup"><span data-stu-id="3629a-179">Where are hello Tomcat log files located?</span></span>

<span data-ttu-id="3629a-180">Azure Market ve özel dağıtımlar için:</span><span class="sxs-lookup"><span data-stu-id="3629a-180">For Azure Marketplace and custom deployments:</span></span>

* <span data-ttu-id="3629a-181">Klasör konumu: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span><span class="sxs-lookup"><span data-stu-id="3629a-181">Folder location: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span></span>
* <span data-ttu-id="3629a-182">İlgilenilen dosyalar:</span><span class="sxs-lookup"><span data-stu-id="3629a-182">Files of interest:</span></span>
    * <span data-ttu-id="3629a-183">catalina. *yyyy-aa-gg*.log</span><span class="sxs-lookup"><span data-stu-id="3629a-183">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="3629a-184">ana bilgisayar-yöneticisi. *yyyy-aa-gg*.log</span><span class="sxs-lookup"><span data-stu-id="3629a-184">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="3629a-185">localhost. *yyyy-aa-gg*.log</span><span class="sxs-lookup"><span data-stu-id="3629a-185">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="3629a-186">Yöneticisi. *yyyy-aa-gg*.log</span><span class="sxs-lookup"><span data-stu-id="3629a-186">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="3629a-187">site_access_log. *yyyy-aa-gg*.log</span><span class="sxs-lookup"><span data-stu-id="3629a-187">site_access_log.*yyyy-mm-dd*.log</span></span>


<span data-ttu-id="3629a-188">Portal için **uygulama ayarları** dağıtımlar:</span><span class="sxs-lookup"><span data-stu-id="3629a-188">For portal **App settings** deployments:</span></span>

* <span data-ttu-id="3629a-189">Klasör konumu: D:\home\LogFiles</span><span class="sxs-lookup"><span data-stu-id="3629a-189">Folder location: D:\home\LogFiles</span></span>
* <span data-ttu-id="3629a-190">İlgilenilen dosyalar:</span><span class="sxs-lookup"><span data-stu-id="3629a-190">Files of interest:</span></span>
    * <span data-ttu-id="3629a-191">catalina. *yyyy-aa-gg*.log</span><span class="sxs-lookup"><span data-stu-id="3629a-191">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="3629a-192">ana bilgisayar-yöneticisi. *yyyy-aa-gg*.log</span><span class="sxs-lookup"><span data-stu-id="3629a-192">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="3629a-193">localhost. *yyyy-aa-gg*.log</span><span class="sxs-lookup"><span data-stu-id="3629a-193">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="3629a-194">Yöneticisi. *yyyy-aa-gg*.log</span><span class="sxs-lookup"><span data-stu-id="3629a-194">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="3629a-195">site_access_log. *yyyy-aa-gg*.log</span><span class="sxs-lookup"><span data-stu-id="3629a-195">site_access_log.*yyyy-mm-dd*.log</span></span>

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a><span data-ttu-id="3629a-196">Nasıl JDBC sürücüsü bağlantı hatalarını giderme?</span><span class="sxs-lookup"><span data-stu-id="3629a-196">How do I troubleshoot JDBC driver connection errors?</span></span>

<span data-ttu-id="3629a-197">Tomcat günlüklerinizi iletisinde aşağıdaki hello görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3629a-197">You might see hello following message in your Tomcat logs:</span></span>

```
hello web application[ROOT] registered hello JDBC driver [com.mysql.jdbc.Driver] but failed toounregister it when hello web application was stopped. tooprevent a memory leak,hello JDBC Driver has been forcibly unregistered
```

<span data-ttu-id="3629a-198">tooresolve hello hata:</span><span class="sxs-lookup"><span data-stu-id="3629a-198">tooresolve hello error:</span></span>

1. <span data-ttu-id="3629a-199">Merhaba sqljdbc*.jar dosyasını uygulama/lib klasörünüzden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="3629a-199">Remove hello sqljdbc*.jar file from your app/lib folder.</span></span>
2. <span data-ttu-id="3629a-200">Merhaba özel Tomcat veya Azure Market Tomcat web sunucusu kullanıyorsanız, bu .jar dosya toohello Tomcat lib klasörüne kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="3629a-200">If you are using hello custom Tomcat or Azure Marketplace Tomcat web server, copy this .jar file toohello Tomcat lib folder.</span></span>
3. <span data-ttu-id="3629a-201">Azure portal Java'dan etkinleştiriyorsanız hello (seçin **Java 1.8** > **Tomcat sunucusunu**), paralel tooyour uygulama hello klasör hello sqljdbc.* jar dosya kopyala.</span><span class="sxs-lookup"><span data-stu-id="3629a-201">If you are enabling Java from hello Azure portal (select **Java 1.8** > **Tomcat server**), copy hello sqljdbc.* jar file in hello folder that's parallel tooyour app.</span></span> <span data-ttu-id="3629a-202">Ardından, aşağıdaki sınıf ayarı toohello web.config dosyasına hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3629a-202">Then, add hello following classpath setting toohello web.config file:</span></span>

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path toohello sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-toocopy-live-log-files"></a><span data-ttu-id="3629a-203">Toocopy dinamik günlük dosyalarını çalıştığınızda neden hataları görüyor?</span><span class="sxs-lookup"><span data-stu-id="3629a-203">Why do I see errors when I attempt toocopy live log files?</span></span>

<span data-ttu-id="3629a-204">Java uygulama (örneğin, Tomcat) için toocopy dinamik günlük dosyaları çalışırsanız, bu FTP hata görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3629a-204">If you try toocopy live log files for a Java app (for example, Tomcat), you might see this FTP error:</span></span>

```
Error transferring file [filename] Copying files from remote side failed.
    
hello process cannot access hello file because it is being used by another process.
```

<span data-ttu-id="3629a-205">Merhaba hata iletisi, FTP hello istemci bağlı olarak değişebilir.</span><span class="sxs-lookup"><span data-stu-id="3629a-205">hello error message might vary, depending on hello FTP client.</span></span>

<span data-ttu-id="3629a-206">Tüm Java uygulamalarını bu bir kilitleme sorunu var.</span><span class="sxs-lookup"><span data-stu-id="3629a-206">All Java apps have this locking issue.</span></span> <span data-ttu-id="3629a-207">Yalnızca Kudu hello uygulama çalışırken bu dosya indirme destekler.</span><span class="sxs-lookup"><span data-stu-id="3629a-207">Only Kudu supports downloading this file while hello app is running.</span></span>

<span data-ttu-id="3629a-208">Durdurma hello uygulamanın toothese dosyaları FTP erişimi verir.</span><span class="sxs-lookup"><span data-stu-id="3629a-208">Stopping hello app allows FTP access toothese files.</span></span>

<span data-ttu-id="3629a-209">Başka bir çözüm toowrite bir zamanlamaya göre çalışır ve bu dosyaları tooa farklı dizine kopyalar bir Web işi ' dir.</span><span class="sxs-lookup"><span data-stu-id="3629a-209">Another workaround is toowrite a WebJob that runs on a schedule and copies these files tooa different directory.</span></span> <span data-ttu-id="3629a-210">Örnek proje için bkz: hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) projesi.</span><span class="sxs-lookup"><span data-stu-id="3629a-210">For a sample project, see hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) project.</span></span>

## <a name="where-do-i-find-hello-log-files-for-jetty"></a><span data-ttu-id="3629a-211">Merhaba günlük dosyaları için Jetty nerede bulabilirim?</span><span class="sxs-lookup"><span data-stu-id="3629a-211">Where do I find hello log files for Jetty?</span></span>

<span data-ttu-id="3629a-212">Market ve özel dağıtımlar için hello günlük dosyası hello D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs klasöründe bulunur.</span><span class="sxs-lookup"><span data-stu-id="3629a-212">For Marketplace and custom deployments, hello log file is in hello D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs folder.</span></span> <span data-ttu-id="3629a-213">Merhaba klasör konumu, kullanmakta olduğunuz Jetty hello sürümü bağlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3629a-213">Note that hello folder location depends on hello version of Jetty you are using.</span></span> <span data-ttu-id="3629a-214">Örneğin, hello yolu buraya 9.1.2 Jetty için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="3629a-214">For example, hello path provided here is for Jetty 9.1.2.</span></span> <span data-ttu-id="3629a-215">Jetty_ için Ara*YYYY_MM_DD*. stderrout.log.</span><span class="sxs-lookup"><span data-stu-id="3629a-215">Look for jetty_*YYYY_MM_DD*.stderrout.log.</span></span>

<span data-ttu-id="3629a-216">Portal uygulama ayarı dağıtımları için D:\home\LogFiles hello günlük dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="3629a-216">For portal App Setting deployments, hello log file is in D:\home\LogFiles.</span></span> <span data-ttu-id="3629a-217">Jetty_ için Ara*YYYY_MM_DD*. stderrout.log</span><span class="sxs-lookup"><span data-stu-id="3629a-217">Look for jetty_*YYYY_MM_DD*.stderrout.log</span></span>

## <a name="can-i-send-email-from-my-azure-web-app"></a><span data-ttu-id="3629a-218">My Azure web uygulamasından e-posta gönderebilir miyim?</span><span class="sxs-lookup"><span data-stu-id="3629a-218">Can I send email from my Azure web app?</span></span>

<span data-ttu-id="3629a-219">Uygulama hizmeti yerleşik e-posta özelliği yoktur.</span><span class="sxs-lookup"><span data-stu-id="3629a-219">App Service doesn't have a built-in email feature.</span></span> <span data-ttu-id="3629a-220">Uygulamanızdan, e-posta göndermek için bazı iyi alternatifleri görmek için bu [yığın taşması tartışma](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span><span class="sxs-lookup"><span data-stu-id="3629a-220">For some good alternatives for sending email from your app, see this [Stack Overflow discussion](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span></span>

## <a name="why-does-my-wordpress-site-redirect-tooanother-url"></a><span data-ttu-id="3629a-221">Neden WordPress Sitem tooanother URL yeniden yönlendirme?</span><span class="sxs-lookup"><span data-stu-id="3629a-221">Why does my WordPress site redirect tooanother URL?</span></span>

<span data-ttu-id="3629a-222">TooAzure son geçiş yaptıysanız, WordPress toohello eski etki alanı URL'si yönlendirebilir.</span><span class="sxs-lookup"><span data-stu-id="3629a-222">If you have recently migrated tooAzure, WordPress might redirect toohello old domain URL.</span></span> <span data-ttu-id="3629a-223">Bu ayar hello MySQL veritabanında kaynaklanır.</span><span class="sxs-lookup"><span data-stu-id="3629a-223">This is caused by a setting in hello MySQL database.</span></span>

<span data-ttu-id="3629a-224">WordPress arkadaş + Azure Site doğrudan hello veritabanında tooupdate hello yeniden yönlendirme URL'sini kullanabileceğiniz uzantısıdır.</span><span class="sxs-lookup"><span data-stu-id="3629a-224">WordPress Buddy+ is an Azure Site Extension that you can use tooupdate hello redirection URL directly in hello database.</span></span> <span data-ttu-id="3629a-225">WordPress arkadaş + kullanma hakkında daha fazla bilgi için bkz: [WordPress araçları ve MySQL geçiş ile WordPress arkadaş +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="3629a-225">For more information about using WordPress Buddy+, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

<span data-ttu-id="3629a-226">Alternatif olarak, SQL sorguları veya PHPMyAdmin kullanarak toomanually güncelleştirme hello yeniden yönlendirme URL'sini tercih ederseniz, bkz. [WordPress: toowrong URL yeniden yönlendirme](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span><span class="sxs-lookup"><span data-stu-id="3629a-226">Alternatively, if you prefer toomanually update hello redirection URL by using SQL queries or PHPMyAdmin, see [WordPress: Redirecting toowrong URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span></span>

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a><span data-ttu-id="3629a-227">Oturum açma WordPress parolamı nasıl değişiyor?</span><span class="sxs-lookup"><span data-stu-id="3629a-227">How do I change my WordPress sign-in password?</span></span>

<span data-ttu-id="3629a-228">Oturum açma WordPress parolanızı unuttuysanız, WordPress arkadaş + tooupdate kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3629a-228">If you have forgotten your WordPress sign-in password, you can use WordPress Buddy+ tooupdate it.</span></span> <span data-ttu-id="3629a-229">Parola, yükleme hello WordPress arkadaş + Azure Site uzantısı ve ardından tam hello adımları açıklanan tooreset [WordPress araçları ve MySQL geçiş ile WordPress arkadaş +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="3629a-229">tooreset your password, install hello WordPress Buddy+ Azure Site Extension, and then complete hello steps described in [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="i-cant-sign-in-toowordpress-how-do-i-resolve-this"></a><span data-ttu-id="3629a-230">İçinde tooWordPress oturum açamazsınız.</span><span class="sxs-lookup"><span data-stu-id="3629a-230">I can't sign in tooWordPress.</span></span> <span data-ttu-id="3629a-231">Bu nasıl giderebilirim?</span><span class="sxs-lookup"><span data-stu-id="3629a-231">How do I resolve this?</span></span>

<span data-ttu-id="3629a-232">Kendiniz WordPress dışında bir eklenti yükledikten sonra son kilitli bulursanız, hatalı bir eklenti olabilir.</span><span class="sxs-lookup"><span data-stu-id="3629a-232">If you find yourself locked out of WordPress after recently installing a plugin, you might have a faulty plugin.</span></span> <span data-ttu-id="3629a-233">WordPress arkadaş + yardımcı olabilecek bir Azure Site uzantısı, WordPress eklentileri devre dışı bırak'dır.</span><span class="sxs-lookup"><span data-stu-id="3629a-233">WordPress Buddy+ is an Azure Site Extension that can help you disable plugins in WordPress.</span></span> <span data-ttu-id="3629a-234">Daha fazla bilgi için bkz: [WordPress araçları ve MySQL geçiş ile WordPress arkadaş +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="3629a-234">For more information, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="how-do-i-migrate-my-wordpress-database"></a><span data-ttu-id="3629a-235">WordPress Veritabanım nasıl geçişini?</span><span class="sxs-lookup"><span data-stu-id="3629a-235">How do I migrate my WordPress database?</span></span>

<span data-ttu-id="3629a-236">Bağlı tooyour WordPress Web sitesidir geçirme hello MySQL veritabanı için birçok seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="3629a-236">You have multiple options for migrating hello MySQL database that's connected tooyour WordPress website:</span></span>

* <span data-ttu-id="3629a-237">Geliştiricileri: Kullanım hello [komut istemi veya PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span><span class="sxs-lookup"><span data-stu-id="3629a-237">Developers: Use hello [command prompt or PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span></span>
* <span data-ttu-id="3629a-238">Olmayan-Geliştiriciler: [WordPress arkadaş +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span><span class="sxs-lookup"><span data-stu-id="3629a-238">Non-developers: Use [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span></span>

## <a name="how-do-i-help-make-wordpress-more-secure"></a><span data-ttu-id="3629a-239">WordPress daha güvenli hale getirmenize nasıl yardımcı?</span><span class="sxs-lookup"><span data-stu-id="3629a-239">How do I help make WordPress more secure?</span></span>

<span data-ttu-id="3629a-240">toolearn WordPress için önerilen güvenlik uygulamaları hakkında bkz [azure'da WordPress güvenlik için en iyi uygulamaları](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span><span class="sxs-lookup"><span data-stu-id="3629a-240">toolearn about security best practices for WordPress, see [Best practices for WordPress security in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span></span>

## <a name="i-am-trying-toouse-phpmyadmin-and-i-see-hello-message-access-denied-how-do-i-resolve-this"></a><span data-ttu-id="3629a-241">Toouse PHPMyAdmin çalışıyorum ve selamlama iletisine "erişim engellendi." bakın</span><span class="sxs-lookup"><span data-stu-id="3629a-241">I am trying toouse PHPMyAdmin, and I see hello message “Access denied.”</span></span> <span data-ttu-id="3629a-242">Bu nasıl giderebilirim?</span><span class="sxs-lookup"><span data-stu-id="3629a-242">How do I resolve this?</span></span>

<span data-ttu-id="3629a-243">Bu uygulama hizmeti örnek Hello MySQL uygulama özelliği henüz çalışmıyorsa bu sorunla karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3629a-243">You might experience this issue if hello MySQL in-app feature isn't running yet in this App Service instance.</span></span> <span data-ttu-id="3629a-244">tooresolve Web sitenizi sorunu, try tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="3629a-244">tooresolve hello issue, try tooaccess your website.</span></span> <span data-ttu-id="3629a-245">Bu hello uygulama MySQL işlemi dahil olmak üzere gerekli hello işlemleri başlatır.</span><span class="sxs-lookup"><span data-stu-id="3629a-245">This starts hello required processes, including hello MySQL in-app process.</span></span> <span data-ttu-id="3629a-246">Uygulama çalışıyor, işlem Explorer'da MySQL bu mysqld.exe olun tooverify hello işlemlerde listelenir.</span><span class="sxs-lookup"><span data-stu-id="3629a-246">tooverify that MySQL in-app is running, in Process Explorer, ensure that mysqld.exe is listed in hello processes.</span></span>

<span data-ttu-id="3629a-247">Uygulama MySQL çalıştığından emin olduktan sonra toouse PHPMyAdmin deneyin.</span><span class="sxs-lookup"><span data-stu-id="3629a-247">After you ensure that MySQL in-app is running, try toouse PHPMyAdmin.</span></span>

## <a name="i-get-an-http-403-error-when-i-try-tooimport-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a><span data-ttu-id="3629a-248">Tooimport deneyin veya MySQL uygulama Veritabanım PHPMyadmin kullanarak dışarı HTTP 403 hata alın.</span><span class="sxs-lookup"><span data-stu-id="3629a-248">I get an HTTP 403 error when I try tooimport or export my MySQL in-app database by using PHPMyadmin.</span></span> <span data-ttu-id="3629a-249">Bu nasıl giderebilirim?</span><span class="sxs-lookup"><span data-stu-id="3629a-249">How do I resolve this?</span></span>

<span data-ttu-id="3629a-250">Chrome eski bir sürümünü kullanıyorsanız, bilinen hata yaşıyor.</span><span class="sxs-lookup"><span data-stu-id="3629a-250">If you are using an older version of Chrome, you might be experiencing a known bug.</span></span> <span data-ttu-id="3629a-251">tooresolve hello sorunu, Chrome yükseltme tooa sürümü.</span><span class="sxs-lookup"><span data-stu-id="3629a-251">tooresolve hello issue, upgrade tooa newer version of Chrome.</span></span> <span data-ttu-id="3629a-252">Ayrıca Internet Explorer veya Edge'i, burada hello sorun oluşmaz gibi farklı bir tarayıcı kullanarak deneyin.</span><span class="sxs-lookup"><span data-stu-id="3629a-252">Also try using a different browser, like Internet Explorer or Edge, where hello issue does not occur.</span></span>
