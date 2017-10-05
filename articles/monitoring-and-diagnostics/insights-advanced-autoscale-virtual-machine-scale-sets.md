---
title: "Azure sanal makineleri kullanarak otomatik ölçeklendirme Gelişmiş | Microsoft Docs"
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
ms.openlocfilehash: 80955535c8d863cd3d8d1b77e2ab8bc016b6d9f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a><span data-ttu-id="f2b32-103">VM ölçek kümesi için Resource Manager şablonları kullanarak gelişmiş otomatik ölçeklendirme yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f2b32-103">Advanced autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>
<span data-ttu-id="f2b32-104">Ölçek ve sanal makine ölçek kümeleri yinelenen bir zamanlamaya göre veya belirli bir tarihe göre performans ölçüm eşiklere dayanarak genişleme kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2b32-104">You can scale-in and scale-out in Virtual Machine Scale Sets based on performance metric thresholds, by a recurring schedule, or by a particular date.</span></span> <span data-ttu-id="f2b32-105">Ölçeklendirme eylemi için e-posta ve Web kancası bildirimleri de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2b32-105">You can also configure email and webhook notifications for scale actions.</span></span> <span data-ttu-id="f2b32-106">Bu kılavuz, bir VM ölçek kümesi üzerinde bir Resource Manager şablonu kullanarak bu nesneleri yapılandırma örneği gösterilir.</span><span class="sxs-lookup"><span data-stu-id="f2b32-106">This walkthrough shows an example of configuring all these objects using a Resource Manager template on a VM Scale Set.</span></span>

> [!NOTE]
> <span data-ttu-id="f2b32-107">Bu izlenecek adımları VM ölçek kümesi için açıklamaktadır, ancak aynı bilgiler için otomatik ölçeklendirmeyi geçerlidir [bulut Hizmetleri](https://azure.microsoft.com/services/cloud-services/), ve [uygulama hizmeti - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="f2b32-107">While this walkthrough explains the steps for VM Scale Sets, the same information applies to autoscaling [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span>
> <span data-ttu-id="f2b32-108">Bir basit performans ölçümü CPU gibi basit bir ölçek giriş/çıkış VM ölçek kümesi ayarda dayanarak, bakın [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) ve [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) belgeleri</span><span class="sxs-lookup"><span data-stu-id="f2b32-108">For a simple scale in/out setting on a VM Scale Set based on a simple performance metric such as CPU, refer to the [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) and [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documents</span></span>
>
>

## <a name="walkthrough"></a><span data-ttu-id="f2b32-109">Kılavuz</span><span class="sxs-lookup"><span data-stu-id="f2b32-109">Walkthrough</span></span>
<span data-ttu-id="f2b32-110">Bu kılavuzda, kullandığımız [Azure kaynak Gezgini](https://resources.azure.com/) yapılandırmak ve ölçek kümesi için otomatik ölçeklendirme ayarı güncelleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f2b32-110">In this walkthrough, we use [Azure Resource Explorer](https://resources.azure.com/) to configure and update the autoscale setting for a scale set.</span></span> <span data-ttu-id="f2b32-111">Azure kaynak Gezgini, Resource Manager şablonları aracılığıyla Azure kaynaklarınızı yönetmek için kolay bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="f2b32-111">Azure Resource Explorer is an easy way to manage Azure resources via Resource Manager templates.</span></span> <span data-ttu-id="f2b32-112">Azure kaynak Gezgini aracı yeniyseniz, okuma [bu giriş](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span><span class="sxs-lookup"><span data-stu-id="f2b32-112">If you are new to Azure Resource Explorer tool, read [this introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span></span>

1. <span data-ttu-id="f2b32-113">Bir temel otomatik ölçeklendirme ayarı ile yeni bir ölçek dağıtın.</span><span class="sxs-lookup"><span data-stu-id="f2b32-113">Deploy a new scale set with a basic autoscale setting.</span></span> <span data-ttu-id="f2b32-114">Bu makalede Windows sahip Azure hızlı başlama Galerisi adresinden kullanan ölçek temel otomatik ölçeklendirme şablonla ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f2b32-114">This article uses the one from the Azure QuickStart Gallery, which has a Windows scale set with a basic autoscale template.</span></span> <span data-ttu-id="f2b32-115">Linux ölçek kümeleri aynı şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="f2b32-115">Linux scale sets work the same way.</span></span>
2. <span data-ttu-id="f2b32-116">Ölçek kümesi oluşturulduktan sonra Azure kaynak Gezgini'nden ölçek kümesi kaynağa gidin.</span><span class="sxs-lookup"><span data-stu-id="f2b32-116">After the scale set is created, navigate to the scale set resource from Azure Resource Explorer.</span></span> <span data-ttu-id="f2b32-117">Aşağıdaki Microsoft.ınsights düğümü altında bakın.</span><span class="sxs-lookup"><span data-stu-id="f2b32-117">You see the following under Microsoft.Insights node.</span></span>

    ![Azure Gezgini](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    <span data-ttu-id="f2b32-119">Şablon yürütme varsayılan otomatik ölçeklendirme ayarı adı ile oluşturdu **'autoscalewad'**.</span><span class="sxs-lookup"><span data-stu-id="f2b32-119">The template execution has created a default autoscale setting with the name **'autoscalewad'**.</span></span> <span data-ttu-id="f2b32-120">Sağ tarafta, bu otomatik ölçeklendirme ayarı tam tanımını görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2b32-120">On the right-hand side, you can view the full definition of this autoscale setting.</span></span> <span data-ttu-id="f2b32-121">Bu durumda, varsayılan otomatik ölçeklendirme ayarında bir CPU tabanlı % genişleme ve ölçek bileşenini kuralı ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="f2b32-121">In this case, the default autoscale setting comes with a CPU% based scale-out and scale-in rule.</span></span>  

3. <span data-ttu-id="f2b32-122">Artık daha fazla profilleri ve zamanlama veya özel gereksinimler dayalı kurallar da ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2b32-122">You can now add more profiles and rules based on the schedule or specific requirements.</span></span> <span data-ttu-id="f2b32-123">Üç profil ile bir otomatik ölçeklendirme ayarı oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="f2b32-123">We create an autoscale setting with three profiles.</span></span> <span data-ttu-id="f2b32-124">Profilleri ve otomatik ölçeklendirme kurallarında anlamak için gözden [otomatik ölçeklendirme en iyi yöntemler](insights-autoscale-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="f2b32-124">To understand profiles and rules in autoscale, review [Autoscale Best Practices](insights-autoscale-best-practices.md).</span></span>  

    | <span data-ttu-id="f2b32-125">Profilleri & kuralları</span><span class="sxs-lookup"><span data-stu-id="f2b32-125">Profiles & Rules</span></span> | <span data-ttu-id="f2b32-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f2b32-126">Description</span></span> |
    |--- | --- |
    | <span data-ttu-id="f2b32-127">**Profili**</span><span class="sxs-lookup"><span data-stu-id="f2b32-127">**Profile**</span></span> |<span data-ttu-id="f2b32-128">**Performans/ölçü dayalı**</span><span class="sxs-lookup"><span data-stu-id="f2b32-128">**Performance/metric based**</span></span> |
    | <span data-ttu-id="f2b32-129">Kural</span><span class="sxs-lookup"><span data-stu-id="f2b32-129">Rule</span></span> |<span data-ttu-id="f2b32-130">Hizmet veri yolu kuyruğu ileti sayısı > x</span><span class="sxs-lookup"><span data-stu-id="f2b32-130">Service Bus Queue Message Count > x</span></span> |
    | <span data-ttu-id="f2b32-131">Kural</span><span class="sxs-lookup"><span data-stu-id="f2b32-131">Rule</span></span> |<span data-ttu-id="f2b32-132">Hizmet veri yolu kuyruğu ileti sayısı < y</span><span class="sxs-lookup"><span data-stu-id="f2b32-132">Service Bus Queue Message Count < y</span></span> |
    | <span data-ttu-id="f2b32-133">Kural</span><span class="sxs-lookup"><span data-stu-id="f2b32-133">Rule</span></span> |<span data-ttu-id="f2b32-134">CPU % > n</span><span class="sxs-lookup"><span data-stu-id="f2b32-134">CPU% > n</span></span> |
    | <span data-ttu-id="f2b32-135">Kural</span><span class="sxs-lookup"><span data-stu-id="f2b32-135">Rule</span></span> |<span data-ttu-id="f2b32-136">CPU % < p</span><span class="sxs-lookup"><span data-stu-id="f2b32-136">CPU% < p</span></span> |
    | <span data-ttu-id="f2b32-137">**Profili**</span><span class="sxs-lookup"><span data-stu-id="f2b32-137">**Profile**</span></span> |<span data-ttu-id="f2b32-138">**Hafta içi gün sabah saat (kuralları yok)**</span><span class="sxs-lookup"><span data-stu-id="f2b32-138">**Weekday morning hours (no rules)**</span></span> |
    | <span data-ttu-id="f2b32-139">**Profili**</span><span class="sxs-lookup"><span data-stu-id="f2b32-139">**Profile**</span></span> |<span data-ttu-id="f2b32-140">**Ürün başlatma gün (kuralları yok)**</span><span class="sxs-lookup"><span data-stu-id="f2b32-140">**Product Launch day (no rules)**</span></span> |

4. <span data-ttu-id="f2b32-141">Bu kılavuz için kullandığımız kuramsal bir ölçeklendirme senaryo aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f2b32-141">Here is a hypothetical scaling scenario that we use for this walk-through.</span></span>

    * <span data-ttu-id="f2b32-142">**Temel yük** - veya ölçeklendirmek my ölçek set.* üzerinde barındırılan Uygulamam üzerindeki yükü göre istiyorum</span><span class="sxs-lookup"><span data-stu-id="f2b32-142">**Load based** - I'd like to scale out or in based on the load on my application hosted on my scale set.*</span></span>
    * <span data-ttu-id="f2b32-143">**Sıra boyutu ileti** -ı bir hizmet veri yolu kuyruğu gelen iletiler için Uygulamam için kullanın.</span><span class="sxs-lookup"><span data-stu-id="f2b32-143">**Message Queue size** - I use a Service Bus Queue for the incoming messages to my application.</span></span> <span data-ttu-id="f2b32-144">Sıranın ileti sayısı ve CPU % kullanın ve ileti sayısı ya da CPU değerse threshold.* bir ölçek eylemi tetiklemek için bir varsayılan profili yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f2b32-144">I use the queue's message count and CPU% and configure a default profile to trigger a scale action if either of message count or CPU hits the threshold.*</span></span>
    * <span data-ttu-id="f2b32-145">**Haftanın günü ve saat** -'Hafta içi gün sabah saat' adlı bir haftalık yinelenen 'zaman günün' temel profil istiyor.</span><span class="sxs-lookup"><span data-stu-id="f2b32-145">**Time of week and day** - I want a weekly recurring 'time of the day' based profile called 'Weekday Morning Hours'.</span></span> <span data-ttu-id="f2b32-146">Geçmiş verilerini temel alarak bu sağlar.* sırasında my uygulamanın yükü işlemek üzere VM örnekleri belirli sayıda daha iyidir bildirin</span><span class="sxs-lookup"><span data-stu-id="f2b32-146">Based on historical data, I know it is better to have certain number of VM instances to handle my application's load during this time.*</span></span>
    * <span data-ttu-id="f2b32-147">**Özel tarih** -'Ürün başlatma Day' profili eklendi.</span><span class="sxs-lookup"><span data-stu-id="f2b32-147">**Special Dates** - I added a 'Product Launch Day' profile.</span></span> <span data-ttu-id="f2b32-148">Uygulamam pazarlama duyuruları nedeniyle ve size yeni bir ürün uygulamasında geçirdiğinizde yükü işlemek üzere hazır olması için t belirli tarihler için İleriyi</span><span class="sxs-lookup"><span data-stu-id="f2b32-148">I plan ahead for specific dates so my application is ready to handle the load due marketing announcements and when we put a new product in the application.*</span></span>
    * <span data-ttu-id="f2b32-149">*Son iki profilleri diğer performans ölçüm tabanlı içinde kurallar bunları da sahip olabilirsiniz. Bu durumda, bir tane değil karar ve bunun yerine varsayılan performans ölçüm yararlanmayı kuralları dayalı. Kurallar yinelenen ve tarih temelli profilleri için isteğe bağlıdır.*</span><span class="sxs-lookup"><span data-stu-id="f2b32-149">*The last two profiles can also have other performance metric based rules within them. In this case, I decided not to have one and instead to rely on the default performance metric based rules. Rules are optional for the recurring and date-based profiles.*</span></span>

    <span data-ttu-id="f2b32-150">Otomatik ölçeklendirme altyapısının önceliği profilleri ve kuralları yakalanan de [otomatik ölçeklendirmeyi en iyi yöntemler](insights-autoscale-best-practices.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="f2b32-150">Autoscale engine's prioritization of the profiles and rules is also captured in the [autoscaling best practices](insights-autoscale-best-practices.md) article.</span></span>
    <span data-ttu-id="f2b32-151">Otomatik ölçeklendirme için ortak ölçümleri listesi için bkz [otomatik ölçeklendirme için ortak ölçümleri](insights-autoscale-common-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="f2b32-151">For a list of common metrics for autoscale, refer [Common metrics for Autoscale](insights-autoscale-common-metrics.md)</span></span>

5. <span data-ttu-id="f2b32-152">Olduğunuzdan emin olun, üzerinde **okuma/yazma** kaynak Gezgininde modu</span><span class="sxs-lookup"><span data-stu-id="f2b32-152">Make sure you are on the **Read/Write** mode in Resource Explorer</span></span>

    ![Autoscalewad, varsayılan otomatik ölçeklendirme ayarı](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. <span data-ttu-id="f2b32-154">Düzenle'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f2b32-154">Click Edit.</span></span> <span data-ttu-id="f2b32-155">**Değiştir** aşağıdaki yapılandırma ile otomatik ölçeklendirme ayarında 'profilleri' öğesi:</span><span class="sxs-lookup"><span data-stu-id="f2b32-155">**Replace** the 'profiles' element in autoscale setting with the following configuration:</span></span>

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
    <span data-ttu-id="f2b32-157">Desteklenen alanlar ve bunların değerleri için bkz: [otomatik ölçeklendirme REST API belgeleri](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2b32-157">For supported fields and their values, see [Autoscale REST API documentation](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span></span> <span data-ttu-id="f2b32-158">Şimdi, otomatik ölçeklendirme ayarı daha önce açıklanan üç profil içerir.</span><span class="sxs-lookup"><span data-stu-id="f2b32-158">Now your autoscale setting contains the three profiles explained previously.</span></span>

7. <span data-ttu-id="f2b32-159">Son olarak, otomatik ölçeklendirme Ara **bildirim** bölümü.</span><span class="sxs-lookup"><span data-stu-id="f2b32-159">Finally, look at the Autoscale **notification** section.</span></span> <span data-ttu-id="f2b32-160">Otomatik ölçeklendirme bildirimleri bir genişletme zaman üç şey yapmanıza olanak sağlar veya eylemi başarıyla tetiklendi.</span><span class="sxs-lookup"><span data-stu-id="f2b32-160">Autoscale notifications allow you to do three things when a scale-out or in action is successfully triggered.</span></span>
   - <span data-ttu-id="f2b32-161">Yönetici ve ortak yöneticileri aboneliğinizin bildir</span><span class="sxs-lookup"><span data-stu-id="f2b32-161">Notify the admin and co-admins of your subscription</span></span>
   - <span data-ttu-id="f2b32-162">Kullanıcı e-posta</span><span class="sxs-lookup"><span data-stu-id="f2b32-162">Email a set of users</span></span>
   - <span data-ttu-id="f2b32-163">Bir Web kancası çağrı tetikler.</span><span class="sxs-lookup"><span data-stu-id="f2b32-163">Trigger a webhook call.</span></span> <span data-ttu-id="f2b32-164">Harekete olduğunda, bu Web kancası otomatik ölçeklendirmeyi koşul hakkındaki meta verileri gönderir ve kaynak ölçek kümesi.</span><span class="sxs-lookup"><span data-stu-id="f2b32-164">When fired, this webhook sends metadata about the autoscaling condition and the scale set resource.</span></span> <span data-ttu-id="f2b32-165">Otomatik ölçeklendirme Web kancası yükü hakkında daha fazla bilgi için bkz: [yapılandırma Web kancası & otomatik ölçeklendirme için e-posta bildirimleri](insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="f2b32-165">To learn more about the payload of autoscale webhook, see [Configure Webhook & Email Notifications for Autoscale](insights-autoscale-to-webhook-email.md).</span></span>

   <span data-ttu-id="f2b32-166">Otomatik ölçeklendirme ayarı değiştirmek için aşağıdakileri ekleyin, **bildirim** öğesi değeri null</span><span class="sxs-lookup"><span data-stu-id="f2b32-166">Add the following to the Autoscale setting replacing your **notification** element whose value is null</span></span>

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

   <span data-ttu-id="f2b32-167">İsabet **Put** otomatik ölçeklendirme ayarı güncelleştirmek için kaynak Gezgininde düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f2b32-167">Hit **Put** button in Resource Explorer to update the autoscale setting.</span></span>

<span data-ttu-id="f2b32-168">Otomatik ölçeklendirme ayarında birden fazla ölçek profillerini içeren ve bildirimleri ölçeklendirmek için ayarlanmış bir VM ölçekte güncelleştirdiniz.</span><span class="sxs-lookup"><span data-stu-id="f2b32-168">You have updated an autoscale setting on a VM Scale set to include multiple scale profiles and scale notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2b32-169">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="f2b32-169">Next Steps</span></span>
<span data-ttu-id="f2b32-170">Otomatik ölçeklendirme hakkında daha fazla bilgi için bu bağlantıları kullanın.</span><span class="sxs-lookup"><span data-stu-id="f2b32-170">Use these links to learn more about autoscaling.</span></span>

[<span data-ttu-id="f2b32-171">Otomatik ölçeklendirme sanal makine ölçek kümeleri ile ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="f2b32-171">TroubleShoot Autoscale with Virtual Machine Scale Sets</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[<span data-ttu-id="f2b32-172">Otomatik ölçeklendirme için ortak ölçümleri</span><span class="sxs-lookup"><span data-stu-id="f2b32-172">Common Metrics for Autoscale</span></span>](insights-autoscale-common-metrics.md)

[<span data-ttu-id="f2b32-173">Azure otomatik ölçeklendirme için en iyi yöntemler</span><span class="sxs-lookup"><span data-stu-id="f2b32-173">Best Practices for Azure Autoscale</span></span>](insights-autoscale-best-practices.md)

[<span data-ttu-id="f2b32-174">Otomatik ölçeklendirme PowerShell kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="f2b32-174">Manage Autoscale using PowerShell</span></span>](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[<span data-ttu-id="f2b32-175">Otomatik ölçeklendirme CLI kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="f2b32-175">Manage Autoscale using CLI</span></span>](insights-cli-samples.md#autoscale)

[<span data-ttu-id="f2b32-176">Web kancası & otomatik ölçeklendirme için e-posta bildirimleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f2b32-176">Configure Webhook & Email Notifications for Autoscale</span></span>](insights-autoscale-to-webhook-email.md)
