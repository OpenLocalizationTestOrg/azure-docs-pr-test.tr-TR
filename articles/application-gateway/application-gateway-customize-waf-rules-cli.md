---
title: "Azure uygulama ağ geçidi - Azure CLI 2.0 Web uygulaması güvenlik duvarı kurallarında özelleştirme | Microsoft Docs"
description: "Bu makalede Azure CLI 2.0 ile uygulama ağ geçidi web uygulaması güvenlik duvarı kurallarında özelleştirme hakkında bilgi sağlar."
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
ms.openlocfilehash: 456be048dc2d82cd50d145b71f17a84a7189ea96
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-the-azure-cli-20"></a><span data-ttu-id="e0744-103">Web uygulaması güvenlik duvarı kuralları Azure CLI 2.0 aracılığıyla özelleştirme</span><span class="sxs-lookup"><span data-stu-id="e0744-103">Customize web application firewall rules through the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0744-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="e0744-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="e0744-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0744-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="e0744-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e0744-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="e0744-107">Azure uygulama ağ geçidi web uygulaması Güvenlik Duvarı (WAF) web uygulamaları için koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="e0744-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="e0744-108">Bu korumalar açık Web uygulaması güvenlik proje (OWASP) çekirdek kuralı ayarlayın (CR tarafından) sağlanır.</span><span class="sxs-lookup"><span data-stu-id="e0744-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="e0744-109">Bazı kurallar hatalı pozitif sonuç neden ve gerçek trafiği engelle.</span><span class="sxs-lookup"><span data-stu-id="e0744-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="e0744-110">Bu nedenle, uygulama ağ geçidi Kural gruplarını ve kurallarını özelleştirme yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="e0744-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="e0744-111">Özel kural gruplarını ve kurallarını hakkında daha fazla bilgi için bkz: [web uygulaması güvenlik duvarı CRS Kural gruplarını ve kurallarını listesi](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="e0744-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="e0744-112">Görünüm kural gruplar ve kurallar</span><span class="sxs-lookup"><span data-stu-id="e0744-112">View rule groups and rules</span></span>

<span data-ttu-id="e0744-113">Aşağıdaki kod örnekleri, kuralları ve yapılandırılabilir Kural gruplarını görüntülemek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="e0744-113">The following code examples show how to view rules and rule groups that are configurable.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="e0744-114">Kural grupları görüntüle</span><span class="sxs-lookup"><span data-stu-id="e0744-114">View rule groups</span></span>

<span data-ttu-id="e0744-115">Aşağıdaki örnek, kural gruplarını görüntülemek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="e0744-115">The following example shows how to view the rule groups:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

<span data-ttu-id="e0744-116">Önceki örnekte kesilmiş yanıttan aşağıdaki çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e0744-116">The following output is a truncated response from the preceding example:</span></span>

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

### <a name="view-rules-in-a-rule-group"></a><span data-ttu-id="e0744-117">Bir kural gruptaki kurallarını görüntüle</span><span class="sxs-lookup"><span data-stu-id="e0744-117">View rules in a rule group</span></span>

<span data-ttu-id="e0744-118">Aşağıdaki örnek, belirtilen kural gruptaki kurallarını görüntülemek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="e0744-118">The following example shows how to view rules in a specified rule group:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

<span data-ttu-id="e0744-119">Önceki örnekte kesilmiş yanıttan aşağıdaki çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e0744-119">The following output is a truncated response from the preceding example:</span></span>

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

## <a name="disable-rules"></a><span data-ttu-id="e0744-120">Kuralları devre dışı</span><span class="sxs-lookup"><span data-stu-id="e0744-120">Disable rules</span></span>

<span data-ttu-id="e0744-121">Aşağıdaki örnek kuralları devre dışı bırakır `910018` ve `910017` bir uygulama ağ geçidi üzerinde:</span><span class="sxs-lookup"><span data-stu-id="e0744-121">The following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="e0744-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e0744-122">Next steps</span></span>

<span data-ttu-id="e0744-123">Devre dışı kurallarınızı yapılandırdıktan sonra WAF günlükleri görüntülemek nasıl öğrenebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0744-123">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="e0744-124">Daha fazla bilgi için bkz: [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="e0744-124">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
