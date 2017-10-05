---
title: "Bir Web uygulaması izleme | Microsoft Docs"
description: "Web uygulamanızdan izleme ayarlama öğrenin"
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: 29df824062d00e01b786533033097948c008588f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-app-service"></a>Uygulama Hizmeti izleme
Bu öğreticide, uygulamanızı izleme ve ortaya çıkan sorunları çözmek için yerleşik platform araçlarını kullanarak aracılığıyla açıklanmaktadır.

Bu belge her bir bölümünü belirli bir özelliği gider. Özellikleri birlikte kullanarak şunları yapmanızı sağlar:
- Uygulamanızı bir sorunu tanımlama.
- Ne zaman sorun kodunuzu platform nedeni veya belirleniyor.
- Kodunuzda sorunun kaynağını daraltın.
- Hata ayıklama ve sorun giderme.

## <a name="before-you-begin"></a>Başlamadan önce
- Açıklanan adımları izleyin ve izlemek için bir Web uygulaması gerekir.
    - Açıklanan adımları izleyerek bir uygulama oluşturabilir [Azure SQL veritabanı ile bir ASP.NET uygulaması oluşturma](app-service-web-tutorial-dotnet-sqldatabase.md) Öğreticisi.

- Denemek istiyorsanız, **uzaktan hata ayıklama** uygulamanızın veya Visual Studio gerekir.
    - Visual Studio yüklü 2017 zaten sahip değilseniz, indirin ve ücretsiz kullanmak [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).
    - Visual Studio kurulumu sırasında **Azure dağıtımını** etkinleştirdiğinizden emin olun.

## <a name="metrics"></a>1. adım - metrikleri görüntüleyin
**Ölçümleri** anlamak kullanışlıdır:
- Uygulama durumu
- Uygulama performansı
- Kaynak tüketimi

Uygulama sorununu araştırırken ölçümleri gözden geçirme başlatmak için uygun bir yerdir. Azure portal sahiptir, uygulama kullanımının ölçümleri görsel olarak incelemek için hızlı bir yolu **Azure İzleyici**.

Ölçümleri, uygulamanız için birkaç anahtar toplamalar arasında bir geçmiş görünümünü sağlar. App service içinde barındırılan herhangi bir uygulama için Web App ve uygulama hizmeti planı izlemeniz gerekir.

> [!NOTE]
> App Service planı, uygulamalarınızı barındırmak için kullanılan fiziksel kaynakları içeren koleksiyonu temsil eder. Bir App Service planına atanan tüm uygulamalar plan tarafından tanımlanan kaynakları paylaşarak birden çok uygulamayı barındırırken maliyetten tasarruf etmenize imkan sağlar.
>
> App Service planları şunları tanımlar:
> * Bölge: Kuzey Avrupa, Doğu ABD, Güneydoğu Asya, vb.
> * Örnek boyutu: Küçük, Orta, büyük, vb.
> * Ölçek sayısı: bir, iki veya üç örnekleri, vb.
> * SKU: Ücretsiz, paylaşılan, temel, standart, Premium, vs.

Web uygulamanız için ölçümleri gözden geçirmek için Git **genel bakış** izlemek istediğiniz uygulamayı dikey. Buradan, uygulamanızın ölçümleri için bir grafik görüntüleyebilirsiniz bir **izleme kutucuğu**. Düzenle ve hangi ölçümleri görüntülemek ve görüntülemek için zaman aralığı için yapılandırmak için kutucuğa tıklayın.

Varsayılan olarak kaynak dikey penceresini görüntüleme uygulama istekleri ve hataları için son saat için sağlar.
![İzleyici uygulama](media/app-service-web-tutorial-monitoring/app-service-monitor.png)

Örnekte de görüldüğü gibi birçok oluşturma uygulamanın sahibiz **HTTP sunucu hataları**. Yüksek hacimli hataların bu uygulamayı araştırmak ihtiyacımız ilk göstergesidir.

> [!TIP]
> Azure İzleyici hakkında daha fazla ile aşağıdaki bağlantılardan öğrenin:
> - [Azure İzleyicisi ile çalışmaya başlama](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Azure ölçümleri](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [Azure İzleyicisi ile desteklenen ölçümleri](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [Azure panoları](..\azure-portal\azure-portal-dashboards.md)

## <a name="alerts"></a>2. adım - uyarılarını yapılandırma
**Uyarıları** yapılandırılabilir uygulamanız için belirli koşullar tetikleyici için.

İçinde [adım 1 - görünüm ölçümleri](#metrics), uygulamanın çok sayıda hataları vardı gördük.

Hata oluştuğunda otomatik olarak bildirim almak için bir uyarı yapılandırmak olanak sağlar. Bu durumda, gönderme ve HTTP 50 X hatalarının sayısı belirli bir eşiğin üstünde gider her zaman e-posta uyarı istiyoruz.

Bir uyarı oluşturmak için gidin **izleme** > **uyarıları** tıklatıp **[+] uyarı Ekle**.

![Uyarılar](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

Uyarı yapılandırması için değerleri girin:
- **Kaynak:** uyarıyla izlemek için site.
- **Ad:** bu durumda, uyarı için bir ad: *yüksek HTTP 50 X*.
- **Açıklama:** bu uyarı en arıyor düz metin açıklaması.
- **Uyarı:** ölçümleri veya olayları uyarıları görünür, bu örnek için ölçümlere arıyoruz.
- **Ölçüm:** bu durumda, izlemek için hangi ölçüm: *HTTP sunucu hataları*.
- **Koşul:** ne zaman uyarı, bu durumda select *büyük* seçeneği.
- **Eşiği:** , bu durumda aramak için değer nedir: *400*.
- **Süresi:** uyarılar ölçüm ortalama değer üzerinde çalışır. Daha küçük süreler daha hassas uyarılar verecek. Bu durumda biz Baktığınız *5 dakika*.
- **E-posta sahipleri ve katkıda bulunanlar:** bu durumda: *etkin*.

Uyarı oluşturduğunuza göre uygulama yapılandırılan eşiğin üstünde gider her zaman bir e-posta gönderilir. Etkin uyarılar ayrıca Azure portalında incelenebilir.

![Tetiklenen uyarıları](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> Azure Uyarıları hakkında daha fazla ile aşağıdaki bağlantılardan öğrenin:
> - [Microsoft Azure içindeki uyarıları nedir](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [Ölçümleri eylem](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Ölçüm uyarı oluşturma](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <a name="companion"></a>3. adım - uygulama hizmeti Yardımcısı
**Uygulama hizmeti Yardımcısı** mobil Cihazınızı (iOS veya Android) yerel bir deneyim uygulamanızı izlemek için kullanışlı bir yol sunar.

Uygulama hizmeti Yardımcısı'nı kullanın:
- Uygulama ölçümleri gözden geçirin
- Gözden geçirme ve act uygulama uyarıları ve öneriler
- Temel sorun giderme gerçekleştirir (göz atın, başlatabilir, durdurabilir, uygulamayı yeniden başlatın)
- Kritik olaylar için anında iletme bildirimleri alın.

![Uygulama hizmeti Yardımcısı](media/app-service-web-tutorial-monitoring/app-service-companion.png)

[![Uygulama hizmeti yardımcı uygulama mağazası](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![uygulama hizmeti Yahoo! Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

Uygulama hizmeti kılavuz yükleyebilirsiniz [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) veya [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

## <a name="diagnose"></a>4. adım - tanılamak ve sorunları çözme
**Sorunları tanılamak ve** form platform sorunları uygulama sorunlarını ayrı yardımcı olur. Ayrıca, Web uygulamanıza geri sağlıklı almak için olası risk azaltmalarını de önerebilir.

![Tanılama ve sorunları](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

Örnek form önceki adımlara devam etmeden, uygulama konusunda tanımlanmasından sorun olduğunu görebiliriz. Buna karşılık, platform kullanılabilirlik % 100'den taşındı değil.

Uygulama sorun ve platform kalır yukarı içerdiğinde biz ile uygulama sorununu giderme NET bir belirti değil.

## <a name="logging"></a>Adım 5 - günlük kaydı
Biz uygulama sorununu hatalarını aşağı daraltıldığı, size daha fazla bilgi almak için uygulama ve sunucu günlüklerini bakabilirsiniz.

Günlük her ikisi de toplamanızı sağlar **uygulama tanılama** ve **Web sunucusu tanılama** Web uygulamanız için günlükleri.

### <a name="application-diagnostics"></a>Uygulama tanılama
Uygulama tanılama çalışma zamanında uygulama tarafından üretilen izlemeleri yakalamanıza olanak sağlar.

Uygulamanız için büyük ölçüde izleme ekleme hata ayıklama ve sabitleme noktası sorunları yeteneğinizi geliştirir.

ASP.NET, uygulama izlemelerini kullanarak oturum açabilir [System.Diagnostics.Trace sınıfı](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) günlük altyapısı tarafından yakalanan olaylar oluşturmak için. Önem derecesi daha kolay filtreleme için izleme de belirtebilirsiniz.

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
Uygulama günlüğü etkinleştirmek için Git **izleme** > **tanılama günlüklerini** ve uygulama değiştirme düğmelerini kullanarak günlük kaydını etkinleştirin.

![İzleyici uygulama](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

Uygulama günlükleri, Web uygulamanızın dosya sistemine depolanan veya blob depolama için gönderilir. Üretim senaryoları için blob storage kullanma önerilir.

> [!IMPORTANT]
> Günlüğü etkinleştirme uygulama performans ve kaynak kullanımı üzerinde bir etkisi yoktur. Üretim senaryoları için hata günlüklerini önerilir. Yalnızca sorunları araştırırken daha ayrıntılı günlük kaydını etkinleştirin.

 ### <a name="web-server-diagnostics"></a>Web sunucu tanıları
Uygulamanızı değil izlenmiş olsa bile web sunucu günlükleri üretilir. Uygulama hizmeti sunucusu günlüklerini üç farklı türde toplayabilirsiniz:

- **Web sunucusu günlüğü**
    - HTTP işlemlerini kullanma hakkında bilgi [W3C Genişletilmiş günlük dosyası biçimi](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).
    - Belirli bir IP adresinden işlenen isteklerin ya da kaç istek sayısı gibi genel site ölçümleri belirlerken yararlıdır.
- **Ayrıntılı hata günlüğü**
    - (Durum kodu 400 veya daha büyük) hatası olduğunu gösteren HTTP durum kodları için ayrıntılı hata bilgileri.
    - [Ayrıntılı hata günlüğü hakkında daha fazla bilgi edinin](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- **Başarısız istek izleme**
    - İstek ve her bileşenin geçen süre işlemek için kullanılan IIS bileşenlerini izleme de dahil olmak üzere, başarısız istekler hakkında ayrıntılı bilgiler.
    - Günlükleri ne yalıtmak çalışılırken bir özel HTTP hata neden olduğunda yararlı isteği başarısız oldu.
    - [Başarısız istek izleme hakkında daha fazla bilgi edinin](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

Sunucu günlük kaydını etkinleştirmek için:
- Git **izleme** > **tanılama günlükleri**.
- Web sunucusu değiştirme düğmelerini kullanarak tanılama farklı türde etkinleştirin.

![İzleyici uygulama](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> Günlüğü etkinleştirme uygulama performans ve kaynak kullanımı üzerinde bir etkisi yoktur. Üretim senaryoları için hata günlüklerini önerilir, yalnızca etkinleştirmek sorunları incelemeye günlüğe kaydetme daha ayrıntılı.

### <a name="accessing-logs"></a>Günlükleri erişme
BLOB storage'da depolanan günlükleri, Azure Storage Gezgini kullanılarak erişilir. Web uygulamanızın dosya sistemi içinde depolanan günlükleri şu yolların altında FTP aracılığıyla erişilen:

- **Uygulama günlüklerini** - `%HOME%/LogFiles/Application/`.
    - Bu klasör uygulama günlüğü tarafından üretilen bilgileri içeren bir veya daha fazla metin dosyalarını içerir.
- **Başarısız istek izlemelerin** - `%HOME%/LogFiles/W3SVC#########/`.
    - Bu klasör bir XSL dosyası ve bir veya daha fazla XML dosyalarını içerir.
- **Ayrıntılı Hata günlüklerini** - `%HOME%/LogFiles/DetailedErrors/`.
    - Bu klasör, uygulamanız tarafından oluşturulan HTTP hataları hakkında kapsamlı bilgi içeren bir veya daha fazla .htm dosyaları içerir.
- **Web sunucu günlükleri** - `%HOME%/LogFiles/http/RawLogs`.
    - Bu klasör, W3C Genişletilmiş günlük dosyası biçimi kullanılarak biçimlendirilmiş bir veya daha fazla metin dosyalarını içerir.

## <a name="streaming"></a>Adım 6 - akış günlük
Karşılaştırılan zaman kazandırır bu yana uygulama hata ayıklama sırasında akış günlükleri uygun [günlükleri erişme](#Accessing-Logs) FTP aracılığıyla.

Uygulama hizmeti akış **uygulama günlüklerini** ve **Web sunucu günlükleri** bunlar oluşturulduğunda.

> [!TIP]
> Akış günlükleri, emin olmak denemeden önce toplama günlükleri açıklandığı gibi etkinleştirdiğiniz [günlüğü](#logging) bölümü.

Akış günlükleri, Git **izleme**> **günlük akışı**. Seçin **uygulama günlüklerini** veya **Web sunucu günlükleri** hangi bilgilere bağlı olarak, aradığınız. Buradan, ayrıca Duraklat, yeniden başlatın ve arabellek temizleyin.

![Akış günlükleri](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> Uygulamasını trafiği olduğunda günlükleri yalnızca oluşturulur, daha fazla olayları veya bilgi almak için günlüklerini ayrıntı da artırabilirsiniz.

## <a name="remote"></a>7. adım - uzaktan hata ayıklama
PIN-uygulamaları sorunları kaynağı işaret sonra kullanarak **uzaktan hata ayıklama** kod yürütmek için.

Uzaktan hata ayıklama sağlar, bir hata ayıklayıcısı bulutta çalışan Web uygulamanıza ekleyebilir. Kesme noktalarını ayarlayın, bellek doğrudan yönetmek, aracılığıyla koda adım ve yerel olarak çalışan bir uygulama için gibi bile kod yolu değiştirin.

Hata ayıklayıcı bulutta çalışan uygulamanıza eklemek için:

- Visual Studio 2017'nı kullanarak hata ayıklama istediğiniz uygulama için çözüm açın
- Yerel geliştirme için gibi bazı Fren noktaları ayarlayın.
- Açık **cloud explorer** (CTRL + /, ctrl + x).
- Azure kimlik bilgilerinizle oturum açın, gerektiği gibi oturum açın.
- Hata ayıklamak istediğiniz uygulamayı bulun
- Seçin **Attach hata ayıklayıcı** form **Eylemler** bölmesi.

![Uzaktan hata ayıklama](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

Visual Studio uzaktan hata ayıklama için uygulamanızı yapılandırır ve uygulamanıza gider bir tarayıcı penceresi açar. Kesme noktaları ve kod aracılığıyla adım tetiklemek için uygulamanızın göz atın.

> [!WARNING]
> Hata ayıklama modunda üretimde çalışan önerilmez. Üretim uygulamanız çıkışı için birden fazla sunucu örneğinin ölçeklenmez ise, hata ayıklama engel web sunucusu diğer isteklere yanıt. Üretim ilgili sorunları gidermek için en iyi şekilde kaynaktır [günlüğe kaydetmeyi yapılandırmak](#logging) ve [Application Insights](#insights).



## <a name="explorer"></a>Adım 8 - işlem Gezgini'ni
Uygulamanız birden fazla örneğine çıkışı ölçeklendirilir zaman **işlem Gezgini'ni** örneği belirli sorunları belirlemenize yardımcı olabilir.

Kullanım **işlem Gezgini'ni** için:

- Tüm işlemler farklı uygulama hizmeti planınızı örneklerinde sıralar.
- Detaya ve işleyicileri ve modülleri her işlemle ilişkili görüntüleyin.
- CPU, çalışma kümesi, görüntüleyin ve iş parçacığı sayısı kaçak işlemleri tanımlamanıza yardımcı olması için işlem düzeyinde
- Açık dosya işlemesi bulun ve hatta belirli işlem örneği sonlandır.

İşlem Gezgini'ni altında bulunabilir **izleme** > **işlem Gezgini'ni**.

![İşlem Gezgini](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <a name="insights"></a>Adım 9 - Application Insights
**Application Insights** uygulamanız için uygulama profili oluşturma ve Gelişmiş izleme özelliklerini sağlar.

Application Insights algılamak ve özel durumları ve Web uygulamanızda performans sorunlarını tanılamak için kullanın.

Web uygulamanız için Application Insights etkinleştirebilirsiniz **izleme** > **Application Insights**

> [!NOTE]
> Application Insights veri toplama başlatmak için Application Insights site uzantıyı yüklemek isteyebilir. Site uzantısı yükleme uygulama yeniden başlatma neden olur.

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

Application Insights ayarlanırsa, daha fazla bilgi edinmek için dahil bağlantıları izleyin zengin bir özellik olan [sonraki adımlar](#next) bölümü.

## <a name="next"></a> Sonraki adımlar

 - [Application Insights nedir](..\application-insights\app-insights-overview.md)
 - [Application Insights ile Azure web uygulaması performans izleme](..\application-insights\app-insights-azure-web-apps.md)
 - [İzleyici kullanılabilirliği ve yanıt hızını Application Insights ile herhangi bir web sitesi](..\application-insights\app-insights-monitor-web-app-availability.md)
