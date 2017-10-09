---
title: "Azure CDN uç noktasında aaaPre yük varlıkları | Microsoft Docs"
description: "Nasıl toopre yük Azure CDN uç noktada önbelleğe alınmış içeriği öğrenin."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 5ea3eba5-1335-413e-9af3-3918ce608a83
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 08ac4b834f1ac8ce59d22e65fa8adea11bafcf17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a>Azure CDN uç noktasında varlıkları önceden yükleme
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Varsayılan olarak, bunlar istendiği varlıklar ilk önbelleğe alınır. Bunun anlamı hello ilk istek her bölgesinden uzun sürebilir, hello uç sunucuların değil gerekeceğinden hello içeriği önbelleğe ve tooforward hello istek toohello kaynak sunucusu gerekir. İçeriği önceden yüklerken bu ilk isabet gecikmesini önler.

Ayrıca tooproviding önbelleğe alınmış varlıkları önceden yükleme daha iyi bir müşteri deneyimi hello kaynak sunucu üzerindeki ağ trafiğini azaltabilir.

> [!NOTE]
> İçerik, kullanıcılar, yeni bir filmi sürüm veya bir yazılım güncelleştirmesi gibi çok sayıda eşzamanlı olarak kullanılabilir tooa olur veya varlıkları önceden yükleme büyük olaylar için yararlı olur.
> 
> 

Bu öğreticide, tüm Azure CDN uç düğümlerde önbelleğe alınmış içeriği önceden yükleme aracılığıyla açıklanmaktadır.

## <a name="walkthrough"></a>Kılavuz
1. Merhaba, [Azure Portal](https://portal.azure.com), toopre yük istediğiniz hello bitiş noktası içeren toohello CDN profili göz atın.  Hello profili dikey penceresi açılır.
2. Merhaba listesinde Hello uç noktasına tıklayın.  Merhaba uç nokta dikey pencere açılır.
3. Merhaba CDN uç noktası dikey penceresinden hello yükle düğmesine tıklayın.
   
    ![CDN uç noktası dikey penceresi](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    Merhaba yük dikey pencere açılır.
   
    ![CDN yük dikey penceresi](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. Merhaba tam yolunu girin tooload istediğiniz her varlık (örn., `/pictures/kitten.png`) hello içinde **yolu** metin kutusu.
   
   > [!TIP]
   > Daha fazla **yolu** kutularındaki metin tooallow girdikten sonra görünür toobuild birden çok varlıkların listesi.  Merhaba üç nokta (...) düğmesini tıklatarak varlıklar hello listesinden silebilirsiniz.
   > 
   > Yollar hello aşağıdaki uygun göreli bir URL olmalıdır [normal ifade](https://msdn.microsoft.com/library/az24scfc.aspx):  
   > >Tek bir dosya yolu yük `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;  
   > >Sorgu dizesi tek bir dosyayı yükleme`@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`  
   > 
   > Her varlık, kendi yolu olması gerekir.  Ön yükleme varlıklar için joker karakter işlevi yoktur.
   > 
   > 
   
    ![Yük düğmesi](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. Merhaba tıklatın **yük** düğmesi.
   
    ![Yük düğmesi](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> Her CDN profili dakikada 10 yük isteklerinin bir sınırlama yoktur. İstek başına 50 yollara izin verilir. Her yol 1024 karakterden oluşan bir yol uzunluğu sınırı vardır.
> 
> 

## <a name="see-also"></a>Ayrıca bkz.
* [Bir Azure CDN uç noktasını temizleme](cdn-purge-endpoint.md)
* [Azure CDN REST API Başvurusu - temizlemek veya bir uç nokta önceden yükleme](https://msdn.microsoft.com/library/mt634451.aspx)

