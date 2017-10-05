---
title: "Azure Application Insights ile canlı web uygulamalarında profil oluşturma | Microsoft Docs"
description: "Web sunucu kodunuzdaki etkin yolunuzda ayak izini düşük Profil Oluşturucu ile tanımlayın."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: ff39f9a84b86c14859aaee50ee368643fb2848ea
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="profiling-live-azure-web-apps-with-application-insights"></a>Application Insights ile canlı Azure web uygulamaları profil oluşturma

*Bu, Application Insights GA uygulama hizmetleri için ve işlem için Önizleme özelliğidir.*

Ne kadar süre her yöntem, canlı web uygulamanızda profil oluşturma aracını kullanarak harcanan Bul [Azure Application Insights](app-insights-overview.md). Uygulamanız tarafından sunulduğunu Canlı istekleri ayrıntılı profillerini gösterir ve 'en uzun süre kullanarak dinamik yolu' vurgular. Ayrıca farklı yanıt sürelerini sahip örnekler otomatik olarak seçer. Profil Oluşturucu yükünü en aza indirmek için çeşitli teknikleri kullanır.

Profil Oluşturucu şu anda Azure App Services üzerinde en az fiyatlandırma katmanı Basic çalışan ASP.NET web uygulamaları için çalışır. 

<a id="installation"></a>
## <a name="enable-the-profiler"></a>Profil Oluşturucu etkinleştir

[Application Insights yükleme](app-insights-asp-net.md) kodunuzda. Zaten yüklüyse, en son sürüme sahip olduğundan emin olun. (Bunu yapmak için Çözüm Gezgini'nde projenize sağ tıklayın ve Manage NuGet paketleri seçin. Güncelleştirmeleri seçin ve tüm paketler güncelleştirebilirsiniz.) Uygulamanızı yeniden dağıtın.

*ASP.NET Core kullanarak? [Burayı](#aspnetcore).*

İçinde [https://portal.azure.com](https://portal.azure.com), web uygulamanız için Application Insights kaynağı açın. Açık **performans** tıklatıp **uygulama Öngörüler profil oluşturucu etkinleştir...** .

![Etkinleştirme profil oluşturucu başlığında tıklatın][enable-profiler-banner]

Alternatif olarak, her zaman tıklayabilirsiniz **yapılandırma** durumunu görüntülemek için etkinleştirmek veya profil oluşturucu devre dışı bırakın.

![Performans dikey penceresinde Yapılandır'ı tıklatın.][performance-blade]

Application Insights ile yapılandırılmış olan web apps Yapılandır dikey penceresinde listelenir. Gerekirse profil oluşturucu aracıyı yüklemek için yönergeleri izleyin. Hiçbir web uygulaması Application Insights ile henüz yapılandırılmışsa tıklatın *bağlantılı uygulama Ekle*.

Kullanım *etkinleştirmek profil oluşturucu* veya *devre dışı profil oluşturucu* düğmeleri Yapılandır dikey penceresinde tüm bağlantılı web uygulamalarını profil oluşturucu denetlemek için.



![Dikey yapılandırın][linked app services]

Tek bir uygulama hizmeti örneği için profil oluşturucu yeniden başlatmak veya durdurmak için onu bulabilirsiniz **uygulama hizmeti kaynak**, **Web işleri**. Altında silmek için Ara **uzantıları**.

![Web işleri için profil oluşturucu devre dışı bırak][disable-profiler-webjob]

Tüm web uygulamaları üzerinde performans sorunları olabildiğince çabuk bulmak için etkinleştirilmiş profil oluşturucu sahip olmasını öneririz.

Değişiklikleri web uygulamanızı dağıtmak için WebDeploy kullanıyorsanız, hariç olun **App_Data** dağıtımı sırasında silinen gelen klasörü. Aksi halde, sonraki Azure web uygulamasını dağıttığınızda profil oluşturucu uzantının dosyalar silinir.

### <a name="using-profiler-with-azure-vms-and-compute-resources-preview"></a>Profil Oluşturucu Azure Vm'leri ve işlem kaynakları (Önizleme) ile kullanma

Olduğunda, [Application Insights Azure uygulama hizmetleri için çalışma zamanında etkinleştir](app-insights-azure-web-apps.md#run-time-instrumentation-with-application-insights), profil oluşturucu otomatik olarak kullanılabilir. (Kaynak için Application Insights zaten etkinleştirilirse, lates sürümüne güncelleştirmeniz gerekebilir **yapılandırma** Sihirbazı.)

Var olan bir [Azure işlem kaynakları için profil oluşturucu önizleme sürümünü](https://go.microsoft.com/fwlink/?linkid=848155).


## <a name="limits"></a>Sınırlar

Varsayılan veri saklama 5 gündür. En fazla 10 GB günde alınan.

Profil Oluşturucu hizmeti için ücret ödemeden yoktur. Web uygulamanızı olmalıdır en az uygulama hizmetleri, temel katmana barındırılan.

## <a name="viewing-profiler-data"></a>Profil Oluşturucu verileri görüntüleme

İşlem listesinde kaydırın ve performans dikey penceresini açın.




![Uygulama Öngörüler performans dikey örnekler sütun][performance-blade-examples]

Tablodaki sütunlar şunlardır:

* **Count** -dikey zaman aralığını bu isteklerin sayısı.
* **ORTANCA** - uygulamanızı bir isteğine yanıt vermek için tipik süresini. Tüm yanıtları yarısı bu değerden daha hızlı.
* **95** yanıtların % 95 bu değerden daha hızlı. Bu şekil ORTANCA çok farklı ise, uygulamanızı aralıklı bir sorun olabilir. (Veya önbelleğe alma gibi bir tasarım özelliği tarafından açıklanan.)
* **Örnekler** -profil oluşturucu bu işlem için Yığın izlemeleri yakalandı simge gösterir.

İzleme Gezgini'ni açmak için örnekler simgesine tıklayın. Profil Oluşturucu yakalanan olduğunu birkaç örnek Gezgini gösterir yanıt süresine göre sınıflandırılmış.

Zamanın isteğini işleyen kodu düzeyi dökümünü göstermek için bir örnek seçin.

![Uygulama Öngörüler izleme Gezgini][trace-explorer]

**Sık kullanılan yolu Göster** açılır biggest, düğüm yaprak ya da en az bir şey kapatın. Çoğu durumda bu düğüm için bir performans düşüklüğü bitişik olacaktır.



* **Etiket**: işlevi veya olay adı. Ağaç kodu ve (SQL ve http olayları gibi) oluşan olaylarla bir karışımını gösterir. Üst olay genel istek süresini temsil eder.
* **Geçen**: İşlem başlangıcı ve sonu arasındaki zaman aralığı.
* **Zaman**: işlevi/olay için diğer işlevleri ilişkisinde zaman çalışıyordu gösterir.

## <a name="how-to-read-performance-data"></a>Performans verileri okumak nasıl

Microsoft Hizmet Profil Oluşturucu örnekleme yöntemini ve araçları birleşimi, uygulamanızın performansını çözümlemek için kullanır.
Ayrıntılı toplama devam ederken, hizmet profil oluşturucu her birinin her milisaniyelik makinenin CPU yönerge işaretçisi örnekleri.
Her örnek şu anda yürütülen, iş parçacığı hem yüksek ve düşük Soyutlama düzeyleri yapmakta olduğu, hangi hakkında ayrıntılı ve faydalı bilgileri vermiş iş parçacığının tam çağrı yığını yakalar. Hizmet Profil Oluşturucu aynı zamanda diğer içerik geçiş olayları gibi olaylar, TPL olayları ve etkinlik bağıntısı ve causality izlemek için iş parçacığı havuzu olayları toplar.

Zaman çizelgesi görünümünde gösterilen çağrı yığını yukarıdaki örnekleme ve araçları sonucudur. Her örnek iş parçacığının tam çağrı yığını yakalar çünkü başvuru diğer çerçeveler yanı sıra, .NET framework kodunu içerir.

### <a id="jitnewobj"></a>Nesne ayırma (`clr!JIT\_New or clr!JIT\_Newarr1`)
`clr!JIT\_New and clr!JIT\_Newarr1`Yönetilen yığınından bellek ayırır .NET framework içinde yardımcı işlevlerdir. `clr!JIT\_New`Nesne ayrılmış olduğunda çağrılır. `clr!JIT\_Newarr1`bir nesne dizisinin atandığında çağrılır. Bu iki işlevler tipik olarak çok hızlı ve görece küçük süreyi sürer. Görürseniz `clr!JIT\_New` veya `clr!JIT\_Newarr1` önemli miktarda zaman çizelgeniz içinde olması, bu kod birçok nesne ayırma ve önemli miktarda bellek tükettikten göstergesidir.

### <a id="theprestub"></a>Kod yükleme (`clr!ThePreStub`)
`clr!ThePreStub`ilk kez yürütmek için kodu hazırlar .NET framework içinde yardımcı işlevdir. Bu genellikle, ancak bunlarla sınırlı olmamak, (yalnızca süre) JIT derleme içerir. Her C# yönteminde `clr!ThePreStub` bir işlem ömrü boyunca en fazla bir kez çağrılmalıdır.

Görürseniz `clr!ThePreStub` önemli ölçüde geçen bir istek için zaman bu yöntem yürütür birincisini isteğidir ve bu yöntem yüklemek .NET framework çalışma zamanının önemli zamanı belirtir. Kullanıcılarınız erişmek veya NGen derlemeleriniz üzerinde çalıştırmayı düşünün önce kodu bölümünü yürütür bir Isınma işlemi göz önünde bulundurabilirsiniz.

### <a id="lockcontention"></a>Kilit çakışması (`clr!JITutil\_MonContention` veya `clr!JITutil\_MonEnterWorker`)
`clr!JITutil\_MonContention`veya `clr!JITutil\_MonEnterWorker` geçerli iş parçacığı bir kilidi serbest bırakılacak bekleyen gösterir. Bu genellikle Monitor.Enter yönteminin çağrılması veya MethodImplOptions.Synchronized özniteliğine sahip bir yöntemi çağrılırken bir C# lock deyimi, yürütülürken görüntülenir. Kilit çakışması genellikle bir kilit iş parçacığı A alır ve iş parçacığı B iş parçacığı A bırakması önce aynı kilidi dener olur.

### <a id="ngencold"></a>Kod yükleme (`[COLD]`)
Yöntem adı içeriyorsa, `[COLD]`, gibi `mscorlib.ni![COLD]System.Reflection.CustomAttribute.IsDefined`, .NET framework çalışma zamanı tarafından optimize edilmemiş kod yürütülmekte olduğu anlamına gelir <a href="https://msdn.microsoft.com/library/e7k32f4k.aspx">profil temelli iyileştirme</a> ilk kez. Her yöntem için bu işlemin süresi boyunca en fazla bir kez gösterilmesi gerekir.

Kod yüklenirken önemli miktarda zaman için bir istek alırsa, bu istek yöntemi iyileştirilmemiş kısmı yürütmek için ilk hangisi olduğunu gösterir. Yarı kullanıcılarınızın erişebilmesi kodu bölümünü yürütür işlemini göz önünde bulundurabilirsiniz.

### <a id="httpclientsend"></a>HTTP isteği gönder
Gibi yöntemler `HttpClient.Send` kodu tamamlamak bir HTTP isteği için bekleyen gösterir.

### <a id="sqlcommand"></a>Veritabanı işlemi
Kod tamamlamak bir veritabanı işlemi bekliyor SqlCommand.Execute gibi yöntemi gösterir.

### <a id="await"></a>Bekleyen (`AWAIT\_TIME`)
`AWAIT\_TIME`kod tamamlamak başka bir görev için beklediğini gösterir. Bu, genellikle C# ile await' deyimi' gerçekleşir. Kod yaptığında C# 'await', iş parçacığı unwinds ve denetim için iş parçacığı havuzu döndürür ve 'await için' tamamlanmasını bekleyen engellenmiş iş parçacığı yok. Ancak, mantıksal olarak bekleme yaptığınız iş parçacığı 'işleminin tamamlanması bekleniyor engellendi'. `AWAIT\_TIME` Görevinin tamamlanmasını bekleyen engellenmiş süresini gösterir.

### <a id="block"></a>Engellenen zaman
`BLOCKED_TIME`kullanılabilir veya tamamlamak bir istek için bekleyen bir iş parçacığı için bekleyen bir eşitleme nesnesi bekleniyor gibi kullanılabilir olması başka bir kaynak için bekliyor. kodu gösterir.

### <a id="cpu"></a>CPU süresi
CPU yönergeleri çalıştırmakla meşgul.

### <a id="disk"></a>Disk Zamanı
Uygulama disk işlemleri gerçekleştiriyor.

### <a id="network"></a>Ağ süresi
Uygulama ağ işlemlerini gerçekleştirme.

### <a id="when"></a>Zaman sütun
Bu düğüm için toplanan dahil örnekleri zaman içinde nasıl farklılık, bir görsel öğe olur. İstek toplam aralığı 32 zaman demet ayrılmıştır ve o düğümü dahil örnekleri bu 32 demet toplanır. Her demet sonra yükseklik ölçeklendirilmiş bir değeri temsil çubuğu olarak temsil edilir. İşaretlenen düğümleri için `CPU_TIME` veya `BLOCKED_TIME`, veya bir kaynağa (cpu, disk, iş parçacığı) kullanan, belirgin bir ilişki olduğu çubuk temsil eder Bu kaynaklardan biri bu demet süresi boyunca kullanma. Bu ölçümleri, birden fazla kaynak tüketen tarafından % 100'den büyük alabilirsiniz. Ortalama bir aralığı içinde iki CPU kullanırsanız, örneğin, daha sonra % 200 alırsınız.


## <a id="troubleshooting"></a>Sorun giderme

### <a name="how-can-i-know-whether-application-insights-profiler-is-running"></a>Application Insights profil oluşturucu çalışır durumda olup olmadığını nasıl öğrenebilirim?

Profil Oluşturucu Web uygulamasında bir sürekli web işi olarak çalıştırır. Web uygulaması kaynağı içinde https://portal.azure.com açın ve Web işleri dikey penceresinde "ApplicationInsightsProfiler" durumunu denetleyin. Çalışıyor durumda değilse, açmak **günlükleri** daha fazla bilgi bulmak için.

### <a name="why-cant-i-find-any-stack-examples-even-though-the-profiler-is-running"></a>Profil Oluşturucu çalışıyor olsa bile neden herhangi yığını örnekler bulamadınız mı?

İşte birkaç şey kontrol edebilirsiniz.

1. Web uygulama hizmet planınız, temel katmana olduğundan emin olun ve üstü.
2. Web uygulamanızın uygulama Öngörüler SDK 2.2 Beta sahiptir ve yukarıda etkin emin olun.
3. Web uygulamanıza Application Insights SDK'sı tarafından kullanılan aynı izleme anahtarı appınsıghts_ınstrumentatıonkey ayarıyla olduğundan emin olun.
4. Web uygulamanızı .net üzerinde çalıştığından emin olun Framework 4.6.
5. Lütfen bir ASP.NET Core uygulama ise, ayrıca denetleyin [gerekli bağımlılıkları](#aspnetcore).

Profil Oluşturucu başlatıldıktan sonra ne zaman profil oluşturucu birkaç performans izlemeleri etkin olarak toplayan kısa Isınma Süresi yoktur. Bundan sonra Profil Oluşturucu performans izlemeleri iki dakika içinde her saat için toplar.  

### <a name="i-was-using-azure-service-profiler-what-happened-to-it"></a>Azure Hizmet Profil Oluşturucu tarafından kullanılan. Ona ne?  

Uygulama Öngörüler profil oluşturucu etkinleştirdiğinizde, Azure hizmet profil oluşturucu Aracısı devre dışı bırakılır.

### <a id="double-counting"></a>Çift paralel iş parçacığı sayımı

Bazı durumlarda yığın görüntüleyicide toplam süre ölçümü gerçek süresi, istek büyük.

Paralel olarak çalışan bir istekle ilişkili iki veya daha fazla iş parçacığı olduğunda bu durum oluşabilir. Toplam iş parçacığı saat sonra geçen süreyi büyük. Çoğu durumda bir iş parçacığından diğerine tamamlamak için bekliyor olabilir. Görüntüleyici bu algılar ve sizi ilgilendirmeyen bekleme atlamak çalışır, ancak ne kritik bilgiler olabilir atlama yerine çok fazla gösteren yan tarafında errs.  

Paralel iş parçacıkları, izlemeleri gördüğünüzde, böylece istek kritik yolunu belirleyebilir hangi iş parçacığı bekleyen belirlemeniz gerekir. Çoğu durumda, hızlı bir şekilde bir bekleme durumuna geçtiğinde iş parçacığı üzerinde başka bir iş parçacığı basitçe bekliyor. Diğerlerinde yoğunlaşabilirsiniz ve bekleyen iş parçacıklarının zamanında yok sayın.

### <a id="issue-loading-trace-in-viewer"></a>Profil oluşturma veri yok

1. Görüntülemeye çalıştığınız veri birkaç haftalık eski ise, zaman filtresi görüntülemeyi deneyin ve yeniden deneyin.

2. Proxy'leri veya bir güvenlik duvarı https://gateway.azureserviceprofiler.net erişim engellemediğinizden denetleyin.

3. Uygulamanızı kullanarak Application Insights izleme anahtarı ile profil etkinleştirdikten Application Insights kaynağı ile aynı olup olmadığını denetleyin. Anahtar genellikle Applicationınsights.Config'de ancak web.config veya app.config de bulunabilir.

### <a name="error-report-in-the-profiling-viewer"></a>Profil oluşturma Görüntüleyicisi'nde hata raporu

Bir destek bileti portalından dosya. Hata iletisi öğesinden bağıntı Kimliğini içerir.

## <a name="manual-installation"></a>El ile yükleme

Profil Oluşturucu yapılandırdığınızda, Web uygulamanızın ayarlar aşağıdaki güncelleştirmeler yapılmıştır. El ile ortamınız, örneğin, uygulamanızı Azure uygulama hizmeti ortamı (ana) çalıştırılıp çalıştırılmadığını gerektiriyorsa, bunları kendiniz yapabilirsiniz:

1. Web uygulaması denetim dikey penceresinde ayarları'nı açın.
2. Ayarlama ".Net Framework sürümünü" v4.6 için.
3. "Her zaman açık" açık olarak ayarlayın.
4. Uygulama ayarı ekleme "__appınsıghts_ınstrumentatıonkey__" ve SDK'sı tarafından kullanılan aynı izleme anahtarı için değer ayarlayın.
5. Gelişmiş Araçlar'ı açın.
6. "Kudu Web sitesini açın Git"'i tıklatın.
7. Kudu Web sitesi, "Site uzantılarını" seçin.
8. Yükleme "__Application Insights__" galerisinden.
9. Web uygulaması yeniden başlatın.

## <a id="aspnetcore"></a>ASP.NET çekirdeği desteği

ASP.NET Core uygulama gereken Microsoft.ApplicationInsights.AspNetCore Nuget Paketi 2.1.0-beta6 yüklemeye veya profil oluşturucu ile çalışmak için daha yüksek. Artık daha düşük sürümler 27/6/2017 sonra destekliyoruz.

## <a name="next-steps"></a>Sonraki adımlar

* [Visual Studio'da Application Insights ile çalışma](https://docs.microsoft.com/azure/application-insights/app-insights-visual-studio)

[performance-blade]: ./media/app-insights-profiler/performance-blade.png
[performance-blade-examples]: ./media/app-insights-profiler/performance-blade-examples.png
[trace-explorer]: ./media/app-insights-profiler/trace-explorer.png
[trace-explorer-toolbar]: ./media/app-insights-profiler/trace-explorer-toolbar.png
[trace-explorer-hint-tip]: ./media/app-insights-profiler/trace-explorer-hint-tip.png
[trace-explorer-hot-path]: ./media/app-insights-profiler/trace-explorer-hot-path.png
[enable-profiler-banner]: ./media/app-insights-profiler/enable-profiler-banner.png
[disable-profiler-webjob]: ./media/app-insights-profiler/disable-profiler-webjob.png
[linked app services]: ./media/app-insights-profiler/linked-app-services.png
