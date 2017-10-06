---
title: "Görünüm Tasarımcısı'nda OMS günlük analizi için aaaPart başvurusu | Microsoft Docs"
description: "Görünüm Tasarımcısı'nda günlük analizi sağlar, toocreate özel hello OMS konsolundaki hello OMS deposundaki verileri farklı görselleştirmesini içeren görünümler. Bu makalede hello ayarlarının hello görselleştirme bölümleri kullanılabilir toouse kendi özel görünümlerinizi de her bir başvuru sağlar."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: 5718d620-b96e-4d33-8616-e127ee9379c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 6a19a451cf4cefd2fa5c94e6f61d812c4f820f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-view-designer-visualization-part-reference"></a>Günlük analizi Görünüm Tasarımcısı görselleştirme bölümü başvurusu
Merhaba Görünüm Tasarımcısı'nda günlük analizi, farklı veri görselleştirmeleri hello OMS depodan içeren toocreate özel görünümler hello OMS konsolunda sağlar. Bu makalede hello ayarlarının hello görselleştirme bölümleri kullanılabilir toouse kendi özel görünümlerinizi de her bir başvuru sağlar.

Görünüm Tasarımcısı için kullanılabilir diğer makaleler şunlardır:

* [Görüntüleme Tasarımcısı](log-analytics-view-designer.md) -hello Görünüm Tasarımcısı ve oluşturma ve özel görünümler düzenleme yordamları genel bakış.
* [Döşeme başvuru](log-analytics-view-designer-tiles.md) -başvuru hello ayarlarının her hello için kendi özel görünümlerinizi de kullanılabilir toouse yerleştirir.

>[!NOTE]
> Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), tüm görünümleri sorgularda hello yazılmalıdır sonra [yeni sorgu dili](https://go.microsoft.com/fwlink/?linkid=856078).  Merhaba çalışma yükseltilmeden önce oluşturulan görünümleri dönüştürülen automtically olacaktır.

Merhaba aşağıdaki tabloda döşeme hello Görünüm Tasarımcısı kullanılabilir hello farklı türleri açıklanmaktadır.  Aşağıdaki Hello bölümler her döşeme türü ayrıntı ve bunların özelliklerini açıklar.

| Görünüm türü | Açıklama |
|:--- |:--- |
| [Sorgu listesi](#list-of-queries-part) |Günlük arama sorguları listesini görüntüler.  Merhaba kullanıcı her sorgu toodisplay sonuçlarını tıklatabilirsiniz. |
| [Sayı & listesi](#number-amp-list-part) |Üstbilgisi tek sayı gösteren kayıt sayısı günlük arama sorgusundan sahiptir.  Liste hello üst on bir sorgunun sonuçlarına hello göreli değerini sayısal bir sütun veya zaman içinde değişiklik gösteren bir grafiği görüntüler. |
| [İki sayı & listesi](#two-numbers-amp-list-part) |Üstbilgisi ayrı günlük arama sorgularından kayıt sayısını gösteren iki sayının sahiptir.  Liste hello üst on bir sorgunun sonuçlarına hello göreli değerini sayısal bir sütun veya zaman içinde değişiklik gösteren bir grafiği görüntüler. |
| [Halka & listesi](#donut-amp-list-part) |Üstbilgi, günlük sorguda değer sütundan özetlenen tek bir sayı görüntüler.  Merhaba halka grafik hello üst üç kayıt sonuçlarını görüntüler. |
| [İki zaman çizelgelerini & listesi](#two-timelines-amp-list-part) |Günlük sorguda değer sütundan üstbilgi görüntüler hello sütun grafikleri ile tek bir sayı görüntüleme belirtme çizgisi olarak zaman içinde iki günlük sorguların sonuçlarını özetlenir.  Liste hello üst on bir sorgunun sonuçlarına hello göreli değerini sayısal bir sütun veya zaman içinde değişiklik gösteren bir grafiği görüntüler. |
| [Bilgi](#information-part) |Üstbilgi statik metin ve isteğe bağlı bir bağlantı gösterir.  Bir veya daha fazla öğeleriyle statik metin ve başlık görüntüler. |
| [Çizgi grafiği, belirtme çizgisi & listesi](#line-chart-callout-amp-list-part) |Üstbilgi saati ve bir belirtme çizgisi özetlenen bir değerle üzerinden birden fazla dizi günlük sorgudan bir çizgi grafiği görüntüler.  Liste hello üst on bir sorgunun sonuçlarına hello göreli değerini sayısal bir sütun veya zaman içinde değişiklik gösteren bir grafiği görüntüler. |
| [Çizgi grafiği & listesi](#line-chart-amp-list-part) |Üstbilgi zaman içinde birden fazla dizi günlük sorgudan bir çizgi grafiği görüntüler.  Liste hello üst on bir sorgunun sonuçlarına hello göreli değerini sayısal bir sütun veya zaman içinde değişiklik gösteren bir grafiği görüntüler. |
| [Çizgi grafikler bölümü yığını](#stack-of-line-charts-part) |Birden fazla seri günlük sorgudan üç ayrı çizgi grafiklerde zaman içinde görüntüler. |

## <a name="list-of-queries-part"></a>Sorguları bölümü listesi
Günlük arama sorguları listesini görüntüler.  Merhaba kullanıcı her sorgu toodisplay sonuçlarını tıklatabilirsiniz.  Merhaba görünüm varsayılan olarak tek bir sorgu içerir ve tıklayabilirsiniz **+ sorgu** tooadd ek sorgular.

![Sorgular görünümünü listesi](media/log-analytics-view-designer/view-list-queries.png)

| Ayar | Açıklama |
|:--- |:--- |
| **Genel** | |
| Başlık |Metin toodisplay hello görünümünün hello üstünde. |
| Yeni Grup |Merhaba geçerli Sergi başlangıç hello görünümünde toocreate yeni bir grup seçin. |
| Önceden seçilen filtreleri |Merhaba kullanıcı bir sorgu seçtiğinde virgülle ayrılmış hello sol Filtre bölmesinde özellikleri tooinclude listesi. |
| Mod işleme |Merhaba sorgu seçildiğinde görüntülenen ilk görüntüleyin.  Merhaba kullanıcı hello sorgu açtıktan sonra herhangi bir kullanılabilir görünüm seçebilirsiniz. |
| **Sorgular** | |
| Arama sorgusu |Sorgu toorun. |
| Kolay ad |Merhaba sorgu toodisplay toohello kullanıcı açıklayıcı adı. |

## <a name="number--list-part"></a>Sayı & listesi bölümü
Üstbilgisi tek sayı gösteren kayıt sayısı günlük arama sorgusundan sahiptir.  Liste hello üst on bir sorgunun sonuçlarına hello göreli değerini sayısal bir sütun veya zaman içinde değişiklik gösteren bir grafiği görüntüler.

![Sorgular görünümünü listesi](media/log-analytics-view-designer/view-number-list.png)

| Ayar | Açıklama |
|:--- |:--- |
| **Genel** | |
| Grup başlığı |Metin toodisplay hello görünümünün hello üstünde. |
| Yeni Grup |Merhaba geçerli Sergi başlangıç hello görünümünde toocreate yeni bir grup seçin. |
| Simgesi |Görüntü dosyası toodisplay sonraki toohello sonucunda hello üstbilgi. |
| Simgesini kullanın |Toohave hello simgesi görüntü seçin. |
| **Başlık** | |
| Gösterge |Metin toodisplay hello üstbilgisinin hello üstünde. |
| Sorgu |Sorgu toorun hello üstbilgisi.  Merhaba hello sorgu tarafından döndürülen kayıt sayısını Hello sayısı görüntülenir. |
| **Liste** | |
| Sorgu |Sorgu toorun hello listesi.  ilk iki özelliklerini hello Hello ilk on kaydeder hello sonuçları görüntülenir.  Merhaba ilk özelliği bir metin değeri ve hello ikinci özelliğini sayısal bir değer olmalıdır.  Çubukları hello göreli hello sayısal sütun değerine göre otomatik olarak oluşturulur.<br><br>Merhaba sorgu toosort hello kayıtlarında hello listesinde Hello sıralama komutunu kullanın.  Merhaba kullanıcı tıklatabilirsiniz sorgulamak ve tüm kayıtları döndürmek tüm toorun hello bakın. |
| Grafik Gizle |Toodisable hello grafik toohello hakkı hello sayısal sütun seçin. |
| Mini Grafikler etkinleştir |Yatay çubuk yerine toodisplay mini grafik seçin.  Bkz: [ortak ayarları](#sparklines) Ayrıntılar için. |
| Renk |Merhaba çubukları veya Mini Grafikler rengi. |
| Ad ve değer ayırıcı |Tooparse hello metin özelliği birden fazla değer istiyorsanız, tek karakter sınırlayıcısı.  Bkz: [ortak ayarları](#name-value-separator) Ayrıntılar için. |
| Gezinti sorgu |Merhaba kullanıcı hello listesinden bir öğe seçtiğinde toorun sorgu.  Bkz: [ortak ayarları](#navigation-query) Ayrıntılar için. |
| **Liste** |**> Sütun başlıkları** |
| Ad |Metin toodisplay hello listesinin ilk sütun hello hello üstünde. |
| Değer |Metin toodisplay hello listesinin hello ikinci sütunun hello üstünde. |
| **Liste** |**> Eşikleri** |
| Eşikleri etkinleştir |Tooenable eşikleri seçin.  Bkz: [ortak ayarları](#thresholds) Ayrıntılar için. |

## <a name="two-numbers--list-part"></a>İki sayı & Liste bölümü
Üstbilgisi ayrı günlük arama sorgularından kayıt sayısını gösteren iki sayının sahiptir.  Liste hello üst on bir sorgunun sonuçlarına hello göreli değerini sayısal bir sütun veya zaman içinde değişiklik gösteren bir grafiği görüntüler.

![İki sayı & Liste Görünümü](media/log-analytics-view-designer/view-two-numbers-list.png)

| Ayar | Açıklama |
|:--- |:--- |
| **Genel** | |
| Grup başlığı |Metin toodisplay hello görünümünün hello üstünde. |
| Yeni Grup |Merhaba geçerli Sergi başlangıç hello görünümünde toocreate yeni bir grup seçin. |
| Simgesi |Görüntü dosyası toodisplay sonraki toohello sonucunda hello üstbilgi. |
| Simgesini kullanın |Toohave hello simgesi görüntü seçin. |
| **Başlık** | |
| Gösterge |Metin toodisplay hello üstbilgisinin hello üstünde. |
| Sorgu |Sorgu toorun hello üstbilgisi.  Merhaba hello sorgu tarafından döndürülen kayıt sayısını Hello sayısı görüntülenir. |
| **Liste** | |
| Sorgu |Sorgu toorun hello listesi.  ilk iki özelliklerini hello Hello ilk on kaydeder hello sonuçları görüntülenir.  Merhaba ilk özelliği bir metin değeri ve hello ikinci özelliğini sayısal bir değer olmalıdır.  Çubukları hello göreli hello sayısal sütun değerine göre otomatik olarak oluşturulur.<br><br>Merhaba sorgu toosort hello kayıtlarında hello listesinde Hello sıralama komutunu kullanın.  Merhaba kullanıcı tıklatabilirsiniz sorgulamak ve tüm kayıtları döndürmek tüm toorun hello bakın. |
| Grafik Gizle |Toodisable hello grafik toohello hakkı hello sayısal sütun seçin. |
| Mini Grafikler etkinleştir |Yatay çubuk yerine toodisplay mini grafik seçin.  Bkz: [ortak ayarları](#sparklines) Ayrıntılar için. |
| Renk |Merhaba çubukları veya Mini Grafikler rengi. |
| İşlem |Merhaba Mini Grafik işlem tooperform.  Bkz: [ortak ayarları](#sparklines) Ayrıntılar için. |
| Ad ve değer ayırıcı |Tooparse hello metin özelliği birden fazla değer istiyorsanız, tek karakter sınırlayıcısı.  Bkz: [ortak ayarları](#name-value-separator) Ayrıntılar için. |
| Gezinti sorgu |Merhaba kullanıcı hello listesinden bir öğe seçtiğinde toorun sorgu.  Bkz: [ortak ayarları](#navigation-query) Ayrıntılar için. |
| **Liste** |**> Sütun başlıkları** |
| Ad |Metin toodisplay hello listesinin ilk sütun hello hello üstünde. |
| Değer |Metin toodisplay hello listesinin hello ikinci sütunun hello üstünde. |
| **Liste** |**> Eşikleri** |
| Eşikleri etkinleştir |Tooenable eşikleri seçin.  Bkz: [ortak ayarları](#thresholds) Ayrıntılar için. |

## <a name="donut--list-part"></a>Halka & listesi bölümü
Üstbilgi, günlük sorguda değer sütundan özetlenen tek bir sayı görüntüler.  Merhaba halka grafik hello üst üç kayıt sonuçlarını görüntüler.

![Halka & Liste Görünümü](media/log-analytics-view-designer/view-donut-list.png)

| Ayar | Açıklama |
|:--- |:--- |
| **Genel** | |
| Grup başlığı |Metin toodisplay hello hello üstündeki döşeme. |
| Yeni Grup |Merhaba geçerli Sergi başlangıç hello görünümünde toocreate yeni bir grup seçin. |
| Simgesi |Görüntü dosyası toodisplay sonraki toohello sonucunda hello üstbilgi. |
| Simgesini kullanın |Toohave hello simgesi görüntü seçin. |
| **Üstbilgi** | |
| Başlık |Metin toodisplay hello üstbilgisinin hello üstünde. |
| Alt Başlığı |Metin toodisplay hello hello üstbilgisinin hello üstünde başlık altında. |
| **Halka** | |
| Sorgu |Merhaba halka toorun sorgu.  Merhaba ilk özelliği bir metin değeri ve hello ikinci özelliğini sayısal bir değer olmalıdır. |
| **Halka** |**> Merkezi** |
| Metin |Metin toodisplay hello halka içindeki hello değeri altında. |
| İşlem |Merhaba işlemi tooperform hello değer özelliği toosummarize tooa tek değeri.<br><br>-TOPLA: tüm kayıtların hello değerlerini ekleyin.<br>-Yüzdesi: Merhaba değerleri tarafından döndürülen hello kayıtları yüzdesi **neden merkezi işleminde kullanılan değerleri** hello sorgusunda toohello toplam kaydı. |
| Merkezi işleminde kullanılan sonuç değerleri |İsteğe bağlı olarak tıklatın hello artı tooadd bir veya daha fazla değer.  Merhaba hello sorgunun sonuçlarını belirttiğiniz hello özellik değerleri ile sınırlı toorecords olacaktır.  Hiçbir değer eklediyseniz, tüm kayıtları hello sorguya dahil edilir. |
| **Ek Seçenekler** |**> Renkleri** |
| Rengi 1<br>Renk 2<br>Rengi 3 |Merhaba her hello halka görüntülenen hello değerlerin Hello rengini seçin. |
| **Ek Seçenekler** |**> Gelişmiş renk eşleme** |
| Alan değeri |Tür hello alan toodisplay adını hello halka eklenirse farklı bir renk olarak. |
| Renk |Merhaba benzersiz alan Hello rengini seçin. |
| **Liste** | |
| Sorgu |Sorgu toorun hello listesi.  Merhaba hello sorgu tarafından döndürülen kayıt sayısını Hello sayısı görüntülenir. |
| Grafik Gizle |Toodisable hello grafik toohello hakkı hello sayısal sütun seçin. |
| Mini Grafikler etkinleştir |Yatay çubuk yerine toodisplay mini grafik seçin.  Bkz: [ortak ayarları](#sparklines) Ayrıntılar için. |
| Renk |Merhaba çubukları veya Mini Grafikler rengi. |
| İşlem |Merhaba Mini Grafik işlem tooperform.  Bkz: [ortak ayarları](#sparklines) Ayrıntılar için. |
| Ad ve değer ayırıcı |Tooparse hello metin özelliği birden fazla değer istiyorsanız, tek karakter sınırlayıcısı.  Bkz: [ortak ayarları](#name-value-separator) Ayrıntılar için. |
| Gezinti sorgu |Merhaba kullanıcı hello listesinden bir öğe seçtiğinde toorun sorgu.  Bkz: [ortak ayarları](#navigation-query) Ayrıntılar için. |
| **Liste** |**> Sütun başlıkları** |
| Ad |Metin toodisplay hello listesinin ilk sütun hello hello üstünde. |
| Değer |Metin toodisplay hello listesinin hello ikinci sütunun hello üstünde. |
| **Liste** |**> Eşikleri** |
| Eşikleri etkinleştir |Tooenable eşikleri seçin.  Bkz: [ortak ayarları](#thresholds) Ayrıntılar için. |

## <a name="two-timelines--list-part"></a>İki zaman çizelgelerini & listesi bölümü
Günlük sorguda değer sütundan üstbilgi görüntüler hello sütun grafikleri ile tek bir sayı görüntüleme belirtme çizgisi olarak zaman içinde iki günlük sorguların sonuçlarını özetlenir.  Liste hello üst on bir sorgunun sonuçlarına hello göreli değerini sayısal bir sütun veya zaman içinde değişiklik gösteren bir grafiği görüntüler.

![İki zaman çizelgelerini & listesini görüntüleyin](media/log-analytics-view-designer/view-two-timelines-list.png)

| Ayar | Açıklama |
|:--- |:--- |
| **Genel** | |
| Grup başlığı |Metin toodisplay hello hello üstündeki döşeme. |
| Yeni Grup |Merhaba geçerli Sergi başlangıç hello görünümünde toocreate yeni bir grup seçin. |
| Simgesi |Görüntü dosyası toodisplay sonraki toohello sonucunda hello üstbilgi. |
| Simgesini kullanın |Toohave hello simgesi görüntü seçin. |
| **İlk grafik<br>ikinci grafik** | |
| Gösterge |Metin toodisplay hello belirtme çizgisi hello ilk serisinin altında. |
| Renk |Toouse hello sütunlar hello seri için renk. |
| Sorgu |Sorgu toorun hello ilk seri için.  her zaman aralığı içindeki kayıtları hello sayısı Merhaba sayımını hello grafik sütunlara göre temsil edilir. |
| İşlem |Merhaba işlemi tooperform hello değer özelliği toosummarize tooa için tek bir değer hello belirtme çizgisi üzerinde.<br><br>-TOPLA: Tüm kayıtları hello değerinden toplamı.<br>-Ortalama: Tüm kayıtları hello değerinden ortalama.<br>-Son örnek: Merhaba son aralığı hello grafikte dahil değeri.<br>-İlk örneği: Merhaba grafikte dahil hello ilk aralığı değeri.<br>-Count: Hello sorgu tarafından döndürülen tüm kayıtların sayısı. |
| **Liste** | |
| Sorgu |Sorgu toorun hello listesi.  Merhaba hello sorgu tarafından döndürülen kayıt sayısını Hello sayısı görüntülenir. |
| Grafik Gizle |Toodisable hello grafik toohello hakkı hello sayısal sütun seçin. |
| Mini Grafikler etkinleştir |Yatay çubuk yerine toodisplay mini grafik seçin.  Bkz: [ortak ayarları](#sparklines) Ayrıntılar için. |
| Renk |Merhaba çubukları veya Mini Grafikler rengi. |
| İşlem |Merhaba Mini Grafik işlem tooperform.  Bkz: [ortak ayarları](#sparklines) Ayrıntılar için. |
| Gezinti sorgu |Merhaba kullanıcı hello listesinden bir öğe seçtiğinde toorun sorgu.  Bkz: [ortak ayarları](#navigation-query) Ayrıntılar için. |
| **Liste** |**> Sütun başlıkları** |
| Ad |Metin toodisplay hello listesinin ilk sütun hello hello üstünde. |
| Değer |Metin toodisplay hello listesinin hello ikinci sütunun hello üstünde. |
| **Liste** |**> Eşikleri** |
| Eşikleri etkinleştir |Tooenable eşikleri seçin.  Bkz: [ortak ayarları](#thresholds) Ayrıntılar için. |

## <a name="information-part"></a>Bilgi bölümü
Üstbilgi statik metin ve isteğe bağlı bir bağlantı gösterir.  Bir veya daha fazla öğeleriyle statik metin ve başlık görüntüler.

![Bilgileri görüntüle](media/log-analytics-view-designer/view-information.png)

| Ayar | Açıklama |
|:--- |:--- |
| **Genel** | |
| Grup başlığı |Metin toodisplay hello hello üstündeki döşeme. |
| Yeni Grup |Merhaba geçerli Sergi başlangıç hello görünümünde toocreate yeni bir grup seçin. |
| Renk |Merhaba üstbilgi arka plan rengi. |
| **Üstbilgi** | |
| Görüntü |Görüntü dosyası toodisplay hello üstbilgisinde. |
| Etiket |Merhaba üst bilgisindeki metin toodisplay. |
| **Üstbilgi** |**> Bağlantı** |
| Etiket |Bağlantı metni. |
| Url |Bağlantı için URL. |
| **Bilgi öğeleri** | |
| Başlık |Her öğesinin metin toodisplay. |
| İçerik |Her öğe için metin toodisplay. |

## <a name="line-chart-callout--list-part"></a>Çizgi grafiği, belirtme çizgisi & Liste bölümü
Üstbilgi saati ve bir belirtme çizgisi özetlenen bir değerle üzerinden birden fazla dizi günlük sorgudan bir çizgi grafiği görüntüler.  Liste hello üst on bir sorgunun sonuçlarına hello göreli değerini sayısal bir sütun veya zaman içinde değişiklik gösteren bir grafiği görüntüler.

![Çizgi grafiği, belirtme çizgisi & Liste Görünümü](media/log-analytics-view-designer/view-line-chart-callout-list.png)

| Ayar | Açıklama |
|:--- |:--- |
| **Genel** | |
| Grup başlığı |Metin toodisplay hello hello üstündeki döşeme. |
| Yeni Grup |Merhaba geçerli Sergi başlangıç hello görünümünde toocreate yeni bir grup seçin. |
| Simgesi |Görüntü dosyası toodisplay sonraki toohello sonucunda hello üstbilgi. |
| Simgesini kullanın |Toohave hello simgesi görüntü seçin. |
| **Üstbilgi** | |
| Başlık |Metin toodisplay hello üstbilgisinin hello üstünde. |
| Alt Başlığı |Metin toodisplay hello hello üstbilgisinin hello üstünde başlık altında. |
| **Çizgi grafiği** | |
| Sorgu |Sorgu toorun hello çizgi grafiği için.  Merhaba ilk özelliği bir metin değeri ve hello ikinci özelliğini sayısal bir değer olmalıdır.  Bu genellikle hello kullanan bir sorgu olur **ölçü** anahtar sözcüğü toosummarize sonuçları.  Merhaba sorgu hello kullanıyorsa **aralığı** anahtar sözcüğü sonra hello hello grafiğin x ekseni bu zaman aralığı kullanır.  Merhaba sorgu hello içermiyorsa **aralığı** anahtar sözcüğü sonra saatlik aralıklarla hello x ekseni için kullanılır. |
| **Çizgi grafiği** |**> Belirtme** |
| Belirtme çizgisi başlık |Metin toodisplay hello belirtme çizgisi değerin üzerinde. |
| Seri adı |Merhaba serisi toouse hello belirtme çizgisi değeri için özellik değeri.  Seri sağlanırsa, hello sorgudan tüm kayıtları kullanılır. |
| İşlem |Merhaba işlemi tooperform hello değer özelliği toosummarize tooa için tek bir değer hello belirtme çizgisi üzerinde.<br><br>-Ortalama: Tüm kayıtları hello değerinden ortalama.<br>-Merhaba sorgu tarafından döndürülen tüm kayıtları Count sayısı.<br>-Son örnek: Merhaba son aralığı hello grafikte dahil değeri.<br>-Max: Merhaba grafikte dahil hello aralıkları maksimum değeri.<br>-Min: Merhaba grafikte dahil hello aralıkları Minimum değeri.<br>-TOPLA: Tüm kayıtları hello değerinden toplamı. |
| **Çizgi grafiği** |**> Y ekseni** |
| Logaritmik ölçek kullan |Toouse Logaritmik ölçek hello y ekseni için seçin. |
| Birimler |Merhaba sorgu tarafından döndürülen hello değerleri Hello birimlerini belirtin.  Bu bilgiler hello değer türleri belirten hello grafik ve isteğe bağlı olarak hello değerleri dönüştürmek için kullanılan toodisplay etiketlerini olur.  Merhaba birim türü hello biriminin hello kategorisini belirtir ve kullanılabilir hello geçerli birim türü değerleri tanımlar.  Dönüştürme toothen hello sayısal bir değer seçerseniz değerler hello geçerli birim türü toohello dönüştürme tootype dönüştürülür. |
| Özel Etiket |Metin toodisplay hello Y ekseni sonraki toohello etiketinin hello birim türü.  Hiçbir etiket belirtilirse, yalnızca hello birim türü görüntülenir. |
| **Liste** | |
| Sorgu |Sorgu toorun hello listesi.  Merhaba hello sorgu tarafından döndürülen kayıt sayısını Hello sayısı görüntülenir. |
| Grafik Gizle |Toodisable hello grafik toohello hakkı hello sayısal sütun seçin. |
| Mini Grafikler etkinleştir |Yatay çubuk yerine toodisplay mini grafik seçin.  Bkz: [ortak ayarları](#sparklines) Ayrıntılar için. |
| Renk |Merhaba çubukları veya Mini Grafikler rengi. |
| İşlem |Merhaba Mini Grafik işlem tooperform.  Bkz: [ortak ayarları](#sparklines) Ayrıntılar için. |
| Ad ve değer ayırıcı |Tooparse hello metin özelliği birden fazla değer istiyorsanız, tek karakter sınırlayıcısı.  Bkz: [ortak ayarları](#name-value-separator) Ayrıntılar için. |
| Gezinti sorgu |Merhaba kullanıcı hello listesinden bir öğe seçtiğinde toorun sorgu.  Bkz: [ortak ayarları](#navigation-query) Ayrıntılar için. |
| **Liste** |**> Sütun başlıkları** |
| Ad |Metin toodisplay hello listesinin ilk sütun hello hello üstünde. |
| Değer |Metin toodisplay hello listesinin hello ikinci sütunun hello üstünde. |
| **Liste** |**> Eşikleri** |
| Eşikleri etkinleştir |Tooenable eşikleri seçin.  Bkz: [ortak ayarları](#thresholds) Ayrıntılar için. |

## <a name="line-chart--list-part"></a>Satır Grafiği & listesi bölümü
Üstbilgi zaman içinde birden fazla dizi günlük sorgudan bir çizgi grafiği görüntüler.  Liste hello üst on bir sorgunun sonuçlarına hello göreli değerini sayısal bir sütun veya zaman içinde değişiklik gösteren bir grafiği görüntüler.

![Satır Grafiği & Liste Görünümü](media/log-analytics-view-designer/view-line-chart-callout-list.png)

| Ayar | Açıklama |
|:--- |:--- |
| **Genel** | |
| Grup başlığı |Metin toodisplay hello hello üstündeki döşeme. |
| Yeni Grup |Merhaba geçerli Sergi başlangıç hello görünümünde toocreate yeni bir grup seçin. |
| Simgesi |Görüntü dosyası toodisplay sonraki toohello sonucunda hello üstbilgi. |
| Simgesini kullanın |Toohave hello simgesi görüntü seçin. |
| **Üstbilgi** | |
| Başlık |Metin toodisplay hello üstbilgisinin hello üstünde. |
| Alt Başlığı |Metin toodisplay hello hello üstbilgisinin hello üstünde başlık altında. |
| **Çizgi grafiği** | |
| Sorgu |Sorgu toorun hello çizgi grafiği için.  Merhaba ilk özelliği bir metin değeri ve hello ikinci özelliğini sayısal bir değer olmalıdır.  Bu genellikle hello kullanan bir sorgu olur **ölçü** anahtar sözcüğü toosummarize sonuçları.  Merhaba sorgu hello kullanıyorsa **aralığı** anahtar sözcüğü sonra hello hello grafiğin x ekseni bu zaman aralığı kullanır.  Merhaba sorgu hello içermiyorsa **aralığı** anahtar sözcüğü sonra saatlik aralıklarla hello x ekseni için kullanılır. |
| **Çizgi grafiği** |**> Y ekseni** |
| Logaritmik ölçek kullan |Toouse Logaritmik ölçek hello y ekseni için seçin. |
| Birimler |Merhaba sorgu tarafından döndürülen hello değerleri Hello birimlerini belirtin.  Bu bilgiler hello değer türleri belirten hello grafik ve isteğe bağlı olarak hello değerleri dönüştürmek için kullanılan toodisplay etiketlerini olur.  Merhaba birim türü hello biriminin hello kategorisini belirtir ve kullanılabilir hello geçerli birim türü değerleri tanımlar.  Dönüştürme toothen hello sayısal bir değer seçerseniz değerler hello geçerli birim türü toohello dönüştürme tootype dönüştürülür. |
| Özel Etiket |Metin toodisplay hello Y ekseni sonraki toohello etiketinin hello birim türü.  Hiçbir etiket belirtilirse, yalnızca hello birim türü görüntülenir. |
| **Liste** | |
| Sorgu |Sorgu toorun hello listesi.  Merhaba hello sorgu tarafından döndürülen kayıt sayısını Hello sayısı görüntülenir. |
| Grafik Gizle |Toodisable hello grafik toohello hakkı hello sayısal sütun seçin. |
| Mini Grafikler etkinleştir |Yatay çubuk yerine toodisplay mini grafik seçin.  Bkz: [ortak ayarları](#sparklines) Ayrıntılar için. |
| Renk |Merhaba çubukları veya Mini Grafikler rengi. |
| İşlem |Merhaba Mini Grafik işlem tooperform.  Bkz: [ortak ayarları](#sparklines) Ayrıntılar için. |
| Ad ve değer ayırıcı |Tooparse hello metin özelliği birden fazla değer istiyorsanız, tek karakter sınırlayıcısı.  Bkz: [ortak ayarları](#name-value-separator) Ayrıntılar için. |
| Gezinti sorgu |Merhaba kullanıcı hello listesinden bir öğe seçtiğinde toorun sorgu.  Bkz: [ortak ayarları](#navigation-query) Ayrıntılar için. |
| **Liste** |**> Sütun başlıkları** |
| Ad |Metin toodisplay hello listesinin ilk sütun hello hello üstünde. |
| Değer |Metin toodisplay hello listesinin hello ikinci sütunun hello üstünde. |
| **Liste** |**> Eşikleri** |
| Eşikleri etkinleştir |Tooenable eşikleri seçin.  Bkz: [ortak ayarları](#thresholds) Ayrıntılar için. |

## <a name="stack-of-line-charts-part"></a>Çizgi grafikler bölümü yığını
Birden fazla seri günlük sorgudan üç ayrı çizgi grafiklerde zaman içinde görüntüler.

![Çizgi grafiklerde yığını](media/log-analytics-view-designer/view-stack-line-charts.png)

| Ayar | Açıklama |
|:--- |:--- |
| **Genel** | |
| Grup başlığı |Metin toodisplay hello hello üstündeki döşeme. |
| Yeni Grup |Merhaba geçerli Sergi başlangıç hello görünümünde toocreate yeni bir grup seçin. |
| Simgesi |Görüntü dosyası toodisplay sonraki toohello sonucunda hello üstbilgi. |
| **Grafik 1<br>grafik 2<br>grafik 3** |**> Üstbilgisi** |
| Başlık |Metin toodisplay hello grafik hello üstünde. |
| Alt Başlığı |Metin toodisplay hello hello üstünde hello Grafik başlığı altında. |
| **Grafik 1<br>grafik 2<br>grafik 3** |**Çizgi grafiği** |
| Sorgu |Sorgu toorun hello çizgi grafiği için.  Merhaba ilk özelliği bir metin değeri ve hello ikinci özelliğini sayısal bir değer olmalıdır.  Bu genellikle hello kullanan bir sorgu olur **ölçü** anahtar sözcüğü toosummarize sonuçları.  Merhaba sorgu hello kullanıyorsa **aralığı** anahtar sözcüğü sonra hello hello grafiğin x ekseni bu zaman aralığı kullanır.  Merhaba sorgu hello içermiyorsa **aralığı** anahtar sözcüğü sonra saatlik aralıklarla hello x ekseni için kullanılır. |
| **Grafik** |**> Y ekseni** |
| Logaritmik ölçek kullan |Toouse Logaritmik ölçek hello y ekseni için seçin. |
| Birimler |Merhaba sorgu tarafından döndürülen hello değerleri Hello birimlerini belirtin.  Bu bilgiler hello değer türleri belirten hello grafik ve isteğe bağlı olarak hello değerleri dönüştürmek için kullanılan toodisplay etiketlerini olur.  Merhaba birim türü hello biriminin hello kategorisini belirtir ve kullanılabilir hello geçerli birim türü değerleri tanımlar.  Dönüştürme toothen hello sayısal bir değer seçerseniz değerler hello geçerli birim türü toohello dönüştürme tootype dönüştürülür. |
| Özel Etiket |Metin toodisplay hello Y ekseni sonraki toohello etiketinin hello birim türü.  Hiçbir etiket belirtilirse, yalnızca hello birim türü görüntülenir. |

## <a name="common-settings"></a>Genel ayarları
Aşağıdaki bölümlerde hello ayarları ortak tooseveral görselleştirme bölümleri açıklanmaktadır.

### <a name="name-value-separator">Ad ve değer ayırıcı</a>
Liste sorgusu tooparse hello metin özelliğinden birden fazla değer istiyorsanız, tek karakter sınırlayıcısı.  Bir sınırlayıcı belirtirseniz, her bir alan tarafından hello aynı ayrılmış için adlarını sağlayabilen hello adı kutusuna sınırlayıcısı.

Örneğin, adlı bir özellik göz önünde bulundurun *konumu* gibi değerler dahil *Redmond yapı 41* ve *Bellevue Building12*.  – Hello ad ve değer ayırıcı için belirttiğiniz ve *Şehir yapı* hello adı için.  Bu her değeri adlı iki özellik ayrıştırın *Şehir* ve *yapı*.

### <a name="navigation-query">Gezinti sorgu</a>
Merhaba kullanıcı hello listesinden bir öğe seçtiğinde toorun sorgu.  Kullanım *{seçili öğe}* tooinclude hello sözdizimi seçili kullanıcı hello öğesi için.

Örneğin, hello sorgu adlı bir sütun sahipse *bilgisayar* ve hello Gezinti sorgu *{seçili öğe}*, gibi bir sorgu *bilgisayar "Bilgisayarım" =* ne zaman çalıştırılır Merhaba kullanıcı bir bilgisayara seçilen.  Merhaba Gezinti sorgu ise *türü olay {seçili öğe} =* sonra hello sorgu *türü olay bilgisayar = "Bilgisayarım" =* çalıştırılması.

### <a name="sparklines">Mini Grafikler</a>
Bir mini grafik zaman içinde bir liste girdisi hello değerini gösteren bir küçük çizgi grafiktir.  Bir liste görselleştirme bölümleri için toodisplay yatay bir çubukla belirten hello göreli değerini sayısal bir sütun veya zamanla değerini gösteren bir mini seçebilirsiniz.

Aşağıdaki tablonun hello Mini Grafikler hello ayarlarını açıklar.

| Ayar | Açıklama |
|:--- |:--- |
| Mini Grafikler etkinleştir |Yatay çubuk yerine toodisplay mini grafik seçin. |
| İşlem |Mini Grafikler etkinleştirilirse, hello işlemi tooperform hello liste toocalculate hello değerleri hello Mini Grafik için her bir özellik üzerinde budur.<br><br>-Son örnek: Merhaba serisi için değer hello zaman aralığı içinde son.<br>-Max: Merhaba serisi hello zaman aralığında maksimum değeri.<br>-Min: Minimum değer hello serisinin hello zaman aralığı içinde.<br>-TOPLA: Hello serisi hello zaman aralığında değerlerinin toplamı.<br>-Özeti: Kullandığı aynı ölçü komut hello sorgu hello üstbilgisinde olarak hello. |

### <a name="thresholds">Eşikleri</a>
Eşikleri belirli bir değeri aşması veya belirli bir aralıkta öğelerin hızlı görsel bir gösterge vermiş listesinde toodisplay sonraki tooeach öğe renkli simgesi sağlar.  Örneğin, bir hata değeri aşarsa, kabul edilebilir değer, bir uyarı gösterir bir aralıkta hello değeriyse, sarı ve kırmızı ile öğeleri için yeşil bir simge görüntüleyebilirsiniz.

Bir bölümü için eşikler etkinleştirdiğinizde, bir veya daha fazla eşikleri belirtmeniz gerekir.  Bir öğenin başlangıç değeri eşik değerden daha büyük ve hello sonraki eşik değerden daha düşük ise, bu renk kullanılır.  Merhaba öğesi sonra yüksek eşik değerinden büyükse, bu rengi ayarlanır.   

Bir eşik değerini her eşik ayarlanmış **varsayılan**.  Merhaba renk diğer değerler aşılırsa Ayarla budur.  Ekleyip hello tıklatarak eşikleri kaldırdığınızda  **+**  veya **x** düğmesi.

Aşağıdaki tablonun hello tresholds hello ayarlarını açıklar.

| Ayar | Açıklama |
|:--- |:--- |
| Eşikleri etkinleştir |Bir renk simgesi toohello kendi sistem durumu göreli toospecified eşikleri belirten her değeri sol toodisplay seçin. |
| Ad |Ad tooidentify hello eşik değeri. |
| Eşik |Merhaba eşik değeri.  Her liste öğesi için Hello sistem durumu rengi tarafından hello öğenin değeri aşıldı hello yüksek eşik değeri toohello rengini ayarlanır.  Eşik değerleri aşılırsa hello renk olan bir varsayılan eşik yoktur. |
| Renk |Merhaba eşik değeri rengi. |

## <a name="next-steps"></a>Sonraki adımlar
* Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) görselleştirme bölümlerindeki toosupport hello sorgular.
