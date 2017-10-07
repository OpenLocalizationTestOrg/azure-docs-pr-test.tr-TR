---
title: "aaaAzure tanılama uzantısı 1.3 ve sonraki yapılandırma şeması | Microsoft Docs"
description: "Şema sürümü 1.3 ve daha sonra Azure tanılama hello Microsoft Azure SDK 2.4 ve daha sonraki bir parçası olarak gönderilir."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: robb
ms.openlocfilehash: bd15d3a79ea818fcb3235854717e58d5da36518e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a>Azure tanılama 1.3 ve daha sonra yapılandırma şeması
> [!NOTE]
> Hello Azure tanılama uzantısını hello bileşen toocollect performans sayaçları ve diğer istatistiklerine kullanılır:
> - Azure Sanal Makineler 
> - Sanal Makine Ölçek Kümeleri
> - Service Fabric 
> - Cloud Services 
> - Ağ Güvenlik Grupları
> 
> Bu sayfa, yalnızca bu hizmetlerden biri kullanıyorsanız geçerlidir.

Bu sayfa sürümleri 1.3 ve daha yeni (Azure SDK 2.4 ve daha yeni) için geçerli değil. Yeni yapılandırma bölümlerinin eklendikleri hangi sürümünde açıklamalı tooshow ' dir.  

Merhaba tanılama başlatır izlediğinizde burada açıklanan hello yapılandırma kullanılan tooset tanılama yapılandırma ayarlarını dosyasıdır.  

Merhaba uzantısı Azure monitör, Application Insights ve günlük analizi gibi diğer Microsoft tanılama ürün ile birlikte kullanılır.



Merhaba ortak yapılandırma dosyası şeması tanımı hello aşağıdaki PowerShell komutunu yürüterek yükleyin:  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

Azure tanılama kullanma hakkında daha fazla bilgi için bkz: [Azure tanılama uzantısını](azure-diagnostics.md).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Merhaba tanılama yapılandırma dosyası örneği  
 Aşağıdaki örnek hello tipik tanılama yapılandırma dosyası gösterir:  

```xml  
<?xml version="1.0" encoding="utf-8"?>  
<DiagnosticsConfiguration  xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">   
  <PublicConfig>  
    <WadCfg>  
      <DiagnosticMonitorConfiguration overallQuotaInMB="10000">  

        <PerformanceCounters scheduledTransferPeriod="PT1M">  
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />  
        </PerformanceCounters>  

        <Directories scheduledTransferPeriod="PT5M">  
          <IISLogs containerName="iislogs" />  
          <FailedRequestLogs containerName="iisfailed" />  

          <DataSources>  
            <DirectoryConfiguration containerName="mynewprocess">  
              <Absolute path="C:\MyNewProcess" expandEnvironment="false" />  
            </DirectoryConfiguration>  
            <DirectoryConfiguration containerName="badapp">  
              <Absolute path="%SYSTEMDRIVE%\BadApp" expandEnvironment="true" />  
            </DirectoryConfiguration>  
            <DirectoryConfiguration containerName="goodapp">  
              <LocalResource name="Skippy" relativePath="..\PeanutButter"/>  
            </DirectoryConfiguration>  
          </DataSources>  

        </Directories>  

        <EtwProviders>  
          <EtwEventSourceProviderConfiguration   
                       provider="MyProviderClass"   
                       scheduledTransferPeriod="PT5M">  
            <Event id="0"/>  
            <Event id="1" eventDestination="errorTable"/>  
            <DefaultEvents />  
          </EtwEventSourceProviderConfiguration>  
          <EtwManifestProviderConfiguration provider="5974b00b-84c2-44bc-9e58-3a2451b4e3ad" scheduledTransferLogLevelFilter="Information" scheduledTransferPeriod="PT2M">  
            <Event id="0"/>  
            <DefaultEvents eventDestination="defaultTable"/>  
          </EtwManifestProviderConfiguration>  
        </EtwProviders>  

        <WindowsEventLog scheduledTransferPeriod="PT5M">  
          <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>  
          <DataSource name="System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]" />  
          <DataSource name="System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]" />  
        </WindowsEventLog>  

        <Logs  bufferQuotaInMB="1024"   
             scheduledTransferPeriod="PT1M"   
             scheduledTransferLogLevelFilter="Verbose"   
             sinks="ApplicationInsights.AppLogs"/>  <!-- sinks attribute added in 1.5 -->  

        <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
          <CrashDumpConfiguration processName="mynewprocess.exe" />  
          <CrashDumpConfiguration processName="badapp.exe"/>  
        </CrashDumps>  

        <DockerSources> <!-- Added in 1.9 --> 
          <Stats enabled="true" sampleRate="PT1M" scheduledTransferPeriod="PT1M" />
        </DockerSources>

      </DiagnosticMonitorConfiguration>  

      <SinksConfig>   <!-- Added in 1.5 -->  
        <Sink name="ApplicationInsights">   
          <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>   
          <Channels>   
            <Channel logLevel="Error" name="Errors"  />   
            <Channel logLevel="Verbose" name="AppLogs"  />   
          </Channels>   
        </Sink>   
        <Sink name="EventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryEventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryStorageAccount"> <!-- Added in 1.7 -->
          <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" />
        </Sink>
   </SinksConfig>

  </WadCfg>  

  <StorageAccount>diagstorageaccount</StorageAccount>
  <StorageType>TableAndBlob</StorageType> <!-- Added in 1.8 -->  
  </PublicConfig>  

  <PrivateConfig>  <!-- Added in 1.3 -->  
    <StorageAccount name="" key="" endpoint="" sasToken="{sas token}"  />  <!-- sasToken in Private config added in 1.8.1 -->  
    <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
   
    <SecondaryStorageAccounts>
       <StorageAccount name="secondarydiagstorageaccount" key="{base64 encoded key}" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
   
    <SecondaryEventHubs>
       <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
    </SecondaryEventHubs>

  </PrivateConfig>  
  <IsEnabled>true</IsEnabled>  
</DiagnosticsConfiguration>  

```  

Merhaba önceki XML yapılandırma dosyası denk JSON. 

json kullanımı genellikle farklı değişkenleri olarak geçirilen çünkü hello PublicConfig ve PrivateConfig ayrılır. Bu durumlar: Resource Manager şablonları, PowerShell ve Visual Studio sanal makine ölçek kümesi. 

```json
"PublicConfig" {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 10000,
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT1M",
                        "unit": "percent"
                    }
                ]
            },
            "Directories": {
                "scheduledTransferPeriod": "PT5M",
                "IISLogs": {
                    "containerName": "iislogs"
                },
                "FailedRequestLogs": {
                    "containerName": "iisfailed"
                },
                "DataSources": [
                    {
                        "containerName": "mynewprocess",
                        "Absolute": {
                            "path": "C:\\MyNewProcess",
                            "expandEnvironment": false
                        }
                    },
                    {
                        "containerName": "badapp",
                        "Absolute": {
                            "path": "%SYSTEMDRIVE%\\BadApp",
                            "expandEnvironment": true
                        }
                    },
                    {
                        "containerName": "goodapp",
                        "LocalResource": {
                            "relativePath": "..\\PeanutButter",
                            "name": "Skippy"
                        }
                    }
                ]
            },
            "EtwProviders": {
                "sinks": "",
                "EtwEventSourceProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT5M",
                        "provider": "MyProviderClass",
                        "Event": [
                            {
                                "id": 0
                            },
                            {
                                "id": 1,
                                "eventDestination": "errorTable"
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ],
                "EtwManifestProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT2M",
                        "scheduledTransferLogLevelFilter": "Information",
                        "provider": "5974b00b-84c2-44bc-9e58-3a2451b4e3ad",
                        "Event": [
                            {
                                "id": 0
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT5M",
                "DataSource": [
                    {
                        "name": "System!*[System[Provider[@Name='Microsoft Antimalware']]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Verbose",
                "sinks": "ApplicationInsights.AppLogs"
            },
            "CrashDumps": {
                "directoryQuotaPercentage": 30,
                "dumpType": "Mini",
                "containerName": "wad-crashdumps",
                "CrashDumpConfiguration": [
                    {
                        "processName": "mynewprocess.exe"
                    },
                    {
                        "processName": "badapp.exe"
                    }
                ]
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
                                "name": "Errors"
                            },
                            {
                                "logLevel": "Verbose",
                                "name": "AppLogs"
                            }
                        ]
                    }
                },
                {
                    "name": "EventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryEventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryStorageAccount",
                    "StorageAccount": {
                        "name": "secondarydiagstorageaccount",
                        "endpoint": "https://core.windows.net"
                    }
                }
            ]
        }
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```json
"PrivateConfig" {
    "storageAccountName": "diagstorageaccount",
    "storageAccountKey": "{base64 encoded key}",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "EventHub": {
        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    },
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "key": "{base64 encoded key}",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    },
    "SecondaryEventHubs": {
        "EventHub": [
            {
                "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                "SharedAccessKeyName": "SendRule",
                "SharedAccessKey": "{base64 encoded key}"
            }
        ]
    }
}

```

## <a name="reading-this-page"></a>Bu sayfa okuma  
 Merhaba aşağıdaki kabaca hello önceki örnekte gösterilen sırada etiketleridir.  Tam açıklama beklediğiniz burada görmüyorsanız, arama hello öğesi veya özniteliği için hello sayfası.  

## <a name="common-attribute-types"></a>Ortak öznitelik türleri  
 **scheduledTransferPeriod** özniteliği birkaç öğelerinde görüntülenir. Bu zamanlanmış aktarımları toostorage toohello minute en yakın yukarı yuvarlanmasını hello aralığını gösterir. Merhaba değeri bir [XML "Süre veri türü."](http://www.w3schools.com/schema/schema_dtypes_date.asp)


## <a name="diagnosticsconfiguration-element"></a>DiagnosticsConfiguration öğesi  
 *Ağaç: Kök - DiagnosticsConfiguration*

Sürüm 1.3 eklendi.  

Merhaba hello tanılama yapılandırma dosyasının en üst düzey öğesi.  

**Öznitelik** xmlns - hello tanılama yapılandırma dosyası için XML ad alanı hello:  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  


|Alt öğeler|Açıklama|  
|--------------------|-----------------|  
|**PublicConfig**|Gereklidir. Açıklama, bu sayfada başka bir yerde bakın.|  
|**PrivateConfig**|İsteğe bağlı. Açıklama, bu sayfada başka bir yerde bakın.|  
|**IsEnabled**|Boole değeri. Açıklama, bu sayfada başka bir yerde bakın.|  

## <a name="publicconfig-element"></a>PublicConfig öğesi  
 *Ağaç: Kök - DiagnosticsConfiguration - PublicConfig*

 Merhaba genel tanılama yapılandırması açıklar.  

|Alt öğeler|Açıklama|  
|--------------------|-----------------|  
|**WadCfg**|Gereklidir. Açıklama, bu sayfada başka bir yerde bakın.|  
|**StorageAccount**|hello Azure depolama hesabı toostore hello verilerde Hello adı. Ayrıca bir parametre olarak hello kümesi AzureServiceDiagnosticsExtension cmdlet'ini çalıştırırken belirtilebilir.|  
|**StorageType**|Olabilir *tablo*, *Blob*, veya *TableAndBlob*. Tablo varsayılandır. TableAndBlob seçildiğinde Tanılama verileri iki kez--tooeach türü kez yazılır.|  
|**LocalResourceDirectory**|Hello dizin hello sanal makineye burada hello Monitoring Agent olay verilerini depolar. Aksi takdirde, ayarlanırsa, hello varsayılan dizin kullanılır:<br /><br /> Worker/web rolü için:`C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`<br /><br /> Bir sanal makine için:`C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`<br /><br /> Gerekli öznitelikler şunlardır:<br /><br /> - **yol** - hello Azure tanılama tarafından kullanılan hello sistem toobe dizininde.<br /><br /> - **expandEnvironment** -ortam değişkenleri hello yol adında genişletilmiş olup olmadığını denetler.|  

## <a name="wadcfg-element"></a>WadCFG öğesi  
 *Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG*
 
 Tanımlar ve toplanan hello telemetri verileri toobe yapılandırır.  


## <a name="diagnosticmonitorconfiguration-element"></a>DiagnosticMonitorConfiguration öğesi 
 *Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*

 Gerekli 

|Öznitelikler|Açıklama|  
|----------------|-----------------|  
| **overallQuotaInMB** | Merhaba maksimum hello tarafından tüketilen yerel disk alanı miktarını çeşitli tanılama veri türlerine Azure tanılama tarafından toplanan. Merhaba varsayılan ayar 5120 MB'tır.<br />
|**useProxyServer** | IE ayarlarının kümesinde olarak Azure tanılama toouse hello proxy sunucusu ayarlarını yapılandırın.|  

<br /> <br />

|Alt öğeler|Açıklama|  
|--------------------|-----------------|  
|**CrashDumps**|Açıklama, bu sayfada başka bir yerde bakın.|  
|**DiagnosticInfrastructureLogs**|Azure tanılama tarafından oluşturulan günlükleri koleksiyonunu etkinleştirin. Merhaba Tanılama Altyapısı günlükleri hello tanılama sistem kendisini sorun giderme için yararlıdır. İsteğe bağlı öznitelikleri şunlardır:<br /><br /> - **scheduledTransferLogLevelFilter** -toplanan hello günlüklerini hello en düşük önem derecesi yapılandırır.<br /><br /> - **scheduledTransferPeriod** -toohello minute en yakın yuvarlanan zamanlanmış aktarımları toostorage hello aralığıdır. Merhaba değeri bir [XML "Süre veri türü."](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**Dizinleri**|Açıklama, bu sayfada başka bir yerde bakın.|  
|**EtwProviders**|Açıklama, bu sayfada başka bir yerde bakın.|  
|**Ölçümler**|Açıklama, bu sayfada başka bir yerde bakın.|  
|**Performans sayaçları**|Açıklama, bu sayfada başka bir yerde bakın.|  
|**WindowsEventLog**|Açıklama, bu sayfada başka bir yerde bakın.| 
|**DockerSources**|Açıklama, bu sayfada başka bir yerde bakın. | 



## <a name="crashdumps-element"></a>CrashDumps öğesi  
 *Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*
 
 Kilitlenme bilgi dökümleri Hello koleksiyonunu etkinleştirin.  

|Öznitelikler|Açıklama|  
|----------------|-----------------|  
|**kapsayıcı adı**|İsteğe bağlı. toostore kilitlenme bilgi dökümleri kullanılan Azure Storage hesabı toobe hello blob kapsayıcısında Hello adı.|  
|**crashDumpType**|İsteğe bağlı.  Azure tanılama toocollect mini ya da tam kilitlenme dökümleri yapılandırır.|  
|**directoryQuotaPercentage**|İsteğe bağlı.  Merhaba yüzdesini yapılandırır **overallQuotaInMB** toobe hello VM üzerinde kilitlenme dökümleri için ayrılmış.|  

|Alt öğeler|Açıklama|  
|--------------------|-----------------|  
|**CrashDumpConfiguration**|Gereklidir. Her işlem için yapılandırma değerlerini tanımlar.<br /><br /> özniteliği aşağıdaki hello de gereklidir:<br /><br /> **işlemadı** - hello kilitlenme dökümü için kullanmak istediğiniz Azure tanılama toocollect hello işlemin adı.|  

## <a name="directories-element"></a>Dizinleri öğesi 
 *Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - dizinler*

 Bir dizinin içeriğini hello koleksiyonunu etkinleştirir Merhaba, IIS erişim isteği günlükleri ve/veya IIS günlüklerini başarısız oldu.  

 İsteğe bağlı **scheduledTransferPeriod** özniteliği. Daha önce açıklama konusuna bakın.  

|Alt öğeler|Açıklama|  
|--------------------|-----------------|  
|**IISLogs**|Bu öğe hello yapılandırmasında dahil olmak üzere IIS günlüklerini hello koleksiyonunu sağlar:<br /><br /> **kapsayıcı adı** -toostore hello IIS günlüklerini kullanılan Azure Storage hesabı toobe hello blob kapsayıcısında hello adı.|   
|**FailedRequestLogs**|Bu öğe hello yapılandırmasında dahil olmak üzere başarısız isteklerin tooan IIS siteniz veya uygulamanız hakkında günlükleri koleksiyonunu sağlar. İzleme seçenekleri altında da etkinleştirmeniz gerekir **sistem. Web sunucusu** içinde **Web.config**.|  
|**Veri kaynakları**|Dizinleri toomonitor listesi.| 




## <a name="datasources-element"></a>Veri kaynakları öğesi  
 *Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - dizinlere - veri kaynakları*

 Dizinleri toomonitor listesi.  

|Alt öğeler|Açıklama|  
|--------------------|-----------------|  
|**DirectoryConfiguration**|Gereklidir. Gerekli öznitelik:<br /><br /> **kapsayıcı adı** - hello hello bu toobe kullanılan toostore hello günlük dosyaları Azure depolama hesabınızdaki blob kapsayıcısının adı.|  





## <a name="directoryconfiguration-element"></a>DirectoryConfiguration öğesi  
 *Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - dizinlere - veri kaynakları - DirectoryConfiguration*

 Her iki hello içerebilir **mutlak** veya **LocalResource** öğesi ikisini birden belirtmeyin.  

|Alt öğeler|Açıklama|  
|--------------------|-----------------|  
|**Mutlak**|mutlak yol toohello directory toomonitor hello. Aşağıdaki öznitelikler hello gereklidir:<br /><br /> - **Yol** -mutlak bir yol toohello directory toomonitor hello.<br /><br /> - **expandEnvironment** -Path ortam değişkenleri genişletilmiş olup olmadığını yapılandırır.|  
|**LocalResource**|Merhaba yolu göreli tooa yerel kaynak toomonitor. Gerekli öznitelikler şunlardır:<br /><br /> - **Ad** -hello hello dizin toomonitor içeren yerel kaynak<br /><br /> - **relativePath** -hello dizin toomonitor içeren yolu göreli tooName hello|  



## <a name="etwproviders-element"></a>EtwProviders öğesi  
 *Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*

 EventSource ETW olayları koleksiyonu yapılandırır ve/veya ETW bildirim dayalı sağlayıcıları.  

|Alt öğeler|Açıklama|  
|--------------------|-----------------|  
|**EtwEventSourceProviderConfiguration**|Koleksiyon üretilen olayların yapılandırır [EventSource sınıfı](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Gerekli öznitelik:<br /><br /> **Sağlayıcı** -hello EventSource olay hello sınıfı adı.<br /><br /> İsteğe bağlı öznitelikleri şunlardır:<br /><br /> - **scheduledTransferLogLevelFilter** -hello minimum önem düzeyi tootransfer tooyour depolama hesabı.<br /><br /> - **scheduledTransferPeriod** -toohello minute en yakın yuvarlanan zamanlanmış aktarımları toostorage hello aralığıdır. Merhaba değeri bir [XML "Süre veri türü."](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**EtwManifestProviderConfiguration**|Gerekli öznitelik:<br /><br /> **Sağlayıcı** -hello Olay sağlayıcısı GUİD'si hello<br /><br /> İsteğe bağlı öznitelikleri şunlardır:<br /><br /> - **scheduledTransferLogLevelFilter** -hello minimum önem düzeyi tootransfer tooyour depolama hesabı.<br /><br /> - **scheduledTransferPeriod** -toohello minute en yakın yuvarlanan zamanlanmış aktarımları toostorage hello aralığıdır. Merhaba değeri bir [XML "Süre veri türü."](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  



## <a name="etweventsourceproviderconfiguration-element"></a>EtwEventSourceProviderConfiguration öğesi  
 *Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwEventSourceProviderConfiguration*

 Koleksiyon üretilen olayların yapılandırır [EventSource sınıfı](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).  

|Alt öğeler|Açıklama|  
|--------------------|-----------------|  
|**DefaultEvents**|İsteğe bağlı öznitelik:<br/><br/> **eventDestination** - hello hello tablo toostore hello olayları adı|  
|**Olay**|Gerekli öznitelik:<br /><br /> **Kimliği** -hello olay hello kimliği.<br /><br /> İsteğe bağlı öznitelik:<br /><br /> **eventDestination** - hello hello tablo toostore hello olayları adı|  



## <a name="etwmanifestproviderconfiguration-element"></a>EtwManifestProviderConfiguration öğesi  
 *Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*

|Alt öğeler|Açıklama|  
|--------------------|-----------------|  
|**DefaultEvents**|İsteğe bağlı öznitelik:<br /><br /> **eventDestination** - hello hello tablo toostore hello olayları adı|  
|**Olay**|Gerekli öznitelik:<br /><br /> **Kimliği** -hello olay hello kimliği.<br /><br /> İsteğe bağlı öznitelik:<br /><br /> **eventDestination** - hello hello tablo toostore hello olayları adı|  



## <a name="metrics-element"></a>Ölçümleri öğesi  
 *Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - ölçümleri*

 Toogenerate hızlı sorguları için en iyi hale getirilmiş bir performans sayacı tablo sağlar. Hello tanımlanan her performans sayacı **performans sayaçları** öğesi hello ölçümleri toplama toohello performans sayacı tablo tablosunda depolanır.  

 Merhaba **ResourceId** özniteliği gereklidir.  Sanal makine için Azure tanılama dağıtıyorsanız hello Hello kaynak kimliği. Merhaba alma **ResourceId** hello gelen [Azure portal](https://portal.azure.com). Seçin **Gözat** -> **kaynak grupları** -> **< adı\>**. Merhaba tıklatın **özellikleri** döşeme ve hello hello değerini kopyalayın **kimliği** alan.  

|Alt öğeler|Açıklama|  
|--------------------|-----------------|  
|**MetricAggregation**|Gerekli öznitelik:<br /><br /> **scheduledTransferPeriod** -toohello minute en yakın yuvarlanan zamanlanmış aktarımları toostorage hello aralığıdır. Merhaba değeri bir [XML "Süre veri türü."](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  



## <a name="performancecounters-element"></a>PerformanceCounters öğesi  
 *Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - performans sayaçları*

 Performans sayaçları Hello koleksiyonunu sağlar.  

 İsteğe bağlı öznitelik:  

 İsteğe bağlı **scheduledTransferPeriod** özniteliği. Daha önce açıklama konusuna bakın.

|Alt öğe|Açıklama|  
|-------------------|-----------------|  
|**PerformanceCounterConfiguration**|Aşağıdaki öznitelikler hello gereklidir:<br /><br /> - **counterSpecifier** - hello hello performans sayacının adı. Örneğin, `\Processor(_Total)\% Processor Time`. tooget hello komutunu çalıştırın, ana bilgisayarda listesini performans sayaçları `typeperf`.<br /><br /> - **sampleRate** -ne sıklıkta hello sayaç örneklenen.<br /><br /> İsteğe bağlı öznitelik:<br /><br /> **Birim** -hello ölçü hello sayacı.|  




## <a name="windowseventlog-element"></a>WindowsEventLog öğesi
 *Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*
 
 Merhaba koleksiyonu, Windows olay günlüklerini sağlar.  

 İsteğe bağlı **scheduledTransferPeriod** özniteliği. Daha önce açıklama konusuna bakın.  

|Alt öğe|Açıklama|  
|-------------------|-----------------|  
|**Veri kaynağı**|Merhaba Windows olay günlüklerini toocollect. Gerekli öznitelik:<br /><br /> **ad** -hello windows olayları toobe açıklayan hello XPath sorgusu toplanır. Örneğin:<br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> tüm olayları toocollect belirtin "*"|  




## <a name="logs-element"></a>Günlükleri öğesi  
 *Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - günlükleri*

 Sürüm 1.0 ve 1.1 sunar. 1.2 ile eksik. 1.3 geri eklendi.  

 Temel Azure günlükleri Hello arabellek yapılandırmasını tanımlar.  

|Öznitelik|Tür|Açıklama|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|**unsignedInt**|İsteğe bağlı. Merhaba en belirtilen hello için kullanılabilir olan dosya sistemi depolama miktarını belirtir veri.<br /><br /> Merhaba varsayılan 0'dır.|  
|**scheduledTransferLogLevelFilterr**|**dize**|İsteğe bağlı. Aktarılır günlük girişlerini Hello en düşük önem derecesini belirtir. Merhaba varsayılan değer **tanımlanmamış**, tüm günlükleri aktarır. Diğer olası değerler (tooleast bilgilerin çoğu sırasına göre) **ayrıntılı**, **bilgi**, **uyarı**, **hata**ve **Kritik**.|  
|**scheduledTransferPeriod**|**süre**|İsteğe bağlı. Zamanlanmış toohello minute en yakın yukarı yuvarlanmasını veri aktarımını Hello aralığını belirtir.<br /><br /> Merhaba, PT0S varsayılandır.|  
|**İç havuzlar** 1.5 inç eklendi|**dize**|İsteğe bağlı. Noktaları tooa havuz konumu tooalso tanılama verisi gönderin. Örneğin, Application Insights.|  

## <a name="dockersources"></a>DockerSources
 *Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*

 İçinde 1.9 eklendi.

|Öğe adı|Açıklama|  
|------------------|-----------------|  
|**İstatistikleri**|Docker kapsayıcıları toocollect istatistikleri Hello sistem bildirir|  

## <a name="sinksconfig-element"></a>SinksConfig öğesi  
 *Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*

 Konumları toosend tanılama veri tooand hello yapılandırması konumların ile ilişkili bir listesi.  

|Öğe adı|Açıklama|  
|------------------|-----------------|  
|**Havuz**|Açıklama, bu sayfada başka bir yerde bakın.|  

## <a name="sink-element"></a>Öğe havuzu
 *Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - havuz*

 Sürüm 1.5 eklendi.  

 Konumları toosend Tanılama verileri tanımlar. Örneğin, Application Insights hizmeti hello.  

|Öznitelik|Tür|Açıklama|  
|---------------|----------|-----------------|  
|**adı**|Dize|Bir dize tanımlayıcı hello sinkname.|  

|Öğesi|Tür|Açıklama|  
|-------------|----------|-----------------|  
|**Application Insights**|Dize|Yalnızca veri tooApplication Öngörüler gönderirken kullanılır. Merhaba erişiminiz etkin bir Application Insights hesabı için izleme anahtarını içerir.|  
|**Kanalları**|Dize|Her ek, akış filtrelemesi için bir tane|  

## <a name="channels-element"></a>Kanallar öğesi  
 *Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - havuz - kanalları*

 Sürüm 1.5 eklendi.  

 Bir havuz geçirme günlük veri akışları için filtreleri tanımlar.  

|Öğesi|Tür|Açıklama|  
|-------------|----------|-----------------|  
|**Kanal**|Dize|Açıklama, bu sayfada başka bir yerde bakın.|  

## <a name="channel-element"></a>Kanal öğesi
 *Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - havuz - kanalları - kanal*

 Sürüm 1.5 eklendi.  

 Konumları toosend Tanılama verileri tanımlar. Örneğin, Application Insights hizmeti hello.  

|Öznitelikler|Tür|Açıklama|  
|----------------|----------|-----------------|  
|**logLevel**|**dize**|Aktarılır günlük girişlerini Hello en düşük önem derecesini belirtir. Merhaba varsayılan değer **tanımlanmamış**, tüm günlükleri aktarır. Diğer olası değerler (tooleast bilgilerin çoğu sırasına göre) **ayrıntılı**, **bilgi**, **uyarı**, **hata**ve **Kritik**.|  
|**adı**|**dize**|Merhaba kanal toorefer için benzersiz bir ad|  


## <a name="privateconfig-element"></a>PrivateConfig öğesi 
 *Ağaç: Kök - DiagnosticsConfiguration - PrivateConfig*

 Sürüm 1.3 eklendi.  

 İsteğe bağlı  

 Merhaba özel ayrıntıları hello depolama hesabının (adı, anahtar ve uç nokta) depolar. Bu bilgiler toohello sanal makine gönderilir, ancak ondan alınamıyor.  

|Alt öğeler|Açıklama|  
|--------------------|-----------------|  
|**StorageAccount**|Merhaba depolama hesabı toouse. Aşağıdaki öznitelikler hello gereklidir<br /><br /> - **ad** - hello hello depolama hesabı adı.<br /><br /> - **anahtar** - hello anahtar toohello depolama hesabı.<br /><br /> - **uç nokta** -hello uç nokta tooaccess hello depolama hesabı. <br /><br /> -**sasToken** (Merhaba özel yapılandırma dosyasında bir SAS belirteci bir depolama hesabı anahtarı yerine belirtebilirsiniz 1.8.1)-eklenir. Merhaba depolama hesabı anahtarı sağladıysanız, göz ardı edilir. <br />SAS belirteci hello gereksinimleri: <br />-Hesap SAS belirteci yalnızca destekler <br />- *b*, *t* hizmet türleri gereklidir. <br /> - *bir*, *c*, *u*, *w* izinleri gereklidir. <br /> - *c*, *o* kaynak türleri gereklidir. <br /> -Yalnızca hello HTTPS protokolünü destekler <br /> -Başlangıç ve sona erme saati geçerli olmalıdır.|  


## <a name="isenabled-element"></a>IsEnabled öğesi  
 *Ağaç: Kök - DiagnosticsConfiguration - IsEnabled*

 Boole değeri. Kullanım `true` tooenable hello Tanılama veya `false` toodisable hello tanılama.
