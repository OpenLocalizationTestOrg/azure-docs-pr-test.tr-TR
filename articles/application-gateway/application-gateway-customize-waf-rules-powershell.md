---
title: "Azure uygulama ağ geçidi - PowerShell Web uygulaması güvenlik duvarı kurallarında özelleştirme | Microsoft Docs"
description: "Bu makalede PowerShell ile uygulama ağ geçidi web uygulaması güvenlik duvarı kurallarında özelleştirme hakkında bilgi sağlar."
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
ms.openlocfilehash: 681625e40035b05c593c6161236cb80b7db576b9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-powershell"></a><span data-ttu-id="43bb6-103">Web uygulaması güvenlik duvarı kuralları PowerShell aracılığıyla özelleştirme</span><span class="sxs-lookup"><span data-stu-id="43bb6-103">Customize web application firewall rules through PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="43bb6-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="43bb6-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="43bb6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="43bb6-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="43bb6-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="43bb6-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="43bb6-107">Azure uygulama ağ geçidi web uygulaması Güvenlik Duvarı (WAF) web uygulamaları için koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="43bb6-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="43bb6-108">Bu korumalar açık Web uygulaması güvenlik proje (OWASP) çekirdek kuralı ayarlayın (CR tarafından) sağlanır.</span><span class="sxs-lookup"><span data-stu-id="43bb6-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="43bb6-109">Bazı kurallar hatalı pozitif sonuç neden ve gerçek trafiği engelle.</span><span class="sxs-lookup"><span data-stu-id="43bb6-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="43bb6-110">Bu nedenle, uygulama ağ geçidi Kural gruplarını ve kurallarını özelleştirme yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="43bb6-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="43bb6-111">Özel kural gruplarını ve kurallarını hakkında daha fazla bilgi için bkz: [web uygulaması güvenlik duvarı CRS Kural gruplarını ve kurallarını listesi](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="43bb6-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS Rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="43bb6-112">Görünüm kural gruplar ve kurallar</span><span class="sxs-lookup"><span data-stu-id="43bb6-112">View rule groups and rules</span></span>

<span data-ttu-id="43bb6-113">Aşağıdaki kod örnekleri, kuralları ve WAF etkin uygulama ağ geçidi üzerinde yapılandırılabilir Kural gruplarını görüntülemek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="43bb6-113">The following code examples show how to view rules and rule groups that are configurable on a WAF-enabled application gateway.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="43bb6-114">Kural grupları görüntüle</span><span class="sxs-lookup"><span data-stu-id="43bb6-114">View rule groups</span></span>

<span data-ttu-id="43bb6-115">Aşağıdaki örnek, kural gruplarını görüntülemek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="43bb6-115">The following example shows how to view rule groups:</span></span>

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

<span data-ttu-id="43bb6-116">Önceki örnekte kesilmiş yanıttan aşağıdaki çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="43bb6-116">The following output is a truncated response from the preceding example:</span></span>

```
OWASP (Ver. 3.0):

    REQUEST-910-IP-REPUTATION:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            910011     Rule 910011
            910012     Rule 910012
            ...        ...

    REQUEST-911-METHOD-ENFORCEMENT:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            911011     Rule 911011
            ...        ...

OWASP (Ver. 2.2.9):

    crs_20_protocol_violations:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            960911     Invalid HTTP Request Line
            981227     Apache Error: Invalid URI in Request.
            960000     Attempted multipart/form-data bypass
            ...        ...
```

## <a name="disable-rules"></a><span data-ttu-id="43bb6-117">Kuralları devre dışı</span><span class="sxs-lookup"><span data-stu-id="43bb6-117">Disable rules</span></span>

<span data-ttu-id="43bb6-118">Aşağıdaki örnek kuralları devre dışı bırakır `910018` ve `910017` bir uygulama ağ geçidi üzerinde:</span><span class="sxs-lookup"><span data-stu-id="43bb6-118">The following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="43bb6-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="43bb6-119">Next steps</span></span>

<span data-ttu-id="43bb6-120">Devre dışı kurallarınızı yapılandırdıktan sonra WAF günlükleri görüntülemek nasıl öğrenebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43bb6-120">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="43bb6-121">Daha fazla bilgi için bkz: [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="43bb6-121">For more information, see [Application Gateway Diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
