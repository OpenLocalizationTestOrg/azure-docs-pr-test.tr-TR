---
title: Azure Application Insights ile aaaMonitor Node.js Hizmetleri | Microsoft Docs
description: "Application Insights ile Node.js hizmetlerindeki performansı izleyin ve sorunları tanılayın."
services: application-insights
documentationcenter: nodejs
author: joshgav
manager: carmonm
ms.assetid: 2ec7f809-5e1a-41cf-9fcd-d0ed4bebd08c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/01/2017
ms.author: bwren
ms.openlocfilehash: 0a7e66990cd4d3a2fcaf3fa779adb336c861f8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a>Application Insights ile Node.js hizmetlerinizi ve uygulamalarınızı izleme

[Azure Application Insights](app-insights-overview.md) toohelp dağıttıktan sonra arka uç Hizmetleri ve bileşenleri izler, [bulmak ve hızlı bir şekilde performans ve diğer sorunları tanılamak](app-insights-detect-triage-diagnose.md). Veri merkeziniz, Azure VM’leri, Web Apps ve hatta diğer genel bulutlar dahil herhangi bir yerde barındırılan Node.js hizmetleri için kullanın.

tooreceive, depolayıp, izleme verilerinizi keşfedin, yönergeleri tooinclude kodunuzda bir aracı aşağıdaki hello izleyin ve azure'da karşılık gelen bir Application Insights kaynağı ayarlayın. Merhaba aracı veri toothat kaynak daha detaylı analiz ve araştırması için gönderir.

Merhaba Node.js Aracısı, gelen ve giden HTTP isteklerini, birkaç sistem ölçümleri ve özel durumları otomatik olarak izleyebilirsiniz. Sürüm 0.20 sonrası sürümlerde, `mongodb`, `mysql` ve `redis` gibi bazı yaygın üçüncü taraf paketlerini de izleyebilir. Tüm olayları tooan gelen HTTP istek bağıntılı daha hızlı sorun giderme için ilgili.

Uygulamanızı daha fazla yönlerini izleyebilirsiniz ve bunları el ile düzenleme tarafından sistem kullanarak hello Aracısı API'si aşağıda açıklanmıştır.

![Örnek performans izleme grafikleri](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a>Başlarken

Şimdi, bir uygulama veya hizmet için izlemeyi ayarlama adımlarına bakalım.

### <a name="resource"></a> App Insights kaynağı oluşturma

**Başlamadan önce**, bir Azure aboneliğine sahip olduğunuzdan emin olun veya [ücretsiz olarak yeni bir tane edinin][azure-free-offer]. Kuruluşunuzun zaten bir Azure aboneliğiniz varsa, bir yönetici izleyebilirsiniz [bu yönergeleri] [ add-aad-user] tooadd, tooit.

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

Şimdi toohello oturum [Azure portal] [ portal] ve hello aşağıda gösterildiği gibi bir Application Insights kaynağı oluşturma - "Yeni"'a tıklayın > "Geliştirici Araçları" > "Application Insights". Merhaba kaynak telemetri verileri, raporlar ve panolar, kural ve uyarı yapılandırma ve daha fazla kaydedilen bu veriler için depolama alanı almak için bir uç nokta içerir.

![App Insights kaynağı oluşturma](./media/app-insights-nodejs/03-new_appinsights_resource.png)

Merhaba kaynak oluşturma sayfasında "Node.js uygulaması" Merhaba uygulama türü açılan listeden seçin. Merhaba uygulama türü hello varsayılan panolar ve raporlar için oluşturduğunuz belirler. Ancak endişelenmeyin, herhangi bir Application Insights kaynağı herhangi bir dil ve platformdan veri toplayabilir.

![Yeni App Insights kaynağı formu](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <a name="agent"></a>Merhaba Node.js aracısını ayarlama

Bu verileri toplamak için zaman tooinclude hello aracı, uygulamanızda sunulmuştur.
Başlat, kaynağın izleme anahtarını kopyalayarak (Bundan sonra tooas başvurulan, `ikey`) aşağıda gösterildiği gibi hello portalından. Merhaba App Insights sistem toospecify gerekir böylece bu anahtar toomap veri tooyour Azure kaynak kullanır, bir ortam değişkeni veya kodunuz hello Aracısı toouse için.  

![İzleme anahtarını kopyalama](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

Ardından, package.json aracılığıyla hello Node.js Aracısı kitaplığı tooyour uygulamanın bağımlılıkları ekleyin. Merhaba kök klasörden, uygulamanızın, çalıştırın:

```bash
npm install applicationinsights --save
```

Şimdi, kodunuzda tooexplicitly yük hello kitaplığı gerekir. Merhaba Aracısı Araçları diğer birçok kitaplıkları içine yerleştirir olduğundan, hatta diğer önce olabildiğince erken yükleyeceğini `require` deyimleri. tooget başlatıldı, ilk .js dosyanızı hello üstüne ekleyin:

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

Merhaba `setup` yöntemi yapılandırır hello izleme anahtarını (ve bu nedenle Azure kaynak) toobe varsayılan olarak tüm izlenen öğeler için kullanılabilir. Çağrı `start` yapılandırma tamamlanmış toobegin toplamak ve telemetri verileri göndermeye sonra.

Ayrıca bir ikey hello ortam değişkeni APPINSİGHTS'dan aracılığıyla sağlayabilir\_çok el ile geçirme yerine INSTRUMENTATIONKEY `setup()` veya `getClient()`. Bu yöntem kaydedilmiş kaynak kodu dışında ikeys ve farklı ortamlar için farklı ikeys toospecify tutmanıza olanak tanır.

Ek yapılandırma seçenekleri aşağıda belirtilmiştir.

Merhaba Aracısı hello araçları anahtar tooany boş dize ayarlayarak telemetri verilerini göndermeden deneyebilirsiniz.

### <a name="monitor"></a> Uygulamanızı izleme

Hello Aracısı hello Node.js çalışma zamanı hakkında telemetriyi ve ortak bazı üçüncü taraf modüllerin otomatik olarak toplar. Uygulamayı şimdi toogenerate kullanın Bu verilerin bazıları.

Ardından hello [Azure portal] [ portal] daha önce oluşturduğunuz toohello Application Insights kaynağı göz atın ve birkaç veri noktası için ilk, görüntü aşağıdaki hello olduğu gibi hello genel bakış zaman çizelgesi bakın. Daha fazla ayrıntı için hello grafikler aracılığıyla'ı tıklatın.

![İlk veri noktaları](./media/app-insights-nodejs/12-first-perf.png)

Merhaba uygulama harita düğmesini tooview hello topolojisi görüntüsü aşağıdaki hello olduğu gibi uygulamanız için bulunan'ı tıklatın. Daha fazla ayrıntı için hello eşlemesindeki bileşenleri üzerinden'ı tıklatın.

![Basit uygulama eşlemesi](./media/app-insights-nodejs/06-appinsights_appmap.png)

Uygulamanız hakkında daha fazla bilgi ve diğer görünümlere hello "Araştır" bölümü altında kullanılabilir hello kullanarak sorunlarını giderebilirsiniz.

![Araştır bölümü](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a>Veri yok mu?

Merhaba aracısı veri gönderimi için toplu işlemleri nedeniyle hello Portalı'nda görüntülenen öğelerin önce bir gecikme olabilir. Görmüyorsanız, veri kaynağınızın düzeltmeleri aşağıdaki hello bazılarını deneyin:

* Merhaba uygulaması bazı daha kullanın; Daha fazla Eylemler toogenerate daha fazla telemetri alın.
* Tıklatın **yenileme** hello portal kaynak görünümünde. Grafikler otomatik olarak kendilerini düzenli olarak yeniler, ancak bu toohappen yenilemeyi hemen zorlar.
* [Gerekli giden bağlantı noktalarının](app-insights-ip-addresses.md) açık olduğunu doğrulayın.
* Açık hello [arama](app-insights-diagnostic-search.md) parçasında ve tek tek olaylarını arayın.
* Merhaba denetleyin [SSS][].


## <a name="agent-configuration"></a>Aracı Yapılandırması

Merhaba aracısının yapılandırma yöntemleri ve varsayılan değerlerine aşağıda verilmiştir.

bir hizmette toofully correlate olayları olarak emin tooset `.setAutoDependencyCorrelation(true)`. Bu hello Aracısı tootrack bağlamı Node.js içinde zaman uyumsuz geri aramalar arasında sağlar.

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>")
    .setAutoDependencyCorrelation(false)
    .setAutoCollectRequests(true)
    .setAutoCollectPerformance(true)
    .setAutoCollectExceptions(true)
    .setAutoCollectDependencies(true)
    .start();
```

## <a name="agent-api"></a>Aracı API'si

<!-- TODO: Fully document agent API. -->

Merhaba .NET Aracısı API tam olarak açıklanan [burada](app-insights-api-custom-events-metrics.md).

İstek, olay, ölçüm veya hello uygulama Öngörüler Node.js istemcisini kullanarak özel durum izleyebilirsiniz. Merhaba aşağıdaki örnek bazılarını hello göstermektedir kullanılabilir API'ler.

```javascript
let appInsights = require("applicationinsights");
appInsights.setup().start(); // assuming ikey in env var
let client = appInsights.getClient();

client.trackEvent("my custom event", {customProperty: "custom property value"});
client.trackException(new Error("handled exceptions can be logged with this method"));
client.trackMetric("custom metric", 3);
client.trackTrace("trace message");

let http = require("http");
http.createServer( (req, res) => {
  client.trackRequest(req, res); // Place at hello beginning of your request handler
});
```

### <a name="track-your-dependencies"></a>Bağımlılıklarınızı izleme

```javascript
let appInsights = require("applicationinsights");
let client = appInsights.getClient();

var success = false;
let startTime = Date.now();
// execute dependency call here....
let duration = Date.now() - startTime;
success = true;

client.trackDependency("dependency name", "command name", duration, success);
```

### <a name="add-a-custom-property-tooall-events"></a>Bir özel özellik tooall olaylar ekleme

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a>HTTP GET isteklerini izleme

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a>Sunucu başlangıç saatini izleme

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a>Diğer kaynaklar

* [Merhaba portalında telemetrinizi izleme](app-insights-dashboards.md)
* [Telemetriniz üzerinden Analiz sorguları yazma](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[SSS]: app-insights-troubleshoot-faq.md
