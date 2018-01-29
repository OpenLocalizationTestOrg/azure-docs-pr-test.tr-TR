---
title: "Visual Studio CodeLens’te Application Insights telemetrisi | Microsoft Belgeleri"
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
ms.author: mbullwin
ms.openlocfilehash: 418c391f896ac60f509b963f0aff70ad699fc43b
ms.sourcegitcommit: e462e5cca2424ce36423f9eff3a0cf250ac146ad
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/01/2017
---
# <a name="application-insights-telemetry-in-visual-studio-codelens"></a>Visual Studio CodeLens’te Application Insights telemetrisi
Web uygulamanızın kodundaki yöntemlere, çalışma zamanı özel durumları ve istek yanıt süreleri hakkında telemetri ile açıklama eklenebilir. [Azure Application Insights](app-insights-overview.md)’ı uygulamanıza yüklerseniz telemetri Visual Studio [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx) içinde (işlevin başvurulduğu yer sayısı veya düzenleyen kişi gibi yararlı bilgileri görmeye alışkın olduğunuz her bir işlevin üst kısmında) görünür.

![CodeLens](./media/app-insights-visual-studio-codelens/codelens-overview.png)

> [!NOTE]
> CodeLens içinde Application Insights, Visual Studio 2015 Güncelleştirme 3 ve üstü ya da [Developer Analytics Tools uzantısının](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a) en sürümleri ile birlikte kullanılabilir. CodeLens, Visual Studio’nun Enterprise ve Professional sürümlerinde kullanılabilir.
> 
> 

## <a name="where-to-find-application-insights-data"></a>Application Insights verileri nerede bulunur
Application Insights telemetrisini web uygulamanızın ortak istek yöntemlerinin CodeLens göstergeleri içinde arayın. CodeLens göstergeleri yöntemin ve diğer bildirimlerin üstünde C# ve Visual Basic code dillerinde gösterilir. Bir yöntem için Application Insights verileri mevcutsa "100 istek, %1 başarısız" veya "10 özel durum" gibi istek ve özel durum göstergeleri görürsünüz. Daha fazla ayrıntı için bir CodeLens göstergesine tıklayın. 

> [!TIP]
> Diğer CodeLens göstergelerinin görünmesinden önce Application Insights istek ve özel durum göstergelerinin yüklenmesi birkaç saniye daha sürebilir.
> 
> 

## <a name="exceptions-in-codelens"></a>CodeLens’teki özel durumlar
![TBD](./media/app-insights-visual-studio-codelens/codelens-exceptions.png)

CodeLens özel durum göstergesi, yöntemin sunduğu isteği işlerken son 24 içinde uygulamanızda en sık gerçekleşen 15 özel durumdan birkaç tanesini gösterir.

Daha fazla ayrıntı için CodeLens özel durum göstergesine tıklayın:

* Önceki 24 saat le onun öncesindeki 24 saat arasında özel durum sayısında meydana gelen değişiklik yüzdesi
* Özel durumu oluşturan işlevin kaynak koduna gitmek için **Koda git** öğesini seçin
* Bu özel durumun son 24 saat içinde gerçekleşen tüm örneklerini sorgulamak için **Ara**’yı seçin
* Bu özel durumun son 24 saat içinde gerçekleşen tüm örneklerine ilişkin bir eğilim görselini görüntülemek için **Eğilim**’i seçin
* Son 24 saat içinde gerçekleşen tüm özel durumları sorgulamak için **Bu uygulamadaki tüm özel durumları görüntüle**’yi seçin
* Son 24 saat içinde gerçekleşen tüm özel durumlara ilişkin bir eğilim görselini görüntülemek için **Özel durum eğilimlerini keşfet**’i seçin. 

> [!TIP]
> CodeLens’te "0 özel durum" görmenize karşın özel durumlar olması gerektiğini biliyorsanız CodeLens’te doğru Application Insights kaynağının seçildiğinden emin olun. Başka bir kaynak seçmek için Çözüm Gezgini'nde projenize sağ tıklayın ve **Application Insights > Telemetri Kaynağı Seç** öğesini seçin. CodeLens, uygulamanızda yalnızca son 24 saat içinde en sık gerçekleşen 15 özel durum için gösterilir; dolayısıyla özel durum en sık gerçekleşen 16. veya daha sonraki bir özel durumsa "0 özel durum" görürsünüz. ASP.NET görünümlerindeki özel durumlar bu görünümleri oluşturan denetleyici yöntemlerinde görünmeyebilir.
> 
> [!TIP]
> CodeLens’te "? özel durum" görürseniz Azure hesabınızı Visual Studio ile ilişkilendirmeniz gerekebilir veya Azure hesabı kimlik bilgilerinizin süresi dolmuş olabilir. Her iki durumda da "? özel durum" öğesine tıklayın ve **Hesap ekle...** öğesini seçerek kimlik bilgilerinizi girin.
> 
> 

## <a name="requests-in-codelens"></a>CodeLens’teki istekler
![TBD](./media/app-insights-visual-studio-codelens/codelens-requests.png)

CodeLens istek göstergesi son 24 saat içinde bir yöntemin sunduğu HTTP isteklerinin sayısını ve başarısız olan isteklerin yüzdesini gösterir.

Daha fazla ayrıntı için CodeLens istek göstergesine tıklayın:

* Son 24 saat ile ondan önceki 24 saat içinde gerçekleşen istek, başarısız istek ve ortalama yanıt sürelerinin mutlak değişimleri ile değişiklik yüzdelerini karşılaştırma
* Son 24 saatte başarısız olmayan isteklerin yüzdesi olarak hesaplanan yöntem güvenilirliği
* Son 24 saatte gerçekleşen tüm (başarısız) istekleri sorgulamak üzere istekler ya da başarısız istekler için **Ara**’yı seçin
* Son 24 saatte gerçekleşen istek, başarısız istek veya ortalama yanıt sürelerine ilişkin bir eğilim görselini görüntülemek için **Eğilim**’i seçin.
* CodeLens verilerinin kaynağını değiştirmek için CodeLens ayrıntılı görünümünün sol üst köşesinden Application Insights kaynağının adını seçin.

## <a name="next"></a>Sonraki adımlar
|  |  |
| --- | --- |
| **[Visual Studio’da Application Insights ile çalışma](app-insights-visual-studio.md)**<br/>Telemetri arayın, CodeLens içindeki verilere bakın ve Application Insights’ı yapılandırın. Hepsi Visual Studio’da. |![Projeye sağ tıklayın ve Application Insights, Ara’yı seçin](./media/app-insights-visual-studio-codelens/34.png) |
| **[Daha fazla veri ekleme](app-insights-asp-net-more.md)**<br/>Kullanımı, kullanılabilirliği, bağımlılıkları, özel durumları izleyin. Günlük altyapılarından izlemeleri tümleştirin. Özel telemetri yazın. |![Visual studio](./media/app-insights-visual-studio-codelens/64.png) |
| **[Application Insights portalıyla çalışma](app-insights-dashboards.md)**<br/>Panolar, güçlü tanılama ve analiz araçları, uyarılar, uygulamanızın canlı bağımlılık haritası ve telemetriyi dışarı aktarma. |![Visual studio](./media/app-insights-visual-studio-codelens/62.png) |

