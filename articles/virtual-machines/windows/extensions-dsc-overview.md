---
title: "aaaDesired durum yapılandırması Azure genel bakış | Microsoft Docs"
description: "PowerShell istenen durum yapılandırması için hello Microsoft Azure uzantısı işleyici kullanarak genel bakış. Önkoşullar, mimari, cmdlet'leri dahil olmak üzere..."
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: bbacbc93-1e7b-4611-a3ec-e3320641f9ba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 01/09/2017
ms.author: zachal
ms.openlocfilehash: b0337a2f1124f35e5e40c1478bd7530427e59d44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-desired-state-configuration-extension-handler"></a><span data-ttu-id="4285b-104">Giriş toohello Azure istenen durum yapılandırması uzantısı işleyicisi</span><span class="sxs-lookup"><span data-stu-id="4285b-104">Introduction toohello Azure Desired State Configuration extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="4285b-105">Hello Azure VM aracısı ve ilişkili uzantıları hello Microsoft Azure altyapı hizmetleri parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="4285b-105">hello Azure VM Agent and associated Extensions are part of hello Microsoft Azure Infrastructure Services.</span></span> <span data-ttu-id="4285b-106">VM uzantıları hello VM işlevlerini genişletmek ve çeşitli VM yönetim işlemlerini basitleştirmek yazılım bileşenleridir.</span><span class="sxs-lookup"><span data-stu-id="4285b-106">VM Extensions are software components that extend hello VM functionality and simplify various VM management operations.</span></span> <span data-ttu-id="4285b-107">Örneğin, hello VMAccess uzantısını kullanılan tooreset yöneticinin parola bulunabilir, veya özel komut dosyası hello uzantısı kullanılan tooexecute hello VM üzerinde bir komut dosyası olabilir.</span><span class="sxs-lookup"><span data-stu-id="4285b-107">For example, hello VMAccess extension can be used tooreset an administrator's password, or hello Custom Script extension can be used tooexecute a script on hello VM.</span></span>

<span data-ttu-id="4285b-108">Bu makalede hello PowerShell istenen durum yapılandırması (DSC) uzantısı hello Azure PowerShell SDK'ın bir parçası olarak Azure VM'ler için tanıtılır.</span><span class="sxs-lookup"><span data-stu-id="4285b-108">This article introduces hello PowerShell Desired State Configuration (DSC) Extension for Azure VMs as part of hello Azure PowerShell SDK.</span></span> <span data-ttu-id="4285b-109">Yeni cmdlet'leri tooupload ve PowerShell DSC yapılandırması hello PowerShell DSC uzantısı ile etkin bir Azure VM uygulamak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4285b-109">You can use new cmdlets tooupload and apply a PowerShell DSC configuration on an Azure VM enabled with hello PowerShell DSC extension.</span></span> <span data-ttu-id="4285b-110">Merhaba PowerShell DSC uzantısı çağrılarının PowerShell DSC tooenact hello içine hello VM DSC yapılandırmasını aldı.</span><span class="sxs-lookup"><span data-stu-id="4285b-110">hello PowerShell DSC extension calls into PowerShell DSC tooenact hello received DSC configuration on hello VM.</span></span> <span data-ttu-id="4285b-111">Bu işlevsellik, hello Azure portal da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4285b-111">This functionality is also available through hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4285b-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4285b-112">Prerequisites</span></span>
<span data-ttu-id="4285b-113">**Yerel makine** toointeract ile Merhaba Azure VM uzantısı, Azure PowerShell SDK hello veya her iki hello Azure portal toouse gerekir.</span><span class="sxs-lookup"><span data-stu-id="4285b-113">**Local machine** toointeract with hello Azure VM extension, you need toouse either hello Azure portal or hello Azure PowerShell SDK.</span></span> 

<span data-ttu-id="4285b-114">**Konuk Aracısı** hello hello DSC yapılandırması tarafından yapılandırılan bir Azure VM toobe Windows Management Framework (WMF) 4.0 veya 5.0 destekleyen bir işletim sistemi gerekir.</span><span class="sxs-lookup"><span data-stu-id="4285b-114">**Guest Agent** hello Azure VM that is configured by hello DSC configuration needs toobe an OS that supports either Windows Management Framework (WMF) 4.0 or 5.0.</span></span> <span data-ttu-id="4285b-115">Merhaba tam desteklenen işletim sistemi sürümlerinin listesi hello bulunabilir [DSC uzantısı sürüm geçmişi](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span><span class="sxs-lookup"><span data-stu-id="4285b-115">hello full list of supported OS versions can be found at hello [DSC Extension Version History](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span></span>

## <a name="terms-and-concepts"></a><span data-ttu-id="4285b-116">Terimleri ve kavramları</span><span class="sxs-lookup"><span data-stu-id="4285b-116">Terms and concepts</span></span>
<span data-ttu-id="4285b-117">Bu kılavuz kavramları aşağıdaki hello bilindiğini varsayar:</span><span class="sxs-lookup"><span data-stu-id="4285b-117">This guide presumes familiarity with hello following concepts:</span></span>

<span data-ttu-id="4285b-118">Yapılandırma - DSC yapılandırma belgesi.</span><span class="sxs-lookup"><span data-stu-id="4285b-118">Configuration - A DSC configuration document.</span></span> 

<span data-ttu-id="4285b-119">Düğümü - DSC yapılandırması için hedef.</span><span class="sxs-lookup"><span data-stu-id="4285b-119">Node - A target for a DSC configuration.</span></span> <span data-ttu-id="4285b-120">Bu belgede "düğümü" her zaman tooan Azure VM ifade eder.</span><span class="sxs-lookup"><span data-stu-id="4285b-120">In this document, "node" always refers tooan Azure VM.</span></span>

<span data-ttu-id="4285b-121">Yapılandırma verilerini - bir .psd1 dosya ortam verileri içeren bir yapılandırma için</span><span class="sxs-lookup"><span data-stu-id="4285b-121">Configuration Data - A .psd1 file containing environmental data for a configuration</span></span>

## <a name="architectural-overview"></a><span data-ttu-id="4285b-122">Mimari genel bakış</span><span class="sxs-lookup"><span data-stu-id="4285b-122">Architectural overview</span></span>
<span data-ttu-id="4285b-123">hello Azure VM Aracısı framework toodeliver Hello Azure DSC uzantısı kullanır, yürürlüğe ve DSC yapılandırmaları Azure Vm'lerinde çalıştırılan hakkında rapor oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4285b-123">hello Azure DSC extension uses hello Azure VM Agent framework toodeliver, enact, and report on DSC configurations running on Azure VMs.</span></span> <span data-ttu-id="4285b-124">Azure portal parametreleri kümesini hello Azure PowerShell SDK veya hello aracılığıyla sağlanan ve Hello DSC uzantısı en az bir yapılandırma belgesini içeren bir .zip dosyası bekler.</span><span class="sxs-lookup"><span data-stu-id="4285b-124">hello DSC extension expects a .zip file containing at least a configuration document, and a set of parameters provided either through hello Azure PowerShell SDK or through hello Azure portal.</span></span>

<span data-ttu-id="4285b-125">Merhaba uzantısı hello için ilk kez çağrıldığında, bir yükleme işlemi çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="4285b-125">When hello extension is called for hello first time, it runs an installation process.</span></span> <span data-ttu-id="4285b-126">Bu işlem mantığı aşağıdaki hello kullanarak hello Windows Management Framework (WMF) sürümünü yükler:</span><span class="sxs-lookup"><span data-stu-id="4285b-126">This process installs a version of hello Windows Management Framework (WMF) using hello following logic:</span></span>

1. <span data-ttu-id="4285b-127">Hello Azure VM işletim sistemi Windows Server 2016 ise, hiçbir işlem yapılmadı.</span><span class="sxs-lookup"><span data-stu-id="4285b-127">If hello Azure VM OS is Windows Server 2016, no action is taken.</span></span> <span data-ttu-id="4285b-128">Windows Server 2016 yüklü PowerShell'in en son sürümünü hello zaten var.</span><span class="sxs-lookup"><span data-stu-id="4285b-128">Windows Server 2016 already has hello latest version of PowerShell installed.</span></span>
2. <span data-ttu-id="4285b-129">Merhaba, `wmfVersion` özelliği belirtildi, hello VM'in işletim sistemiyle uyumlu olmadığı sürece bu hello WMF sürümü yüklenir.</span><span class="sxs-lookup"><span data-stu-id="4285b-129">If hello `wmfVersion` property is specified, that version of hello WMF is installed unless it is incompatible with hello VM's OS.</span></span>
3. <span data-ttu-id="4285b-130">Öyle değilse `wmfVersion` özelliği belirtildi, hello son geçerli sürümü hello WMF yüklendi.</span><span class="sxs-lookup"><span data-stu-id="4285b-130">If no `wmfVersion` property is specified, hello latest applicable version of hello WMF is installed.</span></span>

<span data-ttu-id="4285b-131">Merhaba WMF yeniden başlatma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4285b-131">Installation of hello WMF requires a reboot.</span></span> <span data-ttu-id="4285b-132">Yeniden başlatmanın ardından hello uzantısı hello belirtilen hello .zip dosyası indirir `modulesUrl` özelliği.</span><span class="sxs-lookup"><span data-stu-id="4285b-132">After reboot, hello extension downloads hello .zip file specified in hello `modulesUrl` property.</span></span> <span data-ttu-id="4285b-133">Bu konum Azure blob depolama alanına ise, bir SAS belirteci hello belirtilebilir `sasToken` özelliği tooaccess hello dosya.</span><span class="sxs-lookup"><span data-stu-id="4285b-133">If this location is in Azure blob storage, a SAS token can be specified in hello `sasToken` property tooaccess hello file.</span></span> <span data-ttu-id="4285b-134">Merhaba .zip indirilir ve açılmış sonra tanımlanan yapılandırması işlevi hello `configurationFunction` toogenerate hello MOF dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4285b-134">After hello .zip is downloaded and unpacked, hello configuration function defined in `configurationFunction` is run toogenerate hello MOF file.</span></span> <span data-ttu-id="4285b-135">Merhaba uzantısı sonra çalışır `Start-DscConfiguration -Force` üzerinde oluşturulan hello MOF dosyası.</span><span class="sxs-lookup"><span data-stu-id="4285b-135">hello extension then runs `Start-DscConfiguration -Force` on hello generated MOF file.</span></span> <span data-ttu-id="4285b-136">Merhaba uzantısı çıkış yakalar ve geri toohello Azure durum kanal yazar.</span><span class="sxs-lookup"><span data-stu-id="4285b-136">hello extension captures output and writes it back out toohello Azure Status Channel.</span></span> <span data-ttu-id="4285b-137">Üzerinde hello bu noktasından DSC LCM'yi izleme ve düzeltme normal olarak işler.</span><span class="sxs-lookup"><span data-stu-id="4285b-137">From this point on, hello DSC LCM handles monitoring and correction as normal.</span></span> 

## <a name="powershell-cmdlets"></a><span data-ttu-id="4285b-138">PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="4285b-138">PowerShell cmdlets</span></span>
<span data-ttu-id="4285b-139">PowerShell cmdlet'leri Azure Resource Manager ile kullanılabilir veya Klasik dağıtım modeli toopackage Merhaba, yayımlama ve DSC uzantısı dağıtımlarını izleme.</span><span class="sxs-lookup"><span data-stu-id="4285b-139">PowerShell cmdlets can be used with Azure Resource Manager or hello classic deployment model toopackage, publish, and monitor DSC extension deployments.</span></span> <span data-ttu-id="4285b-140">Merhaba listelenen aşağıdaki cmdlet'leri hello Klasik dağıtım modülleri olsa da, "Azure" "AzureRm" toouse hello Azure Resource Manager modeli ile değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="4285b-140">hello following cmdlets listed are hello classic deployment modules, but "Azure" can be replaced with "AzureRm" toouse hello Azure Resource Manager model.</span></span> <span data-ttu-id="4285b-141">Örneğin, `Publish-AzureVMDscConfiguration` kullanır hello Klasik dağıtım modeli, burada `Publish-AzureRmVMDscConfiguration` Azure Kaynak Yöneticisi'ni kullanır.</span><span class="sxs-lookup"><span data-stu-id="4285b-141">For example,  `Publish-AzureVMDscConfiguration` uses hello classic deployment model, where `Publish-AzureRmVMDscConfiguration` uses Azure Resource Manager.</span></span> 

<span data-ttu-id="4285b-142">`Publish-AzureVMDscConfiguration`bir yapılandırma dosyasında alır, bağımlı DSC kaynakları için tarar ve hello yapılandırması ve DSC kaynakları gerekli tooenact hello yapılandırması içeren bir .zip dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4285b-142">`Publish-AzureVMDscConfiguration` takes in a configuration file, scans it for dependent DSC resources, and creates a .zip file containing hello configuration and DSC resources needed tooenact hello configuration.</span></span> <span data-ttu-id="4285b-143">Hello kullanarak yerel olarak hello paketi oluşturabilirsiniz `-ConfigurationArchivePath` parametresi.</span><span class="sxs-lookup"><span data-stu-id="4285b-143">It can also create hello package locally using hello `-ConfigurationArchivePath` parameter.</span></span> <span data-ttu-id="4285b-144">Aksi takdirde hello .zip dosyası tooAzure blob depolama yayımlar ve bir SAS belirteci ile güvenliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="4285b-144">Otherwise, it publishes hello .zip file tooAzure blob storage and secures it with a SAS token.</span></span>

<span data-ttu-id="4285b-145">Bu cmdlet ile oluşturulan hello .zip dosyası hello hello arşiv klasörü kökünde hello .ps1 yapılandırma komut dosyası vardır.</span><span class="sxs-lookup"><span data-stu-id="4285b-145">hello .zip file created by this cmdlet has hello .ps1 configuration script at hello root of hello archive folder.</span></span> <span data-ttu-id="4285b-146">Kaynaklar hello arşiv klasöre yerleştirilen hello modülü klasörünü sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4285b-146">Resources have hello module folder placed in hello archive folder.</span></span> 

<span data-ttu-id="4285b-147">`Set-AzureVMDscExtension`bir VM yapılandırması nesnesine Hello PowerShell DSC uzantısı tarafından gerekli hello ayarları yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="4285b-147">`Set-AzureVMDscExtension` injects hello settings needed by hello PowerShell DSC extension into a VM configuration object.</span></span> <span data-ttu-id="4285b-148">Merhaba Klasik dağıtım modelinde hello VM değişiklikleri uygulanan tooan Azure VM olmalıdır ile `Update-AzureVM`.</span><span class="sxs-lookup"><span data-stu-id="4285b-148">In hello classic deployment model, hello VM changes must be applied tooan Azure VM with `Update-AzureVM`.</span></span> 

<span data-ttu-id="4285b-149">`Get-AzureVMDscExtension`belirli bir VM'nin Hello DSC uzantı durumunu alır.</span><span class="sxs-lookup"><span data-stu-id="4285b-149">`Get-AzureVMDscExtension` retrieves hello DSC extension status of a particular VM.</span></span> 

<span data-ttu-id="4285b-150">`Get-AzureVMDscExtensionStatus`Merhaba DSC uzantısı işleyici tarafından kamulaştırılmış hello DSC yapılandırması Hello durumunu alır.</span><span class="sxs-lookup"><span data-stu-id="4285b-150">`Get-AzureVMDscExtensionStatus` retrieves hello status of hello DSC configuration enacted by hello DSC extension handler.</span></span> <span data-ttu-id="4285b-151">Bu eylem, bir tek VM veya grup Vm'lere üzerinde gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="4285b-151">This action can be performed on a single VM, or group of VMs.</span></span>

<span data-ttu-id="4285b-152">`Remove-AzureVMDscExtension`Merhaba uzantısı işleyici belirli bir sanal makineden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="4285b-152">`Remove-AzureVMDscExtension` removes hello extension handler from a given virtual machine.</span></span> <span data-ttu-id="4285b-153">Bu cmdlet mu **değil** hello yapılandırmasını kaldırmak, hello WMF kaldırma veya hello sanal makine uygulanan hello ayarlarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4285b-153">This cmdlet does **not** remove hello configuration, uninstall hello WMF, or change hello applied settings on hello virtual machine.</span></span> <span data-ttu-id="4285b-154">Yalnızca hello uzantısı işleyici de kaldırır.</span><span class="sxs-lookup"><span data-stu-id="4285b-154">It only removes hello extension handler.</span></span> 

<span data-ttu-id="4285b-155">**ASM ve Azure Resource Manager cmdlet'lerini temel farklılıkları**</span><span class="sxs-lookup"><span data-stu-id="4285b-155">**Key differences in ASM and Azure Resource Manager cmdlets**</span></span>

* <span data-ttu-id="4285b-156">Azure Resource Manager cmdlet'lerini zaman uyumlu.</span><span class="sxs-lookup"><span data-stu-id="4285b-156">Azure Resource Manager cmdlets are synchronous.</span></span> <span data-ttu-id="4285b-157">ASM cmdlet'leri zaman uyumsuzdur.</span><span class="sxs-lookup"><span data-stu-id="4285b-157">ASM cmdlets are asynchronous.</span></span>
* <span data-ttu-id="4285b-158">ResourceGroupName, VMName, ArchiveStorageAccountName, sürüm ve konum tüm gerekli Azure Kaynak Yöneticisi'nde parametreleridir.</span><span class="sxs-lookup"><span data-stu-id="4285b-158">ResourceGroupName, VMName, ArchiveStorageAccountName, Version, and Location are all required parameters in Azure Resource Manager.</span></span>
* <span data-ttu-id="4285b-159">ArchiveResourceGroupName yeni bir isteğe bağlı parametre için Azure Resource Manager ' dir.</span><span class="sxs-lookup"><span data-stu-id="4285b-159">ArchiveResourceGroupName is a new optional parameter for Azure Resource Manager.</span></span> <span data-ttu-id="4285b-160">Merhaba sanal makinenin oluşturulduğu tooa farklı kaynak hello bir gruptan depolama hesabınıza ait olduğunda, bu parametre belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4285b-160">You can specify this parameter when your storage account belongs tooa different resource group than hello one where hello virtual machine is created.</span></span>
* <span data-ttu-id="4285b-161">Azure Kaynak Yöneticisi'nde ArchiveBlobName ConfigurationArchive çağrılır</span><span class="sxs-lookup"><span data-stu-id="4285b-161">ConfigurationArchive is called ArchiveBlobName in Azure Resource Manager</span></span>
* <span data-ttu-id="4285b-162">Kapsayıcı adı Azure Kaynak Yöneticisi'nde ArchiveContainerName çağrılır</span><span class="sxs-lookup"><span data-stu-id="4285b-162">ContainerName is called ArchiveContainerName in Azure Resource Manager</span></span>
* <span data-ttu-id="4285b-163">Azure Kaynak Yöneticisi'nde ArchiveStorageEndpointSuffix StorageEndpointSuffix çağrılır</span><span class="sxs-lookup"><span data-stu-id="4285b-163">StorageEndpointSuffix is called ArchiveStorageEndpointSuffix in Azure Resource Manager</span></span>
* <span data-ttu-id="4285b-164">Merhaba otomatik güncelleştirme anahtar tooAzure Resource Manager tooenable otomatik hello uzantısı işleyici toohello en son sürüm olarak ve kullanılabilir olduğunda güncelleştirme eklendi.</span><span class="sxs-lookup"><span data-stu-id="4285b-164">hello AutoUpdate switch has been added tooAzure Resource Manager tooenable automatic updating of hello extension handler toohello latest version as and when it is available.</span></span> <span data-ttu-id="4285b-165">Bu parametre hello olası toocause sahip Not VM WMF yayımlanan hello yeni bir sürümü olduğunda hello üzerinde yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="4285b-165">Note this parameter has hello potential toocause reboots on hello VM when a new version of hello WMF is released.</span></span> 

## <a name="azure-portal-functionality"></a><span data-ttu-id="4285b-166">Azure portal işlevi</span><span class="sxs-lookup"><span data-stu-id="4285b-166">Azure portal functionality</span></span>
<span data-ttu-id="4285b-167">Tooa VM göz atın.</span><span class="sxs-lookup"><span data-stu-id="4285b-167">Browse tooa VM.</span></span> <span data-ttu-id="4285b-168">Ayarlar altında "Uzantıları." Genel tıklatın -></span><span class="sxs-lookup"><span data-stu-id="4285b-168">Under Settings -> General click "Extensions."</span></span> <span data-ttu-id="4285b-169">Yeni bir bölme oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4285b-169">A new pane is created.</span></span> <span data-ttu-id="4285b-170">"Ekle"'yi tıklatın ve PowerShell DSC seçin.</span><span class="sxs-lookup"><span data-stu-id="4285b-170">Click "Add" and select PowerShell DSC.</span></span>

<span data-ttu-id="4285b-171">Merhaba portal giriş gerekir.</span><span class="sxs-lookup"><span data-stu-id="4285b-171">hello portal needs input.</span></span>
<span data-ttu-id="4285b-172">**Yapılandırma modülleri veya komut dosyası**: Bu alan zorunludur.</span><span class="sxs-lookup"><span data-stu-id="4285b-172">**Configuration Modules or Script**: This field is mandatory.</span></span> <span data-ttu-id="4285b-173">Bir yapılandırma betiğini içeren bir .ps1 dosyası ya da bir .ps1 yapılandırma betiğini hello kökündeki ve hello .zip içinde modülü klasörlerdeki tüm bağımlı kaynaklarla bir .zip dosyası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4285b-173">Requires a .ps1 file containing a configuration script, or a .zip file with a .ps1 configuration script at hello root, and all dependent resources in module folders within hello .zip.</span></span> <span data-ttu-id="4285b-174">Merhaba ile oluşturulan `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` hello Azure PowerShell SDK'sını dahil cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="4285b-174">It can be created with hello `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` cmdlet included in hello Azure PowerShell SDK.</span></span> <span data-ttu-id="4285b-175">Merhaba .zip dosyası tarafından bir SAS belirteci güvenli, kullanıcı blob depolama alanına yüklenir.</span><span class="sxs-lookup"><span data-stu-id="4285b-175">hello .zip file is uploaded into your user blob storage secured by a SAS token.</span></span> 

<span data-ttu-id="4285b-176">**Yapılandırma verileri PSD1 dosyası**: Bu alan isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4285b-176">**Configuration Data PSD1 File**: This field is optional.</span></span> <span data-ttu-id="4285b-177">Yapılandırmanızı .psd1 yapılandırma veri dosyası gerektiriyorsa, bu alan tooselect kullanın ve tooyour kullanıcı blob depolama burada onu güvenli bir SAS belirteci tarafından karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4285b-177">If your configuration requires a configuration data file in .psd1, use this field tooselect it and upload it tooyour user blob storage, where it is secured by a SAS token.</span></span> 

<span data-ttu-id="4285b-178">**Yapılandırma, modül adı**: .ps1 dosyaları birden çok yapılandırma işlevleri sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="4285b-178">**Module-Qualified Name of Configuration**: .ps1 files can have multiple configuration functions.</span></span> <span data-ttu-id="4285b-179">Ardından hello yapılandırma .ps1 betiği Hello adını girin bir '\' ve hello yapılandırma işlevinin hello adı.</span><span class="sxs-lookup"><span data-stu-id="4285b-179">Enter hello name of hello configuration .ps1 script followed by a  '\' and hello name of hello configuration function.</span></span> <span data-ttu-id="4285b-180">Örneğin, hello adı "configuration.ps1".ps1 komut dosyanız varsa ve "IisInstall" Merhaba yapılandırmadır girersiniz:`configuration.ps1\IisInstall`</span><span class="sxs-lookup"><span data-stu-id="4285b-180">For example, if your .ps1 script has hello name "configuration.ps1", and hello configuration is "IisInstall", you would enter: `configuration.ps1\IisInstall`</span></span>

<span data-ttu-id="4285b-181">**Yapılandırma değişkenleri**: hello yapılandırma işlevi bağımsız değişken alıyorsa, bunları burada hello biçiminde girin `argumentName1=value1,argumentName2=value2`.</span><span class="sxs-lookup"><span data-stu-id="4285b-181">**Configuration Arguments**: If hello configuration function takes arguments, enter them in here in hello format `argumentName1=value1,argumentName2=value2`.</span></span> <span data-ttu-id="4285b-182">Bu biçim PowerShell cmdlet'lerini veya Resource Manager şablonları ile yapılandırma bağımsız değişkenleri nasıl kabul daha farklı bir biçim olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="4285b-182">Note this format is a different format than how configuration arguments are accepted through PowerShell cmdlets or Resource Manager templates.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="4285b-183">Başlarken</span><span class="sxs-lookup"><span data-stu-id="4285b-183">Getting started</span></span>
<span data-ttu-id="4285b-184">Hello Azure DSC uzantısı DSC yapılandırma belgelerde alır ve Azure Vm'lerinde enacts.</span><span class="sxs-lookup"><span data-stu-id="4285b-184">hello Azure DSC extension takes in DSC configuration documents and enacts them on Azure VMs.</span></span> <span data-ttu-id="4285b-185">Bir yapılandırma basit bir örnek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4285b-185">A simple example of a configuration follows.</span></span> <span data-ttu-id="4285b-186">Yerel olarak, "IisInstall.ps1" kaydedin:</span><span class="sxs-lookup"><span data-stu-id="4285b-186">Save it locally as "IisInstall.ps1":</span></span>

```powershell
configuration IISInstall 
{ 
    node "localhost"
    { 
        WindowsFeature IIS 
        { 
            Ensure = "Present" 
            Name = "Web-Server"                       
        } 
    } 
}
```

<span data-ttu-id="4285b-187">VM üzerinde hello adımları yer hello IisInstall.ps1 komut dosyası izleyen hello belirtilen, hello yapılandırma yürütün ve geri durumu rapor.</span><span class="sxs-lookup"><span data-stu-id="4285b-187">hello following steps place hello IisInstall.ps1 script on hello specified VM, execute hello configuration, and report back on status.</span></span>
###<a name="classic-model"></a><span data-ttu-id="4285b-188">Klasik modeli</span><span class="sxs-lookup"><span data-stu-id="4285b-188">Classic model</span></span>
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish hello configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set hello VM toorun hello DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update hello configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a><span data-ttu-id="4285b-189">Azure Resource Manager modeli</span><span class="sxs-lookup"><span data-stu-id="4285b-189">Azure Resource Manager model</span></span>

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish hello configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set hello VM toorun hello DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a><span data-ttu-id="4285b-190">Günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="4285b-190">Logging</span></span>
<span data-ttu-id="4285b-191">Günlükleri yerleştirilir:</span><span class="sxs-lookup"><span data-stu-id="4285b-191">Logs are placed in:</span></span>

<span data-ttu-id="4285b-192">C:\WindowsAzure\Logs\Plugins\Microsoft.PowerShell.DSC\[sürüm numarası]</span><span class="sxs-lookup"><span data-stu-id="4285b-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Version Number]</span></span>

## <a name="next-steps"></a><span data-ttu-id="4285b-193">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4285b-193">Next steps</span></span>
<span data-ttu-id="4285b-194">PowerShell DSC hakkında daha fazla bilgi için [hello PowerShell Belge Merkezi ziyaret](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="4285b-194">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="4285b-195">Merhaba inceleyin [hello DSC uzantısı için Azure Resource Manager şablonu](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4285b-195">Examine hello [Azure Resource Manager template for hello DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="4285b-196">PowerShell DSC ile yönetebileceğiniz toofind işlevsellikler [hello PowerShell Galerisi Gözat](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) daha fazla DSC kaynakları için.</span><span class="sxs-lookup"><span data-stu-id="4285b-196">toofind additional functionality you can manage with PowerShell DSC, [browse hello PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

<span data-ttu-id="4285b-197">Yapılandırmaları hassas parametreleri geçirme hakkında daha fazla bilgi için bkz: [yönetmek hello DSC uzantısı işleyici ile güvenli kimlik bilgileri](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4285b-197">For details on passing sensitive parameters into configurations, see [Manage credentials securely with hello DSC extension handler](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

