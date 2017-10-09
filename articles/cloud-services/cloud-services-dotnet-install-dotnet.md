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
# <a name="install-net-on-azure-cloud-services-roles"></a><span data-ttu-id="50487-103">Azure Cloud Services rollerinde .NET yükleme</span><span class="sxs-lookup"><span data-stu-id="50487-103">Install .NET on Azure Cloud Services roles</span></span>
<span data-ttu-id="50487-104">Bu makalede, nasıl Azure konuk işletim sistemi gelir yok .NET Framework'ün tooinstall sürümlerini hello açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="50487-104">This article describes how tooinstall versions of .NET Framework that don't come with hello Azure Guest OS.</span></span> <span data-ttu-id="50487-105">Bulut hizmeti web ve çalışan rolleri hello konuk işletim sistemi tooconfigure üzerinde .NET kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50487-105">You can use .NET on hello Guest OS tooconfigure your cloud service web and worker roles.</span></span>

<span data-ttu-id="50487-106">Örneğin, Merhaba, herhangi bir .NET 4.6 sürümünden ile gelmez, konuk işletim sistemi ailesi 4, .NET 4.6.1 yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50487-106">For example, you can install .NET 4.6.1 on hello Guest OS family 4, which doesn't come with any release of .NET 4.6.</span></span> <span data-ttu-id="50487-107">(Merhaba konuk işletim sistemi ailesi 5 .NET 4.6 ile gelir.) Merhaba hello en son bilgiler için Azure konuk işletim sistemi sürümü, hello bkz [Azure konuk işletim sistemi sürüm haber](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="50487-107">(hello Guest OS family 5 does come with .NET 4.6.) For hello latest information on hello Azure Guest OS releases, see hello [Azure Guest OS release news](cloud-services-guestos-update-matrix.md).</span></span> 

>[!IMPORTANT]
><span data-ttu-id="50487-108">Hello Azure SDK 2.9 .NET 4.6 hello konuk işletim sistemi ailesi 4 veya önceki bir sürümü dağıtma bir kısıtlama var.</span><span class="sxs-lookup"><span data-stu-id="50487-108">hello Azure SDK 2.9 contains a restriction on deploying .NET 4.6 on hello Guest OS family 4 or earlier.</span></span> <span data-ttu-id="50487-109">Merhaba kısıtlama için bir düzeltme hello üzerinde kullanılabilir [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span><span class="sxs-lookup"><span data-stu-id="50487-109">A fix for hello restriction is available on hello [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span></span>

<span data-ttu-id="50487-110">Bulut hizmeti projenizi bir parçası olarak hello .NET web yükleyicisi tooinstall .NET web ve çalışan rolleri içerir.</span><span class="sxs-lookup"><span data-stu-id="50487-110">tooinstall .NET on your web and worker roles, include hello .NET web installer as part of your cloud service project.</span></span> <span data-ttu-id="50487-111">Merhaba rolün başlangıç görevleri bir parçası olarak Hello Yükleyicisi'ni başlatın.</span><span class="sxs-lookup"><span data-stu-id="50487-111">Start hello installer as part of hello role's startup tasks.</span></span> 

## <a name="add-hello-net-installer-tooyour-project"></a><span data-ttu-id="50487-112">Merhaba .NET yükleyici tooyour proje ekleyin</span><span class="sxs-lookup"><span data-stu-id="50487-112">Add hello .NET installer tooyour project</span></span>
<span data-ttu-id="50487-113">Merhaba, .NET Framework için toodownload hello web yükleyicisi hello sürüm tooinstall istediğinizi seçin:</span><span class="sxs-lookup"><span data-stu-id="50487-113">toodownload hello web installer for hello .NET Framework, choose hello version that you want tooinstall:</span></span>

* [<span data-ttu-id="50487-114">.NET 4.7 web yükleyicisi</span><span class="sxs-lookup"><span data-stu-id="50487-114">.NET 4.7 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=825298)
* [<span data-ttu-id="50487-115">.NET 4.6.1 web yükleyicisi</span><span class="sxs-lookup"><span data-stu-id="50487-115">.NET 4.6.1 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=671729)

<span data-ttu-id="50487-116">tooadd hello Yükleyicisi için bir *web* rol:</span><span class="sxs-lookup"><span data-stu-id="50487-116">tooadd hello installer for a *web* role:</span></span>
  1. <span data-ttu-id="50487-117">İçinde **Çözüm Gezgini**altında **rolleri** , bulut hizmet projenize sağ tıklayın, *web* rolü ve select **Ekle**  >  **Yeni klasör**.</span><span class="sxs-lookup"><span data-stu-id="50487-117">In **Solution Explorer**, under **Roles** in your cloud service project, right-click your *web* role and select **Add** > **New Folder**.</span></span> <span data-ttu-id="50487-118">Adlı bir klasör oluşturun **bin**.</span><span class="sxs-lookup"><span data-stu-id="50487-118">Create a folder named **bin**.</span></span>
  2. <span data-ttu-id="50487-119">Merhaba bin klasörü sağ tıklatın ve seçin **Ekle** > **varolan öğeyi**.</span><span class="sxs-lookup"><span data-stu-id="50487-119">Right-click hello bin folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="50487-120">Merhaba .NET Yükleyicisi'ni seçin ve toohello bin klasörü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="50487-120">Select hello .NET installer and add it toohello bin folder.</span></span>
  
<span data-ttu-id="50487-121">tooadd hello Yükleyicisi için bir *çalışan* rol:</span><span class="sxs-lookup"><span data-stu-id="50487-121">tooadd hello installer for a *worker* role:</span></span>
* <span data-ttu-id="50487-122">Sağ tıklayın, *çalışan* rolü ve select **Ekle** > **varolan öğeyi**.</span><span class="sxs-lookup"><span data-stu-id="50487-122">Right-click your *worker* role and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="50487-123">Merhaba .NET Yükleyicisi'ni seçin ve toohello rolünü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="50487-123">Select hello .NET installer and add it toohello role.</span></span> 

<span data-ttu-id="50487-124">Bu şekilde toohello rol içerik klasördeki dosyalar eklendiğinde bunlar otomatik olarak tooyour bulut hizmet paketi eklenir.</span><span class="sxs-lookup"><span data-stu-id="50487-124">When files are added in this way toohello role content folder, they're automatically added tooyour cloud service package.</span></span> <span data-ttu-id="50487-125">Merhaba olan sonra hello sanal makinede dağıtılan tooa tutarlı konumu dosyaları.</span><span class="sxs-lookup"><span data-stu-id="50487-125">hello files are then deployed tooa consistent location on hello virtual machine.</span></span> <span data-ttu-id="50487-126">Böylece tüm rolleri hello yükleyici kopyasını, bulut hizmeti içindeki her web ve çalışan rolü için bu işlemi yineleyin.</span><span class="sxs-lookup"><span data-stu-id="50487-126">Repeat this process for each web and worker role in your cloud service so that all roles have a copy of hello installer.</span></span>

> [!NOTE]
> <span data-ttu-id="50487-127">Uygulamanız .NET 4.6 hedefliyorsa bile, bulut hizmeti rolü'nde .NET 4.6.1 yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="50487-127">You should install .NET 4.6.1 on your cloud service role even if your application targets .NET 4.6.</span></span> <span data-ttu-id="50487-128">Merhaba konuk işletim sistemi içeren hello Bilgi Bankası [3098779 güncelleştirme](https://support.microsoft.com/kb/3098779) ve [3097997 güncelleştirme](https://support.microsoft.com/kb/3097997).</span><span class="sxs-lookup"><span data-stu-id="50487-128">hello Guest OS includes hello Knowledge Base [update 3098779](https://support.microsoft.com/kb/3098779) and [update 3097997](https://support.microsoft.com/kb/3097997).</span></span> <span data-ttu-id="50487-129">.NET 4.6 hello Bilgi Bankası güncelleştirmeleri üzerinde yüklüyse, .NET uygulamaları çalıştırdığınızda, sorunlar oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="50487-129">Issues can occur when you run your .NET applications if .NET 4.6 is installed on top of hello Knowledge Base updates.</span></span> <span data-ttu-id="50487-130">Bu sorunlar, tooavoid sürümü 4.6 yerine .NET 4.6.1 yükleyin.</span><span class="sxs-lookup"><span data-stu-id="50487-130">tooavoid these issues, install .NET 4.6.1 rather than version 4.6.</span></span> <span data-ttu-id="50487-131">Daha fazla bilgi için bkz: Merhaba [Bilgi Bankası makalesi 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="50487-131">For more information, see hello [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
> 
> 

![Rol içeriğiyle Installer dosyaları][1]

## <a name="define-startup-tasks-for-your-roles"></a><span data-ttu-id="50487-133">Başlangıç görevleri, rolleri tanımlama</span><span class="sxs-lookup"><span data-stu-id="50487-133">Define startup tasks for your roles</span></span>
<span data-ttu-id="50487-134">Bir rolü başlamadan önce başlangıç görevleri tooperform işlemleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50487-134">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="50487-135">Herhangi bir uygulama kodu çalıştırmadan önce bu hello framework hello başlangıç görevinin parçası sağlar gibi hello .NET Framework yükleme yüklenir.</span><span class="sxs-lookup"><span data-stu-id="50487-135">Installing hello .NET Framework as part of hello startup task ensures that hello framework is installed before any application code is run.</span></span> <span data-ttu-id="50487-136">Başlangıç görevleri hakkında daha fazla bilgi için bkz: [Azure'da başlangıç görevleri çalıştırma](cloud-services-startup-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="50487-136">For more information on startup tasks, see [Run startup tasks in Azure](cloud-services-startup-tasks.md).</span></span> 

1. <span data-ttu-id="50487-137">Aşağıdaki içerik toohello ServiceDefinition.csdef dosyasına hello altında hello eklemek **WebRole** veya **örn** düğüm tüm rolleri için:</span><span class="sxs-lookup"><span data-stu-id="50487-137">Add hello following content toohello ServiceDefinition.csdef file under hello **WebRole** or **WorkerRole** node for all roles:</span></span>
   
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
   
    <span data-ttu-id="50487-138">Merhaba önceki yapılandırma hello konsol komutu çalıştırır `install.cmd` .NET Framework ile yönetici ayrıcalıkları tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="50487-138">hello preceding configuration runs hello console command `install.cmd` with administrator privileges tooinstall hello .NET Framework.</span></span> <span data-ttu-id="50487-139">Merhaba yapılandırma da oluşturur bir **LocalStorage** adlı öğe **NETFXInstall**.</span><span class="sxs-lookup"><span data-stu-id="50487-139">hello configuration also creates a **LocalStorage** element named **NETFXInstall**.</span></span> <span data-ttu-id="50487-140">Merhaba başlangıç betiği bu yerel depolama kaynağı hello geçici klasörü toouse ayarlar.</span><span class="sxs-lookup"><span data-stu-id="50487-140">hello startup script sets hello temp folder toouse this local storage resource.</span></span> 
    
    > [!IMPORTANT]
    > <span data-ttu-id="50487-141">tooensure düzeltmek hello framework, bu kaynak tooat kümesi hello boyutu yüklemesi en az 1024 MB.</span><span class="sxs-lookup"><span data-stu-id="50487-141">tooensure correct installation of hello framework, set hello size of this resource tooat least 1,024 MB.</span></span>
    
    <span data-ttu-id="50487-142">Başlangıç görevleri hakkında daha fazla bilgi için bkz: [ortak Azure Cloud Services başlangıç görevleri](cloud-services-startup-tasks-common.md).</span><span class="sxs-lookup"><span data-stu-id="50487-142">For more information about startup tasks, see [Common Azure Cloud Services startup tasks](cloud-services-startup-tasks-common.md).</span></span>

2. <span data-ttu-id="50487-143">Adlı bir dosya oluşturun **Install.cmd** ve hello aşağıdaki toohello betiğin yüklemek ekleyin.</span><span class="sxs-lookup"><span data-stu-id="50487-143">Create a file named **install.cmd** and add hello following install script toohello file.</span></span>

    <span data-ttu-id="50487-144">Merhaba betik hello belirtilen hello .NET Framework sürümünü hello makinede hello kayıt defteri sorgulayarak yüklü olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="50487-144">hello script checks whether hello specified version of hello .NET Framework is already installed on hello machine by querying hello registry.</span></span> <span data-ttu-id="50487-145">Merhaba .NET sürüm yüklü değilse, daha sonra hello .NET web yükleyicisi açılır.</span><span class="sxs-lookup"><span data-stu-id="50487-145">If hello .NET version is not installed, then hello .NET web installer is opened.</span></span> <span data-ttu-id="50487-146">toohelp sorunları gidermek, hello betik günlüklerini depolanan tüm etkinlik toohello startuptasklog-(geçerli tarih ve saat) .txt dosya **InstallLogs** yerel depolama.</span><span class="sxs-lookup"><span data-stu-id="50487-146">toohelp troubleshoot any issues, hello script logs all activity toohello file startuptasklog-(current date and time).txt that is stored in **InstallLogs** local storage.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="50487-147">Temel metin düzenleyici gibi Windows Not Defteri'ni toocreate hello Install.cmd dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="50487-147">Use a basic text editor like Windows Notepad toocreate hello install.cmd file.</span></span> <span data-ttu-id="50487-148">Visual Studio toocreate bir metin dosyasını kullanın ve hello uzantısı too.cmd değiştirirseniz hello dosya UTF-8 bayt sırası işareti içeriyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="50487-148">If you use Visual Studio toocreate a text file and change hello extension too.cmd, hello file might still contain a UTF-8 byte order mark.</span></span> <span data-ttu-id="50487-149">Merhaba komut Hello ilk satırını çalıştırdığınızda bu işareti hataya neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="50487-149">This mark can cause an error when hello first line of hello script is run.</span></span> <span data-ttu-id="50487-150">tooavoid bu hatayı hello bayt sırası işlemesi atlanabilir REM deyimi komut dosyası hello ilk satırının başlangıç yapın.</span><span class="sxs-lookup"><span data-stu-id="50487-150">tooavoid this error, make hello first line of hello script a REM statement that can be skipped by hello byte order processing.</span></span> 
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
   > <span data-ttu-id="50487-151">Bu komut dosyası gösterilmektedir nasıl tooinstall .NET 4.5.2 veya sürekliliği, .NET 4.5.2 zaten mevcut olsa bile için sürüm 4.6 hello Azure konuk işletim sistemi.</span><span class="sxs-lookup"><span data-stu-id="50487-151">This script shows how tooinstall .NET 4.5.2 or version 4.6 for continuity, even though .NET 4.5.2 is already available on hello Azure Guest OS.</span></span> <span data-ttu-id="50487-152">Doğrudan sürümü 4.6, yerine .NET 4.6.1 hello açıklandığı gibi yüklemeniz gerekir [Bilgi Bankası makalesi 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="50487-152">You should directly install .NET 4.6.1 rather than version 4.6, as described in hello [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
   > 
   > 

3. <span data-ttu-id="50487-153">Kullanarak hello Install.cmd dosya tooeach Rol Ekle **Ekle** > **varolan öğeyi** içinde **Çözüm Gezgini** bu konunun önceki kısımlarında açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="50487-153">Add hello install.cmd file tooeach role by using **Add** > **Existing Item** in **Solution Explorer** as described earlier in this topic.</span></span> 

    <span data-ttu-id="50487-154">Bu adım tamamlandıktan sonra tüm rolleri hello .NET yükleyici dosyası ve hello Install.cmd dosyasını olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="50487-154">After this step is complete, all roles should have hello .NET installer file and hello install.cmd file.</span></span>

   ![Rol içeriğe sahip tüm dosyalar][2]

## <a name="configure-diagnostics-tootransfer-startup-logs-tooblob-storage"></a><span data-ttu-id="50487-156">Tanılama tootransfer başlangıç günlükleri tooBlob depolamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="50487-156">Configure Diagnostics tootransfer startup logs tooBlob storage</span></span>
<span data-ttu-id="50487-157">Yükleme sorunlarını giderme toosimplify, hello başlatma işlemi tarafından oluşturulan tüm günlük dosyalarını komut dosyası veya .NET yükleyici tooAzure Blob storage'hello Azure tanılama tootransfer yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50487-157">toosimplify troubleshooting installation issues, you can configure Azure Diagnostics tootransfer any log files generated by hello startup script or hello .NET installer tooAzure Blob storage.</span></span> <span data-ttu-id="50487-158">Bu yaklaşımı kullanarak, Blob depolama alanından hello günlük dosyalarını indirme yerine hello rol tooremote Desktop'a tarafından hello günlüklerini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50487-158">By using this approach, you can view hello logs by downloading hello log files from Blob storage rather than having tooremote desktop into hello role.</span></span>

<span data-ttu-id="50487-159">tooconfigure tanılama hello diagnostics.wadcfgx dosyasını açın ve içerik hello altında aşağıdaki hello eklemek **dizinleri** düğümü:</span><span class="sxs-lookup"><span data-stu-id="50487-159">tooconfigure Diagnostics, open hello diagnostics.wadcfgx file and add hello following content under hello **Directories** node:</span></span> 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

<span data-ttu-id="50487-160">Bu XML hello hello günlük dizininde tanılama tootransfer hello dosyaları yapılandırır **NETFXInstall** kaynak toohello hello tanılama depolama hesabı **netfx yükleme** blob kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="50487-160">This XML configures Diagnostics tootransfer hello files in hello log directory in hello **NETFXInstall** resource toohello Diagnostics storage account in hello **netfx-install** blob container.</span></span>

## <a name="deploy-your-cloud-service"></a><span data-ttu-id="50487-161">Bulut hizmetinize dağıtın</span><span class="sxs-lookup"><span data-stu-id="50487-161">Deploy your cloud service</span></span>
<span data-ttu-id="50487-162">Bulut hizmetinizi dağıttığınızda, henüz yüklü değilse hello başlangıç görevleri hello .NET Framework yükleyin.</span><span class="sxs-lookup"><span data-stu-id="50487-162">When you deploy your cloud service, hello startup tasks install hello .NET Framework if it's not already installed.</span></span> <span data-ttu-id="50487-163">Bulut hizmeti rollerinizi hello olan *meşgul* hello framework yüklenirken durum.</span><span class="sxs-lookup"><span data-stu-id="50487-163">Your cloud service roles are in hello *busy* state while hello framework is being installed.</span></span> <span data-ttu-id="50487-164">Merhaba framework yüklemesi bir yeniden başlatma gerektirirse, hello hizmet rolleri de yeniden başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="50487-164">If hello framework installation requires a restart, hello service roles might also restart.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="50487-165">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="50487-165">Additional resources</span></span>
* <span data-ttu-id="50487-166">[Merhaba .NET Framework yükleme][Installing hello .NET Framework]</span><span class="sxs-lookup"><span data-stu-id="50487-166">[Installing hello .NET Framework][Installing hello .NET Framework]</span></span>
* <span data-ttu-id="50487-167">[Hangi .NET Framework sürümlerinin yüklü olduğunu belirleme][How to: Determine Which .NET Framework Versions Are Installed]</span><span class="sxs-lookup"><span data-stu-id="50487-167">[Determine which .NET Framework versions are installed][How to: Determine Which .NET Framework Versions Are Installed]</span></span>
* <span data-ttu-id="50487-168">[.NET Framework yükleme sorunlarını giderme][Troubleshooting .NET Framework Installations]</span><span class="sxs-lookup"><span data-stu-id="50487-168">[Troubleshooting .NET Framework installations][Troubleshooting .NET Framework Installations]</span></span>

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing hello .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
