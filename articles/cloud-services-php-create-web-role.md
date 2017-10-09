---
title: "aaaCreate Azure PHP için web ve çalışan rolleri | Microsoft Docs"
description: "Bir kılavuzu toocreating PHP web ve çalışan rolleri bir Azure bulut hizmeti ve yapılandırma hello PHP çalışma zamanı."
services: 
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9f7ccda0-bd96-4f7b-a7af-fb279a9e975b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 04a6e8c9c379cb0f854645941b6bc7d614bb91f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-php-web-and-worker-roles"></a>Nasıl toocreate PHP web ve çalışan rolleri
## <a name="overview"></a>Genel Bakış
Bu kılavuz size nasıl toocreate PHP web veya çalışan rolleri Windows geliştirme ortamında, PHP belirli bir sürümünü hello kullanılabilir "yerleşik" sürümlerini seçin, hello PHP yapılandırmasını değiştirmek, uzantılarını etkinleştirme ve son olarak, tooAzure dağıtmak gösterir. Ayrıca açıklanır nasıl tooconfigure bir web veya çalışan rolü toouse sağlayan bir PHP çalışma zamanı (özel yapılandırma ve birlikte uzantıları).

## <a name="what-are-php-web-and-worker-roles"></a>PHP web ve çalışan rolleri nelerdir?
Azure sağlayan üç işlem çalışan uygulamalar için modeli: Azure App Service, Azure sanal makineler ve Azure Cloud Services. Üç modeli PHP destekler. Web ve çalışan rolleri içerir, bulut hizmetleri sağlar *(PaaS) hizmet olarak platform*. Bir bulut hizmetinde bir web rolü adanmış bir Internet Information Services (IIS) web sunucusu toohost ön uç web uygulamaları sağlar. Çalışan rolü kullanıcı etkileşimi ve girişinden bağımsız zaman uyumsuz, uzun süre çalışan veya kalıcı görevleri çalıştırabilir.

Bu seçenekler hakkında daha fazla bilgi için bkz: [Azure tarafından sağlanan seçenekleri barındırma işlem](cloud-services/cloud-services-choose-me.md).

## <a name="download-hello-azure-sdk-for-php"></a>PHP için Hello Azure SDK'sını indirme
Merhaba [PHP için Azure SDK] birçok bileşenden oluşur. Bu makalede iki tanesi kullanır: Azure PowerShell ve Azure öykünücüsünü hello. Bu iki bileşenin hello Microsoft Web Platformu yükleyicisi yüklenebilir. Daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

## <a name="create-a-cloud-services-project"></a>Bulut Hizmetleri projesi oluşturma
bir PHP web veya çalışan rolü oluşturma hello ilk adımı toocreate bir Azure hizmeti projesi oluşturur. bir Azure hizmeti projesi web ve çalışan rolleri için mantıksal bir kapsayıcı görevi görür ve hello projenin içeren [hizmet açıklaması (.csdef)] ve [hizmet yapılandırma (.cscfg)] dosyaları.

toocreate yeni bir Azure hizmet projesi Azure PowerShell'i yönetici olarak çalıştırın ve hello aşağıdaki komutu yürütün:

    PS C:\>New-AzureServiceProject myProject

Bu komut yeni bir dizin oluşturur (`myProject`) toowhich web ve çalışan rolleri ekleyebilirsiniz.

## <a name="add-php-web-or-worker-roles"></a>PHP web veya çalışan rolleri Ekle
bir PHP web rolü tooa projesi tooadd komuttan hello projenin kök dizini içinde aşağıdaki hello çalıştırın:

    PS C:\myProject> Add-AzurePHPWebRole roleName

Çalışan rolü için bu komutu kullanın:

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> Merhaba `roleName` parametresi isteğe bağlıdır. Belirtilmezse, hello rol adı otomatik olarak oluşturulur. oluşturulan hello ilk web rolü olacaktır `WebRole1`, hello ikinci olacaktır `WebRole2`ve benzeri. oluşturulan hello ilk çalışan rolü olacaktır `WorkerRole1`, hello ikinci olacaktır `WorkerRole2`ve benzeri.
>
>

## <a name="specify-hello-built-in-php-version"></a>Merhaba yerleşik PHP sürümünü belirtin
Bir PHP web veya çalışan rolü tooa proje eklediğinizde, böylece her uygulamanızın web veya çalışan örneği üzerinde dağıtıldığında PHP yüklenecek hello projenin yapılandırma dosyalarını değiştirilir. komutu aşağıdaki hello çalıştırmak varsayılan olarak, yüklenecek PHP toosee hello sürümü:

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

Merhaba yukarıdaki hello komut çıktısı şuna benzer toowhat aşağıda gösterilmektedir. Bu örnekte, hello `IsDefault` bayrağı çok ayarlanır`true` hello varsayılan PHP sürümü yüklü olacağını belirten php 5.3.17,.

```
Runtime Version     PackageUri                      IsDefault
------- -------     ----------                      ---------
Node 0.6.17         http://nodertncu.blob.core...   False
Node 0.6.20         http://nodertncu.blob.core...   True
Node 0.8.4          http://nodertncu.blob.core...   False
IISNode 0.1.21      http://nodertncu.blob.core...   True
Cache 1.8.0         http://nodertncu.blob.core...   True
PHP 5.3.17          http://nodertncu.blob.core...   True
PHP 5.4.0           http://nodertncu.blob.core...   False
```

Merhaba PHP çalışma zamanı sürümü tooany listelenen hello PHP sürümlerinin ayarlayabilirsiniz. Örneğin, tooset hello PHP sürümünü (Merhaba ada sahip bir rol için `roleName`) too5.4.0, komutu aşağıdaki kullanım hello:

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> Kullanılabilir PHP sürümlerin hello gelecekteki değişebilir.
>
>

## <a name="customize-hello-built-in-php-runtime"></a>Merhaba yerleşik PHP çalışma zamanı özelleştirme
Yukarıdaki değiştirilmesini dahil olmak üzere hello adımları izlediğinizde yüklü hello PHP çalışma zamanı hello yapılandırmasını üzerinde tam denetime sahip `php.ini` ayarları ve uzantılarını etkinleştirme.

toocustomize yerleşik PHP çalışma zamanı Merhaba, şu adımları izleyin:

1. Adlı yeni bir klasör ekleyin `php`, toohello `bin` web rolünüz dizininde. Çalışan rolü için toohello rolün kök dizin ekleyin.
2. Merhaba, `php` klasörünü adlı başka bir klasör oluşturun `ext`. Herhangi bir yerleştirme `.dll` uzantısı dosyaları (örn., `php_mongo.dll`) bu klasörde tooenable istiyor.
3. Ekleme bir `php.ini` toohello dosya `php` klasör. Tüm özel uzantılar etkinleştirin ve bu dosyadaki tüm PHP yönergeleri ayarlayın. Örneğin, tooturn istediyseniz `display_errors` üzerinde ve hello etkinleştirmek `php_mongo.dll` uzantısı, Merhaba içeriğine, `php.ini` dosya şu şekilde olacaktır:

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> Hello açıkça ayarlamazsanız herhangi bir ayarı `php.ini` otomatik olarak sağlamak dosya tootheir varsayılan değerleri ayarlanabilir. Ancak, bir tam ekleyebilirsiniz göz önünde bulundurmanız `php.ini` dosya.
>
>

## <a name="use-your-own-php-runtime"></a>Kendi PHP çalışma zamanı kullanın
Yerleşik bir PHP çalışma zamanı seçme ve yukarıda açıklandığı gibi yapılandırma yerine bazı durumlarda, kendi PHP çalışma zamanı tooprovide isteyebilirsiniz. Örneğin, kullanabileceğiniz hello geliştirme ortamınızı kullandığınız web veya çalışan rolü aynı PHP çalışma zamanı. Bu, daha kolay tooensure Merhaba uygulaması üretim ortamınızda davranış değişmez kolaylaştırır.

### <a name="configure-a-web-role-toouse-your-own-php-runtime"></a>Bir web rolü toouse kendi PHP çalışma zamanı yapılandırma
tooconfigure bir web rolü toouse sağlarsanız, PHP çalışma zamanı şu adımları izleyin:

1. Bir Azure hizmeti projesi oluşturun ve bu konuda daha önce açıklandığı gibi bir PHP web rolü ekleyin.
2. Oluşturma bir `php` hello klasöründe `bin` web rolün kök dizininde bulunan ve PHP çalışma zamanı (tüm ikili dosyaları, yapılandırma dosyalarını, alt klasörler, vb.) toohello eklemek klasör `php` klasör.
3. (İSTEĞE BAĞLI) Merhaba, PHP çalışma zamanı kullanıyorsa, [SQL Server için PHP için Microsoft Drivers][sqlsrv drivers], web rolü tooinstall tooconfigure gerekir [SQL Server Native Client 2012] [ sql native client] , ne zaman hazırlanır. toodo bunu hello eklemek [sqlncli.msi x64 yükleyici] toohello `bin` web rolün kök dizininde klasör. Merhaba rol sağlandığında hello sonraki adımda açıklanan hello başlangıç betiği sessizce hello yükleyiciyi çalıştırın. PHP çalışma zamanı, SQL Server için PHP için hello Microsoft Drivers kullanmıyorsa, hello sonraki adımda gösterilen hello komut satırı yükseltmesinin hello kaldırabilirsiniz:

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. Yapılandırır bir başlangıç görevi tanımlamak [Internet Information Services (IIS)] [ iis.net] , PHP çalışma zamanı toohandle istekleri için toouse `.php` sayfaları. toodo Bu, açık hello `setup_web.cmd` dosya (Merhaba içinde `bin` web rolün kök dizin dosyası) bir metin Düzenleyicisi'ni ve içeriğini ile Merhaba komut dosyasını değiştirin:

    ```cmd
    @ECHO ON
    cd "%~dp0"

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    SET PHP_FULL_PATH=%~dp0php\php-cgi.exe
    SET NEW_PATH=%PATH%;%RoleRoot%\base\x86

    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%',maxInstances='12',idleTimeout='60000',activityTimeout='3600',requestTimeout='60000',instanceMaxRequests='10000',protocol='NamedPipe',flushNamedPipe='False']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PATH',value='%NEW_PATH%']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PHP_FCGI_MAX_REQUESTS',value='10000']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/handlers /+"[name='PHP',path='*.php',verb='GET,HEAD,POST',modules='FastCgiModule',scriptProcessor='%PHP_FULL_PATH%',resourceType='Either',requireAccess='Script']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /"[fullPath='%PHP_FULL_PATH%'].queueLength:50000"
    ```
5. Uygulama dosyaları tooyour web rolünüz ait kök dizine ekleyin. Bu hello web sunucusunun kök dizininde olacaktır.
6. Uygulamanız yayımlama hello açıklandığı gibi [uygulamanızı yayımlamak](#publish-your-application) bölümüne bakın.

> [!NOTE]
> Merhaba `download.ps1` komut dosyası (Merhaba içinde `bin` hello web rolün kök dizininin klasör), kendi PHP çalışma zamanı kullanmak için yukarıda açıklanan başlangıç adımları izledikten sonra silinebilir.
>
>

### <a name="configure-a-worker-role-toouse-your-own-php-runtime"></a>Çalışan rolü toouse kendi PHP çalışma zamanı yapılandırma
tooconfigure çalışan rolü toouse sağlarsanız, PHP çalışma zamanı şu adımları izleyin:

1. Bir Azure hizmeti projesi oluşturun ve bu konuda daha önce açıklandığı gibi PHP çalışan rolü ekleyin.
2. Oluşturma bir `php` hello çalışan rolün kök dizini klasöründe ve ardından, PHP çalışma zamanı (tüm ikili dosyaları, yapılandırma dosyalarını, alt klasörler, vb.) toohello ekleyin `php` klasör.
3. (İSTEĞE BAĞLI) PHP çalışma zamanı kullanıyorsa [SQL Server için PHP için Microsoft Drivers][sqlsrv drivers], çalışan rolü tooinstall tooconfigure gerekir [SQL Server Native Client 2012] [ sql native client] , ne zaman hazırlanır. toodo bunu hello eklemek [sqlncli.msi x64 yükleyici] toohello çalışan rolün kök dizini. Merhaba rol sağlandığında hello sonraki adımda açıklanan hello başlangıç betiği sessizce hello yükleyiciyi çalıştırın. PHP çalışma zamanı, SQL Server için PHP için hello Microsoft Drivers kullanmıyorsa, hello sonraki adımda gösterilen hello komut satırı yükseltmesinin hello kaldırabilirsiniz:

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. Ekler bir başlangıç görevi tanımlamak, `php.exe` hello rol sağlandığında yürütülebilir toohello çalışan rolün PATH ortam değişkeni. toodo Bu, açık hello `setup_worker.cmd` (Merhaba çalışan rolün kök dizininde) bir metin Düzenleyicisi'nde dosya ve içeriğinin komut dosyası izleyen hello ile değiştirin:

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service toohello web root directory...
    icacls ..\ /grant "Network Service":(OI)(CI)W
    if %ERRORLEVEL% neq 0 goto error
    echo OK

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    setx Path "%PATH%;%~dp0php" /M

    if %ERRORLEVEL% neq 0 goto error

    echo SUCCESS
    exit /b 0

    :error

    echo FAILED
    exit /b -1
    ```
5. Uygulama dosyaları tooyour çalışan rolünüzün ait kök dizine ekleyin.
6. Uygulamanız yayımlama hello açıklandığı gibi [uygulamanızı yayımlamak](#publish-your-application) bölümüne bakın.

## <a name="run-your-application-in-hello-compute-and-storage-emulators"></a>İşlem ve depolama öykünücüsünü hello uygulamanızı çalıştırma
Hello Azure öykünücüsünü toohello bulut dağıtmadan önce Azure uygulamanızı sınayabilir yerel bir ortam sağlar. Merhaba Öykünücüler ve hello Azure ortamı arasındaki bazı farklar vardır. Bu daha iyi görmek toounderstand [geliştirme ve test amacıyla hello Azure storage öykünücüsünü kullanma](storage/common/storage-use-emulator.md).

PHP olmalıdır Not toouse hello işlem öykünücüsü yerel olarak yüklü. Merhaba işlem öykünücüsü, yerel PHP yükleme toorun uygulamanızı kullanır.

Merhaba Öykünücüler projenizde toorun yürütme hello projenizin kök dizinin komutu aşağıdaki:

    PS C:\MyProject> Start-AzureEmulator

Çıktı benzer toothis görürsünüz:

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

Web tarayıcısında açarak ve toohello yerel adres hello çıktıda gösterilen gözatma hello öykünücüsünde çalıştıran uygulamanız görebilirsiniz (`http://127.0.0.1:81` hello örnek çıktıda yukarıdaki).

toostop hello Öykünücüler, bu komutu yürütün:

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a>Uygulamanızı yayımlama
toopublish, uygulamanızın toofirst alma gerekir, yayımlama hello kullanarak ayarları [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet'i. Hello kullanarak uygulamanızı yayımlayabilirsiniz sonra [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet'i. Oturum açma hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için bkz: Merhaba [PHP Geliştirici Merkezi](/develop/php/).

[PHP için Azure SDK]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[hizmet açıklaması (.csdef)]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[hizmet yapılandırma (.cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[sqlncli.msi x64 yükleyici]: http://go.microsoft.com/fwlink/?LinkID=239648
