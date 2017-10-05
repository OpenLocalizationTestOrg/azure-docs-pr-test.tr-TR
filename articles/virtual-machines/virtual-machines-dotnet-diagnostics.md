---
title: "Sanal makinelerin Azure Tanılama'yı kullanma | Microsoft Docs"
description: "Hata ayıklama, performans, izleme, trafik analizi ve daha fazla ölçmek için Azure sanal makinelerden veri toplamak üzere Azure Tanılama'yı kullanarak."
services: virtual-machines
documentationcenter: .net
author: davidmu1
manager: 
editor: 
ms.assetid: dfaabc7a-23e7-4af0-8369-f504d2915b3d
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/16/2016
ms.author: davidmu
ms.openlocfilehash: 8ff6b9825212359617b748aba1c78ed789b130dd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a>Azure sanal makinelerde tanılama etkinleştirme
Bkz: [Azure tanılama genel bakış](../monitoring-and-diagnostics/azure-diagnostics.md) bir arka planda Azure tanılama için.

## <a name="how-to-enable-diagnostics-in-a-virtual-machine"></a>Bir sanal makinede tanılamayı etkinleştirme
Bu ilerlemesi aracılığıyla uzaktan tanılama bir Azure sanal makinesi için bir geliştirme bilgisayardan nasıl yükleneceğini açıklar. Bu Azure sanal makine üzerinde çalışan ve .NET ile telemetri verilerini yayar uygulamanın uygulama da bilgi [EventSource sınıfı][EventSource Class]. Azure tanılama telemetri toplamak ve bir Azure depolama hesabında depolamak için kullanılır.

### <a name="pre-requisites"></a>Ön koşullar
Bir Azure aboneliğiniz varsa ve Azure SDK ile Visual Studio 2017 kullanıyorsanız bu ilerlemesi aracılığıyla varsayar. Bir Azure aboneliğiniz yoksa için kaydolabilirsiniz [ücretsiz deneme][Free Trial]. Emin olun [yükleyin ve Azure PowerShell sürüm 0.8.7 yapılandırın veya daha sonra][Install and configure Azure PowerShell version 0.8.7 or later].

### <a name="step-1-create-a-virtual-machine"></a>1. adım: bir sanal makine oluşturma
1. Geliştirme bilgisayarınızda Visual Studio 2017 başlatın.
2. Visual Studio'da **Sunucu Gezgini** genişletin **Azure**, sağ **sanal makineleri** seçip **sanal makine oluşturma**.
3. Azure aboneliğinizde seçin **bir abonelik seçin** tıklayın ve iletişim **sonraki**.
4. Seçin **Windows Server 2012 R2 Datacenter, Haziran 2017** içinde **bir sanal makine görüntüsü seçin** tıklayın ve iletişim **sonraki**.
5. İçinde **sanal makine temel ayarlarını**, sanal makine adı "wadexample" olarak ayarlayın. Yönetici kullanıcı adı ve parola ayarlayın ve tıklayın **sonraki**.
6. İçinde **bulut hizmeti ayarlarını** "wadexampleVM" adlı yeni bir bulut hizmeti Oluştur iletişim kutusu. "Wadexample" adlı yeni bir depolama hesabı oluşturmak ve tıklayın **sonraki**.
7. **Oluştur**'a tıklayın.

### <a name="step-2-create-your-application"></a>2. adım: uygulamanızı oluşturma
1. Geliştirme bilgisayarınızda Visual Studio 2017 başlatın.
2. Yeni bir Visual C# konsol .NET Framework 4. 5'i hedefleyen uygulaması oluşturun. Projeyi "WadExampleVM" olarak adlandırın.

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. Program.cs içeriğini aşağıdaki kodla değiştirin. Sınıf **SampleEventSourceWriter** dört günlük yöntemlerini uygular: **SendEnums**, **MessageMethod**, **SetOther** ve  **HighFreq**. İlk parametre WriteEvent yöntemi olarak ilgili olay kimliği tanımlar. Run yöntemi uygulanan günlük yöntemlerin her biri çağırır sonsuz bir döngüde uygulayan **SampleEventSourceWriter** 10 saniyede sınıfı.

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums to int for efficient logging.
         public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
         public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
         public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }
       }

       enum MyColor {
         Red,
         Blue,
         Green
       }

       [Flags]
       enum MyFlags {
         Flag1 = 1,
         Flag2 = 2,
         Flag3 = 4
       }

       class Program
       {
         static void Main(string[] args) {
         Trace.TraceInformation("My application entry point called");

         int value = 0;

         while (true) {
             Thread.Sleep(10000);
             Trace.TraceInformation("Working");

             // Emit several events every time we go through the loop
             for (int i = 0; i < 6; i++) {
                 SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
             }

             for (int i = 0; i < 3; i++) {
                 SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                 SampleEventSourceWriter.Log.SetOther(true, 123456789);
             }

             if (value == int.MaxValue) value = 0;
             SampleEventSourceWriter.Log.HighFreq(value++);
         }

        }
      }
     }
     ```
4. Dosyayı kaydedin ve seçin **yapı çözümü** gelen **yapı** kodunuzu oluşturmak için menüsü.

### <a name="step-3-deploy-your-application"></a>3. adım: uygulamanızı dağıtma
1. Sağ tıklayın **WadExampleVM** proje **Çözüm Gezgini** ve **dosya Gezgini'nde klasör Aç**.
2. Gidin *bin\Debug* klasör ve tüm dosyalar (WadExampleVM.*) kopyalayın
3. İçinde **Sunucu Gezgini** sanal makineye sağ tıklayın ve seçin **Uzak Masaüstü kullanarak bağlanmak**.
4. VM bağlandıktan sonra WadExampleVM ve uygulamanızı klasöre dosyaları Yapıştır adlı bir klasör oluşturun.
5. Uygulama WadExampleVM.exe başlatın. Boş konsol penceresini görmeniz gerekir.

### <a name="step-4-create-your-diagnostics-configuration-and-install-the-extension"></a>4. adım: Tanılama yapılandırmanızı oluşturun ve uzantısını yükle
1. Genel yapılandırma dosyası şeması tanımı aşağıdaki PowerShell komutunu yürüterek geliştirme bilgisayarınıza indirin:

     (Get-AzureServiceAvailableExtension - UzantıAdı 'PaaSDiagnostics' - ProviderNamespace 'Microsoft.Azure.Diagnostics'). PublicConfigurationSchema | Out-File-kodlama utf8 - FilePath 'WadConfig.xsd'
2. Visual Studio'da, zaten açık veya Visual Studio'da örnek projesinde açık projeler ile ya da yeni bir XML dosyası açın. Visual Studio'da seçin **Ekle** -> **yeni öğe...** -> **Visual C# öğeleri** -> **veri** -> **XML dosyası**. "WadExample.xml" dosya adı
3. WadConfig.xsd yapılandırma dosyası ile ilişkilendirin. Etkin pencereyi WadExample.xml Düzenleyicisi penceresini olduğundan emin olun. Tuşuna **F4** açmak için **özellikleri** penceresi. Tıklayın **şemaları** özelliğinde **özellikleri** penceresi. Tıklatın **...** içinde **şemaları** özelliği. **Ekle…** düğmesine düğmesini ve XSD dosyasını kaydettiğiniz konuma gidin ve WadConfig.xsd dosyasını seçin. **Tamam** düğmesine tıklayın.
4. Aşağıdaki XML WadExample.xml yapılandırma dosyasının içeriğini değiştirin ve dosyayı kaydedin. Bu yapılandırma dosyasını toplamak için birkaç performans sayaçlarını tanımlar: CPU kullanımı, diğeri bellek kullanımı için. Ardından yapılandırmasını SampleEventSourceWriter sınıftaki yöntemlerin karşılık gelen dört olayları tanımlar.

```
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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a>5. adım: Azure sanal makinenize tanılama uzaktan yükleyin.
Bir VM'de tanılama yönetmek için PowerShell cmdlet'leri şunlardır: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension ve Kaldır-AzureVMDiagnosticsExtension.

1. Geliştirici bilgisayarınızda Azure PowerShell açın.
2. Tanılama VM üzerinde uzaktan yüklemek için komut dosyası yürütme (Değiştir `<user>` kullanıcı dizin adı. Değiştir `<StorageAccountKey>` wadexamplevm depolama hesabınız için depolama hesabınızın anahtarıyla):
```
     $storage_name = "wadexamplevm"
     $key = "<StorageAccountKey>"
     $config_path="c:\users\<user>\documents\visual studio 2017\Projects\WadExampleVM\WadExampleVM\WadExample.xml"
     $service_name="wadexamplevm"
     $vm_name="WadExample"
     $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
     $VM1 = Get-AzureVM -ServiceName $service_name -Name $vm_name
     $VM2 = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $config_path -Version "1.*" -VM $VM1 -StorageContext $storageContext
     $VM3 = Update-AzureVM -ServiceName $service_name -Name $vm_name -VM $VM2.VM
```
### <a name="step-6-look-at-your-telemetry-data"></a>6. adım: Telemetri verilerinizi bakma
Visual Studio'da **Sunucu Gezgini** wadexample depolama hesabınıza gidin. VM yaklaşık 5 dakika yürütüldükten sonra tabloları görmelisiniz **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**,  **WADPerformanceCountersTable** ve **WADSetOtherTable**. Toplanan telemetri görüntülemek için tablolar birine çift tıklayın.

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a>Yapılandırma dosyası şeması
Tanılama yapılandırma dosyası Tanılama aracı başladığında tanılama yapılandırma ayarlarını başlatmak için kullanılan değerleri tanımlar. Bkz: [en son şema başvurusu](https://msdn.microsoft.com/library/azure/mt634524.aspx) geçerli değerler ve örnekler için.

## <a name="troubleshooting"></a>Sorun giderme
Bkz: [sorun giderme Azure tanılama](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) daha fazla bilgi için.

## <a name="next-steps"></a>Sonraki adımlar
[Bkz: sanal makine listesini makaleler Azure tanılama](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) toplama verileri değiştirmek için ilgili sorunları giderme veya Tanılama hakkında daha fazla genel bilgi edinin.

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
