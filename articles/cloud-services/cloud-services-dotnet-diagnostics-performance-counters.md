---
title: "Azure tanılama performans sayaçları aaaUse | Microsoft Docs"
description: "Performansı ayarlamak ve performans sayaçları Azure bulut Hizmetleri veya sanal makine toofind performans sorunlarını kullanın."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: f3250816c01fc6e164a6aae48da5035845e6d2b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a>Oluşturma ve bir Azure uygulamasında performans sayaçlarını kullanma
Bu makalede hello avantajları ve nasıl Azure uygulamanıza tooput performans sayaçları açıklanmaktadır. Toocollect verileri kullanmak, engelleri bulun ve sistem ve uygulama performansı ayarlamak.

Windows Server, IIS ve ASP.NET için kullanılabilen performans sayaçlarının de toplanabilir ve toodetermine hello durumunu Azure web rolleri, çalışan rolleri ve sanal makineleri kullanılır. Ayrıca, oluşturabilir ve özel performans sayaçları kullanın.  

Performans sayacı verilerini inceleyebilirsiniz

1. Doğrudan hello uygulama ana bilgisayarda Uzak Masaüstü kullanarak erişilen hello Performans İzleyicisi aracıyla
2. System Center Operations Manager kullanarak Azure Management Pack Merhaba
3. Merhaba erişim diğer izleme araçları ile tanılama veri tooAzure depolama aktarılan. Bkz: [deposu ve görünüm tanılama verilerini Azure storage'da](https://msdn.microsoft.com/library/azure/hh411534.aspx) daha fazla bilgi için.  

Merhaba, uygulamanızda hello performansını izleme hakkında daha fazla bilgi için [Azure portal](http://portal.azure.com/), bkz: [tooMonitor Cloud Services nasıl](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).

Bir günlük oluşturma ve stratejisi izleme ve tanılama ve diğer teknikleri tootroubleshoot sorunları kullanarak ek ayrıntılı yönergeler için ve Azure uygulamalarını en iyi duruma getirme, bkz: [Azure geliştirmek için en iyi uygulamaları sorunlarını giderme Uygulamaları](https://msdn.microsoft.com/library/azure/hh771389.aspx).

## <a name="enable-performance-counter-monitoring"></a>Performans sayacı izlemeyi etkinleştir
Performans sayaçları varsayılan olarak etkin değildir. Uygulamanızın veya bir başlangıç görevi her rol örneği toomonitor istediğiniz Aracısı Yapılandırma tooinclude hello belirli performans sayaçları hello varsayılan tanılama değiştirmeniz gerekir.

### <a name="performance-counters-available-for-microsoft-azure"></a>Microsoft Azure için kullanılabilen performans sayaçlarının
Azure, Windows Server, IIS ve ASP.NET yığını hello hello performans sayaçları kümesini sağlar. Merhaba aşağıdaki tabloda bazı Azure uygulamaları için özellikle ilgisini çeken hello performans sayaçları listeler.

| Sayacı Kategori: Nesnesi (örneği) | Sayaç adı | Başvuru |
| --- | --- | --- |
| .NET CLR özel durumları (*genel*) |# Durum / sn |Özel durum performans sayaçları |
| .NET CLR bellek (*genel*) |GC % zaman |Bellek performansı sayaçları |
| ASP.NET |Uygulama yeniden başlatma |ASP.NET için performans sayaçları |
| ASP.NET |İstek Yürütme Süresi |ASP.NET için performans sayaçları |
| ASP.NET |Bağlantısı kesilen istek sayısı |ASP.NET için performans sayaçları |
| ASP.NET |Çalışan işlemi yeniden başlatılır |ASP.NET için performans sayaçları |
| ASP.NET uygulamaları (**toplam**) |Toplam istek sayısı |ASP.NET için performans sayaçları |
| ASP.NET uygulamaları (**toplam**) |İsteği/sn |ASP.NET için performans sayaçları |
| ASP.NET v4.0.30319 |İstek Yürütme Süresi |ASP.NET için performans sayaçları |
| ASP.NET v4.0.30319 |İstek Bekleme süresi |ASP.NET için performans sayaçları |
| ASP.NET v4.0.30319 |İstek geçerli |ASP.NET için performans sayaçları |
| ASP.NET v4.0.30319 |Sıraya alınan istek sayısı |ASP.NET için performans sayaçları |
| ASP.NET v4.0.30319 |Reddedilen istek sayısı |ASP.NET için performans sayaçları |
| Bellek |Kullanılabilir MBayt |Bellek performansı sayaçları |
| Bellek |Kaydedilmiş Bayt |Bellek performansı sayaçları |
| İşlemci(_Toplam) |% İşlemci zamanı |ASP.NET için performans sayaçları |
| TCPv4 |Bağlantı hataları |TCP nesnesi |
| TCPv4 |Kurulan bağlantılar |TCP nesnesi |
| TCPv4 |Bağlantıları Sıfırla |TCP nesnesi |
| TCPv4 |Kesim gönderilen/sn |TCP nesnesi |
| Ağ Interface(*) |Alınan Bayt/sn |Ağ arabirimi nesnesi |
| Ağ Interface(*) |Gönderilen bayt/sn |Ağ arabirimi nesnesi |
| Ağ arabirimi (Microsoft sanal makine veri yolu ağ bağdaştırıcısı _2) |Alınan Bayt/sn |Ağ arabirimi nesnesi |
| Ağ arabirimi (Microsoft sanal makine veri yolu ağ bağdaştırıcısı _2) |Gönderilen bayt/sn |Ağ arabirimi nesnesi |
| Ağ arabirimi (Microsoft sanal makine veri yolu ağ bağdaştırıcısı _2) |Toplam Bayt/sn |Ağ arabirimi nesnesi |

## <a name="create-and-add-custom-performance-counters-tooyour-application"></a>Oluşturma ve özel performans sayaçları tooyour uygulama ekleme
Azure destek toocreate sahiptir ve web rolleri ve çalışan rolleri için özel performans sayaçları değiştirin. Merhaba sayaçları kullanılan tootrack ve İzleyici uygulamaya özgü davranışını olabilir. Oluşturun ve bir başlangıç görevi, web rolü ve çalışan rolü yükseltilmiş izinleri olan özel performans sayacı kategorileri ve tanımlayıcıları silin.

> [!NOTE]
> Toocustom performans sayaçları değişiklikleri yapar kod izinleri toorun yükseltilmiş gerekir. Merhaba kodu bir web rolü veya çalışan rolü ise hello rolü hello etiketi içermelidir <Runtime executionContext="elevated" /> hello ServiceDefinition.csdef hello rol tooinitialize için doğru dosya.
>
>

Özel performans sayacı verileri tooAzure depolama hello Tanılama aracı kullanarak gönderebilirsiniz.

Merhaba standart performans sayacı verilerini hello Azure işler tarafından oluşturulur. Özel performans sayacı verilerini, web rolü ya da çalışan rolü uygulamanız tarafından oluşturulmuş olması gerekir. Bkz: [performans sayacı türleri](https://msdn.microsoft.com/library/z573042h.aspx) hello özel performans sayaçları depolanan veri türleri hakkında bilgi için. Bkz: [performans sayaçları örnek](http://code.msdn.microsoft.com/azure/) oluşturur ve bir web rolünde özel performans sayacı verilerini ayarlayan bir örnek.

## <a name="store-and-view-performance-counter-data"></a>Depolama ve görünüm performans sayacı verileri
Azure tanılama diğer bilgilerle performans sayacı verileri önbelleğe alır. Bu veriler, Performans İzleyicisi gibi uzak masaüstü erişimi tooview araçları kullanarak hello rol örneği çalışırken, Uzaktan izleme için kullanılabilir. toopersist hello veri hello rol örneği dışında hello Tanılama Aracı hello veri tooAzure depolama aktarmanız gerekir. önbelleğe alınmış hello performans sayacı verilerini Hello boyut sınırını hello Tanılama Aracı yapılandırılabilir veya olabilir tüm tanılama veri hello için paylaşılan bir sınır toobe parçası yapılandırılmış. Merhaba arabellek boyutunu ayarlama hakkında daha fazla bilgi için bkz: [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) ve [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx). Bkz: [deposu ve görünüm tanılama verilerini Azure storage'da](https://msdn.microsoft.com/library/azure/hh411534.aspx) hello Tanılama Aracı tootransfer veri tooa depolama hesabı kurma genel bir bakış için.

Her yapılandırılmış performans sayacı örneği belirtilen örnekleme hızında kaydedilir ve örneklenen hello veriler aktarılır toohello depolama hesabı zamanlanmış aktarım isteği veya isteğe bağlı aktarım isteği. Otomatik aktarımları olarak dakikada bir kez sıklıkta zamanlanabilir. Performans sayacı verilerini Hello Tanılama aracı tarafından aktarılan bir tablo, WADPerformanceCountersTable, hello depolama hesabında depolanır. Bu tablo erişilen ve standart Azure depolama API yöntemleriyle sorgulanan. Bkz: [Microsoft Azure performans sayaçları örnek](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) sorgulama ve performans sayacı verilerini hello WADPerformanceCountersTable tablosundan görüntüleyen bir örnek.

> [!NOTE]
> Merhaba Tanılama Aracı aktarımı sıklığı ve sıra gecikme bağlı olarak, hello hello depolama hesabındaki en son performans sayacı verilerini birkaç dakika eski olabilir.
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a>Tanılama yapılandırma dosyası kullanarak performans sayaçları sağlar
Azure uygulamanızda yordamı tooenable performans sayaçlarını izleyerek hello kullanın.

## <a name="prerequisites"></a>Ön koşullar
Bu bölümde, uygulamanıza hello Tanılama izleme alınan ve hello tanılama yapılandırma dosyası tooyour Visual Studio çözümü (diagnostics.wadcfg SDK 2.4 ve aşağıda veya diagnostics.wadcfgx SDK 2.5 ve üzeri) eklenen varsayar. Adım 1 ve 2'de bkz [Azure Cloud Services ve sanal makineleri etkinleştirme tanılamada](cloud-services-dotnet-diagnostics.md)) daha fazla bilgi için.

## <a name="step-1-collect-and-store-data-from-performance-counters"></a>1. adım: Toplamak ve performans sayaçlarını veri depolama
Merhaba tanılama tooyour Visual Studio çözümü dosya ekledikten sonra bir Azure uygulamasında hello toplama ve performans sayacı verilerinin depolanması yapılandırabilirsiniz. Bu, performans sayaçları toohello tanılama dosyasını ekleyerek yapılır. Tanılama verilerini, performans sayaçları dahil olmak üzere, ilk hello örneğinde toplanır. kalıcı toohello WADPerformanceCountersTable tablo sonra hello Azure tablo hizmeti hello veri, şunları yapacaksınız şekilde toospecify depolama hesabı, uygulamanızda da hello. Uygulamanızı yerel olarak hello işlem öykünücüsü test ettiğiniz, aynı zamanda tanılama verilerini yerel olarak hello depolama öykünücüsü saklayabilirsiniz. Tanılama verileri depolamak önce toohello önce geçmesi gereken [Azure portal](http://portal.azure.com/) ve klasik depolama hesabı oluşturun. En iyi toolocate depolama hesabınızdaki uygulamadır hello Azure uygulamanız aynı coğrafi konum. Tutma hello tarafından Azure uygulaması ve depolama hesabı olan içinde Merhaba coğrafi konuma, harici bant genişliği maliyetlerini ödeme yapmaktan kaçınmak ve gecikme süresini azaltmak.

### <a name="add-performance-counters-toohello-diagnostics-file"></a>Performans sayaçları toohello tanılama dosyası ekleme
Kullanabileceğiniz birçok sayaç vardır. Merhaba aşağıdaki örnek, web ve çalışan rolü izleme için önerilen birkaç performans sayaçlarını gösterir.

Merhaba tanılama dosyasını (diagnostics.wadcfg SDK 2.4 ve altı veya diagnostics.wadcfgx SDK 2.5 ve üzeri) açın ve toohello DiagnosticMonitorConfiguration öğesi aşağıdaki hello ekleyin:

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use hello Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use hello Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

Merhaba en hello koleksiyon için veri türü (Azure günlükleri, IIS günlükleri, vb.) kullanılabilir dosya sistemi depolama miktarını belirtir hello bufferQuotaInMB özniteliği. Merhaba varsayılan 0'dır. Merhaba kotasına ulaşıldığında, yeni veriler eklendikçe hello eski veriler silinir. Tüm hello bufferQuotaInMB özellikleri Hello toplamını hello OverallQuotaInMB özniteliği hello değerinden büyük olmalıdır. Ne kadar depolama tanılama verilerini hello koleksiyonu için gerekli olacak belirleme daha ayrıntılı bilgi için bkz: Merhaba Kurulum WAD bölümünü [Azure uygulamaları geliştirmek için en iyi uygulamaları sorunlarını giderme](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).

Zamanlanmış veri aktarımlarını hello aralığını belirtir, hello scheduledTransferPeriod özniteliği toohello minute en yakın yukarı yuvarlanmasını. Örnek hello tooPT30M (30 dakika) ayarlanır. Ayar hello aktarımı dönem tooa küçük gibi değer 1 dakika, üretim uygulamanızın performansını olumsuz yönde etkileyen ancak test hızlı çalışan tanılama görmek için kullanışlı olabilir. Merhaba zamanlanmış transfer süresi tanılama veri büyüklükte hello uygulamanızın performansını etkilemez ancak hello örneğinde üzerine değildir küçük tooensure olmalıdır.

Merhaba counterSpecifier özniteliği hello performans sayacı toocollect belirtir. Hello sampleRate özniteliği hello oranı aktarılma hello performans sayacı, bu durumda 30 saniye örneklenen belirtir.

Toocollect istediğiniz hello performans sayaçları ekledikten sonra değişiklikler toohello tanılama dosyanızı kaydedin. Ardından, hello tanılama verilerini için kalıcı toospecify hello depolama hesabınızın olması gerekir.

### <a name="specify-hello-storage-account"></a>Merhaba depolama hesabı belirtin
tanılama bilgileri tooyour Azure depolama hesabı, belirtmeniz gerekir toopersist, hizmet yapılandırma (ServiceConfiguration.cscfg) dosyasında bir bağlantı dizesi.

Azure SDK 2.5 için hello depolama hesabı hello diagnostics.wadcfgx dosyasında belirtilebilir.

> [!NOTE]
> Bu yönergeler yalnızca tooAzure SDK 2.4 geçerlidir ve aşağıdaki. Azure SDK 2.5 için hello depolama hesabı hello diagnostics.wadcfgx dosyasında belirtilebilir.
>
>

tooset hello bağlantı dizelerini:

1. Depolama alanınız için sık kullandığınız metin düzenleyiciyi ve kümesi hello bağlantı dizesi kullanarak hello ServiceConfiguration.Cloud.cscfg dosyasını açın. Merhaba *AccountName* ve *AccountKey* değerleri hello erişim tuşları altında hello depolama hesabı Panosu Azure portalında bulundu.

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. Merhaba ServiceConfiguration.Cloud.cscfg dosyasını kaydedin.
3. Merhaba ServiceConfiguration.Local.cscfg dosyasını açın ve UseDevelopmentStorage tootrue ayarlandığını doğrulayın.

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   Merhaba bağlantı dizelerini ayarlayın, uygulamanızın dağıtıldığında, uygulamanızın tanılama veri tooyour depolama hesabı korunur.
4. Kaydet ve projenizi yapılandırın ve ardından uygulamanızı dağıtın.

## <a name="step-2-optional-create-custom-performance-counters"></a>2. adım: (İsteğe bağlı) oluşturma özel performans sayaçları
Ayrıca toohello performans sayaçları önceden tanımlanmış, kendi özel performans sayaçları toomonitor web veya çalışan rolleri ekleyebilirsiniz. Özel performans sayaçları kullanılan tootrack ve İzleyici uygulamaya özgü davranış ve oluşturulabilir veya bir başlangıç görevi, web rolü ya da yükseltilmiş izinleri olan çalışan rolü silindi.

Hello Azure Tanılama Aracı hello performans sayacı yapılandırması başlattıktan bir dakika hello .wadcfg dosyasından yeniler.  Hello Azure Tanılama Aracı tooload çalıştığında hello OnStart yöntemi özel performans sayaçları oluşturursanız ve başlangıç görevleri bir dakika tooexecute uzun sürer, özel performans sayaçları oluşturulmuş değil bunları.  Bu senaryoda, Azure tanılama doğru özel performans sayaçları dışındaki tüm tanılama verilerini yakalar görürsünüz.  tooresolve bu sorunu hello performans sayaçlarını bir başlangıç görevi oluşturmak veya performans sayaçları hello oluşturduktan sonra başlangıç görevi bazıları toohello OnStart yöntemi iş taşıyın.

Aşağıdaki adımları toocreate sayaç "\MyCustomCounterCategory\MyButton1Counter" adlı basit bir özel performans hello gerçekleştirin:

1. Uygulamanız için Hello Hizmet tanım dosyası (CSDEF) açın.
2. Merhaba çalışma zamanı öğesi toohello WebRole veya örn öğesi tooallow yürütme yükseltilmiş ayrıcalıklarla ekleyin:

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. Merhaba dosyasını kaydedin.
4. Merhaba tanılama dosyasını (diagnostics.wadcfg SDK 2.4 ve altı veya diagnostics.wadcfgx SDK 2.5 ve üzeri) açın ve aşağıdaki toohello DiagnosticMonitorConfiguration hello ekleyin

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. Merhaba dosyasını kaydedin.
6. Merhaba özel performans sayacı kategorisi temel çağırmadan önce hello OnStart yönteminde, rolü oluşturun. OnStart. zaten yoksa, hello aşağıdaki C# örnek özel bir kategori oluşturur:

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. Merhaba sayaçları, uygulamanızda güncelleştirin. Aşağıdaki örneğine hello özel performans sayacı Button1_Click olayları güncelleştirir:

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. Merhaba dosyasını kaydedin.  

Özel performans sayacı verilerini şimdi hello Azure tanılama İzleyici tarafından toplanacaktır.

## <a name="step-3-query-performance-counter-data"></a>3. adım: performans sayacı verileri Sorgulama
Uygulamanız dağıtıldıktan sonra çalışmaya, hello Tanılama izleme başlayacak performans sayaçlarını toplama ve bu verileri tooAzure depolama kalıcı yapma. Visual Studio Araçları Sunucu Gezgini gibi kullandığınız [Azure Storage Gezgini](http://azurestorageexplorer.codeplex.com/), veya [Azure tanılama Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) Cerebrata tarafından hello verilerde tooview hello performans sayaçları WADPerformanceCountersTable tablo. Merhaba tablo hizmetini kullanarak program aracılığıyla da sorgulayabilirsiniz [C#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), veya [PHP](../cosmos-db/table-storage-how-to-use-php.md).

Merhaba aşağıdaki C# örnek temel bir hello WADPerformanceCountersTable Tablo sorgusu gösterir ve hello tanılama veri tooa CSV dosyası kaydeder. Merhaba performans sayaçları tooa CSV dosyası kaydedildikten sonra Microsoft Excel veya bazı diğer aracı toovisualize hello veri özellikleri Grafikleme hello kullanabilirsiniz. Emin tooadd hello Azure SDK'sı .NET Ekim 2012 ve üzeri için dahil edilen bir başvuru tooMicrosoft.WindowsAzure.Storage.dll olabilir. Merhaba, yüklü toohello % Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ dizini derlemesidir.

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get hello connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using hello Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use hello CloudConfigurationManager type
// tooretrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store hello connection string in your web.config or app.config file.
// Use hello ConfigurationManager type tooretrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference toohello storage account using hello connection string.  You can also use hello development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create hello table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute hello table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process hello query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

Varlıkları eşleme türetilen özel bir sınıf kullanarak tooC # nesnelerini **TableEntity**. Merhaba aşağıdaki kod bir performans sayacının hello temsil eden bir varlık sınıfı tanımlar **WADPerformanceCountersTable** tablo.

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a>Sonraki Adımlar
[Azure tanılama üzerinde ek makaleleri görüntüleme](../azure-diagnostics.md)
