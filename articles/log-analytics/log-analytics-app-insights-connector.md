---
title: Azure Application Insights uygulama verilerini aaaView | Microsoft Docs
description: "Merhaba uygulama Öngörüler Bağlayıcısı çözüm toodiagnose performans sorunlarını ve Application Insights ile izlenen uygulamanızla kullanıcıların ne anlama kullanabilirsiniz."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 49280cad-3526-43e1-a365-c6a3bf66db52
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: banders
ms.openlocfilehash: 38109337ebbc8970dccb65365ba8284d9cee19a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-connector-solution-preview-in-operations-management-suite-oms"></a>Uygulama Öngörüler Bağlayıcısı çözümü (Önizleme) Operations Management Suite (OMS)

![Uygulama Öngörüler simgesi](./media/log-analytics-app-insights-connector/app-insights-connector-symbol.png)

Merhaba uygulamaları Öngörüler Bağlayıcısı çözüm performans sorunlarını tanılamak ve ile izlenen kullanıcılar ile uygulamanızı ne anlamanıza yardımcı olur [Application Insights](../application-insights/app-insights-overview.md). Görünümler hello Application Insights'ta geliştiriciler bkz aynı uygulama telemetri OMS içinde kullanılabilir. Ancak, Application Insights uygulamalarınızı OMS ile tümleştirdiğinizde, uygulamalarınızı görünürlüğünü işlemi ve uygulama verilerini tek bir yerde sağlayarak artar. Sahip, hello aynı görünümleri yardımcı olur, uygulama geliştiriciler ile toocollaborate. Merhaba ortak görünümler hello zaman toodetect azaltmak ve uygulama ve platform sorunları gidermek yardımcı olabilir.

Merhaba çözümünü kullandığınızda aşağıdakileri yapabilirsiniz:

- Farklı Azure aboneliklerinde olsalar bile tüm Application Insights uygulamaları tek bir yerde görüntüleyin
- Uygulama verileri ile altyapı verilerin bağıntısını
- Günlük arama açılardan ile uygulama verileri görselleştirin
- Özet günlük analizi veri tooyour Application Insights hello OMS uygulamada ve Azure portalı

## <a name="connected-sources"></a>Bağlı kaynaklar

Diğer çoğu günlük analizi çözümlerden farklı uygulama Öngörüler Bağlayıcısı hello için aracıları tarafından toplanan veriler değil. Merhaba çözümü tarafından kullanılan tüm verileri doğrudan Azure'dan gelir.

| Bağlı Kaynak | Destekleniyor | Açıklama |
| --- | --- | --- |
| [Windows aracıları](log-analytics-windows-agents.md) | Hayır | Merhaba çözüm Windows aracılardan bilgi toplamaz. |
| [Linux aracıları](log-analytics-linux-agents.md) | Hayır | Merhaba çözüm Linux aracılarını bilgi toplamaz. |
| [SCOM yönetim grubu](log-analytics-om-agents.md) | Hayır | Merhaba çözüm bağlı SCOM yönetim grubunda aracılardan gelen bilgiler toplamaz. |
| [Azure depolama hesabı](log-analytics-azure-storage.md) | Hayır | Merhaba çözüm koleksiyonu bilgileri Azure depolama biriminden değil yapar. |

## <a name="prerequisites"></a>Ön koşullar

- tooaccess uygulama Öngörüler Bağlayıcısı bilgi, bir Azure aboneliğinizin olması gerekir
- En az bir yapılandırılmış Application Insights kaynağı olması gerekir.
- Merhaba sahibi veya katkıda bulunanı hello Application Insights kaynağı olmalıdır.

## <a name="configuration"></a>Yapılandırma

1. Hello Azure Web Apps Analytics hello çözümden etkinleştirmek [Azure Market](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ApplicationInsights?tab=Overview) veya açıklanan hello işlemi kullanarak [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).
2. Merhaba OMS portalında tıklatın **ayarları** &gt; **veri** &gt; **Application Insights**.
3. Altında **bir abonelik seçin**, Application Insights kaynaklara sahip bir abonelik seçin ve ardından **uygulama adı**, bir veya daha fazla uygulamaları seçin.
4. **Kaydet** düğmesine tıklayın.

Yaklaşık 30 dakika içinde veri kullanılabilir hale gelir ve Application Insights döşeme hello hello görüntü aşağıdaki gibi verilerle güncelleştirilir:

![Application Insights döşeme](./media/log-analytics-app-insights-connector/app-insights-tile.png)

Diğer tookeep göz önünde noktaları:

- Yalnızca Application Insights uygulamalar tooone OMS çalışma alanı bağlayabilirsiniz.
- Yalnızca bağlayabilirsiniz [standart veya Premium Application Insights kaynağı](https://azure.microsoft.com/pricing/details/application-insights) tooOMS günlük analizi. Ancak, günlük analizi hello ücretsiz katmanına kullanabilirsiniz.

## <a name="management-packs"></a>Yönetim paketleri

Bu çözüm, bağlı yönetim gruplarında herhangi bir Yönetim Paketi yüklemez.

## <a name="use-hello-solution"></a>Merhaba çözümü kullanın

Merhaba aşağıdaki bölümlerde nasıl hello Application Insights Pano tooview gösterilen hello Kanatlar kullanın ve uygulamalarınızı verilerle etkileşimli açıklanmaktadır.

### <a name="view-application-insights-connector-information"></a>Uygulama Öngörüler Bağlayıcısı bilgilerini görüntüleme

Merhaba tıklatın **Application Insights** döşeme tooopen hello **Application Insights** Kanatlar aşağıdaki Pano toosee hello.

![Uygulama öngörüleri Panosu](./media/log-analytics-app-insights-connector/app-insights-dash01.png)

![Uygulama öngörüleri Panosu](./media/log-analytics-app-insights-connector/app-insights-dash02.png)

Merhaba Pano hello tabloda gösterilen hello Kanatlar içerir. Her dikey penceresinde hello dikey'nın ölçütlerine kapsam ve zaman aralığını belirtilen eşleşen too10 öğeleri listeler. Tüm kayıtları tıkladığınızda döndüren bir günlük arama çalıştırabilirsiniz **tümünü görmek** hello altındaki hello dikey ya da hello dikey başlığını tıklatın.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

| **Sütun** | **Açıklama** |
| --- | --- |
| Uygulamalar - uygulama sayısı | Uygulama Hello sayısı uygulama kaynaklarında gösterir. Ayrıca listeleri uygulama adları ve her biri için uygulama kayıt sayısı hello. Merhaba numara toorun günlük arama için tıklatın<code>Type=ApplicationInsights &#124; measure sum(SampledCount) by ApplicationName</code> <br><br>  Bir uygulama adı toorun ana bilgisayar, telemetri türe göre kayıt ve tüm verileri (Merhaba üzerinde son günü dayanarak) türüne göre uygulama kayıtları gösteren hello uygulama için bir günlük arama tıklayın. |
| Veri birimi – ana verileri gönderme | Verileri gönderme barındıran bilgisayar Hello sayısını gösterir. Ayrıca barındıran bilgisayar ve her konak için kayıt sayısı listelenir. Merhaba numara toorun günlük arama için tıklatın<code>Type=ApplicationInsights &#124; measure sum(SampledCount) by Host</code> <br><br> Bir bilgisayar adı toorun üzerinde uygulama kayıtları ana bilgisayar, telemetri türe göre kayıt ve tüm verileri (Merhaba üzerinde son günü dayanarak) türüne göre gösterir hello ana bilgisayar için bir günlük Ara'yı tıklatın. |
| Kullanılabilirlik – Web testini sonuçları | Web test sonuçları, geçişi veya başarısız olduğunu gösteren bir halka grafik gösterir. Merhaba grafik toorun günlük arama için tıklatın<code>Type=ApplicationInsights TelemetryType=Availability &#124; measure sum(SampledCount) by AvailabilityResult</code> <br><br> Sonuçları geçişleri ve tüm testleri için hata hello sayısını gösterir. Bu trafiği ile tüm Web uygulamaları için hello son dakika gösterir. Bir uygulama adı tooview başarısız web testleri ayrıntılarını gösteren bir günlük Ara'yı tıklatın. |
| Sunucu istekleri – saat başına istek sayısı | Bir çizgi grafiği Merhaba, sunucu istek çeşitli uygulamalar için saat başına gösterir. Bir satır hello grafik toosee hello en üst 3 uygulamalarında zamanında noktasına isteklerini almak üzerine gelerek. Ayrıca istekleri ve istek hello sayısı için seçilen hello süresi alma hello uygulamaların bir listesini gösterir. <br><br>Bir günlük Ara Hello grafik toorun <code>Type=ApplicationInsights TelemetryType=Request &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> sunucu istekleri çeşitli uygulamalar için saat başına Merhaba, daha ayrıntılı bir çizgi grafiği gösterir. <br><br> Bir günlük Ara hello listesi toorun uygulamada <code>Type=ApplicationInsights  ApplicationName=yourapplicationname  TelemetryType=Request</code> yanıt kodları istekleri, saat ve istek süresi üzerinden isteklerine ilişkin grafikleri ve istek listesini listesini gösterir.   |
| Hataları – saat başına başarısız istekleri | Başarısız uygulama isteklerini saatte bir çizgi grafiğini gösterir. Merhaba grafik toosee hello üst 3 uygulamalarla bir noktası için başarısız isteklerin zamanında üzerine gelerek. Ayrıca her hello başarısız istek sayısı ile uygulamaların bir listesini gösterir. Bir günlük Ara Hello grafik toorun <code>Type=ApplicationInsights TelemetryType=Request  RequestSuccess = false &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> başarısız uygulama isteklerinin daha ayrıntılı bir çizgi grafiği gösterir. <br><br>Günlük aramasını hello listesi toorun bir öğeyi tıklatın <code>Type=ApplicationInsights ApplicationName=yourapplicationname TelemetryType=Request  RequestSuccess=false</code> başarısız istekleri, grafiklerde gösterilmiştir başarısız istekler zaman ve istek süresi ve başarısız istek yanıt kodları listesini üzerinden. |
| Özel durumlar – saat başına özel durumlar | Saat başına özel durumların bir çizgi grafiği gösterir. Merhaba grafik toosee hello üst 3 uygulamalarla bir nokta için özel durumlar zamanında üzerine gelerek. Ayrıca her özel durum hello sayısı ile uygulamaların bir listesini gösterir. Bir günlük Ara Hello grafik toorun <code>Type=ApplicationInsights TelemetryType=Exception &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> daha ayrıntılı bir bağlantı grafik özel durumların gösterir. <br><br>Günlük aramasını hello listesi toorun bir öğeyi tıklatın <code>Type=ApplicationInsights  ApplicationName=yourapplicationname TelemetryType=Exception</code> özel durumlar, zaman ve başarısız istekleri üzerinden özel durumlara grafiklerde ve özel durum türleri listesini listesini gösterir.  |

### <a name="view-hello-application-insights-perspective-with-log-search"></a>Merhaba Application Insights perspektif günlük arama ile görüntüleme

Hello panosunda herhangi bir öğeyi tıklattığınızda aramada gösterilen Application Insights perspektif bakın. Merhaba perspektif seçili hello telemetri türüne göre bir genişletilmiş görselleştirme sağlar. Bu nedenle, görselleştirme içerik için farklı telemetri türlerini değiştirir.

Merhaba uygulamalar dikey penceresinde herhangi bir yere tıklattığınızda hello varsayılan bkz **uygulamaları** perspektif.

![Uygulama Öngörüler uygulamaları perspektifi](./media/log-analytics-app-insights-connector/applications-blade-drill-search.png)

Merhaba perspektif seçtiğiniz Merhaba uygulaması özetini gösterir.

Merhaba **kullanılabilirlik** dikey web test sonuçlarını ve başarısız olan ilgili istekleri görebileceğiniz farklı perspektif görünümünü gösterir.

![Uygulama Öngörüler kullanılabilirlik perspektifi](./media/log-analytics-app-insights-connector/availability-blade-drill-search.png)

Tıkladığınızda, herhangi bir yere hello **sunucu istekleri** veya **hataları** Kanatlar, hello perspektif bileşenleri toogive değiştirmek, toorequests ilgili bir görsel öğe.

![Uygulama Öngörüler hataları dikey penceresi](./media/log-analytics-app-insights-connector/server-requests-failures-drill-search.png)

Tıkladığınızda, herhangi bir yere hello **özel durumları** dikey penceresinde, gördüğünüz uyarlanmış bir görsel öğe tooexceptions.

![Uygulama Öngörüler özel durumlar dikey penceresi](./media/log-analytics-app-insights-connector/exceptions-blade-drill-search.png)

Olup, bir şey birini tıklatın bağımsız olarak hello **uygulama Öngörüler Bağlayıcısı** Pano hello içinde **arama** kendisi, Application Insights verileri gösterir hello döndüren herhangi bir sorgu sayfası Uygulama Öngörüler perspektif. Örneğin, Application Insights veri görüntülüyorsanız bir **&#42;** sorgu ayrıca hello perspektif sekmesini hello görüntü aşağıdaki gibi gösterilir:

![Application Insights ](./media/log-analytics-app-insights-connector/app-insights-search.png)

Perspektif bileşenleri hello arama sorgusu bağlı olarak güncelleştirilir. Başka bir deyişle, verileri özelliği toosee hello verir hello herhangi bir arama alanı kullanarak hello sonuçları filtreleyebilirsiniz:

- Tüm uygulamalar
- Tek bir seçilen uygulama
- Bir uygulama grubu

### <a name="pivot-tooan-app-in-hello-azure-portal"></a>Pivot tooan uygulamada hello Azure portalı

Uygulama Öngörüler Bağlayıcısı Kanatlar, toopivot toohello seçili tasarlanmış tooenable olan Application Insights uygulama *hello OMS portalı kullandığınızda*. Bir uygulama gidermenize yardımcı olacak üst düzey bir izleme platform hello çözüm kullanabilirsiniz. Olası bir soruna bağlı uygulamalarınızı hiçbirinde gördüğünüzde, ya da ayrıntıya, OMS arama yapabilir veya doğrudan toohello Application Insights uygulama Özet.

toopivot, hello üç noktaya tıklayın (**...** ) hello her satırın sonunda görünür ve seçin **Application Insights Aç**.

>[!NOTE]
>**Application Insights Aç** hello Azure portalında kullanılamaz.

![Application Insights Aç](./media/log-analytics-app-insights-connector/open-in-app-insights.png)

### <a name="sample-corrected-data"></a>Veri örnek düzeltildi

Application Insights sağlar  *[düzeltme örnekleme](../application-insights/app-insights-sampling.md)*  toohelp telemetri trafiğini azaltır. Application Insights uygulamanıza örnekleme etkinleştirdiğinizde, Application Insights hem de OMS depolanan girişleri azaltılmış sayısını alır. Veri tutarlılığı hello korunur sırada **uygulama Öngörüler Bağlayıcısı** sayfası ve Perspektifler, örneklenen verileri özel sorgularınızı el ile düzeltmeniz gerekir.

Örnekleme düzeltme günlük arama sorguda bir örneği burada verilmiştir:

```
Type=ApplicationInsights | measure sum(SampledCount) by TelemetryType
```

Merhaba **örneklenen sayısı** alan tüm girişler mevcut ve gösterir hello hello girişini temsil eden veri noktası sayısı. Application Insights uygulamanız için örnekleme üzerinde kapatırsanız **örneklenen sayısı** 1'den büyük. toocount hello gerçek girdi sayısı bu değeri, uygulamanızın oluşturduğu toplam hello **örneklenen sayısı** alanları.

Örnekleme yalnızca hello toplam girdi sayısı bu değeri, uygulamanızın oluşturduğu etkiler. Ölçüm alanları için toocorrect örnekleme gerekmeyen **RequestDuration** veya **AvailabilityDuration** hello ortalama gösterilen girişleri için bu alanları göstermek için.

## <a name="input-data"></a>Giriş verisi

Merhaba çözüm bağlı Application Insights uygulamalardan veri telemetri türlerini aşağıdaki hello alır:

- Kullanılabilirlik
- Özel durumlar
- İstekler
- Sayfa görünümleri – çalışma tooreceive görünümleri sayfasında, bu bilgileri, uygulamaları toocollect yapılandırmanız gerekir. Daha fazla bilgi için bkz: [PageViews](../application-insights/app-insights-api-custom-events-metrics.md#page-views).
- Özel olaylar – çalışma alanı, tooreceive özel olaylar için bu bilgileri, uygulamaları toocollect yapılandırmanız gerekir. Daha fazla bilgi için bkz: [TrackEvent](../application-insights/app-insights-api-custom-events-metrics.md#trackevent).

Kullanılabilir olduğunda veri Application Insights gelen OMS tarafından alınır.

## <a name="output-data"></a>Çıktı verileri

Bir kayıtla bir *türü* , *Applicationınsights* her giriş veri türü için oluşturulur. Applicationınsights kayıtları hello aşağıdaki bölümlerde gösterilen özelliklere sahiptir:

### <a name="generic-fields"></a>Genel alanlar

| Özellik | Açıklama |
| --- | --- |
| Tür | ApplicationInsights |
| ClientIP |   |
| TimeGenerated | Merhaba kayıt zamanı |
| ApplicationId | Merhaba Application Insights uygulamasının izleme anahtarı |
| ApplicationName | Merhaba Application Insights uygulamasının adı |
| RoleInstance | Sunucu ana bilgisayar kimliği |
| DeviceType | İstemci aygıtı |
| ScreenResolution |   |
| Kıta | Merhaba isteği geldiği Kıtada |
| Ülke | Merhaba isteği geldiği ülke |
| Bölge | Bölge, durum veya burada kaynaklanan isteği hello yerel ayar |
| Şehir | Şehir veya hello isteği geldiği Şehir |
| isSynthetic | Merhaba isteği bir kullanıcı veya otomatik olarak yöntemi tarafından oluşturulup oluşturulmadığını belirtir. Doğru oluşturulan kullanıcı = ya da yanlış = otomatik yöntemi |
| SamplingRate | Merhaba tooportal gönderilen SDK'sı tarafından oluşturulan telemetri yüzdesi. 0,0 100.0 aralığı. |
| SampledCount | 100/(SamplingRate). Örneğin, 4 =&gt; % 25 |
| IsAuthenticated | True veya false |
| Operationıd | Aynı işlem kimliği ilgili öğeler hello Portalı'nda gösterilen hello sahip öğeler. Genellikle hello istek kimliği |
| ParentOperationID | Merhaba üst işlem kimliği |
| OperationName |   |
| SessionID | GUID toouniquely hello isteği oluşturulduğu hello oturum tanımlayın |
| SourceSystem | ApplicationInsights |

### <a name="availability-specific-fields"></a>Kullanılabilirlik özel alanlar

| Özellik | Açıklama |
| --- | --- |
| TelemetryType | Kullanılabilirlik |
| AvailabilityTestName | Merhaba web test adı |
| AvailabilityRunLocation | Http isteğinin coğrafi kaynak |
| AvailabilityResult | Merhaba başarı hello web testi sonuçlarını gösterir |
| AvailabilityMessage | Merhaba ileti ekli toohello web testi |
| AvailabilityCount | 100 /(Sampling Rate). Örneğin, 4 =&gt; % 25 |
| DataSizeMetricValue | 1.0 veya 0,0 |
| DataSizeMetricCount | 100 /(Sampling Rate). Örneğin, 4 =&gt; % 25 |
| AvailabilityDuration | Merhaba web testi sürenin milisaniye cinsinden süre |
| AvailabilityDurationCount | 100 /(Sampling Rate). Örneğin, 4 =&gt; % 25 |
| AvailabilityValue |   |
| AvailabilityMetricCount |   |
| AvailabilityTestId | Merhaba web testi için benzersiz bir GUID |
| AvailabilityTimestamp | Merhaba kullanılabilirlik testinin kesin zaman damgası |
| AvailabilityDurationMin | Örneklenen kayıtlar için bu alan temsil hello veri noktaları için hello minimum web test süresi (milisaniye cinsinden) gösterir. |
| AvailabilityDurationMax | Örneklenen kayıtlar için bu alan temsil hello veri noktaları için hello en büyük web test süresi (milisaniye cinsinden) gösterir. |
| AvailabilityDurationStdDev | Örneklenen kayıtlar için bu alanda hello standart sapma temsil hello veri noktaları için tüm web test süre (milisaniye) arasında gösterilir. |
| AvailabilityMin |   |
| AvailabilityMax |   |
| AvailabilityStdDev | &nbsp;  |

### <a name="exception-specific-fields"></a>Özel durum özel alanlar

| Tür | ApplicationInsights |
| --- | --- |
| TelemetryType | Özel durum |
| ExceptionType | Merhaba özel durum türü |
| ExceptionMethod | Merhaba özel durumu oluşturur hello yöntemi |
| ExceptionAssembly | Derleme içerir hello framework ve sürüm hello ortak anahtar belirteci yanı sıra |
| ExceptionGroup | Merhaba özel durum türü |
| ExceptionHandledAt | Merhaba özel durumun işlenip hello düzeyini gösterir |
| ExceptionCount | 100 /(Sampling Rate). Örneğin, 4 =&gt; % 25 |
| ExceptionMessage | Merhaba özel durum iletisi |
| ExceptionStack | Tam yığını hello özel durumu |
| ExceptionHasStack | Özel durum yığın varsa true |



### <a name="request-specific-fields"></a>İsteği özel alanlar

| Özellik | Açıklama |
| --- | --- |
| Tür | ApplicationInsights |
| TelemetryType | İstek |
| Yanıt kodu | HTTP yanıt gönderilen tooclient |
| RequestSuccess | Başarı veya başarısızlık gösterir. TRUE veya false. |
| RequestId | Kimliği toouniquely hello isteği tanımlayın |
| RequestName | GET/POST + URL tabanı |
| RequestDuration | Merhaba istek süresini saniye cinsinden süre |
| URL | Konak hariç hello istek URL'si |
| Host | Web sunucusu ana bilgisayar |
| URLBase | Tam URL hello isteği |
| ApplicationProtocol | Merhaba uygulama tarafından kullanılan protokol türü |
| RequestCount | 100 /(Sampling Rate). Örneğin, 4 =&gt; % 25 |
| RequestDurationCount | 100 /(Sampling Rate). Örneğin, 4 =&gt; % 25 |
| RequestDurationMin | Örneklenen kayıtlar için bu alan temsil hello veri noktaları için hello minimum istek süresi (milisaniye cinsinden) gösterir. |
| RequestDurationMax | Örneklenen kayıtlar için bu alan temsil hello veri noktaları için hello en büyük istek süresi (milisaniye cinsinden) gösterir. |
| RequestDurationStdDev | Örneklenen kayıtlar için bu alanda hello standart sapma temsil hello veri noktaları için tüm istek süreleri (milisaniye) arasında gösterilir. |

## <a name="sample-log-searches"></a>Örnek günlük aramaları

Bu çözüm hello Panoda gösterilen örnek günlük aramaları kümesi yok. Örnek günlük arama sorguları açıklamalarını hello ancak gösterilir [görünüm uygulama Öngörüler Bağlayıcısı bilgi](#view-application-insights-connector-information) bölümü.

## <a name="next-steps"></a>Sonraki adımlar

- Kullanım [günlük arama](log-analytics-log-searches.md) tooview ayrıntılı bilgi, Application Insights uygulamalarınız için.
