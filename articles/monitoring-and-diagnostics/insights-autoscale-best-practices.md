---
title: "otomatik ölçeklendirme için aaaBest uygulamaları | Microsoft Docs"
description: "Azure Web uygulamaları, sanal makine ölçek kümeleri ve bulut Hizmetleri için otomatik ölçeklendirme düzenleri"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 9fa2b94b-dfa5-4106-96ff-74fd1fba4657
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: ancav
ms.openlocfilehash: eb731c15e440af93a2675210583878814d0d8818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-autoscale"></a>Otomatik ölçeklendirme için en iyi uygulamalar
Bu makalede, azure'da en iyi yöntemler tooautoscale öğretir. Azure İzleyici otomatik ölçeklendirme uygular yalnızca çok[sanal makine ölçek kümeleri](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [bulut Hizmetleri](https://azure.microsoft.com/services/cloud-services/), ve [uygulama hizmeti - Web Apps](https://azure.microsoft.com/services/app-service/web/). Diğer Azure hizmetleriyle farklı ölçekleme yöntemlerini kullanın.

## <a name="autoscale-concepts"></a>Otomatik ölçeklendirme kavramları
* Bir kaynak yalnızca olabilir *bir* otomatik ölçeklendirme ayarı
* Otomatik ölçeklendirme ayarına sahip olabilir veya daha fazla profilleri ve her bir profili bir veya daha fazla otomatik ölçeklendirme kurallarını sağlayabilirsiniz.
* Otomatik ölçeklendirme ayarı olduğu örnekleri yatay olarak ölçeklendirir. *çıkışı* hello örnekleri artırarak ve *içinde* hello örneklerinin sayısını azaltarak tarafından.
  Otomatik ölçeklendirme ayarı, maksimum, minimum ve varsayılan değer örneklerinin sahiptir.
* Otomatik ölçeklendirme iş her zaman genişleme veya ölçek bileşenini için yapılandırılan eşiği hello taşını hello ölçüm tooscale denetleyerek, ilişkili okur. Listesini görüntüleyebileceğiniz ölçümlerini, otomatik ölçeklendirme tarafından adresindeki ölçeklendirebilirsiniz [Azure İzleyici otomatik ölçeklendirmeyi ortak ölçümleri](insights-autoscale-common-metrics.md).
* Tüm eşikler bir örnek düzeyinde hesaplanır. Örneğin, "ölçek dışarı 1 örneği tarafından ne zaman ortalama CPU > % 80'e örnek sayısı 2 olduğunda", tüm örneklerde hello ortalama CPU % 80 ' büyük olduğunda genişleme anlamına gelir.
* Her zaman e-posta yoluyla bildirimleri hatası alırsınız. Özellikle, hello sahibi, Katkıda Bulunanlar ve okuyucular hello hedef kaynağın e-posta alırsınız. Ayrıca her zaman aldığınız bir *kurtarma* otomatik ölçeklendirme bir hatadan kurtarır ve düzgün çalışan başladığında e-posta.
* Katılımı tooreceive e-posta ve Web kancalarını başarılı ölçek eylemi bildirim.

## <a name="autoscale-best-practices"></a>Otomatik ölçeklendirme en iyi uygulamalar
Otomatik ölçeklendirme kullanırken en iyi uygulamaları izleyerek hello kullanın.

### <a name="ensure-hello-maximum-and-minimum-values-are-different-and-have-an-adequate-margin-between-them"></a>Merhaba maksimum ve minimum değerler farklıdır ve bunlar arasında yeterli bir kenar boşluğu sahip emin olun
En az olan bir ayarı varsa = 2, en fazla 2 = ve hello geçerli örnek sayısı, 2, herhangi bir ölçek eylemi oluşabilir. Kapsayıcı hello maksimum ve minimum örnek sayısı arasında yeterli bir kenar boşluğu tutun. Otomatik ölçeklendirme, her zaman bu sınırlar arasında ölçeklendirir.

### <a name="manual-scaling-is-reset-by-autoscale-min-and-max"></a>Otomatik ölçeklendirme min ve max tarafından el ile ölçeklendirme sıfırlanır
El ile Merhaba örneği sayısı tooa değerini yukarıdaki güncelleştirme veya hello en otomatik ölçeklendirme altyapısı otomatik olarak hello geri toohello minimum (üstündeyse) veya hello maksimum (yüksekse) ölçeklendirir. Örneğin, 3 ile 6 arasında hello aralığı ayarlayın. Bir çalışan örneği varsa, hello otomatik ölçeklendirme altyapısı too3 örnekleri sonraki çalıştırılmasında ölçeklendirir. Benzer şekilde, bu ölçek bileşenini 8 örnekleri sonraki çalıştırılmasında too6 yedekleyin.  Merhaba otomatik ölçeklendirme kurallarını da sıfırlama sürece, el ile ölçeklendirme çok geçicidir.

### <a name="always-use-a-scale-out-and-scale-in-rule-combination-that-performs-an-increase-and-decrease"></a>Her zaman bir artırma ve azaltma yapan bir genişleme ve ölçek bileşenini kural bileşimi kullanın
Otomatik ölçeklendirme ölçek hello maksimum veya minimum değer, kadar tek çıkışı veya, bileşeni yalnızca bir bölümü hello birleşimi kullanırsanız, ulaşıldı.

### <a name="do-not-switch-between-hello-azure-portal-and-hello-azure-classic-portal-when-managing-autoscale"></a>Hello Azure portal ile Merhaba Klasik Azure portalı arasında otomatik ölçeklendirme yönetirken geçme
Bulut Hizmetleri ve uygulama Hizmetleri (Web uygulamaları), hello Azure portal (portal.azure.com) toocreate kullanın ve otomatik ölçeklendirme ayarlarını yönetin. Otomatik ölçeklendirme ayarı yönetmek ve sanal makine ölçek kümeleri için PowerShell'i, CLI veya REST API'yi toocreate kullanın. Merhaba Klasik Azure portalı (manage.windowsazure.com) arasında hello Azure portal (portal.azure.com) otomatik ölçeklendirme yapılandırmaları yönetirken geçiş değil. Klasik Azure portalı hello ve sınırlamaları, temel alınan arka uç vardır. Bir grafik kullanıcı arabirimini kullanarak toohello Azure portal toomanage otomatik ölçeklendirme taşıyın. Merhaba, toouse hello otomatik ölçeklendirme PowerShell'i, CLI veya REST API (üzerinden Azure kaynak Gezgini) seçeneklerdir.

### <a name="choose-hello-appropriate-statistic-for-your-diagnostics-metric"></a>Tanılama ölçümü için uygun istatistiği Hello seçin
Tanılama ölçümleri arasından seçim yapabilirsiniz *ortalama*, *Minimum*, *maksimum* ve *toplam* ölçüm tooscale tarafından olarak. Merhaba en yaygın istatistik *ortalama*.

### <a name="choose-hello-thresholds-carefully-for-all-metric-types"></a>Merhaba eşikleri tüm ölçüm türleri için dikkatle seçin
Dikkatli bir şekilde genişleme ve ölçek-üzerinde pratik durumlarda bağlı olarak farklı eşikler seçme öneririz.

Biz *değil önerilir* hello örnekleriyle gibi otomatik ölçeklendirme ayarları hello out ve koşullar için aynı ya da çok benzer eşik değerleri:

* Örnek 1 artırmasını ne zaman saymak iş parçacığı sayısı < = 600
* 1 ile örnekleri azaltmak ne zaman saymak iş parçacığı sayısı > = 600

Karmaşık görünebilir tooa davranışa neden olabilir, bir örneğe bakalım. Sıra aşağıdaki hello göz önünde bulundurun.

1. İle 2 örnekleri toobegin vardır ve ardından hello ortalama örnek başına iş parçacığı sayısı too625 büyütmeleri varsayalım.
2. Otomatik ölçeklendirme 3 örneğini eklemede çıkışı ölçeklendirir.
3. Ardından, hello ortalama iş parçacığı sayısı örneği arasında too575 düştüğünü varsayalım.
4. Ölçeklendirme önce hangi hello son durum içinde ölçeklendirilmiş durumunda olacaktır otomatik ölçeklendirme tooestimate çalışır. Örneğin, 575 x 3 (geçerli örnek sayısı) 1,725 = / 2 (ölçeklendirilmiş durumlarda son sayısı) 862.5 iş parçacığı =. Bu bile, ölçeği sonra hello ortalama iş parçacığı sayısı kalır hello aynı ve hatta yalnızca küçük bir miktar düşerse otomatik ölçeklendirme tooimmediately genişleme yeniden olurdu anlamına gelir. Ancak, bunu yeniden hello tüm işlemi yinelemeniz, Yukarı ölçeklendirilemez varsa tooan sonsuz döngü baştaki.
5. tooavoid ("flapping" olarak adlandırılır) bu durum olan, otomatik ölçeklendirme hiç ölçeklenmez. Bunun yerine, atlar ve reevaluates yeniden hello koşul hello sonraki zaman hello hizmetin iş yürütür. Merhaba ortalama iş parçacığı sayısı 575 olduğunda otomatik ölçeklendirme toowork görünmeyecektir çünkü bu birçok karıştırır.

Bir ölçek sırasında tahmin hedeflenen tooavoid "durumlarda, ölçek ve genişletme Eylemler sürekli geri ve İleri nereye dalgalanma" dir. Genişleme için ve aynı eşikleri hello seçtiğinizde bu davranışı göz önünde bulundurun.

Merhaba genişleme arasında ve eşikleri yeterli bir kenar boşluğu seçme öneririz. Örnek olarak, daha iyi kural birleşimi aşağıdaki hello göz önünde bulundurun.

* Örnek 1 artırmasını ne zaman saymak CPU % > = 80
* 1 ile örnekleri azaltmak ne zaman saymak CPU % < = 60

Bu durumda  

1. İle 2 örnekleri toostart vardır varsayalım.
2. Merhaba ortalama CPU % örnekleri arasında too80 kalırsa, üçüncü bir örneğini ekleme çıkışı otomatik ölçeklendirme ölçeklendirir.
3. Şimdi zaman hello CPU too60% düştüğünü varsayalım.
4. Otomatik ölçeklendirme'nın ölçek bileşenini kural tooscale bileşenini olsaydı hello son durum tahmin eder. Örneğin, 60 x 3 (geçerli örnek sayısı) 180 = / 2 (ölçeklendirilmiş durumlarda son sayısı) 90 =. Bu nedenle otomatik ölçeklendirme ölçek tooscale kullanıma hemen yeniden gerekir çünkü bileşeni değil. Bunun yerine, ölçekleme atlar.
5. Merhaba sonraki saat otomatik ölçeklendirme hello CPU toofall too50 devam denetler. Yeniden - 50 x 3 örneği tahminleri 150 = / 2 örnekleri başarıyla too2 durumlarda ölçekler için hangi 80, hello genişleme eşiğin altında 75 =.

### <a name="considerations-for-scaling-threshold-values-for-special-metrics"></a>Eşik değerleri için özel ölçümleri ölçeklendirme dikkat edilmesi gereken noktalar
 Depolama veya hizmet veri yolu kuyruğu uzunluğu ölçüm gibi özel ölçümleri hello eşik hello ortalama ileti geçerli örnek sayısı kullanılabilir sayısıdır. Merhaba seçerken dikkatli Bu ölçüm için hello eşik değerini seçin.

Şimdi gösteren bir örnek tooensure ile Merhaba davranışını daha iyi anlamak.

* Depolama kuyruğu iletisi gönderdiğinde sayısı 1 sayısına göre örneklerini artırın > = 50
* Depolama kuyruğu iletisi gönderdiğinde sayısı 1 sayısına göre örnekleri azaltmak < = 10

Merhaba dizisi aşağıdaki noktaları dikkate alın:

1. 2 depolama kuyruğu örneği vardır.
2. İleti gelmeye devam ve hello depolama kuyruğu incelediğinizde hello toplam sayısı 50 okur. Bu otomatik ölçeklendirme bir ölçeklendirme eylemi başlaması gereken varsayabilirsiniz. Ancak, 50/2 olduğunu unutmayın = örneği başına 25 iletileri. Bu nedenle, genişleme gerçekleşmez. Merhaba ilk genişleme toohappen için hello depolama kuyruğu hello toplam ileti sayısı 100 olmalıdır.
3. Ardından, hello toplam ileti sayısı 100 ulaştığında varsayalım.
4. 3 depolama sıra örneği tooa ölçeklendirme eylemi eklenir.  Merhaba sonraki ölçeklendirme eylemi hello kadar toplam hello sıradaki ileti sayısı, çünkü 150 ulaştığında yapılmaz 150/3 = 50.
5. Şimdi hello hello sıradaki ileti sayısı daha küçük alır. 3 örnekleriyle hello ilk ölçek eylemi hello tüm sıralardaki toplam ileti eklemek too30 çünkü olur 30/3 = hello ölçek bileşenini eşiğin örneği başına 10 iletileri.

### <a name="considerations-for-scaling-when-multiple-profiles-are-configured-in-an-autoscale-setting"></a>Otomatik ölçeklendirme ayarında birden çok profil yapılandırıldığında ölçeklendirme dikkat edilmesi gereken noktalar
Otomatik ölçeklendirme ayarında zamanlama veya zaman bağımlılıkları olmadan her zaman uygulanır, bir varsayılan profili seçebilir veya bir tarih ve saat aralığı ile sabit bir dönem için yinelenen bir profil ya da profili seçebilirsiniz.

Otomatik ölçeklendirme hizmeti bunları işlediğinde, her zaman sırasının hello denetler:

1. Sabit tarih profili
2. Yinelenen profili
3. Varsayılan ("her zaman") profil

Otomatik ölçeklendirme profili koşul karşılandığında hello sonraki profili koşul altındaki denetlemez. Otomatik ölçeklendirme, aynı anda yalnızca bir profil işler. Tooalso istiyorsanız, bunun anlamı bir alt katmanlı profili işleme durumundan içerir, bu kurallar hello geçerli profilinde de içermelidir.

Şimdi bu örneği kullanarak gözden geçirin:

Aşağıdaki Hello görüntü gösteren bir otomatik ölçeklendirme ayarı 2 ve en fazla örnekleri minimum örnekleri ile bir varsayılan profili = = 10. Merhaba hello sıradaki ileti sayısı 3'ten az olduğunda hello hello sıradaki ileti sayısı 10 ve ölçek bileşenini büyük olduğunda bu örnekte, yapılandırılmış tooscale kullanıma kurallardır. Şimdi hello kaynak 2 ile 10 örnekleri arasında ölçeklendirebilirsiniz.

Ayrıca, yinelenen bir profili Pazartesi kümesi yok. Minimum örnekleri için ayarlanmış 2 ve en fazla örnekleri = = 12. Yani Pazartesi günü, bu koşul için hello ilk zaman otomatik ölçeklendirme denetler hello örnek sayısı 2 ise, toohello yeni en az 3 ölçeklendirir. Otomatik ölçeklendirme (Pazartesi) bu profili koşul eşleşen toofind sürece bu profil için yapılandırılmış hello CPU tabanlı ölçek genişletme/bileşenini kuralları yalnızca işler. Şu anda bu hello sırası uzunluğu için denetlemez. Hello kuyruk uzunluğu koşulu toobe işaretli de istiyorsanız, ancak, bu kurallardan hello varsayılan profili yanı Pazartesi profilinizde içermelidir.

Otomatik ölçeklendirme geri toohello varsayılan profili geçtiğinde, benzer şekilde, bu ilk hello minimum ve maksimum koşulların karşılandığından olmadığını denetler. Hello hello zaman örneklerinin sayısını 12 ise, en fazla hello hello varsayılan profili için izin verilen too10 içinde ölçeklendirir.

![otomatik ölçeklendirme ayarları](./media/insights-autoscale-best-practices/insights-autoscale-best-practices-2.png)

### <a name="considerations-for-scaling-when-multiple-rules-are-configured-in-a-profile"></a>Birden çok kural, bir profilde yapılandırıldığında ölçeklendirme dikkat edilmesi gereken noktalar
Burada, tooset birden çok kural profilde sahip olduğu durumlar vardır. birden çok kural ayarlandığında otomatik ölçeklendirme kurallar aşağıdaki hello Hizmetleri kullanım tarafından kullanılır.

Üzerinde *ölçeğini*, herhangi bir kural karşılanır otomatik ölçeklendirme çalıştırır.
Üzerinde *ölçek bileşenini*, otomatik ölçeklendirme gerektiren tüm kuralları toobe karşılanır.

tooillustrate, 4 otomatik ölçeklendirme kurallarını izleyen hello olduğunu varsayın:

* Varsa CPU < % 30, Ölçek 1 ile açma
* Varsa bellek < % 50, Ölçek-1 ile
* Varsa CPU > %75, 1 ile genişletme
* Varsa bellek > %75, 1 ile genişletme

Ardından hello izleyin oluşur:

* % 76 CPU, bellek % 50 ise, biz genişletme.
* % 50 CPU, bellek % 76 ise, biz genişletme.

Üzerinde hello diğer yandan, CPU ise % 25 ve bellektir % 51 otomatik ölçeklendirme yapar **değil** ölçek açma. Tooscale içinde sırayla CPU %29 ve bellek % 49 olması gerekir.

### <a name="always-select-a-safe-default-instance-count"></a>Her zaman güvenli varsayılan örnek sayısı seçin
Merhaba varsayılan örnek sayısı, ölçümleri kullanılabilir olmadığında otomatik ölçeklendirme hizmeti toothat sayısını ölçeklendirir önemlidir. Bu nedenle, iş yükleriniz için güvenli bir varsayılan örnek sayısı seçin.

### <a name="configure-autoscale-notifications"></a>Otomatik ölçeklendirme bildirimleri yapılandırma
Koşullar aşağıdaki hello biri oluşursa otomatik ölçeklendirme hello yöneticileri ve katkıda bulunanlar hello kaynağının e-posta ile bildirimde bulunur.

* otomatik ölçeklendirme hizmeti tootake bir eylem başarısız olur.
* Ölçümleri otomatik ölçeklendirme hizmet toomake bir ölçek karar kullanılabilir değil.
* Ölçümleri olan kullanılabilir (Kurtarma) yeniden toomake ölçek karar.
  Ayrıca toohello koşullar yukarıdaki, başarılı ölçeklendirme eylemi için bildirim e-posta veya Web kancası bildirimleri tooget yapılandırabilirsiniz.
  
Merhaba otomatik ölçeklendirme altyapısı bir etkinlik günlüğü uyarı toomonitor hello durumunu de kullanabilirsiniz. Örnekler şunlardır çok[bir etkinlik günlüğü uyarı toomonitor aboneliğinizi tüm otomatik ölçeklendirme altyapısı işlemler oluşturmak](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert) veya çok[tüm otomatik ölçeklendirme ölçek başarısız / ölçek işlemleri bir etkinlik günlüğü uyarı toomonitor oluşturma aboneliğinizi](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).

## <a name="next-steps"></a>Sonraki Adımlar
- [Bir etkinlik günlüğü uyarı toomonitor aboneliğinizi tüm otomatik ölçeklendirme altyapısı işlemler oluşturun.](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [Tüm otomatik ölçeklendirme ölçek başarısız / aboneliğinizi işlemleri ölçeğini bir etkinlik günlüğü uyarı toomonitor oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)
