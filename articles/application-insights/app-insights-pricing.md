---
title: "Azure Application Insights için aaaManage fiyatlandırma ve veri birimi | Microsoft Docs"
description: "Telemetri birimleri yönetin ve Application Insights maliyetlerini izleyin."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: ebd0d843-4780-4ff3-bc68-932aa44185f6
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: bwren
ms.openlocfilehash: 4621c989cd467735aefc48ec9547fcbe1b1ae41b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-pricing-and-data-volume-in-application-insights"></a>Application Insights fiyatlandırma ve veri biriminde yönetme


Fiyatlandırmasını [Azure Application Insights] [ start] uygulama başına veri hacmi dayanır. Telemetri veri 1 GB aylık indirimi olduğundan düşük kullanımı geliştirme sırasında veya küçük bir uygulama için olası toobe boş değildir.

Her bir Application Insights kaynağı ayrı bir hizmet ücretlendirilir ve abonelik tooAzure toohello fatura katkıda bulunur.

İki fiyatlandırma planı vardır. Merhaba varsayılan planı Basic adı verilir. Günlük bir ücretsiz olarak sahip, ancak bazı ek özellikler gibi etkinleştirir hello Kurumsal planlama, seçebilirsiniz [sürekli verme](app-insights-export-telemetry.md).

Fiyatlandırma için Application Insights nasıl çalıştığı hakkında sorularınız varsa, ücretsiz toopost bir soru eşitleyerek bizim [Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=ApplicationInsights). 

## <a name="hello-price-plans"></a>Merhaba fiyat planları

Merhaba bkz [Application Insights fiyatlandırma sayfası] [ pricing] geçerli fiyatlar para birimi değerlerinizi için.

### <a name="basic-plan"></a>Temel plan

Yeni bir Application Insights kaynak oluşturulduğunda ve çoğu müşteri için yeterli hello temel plan hello varsayılandır.

* Merhaba temel planda veri hacmine göre ücretlendirilen: Application Insights tarafından alınan telemetri bayt sayısı. Veri birimi Application Insights tarafından uygulamanızdan alınan sıkıştırılmamış hello JSON veri paketi hello boyutu olarak ölçülür.
İçin [tablo veri analizi içeri](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-import), hello veri birimi gönderilen dosyaların tooApplication Öngörüler sıkıştırılmamış boyutunu hello olarak ölçülür.  
* Yalnızca denemeler geliştirme veya olası toohave toopay olacak şekilde her uygulama için ilk, 1 GB ücretsizdir.
* [Canlı ölçümleri akış](app-insights-live-stream.md) veri yok sayılan amacıyla fiyatlandırma için.
* [Sürekli verme](app-insights-export-telemetry.md) hello temel planda bir ek GB başına ücret için kullanılabilir.

### <a name="enterprise-plan"></a>Kurumsal plan

* Merhaba Kurumsal planda uygulamanıza Application Insights tüm hello özelliklerini kullanabilirsiniz. [Sürekli verme](app-insights-export-telemetry.md) ve 

[Analytics bağlayıcı oturum](https://go.microsoft.com/fwlink/?LinkId=833039&amp;clcid=0x409) hello Kurumsal planda ek bir ücret kullanılabilir.
* Tüm uygulamalar için telemetri hello Kurumsal planda gönderiyor düğüm başına ücret ödersiniz. 
 * A *düğüm* bir fiziksel veya sanal sunucu makinesi ya da uygulamanızı barındıran bir hizmet olarak Platform rol örneği.
 * Geliştirme makineler, istemci tarayıcıları ve mobil cihazları düğümleri olarak sayılmaz.
 * Uygulamanızı bir web hizmeti ve arka uç çalışan gibi telemetri göndermesine çeşitli bileşenleri varsa bunlar ayrı olarak sayılır.
 * [Canlı ölçümleri akış](app-insights-live-stream.md) veri yok sayılan yaratılır abonelik üzerinden fiyatlandırma için uygulama başına düğüm başına ücretlerinizi. 12 uygulamaları sonra hello beş düğümler için ücret için telemetri göndermesini beş düğümleriniz varsa.
* Aylık ücret tırnak içine rağmen yalnızca içinde ve bir düğüm telemetri bir uygulamadan gönderir her saat için ücret ödersiniz. Merhaba saatlik ücret hello aylık ücret tırnak içine alınmış olan / 744 (Merhaba 31 gün ay saat sayısı).
* 200 MB günde bir veri birimi ayırma (saatlik ayrıntı) algılanan her düğüm için verilir. Kullanılmayan veri ayırma bir gün toohello sonraki devredilir değil.
 * Merhaba Kurumsal fiyatlandırma seçeneği seçerseniz, her abonelik günlük indirimi veri hello telemetri toohello Application Insights kaynaklar bu abonelikte gönderme düğüm sayısını temel alır. Bu nedenle tüm günlük verileri gönderme 5 düğümleriniz varsa, bu abonelikte bir havuza alınmış indirimi uygulanan 1 GB tooall hello Application Insights kaynakların gerekir. Bazı düğümler hello veri içerdiğinden diğer düğümlere daha fazla veri tüm düğümleri arasında paylaşılan gönderiyorsanız önemli değildir. Belirli bir tarihteki hello Application Insights kaynakları Bu abonelik için günlük veri ayırma hello dahil daha fazla veri almaya devam ederseniz, hello GB başına fazla kullanım veri ücretleri uygulanır. 
 * Merhaba günlük veri indirimi saat (UTC kullanarak) hello gün içindeki hello sayısı olarak hesaplanır her düğüm tarafından 24 kez 200 MB bölünmüş telemetri gönderiyor. 24 saat hello gün içinde hello 15 sırasında telemetri göndermesini 4 düğüm varsa, o gün olacak için hello veriler dahil şekilde ((4 x 15) / 24) 200 MB = 500 MB x. Merhaba düğümleri o gün 1 GB veri gönderirseniz hello fiyattan GB başına 2.30 ABD Doları, veri fazlalık için 1,15 ABD Doları hello ücret olacaktır.
 * Merhaba Kurumsal planın günlük indirimi hello temel seçeneği seçtiğiniz uygulamalarla paylaşılmayan not alın ve kullanılmayan indirimi gelen günlük devredilir değil. 
* Ayrı düğüm sayısını belirlemek bazı örnekler şunlardır:
| Senaryo                               | Günlük toplam düğüm sayısı |
|:---------------------------------------|:----------------:|
| 1 uygulama 3 Azure uygulama hizmeti örnekleri ve 1 sanal sunucu kullanma | 4 |
| Bu uygulamalar içindeki aynı abonelik hello ve hello Kurumsal plan için 2 VM ve hello Application Insights kaynaklar üzerinde çalışan 3 uygulamalar | 2 | 
| Uygulamaları Öngörüler kaynakları bulunan 4 uygulamaları aynı abonelik hello. Her uygulama 16 saatlerde 2 örnekleri ve 4 örnekleri 8 yoğun saatlerde çalışır. | 13.33 | 
| 1 çalışan rolü ve her 2 örneklerini çalıştıran 1 Web rolü ile birlikte bulut Hizmetleri | 4 | 
| 3 örneği çalıştıran her mikro hizmet 50 mikro services çalıştıran 5-node Service Fabric kümesi | 5|

* Application Insights SDK'sı, uygulamanızın kullandığı Hello kesin düğümü sayım davranışı bağlıdır. 
  * SDK sürümlerinde 2.2 ve sonraki sürümlerde, her ikisi de Application Insights hello [Core SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights/) veya [Web SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) her uygulama ana bilgisayarı bir düğüm olarak rapor, örneğin fiziksel sunucu ve VM konakları veya hello için bilgisayar adı hello Bulut Hizmetleri hello durumda örnek adı.  özel durum uygulamaları kullanarak yalnızca yalnızca hello [.NET Core](https://dotnet.github.io/) ve Merhaba, servis talebi yalnızca bir düğüm bildirilir tüm ana bilgisayarlar için hello ana bilgisayar adı kullanılamadığı için Application Insights çekirdek SDK. 
  * Merhaba SDK önceki sürümlerde hello [Web SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) yalnızca hello yeni SDK sürümleri, ancak hello gibi davranır [Core SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights/) gerçek uygulama ana bilgisayar hello sayısı bağımsız olarak yalnızca tek bir düğüme rapor eder. 
  * Uygulamanızı hello SDK tooset roleInstance tooa özel değer kullanıyorsanız, varsayılan olarak aynı değeri olacağını unutmayın kullanılan düğümlerinin toodetermine hello sayısı. 
  * İstemci makineler veya mobil cihazlardan çalışan bir uygulama ile yeni bir SDK sürümünü kullanıyorsanız, düğümleri hello sayısı (Merhaba çok sayıda istemci makineleri veya mobil cihazlar) çok büyük bir sayı döndürebilir mümkündür. 

### <a name="multi-step-web-tests"></a>Çok adımlı web testleri

İçin ek bir ücret yoktur [çok adımlı web testleri](app-insights-monitor-web-app-availability.md#multi-step-web-tests). Bu, bir dizi eylemi gerçekleştirmek tooweb testleri ifade eder. 

Tek bir sayfayla 'ping sınaması' için ayrı bir ücret ödemeden yoktur. Diğer telemetriyi uygulamanızdan birlikte ping testleri ve çok adımlı testleri telemetrisinden ücretlendirilir.
 
## <a name="operations-management-suite-subscription-entitlement"></a>Operations Management Suite aboneliği yetkilendirme

Olarak [son duyurdu](https://blogs.technet.microsoft.com/msoms/2017/05/19/azure-application-insights-enterprise-as-part-of-operations-management-suite-subscription/), Microsoft Operations Management Suite E1 ve E2 satın müşterilerdir mümkün tooget uygulama Öngörüler Kurumsal hiçbir ek ücret ödemeden ek bileşen olarak. Özellikle, Operations Management Suite E1 ve E2 her birimi hello Kurumsal planı Application Insights yetkilendirme too1 düğümü içerir. Yukarıda belirtildiği gibi her Application Insights düğüm too200 MB günde (ayrı), günlük analizi veri alımı hiçbir ek ücret ödemeden 90 günlük veri saklama ile alınan veri yukarı içerir. 

> [!NOTE]
> Bu yetkilendirme almak tooensure planı fiyatlandırma Application Insights kaynaklarınızı hello Kurumsal olması gerekir. Application Insights kaynakları hello temel planda bir fayda fark olmayan şekilde bu yetkilendirme yalnızca düğümleri olarak uygulanır. Bu yetkilendirme hello özellikleri gösterilen maliyetleri tahmin + dikey fiyatlandırma hello üzerinde görünür olmaz unutmayın. 
>
 
## <a name="review-pricing-plans-and-estimate-costs"></a>Fiyatlandırma planlarını gözden geçirin ve maliyetleri tahmin etme

Applicaition Öngörüler kolay toounderstand hello fiyatlandırma planlarında kullanılabilir ve maliyetleri olasılıkla olan hangi hello son kullanım desenlerini üzerinde temel alabilir kolaylaştırır. Başlangıç açma hello tarafından **özellikleri + fiyatlandırma** dikey penceresinde hello hello Azure portalında Application Insights kaynağını:

![Fiyatlandırma seçin.](./media/app-insights-pricing/01-pricing.png)

**a.** Veri biriminiz hello ay için gözden geçirin. Bu, alınan ve korunan tüm hello verilerini içerir (herhangi sonra [örnekleme](app-insights-sampling.md) sunucu ve istemci uygulamalarını ve kullanılabilirlik testleri.

**b.** Ayrı bir ücret yapılan [çok adımlı web testleri](app-insights-monitor-web-app-availability.md#multi-step-web-tests). (Bu hello veri birimi sorumlu dahil basit kullanılabilirlik testleri içermez.)

**c.** Merhaba Kurumsal planı etkinleştirin.

**d.** Toodata yönetim seçenekleri tooview veri birimi hello geçen ay için aracılığıyla'ı tıklatın, bir günlük sınır ayarlayın veya alım örnekleme ayarlayın.

Uygulama Öngörüler ücretleri tooyour Azure faturasını eklenir. Azure hello faturalama bölüm hello Azure portal veya hello fatura ayrıntılarını görebilirsiniz [Azure Billing Portal](https://account.windowsazure.com/Subscriptions). 

![Merhaba yan menüsünde faturalama seçin.](./media/app-insights-pricing/02-billing.png)

## <a name="data-rate"></a>Veri oranı
Hangi hello veri Gönder birim sınırlıdır üç yolu vardır:

* **Örnekleme:** bu düzenek kullanılabilir sunucu ve istemci uygulamalarınızı en az bozulma ölçümleri ile gönderilen telemetri hello miktarını azaltın. Bu tootune hello veri miktarına sahip hello birincil araçtır. Daha fazla bilgi edinmek [özellikleri örnekleme](app-insights-sampling.md). 
* **Günlük sınır:** hello Azure portal ' Bu Application Insights kaynağı oluşturma ayarlandığında too500 GB/gün. Visual Studio Application Insights kaynağı oluştururken, varsayılan Merhaba, olan olan küçük (yalnızca 32.3 MB/gün) hedeflenen yalnızca toofaciliate test etme. Bu durumda bu hello kullanıcı hello uygulama üretim ortamına dağıtmadan önce hello günlük sınır oluşturacak yöneliktir. bir yüksek trafik uygulama için daha yüksek bir maksimum istediniz sürece hello üst sınır uygulanıyor 500 GB/gün olur. Maksadınızı olması gerektiği gibi hello günlük cap ayarlarken dikkatli **hiçbir zaman toohit hello günlük cap**, çünkü daha sonra hello gün hello kalanı için veri kaybı ve oluşturamıyor toomonitor uygulamanız olabilir. toochange, kullanım hello günlük birimi cap dikey penceresinde hello veri birimi yönetim dikey penceresinden (aşağıya bakın) bağlı. Bazı abonelik türleri için Application Insights kullanılan kredi gerektiğini unutmayın. Merhaba abonelik bir sınırlamak, her gün hello harcama varsa cap dikey yönergeleri nasıl olacaktır ve etkinleştir hello 32.3 MB/gün dışında gerçekleştirilen günlük cap toobe tooremove.  
* **Azaltma:** bu sınırları hello veri oranı too32 k olayları saniyede 1 dakika içinde ortalanır. 


*Uygulamam hızı azaltma hello aşarsa ne olur?*

* Uygulamanızı dakikada uygunluk gönderir veri hacmi Hello. Merhaba dakika içinde ölçülen ortalama hello saniyede oranı aşarsa, hello sunucu bazı istekleri reddeder. Merhaba SDK hello veri arabelleğe alır ve birkaç dakika boyunca bir dalgalanma yaymak tooresend çalışır. Uygulamanızı sürekli veri hızı azaltma hello yukarıda gönderirse, bazı verisi bırakılacak. (Bu şekilde tooresend hello ASP.NET, Java ve JavaScript SDK'ları deneyin; diğer SDK yalnızca kısıtlanan açılan veri olabilir.) Azaltma meydana gelirse, bu gerçekleştirilmedi uyarı bir bildirim görürsünüz.

*Uygulamam gönderme ne kadar verinin nasıl biliyor musunuz?*

* Açık hello **veri birimi Yönetimi** dikey toosee hello günlük veri birimi grafik. 
* Ölçümleri Gezgini'nde, yeni bir grafik ekleyin veya seçin **veri noktası birimi** kendi ölçüm olarak. Gruplandırılması geçin ve group by **veri türü**.

## <a name="tooreduce-your-data-rate"></a>tooreduce veri oranı
Veri biriminiz tooreduce yapabileceğiniz bazı şeyleri şunlardır:

* Kullanım [örnekleme](app-insights-sampling.md). Bu teknoloji, ölçümlerinizi eğriltme ve arama ilgili öğeler arasındaki hello özelliği toonavigate kesintiye olmadan veri oranı azaltır. Sunucu uygulamaları otomatik olarak çalışır.
* [Bildirilebilir Ajax çağrıları hello sayısını sınırlandır](app-insights-javascript.md#detailed-configuration) her sayfa görünümü veya Ajax Raporlama Kapalı anahtarı.
* Koleksiyon modülleri tarafından gerekmez kapalı geçiş [Applicationınsights.config düzenleme](app-insights-configuration-with-applicationinsights-config.md). Örneğin, performans sayaçlarını veya bağımlılık veri inessential karar verebilirsiniz.
* Telemetri tooseparate araçları anahtarlarınızı bölün. 
* Önceden toplama ölçümleri. Uygulamanızda çağrıları tooTrackMetric yerleştirirseniz hello ortalama, hesaplama ve ölçümleri toplu standart sapmasını kabul hello aşırı kullanarak trafiğini azaltabilir. Veya, kullanabileceğiniz bir [önceden toplama paketi](https://www.myget.org/gallery/applicationinsights-sdk-labs).

## <a name="managing-hello-maximum-daily-data-volume"></a>Merhaba maksimum günlük veri birimi yönetme

Toplanan hello günlük birimi cap toolimit hello veri kullanabilirsiniz, ancak hello cap karşılanırsa uygulamanızdan hello günün hello kalanı için gönderilen tüm telemetery kaybıyla sonuçlanır. Bu **değil önerilir** toohave uygulama, toohit hello günlük sınır, bu yana olan oluşturulamıyor tootrack hello sağlık ve performans, uygulamanızın, isabet sonra. 

Bunun yerine, kullanın [örnekleme](app-insights-sampling.md) gibi ve uygulamanızı telemetery kadar yüksek hacimli beklenmedik bir şekilde göndermeye başlar durumunda "son çare olarak" Merhaba günlük cap kullanmak tootune hello veri birimi toohello düzeyi. 

toochange hello günlük kapasite, hello uygulama Insihgts kaynağınız yapılandırma bölümünü tıklatın **veri birimi Yönetimi** sonra **günlük Cap**.

![Merhaba günlük telemetri birim ucu ayarlama](./media/app-insights-pricing/daily-cap.png) 

## <a name="sampling"></a>Örnekleme
[Örnekleme](app-insights-sampling.md) telemetri gönderilme tooyour uygulama hala hello özelliği toofind korunuyor olayları sırasında tanılama aramaları ilişkili bir hello hızının düşürülmesi, yöntemidir ve hala tutma doğru olay sayar. 

Örnekleme tooreduce ücretler ve aylık kotanızı içinde kalmasını etkili bir yoldur. Örneğin, arama kullandığınızda, bulabilmesi için hello örnekleme algoritması telemetri, ilgili öğeler korur hello isteği ilgili tooa belirli özel durum. Merhaba doğru değerleri ölçüm Explorer'da istek hızları, özel durum hızları ve diğer sayılar görebilmesi için hello algoritması doğru sayıları de korur.

Örnekleme çeşitli biçimlerde vardır.

* [Uyarlamalı örnekleme](app-insights-sampling.md) hello uygulamanızı gönderdiği telemetri toohello hacmi otomatik olarak ayarlar ASP.NET SDK için hello varsayılandır. Böylece hello ağda Hello telemetri trafiği azaltılır hello SDK web uygulamanızda içinde otomatik olarak çalışır. 
* *Alım örnekleme* burada uygulamanızdan telemetrinin girer hello Application Insights hizmeti hello noktada çalışır alternatiftir. Merhaba telemetriyi uygulamanızdan gönderilen hacmi etkilemez, ancak hello hizmeti tarafından korunduğunu hello birim azaltır. Tarayıcılar ve diğer SDK telemetri tarafından kullanılan tooreduce hello kota kullanabilirsiniz.

örnekleme, tooset alım hello fiyatlandırma dikey penceresinde hello denetim ayarlayın:

![Merhaba kota ve dikey fiyatlandırma, hello örnekleri kutucuğa tıklayın ve örnekleme kesir seçin.](./media/app-insights-pricing/04.png)

> [!WARNING]
> Merhaba veri örnekleme dikey yalnızca alım örnekleme hello değerini denetler. Uygulamanızda hello Application Insights SDK'sı tarafından uygulanan hello örnekleme hızını yansıtmaz. Merhaba gelen telemetri SDK hello örneklenen alım örnekleme uygulanmaz.
> 

Burada uygulandığından, olsun oranı örnekleme toodiscover hello gerçek kullanmak bir [Analytics sorgu](app-insights-analytics.md) bu gibi:

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

Her kaydı tutulur `itemCount` temsil eder, özgün kayıt eşit too1 + hello kayıt sayısı, önceki atılan hello sayısını gösterir. 


## <a name="automation"></a>Otomasyon

Azure kaynak Yönetimi'ni kullanarak bir komut dosyası tooset hello fiyat planı yazabilirsiniz. [Bilgi nasıl](app-insights-powershell.md#price).

## <a name="limits-summary"></a>Sınırları özeti
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

## <a name="next-steps"></a>Sonraki adımlar

* [Örnekleme](app-insights-sampling.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiproperties]: app-insights-api-custom-events-metrics.md#properties
[start]: app-insights-overview.md
[pricing]: http://azure.microsoft.com/pricing/details/application-insights/

