---
title: "aaaMonitor bir Web uygulaması | Microsoft Docs"
description: "Bilgi nasıl tooset Web uygulamanızdan izleme ayarlama"
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: c2f5e9842c732a804f1caee5d67e53dad24e190a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-app-service"></a>Uygulama Hizmeti izleme
Bu öğreticide, uygulamanızı izleme ve bunlar ortaya çıktığında hello yerleşik platformu araçları toosolve sorunları kullanarak aracılığıyla açıklanmaktadır.

Bu belge her bir bölümünü belirli bir özelliği gider. Merhaba özellikleri birlikte kullanarak şunları yapmanızı sağlar:
- Uygulamanızı bir sorunu tanımlama.
- Merhaba sorun kodu veya hello platformunuz tarafından ne zaman kaynaklanır belirleme.
- Merhaba kaynak kodunuzda hello sorununun daraltın.
- Hata ayıklama ve hello sorunu düzeltme.

## <a name="before-you-begin"></a>Başlamadan önce
- Bir Web uygulaması toomonitor gerekir ve hello izleyin özetlenen adımları.
    - Hello açıklanan başlangıç adımları izleyerek bir uygulama oluşturabilir [Azure SQL veritabanı ile bir ASP.NET uygulaması oluşturma](app-service-web-tutorial-dotnet-sqldatabase.md) Öğreticisi.

- Tootry istiyorsanız verilen **uzaktan hata ayıklama** uygulamanızın veya Visual Studio gerekir.
    - Visual Studio yüklü 2017 zaten sahip değilseniz, indirin ve hello ücretsiz kullanmak [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).
    - Etkinleştirdiğinizden emin olun **Azure geliştirme** hello Visual Studio Kurulumu sırasında.

## <a name="metrics"></a>1. adım - metrikleri görüntüleyin
**Ölçümleri** yararlı toounderstand şunlardır:
- Uygulama durumu
- Uygulama performansı
- Kaynak tüketimi

Bir uygulama sorunu araştırmaya ölçümleri gözden geçirmek iyi toostart olur. Azure portal sahiptir, uygulama kullanımının hello ölçümleri incelemek hızlı şekilde toovisually **Azure İzleyici**.

Ölçümleri, uygulamanız için birkaç anahtar toplamalar arasında bir geçmiş görünümünü sağlar. App service içinde barındırılan herhangi bir uygulama için başlangıç Web uygulaması ve hello uygulama hizmeti planı izlemeniz gerekir.

> [!NOTE]
> Bir uygulama hizmeti planı, uygulamalarınızı kullanılan fiziksel kaynakları toohost hello koleksiyonunu temsil eder. Tüm uygulamaları tooan tanımladığı birden fazla uygulama barındırdığında toosave maliyet izin vererek uygulama hizmeti planı paylaşımı hello kaynaklara atanan.
>
> App Service planları şunları tanımlar:
> * Bölge: Kuzey Avrupa, Doğu ABD, Güneydoğu Asya, vb.
> * Örnek boyutu: Küçük, Orta, büyük, vb.
> * Ölçek sayısı: bir, iki veya üç örnekleri, vb.
> * SKU: Ücretsiz, paylaşılan, temel, standart, Premium, vs.

Web uygulamanızın Git toohello tooreview ölçümleri **genel bakış** dikey penceresinde hello uygulamasının toomonitor istiyor. Buradan, uygulamanızın ölçümleri için bir grafik görüntüleyebilirsiniz bir **izleme kutucuğu**. Merhaba döşeme tooedit'ı tıklatın, hangi ölçümleri tooview yapılandırmak ve zaman aralığı toodisplay hello.

Varsayılan hello kaynak dikey tarafından hello uygulama istekleri için bir görünüm ve hataları hello son saat için sağlar.
![İzleyici uygulama](media/app-service-web-tutorial-monitoring/app-service-monitor.png)

Merhaba örnekte de görüldüğü gibi birçok oluşturma uygulamanın sahibiz **HTTP sunucu hataları**. Merhaba hacmi yüksek hatalar, bu uygulama tooinvestigate ihtiyacımız hello ilk göstergesidir.

> [!TIP]
> Azure İzleyici hakkında daha fazla ile Merhaba bağlantılar aşağıdaki bilgi:
> - [Azure İzleyicisi ile çalışmaya başlama](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Azure ölçümleri](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [Azure İzleyicisi ile desteklenen ölçümleri](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [Azure panoları](..\azure-portal\azure-portal-dashboards.md)

## <a name="alerts"></a>2. adım - uyarılarını yapılandırma
**Uyarıları** uygulamanız için belirli koşullar üzerinde yapılandırılmış tootrigger olabilir.

İçinde [adım 1 - görünüm ölçümleri](#metrics), Merhaba uygulaması çok sayıda hataları vardı gördük.

Bir uyarı yapılandırmak sağlar tooautomatically hatası meydana geldiğinde bildirim. Bu durumda, biz hello uyarı toosend istediğiniz ve belirli bir eşiğin üstünde hello HTTP 50 X hatalarının sayısı gider her zaman e-posta.

bir uyarı, toocreate gidin çok**izleme** > **uyarıları** tıklatıp **[+] uyarı Ekle**.

![Uyarılar](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

Değerleri hello uyarı yapılandırması sağlar:
- **Kaynak:** site toomonitor hello uyarı ile Merhaba.
- **Ad:** bu durumda, uyarı için bir ad: *yüksek HTTP 50 X*.
- **Açıklama:** bu uyarı en arıyor düz metin açıklaması.
- **Uyarı:** ölçümleri veya olayları uyarıları görünür, bu örnek için ölçümlere arıyoruz.
- **Ölçüm:** bu durumda hangi ölçüm toomonitor: *HTTP sunucu hataları*.
- **Koşul:** tooalert, bu durumda seçtiğinizde hello *büyük* seçeneği.
- **Eşiği:** değeri toolook için bu durumda nedir: *400*.
- **Süresi:** uyarıları hello ortalama ölçüm değeri çalışır. Daha küçük süreler daha hassas uyarılar verecek. Bu durumda biz Baktığınız *5 dakika*.
- **E-posta sahipleri ve katkıda bulunanlar:** bu durumda: *etkin*.

Merhaba uyarı bir e-posta oluşturulması tamamlandığına göre hello uygulama gider hello yapılandırılan eşiğin üstünde her zaman gönderilir. Etkin uyarılar hello Azure portal gözden geçirilmesi.

![Tetiklenen uyarıları](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> Azure Uyarıları hakkında daha fazla ile Merhaba bağlantılar aşağıdaki bilgi:
> - [Microsoft Azure içindeki uyarıları nedir](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [Ölçümleri eylem](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Ölçüm uyarı oluşturma](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <a name="companion"></a>3. adım - uygulama hizmeti Yardımcısı
**Uygulama hizmeti Yardımcısı** uygun şekilde toomonitor uygulamanız mobil Cihazınızı (iOS veya Android) yerel bir deneyim sunar.

Uygulama hizmeti Yardımcısı'nı kullanın:
- Uygulama ölçümleri gözden geçirin
- Gözden geçirme ve act uygulama uyarıları ve öneriler
- Temel sorun giderme (Gözat, Başlat, Durdur, yeniden başlatma hello uygulama) gerçekleştirir
- Kritik olaylar için anında iletme bildirimleri alın.

![Uygulama hizmeti Yardımcısı](media/app-service-web-tutorial-monitoring/app-service-companion.png)

[![Uygulama hizmeti yardımcı uygulama mağazası](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![uygulama hizmeti Yahoo! Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

Uygulama hizmeti Yardımcısı hello yükleyebilirsiniz [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) veya [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

## <a name="diagnose"></a>4. adım - tanılamak ve sorunları çözme
**Sorunları tanılamak ve** form platform sorunları uygulama sorunlarını ayrı yardımcı olur. Web uygulaması geri toohealthy olası risk azaltmalarını tooget de önerebilir.

![Tanılama ve sorunları](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

Merhaba örnek form önceki adımlara devam etmeden, biz Merhaba uygulaması sorunları tanımlanmasından sahip olduğunu görebilirsiniz. Buna karşılık, hello platform kullanılabilirlik % 100'den taşındı değil.

Ne zaman hello uygulama sorunu yaşıyor ve hello platform kalır yukarı biz ile uygulama sorununu giderme NET bir belirti olur.

## <a name="logging"></a>Adım 5 - günlük kaydı
Biz hello hataları tooan uygulama sorunu belirlemelerine daraltıldığı, hello uygulama ve sunucu günlüklerini tooget daha fazla bilgi bakabilirsiniz.

Günlük toocollect hem verir **uygulama tanılama** ve **Web sunucusu tanılama** Web uygulamanız için günlükleri.

### <a name="application-diagnostics"></a>Uygulama tanılama
Uygulama tanılama zamanında hello uygulama tarafından üretilen, toocapture izlemeleri sağlar.

İzleme tooyour ekleme uygulama büyük ölçüde özelliği toodebug ve sabitleme noktası sorunları artırır.

ASP.NET, uygulama izlemelerini kullanarak oturum açabilir [System.Diagnostics.Trace sınıfı](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) hello günlük altyapısı tarafından yakalanan toogenerate olaylar. Daha kolay filtreleme hello izleme hello önemini de belirtebilirsiniz.

```csharp
public ActionResult Delete(Guid? id)
{
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id);
    if (id == null)
    {
        System.Diagnostics.Trace.TraceError("/Todos/Delete/ failed, ID is null");
        return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
    }
    Todo todo = db.Todoes.Find(id);
    if (todo == null)
    {
        System.Diagnostics.Trace.TraceWarning("/Todos/Delete/ failed, ID: " + id + " could not be found");
        return HttpNotFound();
    }
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id + "completed successfully");
    return View(todo);
}
```
tooenable uygulama günlüğü Git çok**izleme** > **tanılama günlüklerini** ve uygulama hello değiştirme düğmelerini kullanarak günlük kaydını etkinleştirin.

![İzleyici uygulama](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

Uygulama günlüklerini saklı tooyour Web uygulamanızın dosya sistemi olabilir veya tooblob depolama gönderilir. Üretim senaryoları için önerilen toouse blob depolama birimi değil.

> [!IMPORTANT]
> Günlüğü etkinleştirme uygulama performans ve kaynak kullanımı üzerinde bir etkisi yoktur. Üretim senaryoları için hata günlüklerini önerilir. Yalnızca sorunları araştırırken daha ayrıntılı günlük kaydını etkinleştirin.

 ### <a name="web-server-diagnostics"></a>Web sunucu tanıları
Uygulamanızı değil izlenmiş olsa bile web sunucu günlükleri üretilir. Uygulama hizmeti sunucusu günlüklerini üç farklı türde toplayabilirsiniz:

- **Web sunucusu günlüğü**
    - Hello kullanarak HTTP işlemler hakkında bilgi [W3C Genişletilmiş günlük dosyası biçimi](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).
    - İşlenen istek hello sayısı veya belirli bir IP adresinden kaç isteklerdir gibi genel site ölçümleri belirlerken yararlıdır.
- **Ayrıntılı hata günlüğü**
    - (Durum kodu 400 veya daha büyük) hatası olduğunu gösteren HTTP durum kodları için ayrıntılı hata bilgileri.
    - [Ayrıntılı hata günlüğü hakkında daha fazla bilgi edinin](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- **Başarısız istek izleme**
    - Merhaba IIS bileşenlerini izleme de dahil olmak üzere, başarısız istekler hakkında ayrıntılı bilgi, her bileşenin geçen tooprocess hello istek ve hello süre kullanılır.
    - Başarısız istek günlükleri tooisolate belirli bir HTTP hata neden olan çalışırken yararlıdır.
    - [Başarısız istek izleme hakkında daha fazla bilgi edinin](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

tooenable Server günlüğü:
- çok Git**izleme** > **tanılama günlükleri**.
- Web sunucusu tanılama hello değiştirme düğmelerini kullanarak farklı türlerde Hello etkinleştirin.

![İzleyici uygulama](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> Günlüğü etkinleştirme uygulama performans ve kaynak kullanımı üzerinde bir etkisi yoktur. Üretim senaryoları için hata günlüklerini önerilir, yalnızca etkinleştirmek sorunları incelemeye günlüğe kaydetme daha ayrıntılı.

### <a name="accessing-logs"></a>Günlükleri erişme
BLOB storage'da depolanan günlükleri, Azure Storage Gezgini kullanılarak erişilir. Merhaba Web uygulamanızın dosya sistemi içinde depolanan günlükleri yolları aşağıdaki hello altında FTP aracılığıyla erişilen:

- **Uygulama günlüklerini** - `%HOME%/LogFiles/Application/`.
    - Bu klasör uygulama günlüğü tarafından üretilen bilgileri içeren bir veya daha fazla metin dosyalarını içerir.
- **Başarısız istek izlemelerin** - `%HOME%/LogFiles/W3SVC#########/`.
    - Bu klasör bir XSL dosyası ve bir veya daha fazla XML dosyalarını içerir.
- **Ayrıntılı Hata günlüklerini** - `%HOME%/LogFiles/DetailedErrors/`.
    - Bu klasör, uygulamanız tarafından oluşturulan HTTP hataları hakkında kapsamlı bilgi içeren bir veya daha fazla .htm dosyaları içerir.
- **Web sunucu günlükleri** - `%HOME%/LogFiles/http/RawLogs`.
    - Bu klasör hello W3C Genişletilmiş günlük dosyası biçimi kullanılarak biçimlendirilmiş bir veya daha fazla metin dosyalarını içerir.

## <a name="streaming"></a>Adım 6 - akış günlük
Çok karşılaştırıldığında zaman kazandırır bu yana uygulama hata ayıklama sırasında akış günlükleri uygun[hello günlüklerine erişme](#Accessing-Logs) FTP aracılığıyla.

Uygulama hizmeti akış **uygulama günlüklerini** ve **Web sunucu günlükleri** bunlar oluşturulduğunda.

> [!TIP]
> Toostream günlükleri, denemeden önce hello açıklandığı gibi toplama günlükleri etkinleştirdiğinizden emin olun [günlüğü](#logging) bölümü.

toostream günlükleri, Git çok**izleme**> **günlük akışı**. Seçin **uygulama günlüklerini** veya **Web sunucu günlükleri** hangi bilgilere bağlı olarak, aradığınız. Buradan, ayrıca Duraklat, yeniden başlatın ve hello arabellek temizleyin.

![Akış günlükleri](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> Merhaba uygulamasını trafiği olduğunda günlükleri yalnızca oluşturulan, ayrıca daha fazla olayları veya bilgi günlükleri tooget hello ayrıntı düzeyini artırabilirsiniz.

## <a name="remote"></a>7. adım - uzaktan hata ayıklama
Merhaba uygulamaları sorunları PIN işaret hello kaynağına sahip olduktan sonra kullanın **uzaktan hata ayıklama** hello kodlarda toowalk.

Uzaktan hata ayıklama sağlar, hata ayıklayıcı tooyour Web uygulaması ekleme hello bulutta çalışan. Kesme noktalarını ayarlayın, bellek doğrudan işlemek, kod üzerinden adım ve bile yerel olarak çalışan bir uygulama için gibi hello kod yolu değiştirin.

Merhaba bulutta çalışan tooattach hello hata ayıklayıcı tooyour uygulama:

- Visual Studio 2017, hello uygulama için açık hello çözümü kullanarak toodebug istediğiniz
- Yerel geliştirme için gibi bazı Fren noktaları ayarlayın.
- Açık **cloud explorer** (CTRL + /, ctrl + x).
- Azure kimlik bilgilerinizle oturum açın, gerektiği gibi oturum açın.
- Toodebug istediğiniz Bul hello uygulama
- Seçin **Attach hata ayıklayıcı** form hello **Eylemler** bölmesi.

![Uzaktan hata ayıklama](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

Visual Studio uzaktan hata ayıklama için uygulamanızı yapılandırır ve tooyour uygulama gider bir tarayıcı penceresi açar. Uygulama tootrigger kesme noktalarına göz ve aracılığıyla hello koda adım.

> [!WARNING]
> Hata ayıklama modunda üretimde çalışan önerilmez. Üretim uygulamanız toomultiple sunucu örnekleri ölçeklenmez ise, yanıt veren tooother istekleri hello web sunucusundan engel hata ayıklama. Üretim ilgili sorunları gidermek için en iyi çok kaynaktır[günlüğe kaydetmeyi yapılandırmak](#logging) ve [Application Insights](#insights).



## <a name="explorer"></a>Adım 8 - işlem Gezgini'ni
Uygulamanız birden fazla, toomore çıkışı ölçeklendirilir zaman **işlem Gezgini'ni** örneği belirli sorunları belirlemenize yardımcı olabilir.

Kullanım **işlem Gezgini'ni** için:

- Tüm hello işlemleri farklı uygulama hizmeti planınızı örneklerinde sıralar.
- Detaya ve hello işleyicileri ve modülleri her işlemle ilişkili görüntüleyin.
- Merhaba görünüm CPU, çalışma kümesine ve iş parçacığı sayısını işlem düzeyi toohelp kaçak işlemleri tanımlayın
- Açık dosya işlemesi bulun ve hatta belirli işlem örneği sonlandır.

İşlem Gezgini'ni altında bulunabilir **izleme** > **işlem Gezgini'ni**.

![İşlem Gezgini](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <a name="insights"></a>Adım 9 - Application Insights
**Application Insights** uygulamanız için uygulama profili oluşturma ve Gelişmiş izleme özelliklerini sağlar.

Özel durumlar ve Web uygulamanızda performans sorunlarını tanılamak ve Application Insights toodetect kullanın.

Web uygulamanız için Application Insights etkinleştirebilirsiniz **izleme** > **Application Insights**

> [!NOTE]
> Application Insights tooinstall hello Application Insights site uzantısı toostart veri toplamayı isteyebilir. Merhaba site uzantısı yükleme uygulama yeniden başlatma neden olur.

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

Application Insights sahip zengin bir özellik kümesi, toolearn daha izleyin hello içerdiği hello bağlantılar [sonraki adımlar](#next) bölümü.

## <a name="next"></a> Sonraki adımlar

 - [Application Insights nedir](..\application-insights\app-insights-overview.md)
 - [Application Insights ile Azure web uygulaması performans izleme](..\application-insights\app-insights-azure-web-apps.md)
 - [İzleyici kullanılabilirliği ve yanıt hızını Application Insights ile herhangi bir web sitesi](..\application-insights\app-insights-monitor-web-app-availability.md)
