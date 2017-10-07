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
# <a name="customize-web-application-firewall-rules-through-hello-azure-cli-20"></a><span data-ttu-id="5c47b-103">Web uygulaması güvenlik duvarı kuralları hello Azure CLI 2.0 aracılığıyla özelleştirme</span><span class="sxs-lookup"><span data-stu-id="5c47b-103">Customize web application firewall rules through hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5c47b-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="5c47b-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="5c47b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c47b-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="5c47b-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5c47b-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="5c47b-107">Hello Azure uygulama ağ geçidi web uygulaması Güvenlik Duvarı (WAF) web uygulamaları için koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="5c47b-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="5c47b-108">Bu korumalar hello açık Web uygulaması güvenlik proje (OWASP) çekirdek kuralı ayarlayın (CR) tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="5c47b-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="5c47b-109">Bazı kurallar hatalı pozitif sonuç neden ve gerçek trafiği engelle.</span><span class="sxs-lookup"><span data-stu-id="5c47b-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="5c47b-110">Bu nedenle, uygulama ağ geçidi hello yetenek toocustomize Kural gruplarını ve kurallarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="5c47b-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="5c47b-111">Merhaba belirli kuralı grupları ve kuralları hakkında daha fazla bilgi için bkz: [web uygulaması güvenlik duvarı CRS Kural gruplarını ve kurallarını listesi](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="5c47b-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="5c47b-112">Görünüm kural gruplar ve kurallar</span><span class="sxs-lookup"><span data-stu-id="5c47b-112">View rule groups and rules</span></span>

<span data-ttu-id="5c47b-113">kod örnekleri aşağıdaki hello nasıl tooview kurallar ve kural yapılandırılabilir grupları göster.</span><span class="sxs-lookup"><span data-stu-id="5c47b-113">hello following code examples show how tooview rules and rule groups that are configurable.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="5c47b-114">Kural grupları görüntüle</span><span class="sxs-lookup"><span data-stu-id="5c47b-114">View rule groups</span></span>

<span data-ttu-id="5c47b-115">Aşağıdaki örneğine hello nasıl tooview hello Kural gruplarını gösterir:</span><span class="sxs-lookup"><span data-stu-id="5c47b-115">hello following example shows how tooview hello rule groups:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

<span data-ttu-id="5c47b-116">Çıktı aşağıdaki hello örnek önceki hello kesilmiş yanıttan şöyledir:</span><span class="sxs-lookup"><span data-stu-id="5c47b-116">hello following output is a truncated response from hello preceding example:</span></span>

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

### <a name="view-rules-in-a-rule-group"></a><span data-ttu-id="5c47b-117">Bir kural gruptaki kurallarını görüntüle</span><span class="sxs-lookup"><span data-stu-id="5c47b-117">View rules in a rule group</span></span>

<span data-ttu-id="5c47b-118">Aşağıdaki örneğine hello nasıl tooview belirtilen kural grubunda kurallar gösterir:</span><span class="sxs-lookup"><span data-stu-id="5c47b-118">hello following example shows how tooview rules in a specified rule group:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

<span data-ttu-id="5c47b-119">Çıktı aşağıdaki hello örnek önceki hello kesilmiş yanıttan şöyledir:</span><span class="sxs-lookup"><span data-stu-id="5c47b-119">hello following output is a truncated response from hello preceding example:</span></span>

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

## <a name="disable-rules"></a><span data-ttu-id="5c47b-120">Kuralları devre dışı</span><span class="sxs-lookup"><span data-stu-id="5c47b-120">Disable rules</span></span>

<span data-ttu-id="5c47b-121">Merhaba aşağıdaki örnek kuralları devre dışı bırakır `910018` ve `910017` bir uygulama ağ geçidi üzerinde:</span><span class="sxs-lookup"><span data-stu-id="5c47b-121">hello following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="5c47b-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5c47b-122">Next steps</span></span>

<span data-ttu-id="5c47b-123">Devre dışı kurallarınızı yapılandırdıktan sonra öğrenebilirsiniz nasıl tooview WAF günlüklerinizi.</span><span class="sxs-lookup"><span data-stu-id="5c47b-123">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="5c47b-124">Daha fazla bilgi için bkz: [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="5c47b-124">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
