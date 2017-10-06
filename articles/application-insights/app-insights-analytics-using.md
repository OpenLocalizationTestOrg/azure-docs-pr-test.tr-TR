---
title: "aaaUsing analizi - hello güçlü arama aracının Azure Application Insights | Microsoft Docs"
description: "Merhaba Analytics, Application Insights hello güçlü tanılama arama aracını kullanma. "
services: application-insights
documentationcenter: 
author: danhadari
manager: carmonm
ms.assetid: c3b34430-f592-4c32-b900-e9f50ca096b3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6e0246848457db368c57d08c47b5bf73f4e5e3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-analytics-in-application-insights"></a>Application Insights'ta Analytics kullanma
[Analytics](app-insights-analytics.md) hello güçlü arama özelliği [Application Insights](app-insights-overview.md). Bu sayfaları günlük analizi sorgu dili açıklanmaktadır.

* **[Merhaba tanıtım videosunu izleyin](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Benzetimli verilerimizi Analytics sürücüde test](https://analytics.applicationinsights.io/demo)**  uygulamanızı veri tooApplication Öngörüler henüz değil gönderiliyorsa.

## <a name="open-analytics"></a>Açık analizi
Giriş kaynağının, uygulamanızın Application ınsights'ta, Analytics'ı tıklatın.

![Portal.Azure.com açın, Application Insights kaynağınıza açın ve analizi'ı tıklatın.](./media/app-insights-analytics-using/001.png)

Merhaba satır içi öğretici neler yapabileceğiniz hakkında fikir edinmek sağlar.

Var olan bir [burada daha kapsamlı Turu](app-insights-analytics-tour.md).

## <a name="query-your-telemetry"></a>Telemetrinizi sorgu
### <a name="write-a-query"></a>Bir sorgu yazın
![Şema görüntüleme](./media/app-insights-analytics-using/150.png)

Merhaba adını hello sol tarafta listelenen hello tablolar ile başlar (veya hello [aralığı](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) veya [UNION](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) işleçleri). Kullanım `|` kanalı a toocreate [işleçleri](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html). 

IntelliSense hello işleçleri ile kullanabileceğiniz hello ifade öğeleri ister. Merhaba bilgi simgesini tıklatın (veya CTRL + ARA ÇUBUĞU tuşlarına basın) tooget daha uzun bir açıklama ve örnekleri toouse her öğe.

Merhaba bkz [Analytics dil Turu](app-insights-analytics-tour.md) ve [dil başvurusu](app-insights-analytics-reference.md).

### <a name="run-a-query"></a>Sorgu çalıştırma
![Bir sorgu çalıştırılarak](./media/app-insights-analytics-using/130.png)

1. Sorguda tek satır sonları kullanabilirsiniz.
2. Merhaba imleç içinde veya toorun istediğiniz hello sorgu hello sonunda yerleştirin.
3. Sorgunuzu Hello zaman aralığını denetleyin. (Bunu değiştirmek veya kendi dahil ederek geçersiz kılma [ `where...timestamp...` ](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) yan tümcesinde, sorgunuzu.)
3. Git toorun hello sorgu tıklayın.
4. Boş satırlar sorgunuzda koymayın. Boş satırlar ile ayırarak bir sorgu sekmede birkaç ayrılmış sorguları kullanmaya devam edebilir. Merhaba imleç sahip hello sorguyu çalıştırır.

### <a name="save-a-query"></a>Bir sorguyu kaydetme
![Bir sorguyu kaydetme](./media/app-insights-analytics-using/140.png)

1. Merhaba geçerli sorgu dosyasını kaydedin.
2. Kaydedilmiş sorgu dosyasını açın.
3. Yeni bir sorgu dosyası oluşturun.

## <a name="see-hello-details"></a>Merhaba Ayrıntılar bakın
Merhaba sonuçları toosee herhangi bir satırın özelliklerini tam listesini genişletin. Daha fazla herhangi bir yapılandırılmış değer - Örneğin, özellik, özel boyutları veya bir özel durum listeleme hello yığını genişletebilirsiniz.

![Bir satır genişletin](./media/app-insights-analytics-using/070.png)

## <a name="arrange-hello-results"></a>Merhaba sonuçları düzenleyin
Sıralama, filtre, sayfalara bölme ve grup, sorgunun döndürdüğü hello sonuçları.

> [!NOTE]
> Sıralama, gruplandırma ve filtreleme hello tarayıcıda sorgunuzu yeniden çalıştırmayın. Bunlar yalnızca son sorgu tarafından döndürülen hello sonuçları yeniden düzenleyin. 
> 
> tooperform hello sonuç döndürmeden önce hello Server'daki bu görevler yazma sorgunuzu hello ile [sıralama](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [özetlemek](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) ve [burada](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) işleçler.
> 
> 

Yaptığınız hello sütunları çekme toosee gibi sütun üst bilgileri toorearrange bunları ve yeniden boyutlandırma sütunları kendi kenarlıklarını sürükleyerek sürükleyin.

![Sütunları düzenleme](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a>Sıralama ve filtreleme öğeleri
Sonuçlarınızı hello head bir sütunun tıklayarak sıralayın. Toosort hello başka bir şekilde yeniden tıklayın ve tıklatın üçüncü kez toorevert toohello özgün sorgu tarafından döndürülen sıralama.

Merhaba filtre simgesini toonarrow aramanızı kullanın.

![Sütunları sıralama ve filtreleme](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a>Öğeleri gruplandırma
toosort birden fazla sütuna göre gruplandırma kullanın. İlk etkinleştirmek ve sütun üst bilgileri Merhaba tablonun yukarısındaki hello alanına sürükleyin.

![Grup](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a>Bazı sonuçları eksik mi?

Beklediğiniz tüm hello sonuçları görmüyorsanız düşünüyorsanız, birkaç olası nedeni vardır.

* **Zaman aralığı filtresi**. Varsayılan olarak, yalnızca son 24 saat hello sonuçları görürsünüz. Merhaba kaynak tablolardan alınan sonuçları hello aralığını sınırlar otomatik bir filtre yok. 

    Bununla birlikte, hello zaman aralığını değiştirebilirsiniz hello açılan menüsünü kullanarak filtre.

    Ya da kendi dahil ederek hello otomatik aralık geçersiz kılabilirsiniz [ `where  ... timestamp ...` yan tümcesi](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) sorgunuzu içine. Örneğin:

    `requests | where timestamp > ago('2d')`

* **Sonuç sınırı**. Merhaba portalından döndürülen hello sonuçları yaklaşık 10 k satırlarda sınırı yoktur. Merhaba sınırın gidin, bir uyarı gösterir. Bu durumda, sonuçlarınızı hello tablosundaki sıralama her zaman, tüm hello gerçek ilk veya son sonuçları göstermeyecektir. 

    İyi bir uygulama tooavoid basarsa hello sınırı'dir. Merhaba zaman aralığı filtresi veya işleçleri gibi kullanın:

  * [zaman damgası tarafından ilk 100](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [100 alın](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [Özetle](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [Burada zaman damgası > ago(3d)](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

(10'dan fazla k satırları istiyorsunuz? Kullanmayı [sürekli verme](app-insights-export-telemetry.md) yerine. Analytics alınırken ham verileri yerine analiz için tasarlanmıştır.)

## <a name="diagrams"></a>Diyagramları
İstediğiniz diyagram Hello türünü seçin:

![Bir diyagram türü seçin](./media/app-insights-analytics-using/230.png)

Merhaba sağ türlerinin birkaç sütun varsa, hello x ve y eksenleri ve boyutları toosplit hello sonuçlarına göre bir sütun seçebilirsiniz.

Varsayılan olarak, sonuçlar başlangıçta tablo olarak görüntülenir ve hello diyagramı el ile seçin. Ancak hello kullanabilirsiniz [yönergesi işlemek](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) hello sonunda sorgu tooselect bir diyagramı.

### <a name="analytics-diagnostics"></a>Analytics tanılama


Bir timechart üzerinde ani ani veya verilerinizi adımda ise hello satırında vurgulanan noktasının görebilirsiniz. Bu Analytics tanılama hello ani değişiklik filtre özellikleri bileşimini belirledi gösterir. Başlangıç noktası tooget hello filtre ve toosee hello filtrelenmiş sürüm üzerinde daha fazla ayrıntı'ı tıklatın. Bu, hangi nedeniyle hello değişiklik belirlemenize yardımcı olabilir. 

[Analytics Tanılama hakkında daha fazla bilgi edinin](app-insights-analytics-diagnostics.md)


![Analytics tanılama](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-toodashboard"></a>PIN toodashboard
Bir diyagram veya tablo tooone, sabitleyebilirsiniz, [panolar paylaşılan](app-insights-dashboards.md) -yalnızca hello PIN'ı tıklatın. (Çok gerekebilecek[yükseltme uygulamanızı paket fiyatlandırma kullanıcının](app-insights-pricing.md) bu özellik üzerinde tooturn.) 

![Merhaba PIN'ı tıklatın](./media/app-insights-analytics-using/pin-01.png)

Bu, hello performans veya web hizmetlerinizi kullanımını izleme Panosu toohelp birlikte geçirdiğinizde, oldukça karmaşık bir analiz hello yanında diğer ölçümleri ekleyebilirsiniz, anlamına gelir. 

Dört veya daha az sütun varsa bir tablo toohello Pano sabitleyebilirsiniz. Yalnızca hello üst yedi satır görüntülenir.

### <a name="dashboard-refresh"></a>Pano yenileme
Merhaba sabitlenmiş grafik toohello Pano hello sorgu yaklaşık olarak saatte yeniden çalıştırarak otomatik olarak yenilenir. Merhaba Yenile düğmesini tıklatabilirsiniz.

### <a name="automatic-simplifications"></a>Otomatik basitleştirme

Belirli basitleştirme tooa panoya Sabitle uygulanan tooa grafik olur.

**Kısıtlama süresi:** sorgular son 14 gün otomatik olarak sınırlı toohello gerçekleşiyor. Merhaba etkisi olan hello aynı sorgunuz içeriyorsa gibi `where timestamp > ago(14d)`.

**Bin sayısı kısıtlaması:** ayrık depo (genellikle bir çubuk grafiği), daha az doldurulan depo otomatik olarak gruplandırılır bir tek "başkalarının" Merhaba çok sahip bir grafik görüntülerseniz depo. Örneğin, bu sorgu:

    requests | summarize count_search = count() by client_CountryOrRegion

analytics'te şöyle görünür:

![İle uzun tail grafik](./media/app-insights-analytics-using/pin-07.png)

ancak tooa panoya Sabitle, şöyle görünür:

![İle sınırlı depo grafik](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-tooexcel"></a>TooExcel dışarı aktarma
Bir sorgu çalıştırdıktan sonra bir .csv dosyası indirebilirsiniz. Tıklatın **Excel'e,**.

## <a name="export-toopower-bi"></a>TooPower BI dışarı aktarma
Sorguda Hello imleç koyun ve seçin **verme, Power BI**.

![Analytics tooPower BI ' dışarı aktarma](./media/app-insights-analytics-using/240.png)

Power BI'da hello sorgu çalıştırın. Toorefresh bir zamanlamaya göre ayarlayabilirsiniz.

Power BI sayesinde, çok çeşitli kaynaklardan verileri bir araya getirme panolar oluşturabilirsiniz.

[Dışarı aktarma tooPower BI hakkında daha fazla bilgi edinin](app-insights-export-power-bi.md)

## <a name="deep-link"></a>Ayrıntılı bağlantı

Bir bağlantı altında **verme, paylaşım bağlantı** tooanother kullanıcı gönderebilir. Merhaba kullanıcının sağlanan [erişim tooyour kaynak grubu](app-insights-resources-roles-access-control.md), hello sorgu hello Analytics UI açılır.

(Sonra hello sorgu metni hello bağlantıdaki görünür "? q =" gzip sıkıştırılmış ve base-64 kodlamalı. Kod toogenerate ayrıntılı bağlantılar toousers sağladığınız yazabilirsiniz. Ancak, hello kodundan yolu toorun Analytics hello kullanarak önerilir [REST API](https://dev.applicationinsights.io/).)


## <a name="automation"></a>Otomasyon

Kullanım hello [veri erişim REST API](https://dev.applicationinsights.io/) toorun Analytics sorgular. [Örneğin](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (PowerShell kullanarak):

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

Analytics UI Hello farklı olarak, herhangi bir zaman damgası sınırlaması tooyour sorgu hello REST API otomatik olarak eklemez. Tooadd kendi where yan tümcesi, büyük yanıtları alma tooavoid unutmayın.



## <a name="import-data"></a>Veri içeri aktarma

Bir CSV dosyasından veri içeri aktarabilirsiniz. Tipik bir kullanım, telemetrisinden tablolarla katılabilirsiniz tooimport statik verilerdir. 

Örneğin, kimliği doğrulanmış kullanıcılar, telemetri bir diğer ad veya karıştırılmış kimliğe göre belirlenirse, diğer adlar tooreal adlarını eşleyen bir tablo içe aktarılamadı. Merhaba isteği telemetriyi bir birleştirme gerçekleştirerek hello Analytics raporlarında gerçek adlarına göre kullanıcılar tanımlayabilirsiniz.

### <a name="define-your-data-schema"></a>Veri şemanızı tanımlayın

1. Tıklatın **ayarları** (sol üst) ve ardından **veri kaynakları**. 
2. Merhaba yönergeleri izleyerek bir veri kaynağı ekleyin. Olduğunuz en az on satır içermelidir hello veri örneği toosupply istedi. Ardından, hello şema de düzeltin.

Bu, daha sonra bir veri kaynağı tanımlar tooimport tek tek tablolar kullanın.

### <a name="import-a-table"></a>Tablo alma

1. Veri kaynağı tanımınız hello listeden açın.
2. "Karşıya Yükle" seçeneğini tıklatın ve hello yönergeleri tooupload hello tablo izleyin. Bu çağrı tooa REST API içerir ve dolayısıyla kolay tooautomate taşır. 

Tablonuz analitik sorguları kullanmak için kullanıma sunulmuştur. Analizleri görünür 

### <a name="use-hello-table"></a>Merhaba tabloyu kullanın

Şimdi veri kaynağı tanımınız varsayın `usermap`, ve iki alan olduğunu `realName` ve `user_AuthenticatedId`. Merhaba `requests` da tablolu adında bir alan `user_AuthenticatedId`kolay toojoin gelir bunları:

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
Merhaba isteklerinin ortaya çıkan tabloda sahip başka bir sütuna `realName`.

### <a name="import-from-logstash"></a>LogStash alma

Kullanırsanız [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), günlüklerinizi Analytics tooquery kullanabilirsiniz. Kullanım hello [veri analizi kanallar eklentisi](https://github.com/Microsoft/logstash-output-application-insights). 

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

