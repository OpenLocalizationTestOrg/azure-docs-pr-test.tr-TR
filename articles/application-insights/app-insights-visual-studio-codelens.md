---
title: Visual Studio CodeLens Insights telemetri aaaApplication | Microsoft Docs
description: "Application Insights istek ve özel durum telemetrinize Visual Studio’daki CodeLens ile hızlıca erişin."
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 93559e44-23cb-4b9d-8425-60f7f0d0a82c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: e812aa48f2a67eea860e7ecde341855763bb8a8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-in-visual-studio-codelens"></a>Visual Studio CodeLens’te Application Insights telemetrisi
Merhaba kod, web uygulamanızın yöntemleri, çalışma zamanı özel durumlar hakkında telemetri ile Açıklama ve yanıt sürelerini isteyin. Yüklerseniz [Azure Application Insights](app-insights-overview.md) uygulamanızda, Visual Studio'da hello telemetri görünen [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx) -hello notları kullanıldığı her işlevi hello üstündeki tooseeing yararlı Yerler hello işlevi hello sayısı gibi bilgiler başvuruluyor veya Düzenleyen son kişiye hello.

![CodeLens](./media/app-insights-visual-studio-codelens/codelens-overview.png)

> [!NOTE]
> Application Insights codelens'te Visual Studio 2015 güncelleştirme 3'te kullanılabilir ve daha sonra veya hello en son sürümü ile [Geliştirici analiz araçları uzantısı](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a). CodeLens hello Enterprise ve Professional Visual Studio sürümlerinde kullanılabilir.
> 
> 

## <a name="where-toofind-application-insights-data"></a>Burada toofind Application Insights veri
Merhaba CodeLens göstergelerini hello genel istek yöntemleri web uygulamanıza Application Insights telemetri arayın. CodeLens göstergeleri yöntemin ve diğer bildirimlerin üstünde C# ve Visual Basic code dillerinde gösterilir. Bir yöntem için Application Insights verileri mevcutsa "100 istek, %1 başarısız" veya "10 özel durum" gibi istek ve özel durum göstergeleri görürsünüz. Daha fazla ayrıntı için bir CodeLens göstergesine tıklayın. 

> [!TIP]
> Application Insights istemek ve özel durum göstergeleri, fazladan birkaç saniye sürebilir diğer CodeLens göstergeleri göründükten sonra tooload.
> 
> 

## <a name="exceptions-in-codelens"></a>CodeLens’teki özel durumlar
![TBD](./media/app-insights-visual-studio-codelens/codelens-exceptions.png)

Merhaba özel durum CodeLens göstergesi hello hello 15 hello isteği işlerken bağlı olarak, bu süre boyunca, uygulamanızdaki en sık tekrarlanan özel durumlar hello yöntemi tarafından sunulan gelen Son 24 saatte oluşan özel durumlar hello sayısını gösterir.

toosee daha ayrıntılı, hello özel durumları CodeLens göstergesi tıklatın:

* Merhaba yüzdesi 24 saat sayısı hello en son 24 saat göreli toohello önceki özel durumlar olarak değiştirme
* Seçin **Git toocode** toonavigate toohello kaynak kodunu hello özel durum atma hello işlevi
* Seçin **arama** son 24 saat içinde gerçekleşen bu özel durumun tüm örneklerini hello tooquery
* Seçin **eğilim** tooview bu özel durumun son 24 saat içinde hello yineleme için bir eğilim Görselleştirme
* Seçin **Bu uygulamadaki tüm özel durumlarını görüntülemek** tooquery hello son 24 saat içinde gerçekleşen tüm özel durumları
* Seçin **özel durum eğilimleri keşfedin** tooview eğilim görselleştirme hello son 24 saatte oluşan tüm özel durumlar için. 

> [!TIP]
> "0 özel durumlar" CodeLens bakın, ancak özel durumlar olmalıdır bildiğiniz toomake hello doğru Application Insights kaynağı CodeLens seçili olduğundan emin denetleyin. tooselect başka bir kaynak hello Çözüm Gezgini'nde projenize sağ tıklayın ve seçin **Application Insights > Telemetri Kaynağı Seç**. CodeLens yalnızca 15 hello için en sık karşılaşılan özel durumlar hello uygulamanızda son 24 saat kadar olan bir özel durum Merhaba, 16 en sık veya daha az gösterilen, "0 özel durumlar." görürsünüz Özel durumlar ASP.NET görünümlerden bu görünümler oluşturulan hello denetleyicisi yöntemlerde görünmeyebilir.
> 
> [!TIP]
> CodeLens’te "? özel durumlar"codelens'te, Visual Studio ya da Azure hesabı kimlik bilgileriniz Azure hesabınızla süresi sona ermiş olabilir tooassociate gerekir. Her iki durumda da "? özel durumlar"ve **Hesap Ekle...**  tooenter kimlik bilgilerinizi.
> 
> 

## <a name="requests-in-codelens"></a>CodeLens’teki istekler
![TBD](./media/app-insights-visual-studio-codelens/codelens-requests.png)

Merhaba CodeLens gösterge gösterir hello HTTP sayısı isteği isteklerine edilmiş 24 saat yanı sıra, başarısız olan bu isteklerin yüzdesini hello geçmiş hello yönteminde hizmet verilen.

Daha fazla ayrıntı toosee tıklatın hello CodeLens göstergesi ister:

* 24 saat karşılaştırıldığında 24 saat toohello önceki geçmiş hello üzerinden istekleri, başarısız olan istekler ve ortalama yanıt sürelerini sayısını mutlak ve yüzde değişiklikleri hello
* Merhaba güvenilirliğini hello son 24 saat başarısız olmadıysa istekleri hello yüzdesi olarak hesaplanan hello yöntemi
* Seçin **arama** istekleri ya da tüm hello hello son 24 saatte oluştu (başarısız) istekler başarısız isteklerin tooquery için
* Seçin **eğilim** tooview eğilim görselleştirme istekleri, başarısız olan istekler veya ortalama yanıt süresi hello son 24 saat.
* Merhaba sol üst köşesinde hello CodeLens Ayrıntılar görünümü toochange hello kaynağıdır CodeLens verileri için hangi kaynak hello Application Insights kaynağı Hello adını seçin.

## <a name="next"></a>Sonraki adımlar
|  |  |
| --- | --- |
| **[Visual Studio’da Application Insights ile çalışma](app-insights-visual-studio.md)**<br/>Telemetri arayın, CodeLens içindeki verilere bakın ve Application Insights’ı yapılandırın. Hepsi Visual Studio’da. |![Merhaba projesine sağ tıklayın ve Application Insights seçme arama](./media/app-insights-visual-studio-codelens/34.png) |
| **[Daha fazla veri ekleme](app-insights-asp-net-more.md)**<br/>Kullanımı, kullanılabilirliği, bağımlılıkları, özel durumları izleyin. Günlük altyapılarından izlemeleri tümleştirin. Özel telemetri yazın. |![Visual studio](./media/app-insights-visual-studio-codelens/64.png) |
| **[Merhaba Application Insights portalıyla çalışma](app-insights-dashboards.md)**<br/>Panolar, güçlü tanılama ve analiz araçları, uyarılar, uygulamanızın canlı bağımlılık haritası ve telemetriyi dışarı aktarma. |![Visual studio](./media/app-insights-visual-studio-codelens/62.png) |

