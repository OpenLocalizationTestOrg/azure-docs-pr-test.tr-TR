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
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a>Visual Studio için Python web ve çalışan rolleri içeren Python Araçları

Bu makalede, [Visual Studio için Python Araçları][Python Tools for Visual Studio] ile Python web ve çalışan rollerini kullanmaya genel bir bakış sunulmuştur. Bilgi nasıl toouse Visual Studio toocreate ve Python kullanan temel bir bulut hizmeti dağıtın.

## <a name="prerequisites"></a>Ön koşullar
* [Visual Studio 2013, 2015 veya 2017](https://www.visualstudio.com/)
* [Visual Studio için Python Araçları][Python Tools for Visual Studio] (PTVS)
* [VS 2013 için Azure SDK Araçları][Azure SDK Tools for VS 2013] veya  
[VS 2015 için Azure SDK Araçları][Azure SDK Tools for VS 2015] veya  
[VS 2017 için Azure SDK Araçları][Azure SDK Tools for VS 2017]
* [Python 2.7 32-bit][Python 2.7 32-bit] veya [Python 3.5 32-bit][Python 3.5 32-bit]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a>Python web ve çalışan rolleri nelerdir?
Azure, uygulama çalıştırmak için üç işlem modeli sağlar: [Azure App Service’teki Web Apps özelliği][execution model-web sites], [Azure Sanal Makineler][execution model-vms] ve [Azure Cloud Services][execution model-cloud services]. Python bu üç modeli de destekler. Web ve çalışan rolleri içeren Cloud Services *Hizmet Olarak Platform (PaaS)* sunar. Çalışan rolü kullanıcı etkileşimi ve girişinden bağımsız zaman uyumsuz, uzun süre çalışan veya kalıcı görevleri çalıştırabilir sırada bir bulut hizmetinde bir web rolü adanmış bir Internet Information Services (IIS) web sunucusu toohost ön uç web uygulamaları, sağlar.

Daha fazla bilgi için bkz. [Bulut Hizmeti nedir?].

> [!NOTE]
> *Toobuild basit bir Web sitesi mi arıyorsunuz?*
> Senaryonuz yalnızca basit Web sitesi ön uç içeriyorsa, Azure App Service'te hello basit Web Apps özelliğini kullanmayı düşünün. Web siteniz büyüdükçe ve gereksinimleriniz değiştikçe kolayca bulut hizmeti tooa yükseltebilirsiniz. Merhaba bkz <a href="/develop/python/">Python Geliştirici Merkezi</a> hello Azure App Service'te Web Apps özelliğini geliştirme kapak makaleler için.
> <br />
> 
> 

## <a name="project-creation"></a>Proje oluşturma
Visual Studio'da seçebileceğiniz **Azure bulut hizmeti** hello içinde **yeni proje** iletişim kutusunda **Python**.

![Yeni Proje İletişim Kutusu](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

Hello Azure bulut hizmeti sihirbazında, yeni web ve çalışan rolleri oluşturabilirsiniz.

![Azure Bulut Hizmeti İletişim Kutusu](./media/cloud-services-python-ptvs/new-service-wizard.png)

Merhaba çalışan rolü şablonu Demirbaş kod tooconnect tooan Azure depolama hesabı veya Azure Service Bus ile gelir.

![Bulut Hizmeti Çözümü](./media/cloud-services-python-ptvs/worker.png)

Web veya çalışan rolleri tooan olan bir bulut hizmetini herhangi bir zamanda ekleyebilirsiniz.  Çözümünüzde tooadd mevcut projeleri seçin veya yenilerini oluşturun.

![Rol Komutu Ekleme](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

Bulut hizmetiniz farklı dillerde uygulanan roller içerebilir.  Örneğin, Python veya C# çalışan rolleri ile Django kullanılarak uygulanan bir Python web rolünüz olabilir.  Service Bus kuyruklarını veya depolama kuyruklarını kullanarak rolleriniz arasında kolaya iletişim kurabilirsiniz.

## <a name="install-python-on-hello-cloud-service"></a>Python hello bulut hizmetini yükleme
> [!WARNING]
> Visual Studio ile (Merhaba zaman bu makalenin en son güncelleştirildiği) yüklü olan hello Kurulum komut çalışmaz. Bu bölümde geçici bir çözüm açıklanmaktadır.
> 
> 

Merhaba ana hello Kurulum kodlarıyla python yüklemeyin sorunudur. İlk olarak, iki tanımlamak [başlangıç görevleri](cloud-services-startup-tasks.md) hello içinde [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) dosya. Merhaba ilk görevi (**PrepPython.ps1**) indirir ve hello Python çalışma zamanı yükler. Merhaba ikinci görev (**PipInstaller.ps1**) olabilecek bağımlılıkları PIP tooinstall çalıştırır.

komut dosyaları aşağıdaki hello Python 3.5 hedefleme yazılmıştır. Toouse hello sürüm istiyorsanız, python, kümesi hello 2.x **PYTHON2** değişkeni dosya çok**üzerinde** hello iki başlangıç görevi ve hello çalışma zamanı görev için: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.

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

Merhaba **PYTHON2** ve **PYPATH** toohello çalışan başlangıç görevi değişkenleri eklenmiştir. Merhaba **PYPATH** değişkeni Merhaba, yalnızca kullanılan **PYTHON2** değişkenini çok ayarlamak**üzerinde**.

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

#### <a name="sample-servicedefinitioncsdef"></a>Örnek ServiceDefinition.csdef
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



Ardından, hello oluşturun **PrepPython.ps1** ve **PipInstaller.ps1** hello dosyalarında **. / bin** rolünüze klasörü.

#### <a name="preppythonps1"></a>PrepPython.ps1
Bu betik python yükler. Merhaba, **PYTHON2** ortam değişkenini çok ayarlamak**üzerinde**, Python 2.7 yüklendikten sonra Aksi takdirde Python 3.5 yüklenir.

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

#### <a name="pipinstallerps1"></a>PipInstaller.ps1
Bu komut dosyası PIP çağırır ve tüm hello bağımlılıklarını hello yükler **requirements.txt** dosya. Merhaba, **PYTHON2** ortam değişkenini çok ayarlamak**üzerinde**, Python 2.7 kullanılırsa, aksi halde Python 3.5 kullanılır.

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

#### <a name="modify-launchworkerps1"></a>LaunchWorker.ps1’i değiştirme
> [!NOTE]
> Merhaba durumda bir **çalışan rolü** projesi **LauncherWorker.ps1** gerekli tooexecute hello başlatma dosyasını bir dosyadır. İçinde bir **web rolü** projesi, hello başlangıç dosyasına bunun yerine hello Proje Özellikleri'nde tanımlanır.
> 
> 

Merhaba **bin\LaunchWorker.ps1** hazırlık iş ancak birçok gerçekten işe yaramazsa toodo ilk olarak oluşturuldu. Bu dosyayı Merhaba içeriğine komut dosyası izleyen hello ile değiştirin.

Bu komut dosyasını hello çağıran **worker.py** python projenizden dosya. Merhaba, **PYTHON2** ortam değişkenini çok ayarlamak**üzerinde**, Python 2.7 kullanılırsa, aksi halde Python 3.5 kullanılır.

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

#### <a name="pscmd"></a>ps.cmd
Merhaba Visual Studio şablonları oluşturmuş bir **ps.cmd** hello dosyasında **. / bin** klasör. Bu kabuk betiği hello PowerShell sarmalayıcı betikleri yukarıdaki çağırır ve adlı hello PowerShell sarmalayıcı hello adını temel alarak günlük kaydını sağlar. Bu dosya oluşturulmadıysa içinde olması gerekenler aşağıda verilmiştir. 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a>Yerel olarak çalıştırma
Bulut hizmeti projenizi başlangıç başlangıç projesi olarak ayarla ve F5 tuşuna basarsanız, hello bulut hizmeti hello yerel Azure öykünücüsünde çalışır.

PTVS destekler; ancak başlatma hata ayıklama hello öykünücüsünde (örneğin, kesme noktaları) çalışmaz.

toodebug, web ve çalışan rolleri hello rolü projesi hello başlangıç projesi olarak ayarlayın ve yerine hata ayıklama.  Ayrıca, birden fazla başlangıç projesi ayarlayabilirsiniz.  Merhaba çözüme sağ tıklayın ve ardından **başlangıç projelerini Ayarla**.

![Çözüm Başlangıç Projesi Özellikleri](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-tooazure"></a>TooAzure yayımlama
toopublish, hello çözümde hello bulut hizmeti projesine sağ tıklayın ve ardından **Yayımla**.

![Microsoft Azure Yayımlama Oturumu Açma](./media/cloud-services-python-ptvs/publish-sign-in.png)

Merhaba Sihirbazı izleyin. Gerekirse uzak masaüstünü etkinleştirin. Uzak Masaüstü toodebug bir şey gerektiğinde faydalıdır.

Yapılandırma ayarları bittiğinde **Yayımla**’ya tıklayın.

Merhaba çıktı penceresinde devam eden bazı işlemler görünür, ardından hello Microsoft Azure Etkinlik Günlüğü penceresini görürsünüz.

![Microsoft Azure Etkinlik Günlüğü Penceresi](./media/cloud-services-python-ptvs/publish-activity-log.png)

Birkaç dakika toocomplete, ardından web dağıtım alır ve/veya çalışan rolleri Azure üzerinde çalışan!

### <a name="investigate-logs"></a>Günlükleri araştırma
Merhaba bulut hizmeti sanal makine başlatıldığında ve Python yüklendikten sonra hata iletileri hello günlükleri toofind bakabilirsiniz. Bu günlükler hello bulunan **C:\Resources\Directory\\{rolü} \LogFiles** klasör. **PrepPython.err.txt** Python yüklediyseniz hello betik toodetect bulunduğunda gelen en az bir hata var ve **PipInstaller.err.txt** PIP eski bir sürümü hakkında şikayetçi.

## <a name="next-steps"></a>Sonraki adımlar
Visual Studio için Python Araçları'ndaki web ve çalışan rolleri ile çalışma hakkında daha ayrıntılı bilgi için hello PTVS belgelerine bakın:

* [Bulut Hizmeti Projeleri][Cloud Service Projects]

Azure Storage veya Service Bus kullanarak gibi web ve çalışan rolleri, Azure hizmetlerini kullanma hakkında daha fazla ayrıntı için aşağıdaki makaleleri hello bakın:

* [Blob Hizmeti][Blob Service]
* [Tablo Hizmeti][Table Service]
* [Kuyruk Hizmeti][Queue Service]
* [Service Bus Kuyrukları][Service Bus Queues]
* [Service Bus Konuları][Service Bus Topics]

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
