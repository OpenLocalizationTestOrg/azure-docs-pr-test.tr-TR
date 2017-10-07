---
title: "Azure Application Insights ile Java eclipse'te aaaGet Başlarken | Microsoft docs"
description: "Merhaba Eclipse eklenti tooadd performans ve kullanım tooyour Java Web Application Insights ile izleme kullanın"
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: e88c9f53-cd90-4abc-b097-1f170937908e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: 3142a26a9e2d14c2c433882e3d337f2a8c8f2247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a>Application Insights ile Java eclipse'te kullanmaya başlama
Merhaba Application Insights SDK'sı, telemetri Java web uygulamanızı gönderir kullanımını ve performansını analiz edin. Merhaba kutusunu telemetri artı toowrite özel telemetri kullanabileceğiniz bir API dışında elde etmeniz hello Eclipse için Application Insights eklenti hello SDK projenize otomatik olarak yükler.   

## <a name="prerequisites"></a>Ön koşullar
Şu anda hello eklenti Maven projelerini ve Eclipse dinamik Web projeleri için çalışır.
([Application Insights Ekle tooother Java proje türleri][java].)

Gerekenler:

* Oracle JRE 1.6 veya sonraki sürümleri
* Bir abonelik çok[Microsoft Azure](https://azure.microsoft.com/).
* [Java EE geliştiricileri için Eclipse IDE](http://www.eclipse.org/downloads/), Indigo olarak biliniyordu veya üzeri.
* Windows 7 veya üzeri ya da Windows Server 2008 veya üzeri

## <a name="install-hello-sdk-on-eclipse-one-time"></a>Eclipse (bir kez) üzerinde Hello SDK yükleme
Yalnızca bu makine başına bir kez toodo gerekir. Bu adım, daha sonra hello SDK tooeach dinamik Web projesi ekleyebilirsiniz bir araç yükler.

1. Eclipse'te, Yardım, yeni yazılım Yükle'yi tıklatın.

    ![Yardım, yeni yazılım yükleme](./media/app-insights-java-eclipse/0-plugin.png)
2. Merhaba SDK Azure Araç Seti altında http://dl.microsoft.com/eclipse kullanılıyor.
3. İşaretini **tüm güncelleştirme siteleri başvurun...**

    ![Application Insights SDK'sı, temizlemek için kişi tüm siteleri güncelleştir](./media/app-insights-java-eclipse/1-plugin.png)

Her bir Java projesi için adımları kalan hello izleyin.

## <a name="create-an-application-insights-resource-in-azure"></a>Application Insights kaynağı oluşturma
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Yeni Application Insights kaynağı oluşturma Merhaba uygulama türü tooJava web uygulaması ayarlayın.  

    ![Tıklama + ve Application Insights seçme](./media/app-insights-java-eclipse/01-create.png)  

4. Hello hello yeni kaynağın izleme anahtarını bulun. Toopaste Bu kod projenize kısa bir süre sonra ihtiyacınız olacaktır.  

    ![Merhaba yeni kaynağa genel bakışta, Özellikler'i tıklatın ve hello izleme anahtarını kopyalama](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-tooyour-project"></a>Application Insights tooyour proje ekleyin
1. Application Insights hello bağlam menüsünden Java web projenize ekleyin.

    ![Merhaba yeni kaynağa genel bakışta, Özellikler'i tıklatın ve hello izleme anahtarını kopyalama](./media/app-insights-java-eclipse/02-context-menu.png)
2. Hello Azure portal ' aldığınız hello izleme anahtarını yapıştırın.

    ![Merhaba yeni kaynağa genel bakışta, Özellikler'i tıklatın ve hello izleme anahtarını kopyalama](./media/app-insights-java-eclipse/03-ikey.png)

başlangıç anahtarı telemetrinin her öğesiyle birlikte gönderilir ve Application Insights toodisplay söyler kaynağınız içinde.

## <a name="run-hello-application-and-see-metrics"></a>Merhaba uygulamayı çalıştırın ve ölçümleri bakın
Uygulamanızı çalıştırın.

Microsoft Azure'da tooyour Application Insights kaynağı döndür.

HTTP istekleri verileri hello genel bakış dikey penceresinde görünür. (Orada değilse, birkaç saniye bekleyip Yenile’ye tıklayın.)

![Sunucu yanıtı, istek sayısını ve hataları ](./media/app-insights-java-eclipse/5-results.png)

Tıklatın herhangi grafik toosee ayrıntılı ölçümler.

![Ada göre istek sayısı](./media/app-insights-java-eclipse/6-barchart.png)

[Ölçümler hakkında daha fazla bilgi edinin.][metrics]

Ve istek hello özellikleri görüntülendiğinde, istekler ve özel durumlar gibi ilişkili hello telemetri olayları görebilirsiniz.

![Bu istek için tüm izlemeleri](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a>İstemci tarafı telemetri
Merhaba hızlı başlangıç dikey penceresinden Get kod toomonitor web sayfalarımı tıklayın:

![Uygulama genel bakış dikey pencerenizde, Hızlı Başlat'ı seçin, web sayfalarımı kod toomonitor alın. Merhaba betiği kopyalayın.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

HTML dosyalarınızı hello head içinde Hello kod parçacığını ekleyin.

#### <a name="view-client-side-data"></a>İstemci tarafı verileri görüntüleme
Güncelleştirilmiş web sayfalarınıza açın ve bunları kullanın. Veya iki dakika bekleyin, sonra tooApplication Öngörüler ve açık hello kullanım dikey döndürür. (Merhaba genel bakış dikey penceresinden aşağı kaydırın ve kullanımı'nı tıklatın.)

Sayfa görünümü, kullanıcı ve oturum ölçümleri hello kullanım dikey penceresinde görünür:

![Oturumlar, kullanıcılar ve sayfa görünümleri](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

[İstemci tarafı telemetri için ayarlama hakkında daha fazla bilgi edinin.][usage]

## <a name="publish-your-application"></a>Uygulamanızı yayımlama
Artık uygulama toohello sunucunuza yayımlayın, kullanmak ve hello portalda hello telemetri izleyin, kullanıcıların izin verir.

* Güvenlik duvarınızın, uygulama toosend telemetri toothese bağlantı noktaları verdiğinden emin olun:

  * dc.services.visualstudio.com:443
  * dc.services.visualstudio.com:80
  * f5.services.visualstudio.com:443
  * f5.services.visualstudio.com:80
* Windows sunucularda yüklenecekler:

  * [Microsoft Visual C++ Yeniden Dağıtılabilir](http://www.microsoft.com/download/details.aspx?id=40784)

    (Performans sayaçlarını etkinleştirir.)

## <a name="exceptions-and-request-failures"></a>Özel durumlar ve istek hataları
İşlenmeyen özel durumlar otomatik olarak toplanır:

![](./media/app-insights-java-eclipse/21-exceptions.png)

diğer özel durumlar toocollect verileri, iki seçeneğiniz vardır:

* [INSERT çağırır tooTrackException kodunuzda](app-insights-api-custom-events-metrics.md#trackexception).
* [Sunucunuza Hello Java Agent Yükleme](app-insights-java-agent.md). Toowatch istediğiniz hello yöntemleri belirtin.

## <a name="monitor-method-calls-and-external-dependencies"></a>Yöntem çağrılarını ve dış bağımlılıkları izleme
[Merhaba Java Agent Yükleme](app-insights-java-agent.md) toolog belirtilen dahili yöntemleri ve zamanlama verileriyle JDBC yapılan çağrıları.

## <a name="performance-counters"></a>Performans sayaçları
Genel Bakış dikey penceresini aşağı kaydırarak ve hello tıklatın **sunucuları** döşeme. Bir dizi performans sayacı göreceksiniz.

![Tooclick hello sunucuları döşeme kaydırın](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a>Performans sayacı koleksiyonunu özelleştirme
performans sayaçları, standart kümesi hello toodisable koleksiyonu hello hello Applicationınsights.XML dosyasının kök düğümü altında koddan hello ekleyin:

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a>Ek performans sayaçlarını toplama
Ek performans sayaçları toobe toplanan belirtebilirsiniz.

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a>JMX sayaçları (Java sanal makinesi hello tarafından gösterilen)

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* `displayName`– hello Application Insights portalında görüntülenen hello adı.
* `objectName`– hello JMX nesne adı.
* `attribute`– hello JMX nesne adı toofetch hello özniteliği
* `type`(isteğe bağlı) - JMX nesnenin öznitelik türü hello:
  * Varsayılan: int veya long gibi basit bir tür.
  * `composite`: hello performans sayacı verileri 'Attribute.Data' hello biçiminde değil
  * `tabular`: hello performans sayacı verileri tablo satırı hello biçiminde değil

#### <a name="windows-performance-counters"></a>Windows performans sayaçları
Her [Windows performans sayacı](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) bir kategorinin üyesidir (Merhaba, bir alanın bir sınıf üyesi olduğunu aynı şekilde). Kategoriler genel olabileceği gibi numaralı veya adlı örneklere de sahip olabilir.

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* displayName – hello Application Insights portalında görüntülenen hello adı.
* categoryName – bu performans sayacı ilişkilendirildiği hello performans sayacı kategorisi (performans nesnesi).
* counterName – hello hello performans sayacının adını.
* instanceName – hello hello performans sayacı kategorisi örneğinin adını ya da boş bir dize (""), tek bir örnek hello kategorisi içerir. Merhaba categoryName işlem toocollect istediğinizi hello performans sayacı olduğundan hello geçerli JVM işleminden ise, uygulamanızı çalıştıran, belirtin `"__SELF__"`.

Özel ölçümleriniz [Ölçüm Gezgini][metrics]'nde olduğundan performans sayaçlarınız görünürdür.

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a>Unix Performans sayaçları
* [Merhaba Application Insights eklentisiyle collectd yükleyin](app-insights-java-collectd.md) tooget çok çeşitli sistem ve ağ verileri.

## <a name="availability-web-tests"></a>Kullanılabilirlik web testleri
Application Insights olan yukarı düzenli aralıklarla toocheck ve düzgün yanıt Web sitenizi test edebilirsiniz. [Yukarı tooset][availability], tooclick kullanılabilirlik aşağı kaydırın.

![Aşağı kaydırıp, Kullanılabilirlik’e ve Web testi ekle’ye tıklama](./media/app-insights-java-eclipse/31-config-web-test.png)

Yanıt süreleri grafiklerine ek olarak, siteniz devre dışı kalırsa e-posta bildirimleri de alacaksınız.

![Web testi örneği](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

[Kullanılabilirlik web testleri hakkında daha fazla bilgi edinin.][availability]

## <a name="diagnostic-logs"></a>Tanılama günlükleri
Logback veya Log4J kullanıyorsanız (1.2 sürümü veya v2.0) izleme için otomatik olarak tooApplication burada keşfedin ve bunlar üzerinde arama Öngörüler gönderilen, izleme günlükleri sahip olabilir.

[Tanılama günlükleri hakkında daha fazla bilgi edinin][javalogs]

## <a name="custom-telemetry"></a>Özel telemetri
Birkaç satır kod ile kullanıcıların gerçekleştirdiği çıkışı, Java web uygulaması toofind eklemek veya toohelp sorunları tanılayın.

Web sayfası JavaScript hem de hello sunucu tarafı Java kod ekleyebilirsiniz.

[Özel telemetri hakkında bilgi edinin][track]

## <a name="next-steps"></a>Sonraki adımlar
#### <a name="detect-and-diagnose-issues"></a>Sorunlarını tanılamak ve Algıla
* [Web istemcisi telemetrisini ekleyin] [ usage] tooget performans telemetrisini hello web istemcisi.
* [Web testleri oluşturma] [ availability] toomake uygulamanızın canlı ve duyarlı kaldığından emin.
* [Olayları ve günlükleri arayın] [ diagnostic] toohelp sorunları tanılayın.
* [Log4J veya Logback izlemelerini yakalama][javalogs]

#### <a name="track-usage"></a>Kullanımı İzleme
* [Web istemcisi telemetrisini ekleyin] [ usage] toomonitor sayfa görünümleri ve temel kullanıcı ölçümleri.
* [Özel olayları ve ölçümleri izleme](app-insights-web-track-usage.md) nasıl uygulamanız, hem hello istemci ve hello sunucu kullanıldığı hakkında toolearn.

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
