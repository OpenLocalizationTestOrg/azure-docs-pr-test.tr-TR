---
title: "aaaTroubleshooting Azure tanılama | Microsoft Docs"
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
ms.openlocfilehash: daaf9fa4c40982eb9ba04030d7e8ea1ad9fe085b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-troubleshooting"></a>Azure tanılama sorunlarını giderme
Sorun giderme bilgileri ilgili toousing Azure tanılama. Azure Tanılama hakkında daha fazla bilgi için bkz: [Azure tanılama genel bakış](azure-diagnostics.md).

## <a name="logical-components"></a>Mantıksal bileşenleri
**Tanılama eklentisi Başlatıcısı (DiagnosticsPluginLauncher.exe)**: hello Azure tanılama uzantısını başlatır. Noktası işleminin hello girdi olarak görevi görür.

**Tanılama Eklentisi (DiagnosticsPlugin.exe)**: Yukarıdaki hello başlatıcısı tarafından başlatılır ve hello İzleme Aracısı yapılandırır, başlatılır ve yaşam süresi yöneten ana işlem. 

**İzleme aracısını (MonAgent\*.exe işlemler)**: Bu işlemleri toplu hello iş hello; yani, izleme, koleksiyon ve aktarımını tanılama verilerini hello.  

## <a name="logartifact-paths"></a>Günlük/yapı yolları
Merhaba yolları toosome önemli günlükleri ve yapıları aşağıda verilmiştir. Biz toothese hello belgenin hello kalan boyunca başvuran tutun:
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
Azure tanılama Azure Portalı'nda görüntülenen ölçüm verileri bir dizi sağlar. Bu verileri portalında görmesini sorunları varsa, onay hello tanılama depolama hesabı -> WADMetrics\* hello karşılık gelen ölçüm kayıtlar varsa toosee tablo. Burada, hello Merhaba tablonun PartitionKey hello kaynak Kimliğini sanal makine veya sanal makine ölçek kümesini ve hello RowKey hello ölçüm adı yani performans sayacı adı.

Merhaba kaynak kimliği yanlış ise, onay tanılama yapılandırması -> ölçümleri hello kaynak kimliği doğru olarak ayarlanmış olsa ResourceId toosee ->.

Merhaba belirli ölçüm için hiçbir veri varsa, onay tanılama yapılandırması -> PerformanceCounter toosee hello ölçüm (performans sayacı) dahil edilmesi durumunda. Varsayılan olarak sayaçları aşağıdaki hello etkinleştiririz.
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

Merhaba yapılandırma doğru olarak ayarlanmış, ancak yine de hello ölçüm verileri göremiyorsanız, hello daha fazla araştırma için aşağıda hello yönergeleri izleyin.


## <a name="azure-diagnostics-is-not-starting"></a>Azure tanılama başlatılıyor değil
Bakmak **DiagnosticsPluginLauncher.log** ve **DiagnosticsPlugin.log** hello hello konumunu dosyalarından günlük dosyaları yukarıdaki neden hakkında bilgi için tanılama toostart başarısız sağlanan. 

Bu günlükler gösteriyorsa `Monitoring Agent not reporting success after launch`, MonAgentHost.exe başlatma bir hata oluştu anlamına gelir. Konum hello günlüklerine için başlangıç konumu için belirtilen `MonAgentHost log file` yukarıdaki hello bölümünde.

Merhaba günlük dosyalarını son satırının Hello hello çıkış kodu içerir.  

```
DiagnosticsPluginLauncher.exe Information: 0 : [4/16/2016 6:24:15 AM] DiagnosticPlugin exited with code 0
```
Görürseniz bir **negatif** çıkış kodu, toohello başvuran [çıkış kodu tablosu](#azure-diagnostics-plugin-exit-codes) hello içinde [başvurular](#references).

## <a name="diagnostics-data-is-not-logged-tooazure-storage"></a>Tanılama verilerini günlüğe tooAzure depolama olduğu
Hiçbir veri gösteren veya yalnızca bazı hello verileri değil gösteren belirleyin.

### <a name="diagnostics-infrastructure-logs"></a>Tanılama altyapı günlükleri
Tanılama altyapı günlükleri, burada içine çalıştıran herhangi bir hata azure tanılama günlükleri ' dir. Etkinleştirdiğinizden emin olun ([nasıl yapılır?](#how-to-check-diagnostics-extension-configuration)) yapılandırmanızda tanılama altyapı günlükleri, yakalama ve hızlı bir şekilde hello görünmesini ilgili hataları arayın `DiagnosticInfrastructureLogsTable` yapılandırılan depolama hesabınızdaki tablo.

### <a name="no-data-is-showing-up"></a>Hiçbir veri gösterme
Merhaba en yaygın tamamen eksik olay verileri hatalı tanımlanmış bir depolama hesabı bilgilerini nedenidir.

Çözüm: Tanılama yapılandırmanızı düzeltin ve tanılama yeniden yükleyin.

Merhaba depolama hesabı ise, doğru yapılandırıldığını, Uzak Masaüstü hello makine ve yapma emin DiagnosticsPlugin.exe ve MonAgentCore.exe çalışır. Bunlar çalışmıyorsa izleyin [Azure tanılama başlamıyor](#azure-diagnostics-is-not-starting). Merhaba işlemler çalıştırıyorsanız, çok bağlantı[yerel olarak yakalanan veri](#is-data-getting-captured-locally) ve bu kılavuzda buradan izleyin.

### <a name="part-of-hello-data-is-missing"></a>Merhaba verilerin bölümü eksik
Bazı veriler alıyorsanız, ancak diğer değil. Bu hello veri toplama anlamına gelir / aktarım ardışık doğru olarak ayarlanmış. Merhaba alt bölümleri izleyin hangi hello sorunu aşağı toonarrow şöyledir:
#### <a name="is-collection-configured"></a>Koleksiyon yapılandırılır: 
Tanılama yapılandırması toplanan verileri toobe belirli bir tür için bildirir hello bölümü içerir. [Yapılandırmanızı gözden](#how-to-check-diagnostics-extension-configuration) toomake, değil görmek için verileri, emin yapılandırılmamış koleksiyonu için.
#### <a name="is-hello-host-generating-data"></a>Merhaba ana bilgisayar veri oluşturuluyor:
- **Performans sayaçları**: perfmon açın ve hello sayacını denetleyin.
- **İzleme günlükleri**: Uzak Masaüstü uygulamasına VM hello ve olmalıdır toohello uygulamanın yapılandırma dosyasını ekleyin.  Merhaba metin dinleyicisi yukarı http://msdn.microsoft.com/library/sk36c28t.aspx tooset bakın.  Merhaba emin olun `<trace>` öğeye sahip `<trace autoflush="true">`.<br />
Oluşturulan izleme günlükleri görmüyorsanız izleyin [daha hakkında günlükleri izleme eksik](#more-about-trace-logs-missing).
- **ETW izlemeleri**: hello VM içine, Uzak Masaüstü'nü ve yükleme PerfView.  Çalışma Dosya -> PerfView içinde kullanıcı komutu -> dinleme etwprovder1, etwprovider2 vb..  Merhaba dinleme komutu büyük/küçük harfe duyarlıdır ve hello virgülle ayrılmış listesini ETW sağlayıcılar arasında boşluk olamaz unutmayın.  Toorun Hello komutu başarısız olursa hello-sağ alt denenen toorun ve hangi hello sonuç neydi hello Perfview aracı toosee hello 'Günlük' düğmesini tıklatabilirsiniz.  Merhaba giriş yeni bir pencere yukarı ve birkaç saniye sonra pop doğru olduğunu varsayarak ETW izlemeleri görmesini başlar.
- **Olay günlükleri**: Uzak Masaüstü hello VM başlatın. Açık `Event Viewer` ve hello olayları mevcut emin olun.
#### <a name="is-data-getting-captured-locally"></a>Verileri yerel olarak yakalanan:
Sonraki hello verileri yerel olarak yakalanır emin olun.
Merhaba veri depolanan yerel olarak `*.tsf` dosyalar [hello yerel depolama için tanılama veri](#log-artifacts-path). Farklı türde günlüklerini toplanan farklı `.tsf` dosyaları. Merhaba benzer toohello tablo adları azure depolama alanında adlardır. Örneğin `Performance Counters` içinde toplanan alma `PerformanceCountersTable.tsf`, olay günlüklerini toplanan `WindowsEventLogsTable.tsf`. Merhaba yönergeleri kullanın [yerel günlük ayıklama](#local-log-extraction) bölümünde tooopen hello yerel koleksiyon dosyaları ve bunları diskte toplanan gördüğünüzden emin olun.

Yerel olarak toplanan günlüklerine bakın yoksa ve zaten hello ana verileri oluşturma, yapılandırma sorunu büyük olasılıkla sahip doğrulandı. Yapılandırmanızı hello uygun bölüm için dikkatle gözden geçirin. Ayrıca MonitoringAgent için oluşturulan hello yapılandırmasını gözden geçirmek [MaConfig.xml](#log-artifacts-path) ve hello ilgili günlük kaynak ve bunu azure tanılama yapılandırması arasında çevirisini kaybolmamasını açıklayan bazı bölümü olduğundan emin olun ve İzleme Aracısı yapılandırması.
#### <a name="is-data-getting-transferred"></a>Veri aktarılır:
Merhaba verileri yerel olarak yakalanır ancak onu hala depolama hesabınızdaki göremiyorsanız doğruladıysanız: 
- Öncelikle, doğru depolama hesabı sağladığınız ve, depolama hesabı verilen anahtarları etc.for hello alındı olmayan emin olun. Bulut Hizmetleri için bazen kimliğinizi kişiler güncelleştirmemeniz bkz kendi `useDevelopmentStorage=true`.
- Depolama hesabının doğru olduğundan sağladıysanız. Merhaba bileşenleri tooreach genel depolama uç noktaları izin verme bazı ağ kısıtlamaları sahip olmadığından emin olun. Merhaba tooremote Desktop'a olan tek yönlü toodo makine ve toowrite bir şey toohello deneyin aynı depolama hesabı kendiniz.
- Son olarak, deneyin ve hangi hata izleme aracısı tarafından rapor bakın. İzleme Aracısı günlüklerinin Yazar `maeventtable.tsf` bulunan [hello yerel depolama için tanılama veri](#log-artifacts-path). ' Ndaki yönergeleri izleyin [yerel günlük ayıklama](#local-log-extraction) tooopen bu dosyayı bölümünde deneyin ve olup olmadığını anlamasına `errors` hataları tooread yerel dosyaları belirten veya toostorage yazma.

### <a name="capturing--archiving-logs"></a>Yakalama / günlükleri arşivleme
Yukarıdaki adımları hello aracılığıyla oluştu ancak ne yanlış ve destek hakkında düşünmeye tahmin edebileceği değil. Merhaba ilk şey, isteyebilir makinenizden toocollect günlükleri ' dir. Bu kendiniz yaparak zamandan tasarruf edebilirsiniz. Merhaba çalıştırmak `CollectGuestLogs.exe` adresindeki yardımcı programı [günlük toplama yardımcı programının yolu](#log-artifacts-path) ve tüm ilgili azure günlüklerini zip dosyasıyla hello oluşturur aynı klasöre.

## <a name="diagnostics-data-tables-not-found"></a>Tanılama veri tabloları bulunamadı
ETW olayları tutan Azure depolama Hello tablolarda koddan hello kullanarak adlandırılır:

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

### <a name="how-toocheck-diagnostics-extension-configuration"></a>Nasıl toocheck tanılama uzantı yapılandırmasını
en kolay yolu toocheck hello uzantısı yapılandırmanızı toonavigate toohttp://resources.azure.com, toohello hangi hello Azure tanılama uzantısını üzerinde sanal makine veya Bulut hizmeti gidin (IaaSDiagnostics / PaaDiagnostics) şüphe duyuluyor.

Alternatif olarak, Uzak Masaüstü hello makine ve hello Azure tanılama yapılandırma dosyası bakma açıklanan hello uygun bölümünde [burada](#log-artifacts-path).

İçin büyük/küçük harf ya da aramada **Microsoft.Azure.Diagnostics** hello ardından **xmlCfg** veya **WadCfg** alan. 

Merhaba WadCfg alan varsa, sanal makineleri durumunda bunu hello config JSON'de anlamına gelir. Merhaba xmlCfg alan varsa, hello config XML'dir ve Base64 ile kodlanmış anlamına gelir. Çok ihtiyacınız[çözülmesi](http://www.bing.com/search?q=base64+decoder) toosee hello tanılama tarafından yüklenen XML.

Disk, hello yapılandırmasından çekme bulut hizmeti rolü için hello verileri base64 ile kodlanmış çok gerekir böylece ise[çözülmesi](http://www.bing.com/search?q=base64+decoder) toosee hello tanılama tarafından yüklenen XML.

### <a name="azure-diagnostics-plugin-exit-codes"></a>Azure tanılama eklentisi çıkış kodları
Merhaba eklentisi çıkış kodları aşağıdaki hello döndürür:

| Çıkış kodu | Açıklama |
| --- | --- |
| 0 |Başarılı. |
| -1 |Genel hata. |
| -2 |%S tooload hello rcf dosyası.<p>Merhaba Konuk Aracısı eklentisi Başlatıcısı el ile yanlış bir şekilde hello VM üzerinde çağrılırsa, bu dahili bir hata yalnızca gerçekleşmelidir. |
| -3 |Merhaba tanılama yapılandırma dosyası yüklenemiyor.<p><p>Çözüm: nedeni, şema doğrulaması geçirme olmayan bir yapılandırma dosyası. Merhaba, tooprovide hello şeması ile uyumlu bir yapılandırma dosyası çözümüdür. |
| -4 |İzleme Aracısı tanılama hello başka bir örneği zaten hello yerel kaynak dizini kullanıyor.<p><p>Çözüm: için farklı bir değer belirtin **LocalResourceDirectory**. |
| -6 |Geçersiz komut satırı ile toolaunch tanılama Hello Konuk Aracısı eklentisi Başlatıcısı çalıştı.<p><p>Merhaba Konuk Aracısı eklentisi Başlatıcısı el ile yanlış bir şekilde hello VM üzerinde çağrılırsa, bu dahili bir hata yalnızca gerçekleşmelidir. |
| -10 |Merhaba tanılama eklentisi işlenmeyen bir özel durum ile çıkıldı. |
| -11 |Merhaba Konuk Aracısı yüklenemiyor toocreate hello işlem başlatma ve İzleme Aracısı hello izleme sorumlu.<p><p>Çözüm: yeterli sistem kaynaklarının kullanılabilir toolaunch yeni işlemler olduğunu doğrulayın.<p> |
| -101 |Merhaba tanılama eklentisi çağrılırken geçersiz bağımsız değişkenler.<p><p>Merhaba Konuk Aracısı eklentisi Başlatıcısı el ile yanlış bir şekilde hello VM üzerinde çağrılırsa, bu dahili bir hata yalnızca gerçekleşmelidir. |
| -102 |Merhaba Eklenti yüklenemiyor tooinitialize kendisini bir işlemdir.<p><p>Çözüm: yeterli sistem kaynaklarının kullanılabilir toolaunch yeni işlemler olduğunu doğrulayın. |
| -103 |Merhaba Eklenti yüklenemiyor tooinitialize kendisini bir işlemdir. Özellikle oluşturulamıyor toocreate hello Günlükçü nesne değil.<p><p>Çözüm: yeterli sistem kaynaklarının kullanılabilir toolaunch yeni işlemler olduğunu doğrulayın. |
| -104 |Merhaba Konuk aracısı tarafından sağlanan oluşturulamıyor tooload hello rcf dosyası.<p><p>Merhaba Konuk Aracısı eklentisi Başlatıcısı el ile yanlış bir şekilde hello VM üzerinde çağrılırsa, bu dahili bir hata yalnızca gerçekleşmelidir. |
| -105 |Merhaba tanılama eklentisi hello tanılama yapılandırma dosyası açılamıyor.<p><p>Hello tanılama eklentisini el ile yanlış bir şekilde hello VM üzerinde çağrılırsa, bu dahili bir hata yalnızca gerçekleşmelidir. |
| -106 |Merhaba tanılama yapılandırma dosyası okunamıyor.<p><p>Çözüm: nedeni, şema doğrulaması geçirme olmayan bir yapılandırma dosyası. Bu nedenle tooprovide hello şeması ile uyumlu bir yapılandırma dosyası hello çözümüdür. Bkz: [nasıl toocheck tanılama uzantı yapılandırmasını](#how-to-check-diagnostics-extension-configuration). |
| -107 |İzleme Aracısı hello kaynak dizin geçişi toohello geçersiz.<p><p>İzleme Aracısı hello el ile yanlış bir şekilde hello VM üzerinde çağrılırsa, bu dahili bir hata yalnızca gerçekleşmelidir.</p> |
| -108 |%S tooconvert hello tanılama yapılandırma dosyasına hello Aracısı Yapılandırma dosyası izleme.<p><p>Merhaba tanılama eklentisini el ile geçersiz bir yapılandırma dosyası ile çağrılırsa, bu dahili bir hata yalnızca gerçekleşmelidir. |
| -110 |Genel tanılama yapılandırma hatası.<p><p>Merhaba tanılama eklentisini el ile geçersiz bir yapılandırma dosyası ile çağrılırsa, bu dahili bir hata yalnızca gerçekleşmelidir. |
| -111 |%S toostart hello İzleme Aracısı.<p><p>Çözüm: yeterli sistem kaynaklarının kullanılabilir olduğundan emin olun. |
| -112 |Genel hata |

### <a name="local-log-extraction"></a>Yerel günlük ayıklama
İzleme Aracısı hello toplar günlükleri ve yapı olarak `.tsf` dosyaları. `.tsf`Dosya okunabilir değildir ancak içine dönüştürebilirsiniz bir `.csv` gibi: 

```
<Azure diagnostics extension package>\Monitor\x64\table2csv.exe <relevantLogFile>.tsf
```
Yeni bir dosya olarak adlandırılan `<relevantLogFile>.csv` hello aynı oluşturulacak hello karşılık gelen olarak yolu `.tsf` dosya.

**Not**: toorun bu yardımcı program hello ana tsf dosyası (örn., PerformanceCountersTable.tsf) karşı yeterlidir. dosyaları eşlik hello (örn., PerformanceCountersTables_\*\*001.tsf, PerformanceCountersTables_\*\*002. tsf vb.) otomatik olarak işlenir.

### <a name="more-about-trace-logs-missing"></a>Eksik izleme günlükleri hakkında daha fazla bilgi

**Not:** yalnızca Iaas VM üzerinde çalışan bir uygulama üzerinde hello DiagnosticsMonitorTraceListener yapılandırmadıysanız bu çoğunlukla toocloud Hizmetleri için geçerlidir. 

- DiagnosticMonitorTraceListener hello web.config veya app.config yapılandırıldığından emin hello olun.  Bu bulut hizmeti projelerinde varsayılan olarak yapılandırılır, ancak bazı müşteriler, açıklama hello izleme deyimleri toonot neden olacak çıkış tanılama tarafından toplanan. 
- Günlükleri hello çalıştırın veya OnStart yönteminden yazılmaz DiagnosticMonitorTraceListener hello App.config dosyasının içinde olduğundan emin hello olun.  Merhaba web.config dosyasında varsayılandır tarafından ancak, yalnızca içinde w3wp.exe çalışan toocode uygulanır; Bu nedenle WaIISHost.exe içinde çalışan app.config toocapture izlemeleri de gerekir.
- Diagnostics.Debug.WriteXXX yerine Diagnostics.Trace.TraceXXX kullandığınızdan emin olun.  Merhaba hata ayıklama bildirimlerini kaldırılacak yayın derlemeden.
- Merhaba Diagnostics.Trace satırları (Reflector, ildasm veya ILSpy tooverify kullanın) gerçekte hello derlenmiş kod olduğundan emin olun.  Merhaba izleme koşullu derleme simgesi kullanmadığınız sürece Diagnostics.Trace komutları derlenmiş hello ikiliden kaldırılır.  MSBuild toobuild hello projesi kullanarak, bu yaygın bir sorun toorun içine olur.

## <a name="known-issues-and-mitigations"></a>Bilinen sorunlar ve bunları azaltmanın yollarını
Bilinen Azaltıcı Etkenler ile ilgili bilinen sorunların listesi aşağıdadır:

**1. .NET 4.5 bağımlılık:**

WAD, .NET 4.5 framework veya üzeri bir çalışma zamanı bağımlılık vardır. Bu yazma hello zaman tüm resmi azure sanal makine temel görüntülerinin yanı sıra bulut Hizmetleri için sağlanan tüm makineler .NET 4.5 veya üzerinde yüklü. Ancak hala olası tooland toorun WAD .NET 4.5 olmayan bir makine veya üzeri deneyin burada bir durumda değil. Bu, makinenize bir eski görüntü veya anlık görüntü dışına oluşturmak ortaya çıkar; veya kendi özel disk getirin.

Bu genellikle bir çıkış kodu olarak bildirimleri **255** DiagnosticsPluginLauncher.exe çalışırken. Toohello işlenmeyen özel durum başarısız olur: 
```
System.IO.FileLoadException: Could not load file or assembly 'System.Threading.Tasks, Version=1.5.11.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' or one of its dependencies
```

**Azaltma:** .NET 4.5 veya üstü makinenize yükleyin.

**2. Performans sayaçları verileri kullanılabilir depolama ancak portalında gösterilmiyor**

Sanal makineler portal deneyimi, varsayılan olarak belirli performans sayaçlarını gösterir. Bunları görmüyorsanız ve depolama alanında kullanılabilir olduğundan hello veri oluşturulan bilmek istiyorsanız. Denetleme:
- Depolama alanında Hello veriler İngilizce sayaç adı varsa. Merhaba sayaç adları İngilizce değilse, portal ölçüm grafik mümkün toorecognize olmaz.
- Joker karakterler kullanıyorsanız (\*), performans sayacı adlarını yapılandırılmış ve sayaç toplanan mümkün toocorrelate hello hello portal olmaz.

**Azaltma**: hello makinenin dil tooEnglish sistem hesapları için değiştirin. Denetim Masası -> bölge Yönetim -> kopyalama ayarlar -> -> merhaba özel dil olmaması "Hoş Geldiniz ekranı ve sistem hesapları" seçeneğinin işaretini kaldırın uygulanan toosystem hesabı. Ayrıca birincil tüketim deneyiminizi portal toobe istiyorsanız joker karakterler kullanmayın emin olun.
