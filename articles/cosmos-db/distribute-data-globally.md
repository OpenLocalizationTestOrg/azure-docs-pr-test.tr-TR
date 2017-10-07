---
title: Genel olarak Azure Cosmos DB ile aaaDistribute veri | Microsoft Docs
description: "Azure Cosmos DB, genel olarak dağıtılmış, belirleyebiliriz model veritabanı hizmeti genel veritabanlarından kullanarak planet ölçekli coğrafi çoğaltma, yük devretme ve veri kurtarma hakkında bilgi edinin."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: ba5ad0cc-aa1f-4f40-aee9-3364af070725
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/14/2017
ms.author: arramac
ms.openlocfilehash: b50e8433dc7e70c54d68c4c2f99954a13f4951f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodistribute-data-globally-with-azure-cosmos-db"></a>Nasıl toodistribute verilerle genel Azure Cosmos DB
Azure bulunabilen - 30 + coğrafi bölgeler arasında genel ayak izini sahiptir ve sürekli genişleyen. Dünya çapında iletişim durumu ile tooits geliştiriciler Azure'un sunduğu Ayrıştırılan hello yetenekleri özelliği toobuild Merhaba, dağıtmak ve genel olarak dağıtılmış uygulamaları kolayca yönetin biridir. 

[Azure Cosmos DB](../cosmos-db/introduction.md), Microsoft'un görev açısından kritik uygulamalar için genel olarak dağıtılmış çok modelli veritabanı hizmetidir. Azure Cosmos DB sağlar anahtar teslimi genel dağıtım [üretilen iş ve depolama esnek ölçeklendirme](../cosmos-db/partition-data.md) dünya, tek basamaklı milisaniyelik gecikme hello 99, adresindeki [beş iyi tanımlanmış tutarlılık düzeyleri ](consistency-levels.md), yüksek oranda kullanılabilirlik, tarafından yedeklenen tüm garanti [endüstri lideri SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure Cosmos DB [verileri otomatik olarak dizinler](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) toodeal şema ve dizin yönetimi ile gerektirmeden. Çok modelli olan bu hizmet belge, anahtar-değer, grafik ve sütunlu veri modellerini destekler. Cloud doğacak bir hizmet olarak Azure Cosmos DB dikkatle çoklu kiracı ve genel dağıtım noktasından plan hello ile geliştirilmiştir.

**Tek bir Azure Cosmos DB koleksiyon bölümlenmiş ve birçok Azure bölgesinde dağıtılmış**

![Bölümlenmiş ve üç bölgeler arasında dağıtılmış azure Cosmos DB koleksiyonu](./media/distribute-data-globally/global-apps.png)

Biz Azure Cosmos DB oluşturulurken öğrendiğiniz gibi genel dağıtım ekleme bir sonradan akla olamaz - "cıvatalı"tek site"veritabanı sistem üzerinde açma" olamaz. Geleneksel coğrafi olağanüstü durum kurtarma (DR coğrafi) "tek siteli" veritabanı tarafından sunulan ötesinde genel olarak dağıtılmış bir veritabanı tarafından sunulan hello yetenekleri span. Tek site veritabanları coğrafi DR özelliği sunan Genel dağıtılmış veritabanlarının katı bir alt kümesidir. 

İle anahtar teslimi genel dağıtım Azure Cosmos veritabanı, geliştiricilerin toobuild kendi çoğaltma yapı iskelesi ya da hello Lambda desen kullanan tarafından gerekmez (örneğin, [AWS DynamoDB çoğaltma](https://github.com/awslabs/dynamodb-cross-region-library/blob/master/README.md)) hello veritabanı günlüğü üzerinden ya da "çift yazma" birden çok bölgeler arasında yapılıyor. Biz değil, bu tür yaklaşımlardan imkansız tooensure doğruluk olduğundan bu yaklaşım önerilir ve ses SLA sağlayın. 

Bu makalede, Azure Cosmos veritabanı genel dağıtım özelliklerine genel bakış sağlar. Biz de Azure Cosmos DB'ın benzersiz bir yaklaşım tooproviding açıklayan kapsamlı SLA. 

## <a id="EnableGlobalDistribution"></a>Anahtar teslimi genel dağıtım etkinleştirme
Azure Cosmos DB sağlar hello aşağıdaki özellikleri tooenable, tooeasily planet ölçek uygulamalar yazma. Bu özellikleri hello Azure Cosmos veritabanı kaynak sağlayıcı tabanlı kullanılabilir [REST API'leri](https://docs.microsoft.com/rest/api/documentdbresourceprovider/) hello Azure portal yanı sıra.

### <a id="RegionalPresence"></a>Her yerden bölgesel varlığı 
Azure sürekli olarak artmaktadır coğrafi varlığını getirerek [yeni bölgeler](https://azure.microsoft.com/regions/) çevrimiçi. Azure Cosmos DB tüm yeni Azure bölgeleri varsayılan olarak kullanılabilir. İş için yeni bölge hello Azure açar açmaz bu tooassociate Azure Cosmos DB veritabanı hesabınızla coğrafi bölge sağlar.

**Varsayılan olarak tüm Azure bölgeleri Azure Cosmos DB kullanılamıyor**

![Azure Cosmos DB'de kullanılabilir tüm Azure bölgeleri](./media/distribute-data-globally/azure-regions.png)

### <a id="UnlimitedRegionsPerAccount"></a>Bölgeler sınırsız sayıda Azure Cosmos DB veritabanı hesabınızı ile ilişkilendirme
Azure Cosmos DB tooassociate sağlayan herhangi bir sayıda Azure Cosmos DB ile Azure bölgeleri hesabı veritabanı. Coğrafi yalıtma kısıtlamaları dışında (örneğin, Çin, Almanya), Azure Cosmos DB veritabanı hesabınızla ilişkili olabilir bölgeler hello sayısının bir sınırlama yoktur. Aşağıdaki şekilde hello 25 Azure bölgeler arasında bir veritabanı hesabı yapılandırıldı toospan gösterir.  

**Bir kiracının Azure Cosmos DB veritabanı hesabı yayılan 25 Azure bölgeleri**

![25 Azure bölgeleri kapsayıcı azure Cosmos DB veritabanı hesabı](./media/distribute-data-globally/spanning-regions.png)

### <a id="PolicyBasedGeoFencing"></a>İlke tabanlı coğrafi yalıtma
Azure Cosmos DB tasarlanmış toohave ilke tabanlı coğrafı Özellikleri ' dir. Coğrafi yalıtma önemli bileşeni tooensure veri denetim ve uyumu kısıtlamaları olan ve belirli bir bölgede hesabınızla ilişkilendirdiğiniz engelleyebilir. Coğrafi yalıtma örnekleri arasında (ancak sınırlı değildir), genel dağıtım toohello bölgeleri sovereign Bulutu (örneğin, Çin ve Almanya) içinde veya kamu vergi sınırında (örneğin, Avustralya) kapsamı. Hello ilkeleri, Azure aboneliğinizin hello meta veriler kullanılarak denetlenir.

### <a id="DynamicallyAddRegions"></a>Dinamik olarak ekleme ve bölgeler kaldırma
Azure Cosmos DB verir tooadd (ilişkilendirme) veya kaldırma (ilişkilendirmesini) bölgeleri tooyour veritabanı hesabı, herhangi bir noktada (bkz [önceki şekil](#UnlimitedRegionsPerAccount)). Paralel bölümleri arasında veri çoğaltmak Azure Cosmos DB yeni bir bölge çevrimiçi olduğunda, Azure Cosmos DB 30 dakika içinde herhangi bir yere too100 TBs yukarı Merhaba Dünya için de kullanılabilir olmasını sağlar. 

### <a id="FailoverPriorities"></a>Yük devretme öncelikler
toocontrol tam bir dizi Azure Cosmos DB çok bölgesel bir kesintinin olduğunda bölgesel yük devretme işlemlerini tooassociate hello öncelik toovarious bölgeler hello veritabanı hesabıyla ilişkilendirilmiş sağlar (aşağıdaki şekilde hello bakın). Azure Cosmos DB hello otomatik yük devretme sırası belirttiğiniz hello öncelik sırasına göre oluşmamasını sağlar. Bölgesel yük devretme hakkında daha fazla bilgi için bkz: [Azure Cosmos veritabanı iş sürekliliği için otomatik bölgesel yük devretme işlemlerini](regional-failover.md).

**Bir kiracı Azure Cosmos DB'nin veritabanı hesabıyla ilişkilendirilmiş bölgeler için hello yük devretme öncelik sırasına (sağ bölme) yapılandırabilirsiniz**

![Yük devretme öncelikleri Azure Cosmos DB ile yapılandırma](./media/distribute-data-globally/failover-priorities.png)

### <a id="OfflineRegions"></a>Dinamik olarak bir bölge "Çevrimdışı" alma
Azure Cosmos DB veritabanınızın belirli bir bölgede çevrimdışı hesap ve daha sonra yeniden çevrimiçi duruma tootake sağlar. Çevrimdışı olarak işaretlenmiş bölgeleri etkin olarak çoğaltmasında katılmak ve hello yük devretme dizisinin bir parçası değildir. Bu, bilinen son iyi veritabanı görüntüsü hello birinde tooyour uygulama yükseltmeleri riskli sunulmadan önce bölgeler okuyun toofreeze hello sağlar.

### <a id="ConsistencyLevels"></a>Genel olarak çoğaltılmış veritabanları için birden çok iyi tanımlanmış tutarlılık modelleri
Azure Cosmos DB sunan [birden çok iyi tanımlanmış tutarlılık düzeylerini](consistency-levels.md) SLA ile yedeklenir. Belirli tutarlılık modelden (Merhaba kullanılabilir seçenekler listesi) hello iş yükü/senaryoları bağlı olarak seçebilirsiniz. 

### <a id="TunableConsistency"></a>Genel olarak çoğaltılmış veritabanları için ince ayarlanabilir tutarlılık
Azure Cosmos DB tooprogrammatically geçersiz kılma sağlar ve çalışma zamanında bir istek başına hello varsayılan tutarlılık seçeneği hafifletin. 

### <a id="DynamicallyConfigurableReadWriteRegions"></a>Dinamik olarak yapılandırılabilir okuma ve yazma bölgeleri
Azure Cosmos DB tooconfigure hello bölgeler (Merhaba veritabanıyla ilişkili), "Okuma", "yazma" veya "okuma/yazma" bölgeleri için sağlar. 

### <a id="ElasticallyScaleThroughput"></a>Azure bölgeler arasında özellikler esnek ölçeklendirme işleme
Özellikler esnek bir Azure Cosmos DB koleksiyonu tarafından sağlama verimlilik programlı olarak ölçeklendirebilirsiniz. Merhaba işleme uygulanan tooall hello bölgeler hello koleksiyonu içinde dağıtılmış olur.

### <a id="GeoLocalReadsAndWrites"></a>Coğrafi yerel okuma ve yazma işlemleri
Genel olarak dağıtılmış bir veritabanı anahtar yararı Hello toooffer düşük gecikmeli erişim toohello Merhaba Dünya başka bir yerindeki verilerdir. Azure Cosmos DB çeşitli veritabanı işlemleri için P99 en düşük gecikme süresi garanti sunar. Bu, tüm okuma yönlendirilmiş toohello yakın yerel okuma bölge olmasını sağlar. tooserve Okuma isteği okuma hello verildiği hello çekirdek yerel toohello bölge kullanılır; Merhaba aynı toohello yazma geçerlidir. Yalnızca çoğaltmaların çoğunluğu işlemi hello yazma yerel olarak ancak uzak çoğaltmaları tooacknowledge hello yazma üzerinde geçişli olmadan tamamlandığı sonra yazma onaylanır. Farklı put, Azure Cosmos DB hello çoğaltma Protokolü okuma hello ve çekirdekleri her zaman yerel toohello okuma ve hangi hello isteği verilen bölgelerde, sırasıyla yazma yazma hello varsayım altında çalışır.

### <a id="ManualFailover"></a>Bölgesel yük devretme el ile başlatın
Azure Cosmos DB tootrigger hello hello veritabanı hesabı toovalidate hello Yük Devretmesini sağlar *tooend sona* kullanılabilirlik özelliklerini hello tüm uygulama (ötesinde hello veritabanı). Her ikisi de güvenliği hello ve hello hatası algılama ve öncü seçim liveness özelliklerini garanti edilir olduğundan, Azure Cosmos DB garanti *sıfır veri kaybı* Kiracı tarafından başlatılan el ile yük devretme işlemi için.

### <a id="AutomaticFailover"></a>Otomatik Yük devretme
Azure Cosmos DB bir veya daha fazla bölgesel kesintiler durumunda otomatik yük devretme destekler. Bölgesel bir yük devretme sırasında Azure Cosmos DB okuma gecikmesi, çalışma süresini kullanılabilirlik, tutarlılık ve verimlilik SLA tutar. Azure Cosmos DB bir üst sınır otomatik yük devretme işlemi toocomplete hello süresini sağlar. Bu hello olası veri kaybı hello bölgesel kesintisi sırasında penceredir.

### <a id="GranularFailover"></a>Farklı bir yük devretme ayrıntı düzeyi için tasarlanmış
Şu anda otomatik hello ve el ile yük devretme yetenekleri hello veritabanı hesabı hello bazda sunulur. Not, dahili olarak Azure Cosmos DB olduğu tasarlanmış toooffer *otomatik* yük devretme işleminde daha hassas ayrıntı düzeyi bir veritabanı, koleksiyon veya hatta bir bölümünü (anahtarları çeşitli sahip olan bir koleksiyon). 

### <a id="MultiHomingAPIs"></a>Azure Cosmos DB çok girişli API'leri
Azure Cosmos DB verir toointeract kullanarak hello veritabanıyla mantıksal (bölge belirsiz) ya da fiziksel (bölgeye özgü) uç noktaları. Mantıksal uç noktalarını kullanarak yük devretme durumunda çok konaklı hello uygulama saydam olabilir sağlar. İkincisi, fiziksel uç noktaları Merhaba, hassas bir denetim toohello uygulama tooredirect okur ve toospecific bölgeler Yazar sağlar.

Nasıl tooconfigure hello tercihlerini okuma hakkında bilgi bulabilirsiniz [DocumentDB API](../cosmos-db/tutorial-global-distribution-documentdb.md), [grafik API'si](../cosmos-db/tutorial-global-distribution-graph.md), [tablo API](../cosmos-db/tutorial-global-distribution-table.md), ve [MongoDB API](../cosmos-db/tutorial-global-distribution-mongodb.md)kendi ilgili makaleler bağlı.

### <a id="TransparentSchemaMigration"></a>Saydam ve tutarlı veritabanı şeması ve dizin geçirme 
Azure Cosmos DB olan tam olarak [şema belirsiz](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf). Veritabanı Altyapısı'nın Hello benzersiz tasarım tooautomatically sağlar ve zaman uyumlu olarak herhangi bir şemayı ya da ikincil dizinlerin sizden gerek kalmadan alır hello verilerin tümü dizin. Bu, tooiterate Genel dağıtılmış uygulamanızı hızlı bir şekilde veritabanı şeması ve dizin geçiş hakkında kaygı veya şema değişiklikleri çok aşaması piyasaya sürülmeleri Eşgüdümleme sağlar. Azure Cosmos DB açıkça tarafından yapılan tüm değişiklikler tooindexing ilkeleri neden olmaz, performans veya kullanılabilirlik düşüşü güvence altına alır.  

### <a id="ComprehensiveSLAs"></a>Kapsamlı SLA (ötesinde yalnızca yüksek oranda kullanılabilir)
Genel olarak dağıtılmış veritabanı hizmet olarak Azure Cosmos DB iyi tanımlanmış SLA sunar **veri kaybı**, **kullanılabilirlik**, **P99 gecikme süresi**, **işleme**  ve **tutarlılık** hello veritabanıyla ilişkili bölgeler hello sayısı bakılmaksızın bir bütün olarak hello veritabanı için.  

## <a id="LatencyGuarantees"></a>Gecikme garanti
Hello Azure Cosmos DB toooffer düşük gecikmeli erişim tooyour veri Merhaba Dünya başka bir yerindeki gibi bir genel dağıtılmış veritabanı hizmetinin temel avantaj. Azure Cosmos DB garantili düşük gecikme süresi P99 çeşitli veritabanı işlemleri sunar. Azure Cosmos DB kullanan hello çoğaltma protokolü, veritabanı işlemleri, hello sağlar (İdeal olarak, hem okuyan ve yazan) her zaman hello bölge yerel toothat hello istemcisi gerçekleştirilir. Merhaba gecikme P99 için Azure Cosmos DB SLA içerir hem okuma ve yazma işlemlerinin (zaman uyumlu olarak) dizinli ve çeşitli istek ve yanıt boyutları için sorgular. Merhaba gecikme garanti yazmalar için dayanıklı çoğunluğu çekirdek işlemeleri hello yerel veri merkezinde bulunan içerir.

### <a id="LatencyAndConsistency"></a>Gecikme süresi'nin ilişki tutarlılık 
İsteğe bağlı olarak bir genel dağıtılmış hizmet toooffer güçlü tutarlılık için Genel dağıtılmış kurulumunda, toosynchronously çoğaltma hello yazma gerekir ya da zaman uyumlu çapraz bölge okuma – açık ve hello geniş alan ağı güvenilirlik dikte hello hızına gerçekleştirin Bu güçlü tutarlılık yüksek gecikme ve veritabanı işlemleri düşük kullanılabilirliği ile sonuçlanır. Bu nedenle, düşük gecikme süreleri P99 ve 99.99 kullanılabilirliğini garanti sipariş toooffer içinde zaman uyumsuz çoğaltma hello service uygulamanız gerekir. Merhaba hizmeti de sağlaması gerekir bu içinde dönüş gerektiren [iyi tanımlanmış, gevşek tutarlılık choice(s)](consistency-levels.md) – güçlü daha zayıf (toooffer düşük gecikme süresi ve kullanılabilirliğini garanti) ve "son" tutarlılık (ideal güçlü toooffer sezgisel bir programlama modeli).

Azure Cosmos DB okuma işlemi değil gerekli toocontact çoğaltmaları birden çok bölgeleri toodeliver hello belirli tutarlılık düzeyi garantisi arasında olmasını sağlar. Benzer şekilde, (yani yazma zaman uyumsuz olarak bölgeler arasında çoğaltılır) tüm hello bölgelerde hello veri çoğaltılırken bir yazma işlemi engellediği değil sağlar. Birden çok gevşek tutarlılık düzeylerini bölgeli veritabanı hesapları için kullanılabilir. 

### <a id="LatencyAndAvailability"></a>Kullanılabilirlik ile gecikme'nın ilişkisi 
Gecikme süresi ve kullanılabilirlik olan hello iki tarafı da hello aynı para. Gecikme kararlı durum ve kullanılabilirlik, hatalar hello yüz hello işleminin hakkında konuşun. Merhaba uygulama açısından bir yavaş çalışan veritabanı kullanılamıyor bir veritabanından ayırt işlemdir. 

kullanılamazlık, Azure Cosmos DB gelen toodistinguish yüksek gecikme çeşitli veritabanı işlemlerini gecikme üzerinde mutlak bir üst sınır sağlar. Azure Cosmos DB Hello veritabanı işlemi hello üst sınır toocomplete uzun sürüyorsa, zaman aşımı hatası döndürür. Bu hello zaman aşımları hello kullanılabilirlik SLA karşı sayılır Hello Azure Cosmos DB kullanılabilirlik SLA'sı sağlar. 

### <a id="LatencyAndThroughput"></a>Üretilen iş ile gecikme'nın ilişkisi
Azure Cosmos DB, gecikme ve verimlilik arasında seçim yapmaz. Her iki gecikme süresi P99 hello SLA geliştirir ve sağlanan hello verimlilik sağlamak. 

## <a id="ConsistencyGuarantees"></a>Tutarlılık
Merhaba sırasında [güçlü tutarlılık modeli](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) hello altın standart hello hızı yüksek fiyatı yüksek gecikme (kararlı durumda) ve (Merhaba yüz hatalar) kullanılabilirlik kaybına gelen programlamasına. 

Azure Cosmos DB bir iyi tanımlanmış programlama modeli tooyou tooreason çoğaltılmış verilerinin tutarlılık hakkında sunar. İçinde toobuild çok konaklı uygulamalar tooenable sipariş, Azure Cosmos DB tarafından kullanıma sunulan hello tutarlılık modelleri tasarlanmış toobe bölge belirsizdir ve hello okuma ve yazma işlemleri Burada sunulan gelen hello bölge bağlı değil. 

Azure Cosmos veritabanı tutarlılık SLA % 100'okuma isteklerinin hello tutarlılığı garanti, (Merhaba varsayılan tutarlılık düzeyi hello veritabanı hesabındaki veya hello isteğinde geçersiz kılınmış hello değeri tarafından istenen hello tutarlılık düzeyi için karşıladığını garanti altına alır. ). Merhaba tutarlılık düzeyi ile ilişkili tüm hello tutarlılığı garanti sağlanırsa Okuma isteği karşılanır toohave hello tutarlılık SLA olarak kabul edilir. Merhaba aşağıdaki tabloda Azure Cosmos DB tarafından sunulan toospecific tutarlılık düzeylerini karşılık hello tutarlılığı garanti yakalar.

**Verilen tutarlılık düzeyi Azure Cosmos veritabanı ile ilişkili tutarlılığı garanti**

<table>
    <tr>
        <td><strong>Tutarlılık düzeyi</strong></td>
        <td><strong>Tutarlılık özellikleri</strong></td>
        <td><strong>SLA</strong></td>
    </tr>
    <tr>
        <td rowspan="3">Oturum</td>
        <td>Okuma kendi yazma</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Monoton okuma</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Tutarlı öneki</td>
        <td>100%</td>
    </tr>
    <tr>
        <td rowspan="3">Sınırlanmış eskime durumu</td>
        <td>Monoton okuma (bölge içinde)</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Tutarlı öneki</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Bağlı eskime durumu &lt; K, T</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Tutarlı öneki</td>
        <td>Tutarlı öneki</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Güçlü</td>
        <td>Linearizable</td>
        <td>100%</td>
    </tr>
</table>

### <a id="ConsistencyAndAvailability"></a>Kullanılabilirlik ile tutarlılık'ın ilişkisi
Merhaba [impossibility sonuç](http://www.glassbeam.com/sites/all/themes/glassbeam/images/blog/10.1.1.67.6951.pdf) Merhaba, [CAP Teoremi](https://people.eecs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf) hello sistem tooremain ve teklif linearizable tutarlılık hataları hello yüzünü gerçekten olanaksız olduğunu kanıtlar. Merhaba veritabanı hizmeti toobe seçim CP veya AP - TP sistemleri hello AP sistemleri atlayabilirsiniz sırasında kullanılabilirlik linearizable tutarlılık lehinde atlayabilirsiniz [linearizable tutarlılık](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) kullanılabilirlik lehinde. Azure Cosmos DB hiçbir zaman hello ihlal CP sistem resmi olarak kolaylaştırır tutarlılık düzeyi istendi. Bununla birlikte, pratikte tutarlılık tümü veya hiçbiri teklifinde değil – hello tutarlılık spektrumun linearizable ve nihai tutarlılık arasında boyunca birden çok iyi tanımlanmış tutarlılık model vardır. Azure Cosmos DB'de tooidentify denedik birkaç hello rahat tutarlılık modelleri gerçek dünya Uygulanabilirlik ve sezgisel bir programlama modeli. Azure Cosmos DB 99.99 kullanılabilirlik SLA'sı ile birlikte sunarak hello tutarlılık kullanılabilirlik bileşim gider [birden çok rahat henüz iyi tanımlanmış tutarlılık düzeylerini](consistency-levels.md). 

### <a id="ConsistencyAndAvailability"></a>Gecikme süresi ile tutarlılık'in ilişki
Daha kapsamlı bir değişim ucunun Prof. Daniel Abadi tarafından önerilen ve çağrılır [PACELC](http://cs-www.cs.yale.edu/homes/dna/papers/abadi-pacelc.pdf), hangi de gecikme süresi ve tutarlılık bileşim kararlı durumda hesapları. Kararlı durumda belirten, hello veritabanı sistem tutarlılık ve gecikme süresi arasında seçmeniz gerekir. (Zaman uyumsuz çoğaltma ve yerel okuma, yazma çekirdekleri tarafından desteklenir) birden çok gevşek tutarlılık modelleriyle Azure Cosmos DB tüm okuma ve yazma işlemleri yerel toohello okuma olan ve bölgeler sırasıyla yazma sağlar.  Bu hello tutarlılık düzeyleri için hello bölge içindeki Azure Cosmos DB toooffer düşük gecikme süresi garanti tanır.  

### <a id="ConsistencyAndThroughput"></a>Üretilen iş ile tutarlılık'ın ilişkisi
Belirli tutarlılık modeli Hello uygulaması üzerinde hello seçimine bağlı olduğundan bir [çekirdek türü](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf), hello verimliliği de göre değişir tutarlılık hello seçimi. Örneğin, Azure Cosmos DB'de hello işleme kesinlikle tutarlı okuma ile sonuçta tutarlı okuma, kabaca yarım toothat olabilir. 
 
**İlişki belirli tutarlılık düzeyi Azure Cosmos veritabanı için okuma kapasitesi**

![Tutarlılık ve üretilen iş arasındaki ilişki](./media/distribute-data-globally/consistency-and-throughput.png)

## <a id="ThroughputGuarantees"></a>Üretilen iş garanti altına alır. 
Azure Cosmos DB tooscale üretilen işi (yanı sıra, depolama), Özellikler esnek hello isteğe bağlı olarak farklı bölgelere sağlar. 

**(Üç parça) bölümlenmiş ve üç Azure bölgeler arasında dağıtılan bir tek bir Azure Cosmos DB koleksiyonu**

![Azure Cosmos DB dağıtılmış ve Koleksiyonlar bölümlenmiş](../cosmos-db/media/introduction/azure-cosmos-db-global-distribution.png)

Bir Azure Cosmos DB koleksiyonu bir bölge içinde ve ardından bölgeler arasında iki boyutu – kullanarak dağıtılmış. Bunu yapmak için: 

* Tek bir bölge içinde kaynak bölümler bakımından çıkışı bir Azure Cosmos DB koleksiyonu ölçeklendirilir. Her kaynak bölümü anahtar yönetir ve kesinlikle tutarlı ve çoğaltmaları kümesi arasında durumu makine çoğaltma, yüksek oranda kullanılabilir. Azure Cosmos DB bir tam olarak yönetilen kaynak bir kaynak bölümü, sistem ayrılan kaynaklar tooit hello bütçesi verimliliğini payını teslim etmek için sorumlu olduğu sistemidir. bir Azure Cosmos DB koleksiyonunu Hello ölçeklendirme tamamen saydamdır – Azure Cosmos DB hello kaynak bölümlerini yönetir ve böler ve gerektiğinde birleştirir. 
* Her hello kaynak bölümlerinin daha sonra birçok bölgeye dağıtılır. Sahip olan kaynak bölümler hello anahtarları aynı kümesini çeşitli bölgeler form bölüm kümesi boyunca (bkz [önceki şekil](#ThroughputGuarantees)).  Bir bölüm kümesi içindeki kaynak bölümler durumu makine çoğaltma hello arasında birden çok bölgeye kullanılarak düzenlenir. Yapılandırılan hello tutarlılık düzeyi bağlı olarak, farklı topoloji (örneğin, yıldız, zincir, ağaç vb.) kullanarak dinamik olarak hello kaynak bölümler bir bölüm kümesi içinde yapılandırılır. 

Bir hızlı yanıt veren bölüm yönetimi, Yük Dengeleme ve katı kaynak İdaresi sayesinde, Azure Cosmos DB tooelastically ölçek verimlilik Azure Cosmos DB koleksiyonunda birden çok Azure bölgeler arasında sağlar. Bir koleksiyon üzerinde değişen üretilen işi bir çalışma zamanı Azure Cosmos veritabanı - gibi Azure Cosmos DB hello isteği toochange hello işleme için gecikme süresini mutlak üst sınırı garanti diğer veritabanı işlemleri ile işlemdir. Örnek olarak, aşağıdaki şekilde hello hello talebe göre özellikler esnek sağlanan işleme (1 M - 10 M İsteği/sn iki bölgeler arasında değişen) ile bir müşterinin koleksiyonda gösterir.
 
**Müşteri'nin koleksiyonuyla özellikler esnek sağlanan işleme (1M - 10M İsteği/sn)**

![Azure Cosmos DB özellikler esnek işleme sağlanan](./media/distribute-data-globally/elastic-throughput.png)

### <a id="ThroughputAndConsistency"></a>Tutarlılık işleme'nin ilişki 
Aynı [üretilen iş ile tutarlılık'in ilişki](#ConsistencyAndThroughput).

### <a id="ThroughputAndAvailability"></a>Kullanılabilirlik ile işleme'nin ilişki
Azure Cosmos DB toomaintain toohello verimlilik Hello değişiklik yapıldığında, kullanılabilirlik devam eder. Azure Cosmos DB bölümleri (örneğin, bölme, birleştirme, kopyalama işlemleri) şeffaf bir şekilde yönetir ve Merhaba uygulaması özellikler esnek artırır veya verimliliği azaltır sırada hello operations performans veya kullanılabilirlik, kurtulabilirsiniz değil, sağlar. 

## <a id="AvailabilityGuarantees"></a>Kullanılabilirlik garantilerinden
Azure Cosmos DB % 99,99 açık kalma süresi kullanılabilirlik SLA her hello için veri ve denetim düzlemi işlemleri sunar. Daha önce açıklandığı gibi Azure Cosmos veritabanı kullanılabilirlik garantilerinden her veri ve denetim düzlemi işlemleri için gecikme süresini mutlak bir üst sınır içerir. Merhaba kullanılabilirlik garantilerinden steadfast ve bölgeler ve coğrafi uzaklığı bölgeler arasında hello numarasıyla değiştirmeyin. Kullanılabilirlik garantilerinden hem el ile yanı sıra, otomatik yük devretme kümelemesiyle uygulayın. Azure Cosmos DB uygulamanızı mantıksal uç noktalarına karşı çalışabilir saydam yük devretme durumunda hello istekleri toohello yeni bölge yönlendirebilir emin olun ve saydam çok girişli API'ler sunar. Farklı put, uygulamanızın toobe bölgesel yük devretme sırasında imzalanmasını gerekli değildir ve hello kullanılabilirlik SLA korunur.

### <a id="AvailabilityAndConsistency"></a>Tutarlılık, gecikme ve verimlilik ile kullanılabilirlik'ın ilişkisi
Kullanılabilirlik'in ilişki tutarlılık, gecikme ve verimlilik ile açıklanan [kullanılabilirlik ile tutarlılık'in ilişki](#ConsistencyAndAvailability), [kullanılabilirlik ile gecikme'nin ilişki](#LatencyAndAvailability) ve [kullanılabilirlik ile işleme'nin ilişki](#ThroughputAndAvailability). 

## <a id="GuaranteesAgainstDataLoss"></a>Garanti ve "veri kaybı" Sistem davranışı
Azure Cosmos DB'de (koleksiyonunun) her bölüm en az 10-20 hata etki alanlarında yayılır çoğaltmaları sayısına göre yüksek oranda kullanılabilir hale getirilir. Bunlar toohello istemci onaylanan önce tüm yazma işlemlerini çoğaltmaların çoğunluğu çekirdek tarafından eş zamanlı olarak ve işlemi çalışıyoruz. Zaman uyumsuz çoğaltma ile birlikte, birçok bölgeye yayılan bölümleri arasında uygulanır. Azure Cosmos DB bir kiracı tarafından başlatılan el ile yük devretme için hiçbir veri kaybı olduğunu güvence altına alır. Otomatik Yük devretme sırasında Azure Cosmos DB hello yapılandırılmış bir üst sınırının eskime durumu aralığı hello veri kaybı penceresinde SLA'sını bir parçası olarak ilişkisindeki güvence altına alır.

## <a id="CustomerFacingSLAMetrics"></a>Müşteri dönük SLA ölçümlerini
Azure Cosmos DB hello verimlilik, gecikme, tutarlılık ve kullanılabilirlik ölçümleri şeffaf bir şekilde kullanıma sunar. Bu ölçümleri programlamayla ve hello Azure portal (aşağıdaki şekilde bakın) üzerinden erişilebilir. Azure Application Insights'ı kullanarak çeşitli eşikleri uyarılar ayarlayabilirsiniz.
 
**Tutarlılık, gecikme süresi, performans ve kullanılabilirlik ölçümleridir, saydam kullanılabilir tooeach Kiracı**

![Azure Cosmos DB müşteri görünür SLA ölçümlerini](./media/distribute-data-globally/customer-slas.png)

## <a id="Next Steps"></a>Sonraki adımlar
* Azure Cosmos DB kullanarak hesabı üzerinde genel çoğaltma tooimplement hello Azure portal, bkz: [nasıl tooperform Azure Cosmos DB genel veritabanı çoğaltması kullanılarak izin ver hello Azure portal](tutorial-global-distribution-documentdb.md).
* toolearn konusunda tooimplement birden çok yöneticili mimarileri Azure Cosmos DB ile bkz [Azure Cosmos DB ile birden çok ana veritabanı mimarileri](multi-region-writers.md).
* Azure Cosmos DB'de otomatik ve el ile yük devretme iş nasıl toolearn hakkında daha fazla bilgi görmek [bölgesel yük devretme işlemlerini Azure Cosmos veritabanı](regional-failover.md).

## <a id="References"></a>Başvuruları
1. Eric Brewer. [Doğru sağlam dağıtılmış sistemleri](https://people.eecs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf)
2. Eric Brewer. [CAP üzeri – on iki yıllık hello kuralları nasıl değiştiğini](http://informatik.unibas.ch/fileadmin/Lectures/HS2012/CS341/workshops/reportsAndSlides/PresentationKevinUrban.pdf)
3. Gilbert, Lynch. - [Brewer &#39; s Conjecture ve tutarlı, kullanılabilir uygulanabilirliğini, bölüm dayanıklı Web Hizmetleri](http://www.glassbeam.com/sites/all/themes/glassbeam/images/blog/10.1.1.67.6951.pdf)
4. Daniel Abadi. [Veritabanı sistemleri tasarım tutarlılık bileşim Modern içinde dağıtılmış](http://cs-www.cs.yale.edu/homes/dna/papers/abadi-pacelc.pdf)
5. Martin Kleppmann. [Lütfen CP veya AP veritabanları çağırma durdurun](https://martin.kleppmann.com/2015/05/11/please-stop-calling-databases-cp-or-ap.html)
6. Peter Bailis et al. [Probabilistic sınırlanmış eskime durumu (PBS) pratik kısmi çekirdekleri için](http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf)
7. Naor ve Wool. [Yükü, kapasitesi ve çekirdek sistemlerinde kullanılabilirlik](http://www.cs.utexas.edu/~lorenzo/corsi/cs395t/04S/notes/naor98load.pdf)
8. Herlihy ve ki. [Lineralizability: Eşzamanlı nesneler için doğruluk koşul](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf)
9. [Azure Cosmos DB SLA'sı](https://azure.microsoft.com/support/legal/sla/cosmos-db/)
