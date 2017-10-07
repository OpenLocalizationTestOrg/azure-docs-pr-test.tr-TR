---
title: Visual Studio'da Azure Application Insights aaaDebug uygulamalarla | Microsoft Docs
description: "Hata ayıklama ve üretim sırasında wen uygulaması performans analizi ve tanılama."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/7/2017
ms.author: bwren
ms.openlocfilehash: 20491fbe4505bf719039e5d1c220b1afec01db25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a>Visual Studio'da Azure Application Insights uygulamalarınızla hata ayıklama
Visual Studio’da (2015 ve sonraki sürümler) hem hata ayıklama hem de üretim sırasında [Azure Application Insights](app-insights-overview.md)’tan alınan telemetri verilerini kullanarak, ASP.NET web uygulamanızdaki performansı çözümleyebilir ve sorunları tanılayabilirsiniz.

Visual Studio 2017'nı kullanarak ASP.NET web uygulamanızı oluşturduğunuz veya daha sonra hello Application Insights SDK'sı zaten sahip olur. Aksi takdirde, bu nedenle, bu işlemi yapmadıysanız [Application Insights tooyour uygulama Ekle](app-insights-asp-net.md).

toomonitor uygulamanızı Canlı üretimde olduğunda, normalde hello hello Application Insights telemetriyi görüntüleyebilir [Azure portal](https://portal.azure.com), burada uyarıları ayarlama ve güçlü izleme araçlarını uygulayın. Ancak, hata ayıklama için ayrıca arama ve Visual Studio hello telemetriyi çözümle. Visual Studio tooanalyze telemetri üretim sitenizden hem çalıştırır, geliştirme makinenizde hata ayıklama kullanabilirsiniz. Merhaba SDK toosend telemetri toohello Azure portal henüz yapılandırılmamış henüz olsa bile, hello ikinci durumda, hata ayıklama çalışmalarınızı çözümleyebilirsiniz. 

## <a name="run"></a> Projenizin hatalarını ayıklama
F5 kullanarak web uygulamanızı yerel hata ayıklama modunda çalıştırın. Farklı sayfalara toogenerate bazı telemetriyi açın.

Visual Studio'da, projenizdeki hello Application Insights modülü tarafından günlüğe hello etkinliklerin sayısını görürsünüz.

![Visual Studio'da hata ayıklama sırasında hello Application Insights düğmesi gösterilir.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

Bu düğme toosearch telemetrinizi'ı tıklatın. 

## <a name="application-insights-search"></a>Application Insights araması
Merhaba uygulama Insights arama penceresi günlüğe kaydedilmiş olayları gösterir. (Application Insights'ı ayarladığınızda tooAzure kaydolduysanız arayabilirsiniz hello hello Azure portal'ın olaylar ile aynıdır.)

![Merhaba projesine sağ tıklayın ve Application Insights seçme arama](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> Filtre seçimini kaldırın veya seçin sonra hello metin arama alanı hello sonunda hello arama düğmesini tıklatın.
>

Merhaba serbest metin arama hello olayları tüm alanlarda çalışır. Örneğin, bir sayfanın hello URL'SİNİN bir parçası için arama; ya da istemcinin şehri gibi bir özelliğin değerini hello; veya bir izleme günlüğündeki belirli kelimeleri.

Tüm olay toosee ayrıntılı özelliklerini'ı tıklatın.

İstekleri tooyour web uygulaması için toohello koduyla tıklatabilirsiniz.

![İstek Ayrıntıları altında toohello koduyla'ı tıklatın.](./media/app-insights-visual-studio/31.png)

İlgili öğeler de açabilirsiniz toohelp tanılamak başarısız isteklerin veya özel durumları.

![İstek Ayrıntıları altında toorelated öğeleri kaydırın](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a>Özel durumları görüntüle ve başarısız isteklerin
Merhaba arama penceresinde özel durum raporları göster. (ASP.NET uygulaması bazı eski türlerinde çok elinizde[özel durum izleme ayarladıysanız](app-insights-asp-net-exceptions.md) hello çerçevesi tarafından işlenen toosee özel durumlar.)

Bir özel durum tooget Yığın İzleme'yi tıklatın. Visual Studio'da hello uygulamanın Hello kodunu açıksa, hello yığın izleme toohello ilgili satırından hello kod aracılığıyla tıklayabilirsiniz.

![Özel durum yığın izlemesi](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-hello-code"></a>Merhaba kodda istek ve özel durum özetlerini görüntüleyin
Hello her işleyici yöntemi Yukarıdaki kod Mercek satır, hello istekler ve özel durumlar Application Insights tarafından hello son 24 h oturum sayısını bakın.

![Özel durum yığın izlemesi](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> Kod Mercek varsa yalnızca Application Insights verileri gösterir [uygulama toosend telemetri toohello Application Insights portalınızdaki yapılandırılmış](app-insights-asp-net.md).
>

[Kod Odağı’nda Application Insights hakkında daha fazla bilgi](app-insights-visual-studio-codelens.md)

## <a name="trends"></a>Eğilimler
Eğilimler, uygulamanızın zaman içinde nasıl davrandığını görselleştirmeye yönelik bir araçtır. 

Seçin **Telemetri eğilimlerini keşfet** hello Application Insights araç çubuğu düğmesini veya uygulama Insights arama penceresi. Başlatılan beş ortak sorguları tooget birini seçin. Telemetri türleri, zaman aralıkları ve diğer özelliklere göre farklı veri kümelerini çözümleyebilirsiniz. 

verilerinizde, toofind anormallikleri hello "Görünüm türü" açılan altındaki hello anomali seçeneklerden birini seçin. Merhaba filtreleme seçenekleri hello pencerenin hello altındaki içinde kolay toohone üzerinde belirli alt olun.

![Eğilimler](./media/app-insights-visual-studio/51.png)

[Eğilimler hakkında daha fazla bilgi](app-insights-visual-studio-trends.md).

## <a name="local-monitoring"></a>Yerel izleme
(Visual Studio 2015 Update'ten 2) Merhaba SDK toosend telemetri toohello Application Insights portalındaki yapılandırmadıysanız (yani izleme anahtarı Applicationınsights.Config'de) hello tanılama penceresinde en son hata ayıklama oturumunuzda telemetri görüntüler. 

Daha önce uygulamanızın önceki bir sürümünü yayımladıysanız bu iyi bir şeydir. Hata ayıklama oturumları toobe hello telemetrisinden hello hello telemetriyi ile Merhaba yayımlanan uygulamanın Application Insights portalından karma istemezsiniz.

Bazı varsa de kullanışlıdır [özel telemetri](app-insights-api-custom-events-metrics.md) telemetri toohello portal göndermeden önce toodebug istiyor.

* *İlk başta, t tam olarak Application Insights toosend telemetri toohello portal yapılandırılmamış. Ancak şimdi toosee hello telemetriyi yalnızca Visual Studio'da istersiniz.*
  
  * Merhaba arama penceresinin Ayarlar bölümünde var. bir seçenek toosearch yerel tanılama uygulamanızı telemetri toohello portal gönderse bile
  * toohello portalı, açıklama hello satırı çıkışı gönderilen toostop telemetri `<instrumentationkey>...` applicationınsights.Config'de. Hazır toosend telemetri toohello portal yeniden olduğunuzda açıklamayı kaldırın.


## <a name="next-steps"></a>Sonraki adımlar
|  |  |
| --- | --- |
| **[Daha fazla veri ekleme](app-insights-asp-net-more.md)**<br/>Kullanımı, kullanılabilirliği, bağımlılıkları, özel durumları izleyin. Günlük altyapılarından izlemeleri tümleştirin. Özel telemetri yazın. |![Visual studio](./media/app-insights-visual-studio/64.png) |
| **[Merhaba Application Insights portalıyla çalışma](app-insights-dashboards.md)**<br/>Panolar, güçlü tanılama ve analiz araçları, uyarılar, uygulama ve dışarı aktarılan telemetri verileri Canlı bağımlılık Haritası görüntüleyin. |![Visual studio](./media/app-insights-visual-studio/62.png) |

