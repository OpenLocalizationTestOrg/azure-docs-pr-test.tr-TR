---
title: "aaaAzure CDN'ye genel bakış | Microsoft Docs"
description: "Azure içerik teslim ağı (CDN) olan hangi hello öğrenin ve nasıl toouse, blobları ve statik içerik önbelleğe alma tarafından toodeliver yüksek bant genişliği içeriği."
services: cdn
documentationcenter: 
author: smcevoy
manager: akucer
editor: 
ms.assetid: 866e0c30-1f33-43a5-91f0-d22f033b16c6
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/08/2017
ms.author: v-semcev
ms.openlocfilehash: e0230a6e107969b845985f2f4d357bf93cd40d42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-azure-content-delivery-network-cdn"></a>Hello Azure içerik teslim ağı (CDN) genel bakış
> [!NOTE]
> Bu belge, Azure içerik teslim ağı (CDN) olan hangi Merhaba, nasıl çalıştığı ve her Azure CDN ürününün hello özelliklerini açıklar.  Bu bilgiler tooskip istediğiniz ve düz tooa öğretici gitmek toocreate bir CDN uç noktası bkz [Azure CDN'yi kullanma](cdn-create-new-endpoint.md).  Toosee mevcut CDN düğümü konumları listesini istiyorsanız, bkz: [Azure CDN POP konumları](cdn-pop-locations.md).
> 
> 

Hello Azure içerik teslim ağı (CDN) içerik toousers teslim stratejik olarak yerleştirilmiş konumlardaki tooprovide en yüksek verimlilik statik web içeriği önbelleğe alır.  Merhaba CDN geliştiriciler Merhaba dünya genelindeki fiziksel düğümlerde hello içeriği önbelleğe alarak yüksek bant genişliği içeriği teslimi için genel bir çözüm sunar. 

Merhaba hello CDN toocache web sitesi varlıklarını kullanmanın avantajları şunlardır:

* Özellikle birden çok gidiş dönüş nerede uygulamaları kullanarak tooload içeriği gerektiğinde son kullanıcılar için daha iyi performans ve kullanıcı deneyimi.
* Büyük ölçeklendirme toobetter hello bir ürün başlangıcında olay başlatma gibi anlık yüksek düzeyde yükü işleyin.
* Kullanıcı isteklerinin dağıtımı ve uç sunuculardan içerik hizmet veren toohello kaynak daha az trafik gönderilir.

## <a name="how-it-works"></a>Nasıl çalışır?
![CDN'ye Genel Bakış](./media/cdn-overview/cdn-overview.png)

1. Bir kullanıcı (Alice), `<endpointname>.azureedge.net` gibi özel bir etki alanı adına sahip olan bir URL'yi kullanarak bir dosya (varlık olarak da adlandırılır) isteğinde bulunur.  DNS hello isteği toohello en iyi gerçekleştirme bulunma noktası (POP) konumuna yönlendirir.  Genellikle bu hello coğrafi olarak en yakın toohello kullanıcı POP adıdır.
2. Merhaba POP Hello uç sunucuların önbelleğinde hello dosya yoksa, hello uç sunucusunu hello dosya hello kaynaktan ister.  Merhaba kaynak bir Azure Web uygulaması, Azure bulut hizmeti, Azure depolama hesabı veya herhangi bir genel olarak erişilebilir web sunucusu olabilir.
3. Merhaba kaynak hello dosyanın için-yaşam süresi (TTL) açıklayan isteğe bağlı HTTP üst bilgileri de dahil olmak üzere hello dosya toohello uç sunucu, döndürür.
4. Merhaba uç sunucusunu hello dosyayı önbelleğe alır ve hello dosya toohello özgün istek (Alice) döndürür.  Merhaba TTL süresi dolana kadar hello dosya hello uç sunucuda önbelleğe alınmış olarak kalır.  Merhaba kaynak bir TTL belirtmemişse hello varsayılan TTL yedi gündür.
5. Ek kullanıcılar aynı aynı URL'yi kullanarak dosya ve ayrıca Mayıs isteği hello yönlendirilmiş toothat olması olabilir aynı POP.
6. Merhaba dosya Merhaba TTL Süresi dolmamışsa hello uç sunucusunu hello dosya hello önbellekten döndürür.  Bu, daha hızlı ve daha duyarlı bir kullanıcı deneyimi sağlar.

## <a name="azure-cdn-features"></a>Azure CDN'nin Özellikleri
Üç Azure CDN ürünü mevcuttur: **Akamai'den Azure CDN Standart**, **Verizon'dan Azure CDN Standart** ve **Verizon'dan Azure CDN Premium**.  Merhaba aşağıdaki tabloda her ürünle birlikte sunulan hello özellikleri listeler.

|  | Standart Akamai | Standart Verizon | Premium Verizon |
| --- | --- | --- | --- |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __Performans Özellikleri ve İyileştirmeler__ |
| [Dinamik Site Hızlandırma](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration) | **&#x2713;**  | **&#x2713;** | **&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Dinamik Site Hızlandırma - Uyarlamalı Görüntü Sıkıştırma](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#adaptive-image-compression-akamai-only) | **&#x2713;**  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Dinamik Site Hızlandırma - Nesneleri Önceden Getirme](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#object-prefetch-akamai-only) | **&#x2713;**  |  |  |
| [Video Akışı iyileştirmesi](https://docs.microsoft.com/azure/cdn/cdn-media-streaming-optimization) | **&#x2713;**  | \* |  \* |
| [Büyük Dosya İyileştirmesi](https://docs.microsoft.com/azure/cdn/cdn-large-file-optimization) | **&#x2713;**  | \* |  \* |
| [Genel Sunucu Yük Dengelemesi (GSLB)](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-load-balancing-azure) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Hızlı temizleme](cdn-purge-endpoint.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Varlık önceden yükleme](cdn-preload-endpoint.md) | |**&#x2713;** |**&#x2713;** |
| [Sorgu dizesini önbelleğe alma](cdn-query-string.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| IPv4/IPv6 ikili yığını |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [HTTP/2 desteği](cdn-http2.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __Güvenlik__ |
| CDN uç noktasıyla HTTPS desteği |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Özel etki alanı HTTPS](cdn-custom-ssl.md) | |**&#x2713;** |**&#x2713;** |
| [Özel etki alanı adı desteği](cdn-map-content-to-custom-domain.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Coğrafi filtreleme](cdn-restrict-access-by-country.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Belirteç kimlik doğrulaması](cdn-token-auth.md)|  |  |**&#x2713;**| 
| [DDOS koruması](https://www.us-cert.gov/ncas/tips/ST04-015) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __Analiz ve Raporlama__ |
| [Temel analiz](cdn-analyze-usage-patterns.md) | **&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Gelişmiş HTTP raporları](cdn-advanced-http-reports.md) | | |**&#x2713;** |
| [Gerçek zamanlı istatistikler](cdn-real-time-stats.md) | | |**&#x2713;** |
| [Gerçek zamanlı uyarılar](cdn-real-time-alerts.md) | | |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __Kullanım Kolaylığı__ |
| [Storage](cdn-create-a-storage-account-with-cdn.md), [Cloud Services](cdn-cloud-service-with-cdn.md), [Web Apps](../app-service-web/app-service-web-tutorial-content-delivery-network.md) ve [Media Services](../media-services/media-services-portal-manage-streaming-endpoints.md) gibi Azure hizmetleriyle kolay tümleştirme |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [REST API](https://msdn.microsoft.com/library/mt634456.aspx), [.NET](cdn-app-dev-net.md), [Node.js](cdn-app-dev-node.md), veya [PowerShell](cdn-manage-powershell.md) aracılığıyla yönetim. |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Özelleştirilebilir, kural tabanlı içerik teslim altyapısı](cdn-rules-engine.md) | | |**&#x2713;** |
| Önbellek/üstbilgi ayarları ([kurallar altyapısı](cdn-rules-engine.md) kullanılarak) | | |**&#x2713;** |
| URL yeniden yönlendirme/yeniden yazma ([kurallar altyapısı](cdn-rules-engine.md) kullanılarak) | | |**&#x2713;** |
| Mobil cihaz kuralları ([kurallar altyapısı](cdn-rules-engine.md) kullanılarak) | | |**&#x2713;** |

\* Verizon, doğrudan bir Genel Web Teslimatı aracılığıyla büyük dosya ve medya göndermeyi destekler.


> [!TIP]
> Azure CDN toosee istediğiniz bir özellik var mı?  [Bize geri bildirim sağlayın](https://feedback.azure.com/forums/169397-cdn)! 
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
CDN ile çalışmaya tooget bkz [Azure CDN'yi kullanma](cdn-create-new-endpoint.md).

Artık, var olan bir CDN müşterisiyseniz, CDN uç noktalarınızı hello aracılığıyla yönetebilirsiniz [Microsoft Azure portal](https://portal.azure.com) veya [PowerShell](cdn-manage-powershell.md).

toosee CDN eylemde Merhaba, hello denetleyin [Build 2016 oturumu videomuza, video](https://azure.microsoft.com/documentation/videos/build-2016-leveraging-the-new-azure-cdn-apis-to-build-wicked-fast-applications/).

Bilgi nasıl tooautomate Azure CDN ile [.NET](cdn-app-dev-net.md) veya [Node.js](cdn-app-dev-node.md).

Fiyatlandırma bilgileri için bkz. [CDN Fiyatlandırması](https://azure.microsoft.com/pricing/details/cdn/).

