---
title: "aaaAzure tanılama 1.2 yapılandırma şeması | Microsoft Docs"
description: "YALNIZCA Azure sanal makineler, sanal makine ölçek kümeleri, Service Fabric veya Bulut Hizmetleri ile Azure SDK 2.5 kullanıyorsanız ilgilidir."
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
ms.openlocfilehash: 31559317b696556a64b51b58800b176ade9a4679
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-12-configuration-schema"></a>Azure tanılama 1.2 yapılandırma şeması
> [!NOTE]
> Azure tanılama hello kullanılan bileşen toocollect performans sayaçları ve diğer Azure sanal makineler, sanal makine ölçek kümeleri, Service Fabric ve Cloud Services istatistiklerine ' dir.  Bu sayfa, yalnızca bu hizmetlerden biri kullanıyorsanız geçerlidir.
>

Azure tanılama Azure monitör, Application Insights ve günlük analizi gibi diğer Microsoft tanılama ürünlerle kullanılır.

Bu şemayı hello tanılama İzleyicisi başlatıldığında tooinitialize tanılama yapılandırma ayarlarını kullanabilirsiniz hello olası değerleri tanımlar.  


 Merhaba ortak yapılandırma dosyası şeması tanımı hello aşağıdaki PowerShell komutunu yürüterek yükleyin:  

```PowerShell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

 Azure tanılama kullanma hakkında daha fazla bilgi için bkz: [Azure Cloud Services etkinleştirme tanılamada](http://azure.microsoft.com/documentation/articles/cloud-services-dotnet-diagnostics/).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Merhaba tanılama yapılandırma dosyası örneği  
 Aşağıdaki örnek hello tipik tanılama yapılandırma dosyası gösterir:  

```xml
<?xml version="1.0" encoding="utf-8"?>  
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">  
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
        <EtwEventSourceProviderConfiguration provider="MyProviderClass" scheduledTransferPeriod="PT5M">  
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
      <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
        <CrashDumpConfiguration processName="mynewprocess.exe" />  
        <CrashDumpConfiguration processName="badapp.exe"/>  
      </CrashDumps>  
    </DiagnosticMonitorConfiguration>  
  </WadCfg>  
</PublicConfig>  

```  

## <a name="diagnostics-configuration-namespace"></a>Tanılama yapılandırması Namespace  
 Merhaba tanılama yapılandırma dosyası için Hello XML ad alanı şöyledir:  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="publicconfig-element"></a>PublicConfig öğesi  
 Merhaba tanılama yapılandırma dosyasının en üst düzey öğesi. Merhaba aşağıdaki tabloda hello yapılandırma dosyasının hello öğelerini açıklar.  

|Öğe adı|Açıklama|  
|------------------|-----------------|  
|**WadCfg**|Gereklidir. Merhaba telemetri verileri toobe için yapılandırma ayarlarını toplanır.|  
|**StorageAccount**|hello Azure depolama hesabı toostore hello verilerde Hello adı. Bu da bir parametre olarak hello kümesi AzureServiceDiagnosticsExtension cmdlet'ini çalıştırırken belirtilebilir.|  
|**LocalResourceDirectory**|Merhaba sanal makine toobe Hello dizinde İzleme Aracısı toostore olay verilerini hello tarafından kullanılır. Aksi halde kümesi, hello varsayılan dizin kullanılır:<br /><br /> Worker/web rolü için:`C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`<br /><br /> Bir sanal makine için:`C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`<br /><br /> Gerekli öznitelikler şunlardır:<br /><br /> -                      **yol** - hello Azure tanılama tarafından kullanılan hello sistem toobe dizininde.<br /><br /> -                      **expandEnvironment** -ortam değişkenleri hello yol adında genişletilmiş olup olmadığını denetler.|  

## <a name="wadcfg-element"></a>WadCFG öğesi  
Toplanan hello telemetri verileri toobe için yapılandırma ayarlarını tanımlar. Aşağıdaki tablonun hello alt öğeleri açıklanmıştır:  

|Öğe adı|Açıklama|  
|------------------|-----------------|  
|**DiagnosticMonitorConfiguration**|Gereklidir. İsteğe bağlı öznitelikleri şunlardır:<br /><br /> -                     **overallQuotaInMB** -hello maksimum hello tarafından tüketilen yerel disk alanı miktarını tanılama verilerini çeşitli türlerde toplanan tarafından Azure tanılama. Merhaba varsayılan ayar 5120 MB'tır.<br /><br /> -                     **useProxyServer** -IE ayarlarının kümesinde olarak Azure tanılama yapılandırmak toouse hello proxy sunucusu ayarları.|  
|**CrashDumps**|Kilitlenme bilgi dökümleri koleksiyonunu etkinleştirin. İsteğe bağlı öznitelikleri şunlardır:<br /><br /> -                     **kapsayıcı adı** -toostore kilitlenme bilgi dökümleri kullanılan Azure Storage hesabı toobe hello blob kapsayıcısında hello adı.<br /><br /> -                     **crashDumpType** -yapılandırır Azure tanılama toocollect Mini ya da tam kilitlenme dökümleri.<br /><br /> -                     **directoryQuotaPercentage**-hello yüzdesini yapılandırır **overallQuotaInMB** toobe hello VM üzerinde kilitlenme dökümleri için ayrılmış.|  
|**DiagnosticInfrastructureLogs**|Azure tanılama tarafından oluşturulan günlükleri koleksiyonunu etkinleştirin. Merhaba Tanılama Altyapısı günlükleri hello tanılama sistem kendisini sorun giderme için yararlıdır. İsteğe bağlı öznitelikleri şunlardır:<br /><br /> -                     **scheduledTransferLogLevelFilter** -toplanan hello günlüklerini hello en düşük önem derecesi yapılandırır.<br /><br /> -                     **scheduledTransferPeriod** -toohello minute en yakın yuvarlanan zamanlanmış aktarımları toostorage hello aralığıdır. Merhaba değeri bir [XML "Süre veri türü."](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**Dizinleri**|Bir dizinin içeriğini hello koleksiyonunu etkinleştirir Merhaba, IIS erişim isteği günlükleri ve/veya IIS günlüklerini başarısız oldu. İsteğe bağlı öznitelik:<br /><br /> **scheduledTransferPeriod** -toohello minute en yakın yuvarlanan zamanlanmış aktarımları toostorage hello aralığıdır. Merhaba değeri bir [XML "Süre veri türü."](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**EtwProviders**|EventSource ETW olayları koleksiyonu yapılandırır ve/veya ETW bildirim dayalı sağlayıcıları.|  
|**Ölçümler**|Bu öğe toogenerate hızlı sorguları için en iyi hale getirilmiş bir performans sayacı tablo sağlar. Hello tanımlanan her performans sayacı **performans sayaçları** öğesi hello ölçümleri toplama toohello performans sayacı tablo tablosunda depolanır. Gerekli öznitelik:<br /><br /> **ResourceId** -hello kaynak hello Azure tanılama dağıttığınız sanal makine Kimliğini budur. Merhaba alma **ResourceId** hello gelen [Azure portal](https://portal.azure.com). Seçin **Gözat** -> **kaynak grupları** -> **< adı\>**. Merhaba tıklatın **özellikleri** döşeme ve hello hello değerini kopyalayın **kimliği** alan.|  
|**Performans sayaçları**|Performans sayaçları Hello koleksiyonunu sağlar. İsteğe bağlı öznitelik:<br /><br /> **scheduledTransferPeriod** -toohello minute en yakın yuvarlanan zamanlanmış aktarımları toostorage hello aralığıdır. Değer bir [XML "Süre veri türü".](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**WindowsEventLog**|Merhaba koleksiyonu, Windows olay günlüklerini sağlar. İsteğe bağlı öznitelik:<br /><br /> **scheduledTransferPeriod** -toohello minute en yakın yuvarlanan zamanlanmış aktarımları toostorage hello aralığıdır. Değer bir [XML "Süre veri türü".](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  

## <a name="crashdumps-element"></a>CrashDumps öğesi  
 Kilitlenme bilgi dökümleri koleksiyonunu sağlar. Aşağıdaki tablonun hello alt öğeleri açıklanmıştır:  

|Öğe adı|Açıklama|  
|------------------|-----------------|  
|**CrashDumpConfiguration**|Gereklidir. Gerekli öznitelik:<br /><br /> **işlemadı** - hello kilitlenme dökümü için kullanmak istediğiniz Azure tanılama toocollect hello işlemin adı.|  
|**crashDumpType**|Azure tanılama toocollect mini ya da tam kilitlenme dökümleri yapılandırır.|  
|**directoryQuotaPercentage**|Merhaba yüzdesini yapılandırır **overallQuotaInMB** toobe hello VM üzerinde kilitlenme dökümleri için ayrılmış.|  

## <a name="directories-element"></a>Dizinleri öğesi  
 Bir dizinin içeriğini hello koleksiyonunu etkinleştirir Merhaba, IIS erişim isteği günlükleri ve/veya IIS günlüklerini başarısız oldu. Aşağıdaki tablonun hello alt öğeleri açıklanmıştır:  

|Öğe adı|Açıklama|  
|------------------|-----------------|  
|**Veri kaynakları**|Dizinleri toomonitor listesi.|  
|**FailedRequestLogs**|Bu öğe hello yapılandırmasında dahil olmak üzere başarısız isteklerin tooan IIS siteniz veya uygulamanız hakkında günlükleri koleksiyonunu sağlar. İzleme seçenekleri altında da etkinleştirmeniz gerekir **sistem. Web sunucusu** içinde **Web.config**.|  
|**IISLogs**|Bu öğe hello yapılandırmasında dahil olmak üzere IIS günlüklerini hello koleksiyonunu sağlar:<br /><br /> **kapsayıcı adı** -toostore hello IIS günlüklerini kullanılan Azure Storage hesabı toobe hello blob kapsayıcısında hello adı.|  

## <a name="datasources-element"></a>Veri kaynakları öğesi  
 Dizinleri toomonitor listesi. Aşağıdaki tablonun hello alt öğeleri açıklanmıştır:  

|Öğe adı|Açıklama|  
|------------------|-----------------|  
|**DirectoryConfiguration**|Gereklidir. Gerekli öznitelik:<br /><br /> **kapsayıcı adı** -Azure depolama alanınızı hello blob kapsayıcısında hello adını hesap kullanılan toobe toostore hello günlük dosyaları.|  

## <a name="directoryconfiguration-element"></a>DirectoryConfiguration öğesi  
 **DirectoryConfiguration** ya da hello içerebilir **mutlak** veya **LocalResource** öğesi ikisini birden belirtmeyin. Aşağıdaki tablonun hello alt öğeleri açıklanmıştır:  

|Öğe adı|Açıklama|  
|------------------|-----------------|  
|**Mutlak**|mutlak yol toohello directory toomonitor hello. Aşağıdaki öznitelikler hello gereklidir:<br /><br /> -                     **Yol** -mutlak bir yol toohello directory toomonitor hello.<br /><br /> -                      **expandEnvironment** -Path ortam değişkenleri genişletilmiş olup olmadığını yapılandırır.|  
|**LocalResource**|Merhaba yolu göreli tooa yerel kaynak toomonitor. Gerekli öznitelikler şunlardır:<br /><br /> -                     **Ad** -hello hello dizin toomonitor içeren yerel kaynak<br /><br /> -                     **relativePath** -hello dizin toomonitor içeren yolu göreli tooName hello|  

## <a name="etwproviders-element"></a>EtwProviders öğesi  
 EventSource ETW olayları koleksiyonu yapılandırır ve/veya ETW bildirim dayalı sağlayıcıları. Aşağıdaki tablonun hello alt öğeleri açıklanmıştır:  

|Öğe adı|Açıklama|  
|------------------|-----------------|  
|**EtwEventSourceProviderConfiguration**|Koleksiyon üretilen olayların yapılandırır [EventSource sınıfı](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Gerekli öznitelik:<br /><br /> **Sağlayıcı** -hello EventSource olay hello sınıfı adı.<br /><br /> İsteğe bağlı öznitelikleri şunlardır:<br /><br /> -                     **scheduledTransferLogLevelFilter** -hello minimum önem düzeyi tootransfer tooyour depolama hesabı.<br /><br /> -                     **scheduledTransferPeriod** -toohello minute en yakın yuvarlanan zamanlanmış aktarımları toostorage hello aralığıdır. Değer bir [XML süresi veri türü](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  
|**EtwManifestProviderConfiguration**|Gerekli öznitelik:<br /><br /> **Sağlayıcı** -hello Olay sağlayıcısı GUİD'si hello<br /><br /> İsteğe bağlı öznitelikleri şunlardır:<br /><br /> - **scheduledTransferLogLevelFilter** -hello minimum önem düzeyi tootransfer tooyour depolama hesabı.<br /><br /> -                     **scheduledTransferPeriod** -toohello minute en yakın yuvarlanan zamanlanmış aktarımları toostorage hello aralığıdır. Değer bir [XML süresi veri türü](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  

## <a name="etweventsourceproviderconfiguration-element"></a>EtwEventSourceProviderConfiguration öğesi  
 Koleksiyon üretilen olayların yapılandırır [EventSource sınıfı](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Aşağıdaki tablonun hello alt öğeleri açıklanmıştır:  

|Öğe adı|Açıklama|  
|------------------|-----------------|  
|**DefaultEvents**|İsteğe bağlı öznitelik:<br /><br /> **eventDestination** - hello hello tablo toostore hello olayları adı|  
|**Olay**|Gerekli öznitelik:<br /><br /> **Kimliği** -hello olay hello kimliği.<br /><br /> İsteğe bağlı öznitelik:<br /><br /> **eventDestination** - hello hello tablo toostore hello olayları adı|  

## <a name="etwmanifestproviderconfiguration-element"></a>EtwManifestProviderConfiguration öğesi  
 Aşağıdaki tablonun hello alt öğeleri açıklanmıştır:  

|Öğe adı|Açıklama|  
|------------------|-----------------|  
|**DefaultEvents**|İsteğe bağlı öznitelik:<br /><br /> **eventDestination** - hello hello tablo toostore hello olayları adı|  
|**Olay**|Gerekli öznitelik:<br /><br /> **Kimliği** -hello olay hello kimliği.<br /><br /> İsteğe bağlı öznitelik:<br /><br /> **eventDestination** - hello hello tablo toostore hello olayları adı|  

## <a name="metrics-element"></a>Ölçümleri öğesi  
 Toogenerate hızlı sorguları için en iyi hale getirilmiş bir performans sayacı tablo sağlar. Aşağıdaki tablonun hello alt öğeleri açıklanmıştır:  

|Öğe adı|Açıklama|  
|------------------|-----------------|  
|**MetricAggregation**|Gerekli öznitelik:<br /><br /> **scheduledTransferPeriod** -toohello minute en yakın yuvarlanan zamanlanmış aktarımları toostorage hello aralığıdır. Değer bir [XML süresi veri türü](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  

## <a name="performancecounters-element"></a>PerformanceCounters öğesi  
 Performans sayaçları Hello koleksiyonunu sağlar. Aşağıdaki tablonun hello alt öğeleri açıklanmıştır:  

|Öğe adı|Açıklama|  
|------------------|-----------------|  
|**PerformanceCounterConfiguration**|Aşağıdaki öznitelikler hello gereklidir:<br /><br /> -                     **counterSpecifier** - hello hello performans sayacının adı. Örneğin, `\Processor(_Total)\% Processor Time`. tooget hello komutunu çalıştırın, ana bilgisayardaki performans sayaçlarının listesi `typeperf`.<br /><br /> -                     **sampleRate** -ne sıklıkta hello sayaç örneklenen.<br /><br /> İsteğe bağlı öznitelik:<br /><br /> **Birim** -hello ölçü hello sayacı.|  

## <a name="performancecounterconfiguration-element"></a>PerformanceCounterConfiguration öğesi  
 Aşağıdaki tablonun hello alt öğeleri açıklanmıştır:  

|Öğe adı|Açıklama|  
|------------------|-----------------|  
|**ek açıklama**|Gerekli öznitelik:<br /><br /> **displayName** -hello sayaç hello görünen adı<br /><br /> İsteğe bağlı öznitelik:<br /><br /> **yerel ayar** -hello sayaç adı görüntülerken, yerel ayar toouse hello|  

## <a name="windowseventlog-element"></a>WindowsEventLog öğesi  
 Aşağıdaki tablonun hello alt öğeleri açıklanmıştır:  

|Öğe adı|Açıklama|  
|------------------|-----------------|  
|**Veri kaynağı**|Merhaba Windows olay günlüklerini toocollect. Gerekli öznitelik:<br /><br /> **ad** -hello windows olayları toobe açıklayan hello XPath sorgusu toplanır. Örneğin:<br /><br /> `Application!*[System[(Level >= 3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level >= 3]]`<br /><br /> tüm olayları toocollect belirtin "*".|
