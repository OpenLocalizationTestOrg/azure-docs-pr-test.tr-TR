---
title: Java web projesinde Application Insights aaaTroubleshoot
description: "Sorun giderme kılavuzu - Application Insights ile canlı Java uygulamalarını izleme."
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: c274c01b1992971fae194c3e510512ca06ab76b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a>Java için Application Insights Sorun Giderme, Soru ve Yanıt
Sorular veya sorunlar [Java'da Azure Application Insights][java]? Burada, bazı ipuçları verilmektedir.

## <a name="build-errors"></a>Derleme hataları
**Eclipse'te, ekleme hello olduğunda Application Insights SDK Maven veya Gradle, aracılığıyla derleme veya sağlama toplamı doğrulama hataları alıyorum.**

* Varsa hello bağımlılık <version> öğesi bir desen ile joker karakterler kullanarak (örneğin (Maven) `<version>[1.0,)</version>` veya (Gradle) `version:'1.0.+'`), belirli bir sürümü gibi yerine belirtmeyi deneyin `1.0.2`. Merhaba bkz [sürüm notları](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) hello son sürüm için.

## <a name="no-data"></a>Veri yok
**Application Insights başarıyla eklendi ve Uygulamam çalıştı, ancak hiç veri hello portalında gördüğünüze göre.**

* Bir dakika bekleyip Yenile'ye tıklayın. Merhaba grafikler kendilerini düzenli olarak yeniler, ancak aynı zamanda el ile yenileyebilirsiniz. Merhaba yenileme aralığı hello grafiğin zaman aralığı hello bağlıdır.
* Merhaba Applicationınsights.xml dosyasını (projenizin kaynaklar klasörüne hello) tanımlanan bir izleme anahtarı olup olmadığını denetleyin
* Olduğunu doğrulayın hiçbir `<DisableTelemetry>true</DisableTelemetry>` hello xml dosyasında düğümü.
* Güvenlik Duvarı'nda tooopen TCP bağlantı noktaları 80 ve 443 giden trafiği toodc.services.visualstudio.com için olabilir. Merhaba bkz [güvenlik duvarı özel durumlarını tam listesi](app-insights-ip-addresses.md)
* Merhaba Microsoft Azure Panosu başlatmak, hello hizmet durumu haritası bakın. Bazı uyarı göstergeleri varsa, bunlar tooOK döndürmüş kapatın ve, Application Insights uygulama dikey penceresini yeniden açın kadar bekleyin.
* Ekleyerek toohello IDE konsol penceresinde, günlük özelliğini açın bir `<SDKLogger />` öğesi düğümünde hello kök hello Applicationınsights.xml dosyasını (projenizin kaynaklar klasörüne hello) ve [Hata] başında girişlerini denetleyin.
* Bu hello Applicationınsights.xml dosyasını başarıyla hello Java SDK'sı tarafından bir "yapılandırma dosyası başarıyla bulundu" deyimi için hello konsolun çıktı iletileri bakarak yüklendi doğru emin olun.
* Merhaba yapılandırma dosyası bulunamazsa, burada hello yapılandırma dosyası için Aranmakta olan hello çıktı iletileri toosee denetleyin ve Applicationınsights.XML arama konumların birinde bulunan bu hello emin olun. Altın kural, hello uygulama Öngörüler SDK Jar'lar hello yapılandırma dosyası yerleştirebilirsiniz. Örneğin: Tomcat'te bu WEB-INF/lib klasörüne hello anlamına gelir.

#### <a name="i-used-toosee-data-but-it-has-stopped"></a>Toosee veri kullanılır, ancak bunu durduruldu
* Merhaba denetleyin [durum blog](http://blogs.msdn.com/b/applicationinsights-status/).
* Veri noktalarının aylık kota ulaşıp? Ayarları/kota ve fiyatlandırma toofind kullanıma açın. Bu durumda, planınızı yükseltmek veya ek kapasite için ödeme yaparsınız. Merhaba bkz [düzeni fiyatlandırma](https://azure.microsoft.com/pricing/details/application-insights/).

#### <a name="i-dont-see-all-hello-data-im-expecting"></a>Tüm hello veri bekleniyor görmüyorum
* Açık hello kotalar ve fiyatlandırma dikey ve onay olup [örnekleme](app-insights-sampling.md) içinde bir işlemdir. (% 100 iletim örnekleme işleminde değil anlamına gelir.) Merhaba Application Insights hizmeti kümesi tooaccept uygulamanızdan ulaşan hello telemetri yalnızca bir kısmı olabilir. Bu telemetrinin aylık kota içinde tutmanıza yardımcı olur. 

## <a name="no-usage-data"></a>Kullanım verisi yok
**İstek ve yanıt süreleri, ancak hiçbir sayfa görünümü, tarayıcı hakkındaki verileri veya kullanıcı verileri görüyorum.**

Merhaba sunucudan uygulama toosend telemetrinize başarıyla ayarlandı. Sonraki adımınız çok şimdi[web sayfalarını toosend telemetrinize hello web tarayıcısından ayarlamak][usage].

Alternatif olarak, istemci bir uygulamada ise bir [telefon veya başka bir aygıt][platforms], buradan telemetri gönderebilir. 

Kullanım hello aynı araçları anahtar tooset hem istemci hem de sunucu telemetri ayarlama. Merhaba veri, aynı Application Insights kaynağı hello ve istemci ve sunucu mümkün toocorrelate olayları olacak görünür.


## <a name="disabling-telemetry"></a>Telemetri devre dışı bırakma
**Telemetri koleksiyonunu nasıl devre dışı bırakabilirim?**

Kod:

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

**Veya** 

Applicationınsights.XML (klasöründe hello kaynakları projenize) güncelleştirin. Merhaba aşağıdaki hello kök düğümü altına ekleyin:

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

Merhaba değeri değiştirdiğinizde hello XML yöntemi kullanarak, toorestart hello uygulamaya sahip.

## <a name="changing-hello-target"></a>Merhaba hedef değiştirme
**Proje için verileri gönderir hangi Azure kaynak nasıl değiştirebilir miyim?**

* [Hello hello yeni kaynağın izleme anahtarını alır.][java]
* Eclipse için hello Azure Araç Seti kullanarak Application Insights tooyour proje eklediyseniz, web projenize sağ tıklayın, seçin **Azure**, **yapılandırma Application Insights**ve başlangıç anahtarı değiştirin.
* Aksi takdirde hello anahtar projeniz hello kaynaklar klasörüne Applicationınsights.XML güncelleştirin.

## <a name="debug-data-from-hello-sdk"></a>Merhaba SDK verilerden hata ayıklama

**SDK yapılması hangi hello nasıl bulabilirim?**

tooget hello API, neler olduğunu hakkında daha fazla bilgi eklemek `<SDKLogger/>` hello hello Applicationınsights.XML yapılandırma dosyasının kök düğümü altında.

Merhaba Günlükçü toooutput tooa dosya talimatını:

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

Merhaba dosyaları altında bulunabilir `%temp%\javasdklogs` veya `java.io.tmpdir` Tomcat sunucusunu durumunda.


## <a name="hello-azure-start-screen"></a>Hello Azure başlangıç ekranı
**Konumundaki arayan [Azure portal hello](https://portal.azure.com). Merhaba harita bir şey Uygulamam hakkında bilgi ver mu?**

Hayır, hello world hello Azure sunucularının durumunu gösterir.

*Hello Azure başlangıç Panosu (giriş ekranı) nasıl veri Uygulamam hakkında bulabilirim?*

Varsayılmıştır [Application Insights için uygulamanızı ayarlayın][java], Gözat'ı tıklatın, Application Insights'ı seçin ve uygulamanız için oluşturulan hello Uygulama kaynağı seçin. tooget var. daha hızlı gelecekte, uygulama toohello başlangıç panonuzu sabitleyebilirsiniz.

## <a name="intranet-servers"></a>İntranet sunucuları
**İntranetimde bulunan bir sunucu izleyebilir mi?**

Evet, sunucunuzun telemetri toohello Application Insights portalı üzerinden göndermek için sağlanan genel internet hello. 

Güvenlik Duvarı'nda tooopen TCP bağlantı noktaları 80 ve 443 giden trafiği toodc.services.visualstudio.com ve f5.services.visualstudio.com olabilir.

## <a name="data-retention"></a>Veri saklama
**Ne kadar veri hello Portalı'nda tutulur? Güvenli mi?**

Bkz: [veri saklama ve gizlilik][data].

## <a name="next-steps"></a>Sonraki adımlar
**Java sunucu Uygulamam için Application Insights'ı ayarlarım. Başka ne yapabilirim?**

* [Web sayfalarınıza kullanılabilirliğini izleyin][availability]
* [Web sayfası kullanımını izleme][usage]
* [Cihaz uygulamalarınızdaki sorunlarını tanılamak ve kullanımını izleme][platforms]
* [Kod tootrack kullanımı, uygulamanızın yazma][track]
* [Tanılama günlüklerini yakalama][javalogs]

## <a name="get-help"></a>Yardım alın
* [Stack Overflow](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

