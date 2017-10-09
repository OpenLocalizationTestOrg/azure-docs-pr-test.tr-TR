---
title: "aaaStream hello Azure etkinlik günlüğü tooEvent hub | Microsoft Docs"
description: "Nasıl toostream hello Azure etkinlik günlüğü tooEvent hub'ları hakkında bilgi edinin."
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
ms.openlocfilehash: 336f92771b9d4379ad9dbcadc6997dfae7fae7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-hello-azure-activity-log-tooevent-hubs"></a><span data-ttu-id="38199-103">Hello Azure etkinlik günlüğü tooEvent hub akışı</span><span class="sxs-lookup"><span data-stu-id="38199-103">Stream hello Azure Activity Log tooEvent Hubs</span></span>
<span data-ttu-id="38199-104">Merhaba [ **Azure etkinlik günlüğü** ](monitoring-overview-activity-logs.md) içinde hello Portalı'nda hello yerleşik "Verme" seçeneğini kullanarak gerçek zamanlı tooany uygulama yakın gönderilebilen ya da hizmet veri yolu kural kimliği hello aracılığıyla bir günlük profilinde hello etkinleştirerek Azure PowerShell cmdlet'lerini veya Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="38199-104">hello [**Azure Activity Log**](monitoring-overview-activity-logs.md) can be streamed in near real time tooany application using hello built-in “Export” option in hello portal, or by enabling hello Service Bus Rule Id in a Log Profile via hello Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-hello-activity-log-and-event-hubs"></a><span data-ttu-id="38199-105">Merhaba etkinlik günlüğü ve olay hub'ları ile yapabilecekleriniz</span><span class="sxs-lookup"><span data-stu-id="38199-105">What you can do with hello Activity Log and Event Hubs</span></span>
<span data-ttu-id="38199-106">Merhaba etkinlik günlüğü yeteneği akış hello kullanabilir birkaç yollar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="38199-106">Here are just a few ways you might use hello streaming capability for hello Activity Log:</span></span>

* <span data-ttu-id="38199-107">**Akış toothird taraf günlüğe kaydetme ve telemetri sistemlerde** – zaman içinde olay hub'ları akış hello mekanizması toopipe etkinlik günlüğü üçüncü taraf Sıem'lerden duruma ve oturum analiz çözümleri.</span><span class="sxs-lookup"><span data-stu-id="38199-107">**Stream toothird-party logging and telemetry systems** – Over time, Event Hubs streaming will become hello mechanism toopipe your Activity Log into third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="38199-108">**Bir özel telemetri ve günlüğe kaydetme platformu yapı** – özel olarak geliştirilmiş telemetri platform zaten varsa veya olan hello alma yalnızca biri, yüksek düzeyde ölçeklenebilir hello yayımlama-abone olma yapı hakkında olay hub'ları yapısını tooflexibly verir düşünüyorum Etkinlik günlüğü.</span><span class="sxs-lookup"><span data-stu-id="38199-108">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest hello activity log.</span></span> [<span data-ttu-id="38199-109">Bir küresel ölçekteki telemetri Platform dan Rosanova'nın Kılavuzu toousing Event Hubs bakın.</span><span class="sxs-lookup"><span data-stu-id="38199-109">See Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform here.</span></span>](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-hello-activity-log"></a><span data-ttu-id="38199-110">Merhaba etkinlik günlüğü akışı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="38199-110">Enable streaming of hello Activity Log</span></span>
<span data-ttu-id="38199-111">Etkinlik günlüğü Merhaba program aracılığıyla veya hello Portalı aracılığıyla akış etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38199-111">You can enable streaming of hello Activity Log either programmatically or via hello portal.</span></span> <span data-ttu-id="38199-112">Her iki durumda da, bir hizmet veri yolu Namespace ve bu ad alanı için bir paylaşılan erişim ilkesi seçin ve hello ilk yeni etkinlik günlüğü olay gerçekleştiğinde bir olay hub'ı bu ad alanında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="38199-112">Either way, you pick a Service Bus Namespace and a shared access policy for that namespace, and an Event Hub is created in that namespace when hello first new Activity Log event occurs.</span></span> <span data-ttu-id="38199-113">Bir hizmet veri yolu Namespace yoksa, öncelikle toocreate biri gerekir.</span><span class="sxs-lookup"><span data-stu-id="38199-113">If you do not have a Service Bus Namespace, you first need toocreate one.</span></span> <span data-ttu-id="38199-114">Etkinlik günlüğü olaylarını toothis Service Bus Namespace önceden akışı değilse, daha önce oluşturulmuş bir Event Hub hello yeniden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="38199-114">If you have previously streamed Activity Log events toothis Service Bus Namespace, hello Event Hub that was previously created will be reused.</span></span> <span data-ttu-id="38199-115">Merhaba paylaşılan erişim ilkesi hello akış mekanizması vardır hello izinleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="38199-115">hello shared access policy defines hello permissions that hello streaming mechanism has.</span></span> <span data-ttu-id="38199-116">Günümüzde, tooan olay hub'ları akış gerektirir **Yönet**, **Gönder**, ve **dinleme** izinleri.</span><span class="sxs-lookup"><span data-stu-id="38199-116">Today, streaming tooan Event Hubs requires **Manage**, **Send**, and **Listen** permissions.</span></span> <span data-ttu-id="38199-117">Oluşturun veya hello "Yapılandırma" sekmesi altında hello Klasik Portalı'nda hizmet veri yolu Namespace paylaşılan erişim ilkeleri, hizmet veri yolu Namespace için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="38199-117">You can create or modify Service Bus Namespace shared access policies in hello classic portal under hello “Configure” tab for your Service Bus Namespace.</span></span> <span data-ttu-id="38199-118">tooupdate etkinlik günlüğü günlük profili tooinclude akış Merhaba, hello kullanıcı hello değişiklik yapmadan bu hizmet veri yolu yetkilendirme kuralı hello ListKey izninizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="38199-118">tooupdate hello Activity Log log profile tooinclude streaming, hello user making hello change must have hello ListKey permission on that Service Bus Authorization Rule.</span></span>

<span data-ttu-id="38199-119">Merhaba hizmet veri yolu veya olay hub'ad alanı toobe hello yok uygun RBAC erişim tooboth abonelikleri hello ayarı yapılandıran hello kullanıcının sahip olduğu sürece günlükleri yayma hello abonelik aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="38199-119">hello service bus or event hub namespace does not have toobe in hello same subscription as hello subscription emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

### <a name="via-azure-portal"></a><span data-ttu-id="38199-120">Azure portalı üzerinden</span><span class="sxs-lookup"><span data-stu-id="38199-120">Via Azure portal</span></span>
1. <span data-ttu-id="38199-121">Toohello gidin **etkinlik günlüğü** yan hello portalının sol hello üzerinde hello menüsünü kullanarak dikey.</span><span class="sxs-lookup"><span data-stu-id="38199-121">Navigate toohello **Activity Log** blade using hello menu on hello left side of hello portal.</span></span>
   
    ![TooActivity günlük portalında gidin](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. <span data-ttu-id="38199-123">Merhaba tıklatın **dışarı** hello dikey penceresinde hello üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="38199-123">Click hello **Export** button at hello top of hello blade.</span></span>
   
    ![Portalında Dışarı Aktar](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. <span data-ttu-id="38199-125">Görüntülenen hello dikey penceresinde hello bölgeler için toostream olaylar ve hello Service Bus bu olayları akış için oluşturulan bir olay hub'ı toobe istediğiniz Namespace istediğiniz seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38199-125">In hello blade that appears, you can select hello regions for which you would like toostream events and hello Service Bus Namespace in which you would like an Event Hub toobe created for streaming these events.</span></span>
   
    ![Etkinlik günlüğü dikey dışarı aktarma](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. <span data-ttu-id="38199-127">Tıklatın **kaydetmek** toosave bu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="38199-127">Click **Save** toosave these settings.</span></span> <span data-ttu-id="38199-128">Hello ayarları hemen uygulanan tooyour abonelik olabilir.</span><span class="sxs-lookup"><span data-stu-id="38199-128">hello settings are immediately be applied tooyour subscription.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="38199-129">PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="38199-129">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="38199-130">Bir günlük profili zaten varsa, bu profili ilk tooremove gerekir.</span><span class="sxs-lookup"><span data-stu-id="38199-130">If a log profile already exists, you first need tooremove that profile.</span></span>

1. <span data-ttu-id="38199-131">Kullanım `Get-AzureRmLogProfile` günlük profili varsa, tooidentify</span><span class="sxs-lookup"><span data-stu-id="38199-131">Use `Get-AzureRmLogProfile` tooidentify if a log profile exists</span></span>
2. <span data-ttu-id="38199-132">Aksi takdirde kullanmak `Remove-AzureRmLogProfile` tooremove onu.</span><span class="sxs-lookup"><span data-stu-id="38199-132">If so, use `Remove-AzureRmLogProfile` tooremove it.</span></span>
3. <span data-ttu-id="38199-133">Kullanım `Set-AzureRmLogProfile` toocreate bir profili:</span><span class="sxs-lookup"><span data-stu-id="38199-133">Use `Set-AzureRmLogProfile` toocreate a profile:</span></span>

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

<span data-ttu-id="38199-134">Merhaba Service Bus kural kimliği olduğundan bu biçiminde bir dize: {hizmet veri yolu kaynak kimliği} /authorizationrules/ {anahtar adı}, örneğin</span><span class="sxs-lookup"><span data-stu-id="38199-134">hello Service Bus Rule ID is a string with this format: {service bus resource ID}/authorizationrules/{key name}, for example</span></span> 

### <a name="via-azure-cli"></a><span data-ttu-id="38199-135">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="38199-135">Via Azure CLI</span></span>
<span data-ttu-id="38199-136">Bir günlük profili zaten varsa, bu profili ilk tooremove gerekir.</span><span class="sxs-lookup"><span data-stu-id="38199-136">If a log profile already exists, you first need tooremove that profile.</span></span>

1. <span data-ttu-id="38199-137">Kullanım `azure insights logprofile list` günlük profili varsa, tooidentify</span><span class="sxs-lookup"><span data-stu-id="38199-137">Use `azure insights logprofile list` tooidentify if a log profile exists</span></span>
2. <span data-ttu-id="38199-138">Aksi takdirde kullanmak `azure insights logprofile delete` tooremove onu.</span><span class="sxs-lookup"><span data-stu-id="38199-138">If so, use `azure insights logprofile delete` tooremove it.</span></span>
3. <span data-ttu-id="38199-139">Kullanım `azure insights logprofile add` toocreate bir profili:</span><span class="sxs-lookup"><span data-stu-id="38199-139">Use `azure insights logprofile add` toocreate a profile:</span></span>

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

<span data-ttu-id="38199-140">Merhaba Service Bus kural kimliği olduğundan bu biçiminde bir dize: `{service bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="38199-140">hello Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span></span>

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a><span data-ttu-id="38199-141">Olay hub'ları hello günlük verilerini nasıl kullanabilir?</span><span class="sxs-lookup"><span data-stu-id="38199-141">How do I consume hello log data from Event Hubs?</span></span>
<span data-ttu-id="38199-142">[Merhaba şema hello etkinlik günlüğü için kullanılabilir burada](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="38199-142">[hello schema for hello Activity Log is available here](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="38199-143">Her bir olaydır JSON BLOB'ları "kayıtlar." olarak adlandırılan bir dizi</span><span class="sxs-lookup"><span data-stu-id="38199-143">Each event is in an array of JSON blobs called “records.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="38199-144">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="38199-144">Next Steps</span></span>
* [<span data-ttu-id="38199-145">Arşiv hello etkinlik günlüğü tooa depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="38199-145">Archive hello Activity Log tooa storage account</span></span>](monitoring-archive-activity-log.md)
* [<span data-ttu-id="38199-146">Okuma hello hello Azure etkinlik günlüğü genel bakış</span><span class="sxs-lookup"><span data-stu-id="38199-146">Read hello overview of hello Azure Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="38199-147">Etkinlik günlüğü olaya dayanarak bir uyarı ayarlama</span><span class="sxs-lookup"><span data-stu-id="38199-147">Set up an alert based on an Activity Log event</span></span>](insights-auditlog-to-webhook-email.md)

