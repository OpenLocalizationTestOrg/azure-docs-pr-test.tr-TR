---
title: "Olay hub'ları için Azure etkinlik günlüğü akış | Microsoft Docs"
description: "Olay hub'ları için Azure etkinlik günlüğü akış öğrenin."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ec4c2d2c-8907-484f-a910-712403a06829
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/06/2017
ms.author: johnkem
ms.openlocfilehash: 88c5701279f370914fac68872d67b02a7571748a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="stream-the-azure-activity-log-to-event-hubs"></a><span data-ttu-id="ec61e-103">Akış Event hubs'a Azure etkinlik günlüğü</span><span class="sxs-lookup"><span data-stu-id="ec61e-103">Stream the Azure Activity Log to Event Hubs</span></span>
<span data-ttu-id="ec61e-104">[ **Azure etkinlik günlüğü** ](monitoring-overview-activity-logs.md) portalında veya Azure PowerShell aracılığıyla bir günlük profilinde Service Bus kural kimliği etkinleştirerek yerleşik "Verme" seçeneğini kullanarak herhangi bir uygulama için yakın gerçek zamanlı akış Cmdlet'lerini veya Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ec61e-104">The [**Azure Activity Log**](monitoring-overview-activity-logs.md) can be streamed in near real time to any application using the built-in “Export” option in the portal, or by enabling the Service Bus Rule Id in a Log Profile via the Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-the-activity-log-and-event-hubs"></a><span data-ttu-id="ec61e-105">Etkinlik günlüğü ve olay hub'ları ile yapabilecekleriniz</span><span class="sxs-lookup"><span data-stu-id="ec61e-105">What you can do with the Activity Log and Event Hubs</span></span>
<span data-ttu-id="ec61e-106">Etkinlik günlüğü için akış özelliği kullanabilir birkaç yollar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ec61e-106">Here are just a few ways you might use the streaming capability for the Activity Log:</span></span>

* <span data-ttu-id="ec61e-107">**Üçüncü taraf günlüğe kaydetme ve telemetri sistemlerde akışına** – zaman içinde olay hub'ları akış üçüncü taraf Sıem'lerden etkinlik günlüğü kanal ve analiz çözümleri oturum mekanizması olur.</span><span class="sxs-lookup"><span data-stu-id="ec61e-107">**Stream to third-party logging and telemetry systems** – Over time, Event Hubs streaming will become the mechanism to pipe your Activity Log into third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="ec61e-108">**Özel telemetri ve günlüğe kaydetme platform derleme** – yayımlama-abone yapısı bir özel olarak geliştirilmiş telemetri platform veya olan biri, yüksek düzeyde ölçeklenebilir oluşturma hakkında düşünüyorum yalnızca zaten varsa Event Hubs, esnek etkinlik günlüğü alma olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ec61e-108">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest the activity log.</span></span> [<span data-ttu-id="ec61e-109">Olay hub'ları bir küresel ölçekteki telemetri platform burada kullanmanın Dan Rosanova'nın Kılavuzu'na bakın.</span><span class="sxs-lookup"><span data-stu-id="ec61e-109">See Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform here.</span></span>](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-the-activity-log"></a><span data-ttu-id="ec61e-110">Etkinlik günlüğü akışı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ec61e-110">Enable streaming of the Activity Log</span></span>
<span data-ttu-id="ec61e-111">Etkinlik günlüğü program aracılığıyla veya portal aracılığıyla akış etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec61e-111">You can enable streaming of the Activity Log either programmatically or via the portal.</span></span> <span data-ttu-id="ec61e-112">Her iki durumda da, bir hizmet veri yolu Namespace ve bu ad alanı için bir paylaşılan erişim ilkesi seçin ve ilk yeni etkinlik günlüğü olay gerçekleştiğinde bir olay hub'ı bu ad alanında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ec61e-112">Either way, you pick a Service Bus Namespace and a shared access policy for that namespace, and an Event Hub is created in that namespace when the first new Activity Log event occurs.</span></span> <span data-ttu-id="ec61e-113">Hizmet veri yolu Namespace yoksa, öncelikle bir oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec61e-113">If you do not have a Service Bus Namespace, you first need to create one.</span></span> <span data-ttu-id="ec61e-114">Bu hizmet veri yolu Namespace etkinlik günlüğü olaylarını önceden akışı değilse, daha önce oluşturulmuş olay hub'ı yeniden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ec61e-114">If you have previously streamed Activity Log events to this Service Bus Namespace, the Event Hub that was previously created will be reused.</span></span> <span data-ttu-id="ec61e-115">Paylaşılan Erişim İlkesi akış mekanizmaya sahip izinleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ec61e-115">The shared access policy defines the permissions that the streaming mechanism has.</span></span> <span data-ttu-id="ec61e-116">Günümüzde, bir olay hub'ları için akış gerektirir **Yönet**, **Gönder**, ve **dinleme** izinleri.</span><span class="sxs-lookup"><span data-stu-id="ec61e-116">Today, streaming to an Event Hubs requires **Manage**, **Send**, and **Listen** permissions.</span></span> <span data-ttu-id="ec61e-117">Oluşturun veya "Yapılandırma" sekmesi altında Klasik Portalı'nda hizmet veri yolu Namespace paylaşılan erişim ilkeleri, hizmet veri yolu Namespace için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ec61e-117">You can create or modify Service Bus Namespace shared access policies in the classic portal under the “Configure” tab for your Service Bus Namespace.</span></span> <span data-ttu-id="ec61e-118">Akış dahil etmek için etkinlik günlüğü günlük profilini güncelleştirmek için değişiklik yapmadan kullanıcı bu hizmet veri yolu yetkilendirme kuralı ListKey izni olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ec61e-118">To update the Activity Log log profile to include streaming, the user making the change must have the ListKey permission on that Service Bus Authorization Rule.</span></span>

<span data-ttu-id="ec61e-119">Hizmet veri yolu veya olay hub'ı ad ayarı yapılandıran kullanıcı her iki aboneliğin uygun RBAC erişime sahip olduğu sürece günlükleri yayma abonelik ile aynı abonelikte olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ec61e-119">The service bus or event hub namespace does not have to be in the same subscription as the subscription emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

### <a name="via-azure-portal"></a><span data-ttu-id="ec61e-120">Azure portalı üzerinden</span><span class="sxs-lookup"><span data-stu-id="ec61e-120">Via Azure portal</span></span>
1. <span data-ttu-id="ec61e-121">Gidin **etkinlik günlüğü** portalın sol tarafta menüsünü kullanarak dikey.</span><span class="sxs-lookup"><span data-stu-id="ec61e-121">Navigate to the **Activity Log** blade using the menu on the left side of the portal.</span></span>
   
    ![Etkinlik günlüğü portalında gidin](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. <span data-ttu-id="ec61e-123">Tıklatın **verme** dikey pencerenin üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ec61e-123">Click the **Export** button at the top of the blade.</span></span>
   
    ![Portalında Dışarı Aktar](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. <span data-ttu-id="ec61e-125">Görüntülenen dikey penceresinde, akış olayları ve hizmet veri yolu Namespace bu olayları akış için oluşturulacak bir Event Hub istediğiniz için istediğiniz bölgeleri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec61e-125">In the blade that appears, you can select the regions for which you would like to stream events and the Service Bus Namespace in which you would like an Event Hub to be created for streaming these events.</span></span>
   
    ![Etkinlik günlüğü dikey dışarı aktarma](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. <span data-ttu-id="ec61e-127">Tıklatın **kaydetmek** bu ayarları kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="ec61e-127">Click **Save** to save these settings.</span></span> <span data-ttu-id="ec61e-128">Ayarları olan hemen uygulanması aboneliğinize.</span><span class="sxs-lookup"><span data-stu-id="ec61e-128">The settings are immediately be applied to your subscription.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="ec61e-129">PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="ec61e-129">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="ec61e-130">Bir günlük profili zaten varsa, önce bu profili kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec61e-130">If a log profile already exists, you first need to remove that profile.</span></span>

1. <span data-ttu-id="ec61e-131">Kullanım `Get-AzureRmLogProfile` günlük profili olup olmadığını belirlemek için</span><span class="sxs-lookup"><span data-stu-id="ec61e-131">Use `Get-AzureRmLogProfile` to identify if a log profile exists</span></span>
2. <span data-ttu-id="ec61e-132">Aksi takdirde kullanmak `Remove-AzureRmLogProfile` kaldırmak için.</span><span class="sxs-lookup"><span data-stu-id="ec61e-132">If so, use `Remove-AzureRmLogProfile` to remove it.</span></span>
3. <span data-ttu-id="ec61e-133">Kullanım `Set-AzureRmLogProfile` bir profil oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="ec61e-133">Use `Set-AzureRmLogProfile` to create a profile:</span></span>

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

<span data-ttu-id="ec61e-134">Hizmet veri yolu kural kimliği bu biçiminde bir dizedir: {hizmet veri yolu kaynak kimliği} /authorizationrules/ {anahtar adı}, örneğin</span><span class="sxs-lookup"><span data-stu-id="ec61e-134">The Service Bus Rule ID is a string with this format: {service bus resource ID}/authorizationrules/{key name}, for example</span></span> 

### <a name="via-azure-cli"></a><span data-ttu-id="ec61e-135">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ec61e-135">Via Azure CLI</span></span>
<span data-ttu-id="ec61e-136">Bir günlük profili zaten varsa, önce bu profili kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec61e-136">If a log profile already exists, you first need to remove that profile.</span></span>

1. <span data-ttu-id="ec61e-137">Kullanım `azure insights logprofile list` günlük profili olup olmadığını belirlemek için</span><span class="sxs-lookup"><span data-stu-id="ec61e-137">Use `azure insights logprofile list` to identify if a log profile exists</span></span>
2. <span data-ttu-id="ec61e-138">Aksi takdirde kullanmak `azure insights logprofile delete` kaldırmak için.</span><span class="sxs-lookup"><span data-stu-id="ec61e-138">If so, use `azure insights logprofile delete` to remove it.</span></span>
3. <span data-ttu-id="ec61e-139">Kullanım `azure insights logprofile add` bir profil oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="ec61e-139">Use `azure insights logprofile add` to create a profile:</span></span>

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

<span data-ttu-id="ec61e-140">Hizmet veri yolu kural kimliği bu biçiminde bir dizedir: `{service bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="ec61e-140">The Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span></span>

## <a name="how-do-i-consume-the-log-data-from-event-hubs"></a><span data-ttu-id="ec61e-141">Olay hub'ları günlük verilerini nasıl kullanabilir?</span><span class="sxs-lookup"><span data-stu-id="ec61e-141">How do I consume the log data from Event Hubs?</span></span>
<span data-ttu-id="ec61e-142">[Etkinlik günlüğü için şemayı buraya kullanılabilir](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="ec61e-142">[The schema for the Activity Log is available here](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="ec61e-143">Her bir olaydır JSON BLOB'ları "kayıtlar." olarak adlandırılan bir dizi</span><span class="sxs-lookup"><span data-stu-id="ec61e-143">Each event is in an array of JSON blobs called “records.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec61e-144">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="ec61e-144">Next Steps</span></span>
* [<span data-ttu-id="ec61e-145">Arşiv depolama hesabı etkinlik günlüğü</span><span class="sxs-lookup"><span data-stu-id="ec61e-145">Archive the Activity Log to a storage account</span></span>](monitoring-archive-activity-log.md)
* [<span data-ttu-id="ec61e-146">Azure etkinlik günlüğü bakış okuma</span><span class="sxs-lookup"><span data-stu-id="ec61e-146">Read the overview of the Azure Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="ec61e-147">Etkinlik günlüğü olaya dayanarak bir uyarı ayarlama</span><span class="sxs-lookup"><span data-stu-id="ec61e-147">Set up an alert based on an Activity Log event</span></span>](insights-auditlog-to-webhook-email.md)

