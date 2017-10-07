---
title: "çok kiracılı geri aaaOverview Azure uygulama ağ geçidi ile biten | Microsoft Docs"
description: "Bu sayfa için çok kiracılı arka uçları hello uygulama ağ geçidi Destek genel bir bakış sağlar."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: b7da8c9c68e34bd83ad2b828fab62c00caea354a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-support-for-multi-tenant-back-ends"></a>Çok kiracılı arka uçlar için Application Gateway desteği

Azure Application Gateway, arka uç havuzlarının bir parçası olarak sanal makine ölçek kümeleri, ağ arabirimleri, ortak/özel IP veya tam etki alanı adını (FQDN) destekler. Varsayılan olarak, uygulama ağ geçidi hello istemciden gelen HTTP ana bilgisayar üstbilgisi hello değiştirmez ve üstbilgi değiştirilmemiş toohello arka uç gönderir hello. Gibi birçok hizmeti [Azure Web Apps](../app-service-web/app-service-web-overview.md) ve [API Management](../api-management/api-management-key-concepts.md) doğası gereği çok kiracılı ve bir özel ana bilgisayar üstbilgisi veya SNI uzantısı tooresolve toohello doğru uç noktası kullanır. Uygulama ağ geçidi hello arka uç HTTP ayarlarınızı temel alan kullanıcılar toooverwrite hello gelen HTTP ana bilgisayar üstbilgisi hello özelliği artık destekliyor. Bu özellik Azure Web Apps ve API Management uygulamalarında çok kiracılı arka uçlar için destek sağlar. Bu özellik standart hello ve WAF SKU için kullanılabilir. Çok kiracılı geri desteği de SSL sonlandırma ve son tooend SSL senaryoları ile çalışır sonlandırın.

![web uygulaması senaryosu](./media/application-gateway-web-app-overview/scenario.png)

bir ana bilgisayar geçersiz kılma adresindeki tanımlı hello özelliği toospecify hello HTTP ayarları ve olması geri uygulanan tooany bitiş havuzu kural oluşturma sırasında. Çok kiracılı geri ana bilgisayar üstbilgisi ve SNI uzantısı geçersiz kılma iki yolu aşağıdaki Destek hello sona erer.

1. Merhaba özelliği tooset hello ana bilgisayar adı tooa hello değerinde HTTP ayarlar sabit. Bu özellik bu hello ana bilgisayar üstbilgisi geçersiz kılınmıştır sağlar toothis hello HTTP ayarları uygulanır burada tüm trafiği toohello arka uç havuzu için değer. Son tooend SSL kullanırken, bu geçersiz kılınan ana bilgisayar adı hello SNI uzantısı kullanılır. Bu özellik, burada bir arka uç havuzu grubu hello gelen müşteri ana bilgisayar üstbilgisi farklı bir ana bilgisayar üstbilgisi bekliyor senaryolara olanak sağlar.

2. Merhaba IP veya FQDN hello arka uç havuzu üyelerinin Hello özelliği tooderive hello ana bilgisayar adı. HTTP ayarları bir seçenek toopick hello ana bilgisayar adı hello seçeneği tooderive ana bilgisayar adı bir bireysel arka uç havuzu üyeden ile yapılandırılmış bir arka uç havuzu üyesinin FQDN gelen de sağlar. Son tooend SSL kullanırken, bu ana bilgisayar adı FQDN hello türetilmiş ve hello SNI uzantısı kullanılır. Bu özellik, burada bir arka uç havuzu Azure web uygulamaları gibi iki veya daha fazla çok kiracılı PaaS hizmetlerini olabilir ve hello isteğin ana bilgisayar üstbilgisi tooeach üye FQDN'sini türetilen hello ana bilgisayar adını içeriyorsa senaryolara olanak sağlar.

> [!NOTE]
> Hem durumlarda önceki hello hello ayarları yalnızca hello dinamik trafik ve değil hello sistem durumu araştırma davranışlarını etkiler. Özel zaten destek hello özelliği toospecify hello araştırma yapılandırmasında bir ana bilgisayar üstbilgisi araştırmaları. Özel araştırmalara şimdi hello özelliği tooderive hello ana bilgisayar üstbilgisi davranışı şu anda yapılandırılmış hello HTTP ayarlarından da destekler. Bu yapılandırma hello kullanarak belirtilebilir `PickHostNameFromback endAddress` hello araştırma yapılandırmasında parametre. Son tooend işlevselliği toowork için hello araştırma ve hello HTTP ayarları değiştirilmiş tooreflect hello doğru yapılandırma olması gerekir.

Bu özellik ile Merhaba seçenekleri hello HTTP ayarları ve özel yoklamaları toohello uygun yapılandırma müşteriler belirtin. Bu ayar daha sonra bağlı tooa dinleyicisi ile bir end havuzu bir kural kullanarak.

## <a name="next-steps"></a>Sonraki adımlar

Bilgi nasıl tooset bir web uygulaması gibi bir arka sahip bir uygulama ağ geçidi yukarı bitiş havuz üyesi ziyaret ederek: [yapılandırma App Service web apps ile uygulama ağ geçidi](application-gateway-web-app-powershell.md)
