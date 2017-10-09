---
title: "Azure API Management ile azaltma aaaAdvanced isteği"
description: "Bilgi nasıl toocreate ve esnek kota ve ilkeleri Azure API Management ile hız sınırı uygulayın."
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: fc813a65-7793-4c17-8bb9-e387838193ae
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: ac87f83118a37bd587fddf044e5c2d6fc2af9031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a>Gelişmiş istek azaltma ile Azure API Yönetimi
Mümkün toothrottle gelen istekleri olan Azure API Management önemli bir rol var. API Management sağlar ya da kontrol eden hello oranı istekler veya hello toplam istekleri/veri transfer, API sağlayıcıları tooprotect kötüye kendi API'lerden ve farklı API ürün katmanları için değeri oluşturun.

## <a name="product-based-throttling"></a>Ürün tabanlı azaltma
toodate, kısıtlama yetenekleri hello oranı sınırlı toobeing kapsamlı tooa belirli ürün abonelik (aslında bir anahtarı), API Management yayımcı portalına hello tanımlanan. Merhaba API sağlayıcısı tooapply sınırları toouse kendi API açmış hello geliştiriciler için faydalıdır, ancak bu, örneğin, tek tek son kullanıcılar hello API için azaltma korumaz. Bu, hello geliştiricinin uygulama tooconsume tek bir kullanıcı için tüm kota hello ve ardından diğer müşteriler hello Developer mümkün toouse Merhaba uygulaması engelleyen mümkün olur. Ayrıca, bir istek hacmi yüksek oluşturabilir çeşitli müşteriler erişim toooccasional kullanıcıları sınırlayabilir.

## <a name="custom-key-based-throttling"></a>Özel anahtar tabanlı azaltma
Merhaba yeni [anahtar tarafından hızı sınırı](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) ve [kota anahtarı](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) önemli ölçüde daha esnek bir çözüm tootraffic denetim ilkeleri sağlar. Bu yeni ilkeleri kullanılan tootrack trafiği kullanım olacaktır toodefine ifadeleri tooidentify hello anahtarlarının izin verir. Bu çalışır hello şekilde kolay bir örnekle gösterilmiştir. 

## <a name="ip-address-throttling"></a>IP adresi azaltma
Merhaba aşağıdaki ilkeleri kısıtlamak tek bir istemci IP adresi tooonly 10 dakikada 1.000.000 çağrıları ve bant genişliği aylık 10.000 kilobayt toplam çağırır. 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

Merhaba Internet üzerindeki tüm istemcilere benzersiz bir IP adresi kullandıysanız, bu kullanıcı tarafından kullanımı sınırlama, etkili bir yol olabilir. Ancak, birden çok kullanıcı bir NAT cihazı üzerinden toothem erişilirken hello Internet nedeniyle tek bir ortak IP adresi paylaşımı olacak oldukça olasıdır. Buna karşın, kimliği doğrulanmamış erişim hello izin API'leri için `IpAddress` hello en iyi seçenek olabilir.

## <a name="user-identity-throttling"></a>Kullanıcı Kimliği azaltma
Son kullanıcının kimliği doğrulandıktan sonra azaltma anahtarı tanıtan bir, bilgilere dayalı olarak oluşturulabilen kullanıcı.

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

Bu örnekte biz hello Authorization Üstbilgisi ayıklama ve çok Dönüştür`JWT` nesne ve hello belirteci tooidentify hello kullanıcının hello konu ve anahtar sınırlama hello hızı olarak kullanın. Merhaba kullanıcı kimliği hello depolanıyorsa `JWT` hello başka birini sonra değer onun yerine kullanılabilir talep gibi.

## <a name="combined-policies"></a>Birleşik ilkeleri
Yeni ilkeler azaltma hello kısıtlama ilkeleri varolan hello daha fazla denetim sağlar ancak da hala her iki özelliği birleştirme değer vardır. Ürün abonelik anahtarı tarafından azaltma ([abonelik tarafından çağrı hızını sınırla](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) ve [abonelik tarafından kullanım kotası ayarla](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) temel kullanım düzeyleri şarj tarafından bir API tooenable monetizing harika bir yoludur. Merhaba kullanıcı tarafından mümkün toothrottle olma daha hassas denetim tamamlayıcı ve bir kullanıcının davranışına başka bir hello deneyimi düşürmesini engeller. 

## <a name="client-driven-throttling"></a>Azaltma yönetilen istemci
Anahtar azaltma hello kullanarak tanımlandığında bir [ilke ifadesi](https://msdn.microsoft.com/library/azure/dn910913.aspx), hello azaltma nasıl kapsamlıdır seçme hello API sağlayıcı ise. Bununla birlikte, bir geliştirici isteyebilirsiniz nasıl oranı toocontrol sınırlamak kendi müşteriler. Bu hello API sağlayıcısı tarafından bir özel üstbilgi tooallow hello Geliştirici istemci uygulaması toocommunicate hello anahtar toohello API sunarak etkinleştirilmesi.

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

Bu hello geliştiricinin istemci uygulaması toochoose sağlar anahtar sınırlama toocreate hello oranı nasıl istedikleri. Biraz resimleri ile bir istemci Geliştirici anahtarları toousers kümelerini ayırma ve hello anahtar kullanımı döndürme kendi oranı katmanları oluşturabilirsiniz.

## <a name="summary"></a>Özet
Azure API Management oranı tooboth azaltma teklif korumak ve değer tooyour API hizmeti eklemek sağlar. Yeni özel ölçüm kuralları ilkeleriyle azaltma hello yüksekse, bu ilkeleri tooenable üzerinde denetim müşteriler toobuild daha da iyi uygulamalarınızı düzey izin verir. Bu makalede Hello örnekler, istemci IP adresleri, kullanıcı kimliği ve istemci oluşturulan değerleri anahtarlarla sınırlama üretim hızına göre bu yeni ilkeleri hello kullanımını göstermektedir. Ancak, diğer birçok kullanılabilecek kullanıcı aracısı, URL yolu parçaları, ileti boyutu gibi selamlama iletisine bölümleri vardır.

## <a name="next-steps"></a>Sonraki adımlar
Lütfen bize Geri bildiriminizi hello Disqus iş parçacığı için bu konunun verin. Senaryolarınız mantıksal bir seçenek olan diğer olası anahtar değerleri hakkında harika toohear olacaktır.

## <a name="watch-a-video-overview-of-these-policies"></a>Bu ilkelerin video genel izleyin
Merhaba hakkında daha fazla bilgi için [anahtar tarafından hızı sınırı](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) ve [kota anahtarı](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) bu makalede ele alınan ilkeleri Lütfen video aşağıdaki hello izleyin.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

