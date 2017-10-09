---
title: "aaaAzure işlem - Linux tanılama uzantısını | Microsoft Docs"
description: "Nasıl tooconfigure Azure Linux tanılama uzantısını (LAD) toocollect ölçümleri hello ve Linux Azure'da çalışan Vm'lerden gelen olayları günlüğe kaydedin."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a><span data-ttu-id="5956b-103">Linux tanılama uzantısını toomonitor ölçümleri ve günlükleri kullanın</span><span class="sxs-lookup"><span data-stu-id="5956b-103">Use Linux Diagnostic Extension toomonitor metrics and logs</span></span>

<span data-ttu-id="5956b-104">Bu belgede sürüm 3.0 ve hello Linux tanılama uzantı, daha yeni açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5956b-104">This document describes version 3.0 and newer of hello Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5956b-105">2.3 ve eski sürümü hakkında daha fazla bilgi için bkz: [bu belgeyi](./classic/diagnostic-extension-v2.md).</span><span class="sxs-lookup"><span data-stu-id="5956b-105">For information about version 2.3 and older, see [this document](./classic/diagnostic-extension-v2.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="5956b-106">Giriş</span><span class="sxs-lookup"><span data-stu-id="5956b-106">Introduction</span></span>

<span data-ttu-id="5956b-107">Merhaba Linux tanılama uzantısını Microsoft Azure üzerinde çalışan bir Linux VM kullanıcı İzleyicisi Merhaba durumunu yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="5956b-107">hello Linux Diagnostic Extension helps a user monitor hello health of a Linux VM running on Microsoft Azure.</span></span> <span data-ttu-id="5956b-108">Hello aşağıdaki özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="5956b-108">It has hello following capabilities:</span></span>

* <span data-ttu-id="5956b-109">VM hello sistem performans ölçümleri toplar ve bunları belirtilen depolama hesabı belirli bir tabloda depolar.</span><span class="sxs-lookup"><span data-stu-id="5956b-109">Collects system performance metrics from hello VM and stores them in a specific table in a designated storage account.</span></span>
* <span data-ttu-id="5956b-110">Syslog günlüğü olaylarını alır ve bunları belirli bir depolama hesabı belirlenmiş hello tabloda depolar.</span><span class="sxs-lookup"><span data-stu-id="5956b-110">Retrieves log events from syslog and stores them in a specific table in hello designated storage account.</span></span>
* <span data-ttu-id="5956b-111">Toplanan ve karşıya kullanıcılar toocustomize hello veri ölçümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="5956b-111">Enables users toocustomize hello data metrics that are collected and uploaded.</span></span>
* <span data-ttu-id="5956b-112">Kullanıcıların toocustomize hello syslog tesis ve toplanan ve karşıya olayların önem düzeyleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="5956b-112">Enables users toocustomize hello syslog facilities and severity levels of events that are collected and uploaded.</span></span>
* <span data-ttu-id="5956b-113">Kullanıcıların tooupload belirtilen günlük dosyaları tooa atanan depolama tablosu sağlar.</span><span class="sxs-lookup"><span data-stu-id="5956b-113">Enables users tooupload specified log files tooa designated storage table.</span></span>
* <span data-ttu-id="5956b-114">Ölçümleri ve günlük olayları tooarbitrary EventHub uç noktaları ve JSON biçimli BLOB'lar hello göndermeyi destekler, depolama hesabı atanmış.</span><span class="sxs-lookup"><span data-stu-id="5956b-114">Supports sending metrics and log events tooarbitrary EventHub endpoints and JSON-formatted blobs in hello designated storage account.</span></span>

<span data-ttu-id="5956b-115">Bu uzantı, hem Azure dağıtım modelleri ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="5956b-115">This extension works with both Azure deployment models.</span></span>

## <a name="installing-hello-extension-in-your-vm"></a><span data-ttu-id="5956b-116">Merhaba uzantısı VM ile yükleme</span><span class="sxs-lookup"><span data-stu-id="5956b-116">Installing hello extension in your VM</span></span>

<span data-ttu-id="5956b-117">Bu uzantı hello Azure PowerShell cmdlet'lerini, Azure CLI komut dosyaları veya Azure dağıtım şablonları kullanarak etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5956b-117">You can enable this extension by using hello Azure PowerShell cmdlets, Azure CLI scripts, or Azure deployment templates.</span></span> <span data-ttu-id="5956b-118">Daha fazla bilgi için bkz: [uzantıları özelliklerinin](./extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="5956b-118">For more information, see [Extensions Features](./extensions-features.md).</span></span>

<span data-ttu-id="5956b-119">Hello Azure portal kullanılan tooenable veya LAD 3.0 yapılandırma değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="5956b-119">hello Azure portal cannot be used tooenable or configure LAD 3.0.</span></span> <span data-ttu-id="5956b-120">Bunun yerine, yükler ve sürüm 2.3 yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="5956b-120">Instead, it installs and configures version 2.3.</span></span> <span data-ttu-id="5956b-121">Azure portal grafikleri ve uyarılar iki sürümünü de hello uzantısı verilerle çalışır.</span><span class="sxs-lookup"><span data-stu-id="5956b-121">Azure portal graphs and alerts work with data from both versions of hello extension.</span></span>

<span data-ttu-id="5956b-122">Bu yükleme yönergeleri ve [indirilebilir örnek yapılandırma](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) LAD 3.0 yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="5956b-122">These installation instructions and a [downloadable sample configuration](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configure LAD 3.0 to:</span></span>

* <span data-ttu-id="5956b-123">yakalama ve depolama ölçümler aynı LAD 2.3 tarafından sağlanan gibi hello;</span><span class="sxs-lookup"><span data-stu-id="5956b-123">capture and store hello same metrics as were provided by LAD 2.3;</span></span>
* <span data-ttu-id="5956b-124">dosya sistemi ölçümler, yeni tooLAD 3.0 yararlı bir dizi yakalama;</span><span class="sxs-lookup"><span data-stu-id="5956b-124">capture a useful set of file system metrics, new tooLAD 3.0;</span></span>
* <span data-ttu-id="5956b-125">Yakalama LAD 2.3 ile etkin hello varsayılan syslog toplama;</span><span class="sxs-lookup"><span data-stu-id="5956b-125">capture hello default syslog collection enabled by LAD 2.3;</span></span>
* <span data-ttu-id="5956b-126">Merhaba grafik ve VM ölçümleri uyarmak için Azure portal deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="5956b-126">enable hello Azure portal experience for charting and alerting on VM metrics.</span></span>

<span data-ttu-id="5956b-127">Merhaba indirilebilir yapılandırma yalnızca bir örnektir; toosuit değiştirmek, kendi gereksinimlerinizi.</span><span class="sxs-lookup"><span data-stu-id="5956b-127">hello downloadable configuration is just an example; modify it toosuit your own needs.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="5956b-128">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5956b-128">Prerequisites</span></span>

* <span data-ttu-id="5956b-129">**Azure Linux Aracısı sürüm 2.2.0 veya daha sonra**.</span><span class="sxs-lookup"><span data-stu-id="5956b-129">**Azure Linux Agent version 2.2.0 or later**.</span></span> <span data-ttu-id="5956b-130">Çoğu Azure VM Linux galeri görüntüleri sürüm 2.2.7 dahil etmek veya daha sonra.</span><span class="sxs-lookup"><span data-stu-id="5956b-130">Most Azure VM Linux gallery images include version 2.2.7 or later.</span></span> <span data-ttu-id="5956b-131">Çalıştırma `/usr/sbin/waagent -version` tooconfirm hello sürüm hello VM üzerinde yüklü.</span><span class="sxs-lookup"><span data-stu-id="5956b-131">Run `/usr/sbin/waagent -version` tooconfirm hello version installed on hello VM.</span></span> <span data-ttu-id="5956b-132">Merhaba VM hello Konuk aracısının daha eski bir sürümünü çalıştırıyorsa, izleyin [bu yönergeleri](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate onu.</span><span class="sxs-lookup"><span data-stu-id="5956b-132">If hello VM is running an older version of hello guest agent, follow [these instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate it.</span></span>
* <span data-ttu-id="5956b-133">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="5956b-133">**Azure CLI**.</span></span> <span data-ttu-id="5956b-134">[Azure CLI 2.0 Hello ayarlamak](https://docs.microsoft.com/cli/azure/install-azure-cli) makinenizde ortamı.</span><span class="sxs-lookup"><span data-stu-id="5956b-134">[Set up hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) environment on your machine.</span></span>
* <span data-ttu-id="5956b-135">zaten yoksa wget komutu Hello: çalıştırmak `sudo apt-get install wget`.</span><span class="sxs-lookup"><span data-stu-id="5956b-135">hello wget command, if you don't already have it: Run `sudo apt-get install wget`.</span></span>
* <span data-ttu-id="5956b-136">Var olan bir Azure aboneliği ve mevcut bir depolama hesabı içinde toostore hello veri.</span><span class="sxs-lookup"><span data-stu-id="5956b-136">An existing Azure subscription and an existing storage account within it toostore hello data.</span></span>

### <a name="sample-installation"></a><span data-ttu-id="5956b-137">Örnek yükleme</span><span class="sxs-lookup"><span data-stu-id="5956b-137">Sample installation</span></span>

<span data-ttu-id="5956b-138">Merhaba doğru parametreleri hello üzerinde ilk üç satırını doldurun, sonra da kök olarak bu betiği yürütün:</span><span class="sxs-lookup"><span data-stu-id="5956b-138">Fill in hello correct parameters on hello first three lines, then execute this script as root:</span></span>

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

<span data-ttu-id="5956b-139">Merhaba örnek yapılandırma Hello URL'sini ve içeriğini, konu toochange var.</span><span class="sxs-lookup"><span data-stu-id="5956b-139">hello URL for hello sample configuration, and its contents, are subject toochange.</span></span> <span data-ttu-id="5956b-140">Merhaba portal ayarları JSON dosyasının bir kopyasını indirin ve gereksinimlerinize göre özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="5956b-140">Download a copy of hello portal settings JSON file and customize it for your needs.</span></span> <span data-ttu-id="5956b-141">Tüm Şablonları ya da Otomasyon, oluşturmak, her zaman bu URL'yi indirmek yerine kendi kopyanızı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5956b-141">Any templates or automation you construct should use your own copy, rather than downloading that URL each time.</span></span>

### <a name="updating-hello-extension-settings"></a><span data-ttu-id="5956b-142">Merhaba uzantısı ayarları güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="5956b-142">Updating hello extension settings</span></span>

<span data-ttu-id="5956b-143">Korumalı veya genel ayarları değiştirdikten sonra bunları toohello VM çalıştırarak dağıtma hello aynı komutu.</span><span class="sxs-lookup"><span data-stu-id="5956b-143">After you've changed your Protected or Public settings, deploy them toohello VM by running hello same command.</span></span> <span data-ttu-id="5956b-144">Herhangi bir şey hello ayarlarını değiştirdiyseniz, güncelleştirilmiş hello ayarları toohello uzantısı gönderilir.</span><span class="sxs-lookup"><span data-stu-id="5956b-144">If anything changed in hello settings, hello updated settings are sent toohello extension.</span></span> <span data-ttu-id="5956b-145">LAD hello yapılandırma yeniden yükler ve kendisini yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="5956b-145">LAD reloads hello configuration and restarts itself.</span></span>

### <a name="migration-from-previous-versions-of-hello-extension"></a><span data-ttu-id="5956b-146">Merhaba uzantısı eski sürümlerinden geçiş</span><span class="sxs-lookup"><span data-stu-id="5956b-146">Migration from previous versions of hello extension</span></span>

<span data-ttu-id="5956b-147">Merhaba uzantısı'nın en son sürüm Hello **3.0**.</span><span class="sxs-lookup"><span data-stu-id="5956b-147">hello latest version of hello extension is **3.0**.</span></span> <span data-ttu-id="5956b-148">**Eski sürümlerini (2.x) kullanım dışıdır ve ve 31 Temmuz 2018 sonrasında yayımdan**.</span><span class="sxs-lookup"><span data-stu-id="5956b-148">**Any old versions (2.x) are deprecated and may be unpublished on or after July 31, 2018**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5956b-149">Bu uzantı hello uzantısı'nın en son değişiklikleri toohello yapılandırma tanıtır.</span><span class="sxs-lookup"><span data-stu-id="5956b-149">This extension introduces breaking changes toohello configuration of hello extension.</span></span> <span data-ttu-id="5956b-150">Bu tür bir değişiklik tooimprove hello güvenlik hello uzantısının bulunuldu; Sonuç olarak, geriye dönük uyumluluk 2.x ile korunmasını değil.</span><span class="sxs-lookup"><span data-stu-id="5956b-150">One such change was made tooimprove hello security of hello extension; as a result, backwards compatibility with 2.x could not be maintained.</span></span> <span data-ttu-id="5956b-151">Ayrıca, bu uzantı için uzantı yayımcı hello hello yayımcı hello 2.x sürümleri için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="5956b-151">Also, hello Extension Publisher for this extension is different than hello publisher for hello 2.x versions.</span></span>
>
> <span data-ttu-id="5956b-152">toomigrate sürümünden 2.x toothis yeni hello uzantısı hello eski uzantısı (altında hello eski Yayımcı adı) ve ardından hello uzantısı 3 sürümünü yükleyin kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5956b-152">toomigrate from 2.x toothis new version of hello extension, you must uninstall hello old extension (under hello old publisher name), then install version 3 of hello extension.</span></span>

<span data-ttu-id="5956b-153">Öneriler:</span><span class="sxs-lookup"><span data-stu-id="5956b-153">Recommendations:</span></span>

* <span data-ttu-id="5956b-154">Merhaba uzantı etkin otomatik alt sürüm yükseltme işlemine yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5956b-154">Install hello extension with automatic minor version upgrade enabled.</span></span>
  * <span data-ttu-id="5956b-155">Merhaba uzantısı Azure XPLAT CLI veya Powershell aracılığıyla yüklüyorsanız, Klasik dağıtım modeli VM'ler, '3.*' hello sürüm olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="5956b-155">On classic deployment model VMs, specify '3.*' as hello version if you are installing hello extension through Azure XPLAT CLI or Powershell.</span></span>
  * <span data-ttu-id="5956b-156">Sanal makineleri üzerinde Azure Resource Manager dağıtım modeli, dahil ' "olan": true' hello VM Dağıtım şablonu olarak.</span><span class="sxs-lookup"><span data-stu-id="5956b-156">On Azure Resource Manager deployment model VMs, include '"autoUpgradeMinorVersion": true' in hello VM deployment template.</span></span>
* <span data-ttu-id="5956b-157">Yeni/farklı bir depolama hesabı LAD 3.0 için kullanın.</span><span class="sxs-lookup"><span data-stu-id="5956b-157">Use a new/different storage account for LAD 3.0.</span></span> <span data-ttu-id="5956b-158">Bir hesap sorunlu paylaşımı olun birkaç küçük uyumsuzlukları LAD 2.3 LAD 3.0 arasındaki vardır:</span><span class="sxs-lookup"><span data-stu-id="5956b-158">There are several small incompatibilities between LAD 2.3 and LAD 3.0 that make sharing an account troublesome:</span></span>
  * <span data-ttu-id="5956b-159">LAD 3.0 syslog olayları farklı bir ada sahip bir tablo olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="5956b-159">LAD 3.0 stores syslog events in a table with a different name.</span></span>
  * <span data-ttu-id="5956b-160">Merhaba counterSpecifier dizeleri için `builtin` ölçümleri farklı LAD 3. 0 '.</span><span class="sxs-lookup"><span data-stu-id="5956b-160">hello counterSpecifier strings for `builtin` metrics differ in LAD 3.0.</span></span>

## <a name="protected-settings"></a><span data-ttu-id="5956b-161">Korumalı ayarları</span><span class="sxs-lookup"><span data-stu-id="5956b-161">Protected settings</span></span>

<span data-ttu-id="5956b-162">Bu yapılandırma bilgileri kümesi genel görünümünde, örneğin, depolama kimlik korunması gereken hassas bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="5956b-162">This set of configuration information contains sensitive information that should be protected from public view, for example, storage credentials.</span></span> <span data-ttu-id="5956b-163">Bu ayarları şifreli biçimde hello uzantısı tarafından depolanan iletilen tooand verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="5956b-163">These settings are transmitted tooand stored by hello extension in encrypted form.</span></span>

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

<span data-ttu-id="5956b-164">Ad</span><span class="sxs-lookup"><span data-stu-id="5956b-164">Name</span></span> | <span data-ttu-id="5956b-165">Değer</span><span class="sxs-lookup"><span data-stu-id="5956b-165">Value</span></span>
---- | -----
<span data-ttu-id="5956b-166">storageAccountName</span><span class="sxs-lookup"><span data-stu-id="5956b-166">storageAccountName</span></span> | <span data-ttu-id="5956b-167">Veri hello uzantısı tarafından yazılmış hello depolama hesabı Hello adı.</span><span class="sxs-lookup"><span data-stu-id="5956b-167">hello name of hello storage account in which data is written by hello extension.</span></span>
<span data-ttu-id="5956b-168">storageAccountEndPoint</span><span class="sxs-lookup"><span data-stu-id="5956b-168">storageAccountEndPoint</span></span> | <span data-ttu-id="5956b-169">(isteğe bağlı) hello uç noktası hangi hello depolama hesabı zaten hello bulut tanımlama.</span><span class="sxs-lookup"><span data-stu-id="5956b-169">(optional) hello endpoint identifying hello cloud in which hello storage account exists.</span></span> <span data-ttu-id="5956b-170">Bu ayar olmazsa LAD toohello Azure genel bulutunda, varsayılan olarak `https://core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="5956b-170">If this setting is absent, LAD defaults toohello Azure public cloud, `https://core.windows.net`.</span></span> <span data-ttu-id="5956b-171">toouse bir depolama hesabı Azure Almanya, Azure kamu ya da Azure Çin'de, bu değeri uygun şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5956b-171">toouse a storage account in Azure Germany, Azure Government, or Azure China, set this value accordingly.</span></span>
<span data-ttu-id="5956b-172">storageAccountSasToken</span><span class="sxs-lookup"><span data-stu-id="5956b-172">storageAccountSasToken</span></span> | <span data-ttu-id="5956b-173">Bir [hesap SAS belirteci](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) Blob ve tablo hizmeti (`ss='bt'`), geçerli toocontainers ve nesneler (`srt='co'`), hangi verir ekleyin, oluşturmak, liste, güncelleştirme ve yazma izinleri (`sp='acluw'`).</span><span class="sxs-lookup"><span data-stu-id="5956b-173">An [Account SAS token](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) for Blob and Table services (`ss='bt'`), applicable toocontainers and objects (`srt='co'`), which grants add, create, list, update, and write permissions (`sp='acluw'`).</span></span> <span data-ttu-id="5956b-174">Yapmak *değil* hello başında soru işareti (?) içerir.</span><span class="sxs-lookup"><span data-stu-id="5956b-174">Do *not* include hello leading question-mark (?).</span></span>
<span data-ttu-id="5956b-175">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="5956b-175">mdsdHttpProxy</span></span> | <span data-ttu-id="5956b-176">(isteğe bağlı) HTTP proxy gerekli bilgileri tooenable hello uzantısı tooconnect toohello belirtilen depolama hesabı ve uç nokta.</span><span class="sxs-lookup"><span data-stu-id="5956b-176">(optional) HTTP proxy information needed tooenable hello extension tooconnect toohello specified storage account and endpoint.</span></span>
<span data-ttu-id="5956b-177">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="5956b-177">sinksConfig</span></span> | <span data-ttu-id="5956b-178">(isteğe bağlı) Alternatif hedefleri toowhich ölçümleri ve olayları ayrıntılarını alınabilir.</span><span class="sxs-lookup"><span data-stu-id="5956b-178">(optional) Details of alternative destinations toowhich metrics and events can be delivered.</span></span> <span data-ttu-id="5956b-179">Merhaba uzantısı tarafından desteklenen her veri havuzu belirli ayrıntılarını Hello izleyen hello bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="5956b-179">hello specific details of each data sink supported by hello extension are covered in hello sections that follow.</span></span>

<span data-ttu-id="5956b-180">Gerekli hello SAS belirteci hello Azure portal aracılığıyla kolayca oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5956b-180">You can easily construct hello required SAS token through hello Azure portal.</span></span>

1. <span data-ttu-id="5956b-181">Merhaba uzantısı toowrite istediğiniz hello genel amaçlı depolama hesabı toowhich seçin</span><span class="sxs-lookup"><span data-stu-id="5956b-181">Select hello general-purpose storage account toowhich you want hello extension toowrite</span></span>
1. <span data-ttu-id="5956b-182">"Hello ayarları bölümünden hello soldaki menüden erişim imzası paylaşılan" seçin</span><span class="sxs-lookup"><span data-stu-id="5956b-182">Select "Shared access signature" from hello Settings part of hello left menu</span></span>
1. <span data-ttu-id="5956b-183">Daha önce açıklandığı gibi hello uygun bölümleri olun</span><span class="sxs-lookup"><span data-stu-id="5956b-183">Make hello appropriate sections as previously described</span></span>
1. <span data-ttu-id="5956b-184">Merhaba "SAS oluştur" düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5956b-184">Click hello "Generate SAS" button.</span></span>

![Görüntü](./media/diagnostic-extension/make_sas.png)

<span data-ttu-id="5956b-186">Kopya hello SAS hello storageAccountSasToken alanına oluşturulan; Merhaba başında soru işareti kaldırın ("?").</span><span class="sxs-lookup"><span data-stu-id="5956b-186">Copy hello generated SAS into hello storageAccountSasToken field; remove hello leading question-mark ("?").</span></span>

### <a name="sinksconfig"></a><span data-ttu-id="5956b-187">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="5956b-187">sinksConfig</span></span>

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

<span data-ttu-id="5956b-188">Bu isteğe bağlı bir bölüm toowhich hello uzantısı topladığı hello bilgileri gönderir ek hedefleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5956b-188">This optional section defines additional destinations toowhich hello extension sends hello information it collects.</span></span> <span data-ttu-id="5956b-189">Merhaba "havuz" dizi her ek veri havuzu için bir nesne içeriyor.</span><span class="sxs-lookup"><span data-stu-id="5956b-189">hello "sink" array contains an object for each additional data sink.</span></span> <span data-ttu-id="5956b-190">Merhaba diğer öznitelikleri hello nesnesindeki hello "tür" özniteliği belirler.</span><span class="sxs-lookup"><span data-stu-id="5956b-190">hello "type" attribute determines hello other attributes in hello object.</span></span>

<span data-ttu-id="5956b-191">Öğesi</span><span class="sxs-lookup"><span data-stu-id="5956b-191">Element</span></span> | <span data-ttu-id="5956b-192">Değer</span><span class="sxs-lookup"><span data-stu-id="5956b-192">Value</span></span>
------- | -----
<span data-ttu-id="5956b-193">ad</span><span class="sxs-lookup"><span data-stu-id="5956b-193">name</span></span> | <span data-ttu-id="5956b-194">Bir dize toorefer toothis havuz hello uzantı yapılandırmasındaki başka bir yerde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5956b-194">A string used toorefer toothis sink elsewhere in hello extension configuration.</span></span>
<span data-ttu-id="5956b-195">type</span><span class="sxs-lookup"><span data-stu-id="5956b-195">type</span></span> | <span data-ttu-id="5956b-196">Havuz tanımlanmakta Hello türü.</span><span class="sxs-lookup"><span data-stu-id="5956b-196">hello type of sink being defined.</span></span> <span data-ttu-id="5956b-197">Diğer değerleri (varsa) hello bu tür durumlarda belirler.</span><span class="sxs-lookup"><span data-stu-id="5956b-197">Determines hello other values (if any) in instances of this type.</span></span>

<span data-ttu-id="5956b-198">Merhaba Linux tanılama uzantısını 3.0 sürümünü iki havuz türlerini destekler: EventHub ve JsonBlob.</span><span class="sxs-lookup"><span data-stu-id="5956b-198">Version 3.0 of hello Linux Diagnostic Extension supports two sink types: EventHub, and JsonBlob.</span></span>

#### <a name="hello-eventhub-sink"></a><span data-ttu-id="5956b-199">Merhaba EventHub havuz</span><span class="sxs-lookup"><span data-stu-id="5956b-199">hello EventHub sink</span></span>

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

<span data-ttu-id="5956b-200">Merhaba "sasURL" giriş hello olay hub'ı toowhich veri için SAS belirteci dahil tam URL'yi yayınlanmalıdır hello içeriyor.</span><span class="sxs-lookup"><span data-stu-id="5956b-200">hello "sasURL" entry contains hello full URL, including SAS token, for hello Event Hub toowhich data should be published.</span></span> <span data-ttu-id="5956b-201">LAD hello gönderme talep sağlayan bir ilke adlandırma SAS gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5956b-201">LAD requires a SAS naming a policy that enables hello Send claim.</span></span> <span data-ttu-id="5956b-202">Örnek:</span><span class="sxs-lookup"><span data-stu-id="5956b-202">An example:</span></span>

* <span data-ttu-id="5956b-203">Adlı bir olay hub'ları ad alanı oluşturma`contosohub`</span><span class="sxs-lookup"><span data-stu-id="5956b-203">Create an Event Hubs namespace called `contosohub`</span></span>
* <span data-ttu-id="5956b-204">Adlı hello ad alanında bir olay hub'ı oluşturma`syslogmsgs`</span><span class="sxs-lookup"><span data-stu-id="5956b-204">Create an Event Hub in hello namespace called `syslogmsgs`</span></span>
* <span data-ttu-id="5956b-205">Olay Hub'ın adlandırılmış hello üzerinde bir paylaşılan erişim ilkesi oluşturun `writer` etkinleştirir gönderme talep hello</span><span class="sxs-lookup"><span data-stu-id="5956b-205">Create a Shared access policy on hello Event Hub named `writer` that enables hello Send claim</span></span>

<span data-ttu-id="5956b-206">Bir SAS iyi 1 Ocak 2018 gece yarısı UTC kadar oluşturduysanız hello sasURL değeri olabilir:</span><span class="sxs-lookup"><span data-stu-id="5956b-206">If you created a SAS good until midnight UTC on January 1, 2018, hello sasURL value might be:</span></span>

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

<span data-ttu-id="5956b-207">Olay hub'ları için SAS belirteci oluşturma hakkında daha fazla bilgi için bkz: [bu web sayfası](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5956b-207">For more information about generating SAS tokens for Event Hubs, see [this web page](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span></span>

#### <a name="hello-jsonblob-sink"></a><span data-ttu-id="5956b-208">Merhaba JsonBlob havuz</span><span class="sxs-lookup"><span data-stu-id="5956b-208">hello JsonBlob sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

<span data-ttu-id="5956b-209">Veri yönergelerine uygun tooa JsonBlob havuz BLOB'ları Azure depolama alanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="5956b-209">Data directed tooa JsonBlob sink is stored in blobs in Azure storage.</span></span> <span data-ttu-id="5956b-210">Her örneği LAD blob her saat için her bir havuz adı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5956b-210">Each instance of LAD creates a blob every hour for each sink name.</span></span> <span data-ttu-id="5956b-211">Her bir blob her zaman nesne sözdizimsel olarak geçerli bir JSON dizisi içerir.</span><span class="sxs-lookup"><span data-stu-id="5956b-211">Each blob always contains a syntactically valid JSON array of object.</span></span> <span data-ttu-id="5956b-212">Yeni girişler toohello dizi otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="5956b-212">New entries are atomically added toohello array.</span></span> <span data-ttu-id="5956b-213">BLOB'ları bir kapsayıcıda hello hello havuzu olarak aynı ad ile depolanır.</span><span class="sxs-lookup"><span data-stu-id="5956b-213">Blobs are stored in a container with hello same name as hello sink.</span></span> <span data-ttu-id="5956b-214">BLOB kapsayıcı adları JsonBlob havuzlarını toohello adlarını uygulamak için Azure depolama kuralları hello: küçük harf alfasayısal ASCII karakterler veya tire 3 ile 63 arasında.</span><span class="sxs-lookup"><span data-stu-id="5956b-214">hello Azure storage rules for blob container names apply toohello names of JsonBlob sinks: between 3 and 63 lower-case alphanumeric ASCII characters or dashes.</span></span>

## <a name="public-settings"></a><span data-ttu-id="5956b-215">Genel ayarları</span><span class="sxs-lookup"><span data-stu-id="5956b-215">Public settings</span></span>

<span data-ttu-id="5956b-216">Bu yapı çeşitli bloklarını hello uzantısı tarafından toplanan hello bilgiler denetleyen ayarları içerir.</span><span class="sxs-lookup"><span data-stu-id="5956b-216">This structure contains various blocks of settings that control hello information collected by hello extension.</span></span> <span data-ttu-id="5956b-217">Her ayar isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="5956b-217">Each setting is optional.</span></span> <span data-ttu-id="5956b-218">Belirtirseniz `ladCfg`, de belirtmeniz gerekir `StorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="5956b-218">If you specify `ladCfg`, you must also specify `StorageAccount`.</span></span>

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

<span data-ttu-id="5956b-219">Öğesi</span><span class="sxs-lookup"><span data-stu-id="5956b-219">Element</span></span> | <span data-ttu-id="5956b-220">Değer</span><span class="sxs-lookup"><span data-stu-id="5956b-220">Value</span></span>
------- | -----
<span data-ttu-id="5956b-221">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="5956b-221">StorageAccount</span></span> | <span data-ttu-id="5956b-222">Veri hello uzantısı tarafından yazılmış hello depolama hesabı Hello adı.</span><span class="sxs-lookup"><span data-stu-id="5956b-222">hello name of hello storage account in which data is written by hello extension.</span></span> <span data-ttu-id="5956b-223">Olmalıdır hello belirtildiği gibi aynı adı hello [ayarların korumalı](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="5956b-223">Must be hello same name as is specified in hello [Protected settings](#protected-settings).</span></span>
<span data-ttu-id="5956b-224">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="5956b-224">mdsdHttpProxy</span></span> | <span data-ttu-id="5956b-225">(isteğe bağlı) Merhaba olduğu gibi aynı [ayarların korumalı](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="5956b-225">(optional) Same as in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="5956b-226">Merhaba ortak değer varsa hello özel değer tarafından geçersiz ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5956b-226">hello public value is overridden by hello private value, if set.</span></span> <span data-ttu-id="5956b-227">Yerleştirin bir Parolada hello gibi bir gizlilik içeren proxy ayarlarını [ayarların korumalı](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="5956b-227">Place proxy settings that contain a secret, such as a password, in hello [Protected settings](#protected-settings).</span></span>

<span data-ttu-id="5956b-228">Aşağıdaki bölümlerde hello ayrıntılı Hello kalan öğeleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5956b-228">hello remaining elements are described in detail in hello following sections.</span></span>

### <a name="ladcfg"></a><span data-ttu-id="5956b-229">ladCfg</span><span class="sxs-lookup"><span data-stu-id="5956b-229">ladCfg</span></span>

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

<span data-ttu-id="5956b-230">Bu isteğe bağlı yapısı denetimleri hello toplama ölçümleri ve teslimat toohello Azure ölçümleri hizmeti ve tooother veri günlüklerini iç havuzlar.</span><span class="sxs-lookup"><span data-stu-id="5956b-230">This optional structure controls hello gathering of metrics and logs for delivery toohello Azure Metrics service and tooother data sinks.</span></span> <span data-ttu-id="5956b-231">Ya da belirtmeniz gerekir `performanceCounters` veya `syslogEvents` veya her ikisini de.</span><span class="sxs-lookup"><span data-stu-id="5956b-231">You must specify either `performanceCounters` or `syslogEvents` or both.</span></span> <span data-ttu-id="5956b-232">Merhaba belirtmelisiniz `metrics` yapısı.</span><span class="sxs-lookup"><span data-stu-id="5956b-232">You must specify hello `metrics` structure.</span></span>

<span data-ttu-id="5956b-233">Öğesi</span><span class="sxs-lookup"><span data-stu-id="5956b-233">Element</span></span> | <span data-ttu-id="5956b-234">Değer</span><span class="sxs-lookup"><span data-stu-id="5956b-234">Value</span></span>
------- | -----
<span data-ttu-id="5956b-235">eventVolume</span><span class="sxs-lookup"><span data-stu-id="5956b-235">eventVolume</span></span> | <span data-ttu-id="5956b-236">(isteğe bağlı) Denetimleri hello depolama tablo içinde oluşturulan bölüm sayısı hello.</span><span class="sxs-lookup"><span data-stu-id="5956b-236">(optional) Controls hello number of partitions created within hello storage table.</span></span> <span data-ttu-id="5956b-237">Biri olmalıdır `"Large"`, `"Medium"`, veya `"Small"`.</span><span class="sxs-lookup"><span data-stu-id="5956b-237">Must be one of `"Large"`, `"Medium"`, or `"Small"`.</span></span> <span data-ttu-id="5956b-238">Belirtilmezse, hello varsayılan değerdir `"Medium"`.</span><span class="sxs-lookup"><span data-stu-id="5956b-238">If not specified, hello default value is `"Medium"`.</span></span>
<span data-ttu-id="5956b-239">sampleRateInSeconds</span><span class="sxs-lookup"><span data-stu-id="5956b-239">sampleRateInSeconds</span></span> | <span data-ttu-id="5956b-240">Ham (unaggregated) ölçümleri topluluğu arasındaki (isteğe bağlı) hello varsayılan zaman aralığı.</span><span class="sxs-lookup"><span data-stu-id="5956b-240">(optional) hello default interval between collection of raw (unaggregated) metrics.</span></span> <span data-ttu-id="5956b-241">desteklenen hello en küçük örnek hızı 15 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="5956b-241">hello smallest supported sample rate is 15 seconds.</span></span> <span data-ttu-id="5956b-242">Belirtilmezse, hello varsayılan değerdir `15`.</span><span class="sxs-lookup"><span data-stu-id="5956b-242">If not specified, hello default value is `15`.</span></span>

#### <a name="metrics"></a><span data-ttu-id="5956b-243">metrics</span><span class="sxs-lookup"><span data-stu-id="5956b-243">metrics</span></span>

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

<span data-ttu-id="5956b-244">Öğesi</span><span class="sxs-lookup"><span data-stu-id="5956b-244">Element</span></span> | <span data-ttu-id="5956b-245">Değer</span><span class="sxs-lookup"><span data-stu-id="5956b-245">Value</span></span>
------- | -----
<span data-ttu-id="5956b-246">resourceId</span><span class="sxs-lookup"><span data-stu-id="5956b-246">resourceId</span></span> | <span data-ttu-id="5956b-247">Hello Azure Resource Manager kaynak kimliği hello VM veya hello sanal makine ölçek VM ait toowhich hello ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5956b-247">hello Azure Resource Manager resource ID of hello VM or of hello virtual machine scale set toowhich hello VM belongs.</span></span> <span data-ttu-id="5956b-248">Bu ayar olmalıdır herhangi JsonBlob havuz hello yapılandırmada kullanılıp kullanılmayacağını da belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="5956b-248">This setting must be also specified if any JsonBlob sink is used in hello configuration.</span></span>
<span data-ttu-id="5956b-249">scheduledTransferPeriod</span><span class="sxs-lookup"><span data-stu-id="5956b-249">scheduledTransferPeriod</span></span> | <span data-ttu-id="5956b-250">Birleşik ölçümleri toobe olduğu hello sıklığı hesaplanan ve 8601 olduğu zaman aralığı ifade edilen tooAzure ölçümleri, aktarılır.</span><span class="sxs-lookup"><span data-stu-id="5956b-250">hello frequency at which aggregate metrics are toobe computed and transferred tooAzure Metrics, expressed as an IS 8601 time interval.</span></span> <span data-ttu-id="5956b-251">Merhaba en küçük aktarım süresi 60, diğer bir deyişle, PT1M saniyedir.</span><span class="sxs-lookup"><span data-stu-id="5956b-251">hello smallest transfer period is 60 seconds, that is, PT1M.</span></span> <span data-ttu-id="5956b-252">En az bir scheduledTransferPeriod belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5956b-252">You must specify at least one scheduledTransferPeriod.</span></span>

<span data-ttu-id="5956b-253">Merhaba performans sayaçları bölümünde belirtilen ölçümleri 15 dakikada toplanır hello veya hello sayaç için açıkça tanımlanmış hello örnek hızı örnekleri.</span><span class="sxs-lookup"><span data-stu-id="5956b-253">Samples of hello metrics specified in hello performanceCounters section are collected every 15 seconds or at hello sample rate explicitly defined for hello counter.</span></span> <span data-ttu-id="5956b-254">Birden çok scheduledTransferPeriod sıklıklarını (Merhaba örnekte olduğu gibi) görünüyorsa, her bir toplama bağımsız olarak hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="5956b-254">If multiple scheduledTransferPeriod frequencies appear (as in hello example), each aggregation is computed independently.</span></span>

#### <a name="performancecounters"></a><span data-ttu-id="5956b-255">performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="5956b-255">performanceCounters</span></span>

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

<span data-ttu-id="5956b-256">Bu isteğe bağlı bir bölüm ölçümleri hello koleksiyonunu denetler.</span><span class="sxs-lookup"><span data-stu-id="5956b-256">This optional section controls hello collection of metrics.</span></span> <span data-ttu-id="5956b-257">Ham örnekleri her biri için toplanmış [scheduledTransferPeriod](#metrics) tooproduce bu değerler:</span><span class="sxs-lookup"><span data-stu-id="5956b-257">Raw samples are aggregated for each [scheduledTransferPeriod](#metrics) tooproduce these values:</span></span>

* <span data-ttu-id="5956b-258">Ortalama</span><span class="sxs-lookup"><span data-stu-id="5956b-258">mean</span></span>
* <span data-ttu-id="5956b-259">en az</span><span class="sxs-lookup"><span data-stu-id="5956b-259">minimum</span></span>
* <span data-ttu-id="5956b-260">Maksimum</span><span class="sxs-lookup"><span data-stu-id="5956b-260">maximum</span></span>
* <span data-ttu-id="5956b-261">Son toplanan değeri</span><span class="sxs-lookup"><span data-stu-id="5956b-261">last-collected value</span></span>
* <span data-ttu-id="5956b-262">kullanılan toocompute hello toplam ham örnekleri sayısı</span><span class="sxs-lookup"><span data-stu-id="5956b-262">count of raw samples used toocompute hello aggregate</span></span>

<span data-ttu-id="5956b-263">Öğesi</span><span class="sxs-lookup"><span data-stu-id="5956b-263">Element</span></span> | <span data-ttu-id="5956b-264">Değer</span><span class="sxs-lookup"><span data-stu-id="5956b-264">Value</span></span>
------- | -----
<span data-ttu-id="5956b-265">İç havuzlar</span><span class="sxs-lookup"><span data-stu-id="5956b-265">sinks</span></span> | <span data-ttu-id="5956b-266">(isteğe bağlı) Adlarının virgülle ayrılmış bir liste iç havuzlar toowhich LAD toplanmış ölçüm sonuçlarını gönderir.</span><span class="sxs-lookup"><span data-stu-id="5956b-266">(optional) A comma-separated list of names of sinks toowhich LAD sends aggregated metric results.</span></span> <span data-ttu-id="5956b-267">Tüm toplanan ölçümler listelenen yayımlanan tooeach havuz ' dir.</span><span class="sxs-lookup"><span data-stu-id="5956b-267">All aggregated metrics are published tooeach listed sink.</span></span> <span data-ttu-id="5956b-268">Bkz: [sinksConfig](#sinksconfig).</span><span class="sxs-lookup"><span data-stu-id="5956b-268">See [sinksConfig](#sinksconfig).</span></span> <span data-ttu-id="5956b-269">Örnek: `"EHsink1, myjsonsink"`.</span><span class="sxs-lookup"><span data-stu-id="5956b-269">Example: `"EHsink1, myjsonsink"`.</span></span>
<span data-ttu-id="5956b-270">type</span><span class="sxs-lookup"><span data-stu-id="5956b-270">type</span></span> | <span data-ttu-id="5956b-271">Merhaba ölçüsünün Hello gerçek sağlayıcısını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5956b-271">Identifies hello actual provider of hello metric.</span></span>
<span data-ttu-id="5956b-272">sınıfı</span><span class="sxs-lookup"><span data-stu-id="5956b-272">class</span></span> | <span data-ttu-id="5956b-273">"Sayacı birlikte" Merhaba belirli ölçüm hello sağlayıcının ad alanı içindeki tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5956b-273">Together with "counter", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="5956b-274">Sayaç</span><span class="sxs-lookup"><span data-stu-id="5956b-274">counter</span></span> | <span data-ttu-id="5956b-275">"Sınıf ile birlikte" Merhaba belirli ölçüm hello sağlayıcının ad alanı içindeki tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5956b-275">Together with "class", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="5956b-276">counterSpecifier</span><span class="sxs-lookup"><span data-stu-id="5956b-276">counterSpecifier</span></span> | <span data-ttu-id="5956b-277">Merhaba belirli ölçüm hello Azure ölçümleri ad alanı içindeki tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5956b-277">Identifies hello specific metric within hello Azure Metrics namespace.</span></span>
<span data-ttu-id="5956b-278">Koşul</span><span class="sxs-lookup"><span data-stu-id="5956b-278">condition</span></span> | <span data-ttu-id="5956b-279">(isteğe bağlı) Bu nesnenin tüm örneklerde toplama seçer hello veya seçer hello nesne toowhich hello ölçüm belirli bir örneği uygular.</span><span class="sxs-lookup"><span data-stu-id="5956b-279">(optional) Selects a specific instance of hello object toowhich hello metric applies or selects hello aggregation across all instances of that object.</span></span> <span data-ttu-id="5956b-280">Daha fazla bilgi için bkz: Merhaba [ `builtin` ölçüm tanımlarını](#metrics-supported-by-builtin).</span><span class="sxs-lookup"><span data-stu-id="5956b-280">For more information, see hello [`builtin` metric definitions](#metrics-supported-by-builtin).</span></span>
<span data-ttu-id="5956b-281">sampleRate</span><span class="sxs-lookup"><span data-stu-id="5956b-281">sampleRate</span></span> | <span data-ttu-id="5956b-282">Bu ölçüm için ham örnek toplanan hello oranı ayarlar 8601 aralığı BELİRTİR.</span><span class="sxs-lookup"><span data-stu-id="5956b-282">IS 8601 interval that sets hello rate at which raw samples for this metric are collected.</span></span> <span data-ttu-id="5956b-283">Ayarlanmadı, hello toplama aralığı başlangıç değeri olarak ayarlanmış olup olmadığını [sampleRateInSeconds](#ladcfg).</span><span class="sxs-lookup"><span data-stu-id="5956b-283">If not set, hello collection interval is set by hello value of [sampleRateInSeconds](#ladcfg).</span></span> <span data-ttu-id="5956b-284">Merhaba kısa desteklenen örnek hızı 15 saniye (PT15S) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5956b-284">hello shortest supported sample rate is 15 seconds (PT15S).</span></span>
<span data-ttu-id="5956b-285">Birim</span><span class="sxs-lookup"><span data-stu-id="5956b-285">unit</span></span> | <span data-ttu-id="5956b-286">Bu dizeler biri olmalıdır: "Count", "Bayt sayısı", "Saniye", "Yüzde", "CountPerSecond", "BytesPerSecond", "Milisaniyelik".</span><span class="sxs-lookup"><span data-stu-id="5956b-286">Should be one of these strings: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span></span> <span data-ttu-id="5956b-287">Merhaba ölçüm için Hello birimi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5956b-287">Defines hello unit for hello metric.</span></span> <span data-ttu-id="5956b-288">Merhaba, bu birim veri değerleri toomatch toplanan hello toplanan veri tüketicileri bekler.</span><span class="sxs-lookup"><span data-stu-id="5956b-288">Consumers of hello collected data expect hello collected data values toomatch this unit.</span></span> <span data-ttu-id="5956b-289">Bu alan LAD yoksayar.</span><span class="sxs-lookup"><span data-stu-id="5956b-289">LAD ignores this field.</span></span>
<span data-ttu-id="5956b-290">Görünen adı</span><span class="sxs-lookup"><span data-stu-id="5956b-290">displayName</span></span> | <span data-ttu-id="5956b-291">Merhaba etiketinde (Merhaba ilişkili yerel ayarı tarafından belirtilen hello dili) toobe Azure ölçümleri toothis verilerde bağlı.</span><span class="sxs-lookup"><span data-stu-id="5956b-291">hello label (in hello language specified by hello associated locale setting) toobe attached toothis data in Azure Metrics.</span></span> <span data-ttu-id="5956b-292">Bu alan LAD yoksayar.</span><span class="sxs-lookup"><span data-stu-id="5956b-292">LAD ignores this field.</span></span>

<span data-ttu-id="5956b-293">Merhaba counterSpecifier rasgele bir tanımlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="5956b-293">hello counterSpecifier is an arbitrary identifier.</span></span> <span data-ttu-id="5956b-294">Azure portal grafik ve özelliği, uyarı hello gibi ölçümleri tüketicilerinin counterSpecifier "bir ölçüm veya bir ölçüm örneğini tanımlayan anahtarı" Merhaba kullanın.</span><span class="sxs-lookup"><span data-stu-id="5956b-294">Consumers of metrics, like hello Azure portal charting and alerting feature, use counterSpecifier as hello "key" that identifies a metric or an instance of a metric.</span></span> <span data-ttu-id="5956b-295">İçin `builtin` ölçümleri, öneririz ile başlayan counterSpecifier değerleri kullandığınız `/builtin/`.</span><span class="sxs-lookup"><span data-stu-id="5956b-295">For `builtin` metrics, we recommend you use counterSpecifier values that begin with `/builtin/`.</span></span> <span data-ttu-id="5956b-296">Ölçüm belirli bir örneği topluyorsanız hello örneği toohello counterSpecifier değerini hello tanıtıcısı ekleme öneririz.</span><span class="sxs-lookup"><span data-stu-id="5956b-296">If you are collecting a specific instance of a metric, we recommend you attach hello identifier of hello instance toohello counterSpecifier value.</span></span> <span data-ttu-id="5956b-297">Bazı örnekler:</span><span class="sxs-lookup"><span data-stu-id="5956b-297">Some examples:</span></span>

* <span data-ttu-id="5956b-298">`/builtin/Processor/PercentIdleTime`-Tüm çekirdek arasında ortalaması boşta kalma süresi</span><span class="sxs-lookup"><span data-stu-id="5956b-298">`/builtin/Processor/PercentIdleTime` - Idle time averaged across all cores</span></span>
* <span data-ttu-id="5956b-299">`/builtin/Disk/FreeSpace(/mnt)`-Merhaba /mnt filesystem boş alan</span><span class="sxs-lookup"><span data-stu-id="5956b-299">`/builtin/Disk/FreeSpace(/mnt)` - Free space for hello /mnt filesystem</span></span>
* <span data-ttu-id="5956b-300">`/builtin/Disk/FreeSpace`-Boş alan tüm takılı bağlanan dosya sistemlerinin ortalaması</span><span class="sxs-lookup"><span data-stu-id="5956b-300">`/builtin/Disk/FreeSpace` - Free space averaged across all mounted filesystems</span></span>

<span data-ttu-id="5956b-301">LAD ne hello Azure portal hello counterSpecifier değeri toomatch herhangi düzeni bekliyor.</span><span class="sxs-lookup"><span data-stu-id="5956b-301">Neither LAD nor hello Azure portal expects hello counterSpecifier value toomatch any pattern.</span></span> <span data-ttu-id="5956b-302">CounterSpecifier değerleri nasıl oluşturmak tutarlı olması.</span><span class="sxs-lookup"><span data-stu-id="5956b-302">Be consistent in how you construct counterSpecifier values.</span></span>

<span data-ttu-id="5956b-303">Belirttiğinizde `performanceCounters`, LAD her zaman Azure depolama alanında veri tooa tablosu yazar.</span><span class="sxs-lookup"><span data-stu-id="5956b-303">When you specify `performanceCounters`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="5956b-304">Siz sahip hello aynı tooJSON blobları ve/veya olay hub'ları yazılan veriler, ancak depolama veri tooa tablosu devre dışı bırakılamıyor.</span><span class="sxs-lookup"><span data-stu-id="5956b-304">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="5956b-305">Merhaba tanılama uzantı yapılandırılmamış toouse tüm örnekleri aynı depolama hesabı adı ve uç nokta Ekle kendi ölçümleri ve günlükleri toohello hello aynı tablo.</span><span class="sxs-lookup"><span data-stu-id="5956b-305">All instances of hello diagnostic extension configured toouse hello same storage account name and endpoint add their metrics and logs toohello same table.</span></span> <span data-ttu-id="5956b-306">Çok fazla sayıda sanal makineleri yazıyorsanız aynı tablo bölümleme, Azure daraltabilir toohello toothat bölüm yazar.</span><span class="sxs-lookup"><span data-stu-id="5956b-306">If too many VMs are writing toohello same table partition, Azure can throttle writes toothat partition.</span></span> <span data-ttu-id="5956b-307">Merhaba eventVolume nedenler girişleri toobe ayarı 1 (küçük), 10 (Orta) ya da 100 (büyük) farklı bölümleri arasında yayılır.</span><span class="sxs-lookup"><span data-stu-id="5956b-307">hello eventVolume setting causes entries toobe spread across 1 (Small), 10 (Medium), or 100 (Large) different partitions.</span></span> <span data-ttu-id="5956b-308">Genellikle, "Orta" yeterli tooensure trafiğinin azaltılacağı değil.</span><span class="sxs-lookup"><span data-stu-id="5956b-308">Usually, "Medium" is sufficient tooensure traffic is not throttled.</span></span> <span data-ttu-id="5956b-309">hello Azure portal Hello Azure ölçümleri özelliği bu tablo tooproduce grafikleri veya tootrigger uyarıları hello verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="5956b-309">hello Azure Metrics feature of hello Azure portal uses hello data in this table tooproduce graphs or tootrigger alerts.</span></span> <span data-ttu-id="5956b-310">Bu dizeler hello birleşimini Hello tablo adıdır:</span><span class="sxs-lookup"><span data-stu-id="5956b-310">hello table name is hello concatenation of these strings:</span></span>

* `WADMetrics`
* <span data-ttu-id="5956b-311">Merhaba tablosunda depolanan değerleri Hello "scheduledTransferPeriod" Merhaba için bir araya getirilir</span><span class="sxs-lookup"><span data-stu-id="5956b-311">hello "scheduledTransferPeriod" for hello aggregated values stored in hello table</span></span>
* `P10DV2S`
* <span data-ttu-id="5956b-312">10 günde değişiklikleri "YYYYAAGG" Merhaba formunda bir tarih</span><span class="sxs-lookup"><span data-stu-id="5956b-312">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="5956b-313">Örnekler `WADMetricsPT1HP10DV2S20170410` ve `WADMetricsPT1MP10DV2S20170609`.</span><span class="sxs-lookup"><span data-stu-id="5956b-313">Examples include `WADMetricsPT1HP10DV2S20170410` and `WADMetricsPT1MP10DV2S20170609`.</span></span>

#### <a name="syslogevents"></a><span data-ttu-id="5956b-314">syslogEvents</span><span class="sxs-lookup"><span data-stu-id="5956b-314">syslogEvents</span></span>

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

<span data-ttu-id="5956b-315">Bu isteğe bağlı bir bölüm syslog günlük olayları hello koleksiyonunu denetler.</span><span class="sxs-lookup"><span data-stu-id="5956b-315">This optional section controls hello collection of log events from syslog.</span></span> <span data-ttu-id="5956b-316">Merhaba bölüm atlanırsa, syslog olayları hiç yakalanmaz.</span><span class="sxs-lookup"><span data-stu-id="5956b-316">If hello section is omitted, syslog events are not captured at all.</span></span>

<span data-ttu-id="5956b-317">Merhaba syslogEventConfiguration koleksiyonun her syslog özelliğini ilgi için bir girişi yok.</span><span class="sxs-lookup"><span data-stu-id="5956b-317">hello syslogEventConfiguration collection has one entry for each syslog facility of interest.</span></span> <span data-ttu-id="5956b-318">MinSeverity belirli olanağı için "hiçbiri", veya bu tesis hello öğesinde hiç görünmüyorsa, bu tesis hiçbir olaylarından yakalanır.</span><span class="sxs-lookup"><span data-stu-id="5956b-318">If minSeverity is "NONE" for a particular facility, or if that facility does not appear in hello element at all, no events from that facility are captured.</span></span>

<span data-ttu-id="5956b-319">Öğesi</span><span class="sxs-lookup"><span data-stu-id="5956b-319">Element</span></span> | <span data-ttu-id="5956b-320">Değer</span><span class="sxs-lookup"><span data-stu-id="5956b-320">Value</span></span>
------- | -----
<span data-ttu-id="5956b-321">İç havuzlar</span><span class="sxs-lookup"><span data-stu-id="5956b-321">sinks</span></span> | <span data-ttu-id="5956b-322">Adlarının virgülle ayrılmış bir liste iç havuzlar toowhich ayrı günlük olayları yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="5956b-322">A comma-separated list of names of sinks toowhich individual log events are published.</span></span> <span data-ttu-id="5956b-323">SyslogEventConfiguration Hello kısıtlamaları eşleşen tüm günlük listelenen yayımlanan tooeach havuz olaylardır.</span><span class="sxs-lookup"><span data-stu-id="5956b-323">All log events matching hello restrictions in syslogEventConfiguration are published tooeach listed sink.</span></span> <span data-ttu-id="5956b-324">Örnek: "EHforsyslog"</span><span class="sxs-lookup"><span data-stu-id="5956b-324">Example: "EHforsyslog"</span></span>
<span data-ttu-id="5956b-325">facilityName</span><span class="sxs-lookup"><span data-stu-id="5956b-325">facilityName</span></span> | <span data-ttu-id="5956b-326">Bir syslog tesis adı (gibi "günlük\_kullanıcı" veya "günlük\_LOCAL0").</span><span class="sxs-lookup"><span data-stu-id="5956b-326">A syslog facility name (such as "LOG\_USER" or "LOG\_LOCAL0").</span></span> <span data-ttu-id="5956b-327">Merhaba Hello "özelliği" bölümüne bakın [syslog adam sayfa](http://man7.org/linux/man-pages/man3/syslog.3.html) hello tam listesi için.</span><span class="sxs-lookup"><span data-stu-id="5956b-327">See hello "facility" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span>
<span data-ttu-id="5956b-328">minSeverity</span><span class="sxs-lookup"><span data-stu-id="5956b-328">minSeverity</span></span> | <span data-ttu-id="5956b-329">Bir syslog önem düzeyi (gibi "günlük\_hata" veya "günlük\_bilgileri").</span><span class="sxs-lookup"><span data-stu-id="5956b-329">A syslog severity level (such as "LOG\_ERR" or "LOG\_INFO").</span></span> <span data-ttu-id="5956b-330">Merhaba Hello "düzeyi" bölümüne bakın [syslog adam sayfa](http://man7.org/linux/man-pages/man3/syslog.3.html) hello tam listesi için.</span><span class="sxs-lookup"><span data-stu-id="5956b-330">See hello "level" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span> <span data-ttu-id="5956b-331">Merhaba uzantısı gönderilen olaylar toohello olanağı yakalar veya düzeyi hello belirtilen.</span><span class="sxs-lookup"><span data-stu-id="5956b-331">hello extension captures events sent toohello facility at or above hello specified level.</span></span>

<span data-ttu-id="5956b-332">Belirttiğinizde `syslogEvents`, LAD her zaman Azure depolama alanında veri tooa tablosu yazar.</span><span class="sxs-lookup"><span data-stu-id="5956b-332">When you specify `syslogEvents`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="5956b-333">Siz sahip hello aynı tooJSON blobları ve/veya olay hub'ları yazılan veriler, ancak depolama veri tooa tablosu devre dışı bırakılamıyor.</span><span class="sxs-lookup"><span data-stu-id="5956b-333">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="5956b-334">Bu tablo için davranış bölümleme hello aynı için açıklandığı gibi hello olduğu `performanceCounters`.</span><span class="sxs-lookup"><span data-stu-id="5956b-334">hello partitioning behavior for this table is hello same as described for `performanceCounters`.</span></span> <span data-ttu-id="5956b-335">Bu dizeler hello birleşimini Hello tablo adıdır:</span><span class="sxs-lookup"><span data-stu-id="5956b-335">hello table name is hello concatenation of these strings:</span></span>

* `LinuxSyslog`
* <span data-ttu-id="5956b-336">10 günde değişiklikleri "YYYYAAGG" Merhaba formunda bir tarih</span><span class="sxs-lookup"><span data-stu-id="5956b-336">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="5956b-337">Örnekler `LinuxSyslog20170410` ve `LinuxSyslog20170609`.</span><span class="sxs-lookup"><span data-stu-id="5956b-337">Examples include `LinuxSyslog20170410` and `LinuxSyslog20170609`.</span></span>

### <a name="perfcfg"></a><span data-ttu-id="5956b-338">perfCfg</span><span class="sxs-lookup"><span data-stu-id="5956b-338">perfCfg</span></span>

<span data-ttu-id="5956b-339">Bu isteğe bağlı bir bölüm rasgele yürütülmesi denetimleri [OMI](https://github.com/Microsoft/omi) sorgular.</span><span class="sxs-lookup"><span data-stu-id="5956b-339">This optional section controls execution of arbitrary [OMI](https://github.com/Microsoft/omi) queries.</span></span>

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

<span data-ttu-id="5956b-340">Öğesi</span><span class="sxs-lookup"><span data-stu-id="5956b-340">Element</span></span> | <span data-ttu-id="5956b-341">Değer</span><span class="sxs-lookup"><span data-stu-id="5956b-341">Value</span></span>
------- | -----
<span data-ttu-id="5956b-342">Namespace</span><span class="sxs-lookup"><span data-stu-id="5956b-342">namespace</span></span> | <span data-ttu-id="5956b-343">(isteğe bağlı) hello OMI ad alanı içinde hangi hello sorgu yürütülmelidir.</span><span class="sxs-lookup"><span data-stu-id="5956b-343">(optional) hello OMI namespace within which hello query should be executed.</span></span> <span data-ttu-id="5956b-344">Belirtilmezse, "kök/hello tarafından uygulanan scx", hello varsayılan değer olan [System Center platformlar arası sağlayıcıları](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span><span class="sxs-lookup"><span data-stu-id="5956b-344">If unspecified, hello default value is "root/scx", implemented by hello [System Center Cross-platform Providers](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span></span>
<span data-ttu-id="5956b-345">sorgu</span><span class="sxs-lookup"><span data-stu-id="5956b-345">query</span></span> | <span data-ttu-id="5956b-346">Merhaba OMI sorgu toobe yürütülür.</span><span class="sxs-lookup"><span data-stu-id="5956b-346">hello OMI query toobe executed.</span></span>
<span data-ttu-id="5956b-347">Tablo</span><span class="sxs-lookup"><span data-stu-id="5956b-347">table</span></span> | <span data-ttu-id="5956b-348">Depolama hesabı belirlenmiş hello de (isteğe bağlı) hello Azure depolama tablosunda (bkz [ayarların korumalı](#protected-settings)).</span><span class="sxs-lookup"><span data-stu-id="5956b-348">(optional) hello Azure storage table, in hello designated storage account (see [Protected settings](#protected-settings)).</span></span>
<span data-ttu-id="5956b-349">frequency</span><span class="sxs-lookup"><span data-stu-id="5956b-349">frequency</span></span> | <span data-ttu-id="5956b-350">(isteğe bağlı) hello hello sorgunun yürütülmesi, arasındaki saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="5956b-350">(optional) hello number of seconds between execution of hello query.</span></span> <span data-ttu-id="5956b-351">300 (5 dakika); varsayılan değer: en düşük değer 15 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="5956b-351">Default value is 300 (5 minutes); minimum value is 15 seconds.</span></span>
<span data-ttu-id="5956b-352">İç havuzlar</span><span class="sxs-lookup"><span data-stu-id="5956b-352">sinks</span></span> | <span data-ttu-id="5956b-353">(isteğe bağlı) Ek havuzlarını toowhich ham örnek ölçüm sonuçlarını adlarının virgülle ayrılmış bir liste yayımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5956b-353">(optional) A comma-separated list of names of additional sinks toowhich raw sample metric results should be published.</span></span> <span data-ttu-id="5956b-354">Bu ham örnekleri toplama yok veya Azure ölçümleri hello uzantısı tarafından hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="5956b-354">No aggregation of these raw samples is computed by hello extension or by Azure Metrics.</span></span>

<span data-ttu-id="5956b-355">"Tablo" veya "İç havuzlar" ya da her ikisini de belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5956b-355">Either "table" or "sinks", or both, must be specified.</span></span>

### <a name="filelogs"></a><span data-ttu-id="5956b-356">fileLogs</span><span class="sxs-lookup"><span data-stu-id="5956b-356">fileLogs</span></span>

<span data-ttu-id="5956b-357">Denetimleri hello günlük dosyalarının yakalayın.</span><span class="sxs-lookup"><span data-stu-id="5956b-357">Controls hello capture of log files.</span></span> <span data-ttu-id="5956b-358">LAD toohello dosyası yazılırken yeni metin satırlarını yakalar ve tootable satırları ve/veya belirtilen tüm havuzlarını (JsonBlob veya EventHub) yazar.</span><span class="sxs-lookup"><span data-stu-id="5956b-358">LAD captures new text lines as they are written toohello file and writes them tootable rows and/or any specified sinks (JsonBlob or EventHub).</span></span>

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

<span data-ttu-id="5956b-359">Öğesi</span><span class="sxs-lookup"><span data-stu-id="5956b-359">Element</span></span> | <span data-ttu-id="5956b-360">Değer</span><span class="sxs-lookup"><span data-stu-id="5956b-360">Value</span></span>
------- | -----
<span data-ttu-id="5956b-361">Dosya</span><span class="sxs-lookup"><span data-stu-id="5956b-361">file</span></span> | <span data-ttu-id="5956b-362">Merhaba günlük dosyası toobe tam yol adı Hello izlenen ve yakalanan.</span><span class="sxs-lookup"><span data-stu-id="5956b-362">hello full pathname of hello log file toobe watched and captured.</span></span> <span data-ttu-id="5956b-363">Merhaba pathname tek bir dosya adı olmalıdır; bir dizin adı veya joker karakterler içeriyor.</span><span class="sxs-lookup"><span data-stu-id="5956b-363">hello pathname must name a single file; it cannot name a directory or contain wildcards.</span></span>
<span data-ttu-id="5956b-364">Tablo</span><span class="sxs-lookup"><span data-stu-id="5956b-364">table</span></span> | <span data-ttu-id="5956b-365">(isteğe bağlı) hello Azure depolama tablosunda belirtilen hello depolama hesabı (belirtildiği şekilde korumalı hello yapılandırmasında), hangi yeni satırlarına hello "Merhaba dosyasının kuyruk" yazılır.</span><span class="sxs-lookup"><span data-stu-id="5956b-365">(optional) hello Azure storage table, in hello designated storage account (as specified in hello protected configuration), into which new lines from hello "tail" of hello file are written.</span></span>
<span data-ttu-id="5956b-366">İç havuzlar</span><span class="sxs-lookup"><span data-stu-id="5956b-366">sinks</span></span> | <span data-ttu-id="5956b-367">(isteğe bağlı) Ek havuzlarını toowhich günlük satırları adlarının virgülle ayrılmış bir liste gönderdi.</span><span class="sxs-lookup"><span data-stu-id="5956b-367">(optional) A comma-separated list of names of additional sinks toowhich log lines sent.</span></span>

<span data-ttu-id="5956b-368">"Tablo" veya "İç havuzlar" ya da her ikisini de belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5956b-368">Either "table" or "sinks", or both, must be specified.</span></span>

## <a name="metrics-supported-by-hello-builtin-provider"></a><span data-ttu-id="5956b-369">Merhaba yerleşik sağlayıcı tarafından desteklenen ölçümleri</span><span class="sxs-lookup"><span data-stu-id="5956b-369">Metrics supported by hello builtin provider</span></span>

<span data-ttu-id="5956b-370">Merhaba yerleşik ölçüm ölçümleri en ilginç tooa geniş kullanıcı kümesi için kaynak sağlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="5956b-370">hello builtin metric provider is a source of metrics most interesting tooa broad set of users.</span></span> <span data-ttu-id="5956b-371">Bu ölçümler beş geniş sınıflara ayrılır:</span><span class="sxs-lookup"><span data-stu-id="5956b-371">These metrics fall into five broad classes:</span></span>

* <span data-ttu-id="5956b-372">İşlemci</span><span class="sxs-lookup"><span data-stu-id="5956b-372">Processor</span></span>
* <span data-ttu-id="5956b-373">Bellek</span><span class="sxs-lookup"><span data-stu-id="5956b-373">Memory</span></span>
* <span data-ttu-id="5956b-374">Ağ</span><span class="sxs-lookup"><span data-stu-id="5956b-374">Network</span></span>
* <span data-ttu-id="5956b-375">Dosya sistemi</span><span class="sxs-lookup"><span data-stu-id="5956b-375">Filesystem</span></span>
* <span data-ttu-id="5956b-376">Disk</span><span class="sxs-lookup"><span data-stu-id="5956b-376">Disk</span></span>

### <a name="builtin-metrics-for-hello-processor-class"></a><span data-ttu-id="5956b-377">Merhaba işlemci sınıfı için yerleşik ölçümleri</span><span class="sxs-lookup"><span data-stu-id="5956b-377">builtin metrics for hello Processor class</span></span>

<span data-ttu-id="5956b-378">Merhaba ölçümleri işlemci sınıfının hello VM işlemci kullanımı hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="5956b-378">hello Processor class of metrics provides information about processor usage in hello VM.</span></span> <span data-ttu-id="5956b-379">Yüzdeleri toplanırken hello hello ortalama tüm CPU'lar arasında sonucudur.</span><span class="sxs-lookup"><span data-stu-id="5956b-379">When aggregating percentages, hello result is hello average across all CPUs.</span></span> <span data-ttu-id="5956b-380">Bir iki çekirdek VM, bir çekirdek % 100 meşgul ve % 100 boşta hello diğer şeklindeydi hello PercentIdleTime 50 olur bildirilen.</span><span class="sxs-lookup"><span data-stu-id="5956b-380">In a two core VM, if one core was 100% busy and hello other was 100% idle, hello reported PercentIdleTime would be 50.</span></span> <span data-ttu-id="5956b-381">Her çekirdek % 50 meşgul ise aynı hello dönem sonuç 50 de olacaktır hello bildirdi.</span><span class="sxs-lookup"><span data-stu-id="5956b-381">If each core was 50% busy for hello same period, hello reported result would also be 50.</span></span> <span data-ttu-id="5956b-382">Bir dört çekirdek VM, bir çekirdek % 100 meşgul ve hello boşta, diğerleri hello PercentIdleTime 75 olacaktır bildirdi.</span><span class="sxs-lookup"><span data-stu-id="5956b-382">In a four core VM, with one core 100% busy and hello others idle, hello reported PercentIdleTime would be 75.</span></span>

<span data-ttu-id="5956b-383">Sayaç</span><span class="sxs-lookup"><span data-stu-id="5956b-383">counter</span></span> | <span data-ttu-id="5956b-384">Anlamı</span><span class="sxs-lookup"><span data-stu-id="5956b-384">Meaning</span></span>
------- | -------
<span data-ttu-id="5956b-385">PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="5956b-385">PercentIdleTime</span></span> | <span data-ttu-id="5956b-386">İşlemci hello çekirdek boşta döngü yürütülmekte hello toplama penceresi sırasında zamanı yüzdesi</span><span class="sxs-lookup"><span data-stu-id="5956b-386">Percentage of time during hello aggregation window that processors were executing hello kernel idle loop</span></span>
<span data-ttu-id="5956b-387">percentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="5956b-387">PercentProcessorTime</span></span> | <span data-ttu-id="5956b-388">Boş olmayan bir iş parçacığı yürütme zamanı yüzdesi</span><span class="sxs-lookup"><span data-stu-id="5956b-388">Percentage of time executing a non-idle thread</span></span>
<span data-ttu-id="5956b-389">PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="5956b-389">PercentIOWaitTime</span></span> | <span data-ttu-id="5956b-390">G/ç işlemleri toocomplete için beklerken zaman yüzdesi</span><span class="sxs-lookup"><span data-stu-id="5956b-390">Percentage of time waiting for IO operations toocomplete</span></span>
<span data-ttu-id="5956b-391">PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="5956b-391">PercentInterruptTime</span></span> | <span data-ttu-id="5956b-392">Donanım/yazılım kesmeler ve DPC'ler (ertelenmiş yordam çağrılarını) yürütme zamanı yüzdesi</span><span class="sxs-lookup"><span data-stu-id="5956b-392">Percentage of time executing hardware/software interrupts and DPCs (deferred procedure calls)</span></span>
<span data-ttu-id="5956b-393">PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="5956b-393">PercentUserTime</span></span> | <span data-ttu-id="5956b-394">Boş olmayan süresini hello toplama penceresi sırasında hello zamanın normal öncelik en fazla kullanıcı yüzdesi</span><span class="sxs-lookup"><span data-stu-id="5956b-394">Of non-idle time during hello aggregation window, hello percentage of time spent in user more at normal priority</span></span>
<span data-ttu-id="5956b-395">PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="5956b-395">PercentNiceTime</span></span> | <span data-ttu-id="5956b-396">Boş olmayan süresini alçaltılmış (iyi) öncelikli harcanan yüzdeyle hello</span><span class="sxs-lookup"><span data-stu-id="5956b-396">Of non-idle time, hello percentage spent at lowered (nice) priority</span></span>
<span data-ttu-id="5956b-397">PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="5956b-397">PercentPrivilegedTime</span></span> | <span data-ttu-id="5956b-398">Boş olmayan süresini ayrıcalıklı (çekirdek) modda harcanan yüzdeyle hello</span><span class="sxs-lookup"><span data-stu-id="5956b-398">Of non-idle time, hello percentage spent in privileged (kernel) mode</span></span>

<span data-ttu-id="5956b-399">Merhaba bir too100% en ilk dört sayaçları sum.</span><span class="sxs-lookup"><span data-stu-id="5956b-399">hello first four counters should sum too100%.</span></span> <span data-ttu-id="5956b-400">Merhaba son üç ayrıca toplam too100% sayaçları; Bunlar PercentProcessorTime, PercentIOWaitTime ve PercentInterruptTime hello toplamını ayırabilir.</span><span class="sxs-lookup"><span data-stu-id="5956b-400">hello last three counters also sum too100%; they subdivide hello sum of PercentProcessorTime, PercentIOWaitTime, and PercentInterruptTime.</span></span>

<span data-ttu-id="5956b-401">tek bir ölçüm toplanan tüm işlemciler arasında tooobtain ayarlamak `"condition": "IsAggregate=TRUE"`.</span><span class="sxs-lookup"><span data-stu-id="5956b-401">tooobtain a single metric aggregated across all processors, set `"condition": "IsAggregate=TRUE"`.</span></span> <span data-ttu-id="5956b-402">İkinci mantıksal işlemciye bir dört hello çekirdek VM olarak tooobtain belirli bir işlemci için bir ölçüm ayarlamak `"condition": "Name=\\"1\\""`.</span><span class="sxs-lookup"><span data-stu-id="5956b-402">tooobtain a metric for a specific processor, such as hello second logical processor of a four core VM, set `"condition": "Name=\\"1\\""`.</span></span> <span data-ttu-id="5956b-403">Mantıksal işlemci numaralarıdır hello aralığında `[0..n-1]`.</span><span class="sxs-lookup"><span data-stu-id="5956b-403">Logical processor numbers are in hello range `[0..n-1]`.</span></span>

### <a name="builtin-metrics-for-hello-memory-class"></a><span data-ttu-id="5956b-404">Merhaba bellek sınıfı için yerleşik ölçümleri</span><span class="sxs-lookup"><span data-stu-id="5956b-404">builtin metrics for hello Memory class</span></span>

<span data-ttu-id="5956b-405">Merhaba ölçümleri sınıfının bellek disk belleği ve değiştirmeyi bellek kullanımı hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="5956b-405">hello Memory class of metrics provides information about memory utilization, paging, and swapping.</span></span>

<span data-ttu-id="5956b-406">Sayaç</span><span class="sxs-lookup"><span data-stu-id="5956b-406">counter</span></span> | <span data-ttu-id="5956b-407">Anlamı</span><span class="sxs-lookup"><span data-stu-id="5956b-407">Meaning</span></span>
------- | -------
<span data-ttu-id="5956b-408">AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="5956b-408">AvailableMemory</span></span> | <span data-ttu-id="5956b-409">MIB kullanılabilir fiziksel bellek</span><span class="sxs-lookup"><span data-stu-id="5956b-409">Available physical memory in MiB</span></span>
<span data-ttu-id="5956b-410">PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="5956b-410">PercentAvailableMemory</span></span> | <span data-ttu-id="5956b-411">Kullanılabilir fiziksel belleğin toplam bellek yüzdesi</span><span class="sxs-lookup"><span data-stu-id="5956b-411">Available physical memory as a percent of total memory</span></span>
<span data-ttu-id="5956b-412">UsedMemory</span><span class="sxs-lookup"><span data-stu-id="5956b-412">UsedMemory</span></span> | <span data-ttu-id="5956b-413">Kullanımda fiziksel bellek (MIB)</span><span class="sxs-lookup"><span data-stu-id="5956b-413">In-use physical memory (MiB)</span></span>
<span data-ttu-id="5956b-414">PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="5956b-414">PercentUsedMemory</span></span> | <span data-ttu-id="5956b-415">Kullanımdaki fiziksel belleğin toplam bellek yüzdesi</span><span class="sxs-lookup"><span data-stu-id="5956b-415">In-use physical memory as a percent of total memory</span></span>
<span data-ttu-id="5956b-416">PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="5956b-416">PagesPerSec</span></span> | <span data-ttu-id="5956b-417">Toplam disk belleği (okuma/yazma)</span><span class="sxs-lookup"><span data-stu-id="5956b-417">Total paging (read/write)</span></span>
<span data-ttu-id="5956b-418">PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="5956b-418">PagesReadPerSec</span></span> | <span data-ttu-id="5956b-419">Depolama (takas dosyası, program dosyası, eşlenmiş dosya, vb.) yedekleme sayfaları oku</span><span class="sxs-lookup"><span data-stu-id="5956b-419">Pages read from backing store (swap file, program file, mapped file, etc.)</span></span>
<span data-ttu-id="5956b-420">PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="5956b-420">PagesWrittenPerSec</span></span> | <span data-ttu-id="5956b-421">Toobacking yazılan sayfa depolamak (takas dosyası, eşlenmiş dosya, vb.)</span><span class="sxs-lookup"><span data-stu-id="5956b-421">Pages written toobacking store (swap file, mapped file, etc.)</span></span>
<span data-ttu-id="5956b-422">AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="5956b-422">AvailableSwap</span></span> | <span data-ttu-id="5956b-423">Kullanılmayan takas alanı (MIB)</span><span class="sxs-lookup"><span data-stu-id="5956b-423">Unused swap space (MiB)</span></span>
<span data-ttu-id="5956b-424">PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="5956b-424">PercentAvailableSwap</span></span> | <span data-ttu-id="5956b-425">Kullanılmayan değiştirme alanının toplam değiştirme yüzdesi</span><span class="sxs-lookup"><span data-stu-id="5956b-425">Unused swap space as a percentage of total swap</span></span>
<span data-ttu-id="5956b-426">UsedSwap</span><span class="sxs-lookup"><span data-stu-id="5956b-426">UsedSwap</span></span> | <span data-ttu-id="5956b-427">Kullanımda takas alanı (MIB)</span><span class="sxs-lookup"><span data-stu-id="5956b-427">In-use swap space (MiB)</span></span>
<span data-ttu-id="5956b-428">PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="5956b-428">PercentUsedSwap</span></span> | <span data-ttu-id="5956b-429">Değiştirme alanının toplam değiştirme yüzdesi olarak kullanımda</span><span class="sxs-lookup"><span data-stu-id="5956b-429">In-use swap space as a percentage of total swap</span></span>

<span data-ttu-id="5956b-430">Bu sınıf ölçümleri yalnızca tek bir örneği vardır.</span><span class="sxs-lookup"><span data-stu-id="5956b-430">This class of metrics has only a single instance.</span></span> <span data-ttu-id="5956b-431">Merhaba "koşul" özniteliği yok yararlı ayarlara sahip ve alınmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="5956b-431">hello "condition" attribute has no useful settings and should be omitted.</span></span>

### <a name="builtin-metrics-for-hello-network-class"></a><span data-ttu-id="5956b-432">Merhaba ağ sınıfı için yerleşik ölçümleri</span><span class="sxs-lookup"><span data-stu-id="5956b-432">builtin metrics for hello Network class</span></span>

<span data-ttu-id="5956b-433">Hello ölçümleri ağ sınıfı önyüklemeden tek tek ağ arabirimleri üzerinde ağ etkinliği hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="5956b-433">hello Network class of metrics provides information about network activity on an individual network interfaces since boot.</span></span> <span data-ttu-id="5956b-434">LAD ana ölçümleri alınabilir bant genişliği ölçümleri kullanıma sunmuyor.</span><span class="sxs-lookup"><span data-stu-id="5956b-434">LAD does not expose bandwidth metrics, which can be retrieved from host metrics.</span></span>

<span data-ttu-id="5956b-435">Sayaç</span><span class="sxs-lookup"><span data-stu-id="5956b-435">counter</span></span> | <span data-ttu-id="5956b-436">Anlamı</span><span class="sxs-lookup"><span data-stu-id="5956b-436">Meaning</span></span>
------- | -------
<span data-ttu-id="5956b-437">BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="5956b-437">BytesTransmitted</span></span> | <span data-ttu-id="5956b-438">Önyüklemeden gönderilen toplam bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="5956b-438">Total bytes sent since boot</span></span>
<span data-ttu-id="5956b-439">BytesReceived</span><span class="sxs-lookup"><span data-stu-id="5956b-439">BytesReceived</span></span> | <span data-ttu-id="5956b-440">Önyüklemeden alınan toplam bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="5956b-440">Total bytes received since boot</span></span>
<span data-ttu-id="5956b-441">BytesTotal</span><span class="sxs-lookup"><span data-stu-id="5956b-441">BytesTotal</span></span> | <span data-ttu-id="5956b-442">Gönderilen veya alınan önyüklemeden toplam bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="5956b-442">Total bytes sent or received since boot</span></span>
<span data-ttu-id="5956b-443">PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="5956b-443">PacketsTransmitted</span></span> | <span data-ttu-id="5956b-444">Önyüklemeden gönderilen toplam paket sayısı</span><span class="sxs-lookup"><span data-stu-id="5956b-444">Total packets sent since boot</span></span>
<span data-ttu-id="5956b-445">PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="5956b-445">PacketsReceived</span></span> | <span data-ttu-id="5956b-446">Önyüklemeden alınan toplam paket sayısı</span><span class="sxs-lookup"><span data-stu-id="5956b-446">Total packets received since boot</span></span>
<span data-ttu-id="5956b-447">TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="5956b-447">TotalRxErrors</span></span> | <span data-ttu-id="5956b-448">Sayısı önyüklemeden hataları alırsınız</span><span class="sxs-lookup"><span data-stu-id="5956b-448">Number of receive errors since boot</span></span>
<span data-ttu-id="5956b-449">TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="5956b-449">TotalTxErrors</span></span> | <span data-ttu-id="5956b-450">Sayısı önyüklemeden iletme işlemi hataları</span><span class="sxs-lookup"><span data-stu-id="5956b-450">Number of transmit errors since boot</span></span>
<span data-ttu-id="5956b-451">TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="5956b-451">TotalCollisions</span></span> | <span data-ttu-id="5956b-452">Çakışmaları önyüklemeden hello ağ bağlantı noktaları tarafından bildirilen sayısı</span><span class="sxs-lookup"><span data-stu-id="5956b-452">Number of collisions reported by hello network ports since boot</span></span>

 <span data-ttu-id="5956b-453">Bu sınıf instanced rağmen LAD tüm ağ aygıtlarını toplanan yakalama ağ ölçümleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="5956b-453">Although this class is instanced, LAD does not support capturing Network metrics aggregated across all network devices.</span></span> <span data-ttu-id="5956b-454">eth0 gibi belirli bir arabirim için tooobtain hello ölçümleri ayarlamak `"condition": "InstanceID=\\"eth0\\""`.</span><span class="sxs-lookup"><span data-stu-id="5956b-454">tooobtain hello metrics for a specific interface, such as eth0, set `"condition": "InstanceID=\\"eth0\\""`.</span></span>

### <a name="builtin-metrics-for-hello-filesystem-class"></a><span data-ttu-id="5956b-455">Merhaba Filesystem sınıfı için yerleşik ölçümleri</span><span class="sxs-lookup"><span data-stu-id="5956b-455">builtin metrics for hello Filesystem class</span></span>

<span data-ttu-id="5956b-456">Merhaba ölçümleri Filesystem sınıfının filesystem kullanımı hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="5956b-456">hello Filesystem class of metrics provides information about filesystem usage.</span></span> <span data-ttu-id="5956b-457">Mutlak ve yüzde değerleri, görüntülenen tooan normal kullanıcı (kök değil) olduğu raporlanır.</span><span class="sxs-lookup"><span data-stu-id="5956b-457">Absolute and percentage values are reported as they'd be displayed tooan ordinary user (not root).</span></span>

<span data-ttu-id="5956b-458">Sayaç</span><span class="sxs-lookup"><span data-stu-id="5956b-458">counter</span></span> | <span data-ttu-id="5956b-459">Anlamı</span><span class="sxs-lookup"><span data-stu-id="5956b-459">Meaning</span></span>
------- | -------
<span data-ttu-id="5956b-460">FreeSpace</span><span class="sxs-lookup"><span data-stu-id="5956b-460">FreeSpace</span></span> | <span data-ttu-id="5956b-461">Bayt cinsinden kullanılabilir disk alanı</span><span class="sxs-lookup"><span data-stu-id="5956b-461">Available disk space in bytes</span></span>
<span data-ttu-id="5956b-462">UsedSpace</span><span class="sxs-lookup"><span data-stu-id="5956b-462">UsedSpace</span></span> | <span data-ttu-id="5956b-463">Kullanılan disk alanı bayt</span><span class="sxs-lookup"><span data-stu-id="5956b-463">Used disk space in bytes</span></span>
<span data-ttu-id="5956b-464">PercentFreeSpace</span><span class="sxs-lookup"><span data-stu-id="5956b-464">PercentFreeSpace</span></span> | <span data-ttu-id="5956b-465">Boş alan yüzdesi</span><span class="sxs-lookup"><span data-stu-id="5956b-465">Percentage free space</span></span>
<span data-ttu-id="5956b-466">PercentUsedSpace</span><span class="sxs-lookup"><span data-stu-id="5956b-466">PercentUsedSpace</span></span> | <span data-ttu-id="5956b-467">Kullanılan yüzde alanı</span><span class="sxs-lookup"><span data-stu-id="5956b-467">Percentage used space</span></span>
<span data-ttu-id="5956b-468">PercentFreeInodes</span><span class="sxs-lookup"><span data-stu-id="5956b-468">PercentFreeInodes</span></span> | <span data-ttu-id="5956b-469">Kullanılmayan inode yüzdesi</span><span class="sxs-lookup"><span data-stu-id="5956b-469">Percentage of unused inodes</span></span>
<span data-ttu-id="5956b-470">PercentUsedInodes</span><span class="sxs-lookup"><span data-stu-id="5956b-470">PercentUsedInodes</span></span> | <span data-ttu-id="5956b-471">Tüm bağlanan dosya sistemlerinin arasında toplamı (kullanımda) ayrılmış inode yüzdesi</span><span class="sxs-lookup"><span data-stu-id="5956b-471">Percentage of allocated (in use) inodes summed across all filesystems</span></span>
<span data-ttu-id="5956b-472">BytesReadPerSecond</span><span class="sxs-lookup"><span data-stu-id="5956b-472">BytesReadPerSecond</span></span> | <span data-ttu-id="5956b-473">Saniye başına okunan bayt</span><span class="sxs-lookup"><span data-stu-id="5956b-473">Bytes read per second</span></span>
<span data-ttu-id="5956b-474">BytesWrittenPerSecond</span><span class="sxs-lookup"><span data-stu-id="5956b-474">BytesWrittenPerSecond</span></span> | <span data-ttu-id="5956b-475">Saniye başına yazılan bayt</span><span class="sxs-lookup"><span data-stu-id="5956b-475">Bytes written per second</span></span>
<span data-ttu-id="5956b-476">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="5956b-476">BytesPerSecond</span></span> | <span data-ttu-id="5956b-477">Okunan veya saniye başına yazılan bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="5956b-477">Bytes read or written per second</span></span>
<span data-ttu-id="5956b-478">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="5956b-478">ReadsPerSecond</span></span> | <span data-ttu-id="5956b-479">Saniye başına okuma işlemleri</span><span class="sxs-lookup"><span data-stu-id="5956b-479">Read operations per second</span></span>
<span data-ttu-id="5956b-480">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="5956b-480">WritesPerSecond</span></span> | <span data-ttu-id="5956b-481">Saniye başına işlem yazma</span><span class="sxs-lookup"><span data-stu-id="5956b-481">Write operations per second</span></span>
<span data-ttu-id="5956b-482">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="5956b-482">TransfersPerSecond</span></span> | <span data-ttu-id="5956b-483">Saniye başına okuma veya yazma işlemi</span><span class="sxs-lookup"><span data-stu-id="5956b-483">Read or write operations per second</span></span>

<span data-ttu-id="5956b-484">Tüm dosya sistemleri arasında toplanmış değerler elde edilebilir ayarlayarak `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="5956b-484">Aggregated values across all file systems can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="5956b-485">Belirli bağlı dosya sistemi için aşağıdaki gibi değerler "/ mnt", ayarlayarak elde `"condition": 'Name="/mnt"'`.</span><span class="sxs-lookup"><span data-stu-id="5956b-485">Values for a specific mounted file system, such as "/mnt", can be obtained by setting `"condition": 'Name="/mnt"'`.</span></span>

### <a name="builtin-metrics-for-hello-disk-class"></a><span data-ttu-id="5956b-486">Merhaba Disk sınıfı için yerleşik ölçümleri</span><span class="sxs-lookup"><span data-stu-id="5956b-486">builtin metrics for hello Disk class</span></span>

<span data-ttu-id="5956b-487">Merhaba ölçümleri Disk sınıfının disk Aygıt kullanımı hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="5956b-487">hello Disk class of metrics provides information about disk device usage.</span></span> <span data-ttu-id="5956b-488">Bu istatistikler sürücünün tamamını toohello uygulayın.</span><span class="sxs-lookup"><span data-stu-id="5956b-488">These statistics apply toohello entire drive.</span></span> <span data-ttu-id="5956b-489">Bir cihazda birden çok dosya sistemleri varsa, bu aygıt için hello sayaçları, etkili bir şekilde, bunların tümünün toplanan var.</span><span class="sxs-lookup"><span data-stu-id="5956b-489">If there are multiple file systems on a device, hello counters for that device are, effectively, aggregated across all of them.</span></span>

<span data-ttu-id="5956b-490">Sayaç</span><span class="sxs-lookup"><span data-stu-id="5956b-490">counter</span></span> | <span data-ttu-id="5956b-491">Anlamı</span><span class="sxs-lookup"><span data-stu-id="5956b-491">Meaning</span></span>
------- | -------
<span data-ttu-id="5956b-492">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="5956b-492">ReadsPerSecond</span></span> | <span data-ttu-id="5956b-493">Saniye başına okuma işlemleri</span><span class="sxs-lookup"><span data-stu-id="5956b-493">Read operations per second</span></span>
<span data-ttu-id="5956b-494">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="5956b-494">WritesPerSecond</span></span> | <span data-ttu-id="5956b-495">Saniye başına işlem yazma</span><span class="sxs-lookup"><span data-stu-id="5956b-495">Write operations per second</span></span>
<span data-ttu-id="5956b-496">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="5956b-496">TransfersPerSecond</span></span> | <span data-ttu-id="5956b-497">Saniye başına toplam işlem</span><span class="sxs-lookup"><span data-stu-id="5956b-497">Total operations per second</span></span>
<span data-ttu-id="5956b-498">AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="5956b-498">AverageReadTime</span></span> | <span data-ttu-id="5956b-499">Okuma işlemi başına ortalama saniye</span><span class="sxs-lookup"><span data-stu-id="5956b-499">Average seconds per read operation</span></span>
<span data-ttu-id="5956b-500">AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="5956b-500">AverageWriteTime</span></span> | <span data-ttu-id="5956b-501">Yazma işlemi başına ortalama saniye</span><span class="sxs-lookup"><span data-stu-id="5956b-501">Average seconds per write operation</span></span>
<span data-ttu-id="5956b-502">AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="5956b-502">AverageTransferTime</span></span> | <span data-ttu-id="5956b-503">İşlem başına ortalama saniye</span><span class="sxs-lookup"><span data-stu-id="5956b-503">Average seconds per operation</span></span>
<span data-ttu-id="5956b-504">AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="5956b-504">AverageDiskQueueLength</span></span> | <span data-ttu-id="5956b-505">Sıraya alınan disk işlemleri ortalama sayısı</span><span class="sxs-lookup"><span data-stu-id="5956b-505">Average number of queued disk operations</span></span>
<span data-ttu-id="5956b-506">ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="5956b-506">ReadBytesPerSecond</span></span> | <span data-ttu-id="5956b-507">Saniye başına okunan bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="5956b-507">Number of bytes read per second</span></span>
<span data-ttu-id="5956b-508">WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="5956b-508">WriteBytesPerSecond</span></span> | <span data-ttu-id="5956b-509">Saniye başına yazılan bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="5956b-509">Number of bytes written per second</span></span>
<span data-ttu-id="5956b-510">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="5956b-510">BytesPerSecond</span></span> | <span data-ttu-id="5956b-511">Okunan veya saniye başına yazılan bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="5956b-511">Number of bytes read or written per second</span></span>

<span data-ttu-id="5956b-512">Tüm diskler boyunca toplanan değerler elde edilebilir ayarlayarak `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="5956b-512">Aggregated values across all disks can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="5956b-513">tooget bilgilerini (örneğin, / dev/sdf1), belirli bir aygıt için `"condition": "Name=\\"/dev/sdf1\\""`.</span><span class="sxs-lookup"><span data-stu-id="5956b-513">tooget information for a specific device (for example, /dev/sdf1), set `"condition": "Name=\\"/dev/sdf1\\""`.</span></span>

## <a name="installing-and-configuring-lad-30-via-cli"></a><span data-ttu-id="5956b-514">Yükleme ve LAD 3.0 CLI üzerinden yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5956b-514">Installing and configuring LAD 3.0 via CLI</span></span>

<span data-ttu-id="5956b-515">Korumalı ayarlarınızı PrivateConfig.json hello dosyasında ve genel yapılandırma bilgilerinizi PublicConfig.json varsayılarak, şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5956b-515">Assuming your protected settings are in hello file PrivateConfig.json and your public configuration information is in PublicConfig.json, run this command:</span></span>

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

<span data-ttu-id="5956b-516">Merhaba komutu hello Azure CLI hello Azure kaynak yönetimi modu (arm) kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="5956b-516">hello command assumes you are using hello Azure Resource Management mode (arm) of hello Azure CLI.</span></span> <span data-ttu-id="5956b-517">Klasik dağıtım için tooconfigure LAD (ASM) VM'ler model, çok geçiş "asm" modu (`azure config mode asm`) ve hello kaynak grubu adı hello komutta atlayın.</span><span class="sxs-lookup"><span data-stu-id="5956b-517">tooconfigure LAD for classic deployment model (ASM) VMs, switch too"asm" mode (`azure config mode asm`) and omit hello resource group name in hello command.</span></span> <span data-ttu-id="5956b-518">Daha fazla bilgi için bkz: Merhaba [platformlar arası CLI belgelerine](https://docs.microsoft.com/azure/xplat-cli-connect).</span><span class="sxs-lookup"><span data-stu-id="5956b-518">For more information, see hello [cross-platform CLI documentation](https://docs.microsoft.com/azure/xplat-cli-connect).</span></span>

## <a name="an-example-lad-30-configuration"></a><span data-ttu-id="5956b-519">Bir örnek LAD 3.0 yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5956b-519">An example LAD 3.0 configuration</span></span>

<span data-ttu-id="5956b-520">Tanımları, burada ait bir örnek LAD 3.0 uzantısı yapılandırması bazı açıklama ile önceki hello temel.</span><span class="sxs-lookup"><span data-stu-id="5956b-520">Based on hello preceding definitions, here's a sample LAD 3.0 extension configuration with some explanation.</span></span> <span data-ttu-id="5956b-521">tooapply Bu örnek tooyour durumda, kendi depolama hesabı adı kullanın, hesap SAS belirteci ve EventHubs SAS belirteçleri.</span><span class="sxs-lookup"><span data-stu-id="5956b-521">tooapply this sample tooyour case, you should use your own storage account name, account SAS token, and EventHubs SAS tokens.</span></span>

### <a name="privateconfigjson"></a><span data-ttu-id="5956b-522">PrivateConfig.json</span><span class="sxs-lookup"><span data-stu-id="5956b-522">PrivateConfig.json</span></span>

<span data-ttu-id="5956b-523">Bu özel ayarları yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="5956b-523">These private settings configure:</span></span>

* <span data-ttu-id="5956b-524">bir depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="5956b-524">a storage account</span></span>
* <span data-ttu-id="5956b-525">eşleşen hesap SAS belirteci</span><span class="sxs-lookup"><span data-stu-id="5956b-525">a matching account SAS token</span></span>
* <span data-ttu-id="5956b-526">birkaç havuzlarını (JsonBlob veya EventHubs SAS belirteci ile)</span><span class="sxs-lookup"><span data-stu-id="5956b-526">several sinks (JsonBlob or EventHubs with SAS tokens)</span></span>

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

### <a name="publicconfigjson"></a><span data-ttu-id="5956b-527">PublicConfig.json</span><span class="sxs-lookup"><span data-stu-id="5956b-527">PublicConfig.json</span></span>

<span data-ttu-id="5956b-528">Bu genel ayarları için LAD neden:</span><span class="sxs-lookup"><span data-stu-id="5956b-528">These public settings cause LAD to:</span></span>

* <span data-ttu-id="5956b-529">Yüzde işlemci zamanı ve kullanılan disk alanı ölçümleri toohello karşıya `WADMetrics*` tablosu</span><span class="sxs-lookup"><span data-stu-id="5956b-529">Upload percent-processor-time and used-disk-space metrics toohello `WADMetrics*` table</span></span>
* <span data-ttu-id="5956b-530">Syslog tesis "kullanıcı" ve önem derecesi "bilgi" toohello iletilerden karşıya `LinuxSyslog*` tablosu</span><span class="sxs-lookup"><span data-stu-id="5956b-530">Upload messages from syslog facility "user" and severity "info" toohello `LinuxSyslog*` table</span></span>
* <span data-ttu-id="5956b-531">Adlı ham OMI sorgu sonuçları (PercentProcessorTime ve PercentIdleTime) toohello karşıya `LinuxCPU` tablosu</span><span class="sxs-lookup"><span data-stu-id="5956b-531">Upload raw OMI query results (PercentProcessorTime and PercentIdleTime) toohello named `LinuxCPU` table</span></span>
* <span data-ttu-id="5956b-532">Dosyasına eklenen satır karşıya `/var/log/myladtestlog` toohello `MyLadTestLog` tablo</span><span class="sxs-lookup"><span data-stu-id="5956b-532">Upload appended lines in file `/var/log/myladtestlog` toohello `MyLadTestLog` table</span></span>

<span data-ttu-id="5956b-533">Her durumda için veri yüklenir:</span><span class="sxs-lookup"><span data-stu-id="5956b-533">In each case, data is also uploaded to:</span></span>

* <span data-ttu-id="5956b-534">Azure Blob storage (kapsayıcı adı: Merhaba JsonBlob havuzunda tanımlandığı gibi)</span><span class="sxs-lookup"><span data-stu-id="5956b-534">Azure Blob storage (container name is as defined in hello JsonBlob sink)</span></span>
* <span data-ttu-id="5956b-535">EventHubs uç noktası (Merhaba EventHubs havuzunda belirtildiği şekilde)</span><span class="sxs-lookup"><span data-stu-id="5956b-535">EventHubs endpoint (as specified in hello EventHubs sink)</span></span>

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

<span data-ttu-id="5956b-536">Merhaba `resourceId` hello hello VM veya hello sanal makine ölçek kümesi yapılandırma eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="5956b-536">hello `resourceId` in hello configuration must match that of hello VM or hello virtual machine scale set.</span></span>

* <span data-ttu-id="5956b-537">Grafik ve uyarı azure platformu ölçümleri hello ResourceId hello üzerinde çalıştığınız VM, bilir.</span><span class="sxs-lookup"><span data-stu-id="5956b-537">Azure platform metrics charting and alerting knows hello resourceId of hello VM you're working on.</span></span> <span data-ttu-id="5956b-538">Toofind hello veri hello ResourceId hello arama anahtarı kullanarak, VM için bekler.</span><span class="sxs-lookup"><span data-stu-id="5956b-538">It expects toofind hello data for your VM using hello resourceId hello lookup key.</span></span>
* <span data-ttu-id="5956b-539">Azure otomatik ölçeklendirme kullanırsanız, hello ResourceId hello otomatik ölçeklendirme yapılandırmasında LAD tarafından kullanılan hello ResourceId eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5956b-539">If you use Azure autoscale, hello resourceId in hello autoscale configuration must match hello resourceId used by LAD.</span></span>
* <span data-ttu-id="5956b-540">Merhaba ResourceId LAD tarafından yazılan JsonBlobs hello adlarını içinde yerleşik olarak bulunur.</span><span class="sxs-lookup"><span data-stu-id="5956b-540">hello resourceId is built into hello names of JsonBlobs written by LAD.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="5956b-541">Verilerinizi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="5956b-541">View your data</span></span>

<span data-ttu-id="5956b-542">Hello Azure portal tooview performans verileri kullanma veya Uyarıları ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="5956b-542">Use hello Azure portal tooview performance data or set alerts:</span></span>

![Görüntü](./media/diagnostic-extension/graph_metrics.png)

<span data-ttu-id="5956b-544">Merhaba `performanceCounters` verileri her zaman bir Azure Storage tablosunda depolanır.</span><span class="sxs-lookup"><span data-stu-id="5956b-544">hello `performanceCounters` data are always stored in an Azure Storage table.</span></span> <span data-ttu-id="5956b-545">Azure depolama API'leri, birçok diller ve platformlar için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5956b-545">Azure Storage APIs are available for many languages and platforms.</span></span>

<span data-ttu-id="5956b-546">TooJsonBlob havuzlarını gönderilen veriler hello adlı hello depolama hesabındaki BLOB depolanır [ayarların korumalı](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="5956b-546">Data sent tooJsonBlob sinks is stored in blobs in hello storage account named in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="5956b-547">Tüm Azure Blob Depolama API'leri kullanılarak hello blob verileri kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="5956b-547">You can consume hello blob data using any Azure Blob Storage APIs.</span></span>

<span data-ttu-id="5956b-548">Ayrıca, bu kullanıcı Arabirimi araçlarını tooaccess hello verileri Azure depolama alanında kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5956b-548">In addition, you can use these UI tools tooaccess hello data in Azure Storage:</span></span>

* <span data-ttu-id="5956b-549">Visual Studio Sunucu Gezgini.</span><span class="sxs-lookup"><span data-stu-id="5956b-549">Visual Studio Server Explorer.</span></span>
* <span data-ttu-id="5956b-550">[Microsoft Azure Storage Gezgini](https://azurestorageexplorer.codeplex.com/ "Azure Storage Gezgini").</span><span class="sxs-lookup"><span data-stu-id="5956b-550">[Microsoft Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

<span data-ttu-id="5956b-551">Bu oturumunun anlık görüntüsü, bir Microsoft Azure Storage Gezgini hello Azure Storage tablolarının ve kapsayıcıları test VM üzerinde doğru şekilde yapılandırılmış bir LAD 3.0 uzantısı üretilen gösterir.</span><span class="sxs-lookup"><span data-stu-id="5956b-551">This snapshot of a Microsoft Azure Storage Explorer session shows hello generated Azure Storage tables and containers from a correctly configured LAD 3.0 extension on a test VM.</span></span> <span data-ttu-id="5956b-552">Merhaba görüntü hello ile tam olarak eşleşmiyor [örnek LAD 3.0 yapılandırma](#an-example-lad-30-configuration).</span><span class="sxs-lookup"><span data-stu-id="5956b-552">hello image doesn't match exactly with hello [sample LAD 3.0 configuration](#an-example-lad-30-configuration).</span></span>

![Görüntü](./media/diagnostic-extension/stg_explorer.png)

<span data-ttu-id="5956b-554">Hello ilgili bkz [EventHubs belgelerine](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn nasıl tooconsume iletileri tooan EventHubs endpoint yayımlandı.</span><span class="sxs-lookup"><span data-stu-id="5956b-554">See hello relevant [EventHubs documentation](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn how tooconsume messages published tooan EventHubs endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5956b-555">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5956b-555">Next steps</span></span>

* <span data-ttu-id="5956b-556">Ölçüm uyarıları oluşturma [Azure İzleyici](../../monitoring-and-diagnostics/insights-alerts-portal.md) topladığınız hello ölçümünün.</span><span class="sxs-lookup"><span data-stu-id="5956b-556">Create metric alerts in [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) for hello metrics you collect.</span></span>
* <span data-ttu-id="5956b-557">Oluşturma [izleme grafikleri](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) ölçümlerinizi için.</span><span class="sxs-lookup"><span data-stu-id="5956b-557">Create [monitoring charts](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) for your metrics.</span></span>
* <span data-ttu-id="5956b-558">Nasıl çok öğrenin[bir sanal makine ölçek kümesi oluşturma](/azure/virtual-machines/linux/tutorial-create-vmss) , ölçümleri toocontrol otomatik ölçeklendirmeyi kullanma.</span><span class="sxs-lookup"><span data-stu-id="5956b-558">Learn how too[create a virtual machine scale set](/azure/virtual-machines/linux/tutorial-create-vmss) using your metrics toocontrol autoscaling.</span></span>
