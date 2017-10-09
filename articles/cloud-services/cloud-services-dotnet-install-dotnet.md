---
title: Azure Cloud Services rolleri .NET aaaInstall | Microsoft Docs
description: "Bu makalede nasıl toomanually yüklemesi hello .NET Framework üzerinde bulut hizmeti web ve çalışan rolleri açıklayan"
services: cloud-services
documentationcenter: .net
author: thraka
manager: timlt
editor: 
ms.assetid: 8d1243dc-879c-4d1f-9ed0-eecd1f6a6653
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: adegeo
ms.openlocfilehash: 45f0f30221292f98c591511b091b02ebe1c1272c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-net-on-azure-cloud-services-roles"></a>Azure Cloud Services rollerinde .NET yükleme
Bu makalede, nasıl Azure konuk işletim sistemi gelir yok .NET Framework'ün tooinstall sürümlerini hello açıklanmaktadır. Bulut hizmeti web ve çalışan rolleri hello konuk işletim sistemi tooconfigure üzerinde .NET kullanabilirsiniz.

Örneğin, Merhaba, herhangi bir .NET 4.6 sürümünden ile gelmez, konuk işletim sistemi ailesi 4, .NET 4.6.1 yükleyebilirsiniz. (Merhaba konuk işletim sistemi ailesi 5 .NET 4.6 ile gelir.) Merhaba hello en son bilgiler için Azure konuk işletim sistemi sürümü, hello bkz [Azure konuk işletim sistemi sürüm haber](cloud-services-guestos-update-matrix.md). 

>[!IMPORTANT]
>Hello Azure SDK 2.9 .NET 4.6 hello konuk işletim sistemi ailesi 4 veya önceki bir sürümü dağıtma bir kısıtlama var. Merhaba kısıtlama için bir düzeltme hello üzerinde kullanılabilir [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.

Bulut hizmeti projenizi bir parçası olarak hello .NET web yükleyicisi tooinstall .NET web ve çalışan rolleri içerir. Merhaba rolün başlangıç görevleri bir parçası olarak Hello Yükleyicisi'ni başlatın. 

## <a name="add-hello-net-installer-tooyour-project"></a>Merhaba .NET yükleyici tooyour proje ekleyin
Merhaba, .NET Framework için toodownload hello web yükleyicisi hello sürüm tooinstall istediğinizi seçin:

* [.NET 4.7 web yükleyicisi](http://go.microsoft.com/fwlink/?LinkId=825298)
* [.NET 4.6.1 web yükleyicisi](http://go.microsoft.com/fwlink/?LinkId=671729)

tooadd hello Yükleyicisi için bir *web* rol:
  1. İçinde **Çözüm Gezgini**altında **rolleri** , bulut hizmet projenize sağ tıklayın, *web* rolü ve select **Ekle**  >  **Yeni klasör**. Adlı bir klasör oluşturun **bin**.
  2. Merhaba bin klasörü sağ tıklatın ve seçin **Ekle** > **varolan öğeyi**. Merhaba .NET Yükleyicisi'ni seçin ve toohello bin klasörü ekleyin.
  
tooadd hello Yükleyicisi için bir *çalışan* rol:
* Sağ tıklayın, *çalışan* rolü ve select **Ekle** > **varolan öğeyi**. Merhaba .NET Yükleyicisi'ni seçin ve toohello rolünü ekleyin. 

Bu şekilde toohello rol içerik klasördeki dosyalar eklendiğinde bunlar otomatik olarak tooyour bulut hizmet paketi eklenir. Merhaba olan sonra hello sanal makinede dağıtılan tooa tutarlı konumu dosyaları. Böylece tüm rolleri hello yükleyici kopyasını, bulut hizmeti içindeki her web ve çalışan rolü için bu işlemi yineleyin.

> [!NOTE]
> Uygulamanız .NET 4.6 hedefliyorsa bile, bulut hizmeti rolü'nde .NET 4.6.1 yüklemeniz gerekir. Merhaba konuk işletim sistemi içeren hello Bilgi Bankası [3098779 güncelleştirme](https://support.microsoft.com/kb/3098779) ve [3097997 güncelleştirme](https://support.microsoft.com/kb/3097997). .NET 4.6 hello Bilgi Bankası güncelleştirmeleri üzerinde yüklüyse, .NET uygulamaları çalıştırdığınızda, sorunlar oluşabilir. Bu sorunlar, tooavoid sürümü 4.6 yerine .NET 4.6.1 yükleyin. Daha fazla bilgi için bkz: Merhaba [Bilgi Bankası makalesi 3118750](https://support.microsoft.com/kb/3118750).
> 
> 

![Rol içeriğiyle Installer dosyaları][1]

## <a name="define-startup-tasks-for-your-roles"></a>Başlangıç görevleri, rolleri tanımlama
Bir rolü başlamadan önce başlangıç görevleri tooperform işlemleri kullanabilirsiniz. Herhangi bir uygulama kodu çalıştırmadan önce bu hello framework hello başlangıç görevinin parçası sağlar gibi hello .NET Framework yükleme yüklenir. Başlangıç görevleri hakkında daha fazla bilgi için bkz: [Azure'da başlangıç görevleri çalıştırma](cloud-services-startup-tasks.md). 

1. Aşağıdaki içerik toohello ServiceDefinition.csdef dosyasına hello altında hello eklemek **WebRole** veya **örn** düğüm tüm rolleri için:
   
    ```xml
    <LocalResources>
      <LocalStorage name="NETFXInstall" sizeInMB="1024" cleanOnRoleRecycle="false" />
    </LocalResources>    
    <Startup>
      <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
        <Environment>
          <Variable name="PathToNETFXInstall">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='NETFXInstall']/@path" />
          </Variable>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
    ```
   
    Merhaba önceki yapılandırma hello konsol komutu çalıştırır `install.cmd` .NET Framework ile yönetici ayrıcalıkları tooinstall hello. Merhaba yapılandırma da oluşturur bir **LocalStorage** adlı öğe **NETFXInstall**. Merhaba başlangıç betiği bu yerel depolama kaynağı hello geçici klasörü toouse ayarlar. 
    
    > [!IMPORTANT]
    > tooensure düzeltmek hello framework, bu kaynak tooat kümesi hello boyutu yüklemesi en az 1024 MB.
    
    Başlangıç görevleri hakkında daha fazla bilgi için bkz: [ortak Azure Cloud Services başlangıç görevleri](cloud-services-startup-tasks-common.md).

2. Adlı bir dosya oluşturun **Install.cmd** ve hello aşağıdaki toohello betiğin yüklemek ekleyin.

    Merhaba betik hello belirtilen hello .NET Framework sürümünü hello makinede hello kayıt defteri sorgulayarak yüklü olup olmadığını denetler. Merhaba .NET sürüm yüklü değilse, daha sonra hello .NET web yükleyicisi açılır. toohelp sorunları gidermek, hello betik günlüklerini depolanan tüm etkinlik toohello startuptasklog-(geçerli tarih ve saat) .txt dosya **InstallLogs** yerel depolama.

    > [!IMPORTANT]
    > Temel metin düzenleyici gibi Windows Not Defteri'ni toocreate hello Install.cmd dosyasını kullanın. Visual Studio toocreate bir metin dosyasını kullanın ve hello uzantısı too.cmd değiştirirseniz hello dosya UTF-8 bayt sırası işareti içeriyor olabilir. Merhaba komut Hello ilk satırını çalıştırdığınızda bu işareti hataya neden olabilir. tooavoid bu hatayı hello bayt sırası işlemesi atlanabilir REM deyimi komut dosyası hello ilk satırının başlangıç yapın. 
    > 
    >
   
    ```cmd
    REM Set hello value of netfx tooinstall appropriate .NET Framework. 
    REM ***** tooinstall .NET 4.5.2 set hello variable netfx too"NDP452" *****
    REM ***** tooinstall .NET 4.6 set hello variable netfx too"NDP46" *****
    REM ***** tooinstall .NET 4.6.1 set hello variable netfx too"NDP461" *****
    REM ***** tooinstall .NET 4.6.2 set hello variable netfx too"NDP462" *****
    REM ***** tooinstall .NET 4.7 set hello variable netfx too"NDP47" *****
    set netfx="NDP47"

    REM ***** Set script start timestamp *****
    set timehour=%time:~0,2%
    set timestamp=%date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2%
    set "log=install.cmd started %timestamp%."

    REM ***** Exit script if running in Emulator *****
    if %ComputeEmulatorRunning%=="true" goto exit

    REM ***** Needed toocorrectly install .NET 4.6.1, otherwise you may see an out of disk space error *****
    set TMP=%PathToNETFXInstall%
    set TEMP=%PathToNETFXInstall%

    REM ***** Setup .NET filenames and registry keys *****
    if %netfx%=="NDP47" goto NDP47
    if %netfx%=="NDP462" goto NDP462
    if %netfx%=="NDP461" goto NDP461
    if %netfx%=="NDP46" goto NDP46
        set "netfxinstallfile=NDP452-KB2901954-Web.exe"
        set netfxregkey="0x5cbf5"
        goto logtimestamp

    :NDP46
    set "netfxinstallfile=NDP46-KB3045560-Web.exe"
    set netfxregkey="0x6004f"
    goto logtimestamp

    :NDP461
    set "netfxinstallfile=NDP461-KB3102438-Web.exe"
    set netfxregkey="0x6040e"
    goto logtimestamp

    :NDP462
    set "netfxinstallfile=NDP462-KB3151802-Web.exe"
    set netfxregkey="0x60632"

    :NDP47
    set "netfxinstallfile=NDP47-KB3186500-Web.exe"
    set netfxregkey="0x707FE"

    :logtimestamp
    REM ***** Setup LogFile with timestamp *****
    md "%PathToNETFXInstall%\log"
    set startuptasklog="%PathToNETFXInstall%log\startuptasklog-%timestamp%.txt"
    set netfxinstallerlog="%PathToNETFXInstall%log\NetFXInstallerLog-%timestamp%"
    echo %log% >> %startuptasklog%
    echo Logfile generated at: %startuptasklog% >> %startuptasklog%
    echo TMP set to: %TMP% >> %startuptasklog%
    echo TEMP set to: %TEMP% >> %startuptasklog%

    REM ***** Check if .NET is installed *****
    echo Checking if .NET (%netfx%) is installed >> %startuptasklog%
    set /A netfxregkeydecimal=%netfxregkey%
    set foundkey=0
    FOR /F "usebackq skip=2 tokens=1,2*" %%A in (`reg query "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full" /v Release 2^>nul`) do @set /A foundkey=%%C
    echo Minimum required key: %netfxregkeydecimal% -- found key: %foundkey% >> %startuptasklog%
    if %foundkey% GEQ %netfxregkeydecimal% goto installed

    REM ***** Installing .NET *****
    echo Installing .NET with commandline: start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog%  /chainingpackage "CloudService Startup Task" >> %startuptasklog%
    start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog% /chainingpackage "CloudService Startup Task" >> %startuptasklog% 2>>&1
    if %ERRORLEVEL%== 0 goto installed
        echo .NET installer exited with code %ERRORLEVEL% >> %startuptasklog%    
        if %ERRORLEVEL%== 3010 goto restart
        if %ERRORLEVEL%== 1641 goto restart
        echo .NET (%netfx%) install failed with Error Code %ERRORLEVEL%. Further logs can be found in %netfxinstallerlog% >> %startuptasklog%

    :restart
    echo Restarting toocomplete .NET (%netfx%) installation >> %startuptasklog%
    EXIT /B %ERRORLEVEL%

    :installed
    echo .NET (%netfx%) is installed >> %startuptasklog%

    :end
    echo install.cmd completed: %date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2% >> %startuptasklog%

    :exit
    EXIT /B 0
    ```
   
   > [!NOTE]
   > Bu komut dosyası gösterilmektedir nasıl tooinstall .NET 4.5.2 veya sürekliliği, .NET 4.5.2 zaten mevcut olsa bile için sürüm 4.6 hello Azure konuk işletim sistemi. Doğrudan sürümü 4.6, yerine .NET 4.6.1 hello açıklandığı gibi yüklemeniz gerekir [Bilgi Bankası makalesi 3118750](https://support.microsoft.com/kb/3118750).
   > 
   > 

3. Kullanarak hello Install.cmd dosya tooeach Rol Ekle **Ekle** > **varolan öğeyi** içinde **Çözüm Gezgini** bu konunun önceki kısımlarında açıklandığı gibi. 

    Bu adım tamamlandıktan sonra tüm rolleri hello .NET yükleyici dosyası ve hello Install.cmd dosyasını olması gerekir.

   ![Rol içeriğe sahip tüm dosyalar][2]

## <a name="configure-diagnostics-tootransfer-startup-logs-tooblob-storage"></a>Tanılama tootransfer başlangıç günlükleri tooBlob depolamayı yapılandırma
Yükleme sorunlarını giderme toosimplify, hello başlatma işlemi tarafından oluşturulan tüm günlük dosyalarını komut dosyası veya .NET yükleyici tooAzure Blob storage'hello Azure tanılama tootransfer yapılandırabilirsiniz. Bu yaklaşımı kullanarak, Blob depolama alanından hello günlük dosyalarını indirme yerine hello rol tooremote Desktop'a tarafından hello günlüklerini görüntüleyebilirsiniz.

tooconfigure tanılama hello diagnostics.wadcfgx dosyasını açın ve içerik hello altında aşağıdaki hello eklemek **dizinleri** düğümü: 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

Bu XML hello hello günlük dizininde tanılama tootransfer hello dosyaları yapılandırır **NETFXInstall** kaynak toohello hello tanılama depolama hesabı **netfx yükleme** blob kapsayıcısı.

## <a name="deploy-your-cloud-service"></a>Bulut hizmetinize dağıtın
Bulut hizmetinizi dağıttığınızda, henüz yüklü değilse hello başlangıç görevleri hello .NET Framework yükleyin. Bulut hizmeti rollerinizi hello olan *meşgul* hello framework yüklenirken durum. Merhaba framework yüklemesi bir yeniden başlatma gerektirirse, hello hizmet rolleri de yeniden başlatılabilir. 

## <a name="additional-resources"></a>Ek kaynaklar
* [Merhaba .NET Framework yükleme][Installing hello .NET Framework]
* [Hangi .NET Framework sürümlerinin yüklü olduğunu belirleme][How to: Determine Which .NET Framework Versions Are Installed]
* [.NET Framework yükleme sorunlarını giderme][Troubleshooting .NET Framework Installations]

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing hello .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
