---
title: "oluşturma ve Azure günlük analizi günlük sorgularda düzenleme aaaPortals | Microsoft Docs"
description: "Bu makalede Azure günlük analizi toocreate kullanın ve günlük aramaları düzenleme hello portalları açıklanmaktadır."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 7a2657574a132b2c4298511bb31259e68113ac91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="portals-for-creating-and-editing-log-queries-in-azure-log-analytics"></a>Oluşturma ve Azure günlük analizi günlük sorgularda düzenleme için portalları

> [!NOTE]
> Bu makalede Azure günlük analizi hello yeni sorgu dili kullanarak portallarında açıklanmaktadır.  Merhaba yeni dil hakkında daha fazla bilgi ve çalışma alanı hello yordamı tooupgrade almak [Azure günlük analizi çalışma alanı toonew günlük aramanızı yükseltme](log-analytics-log-search-upgrade.md).  
>
> Çalışma alanınızı yükseltilmiş toohello yeni sorgu dili bırakılmamışsa, çok başvurmalıdır[Bul günlük aramaları günlük analizi kullanarak verileri](log-analytics-log-searches.md) hello hello günlük arama Portalı'nın geçerli sürümü hakkında bilgi için.

Günlük analizi tooretrieve veri yerlerde çeşitli günlük aramaları hello çalışma alanından kullanın.  Gerçekte oluşturmak ve sorguları düzenleme için aşağıda açıklanan iki seçeneğiniz vardır, ayrıca tooworking etkileşimli olarak ile veri ancak döndürdü.  

## <a name="log-search-portal"></a>Günlük arama portalı
Merhaba günlük arama portal hello Azure portal veya hello OMS portalı erişilebilir.  Tek bir satıra oluşturulabilir temel sorguları oluşturmak için uygundur.  bir dış portal başlatmadan Hello günlük arama portal kullanılabilir ve tooperform işlevleri, çeşitli uyarı kuralları oluşturma, bilgisayar gruplarını oluşturma ve hello hello sorgunun sonuçlarını dışarı aktarma gibi günlük aramaları ile kullanabilirsiniz.  

Merhaba günlük arama portal hello sorgu dili hakkında tam bilgi gerek kalmadan hello sorguyu düzenlemek için birden çok özellik sağlar.  Bu özelliklerin özetini almak [oluşturma günlük hello günlük arama portalı kullanarak Azure günlük analizi aramalarda](log-analytics-log-search-log-search-portal.md).


![Arama portalında oturum açın](media/log-analytics-log-search-portals/log-search-portal.png)

## <a name="advanced-analytics-portal"></a>Gelişmiş Analytics portalı
Merhaba gelişmiş analizler portal hello günlük arama Portalı'nda kullanılamıyor gelişmiş işlevselliği sağlayan adanmış bir portalıdır.  Özellikler hello özelliği tooedit sorguda birden çok satıra içerir, seçime bağlı olarak kod, içeriğe duyarlı IntelliSense ve akıllı Analytics yürütün.  Merhaba Advanced Analytics portal ya da günlük arama kaydedilmiş veya kopyalanır ve diğer günlük analizi elemanlara yapıştırılan karmaşık sorgular tasarlamak için en uygun durumda.  Merhaba Advanced Analytics portalından hello günlük arama Portalı'nda bir bağlantıyı başlatın.

![Gelişmiş Analytics portalı](media/log-analytics-log-search-portals/advanced-analytics-portal.png)


Gelişmiş özelliklerini nedeniyle, genellikle hello gelişmiş analizler portal birincil aracınız olarak oluşturmak ve sorguları düzenleme için kullanırsınız.  Merhaba sorgu beklendiği gibi çalışır ve ardından kopyalayıp hello günlük arama portalı veya Görünüm Tasarımcısı gibi başka bir yere yapıştırın saptadıktan sonra.  Merhaba Advanced Analytics portalı birden fazla satır sorgularıyla ancak desteklediğinden, bir sorgu bu portaldan kopyalarken tootake hello aşağıdakileri göz önünde bulundurmanız gerekir.

- Kopyalanır ve başka bir konuma yapıştırılan önce açıklamaları hello sorgudan kaldırılması gerekir.  İki eğik çizgi ile koyarak bir satır yorum yapabileceği (/ /).  Tek bir satıra birden çok satır sorgu yapıştırın, satır sonları kaldırılır.  Yorumlar eklenirse hello ilk açıklama sonra tüm karakterleri hello yorum bir parçası olarak kabul edilir.


## <a name="next-steps"></a>Sonraki adımlar

- Bir öğreticide hello kullanarak yol [günlük arama portal](log-analytics-log-search-log-search-portal.md) veya hello [Advanced Analytics portalı](https://go.microsoft.com/fwlink/?linkid=856587) toocreate sorgular.
- Kullanıma bir [sorgu yazmakla ilgili öğretici](https://go.microsoft.com/fwlink/?linkid=856078) hello yeni sorgu dilini kullanma.
