---
title: "Azure uygulama ağ geçidi - PowerShell aaaCustomize web uygulaması güvenlik duvarı kuralları | Microsoft Docs"
description: "Bu makalede, nasıl toocustomize web uygulaması güvenlik duvarı PowerShell ile uygulama ağ geçidi olarak kurallar hakkında bilgi sağlar."
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
ms.openlocfilehash: f320e687b0f621515255469dac8e375cdd900dda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-powershell"></a><span data-ttu-id="00a33-103">Web uygulaması güvenlik duvarı kuralları PowerShell aracılığıyla özelleştirme</span><span class="sxs-lookup"><span data-stu-id="00a33-103">Customize web application firewall rules through PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="00a33-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="00a33-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="00a33-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="00a33-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="00a33-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="00a33-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="00a33-107">Hello Azure uygulama ağ geçidi web uygulaması Güvenlik Duvarı (WAF) web uygulamaları için koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="00a33-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="00a33-108">Bu korumalar hello açık Web uygulaması güvenlik proje (OWASP) çekirdek kuralı ayarlayın (CR) tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="00a33-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="00a33-109">Bazı kurallar hatalı pozitif sonuç neden ve gerçek trafiği engelle.</span><span class="sxs-lookup"><span data-stu-id="00a33-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="00a33-110">Bu nedenle, uygulama ağ geçidi hello yetenek toocustomize Kural gruplarını ve kurallarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="00a33-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="00a33-111">Merhaba belirli kuralı grupları ve kuralları hakkında daha fazla bilgi için bkz: [web uygulaması güvenlik duvarı CRS Kural gruplarını ve kurallarını listesi](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="00a33-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS Rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="00a33-112">Görünüm kural gruplar ve kurallar</span><span class="sxs-lookup"><span data-stu-id="00a33-112">View rule groups and rules</span></span>

<span data-ttu-id="00a33-113">kod örnekleri aşağıdaki hello nasıl tooview kuralları ve WAF etkin uygulama ağ geçidi üzerinde yapılandırılabilir grupları kural gösterir.</span><span class="sxs-lookup"><span data-stu-id="00a33-113">hello following code examples show how tooview rules and rule groups that are configurable on a WAF-enabled application gateway.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="00a33-114">Kural grupları görüntüle</span><span class="sxs-lookup"><span data-stu-id="00a33-114">View rule groups</span></span>

<span data-ttu-id="00a33-115">örnekte gösterildiği nasıl aşağıdaki hello tooview kuralı grupları:</span><span class="sxs-lookup"><span data-stu-id="00a33-115">hello following example shows how tooview rule groups:</span></span>

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

<span data-ttu-id="00a33-116">Çıktı aşağıdaki hello örnek önceki hello kesilmiş yanıttan şöyledir:</span><span class="sxs-lookup"><span data-stu-id="00a33-116">hello following output is a truncated response from hello preceding example:</span></span>

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

## <a name="disable-rules"></a><span data-ttu-id="00a33-117">Kuralları devre dışı</span><span class="sxs-lookup"><span data-stu-id="00a33-117">Disable rules</span></span>

<span data-ttu-id="00a33-118">Merhaba aşağıdaki örnek kuralları devre dışı bırakır `910018` ve `910017` bir uygulama ağ geçidi üzerinde:</span><span class="sxs-lookup"><span data-stu-id="00a33-118">hello following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="00a33-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="00a33-119">Next steps</span></span>

<span data-ttu-id="00a33-120">Devre dışı kurallarınızı yapılandırdıktan sonra öğrenebilirsiniz nasıl tooview WAF günlüklerinizi.</span><span class="sxs-lookup"><span data-stu-id="00a33-120">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="00a33-121">Daha fazla bilgi için bkz: [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="00a33-121">For more information, see [Application Gateway Diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
