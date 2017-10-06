---
title: "Azure CDN önbelleğe alma davranışını sorgu dizeleriyle - Premium aaaControl | Microsoft Docs"
description: "Azure CDN sorgu dizesini önbelleğe alma denetimleri nasıl sorgu dizeleri içerdiğinde önbelleğe toobe dosyalarıdır."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5c97cf0230ae13fd378bfce49481f3135a5ef101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a>Denetim Azure CDN önbelleğe alma davranışını sorgu dizeleriyle - Premium
> [!div class="op_single_selector"]
> * [Standart](cdn-query-string.md)
> * [Verizon'dan Azure CDN Premium](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a>Genel Bakış
Sorgu dizeleri içerdiğinde önbelleğe toobe nasıl dosyalarıdır denetimleri önbelleğe alma sorgu dizesi.

> [!IMPORTANT]
> Merhaba standart ve Premium CDN ürünler sağlar hello aynı sorgu dizesini önbelleğe alma işlevselliği, ancak hello kullanıcı arabirimi farklıdır.  Merhaba arabirimi için bu belgede açıklanan **verizon'dan Azure CDN Premium**.  İle sorgu dizesi önbelleğe alma için **akamai'den Azure CDN standart** ve **verizon'dan Azure CDN standart**, bkz: [CDN önbelleğe alma davranışını denetleme, sorgu dizeleri içeren istekleri](cdn-query-string.md).
> 
> 

Üç modu kullanılabilir:

* **Standart önbellek**: hello varsayılan mod budur.  Merhaba CDN kenar düğümüne hello sorgu dizesi hello ilk istek ve önbellek hello varlık hello istek sahibi toohello kaynaktan geçer.  Merhaba önbelleğe alınan varlık süresi doluncaya kadar hello kenar düğümden sunulan tüm istekler bu varlık için hello sorgu dizesi göz ardı eder.
* **Hayır-cache**: Bu modda, hello CDN kenar düğümüne sorgu dizeleri içeren istekleri önbelleğe alınmaz.  Merhaba kenar düğümüne hello varlık doğrudan hello kaynaktan alır ve her istek ile toohello istek sahibi geçirir.
* **Önbellek benzersiz**: Bu mod, kendi önbelleği ile benzersiz bir varlık olarak bir sorgu dizesi her bir istekle değerlendirir.  Örneğin, yanıt için bir istek için hello kaynaktan hello *foo.ashx?q=bar* o aynı sorgu dizesi ile sonraki önbellekler için döndürülen ve hello kenar düğümüne önbelleğe.  Bir istek için *foo.ashx?q=somethingelse* toolive kendi süresiyle ayrı bir varlık olarak önbelleğe alınması.

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a>Sorgu dizesini önbelleğe alma premium CDN profili ayarlarını değiştirme
1. Merhaba CDN profili dikey penceresinden hello tıklayın **Yönet** düğmesi.
   
    ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    Merhaba CDN Yönetim Portalı açar.
2. Merhaba üzerine getirin **HTTP büyük** sekmesini ve ardından hello üzerine getirin **önbellek ayarları** çıkma.  Tıklayın **sorgu dizesi önbelleğe alma**.
   
    Sorgu dizesini önbelleğe alma seçenekleri görüntülenir.
   
    ![CDN sorgu dizesini önbelleğe alma seçenekleri](./media/cdn-query-string-premium/cdn-query-string.png)
3. Seçiminizi yaptıktan sonra hello tıklatın **güncelleştirme** düğmesi.

> [!IMPORTANT]
> Merhaba kayıt toopropagate hello CDN aracılığıyla süredir yararlanırken hello ayarları değişiklikleri hemen görünür olmayabilir.  <b>Verizon'dan Azure CDN</b> profilleri için yayma işlemi genellikle 90 dakika içinde tamamlanır ancak bazı durumlarda daha uzun sürebilir.
> 
> 

