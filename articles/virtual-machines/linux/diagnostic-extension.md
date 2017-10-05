---
title: "Azure işlem - Linux tanılama uzantısını | Microsoft Docs"
description: "Azure Linux tanılama uzantısını (ölçümleri toplamak ve Linux Azure'da çalışan Vm'lerden gelen olayları günlüğe LAD) yapılandırmak nasıl."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 525d706bd709ae72f2dca1c21e06db533ccf32b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="use-linux-diagnostic-extension-to-monitor-metrics-and-logs"></a><span data-ttu-id="08711-103">Ölçümleri ve günlükleri izlemek için Linux tanılama uzantısını kullanın</span><span class="sxs-lookup"><span data-stu-id="08711-103">Use Linux Diagnostic Extension to monitor metrics and logs</span></span>

<span data-ttu-id="08711-104">Bu belgede sürüm 3.0 ve Linux tanılama uzantısı'nın daha yeni açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="08711-104">This document describes version 3.0 and newer of the Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08711-105">2.3 ve eski sürümü hakkında daha fazla bilgi için bkz: [bu belgeyi](./classic/diagnostic-extension-v2.md).</span><span class="sxs-lookup"><span data-stu-id="08711-105">For information about version 2.3 and older, see [this document](./classic/diagnostic-extension-v2.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="08711-106">Giriş</span><span class="sxs-lookup"><span data-stu-id="08711-106">Introduction</span></span>

<span data-ttu-id="08711-107">Linux tanılama uzantısını kullanıcı İzleyicisi sistem durumu Microsoft Azure üzerinde çalışan bir Linux VM yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="08711-107">The Linux Diagnostic Extension helps a user monitor the health of a Linux VM running on Microsoft Azure.</span></span> <span data-ttu-id="08711-108">Aşağıdaki özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="08711-108">It has the following capabilities:</span></span>

* <span data-ttu-id="08711-109">Sanal makineden sistem performans ölçümleri toplar ve bunları belirtilen depolama hesabı belirli bir tabloda depolar.</span><span class="sxs-lookup"><span data-stu-id="08711-109">Collects system performance metrics from the VM and stores them in a specific table in a designated storage account.</span></span>
* <span data-ttu-id="08711-110">Syslog günlüğü olaylarını alır ve bunları belirtilen depolama hesabında belirli bir tabloda depolar.</span><span class="sxs-lookup"><span data-stu-id="08711-110">Retrieves log events from syslog and stores them in a specific table in the designated storage account.</span></span>
* <span data-ttu-id="08711-111">Kullanıcıların, toplanan ve karşıya veri ölçümlerini özelleştirme olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="08711-111">Enables users to customize the data metrics that are collected and uploaded.</span></span>
* <span data-ttu-id="08711-112">Syslog tesisler ve toplanan ve karşıya olayların önem düzeyleri özelleştirmek kullanıcıların sağlar.</span><span class="sxs-lookup"><span data-stu-id="08711-112">Enables users to customize the syslog facilities and severity levels of events that are collected and uploaded.</span></span>
* <span data-ttu-id="08711-113">Belirtilen günlük dosyalarını karşıya yüklemek için atanmış depolama tablosu olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="08711-113">Enables users to upload specified log files to a designated storage table.</span></span>
* <span data-ttu-id="08711-114">Rastgele EventHub uç noktaları ve atanan depolama hesabındaki BLOB JSON biçimli ölçümleri ve günlük olayları göndermeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="08711-114">Supports sending metrics and log events to arbitrary EventHub endpoints and JSON-formatted blobs in the designated storage account.</span></span>

<span data-ttu-id="08711-115">Bu uzantı, hem Azure dağıtım modelleri ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="08711-115">This extension works with both Azure deployment models.</span></span>

## <a name="installing-the-extension-in-your-vm"></a><span data-ttu-id="08711-116">VM uzantısı yükleme</span><span class="sxs-lookup"><span data-stu-id="08711-116">Installing the extension in your VM</span></span>

<span data-ttu-id="08711-117">Azure PowerShell cmdlet'lerini, Azure CLI betikleri veya Azure dağıtım şablonları kullanarak bu uzantı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08711-117">You can enable this extension by using the Azure PowerShell cmdlets, Azure CLI scripts, or Azure deployment templates.</span></span> <span data-ttu-id="08711-118">Daha fazla bilgi için bkz: [uzantıları özelliklerinin](./extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="08711-118">For more information, see [Extensions Features](./extensions-features.md).</span></span>

<span data-ttu-id="08711-119">Azure Portalı'nı etkinleştirmek veya LAD 3.0 yapılandırmak için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="08711-119">The Azure portal cannot be used to enable or configure LAD 3.0.</span></span> <span data-ttu-id="08711-120">Bunun yerine, yükler ve sürüm 2.3 yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="08711-120">Instead, it installs and configures version 2.3.</span></span> <span data-ttu-id="08711-121">Azure portal grafikleri ve uyarıları her iki sürümünün de uzantısı verilerle çalışır.</span><span class="sxs-lookup"><span data-stu-id="08711-121">Azure portal graphs and alerts work with data from both versions of the extension.</span></span>

<span data-ttu-id="08711-122">Bu yükleme yönergeleri ve [indirilebilir örnek yapılandırma](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) LAD 3.0 yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="08711-122">These installation instructions and a [downloadable sample configuration](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configure LAD 3.0 to:</span></span>

* <span data-ttu-id="08711-123">yakalama ve LAD 2.3 tarafından sağlanan ölçümler aynı depolama;</span><span class="sxs-lookup"><span data-stu-id="08711-123">capture and store the same metrics as were provided by LAD 2.3;</span></span>
* <span data-ttu-id="08711-124">dosya sistemi ölçümleri, LAD 3.0 için yeni yararlı bir dizi yakalama;</span><span class="sxs-lookup"><span data-stu-id="08711-124">capture a useful set of file system metrics, new to LAD 3.0;</span></span>
* <span data-ttu-id="08711-125">Yakalama LAD 2.3 ile etkin varsayılan syslog toplama;</span><span class="sxs-lookup"><span data-stu-id="08711-125">capture the default syslog collection enabled by LAD 2.3;</span></span>
* <span data-ttu-id="08711-126">Grafik ve VM ölçümleri uyarmak için Azure portal deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="08711-126">enable the Azure portal experience for charting and alerting on VM metrics.</span></span>

<span data-ttu-id="08711-127">İndirilebilir yapılandırma yalnızca bir örnektir; kendi gereksinimlerinize uyacak şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="08711-127">The downloadable configuration is just an example; modify it to suit your own needs.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="08711-128">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="08711-128">Prerequisites</span></span>

* <span data-ttu-id="08711-129">**Azure Linux Aracısı sürüm 2.2.0 veya daha sonra**.</span><span class="sxs-lookup"><span data-stu-id="08711-129">**Azure Linux Agent version 2.2.0 or later**.</span></span> <span data-ttu-id="08711-130">Çoğu Azure VM Linux galeri görüntüleri sürüm 2.2.7 dahil etmek veya daha sonra.</span><span class="sxs-lookup"><span data-stu-id="08711-130">Most Azure VM Linux gallery images include version 2.2.7 or later.</span></span> <span data-ttu-id="08711-131">Çalıştırma `/usr/sbin/waagent -version` VM'de yüklü sürümünü onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="08711-131">Run `/usr/sbin/waagent -version` to confirm the version installed on the VM.</span></span> <span data-ttu-id="08711-132">VM Konuk aracısının daha eski bir sürümünü çalıştırıyorsa, izleyin [bu yönergeleri](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="08711-132">If the VM is running an older version of the guest agent, follow [these instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) to update it.</span></span>
* <span data-ttu-id="08711-133">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="08711-133">**Azure CLI**.</span></span> <span data-ttu-id="08711-134">[Azure CLI 2.0 ayarlama](https://docs.microsoft.com/cli/azure/install-azure-cli) makinenizde ortamı.</span><span class="sxs-lookup"><span data-stu-id="08711-134">[Set up the Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) environment on your machine.</span></span>
* <span data-ttu-id="08711-135">Zaten yoksa wget komutu: çalıştırmak `sudo apt-get install wget`.</span><span class="sxs-lookup"><span data-stu-id="08711-135">The wget command, if you don't already have it: Run `sudo apt-get install wget`.</span></span>
* <span data-ttu-id="08711-136">Var olan bir Azure aboneliği ve içerdiği verileri depolamak için varolan bir depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="08711-136">An existing Azure subscription and an existing storage account within it to store the data.</span></span>

### <a name="sample-installation"></a><span data-ttu-id="08711-137">Örnek yükleme</span><span class="sxs-lookup"><span data-stu-id="08711-137">Sample installation</span></span>

<span data-ttu-id="08711-138">İlk üç satırını doğru parametreleri doldurun, sonra da kök olarak bu betiği yürütün:</span><span class="sxs-lookup"><span data-stu-id="08711-138">Fill in the correct parameters on the first three lines, then execute this script as root:</span></span>

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login to Azure first before anything else
az login

# Select the subscription containing the storage account
az account set --subscription <your_azure_subscription_id>

# Download the sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build the VM resource ID. Replace storage account name and resource ID in the public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build the protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure to install and enable the extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

<span data-ttu-id="08711-139">Örnek yapılandırmasını ve içeriğini, URL'sini olan değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="08711-139">The URL for the sample configuration, and its contents, are subject to change.</span></span> <span data-ttu-id="08711-140">Portal ayarlarını JSON dosyasının bir kopyasını indirin ve gereksinimlerinize göre özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="08711-140">Download a copy of the portal settings JSON file and customize it for your needs.</span></span> <span data-ttu-id="08711-141">Tüm Şablonları ya da Otomasyon, oluşturmak, her zaman bu URL'yi indirmek yerine kendi kopyanızı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="08711-141">Any templates or automation you construct should use your own copy, rather than downloading that URL each time.</span></span>

### <a name="updating-the-extension-settings"></a><span data-ttu-id="08711-142">Uzantı ayarları güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="08711-142">Updating the extension settings</span></span>

<span data-ttu-id="08711-143">Korumalı veya genel ayarları değiştirdikten sonra bunları VM'ye aynı komutu çalıştırarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="08711-143">After you've changed your Protected or Public settings, deploy them to the VM by running the same command.</span></span> <span data-ttu-id="08711-144">Herhangi bir şey ayarlarında değiştirdiyseniz, güncelleştirilmiş ayarlar uzantısı gönderilir.</span><span class="sxs-lookup"><span data-stu-id="08711-144">If anything changed in the settings, the updated settings are sent to the extension.</span></span> <span data-ttu-id="08711-145">LAD yapılandırmasını yeniden yükler ve kendisini yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="08711-145">LAD reloads the configuration and restarts itself.</span></span>

### <a name="migration-from-previous-versions-of-the-extension"></a><span data-ttu-id="08711-146">Uzantı eski sürümlerinden geçiş</span><span class="sxs-lookup"><span data-stu-id="08711-146">Migration from previous versions of the extension</span></span>

<span data-ttu-id="08711-147">Uzantısı'nın en son sürüm **3.0**.</span><span class="sxs-lookup"><span data-stu-id="08711-147">The latest version of the extension is **3.0**.</span></span> <span data-ttu-id="08711-148">**Eski sürümlerini (2.x) kullanım dışıdır ve ve 31 Temmuz 2018 sonrasında yayımdan**.</span><span class="sxs-lookup"><span data-stu-id="08711-148">**Any old versions (2.x) are deprecated and may be unpublished on or after July 31, 2018**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08711-149">Bu uzantı uzantısı yapılandırma için önemli değişiklikler tanıtır.</span><span class="sxs-lookup"><span data-stu-id="08711-149">This extension introduces breaking changes to the configuration of the extension.</span></span> <span data-ttu-id="08711-150">Bu tür bir değişiklik uzantısı güvenliğini geliştirmek üzere yapılmıştır; Sonuç olarak, geriye dönük uyumluluk 2.x ile korunmasını değil.</span><span class="sxs-lookup"><span data-stu-id="08711-150">One such change was made to improve the security of the extension; as a result, backwards compatibility with 2.x could not be maintained.</span></span> <span data-ttu-id="08711-151">Ayrıca, bu uzantı için uzantı yayımcı yayımcı 2.x sürümleri için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="08711-151">Also, the Extension Publisher for this extension is different than the publisher for the 2.x versions.</span></span>
>
> <span data-ttu-id="08711-152">Bu yeni sürümü uzantısı 2.x geçirmek için (altında eski Yayımcı adı) eski uzantısını Kaldır, sonra uzantısı 3 sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="08711-152">To migrate from 2.x to this new version of the extension, you must uninstall the old extension (under the old publisher name), then install version 3 of the extension.</span></span>

<span data-ttu-id="08711-153">Öneriler:</span><span class="sxs-lookup"><span data-stu-id="08711-153">Recommendations:</span></span>

* <span data-ttu-id="08711-154">Uzantı etkin otomatik alt sürüm yükseltme işlemine yükleyin.</span><span class="sxs-lookup"><span data-stu-id="08711-154">Install the extension with automatic minor version upgrade enabled.</span></span>
  * <span data-ttu-id="08711-155">Azure XPLAT CLI veya Powershell ile uzantısı yüklüyorsanız, Klasik dağıtım modeli VM'ler, '3.*' sürüm olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="08711-155">On classic deployment model VMs, specify '3.*' as the version if you are installing the extension through Azure XPLAT CLI or Powershell.</span></span>
  * <span data-ttu-id="08711-156">Sanal makineleri üzerinde Azure Resource Manager dağıtım modeli, dahil ' "olan": true' VM Dağıtım şablonu olarak.</span><span class="sxs-lookup"><span data-stu-id="08711-156">On Azure Resource Manager deployment model VMs, include '"autoUpgradeMinorVersion": true' in the VM deployment template.</span></span>
* <span data-ttu-id="08711-157">Yeni/farklı bir depolama hesabı LAD 3.0 için kullanın.</span><span class="sxs-lookup"><span data-stu-id="08711-157">Use a new/different storage account for LAD 3.0.</span></span> <span data-ttu-id="08711-158">Bir hesap sorunlu paylaşımı olun birkaç küçük uyumsuzlukları LAD 2.3 LAD 3.0 arasındaki vardır:</span><span class="sxs-lookup"><span data-stu-id="08711-158">There are several small incompatibilities between LAD 2.3 and LAD 3.0 that make sharing an account troublesome:</span></span>
  * <span data-ttu-id="08711-159">LAD 3.0 syslog olayları farklı bir ada sahip bir tablo olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="08711-159">LAD 3.0 stores syslog events in a table with a different name.</span></span>
  * <span data-ttu-id="08711-160">CounterSpecifier dizeleri için `builtin` ölçümleri farklı LAD 3. 0 '.</span><span class="sxs-lookup"><span data-stu-id="08711-160">The counterSpecifier strings for `builtin` metrics differ in LAD 3.0.</span></span>

## <a name="protected-settings"></a><span data-ttu-id="08711-161">Korumalı ayarları</span><span class="sxs-lookup"><span data-stu-id="08711-161">Protected settings</span></span>

<span data-ttu-id="08711-162">Bu yapılandırma bilgileri kümesi genel görünümünde, örneğin, depolama kimlik korunması gereken hassas bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="08711-162">This set of configuration information contains sensitive information that should be protected from public view, for example, storage credentials.</span></span> <span data-ttu-id="08711-163">Bu ayarlar için iletilen ve uzantısı ile şifrelenmiş biçimde depolanır.</span><span class="sxs-lookup"><span data-stu-id="08711-163">These settings are transmitted to and stored by the extension in encrypted form.</span></span>

```json
{
    "storageAccountName" : "the storage account to receive data",
    "storageAccountEndPoint": "the hostname suffix for the cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

<span data-ttu-id="08711-164">Ad</span><span class="sxs-lookup"><span data-stu-id="08711-164">Name</span></span> | <span data-ttu-id="08711-165">Değer</span><span class="sxs-lookup"><span data-stu-id="08711-165">Value</span></span>
---- | -----
<span data-ttu-id="08711-166">storageAccountName</span><span class="sxs-lookup"><span data-stu-id="08711-166">storageAccountName</span></span> | <span data-ttu-id="08711-167">Veri uzantısı tarafından yazılmış depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="08711-167">The name of the storage account in which data is written by the extension.</span></span>
<span data-ttu-id="08711-168">storageAccountEndPoint</span><span class="sxs-lookup"><span data-stu-id="08711-168">storageAccountEndPoint</span></span> | <span data-ttu-id="08711-169">(isteğe bağlı) Depolama hesabının bulunduğu bulut tanımlayan uç noktası.</span><span class="sxs-lookup"><span data-stu-id="08711-169">(optional) The endpoint identifying the cloud in which the storage account exists.</span></span> <span data-ttu-id="08711-170">Bu ayar olmazsa LAD Azure genel bulut için varsayılan olarak `https://core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="08711-170">If this setting is absent, LAD defaults to the Azure public cloud, `https://core.windows.net`.</span></span> <span data-ttu-id="08711-171">Bir depolama hesabı Azure Almanya, Azure kamu ya da Azure Çin'de kullanmak için bu değeri uygun şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="08711-171">To use a storage account in Azure Germany, Azure Government, or Azure China, set this value accordingly.</span></span>
<span data-ttu-id="08711-172">storageAccountSasToken</span><span class="sxs-lookup"><span data-stu-id="08711-172">storageAccountSasToken</span></span> | <span data-ttu-id="08711-173">Bir [hesap SAS belirteci](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) Blob ve tablo hizmeti (`ss='bt'`), kapsayıcılar ve nesneler için geçerlidir (`srt='co'`), hangi verir ekleyin, oluşturmak, liste, güncelleştirme ve yazma izinleri (`sp='acluw'`).</span><span class="sxs-lookup"><span data-stu-id="08711-173">An [Account SAS token](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) for Blob and Table services (`ss='bt'`), applicable to containers and objects (`srt='co'`), which grants add, create, list, update, and write permissions (`sp='acluw'`).</span></span> <span data-ttu-id="08711-174">Yapmak *değil* başında soru işareti (?) içerir.</span><span class="sxs-lookup"><span data-stu-id="08711-174">Do *not* include the leading question-mark (?).</span></span>
<span data-ttu-id="08711-175">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="08711-175">mdsdHttpProxy</span></span> | <span data-ttu-id="08711-176">(isteğe bağlı) Belirtilen depolama hesabına ve uç noktası'na bağlanmak uzantıyı etkinleştirmek için gereken HTTP proxy bilgileri.</span><span class="sxs-lookup"><span data-stu-id="08711-176">(optional) HTTP proxy information needed to enable the extension to connect to the specified storage account and endpoint.</span></span>
<span data-ttu-id="08711-177">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="08711-177">sinksConfig</span></span> | <span data-ttu-id="08711-178">(isteğe bağlı) Alternatif hedefler için ölçümleri ve olayları teslim edilebilir ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="08711-178">(optional) Details of alternative destinations to which metrics and events can be delivered.</span></span> <span data-ttu-id="08711-179">Genişletme tarafından desteklenen her veri havuzu belirli ayrıntılarını izleyen bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="08711-179">The specific details of each data sink supported by the extension are covered in the sections that follow.</span></span>

<span data-ttu-id="08711-180">Azure portalı üzerinden gerekli SAS belirteci kolayca oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08711-180">You can easily construct the required SAS token through the Azure portal.</span></span>

1. <span data-ttu-id="08711-181">Uzantı yazmak için istediğiniz genel amaçlı depolama hesabı seçin</span><span class="sxs-lookup"><span data-stu-id="08711-181">Select the general-purpose storage account to which you want the extension to write</span></span>
1. <span data-ttu-id="08711-182">"Erişim imzası soldaki menüden ayarları bölümünden paylaşılan" seçin</span><span class="sxs-lookup"><span data-stu-id="08711-182">Select "Shared access signature" from the Settings part of the left menu</span></span>
1. <span data-ttu-id="08711-183">Daha önce açıklandığı gibi uygun bölümleri olun</span><span class="sxs-lookup"><span data-stu-id="08711-183">Make the appropriate sections as previously described</span></span>
1. <span data-ttu-id="08711-184">"SAS oluştur" düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="08711-184">Click the "Generate SAS" button.</span></span>

![Görüntü](./media/diagnostic-extension/make_sas.png)

<span data-ttu-id="08711-186">Oluşturulan SAS storageAccountSasToken alana kopyalayın; önde gelen soru işareti kaldırın ("?").</span><span class="sxs-lookup"><span data-stu-id="08711-186">Copy the generated SAS into the storageAccountSasToken field; remove the leading question-mark ("?").</span></span>

### <a name="sinksconfig"></a><span data-ttu-id="08711-187">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="08711-187">sinksConfig</span></span>

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

<span data-ttu-id="08711-188">Bu isteğe bağlı bir bölüm, uzantı topladığı bilgileri gönderdiği ek hedefleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="08711-188">This optional section defines additional destinations to which the extension sends the information it collects.</span></span> <span data-ttu-id="08711-189">"Havuz" dizi her ek veri havuzu için bir nesne içeriyor.</span><span class="sxs-lookup"><span data-stu-id="08711-189">The "sink" array contains an object for each additional data sink.</span></span> <span data-ttu-id="08711-190">"Tür" özniteliği nesnesindeki diğer öznitelikleri belirler.</span><span class="sxs-lookup"><span data-stu-id="08711-190">The "type" attribute determines the other attributes in the object.</span></span>

<span data-ttu-id="08711-191">Öğesi</span><span class="sxs-lookup"><span data-stu-id="08711-191">Element</span></span> | <span data-ttu-id="08711-192">Değer</span><span class="sxs-lookup"><span data-stu-id="08711-192">Value</span></span>
------- | -----
<span data-ttu-id="08711-193">ad</span><span class="sxs-lookup"><span data-stu-id="08711-193">name</span></span> | <span data-ttu-id="08711-194">Bu havuz başka bir uzantı yapılandırmasındaki başvurmak için kullanılan bir dize.</span><span class="sxs-lookup"><span data-stu-id="08711-194">A string used to refer to this sink elsewhere in the extension configuration.</span></span>
<span data-ttu-id="08711-195">type</span><span class="sxs-lookup"><span data-stu-id="08711-195">type</span></span> | <span data-ttu-id="08711-196">Tanımlanan Havuz türü.</span><span class="sxs-lookup"><span data-stu-id="08711-196">The type of sink being defined.</span></span> <span data-ttu-id="08711-197">Diğer değerler, bu tür durumlarda (varsa) belirler.</span><span class="sxs-lookup"><span data-stu-id="08711-197">Determines the other values (if any) in instances of this type.</span></span>

<span data-ttu-id="08711-198">Linux tanılama uzantısını 3.0 sürümünü iki havuz türlerini destekler: EventHub ve JsonBlob.</span><span class="sxs-lookup"><span data-stu-id="08711-198">Version 3.0 of the Linux Diagnostic Extension supports two sink types: EventHub, and JsonBlob.</span></span>

#### <a name="the-eventhub-sink"></a><span data-ttu-id="08711-199">EventHub havuz</span><span class="sxs-lookup"><span data-stu-id="08711-199">The EventHub sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

<span data-ttu-id="08711-200">"SasURL" giriş olay verileri yayımlanması gerekir Hub için SAS belirteci dahil tam URL'yi içerir.</span><span class="sxs-lookup"><span data-stu-id="08711-200">The "sasURL" entry contains the full URL, including SAS token, for the Event Hub to which data should be published.</span></span> <span data-ttu-id="08711-201">LAD Gönder sağlayan bir ilke adlandırma SAS talep gerektirir.</span><span class="sxs-lookup"><span data-stu-id="08711-201">LAD requires a SAS naming a policy that enables the Send claim.</span></span> <span data-ttu-id="08711-202">Örnek:</span><span class="sxs-lookup"><span data-stu-id="08711-202">An example:</span></span>

* <span data-ttu-id="08711-203">Adlı bir olay hub'ları ad alanı oluşturma`contosohub`</span><span class="sxs-lookup"><span data-stu-id="08711-203">Create an Event Hubs namespace called `contosohub`</span></span>
* <span data-ttu-id="08711-204">Bir Event Hub'adlı ad alanı oluşturma`syslogmsgs`</span><span class="sxs-lookup"><span data-stu-id="08711-204">Create an Event Hub in the namespace called `syslogmsgs`</span></span>
* <span data-ttu-id="08711-205">Olay adlı hub'ına bir paylaşılan erişim ilkesi oluşturun `writer` gönderme talep sağlar</span><span class="sxs-lookup"><span data-stu-id="08711-205">Create a Shared access policy on the Event Hub named `writer` that enables the Send claim</span></span>

<span data-ttu-id="08711-206">Bir SAS iyi 1 Ocak 2018 gece yarısı UTC kadar oluşturduysanız sasURL değeri olabilir:</span><span class="sxs-lookup"><span data-stu-id="08711-206">If you created a SAS good until midnight UTC on January 1, 2018, the sasURL value might be:</span></span>

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

<span data-ttu-id="08711-207">Olay hub'ları için SAS belirteci oluşturma hakkında daha fazla bilgi için bkz: [bu web sayfası](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span><span class="sxs-lookup"><span data-stu-id="08711-207">For more information about generating SAS tokens for Event Hubs, see [this web page](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span></span>

#### <a name="the-jsonblob-sink"></a><span data-ttu-id="08711-208">JsonBlob havuz</span><span class="sxs-lookup"><span data-stu-id="08711-208">The JsonBlob sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

<span data-ttu-id="08711-209">JsonBlob havuzuna yönlendirilen verileri BLOB'ları Azure depolama alanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="08711-209">Data directed to a JsonBlob sink is stored in blobs in Azure storage.</span></span> <span data-ttu-id="08711-210">Her örneği LAD blob her saat için her bir havuz adı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="08711-210">Each instance of LAD creates a blob every hour for each sink name.</span></span> <span data-ttu-id="08711-211">Her bir blob her zaman nesne sözdizimsel olarak geçerli bir JSON dizisi içerir.</span><span class="sxs-lookup"><span data-stu-id="08711-211">Each blob always contains a syntactically valid JSON array of object.</span></span> <span data-ttu-id="08711-212">Yeni girişler dizisine otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="08711-212">New entries are atomically added to the array.</span></span> <span data-ttu-id="08711-213">BLOB'ları, havuz olarak aynı ada sahip bir kapsayıcıda depolanır.</span><span class="sxs-lookup"><span data-stu-id="08711-213">Blobs are stored in a container with the same name as the sink.</span></span> <span data-ttu-id="08711-214">Blob kapsayıcı adları için Azure depolama kuralları JsonBlob havuzlarını adları için geçerlidir: küçük harf alfasayısal ASCII karakterler veya tire 3 ile 63 arasında.</span><span class="sxs-lookup"><span data-stu-id="08711-214">The Azure storage rules for blob container names apply to the names of JsonBlob sinks: between 3 and 63 lower-case alphanumeric ASCII characters or dashes.</span></span>

## <a name="public-settings"></a><span data-ttu-id="08711-215">Genel ayarları</span><span class="sxs-lookup"><span data-stu-id="08711-215">Public settings</span></span>

<span data-ttu-id="08711-216">Bu yapı çeşitli bloklarını uzantısı tarafından toplanan bilgiler denetleyen ayarları içerir.</span><span class="sxs-lookup"><span data-stu-id="08711-216">This structure contains various blocks of settings that control the information collected by the extension.</span></span> <span data-ttu-id="08711-217">Her ayar isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="08711-217">Each setting is optional.</span></span> <span data-ttu-id="08711-218">Belirtirseniz `ladCfg`, de belirtmeniz gerekir `StorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="08711-218">If you specify `ladCfg`, you must also specify `StorageAccount`.</span></span>

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "the storage account to receive data",
    "mdsdHttpProxy" : ""
}
```

<span data-ttu-id="08711-219">Öğesi</span><span class="sxs-lookup"><span data-stu-id="08711-219">Element</span></span> | <span data-ttu-id="08711-220">Değer</span><span class="sxs-lookup"><span data-stu-id="08711-220">Value</span></span>
------- | -----
<span data-ttu-id="08711-221">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="08711-221">StorageAccount</span></span> | <span data-ttu-id="08711-222">Veri uzantısı tarafından yazılmış depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="08711-222">The name of the storage account in which data is written by the extension.</span></span> <span data-ttu-id="08711-223">Belirtilen ada olmalıdır [ayarların korumalı](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="08711-223">Must be the same name as is specified in the [Protected settings](#protected-settings).</span></span>
<span data-ttu-id="08711-224">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="08711-224">mdsdHttpProxy</span></span> | <span data-ttu-id="08711-225">(isteğe bağlı) Aynı olarak [ayarların korumalı](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="08711-225">(optional) Same as in the [Protected settings](#protected-settings).</span></span> <span data-ttu-id="08711-226">Ortak değeri, varsa özel değer tarafından geçersiz ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="08711-226">The public value is overridden by the private value, if set.</span></span> <span data-ttu-id="08711-227">Bir parola gibi bir gizlilik bulunması proxy ayarlarını yerleştirin [ayarların korumalı](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="08711-227">Place proxy settings that contain a secret, such as a password, in the [Protected settings](#protected-settings).</span></span>

<span data-ttu-id="08711-228">Kalan öğeleri aşağıdaki bölümlerde ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="08711-228">The remaining elements are described in detail in the following sections.</span></span>

### <a name="ladcfg"></a><span data-ttu-id="08711-229">ladCfg</span><span class="sxs-lookup"><span data-stu-id="08711-229">ladCfg</span></span>

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

<span data-ttu-id="08711-230">Bu isteğe bağlı yapısı denetimleri ölçümleri ve Azure ölçümleri hizmetine ve diğer veri teslimi için günlükleri toplama iç havuzlar.</span><span class="sxs-lookup"><span data-stu-id="08711-230">This optional structure controls the gathering of metrics and logs for delivery to the Azure Metrics service and to other data sinks.</span></span> <span data-ttu-id="08711-231">Ya da belirtmeniz gerekir `performanceCounters` veya `syslogEvents` veya her ikisini de.</span><span class="sxs-lookup"><span data-stu-id="08711-231">You must specify either `performanceCounters` or `syslogEvents` or both.</span></span> <span data-ttu-id="08711-232">Belirtmeniz gerekir `metrics` yapısı.</span><span class="sxs-lookup"><span data-stu-id="08711-232">You must specify the `metrics` structure.</span></span>

<span data-ttu-id="08711-233">Öğesi</span><span class="sxs-lookup"><span data-stu-id="08711-233">Element</span></span> | <span data-ttu-id="08711-234">Değer</span><span class="sxs-lookup"><span data-stu-id="08711-234">Value</span></span>
------- | -----
<span data-ttu-id="08711-235">eventVolume</span><span class="sxs-lookup"><span data-stu-id="08711-235">eventVolume</span></span> | <span data-ttu-id="08711-236">(isteğe bağlı) Depolama tablo içinde oluşturulan bölümlere sayısını denetler.</span><span class="sxs-lookup"><span data-stu-id="08711-236">(optional) Controls the number of partitions created within the storage table.</span></span> <span data-ttu-id="08711-237">Biri olmalıdır `"Large"`, `"Medium"`, veya `"Small"`.</span><span class="sxs-lookup"><span data-stu-id="08711-237">Must be one of `"Large"`, `"Medium"`, or `"Small"`.</span></span> <span data-ttu-id="08711-238">Belirtilmezse, varsayılan değer: `"Medium"`.</span><span class="sxs-lookup"><span data-stu-id="08711-238">If not specified, the default value is `"Medium"`.</span></span>
<span data-ttu-id="08711-239">sampleRateInSeconds</span><span class="sxs-lookup"><span data-stu-id="08711-239">sampleRateInSeconds</span></span> | <span data-ttu-id="08711-240">(isteğe bağlı) Ham (unaggregated) ölçümleri topluluğu arasındaki varsayılan zaman aralığı.</span><span class="sxs-lookup"><span data-stu-id="08711-240">(optional) The default interval between collection of raw (unaggregated) metrics.</span></span> <span data-ttu-id="08711-241">En küçük desteklenen örnek hızı 15 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="08711-241">The smallest supported sample rate is 15 seconds.</span></span> <span data-ttu-id="08711-242">Belirtilmezse, varsayılan değer: `15`.</span><span class="sxs-lookup"><span data-stu-id="08711-242">If not specified, the default value is `15`.</span></span>

#### <a name="metrics"></a><span data-ttu-id="08711-243">metrics</span><span class="sxs-lookup"><span data-stu-id="08711-243">metrics</span></span>

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

<span data-ttu-id="08711-244">Öğesi</span><span class="sxs-lookup"><span data-stu-id="08711-244">Element</span></span> | <span data-ttu-id="08711-245">Değer</span><span class="sxs-lookup"><span data-stu-id="08711-245">Value</span></span>
------- | -----
<span data-ttu-id="08711-246">resourceId</span><span class="sxs-lookup"><span data-stu-id="08711-246">resourceId</span></span> | <span data-ttu-id="08711-247">VM ait olduğu Azure Resource Manager kaynak kimliği VM veya sanal makine ölçek kümesi.</span><span class="sxs-lookup"><span data-stu-id="08711-247">The Azure Resource Manager resource ID of the VM or of the virtual machine scale set to which the VM belongs.</span></span> <span data-ttu-id="08711-248">Bu ayar olmalıdır herhangi JsonBlob havuz yapılandırmada kullanılırsa da belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="08711-248">This setting must be also specified if any JsonBlob sink is used in the configuration.</span></span>
<span data-ttu-id="08711-249">scheduledTransferPeriod</span><span class="sxs-lookup"><span data-stu-id="08711-249">scheduledTransferPeriod</span></span> | <span data-ttu-id="08711-250">Hesaplanan ve Azure 8601 olduğu zaman aralığı ifade edilen ölçümleri, aktarılan toplam ölçümleri olan sıklığı.</span><span class="sxs-lookup"><span data-stu-id="08711-250">The frequency at which aggregate metrics are to be computed and transferred to Azure Metrics, expressed as an IS 8601 time interval.</span></span> <span data-ttu-id="08711-251">En küçük aktarım süresi 60, diğer bir deyişle, PT1M saniyedir.</span><span class="sxs-lookup"><span data-stu-id="08711-251">The smallest transfer period is 60 seconds, that is, PT1M.</span></span> <span data-ttu-id="08711-252">En az bir scheduledTransferPeriod belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="08711-252">You must specify at least one scheduledTransferPeriod.</span></span>

<span data-ttu-id="08711-253">Performans sayaçları bölümünde belirtilen ölçümleri örnekleri 15 dakikada toplanan veya örnek oranı açıkça sayaç için tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="08711-253">Samples of the metrics specified in the performanceCounters section are collected every 15 seconds or at the sample rate explicitly defined for the counter.</span></span> <span data-ttu-id="08711-254">Birden çok scheduledTransferPeriod sıklıklarını (örnekte olduğu gibi) görünüyorsa, her bir toplama bağımsız olarak hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="08711-254">If multiple scheduledTransferPeriod frequencies appear (as in the example), each aggregation is computed independently.</span></span>

#### <a name="performancecounters"></a><span data-ttu-id="08711-255">performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="08711-255">performanceCounters</span></span>

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

<span data-ttu-id="08711-256">Bu isteğe bağlı bir bölüm ölçümleri koleksiyonunu denetler.</span><span class="sxs-lookup"><span data-stu-id="08711-256">This optional section controls the collection of metrics.</span></span> <span data-ttu-id="08711-257">Ham örnekleri her biri için toplanmış [scheduledTransferPeriod](#metrics) bu değerleri oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="08711-257">Raw samples are aggregated for each [scheduledTransferPeriod](#metrics) to produce these values:</span></span>

* <span data-ttu-id="08711-258">Ortalama</span><span class="sxs-lookup"><span data-stu-id="08711-258">mean</span></span>
* <span data-ttu-id="08711-259">en az</span><span class="sxs-lookup"><span data-stu-id="08711-259">minimum</span></span>
* <span data-ttu-id="08711-260">Maksimum</span><span class="sxs-lookup"><span data-stu-id="08711-260">maximum</span></span>
* <span data-ttu-id="08711-261">Son toplanan değeri</span><span class="sxs-lookup"><span data-stu-id="08711-261">last-collected value</span></span>
* <span data-ttu-id="08711-262">Toplama hesaplamak için kullanılan ham örneklerin sayısı</span><span class="sxs-lookup"><span data-stu-id="08711-262">count of raw samples used to compute the aggregate</span></span>

<span data-ttu-id="08711-263">Öğesi</span><span class="sxs-lookup"><span data-stu-id="08711-263">Element</span></span> | <span data-ttu-id="08711-264">Değer</span><span class="sxs-lookup"><span data-stu-id="08711-264">Value</span></span>
------- | -----
<span data-ttu-id="08711-265">İç havuzlar</span><span class="sxs-lookup"><span data-stu-id="08711-265">sinks</span></span> | <span data-ttu-id="08711-266">(isteğe bağlı) Hangi LAD gönderir ölçüm sonuçlarını toplanan havuzlarını adlarının virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="08711-266">(optional) A comma-separated list of names of sinks to which LAD sends aggregated metric results.</span></span> <span data-ttu-id="08711-267">Tüm toplanan ölçümler için listelenen her havuz yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="08711-267">All aggregated metrics are published to each listed sink.</span></span> <span data-ttu-id="08711-268">Bkz: [sinksConfig](#sinksconfig).</span><span class="sxs-lookup"><span data-stu-id="08711-268">See [sinksConfig](#sinksconfig).</span></span> <span data-ttu-id="08711-269">Örnek: `"EHsink1, myjsonsink"`.</span><span class="sxs-lookup"><span data-stu-id="08711-269">Example: `"EHsink1, myjsonsink"`.</span></span>
<span data-ttu-id="08711-270">type</span><span class="sxs-lookup"><span data-stu-id="08711-270">type</span></span> | <span data-ttu-id="08711-271">Ölçümün gerçek sağlayıcısını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="08711-271">Identifies the actual provider of the metric.</span></span>
<span data-ttu-id="08711-272">sınıfı</span><span class="sxs-lookup"><span data-stu-id="08711-272">class</span></span> | <span data-ttu-id="08711-273">"Sayacı" ile birlikte sağlayıcının ad alanı içindeki belirli ölçüm tanımlar.</span><span class="sxs-lookup"><span data-stu-id="08711-273">Together with "counter", identifies the specific metric within the provider's namespace.</span></span>
<span data-ttu-id="08711-274">Sayaç</span><span class="sxs-lookup"><span data-stu-id="08711-274">counter</span></span> | <span data-ttu-id="08711-275">"Sınıf" ile birlikte sağlayıcının ad alanı içindeki belirli ölçüm tanımlar.</span><span class="sxs-lookup"><span data-stu-id="08711-275">Together with "class", identifies the specific metric within the provider's namespace.</span></span>
<span data-ttu-id="08711-276">counterSpecifier</span><span class="sxs-lookup"><span data-stu-id="08711-276">counterSpecifier</span></span> | <span data-ttu-id="08711-277">Azure ölçümleri ad alanı içindeki belirli ölçüm tanımlar.</span><span class="sxs-lookup"><span data-stu-id="08711-277">Identifies the specific metric within the Azure Metrics namespace.</span></span>
<span data-ttu-id="08711-278">Koşul</span><span class="sxs-lookup"><span data-stu-id="08711-278">condition</span></span> | <span data-ttu-id="08711-279">(isteğe bağlı) Ölçüm uygular veya toplama söz konusu nesne tüm örneklerinde seçer nesne belirli bir örneği seçer.</span><span class="sxs-lookup"><span data-stu-id="08711-279">(optional) Selects a specific instance of the object to which the metric applies or selects the aggregation across all instances of that object.</span></span> <span data-ttu-id="08711-280">Daha fazla bilgi için bkz: [ `builtin` ölçüm tanımlarını](#metrics-supported-by-builtin).</span><span class="sxs-lookup"><span data-stu-id="08711-280">For more information, see the [`builtin` metric definitions](#metrics-supported-by-builtin).</span></span>
<span data-ttu-id="08711-281">sampleRate</span><span class="sxs-lookup"><span data-stu-id="08711-281">sampleRate</span></span> | <span data-ttu-id="08711-282">Toplanan ve bu ölçüm için ham örnek hızı ayarlar 8601 aralığı BELİRTİR.</span><span class="sxs-lookup"><span data-stu-id="08711-282">IS 8601 interval that sets the rate at which raw samples for this metric are collected.</span></span> <span data-ttu-id="08711-283">Ayarlanmadı, toplama aralığı değeri olarak ayarlanmış olup olmadığını [sampleRateInSeconds](#ladcfg).</span><span class="sxs-lookup"><span data-stu-id="08711-283">If not set, the collection interval is set by the value of [sampleRateInSeconds](#ladcfg).</span></span> <span data-ttu-id="08711-284">En kısa desteklenen örnek hızı 15 (PT15S) saniyedir.</span><span class="sxs-lookup"><span data-stu-id="08711-284">The shortest supported sample rate is 15 seconds (PT15S).</span></span>
<span data-ttu-id="08711-285">Birim</span><span class="sxs-lookup"><span data-stu-id="08711-285">unit</span></span> | <span data-ttu-id="08711-286">Bu dizeler biri olmalıdır: "Count", "Bayt sayısı", "Saniye", "Yüzde", "CountPerSecond", "BytesPerSecond", "Milisaniyelik".</span><span class="sxs-lookup"><span data-stu-id="08711-286">Should be one of these strings: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span></span> <span data-ttu-id="08711-287">Ölçü birimi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="08711-287">Defines the unit for the metric.</span></span> <span data-ttu-id="08711-288">Toplanan veri tüketicileri bu birimi eşleştirmek için toplanan veri değerleri bekler.</span><span class="sxs-lookup"><span data-stu-id="08711-288">Consumers of the collected data expect the collected data values to match this unit.</span></span> <span data-ttu-id="08711-289">Bu alan LAD yoksayar.</span><span class="sxs-lookup"><span data-stu-id="08711-289">LAD ignores this field.</span></span>
<span data-ttu-id="08711-290">Görünen adı</span><span class="sxs-lookup"><span data-stu-id="08711-290">displayName</span></span> | <span data-ttu-id="08711-291">Etiket (ilişkili yerel ayarı tarafından belirtilen dilde) bu verileri Azure ölçümleri eklenmiş.</span><span class="sxs-lookup"><span data-stu-id="08711-291">The label (in the language specified by the associated locale setting) to be attached to this data in Azure Metrics.</span></span> <span data-ttu-id="08711-292">Bu alan LAD yoksayar.</span><span class="sxs-lookup"><span data-stu-id="08711-292">LAD ignores this field.</span></span>

<span data-ttu-id="08711-293">CounterSpecifier rasgele bir tanımlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="08711-293">The counterSpecifier is an arbitrary identifier.</span></span> <span data-ttu-id="08711-294">Tüketiciler ölçümleri, Azure portal grafik ister ve özelliği, uyarı counterSpecifier "bir ölçüm veya bir ölçüm örneğini tanımlayan anahtar olarak" kullanın.</span><span class="sxs-lookup"><span data-stu-id="08711-294">Consumers of metrics, like the Azure portal charting and alerting feature, use counterSpecifier as the "key" that identifies a metric or an instance of a metric.</span></span> <span data-ttu-id="08711-295">İçin `builtin` ölçümleri, öneririz ile başlayan counterSpecifier değerleri kullandığınız `/builtin/`.</span><span class="sxs-lookup"><span data-stu-id="08711-295">For `builtin` metrics, we recommend you use counterSpecifier values that begin with `/builtin/`.</span></span> <span data-ttu-id="08711-296">Ölçüm belirli bir örneği topluyorsanız counterSpecifier değerine örneğinin tanıtıcısı ekleme öneririz.</span><span class="sxs-lookup"><span data-stu-id="08711-296">If you are collecting a specific instance of a metric, we recommend you attach the identifier of the instance to the counterSpecifier value.</span></span> <span data-ttu-id="08711-297">Bazı örnekler:</span><span class="sxs-lookup"><span data-stu-id="08711-297">Some examples:</span></span>

* <span data-ttu-id="08711-298">`/builtin/Processor/PercentIdleTime`-Tüm çekirdek arasında ortalaması boşta kalma süresi</span><span class="sxs-lookup"><span data-stu-id="08711-298">`/builtin/Processor/PercentIdleTime` - Idle time averaged across all cores</span></span>
* <span data-ttu-id="08711-299">`/builtin/Disk/FreeSpace(/mnt)`-/Mnt dosya sistemi boş alan</span><span class="sxs-lookup"><span data-stu-id="08711-299">`/builtin/Disk/FreeSpace(/mnt)` - Free space for the /mnt filesystem</span></span>
* <span data-ttu-id="08711-300">`/builtin/Disk/FreeSpace`-Boş alan tüm takılı bağlanan dosya sistemlerinin ortalaması</span><span class="sxs-lookup"><span data-stu-id="08711-300">`/builtin/Disk/FreeSpace` - Free space averaged across all mounted filesystems</span></span>

<span data-ttu-id="08711-301">Ne LAD ne de Azure portalında herhangi bir desenle eşleşen counterSpecifier değeri bekler.</span><span class="sxs-lookup"><span data-stu-id="08711-301">Neither LAD nor the Azure portal expects the counterSpecifier value to match any pattern.</span></span> <span data-ttu-id="08711-302">CounterSpecifier değerleri nasıl oluşturmak tutarlı olması.</span><span class="sxs-lookup"><span data-stu-id="08711-302">Be consistent in how you construct counterSpecifier values.</span></span>

<span data-ttu-id="08711-303">Belirttiğinizde `performanceCounters`, LAD her zaman Yazar verileri Azure depolama alanında bir tablo.</span><span class="sxs-lookup"><span data-stu-id="08711-303">When you specify `performanceCounters`, LAD always writes data to a table in Azure storage.</span></span> <span data-ttu-id="08711-304">JSON BLOB'ları ve/veya olay hub'ları yazılan aynı veri olabilir, ancak bir tabloya veri depolama devre dışı bırakılamıyor.</span><span class="sxs-lookup"><span data-stu-id="08711-304">You can have the same data written to JSON blobs and/or Event Hubs, but you cannot disable storing data to a table.</span></span> <span data-ttu-id="08711-305">Tanılama uzantısını tüm örnekleri aynı depolama hesabı adı kullanmak üzere yapılandırılmış ve uç nokta, aynı tabloya kendi ölçümleri ve günlükleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="08711-305">All instances of the diagnostic extension configured to use the same storage account name and endpoint add their metrics and logs to the same table.</span></span> <span data-ttu-id="08711-306">Çok fazla sayıda sanal makineleri aynı tablo bölüme yazıyorsanız, Azure yazma daraltabilir bu bölümü.</span><span class="sxs-lookup"><span data-stu-id="08711-306">If too many VMs are writing to the same table partition, Azure can throttle writes to that partition.</span></span> <span data-ttu-id="08711-307">EventVolume ayar 1 (küçük), 10 (Orta) üzerinden yayılan ya da 100 (büyük) farklı bölümleri sağlanacak girişlerinin neden olur.</span><span class="sxs-lookup"><span data-stu-id="08711-307">The eventVolume setting causes entries to be spread across 1 (Small), 10 (Medium), or 100 (Large) different partitions.</span></span> <span data-ttu-id="08711-308">Genellikle, "Orta" trafik değil kısıtlanan emin olmak yeterli olur.</span><span class="sxs-lookup"><span data-stu-id="08711-308">Usually, "Medium" is sufficient to ensure traffic is not throttled.</span></span> <span data-ttu-id="08711-309">Azure Portalı'nın Azure ölçümleri özelliği veri grafikleri üretmek için veya uyarıları tetiklemek için bu tabloyu kullanır.</span><span class="sxs-lookup"><span data-stu-id="08711-309">The Azure Metrics feature of the Azure portal uses the data in this table to produce graphs or to trigger alerts.</span></span> <span data-ttu-id="08711-310">Bu dizeler birleşimini tablo adıdır:</span><span class="sxs-lookup"><span data-stu-id="08711-310">The table name is the concatenation of these strings:</span></span>

* `WADMetrics`
* <span data-ttu-id="08711-311">Tabloda depolanan toplanmış değerler için "scheduledTransferPeriod"</span><span class="sxs-lookup"><span data-stu-id="08711-311">The "scheduledTransferPeriod" for the aggregated values stored in the table</span></span>
* `P10DV2S`
* <span data-ttu-id="08711-312">10 günde değişiklikleri "YYYYAAGG" biçiminde bir tarih</span><span class="sxs-lookup"><span data-stu-id="08711-312">A date, in the form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="08711-313">Örnekler `WADMetricsPT1HP10DV2S20170410` ve `WADMetricsPT1MP10DV2S20170609`.</span><span class="sxs-lookup"><span data-stu-id="08711-313">Examples include `WADMetricsPT1HP10DV2S20170410` and `WADMetricsPT1MP10DV2S20170609`.</span></span>

#### <a name="syslogevents"></a><span data-ttu-id="08711-314">syslogEvents</span><span class="sxs-lookup"><span data-stu-id="08711-314">syslogEvents</span></span>

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

<span data-ttu-id="08711-315">Bu isteğe bağlı bir bölüm syslog günlük olayları koleksiyonu denetler.</span><span class="sxs-lookup"><span data-stu-id="08711-315">This optional section controls the collection of log events from syslog.</span></span> <span data-ttu-id="08711-316">Bölüm atlanırsa, syslog olayları hiç yakalanmaz.</span><span class="sxs-lookup"><span data-stu-id="08711-316">If the section is omitted, syslog events are not captured at all.</span></span>

<span data-ttu-id="08711-317">SyslogEventConfiguration koleksiyon her syslog özelliğini ilgi için bir giriş içeriyor.</span><span class="sxs-lookup"><span data-stu-id="08711-317">The syslogEventConfiguration collection has one entry for each syslog facility of interest.</span></span> <span data-ttu-id="08711-318">MinSeverity "Hiçbiri" için belirli bir özellik varsa veya bu tesis öğesinde hiç görünmüyorsa, bu tesis hiçbir olaylarından yakalanır.</span><span class="sxs-lookup"><span data-stu-id="08711-318">If minSeverity is "NONE" for a particular facility, or if that facility does not appear in the element at all, no events from that facility are captured.</span></span>

<span data-ttu-id="08711-319">Öğesi</span><span class="sxs-lookup"><span data-stu-id="08711-319">Element</span></span> | <span data-ttu-id="08711-320">Değer</span><span class="sxs-lookup"><span data-stu-id="08711-320">Value</span></span>
------- | -----
<span data-ttu-id="08711-321">İç havuzlar</span><span class="sxs-lookup"><span data-stu-id="08711-321">sinks</span></span> | <span data-ttu-id="08711-322">Ayrı günlük olayları yayımlanan havuzlarını adlarının virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="08711-322">A comma-separated list of names of sinks to which individual log events are published.</span></span> <span data-ttu-id="08711-323">SyslogEventConfiguration kısıtlamalarına eşleşen tüm günlük olayları için listelenen her havuz yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="08711-323">All log events matching the restrictions in syslogEventConfiguration are published to each listed sink.</span></span> <span data-ttu-id="08711-324">Örnek: "EHforsyslog"</span><span class="sxs-lookup"><span data-stu-id="08711-324">Example: "EHforsyslog"</span></span>
<span data-ttu-id="08711-325">facilityName</span><span class="sxs-lookup"><span data-stu-id="08711-325">facilityName</span></span> | <span data-ttu-id="08711-326">Bir syslog tesis adı (gibi "günlük\_kullanıcı" veya "günlük\_LOCAL0").</span><span class="sxs-lookup"><span data-stu-id="08711-326">A syslog facility name (such as "LOG\_USER" or "LOG\_LOCAL0").</span></span> <span data-ttu-id="08711-327">"Özelliği" bölümüne bakın [syslog adam sayfa](http://man7.org/linux/man-pages/man3/syslog.3.html) tam listesi için.</span><span class="sxs-lookup"><span data-stu-id="08711-327">See the "facility" section of the [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for the full list.</span></span>
<span data-ttu-id="08711-328">minSeverity</span><span class="sxs-lookup"><span data-stu-id="08711-328">minSeverity</span></span> | <span data-ttu-id="08711-329">Bir syslog önem düzeyi (gibi "günlük\_hata" veya "günlük\_bilgileri").</span><span class="sxs-lookup"><span data-stu-id="08711-329">A syslog severity level (such as "LOG\_ERR" or "LOG\_INFO").</span></span> <span data-ttu-id="08711-330">"Düzeyi" bölümüne bakın [syslog adam sayfa](http://man7.org/linux/man-pages/man3/syslog.3.html) tam listesi için.</span><span class="sxs-lookup"><span data-stu-id="08711-330">See the "level" section of the [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for the full list.</span></span> <span data-ttu-id="08711-331">Uzantı veya belirtilen düzeyin üstü tesis gönderilen olayları yakalar.</span><span class="sxs-lookup"><span data-stu-id="08711-331">The extension captures events sent to the facility at or above the specified level.</span></span>

<span data-ttu-id="08711-332">Belirttiğinizde `syslogEvents`, LAD her zaman Yazar verileri Azure depolama alanında bir tablo.</span><span class="sxs-lookup"><span data-stu-id="08711-332">When you specify `syslogEvents`, LAD always writes data to a table in Azure storage.</span></span> <span data-ttu-id="08711-333">JSON BLOB'ları ve/veya olay hub'ları yazılan aynı veri olabilir, ancak bir tabloya veri depolama devre dışı bırakılamıyor.</span><span class="sxs-lookup"><span data-stu-id="08711-333">You can have the same data written to JSON blobs and/or Event Hubs, but you cannot disable storing data to a table.</span></span> <span data-ttu-id="08711-334">Bu tablo için bölümleme davranışı için açıklandığı gibi aynıdır `performanceCounters`.</span><span class="sxs-lookup"><span data-stu-id="08711-334">The partitioning behavior for this table is the same as described for `performanceCounters`.</span></span> <span data-ttu-id="08711-335">Bu dizeler birleşimini tablo adıdır:</span><span class="sxs-lookup"><span data-stu-id="08711-335">The table name is the concatenation of these strings:</span></span>

* `LinuxSyslog`
* <span data-ttu-id="08711-336">10 günde değişiklikleri "YYYYAAGG" biçiminde bir tarih</span><span class="sxs-lookup"><span data-stu-id="08711-336">A date, in the form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="08711-337">Örnekler `LinuxSyslog20170410` ve `LinuxSyslog20170609`.</span><span class="sxs-lookup"><span data-stu-id="08711-337">Examples include `LinuxSyslog20170410` and `LinuxSyslog20170609`.</span></span>

### <a name="perfcfg"></a><span data-ttu-id="08711-338">perfCfg</span><span class="sxs-lookup"><span data-stu-id="08711-338">perfCfg</span></span>

<span data-ttu-id="08711-339">Bu isteğe bağlı bir bölüm rasgele yürütülmesi denetimleri [OMI](https://github.com/Microsoft/omi) sorgular.</span><span class="sxs-lookup"><span data-stu-id="08711-339">This optional section controls execution of arbitrary [OMI](https://github.com/Microsoft/omi) queries.</span></span>

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

<span data-ttu-id="08711-340">Öğesi</span><span class="sxs-lookup"><span data-stu-id="08711-340">Element</span></span> | <span data-ttu-id="08711-341">Değer</span><span class="sxs-lookup"><span data-stu-id="08711-341">Value</span></span>
------- | -----
<span data-ttu-id="08711-342">Namespace</span><span class="sxs-lookup"><span data-stu-id="08711-342">namespace</span></span> | <span data-ttu-id="08711-343">(isteğe bağlı) Sorgu içinde yürütülmesi gereken OMI ad alanı.</span><span class="sxs-lookup"><span data-stu-id="08711-343">(optional) The OMI namespace within which the query should be executed.</span></span> <span data-ttu-id="08711-344">Belirtilmezse, "kök/tarafından uygulanan scx", varsayılan değer: [System Center platformlar arası sağlayıcıları](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span><span class="sxs-lookup"><span data-stu-id="08711-344">If unspecified, the default value is "root/scx", implemented by the [System Center Cross-platform Providers](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span></span>
<span data-ttu-id="08711-345">sorgu</span><span class="sxs-lookup"><span data-stu-id="08711-345">query</span></span> | <span data-ttu-id="08711-346">Yürütülecek OMI sorgu.</span><span class="sxs-lookup"><span data-stu-id="08711-346">The OMI query to be executed.</span></span>
<span data-ttu-id="08711-347">Tablo</span><span class="sxs-lookup"><span data-stu-id="08711-347">table</span></span> | <span data-ttu-id="08711-348">(isteğe bağlı) Azure depolama tablosunda belirtilen depolama hesabı (bkz [ayarların korumalı](#protected-settings)).</span><span class="sxs-lookup"><span data-stu-id="08711-348">(optional) The Azure storage table, in the designated storage account (see [Protected settings](#protected-settings)).</span></span>
<span data-ttu-id="08711-349">Sıklık</span><span class="sxs-lookup"><span data-stu-id="08711-349">frequency</span></span> | <span data-ttu-id="08711-350">(isteğe bağlı) Sorgu yürütme arasındaki saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="08711-350">(optional) The number of seconds between execution of the query.</span></span> <span data-ttu-id="08711-351">300 (5 dakika); varsayılan değer: en düşük değer 15 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="08711-351">Default value is 300 (5 minutes); minimum value is 15 seconds.</span></span>
<span data-ttu-id="08711-352">İç havuzlar</span><span class="sxs-lookup"><span data-stu-id="08711-352">sinks</span></span> | <span data-ttu-id="08711-353">(isteğe bağlı) Ham örnek ölçüm sonuçlarını yayımlanan ek havuzlarını adlarının virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="08711-353">(optional) A comma-separated list of names of additional sinks to which raw sample metric results should be published.</span></span> <span data-ttu-id="08711-354">Bu ham örnekleri toplama yok veya Azure ölçümleri uzantısı tarafından hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="08711-354">No aggregation of these raw samples is computed by the extension or by Azure Metrics.</span></span>

<span data-ttu-id="08711-355">"Tablo" veya "İç havuzlar" ya da her ikisini de belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="08711-355">Either "table" or "sinks", or both, must be specified.</span></span>

### <a name="filelogs"></a><span data-ttu-id="08711-356">fileLogs</span><span class="sxs-lookup"><span data-stu-id="08711-356">fileLogs</span></span>

<span data-ttu-id="08711-357">Günlük dosyalarının yakalama denetler.</span><span class="sxs-lookup"><span data-stu-id="08711-357">Controls the capture of log files.</span></span> <span data-ttu-id="08711-358">LAD dosyasına yazılır gibi yeni metin satırlarını yakalar ve tablo satırları ve/veya belirtilen tüm havuzlarını (JsonBlob veya EventHub) yazar.</span><span class="sxs-lookup"><span data-stu-id="08711-358">LAD captures new text lines as they are written to the file and writes them to table rows and/or any specified sinks (JsonBlob or EventHub).</span></span>

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

<span data-ttu-id="08711-359">Öğesi</span><span class="sxs-lookup"><span data-stu-id="08711-359">Element</span></span> | <span data-ttu-id="08711-360">Değer</span><span class="sxs-lookup"><span data-stu-id="08711-360">Value</span></span>
------- | -----
<span data-ttu-id="08711-361">Dosya</span><span class="sxs-lookup"><span data-stu-id="08711-361">file</span></span> | <span data-ttu-id="08711-362">İzlenen ve yakalanan için günlük dosyasının tam yol adı.</span><span class="sxs-lookup"><span data-stu-id="08711-362">The full pathname of the log file to be watched and captured.</span></span> <span data-ttu-id="08711-363">Yol, tek bir dosya adı olmalıdır; bir dizin adı veya joker karakterler içeriyor.</span><span class="sxs-lookup"><span data-stu-id="08711-363">The pathname must name a single file; it cannot name a directory or contain wildcards.</span></span>
<span data-ttu-id="08711-364">Tablo</span><span class="sxs-lookup"><span data-stu-id="08711-364">table</span></span> | <span data-ttu-id="08711-365">(isteğe bağlı) İçine yeni dosya "kuyruğu" satırlarından yazılır belirtilen depolama hesabında (belirtildiği şekilde korumalı yapılandırma), Azure depolama tablo.</span><span class="sxs-lookup"><span data-stu-id="08711-365">(optional) The Azure storage table, in the designated storage account (as specified in the protected configuration), into which new lines from the "tail" of the file are written.</span></span>
<span data-ttu-id="08711-366">İç havuzlar</span><span class="sxs-lookup"><span data-stu-id="08711-366">sinks</span></span> | <span data-ttu-id="08711-367">(isteğe bağlı) Günlük gönderilen hatları için ek havuzlarını adlarının virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="08711-367">(optional) A comma-separated list of names of additional sinks to which log lines sent.</span></span>

<span data-ttu-id="08711-368">"Tablo" veya "İç havuzlar" ya da her ikisini de belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="08711-368">Either "table" or "sinks", or both, must be specified.</span></span>

## <a name="metrics-supported-by-the-builtin-provider"></a><span data-ttu-id="08711-369">Yerleşik sağlayıcı tarafından desteklenen ölçümleri</span><span class="sxs-lookup"><span data-stu-id="08711-369">Metrics supported by the builtin provider</span></span>

<span data-ttu-id="08711-370">Yerleşik ölçüm ölçümleri geniş bir kullanıcı kümesi için en ilgi çekici bir kaynak sağlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="08711-370">The builtin metric provider is a source of metrics most interesting to a broad set of users.</span></span> <span data-ttu-id="08711-371">Bu ölçümler beş geniş sınıflara ayrılır:</span><span class="sxs-lookup"><span data-stu-id="08711-371">These metrics fall into five broad classes:</span></span>

* <span data-ttu-id="08711-372">İşlemci</span><span class="sxs-lookup"><span data-stu-id="08711-372">Processor</span></span>
* <span data-ttu-id="08711-373">Bellek</span><span class="sxs-lookup"><span data-stu-id="08711-373">Memory</span></span>
* <span data-ttu-id="08711-374">Ağ</span><span class="sxs-lookup"><span data-stu-id="08711-374">Network</span></span>
* <span data-ttu-id="08711-375">Dosya sistemi</span><span class="sxs-lookup"><span data-stu-id="08711-375">Filesystem</span></span>
* <span data-ttu-id="08711-376">Disk</span><span class="sxs-lookup"><span data-stu-id="08711-376">Disk</span></span>

### <a name="builtin-metrics-for-the-processor-class"></a><span data-ttu-id="08711-377">İşlemci sınıfı için yerleşik ölçümleri</span><span class="sxs-lookup"><span data-stu-id="08711-377">builtin metrics for the Processor class</span></span>

<span data-ttu-id="08711-378">Ölçümleri işlemci sınıfının VM'deki işlemci kullanımı hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="08711-378">The Processor class of metrics provides information about processor usage in the VM.</span></span> <span data-ttu-id="08711-379">Yüzdeleri toplanırken ortalama tüm CPU'lar arasında sonucudur.</span><span class="sxs-lookup"><span data-stu-id="08711-379">When aggregating percentages, the result is the average across all CPUs.</span></span> <span data-ttu-id="08711-380">Bir iki çekirdek VM, bir çekirdek % 100 meşgul ve diğer % 100 boşta şeklindeydi durumunda bildirilen PercentIdleTime 50 olur.</span><span class="sxs-lookup"><span data-stu-id="08711-380">In a two core VM, if one core was 100% busy and the other was 100% idle, the reported PercentIdleTime would be 50.</span></span> <span data-ttu-id="08711-381">Her çekirdek % 50 aynı dönem için meşgul ise, bildirilen sonuç da 50 olur.</span><span class="sxs-lookup"><span data-stu-id="08711-381">If each core was 50% busy for the same period, the reported result would also be 50.</span></span> <span data-ttu-id="08711-382">Bir çekirdek % 100 meşgul ve diğerleri boşta ile dört çekirdek VM içinde bildirilen PercentIdleTime 75 olacaktır.</span><span class="sxs-lookup"><span data-stu-id="08711-382">In a four core VM, with one core 100% busy and the others idle, the reported PercentIdleTime would be 75.</span></span>

<span data-ttu-id="08711-383">Sayaç</span><span class="sxs-lookup"><span data-stu-id="08711-383">counter</span></span> | <span data-ttu-id="08711-384">Anlamı</span><span class="sxs-lookup"><span data-stu-id="08711-384">Meaning</span></span>
------- | -------
<span data-ttu-id="08711-385">PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="08711-385">PercentIdleTime</span></span> | <span data-ttu-id="08711-386">İşlemci çekirdeği boşta döngü yürütülmekte toplama penceresi sırasında zamanı yüzdesi</span><span class="sxs-lookup"><span data-stu-id="08711-386">Percentage of time during the aggregation window that processors were executing the kernel idle loop</span></span>
<span data-ttu-id="08711-387">percentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="08711-387">PercentProcessorTime</span></span> | <span data-ttu-id="08711-388">Boş olmayan bir iş parçacığı yürütme zamanı yüzdesi</span><span class="sxs-lookup"><span data-stu-id="08711-388">Percentage of time executing a non-idle thread</span></span>
<span data-ttu-id="08711-389">PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="08711-389">PercentIOWaitTime</span></span> | <span data-ttu-id="08711-390">G/ç işlemlerinin tamamlanması beklenirken zaman yüzdesi</span><span class="sxs-lookup"><span data-stu-id="08711-390">Percentage of time waiting for IO operations to complete</span></span>
<span data-ttu-id="08711-391">PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="08711-391">PercentInterruptTime</span></span> | <span data-ttu-id="08711-392">Donanım/yazılım kesmeler ve DPC'ler (ertelenmiş yordam çağrılarını) yürütme zamanı yüzdesi</span><span class="sxs-lookup"><span data-stu-id="08711-392">Percentage of time executing hardware/software interrupts and DPCs (deferred procedure calls)</span></span>
<span data-ttu-id="08711-393">PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="08711-393">PercentUserTime</span></span> | <span data-ttu-id="08711-394">Boş olmayan süresini toplama penceresi sırasında zamanın normal öncelik en fazla kullanıcı yüzdesi</span><span class="sxs-lookup"><span data-stu-id="08711-394">Of non-idle time during the aggregation window, the percentage of time spent in user more at normal priority</span></span>
<span data-ttu-id="08711-395">PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="08711-395">PercentNiceTime</span></span> | <span data-ttu-id="08711-396">Boş olmayan süre yüzdesi alçaltılmış (iyi) öncelikli harcanan</span><span class="sxs-lookup"><span data-stu-id="08711-396">Of non-idle time, the percentage spent at lowered (nice) priority</span></span>
<span data-ttu-id="08711-397">PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="08711-397">PercentPrivilegedTime</span></span> | <span data-ttu-id="08711-398">Boş olmayan süresini yüzde ayrıcalıklı (çekirdek) modda harcanan</span><span class="sxs-lookup"><span data-stu-id="08711-398">Of non-idle time, the percentage spent in privileged (kernel) mode</span></span>

<span data-ttu-id="08711-399">İlk dört sayaçları % 100'e sum.</span><span class="sxs-lookup"><span data-stu-id="08711-399">The first four counters should sum to 100%.</span></span> <span data-ttu-id="08711-400">Son üç sayaçlar da toplam % 100; Bunlar PercentProcessorTime, PercentIOWaitTime ve PercentInterruptTime toplamını ayırabilir.</span><span class="sxs-lookup"><span data-stu-id="08711-400">The last three counters also sum to 100%; they subdivide the sum of PercentProcessorTime, PercentIOWaitTime, and PercentInterruptTime.</span></span>

<span data-ttu-id="08711-401">Tüm işlemciler arasında toplanan tek bir ölçüm elde etmek için ayarlama `"condition": "IsAggregate=TRUE"`.</span><span class="sxs-lookup"><span data-stu-id="08711-401">To obtain a single metric aggregated across all processors, set `"condition": "IsAggregate=TRUE"`.</span></span> <span data-ttu-id="08711-402">Bir dört ikinci mantıksal İşlemci çekirdek VM gibi belirli bir işlemci için bir ölçüm elde etmek için ayarlama `"condition": "Name=\\"1\\""`.</span><span class="sxs-lookup"><span data-stu-id="08711-402">To obtain a metric for a specific processor, such as the second logical processor of a four core VM, set `"condition": "Name=\\"1\\""`.</span></span> <span data-ttu-id="08711-403">Mantıksal işlemci numaralarıdır aralığında `[0..n-1]`.</span><span class="sxs-lookup"><span data-stu-id="08711-403">Logical processor numbers are in the range `[0..n-1]`.</span></span>

### <a name="builtin-metrics-for-the-memory-class"></a><span data-ttu-id="08711-404">Bellek sınıfı için yerleşik ölçümleri</span><span class="sxs-lookup"><span data-stu-id="08711-404">builtin metrics for the Memory class</span></span>

<span data-ttu-id="08711-405">Ölçümleri bellek sınıfının disk belleği ve değiştirmeyi bellek kullanımı hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="08711-405">The Memory class of metrics provides information about memory utilization, paging, and swapping.</span></span>

<span data-ttu-id="08711-406">Sayaç</span><span class="sxs-lookup"><span data-stu-id="08711-406">counter</span></span> | <span data-ttu-id="08711-407">Anlamı</span><span class="sxs-lookup"><span data-stu-id="08711-407">Meaning</span></span>
------- | -------
<span data-ttu-id="08711-408">AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="08711-408">AvailableMemory</span></span> | <span data-ttu-id="08711-409">MIB kullanılabilir fiziksel bellek</span><span class="sxs-lookup"><span data-stu-id="08711-409">Available physical memory in MiB</span></span>
<span data-ttu-id="08711-410">PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="08711-410">PercentAvailableMemory</span></span> | <span data-ttu-id="08711-411">Kullanılabilir fiziksel belleğin toplam bellek yüzdesi</span><span class="sxs-lookup"><span data-stu-id="08711-411">Available physical memory as a percent of total memory</span></span>
<span data-ttu-id="08711-412">UsedMemory</span><span class="sxs-lookup"><span data-stu-id="08711-412">UsedMemory</span></span> | <span data-ttu-id="08711-413">Kullanımda fiziksel bellek (MIB)</span><span class="sxs-lookup"><span data-stu-id="08711-413">In-use physical memory (MiB)</span></span>
<span data-ttu-id="08711-414">PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="08711-414">PercentUsedMemory</span></span> | <span data-ttu-id="08711-415">Kullanımdaki fiziksel belleğin toplam bellek yüzdesi</span><span class="sxs-lookup"><span data-stu-id="08711-415">In-use physical memory as a percent of total memory</span></span>
<span data-ttu-id="08711-416">PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="08711-416">PagesPerSec</span></span> | <span data-ttu-id="08711-417">Toplam disk belleği (okuma/yazma)</span><span class="sxs-lookup"><span data-stu-id="08711-417">Total paging (read/write)</span></span>
<span data-ttu-id="08711-418">PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="08711-418">PagesReadPerSec</span></span> | <span data-ttu-id="08711-419">Depolama (takas dosyası, program dosyası, eşlenmiş dosya, vb.) yedekleme sayfaları oku</span><span class="sxs-lookup"><span data-stu-id="08711-419">Pages read from backing store (swap file, program file, mapped file, etc.)</span></span>
<span data-ttu-id="08711-420">PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="08711-420">PagesWrittenPerSec</span></span> | <span data-ttu-id="08711-421">Yedekleme deposu (takas dosyası, eşlenmiş dosya, vb.) yazılan sayfa</span><span class="sxs-lookup"><span data-stu-id="08711-421">Pages written to backing store (swap file, mapped file, etc.)</span></span>
<span data-ttu-id="08711-422">AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="08711-422">AvailableSwap</span></span> | <span data-ttu-id="08711-423">Kullanılmayan takas alanı (MIB)</span><span class="sxs-lookup"><span data-stu-id="08711-423">Unused swap space (MiB)</span></span>
<span data-ttu-id="08711-424">PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="08711-424">PercentAvailableSwap</span></span> | <span data-ttu-id="08711-425">Kullanılmayan değiştirme alanının toplam değiştirme yüzdesi</span><span class="sxs-lookup"><span data-stu-id="08711-425">Unused swap space as a percentage of total swap</span></span>
<span data-ttu-id="08711-426">UsedSwap</span><span class="sxs-lookup"><span data-stu-id="08711-426">UsedSwap</span></span> | <span data-ttu-id="08711-427">Kullanımda takas alanı (MIB)</span><span class="sxs-lookup"><span data-stu-id="08711-427">In-use swap space (MiB)</span></span>
<span data-ttu-id="08711-428">PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="08711-428">PercentUsedSwap</span></span> | <span data-ttu-id="08711-429">Değiştirme alanının toplam değiştirme yüzdesi olarak kullanımda</span><span class="sxs-lookup"><span data-stu-id="08711-429">In-use swap space as a percentage of total swap</span></span>

<span data-ttu-id="08711-430">Bu sınıf ölçümleri yalnızca tek bir örneği vardır.</span><span class="sxs-lookup"><span data-stu-id="08711-430">This class of metrics has only a single instance.</span></span> <span data-ttu-id="08711-431">"Koşul" özniteliği yok yararlı ayarlara sahip ve alınmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="08711-431">The "condition" attribute has no useful settings and should be omitted.</span></span>

### <a name="builtin-metrics-for-the-network-class"></a><span data-ttu-id="08711-432">Ağ sınıfı için yerleşik ölçümleri</span><span class="sxs-lookup"><span data-stu-id="08711-432">builtin metrics for the Network class</span></span>

<span data-ttu-id="08711-433">Ölçümleri ağ sınıfı, önyüklemeden tek tek ağ arabirimleri üzerinde ağ etkinliği hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="08711-433">The Network class of metrics provides information about network activity on an individual network interfaces since boot.</span></span> <span data-ttu-id="08711-434">LAD ana ölçümleri alınabilir bant genişliği ölçümleri kullanıma sunmuyor.</span><span class="sxs-lookup"><span data-stu-id="08711-434">LAD does not expose bandwidth metrics, which can be retrieved from host metrics.</span></span>

<span data-ttu-id="08711-435">Sayaç</span><span class="sxs-lookup"><span data-stu-id="08711-435">counter</span></span> | <span data-ttu-id="08711-436">Anlamı</span><span class="sxs-lookup"><span data-stu-id="08711-436">Meaning</span></span>
------- | -------
<span data-ttu-id="08711-437">BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="08711-437">BytesTransmitted</span></span> | <span data-ttu-id="08711-438">Önyüklemeden gönderilen toplam bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="08711-438">Total bytes sent since boot</span></span>
<span data-ttu-id="08711-439">BytesReceived</span><span class="sxs-lookup"><span data-stu-id="08711-439">BytesReceived</span></span> | <span data-ttu-id="08711-440">Önyüklemeden alınan toplam bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="08711-440">Total bytes received since boot</span></span>
<span data-ttu-id="08711-441">BytesTotal</span><span class="sxs-lookup"><span data-stu-id="08711-441">BytesTotal</span></span> | <span data-ttu-id="08711-442">Gönderilen veya alınan önyüklemeden toplam bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="08711-442">Total bytes sent or received since boot</span></span>
<span data-ttu-id="08711-443">PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="08711-443">PacketsTransmitted</span></span> | <span data-ttu-id="08711-444">Önyüklemeden gönderilen toplam paket sayısı</span><span class="sxs-lookup"><span data-stu-id="08711-444">Total packets sent since boot</span></span>
<span data-ttu-id="08711-445">PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="08711-445">PacketsReceived</span></span> | <span data-ttu-id="08711-446">Önyüklemeden alınan toplam paket sayısı</span><span class="sxs-lookup"><span data-stu-id="08711-446">Total packets received since boot</span></span>
<span data-ttu-id="08711-447">TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="08711-447">TotalRxErrors</span></span> | <span data-ttu-id="08711-448">Sayısı önyüklemeden hataları alırsınız</span><span class="sxs-lookup"><span data-stu-id="08711-448">Number of receive errors since boot</span></span>
<span data-ttu-id="08711-449">TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="08711-449">TotalTxErrors</span></span> | <span data-ttu-id="08711-450">Sayısı önyüklemeden iletme işlemi hataları</span><span class="sxs-lookup"><span data-stu-id="08711-450">Number of transmit errors since boot</span></span>
<span data-ttu-id="08711-451">TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="08711-451">TotalCollisions</span></span> | <span data-ttu-id="08711-452">Çakışmaları önyüklemeden ağ bağlantı noktaları tarafından bildirilen sayısı</span><span class="sxs-lookup"><span data-stu-id="08711-452">Number of collisions reported by the network ports since boot</span></span>

 <span data-ttu-id="08711-453">Bu sınıf instanced rağmen LAD tüm ağ aygıtlarını toplanan yakalama ağ ölçümleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="08711-453">Although this class is instanced, LAD does not support capturing Network metrics aggregated across all network devices.</span></span> <span data-ttu-id="08711-454">Eth0 gibi belirli bir arabirim için ölçümler elde etmek için ayarlama `"condition": "InstanceID=\\"eth0\\""`.</span><span class="sxs-lookup"><span data-stu-id="08711-454">To obtain the metrics for a specific interface, such as eth0, set `"condition": "InstanceID=\\"eth0\\""`.</span></span>

### <a name="builtin-metrics-for-the-filesystem-class"></a><span data-ttu-id="08711-455">dosya sistemi sınıfı için yerleşik ölçümleri</span><span class="sxs-lookup"><span data-stu-id="08711-455">builtin metrics for the Filesystem class</span></span>

<span data-ttu-id="08711-456">Dosya sistemi sınıfı ölçümleri filesystem kullanımı hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="08711-456">The Filesystem class of metrics provides information about filesystem usage.</span></span> <span data-ttu-id="08711-457">Mutlak ve yüzde değerleri, normal bir kullanıcıya (kök değil) görüntülenen olarak bildirilir.</span><span class="sxs-lookup"><span data-stu-id="08711-457">Absolute and percentage values are reported as they'd be displayed to an ordinary user (not root).</span></span>

<span data-ttu-id="08711-458">Sayaç</span><span class="sxs-lookup"><span data-stu-id="08711-458">counter</span></span> | <span data-ttu-id="08711-459">Anlamı</span><span class="sxs-lookup"><span data-stu-id="08711-459">Meaning</span></span>
------- | -------
<span data-ttu-id="08711-460">FreeSpace</span><span class="sxs-lookup"><span data-stu-id="08711-460">FreeSpace</span></span> | <span data-ttu-id="08711-461">Bayt cinsinden kullanılabilir disk alanı</span><span class="sxs-lookup"><span data-stu-id="08711-461">Available disk space in bytes</span></span>
<span data-ttu-id="08711-462">UsedSpace</span><span class="sxs-lookup"><span data-stu-id="08711-462">UsedSpace</span></span> | <span data-ttu-id="08711-463">Kullanılan disk alanı bayt</span><span class="sxs-lookup"><span data-stu-id="08711-463">Used disk space in bytes</span></span>
<span data-ttu-id="08711-464">PercentFreeSpace</span><span class="sxs-lookup"><span data-stu-id="08711-464">PercentFreeSpace</span></span> | <span data-ttu-id="08711-465">Boş alan yüzdesi</span><span class="sxs-lookup"><span data-stu-id="08711-465">Percentage free space</span></span>
<span data-ttu-id="08711-466">PercentUsedSpace</span><span class="sxs-lookup"><span data-stu-id="08711-466">PercentUsedSpace</span></span> | <span data-ttu-id="08711-467">Kullanılan yüzde alanı</span><span class="sxs-lookup"><span data-stu-id="08711-467">Percentage used space</span></span>
<span data-ttu-id="08711-468">PercentFreeInodes</span><span class="sxs-lookup"><span data-stu-id="08711-468">PercentFreeInodes</span></span> | <span data-ttu-id="08711-469">Kullanılmayan inode yüzdesi</span><span class="sxs-lookup"><span data-stu-id="08711-469">Percentage of unused inodes</span></span>
<span data-ttu-id="08711-470">PercentUsedInodes</span><span class="sxs-lookup"><span data-stu-id="08711-470">PercentUsedInodes</span></span> | <span data-ttu-id="08711-471">Tüm bağlanan dosya sistemlerinin arasında toplamı (kullanımda) ayrılmış inode yüzdesi</span><span class="sxs-lookup"><span data-stu-id="08711-471">Percentage of allocated (in use) inodes summed across all filesystems</span></span>
<span data-ttu-id="08711-472">BytesReadPerSecond</span><span class="sxs-lookup"><span data-stu-id="08711-472">BytesReadPerSecond</span></span> | <span data-ttu-id="08711-473">Saniye başına okunan bayt</span><span class="sxs-lookup"><span data-stu-id="08711-473">Bytes read per second</span></span>
<span data-ttu-id="08711-474">BytesWrittenPerSecond</span><span class="sxs-lookup"><span data-stu-id="08711-474">BytesWrittenPerSecond</span></span> | <span data-ttu-id="08711-475">Saniye başına yazılan bayt</span><span class="sxs-lookup"><span data-stu-id="08711-475">Bytes written per second</span></span>
<span data-ttu-id="08711-476">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="08711-476">BytesPerSecond</span></span> | <span data-ttu-id="08711-477">Okunan veya saniye başına yazılan bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="08711-477">Bytes read or written per second</span></span>
<span data-ttu-id="08711-478">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="08711-478">ReadsPerSecond</span></span> | <span data-ttu-id="08711-479">Saniye başına okuma işlemleri</span><span class="sxs-lookup"><span data-stu-id="08711-479">Read operations per second</span></span>
<span data-ttu-id="08711-480">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="08711-480">WritesPerSecond</span></span> | <span data-ttu-id="08711-481">Saniye başına işlem yazma</span><span class="sxs-lookup"><span data-stu-id="08711-481">Write operations per second</span></span>
<span data-ttu-id="08711-482">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="08711-482">TransfersPerSecond</span></span> | <span data-ttu-id="08711-483">Saniye başına okuma veya yazma işlemi</span><span class="sxs-lookup"><span data-stu-id="08711-483">Read or write operations per second</span></span>

<span data-ttu-id="08711-484">Tüm dosya sistemleri arasında toplanmış değerler elde edilebilir ayarlayarak `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="08711-484">Aggregated values across all file systems can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="08711-485">Belirli bağlı dosya sistemi için aşağıdaki gibi değerler "/ mnt", ayarlayarak elde `"condition": 'Name="/mnt"'`.</span><span class="sxs-lookup"><span data-stu-id="08711-485">Values for a specific mounted file system, such as "/mnt", can be obtained by setting `"condition": 'Name="/mnt"'`.</span></span>

### <a name="builtin-metrics-for-the-disk-class"></a><span data-ttu-id="08711-486">Disk sınıfı için yerleşik ölçümleri</span><span class="sxs-lookup"><span data-stu-id="08711-486">builtin metrics for the Disk class</span></span>

<span data-ttu-id="08711-487">Ölçümleri Disk sınıfının disk Aygıt kullanımı hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="08711-487">The Disk class of metrics provides information about disk device usage.</span></span> <span data-ttu-id="08711-488">Bu istatistikler sürücünün tamamını uygulayın.</span><span class="sxs-lookup"><span data-stu-id="08711-488">These statistics apply to the entire drive.</span></span> <span data-ttu-id="08711-489">Bir cihazda birden çok dosya sistemleri varsa, bu aygıt için sayaçları, etkili bir şekilde, bunların tümünün toplanan var.</span><span class="sxs-lookup"><span data-stu-id="08711-489">If there are multiple file systems on a device, the counters for that device are, effectively, aggregated across all of them.</span></span>

<span data-ttu-id="08711-490">Sayaç</span><span class="sxs-lookup"><span data-stu-id="08711-490">counter</span></span> | <span data-ttu-id="08711-491">Anlamı</span><span class="sxs-lookup"><span data-stu-id="08711-491">Meaning</span></span>
------- | -------
<span data-ttu-id="08711-492">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="08711-492">ReadsPerSecond</span></span> | <span data-ttu-id="08711-493">Saniye başına okuma işlemleri</span><span class="sxs-lookup"><span data-stu-id="08711-493">Read operations per second</span></span>
<span data-ttu-id="08711-494">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="08711-494">WritesPerSecond</span></span> | <span data-ttu-id="08711-495">Saniye başına işlem yazma</span><span class="sxs-lookup"><span data-stu-id="08711-495">Write operations per second</span></span>
<span data-ttu-id="08711-496">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="08711-496">TransfersPerSecond</span></span> | <span data-ttu-id="08711-497">Saniye başına toplam işlem</span><span class="sxs-lookup"><span data-stu-id="08711-497">Total operations per second</span></span>
<span data-ttu-id="08711-498">AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="08711-498">AverageReadTime</span></span> | <span data-ttu-id="08711-499">Okuma işlemi başına ortalama saniye</span><span class="sxs-lookup"><span data-stu-id="08711-499">Average seconds per read operation</span></span>
<span data-ttu-id="08711-500">AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="08711-500">AverageWriteTime</span></span> | <span data-ttu-id="08711-501">Yazma işlemi başına ortalama saniye</span><span class="sxs-lookup"><span data-stu-id="08711-501">Average seconds per write operation</span></span>
<span data-ttu-id="08711-502">AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="08711-502">AverageTransferTime</span></span> | <span data-ttu-id="08711-503">İşlem başına ortalama saniye</span><span class="sxs-lookup"><span data-stu-id="08711-503">Average seconds per operation</span></span>
<span data-ttu-id="08711-504">AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="08711-504">AverageDiskQueueLength</span></span> | <span data-ttu-id="08711-505">Sıraya alınan disk işlemleri ortalama sayısı</span><span class="sxs-lookup"><span data-stu-id="08711-505">Average number of queued disk operations</span></span>
<span data-ttu-id="08711-506">ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="08711-506">ReadBytesPerSecond</span></span> | <span data-ttu-id="08711-507">Saniye başına okunan bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="08711-507">Number of bytes read per second</span></span>
<span data-ttu-id="08711-508">WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="08711-508">WriteBytesPerSecond</span></span> | <span data-ttu-id="08711-509">Saniye başına yazılan bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="08711-509">Number of bytes written per second</span></span>
<span data-ttu-id="08711-510">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="08711-510">BytesPerSecond</span></span> | <span data-ttu-id="08711-511">Okunan veya saniye başına yazılan bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="08711-511">Number of bytes read or written per second</span></span>

<span data-ttu-id="08711-512">Tüm diskler boyunca toplanan değerler elde edilebilir ayarlayarak `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="08711-512">Aggregated values across all disks can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="08711-513">Belirli bir aygıt (örneğin, / dev/sdf1) için bilgi almak için ayarlanmış `"condition": "Name=\\"/dev/sdf1\\""`.</span><span class="sxs-lookup"><span data-stu-id="08711-513">To get information for a specific device (for example, /dev/sdf1), set `"condition": "Name=\\"/dev/sdf1\\""`.</span></span>

## <a name="installing-and-configuring-lad-30-via-cli"></a><span data-ttu-id="08711-514">Yükleme ve LAD 3.0 CLI üzerinden yapılandırma</span><span class="sxs-lookup"><span data-stu-id="08711-514">Installing and configuring LAD 3.0 via CLI</span></span>

<span data-ttu-id="08711-515">Korumalı ayarlarınızı PrivateConfig.json dosyasında ve genel yapılandırma bilgilerinizi PublicConfig.json varsayılarak, şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="08711-515">Assuming your protected settings are in the file PrivateConfig.json and your public configuration information is in PublicConfig.json, run this command:</span></span>

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

<span data-ttu-id="08711-516">Komutu, Azure CLI Azure kaynak yönetimi modunu (arm) kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="08711-516">The command assumes you are using the Azure Resource Management mode (arm) of the Azure CLI.</span></span> <span data-ttu-id="08711-517">Klasik dağıtım için LAD yapılandırmak için (ASM) VM'ler model, "asm" moda geç (`azure config mode asm`) ve kaynak grubu adı komutta atlayın.</span><span class="sxs-lookup"><span data-stu-id="08711-517">To configure LAD for classic deployment model (ASM) VMs, switch to "asm" mode (`azure config mode asm`) and omit the resource group name in the command.</span></span> <span data-ttu-id="08711-518">Daha fazla bilgi için bkz: [platformlar arası CLI belgelerine](https://docs.microsoft.com/azure/xplat-cli-connect).</span><span class="sxs-lookup"><span data-stu-id="08711-518">For more information, see the [cross-platform CLI documentation](https://docs.microsoft.com/azure/xplat-cli-connect).</span></span>

## <a name="an-example-lad-30-configuration"></a><span data-ttu-id="08711-519">Bir örnek LAD 3.0 yapılandırma</span><span class="sxs-lookup"><span data-stu-id="08711-519">An example LAD 3.0 configuration</span></span>

<span data-ttu-id="08711-520">Önceki tanımları bağlı olarak, bazı açıklama ile örnek bir LAD 3.0 uzantısı yapılandırma aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="08711-520">Based on the preceding definitions, here's a sample LAD 3.0 extension configuration with some explanation.</span></span> <span data-ttu-id="08711-521">Bu örnek çalışmanıza uygulamak için kendi depolama hesabı adı, hesap SAS belirteci ve EventHubs SAS belirteçleri kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="08711-521">To apply this sample to your case, you should use your own storage account name, account SAS token, and EventHubs SAS tokens.</span></span>

### <a name="privateconfigjson"></a><span data-ttu-id="08711-522">PrivateConfig.json</span><span class="sxs-lookup"><span data-stu-id="08711-522">PrivateConfig.json</span></span>

<span data-ttu-id="08711-523">Bu özel ayarları yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="08711-523">These private settings configure:</span></span>

* <span data-ttu-id="08711-524">bir depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="08711-524">a storage account</span></span>
* <span data-ttu-id="08711-525">eşleşen hesap SAS belirteci</span><span class="sxs-lookup"><span data-stu-id="08711-525">a matching account SAS token</span></span>
* <span data-ttu-id="08711-526">birkaç havuzlarını (JsonBlob veya EventHubs SAS belirteci ile)</span><span class="sxs-lookup"><span data-stu-id="08711-526">several sinks (JsonBlob or EventHubs with SAS tokens)</span></span>

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a><span data-ttu-id="08711-527">PublicConfig.json</span><span class="sxs-lookup"><span data-stu-id="08711-527">PublicConfig.json</span></span>

<span data-ttu-id="08711-528">Bu genel ayarları için LAD neden:</span><span class="sxs-lookup"><span data-stu-id="08711-528">These public settings cause LAD to:</span></span>

* <span data-ttu-id="08711-529">Yüzde işlemci zamanı ve kullanılan disk alanı ölçümlere karşıya `WADMetrics*` tablosu</span><span class="sxs-lookup"><span data-stu-id="08711-529">Upload percent-processor-time and used-disk-space metrics to the `WADMetrics*` table</span></span>
* <span data-ttu-id="08711-530">Syslog tesis "kullanıcı" ve önem derecesi "bilgisi" iletileri karşıya `LinuxSyslog*` tablosu</span><span class="sxs-lookup"><span data-stu-id="08711-530">Upload messages from syslog facility "user" and severity "info" to the `LinuxSyslog*` table</span></span>
* <span data-ttu-id="08711-531">Ham OMI sorgu sonuçları (PercentProcessorTime ve PercentIdleTime) adlandırılmış karşıya `LinuxCPU` tablosu</span><span class="sxs-lookup"><span data-stu-id="08711-531">Upload raw OMI query results (PercentProcessorTime and PercentIdleTime) to the named `LinuxCPU` table</span></span>
* <span data-ttu-id="08711-532">Dosyasına eklenen satır karşıya `/var/log/myladtestlog` için `MyLadTestLog` tablosu</span><span class="sxs-lookup"><span data-stu-id="08711-532">Upload appended lines in file `/var/log/myladtestlog` to the `MyLadTestLog` table</span></span>

<span data-ttu-id="08711-533">Her durumda için veri yüklenir:</span><span class="sxs-lookup"><span data-stu-id="08711-533">In each case, data is also uploaded to:</span></span>

* <span data-ttu-id="08711-534">Azure Blob storage (kapsayıcı adı: JsonBlob havuzunda tanımlandığı gibi)</span><span class="sxs-lookup"><span data-stu-id="08711-534">Azure Blob storage (container name is as defined in the JsonBlob sink)</span></span>
* <span data-ttu-id="08711-535">EventHubs uç noktası (EventHubs havuzunda belirtildiği şekilde)</span><span class="sxs-lookup"><span data-stu-id="08711-535">EventHubs endpoint (as specified in the EventHubs sink)</span></span>

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

<span data-ttu-id="08711-536">`resourceId` Yapılandırmada VM veya sanal makine ölçek kümesi aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="08711-536">The `resourceId` in the configuration must match that of the VM or the virtual machine scale set.</span></span>

* <span data-ttu-id="08711-537">Grafik ve uyarı azure platformu ölçümleri, üzerinde çalıştığınız VM ResourceId bilir.</span><span class="sxs-lookup"><span data-stu-id="08711-537">Azure platform metrics charting and alerting knows the resourceId of the VM you're working on.</span></span> <span data-ttu-id="08711-538">Verileri ResourceId kullanarak, VM için arama anahtarı bulmak bekliyor.</span><span class="sxs-lookup"><span data-stu-id="08711-538">It expects to find the data for your VM using the resourceId the lookup key.</span></span>
* <span data-ttu-id="08711-539">Azure otomatik ölçeklendirme kullanırsanız, otomatik ölçeklendirme yapılandırmasında ResourceId LAD tarafından kullanılan ResourceId eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="08711-539">If you use Azure autoscale, the resourceId in the autoscale configuration must match the resourceId used by LAD.</span></span>
* <span data-ttu-id="08711-540">ResourceId LAD tarafından yazılan JsonBlobs adlarını içinde yerleşik olarak bulunur.</span><span class="sxs-lookup"><span data-stu-id="08711-540">The resourceId is built into the names of JsonBlobs written by LAD.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="08711-541">Verilerinizi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="08711-541">View your data</span></span>

<span data-ttu-id="08711-542">Performans verilerini görüntülemek veya uyarıları ayarlamak için Azure portalını kullanın:</span><span class="sxs-lookup"><span data-stu-id="08711-542">Use the Azure portal to view performance data or set alerts:</span></span>

![Görüntü](./media/diagnostic-extension/graph_metrics.png)

<span data-ttu-id="08711-544">`performanceCounters` Verileri her zaman bir Azure Storage tablosunda depolanır.</span><span class="sxs-lookup"><span data-stu-id="08711-544">The `performanceCounters` data are always stored in an Azure Storage table.</span></span> <span data-ttu-id="08711-545">Azure depolama API'leri, birçok diller ve platformlar için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="08711-545">Azure Storage APIs are available for many languages and platforms.</span></span>

<span data-ttu-id="08711-546">JsonBlob havuzlarını gönderilen veriler adlı depolama hesabındaki BLOB depolanır [ayarların korumalı](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="08711-546">Data sent to JsonBlob sinks is stored in blobs in the storage account named in the [Protected settings](#protected-settings).</span></span> <span data-ttu-id="08711-547">Tüm Azure Blob Depolama API'leri kullanarak blob verileri kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="08711-547">You can consume the blob data using any Azure Blob Storage APIs.</span></span>

<span data-ttu-id="08711-548">Ayrıca, Azure depolama alanındaki verilere erişmek için bu UI araçları kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="08711-548">In addition, you can use these UI tools to access the data in Azure Storage:</span></span>

* <span data-ttu-id="08711-549">Visual Studio Sunucu Gezgini.</span><span class="sxs-lookup"><span data-stu-id="08711-549">Visual Studio Server Explorer.</span></span>
* <span data-ttu-id="08711-550">[Microsoft Azure Storage Gezgini](https://azurestorageexplorer.codeplex.com/ "Azure Storage Gezgini").</span><span class="sxs-lookup"><span data-stu-id="08711-550">[Microsoft Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

<span data-ttu-id="08711-551">Bu oturumunun anlık görüntüsü, bir Microsoft Azure Storage Gezgini test VM üzerinde oluşturulan Azure Storage tablolarının ve doğru yapılandırılmış bir LAD 3.0 uzantısı kapsayıcılardan gösterir.</span><span class="sxs-lookup"><span data-stu-id="08711-551">This snapshot of a Microsoft Azure Storage Explorer session shows the generated Azure Storage tables and containers from a correctly configured LAD 3.0 extension on a test VM.</span></span> <span data-ttu-id="08711-552">Görüntü ile tam olarak eşleşmiyor [örnek LAD 3.0 yapılandırma](#an-example-lad-30-configuration).</span><span class="sxs-lookup"><span data-stu-id="08711-552">The image doesn't match exactly with the [sample LAD 3.0 configuration](#an-example-lad-30-configuration).</span></span>

![Görüntü](./media/diagnostic-extension/stg_explorer.png)

<span data-ttu-id="08711-554">İlgili bkz [EventHubs belgelerine](../../event-hubs/event-hubs-what-is-event-hubs.md) EventHubs uç noktasına yayımlanan iletilerin kullanma hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="08711-554">See the relevant [EventHubs documentation](../../event-hubs/event-hubs-what-is-event-hubs.md) to learn how to consume messages published to an EventHubs endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08711-555">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="08711-555">Next steps</span></span>

* <span data-ttu-id="08711-556">Ölçüm uyarıları oluşturma [Azure İzleyici](../../monitoring-and-diagnostics/insights-alerts-portal.md) topladığınız ölçümünün.</span><span class="sxs-lookup"><span data-stu-id="08711-556">Create metric alerts in [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) for the metrics you collect.</span></span>
* <span data-ttu-id="08711-557">Oluşturma [izleme grafikleri](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) ölçümlerinizi için.</span><span class="sxs-lookup"><span data-stu-id="08711-557">Create [monitoring charts](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) for your metrics.</span></span>
* <span data-ttu-id="08711-558">Bilgi nasıl [bir sanal makine ölçek kümesi oluşturma](/azure/virtual-machines/linux/tutorial-create-vmss) ölçümlerinizi otomatik ölçeklendirmeyi denetlemek için kullanma.</span><span class="sxs-lookup"><span data-stu-id="08711-558">Learn how to [create a virtual machine scale set](/azure/virtual-machines/linux/tutorial-create-vmss) using your metrics to control autoscaling.</span></span>
