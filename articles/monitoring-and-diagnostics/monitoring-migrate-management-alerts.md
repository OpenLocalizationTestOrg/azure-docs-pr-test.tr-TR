---
title: "Yönetim olaylarını tooActivity günlük uyarıları üzerinde Azure uyarıları aaaMigrate | Microsoft Docs"
description: "Uyarılar yönetim olaylarına 1 Ekim kaldırılır. Geçirme kullanılamamasıdır uyarıları ile hazırlayın."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: johnkem
ms.openlocfilehash: e00bc4f0bad4e8f97443310770c333d250e343ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-alerts-on-management-events-tooactivity-log-alerts"></a>Azure Uyarıları Yönetimi olayları tooActivity günlük uyarılar hakkında geçirme


> [!WARNING]
> Yönetim olaylarını uyarılar veya ondan sonra Ekim 1 kapatılır. Bu uyarılar varsa ve bu durumda geçiş toounderstand aşağıda hello yönergeleri kullanın.
>
> 

## <a name="what-is-changing"></a>Ne değiştirme

Azure İzleyicisi'ni (önceki adıyla Azure Öngörüler) yeteneği toocreate dışına Yönetimi olayları tetiklenir ve bildirimleri, tooa Web kancası URL'si veya e-posta adresleri oluşturulan bir uyarı sunmuştur. Oluşturmuş olabileceğiniz bunlardan birini uyarıları şu yollardan biriyle:
* Hello bazı kaynak türleri için Azure portalı, bölümünde İzleme -> Uyarılar -> Ekle "Uyarı" olarak ayarlandığı çok uyarı, "Olayları"
* Çalışan hello Ekle-AzureRmLogAlertRule PowerShell cmdlet tarafından
* Doğrudan kullanarak [uyarı REST API Merhaba](http://docs.microsoft.com/rest/api/monitor/alertrules) "ManagementEventRuleCondition" ve dataSource.odata.type ile odata.type = "RuleManagementEventDataSource" =
 
Merhaba aşağıdaki PowerShell betiğini tüm uyarıların bir listesi, abonelik, aynı zamanda her uyarıdaki hello koşullara sahip Yönetimi olayları döndürür.

```powershell
Login-AzureRmAccount
$alerts = $null
foreach ($rg in Get-AzureRmResourceGroup ) {
  $alerts += Get-AzureRmAlertRule -ResourceGroup $rg.ResourceGroupName
}
foreach ($alert in $alerts) {
  if($alert.Properties.Condition.DataSource.GetType().Name.Equals("RuleManagementEventDataSource")) {
    "Alert Name: " + $alert.Name
    "Alert Resource ID: " + $alert.Id
    "Alert conditions:"
    $alert.Properties.Condition.DataSource
    "---------------------------------"
  }
} 
```

Hiçbir uyarı yönetim olaylarına varsa, hello PowerShell cmdlet'i yukarıdaki uyarı iletilerini bunun gibi bir dizi çıktı:

`WARNING: hello output of this cmdlet will be flattened, i.e. elimination of hello properties field, in a future release tooimprove hello user experience.`

Bu uyarı iletilerini göz ardı edilebilir. Yönetim olaylarına uyarıları varsa, bu PowerShell cmdlet'ini hello çıktısı şuna benzeyecektir:

```
Alert Name: webhookEvent1
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/webhookEvent1
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : microsoft.web/sites/start/action
ResourceGroupName    : 
ResourceProviderName : 
Status               : succeeded
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Web/sites/samplealertapp

---------------------------------
Alert Name: someclilogalert
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/someclilogalert
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : Start
ResourceGroupName    : 
ResourceProviderName : 
Status               : 
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Compute/virtualMachines/Seaofclouds

---------------------------------
```

Her uyarı kesikli çizgi ile ayrılır ve hello kaynak Kimliğini hello uyarı ve izlenen hello belirli kural ayrıntıları içerir.

Bu işlev çok geçti[Azure etkinlik günlüğü uyarıları izleme](monitoring-activity-log-alerts.md). Bu yeni uyarılar tooset etkinlik günlüğü olaylarını bir koşula etkinleştirin ve yeni bir olay hello koşul eşleştiğinde bir bildirim alırsınız. Bunlar ayrıca Yönetim olaylarına uyarılardan çeşitli iyileştirmeler sağlar:
* Grubunuzun bildirim alıcıların ("eylem") kullanarak çok sayıda uyarı yeniden [Eylem grupları](monitoring-action-groups.md), bir uyarı alması gereken değiştirme hello karmaşıklığını azaltır.
* Doğrudan eylem gruplarıyla SMS kullanarak telefonunuza bir bildirim alırsınız.
* Yapabilecekleriniz [Resource Manager şablonları ile etkinlik günlüğü uyarıları oluşturma](monitoring-create-activity-log-alerts-with-resource-manager-template.md).
* Daha fazla esneklik ve karmaşıklık toomeet ile kendi özel gereksinimlerinize göre koşullar oluşturabilirsiniz.
* Bildirimleri daha hızlı bir şekilde teslim edilir.
 
## <a name="how-toomigrate"></a>Nasıl toomigrate
 
Yeni Etkinlik günlüğü uyarısı toocreate, şunlardan birini yapabilirsiniz:
* İzleyin [nasıl toocreate uyarıda bir hello Azure portalı üzerinde kılavuzumuzu](monitoring-activity-log-alerts.md)
* Nasıl çok öğrenin[Resource Manager şablonu kullanarak bir uyarı oluşturabilir.](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
 
Daha önce oluşturduğunuz yönetim olaylarını uyarılar otomatik olarak geçirilen tooActivity günlük uyarıları olmaz. Şu anda yapılandırdıysanız ve el ile etkinlik günlüğü uyarıları olarak yeniden oluşturmanız yönetim olaylarına PowerShell komut dosyası toolist hello uyarıları önceki toouse hello gerekir. Bu uyarılar yönetim olayları artık Azure aboneliğinizde görünür olacak Ekim 1 önce yapılmalıdır. Azure uyarıları, Azure İzleyici ölçüm uyarıları, Application Insights uyarıları ve günlük analizi uyarılar dahil olmak üzere diğer türleri, bu değişiklikten etkilenmez. Herhangi bir sorunuz varsa, aşağıdaki hello yorumları gönderin.


## <a name="next-steps"></a>Sonraki adımlar

* Daha fazla bilgi edinmek [etkinlik günlüğü](monitoring-overview-activity-logs.md)
* Yapılandırma [Azure Portalı aracılığıyla etkinlik günlüğü uyarıları](monitoring-activity-log-alerts.md)
* Yapılandırma [etkinlik günlüğü uyarıları aracılığıyla kaynak yöneticisi](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
* Gözden geçirme hello [etkinlik günlüğü uyarı Web kancası şeması](monitoring-activity-log-alerts-webhook.md)
* Daha fazla bilgi edinmek [hizmet bildirimleri](monitoring-service-notifications.md)
* Daha fazla bilgi edinmek [Eylem grupları](monitoring-action-groups.md)
