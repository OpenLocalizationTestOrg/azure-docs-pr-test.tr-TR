---
title: "aaaBest yöntemler ve Azure Web uygulamaları üzerinde düğümü uygulamalar için sorun giderme kılavuzu"
description: "Merhaba en iyi yöntemler ve sorun giderme adımları düğümü uygulamaları için Azure Web Apps öğrenin."
services: app-service\web
documentationcenter: nodejs
author: ranjithr
manager: wadeh
editor: 
ms.assetid: 387ea217-7910-4468-8987-9a1022a99bef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 06/06/2016
ms.author: ranjithr
ms.openlocfilehash: 975898142a224f14df1091a46d16e9074d9e2831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-and-troubleshooting-guide-for-node-applications-on-azure-web-apps"></a>En iyi yöntemler ve Azure Web uygulamaları üzerinde düğümü uygulamalar için sorun giderme kılavuzu
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Bu makalede, hello en iyi yöntemler ve sorun giderme adımları için öğreneceksiniz [düğümü uygulamaları](app-service-web-get-started-nodejs.md) Azure Webapps üzerinde çalışan (ile [iisnode](https://github.com/azure/iisnode)).

> [!WARNING]
> Sorun giderme adımlarını üretim sitenizde kullanırken dikkatli olun. Önerilir tootroubleshoot uygulamanıza üretim dışı örneğin hazırlama yuvası Kurulum ve hello sorun düzeltildiğinde, hazırlama yuvası, üretim yuvası ile takas.
> 
> 

## <a name="iisnode-configuration"></a>IISNODE yapılandırma
Bu [şema dosyası](https://github.com/Azure/iisnode/blob/master/src/config/iisnode_schema_x64.xml) için ıısnode yapılandırılabilir tüm hello ayarlarını gösterir. Uygulamanız için yararlı olacak hello ayarlardan bazıları şunlardır:

* nodeProcessCountPerApplication
  
    Bu ayar, IIS uygulaması başlatılan düğüm işlemlerin hello sayısını denetler. Varsayılan değer 1'dir. Bu too0 ayarlayarak, VM çekirdek sayısı sayıda node.exe ait başlatabilirsiniz. Tüm hello çekirdek makinenizde kullanabilir için önerilen değeri çoğu uygulama için 0'dır. Node.exe tek bir node.exe en fazla 1 Çekirdeği ve tooget en yüksek performans, düğüm uygulamanızın dışında kullanacak şekilde akan tüm çekirdek tooutilize istersiniz.
* nodeProcessCommandLine
  
    Bu ayar, hello yolu toohello node.exe denetler. Bu değer toopoint tooyour node.exe sürümü ayarlayabilirsiniz.
* maxConcurrentRequestsPerProcess
  
    Bu ayar hello en fazla iisnode tooeach node.exe tarafından gönderilen eşzamanlı istek sayısını denetler. Azure webapps üzerinde bu hello varsayılan değer sonsuzdur. Bu ayar hakkında tooworry olmayacaktır. Azure webapps dışında hello varsayılan değer 1024'tür. Tooconfigure kaç uygulamanızı istekleri bağlı olarak bu alır ve ne kadar hızlı uygulamanızı her isteğini işler isteyebilirsiniz.
* maxNamedPipeConnectionRetry
  
    Bu ayar hello en fazla kaç kez iisnode kanal toosend hello isteği toonode.exe adlı hello yapmayı bağlantıda deneyecek denetler. Bu ayar namedPipeConnectionRetryDelay birlikte hello iisnode içindeki her bir isteği toplam zaman aşımı belirler. Varsayılan değer Azure Webapps üzerinde 200'dür. Zaman aşımı saniye cinsinden toplam = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000
* namedPipeConnectionRetryDelay
  
    Süre (ms) iisnode bu ayarı denetimleri hello miktarı her yeniden deneme toosend isteği toonode.exe hello adlandırılmış kanal üzerinden arasında bekler. 250ms varsayılan değerdir.
    Zaman aşımı saniye cinsinden toplam = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000
  
    Varsayılan olarak azure webapps üzerinde iisnode toplam zaman aşımı hello 200 olan \* 250ms = 50 saniye.
* logDirectory
  
    Bu ayar, iisnode stdout/stderr burada oturum hello dizin denetler. Varsayılan değer göreli toohello ana komut dosyası dizini (ana server.js mevcut olduğu dizin) olan iisnode:
* debuggerExtensionDll
  
    Bu ayar, node-Inspector iisnode hangi sürümünün düğümü uygulamanızın hatalarını ayıklama kullanacağı denetler. Şu anda iisnode denetçisi 0.7.3.dll ve iisnode inspector.dll hello yalnızca 2 geçerli için bu ayarı değerlerdir. İisnode denetçisi 0.7.3.dll varsayılan değerdir. iisnode denetçisi 0.7.3.dll sürüm düğümü denetçisi 0.7.3 ve bu sürümü, azure webapp toouse tooenable websockets gerekir böylece websockets, kullanır. Bkz: <http://www.ranjithr.com/?p=98> nasıl tooconfigure iisnode toouse hello yeni node-Inspector hakkında daha fazla bilgi.
* flushResponse
  
    Merhaba varsayılan IIS temizleme önce too4MB yanıt verileri arabelleği veya hello yanıt hello sonuna kadar hangisi önce gelirse davranıştır. iisnode yapılandırma Bu davranış toooverride ayarı sunar: tooflush hello yanıt Varlık gövdesi bir parçasını iisnode olan en kısa sürede alır, node.exe, tooset hello gereksinim iisnode/@flushResponse web.config too'true özniteliğinde ':
  
    ```
    <configuration>    
        <system.webServer>    
            <!-- ... -->    
            <iisnode flushResponse="true" />    
        </system.webServer>    
    </configuration>
    ```
  
    Merhaba yanıt Varlık gövdesi her parçasında temizleme etkinleştirilmesi ~ %5 (itibariyle v0.1.13) tarafından hello sistem hello verimini azaltan performansa ekler, dolayısıyla tooscope (örneğin hello kullanarak yanıt akış gerektiren bu ayar yalnızca tooendpoints en iyi <location> hello web.config öğesinde)
  
    Uygulamalar, akış için ek toothis içinde tooalso kümesi responseBufferLimit iisnode işleyici too0 biri gerekir.
  
    ```
    <handlers>    
        <add name="iisnode" path="app.js" verb="\*" modules="iisnode" responseBufferLimit="0"/>    
    </handlers>
    ```
* watchedFiles
  
    Bu değişiklikleri izlenen dosyaların noktalı virgülle ayrılmış listesidir. Bir değişiklik tooa dosyası hello uygulama toorecycle neden olur. Bir isteğe bağlı dizin adı artı hello ana uygulama giriş noktası bulunduğu göreli toohello dizin olan gerekli dosya adı her girdi oluşur. Joker karakterler hello dosya adı bölümünde yalnızca izin verilir. Varsayılan değer "\*. js;web.config"
* recycleSignalEnabled
  
    Varsayılan değer false şeklindedir. Etkinleştirilirse, düğüm uygulamanızı adlandırılmış tooa bağlanabilir (ortam değişkeni IISNODE\_denetim\_kanal) ve "Geri Dönüşüm" iletisi gönderin. Bu hello w3wp toorecycle düzgün biçimde neden olur.
* idlePageOutTimePeriod
  
    Varsayılan değer bu özellik devre dışı yani 0'dır. Ne zaman kümesi toosome değeri 0'dan iisnode büyük tüm alt sayfa her 'idlePageOutTimePeriod' milisaniyede işler. toounderstand ne sayfa anlamına gelir, lütfen toothis bakın [belgelerine](https://msdn.microsoft.com/library/windows/desktop/ms682606.aspx). Bu ayar çok miktarda bellek kullanır ve toopageout bellek toodisk istediğiniz uygulamalar için yararlı olacak bazen toofree bazı RAM.

> [!WARNING]
> Yapılandırma ayarları üretim uygulamaları aşağıdaki hello etkinleştirirken dikkatli olun. Önerilir toonot Canlı üretim uygulamaları etkinleştirin.
> 
> 

* debugHeaderEnabled
  
    Merhaba varsayılan değer false şeklindedir. Varsa ayarlamak tootrue, iisnode gönderir hello iisnode-debug üstbilgi değeri olan bir URL bir HTTP yanıt üstbilgisi iisnode-debug tooevery HTTP yanıtının eklenir. Tanılama bilgileri tek tek parçaları hello URL parçası bakarak konusunda, ancak daha iyi görselleştirme hello URL hello tarayıcısında açarak elde edilir.
* loggingEnabled
  
    Bu ayar tarafından iisnode stdout ve stderr hello günlüğe kaydedilmesini denetler. Iisnode stdout/stderr başlatılır düğümü işlemlerden yakalamak ve hello 'logDirectory' ayarında belirtilen toohello dizinine yazma. Etkinleştirme sonra uygulamanızı günlükleri toohello dosya sistemi yazma ve hello uygulama tarafından gerçekleştirilen günlük hello miktarına bağlı olarak, olabilir performans etkileri.
* devErrorsEnabled
  
    Varsayılan değer false şeklindedir. Tootrue, ayarlandığında iisnode tarayıcınızdaki hello HTTP durum kodu ve Win32 hata kodu görüntülenir. Merhaba win32 kodu belirli türde bir sorunları hata ayıklamaya yardımcı olacaktır.
* debuggingEnabled (Canlı üretim sitesinde etkinleştirmeyin.)
  
    Bu ayar, hata ayıklama özelliği denetler. Iisnode node-Inspector ile tümleşiktir. Bu ayarın etkinleştirilmesi, düğüm uygulamanızın veya hata ayıklamayı etkinleştir. Bu ayar etkinleştirildiğinde, iisnode düzeni hello gerekli node-Inspector 'debuggerVirtualDir' dizindeki dosya hello ilk hata ayıklama isteği tooyour düğüm uygulama üzerinde olacaktır. Bir istek toohttp://yoursite/server.js/debug göndererek hello node-Inspector yükleyebilirsiniz. 'DebuggerPathSegment' ayarıyla hello hata ayıklama URL kesimi kontrol edebilirsiniz. Varsayılan debuggerPathSegment tarafından = 'debug'. Başkaları tarafından bulunan daha zor toobe olmasını sağlayın, örneğin bu tooa GUID ayarlayabilirsiniz.
  
    Bu kontrol [bağlantı](https://tomasz.janczuk.org/2011/11/debug-nodejs-applications-on-windows.html) hata ayıklama hakkında daha fazla bilgi.

## <a name="scenarios-and-recommendationstroubleshooting"></a>Senaryolar ve öneriler ve giderme
### <a name="my-node-application-is-making-too-many-outbound-calls"></a>Düğüm Uygulamam çok fazla giden çağrıları yapma.
Birçok uygulama toomake giden bağlantılar normal işlemlerinin bir parçası olarak istersiniz. Örneğin, bir istek geldiğinde, düğüm uygulamanızı toocontact başka bir yerde bir REST API istediğiniz ve bazı bilgileri tooprocess hello isteğini alın. Http veya https çağrıları yapılırken toouse canlı tutma Aracısı istersiniz. Örneğin, bu giden çağrıları yapılırken canlı tutma aracısı olarak hello agentkeepalive modülü kullanabilirsiniz. Bu hello yuva azure webapp VM ve giden her istek için yeni yuva oluşturma azalan hello yükünü yeniden kullanıldığı emin olur. Ayrıca, bu daha az sayıda yuva toomake birçok Giden istekleri ve bu nedenle, VM başına ayrılmış hello maxSockets aşmayan kullandığınızdan emin olur. Azure Webapps öneriye tooset hello agentKeepAlive maxSockets VM başına 160 yuva tooa toplam değer olacaktır. Bu VM hello üzerinde çalışan 4 node.exe varsa, tooset hello agentKeepAlive maxSockets too40 160 VM başına toplam olan node.exe başına istiyor anlamına gelir.

Örnek [agentKeepALive](https://www.npmjs.com/package/agentkeepalive) yapılandırma:

```
var keepaliveAgent = new Agent({    
    maxSockets: 40,    
    maxFreeSockets: 10,    
    timeout: 60000,    
    keepAliveTimeout: 300000    
});
```

Bu örnek, VM'de çalıştırılan 4 node.exe olduğunu varsayar. Merhaba VM üzerinde çalışan node.exe farklı sayıda varsa, toomodify hello maxSockets buna uygun olarak ayarlanması gerekir.

### <a name="my-node-application-is-consuming-too-much-cpu"></a>Düğüm Uygulamam çok fazla CPU tüketilmesine neden olabilir.
Yüksek cpu tüketimi hakkında portalınızdaki Azure Webapps bir öneri büyük olasılıkla alırsınız. Kurulum izleyiciler toowatch belirli kullanabileceğiniz [ölçümleri](web-sites-monitor.md). Merhaba Hello CPU kullanımı denetlerken [Azure portalı panosunun](../application-insights/app-insights-web-monitor-performance.md), hello en yüksek değerleri kaçırmamak için hello en yüksek değerleri için CPU gözden geçirin.
Burada, uygulamanızın çok fazla CPU kullanan ve nedenini açıklayan olamaz düşündüğünüz durumlarda tooprofile düğümü uygulamanız gerekir.

### 
#### <a name="profiling-your-node-application-on-azure-webapps-with-v8-profiler"></a>Düğüm Uygulamanızı azure webapps V8 Profil Oluşturucu ile profil oluşturma
Örneğin, deyin aşağıda gösterildiği gibi tooprofile istediğiniz bir hello world uygulamanız olanak tanır:

```
var http = require('http');    
function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    WriteConsoleLog();    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

Tooyour scm site https://yoursite.scm.azurewebsites.net/DebugConsole gidin

Aşağıda gösterildiği gibi bir komut istemi görürsünüz. Site/wwwroot dizinine gidin

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_install_v8.png)

"Npm yükleme v8 profil oluşturucu" Merhaba komutunu çalıştırın

Bu profil oluşturucu v8 düğümü altında yüklemelidir\_modülleri dizin ve tüm bağımlılıkları.
Şimdi, uygulamanızın server.js tooprofile düzenleyin.

```
var http = require('http');    
var profiler = require('v8-profiler');    
var fs = require('fs');

function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    profiler.startProfiling('HandleRequest');    
    WriteConsoleLog();    
    fs.writeFileSync('profile.cpuprofile', JSON.stringify(profiler.stopProfiling('HandleRequest')));    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

değişiklikler yukarıda Hello hello WriteConsoleLog işlevi profil ve hello profili çıktı too'profile.cpuprofile yazma ' dosyasını site wwwroot altında. Bir istek tooyour uygulaması gönderin. Site wwwroot altında oluşturulan 'profile.cpuprofile' dosyasını görürsünüz.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_profile.cpuprofile.png)

Bu dosyayı yükleyin ve bu dosyayı Chrome F12 araçları ile tooopen gerekir. Chrome üzerinde F12 isabet ve "Profilleri sekmesini" Merhaba üzerinde'i tıklatın. "Yük" düğmesine tıklayın. Az önce indirdiğiniz profile.cpuprofile dosyanızı seçin. Yeni yüklenen hello profiline tıklayın.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/chrome_tools_view.png)

Başlangıç saati % 95 aşağıda gösterildiği gibi WriteConsoleLog işlevi tarafından tüketilen görürsünüz. Bu ayrıca hello tam satır numaralarını ve hello soruna neden kaynak dosyaları gösterilmektedir.

### <a name="my-node-application-is-consuming-too-much-memory"></a>Düğüm Uygulamam çok fazla bellek tükettikten.
Yüksek bellek tüketimi hakkında portalınızdaki Azure Webapps bir öneri büyük olasılıkla alırsınız. Kurulum izleyiciler toowatch belirli kullanabileceğiniz [ölçümleri](web-sites-monitor.md). Merhaba Hello bellek kullanımı denetlerken [Azure portalı panosunun](../application-insights/app-insights-web-monitor-performance.md), hello en yüksek değerleri kaçırmamak için bellek hello en yüksek değerleri gözden geçirin.

#### <a name="leak-detection-and-heap-diffing-for-nodejs"></a>Sızıntısı algılama ve node.js için yığın farkı alınıyor
Kullanabileceğinizi [düğümü memwatch](https://github.com/lloyd/node-memwatch) toohelp sizi tanımlamak bellek sızıntılarını.
Uygulamanızda memwatch v8 profil oluşturucu ve düzenleme, kod toocapture ve fark yığınlara tooidentify hello bellek sızıntıları gibi yükleyebilirsiniz.

### <a name="my-nodeexes-are-getting-killed-randomly"></a>My node.exe's rastgele sonlandırıldı
Neden bu geçekleşmiş birkaç nedeni vardır:

1. Uygulamanızı Lütfen onay d: Yakalanmayan Özel durumlar – atma\\ev\\LogFiles\\uygulama\\hello Ayrıntılar için günlük errors.txt dosyasını hello özel durum belirtildi. Bu dosya, bunu temel alarak, uygulamanızın giderebilmemiz hello yığın izlemesi sahiptir.
2. Uygulamanızın hangi Başlarken gelen diğer işlemleri etkileyen çok fazla bellek tükettikten. Node.exe's Hello toplam VM bellek Kapat too100% ise sonlandırıldı hello işlem yöneticisi toolet tarafından diğer işlemleri fırsat toodo bazı iş alın. toofix Bu, uygulamanızın olmayan bellek sızıntısı emin olun ya da uygulama, gerçekten toouse çok miktarda bellek gerekiyorsa, lütfen tooa ölçeklendirme çok daha fazla RAM ile büyük VM.

### <a name="my-node-application-does-not-start"></a>Düğüm Uygulamam başlamıyor
Uygulamanızı başlangıçta 500 hataları döndürüyor birkaç nedeni olabilir:

1. Node.exe hello doğru konumda mevcut değil. NodeProcessCommandLine ayarını denetleyin.
2. Ana komut dosyası hello doğru konumda mevcut değil. Web.config denetleyin ve hello işleyicileri bölüm eşleşmeleri hello ana komut dosyasında hello hello ana komut dosyası adını emin olun.
3. Web.config yapılandırması doğru değil-hello ayarları adları/değerlerini denetleyin.
4. Soğuk başlangıç – uygulamanızı toostartup çok uzun sürüyor. Uygulamanızı daha uzun sürerse (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000 saniye iisnode 500 hata döndürür. Uygulamanızı başlatmak zaman tooprevent iisnode zaman aşımına uğrama ve hello 500 hata döndürüyor bu ayarları toomatch Hello değerini artırın.

### <a name="my-node-application-crashed"></a>Düğüm Uygulamam kilitlendi
Uygulamanızı Lütfen onay d: Yakalanmayan Özel durumlar – atma\\ev\\LogFiles\\uygulama\\hello Ayrıntılar için günlük errors.txt dosyasını hello özel durum belirtildi. Bu dosya, bunu temel alarak, uygulamanızın giderebilmemiz hello yığın izlemesi sahiptir.

### <a name="my-node-application-takes-too-much-time-toostartup-cold-start"></a>Çok fazla zaman toostartup (Cold Start) düğüm Uygulamam alır
Bunun en yaygın nedeni Merhaba uygulaması çok sayıda dosya hello düğümünde olmasıdır\_modülleri ve hello uygulama çalıştığında tooload başlatma sırasında bu dosyaların çoğu. Merhaba ağ paylaşımında Azure Webapps dosyalarınızın bulunduğu varsayılan olarak, çok sayıda dosya yükleme biraz zaman alabilir.
Bazı çözümleri toomake bu daha hızlı şunlardır:

1. Düz bağımlılık yapısı ve yinelenen bağımlılık modüllerinizi npm3 tooinstall kullanarak olduğundan emin olun.
2. Toolazy yük düğümünüz deneyin\_modülleri ve tüm başlangıçta hello modüllerin yük değil. Bu gerçekten ihtiyacınız olduğunda bu hello çağrısı toorequire('module')'in yapılması anlamına gelir hello işlev içinde toouse hello modülü deneyin.
3. Azure Webapps yerel önbelleği olarak adlandırılan bir özellik sunar. Bu özellik hello ağ paylaşımı toohello yerel diskte hello VM içeriğinizi kopyalar. Merhaba dosyaları yerel olduğundan, hello yükleme zamanı düğümünün\_modülleri çok daha hızlı. -Bu [belgelerine](../app-service/app-service-local-cache.md) nasıl toouse yerel önbellekteki daha ayrıntılı açıklanır.

## <a name="iisnode-http-status-and-substatus"></a>IISNODE http durumu ve alt durumu
Bu [kaynak dosyası](https://github.com/Azure/iisnode/blob/master/src/iisnode/cnodeconstants.h) tüm hello olası durum substatus birleşimi iisnode hatası durumunda dönebilirsiniz listeler.

Uygulama toosee hello win32 hata kodu için FREB etkinleştir (Lütfen FREB performans nedenleriyle üretim dışı sitelerindeki yalnızca etkinleştirdiğinizden emin olun).

| Http durumu | HTTP alt durum | Olası bir nedeni? |
| --- | --- | --- |
| 500 |1000 |Merhaba isteği tooIISNODE göndermeyi bazı sorun oluştu – node.exe başlatıldığından ise denetleyin. Başlangıçta node.exe çökme. Hatalar için web.config yapılandırmanızı denetleyin. |
| 500 |1001 |-Win32Error 0x2 - uygulama toohello URL yanıt vermiyor. Onay URL yeniden yazma kuralları veya express uygulamanızı tanımlanan hello doğru rotalar varsa. -Win32Error 0x6d – adlandırılmış kanal meşgul – hello kanal meşgul olduğundan Node.exe isteklerini kabul etmiyor. Yüksek cpu kullanımını denetleyin. -Diğer hataları – denetleyin, node.exe kilitlendi. |
| 500 |1002 |Node.exe kilitlendi – d: denetleyin\\ev\\LogFiles\\yığın izlemesi için günlük errors.txt. |
| 500 |1003 |Kanal yapılandırma sorunu – hiçbir zaman bu görmeniz gerekir, ancak bunu yaparsanız, kanal Yapılandırması adlı hello yanlıştır. |
| 500 |1004-1018 |Merhaba istek veya işleme hello yanıt denetleyicisinden node.exe gönderilirken bazı hata oluştu. Node.exe kilitlendi olmadığını denetleyin. d: denetleyin\\ev\\LogFiles\\yığın izlemesi için günlük errors.txt. |
| 503 |1000 |Yeterli bellek tooallocate daha kanal bağlantısı adı. Uygulamanız çok bellek neden tükettikten denetleyin. MaxConcurrentRequestsPerProcess ayarının değerini denetleyin. Varsa, not sonsuz ve çok sayıda isteği varsa, bu değer tooprevent bu hatayı artırın. |
| 503 |1001 |Merhaba uygulamasını geri dönüşüme olduğundan isteği gönderilen toonode.exe bulunamadı. Merhaba uygulamasını geri dönüşüme sonra istekleri normalde hizmet. |
| 503 |1002 |Gerçek bir nedenle – isteği onay win32 hata kodu gönderilen tooa node.exe bulunamadı. |
| 503 |1003 |Adlandırılmış kanal çok meşgul – düğüm CPU çok kullanmadığına denetleyin |

DÜĞÜM olarak adlandırılır NODE.exe içinde bir ayar yoktur\_BEKLEYEN\_kanal\_örnekleri. Azure webapps dışında varsayılan olarak bu değer 4 olur. Başka bir deyişle, bu node.exe hello adlandırılmış bir zaman 4 isteği yalnızca kabul edebilir. Azure Webapps, bu değer too5000 ayarlanır ve bu değer azure webapps üzerinde çalışan çoğu düğümü uygulamalar için yeterince iyi olmalıdır. Biz hello düğümü için yüksek bir değere sahip olduğundan, 503.1003 üzerinde azure webapps görülmemelidir\_BEKLEYEN\_kanal\_örnekleri.  |

## <a name="more-resources"></a>Diğer kaynaklar
Azure App Service node.js uygulamaları hakkında daha fazla bu bağlantılar toolearn izleyin.

* [Azure App Service'te Node.js web uygulamalarını kullanmaya başlama](app-service-web-get-started-nodejs.md)
* [Nasıl toodebug bir Node.js web uygulamasını Azure App Service'te](web-sites-nodejs-debug.md)
* [Azure uygulamalarıyla Node.js Modüllerini kullanma](../nodejs-use-node-modules-azure-apps.md)
* [Azure Uygulama Hizmeti Web Apps: Node.js](https://blogs.msdn.microsoft.com/silverlining/2012/06/14/windows-azure-websites-node-js/)
* [Node.js Geliştirici Merkezi](../nodejs-use-node-modules-azure-apps.md)
* [Merhaba Süper gizli Kudu hata ayıklama konsolunu keşfetme](https://azure.microsoft.com/documentation/videos/super-secret-kudu-debug-console-for-azure-web-sites/)

