---
title: "aaaDynamic Azure CDN aracılığıyla Site hızlandırma"
description: "Dinamik site hızlandırma derinlemesine bakış"
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
ms.date: 08/02/2017
ms.author: v-semcev
ms.openlocfilehash: 37e6312ae5e83448f2d87c95ef48c387355748bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-site-acceleration-via-azure-cdn"></a>Azure CDN aracılığıyla dinamik Site hızlandırma

İle Merhaba açılımı sosyal medya, elektronik ticareti ve hello kişiselleştirilmiş hyper web içerik hello hızlı bir şekilde artan yüzdesi tooend kullanıcılara sunulan gerçek zamanlı olarak oluşturulur. Kullanıcıların hızlı, güvenilir ve kişiselleştirilmiş web deneyimleri, kullanıcıların tarayıcı, konum, cihaz veya ağ bağımsız bekler. Ancak, bu nedenle de çekici bu deneyimleri olun hello çok yenilikleri yavaş sayfa yüklemeleri ve hello kalitesinden hello tüketici riske. 

Standart CDN özelliği hello özelliği toocache dosyaları daha yakından tooend kullanıcılar toospeed teslimini statik dosyaları içerir. Hello sunucu yanıt toouser davranışını hello içerik oluşturduğundan ancak, dinamik web uygulamalarıyla kenar konumlarda o içeriği önbelleğe alma mümkün değildir. Bu tür bir içeriğin Hello teslimat hızlandırma daha geleneksel sınır önbelleğe alma daha karmaşıktır ve ince başlangıcı toodelivery hello tüm veri yolundan boyunca her öğe ayarladığını bir uçtan uca çözümü gerektirir. Azure CDN dinamik Site Hızlandırma (DSA ile), dinamik içerik web sayfalarıyla hello performansını sorunlarında geliştirildi.

Azure CDN Akamai ve Verizon sunar DSA iyileştirme hello ile **için en iyi duruma getirilmiş** uç nokta oluşturma sırasında menüsü.

## <a name="configuring-cdn-endpoint-tooaccelerate-delivery-of-dynamic-files"></a>CDN uç noktası tooaccelerate dinamik dosyaları teslimini yapılandırma

Merhaba seçerek Azure portalı üzerinden dinamik dosyaları, CDN uç noktası toooptimize teslimini yapılandırabilirsiniz **dinamik site hızlandırma** seçeneği hello altında **için en iyi duruma getirilmiş** sırasında özellik seçimi Merhaba uç nokta oluşturma. Bizim REST API de kullanabilirsiniz veya hello istemci SDK'ları toodo hiçbirini programlı olarak aynı anlama hello. 

### <a name="probe-path"></a>Araştırma yolu
Bir özellik belirli tooDynamic Site hızlandırma araştırma yoludur ve geçerli bir tane oluşturmak için gereklidir. DSA kullanan küçük bir *araştırma yolu* dosya yerleştirilen hello kaynak toooptimize yönlendirme için ağ yapılandırmalarını hello CDN üzerinde. Karşıdan yükle ve örnek dosya tooyour sitemizi karşıya yükleme veya var olan bir varlık hello varlık varsa olan yaklaşık 10 KB hello araştırma yolu için bunun yerine, kaynak kullanın.

> [!Note]
> DSA ekstra ücret doğurur. Daha fazla bilgi için bkz: Merhaba [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/cdn/) daha fazla bilgi için.

Aşağıdaki ekran görüntüleri hello Azure Portalı aracılığıyla hello işlemi gösterilmektedir.
 
![Yeni bir CDN uç noktası ekleme](./media/cdn-dynamic-site-acceleration/01_Endpoint_Profile.png) 

*Şekil 1: hello CDN profili yeni bir CDN uç noktası ekleme*
 
![DSA ile yeni bir CDN uç noktası oluşturma](./media/cdn-dynamic-site-acceleration/02_Optimized_DSA.png)  

*Şekil 2: dinamik site hızlandırma seçili iyileştirme bir CDN uç noktası oluşturma*

Merhaba CDN uç nokta oluşturulduktan sonra hello DSA iyileştirmeler belirli ölçütlere uyan tüm dosyaları için geçerlidir. bölümden hello DSA iyileştirme ayrıntılı açıklar.

## <a name="dsa-optimization-using-azure-cdn"></a>DSA Azure CDN kullanarak en iyi duruma getirme

Azure CDN dinamik Site hızlandırmasını teknikleri izleyerek hello kullanarak dinamik varlıklarını teslimat hızlandırır:

-   Rota iyileştirme
-   TCP en iyi duruma getirme
-   Nesne önceden getirme (yalnızca Akamai)
-   Mobil görüntü sıkıştırma (yalnızca Akamai)

### <a name="route-optimization"></a>Rota iyileştirme

Rota iyileştirme Hello Internet burada trafiği ve geçici olarak kesintileri sürekli hello ağ topolojisi değişen bir dinamik yer olduğundan önemlidir. Merhaba sınır ağ geçidi Protokolü (BGP), hello Internet yönlendirme protokolünün hello olmakla birlikte daha hızlı yollar Ara durum noktası (PoP) sunucuları aracılığıyla olabilir. 

Rota iyileştirme, bir site sürekli olarak erişilebilir ve dinamik içeriktir şekilde hello en iyi yolu toohello kaynak hello en hızlı ve en güvenilir yol olası yoluyla tooend kullanıcılar teslim seçer. 

Hello Akamai ağ teknikleri toocollect gerçek zamanlı verileri kullanır ve hello açık Internet toodetermine hello hızlı rota hello kaynak hello arasındaki arasında farklı düğümlerde hello Akamai sunucu gibi hello varsayılan BGP yönlendirme çeşitli yollarını Karşılaştır CDN uç. Bu teknikler Internet kaçının tıkanıklık noktaları ve uzun yollar. 

Benzer şekilde, her noktaya yayın DNS, yüksek kapasiteli bir birleşimini destek POP ve sistem durumu denetimlerini toodetermine hello en iyi ağ geçitleri toobest rota verilerinden hello Verizon ağ kullanan istemci toohello kaynak hello.
 
Sonuç olarak, tam olarak dinamik ve işlem içeriği daha hızlı ve daha güvenilir bir şekilde teslim edilir uncacheable olsa bile tooend kullanıcılar. 

### <a name="tcp-optimizations"></a>TCP en iyi duruma getirme

İletim Denetimi Protokolü (TCP) hello standart hello Internet Protokolü paketi, bir IP ağ üzerinde uygulamalar arasında toodeliver bilgileri kullanılır.  Varsayılan olarak, birden fazla arka vardır ve İleri istekleri ölçekte verimsiz sonucunda sınırları tooavoid ağ congestions yanı sıra bir TCP bağlantı kurma tooset gerekli. Akamai'den Azure CDN üç alana iyileştirerek bu sorunla ilgilidir: 

 - Yavaş başlatma ortadan
 - Yararlanmayı kalıcı bağlantılar
 - TCP paket parametrelerini (yalnızca Akamai) ayarlama

#### <a name="eliminating-slow-start"></a>Yavaş başlatma ortadan

*Yavaş başlatma* hello hello ağ üzerinden gönderilen veri miktarını sınırlandırarak Ağ Tıkanıklığı engeller hello TCP protokolü, bir parçasıdır. Bu küçük tıkanıklık pencere boyutları gönderici ve alıcı arasındaki ile Merhaba maksimum sınıra veya paket kaybı algılandığında kadar başlamanızı sağlar.

Azure CDN Akamai ve Verizon üç adımda yavaş başlatma ortadan kaldırır:

1.  Akamai ve Verizon'ın ağ durumunu ve bant genişliği toomeasure hello bant genişliği kenar PoP sunucuları arasındaki bağlantılar izleme kullanın.
2. Hello ölçümleri, böylece her sunucu hello ağ koşulları farkındadır ve sunucu sistem durumunu hello diğer POP etrafında kenar PoP sunucular arasında paylaşılır.  
3. Merhaba CDN uç sunucuların mümkün toomake varsayımlar kendi yakınlık diğer CDN uç sunucularıyla iletişim kurarken hangi hello en iyi pencere boyutunu olmalıdır gibi bazı iletim parametreleri hakkında sunulmuştur. Bu adım hello hello CDN uç sunucuları arasındaki hello bağlantı durumunu daha yüksek paket veri aktarımını yeteneğine sahipse hello ilk tıkanıklık pencere boyutu artırılabilir anlamına gelir.  

#### <a name="leveraging-persistent-connections"></a>Yararlanmayı kalıcı bağlantılar

Bir CDN kullanarak, daha az benzersiz makine doğrudan tooyour kaynak doğrudan bağlanan kullanıcıları ile karşılaştırıldığında tooyour kaynak sunucuya bağlanın. Azure CDN Akamai ve Verizon hello kaynağına sahip daha az bağlantıları da kullanıcı istekleri birlikte tooestablish havuza alır.

Daha önce belirtildiği gibi TCP bağlantıları birçok istek el sıkışma tooestablish yeni bir bağlantı İleri ve geri alın. Kalıcı bağlantılar, olarak da bilinen "HTTP Etkin tutmayı," varolan TCP bağlantılarını HTTP isteklerini toosave gidiş dönüş için defalarca ve teslimat hızı. 

Merhaba Verizon ağ düzenli tutma paketleri hello TCP bağlantısı tooprevent kapatılan gelen açık bir bağlantı üzerinden de gönderir.

#### <a name="tuning-tcp-packet-parameters"></a>TCP paket parametrelerini ayarlama

Akamai'den Azure CDN Ayrıca sunucu-sunucu bağlantıları yöneten hello parametreleri ayarladığını ve hello miktarını hello sitede teknikleri izleyerek hello kullanarak katıştırılmış içerik gerekli dönüşleri tooretrieve round uzun mesafe azaltır:

1.  Daha fazla paket için onay beklemeden gönderilebilecek hello ilk tıkanıklık penceresi artan.
2.  Merhaba ilk yeniden aktarım zaman aşımı, böylece kaybı algılanır ve aktarım daha hızlı bir şekilde gerçekleşir kısaltır.
3.  Azalan hello minimum ve maksimum yeniden ilettiği paketleri iletim kaybolduğundan varsayılarak önce zaman aşımı tooreduce hello bekleme süresi.

### <a name="object-prefetch-akamai-only"></a>Nesne önceden getirme (yalnızca Akamai)

Çoğu Web siteleri görüntüler ve komut dosyaları gibi çeşitli diğer kaynaklara başvuran bir HTML sayfası oluşur. Genellikle, bir istemci bir Web sayfası istediğinde hello tarayıcı ilk indirir ve hello HTML nesneyi ayrıştırır ve gerekli toofully olan toolinked varlıklar hello sayfa yükleme ek istekler sunar. 

*Önceden getirme* tooretrieve görüntüleri bir tekniktir ve komut dosyaları hello HTML toohello tarayıcı sunulur ve hello önce tarayıcı bile bu nesne istek yaptığında bu hello HTML sayfası katıştırılmış. 

Merhaba ile **hazırlık** seçeneği hello zaman zaman CDN hizmet hello HTML taban sayfası toohello istemci tarayıcısına hello hello CDN açık hello HTML dosyası ayrıştırır ve tüm bağlı kaynaklar için ek istekler yapıp kendi önbelleğinde depolamak. Merhaba istemci hello istekleri hello bağlı varlıkları için yaptığında, hello CDN uç sunucusu zaten sahip hello istenen nesneler ve bunları gidiş dönüş toohello kaynak hemen hizmet verebilir. Bu iyileştirme alınabilir ve alınabilir olmayan içerik fayda sağlar.

### <a name="adaptive-image-compression-akamai-only"></a>Uyarlamalı görüntü sıkıştırma (yalnızca Akamai)

Bazı aygıtlar, özellikle mobil olanları zaman tootime daha yavaş ağ hızlarını karşılaşırsınız. Bu senaryolarda daha yararlı hello kullanıcı tooreceive küçük resimleri, Web sayfası için tam çözüm görüntüleri uzun süredir bekleyen daha hızlı bir şekilde yerine.

Bu özellik otomatik olarak ağ kalite izler ve ağ hızları yavaş tooimprove teslim saati olduğunda standart JPEG sıkıştırma yöntemlerini uygular.

Uyarlamalı görüntü sıkıştırma | Dosya uzantıları  
--- | ---  
JPEG sıkıştırma | .jpg, .jpeg, .jpe, .jig, .jgig, .jgi

## <a name="caching"></a>Önbelleğe alma

Bile hello kaynak hello yanıtta önbellek denetimi/expires üst bilgileri içerdiğinde DSA ile önbelleğe alma hello CDN, varsayılan olarak kapalıdır. DSA genellikle benzersiz tooeach istemci olduğundan önbelleğe alınması gereken olmayan bir dinamik varlıklar için kullanıldığından bu varsayılan kapalıdır ve varsayılan olarak önbelleğe alma özelliğini açmak Bu davranış bölünebilir.

Statik ve dinamik varlıklar karışımını içeren bir Web sitesi varsa, en iyi tootake bir karma yaklaşım tooget hello en iyi performans olur. 

ADN Verizon Premium ile kullanıyorsanız, geri hello kurallar altyapısı kullanarak özel durumlarda önbelleğe alma kapatabilirsiniz.  

Toouse iki CDN uç noktası alternatiftir. DSA toodeliver dinamik varlıklar biriyle ve statik iyileştirme başka bir uç nokta, genel gibi web teslim toodelivery alınabilir varlıklar yazın. Bu alternatif sipariş tooaccomplish içinde toohello varlık üzerinde hello doğrudan CDN uç noktası toouse planlama, Web sayfası URL'leri toolink değiştirecektir. 

Örneğin: `mydynamic.azureedge.net/index.html` dinamik bir sayfa ve hello DSA uç noktasından yüklenir.  Merhaba html sayfası başvuruyor JavaScript kitaplıklarını gibi birden çok statik varlıklar veya gelen yüklenen görüntüleri statik CDN uç noktası gibi hello `mystatic.azureedge.net/banner.jpg` ve `mystatic.azureedge.net/scripts.js`. 

Bir örnek bulabilirsiniz [burada](https://docs.microsoft.com/azure/cdn/cdn-cloud-service-with-cdn#controller) nasıl toouse denetleyicileri bir ASP.NET uygulaması tooserve içerik belirli bir CDN URL yoluyla web üzerinde.




