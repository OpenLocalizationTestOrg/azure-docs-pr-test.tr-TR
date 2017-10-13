---
title: "Azure Application Gateway ile çok kiracılı arka uçlara genel bakış | Microsoft Docs"
description: "Bu sayfada, Application Gateway’in çok kiracılı arka uç desteği için genel bir bakış sunulmuştur."
documentationcenter: na
services: application-gateway
author: davidmu1
manager: timlt
editor: 
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: davidmu
ms.openlocfilehash: c29ff60a50e68c75b4e8f62713d6d1fffd2123d6
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="application-gateway-support-for-multi-tenant-back-ends"></a>Çok kiracılı arka uçlar için Application Gateway desteği

Azure Application Gateway, arka uç havuzlarının bir parçası olarak sanal makine ölçek kümeleri, ağ arabirimleri, ortak/özel IP veya tam etki alanı adını (FQDN) destekler. Varsayılan olarak, application gateway istemciden gelen HTTP ana bilgisayar üst bilgisini değiştirmez ve üst bilgiyi değiştirilmemiş halde arka uca gönderir. Nitelik bakımından çok kiracılı olup doğru uç noktaya çözümlemek için belirli bir ana bilgisayar üst bilgisini veya SNI uzantısını kullanan, [Azure Web Apps](../app-service/app-service-web-overview.md) ve [API Management](../api-management/api-management-key-concepts.md) gibi çok sayıda hizmet vardır. Application Gateway artık kullanıcıların arka uç HTTP ayarlarına göre gelen HTTP ana bilgisayar üst bilgisinin üzerine yazmasını desteklemektedir. Bu özellik Azure Web Apps ve API Management uygulamalarında çok kiracılı arka uçlar için destek sağlar. Bu özellik hem standart hem de WAF SKU’sunda kullanılabilir. Çok kiracılı arka uç desteği ayrıca SSL sonlandırma ve uçtan uca SSL senaryoları ile çalışır.

![web uygulaması senaryosu](./media/application-gateway-web-app-overview/scenario.png)

Ana bilgisayar geçersiz kılma işlemi belirtme olanağı HTTP ayarlarında tanımlanır ve kural oluşturma sırasında herhangi bir arka uç havuzuna uygulanabilir. Çok kiracılı arka uçlar, ana bilgisayar üst bilgisini ve SNI uzantısını aşağıdaki iki yöntemle geçersiz kılmayı destekler.

1. Ana bilgisayar adını HTTP ayarlarında sabit bir değere ayarlama. Bu özellik, HTTP ayarlarının uygulandığı arka uç havuzuna giden tüm trafik için ana bilgisayar üst bilgisinin bu değerle geçersiz kılınmasını sağlar. Uçtan uca SSL kullanılırken, geçersiz kılınan bu ana bilgisayar adı SNI uzantısında kullanılır. Bu özellik, bir arka uç havuzu grubunun gelen müşteri ana bilgisayar üst bilgisinden farklı bir ana bilgisayar üst bilgisi beklediği senaryoların gerçekleşmesine olanak tanır.

2. Arka uç havuzu üyelerinin IP veya FQDN’sinden ana bilgisayar adını türetme. HTTP ayarları ayrıca, tek bir arka uç havuzu üyesinden ana bilgisayar adı türetme seçeneğiyle birlikte yapılandırılması durumunda, bir arka uç havuzu üyesinin FQDN’sinden ana bilgisayar adını belirleme seçeneği sağlar. Uçtan uca SSL kullanılırken, bu ana bilgisayar adı FQDN’den türetilir ve SNI uzantısında kullanılır. Bu özellik, bir arka uç havuzunun Azure Web Apps gibi iki veya daha fazla çok kiracılı PaaS hizmetine sahip olabileceği ve her bir üyeye gönderilen isteğin ana bilgisayar üst bilgisinde FQDN’den türetilmiş ana bilgisayar adının bulunduğu senaryoların gerçekleşmesine olanak tanır.

> [!NOTE]
> Önceki örneklerin her ikisinde de, ayarlar yalnızca canlı trafik davranışını etkiler ve sistem durumu araştırma davranışını etkilemez. Özel araştırmalar, araştırma yapılandırmasında bir ana bilgisayar üst bilgisi belirtme olanağını zaten desteklemektedir. Özel araştırmalar artık o anda yapılandırılmış HTTP ayarlarından ana bilgisayar üst bilgisi davranışını türetme olanağını da desteklemektedir. Bu yapılandırma, araştırma yapılandırmasındaki `PickHostNameFromback endAddress` parametresi kullanılarak belirtilebilir. Uçtan uca işlevselliğin çalışması için hem araştırma hem de HTTP ayarları doğru yapılandırmayı yansıtacak şekilde değiştirilmelidir.

Bu özellik sayesinde müşteriler, HTTP ayarları ve özel araştırmalardaki seçenekleri uygun yapılandırmaya göre belirtebilir. Bu ayar daha sonra bir kural kullanılarak dinleyiciye ve arka uç havuzuna bağlanır.

## <a name="next-steps"></a>Sonraki adımlar

Bir web uygulaması ile arka uç havuzu olarak uygulama ağ geçidi oluşturma hakkında bilgi için bkz. [Application Gateway ile App Service web uygulamaları yapılandırma](application-gateway-web-app-powershell.md)
