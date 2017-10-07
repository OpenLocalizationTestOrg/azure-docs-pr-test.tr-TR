---
title: "Azure Application Insights ile aaaJava web uygulaması analizi | Microsoft Docs"
description: "Application Insights ile Java web uygulamaları için Uygulama Performansı İzleme. "
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 051d4285-f38a-45d8-ad8a-45c3be828d91
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6555ee53a44f937350e4fa296080f7dce4f45226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a>Java web projesinde Application Insights ile başlarken


[Application Insights](https://azure.microsoft.com/services/application-insights/) yardımcı olan web geliştiricileri hello performansını ve canlı uygulamanızın kullanımını anlamak için bir genişletilebilir bir analiz hizmetidir. Çok kullanmak[performans sorunlarını ve özel durumlarını saptayıp tanılamanıza](app-insights-detect-triage-diagnose.md), ve [kod yazmayı] [ api] tootrack hangi kullanıcıların uygulamanızı yapın.

![örnek veri](./media/app-insights-java-get-started/5-results.png)

Application Insights; Linux, Unix veya Windows üzerinde çalışan Java uygulamalarını destekler.

Gerekenler:

* Oracle JRE 1.6 veya sonraki sürümleri ya da Zulu JRE 1.6 veya sonraki sürümleri
* Bir abonelik çok[Microsoft Azure](https://azure.microsoft.com/).

*Zaten Canlı olan bir web uygulaması varsa, hello alternatif yordam çok izleyebilirsiniz[hello SDK hello web sunucusunda çalışma zamanında ekleme](app-insights-java-live.md). Bu alternatif hello kodun yeniden engellese de, hello seçeneği toowrite kod tootrack kullanıcı etkinliği elde etmezsiniz.*

## <a name="1-get-an-application-insights-instrumentation-key"></a>1. Application Insights izleme anahtarı edinme
1. İçinde toohello oturum [Microsoft Azure portal](https://portal.azure.com).
2. Bir Application Insights kaynağı oluşturun. Merhaba uygulama türü tooJava web uygulaması ayarlayın.

    ![Ad girme, Java web uygulaması seçme ve Oluştur’a tıklama](./media/app-insights-java-get-started/02-create.png)
3. Hello hello yeni kaynağın izleme anahtarını bulun. Toopaste bu anahtar kod projenize kısa bir süre sonra ihtiyacınız vardır.

    ![Merhaba yeni kaynağa genel bakışta, Özellikler'i tıklatın ve hello izleme anahtarını kopyalama](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-hello-application-insights-sdk-for-java-tooyour-project"></a>2. Java tooyour projesi için Hello Application Insights SDK ekleme
*Projeniz için uygun şekilde Hello seçin.*

#### <a name="if-youre-using-eclipse-toocreate-a-maven-or-dynamic-web-project-"></a>Kullanıyorsanız, toocreate Maven veya dinamik Web projesi Tutulma...
Kullanım hello [Java eklentisi için Application Insights SDK][eclipse].

#### <a name="if-youre-using-maven"></a>Maven kullanıyorsanız...
Projeniz zaten toouse Maven derleme için ayarladıysanız, aşağıdaki kodu tooyour pom.xml dosyasına hello birleştirin.

Ardından, yenileme hello proje bağımlılıkları tooget hello ikili dosyaları indirilir.

```XML

    <repositories>
       <repository>
          <id>central</id>
          <name>Central</name>
          <url>http://repo1.maven.org/maven2</url>
       </repository>
    </repositories>

    <dependencies>
      <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-web</artifactId>
        <!-- or applicationinsights-core for bare API -->
        <version>[1.0,)</version>
      </dependency>
    </dependencies>
```

* *Derleme veya sağlama toplamı doğrulama hataları mı var?* `<version>1.0.n</version>` gibi belirli bir sürümü kullanmayı deneyin. Hello hello en son sürümünü bulacaksınız [SDK sürüm notlarında](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) veya bizim [Maven yapıtları](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).
* *Tooupdate tooa gereken yeni SDK?* Proje bağımlılıklarınızı yenileyin.

#### <a name="if-youre-using-gradle"></a>Gradle kullanıyorsanız...
Projeniz zaten toouse Gradle derleme için ayarladıysanız, aşağıdaki kodu tooyour build.gradle dosyasına hello birleştirin.

Ardından yenileme hello proje bağımlılıkları tooget hello ikili dosyaları indirilir.

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* *Derleme veya sağlama toplamı doğrulama hataları mı var? `version:'1.0.n'` gibi belirli bir sürümü kullanmayı deneyin*. *Hello hello en son sürümünü bulacaksınız [SDK sürüm notlarında](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*
* *tooupdate tooa yeni SDK'sı*
  * Proje bağımlılıklarınızı yenileyin.

#### <a name="otherwise-"></a>Aksi taktirde...
El ile Merhaba SDK ekleyin:

1. Merhaba karşıdan [Java için Application Insights SDK](https://aka.ms/aijavasdk).
2. Hello ikili dosyaları hello zip dosyasından ayıklayıp tooyour proje ekleyin.

### <a name="questions"></a>Sorular...
* *Merhaba hello arasındaki ilişki nedir `-core` ve `-web` hello zip bileşenlerinde?*

  * `applicationinsights-core`tam API hello sağlar. Bu bileşen her zaman gerekecektir.
  * `applicationinsights-web`, HTTP istek sayısını ve yanıt sürelerini izleyen ölçümleri sağlar. Bu telemetrinin otomatik olarak toplanmasını istemiyorsanız, bu bileşeni atlayabilirsiniz. Örneğin, toowrite kendi istiyorsanız.
* *tooupdate hello değişiklikleri yayımladığınızda SDK*

  * Merhaba son karşıdan [Java için Application Insights SDK](https://aka.ms/qqkaq6) ve eskilerle hello Değiştir.
  * Değişiklikleri hello açıklanan [SDK sürüm notlarında](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).

## <a name="3-add-an-application-insights-xml-file"></a>3. Application Insights .xml dosyasını ekleme
Projenizde toohello kaynaklar klasörüne applicationınsights.xml dosyasını ekleyin veya tooyour projenin dağıtım sınıfı yoluna eklendiğinden emin olun. XML içine aşağıdaki hello kopyalayın.

Hello Azure portal ' aldığınız hello izleme anahtarını Bununla değiştirin.

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- hello key from hello portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data tooeach event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```


* Merhaba izleme anahtarı telemetrinin her öğesiyle birlikte gönderilir ve Application Insights toodisplay söyler kaynağınız içinde.
* Merhaba HTTP isteği bileşeni isteğe bağlıdır. İstek ve yanıt sürelerini toohello portal hakkında telemetriyi otomatik olarak gönderir.
* Olay bağıntısı bir toplama toohello HTTP isteği bileşendir. Merhaba sunucu tarafından alınan bir tanımlayıcı tooeach isteği atar ve bu tanımlayıcı telemetri bir özellik tooevery öğesi olarak 'Operation.Id' hello özelliği olarak ekler. Bir filtre ayarlayarak her istekle ilişkili toocorrelate hello telemetri tanır [tanılama arama][diagnostic].
* Merhaba Application Insights anahtar geçirilebilir dinamik olarak hello Azure portalında bir sistem özelliği olarak (-DAPPLICATION_INSIGHTS_IKEY your_ikey =). Tanımlı bir özellik yoksa, Azure Uygulama Ayarlarında ortam değişkeni (APPLICATION_INSIGHTS_IKEY) denetlenir. Her iki hello özellikleri tanımsızdır hello varsayılan InstrumentationKey Applicationınsights.xml kullanılır. Bu sıra toomanage yardımcı olan farklı ortamlar için farklı InstrumentationKeys dinamik olarak.

### <a name="alternative-ways-tooset-hello-instrumentation-key"></a>Alternatif yolu tooset hello izleme anahtarı
Application Insights SDK'sı hello anahtarı bu sırayla arar:

1. Sistem özelliği: -DAPPLICATION_INSIGHTS_IKEY=your_ikey
2. Ortam değişkeni: APPLICATION_INSIGHTS_IKEY
3. Yapılandırma dosyası: ApplicationInsights.xml

Ayrıca [kod içinde ayarlayabilirsiniz](app-insights-api-custom-events-metrics.md#ikey):

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a>4. HTTP filtresi ekleme
Merhaba son yapılandırma adımı, her web isteğini hello HTTP isteği bileşeni toolog sağlar. (Yalnızca hello tam API istiyorsanız gerekmez.)

Bulup, proje ve uygulama filtrelerinizin yapılandırıldığı koddan hello web uygulaması düğümü altında birleştirme hello hello web.xml dosyasını açın.

tooget hello en doğru sonuçlar, hello filtre önce tüm diğer filtrelerle eşlenmesi gerekir.

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a>Spring Web MVC 3.1 veya sonraki sürümleri kullanıyorsanız
Bu öğeleri Düzenle *-servlet.xml tooinclude hello Application Insights paketi:

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a>Struts 2 kullanıyorsanız
Bu öğe toohello Struts yapılandırma dosyasına (genellikle adlandırılmış struts.xml veya struts default.xml) ekleyin:

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

(Varsayılan yığında tanımlı dinleyiciler varsa hello dinleyiciyi yalnızca toothat yığın eklenebilir.)

## <a name="5-run-your-application"></a>5. Uygulamanızı çalıştırma
Geliştirme makinenizde hata ayıklama modunda çalıştırın ya da tooyour server yayımlama.

## <a name="6-view-your-telemetry-in-application-insights"></a>6. Application Insights'da telemetrinizi görüntüleme
Tooyour Application Insights kaynağını dönmek [Microsoft Azure portal](https://portal.azure.com).

HTTP istekleri verileri hello genel bakış dikey penceresinde görüntülenir. (Orada değilse, birkaç saniye bekleyip Yenile’ye tıklayın.)

![örnek veri](./media/app-insights-java-get-started/5-results.png)

[Ölçümler hakkında daha fazla bilgi edinin.][metrics]

Daha ayrıntılı herhangi grafik toosee geçişli tıklatma ölçümleri birleştirilir.

![](./media/app-insights-java-get-started/6-barchart.png)

> Application Insights varsayar MVC uygulamaları için HTTP isteklerini hello biçimi: `VERB controller/action`. Örneğin, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` ve `GET Home/Product/sdf96vws`; `GET Home/Product` içinde gruplandırılır. Bu gruplandırma, istek sayısı veya isteklerin yürütülme süresi gibi anlamlı istek toplamalarını etkinleştirir.
>
>

### <a name="instance-data"></a>Örnek veriler
Belirli bir istek geçişli tıklatma toosee tek tek örneklerini yazın.

Application Insights’ta iki tür veri görüntülenir: ortalama, sayım ve toplam olarak depolanan birleşik veriler; HTTP isteklerinin tek tek raporu, özel durumlar, sayfa görünümleri veya özel olaylar olarak görüntülenen örnek veriler.

İstek Hello özellikleri görüntülendiğinde, istekler ve özel durumlar gibi ilişkili hello telemetri olayları görebilirsiniz.

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a>Analiz: Güçlü sorgu dili
Daha fazla veri birleştirdiğinizde hem tooaggregate veri ve toofind ayrı ayrı örnekleri sorguları çalıştırabilirsiniz.  [Analiz](app-insights-analytics.md) hem performans, hem de kullanım için olmasının yanı sıra tanılama için de güçlü bir araçtır.

![Analizi örneği](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-hello-server"></a>7. Uygulamanızı hello sunucusuna yükleyin
Artık uygulama toohello sunucunuza yayımlayın, kullanmak ve hello portalda hello telemetri izleyin, kullanıcıların izin verir.

* Güvenlik duvarınızın, uygulama toosend telemetri toothese bağlantı noktaları verdiğinden emin olun:

  * dc.services.visualstudio.com:443
  * f5.services.visualstudio.com:443

* Giden trafiğin güvenlik duvarından geçirilmesi gerekiyorsa, `http.proxyHost` ve `http.proxyPort` sistem özelliklerini tanımlayın.

* Windows sunucularda yüklenecekler:

  * [Microsoft Visual C++ Yeniden Dağıtılabilir](http://www.microsoft.com/download/details.aspx?id=40784)

    (Bu bileşen, performans sayaçlarını etkinleştirir.)


## <a name="exceptions-and-request-failures"></a>Özel durumlar ve istek hataları
İşlenmeyen özel durumlar otomatik olarak toplanır:

![Ayarlar, Hatalar’ı açın](./media/app-insights-java-get-started/21-exceptions.png)

diğer özel durumlar toocollect verileri, iki seçeneğiniz vardır:

* [INSERT çağırır tootrackException() kodunuzda][apiexceptions].
* [Sunucunuza Hello Java Agent Yükleme](app-insights-java-agent.md). Toowatch istediğiniz hello yöntemleri belirtin.

## <a name="monitor-method-calls-and-external-dependencies"></a>Yöntem çağrılarını ve dış bağımlılıkları izleme
[Merhaba Java Agent Yükleme](app-insights-java-agent.md) toolog belirtilen dahili yöntemleri ve zamanlama verileriyle JDBC yapılan çağrıları.

## <a name="performance-counters"></a>Performans sayaçları
Açık **ayarları**, **sunucuları**, toosee bir dizi performans sayacı.

![](./media/app-insights-java-get-started/11-perf-counters.png)

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

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a>Unix Performans sayaçları
* [Merhaba Application Insights eklentisiyle collectd yükleyin](app-insights-java-collectd.md) tooget çok çeşitli sistem ve ağ verileri.

## <a name="get-user-and-session-data"></a>Kullanıcı ve oturum verilerini alma
Tamam, web sunucunuzdan telemetri gönderiyorsunuz. Şimdi tooget Merhaba, uygulamanızın 360 derecelik tam görünümünü daha izleme ekleyebilirsiniz:

* [Telemetri tooyour web sayfaları eklemek] [ usage] toomonitor sayfa görünümlerini ve kullanıcı ölçümlerini.
* [Web testleri oluşturma] [ availability] toomake uygulamanızın canlı ve duyarlı kaldığından emin.

## <a name="capture-log-traces"></a>Günlük izlemelerini yakalama
Log4J, Logback veya başka günlük altyapılarına günlüklerinden inin ve Application Insights tooslice kullanın. Merhaba günlükleri HTTP istekleri ve başka telemetriyle ilişkilendirebilirsiniz. [Nasıl olduğunu öğrenin][javalogs].

## <a name="send-your-own-telemetry"></a>Kendi telemetrinizi gönderme
Merhaba SDK yüklediniz, kendi telemetrinizi hello API toosend kullanabilirsiniz.

* [Özel olayları ve ölçümleri izleme] [ api] hangi kullanıcıların uygulamanızla yaptıkları toolearn.
* [Olayları ve günlükleri arayın] [ diagnostic] toohelp sorunları tanılayın.

## <a name="availability-web-tests"></a>Kullanılabilirlik web testleri
Application Insights olan yukarı düzenli aralıklarla toocheck ve düzgün yanıt Web sitenizi test edebilirsiniz. [Yukarı tooset][availability], Web testleri'ı tıklatın.

![Web testleri’ne ve ardından Web testi ekle’ye tıklayın](./media/app-insights-java-get-started/31-config-web-test.png)

Yanıt süreleri grafiklerine ek olarak, siteniz devre dışı kalırsa e-posta bildirimleri de alacaksınız.

![Web testi örneği](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

[Kullanılabilirlik web testleri hakkında daha fazla bilgi edinin.][availability]

## <a name="questions-problems"></a>Sorularınız mı var? Sorunlarınız mı var?
[Java Sorun Giderme](app-insights-java-troubleshoot.md)

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Sonraki adımlar
* [Bağımlılık çağrılarını izleme](app-insights-java-agent.md)
* [Unix Performans sayaçlarını izleme](app-insights-java-collectd.md)
* Ekleme [tooyour web sayfalarını izleme](app-insights-javascript.md) toomonitor sayfa yükleme süresi, AJAX çağrıları, tarayıcı özel durumları.
* Yazma [özel telemetri](app-insights-api-custom-events-metrics.md) tootrack kullanım hello tarayıcıda veya hello sunucusu.
* Oluşturma [panolar](app-insights-dashboards.md) sisteminizi izleme toobring birlikte hello anahtar grafikleri.
* Uygulamanızdan telemetri üzerinde güçlü sorgular yapmak için [Analytics](app-insights-analytics.md)'i kullanın
* Daha fazla bilgi için bkz. [Java geliştiricileri için Azure](/java/azure).

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
