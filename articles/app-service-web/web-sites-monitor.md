---
title: Azure uygulama hizmetinde uygulamalar aaaMonitor | Microsoft Docs
description: "Azure Portal kullanarak Azure App Service'te toomonitor uygulamalarını nasıl hello öğrenin."
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: d273da4e-07de-48e0-b99d-4020d84a425e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: byvinyal
ms.openlocfilehash: 80d5a466102a894a49d04ae35aa54cc1d05a58df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a>Nasıl yapılır: Azure uygulama hizmetinde uygulamaları izleme
[Uygulama hizmeti](http://go.microsoft.com/fwlink/?LinkId=529714) hello yerleşik izleme işlevselliği sağlayan [Azure Portal](https://portal.azure.com).
Bu hello özelliği tooreview içerir **kotaları** ve **ölçümleri** hello ayarlama uygulama hizmeti planı yanı sıra bir uygulama için **uyarıları** ve hatta **ölçeklendirme** bu ölçümleri göre otomatik olarak.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a>Anlama kotalar ve ölçümleri
### <a name="quotas"></a>Kotalar
App Service içinde barındırılan konu toocertain uygulamalardır *sınırları* kullanabilecekleri kaynaklar. Merhaba sınırları hello tarafından tanımlanan **uygulama hizmeti planı** hello uygulamayla ilişkili.

Merhaba uygulaması barındırılıyorsa bir **serbest** veya **paylaşılan** planlama hello uygulama kullanabileceğiniz hello kaynaklardaki hello sınırları tarafından tanımlanan sonra **kotaları**.

Merhaba uygulaması barındırılıyorsa bir **temel**, **standart** veya **Premium** planlama hello sınırları kullanabilecekleri hello kaynaklar tarafından hello ayarlayın, sonra da **boyutu** (Küçük, Orta, büyük) ve **örnek sayısını** (1, 2, 3,...) Merhaba, **uygulama hizmeti planı**.

**Kotalar** için **serbest** veya **paylaşılan** uygulamalar şunlardır:

* **CPU(short)**
  * Bu uygulamada 5 dakikalık bir zaman aralığı için izin verilen CPU miktarı. Bu kota her 5 dakikada bir yeniden ayarlar.
* **CPU(Day)**
  * CPU bir gün içinde bu uygulama için izin verilen toplam miktarı. Bu kota UTC gece 24 saatte yeniden ayarlar.
* **Bellek**
  * Bu uygulama için izin verilen bellek toplam miktarı.
* **Bant genişliği**
  * Giden bant genişliği bir gün içinde bu uygulama için izin verilen toplam miktarı.
    Bu kota UTC gece 24 saatte yeniden ayarlar.
* **Dosya sistemi**
  * İzin verilen depolama alanı toplam miktarı.

barındırılan yalnızca kota geçerli tooapps hello **temel**, **standart** ve **Premium** planları olan **dosya sistemi**.

Merhaba belirli kotalar, sınırları ve farklı uygulama hizmeti SKU'ları hello kullanılabilir özellikler hakkında daha fazla bilgi şurada bulunabilir: [Azure aboneliği hizmet sınırları](../azure-subscription-service-limits.md#app-service-limits)

#### <a name="quota-enforcement"></a>Kota zorlama
Kullanım uygulamada hello aşarsa **CPU (kısa)**, **CPU (gün)**, veya **bant genişliği** hello kota yeniden getirilene kadar kota sonra hello uygulama durdurulacak. Tüm gelen istekleri sonuçlanır bu süre boyunca bir **HTTP 403**.
![][http403]

Varsa hello uygulama **bellek** kota aşıldı sonra hello uygulama yeniden başlatılmasından olacaktır.

Merhaba, **Filesystem** kota aşıldı sonra herhangi bir yazma işlemi başarısız olur, bu toologs yazma içerir.

Kotalar artırılabilir veya uygulama hizmeti planınızı yükselterek uygulamanızdan kaldırıldı.

### <a name="metrics"></a>Ölçümler
**Ölçümleri** hello uygulama ya da uygulama hizmeti planının davranışı hakkında bilgi sağlar.

İçin bir **uygulama**, hello kullanılabilir ölçümler şunlardır:

* **Ortalama yanıt süresi**
  * MS hello uygulama tooserve istekleri için geçen ortalama süre hello.
* **Ortalama bellek çalışma kümesi**
  * Merhaba ortalama MIB hello uygulama tarafından kullanılan bellek miktarı.
* **CPU süresi**
  * CPU miktarını Hello hello uygulama tarafından kullanılan saniye cinsinden. Bu ölçüm bakın hakkında daha fazla bilgi için: [CPU zamanı vs CPU yüzdesi](#cpu-time-vs-cpu-percentage)
* **Verileri**
  * Merhaba hello uygulamada MIB tarafından tüketilen gelen bant genişliği miktarı.
* **Giden veriler**
  * Merhaba hello uygulamada MIB tarafından tüketilen giden bant genişliği miktarı.
* **HTTP 2xx**
  * Bir http durum kodunu kaynaklanan isteklerin sayısı > = 200 ancak < 300.
* **HTTP 3xx**
  * Bir http durum kodunu kaynaklanan isteklerin sayısı > = 300 ancak < 400.
* **HTTP 401**
  * HTTP 401 durum kodunu kaynaklanan isteklerin sayısı.
* **HTTP 403**
  * HTTP 403 durum kodunu kaynaklanan isteklerin sayısı.
* **HTTP 404**
  * HTTP 404 durum kodunu kaynaklanan isteklerin sayısı.
* **HTTP 406**
  * HTTP 406 durum kodunu kaynaklanan isteklerin sayısı.
* **HTTP 4xx**
  * Bir http durum kodunu kaynaklanan isteklerin sayısı > = 400 ancak < 500.
* **HTTP sunucu hataları**
  * Bir http durum kodunu kaynaklanan isteklerin sayısı > = 500 ancak < 600.
* **Bellek çalışma kümesi**
  * Geçerli hello uygulamada MIB tarafından kullanılan bellek miktarı.
* **İstekleri**
  * Sonuçta elde edilen HTTP durum kodunu ne olursa olsun istekleri toplam sayısı.

İçin bir **uygulama hizmeti planı**, hello kullanılabilir ölçümler şunlardır:

> [!NOTE]
> Uygulama hizmeti planı ölçümleri planları için kullanılabilir yalnızca **temel**, **standart** ve **Premium** SKU.
> 
> 

* **CPU yüzdesi**
  * Merhaba ortalama CPU hello planının tüm örneklerinde kullanılır.
* **Bellek yüzdesi**
  * Merhaba ortalama bellek hello planının tüm örneklerinde kullanılır.
* **Verileri**
  * Merhaba planının tüm örneklerinde kullanılan hello ortalama gelen bant genişliği.
* **Giden veriler**
  * Merhaba ortalama hello planının tüm örneklerinde kullanılan bant genişliği giden.
* **Disk Sırası Uzunluğu**
  * Merhaba ortalama sayısı okuma ve yazma depolama üzerinde sıraya alınan istekleri. Yüksek disk sırası uzunluğu tooexcessive disk g/ç yavaşlamadan bir uygulamanın göstergesidir.
* **HTTP sırası uzunluğu**
  * Merhaba ortalama yerine getirilmesini önce toosit hello sırasına olan HTTP isteği sayısı. Yüksek veya artan HTTP sırası uzunluğu, yoğun yük altında bir planı belirtisidir.

### <a name="cpu-time-vs-cpu-percentage"></a>CPU zamanı vs CPU yüzdesi
<!-- toodo: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

CPU kullanımı yansıtacak 2 ölçümleri vardır. **CPU süresi** ve **CPU yüzdesi**

**CPU süresi** barındırılan uygulamalar için yararlıdır **serbest** veya **paylaşılan** kendi kotaları birini hello uygulama tarafından kullanılan CPU dakika cinsinden tanımlanır beri planları.

**CPU yüzdesi** hello üzerinde barındırılan uygulamalar için diğer yandan yararlıdır **temel**, **standart** ve **premium** dışa Genişletilebilir beri planları ve bu ölçüm Merhaba iyi bir göstergesidir tüm örneklerde genel kullanım.

## <a name="metrics-granularity-and-retention-policy"></a>Ölçümleri ayrıntı düzeyi ve bekletme ilkesi
Bir uygulama ve uygulama hizmeti planı ölçümleri oturum ve hello ile Merhaba hizmet tarafından toplanan ayrıntı düzeyi ve bekletme ilkeleri aşağıdaki:

* **Dakika** ayrıntı düzeyi ölçümleri için korunur **48 saat**
* **Saat** ayrıntı düzeyi ölçümleri için korunur **30 gün**
* **Gün** ayrıntı düzeyi ölçümleri için korunur **90 gün**

## <a name="monitoring-quotas-and-metrics-in-hello-azure-portal"></a>Kotalar ve ölçümleri hello Azure Portal izleme.
Merhaba farklı hello durumunu gözden geçirebilirsiniz **kotaları** ve **ölçümleri** hello uygulamada etkileyen [Azure Portal](https://portal.azure.com).

![][quotas]
**Kotalar** ayarlar altında bulunabilir >**kotaları**. Merhaba UX gözden geçirmenizi sağlar: (1) hello kotaları adı, (2), sıfırlama aralığı, (3), geçerli sınırı ve (4) geçerli değeri.

![][metrics]
**Ölçümleri** hello kaynak dikey penceresinden doğrudan erişim olabilir. Merhaba grafik tarafından da özelleştirebilirsiniz: (1) **tıklatın** ve seçin (2) üzerinde **grafiği Düzenle**.
Buradan hello (3) değiştirebilirsiniz **zaman aralığı**, (4) **grafik türü**ve (5) **ölçümleri** toodisplay.  

Burada ölçümler hakkında daha fazla bilgi edinebilirsiniz: [izleme hizmeti ölçümleri](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).

## <a name="alerts-and-autoscale"></a>Uyarılar ve otomatik ölçeklendirme
Bir uygulama veya uygulama hizmeti planı tooalerts, toolearn bunu hakkında daha fazla yukarı bağlanabilir için ölçümlerini görmek [uyarı bildirimleri alma](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

Basic barındırılan uygulama hizmeti uygulamalar standart veya premium App Service planları Destek **otomatik ölçeklendirme**. Merhaba uygulaması atlayarak sağlama olduğunda bu uygulama hizmeti planı ölçümleri izleyin ve artırabilir veya gerektiği gibi ek kaynaklar sağlayarak hello örnek sayısı azaltabilirsiniz tooconfigure kuralları veya kaydetme para sağlar. Otomatik ölçek burada hakkında daha fazla bilgi edinebilirsiniz: [nasıl tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) ve burada [Azure İzleyici otomatik ölçeklendirmeyi yönelik en iyi uygulamalar](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
