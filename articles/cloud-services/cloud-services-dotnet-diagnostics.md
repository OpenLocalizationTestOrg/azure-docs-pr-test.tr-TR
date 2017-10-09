---
title: "aaaHow toouse bulut Hizmetleri ile Azure tanılama (.NET) | Microsoft Docs"
description: "Azure tanılama toogather kullanarak verileri azure'dan hata ayıklama, performans, izleme, trafik analizi ve daha fazla ölçme bulut Hizmetleri."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 89623a0e-4e78-4b67-a446-7d19a35a44be
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/22/2017
ms.author: robb
ms.openlocfilehash: 1525eac1e85955d8f05aa21a9805e0a80d0e4bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a>Azure Cloud Services, Azure Tanılama'yı etkinleştirme
Bkz: [Azure tanılama genel bakış](../azure-diagnostics.md) bir arka planda Azure tanılama için.

## <a name="how-tooenable-diagnostics-in-a-worker-role"></a>Nasıl tooEnable çalışan rolü tanılamada
Bu kılavuzda nasıl tooimplement telemetri verilerini kullanarak gösterdiği Azure çalışan rolüne hello .NET EventSource sınıfı açıklar. Azure tanılama kullanılan toocollect hello telemetri verilerinin ve bir Azure depolama hesabında depolamak. Çalışan rolü oluştururken, Visual Studio tanılama 1.0 Azure SDK'ları ve önceki sürümler için .NET 2.4 hello çözümde bir parçası olarak otomatik olarak etkinleştirir. Merhaba aşağıdaki yönergeleri hello çalışan rolü hello çözümden tanılama 1.0 devre dışı bırakma ve tanılama 1.2 dağıtma veya 1.3 tooyour çalışan rolü oluşturmak için hello işlemi açıklanmaktadır.

### <a name="prerequisites"></a>Ön koşullar
Bu makale bir Azure aboneliğiniz varsa ve hello Azure SDK ile Visual Studio'ya varsayar. Bir Azure aboneliğiniz yoksa, hello için kaydolabilirsiniz [ücretsiz deneme][Free Trial]. Emin olun çok[yükleyin ve Azure PowerShell sürüm 0.8.7 yapılandırın veya daha sonra][Install and configure Azure PowerShell version 0.8.7 or later].

### <a name="step-1-create-a-worker-role"></a>1. adım: Çalışan rolü oluşturma
1. **Visual Studio**’yu başlatın.
2. Oluşturma bir **Azure bulut hizmeti** hello projeden **bulut** .NET Framework 4. 5'i hedefleyen şablonu.  Merhaba projeyi "WadExample" olarak adlandırın ve Tamam'ı tıklatın.
3. Seçin **çalışan rolü** ve Tamam'ı tıklatın. başlangıç projesi oluşturulur.
4. İçinde **Çözüm Gezgini**, hello çift **WorkerRole1** özellikleri dosya.
5. Merhaba, **yapılandırma** sekmesinde, kaldırma onay **tanılamayı etkinleştir** toodisable tanılama 1.0 (Azure SDK 2.4 ve önceki).
6. Çözüm tooverify yapı hata vardır.

### <a name="step-2-instrument-your-code"></a>2. adım: kodunuzu izleme
WorkerRole.cs Merhaba içeriğine koddan hello ile değiştirin. Merhaba devralınan sınıfı SampleEventSourceWriter, hello [EventSource sınıfı][EventSource Class], dört günlük yöntemlerini uygular: **SendEnums**, **MessageMethod** , **SetOther** ve **HighFreq**. İlk parametre toohello hello **WriteEvent** yöntemi hello ilgili olay hello kimliği tanımlar. Merhaba Run yöntemi uygulayan her hello hello uygulanan günlük yöntemlerini çağıran sonsuz bir döngüde **SampleEventSourceWriter** 10 saniyede sınıfı.

```csharp
using Microsoft.WindowsAzure.ServiceRuntime;
using System;
using System.Diagnostics;
using System.Diagnostics.Tracing;
using System.Net;
using System.Threading;

namespace WorkerRole1
{
    sealed class SampleEventSourceWriter : EventSource
    {
        public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
        public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); }// Cast enums tooint for efficient logging.
        public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
        public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
        public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }

    }

    enum MyColor
    {
        Red,
        Blue,
        Green
    }

    [Flags]
    enum MyFlags
    {
        Flag1 = 1,
        Flag2 = 2,
        Flag3 = 4
    }

    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
            // This is a sample worker implementation. Replace with your logic.
            Trace.TraceInformation("WorkerRole1 entry point called");

            int value = 0;

            while (true)
            {
                Thread.Sleep(10000);
                Trace.TraceInformation("Working");

                // Emit several events every time we go through hello loop
                for (int i = 0; i < 6; i++)
                {
                    SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
                }

                for (int i = 0; i < 3; i++)
                {
                    SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                    SampleEventSourceWriter.Log.SetOther(true, 123456789);
                }

                if (value == int.MaxValue) value = 0;
                SampleEventSourceWriter.Log.HighFreq(value++);
            }
        }

        public override bool OnStart()
        {
            // Set hello maximum number of concurrent connections
            ServicePointManager.DefaultConnectionLimit = 12;

            // For information on handling configuration changes
            // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.

            return base.OnStart();
        }
    }
}
```


### <a name="step-3-deploy-your-worker-role"></a>Adım 3: çalışan rolünüzün dağıtma

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. Merhaba seçerek, çalışan rolü tooAzure gelen Visual Studio içinde dağıtmak **WadExample** sonra Çözüm Gezgini hello bir projede **Yayımla** hello gelen **yapı** menüsü.
2. Aboneliğinizi seçin.
3. Merhaba, **Microsoft Azure yayımlama ayarları** iletişim kutusunda **yeni oluştur...** .
4. Merhaba, **bulut hizmeti oluşturma ve depolama hesabı** iletişim kutusunda, girin bir **adı** (örneğin, "WadExample") ve bir bölge veya benzeşim grubu seçin.
5. Set hello **ortam** çok**hazırlama**.
6. Diğer değiştirme **ayarları** olarak uygun ve tıklatın **Yayımla**.
7. Merhaba, bulut hizmeti olan Azure Portalı'nda dağıtım tamamlandıktan sonra onaylayın bir **çalıştıran** durumu.

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-hello-extension"></a>4. adım: Tanılama yapılandırma dosyanızı oluşturun ve hello uzantısını yükle
1. Merhaba ortak yapılandırma dosyası şeması tanımı hello aşağıdaki PowerShell komutunu yürüterek yükleyin:

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. Bir XML dosyası tooyour ekleme **WorkerRole1** hello üzerinde sağ tıklanarak proje **WorkerRole1** proje ve seçin **Ekle** -> **yeni öğe...** -> **Visual C# öğeleri** -> **veri** -> **XML dosyası**. "WadExample.xml" Merhaba dosya adı.

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. Merhaba WadConfig.xsd hello yapılandırma dosyası ile ilişkilendirin. Merhaba WadExample.xml Düzenleyicisi penceresinde hello etkin pencereyi olduğundan emin olun. Tuşuna **F4** tooopen hello **özellikleri** penceresi. Merhaba tıklatın **şemaları** hello özelliğinde **özellikleri** penceresi. Merhaba tıklatın **...** Merhaba, **şemaları** özelliği. Merhaba tıklatın **Ekle...** düğme ve hello XSD dosyası ve select hello dosya WadConfig.xsd kaydettiğiniz toohello konuma gidin. **Tamam** düğmesine tıklayın.

4. Merhaba WadExample.xml yapılandırma dosyası Hello içeriğini hello dosyayı Kaydet XML aşağıdaki hello ile değiştirin. Bu yapılandırma dosyası birkaç performans sayaçları toocollect tanımlar: CPU kullanımı, diğeri bellek kullanımı için. Ardından hello yapılandırmasını hello SampleEventSourceWriter sınıfı toohello yöntemleri karşılık gelen hello dört olayları tanımlar.

```xml
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="25000">
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT1M" unit="bytes"/>
      </PerformanceCounters>
      <EtwProviders>
        <EtwEventSourceProviderConfiguration provider="SampleEventSourceWriter" scheduledTransferPeriod="PT5M">
          <Event id="1" eventDestination="EnumsTable"/>
          <Event id="2" eventDestination="MessageTable"/>
          <Event id="3" eventDestination="SetOtherTable"/>
          <Event id="4" eventDestination="HighFreqTable"/>
          <DefaultEvents eventDestination="DefaultTable" />
        </EtwEventSourceProviderConfiguration>
      </EtwProviders>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```

### <a name="step-5-install-diagnostics-on-your-worker-role"></a>5. adım: Tanılama, çalışan rolü yükleyin.
Merhaba tanılama bir web veya çalışan rolü yönetmek için PowerShell cmdlet'leri şunlardır: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension ve Kaldır-AzureServiceDiagnosticsExtension.

1. Azure PowerShell'i açın.
2. Çalışan rolünüzün Hello betik tooinstall tanılama yürütme (Değiştir *StorageAccountKey* hello depolama hesabınızın anahtarıyla wadexample depolama hesabınız için ve *config_path* hello yolu ile toohello *WadExample.xml* dosyası):

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a>6. adım: Telemetri verilerinizi bakma
Merhaba Visual Studio içinde **Sunucu Gezgini**, toohello wadexample depolama hesabına gidin. Yaklaşık beş (5) dakika Hello bulut hizmeti yürütüldükten sonra hello tabloları görmelisiniz **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** ve **WADSetOtherTable**. Toplanan hello tabloları tooview hello telemetri birini çift tıklatın.

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a>Yapılandırma dosyası şeması
Merhaba tanılama yapılandırma dosyası hello Tanılama aracı başladığında kullanılan tooinitialize tanılama yapılandırma ayarlarının değerleri tanımlar. Merhaba bkz [en son şema başvurusu](https://msdn.microsoft.com/library/azure/mt634524.aspx) geçerli değerler ve örnekler için.

## <a name="troubleshooting"></a>Sorun giderme
Konusunda sorun yaşıyorsanız, bkz: [sorun giderme Azure tanılama](../azure-diagnostics-troubleshooting.md) sık karşılaşılan sorunları ile ilgili Yardım.

## <a name="next-steps"></a>Sonraki Adımlar
[İlgili Azure sanal makinesi tanılama makaleler listesini görmek](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) toochange hello verileri toplama, sorunları gidermek veya Tanılama hakkında daha fazla genel bilgi.

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
