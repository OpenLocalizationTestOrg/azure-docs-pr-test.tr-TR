---
title: "Azure Application Insights aaaSet uyarılar | Microsoft Docs"
description: "Yavaş yanıt süreleri, özel durumlar ve diğer performans veya web uygulamanızda kullanım değişiklikler hakkında bilgi edinin."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: f8ebde72-f819-4ba5-afa2-31dbd49509a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: e160cb173e68fda2e6d97f29da342c46b7ac4f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-alerts-in-application-insights"></a>Application Insights'ta uyarıları ayarlama
[Azure Application Insights] [ start] performans veya kullanım ölçümü web uygulamanızda toochanges uyarabilir. 

Application Insights üzerinde Canlı uygulamanızı izler bir [çeşitli platformlar] [ platforms] performans sorunlarını tanılama ve kullanım biçimlerini toohelp.

Uyarılar üç tür vardır:

* **Ölçüm uyarıları** zaman - yanıt süreleri, özel durum sayısı, CPU kullanımı ya da sayfa görünümleri gibi belirli bir süre için bir eşik değeri bir ölçüm kestiği söyleyin. 
* [**Web testleri** ] [ availability] sitenizi hello üzerinde kullanılabilir olduğunda size internet veya yavaş yanıt. [Daha fazla bilgi edinin][availability].
* [**Öngörülü tanılama** ](app-insights-proactive-diagnostics.md) otomatik olarak yapılandırılan toonotify, olağan dışı performans desenleri hakkında.

Biz bu makalede ölçüm uyarıları odaklanılmaktadır.

## <a name="set-a-metric-alert"></a>Ölçüm uyarı ayarlama
Açık hello uyarı kuralları dikey ve kullanım hello düğmesi ekleyin. 

![Merhaba uyarı kuralları dikey penceresinde eklemek uyarı seçin. Uygulamanızın kaynak toomeasure hello olarak ayarlamak, hello uyarı için bir ad ve bir ölçüm seçin.](./media/app-insights-alerts/01-set-metric.png)

* Merhaba kaynak hello önce diğer özellikleri ayarlayın. **Merhaba "(bileşenler)" kaynağı seçin** performans ya da kullanım ölçümleri tooset uyarılar istiyorsanız.
* toohello uyarı vermek hello adı (yalnızca, uygulama) hello kaynak grubunda benzersiz olmalıdır.
* Dikkatli toonote hello birimleri tooenter hello eşik değeri sorulur olabilir.
* "E-posta sahipleri..." Merhaba kutuyu işaretlerseniz, uyarılar erişim toothis kaynak grubuna sahip e-posta tooeveryone tarafından gönderilir. Bu ayarlar kişiler, tooexpand eklemek bunları toohello [kaynak grubuna veya aboneliğe](app-insights-resources-roles-access-control.md) (kaynak hello değil).
* "Ek e-postaları" belirtirseniz, uyarılar toothose kişiler veya gruplar (olsun veya olmasın, hello "sahipleri e-posta..." kutusunu işaretli) gönderilir. 
* Ayarlanmış bir [Web kancası adresi](../monitoring-and-diagnostics/insights-webhooks-alerts.md) tooalerts yanıt veren bir web uygulamasını kurup ayarlarsanız. Merhaba uyarı etkinleştirildiğinde, hem bu çözümlendiğinde denir. (Ancak şu anda sorgu parametreleri Web kancası özellikleri olarak geçirilecek değil olduğunu unutmayın.)
* Devre dışı bırakabilir veya etkinleştir hello Uyarı: hello düğmeleri hello dikey penceresinde hello üstündeki bakın.

*Merhaba Ekle uyarı düğmesini görmek yok.* 

* Bir kurumsal hesap kullanıyor musunuz? Sahibi veya katkıda erişim toothis Uygulama kaynağı varsa, uyarılar ayarlayabilirsiniz. Merhaba erişim denetimi dikey göz atın. [Erişim denetimi hakkında bilgi edinin][roles].

> [!NOTE]
> Merhaba uyarıları dikey penceresinde, zaten var olduğu bir uyarı kümesi bkz: [öngörülü tanılama](app-insights-proactive-failure-diagnostics.md). Merhaba otomatik uyarı bir belirli ölçüm, isteği hata oranı izler. Toodisable hello öngörülü uyarı karar sürece, isteği hata oranı kendi uyarıdaki tooset gerek yoktur. 
> 
> 

## <a name="see-your-alerts"></a>Uyarılarınızı bakın
Bir e-posta uyarı değişiklikleri durum olduğunda, etkin ve etkin arasında alın. 

Her uyarı geçerli durumunu Hello hello uyarı kuralları dikey penceresinde görüntülenir.

Aşağı açılan hello uyarılar son etkinliğin bir özeti verilmiştir:

![Aşağı açılan uyarıları](./media/app-insights-alerts/010-alert-drop.png)

durum değişiklikleri Hello geçmişini hello etkinlik günlüğü şöyledir:

![Merhaba genel bakış dikey penceresinde, ayarlar, Denetim günlükleri'ı tıklatın.](./media/app-insights-alerts/09-alerts.png)

## <a name="how-alerts-work"></a>Uyarılar nasıl çalışır?
* Üç durumlu bir uyarı vardır: "Hiçbir zaman etkinleştirilmiş", "Etkinleştirildi" ve "Çözümlendi." Etkinleştirilen anlamına gelir, son değerlendirildiğinde true, belirtilen koşul hello.
* Bir uyarı durumu değiştiğinde bildirim oluşturulur. (Merhaba uyarı oluşturduğunuzda hello Uyarı koşulu zaten true ise, hello koşul yanlış gider kadar bir bildirim alamayabilirsiniz.)
* Merhaba e-posta kutusunu işaretli veya e-posta adresleri sağlanan her bir bildirim e-posta oluşturur. Merhaba bildirimleri aşağı açılan listesinde de bakabilirsiniz.
* Bir uyarı, bir ölçüm geldiğinde, ancak aksi, her defasında değerlendirilir.
* Merhaba değerlendirme süresi önceki hello hello ölçüm toplar ve toohello eşik toodetermine hello yeni durumu karşılaştırır.
* Seçtiğiniz hello dönemi üzerinde ölçümleri toplanır hello aralığını belirtir. Ne sıklıkta hello uyarı değerlendirilir etkilemez: varış ölçümleri hello sıklığını bağlıdır.
* Hiçbir veri bir süre için belirli bir ölçüm gelirse hello boşluk uyarı değerlendirmesi ve ölçüm Gezgini hello grafiklerde farklı etkilere sahiptir. Hiçbir veri hello grafiğin örnekleme aralığı daha uzun süre görülür, ölçüm Explorer'da hello grafik 0 değerini gösterir. Ancak aynı Ölçüm değil üzerinde hello dayalı bir uyarı olmasını ve hello değişmeden uyarının durumu kalır. 
  
    Veri sonunda ulaştığında hello grafik geri tooa sıfır olmayan bir değer atlar. Merhaba uyarı değerlendirir belirttiğiniz hello dönem için kullanılabilir hello veri göre. Merhaba yeni veri noktası hello yalnızca bir hello dönemde kullanılabilir ise, birleşik hello yalnızca üzerinde veri noktası temel alır.
* Uzun süre ayarlasanız bile bir uyarı uyarı ve sağlam durumları arasında sık Titreşim. Hello eşik Hello ölçüm değeri gezinen bu durum meydana gelebilir. Merhaba eşiği hiçbir hysteresis yoktur: hello geçiş tooalert olur aynı değeri hello geçiş toohealthy hello adresindeki.

## <a name="what-are-good-alerts-tooset"></a>İyi uyarıları tooset nelerdir?
Uygulamanızda bağlıdır. toostart, onu sahip en iyi olmayan tooset çok fazla ölçümleri. Uygulamanızı çalışırken, ölçüm grafiklerinizi arayan biraz zaman ayırın tooget bir kullanım için nasıl normal şekilde davranır. Bu uygulama performansını yolları tooimprove bulmanıza yardımcı olur. Merhaba ölçümleri hello normal bölgesi dışından olduğunuzda uyarıları tootell, ayarlayın. 

Popüler uyarıları şunları içerir:

* [Tarayıcı ölçümleri][client], özellikle tarayıcı **sayfa yükleme süreleri**, web uygulamaları için iyidir. Sayfanız birçok komut dosyaları varsa, göz önünde bulundurmanız gerekenler **tarayıcı özel durumları**. Sipariş tooget bu ölçümleri ve uyarılar, tooset çalışır duruma getirdikten [web sayfası izleme][client].
* **Sunucu yanıt süresi** hello sunucu tarafı web uygulamaları için. Orantısız ile yüksek istek hızları değişiyorsa uyarılarını ayarlama yanı sıra bu ölçüm toosee takip: değişim uygulamanızı kaynakları tükendi çalıştığını gösterebilir. 
* **Sunucu özel durumları** -toosee bunları, sahip olduğunuz toodo bazı [ek kurulum](app-insights-asp-net-exceptions.md).

Unutmayın [öngörülü hata oranı tanılama](app-insights-proactive-failure-diagnostics.md) otomatik olarak, uygulamanızı toorequests hata kodlarıyla yanıt İzleyicisi Merhaba oranı. 

## <a name="automation"></a>Otomasyon
* [Uyarıları Ayarlama PowerShell tooautomate kullanım](app-insights-powershell-alerts.md)
* [Web kancası tooautomate yanıt veren tooalerts kullanın](../monitoring-and-diagnostics/insights-webhooks-alerts.md)

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="see-also"></a>Ayrıca bkz.
* [Kullanılabilirlik web testleri](app-insights-monitor-web-app-availability.md)
* [Uyarıları Ayarlama otomatikleştirme](app-insights-powershell-alerts.md)
* [Öngörülü tanılama](app-insights-proactive-diagnostics.md) 

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[platforms]: app-insights-platforms.md
[roles]: app-insights-resources-roles-access-control.md
[start]: app-insights-overview.md

