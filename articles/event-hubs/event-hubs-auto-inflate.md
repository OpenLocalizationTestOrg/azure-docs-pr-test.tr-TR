---
title: "Azure Event Hubs üretilen iş birimleri aaaAutomatically ölçek | Microsoft Docs"
description: "Bir ad alanı tooautomatically ölçekte üretilen iş birimleri otomatik Şişir etkinleştir"
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
ms.openlocfilehash: 0f5216bcd619ccddc1fd4063a2f0131bfa36c7d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a><span data-ttu-id="38e96-103">Azure Event Hubs üretilen iş birimleri otomatik olarak ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="38e96-103">Automatically scale up Azure Event Hubs throughput units</span></span>

## <a name="overview"></a><span data-ttu-id="38e96-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="38e96-104">Overview</span></span>

<span data-ttu-id="38e96-105">Azure Event Hubs platform akış yüksek düzeyde ölçeklenebilir bir veridir.</span><span class="sxs-lookup"><span data-stu-id="38e96-105">Azure Event Hubs is a highly scalable data streaming platform.</span></span> <span data-ttu-id="38e96-106">Bu nedenle, Event Hubs müşteriler ekleme toohello hizmeti yeniden kullanımı genellikle artırın.</span><span class="sxs-lookup"><span data-stu-id="38e96-106">As such, Event Hubs customers often increase their usage after onboarding toohello service.</span></span> <span data-ttu-id="38e96-107">Böyle artar ve büyük aktarımı hızlarını işleyebilme artan önceden hello üretilen iş birimleri (TUs) tooscale olay hub'ları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="38e96-107">Such increases require increasing hello predetermined throughput units (TUs) tooscale Event Hubs and handle larger transfer rates.</span></span> <span data-ttu-id="38e96-108">Merhaba *otomatik Şişir* olay hub'larını özelliği TUs toomeet kullanımı ihtiyaçları hello sayısı otomatik olarak ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="38e96-108">hello *Auto-inflate* feature of Event Hubs automatically scales up hello number of TUs toomeet usage needs.</span></span> <span data-ttu-id="38e96-109">TUs artırma engeller senaryoları, azaltma:</span><span class="sxs-lookup"><span data-stu-id="38e96-109">Increasing TUs prevents throttling scenarios, in which:</span></span>

* <span data-ttu-id="38e96-110">Oranları aşan veri giriş TUs ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="38e96-110">Data ingress rates exceed set TUs.</span></span>
* <span data-ttu-id="38e96-111">Oranları aşan veri çıkışı isteği TUs ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="38e96-111">Data egress request rates exceed set TUs.</span></span>

## <a name="how-auto-inflate-works"></a><span data-ttu-id="38e96-112">Otomatik Şişir nasıl çalışır</span><span class="sxs-lookup"><span data-stu-id="38e96-112">How Auto-inflate works</span></span>

<span data-ttu-id="38e96-113">Olay hub'ları trafiği işleme birimleri tarafından denetlenir.</span><span class="sxs-lookup"><span data-stu-id="38e96-113">Event Hubs traffic is controlled by throughput units.</span></span> <span data-ttu-id="38e96-114">Tek bir TU; giriş ve çıkış miktarı iki kez saniyede 1 MB sağlar.</span><span class="sxs-lookup"><span data-stu-id="38e96-114">A single TU allows 1 MB per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="38e96-115">Standart olay hub'ları 1-20 işleme birimleri ile yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="38e96-115">Standard Event Hubs can be configured with 1-20 throughput units.</span></span> <span data-ttu-id="38e96-116">Otomatik Şişir sağlar, toostart hello en düşük gerekli işleme birimleri ile küçük.</span><span class="sxs-lookup"><span data-stu-id="38e96-116">Auto-inflate enables you toostart small with hello minimum required throughput units.</span></span> <span data-ttu-id="38e96-117">Merhaba özelliği sonra toohello sınırı trafiğinizi hello artış bağlı olarak, gerek üretilen iş birimleri otomatik olarak ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="38e96-117">hello feature then scales automatically toohello maximum limit of throughput units you need, depending on hello increase in your traffic.</span></span> <span data-ttu-id="38e96-118">Otomatik Şişir hello aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="38e96-118">Auto-inflate provides hello following benefits:</span></span>

- <span data-ttu-id="38e96-119">Verimli ölçeklendirme mekanizması toostart küçük ve ölçek büyütme olarak artar.</span><span class="sxs-lookup"><span data-stu-id="38e96-119">An efficient scaling mechanism toostart small and scale up as you grow.</span></span>
- <span data-ttu-id="38e96-120">Toohello belirtilen üst sınır azaltma bir sorun olmadan otomatik olarak ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="38e96-120">Automatically scale toohello specified upper limit without throttling issues.</span></span>
- <span data-ttu-id="38e96-121">Daha fazla denetim ölçekleme üzerinde ne zaman denetimi olarak ve ne kadar tooscale.</span><span class="sxs-lookup"><span data-stu-id="38e96-121">More control over scaling, as you control when and how much tooscale.</span></span>

## <a name="enable-auto-inflate-on-a-namespace"></a><span data-ttu-id="38e96-122">Bir ad otomatik Şişir etkinleştir</span><span class="sxs-lookup"><span data-stu-id="38e96-122">Enable Auto-inflate on a namespace</span></span>

<span data-ttu-id="38e96-123">Etkinleştirmek veya otomatik Şişir yöntemler aşağıdaki hello birini kullanarak bir ad alanı üzerinde devre dışı bırakabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="38e96-123">You can enable or disable Auto-inflate on a namespace using either of hello following methods:</span></span>

1. <span data-ttu-id="38e96-124">Merhaba [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="38e96-124">hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="38e96-125">Bir Azure Resource Manager şablonu.</span><span class="sxs-lookup"><span data-stu-id="38e96-125">An Azure Resource Manager template.</span></span>

### <a name="enable-auto-inflate-through-hello-portal"></a><span data-ttu-id="38e96-126">Otomatik Şişir hello portal üzerinden etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="38e96-126">Enable Auto-inflate through hello portal</span></span>

<span data-ttu-id="38e96-127">Bir olay hub'ları ad alanı oluştururken, bir ad alanı hello otomatik Şişir özelliğini etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="38e96-127">You can enable hello Auto-inflate feature on a namespace when creating an Event Hubs namespace:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

<span data-ttu-id="38e96-128">Bu seçeneği etkinleştirdiğinizde, üretilen iş birimleri küçük başlayın ve kullanımınızı artış gerektiği ölçeği.</span><span class="sxs-lookup"><span data-stu-id="38e96-128">With this option enabled, you can start small on your throughput units and scale up as your usage needs increase.</span></span> <span data-ttu-id="38e96-129">Merhaba Enflasyon için üst sınır fiyatlandırma, saat başına kullanılan TUs hello sayısına bağlı olan etkilemez.</span><span class="sxs-lookup"><span data-stu-id="38e96-129">hello upper limit for inflation does not affect pricing, which depends on hello number of TUs used per hour.</span></span>

<span data-ttu-id="38e96-130">Otomatik Şişir etkinleştirebilirsiniz hello kullanarak **ölçek** hello ayarları dikey penceresinde hello portal seçeneği:</span><span class="sxs-lookup"><span data-stu-id="38e96-130">You can also enable Auto-inflate using hello **Scale** option on hello settings blade in hello portal:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a><span data-ttu-id="38e96-131">Bir Azure Resource Manager şablonu kullanarak otomatik Şişir etkinleştir</span><span class="sxs-lookup"><span data-stu-id="38e96-131">Enable Auto-Inflate using an Azure Resource Manager template</span></span>

<span data-ttu-id="38e96-132">Bir Azure Resource Manager şablon dağıtımı sırasında otomatik Şişir etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38e96-132">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="38e96-133">Örneğin, kümesi hello `isAutoInflateEnabled` özelliği çok**true** ve `maximumThroughputUnits` too10.</span><span class="sxs-lookup"><span data-stu-id="38e96-133">For example, set hello `isAutoInflateEnabled` property too**true** and set `maximumThroughputUnits` too10.</span></span>

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

<span data-ttu-id="38e96-134">Merhaba Hello tam şablonu için bkz [olay hub'ı oluşturma ad alanı ve Şişir etkinleştir](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) şablonunu github'dan edinilebilir.</span><span class="sxs-lookup"><span data-stu-id="38e96-134">For hello complete template, see hello [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38e96-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="38e96-135">Next steps</span></span>

<span data-ttu-id="38e96-136">Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="38e96-136">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="38e96-137">Event Hubs’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="38e96-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="38e96-138">Olay Hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="38e96-138">Create an Event Hub</span></span>](event-hubs-create.md)
