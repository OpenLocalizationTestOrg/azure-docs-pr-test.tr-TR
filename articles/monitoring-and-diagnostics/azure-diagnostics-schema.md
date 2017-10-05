---
title: "Azure tanılama uzantı yapılandırmasını şema sürümleri ve geçmiş | Microsoft Docs"
description: "Azure sanal makineler, VM ölçek kümesi, Service Fabric ve Cloud Services performans sayacı toplama ilgili."
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
ms.openlocfilehash: 119e8a237f24cdc80a1ab8e376f2b308c9eada05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-diagnostics-extention-configuration-schema-versions-and-history"></a><span data-ttu-id="f60e5-103">Azure tanılama uzantı yapılandırmasını şema sürümleri ve geçmişi</span><span class="sxs-lookup"><span data-stu-id="f60e5-103">Azure Diagnostics extention configuration schema versions and history</span></span>
<span data-ttu-id="f60e5-104">Bu sayfa dizinlerinin Azure tanılama uzantı şema sürümlerinde Microsoft Azure SDK'sı bir parçası olarak gönderilir.</span><span class="sxs-lookup"><span data-stu-id="f60e5-104">This page indexes Azure Diagnostics extension schema versions shipped as part of the Microsoft Azure SDK.</span></span>  

> [!NOTE]
> <span data-ttu-id="f60e5-105">Azure tanılama uzantısını performans sayaçları ve diğer istatistikleri toplamak için kullanılan bileşendir:</span><span class="sxs-lookup"><span data-stu-id="f60e5-105">The Azure Diagnostics extension is the component used to collect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="f60e5-106">Azure Sanal Makineler</span><span class="sxs-lookup"><span data-stu-id="f60e5-106">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="f60e5-107">Sanal Makine Ölçek Kümeleri</span><span class="sxs-lookup"><span data-stu-id="f60e5-107">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="f60e5-108">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f60e5-108">Service Fabric</span></span> 
> - <span data-ttu-id="f60e5-109">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="f60e5-109">Cloud Services</span></span> 
> - <span data-ttu-id="f60e5-110">Ağ Güvenlik Grupları</span><span class="sxs-lookup"><span data-stu-id="f60e5-110">Network Security Groups</span></span>
> 
> <span data-ttu-id="f60e5-111">Bu sayfa, yalnızca bu hizmetlerden biri kullanıyorsanız geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f60e5-111">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="f60e5-112">Azure tanılama uzantısını Azure monitör, Application Insights ve günlük analizi gibi diğer Microsoft tanılama ürünlerle kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f60e5-112">The Azure Diagnostics extension is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span> <span data-ttu-id="f60e5-113">Daha fazla bilgi için bkz: [Microsoft izleme araçlarına genel bakış](monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f60e5-113">For more information see [Microsoft Monitoring Tools Overview](monitoring-overview.md).</span></span>

## <a name="azure-sdk-and-diagnostics-versions-shipping-chart"></a><span data-ttu-id="f60e5-114">Grafik sevkiyat azure SDK ve tanılama sürümleri</span><span class="sxs-lookup"><span data-stu-id="f60e5-114">Azure SDK and diagnostics versions shipping chart</span></span>  

|<span data-ttu-id="f60e5-115">Azure SDK sürümü</span><span class="sxs-lookup"><span data-stu-id="f60e5-115">Azure SDK version</span></span> | <span data-ttu-id="f60e5-116">Tanılama genişletme sürümü</span><span class="sxs-lookup"><span data-stu-id="f60e5-116">Diagnostics extension version</span></span> | <span data-ttu-id="f60e5-117">modeli</span><span class="sxs-lookup"><span data-stu-id="f60e5-117">Model</span></span>|  
|------------------|-------------------------------|------|  
|<span data-ttu-id="f60e5-118">1.x</span><span class="sxs-lookup"><span data-stu-id="f60e5-118">1.x</span></span>               |<span data-ttu-id="f60e5-119">1.0</span><span class="sxs-lookup"><span data-stu-id="f60e5-119">1.0</span></span>                            |<span data-ttu-id="f60e5-120">eklentisi</span><span class="sxs-lookup"><span data-stu-id="f60e5-120">plug-in</span></span>|  
|<span data-ttu-id="f60e5-121">2.0 - 2.4</span><span class="sxs-lookup"><span data-stu-id="f60e5-121">2.0 - 2.4</span></span>         |<span data-ttu-id="f60e5-122">1.0</span><span class="sxs-lookup"><span data-stu-id="f60e5-122">1.0</span></span>                            |<span data-ttu-id="f60e5-123">eklentisi</span><span class="sxs-lookup"><span data-stu-id="f60e5-123">plug-in</span></span>|  
|<span data-ttu-id="f60e5-124">2.5</span><span class="sxs-lookup"><span data-stu-id="f60e5-124">2.5</span></span>               |<span data-ttu-id="f60e5-125">1.2</span><span class="sxs-lookup"><span data-stu-id="f60e5-125">1.2</span></span>                            |<span data-ttu-id="f60e5-126">Uzantısı</span><span class="sxs-lookup"><span data-stu-id="f60e5-126">extension</span></span>|  
|<span data-ttu-id="f60e5-127">2.6</span><span class="sxs-lookup"><span data-stu-id="f60e5-127">2.6</span></span>               |<span data-ttu-id="f60e5-128">1.3</span><span class="sxs-lookup"><span data-stu-id="f60e5-128">1.3</span></span>                            |<span data-ttu-id="f60e5-129">"</span><span class="sxs-lookup"><span data-stu-id="f60e5-129">"</span></span>|  
|<span data-ttu-id="f60e5-130">2.7</span><span class="sxs-lookup"><span data-stu-id="f60e5-130">2.7</span></span>               |<span data-ttu-id="f60e5-131">1.4</span><span class="sxs-lookup"><span data-stu-id="f60e5-131">1.4</span></span>                            |<span data-ttu-id="f60e5-132">"</span><span class="sxs-lookup"><span data-stu-id="f60e5-132">"</span></span>|  
|<span data-ttu-id="f60e5-133">2.8</span><span class="sxs-lookup"><span data-stu-id="f60e5-133">2.8</span></span>               |<span data-ttu-id="f60e5-134">1.5</span><span class="sxs-lookup"><span data-stu-id="f60e5-134">1.5</span></span>                            |<span data-ttu-id="f60e5-135">"</span><span class="sxs-lookup"><span data-stu-id="f60e5-135">"</span></span>|  
|<span data-ttu-id="f60e5-136">2.9</span><span class="sxs-lookup"><span data-stu-id="f60e5-136">2.9</span></span>               |<span data-ttu-id="f60e5-137">1.6</span><span class="sxs-lookup"><span data-stu-id="f60e5-137">1.6</span></span>                            |<span data-ttu-id="f60e5-138">"</span><span class="sxs-lookup"><span data-stu-id="f60e5-138">"</span></span>|
|<span data-ttu-id="f60e5-139">2.96</span><span class="sxs-lookup"><span data-stu-id="f60e5-139">2.96</span></span>              |<span data-ttu-id="f60e5-140">1.7</span><span class="sxs-lookup"><span data-stu-id="f60e5-140">1.7</span></span>                            |<span data-ttu-id="f60e5-141">"</span><span class="sxs-lookup"><span data-stu-id="f60e5-141">"</span></span>|
|<span data-ttu-id="f60e5-142">2.96</span><span class="sxs-lookup"><span data-stu-id="f60e5-142">2.96</span></span>              |<span data-ttu-id="f60e5-143">1.8</span><span class="sxs-lookup"><span data-stu-id="f60e5-143">1.8</span></span>                            |<span data-ttu-id="f60e5-144">"</span><span class="sxs-lookup"><span data-stu-id="f60e5-144">"</span></span>|
|<span data-ttu-id="f60e5-145">2.96</span><span class="sxs-lookup"><span data-stu-id="f60e5-145">2.96</span></span>              |<span data-ttu-id="f60e5-146">1.8.1</span><span class="sxs-lookup"><span data-stu-id="f60e5-146">1.8.1</span></span>                          |<span data-ttu-id="f60e5-147">"</span><span class="sxs-lookup"><span data-stu-id="f60e5-147">"</span></span>|
|<span data-ttu-id="f60e5-148">2.96</span><span class="sxs-lookup"><span data-stu-id="f60e5-148">2.96</span></span>              |<span data-ttu-id="f60e5-149">1.9</span><span class="sxs-lookup"><span data-stu-id="f60e5-149">1.9</span></span>                            |<span data-ttu-id="f60e5-150">"</span><span class="sxs-lookup"><span data-stu-id="f60e5-150">"</span></span>|



 <span data-ttu-id="f60e5-151">İlk Azure SDK'sını yüklendiğinde Azure tanılama sürümü var anlamına eklenti modelinde--sevk azure tanılama sürüm 1.0 ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="f60e5-151">Azure Diagnostics version 1.0 first shipped in a plug-in model -- meaning that when you installed the Azure SDK, you got the version of Azure diagnostics shipped with it.</span></span>  

 <span data-ttu-id="f60e5-152">Azure tanılama SDK 2.5 (tanılama sürüm 1.2) ile başlayan bir uzantı modeline geçti.</span><span class="sxs-lookup"><span data-stu-id="f60e5-152">Starting with SDK 2.5 (diagnostics version 1.2), Azure diagnostics went to an extension model.</span></span> <span data-ttu-id="f60e5-153">Yeni özellikleri kullanmak için Araçlar yalnızca yeni Azure SDK'ları içinde kullanılabilir, ancak Azure Tanılama'yı kullanarak herhangi bir hizmeti son sevkiyat sürüm doğrudan Azure'dan çekme.</span><span class="sxs-lookup"><span data-stu-id="f60e5-153">The tools to utilize new features were only available in newer Azure SDKs, but any service using Azure diagnostics would pick up the latest shipping version directly from Azure.</span></span> <span data-ttu-id="f60e5-154">Örneğin, hala SDK 2.5 kullanan herkes yeni özellikleri kullanıyorsanız önceki tabloda bakılmaksızın gösterilen en son sürümünü yüklemeye.</span><span class="sxs-lookup"><span data-stu-id="f60e5-154">For example, anyone still using SDK 2.5 would be loading the latest version shown in the previous table, regardless if they are using the newer features.</span></span>  

## <a name="schemas-index"></a><span data-ttu-id="f60e5-155">Şemalar dizini</span><span class="sxs-lookup"><span data-stu-id="f60e5-155">Schemas index</span></span>  
<span data-ttu-id="f60e5-156">Azure tanılama farklı sürümlerini farklı yapılandırma şemaları kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="f60e5-156">Different versions of Azure diagnostics use different configuration schemas.</span></span> 

[<span data-ttu-id="f60e5-157">Tanılama 1.0 yapılandırma şeması</span><span class="sxs-lookup"><span data-stu-id="f60e5-157">Diagnostics 1.0 Configuration Schema</span></span>](azure-diagnostics-schema-1dot0.md)  

[<span data-ttu-id="f60e5-158">Tanılama 1.2 yapılandırma şeması</span><span class="sxs-lookup"><span data-stu-id="f60e5-158">Diagnostics 1.2 Configuration Schema</span></span>](azure-diagnostics-schema-1dot2.md)  

[<span data-ttu-id="f60e5-159">Tanılama 1.3 ve daha sonra yapılandırma şeması</span><span class="sxs-lookup"><span data-stu-id="f60e5-159">Diagnostics 1.3 and later Configuration Schema</span></span>](azure-diagnostics-schema-1dot3-and-later.md)  

## <a name="version-history"></a><span data-ttu-id="f60e5-160">Sürüm geçmişi</span><span class="sxs-lookup"><span data-stu-id="f60e5-160">Version history</span></span>


### <a name="diagnostics-extension-19"></a><span data-ttu-id="f60e5-161">Tanılama uzantısını 1.9</span><span class="sxs-lookup"><span data-stu-id="f60e5-161">Diagnostics extension 1.9</span></span> 
<span data-ttu-id="f60e5-162">Docker desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="f60e5-162">Added Docker support.</span></span>


### <a name="diagnostics-extension-181"></a><span data-ttu-id="f60e5-163">Tanılama uzantısını 1.8.1</span><span class="sxs-lookup"><span data-stu-id="f60e5-163">Diagnostics extension 1.8.1</span></span> 
<span data-ttu-id="f60e5-164">Bir SAS belirteci bir depolama hesabı anahtarı yerine özel yapılandırma dosyasında belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f60e5-164">Can specify a SAS token instead of a storage account key in the private config.</span></span> <span data-ttu-id="f60e5-165">Bir SAS belirteci sağlanırsa, depolama hesabı anahtarı göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="f60e5-165">If a SAS token is provided, the storage account key is ignored.</span></span>


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


### <a name="diagnostics-extension-18"></a><span data-ttu-id="f60e5-166">Tanılama uzantısını 1,8</span><span class="sxs-lookup"><span data-stu-id="f60e5-166">Diagnostics extension 1.8</span></span> 
<span data-ttu-id="f60e5-167">PublicConfig için eklenen depolama türü.</span><span class="sxs-lookup"><span data-stu-id="f60e5-167">Added Storage Type to PublicConfig.</span></span> <span data-ttu-id="f60e5-168">StorageType olabilir *tablo*, *Blob*, *TableAndBlob*.</span><span class="sxs-lookup"><span data-stu-id="f60e5-168">StorageType can be *Table*, *Blob*, *TableAndBlob*.</span></span> <span data-ttu-id="f60e5-169">*Tablo* varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="f60e5-169">*Table* is the default.</span></span>


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


### <a name="diagnostics-extension-17"></a><span data-ttu-id="f60e5-170">Tanılama uzantısını 1.7</span><span class="sxs-lookup"><span data-stu-id="f60e5-170">Diagnostics extension 1.7</span></span> 
<span data-ttu-id="f60e5-171">EventHub için rota özelliği eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="f60e5-171">Added the ability to route to EventHub.</span></span>

### <a name="diagnostics-extension-15"></a><span data-ttu-id="f60e5-172">Tanılama uzantısını 1.5</span><span class="sxs-lookup"><span data-stu-id="f60e5-172">Diagnostics extension 1.5</span></span>
<span data-ttu-id="f60e5-173">İç havuzlar öğesi ve Tanılama verileri gönderme olanağı eklenen [Application Insights](../application-insights/app-insights-cloudservices.md) sistem ve altyapı düzeyinde yanı sıra, uygulamanızın üzerinde sorunları tanılamak kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="f60e5-173">Added the sinks element and the ability to send diagnostics data to [Application Insights](../application-insights/app-insights-cloudservices.md) making it easier to diagnose issues across your application as well as the system and infrastructure level.</span></span>

### <a name="azure-sdk-26-and-diagnostics-extension-13"></a><span data-ttu-id="f60e5-174">Azure SDK 2.6 ve tanılama uzantısı 1.3</span><span class="sxs-lookup"><span data-stu-id="f60e5-174">Azure SDK 2.6 and diagnostics extension 1.3</span></span> 
<span data-ttu-id="f60e5-175">Visual Studio bulut hizmeti projeleri için aşağıdaki değişiklikler yapıldı.</span><span class="sxs-lookup"><span data-stu-id="f60e5-175">For Cloud Service projects in Visual Studio, the following changes were made.</span></span> <span data-ttu-id="f60e5-176">(Bu değişikliklerin Azure SDK'ın sonraki sürümleri için de geçerlidir.)</span><span class="sxs-lookup"><span data-stu-id="f60e5-176">(These changes also apply to later versions of Azure SDK.)</span></span>

* <span data-ttu-id="f60e5-177">Yerel öykünücüsü artık tanılama destekler.</span><span class="sxs-lookup"><span data-stu-id="f60e5-177">The local emulator now supports diagnostics.</span></span> <span data-ttu-id="f60e5-178">Bu tanılama verilerini toplamak ve geliştirme ve Visual Studio'da test ederken, uygulamanızın doğru izlemeleri oluşturuyor olun anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="f60e5-178">This means you can collect diagnostics data and ensure your application is creating the right traces while you're developing and testing in Visual Studio.</span></span> <span data-ttu-id="f60e5-179">Bağlantı dizesi `UseDevelopmentStorage=true` Azure storage öykünücüsü kullanarak bulut hizmeti projenizi Visual Studio'da çalıştırıyorsanız tanılama veri toplamayı etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="f60e5-179">The connection string `UseDevelopmentStorage=true` enables diagnostics data collection while you're running your cloud service project in Visual Studio by using the Azure storage emulator.</span></span> <span data-ttu-id="f60e5-180">Tüm tanılama verilerini (geliştirme depolama) depolama hesabında toplanır.</span><span class="sxs-lookup"><span data-stu-id="f60e5-180">All diagnostics data is collected in the (Development Storage) storage account.</span></span>
* <span data-ttu-id="f60e5-181">Tanılama depolama hesabı bağlantı dizesi (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) bir kez daha hizmet yapılandırma (.cscfg) dosyasında depolanır.</span><span class="sxs-lookup"><span data-stu-id="f60e5-181">The diagnostics storage account connection string (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) is stored once again in the service configuration (.cscfg) file.</span></span> <span data-ttu-id="f60e5-182">Azure SDK 2.5 diagnostics.wadcfgx dosyasında tanılama depolama hesabı belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="f60e5-182">In Azure SDK 2.5 the diagnostics storage account was specified in the diagnostics.wadcfgx file.</span></span>

<span data-ttu-id="f60e5-183">Azure SDK 2.4 ve önceki bağlantı dizesini nasıl çalıştığı ve nasıl Azure SDK 2.6 ve daha sonra çalıştığı arasında önemli bazı farklar vardır.</span><span class="sxs-lookup"><span data-stu-id="f60e5-183">There are some notable differences between how the connection string worked in Azure SDK 2.4 and earlier and how it works in Azure SDK 2.6 and later.</span></span>

* <span data-ttu-id="f60e5-184">Azure SDK 2.4 ve önceki sürümlerinde, bağlantı dizesi tanılama günlükleri aktarmak için depolama hesabı bilgilerini almak için bir çalışma zamanı tanılama eklenti tarafından kullanıldı.</span><span class="sxs-lookup"><span data-stu-id="f60e5-184">In Azure SDK 2.4 and earlier, the connection string was used as a runtime by the diagnostics plugin to get the storage account information for transferring diagnostics logs.</span></span>
* <span data-ttu-id="f60e5-185">Azure SDK 2.6 ve daha sonra tanılama bağlantı dizesi yayımlama sırasında uygun depolama hesap bilgileriyle tanılama uzantısını yapılandırmak için Visual Studio tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f60e5-185">In Azure SDK 2.6 and later, the diagnostics connection string is used by Visual Studio to configure the diagnostics extension with the appropriate storage account information during publishing.</span></span> <span data-ttu-id="f60e5-186">Bağlantı dizesi, Visual Studio yayımlama için kullanacağı farklı hizmet yapılandırması için farklı depolama hesapları tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f60e5-186">The connection string lets you define different storage accounts for different service configurations that Visual Studio will use when publishing.</span></span> <span data-ttu-id="f60e5-187">Ancak, tanılama eklentisi artık (sonra Azure SDK 2.5) kullanılabilir olmadığından, .cscfg dosyası tek başına tanılama uzantısını etkinleştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="f60e5-187">However, because the diagnostics plugin is no longer available (after Azure SDK 2.5), the .cscfg file by itself can't enable the Diagnostics Extension.</span></span> <span data-ttu-id="f60e5-188">Uzantısı ayrı olarak Visual Studio veya PowerShell gibi araçlar aracılığıyla etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f60e5-188">You have to enable the extension separately through tools such as Visual Studio or PowerShell.</span></span>
* <span data-ttu-id="f60e5-189">Tanılama uzantısını PowerShell ile yapılandırma işlemini basitleştirmek için Visual Studio Paketi çıktısını de tanılama uzantısını her rol için ortak yapılandırma XML içeriyor.</span><span class="sxs-lookup"><span data-stu-id="f60e5-189">To simplify the process of configuring the diagnostics extension with PowerShell, the package output from Visual Studio also contains the public configuration XML for the diagnostics extension for each role.</span></span> <span data-ttu-id="f60e5-190">Visual Studio tanılama bağlantı dizesi ortak yapılandırmada depolama hesabı bilgilerini doldurmak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="f60e5-190">Visual Studio uses the diagnostics connection string to populate the storage account information present in the public configuration.</span></span> <span data-ttu-id="f60e5-191">Genel yapılandırma dosyaları Uzantıları klasöründe oluşturulur ve desen PaaSDiagnostics izleyin. <RoleName>. PubConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="f60e5-191">The public config files are created in the Extensions folder and follow the pattern PaaSDiagnostics.<RoleName>.PubConfig.xml.</span></span> <span data-ttu-id="f60e5-192">Tüm PowerShell tabanlı dağıtımlar, her yapılandırma bir Role eşleştirmek için bu deseni kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f60e5-192">Any PowerShell based deployments can use this pattern to map each configuration to a Role.</span></span>
* <span data-ttu-id="f60e5-193">.Cscfg dosyasında bağlantı dizesini de Azure portal tarafından içinde görüntülenebilir tanılama verilerini erişmek için kullanılan **izleme** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="f60e5-193">The connection string in the .cscfg file is also used by the Azure portal to access the diagnostics data so it can appear in the **Monitoring** tab.</span></span> <span data-ttu-id="f60e5-194">Bağlantı dizesi, ayrıntılı izleme verileri portalda göstermek için bu hizmeti yapılandırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f60e5-194">The connection string is needed to configure the service to show verbose monitoring data in the portal.</span></span>

#### <a name="migrating-projects-to-azure-sdk-26-and-later"></a><span data-ttu-id="f60e5-195">Azure SDK 2.6 ve daha sonra geçirme projeleri</span><span class="sxs-lookup"><span data-stu-id="f60e5-195">Migrating projects to Azure SDK 2.6 and later</span></span>
<span data-ttu-id="f60e5-196">Ardından .wadcfgx dosyasında belirtilen tanılama depolama hesabı varsa Azure SDK 2.5-Azure SDK 2.6 veya sonraki sürümleri geçirilirken var. kalır.</span><span class="sxs-lookup"><span data-stu-id="f60e5-196">When migrating from Azure SDK 2.5 to Azure SDK 2.6 or later, if you had a diagnostics storage account specified in the .wadcfgx file, then it will stay there.</span></span> <span data-ttu-id="f60e5-197">Farklı depolama hesapları farklı depolama yapılandırmaları için kullanma esnekliğini yararlanmak için bağlantı dizesi projenize el ile eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f60e5-197">To take advantage of the flexibility of using different storage accounts for different storage configurations, you'll have to manually add the connection string to your project.</span></span> <span data-ttu-id="f60e5-198">Azure SDK 2.4 veya daha önceki Azure SDK 2.6 proje geçiş, tanılama bağlantı dizeleri korunur.</span><span class="sxs-lookup"><span data-stu-id="f60e5-198">If you're migrating a project from Azure SDK 2.4 or earlier to Azure SDK 2.6, then the diagnostics connection strings are preserved.</span></span> <span data-ttu-id="f60e5-199">Ancak, nasıl bağlantı dizeleri Azure SDK 2.6 belirtildiği şekilde önceki bölümde davranılır değişiklikler lütfen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f60e5-199">However, please note the changes in how connection strings are treated in Azure SDK 2.6 as specified in the previous section.</span></span>

#### <a name="how-visual-studio-determines-the-diagnostics-storage-account"></a><span data-ttu-id="f60e5-200">Visual Studio tanılama depolama hesabı nasıl belirler</span><span class="sxs-lookup"><span data-stu-id="f60e5-200">How Visual Studio determines the diagnostics storage account</span></span>
* <span data-ttu-id="f60e5-201">Bir tanılama bağlantı dizesi .cscfg dosyasında belirtilmediği takdirde, Visual Studio yayımlarken ve genel yapılandırma xml dosyalarını paketlemesi sırasında oluştururken tanılama uzantısını yapılandırmak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="f60e5-201">If a diagnostics connection string is specified in the .cscfg file, Visual Studio uses it to configure the diagnostics extension when publishing, and when generating the public configuration xml files during packaging.</span></span>
* <span data-ttu-id="f60e5-202">Bir tanılama bağlantı dizesi .cscfg dosyasında belirtilirse, ardından Visual Studio .wadcfgx dosyasında belirtilen depolama hesabı yayımlama ve genel yapılandırma xml dosyalarını oluşturmak tanılama uzantısını yapılandırmak üzere kullanmaya geri döner paketleme olduğunda.</span><span class="sxs-lookup"><span data-stu-id="f60e5-202">If no diagnostics connection string is specified in the .cscfg file, then Visual Studio falls back to using the storage account specified in the .wadcfgx file to configure the diagnostics extension when publishing, and generating the public configuration xml files when packaging.</span></span>
* <span data-ttu-id="f60e5-203">.Cscfg dosyası tanılama bağlantı dizesinde .wadcfgx dosya depolama hesabında daha önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="f60e5-203">The diagnostics connection string in the .cscfg file takes precedence over the storage account in the .wadcfgx file.</span></span> <span data-ttu-id="f60e5-204">Bir tanılama bağlantı dizesi .cscfg dosyasında belirtilmediği takdirde, Visual Studio kullanan ve .wadcfgx depolama hesabında yok sayar.</span><span class="sxs-lookup"><span data-stu-id="f60e5-204">If a diagnostics connection string is specified in the .cscfg file, then Visual Studio uses that and ignores the storage account in .wadcfgx.</span></span>

#### <a name="what-does-the-update-development-storage-connection-strings-checkbox-do"></a><span data-ttu-id="f60e5-205">"Güncelleştirme geliştirme storage bağlantı dizelerini..." yaptığı</span><span class="sxs-lookup"><span data-stu-id="f60e5-205">What does the "Update development storage connection strings…"</span></span> <span data-ttu-id="f60e5-206">onay kutusu musunuz?</span><span class="sxs-lookup"><span data-stu-id="f60e5-206">checkbox do?</span></span>
<span data-ttu-id="f60e5-207">Onay kutusunu **güncelleştirme geliştirme storage bağlantı dizelerini tanılama ve önbelleğe alma için Microsoft Azure depolama hesabı kimlik bilgileriyle Microsoft Azure yayımlama sırasında** tüm geliştirme güncelleştirmek için kullanışlı bir yöntem sunar Yayımlama sırasında belirtilen Azure depolama hesabı ile depolama hesabı bağlantı dizeleri.</span><span class="sxs-lookup"><span data-stu-id="f60e5-207">The checkbox for **Update development storage connection strings for Diagnostics and Caching with Microsoft Azure storage account credentials when publishing to Microsoft Azure** gives you a convenient way to update any development storage account connection strings with the Azure storage account specified during publishing.</span></span>

<span data-ttu-id="f60e5-208">Örneğin, bu onay kutusunu seçin ve tanılama bağlantı dizesini belirtir varsayalım `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="f60e5-208">For example, suppose you select this checkbox and the diagnostics connection string specifies `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="f60e5-209">Projeyi Azure'da yayımlarken, Visual Studio Yayımlama Sihirbazı'nda belirtilen depolama hesabıyla tanılama bağlantı dizesi otomatik olarak güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="f60e5-209">When you publish the project to Azure, Visual Studio will automatically update the diagnostics connection string with the storage account you specified in the Publish wizard.</span></span> <span data-ttu-id="f60e5-210">Gerçek depolama hesabı tanılama bağlantı dizesi olarak belirtilmişse, ancak, ardından o hesabı yerine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f60e5-210">However, if a real storage account was specified as the diagnostics connection string, then that account is used instead.</span></span>

### <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a><span data-ttu-id="f60e5-211">Tanılama işlevleri farklılıkları Azure SDK 2.4 ve önceki ve Azure SDK 2,5 ve üzeri</span><span class="sxs-lookup"><span data-stu-id="f60e5-211">Diagnostics functionality differences between Azure SDK 2.4 and earlier and Azure SDK 2.5 and later</span></span>
<span data-ttu-id="f60e5-212">Projenizi Azure SDK 2.4 Azure SDK 2.5 veya sonraki bir sürümüne yükseltiyorsanız, aşağıdaki tanılama işlevleri farklılıkları göz önünde bulundurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f60e5-212">If you're upgrading your project from Azure SDK 2.4 to Azure SDK 2.5 or later, you should bear in mind the following diagnostics functionality differences.</span></span>

* <span data-ttu-id="f60e5-213">**Yapılandırma API'leri dışıdır** – tanılama program yapılandırması Azure SDK 2.4 veya önceki sürümlerde kullanılabilir, ancak Azure SDK 2.5 ve daha sonra kullanım dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="f60e5-213">**Configuration APIs are deprecated** – Programmatic configuration of diagnostics is available in Azure SDK 2.4 or earlier versions, but is deprecated in Azure SDK 2.5 and later.</span></span> <span data-ttu-id="f60e5-214">Tanılama yapılandırmanızı kodda şu anda tanımlanmış olması durumunda, bu ayarları çalışmaya devam Diagnostics sırayla geçirilen proje en baştan yeniden yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f60e5-214">If your diagnostics configuration is currently defined in code, you'll need to reconfigure those settings from scratch in the migrated project in order for diagnostics to keep working.</span></span> <span data-ttu-id="f60e5-215">Tanılama yapılandırması için Azure SDK 2.4 diagnostics.wadcfg ve diagnostics.wadcfgx ve sonraki sürümler için Azure SDK 2.5 dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="f60e5-215">The diagnostics configuration file for Azure SDK 2.4 is diagnostics.wadcfg, and diagnostics.wadcfgx for Azure SDK 2.5 and later.</span></span>
* <span data-ttu-id="f60e5-216">**Bulut hizmeti uygulamaları için tanılama yalnızca rol düzeyinde örnek düzeyinde yapılandırılabilir.**</span><span class="sxs-lookup"><span data-stu-id="f60e5-216">**Diagnostics for cloud service applications can only be configured at the role level, not at the instance level.**</span></span>
* <span data-ttu-id="f60e5-217">**Uygulamanızı dağıtma her zaman, tanılama yapılandırması güncelleştirilir** – tanılama yapılandırmanızı Server Explorer'dan değiştirirseniz ve uygulamanızı yeniden dağıtın bu eşlik sorunlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="f60e5-217">**Every time you deploy your app, the diagnostics configuration is updated** – This can cause parity issues if you change your diagnostics configuration from Server Explorer and then redeploy your app.</span></span>
* <span data-ttu-id="f60e5-218">**Azure SDK 2.5 ve daha sonra kilitlenme bilgi dökümleri tanılama yapılandırma dosyasındaki kodu değil, yapılandırılan** – kodda yapılandırılmış kilitlenme bilgi dökümleri varsa, el ile yapılandırma koddan yapılandırma dosyasına aktarmak çünkü gerekir kilitlenme bilgi dökümleri geçiş sırasında Azure SDK 2.6 aktarılmaz.</span><span class="sxs-lookup"><span data-stu-id="f60e5-218">**In Azure SDK 2.5 and later, crash dumps are configured in the diagnostics configuration file, not in code** – If you have crash dumps configured in code, you'll have to manually transfer the configuration from code to the configuration file, because the crash dumps aren't transferred during the migration to Azure SDK 2.6.</span></span>

