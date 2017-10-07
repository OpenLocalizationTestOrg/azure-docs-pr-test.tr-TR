---
title: "aaaHow toouse sanal makinelerinde Azure tanılama | Microsoft Docs"
description: "Azure tanılama toogather verilerini Azure sanal makineleri gelen hata ayıklama, performans, izleme, trafik analizi ve daha fazla ölçmek için kullanma."
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
ms.openlocfilehash: 54cdfd30d7bbbb71af449826e90234faf5ecdf44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a>Azure sanal makinelerde tanılama etkinleştirme
Bkz: [Azure tanılama genel bakış](../monitoring-and-diagnostics/azure-diagnostics.md) bir arka planda Azure tanılama için.

## <a name="how-tooenable-diagnostics-in-a-virtual-machine"></a>Nasıl tooEnable bir sanal makinede tanılama
Bu ilerlemesi üzerinden nasıl tooremotely yükleme tanılama tooan Azure sanal makinesi bir geliştirme bilgisayardan açıklar. Nasıl tooimplement, Azure sanal makinede çalışan ve telemetri verilerini kullanarak yayar bir uygulama hello .NET da bilgi [EventSource sınıfı][EventSource Class]. Azure tanılama kullanılan toocollect hello telemetri olduğundan ve bir Azure depolama hesabında saklayın.

### <a name="pre-requisites"></a>Ön koşullar
Bir Azure aboneliğiniz varsa ve Visual Studio 2017 hello Azure SDK'sı ile kullanıyorsanız bu ilerlemesi aracılığıyla varsayar. Bir Azure aboneliğiniz yoksa, hello için kaydolabilirsiniz [ücretsiz deneme][Free Trial]. Emin olun çok[yükleyin ve Azure PowerShell sürüm 0.8.7 yapılandırın veya daha sonra][Install and configure Azure PowerShell version 0.8.7 or later].

### <a name="step-1-create-a-virtual-machine"></a>1. adım: bir sanal makine oluşturma
1. Geliştirme bilgisayarınızda Visual Studio 2017 başlatın.
2. Merhaba Visual Studio içinde **Sunucu Gezgini** genişletin **Azure**, sağ **sanal makineleri** seçip **sanal makine oluşturma**.
3. Hello Azure aboneliğinizi seçin **bir abonelik seçin** tıklayın ve iletişim **sonraki**.
4. Seçin **Windows Server 2012 R2 Datacenter, Haziran 2017** hello içinde **bir sanal makine görüntüsü seçin** tıklayın ve iletişim **sonraki**.
5. Merhaba, **sanal makine temel ayarlarını**, hello sanal makine adı çok Ayarla "wadexample". Yönetici kullanıcı adı ve parola ayarlayın ve tıklayın **sonraki**.
6. Merhaba, **bulut hizmeti ayarlarını** "wadexampleVM" adlı yeni bir bulut hizmeti Oluştur iletişim kutusu. "Wadexample" adlı yeni bir depolama hesabı oluşturmak ve tıklayın **sonraki**.
7. **Oluştur**'a tıklayın.

### <a name="step-2-create-your-application"></a>2. adım: uygulamanızı oluşturma
1. Geliştirme bilgisayarınızda Visual Studio 2017 başlatın.
2. Yeni bir Visual C# konsol .NET Framework 4. 5'i hedefleyen uygulaması oluşturun. Merhaba projeyi "WadExampleVM" olarak adlandırın.

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. Program.cs içeriğini Hello koddan hello ile değiştirin. Merhaba sınıfı **SampleEventSourceWriter** dört günlük yöntemlerini uygular: **SendEnums**, **MessageMethod**, **SetOther** ve  **HighFreq**. Merhaba ilk parametre toohello WriteEvent yöntemi hello ilgili olay hello kimliği tanımlar. Merhaba Run yöntemi uygulayan her hello hello uygulanan günlük yöntemlerini çağıran sonsuz bir döngüde **SampleEventSourceWriter** 10 saniyede sınıfı.

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums tooint for efficient logging.
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

             // Emit several events every time we go through hello loop
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
4. Merhaba dosyayı kaydedin ve seçin **yapı çözümü** hello gelen **yapı** menü toobuild kodunuzu.

### <a name="step-3-deploy-your-application"></a>3. adım: uygulamanızı dağıtma
1. Hello üzerinde sağ **WadExampleVM** proje **Çözüm Gezgini** ve **dosya Gezgini'nde klasör Aç**.
2. Toohello gidin *bin\Debug* klasörünü ve tüm hello kopyalama dosyaları (WadExampleVM.*)
3. İçinde **Sunucu Gezgini** hello sanal makineye sağ tıklayın ve seçin **Uzak Masaüstü kullanarak bağlanmak**.
4. Toohello VM bağlandıktan sonra WadExampleVM adlı bir klasör oluşturun ve uygulama dosyalarınızı hello klasöre yapıştırın.
5. Merhaba uygulaması WadExampleVM.exe başlatın. Boş konsol penceresini görmeniz gerekir.

### <a name="step-4-create-your-diagnostics-configuration-and-install-hello-extension"></a>4. adım: Tanılama yapılandırmanızı oluşturun ve hello uzantısını yükleyin
1. Hello ortak yapılandırma dosyası şeması tanımı tooyour geliştirme bilgisayarınızda hello aşağıdaki PowerShell komutunu yürüterek yükleyin:

     (Get-AzureServiceAvailableExtension - UzantıAdı 'PaaSDiagnostics' - ProviderNamespace 'Microsoft.Azure.Diagnostics'). PublicConfigurationSchema | Out-File-kodlama utf8 - FilePath 'WadConfig.xsd'
2. Visual Studio'da, zaten açık veya Visual Studio'da örnek projesinde açık projeler ile ya da yeni bir XML dosyası açın. Visual Studio'da seçin **Ekle** -> **yeni öğe...** -> **Visual C# öğeleri** -> **veri** -> **XML dosyası**. "WadExample.xml" Merhaba dosya adı
3. Merhaba WadConfig.xsd hello yapılandırma dosyası ile ilişkilendirin. Merhaba WadExample.xml Düzenleyicisi penceresinde hello etkin pencereyi olduğundan emin olun. Tuşuna **F4** tooopen hello **özellikleri** penceresi. Tıklatın hello üzerinde **şemaları** hello özelliğinde **özellikleri** penceresi. Merhaba tıklatın **...** Merhaba, **şemaları** özelliği. Merhaba tıklatın **Ekle...** düğme ve hello XSD dosyası ve select hello dosya WadConfig.xsd kaydettiğiniz toohello konuma gidin. **Tamam** düğmesine tıklayın.
4. Merhaba WadExample.xml yapılandırma dosyası Hello içeriğini hello dosyayı Kaydet XML aşağıdaki hello ile değiştirin. Bu yapılandırma dosyası birkaç performans sayaçları toocollect tanımlar: CPU kullanımı, diğeri bellek kullanımı için. Ardından hello yapılandırmasını hello SampleEventSourceWriter sınıfı toohello yöntemleri karşılık gelen hello dört olayları tanımlar.

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
Merhaba bir VM'de tanılama yönetmek için PowerShell cmdlet'leri şunlardır: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension ve Kaldır-AzureVMDiagnosticsExtension.

1. Geliştirici bilgisayarınızda Azure PowerShell açın.
2. Merhaba betik tooremotely yükleme tanılama VM üzerinde yürütme (Değiştir `<user>` kullanıcı dizin adı. Değiştir `<StorageAccountKey>` hello depolama hesabınızın anahtarıyla wadexamplevm depolama hesabınız için):
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
Merhaba Visual Studio içinde **Sunucu Gezgini** toohello wadexample depolama hesabına gidin. VM yaklaşık 5 dakika çalışıyor hello sonra hello tabloları görmelisiniz **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**,  **WADPerformanceCountersTable** ve **WADSetOtherTable**. Toplanan hello tabloları tooview hello telemetri birine çift tıklayın.

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a>Yapılandırma dosyası şeması
Merhaba tanılama yapılandırma dosyası hello Tanılama aracı başladığında kullanılan tooinitialize tanılama yapılandırma ayarlarının değerleri tanımlar. Merhaba bkz [en son şema başvurusu](https://msdn.microsoft.com/library/azure/mt634524.aspx) geçerli değerler ve örnekler için.

## <a name="troubleshooting"></a>Sorun giderme
Bkz: [sorun giderme Azure tanılama](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) daha fazla bilgi için.

## <a name="next-steps"></a>Sonraki adımlar
[Bkz: sanal makine listesini makaleler Azure tanılama](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) toochange hello verileri toplama, sorunları gidermek veya Tanılama hakkında daha fazla genel bilgi.

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
