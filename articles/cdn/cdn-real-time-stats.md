---
title: "Azure CDN içinde aaaReal zamanı istatistikleri | Microsoft Docs"
description: "Gerçek zamanlı İstatistikler içerik tooyour istemcileri teslim edilirken Azure CDN hello performansını hakkında gerçek zamanlı verileri sağlar."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c7989340-1172-4315-acbb-186ba34dd52a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 68900a5092b767e45c1fdf9cef2cd03f55f38a6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a>Microsoft Azure cdn'de gerçek zamanlı İstatistikler
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Genel Bakış
Bu belgede, Microsoft Azure cdn'de gerçek zamanlı İstatistikler açıklanmaktadır.  Bu işlev içerik tooyour istemcileri teslim edilirken bant genişliği, önbellek durumları ve eşzamanlı bağlantı tooyour CDN profili gibi gerçek zamanlı verileri sağlar. Bu, sürekli hello Hizmetinizin durumunu servise olaylar dahil olmak üzere, herhangi bir zamanda izlenmesini sağlar.

grafikleri aşağıdaki hello kullanılabilir:

* [Bant genişliği](#bandwidth)
* [Durum kodları](#status-codes)
* [Önbellek durumları](#cache-statuses)
* [Bağlantılar](#connections)

## <a name="accessing-real-time-stats"></a>Gerçek zamanlı İstatistikler erişme
1. Merhaba, [Azure Portal](https://portal.azure.com), tooyour CDN profili göz atın.
   
    ![CDN profili dikey penceresi](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. Merhaba CDN profili dikey penceresinden hello tıklayın **Yönet** düğmesi.
   
    ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    Merhaba CDN Yönetim Portalı açar.
3. Merhaba üzerine getirin **Analytics** sekmesini ve ardından hello üzerine getirin **gerçek zamanlı İstatistikler** çıkma.  Tıklayın **HTTP büyük nesne**.
   
    ![CDN Yönetim Portalı](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    Merhaba gerçek zamanlı İstatistikler grafikleri görüntülenir.

Her hello grafikleri hello sayfa yüklendiğinde başlangıç hello seçili zaman aralığı için gerçek zamanlı istatistikler görüntüler.  Merhaba grafikleri birkaç dakikada otomatik olarak güncelleştirilir.  Merhaba **Grafiği Yenile** , varsa, Temizle düğmesi hello grafiği, daha sonra yalnızca gösterilir seçili hello veri.

## <a name="bandwidth"></a>Bant Genişliği
![Bant genişliği grafiği](./media/cdn-real-time-stats/cdn-bandwidth.png)

Merhaba **bant genişliği** grafiği hello hello seçili zaman aralığı içinde hello geçerli platform için kullanılan bant genişliği miktarını görüntüler. Merhaba gölgeli hello grafik kısmı bant genişliği kullanımını gösterir. Merhaba tam şu anda kullanılan bant genişliği miktarını doğrudan hello çizgi grafiği altında görüntülenir.

## <a name="status-codes"></a>Durum kodları
![Durum kodu grafiği](./media/cdn-real-time-stats/cdn-status-codes.png)

Merhaba **durum kodları** grafik belirli HTTP yanıt kodları hello seçili zaman aralığı içinde ne sıklıkta gerçekleştiğini gösterir.

> [!TIP]
> HTTP durum kodu seçeneğin açıklaması için bkz: [Azure CDN HTTP durum kodları](https://msdn.microsoft.com/library/mt759238.aspx).
> 
> 

HTTP durum kodları listesini doğrudan hello grafik görüntülenir. Bu liste hello çizgi grafiği ve hello geçerli sayısı, durum kodu için saniye başına dahil her durum kodu gösterir. Varsayılan olarak, bu durum kodunun hello grafikteki her biri için bir satır görüntülenir. Ancak, CDN yapılandırmanız için özel öneme sahip İzleyicisi Merhaba durum kodları tooonly seçebilirsiniz. toodo Bu, istenen hello durum kodları denetleyin ve diğer tüm seçeneklerini temizleyin ve ardından **Grafiği Yenile**. 

Bir özel durum kodu için günlüğe kaydedilen verileri geçici olarak gizleyebilirsiniz.  Doğrudan hello grafik aşağıda Hello göstergeden toohide istediğiniz hello durum kodu'ı tıklatın. Merhaba durum kodu hemen hello grafikten gizlenir. Bu durum kodu yeniden tıklandığında yeniden görüntülenen bu seçeneği toobe neden olur.

## <a name="cache-statuses"></a>Önbellek durumları
![Önbellek durumları grafiği](./media/cdn-real-time-stats/cdn-cache-status.png)

Merhaba **önbellek durumları** grafik belirli türde bir önbellek durumları hello seçili zaman aralığı içinde ne sıklıkta gerçekleştiğini gösterir. 

> [!TIP]
> Her önbellek durum kodu seçeneği açıklaması için bkz: [Azure CDN önbellek durum kodları](https://msdn.microsoft.com/library/mt759237.aspx).
> 
> 

Önbellek durum kodları listesini doğrudan hello grafik görüntülenir. Bu liste hello çizgi grafiği ve hello geçerli sayısı, durum kodu için saniye başına dahil her durum kodu gösterir. Varsayılan olarak, bu durum kodunun hello grafikteki her biri için bir satır görüntülenir. Ancak, CDN yapılandırmanız için özel öneme sahip İzleyicisi Merhaba durum kodları tooonly seçebilirsiniz. toodo Bu, istenen hello durum kodları denetleyin ve diğer tüm seçeneklerini temizleyin ve ardından **Grafiği Yenile**. 

Bir özel durum kodu için günlüğe kaydedilen verileri geçici olarak gizleyebilirsiniz.  Doğrudan hello grafik aşağıda Hello göstergeden toohide istediğiniz hello durum kodu'ı tıklatın. Merhaba durum kodu hemen hello grafikten gizlenir. Bu durum kodu yeniden tıklandığında yeniden görüntülenen bu seçeneği toobe neden olur.

## <a name="connections"></a>Bağlantılar
![Bağlantıları grafiği](./media/cdn-real-time-stats/cdn-connections.png)

Bu grafik, kaç tane bağlantıları kurulan tooyour uç sunucuların edildiğini gösterir. Her istek için bir bağlantı bizim CDN sonuçlarında geçtiği bir varlık.

## <a name="next-steps"></a>Sonraki Adımlar
* İle bilgi edinin [Azure CDN gerçek zamanlı uyarılar](cdn-real-time-alerts.md)
* Dıg ile daha derin [Gelişmiş HTTP raporları](cdn-advanced-http-reports.md)
* Analiz [kullanım desenleri](cdn-analyze-usage-patterns.md)

