---
title: "aaaProtecting uygulamalarınızı Azure Güvenlik Merkezi'nde | Microsoft Docs"
description: "Yardımcı olacak öneriler Azure Güvenlik Merkezi'nde Azure uygulamalarınızı korumaya ve güvenlik ilkeleriyle uyumlu olmak bu belge adresleri."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: b5fc7a9e-24b1-415f-b3b5-62a53f5dd424
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: terrylan
ms.openlocfilehash: da5e02cc2bad55c64e4da14e4e10efd6ddeab39e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-applications-in-azure-security-center"></a>Uygulamalarınızı Azure Güvenlik Merkezi'nde koruma
Azure Güvenlik Merkezi hello Azure kaynaklarınızın güvenlik durumunu çözümler. Güvenlik Merkezi olası güvenlik açıklarını belirlediğinde, gerekli hello denetimlerini yapılandırma hello işleminde size kılavuzluk öneriler oluşturur.  Önerileri tooAzure kaynak türleri geçerlidir: sanal ağ, SQL ve uygulamaları makineleri (VM'ler).

Bu makalede tooapplications uygulamak önerileri giderir.  Uygulama önerileri merkezi bir web uygulaması güvenlik duvarı dağıtımını etrafında.  Bir başvuru toohelp olarak kullanımı hello tablo aşağıda hello kullanılabilir uygulama önerileri ve onu uygularsanız her birini ne yaptığını anlayın.

## <a name="available-application-recommendations"></a>Kullanılabilir uygulama önerileri
| Öneri | Açıklama |
| --- | --- |
| [Web uygulaması güvenlik duvarı ekleme](security-center-add-web-application-firewall.md) |Web uç noktaları için web uygulaması Güvenlik Duvarı (WAF) dağıtmak önerir. WAF öneri açık gelen web bağlantı noktaları (80,443) içeren bir ilişkili ağ güvenlik grubu olan tüm genel kullanıma yönelik IP'si için (örnek düzeyinde IP veya yük dengeli IP) gösterilir.</br></br>Güvenlik Merkezi WAF toohelp provizyon sanal makineler ve uygulama hizmeti ortamı, web uygulamalarınızı hedefleyen saldırılara karşı korumaya önerir. Uygulama hizmeti ortamı (ana) olan bir [Premium](https://azure.microsoft.com/pricing/details/app-service/) hizmet planı seçeneği Azure App Service, güvenli bir şekilde Azure App Service uygulamalarını çalıştırmak için tam yalıtılmış ve ayrılmış bir ortam sağlar. toolearn ana, hakkında daha fazla bilgi görmek hello [uygulama hizmeti ortamı belgeleri](../app-service/app-service-app-service-environments-readme.md).</br></br>Bu uygulamalar tooyour varolan WAF dağıtımlar ekleyerek, birden çok web uygulamasına Güvenlik Merkezi'nde koruyabilirsiniz. |
| [Uygulama korumasını sonlandırma](security-center-add-web-application-firewall.md#finalize-application-protection) |toocomplete hello yapılandırmasını WAF, trafiği yeniden yönlendirilen toohello WAF Gereci olması gerekir. Bu öneri aşağıdaki hello gerekli Kurulum değişiklikleri tamamlar. |

## <a name="see-also"></a>Ayrıca bkz.
toolearn tooother Azure kaynak türleri bkz hello aşağıdaki öneriler hakkında daha fazla bilgi:

* [Azure Güvenlik Merkezi'nde, sanal makineleri koruma](security-center-virtual-machine-recommendations.md)
* [Azure Güvenlik Merkezi, ağınızda koruma](security-center-network-recommendations.md)
* [Azure SQL hizmetinizi Azure Güvenlik Merkezi'nde koruma](security-center-sql-service-recommendations.md)

Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
