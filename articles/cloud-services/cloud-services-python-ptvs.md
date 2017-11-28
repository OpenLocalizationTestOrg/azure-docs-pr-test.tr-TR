---
title: "aaaGet başlatılan Python ve Azure Cloud Services | Microsoft Docs"
description: "Visual Studio toocreate Azure bulut hizmetlerine web rolleri ve çalışan rolleri dahil olmak üzere için Python araçları kullanarak genel bakış."
services: cloud-services
documentationcenter: python
author: thraka
manager: timlt
editor: 
ms.assetid: 5489405d-6fa9-4b11-a161-609103cbdc18
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: f5fd85e754839f146abe912351c59dc4a148c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a><span data-ttu-id="e1fca-103">Visual Studio için Python web ve çalışan rolleri içeren Python Araçları</span><span class="sxs-lookup"><span data-stu-id="e1fca-103">Python web and worker roles with Python Tools for Visual Studio</span></span>

<span data-ttu-id="e1fca-104">Bu makalede, [Visual Studio için Python Araçları][Python Tools for Visual Studio] ile Python web ve çalışan rollerini kullanmaya genel bir bakış sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="e1fca-104">This article provides an overview of using Python web and worker roles using [Python Tools for Visual Studio][Python Tools for Visual Studio].</span></span> <span data-ttu-id="e1fca-105">Bilgi nasıl toouse Visual Studio toocreate ve Python kullanan temel bir bulut hizmeti dağıtın.</span><span class="sxs-lookup"><span data-stu-id="e1fca-105">Learn how toouse Visual Studio toocreate and deploy a basic Cloud Service that uses Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1fca-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e1fca-106">Prerequisites</span></span>
* [<span data-ttu-id="e1fca-107">Visual Studio 2013, 2015 veya 2017</span><span class="sxs-lookup"><span data-stu-id="e1fca-107">Visual Studio 2013, 2015, or 2017</span></span>](https://www.visualstudio.com/)
* <span data-ttu-id="e1fca-108">[Visual Studio için Python Araçları][Python Tools for Visual Studio] (PTVS)</span><span class="sxs-lookup"><span data-stu-id="e1fca-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span></span>
* <span data-ttu-id="e1fca-109">[VS 2013 için Azure SDK Araçları][Azure SDK Tools for VS 2013] veya</span><span class="sxs-lookup"><span data-stu-id="e1fca-109">[Azure SDK Tools for VS 2013][Azure SDK Tools for VS 2013] or</span></span>  
<span data-ttu-id="e1fca-110">[VS 2015 için Azure SDK Araçları][Azure SDK Tools for VS 2015] veya</span><span class="sxs-lookup"><span data-stu-id="e1fca-110">[Azure SDK Tools for VS 2015][Azure SDK Tools for VS 2015] or</span></span>  
<span data-ttu-id="e1fca-111">[VS 2017 için Azure SDK Araçları][Azure SDK Tools for VS 2017]</span><span class="sxs-lookup"><span data-stu-id="e1fca-111">[Azure SDK Tools for VS 2017][Azure SDK Tools for VS 2017]</span></span>
* <span data-ttu-id="e1fca-112">[Python 2.7 32-bit][Python 2.7 32-bit] veya [Python 3.5 32-bit][Python 3.5 32-bit]</span><span class="sxs-lookup"><span data-stu-id="e1fca-112">[Python 2.7 32-bit][Python 2.7 32-bit] or [Python 3.5 32-bit][Python 3.5 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a><span data-ttu-id="e1fca-113">Python web ve çalışan rolleri nelerdir?</span><span class="sxs-lookup"><span data-stu-id="e1fca-113">What are Python web and worker roles?</span></span>
<span data-ttu-id="e1fca-114">Azure, uygulama çalıştırmak için üç işlem modeli sağlar: [Azure App Service’teki Web Apps özelliği][execution model-web sites], [Azure Sanal Makineler][execution model-vms] ve [Azure Cloud Services][execution model-cloud services].</span><span class="sxs-lookup"><span data-stu-id="e1fca-114">Azure provides three compute models for running applications: [Web Apps feature in Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms], and [Azure Cloud Services][execution model-cloud services].</span></span> <span data-ttu-id="e1fca-115">Python bu üç modeli de destekler.</span><span class="sxs-lookup"><span data-stu-id="e1fca-115">All three models support Python.</span></span> <span data-ttu-id="e1fca-116">Web ve çalışan rolleri içeren Cloud Services *Hizmet Olarak Platform (PaaS)* sunar.</span><span class="sxs-lookup"><span data-stu-id="e1fca-116">Cloud Services, which include web and worker roles, provide *Platform as a Service (PaaS)*.</span></span> <span data-ttu-id="e1fca-117">Çalışan rolü kullanıcı etkileşimi ve girişinden bağımsız zaman uyumsuz, uzun süre çalışan veya kalıcı görevleri çalıştırabilir sırada bir bulut hizmetinde bir web rolü adanmış bir Internet Information Services (IIS) web sunucusu toohost ön uç web uygulamaları, sağlar.</span><span class="sxs-lookup"><span data-stu-id="e1fca-117">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server toohost front end web applications, while a worker role can run asynchronous, long-running, or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="e1fca-118">Daha fazla bilgi için bkz. [Bulut Hizmeti nedir?].</span><span class="sxs-lookup"><span data-stu-id="e1fca-118">For more information, see [What is a Cloud Service?].</span></span>

> [!NOTE]
> <span data-ttu-id="e1fca-119">*Toobuild basit bir Web sitesi mi arıyorsunuz?*</span><span class="sxs-lookup"><span data-stu-id="e1fca-119">*Looking toobuild a simple website?*</span></span>
> <span data-ttu-id="e1fca-120">Senaryonuz yalnızca basit Web sitesi ön uç içeriyorsa, Azure App Service'te hello basit Web Apps özelliğini kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="e1fca-120">If your scenario involves just a simple website front end, consider using hello lightweight Web Apps feature in Azure App Service.</span></span> <span data-ttu-id="e1fca-121">Web siteniz büyüdükçe ve gereksinimleriniz değiştikçe kolayca bulut hizmeti tooa yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1fca-121">You can easily upgrade tooa Cloud Service as your website grows and your requirements change.</span></span> <span data-ttu-id="e1fca-122">Merhaba bkz <a href="/develop/python/">Python Geliştirici Merkezi</a> hello Azure App Service'te Web Apps özelliğini geliştirme kapak makaleler için.</span><span class="sxs-lookup"><span data-stu-id="e1fca-122">See hello <a href="/develop/python/">Python Developer Center</a> for articles that cover development of hello Web Apps feature in Azure App Service.</span></span>
> <br />
> 
> 

## <a name="project-creation"></a><span data-ttu-id="e1fca-123">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1fca-123">Project creation</span></span>
<span data-ttu-id="e1fca-124">Visual Studio'da seçebileceğiniz **Azure bulut hizmeti** hello içinde **yeni proje** iletişim kutusunda **Python**.</span><span class="sxs-lookup"><span data-stu-id="e1fca-124">In Visual Studio, you can select **Azure Cloud Service** in hello **New Project** dialog box, under **Python**.</span></span>

![Yeni Proje İletişim Kutusu](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

<span data-ttu-id="e1fca-126">Hello Azure bulut hizmeti sihirbazında, yeni web ve çalışan rolleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1fca-126">In hello Azure Cloud Service wizard, you can create new web and worker roles.</span></span>

![Azure Bulut Hizmeti İletişim Kutusu](./media/cloud-services-python-ptvs/new-service-wizard.png)

<span data-ttu-id="e1fca-128">Merhaba çalışan rolü şablonu Demirbaş kod tooconnect tooan Azure depolama hesabı veya Azure Service Bus ile gelir.</span><span class="sxs-lookup"><span data-stu-id="e1fca-128">hello worker role template comes with boilerplate code tooconnect tooan Azure storage account or Azure Service Bus.</span></span>

![Bulut Hizmeti Çözümü](./media/cloud-services-python-ptvs/worker.png)

<span data-ttu-id="e1fca-130">Web veya çalışan rolleri tooan olan bir bulut hizmetini herhangi bir zamanda ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1fca-130">You can add web or worker roles tooan existing cloud service at any time.</span></span>  <span data-ttu-id="e1fca-131">Çözümünüzde tooadd mevcut projeleri seçin veya yenilerini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e1fca-131">You can choose tooadd existing projects in your solution, or create new ones.</span></span>

![Rol Komutu Ekleme](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

<span data-ttu-id="e1fca-133">Bulut hizmetiniz farklı dillerde uygulanan roller içerebilir.</span><span class="sxs-lookup"><span data-stu-id="e1fca-133">Your cloud service can contain roles implemented in different languages.</span></span>  <span data-ttu-id="e1fca-134">Örneğin, Python veya C# çalışan rolleri ile Django kullanılarak uygulanan bir Python web rolünüz olabilir.</span><span class="sxs-lookup"><span data-stu-id="e1fca-134">For example, you can have a Python web role implemented using Django, with Python, or with C# worker roles.</span></span>  <span data-ttu-id="e1fca-135">Service Bus kuyruklarını veya depolama kuyruklarını kullanarak rolleriniz arasında kolaya iletişim kurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1fca-135">You can easily communicate between your roles using Service Bus queues or storage queues.</span></span>

## <a name="install-python-on-hello-cloud-service"></a><span data-ttu-id="e1fca-136">Python hello bulut hizmetini yükleme</span><span class="sxs-lookup"><span data-stu-id="e1fca-136">Install Python on hello cloud service</span></span>
> [!WARNING]
> <span data-ttu-id="e1fca-137">Visual Studio ile (Merhaba zaman bu makalenin en son güncelleştirildiği) yüklü olan hello Kurulum komut çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="e1fca-137">hello setup scripts that are installed with Visual Studio (at hello time this article was last updated) do not work.</span></span> <span data-ttu-id="e1fca-138">Bu bölümde geçici bir çözüm açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e1fca-138">This section describes a workaround.</span></span>
> 
> 

<span data-ttu-id="e1fca-139">Merhaba ana hello Kurulum kodlarıyla python yüklemeyin sorunudur.</span><span class="sxs-lookup"><span data-stu-id="e1fca-139">hello main problem with hello setup scripts is that they do not install python.</span></span> <span data-ttu-id="e1fca-140">İlk olarak, iki tanımlamak [başlangıç görevleri](cloud-services-startup-tasks.md) hello içinde [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) dosya.</span><span class="sxs-lookup"><span data-stu-id="e1fca-140">First, define two [startup tasks](cloud-services-startup-tasks.md) in hello [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) file.</span></span> <span data-ttu-id="e1fca-141">Merhaba ilk görevi (**PrepPython.ps1**) indirir ve hello Python çalışma zamanı yükler.</span><span class="sxs-lookup"><span data-stu-id="e1fca-141">hello first task (**PrepPython.ps1**) downloads and installs hello Python runtime.</span></span> <span data-ttu-id="e1fca-142">Merhaba ikinci görev (**PipInstaller.ps1**) olabilecek bağımlılıkları PIP tooinstall çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="e1fca-142">hello second task (**PipInstaller.ps1**) runs pip tooinstall any dependencies you may have.</span></span>

<span data-ttu-id="e1fca-143">komut dosyaları aşağıdaki hello Python 3.5 hedefleme yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="e1fca-143">hello following scripts were written targeting Python 3.5.</span></span> <span data-ttu-id="e1fca-144">Toouse hello sürüm istiyorsanız, python, kümesi hello 2.x **PYTHON2** değişkeni dosya çok**üzerinde** hello iki başlangıç görevi ve hello çalışma zamanı görev için: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span><span class="sxs-lookup"><span data-stu-id="e1fca-144">If you want toouse hello version 2.x of python, set hello **PYTHON2** variable file too**on** for hello two startup tasks and hello runtime task: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span></span>

```xml
<Startup>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>
  </Task>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>

  </Task>

</Startup>
```

<span data-ttu-id="e1fca-145">Merhaba **PYTHON2** ve **PYPATH** toohello çalışan başlangıç görevi değişkenleri eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="e1fca-145">hello **PYTHON2** and **PYPATH** variables must be added toohello worker startup task.</span></span> <span data-ttu-id="e1fca-146">Merhaba **PYPATH** değişkeni Merhaba, yalnızca kullanılan **PYTHON2** değişkenini çok ayarlamak**üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="e1fca-146">hello **PYPATH** variable is only used if hello **PYTHON2** variable is set too**on**.</span></span>

```xml
<Runtime>
  <Environment>
    <Variable name="EMULATED">
      <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
    </Variable>
    <Variable name="PYTHON2" value="off" />
    <Variable name="PYPATH" value="%SystemDrive%\Python27" />
  </Environment>
  <EntryPoint>
    <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
  </EntryPoint>
</Runtime>
```

#### <a name="sample-servicedefinitioncsdef"></a><span data-ttu-id="e1fca-147">Örnek ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="e1fca-147">Sample ServiceDefinition.csdef</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="AzureCloudServicePython" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
      <Setting name="Python2" />
    </ConfigurationSettings>
    <Startup>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="EMULATED">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
        </Variable>
        <Variable name="PYTHON2" value="off" />
        <Variable name="PYPATH" value="%SystemDrive%\Python27" />
      </Environment>
      <EntryPoint>
        <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
      </EntryPoint>
    </Runtime>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
  </WorkerRole>
</ServiceDefinition>
```



<span data-ttu-id="e1fca-148">Ardından, hello oluşturun **PrepPython.ps1** ve **PipInstaller.ps1** hello dosyalarında **. / bin** rolünüze klasörü.</span><span class="sxs-lookup"><span data-stu-id="e1fca-148">Next, create hello **PrepPython.ps1** and **PipInstaller.ps1** files in hello **./bin** folder of your role.</span></span>

#### <a name="preppythonps1"></a><span data-ttu-id="e1fca-149">PrepPython.ps1</span><span class="sxs-lookup"><span data-stu-id="e1fca-149">PrepPython.ps1</span></span>
<span data-ttu-id="e1fca-150">Bu betik python yükler.</span><span class="sxs-lookup"><span data-stu-id="e1fca-150">This script installs python.</span></span> <span data-ttu-id="e1fca-151">Merhaba, **PYTHON2** ortam değişkenini çok ayarlamak**üzerinde**, Python 2.7 yüklendikten sonra Aksi takdirde Python 3.5 yüklenir.</span><span class="sxs-lookup"><span data-stu-id="e1fca-151">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is installed, otherwise Python 3.5 is installed.</span></span>

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if python is installed...$nl"
    if ($is_python2) {
        & "${env:SystemDrive}\Python27\python.exe"  -V | Out-Null
    }
    else {
        py -V | Out-Null
    }

    if (-not $?) {

        $url = "https://www.python.org/ftp/python/3.5.2/python-3.5.2-amd64.exe"
        $outFile = "${env:TEMP}\python-3.5.2-amd64.exe"

        if ($is_python2) {
            $url = "https://www.python.org/ftp/python/2.7.12/python-2.7.12.amd64.msi"
            $outFile = "${env:TEMP}\python-2.7.12.amd64.msi"
        }

        Write-Output "Not found, downloading $url too$outFile$nl"
        Invoke-WebRequest $url -OutFile $outFile
        Write-Output "Installing$nl"

        if ($is_python2) {
            Start-Process msiexec.exe -ArgumentList "/q", "/i", "$outFile", "ALLUSERS=1" -Wait
        }
        else {
            Start-Process "$outFile" -ArgumentList "/quiet", "InstallAllUsers=1" -Wait
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Already installed"
    }
}
```

#### <a name="pipinstallerps1"></a><span data-ttu-id="e1fca-152">PipInstaller.ps1</span><span class="sxs-lookup"><span data-stu-id="e1fca-152">PipInstaller.ps1</span></span>
<span data-ttu-id="e1fca-153">Bu komut dosyası PIP çağırır ve tüm hello bağımlılıklarını hello yükler **requirements.txt** dosya.</span><span class="sxs-lookup"><span data-stu-id="e1fca-153">This script calls up pip and installs all of hello dependencies in hello **requirements.txt** file.</span></span> <span data-ttu-id="e1fca-154">Merhaba, **PYTHON2** ortam değişkenini çok ayarlamak**üzerinde**, Python 2.7 kullanılırsa, aksi halde Python 3.5 kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e1fca-154">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if requirements.txt exists$nl"
    if (Test-Path ..\requirements.txt) {
        Write-Output "Found. Processing pip$nl"

        if ($is_python2) {
            & "${env:SystemDrive}\Python27\python.exe" -m pip install -r ..\requirements.txt
        }
        else {
            py -m pip install -r ..\requirements.txt
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Not found$nl"
    }
}
```

#### <a name="modify-launchworkerps1"></a><span data-ttu-id="e1fca-155">LaunchWorker.ps1’i değiştirme</span><span class="sxs-lookup"><span data-stu-id="e1fca-155">Modify LaunchWorker.ps1</span></span>
> [!NOTE]
> <span data-ttu-id="e1fca-156">Merhaba durumda bir **çalışan rolü** projesi **LauncherWorker.ps1** gerekli tooexecute hello başlatma dosyasını bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="e1fca-156">In hello case of a **worker role** project, **LauncherWorker.ps1** file is required tooexecute hello startup file.</span></span> <span data-ttu-id="e1fca-157">İçinde bir **web rolü** projesi, hello başlangıç dosyasına bunun yerine hello Proje Özellikleri'nde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="e1fca-157">In a **web role** project, hello startup file is instead defined in hello project properties.</span></span>
> 
> 

<span data-ttu-id="e1fca-158">Merhaba **bin\LaunchWorker.ps1** hazırlık iş ancak birçok gerçekten işe yaramazsa toodo ilk olarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="e1fca-158">hello **bin\LaunchWorker.ps1** was originally created toodo a lot of prep work but it doesn't really work.</span></span> <span data-ttu-id="e1fca-159">Bu dosyayı Merhaba içeriğine komut dosyası izleyen hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e1fca-159">Replace hello contents in that file with hello following script.</span></span>

<span data-ttu-id="e1fca-160">Bu komut dosyasını hello çağıran **worker.py** python projenizden dosya.</span><span class="sxs-lookup"><span data-stu-id="e1fca-160">This script calls hello **worker.py** file from your python project.</span></span> <span data-ttu-id="e1fca-161">Merhaba, **PYTHON2** ortam değişkenini çok ayarlamak**üzerinde**, Python 2.7 kullanılırsa, aksi halde Python 3.5 kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e1fca-161">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated)
{
    Write-Output "Running worker.py$nl"

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
else
{
    Write-Output "Running (EMULATED) worker.py$nl"

    # Customize tooyour local dev environment

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
```

#### <a name="pscmd"></a><span data-ttu-id="e1fca-162">ps.cmd</span><span class="sxs-lookup"><span data-stu-id="e1fca-162">ps.cmd</span></span>
<span data-ttu-id="e1fca-163">Merhaba Visual Studio şablonları oluşturmuş bir **ps.cmd** hello dosyasında **. / bin** klasör.</span><span class="sxs-lookup"><span data-stu-id="e1fca-163">hello Visual Studio templates should have created a **ps.cmd** file in hello **./bin** folder.</span></span> <span data-ttu-id="e1fca-164">Bu kabuk betiği hello PowerShell sarmalayıcı betikleri yukarıdaki çağırır ve adlı hello PowerShell sarmalayıcı hello adını temel alarak günlük kaydını sağlar.</span><span class="sxs-lookup"><span data-stu-id="e1fca-164">This shell script calls out hello PowerShell wrapper scripts above and provides logging based on hello name of hello PowerShell wrapper called.</span></span> <span data-ttu-id="e1fca-165">Bu dosya oluşturulmadıysa içinde olması gerekenler aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e1fca-165">If this file wasn't created, here is what should be in it.</span></span> 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a><span data-ttu-id="e1fca-166">Yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e1fca-166">Run locally</span></span>
<span data-ttu-id="e1fca-167">Bulut hizmeti projenizi başlangıç başlangıç projesi olarak ayarla ve F5 tuşuna basarsanız, hello bulut hizmeti hello yerel Azure öykünücüsünde çalışır.</span><span class="sxs-lookup"><span data-stu-id="e1fca-167">If you set your cloud service project as hello startup project and press F5, hello cloud service runs in hello local Azure emulator.</span></span>

<span data-ttu-id="e1fca-168">PTVS destekler; ancak başlatma hata ayıklama hello öykünücüsünde (örneğin, kesme noktaları) çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="e1fca-168">Although PTVS supports launching in hello emulator, debugging (for example, breakpoints) does not work.</span></span>

<span data-ttu-id="e1fca-169">toodebug, web ve çalışan rolleri hello rolü projesi hello başlangıç projesi olarak ayarlayın ve yerine hata ayıklama.</span><span class="sxs-lookup"><span data-stu-id="e1fca-169">toodebug your web and worker roles, you can set hello role project as hello startup project and debug that instead.</span></span>  <span data-ttu-id="e1fca-170">Ayrıca, birden fazla başlangıç projesi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1fca-170">You can also set multiple startup projects.</span></span>  <span data-ttu-id="e1fca-171">Merhaba çözüme sağ tıklayın ve ardından **başlangıç projelerini Ayarla**.</span><span class="sxs-lookup"><span data-stu-id="e1fca-171">Right-click hello solution and then select **Set StartUp Projects**.</span></span>

![Çözüm Başlangıç Projesi Özellikleri](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-tooazure"></a><span data-ttu-id="e1fca-173">TooAzure yayımlama</span><span class="sxs-lookup"><span data-stu-id="e1fca-173">Publish tooAzure</span></span>
<span data-ttu-id="e1fca-174">toopublish, hello çözümde hello bulut hizmeti projesine sağ tıklayın ve ardından **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="e1fca-174">toopublish, right-click hello cloud service project in hello solution and then select **Publish**.</span></span>

![Microsoft Azure Yayımlama Oturumu Açma](./media/cloud-services-python-ptvs/publish-sign-in.png)

<span data-ttu-id="e1fca-176">Merhaba Sihirbazı izleyin.</span><span class="sxs-lookup"><span data-stu-id="e1fca-176">Follow hello wizard.</span></span> <span data-ttu-id="e1fca-177">Gerekirse uzak masaüstünü etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e1fca-177">If you need to, enable remote desktop.</span></span> <span data-ttu-id="e1fca-178">Uzak Masaüstü toodebug bir şey gerektiğinde faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="e1fca-178">Remote desktop is helpful when you need toodebug something.</span></span>

<span data-ttu-id="e1fca-179">Yapılandırma ayarları bittiğinde **Yayımla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1fca-179">When you are done configuring settings, click **Publish**.</span></span>

<span data-ttu-id="e1fca-180">Merhaba çıktı penceresinde devam eden bazı işlemler görünür, ardından hello Microsoft Azure Etkinlik Günlüğü penceresini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="e1fca-180">Some progress appears in hello output window, then you'll see hello Microsoft Azure Activity Log window.</span></span>

![Microsoft Azure Etkinlik Günlüğü Penceresi](./media/cloud-services-python-ptvs/publish-activity-log.png)

<span data-ttu-id="e1fca-182">Birkaç dakika toocomplete, ardından web dağıtım alır ve/veya çalışan rolleri Azure üzerinde çalışan!</span><span class="sxs-lookup"><span data-stu-id="e1fca-182">Deployment takes several minutes toocomplete, then your web and/or worker roles run on Azure!</span></span>

### <a name="investigate-logs"></a><span data-ttu-id="e1fca-183">Günlükleri araştırma</span><span class="sxs-lookup"><span data-stu-id="e1fca-183">Investigate logs</span></span>
<span data-ttu-id="e1fca-184">Merhaba bulut hizmeti sanal makine başlatıldığında ve Python yüklendikten sonra hata iletileri hello günlükleri toofind bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1fca-184">After hello cloud service virtual machine starts up and installs Python, you can look at hello logs toofind any failure messages.</span></span> <span data-ttu-id="e1fca-185">Bu günlükler hello bulunan **C:\Resources\Directory\\{rolü} \LogFiles** klasör.</span><span class="sxs-lookup"><span data-stu-id="e1fca-185">These logs are located in hello **C:\Resources\Directory\\{role}\LogFiles** folder.</span></span> <span data-ttu-id="e1fca-186">**PrepPython.err.txt** Python yüklediyseniz hello betik toodetect bulunduğunda gelen en az bir hata var ve **PipInstaller.err.txt** PIP eski bir sürümü hakkında şikayetçi.</span><span class="sxs-lookup"><span data-stu-id="e1fca-186">**PrepPython.err.txt** has at least one error in it from when hello script tries toodetect if Python is installed and **PipInstaller.err.txt** may complain about an outdated version of pip.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1fca-187">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e1fca-187">Next steps</span></span>
<span data-ttu-id="e1fca-188">Visual Studio için Python Araçları'ndaki web ve çalışan rolleri ile çalışma hakkında daha ayrıntılı bilgi için hello PTVS belgelerine bakın:</span><span class="sxs-lookup"><span data-stu-id="e1fca-188">For more detailed information about working with web and worker roles in Python Tools for Visual Studio, see hello PTVS documentation:</span></span>

* <span data-ttu-id="e1fca-189">[Bulut Hizmeti Projeleri][Cloud Service Projects]</span><span class="sxs-lookup"><span data-stu-id="e1fca-189">[Cloud Service Projects][Cloud Service Projects]</span></span>

<span data-ttu-id="e1fca-190">Azure Storage veya Service Bus kullanarak gibi web ve çalışan rolleri, Azure hizmetlerini kullanma hakkında daha fazla ayrıntı için aşağıdaki makaleleri hello bakın:</span><span class="sxs-lookup"><span data-stu-id="e1fca-190">For more details about using Azure services from your web and worker roles, such as using Azure Storage or Service Bus, see hello following articles:</span></span>

* <span data-ttu-id="e1fca-191">[Blob Hizmeti][Blob Service]</span><span class="sxs-lookup"><span data-stu-id="e1fca-191">[Blob Service][Blob Service]</span></span>
* <span data-ttu-id="e1fca-192">[Tablo Hizmeti][Table Service]</span><span class="sxs-lookup"><span data-stu-id="e1fca-192">[Table Service][Table Service]</span></span>
* <span data-ttu-id="e1fca-193">[Kuyruk Hizmeti][Queue Service]</span><span class="sxs-lookup"><span data-stu-id="e1fca-193">[Queue Service][Queue Service]</span></span>
* <span data-ttu-id="e1fca-194">[Service Bus Kuyrukları][Service Bus Queues]</span><span class="sxs-lookup"><span data-stu-id="e1fca-194">[Service Bus Queues][Service Bus Queues]</span></span>
* <span data-ttu-id="e1fca-195">[Service Bus Konuları][Service Bus Topics]</span><span class="sxs-lookup"><span data-stu-id="e1fca-195">[Service Bus Topics][Service Bus Topics]</span></span>

<!--Link references-->

[Bulut Hizmeti nedir?]: cloud-services-choose-me.md
[execution model-web sites]: ../app-service-web/app-service-web-overview.md
[execution model-vms]:../virtual-machines/windows/overview.md
[execution model-cloud services]: cloud-services-choose-me.md
[Python Developer Center]: /develop/python/

[Blob Service]:../storage/blobs/storage-python-how-to-use-blob-storage.md
[Queue Service]: ../storage/queues/storage-python-how-to-use-queue-storage.md
[Table Service]:../cosmos-db/table-storage-how-to-use-python.md
[Service Bus Queues]: ../service-bus-messaging/service-bus-python-how-to-use-queues.md
[Service Bus Topics]: ../service-bus-messaging/service-bus-python-how-to-use-topics-subscriptions.md


<!--External Link references-->

[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs
[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure SDK Tools for VS 2013]: http://go.microsoft.com/fwlink/?LinkId=746482
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=746481
[Azure SDK Tools for VS 2017]: http://go.microsoft.com/fwlink/?LinkId=746483
[Python 2.7 32-bit]: https://www.python.org/downloads/
[Python 3.5 32-bit]: https://www.python.org/downloads/
