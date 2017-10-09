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
# <a name="common-cloud-service-startup-tasks"></a>Genel bulut hizmeti başlangıç görevleri
Bu makalede bazı örnekler ortak başlangıç görevleri, bulut hizmetinizin tooperform isteyebilirsiniz. Bir rolü başlamadan önce başlangıç görevleri tooperform işlemleri kullanabilirsiniz. Bir bileşeni yüklemek, COM bileşenlerini kaydetme, kayıt defteri anahtarlarını ayarlamak veya uzun süre çalışan bir işlem başlatılıyor tooperform isteyebilirsiniz işlemleri içerir. 

Bkz: [bu makalede](cloud-services-startup-tasks.md) toounderstand nasıl iş başlangıç görevleri ve özellikle nasıl toocreate hello bir başlangıç görevi tanımlayan girişinin.

> [!NOTE]
> Başlangıç değil yalnızca tooCloud Service Web ve çalışan rolleri geçerli tooVirtual makineleri görevlerdir.
> 

## <a name="define-environment-variables-before-a-role-starts"></a>Bir rolü başlatılmadan önce ortamı değişkenleri tanımlayın
Belirli bir görev için tanımlanan ortam değişkenlerini gerekirse hello kullanın [ortam] öğesi hello içinde [görev] öğesi.

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

Değişkenleri de kullanabilir bir [geçerli Azure XPath değeri](cloud-services-role-config-xpath.md) hello dağıtım hakkında bir şeyler tooreference. Hello yerine `value` özniteliği, tanımlayan bir [RoleInstanceValue] alt öğesi.

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a>IIS Başlangıç AppCmd.exe ile yapılandırma
Merhaba [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) komut satırı aracı, Azure üzerinde başlangıçta kullanılan toomanage IIS ayarları olabilir. *AppCmd.exe* Azure üzerinde uygun ve komut satırı erişim tooconfiguration ayarları kullanmak üzere başlangıç görevleri sağlar. Kullanarak *AppCmd.exe*, Web sitesi ayarlarını eklenemez, değiştiren veya uygulamaları ve sitelerin kaldırılamaz.

Ancak, vardır için birkaç şey toowatch çıkışı, hello kullanımda *AppCmd.exe* bir başlangıç görevi olarak:

* Başlangıç görevi birden çok kez yeniden başlatmalar arasında çalıştırabilirsiniz. Örneğin, ne zaman bir rol geri dönüştürür.
* Varsa bir *AppCmd.exe* eylem birden çok kez gerçekleştirilir, hataya neden. Örneğin, tooadd bir bölümü çok çalışıyor*Web.config* iki kez hataya neden.
* Başlangıç görevleri, sıfır olmayan çıkış kodu döndürmesi durumunda başarısız veya **errorlevel**. Örneğin, *AppCmd.exe* bir hata oluşturur.

İyi bir uygulama toocheck hello olan **errorlevel** çağırdıktan sonra *AppCmd.exe*, hangi ise kolay toodo hello çağrısı çok kaydırma*AppCmd.exe* ile bir *.cmd*  dosya. Bilinen bir algılama **errorlevel** yanıtı yok sayın veya için geri geçirin.

tarafından döndürülen errorlevel hello *AppCmd.exe* hello Winerror.h'de dosyasında listelenir ve ayrıca görülebilir [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).

### <a name="example-of-managing-hello-error-level"></a>Örnek hello hata düzeyi yönetme
Bu örnek bir sıkıştırma bölümü ve JSON toohello için sıkıştırma girişi ekler *Web.config* dosyasıyla hata işleme ve günlüğe kaydetme.

Merhaba hello ilgili bölümleri [ServiceDefinition.csdef] dosya burada gösterilen, hello ayarlama içeren [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) çok öznitelik`elevated` toogive *AppCmd.exe*  yeterli izinleri toochange hello ayarlarında hello *Web.config* dosyası:

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

Merhaba *Startup.cmd* toplu iş dosyası kullanır *AppCmd.exe* tooadd sıkıştırma bölüm ve sıkıştırma giriş JSON toohello için *Web.config* dosya. Beklenen hello **errorlevel** 183 hello doğrula kullanarak toozero ayarlanır. EXE komut satırı programı. Beklenmeyen errorlevels oturum tooStartupErrorLog.txt ' dir.

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

## <a name="add-firewall-rules"></a>Güvenlik duvarı kuralları ekleme
Azure üzerinde etkili bir şekilde iki güvenlik duvarı vardır. Merhaba ilk güvenlik duvarı hello sanal makine ve hello world dışında arasındaki bağlantıları denetler. Bu güvenlik duvarı tarafından hello denetlenir [uç noktaları] hello öğesinde [ServiceDefinition.csdef] dosya.

Merhaba ikinci güvenlik duvarı hello sanal makine ve sanal makinenin içinde hello işlemleri arasındaki bağlantıları denetler. Bu güvenlik duvarı tarafından hello denetlenebilir `netsh advfirewall firewall` komut satırı aracı.

Azure güvenlik duvarı kuralları rollerinizi içinde başlatılan hello işlemler için oluşturur. Bir hizmet veya programın başlattığınızda, örneğin, Azure otomatik olarak hello gerekli güvenlik duvarı kuralları tooallow bu hizmet toocommunicate hello Internet ile oluşturur. Ancak, rolünüze (örneğin, bir COM + hizmet ya da Windows zamanlanmış bir görev) dışında bir işlem tarafından başlatılan bir hizmet oluşturursanız, toomanually gerekir bir güvenlik duvarı kuralı tooallow erişim toothat hizmeti oluşturun. Bu güvenlik duvarı kuralları, bir başlangıç görevi kullanılarak oluşturulabilir.

Bir güvenlik duvarı kuralı oluşturan bir başlangıç görevi olmalıdır bir [executionContext][görev] , **yükseltilmiş**. Aşağıdaki başlangıç görevi toohello hello eklemek [ServiceDefinition.csdef] dosya.

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

tooadd hello güvenlik duvarı kuralı, hello uygun kullanmalıdır `netsh advfirewall firewall` başlangıç toplu iş dosyası komutları. Bu örnekte, hello başlangıç görevi güvenlik ve şifreleme'yi TCP bağlantı noktası 80 gerektirir.

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a>Belirli bir IP adres bloğu
IIS değiştirerek bir Azure web rolü erişim tooa belirtilen IP adresleri kümesini kısıtlayabilirsiniz **web.config** dosya. Toouse hello kilidini açan bir komut dosyası etmeniz **IPSecurity** hello bölümünü **ApplicationHost.config** dosya.

toodo kilidini hello **IPSecurity** hello bölümünü **ApplicationHost.config** dosya, rol başlangıcında çalışan bir komut dosyası oluşturun. Merhaba kök düzeyinde web rolünüz adlı bir klasör oluşturun **başlangıç** ve bu klasör içinde adlı bir toplu iş dosyası oluşturmak **startup.cmd**. Bu dosya tooyour Visual Studio projesi eklemek hello özelliklerini ve çok**her zaman Kopyala** tooensure paketinize eklenmiştir.

Aşağıdaki başlangıç görevi toohello hello eklemek [ServiceDefinition.csdef] dosya.

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

Bu komut toohello ekleme **startup.cmd** dosyası:

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

Bu görev hello neden **startup.cmd** hello web rolü başlatılan her çalıştığında, çalışması dosya toobe gerekli o hello sağlama toplu **IPSecurity** bölümdür kilidi.

Son olarak, hello değiştirme [system.webServer bölümü](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) web rolün **web.config** tooadd erişim izni IP adresleri listesi hello aşağıdaki örnekte gösterildiği gibi dosya:

Bu örnek yapılandırma **sağlayan** tüm IP'ler tooaccess iki tanımlanmış hello dışında sunucu hello

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

Bu örnek yapılandırma **engellediği** hello sunucu hello tanımlanan iki dışında erişimini tüm IP'ler.

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

## <a name="create-a-powershell-startup-task"></a>PowerShell başlangıç görev oluşturma
Windows PowerShell komut dosyalarını doğrudan hello çağrılamaz [ServiceDefinition.csdef] dosyası, ancak bunlar çağrılabilir gelen bir başlangıç toplu iş dosyası içinde.

PowerShell (varsayılan), imzalanmamış komut dosyalarının çalışmaz. Kodunuzu oturum sürece tooconfigure PowerShell gereksinim toorun imzalanmamış komut dosyaları. toorun imzalanmamış komut dosyaları hello **ExecutionPolicy** çok ayarlanmalıdır**Kısıtlanmamış**. Merhaba **ExecutionPolicy** ayarına kullanım Windows PowerShell hello sürümü temel alır.

```cmd
REM   Run an unsigned PowerShell script and log hello output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

1.0, sürüm 2 toorun zorlayabilirsiniz veya bir konuk çalıştırır PowerShell 2.0 olan işletim sistemi kullanıyorsanız ve bu mümkün değilse, sürüm 1 kullanın.

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

## <a name="create-files-in-local-storage-from-a-startup-task"></a>Yerel depolama biriminden bir başlangıç görevi dosyaları oluşturma
Yerel depolama kaynağı toostore kullanabilirsiniz, daha sonra uygulamanız tarafından erişilebilen, başlangıç görevi tarafından oluşturulan dosyalar.

toocreate Merhaba yerel depolama kaynağı, ekleme bir [LocalResources] bölüm toohello [ServiceDefinition.csdef] dosya ve hello ekleyin [LocalStorage] alt öğesi. Merhaba yerel depolama kaynağı başlangıç görev için benzersiz bir ad ve uygun bir boyut verin.

Başlangıç görevi, yerel depolama kaynağı toouse, toocreate bir ortam değişkeni tooreference hello yerel depolama kaynak konumu gerekir. Başlangıç görevi hello ve Merhaba uygulaması mümkün tooread ve dosyaları toohello yerel depolama kaynağı yazma.

Merhaba hello ilgili bölümleri **ServiceDefinition.csdef** dosya burada gösterilir:

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

Örnek olarak, bu **Startup.cmd** toplu iş dosyası kullanan hello **PathToStartupStorage** ortam değişkeni toocreate hello dosya **MyTest.txt** hello yerel depolama konum.

```cmd
REM   Create a simple text file.

ECHO This text will go into hello MyTest.txt file which will be in hello    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed tooby hello PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO hello contents of hello PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit hello batch file with ERRORLEVEL 0.

EXIT /b 0
```

Hello kullanarak yerel depolama klasörü hello Azure SDK ' erişebilirsiniz [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) yöntemi.

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-hello-emulator-or-cloud"></a>Merhaba öykünücü veya Bulut çalıştırın
Merhaba işlem öykünücüsü olduğu hello karşılaştırıldığında bulut toowhen içinde çalışırken farklı adımları gerçekleştirmeniz, başlangıç görevi olabilir. Örneğin, yalnızca hello öykünücüsünde çalışırken toouse SQL verilerinizi yeni bir kopyasını isteyebilirsiniz. Veya hello öykünücüsünde çalıştırırken toodo gerekmeyen hello bulut için bazı performans iyileştirmelerini toodo isteyebilirsiniz.

Bu özelliği tooperform hello eylemleri işlem öykünücüsü ve hello bulut hello bir ortam değişkeni oluşturarak gerçekleştirilebilir farklı [ServiceDefinition.csdef] dosya. Ardından, başlangıç görevi bu ortam değişkenine bir değer için sınayın.

toocreate hello ortam değişkeni hello eklemek [değişkeni]/[RoleInstanceValue] öğesi ve bir XPath değeri oluşturun `/RoleEnvironment/Deployment/@emulated`. Merhaba hello değerini **ComputeEmulatorRunning %** ortam değişkenidir `true` hello işlem öykünücüsü üzerinde çalışırken ve `false` hello bulut üzerinde çalışırken.

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

Başlangıç görevi şimdi hello denetimi **ComputeEmulatorRunning %** olup hello hello rolünü çalıştıran bağlı ortam değişkeni tooperform farklı eylemleri Bulut veya öykünücü hello. Bu ortam değişkeninin denetler .cmd Kabuk betiği'dir.

```cmd
REM   Check if this task is running on hello compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on hello compute emulator. Perform tasks that must be run only in hello compute emulator.
) ELSE (
    REM   This task is running on hello cloud. Perform tasks that must be run only in hello cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a>Görevinizi zaten çalıştırılıp çalıştırılmadığını Algıla
Merhaba rol başlangıç görevleri toorun tekrar yapmasına neden yeniden başlatma geri dönüşüm. Bir görev VM barındırma hello üzerinde önceden çalıştırıldıktan hiçbir bayrağı tooindicate yoktur. Birden çok kez çalıştırmak olduğu önemli değildir, bazı görevler de sahip olabilir. Ancak, birden çok kez çalışan bir görev tooprevent ihtiyaç duyacağınız bir durumla çalıştırabilirsiniz.

bir görev zaten çalışan hello en basit yolu toodetect olan toocreate hello dosyasında **% TEMP %** hello görev başarılı olduğunda klasörü ve hello de göz hello görevini Başlat. Sizin için yapar bir örnek cmd Kabuk betiği'dir.

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

## <a name="task-best-practices"></a>Görev en iyi uygulamalar
Görev web veya çalışan rolü için yapılandırırken izlemeniz gereken bazı en iyi uygulamalar şunlardır.

### <a name="always-log-startup-activities"></a>Her zaman günlük başlangıç etkinlikleri
İyi tooget olacak şekilde visual Studio hata ayıklayıcısı toostep toplu iş dosyaları kadar veri toplu iş dosyaları hello işlemi mümkün olduğunca üzerinde sağlamaz. Toplu iş dosyaları Hello çıktısı günlüğü her ikisi de **stdout** ve **stderr**, toodebug çalışırken önemli bilgileri verin ve toplu iş dosyaları düzeltin. toolog hem **stdout** ve **stderr** toohello StartupLog.txt hello dizine işaret tooby hello dosyasında **% TEMP %** ortam değişkeni hello metin ekleme`>>  "%TEMP%\\StartupLog.txt" 2>&1`özel toohello sonuna satırları toolog istiyor. Örneğin, hello tooexecute setup.exe **PathToApp1Install %** dizini:

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

toosimplify, xml, bir sarmalayıcı oluşturur *cmd* tüm, başlangıç çağrılar dosya görevlerin yanı sıra günlüğe kaydetme ve her alt görev paylaşımları hello aynı ortam değişkenleri sağlar.

Ancak toouse sinir bozucu bulabilirsiniz `>> "%TEMP%\StartupLog.txt" 2>&1` her başlangıç görevi hello ucunda. Görev günlüğü, günlük kaydı işleyen bir sarmalayıcı oluşturarak uygulayabilir. Bu sarmalayıcı toorun istediğiniz hello gerçek toplu iş dosyasını çağırır. Herhangi bir çıktı hello hedef toplu iş dosyasından yeniden yönlendirilen toohello olacaktır *Startuplog.txt* dosya.

Aşağıdaki örneğine hello tooredirect tüm bir başlangıç toplu iş dosyasından nasıl çıktısını gösterir. Bu örnekte, çağıran bir başlangıç görevi hello ServerDefinition.csdef dosyası oluşturur *logwrap.cmd*. *logwrap.cmd* çağrıları *Startup2.cmd*, tüm çıktı çok yönlendirme**% TEMP %\\StartupLog.txt**.

ServiceDefinition.cmd:

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

**logwrap.cmd:**

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

**Startup2.cmd:**

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

Örnek hello çıktısında **StartupLog.txt** dosyası:

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> Merhaba **StartupLog.txt** dosya hello bulunur *C:\Resources\temp\\{rol tanımlayıcısı} \RoleTemp* klasör.
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a>Başlangıç görevi için uygun şekilde executionContext ayarlayın
Ayrıcalıkları hello başlangıç görevi için uygun şekilde ayarlayın. Bazen normal ayrıcalıklara sahip Hello rolünü çalıştıran olsa bile başlangıç görevleri yükseltilmiş ayrıcalıklarla çalıştırmanız gerekir.

Merhaba [executionContext][görev] öznitelik hello başlangıç görevi hello öncelik düzeyi ayarlar. Kullanarak `executionContext="limited"` hello hello rolü olarak aynı ayrıcalık düzeyi hello başlangıç görevinin anlamına gelir. Kullanarak `executionContext="elevated"` hello başlangıç görevi, yönetici ayrıcalıkları tooyour rol vermeden görev tooperform yönetici görevleri sağlayan hello başlangıç yönetici ayrıcalıklarına sahip anlamına gelir.

Yükseltilmiş ayrıcalıklar gerektiren bir başlangıç görevi kullanan bir başlangıç görevi örneğidir **AppCmd.exe** tooconfigure IIS. **AppCmd.exe** gerektirir `executionContext="elevated"`.

### <a name="use-hello-appropriate-tasktype"></a>Merhaba uygun taskType kullanın
Merhaba [taskType][görev] özniteliği belirler hello şekilde hello başlangıç görevi gerçekleştirilir. Üç değer vardır: **basit**, **arka plan**, ve **ön plan**. Merhaba arka plan ve ön plan görevleri zaman uyumsuz olarak başlatılır ve ardından hello Basit görevler eşzamanlı olarak yürütülen bir kerede.

İle **basit** başlangıç görevleri, başlangıç görevleri çalıştırdığınız hello siparişe hangi hello görevleri hello ServiceDefinition.csdef dosyasında listelenen hello göre ayarlayabilirsiniz. Varsa bir **basit** görev biter sıfır olmayan çıkış kodu, ardından hello başlangıç yordamı durdurur ve hello rol başlatılmaz.

Merhaba arasındaki farkı **arka plan** başlangıç görevleri ve **ön plan** başlangıç görevleri olan **ön plan** görevleri tutmak hello rol çalışan hello kadar  **ön plan** görev sona erer. Bu ayrıca, hello anlamına gelir **ön plan** görevin askıda kalmasına ya da çökme (Crash), hello rol değil geri dönüşüm hello kadar **ön plan** görev zorunlu kapalı. Bu nedenle, **arka plan** görevleri hello bu özelliği gerekmedikçe zaman uyumsuz başlangıç görevleri için önerilen **ön plan** görev.

### <a name="end-batch-files-with-exit-b-0"></a>Çık /B 0 ile son toplu iş dosyaları
Merhaba rolü yalnızca Merhaba, başlatacak **errorlevel** her basit başlangıç sıfır görevdir. Tüm programları hello Ayarla **errorlevel** (çıkış kodu), doğru şekilde hello toplu iş dosyası bitmelidir bir `EXIT /B 0` her şeyin doğru şekilde çalıştırdıysanız.

Eksik `EXIT /B 0` hello başlangıç toplu dosyasının sonuna bir ortak başlatılmaz rolleri nedenidir.

> [!NOTE]
> İç içe geçmiş toplu fark ettim dosyalar bazen askıda hello kullanırken `/B` parametresi. Başka bir toplu iş dosyası, geçerli toplu iş dosyasını çağırıyorsa ister hello kullanırsanız, bu yanıt vermemesine sorun gerçekleşmez emin toomake isteyebilir [günlük sarmalayıcı](#always-log-startup-activities). Merhaba atlayabilirsiniz `/B` parametresi bu durumda.
> 
> 

### <a name="expect-startup-tasks-toorun-more-than-once"></a>Başlangıç görevleri toorun birden çok kez beklediğiniz
Yeniden başlatma tüm rol dönüştürür içerir, ancak çalışan tüm başlangıç görevleri tüm rol dönüştürür içerir. Bu, başlangıç görevleri birden çok kez herhangi bir sorun olmadan yeniden başlatmalar arasında mümkün toorun olması gerektiği anlamına gelir. Bu hello ele alınmıştır [bölüm önceki](#detect-that-your-task-has-already-run).

### <a name="use-local-storage-toostore-files-that-must-be-accessed-in-hello-role"></a>Merhaba rolünde erişilmelidir yerel depolama toostore dosyaları kullanma
Toocopy istediğiniz ya da başlangıç görev sırasında bir dosya oluşturun, sonra erişilebilir tooyour rolüdür sonra bu dosyayı yerel depolama alanına yerleştirilmelidir. Merhaba bkz [bölüm önceki](#create-files-in-local-storage-from-a-startup-task).

## <a name="next-steps"></a>Sonraki adımlar
Gözden hello bulut [hizmet modeli ve paket](cloud-services-model-and-package.md)

Hakkında daha fazla bilgi [görevleri](cloud-services-startup-tasks.md) çalışır.

[Oluşturma ve dağıtma](cloud-services-how-to-create-deploy-portal.md) , bulut hizmet paketi.

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
