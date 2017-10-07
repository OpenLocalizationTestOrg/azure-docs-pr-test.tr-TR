---
title: "aaaCustomize web uygulaması güvenlik duvarı kuralları Azure uygulama ağ geçidi - Azure portalı | Microsoft Docs"
description: "Bu makalede, nasıl toocustomize web uygulaması güvenlik duvarı uygulama ağ geçidi'nde hello Azure portal ile kurallar hakkında bilgi sağlar."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 1159500b-17ba-41e7-88d6-b96986795084
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: gwallace
ms.openlocfilehash: 36a999279e0370b9f803e12257856a56753b23a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-portal"></a>Web uygulaması güvenlik duvarı kuralları hello Azure portal aracılığıyla özelleştirme

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md)

Hello Azure uygulama ağ geçidi web uygulaması Güvenlik Duvarı (WAF) web uygulamaları için koruma sağlar. Bu korumalar hello açık Web uygulaması güvenlik proje (OWASP) çekirdek kuralı ayarlayın (CR) tarafından sağlanır. Bazı kurallar hatalı pozitif sonuç neden ve gerçek trafiği engelle. Bu nedenle, uygulama ağ geçidi hello yetenek toocustomize Kural gruplarını ve kurallarını sağlar. Merhaba belirli kuralı grupları ve kuralları hakkında daha fazla bilgi için bkz: [web uygulaması güvenlik duvarı CRS Kural gruplarını ve kurallarını listesi](application-gateway-crs-rulegroups-rules.md).

>[!NOTE]
> Uygulama ağ geçidiniz hello WAF katmanı kullanmıyorsa hello seçeneği tooupgrade hello uygulama ağ geçidi toohello WAF katmanı hello sağ bölmede görüntülenir. 

![WAF etkinleştir][fig1]

## <a name="view-rule-groups-and-rules"></a>Görünüm kural gruplar ve kurallar

**tooview kural gruplar ve kurallar**
   1. Toohello uygulama ağ geçidi göz atın ve ardından **Web uygulaması güvenlik duvarı**.  
   2. Seçin **Gelişmiş kural yapılandırmasını**.  
   Bu görünüm, kural kümesi seçilen hello ile sağlanan tüm hello Kural gruplarını hello sayfasında bir tablo gösterir. Tüm hello kuralın onay kutularını seçilir.

![Devre dışı kurallarını yapılandırma][1]

## <a name="search-for-rules-toodisable"></a>Kuralları toodisable arayın

Merhaba **Web uygulaması güvenlik duvarı ayarlarını** dikey metin arama toofilter hello kurallarla hello yeteneği sağlar. Hello sonucu yalnızca hello kuralı grupları ve aradığınız hello metin içeren kurallarını görüntüler.

![Kuralları arayın][2]

## <a name="disable-rule-groups-and-rules"></a>Kural gruplarını ve kurallarını devre dışı bırak

Olduğunda, olduğunuz kuralları devre dışı bırakma, tüm kural grubu veya bir veya daha fazla kural grubu altında belirli kurallar devre dışı bırakabilirsiniz. 

**toodisable kuralı grupları veya belirli kurallar**

   1. Merhaba kuralları veya toodisable istediğiniz kuralı grupları arayın.
   2. Merhaba toodisable istediğiniz kuralları için hello onay kutularını temizleyin. 
   2. **Kaydet**’i seçin. 

![Değişiklikleri Kaydet][3]

## <a name="next-steps"></a>Sonraki adımlar

Devre dışı kurallarınızı yapılandırdıktan sonra öğrenebilirsiniz nasıl tooview WAF günlüklerinizi. Daha fazla bilgi için bkz: [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
