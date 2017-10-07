---
title: "Service Fabric uygulamaları için planlama aaaCapacity | Microsoft Docs"
description: "Nasıl tooidentify hello Service Fabric uygulaması için gereken işlem düğümü sayısını açıklar"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: markfuss
editor: 
ms.assetid: 9fa47be0-50a2-4a51-84a5-20992af94bea
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 44a69e9d8ec5efcc43122dc42e8f923ef37378f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="capacity-planning-for-service-fabric-applications"></a>Kapasite planlama için Service Fabric uygulamaları
Bu belge nasıl tooestimate hello tutar öğretilmektedir kaynaklarının (CPU, RAM, disk depolama) Azure Service Fabric uygulamalarınızı toorun gerekir. Zaman içinde kaynak gereksinimleri toochange için yaygın bir sorundur. Siz hizmetinizi geliştirmek ve test, ve ardından üretim gidin ve popülerliği içinde uygulamanız büyüdükçe gibi daha fazla kaynak gerektirir genellikle birkaç kaynakları gerektirir. Uygulamanızı tasarlarken, uzun vadeli hello gereksinimleri düşünün ve hizmet tooscale toomeet yüksek müşteri isteğe izin seçimler.

 Service Fabric kümesi oluşturduğunuzda, ne sanal makineleri (VM'ler) tür hello küme yapmak karar verin. Her VM sınırlı miktarda kaynak hello formunda CPU (çekirdekler ve hız), ağ bant genişliği, RAM ve disk depolaması ile birlikte gelir. Hizmetinizi zamanla büyüdükçe, daha büyük kaynakları sunar ve/veya daha fazla sanal makineleri tooyour küme eklemek tooVMs yükseltebilirsiniz. dinamik olarak toohello küme eklendiklerinde yeni VM'ler özelliklerden yararlanabilirsiniz şekilde toodo hello İkincisi, hizmetiniz başlangıçta mimari gerekir.

Bazı hizmetler hello VM'ler kendilerini üzerinde çok az toono veri yönetin. Bu nedenle, bu hizmetleri hello seçerek anlamı öncelikle performansı, durmalısınız için planlama kapasite CPU (çekirdekler ve hız) hello VM'lerin uygun. Ayrıca, ağ aktarımları ne sıklıkta ortaya çıkan ve ne kadar verinin aktarıldığı dahil olmak üzere ağ bant genişliğini göz önünde bulundurmalısınız. Hizmetinizi iyi hizmet kullanım arttıkça tooperform gerekirse, daha fazla sanal makineleri toohello küme ekleyin ve tüm hello VM'ler üzerindeki yük dengeleme hello ağ isteklerini.

Merhaba VM'ler üzerinde büyük miktarlarda verinin yönetme hizmetleri için kapasite planlaması öncelikle boyutuna odaklanmanız gerekir. Bu nedenle, hello hello VM'in RAM ve disk depolama kapasitesini dikkatlice düşünün. Windows Hello sanal bellek yönetim sisteminin disk alanı RAM tooapplication kod gibi bakın sağlar. Ayrıca, hello Service Fabric çalışma zamanı bellek ve taşıma hello soğuk veri toodisk yalnızca dinamik veri tutma akıllı disk belleği sağlar. Uygulamalar, bu nedenle hello VM üzerinde kullanılabilşir olandan daha fazla bellek kullanabilir. Merhaba VM daha fazla disk depolama alanı RAM tutabilirsiniz olduğundan daha fazla RAM sahip performansı, yalnızca artırır. Merhaba seçtiğiniz VM hello VM üzerinde istediğiniz bir disk büyüklükte toostore hello veri olması gerekir. Benzer şekilde, hello VM size istediğiniz performans hello yeterli RAM tooprovide olması gerekir. Hizmetinizin veri zaman içinde büyürse, tüm hello VM'ler arasında daha fazla sanal makineleri toohello küme ve bölüm hello veri ekleyebilirsiniz.

## <a name="determine-how-many-nodes-you-need"></a>Gereksinim duyduğunuz kaç düğümleri belirler
Hizmetinizi bölümleme tooscale hizmetinizin veri çıkışı sağlar. Bölümleme hakkında daha fazla bilgi için bkz: [bölümleme Service Fabric](service-fabric-concepts-partitioning.md). Her bölüm tek bir VM'ye sığması gerekir, ancak tek bir VM üzerinde birden çok (küçük) bölüm yerleştirilebilir. Bu nedenle, daha fazla küçük bölümlemeye sahip olmak birkaç büyük bölümlemeye sahip olmak daha büyük esneklik sağlar. Merhaba dengelemeyi bölümleri çok sayıda sahip Service Fabric yükü artırır ve bölümler uygulaması yapılan işlem gerçekleştirilemiyor ' dir. Aynı zamanda hizmet kodunuzun sık farklı bölümlerde canlı veri tooaccess parçalarını gerekiyorsa ayrıca daha fazla olası ağ trafiği vardır. Hizmetinizi tasarlarken, bu Artıları ve eksileri tooarrive en etkili bir bölümleme stratejisine dikkatle düşünmelisiniz.

Uygulamanız bir yıl içinde toogrow tooDB_Size GB beklediğiniz bir depolama boyutuna sahip tek bir durum bilgisi olan hizmet sahip varsayalım. Daha fazla uygulama (ve bölümler) olarak istekli tooadd olan bu yıl ötesinde büyüme karşılaşırsınız.  hizmeti etkiler toplam DB_Size hello için çoğaltmalar Merhaba sayısını belirler hello çoğaltma faktörüyle (RF). Merhaba tüm çoğaltmalar arasında toplam DB_Size hello çoğaltma tarafından DB_Size çarpılan faktörü olur.  Node_Size temsil eden hello disk alanı/RAM düğüm başına hizmetiniz için toouse istiyor. En iyi performans için hello DB_Size, hello kümesi ve VM seçilmelidir Merhaba, RAM hello olan bir Node_Size arasında belleğe sığması. RAM kapasite hello büyük bir Node_Size ayırarak hello Service Fabric çalışma zamanı tarafından sağlanan Başlangıç disk belleği öğesine bağlı. Bu nedenle, performansınızı tüm verilerinizi toobe etkin (itibaren sonra hello verileri içeri/dışarı havuzda) kabul ediliyorsa uygun olmayabilir. Ancak, yalnızca bir kesir hello veri etkin olduğu birçok hizmetler için daha düşük maliyetli değildir.

maksimum performans için gereken düğümleri Hello sayısı aşağıdaki gibi hesaplanabilir:

```
Number of Nodes = (DB_Size * RF)/Node_Size

```


## <a name="account-for-growth"></a>Büyüme için hesabı
Toocompute hello düğüm sayısı, hizmet toogrow için ayrıca beklediğiniz DB_Size hello üzerinde toohello ile başlayan DB_Size bağlı olarak isteyebilirsiniz. Ardından, düğüm sayısını hello aşırı sağlama değil böylece hizmetinizi büyüdükçe hello düğüm sayısı artar. Ancak hello bölüm sayısı en fazla büyüme hizmetinizi çalıştırırken, gerekli olan düğüm sayısını hello dayanmalıdır.

Bu iyi toohave bazı ek makineler herhangi bir zamanda kullanılabilir olduğu (örneğin, birkaç VM'yi kesilirse) herhangi bir beklenmeyen ani veya hata işleyebilir.  Beklenen ani kullanarak Hello ek kapasite belirlenemediğinden, bir başlangıç noktası tooreserve açıkken birkaç ek VM'ler (yüzde 5-10 ek).

Merhaba önceki tek bir durum bilgisi olan hizmet varsayar. Birden fazla durum bilgisi olan hizmet varsa, diğer hizmetler hello eşitlik hello tooadd hello ilişkili DB_Size gerekir. Alternatif olarak, her durum bilgisi olan hizmet için ayrı ayrı düğüm sayısını hello hesaplayabilirsiniz.  Hizmetinizi çoğaltmaları veya dengeli olmayan bölüm olabilir. Bölümler diğerlerinden daha fazla veri de olabilen aklınızda bulundurun. Bölümleme hakkında daha fazla bilgi için bkz: [makale en iyi uygulamalar üzerinde bölümleme](service-fabric-concepts-partitioning.md). Ancak, hello önceki eşitlik bölüm ve çoğaltma olan Service Fabric hello çoğaltmaları hello düğümler arasında iyileştirilmiş bir şekilde genişlediğini olduğunu sağladığından belirsiz.

## <a name="use-a-spreadsheet-for-cost-calculation"></a>Maliyeti hesaplama için bir elektronik kullanın
Şimdi şimdi bazı gerçek sayılar hello formülde yerleştirin. Bir [örnek elektronik tablo](https://servicefabricsdkstorage.blob.core.windows.net/publicrelease/SF%20VM%20Cost%20calculator-NEW.xlsx) nasıl tooplan hello üç tür veri nesneleri içeren bir uygulama kapasiteyi gösterir. Her bir nesne için boyutuna ve kaç tane toohave bekliyoruz nesneleri yaklaşık. Biz de her nesne türünde istiyoruz kaç çoğaltmaları seçin. Merhaba elektronik tablo hello toplam bellek toobe hello kümesinde depolanan miktarını hesaplar.

Ardından bir VM boyutu ve aylık maliyeti girin. VM boyutu Hello üzerinde bağlı olarak, hello elektronik tablo hello düğümlerinde veri toophysically uygun toosplit kullanmalısınız bölüm minimum sayısı hello söyler. Çok sayıda, uygulamanızın belirli hesaplama ve ağ trafiği gereksinimleriyle bölümleri tooaccommodate işlemleriniz. Merhaba elektronik tablo hello hello kullanıcı profili nesnelerini yönetme bölüm sayısı bir toosix artırmıştır gösterir.

Şimdi, bu bilgilere dayanarak hello elektronik tablo 26 düğümlü bir küme üzerinde istenen hello bölümler ve çoğaltmalar tüm hello verilerle fiziksel olarak alabilir gösterir. Bazı ek düğümler tooaccommodate düğüm hatalarını ve yükseltmeleri isteyebilirsiniz ancak, bu küme densely, paketlenmiş. Merhaba elektronik tablo, aynı zamanda boş düğümleri gerekir çünkü birden fazla 57 düğümleri sahip herhangi bir ek değer sağladığını gösterir. Yeniden 57 düğümleri yukarıda toogo yine de tooaccommodate düğüm hatalarını ve yükseltmeleri isteyebilirsiniz. Uygulamanızın belirli gereksinimlere hello elektronik tablo toomatch değiştirebilirsiniz.   

![Maliyet hesaplamasında elektronik tablo][Image1]

## <a name="next-steps"></a>Sonraki adımlar
Kullanıma [bölümleme Service Fabric Hizmetleri] [ 10] toolearn hizmetinizi bölümleme hakkında daha fazla bilgi.

<!--Image references-->
[Image1]: ./media/SF-Cost.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-concepts-partitioning.md
