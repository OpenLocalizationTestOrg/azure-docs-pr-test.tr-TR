---
title: ".NET uygulamaları için uygulama Öngörüler anlık görüntü hata ayıklayıcı aaaAzure | Microsoft Docs"
description: "Hata ayıklama anlık görüntüleri otomatik olarak üretim .NET uygulamaları özel durumlar, toplanan"
services: application-insights
documentationcenter: 
author: qubitron
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: bwren
ms.openlocfilehash: f0173a752b5795d934fbab1bd53eb077433edc90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a>Anlık görüntü özel durumları .NET uygulamalarında hata ayıklama

Özel durum oluştuğunda, hata ayıklama anlık görüntü canlı web uygulamanızı otomatik olarak toplayabilirsiniz. değişkenleri hello şu anda hello özel durum sırasında oluşturuldu ve Hello anlık görüntü kaynak kodu hello durumunu gösterir. Başlangıç anlık görüntü hata ayıklayıcısı (Önizleme) içinde [Azure Application Insights](app-insights-overview.md) özel durum, web uygulamanızın telemetrisinden izler. Böylece toodiagnose sorunları üretimde gereksinim hello bilgileri sahip anlık görüntüleri, üst atma özel durumlar toplar. Merhaba dahil [anlık görüntü Toplayıcı NuGet paketi](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) uygulamanızda ve isteğe bağlı olarak koleksiyon parametrelerinde yapılandırma [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md). Anlık görüntüler görünmez [özel durumları](app-insights-asp-net-exceptions.md) hello Application Insights portalında.

Hata ayıklama anlık görüntüleri hello portal toosee hello çağrı yığınında görüntüleyebilir ve her çağrı yığını çerçevesi en değişkenlerle inceleyin. Kaynak kodu, Visual Studio 2017 kuruluş tarafından sahip açık anlık görüntüleri ile daha güçlü bir hata ayıklama deneyimini tooget [Visual Studio için başlangıç anlık görüntü hata ayıklayıcısı uzantısı yükleme](https://aka.ms/snapshotdebugger).

Anlık görüntü koleksiyonu için kullanılabilir:
* .NET framework ve ASP.NET uygulamaları .NET Framework 4.5 veya sonraki sürümlerini çalıştırıyor.
* Windows üzerinde çalışan .NET core 2.0 ve ASP.NET Core 2.0 uygulamaları.

### <a name="configure-snapshot-collection-for-aspnet-applications"></a>ASP.NET uygulamaları için anlık görüntü koleksiyonunu yapılandırma

1. [Application Insights web uygulamanızda etkinleştirmek](app-insights-asp-net.md), henüz yapmadınız.

2. Merhaba dahil [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) uygulamanıza NuGet paketi. 

3. Paket çok eklenen hello hello varsayılan seçenekleri gözden geçir[Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md):

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- hello default is true, but you can disable Snapshot Debugging by setting it toofalse -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this tootrue. -->
        <!-- DeveloperMode is a property on hello active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need toosee an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- hello maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- hello maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often tooreset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- hello maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- hello maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. Anlık görüntüler, bildirilen tooApplication Öngörüler yalnızca özel durumları toplanır. Bazı durumlarda (örneğin, daha eski sürümleri hello .NET platformu), çok gerekebilir[özel durum koleksiyonunu yapılandırma](app-insights-asp-net-exceptions.md#exceptions) toosee istisnalar hello portalında anlık görüntüler.


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a>ASP.NET Core 2.0 uygulamaları için anlık görüntü koleksiyonunu yapılandırma

1. [Application Insights ASP.NET Core web uygulamanızda etkinleştirmek](app-insights-asp-net-core.md), henüz yapmadınız.

2. Merhaba dahil [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) uygulamanıza NuGet paketi.

3. Merhaba değiştirme `ConfigureServices` uygulamanızın yönteminde `Startup` tooadd hello anlık görüntü toplayıcının telemetri işlemci sınıfı. Merhaba kodu eklemeniz gerekir hello başvurulan hello Microsoft.ApplicationInsights.ASPNETCore NuGet paketi sürümüne bağlıdır.

   Microsoft.ApplicationInsights.AspNetCore 2.1.0 ekleyin:
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   Microsoft.ApplicationInsights.AspNetCore 2.1.1 ekleyin:
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       private class SnapshotCollectorTelemetryProcessorFactory : ITelemetryProcessorFactory
       {
           public ITelemetryProcessor Create(ITelemetryProcessor next) =>
               new SnapshotCollectorTelemetryProcessor(next);
       }

       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a>Diğer .NET uygulamaları için anlık görüntü koleksiyonunu yapılandırma

1. Uygulamanızı Application Insights ile zaten izlenmemektedir, başlayın [Application Insights ve ayar hello izleme anahtarını etkinleştirme](app-insights-windows-desktop.md).

2. Merhaba eklemek [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) uygulamanıza NuGet paketi.

3. Anlık görüntüler, bildirilen tooApplication Öngörüler yalnızca özel durumları toplanır. Kod tooreport toomodify gerekebilir bunları. Uygulamanızı hello yapısını hello özel durum kodu işleme bağlıdır, ancak bir örnek aşağıda verilmiştir:
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle hello request.
        }
        catch (Exception ex)
        {
            // Report hello exception tooApplication Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow hello exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a>İzinleri

Hello Azure abonelik sahipleri anlık görüntüleri inceleyebilirsiniz. Diğer kullanıcıların bir sahibi tarafından izin verilmesi gerekir.

toogrant izni, Ata hello `Application Insights Snapshot Debugger` anlık görüntüleri araştırmasını rol toousers. Bu rol, tooindividual kullanıcıları veya grupları hello hedef Application Insights kaynağı için abonelik sahipleri tarafından veya kaynak grubu ya da abonelik atanabilir.

1. Merhaba erişim denetimi (IAM) dikey penceresini açın.
1. Merhaba + Ekle düğmesini tıklatın.
1. Uygulama Öngörüler anlık görüntü hata ayıklayıcı hello rolleri aşağı açılan listeden seçin.
1. Arayın ve hello kullanıcı tooadd için bir ad girin.
1. Merhaba Kaydet düğmesine tooadd hello kullanıcı toohello rolüne tıklayın.


[!IMPORTANT]
    Anlık görüntüler olası değişken ve parametre değerlerini kişisel ve diğer hassas bilgiler içerebilir.

## <a name="debug-snapshots-in-hello-application-insights-portal"></a>Anlık görüntüler hello Application Insights portalında hata ayıklama

Belirli bir özel durum ya da bir sorun kimliği için bir anlık görüntü kullanılabiliyorsa, bir **açık hata ayıklama anlık görüntü** düğmesinin üzerinde hello [özel durum](app-insights-asp-net-exceptions.md) hello Application Insights portalında.

![Özel durum açık hata ayıklama anlık görüntü düğmesine](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

Hello hata ayıklama anlık Görünüm'de, çağrı yığını ve değişkenleri bölmesine bakın. Seçtiğinizde hello çağrı yığını Bölmesi'nde hello çağrının çerçeveler yığın, yerel değişkenleri görüntüleyebilir ve bu işlev parametrelerini hello değişkenleri bölmesinde çağırın.

![Görünüm hata ayıklama anlık hello portalı](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

Varsayılan olarak görüntülenebilir olmadıkları ve anlık görüntüleri hassas bilgiler içerebilir. tooview anlık görüntüler, hello olmalıdır `Application Insights Snapshot Debugger` atanan rolü tooyou.

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a>Visual Studio 2017 Enterprise sahip anlık görüntüleri hata ayıklama
1. Merhaba tıklatın **karşıdan anlık görüntü** düğmesini toodownload bir `.diagsession` Visual Studio 2017 kuruluş tarafından açılabilir dosya. 

2. tooopen hello `.diagsession` dosya, şunları yapmalısınız ilk [hello anlık görüntü hata ayıklayıcısı uzantısı için Visual Studio yükleyip](https://aka.ms/snapshotdebugger).

3. Başlangıç anlık görüntü dosyasını açın sonra Visual Studio'da hello mini döküm hata ayıklama sayfası görünür. Tıklatın **yönetilen kod hata ayıklama** hello anlık görüntü hata ayıklama toostart. Başlangıç anlık görüntü toohello kod satırı, böylece hello işleminin geçerli durumunu hello ayıklayabilirsiniz burada hello özel durum oluştu açar.

    ![Visual Studio'da hata ayıklama anlık görünümü](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

Merhaba indirilen anlık görüntü web uygulaması sunucunuzda bulundu herhangi sembol dosyalarını içerir. Kaynak kodu ile gerekli tooassociate anlık görüntü verilerini bu simge dosyalarıdır. Web uygulamalarınızı yayımladığınızda, uygulama hizmeti uygulamalarınız için emin tooenable simgesi dağıtımı yapın.

## <a name="how-snapshots-work"></a>Anlık görüntüler nasıl çalışır

Uygulamanız başladığında, ayrı anlık görüntü yükleyici işlemi, uygulamanız için anlık görüntü istekleri izleyen oluşturulur. Bir anlık görüntü istendiğinde işlem çalışan hello bir gölge kopyasını yaklaşık 10 too20 dakika içinde yapılır. Merhaba gölge işleminin ardından analiz ve bir anlık görüntü toorun hello ana işlem devam ederken oluşturulur ve trafik toousers hizmet. tüm ilgili simge (.pdb) dosyalar ile birlikte yüklenen tooApplication Öngörüler tooview gerekirse hello anlık görüntüsüdür hello anlık görüntü.

## <a name="current-limitations"></a>Geçerli sınırlamalar

### <a name="publish-symbols"></a>Simgeler yayımlama
Başlangıç anlık görüntü hata ayıklayıcı simge dosyaları hello üretim sunucusu toodecode değişkenleri ve tooprovide Visual Studio'da hata ayıklama deneyimini gerektirir. tooApp hizmet yayımladığında hello 15.2 sürümü Visual Studio 2017, sürüm derlemeleri simgelerini varsayılan olarak yayımlar. Önceki sürümlerde, tooadd hello aşağıdakiler satır tooyour yayımlama profili `.pubxml` simgeleri yayın modunda yayımlanan dosyasını:

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

Azure işlem ve diğer türleri için hello simge dosyaları hello olduğundan emin olun hello ana uygulama .dll aynı klasörü (genellikle `wwwroot/bin`) veya hello geçerli yolda kullanılabilir.

### <a name="optimized-builds"></a>En iyi duruma getirilmiş derlemeleri
Bazı durumlarda, yerel değişkenleri hello oluşturma işlemi sırasında uygulanan en iyi duruma getirme nedeniyle yayın derlemelerde görüntülenemiyor.

## <a name="troubleshooting"></a>Sorun giderme

Bu ipuçları hello anlık görüntü hata ayıklayıcı sorunlarını gidermenize yardımcı olur.

### <a name="verify-hello-instrumentation-key"></a>Merhaba izleme anahtarını doğrulayın

Yayımlanan uygulamanızda hello doğru izleme anahtarını kullandığınızdan emin olun. Genellikle, Application Insights hello izleme anahtarını hello Applicationınsights.config dosyasını okur. Hello değeri olan Merhaba, aynı hello Portalı'nda bkz hello Application Insights kaynağı için hello araçları anahtar olarak doğrulayın.

### <a name="check-hello-uploader-logs"></a>Merhaba yükleyici günlüklerini kontrol edin

Bir anlık görüntü oluşturulduktan sonra bir mini döküm dosyası (.dmp) disk üzerinde oluşturulur. Ayrı yükleyici işlem, mini döküm dosyası alır ve bunu, tooApplication Öngörüler anlık görüntü hata ayıklayıcı depolama gibi ilişkili tüm pdb birlikte yükler. Merhaba mini döküm başarıyla yükledi sonra diskten silinir. Merhaba mini döküm yükleyici için Hello günlük dosyaları diskte korunur. Bir uygulama hizmeti ortamı'nda, bu günlükler bulabilirsiniz `D:\Home\LogFiles\Uploader_*.log`. Kullanım hello Kudu yönetim sitesi için uygulama hizmeti toofind bu günlük dosyaları.

1. Uygulama hizmeti uygulamanızı hello Azure portalını açın.

2. Select hello **Gelişmiş Araçlar** dikey veya arama **Kudu**.
3. tıklatın **Git**.
4. Merhaba, **hata ayıklama konsoluna** aşağı açılan liste kutusunda **CMD**.
5. Tıklatın **LogFiles**.

İle başlayan bir ada sahip en az bir dosya görmelisiniz `Uploader_` ve `.log` uzantısı. Tüm günlük dosyalarını Hello uygun simgeye toodownload tıklatın veya bir tarayıcıda açın.
Merhaba dosya adı hello makine adını içerir. Uygulama hizmeti örneğinizi birden fazla makine üzerinde barındırılıyorsa, her makine için farklı günlük dosyaları vardır. Merhaba yükleyici yeni bir mini döküm dosyası algıladığında hello günlük dosyasına kaydedilir. Başarılı bir karşıya yükleme bir örneği burada verilmiştir:

```
MinidumpUploader.exe Information: 0 : Dump available 139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:08.0349846Z
MinidumpUploader.exe Information: 0 : Uploading D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp, 329.12 MB
    DateTime=2017-05-25T14:25:16.0145444Z
MinidumpUploader.exe Information: 0 : Upload successful.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Extracting PDB info from D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Matched 2 PDB(s) with local files.
    DateTime=2017-05-25T14:25:44.2310982Z
MinidumpUploader.exe Information: 0 : Stamp does not want any of our matched PDBs.
    DateTime=2017-05-25T14:25:44.5435948Z
MinidumpUploader.exe Information: 0 : Deleted D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:44.6095821Z
```

Merhaba izleme anahtarını Hello önceki örnekte olduğu `c12a605e73c44346a984e00000000000`. Bu değer, uygulamanız için hello izleme anahtarını eşleşmelidir.
Merhaba mini döküm hello Kimliğine sahip bir anlık görüntüsü ile ilişkili `139e411a23934dc0b9ea08a626db16c5`. Bu kimliği kullanabilirsiniz sonraki toolocate hello ilişkili uygulama Öngörüler analytics'te özel durum telemetrisi.

Merhaba Yükleyici her 15 dakikada hakkında yeni pdb tarar. Örnek aşağıda verilmiştir:

```
MinidumpUploader.exe Information: 0 : PDB rescan requested.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\home\site\wwwroot\ for local PDBs.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\local\Temporary ASP.NET Files\root\a6554c94\e3ad6f22\assembly\dl3\81d5008b\00b93cc8_dec5d201 for local PDBs.
    DateTime=2017-05-25T15:11:38.8160276Z
MinidumpUploader.exe Information: 0 : Local PDB scan complete. Found 2 PDB(s).
    DateTime=2017-05-25T15:11:38.8316450Z
MinidumpUploader.exe Information: 0 : Deleted PDB scan marker D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\.pdbscan.
    DateTime=2017-05-25T15:11:38.8316450Z
```

Uygulamalar için _değil_ App Service içinde barındırılan, hello yükleyici hello günlüklerin hello Mini dökümler aynı klasöre: `%TEMP%\Dumps\<ikey>` (burada `<ikey>` araçları anahtarınız).

### <a name="use-application-insights-search-toofind-exceptions-with-snapshots"></a>Anlık görüntü toofind istisnalar kullanım Application Insights arama

Bir anlık görüntü oluşturulduğunda, özel durum atma hello bir anlık görüntü kimliği ile etiketlenir Merhaba özel durum telemetrisi bildirilen tooApplication Öngörüler olduğunda, bu anlık görüntü kimliği bir özel özellik olarak dahil edilir. Merhaba Ara dikey Application Insights'ta kullanarak, tüm telemetri hello ile bulabilirsiniz `ai.snapshot.id` özel özellik.

1. Tooyour Application Insights kaynağını hello Azure portalına göz atın.
2. Tıklatın **arama**.
3. Tür `ai.snapshot.id` arama metin kutusuna hello ve Enter tuşuna basın.

![Bir anlık görüntü kimliği hello portalındaki telemetriyle arayın](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

Bu arama sonuç döndürürse, hiç anlık görüntü uygulamanıza hello seçili zaman aralığı için raporlanan tooApplication Insights yoktu.

Merhaba yükleyici günlükleri, belirli bir anlık görüntüye Kimliğinden toosearch bu kimliği hello arama kutusuna yazın. Karşıya yüklenen bildiğiniz bir anlık görüntü için telemetri bulamazsanız, aşağıdaki adımları izleyin:

1. Merhaba sağ Application Insights kaynağı hello izleme anahtarını doğrulayarak arıyorsanız denetleyin.

2. Merhaba zaman damgası hello yükleyici günlüğündeki kullanarak, bu zaman aralığı hello arama toocover hello zaman aralığı filtresi ayarlayın.

Bu anlık görüntü Kimliğine sahip bir özel durum hala göremiyorsanız hello özel durum telemetrisi bildirilen tooApplication Öngörüler değildi. Bu durum, hello anlık görüntü sürdü sonra uygulamanızın kilitlendi, ancak hello özel durum telemetrisi bildirilen önce gerçekleşebilir. Bu durumda, uygulama hizmeti günlüklerini altında hello denetleyin `Diagnose and solve problems` olsaydı beklenmeyen toosee yeniden başlatır veya işlenmeyen özel durum.

## <a name="next-steps"></a>Sonraki adımlar

* [Kodunuzda snappoints ayarlamak](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) için bir özel durum bekleniyor olmadan tooget anlık görüntüler.
* [Özel durumlar, web uygulamalarında tanılama](app-insights-asp-net-exceptions.md) açıklar nasıl toomake daha fazla özel durumları görünür tooApplication Öngörüler. 
* [Akıllı algılama](app-insights-proactive-diagnostics.md) performans anormalliklerini otomatik olarak bulur.
