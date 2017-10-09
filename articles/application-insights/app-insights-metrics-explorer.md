---
title: "Azure Application Insights ölçümlerini aaaExploring | Microsoft Docs"
description: "Ölçüm explorer toointerpret grafikleri nasıl ve nasıl toocustomize ölçüm Gezgini dikey."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: bwren
ms.openlocfilehash: b77ae227ae61e800ad6f3af8a05cd123ea1d69e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-metrics-in-application-insights"></a>Application ınsights'ta ölçümleri keşfederken
Ölçümlerini [Application Insights] [ start] ölçülen değerleri ve telemetri uygulamanızdan gönderilen olaylar sayısı. Performans sorunlarını algılamak ve eğilimleri, uygulamanızın nasıl kullanıldığını içinde izleme yardımcı olur. Çok çeşitli standart ölçümleri yoktur ve kendi özel ölçümleri ve olayları de oluşturabilirsiniz.

Ölçümleri ve olay sayısını, SUM'ları, ortalama veya sayıları gibi toplanmış değerler grafiklerinde görüntülenir.

Grafikler dizi örnek aşağıda verilmiştir:

![](./media/app-insights-metrics-explorer/01-overview.png)

Her yerde ölçümler grafiklerde hello Application Insights portalında bulun. Çoğu durumda bunlar özelleştirilebilir ve daha fazla grafik toohello dikey ekleyebilirsiniz. Merhaba genel bakış dikey penceresinden toomore tıklayın ("Sunucuları" gibi başlıkları olan) grafikler, ayrıntılı veya **ölçüm Gezgini** tooopen özel grafikler oluşturduğunuz yeni bir dikey pencere.

## <a name="time-range"></a>Zaman aralığı
Merhaba hello grafikler veya tüm dikey kılavuzları kapsadığı zaman aralığını değiştirebilirsiniz.

![Dikey penceresinde hello Azure portalı uygulamanızda açık hello genel bakış](./media/app-insights-metrics-explorer/03-range.png)

Henüz görünen kurmadı bazı veriler bekliyorsunuz, Yenile'yi tıklatın. Grafikler kendilerini aralıklarla yenileme ancak hello aralıkları büyük zaman aralıkları için daha uzun. Bir grafik, verileri toocome hello analiz ardışık düzeninden biraz sürebilir.

bir grafik parçası içine toozoom üzerine sürükleyin:

![Bir grafik parçası arasında sürükleyin.](./media/app-insights-metrics-explorer/12-drag.png)

Merhaba geri Yakınlaştırma düğmesi toorestore'ı tıklatın.

## <a name="granularity-and-point-values"></a>Ayrıntı düzeyi ve noktası değerleri
Fare bu noktada hello grafik toodisplay hello değerleri hello ölçümleri gelin.

![Merhaba fare grafiğinin üzerine getirin](./media/app-insights-metrics-explorer/02-focus.png)

belirli bir noktada hello ölçüm Hello değerini hello önceki örnekleme aralığı içinde toplanır.

Merhaba örnekleme aralığı veya "ayrıntı düzeyi" Merhaba dikey penceresinde hello üstünde gösterilir.

![bir dikey pencere Hello üstbilgisi.](./media/app-insights-metrics-explorer/11-grain.png)

Merhaba zaman aralığı dikey penceresinde hello ayrıntı düzeyi ayarlayabilirsiniz:

![bir dikey pencere Hello üstbilgisi.](./media/app-insights-metrics-explorer/grain.png)

Merhaba ayrıntı kullanılabilir seçtiğiniz hello zaman aralığı bağlıdır. Merhaba açık ayrıntı alternatifleri hello zaman aralığına ilişkin toohello "Otomatik" ayrıntı düzeyi var.


## <a name="editing-charts-and-grids"></a>Grafikler ve Izgaralar düzenleme
Yeni bir grafik toohello dikey pencere tooadd:

![Ölçümleri Explorer'da eklemek grafik seçin](./media/app-insights-metrics-explorer/04-add.png)

Seçin **Düzenle** bir mevcut veya yeni bir grafik tooedit gösterdiklerini:

![Bir veya daha çok ölçümü seçin](./media/app-insights-metrics-explorer/08-select.png)

Kısıtlamaları birlikte görüntülenebilir hello birleşimleri hakkında olsa grafikte, birden fazla ölçüm görüntüleyebilirsiniz. Başkalarının devre dışı bırakılır hello bazıları bir ölçüm seçtiğiniz üzerine çıkar.

Kodlu [özel ölçümleri] [ track] uygulamanıza (çağrıları tooTrackMetric ve TrackEvent) bunlar burada listelenir.

## <a name="segment-your-data"></a>Verilerinizi segmentlere
Özelliği - Örneğin, toocompare sayfa görünümleri istemcilerde farklı işletim sistemleri tarafından bir ölçüm bölebilirsiniz.

Bir grafik veya kılavuz, gruplandırılması geçin ve özellik toogroup tarafından seçin:

![Gruplandırma'kümesi seçip bir özellik içinde Group By'ı seçin](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> Gruplandırma kullandığınızda, hello alan ve çubuk grafik türleri Yığılmış bir görünüm sağlar. Merhaba toplama yöntemi toplam olduğu bu uygundur. Ancak hello toplama türü ortalama olduğu hello çizgi veya kılavuz görüntü türlerini seçin.
>
>

Kodlu [özel ölçümleri] [ track] uygulamanıza ve özellik değerlerini içerir, mümkün tooselect hello özelliğinin hello listesinde olması.

Merhaba grafik bölümlenmiş veri için çok küçük mi? Kendi yüksekliğini ayarlayın:

![Merhaba kaydırıcısını ayarlayın](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a>Toplama türleri
Varsayılan olarak hello tarafında Hello gösterge genellikle hello grafik hello dönemi boyunca toplanan hello değerini gösterir. Merhaba grafiğinin üzerine getirirseniz, o noktada hello değerini gösterir.

Her veri hello grafik hello örnekleme aralığı veya "ayrıntı düzeyi" önceki alınan hello veri değerlerinin bir toplama noktasıdır. Merhaba ayrıntı düzeyi hello dikey penceresinde hello üst kısmında gösterilen ve hello ile değişir hello grafik genel ölçeğini.

Ölçümleri farklı şekilde toplanabilir:

* **Count** hello örnekleme aralığında alınan hello olayların sayısıdır. İstekleri gibi olaylar için kullanılır. Merhaba yükseklik Çeşitlemeler hello grafiğin hello olaylar meydana geldiği hello oranı Çeşitlemeler gösterir. Ancak, hello örnekleme aralığı değiştirdiğinizde hello sayısal değer değiştiğine dikkat edin.
* **Sum** hello örnekleme aralığı veya hello grafik hello süre üzerinden alınan tüm hello veri noktalarının hello değerleri toplar.
* **Ortalama** böler hello hello aralığı içinde alınan veri noktası sayısı tarafından Sum hello.
* **Benzersiz** sayıları, kullanıcıları ve hesaplarını sayısı için kullanılır. Merhaba örnekleme aralığı içinde ya da hello grafik hello süre boyunca hello şekil farklı kullanıcılar bu süre içinde görülen hello sayısını gösterir.
* **%**-Her bir toplama yüzdesi sürümleri yalnızca bölümlenmiş grafiklerle kullanılır. Merhaba toplam her zaman too100% ekler ve farklı bileşenlerin toplam hello göreli katkı hello grafik gösterir.

    ![Yüzdesi toplama](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-hello-aggregation-type"></a>Merhaba toplama türünü değiştir

![Merhaba grafik düzenleyin ve ardından toplama seçin](./media/app-insights-metrics-explorer/05-aggregation.png)

Yeni bir grafik veya olduğunda tüm ölçüm seçili oluşturduğunuzda her ölçümü için hello varsayılan yöntemi gösterilir:

![Tüm ölçümleri toosee hello Varsayılanları seçimini kaldırın](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a>PIN y ekseni 
Varsayılan olarak bir grafik sıfır hello veri aralığında toogive görsel bir hello değerlerin Zamanlayıcının en yüksek değerleri kasa başlayarak Y ekseni değerleri gösterir. Ancak bazı durumlarda birden fazla ilginç toovisually olabilir hello Zamanlayıcının değerleri küçük değişiklikler inceleyin. Özelleştirmeleri ister için bu kullanım y ekseni aralık düzenleme özelliği toopin hello y ekseni minimum veya maksimum değeri istediğiniz yerde hello.
"Gelişmiş" onay kutusunu toobring hello yukarı üzerinde y ekseni aralığını ayarlar'ı tıklatın.

![Gelişmiş Ayarlar'ı tıklatın, özel aralık seçin ve min en yüksek değerleri belirtin](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a>Verilerinizi filtre
Seçilen özellik değerlerini birtakım toosee yalnızca hello ölçümleri:

![Filtre'yi tıklatın, bir özelliği'ni genişletin ve bazı değerleri kontrol edin](./media/app-insights-metrics-explorer/19-filter.png)

Belirli bir özellik için herhangi bir değer seçmezseniz, onu sahip hello aynı tümünü seçmek: söz konusu özellik üzerinde hiçbir filtre yoktur.

Her özellik değerini yanında olayların bildirimi hello sayar. Bir özellik değerlerini seçtiğinizde hello değerleri ayarlanır diğer mülkiyet sayar.

Filtreler tooall hello grafikleri bir dikey pencerede uygulayın. Farklı Filtreler uygulanmış istiyorsanız toodifferent grafikleri oluşturun ve farklı ölçümleri Kanatlar kaydedin. İsterseniz, böylece bunları diğer gördüğünüz farklı Kanatlar toohello panosundan grafikleri sabitleyebilirsiniz.

### <a name="remove-bot-and-web-test-traffic"></a>Bot ve web testi trafiği Kaldır
Kullanım hello filtre **gerçek veya yapay trafiği** ve denetleme **gerçek**.

Göre filtre uygulayabilirsiniz **yapay trafik kaynak**.

### <a name="tooadd-properties-toohello-filter-list"></a>tooadd özellikleri toohello filtre listesi
Toofilter telemetri kategorisine kendi seçme ister misiniz? Örneğin, kullanıcılarınız farklı kategorilere yukarı bölmek olabilir ve verilerinizi kategorilerine göre segmentlere ayırmak istiyor musunuz.

[Kendi özellik oluşturmak](app-insights-api-custom-events-metrics.md#properties). Bunu kümesinde bir [Telemetri Başlatıcı](app-insights-api-custom-events-metrics.md#defaults) toohave hello standart telemetri dahil olmak üzere farklı SDK modülleri tarafından gönderilen tüm telemetri - görünür.

## <a name="edit-hello-chart-type"></a>Merhaba grafik türü Düzenle
Kılavuzları ve grafiklerinizi arasında geçiş yapabilirsiniz dikkat edin:

![Kılavuz veya grafiği seçin, sonra bir grafik türü seçin](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a>Ölçümleri dikey pencerenizin Kaydet
Bazı grafiklerde oluşturduğunuz zaman, sık kullanılan olarak kaydedebilirsiniz. Kurumsal bir hesap kullanırsanız, tooshare diğer ile ekip üyelerinin olup olmadığını seçebilirsiniz.

![Sık kullanılan seçin](./media/app-insights-metrics-explorer/21-favorite-save.png)

toosee hello dikey penceresini yeniden **gidin toohello genel bakış dikey** ve Sık Kullanılanlar açın:

![Sık Kullanılanlar Hello genel bakış dikey penceresinde, seçin](./media/app-insights-metrics-explorer/22-favorite-get.png)

Kaydettiğinizde göreli zaman aralığını seçerseniz, hello dikey penceresinde hello son Ölçümleriyle güncelleştirilir. Mutlak zaman aralığını seçerseniz, Göster her zaman aynı veri hello.

## <a name="reset-hello-blade"></a>Merhaba dikey Sıfırla
Yalnızca bir dikey pencerede düzenleyebilir, ancak tooget geri toohello özgün kaydedilmiş kümesi ister misiniz, Sıfırla'yı tıklatın.

![Ölçüm Gezgini hello üstündeki Hello düğmeleri](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a>Canlı ölçümleri akış

Telemetrinizi hakkında daha fazla anlık görünümü için açık [canlı akış](app-insights-live-stream.md). Çoğu ölçümleri toplama hello işlemi nedeniyle birkaç dakika tooappear alın. Bunun aksine, Canlı ölçümleri düşük gecikme süresi için en iyi duruma getirilir. 

## <a name="set-alerts"></a>Uyarı ayarlama
alışılmadık değerlerin herhangi bir ölçümü, e-postayla bildirim toobe bir uyarı ekleyin. Toosend hello e-posta toohello hesap yöneticileri ya da toospecific e-posta adreslerini seçebilirsiniz.

![Uyarı kuralları, ekleme uyarı ölçümleri Explorer'da seçin](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

[Uyarılar hakkında daha fazla bilgi][alerts].


## <a name="continuous-export"></a>Sürekli Dışarı Aktarma
Böylece dışarıdan işleyebilmesi için sürekli olarak verilen verileri istiyorsanız kullanmayı [sürekli verme](app-insights-export-telemetry.md).

### <a name="power-bi"></a>Power BI
Verilerinizin daha zengin görünümlerini isterseniz [tooPower BI verme](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).

## <a name="analytics"></a>Analiz
[Analytics](app-insights-analytics.md) daha verimli bir şekilde tooanalyze güçlü sorgu dili kullanarak telemetrinizi değil. Toocombine istediğiniz veya ölçümleri sonuçlarından işlem veya ayrıntılı incelenmesi uygulamanızın son performansını gerçekleştirmek, bunu kullanın. 

Bir ölçüm grafikten hello Analytics simgesi tooget tıklatabilirsiniz doğrudan toohello eşdeğer Analytics sorgu.

## <a name="troubleshooting"></a>Sorun giderme
*Herhangi bir veri my grafikte bakın yok.*

* Filtreler tooall hello grafikleri hello dikey penceresinde uygulayın. Bir grafik odaklanan olsa da, tüm hello verilerini başka bir dışlar bir filtre ayarlamak alamadık, emin olun.

    Farklı grafiklerde tooset farklı filtreler istiyorsanız, bunları kaydetmek farklı dikey olarak ayrı Sık Kullanılanlar oluşturun. İsterseniz, böylece bunları diğer görebilirsiniz bunları toohello Pano sabitleyebilirsiniz.
* Merhaba ölçüm üzerinde tanımlı değil bir özelliği bir grafik grupla, ardından olacaktır hiçbir şey hello grafikte. 'Group by' temizlemeyi deneyin veya farklı gruplandırma özelliği seçin.
* Performans verilerini (CPU, g/ç hızı vb.) Java web Hizmetleri, Windows Masaüstü uygulamaları, kullanılabilir [IIS, uygulama ve hizmetlere Durum İzleyicisi yüklerseniz web](app-insights-monitor-performance-live-website-now.md), ve [Azure Cloud Services](app-insights-azure.md). Azure Web siteleri için kullanılabilir değil.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Sonraki adımlar
* [Application Insights ile kullanım izleme](app-insights-web-track-usage.md)
* [Tanılama aramayı kullanma](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
