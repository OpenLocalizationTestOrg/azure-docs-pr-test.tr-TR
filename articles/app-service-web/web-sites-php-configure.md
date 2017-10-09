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
# <a name="configure-php-in-azure-app-service-web-apps"></a>Azure App Service Web Apps PHP yapılandırma
## <a name="introduction"></a>Giriş
Bu kılavuz size nasıl tooconfigure hello yerleşik PHP çalışma zamanı Web uygulamalarının gösterir [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), özel bir PHP çalışma zamanı sağlamak ve uzantılarını etkinleştirme. Uygulama hizmeti toouse hello için kaydolun [ücretsiz deneme sürümü]. tooget hello en bu Rehberde, önce bir PHP web uygulaması App Service'te oluşturmanız gerekir.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-hello-built-in-php-version"></a>Nasıl yapılır: değişiklik hello yerleşik PHP sürümü
Bir App Service web uygulaması oluşturduğunuzda varsayılan olarak, PHP 5.5 yüklü ve kullanmak için hemen kullanılabilir durumdadır. Merhaba en iyi şekilde toosee hello kullanılabilir sürüm düzeltme, varsayılan yapılandırmasıyla ve hello etkin uzantıları olan toodeploy hello çağıran bir komut dosyası [phpinfo()] işlevi.

PHP 5.6 ve PHP 7.0 sürümleri de kullanılabilir, ancak varsayılan olarak etkin değildir. tooupdate hello PHP sürümünü, bu yöntemlerden birini izleyin:

### <a name="azure-portal"></a>Azure Portal
1. Merhaba tooyour web uygulamasında Gözat [Azure Portal](https://portal.azure.com) üzerinde hello tıklatıp **ayarları** düğmesi.
   
    ![Web uygulaması ayarları][settings-button]
2. Merhaba gelen **ayarları** dikey seçin **uygulama ayarları** ve hello yeni PHP sürümünü seçin.
   
    ![Uygulama ayarları][application-settings]
3. Merhaba tıklatın **kaydetmek** düğmesi hello hello üstündeki **Web uygulaması ayarları** dikey.
   
    ![Yapılandırma ayarlarını Kaydet][save-button]

### <a name="azure-powershell-windows"></a>Azure PowerShell'i (Windows)
1. Azure PowerShell ve oturum açma tooyour hesap açın:
   
        PS C:\> Login-AzureRmAccount
2. Merhaba web uygulaması için Hello PHP sürümünü ayarlayın.
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. Merhaba PHP sürümünü şimdi ayarlayın. Bu ayarları doğrulayabilirsiniz:
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a>Azure komut satırı arabirimi (Linux, Mac, Windows)
toouse Merhaba Azure komut satırı arabirimi, sahip olmanız gerekir **Node.js** bilgisayarınızda yüklü.

1. Terminali açın ve oturum açma tooyour hesabı.
   
        azure login
2. Merhaba web uygulaması için Hello PHP sürümünü ayarlayın.
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. Merhaba PHP sürümünü şimdi ayarlayın. Bu ayarları doğrulayabilirsiniz:
   
        azure site show {app-name}

> [!NOTE] 
> Merhaba [Azure CLI 2.0](https://github.com/Azure/azure-cli) eşdeğer toohello yukarıdaki komutları şunlardır:
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-hello-built-in-php-configurations"></a>Nasıl yapılır: hello yerleşik PHP yapılandırmalarını değiştirme
Tüm yerleşik PHP çalışma zamanı için hello yapılandırma seçeneklerinden herhangi birini hello adımları izleyerek değiştirebilirsiniz. (Php.ini yönergeleri hakkında daha fazla bilgi için bkz: [php.ini yönergeleri listesi].)

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a>PHP değiştirme\_ını\_kullanıcı, PHP\_ını\_PERDIR, PHP\_ını\_tüm yapılandırma ayarları
1. Ekleme bir [. user.ini] dosyası tooyour kök dizini.
2. Yapılandırma ayarları toohello ekleme `.user.ini` kullanarak dosya hello içinde kullandığınız aynı sözdizimini bir `php.ini` dosyası. Örneğin, tooturn hello istediyseniz `display_errors` ayarı ve ayarlamayı `upload_max_filesize` too10M, ayarlama, `.user.ini` dosyası bu metin içerebilir:
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on toowrite errors tood:\home\LogFiles\php_errors.log
        ; log_errors=On
3. Web uygulamanızı dağıtın.
4. Merhaba web uygulaması yeniden başlatın. (Yeniden başlatma gereklidir çünkü hangi PHP hello sıklığı okur `.user.ini` dosyaları hello tarafından yönetilir `user_ini.cache_ttl` sistem düzeyi ayarı ve 300 saniye (5 dakika) varsayılan ayarı. Yeniden başlatma hello web uygulaması zorlar PHP tooread hello yeni ayarlarında hello `.user.ini` dosyası.)

Bir alternatif toousing olarak bir `.user.ini` dosyası hello kullanabilirsiniz [ini_set()] işlevinde, sistem düzeyinde yönergeleri olmayan betikleri tooset yapılandırma seçenekleri.

### <a name="changing-phpinisystem-configuration-settings"></a>PHP değiştirme\_ını\_sistemi yapılandırma ayarları
1. Web uygulaması hello anahtara sahip bir uygulama ayarı tooyour eklemek `PHP_INI_SCAN_DIR` ve değeri`d:\home\site\ini`
2. Oluşturma bir `settings.ini` Kudu konsolunu kullanarak dosya (http://&lt;site adı&gt;. scm.azurewebsite.net) hello içinde `d:\home\site\ini` dizin.
3. Yapılandırma ayarları toohello eklemek `settings.ini` kullanarak dosya hello aynı sözdizimini kullanan bir php.ini dosyası. Örneğin, toopoint hello istediyseniz `curl.cainfo` tooa ayarlama `*.crt` dosyası ve 'too512K, ayarı wincache.maxfilesize' ayarlayın, `settings.ini` dosyası bu metin içerebilir:
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. Web uygulaması tooload hello değişikliklerinizi yeniden başlatın.

## <a name="how-to-enable-extensions-in-hello-default-php-runtime"></a>Nasıl yapılır: hello varsayılan PHP çalışma zamanında eklentilerini etkinleştir
Merhaba önceki bölümde, hello en iyi şekilde toosee hello varsayılan PHP sürümü, varsayılan yapılandırma ve etkin hello belirtildiği gibi uzantıları olan toodeploy çağıran bir komut dosyası [phpinfo()]. tooenable ek uzantıları hello adımları izleyin:

### <a name="configure-via-ini-settings"></a>Aracılığıyla INI ayarlarını yapılandırma
1. Ekleme bir `ext` directory toohello `d:\home\site` dizini.
2. PUT `.dll` hello uzantısı dosyalarında `ext` dizin (örneğin, `php_xdebug.dll`). Merhaba uzantıları olan VC9 ve iş parçacığı güvenli olmayan (nts) uyumlu ve PHP, varsayılan sürümü ile uyumlu olduğundan emin olun.
3. Web uygulaması hello anahtara sahip bir uygulama ayarı tooyour eklemek `PHP_INI_SCAN_DIR` ve değeri`d:\home\site\ini`
4. Oluşturma bir `ini` dosyasını `d:\home\site\ini` adlı `extensions.ini`.
5. Yapılandırma ayarları toohello eklemek `extensions.ini` kullanarak dosya hello aynı sözdizimini kullanan bir php.ini dosyası. Örneğin, MongoDB ve XDebug tooenable hello uzantıları, istediyseniz, `extensions.ini` bu metin dosyasını içerebilir:
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. Web uygulaması tooload hello değişikliklerinizi yeniden başlatın.

### <a name="configure-via-app-setting"></a>Uygulama ayarı aracılığıyla yapılandırın
1. Ekleme bir `bin` toohello kök dizin.
2. PUT `.dll` hello uzantısı dosyalarında `bin` dizin (örneğin, `php_xdebug.dll`). Merhaba uzantıları olan VC9 ve iş parçacığı güvenli olmayan (nts) uyumlu ve PHP, varsayılan sürümü ile uyumlu olduğundan emin olun.
3. Web uygulamanızı dağıtın.
4. Tooyour web uygulamasında hello Azure Portal gidin ve üzerinde hello tıklatın **ayarları** düğmesi.
   
    ![Web uygulaması ayarları][settings-button]
5. Merhaba gelen **ayarları** dikey seçin **uygulama ayarları** ve toohello kaydırma **uygulama ayarları** bölümü.
6. Merhaba, **uygulama ayarları** bölümünde, oluşturmak bir **php_extensıons** anahtarı. Bu anahtar için Hello değeri bir yolu göreli toowebsite kök olacaktır: **bin\your ext dosya**.
   
    ![Uygulama ayarları uzantı etkinleştirilemedi][php-extensions]
7. Merhaba tıklatın **kaydetmek** düğmesi hello hello üstündeki **Web uygulaması ayarları** dikey.
   
    ![Yapılandırma ayarlarını Kaydet][save-button]

Zend uzantıları de desteklenir kullanarak bir **PHP_ZENDEXTENSIONS** anahtarı. tooenable birden çok uzantı içeren virgülle ayrılmış bir listesini `.dll` hello uygulama ayarının değeri için dosyaları.

## <a name="how-to-use-a-custom-php-runtime"></a>Nasıl yapılır: özel bir PHP çalışma zamanı kullanın
Merhaba varsayılan PHP Çalışma Zamanı Modülü yerine, PHP komut dosyalarının tooexecute sağlayan bir PHP çalışma zamanı App Service Web Apps kullanabilirsiniz. Sağladığınız hello çalışma zamanı tarafından yapılandırılabilir bir `php.ini` de belirtmeniz dosya. toouse özel bir PHP çalışma zamanı Web uygulamalarıyla hello adımları izleyin.

1. Bir iş parçacığı güvenli, VC9 veya VC11 uyumlu PHP için Windows sürümü edinin. Windows için PHP'nin en son sürümleri şurada bulunabilir: [http://windows.php.net/download/]. Eski sürümleri burada hello arşivindeki bulunabilir: [http://windows.php.net/downloads/releases/archives/].
2. Merhaba değiştirme `php.ini` dosya, çalışma zamanı için. Sistem düzeyinde-yalnızca yönergeleri yapılandırma ayarları Web uygulamaları tarafından yoksayılacak unutmayın. (Sistem düzeyinde-yalnızca yönergeleri hakkında daha fazla bilgi için bkz: [php.ini yönergeleri listesi]).
3. İsteğe bağlı olarak, uzantıları tooyour PHP çalışma zamanı ekleyin ve bunları hello etkinleştirmek `php.ini` dosya.
4. Ekleme bir `bin` tooyour kök dizin ve, PHP çalışma zamanı da içeren put hello dizin (örneğin, `bin\php`).
5. Web uygulamanızı dağıtın.
6. Tooyour web uygulamasında hello Azure Portal gidin ve üzerinde hello tıklatın **ayarları** düğmesi.
   
    ![Web uygulaması ayarları][settings-button]
7. Merhaba gelen **ayarları** dikey seçin **uygulama ayarları** ve toohello kaydırma **işleyici eşlemeleri** bölümü. Ekleme `*.php` toohello uzantısı alan ve hello yolu toohello ekleyin `php-cgi.exe` yürütülebilir. PHP çalışma zamanı hello yerleştirirseniz `bin` , uygulamanın hello kök dizininde, hello yolu olacaktır `D:\home\site\wwwroot\bin\php\php-cgi.exe`.
   
    ![İşleyici eşlemeleri işleyici belirtin][handler-mappings]
8. Merhaba tıklatın **kaydetmek** düğmesi hello hello üstündeki **Web uygulaması ayarları** dikey.
   
    ![Yapılandırma ayarlarını Kaydet][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a>Nasıl yapılır: Azure içinde Oluşturucu Otomasyonu
PHP projeniz varsa varsayılan olarak, uygulama hizmeti ile composer.json, hiçbir şey yapmaz. Kullanırsanız [Git dağıtımı](app-service-deploy-local-git.md), sırasında işleme composer.json etkinleştirebilirsiniz `git push` hello Composer uzantısını etkinleştirerek.

> [!NOTE]
> Yapabilecekleriniz [birinci sınıf oluşturucu desteği için uygulama hizmeti burada oy](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!
> 
> 

1. PHP ile web uygulamanızın dikey penceresinde hello [Azure portal](https://portal.azure.com), tıklatın **Araçları** > **uzantıları**.
   
    ![Azure Portal ayarları dikey tooenable Azure Otomasyonu'nda Oluşturucusu](./media/web-sites-php-configure/composer-extension-settings.png)
2. Tıklatın **Ekle**, ardından **Oluşturucu**.
   
    ![Azure'da Composer uzantısını tooenable Oluşturucu Otomasyonu ekleyin](./media/web-sites-php-configure/composer-extension-add.png)
3. Tıklatın **Tamam** tooaccept yasal koşulları. Tıklatın **Tamam** yeniden tooadd hello uzantısı.
   
    Merhaba **yüklü uzantıları** dikey şimdi hello Composer uzantısını göster.  
    ![Yasal koşullar tooenable Oluşturucu Azure Otomasyonu'nda kabul et](./media/web-sites-php-configure/composer-extension-view.png)
4. Şimdi, gerçekleştirmek `git add`, `git commit`, ve `git push` hello önceki bölümde ister. Oluşturucu composer.json içinde tanımlanan bağımlılıklar yüklüyor şimdi görürsünüz.
   
    ![Azure Otomasyonu'nda Oluşturucusu ile Git dağıtımı](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için bkz: Merhaba [PHP Geliştirici Merkezi](/develop/php/).

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
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

