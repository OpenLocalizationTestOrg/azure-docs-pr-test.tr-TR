---
title: aaaConfigure PHP Azure App Service Web Apps ile | Microsoft Docs
description: "Nasıl tooconfigure varsayılan PHP yükleme hello veya Azure App Service'deki Web uygulamaları için özel bir PHP yükleme ekleme öğrenin."
services: app-service
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 95c4072b-8570-496b-9c48-ee21a223fb60
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 2e461e4a269a4ce5614f5f05560f38bc53066251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-php-in-azure-app-service-web-apps"></a><span data-ttu-id="4ba3e-103">Azure App Service Web Apps PHP yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4ba3e-103">Configure PHP in Azure App Service Web Apps</span></span>
## <a name="introduction"></a><span data-ttu-id="4ba3e-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="4ba3e-104">Introduction</span></span>
<span data-ttu-id="4ba3e-105">Bu kılavuz size nasıl tooconfigure hello yerleşik PHP çalışma zamanı Web uygulamalarının gösterir [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), özel bir PHP çalışma zamanı sağlamak ve uzantılarını etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-105">This guide will show you how tooconfigure hello built-in PHP runtime for Web Apps in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), provide a custom PHP runtime, and enable extensions.</span></span> <span data-ttu-id="4ba3e-106">Uygulama hizmeti toouse hello için kaydolun [ücretsiz deneme sürümü].</span><span class="sxs-lookup"><span data-stu-id="4ba3e-106">toouse App Service, sign up for hello [free trial].</span></span> <span data-ttu-id="4ba3e-107">tooget hello en bu Rehberde, önce bir PHP web uygulaması App Service'te oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-107">tooget hello most from this guide, you should first create a PHP web app in App Service.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-hello-built-in-php-version"></a><span data-ttu-id="4ba3e-108">Nasıl yapılır: değişiklik hello yerleşik PHP sürümü</span><span class="sxs-lookup"><span data-stu-id="4ba3e-108">How to: Change hello built-in PHP version</span></span>
<span data-ttu-id="4ba3e-109">Bir App Service web uygulaması oluşturduğunuzda varsayılan olarak, PHP 5.5 yüklü ve kullanmak için hemen kullanılabilir durumdadır.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-109">By default, PHP 5.5 is installed and immediately available for use when you create an App Service web app.</span></span> <span data-ttu-id="4ba3e-110">Merhaba en iyi şekilde toosee hello kullanılabilir sürüm düzeltme, varsayılan yapılandırmasıyla ve hello etkin uzantıları olan toodeploy hello çağıran bir komut dosyası [phpinfo()] işlevi.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-110">hello best way toosee hello available release revision, its default configuration, and hello enabled extensions is toodeploy a script that calls hello [phpinfo()] function.</span></span>

<span data-ttu-id="4ba3e-111">PHP 5.6 ve PHP 7.0 sürümleri de kullanılabilir, ancak varsayılan olarak etkin değildir.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-111">PHP 5.6 and PHP 7.0 versions are also available, but not enabled by default.</span></span> <span data-ttu-id="4ba3e-112">tooupdate hello PHP sürümünü, bu yöntemlerden birini izleyin:</span><span class="sxs-lookup"><span data-stu-id="4ba3e-112">tooupdate hello PHP version, follow one of these methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="4ba3e-113">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4ba3e-113">Azure Portal</span></span>
1. <span data-ttu-id="4ba3e-114">Merhaba tooyour web uygulamasında Gözat [Azure Portal](https://portal.azure.com) üzerinde hello tıklatıp **ayarları** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-114">Browse tooyour web app in hello [Azure Portal](https://portal.azure.com) and click on hello **Settings** button.</span></span>
   
    ![Web uygulaması ayarları][settings-button]
2. <span data-ttu-id="4ba3e-116">Merhaba gelen **ayarları** dikey seçin **uygulama ayarları** ve hello yeni PHP sürümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-116">From hello **Settings** blade select **Application Settings** and choose hello new PHP version.</span></span>
   
    ![Uygulama ayarları][application-settings]
3. <span data-ttu-id="4ba3e-118">Merhaba tıklatın **kaydetmek** düğmesi hello hello üstündeki **Web uygulaması ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-118">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Yapılandırma ayarlarını Kaydet][save-button]

### <a name="azure-powershell-windows"></a><span data-ttu-id="4ba3e-120">Azure PowerShell'i (Windows)</span><span class="sxs-lookup"><span data-stu-id="4ba3e-120">Azure PowerShell (Windows)</span></span>
1. <span data-ttu-id="4ba3e-121">Azure PowerShell ve oturum açma tooyour hesap açın:</span><span class="sxs-lookup"><span data-stu-id="4ba3e-121">Open Azure PowerShell, and login tooyour account:</span></span>
   
        PS C:\> Login-AzureRmAccount
2. <span data-ttu-id="4ba3e-122">Merhaba web uygulaması için Hello PHP sürümünü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-122">Set hello PHP version for hello web app.</span></span>
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. <span data-ttu-id="4ba3e-123">Merhaba PHP sürümünü şimdi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-123">hello PHP version is now set.</span></span> <span data-ttu-id="4ba3e-124">Bu ayarları doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4ba3e-124">You can confirm these settings:</span></span>
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a><span data-ttu-id="4ba3e-125">Azure komut satırı arabirimi (Linux, Mac, Windows)</span><span class="sxs-lookup"><span data-stu-id="4ba3e-125">Azure Command-Line Interface (Linux, Mac, Windows)</span></span>
<span data-ttu-id="4ba3e-126">toouse Merhaba Azure komut satırı arabirimi, sahip olmanız gerekir **Node.js** bilgisayarınızda yüklü.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-126">toouse hello Azure Command-Line Interface, you must have **Node.js** installed on your computer.</span></span>

1. <span data-ttu-id="4ba3e-127">Terminali açın ve oturum açma tooyour hesabı.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-127">Open Terminal, and login tooyour account.</span></span>
   
        azure login
2. <span data-ttu-id="4ba3e-128">Merhaba web uygulaması için Hello PHP sürümünü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-128">Set hello PHP version for hello web app.</span></span>
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. <span data-ttu-id="4ba3e-129">Merhaba PHP sürümünü şimdi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-129">hello PHP version is now set.</span></span> <span data-ttu-id="4ba3e-130">Bu ayarları doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4ba3e-130">You can confirm these settings:</span></span>
   
        azure site show {app-name}

> [!NOTE] 
> <span data-ttu-id="4ba3e-131">Merhaba [Azure CLI 2.0](https://github.com/Azure/azure-cli) eşdeğer toohello yukarıdaki komutları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4ba3e-131">hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands that are equivalent toohello above are:</span></span>
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-hello-built-in-php-configurations"></a><span data-ttu-id="4ba3e-132">Nasıl yapılır: hello yerleşik PHP yapılandırmalarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="4ba3e-132">How to: Change hello built-in PHP configurations</span></span>
<span data-ttu-id="4ba3e-133">Tüm yerleşik PHP çalışma zamanı için hello yapılandırma seçeneklerinden herhangi birini hello adımları izleyerek değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-133">For any built-in PHP runtime, you can change any of hello configuration options by following hello steps below.</span></span> <span data-ttu-id="4ba3e-134">(Php.ini yönergeleri hakkında daha fazla bilgi için bkz: [php.ini yönergeleri listesi].)</span><span class="sxs-lookup"><span data-stu-id="4ba3e-134">(For information about php.ini directives, see [List of php.ini directives].)</span></span>

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a><span data-ttu-id="4ba3e-135">PHP değiştirme\_ını\_kullanıcı, PHP\_ını\_PERDIR, PHP\_ını\_tüm yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="4ba3e-135">Changing PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL configuration settings</span></span>
1. <span data-ttu-id="4ba3e-136">Ekleme bir [. user.ini] dosyası tooyour kök dizini.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-136">Add a [.user.ini] file tooyour root directory.</span></span>
2. <span data-ttu-id="4ba3e-137">Yapılandırma ayarları toohello ekleme `.user.ini` kullanarak dosya hello içinde kullandığınız aynı sözdizimini bir `php.ini` dosyası.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-137">Add configuration settings toohello `.user.ini` file using hello same syntax you would use in a `php.ini` file.</span></span> <span data-ttu-id="4ba3e-138">Örneğin, tooturn hello istediyseniz `display_errors` ayarı ve ayarlamayı `upload_max_filesize` too10M, ayarlama, `.user.ini` dosyası bu metin içerebilir:</span><span class="sxs-lookup"><span data-stu-id="4ba3e-138">For example, if you wanted tooturn hello `display_errors` setting on and set `upload_max_filesize` setting too10M, your `.user.ini` file would contain this text:</span></span>
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on toowrite errors tood:\home\LogFiles\php_errors.log
        ; log_errors=On
3. <span data-ttu-id="4ba3e-139">Web uygulamanızı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-139">Deploy your web app.</span></span>
4. <span data-ttu-id="4ba3e-140">Merhaba web uygulaması yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-140">Restart hello web app.</span></span> <span data-ttu-id="4ba3e-141">(Yeniden başlatma gereklidir çünkü hangi PHP hello sıklığı okur `.user.ini` dosyaları hello tarafından yönetilir `user_ini.cache_ttl` sistem düzeyi ayarı ve 300 saniye (5 dakika) varsayılan ayarı.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-141">(Restarting is necessary because hello frequency with which PHP reads `.user.ini` files is governed by hello `user_ini.cache_ttl` setting, which is a system level setting and is 300 seconds (5 minutes) by default.</span></span> <span data-ttu-id="4ba3e-142">Yeniden başlatma hello web uygulaması zorlar PHP tooread hello yeni ayarlarında hello `.user.ini` dosyası.)</span><span class="sxs-lookup"><span data-stu-id="4ba3e-142">Restarting hello web app forces PHP tooread hello new settings in hello `.user.ini` file.)</span></span>

<span data-ttu-id="4ba3e-143">Bir alternatif toousing olarak bir `.user.ini` dosyası hello kullanabilirsiniz [ini_set()] işlevinde, sistem düzeyinde yönergeleri olmayan betikleri tooset yapılandırma seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-143">As an alternative toousing a `.user.ini` file, you can use hello [ini_set()] function in scripts tooset configuration options that are not system-level directives.</span></span>

### <a name="changing-phpinisystem-configuration-settings"></a><span data-ttu-id="4ba3e-144">PHP değiştirme\_ını\_sistemi yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="4ba3e-144">Changing PHP\_INI\_SYSTEM configuration settings</span></span>
1. <span data-ttu-id="4ba3e-145">Web uygulaması hello anahtara sahip bir uygulama ayarı tooyour eklemek `PHP_INI_SCAN_DIR` ve değeri`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="4ba3e-145">Add an App Setting tooyour Web App with hello key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
2. <span data-ttu-id="4ba3e-146">Oluşturma bir `settings.ini` Kudu konsolunu kullanarak dosya (http://&lt;site adı&gt;. scm.azurewebsite.net) hello içinde `d:\home\site\ini` dizin.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-146">Create an `settings.ini` file using Kudu Console (http://&lt;site-name&gt;.scm.azurewebsite.net) in hello `d:\home\site\ini` directory.</span></span>
3. <span data-ttu-id="4ba3e-147">Yapılandırma ayarları toohello eklemek `settings.ini` kullanarak dosya hello aynı sözdizimini kullanan bir php.ini dosyası.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-147">Add configuration settings toohello `settings.ini` file using hello same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="4ba3e-148">Örneğin, toopoint hello istediyseniz `curl.cainfo` tooa ayarlama `*.crt` dosyası ve 'too512K, ayarı wincache.maxfilesize' ayarlayın, `settings.ini` dosyası bu metin içerebilir:</span><span class="sxs-lookup"><span data-stu-id="4ba3e-148">For example, if you wanted toopoint hello `curl.cainfo` setting tooa `*.crt` file and set 'wincache.maxfilesize' setting too512K, your `settings.ini` file would contain this text:</span></span>
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. <span data-ttu-id="4ba3e-149">Web uygulaması tooload hello değişikliklerinizi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-149">Restart your Web App tooload hello changes.</span></span>

## <a name="how-to-enable-extensions-in-hello-default-php-runtime"></a><span data-ttu-id="4ba3e-150">Nasıl yapılır: hello varsayılan PHP çalışma zamanında eklentilerini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="4ba3e-150">How to: Enable extensions in hello default PHP runtime</span></span>
<span data-ttu-id="4ba3e-151">Merhaba önceki bölümde, hello en iyi şekilde toosee hello varsayılan PHP sürümü, varsayılan yapılandırma ve etkin hello belirtildiği gibi uzantıları olan toodeploy çağıran bir komut dosyası [phpinfo()].</span><span class="sxs-lookup"><span data-stu-id="4ba3e-151">As noted in hello previous section, hello best way toosee hello default PHP version, its default configuration, and hello enabled extensions is toodeploy a script that calls [phpinfo()].</span></span> <span data-ttu-id="4ba3e-152">tooenable ek uzantıları hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4ba3e-152">tooenable additional extensions, follow hello steps below:</span></span>

### <a name="configure-via-ini-settings"></a><span data-ttu-id="4ba3e-153">Aracılığıyla INI ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4ba3e-153">Configure via ini settings</span></span>
1. <span data-ttu-id="4ba3e-154">Ekleme bir `ext` directory toohello `d:\home\site` dizini.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-154">Add a `ext` directory toohello `d:\home\site` directory.</span></span>
2. <span data-ttu-id="4ba3e-155">PUT `.dll` hello uzantısı dosyalarında `ext` dizin (örneğin, `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="4ba3e-155">Put `.dll` extension files in hello `ext` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="4ba3e-156">Merhaba uzantıları olan VC9 ve iş parçacığı güvenli olmayan (nts) uyumlu ve PHP, varsayılan sürümü ile uyumlu olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-156">Make sure that hello extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="4ba3e-157">Web uygulaması hello anahtara sahip bir uygulama ayarı tooyour eklemek `PHP_INI_SCAN_DIR` ve değeri`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="4ba3e-157">Add an App Setting tooyour Web App with hello key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
4. <span data-ttu-id="4ba3e-158">Oluşturma bir `ini` dosyasını `d:\home\site\ini` adlı `extensions.ini`.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-158">Create an `ini` file in `d:\home\site\ini` called `extensions.ini`.</span></span>
5. <span data-ttu-id="4ba3e-159">Yapılandırma ayarları toohello eklemek `extensions.ini` kullanarak dosya hello aynı sözdizimini kullanan bir php.ini dosyası.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-159">Add configuration settings toohello `extensions.ini` file using hello same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="4ba3e-160">Örneğin, MongoDB ve XDebug tooenable hello uzantıları, istediyseniz, `extensions.ini` bu metin dosyasını içerebilir:</span><span class="sxs-lookup"><span data-stu-id="4ba3e-160">For example, if you wanted tooenable hello MongoDB and XDebug extensions, your `extensions.ini` file would contain this text:</span></span>
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. <span data-ttu-id="4ba3e-161">Web uygulaması tooload hello değişikliklerinizi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-161">Restart your Web App tooload hello changes.</span></span>

### <a name="configure-via-app-setting"></a><span data-ttu-id="4ba3e-162">Uygulama ayarı aracılığıyla yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4ba3e-162">Configure via App Setting</span></span>
1. <span data-ttu-id="4ba3e-163">Ekleme bir `bin` toohello kök dizin.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-163">Add a `bin` directory toohello root directory.</span></span>
2. <span data-ttu-id="4ba3e-164">PUT `.dll` hello uzantısı dosyalarında `bin` dizin (örneğin, `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="4ba3e-164">Put `.dll` extension files in hello `bin` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="4ba3e-165">Merhaba uzantıları olan VC9 ve iş parçacığı güvenli olmayan (nts) uyumlu ve PHP, varsayılan sürümü ile uyumlu olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-165">Make sure that hello extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="4ba3e-166">Web uygulamanızı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-166">Deploy your web app.</span></span>
4. <span data-ttu-id="4ba3e-167">Tooyour web uygulamasında hello Azure Portal gidin ve üzerinde hello tıklatın **ayarları** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-167">Browse tooyour web app in hello Azure Portal and click on hello **Settings** button.</span></span>
   
    ![Web uygulaması ayarları][settings-button]
5. <span data-ttu-id="4ba3e-169">Merhaba gelen **ayarları** dikey seçin **uygulama ayarları** ve toohello kaydırma **uygulama ayarları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-169">From hello **Settings** blade select **Application Settings** and scroll toohello **App settings** section.</span></span>
6. <span data-ttu-id="4ba3e-170">Merhaba, **uygulama ayarları** bölümünde, oluşturmak bir **php_extensıons** anahtarı.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-170">In hello **App settings** section, create a **PHP_EXTENSIONS** key.</span></span> <span data-ttu-id="4ba3e-171">Bu anahtar için Hello değeri bir yolu göreli toowebsite kök olacaktır: **bin\your ext dosya**.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-171">hello value for this key would be a path relative toowebsite root: **bin\your-ext-file**.</span></span>
   
    ![Uygulama ayarları uzantı etkinleştirilemedi][php-extensions]
7. <span data-ttu-id="4ba3e-173">Merhaba tıklatın **kaydetmek** düğmesi hello hello üstündeki **Web uygulaması ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-173">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Yapılandırma ayarlarını Kaydet][save-button]

<span data-ttu-id="4ba3e-175">Zend uzantıları de desteklenir kullanarak bir **PHP_ZENDEXTENSIONS** anahtarı.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-175">Zend extensions are also supported by using a **PHP_ZENDEXTENSIONS** key.</span></span> <span data-ttu-id="4ba3e-176">tooenable birden çok uzantı içeren virgülle ayrılmış bir listesini `.dll` hello uygulama ayarının değeri için dosyaları.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-176">tooenable multiple extensions, include a comma-separated list of `.dll` files for hello app setting value.</span></span>

## <a name="how-to-use-a-custom-php-runtime"></a><span data-ttu-id="4ba3e-177">Nasıl yapılır: özel bir PHP çalışma zamanı kullanın</span><span class="sxs-lookup"><span data-stu-id="4ba3e-177">How to: Use a custom PHP runtime</span></span>
<span data-ttu-id="4ba3e-178">Merhaba varsayılan PHP Çalışma Zamanı Modülü yerine, PHP komut dosyalarının tooexecute sağlayan bir PHP çalışma zamanı App Service Web Apps kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-178">Instead of hello default PHP runtime, App Service Web Apps can use a PHP runtime that you provide tooexecute PHP scripts.</span></span> <span data-ttu-id="4ba3e-179">Sağladığınız hello çalışma zamanı tarafından yapılandırılabilir bir `php.ini` de belirtmeniz dosya.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-179">hello runtime that you provide can be configured by a `php.ini` file that you also provide.</span></span> <span data-ttu-id="4ba3e-180">toouse özel bir PHP çalışma zamanı Web uygulamalarıyla hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-180">toouse a custom PHP runtime with Web Apps, follow hello steps below.</span></span>

1. <span data-ttu-id="4ba3e-181">Bir iş parçacığı güvenli, VC9 veya VC11 uyumlu PHP için Windows sürümü edinin.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-181">Obtain a non-thread-safe, VC9 or VC11 compatible version of PHP for Windows.</span></span> <span data-ttu-id="4ba3e-182">Windows için PHP'nin en son sürümleri şurada bulunabilir: [http://windows.php.net/download/].</span><span class="sxs-lookup"><span data-stu-id="4ba3e-182">Recent releases of PHP for Windows can be found here: [http://windows.php.net/download/].</span></span> <span data-ttu-id="4ba3e-183">Eski sürümleri burada hello arşivindeki bulunabilir: [http://windows.php.net/downloads/releases/archives/].</span><span class="sxs-lookup"><span data-stu-id="4ba3e-183">Older releases can be found in hello archive here: [http://windows.php.net/downloads/releases/archives/].</span></span>
2. <span data-ttu-id="4ba3e-184">Merhaba değiştirme `php.ini` dosya, çalışma zamanı için.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-184">Modify hello `php.ini` file for your runtime.</span></span> <span data-ttu-id="4ba3e-185">Sistem düzeyinde-yalnızca yönergeleri yapılandırma ayarları Web uygulamaları tarafından yoksayılacak unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-185">Note that any configuration settings that are system-level-only directives will be ignored by Web Apps.</span></span> <span data-ttu-id="4ba3e-186">(Sistem düzeyinde-yalnızca yönergeleri hakkında daha fazla bilgi için bkz: [php.ini yönergeleri listesi]).</span><span class="sxs-lookup"><span data-stu-id="4ba3e-186">(For information about system-level-only directives, see [List of php.ini directives]).</span></span>
3. <span data-ttu-id="4ba3e-187">İsteğe bağlı olarak, uzantıları tooyour PHP çalışma zamanı ekleyin ve bunları hello etkinleştirmek `php.ini` dosya.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-187">Optionally, add extensions tooyour PHP runtime and enable them in hello `php.ini` file.</span></span>
4. <span data-ttu-id="4ba3e-188">Ekleme bir `bin` tooyour kök dizin ve, PHP çalışma zamanı da içeren put hello dizin (örneğin, `bin\php`).</span><span class="sxs-lookup"><span data-stu-id="4ba3e-188">Add a `bin` directory tooyour root directory, and put hello directory that contains your PHP runtime in it (for example, `bin\php`).</span></span>
5. <span data-ttu-id="4ba3e-189">Web uygulamanızı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-189">Deploy your web app.</span></span>
6. <span data-ttu-id="4ba3e-190">Tooyour web uygulamasında hello Azure Portal gidin ve üzerinde hello tıklatın **ayarları** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-190">Browse tooyour web app in hello Azure Portal and click on hello **Settings** button.</span></span>
   
    ![Web uygulaması ayarları][settings-button]
7. <span data-ttu-id="4ba3e-192">Merhaba gelen **ayarları** dikey seçin **uygulama ayarları** ve toohello kaydırma **işleyici eşlemeleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-192">From hello **Settings** blade select **Application Settings** and scroll toohello **Handler mappings** section.</span></span> <span data-ttu-id="4ba3e-193">Ekleme `*.php` toohello uzantısı alan ve hello yolu toohello ekleyin `php-cgi.exe` yürütülebilir.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-193">Add `*.php` toohello Extension field and add hello path toohello `php-cgi.exe` executable.</span></span> <span data-ttu-id="4ba3e-194">PHP çalışma zamanı hello yerleştirirseniz `bin` , uygulamanın hello kök dizininde, hello yolu olacaktır `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-194">If you put your PHP runtime in hello `bin` directory in hello root of you application, hello path will be `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span></span>
   
    ![İşleyici eşlemeleri işleyici belirtin][handler-mappings]
8. <span data-ttu-id="4ba3e-196">Merhaba tıklatın **kaydetmek** düğmesi hello hello üstündeki **Web uygulaması ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-196">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Yapılandırma ayarlarını Kaydet][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a><span data-ttu-id="4ba3e-198">Nasıl yapılır: Azure içinde Oluşturucu Otomasyonu</span><span class="sxs-lookup"><span data-stu-id="4ba3e-198">How to: Enable Composer automation in Azure</span></span>
<span data-ttu-id="4ba3e-199">PHP projeniz varsa varsayılan olarak, uygulama hizmeti ile composer.json, hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-199">By default, App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="4ba3e-200">Kullanırsanız [Git dağıtımı](app-service-deploy-local-git.md), sırasında işleme composer.json etkinleştirebilirsiniz `git push` hello Composer uzantısını etkinleştirerek.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-200">If you use [Git deployment](app-service-deploy-local-git.md), you can enable composer.json processing during `git push` by enabling hello Composer extension.</span></span>

> [!NOTE]
> <span data-ttu-id="4ba3e-201">Yapabilecekleriniz [birinci sınıf oluşturucu desteği için uygulama hizmeti burada oy](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span><span class="sxs-lookup"><span data-stu-id="4ba3e-201">You can [vote for first-class Composer support in App Service here](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span></span>
> 
> 

1. <span data-ttu-id="4ba3e-202">PHP ile web uygulamanızın dikey penceresinde hello [Azure portal](https://portal.azure.com), tıklatın **Araçları** > **uzantıları**.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-202">In your PHP web app's blade in hello [Azure portal](https://portal.azure.com), click **Tools** > **Extensions**.</span></span>
   
    ![Azure Portal ayarları dikey tooenable Azure Otomasyonu'nda Oluşturucusu](./media/web-sites-php-configure/composer-extension-settings.png)
2. <span data-ttu-id="4ba3e-204">Tıklatın **Ekle**, ardından **Oluşturucu**.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-204">Click **Add**, then click **Composer**.</span></span>
   
    ![Azure'da Composer uzantısını tooenable Oluşturucu Otomasyonu ekleyin](./media/web-sites-php-configure/composer-extension-add.png)
3. <span data-ttu-id="4ba3e-206">Tıklatın **Tamam** tooaccept yasal koşulları.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-206">Click **OK** tooaccept legal terms.</span></span> <span data-ttu-id="4ba3e-207">Tıklatın **Tamam** yeniden tooadd hello uzantısı.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-207">Click **OK** again tooadd hello extension.</span></span>
   
    <span data-ttu-id="4ba3e-208">Merhaba **yüklü uzantıları** dikey şimdi hello Composer uzantısını göster.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-208">hello **Installed extensions** blade will now show hello Composer extension.</span></span>  
    <span data-ttu-id="4ba3e-209">![Yasal koşullar tooenable Oluşturucu Azure Otomasyonu'nda kabul et](./media/web-sites-php-configure/composer-extension-view.png)</span><span class="sxs-lookup"><span data-stu-id="4ba3e-209">![Accept legal terms tooenable Composer automation in Azure](./media/web-sites-php-configure/composer-extension-view.png)</span></span>
4. <span data-ttu-id="4ba3e-210">Şimdi, gerçekleştirmek `git add`, `git commit`, ve `git push` hello önceki bölümde ister.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-210">Now, perform `git add`, `git commit`, and `git push` like in hello previous section.</span></span> <span data-ttu-id="4ba3e-211">Oluşturucu composer.json içinde tanımlanan bağımlılıklar yüklüyor şimdi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-211">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Azure Otomasyonu'nda Oluşturucusu ile Git dağıtımı](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a><span data-ttu-id="4ba3e-213">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4ba3e-213">Next steps</span></span>
<span data-ttu-id="4ba3e-214">Daha fazla bilgi için bkz: Merhaba [PHP Geliştirici Merkezi](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="4ba3e-214">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

> [!NOTE]
> <span data-ttu-id="4ba3e-215">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-215">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="4ba3e-216">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="4ba3e-216">No credit cards required; no commitments.</span></span>
> 
> 

[ücretsiz deneme sürümü]: https://www.windowsazure.com/pricing/free-trial/
[phpinfo()]: http://php.net/manual/en/function.phpinfo.php
[select-php-version]: ./media/web-sites-php-configure/select-php-version.png
[php.ini yönergeleri listesi]: http://www.php.net/manual/en/ini.list.php
[. user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php
[ini_set()]: http://www.php.net/manual/en/function.ini-set.php
[application-settings]: ./media/web-sites-php-configure/application-settings.png
[settings-button]: ./media/web-sites-php-configure/settings-button.png
[save-button]: ./media/web-sites-php-configure/save-button.png
[php-extensions]: ./media/web-sites-php-configure/php-extensions.png
[handler-mappings]: ./media/web-sites-php-configure/handler-mappings.png
[http://windows.php.net/download/]: http://windows.php.net/download/
[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/
[SETPHPVERCLI]: ./media/web-sites-php-configure/ChangePHPVersion-XPlatCLI.png
[GETPHPVERCLI]: ./media/web-sites-php-configure/ShowPHPVersion-XplatCLI.png
[SETPHPVERPS]: ./media/web-sites-php-configure/ChangePHPVersion-PS.png
[GETPHPVERPS]: ./media/web-sites-php-configure/ShowPHPVersion-PS.png

