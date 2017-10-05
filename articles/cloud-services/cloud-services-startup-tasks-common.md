---
title: "Bulut Hizmetleri için genel başlangıç görevleri | Microsoft Docs"
description: "Bulut Hizmetleri web rolü ya da çalışan rolü gerçekleştirmek istediğinizi düşünelim ortak başlangıç görevleri, bazı örnekler sağlar."
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
ms.openlocfilehash: cee23da5b089b02bfc0ef10afd60f0f2272585b1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="common-cloud-service-startup-tasks"></a><span data-ttu-id="86c46-103">Genel bulut hizmeti başlangıç görevleri</span><span class="sxs-lookup"><span data-stu-id="86c46-103">Common Cloud Service startup tasks</span></span>
<span data-ttu-id="86c46-104">Bu makale, bulut hizmetinizin gerçekleştirmek istediğinizi düşünelim ortak başlangıç görevleri, bazı örnekler sağlar.</span><span class="sxs-lookup"><span data-stu-id="86c46-104">This article provides some examples of common startup tasks you may want to perform in your cloud service.</span></span> <span data-ttu-id="86c46-105">Başlangıç görevi, bir rol başlamadan önce işlemlerini gerçekleştirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86c46-105">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="86c46-106">Bir bileşeni yüklemek, COM bileşenlerini kaydetme, kayıt defteri anahtarlarını ayarlamak veya uzun süre çalışan bir işlem başlatılıyor gerçekleştirmek isteyebileceğiniz işlemleri içerir.</span><span class="sxs-lookup"><span data-stu-id="86c46-106">Operations that you might want to perform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span> 

<span data-ttu-id="86c46-107">Bkz: [bu makalede](cloud-services-startup-tasks.md) nasıl iş başlangıç görevleri ve bir başlangıç görevi tanımlayan girişinin özellikle nasıl oluşturulacağını öğrenmek için.</span><span class="sxs-lookup"><span data-stu-id="86c46-107">See [this article](cloud-services-startup-tasks.md) to understand how startup tasks work, and specifically how to create the entries that define a startup task.</span></span>

> [!NOTE]
> <span data-ttu-id="86c46-108">Başlangıç görevi sanal makineler için yalnızca bulut hizmeti Web ve çalışan rolleri için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="86c46-108">Startup tasks are not applicable to Virtual Machines, only to Cloud Service Web and Worker roles.</span></span>
> 

## <a name="define-environment-variables-before-a-role-starts"></a><span data-ttu-id="86c46-109">Bir rolü başlatılmadan önce ortamı değişkenleri tanımlayın</span><span class="sxs-lookup"><span data-stu-id="86c46-109">Define environment variables before a role starts</span></span>
<span data-ttu-id="86c46-110">Belirli bir görev için tanımlanan ortam değişkenlerini gerekiyorsa kullanın [ortam] öğesi içinde [görev] öğesi.</span><span class="sxs-lookup"><span data-stu-id="86c46-110">If you need environment variables defined for a specific task, use the [Environment] element inside the [Task] element.</span></span>

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

<span data-ttu-id="86c46-111">Değişkenleri de kullanabilir bir [geçerli Azure XPath değeri](cloud-services-role-config-xpath.md) dağıtımı hakkında bir şey başvurmak için.</span><span class="sxs-lookup"><span data-stu-id="86c46-111">Variables can also use a [valid Azure XPath value](cloud-services-role-config-xpath.md) to reference something about the deployment.</span></span> <span data-ttu-id="86c46-112">Yerine `value` özniteliği, tanımlayan bir [RoleInstanceValue] alt öğesi.</span><span class="sxs-lookup"><span data-stu-id="86c46-112">Instead of using the `value` attribute, define a [RoleInstanceValue] child element.</span></span>

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a><span data-ttu-id="86c46-113">IIS Başlangıç AppCmd.exe ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="86c46-113">Configure IIS startup with AppCmd.exe</span></span>
<span data-ttu-id="86c46-114">[AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) komut satırı aracı, Azure üzerinde başlangıçta IIS ayarlarını yönetmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="86c46-114">The [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) command-line tool can be used to manage IIS settings at startup on Azure.</span></span> <span data-ttu-id="86c46-115">*AppCmd.exe* yapılandırma ayarlarına başlangıç görevleri Azure ile ilgili kullanım için kullanışlı, komut satırı erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="86c46-115">*AppCmd.exe* provides convenient, command-line access to configuration settings for use in startup tasks on Azure.</span></span> <span data-ttu-id="86c46-116">Kullanarak *AppCmd.exe*, Web sitesi ayarlarını eklenemez, değiştiren veya uygulamaları ve sitelerin kaldırılamaz.</span><span class="sxs-lookup"><span data-stu-id="86c46-116">Using *AppCmd.exe*, Website settings can be added, modified, or removed for applications and sites.</span></span>

<span data-ttu-id="86c46-117">Ancak, kullanımda dikkat edilmesi gereken birkaç şey vardır *AppCmd.exe* bir başlangıç görevi olarak:</span><span class="sxs-lookup"><span data-stu-id="86c46-117">However, there are a few things to watch out for in the use of *AppCmd.exe* as a startup task:</span></span>

* <span data-ttu-id="86c46-118">Başlangıç görevi birden çok kez yeniden başlatmalar arasında çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86c46-118">Startup tasks can be run more than once between reboots.</span></span> <span data-ttu-id="86c46-119">Örneğin, ne zaman bir rol geri dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="86c46-119">For instance, when a role recycles.</span></span>
* <span data-ttu-id="86c46-120">Varsa bir *AppCmd.exe* eylem birden çok kez gerçekleştirilir, hataya neden.</span><span class="sxs-lookup"><span data-stu-id="86c46-120">If a *AppCmd.exe* action is performed more than once, it may generate an error.</span></span> <span data-ttu-id="86c46-121">Örneğin, bir bölüme eklenmeye çalışılıyor *Web.config* iki kez hataya neden.</span><span class="sxs-lookup"><span data-stu-id="86c46-121">For example, attempting to add a section to *Web.config* twice could generate an error.</span></span>
* <span data-ttu-id="86c46-122">Başlangıç görevleri, sıfır olmayan çıkış kodu döndürmesi durumunda başarısız veya **errorlevel**.</span><span class="sxs-lookup"><span data-stu-id="86c46-122">Startup tasks fail if they return a non-zero exit code or **errorlevel**.</span></span> <span data-ttu-id="86c46-123">Örneğin, *AppCmd.exe* bir hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="86c46-123">For example, when *AppCmd.exe* generates an error.</span></span>

<span data-ttu-id="86c46-124">Denetlemek için iyi bir uygulamadır **errorlevel** çağırdıktan sonra *AppCmd.exe*, çağrısı kaydırma yapın kolay olduğu *AppCmd.exe* ile bir *.cmd* dosya.</span><span class="sxs-lookup"><span data-stu-id="86c46-124">It is a good practice to check the **errorlevel** after calling *AppCmd.exe*, which is easy to do if you wrap the call to *AppCmd.exe* with a *.cmd* file.</span></span> <span data-ttu-id="86c46-125">Bilinen bir algılama **errorlevel** yanıtı yok sayın veya için geri geçirin.</span><span class="sxs-lookup"><span data-stu-id="86c46-125">If you detect a known **errorlevel** response, you can ignore it, or pass it back.</span></span>

<span data-ttu-id="86c46-126">Tarafından döndürülen errorlevel *AppCmd.exe* Winerror.h'de dosyasında listelenir ve ayrıca görülebilir [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span><span class="sxs-lookup"><span data-stu-id="86c46-126">The errorlevel returned by *AppCmd.exe* are listed in the winerror.h file, and can also be seen on [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span></span>

### <a name="example-of-managing-the-error-level"></a><span data-ttu-id="86c46-127">Örnek hata düzeyi yönetme</span><span class="sxs-lookup"><span data-stu-id="86c46-127">Example of managing the error level</span></span>
<span data-ttu-id="86c46-128">Bu örnek için JSON için sıkıştırma bölüm ve bir sıkıştırma girişi ekler *Web.config* dosyasıyla hata işleme ve günlüğe kaydetme.</span><span class="sxs-lookup"><span data-stu-id="86c46-128">This example adds a compression section and a compression entry for JSON to the *Web.config* file, with error handling and logging.</span></span>

<span data-ttu-id="86c46-129">İlgili bölümleri [ServiceDefinition.csdef] dosya burada gösterilen, ayar içeren [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) özniteliğini `elevated` vermek için *AppCmd.exe* ayarları değiştirmek için yeterli izinlere *Web.config* dosyası:</span><span class="sxs-lookup"><span data-stu-id="86c46-129">The relevant sections of the [ServiceDefinition.csdef] file are shown here, which include setting the [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) attribute to `elevated` to give *AppCmd.exe* sufficient permissions to change the settings in the *Web.config* file:</span></span>

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

<span data-ttu-id="86c46-130">*Startup.cmd* toplu iş dosyası kullanır *AppCmd.exe* için JSON için bir sıkıştırma bölümü ve sıkıştırma giriş eklemek için *Web.config* dosya.</span><span class="sxs-lookup"><span data-stu-id="86c46-130">The *Startup.cmd* batch file uses *AppCmd.exe* to add a compression section and a compression entry for JSON to the *Web.config* file.</span></span> <span data-ttu-id="86c46-131">Beklenen **errorlevel** 183 sıfır doğrula kullanmaya ayarlanır. EXE komut satırı programı.</span><span class="sxs-lookup"><span data-stu-id="86c46-131">The expected **errorlevel** of 183 is set to zero using the VERIFY.EXE command-line program.</span></span> <span data-ttu-id="86c46-132">Beklenmeyen errorlevels StartupErrorLog.txt için günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="86c46-132">Unexpected errorlevels are logged to StartupErrorLog.txt.</span></span>

```cmd
REM   *** Add a compression section to the Web.config file. ***
%windir%\system32\inetsrv\appcmd set config /section:urlCompression /doDynamicCompression:True /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1

REM   ERRORLEVEL 183 occurs when trying to add a section that already exists. This error is expected if this
REM   batch file were executed twice. This can occur and must be accounted for in a Azure startup
REM   task. To handle this situation, set the ERRORLEVEL to zero by using the Verify command. The Verify
REM   command will safely set the ERRORLEVEL to zero.
IF %ERRORLEVEL% EQU 183 DO VERIFY > NUL

REM   If the ERRORLEVEL is not zero at this point, some other error occurred.
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding a compression section to the Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Add compression for json. ***
%windir%\system32\inetsrv\appcmd set config  -section:system.webServer/httpCompression /+"dynamicTypes.[mimeType='application/json; charset=utf-8',enabled='True']" /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1
IF %ERRORLEVEL% EQU 183 VERIFY > NUL
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding the JSON compression type to the Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Exit batch file. ***
EXIT /b 0

REM   *** Log error and exit ***
:ErrorExit
REM   Report the date, time, and ERRORLEVEL of the error.
DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
ECHO An error occurred during startup. ERRORLEVEL = %ERRORLEVEL% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT %ERRORLEVEL%
```

## <a name="add-firewall-rules"></a><span data-ttu-id="86c46-133">Güvenlik duvarı kuralları ekleme</span><span class="sxs-lookup"><span data-stu-id="86c46-133">Add firewall rules</span></span>
<span data-ttu-id="86c46-134">Azure üzerinde etkili bir şekilde iki güvenlik duvarı vardır.</span><span class="sxs-lookup"><span data-stu-id="86c46-134">In Azure, there are effectively two firewalls.</span></span> <span data-ttu-id="86c46-135">Güvenlik Duvarı'nı ilk sanal makine ve dış dünya arasındaki bağlantıları denetler.</span><span class="sxs-lookup"><span data-stu-id="86c46-135">The first firewall controls connections between the virtual machine and the outside world.</span></span> <span data-ttu-id="86c46-136">Bu güvenlik duvarı tarafından denetlenen [uç noktaları] öğesinde [ServiceDefinition.csdef] dosya.</span><span class="sxs-lookup"><span data-stu-id="86c46-136">This firewall is controlled by the [EndPoints] element in the [ServiceDefinition.csdef] file.</span></span>

<span data-ttu-id="86c46-137">Güvenlik Duvarı'nı ikinci sanal makine ve sanal makinenin süreçlerinde arasındaki bağlantıları denetler.</span><span class="sxs-lookup"><span data-stu-id="86c46-137">The second firewall controls connections between the virtual machine and the processes within that virtual machine.</span></span> <span data-ttu-id="86c46-138">Bu güvenlik duvarı tarafından denetlenen `netsh advfirewall firewall` komut satırı aracı.</span><span class="sxs-lookup"><span data-stu-id="86c46-138">This firewall can be controlled by the `netsh advfirewall firewall` command-line tool.</span></span>

<span data-ttu-id="86c46-139">Azure güvenlik duvarı kuralları rollerinizi içinde başlatılan işlemleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="86c46-139">Azure creates firewall rules for the processes started within your roles.</span></span> <span data-ttu-id="86c46-140">Örneğin, bir hizmet veya programın başlattığınızda, Azure Internet ile iletişim kurmak bu hizmetin izin vermek için gerekli güvenlik duvarı kuralları otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="86c46-140">For example, when you start a service or program, Azure automatically creates the necessary firewall rules to allow that service to communicate with the Internet.</span></span> <span data-ttu-id="86c46-141">Ancak, rolünüze (örneğin, bir COM + hizmet ya da Windows zamanlanmış bir görev) dışında bir işlem tarafından başlatılan bir hizmet oluşturursanız, bu hizmete erişmesine izin vermek için bir güvenlik duvarı kuralı el ile oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="86c46-141">However, if you create a service that is started by a process outside your role (like a COM+ service or a Windows Scheduled Task), you need to manually create a firewall rule to allow access to that service.</span></span> <span data-ttu-id="86c46-142">Bu güvenlik duvarı kuralları, bir başlangıç görevi kullanılarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="86c46-142">These firewall rules can be created by using a startup task.</span></span>

<span data-ttu-id="86c46-143">Bir güvenlik duvarı kuralı oluşturan bir başlangıç görevi olmalıdır bir [executionContext][görev] , **yükseltilmiş**.</span><span class="sxs-lookup"><span data-stu-id="86c46-143">A startup task that creates a firewall rule must have an [executionContext][Task] of **elevated**.</span></span> <span data-ttu-id="86c46-144">Aşağıdaki başlangıç görevi eklemek [ServiceDefinition.csdef] dosya.</span><span class="sxs-lookup"><span data-stu-id="86c46-144">Add the following startup task to the [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="86c46-145">Güvenlik duvarı kuralı eklemek için uygun kullanmalısınız `netsh advfirewall firewall` başlangıç toplu iş dosyası komutları.</span><span class="sxs-lookup"><span data-stu-id="86c46-145">To add the firewall rule, you must use the appropriate `netsh advfirewall firewall` commands in your startup batch file.</span></span> <span data-ttu-id="86c46-146">Bu örnekte, başlangıç görevi güvenlik ve şifreleme'yi TCP bağlantı noktası 80 gerektirir.</span><span class="sxs-lookup"><span data-stu-id="86c46-146">In this example, the startup task requires security and encryption for TCP port 80.</span></span>

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a><span data-ttu-id="86c46-147">Belirli bir IP adres bloğu</span><span class="sxs-lookup"><span data-stu-id="86c46-147">Block a specific IP address</span></span>
<span data-ttu-id="86c46-148">IIS değiştirerek belirtilen IP adresleri kümesi için bir Azure web rolü erişimi kısıtlayabilirsiniz **web.config** dosya.</span><span class="sxs-lookup"><span data-stu-id="86c46-148">You can restrict an Azure web role access to a set of specified IP addresses by modifying your IIS **web.config** file.</span></span> <span data-ttu-id="86c46-149">Ayrıca kilidini açan bir komut dosyası kullanmanıza gerek **IPSecurity** bölümünü **ApplicationHost.config** dosya.</span><span class="sxs-lookup"><span data-stu-id="86c46-149">You also need to use a command file which unlocks the **ipSecurity** section of the **ApplicationHost.config** file.</span></span>

<span data-ttu-id="86c46-150">Kilidini açmak için **IPSecurity** bölümünü **ApplicationHost.config** dosya, rol başlangıcında çalışan bir komut dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="86c46-150">To do unlock the **ipSecurity** section of the **ApplicationHost.config** file, create a command file that runs at role start.</span></span> <span data-ttu-id="86c46-151">Adlı web rolünüz kök düzeyinde bir klasör oluşturun **başlangıç** ve bu klasör içinde adlı bir toplu iş dosyası oluşturmak **startup.cmd**.</span><span class="sxs-lookup"><span data-stu-id="86c46-151">Create a folder at the root level of your web role called **startup** and, within this folder, create a batch file called **startup.cmd**.</span></span> <span data-ttu-id="86c46-152">Bu dosyayı Visual Studio projenize ekleyin ve özelliklerini ayarlamak **her zaman Kopyala** paketinize bulunduğundan emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="86c46-152">Add this file to your Visual Studio project and set the properties to **Copy Always** to ensure that it is included in your package.</span></span>

<span data-ttu-id="86c46-153">Aşağıdaki başlangıç görevi eklemek [ServiceDefinition.csdef] dosya.</span><span class="sxs-lookup"><span data-stu-id="86c46-153">Add the following startup task to the [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="86c46-154">Bu komut eklemek **startup.cmd** dosyası:</span><span class="sxs-lookup"><span data-stu-id="86c46-154">Add this command to the **startup.cmd** file:</span></span>

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

<span data-ttu-id="86c46-155">Bu görev neden **startup.cmd** gerekli sağlanarak web rolü başlatılmadan her zaman çalıştırılmak üzere toplu iş dosyası **IPSecurity** bölümdür kilidi.</span><span class="sxs-lookup"><span data-stu-id="86c46-155">This task causes the **startup.cmd** batch file to be run every time the web role is initialized, ensuring that the required **ipSecurity** section is unlocked.</span></span>

<span data-ttu-id="86c46-156">Son olarak, değişiklik [system.webServer bölümü](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) web rolün **web.config** dosya erişim izni IP adresleri listesi aşağıdaki örnekte gösterildiği gibi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="86c46-156">Finally, modify the [system.webServer section](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) your web role’s **web.config** file to add a list of IP addresses that are granted access, as shown in the following example:</span></span>

<span data-ttu-id="86c46-157">Bu örnek yapılandırma **sağlayan** tanımlanan iki dışında sunucuya erişmek için tüm IP'ler</span><span class="sxs-lookup"><span data-stu-id="86c46-157">This sample config **allows** all IPs to access the server except the two defined</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are granted access-->
    <ipSecurity>
        <!--The following IP addresses are denied access-->
        <add allowed="false" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="false" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

<span data-ttu-id="86c46-158">Bu örnek yapılandırma **engellediği** sunucu tanımlanan iki dışında erişimini tüm IP'ler.</span><span class="sxs-lookup"><span data-stu-id="86c46-158">This sample config **denies** all IPs from accessing the server except for the two defined.</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are denied access-->
    <ipSecurity allowUnlisted="false">
        <!--The following IP addresses are granted access-->
        <add allowed="true" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="true" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

## <a name="create-a-powershell-startup-task"></a><span data-ttu-id="86c46-159">PowerShell başlangıç görev oluşturma</span><span class="sxs-lookup"><span data-stu-id="86c46-159">Create a PowerShell startup task</span></span>
<span data-ttu-id="86c46-160">Windows PowerShell komut dosyalarını, doğrudan çağrılamaz [ServiceDefinition.csdef] dosyası, ancak bunlar çağrılabilir gelen bir başlangıç toplu iş dosyası içinde.</span><span class="sxs-lookup"><span data-stu-id="86c46-160">Windows PowerShell scripts cannot be called directly from the [ServiceDefinition.csdef] file, but they can be invoked from within a startup batch file.</span></span>

<span data-ttu-id="86c46-161">PowerShell (varsayılan), imzalanmamış komut dosyalarının çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="86c46-161">PowerShell (by default) does not run unsigned scripts.</span></span> <span data-ttu-id="86c46-162">Kodunuzu oturum sürece, imzalanmamış komut dosyalarını çalıştırmak üzere yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="86c46-162">Unless you sign your script, you need to configure PowerShell to run unsigned scripts.</span></span> <span data-ttu-id="86c46-163">İmzasız betikleri çalıştırmak için **ExecutionPolicy** ayarlanmalıdır **Kısıtlanmamış**.</span><span class="sxs-lookup"><span data-stu-id="86c46-163">To run unsigned scripts, the **ExecutionPolicy** must be set to **Unrestricted**.</span></span> <span data-ttu-id="86c46-164">**ExecutionPolicy** ayarına kullanım üzerindeki Windows PowerShell sürümü temel alır.</span><span class="sxs-lookup"><span data-stu-id="86c46-164">The **ExecutionPolicy** setting that you use is based on the version of Windows PowerShell.</span></span>

```cmd
REM   Run an unsigned PowerShell script and log the output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

<span data-ttu-id="86c46-165">Çalıştırır PowerShell 2.0 olan bir konuk işletim veya sürüm 2 çalıştırmak için zorlayabilirsiniz 1.0 kullanıyorsanız ve kullanılamaz durumdaysa, sürüm 1 kullanın.</span><span class="sxs-lookup"><span data-stu-id="86c46-165">If you're using a Guest OS that is runs PowerShell 2.0 or 1.0 you can force version 2 to run, and if unavailable, use version 1.</span></span>

```cmd
REM   Attempt to set the execution policy by using PowerShell version 2.0 syntax.
PowerShell -Version 2.0 -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If PowerShell version 2.0 isn't available. Set the execution policy by using the PowerShell
IF %ERRORLEVEL% EQU -393216 (
   PowerShell -Command "Set-ExecutionPolicy Unrestricted" >> "%TEMP%\StartupLog.txt" 2>&1
   PowerShell .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1
)

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

## <a name="create-files-in-local-storage-from-a-startup-task"></a><span data-ttu-id="86c46-166">Yerel depolama biriminden bir başlangıç görevi dosyaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="86c46-166">Create files in local storage from a startup task</span></span>
<span data-ttu-id="86c46-167">Daha sonra uygulamanız tarafından erişilen, başlangıç görevi tarafından oluşturulan dosyaları depolamak için bir yerel depolama kaynağı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86c46-167">You can use a local storage resource to store files created by your startup task that is accessed later by your application.</span></span>

<span data-ttu-id="86c46-168">Yerel depolama kaynağı oluşturmak için Ekle bir [LocalResources] için bölüm [ServiceDefinition.csdef] dosya ve ardından ekleyin [LocalStorage] alt öğesi.</span><span class="sxs-lookup"><span data-stu-id="86c46-168">To create the local storage resource, add a [LocalResources] section to the [ServiceDefinition.csdef] file and then add the [LocalStorage] child element.</span></span> <span data-ttu-id="86c46-169">Yerel depolama kaynağı başlangıç görev için benzersiz bir ad ve uygun bir boyut verin.</span><span class="sxs-lookup"><span data-stu-id="86c46-169">Give the local storage resource a unique name and an appropriate size for your startup task.</span></span>

<span data-ttu-id="86c46-170">Yerel depolama kaynağı başlangıç görevinde kullanmak için yerel depolama kaynak konumu başvurmak için bir ortam değişkeni oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="86c46-170">To use a local storage resource in your startup task, you need to create an environment variable to reference the local storage resource location.</span></span> <span data-ttu-id="86c46-171">Ardından başlangıç görev ve uygulama dosyaları okuma ve yerel depolama kaynağı yazma imkanınız olur.</span><span class="sxs-lookup"><span data-stu-id="86c46-171">Then the startup task and the application are able to read and write files to the local storage resource.</span></span>

<span data-ttu-id="86c46-172">İlgili bölümleri **ServiceDefinition.csdef** dosya burada gösterilir:</span><span class="sxs-lookup"><span data-stu-id="86c46-172">The relevant sections of the **ServiceDefinition.csdef** file are shown here:</span></span>

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

<span data-ttu-id="86c46-173">Örnek olarak, bu **Startup.cmd** toplu iş dosyası kullanır **PathToStartupStorage** dosyası oluşturmak için ortam değişkeni **MyTest.txt** yerel depolama konumunda.</span><span class="sxs-lookup"><span data-stu-id="86c46-173">As an example, this **Startup.cmd** batch file uses the **PathToStartupStorage** environment variable to create the file **MyTest.txt** on the local storage location.</span></span>

```cmd
REM   Create a simple text file.

ECHO This text will go into the MyTest.txt file which will be in the    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed to by the PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO The contents of the PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit the batch file with ERRORLEVEL 0.

EXIT /b 0
```

<span data-ttu-id="86c46-174">Azure SDK kullanarak yerel depolama klasörüne erişebilecek [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="86c46-174">You can access local storage folder from the Azure SDK by using the [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-the-emulator-or-cloud"></a><span data-ttu-id="86c46-175">Öykünücü veya Bulut çalıştırın</span><span class="sxs-lookup"><span data-stu-id="86c46-175">Run in the emulator or cloud</span></span>
<span data-ttu-id="86c46-176">İşlem öykünücüsü olduğunda karşılaştırılan bulutta çalışırken farklı adımları gerçekleştirmeniz, başlangıç görevi olabilir.</span><span class="sxs-lookup"><span data-stu-id="86c46-176">You can have your startup task perform different steps when it is operating in the cloud compared to when it is in the compute emulator.</span></span> <span data-ttu-id="86c46-177">Örneğin, yalnızca öykünücüsünde çalışırken SQL verilerinizi yeni bir kopyasını kullanmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86c46-177">For example, you may want to use a fresh copy of your SQL data only when running in the emulator.</span></span> <span data-ttu-id="86c46-178">Veya öykünücüsünde çalıştırırken yapmanıza gerek yoktur bulut için bazı performans iyileştirmelerini yapmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86c46-178">Or you may want to do some performance optimizations for the cloud that you don't need to do when running in the emulator.</span></span>

<span data-ttu-id="86c46-179">İşlem öykünücüsü ve bulut üzerinde farklı eylemler gerçekleştirmek için bu özelliği bir ortam değişkeni oluşturarak gerçekleştirilebilir [ServiceDefinition.csdef] dosya.</span><span class="sxs-lookup"><span data-stu-id="86c46-179">This ability to perform different actions on the compute emulator and the cloud can be accomplished by creating an environment variable in the [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="86c46-180">Ardından, başlangıç görevi bu ortam değişkenine bir değer için sınayın.</span><span class="sxs-lookup"><span data-stu-id="86c46-180">You then test that environment variable for a value in your startup task.</span></span>

<span data-ttu-id="86c46-181">Ortam değişkeni oluşturmak için Ekle [değişkeni]/[RoleInstanceValue] öğesi ve bir XPath değeri oluşturun `/RoleEnvironment/Deployment/@emulated`.</span><span class="sxs-lookup"><span data-stu-id="86c46-181">To create the environment variable, add the [Variable]/[RoleInstanceValue] element and create an XPath value of `/RoleEnvironment/Deployment/@emulated`.</span></span> <span data-ttu-id="86c46-182">Değeri **ComputeEmulatorRunning %** ortam değişkenidir `true` işlem öykünücüsü üzerinde çalışırken ve `false` bulut üzerinde çalışırken.</span><span class="sxs-lookup"><span data-stu-id="86c46-182">The value of the **%ComputeEmulatorRunning%** environment variable is `true` when running on the compute emulator, and `false` when running on the cloud.</span></span>

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

<span data-ttu-id="86c46-183">Görev şimdi denetleyebilirsiniz **ComputeEmulatorRunning %** farklı eylemler gerçekleştirmek için ortam değişkeni tabanlı rol Bulut veya öykünücü çalıştıran.</span><span class="sxs-lookup"><span data-stu-id="86c46-183">The task can now check the **%ComputeEmulatorRunning%** environment variable to perform different actions based on whether the role is running in the cloud or the emulator.</span></span> <span data-ttu-id="86c46-184">Bu ortam değişkeninin denetler .cmd Kabuk betiği'dir.</span><span class="sxs-lookup"><span data-stu-id="86c46-184">Here is a .cmd shell script that checks for that environment variable.</span></span>

```cmd
REM   Check if this task is running on the compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on the compute emulator. Perform tasks that must be run only in the compute emulator.
) ELSE (
    REM   This task is running on the cloud. Perform tasks that must be run only in the cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a><span data-ttu-id="86c46-185">Görevinizi zaten çalıştırılıp çalıştırılmadığını Algıla</span><span class="sxs-lookup"><span data-stu-id="86c46-185">Detect that your task has already run</span></span>
<span data-ttu-id="86c46-186">Rolü yeniden çalıştırmak, başlangıç görevleri neden başlatmadan geri dönüşüm.</span><span class="sxs-lookup"><span data-stu-id="86c46-186">The role may recycle without a reboot causing your startup tasks to run again.</span></span> <span data-ttu-id="86c46-187">Bir görev, barındırma VM üzerinde zaten çalıştırılıp çalıştırılmadığını gösteren bayrak yoktur.</span><span class="sxs-lookup"><span data-stu-id="86c46-187">There is no flag to indicate that a task has already run on the hosting VM.</span></span> <span data-ttu-id="86c46-188">Birden çok kez çalıştırmak olduğu önemli değildir, bazı görevler de sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="86c46-188">You may have some tasks where it doesn't matter that they run multiple times.</span></span> <span data-ttu-id="86c46-189">Ancak, burada bir görevin birden çok kez çalışmasını engellemek için gereken bir durumla içine çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="86c46-189">However, you may run into a situation where you need to prevent a task from running more than once.</span></span>

<span data-ttu-id="86c46-190">Bir görev zaten çalıştırılıp çalıştırılmadığını belirlemek için basit bir dosyada oluşturmak için yoldur **% TEMP %** görev başarılı olduğunda klasörü ve başlangıç görevinin de bakın.</span><span class="sxs-lookup"><span data-stu-id="86c46-190">The simplest way to detect that a task has already run is to create a file in the **%TEMP%** folder when the task is successful and look for it at the start of the task.</span></span> <span data-ttu-id="86c46-191">Sizin için yapar bir örnek cmd Kabuk betiği'dir.</span><span class="sxs-lookup"><span data-stu-id="86c46-191">Here is a sample cmd shell script that does that for you.</span></span>

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
  REM   The application installed without error. Create a file to indicate that the task
  REM   does not need to be run again.

  ECHO This line will create a file to indicate that Application 1 installed correctly. > "%RoleRoot%\Task1_Success.txt"

) ELSE (
  REM   An error occurred. Log the error and exit with the error code.

  DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
  TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
  ECHO  An error occurred running task 1. Errorlevel = %ERRORLEVEL%. >> "%TEMP%\StartupLog.txt" 2>&1

  EXIT %ERRORLEVEL%
)

:Finish

REM   Exit normally.
EXIT /B 0
```

## <a name="task-best-practices"></a><span data-ttu-id="86c46-192">Görev en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="86c46-192">Task best practices</span></span>
<span data-ttu-id="86c46-193">Görev web veya çalışan rolü için yapılandırırken izlemeniz gereken bazı en iyi uygulamalar şunlardır.</span><span class="sxs-lookup"><span data-stu-id="86c46-193">Here are some best practices you should follow when configuring task for your web or worker role.</span></span>

### <a name="always-log-startup-activities"></a><span data-ttu-id="86c46-194">Her zaman günlük başlangıç etkinlikleri</span><span class="sxs-lookup"><span data-stu-id="86c46-194">Always log startup activities</span></span>
<span data-ttu-id="86c46-195">Visual Studio için toplu iş dosyaları işlemi mümkün olduğunca kadar veri almak üzere iyi olacak şekilde toplu iş dosyaları, adım için bir hata ayıklayıcısı sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="86c46-195">Visual Studio does not provide a debugger to step through batch files, so it's good to get as much data on the operation of batch files as possible.</span></span> <span data-ttu-id="86c46-196">Toplu iş dosyaları çıktısı günlüğü her ikisi de **stdout** ve **stderr**, hata ayıklama ve toplu iş dosyaları düzeltme çalışılırken önemli bilgileri verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86c46-196">Logging the output of batch files, both **stdout** and **stderr**, can give you important information when trying to debug and fix batch files.</span></span> <span data-ttu-id="86c46-197">Hem günlük için **stdout** ve **stderr** StartupLog.txt dizinindeki dosyasına işaret için tarafından **% TEMP %** ortam değişkeni, bir metin eklemek `>>  "%TEMP%\\StartupLog.txt" 2>&1` belirli satırları oturum istediğiniz sonuna.</span><span class="sxs-lookup"><span data-stu-id="86c46-197">To log both **stdout** and **stderr** to the StartupLog.txt file in the directory pointed to by the **%TEMP%** environment variable, add the text `>>  "%TEMP%\\StartupLog.txt" 2>&1` to the end of specific lines you want to log.</span></span> <span data-ttu-id="86c46-198">Örneğin, setup.exe yürütmek için **PathToApp1Install %** dizini:</span><span class="sxs-lookup"><span data-stu-id="86c46-198">For example, to execute setup.exe in the **%PathToApp1Install%** directory:</span></span>

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

<span data-ttu-id="86c46-199">Xml dosyanızı basitleştirmek için bir sarmalayıcı oluşturabilirsiniz *cmd* tüm, başlangıç çağrılar dosya görevlerin yanı sıra günlüğe kaydetme ve her alt görev aynı ortam değişkenlerini paylaşır sağlar.</span><span class="sxs-lookup"><span data-stu-id="86c46-199">To simplify your xml, you can create a wrapper *cmd* file that calls all of your startup tasks along with logging and ensures each child-task shares the same environment variables.</span></span>

<span data-ttu-id="86c46-200">Bu rahatsız edici kullanmak olsa bulabilirsiniz `>> "%TEMP%\StartupLog.txt" 2>&1` her başlangıç görevi ucunda.</span><span class="sxs-lookup"><span data-stu-id="86c46-200">You may find it annoying though to use `>> "%TEMP%\StartupLog.txt" 2>&1` on the end of each startup task.</span></span> <span data-ttu-id="86c46-201">Görev günlüğü, günlük kaydı işleyen bir sarmalayıcı oluşturarak uygulayabilir.</span><span class="sxs-lookup"><span data-stu-id="86c46-201">You can enforce task logging by creating a wrapper that handles logging for you.</span></span> <span data-ttu-id="86c46-202">Bu sarmalayıcı çalıştırmak istediğiniz gerçek toplu iş dosyasını çağırır.</span><span class="sxs-lookup"><span data-stu-id="86c46-202">This wrapper calls the real batch file you want to run.</span></span> <span data-ttu-id="86c46-203">Hedef toplu iş dosyasından herhangi bir çıktı yönlendirilecek *Startuplog.txt* dosya.</span><span class="sxs-lookup"><span data-stu-id="86c46-203">Any output from the target batch file will be redirected to the *Startuplog.txt* file.</span></span>

<span data-ttu-id="86c46-204">Aşağıdaki örnek, başlangıç toplu iş dosyasından tüm çıktı yeniden yönlendirme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="86c46-204">The following example shows how to redirect all output from a startup batch file.</span></span> <span data-ttu-id="86c46-205">Bu örnekte ServerDefinition.csdef dosyasını çağıran bir başlangıç görevi oluşturur *logwrap.cmd*.</span><span class="sxs-lookup"><span data-stu-id="86c46-205">In this example, the ServerDefinition.csdef file creates a startup task that calls *logwrap.cmd*.</span></span> <span data-ttu-id="86c46-206">*logwrap.cmd* çağrıları *Startup2.cmd*, tüm çıktı yeniden yönlendirme **% TEMP %\\StartupLog.txt**.</span><span class="sxs-lookup"><span data-stu-id="86c46-206">*logwrap.cmd* calls *Startup2.cmd*, redirecting all output to **%TEMP%\\StartupLog.txt**.</span></span>

<span data-ttu-id="86c46-207">ServiceDefinition.cmd:</span><span class="sxs-lookup"><span data-stu-id="86c46-207">ServiceDefinition.cmd:</span></span>

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

<span data-ttu-id="86c46-208">**logwrap.cmd:**</span><span class="sxs-lookup"><span data-stu-id="86c46-208">**logwrap.cmd:**</span></span>

```cmd
@ECHO OFF

REM   logwrap.cmd calls passed in batch file, redirecting all output to the StartupLog.txt log file.

ECHO [%date% %time%] == START logwrap.cmd ============================================== >> "%TEMP%\StartupLog.txt" 2>&1
ECHO [%date% %time%] Running %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Call the child command batch file, redirecting all output to the StartupLog.txt log file.
START /B /WAIT %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Log the completion of child command.
ECHO [%date% %time%] Done >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (

   REM   No errors occurred. Exit logwrap.cmd normally.
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B 0

) ELSE (

   REM   Log the error.
   ECHO [%date% %time%] An error occurred. The ERRORLEVEL = %ERRORLEVEL%.  >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B %ERRORLEVEL%

)
```

<span data-ttu-id="86c46-209">**Startup2.cmd:**</span><span class="sxs-lookup"><span data-stu-id="86c46-209">**Startup2.cmd:**</span></span>

```cmd
@ECHO OFF

REM   This is the batch file where the startup steps should be performed. Because of the
REM   way Startup2.cmd was called, all commands and their outputs will be stored in the
REM   StartupLog.txt file in the directory pointed to by the TEMP environment variable.

REM   If an error occurs, the following command will pass the ERRORLEVEL back to the
REM   calling batch file.

ECHO [%date% %time%] Some log information about this task
ECHO [%date% %time%] Some more log information about this task

EXIT %ERRORLEVEL%
```

<span data-ttu-id="86c46-210">Örnek çıkış **StartupLog.txt** dosyası:</span><span class="sxs-lookup"><span data-stu-id="86c46-210">Sample output in the **StartupLog.txt** file:</span></span>

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> <span data-ttu-id="86c46-211">**StartupLog.txt** dosyasının bulunduğu *C:\Resources\temp\\{rol tanımlayıcısı} \RoleTemp* klasör.</span><span class="sxs-lookup"><span data-stu-id="86c46-211">The **StartupLog.txt** file is located in the *C:\Resources\temp\\{role identifier}\RoleTemp* folder.</span></span>
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a><span data-ttu-id="86c46-212">Başlangıç görevi için uygun şekilde executionContext ayarlayın</span><span class="sxs-lookup"><span data-stu-id="86c46-212">Set executionContext appropriately for startup tasks</span></span>
<span data-ttu-id="86c46-213">Başlangıç görevi için uygun şekilde ayrıcalıkları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="86c46-213">Set privileges appropriately for the startup task.</span></span> <span data-ttu-id="86c46-214">Bazen normal ayrıcalıklara sahip rolünü çalıştıran olsa bile başlangıç görevleri yükseltilmiş ayrıcalıklarla çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="86c46-214">Sometimes startup tasks must run with elevated privileges even though the role runs with normal privileges.</span></span>

<span data-ttu-id="86c46-215">[ExecutionContext][görev] öznitelik başlangıç görevi öncelik düzeyi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="86c46-215">The [executionContext][Task] attribute sets the privilege level of the startup task.</span></span> <span data-ttu-id="86c46-216">Kullanarak `executionContext="limited"` başlangıç görevi rolle aynı ayrıcalık düzeyi olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="86c46-216">Using `executionContext="limited"` means the startup task has the same privilege level as the role.</span></span> <span data-ttu-id="86c46-217">Kullanarak `executionContext="elevated"` başlangıç görevi rolünüz için yönetici ayrıcalıkları vermeden yönetici görevlerini gerçekleştirmek başlangıç görevi sağlayan yönetici ayrıcalıklarına sahip anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="86c46-217">Using `executionContext="elevated"` means the startup task has administrator privileges, which allows the startup task to perform administrator tasks without giving administrator privileges to your role.</span></span>

<span data-ttu-id="86c46-218">Yükseltilmiş ayrıcalıklar gerektiren bir başlangıç görevi kullanan bir başlangıç görevi örneğidir **AppCmd.exe** IIS'yi yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="86c46-218">An example of a startup task that requires elevated privileges is a startup task that uses **AppCmd.exe** to configure IIS.</span></span> <span data-ttu-id="86c46-219">**AppCmd.exe** gerektirir `executionContext="elevated"`.</span><span class="sxs-lookup"><span data-stu-id="86c46-219">**AppCmd.exe** requires `executionContext="elevated"`.</span></span>

### <a name="use-the-appropriate-tasktype"></a><span data-ttu-id="86c46-220">Uygun taskType kullanın</span><span class="sxs-lookup"><span data-stu-id="86c46-220">Use the appropriate taskType</span></span>
<span data-ttu-id="86c46-221">[TaskType][görev] özniteliği belirler başlangıç görevi şekilde gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="86c46-221">The [taskType][Task] attribute determines the way the startup task is executed.</span></span> <span data-ttu-id="86c46-222">Üç değer vardır: **basit**, **arka plan**, ve **ön plan**.</span><span class="sxs-lookup"><span data-stu-id="86c46-222">There are three values: **simple**, **background**, and **foreground**.</span></span> <span data-ttu-id="86c46-223">Arka plan ve ön plan görevleri zaman uyumsuz olarak başlatılır ve ardından basit görevler eşzamanlı olarak yürütülen bir kerede.</span><span class="sxs-lookup"><span data-stu-id="86c46-223">The background and foreground tasks are started asynchronously, and then the simple tasks are executed synchronously one at a time.</span></span>

<span data-ttu-id="86c46-224">İle **basit** başlangıç görevleri, görevlerin çalıştığı sırada görevleri ServiceDefinition.csdef dosyasında listelenen sıraya göre ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86c46-224">With **simple** startup tasks, you can set the order in which the tasks run by the order in which the tasks are listed in the ServiceDefinition.csdef file.</span></span> <span data-ttu-id="86c46-225">Varsa bir **basit** görev sıfır olmayan çıkış kodu ile sona erer ve ardından başlangıç yordamı durur ve rol başlatılmaz.</span><span class="sxs-lookup"><span data-stu-id="86c46-225">If a **simple** task ends with a non-zero exit code, then the startup procedure stops and the role does not start.</span></span>

<span data-ttu-id="86c46-226">Arasındaki farkı **arka plan** başlangıç görevleri ve **ön plan** başlangıç görevleri olan **ön plan** görevleri tutmak kadar çalışan rolü **ön plan** görev sona erer.</span><span class="sxs-lookup"><span data-stu-id="86c46-226">The difference between **background** startup tasks and **foreground** startup tasks is that **foreground** tasks keep the role running until the **foreground** task ends.</span></span> <span data-ttu-id="86c46-227">Bu aynı zamanda olması durumunda gelir **ön plan** görevin askıda kalmasına ya da çökme (Crash), rol değil geri dönüşüm kadar **ön plan** görev zorunlu kapalı.</span><span class="sxs-lookup"><span data-stu-id="86c46-227">This also means that if the **foreground** task hangs or crashes, the role will not recycle until the **foreground** task is forced closed.</span></span> <span data-ttu-id="86c46-228">Bu nedenle, **arka plan** görevleri bu özelliği gerekmedikçe zaman uyumsuz başlangıç görevleri için önerilen **ön plan** görev.</span><span class="sxs-lookup"><span data-stu-id="86c46-228">For this reason, **background** tasks are recommended for asynchronous startup tasks unless you need that feature of the **foreground** task.</span></span>

### <a name="end-batch-files-with-exit-b-0"></a><span data-ttu-id="86c46-229">Çık /B 0 ile son toplu iş dosyaları</span><span class="sxs-lookup"><span data-stu-id="86c46-229">End batch files with EXIT /B 0</span></span>
<span data-ttu-id="86c46-230">Rol, yalnızca başlatacak **errorlevel** her basit başlangıç sıfır görevdir.</span><span class="sxs-lookup"><span data-stu-id="86c46-230">The role will only start if the **errorlevel** from each of your simple startup task is zero.</span></span> <span data-ttu-id="86c46-231">Tüm programları Ayarla **errorlevel** (çıkış kodu), doğru şekilde toplu dosya bitmelidir bir `EXIT /B 0` her şeyin doğru şekilde çalıştırdıysanız.</span><span class="sxs-lookup"><span data-stu-id="86c46-231">Not all programs set the **errorlevel** (exit code) correctly, so the batch file should end with an `EXIT /B 0` if everything ran correctly.</span></span>

<span data-ttu-id="86c46-232">Eksik `EXIT /B 0` başlatılmaz rolleri ortak bir nedeni bir başlangıç toplu işlemin sonunda dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="86c46-232">A missing `EXIT /B 0` at the end of a startup batch file is a common cause of roles that do not start.</span></span>

> [!NOTE]
> <span data-ttu-id="86c46-233">İç içe geçmiş toplu fark ettim dosyalar bazen askıda kullanırken `/B` parametresi.</span><span class="sxs-lookup"><span data-stu-id="86c46-233">I've noticed that nested batch files sometimes hang when using the `/B` parameter.</span></span> <span data-ttu-id="86c46-234">Başka bir toplu iş dosyası, geçerli toplu iş dosyasını çağırıyorsa ister kullanırsanız, bu yanıt vermemesine sorun gerçekleşmez emin olmak isteyebilirsiniz [günlük sarmalayıcı](#always-log-startup-activities).</span><span class="sxs-lookup"><span data-stu-id="86c46-234">You may want to make sure that this hang problem does not happen if another batch file calls your current batch file, like if you use the [log wrapper](#always-log-startup-activities).</span></span> <span data-ttu-id="86c46-235">Atlayabilirsiniz `/B` parametresi bu durumda.</span><span class="sxs-lookup"><span data-stu-id="86c46-235">You can omit the `/B` parameter in this case.</span></span>
> 
> 

### <a name="expect-startup-tasks-to-run-more-than-once"></a><span data-ttu-id="86c46-236">Birden çok kez çalıştırmak için başlangıç görevleri beklediğiniz</span><span class="sxs-lookup"><span data-stu-id="86c46-236">Expect startup tasks to run more than once</span></span>
<span data-ttu-id="86c46-237">Yeniden başlatma tüm rol dönüştürür içerir, ancak çalışan tüm başlangıç görevleri tüm rol dönüştürür içerir.</span><span class="sxs-lookup"><span data-stu-id="86c46-237">Not all role recycles include a reboot, but all role recycles include running all startup tasks.</span></span> <span data-ttu-id="86c46-238">Bu, başlangıç görevleri herhangi bir sorun olmadan yeniden başlatmalar arasında birden çok kez çalıştırmanız mümkün olması gerektiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="86c46-238">This means that startup tasks must be able to run multiple times between reboots without any problems.</span></span> <span data-ttu-id="86c46-239">Bu konu ele alınmıştır [bölüm önceki](#detect-that-your-task-has-already-run).</span><span class="sxs-lookup"><span data-stu-id="86c46-239">This is discussed in the [preceding section](#detect-that-your-task-has-already-run).</span></span>

### <a name="use-local-storage-to-store-files-that-must-be-accessed-in-the-role"></a><span data-ttu-id="86c46-240">Roldeki erişilmelidir dosyalarını depolamak için yerel depolama kullanın</span><span class="sxs-lookup"><span data-stu-id="86c46-240">Use local storage to store files that must be accessed in the role</span></span>
<span data-ttu-id="86c46-241">Kopyalama veya rolünüz için erişilebilir olduğundan, başlangıç görev sırasında bir dosya oluşturmak istiyorsanız, bu dosya yerel depolama alanına yerleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="86c46-241">If you want to copy or create a file during your startup task that is then accessible to your role, then that file must be placed in local storage.</span></span> <span data-ttu-id="86c46-242">Bkz: [bölüm önceki](#create-files-in-local-storage-from-a-startup-task).</span><span class="sxs-lookup"><span data-stu-id="86c46-242">See the [preceding section](#create-files-in-local-storage-from-a-startup-task).</span></span>

## <a name="next-steps"></a><span data-ttu-id="86c46-243">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="86c46-243">Next steps</span></span>
<span data-ttu-id="86c46-244">Bulut gözden [hizmet modeli ve paket](cloud-services-model-and-package.md)</span><span class="sxs-lookup"><span data-stu-id="86c46-244">Review the cloud [service model and package](cloud-services-model-and-package.md)</span></span>

<span data-ttu-id="86c46-245">Hakkında daha fazla bilgi [görevleri](cloud-services-startup-tasks.md) çalışır.</span><span class="sxs-lookup"><span data-stu-id="86c46-245">Learn more about how [Tasks](cloud-services-startup-tasks.md) work.</span></span>

<span data-ttu-id="86c46-246">[Oluşturma ve dağıtma](cloud-services-how-to-create-deploy-portal.md) , bulut hizmet paketi.</span><span class="sxs-lookup"><span data-stu-id="86c46-246">[Create and deploy](cloud-services-how-to-create-deploy-portal.md) your cloud service package.</span></span>

<span data-ttu-id="86c46-247">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span><span class="sxs-lookup"><span data-stu-id="86c46-247">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span></span>
<span data-ttu-id="86c46-248">[görev]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span><span class="sxs-lookup"><span data-stu-id="86c46-248">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span></span>
[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
<span data-ttu-id="86c46-249">[ortam]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span><span class="sxs-lookup"><span data-stu-id="86c46-249">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span></span>
<span data-ttu-id="86c46-250">[değişkeni]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span><span class="sxs-lookup"><span data-stu-id="86c46-250">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span></span>
<span data-ttu-id="86c46-251">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span><span class="sxs-lookup"><span data-stu-id="86c46-251">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span></span>
[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
<span data-ttu-id="86c46-252">[Uç noktaları]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints</span><span class="sxs-lookup"><span data-stu-id="86c46-252">[Endpoints]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints</span></span>
<span data-ttu-id="86c46-253">[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage</span><span class="sxs-lookup"><span data-stu-id="86c46-253">[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage</span></span>
<span data-ttu-id="86c46-254">[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources</span><span class="sxs-lookup"><span data-stu-id="86c46-254">[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources</span></span>
<span data-ttu-id="86c46-255">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span><span class="sxs-lookup"><span data-stu-id="86c46-255">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span></span>
