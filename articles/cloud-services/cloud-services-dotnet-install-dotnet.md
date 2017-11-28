---
title: "Azure Cloud Services rollerinde .NET yükleme | Microsoft Docs"
description: "Bu makalede, .NET Framework üzerinde bulut hizmeti web ve çalışan rolleri el ile yüklemek açıklar"
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
ms.openlocfilehash: a9cffa275ae6b9315b821d3160b17a997a1523f7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="install-net-on-azure-cloud-services-roles"></a><span data-ttu-id="fe9bd-103">Azure Cloud Services rollerinde .NET yükleme</span><span class="sxs-lookup"><span data-stu-id="fe9bd-103">Install .NET on Azure Cloud Services roles</span></span>
<span data-ttu-id="fe9bd-104">Bu makalede, Azure konuk işletim Sistemleri ile gelir yok .NET Framework sürümleri yüklemeyi açıklar.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-104">This article describes how to install versions of .NET Framework that don't come with the Azure Guest OS.</span></span> <span data-ttu-id="fe9bd-105">Bulut hizmeti web ve çalışan rolleri yapılandırmak için konuk işletim sisteminde .NET kullanın.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-105">You can use .NET on the Guest OS to configure your cloud service web and worker roles.</span></span>

<span data-ttu-id="fe9bd-106">Örneğin, herhangi bir .NET 4.6 sürümünden ile gelmez konuk işletim sistemi ailesi 4, .NET 4.6.1 yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-106">For example, you can install .NET 4.6.1 on the Guest OS family 4, which doesn't come with any release of .NET 4.6.</span></span> <span data-ttu-id="fe9bd-107">(5 konuk işletim sistemi ailesi .NET 4.6 ile gelir.) En son Azure konuk işletim sistemi sürümleri hakkında bilgi için [Azure konuk işletim sistemi sürüm haber](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="fe9bd-107">(The Guest OS family 5 does come with .NET 4.6.) For the latest information on the Azure Guest OS releases, see the [Azure Guest OS release news](cloud-services-guestos-update-matrix.md).</span></span> 

>[!IMPORTANT]
><span data-ttu-id="fe9bd-108">Azure SDK 2.9 .NET 4.6 konuk işletim sistemi ailesi 4 veya önceki bir sürümü dağıtma üzerine bir kısıtlama var.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-108">The Azure SDK 2.9 contains a restriction on deploying .NET 4.6 on the Guest OS family 4 or earlier.</span></span> <span data-ttu-id="fe9bd-109">Kısıtlama için bir düzeltme edinilebilir [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-109">A fix for the restriction is available on the [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span></span>

<span data-ttu-id="fe9bd-110">.NET web ve çalışan rollerinde yüklemek için bulut hizmeti projenizi bir parçası olarak .NET web yükleyicisi içerir.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-110">To install .NET on your web and worker roles, include the .NET web installer as part of your cloud service project.</span></span> <span data-ttu-id="fe9bd-111">Yükleyici rolün başlangıç görevleri bir parçası olarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-111">Start the installer as part of the role's startup tasks.</span></span> 

## <a name="add-the-net-installer-to-your-project"></a><span data-ttu-id="fe9bd-112">.NET yükleyici projenize ekleyin</span><span class="sxs-lookup"><span data-stu-id="fe9bd-112">Add the .NET installer to your project</span></span>
<span data-ttu-id="fe9bd-113">.NET Framework için web yükleyici indirmek için yüklemek istediğiniz sürümü seçin:</span><span class="sxs-lookup"><span data-stu-id="fe9bd-113">To download the web installer for the .NET Framework, choose the version that you want to install:</span></span>

* [<span data-ttu-id="fe9bd-114">.NET 4.7 web yükleyicisi</span><span class="sxs-lookup"><span data-stu-id="fe9bd-114">.NET 4.7 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=825298)
* [<span data-ttu-id="fe9bd-115">.NET 4.6.1 web yükleyicisi</span><span class="sxs-lookup"><span data-stu-id="fe9bd-115">.NET 4.6.1 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=671729)

<span data-ttu-id="fe9bd-116">Yükleyicisi eklemek için bir *web* rol:</span><span class="sxs-lookup"><span data-stu-id="fe9bd-116">To add the installer for a *web* role:</span></span>
  1. <span data-ttu-id="fe9bd-117">İçinde **Çözüm Gezgini**altında **rolleri** , bulut hizmet projenize sağ tıklayın, *web* rolü ve select **Ekle**  >  **Yeni klasör**.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-117">In **Solution Explorer**, under **Roles** in your cloud service project, right-click your *web* role and select **Add** > **New Folder**.</span></span> <span data-ttu-id="fe9bd-118">Adlı bir klasör oluşturun **bin**.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-118">Create a folder named **bin**.</span></span>
  2. <span data-ttu-id="fe9bd-119">Bin klasörü sağ tıklatın ve seçin **Ekle** > **varolan öğeyi**.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-119">Right-click the bin folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="fe9bd-120">.NET Yükleyicisi'ni seçin ve bin klasörüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-120">Select the .NET installer and add it to the bin folder.</span></span>
  
<span data-ttu-id="fe9bd-121">Yükleyicisi eklemek için bir *çalışan* rol:</span><span class="sxs-lookup"><span data-stu-id="fe9bd-121">To add the installer for a *worker* role:</span></span>
* <span data-ttu-id="fe9bd-122">Sağ tıklayın, *çalışan* rolü ve select **Ekle** > **varolan öğeyi**.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-122">Right-click your *worker* role and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="fe9bd-123">.NET Yükleyicisi'ni seçin ve role ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-123">Select the .NET installer and add it to the role.</span></span> 

<span data-ttu-id="fe9bd-124">Bu şekilde rol içerik klasörüne dosyalar eklendiğinde bunlar otomatik olarak, bulut hizmet paketi eklenir.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-124">When files are added in this way to the role content folder, they're automatically added to your cloud service package.</span></span> <span data-ttu-id="fe9bd-125">Dosyaları daha sonra sanal makinede tutarlı bir konumuna dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-125">The files are then deployed to a consistent location on the virtual machine.</span></span> <span data-ttu-id="fe9bd-126">Böylece tüm rolleri yükleyici kopyasını, bulut hizmeti içindeki her web ve çalışan rolü için bu işlemi yineleyin.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-126">Repeat this process for each web and worker role in your cloud service so that all roles have a copy of the installer.</span></span>

> [!NOTE]
> <span data-ttu-id="fe9bd-127">Uygulamanız .NET 4.6 hedefliyorsa bile, bulut hizmeti rolü'nde .NET 4.6.1 yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-127">You should install .NET 4.6.1 on your cloud service role even if your application targets .NET 4.6.</span></span> <span data-ttu-id="fe9bd-128">Bilgi Bankası konuk işletim sistemi içeren [3098779 güncelleştirme](https://support.microsoft.com/kb/3098779) ve [3097997 güncelleştirme](https://support.microsoft.com/kb/3097997).</span><span class="sxs-lookup"><span data-stu-id="fe9bd-128">The Guest OS includes the Knowledge Base [update 3098779](https://support.microsoft.com/kb/3098779) and [update 3097997](https://support.microsoft.com/kb/3097997).</span></span> <span data-ttu-id="fe9bd-129">.NET 4.6 üstünde Bilgi Bankası güncelleştirmeler yüklediyseniz, .NET uygulamalarınızın çalıştırdığınızda sorunlar oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-129">Issues can occur when you run your .NET applications if .NET 4.6 is installed on top of the Knowledge Base updates.</span></span> <span data-ttu-id="fe9bd-130">Bu sorunları önlemek için sürümü 4.6 yerine .NET 4.6.1 yükleyin.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-130">To avoid these issues, install .NET 4.6.1 rather than version 4.6.</span></span> <span data-ttu-id="fe9bd-131">Daha fazla bilgi için bkz: [Bilgi Bankası makalesi 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="fe9bd-131">For more information, see the [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
> 
> 

![Rol içeriğiyle Installer dosyaları][1]

## <a name="define-startup-tasks-for-your-roles"></a><span data-ttu-id="fe9bd-133">Başlangıç görevleri, rolleri tanımlama</span><span class="sxs-lookup"><span data-stu-id="fe9bd-133">Define startup tasks for your roles</span></span>
<span data-ttu-id="fe9bd-134">Başlangıç görevi, bir rol başlamadan önce işlemlerini gerçekleştirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-134">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="fe9bd-135">Başlangıç görevinin bir parçası .NET Framework yükleme herhangi bir uygulama kodu çalıştırmadan önce framework yüklendiğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-135">Installing the .NET Framework as part of the startup task ensures that the framework is installed before any application code is run.</span></span> <span data-ttu-id="fe9bd-136">Başlangıç görevleri hakkında daha fazla bilgi için bkz: [Azure'da başlangıç görevleri çalıştırma](cloud-services-startup-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="fe9bd-136">For more information on startup tasks, see [Run startup tasks in Azure](cloud-services-startup-tasks.md).</span></span> 

1. <span data-ttu-id="fe9bd-137">ServiceDefinition.csdef dosyasında altına aşağıdaki içeriği ekleyin **WebRole** veya **örn** düğüm tüm rolleri için:</span><span class="sxs-lookup"><span data-stu-id="fe9bd-137">Add the following content to the ServiceDefinition.csdef file under the **WebRole** or **WorkerRole** node for all roles:</span></span>
   
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
   
    <span data-ttu-id="fe9bd-138">Önceki yapılandırma Konsolu komutu çalıştırır `install.cmd` .NET Framework'ü yüklemek için yönetici ayrıcalıklarına sahip.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-138">The preceding configuration runs the console command `install.cmd` with administrator privileges to install the .NET Framework.</span></span> <span data-ttu-id="fe9bd-139">Yapılandırma da oluşturur bir **LocalStorage** adlı öğe **NETFXInstall**.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-139">The configuration also creates a **LocalStorage** element named **NETFXInstall**.</span></span> <span data-ttu-id="fe9bd-140">Başlangıç betiği bu yerel depolama kaynağı kullanmak için geçici klasörü ayarlar.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-140">The startup script sets the temp folder to use this local storage resource.</span></span> 
    
    > [!IMPORTANT]
    > <span data-ttu-id="fe9bd-141">Framework'ün doğru yükleme sağlamak için bu kaynak boyutu en az 1024 MB olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-141">To ensure correct installation of the framework, set the size of this resource to at least 1,024 MB.</span></span>
    
    <span data-ttu-id="fe9bd-142">Başlangıç görevleri hakkında daha fazla bilgi için bkz: [ortak Azure Cloud Services başlangıç görevleri](cloud-services-startup-tasks-common.md).</span><span class="sxs-lookup"><span data-stu-id="fe9bd-142">For more information about startup tasks, see [Common Azure Cloud Services startup tasks](cloud-services-startup-tasks-common.md).</span></span>

2. <span data-ttu-id="fe9bd-143">Adlı bir dosya oluşturun **Install.cmd** ve aşağıdaki yükleme betik dosyasına ekleme.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-143">Create a file named **install.cmd** and add the following install script to the file.</span></span>

    <span data-ttu-id="fe9bd-144">Komut dosyası belirtilen .NET Framework sürümünü makinede kayıt sorgulayarak yüklü olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-144">The script checks whether the specified version of the .NET Framework is already installed on the machine by querying the registry.</span></span> <span data-ttu-id="fe9bd-145">.NET sürüm yüklü değilse .NET web yükleyicisi açılmış.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-145">If the .NET version is not installed, then the .NET web installer is opened.</span></span> <span data-ttu-id="fe9bd-146">Sorunları gidermenize yardımcı olması için betik tüm etkinlik depolanan startuptasklog-(geçerli tarih ve saat) .txt dosya oturum **InstallLogs** yerel depolama.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-146">To help troubleshoot any issues, the script logs all activity to the file startuptasklog-(current date and time).txt that is stored in **InstallLogs** local storage.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="fe9bd-147">Install.cmd dosyasını oluşturmak için Windows Not Defteri gibi bir temel metin düzenleyicisi kullanın.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-147">Use a basic text editor like Windows Notepad to create the install.cmd file.</span></span> <span data-ttu-id="fe9bd-148">Bir metin dosyası oluşturun ve uzantı için .cmd değiştirmek için Visual Studio kullanıyorsanız, dosya UTF-8 bayt sırası işareti içeriyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-148">If you use Visual Studio to create a text file and change the extension to .cmd, the file might still contain a UTF-8 byte order mark.</span></span> <span data-ttu-id="fe9bd-149">Komut dosyasının ilk satırını çalıştırdığınızda bu işareti hataya neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-149">This mark can cause an error when the first line of the script is run.</span></span> <span data-ttu-id="fe9bd-150">Bu hatayı önlemek için komut dosyasının ilk satırı bayt sırası işlemesi atlanabilir REM deyimi olun.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-150">To avoid this error, make the first line of the script a REM statement that can be skipped by the byte order processing.</span></span> 
    > 
    >
   
    ```cmd
    REM Set the value of netfx to install appropriate .NET Framework. 
    REM ***** To install .NET 4.5.2 set the variable netfx to "NDP452" *****
    REM ***** To install .NET 4.6 set the variable netfx to "NDP46" *****
    REM ***** To install .NET 4.6.1 set the variable netfx to "NDP461" *****
    REM ***** To install .NET 4.6.2 set the variable netfx to "NDP462" *****
    REM ***** To install .NET 4.7 set the variable netfx to "NDP47" *****
    set netfx="NDP47"

    REM ***** Set script start timestamp *****
    set timehour=%time:~0,2%
    set timestamp=%date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2%
    set "log=install.cmd started %timestamp%."

    REM ***** Exit script if running in Emulator *****
    if %ComputeEmulatorRunning%=="true" goto exit

    REM ***** Needed to correctly install .NET 4.6.1, otherwise you may see an out of disk space error *****
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
    echo Restarting to complete .NET (%netfx%) installation >> %startuptasklog%
    EXIT /B %ERRORLEVEL%

    :installed
    echo .NET (%netfx%) is installed >> %startuptasklog%

    :end
    echo install.cmd completed: %date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2% >> %startuptasklog%

    :exit
    EXIT /B 0
    ```
   
   > [!NOTE]
   > <span data-ttu-id="fe9bd-151">.NET 4.5.2 zaten Azure konuk işletim sisteminde kullanılabilir olsa bile bu betiği .NET 4.5.2 veya sürümü 4.6 sürekliliği için nasıl yükleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-151">This script shows how to install .NET 4.5.2 or version 4.6 for continuity, even though .NET 4.5.2 is already available on the Azure Guest OS.</span></span> <span data-ttu-id="fe9bd-152">Doğrudan sürümü 4.6, yerine .NET 4.6.1 açıklandığı gibi yüklemeniz gerekir [Bilgi Bankası makalesi 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="fe9bd-152">You should directly install .NET 4.6.1 rather than version 4.6, as described in the [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
   > 
   > 

3. <span data-ttu-id="fe9bd-153">Install.cmd dosyasını kullanarak her role eklemek **Ekle** > **varolan öğeyi** içinde **Çözüm Gezgini** bu konunun önceki kısımlarında açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-153">Add the install.cmd file to each role by using **Add** > **Existing Item** in **Solution Explorer** as described earlier in this topic.</span></span> 

    <span data-ttu-id="fe9bd-154">Bu adım tamamlandıktan sonra tüm rolleri Install.cmd dosyasını ve .NET yükleyici dosyası olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-154">After this step is complete, all roles should have the .NET installer file and the install.cmd file.</span></span>

   ![Rol içeriğe sahip tüm dosyalar][2]

## <a name="configure-diagnostics-to-transfer-startup-logs-to-blob-storage"></a><span data-ttu-id="fe9bd-156">Blob depolama alanına başlangıç günlükleri aktarmak için tanılama Yapılandır</span><span class="sxs-lookup"><span data-stu-id="fe9bd-156">Configure Diagnostics to transfer startup logs to Blob storage</span></span>
<span data-ttu-id="fe9bd-157">Yükleme sorunlarını giderme basitleştirmek için başlangıç betiği veya Azure Blob depolama alanına .NET yükleyici tarafından oluşturulan tüm günlük dosyaları aktarmak için Azure tanılama yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-157">To simplify troubleshooting installation issues, you can configure Azure Diagnostics to transfer any log files generated by the startup script or the .NET installer to Azure Blob storage.</span></span> <span data-ttu-id="fe9bd-158">Bu yaklaşımı kullanarak, rol içine, Uzak Masaüstü'nü gerek kalmadan yerine Blob depolama alanından günlük dosyaları indirme günlükleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-158">By using this approach, you can view the logs by downloading the log files from Blob storage rather than having to remote desktop into the role.</span></span>

<span data-ttu-id="fe9bd-159">Tanılama yapılandırmak için diagnostics.wadcfgx dosyasını açın ve aşağıdaki içeriği altında eklemek **dizinleri** düğümü:</span><span class="sxs-lookup"><span data-stu-id="fe9bd-159">To configure Diagnostics, open the diagnostics.wadcfgx file and add the following content under the **Directories** node:</span></span> 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

<span data-ttu-id="fe9bd-160">Tanılama günlük dizininde dosya aktarmak için bu XML yapılandırır **NETFXInstall** kaynak tanılama depolama hesabı **netfx yükleme** blob kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-160">This XML configures Diagnostics to transfer the files in the log directory in the **NETFXInstall** resource to the Diagnostics storage account in the **netfx-install** blob container.</span></span>

## <a name="deploy-your-cloud-service"></a><span data-ttu-id="fe9bd-161">Bulut hizmetinize dağıtın</span><span class="sxs-lookup"><span data-stu-id="fe9bd-161">Deploy your cloud service</span></span>
<span data-ttu-id="fe9bd-162">Bulut hizmetinizi dağıttığınızda, başlangıç görevleri henüz yüklü değilse .NET Framework yükleyin.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-162">When you deploy your cloud service, the startup tasks install the .NET Framework if it's not already installed.</span></span> <span data-ttu-id="fe9bd-163">Bulut hizmeti rollerinizi bulunan *meşgul* framework yüklenirken durum.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-163">Your cloud service roles are in the *busy* state while the framework is being installed.</span></span> <span data-ttu-id="fe9bd-164">Framework yüklemesi bir yeniden başlatma gerektirirse, hizmet rolleri de yeniden başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="fe9bd-164">If the framework installation requires a restart, the service roles might also restart.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fe9bd-165">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="fe9bd-165">Additional resources</span></span>
* <span data-ttu-id="fe9bd-166">[.NET Framework yükleme][Installing the .NET Framework]</span><span class="sxs-lookup"><span data-stu-id="fe9bd-166">[Installing the .NET Framework][Installing the .NET Framework]</span></span>
* <span data-ttu-id="fe9bd-167">[Hangi .NET Framework sürümlerinin yüklü olduğunu belirleme][How to: Determine Which .NET Framework Versions Are Installed]</span><span class="sxs-lookup"><span data-stu-id="fe9bd-167">[Determine which .NET Framework versions are installed][How to: Determine Which .NET Framework Versions Are Installed]</span></span>
* <span data-ttu-id="fe9bd-168">[.NET Framework yükleme sorunlarını giderme][Troubleshooting .NET Framework Installations]</span><span class="sxs-lookup"><span data-stu-id="fe9bd-168">[Troubleshooting .NET Framework installations][Troubleshooting .NET Framework Installations]</span></span>

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing the .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
