---
title: "aaaMonitor uygulamanızın sistem durumu ve Application Insights ile kullanım"
description: "Application Insights ile çalışmaya başlayın. Kullanım, kullanılabilirlik ve şirket içi veya Microsoft Azure uygulamalarının performansını analiz edin."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 9230a6e65e5afb00c36122ff1d1de01ba19cd7f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-in-web-applications"></a>Web uygulamalarının performansını izleme


Uygulamanızın düzgün çalışıp emin olun ve hatalar hakkında hızlı bir şekilde öğrenin. [Application Insights] [ start] herhangi bir performans sorunlarını ve özel durumlar hakkında söyleyin ve bulmak ve hello tanılamanıza yardımcı kök neden olur.

Application Insights, Java ve ASP.NET web uygulamaları ve Hizmetleri, WCF hizmetleri izleyebilirsiniz. Bunlar barındırılan şirket içi, sanal makinelerde ya da Microsoft Azure Web siteleri farklı olabilir. 

Merhaba istemci tarafında, Application Insights telemetri web sayfalarını ve çok çeşitli cihazlar iOS, Android ve Windows mağazası uygulamaları dahil olmak üzere alabilir.

>[!Note]
> Size yeni bir deneyim bulma yavaş sayfaları web uygulamanızda gerçekleştirmek için kullanılabilir yaptınız. Erişim tooit yoksa, Önizleme seçeneklerinizi hello ile yapılandırarak etkinleştirmek [Önizleme dikey](app-insights-previews.md). Bu yeni deneyim okuyun [bulup hello etkileşimli performans araştırma ile performans sorunları giderin](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).

## <a name="setup"></a>Performans izleme işlevini ayarlama
Application Insights tooyour henüz eklemediyseniz (diğer bir deyişle, Applicationınsights.config yoksa) projesi, şu yöntemlerden birini kullanarak seçin tooget başlatıldı:

* [ASP.NET web uygulamaları](app-insights-asp-net.md)
  * [Özel durum izleme Ekle](app-insights-asp-net-exceptions.md)
  * [Bağımlılık izleme Ekle](app-insights-monitor-performance-live-website-now.md)
* [J2EE web uygulamaları](app-insights-java-get-started.md)
  * [Bağımlılık izleme Ekle](app-insights-java-agent.md)

## <a name="view"></a>Performans ölçümleri keşfederken
İçinde [Azure portal hello](https://portal.azure.com), uygulamanız için ayarladığınız toohello Application Insights kaynağı göz atın. Merhaba genel bakış dikey temel performans verilerini gösterir:

Tüm grafik toosee toosee sonuçları ve daha fazla ayrıntı için daha uzun bir süre tıklayın. Örneğin, hello istekleri kutucuğa tıklayın ve bir zaman aralığı seçin:

![Toomore verilerine tıklayın ve bir zaman aralığı seçin](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

Bir grafik toochoose, görüntüler, veya yeni bir grafik ekleyin ve onun ölçümleri seçin hangi ölçümleri tıklatın:

![Bir grafik toochoose ölçümleri'ı tıklatın](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> **Tüm hello ölçümleri işaretini** kullanılabilir toosee hello tam seçimi. Merhaba ölçümleri gruba ayrılır; herhangi bir grubun üyesi seçildiğinde, bu yalnızca hello diğer grubun üyesi görünür.

## <a name="metrics"></a>Tüm ortalama yaptığı? Performans kutucukları ve raporlar
Çeşitli performans ölçümleri alma vardır. Varsayılan hello uygulaması dikey penceresinde görünen olanla başlayalım tıklatın.

### <a name="requests"></a>İstekler
Merhaba belirli bir süre içinde alınan HTTP isteklerinin sayısı. Bu hello yük değiştikçe uygulamanızı nasıl davranacağını diğer raporları toosee hello sonuçlarına karşılaştırın.

HTTP istekleri sayfaları, veri ve görüntüleri için tüm GET veya POST istekleri içerir.

Merhaba döşeme tooget sayar belirli URL'ler için tıklatın.

### <a name="average-response-time"></a>Ortalama yanıt süresi
Döndürülen uygulama ve hello yanıtınız girerek web isteği arasındaki ölçüleri hello süre.

Başlangıç noktaları bir hareketli ortalama gösterir. Çok sayıda isteği varsa, olabilir hello ortalama belirgin yoğun olmayan gelen sapma veya hello grafiğinde DIP bazı.

Olağan dışı yükselmeleri arayın. Genel olarak, bir artışa istekleri ile yanıt süresi toorise bekler. Hello neden orantısız ise, uygulamanızın kullandığı bir hizmet CPU veya hello kapasitesi gibi bir kaynak sınırına ulaşması.

Merhaba döşeme tooget kez belirli URL'ı tıklatın.

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a>En yavaş istekler
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

Hangi isteklerinin performans ayarlaması gerekebilir gösterir.

### <a name="failed-requests"></a>Başarısız istekler
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

Yakalanmayan bir özel durum oluşturdu isteği sayısı.

Merhaba döşeme toosee hello belirli hataları ayrıntılarını tıklayın ve kendi ayrıntı ayrı istek toosee seçin. 

Hatalar için temsili bir örnek için tek tek denetleme korunur.

### <a name="other-metrics"></a>Diğer ölçümleri
toosee görüntülemek, bir grafiğe tıklayın ve ardından tüm hello ölçümleri toosee hello tam kullanılabilir seçimini kaldırın hangi diğer ölçümleri. ()'ı toosee her ölçümü 's tanımı.

![Tüm ölçümleri toosee hello tüm seçimini kaldırın](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

Tüm ölçüm devre dışı bırakır hello seçerek üzerinde bulunamaz başkalarının aynı grafik hello.

## <a name="set-alerts"></a>Uyarı ayarlama
alışılmadık değerlerin herhangi bir ölçümü, e-postayla bildirim toobe bir uyarı ekleyin. Toosend hello e-posta toohello hesap yöneticileri ya da toospecific e-posta adreslerini seçebilirsiniz.

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

Merhaba kaynak hello önce diğer özellikleri ayarlayın. Performans ya da kullanım ölçümleri tooset uyarılar istiyorsanız hello Web testine kaynakları seçmeyin.

Dikkatli toonote hello birimleri tooenter hello eşik değeri sorulur olabilir.

*Merhaba Ekle uyarı düğmesini görmek yok.* -Bu salt okunur erişime sahip bir grup hesabı toowhich mi? Merhaba hesap yöneticinize danışın.

## <a name="diagnosis"></a>Sorunlarını tanılama
Aşağıda, bulma ve performans sorunlarını tanılamak için birkaç ipucu verilmiştir:

* Ayarlanan [web testleri] [ availability] web sitenizi arıza ya da yanlış veya yavaş yanıt uyarı toobe. 
* Hataları veya yavaş yanıt ilgili tooload varsa hello isteği diğer ölçümleri toosee sayısıyla karşılaştırın.
* [Ekle ve arama izleme deyimleri] [ diagnostic] sorunları, kod toohelp sabitleme.
* Web uygulamanızda işlemiyle izlemek [ölçümleri bir canlı akışı][livestream].
* .Net uygulamanızla Hello durumunu yakalama [anlık görüntü hata ayıklayıcı][snapshot].

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a>Bulun ve etkileşimli performans araştırma ile performans sorunları giderin

Genel performansını yavaşlamasının hello yeni Application Insights etkileşimli performans araştırma toolocate alanlarını Web uygulamanızı kullanabilirsiniz. Yavaşlamadan olan ve hello kullanan Bul belirli sayfaları hızla yapabilirsiniz [profil oluşturma aracı](app-insights-profiler.md) bu sayfaları arasında bir bağıntı ise toosee.

### <a name="create-a-list-of-slow-performing-pages"></a>Yavaş gerçekleştiren sayfalar listesi oluşturma 

performans sorunları bulmak için ilk adımı hello tooget hello sayfaları yanıt yavaş listesini oluşturur. Aşağıda gösterilen hello ekran hello performans dikey tooget olası sayfaları tooinvestigate daha ayrıntılı bir listesini kullanmayı gösterir. Bu sayfadan yaklaşık 6:00 PM ve yeniden yaklaşık 10 PM, olduğunu bir konumlanır hello uygulama yanıt süresini hello hızlı şekilde görebilirsiniz. Merhaba GET müşteri/Ayrıntılar işlemi işlemleri bir 507.05 milisaniye ortalama yanıt süresi ile uzun çalışan olduğunu da görebilirsiniz. 

![Uygulama Öngörüler etkileşimli performansı](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a>Belirli sayfalara detaya gitme

Uygulamanızın performansını görüntüsünü oluşturduktan sonra belirli yavaş performanslı işlemleri daha fazla bilgi alabilirsiniz. Aşağıda gösterildiği gibi hello listesi toosee hello ayrıntıları herhangi bir işlem tıklayın. Merhaba grafikten hello performans bir bağımlılığı dayanarak if görebilirsiniz. Kaç tane kullanıcılar deneyimli hello çeşitli yanıt sürelerini de görebilirsiniz. 

![Uygulama Öngörüler işlemleri dikey penceresi](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a>Belirli bir döneme detaya gitme

Zaman tooinvestigate noktasında tanımladıktan sonra hatta başka toolook hello performans konumlanır neden olabilecek hello belirli işlemler sırasında detaya. Belirli bir noktasında zamanında tıkladığınızda hello Ayrıntılar aşağıda gösterildiği gibi hello sayfasının alın. Hello hello sunucu yanıt kodları ve hello işlemi süresi yanı sıra belirli bir süre için listelenen hello işlemleri, aşağıdaki örnekte görebilirsiniz. Ayrıca bu bilgileri tooyour geliştirme ekibi toosend ihtiyacınız varsa, TFS iş öğesi açmak için hello url vardır.

![Uygulama Öngörüler saat dilimi](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a>Belirli bir işlemi detaya gitme

Zaman tooinvestigate noktasında tanımladıktan sonra hatta başka toolook hello performans konumlanır neden olabilecek hello belirli işlemler sırasında detaya. Bir işlem hello listesi toosee hello ayrıntıları aşağıda gösterildiği gibi hello işleminin tıklayın. Merhaba işlemi başarısız oldu ve Application Insights hello hello ayrıntılarını sağlamıştır görebilirsiniz Bu örnekte hello uygulama özel durum oluşturdu. Yeniden, bu dikey pencereden bir TFS iş öğesi kolayca oluşturabilirsiniz.

![Uygulama Öngörüler işlemi dikey penceresi](./media/app-insights-web-monitor-performance/performance3.png)


## <a name="next"></a>Sonraki adımlar
[Web testleri] [ availability] -web istekleri tooyour uygulama düzenli aralıklarla Merhaba Dünya göndermiş.

[Yakalama ve arama tanılama izlemeleri] [ diagnostic] - Ekle izleme çağrıları ve hello sonuçları toopinpoint sorunları SIFT.

[Kullanımı izleme] [ usage] -kişiler, uygulamanızın kullanımını bulun.

[Sorun giderme] [ qna] - ve soru- cevap



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



