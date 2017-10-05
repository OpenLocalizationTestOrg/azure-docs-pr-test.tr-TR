---
title: "Azure Event Hubs üretilen iş birimleri otomatik olarak ölçeklendirin | Microsoft Docs"
description: "Otomatik olarak üretilen iş birimleri ölçeklendirmek için bir ad alanında otomatik Şişir etkinleştir"
services: event-hubs
documentationcenter: na
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: shvija;sethm
ms.openlocfilehash: b085091ea7bfd601efb0eee84144ddd091422d6e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a><span data-ttu-id="c017b-103">Azure Event Hubs üretilen iş birimleri otomatik olarak ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="c017b-103">Automatically scale up Azure Event Hubs throughput units</span></span>

## <a name="overview"></a><span data-ttu-id="c017b-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c017b-104">Overview</span></span>

<span data-ttu-id="c017b-105">Azure Event Hubs platform akış yüksek düzeyde ölçeklenebilir bir veridir.</span><span class="sxs-lookup"><span data-stu-id="c017b-105">Azure Event Hubs is a highly scalable data streaming platform.</span></span> <span data-ttu-id="c017b-106">Bu nedenle, Event Hubs müşteriler genellikle kullanımları hizmetine ekleme sonra artırın.</span><span class="sxs-lookup"><span data-stu-id="c017b-106">As such, Event Hubs customers often increase their usage after onboarding to the service.</span></span> <span data-ttu-id="c017b-107">Bu tür artar önceden belirlenmiş üretilen iş birimleri (olay hub'ları ölçeklendirme ve daha büyük aktarım hızlarıyla işlemek için TUs) artırma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c017b-107">Such increases require increasing the predetermined throughput units (TUs) to scale Event Hubs and handle larger transfer rates.</span></span> <span data-ttu-id="c017b-108">*Otomatik Şişir* olay hub'larını özelliği kullanım gereksinimlerini karşılamak için TUs numarayı oluşturan otomatik olarak ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="c017b-108">The *Auto-inflate* feature of Event Hubs automatically scales up the number of TUs to meet usage needs.</span></span> <span data-ttu-id="c017b-109">TUs artırma engeller senaryoları, azaltma:</span><span class="sxs-lookup"><span data-stu-id="c017b-109">Increasing TUs prevents throttling scenarios, in which:</span></span>

* <span data-ttu-id="c017b-110">Oranları aşan veri giriş TUs ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c017b-110">Data ingress rates exceed set TUs.</span></span>
* <span data-ttu-id="c017b-111">Oranları aşan veri çıkışı isteği TUs ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c017b-111">Data egress request rates exceed set TUs.</span></span>

## <a name="how-auto-inflate-works"></a><span data-ttu-id="c017b-112">Otomatik Şişir nasıl çalışır</span><span class="sxs-lookup"><span data-stu-id="c017b-112">How Auto-inflate works</span></span>

<span data-ttu-id="c017b-113">Olay hub'ları trafiği işleme birimleri tarafından denetlenir.</span><span class="sxs-lookup"><span data-stu-id="c017b-113">Event Hubs traffic is controlled by throughput units.</span></span> <span data-ttu-id="c017b-114">Tek bir TU; giriş ve çıkış miktarı iki kez saniyede 1 MB sağlar.</span><span class="sxs-lookup"><span data-stu-id="c017b-114">A single TU allows 1 MB per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="c017b-115">Standart olay hub'ları 1-20 işleme birimleri ile yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="c017b-115">Standard Event Hubs can be configured with 1-20 throughput units.</span></span> <span data-ttu-id="c017b-116">Otomatik Şişir en düşük gerekli işleme birimleri ile küçük Başlat olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="c017b-116">Auto-inflate enables you to start small with the minimum required throughput units.</span></span> <span data-ttu-id="c017b-117">Özellik sonra otomatik olarak üretilen iş birimleri trafiğinizi artış bağlı olarak, gereken maksimum sınırı ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="c017b-117">The feature then scales automatically to the maximum limit of throughput units you need, depending on the increase in your traffic.</span></span> <span data-ttu-id="c017b-118">Otomatik Şişir aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="c017b-118">Auto-inflate provides the following benefits:</span></span>

- <span data-ttu-id="c017b-119">Küçük başlayın ve büyüdükçe ölçeği için verimli bir ölçeklendirme mekanizması.</span><span class="sxs-lookup"><span data-stu-id="c017b-119">An efficient scaling mechanism to start small and scale up as you grow.</span></span>
- <span data-ttu-id="c017b-120">Otomatik olarak belirtilen üst sınıra sorunları azaltma olmadan ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="c017b-120">Automatically scale to the specified upper limit without throttling issues.</span></span>
- <span data-ttu-id="c017b-121">Daha fazla ölçeklendirme üzerinden ne zaman denetimi olarak ve ölçek için ne kadar denetler.</span><span class="sxs-lookup"><span data-stu-id="c017b-121">More control over scaling, as you control when and how much to scale.</span></span>

## <a name="enable-auto-inflate-on-a-namespace"></a><span data-ttu-id="c017b-122">Bir ad otomatik Şişir etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c017b-122">Enable Auto-inflate on a namespace</span></span>

<span data-ttu-id="c017b-123">Etkinleştirmek veya otomatik Şişir aşağıdaki yöntemlerden birini kullanarak bir ad üzerinde devre dışı bırakabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c017b-123">You can enable or disable Auto-inflate on a namespace using either of the following methods:</span></span>

1. <span data-ttu-id="c017b-124">[Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c017b-124">The [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c017b-125">Bir Azure Resource Manager şablonu.</span><span class="sxs-lookup"><span data-stu-id="c017b-125">An Azure Resource Manager template.</span></span>

### <a name="enable-auto-inflate-through-the-portal"></a><span data-ttu-id="c017b-126">Portal etkinleştirme otomatik Şişir</span><span class="sxs-lookup"><span data-stu-id="c017b-126">Enable Auto-inflate through the portal</span></span>

<span data-ttu-id="c017b-127">Bir olay hub'ları ad alanı oluştururken bir ad alanı otomatik Şişir özelliğini etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c017b-127">You can enable the Auto-inflate feature on a namespace when creating an Event Hubs namespace:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

<span data-ttu-id="c017b-128">Bu seçeneği etkinleştirdiğinizde, üretilen iş birimleri küçük başlayın ve kullanımınızı artış gerektiği ölçeği.</span><span class="sxs-lookup"><span data-stu-id="c017b-128">With this option enabled, you can start small on your throughput units and scale up as your usage needs increase.</span></span> <span data-ttu-id="c017b-129">Enflasyon için üst sınır fiyatlandırma, saat başına kullanılan TUs sayısına bağlı olan etkilemez.</span><span class="sxs-lookup"><span data-stu-id="c017b-129">The upper limit for inflation does not affect pricing, which depends on the number of TUs used per hour.</span></span>

<span data-ttu-id="c017b-130">Otomatik Şişir-kullanarak da etkinleştirebilirsiniz **ölçek** seçeneği ayarlar dikey penceresinde Portalı'nda:</span><span class="sxs-lookup"><span data-stu-id="c017b-130">You can also enable Auto-inflate using the **Scale** option on the settings blade in the portal:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a><span data-ttu-id="c017b-131">Bir Azure Resource Manager şablonu kullanarak otomatik Şişir etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c017b-131">Enable Auto-Inflate using an Azure Resource Manager template</span></span>

<span data-ttu-id="c017b-132">Bir Azure Resource Manager şablon dağıtımı sırasında otomatik Şişir etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c017b-132">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="c017b-133">Örneğin, `isAutoInflateEnabled` özelliğine **true** ve `maximumThroughputUnits` 10.</span><span class="sxs-lookup"><span data-stu-id="c017b-133">For example, set the `isAutoInflateEnabled` property to **true** and set `maximumThroughputUnits` to 10.</span></span>

```json
"resources": [
        {
            "apiVersion": "2017-04-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "properties": {
                "isAutoInflateEnabled": true,
                "maximumThroughputUnits": 10
            },
            "resources": [
                {
                    "apiVersion": "2017-04-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {},
                    "resources": [
                        {
                            "apiVersion": "2017-04-01",
                            "name": "[parameters('consumerGroupName')]",
                            "type": "ConsumerGroups",
                            "dependsOn": [
                                "[parameters('eventHubName')]"
                            ],
                            "properties": {}
                        }
                    ]
                }
            ]
        }
    ]
```

<span data-ttu-id="c017b-134">Tam şablon için bkz: [olay hub'ı oluşturma ad alanı ve Şişir etkinleştir](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) github'da şablonu.</span><span class="sxs-lookup"><span data-stu-id="c017b-134">For the complete template, see the [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c017b-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c017b-135">Next steps</span></span>

<span data-ttu-id="c017b-136">Aşağıdaki bağlantıları inceleyerek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c017b-136">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="c017b-137">Event Hubs’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="c017b-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="c017b-138">Olay Hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c017b-138">Create an Event Hub</span></span>](event-hubs-create.md)
