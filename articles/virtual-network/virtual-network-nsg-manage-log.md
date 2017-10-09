---
title: "aaaMonitor işlemleri, olayları ve Nsg'ler sayaçları | Microsoft Docs"
description: "Bilgi nasıl tooenable sayaçları, olaylar ve Nsg'ler için işlem günlüğü"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2e699078-043f-48bd-8aa8-b011a32d98ca
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/31/2017
ms.author: jdial
ms.openlocfilehash: f16f1a0ad693028ee7aba21574b5c8ddfcd27096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-network-security-groups-nsgs"></a><span data-ttu-id="b491d-103">Ağ güvenlik grupları (NSG’ler) için Log Analytics</span><span class="sxs-lookup"><span data-stu-id="b491d-103">Log analytics for network security groups (NSGs)</span></span>

<span data-ttu-id="b491d-104">Tanılama günlük kategorileri için Nsg'ler aşağıdaki hello etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b491d-104">You can enable hello following diagnostic log categories for NSGs:</span></span>

* <span data-ttu-id="b491d-105">**Olay:** için hangi NSG kuralları: uygulanan tooVMs ve örnek rolleriniz MAC adresine dayalı girişleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b491d-105">**Event:** Contains entries for which NSG rules are applied tooVMs and instance roles based on MAC address.</span></span> <span data-ttu-id="b491d-106">Bu kurallar Hello durumunun her 60 saniyede toplanır.</span><span class="sxs-lookup"><span data-stu-id="b491d-106">hello status for these rules is collected every 60 seconds.</span></span>
* <span data-ttu-id="b491d-107">**Kural sayacı:** kaç kez her NSG için içerir girişleri kural uygulanan toodeny ya da trafiğine izin verme.</span><span class="sxs-lookup"><span data-stu-id="b491d-107">**Rule counter:** Contains entries for how many times each NSG rule is applied toodeny or allow traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="b491d-108">Tanılama günlüklerini yalnızca hello Azure Resource Manager dağıtım modeli aracılığıyla dağıtılan Nsg'ler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b491d-108">Diagnostic logs are only available for NSGs deployed through hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="b491d-109">Merhaba Klasik dağıtım modeli aracılığıyla dağıtılan Nsg'ler için tanılama günlüğü etkinleştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="b491d-109">You cannot enable diagnostic logging for NSGs deployed through hello classic deployment model.</span></span> <span data-ttu-id="b491d-110">Daha iyi hello iki modellerinin anlamak için hello başvuru [anlama Azure dağıtım modelleri](../resource-manager-deployment-model.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="b491d-110">For a better understanding of hello two models, reference hello [Understanding Azure deployment models](../resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="b491d-111">Etkinlik günlüğü (daha önce denetim veya işlem günlükleri olarak bilinir) ya da Azure dağıtım modeliyle oluşturulan Nsg'ler için varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="b491d-111">Activity logging (previously known as audit or operational logs) is enabled by default for NSGs created through either Azure deployment model.</span></span> <span data-ttu-id="b491d-112">hangi işlemleri hello etkinlik günlüğünde, kaynak türleri aşağıdaki hello içeren girdileri arayın üzerinde Nsg'ler tamamlandığını toodetermine:</span><span class="sxs-lookup"><span data-stu-id="b491d-112">toodetermine which operations were completed on NSGs in hello activity log, look for entries that contain hello following resource types:</span></span> 

- <span data-ttu-id="b491d-113">Microsoft.ClassicNetwork/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="b491d-113">Microsoft.ClassicNetwork/networkSecurityGroups</span></span> 
- <span data-ttu-id="b491d-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="b491d-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span></span>
- <span data-ttu-id="b491d-115">Microsoft.Network/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="b491d-115">Microsoft.Network/networkSecurityGroups</span></span>
- <span data-ttu-id="b491d-116">Microsoft.Network/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="b491d-116">Microsoft.Network/networkSecurityGroups/securityRules</span></span> 

<span data-ttu-id="b491d-117">Okuma hello [hello Azure etkinlik günlüğü'ne genel bakış](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) makale toolearn etkinlik günlükleri hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="b491d-117">Read hello [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) article toolearn more about activity logs.</span></span> 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="b491d-118">Tanılama günlüğünü etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="b491d-118">Enable diagnostic logging</span></span>

<span data-ttu-id="b491d-119">Tanılama günlüğü etkin, için *her* NSG toocollect verileri istiyor.</span><span class="sxs-lookup"><span data-stu-id="b491d-119">Diagnostic logging must be enabled for *each* NSG you want toocollect data for.</span></span> <span data-ttu-id="b491d-120">Merhaba [genel bakış, Azure tanılama günlükleri](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) makalede açıklanır tanılama günlüklerini burada gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="b491d-120">hello [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article explains where diagnostic logs can be sent.</span></span> <span data-ttu-id="b491d-121">Varolan bir NSG yoksa, tam hello hello adımları [bir ağ güvenlik grubu oluşturun](virtual-networks-create-nsg-arm-pportal.md) makale toocreate biri.</span><span class="sxs-lookup"><span data-stu-id="b491d-121">If you don't have an existing NSG, complete hello steps in hello [Create a network security group](virtual-networks-create-nsg-arm-pportal.md) article toocreate one.</span></span> <span data-ttu-id="b491d-122">NSG herhangi bir yöntem aşağıdaki hello kullanarak oturum tanılama etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b491d-122">You can enable NSG diagnostic logging using any of hello following methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="b491d-123">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="b491d-123">Azure portal</span></span>

<span data-ttu-id="b491d-124">toouse hello portal tooenable günlüğe kaydetme, oturum açma toohello [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b491d-124">toouse hello portal tooenable logging, login toohello [portal](https://portal.azure.com).</span></span> <span data-ttu-id="b491d-125">Tıklatın **daha fazla hizmet**, ardından *ağ güvenlik grubu*.</span><span class="sxs-lookup"><span data-stu-id="b491d-125">Click **More services**, then type *network security groups*.</span></span> <span data-ttu-id="b491d-126">Hello için oturum açma tooenable istediğiniz NSG seçin.</span><span class="sxs-lookup"><span data-stu-id="b491d-126">Select hello NSG you want tooenable logging for.</span></span> <span data-ttu-id="b491d-127">İşlem olmayan kaynakları hello Hello yönergeleri izleyin [hello portalında tanılama günlüklerini etkinleştirme](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) makalesi.</span><span class="sxs-lookup"><span data-stu-id="b491d-127">Follow hello instructions for non-compute resources in hello [Enable diagnostic logs in hello portal](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="b491d-128">Seçin **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, veya her iki kategorilerini günlükleri.</span><span class="sxs-lookup"><span data-stu-id="b491d-128">Select **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, or both categories of logs.</span></span>

### <a name="powershell"></a><span data-ttu-id="b491d-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b491d-129">PowerShell</span></span>

<span data-ttu-id="b491d-130">Günlük, toouse PowerShell tooenable hello içinde hello yönergeleri izleyerek [PowerShell aracılığıyla tanılama günlüklerini etkinleştirme](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) makale.</span><span class="sxs-lookup"><span data-stu-id="b491d-130">toouse PowerShell tooenable logging, follow hello instructions in hello [Enable diagnostic logs via PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="b491d-131">Bir komut hello makaleden girmeden önce bilgisinden hello değerlendirin:</span><span class="sxs-lookup"><span data-stu-id="b491d-131">Evaluate hello following information before entering a command from hello article:</span></span>

- <span data-ttu-id="b491d-132">Merhaba değeri toouse hello için belirleyebilirsiniz `-ResourceId` hello komutunu girerek aşağıdaki hello [metin] uygun şekilde değiştirerek parametresi `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span><span class="sxs-lookup"><span data-stu-id="b491d-132">You can determine hello value toouse for hello `-ResourceId` parameter by replacing hello following [text], as appropriate, then entering hello command `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span></span> <span data-ttu-id="b491d-133">Merhaba kimliği hello komut çıktısı arar benzer çok*/subscriptions/ [abonelik Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG adı]*.</span><span class="sxs-lookup"><span data-stu-id="b491d-133">hello ID output from hello command looks similar too*/subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="b491d-134">Günlük kategori toocollect verileri yalnızca istiyorsanız ekleyin `-Categories [category]` toohello kategori olduğu ya da hello makaledeki hello komutunun sonuna *NetworkSecurityGroupEvent* veya *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="b491d-134">If you only want toocollect data from log category add `-Categories [category]` toohello end of hello command in hello article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="b491d-135">Merhaba kullanmazsanız `-Categories` parametresi, veri toplama kategorileri hem günlük için etkinleştirildi.</span><span class="sxs-lookup"><span data-stu-id="b491d-135">If you don't use hello `-Categories` parameter, data collection is enabled for both log categories.</span></span>

### <a name="azure-command-line-interface-cli"></a><span data-ttu-id="b491d-136">Azure komut satırı arabirimi (CLI)</span><span class="sxs-lookup"><span data-stu-id="b491d-136">Azure command-line interface (CLI)</span></span>

<span data-ttu-id="b491d-137">toouse CLI tooenable günlük Merhaba, hello hello yönergeleri izleyin [CLI aracılığıyla tanılama günlüklerini etkinleştirme](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) makalesi.</span><span class="sxs-lookup"><span data-stu-id="b491d-137">toouse hello CLI tooenable logging, follow hello instructions in hello [Enable diagnostic logs via CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="b491d-138">Bir komut hello makaleden girmeden önce bilgisinden hello değerlendirin:</span><span class="sxs-lookup"><span data-stu-id="b491d-138">Evaluate hello following information before entering a command from hello article:</span></span>

- <span data-ttu-id="b491d-139">Merhaba değeri toouse hello için belirleyebilirsiniz `-ResourceId` hello komutunu girerek aşağıdaki hello [metin] uygun şekilde değiştirerek parametresi `azure network nsg show [resource-group-name] [nsg-name]`.</span><span class="sxs-lookup"><span data-stu-id="b491d-139">You can determine hello value toouse for hello `-ResourceId` parameter by replacing hello following [text], as appropriate, then entering hello command `azure network nsg show [resource-group-name] [nsg-name]`.</span></span> <span data-ttu-id="b491d-140">Merhaba kimliği hello komut çıktısı arar benzer çok*/subscriptions/ [abonelik Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG adı]*.</span><span class="sxs-lookup"><span data-stu-id="b491d-140">hello ID output from hello command looks similar too*/subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="b491d-141">Günlük kategori toocollect verileri yalnızca istiyorsanız ekleyin `-Categories [category]` toohello kategori olduğu ya da hello makaledeki hello komutunun sonuna *NetworkSecurityGroupEvent* veya *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="b491d-141">If you only want toocollect data from log category add `-Categories [category]` toohello end of hello command in hello article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="b491d-142">Merhaba kullanmazsanız `-Categories` parametresi, veri toplama kategorileri hem günlük için etkinleştirildi.</span><span class="sxs-lookup"><span data-stu-id="b491d-142">If you don't use hello `-Categories` parameter, data collection is enabled for both log categories.</span></span>

## <a name="logged-data"></a><span data-ttu-id="b491d-143">Günlüğe kaydedilen veriler</span><span class="sxs-lookup"><span data-stu-id="b491d-143">Logged data</span></span>

<span data-ttu-id="b491d-144">JSON biçimli veriler için her iki günlüklerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="b491d-144">JSON-formatted data is written for both logs.</span></span> <span data-ttu-id="b491d-145">Her günlük türü için yazılan hello belirli veri bölümleri aşağıdaki hello listelenir:</span><span class="sxs-lookup"><span data-stu-id="b491d-145">hello specific data written for each log type is listed in hello following sections:</span></span>

### <a name="event-log"></a><span data-ttu-id="b491d-146">Olay günlüğü</span><span class="sxs-lookup"><span data-stu-id="b491d-146">Event log</span></span>
<span data-ttu-id="b491d-147">Bu günlük kuralları uygulanan tooVMs olan ve MAC adresine dayalı hizmet rolü örneklerinin bulut hangi NSG hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="b491d-147">This log contains information about which NSG rules are applied tooVMs and cloud service role instances, based on MAC address.</span></span> <span data-ttu-id="b491d-148">Örnek veri aşağıdaki hello her olay için günlüğe kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="b491d-148">hello following example data is logged for each event:</span></span>

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupEvent",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION-ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupEvents",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-B791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "priority":1000,
        "type":"allow",
        "conditions":{
            "protocols":"6",
            "destinationPortRange":"3389-3389",
            "sourcePortRange":"0-65535",
            "sourceIP":"0.0.0.0/0",
            "destinationIP":"0.0.0.0/0"
            }
        }
}
```

### <a name="rule-counter-log"></a><span data-ttu-id="b491d-149">Kural sayacı günlüğü</span><span class="sxs-lookup"><span data-stu-id="b491d-149">Rule counter log</span></span>

<span data-ttu-id="b491d-150">Bu günlük, her kural tooresources hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="b491d-150">This log contains information about each rule applied tooresources.</span></span> <span data-ttu-id="b491d-151">Hello bir kuralın uygulanacağı her zaman en aşağıdaki örnek veriler günlüğe kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="b491d-151">hello following example data is logged each time a rule is applied:</span></span>

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupRuleCounter",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]TESTRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupCounters",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "type":"allow",
        "matchedConnections":125
        }
}
```

## <a name="view-and-analyze-logs"></a><span data-ttu-id="b491d-152">Görüntülemek ve günlüklerini analiz edin</span><span class="sxs-lookup"><span data-stu-id="b491d-152">View and analyze logs</span></span>

<span data-ttu-id="b491d-153">toolearn tooview etkinlik oturum nasıl veri okuma hello [hello Azure etkinlik günlüğü'ne genel bakış](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="b491d-153">toolearn how tooview activity log data, read hello [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="b491d-154">toolearn tooview tanılama günlük nasıl veri okuma hello [genel bakış, Azure tanılama günlükleri](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="b491d-154">toolearn how tooview diagnostic log data, read hello [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="b491d-155">Tanılama veri tooLog Analytics gönderirseniz, hello kullanabilirsiniz [Azure ağ güvenlik grubu analytics](../log-analytics/log-analytics-azure-networking-analytics.md) Gelişmiş ınsights (Önizleme) yönetimi çözümü.</span><span class="sxs-lookup"><span data-stu-id="b491d-155">If you send diagnostics data tooLog Analytics, you can use hello [Azure Network Security Group analytics](../log-analytics/log-analytics-azure-networking-analytics.md) (preview) management solution for enhanced insights.</span></span> 
