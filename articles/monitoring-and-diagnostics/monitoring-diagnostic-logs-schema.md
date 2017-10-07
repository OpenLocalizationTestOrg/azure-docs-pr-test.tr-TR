---
title: "aaaAzure tanılama günlükleri desteklenen Hizmetleri ve şemaları | Microsoft Docs"
description: "Azure tanılama günlüklerini Hello desteklenen Hizmetleri ve olay şema anlayın."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: a3cbf5267e1bd0dc257f4fb4f42c323644046a6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="supported-services-schemas-and-categories-for-azure-diagnostic-logs"></a>Desteklenen hizmetler, şemalar ve Azure tanılama günlükleri için kategorileri

[Azure kaynak tanılama günlüklerini](monitoring-overview-of-diagnostic-logs.md) olan hello işlemi bu kaynağın açıklayan Azure kaynaklarınızı tarafından gösterilen günlükleri. Kaynak türü bu günlüklerin belirli. Bu makalede, her hizmeti tarafından oluşturulan olaylar için desteklenen Hizmetleri ve olay şema hello kümesi verilmiştir. Bu makalede ayrıca kaynak türüne göre kullanılabilen günlük kategorilerinin tam bir listesini içerir.

## <a name="supported-services-and-schemas-for-resource-diagnostic-logs"></a>Desteklenen kaynak tanılama günlüklerini Hizmetleri ve şemaları
Kaynak tanılama günlükleri için Hello şeması hello kaynak ve günlük kategoriye göre değişir.   

| Hizmet | Şema & belgeleri |
| --- | --- |
| API Management | Şema kullanılamaz. |
| Application Gatewayler |[Uygulama ağ geçidi için tanılama günlükleri](../application-gateway/application-gateway-diagnostics.md) |
| Azure Otomasyonu |[Azure otomasyonu için günlük analizi](../automation/automation-manage-send-joblogs-log-analytics.md) |
| Azure Batch |[Azure Batch Tanılama Günlüğü](../batch/batch-diagnostics.md) |
| Müşteri Öngörüler | Şema kullanılamaz. |
| Content Delivery Network | Şema kullanılamaz. |
| CosmosDB | Şema kullanılamaz. |
| Data Lake Analytics |[Azure Data Lake Analytics’te tanılama günlüklerine erişim](../data-lake-analytics/data-lake-analytics-diagnostic-logs.md) |
| Data Lake Store |[Azure Data Lake Store için tanılama günlüklerine erişme](../data-lake-store/data-lake-store-diagnostic-logs.md) |
| Event Hubs |[Azure Event Hubs tanılama günlükleri](../event-hubs/event-hubs-diagnostic-logs.md) |
| Anahtar Kasası |[Azure Anahtar Kasası Günlüğü](../key-vault/key-vault-logging.md) |
| Yük Dengeleyici |[Azure Load Balancer için Log Analytics](../load-balancer/load-balancer-monitor-log.md) |
| Logic Apps |[Logic Apps B2B özel izleme şeması](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md) |
| Ağ Güvenlik Grupları |[Ağ güvenlik grupları (NSG’ler) için Log Analytics](../virtual-network/virtual-network-nsg-manage-log.md) |
| Kurtarma Hizmetleri | Şema kullanılamaz.|
| Arama |[Etkinleştirme ve arama trafiği Analytics kullanma](../search/search-traffic-analytics.md) |
| Sunucu Yönetimi | Şema kullanılamaz. |
| Service Bus |[Azure Service Bus tanılama günlükleri](../service-bus-messaging/service-bus-diagnostic-logs.md) |
| Akış Analizi |[İş tanılama günlükleri](../stream-analytics/stream-analytics-job-diagnostic-logs.md) |

## <a name="supported-log-categories-per-resource-type"></a>Kaynak türü başına günlük kategoriler desteklenen
|Kaynak Türü|Kategori|Kategori görünen adı|
|---|---|---|
|Microsoft.ApiManagement/service|GatewayLogs|Günlükleri ilgili tooApiManagement ağ geçidi|
|Microsoft.Automation/automationAccounts|JobLogs|İş günlükleri|
|Microsoft.Automation/automationAccounts|JobStreams|İş akışları|
|Microsoft.Automation/automationAccounts|DscNodeStatus|DSC düğüm durumu|
|Microsoft.Batch/batchAccounts|ServiceLog|Hizmet Günlükleri|
|Microsoft.Cdn/profiles/endpoints|CoreAnalytics|Merhaba ölçümlerini hello uç noktası, örneğin, bant genişliği, çıkış, vb. alır.|
|Microsoft.CustomerInsights/hubs|AuditEvents|AuditEvents|
|Microsoft.DataLakeAnalytics/accounts|Denetim|Denetim Günlükleri|
|Microsoft.DataLakeAnalytics/accounts|İstekler|İstek günlükleri|
|Microsoft.DataLakeStore/accounts|Denetim|Denetim Günlükleri|
|Microsoft.DataLakeStore/accounts|İstekler|İstek günlükleri|
|Microsoft.DocumentDB/databaseAccounts|DataPlaneRequests|DataPlaneRequests|
|Microsoft.EventHub/namespaces|ArchiveLogs|Arşiv günlükleri|
|Microsoft.EventHub/namespaces|OperationalLogs|İşlem günlükleri|
|Microsoft.EventHub/namespaces|AutoScaleLogs|Otomatik ölçek günlükleri|
|Microsoft.KeyVault/vaults|AuditEvent|Denetim Günlükleri|
|Microsoft.Logic/workflows|İş akışı WorkflowRuntime|İş akışı çalışma zamanı Tanılama Olayları|
|Microsoft.Logic/integrationAccounts|IntegrationAccountTrackingEvents|Tümleştirme hesap izleme olayları|
|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupEvent|Ağ güvenlik grubu olayı|
|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupRuleCounter|Ağ güvenlik grubu kural sayacı|
|Microsoft.Network/loadBalancers|LoadBalancerAlertEvent|Yük Dengeleyici uyarı olayları|
|Microsoft.Network/loadBalancers|LoadBalancerProbeHealthStatus|Yük Dengeleyici araştırması sistem durumu|
|Microsoft.Network/applicationGateways|ApplicationGatewayAccessLog|Uygulama ağ geçidi erişim günlüğü|
|Microsoft.Network/applicationGateways|ApplicationGatewayPerformanceLog|Uygulama ağ geçidi performans günlüğü|
|Microsoft.Network/applicationGateways|ApplicationGatewayFirewallLog|Uygulama ağ geçidi güvenlik duvarı günlüğü|
|Microsoft.RecoveryServices/Vaults|AzureBackupReport|Raporlama verilerini azure yedekleme|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryJobs|Azure Site Recovery işleri|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryEvents|Azure Site kurtarma olayları|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryReplicatedItems|Azure Site Recovery çoğaltılan öğeler|
|Microsoft.Search/searchServices|OperationLogs|İşlem günlükleri|
|Microsoft.ServiceBus/namespaces|OperationalLogs|İşlem günlükleri|
|Microsoft.StreamAnalytics/streamingjobs|Yürütme|Yürütme|
|Microsoft.StreamAnalytics/streamingjobs|Yazma|Yazma|

## <a name="next-steps"></a>Sonraki Adımlar

* [Tanılama günlükleri hakkında daha fazla bilgi edinin](monitoring-overview-of-diagnostic-logs.md)
* [Kaynağın tanılama günlükleri çok akış**olay hub'ları**](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Hello Azure İzleyici REST API'sini kullanarak kaynak tanılama ayarlarını değiştirme](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [Günlük analizi ile Azure depolama biriminden günlüklerini analiz edin](../log-analytics/log-analytics-azure-storage.md)
