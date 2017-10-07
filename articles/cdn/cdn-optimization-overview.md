---
title: "aaaOptimize senaryonuz için Azure içerik teslim"
description: "Nasıl toooptimize teslim içeriğinizin belirli senaryoları için"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: 922a92fdbf7e6e21f2b5ae9a2fb4ac32735fc15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-azure-content-delivery-for-your-scenario"></a>Azure içerik teslim senaryonuz için en iyi duruma getirme

İçerik tooa geniş global kullanıcılara iletirken, içeriğinizin kritik tooensure en iyi duruma getirilmiş hello teslimat olur. Hello Azure içerik teslim ağı hello teslim deneyimi hello sahip olduğunuz içerik türüne göre en iyi duruma getirebilirsiniz. Bir Web sitesi, bir canlı akış, bir video veya büyük bir dosya yüklemek için içerik olabilir. Bir içerik teslim ağı (CDN) uç noktası oluşturduğunuzda, bir senaryo hello belirttiğiniz **için en iyi duruma getirilmiş** seçeneği. Tercih ettiğiniz hangi iyileştirme uygulanan toohello içerik hello CDN uç noktasından teslim belirler.

Tasarlanmış toouse en iyi yöntem davranışları tooimprove içerik teslim performansı en iyi duruma getirme seçimlerdir ve daha iyi kaynak boşaltabilirsiniz. Senaryo seçimlerinizi kısmi önbelleğe alma, nesne Öbekleme ve hello Kaynak başarısızlığı yeniden deneme ilkesi için yapılandırmaları değiştirerek performansını etkiler. 

Bu makale, çeşitli en iyi duruma getirme özellikleri ve ne zaman kullanmanız gerektiğine genel bakış sağlar. Özellikleri ve sınırlamaları hakkında daha fazla bilgi için her tek tek en iyi duruma getirme türü hello ilgili makalelerine bakın.

> [!NOTE]
> **İçin en iyi duruma getirilmiş** seçenekleri seçtiğiniz hello sağlayıcısı göre değişir. CDN sağlayıcıları geliştirme hello senaryo bağlı olarak, farklı şekillerde uygulayın. 

## <a name="provider-options"></a>Sağlayıcı seçenekleri

Merhaba akamai'den Azure içerik teslim ağı destekler:

* Genel web teslim 

* Genel medya

* İsteğe bağlı video medya

* Büyük dosya indirme

* Dinamik site hızlandırma 

Merhaba verizon'dan Azure içerik teslim ağı yalnızca genel web teslim destekler. Video isteğe bağlı ve büyük dosya indirme için kullanılabilir. Bir en iyi duruma getirme türü tooselect yok.

Farklı sağlayıcı tooselect Merhaba, teslimat için en iyi sağlayıcısı arasındaki performans Çeşitlemeler test öneririz.

## <a name="select-and-configure-optimization-types"></a>Seçin ve en iyi duruma getirme türlerini yapılandır

Yeni bir uç noktası toocreate hello senaryo en iyi şekilde eşleşen bir en iyi duruma getirme türü ve uç nokta toodeliver hello istediğiniz içerik türü seçin. **Genel web teslim** hello varsayılan seçimdir. Herhangi bir zamanda herhangi bir varolan Akamai uç nokta için hello en iyi duruma getirme seçeneği güncelleştirebilirsiniz. Bu değişiklik hello CDN teslimat kesme değil. 

1. Standart Akamai profilindeki bir uç nokta seçin.

    ![Uç nokta seçimi ](./media/cdn-optimization-overview/01_Akamai.png)

2. Altında **ayarları**seçin **en iyi duruma getirme**. Merhaba sonra bir türü seçin **için en iyi duruma getirilmiş** aşağı açılan liste.

    ![En iyi duruma getirme ve türü seçimi](./media/cdn-optimization-overview/02_Select.png)

## <a name="optimization-for-specific-scenarios"></a>Belirli senaryolar için en iyi duruma getirme

Merhaba CDN uç senaryoları aşağıdaki hello biri için en iyi duruma getirebilirsiniz. 

### <a name="general-web-delivery"></a>Genel web teslim

Genel web teslim hello en yaygın iyileştirme seçenektir. Web sayfaları ve web uygulamaları gibi genel web içerik iyileştirme için tasarlanmıştır. Bu iyileştirme dosyası için de kullanılabilir ve video indirir.

Tipik bir Web sitesi dinamik ve statik içeriği içerir. Statik içerik görüntüleri, JavaScript kitaplıklarını ve önbelleğe alınmış ve toodifferent kullanıcılar teslim stil sayfaları içerir. Haber öğeleri tooa kullanıcı profili uyarlanmış gibi dinamik içerik bireysel bir kullanıcı için kişiselleştirilmiş. Alışveriş sepeti içeriği gibi benzersiz tooeach kullanıcı olduğundan dinamik içerik önbelleğe değil. Genel web teslim, Web sitenizin tamamını en iyi duruma getirebilirsiniz. 

> [!NOTE]
> Merhaba akamai'den Azure içerik teslim ağı kullanırsanız, bu en iyi duruma getirme, ortalama dosya boyutu 10 MB'den küçük ise toouse isteyebilirsiniz. Ortalama dosya boyutu 10 MB'den büyük ise, seçin **büyük dosya indirme** hello gelen **için en iyi duruma getirilmiş** aşağı açılan liste.

### <a name="general-media-streaming"></a>Genel medya

Canlı akış ve isteğe bağlı video akış için toouse hello uç noktası gerekiyorsa, en iyi duruma getirme Genel medya öneririz.

Geç hello istemcide gelmesini paketleri sık video içeriği arabelleğe alma gibi ek olarak, düzeyi düşürülmüş görüntüleme deneyimini neden olabileceğinden Media akışı hassas, saattir. En iyi duruma getirme medya medya içerik teslimat hello gecikmesini azaltır ve kullanıcılar için kesintisiz bir akış deneyimi sağlar. 

Bu senaryo, Azure medya hizmeti müşteriler için yaygın bir durumdur. Azure media Services'i kullanırken, canlı ve isteğe bağlı akış için kullanılan bir akış uç noktasını alın. Canlı tooon isteğe bağlı Akış değiştirdiğinizde, bu senaryo ile tooswitch tooanother endpoint müşteriler gerek yoktur. Genel ortam akış en iyi duruma getirme, bu tür senaryosu destekler.

Merhaba verizon'dan Azure içerik teslim ağı hello genel web teslim en iyi duruma getirme türü toodeliver akış medya içeriği kullanır.

toolearn daha iyileştirme, akış medya hakkında bkz [en iyi duruma getirme medya](cdn-media-streaming-optimization.md).

### <a name="video-on-demand-media-streaming"></a>İsteğe bağlı video medya

İsteğe bağlı video medya akış iyileştirme isteğe bağlı video akış içeriği artırır. İsteğe bağlı video akış için bir uç nokta kullanırsanız, bu seçenek toouse isteyebilirsiniz.

Merhaba verizon'dan Azure içerik teslim ağı hello genel web teslim en iyi duruma getirme türü toodeliver akış medya içeriği kullanır.

toolearn daha iyileştirme, akış medya hakkında bkz [en iyi duruma getirme medya](cdn-media-streaming-optimization.md).

> [!NOTE]
> Merhaba endpoint isteğe bağlı video içeriği öncelikle hizmet veriyorsa, bu en iyi duruma getirme türünü kullanın. Bu en iyi duruma getirme ve hello genel medya akış iyileştirme arasındaki temel farklardan Hello hello bağlantı yeniden deneme zaman aşımı ' dir. Merhaba zaman aşımı çok kısa toowork canlı akış senaryolarında ' dir.

### <a name="large-file-download"></a>Büyük dosya indirme

Merhaba akamai'den Azure içerik teslim ağı kullanırsanız, büyük dosya indirme toodeliver dosyaları 1,8 GB'den büyük kullanmanız gerekir. Merhaba verizon'dan Azure içerik teslim ağı dosya indirme boyutu, genel web teslim iyileştirmeden bir sınırlama yoktur.

Merhaba akamai'den Azure içerik teslim ağı kullanırsanız, büyük dosya yüklemeleri 10 MB'den büyük içerik için en iyi duruma getirilir. Ortalama dosya boyutu 10 MB'den daha küçükse, toouse genel web teslim isteyebilirsiniz. Ortalama dosya boyutu 10 MB'den büyük tutarlı bir şekilde daha verimli toocreate büyük dosyalar için ayrı bir uç noktası geçersiz olabilir. Örneğin, bellenim ve yazılım güncelleştirmeleri genellikle büyük dosyalarıdır.

Merhaba verizon'dan Azure içerik teslim ağı hello genel web teslim en iyi duruma getirme türü toodeliver akış medya içeriği kullanır.

toolearn büyük dosya iyileştirme hakkında daha fazla bilgi görmek [büyük dosya iyileştirme](cdn-large-file-optimization.md).

### <a name="dynamic-site-acceleration"></a>Dinamik site hızlandırma

 Dinamik site hızlandırma Akamai ve Verizon içerik teslim ağı profillerden kullanılabilir. Bu iyileştirme bir ek ücret toouse içerir. Daha fazla bilgi için fiyatlandırma sayfası hello bakın.

Dinamik site hızlandırma hello gecikme süresi ve dinamik içerik performansını çeşitli teknikleri içerir. Teknikler rota ve ağ iyileştirme, TCP en iyi duruma getirme ve daha fazlasını içerir. 

Bu en iyi duruma getirme tooaccelerate alınabilir bulunmayan çok sayıda yanıtları içeren bir web uygulamasını kullanabilirsiniz. Arama sonuçları, teslim alma işlemleri veya gerçek zamanlı verileri örnektir. Toouse çekirdek CDN statik verileri önbelleğe alma özelliklerini devam edebilirsiniz. 



