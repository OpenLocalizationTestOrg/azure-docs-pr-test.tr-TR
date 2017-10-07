---
title: Azure Application Insights tooSQL verme | Microsoft Docs
description: "Sürekli olarak kullanarak Stream Analytics Application Insights veri tooSQL verin."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 48903032-2c99-4987-9948-d6e4559b4a63
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/06/2015
ms.author: bwren
ms.openlocfilehash: 58b579499113751a088dc7e66cbec71529773322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-export-toosql-from-application-insights-using-stream-analytics"></a>İzlenecek yol: uygulama kullanarak Stream Analytics ilişkin bilgiler tooSQL dışarı aktarma
Bu makalede gösterilmektedir nasıl toomove telemetri verilerinizden [Azure Application Insights] [ start] kullanarak bir Azure SQL veritabanına [sürekli verme] [ export] ve [Azure akış analizi](https://azure.microsoft.com/services/stream-analytics/). 

Sürekli verme telemetri verileri JSON biçiminde Azure depolama alanına taşır. Biz Azure akış analizi kullanarak hello JSON nesneleri ayrıştırabilir ve bir veritabanı tablosundaki satırları oluşturmak.

(Daha genel olarak, sürekli verme hello yolu toodo olduğundan, kendi analiz hello telemetri uygulamalarınızı tooApplication Öngörüler Gönder. Bu kod örneği toodo veri toplama gibi hello dışarı telemetri ile başka şeyler uyarlayabilirsiniz.)

Merhaba varsayımıyla toomonitor hello uygulamayı zaten sahip başlayacağız.

Bu örnekte, biz hello sayfası görünüm verilerini kullanarak, ancak hello aynı düzeni kolayca tooother veri türleri özel etkinlikler ve özel durumlar gibi genişletilebilir. 

## <a name="add-application-insights-tooyour-application"></a>Application Insights tooyour uygulama ekleme
tooget başlatıldı:

1. [Web sayfalarınız için Application Insights'ı ayarlamak](app-insights-javascript.md). 
   
    (Bu örnekte, sayfa görünümü verileri hello istemci tarayıcıları işleme biz odaklanmak, ancak Application Insights'ı için hello sunucu tarafı ayarlayabilir, [Java](app-insights-java-get-started.md) veya [ASP.NET](app-insights-asp-net.md) uygulama ve işlem isteği bağımlılık ve diğer sunucu telemetri.)
2. Uygulamanızı yayımlayın ve telemetri verilerini Application Insights kaynağınıza görünmesini izleyin.

## <a name="create-storage-in-azure"></a>Depolama oluşturma
Toocreate hello depolama önce gerekir böylece sürekli dışarı aktarma veri tooan Azure depolama hesabı, her zaman çıkarır.

1. Merhaba, aboneliğinizde depolama hesabı oluşturma [Azure portal][portal].
   
    ![Azure portalında yeni, verileri depolama birimi seçin. Klasik seçin, oluşturun. Depolama adı sağlayın.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. Bir kapsayıcı oluşturma
   
    ![Merhaba yeni depolama kapsayıcıları seçin, Merhaba kapsayıcılara döşeme tıklatın ve ardından Ekle](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. Merhaba depolama erişim tuşu kopyalama
   
    Bunu en kısa sürede tooset hello giriş toohello stream analytics hizmeti yukarı ihtiyacınız vardır.
   
    ![Merhaba depolama ayarları, anahtarları, açın ve hello birincil erişim anahtarını bir kopyasını alın](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-tooazure-storage"></a>Sürekli verme tooAzure depolama Başlat
1. Hello Azure portal, uygulamanız için oluşturulan toohello Application Insights kaynağı göz atın.
   
    ![Gözat, Application Insights, uygulamanızı seçin](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. Sürekli verme oluşturun.
   
    ![Ayarları, sürekli verme ekleme seçin](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    Daha önce oluşturduğunuz hello depolama hesabı seçin:

    ![Merhaba dışa aktarma hedefi ayarlama](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    İstediğiniz hello olay türlerini toosee ayarlayın:

    ![Olay türlerini seçin](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. Accumulate bazı veriler sağlar. Arkanıza yaslanın ve kişilere uygulamanızın biraz kullanın. Telemetri geldikçe ve istatistiksel grafiklerde görürsünüz [ölçüm Gezgini](app-insights-metrics-explorer.md) ve olayları tek tek [tanılama arama](app-insights-diagnostic-search.md). 
   
    Ve ayrıca hello veri tooyour depolama dışa aktarır. 
2. Merhaba portalında ya da dışa hello verileri - Seç **Gözat**, depolama hesabınızı seçin ve ardından **kapsayıcıları** - ya da Visual Studio. Visual Studio'da, **görüntülemek / Cloud Explorer**ve Azure açın / depolama. (Bu menü seçeneği yoksa, tooinstall hello Azure SDK'sı gerekir: hello yeni proje iletişim kutusu açın ve Visual C# açın / bulut / .NET için Microsoft Azure SDK'sını alın.)
   
    ![Visual Studio'da açın Server Browser, Azure, depolama](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    Merhaba ortak hello uygulama adı ve araçları anahtarından türetilen hello yol adı parçası not edin. 

Merhaba olayları tooblob dosyaları JSON biçiminde yazılır. Her dosya bir veya daha fazla olaylar içerebilir. Bu nedenle tooread hello olay verileri ve filtre istiyoruz hello alanları isteriz. Her türlü hello verilerle yapabileceğimiz bir şey vardır, ancak bizim planı bugün toouse Stream Analytics toomove hello veri tooa SQL veritabanıdır. Bu kolay toorun çok sayıda ilginç sorguları hale getirir.

## <a name="create-an-azure-sql-database"></a>Bir Azure SQL veritabanı oluşturma
Bir kez daha, aboneliğinizde başlayarak [Azure portal][portal], hello veritabanı oluşturma (ve yeni bir sunucu zaten bir olduğuna sürece) toowhich hello veri yazma.

![Yeni, verileri, SQL](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

Merhaba veritabanı sunucusunu tooAzure Hizmetleri erişimine izin verdiğinden emin olun:

![Gözat, sunucuları, sunucunuz, ayarları, güvenlik duvarı, erişim izni tooAzure](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a>Azure SQL DB tablosu oluşturma
Tercih edilen Yönetim aracınızla hello önceki bölümde oluşturduğunuz toohello veritabanını bağlayın. Bu kılavuzda, biz kullanacağınız [SQL Server Yönetim Araçları](https://msdn.microsoft.com/ms174173.aspx) (SSMS).

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

Yeni bir sorgu oluşturun ve aşağıdaki T-SQL hello yürütün:

```SQL

CREATE TABLE [dbo].[PageViewsTable](
    [pageName] [nvarchar](max) NOT NULL,
    [viewCount] [int] NOT NULL,
    [url] [nvarchar](max) NULL,
    [urlDataPort] [int] NULL,
    [urlDataprotocol] [nvarchar](50) NULL,
    [urlDataHost] [nvarchar](50) NULL,
    [urlDataBase] [nvarchar](50) NULL,
    [urlDataHashTag] [nvarchar](max) NULL,
    [eventTime] [datetime] NOT NULL,
    [isSynthetic] [nvarchar](50) NULL,
    [deviceId] [nvarchar](50) NULL,
    [deviceType] [nvarchar](50) NULL,
    [os] [nvarchar](50) NULL,
    [osVersion] [nvarchar](50) NULL,
    [locale] [nvarchar](50) NULL,
    [userAgent] [nvarchar](max) NULL,
    [browser] [nvarchar](50) NULL,
    [browserVersion] [nvarchar](50) NULL,
    [screenResolution] [nvarchar](50) NULL,
    [sessionId] [nvarchar](max) NULL,
    [sessionIsFirst] [nvarchar](50) NULL,
    [clientIp] [nvarchar](50) NULL,
    [continent] [nvarchar](50) NULL,
    [country] [nvarchar](50) NULL,
    [province] [nvarchar](50) NULL,
    [city] [nvarchar](50) NULL
)

CREATE CLUSTERED INDEX [pvTblIdx] ON [dbo].[PageViewsTable]
(
    [eventTime] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, DROP_EXISTING = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON)

```

![](./media/app-insights-code-sample-export-sql-stream-analytics/34-create-table.png)

Bu örnekte, sayfa görünümleri verilerden kullanıyoruz. toosee kullanılabilir diğer veri Merhaba, JSON çıktısını inceleyin ve hello bkz [veri modeli verme](app-insights-export-data-model.md).

## <a name="create-an-azure-stream-analytics-instance"></a>Bir Azure akış analizi örneği oluşturma
Merhaba gelen [Klasik Azure portalı](https://manage.windowsazure.com/)hello Azure Stream Analytics hizmeti seçin ve yeni bir Stream Analytics işi oluştur:

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

Merhaba yeni iş oluşturulduğunda ayrıntılarını genişletin:

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a>Blob konum ayarlama
Sürekli verme blob tootake girişten ayarlayın:

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

Şimdi, depolama, daha önce not ettiğiniz hesabınızdan, hello birincil erişim anahtarı gerekir. Bu depolama hesabı anahtarı hello ayarlayın.

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a>Set yol önek deseni
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

Emin tooset hello tarih biçimi fazla olması**YYYY-AA-GG** (ile **tire**).

Stream Analytics hello giriş dosyaları hello depoda nasıl bulacağını Hello yol önek deseni belirtir. Tooset gerekir, toocorrespond toohow sürekli verme hello verileri depolar. Aşağıdaki gibi ayarlayın:

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

Bu örnekte:

* `webapplication27`Merhaba Application Insights kaynağı Hello adıdır **tüm alt durumda**. 
* `1234...`Merhaba izleme anahtarını hello Application Insights kaynağı olan **kaldırılan çizgilerle**. 
* `PageViews`Merhaba türü verilerin tooanalyze istiyoruz. Merhaba kullanılabilir türler hello filtresi sürekli dışarı aktarma ile Ayarla bağlıdır. Kullanılabilir diğer türleri Hello dışarı aktarılan verileri toosee hello inceleyin ve hello bakın [veri modeli verme](app-insights-export-data-model.md).
* `/{date}/{time}`bir desen tam anlamıyla yazılır.

tooget hello adı ve Application Insights kaynağınıza iKey Essentials kendi genel bakış sayfasında açın veya ayarları'nı açın.

#### <a name="finish-initial-setup"></a>İlk Kurulumu tamamlayın
Merhaba seri hale getirme biçimi onaylayın:

![Onayla ve sihirbazı kapatın](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

Merhaba sihirbazı kapatın ve hello Kurulum toocomplete için bekleyin.

> [!TIP]
> Merhaba Giriş yolu doğru şekilde ayarladığınızdan emin hello örnek işlevi toocheck kullanın. Başarısız olursa: olup olmadığını veri seçtiğiniz hello örnek zaman aralığı için hello depolama birimindeki denetleyin. Merhaba giriş tanımını düzenlemek ve hello depolama hesabı, yol öneki ve tarih biçimi doğru denetleyin.
> 
> 

## <a name="set-query"></a>Set sorgu
Merhaba sorgu bölümünü açın:

![Stream analytics sorgu seçin](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

Merhaba varsayılan sorguyla değiştirin:

```SQL

    SELECT flat.ArrayValue.name as pageName
    , flat.ArrayValue.count as viewCount
    , flat.ArrayValue.url as url
    , flat.ArrayValue.urlData.port as urlDataPort
    , flat.ArrayValue.urlData.protocol as urlDataprotocol
    , flat.ArrayValue.urlData.host as urlDataHost
    , flat.ArrayValue.urlData.base as urlDataBase
    , flat.ArrayValue.urlData.hashTag as urlDataHashTag
      ,A.context.data.eventTime as eventTime
      ,A.context.data.isSynthetic as isSynthetic
      ,A.context.device.id as deviceId
      ,A.context.device.type as deviceType
      ,A.context.device.os as os
      ,A.context.device.osVersion as osVersion
      ,A.context.device.locale as locale
      ,A.context.device.userAgent as userAgent
      ,A.context.device.browser as browser
      ,A.context.device.browserVersion as browserVersion
      ,A.context.device.screenResolution.value as screenResolution
      ,A.context.session.id as sessionId
      ,A.context.session.isFirst as sessionIsFirst
      ,A.context.location.clientip as clientIp
      ,A.context.location.continent as continent
      ,A.context.location.country as country
      ,A.context.location.province as province
      ,A.context.location.city as city
    INTO
      AIOutput
    FROM AIinput A
    CROSS APPLY GetElements(A.[view]) as flat


```

Belirli toopage görünüm verilerini olduğuna ilk birkaç özellikleri hello edin. Dışarı aktarma diğer telemetri türlerinin farklı özelliklere sahip olur. Merhaba bkz [ayrıntılı hello özellik türleri ve değerleri için veri modeli başvurusu.](app-insights-export-data-model.md)

## <a name="set-up-output-toodatabase"></a>Çıktı toodatabase ayarlayın
SQL hello çıkış olarak seçin.

![Çıkış akış analizleri seçin](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

Merhaba SQL veritabanı belirtin.

![Veritabanınızın Hello ayrıntıları doldurun](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

Merhaba sihirbazı kapatın ve hello çıkış ayarlanmış bir bildirim bekler.

## <a name="start-processing"></a>İşlemini Başlat
Merhaba iş hello eylem çubuğundan başlatın:

![Akış analizi Başlat'ı tıklatın.](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

Toostart işleme şimdi veya daha önceki verilerle toostart başlayarak verileri hello olup olmadığını seçebilirsiniz. Merhaba ikinci verme sürekli bir süredir çalışıyor olsaydı yararlıdır.

![Akış analizi Başlat'ı tıklatın.](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

Birkaç dakika sonra tooSQL sunucu yönetim araçları geri dönün ve içinde veri hello akan izleyin. Örneğin, şöyle bir sorguyu kullanın:

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a>İlgili makaleler
* [Akış analizi kullanarak tooPowerBI dışarı aktarma](app-insights-export-power-bi.md)
* [Ayrıntılı veri başvuru hello özellik türleri ve değerleri için model.](app-insights-export-data-model.md)
* [Application ınsights'ta sürekli dışarı aktarma](app-insights-export-telemetry.md)
* [Application Insights](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

