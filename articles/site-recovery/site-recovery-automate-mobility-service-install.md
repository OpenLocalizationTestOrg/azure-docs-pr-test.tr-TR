---
title: "Azure Otomasyonu DSC Site Recovery Mobility hizmetiyle dağıtma | Microsoft Docs"
description: "VMware sanal ve fiziksel sunucu çoğaltma Azure için Azure Site Recovery Mobility hizmeti ve Azure Aracısı otomatik olarak dağıtmak için Azure Otomasyonu DSC kullanmayı açıklar"
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
ms.openlocfilehash: bcc5f11afbecac8fe63935f3401dd3e2d767e8aa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-the-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a><span data-ttu-id="83d56-103">Azure Otomasyonu DSC Mobility hizmetiyle VM çoğaltması için dağıtma</span><span class="sxs-lookup"><span data-stu-id="83d56-103">Deploy the Mobility service with Azure Automation DSC for replication of VM</span></span>
<span data-ttu-id="83d56-104">Operations Management Suite biz kapsamlı yedekleme ve iş sürekliliği planınızın bir parçası olarak kullanabileceğiniz olağanüstü durum kurtarma çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="83d56-104">In Operations Management Suite, we provide you with a comprehensive backup and disaster recovery solution that you can use as part of your business continuity plan.</span></span>

<span data-ttu-id="83d56-105">Biz bu gezisine Hyper-V ile birlikte Hyper-V çoğaltma kullanılarak başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="83d56-105">We started this journey together with Hyper-V by using Hyper-V Replica.</span></span> <span data-ttu-id="83d56-106">Ancak biz müşteriler kendi bulut birden fazla hiper ve platformlar olduğundan heterojen Kurulum desteklemek için genişletilen.</span><span class="sxs-lookup"><span data-stu-id="83d56-106">But we have expanded to support a heterogeneous setup because customers have multiple hypervisors and platforms in their clouds.</span></span>

<span data-ttu-id="83d56-107">VMware iş yükleri ve/veya fiziksel sunucuları bugün çalıştırıyorsanız, yönetim sunucusu tüm Azure Site Recovery bileşenlerini Azure Hedefinizi olduğunda, Azure ile iletişim ve veri çoğaltmayı düzenlemek için ortamınızda çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="83d56-107">If you are running VMware workloads and/or physical servers today, a management server runs all of the Azure Site Recovery components in your environment to handle the communication and data replication with Azure, when Azure is your destination.</span></span>

## <a name="deploy-the-site-recovery-mobility-service-by-using-automation-dsc"></a><span data-ttu-id="83d56-108">Automation DSC kullanarak Site Recovery Mobility hizmeti dağıtma</span><span class="sxs-lookup"><span data-stu-id="83d56-108">Deploy the Site Recovery Mobility service by using Automation DSC</span></span>
<span data-ttu-id="83d56-109">Bu yönetim sunucusu yaptığı bir hızlı dökümünü yaparak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="83d56-109">Let's start by doing a quick breakdown of what this management server does.</span></span>

<span data-ttu-id="83d56-110">Yönetim sunucusu, çeşitli sunucu rolleri çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="83d56-110">The management server runs several server roles.</span></span> <span data-ttu-id="83d56-111">Bu roller, biri *yapılandırma*, hangi iletişimi düzenler ve veri çoğaltma ve kurtarma işlemlerini yönetir.</span><span class="sxs-lookup"><span data-stu-id="83d56-111">One of these roles is *configuration*, which coordinates communication and manages data replication and recovery processes.</span></span>

<span data-ttu-id="83d56-112">Ayrıca, *işlem* rol çoğaltma ağ geçidi olarak davranır.</span><span class="sxs-lookup"><span data-stu-id="83d56-112">In addition, the *process* role acts as a replication gateway.</span></span> <span data-ttu-id="83d56-113">Bu rolü korumalı kaynak makinelerden çoğaltma verilerini alıp, önbelleğe alma, sıkıştırma ve şifreleme iyileştirir ve Azure depolama hesabı için gönderir.</span><span class="sxs-lookup"><span data-stu-id="83d56-113">This role receives replication data from protected source machines, optimizes it with caching, compression, and encryption, and then sends it to an Azure storage account.</span></span> <span data-ttu-id="83d56-114">İşlev işlem rolü için ayrıca Mobility hizmetinin korunan makinelere göndermeli ve VMware vm'lerinin otomatik bulma gerçekleştirmek için biridir.</span><span class="sxs-lookup"><span data-stu-id="83d56-114">One of the functions for the process role is also to push installation of the Mobility service to protected machines and perform automatic discovery of VMware VMs.</span></span>

<span data-ttu-id="83d56-115">Varsa, adlı bir azure'dan *ana hedef* rolü, bu işlemin bir parçası olarak çoğaltma verileri işleyecek.</span><span class="sxs-lookup"><span data-stu-id="83d56-115">If there's a failback from Azure, the *master target* role will handle the replication data as part of this operation.</span></span>

<span data-ttu-id="83d56-116">Korumalı makineler için biz Bel *Mobility hizmeti*.</span><span class="sxs-lookup"><span data-stu-id="83d56-116">For the protected machines, we rely on the *Mobility service*.</span></span> <span data-ttu-id="83d56-117">Bu bileşen, Azure'a çoğaltmak istediğiniz her makineye (VMware VM veya fiziksel sunucusu) dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="83d56-117">This component is deployed to every machine (VMware VM or physical server) that you want to replicate to Azure.</span></span> <span data-ttu-id="83d56-118">Makinede veri Yazar yakalar ve bunları (işlem rolü) yönetim sunucusuna iletir.</span><span class="sxs-lookup"><span data-stu-id="83d56-118">It captures data writes on the machine and forwards them to the management server (process role).</span></span>

<span data-ttu-id="83d56-119">İş sürekliliği ile ilgilenirken iş yüklerinizi, altyapınızı ve ilgili bileşenleri anlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="83d56-119">When you're dealing with business continuity, it's important to understand your workloads, your infrastructure, and the components involved.</span></span> <span data-ttu-id="83d56-120">Ardından Kurtarma süresi hedefi (RTO) ve kurtarma noktası hedefi (RPO) gereksinimleri karşılayabilir.</span><span class="sxs-lookup"><span data-stu-id="83d56-120">You can then meet the requirements for your recovery time objective (RTO) and recovery point objective (RPO).</span></span> <span data-ttu-id="83d56-121">Bu bağlamda Mobility hizmeti beklediğiniz şekilde iş yüklerinizi korunmasını sağlamak için anahtardır.</span><span class="sxs-lookup"><span data-stu-id="83d56-121">In this context, the Mobility service is key to ensuring that your workloads are protected as you would expect.</span></span>

<span data-ttu-id="83d56-122">Bu nedenle nasıl, iyileştirilmiş bir şekilde, bazı Operations Management Suite bileşenleri Yardım ile güvenilir bir korumalı kurulum olmasını sağlayabilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="83d56-122">So how can you, in an optimized way, ensure that you have a reliable protected setup with help from some Operations Management Suite components?</span></span>

<span data-ttu-id="83d56-123">Bu makalede, emin olmak için Azure Otomasyonu istenen durum yapılandırması (DSC), Site Recovery ile birlikte nasıl kullanabileceğinize bir örnek sağlar:</span><span class="sxs-lookup"><span data-stu-id="83d56-123">This article provides an example of how you can use Azure Automation Desired State Configuration (DSC), together with Site Recovery, to ensure that:</span></span>

* <span data-ttu-id="83d56-124">Mobility hizmeti ve Azure VM aracısını korumak istediğiniz Windows makineler dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="83d56-124">The Mobility service and Azure VM agent are deployed to the Windows machines that you want to protect.</span></span>
* <span data-ttu-id="83d56-125">Çoğaltma hedefi Azure olduğunda Mobility hizmeti ve Azure VM Aracısı her zaman çalışır.</span><span class="sxs-lookup"><span data-stu-id="83d56-125">The Mobility service and Azure VM agent are always running when Azure is the replication target.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83d56-126">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="83d56-126">Prerequisites</span></span>
* <span data-ttu-id="83d56-127">Gerekli Kurulum depolamak için bir depo</span><span class="sxs-lookup"><span data-stu-id="83d56-127">A repository to store the required setup</span></span>
* <span data-ttu-id="83d56-128">Yönetim sunucusu ile kaydetmek için gerekli parolayı depolamak için bir depo</span><span class="sxs-lookup"><span data-stu-id="83d56-128">A repository to store the required passphrase to register with the management server</span></span>

  > [!NOTE]
  > <span data-ttu-id="83d56-129">Her yönetim sunucusu için benzersiz bir parola oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="83d56-129">A unique passphrase is generated for each management server.</span></span> <span data-ttu-id="83d56-130">Birden çok yönetim sunucusu dağıtmak için kullanacaksanız, doğru parolayı passphrase.txt dosyasında depolanır olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="83d56-130">If you are going to deploy multiple management servers, you have to ensure that the correct passphrase is stored in the passphrase.txt file.</span></span>
  >
  >
* <span data-ttu-id="83d56-131">Windows Management Framework (WMF) koruma (Automation DSC gereksinimini) için etkinleştirmek istediğiniz makinelere yüklenen 5.0</span><span class="sxs-lookup"><span data-stu-id="83d56-131">Windows Management Framework (WMF) 5.0 installed on the machines that you want to enable for protection (a requirement for Automation DSC)</span></span>

  > [!NOTE]
  > <span data-ttu-id="83d56-132">WMF 4.0 yüklü olan Windows için DSC makineler kullanmak istiyorsanız, bölümüne bakın. [kullanmak DSC bağlantısı kesilmiş ortamlarda](## Use DSC in disconnected environments).</span><span class="sxs-lookup"><span data-stu-id="83d56-132">If you want to use DSC for Windows machines that have WMF 4.0 installed, see the section [Use DSC in disconnected environments](## Use DSC in disconnected environments).</span></span>
  

<span data-ttu-id="83d56-133">Mobility hizmetinin komut satırından yüklenebilir ve birkaç bağımsız değişken kabul eder.</span><span class="sxs-lookup"><span data-stu-id="83d56-133">The Mobility service can be installed through the command line and accepts several arguments.</span></span> <span data-ttu-id="83d56-134">İşte bu nedenle ikili dosyaları (bunları, kurulumdan ayıkladıktan sonra) sahip ve bunları burada, alabilir bunları DSC Yapılandırması kullanılarak bir yerde depolamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="83d56-134">That’s why you need to have the binaries (after extracting them from your setup) and store them in a place where you can retrieve them by using a DSC configuration.</span></span>

## <a name="step-1-extract-binaries"></a><span data-ttu-id="83d56-135">1. adım: Extract ikili dosyalar</span><span class="sxs-lookup"><span data-stu-id="83d56-135">Step 1: Extract binaries</span></span>
1. <span data-ttu-id="83d56-136">Bu kurulum için gereken dosyaları ayıklamak için yönetim sunucunuzda aşağıdaki dizinine göz atın:</span><span class="sxs-lookup"><span data-stu-id="83d56-136">To extract the files that you need for this setup, browse to the following directory on your management server:</span></span>

    <span data-ttu-id="83d56-137">**\Microsoft azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span><span class="sxs-lookup"><span data-stu-id="83d56-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span></span>

    <span data-ttu-id="83d56-138">Bu klasörde, adlandırılmış bir MSI dosyası görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="83d56-138">In this folder, you should see an MSI file named:</span></span>

    <span data-ttu-id="83d56-139">**Microsoft ASR_UA_version_Windows_GA_date_Release.exe**</span><span class="sxs-lookup"><span data-stu-id="83d56-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span></span>

    <span data-ttu-id="83d56-140">Yükleyici ayıklamak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="83d56-140">Use the following command to extract the installer:</span></span>

    <span data-ttu-id="83d56-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span><span class="sxs-lookup"><span data-stu-id="83d56-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span></span>
2. <span data-ttu-id="83d56-142">Tüm dosyaları seçin ve bir sıkıştırılmış (ZIP) klasöre gönderin.</span><span class="sxs-lookup"><span data-stu-id="83d56-142">Select all files and send them to a compressed (zipped) folder.</span></span>

<span data-ttu-id="83d56-143">Automation DSC kullanarak kurulum mobilite hizmetinin otomatik hale getirmek için gereken ikili dosyalar artık sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="83d56-143">You now have the binaries that you need to automate the setup of the Mobility service by using Automation DSC.</span></span>

### <a name="passphrase"></a><span data-ttu-id="83d56-144">Parola</span><span class="sxs-lookup"><span data-stu-id="83d56-144">Passphrase</span></span>
<span data-ttu-id="83d56-145">Ardından, bu sıkıştırılmış klasörü eklemek istediğiniz yeri belirlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="83d56-145">Next, you need to determine where you want to place this zipped folder.</span></span> <span data-ttu-id="83d56-146">Kurulum için gereken parolayı depolamak için sonraki gösterildiği gibi bir Azure depolama hesabı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83d56-146">You can use an Azure storage account, as shown later, to store the passphrase that you need for the setup.</span></span> <span data-ttu-id="83d56-147">Aracı, sonra Yönetim sunucusu işleminin bir parçası olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="83d56-147">The agent will then register with the management server as part of the process.</span></span>

<span data-ttu-id="83d56-148">Yönetim sunucusu dağıtıldığında aldığınız parolayı bir metin dosyasına passphrase.txt kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="83d56-148">The passphrase that you got when you deployed the management server can be saved to a text file as passphrase.txt.</span></span>

<span data-ttu-id="83d56-149">Daraltılmış klasörü ve parola ayrılmış bir Azure depolama hesabı kapsayıcısında yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="83d56-149">Place both the zipped folder and the passphrase in a dedicated container in the Azure storage account.</span></span>

![Klasör konumu](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

<span data-ttu-id="83d56-151">Bu dosyalar, ağınızdaki bir paylaşımında tutmak tercih ederseniz, bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83d56-151">If you prefer to keep these files on a share on your network, you can do so.</span></span> <span data-ttu-id="83d56-152">Daha sonra kullanacaksınız DSC kaynağı erişimi vardır ve Kurulum ve parola alabilirsiniz emin olmak yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="83d56-152">You just need to ensure that the DSC resource that you will be using later has access and can get the setup and passphrase.</span></span>

## <a name="step-2-create-the-dsc-configuration"></a><span data-ttu-id="83d56-153">2. adım: DSC yapılandırması oluşturma</span><span class="sxs-lookup"><span data-stu-id="83d56-153">Step 2: Create the DSC configuration</span></span>
<span data-ttu-id="83d56-154">Kurulum WMF 5.0 bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="83d56-154">The setup depends on WMF 5.0.</span></span> <span data-ttu-id="83d56-155">Makine başarıyla Otomasyonu DSC aracılığıyla yapılandırmayı uygulamak WMF 5.0 bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="83d56-155">For the machine to successfully apply the configuration through Automation DSC, WMF 5.0 needs to be present.</span></span>

<span data-ttu-id="83d56-156">Aşağıdaki örnek DSC yapılandırma ortamı kullanır:</span><span class="sxs-lookup"><span data-stu-id="83d56-156">The environment uses the following example DSC configuration:</span></span>

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
<span data-ttu-id="83d56-157">Yapılandırma aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="83d56-157">The configuration will do the following:</span></span>

* <span data-ttu-id="83d56-158">Değişkenleri yapılandırma Mobility hizmeti ve Azure VM Aracısı ikili dosyalarının alınacağı söyleyecektir parola alınacağı ve çıktı depolanacağı konumu.</span><span class="sxs-lookup"><span data-stu-id="83d56-158">The variables will tell the configuration where to get the binaries for the Mobility service and the Azure VM agent, where to get the passphrase, and where to store the output.</span></span>
* <span data-ttu-id="83d56-159">Böylece kullanabileceğiniz yapılandırma xPSDesiredStateConfiguration DSC kaynağı alacak `xRemoteFile` depodan dosyalarını indirmek için.</span><span class="sxs-lookup"><span data-stu-id="83d56-159">The configuration will import the xPSDesiredStateConfiguration DSC resource, so that you can use `xRemoteFile` to download the files from the repository.</span></span>
* <span data-ttu-id="83d56-160">Yapılandırma İkili dosyalarını depolamak istediğiniz bir dizin oluşturur.</span><span class="sxs-lookup"><span data-stu-id="83d56-160">The configuration will create a directory where you want to store the binaries.</span></span>
* <span data-ttu-id="83d56-161">Arşiv kaynak dosyaları sıkıştırılmış klasörden ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="83d56-161">The archive resource will extract the files from the zipped folder.</span></span>
* <span data-ttu-id="83d56-162">' % S'paketinin yükleme kaynak Mobility hizmeti UNIFIEDAGENT yükler. EXE yükleyici belirli bağımsız değişkenlere sahip.</span><span class="sxs-lookup"><span data-stu-id="83d56-162">The package Install resource will install the Mobility service from the UNIFIEDAGENT.EXE installer with the specific arguments.</span></span> <span data-ttu-id="83d56-163">(Bağımsız değişkenler oluşturmak değişkenleri ortamınız yansıtacak şekilde değiştirilmesi gerekir.)</span><span class="sxs-lookup"><span data-stu-id="83d56-163">(The variables that construct the arguments need to be changed to reflect your environment.)</span></span>
* <span data-ttu-id="83d56-164">Paket AzureAgent kaynak Azure'da çalışan her VM üzerinde önerilen Azure VM aracısı yükler.</span><span class="sxs-lookup"><span data-stu-id="83d56-164">The package AzureAgent resource will install the Azure VM agent, which is recommended on every VM that runs in Azure.</span></span> <span data-ttu-id="83d56-165">Azure VM aracısı ayrıca, yük devretme sonrasında VM uzantıları eklemek mümkün kılar.</span><span class="sxs-lookup"><span data-stu-id="83d56-165">The Azure VM agent also makes it possible to add extensions to the VM after failover.</span></span>
* <span data-ttu-id="83d56-166">Hizmet kaynağı veya kaynakları ilgili Mobility hizmetlerinin ve Azure Hizmetleri zaman çalıştığını güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="83d56-166">The service resource or resources will ensure that the related Mobility services and the Azure services are always running.</span></span>

<span data-ttu-id="83d56-167">Yapılandırma olarak Kaydet **ASRMobilityService**.</span><span class="sxs-lookup"><span data-stu-id="83d56-167">Save the configuration as **ASRMobilityService**.</span></span>

> [!NOTE]
> <span data-ttu-id="83d56-168">Böylece aracı doğru bağlanır ve doğru parolayı kullanacağı gerçek yönetim sunucusu yansıtacak şekilde CSIP yapılandırmanızda değiştirmek unutmayın.</span><span class="sxs-lookup"><span data-stu-id="83d56-168">Remember to replace the CSIP in your configuration to reflect the actual management server, so that the agent will be connected correctly and will use the correct passphrase.</span></span>
>
>

## <a name="step-3-upload-to-automation-dsc"></a><span data-ttu-id="83d56-169">3. adım: Automation DSC karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="83d56-169">Step 3: Upload to Automation DSC</span></span>
<span data-ttu-id="83d56-170">Yaptığınız DSC yapılandırması gerekli bir DSC kaynakları Modülü (xPSDesiredStateConfiguration) alacağı için DSC yapılandırması karşıya yüklemeden önce otomasyon modülü içeri aktarmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="83d56-170">Because the DSC configuration that you made will import a required DSC resource module (xPSDesiredStateConfiguration), you need to import that module in Automation before you upload the DSC configuration.</span></span>

<span data-ttu-id="83d56-171">Otomasyon hesabınızda oturum açın, Gözat **varlıklar** > **modülleri**, tıklatıp **Gözat galeri**.</span><span class="sxs-lookup"><span data-stu-id="83d56-171">Sign in to your Automation account, browse to **Assets** > **Modules**, and click **Browse Gallery**.</span></span>

<span data-ttu-id="83d56-172">Modül için burada arama ve hesabınıza aktarın.</span><span class="sxs-lookup"><span data-stu-id="83d56-172">Here you can search for the module and import it to your account.</span></span>

![İçeri aktarma modülü](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

<span data-ttu-id="83d56-174">Bu bitirdikten sonra makinenize yüklü Azure Resource Manager modüllerini sahip olduğu gidin ve yeni oluşturulan DSC yapılandırması içeri aktarmak için devam edin.</span><span class="sxs-lookup"><span data-stu-id="83d56-174">When you finish this, go to your machine where you have the Azure Resource Manager modules installed and proceed to import the newly created DSC configuration.</span></span>

### <a name="import-cmdlets"></a><span data-ttu-id="83d56-175">İçeri aktarma cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="83d56-175">Import cmdlets</span></span>
<span data-ttu-id="83d56-176">PowerShell'de, Azure aboneliğinizde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="83d56-176">In PowerShell, sign in to your Azure subscription.</span></span> <span data-ttu-id="83d56-177">Automation hesabı bilgilerinizi bir değişkende yakalamak ve ortamınızı yansıtmak üzere cmdlet'leri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="83d56-177">Modify the cmdlets to reflect your environment and capture your Automation account information in a variable:</span></span>

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

<span data-ttu-id="83d56-178">Yapılandırma, aşağıdaki cmdlet'i kullanarak Automation DSC karşıya yükle:</span><span class="sxs-lookup"><span data-stu-id="83d56-178">Upload the configuration to Automation DSC by using the following cmdlet:</span></span>

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-the-configuration-in-automation-dsc"></a><span data-ttu-id="83d56-179">Automation DSC yapılandırmasını derleme</span><span class="sxs-lookup"><span data-stu-id="83d56-179">Compile the configuration in Automation DSC</span></span>
<span data-ttu-id="83d56-180">Ardından, onu düğümlerine kaydetmek başlayabilmeniz Automation DSC yapılandırmasını derleme gerekir.</span><span class="sxs-lookup"><span data-stu-id="83d56-180">Next, you need to compile the configuration in Automation DSC, so that you can start to register nodes to it.</span></span> <span data-ttu-id="83d56-181">Aşağıdaki cmdlet'i çalıştırarak elde:</span><span class="sxs-lookup"><span data-stu-id="83d56-181">You achieve that by running the following cmdlet:</span></span>

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

<span data-ttu-id="83d56-182">Barındırılan DSC çekme hizmet yapılandırmasını temel olarak dağıtıyorsunuz için bu işlem birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="83d56-182">This can take a few minutes, because you're basically deploying the configuration to the hosted DSC pull service.</span></span>

<span data-ttu-id="83d56-183">Yapılandırma derledikten sonra PowerShell'i (Get-AzureRmAutomationDscCompilationJob) kullanarak veya kullanarak iş bilgilerini alabilir [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="83d56-183">After you compile the configuration, you can retrieve the job information by using PowerShell (Get-AzureRmAutomationDscCompilationJob) or by using the [Azure portal](https://portal.azure.com/).</span></span>

![İş alma](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

<span data-ttu-id="83d56-185">Şimdi başarıyla yayımlandı ve Automation DSC, DSC yapılandırması karşıya.</span><span class="sxs-lookup"><span data-stu-id="83d56-185">You have now successfully published and uploaded your DSC configuration to Automation DSC.</span></span>

## <a name="step-4-onboard-machines-to-automation-dsc"></a><span data-ttu-id="83d56-186">4. adım: Automation DSC yerleşik makinelere</span><span class="sxs-lookup"><span data-stu-id="83d56-186">Step 4: Onboard machines to Automation DSC</span></span>
> [!NOTE]
> <span data-ttu-id="83d56-187">Bu senaryo Tamamlanıyor önkoşulları Windows makinelerinizi WMF en son sürümüyle güncelleştirilir biridir.</span><span class="sxs-lookup"><span data-stu-id="83d56-187">One of the prerequisites for completing this scenario is that your Windows machines are updated with the latest version of WMF.</span></span> <span data-ttu-id="83d56-188">Karşıdan yükleyip, platformlar için doğru sürümünü yüklemek [Yükleme Merkezi'nden](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="83d56-188">You can download and install the correct version for your platform from the [Download Center](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>
>
>

<span data-ttu-id="83d56-189">Düğümleriniz için uygulayacağınız DSC için şimdi bir metaconfig oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="83d56-189">You will now create a metaconfig for DSC that you will apply to your nodes.</span></span> <span data-ttu-id="83d56-190">Bu başarılı olması için uç nokta URL'sini ve azure'da seçili Automation hesabınız için birincil anahtarınızı almak gerekir.</span><span class="sxs-lookup"><span data-stu-id="83d56-190">To succeed with this, you need to retrieve the endpoint URL and the primary key for your selected Automation account in Azure.</span></span> <span data-ttu-id="83d56-191">Bu değerleri altında bulabilirsiniz **anahtarları** üzerinde **tüm ayarları** Otomasyon hesabı dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="83d56-191">You can find these values under **Keys** on the **All settings** blade for the Automation account.</span></span>

![Anahtar değerleri](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

<span data-ttu-id="83d56-193">Bu örnekte, Site Recovery kullanarak korumak istediğiniz bir Windows Server 2012 R2 fiziksel sunucu vardır.</span><span class="sxs-lookup"><span data-stu-id="83d56-193">In this example, you have a Windows Server 2012 R2 physical server that you want to protect by using Site Recovery.</span></span>

### <a name="check-for-any-pending-file-rename-operations-in-the-registry"></a><span data-ttu-id="83d56-194">Kayıt defterindeki dosya yeniden adlandırma işlemleri beklemedeki denetle</span><span class="sxs-lookup"><span data-stu-id="83d56-194">Check for any pending file rename operations in the registry</span></span>
<span data-ttu-id="83d56-195">Automation DSC noktayla sunucu ilişkilendirilecek başlamadan önce tüm bekleyen kayıt defteri dosyasını yeniden adlandırma işlemleri için denetlemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="83d56-195">Before you start to associate the server with the Automation DSC endpoint, we recommend that you check for any pending file rename operations in the registry.</span></span> <span data-ttu-id="83d56-196">Bekleyen bir yeniden başlatma nedeniyle tamamlama Kurulum yasaklayabilir.</span><span class="sxs-lookup"><span data-stu-id="83d56-196">They might prohibit the setup from finishing due to a pending reboot.</span></span>

<span data-ttu-id="83d56-197">Hiçbir yeniden başlatma bekleniyor sunucuda olduğunu doğrulamak için aşağıdaki cmdlet'i çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="83d56-197">Run the following cmdlet to verify that there’s no pending reboot on the server:</span></span>

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
<span data-ttu-id="83d56-198">Bu boş gösterir, devam etmek için Tamam demektir.</span><span class="sxs-lookup"><span data-stu-id="83d56-198">If this shows empty, you are OK to proceed.</span></span> <span data-ttu-id="83d56-199">Aksi durumda, bu sunucunun bir bakım penceresi sırasında yeniden tarafından bulundurmalıdır.</span><span class="sxs-lookup"><span data-stu-id="83d56-199">If not, you should address this by rebooting the server during a maintenance window.</span></span>

<span data-ttu-id="83d56-200">Sunucuda yapılandırmayı uygulamak için PowerShell Tümleşik komut dosyası ortamı (ISE) başlatın ve aşağıdaki komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="83d56-200">To apply the configuration on the server, start the PowerShell Integrated Scripting Environment (ISE) and run the following script.</span></span> <span data-ttu-id="83d56-201">Bu, Automation DSC hizmete kaydolmak ve özel yapılandırma (ASRMobilityService.localhost) almak için yerel Configuration Manager altyapısı yönlendiren aslında bir DSC yerel yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="83d56-201">This is essentially a DSC local configuration that will instruct the Local Configuration Manager engine to register with the Automation DSC service and retrieve the specific configuration (ASRMobilityService.localhost).</span></span>

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

<span data-ttu-id="83d56-202">Bu yapılandırma, kendisini Otomasyonu DSC'ye kaydetmek yerel Configuration Manager altyapısı neden olur.</span><span class="sxs-lookup"><span data-stu-id="83d56-202">This configuration will cause the Local Configuration Manager engine to register itself with Automation DSC.</span></span> <span data-ttu-id="83d56-203">Ayrıca, altyapı nasıl çalışacağını, yapılandırma değişikliklerini (ApplyAndAutoCorrect) ise ne yapmanız gerektiğini ve yeniden başlatma gerekli olduğunda nasıl, yapılandırmaya devam etmek belirler.</span><span class="sxs-lookup"><span data-stu-id="83d56-203">It will also determine how the engine should operate, what it should do if there's a configuration drift (ApplyAndAutoCorrect), and how it should proceed with the configuration if a reboot is required.</span></span>

<span data-ttu-id="83d56-204">Automation DSC ile kaydetmek, sonra bu komut dosyasını çalıştırın, düğüm başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="83d56-204">After you run this script, the node should start to register with Automation DSC.</span></span>

![Düğüm kayıt işlemi sürüyor](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

<span data-ttu-id="83d56-206">Azure portalına geri dönün, yeni kayıtlı düğümü Portalı'nda artık göründükten görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83d56-206">If you go back to the Azure portal, you can see that the newly registered node has now appeared in the portal.</span></span>

![Portalı'nda kayıtlı düğümü](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

<span data-ttu-id="83d56-208">Sunucuda, düğüm doğru şekilde kaydedildiğini doğrulamak için aşağıdaki PowerShell cmdlet'ini çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="83d56-208">On the server, you can run the following PowerShell cmdlet to verify that the node has been registered correctly:</span></span>

```powershell
Get-DscLocalConfigurationManager
```

<span data-ttu-id="83d56-209">Yapılandırma çekilen ve sunucuya uyguladıktan sonra aşağıdaki cmdlet'i çalıştırarak doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="83d56-209">After the configuration has been pulled and applied to the server, you can verify this by running the following cmdlet:</span></span>

```powershell
Get-DscConfigurationStatus
```

<span data-ttu-id="83d56-210">Sunucu yapılandırmasını başarıyla çekilen çıkış gösterir:</span><span class="sxs-lookup"><span data-stu-id="83d56-210">The output shows that the server has successfully pulled its configuration:</span></span>

![Çıktı](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

<span data-ttu-id="83d56-212">Ayrıca, Mobility hizmeti Kurulumu konumunda bulunan kendi günlük sahip *SystemDrive*\ProgramData\ASRSetupLogs.</span><span class="sxs-lookup"><span data-stu-id="83d56-212">In addition, the Mobility service setup has its own log that can be found at *SystemDrive*\ProgramData\ASRSetupLogs.</span></span>

<span data-ttu-id="83d56-213">İşte bu kadar.</span><span class="sxs-lookup"><span data-stu-id="83d56-213">That’s it.</span></span> <span data-ttu-id="83d56-214">Şimdi başarıyla dağıtılan ve Site Recovery kullanarak korumak istediğiniz makinede Mobility hizmeti kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="83d56-214">You have now successfully deployed and registered the Mobility service on the machine that you want to protect by using Site Recovery.</span></span> <span data-ttu-id="83d56-215">DSC gerekli hizmetler her zaman çalışır durumda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="83d56-215">DSC will make sure that the required services are always running.</span></span>

![Başarılı dağıtım](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

<span data-ttu-id="83d56-217">Yönetim sunucusu başarılı dağıtım algılandıktan sonra korumayı yapılandırın ve Site Recovery kullanarak makinesinde çoğaltmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="83d56-217">After the management server detects the successful deployment, you can configure protection and enable replication on the machine by using Site Recovery.</span></span>

## <a name="use-dsc-in-disconnected-environments"></a><span data-ttu-id="83d56-218">Bağlantısı kesilmiş ortamlarda DSC kullanın</span><span class="sxs-lookup"><span data-stu-id="83d56-218">Use DSC in disconnected environments</span></span>
<span data-ttu-id="83d56-219">Makinelerinizi Internet'e bağlı değilseniz hala dağıtmak ve korumak istediğiniz iş yükünü Mobility hizmeti yapılandırmak için DSC üzerinde güvenebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83d56-219">If your machines aren’t connected to the Internet, you can still rely on DSC to deploy and configure the Mobility service on the workloads that you want to protect.</span></span>

<span data-ttu-id="83d56-220">Temelde Automation DSC'den alma aynı yetenekleri sağlamak için ortamınızdaki kendi DSC istek sunucusuyla örneği.</span><span class="sxs-lookup"><span data-stu-id="83d56-220">You can instantiate your own DSC pull server in your environment to essentially provide the same capabilities that you get from Automation DSC.</span></span> <span data-ttu-id="83d56-221">Diğer bir deyişle, istemcilerin (kaydedildikten sonra) yapılandırma DSC uç çeker.</span><span class="sxs-lookup"><span data-stu-id="83d56-221">That is, the clients will pull the configuration (after it's registered) to the DSC endpoint.</span></span> <span data-ttu-id="83d56-222">Ancak, yerel olarak veya uzaktan DSC yapılandırması makinelerinize, el ile göndermek için başka bir seçenek değildir.</span><span class="sxs-lookup"><span data-stu-id="83d56-222">However, another option is to manually push the DSC configuration to your machines, either locally or remotely.</span></span>

<span data-ttu-id="83d56-223">Bu örnekte, bilgisayar adı için ek bir parametre yoktur.</span><span class="sxs-lookup"><span data-stu-id="83d56-223">Note that in this example, there's an added parameter for the computer name.</span></span> <span data-ttu-id="83d56-224">Uzak dosyalar, artık korumak istediğiniz makinelere tarafından erişilebilir olması gereken bir uzak paylaşım bulunur.</span><span class="sxs-lookup"><span data-stu-id="83d56-224">The remote files are now located on a remote share that should be accessible by the machines that you want to protect.</span></span> <span data-ttu-id="83d56-225">Komut dosyasının sonuna yapılandırma enacts ve DSC yapılandırması hedef bilgisayara uygulanan başlar.</span><span class="sxs-lookup"><span data-stu-id="83d56-225">The end of the script enacts the configuration and then starts to apply the DSC configuration to the target computer.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="83d56-226">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="83d56-226">Prerequisites</span></span>
<span data-ttu-id="83d56-227">XPSDesiredStateConfiguration PowerShell Modülü yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="83d56-227">Make sure that the xPSDesiredStateConfiguration PowerShell module is installed.</span></span> <span data-ttu-id="83d56-228">WMF 5.0 yüklü olduğu Windows makineler için aşağıdaki cmdlet'i hedef makinelerde çalıştırarak xPSDesiredStateConfiguration modülü yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="83d56-228">For Windows machines where WMF 5.0 is installed, you can install the xPSDesiredStateConfiguration module by running the following cmdlet on the target machines:</span></span>

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

<span data-ttu-id="83d56-229">Ayrıca, indirin ve WMF 4.0 yüklü Windows makineler dağıtmanız gerektiğinde modülü kaydedin.</span><span class="sxs-lookup"><span data-stu-id="83d56-229">You can also download and save the module in case you need to distribute it to Windows machines that have WMF 4.0.</span></span> <span data-ttu-id="83d56-230">Bu cmdlet, PowerShellGet (WMF 5.0) mevcut olduğu bir makinede çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="83d56-230">Run this cmdlet on a machine where PowerShellGet (WMF 5.0) is present:</span></span>

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

<span data-ttu-id="83d56-231">Ayrıca WMF 4.0 için emin [Windows 8.1 güncelleştirmesi KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) makinelerde yüklü.</span><span class="sxs-lookup"><span data-stu-id="83d56-231">Also for WMF 4.0, ensure that the [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) is installed on the machines.</span></span>

<span data-ttu-id="83d56-232">Aşağıdaki yapılandırma WMF 5.0 ve WMF 4.0 sahip Windows makinelerine iletilmesini:</span><span class="sxs-lookup"><span data-stu-id="83d56-232">The following configuration can be pushed to Windows machines that have WMF 5.0 and WMF 4.0:</span></span>

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

<span data-ttu-id="83d56-233">Şirket ağınıza Automation DSC'den alabilirsiniz yetenekleri taklit etmek üzere kendi DSC çekme sunucusuna örneği oluşturmak istiyorsanız, bkz: [DSC web çekme sunucusu kurma](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="83d56-233">If you want to instantiate your own DSC pull server on your corporate network to mimic the capabilities that you can get from Automation DSC, see [Setting up a DSC web pull server](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span></span>

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="83d56-234">İsteğe bağlı: DSC yapılandırması bir Azure Resource Manager şablonu kullanarak dağıtın</span><span class="sxs-lookup"><span data-stu-id="83d56-234">Optional: Deploy a DSC configuration by using an Azure Resource Manager template</span></span>
<span data-ttu-id="83d56-235">Bu makalede nasıl otomatik olarak Mobility hizmeti ve Azure VM Aracısı--dağıtmak ve sağlamak için kendi DSC yapılandırması korumak istediğiniz makinelerde çalıştırılan oluşturabileceğiniz üzerinde odaklı.</span><span class="sxs-lookup"><span data-stu-id="83d56-235">This article has focused on how you can create your own DSC configuration to automatically deploy the Mobility service and the Azure VM Agent--and ensure that they are running on the machines that you want to protect.</span></span> <span data-ttu-id="83d56-236">Biz de bu DSC yapılandırması için yeni veya var olan bir Azure Otomasyonu hesabı dağıtacağınız bir Azure Resource Manager şablonu vardır.</span><span class="sxs-lookup"><span data-stu-id="83d56-236">We also have an Azure Resource Manager template that will deploy this DSC configuration to a new or existing Azure Automation account.</span></span> <span data-ttu-id="83d56-237">Şablon değişkenleri ortamınız için içerecek Otomasyon varlıkları oluşturmak için giriş parametreleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="83d56-237">The template will use input parameters to create Automation assets that will contain the variables for your environment.</span></span>

<span data-ttu-id="83d56-238">Şablon dağıttıktan sonra yalnızca 4. adım giriş için bu kılavuzdaki makinelerinizi başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83d56-238">After you deploy the template, you can simply refer to step 4 in this guide to onboard your machines.</span></span>

<span data-ttu-id="83d56-239">Şablon aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="83d56-239">The template will do the following:</span></span>

1. <span data-ttu-id="83d56-240">Var olan Otomasyon hesabını kullanabilir veya yeni bir tane oluşturun</span><span class="sxs-lookup"><span data-stu-id="83d56-240">Use an existing Automation account or create a new one</span></span>
2. <span data-ttu-id="83d56-241">Giriş parametreleri için alın:</span><span class="sxs-lookup"><span data-stu-id="83d56-241">Take input parameters for:</span></span>
   * <span data-ttu-id="83d56-242">ASRRemoteFile--Mobility hizmeti Kurulumu depoladığınız konumu</span><span class="sxs-lookup"><span data-stu-id="83d56-242">ASRRemoteFile--the location where you have stored the Mobility service setup</span></span>
   * <span data-ttu-id="83d56-243">ASRPassphrase--passphrase.txt dosyasını depoladığınız konumu</span><span class="sxs-lookup"><span data-stu-id="83d56-243">ASRPassphrase--the location where you have stored the passphrase.txt file</span></span>
   * <span data-ttu-id="83d56-244">ASRCSEndpoint--yönetim sunucunuzun IP adresi</span><span class="sxs-lookup"><span data-stu-id="83d56-244">ASRCSEndpoint--the IP address of your management server</span></span>
3. <span data-ttu-id="83d56-245">XPSDesiredStateConfiguration PowerShell modülünü içeri aktarın</span><span class="sxs-lookup"><span data-stu-id="83d56-245">Import the xPSDesiredStateConfiguration PowerShell module</span></span>
4. <span data-ttu-id="83d56-246">Oluşturma ve DSC yapılandırmasını derleme</span><span class="sxs-lookup"><span data-stu-id="83d56-246">Create and compile the DSC configuration</span></span>

<span data-ttu-id="83d56-247">Makinelerinizi koruması için ekleme başlayabilmeniz için yukarıdaki adımların tümünü doğru sırada gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="83d56-247">All the preceding steps will happen in the right order, so that you can start onboarding your machines for protection.</span></span>

<span data-ttu-id="83d56-248">Şablon dağıtımı için yönergeler bulunan [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span><span class="sxs-lookup"><span data-stu-id="83d56-248">The template, with instructions for deployment, is located on [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span></span>

<span data-ttu-id="83d56-249">PowerShell kullanarak şablonu dağıtma:</span><span class="sxs-lookup"><span data-stu-id="83d56-249">Deploy the template by using PowerShell:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="83d56-250">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="83d56-250">Next steps</span></span>
<span data-ttu-id="83d56-251">Mobility hizmeti aracıları dağıttıktan sonra şunları yapabilirsiniz [çoğaltmayı etkinleştirme](site-recovery-vmware-to-azure.md) sanal makineler için.</span><span class="sxs-lookup"><span data-stu-id="83d56-251">After you deploy the Mobility service agents, you can [enable replication](site-recovery-vmware-to-azure.md) for the virtual machines.</span></span>
