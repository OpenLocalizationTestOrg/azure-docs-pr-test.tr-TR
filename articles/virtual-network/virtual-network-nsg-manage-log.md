---
title: "İzleme işlemleri, olaylar ve sayaçlar için Nsg'ler | Microsoft Docs"
description: "Sayaçlar, olayları ve Nsg'ler için işlem günlüğünü etkinleştirme hakkında bilgi edinin"
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
ms.openlocfilehash: 552f37dd704de25159bc0f0ad34fdae9ed8b73f5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="log-analytics-for-network-security-groups-nsgs"></a><span data-ttu-id="c559b-103">Ağ güvenlik grupları (NSG’ler) için Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c559b-103">Log analytics for network security groups (NSGs)</span></span>

<span data-ttu-id="c559b-104">Aşağıdaki tanılama günlük kategorileri için Nsg'ler etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c559b-104">You can enable the following diagnostic log categories for NSGs:</span></span>

* <span data-ttu-id="c559b-105">**Olay:** hangi NSG kuralları Vm'lere uygulanan ve örnek MAC adresine dayalı rolleri girişleri içerir.</span><span class="sxs-lookup"><span data-stu-id="c559b-105">**Event:** Contains entries for which NSG rules are applied to VMs and instance roles based on MAC address.</span></span> <span data-ttu-id="c559b-106">Bu kurallar durumunun her 60 saniyede toplanır.</span><span class="sxs-lookup"><span data-stu-id="c559b-106">The status for these rules is collected every 60 seconds.</span></span>
* <span data-ttu-id="c559b-107">**Kural sayacı:** kaç kez her NSG için içerir girişleri kural reddetmek veya trafiğine izin vermek üzere uygulanır.</span><span class="sxs-lookup"><span data-stu-id="c559b-107">**Rule counter:** Contains entries for how many times each NSG rule is applied to deny or allow traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="c559b-108">Tanılama günlükleri, yalnızca Azure Resource Manager dağıtım modeli aracılığıyla dağıtılan Nsg'ler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c559b-108">Diagnostic logs are only available for NSGs deployed through the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="c559b-109">Klasik dağıtım modeli aracılığıyla dağıtılan Nsg'ler için tanılama günlüğü etkinleştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="c559b-109">You cannot enable diagnostic logging for NSGs deployed through the classic deployment model.</span></span> <span data-ttu-id="c559b-110">Daha iyi iki modellerinin anlamak için başvuru [anlama Azure dağıtım modelleri](../resource-manager-deployment-model.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="c559b-110">For a better understanding of the two models, reference the [Understanding Azure deployment models](../resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="c559b-111">Etkinlik günlüğü (daha önce denetim veya işlem günlükleri olarak bilinir) ya da Azure dağıtım modeliyle oluşturulan Nsg'ler için varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="c559b-111">Activity logging (previously known as audit or operational logs) is enabled by default for NSGs created through either Azure deployment model.</span></span> <span data-ttu-id="c559b-112">Hangi işlemleri üzerinde Nsg'ler etkinlik günlüğünde tamamlandığını belirlemek için aşağıdaki kaynak türlerini içeren girdilerini arayın:</span><span class="sxs-lookup"><span data-stu-id="c559b-112">To determine which operations were completed on NSGs in the activity log, look for entries that contain the following resource types:</span></span> 

- <span data-ttu-id="c559b-113">Microsoft.ClassicNetwork/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="c559b-113">Microsoft.ClassicNetwork/networkSecurityGroups</span></span> 
- <span data-ttu-id="c559b-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="c559b-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span></span>
- <span data-ttu-id="c559b-115">Microsoft.Network/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="c559b-115">Microsoft.Network/networkSecurityGroups</span></span>
- <span data-ttu-id="c559b-116">Microsoft.Network/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="c559b-116">Microsoft.Network/networkSecurityGroups/securityRules</span></span> 

<span data-ttu-id="c559b-117">Okuma [Azure etkinlik günlüğü'ne genel bakış](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) etkinlik günlükleri hakkında daha fazla bilgi için makalenin.</span><span class="sxs-lookup"><span data-stu-id="c559b-117">Read the [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) article to learn more about activity logs.</span></span> 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="c559b-118">Tanılama günlüğünü etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c559b-118">Enable diagnostic logging</span></span>

<span data-ttu-id="c559b-119">Tanılama günlüğü etkin, için *her* için veri toplamak istediğiniz NSG.</span><span class="sxs-lookup"><span data-stu-id="c559b-119">Diagnostic logging must be enabled for *each* NSG you want to collect data for.</span></span> <span data-ttu-id="c559b-120">[Genel bakış, Azure tanılama günlükleri](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) makalede açıklanır tanılama günlüklerini burada gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="c559b-120">The [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article explains where diagnostic logs can be sent.</span></span> <span data-ttu-id="c559b-121">Varolan bir NSG yoksa, bölümündeki adımları tamamlamanız [bir ağ güvenlik grubu oluşturun](virtual-networks-create-nsg-arm-pportal.md) makale bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c559b-121">If you don't have an existing NSG, complete the steps in the [Create a network security group](virtual-networks-create-nsg-arm-pportal.md) article to create one.</span></span> <span data-ttu-id="c559b-122">NSG aşağıdaki yöntemlerden birini kullanarak oturum tanılama etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c559b-122">You can enable NSG diagnostic logging using any of the following methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="c559b-123">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="c559b-123">Azure portal</span></span>

<span data-ttu-id="c559b-124">Günlük, oturum açma etkinleştirmek için portalı kullanmak için [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c559b-124">To use the portal to enable logging, login to the [portal](https://portal.azure.com).</span></span> <span data-ttu-id="c559b-125">Tıklatın **daha fazla hizmet**, ardından *ağ güvenlik grubu*.</span><span class="sxs-lookup"><span data-stu-id="c559b-125">Click **More services**, then type *network security groups*.</span></span> <span data-ttu-id="c559b-126">İçin günlük kaydını etkinleştirmek istediğiniz NSG seçin.</span><span class="sxs-lookup"><span data-stu-id="c559b-126">Select the NSG you want to enable logging for.</span></span> <span data-ttu-id="c559b-127">İşlem olmayan kaynakları için yönergeleri izleyin [portalında tanılama günlüklerini etkinleştirme](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) makalesi.</span><span class="sxs-lookup"><span data-stu-id="c559b-127">Follow the instructions for non-compute resources in the [Enable diagnostic logs in the portal](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="c559b-128">Seçin **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, veya her iki kategorilerini günlükleri.</span><span class="sxs-lookup"><span data-stu-id="c559b-128">Select **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, or both categories of logs.</span></span>

### <a name="powershell"></a><span data-ttu-id="c559b-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c559b-129">PowerShell</span></span>

<span data-ttu-id="c559b-130">Günlük kaydını etkinleştirmek için PowerShell kullanmak için ' ndaki yönergeleri izleyin [PowerShell aracılığıyla tanılama günlüklerini etkinleştirme](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) makalesi.</span><span class="sxs-lookup"><span data-stu-id="c559b-130">To use PowerShell to enable logging, follow the instructions in the [Enable diagnostic logs via PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="c559b-131">Bir komut makaleden girmeden önce aşağıdaki bilgileri değerlendirin:</span><span class="sxs-lookup"><span data-stu-id="c559b-131">Evaluate the following information before entering a command from the article:</span></span>

- <span data-ttu-id="c559b-132">İçin kullanılacak bir değer belirleyebilirsiniz `-ResourceId` aşağıdaki değiştirerek parametresi [metin] uygun şekilde, sonra komutu girerek `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span><span class="sxs-lookup"><span data-stu-id="c559b-132">You can determine the value to use for the `-ResourceId` parameter by replacing the following [text], as appropriate, then entering the command `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span></span> <span data-ttu-id="c559b-133">Komut Kimliği çıktısı için benzer */subscriptions/ [abonelik Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG adı]*.</span><span class="sxs-lookup"><span data-stu-id="c559b-133">The ID output from the command looks similar to */subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="c559b-134">Yalnızca günlük kategoriden veri toplamak istiyorsanız eklemek `-Categories [category]` kategori olduğu ya da makalede, komut sonuna *NetworkSecurityGroupEvent* veya *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="c559b-134">If you only want to collect data from log category add `-Categories [category]` to the end of the command in the article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="c559b-135">Kullanmazsanız `-Categories` parametresi, veri toplama kategorileri hem günlük için etkinleştirildi.</span><span class="sxs-lookup"><span data-stu-id="c559b-135">If you don't use the `-Categories` parameter, data collection is enabled for both log categories.</span></span>

### <a name="azure-command-line-interface-cli"></a><span data-ttu-id="c559b-136">Azure komut satırı arabirimi (CLI)</span><span class="sxs-lookup"><span data-stu-id="c559b-136">Azure command-line interface (CLI)</span></span>

<span data-ttu-id="c559b-137">Günlük kaydını etkinleştirmek için CLI kullanmak için ' ndaki yönergeleri izleyin [CLI aracılığıyla tanılama günlüklerini etkinleştirme](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) makalesi.</span><span class="sxs-lookup"><span data-stu-id="c559b-137">To use the CLI to enable logging, follow the instructions in the [Enable diagnostic logs via CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="c559b-138">Bir komut makaleden girmeden önce aşağıdaki bilgileri değerlendirin:</span><span class="sxs-lookup"><span data-stu-id="c559b-138">Evaluate the following information before entering a command from the article:</span></span>

- <span data-ttu-id="c559b-139">İçin kullanılacak bir değer belirleyebilirsiniz `-ResourceId` aşağıdaki değiştirerek parametresi [metin] uygun şekilde, sonra komutu girerek `azure network nsg show [resource-group-name] [nsg-name]`.</span><span class="sxs-lookup"><span data-stu-id="c559b-139">You can determine the value to use for the `-ResourceId` parameter by replacing the following [text], as appropriate, then entering the command `azure network nsg show [resource-group-name] [nsg-name]`.</span></span> <span data-ttu-id="c559b-140">Komut Kimliği çıktısı için benzer */subscriptions/ [abonelik Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG adı]*.</span><span class="sxs-lookup"><span data-stu-id="c559b-140">The ID output from the command looks similar to */subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="c559b-141">Yalnızca günlük kategoriden veri toplamak istiyorsanız eklemek `-Categories [category]` kategori olduğu ya da makalede, komut sonuna *NetworkSecurityGroupEvent* veya *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="c559b-141">If you only want to collect data from log category add `-Categories [category]` to the end of the command in the article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="c559b-142">Kullanmazsanız `-Categories` parametresi, veri toplama kategorileri hem günlük için etkinleştirildi.</span><span class="sxs-lookup"><span data-stu-id="c559b-142">If you don't use the `-Categories` parameter, data collection is enabled for both log categories.</span></span>

## <a name="logged-data"></a><span data-ttu-id="c559b-143">Günlüğe kaydedilen veriler</span><span class="sxs-lookup"><span data-stu-id="c559b-143">Logged data</span></span>

<span data-ttu-id="c559b-144">JSON biçimli veriler için her iki günlüklerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="c559b-144">JSON-formatted data is written for both logs.</span></span> <span data-ttu-id="c559b-145">Her günlük türü için yazılan özel veriler aşağıdaki bölümlerde listelenmiştir:</span><span class="sxs-lookup"><span data-stu-id="c559b-145">The specific data written for each log type is listed in the following sections:</span></span>

### <a name="event-log"></a><span data-ttu-id="c559b-146">Olay günlüğü</span><span class="sxs-lookup"><span data-stu-id="c559b-146">Event log</span></span>
<span data-ttu-id="c559b-147">Bu günlük kuralları Vm'lere uygulanan ve MAC adresine dayalı hizmet rolü örneklerinin bulut hangi NSG hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="c559b-147">This log contains information about which NSG rules are applied to VMs and cloud service role instances, based on MAC address.</span></span> <span data-ttu-id="c559b-148">Aşağıdaki örnek veriler, her olay için günlüğe kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="c559b-148">The following example data is logged for each event:</span></span>

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

### <a name="rule-counter-log"></a><span data-ttu-id="c559b-149">Kural sayacı günlüğü</span><span class="sxs-lookup"><span data-stu-id="c559b-149">Rule counter log</span></span>

<span data-ttu-id="c559b-150">Bu günlük kaynaklara uygulanma her bir kural hakkındaki bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="c559b-150">This log contains information about each rule applied to resources.</span></span> <span data-ttu-id="c559b-151">Aşağıdaki örnek veriler her zaman bir kuralın uygulanacağı günlüğe kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="c559b-151">The following example data is logged each time a rule is applied:</span></span>

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

## <a name="view-and-analyze-logs"></a><span data-ttu-id="c559b-152">Görüntülemek ve günlüklerini analiz edin</span><span class="sxs-lookup"><span data-stu-id="c559b-152">View and analyze logs</span></span>

<span data-ttu-id="c559b-153">Etkinlik günlüğü verilerini görüntülemek nasıl öğrenmek için [Azure etkinlik günlüğü'ne genel bakış](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="c559b-153">To learn how to view activity log data, read the [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="c559b-154">Tanılama günlük verilerini görüntülemek nasıl öğrenmek için [genel bakış, Azure tanılama günlükleri](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="c559b-154">To learn how to view diagnostic log data, read the [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="c559b-155">Günlük analizi için tanılama verilerini gönderirseniz, kullanabileceğiniz [Azure ağ güvenlik grubu analytics](../log-analytics/log-analytics-azure-networking-analytics.md) Gelişmiş ınsights (Önizleme) yönetimi çözümü.</span><span class="sxs-lookup"><span data-stu-id="c559b-155">If you send diagnostics data to Log Analytics, you can use the [Azure Network Security Group analytics](../log-analytics/log-analytics-azure-networking-analytics.md) (preview) management solution for enhanced insights.</span></span> 
