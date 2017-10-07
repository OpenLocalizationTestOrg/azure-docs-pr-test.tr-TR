---
title: "Azure uygulama ağ geçidi - Azure CLI 2.0 aaaCustomize web uygulaması güvenlik duvarı kuralları | Microsoft Docs"
description: "Bu makalede, nasıl toocustomize web uygulaması güvenlik duvarı uygulama ağ geçidi'nde hello Azure CLI 2.0 ile kurallar hakkında bilgi sağlar."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: b83ffb9f6a7e0d0c8c970885d2bcb3b63d32581c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-cli-20"></a>Web uygulaması güvenlik duvarı kuralları hello Azure CLI 2.0 aracılığıyla özelleştirme

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md)

Hello Azure uygulama ağ geçidi web uygulaması Güvenlik Duvarı (WAF) web uygulamaları için koruma sağlar. Bu korumalar hello açık Web uygulaması güvenlik proje (OWASP) çekirdek kuralı ayarlayın (CR) tarafından sağlanır. Bazı kurallar hatalı pozitif sonuç neden ve gerçek trafiği engelle. Bu nedenle, uygulama ağ geçidi hello yetenek toocustomize Kural gruplarını ve kurallarını sağlar. Merhaba belirli kuralı grupları ve kuralları hakkında daha fazla bilgi için bkz: [web uygulaması güvenlik duvarı CRS Kural gruplarını ve kurallarını listesi](application-gateway-crs-rulegroups-rules.md).

## <a name="view-rule-groups-and-rules"></a>Görünüm kural gruplar ve kurallar

kod örnekleri aşağıdaki hello nasıl tooview kurallar ve kural yapılandırılabilir grupları göster.

### <a name="view-rule-groups"></a>Kural grupları görüntüle

Aşağıdaki örneğine hello nasıl tooview hello Kural gruplarını gösterir:

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

Çıktı aşağıdaki hello örnek önceki hello kesilmiş yanıttan şöyledir:

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  },
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_2.2.9",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
   "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "crs_20_protocol_violations",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "2.2.9",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

### <a name="view-rules-in-a-rule-group"></a>Bir kural gruptaki kurallarını görüntüle

Aşağıdaki örneğine hello nasıl tooview belirtilen kural grubunda kurallar gösterir:

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

Çıktı aşağıdaki hello örnek önceki hello kesilmiş yanıttan şöyledir:

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": [
          {
            "description": "Rule 910011",
            "ruleId": 910011
          },
          ...
        ]
      }
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

## <a name="disable-rules"></a>Kuralları devre dışı

Merhaba aşağıdaki örnek kuralları devre dışı bırakır `910018` ve `910017` bir uygulama ağ geçidi üzerinde:

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a>Sonraki adımlar

Devre dışı kurallarınızı yapılandırdıktan sonra öğrenebilirsiniz nasıl tooview WAF günlüklerinizi. Daha fazla bilgi için bkz: [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
