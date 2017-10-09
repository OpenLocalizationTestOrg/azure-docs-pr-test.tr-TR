---
title: "aaaAzure tanılama uzantı yapılandırmasını şema sürümleri ve geçmiş | Microsoft Docs"
description: "Azure sanal makineler, VM ölçek kümesi, Service Fabric ve Cloud Services ilgili toocollecting performans sayaçları."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/16/2017
ms.author: robb
ms.openlocfilehash: 854ad118f660810aa38703670284794d658142c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-extention-configuration-schema-versions-and-history"></a><span data-ttu-id="ece10-103">Azure tanılama uzantı yapılandırmasını şema sürümleri ve geçmişi</span><span class="sxs-lookup"><span data-stu-id="ece10-103">Azure Diagnostics extention configuration schema versions and history</span></span>
<span data-ttu-id="ece10-104">Bu sayfa dizinlerinin Azure tanılama uzantı şema sürümleri hello Microsoft Azure SDK'sı bir parçası olarak gönderilir.</span><span class="sxs-lookup"><span data-stu-id="ece10-104">This page indexes Azure Diagnostics extension schema versions shipped as part of hello Microsoft Azure SDK.</span></span>  

> [!NOTE]
> <span data-ttu-id="ece10-105">Hello Azure tanılama uzantısını hello bileşen toocollect performans sayaçları ve diğer istatistiklerine kullanılır:</span><span class="sxs-lookup"><span data-stu-id="ece10-105">hello Azure Diagnostics extension is hello component used toocollect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="ece10-106">Azure Sanal Makineler</span><span class="sxs-lookup"><span data-stu-id="ece10-106">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="ece10-107">Sanal Makine Ölçek Kümeleri</span><span class="sxs-lookup"><span data-stu-id="ece10-107">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="ece10-108">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ece10-108">Service Fabric</span></span> 
> - <span data-ttu-id="ece10-109">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="ece10-109">Cloud Services</span></span> 
> - <span data-ttu-id="ece10-110">Ağ Güvenlik Grupları</span><span class="sxs-lookup"><span data-stu-id="ece10-110">Network Security Groups</span></span>
> 
> <span data-ttu-id="ece10-111">Bu sayfa, yalnızca bu hizmetlerden biri kullanıyorsanız geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ece10-111">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="ece10-112">Hello Azure tanılama uzantısını Azure monitör, Application Insights ve günlük analizi gibi diğer Microsoft tanılama ürünlerle kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ece10-112">hello Azure Diagnostics extension is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span> <span data-ttu-id="ece10-113">Daha fazla bilgi için bkz: [Microsoft izleme araçlarına genel bakış](monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ece10-113">For more information see [Microsoft Monitoring Tools Overview](monitoring-overview.md).</span></span>

## <a name="azure-sdk-and-diagnostics-versions-shipping-chart"></a><span data-ttu-id="ece10-114">Grafik sevkiyat azure SDK ve tanılama sürümleri</span><span class="sxs-lookup"><span data-stu-id="ece10-114">Azure SDK and diagnostics versions shipping chart</span></span>  

|<span data-ttu-id="ece10-115">Azure SDK sürümü</span><span class="sxs-lookup"><span data-stu-id="ece10-115">Azure SDK version</span></span> | <span data-ttu-id="ece10-116">Tanılama genişletme sürümü</span><span class="sxs-lookup"><span data-stu-id="ece10-116">Diagnostics extension version</span></span> | <span data-ttu-id="ece10-117">modeli</span><span class="sxs-lookup"><span data-stu-id="ece10-117">Model</span></span>|  
|------------------|-------------------------------|------|  
|<span data-ttu-id="ece10-118">1.x</span><span class="sxs-lookup"><span data-stu-id="ece10-118">1.x</span></span>               |<span data-ttu-id="ece10-119">1.0</span><span class="sxs-lookup"><span data-stu-id="ece10-119">1.0</span></span>                            |<span data-ttu-id="ece10-120">eklentisi</span><span class="sxs-lookup"><span data-stu-id="ece10-120">plug-in</span></span>|  
|<span data-ttu-id="ece10-121">2.0 - 2.4</span><span class="sxs-lookup"><span data-stu-id="ece10-121">2.0 - 2.4</span></span>         |<span data-ttu-id="ece10-122">1.0</span><span class="sxs-lookup"><span data-stu-id="ece10-122">1.0</span></span>                            |<span data-ttu-id="ece10-123">eklentisi</span><span class="sxs-lookup"><span data-stu-id="ece10-123">plug-in</span></span>|  
|<span data-ttu-id="ece10-124">2.5</span><span class="sxs-lookup"><span data-stu-id="ece10-124">2.5</span></span>               |<span data-ttu-id="ece10-125">1.2</span><span class="sxs-lookup"><span data-stu-id="ece10-125">1.2</span></span>                            |<span data-ttu-id="ece10-126">Uzantısı</span><span class="sxs-lookup"><span data-stu-id="ece10-126">extension</span></span>|  
|<span data-ttu-id="ece10-127">2.6</span><span class="sxs-lookup"><span data-stu-id="ece10-127">2.6</span></span>               |<span data-ttu-id="ece10-128">1.3</span><span class="sxs-lookup"><span data-stu-id="ece10-128">1.3</span></span>                            |<span data-ttu-id="ece10-129">"</span><span class="sxs-lookup"><span data-stu-id="ece10-129">"</span></span>|  
|<span data-ttu-id="ece10-130">2.7</span><span class="sxs-lookup"><span data-stu-id="ece10-130">2.7</span></span>               |<span data-ttu-id="ece10-131">1.4</span><span class="sxs-lookup"><span data-stu-id="ece10-131">1.4</span></span>                            |<span data-ttu-id="ece10-132">"</span><span class="sxs-lookup"><span data-stu-id="ece10-132">"</span></span>|  
|<span data-ttu-id="ece10-133">2.8</span><span class="sxs-lookup"><span data-stu-id="ece10-133">2.8</span></span>               |<span data-ttu-id="ece10-134">1.5</span><span class="sxs-lookup"><span data-stu-id="ece10-134">1.5</span></span>                            |<span data-ttu-id="ece10-135">"</span><span class="sxs-lookup"><span data-stu-id="ece10-135">"</span></span>|  
|<span data-ttu-id="ece10-136">2.9</span><span class="sxs-lookup"><span data-stu-id="ece10-136">2.9</span></span>               |<span data-ttu-id="ece10-137">1.6</span><span class="sxs-lookup"><span data-stu-id="ece10-137">1.6</span></span>                            |<span data-ttu-id="ece10-138">"</span><span class="sxs-lookup"><span data-stu-id="ece10-138">"</span></span>|
|<span data-ttu-id="ece10-139">2.96</span><span class="sxs-lookup"><span data-stu-id="ece10-139">2.96</span></span>              |<span data-ttu-id="ece10-140">1.7</span><span class="sxs-lookup"><span data-stu-id="ece10-140">1.7</span></span>                            |<span data-ttu-id="ece10-141">"</span><span class="sxs-lookup"><span data-stu-id="ece10-141">"</span></span>|
|<span data-ttu-id="ece10-142">2.96</span><span class="sxs-lookup"><span data-stu-id="ece10-142">2.96</span></span>              |<span data-ttu-id="ece10-143">1.8</span><span class="sxs-lookup"><span data-stu-id="ece10-143">1.8</span></span>                            |<span data-ttu-id="ece10-144">"</span><span class="sxs-lookup"><span data-stu-id="ece10-144">"</span></span>|
|<span data-ttu-id="ece10-145">2.96</span><span class="sxs-lookup"><span data-stu-id="ece10-145">2.96</span></span>              |<span data-ttu-id="ece10-146">1.8.1</span><span class="sxs-lookup"><span data-stu-id="ece10-146">1.8.1</span></span>                          |<span data-ttu-id="ece10-147">"</span><span class="sxs-lookup"><span data-stu-id="ece10-147">"</span></span>|
|<span data-ttu-id="ece10-148">2.96</span><span class="sxs-lookup"><span data-stu-id="ece10-148">2.96</span></span>              |<span data-ttu-id="ece10-149">1.9</span><span class="sxs-lookup"><span data-stu-id="ece10-149">1.9</span></span>                            |<span data-ttu-id="ece10-150">"</span><span class="sxs-lookup"><span data-stu-id="ece10-150">"</span></span>|



 <span data-ttu-id="ece10-151">Azure tanılama sürüm 1.0 ilk hello Azure SDK'sı yüklendiğinde hello Azure Tanılama ile birlikte gelen sürümünü aldı yani bir eklenti modeli--geliyordu.</span><span class="sxs-lookup"><span data-stu-id="ece10-151">Azure Diagnostics version 1.0 first shipped in a plug-in model -- meaning that when you installed hello Azure SDK, you got hello version of Azure diagnostics shipped with it.</span></span>  

 <span data-ttu-id="ece10-152">SDK 2.5 (tanılama sürüm 1.2) ile Azure tanılama başlatılıyor tooan uzantısı model geçti.</span><span class="sxs-lookup"><span data-stu-id="ece10-152">Starting with SDK 2.5 (diagnostics version 1.2), Azure diagnostics went tooan extension model.</span></span> <span data-ttu-id="ece10-153">Merhaba araçları tooutilize yeni özellikler yalnızca yeni Azure SDK'ları içinde kullanılabilir, ancak Azure Tanılama'yı kullanarak herhangi bir hizmeti hello son sevkiyat sürüm doğrudan Azure'dan çekme.</span><span class="sxs-lookup"><span data-stu-id="ece10-153">hello tools tooutilize new features were only available in newer Azure SDKs, but any service using Azure diagnostics would pick up hello latest shipping version directly from Azure.</span></span> <span data-ttu-id="ece10-154">Örneğin, hala SDK 2.5 kullanan herkes hello yeni özellikleri kullanıyorsanız hello önceki tabloda bakılmaksızın gösterilen hello en son sürümünü yüklemeye.</span><span class="sxs-lookup"><span data-stu-id="ece10-154">For example, anyone still using SDK 2.5 would be loading hello latest version shown in hello previous table, regardless if they are using hello newer features.</span></span>  

## <a name="schemas-index"></a><span data-ttu-id="ece10-155">Şemalar dizini</span><span class="sxs-lookup"><span data-stu-id="ece10-155">Schemas index</span></span>  
<span data-ttu-id="ece10-156">Azure tanılama farklı sürümlerini farklı yapılandırma şemaları kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="ece10-156">Different versions of Azure diagnostics use different configuration schemas.</span></span> 

[<span data-ttu-id="ece10-157">Tanılama 1.0 yapılandırma şeması</span><span class="sxs-lookup"><span data-stu-id="ece10-157">Diagnostics 1.0 Configuration Schema</span></span>](azure-diagnostics-schema-1dot0.md)  

[<span data-ttu-id="ece10-158">Tanılama 1.2 yapılandırma şeması</span><span class="sxs-lookup"><span data-stu-id="ece10-158">Diagnostics 1.2 Configuration Schema</span></span>](azure-diagnostics-schema-1dot2.md)  

[<span data-ttu-id="ece10-159">Tanılama 1.3 ve daha sonra yapılandırma şeması</span><span class="sxs-lookup"><span data-stu-id="ece10-159">Diagnostics 1.3 and later Configuration Schema</span></span>](azure-diagnostics-schema-1dot3-and-later.md)  

## <a name="version-history"></a><span data-ttu-id="ece10-160">Sürüm geçmişi</span><span class="sxs-lookup"><span data-stu-id="ece10-160">Version history</span></span>


### <a name="diagnostics-extension-19"></a><span data-ttu-id="ece10-161">Tanılama uzantısını 1.9</span><span class="sxs-lookup"><span data-stu-id="ece10-161">Diagnostics extension 1.9</span></span> 
<span data-ttu-id="ece10-162">Docker desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="ece10-162">Added Docker support.</span></span>


### <a name="diagnostics-extension-181"></a><span data-ttu-id="ece10-163">Tanılama uzantısını 1.8.1</span><span class="sxs-lookup"><span data-stu-id="ece10-163">Diagnostics extension 1.8.1</span></span> 
<span data-ttu-id="ece10-164">Bir depolama hesabı anahtarı yerine bir SAS belirteci hello özel yapılandırma dosyasında belirtebilirsiniz. Bir SAS belirteci sağlanırsa, hello depolama hesabı anahtarı göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="ece10-164">Can specify a SAS token instead of a storage account key in hello private config. If a SAS token is provided, hello storage account key is ignored.</span></span>


```json
{
    "storageAccountName": "diagstorageaccount",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    }
}
```

```xml
<PrivateConfig>
    <StorageAccount name="diagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    <SecondaryStorageAccounts>
        <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
</PrivateConfig>
```


### <a name="diagnostics-extension-18"></a><span data-ttu-id="ece10-165">Tanılama uzantısını 1,8</span><span class="sxs-lookup"><span data-stu-id="ece10-165">Diagnostics extension 1.8</span></span> 
<span data-ttu-id="ece10-166">Eklenen depolama türü tooPublicConfig.</span><span class="sxs-lookup"><span data-stu-id="ece10-166">Added Storage Type tooPublicConfig.</span></span> <span data-ttu-id="ece10-167">StorageType olabilir *tablo*, *Blob*, *TableAndBlob*.</span><span class="sxs-lookup"><span data-stu-id="ece10-167">StorageType can be *Table*, *Blob*, *TableAndBlob*.</span></span> <span data-ttu-id="ece10-168">*Tablo* hello varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="ece10-168">*Table* is hello default.</span></span>


```json
{
    "WadCfg": {
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```xml
<PublicConfig>
    <WadCfg />
    <StorageAccount>diagstorageaccount</StorageAccount>
    <StorageType>TableAndBlob</StorageType>
</PublicConfig>
```


### <a name="diagnostics-extension-17"></a><span data-ttu-id="ece10-169">Tanılama uzantısını 1.7</span><span class="sxs-lookup"><span data-stu-id="ece10-169">Diagnostics extension 1.7</span></span> 
<span data-ttu-id="ece10-170">Eklenen hello özelliği tooroute tooEventHub.</span><span class="sxs-lookup"><span data-stu-id="ece10-170">Added hello ability tooroute tooEventHub.</span></span>

### <a name="diagnostics-extension-15"></a><span data-ttu-id="ece10-171">Tanılama uzantısını 1.5</span><span class="sxs-lookup"><span data-stu-id="ece10-171">Diagnostics extension 1.5</span></span>
<span data-ttu-id="ece10-172">Merhaba öğesi ve hello özelliği toosend tanılama verilerini çok iç havuzlar eklenen[Application Insights](../application-insights/app-insights-cloudservices.md) daha kolay toodiagnose sorunları, uygulamanın yanı sıra arasında hello sistem ve altyapı düzeyinde yapma.</span><span class="sxs-lookup"><span data-stu-id="ece10-172">Added hello sinks element and hello ability toosend diagnostics data too[Application Insights](../application-insights/app-insights-cloudservices.md) making it easier toodiagnose issues across your application as well as hello system and infrastructure level.</span></span>

### <a name="azure-sdk-26-and-diagnostics-extension-13"></a><span data-ttu-id="ece10-173">Azure SDK 2.6 ve tanılama uzantısı 1.3</span><span class="sxs-lookup"><span data-stu-id="ece10-173">Azure SDK 2.6 and diagnostics extension 1.3</span></span> 
<span data-ttu-id="ece10-174">Visual Studio bulut hizmeti projeleri için hello aşağıdaki değişiklikler yapıldı.</span><span class="sxs-lookup"><span data-stu-id="ece10-174">For Cloud Service projects in Visual Studio, hello following changes were made.</span></span> <span data-ttu-id="ece10-175">(Bu değişikliklerin Azure SDK'ın toolater sürümleri de geçerlidir.)</span><span class="sxs-lookup"><span data-stu-id="ece10-175">(These changes also apply toolater versions of Azure SDK.)</span></span>

* <span data-ttu-id="ece10-176">Merhaba yerel öykünücüsü artık tanılama destekler.</span><span class="sxs-lookup"><span data-stu-id="ece10-176">hello local emulator now supports diagnostics.</span></span> <span data-ttu-id="ece10-177">Bu tanılama verilerini toplamak ve geliştirme ve Visual Studio'da test ederken, uygulamanızın doğru izlemeleri hello oluşturuyor olun anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ece10-177">This means you can collect diagnostics data and ensure your application is creating hello right traces while you're developing and testing in Visual Studio.</span></span> <span data-ttu-id="ece10-178">Merhaba bağlantı dizesi `UseDevelopmentStorage=true` hello Azure storage öykünücüsü kullanarak bulut hizmeti projenizi Visual Studio'da çalıştırıyorsanız tanılama veri toplamayı etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="ece10-178">hello connection string `UseDevelopmentStorage=true` enables diagnostics data collection while you're running your cloud service project in Visual Studio by using hello Azure storage emulator.</span></span> <span data-ttu-id="ece10-179">Tüm tanılama verilerini hello (geliştirme depolama) depolama hesabında toplanır.</span><span class="sxs-lookup"><span data-stu-id="ece10-179">All diagnostics data is collected in hello (Development Storage) storage account.</span></span>
* <span data-ttu-id="ece10-180">Merhaba tanılama depolama hesabı bağlantı dizesi (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) bir kez daha hello hizmet yapılandırma (.cscfg) dosyasında depolanır.</span><span class="sxs-lookup"><span data-stu-id="ece10-180">hello diagnostics storage account connection string (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) is stored once again in hello service configuration (.cscfg) file.</span></span> <span data-ttu-id="ece10-181">Azure SDK 2.5 hello diagnostics.wadcfgx dosyasında hello tanılama depolama hesabı belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="ece10-181">In Azure SDK 2.5 hello diagnostics storage account was specified in hello diagnostics.wadcfgx file.</span></span>

<span data-ttu-id="ece10-182">Azure SDK 2.4 ve önceki hello bağlantı dizesini nasıl çalıştığı ve nasıl Azure SDK 2.6 ve daha sonra çalıştığı arasında önemli bazı farklar vardır.</span><span class="sxs-lookup"><span data-stu-id="ece10-182">There are some notable differences between how hello connection string worked in Azure SDK 2.4 and earlier and how it works in Azure SDK 2.6 and later.</span></span>

* <span data-ttu-id="ece10-183">Azure SDK 2.4 ve önceki sürümlerinde, hello bağlantı dizesi çalışma zamanı tanılama günlükleri aktarmak için hello tanılama eklentisi tooget hello depolama hesabı bilgilerini tarafından kullanıldı.</span><span class="sxs-lookup"><span data-stu-id="ece10-183">In Azure SDK 2.4 and earlier, hello connection string was used as a runtime by hello diagnostics plugin tooget hello storage account information for transferring diagnostics logs.</span></span>
* <span data-ttu-id="ece10-184">Azure SDK 2.6 ve daha sonra hello tanılama bağlantı dizesi Visual Studio tooconfigure hello tanılama uzantısını yayımlama sırasında hello uygun depolama hesabı bilgileri ile tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ece10-184">In Azure SDK 2.6 and later, hello diagnostics connection string is used by Visual Studio tooconfigure hello diagnostics extension with hello appropriate storage account information during publishing.</span></span> <span data-ttu-id="ece10-185">Merhaba bağlantı dizesi, Visual Studio yayımlama için kullanacağı farklı hizmet yapılandırması için farklı depolama hesapları tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ece10-185">hello connection string lets you define different storage accounts for different service configurations that Visual Studio will use when publishing.</span></span> <span data-ttu-id="ece10-186">Ancak, Hello tanılama eklentisi artık (sonra Azure SDK 2.5) kullanılabilir olmadığından, hello .cscfg dosyası tek başına hello tanılama uzantısını etkinleştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="ece10-186">However, because hello diagnostics plugin is no longer available (after Azure SDK 2.5), hello .cscfg file by itself can't enable hello Diagnostics Extension.</span></span> <span data-ttu-id="ece10-187">Tooenable hello uzantısı ayrı olarak Visual Studio veya PowerShell gibi araçlar aracılığıyla var.</span><span class="sxs-lookup"><span data-stu-id="ece10-187">You have tooenable hello extension separately through tools such as Visual Studio or PowerShell.</span></span>
* <span data-ttu-id="ece10-188">PowerShell ile Merhaba tanılama uzantısını yapılandırma toosimplify hello işlemi, hello paket çıktı Visual Studio'dan hello genel yapılandırması XML hello tanılama uzantısını her rol için de içerir.</span><span class="sxs-lookup"><span data-stu-id="ece10-188">toosimplify hello process of configuring hello diagnostics extension with PowerShell, hello package output from Visual Studio also contains hello public configuration XML for hello diagnostics extension for each role.</span></span> <span data-ttu-id="ece10-189">Visual Studio hello tanılama bağlantı dizesi toopopulate hello depolama hesabı bilgilerini hello ortak yapılandırmada mevcut kullanır.</span><span class="sxs-lookup"><span data-stu-id="ece10-189">Visual Studio uses hello diagnostics connection string toopopulate hello storage account information present in hello public configuration.</span></span> <span data-ttu-id="ece10-190">Merhaba ortak yapılandırma dosyaları hello Uzantıları klasöründe oluşturulur ve hello düzeni PaaSDiagnostics izleyin. <RoleName>. PubConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="ece10-190">hello public config files are created in hello Extensions folder and follow hello pattern PaaSDiagnostics.<RoleName>.PubConfig.xml.</span></span> <span data-ttu-id="ece10-191">Tüm temel PowerShell dağıtımları her yapılandırma tooa rolü bu deseni toomap kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ece10-191">Any PowerShell based deployments can use this pattern toomap each configuration tooa Role.</span></span>
* <span data-ttu-id="ece10-192">hello görüntülenebilir hello hello .cscfg dosyasında bağlantı dizesini de Azure portal tooaccess hello tanılama verilerini hello tarafından kullanılan **izleme** sekmesini hello bağlantı dizesidir, gerekli tooconfigure hello hizmet tooshow ayrıntılı izleme verilerini hello Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="ece10-192">hello connection string in hello .cscfg file is also used by hello Azure portal tooaccess hello diagnostics data so it can appear in hello **Monitoring** tab. hello connection string is needed tooconfigure hello service tooshow verbose monitoring data in hello portal.</span></span>

#### <a name="migrating-projects-tooazure-sdk-26-and-later"></a><span data-ttu-id="ece10-193">Geçirme projeleri tooAzure SDK 2.6 ve sonrası</span><span class="sxs-lookup"><span data-stu-id="ece10-193">Migrating projects tooAzure SDK 2.6 and later</span></span>
<span data-ttu-id="ece10-194">Ardından Azure SDK 2.5 tooAzure SDK 2.6 den geçirme veya daha sonra hello .wadcfgx dosyasında belirtilen tanılama depolama hesabı olsaydı var. kalır.</span><span class="sxs-lookup"><span data-stu-id="ece10-194">When migrating from Azure SDK 2.5 tooAzure SDK 2.6 or later, if you had a diagnostics storage account specified in hello .wadcfgx file, then it will stay there.</span></span> <span data-ttu-id="ece10-195">farklı depolama yapılandırmaları için farklı depolama kullanmanın hello esneklik tootake avantajlarından hesapları, hello bağlantı dizesi tooyour projesi eklemek toomanually sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ece10-195">tootake advantage of hello flexibility of using different storage accounts for different storage configurations, you'll have toomanually add hello connection string tooyour project.</span></span> <span data-ttu-id="ece10-196">Azure SDK 2.4 veya önceki tooAzure SDK 2.6 proje geçiş, bağlantı dizeleri korunur tanılama hello.</span><span class="sxs-lookup"><span data-stu-id="ece10-196">If you're migrating a project from Azure SDK 2.4 or earlier tooAzure SDK 2.6, then hello diagnostics connection strings are preserved.</span></span> <span data-ttu-id="ece10-197">Ancak, nasıl bağlantı dizeleri Azure SDK 2.6 belirtildiği şekilde hello önceki bölümde davranılır hello değişiklikler lütfen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ece10-197">However, please note hello changes in how connection strings are treated in Azure SDK 2.6 as specified in hello previous section.</span></span>

#### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a><span data-ttu-id="ece10-198">Visual Studio hello tanılama depolama hesabı nasıl belirler</span><span class="sxs-lookup"><span data-stu-id="ece10-198">How Visual Studio determines hello diagnostics storage account</span></span>
* <span data-ttu-id="ece10-199">Bir tanılama bağlantı dizesi hello .cscfg dosyasında belirtilmediği takdirde, Visual Studio tooconfigure hello tanılama uzantısını yayımlarken ve hello ortak yapılandırma xml dosyalarını paketlemesi sırasında oluştururken kullanır.</span><span class="sxs-lookup"><span data-stu-id="ece10-199">If a diagnostics connection string is specified in hello .cscfg file, Visual Studio uses it tooconfigure hello diagnostics extension when publishing, and when generating hello public configuration xml files during packaging.</span></span>
* <span data-ttu-id="ece10-200">Bir tanılama bağlantı dizesi hello .cscfg dosyasında belirtilirse, ardından Visual Studio geri yayımlama ve hello ortak oluşturma hello .wadcfgx dosya tooconfigure hello tanılama uzantısını belirtilen toousing hello depolama hesabı döner paketleme yapılandırma xml dosyaları.</span><span class="sxs-lookup"><span data-stu-id="ece10-200">If no diagnostics connection string is specified in hello .cscfg file, then Visual Studio falls back toousing hello storage account specified in hello .wadcfgx file tooconfigure hello diagnostics extension when publishing, and generating hello public configuration xml files when packaging.</span></span>
* <span data-ttu-id="ece10-201">Merhaba tanılama bağlantı dizesi hello .cscfg dosyasında hello depolama hesabı hello .wadcfgx dosyasında daha önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="ece10-201">hello diagnostics connection string in hello .cscfg file takes precedence over hello storage account in hello .wadcfgx file.</span></span> <span data-ttu-id="ece10-202">Bir tanılama bağlantı dizesi ise hello .cscfg dosyasında belirtilen sonra Visual Studio kullanan ve .wadcfgx hello depolama hesabında yok sayar.</span><span class="sxs-lookup"><span data-stu-id="ece10-202">If a diagnostics connection string is specified in hello .cscfg file, then Visual Studio uses that and ignores hello storage account in .wadcfgx.</span></span>

#### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a><span data-ttu-id="ece10-203">Ne "geliştirme storage bağlantı dizelerini güncelleştir..." Merhaba</span><span class="sxs-lookup"><span data-stu-id="ece10-203">What does hello "Update development storage connection strings…"</span></span> <span data-ttu-id="ece10-204">onay kutusu musunuz?</span><span class="sxs-lookup"><span data-stu-id="ece10-204">checkbox do?</span></span>
<span data-ttu-id="ece10-205">onay kutusunu hello **güncelleştirme geliştirme storage bağlantı dizelerini tanılama ve önbelleğe alma için Microsoft Azure depolama hesabı kimlik bilgilerinizle tooMicrosoft Azure yayımlarken** herhangi bir yöntemdir tooupdate sağlar Yayımlama sırasında belirtilen hello Azure depolama hesabı ile geliştirme depolama hesabı bağlantı dizeleri.</span><span class="sxs-lookup"><span data-stu-id="ece10-205">hello checkbox for **Update development storage connection strings for Diagnostics and Caching with Microsoft Azure storage account credentials when publishing tooMicrosoft Azure** gives you a convenient way tooupdate any development storage account connection strings with hello Azure storage account specified during publishing.</span></span>

<span data-ttu-id="ece10-206">Örneğin, bu onay kutusunu seçin ve hello tanılama bağlantı dizesini belirtir varsayalım `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="ece10-206">For example, suppose you select this checkbox and hello diagnostics connection string specifies `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="ece10-207">Merhaba proje tooAzure yayımladığınızda, Visual Studio hello tanılama bağlantı dizesi hello Yayımlama Sihirbazı'nda belirtilen hello depolama hesabıyla otomatik olarak güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="ece10-207">When you publish hello project tooAzure, Visual Studio will automatically update hello diagnostics connection string with hello storage account you specified in hello Publish wizard.</span></span> <span data-ttu-id="ece10-208">Gerçek depolama hesabı hello tanılama bağlantı dizesi olarak belirtilmişse, ancak, ardından o hesabı yerine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ece10-208">However, if a real storage account was specified as hello diagnostics connection string, then that account is used instead.</span></span>

### <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a><span data-ttu-id="ece10-209">Tanılama işlevleri farklılıkları Azure SDK 2.4 ve önceki ve Azure SDK 2,5 ve üzeri</span><span class="sxs-lookup"><span data-stu-id="ece10-209">Diagnostics functionality differences between Azure SDK 2.4 and earlier and Azure SDK 2.5 and later</span></span>
<span data-ttu-id="ece10-210">Projenizi Azure SDK 2.4 tooAzure SDK 2.5 veya sonraki ' yükseltiyorsanız, Tanılama işlevleri farklılıkları aşağıdaki göz hello bulundurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ece10-210">If you're upgrading your project from Azure SDK 2.4 tooAzure SDK 2.5 or later, you should bear in mind hello following diagnostics functionality differences.</span></span>

* <span data-ttu-id="ece10-211">**Yapılandırma API'leri dışıdır** – tanılama program yapılandırması Azure SDK 2.4 veya önceki sürümlerde kullanılabilir, ancak Azure SDK 2.5 ve daha sonra kullanım dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="ece10-211">**Configuration APIs are deprecated** – Programmatic configuration of diagnostics is available in Azure SDK 2.4 or earlier versions, but is deprecated in Azure SDK 2.5 and later.</span></span> <span data-ttu-id="ece10-212">Tanılama yapılandırmanızı kodda şu anda tanımlanmış olması durumunda, bu ayarları hello geçirilen proje sırada tanılama tookeep çalışmak için en baştan tooreconfigure gerekir.</span><span class="sxs-lookup"><span data-stu-id="ece10-212">If your diagnostics configuration is currently defined in code, you'll need tooreconfigure those settings from scratch in hello migrated project in order for diagnostics tookeep working.</span></span> <span data-ttu-id="ece10-213">Merhaba tanılama yapılandırması için Azure SDK 2.4 diagnostics.wadcfg ve diagnostics.wadcfgx ve sonraki sürümler için Azure SDK 2.5 dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="ece10-213">hello diagnostics configuration file for Azure SDK 2.4 is diagnostics.wadcfg, and diagnostics.wadcfgx for Azure SDK 2.5 and later.</span></span>
* <span data-ttu-id="ece10-214">**Bulut hizmeti uygulamaları için tanılama hello rol düzeyinde hello örnek düzeyinde değil yalnızca yapılandırılabilir.**</span><span class="sxs-lookup"><span data-stu-id="ece10-214">**Diagnostics for cloud service applications can only be configured at hello role level, not at hello instance level.**</span></span>
* <span data-ttu-id="ece10-215">**Uygulamanızı dağıtma her zaman hello tanılama yapılandırması güncelleştirilir** – tanılama yapılandırmanızı Server Explorer'dan değiştirirseniz ve uygulamanızı yeniden dağıtın bu eşlik sorunlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="ece10-215">**Every time you deploy your app, hello diagnostics configuration is updated** – This can cause parity issues if you change your diagnostics configuration from Server Explorer and then redeploy your app.</span></span>
* <span data-ttu-id="ece10-216">**Azure SDK 2.5 ve daha sonra kilitlenme bilgi dökümleri değil kodda hello tanılama yapılandırma dosyasındaki yapılandırılan** – kodda yapılandırılmış kilitlenme bilgi dökümleri varsa, kodu toohello yapılandırma dosyasından toomanually aktarımı hello yapılandırma gerekir. Merhaba kilitlenme dökümleri çünkü hello geçiş tooAzure SDK 2.6 sırasında aktarılmaz.</span><span class="sxs-lookup"><span data-stu-id="ece10-216">**In Azure SDK 2.5 and later, crash dumps are configured in hello diagnostics configuration file, not in code** – If you have crash dumps configured in code, you'll have toomanually transfer hello configuration from code toohello configuration file, because hello crash dumps aren't transferred during hello migration tooAzure SDK 2.6.</span></span>

