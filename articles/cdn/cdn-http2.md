---
title: "Azure CDN aaaHTTP/2 desteği | Microsoft Docs"
description: "HTTP/2 ve CDN desteği hakkında bilgi edinin."
services: cdn
documentationcenter: 
author: lichard
manager: erikre
editor: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: 2e5e5345e8cf5c40e080ebf18b4f13a239a5aac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="http2-support-in-azure-cdn"></a>Azure CDN HTTP/2 desteği

HTTP/2 büyük düzeltme tooHTTP/1.1\ olur. Daha hızlı web performans, daha az yanıt süresi ve gelişmiş bir kullanıcı, hello bilinen HTTP yöntemleri, durum kodları ve semantiği korurken deneyimi sağlar. HTTP/2 ile HTTP ve HTTPS tasarlanmış toowork olsa da, birçok istemci web tarayıcısı TLS yalnızca HTTP/2 destekler.

###<a name="http2-benefits"></a>HTTP/2 avantajları

HTTP/2 Hello avantajları şunlardır:

*   **Çoğullama ve eşzamanlılık**

    HTTP 1.1 kullanarak, birden çok birden çok kaynak istekleri birden fazla TCP bağlantısı gerektirir ve her bağlantı ile ilişkili performans yüke sahiptir. HTTP/2 tek bir TCP bağlantı üzerinde istenen birden çok kaynak toobe sağlar.

*   **Üstbilgi sıkıştırma**

    Sunulacak kaynakları Hello HTTP üstbilgilerini sıkıştırarak hello kablo zamanında önemli ölçüde azalır.

*   **Akış bağımlılıkları**

    Akış bağımlılıkları olan kaynakların öncelik tooindicate toohello sunucu hello istemci izin verin.


##<a name="http2-browser-support"></a>HTTP/2 tarayıcı desteği

Tüm önde gelen tarayıcılar hello HTTP/2 desteği geçerli sürümlerine uyguladık. Desteklenmeyen tarayıcılar otomatik olarak geri dönüş tooHTTP/1.1 olur.

|Tarayıcı|En düşük sürüm|
|-------------|------------|
|Microsoft Edge| 12|
|Google Chrome| 43|
|Mozilla Firefox| 38|
|Opera| 32|
|Safari| 9|

##<a name="enabling-http2-support-in-azure-cdn"></a>Azure CDN HTTP/2 desteğini etkinleştirme

HTTP/2 desteği şu anda etkin mi **akamai'den Azure CDN** ve **verizon'dan Azure CDN** profilleri. Başka bir eylem müşterilerden gereklidir.

##<a name="next-steps"></a>Sonraki Adımlar

toosee hello HTTP/2 eylem avantajlar [akamai'den bu demo](https://http2.akamai.com/demo).

HTTP/2 hakkında daha fazla toolearn kaynakları aşağıdaki hello ziyaret edin:

*   [HTTP/2 belirtimi giriş sayfası](https://http2.github.io/)
*   [Resmi HTTP/2 ile ilgili SSS](https://http2.github.io/faq/)
*   [Akamai HTTP/2 bilgileri](https://http2.akamai.com/)

Azure CDN'ın kullanılabilir özellikler hakkında daha fazla toolearn bkz hello [Azure CDN'ye genel bakış](https://azure.microsoft.com/documentation/articles/cdn-overview/).
