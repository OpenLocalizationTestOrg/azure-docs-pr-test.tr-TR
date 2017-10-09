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
# <a name="log-analytics-for-network-security-groups-nsgs"></a>Ağ güvenlik grupları (NSG’ler) için Log Analytics

Tanılama günlük kategorileri için Nsg'ler aşağıdaki hello etkinleştirebilirsiniz:

* **Olay:** için hangi NSG kuralları: uygulanan tooVMs ve örnek rolleriniz MAC adresine dayalı girişleri içerir. Bu kurallar Hello durumunun her 60 saniyede toplanır.
* **Kural sayacı:** kaç kez her NSG için içerir girişleri kural uygulanan toodeny ya da trafiğine izin verme.

> [!NOTE]
> Tanılama günlüklerini yalnızca hello Azure Resource Manager dağıtım modeli aracılığıyla dağıtılan Nsg'ler için kullanılabilir. Merhaba Klasik dağıtım modeli aracılığıyla dağıtılan Nsg'ler için tanılama günlüğü etkinleştiremezsiniz. Daha iyi hello iki modellerinin anlamak için hello başvuru [anlama Azure dağıtım modelleri](../resource-manager-deployment-model.md) makalesi.

Etkinlik günlüğü (daha önce denetim veya işlem günlükleri olarak bilinir) ya da Azure dağıtım modeliyle oluşturulan Nsg'ler için varsayılan olarak etkindir. hangi işlemleri hello etkinlik günlüğünde, kaynak türleri aşağıdaki hello içeren girdileri arayın üzerinde Nsg'ler tamamlandığını toodetermine: 

- Microsoft.ClassicNetwork/networkSecurityGroups 
- Microsoft.ClassicNetwork/networkSecurityGroups/securityRules
- Microsoft.Network/networkSecurityGroups
- Microsoft.Network/networkSecurityGroups/securityRules 

Okuma hello [hello Azure etkinlik günlüğü'ne genel bakış](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) makale toolearn etkinlik günlükleri hakkında daha fazla bilgi. 

## <a name="enable-diagnostic-logging"></a>Tanılama günlüğünü etkinleştirme

Tanılama günlüğü etkin, için *her* NSG toocollect verileri istiyor. Merhaba [genel bakış, Azure tanılama günlükleri](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) makalede açıklanır tanılama günlüklerini burada gönderilebilir. Varolan bir NSG yoksa, tam hello hello adımları [bir ağ güvenlik grubu oluşturun](virtual-networks-create-nsg-arm-pportal.md) makale toocreate biri. NSG herhangi bir yöntem aşağıdaki hello kullanarak oturum tanılama etkinleştirebilirsiniz:

### <a name="azure-portal"></a>Azure portalına

toouse hello portal tooenable günlüğe kaydetme, oturum açma toohello [portal](https://portal.azure.com). Tıklatın **daha fazla hizmet**, ardından *ağ güvenlik grubu*. Hello için oturum açma tooenable istediğiniz NSG seçin. İşlem olmayan kaynakları hello Hello yönergeleri izleyin [hello portalında tanılama günlüklerini etkinleştirme](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) makalesi. Seçin **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, veya her iki kategorilerini günlükleri.

### <a name="powershell"></a>PowerShell

Günlük, toouse PowerShell tooenable hello içinde hello yönergeleri izleyerek [PowerShell aracılığıyla tanılama günlüklerini etkinleştirme](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) makale. Bir komut hello makaleden girmeden önce bilgisinden hello değerlendirin:

- Merhaba değeri toouse hello için belirleyebilirsiniz `-ResourceId` hello komutunu girerek aşağıdaki hello [metin] uygun şekilde değiştirerek parametresi `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`. Merhaba kimliği hello komut çıktısı arar benzer çok*/subscriptions/ [abonelik Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG adı]*.
- Günlük kategori toocollect verileri yalnızca istiyorsanız ekleyin `-Categories [category]` toohello kategori olduğu ya da hello makaledeki hello komutunun sonuna *NetworkSecurityGroupEvent* veya *NetworkSecurityGroupRuleCounter*. Merhaba kullanmazsanız `-Categories` parametresi, veri toplama kategorileri hem günlük için etkinleştirildi.

### <a name="azure-command-line-interface-cli"></a>Azure komut satırı arabirimi (CLI)

toouse CLI tooenable günlük Merhaba, hello hello yönergeleri izleyin [CLI aracılığıyla tanılama günlüklerini etkinleştirme](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) makalesi. Bir komut hello makaleden girmeden önce bilgisinden hello değerlendirin:

- Merhaba değeri toouse hello için belirleyebilirsiniz `-ResourceId` hello komutunu girerek aşağıdaki hello [metin] uygun şekilde değiştirerek parametresi `azure network nsg show [resource-group-name] [nsg-name]`. Merhaba kimliği hello komut çıktısı arar benzer çok*/subscriptions/ [abonelik Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG adı]*.
- Günlük kategori toocollect verileri yalnızca istiyorsanız ekleyin `-Categories [category]` toohello kategori olduğu ya da hello makaledeki hello komutunun sonuna *NetworkSecurityGroupEvent* veya *NetworkSecurityGroupRuleCounter*. Merhaba kullanmazsanız `-Categories` parametresi, veri toplama kategorileri hem günlük için etkinleştirildi.

## <a name="logged-data"></a>Günlüğe kaydedilen veriler

JSON biçimli veriler için her iki günlüklerine yazılır. Her günlük türü için yazılan hello belirli veri bölümleri aşağıdaki hello listelenir:

### <a name="event-log"></a>Olay günlüğü
Bu günlük kuralları uygulanan tooVMs olan ve MAC adresine dayalı hizmet rolü örneklerinin bulut hangi NSG hakkında bilgiler içerir. Örnek veri aşağıdaki hello her olay için günlüğe kaydedilir:

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

### <a name="rule-counter-log"></a>Kural sayacı günlüğü

Bu günlük, her kural tooresources hakkında bilgi içerir. Hello bir kuralın uygulanacağı her zaman en aşağıdaki örnek veriler günlüğe kaydedilir:

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

## <a name="view-and-analyze-logs"></a>Görüntülemek ve günlüklerini analiz edin

toolearn tooview etkinlik oturum nasıl veri okuma hello [hello Azure etkinlik günlüğü'ne genel bakış](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) makalesi. toolearn tooview tanılama günlük nasıl veri okuma hello [genel bakış, Azure tanılama günlükleri](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) makalesi. Tanılama veri tooLog Analytics gönderirseniz, hello kullanabilirsiniz [Azure ağ güvenlik grubu analytics](../log-analytics/log-analytics-azure-networking-analytics.md) Gelişmiş ınsights (Önizleme) yönetimi çözümü. 
