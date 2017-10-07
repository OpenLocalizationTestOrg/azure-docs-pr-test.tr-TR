---
title: "Azure sanal makineleri kullanarak otomatik ölçeklendirme aaaAdvanced | Microsoft Docs"
description: "Birden çok kural ve e-posta göndermek ve ölçek eylemleri ile Web kancası URL'leri çağrı profillerinin Resource Manager ve VM ölçek kümesi kullanır."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 7e3576e2-4a2b-4736-b5ae-98c4689cdd2b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2016
ms.author: ancav
ms.openlocfilehash: ecb01e3094f715837b75ef07a7dbecdf0f2e78f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a><span data-ttu-id="d91f6-103">VM ölçek kümesi için Resource Manager şablonları kullanarak gelişmiş otomatik ölçeklendirme yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d91f6-103">Advanced autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>
<span data-ttu-id="d91f6-104">Ölçek ve sanal makine ölçek kümeleri yinelenen bir zamanlamaya göre veya belirli bir tarihe göre performans ölçüm eşiklere dayanarak genişleme kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d91f6-104">You can scale-in and scale-out in Virtual Machine Scale Sets based on performance metric thresholds, by a recurring schedule, or by a particular date.</span></span> <span data-ttu-id="d91f6-105">Ölçeklendirme eylemi için e-posta ve Web kancası bildirimleri de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d91f6-105">You can also configure email and webhook notifications for scale actions.</span></span> <span data-ttu-id="d91f6-106">Bu kılavuz, bir VM ölçek kümesi üzerinde bir Resource Manager şablonu kullanarak bu nesneleri yapılandırma örneği gösterilir.</span><span class="sxs-lookup"><span data-stu-id="d91f6-106">This walkthrough shows an example of configuring all these objects using a Resource Manager template on a VM Scale Set.</span></span>

> [!NOTE]
> <span data-ttu-id="d91f6-107">Bu kılavuz, VM ölçek kümesi için hello adımlar açıklanmaktadır, ancak hello aynı bilgiler tooautoscaling geçerlidir [bulut Hizmetleri](https://azure.microsoft.com/services/cloud-services/), ve [uygulama hizmeti - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="d91f6-107">While this walkthrough explains hello steps for VM Scale Sets, hello same information applies tooautoscaling [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span>
> <span data-ttu-id="d91f6-108">Bir basit performans ölçümü CPU gibi basit bir ölçek giriş/çıkış VM ölçek kümesi ayarda dayalı için toohello başvuran [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) ve [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) belgeleri</span><span class="sxs-lookup"><span data-stu-id="d91f6-108">For a simple scale in/out setting on a VM Scale Set based on a simple performance metric such as CPU, refer toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) and [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documents</span></span>
>
>

## <a name="walkthrough"></a><span data-ttu-id="d91f6-109">Kılavuz</span><span class="sxs-lookup"><span data-stu-id="d91f6-109">Walkthrough</span></span>
<span data-ttu-id="d91f6-110">Bu kılavuzda, kullandığımız [Azure kaynak Gezgini](https://resources.azure.com/) tooconfigure ve güncelleştirme hello otomatik ölçeklendirme ayarının ölçek kümesi için.</span><span class="sxs-lookup"><span data-stu-id="d91f6-110">In this walkthrough, we use [Azure Resource Explorer](https://resources.azure.com/) tooconfigure and update hello autoscale setting for a scale set.</span></span> <span data-ttu-id="d91f6-111">Azure kaynak Gezgini kolay bir yolu toomanage olan Resource Manager şablonları aracılığıyla Azure kaynakları.</span><span class="sxs-lookup"><span data-stu-id="d91f6-111">Azure Resource Explorer is an easy way toomanage Azure resources via Resource Manager templates.</span></span> <span data-ttu-id="d91f6-112">Yeni tooAzure kaynak Gezgini aracı varsa, okuma [bu giriş](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span><span class="sxs-lookup"><span data-stu-id="d91f6-112">If you are new tooAzure Resource Explorer tool, read [this introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span></span>

1. <span data-ttu-id="d91f6-113">Bir temel otomatik ölçeklendirme ayarı ile yeni bir ölçek dağıtın.</span><span class="sxs-lookup"><span data-stu-id="d91f6-113">Deploy a new scale set with a basic autoscale setting.</span></span> <span data-ttu-id="d91f6-114">Bu makalede hello sahip bir Windows Azure hızlı başlama Galerisi gelen hello kullanan ölçek kümesi temel otomatik ölçeklendirme şablonla.</span><span class="sxs-lookup"><span data-stu-id="d91f6-114">This article uses hello one from hello Azure QuickStart Gallery, which has a Windows scale set with a basic autoscale template.</span></span> <span data-ttu-id="d91f6-115">Linux ölçek ayarlar çalışma hello aynı şekilde.</span><span class="sxs-lookup"><span data-stu-id="d91f6-115">Linux scale sets work hello same way.</span></span>
2. <span data-ttu-id="d91f6-116">Merhaba ölçek kümesi oluşturulduktan sonra Azure kaynak Gezgini toohello ölçek kümesi kaynaktan gidin.</span><span class="sxs-lookup"><span data-stu-id="d91f6-116">After hello scale set is created, navigate toohello scale set resource from Azure Resource Explorer.</span></span> <span data-ttu-id="d91f6-117">Merhaba aşağıdaki Microsoft.ınsights düğümü altında bakın.</span><span class="sxs-lookup"><span data-stu-id="d91f6-117">You see hello following under Microsoft.Insights node.</span></span>

    ![Azure Gezgini](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    <span data-ttu-id="d91f6-119">Hello şablon yürütme hello ada sahip varsayılan bir otomatik ölçeklendirme ayarı oluşturdu **'autoscalewad'**.</span><span class="sxs-lookup"><span data-stu-id="d91f6-119">hello template execution has created a default autoscale setting with hello name **'autoscalewad'**.</span></span> <span data-ttu-id="d91f6-120">Merhaba sağ tarafta, bu otomatik ölçeklendirme ayarı tam tanımını hello görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d91f6-120">On hello right-hand side, you can view hello full definition of this autoscale setting.</span></span> <span data-ttu-id="d91f6-121">Bu durumda, hello varsayılan otomatik ölçeklendirme ayarında bir CPU tabanlı % genişleme ve ölçek bileşenini kuralı ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="d91f6-121">In this case, hello default autoscale setting comes with a CPU% based scale-out and scale-in rule.</span></span>  

3. <span data-ttu-id="d91f6-122">Artık daha fazla profilleri ve hello zamanlama veya özel gereksinimler dayalı kurallar ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d91f6-122">You can now add more profiles and rules based on hello schedule or specific requirements.</span></span> <span data-ttu-id="d91f6-123">Üç profil ile bir otomatik ölçeklendirme ayarı oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="d91f6-123">We create an autoscale setting with three profiles.</span></span> <span data-ttu-id="d91f6-124">toounderstand profilleri ve otomatik ölçeklendirme, kuralları gözden [otomatik ölçeklendirme en iyi yöntemler](insights-autoscale-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="d91f6-124">toounderstand profiles and rules in autoscale, review [Autoscale Best Practices](insights-autoscale-best-practices.md).</span></span>  

    | <span data-ttu-id="d91f6-125">Profilleri & kuralları</span><span class="sxs-lookup"><span data-stu-id="d91f6-125">Profiles & Rules</span></span> | <span data-ttu-id="d91f6-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d91f6-126">Description</span></span> |
    |--- | --- |
    | <span data-ttu-id="d91f6-127">**Profili**</span><span class="sxs-lookup"><span data-stu-id="d91f6-127">**Profile**</span></span> |<span data-ttu-id="d91f6-128">**Performans/ölçü dayalı**</span><span class="sxs-lookup"><span data-stu-id="d91f6-128">**Performance/metric based**</span></span> |
    | <span data-ttu-id="d91f6-129">Kural</span><span class="sxs-lookup"><span data-stu-id="d91f6-129">Rule</span></span> |<span data-ttu-id="d91f6-130">Hizmet veri yolu kuyruğu ileti sayısı > x</span><span class="sxs-lookup"><span data-stu-id="d91f6-130">Service Bus Queue Message Count > x</span></span> |
    | <span data-ttu-id="d91f6-131">Kural</span><span class="sxs-lookup"><span data-stu-id="d91f6-131">Rule</span></span> |<span data-ttu-id="d91f6-132">Hizmet veri yolu kuyruğu ileti sayısı < y</span><span class="sxs-lookup"><span data-stu-id="d91f6-132">Service Bus Queue Message Count < y</span></span> |
    | <span data-ttu-id="d91f6-133">Kural</span><span class="sxs-lookup"><span data-stu-id="d91f6-133">Rule</span></span> |<span data-ttu-id="d91f6-134">CPU % > n</span><span class="sxs-lookup"><span data-stu-id="d91f6-134">CPU% > n</span></span> |
    | <span data-ttu-id="d91f6-135">Kural</span><span class="sxs-lookup"><span data-stu-id="d91f6-135">Rule</span></span> |<span data-ttu-id="d91f6-136">CPU % < p</span><span class="sxs-lookup"><span data-stu-id="d91f6-136">CPU% < p</span></span> |
    | <span data-ttu-id="d91f6-137">**Profili**</span><span class="sxs-lookup"><span data-stu-id="d91f6-137">**Profile**</span></span> |<span data-ttu-id="d91f6-138">**Hafta içi gün sabah saat (kuralları yok)**</span><span class="sxs-lookup"><span data-stu-id="d91f6-138">**Weekday morning hours (no rules)**</span></span> |
    | <span data-ttu-id="d91f6-139">**Profili**</span><span class="sxs-lookup"><span data-stu-id="d91f6-139">**Profile**</span></span> |<span data-ttu-id="d91f6-140">**Ürün başlatma gün (kuralları yok)**</span><span class="sxs-lookup"><span data-stu-id="d91f6-140">**Product Launch day (no rules)**</span></span> |

4. <span data-ttu-id="d91f6-141">Bu kılavuz için kullandığımız kuramsal bir ölçeklendirme senaryo aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d91f6-141">Here is a hypothetical scaling scenario that we use for this walk-through.</span></span>

    * <span data-ttu-id="d91f6-142">**Temel yük** -tooscale veya my ölçek set.* üzerinde barındırılan Uygulamam hello yüküne göre istiyorum</span><span class="sxs-lookup"><span data-stu-id="d91f6-142">**Load based** - I'd like tooscale out or in based on hello load on my application hosted on my scale set.*</span></span>
    * <span data-ttu-id="d91f6-143">**Sıra boyutu ileti** -ı Merhaba gelen iletileri toomy uygulaması için bir hizmet veri yolu kuyruğu kullanın.</span><span class="sxs-lookup"><span data-stu-id="d91f6-143">**Message Queue size** - I use a Service Bus Queue for hello incoming messages toomy application.</span></span> <span data-ttu-id="d91f6-144">Merhaba sıranın ileti sayısı ve CPU % kullanın ve ileti sayısı veya CPU isabet threshold.* hello bir varsayılan profili tootrigger bir ölçek eylemi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d91f6-144">I use hello queue's message count and CPU% and configure a default profile tootrigger a scale action if either of message count or CPU hits hello threshold.*</span></span>
    * <span data-ttu-id="d91f6-145">**Haftanın günü ve saat** -'Hafta içi gün sabah saat' adlı bir haftalık yinelenen 'zaman hello günün' temel profil istiyor.</span><span class="sxs-lookup"><span data-stu-id="d91f6-145">**Time of week and day** - I want a weekly recurring 'time of hello day' based profile called 'Weekday Morning Hours'.</span></span> <span data-ttu-id="d91f6-146">Geçmiş verilerini temel alarak VM sayısı toohandle my uygulamanın yükleme sırasında bu sağlar.* örnekleri belirli daha iyi toohave olduğunu bilmeniz</span><span class="sxs-lookup"><span data-stu-id="d91f6-146">Based on historical data, I know it is better toohave certain number of VM instances toohandle my application's load during this time.*</span></span>
    * <span data-ttu-id="d91f6-147">**Özel tarih** -'Ürün başlatma Day' profili eklendi.</span><span class="sxs-lookup"><span data-stu-id="d91f6-147">**Special Dates** - I added a 'Product Launch Day' profile.</span></span> <span data-ttu-id="d91f6-148">Böylece Uygulamam hazır toohandle hello yük pazarlama duyuruları nedeniyle ve biz hello uygulamasında yeni bir ürün zaman put t belirli tarihler için İleriyi</span><span class="sxs-lookup"><span data-stu-id="d91f6-148">I plan ahead for specific dates so my application is ready toohandle hello load due marketing announcements and when we put a new product in hello application.*</span></span>
    * <span data-ttu-id="d91f6-149">*Son iki Hello profilleri diğer performans ölçüm tabanlı içinde kurallar bunları da sahip olabilirsiniz. Bu durumda değil toohave bir karar ve bunun yerine toorely üzerinde hello varsayılan performans ölçüm kuralları dayalı. Kuralları hello yinelenen ve tarih temelli profilleri için isteğe bağlıdır.*</span><span class="sxs-lookup"><span data-stu-id="d91f6-149">*hello last two profiles can also have other performance metric based rules within them. In this case, I decided not toohave one and instead toorely on hello default performance metric based rules. Rules are optional for hello recurring and date-based profiles.*</span></span>

    <span data-ttu-id="d91f6-150">Otomatik ölçeklendirme altyapısının önceliği hello profilleri ve kuralları hello ayrıca yakalanan [otomatik ölçeklendirmeyi en iyi yöntemler](insights-autoscale-best-practices.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="d91f6-150">Autoscale engine's prioritization of hello profiles and rules is also captured in hello [autoscaling best practices](insights-autoscale-best-practices.md) article.</span></span>
    <span data-ttu-id="d91f6-151">Otomatik ölçeklendirme için ortak ölçümleri listesi için bkz [otomatik ölçeklendirme için ortak ölçümleri](insights-autoscale-common-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="d91f6-151">For a list of common metrics for autoscale, refer [Common metrics for Autoscale](insights-autoscale-common-metrics.md)</span></span>

5. <span data-ttu-id="d91f6-152">Merhaba üzerinde olduğundan emin olun **okuma/yazma** kaynak Gezgininde modu</span><span class="sxs-lookup"><span data-stu-id="d91f6-152">Make sure you are on hello **Read/Write** mode in Resource Explorer</span></span>

    ![Autoscalewad, varsayılan otomatik ölçeklendirme ayarı](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. <span data-ttu-id="d91f6-154">Düzenle'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d91f6-154">Click Edit.</span></span> <span data-ttu-id="d91f6-155">**Değiştir** hello 'profilleri' öğesinde yapılandırma aşağıdaki hello otomatik ölçeklendirme ayarı:</span><span class="sxs-lookup"><span data-stu-id="d91f6-155">**Replace** hello 'profiles' element in autoscale setting with hello following configuration:</span></span>

    ![Profilleri](./media/insights-advanced-autoscale-vmss/profiles.png)

    ```
    {
            "name": "Perf_Based_Scale",
            "capacity": {
              "minimum": "2",
              "maximum": "12",
              "default": "2"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 10
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 3
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 85
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          },
          {
            "name": "Weekday_Morning_Hours_Scale",
            "capacity": {
              "minimum": "4",
              "maximum": "12",
              "default": "4"
            },
            "rules": [],
            "recurrence": {
              "frequency": "Week",
              "schedule": {
                "timeZone": "Pacific Standard Time",
                "days": [
                  "Monday",
                  "Tuesday",
                  "Wednesday",
                  "Thursday",
                  "Friday"
                ],
                "hours": [
                  6
                ],
                "minutes": [
                  0
                ]
              }
            }
          },
          {
            "name": "Product_Launch_Day",
            "capacity": {
              "minimum": "6",
              "maximum": "20",
              "default": "6"
            },
            "rules": [],
            "fixedDate": {
              "timeZone": "Pacific Standard Time",
              "start": "2016-06-20T00:06:00Z",
              "end": "2016-06-21T23:59:00Z"
            }
          }
    ```
    <span data-ttu-id="d91f6-157">Desteklenen alanlar ve bunların değerleri için bkz: [otomatik ölçeklendirme REST API belgeleri](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="d91f6-157">For supported fields and their values, see [Autoscale REST API documentation](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span></span> <span data-ttu-id="d91f6-158">Şimdi, otomatik ölçeklendirme ayarında daha önce açıklanan hello üç profil içerir.</span><span class="sxs-lookup"><span data-stu-id="d91f6-158">Now your autoscale setting contains hello three profiles explained previously.</span></span>

7. <span data-ttu-id="d91f6-159">Son olarak, otomatik ölçeklendirme hello Ara **bildirim** bölümü.</span><span class="sxs-lookup"><span data-stu-id="d91f6-159">Finally, look at hello Autoscale **notification** section.</span></span> <span data-ttu-id="d91f6-160">Otomatik ölçeklendirme bildirimleri toodo üç şey bir genişletme zaman izin verin veya eylemi başarıyla tetiklendi.</span><span class="sxs-lookup"><span data-stu-id="d91f6-160">Autoscale notifications allow you toodo three things when a scale-out or in action is successfully triggered.</span></span>
   - <span data-ttu-id="d91f6-161">Hello Yöneticisi ve ortak yöneticileri aboneliğinizin bildir</span><span class="sxs-lookup"><span data-stu-id="d91f6-161">Notify hello admin and co-admins of your subscription</span></span>
   - <span data-ttu-id="d91f6-162">Kullanıcı e-posta</span><span class="sxs-lookup"><span data-stu-id="d91f6-162">Email a set of users</span></span>
   - <span data-ttu-id="d91f6-163">Bir Web kancası çağrı tetikler.</span><span class="sxs-lookup"><span data-stu-id="d91f6-163">Trigger a webhook call.</span></span> <span data-ttu-id="d91f6-164">Harekete, bu Web kancası hello otomatik ölçeklendirmeyi koşul hakkındaki meta verileri gönderir ve kaynak hello ölçek kümesi.</span><span class="sxs-lookup"><span data-stu-id="d91f6-164">When fired, this webhook sends metadata about hello autoscaling condition and hello scale set resource.</span></span> <span data-ttu-id="d91f6-165">otomatik ölçeklendirme Web kancası hello yükünü hakkında daha fazla toolearn bkz [yapılandırma Web kancası & otomatik ölçeklendirme için e-posta bildirimleri](insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="d91f6-165">toolearn more about hello payload of autoscale webhook, see [Configure Webhook & Email Notifications for Autoscale](insights-autoscale-to-webhook-email.md).</span></span>

   <span data-ttu-id="d91f6-166">Toohello otomatik ölçeklendirme ayarı değiştirerek aşağıdaki hello eklemek, **bildirim** öğesi değeri null</span><span class="sxs-lookup"><span data-stu-id="d91f6-166">Add hello following toohello Autoscale setting replacing your **notification** element whose value is null</span></span>

   ```
   "notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": true,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]

   ```

   <span data-ttu-id="d91f6-167">İsabet **Put** kaynak Gezgini tooupdate hello otomatik ölçeklendirme ayarında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d91f6-167">Hit **Put** button in Resource Explorer tooupdate hello autoscale setting.</span></span>

<span data-ttu-id="d91f6-168">Bir otomatik ölçeklendirme VM ölçek kümesi tooinclude üzerinde birden fazla ölçek profilleri ayarı güncelleştirdiniz ve bildirimleri ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="d91f6-168">You have updated an autoscale setting on a VM Scale set tooinclude multiple scale profiles and scale notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d91f6-169">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="d91f6-169">Next Steps</span></span>
<span data-ttu-id="d91f6-170">Otomatik ölçeklendirme hakkında daha fazla bu bağlantılar toolearn kullanın.</span><span class="sxs-lookup"><span data-stu-id="d91f6-170">Use these links toolearn more about autoscaling.</span></span>

[<span data-ttu-id="d91f6-171">Otomatik ölçeklendirme sanal makine ölçek kümeleri ile ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="d91f6-171">TroubleShoot Autoscale with Virtual Machine Scale Sets</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[<span data-ttu-id="d91f6-172">Otomatik ölçeklendirme için ortak ölçümleri</span><span class="sxs-lookup"><span data-stu-id="d91f6-172">Common Metrics for Autoscale</span></span>](insights-autoscale-common-metrics.md)

[<span data-ttu-id="d91f6-173">Azure otomatik ölçeklendirme için en iyi yöntemler</span><span class="sxs-lookup"><span data-stu-id="d91f6-173">Best Practices for Azure Autoscale</span></span>](insights-autoscale-best-practices.md)

[<span data-ttu-id="d91f6-174">Otomatik ölçeklendirme PowerShell kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="d91f6-174">Manage Autoscale using PowerShell</span></span>](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[<span data-ttu-id="d91f6-175">Otomatik ölçeklendirme CLI kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="d91f6-175">Manage Autoscale using CLI</span></span>](insights-cli-samples.md#autoscale)

[<span data-ttu-id="d91f6-176">Web kancası & otomatik ölçeklendirme için e-posta bildirimleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d91f6-176">Configure Webhook & Email Notifications for Autoscale</span></span>](insights-autoscale-to-webhook-email.md)
