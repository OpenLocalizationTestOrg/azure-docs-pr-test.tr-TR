---
title: "Azure Application Insights gelen akış analizi kullanarak aaaExport | Microsoft Docs"
description: "Akış analizi sürekli dönüştürebilirsiniz, filtre ve rota hello veri Application Insights ' dışarı aktarma."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 31594221-17bd-4e5e-9534-950f3b022209
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: fda9b64f588c520833b2669eafdf650efc3de6be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-stream-analytics-tooprocess-exported-data-from-application-insights"></a>Application Insights kullanım Stream Analytics tooprocess verilen verileri
[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) veri işlemeye hello ideal araçtır [Application Insights ' dışarı](app-insights-export-telemetry.md). Akış analizi, çeşitli kaynaklardan veri çeker. Bu dönüştürme ve hello verilere filtre ve ardından havuzlarını tooa çeşitli rota.

Bu örnekte, yeniden adlandırır Application Insights ' verileri alır ve bazı hello alanlarını işler ve Power BI kanallar bir bağdaştırıcıya oluşturacağız.

> [!WARNING]
> Çok daha iyi ve daha kolay [toodisplay Application Insights Power BI'daki veriler, önerilen yollar](app-insights-export-power-bi.md). Merhaba burada gösterilen yalnızca bir örnek tooillustrate yoludur nasıl tooprocess verilen verileri.
> 
> 

![Blok Diyagramı SA tooPBI aracılığıyla dışarı aktarma](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a>Depolama oluşturma
Toocreate hello depolama önce gerekir böylece sürekli dışarı aktarma veri tooan Azure depolama hesabı, her zaman çıkarır.

1. Aboneliğinizdeki hello "Klasik" depolama hesabı oluşturma [Azure portal](https://portal.azure.com).
   
   ![Azure portalında yeni, verileri depolama seçin](./media/app-insights-export-stream-analytics/030.png)
2. Bir kapsayıcı oluşturma
   
    ![Merhaba yeni depolama kapsayıcıları seçin, Merhaba kapsayıcılara döşeme tıklatın ve ardından Ekle](./media/app-insights-export-stream-analytics/040.png)
3. Merhaba depolama erişim tuşu kopyalama
   
    Bunu en kısa sürede tooset hello giriş toohello stream analytics hizmeti yukarı ihtiyacınız vardır.
   
    ![Merhaba depolama ayarları, anahtarları, açın ve hello birincil erişim anahtarını bir kopyasını alın](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-tooazure-storage"></a>Sürekli verme tooAzure depolama Başlat
[Sürekli verme](app-insights-export-telemetry.md) Application Insights Azure depolama alanına gelen verileri taşır.

1. Hello Azure portal, uygulamanız için oluşturulan toohello Application Insights kaynağı göz atın.
   
    ![Gözat, Application Insights, uygulamanızı seçin](./media/app-insights-export-stream-analytics/050.png)
2. Sürekli verme oluşturun.
   
    ![Ayarları, sürekli verme ekleme seçin](./media/app-insights-export-stream-analytics/060.png)

    Daha önce oluşturduğunuz hello depolama hesabı seçin:

    ![Merhaba dışa aktarma hedefi ayarlama](./media/app-insights-export-stream-analytics/070.png)

    İstediğiniz hello olay türlerini toosee ayarlayın:

    ![Olay türlerini seçin](./media/app-insights-export-stream-analytics/080.png)

1. Accumulate bazı veriler sağlar. Arkanıza yaslanın ve kişilere uygulamanızın biraz kullanın. Telemetri geldikçe ve istatistiksel grafiklerde görürsünüz [ölçüm Gezgini](app-insights-metrics-explorer.md) ve olayları tek tek [tanılama arama](app-insights-diagnostic-search.md). 
   
    Ve ayrıca hello veri tooyour depolama dışa aktarır. 
2. Dışa aktarılan hello veri inceleyin. Visual Studio'da, **görüntülemek / Cloud Explorer**ve Azure açın / depolama. (Bu menü seçeneği yoksa, tooinstall hello Azure SDK'sı gerekir: hello yeni proje iletişim kutusu açın ve Visual C# açın / bulut / .NET için Microsoft Azure SDK'sını alın.)
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    Merhaba ortak hello uygulama adı ve araçları anahtarından türetilen hello yol adı parçası not edin. 

Merhaba olayları tooblob dosyaları JSON biçiminde yazılır. Her dosya bir veya daha fazla olaylar içerebilir. Bu nedenle tooread hello olay verileri ve filtre istiyoruz hello alanları isteriz. Her türlü hello verilerle yapabileceğimiz bir şey vardır, ancak bizim bugün toouse Stream Analytics toopipe hello veri tooPower BI planınızdır.

## <a name="create-an-azure-stream-analytics-instance"></a>Bir Azure akış analizi örneği oluşturma
Merhaba gelen [Klasik Azure portalı](https://manage.windowsazure.com/)hello Azure Stream Analytics hizmeti seçin ve yeni bir Stream Analytics işi oluştur:

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

Merhaba yeni iş oluşturulduğunda ayrıntılarını genişletin:

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a>Blob konum ayarlama
Sürekli verme blob tootake girişten ayarlayın:

![](./media/app-insights-export-stream-analytics/120.png)

Şimdi, depolama, daha önce not ettiğiniz hesabınızdan, hello birincil erişim anahtarı gerekir. Bu depolama hesabı anahtarı hello ayarlayın.

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a>Set yol önek deseni
![](./media/app-insights-export-stream-analytics/140.png)

**Emin tooset hello tarih biçimi tooYYYY-aa-gg (çizgilerle) olabilir.**

Stream Analytics hello giriş dosyaları hello depolama burada bulur Hello yol önek deseni belirtir. Tooset gerekir, toocorrespond toohow sürekli verme hello verileri depolar. Aşağıdaki gibi ayarlayın:

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

Bu örnekte:

* `webapplication27`Merhaba Application Insights kaynağı Hello adıdır **tüm küçük**.
* `1234...`Merhaba izleme anahtarını hello Application Insights kaynağı olan **tire atlama**. 
* `PageViews`Merhaba türü tooanalyze istediğiniz verileri. Merhaba kullanılabilir türler hello filtresi sürekli dışarı aktarma ile Ayarla bağlıdır. Kullanılabilir diğer türleri Hello dışarı aktarılan verileri toosee hello inceleyin ve hello bakın [veri modeli verme](app-insights-export-data-model.md).
* `/{date}/{time}`bir desen tam anlamıyla yazılır.

> [!NOTE]
> Merhaba depolama toomake hello yolu doğru alma emin inceleyin.
> 
> 

### <a name="finish-initial-setup"></a>İlk Kurulumu tamamlayın
Merhaba seri hale getirme biçimi onaylayın:

![Onayla ve sihirbazı kapatın](./media/app-insights-export-stream-analytics/150.png)

Merhaba sihirbazı kapatın ve hello Kurulum toocomplete için bekleyin.

> [!TIP]
> Merhaba örnek komut toodownload bazı verileri kullanın. Bu bir test örneği toodebug sorgunuzu tutun.
> 
> 

## <a name="set-hello-output"></a>Set hello çıktı
Şimdi, işi seçin ve hello çıkış ayarlayın.

![Merhaba yeni kanal seçin, çıkışları, Ekle, Power BI'ı tıklatın](./media/app-insights-export-stream-analytics/160.png)

Sağlayın, **iş veya Okul hesabı** tooauthorize Stream Analytics tooaccess Power BI kaynağınız. Ardından hello çıktı için ve hello hedef Power BI veri kümesi ve tablo için bir ad oluşturun.

![Üç adları stok](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-hello-query"></a>Set hello sorgu
Merhaba sorgu giriş toooutput hello çevrilmesi yönetir.

![Merhaba işi seçin ve sorguyu tıklayın. Aşağıdaki Hello örneği yapıştırın.](./media/app-insights-export-stream-analytics/180.png)

Merhaba sağ çıkış Al hello Test işlevi toocheck kullanın. Merhaba giriş sayfadan sürdü hello örnek veri verin. 

### <a name="query-toodisplay-counts-of-events"></a>Sorgu toodisplay olayları sayısı
Bu sorgu yapıştırın:

```SQL

    SELECT
      flat.ArrayValue.name,
      count(*)
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.[event]) as flat
    GROUP BY TumblingWindow(minute, 1), flat.ArrayValue.name
```

* Biz toohello akış girişine vermiş hello diğer dışarı aktarma girişi adıdır
* pbı çıkış tanımladığımız hello çıkış diğer adıdır
* Kullanırız [dış uygulamak GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) hello olay adı bir iç içe geçmiş JSON arrray olduğundan. Ardından hello Select Çekmeleri bir sayısını hello hello süre ad örnekleriyle birlikte olay adı hello. Merhaba [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) yan tümcesi süreleri 1 dakika içinde hello öğeleri gruplandırır.

### <a name="query-toodisplay-metric-values"></a>Sorgu toodisplay ölçüm değerleri
```SQL

    SELECT
      A.context.data.eventtime,
      avg(CASE WHEN flat.arrayvalue.myMetric.value IS NULL THEN 0 ELSE  flat.arrayvalue.myMetric.value END) as myValue
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.context.custom.metrics) as flat
    GROUP BY TumblingWindow(minute, 1), A.context.data.eventtime

``` 

* Bu sorgu hello ölçümleri telemetri tooget hello olay süresi ve hello ölçüm değeri olarak ayrıntılı açıklanmıştır. Merhaba dış uygulamak GetElements düzeni tooextract hello satırları kullanırız şekilde hello ölçüm bir dizi içinde değerlerdir. "myMetric" Merhaba hello ölçüm bu durumda adıdır. 

### <a name="query-tooinclude-values-of-dimension-properties"></a>Sorgu tooinclude değerleri boyut özellikleri
```SQL

    WITH flat AS (
    SELECT
      MySource.context.data.eventTime as eventTime,
      InstanceId = MyDimension.ArrayValue.InstanceId.value,
      BusinessUnitId = MyDimension.ArrayValue.BusinessUnitId.value
    FROM MySource
    OUTER APPLY GetArrayElements(MySource.context.custom.dimensions) MyDimension
    )
    SELECT
     eventTime,
     InstanceId,
     BusinessUnitId
    INTO AIOutput
    FROM flat

```

* Bu sorgu hello boyut dizisindeki sabit dizinindeki olan belirli bir boyut bağlı olarak hello boyut özelliklerinin değerlerini içerir.

## <a name="run-hello-job"></a>Merhaba işini çalıştır
Merhaba toostart hello işten geçmiş bir tarih seçebilirsiniz. 

![Merhaba işi seçin ve sorguyu tıklayın. Aşağıdaki Hello örneği yapıştırın.](./media/app-insights-export-stream-analytics/190.png)

Merhaba işi çalışıyor kadar bekleyin.

## <a name="see-results-in-power-bi"></a>Power BI sonuçlarına bakın
> [!WARNING]
> Çok daha iyi ve daha kolay [toodisplay Application Insights Power BI'daki veriler, önerilen yollar](app-insights-export-power-bi.md). Merhaba burada gösterilen yalnızca bir örnek tooillustrate yoludur nasıl tooprocess verilen verileri.
> 
> 

Power BI iş veya Okul hesabı ve select hello dataset ve hello hello Stream Analytics işi çıkış olarak tanımlanan tablo açın.

![Power BI'da veri kümesi ve alanları seçin.](./media/app-insights-export-stream-analytics/200.png)

Artık bu veri kümesi raporlarında ve panolarında kullanarak [Power BI](https://powerbi.microsoft.com).

![Power BI'da veri kümesi ve alanları seçin.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a>Veri yok mu?
* Denetleyin, [kümesi hello tarih biçimi](#set-path-prefix-pattern) doğru tooYYYY-aa-gg (çizgilerle ile).

## <a name="video"></a>Video
Noam Ben Zeev tooprocess akış analizi kullanarak verileri nasıl dışa gösterir.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* [Sürekli dışarı aktarma](app-insights-export-telemetry.md)
* [Ayrıntılı veri başvuru hello özellik türleri ve değerleri için model.](app-insights-export-data-model.md)
* [Application Insights](app-insights-overview.md)

