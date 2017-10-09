---
title: "aaaAzure Service Bus tanılama günlüklerini | Microsoft Docs"
description: "Bilgi nasıl tooset azure'da hizmet veri yolu için tanılama günlüklerini ayarlama."
keywords: 
documentationcenter: .net
services: service-bus-messaging
author: banisadr
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: babanisa;sethm
ms.openlocfilehash: e48d6eaba6e865ae39f5b07ed6cd53d74c92e2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-diagnostic-logs"></a><span data-ttu-id="01748-103">Hizmet veri yolu tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="01748-103">Service Bus diagnostic logs</span></span>

<span data-ttu-id="01748-104">Azure hizmet veri yolu için iki tür günlükleri görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="01748-104">You can view two types of logs for Azure Service Bus:</span></span>
* <span data-ttu-id="01748-105">**[Etkinlik günlükleri](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="01748-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="01748-106">Bu günlükler bir iş üzerinde gerçekleştirilen işlemler hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="01748-106">These logs contain information about operations performed on a job.</span></span> <span data-ttu-id="01748-107">Merhaba günlükleri her zaman etkindir.</span><span class="sxs-lookup"><span data-stu-id="01748-107">hello logs are always enabled.</span></span>
* <span data-ttu-id="01748-108">**[Tanılama günlüklerini](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="01748-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="01748-109">İçinde bir işi olur daha zengin hakkında bilgi için tanılama günlüklerini yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01748-109">You can configure diagnostic logs for richer information about everything that happens within a job.</span></span> <span data-ttu-id="01748-110">Tanılama güncelleştirmeleri ve hello iş çalışırken oluşan etkinlikler dahil olmak üzere hello iş silinene kadar hello iş oluşturulur hello zamandan kapak etkinlikleri günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="01748-110">Diagnostic logs cover activities from hello time hello job is created until hello job is deleted, including updates and activities that occur while hello job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="01748-111">Tanılama günlüklerini Aç</span><span class="sxs-lookup"><span data-stu-id="01748-111">Turn on diagnostic logs</span></span>

<span data-ttu-id="01748-112">Tanılama günlükleri, varsayılan olarak devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="01748-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="01748-113">tooenable tanılama günlükleri, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="01748-113">tooenable diagnostic logs, perform hello following steps:</span></span>

1.  <span data-ttu-id="01748-114">Merhaba, [Azure portal](https://portal.azure.com)altında **izleme + Yönetim**, tıklatın **tanılama günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="01748-114">In hello [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![Dikey gezinti toodiagnostic günlükleri](./media/service-bus-diagnostic-logs/image1.png)

2. <span data-ttu-id="01748-116">Toomonitor istediğiniz hello kaynak'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="01748-116">Click hello resource you want toomonitor.</span></span>  

3.  <span data-ttu-id="01748-117">Tıklatın **tanılamayı açın**.</span><span class="sxs-lookup"><span data-stu-id="01748-117">Click **Turn on diagnostics**.</span></span>

    ![Tanılama günlüklerini Aç](./media/service-bus-diagnostic-logs/image2.png)

4.  <span data-ttu-id="01748-119">İçin **durum**, tıklatın **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="01748-119">For **Status**, click **On**.</span></span>

    ![Tanılama günlüklerini durumunu değiştirme](./media/service-bus-diagnostic-logs/image3.png)

5.  <span data-ttu-id="01748-121">İstediğiniz kümesi hello arşiv hedef; Örneğin, bir depolama hesabı, bir olay hub'ı veya Azure günlük analizi.</span><span class="sxs-lookup"><span data-stu-id="01748-121">Set hello archive target that you want; for example, a storage account, an Event Hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="01748-122">Merhaba yeni tanılama ayarları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="01748-122">Save hello new diagnostics settings.</span></span>

<span data-ttu-id="01748-123">Yeni ayarları yaklaşık 10 dakika içinde etkinleşir.</span><span class="sxs-lookup"><span data-stu-id="01748-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="01748-124">Bundan sonra günlükler hello üzerinde yapılandırılmış hello arşivleme hedef görünür **tanılama günlükleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="01748-124">After that, logs appear in hello configured archival target, on hello **Diagnostics logs** blade.</span></span>

<span data-ttu-id="01748-125">Merhaba tanılama yapılandırma hakkında daha fazla bilgi için bkz: [Azure tanılama günlükleri'ne genel bakış](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="01748-125">For more information about configuring diagnostics, see hello [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="01748-126">Tanılama günlüklerini şeması</span><span class="sxs-lookup"><span data-stu-id="01748-126">Diagnostic logs schema</span></span>

<span data-ttu-id="01748-127">Tüm günlükler JavaScript nesne gösterimi (JSON) biçiminde depolanır.</span><span class="sxs-lookup"><span data-stu-id="01748-127">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="01748-128">Her giriş bölümden hello açıklanan hello biçimini kullanan alanlarına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="01748-128">Each entry has string fields that use hello format described in hello following section.</span></span>

## <a name="operational-logs-schema"></a><span data-ttu-id="01748-129">İşlem günlükleri şeması</span><span class="sxs-lookup"><span data-stu-id="01748-129">Operational logs schema</span></span>

<span data-ttu-id="01748-130">Hello günlüklerini **OperationalLogs** kategori yakalama ne Service Bus işlemleri sırasında olur.</span><span class="sxs-lookup"><span data-stu-id="01748-130">Logs in hello **OperationalLogs** category capture what happens during Service Bus operations.</span></span> <span data-ttu-id="01748-131">Özellikle, bu günlükler hello işlem türü, kuyruk oluşturma, kullanılan, kaynakları dahil yakalamak ve hello işlemin durumunu hello.</span><span class="sxs-lookup"><span data-stu-id="01748-131">Specifically, these logs capture hello operation type, including queue creation, resources used, and hello status of hello operation.</span></span>

<span data-ttu-id="01748-132">İşlem günlüğü JSON dizeler, aşağıdaki tablonun hello listelenen öğeleri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="01748-132">Operational log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="01748-133">Ad</span><span class="sxs-lookup"><span data-stu-id="01748-133">Name</span></span> | <span data-ttu-id="01748-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="01748-134">Description</span></span>
------- | -------
<span data-ttu-id="01748-135">Etkinlik Kimliği</span><span class="sxs-lookup"><span data-stu-id="01748-135">ActivityId</span></span> | <span data-ttu-id="01748-136">İzleme için kullanılan iç kimliği</span><span class="sxs-lookup"><span data-stu-id="01748-136">Internal ID, used for tracking</span></span>
<span data-ttu-id="01748-137">EventName</span><span class="sxs-lookup"><span data-stu-id="01748-137">EventName</span></span> | <span data-ttu-id="01748-138">İşlem adı</span><span class="sxs-lookup"><span data-stu-id="01748-138">Operation name</span></span>           
<span data-ttu-id="01748-139">resourceId</span><span class="sxs-lookup"><span data-stu-id="01748-139">resourceId</span></span> | <span data-ttu-id="01748-140">Azure Resource Manager kaynak kimliği</span><span class="sxs-lookup"><span data-stu-id="01748-140">Azure Resource Manager resource ID</span></span>
<span data-ttu-id="01748-141">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="01748-141">SubscriptionId</span></span> | <span data-ttu-id="01748-142">Abonelik Kimliği</span><span class="sxs-lookup"><span data-stu-id="01748-142">Subscription ID</span></span>
<span data-ttu-id="01748-143">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="01748-143">EventTimeString</span></span> | <span data-ttu-id="01748-144">İşlem süresi</span><span class="sxs-lookup"><span data-stu-id="01748-144">Operation time</span></span>
<span data-ttu-id="01748-145">EventProperties</span><span class="sxs-lookup"><span data-stu-id="01748-145">EventProperties</span></span> | <span data-ttu-id="01748-146">İşlem özellikleri</span><span class="sxs-lookup"><span data-stu-id="01748-146">Operation properties</span></span>
<span data-ttu-id="01748-147">Durum</span><span class="sxs-lookup"><span data-stu-id="01748-147">Status</span></span> | <span data-ttu-id="01748-148">İşlem durumu</span><span class="sxs-lookup"><span data-stu-id="01748-148">Operation status</span></span>
<span data-ttu-id="01748-149">Çağıran</span><span class="sxs-lookup"><span data-stu-id="01748-149">Caller</span></span> | <span data-ttu-id="01748-150">Arayan işlemi (Azure portalı veya yönetim istemcisi)</span><span class="sxs-lookup"><span data-stu-id="01748-150">Caller of operation (Azure portal or management client)</span></span>
<span data-ttu-id="01748-151">category</span><span class="sxs-lookup"><span data-stu-id="01748-151">category</span></span> | <span data-ttu-id="01748-152">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="01748-152">OperationalLogs</span></span>

<span data-ttu-id="01748-153">Bir işlem günlüğü JSON dize örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="01748-153">Here's an example of an operational log JSON string:</span></span>

```json
{
  "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
  "EventName": "Create Queue",
  "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.SERVICEBUS/NAMESPACES/SHOEBOXEHNS-CY4001",
  "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
  "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
  "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
  "Status": "Succeeded",
  "Caller": "ServiceBus Client",
  "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="01748-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="01748-154">Next steps</span></span>

<span data-ttu-id="01748-155">Service Bus hakkında daha fazla bağlantılar toolearn aşağıdaki hello ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="01748-155">Visit hello following links toolearn more about Service Bus:</span></span>

* [<span data-ttu-id="01748-156">Giriş tooService veri yolu</span><span class="sxs-lookup"><span data-stu-id="01748-156">Introduction tooService Bus</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="01748-157">Service Bus ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="01748-157">Get started with Service Bus</span></span>](service-bus-dotnet-get-started-with-queues.md)
