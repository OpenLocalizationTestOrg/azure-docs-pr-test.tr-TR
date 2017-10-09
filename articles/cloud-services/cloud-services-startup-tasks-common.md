---
title: "Bulut Hizmetleri için aaaCommon başlangıç görevleri | Microsoft Docs"
description: "Bazı örnekler verilmektedir ortak başlangıç görevleri bulut Hizmetleri web rolü veya çalışan rolü tooperform isteyebilirsiniz."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: a7095dad-1ee7-4141-bc6a-ef19a6e570f1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: c80fac4079439410dfc3795e4bce0fbc07dbbfab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="common-cloud-service-startup-tasks"></a><span data-ttu-id="d3eac-103">Genel bulut hizmeti başlangıç görevleri</span><span class="sxs-lookup"><span data-stu-id="d3eac-103">Common Cloud Service startup tasks</span></span>
<span data-ttu-id="d3eac-104">Bu makalede bazı örnekler ortak başlangıç görevleri, bulut hizmetinizin tooperform isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3eac-104">This article provides some examples of common startup tasks you may want tooperform in your cloud service.</span></span> <span data-ttu-id="d3eac-105">Bir rolü başlamadan önce başlangıç görevleri tooperform işlemleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3eac-105">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="d3eac-106">Bir bileşeni yüklemek, COM bileşenlerini kaydetme, kayıt defteri anahtarlarını ayarlamak veya uzun süre çalışan bir işlem başlatılıyor tooperform isteyebilirsiniz işlemleri içerir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-106">Operations that you might want tooperform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span> 

<span data-ttu-id="d3eac-107">Bkz: [bu makalede](cloud-services-startup-tasks.md) toounderstand nasıl iş başlangıç görevleri ve özellikle nasıl toocreate hello bir başlangıç görevi tanımlayan girişinin.</span><span class="sxs-lookup"><span data-stu-id="d3eac-107">See [this article](cloud-services-startup-tasks.md) toounderstand how startup tasks work, and specifically how toocreate hello entries that define a startup task.</span></span>

> [!NOTE]
> <span data-ttu-id="d3eac-108">Başlangıç değil yalnızca tooCloud Service Web ve çalışan rolleri geçerli tooVirtual makineleri görevlerdir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-108">Startup tasks are not applicable tooVirtual Machines, only tooCloud Service Web and Worker roles.</span></span>
> 

## <a name="define-environment-variables-before-a-role-starts"></a><span data-ttu-id="d3eac-109">Bir rolü başlatılmadan önce ortamı değişkenleri tanımlayın</span><span class="sxs-lookup"><span data-stu-id="d3eac-109">Define environment variables before a role starts</span></span>
<span data-ttu-id="d3eac-110">Belirli bir görev için tanımlanan ortam değişkenlerini gerekirse hello kullanın [ortam] öğesi hello içinde [görev] öğesi.</span><span class="sxs-lookup"><span data-stu-id="d3eac-110">If you need environment variables defined for a specific task, use hello [Environment] element inside hello [Task] element.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
                <Environment>
                    <Variable name="MyEnvironmentVariable" value="MyVariableValue" />
                </Environment>
            </Task>
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="d3eac-111">Değişkenleri de kullanabilir bir [geçerli Azure XPath değeri](cloud-services-role-config-xpath.md) hello dağıtım hakkında bir şeyler tooreference.</span><span class="sxs-lookup"><span data-stu-id="d3eac-111">Variables can also use a [valid Azure XPath value](cloud-services-role-config-xpath.md) tooreference something about hello deployment.</span></span> <span data-ttu-id="d3eac-112">Hello yerine `value` özniteliği, tanımlayan bir [RoleInstanceValue] alt öğesi.</span><span class="sxs-lookup"><span data-stu-id="d3eac-112">Instead of using hello `value` attribute, define a [RoleInstanceValue] child element.</span></span>

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a><span data-ttu-id="d3eac-113">IIS Başlangıç AppCmd.exe ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d3eac-113">Configure IIS startup with AppCmd.exe</span></span>
<span data-ttu-id="d3eac-114">Merhaba [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) komut satırı aracı, Azure üzerinde başlangıçta kullanılan toomanage IIS ayarları olabilir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-114">hello [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) command-line tool can be used toomanage IIS settings at startup on Azure.</span></span> <span data-ttu-id="d3eac-115">*AppCmd.exe* Azure üzerinde uygun ve komut satırı erişim tooconfiguration ayarları kullanmak üzere başlangıç görevleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="d3eac-115">*AppCmd.exe* provides convenient, command-line access tooconfiguration settings for use in startup tasks on Azure.</span></span> <span data-ttu-id="d3eac-116">Kullanarak *AppCmd.exe*, Web sitesi ayarlarını eklenemez, değiştiren veya uygulamaları ve sitelerin kaldırılamaz.</span><span class="sxs-lookup"><span data-stu-id="d3eac-116">Using *AppCmd.exe*, Website settings can be added, modified, or removed for applications and sites.</span></span>

<span data-ttu-id="d3eac-117">Ancak, vardır için birkaç şey toowatch çıkışı, hello kullanımda *AppCmd.exe* bir başlangıç görevi olarak:</span><span class="sxs-lookup"><span data-stu-id="d3eac-117">However, there are a few things toowatch out for in hello use of *AppCmd.exe* as a startup task:</span></span>

* <span data-ttu-id="d3eac-118">Başlangıç görevi birden çok kez yeniden başlatmalar arasında çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3eac-118">Startup tasks can be run more than once between reboots.</span></span> <span data-ttu-id="d3eac-119">Örneğin, ne zaman bir rol geri dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="d3eac-119">For instance, when a role recycles.</span></span>
* <span data-ttu-id="d3eac-120">Varsa bir *AppCmd.exe* eylem birden çok kez gerçekleştirilir, hataya neden.</span><span class="sxs-lookup"><span data-stu-id="d3eac-120">If a *AppCmd.exe* action is performed more than once, it may generate an error.</span></span> <span data-ttu-id="d3eac-121">Örneğin, tooadd bir bölümü çok çalışıyor*Web.config* iki kez hataya neden.</span><span class="sxs-lookup"><span data-stu-id="d3eac-121">For example, attempting tooadd a section too*Web.config* twice could generate an error.</span></span>
* <span data-ttu-id="d3eac-122">Başlangıç görevleri, sıfır olmayan çıkış kodu döndürmesi durumunda başarısız veya **errorlevel**.</span><span class="sxs-lookup"><span data-stu-id="d3eac-122">Startup tasks fail if they return a non-zero exit code or **errorlevel**.</span></span> <span data-ttu-id="d3eac-123">Örneğin, *AppCmd.exe* bir hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d3eac-123">For example, when *AppCmd.exe* generates an error.</span></span>

<span data-ttu-id="d3eac-124">İyi bir uygulama toocheck hello olan **errorlevel** çağırdıktan sonra *AppCmd.exe*, hangi ise kolay toodo hello çağrısı çok kaydırma*AppCmd.exe* ile bir *.cmd*  dosya.</span><span class="sxs-lookup"><span data-stu-id="d3eac-124">It is a good practice toocheck hello **errorlevel** after calling *AppCmd.exe*, which is easy toodo if you wrap hello call too*AppCmd.exe* with a *.cmd* file.</span></span> <span data-ttu-id="d3eac-125">Bilinen bir algılama **errorlevel** yanıtı yok sayın veya için geri geçirin.</span><span class="sxs-lookup"><span data-stu-id="d3eac-125">If you detect a known **errorlevel** response, you can ignore it, or pass it back.</span></span>

<span data-ttu-id="d3eac-126">tarafından döndürülen errorlevel hello *AppCmd.exe* hello Winerror.h'de dosyasında listelenir ve ayrıca görülebilir [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3eac-126">hello errorlevel returned by *AppCmd.exe* are listed in hello winerror.h file, and can also be seen on [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span></span>

### <a name="example-of-managing-hello-error-level"></a><span data-ttu-id="d3eac-127">Örnek hello hata düzeyi yönetme</span><span class="sxs-lookup"><span data-stu-id="d3eac-127">Example of managing hello error level</span></span>
<span data-ttu-id="d3eac-128">Bu örnek bir sıkıştırma bölümü ve JSON toohello için sıkıştırma girişi ekler *Web.config* dosyasıyla hata işleme ve günlüğe kaydetme.</span><span class="sxs-lookup"><span data-stu-id="d3eac-128">This example adds a compression section and a compression entry for JSON toohello *Web.config* file, with error handling and logging.</span></span>

<span data-ttu-id="d3eac-129">Merhaba hello ilgili bölümleri [ServiceDefinition.csdef] dosya burada gösterilen, hello ayarlama içeren [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) çok öznitelik`elevated` toogive *AppCmd.exe*  yeterli izinleri toochange hello ayarlarında hello *Web.config* dosyası:</span><span class="sxs-lookup"><span data-stu-id="d3eac-129">hello relevant sections of hello [ServiceDefinition.csdef] file are shown here, which include setting hello [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) attribute too`elevated` toogive *AppCmd.exe* sufficient permissions toochange hello settings in hello *Web.config* file:</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="d3eac-130">Merhaba *Startup.cmd* toplu iş dosyası kullanır *AppCmd.exe* tooadd sıkıştırma bölüm ve sıkıştırma giriş JSON toohello için *Web.config* dosya.</span><span class="sxs-lookup"><span data-stu-id="d3eac-130">hello *Startup.cmd* batch file uses *AppCmd.exe* tooadd a compression section and a compression entry for JSON toohello *Web.config* file.</span></span> <span data-ttu-id="d3eac-131">Beklenen hello **errorlevel** 183 hello doğrula kullanarak toozero ayarlanır. EXE komut satırı programı.</span><span class="sxs-lookup"><span data-stu-id="d3eac-131">hello expected **errorlevel** of 183 is set toozero using hello VERIFY.EXE command-line program.</span></span> <span data-ttu-id="d3eac-132">Beklenmeyen errorlevels oturum tooStartupErrorLog.txt ' dir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-132">Unexpected errorlevels are logged tooStartupErrorLog.txt.</span></span>

```cmd
REM   *** Add a compression section toohello Web.config file. ***
%windir%\system32\inetsrv\appcmd set config /section:urlCompression /doDynamicCompression:True /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1

REM   ERRORLEVEL 183 occurs when trying tooadd a section that already exists. This error is expected if this
REM   batch file were executed twice. This can occur and must be accounted for in a Azure startup
REM   task. toohandle this situation, set hello ERRORLEVEL toozero by using hello Verify command. hello Verify
REM   command will safely set hello ERRORLEVEL toozero.
IF %ERRORLEVEL% EQU 183 DO VERIFY > NUL

REM   If hello ERRORLEVEL is not zero at this point, some other error occurred.
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding a compression section toohello Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Add compression for json. ***
%windir%\system32\inetsrv\appcmd set config  -section:system.webServer/httpCompression /+"dynamicTypes.[mimeType='application/json; charset=utf-8',enabled='True']" /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1
IF %ERRORLEVEL% EQU 183 VERIFY > NUL
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding hello JSON compression type toohello Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Exit batch file. ***
EXIT /b 0

REM   *** Log error and exit ***
:ErrorExit
REM   Report hello date, time, and ERRORLEVEL of hello error.
DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
ECHO An error occurred during startup. ERRORLEVEL = %ERRORLEVEL% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT %ERRORLEVEL%
```

## <a name="add-firewall-rules"></a><span data-ttu-id="d3eac-133">Güvenlik duvarı kuralları ekleme</span><span class="sxs-lookup"><span data-stu-id="d3eac-133">Add firewall rules</span></span>
<span data-ttu-id="d3eac-134">Azure üzerinde etkili bir şekilde iki güvenlik duvarı vardır.</span><span class="sxs-lookup"><span data-stu-id="d3eac-134">In Azure, there are effectively two firewalls.</span></span> <span data-ttu-id="d3eac-135">Merhaba ilk güvenlik duvarı hello sanal makine ve hello world dışında arasındaki bağlantıları denetler.</span><span class="sxs-lookup"><span data-stu-id="d3eac-135">hello first firewall controls connections between hello virtual machine and hello outside world.</span></span> <span data-ttu-id="d3eac-136">Bu güvenlik duvarı tarafından hello denetlenir [uç noktaları] hello öğesinde [ServiceDefinition.csdef] dosya.</span><span class="sxs-lookup"><span data-stu-id="d3eac-136">This firewall is controlled by hello [EndPoints] element in hello [ServiceDefinition.csdef] file.</span></span>

<span data-ttu-id="d3eac-137">Merhaba ikinci güvenlik duvarı hello sanal makine ve sanal makinenin içinde hello işlemleri arasındaki bağlantıları denetler.</span><span class="sxs-lookup"><span data-stu-id="d3eac-137">hello second firewall controls connections between hello virtual machine and hello processes within that virtual machine.</span></span> <span data-ttu-id="d3eac-138">Bu güvenlik duvarı tarafından hello denetlenebilir `netsh advfirewall firewall` komut satırı aracı.</span><span class="sxs-lookup"><span data-stu-id="d3eac-138">This firewall can be controlled by hello `netsh advfirewall firewall` command-line tool.</span></span>

<span data-ttu-id="d3eac-139">Azure güvenlik duvarı kuralları rollerinizi içinde başlatılan hello işlemler için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d3eac-139">Azure creates firewall rules for hello processes started within your roles.</span></span> <span data-ttu-id="d3eac-140">Bir hizmet veya programın başlattığınızda, örneğin, Azure otomatik olarak hello gerekli güvenlik duvarı kuralları tooallow bu hizmet toocommunicate hello Internet ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d3eac-140">For example, when you start a service or program, Azure automatically creates hello necessary firewall rules tooallow that service toocommunicate with hello Internet.</span></span> <span data-ttu-id="d3eac-141">Ancak, rolünüze (örneğin, bir COM + hizmet ya da Windows zamanlanmış bir görev) dışında bir işlem tarafından başlatılan bir hizmet oluşturursanız, toomanually gerekir bir güvenlik duvarı kuralı tooallow erişim toothat hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d3eac-141">However, if you create a service that is started by a process outside your role (like a COM+ service or a Windows Scheduled Task), you need toomanually create a firewall rule tooallow access toothat service.</span></span> <span data-ttu-id="d3eac-142">Bu güvenlik duvarı kuralları, bir başlangıç görevi kullanılarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-142">These firewall rules can be created by using a startup task.</span></span>

<span data-ttu-id="d3eac-143">Bir güvenlik duvarı kuralı oluşturan bir başlangıç görevi olmalıdır bir [executionContext][görev] , **yükseltilmiş**.</span><span class="sxs-lookup"><span data-stu-id="d3eac-143">A startup task that creates a firewall rule must have an [executionContext][Task] of **elevated**.</span></span> <span data-ttu-id="d3eac-144">Aşağıdaki başlangıç görevi toohello hello eklemek [ServiceDefinition.csdef] dosya.</span><span class="sxs-lookup"><span data-stu-id="d3eac-144">Add hello following startup task toohello [ServiceDefinition.csdef] file.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="AddFirewallRules.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="d3eac-145">tooadd hello güvenlik duvarı kuralı, hello uygun kullanmalıdır `netsh advfirewall firewall` başlangıç toplu iş dosyası komutları.</span><span class="sxs-lookup"><span data-stu-id="d3eac-145">tooadd hello firewall rule, you must use hello appropriate `netsh advfirewall firewall` commands in your startup batch file.</span></span> <span data-ttu-id="d3eac-146">Bu örnekte, hello başlangıç görevi güvenlik ve şifreleme'yi TCP bağlantı noktası 80 gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-146">In this example, hello startup task requires security and encryption for TCP port 80.</span></span>

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a><span data-ttu-id="d3eac-147">Belirli bir IP adres bloğu</span><span class="sxs-lookup"><span data-stu-id="d3eac-147">Block a specific IP address</span></span>
<span data-ttu-id="d3eac-148">IIS değiştirerek bir Azure web rolü erişim tooa belirtilen IP adresleri kümesini kısıtlayabilirsiniz **web.config** dosya.</span><span class="sxs-lookup"><span data-stu-id="d3eac-148">You can restrict an Azure web role access tooa set of specified IP addresses by modifying your IIS **web.config** file.</span></span> <span data-ttu-id="d3eac-149">Toouse hello kilidini açan bir komut dosyası etmeniz **IPSecurity** hello bölümünü **ApplicationHost.config** dosya.</span><span class="sxs-lookup"><span data-stu-id="d3eac-149">You also need toouse a command file which unlocks hello **ipSecurity** section of hello **ApplicationHost.config** file.</span></span>

<span data-ttu-id="d3eac-150">toodo kilidini hello **IPSecurity** hello bölümünü **ApplicationHost.config** dosya, rol başlangıcında çalışan bir komut dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d3eac-150">toodo unlock hello **ipSecurity** section of hello **ApplicationHost.config** file, create a command file that runs at role start.</span></span> <span data-ttu-id="d3eac-151">Merhaba kök düzeyinde web rolünüz adlı bir klasör oluşturun **başlangıç** ve bu klasör içinde adlı bir toplu iş dosyası oluşturmak **startup.cmd**.</span><span class="sxs-lookup"><span data-stu-id="d3eac-151">Create a folder at hello root level of your web role called **startup** and, within this folder, create a batch file called **startup.cmd**.</span></span> <span data-ttu-id="d3eac-152">Bu dosya tooyour Visual Studio projesi eklemek hello özelliklerini ve çok**her zaman Kopyala** tooensure paketinize eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-152">Add this file tooyour Visual Studio project and set hello properties too**Copy Always** tooensure that it is included in your package.</span></span>

<span data-ttu-id="d3eac-153">Aşağıdaki başlangıç görevi toohello hello eklemek [ServiceDefinition.csdef] dosya.</span><span class="sxs-lookup"><span data-stu-id="d3eac-153">Add hello following startup task toohello [ServiceDefinition.csdef] file.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WebRole name="WebRole1">
        ...
        <Startup>
            <Task commandLine="startup.cmd" executionContext="elevated" />
        </Startup>
    </WebRole>
</ServiceDefinition>
```

<span data-ttu-id="d3eac-154">Bu komut toohello ekleme **startup.cmd** dosyası:</span><span class="sxs-lookup"><span data-stu-id="d3eac-154">Add this command toohello **startup.cmd** file:</span></span>

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

<span data-ttu-id="d3eac-155">Bu görev hello neden **startup.cmd** hello web rolü başlatılan her çalıştığında, çalışması dosya toobe gerekli o hello sağlama toplu **IPSecurity** bölümdür kilidi.</span><span class="sxs-lookup"><span data-stu-id="d3eac-155">This task causes hello **startup.cmd** batch file toobe run every time hello web role is initialized, ensuring that hello required **ipSecurity** section is unlocked.</span></span>

<span data-ttu-id="d3eac-156">Son olarak, hello değiştirme [system.webServer bölümü](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) web rolün **web.config** tooadd erişim izni IP adresleri listesi hello aşağıdaki örnekte gösterildiği gibi dosya:</span><span class="sxs-lookup"><span data-stu-id="d3eac-156">Finally, modify hello [system.webServer section](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) your web role’s **web.config** file tooadd a list of IP addresses that are granted access, as shown in hello following example:</span></span>

<span data-ttu-id="d3eac-157">Bu örnek yapılandırma **sağlayan** tüm IP'ler tooaccess iki tanımlanmış hello dışında sunucu hello</span><span class="sxs-lookup"><span data-stu-id="d3eac-157">This sample config **allows** all IPs tooaccess hello server except hello two defined</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are granted access-->
    <ipSecurity>
        <!--hello following IP addresses are denied access-->
        <add allowed="false" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="false" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

<span data-ttu-id="d3eac-158">Bu örnek yapılandırma **engellediği** hello sunucu hello tanımlanan iki dışında erişimini tüm IP'ler.</span><span class="sxs-lookup"><span data-stu-id="d3eac-158">This sample config **denies** all IPs from accessing hello server except for hello two defined.</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are denied access-->
    <ipSecurity allowUnlisted="false">
        <!--hello following IP addresses are granted access-->
        <add allowed="true" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="true" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

## <a name="create-a-powershell-startup-task"></a><span data-ttu-id="d3eac-159">PowerShell başlangıç görev oluşturma</span><span class="sxs-lookup"><span data-stu-id="d3eac-159">Create a PowerShell startup task</span></span>
<span data-ttu-id="d3eac-160">Windows PowerShell komut dosyalarını doğrudan hello çağrılamaz [ServiceDefinition.csdef] dosyası, ancak bunlar çağrılabilir gelen bir başlangıç toplu iş dosyası içinde.</span><span class="sxs-lookup"><span data-stu-id="d3eac-160">Windows PowerShell scripts cannot be called directly from hello [ServiceDefinition.csdef] file, but they can be invoked from within a startup batch file.</span></span>

<span data-ttu-id="d3eac-161">PowerShell (varsayılan), imzalanmamış komut dosyalarının çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="d3eac-161">PowerShell (by default) does not run unsigned scripts.</span></span> <span data-ttu-id="d3eac-162">Kodunuzu oturum sürece tooconfigure PowerShell gereksinim toorun imzalanmamış komut dosyaları.</span><span class="sxs-lookup"><span data-stu-id="d3eac-162">Unless you sign your script, you need tooconfigure PowerShell toorun unsigned scripts.</span></span> <span data-ttu-id="d3eac-163">toorun imzalanmamış komut dosyaları hello **ExecutionPolicy** çok ayarlanmalıdır**Kısıtlanmamış**.</span><span class="sxs-lookup"><span data-stu-id="d3eac-163">toorun unsigned scripts, hello **ExecutionPolicy** must be set too**Unrestricted**.</span></span> <span data-ttu-id="d3eac-164">Merhaba **ExecutionPolicy** ayarına kullanım Windows PowerShell hello sürümü temel alır.</span><span class="sxs-lookup"><span data-stu-id="d3eac-164">hello **ExecutionPolicy** setting that you use is based on hello version of Windows PowerShell.</span></span>

```cmd
REM   Run an unsigned PowerShell script and log hello output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

<span data-ttu-id="d3eac-165">1.0, sürüm 2 toorun zorlayabilirsiniz veya bir konuk çalıştırır PowerShell 2.0 olan işletim sistemi kullanıyorsanız ve bu mümkün değilse, sürüm 1 kullanın.</span><span class="sxs-lookup"><span data-stu-id="d3eac-165">If you're using a Guest OS that is runs PowerShell 2.0 or 1.0 you can force version 2 toorun, and if unavailable, use version 1.</span></span>

```cmd
REM   Attempt tooset hello execution policy by using PowerShell version 2.0 syntax.
PowerShell -Version 2.0 -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If PowerShell version 2.0 isn't available. Set hello execution policy by using hello PowerShell
IF %ERRORLEVEL% EQU -393216 (
   PowerShell -Command "Set-ExecutionPolicy Unrestricted" >> "%TEMP%\StartupLog.txt" 2>&1
   PowerShell .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1
)

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="create-files-in-local-storage-from-a-startup-task"></a><span data-ttu-id="d3eac-166">Yerel depolama biriminden bir başlangıç görevi dosyaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="d3eac-166">Create files in local storage from a startup task</span></span>
<span data-ttu-id="d3eac-167">Yerel depolama kaynağı toostore kullanabilirsiniz, daha sonra uygulamanız tarafından erişilebilen, başlangıç görevi tarafından oluşturulan dosyalar.</span><span class="sxs-lookup"><span data-stu-id="d3eac-167">You can use a local storage resource toostore files created by your startup task that is accessed later by your application.</span></span>

<span data-ttu-id="d3eac-168">toocreate Merhaba yerel depolama kaynağı, ekleme bir [LocalResources] bölüm toohello [ServiceDefinition.csdef] dosya ve hello ekleyin [LocalStorage] alt öğesi.</span><span class="sxs-lookup"><span data-stu-id="d3eac-168">toocreate hello local storage resource, add a [LocalResources] section toohello [ServiceDefinition.csdef] file and then add hello [LocalStorage] child element.</span></span> <span data-ttu-id="d3eac-169">Merhaba yerel depolama kaynağı başlangıç görev için benzersiz bir ad ve uygun bir boyut verin.</span><span class="sxs-lookup"><span data-stu-id="d3eac-169">Give hello local storage resource a unique name and an appropriate size for your startup task.</span></span>

<span data-ttu-id="d3eac-170">Başlangıç görevi, yerel depolama kaynağı toouse, toocreate bir ortam değişkeni tooreference hello yerel depolama kaynak konumu gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-170">toouse a local storage resource in your startup task, you need toocreate an environment variable tooreference hello local storage resource location.</span></span> <span data-ttu-id="d3eac-171">Başlangıç görevi hello ve Merhaba uygulaması mümkün tooread ve dosyaları toohello yerel depolama kaynağı yazma.</span><span class="sxs-lookup"><span data-stu-id="d3eac-171">Then hello startup task and hello application are able tooread and write files toohello local storage resource.</span></span>

<span data-ttu-id="d3eac-172">Merhaba hello ilgili bölümleri **ServiceDefinition.csdef** dosya burada gösterilir:</span><span class="sxs-lookup"><span data-stu-id="d3eac-172">hello relevant sections of hello **ServiceDefinition.csdef** file are shown here:</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">
    ...

    <LocalResources>
      <LocalStorage name="StartupLocalStorage" sizeInMB="5"/>
    </LocalResources>

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="PathToStartupStorage">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
  </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="d3eac-173">Örnek olarak, bu **Startup.cmd** toplu iş dosyası kullanan hello **PathToStartupStorage** ortam değişkeni toocreate hello dosya **MyTest.txt** hello yerel depolama konum.</span><span class="sxs-lookup"><span data-stu-id="d3eac-173">As an example, this **Startup.cmd** batch file uses hello **PathToStartupStorage** environment variable toocreate hello file **MyTest.txt** on hello local storage location.</span></span>

```cmd
REM   Create a simple text file.

ECHO This text will go into hello MyTest.txt file which will be in hello    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed tooby hello PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO hello contents of hello PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit hello batch file with ERRORLEVEL 0.

EXIT /b 0
```

<span data-ttu-id="d3eac-174">Hello kullanarak yerel depolama klasörü hello Azure SDK ' erişebilirsiniz [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d3eac-174">You can access local storage folder from hello Azure SDK by using hello [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-hello-emulator-or-cloud"></a><span data-ttu-id="d3eac-175">Merhaba öykünücü veya Bulut çalıştırın</span><span class="sxs-lookup"><span data-stu-id="d3eac-175">Run in hello emulator or cloud</span></span>
<span data-ttu-id="d3eac-176">Merhaba işlem öykünücüsü olduğu hello karşılaştırıldığında bulut toowhen içinde çalışırken farklı adımları gerçekleştirmeniz, başlangıç görevi olabilir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-176">You can have your startup task perform different steps when it is operating in hello cloud compared toowhen it is in hello compute emulator.</span></span> <span data-ttu-id="d3eac-177">Örneğin, yalnızca hello öykünücüsünde çalışırken toouse SQL verilerinizi yeni bir kopyasını isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3eac-177">For example, you may want toouse a fresh copy of your SQL data only when running in hello emulator.</span></span> <span data-ttu-id="d3eac-178">Veya hello öykünücüsünde çalıştırırken toodo gerekmeyen hello bulut için bazı performans iyileştirmelerini toodo isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3eac-178">Or you may want toodo some performance optimizations for hello cloud that you don't need toodo when running in hello emulator.</span></span>

<span data-ttu-id="d3eac-179">Bu özelliği tooperform hello eylemleri işlem öykünücüsü ve hello bulut hello bir ortam değişkeni oluşturarak gerçekleştirilebilir farklı [ServiceDefinition.csdef] dosya.</span><span class="sxs-lookup"><span data-stu-id="d3eac-179">This ability tooperform different actions on hello compute emulator and hello cloud can be accomplished by creating an environment variable in hello [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="d3eac-180">Ardından, başlangıç görevi bu ortam değişkenine bir değer için sınayın.</span><span class="sxs-lookup"><span data-stu-id="d3eac-180">You then test that environment variable for a value in your startup task.</span></span>

<span data-ttu-id="d3eac-181">toocreate hello ortam değişkeni hello eklemek [değişkeni]/[RoleInstanceValue] öğesi ve bir XPath değeri oluşturun `/RoleEnvironment/Deployment/@emulated`.</span><span class="sxs-lookup"><span data-stu-id="d3eac-181">toocreate hello environment variable, add hello [Variable]/[RoleInstanceValue] element and create an XPath value of `/RoleEnvironment/Deployment/@emulated`.</span></span> <span data-ttu-id="d3eac-182">Merhaba hello değerini **ComputeEmulatorRunning %** ortam değişkenidir `true` hello işlem öykünücüsü üzerinde çalışırken ve `false` hello bulut üzerinde çalışırken.</span><span class="sxs-lookup"><span data-stu-id="d3eac-182">hello value of hello **%ComputeEmulatorRunning%** environment variable is `true` when running on hello compute emulator, and `false` when running on hello cloud.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">

    ...

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>

  </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="d3eac-183">Başlangıç görevi şimdi hello denetimi **ComputeEmulatorRunning %** olup hello hello rolünü çalıştıran bağlı ortam değişkeni tooperform farklı eylemleri Bulut veya öykünücü hello.</span><span class="sxs-lookup"><span data-stu-id="d3eac-183">hello task can now check hello **%ComputeEmulatorRunning%** environment variable tooperform different actions based on whether hello role is running in hello cloud or hello emulator.</span></span> <span data-ttu-id="d3eac-184">Bu ortam değişkeninin denetler .cmd Kabuk betiği'dir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-184">Here is a .cmd shell script that checks for that environment variable.</span></span>

```cmd
REM   Check if this task is running on hello compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on hello compute emulator. Perform tasks that must be run only in hello compute emulator.
) ELSE (
    REM   This task is running on hello cloud. Perform tasks that must be run only in hello cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a><span data-ttu-id="d3eac-185">Görevinizi zaten çalıştırılıp çalıştırılmadığını Algıla</span><span class="sxs-lookup"><span data-stu-id="d3eac-185">Detect that your task has already run</span></span>
<span data-ttu-id="d3eac-186">Merhaba rol başlangıç görevleri toorun tekrar yapmasına neden yeniden başlatma geri dönüşüm.</span><span class="sxs-lookup"><span data-stu-id="d3eac-186">hello role may recycle without a reboot causing your startup tasks toorun again.</span></span> <span data-ttu-id="d3eac-187">Bir görev VM barındırma hello üzerinde önceden çalıştırıldıktan hiçbir bayrağı tooindicate yoktur.</span><span class="sxs-lookup"><span data-stu-id="d3eac-187">There is no flag tooindicate that a task has already run on hello hosting VM.</span></span> <span data-ttu-id="d3eac-188">Birden çok kez çalıştırmak olduğu önemli değildir, bazı görevler de sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-188">You may have some tasks where it doesn't matter that they run multiple times.</span></span> <span data-ttu-id="d3eac-189">Ancak, birden çok kez çalışan bir görev tooprevent ihtiyaç duyacağınız bir durumla çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3eac-189">However, you may run into a situation where you need tooprevent a task from running more than once.</span></span>

<span data-ttu-id="d3eac-190">bir görev zaten çalışan hello en basit yolu toodetect olan toocreate hello dosyasında **% TEMP %** hello görev başarılı olduğunda klasörü ve hello de göz hello görevini Başlat.</span><span class="sxs-lookup"><span data-stu-id="d3eac-190">hello simplest way toodetect that a task has already run is toocreate a file in hello **%TEMP%** folder when hello task is successful and look for it at hello start of hello task.</span></span> <span data-ttu-id="d3eac-191">Sizin için yapar bir örnek cmd Kabuk betiği'dir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-191">Here is a sample cmd shell script that does that for you.</span></span>

```cmd
REM   If Task1_Success.txt exists, then Application 1 is already installed.
IF EXIST "%RoleRoot%\Task1_Success.txt" (
  ECHO Application 1 is already installed. Exiting. >> "%TEMP%\StartupLog.txt" 2>&1
  GOTO Finish
)

REM   Run your real exe task
ECHO Running XYZ >> "%TEMP%\StartupLog.txt" 2>&1
"%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (
  REM   hello application installed without error. Create a file tooindicate that hello task
  REM   does not need toobe run again.

  ECHO This line will create a file tooindicate that Application 1 installed correctly. > "%RoleRoot%\Task1_Success.txt"

) ELSE (
  REM   An error occurred. Log hello error and exit with hello error code.

  DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
  TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
  ECHO  An error occurred running task 1. Errorlevel = %ERRORLEVEL%. >> "%TEMP%\StartupLog.txt" 2>&1

  EXIT %ERRORLEVEL%
)

:Finish

REM   Exit normally.
EXIT /B 0
```

## <a name="task-best-practices"></a><span data-ttu-id="d3eac-192">Görev en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="d3eac-192">Task best practices</span></span>
<span data-ttu-id="d3eac-193">Görev web veya çalışan rolü için yapılandırırken izlemeniz gereken bazı en iyi uygulamalar şunlardır.</span><span class="sxs-lookup"><span data-stu-id="d3eac-193">Here are some best practices you should follow when configuring task for your web or worker role.</span></span>

### <a name="always-log-startup-activities"></a><span data-ttu-id="d3eac-194">Her zaman günlük başlangıç etkinlikleri</span><span class="sxs-lookup"><span data-stu-id="d3eac-194">Always log startup activities</span></span>
<span data-ttu-id="d3eac-195">İyi tooget olacak şekilde visual Studio hata ayıklayıcısı toostep toplu iş dosyaları kadar veri toplu iş dosyaları hello işlemi mümkün olduğunca üzerinde sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="d3eac-195">Visual Studio does not provide a debugger toostep through batch files, so it's good tooget as much data on hello operation of batch files as possible.</span></span> <span data-ttu-id="d3eac-196">Toplu iş dosyaları Hello çıktısı günlüğü her ikisi de **stdout** ve **stderr**, toodebug çalışırken önemli bilgileri verin ve toplu iş dosyaları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="d3eac-196">Logging hello output of batch files, both **stdout** and **stderr**, can give you important information when trying toodebug and fix batch files.</span></span> <span data-ttu-id="d3eac-197">toolog hem **stdout** ve **stderr** toohello StartupLog.txt hello dizine işaret tooby hello dosyasında **% TEMP %** ortam değişkeni hello metin ekleme`>>  "%TEMP%\\StartupLog.txt" 2>&1`özel toohello sonuna satırları toolog istiyor.</span><span class="sxs-lookup"><span data-stu-id="d3eac-197">toolog both **stdout** and **stderr** toohello StartupLog.txt file in hello directory pointed tooby hello **%TEMP%** environment variable, add hello text `>>  "%TEMP%\\StartupLog.txt" 2>&1` toohello end of specific lines you want toolog.</span></span> <span data-ttu-id="d3eac-198">Örneğin, hello tooexecute setup.exe **PathToApp1Install %** dizini:</span><span class="sxs-lookup"><span data-stu-id="d3eac-198">For example, tooexecute setup.exe in hello **%PathToApp1Install%** directory:</span></span>

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

<span data-ttu-id="d3eac-199">toosimplify, xml, bir sarmalayıcı oluşturur *cmd* tüm, başlangıç çağrılar dosya görevlerin yanı sıra günlüğe kaydetme ve her alt görev paylaşımları hello aynı ortam değişkenleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="d3eac-199">toosimplify your xml, you can create a wrapper *cmd* file that calls all of your startup tasks along with logging and ensures each child-task shares hello same environment variables.</span></span>

<span data-ttu-id="d3eac-200">Ancak toouse sinir bozucu bulabilirsiniz `>> "%TEMP%\StartupLog.txt" 2>&1` her başlangıç görevi hello ucunda.</span><span class="sxs-lookup"><span data-stu-id="d3eac-200">You may find it annoying though toouse `>> "%TEMP%\StartupLog.txt" 2>&1` on hello end of each startup task.</span></span> <span data-ttu-id="d3eac-201">Görev günlüğü, günlük kaydı işleyen bir sarmalayıcı oluşturarak uygulayabilir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-201">You can enforce task logging by creating a wrapper that handles logging for you.</span></span> <span data-ttu-id="d3eac-202">Bu sarmalayıcı toorun istediğiniz hello gerçek toplu iş dosyasını çağırır.</span><span class="sxs-lookup"><span data-stu-id="d3eac-202">This wrapper calls hello real batch file you want toorun.</span></span> <span data-ttu-id="d3eac-203">Herhangi bir çıktı hello hedef toplu iş dosyasından yeniden yönlendirilen toohello olacaktır *Startuplog.txt* dosya.</span><span class="sxs-lookup"><span data-stu-id="d3eac-203">Any output from hello target batch file will be redirected toohello *Startuplog.txt* file.</span></span>

<span data-ttu-id="d3eac-204">Aşağıdaki örneğine hello tooredirect tüm bir başlangıç toplu iş dosyasından nasıl çıktısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-204">hello following example shows how tooredirect all output from a startup batch file.</span></span> <span data-ttu-id="d3eac-205">Bu örnekte, çağıran bir başlangıç görevi hello ServerDefinition.csdef dosyası oluşturur *logwrap.cmd*.</span><span class="sxs-lookup"><span data-stu-id="d3eac-205">In this example, hello ServerDefinition.csdef file creates a startup task that calls *logwrap.cmd*.</span></span> <span data-ttu-id="d3eac-206">*logwrap.cmd* çağrıları *Startup2.cmd*, tüm çıktı çok yönlendirme**% TEMP %\\StartupLog.txt**.</span><span class="sxs-lookup"><span data-stu-id="d3eac-206">*logwrap.cmd* calls *Startup2.cmd*, redirecting all output too**%TEMP%\\StartupLog.txt**.</span></span>

<span data-ttu-id="d3eac-207">ServiceDefinition.cmd:</span><span class="sxs-lookup"><span data-stu-id="d3eac-207">ServiceDefinition.cmd:</span></span>

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

<span data-ttu-id="d3eac-208">**logwrap.cmd:**</span><span class="sxs-lookup"><span data-stu-id="d3eac-208">**logwrap.cmd:**</span></span>

```cmd
@ECHO OFF

REM   logwrap.cmd calls passed in batch file, redirecting all output toohello StartupLog.txt log file.

ECHO [%date% %time%] == START logwrap.cmd ============================================== >> "%TEMP%\StartupLog.txt" 2>&1
ECHO [%date% %time%] Running %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Call hello child command batch file, redirecting all output toohello StartupLog.txt log file.
START /B /WAIT %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Log hello completion of child command.
ECHO [%date% %time%] Done >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (

   REM   No errors occurred. Exit logwrap.cmd normally.
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B 0

) ELSE (

   REM   Log hello error.
   ECHO [%date% %time%] An error occurred. hello ERRORLEVEL = %ERRORLEVEL%.  >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B %ERRORLEVEL%

)
```

<span data-ttu-id="d3eac-209">**Startup2.cmd:**</span><span class="sxs-lookup"><span data-stu-id="d3eac-209">**Startup2.cmd:**</span></span>

```cmd
@ECHO OFF

REM   This is hello batch file where hello startup steps should be performed. Because of the
REM   way Startup2.cmd was called, all commands and their outputs will be stored in the
REM   StartupLog.txt file in hello directory pointed tooby hello TEMP environment variable.

REM   If an error occurs, hello following command will pass hello ERRORLEVEL back toothe
REM   calling batch file.

ECHO [%date% %time%] Some log information about this task
ECHO [%date% %time%] Some more log information about this task

EXIT %ERRORLEVEL%
```

<span data-ttu-id="d3eac-210">Örnek hello çıktısında **StartupLog.txt** dosyası:</span><span class="sxs-lookup"><span data-stu-id="d3eac-210">Sample output in hello **StartupLog.txt** file:</span></span>

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> <span data-ttu-id="d3eac-211">Merhaba **StartupLog.txt** dosya hello bulunur *C:\Resources\temp\\{rol tanımlayıcısı} \RoleTemp* klasör.</span><span class="sxs-lookup"><span data-stu-id="d3eac-211">hello **StartupLog.txt** file is located in hello *C:\Resources\temp\\{role identifier}\RoleTemp* folder.</span></span>
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a><span data-ttu-id="d3eac-212">Başlangıç görevi için uygun şekilde executionContext ayarlayın</span><span class="sxs-lookup"><span data-stu-id="d3eac-212">Set executionContext appropriately for startup tasks</span></span>
<span data-ttu-id="d3eac-213">Ayrıcalıkları hello başlangıç görevi için uygun şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d3eac-213">Set privileges appropriately for hello startup task.</span></span> <span data-ttu-id="d3eac-214">Bazen normal ayrıcalıklara sahip Hello rolünü çalıştıran olsa bile başlangıç görevleri yükseltilmiş ayrıcalıklarla çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-214">Sometimes startup tasks must run with elevated privileges even though hello role runs with normal privileges.</span></span>

<span data-ttu-id="d3eac-215">Merhaba [executionContext][görev] öznitelik hello başlangıç görevi hello öncelik düzeyi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d3eac-215">hello [executionContext][Task] attribute sets hello privilege level of hello startup task.</span></span> <span data-ttu-id="d3eac-216">Kullanarak `executionContext="limited"` hello hello rolü olarak aynı ayrıcalık düzeyi hello başlangıç görevinin anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-216">Using `executionContext="limited"` means hello startup task has hello same privilege level as hello role.</span></span> <span data-ttu-id="d3eac-217">Kullanarak `executionContext="elevated"` hello başlangıç görevi, yönetici ayrıcalıkları tooyour rol vermeden görev tooperform yönetici görevleri sağlayan hello başlangıç yönetici ayrıcalıklarına sahip anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-217">Using `executionContext="elevated"` means hello startup task has administrator privileges, which allows hello startup task tooperform administrator tasks without giving administrator privileges tooyour role.</span></span>

<span data-ttu-id="d3eac-218">Yükseltilmiş ayrıcalıklar gerektiren bir başlangıç görevi kullanan bir başlangıç görevi örneğidir **AppCmd.exe** tooconfigure IIS.</span><span class="sxs-lookup"><span data-stu-id="d3eac-218">An example of a startup task that requires elevated privileges is a startup task that uses **AppCmd.exe** tooconfigure IIS.</span></span> <span data-ttu-id="d3eac-219">**AppCmd.exe** gerektirir `executionContext="elevated"`.</span><span class="sxs-lookup"><span data-stu-id="d3eac-219">**AppCmd.exe** requires `executionContext="elevated"`.</span></span>

### <a name="use-hello-appropriate-tasktype"></a><span data-ttu-id="d3eac-220">Merhaba uygun taskType kullanın</span><span class="sxs-lookup"><span data-stu-id="d3eac-220">Use hello appropriate taskType</span></span>
<span data-ttu-id="d3eac-221">Merhaba [taskType][görev] özniteliği belirler hello şekilde hello başlangıç görevi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-221">hello [taskType][Task] attribute determines hello way hello startup task is executed.</span></span> <span data-ttu-id="d3eac-222">Üç değer vardır: **basit**, **arka plan**, ve **ön plan**.</span><span class="sxs-lookup"><span data-stu-id="d3eac-222">There are three values: **simple**, **background**, and **foreground**.</span></span> <span data-ttu-id="d3eac-223">Merhaba arka plan ve ön plan görevleri zaman uyumsuz olarak başlatılır ve ardından hello Basit görevler eşzamanlı olarak yürütülen bir kerede.</span><span class="sxs-lookup"><span data-stu-id="d3eac-223">hello background and foreground tasks are started asynchronously, and then hello simple tasks are executed synchronously one at a time.</span></span>

<span data-ttu-id="d3eac-224">İle **basit** başlangıç görevleri, başlangıç görevleri çalıştırdığınız hello siparişe hangi hello görevleri hello ServiceDefinition.csdef dosyasında listelenen hello göre ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3eac-224">With **simple** startup tasks, you can set hello order in which hello tasks run by hello order in which hello tasks are listed in hello ServiceDefinition.csdef file.</span></span> <span data-ttu-id="d3eac-225">Varsa bir **basit** görev biter sıfır olmayan çıkış kodu, ardından hello başlangıç yordamı durdurur ve hello rol başlatılmaz.</span><span class="sxs-lookup"><span data-stu-id="d3eac-225">If a **simple** task ends with a non-zero exit code, then hello startup procedure stops and hello role does not start.</span></span>

<span data-ttu-id="d3eac-226">Merhaba arasındaki farkı **arka plan** başlangıç görevleri ve **ön plan** başlangıç görevleri olan **ön plan** görevleri tutmak hello rol çalışan hello kadar  **ön plan** görev sona erer.</span><span class="sxs-lookup"><span data-stu-id="d3eac-226">hello difference between **background** startup tasks and **foreground** startup tasks is that **foreground** tasks keep hello role running until hello **foreground** task ends.</span></span> <span data-ttu-id="d3eac-227">Bu ayrıca, hello anlamına gelir **ön plan** görevin askıda kalmasına ya da çökme (Crash), hello rol değil geri dönüşüm hello kadar **ön plan** görev zorunlu kapalı.</span><span class="sxs-lookup"><span data-stu-id="d3eac-227">This also means that if hello **foreground** task hangs or crashes, hello role will not recycle until hello **foreground** task is forced closed.</span></span> <span data-ttu-id="d3eac-228">Bu nedenle, **arka plan** görevleri hello bu özelliği gerekmedikçe zaman uyumsuz başlangıç görevleri için önerilen **ön plan** görev.</span><span class="sxs-lookup"><span data-stu-id="d3eac-228">For this reason, **background** tasks are recommended for asynchronous startup tasks unless you need that feature of hello **foreground** task.</span></span>

### <a name="end-batch-files-with-exit-b-0"></a><span data-ttu-id="d3eac-229">Çık /B 0 ile son toplu iş dosyaları</span><span class="sxs-lookup"><span data-stu-id="d3eac-229">End batch files with EXIT /B 0</span></span>
<span data-ttu-id="d3eac-230">Merhaba rolü yalnızca Merhaba, başlatacak **errorlevel** her basit başlangıç sıfır görevdir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-230">hello role will only start if hello **errorlevel** from each of your simple startup task is zero.</span></span> <span data-ttu-id="d3eac-231">Tüm programları hello Ayarla **errorlevel** (çıkış kodu), doğru şekilde hello toplu iş dosyası bitmelidir bir `EXIT /B 0` her şeyin doğru şekilde çalıştırdıysanız.</span><span class="sxs-lookup"><span data-stu-id="d3eac-231">Not all programs set hello **errorlevel** (exit code) correctly, so hello batch file should end with an `EXIT /B 0` if everything ran correctly.</span></span>

<span data-ttu-id="d3eac-232">Eksik `EXIT /B 0` hello başlangıç toplu dosyasının sonuna bir ortak başlatılmaz rolleri nedenidir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-232">A missing `EXIT /B 0` at hello end of a startup batch file is a common cause of roles that do not start.</span></span>

> [!NOTE]
> <span data-ttu-id="d3eac-233">İç içe geçmiş toplu fark ettim dosyalar bazen askıda hello kullanırken `/B` parametresi.</span><span class="sxs-lookup"><span data-stu-id="d3eac-233">I've noticed that nested batch files sometimes hang when using hello `/B` parameter.</span></span> <span data-ttu-id="d3eac-234">Başka bir toplu iş dosyası, geçerli toplu iş dosyasını çağırıyorsa ister hello kullanırsanız, bu yanıt vermemesine sorun gerçekleşmez emin toomake isteyebilir [günlük sarmalayıcı](#always-log-startup-activities).</span><span class="sxs-lookup"><span data-stu-id="d3eac-234">You may want toomake sure that this hang problem does not happen if another batch file calls your current batch file, like if you use hello [log wrapper](#always-log-startup-activities).</span></span> <span data-ttu-id="d3eac-235">Merhaba atlayabilirsiniz `/B` parametresi bu durumda.</span><span class="sxs-lookup"><span data-stu-id="d3eac-235">You can omit hello `/B` parameter in this case.</span></span>
> 
> 

### <a name="expect-startup-tasks-toorun-more-than-once"></a><span data-ttu-id="d3eac-236">Başlangıç görevleri toorun birden çok kez beklediğiniz</span><span class="sxs-lookup"><span data-stu-id="d3eac-236">Expect startup tasks toorun more than once</span></span>
<span data-ttu-id="d3eac-237">Yeniden başlatma tüm rol dönüştürür içerir, ancak çalışan tüm başlangıç görevleri tüm rol dönüştürür içerir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-237">Not all role recycles include a reboot, but all role recycles include running all startup tasks.</span></span> <span data-ttu-id="d3eac-238">Bu, başlangıç görevleri birden çok kez herhangi bir sorun olmadan yeniden başlatmalar arasında mümkün toorun olması gerektiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-238">This means that startup tasks must be able toorun multiple times between reboots without any problems.</span></span> <span data-ttu-id="d3eac-239">Bu hello ele alınmıştır [bölüm önceki](#detect-that-your-task-has-already-run).</span><span class="sxs-lookup"><span data-stu-id="d3eac-239">This is discussed in hello [preceding section](#detect-that-your-task-has-already-run).</span></span>

### <a name="use-local-storage-toostore-files-that-must-be-accessed-in-hello-role"></a><span data-ttu-id="d3eac-240">Merhaba rolünde erişilmelidir yerel depolama toostore dosyaları kullanma</span><span class="sxs-lookup"><span data-stu-id="d3eac-240">Use local storage toostore files that must be accessed in hello role</span></span>
<span data-ttu-id="d3eac-241">Toocopy istediğiniz ya da başlangıç görev sırasında bir dosya oluşturun, sonra erişilebilir tooyour rolüdür sonra bu dosyayı yerel depolama alanına yerleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="d3eac-241">If you want toocopy or create a file during your startup task that is then accessible tooyour role, then that file must be placed in local storage.</span></span> <span data-ttu-id="d3eac-242">Merhaba bkz [bölüm önceki](#create-files-in-local-storage-from-a-startup-task).</span><span class="sxs-lookup"><span data-stu-id="d3eac-242">See hello [preceding section](#create-files-in-local-storage-from-a-startup-task).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3eac-243">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d3eac-243">Next steps</span></span>
<span data-ttu-id="d3eac-244">Gözden hello bulut [hizmet modeli ve paket](cloud-services-model-and-package.md)</span><span class="sxs-lookup"><span data-stu-id="d3eac-244">Review hello cloud [service model and package](cloud-services-model-and-package.md)</span></span>

<span data-ttu-id="d3eac-245">Hakkında daha fazla bilgi [görevleri](cloud-services-startup-tasks.md) çalışır.</span><span class="sxs-lookup"><span data-stu-id="d3eac-245">Learn more about how [Tasks](cloud-services-startup-tasks.md) work.</span></span>

<span data-ttu-id="d3eac-246">[Oluşturma ve dağıtma](cloud-services-how-to-create-deploy-portal.md) , bulut hizmet paketi.</span><span class="sxs-lookup"><span data-stu-id="d3eac-246">[Create and deploy](cloud-services-how-to-create-deploy-portal.md) your cloud service package.</span></span>

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[görev]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[ortam]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[değişkeni]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
[Uç noktaları]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints
[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage
[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
