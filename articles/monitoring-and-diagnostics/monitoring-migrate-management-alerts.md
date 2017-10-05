---
title: "Etkinlik günlüğü Uyarıları Yönetimi olayları Azure uyarılar geçirme | Microsoft Docs"
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
ms.openlocfilehash: 08a457029d3721f5c38dbcd2d2aab7d09a241d8f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="migrate-azure-alerts-on-management-events-to-activity-log-alerts"></a><span data-ttu-id="a70f1-104">Etkinlik günlüğü Uyarıları Yönetimi olayları Azure uyarılar geçirme</span><span class="sxs-lookup"><span data-stu-id="a70f1-104">Migrate Azure alerts on management events to Activity Log alerts</span></span>


> [!WARNING]
> <span data-ttu-id="a70f1-105">Yönetim olaylarını uyarılar veya ondan sonra Ekim 1 kapatılır.</span><span class="sxs-lookup"><span data-stu-id="a70f1-105">Alerts on management events will be turned off on or after October 1.</span></span> <span data-ttu-id="a70f1-106">Bu uyarılar ve öyleyse geçirmek anlamak için aşağıdaki yönergeleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="a70f1-106">Use the directions below to understand if you have these alerts and migrate them if so.</span></span>
>
> 

## <a name="what-is-changing"></a><span data-ttu-id="a70f1-107">Ne değiştirme</span><span class="sxs-lookup"><span data-stu-id="a70f1-107">What is changing</span></span>

<span data-ttu-id="a70f1-108">Azure İzleyicisi'ni (önceki adıyla Azure Öngörüler) Yönetimi olayları dışına tetiklenir ve bir Web kancası URL'si veya e-posta adreslerine bildirim oluşturulan bir uyarı oluşturmak için bir özellik sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="a70f1-108">Azure Monitor (formerly Azure Insights) offered a capability to create an alert that triggered off of management events and generated notifications to a webhook URL or email addresses.</span></span> <span data-ttu-id="a70f1-109">Oluşturmuş olabileceğiniz bunlardan birini uyarıları şu yollardan biriyle:</span><span class="sxs-lookup"><span data-stu-id="a70f1-109">You may have created one of these alerts any of these ways:</span></span>
* <span data-ttu-id="a70f1-110">Belirli kaynak türlerine yönelik Azure portalında bölümünde İzleme -> Uyarılar -> Ekle "Uyarı" olarak ayarlandığı "Olayları" Uyarısı,</span><span class="sxs-lookup"><span data-stu-id="a70f1-110">In the Azure portal for certain resource types, under Monitoring -> Alerts -> Add Alert, where “Alert on” is set to “Events”</span></span>
* <span data-ttu-id="a70f1-111">Add-AzureRmLogAlertRule PowerShell cmdlet'ini çalıştırarak</span><span class="sxs-lookup"><span data-stu-id="a70f1-111">By running the Add-AzureRmLogAlertRule PowerShell cmdlet</span></span>
* <span data-ttu-id="a70f1-112">Doğrudan kullanarak [uyarı REST API](http://docs.microsoft.com/rest/api/monitor/alertrules) ile odata.type = "ManagementEventRuleCondition" ve dataSource.odata.type "RuleManagementEventDataSource" =</span><span class="sxs-lookup"><span data-stu-id="a70f1-112">By directly using [the alert REST API](http://docs.microsoft.com/rest/api/monitor/alertrules) with odata.type = “ManagementEventRuleCondition” and dataSource.odata.type = “RuleManagementEventDataSource”</span></span>
 
<span data-ttu-id="a70f1-113">Aşağıdaki PowerShell betiğini her uyarıdaki ayarlanan koşulları yanı sıra, aboneliğiniz olan Yönetim olayları tüm uyarıların bir listesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="a70f1-113">The following PowerShell script returns a list of all alerts on management events that you have in your subscription, as well as the conditions set on each alert.</span></span>

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

<span data-ttu-id="a70f1-114">Yönetim olaylarına herhangi bir uyarı varsa PowerShell cmdlet'i yukarıdaki uyarı iletilerini bunun gibi bir dizi çıktı:</span><span class="sxs-lookup"><span data-stu-id="a70f1-114">If you have no alerts on management events, the PowerShell cmdlet above will output a series of warning messages like this one:</span></span>

`WARNING: The output of this cmdlet will be flattened, i.e. elimination of the properties field, in a future release to improve the user experience.`

<span data-ttu-id="a70f1-115">Bu uyarı iletilerini göz ardı edilebilir.</span><span class="sxs-lookup"><span data-stu-id="a70f1-115">These warning messages can be ignored.</span></span> <span data-ttu-id="a70f1-116">Yönetim olaylarına uyarıları varsa, bu PowerShell cmdlet'ini çıktısı şuna benzeyecektir:</span><span class="sxs-lookup"><span data-stu-id="a70f1-116">If you do have alerts on management events, the output of this PowerShell cmdlet will look like this:</span></span>

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

<span data-ttu-id="a70f1-117">Her uyarı kesikli çizgi ile ayrılır ve ayrıntıları uyarı ve izlenmekte olan belirli kuralın kaynak Kimliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="a70f1-117">Each alert is separated by a dashed line and details include the resource ID of the alert and the specific rule being monitored.</span></span>

<span data-ttu-id="a70f1-118">Bu işlev için geçişi [Azure etkinlik günlüğü uyarıları izleme](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="a70f1-118">This functionality has been transitioned to [Azure Monitor Activity Log Alerts](monitoring-activity-log-alerts.md).</span></span> <span data-ttu-id="a70f1-119">Bu yeni uyarılar, etkinlik günlüğü olaylarını bir koşul ayarlamaya ve yeni bir olay koşul eşleştiğinde bir bildirim almak etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a70f1-119">These new alerts enable you to set a condition on Activity Log events and receive a notification when a new event matches the condition.</span></span> <span data-ttu-id="a70f1-120">Bunlar ayrıca Yönetim olaylarına uyarılardan çeşitli iyileştirmeler sağlar:</span><span class="sxs-lookup"><span data-stu-id="a70f1-120">They also offer several improvements from alerts on management events:</span></span>
* <span data-ttu-id="a70f1-121">Grubunuzun bildirim alıcıların ("eylem") kullanarak çok sayıda uyarı yeniden [Eylem grupları](monitoring-action-groups.md), bir uyarı alması gereken değiştirme karmaşıklığını azaltır.</span><span class="sxs-lookup"><span data-stu-id="a70f1-121">You can reuse your group of notification recipients (“actions”) across many alerts using [Action Groups](monitoring-action-groups.md), reducing the complexity of changing who should receive an alert.</span></span>
* <span data-ttu-id="a70f1-122">Doğrudan eylem gruplarıyla SMS kullanarak telefonunuza bir bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="a70f1-122">You can receive a notification directly on your phone using SMS with Action Groups.</span></span>
* <span data-ttu-id="a70f1-123">Yapabilecekleriniz [Resource Manager şablonları ile etkinlik günlüğü uyarıları oluşturma](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="a70f1-123">You can [create Activity Log Alerts with Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
* <span data-ttu-id="a70f1-124">Daha fazla esneklik ve belirli ihtiyaçlarınızı karşılaması için karmaşıklık koşullar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a70f1-124">You can create conditions with greater flexibility and complexity to meet your specific needs.</span></span>
* <span data-ttu-id="a70f1-125">Bildirimleri daha hızlı bir şekilde teslim edilir.</span><span class="sxs-lookup"><span data-stu-id="a70f1-125">Notifications are delivered more quickly.</span></span>
 
## <a name="how-to-migrate"></a><span data-ttu-id="a70f1-126">Geçirme</span><span class="sxs-lookup"><span data-stu-id="a70f1-126">How to migrate</span></span>
 
<span data-ttu-id="a70f1-127">Yeni Etkinlik günlüğü uyarısı oluşturmak için şunlardan birini yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a70f1-127">To create a new Activity Log Alert, you can either:</span></span>
* <span data-ttu-id="a70f1-128">İzleyin [kılavuzumuzu Azure portalında bir uyarı oluşturma hakkında](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="a70f1-128">Follow [our guide on how to create an alert in the Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="a70f1-129">Bilgi edinmek için nasıl [Resource Manager şablonu kullanarak bir uyarı oluşturabilir.](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="a70f1-129">Learn how to [create an alert using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
 
<span data-ttu-id="a70f1-130">Daha önce oluşturduğunuz yönetim olaylarını uyarılar, etkinlik günlüğü uyarıları otomatik olarak geçirilmez.</span><span class="sxs-lookup"><span data-stu-id="a70f1-130">Alerts on management events that you have previously created will not be automatically migrated to Activity Log Alerts.</span></span> <span data-ttu-id="a70f1-131">Şu anda yapılandırdıysanız ve el ile etkinlik günlüğü uyarıları olarak yeniden oluşturmanız Yönetimi olayları uyarılar listelemek için yukarıdaki PowerShell komut dosyasını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a70f1-131">You need to use the preceding PowerShell script to list the alerts on management events that you currently have configured and manually recreate them as Activity Log Alerts.</span></span> <span data-ttu-id="a70f1-132">Bu uyarılar yönetim olayları artık Azure aboneliğinizde görünür olacak Ekim 1 önce yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a70f1-132">This must be done before October 1, after which alerts on management events will no longer be visible in your Azure subscription.</span></span> <span data-ttu-id="a70f1-133">Azure uyarıları, Azure İzleyici ölçüm uyarıları, Application Insights uyarıları ve günlük analizi uyarılar dahil olmak üzere diğer türleri, bu değişiklikten etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="a70f1-133">Other types of Azure alerts, including Azure Monitor metric alerts, Application Insights alerts, and Log Analytics alerts are unaffected by this change.</span></span> <span data-ttu-id="a70f1-134">Herhangi bir sorunuz varsa, aşağıdaki yorumları gönderin.</span><span class="sxs-lookup"><span data-stu-id="a70f1-134">If you have any questions, post in the comments below.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a70f1-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a70f1-135">Next steps</span></span>

* <span data-ttu-id="a70f1-136">Daha fazla bilgi edinmek [etkinlik günlüğü](monitoring-overview-activity-logs.md)</span><span class="sxs-lookup"><span data-stu-id="a70f1-136">Learn more about [Activity Log](monitoring-overview-activity-logs.md)</span></span>
* <span data-ttu-id="a70f1-137">Yapılandırma [Azure Portalı aracılığıyla etkinlik günlüğü uyarıları](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="a70f1-137">Configure [Activity Log Alerts via Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="a70f1-138">Yapılandırma [etkinlik günlüğü uyarıları aracılığıyla kaynak yöneticisi](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="a70f1-138">Configure [Activity Log Alerts via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
* <span data-ttu-id="a70f1-139">Gözden geçirme [etkinlik günlüğü uyarı Web kancası şeması](monitoring-activity-log-alerts-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="a70f1-139">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)</span></span>
* <span data-ttu-id="a70f1-140">Daha fazla bilgi edinmek [hizmet bildirimleri](monitoring-service-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="a70f1-140">Learn more about [Service Notifications](monitoring-service-notifications.md)</span></span>
* <span data-ttu-id="a70f1-141">Daha fazla bilgi edinmek [Eylem grupları](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="a70f1-141">Learn more about [Action Groups](monitoring-action-groups.md)</span></span>
