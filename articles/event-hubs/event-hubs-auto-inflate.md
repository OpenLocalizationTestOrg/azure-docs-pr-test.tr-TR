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
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a>Azure Event Hubs üretilen iş birimleri otomatik olarak ölçeklendirin

## <a name="overview"></a>Genel Bakış

Azure Event Hubs platform akış yüksek düzeyde ölçeklenebilir bir veridir. Bu nedenle, Event Hubs müşteriler ekleme toohello hizmeti yeniden kullanımı genellikle artırın. Böyle artar ve büyük aktarımı hızlarını işleyebilme artan önceden hello üretilen iş birimleri (TUs) tooscale olay hub'ları gerektirir. Merhaba *otomatik Şişir* olay hub'larını özelliği TUs toomeet kullanımı ihtiyaçları hello sayısı otomatik olarak ölçeklendirir. TUs artırma engeller senaryoları, azaltma:

* Oranları aşan veri giriş TUs ayarlayın.
* Oranları aşan veri çıkışı isteği TUs ayarlayın.

## <a name="how-auto-inflate-works"></a>Otomatik Şişir nasıl çalışır

Olay hub'ları trafiği işleme birimleri tarafından denetlenir. Tek bir TU; giriş ve çıkış miktarı iki kez saniyede 1 MB sağlar. Standart olay hub'ları 1-20 işleme birimleri ile yapılandırılabilir. Otomatik Şişir sağlar, toostart hello en düşük gerekli işleme birimleri ile küçük. Merhaba özelliği sonra toohello sınırı trafiğinizi hello artış bağlı olarak, gerek üretilen iş birimleri otomatik olarak ölçeklendirir. Otomatik Şişir hello aşağıdaki avantajları sağlar:

- Verimli ölçeklendirme mekanizması toostart küçük ve ölçek büyütme olarak artar.
- Toohello belirtilen üst sınır azaltma bir sorun olmadan otomatik olarak ölçeklendirin.
- Daha fazla denetim ölçekleme üzerinde ne zaman denetimi olarak ve ne kadar tooscale.

## <a name="enable-auto-inflate-on-a-namespace"></a>Bir ad otomatik Şişir etkinleştir

Etkinleştirmek veya otomatik Şişir yöntemler aşağıdaki hello birini kullanarak bir ad alanı üzerinde devre dışı bırakabilirsiniz:

1. Merhaba [Azure portal](https://portal.azure.com).
2. Bir Azure Resource Manager şablonu.

### <a name="enable-auto-inflate-through-hello-portal"></a>Otomatik Şişir hello portal üzerinden etkinleştirme

Bir olay hub'ları ad alanı oluştururken, bir ad alanı hello otomatik Şişir özelliğini etkinleştirebilirsiniz:
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

Bu seçeneği etkinleştirdiğinizde, üretilen iş birimleri küçük başlayın ve kullanımınızı artış gerektiği ölçeği. Merhaba Enflasyon için üst sınır fiyatlandırma, saat başına kullanılan TUs hello sayısına bağlı olan etkilemez.

Otomatik Şişir etkinleştirebilirsiniz hello kullanarak **ölçek** hello ayarları dikey penceresinde hello portal seçeneği:
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a>Bir Azure Resource Manager şablonu kullanarak otomatik Şişir etkinleştir

Bir Azure Resource Manager şablon dağıtımı sırasında otomatik Şişir etkinleştirebilirsiniz. Örneğin, kümesi hello `isAutoInflateEnabled` özelliği çok**true** ve `maximumThroughputUnits` too10.

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

Merhaba Hello tam şablonu için bkz [olay hub'ı oluşturma ad alanı ve Şişir etkinleştir](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) şablonunu github'dan edinilebilir.

## <a name="next-steps"></a>Sonraki adımlar

Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:

* [Event Hubs’a genel bakış](event-hubs-what-is-event-hubs.md)
* [Olay Hub’ı oluşturma](event-hubs-create.md)
