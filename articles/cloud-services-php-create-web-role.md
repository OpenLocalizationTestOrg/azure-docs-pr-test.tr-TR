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
# <a name="how-toocreate-php-web-and-worker-roles"></a><span data-ttu-id="34107-103">Nasıl toocreate PHP web ve çalışan rolleri</span><span class="sxs-lookup"><span data-stu-id="34107-103">How toocreate PHP web and worker roles</span></span>
## <a name="overview"></a><span data-ttu-id="34107-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="34107-104">Overview</span></span>
<span data-ttu-id="34107-105">Bu kılavuz size nasıl toocreate PHP web veya çalışan rolleri Windows geliştirme ortamında, PHP belirli bir sürümünü hello kullanılabilir "yerleşik" sürümlerini seçin, hello PHP yapılandırmasını değiştirmek, uzantılarını etkinleştirme ve son olarak, tooAzure dağıtmak gösterir.</span><span class="sxs-lookup"><span data-stu-id="34107-105">This guide will show you how toocreate PHP web or worker roles in a Windows development environment, choose a specific version of PHP from hello "built-in" versions available, change hello PHP configuration, enable extensions, and finally, deploy tooAzure.</span></span> <span data-ttu-id="34107-106">Ayrıca açıklanır nasıl tooconfigure bir web veya çalışan rolü toouse sağlayan bir PHP çalışma zamanı (özel yapılandırma ve birlikte uzantıları).</span><span class="sxs-lookup"><span data-stu-id="34107-106">It also describes how tooconfigure a web or worker role toouse a PHP runtime (with custom configuration and extensions) that you provide.</span></span>

## <a name="what-are-php-web-and-worker-roles"></a><span data-ttu-id="34107-107">PHP web ve çalışan rolleri nelerdir?</span><span class="sxs-lookup"><span data-stu-id="34107-107">What are PHP web and worker roles?</span></span>
<span data-ttu-id="34107-108">Azure sağlayan üç işlem çalışan uygulamalar için modeli: Azure App Service, Azure sanal makineler ve Azure Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="34107-108">Azure provides three compute models for running applications: Azure App Service, Azure Virtual Machines, and Azure Cloud Services.</span></span> <span data-ttu-id="34107-109">Üç modeli PHP destekler.</span><span class="sxs-lookup"><span data-stu-id="34107-109">All three models support PHP.</span></span> <span data-ttu-id="34107-110">Web ve çalışan rolleri içerir, bulut hizmetleri sağlar *(PaaS) hizmet olarak platform*.</span><span class="sxs-lookup"><span data-stu-id="34107-110">Cloud Services, which includes web and worker roles, provides *platform as a service (PaaS)*.</span></span> <span data-ttu-id="34107-111">Bir bulut hizmetinde bir web rolü adanmış bir Internet Information Services (IIS) web sunucusu toohost ön uç web uygulamaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="34107-111">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server toohost front-end web applications.</span></span> <span data-ttu-id="34107-112">Çalışan rolü kullanıcı etkileşimi ve girişinden bağımsız zaman uyumsuz, uzun süre çalışan veya kalıcı görevleri çalıştırabilir.</span><span class="sxs-lookup"><span data-stu-id="34107-112">A worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="34107-113">Bu seçenekler hakkında daha fazla bilgi için bkz: [Azure tarafından sağlanan seçenekleri barındırma işlem](cloud-services/cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="34107-113">For more information about these options, see [Compute hosting options provided by Azure](cloud-services/cloud-services-choose-me.md).</span></span>

## <a name="download-hello-azure-sdk-for-php"></a><span data-ttu-id="34107-114">PHP için Hello Azure SDK'sını indirme</span><span class="sxs-lookup"><span data-stu-id="34107-114">Download hello Azure SDK for PHP</span></span>
<span data-ttu-id="34107-115">Merhaba [PHP için Azure SDK] birçok bileşenden oluşur.</span><span class="sxs-lookup"><span data-stu-id="34107-115">hello [Azure SDK for PHP] consists of several components.</span></span> <span data-ttu-id="34107-116">Bu makalede iki tanesi kullanır: Azure PowerShell ve Azure öykünücüsünü hello.</span><span class="sxs-lookup"><span data-stu-id="34107-116">This article will use two of them: Azure PowerShell and hello Azure emulators.</span></span> <span data-ttu-id="34107-117">Bu iki bileşenin hello Microsoft Web Platformu yükleyicisi yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="34107-117">These two components can be installed via hello Microsoft Web Platform Installer.</span></span> <span data-ttu-id="34107-118">Daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="34107-118">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="create-a-cloud-services-project"></a><span data-ttu-id="34107-119">Bulut Hizmetleri projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="34107-119">Create a Cloud Services project</span></span>
<span data-ttu-id="34107-120">bir PHP web veya çalışan rolü oluşturma hello ilk adımı toocreate bir Azure hizmeti projesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="34107-120">hello first step in creating a PHP web or worker role is toocreate an Azure Service project.</span></span> <span data-ttu-id="34107-121">bir Azure hizmeti projesi web ve çalışan rolleri için mantıksal bir kapsayıcı görevi görür ve hello projenin içeren [hizmet açıklaması (.csdef)] ve [hizmet yapılandırma (.cscfg)] dosyaları.</span><span class="sxs-lookup"><span data-stu-id="34107-121">an Azure Service project serves as a logical container for web and worker roles, and it contains hello project's [service definition (.csdef)] and [service configuration (.cscfg)] files.</span></span>

<span data-ttu-id="34107-122">toocreate yeni bir Azure hizmet projesi Azure PowerShell'i yönetici olarak çalıştırın ve hello aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="34107-122">toocreate a new Azure Service project, run Azure PowerShell as an administrator, and execute hello following command:</span></span>

    PS C:\>New-AzureServiceProject myProject

<span data-ttu-id="34107-123">Bu komut yeni bir dizin oluşturur (`myProject`) toowhich web ve çalışan rolleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34107-123">This command will create a new directory (`myProject`) toowhich you can add web and worker roles.</span></span>

## <a name="add-php-web-or-worker-roles"></a><span data-ttu-id="34107-124">PHP web veya çalışan rolleri Ekle</span><span class="sxs-lookup"><span data-stu-id="34107-124">Add PHP web or worker roles</span></span>
<span data-ttu-id="34107-125">bir PHP web rolü tooa projesi tooadd komuttan hello projenin kök dizini içinde aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="34107-125">tooadd a PHP web role tooa project, run hello following command from within hello project's root directory:</span></span>

    PS C:\myProject> Add-AzurePHPWebRole roleName

<span data-ttu-id="34107-126">Çalışan rolü için bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="34107-126">For a worker role, use this command:</span></span>

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> <span data-ttu-id="34107-127">Merhaba `roleName` parametresi isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="34107-127">hello `roleName` parameter is optional.</span></span> <span data-ttu-id="34107-128">Belirtilmezse, hello rol adı otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="34107-128">If it is omitted, hello role name will be automatically generated.</span></span> <span data-ttu-id="34107-129">oluşturulan hello ilk web rolü olacaktır `WebRole1`, hello ikinci olacaktır `WebRole2`ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="34107-129">hello first web role created will be `WebRole1`, hello second will be `WebRole2`, and so on.</span></span> <span data-ttu-id="34107-130">oluşturulan hello ilk çalışan rolü olacaktır `WorkerRole1`, hello ikinci olacaktır `WorkerRole2`ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="34107-130">hello first worker role created will be `WorkerRole1`, hello second will be `WorkerRole2`, and so on.</span></span>
>
>

## <a name="specify-hello-built-in-php-version"></a><span data-ttu-id="34107-131">Merhaba yerleşik PHP sürümünü belirtin</span><span class="sxs-lookup"><span data-stu-id="34107-131">Specify hello built-in PHP version</span></span>
<span data-ttu-id="34107-132">Bir PHP web veya çalışan rolü tooa proje eklediğinizde, böylece her uygulamanızın web veya çalışan örneği üzerinde dağıtıldığında PHP yüklenecek hello projenin yapılandırma dosyalarını değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="34107-132">When you add a PHP web or worker role tooa project, hello project's configuration files are modified so that PHP will be installed on each web or worker instance of your application when it is deployed.</span></span> <span data-ttu-id="34107-133">komutu aşağıdaki hello çalıştırmak varsayılan olarak, yüklenecek PHP toosee hello sürümü:</span><span class="sxs-lookup"><span data-stu-id="34107-133">toosee hello version of PHP that will be installed by default, run hello following command:</span></span>

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

<span data-ttu-id="34107-134">Merhaba yukarıdaki hello komut çıktısı şuna benzer toowhat aşağıda gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="34107-134">hello output from hello command above will look similar toowhat is shown below.</span></span> <span data-ttu-id="34107-135">Bu örnekte, hello `IsDefault` bayrağı çok ayarlanır`true` hello varsayılan PHP sürümü yüklü olacağını belirten php 5.3.17,.</span><span class="sxs-lookup"><span data-stu-id="34107-135">In this example, hello `IsDefault` flag is set too`true` for PHP 5.3.17, indicating that it will be hello default PHP version installed.</span></span>

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

<span data-ttu-id="34107-136">Merhaba PHP çalışma zamanı sürümü tooany listelenen hello PHP sürümlerinin ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34107-136">You can set hello PHP runtime version tooany of hello PHP versions that are listed.</span></span> <span data-ttu-id="34107-137">Örneğin, tooset hello PHP sürümünü (Merhaba ada sahip bir rol için `roleName`) too5.4.0, komutu aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="34107-137">For example, tooset hello PHP version (for a role with hello name `roleName`) too5.4.0, use hello following command:</span></span>

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> <span data-ttu-id="34107-138">Kullanılabilir PHP sürümlerin hello gelecekteki değişebilir.</span><span class="sxs-lookup"><span data-stu-id="34107-138">Available PHP versions may change in hello future.</span></span>
>
>

## <a name="customize-hello-built-in-php-runtime"></a><span data-ttu-id="34107-139">Merhaba yerleşik PHP çalışma zamanı özelleştirme</span><span class="sxs-lookup"><span data-stu-id="34107-139">Customize hello built-in PHP runtime</span></span>
<span data-ttu-id="34107-140">Yukarıdaki değiştirilmesini dahil olmak üzere hello adımları izlediğinizde yüklü hello PHP çalışma zamanı hello yapılandırmasını üzerinde tam denetime sahip `php.ini` ayarları ve uzantılarını etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="34107-140">You have complete control over hello configuration of hello PHP runtime that is installed when you follow hello steps above, including modification of `php.ini` settings and enabling of extensions.</span></span>

<span data-ttu-id="34107-141">toocustomize yerleşik PHP çalışma zamanı Merhaba, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="34107-141">toocustomize hello built-in PHP runtime, follow these steps:</span></span>

1. <span data-ttu-id="34107-142">Adlı yeni bir klasör ekleyin `php`, toohello `bin` web rolünüz dizininde.</span><span class="sxs-lookup"><span data-stu-id="34107-142">Add a new folder, named `php`, toohello `bin` directory of your web role.</span></span> <span data-ttu-id="34107-143">Çalışan rolü için toohello rolün kök dizin ekleyin.</span><span class="sxs-lookup"><span data-stu-id="34107-143">For a worker role, add it toohello role's root directory.</span></span>
2. <span data-ttu-id="34107-144">Merhaba, `php` klasörünü adlı başka bir klasör oluşturun `ext`.</span><span class="sxs-lookup"><span data-stu-id="34107-144">In hello `php` folder, create another folder called `ext`.</span></span> <span data-ttu-id="34107-145">Herhangi bir yerleştirme `.dll` uzantısı dosyaları (örn., `php_mongo.dll`) bu klasörde tooenable istiyor.</span><span class="sxs-lookup"><span data-stu-id="34107-145">Put any `.dll` extension files (e.g., `php_mongo.dll`) that you want tooenable in this folder.</span></span>
3. <span data-ttu-id="34107-146">Ekleme bir `php.ini` toohello dosya `php` klasör.</span><span class="sxs-lookup"><span data-stu-id="34107-146">Add a `php.ini` file toohello `php` folder.</span></span> <span data-ttu-id="34107-147">Tüm özel uzantılar etkinleştirin ve bu dosyadaki tüm PHP yönergeleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="34107-147">Enable any custom extensions and set any PHP directives in this file.</span></span> <span data-ttu-id="34107-148">Örneğin, tooturn istediyseniz `display_errors` üzerinde ve hello etkinleştirmek `php_mongo.dll` uzantısı, Merhaba içeriğine, `php.ini` dosya şu şekilde olacaktır:</span><span class="sxs-lookup"><span data-stu-id="34107-148">For example, if you wanted tooturn `display_errors` on and enable hello `php_mongo.dll` extension, hello contents of your `php.ini` file would be as follows:</span></span>

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> <span data-ttu-id="34107-149">Hello açıkça ayarlamazsanız herhangi bir ayarı `php.ini` otomatik olarak sağlamak dosya tootheir varsayılan değerleri ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="34107-149">Any settings that you don't explicitly set in hello `php.ini` file that you provide will automatically be set tootheir default values.</span></span> <span data-ttu-id="34107-150">Ancak, bir tam ekleyebilirsiniz göz önünde bulundurmanız `php.ini` dosya.</span><span class="sxs-lookup"><span data-stu-id="34107-150">However, keep in mind that you can add a complete `php.ini` file.</span></span>
>
>

## <a name="use-your-own-php-runtime"></a><span data-ttu-id="34107-151">Kendi PHP çalışma zamanı kullanın</span><span class="sxs-lookup"><span data-stu-id="34107-151">Use your own PHP runtime</span></span>
<span data-ttu-id="34107-152">Yerleşik bir PHP çalışma zamanı seçme ve yukarıda açıklandığı gibi yapılandırma yerine bazı durumlarda, kendi PHP çalışma zamanı tooprovide isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34107-152">In some cases, instead of selecting a built-in PHP runtime and configuring it as described above, you may want tooprovide your own PHP runtime.</span></span> <span data-ttu-id="34107-153">Örneğin, kullanabileceğiniz hello geliştirme ortamınızı kullandığınız web veya çalışan rolü aynı PHP çalışma zamanı.</span><span class="sxs-lookup"><span data-stu-id="34107-153">For example, you can use hello same PHP runtime in a web or worker role that you use in your development environment.</span></span> <span data-ttu-id="34107-154">Bu, daha kolay tooensure Merhaba uygulaması üretim ortamınızda davranış değişmez kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="34107-154">This makes it easier tooensure that hello application will not change behavior in your production environment.</span></span>

### <a name="configure-a-web-role-toouse-your-own-php-runtime"></a><span data-ttu-id="34107-155">Bir web rolü toouse kendi PHP çalışma zamanı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34107-155">Configure a web role toouse your own PHP runtime</span></span>
<span data-ttu-id="34107-156">tooconfigure bir web rolü toouse sağlarsanız, PHP çalışma zamanı şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="34107-156">tooconfigure a web role toouse a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="34107-157">Bir Azure hizmeti projesi oluşturun ve bu konuda daha önce açıklandığı gibi bir PHP web rolü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="34107-157">Create an Azure Service project and add a PHP web role as described previously in this topic.</span></span>
2. <span data-ttu-id="34107-158">Oluşturma bir `php` hello klasöründe `bin` web rolün kök dizininde bulunan ve PHP çalışma zamanı (tüm ikili dosyaları, yapılandırma dosyalarını, alt klasörler, vb.) toohello eklemek klasör `php` klasör.</span><span class="sxs-lookup"><span data-stu-id="34107-158">Create a `php` folder in hello `bin` folder that is in your web role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) toohello `php` folder.</span></span>
3. <span data-ttu-id="34107-159">(İSTEĞE BAĞLI) Merhaba, PHP çalışma zamanı kullanıyorsa, [SQL Server için PHP için Microsoft Drivers][sqlsrv drivers], web rolü tooinstall tooconfigure gerekir [SQL Server Native Client 2012] [ sql native client] , ne zaman hazırlanır.</span><span class="sxs-lookup"><span data-stu-id="34107-159">(OPTIONAL) If your PHP runtime uses hello [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need tooconfigure your web role tooinstall [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="34107-160">toodo bunu hello eklemek [sqlncli.msi x64 yükleyici] toohello `bin` web rolün kök dizininde klasör.</span><span class="sxs-lookup"><span data-stu-id="34107-160">toodo this, add hello [sqlncli.msi x64 installer] toohello `bin` folder in your web role's root directory.</span></span> <span data-ttu-id="34107-161">Merhaba rol sağlandığında hello sonraki adımda açıklanan hello başlangıç betiği sessizce hello yükleyiciyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="34107-161">hello startup script described in hello next step will silently run hello installer when hello role is provisioned.</span></span> <span data-ttu-id="34107-162">PHP çalışma zamanı, SQL Server için PHP için hello Microsoft Drivers kullanmıyorsa, hello sonraki adımda gösterilen hello komut satırı yükseltmesinin hello kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="34107-162">If your PHP runtime does not use hello Microsoft Drivers for PHP for SQL Server, you can remove hello following line from hello script shown in hello next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="34107-163">Yapılandırır bir başlangıç görevi tanımlamak [Internet Information Services (IIS)] [ iis.net] , PHP çalışma zamanı toohandle istekleri için toouse `.php` sayfaları.</span><span class="sxs-lookup"><span data-stu-id="34107-163">Define a startup task that configures [Internet Information Services (IIS)][iis.net] toouse your PHP runtime toohandle requests for `.php` pages.</span></span> <span data-ttu-id="34107-164">toodo Bu, açık hello `setup_web.cmd` dosya (Merhaba içinde `bin` web rolün kök dizin dosyası) bir metin Düzenleyicisi'ni ve içeriğini ile Merhaba komut dosyasını değiştirin:</span><span class="sxs-lookup"><span data-stu-id="34107-164">toodo this, open hello `setup_web.cmd` file (in hello `bin` file of your web role's root directory) in a text editor and replace its contents with hello following script:</span></span>

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
5. <span data-ttu-id="34107-165">Uygulama dosyaları tooyour web rolünüz ait kök dizine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="34107-165">Add your application files tooyour web role's root directory.</span></span> <span data-ttu-id="34107-166">Bu hello web sunucusunun kök dizininde olacaktır.</span><span class="sxs-lookup"><span data-stu-id="34107-166">This will be hello web server's root directory.</span></span>
6. <span data-ttu-id="34107-167">Uygulamanız yayımlama hello açıklandığı gibi [uygulamanızı yayımlamak](#publish-your-application) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="34107-167">Publish your application as described in hello [Publish your application](#publish-your-application) section below.</span></span>

> [!NOTE]
> <span data-ttu-id="34107-168">Merhaba `download.ps1` komut dosyası (Merhaba içinde `bin` hello web rolün kök dizininin klasör), kendi PHP çalışma zamanı kullanmak için yukarıda açıklanan başlangıç adımları izledikten sonra silinebilir.</span><span class="sxs-lookup"><span data-stu-id="34107-168">hello `download.ps1` script (in hello `bin` folder of hello web role's root directory) can be deleted after you follow hello steps described above for using your own PHP runtime.</span></span>
>
>

### <a name="configure-a-worker-role-toouse-your-own-php-runtime"></a><span data-ttu-id="34107-169">Çalışan rolü toouse kendi PHP çalışma zamanı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34107-169">Configure a worker role toouse your own PHP runtime</span></span>
<span data-ttu-id="34107-170">tooconfigure çalışan rolü toouse sağlarsanız, PHP çalışma zamanı şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="34107-170">tooconfigure a worker role toouse a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="34107-171">Bir Azure hizmeti projesi oluşturun ve bu konuda daha önce açıklandığı gibi PHP çalışan rolü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="34107-171">Create an Azure Service project and add a PHP worker role as described previously in this topic.</span></span>
2. <span data-ttu-id="34107-172">Oluşturma bir `php` hello çalışan rolün kök dizini klasöründe ve ardından, PHP çalışma zamanı (tüm ikili dosyaları, yapılandırma dosyalarını, alt klasörler, vb.) toohello ekleyin `php` klasör.</span><span class="sxs-lookup"><span data-stu-id="34107-172">Create a `php` folder in hello worker role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) toohello `php` folder.</span></span>
3. <span data-ttu-id="34107-173">(İSTEĞE BAĞLI) PHP çalışma zamanı kullanıyorsa [SQL Server için PHP için Microsoft Drivers][sqlsrv drivers], çalışan rolü tooinstall tooconfigure gerekir [SQL Server Native Client 2012] [ sql native client] , ne zaman hazırlanır.</span><span class="sxs-lookup"><span data-stu-id="34107-173">(OPTIONAL) If your PHP runtime uses [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need tooconfigure your worker role tooinstall [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="34107-174">toodo bunu hello eklemek [sqlncli.msi x64 yükleyici] toohello çalışan rolün kök dizini.</span><span class="sxs-lookup"><span data-stu-id="34107-174">toodo this, add hello [sqlncli.msi x64 installer] toohello worker role's root directory.</span></span> <span data-ttu-id="34107-175">Merhaba rol sağlandığında hello sonraki adımda açıklanan hello başlangıç betiği sessizce hello yükleyiciyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="34107-175">hello startup script described in hello next step will silently run hello installer when hello role is provisioned.</span></span> <span data-ttu-id="34107-176">PHP çalışma zamanı, SQL Server için PHP için hello Microsoft Drivers kullanmıyorsa, hello sonraki adımda gösterilen hello komut satırı yükseltmesinin hello kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="34107-176">If your PHP runtime does not use hello Microsoft Drivers for PHP for SQL Server, you can remove hello following line from hello script shown in hello next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="34107-177">Ekler bir başlangıç görevi tanımlamak, `php.exe` hello rol sağlandığında yürütülebilir toohello çalışan rolün PATH ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="34107-177">Define a startup task that adds your `php.exe` executable toohello worker role's PATH environment variable when hello role is provisioned.</span></span> <span data-ttu-id="34107-178">toodo Bu, açık hello `setup_worker.cmd` (Merhaba çalışan rolün kök dizininde) bir metin Düzenleyicisi'nde dosya ve içeriğinin komut dosyası izleyen hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="34107-178">toodo this, open hello `setup_worker.cmd` file (in hello worker role's root directory) in a text editor and replace its contents with hello following script:</span></span>

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
5. <span data-ttu-id="34107-179">Uygulama dosyaları tooyour çalışan rolünüzün ait kök dizine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="34107-179">Add your application files tooyour worker role's root directory.</span></span>
6. <span data-ttu-id="34107-180">Uygulamanız yayımlama hello açıklandığı gibi [uygulamanızı yayımlamak](#publish-your-application) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="34107-180">Publish your application as described in hello [Publish your application](#publish-your-application) section below.</span></span>

## <a name="run-your-application-in-hello-compute-and-storage-emulators"></a><span data-ttu-id="34107-181">İşlem ve depolama öykünücüsünü hello uygulamanızı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="34107-181">Run your application in hello compute and storage emulators</span></span>
<span data-ttu-id="34107-182">Hello Azure öykünücüsünü toohello bulut dağıtmadan önce Azure uygulamanızı sınayabilir yerel bir ortam sağlar.</span><span class="sxs-lookup"><span data-stu-id="34107-182">hello Azure emulators provide a local environment in which you can test your Azure application before you deploy it toohello cloud.</span></span> <span data-ttu-id="34107-183">Merhaba Öykünücüler ve hello Azure ortamı arasındaki bazı farklar vardır.</span><span class="sxs-lookup"><span data-stu-id="34107-183">There are some differences between hello emulators and hello Azure environment.</span></span> <span data-ttu-id="34107-184">Bu daha iyi görmek toounderstand [geliştirme ve test amacıyla hello Azure storage öykünücüsünü kullanma](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="34107-184">toounderstand this better, see [Use hello Azure storage emulator for development and testing](storage/common/storage-use-emulator.md).</span></span>

<span data-ttu-id="34107-185">PHP olmalıdır Not toouse hello işlem öykünücüsü yerel olarak yüklü.</span><span class="sxs-lookup"><span data-stu-id="34107-185">Note that you must have PHP installed locally toouse hello compute emulator.</span></span> <span data-ttu-id="34107-186">Merhaba işlem öykünücüsü, yerel PHP yükleme toorun uygulamanızı kullanır.</span><span class="sxs-lookup"><span data-stu-id="34107-186">hello compute emulator will use your local PHP installation toorun your application.</span></span>

<span data-ttu-id="34107-187">Merhaba Öykünücüler projenizde toorun yürütme hello projenizin kök dizinin komutu aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="34107-187">toorun your project in hello emulators, execute hello following command from your project's root directory:</span></span>

    PS C:\MyProject> Start-AzureEmulator

<span data-ttu-id="34107-188">Çıktı benzer toothis görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="34107-188">You will see output similar toothis:</span></span>

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

<span data-ttu-id="34107-189">Web tarayıcısında açarak ve toohello yerel adres hello çıktıda gösterilen gözatma hello öykünücüsünde çalıştıran uygulamanız görebilirsiniz (`http://127.0.0.1:81` hello örnek çıktıda yukarıdaki).</span><span class="sxs-lookup"><span data-stu-id="34107-189">You can see your application running in hello emulator by opening a web browser and browsing toohello local address shown in hello output (`http://127.0.0.1:81` in hello example output above).</span></span>

<span data-ttu-id="34107-190">toostop hello Öykünücüler, bu komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="34107-190">toostop hello emulators, execute this command:</span></span>

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a><span data-ttu-id="34107-191">Uygulamanızı yayımlama</span><span class="sxs-lookup"><span data-stu-id="34107-191">Publish your application</span></span>
<span data-ttu-id="34107-192">toopublish, uygulamanızın toofirst alma gerekir, yayımlama hello kullanarak ayarları [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="34107-192">toopublish your application, you need toofirst import your publish settings by using hello [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span></span> <span data-ttu-id="34107-193">Hello kullanarak uygulamanızı yayımlayabilirsiniz sonra [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="34107-193">Then you can publish your application by using hello [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span></span> <span data-ttu-id="34107-194">Oturum açma hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="34107-194">For information about signing in, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="next-steps"></a><span data-ttu-id="34107-195">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="34107-195">Next steps</span></span>
<span data-ttu-id="34107-196">Daha fazla bilgi için bkz: Merhaba [PHP Geliştirici Merkezi](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="34107-196">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

[PHP için Azure SDK]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[hizmet açıklaması (.csdef)]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[hizmet yapılandırma (.cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[sqlncli.msi x64 yükleyici]: http://go.microsoft.com/fwlink/?LinkID=239648
