---
title: "Azure Application Insights ile aaaProfiling dinamik web uygulamaları | Microsoft Docs"
description: "Web sunucu kodunuzdaki Hello etkin yolunuzda ayak izini düşük Profil Oluşturucu ile tanımlayın."
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
ms.openlocfilehash: 3c7f21076f19335e0f006327932e13623ec9526b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="profiling-live-azure-web-apps-with-application-insights"></a>Application Insights ile canlı Azure web uygulamaları profil oluşturma

*Bu, Application Insights GA uygulama hizmetleri için ve işlem için Önizleme özelliğidir.*

Ne kadar süre her yöntem, canlı web uygulamanızda aracının profil hello kullanarak harcanan Bul [Azure Application Insights](app-insights-overview.md). Uygulamanız tarafından sunulduğunu Canlı istekleri ayrıntılı profillerini gösterir ve 'hello çoğu zaman kullanarak etkin yolunuzda' hello vurgular. Ayrıca farklı yanıt sürelerini sahip örnekler otomatik olarak seçer. Hello profil oluşturucu çeşitli teknikleri toominimize yükünü kullanır.

Hello profil oluşturucu şu anda works ASP.NET için Azure App Services üzerinde çalışan uygulamalar web içinde en az hello Basic fiyatlandırma katmanı. 

<a id="installation"></a>
## <a name="enable-hello-profiler"></a>Hello profil oluşturucu etkinleştir

[Application Insights yükleme](app-insights-asp-net.md) kodunuzda. Zaten yüklüyse, hello en son sürüme sahip olduğundan emin olun. (toodo Bu, Çözüm Gezgini'nde projenize sağ tıklayın ve Manage NuGet paketleri seçin. Güncelleştirmeleri seçin ve tüm paketler güncelleştirebilirsiniz.) Uygulamanızı yeniden dağıtın.

*ASP.NET Core kullanarak? [Burayı](#aspnetcore).*

İçinde [https://portal.azure.com](https://portal.azure.com), hello Application Insights kaynağı web uygulamanız için açın. Açık **performans** tıklatıp **uygulama Öngörüler profil oluşturucu etkinleştir...** .

![Merhaba etkinleştir profil oluşturucu başlığında tıklatın][enable-profiler-banner]

Alternatif olarak, her zaman tıklayabilirsiniz **yapılandırma** tooview durumu, etkinleştirme veya devre dışı hello profil oluşturucu devre dışı.

![Merhaba performans dikey penceresinde Yapılandır'ı tıklatın.][performance-blade]

Application Insights ile yapılandırılmış olan web apps Yapılandır dikey penceresinde listelenir. Gerekirse yönergeleri tooinstall hello Profil Oluşturucu aracı izleyin. Hiçbir web uygulaması Application Insights ile henüz yapılandırılmışsa tıklatın *bağlantılı uygulama Ekle*.

Kullanım hello *etkinleştirmek profil oluşturucu* veya *devre dışı profil oluşturucu* hello Yapılandır dikey toocontrol düğmeleri hello profil oluşturucu, tüm bağlı web uygulamaları.



![Dikey yapılandırın][linked app services]

toostop veya yeniden başlatma hello profil oluşturucu bağımsız bir uygulama hizmeti örnek için bulabilirsiniz, **hello uygulama hizmeti kaynak olarak**, **Web işleri**. toodelete, görünüm altında **uzantıları**.

![Web işleri için profil oluşturucu devre dışı bırak][disable-profiler-webjob]

Hello profil oluşturucu mümkün olan en kısa sürede tüm performans sorunları tüm, web uygulamaları toodiscover üzerinde etkin olmasını öneririz.

WebDeploy toodeploy değişiklikleri tooyour web uygulaması kullanırsanız, hello hariç olmak **App_Data** dağıtımı sırasında silinen gelen klasörü. Merhaba web uygulama tooAzure sonraki dağıttığınızda Aksi takdirde hello profil oluşturucu uzantının dosyalar silinir.

### <a name="using-profiler-with-azure-vms-and-compute-resources-preview"></a>Profil Oluşturucu Azure Vm'leri ve işlem kaynakları (Önizleme) ile kullanma

Olduğunda, [Application Insights Azure uygulama hizmetleri için çalışma zamanında etkinleştir](app-insights-azure-web-apps.md#run-time-instrumentation-with-application-insights), profil oluşturucu otomatik olarak kullanılabilir. (Application Insights zaten hello kaynak için etkinleştirilirse, tooupdate toohello lates sürümü hello üzerinden gerekebilecek **yapılandırma** Sihirbazı.)

Var olan bir [hello profil oluşturucu Azure işlem kaynakları için önizleme sürümünü](https://go.microsoft.com/fwlink/?linkid=848155).


## <a name="limits"></a>Sınırlar

Merhaba varsayılan veri saklama 5 gündür. En fazla 10 GB günde alınan.

Hello profil oluşturucu hizmeti için ücret ödemeden yoktur. İçinde web uygulamanızı barındırılmalıdır en az, uygulama hizmetleri, temel katmana hello.

## <a name="viewing-profiler-data"></a>Profil Oluşturucu verileri görüntüleme

Merhaba performans dikey ve toohello işlem listesinde aşağı kaydırın açın.




![Uygulama Öngörüler performans dikey örnekler sütun][performance-blade-examples]

Merhaba tablodaki Hello sütunlar şunlardır:

* **Count** -hello hello dikey penceresinde hello zaman aralığını bu isteklerin sayısı.
* **ORTANCA** -hello tipik süresi uygulamanızı toorespond tooa isteği alır. Tüm yanıtları yarısı bu değerden daha hızlı.
* **95** yanıtların % 95 bu değerden daha hızlı. Bu şekil hello ORTANCA çok farklı ise, uygulamanızı aralıklı bir sorun olabilir. (Veya önbelleğe alma gibi bir tasarım özelliği tarafından açıklanan.)
* **Örnekler** -o hello profil oluşturucu, bu işlem için Yığın izlemeleri yakalanan bir simge gösterir.

Merhaba örnekler simgesi tooopen hello izleme explorer'ı tıklatın. yanıt süresine göre sınıflandırılmış profil oluşturucu hello birkaç örnek yakalanan, hello explorer gösterir.

Bir örnek tooshow süresi geçen yürütülen hello isteği kodu düzeyi dökümünü seçin.

![Uygulama Öngörüler izleme Gezgini][trace-explorer]

**Sık kullanılan yolu Göster** açılır hello büyük yaprak düğümü ya da en az bir şey kapatın. Çoğu durumda bu düğüm bitişik tooa performans düşüklüğü olacaktır.



* **Etiket**: hello işlevin veya olay hello adı. Merhaba ağacı kodu ve (SQL ve http olayları gibi) oluşan olaylarla bir karışımını gösterir. Merhaba üst olay temsil eden hello genel istek süresi.
* **Geçen**: hello hello işlem başlangıcı ve hello bitiş arasındaki hello zaman aralığı.
* **Zaman**: hello işlevi/olay ilişkisi tooother işlevlerde zaman çalışıyordu gösterir.

## <a name="how-tooread-performance-data"></a>Nasıl tooread performans verileri

Microsoft Hizmet Profil Oluşturucu örnekleme yöntemini ve araçları tooanalyze hello uygulamanızın performansını, bir birleşimini kullanır.
Ayrıntılı toplama devam ederken, hizmet profil oluşturucu örnekleri her birinin her milisaniyelik hello makinenin CPU yönerge işaretçisi hello.
Her örnek hello tam çağrı yığını şu anda yürütülen, iş parçacığı hem yüksek ve düşük Soyutlama düzeyleri yapmakta olduğu, hangi hakkında ayrıntılı ve faydalı bilgileri vermiş hello iş parçacığının yakalar. Hizmet Profil Oluşturucu aynı zamanda diğer içerik geçiş olayları gibi olaylar, TPL olayları ve iş parçacığı havuzu olayları tootrack etkinlik bağıntısı ve causality toplar.

Merhaba zaman çizelgesi görünümünde gösterilen hello çağrı yığını hello örnekleme ve araçları yukarıda hello sonucudur. Her örnek hello tam çağrı yığını hello iş parçacığının yakalar çünkü başvuru diğer çerçeveler yanı sıra hello .NET framework koddan içerir.

### <a id="jitnewobj"></a>Nesne ayırma (`clr!JIT\_New or clr!JIT\_Newarr1`)
`clr!JIT\_New and clr!JIT\_Newarr1`Yönetilen yığınından bellek ayırır .NET framework içinde yardımcı işlevlerdir. `clr!JIT\_New`Nesne ayrılmış olduğunda çağrılır. `clr!JIT\_Newarr1`bir nesne dizisinin atandığında çağrılır. Bu iki işlevler tipik olarak çok hızlı ve görece küçük süreyi sürer. Görürseniz `clr!JIT\_New` veya `clr!JIT\_Newarr1` önemli bir süre içinde zaman çizelgeniz alın, onu hello kod birçok nesne ayırma ve önemli miktarda bellek tükettikten göstergesidir.

### <a id="theprestub"></a>Kod yükleme (`clr!ThePreStub`)
`clr!ThePreStub`Merhaba kod tooexecute hello için ilk kez hazırlar .NET framework içinde yardımcı işlevdir. Bu genellikle, ancak bunlarla sınırlı olmamak, (yalnızca süre) JIT derleme içerir. Her C# yönteminde `clr!ThePreStub` en fazla bir kez bir işlemin hello ömrü boyunca çağrılmalıdır.

Görürseniz `clr!ThePreStub` önemli ölçüde geçen bir istek için zaman bu istek olup, yöntemi ve .NET framework çalışma zamanı tooload yöntemi önemli olduğunu hello süredir yürüten birinci hello belirtir. Kullanıcılarınız erişmek veya NGen derlemeleriniz üzerinde çalıştırmayı düşünün önce hello kod bölümünü yürütür bir Isınma işlemi göz önünde bulundurabilirsiniz.

### <a id="lockcontention"></a>Kilit çakışması (`clr!JITutil\_MonContention` veya `clr!JITutil\_MonEnterWorker`)
`clr!JITutil\_MonContention`veya `clr!JITutil\_MonEnterWorker` hello geçerli iş parçacığının yayımlanan bir kilit toobe için bekleyen gösterir. Bu genellikle Monitor.Enter yönteminin çağrılması veya MethodImplOptions.Synchronized özniteliğine sahip bir yöntemi çağrılırken bir C# lock deyimi, yürütülürken görüntülenir. Kilit çakışması genellikle bir kilit iş parçacığı A alır ve iş parçacığı B iş parçacığı A bırakması önce aynı kilitlemek tooacquire hello çalışır olur.

### <a id="ngencold"></a>Kod yükleme (`[COLD]`)
Merhaba yöntemi adı içeriyorsa, `[COLD]`, gibi `mscorlib.ni![COLD]System.Reflection.CustomAttribute.IsDefined`, o hello .NET framework çalışma zamanı tarafından optimize edilmemiş kodu yürütme anlamına gelir <a href="https://msdn.microsoft.com/library/e7k32f4k.aspx">profil temelli iyileştirme</a> hello ilk kez için. Her yöntemi için en fazla bir kez hello işleminin hello ömrü boyunca gösterilmesi gerekir.

Kod yüklenirken önemli miktarda zaman için bir istek alırsa, bu istek hello ilk bir tooexecute hello iyileştirilmemiş hello yöntemi bölümüdür gösterir. Yarı kullanıcılarınızın erişebilmesi hello kod bölümünü yürütür işlemini göz önünde bulundurabilirsiniz.

### <a id="httpclientsend"></a>HTTP isteği gönder
Gibi yöntemler `HttpClient.Send` hello kodu için bir HTTP isteği toocomplete bekleyen gösterir.

### <a id="sqlcommand"></a>Veritabanı işlemi
Yöntemi SqlCommand.Execute gibi hello kodu için bir veritabanı işlemi toocomplete beklediğini gösterir.

### <a id="await"></a>Bekleyen (`AWAIT\_TIME`)
`AWAIT\_TIME`Hello kod için başka bir görev toocomplete beklediğini belirtir. Bu, genellikle C# ile await' deyimi' gerçekleşir. Merhaba kod yaptığında C# 'await 'özelliğini, hello iş parçacığı unwinds ve denetim toohello iş parçacığı havuzu döndürür ve hello 'await' toofinish için bekleyen engellenmiş iş parçacığı yok. Ancak, mantıksal olarak iş parçacığı hello await vermedi ' hello işlemi toocomplete için beklerken engellendi' hello. `AWAIT\_TIME` Hello görev toocomplete için bekleyen engellenmiş hello süresini gösterir.

### <a id="block"></a>Engellenen zaman
`BLOCKED_TIME`eşitleme nesnesi beklenirken, bir iş parçacığı toobe kullanılabilir ya da bir istek toofinish bekleniyor bekleniyor gibi kullanılabilir başka bir kaynak toobe Hello kodu bekleniyor gösterir.

### <a id="cpu"></a>CPU süresi
Merhaba CPU hello yönergeleri çalıştırmakla meşgul.

### <a id="disk"></a>Disk Zamanı
Merhaba uygulaması disk işlemleri gerçekleştiriyor.

### <a id="network"></a>Ağ süresi
Merhaba uygulaması ağ işlemlerini gerçekleştirme.

### <a id="when"></a>Zaman sütun
Merhaba dahil örnekleri için bir düğüm toplanan zaman içinde nasıl farklılık, bir görsel öğe budur. Merhaba isteği Hello toplam aralığı 32 zaman demet ayrılmıştır ve hello dahil örnekleri bu düğüm için bu 32 demet toplanır. Her demet sonra yükseklik ölçeklendirilmiş bir değeri temsil çubuğu olarak temsil edilir. İşaretlenen düğümleri için `CPU_TIME` veya `BLOCKED_TIME`, veya bir kaynağa (cpu, disk, iş parçacığı) kullanan, belirgin bir ilişki olduğunda, bu kaynaklardan biri hello süre bu demet, tüketen temsil çubuğu hello. Bu ölçümleri, birden fazla kaynak tüketen tarafından % 100'den büyük alabilirsiniz. Ortalama bir aralığı içinde iki CPU kullanırsanız, örneğin, daha sonra % 200 alırsınız.


## <a id="troubleshooting"></a>Sorun giderme

### <a name="how-can-i-know-whether-application-insights-profiler-is-running"></a>Application Insights profil oluşturucu çalışır durumda olup olmadığını nasıl öğrenebilirim?

Hello Profil Oluşturucu Web uygulamasında bir sürekli web işi olarak çalıştırır. Https://portal.azure.com içinde hello Web uygulaması kaynağı açın ve hello Web işleri dikey penceresinde "ApplicationInsightsProfiler" durumunu denetleyin. Çalışıyor durumda değilse, açmak **günlükleri** toofind daha fazla bilgi.

### <a name="why-cant-i-find-any-stack-examples-even-though-hello-profiler-is-running"></a>Neden Hello profil oluşturucu çalışıyor olsa bile tüm yığın örnekler bulamadınız mı?

İşte birkaç şey kontrol edebilirsiniz.

1. Web uygulama hizmet planınız, temel katmana olduğundan emin olun ve üstü.
2. Web uygulamanızın uygulama Öngörüler SDK 2.2 Beta sahiptir ve yukarıda etkin emin olun.
3. Web uygulamanıza Application Insights SDK'sı tarafından kullanılan aynı izleme anahtarını hello hello appınsıghts_ınstrumentatıonkey ayarıyla olduğundan emin olun.
4. Web uygulamanızı .net üzerinde çalıştığından emin olun Framework 4.6.
5. Lütfen bir ASP.NET Core uygulama ise, ayrıca denetleyin [hello gerekli bağımlılıkları](#aspnetcore).

Hello profil oluşturucu başlatıldıktan sonra ne zaman hello profil oluşturucu birkaç performans izlemeleri etkin olarak toplayan kısa Isınma Süresi yoktur. Bundan sonra hello profil oluşturucu performans izlemeleri iki dakika içinde her saat için toplar.  

### <a name="i-was-using-azure-service-profiler-what-happened-tooit"></a>Azure Hizmet Profil Oluşturucu tarafından kullanılan. Hangi happened tooit?  

Uygulama Öngörüler profil oluşturucu etkinleştirdiğinizde, Azure hizmet profil oluşturucu Aracısı devre dışı bırakılır.

### <a id="double-counting"></a>Çift paralel iş parçacığı sayımı

Bazı durumlarda hello toplam süre ölçümü hello yığını Görüntüleyicisi'nde hello gerçek süresi hello isteği, büyük.

Paralel olarak çalışan bir istekle ilişkili iki veya daha fazla iş parçacığı olduğunda bu durum oluşabilir. Merhaba toplam iş parçacığı saat sonra hello geçen süre büyük. Çoğu durumda tek bir iş parçacığı bekliyor olabilir diğer toocomplete hello. Bu Görüntüleyici çalıştığında toodetect hello ve hello sizi ilgilendirmeyen bekleme atlayın, ancak ne kritik bilgiler olabilir atlama yerine çok fazla gösteren, hello tarafında errs.  

Paralel iş parçacıkları, izlemeleri gördüğünüzde, böylece hello isteği hello kritik yolunu belirleyebilir, iş parçacıkları bekleyen toodetermine gerekir. Çoğu durumda, hızlı bir şekilde bekleme durumuna geçer yalnızca bekliyor üzerinde hello iş parçacığı başka bir iş parçacığı hello. Yoğunlaşabilirsiniz başkalarının hello ve hello bekleyen iş parçacıklarının hello zamanında yoksay.

### <a id="issue-loading-trace-in-viewer"></a>Profil oluşturma veri yok

1. Merhaba veri deniyorsanız tooview birkaç haftalık eski zaman filtresi görüntülemeyi deneyin ve yeniden deneyin.

2. Proxy'leri veya bir güvenlik duvarı erişim toohttps://gateway.azureserviceprofiler.net engellemediğinizden denetleyin.

3. Application Insights izleme anahtarı uygulamanızda kullandığınız aynı hello ile profil etkinleştirdikten Application Insights kaynağı olarak hello bu hello denetleyin. başlangıç anahtarı genellikle Applicationınsights.Config'de ancak web.config veya app.config de bulunabilir.

### <a name="error-report-in-hello-profiling-viewer"></a>Hata raporu içinde hello Görüntüleyicisi profil oluşturma

Bir destek bileti hello portalından dosya. Merhaba bağıntı kimliği hello hata iletisi içerir.

## <a name="manual-installation"></a>El ile yükleme

Hello profil oluşturucu yapılandırdığınızda hello aşağıdaki güncelleştirmeleri toohello Web uygulamanızın ayarlar yapılır. El ile ortamınız, örneğin, uygulamanızı Azure uygulama hizmeti ortamı (ana) çalıştırılıp çalıştırılmadığını gerektiriyorsa, bunları kendiniz yapabilirsiniz:

1. Merhaba web uygulaması denetim dikey penceresinde ayarları'nı açın.
2. Ayarlama ".Net Framework sürümünü" toov4.6.
3. TooOn "Her zaman açık" olarak ayarlayın.
4. Uygulama ayarı ekleme "__appınsıghts_ınstrumentatıonkey__" ve kümesi hello değeri toohello aynı izleme anahtarını hello SDK tarafından kullanılır.
5. Gelişmiş Araçlar'ı açın.
6. Tooopen hello Kudu Web sitesi "Git"'i tıklatın.
7. "Site uzantılarını" Merhaba Kudu Web sitesi seçin.
8. Yükleme "__Application Insights__" galerisinden.
9. Merhaba web uygulaması yeniden başlatın.

## <a id="aspnetcore"></a>ASP.NET çekirdeği desteği

ASP.NET Core uygulamanın tooinstall Microsoft.ApplicationInsights.AspNetCore Nuget Paketi 2.1.0-beta6 ya da daha yüksek toowork hello Profil Oluşturucu ile gerekir. Artık hello alt sürümleri 27/6/2017 sonra destekliyoruz.

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
