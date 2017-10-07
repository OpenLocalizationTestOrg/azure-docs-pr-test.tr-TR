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
# <a name="migrate-azure-alerts-on-management-events-tooactivity-log-alerts"></a><span data-ttu-id="c9b6a-104">Azure Uyarıları Yönetimi olayları tooActivity günlük uyarılar hakkında geçirme</span><span class="sxs-lookup"><span data-stu-id="c9b6a-104">Migrate Azure alerts on management events tooActivity Log alerts</span></span>


> [!WARNING]
> <span data-ttu-id="c9b6a-105">Yönetim olaylarını uyarılar veya ondan sonra Ekim 1 kapatılır.</span><span class="sxs-lookup"><span data-stu-id="c9b6a-105">Alerts on management events will be turned off on or after October 1.</span></span> <span data-ttu-id="c9b6a-106">Bu uyarılar varsa ve bu durumda geçiş toounderstand aşağıda hello yönergeleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="c9b6a-106">Use hello directions below toounderstand if you have these alerts and migrate them if so.</span></span>
>
> 

## <a name="what-is-changing"></a><span data-ttu-id="c9b6a-107">Ne değiştirme</span><span class="sxs-lookup"><span data-stu-id="c9b6a-107">What is changing</span></span>

<span data-ttu-id="c9b6a-108">Azure İzleyicisi'ni (önceki adıyla Azure Öngörüler) yeteneği toocreate dışına Yönetimi olayları tetiklenir ve bildirimleri, tooa Web kancası URL'si veya e-posta adresleri oluşturulan bir uyarı sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="c9b6a-108">Azure Monitor (formerly Azure Insights) offered a capability toocreate an alert that triggered off of management events and generated notifications tooa webhook URL or email addresses.</span></span> <span data-ttu-id="c9b6a-109">Oluşturmuş olabileceğiniz bunlardan birini uyarıları şu yollardan biriyle:</span><span class="sxs-lookup"><span data-stu-id="c9b6a-109">You may have created one of these alerts any of these ways:</span></span>
* <span data-ttu-id="c9b6a-110">Hello bazı kaynak türleri için Azure portalı, bölümünde İzleme -> Uyarılar -> Ekle "Uyarı" olarak ayarlandığı çok uyarı, "Olayları"</span><span class="sxs-lookup"><span data-stu-id="c9b6a-110">In hello Azure portal for certain resource types, under Monitoring -> Alerts -> Add Alert, where “Alert on” is set too“Events”</span></span>
* <span data-ttu-id="c9b6a-111">Çalışan hello Ekle-AzureRmLogAlertRule PowerShell cmdlet tarafından</span><span class="sxs-lookup"><span data-stu-id="c9b6a-111">By running hello Add-AzureRmLogAlertRule PowerShell cmdlet</span></span>
* <span data-ttu-id="c9b6a-112">Doğrudan kullanarak [uyarı REST API Merhaba](http://docs.microsoft.com/rest/api/monitor/alertrules) "ManagementEventRuleCondition" ve dataSource.odata.type ile odata.type = "RuleManagementEventDataSource" =</span><span class="sxs-lookup"><span data-stu-id="c9b6a-112">By directly using [hello alert REST API](http://docs.microsoft.com/rest/api/monitor/alertrules) with odata.type = “ManagementEventRuleCondition” and dataSource.odata.type = “RuleManagementEventDataSource”</span></span>
 
<span data-ttu-id="c9b6a-113">Merhaba aşağıdaki PowerShell betiğini tüm uyarıların bir listesi, abonelik, aynı zamanda her uyarıdaki hello koşullara sahip Yönetimi olayları döndürür.</span><span class="sxs-lookup"><span data-stu-id="c9b6a-113">hello following PowerShell script returns a list of all alerts on management events that you have in your subscription, as well as hello conditions set on each alert.</span></span>

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

<span data-ttu-id="c9b6a-114">Hiçbir uyarı yönetim olaylarına varsa, hello PowerShell cmdlet'i yukarıdaki uyarı iletilerini bunun gibi bir dizi çıktı:</span><span class="sxs-lookup"><span data-stu-id="c9b6a-114">If you have no alerts on management events, hello PowerShell cmdlet above will output a series of warning messages like this one:</span></span>

`WARNING: hello output of this cmdlet will be flattened, i.e. elimination of hello properties field, in a future release tooimprove hello user experience.`

<span data-ttu-id="c9b6a-115">Bu uyarı iletilerini göz ardı edilebilir.</span><span class="sxs-lookup"><span data-stu-id="c9b6a-115">These warning messages can be ignored.</span></span> <span data-ttu-id="c9b6a-116">Yönetim olaylarına uyarıları varsa, bu PowerShell cmdlet'ini hello çıktısı şuna benzeyecektir:</span><span class="sxs-lookup"><span data-stu-id="c9b6a-116">If you do have alerts on management events, hello output of this PowerShell cmdlet will look like this:</span></span>

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

<span data-ttu-id="c9b6a-117">Her uyarı kesikli çizgi ile ayrılır ve hello kaynak Kimliğini hello uyarı ve izlenen hello belirli kural ayrıntıları içerir.</span><span class="sxs-lookup"><span data-stu-id="c9b6a-117">Each alert is separated by a dashed line and details include hello resource ID of hello alert and hello specific rule being monitored.</span></span>

<span data-ttu-id="c9b6a-118">Bu işlev çok geçti[Azure etkinlik günlüğü uyarıları izleme](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="c9b6a-118">This functionality has been transitioned too[Azure Monitor Activity Log Alerts](monitoring-activity-log-alerts.md).</span></span> <span data-ttu-id="c9b6a-119">Bu yeni uyarılar tooset etkinlik günlüğü olaylarını bir koşula etkinleştirin ve yeni bir olay hello koşul eşleştiğinde bir bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="c9b6a-119">These new alerts enable you tooset a condition on Activity Log events and receive a notification when a new event matches hello condition.</span></span> <span data-ttu-id="c9b6a-120">Bunlar ayrıca Yönetim olaylarına uyarılardan çeşitli iyileştirmeler sağlar:</span><span class="sxs-lookup"><span data-stu-id="c9b6a-120">They also offer several improvements from alerts on management events:</span></span>
* <span data-ttu-id="c9b6a-121">Grubunuzun bildirim alıcıların ("eylem") kullanarak çok sayıda uyarı yeniden [Eylem grupları](monitoring-action-groups.md), bir uyarı alması gereken değiştirme hello karmaşıklığını azaltır.</span><span class="sxs-lookup"><span data-stu-id="c9b6a-121">You can reuse your group of notification recipients (“actions”) across many alerts using [Action Groups](monitoring-action-groups.md), reducing hello complexity of changing who should receive an alert.</span></span>
* <span data-ttu-id="c9b6a-122">Doğrudan eylem gruplarıyla SMS kullanarak telefonunuza bir bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="c9b6a-122">You can receive a notification directly on your phone using SMS with Action Groups.</span></span>
* <span data-ttu-id="c9b6a-123">Yapabilecekleriniz [Resource Manager şablonları ile etkinlik günlüğü uyarıları oluşturma](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="c9b6a-123">You can [create Activity Log Alerts with Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
* <span data-ttu-id="c9b6a-124">Daha fazla esneklik ve karmaşıklık toomeet ile kendi özel gereksinimlerinize göre koşullar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9b6a-124">You can create conditions with greater flexibility and complexity toomeet your specific needs.</span></span>
* <span data-ttu-id="c9b6a-125">Bildirimleri daha hızlı bir şekilde teslim edilir.</span><span class="sxs-lookup"><span data-stu-id="c9b6a-125">Notifications are delivered more quickly.</span></span>
 
## <a name="how-toomigrate"></a><span data-ttu-id="c9b6a-126">Nasıl toomigrate</span><span class="sxs-lookup"><span data-stu-id="c9b6a-126">How toomigrate</span></span>
 
<span data-ttu-id="c9b6a-127">Yeni Etkinlik günlüğü uyarısı toocreate, şunlardan birini yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c9b6a-127">toocreate a new Activity Log Alert, you can either:</span></span>
* <span data-ttu-id="c9b6a-128">İzleyin [nasıl toocreate uyarıda bir hello Azure portalı üzerinde kılavuzumuzu](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="c9b6a-128">Follow [our guide on how toocreate an alert in hello Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="c9b6a-129">Nasıl çok öğrenin[Resource Manager şablonu kullanarak bir uyarı oluşturabilir.](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="c9b6a-129">Learn how too[create an alert using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
 
<span data-ttu-id="c9b6a-130">Daha önce oluşturduğunuz yönetim olaylarını uyarılar otomatik olarak geçirilen tooActivity günlük uyarıları olmaz.</span><span class="sxs-lookup"><span data-stu-id="c9b6a-130">Alerts on management events that you have previously created will not be automatically migrated tooActivity Log Alerts.</span></span> <span data-ttu-id="c9b6a-131">Şu anda yapılandırdıysanız ve el ile etkinlik günlüğü uyarıları olarak yeniden oluşturmanız yönetim olaylarına PowerShell komut dosyası toolist hello uyarıları önceki toouse hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9b6a-131">You need toouse hello preceding PowerShell script toolist hello alerts on management events that you currently have configured and manually recreate them as Activity Log Alerts.</span></span> <span data-ttu-id="c9b6a-132">Bu uyarılar yönetim olayları artık Azure aboneliğinizde görünür olacak Ekim 1 önce yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c9b6a-132">This must be done before October 1, after which alerts on management events will no longer be visible in your Azure subscription.</span></span> <span data-ttu-id="c9b6a-133">Azure uyarıları, Azure İzleyici ölçüm uyarıları, Application Insights uyarıları ve günlük analizi uyarılar dahil olmak üzere diğer türleri, bu değişiklikten etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="c9b6a-133">Other types of Azure alerts, including Azure Monitor metric alerts, Application Insights alerts, and Log Analytics alerts are unaffected by this change.</span></span> <span data-ttu-id="c9b6a-134">Herhangi bir sorunuz varsa, aşağıdaki hello yorumları gönderin.</span><span class="sxs-lookup"><span data-stu-id="c9b6a-134">If you have any questions, post in hello comments below.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c9b6a-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c9b6a-135">Next steps</span></span>

* <span data-ttu-id="c9b6a-136">Daha fazla bilgi edinmek [etkinlik günlüğü](monitoring-overview-activity-logs.md)</span><span class="sxs-lookup"><span data-stu-id="c9b6a-136">Learn more about [Activity Log](monitoring-overview-activity-logs.md)</span></span>
* <span data-ttu-id="c9b6a-137">Yapılandırma [Azure Portalı aracılığıyla etkinlik günlüğü uyarıları](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="c9b6a-137">Configure [Activity Log Alerts via Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="c9b6a-138">Yapılandırma [etkinlik günlüğü uyarıları aracılığıyla kaynak yöneticisi](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="c9b6a-138">Configure [Activity Log Alerts via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
* <span data-ttu-id="c9b6a-139">Gözden geçirme hello [etkinlik günlüğü uyarı Web kancası şeması](monitoring-activity-log-alerts-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="c9b6a-139">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)</span></span>
* <span data-ttu-id="c9b6a-140">Daha fazla bilgi edinmek [hizmet bildirimleri](monitoring-service-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="c9b6a-140">Learn more about [Service Notifications](monitoring-service-notifications.md)</span></span>
* <span data-ttu-id="c9b6a-141">Daha fazla bilgi edinmek [Eylem grupları](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="c9b6a-141">Learn more about [Action Groups](monitoring-action-groups.md)</span></span>
