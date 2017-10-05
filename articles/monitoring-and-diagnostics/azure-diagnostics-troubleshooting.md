---
title: "Azure tanılama sorunlarını giderme | Microsoft Docs"
description: "Azure Virtual Machines, Service Fabric veya Bulut Hizmetleri Azure tanılama kullanırken sorunlarını giderin."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 66469bce-d457-4d1e-b550-a08d2be4d28c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: robb
ms.openlocfilehash: a0cb529836b14df71e83616f4f625a002c535b7b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-diagnostics-troubleshooting"></a>Azure tanılama sorunlarını giderme
Sorun giderme bilgileri için Azure Tanılama'yı kullanarak ilgili. Azure Tanılama hakkında daha fazla bilgi için bkz: [Azure tanılama genel bakış](azure-diagnostics.md).

## <a name="logical-components"></a>Mantıksal bileşenleri
**Tanılama eklentisi Başlatıcısı (DiagnosticsPluginLauncher.exe)**: Azure tanılama uzantısını başlatır. Giriş gören işlem gelin.

**Tanılama Eklentisi (DiagnosticsPlugin.exe)**: Yukarıdaki başlatıcısı tarafından başlatılır İzleme Aracısı yapılandırır, başlatılır ve yaşam süresi yönetir ana işlem. 

**İzleme aracısını (MonAgent\*.exe işlemler)**: toplu iş; yani, izleme, koleksiyon ve tanılama veri aktarımını bu işlemleri yapın.  

## <a name="logartifact-paths"></a>Günlük/yapı yolları
Burada, bazı önemli günlükleri ve yapıları yolları bulunmaktadır. Bu belgenin geri kalanında başvuran tutun:
### <a name="cloud-services"></a>Cloud Services
| Yapı | Yol |
| --- | --- |
| **Azure tanılama yapılandırma dosyası** | %SystemDrive%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<sürüm > \Config.txt |
| **Günlük dosyaları** | C:\Logs\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<sürüm > \ |
| **Tanılama verileri için yerel depolama** | C:\Resources\Directory\<CloudServiceDeploymentID >.\< Rol adı >. DiagnosticStore\WAD0107\Tables |
| **İzleme Aracısı Yapılandırma dosyası** | C:\Resources\Directory\<CloudServiceDeploymentID >.\< Rol adı >. DiagnosticStore\WAD0107\Configuration\MaConfig.xml |
| **Azure tanılama uzantısını paketi** | %SystemDrive%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<sürüm > |
| **Günlük toplama yardımcı programı yolu** | %SystemDrive%\Packages\GuestAgent\ |
| **MonAgentHost günlük dosyası** | C:\Resources\Directory\<CloudServiceDeploymentID >.\< Rol adı >. DiagnosticStore\WAD0107\Configuration\MonAgentHost. < seq_num > .log |

### <a name="virtual-machines"></a>Virtual Machines
| Yapı | Yol |
| --- | --- |
| **Azure tanılama yapılandırma dosyası** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<sürüm > \RuntimeSettings |
| **Günlük dosyaları** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<sürüm > \Logs\ |
| **Tanılama verileri için yerel depolama** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion > \WAD0107\Tables |
| **İzleme Aracısı Yapılandırma dosyası** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion > \WAD0107\Configuration\MaConfig.xml |
| **Durum dosyası** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<sürüm > \Status |
| **Azure tanılama uzantısını paketi** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion >|
| **Günlük toplama yardımcı programı yolu** | C:\WindowsAzure\Packages |
| **MonAgentHost günlük dosyası** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion > \WAD0107\Configuration\MonAgentHost. < seq_num > .log |

## <a name="metric-data-doesnt-show-in-azure-portal"></a>Azure portalında ölçüm verileri göstermiyor
Azure tanılama Azure Portalı'nda görüntülenen ölçüm verileri bir dizi sağlar. Bu verileri portalında görmesini sorunları varsa, onay tanılama depolama hesabı -> WADMetrics\* karşılık gelen ölçüm kayıt olup olmadığını görmek için tablo. Burada, tablonun PartitionKey sanal makine veya sanal makine ölçek kümesi kaynak Kimliğini, ve RowKey ölçüm adı yani performans sayacı adı.

Kaynak Kimliği yanlış ise, onay tanılama yapılandırması -> ölçümleri ResourceId kaynak kimliği doğru olarak ayarlanmış olup olmadığını görmek için ->.

Belirli ölçüm için hiçbir veri varsa, onay tanılama yapılandırması PerformanceCounter ölçüm (performans sayacı) dahil olup olmadığını görmek için ->. Varsayılan olarak aşağıdaki sayaçları etkinleştiririz.
- \Processor(_Total)\% Processor Time
- \Memory\Available Bytes
- \ASP.NET uygulamaları (__toplam__) \Requests/Sec
- \ASP.NET uygulamaları (__toplam__) \Errors toplam/sn
- \ASP.NET\Requests sıraya alındı
- \ASP.NET\Requests reddetti
- \Processor(W3wp)\% işlemci zamanı
- \Process (w3wp) \Private bayt
- \Process(WaIISHost)\% işlemci zamanı
- \Process (WaIISHost) \Private bayt
- \Process(WaWorkerHost)\% işlemci zamanı
- \Process (WaWorkerHost) \Private bayt
- \Memory\Page Hatası/sn
- \.NET CLR bellek (_genel_)\% de harcanan % zaman
- \LogicalDisk (C:) \Disk Yazma Bayt/sn
- \LogicalDisk (C:) \Disk Okuma Bayt/sn
- \LogicalDisk (D:) \Disk Yazma Bayt/sn
- \LogicalDisk (D:) \Disk Okuma Bayt/sn

Yapılandırma doğru olarak ayarlanmış, ancak yine de ölçüm verilerinin göremiyorsanız, daha fazla araştırma için aşağıdaki yönergeleri izleyin.


## <a name="azure-diagnostics-is-not-starting"></a>Azure tanılama başlatılıyor değil
Bakmak **DiagnosticsPluginLauncher.log** ve **DiagnosticsPlugin.log** neden tanılama başlatılamadı hakkında bilgi için günlük dosyalarının konumu dosyalarından sağlanan üstünde. 

Bu günlükler gösteriyorsa `Monitoring Agent not reporting success after launch`, MonAgentHost.exe başlatma bir hata oluştu anlamına gelir. Konum günlüklerine için için belirtilen bir konuma `MonAgentHost log file` yukarıdaki bölümde.

Günlük dosyaları son satırının çıkış kodu içerir.  

```
DiagnosticsPluginLauncher.exe Information: 0 : [4/16/2016 6:24:15 AM] DiagnosticPlugin exited with code 0
```
Görürseniz bir **negatif** çıkış kodu, başvurmak [çıkış kodu tablosu](#azure-diagnostics-plugin-exit-codes) içinde [başvurular](#references).

## <a name="diagnostics-data-is-not-logged-to-azure-storage"></a>Tanılama verilerini günlüğe Azure Storage olduğu
Hiçbir veri gösteren veya yalnızca bazı verileri değil gösteren belirleyin.

### <a name="diagnostics-infrastructure-logs"></a>Tanılama altyapı günlükleri
Tanılama altyapı günlükleri, burada içine çalıştıran herhangi bir hata azure tanılama günlükleri ' dir. Etkinleştirdiğinizden emin olun ([nasıl yapılır?](#how-to-check-diagnostics-extension-configuration)) yapılandırmanızda tanılama altyapı günlükleri, yakalama ve hızlı bir şekilde görünmesini ilgili hataları arayın `DiagnosticInfrastructureLogsTable` yapılandırılan depolama hesabınızdaki tablo.

### <a name="no-data-is-showing-up"></a>Hiçbir veri gösterme
Olay tamamen eksik veri yanlış en yaygın nedenlerini depolama hesabı bilgilerini tanımlanır.

Çözüm: Tanılama yapılandırmanızı düzeltin ve tanılama yeniden yükleyin.

Depolama hesabı ise, doğru yapılandırıldığını, Uzak Masaüstü emin olun ve makine içine DiagnosticsPlugin.exe ve MonAgentCore.exe çalışır. Bunlar çalışmıyorsa izleyin [Azure tanılama başlamıyor](#azure-diagnostics-is-not-starting). İşlem çalıştırıyorsa atlamak [yerel olarak yakalanan veri](#is-data-getting-captured-locally) ve bu kılavuzda buradan izleyin.

### <a name="part-of-the-data-is-missing"></a>Verilerin bir kısmını eksik
Bazı veriler alıyorsanız, ancak diğer değil. Bu veri koleksiyonu anlamına gelir / aktarım ardışık doğru olarak ayarlanmış. Sorunun ne olduğunu aşağı daraltmak için alt bölümleri burada izleyin:
#### <a name="is-collection-configured"></a>Koleksiyon yapılandırılır: 
Tanılama yapılandırması, belirli bir veri türü için toplanacak bildirir bölümü içerir. [Yapılandırmanızı gözden](#how-to-check-diagnostics-extension-configuration) değil aradığınız değil yapılandırdığınız koleksiyonu için veri emin olmak için.
#### <a name="is-the-host-generating-data"></a>Ana bilgisayar veri oluşturuluyor:
- **Performans sayaçları**: perfmon açın ve sayaç denetleyin.
- **İzleme günlükleri**: Uzak Masaüstü VM başlatın ve bir olmalıdır uygulamanın yapılandırma dosyasına ekleyin.  Metin dinleyicisi Kur http://msdn.microsoft.com/library/sk36c28t.aspx bakın.  Emin olun `<trace>` öğeye sahip `<trace autoflush="true">`.<br />
Oluşturulan izleme günlükleri görmüyorsanız izleyin [daha hakkında günlükleri izleme eksik](#more-about-trace-logs-missing).
- **ETW izlemeleri**: Uzak Masaüstü VM ve yükleme PerfView başlatın.  Çalışma Dosya -> PerfView içinde kullanıcı komutu -> dinleme etwprovder1, etwprovider2 vb..  Dinleme komutu büyük/küçük harfe duyarlıdır ve ETW sağlayıcılar virgülle ayrılmış listesi arasında boşluk olamaz unutmayın.  Çalıştırmak komutu başarısız olursa ne çalıştırmak için yapılmaya çalışıldı ve sonucu neydi görmek için Perfview aracı sağ alt 'Günlük' düğmesini tıklatabilirsiniz.  Giriş varsayarak, yeni bir pencere yukarı ve ETW izlemeleri görmesini başlayacak birkaç saniye sonra pop doğrudur.
- **Olay günlükleri**: Uzak Masaüstü VM başlatın. Açık `Event Viewer` ve olayları mevcut emin olun.
#### <a name="is-data-getting-captured-locally"></a>Verileri yerel olarak yakalanan:
Sonraki verileri yerel olarak yakalanır emin olun.
Verileri yerel olarak depolanan `*.tsf` dosyalar [Tanılama verileri için yerel deposu](#log-artifacts-path). Farklı türde günlüklerini toplanan farklı `.tsf` dosyaları. Azure depolama alanında Tablo adları için benzer adlardır. Örneğin `Performance Counters` içinde toplanan alma `PerformanceCountersTable.tsf`, olay günlüklerini toplanan `WindowsEventLogsTable.tsf`. Konusundaki yönergeleri kullanın [yerel günlük ayıklama](#local-log-extraction) bölümü yerel koleksiyon dosyaları açmak ve bunları diskte toplanan gördüğünüzden emin olun.

Yerel olarak toplanan günlüklerini görmüyorum ve ana bilgisayar veri oluşturuyor zaten doğruladıktan büyük olasılıkla bir yapılandırma sorunu varsa. Yapılandırmanıza uygun bölüm için dikkatle gözden geçirin. Ayrıca MonitoringAgent için oluşturulan yapılandırmasını gözden geçirmek [MaConfig.xml](#log-artifacts-path) ve olduğunu denetleyin ilgili günlük kaynağını açıklayan bazı bölüm ve azure tanılama yapılandırması arasında çevirisini kaybolmamasını ve İzleme Aracısı yapılandırması.
#### <a name="is-data-getting-transferred"></a>Veri aktarılır:
Verileri yerel olarak yakalanır ancak onu hala depolama hesabınızdaki göremiyorsanız doğruladıysanız: 
- Öncelikle, doğru depolama hesabı sağladığınız ve, anahtarları etc.for belirtilen depolama hesabı toplu olmayan emin olun. Bulut Hizmetleri için bazen kimliğinizi kişiler güncelleştirmemeniz bkz kendi `useDevelopmentStorage=true`.
- Depolama hesabının doğru olduğundan sağladıysanız. Genel depolama uç noktaları ulaşması bileşenleri izin verme bazı ağ kısıtlamaları sahip olmadığından emin olun. Bunu yapmanın bir yolu makinede Uzak Masaüstü ve bir şey için aynı depolama hesabındaki kendiniz yazmak deneyin.
- Son olarak, deneyin ve hangi hata izleme aracısı tarafından rapor bakın. İzleme Aracısı günlüklerinin Yazar `maeventtable.tsf` bulunan [Tanılama verileri için yerel deposu](#log-artifacts-path). ' Ndaki yönergeleri izleyin [yerel günlük ayıklama](#local-log-extraction) bu dosyayı açın ve deneyin ve olup olmadığını anlamasına bölüm `errors` yerel dosyaları okumak veya depolama alanına yazmak için hatalarını gösteren.

### <a name="capturing--archiving-logs"></a>Yakalama / günlükleri arşivleme
Yukarıdaki adımları oluştu ancak ne yanlış ve destek hakkında düşünmeye tahmin edebileceği değil. Bunlar isteyebilir ilk şey, makinenizden günlükleri toplamaktır. Bu kendiniz yaparak zamandan tasarruf edebilirsiniz. Çalıştırma `CollectGuestLogs.exe` adresindeki yardımcı programı [günlük toplama yardımcı programının yolu](#log-artifacts-path) ve tüm ilgili azure günlüklerini zip dosyasıyla aynı klasöre oluşturur.

## <a name="diagnostics-data-tables-not-found"></a>Tanılama veri tabloları bulunamadı
ETW olayları tutan Azure depolama tablolarda, aşağıdaki kodu kullanarak adlandırılır:

```C#
        if (String.IsNullOrEmpty(eventDestination)) {
            if (e == "DefaultEvents")
                tableName = "WADDefault" + MD5(provider);
            else
                tableName = "WADEvent" + MD5(provider) + eventId;
        }
        else
            tableName = "WAD" + eventDestination;
```

Örnek aşağıda verilmiştir:

```XML
        <EtwEventSourceProviderConfiguration provider="prov1">
          <Event id="1" />
          <Event id="2" eventDestination="dest1" />
          <DefaultEvents />
        </EtwEventSourceProviderConfiguration>
        <EtwEventSourceProviderConfiguration provider="prov2">
          <DefaultEvents eventDestination="dest2" />
        </EtwEventSourceProviderConfiguration>
```
```JSON
"EtwEventSourceProviderConfiguration": [
    {
        "provider": "prov1",
        "Event": [
            {
                "id": 1
            },
            {
                "id": 2,
                "eventDestination": "dest1"
            }
        ],
        "DefaultEvents": {
            "eventDestination": "DefaultEventDestination",
            "sinks": ""
        }
    },
    {
        "provider": "prov2",
        "DefaultEvents": {
            "eventDestination": "dest2"
        }
    }
]
```
4 tabloları oluşturan:

| Olay | Tablo adı |
| --- | --- |
| Sağlayıcı "prov1" = &lt;olay kimliği = "1" /&gt; |WADEvent + MD5("prov1") + "1" |
| Sağlayıcı "prov1" = &lt;olay kimliği "2" eventDestination = "dest1" = /&gt; |WADdest1 |
| Sağlayıcı "prov1" = &lt;DefaultEvents /&gt; |WADDefault+MD5("prov1") |
| Sağlayıcı "prov2" = &lt;DefaultEvents eventDestination "dest2" = /&gt; |WADdest2 |

## <a name="references"></a>Başvurular

### <a name="how-to-check-diagnostics-extension-configuration"></a>Tanılama uzantı yapılandırmasını denetleme
Uzantı yapılandırmanızı http://resources.azure.com için gitmek için denetlemek için en kolay yolu gidin sanal makine veya Bulut hizmeti, Azure tanılama uzantısını (IaaSDiagnostics / PaaDiagnostics) şüphe duyuluyor.

Alternatif olarak, makine ve Azure tanılama yapılandırma dosyası bakmak, Uzak Masaüstü'nü uygun bölümünde açıklanan [burada](#log-artifacts-path).

İçin büyük/küçük harf ya da aramada **Microsoft.Azure.Diagnostics** ardından **xmlCfg** veya **WadCfg** alan. 

WadCfg alan varsa, sanal makineleri durumunda, bu yapılandırma JSON'de anlamına gelir. XmlCfg alan varsa, bu yapılandırma XML'dir ve Base64 ile kodlanmış anlamına gelir. Yapmanız [çözülmesi](http://www.bing.com/search?q=base64+decoder) altyapınıza yüklendi XML görmek için.

Disk, yapılandırmasından çekme bulut hizmeti rolü için verileri base64 ile kodlanmış gerekir böylece ise [çözülmesi](http://www.bing.com/search?q=base64+decoder) altyapınıza yüklendi XML görmek için.

### <a name="azure-diagnostics-plugin-exit-codes"></a>Azure tanılama eklentisi çıkış kodları
Eklentisi aşağıdaki çıkış kodlarını döndürür:

| Çıkış kodu | Açıklama |
| --- | --- |
| 0 |Başarılı. |
| -1 |Genel hata. |
| -2 |Rcf dosyası yüklenemiyor.<p>Konuk Aracısı eklentisi Başlatıcısı'nı el ile yanlış, VM çağrılırsa, bu dahili bir hata yalnızca gerçekleşmelidir. |
| -3 |Tanılama yapılandırma dosyası yüklenemiyor.<p><p>Çözüm: nedeni, şema doğrulaması geçirme olmayan bir yapılandırma dosyası. Çözüm, şemasıyla uyumlu bir yapılandırma dosyası sağlamaktır. |
| -4 |Tanılama İzleme Aracısı başka bir örneği zaten yerel kaynak dizini kullanıyor.<p><p>Çözüm: için farklı bir değer belirtin **LocalResourceDirectory**. |
| -6 |Konuk Aracısı eklentisi Başlatıcısı geçersiz bir komut satırıyla tanılama başlatma girişiminde bulunuldu.<p><p>Konuk Aracısı eklentisi Başlatıcısı'nı el ile yanlış, VM çağrılırsa, bu dahili bir hata yalnızca gerçekleşmelidir. |
| -10 |Tanılama eklentisi işlenmeyen bir özel durum ile çıkıldı. |
| -11 |Konuk Aracısı işlemi başlatma ve İzleme Aracısı'nı izleme sorumlu oluşturamadı.<p><p>Çözüm: yeterli sistem kaynaklarının yeni işlemleri başlatmak kullanılabilir olduğundan emin olun.<p> |
| -101 |Tanılama eklentisi çağrılırken geçersiz bağımsız değişkenler.<p><p>Konuk Aracısı eklentisi Başlatıcısı'nı el ile yanlış, VM çağrılırsa, bu dahili bir hata yalnızca gerçekleşmelidir. |
| -102 |Eklentisi olarak kendisi başlatamadı işlemidir.<p><p>Çözüm: yeterli sistem kaynaklarının yeni işlemleri başlatmak kullanılabilir olduğundan emin olun. |
| -103 |Eklentisi olarak kendisi başlatamadı işlemidir. Özellikle Günlükçü nesnesini oluşturamadı.<p><p>Çözüm: yeterli sistem kaynaklarının yeni işlemleri başlatmak kullanılabilir olduğundan emin olun. |
| -104 |Konuk aracısı tarafından sağlanan rcf dosyası yüklenemiyor.<p><p>Konuk Aracısı eklentisi Başlatıcısı'nı el ile yanlış, VM çağrılırsa, bu dahili bir hata yalnızca gerçekleşmelidir. |
| -105 |Tanılama eklentisi tanılama yapılandırma dosyası açılamıyor.<p><p>Tanılama eklentisini el ile yanlış, VM çağrılırsa, bu dahili bir hata yalnızca gerçekleşmelidir. |
| -106 |Tanılama yapılandırma dosyası okunamıyor.<p><p>Çözüm: nedeni, şema doğrulaması geçirme olmayan bir yapılandırma dosyası. Bu nedenle uyumlu bir yapılandırma dosyası şeması ile sağlamak için çözümüdür. Bkz: [tanılama uzantı yapılandırmasını denetleme](#how-to-check-diagnostics-extension-configuration). |
| -107 |İzleme Aracısı kaynak directory geçişine geçersiz.<p><p>İzleme Aracısı'nı el ile yanlış, VM çağrılırsa, bu dahili bir hata yalnızca gerçekleşmelidir.</p> |
| -108 |İzleme Aracısı yapılandırma dosyasına tanılama yapılandırma dosyası dönüştürülemiyor.<p><p>Tanılama eklentisini el ile geçersiz bir yapılandırma dosyası ile çağrılırsa, bu dahili bir hata yalnızca gerçekleşmelidir. |
| -110 |Genel tanılama yapılandırma hatası.<p><p>Tanılama eklentisini el ile geçersiz bir yapılandırma dosyası ile çağrılırsa, bu dahili bir hata yalnızca gerçekleşmelidir. |
| -111 |İzleme Aracısı başlatılamadı.<p><p>Çözüm: yeterli sistem kaynaklarının kullanılabilir olduğundan emin olun. |
| -112 |Genel hata |

### <a name="local-log-extraction"></a>Yerel günlük ayıklama
İzleme Aracısı günlükleri ve yapı olarak toplayan `.tsf` dosyaları. `.tsf`Dosya okunabilir değildir ancak içine dönüştürebilirsiniz bir `.csv` gibi: 

```
<Azure diagnostics extension package>\Monitor\x64\table2csv.exe <relevantLogFile>.tsf
```
Yeni bir dosya olarak adlandırılan `<relevantLogFile>.csv` ilgili olarak aynı yol içinde oluşturulacak `.tsf` dosya.

**Not**: Bu yardımcı programı ana tsf dosyasını (örn., PerformanceCountersTable.tsf) karşı çalıştırmak yeterlidir. Eşlik eden dosyaları (örn., PerformanceCountersTables_\*\*001.tsf, PerformanceCountersTables_\*\*002. tsf vb.) otomatik olarak işlenir.

### <a name="more-about-trace-logs-missing"></a>Eksik izleme günlükleri hakkında daha fazla bilgi

**Not:** yalnızca Iaas VM üzerinde çalışan bir uygulama üzerinde DiagnosticsMonitorTraceListener yapılandırmadıysanız bu çoğunlukla bulut Hizmetleri için geçerlidir. 

- DiagnosticMonitorTraceListener web.config veya app.config yapılandırıldığından emin olun.  Bu bulut hizmeti projelerinde varsayılan olarak yapılandırılır, ancak bazı müşteriler tarafından tanılama değil toplanacak izleme deyimleri neden olur, çıkışı açıklama. 
- Günlükleri çalıştırın veya OnStart yönteminden yazılmaz DiagnosticMonitorTraceListener App.config dosyasının içinde olduğundan emin olun.  Varsayılan olarak, web.config dosyasında olmakla birlikte, yalnızca içinde w3wp.exe çalışan kodu uygular; Bu nedenle WaIISHost.exe içinde çalışan izlemelerini yakalama App.Config'de gerekir.
- Diagnostics.Debug.WriteXXX yerine Diagnostics.Trace.TraceXXX kullandığınızdan emin olun.  Hata ayıklama bildirimlerini kaldırılacak yayın derlemeden.
- (Reflector, ildasm veya doğrulamak için ILSpy kullanın) Diagnostics.Trace satırları gerçekte derlenmiş kod olduğundan emin olun.  İzleme koşullu derleme simgenin kullanmadığınız sürece Diagnostics.Trace komutları derlenmiş ikili dosyadan kaldırılır.  MSBuild Projesi derlemek için kullanılıyorsa, ardından bu içine çalıştırmak için yaygın görülen bir sorundur.

## <a name="known-issues-and-mitigations"></a>Bilinen sorunlar ve bunları azaltmanın yollarını
Bilinen Azaltıcı Etkenler ile ilgili bilinen sorunların listesi aşağıdadır:

**1. .NET 4.5 bağımlılık:**

WAD, .NET 4.5 framework veya üzeri bir çalışma zamanı bağımlılık vardır. Bu yazma zamanında tüm resmi azure sanal makine temel görüntülerinin yanı sıra bulut Hizmetleri için sağlanan tüm makineler .NET 4.5 veya üzerinde yüklü. Hala .NET 4.5 olmayan bir makinede veya yukarıdaki WAD çalıştırmayı deneyin olduğu bir durumda güden ancak mümkün. Bu, makinenize bir eski görüntü veya anlık görüntü dışına oluşturmak ortaya çıkar; veya kendi özel disk getirin.

Bu genellikle bir çıkış kodu olarak bildirimleri **255** DiagnosticsPluginLauncher.exe çalışırken. İşlenmeyen özel durum nedeniyle başarısız olur: 
```
System.IO.FileLoadException: Could not load file or assembly 'System.Threading.Tasks, Version=1.5.11.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' or one of its dependencies
```

**Azaltma:** .NET 4.5 veya üstü makinenize yükleyin.

**2. Performans sayaçları verileri kullanılabilir depolama ancak portalında gösterilmiyor**

Sanal makineler portal deneyimi, varsayılan olarak belirli performans sayaçlarını gösterir. Depolama alanında kullanılabilir olduğundan bunları görmüyorum ve biliyorsanız veri oluşturulan. Denetleme:
- Depolama verileri İngilizce sayaç adı varsa. Sayaç adları İngilizce değilse, portal ölçüm grafik tanıması mümkün olmaz.
- Joker karakterler kullanıyorsanız (\*), performans sayacı adlarını portal yapılandırılmış ve toplanan sayaç ilişkilendirmek mümkün olmaz.

**Azaltma**: makinenin dil İngilizce'ye sistem hesapları için değiştirin. Denetim Masası -> bölge Yönetim -> kopyalama ayarlar -> -> özel dil sistem hesabına uygulanmamış böylece "Hoş Geldiniz ekranı ve sistem hesapları" seçeneğinin işaretini kaldırın. Ayrıca, portal birincil tüketim deneyiminizi olmasını istiyorsanız joker karakterler kullanmayın emin olun.
