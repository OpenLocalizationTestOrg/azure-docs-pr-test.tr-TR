---
title: "Gerçek kullanıcı ölçümleri Azure trafik Yöneticisi'nde | Microsoft Docs"
description: "Gerçek kullanıcı ölçümleri trafik Yöneticisi'nde giriş"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 09/19/2017
ms.author: kumud
ms.custom: 
ms.openlocfilehash: a7e8ae605b6234341d9ab8b790f4c54d8627f29f
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="traffic-manager-real-user-measurements-overview"></a>Trafik Yöneticisi gerçek kullanıcı ölçümleri genel bakış

>[!NOTE]
>Trafik Yöneticisi'nde gerçek kullanıcı ölçümleri özellik genel önizlemede ve genel kullanılabilirlik özellikleri sürüm gibi aynı düzeyde kullanılabilirlik ve güvenilirlik olmayabilir. Özellik desteklenmiyor, yetenekleri kısıtlı ve tüm Azure konumlarda kullanılamayabilir. Kullanılabilirlik ve bu özellik durumunu en güncel bildirimleri için denetleme [Azure trafik Yöneticisi'ni güncelleştirir](https://azure.microsoft.com/updates/?product=traffic-manager) sayfası.

Performans yönlendirme yöntemini kullanmak için bir trafik Yöneticisi profili ayarladığınızda, hizmet burada DNS sorgu isteği'ten gelen ve bu istek sahipleri en düşük gecikme sağlar Azure bölgesine yönlendirmek için yönlendirme kararlarını verir bakar. Bu trafik Yöneticisi için farklı son kullanıcı ağları tutar ağ gecikmesi Intelligence yararlanarak gerçekleştirilir.

Ağ gecikmesi ölçümleri Azure bölgeleri için son kullanıcılarınızın kullanın, istemci uygulamalarından ölçmek gerçek kullanıcı ölçümleri sağlar ve sahip trafik Yöneticisi düşünün bu bilgileri de yönlendirme kararları verirken. Gerçek kullanıcı ölçümleri Kullan'ı seçerek son kullanıcılarınızın bulunduğu bu ağlardan gelen istekleri için yönlendirme doğruluğunu artırabilir. 

## <a name="how-real-user-measurements-work"></a>Gerçek kullanıcı ölçümleri nasıl çalışır

Gerçek kullanıcı ölçümleri kullanılan son kullanıcı ağlardan görülen Azure bölgeler ile istemci uygulamaları ölçü gecikme sağlayarak çalışır. Kullanıcılar tarafından farklı konumlarda (örneğin, Kuzey Amerika bölgelerde) üzerinden erişilen bir web sayfası varsa en iyi Azure bölgesinde almak için performans yönlendirme yöntemini kullandığınızda, örnek olarak, gerçek kullanıcı ölçümleri gücünü yararlanabileceğiniz hangi sunucu uygulamanızı barındırılır.

Web sayfalarınızda (ile benzersiz bir anahtar da) Azure bir sağlanan JavaScript gömerek başlar. Bir kullanıcı, bir Web sitesini ziyaret olduğunda, yapıldıktan sonra JavaScript trafik Yöneticisi'ni ölçmek Azure bölgeleri hakkında bilgi almak için sorgular. Hizmet uç noktaları kümesini komut dosyasına, sonra bu bölgeler art arda yükleyerek bu Azure bölgelerinde barındırılan ve gecikme süresi arasında belirtmeye tek pikselli bir görüntü isteği gönderildi ölçü ve ilk bayt alındığında saati döndürür . Bu ölçümleri, trafik yöneticisi hizmete geri raporlanır.

Zaman içerisinde, bu birçok kez gerçekleşir ve birçok ağlar, ağ gecikme süresi özellikleri hakkında daha doğru bilgi alma trafik Yöneticisi önde gelen son kullanıcılarınızın bulunur. Bu bilgiler, trafik Yöneticisi tarafından yapılan yönlendirme kararları dahil edilecek alma başlatır. Sonuç olarak, gerçek kullanıcı ölçü gönderilen göre bu kararların daha yüksek doğruluk neden olmaktadır.

Gerçek kullanıcı ölçümleri kullandığınızda, trafik Yöneticisi için gönderilen ölçümleri sayısına göre faturalandırılır. Fiyatlandırma hakkında daha fazla ayrıntı için ziyaret [trafik Yöneticisi fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/traffic-manager/).

## <a name="next-steps"></a>Sonraki adımlar
- Nasıl kullanacağınızı öğrenin [web sayfalarıyla gerçek kullanıcı ölçümleri](traffic-manager-create-rum-web-pages.md)
- Bilgi [trafik Yöneticisi nasıl çalışır?](traffic-manager-overview.md)
- Daha fazla bilgi edinmek [Mobile Merkezi](https://docs.microsoft.com/mobile-center/)
- Daha fazla bilgi edinmek [trafik yönlendirme yöntemleri](traffic-manager-routing-methods.md) Traffic Manager tarafından desteklenen
- Bilgi edinmek için nasıl [bir Traffic Manager profili oluşturma](traffic-manager-create-profile.md)

