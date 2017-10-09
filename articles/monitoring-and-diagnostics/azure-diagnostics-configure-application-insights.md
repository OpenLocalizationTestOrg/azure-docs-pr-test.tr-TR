---
title: "aaaConfigure Azure tanılama toosend veri tooApplication Insights | Microsoft Docs"
description: "Hello Azure tanılama genel yapılandırması toosend veri tooApplication Öngörüler güncelleştirin."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: f9e12c3e-c307-435e-a149-ef0fef20513a
ms.service: monitoring-and-diagnostics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/19/2016
ms.author: robb
ms.openlocfilehash: 7c36f29da8fdc12fa58c17458348a311b900b0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-tooapplication-insights"></a>Bulut hizmeti, sanal makine ya da Service Fabric tanılama veri tooApplication Öngörüler Gönder
Bulut Hizmetleri, sanal makineler, sanal makine ölçek kümeleri ve Service Fabric tüm hello Azure tanılama uzantısını toocollect verileri kullanın.  Azure Tanılama verileri tooAzure depolama tabloları gönderir.  Ancak, ayrıca tüm kanal veya bir alt kümesini hello veri tooother konumları 1.5 veya daha sonra Azure tanılama uzantısını kullanarak erişebilirsiniz.

Bu makalede, Azure tanılama uzantısını tooApplication Öngörüler toosend verileri nasıl hello açıklanmaktadır.

## <a name="diagnostics-configuration-explained"></a>Açıklanan tanılama yapılandırması
Tanılama verileri nerede Gönder ek konumlarının Azure tanılama sunulan uzantısı 1.5 havuzlarını hello.

Bir havuz örnek yapılandırma Application Insights için:

```XML
<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "ApplicationInsights",
            "ApplicationInsights": "{Insert InstrumentationKey}",
            "Channels": {
                "Channel": [
                    {
                        "logLevel": "Error",
                        "name": "MyTopDiagData"
                    },
                    {
                        "logLevel": "Error",
                        "name": "MyLogData"
                    }
                ]
            }
        }
    ]
}
```
- Merhaba **havuz** *adı* hello havuzu benzersiz olarak tanımlayan bir dize değeri bir özniteliktir.

- Merhaba **Applicationınsights** öğesi hello hello Azure Tanılama verileri nerede gönderilir uygulama Öngörüler kaynak izleme anahtarını belirtir.
    - Varolan bir Application Insights kaynağı sahip değilseniz, bkz: [yeni bir Application Insights kaynağı oluşturma](../application-insights/app-insights-create-new-resource.md) kaynak oluşturma ve hello izleme anahtarı alma hakkında daha fazla bilgi.
    - Bir bulut hizmeti Azure SDK 2.8 ve daha sonra geliştiriyorsanız, bu izleme anahtarını otomatik olarak doldurulur. Merhaba değeri hello üzerinde temel **appınsıghts_ınstrumentatıonkey** hello Cloud Service projesi paketleme, hizmet yapılandırma ayarı. Bkz: [bulut hizmeti kullanım Application Insights'a Azure tanılama tootroubleshoot sorunları](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).

- Merhaba **kanalları** öğesi içeren bir veya daha fazla **kanal** öğeleri.
    - Merhaba *adı* özniteliği benzersiz olarak toothat kanal başvuruyor.
    - Merhaba *loglevel* özniteliği kanal hello hello günlük düzeyi verir belirtmenize olanak sağlar. Çoğu tooleast bilgi sırasına Hello kullanılabilir günlük düzeyleri şunlardır:
        - Ayrıntılı
        - Bilgi
        - Uyarı
        - Hata
        - Kritik

Bir kanal bir filtre gibi davranır ve tooselect belirli günlük düzeyleri toosend toohello hedef havuz sağlar. Örneğin, ayrıntılı günlükleri toplamak ve toostorage Gönder ancak yalnızca hataları toohello havuz Gönder.

Merhaba aşağıdaki grafikte bu ilişkiyi gösterir.

![Tanılama genel yapılandırması](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

Grafiği aşağıdaki hello hello yapılandırma değerlerini ve nasıl çalıştığını özetler. Merhaba hiyerarşideki farklı düzeylerde hello yapılandırmasında birden çok havuzlarını içerebilir. en üst düzeyinde hello Hello havuz genel ayar olarak davranır ve hello bir hello tek tek öğesi bir geçersiz kılma toothat genel ayar gibi davranır belirtilmiş.

![Tanılama yapılandırması Application Insights ile iç havuzlar](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a>Tam havuz yapılandırma örneği
İşte hello genel yapılandırmasının tam bir örnek dosya
1. tüm hataları tooApplication Öngörüler gönderir (Merhaba sırasında belirtilen **DiagnosticMonitorConfiguration** düğüm)
2. Ayrıca hello uygulama günlükleri için ayrıntılı düzeyi günlüklerini gönderir (Merhaba sırasında belirtilen **günlükleri** düğüm).

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent toothis channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent toothis channel -->
  </DiagnosticMonitorConfiguration>

<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
  </SinksConfig>
</WadCfg>
```
```JSON
"WadCfg": {
    "DiagnosticMonitorConfiguration": {
        "overallQuotaInMB": 4096,
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent toothis channel",
        "DiagnosticInfrastructureLogs": {
        },
        "PerformanceCounters": {
            "PerformanceCounterConfiguration": [
                {
                    "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                    "sampleRate": "PT3M"
                },
                {
                    "counterSpecifier": "\\Memory\\Available MBytes",
                    "sampleRate": "PT3M"
                }
            ]
        },
        "WindowsEventLog": {
            "scheduledTransferPeriod": "PT1M",
            "DataSource": [
                {
                    "name": "Application!*"
                }
            ]
        },
        "Logs": {
            "scheduledTransferPeriod": "PT1M",
            "scheduledTransferLogLevelFilter": "Verbose",
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent toothis channel"
        }
    },
    "SinksConfig": {
        "Sink": [
            {
                "name": "ApplicationInsights",
                "ApplicationInsights": "{Insert InstrumentationKey}",
                "Channels": {
                    "Channel": [
                        {
                            "logLevel": "Error",
                            "name": "MyTopDiagData"
                        },
                        {
                            "logLevel": "Verbose",
                            "name": "MyLogData"
                        }
                    ]
                }
            }
        ]
    }
}
```
Merhaba önceki yapılandırmada satırlardan hello hello anlamları şu olabilir:

### <a name="send-all-hello-data-that-is-being-collected-by-azure-diagnostics"></a>Azure tanılama tarafından toplanan tüm hello verileri gönder

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-toohello-application-insights-sink"></a>Yalnızca hata günlükleri toohello Application Insights havuz Gönder

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-tooapplication-insights"></a>Ayrıntılı uygulama tooApplication Öngörüler günlüklerini Gönder

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a>Sınırlamalar

- **Kanallar yalnızca türü ve değil performans sayaçlarını günlüğe kaydeder.** Bir performans sayacı öğesi ile bir kanal belirtirseniz, yoksayılır.
- **Merhaba günlük düzeyi için bir kanal tarafından Azure tanılama toplanmakta için hello günlük düzeyi aşamaz.** Örneğin, uygulama günlüğüne hataları hello günlükleri öğesindeki toplamak ve toosend ayrıntılı günlükleri toohello uygulama Insight havuz deneyin. Merhaba *scheduledTransferLogLevelFilter* özniteliği gerekir her zaman toplamak eşit veya hello günlükleri çok daha fazla günlükleri toosend tooa havuz çalışıyorsunuz.
- **Azure tanılama uzantısını tooApplication Insights tarafından toplanan blob verileri gönderemez.** Örneğin, hello altında belirtilen hiçbir şey *dizinleri* düğümü. Merhaba gerçek kilitlenme dökümü kilitlenme dökümleri tooblob depolama gönderilir ve yalnızca kilitlenme döküm hello bir bildirim oluşturulan tooApplication Öngörüler gönderilir.

## <a name="next-steps"></a>Sonraki Adımlar
* Nasıl çok öğrenin[Azure tanılama bilgilerinizi görüntülemek](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) Application ınsights'ta.
* Kullanım [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello uygulamanız için Azure tanılama uzantısını.
* Kullanım [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello uygulamanız için Azure tanılama uzantısını
