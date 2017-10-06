---
title: "aaaAutoscaling ve uygulama hizmeti ortamı v1"
description: "Otomatik ölçeklendirme ve uygulama hizmeti ortamı"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: c23af2d8-d370-4b1f-9b3e-8782321ddccb
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 1a03cf494309e80596b64471d1a067b2f64a9fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a>Otomatik ölçeklendirme ve uygulama hizmeti ortamı v1

> [!NOTE]
> Uygulama hizmeti ortamı v1 hello hakkında makaledir.  Merhaba, daha kolay toouse ve daha güçlü altyapısı üzerinde çalışan uygulama hizmeti ortamı'nın daha yeni bir sürümü var. Merhaba yeni sürümü hakkında daha fazla ile Merhaba Başlat toolearn [giriş toohello uygulama hizmeti ortamı](../app-service/app-service-environment/intro.md).
> 

Azure uygulama hizmeti ortamları desteği *otomatik ölçeklendirmeyi*. Ölçümleri veya zamanlamaya göre otomatik ölçeklendirme ayrı ayrı çalışan havuzlarını kullanabilirsiniz.

![Bir çalışan havuzu için otomatik ölçeklendirme seçenekleri.][intro]

Otomatik ölçeklendirmeyi kaynak kullanımını otomatik olarak büyüyen ve bir uygulama hizmeti ortamı toofit küçültme bütçe ve/veya yük profilinizi en iyi duruma getirir.

## <a name="configure-worker-pool-autoscale"></a>Çalışan havuzu otomatik ölçeklendirme yapılandırın
Merhaba otomatik ölçeklendirme işlevleri hello erişebilirsiniz **ayarları** hello çalışan havuzunda sekmesinde.

![Ayarlar sekmesinde hello çalışan havuzu.][settings-scale]

Buradan, hello arabirimi olmalıdır ne zaman bir uygulama hizmeti ölçeklendirmek gördüğünüz aynı deneyimi planlama hello bu yana oldukça alışkın olduğu. 

![El ile ölçek ayarları.][scale-manual]

Bir otomatik ölçeklendirme profili de yapılandırabilirsiniz.

![Otomatik ölçeklendirme ayarları.][scale-profile]

Otomatik ölçeklendirme profili, ölçekte yararlı tooset kısıtlamalardır. Bu şekilde, bir alt sınır ölçek değeri (1) ve tahmin edilebilir harcama cap bir üst sınır (2) ayarlayarak ayarlayarak deneyimi tutarlı bir performans olabilir.

![Ölçek ayarları profilinde.][scale-profile2]

Bir profili tanımladıktan sonra otomatik ölçeklendirme kurallarını tooscale yukarı veya aşağı hello sayısının hello çalışan havuzunda hello profiliyle tanımlanan hello sınırları içinde ekleyebilirsiniz. Otomatik ölçeklendirme kurallarını ölçümleri temel alır.

![Ölçek kuralı.][scale-rule]

 Herhangi bir çalışan havuzu veya ön uç ölçümleri kullanılan toodefine otomatik ölçeklendirme kurallarını olabilir. Bu ölçümler aynı ölçümleri hello kaynak dikey grafiklerde izlemek veya ayarlamak için uyarıları hello ' dir.

## <a name="autoscale-example"></a>Otomatik ölçeklendirme örneği
Otomatik ölçeklendirme bir uygulama hizmeti ortamında en iyi bir senaryo adım adım ilerlemenizi sağlayarak gösterilebilir.

Otomatik ölçeklendirme ayarladığınızda, bu makalede tüm hello gerekli konuları açıklanmaktadır. Merhaba makale, uygulama hizmeti ortamı'nda barındırılan uygulama hizmeti ortamları otomatik ölçeklendirmeyi içinde faktörü olduğunda içine gelen etkileşimleri yürütmek hello açıklanmaktadır.

### <a name="scenario-introduction"></a>Senaryo giriş
Frank kendisinin tooan uygulama hizmeti ortamı yönetir hello iş yükleri bir kısmı geçirildiğini bir kuruluş için bir sysadmin ' dir.

Merhaba uygulama hizmeti ortamı toomanual ölçek aşağıdaki gibi yapılandırılmış:

* **Ön Uçları:** 3
* **Çalışan havuzunda 1**: 10
* **Çalışan havuzunda 2**: 5
* **Çalışan havuzunda 3**: 5

Çalışan havuzunda 2 ve 3 çalışan havuzunda kalite güvence (QA) ve geliştirme iş yükleri için kullanılan sırasında çalışan havuzu 1 üretim iş yükleri için kullanılır.

QA ve geliştirme için hello App Service planlarına toomanual ölçek yapılandırıldı. Merhaba üretim uygulama hizmeti planı yükünü ve trafik tooautoscale toodeal Çeşitlemeler ile ayarlanır.

Frank hello uygulamayla bilgili ' dir. Ki bu çalışanların hello ofiste oldukları sırada kullanan bir satır iş kolu (LOB) uygulaması olduğundan hello yoğun saatler yük 9: 00'da ve 6:00 arasında olduğunu bilir. Kullanıcılar o gün için bittiğinde kullanım bundan sonra bırakır. Yoğun saatler dışında yoktur hala bazı yük kullanıcılar hello uygulama uzaktan kendi mobil aygıtlar veya ev bilgisayarları kullanarak erişebildiğinden. Uygulama hizmeti planı zaten hello üretim kuralları aşağıdaki hello ile CPU kullanımı dikkate alarak tooautoscale yapılandırılmış:

![LOB uygulaması için özel ayarlar.][asp-scale]

| **Otomatik ölçeklendirme profili – haftanın günlerini – uygulama hizmeti planı** | **Otomatik ölçeklendirme profili – hafta sonları – uygulama hizmeti planı** |
| --- | --- |
| **Ad:** haftanın günü profili |**Ad:** hafta sonu profili |
| **Ölçek tarafından:** zamanlama ve performans kuralları |**Ölçek tarafından:** zamanlama ve performans kuralları |
| **Profil:** haftanın günü |**Profil:** hafta sonu |
| **Tür:** yineleme |**Tür:** yineleme |
| **Hedef aralık:** 5 too20 örnekleri |**Hedef aralık:** 3 too10 örnekleri |
| **Gün sayısı:** Pazartesi, Salı, Çarşamba, Perşembe, Cuma |**Gün sayısı:** Cumartesi, Pazar |
| **Başlangıç zamanı:** 09:00:00 |**Başlangıç zamanı:** 09:00:00 |
| **Saat dilimi:** UTC-08 |**Saat dilimi:** UTC-08 |
|  | |
| **Otomatik ölçeklendirme kuralı (ölçeklendirme)** |**Otomatik ölçeklendirme kuralı (ölçeklendirme)** |
| **Kaynak:** üretim (uygulama hizmeti ortamı) |**Kaynak:** üretim (uygulama hizmeti ortamı) |
| **Ölçüm:** CPU % |**Ölçüm:** CPU % |
| **İşlem:** % 60 daha büyük |**İşlem:** % 80 daha büyük |
| **Süresi:** 5 dakika |**Süresi:** 10 dakika |
| **Zaman toplama:** ortalama |**Zaman toplama:** ortalama |
| **Eylem:** sayısı 2 ile artırın |**Eylem:** sayısı 1 ile artırın |
| **(Dakika) basılı güzel:** 15 |**(Dakika) basılı güzel:** 20 |
|  | |
| **Otomatik ölçeklendirme kural (Ölçek aşağı)** |**Otomatik ölçeklendirme kural (Ölçek aşağı)** |
| **Kaynak:** üretim (uygulama hizmeti ortamı) |**Kaynak:** üretim (uygulama hizmeti ortamı) |
| **Ölçüm:** CPU % |**Ölçüm:** CPU % |
| **İşlem:** % 30'den az |**İşlem:** % 20'den az |
| **Süresi:** 10 dakika |**Süresi:** 15 dakika |
| **Zaman toplama:** ortalama |**Zaman toplama:** ortalama |
| **Eylem:** sayısı 1 ile azaltma |**Eylem:** sayısı 1 ile azaltma |
| **(Dakika) basılı güzel:** 20 |**(Dakika) basılı güzel:** 10 |

### <a name="app-service-plan-inflation-rate"></a>Uygulama hizmeti plan Enflasyon oranı
Saat başına en yüksek bir hızda yapılandırılmış tooautoscale olan uygulama hizmeti planları bunu yapar. Bu oran tabanlı hello otomatik ölçeklendirme kuralı sağlanan hello değerlere hesaplanabilir.

Anlama ve hesaplama hello *uygulama hizmeti plan Enflasyon oranı* ölçek değişiklikleri tooa çalışan havuzu olmadığından anlık uygulama hizmeti ortamı ölçeklendirme için önemlidir.

Uygulama hizmeti plan Enflasyon oranı Hello aşağıdaki gibi hesaplanır:

![Uygulama hizmeti planı Enflasyon oranı hesaplama.][ASP-Inflation]

Merhaba otomatik ölçeklendirme – ölçeği Artır kural hello haftanın günü profili hello üretim uygulama hizmeti planı için temel:

![Otomatik ölçeklendirme üzerinde – ölçeği Artır kural tabanlı haftanın günü için uygulama hizmeti planı Enflasyon oranı.][Equation1]

Hello otomatik ölçeklendirme – ölçeği Artır hello hafta sonu profili hello üretim uygulama hizmeti planı için kuralı hello durumda hello formülü çözümlenmesi:

![Otomatik ölçeklendirme üzerinde – ölçeği Artır kural tabanlı hafta sonları için uygulama hizmeti planı Enflasyon oranı.][Equation2]

Bu değer de ölçek azaltma işlemleri için hesaplanabilir.

Merhaba otomatik ölçeklendirme – ölçek aşağı hello haftanın günü profili hello üretim uygulama hizmeti planı için kuralı göre bunu şu şekilde görünür:

![Otomatik ölçeklendirme üzerinde – ölçek aşağı kural tabanlı haftanın günü için uygulama hizmeti planı Enflasyon oranı.][Equation3]

Hello otomatik ölçeklendirme – ölçek aşağı hello hafta sonu profili hello üretim uygulama hizmeti planı için kuralı hello durumda hello formülü çözümlenmesi:  

![Otomatik ölçeklendirme üzerinde – ölçek aşağı kural tabanlı hafta sonları için uygulama hizmeti planı Enflasyon oranı.][Equation4]

Merhaba üretim uygulama hizmeti planı, maksimum oran hello hafta sırasında sekiz örnekleri/saat ve dört örnekleri/saat hello hafta boyunca büyüyebilir. En fazla dört örnekleri/saat hello hafta sırasında örnekleri ve hafta sonları sırasında altı örnekleri saate serbest bırakabilirsiniz.

Çalışan havuzunda birden çok uygulama hizmeti planları barındırılan toocalculate hello varsa *toplam Enflasyon oranı* hello toplam uygulama hizmeti planları yükleniyor tüm hello hello Enflasyon oranındaki olarak, bir çalışan havuzunda barındırma.

![Çalışan havuzunda barındırılan birden çok uygulama hizmeti planları için toplam Enflasyon oran hesaplaması.][ASP-Total-Inflation]

### <a name="use-hello-app-service-plan-inflation-rate-toodefine-worker-pool-autoscale-rules"></a>Kullanım hello uygulama hizmeti planı Enflasyon oranı toodefine çalışan havuzu otomatik ölçeklendirme kuralları
Çalışan barındıran yapılandırılmış tooautoscale olan uygulama hizmeti planları kapasitesinin bir arabellek ayrılması gereken havuza alır. Merhaba arabellek gerektiği gibi uygulama hizmeti planı küçültmek ve hello otomatik ölçeklendirme işlemleri toogrow için izin verir. Merhaba en küçük arabellek hello toplam uygulama hizmeti planı Enflasyon oranı hesaplanan olacaktır.

Uygulama hizmeti ortamı ölçeklendirme işlemleri bazı zaman tooapply tuttuğundan, herhangi bir değişiklik bir ölçeklendirme işlemi devam ederken ortaya çıkar daha fazla isteğe bağlı değişiklikler için hesap. tooaccommodate bu gecikme, kullanmanızı öneririz hello toplam uygulama hizmeti planı Enflasyon oranı hello en az her otomatik ölçeklendirme işlemi için eklenen örnek sayısı olarak hesaplanır.

Bu bilgiyle Frank hello tanımlayabilirsiniz otomatik ölçeklendirme profili ve kurallar aşağıdaki:

![LOB örnek için otomatik ölçeklendirme profili kuralları.][Worker-Pool-Scale]

| **Otomatik ölçeklendirme profili – haftanın günü** | **Otomatik ölçeklendirme profili – hafta sonları** |
| --- | --- |
| **Ad:** haftanın günü profili |**Ad:** hafta sonu profili |
| **Ölçek tarafından:** zamanlama ve performans kuralları |**Ölçek tarafından:** zamanlama ve performans kuralları |
| **Profil:** haftanın günü |**Profil:** hafta sonu |
| **Tür:** yineleme |**Tür:** yineleme |
| **Hedef aralık:** 13 too25 örnekleri |**Hedef aralık:** 6 too15 örnekleri |
| **Gün sayısı:** Pazartesi, Salı, Çarşamba, Perşembe, Cuma |**Gün sayısı:** Cumartesi, Pazar |
| **Başlangıç zamanı:** 7: 00'da |**Başlangıç zamanı:** 09:00:00 |
| **Saat dilimi:** UTC-08 |**Saat dilimi:** UTC-08 |
|  | |
| **Otomatik ölçeklendirme kuralı (ölçeklendirme)** |**Otomatik ölçeklendirme kuralı (ölçeklendirme)** |
| **Kaynak:** çalışan havuzu 1 |**Kaynak:** çalışan havuzu 1 |
| **Ölçüm:** WorkersAvailable |**Ölçüm:** WorkersAvailable |
| **İşlem:** değerinden 8 |**İşlem:** 3'ten az |
| **Süresi:** 20 dakika |**Süresi:** 30 dakika |
| **Zaman toplama:** ortalama |**Zaman toplama:** ortalama |
| **Eylem:** sayısı 8 ile artırın |**Eylem:** artırmak sayısı 3 ile |
| **(Dakika) basılı güzel:** 180 |**(Dakika) basılı güzel:** 180 |
|  | |
| **Otomatik ölçeklendirme kural (Ölçek aşağı)** |**Otomatik ölçeklendirme kural (Ölçek aşağı)** |
| **Kaynak:** çalışan havuzu 1 |**Kaynak:** çalışan havuzu 1 |
| **Ölçüm:** WorkersAvailable |**Ölçüm:** WorkersAvailable |
| **İşlem:** 8 büyük |**İşlem:** 3'ten büyük |
| **Süresi:** 20 dakika |**Süresi:** 15 dakika |
| **Zaman toplama:** ortalama |**Zaman toplama:** ortalama |
| **Eylem:** sayısı 2 ile azaltma |**Eylem:** sayısı 3 ile azaltma |
| **(Dakika) basılı güzel:** 120 |**(Dakika) basılı güzel:** 120 |

Merhaba hello profilinde tanımlanan hedef aralık hello uygulama hizmeti planı için profili + arabellek tanımlanan hello minimum örnekler tarafından hesaplanır.

Merhaba en fazla aralık hello çalışan havuzunda barındırılan tüm uygulama hizmeti planları için tüm hello maksimum aralıklarını hello toplamı olacaktır.

Merhaba kuralları hello ölçek artırma sayısı yukarı ölçek için uygulama hizmeti planı Enflasyon oranı X kümesi tooat en az 1 olmalıdır.

1 X uygulama hizmeti planı Enflasyon oranı aşağı için ölçek hello veya azaltma sayısı 1/2 X arasında ayarlanmış toosomething olabilir.

### <a name="autoscale-for-front-end-pool"></a>Ön uç havuzu için otomatik ölçeklendirme
Ön uç otomatik ölçeklendirme kurallarını çalışan havuzlarında daha basittir. Öncelikle yapmanız gerekenler  
süresi hello ölçüm ve hello cooldown zamanlayıcılar bir uygulama hizmeti planı üzerinde ölçeklendirme işlemleri anlık olmayan dikkate aldığınızdan emin olun.

Bu senaryo için o hello hata oranı % 80 CPU kullanımı ön uçlar eriştikten sonra artırır ve hello otomatik ölçeklendirme kural tooincrease örneklerinin gibi ayarlar Frank bilir:

![Ön uç havuzu için otomatik ölçeklendirme ayarları.][Front-End-Scale]

| **Otomatik ölçeklendirme profili – ön Uçlar** |
| --- |
| **Ad:** otomatik ölçeklendirme – ön Uçlar |
| **Ölçek tarafından:** zamanlama ve performans kuralları |
| **Profil:** her gün |
| **Tür:** yineleme |
| **Hedef aralık:** 3 too10 örnekleri |
| **Gün sayısı:** her gün |
| **Başlangıç zamanı:** 09:00:00 |
| **Saat dilimi:** UTC-08 |
|  |
| **Otomatik ölçeklendirme kuralı (ölçeklendirme)** |
| **Kaynak:** ön uç havuzu |
| **Ölçüm:** CPU % |
| **İşlem:** % 60 daha büyük |
| **Süresi:** 20 dakika |
| **Zaman toplama:** ortalama |
| **Eylem:** artırmak sayısı 3 ile |
| **(Dakika) basılı güzel:** 120 |
|  |
| **Otomatik ölçeklendirme kural (Ölçek aşağı)** |
| **Kaynak:** çalışan havuzu 1 |
| **Ölçüm:** CPU % |
| **İşlem:** % 30'den az |
| **Süresi:** 20 dakika |
| **Zaman toplama:** ortalama |
| **Eylem:** sayısı 3 ile azaltma |
| **(Dakika) basılı güzel:** 120 |

<!-- IMAGES -->
[intro]: ./media/app-service-environment-auto-scale/introduction.png
[settings-scale]: ./media/app-service-environment-auto-scale/settings-scale.png
[scale-manual]: ./media/app-service-environment-auto-scale/scale-manual.png
[scale-profile]: ./media/app-service-environment-auto-scale/scale-profile.png
[scale-profile2]: ./media/app-service-environment-auto-scale/scale-profile-2.png
[scale-rule]: ./media/app-service-environment-auto-scale/scale-rule.png
[asp-scale]: ./media/app-service-environment-auto-scale/asp-scale.png
[ASP-Inflation]: ./media/app-service-environment-auto-scale/asp-inflation-rate.png
[Equation1]: ./media/app-service-environment-auto-scale/equation1.png
[Equation2]: ./media/app-service-environment-auto-scale/equation2.png
[Equation3]: ./media/app-service-environment-auto-scale/equation3.png
[Equation4]: ./media/app-service-environment-auto-scale/equation4.png
[ASP-Total-Inflation]: ./media/app-service-environment-auto-scale/asp-total-inflation-rate.png
[Worker-Pool-Scale]: ./media/app-service-environment-auto-scale/wp-scale.png
[Front-End-Scale]: ./media/app-service-environment-auto-scale/fe-scale.png
