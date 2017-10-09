---
title: aaaDeploy hello Azure Otomasyonu DSC Site Recovery Mobility hizmetiyle | Microsoft Docs
description: "Nasıl toouse Azure Otomasyonu DSC tooautomatically dağıtmak hello Azure Site Recovery Mobility hizmeti ve Azure Aracısı VMware sanal ve fiziksel sunucu çoğaltma tooAzure açıklar"
services: site-recovery
documentationcenter: 
author: krnese
manager: lorenr
editor: 
ms.assetid: 1f8cd3ac-0522-48eb-a5f0-679ee9192ddb
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: krnese
ms.openlocfilehash: 52cdd13ceb61718a21137180c55db86919af5929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a><span data-ttu-id="21d45-103">VM çoğaltması için Azure Otomasyonu DSC ile Merhaba Mobility hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="21d45-103">Deploy hello Mobility service with Azure Automation DSC for replication of VM</span></span>
<span data-ttu-id="21d45-104">Operations Management Suite biz kapsamlı yedekleme ve iş sürekliliği planınızın bir parçası olarak kullanabileceğiniz olağanüstü durum kurtarma çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="21d45-104">In Operations Management Suite, we provide you with a comprehensive backup and disaster recovery solution that you can use as part of your business continuity plan.</span></span>

<span data-ttu-id="21d45-105">Biz bu gezisine Hyper-V ile birlikte Hyper-V çoğaltma kullanılarak başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="21d45-105">We started this journey together with Hyper-V by using Hyper-V Replica.</span></span> <span data-ttu-id="21d45-106">Ancak müşteriler kendi bulut birden fazla hiper ve platformlar olduğundan genişletilmiş toosupport heterojen Kurulum sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="21d45-106">But we have expanded toosupport a heterogeneous setup because customers have multiple hypervisors and platforms in their clouds.</span></span>

<span data-ttu-id="21d45-107">VMware iş yükleri ve/veya fiziksel sunucuları bugün çalıştırıyorsanız, Azure, hedef olduğunda bir yönetim sunucusu tüm hello Azure Site Recovery bileşenleri, ortam toohandle hello iletişim ve veri çoğaltma, Azure ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="21d45-107">If you are running VMware workloads and/or physical servers today, a management server runs all of hello Azure Site Recovery components in your environment toohandle hello communication and data replication with Azure, when Azure is your destination.</span></span>

## <a name="deploy-hello-site-recovery-mobility-service-by-using-automation-dsc"></a><span data-ttu-id="21d45-108">Automation DSC kullanarak Hello Site Recovery Mobility hizmeti dağıtma</span><span class="sxs-lookup"><span data-stu-id="21d45-108">Deploy hello Site Recovery Mobility service by using Automation DSC</span></span>
<span data-ttu-id="21d45-109">Bu yönetim sunucusu yaptığı bir hızlı dökümünü yaparak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="21d45-109">Let's start by doing a quick breakdown of what this management server does.</span></span>

<span data-ttu-id="21d45-110">Hello yönetim sunucusu, çeşitli sunucu rolleri çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="21d45-110">hello management server runs several server roles.</span></span> <span data-ttu-id="21d45-111">Bu roller, biri *yapılandırma*, hangi iletişimi düzenler ve veri çoğaltma ve kurtarma işlemlerini yönetir.</span><span class="sxs-lookup"><span data-stu-id="21d45-111">One of these roles is *configuration*, which coordinates communication and manages data replication and recovery processes.</span></span>

<span data-ttu-id="21d45-112">Ayrıca, hello *işlem* rol çoğaltma ağ geçidi olarak davranır.</span><span class="sxs-lookup"><span data-stu-id="21d45-112">In addition, hello *process* role acts as a replication gateway.</span></span> <span data-ttu-id="21d45-113">Bu rolü korumalı kaynak makinelerden çoğaltma verilerini alıp, önbelleğe alma, sıkıştırma ve şifreleme iyileştirir ve tooan Azure depolama hesabı gönderir.</span><span class="sxs-lookup"><span data-stu-id="21d45-113">This role receives replication data from protected source machines, optimizes it with caching, compression, and encryption, and then sends it tooan Azure storage account.</span></span> <span data-ttu-id="21d45-114">Hello işlevleri hello işlem rolü için birini de toopush yükleme hello Mobility hizmeti tooprotected makinelerin ve VMware vm'lerinin otomatik bulma gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="21d45-114">One of hello functions for hello process role is also toopush installation of hello Mobility service tooprotected machines and perform automatic discovery of VMware VMs.</span></span>

<span data-ttu-id="21d45-115">Bir azure'dan ise hello *ana hedef* rolü, bu işlemin bir parçası olarak hello çoğaltma verileri işleyecek.</span><span class="sxs-lookup"><span data-stu-id="21d45-115">If there's a failback from Azure, hello *master target* role will handle hello replication data as part of this operation.</span></span>

<span data-ttu-id="21d45-116">Merhaba korumalı makineler için biz üzerinde hello kullanan *Mobility hizmeti*.</span><span class="sxs-lookup"><span data-stu-id="21d45-116">For hello protected machines, we rely on hello *Mobility service*.</span></span> <span data-ttu-id="21d45-117">Bu bileşen tooreplicate tooAzure istediğiniz dağıtılan tooevery (VMware VM veya fiziksel sunucu) makinesidir.</span><span class="sxs-lookup"><span data-stu-id="21d45-117">This component is deployed tooevery machine (VMware VM or physical server) that you want tooreplicate tooAzure.</span></span> <span data-ttu-id="21d45-118">Merhaba makinede veri Yazar yakalar ve bunları toohello yönetim sunucusu (işlem rolü) iletir.</span><span class="sxs-lookup"><span data-stu-id="21d45-118">It captures data writes on hello machine and forwards them toohello management server (process role).</span></span>

<span data-ttu-id="21d45-119">İş sürekliliği ile ilgilenirken önemli toounderstand iş yüklerinizi, altyapı ve hello bileşenleri dahil değil.</span><span class="sxs-lookup"><span data-stu-id="21d45-119">When you're dealing with business continuity, it's important toounderstand your workloads, your infrastructure, and hello components involved.</span></span> <span data-ttu-id="21d45-120">Ardından Kurtarma süresi hedefi (RTO) ve kurtarma noktası hedefi (RPO) hello gereksinimleri karşılayabilir.</span><span class="sxs-lookup"><span data-stu-id="21d45-120">You can then meet hello requirements for your recovery time objective (RTO) and recovery point objective (RPO).</span></span> <span data-ttu-id="21d45-121">Bu bağlamda anahtar tooensuring hello Mobility hizmeti olan beklediğiniz gibi iş yüklerinizi korunur.</span><span class="sxs-lookup"><span data-stu-id="21d45-121">In this context, hello Mobility service is key tooensuring that your workloads are protected as you would expect.</span></span>

<span data-ttu-id="21d45-122">Bu nedenle nasıl, iyileştirilmiş bir şekilde, bazı Operations Management Suite bileşenleri Yardım ile güvenilir bir korumalı kurulum olmasını sağlayabilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="21d45-122">So how can you, in an optimized way, ensure that you have a reliable protected setup with help from some Operations Management Suite components?</span></span>

<span data-ttu-id="21d45-123">Bu makalede, Azure Otomasyonu istenen durum yapılandırması (DSC), Site Recovery, tooensure birlikte nasıl kullanabileceğinize bir örnek sağlar:</span><span class="sxs-lookup"><span data-stu-id="21d45-123">This article provides an example of how you can use Azure Automation Desired State Configuration (DSC), together with Site Recovery, tooensure that:</span></span>

* <span data-ttu-id="21d45-124">Merhaba Mobility hizmeti ve Azure VM Aracısı tooprotect istediğiniz dağıtılan toohello Windows makinelerdir.</span><span class="sxs-lookup"><span data-stu-id="21d45-124">hello Mobility service and Azure VM agent are deployed toohello Windows machines that you want tooprotect.</span></span>
* <span data-ttu-id="21d45-125">Azure hello çoğaltma hedefi olduğunda hello Mobility hizmeti ve Azure VM Aracısı her zaman çalışır.</span><span class="sxs-lookup"><span data-stu-id="21d45-125">hello Mobility service and Azure VM agent are always running when Azure is hello replication target.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21d45-126">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="21d45-126">Prerequisites</span></span>
* <span data-ttu-id="21d45-127">Bir depo toostore gerekli hello Kurulumu</span><span class="sxs-lookup"><span data-stu-id="21d45-127">A repository toostore hello required setup</span></span>
* <span data-ttu-id="21d45-128">Parola tooregister hello yönetim sunucusu ile bir depo toostore hello gerekli</span><span class="sxs-lookup"><span data-stu-id="21d45-128">A repository toostore hello required passphrase tooregister with hello management server</span></span>

  > [!NOTE]
  > <span data-ttu-id="21d45-129">Her yönetim sunucusu için benzersiz bir parola oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="21d45-129">A unique passphrase is generated for each management server.</span></span> <span data-ttu-id="21d45-130">Birden çok yönetim sunucusu toodeploy kullanacaksanız, bu hello parola hello passphrase.txt dosyasında depolanan doğru tooensure sahip.</span><span class="sxs-lookup"><span data-stu-id="21d45-130">If you are going toodeploy multiple management servers, you have tooensure that hello correct passphrase is stored in hello passphrase.txt file.</span></span>
  >
  >
* <span data-ttu-id="21d45-131">Windows Management Framework (WMF) koruma (Automation DSC gereksinimini) için tooenable istediğiniz hello makinelerde yüklü 5.0</span><span class="sxs-lookup"><span data-stu-id="21d45-131">Windows Management Framework (WMF) 5.0 installed on hello machines that you want tooenable for protection (a requirement for Automation DSC)</span></span>

  > [!NOTE]
  > <span data-ttu-id="21d45-132">WMF 4.0 yüklü olan toouse DSC for Windows makineler istiyorsanız hello bölümüne bakın [bağlantısı kesilmiş ortamlarda kullanım DSC](## Use DSC in disconnected environments).</span><span class="sxs-lookup"><span data-stu-id="21d45-132">If you want toouse DSC for Windows machines that have WMF 4.0 installed, see hello section [Use DSC in disconnected environments](## Use DSC in disconnected environments).</span></span>
  

<span data-ttu-id="21d45-133">Merhaba Mobility hizmeti hello komut satırı yüklenebilir ve birkaç bağımsız değişken kabul eder.</span><span class="sxs-lookup"><span data-stu-id="21d45-133">hello Mobility service can be installed through hello command line and accepts several arguments.</span></span> <span data-ttu-id="21d45-134">İşte bu nedenle Burada, alabilir bunları DSC Yapılandırması kullanılarak bir yerde saklayın ve toohave hello ikili dosyaları (bunları, kurulumdan ayıkladıktan sonra) gerekir.</span><span class="sxs-lookup"><span data-stu-id="21d45-134">That’s why you need toohave hello binaries (after extracting them from your setup) and store them in a place where you can retrieve them by using a DSC configuration.</span></span>

## <a name="step-1-extract-binaries"></a><span data-ttu-id="21d45-135">1. adım: Extract ikili dosyalar</span><span class="sxs-lookup"><span data-stu-id="21d45-135">Step 1: Extract binaries</span></span>
1. <span data-ttu-id="21d45-136">Bu kurulum için gereken tooextract hello dosyalar Dizin Yönetim sunucunuzda aşağıdaki toohello göz atın:</span><span class="sxs-lookup"><span data-stu-id="21d45-136">tooextract hello files that you need for this setup, browse toohello following directory on your management server:</span></span>

    <span data-ttu-id="21d45-137">**\Microsoft azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span><span class="sxs-lookup"><span data-stu-id="21d45-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span></span>

    <span data-ttu-id="21d45-138">Bu klasörde, adlandırılmış bir MSI dosyası görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="21d45-138">In this folder, you should see an MSI file named:</span></span>

    <span data-ttu-id="21d45-139">**Microsoft ASR_UA_version_Windows_GA_date_Release.exe**</span><span class="sxs-lookup"><span data-stu-id="21d45-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span></span>

    <span data-ttu-id="21d45-140">Komut tooextract hello Yükleyici aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="21d45-140">Use hello following command tooextract hello installer:</span></span>

    <span data-ttu-id="21d45-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span><span class="sxs-lookup"><span data-stu-id="21d45-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span></span>
2. <span data-ttu-id="21d45-142">Tüm dosyaları seçin ve tooa sıkıştırılmış (ZIP) klasör gönderin.</span><span class="sxs-lookup"><span data-stu-id="21d45-142">Select all files and send them tooa compressed (zipped) folder.</span></span>

<span data-ttu-id="21d45-143">Artık hello ikili dosyaları Automation DSC kullanarak hello Mobility hizmeti tooautomate hello Kurulumu ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="21d45-143">You now have hello binaries that you need tooautomate hello setup of hello Mobility service by using Automation DSC.</span></span>

### <a name="passphrase"></a><span data-ttu-id="21d45-144">Parola</span><span class="sxs-lookup"><span data-stu-id="21d45-144">Passphrase</span></span>
<span data-ttu-id="21d45-145">Ardından, bu sıkıştırılmış klasörü tooplace istediğiniz yere toodetermine gerekir.</span><span class="sxs-lookup"><span data-stu-id="21d45-145">Next, you need toodetermine where you want tooplace this zipped folder.</span></span> <span data-ttu-id="21d45-146">Merhaba kurulum için gereken gösterilen daha sonra toostore hello parola olarak bir Azure depolama hesabı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21d45-146">You can use an Azure storage account, as shown later, toostore hello passphrase that you need for hello setup.</span></span> <span data-ttu-id="21d45-147">Merhaba Aracısı sonra hello yönetim sunucusu hello işleminin bir parçası olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="21d45-147">hello agent will then register with hello management server as part of hello process.</span></span>

<span data-ttu-id="21d45-148">Merhaba yönetim sunucusunu dağıttığınızda aldığınız hello parola tooa metin dosyası passphrase.txt kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="21d45-148">hello passphrase that you got when you deployed hello management server can be saved tooa text file as passphrase.txt.</span></span>

<span data-ttu-id="21d45-149">Merhaba daraltılmış klasörü ve hello parola hello Azure depolama hesabı adanmış bir kapsayıcıda yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="21d45-149">Place both hello zipped folder and hello passphrase in a dedicated container in hello Azure storage account.</span></span>

![Klasör konumu](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

<span data-ttu-id="21d45-151">Bu dosya paylaşımındaki ağınızdaki tookeep tercih ederseniz, bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21d45-151">If you prefer tookeep these files on a share on your network, you can do so.</span></span> <span data-ttu-id="21d45-152">Daha sonra kullanacaksınız hello DSC kaynağı erişimi vardır ve hello Kurulum ve parola alabilirsiniz tooensure yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="21d45-152">You just need tooensure that hello DSC resource that you will be using later has access and can get hello setup and passphrase.</span></span>

## <a name="step-2-create-hello-dsc-configuration"></a><span data-ttu-id="21d45-153">2. adım: hello DSC yapılandırması oluştur</span><span class="sxs-lookup"><span data-stu-id="21d45-153">Step 2: Create hello DSC configuration</span></span>
<span data-ttu-id="21d45-154">WMF 5. 0'Hello Kurulum bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="21d45-154">hello setup depends on WMF 5.0.</span></span> <span data-ttu-id="21d45-155">Automation DSC aracılığıyla hello yapılandırma Hello makine toosuccessfully için uygulama, WMF 5.0 toobe mevcut gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="21d45-155">For hello machine toosuccessfully apply hello configuration through Automation DSC, WMF 5.0 needs toobe present.</span></span>

<span data-ttu-id="21d45-156">Merhaba ortamı örnek DSC yapılandırması aşağıdaki hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="21d45-156">hello environment uses hello following example DSC configuration:</span></span>

```powershell
configuration ASRMobilityService {

    $RemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    $RemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    $RemoteAzureAgent = 'http://go.microsoft.com/fwlink/p/?LinkId=394789'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node localhost {

        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
```
<span data-ttu-id="21d45-157">Merhaba yapılandırması yeterlidir hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="21d45-157">hello configuration will do hello following:</span></span>

* <span data-ttu-id="21d45-158">Merhaba değişkenleri hello yapılandırma tooget hello burada parola ve toostore hello çıktı tooget hello Mobility hizmeti ve hello Azure VM Aracısı ikili dosyaları nerede hello söyler.</span><span class="sxs-lookup"><span data-stu-id="21d45-158">hello variables will tell hello configuration where tooget hello binaries for hello Mobility service and hello Azure VM agent, where tooget hello passphrase, and where toostore hello output.</span></span>
* <span data-ttu-id="21d45-159">böylece kullanabileceğiniz hello yapılandırma hello xPSDesiredStateConfiguration DSC kaynağı alacak `xRemoteFile` hello depodan toodownload hello dosyaları.</span><span class="sxs-lookup"><span data-stu-id="21d45-159">hello configuration will import hello xPSDesiredStateConfiguration DSC resource, so that you can use `xRemoteFile` toodownload hello files from hello repository.</span></span>
* <span data-ttu-id="21d45-160">Merhaba yapılandırmasını toostore hello ikili dosyaları istediğiniz bir dizin oluşturur.</span><span class="sxs-lookup"><span data-stu-id="21d45-160">hello configuration will create a directory where you want toostore hello binaries.</span></span>
* <span data-ttu-id="21d45-161">Merhaba arşiv kaynak hello dosyaları hello sıkıştırılmış klasörden ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="21d45-161">hello archive resource will extract hello files from hello zipped folder.</span></span>
* <span data-ttu-id="21d45-162">Merhaba paket yükleme kaynağı hello Mobility hizmeti UNIFIEDAGENT hello yükler. EXE yükleyici hello belirli bağımsız değişkenlere sahip.</span><span class="sxs-lookup"><span data-stu-id="21d45-162">hello package Install resource will install hello Mobility service from hello UNIFIEDAGENT.EXE installer with hello specific arguments.</span></span> <span data-ttu-id="21d45-163">(Merhaba bağımsız değişkenleri oluşturmak hello değişkenleri ortamınız değiştirilen toobe tooreflect gerekir.)</span><span class="sxs-lookup"><span data-stu-id="21d45-163">(hello variables that construct hello arguments need toobe changed tooreflect your environment.)</span></span>
* <span data-ttu-id="21d45-164">Merhaba paket AzureAgent kaynak Azure'da çalışan her VM üzerinde önerilen hello Azure VM aracısı yükler.</span><span class="sxs-lookup"><span data-stu-id="21d45-164">hello package AzureAgent resource will install hello Azure VM agent, which is recommended on every VM that runs in Azure.</span></span> <span data-ttu-id="21d45-165">Hello Azure VM aracısı ayrıca olası tooadd uzantıları toohello VM yük devretme sonrasında kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="21d45-165">hello Azure VM agent also makes it possible tooadd extensions toohello VM after failover.</span></span>
* <span data-ttu-id="21d45-166">Merhaba Hizmet kaynağı veya kaynakları hello Mobility Hizmetleri ilgili hello Azure hizmetlerinin her zaman çalıştığından emin olun ve.</span><span class="sxs-lookup"><span data-stu-id="21d45-166">hello service resource or resources will ensure that hello related Mobility services and hello Azure services are always running.</span></span>

<span data-ttu-id="21d45-167">Merhaba yapılandırma olarak Kaydet **ASRMobilityService**.</span><span class="sxs-lookup"><span data-stu-id="21d45-167">Save hello configuration as **ASRMobilityService**.</span></span>

> [!NOTE]
> <span data-ttu-id="21d45-168">Böylece Hello Aracısı doğru bağlanır ve hello doğru parolayı kullanır, yapılandırma tooreflect hello gerçek yönetim sunucusu tooreplace hello CSIP unutmayın.</span><span class="sxs-lookup"><span data-stu-id="21d45-168">Remember tooreplace hello CSIP in your configuration tooreflect hello actual management server, so that hello agent will be connected correctly and will use hello correct passphrase.</span></span>
>
>

## <a name="step-3-upload-tooautomation-dsc"></a><span data-ttu-id="21d45-169">3. adım: tooAutomation DSC karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="21d45-169">Step 3: Upload tooAutomation DSC</span></span>
<span data-ttu-id="21d45-170">Yaptığınız hello DSC yapılandırması gerekli bir DSC kaynakları Modülü (xPSDesiredStateConfiguration) alacağı için hello DSC yapılandırma karşıya yüklemeden önce otomasyon modülü tooimport gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="21d45-170">Because hello DSC configuration that you made will import a required DSC resource module (xPSDesiredStateConfiguration), you need tooimport that module in Automation before you upload hello DSC configuration.</span></span>

<span data-ttu-id="21d45-171">Oturum açma tooyour Otomasyon hesabı Gözat çok**varlıklar** > **modülleri**, tıklatıp **Gözat galeri**.</span><span class="sxs-lookup"><span data-stu-id="21d45-171">Sign in tooyour Automation account, browse too**Assets** > **Modules**, and click **Browse Gallery**.</span></span>

<span data-ttu-id="21d45-172">Merhaba modülü burada aratın ve tooyour hesap içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="21d45-172">Here you can search for hello module and import it tooyour account.</span></span>

![İçeri aktarma modülü](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

<span data-ttu-id="21d45-174">Bu tamamladığınızda, hello Azure Resource Manager modüllerini yüklü olduğu tooyour makine gidin ve tooimport yeni oluşturulan hello DSC yapılandırması devam edin.</span><span class="sxs-lookup"><span data-stu-id="21d45-174">When you finish this, go tooyour machine where you have hello Azure Resource Manager modules installed and proceed tooimport hello newly created DSC configuration.</span></span>

### <a name="import-cmdlets"></a><span data-ttu-id="21d45-175">İçeri aktarma cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="21d45-175">Import cmdlets</span></span>
<span data-ttu-id="21d45-176">PowerShell'de tooyour Azure aboneliği oturum açın.</span><span class="sxs-lookup"><span data-stu-id="21d45-176">In PowerShell, sign in tooyour Azure subscription.</span></span> <span data-ttu-id="21d45-177">Ortamınızı Hello cmdlet'leri tooreflect değiştirin ve Automation hesabı bilgilerinizi bir değişkende Yakala:</span><span class="sxs-lookup"><span data-stu-id="21d45-177">Modify hello cmdlets tooreflect your environment and capture your Automation account information in a variable:</span></span>

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

<span data-ttu-id="21d45-178">Merhaba yapılandırma tooAutomation DSC cmdlet'i aşağıdaki hello kullanarak karşıya yükle:</span><span class="sxs-lookup"><span data-stu-id="21d45-178">Upload hello configuration tooAutomation DSC by using hello following cmdlet:</span></span>

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-hello-configuration-in-automation-dsc"></a><span data-ttu-id="21d45-179">Automation DSC Hello yapılandırmasında derleme</span><span class="sxs-lookup"><span data-stu-id="21d45-179">Compile hello configuration in Automation DSC</span></span>
<span data-ttu-id="21d45-180">Ardından, tooregister düğümleri tooit başlayabilmeniz toocompile hello Automation DSC yapılandırmasında gerekir.</span><span class="sxs-lookup"><span data-stu-id="21d45-180">Next, you need toocompile hello configuration in Automation DSC, so that you can start tooregister nodes tooit.</span></span> <span data-ttu-id="21d45-181">Bu cmdlet'i aşağıdaki hello çalıştırarak elde:</span><span class="sxs-lookup"><span data-stu-id="21d45-181">You achieve that by running hello following cmdlet:</span></span>

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

<span data-ttu-id="21d45-182">Hello yapılandırma barındırılan toohello DSC çekme hizmeti temel olarak dağıtıyorsunuz için bu işlem birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="21d45-182">This can take a few minutes, because you're basically deploying hello configuration toohello hosted DSC pull service.</span></span>

<span data-ttu-id="21d45-183">Merhaba yapılandırma derledikten sonra PowerShell (Get-AzureRmAutomationDscCompilationJob) kullanarak veya hello kullanarak hello iş bilgilerini alabilir [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="21d45-183">After you compile hello configuration, you can retrieve hello job information by using PowerShell (Get-AzureRmAutomationDscCompilationJob) or by using hello [Azure portal](https://portal.azure.com/).</span></span>

![İş alma](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

<span data-ttu-id="21d45-185">Şimdi başarıyla yayımlandı ve DSC yapılandırma tooAutomation DSC karşıya.</span><span class="sxs-lookup"><span data-stu-id="21d45-185">You have now successfully published and uploaded your DSC configuration tooAutomation DSC.</span></span>

## <a name="step-4-onboard-machines-tooautomation-dsc"></a><span data-ttu-id="21d45-186">4. adım: Yerleşik makineler tooAutomation DSC</span><span class="sxs-lookup"><span data-stu-id="21d45-186">Step 4: Onboard machines tooAutomation DSC</span></span>
> [!NOTE]
> <span data-ttu-id="21d45-187">Bu senaryo Tamamlanıyor hello önkoşulları Windows makinelerinizi hello en son sürümüyle WMF güncelleştirilir biridir.</span><span class="sxs-lookup"><span data-stu-id="21d45-187">One of hello prerequisites for completing this scenario is that your Windows machines are updated with hello latest version of WMF.</span></span> <span data-ttu-id="21d45-188">Karşıdan yükle ve platformunuza hello gelen hello doğru sürümünü yüklemek [Yükleme Merkezi'nden](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="21d45-188">You can download and install hello correct version for your platform from hello [Download Center](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>
>
>

<span data-ttu-id="21d45-189">Şimdi bir metaconfig tooyour düğümleri uygulanacağını DSC için oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="21d45-189">You will now create a metaconfig for DSC that you will apply tooyour nodes.</span></span> <span data-ttu-id="21d45-190">toosucceed Bu, seçilen Otomasyon hesabınızda Azure tooretrieve hello uç noktası URL'si ve hello birincil anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="21d45-190">toosucceed with this, you need tooretrieve hello endpoint URL and hello primary key for your selected Automation account in Azure.</span></span> <span data-ttu-id="21d45-191">Bu değerleri altında bulabilirsiniz **anahtarları** hello üzerinde **tüm ayarları** dikey penceresinde hello Otomasyon hesabı için.</span><span class="sxs-lookup"><span data-stu-id="21d45-191">You can find these values under **Keys** on hello **All settings** blade for hello Automation account.</span></span>

![Anahtar değerleri](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

<span data-ttu-id="21d45-193">Bu örnekte, tooprotect Site RECOVERY'yi kullanarak istediğiniz bir Windows Server 2012 R2 fiziksel sunucu vardır.</span><span class="sxs-lookup"><span data-stu-id="21d45-193">In this example, you have a Windows Server 2012 R2 physical server that you want tooprotect by using Site Recovery.</span></span>

### <a name="check-for-any-pending-file-rename-operations-in-hello-registry"></a><span data-ttu-id="21d45-194">Dosya yeniden adlandırma işlemleri hello kayıt defterinde beklemedeki denetle</span><span class="sxs-lookup"><span data-stu-id="21d45-194">Check for any pending file rename operations in hello registry</span></span>
<span data-ttu-id="21d45-195">Merhaba Automation DSC noktayla tooassociate hello sunucu başlamadan önce beklemede olan dosya yeniden adlandırma işlemleri hello kayıt defterinde için denetlemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="21d45-195">Before you start tooassociate hello server with hello Automation DSC endpoint, we recommend that you check for any pending file rename operations in hello registry.</span></span> <span data-ttu-id="21d45-196">Son tamamlama hello Kurulum yasaklayabilir tooa yeniden başlatma bekleniyor.</span><span class="sxs-lookup"><span data-stu-id="21d45-196">They might prohibit hello setup from finishing due tooa pending reboot.</span></span>

<span data-ttu-id="21d45-197">Hiçbir yeniden başlatma bekleniyor hello sunucuda olduğunu cmdlet tooverify aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="21d45-197">Run hello following cmdlet tooverify that there’s no pending reboot on hello server:</span></span>

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
<span data-ttu-id="21d45-198">Bu boş gösterir, Tamam tooproceed demektir.</span><span class="sxs-lookup"><span data-stu-id="21d45-198">If this shows empty, you are OK tooproceed.</span></span> <span data-ttu-id="21d45-199">Aksi durumda, bu hello sunucunun bir bakım penceresi sırasında yeniden tarafından bulundurmalıdır.</span><span class="sxs-lookup"><span data-stu-id="21d45-199">If not, you should address this by rebooting hello server during a maintenance window.</span></span>

<span data-ttu-id="21d45-200">Merhaba sunucuda tooapply hello yapılandırma hello PowerShell Tümleşik komut dosyası ortamı (ISE) başlatın ve komut dosyası izleyen hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="21d45-200">tooapply hello configuration on hello server, start hello PowerShell Integrated Scripting Environment (ISE) and run hello following script.</span></span> <span data-ttu-id="21d45-201">Merhaba Automation DSC hizmeti ile Merhaba yerel Configuration Manager altyapısı tooregister istemek ve hello özel yapılandırma (ASRMobilityService.localhost) almak aslında bir DSC yerel yapılandırma budur.</span><span class="sxs-lookup"><span data-stu-id="21d45-201">This is essentially a DSC local configuration that will instruct hello Local Configuration Manager engine tooregister with hello Automation DSC service and retrieve hello specific configuration (ASRMobilityService.localhost).</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration metaconfig {
    param (
        $URL,
        $Key
    )
    node localhost {
        Settings {
            RefreshFrequencyMins = '30'
            RebootNodeIfNeeded = $true
            RefreshMode = 'PULL'
            ActionAfterReboot = 'ContinueConfiguration'
            ConfigurationMode = 'ApplyAndMonitor'
            AllowModuleOverwrite = $true
        }

        ResourceRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }

        ConfigurationRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
            ConfigurationNames = 'ASRMobilityService.localhost'
        }

        ReportServerWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }
    }
}
metaconfig -URL 'https://we-agentservice-prod-1.azure-automation.net/accounts/<YOURAAAccountID>' -Key '<YOURAAAccountKey>'

Set-DscLocalConfigurationManager .\metaconfig -Force -Verbose
```

<span data-ttu-id="21d45-202">Bu yapılandırma hello yerel Configuration Manager altyapısı tooregister kendisini Otomasyonu DSC'ye neden olur.</span><span class="sxs-lookup"><span data-stu-id="21d45-202">This configuration will cause hello Local Configuration Manager engine tooregister itself with Automation DSC.</span></span> <span data-ttu-id="21d45-203">Ayrıca, hello altyapısı nasıl çalışacağını, yapılandırma değişikliklerini (ApplyAndAutoCorrect) ise ne yapmanız gerektiğini ve yeniden başlatma gerekli olduğunda nasıl, hello yapılandırmasıyla devam etmemelisiniz belirler.</span><span class="sxs-lookup"><span data-stu-id="21d45-203">It will also determine how hello engine should operate, what it should do if there's a configuration drift (ApplyAndAutoCorrect), and how it should proceed with hello configuration if a reboot is required.</span></span>

<span data-ttu-id="21d45-204">Bu komut dosyasını çalıştırdıktan sonra hello düğümü Otomasyonu DSC'ye tooregister başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="21d45-204">After you run this script, hello node should start tooregister with Automation DSC.</span></span>

![Düğüm kayıt işlemi sürüyor](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

<span data-ttu-id="21d45-206">Toohello Azure portalına geri dönün, o hello yeni kayıtlı düğüm hello Portalı'nda artık göründükten görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21d45-206">If you go back toohello Azure portal, you can see that hello newly registered node has now appeared in hello portal.</span></span>

![Merhaba Portalı'nda kayıtlı düğümü](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

<span data-ttu-id="21d45-208">Merhaba sunucuda düğümü hello cmdlet tooverify doğru kayıtlı PowerShell aşağıdaki hello çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="21d45-208">On hello server, you can run hello following PowerShell cmdlet tooverify that hello node has been registered correctly:</span></span>

```powershell
Get-DscLocalConfigurationManager
```

<span data-ttu-id="21d45-209">Merhaba yapılandırma çekilen ve uygulanan toohello sunucu alındıktan sonra Bu cmdlet'i aşağıdaki hello çalıştırarak doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="21d45-209">After hello configuration has been pulled and applied toohello server, you can verify this by running hello following cmdlet:</span></span>

```powershell
Get-DscConfigurationStatus
```

<span data-ttu-id="21d45-210">Merhaba çıktısı hello sunucu yapılandırmasıyla başarıyla çekilen gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="21d45-210">hello output shows that hello server has successfully pulled its configuration:</span></span>

![Çıktı](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

<span data-ttu-id="21d45-212">Ayrıca, hello Mobility hizmeti Kurulumu konumunda bulunan kendi günlük sahip *SystemDrive*\ProgramData\ASRSetupLogs.</span><span class="sxs-lookup"><span data-stu-id="21d45-212">In addition, hello Mobility service setup has its own log that can be found at *SystemDrive*\ProgramData\ASRSetupLogs.</span></span>

<span data-ttu-id="21d45-213">İşte bu kadar.</span><span class="sxs-lookup"><span data-stu-id="21d45-213">That’s it.</span></span> <span data-ttu-id="21d45-214">Şimdi başarıyla dağıtılan ve Site Recovery kullanarak tooprotect istediğiniz hello makinedeki hello Mobility hizmeti kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="21d45-214">You have now successfully deployed and registered hello Mobility service on hello machine that you want tooprotect by using Site Recovery.</span></span> <span data-ttu-id="21d45-215">DSC hello gerekli hizmetleri zaman çalışır durumda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="21d45-215">DSC will make sure that hello required services are always running.</span></span>

![Başarılı dağıtım](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

<span data-ttu-id="21d45-217">Merhaba yönetim sunucusu hello başarılı dağıtım algılandıktan sonra korumayı yapılandırın ve Site Recovery kullanarak hello makinesinde çoğaltmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="21d45-217">After hello management server detects hello successful deployment, you can configure protection and enable replication on hello machine by using Site Recovery.</span></span>

## <a name="use-dsc-in-disconnected-environments"></a><span data-ttu-id="21d45-218">Bağlantısı kesilmiş ortamlarda DSC kullanın</span><span class="sxs-lookup"><span data-stu-id="21d45-218">Use DSC in disconnected environments</span></span>
<span data-ttu-id="21d45-219">Makinelerinizi bağlı toohello Internet değilseniz, hala DSC toodeploy üzerinde kullanır ve tooprotect istediğiniz hello iş yükleri üzerinde hello Mobility hizmetini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="21d45-219">If your machines aren’t connected toohello Internet, you can still rely on DSC toodeploy and configure hello Mobility service on hello workloads that you want tooprotect.</span></span>

<span data-ttu-id="21d45-220">Kendi DSC istek sunucusuyla ortamınızda örneği tooessentially hello Automation DSC'den alma aynı yetenekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="21d45-220">You can instantiate your own DSC pull server in your environment tooessentially provide hello same capabilities that you get from Automation DSC.</span></span> <span data-ttu-id="21d45-221">Diğer bir deyişle, (kaydedildikten sonra) hello istemcileri hello yapılandırma çeker toohello DSC uç noktası.</span><span class="sxs-lookup"><span data-stu-id="21d45-221">That is, hello clients will pull hello configuration (after it's registered) toohello DSC endpoint.</span></span> <span data-ttu-id="21d45-222">Ancak, başka bir toomanually itme hello DSC yapılandırma tooyour makineler, yerel olarak veya uzaktan seçenektir.</span><span class="sxs-lookup"><span data-stu-id="21d45-222">However, another option is toomanually push hello DSC configuration tooyour machines, either locally or remotely.</span></span>

<span data-ttu-id="21d45-223">Bu örnekte, hello bilgisayar adı için ek bir parametre yoktur.</span><span class="sxs-lookup"><span data-stu-id="21d45-223">Note that in this example, there's an added parameter for hello computer name.</span></span> <span data-ttu-id="21d45-224">Merhaba uzak dosyalar, artık tooprotect istediğiniz hello makineler tarafından erişilebilir olması gereken bir uzak paylaşım bulunur.</span><span class="sxs-lookup"><span data-stu-id="21d45-224">hello remote files are now located on a remote share that should be accessible by hello machines that you want tooprotect.</span></span> <span data-ttu-id="21d45-225">Merhaba hello komut dosyasının sonuna hello yapılandırma enacts ve ardından tooapply hello DSC yapılandırma toohello hedef bilgisayarı başlatır.</span><span class="sxs-lookup"><span data-stu-id="21d45-225">hello end of hello script enacts hello configuration and then starts tooapply hello DSC configuration toohello target computer.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="21d45-226">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="21d45-226">Prerequisites</span></span>
<span data-ttu-id="21d45-227">Bu hello xPSDesiredStateConfiguration PowerShell Modülü yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="21d45-227">Make sure that hello xPSDesiredStateConfiguration PowerShell module is installed.</span></span> <span data-ttu-id="21d45-228">WMF 5.0 yüklü olduğu Windows makineler için hello xPSDesiredStateConfiguration modülü cmdlet hello hedef makinede aşağıdaki hello çalıştırarak yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="21d45-228">For Windows machines where WMF 5.0 is installed, you can install hello xPSDesiredStateConfiguration module by running hello following cmdlet on hello target machines:</span></span>

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

<span data-ttu-id="21d45-229">Ayrıca indirin ve toodistribute gerektiğinde Merhaba modülü kaydedin, WMF 4.0 sahip tooWindows makineler.</span><span class="sxs-lookup"><span data-stu-id="21d45-229">You can also download and save hello module in case you need toodistribute it tooWindows machines that have WMF 4.0.</span></span> <span data-ttu-id="21d45-230">Bu cmdlet, PowerShellGet (WMF 5.0) mevcut olduğu bir makinede çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="21d45-230">Run this cmdlet on a machine where PowerShellGet (WMF 5.0) is present:</span></span>

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

<span data-ttu-id="21d45-231">Ayrıca bu hello WMF 4.0 için olun [Windows 8.1 güncelleştirmesi KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) hello makinelerde yüklü.</span><span class="sxs-lookup"><span data-stu-id="21d45-231">Also for WMF 4.0, ensure that hello [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) is installed on hello machines.</span></span>

<span data-ttu-id="21d45-232">Merhaba aşağıdaki yapılandırma WMF 5.0 ve WMF 4.0 tooWindows makineler gönderilemez:</span><span class="sxs-lookup"><span data-stu-id="21d45-232">hello following configuration can be pushed tooWindows machines that have WMF 5.0 and WMF 4.0:</span></span>

```powershell
configuration ASRMobilityService {
    param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        [System.String] $ComputerName
    )

    $RemoteFile = '\\myfileserver\share\asr.zip'
    $RemotePassphrase = '\\myfileserver\share\passphrase.txt'
    $RemoteAzureAgent = '\\myfileserver\share\AzureVmAgent.msi'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node $ComputerName {      
        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
ASRMobilityService -ComputerName 'MyTargetComputerName'

Start-DscConfiguration .\ASRMobilityService -Wait -Force -Verbose
```

<span data-ttu-id="21d45-233">Automation DSC'den alabilir, şirket ağı toomimic hello yetenekleri üzerinde kendi DSC istek sunucusuyla tooinstantiate istiyorsanız bkz [DSC web çekme sunucusu kurma](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="21d45-233">If you want tooinstantiate your own DSC pull server on your corporate network toomimic hello capabilities that you can get from Automation DSC, see [Setting up a DSC web pull server](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span></span>

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="21d45-234">İsteğe bağlı: DSC yapılandırması bir Azure Resource Manager şablonu kullanarak dağıtın</span><span class="sxs-lookup"><span data-stu-id="21d45-234">Optional: Deploy a DSC configuration by using an Azure Resource Manager template</span></span>
<span data-ttu-id="21d45-235">Bu makale, kendi DSC yapılandırma tooautomatically nasıl oluşturabileceğinizi üzerinde odaklanılmış hello Mobility hizmeti ve hello Azure VM Aracısı--dağıtmak ve bunlar hello makinelerde tooprotect istediğiniz çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="21d45-235">This article has focused on how you can create your own DSC configuration tooautomatically deploy hello Mobility service and hello Azure VM Agent--and ensure that they are running on hello machines that you want tooprotect.</span></span> <span data-ttu-id="21d45-236">Biz de bu DSC yapılandırması tooa yeni veya var olan Azure Otomasyon hesabı dağıtacağınız bir Azure Resource Manager şablonu vardır.</span><span class="sxs-lookup"><span data-stu-id="21d45-236">We also have an Azure Resource Manager template that will deploy this DSC configuration tooa new or existing Azure Automation account.</span></span> <span data-ttu-id="21d45-237">Merhaba şablon hello değişkenleri ortamınız için içerecek giriş parametreleri toocreate Otomasyon varlıkları kullanır.</span><span class="sxs-lookup"><span data-stu-id="21d45-237">hello template will use input parameters toocreate Automation assets that will contain hello variables for your environment.</span></span>

<span data-ttu-id="21d45-238">Merhaba şablon dağıttıktan sonra bu kılavuzu tooonboard içinde toostep 4 yalnızca makinelerinizi başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="21d45-238">After you deploy hello template, you can simply refer toostep 4 in this guide tooonboard your machines.</span></span>

<span data-ttu-id="21d45-239">Merhaba şablon yeterlidir hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="21d45-239">hello template will do hello following:</span></span>

1. <span data-ttu-id="21d45-240">Var olan Otomasyon hesabını kullanabilir veya yeni bir tane oluşturun</span><span class="sxs-lookup"><span data-stu-id="21d45-240">Use an existing Automation account or create a new one</span></span>
2. <span data-ttu-id="21d45-241">Giriş parametreleri için alın:</span><span class="sxs-lookup"><span data-stu-id="21d45-241">Take input parameters for:</span></span>
   * <span data-ttu-id="21d45-242">ASRRemoteFile--hello Mobility hizmeti Kurulumu depoladığınız hello konumu</span><span class="sxs-lookup"><span data-stu-id="21d45-242">ASRRemoteFile--hello location where you have stored hello Mobility service setup</span></span>
   * <span data-ttu-id="21d45-243">ASRPassphrase--hello passphrase.txt dosyasını depoladığınız hello konumu</span><span class="sxs-lookup"><span data-stu-id="21d45-243">ASRPassphrase--hello location where you have stored hello passphrase.txt file</span></span>
   * <span data-ttu-id="21d45-244">ASRCSEndpoint--yönetim sunucunuzun başlangıç IP adresi</span><span class="sxs-lookup"><span data-stu-id="21d45-244">ASRCSEndpoint--hello IP address of your management server</span></span>
3. <span data-ttu-id="21d45-245">Merhaba xPSDesiredStateConfiguration PowerShell modülünü içeri aktarın</span><span class="sxs-lookup"><span data-stu-id="21d45-245">Import hello xPSDesiredStateConfiguration PowerShell module</span></span>
4. <span data-ttu-id="21d45-246">Oluşturma ve hello DSC yapılandırmasını derleme</span><span class="sxs-lookup"><span data-stu-id="21d45-246">Create and compile hello DSC configuration</span></span>

<span data-ttu-id="21d45-247">Makinelerinizi koruması için ekleme başlayabilmeniz adımları önceki tüm hello hello doğru sırada gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="21d45-247">All hello preceding steps will happen in hello right order, so that you can start onboarding your machines for protection.</span></span>

<span data-ttu-id="21d45-248">Merhaba şablonla dağıtımı için yönergeler bulunur [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span><span class="sxs-lookup"><span data-stu-id="21d45-248">hello template, with instructions for deployment, is located on [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span></span>

<span data-ttu-id="21d45-249">PowerShell kullanarak Hello şablonu dağıtma:</span><span class="sxs-lookup"><span data-stu-id="21d45-249">Deploy hello template by using PowerShell:</span></span>

```powershell
$RGDeployArgs = @{
    Name = 'DSC3'
    ResourceGroupName = 'KNOMS'
    TemplateFile = 'https://raw.githubusercontent.com/krnese/AzureDeploy/master/OMS/MSOMS/DSC/azuredeploy.json'
    OMSAutomationAccountName = 'KNOMSAA'
    ASRRemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    ASRRemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    ASRCSEndpoint = '10.0.0.115'
    DSCJobGuid = [System.Guid]::NewGuid().ToString()
}
New-AzureRmResourceGroupDeployment @RGDeployArgs -Verbose
```

## <a name="next-steps"></a><span data-ttu-id="21d45-250">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="21d45-250">Next steps</span></span>
<span data-ttu-id="21d45-251">Merhaba Mobility hizmeti aracıları dağıttıktan sonra şunları yapabilirsiniz [çoğaltmayı etkinleştirme](site-recovery-vmware-to-azure.md) hello sanal makineler için.</span><span class="sxs-lookup"><span data-stu-id="21d45-251">After you deploy hello Mobility service agents, you can [enable replication](site-recovery-vmware-to-azure.md) for hello virtual machines.</span></span>
