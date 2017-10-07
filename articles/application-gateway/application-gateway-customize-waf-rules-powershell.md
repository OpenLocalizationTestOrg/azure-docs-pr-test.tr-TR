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
# <a name="customize-web-application-firewall-rules-through-powershell"></a>Web uygulaması güvenlik duvarı kuralları PowerShell aracılığıyla özelleştirme

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md)

Hello Azure uygulama ağ geçidi web uygulaması Güvenlik Duvarı (WAF) web uygulamaları için koruma sağlar. Bu korumalar hello açık Web uygulaması güvenlik proje (OWASP) çekirdek kuralı ayarlayın (CR) tarafından sağlanır. Bazı kurallar hatalı pozitif sonuç neden ve gerçek trafiği engelle. Bu nedenle, uygulama ağ geçidi hello yetenek toocustomize Kural gruplarını ve kurallarını sağlar. Merhaba belirli kuralı grupları ve kuralları hakkında daha fazla bilgi için bkz: [web uygulaması güvenlik duvarı CRS Kural gruplarını ve kurallarını listesi](application-gateway-crs-rulegroups-rules.md).

## <a name="view-rule-groups-and-rules"></a>Görünüm kural gruplar ve kurallar

kod örnekleri aşağıdaki hello nasıl tooview kuralları ve WAF etkin uygulama ağ geçidi üzerinde yapılandırılabilir grupları kural gösterir.

### <a name="view-rule-groups"></a>Kural grupları görüntüle

örnekte gösterildiği nasıl aşağıdaki hello tooview kuralı grupları:

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

Çıktı aşağıdaki hello örnek önceki hello kesilmiş yanıttan şöyledir:

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

## <a name="disable-rules"></a>Kuralları devre dışı

Merhaba aşağıdaki örnek kuralları devre dışı bırakır `910018` ve `910017` bir uygulama ağ geçidi üzerinde:

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a>Sonraki adımlar

Devre dışı kurallarınızı yapılandırdıktan sonra öğrenebilirsiniz nasıl tooview WAF günlüklerinizi. Daha fazla bilgi için bkz: [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
