---
title: "Görünüm Tasarımcısı'nda OMS günlük analizi için aaaTile başvurusu | Microsoft Docs"
description: "Görünüm Tasarımcısı'nda günlük analizi sağlar, toocreate özel hello OMS konsolundaki hello OMS deposundaki verileri farklı görselleştirmesini içeren görünümler. Bu makalede hello ayarlarının hello döşeme kullanılabilir toouse kendi özel görünümlerinizi de her bir başvuru sağlar."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: 41787c8f-6c13-4520-b0d3-5d3d84fcf142
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 4706abb16b8a3719f5dbe8c89cd61739391ab8f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-view-designer-tile-reference"></a>Günlük analizi Görünüm Tasarımcısı döşeme başvurusu
Merhaba Görünüm Tasarımcısı'nda günlük analizi sağlar, toocreate özel hello OMS konsolundaki hello OMS deposundaki verileri farklı görselleştirmesini içeren görünümler. Bu makalede hello ayarlarının hello döşeme kullanılabilir toouse kendi özel görünümlerinizi de her bir başvuru sağlar.

Görünüm Tasarımcısı için kullanılabilir diğer makaleler şunlardır:

* [Görüntüleme Tasarımcısı](log-analytics-view-designer.md) -hello Görünüm Tasarımcısı ve oluşturma ve özel görünümler düzenleme yordamları genel bakış.
* [Görselleştirme bölümü başvuru](log-analytics-view-designer-parts.md) -başvuru hello ayarlarının her hello için kendi özel görünümlerinizi de kullanılabilir toouse yerleştirir.

>[!NOTE]
> Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), tüm görünümleri sorgularda hello yazılmalıdır sonra [yeni sorgu dili](https://go.microsoft.com/fwlink/?linkid=856078).  Merhaba çalışma yükseltilmeden önce oluşturulan görünümleri dönüştürülen automtically olacaktır.

Merhaba aşağıdaki tabloda hello farklı döşeme hello Görünüm Tasarımcısı kullanılabilir türlerini listeler.  Aşağıdaki Hello bölümler her döşeme türü ayrıntı ve bunların özelliklerini açıklar.

| Döşeme | Açıklama |
|:--- |:--- |
| [Sayı](#number-tile) |Bir sorgu ndeki kayıtları sayısını gösteren tek bir sayı. |
| [İki sayı](#two-numbers-tile) |İki farklı sorgular kayıtları sayısını gösteren iki tek sayı. |
| [Halka](#donut-tile) |Merhaba Center'da Özet bir değerle bir sorguyu temel halka grafiği. |
| [Çizgi grafiği & belirtme](#line-chart-amp-callout-tile) |Bir sorgu ve bir Özet değerle belirtme çizgisi temel çizgi grafiği. |
| [Çizgi grafiği](#line-chart-tile) |Bir sorguyu temel çizgi grafiği. |
| [İki zaman çizelgeleri](#two-timelines-tile) |Sütun grafiği her ayrı bir sorguyu temel iki dizi. |

## <a name="number-tile"></a>Sayı döşeme
Merhaba **numarası** kutucuğu günlük sorgu ve etiket kayıtlarından hello sayısını gösteren tek bir sayı görüntüler.

![Sayı döşeme](media/log-analytics-view-designer/tile-number.png)

| Ayar | Açıklama |
|:--- |:--- |
| Ad |Metin toodisplay hello hello üstündeki döşeme. |
| Açıklama |Metin toodisplay hello döşeme adı altında. |
| **Döşeme** | |
| Gösterge |Metin toodisplay hello değerin altında. |
| Sorgu |Sorgu toorun.  Merhaba hello sorgu tarafından döndürülen kayıt sayısını Hello sayısı görüntülenir. |
| **Gelişmiş** |**> Veri akışı doğrulama** |
| Etkin |Veri akışı doğrulama hello bölme için etkinleştirilmesi gerekiyorsa seçin.  Bu, veri hello bölme için kullanılabilir değilse, alternatif bir ileti sağlar.  Ne zaman yüklü hello görüntüle ve veri kullanılabilir gelir hello geçici süresi boyunca genellikle kullanılan tooprovide bir ileti budur. |
| Sorgu |Merhaba görünüm için veri varsa toorun toocheck sorgu.  Merhaba sorgu hiç sonuç döndürürse, hello ana sorgudan hello değeri yerine bir ileti görüntülenir. |
| İleti |Merhaba veri akışı doğrulama sorgu hiç veri döndürürse ileti toodisplay.  İleti yok, sağlarsanız, *gerçekleştirme değerlendirme* görüntülenir. |


## <a name="two-numbers-tile"></a>İki sayı döşeme
Merhaba **iki sayı** kutucuğu, her biri için iki farklı günlük sorgular ve etiket kayıtlarını hello sayıyı gösteren iki sayı görüntüler.

![İki sayı döşeme](media/log-analytics-view-designer/tile-two-numbers.png)

| Ayar | Açıklama |
|:--- |:--- |
| Ad |Metin toodisplay hello hello üstündeki döşeme. |
| Açıklama |Metin toodisplay hello döşeme adı altında. |
| **İlk döşeme** | |
| Gösterge |Metin toodisplay hello değerin altında. |
| Sorgu |Sorgu toorun.  Merhaba hello sorgu tarafından döndürülen kayıt sayısını Hello sayısı görüntülenir. |
| **İkinci döşeme** | |
| Gösterge |Metin toodisplay hello değerin altında. |
| Sorgu |Sorgu toorun.  Merhaba hello sorgu tarafından döndürülen kayıt sayısını Hello sayısı görüntülenir. |
| **Gelişmiş** |**> Veri akışı doğrulama** |
| Etkin |Veri akışı doğrulama hello bölme için etkinleştirilmesi gerekiyorsa seçin.  Bu, veri hello bölme için kullanılabilir değilse, alternatif bir ileti sağlar.  Ne zaman yüklü hello görüntüle ve veri kullanılabilir gelir hello geçici süresi boyunca genellikle kullanılan tooprovide bir ileti budur. |
| Sorgu |Merhaba görünüm için veri varsa toorun toocheck sorgu.  Merhaba sorgu hiç sonuç döndürürse, hello ana sorgudan hello değeri yerine bir ileti görüntülenir. |
| İleti |Merhaba veri akışı doğrulama sorgu hiç veri döndürürse ileti toodisplay.  İleti yok, sağlarsanız, *gerçekleştirme değerlendirme* görüntülenir. |


## <a name="donut-tile"></a>Halka döşeme
Merhaba **halka** kutucuğu günlük sorguda değer sütundan özetlenen tek bir sayı görüntüler.  Merhaba halka grafik hello üst üç kayıt sonuçlarını görüntüler.

![Halka döşeme](media/log-analytics-view-designer/tile-donut.png)

| Ayar | Açıklama |
|:--- |:--- |
| Ad |Metin toodisplay hello hello üstündeki döşeme. |
| Açıklama |Metin toodisplay hello döşeme adı altında. |
| **Halka** | |
| Sorgu |Merhaba halka toorun sorgu.  Merhaba ilk özelliği bir metin değeri ve hello ikinci özelliğini sayısal bir değer olmalıdır.  Bu genellikle hello kullanan bir sorgu olur **ölçü** anahtar sözcüğü toosummarize sonuçları. |
| **Halka** |**> Merkezi** |
| Metin |Metin toodisplay hello halka içindeki hello değeri altında. |
| İşlem |Merhaba işlemi tooperform hello değer özelliği toosummarize tooa tek değeri.<br><br>-TOPLA: hello özellik değeri ile tüm kayıtların hello değerlerini ekleyin.<br>-Yüzdesi: Hello özellik değeri karşılaştırıldığında toohello kayıtlarıyla hello toplamı değerleri yüzdesini tüm kayıtların değerlerini toplanır. |
| Merkezi işleminde kullanılan sonuç değerleri |İsteğe bağlı olarak tıklatın hello artı tooadd bir veya daha fazla değer.  Merhaba hello sorgunun sonuçlarını belirttiğiniz hello özellik değerleri ile sınırlı toorecords olacaktır.  Hiçbir değer eklediyseniz, tüm kayıtları hello sorguya dahil edilir. |
| **Halka** |**> Ek seçenekler** |
| Renkleri |Merhaba renk toodisplay hello üç üst özelliklerin her biri için.  İçin belirli özellik değerlerini toospecify alternatif renkleri istiyorsanız, gelişmiş renk eşleme kullanın. |
| Gelişmiş renk eşleme |Belirli özellik değerleri için renk görüntüler.  Belirttiğiniz başlangıç değeri içinde ise üst üç hello sonra hello alternatif renk standart bir renk hello yerine görüntülenir.  Merhaba özellik değilse üst üç hello sonra hello renk görüntülenmez. |
| **Gelişmiş** |**> Veri akışı doğrulama** |
| Etkin |Veri akışı doğrulama hello bölme için etkinleştirilmesi gerekiyorsa seçin.  Bu, veri hello bölme için kullanılabilir değilse, alternatif bir ileti sağlar.  Ne zaman yüklü hello görüntüle ve veri kullanılabilir gelir hello geçici süresi boyunca genellikle kullanılan tooprovide bir ileti budur. |
| Sorgu |Merhaba görünüm için veri varsa toorun toocheck sorgu.  Merhaba sorgu hiç sonuç döndürürse, hello ana sorgudan hello değeri yerine bir ileti görüntülenir. |
| İleti |Merhaba veri akışı doğrulama sorgu hiç veri döndürürse ileti toodisplay.  İleti yok, sağlarsanız, *gerçekleştirme değerlendirme* görüntülenir. |


## <a name="line-chart-tile"></a>Satır grafiği döşeme
Merhaba **çizgi grafiği** kutucuğu, zaman içinde bir günlük sorgudan birden fazla seri ile bir çizgi grafiği görüntüler.  

![Çizgi grafiği & belirtme çizgisi döşeme](media/log-analytics-view-designer/tile-line-chart.png)

| Ayar | Açıklama |
|:--- |:--- |
| Ad |Metin toodisplay hello hello üstündeki döşeme. |
| Açıklama |Metin toodisplay hello döşeme adı altında. |
| **Çizgi grafiği** | |
| Sorgu |Sorgu toorun hello çizgi grafiği için.  Merhaba ilk özelliği bir metin değeri ve hello ikinci özelliğini sayısal bir değer olmalıdır.  Bu genellikle hello kullanan bir sorgu olur **ölçü** anahtar sözcüğü toosummarize sonuçları.  Merhaba sorgu hello kullanıyorsa **aralığı** anahtar sözcüğü sonra hello hello grafiğin x ekseni bu zaman aralığı kullanır.  Merhaba sorgu hello içermiyorsa **aralığı** anahtar sözcüğü sonra saatlik aralıklarla hello x ekseni için kullanılır. |
| **Çizgi grafiği** |**> Y ekseni** |
| Logaritmik ölçek kullan |Toouse Logaritmik ölçek hello y ekseni için seçin. |
| Birimler |Merhaba sorgu tarafından döndürülen hello değerleri Hello birimlerini belirtin.  Bu bilgiler hello değer türleri belirten hello grafik ve isteğe bağlı olarak hello değerleri dönüştürmek için kullanılan toodisplay etiketlerini olur.  Merhaba **birim türü** hello biriminin hello kategorisini belirtir ve hello tanımlar **geçerli birim türü** kullanılabilir değerler.  Bir değer seçerseniz **dönüştürmek** hello sayısal değerler hello dönüştürülür sonra **geçerli birim** toohello yazın **dönüştürmek** türü. |
| Özel Etiket |Metin toodisplay hello Y ekseni sonraki toohello etiketinin hello birim türü.  Hiçbir etiket belirtilirse, yalnızca hello birim türü görüntülenir. |
| **Gelişmiş** |**> Veri akışı doğrulama** |
| Etkin |Veri akışı doğrulama hello bölme için etkinleştirilmesi gerekiyorsa seçin.  Bu, veri hello bölme için kullanılabilir değilse, alternatif bir ileti sağlar.  Ne zaman yüklü hello görüntüle ve veri kullanılabilir gelir hello geçici süresi boyunca genellikle kullanılan tooprovide bir ileti budur. |
| Sorgu |Merhaba görünüm için veri varsa toorun toocheck sorgu.  Merhaba sorgu hiç sonuç döndürürse, hello ana sorgudan hello değeri yerine bir ileti görüntülenir. |
| İleti |Merhaba veri akışı doğrulama sorgu hiç veri döndürürse ileti toodisplay.  İleti yok, sağlarsanız, *gerçekleştirme değerlendirme* görüntülenir. |


## <a name="line-chart--callout-tile"></a>Satır Grafiği & belirtme çizgisi döşeme
Merhaba **çizgi grafiği & belirtme çizgisi** kutucuğu, saat ve özetlenen bir değerle belirtme çizgisi üzerinde birden fazla dizi günlük sorgudan bir çizgi grafiği görüntüler.  

![Çizgi grafiği & belirtme çizgisi döşeme](media/log-analytics-view-designer/tile-line-chart-callout.png)

| Ayar | Açıklama |
|:--- |:--- |
| Ad |Metin toodisplay hello hello üstündeki döşeme. |
| Açıklama |Metin toodisplay hello döşeme adı altında. |
| **Çizgi grafiği** | |
| Sorgu |Sorgu toorun hello çizgi grafiği için.  Merhaba ilk özelliği bir metin değeri ve hello ikinci özelliğini sayısal bir değer olmalıdır.  Bu genellikle hello kullanan bir sorgu olur **ölçü** anahtar sözcüğü toosummarize sonuçları.  Merhaba sorgu hello kullanıyorsa **aralığı** anahtar sözcüğü sonra hello hello grafiğin x ekseni bu zaman aralığı kullanır.  Merhaba sorgu hello içermiyorsa **aralığı** anahtar sözcüğü sonra saatlik aralıklarla hello x ekseni için kullanılır. |
| **Çizgi grafiği** |**> Belirtme** |
| Belirtme çizgisi |Başlık metni toodisplay hello belirtme çizgisi değerin üzerinde. |
| Seri adı |Merhaba serisi toouse hello belirtme çizgisi değeri için özellik değeri.  Seri sağlanırsa, hello sorgudan tüm kayıtları kullanılır. |
| İşlem |Merhaba işlemi tooperform hello değer özelliği toosummarize tooa için tek bir değer hello belirtme çizgisi üzerinde.<br>-Ortalama: Tüm kayıtları hello değerinden ortalama.<br><br>-Count: Hello sorgu tarafından döndürülen tüm kayıtların sayısı.<br>-Son örnek: Merhaba son aralığı hello grafikte dahil değeri.<br>-Max: Merhaba grafikte dahil hello aralıkları maksimum değeri.<br>-Min: Merhaba grafikte dahil hello aralıkları Minimum değeri.<br>-TOPLA: Tüm kayıtları hello değerinden toplamı. |
| **Çizgi grafiği** |**> Y ekseni** |
| Logaritmik ölçek kullan |Toouse Logaritmik ölçek hello y ekseni için seçin. |
| Birimler |Merhaba sorgu tarafından döndürülen hello değerleri Hello birimlerini belirtin.  Bu bilgiler hello değer türleri belirten hello grafik ve isteğe bağlı olarak hello değerleri dönüştürmek için kullanılan toodisplay etiketlerini olur.  Merhaba **birim türü** hello biriminin hello kategorisini belirtir ve hello tanımlar **geçerli birim türü** kullanılabilir değerler.  Bir değer seçerseniz **dönüştürmek** hello sayısal değerler hello dönüştürülür sonra **geçerli birim** toohello yazın **dönüştürmek** türü. |
| Özel Etiket |Metin toodisplay hello Y ekseni sonraki toohello etiketinin hello birim türü.  Hiçbir etiket belirtilirse, yalnızca hello birim türü görüntülenir. |
| **Gelişmiş** |**> Veri akışı doğrulama** |
| Etkin |Veri akışı doğrulama hello bölme için etkinleştirilmesi gerekiyorsa seçin.  Bu, veri hello bölme için kullanılabilir değilse, alternatif bir ileti sağlar.  Ne zaman yüklü hello görüntüle ve veri kullanılabilir gelir hello geçici süresi boyunca genellikle kullanılan tooprovide bir ileti budur. |
| Sorgu |Merhaba görünüm için veri varsa toorun toocheck sorgu.  Merhaba sorgu hiç sonuç döndürürse, hello ana sorgudan hello değeri yerine bir ileti görüntülenir. |
| İleti |Merhaba veri akışı doğrulama sorgu hiç veri döndürürse ileti toodisplay.  İleti yok, sağlarsanız, *gerçekleştirme değerlendirme* görüntülenir. |


## <a name="two-timelines-tile"></a>İki zaman çizelgelerini döşeme
Merhaba **iki zaman çizelgelerini** kutucuğu sütun grafikleri olarak zaman içinde hello iki günlük sorguların sonuçlarını görüntüler.  Belirtme çizgisi her seri için görüntülenir.  

![İki zaman çizelgelerini döşeme](media/log-analytics-view-designer/tile-two-timelines.png)

| Ayar | Açıklama |
|:--- |:--- |
| Ad |Metin toodisplay hello hello üstündeki döşeme. |
| Açıklama |Metin toodisplay hello döşeme adı altında. |
| İlk grafik | |
| Gösterge |Metin toodisplay hello belirtme çizgisi hello ilk serisinin altında. |
| Renk |Renk toouse hello ilk serisi hello sütunlar için. |
| Grafik sorgu |Sorgu toorun hello ilk seri için.  her zaman aralığı içindeki kayıtları hello sayısı Merhaba sayımını hello grafik sütunlara göre temsil edilir. |
| İşlem |Merhaba işlemi tooperform hello değer özelliği toosummarize tooa için tek bir değer hello belirtme çizgisi üzerinde.<br><br>-Ortalama: Tüm kayıtları hello değerinden ortalama.<br>-Count: Hello sorgu tarafından döndürülen tüm kayıtların sayısı.<br>-Son örnek: Merhaba son aralığı hello grafikte dahil değeri.<br>-Max: Merhaba grafikte dahil hello aralıkları maksimum değeri. |
| **İkinci grafik** | |
| Gösterge |Metin toodisplay hello belirtme çizgisi hello ikinci serisinin altında. |
| Renk |Toouse hello sütunlar hello ikinci seri için renk. |
| Grafik sorgu |Sorgu toorun hello ikinci seri için.  her zaman aralığı içindeki kayıtları hello sayısı Merhaba sayımını hello grafik sütunlara göre temsil edilir. |
| İşlem |Merhaba işlemi tooperform hello değer özelliği toosummarize tooa için tek bir değer hello belirtme çizgisi üzerinde.<br><br>-Ortalama: Tüm kayıtları hello değerinden ortalama.<br>-Count: Hello sorgu tarafından döndürülen tüm kayıtların sayısı.<br>-Son örnek: Merhaba son aralığı hello grafikte dahil değeri.<br>-Max: Merhaba grafikte dahil hello aralıkları maksimum değeri. |
| **Gelişmiş** |**> Veri akışı doğrulama** |
| Etkin |Veri akışı doğrulama hello bölme için etkinleştirilmesi gerekiyorsa seçin.  Bu, veri hello bölme için kullanılabilir değilse, alternatif bir ileti sağlar.  Ne zaman yüklü hello görüntüle ve veri kullanılabilir gelir hello geçici süresi boyunca genellikle kullanılan tooprovide bir ileti budur. |
| Sorgu |Merhaba görünüm için veri varsa toorun toocheck sorgu.  Merhaba sorgu hiç sonuç döndürürse, hello ana sorgudan hello değeri yerine bir ileti görüntülenir. |
| İleti |Merhaba veri akışı doğrulama sorgu hiç veri döndürürse ileti toodisplay.  İleti yok, sağlarsanız, *gerçekleştirme değerlendirme* görüntülenir. |


## <a name="next-steps"></a>Sonraki adımlar
* Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) döşeme toosupport hello sorgular.
* Ekleme [görselleştirme bölümleri](log-analytics-view-designer-parts.md) tooyour özel görünüm.
