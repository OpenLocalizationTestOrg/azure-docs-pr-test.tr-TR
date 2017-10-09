---
title: "aaaAzure tanılama 1.0 yapılandırma şeması | Microsoft Docs"
description: "YALNIZCA ilgili Azure SDK 2.4 kullanıyorsanız ve aşağıda Azure sanal makineler, sanal makine ölçek kümeleri, Service Fabric veya Bulut Hizmetleri ile."
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
ms.openlocfilehash: bdd2b26217d6ea28f19e651ab429e7e7401ff57b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-10-configuration-schema"></a>Azure tanılama 1.0 yapılandırma şeması
> [!NOTE]
> Azure tanılama hello kullanılan bileşen toocollect performans sayaçları ve diğer Azure sanal makineler, sanal makine ölçek kümeleri, Service Fabric ve Cloud Services istatistiklerine ' dir.  Bu sayfa, yalnızca bu hizmetlerden biri kullanıyorsanız geçerlidir.
>

Azure tanılama Azure monitör, Application Insights ve günlük analizi gibi diğer Microsoft tanılama ürünlerle kullanılır.

Hello Azure tanılama yapılandırma dosyası kullanılan tooinitialize hello Tanılama izleme olan değerleri tanımlar. Merhaba tanılama başlatır izlerken bu kullanılan tooinitialize tanılama yapılandırma ayarlarını dosyasıdır.  

 Varsayılan olarak, yüklü toohello hello Azure tanılama yapılandırması şema dosyası olan `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` dizini. Değiştir `<version>` hello yüklü hello sürümüyle [Azure SDK'sı](http://www.windowsazure.com/develop/downloads/).  

> [!NOTE]
>  Merhaba tanılama yapılandırma dosyası, genellikle önceki hello başlatma işleminde toplanan tanılama veri toobe gerektiren başlangıç görevleri ile kullanılır. Azure tanılama kullanma hakkında daha fazla bilgi için bkz: [kullanarak Azure tanılama tarafından günlüğü verilerini toplamak](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Merhaba tanılama yapılandırma dosyası örneği  
 Aşağıdaki örnek hello tipik tanılama yapılandırma dosyası gösterir:  

```xml  
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"  
      configurationChangePollInterval="PT1M"  
      overallQuotaInMB="4096">  
   <DiagnosticInfrastructureLogs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  
   <Logs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  

   <Directories bufferQuotaInMB="1024"   
      scheduledTransferPeriod="PT1M">  

      <!-- These three elements specify hello special directories   
           that are set up for hello log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories hello DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative tooa local   
                 resource defined in hello service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- hello counter specifier is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- hello event log name is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a>DiagnosticsConfiguration Namespace  
 Merhaba tanılama yapılandırma dosyası için Hello XML ad alanı şöyledir:  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a>Şema öğeleri  
 Merhaba tanılama yapılandırma dosyası hello aşağıdaki öğeleri içerir.


## <a name="diagnosticmonitorconfiguration-element"></a>DiagnosticMonitorConfiguration öğesi  
Merhaba hello tanılama yapılandırma dosyasının en üst düzey öğesi.  

Öznitelikleri:

|Öznitelik  |Tür   |Gerekli| Varsayılan | Açıklama|  
|-----------|-------|--------|---------|------------|  
|**configurationChangePollInterval**|Süre|İsteğe bağlı | PT1M| Hangi hello tanı İzleyicisi yoklamalar Hello aralıkta tanılama yapılandırma değişikliklerini belirtir.|  
|**overallQuotaInMB**|unsignedInt|İsteğe bağlı| 4000 MB. Bir değer belirtirseniz, bu miktar aşmamalıdır |Merhaba tüm günlük arabellekleri için ayrılan dosya sistemi depolama alanının toplam tutar.|  

## <a name="diagnosticinfrastructurelogs-element"></a>DiagnosticInfrastructureLogs öğesi  
Merhaba temel Tanılama Altyapısı tarafından oluşturulan hello günlükleri Hello arabellek yapılandırmasını tanımlar.

Üst öğe: [DiagnosticMonitorConfiguration öğesi](#DiagnosticMonitorConfiguration).  

Öznitelikleri:

|Öznitelik|Tür|Açıklama|  
|---------|----|-----------------|  
|**bufferQuotaInMB**|unsignedInt|İsteğe bağlı. Merhaba en belirtilen hello için kullanılabilir olan dosya sistemi depolama miktarını belirtir veri.<br /><br /> Merhaba varsayılan 0'dır.|  
|**scheduledTransferLogLevelFilter**|Dize|İsteğe bağlı. Aktarılır günlük girişlerini Hello en düşük önem derecesini belirtir. Merhaba varsayılan değer **tanımlanmamış**. Diğer olası değerler şunlardır: **ayrıntılı**, **bilgi**, **uyarı**, **hata**, ve **kritik**.|  
|**scheduledTransferPeriod**|Süre|İsteğe bağlı. Zamanlanmış toohello minute en yakın yukarı yuvarlanmasını veri aktarımını Hello aralığını belirtir.<br /><br /> Merhaba, PT0S varsayılandır.|  

## <a name="logs-element"></a>Günlükleri öğesi  
 Temel Azure günlükleri Hello arabellek yapılandırmasını tanımlar.

 Üst öğenin: [DiagnosticMonitorConfiguration öğesi](#DiagnosticMonitorConfiguration).  

Öznitelikleri:  

|Öznitelik|Tür|Açıklama|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|İsteğe bağlı. Merhaba en belirtilen hello için kullanılabilir olan dosya sistemi depolama miktarını belirtir veri.<br /><br /> Merhaba varsayılan 0'dır.|  
|**scheduledTransferLogLevelFilter**|Dize|İsteğe bağlı. Aktarılır günlük girişlerini Hello en düşük önem derecesini belirtir. Merhaba varsayılan değer **tanımlanmamış**. Diğer olası değerler şunlardır: **ayrıntılı**, **bilgi**, **uyarı**, **hata**, ve **kritik**.|  
|**scheduledTransferPeriod**|Süre|İsteğe bağlı. Zamanlanmış toohello minute en yakın yukarı yuvarlanmasını veri aktarımını Hello aralığını belirtir.<br /><br /> Merhaba, PT0S varsayılandır.|  

## <a name="directories-element"></a>Dizinleri öğesi  
Merhaba arabellek yapılandırmasını tanımlamak dosya tabanlı günlükleri için tanımlar.

Üst öğenin: [DiagnosticMonitorConfiguration öğesi](#DiagnosticMonitorConfiguration).  


Öznitelikleri:  

|Öznitelik|Tür|Açıklama|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|İsteğe bağlı. Merhaba en belirtilen hello için kullanılabilir olan dosya sistemi depolama miktarını belirtir veri.<br /><br /> Merhaba varsayılan 0'dır.|  
|**scheduledTransferPeriod**|Süre|İsteğe bağlı. Zamanlanmış toohello minute en yakın yukarı yuvarlanmasını veri aktarımını Hello aralığını belirtir.<br /><br /> Merhaba, PT0S varsayılandır.|  

## <a name="crashdumps-element"></a>CrashDumps öğesi  
 Merhaba kilitlenme dökümleri directory tanımlar.

 Üst öğe: [dizinleri öğesi](#Directories).  

Öznitelikleri:  

|Öznitelik|Tür|Açıklama|  
|---------------|----------|-----------------|  
|**kapsayıcı**|Dize|Merhaba hello dizinin Merhaba içeriğine toobe olduğu hello kapsayıcının adını aktarılan.|  
|**directoryQuotaInMB**|unsignedInt|İsteğe bağlı. Hello dizinin Hello maksimum boyutu megabayt cinsinden belirtir.<br /><br /> Merhaba varsayılan 0'dır.|  

## <a name="failedrequestlogs-element"></a>FailedRequestLogs öğesi  
 Merhaba başarısız istek günlük dizini tanımlar.

 Üst öğesi [dizinleri öğesi](#Directories).  

Öznitelikleri:  

|Öznitelik|Tür|Açıklama|  
|---------------|----------|-----------------|  
|**kapsayıcı**|Dize|Merhaba hello dizinin Merhaba içeriğine toobe olduğu hello kapsayıcının adını aktarılan.|  
|**directoryQuotaInMB**|unsignedInt|İsteğe bağlı. Hello dizinin Hello maksimum boyutu megabayt cinsinden belirtir.<br /><br /> Merhaba varsayılan 0'dır.|  

##  <a name="iislogs-element"></a>IISLogs öğesi  
 Merhaba IIS Günlük dizini tanımlar.

 Üst öğesi [dizinleri öğesi](#Directories).  

Öznitelikleri:  

|Öznitelik|Tür|Açıklama|  
|---------------|----------|-----------------|  
|**kapsayıcı**|Dize|Merhaba hello dizinin Merhaba içeriğine toobe olduğu hello kapsayıcının adını aktarılan.|  
|**directoryQuotaInMB**|unsignedInt|İsteğe bağlı. Hello dizinin Hello maksimum boyutu megabayt cinsinden belirtir.<br /><br /> Merhaba varsayılan 0'dır.|  

## <a name="datasources-element"></a>Veri kaynakları öğesi  
 Sıfır veya daha fazla ek günlük dizinleri tanımlar.

 Üst öğe: [dizinleri öğesi](#Directories).

## <a name="directoryconfiguration-element"></a>DirectoryConfiguration öğesi  
 Günlük dosyaları toomonitor Hello dizini tanımlar.

 Üst öğe: [veri kaynakları öğesi](#DataSources).

Öznitelikleri:

|Öznitelik|Tür|Açıklama|  
|---------------|----------|-----------------|  
|**kapsayıcı**|Dize|Merhaba hello dizinin Merhaba içeriğine toobe olduğu hello kapsayıcının adını aktarılan.|  
|**directoryQuotaInMB**|unsignedInt|İsteğe bağlı. Hello dizinin Hello maksimum boyutu megabayt cinsinden belirtir.<br /><br /> Merhaba varsayılan 0'dır.|  

## <a name="absolute-element"></a>Mutlak öğesi  
 İsteğe bağlı ortam genişletme ile Merhaba dizin toomonitor mutlak bir yol tanımlar.

 Üst öğe: [DirectoryConfiguration öğesi](#DirectoryConfiguration).  

Öznitelikleri:  

|Öznitelik|Tür|Açıklama|  
|---------------|----------|-----------------|  
|**yol**|Dize|Gereklidir. mutlak yol toohello directory toomonitor hello.|  
|**expandEnvironment**|Boole değeri|Gereklidir. Varsa çok ayarlamak**doğru**, ortam değişkenleri hello yolun genişletilmiş.|  

## <a name="localresource-element"></a>LocalResource öğesi  
 Merhaba hizmet tanımında tanımlanan yolu göreli tooa yerel bir kaynak tanımlar.

 Üst öğe: [DirectoryConfiguration öğesi](#DirectoryConfiguration).  

Öznitelikleri:  

|Öznitelik|Tür|Açıklama|  
|---------------|----------|-----------------|  
|**adı**|Dize|Gereklidir. Merhaba dizin toomonitor içeren hello yerel kaynak Hello adı.|  
|**relativePath**|Dize|Gereklidir. Merhaba yolu göreli toohello yerel kaynak toomonitor.|  

## <a name="performancecounters-element"></a>PerformanceCounters öğesi  
 Merhaba yolu toohello performans sayacı toocollect tanımlar.

 Üst öğe: [DiagnosticMonitorConfiguration öğesi](#DiagnosticMonitorConfiguration).


 Öznitelikleri:  

|Öznitelik|Tür|Açıklama|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|İsteğe bağlı. Merhaba en belirtilen hello için kullanılabilir olan dosya sistemi depolama miktarını belirtir veri.<br /><br /> Merhaba varsayılan 0'dır.|  
|**scheduledTransferPeriod**|Süre|İsteğe bağlı. Zamanlanmış toohello minute en yakın yukarı yuvarlanmasını veri aktarımını Hello aralığını belirtir.<br /><br /> Merhaba, PT0S varsayılandır.|  

## <a name="performancecounterconfiguration-element"></a>PerformanceCounterConfiguration öğesi  
 Merhaba performans sayacı toocollect tanımlar.

 Üst öğe: [PerformanceCounters öğesi](#PerformanceCounters).  

 Öznitelikleri:  

|Öznitelik|Tür|Açıklama|  
|---------------|----------|-----------------|  
|**counterSpecifier**|Dize|Gereklidir. Merhaba yolu toohello performans sayacı toocollect.|  
|**sampleRate**|Süre|Gereklidir. Performans sayacı hangi hello toplanması gereken hello oranı.|  

## <a name="windowseventlog-element"></a>WindowsEventLog öğesi  
 Merhaba olay günlüklerini toomonitor tanımlar.

 Üst öğe: [DiagnosticMonitorConfiguration öğesi](#DiagnosticMonitorConfiguration).

  Öznitelikleri:

|Öznitelik|Tür|Açıklama|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|İsteğe bağlı. Merhaba en belirtilen hello için kullanılabilir olan dosya sistemi depolama miktarını belirtir veri.<br /><br /> Merhaba varsayılan 0'dır.|  
|**scheduledTransferLogLevelFilter**|Dize|İsteğe bağlı. Aktarılır günlük girişlerini Hello en düşük önem derecesini belirtir. Merhaba varsayılan değer **tanımlanmamış**. Diğer olası değerler şunlardır: **ayrıntılı**, **bilgi**, **uyarı**, **hata**, ve **kritik**.|  
|**scheduledTransferPeriod**|Süre|İsteğe bağlı. Zamanlanmış toohello minute en yakın yukarı yuvarlanmasını veri aktarımını Hello aralığını belirtir.<br /><br /> Merhaba, PT0S varsayılandır.|  

## <a name="datasource-element"></a>Veri kaynağı öğesi  
 Merhaba olay günlüğü toomonitor tanımlar.

 Üst öğe: [WindowsEventLog öğesi](#windowsEventLog).  

 Öznitelikleri:

|Öznitelik|Tür|Açıklama|  
|---------------|----------|-----------------|  
|**adı**|Dize|Gereklidir. Merhaba günlük toocollect belirten bir XPath ifadesi.|  
