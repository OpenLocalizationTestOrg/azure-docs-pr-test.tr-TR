---
title: "aaaUse hello köşe yürütme görünümü Visual Studio için Data Lake araçları içinde | Microsoft Docs"
description: "Nasıl toouse hello köşe yürütme görünümü tooexam Data Lake Analytics işlerini öğrenin."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: fb54d2af8a32aa27a54ff50a73c1b4903677a21e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a>Visual Studio için Data Lake araçları içinde Hello köşe yürütme görünümü kullanın
Nasıl toouse hello köşe yürütme görünümü tooexam Data Lake Analytics işlerini öğrenin.

## <a name="prerequisites"></a>Ön koşullar

Visual Studio toodevelop U-SQL betiği için Data Lake araçları kullanarak, temel bilgiye gerekir.  Bkz: [öğretici: Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme](data-lake-analytics-data-lake-tools-get-started.md).

## <a name="open-hello-vertex-execution-view"></a>Merhaba köşe yürütme görünümü Aç
U-SQL işi Visual Studio için Data Lake araçları içinde açın. Tıklatın **köşe yürütme görünümü** sol alt köşede, hello. İstendiğinde tooload profilleri ilk olabilir ve ağ bağlantınızı bağlı olarak biraz zaman alabilir.

![Data Lake Analytics köşe yürütme görünümü araçları](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a>Köşe yürütme görünümü anlama
Merhaba köşe yürütme görünümü üç bölümden oluşur:

![Data Lake Analytics köşe yürütme görünümü araçları](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

Merhaba **köşe Seçici** hello sol olanak tanır (10 veri top gibi okuma veya aşamasına göre seçin) özellikleri tarafından köşeleri seçin. Merhaba en yaygın olarak kullanılan filtreleri biri toosee hello **kritik yol köşelerinin**. Merhaba **kritik yol** hello uzun bir U-SQL işi köşe zincirine olduğu. Anlama hello kritik yol işleriniz hangi köşe hello uzun süren denetleyerek en iyi duruma getirme için yararlıdır.
  
![Data Lake Analytics köşe yürütme görünümü araçları](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

Merhaba üst orta bölmesinde gösterilir hello **tüm hello köşeleri durumunu çalıştıran**.
  
![Data Lake Analytics köşe yürütme görünümü araçları](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

Merhaba alt bölmeyi her köşe hakkında bilgileri gösterir:
* İşlem adı: Merhaba köşe örneğinin hello adı. StageName farklı bölümlerinin oluşan | VertexName | VertexRunInstance. Örneğin, hello SV7_Split [62] .v1 köşe hello ikinci çalışan örneği için (.v1, dizini 0'dan başlayarak) anlamına gelir 62 köşe sayısının aşama SV7_Split.
* Toplam veri okuma/yazılan: hello verileri bu köşe tarafından okunur/yazılır.
* Durumu/Çıkış durumu: hello köşe sonlandığında hello son durum.
* Çıkış kodu/hatası türü: hello köşe başarısız olduğunda hello hatası.
* Oluşturma nedeni: Neden hello köşe oluşturuldu.
* Kaynak gecikme/işlem gecikmesi/PN sıra gecikme süresi: hello hello köşe toowait kaynakları, tooprocess veri ve hello sırasındaki toostay için geçen süre.
* İşlem/Creator GUID: Merhaba geçerli çalışan köşe veya oluşturana GUID.
* Sürüm: hello n. köşe çalıştıran hello örneği (Merhaba sistem zamanlayın bir köşesinin yeni örnekleri birçok nedeni, örneğin yük devretme, işlem için artıklık, vb.)
* Sürümü zaman oluşturuldu.
* İşlem oluşturma başlangıç süre/işlem sıraya alınan süre/işlem başlangıç saati/işlem tam zamanı: hello köşe işlemi oluşturma; başladığında Merhaba köşe işlem tooqueue başladığında; ne zaman belirli köşe işlemi başlar hello; Merhaba belirli köşe tamamlandığında.

## <a name="next-steps"></a>Sonraki adımlar
* toolog tanılama bilgilerini görmek [Azure Data Lake Analytics için tanılama günlükleri erişme](data-lake-analytics-diagnostic-logs.md)
* toosee daha karmaşık bir sorgu görmek [Web sitesi günlüklerini çözümleme Azure Data Lake Analytics'i kullanarak](data-lake-analytics-analyze-weblogs.md).
* tooview iş ayrıntılarını görmek [kullanım iş tarayıcı ve Azure Data lake Analytics işleri için iş görünümünde](data-lake-analytics-data-lake-tools-view-jobs.md)
