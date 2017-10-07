---
title: "logic apps içinde aaaAdd hello sorgu eylemi | Microsoft Docs"
description: "Filtre dizisi gibi eylemleri gerçekleştirmek için hello sorgu eylemi genel bakış."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: 3d4be901e7e6bf1b644057648930667ab34f2124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-query-action"></a>Merhaba sorgu eylemi ile çalışmaya başlama
Merhaba sorgu eylemini kullanarak toplu ve diziler tooaccomplish iş akışları için çalışabilirsiniz:

* Tüm yüksek öncelikli kayıtları için bir görev veritabanından oluşturun.
* Bir Azure blob e-postalara tüm PDF ekleri kaydedin.

bir mantıksal uygulama Hello sorgu eylemi kullanmaya tooget bkz [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-query-action"></a>Merhaba sorgu eylemi kullanın
Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir. [Eylemler hakkında daha fazla bilgi](connectors-overview.md).  

Merhaba sorgu eylemi, şu anda hello Tasarımcısı'nda gösterilen hello filtre dizisi adlı bir işlem yok. Bu tooquery bir dizi verir ve filtrelenmiş sonuç kümesi döndürür.

İşte nasıl bir mantıksal uygulama ekleyebilirsiniz:

1. Select hello **yeni adım** düğmesi.
2. Seçin **Eylem Ekle**.
3. Merhaba eylem arama kutusuna yazın **filtre** toolist hello **filtre dizisi** eylem.
   
    ![Merhaba sorgu eylemi seçin](./media/connectors-native-query/using-action-1.png)
4. Bir dizi toofilter seçin. (Merhaba aşağıdaki ekran görüntüsünde bir Twitter Arama sonuçlarından hello dizisi gösterir.)
5. Bir koşul tooevaluate her bir öğede oluşturun. (ekran aşağıdaki hello tweet'leri 100'den fazla followers olan kullanıcılardan filtreler.)
   
    ![Tam hello sorgu eylemi](./media/connectors-native-query/using-action-2.png)
   
    Merhaba eylemin hello filtre gereksinimlerini karşılaması sonuçlarını içeren yeni bir dizi çıkarır.
6. Merhaba sol üst köşesindeki hello araç toosave ve, logic app kazandırır hem'ı tıklatın ve yayımlama (etkinleştirin).

## <a name="query-action"></a>Sorgu eylemi
Aşağıda, bu bağlayıcıyı destekler hello eylemin hello Ayrıntılar verilmiştir. Merhaba Bağlayıcısı olası eylem vardır.

| Eylem | Açıklama |
| --- | --- |
| Filtre dizisi |Dizideki her öğe için bir koşulu değerlendirir ve hello sonuçları döndürür |

## <a name="action-details"></a>Eylem ayrıntıları
Merhaba sorgu eylemi bir olası eylemiyle birlikte gelir. Merhaba aşağıdaki tablolar hello gerekli ve isteğe bağlı giriş alanları hello eylem ve hello eylemini kullanarak ile ilişkili hello karşılık gelen çıkış ayrıntıları için açıklamaktadır.

### <a name="filter-array"></a>Filtre dizisi
Merhaba, HTTP giden isteğinde hello eylemi için girdi alanlarının verilmiştir.
A * gerekli bir alan olduğu anlamına gelir.

| Görünen ad | Özellik adı | Açıklama |
| --- | --- | --- |
| Gelen * |Kaynak |Merhaba dizi toofilter |
| Koşul * |Burada |her öğe için bir koşul tooevaluate hello |

<br>

### <a name="output-details"></a>Çıkış Ayrıntıları
Merhaba, hello HTTP yanıtının çıkış ayrıntıları verilmiştir.

| Özellik adı | Veri türü | Açıklama |
| --- | --- | --- |
| Filtrelenmiş dizisi |Dizi |Her filtre uygulanmış bir sonucu için bir nesne içeren bir dizi |

## <a name="next-steps"></a>Sonraki adımlar
Şimdi, hello platform deneyin ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md). Keşfedebilirsiniz bakarak logic apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).

