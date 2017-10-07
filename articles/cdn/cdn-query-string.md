---
title: "Azure CDN önbelleğe alma davranışını sorgu dizeleriyle aaaControl | Microsoft Docs"
description: "Azure CDN sorgu dizesini önbelleğe alma denetimleri nasıl sorgu dizeleri içerdiğinde önbelleğe toobe dosyalarıdır."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 17410e4f-130e-489c-834e-7ca6d6f9778d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e7a138b2decec624a29eb703ad9a291d19c44ee8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a>Denetim Azure CDN önbelleğe alma davranışını sorgu dizeleriyle etkinleştirmek
> [!div class="op_single_selector"]
> * [Standart](cdn-query-string.md)
> * [Verizon'dan Azure CDN Premium](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a>Genel Bakış
Sorgu dizeleri içerdiğinde önbelleğe toobe nasıl dosyalarıdır denetimleri önbelleğe alma sorgu dizesi.

> [!IMPORTANT]
> Merhaba standart ve Premium CDN ürünler sağlar hello aynı sorgu dizesini önbelleğe alma işlevselliği, ancak hello kullanıcı arabirimi farklıdır.  Merhaba arabirimi için bu belgede açıklanan **akamai'den Azure CDN standart** ve **verizon'dan Azure CDN standart**.  İle sorgu dizesi önbelleğe alma için **verizon'dan Azure CDN Premium**, bkz: [CDN önbelleğe alma davranışını denetleme istekleri sorgu dizeleriyle - Premium](cdn-query-string-premium.md).
> 
> 

Üç modu kullanılabilir:

* **Sorgu dizelerini yoksayabilir**: hello varsayılan mod budur.  Merhaba CDN kenar düğümüne hello sorgu dizesi hello ilk istek ve önbellek hello varlık hello istek sahibi toohello kaynaktan geçer.  Merhaba önbelleğe alınan varlık süresi doluncaya kadar hello kenar düğümden sunulan tüm istekler bu varlık için hello sorgu dizesi göz ardı eder.
* **Sorgu dizeleri içeren URL için önbelleğe almayı atla**: Bu modda, hello CDN kenar düğümüne sorgu dizeleri içeren istekleri önbelleğe alınmaz.  Merhaba kenar düğümüne hello varlık doğrudan hello kaynaktan alır ve her istek ile toohello istek sahibi geçirir.
* **Her benzersiz URL'yi önbelleğe**: Bu mod, kendi önbelleği ile benzersiz bir varlık olarak bir sorgu dizesi her bir istekle değerlendirir.  Örneğin, yanıt için bir istek için hello kaynaktan hello *foo.ashx?q=bar* o aynı sorgu dizesi ile sonraki önbellekler için döndürülen ve hello kenar düğümüne önbelleğe.  Bir istek için *foo.ashx?q=somethingelse* toolive kendi süresiyle ayrı bir varlık olarak önbelleğe alınması.

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a>Sorgu dizesini önbelleğe alma standart CDN profili ayarlarını değiştirme
1. Merhaba CDN profili dikey penceresinden toomanage istediğiniz hello CDN uç noktası'ı tıklatın.
   
    ![CDN profili dikey uç noktaları](./media/cdn-query-string/cdn-endpoints.png)
   
    Merhaba CDN uç noktası dikey pencere açılır.
2. Merhaba tıklatın **yapılandırma** düğmesi.
   
    ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-query-string/cdn-config-btn.png)
   
    Merhaba CDN yapılandırma dikey pencere açılır.
3. Merhaba bir ayar seçin **sorgu dizesini önbelleğe alma davranışı** açılır.
   
    ![CDN sorgu dizesini önbelleğe alma seçenekleri](./media/cdn-query-string/cdn-query-string.png)
4. Seçiminizi yaptıktan sonra hello tıklatın **kaydetmek** düğmesi.

> [!IMPORTANT]
> Merhaba kayıt toopropagate hello CDN aracılığıyla süredir yararlanırken hello ayarları değişiklikleri hemen görünür olmayabilir.  <b>Akamai'den Azure CDN</b> profilleri için yayma işlemi genellikle bir dakika içinde tamamlanır.  <b>Verizon'dan Azure CDN</b> profilleri için yayma işlemi genellikle 90 dakika içinde tamamlanır ancak bazı durumlarda daha uzun sürebilir.
> 
> 

