---
title: "aaaRun Linux Azure üzerinde Cassandra | Microsoft Docs"
description: "Nasıl toorun bir Cassandra küme Linux Azure Virtual Machines'de bir Node.js uygulamasını"
services: virtual-machines-linux
documentationcenter: nodejs
author: tomarcher
manager: routlaw
editor: 
tags: azure-service-management
ms.assetid: 30de1f29-e97d-492f-ae34-41ec83488de0
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 381ca301bbe88d3740cf182f9c44fada5b9ba7cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="running-cassandra-with-linux-on-azure-and-accessing-it-from-nodejs"></a>Azure’da Linux ile Cassandra Çalıştırma ve Cassandra’ya Node.js ile Erişme
> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Resource Manager şablonları için bkz: [Datastax Kurumsal](https://azure.microsoft.com/documentation/templates/datastax) ve [Spark küme ve Cassandra CentOS üzerinde](https://azure.microsoft.com/documentation/templates/spark-and-cassandra-on-centos/).

## <a name="overview"></a>Genel Bakış
Microsoft Azure hem de Microsoft işletim sistemleri, uygulama sunucuları, ileti Ara yanı sıra NoSQL ve SQL veritabanlarını hem ticari ve açık kaynak modellerinden iyi olarak Microsoft dışı yazılımlar olarak çalıştırılan bir açık bulut platformudur. Azure dahil olmak üzere genel Bulutları dayanıklı hizmetler oluşturma dikkatli planlama ve kasıtlı mimarisi iyi depolama katmanları olarak hem uygulama sunucuları için gerektirir. Doğal olarak Cassandra'nın dağıtılmış depolama mimarisi hataya dayanıklı küme hataları için yüksek oranda kullanılabilir sistemlerini oluşturmaya yardımcı olur. Cassandra bulut ölçeği cassandra.apache.org Apache yazılım Foundation tarafından tutulan NoSQL veritabanı olan; Cassandra Java'da yazılmış ve bu nedenle hem Linux yanı sıra Windows platformları çalıştırır.

Bu makalenin Hello odak tooshow Cassandra Ubuntu üzerinde Microsoft Azure sanal makineler ve sanal ağlar yararlanarak tek ve birden çok veri merkezi kümesi olarak dağıtımıdır. birden çok disk düğüm yapılandırması gerektirdiğinden hello Küme dağıtımı en iyi duruma getirilmiş üretim iş yükleri için bu makalenin kapsamı dışında uygun halka topolojisi tasarımı ve toosupport hello modelleme verileri gereken çoğaltma, veri tutarlılığı, üretilen iş ve yüksek oranda kullanılabilirlik gereksinimleri.

Bu makale, yapı hello Cassandra küme söz konusu temel yaklaşım tooshow Docker, Chef veya altyapı dağıtımı hello çok daha kolay hale getirebilir Puppet karşılaştırıldığında alır.  

## <a name="hello-deployment-models"></a>Merhaba dağıtım modelleri
Microsoft Azure ağ biri hello Erişim Yasak tooattain ince tanecikli ağ güvenliği olabilir yalıtılmış özel kümeleri hello dağıtımını sağlar.  Bu makalede temel düzeyde hello Cassandra dağıtım gösteren ilgili olduğundan, biz hello tutarlılık düzeyi ve verimlilik için hello en iyi depolama tasarımı odaklanır değil. Bizim kuramsal küme için ağ gereksinimleri hello listesi aşağıdadır:

* Dış sistemler Cassandra veritabanından içinde veya Azure dışına erişemiyor
* Cassandra küme thrift trafiği için yük dengeleyici arkasında toobe sahip
* Her veri merkezinde bir Gelişmiş küme kullanılabilirlik için iki grup Cassandra düğümler dağıtma
* Uygulama sunucusu grubu erişim toohello veritabanı doğrudan sahip yalnızca hello kümeyi bu nedenle, kilitleme
* Ortak ağ uç nokta SSH dışında
* Her Cassandra düğümü sabit bir iç IP adresi gerekiyor

Cassandra dağıtılan tooa tek Azure bölgesi veya toomultiple bölgeler hello iş yükü dağıtılan hello doğasına bağlı olabilir. Bölgeli dağıtım modeli çevrelerini tooserve son kullanıcılar daha yakından tooa belirli Coğrafya hello aracılığıyla olabilir aynı Cassandra altyapı. Cassandra'nın yerleşik düğümü çoğaltma alır dikkatli hello eşitleme çok yöneticisinin birden çok veri merkezleri kaynaklanan yazar ve hello veri tooapplications tutarlı bir görünümünü sunar. Bölgeli dağıtım ile Merhaba risk azaltma hello daha geniş Azure hizmet kesintisi durumunu da yardımcı olabilir. Cassandra'nın ince ayarlanabilir tutarlılık ve çoğaltma topolojisini uygulamaları farklı RPO ihtiyaçlarını karşılamak için yardımcı olur.

### <a name="single-region-deployment"></a>Tek bölge dağıtımı
Tek bölge dağıtımı ve bölgeli modeli oluşturma toplama hello learnings ile başlar. Yukarıda belirtilen hello ağ güvenliği gereksinimleri karşılanabilir böylece azure sanal ağı yalıtılmış kullanılan toocreate alt olacaktır.  Merhaba tek bölge dağıtımı oluşturma'da açıklandığı hello işlemi Ubuntu 14.04 LTS ve Cassandra 2.08 kullanır; Ancak, hello işlem kolayca benimsenen toohello diğer Linux çeşitleri olabilir. Merhaba hello sistemle ilgili hello tek bölge dağıtımı özelliklerini bazıları şunlardır.  

**Yüksek Kullanılabilirlik:** tootwo kullanılabilirlik ayarlar hello düğümleri yüksek kullanılabilirlik için birden çok hata etki alanları arasında yayılır Şekil 1 dağıtılan hello gösterilen Cassandra düğümleri hello. Her kullanılabilirlik kümesiyle açıklama VM'ler eşlenen too2 hata etki alanlarını olur.  Microsoft Azure kullanır hello hata etki alanı toomanage yükseltme etki alanı (örneğin, ana bilgisayar veya konuk işletim sistemi düzeltme eki uygulama/yükseltmeler, uygulama yükseltmelerini) hello kavramı sırasında (örn. donanım veya yazılım hatası) kesinti planlanmamış kavramı, zamanlanan saati yönetmek için kullanılır. Lütfen bakın [Azure uygulamaları için yüksek kullanılabilirlik ve olağanüstü durum kurtarma](http://msdn.microsoft.com/library/dn251004.aspx) yüksek kullanılabilirlik modemle hızlı bağlantılar sağlama, hata ve yükseltme etki alanlarının hello rolü için.

![Tek bölge dağıtımı](./media/cassandra-nodejs/cassandra-linux1.png)

Şekil 1: Tek bölge dağıtımı

Bu yazma Hello anda hello açık eşleme VM'ler tooa belirli bir arıza etki alanı grubunun Azure izin vermeyen unutmayın; Bu nedenle, Şekil 1'de gösterilen bile hello dağıtım modeliyle, istatistiksel olarak olası tüm hello sanal makineleri dört yerine eşlenen tootwo hata etki alanları olabilir.

**Yük Dengeleme Thrift trafiği:** hello web Sunucusu'ndaki Thrift istemci kitaplıkları bir iç yük dengeleyici toohello küme bağlanın. Bu hello iç yük dengeleyici toohello "data" alt ekleme işleminin hello gerektirir (Şekil 1 bakın) hello Cassandra küme barındırma hello bulut hizmeti hello bağlamında. Merhaba iç yük dengeleyici tanımlandıktan sonra her düğüm hello yük dengeli uç nokta toobe hello ek açıklamalar yük dengelenmiş kümeye daha önceden tanımlanmış yük dengeleyicisi adı eklendi gerektirir. Bkz: [Azure iç Yük Dengeleme ](../../../load-balancer/load-balancer-internal-overview.md)daha fazla ayrıntı için.

**Küme oluştururken çekirdeği:** tooselect hello en yüksek oranda kullanılabilir düğümler yeni düğümler hello gibi oluştururken çekirdeği çekirdek düğüm toodiscover hello topolojisi hello kümesinin ile iletişim kurması için önemlidir. Her kullanılabilirlik kümesinden bir düğümü çekirdek düğüm tooavoid tek hata noktası atanır.

**Çoğaltma faktörünü ve tutarlılık düzeyi:** hello çoğaltma faktörü (RF - kopya hello kümesinde depolanan her bir satır sayısı) tarafından Cassandra'nın yerleşik yüksek kullanılabilirlik ve veri dayanıklılığı işlemleri ve tutarlılık düzeyi (sayısı çoğaltmaları toobe okunan yazılan/hello sonuç toohello çağıran döndürmeden önce). Merhaba tutarlılık düzeyi hello CRUD sorgu verme sırasında belirtilen ancak çoğaltma faktörü hello KEYSPACE (benzer tooa ilişkisel veritabanı) oluşturma sırasında belirtilir. Cassandra belgelerine bakın [tutarlılık için yapılandırma](http://www.datastax.com/documentation/cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) tutarlılık ayrıntılarını ve çekirdek hesaplama hello formülü için.

Cassandra iki tür veri bütünlüğü modelleri – tutarlılık ve nihai tutarlılık destekler; Merhaba çoğaltma faktörü ve tutarlılık düzeyi birlikte hello veri yazma işlemi tamamlandığında veya sonuçta tutarlı hemen tutarlı olup olmayacağını belirler. Örneğin, veri tutarlılığı gerekli tooattain yazılmış çoğaltmaları toobe hello sayısı altındaki herhangi bir tutarlılık düzeyi bağlanırken tutarlılık düzeyi her zaman olacak hello sağlar gibi çekirdek belirtme (örn. bir TANE) ÇEKİRDEĞİNİ sonuçta tutarlı olan verileri sonuçlanır.

Yukarıda, 3 ve çekirdek çoğaltma faktörüyle hello 8 düğüm kümesi (2 düğümleri okumak veya tutarlılık için yazılan) okuma/yazma tutarlılık düzeyi, hello teorik kaybı çoğu 1 düğüm başına çoğaltma grubu hello uygulama başlamadan önce hello adresindeki varlığını sürdürmesini Merhaba haberiniz bile hata oluştu. Bu, tüm hello anahtar alanları okuma/yazma isteklerini iyi dengelenmiş varsayar.  Merhaba, dağıtılan hello küme için kullanacağız hello Parametreler şunlardır:

Tek bölge Cassandra küme yapılandırması:

| Küme parametresi | Değer | Açıklamalar |
| --- | --- | --- |
| Düğüm (N) sayısı |8 |Merhaba kümedeki düğümler toplam sayısı |
| Çoğaltma faktörü (RF) |3 |Belirli bir satırın çoğaltmaların sayısı |
| Tutarlılık düzeyi (yazma) |QUORUM[(RF/2) +1) = 2] hello sonuç Merhaba formül yuvarlanır |Merhaba yanıt toohello çağıran gönderilmeden önce hello çoğu 2 çoğaltma Yazar; 3 çoğaltma sonunda tutarlı bir şekilde yazılır. |
| Tutarlılık düzeyi (okuma) |Çekirdek [(RF/2) + 1 = 2] hello formülün hello sonucu aşağı yuvarlanmasını |2 çoğaltma yanıt toohello çağıran göndermeden önce okur. |
| Çoğaltma stratejisi |NetworkTopologyStrategy bakın [veri çoğaltma](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) Cassandra belgelerinde daha fazla bilgi için |Merhaba dağıtım topolojisi anlar ve çoğaltmalar, düğümlerde yerleştirir, böylece tüm hello çoğaltmalar Merhaba üzerinde aynı sona ermez raf |
| Snitch |GossipingPropertyFileSnitch bakın [Snitches](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) Cassandra belgelerinde daha fazla bilgi için |NetworkTopologyStrategy snitch toounderstand hello topoloji kavramı kullanır. GossipingPropertyFileSnitch her düğüm toodata merkezi ve raf eşleme daha iyi denetim olanağı verir. Merhaba küme dedikodu toopropagate sonra bu bilgileri kullanır. Bu dinamik IP ayarı göreli tooPropertyFileSnitch çok daha kolaydır |

**Cassandra küme Azure dikkate alınacak noktalar:** Microsoft Azure sanal makineleri özelliğine disk kalıcılığını; Azure Blob Depolama kullanır Azure depolama her disk yüksek dayanıklılık için 3 çoğaltmalarının kaydeder. Her bir Cassandra tabloya eklenen veri satırının zaten 3 yinelemede depolanır ve bu nedenle veri tutarlılığını zaten hello çoğaltma faktörü (RF) 1 olsa bile dikkate anlamına gelir. Merhaba ana çoğaltma faktörle 1 olan tek bir Cassandra düğüm başarısız olsa bile hello uygulama kapalı kalma süresi yaşar sorunudur. Ancak, bir düğüm Azure yapı denetleyicisi tarafından tanınan hello sorunları (örneğin, donanım, sistem yazılım hataları) çalışmıyorsa, onu yerde kullanarak yeni bir düğüm hazırlayacağınız hello aynı depolama sürücülerini. Bir işlem birkaç dakika sürebilir bir yeni düğümü tooreplace hello eski sağlama.  Benzer şekilde konuk işletim sistemi değişiklikleri gibi planlı bakım etkinlikler, Cassandra yükseltir ve Merhaba kümede çalışırken yükseltme hello düğümlerinin Azure yapı denetleyicisi uygulama değişiklikleri gerçekleştirir.  Çalışırken yükseltme da birkaç düğüm aynı anda sürebilir ve bu nedenle hello küme birkaç bölümler için kısa kapalı kalma süresi karşılaşabilirsiniz. Ancak, hello veri toohello yerleşik Azure Storage artıklık kayıp olmaz.  

Yüksek kullanılabilirlik gerektirmeyen tooAzure sistemleri dağıtılan için (örneğin yaklaşık 99,9 olduğu eşdeğer too8.76 SA/yıl; bkz [yüksek kullanılabilirlik](http://en.wikipedia.org/wiki/High_availability) Ayrıntılar için) RF ile mümkün toorun olabilir = 1 ve tutarlılık düzeyi = ONE.  Yüksek oranda kullanılabilirlik gereksinimleri, RF olan uygulamalar için 3 ve tutarlılık düzeyi = = çekirdek hello çoğaltmaları bir düğümlerinin hello birinin kesinti hello tolerans. RF = 1 geleneksel dağıtımlarda (örn. şirket içi), disk hataları gibi sorunlar kaynaklanan toohello olası veri kaybı nedeniyle kullanılamaz.   

## <a name="multi-region-deployment"></a>Çok bölge dağıtımı
Cassandra'nın veri merkezi kullanmayan çoğaltma ve tutarlılık modeli yardımcı hello kutusu hello olmadan dışında hello bölgeli dağıtımla yukarıda açıklanan tüm dış araçları için gerekir. Burada, birden çok yöneticili yazmalar için veritabanı yansıtma için hello Kurulum oldukça karmaşık olabilir bu hello geleneksel ilişkisel veritabanlarından oldukça farklı değildir. Ayarlanmış bir çok bölgede Cassandra hello aşağıdakiler dahil hello kullanım senaryoları yardımcı olabilir:

**Yakınlık dayalı dağıtım:** Kiracı Kullanıcı Temizle eşleme ile çok kiracılı uygulamalara-için-bölge hello bölgeli kümenin düşük gecikme tarafından benefited. Örneğin, bir öğrenme yönetim sistemleri için eğitim kurumları Doğu ABD ve Batı ABD bölgeleri tooserve hello ilgili artık kampüsünde için Dağıtılmış bir kümede dağıtabilirsiniz analytics yanı sıra işlem. Merhaba veri hello zaman okuma ve yazma işlemleri sırasında yerel olarak tutarlı olabilir ve her iki hello bölgeler arasında sonuçta tutarlı olabilir. Medya dağıtım, e-ticaret ve herhangi bir şey gibi diğer örnekler vardır ve yoğunlaşmıştır coğrafi kullanıcı temel görevi gören her şeyi, bu dağıtım modeli için iyi durumdur.

**Yüksek Kullanılabilirlik:** artıklık yazılım ve donanım yüksek kullanılabilirliğini modemle hızlı bağlantılar sağlama bir anahtar etken; yapı güvenilir bulut sistemleri Microsoft Azure üzerinde ayrıntılı bilgi için bkz. Microsoft Azure üzerinde doğru artıklık elde hello yalnızca güvenilir bir bölgeli küme dağıtarak yoludur. Uygulamaları bir etkin-etkin veya etkin-Pasif modu dağıtılabilir ve hello bölgelerinden kapalı ise, Azure Traffic Manager trafik toohello etkin bölge yönlendirebilirsiniz.  Merhaba kullanılabilirlik 99,9, ise hello tek bölge dağıtımı ile iki bölge dağıtımı hello formülüne göre hesaplanan 99.9999 kullanılabilirliği elde edebilirsiniz: (1-(1-0.999) * (1-0.999)) * 100); Ayrıntılar için kağıt yukarıda Hello bakın.

**Olağanüstü durum kurtarma:** bölgeli Cassandra küme düzgün bir şekilde tasarlanmış, dayanacak geri dönülemez veri merkezi kesintilerini. Bir bölge kapalı ise, hello dağıtılan uygulama tooother bölgeler hello son kullanıcıların hizmet veren başlatabilirsiniz. Tüm diğer iş sürekliliği uygulamaları gibi hello uygulama toobe hello veri hello zaman uyumsuz ardışık düzeninde kaynaklanan bazı veri kaybıyla dayanıklı sahiptir. Ancak, Cassandra hello kurtarma geleneksel veritabanı kurtarma işlemleri tarafından harcanan hello süre çok swifter yapar. Şekil 2 sekiz düğümlerle hello tipik bölgeli dağıtım modeli, her bölgede gösterir. Yansıtma görüntülerini Merhaba için iki bölgeleri olan simetrisi; aynı gerçek dünya tasarımları hello iş yükü türünü (örn. işlem veya analitik), RPO, RTO, veri tutarlılığı ve kullanılabilirlik gereksinimlerine bağlıdır.

![Çoklu bölge dağıtımı](./media/cassandra-nodejs/cassandra-linux2.png)

Şekil 2: Bölgeli Cassandra dağıtımı

### <a name="network-integration"></a>Ağ tümleştirme
Sanal makineler üzerinde iki bölgede bulunan dağıtılan tooprivate ağlar birbirleri ile iletişim kurar kümesi VPN tüneli kullanma. Merhaba VPN tüneli hello ağ dağıtım işlemi sırasında sağlanan iki yazılım ağ geçidi bağlanır. Her iki bölgeden "web" ve "data" alt bakımından benzer ağ mimarisi; yine de sahip istiyor musunuz? Azure ağı gerektiğinde kadar alt ağlar hello oluşturulmasına izin verir ve ağ güvenliği tarafından gerektiği şekilde ACL'ler uygulayın. Merhaba küme topolojisi tasarlarken, veri merkezi iletişimi gecikme süresi ve hello ekonomik etkisini hello ağ trafiği gerek toobe kabul ağlar arası.

### <a name="data-consistency-for-multi-data-center-deployment"></a>Birden çok veri merkezi dağıtım için veri tutarlılığı
Dağıtımları gerek toobe hello küme topolojisi etkisini performans ve yüksek kullanılabilirlik farkında dağıtılmış. Merhaba çekirdek hello bu şekilde seçtiğiniz RF ve tutarlılık düzeyi gereksinimi toobe tüm hello veri merkezleri hello kullanılabilirliğini bağımlı değil.
Tutarlılık düzeyi (okuma ve yazma) bu hello yerel emin olmanızı sağlayacak için yüksek tutarlılık, bir LOCAL_QUORUM gerektiren bir sistem okuma ve yazma hello yerel karşılanır veri aktarılırken düğümleri toohello uzak veri merkezleri zaman uyumsuz olarak kopyalandığı.  Tablo 2 hello yapılandırma ayrıntıları daha sonra hello özetlenen hello bölgeli kümesi için yazma yukarı özetlenmiştir.

**İki bölge Cassandra küme yapılandırması**

| Küme parametresi | Değer | Açıklamalar |
| --- | --- | --- |
| Düğüm (N) sayısı |8 + 8 |Merhaba kümedeki düğümler toplam sayısı |
| Çoğaltma faktörü (RF) |3 |Belirli bir satırın çoğaltmaların sayısı |
| Tutarlılık düzeyi (yazma) |LOCAL_QUORUM [(sum(RF)/2) +1) = 4] hello formülün hello sonucu aşağı yuvarlanmasını |2 düğümleri toohello ilk veri merkezi zaman uyumlu olarak yazılır; Merhaba ek 2 düğümler çekirdek için gereken zaman uyumsuz olarak toohello 2 veri merkezi yazılır. |
| Tutarlılık düzeyi (okuma) |LOCAL_QUORUM ((RF/2) + 1) = 2 hello formülün hello sonucu aşağı yuvarlanmasını |Okuma isteği yalnızca bir bölgesinden karşılanır; Merhaba yanıt geri toohello istemci gönderilmeden önce 2 düğümleri salt okunurdur. |
| Çoğaltma stratejisi |NetworkTopologyStrategy bakın [veri çoğaltma](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) Cassandra belgelerinde daha fazla bilgi için |Merhaba dağıtım topolojisi anlar ve çoğaltmalar, düğümlerde yerleştirir, böylece tüm hello çoğaltmalar Merhaba üzerinde aynı sona ermez raf |
| Snitch |GossipingPropertyFileSnitch bakın [Snitches](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) Cassandra belgelerinde daha fazla bilgi için |NetworkTopologyStrategy snitch toounderstand hello topoloji kavramı kullanır. GossipingPropertyFileSnitch her düğüm toodata merkezi ve raf eşleme daha iyi denetim olanağı verir. Merhaba küme dedikodu toopropagate sonra bu bilgileri kullanır. Bu dinamik IP ayarı göreli tooPropertyFileSnitch çok daha kolaydır |

## <a name="hello-software-configuration"></a>Merhaba yazılım yapılandırma
yazılım sürümleri aşağıdaki hello hello dağıtımı sırasında kullanılır:

<table>
<tr><th>Yazılım</th><th>Kaynak</th><th>Sürüm</th></tr>
<tr><td>JRE    </td><td>[JRE 8](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) </td><td>8U5</td></tr>
<tr><td>JNA    </td><td>[JNA](https://github.com/twall/jna) </td><td> 3.2.7</td></tr>
<tr><td>Cassandra</td><td>[Apache Cassandra 2.0.8](http://www.apache.org/dist/cassandra/2.0.8/apache-cassandra-2.0.8-bin.tar.gz)</td><td> 2.0.8</td></tr>
<tr><td>Ubuntu    </td><td>[Microsoft Azure](https://azure.microsoft.com/) </td><td>14.04 LTS</td></tr>
</table>

JRE indirme Oracle lisans, toosimplify hello dağıtım, tüm gerekli yazılım toohello Masaüstü biz precursor toohello küme olarak oluşturulacağını hello Ubuntu şablon görüntüsü daha sonra yüklemeyle hello indirme el ile kabul gerektirdiğinden dağıtımı.

Bir dizine iyi bilinen yükleme (örneğin Windows %TEMP%/downloads veya ~/Downloads çoğu Linux dağıtımları veya Mac üzerinde) hello yerel bilgisayarda yazılım yukarıda Hello indirin.

### <a name="create-ubuntu-vm"></a>UBUNTU VM OLUŞTURMA
Böylece Hello görüntü birçok Cassandra düğümlerini sağlamak için yeniden kullanılabilir hello işleminin bu adımında Ubuntu görüntü hello önkoşul yazılımı ile oluşturacağız.  

#### <a name="step-1-generate-ssh-key-pair"></a>1. adım: SSH anahtar çifti oluşturma
Azure PEM ya da DER ortak anahtar zaman sağlama hello kodlanmış bir X509 gerekir. Ne bulunan hello yönergeleri kullanarak bir genel/özel anahtar çifti oluşturmak tooUse SSH Linux Azure üzerinde. Bir SSH istemcisi Windows veya Linux olarak toouse putty.exe düşünüyorsanız, tooconvert sahip hello PEM kodlanmış puttygen.exe; kullanarak RSA özel anahtar tooPPK biçimi Merhaba yönergeler için bu web sayfası yukarıda hello bulunabilir.

#### <a name="step-2-create-ubuntu-template-vm"></a>2. adım: Ubuntu şablonu VM oluşturma
toocreate hello şablonu VM dizisi şu Azure Klasik portalı ve kullanım hello hello oturum: yeni, işlem, sanal makine, başlangıç Galerisi, UBUNTU, Ubuntu Server 14.04 LTS tıklatın ve ardından hello sağ oka tıklayın. Bir Linux VM toocreate nasıl görürüm açıklayan bir öğretici için çalışan bir sanal makine Linux oluşturun.

#1 "sanal makine yapılandırma" Merhaba ekranında bilgisinden hello girin:

<table>
<tr><th>ALAN ADI              </td><td>       ALAN DEĞERİ               </td><td>         AÇIKLAMALAR                </td><tr>
<tr><td>SÜRÜM YAYIN TARİHİ    </td><td> Merhaba açılan tarih seçin</td><td></td><tr>
<tr><td>SANAL MAKİNE ADI    </td><td> CASS şablonu                   </td><td> Bu hello VM hello ana adıdır </td><tr>
<tr><td>KATMANI                     </td><td> STANDART                           </td><td> Merhaba varsayılan adı bırakın              </td><tr>
<tr><td>BOYUTU                     </td><td> A1                              </td><td>G/ç hello üzerinde VM tabanlı select hello gerekiyor; Bu amaçla hello varsayılan adı bırakın </td><tr>
<tr><td> YENİ BİR KULLANICI ADI             </td><td> yerelyönetici                       </td><td> "Yönetici" Ubuntu 12. xx ve sonra ayrılmış kullanıcı adı sağlanmış</td><tr>
<tr><td> KİMLİK DOĞRULAMASI         </td><td> Onay kutusu                 </td><td>Bir SSH anahtarı ile toosecure istiyorsanız denetleyin </td><tr>
<tr><td> SERTİFİKA             </td><td> Merhaba ortak anahtar sertifikası dosya adı </td><td> Daha önce oluşturulan hello ortak anahtarı kullanır</td><tr>
<tr><td> Yeni parola    </td><td> güçlü parola </td><td> </td><tr>
<tr><td> Parolayı onaylayın    </td><td> güçlü parola </td><td></td><tr>
</table>

#2 hello "sanal makine yapılandırma" ekranında bilgisinden hello girin:

<table>
<tr><th>ALAN ADI             </th><th> ALAN DEĞERİ                       </th><th> AÇIKLAMALAR                                 </th></tr>
<tr><td> BULUT HİZMETİ    </td><td> Yeni bir bulut hizmeti oluştur    </td><td>Sanal makineler gibi bir kapsayıcı işlem kaynaklarını bulut hizmetidir</td></tr>
<tr><td> BULUT HİZMETİ DNS ADI    </td><td>ubuntu template.cloudapp.net    </td><td>Bir makine belirsiz yük dengeleyici ad verin</td></tr>
<tr><td> BÖLGE/BENZEŞİM GRUBU/SANAL AĞ </td><td>    Batı ABD    </td><td> Web uygulamalarınızın hello Cassandra küme erişimlerin bir bölge seçin</td></tr>
<tr><td>DEPOLAMA HESABI </td><td>    Varsayılanı kullan    </td><td>Belirli bir bölgedeki Hello varsayılan depolama hesabı ya da önceden oluşturulmuş depolama hesabı kullanın</td></tr>
<tr><td>KULLANILABİLİRLİK KÜMESİ </td><td>    None </td><td>    Boş bırakın</td></tr>
<tr><td>UÇ NOKTALARI    </td><td>Varsayılanı kullan </td><td>    Merhaba varsayılan SSH yapılandırmasını kullanın </td></tr>
</table>

Sağ oka tıklayın, #3 Merhaba ekranında hello Varsayılanları bırakabilir ve hello "onay" düğmesine toocomplete hello VM sağlama işlemi'ı tıklatın. Birkaç dakika sonra hello VM hello adı "ubuntu-şablon" ile "çalışır" durumda olması gerekir.

### <a name="install-hello-necessary-software"></a>Merhaba gerekli yazılımı yükleyin
#### <a name="step-1-upload-tarballs"></a>1. adım: Karşıya yükleme tarballs
SCP veya pscp kullanarak kopyalama hello daha önce yazılım çok indirilen ~ / yüklemeleri dizinini kullanarak komut biçimi aşağıdaki hello:

##### <a name="pscp-server-jre-8u5-linux-x64targz-localadminhk-cas-templatecloudappnethomelocaladmindownloadsserver-jre-8u5-linux-x64targz"></a>pscp server-jre-8u5-linux-x64.tar.gzlocaladmin@hk-cas-template.cloudapp.net:/home/localadmin/downloads/server-jre-8u5-linux-x64.tar.gz
Merhaba komutu yukarıda de JRE hello Cassandra BITS için yineleyin.

#### <a name="step-2-prepare-hello-directory-structure-and-extract-hello-archives"></a>2. adım: hello dizin yapısını hazırlamak ve hello arşivler Ayıkla
VM Hello oturum ve hello dizin yapısını oluşturun ve yazılım hello bash aşağıdaki komut dosyası kullanarak bir süper kullanıcı olarak ayıklayın:

    #!/bin/bash
    CASS_INSTALL_DIR="/opt/cassandra"
    JRE_INSTALL_DIR="/opt/java"
    CASS_DATA_DIR="/var/lib/cassandra"
    CASS_LOG_DIR="/var/log/cassandra"
    DOWNLOADS_DIR="~/downloads"
    JRE_TARBALL="server-jre-8u5-linux-x64.tar.gz"
    CASS_TARBALL="apache-cassandra-2.0.8-bin.tar.gz"
    SVC_USER="localadmin"

    RESET_ERROR=1
    MKDIR_ERROR=2

    reset_installation ()
    {
       rm -rf $CASS_INSTALL_DIR 2> /dev/null
       rm -rf $JRE_INSTALL_DIR 2> /dev/null
       rm -rf $CASS_DATA_DIR 2> /dev/null
       rm -rf $CASS_LOG_DIR 2> /dev/null
    }
    make_dir ()
    {
       if [ -z "$1" ]
       then
          echo "make_dir: invalid directory name"
          exit $MKDIR_ERROR
       fi

       if [ -d "$1" ]
       then
          echo "make_dir: directory already exists"
          exit $MKDIR_ERROR
       fi

       mkdir $1 2>/dev/null
       if [ $? != 0 ]
       then
          echo "directory creation failed"
          exit $MKDIR_ERROR
       fi
    }

    unzip()
    {
       if [ $# == 2 ]
       then
          tar xzf $1 -C $2
       else
          echo "archive error"
       fi

    }

    if [ -n "$1" ]
    then
       SVC_USER=$1
    fi

    reset_installation
    make_dir $CASS_INSTALL_DIR
    make_dir $JRE_INSTALL_DIR
    make_dir $CASS_DATA_DIR
    make_dir $CASS_LOG_DIR

    #unzip JRE and Cassandra
    unzip $HOME/downloads/$JRE_TARBALL $JRE_INSTALL_DIR
    unzip $HOME/downloads/$CASS_TARBALL $CASS_INSTALL_DIR

    #Change hello ownership toohello service credentials

    chown -R $SVC_USER:$GROUP $CASS_DATA_DIR
    chown -R $SVC_USER:$GROUP $CASS_LOG_DIR
    echo "edit /etc/profile tooadd JRE toohello PATH"
    echo "installation is complete"


Bu komut dosyası VIM penceresine yapıştırın, emin tooremove hello satır dönmesi ('\r ") komutu aşağıdaki hello kullanarak:

    tr -d '\r' <infile.sh >outfile.sh

#### <a name="step-3-edit-etcprofile"></a>3. adım: vb./profilini düzenle
Merhaba sonunda Hello aşağıdakileri ekleyin:

    JAVA_HOME=/opt/java/jdk1.8.0_05
    CASS_HOME= /opt/cassandra/apache-cassandra-2.0.8
    PATH=$PATH:$HOME/bin:$JAVA_HOME/bin:$CASS_HOME/bin
    export JAVA_HOME
    export CASS_HOME
    export PATH

#### <a name="step-4-install-jna-for-production-systems"></a>4. adım: Yükleme JNA üretim sistemleri için
Kullanım hello aşağıdaki komut dizisi: hello şu komutu yükleme jna-3.2.7.jar ve jna platform 3.2.7.jar too/usr/share.java directory sudo apt get yükleyecek libjna java

Sembolik bağlantılar $CASS_HOME/lib dizininde oluşturun, böylece Cassandra başlangıç betiği bu Kavanoz bulabilirsiniz:

    ln -s /usr/share/java/jna-3.2.7.jar $CASS_HOME/lib/jna.jar

    ln -s /usr/share/java/jna-platform-3.2.7.jar $CASS_HOME/lib/jna-platform.jar

#### <a name="step-5-configure-cassandrayaml"></a>Adım 5: cassandra.yaml yapılandırma
[Biz bu hello gerçek sağlama sırasında ince ayar] tüm hello sanal makineler için gerekli her VM tooreflect yapılandırmasında cassandra.yaml düzenleyin:

<table>
<tr><th>Alan adı   </th><th> Değer  </th><th>    Açıklamalar </th></tr>
<tr><td>küme_adı </td><td>    "CustomerService"    </td><td> Dağıtımınızı yansıtır hello adını kullan</td></tr>
<tr><td>listen_address    </td><td>[boş bırakın]    </td><td> "Localhost" Sil </td></tr>
<tr><td>rpc_addres   </td><td>[boş bırakın]    </td><td> "Localhost" Sil </td></tr>
<tr><td>oluştururken Çekirdeği    </td><td>"10.1.2.4, 10.1.2.6, 10.1.2.8"    </td><td>Şu oluştururken çekirdeği atanan tüm hello IP adresleri listesi.</td></tr>
<tr><td>endpoint_snitch </td><td> org.apache.cassandra.locator.GossipingPropertyFileSnitch </td><td> Bu NetworkTopologyStrateg hello tarafından çıkarımını yapma hello veri merkezi ve hello VM hello sunucu rafı için kullanılır</td></tr>
</table>

#### <a name="step-6-capture-hello-vm-image"></a>6. adım: hello VM görüntüsü yakalama
Merhaba sanal makineye hello hostname (hk-CA-template.cloudapp.net) ve daha önce oluşturduğunuz hello SSH özel anahtarı kullanarak oturum açın. Bkz. nasıl kullanarak toolog hello komutu ssh veya putty.exe tooUse Linux için azure'da SSH ayrıntıları nasıl.

Eylemler toocapture hello görüntü dizisini aşağıdaki hello yürütün:

##### <a name="1-deprovision"></a>1. Deprovision
Merhaba komutunu "sudo waagent-deprovision + kullanıcı" tooremove sanal makine örneği belirli bilgileri. İçin bkz: [nasıl tooCapture Linux sanal makine](capture-image.md) tooUse bir şablon olarak daha ayrıntılı hello görüntü yakalama işlemi.

##### <a name="2-shutdown-hello-vm"></a>2: kapatma hello VM
Merhaba sanal makinenin vurgulanmış emin olun ve hello altındaki komut çubuğundan hello kapatma bağlantısına tıklayın.

##### <a name="3-capture-hello-image"></a>3: yakalama hello görüntüsü
Merhaba sanal makinenin vurgulanmış emin olun ve hello altındaki komut çubuğundan hello YAKALAMA bağlantısını tıklatın. Merhaba sonraki ekranda, (örneğin hk-cas-2-08-ub-14-04-2014071) bir görüntü adı verin ve görüntü açıklaması uygun hello "onay" işareti toofinish hello YAKALAMA işlemi'ı tıklatın.

Bu işlem birkaç saniye sürer ve hello görüntü GÖRÜNTÜLERİM Merhaba görüntü Galerisi bölümünde kullanılabilir olmalıdır. Merhaba görüntüsü başarıyla yakalandı sonra hello kaynak VM otomatik olarak silinir. 

## <a name="single-region-deployment-process"></a>Tek bölge dağıtım işlemi
**1. adım: hello sanal ağ oluşturma** hello Azure portalında oturum ve aşağıdaki tablonun hello gösterilen bir sanal ağ (Klasik) hello özniteliklerle oluşturun. Bkz: [hello Azure portal kullanarak bir sanal ağ (Klasik) oluşturmak](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md) hello işleminin ayrıntılı adımlar için.      

<table>
<tr><th>VM öznitelik adı</th><th>Değer</th><th>Açıklamalar</th></tr>
<tr><td>Ad</td><td>vnet-cass-Batı-ABD</td><td></td></tr>
<tr><td>Bölge</td><td>Batı ABD</td><td></td></tr>
<tr><td>DNS sunucuları</td><td>None</td><td>Bir DNS sunucusu kullanmıyorsanız gibi bu iletiyi yoksayın</td></tr>
<tr><td>Adres alanı</td><td>10.1.0.0/16</td><td></td></tr>    
<tr><td>Başlangıç IP</td><td>10.1.0.0</td><td></td></tr>    
<tr><td>CIDR </td><td>/16 (65531)</td><td></td></tr>
</table>

Alt ağları aşağıdaki hello ekleyin:

<table>
<tr><th>Ad</th><th>Başlangıç IP</th><th>CIDR</th><th>Açıklamalar</th></tr>
<tr><td>Web</td><td>10.1.1.0</td><td>/24 (251)</td><td>Merhaba web grubu için alt ağ</td></tr>
<tr><td>Veri</td><td>10.1.2.0</td><td>/24 (251)</td><td>Merhaba veritabanı düğümleri için alt ağ</td></tr>
</table>

Veri ve Web alt ağ güvenlik grupları üzerinden hangi hello kapsamını bu makalenin kapsamı dışındadır korunabilir.  

**2. adım: Sanal makine sağlamak** daha önce oluşturduğunuz hello görüntüsünü kullanarak, sunucu "hk-c-svc-Batı" Merhaba bulutta sanal makineler aşağıdaki hello oluşturur ve bunları aşağıda gösterildiği gibi toohello ilgili alt ağlarına bağlayın:

<table>
<tr><th>Makine adı    </th><th>Alt ağ    </th><th>IP Adresi    </th><th>Kullanılabilirlik kümesi</th><th>DC/raf</th><th>Çekirdek?</th></tr>
<tr><td>HK-c1-Batı-ABD    </td><td>Veri    </td><td>10.1.2.4    </td><td>HK-c-aset-1    </td><td>DC WESTUS raf = raf1 = </td><td>Evet</td></tr>
<tr><td>HK-c2-Batı-ABD    </td><td>Veri    </td><td>10.1.2.5    </td><td>HK-c-aset-1    </td><td>DC WESTUS raf = raf1 =    </td><td>Hayır </td></tr>
<tr><td>HK-c3-Batı-ABD    </td><td>Veri    </td><td>10.1.2.6    </td><td>HK-c-aset-1    </td><td>DC WESTUS raf = rack2 =    </td><td>Evet</td></tr>
<tr><td>HK-c4-Batı-ABD    </td><td>Veri    </td><td>10.1.2.7    </td><td>HK-c-aset-1    </td><td>DC WESTUS raf = rack2 =    </td><td>Hayır </td></tr>
<tr><td>HK-c5-Batı-ABD    </td><td>Veri    </td><td>10.1.2.8    </td><td>HK-c-aset-2    </td><td>DC WESTUS raf = rack3 =    </td><td>Evet</td></tr>
<tr><td>HK-c6-Batı-ABD    </td><td>Veri    </td><td>10.1.2.9    </td><td>HK-c-aset-2    </td><td>DC WESTUS raf = rack3 =    </td><td>Hayır </td></tr>
<tr><td>HK-c7-Batı-ABD    </td><td>Veri    </td><td>10.1.2.10    </td><td>HK-c-aset-2    </td><td>DC WESTUS raf = rack4 =    </td><td>Evet</td></tr>
<tr><td>HK-c8-Batı-ABD    </td><td>Veri    </td><td>10.1.2.11    </td><td>HK-c-aset-2    </td><td>DC WESTUS raf = rack4 =    </td><td>Hayır </td></tr>
<tr><td>HK-w1-Batı-ABD    </td><td>Web    </td><td>10.1.1.4    </td><td>HK-w-aset-1    </td><td>                       </td><td>Yok</td></tr>
<tr><td>HK-w2-Batı-ABD    </td><td>Web    </td><td>10.1.1.5    </td><td>HK-w-aset-1    </td><td>                       </td><td>Yok</td></tr>
</table>

Hello VM'lerin listesini yukarıda oluşturma işlemi aşağıdaki hello gerektirir:

1. Belirli bir bölgedeki bir boş bulut hizmeti oluşturma
2. Merhaba daha önce yakalanan görüntüden bir VM oluşturun ve daha önce oluşturduğunuz toohello sanal ağ ekleyin; Bu tüm hello VM'ler için yineleyin
3. Bir iç yük dengeleyici toohello bulut hizmeti ekleyin ve toohello "data" alt ağ ekleme
4. Daha önce oluşturduğunuz her VM için bir yük dengeli kümesi bağlı daha önce oluşturduğunuz toohello iç yük dengeleyici üzerinden thrift trafiği için bir yük dengeli uç noktası ekleme

Klasik Azure portalını kullanarak işlem yukarıda Hello çalıştırılabilir; Windows makine (kullanın) erişim tooa Windows makine yoksa Azure VM'de bir PowerShell komut dosyası tooprovision aşağıdaki hello tüm 8 sanal makineleri otomatik olarak kullanın.

**Listesi 1: PowerShell Betiği sanal makineleri sağlama**

        #Tested with Azure Powershell - November 2014
        #This powershell script deployes a number of VMs from an existing image inside an Azure region
        #Import your Azure subscription into hello current Powershell session before proceeding
        #hello process: 1. create Azure Storage account, 2. create virtual network, 3.create hello VM template, 2. crate a list of VMs from hello template

        #fundamental variables - change these tooreflect your subscription
        $country="us"; $region="west"; $vnetName = "your_vnet_name";$storageAccount="your_storage_account"
        $numVMs=8;$prefix = "hk-cass";$ilbIP="your_ilb_ip"
        $subscriptionName = "Azure_subscription_name";
        $vmSize="ExtraSmall"; $imageName="your_linux_image_name"
        $ilbName="ThriftInternalLB"; $thriftEndPoint="ThriftEndPoint"

        #generated variables
        $serviceName = "$prefix-svc-$region-$country"; $azureRegion = "$region $country"

        $vmNames = @()
        for ($i=0; $i -lt $numVMs; $i++)
        {
           $vmNames+=("$prefix-vm"+($i+1) + "-$region-$country" );
        }

        #select an Azure subscription already imported into Powershell session
        Select-AzureSubscription -SubscriptionName $subscriptionName -Current
        Set-AzureSubscription -SubscriptionName $subscriptionName -CurrentStorageAccountName $storageAccount

        #create an empty cloud service
        New-AzureService -ServiceName $serviceName -Label "hkcass$region" -Location $azureRegion
        Write-Host "Created $serviceName"

        $VMList= @()   # stores hello list of azure vm configuration objects
        #create hello list of VMs
        foreach($vmName in $vmNames)
        {
           $VMList += New-AzureVMConfig -Name $vmName -InstanceSize ExtraSmall -ImageName $imageName |
           Add-AzureProvisioningConfig -Linux -LinuxUser "localadmin" -Password "Local123" |
           Set-AzureSubnet "data"
        }

        New-AzureVM -ServiceName $serviceName -VNetName $vnetName -VMs $VMList

        #Create internal load balancer
        Add-AzureInternalLoadBalancer -ServiceName $serviceName -InternalLoadBalancerName $ilbName -SubnetName "data" -StaticVNetIPAddress "$ilbIP"
        Write-Host "Created $ilbName"
        #Add add hello thrift endpoint toohello internal load balancer for all hello VMs
        foreach($vmName in $vmNames)
        {
            Get-AzureVM -ServiceName $serviceName -Name $vmName |
                Add-AzureEndpoint -Name $thriftEndPoint -LBSetName "ThriftLBSet" -Protocol tcp -LocalPort 9160 -PublicPort 9160 -ProbePort 9160 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ilbName |
                Update-AzureVM

            Write-Host "created $vmName"     
        }

**3. adım: Her VM Cassandra yapılandırma**

VM Hello oturum ve hello aşağıdakileri yapın:

* Merkezi ve raf $CASS_HOME/conf/cassandra-rackdc.properties toospecify hello veri özelliklerini düzenleyin:
  
       dc =EASTUS, rack =rack1
* Cassandra.yaml tooconfigure çekirdek düğümleri aşağıdaki şekilde düzenleyin:
  
       Seeds: "10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10"

**4. adım: hello VM'ler başlatmak ve hello küme test etme**

Merhaba düğümlerden (örneğin hk-c1-Batı-us) günlüğüne ve çalışma hello komutu toosee hello hello küme durumunu izleyen:

       nodetool –h 10.1.2.4 –p 7199 status

Merhaba görüntü benzer toohello biri aşağıda bir 8 düğüm kümesi için görmeniz gerekir:

<table>
<tr><th>Durum</th><th>Adres    </th><th>Yükleme    </th><th>Belirteçler    </th><th>Sahibi </th><th>Ana bilgisayar kimliği    </th><th>Raf</th></tr>
<tr><th>KALDIRMA    </td><td>10.1.2.4     </td><td>87.81 KB    </td><td>256    </td><td>38.0%    </td><td>GUID (kaldırılır)</td><td>raf1</td></tr>
<tr><th>KALDIRMA    </td><td>10.1.2.5     </td><td>41.08 KB    </td><td>256    </td><td>68.9%    </td><td>GUID (kaldırılır)</td><td>raf1</td></tr>
<tr><th>KALDIRMA    </td><td>10.1.2.6     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>GUID (kaldırılır)</td><td>rack2</td></tr>
<tr><th>KALDIRMA    </td><td>10.1.2.7     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>GUID (kaldırılır)</td><td>rack2</td></tr>
<tr><th>KALDIRMA    </td><td>10.1.2.8     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>GUID (kaldırılır)</td><td>rack3</td></tr>
<tr><th>KALDIRMA    </td><td>10.1.2.9     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>GUID (kaldırılır)</td><td>rack3</td></tr>
<tr><th>KALDIRMA    </td><td>10.1.2.10     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>GUID (kaldırılır)</td><td>rack4</td></tr>
<tr><th>KALDIRMA    </td><td>10.1.2.11     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>GUID (kaldırılır)</td><td>rack4</td></tr>
</table>

## <a name="test-hello-single-region-cluster"></a>Test hello tek bölge kümesi
Aşağıdaki adımları tootest hello küme hello kullan:

1. Merhaba Powershell komutu Get-AzureInternalLoadbalancer komutunu kullanarak, hello iç yük dengeleyici hello IP adresi (örneğin Al  10.1.2.101). Merhaba komutun Hello sözdizimi aşağıda gösterilmektedir: Get-AzureLoadbalancer – [hello iç yük dengeleyici IP adresini birlikte hello ayrıntılarını görüntüler] ServiceName "hk-c-svc-Batı-us"
2. Merhaba web grubu VM (örneğin hk-w1-Batı-us) günlüğüne Putty kullanarak veya ssh
3. $CASS_HOME/bin/cqlsh 10.1.2.101 yürütme 9160
4. Merhaba küme çalışıyorsanız CQL komutları tooverify aşağıdaki hello kullan:
   
     İLE çoğaltma oluşturma KEYSPACE customers_ks = {'sınıfı': 'SimpleStrategy', 'replication_factor': 3};   Customers_ks; kullanın.   Tablo Customers(customer_id int PRIMARY KEY, firstname text, lastname text); oluşturma   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INSERT INTO Customers(customer_id, firstname, lastname) değerleri (2, 'Jane', 'Etikan');
   
     SEÇİN * MÜŞTERİLERDEN;

Hello gibi bir görüntü görmeniz gerekir:

<table>
  <tr><th> customer_id </th><th> FirstName </th><th> Soyadı </th></tr>
  <tr><td> 1 </td><td> John </td><td> Doe </td></tr>
  <tr><td> 2 </td><td> Jane </td><td> Doe </td></tr>
</table>

4. adımda oluşturduğunuz bu hello keyspace SimpleStrategy 3'ün bir replication_factor kullanır. Lütfen unutmayın. SimpleStrategy NetworkTopologyStrategy çok veri merkezi ancak dağıtımlar için tek bir veri merkezi dağıtımları önerilir. Replication_factor 3 düğümü hataları için dayanıklılık sunar.

## <a id="tworegion"></a>Bölgeli dağıtım işlemi
Merhaba tek bölge dağıtımı tamamlandı yararlanır ve hello ikinci bölge yüklemek için aynı işlemi hello yineleyin başlar. Merhaba anahtar arasındaki hello tek ve birden çok bölgede dağıtım hello VPN tüneli Kurulum arası bölge iletişimi için farktır; Biz başlatılır hello ağ yüklemesi ile hello VM'ler sağlamak ve Cassandra yapılandırın.

### <a name="step-1-create-hello-virtual-network-at-hello-2nd-region"></a>1. adım: hello sanal ağ hello oluşturma 2 bölge
Klasik Azure portalı Hello oturum ve hello öznitelikleri göster hello tablosundaki ile bir sanal ağ oluşturun. Bkz: [hello Klasik Azure portalı Cloud-Only sanal ağ yapılandırma](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md) hello işleminin ayrıntılı adımlar için.      

<table>
<tr><th>Öznitelik adı    </th><th>Değer    </th><th>Açıklamalar</th></tr>
<tr><td>Ad    </td><td>vnet-cass-Doğu-us</td><td></td></tr>
<tr><td>Bölge    </td><td>Doğu ABD</td><td></td></tr>
<tr><td>DNS sunucuları        </td><td></td><td>Bir DNS sunucusu kullanmıyorsanız gibi bu iletiyi yoksayın</td></tr>
<tr><td>Noktadan siteye VPN bağlantısını yapılandırma</td><td></td><td>        Bu iletiyi yoksayın</td></tr>
<tr><td>Siteden siteye VPN'yi yapılandırın</td><td></td><td>        Bu iletiyi yoksayın</td></tr>
<tr><td>Adres alanı    </td><td>10.2.0.0/16</td><td></td></tr>
<tr><td>Başlangıç IP    </td><td>10.2.0.0    </td><td></td></tr>
<tr><td>CIDR    </td><td>/16 (65531)</td><td></td></tr>
</table>

Alt ağları aşağıdaki hello ekleyin:

<table>
<tr><th>Ad    </th><th>Başlangıç IP    </th><th>CIDR    </th><th>Açıklamalar</th></tr>
<tr><td>Web    </td><td>10.2.1.0    </td><td>/24 (251)    </td><td>Merhaba web grubu için alt ağ</td></tr>
<tr><td>Veri    </td><td>10.2.2.0    </td><td>/24 (251)    </td><td>Merhaba veritabanı düğümleri için alt ağ</td></tr>
</table>


### <a name="step-2-create-local-networks"></a>2. adım: Yerel ağlar oluşturma
Azure sanal ağ yerel bir ağda tooa uzak site özel bir bulut ya da başka bir Azure bölgesi de dahil olmak üzere eşleyen bir proxy adresi alanıdır. Bu proxy adres alanı ilişkili tooa uzak yönlendirme ağ toohello sağ hedefleri ağ için ağ geçididir. Bkz: [VNet tooVNet bağlantı yapılandırma](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) VNET-VNET bağlantı kurarak hello hakkında yönergeler için.

Aşağıdaki ayrıntılara hello başına iki yerel ağlar oluşturun:

| Ağ adı | VPN ağ geçidi adresi | Adres alanı | Açıklamalar |
| --- | --- | --- | --- |
| HK-lnet-Map-to-East-us |23.1.1.1 |10.2.0.0/16 |Merhaba yerel ağ oluşturulurken bir yer tutucu ağ geçidi adresi verin. Merhaba ağ geçidi oluşturulduktan sonra hello gerçek ağ geçidi adresi girilir. Merhaba adres alanı olduğundan emin olun tam olarak eşleşen hello ilgili uzak VNET; Bu durumda hello VNET hello Doğu ABD bölgesinde oluşturulur. |
| HK-lnet-Map-to-West-us |23.2.2.2 |10.1.0.0/16 |Merhaba yerel ağ oluşturulurken bir yer tutucu ağ geçidi adresi verin. Merhaba ağ geçidi oluşturulduktan sonra hello gerçek ağ geçidi adresi girilir. Merhaba adres alanı olduğundan emin olun tam olarak eşleşen hello ilgili uzak VNET; Bu durumda hello VNET hello Batı ABD bölgesi oluşturulur. |

### <a name="step-3-map-local-network-toohello-respective-vnets"></a>3. adım: Eşleme "Yerel" Ağ toohello ilgili sanal ağları
Hello Klasik Azure portalı, her sanal ağ seçin, "Yapılandır"'ı tıklatın, "Bağlan toohello yerel ağ" denetleyin ve aşağıdaki ayrıntılara hello başına hello yerel ağlar seçin:

| Sanal Ağ | Yerel ağ |
| --- | --- |
| HK-vnet-Batı-ABD |HK-lnet-Map-to-East-us |
| HK-vnet-Doğu-us |HK-lnet-Map-to-West-us |

### <a name="step-4-create-gateways-on-vnet1-and-vnet2"></a>4. adım: Ağ geçitleri VNET1 ve vnet2'yi oluşturma
Her iki hello sanal ağlar Hello panodan oluşturmak hello VPN ağ geçidi sağlama işlemini tetikler ağ geçidi'ı tıklatın. Her sanal ağ Panosu birkaç dakika hello sonra hello gerçek ağ geçidi adresi görüntülemelidir.

### <a name="step-5-update-local-networks-with-hello-respective-gateway-addresses"></a>5. adım: Güncelleştirme "Yerel" ağlar hello ilgili "ağ geçidi" adresleri
Her iki hello yerel ağlar tooreplace hello yer tutucu ağ geçidi IP sağlanan adresi hello yalnızca hello gerçek IP adresi ile ağ geçidi düzenleyin. Eşleme aşağıdaki hello kullan:

<table>
<tr><th>Yerel ağ    </th><th>Sanal Ağ Geçidi</th></tr>
<tr><td>HK-lnet-Map-to-East-us </td><td>Ağ geçidi hk-vnet-Batı-ABD</td></tr>
<tr><td>HK-lnet-Map-to-West-us </td><td>Ağ geçidi hk-vnet-Doğu-ABD</td></tr>
</table>

### <a name="step-6-update-hello-shared-key"></a>6. adım: Güncelleştirme hello paylaşılan anahtar
PowerShell komut dosyası tooupdate hello IPSec anahtarı her VPN ağ geçidi [hello artırmak amacıyla anahtarı hem hello ağ geçitleri için kullanın] aşağıdaki kullanım hello: Set-AzureVNetGatewayKey - vnetname adlı hk-vnet-Doğu-us - LocalNetworkSiteName hk-lnet-map-to-west-us - SharedKey D9E76BKK Set-AzureVNetGatewayKey - vnetname adlı hk-vnet-Batı-us - LocalNetworkSiteName hk-lnet-map-to-east-us - SharedKey D9E76BKK

### <a name="step-7-establish-hello-vnet-to-vnet-connection"></a>7. adım: Merhaba VNET-VNET bağlantısı
Hello Klasik Azure Portalı ' hem hello sanal ağlar tooestablish ağ geçidi için ağ geçidi bağlantı hello "PANO" menüsünü kullanın. Merhaba "BAĞLAN" menü öğeleri hello alt kısımdaki araç kullanın. Birkaç dakika sonra hello Pano hello bağlantı ayrıntıları grafik görüntülemelidir.

### <a name="step-8-create-hello-virtual-machines-in-region-2"></a>8. adım: #2 bölgede hello sanal makineler oluşturma
Aynı adımlar veya #2 bölgede bulunan hello görüntü VHD dosyası toohello Azure depolama hesabı kopyalama aşağıdaki hello tarafından bölge #1 dağıtımı'nda açıklandığı gibi Hello Ubuntu görüntü oluşturabilir ve hello görüntü oluşturabilirsiniz. Bu görüntüyü kullanın ve yeni bir bulut hizmeti hk-c-svc-Doğu-us sanal makinelerin listesini aşağıdaki hello oluşturun:

| Makine adı | Alt ağ | IP Adresi | Kullanılabilirlik kümesi | DC/raf | Çekirdek? |
| --- | --- | --- | --- | --- | --- |
| HK-c1-Doğu-us |Veri |10.2.2.4 |HK-c-aset-1 |DC EASTUS raf = raf1 = |Evet |
| HK-c2-Doğu-us |Veri |10.2.2.5 |HK-c-aset-1 |DC EASTUS raf = raf1 = |Hayır |
| HK-c3-Doğu-us |Veri |10.2.2.6 |HK-c-aset-1 |DC EASTUS raf = rack2 = |Evet |
| HK-c5-Doğu-us |Veri |10.2.2.8 |HK-c-aset-2 |DC EASTUS raf = rack3 = |Evet |
| HK-c6-Doğu-us |Veri |10.2.2.9 |HK-c-aset-2 |DC EASTUS raf = rack3 = |Hayır |
| HK-c7-Doğu-us |Veri |10.2.2.10 |HK-c-aset-2 |DC EASTUS raf = rack4 = |Evet |
| HK-c8-Doğu-us |Veri |10.2.2.11 |HK-c-aset-2 |DC EASTUS raf = rack4 = |Hayır |
| HK-w1-Doğu-us |Web |10.2.1.4 |HK-w-aset-1 |Yok |Yok |
| HK-w2-Doğu-us |Web |10.2.1.5 |HK-w-aset-1 |Yok |Yok |

İzleme hello aynı bölge #1 olarak yönergeleri ancak 10.2.xxx.xxx adres alanı kullanın.

### <a name="step-9-configure-cassandra-on-each-vm"></a>9. adım: Her VM Cassandra yapılandırma
VM Hello oturum ve hello aşağıdakileri yapın:

1. $CASS_HOME/conf/cassandra-rackdc.properties toospecify hello veri merkezi ve raf özellikleri hello biçimde düzenleyin: dc EASTUS raf = raf1 =
2. Cassandra.yaml tooconfigure çekirdek düğümleri düzenleyin: oluştururken çekirdeği: "10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10,10.2.2.4,10.2.2.6,10.2.2.8,10.2.2.10"

### <a name="step-10-start-cassandra"></a>10. adım: Cassandra Başlat
Her bir VM oturum ve hello aşağıdaki komutu çalıştırarak hello arka planda Cassandra Başlat: $CASS_HOME/bin/cassandra

## <a name="test-hello-multi-region-cluster"></a>Test hello bölgeli küme
Artık her Azure bölgesi 8 düğümler ile dağıtılan too16 düğüm Cassandra olmuştur. Bu düğümler aynı hello ortak küme adı ve hello çekirdek düğüm yapılandırması, küme hello arasındadır. İşlem tootest hello küme aşağıdaki hello kullan:

### <a name="step-1-get-hello-internal-load-balancer-ip-for-both-hello-regions-using-powershell"></a>1. adım: hello iç yük dengeleyici IP PowerShell kullanarak her iki hello bölgeler için alın.
* Get-AzureInternalLoadbalancer - ServiceName "hk-c-svc-Batı-us"
* Get-AzureInternalLoadbalancer - ServiceName "hk-c-svc-Doğu-us"  
  
    Not hello IP adresleri (örneğin - 10.1.2.101, Doğu - Batı 10.2.2.101) görüntülenir.

### <a name="step-2-execute-hello-following-in-hello-west-region-after-logging-into-hk-w1-west-us"></a>2. adım: hello aşağıdakileri oturum hk-w1-Batı-us açtıktan sonra hello Batı bölgesinde yürütün
1. $CASS_HOME/bin/cqlsh 10.1.2.101 yürütme 9160
2. CQL komutları aşağıdaki hello yürütün:
   
     İLE çoğaltma oluşturma KEYSPACE customers_ks = {'sınıfı': 'NetworkToplogyStrategy', 'WESTUS': 3 'EASTUS': 3};   Customers_ks; kullanın.   Tablo Customers(customer_id int PRIMARY KEY, firstname text, lastname text); oluşturma   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INSERT INTO Customers(customer_id, firstname, lastname) değerleri (2, 'Jane', 'Etikan');   SEÇİN * MÜŞTERİLERDEN;

Hello gibi bir görüntü görmeniz gerekir:

| customer_id | FirstName | Soyadı |
| --- | --- | --- |
| 1 |John |Doe |
| 2 |Jane |Doe |

### <a name="step-3-execute-hello-following-in-hello-east-region-after-logging-into-hk-w1-east-us"></a>3. adım: oturum hk-w1-Doğu-us açtıktan sonra hello Doğu bölgede hello aşağıdakileri yürütün:
1. $CASS_HOME/bin/cqlsh 10.2.2.101 yürütme 9160
2. CQL komutları aşağıdaki hello yürütün:
   
     Customers_ks; kullanın.   Tablo Customers(customer_id int PRIMARY KEY, firstname text, lastname text); oluşturma   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INSERT INTO Customers(customer_id, firstname, lastname) değerleri (2, 'Jane', 'Etikan');   SEÇİN * MÜŞTERİLERDEN;

Aynı hello Batı bölge için görülen görüntülemek hello görmeniz gerekir:

| customer_id | FirstName | Soyadı |
| --- | --- | --- |
| 1 |John |Doe |
| 2 |Jane |Doe |

Birkaç daha fazla eklemeleri yürütün ve bu çoğaltılmış toowest görmek-bize hello kümenin parçası.

## <a name="test-cassandra-cluster-from-nodejs"></a>Test Cassandra Node.js kümeden
Merhaba "web" katmanında hello Linux VM'ler birini kullanarak daha önce crated, basit bir Node.js komut dosyası tooread önceden eklenen hello veri yürütülmez.

**1. adım: Node.js ve Cassandra istemcisi yükleme**

1. Node.js ve npm yükleme
2. Düğüm paketi "cassandra-istemci" yükleme npm kullanma
3. Alınan hello veri hello json dizesi görüntüleyen hello Kabuk isteminde komut dosyası izleyen hello yürütün:
   
        var pooledCon = require('cassandra-client').PooledConnection;
        var ksName = "custsupport_ks";
        var cfName = "customers_cf";
        var hostList = ['internal_loadbalancer_ip:9160'];
        var ksConOptions = { hosts: hostList,
                             keyspace: ksName, use_bigints: false };
   
        function createKeyspace(callback){
           var cql = 'CREATE KEYSPACE ' + ksName + ' WITH strategy_class=SimpleStrategy AND strategy_options:replication_factor=1';
           var sysConOptions = { hosts: hostList,  
                                 keyspace: 'system', use_bigints: false };
           var con = new pooledCon(sysConOptions);
           con.execute(cql,[],function(err) {
           if (err) {
             console.log("Failed toocreate Keyspace: " + ksName);
             console.log(err);
           }
           else {
             console.log("Created Keyspace: " + ksName);
             callback(ksConOptions, populateCustomerData);
           }
           });
           con.shutdown();
        }
   
        function createColumnFamily(ksConOptions, callback){
          var params = ['customers_cf','custid','varint','custname',
                        'text','custaddress','text'];
          var cql = 'CREATE COLUMNFAMILY ? (? ? PRIMARY KEY,? ?, ? ?)';
        var con =  new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) {
                 console.log("Failed toocreate column family: " + params[0]);
                 console.log(err);
              }
              else {
                 console.log("Created column family: " + params[0]);
                 callback();
              }
          });
          con.shutdown();
        }
   
        //populate Data
        function populateCustomerData() {
           var params = ['John','Infinity Dr, TX', 1];
           updateCustomer(ksConOptions,params);
   
           params = ['Tom','Fermat Ln, WA', 2];
           updateCustomer(ksConOptions,params);
        }
   
        //update will also insert hello record if none exists
        function updateCustomer(ksConOptions,params)
        {
          var cql = 'UPDATE customers_cf SET custname=?,custaddress=? where custid=?';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) console.log(err);
              else console.log("Inserted customer : " + params[0]);
          });
          con.shutdown();
        }
   
        //read hello two rows inserted above
        function readCustomer(ksConOptions)
        {
          var cql = 'SELECT * FROM customers_cf WHERE custid IN (1,2)';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,[],function(err,rows) {
              if (err)
                 console.log(err);
              else
                 for (var i=0; i<rows.length; i++)
                    console.log(JSON.stringify(rows[i]));
            });
           con.shutdown();
        }
   
        //exectue hello code
        createKeyspace(createColumnFamily);
        readCustomer(ksConOptions)

## <a name="conclusion"></a>Sonuç
Microsoft Azure tarafından bu alıştırmada gösterildiği gibi hem Microsoft, hem de açık kaynak yazılımının hello çalışmasını sağlayan esnek bir platformdur. Yüksek oranda kullanılabilir Cassandra kümeleri tek bir veri merkezi hello hello küme düğümlerinin birden çok hata etki alanlarında yayılmak üzerinden dağıtılabilir. Cassandra kümeleri de olağanüstü durum kanıtını sistemler için birden çok coğrafi olarak birbirinden uzak Azure bölgeleri üzerinden dağıtılabilir. Azure ve Cassandra birlikte etkinleştirir düzeyde ölçeklenebilir, yüksek oranda kullanılabilir yapımı hello ve olağanüstü durum kurtarılabilir bulut Hizmetleri tarafından bugünün internet Hizmetleri ölçeği.  

## <a name="references"></a>Başvurular
* [http://cassandra.apache.org](http://cassandra.apache.org)
* [http://www.datastax.com](http://www.datastax.com)
* [http://www.nodejs.org](http://www.nodejs.org)

