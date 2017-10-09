---
title: "aaaDesign Azure şablonları karmaşık çözümleri | Microsoft Docs"
description: "Karmaşık senaryolar için Azure Resource Manager şablonları tasarlamak için en iyi uygulamaları gösterir"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ce1141d6-ece7-4976-acea-1db1f775409e
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: aa45e9a46d79a6336b696cff8fd37f65fa449f11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-azure-resource-manager-templates-when-deploying-complex-solutions"></a>Karmaşık çözümleri dağıtımı sırasında Azure Resource Manager şablonları için Tasarım desenleri
Azure Resource Manager şablonları temel alarak esnek bir yaklaşım kullanarak karmaşık topolojiler hızlı ve tutarlı bir şekilde dağıtabilirsiniz. Bu dağıtımlar teklifleri gelişmesi çekirdek veya aykırı değer senaryoları veya müşteriler için tooaccommodate çeşitleri olarak kolayca uyarlayabilirsiniz.

Bu konuda daha büyük bir Teknik İnceleme bir parçasıdır. tam kağıt tooread hello karşıdan [World sınıfı Azure Resource Manager şablonları konuları ve kanıtlanmış yöntemler](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).

Şablonları hello uyumluluk ve okunabilirliği JavaScript nesne gösterimi (JSON) ile Azure Resource Manager temel hello hello yararları birleştirin. Şablonları kullanarak şunları yapabilirsiniz:

* Topolojileri ve yüklerini tutarlı bir şekilde dağıtın.
* Tüm kaynaklarınızı birlikte kaynak gruplarını kullanarak bir uygulama yönetin.
* Rol tabanlı erişim denetimi (RBAC) toogrant uygun erişim toousers, grupları ve Hizmetleri uygulayın.
* Toplamaları faturalama gibi etiketleme ilişkilendirmeleri toostreamline görevleri kullanın.

Bu makalede tüketim senaryoları, mimari ve bizim tasarım oturumlar ve gerçek şablonu uygulamaları Azure Müşteri danışma ekibi (AzureCAT) müşterilerle sırasında tanımlanan uygulama desenleri ayrıntıları sağlar. Merhaba geliştirme 12 hello üst Linux tabanlı OSS teknolojileri de dahil olmak üzere, şablonları tarafından haberdar yöntemler kanıtlanmış akademik gölgeden uzak Bu yaklaşımlar: Apache Kafka, Apache Spark, Cloudera, Couchbase, Hortonworks HDP, DataStax kuruluş tarafından sağlanmıştır Apache Cassandra, Elasticsearch, Jenkins, MongoDB, PostgreSQL, Redis ve Nagios. 

Bu makalede world sınıfı Azure Resource Manager şablonları mimari bu kanıtlanmış yöntemleri toohelp paylaşır.  

Müşteriler bizim iş birkaç Resource Manager şablonu kullanımı deneyimleri kuruluşlar, sistem tümleştiricileri (SI) s ve CSV arasında belirledik. Merhaba aşağıdaki bölümler yaygın senaryolar ve desenler üst düzey bir genel bakış için farklı müşteri türleri sağlar.

## <a name="enterprises-and-system-integrators"></a>Kuruluşlar ve sistem tümleştiricileri
Büyük kuruluşlar içinde biz sık Resource Manager şablonları iki tüketicileri bkz: İç yazılım geliştirme ekipleri ve kurumsal BT. Biz hello SIS hello senaryolarda kuruluşlar için toohello senaryoları eşleme buldunuz bunu hello ilgili noktaların aynısı geçerlidir.

### <a name="internal-software-development-teams"></a>İç yazılım geliştirme ekiplerinin
Ekibinizin iş yazılım toosupport geliştirir, şablonları tooquickly dağıtmak teknolojileri iş özgü çözümleri kullanmak için kolay bir yol sağlar. Şablonları da kullanabilirsiniz toorapidly takım üyeleri toogain gerekli becerilere etkinleştirmek eğitim ortamlar oluşturun.

Şablon olarak kullanabilirsiniz-genişletmek veya tooaccommodate oluşturan gereksinimlerinizi. İçinde şablonları etiketleme kullanarak, takım, proje, tek tek ve eğitim gibi çeşitli görünümlerle fatura özeti sağlayabilirsiniz.

İşletmeler genellikle bir çözümün tutarlı bir dağıtım için bir şablon toocreate yazılım geliştirme ekipleri istiyor. Bu ortam içinde belirli öğeleri sabit kalır ve geçersiz kılınamaz hello şablon kısıtlamaları kolaylaştırır. Örneğin, bir banka Programcı bankacılık çözüm gözden olamaz gerektirdiğinden şablonu tooinclude RBAC toosend veri tooa Kişisel depolama hesabı.

### <a name="corporate-it"></a>Kurumsal BT
Kurumsal BT kuruluşları bulut kapasite ve bulutta barındırılan özellikleri teslim etmek için şablonlar normalde kullanın.

#### <a name="cloud-capacity"></a>Bulut kapasitesi
Genel bir kurumsal BT grupları tooprovide bulut kapasitesi takımlar için "standart boyutları küçük, Orta gibi sunumu ve büyük olan ısı boyutlarına" yoludur. Merhaba boyutta ısı teklifleri farklı kaynak türleri ve miktarları olası toouse şablonları kolaylaştırır Standartlaştırma düzeyini sağlarken karıştırabilirsiniz. Hello şablonları kapasite şirket ilkelerini uygulamaya zorlar ve etiketleme tooprovide geri ödeme tooconsuming kuruluşlar kullanan tutarlı bir yol sunar.

Örneğin, tooprovide geliştirme, test ve üretim ortamlarında içinde hangi hello yazılım geliştirme ekipleri çözümleri dağıtabilirsiniz gerekebilir. Merhaba ortamını önceden tanımlanmış ağ topolojisine sahip ve erişim toohello ortak Internet ve paket incelemesi yöneten kuralları gibi yazılım geliştirme ekipleri hello öğeleri değişiklik yapamaz. Ayrıca bu ortamlar için kuruluşa özgü rolleri hello ortamı için birbirinden ayrı erişim haklarına sahip olabilir.

#### <a name="cloud-hosted-capabilities"></a>Bulutta barındırılan özellikleri
Bağımsız yazılım paketleri veya iş toointernal satırları sunulan bileşik teklifleri dahil olmak üzere şablonları toosupport bulutta barındırılan özellikleri kullanabilirsiniz. Hizmet olarak analytics bileşik sunumun bir örnek olabilir — analizi, Görselleştirme ve diğer teknolojiler — önceden tanımlanmış ağ topolojisini en iyi duruma getirilmiş ve bağlı bir yapılandırmasına sunulan.

Bulutta barındırılan yetenekleri hello güvenlik ve bunlar derlendiği sunumu hello bulut kapasitesi tarafından kurulan rol konuları etkilenir. Bu özellikler, olduğu gibi veya yönetilen bir hizmet olarak sunulur. İkinci Hello için erişim kısıtlı rolleri gerekli yönetim amacıyla hello ortamına tooenable erişim.

## <a name="cloud-service-vendors"></a>Bulut hizmeti satıcılar
Toomany csv görüştükten sonra müşteriler ve ilişkili gereksinimleri için toodeploy Hizmetleri gerçekleştirebileceğiniz birden çok yaklaşımlar belirledik.

### <a name="csv-hosted-offering"></a>CSV barındırılan teklifi
Kendi Azure aboneliğinizde teklifinizle barındırıyorsanız, iki barındırma yaklaşım ortaktır: her müşteri için ayrı bir dağıtım dağıtma veya tüm müşteriler için kullanılan bir paylaşılan altyapı destekleyen ölçek birimleri dağıtma.

* **Ayrı dağıtımları her müşteri için.** Ayrı dağıtımları her müşteri Sabit topolojiler farklı bilinen yapılandırmaları gerektirir. Bu dağıtımlar, başka bir sanal makine (VM) boyutları, değişen sayıda düğüm ve ilişkili depolama farklı miktarda olabilir. Etiketleme dağıtımları her müşteri dökümü faturalama için kullanılır. RBAC etkin tooallow müşteriler erişim tooaspects kendi bulut ortamı olabilir.
* **Ölçek birimleri paylaşılan çok kiracılı ortamlarda.** Bir şablon çok kiracılı ortamları için bir ölçek birimi temsil edebilir. Bu durumda, aynı alt hello kullanılan toosupport tüm müşterileri içindir. Merhaba dağıtımları barındırılan hello sunumu, kullanıcı sayısı ve işlem sayısı gibi kapasiteyi düzeyini teslim kaynakların bir grubu temsil eder. Bu ölçek birimleri artırılabilir veya isteğe bağlı gerektirdiği şekilde azaltılabilir.

### <a name="csv-offering-injected-into-customer-subscription"></a>Müşteri aboneliğini eklenen CSV teklifi
Son müşteriler tarafından ait abonelikleri içine yazılımınızı toodeploy isteyebilirsiniz. Bir müşterinin Azure hesaba şablonları toodeploy ayrı dağıtımları kullanabilirsiniz.

Güncelleştirme ve hello dağıtım hello müşterinin hesabına içinde yönetmek için bu dağıtımlar RBAC kullanın.

### <a name="azure-marketplace"></a>Azure Market
tooadvertise ve Teklifleriniz Azure Marketi gibi bir Market üzerinden satmak, müşterinin Azure hesabında çalıştırmak dağıtım türlerini şablonları toodeliver ayrı geliştirebilirsiniz. Bu ayrı dağıtımlar genellikle ısı boyutu (küçük, Orta, büyük), ürün/izleyici türü (topluluk, geliştirici, Kurumsal) veya özellik türünü (Basit, yüksek kullanılabilirlik) tanımlanabilir.  Bazı durumlarda toospecify izin bu tür VM türüne veya disk sayısı gibi hello dağıtım belirli öznitelikler.

## <a name="oss-projects"></a>OSS projeleri
Açık kaynak projeleri içinde Resource Manager şablonları topluluk toodeploy hızla kanıtlanmış yöntemleri kullanarak bir çözüm sağlar. Merhaba topluluk zamanla düzeltebilirsiniz şekilde şablonlar GitHub deposunda depolayabilir. Kullanıcıların bu şablonları kendi Azure abonelikleri dağıtın.

Merhaba aşağıdaki bölümlerde çözümünüzü tasarlamadan önce tooconsider gereken hello şeyler tanımlayın.

## <a name="identifying-what-is-outside-and-inside-a-vm"></a>Bir VM içinde ve dışında ne olduğunu tanımlama
Şablonunuzu tasarlarken, hello sanal makineleri (VM'ler) içinde ve dışında nedir bakımından hello gereksinimleri en yararlı toolook şöyledir:

* Dış VM'ler ve diğer kaynakları, dağıtımınızın hello ağ topolojisi, etiketleme, başvuruları toohello sertifikaları/parolalar ve rol tabanlı erişim denetimi gibi hello anlamına gelir. Tüm bu kaynaklar, şablonunuza bir parçasıdır.
* Durum yapılandırma Hello yazılımı yüklü ve genel istenen iç anlamına gelir. VM uzantıları veya komut dosyaları gibi diğer mekanizmaları tamamen veya kısmen kullanılır. Bu mekanizmaların tanımlanır ve hello şablon tarafından yürütülen ancak içinde değil.

"Hello kutu içinde" yaptığınız etkinlik ortak örnekler-  

* Yükleme veya sunucu rolleri ve özellikleri kaldırma
* Yazılımı yükleme ve başlangıç düğümü veya küme düzeyinde yapılandırma
* Bir web sunucusu üzerindeki Web siteleri dağıtma
* Veritabanı şemalarını dağıtma
* Kayıt defteri ya da başka tür yapılandırma ayarlarını yönetme
* Dosyaları ve dizinleri yönetin
* Başlatma, durdurma ve işlem ve hizmetleri yönetmek
* Yerel grupları ve kullanıcı hesaplarını yönetme
* Yükleme ve paketleri (.msi, .exe, yum, vb.) yönetme
* Ortam değişkenleri yönetme
* Yerel (Windows PowerShell, bash, vs.) komut dosyalarını çalıştır

### <a name="desired-state-configuration-dsc"></a>İstenen durum yapılandırması (DSC)
Merhaba iç Vm'leriniz dağıtım ötesinde durumuyla ilgili düşünüyorum, bu dağıtımın "tanımlanan ve kullanıma hello yapılandırmasından kaynak denetimine kayma değil" emin toomake istiyorsunuz. Bu yaklaşım, geliştiricilerin sağlar veya işlem personeli vetted, test, veya kaynak denetiminde kaydedilen geçici değişiklikleri tooan ortamı yapmayın. Merhaba el ile yapılan değişiklikler kaynak denetiminde olmadığı için bu denetim önemlidir. Bunlar ayrıca hello standart dağıtımının bir parçası değildir ve gelecekte otomatik dağıtımları hello yazılımın etkiler.

İç çalışanlarınızın istenen durum yapılandırması da güvenlik açısından önemlidir. Bilgisayar korsanlarının toocompromise düzenli olarak çalıştığınız ve yazılım sistemleri yararlanma. Başarılı olduğunda, ortak tooinstall dosyalar ve aksi durumda hello güvenliği aşılmış bir sistem durumunu değiştirin. İstenen durum Yapılandırması'nı kullanarak istenen hello Fiili durumu arasındaki farkları belirleyin ve bilinen yapılandırmasını geri yükleyin.

Merhaba en popüler mekanizmalar DSC - PowerShell DSC, Chef ve Puppet için kaynak uzantıları vardır. Bu uzantılar her hello ilk durumunda, VM dağıtabilir ve ayrıca kullanılan toomake durumu korunur hello istenen emin olun.

## <a name="common-template-scopes"></a>Ortak şablon kapsamları
Ortaya çıkan üç anahtar çözüm şablonları kapsamları deneyimi bizim gördük. Bu üç kapsamları – kapasite, yetenek ve uçtan uca çözüm – hello aşağıdaki bölümlerde açıklanmıştır.

### <a name="capacity-scope"></a>Kapasite kapsamı
Kapasite kapsam önceden yapılandırılmış toobe düzenlemeleri ve ilkeleri ile uyumlu olan standart topolojisinde kaynak kümesi sunar. Merhaba en yaygın örnek bir kurumsal BT veya SI senaryo standart geliştirme ortamında dağıtıyor.

### <a name="capability-scope"></a>Özellik kapsamı
Bir özellik kapsamı dağıtma ve belirli bir teknolojinin topolojisini yapılandırma odaklanmıştır. SQL Server'ı Cassandra, Hadoop gibi teknolojileri de dahil olmak üzere genel senaryoları.

### <a name="end-to-end-solution-scope"></a>Uçtan uca çözüm kapsamı
Bir uçtan uca çözüm kapsamını tek bir özellik hedeflenen ve bunun yerine birden çok yeteneklerini oluşan son tooend çözümünü teslim üzerinde odaklanmıştır.  

Bir çözüm kapsamlı şablon kapsamı bir veya daha fazla özellik kapsamlı şablonlarıyla çözüme özel kaynakları, mantığı ve istenen durumu kümesi olarak ortaya çıkmaktadır. Bir son tooend veri ardışık düzen çözüm şablonu çözüm kapsamlı bir şablon örnektir. Merhaba şablonu Kafka, Storm ve Hadoop gibi birden çok özellik kapsamlı çözüm şablonlarıyla çözüme özel topoloji ve durum karışımı.

## <a name="choosing-free-form-vs-known-configurations"></a>Serbest biçimli bilinen yapılandırmaları ve seçme
Bir şablon tüketicileri hello utmost esneklik, ancak birçok konuları hello seçim olup etkileyen başlangıçta düşünebilirsiniz toouse serbest biçimli yapılandırmaları bilinen yapılandırmaları karşılaştırması. Bu bölümde hello anahtar müşteri gereksinimlerine ve bu belgede paylaşılan hello yaklaşım şeklinde teknik konuları tanımlar.

### <a name="free-form-configurations"></a>Serbest biçimli yapılandırmaları
Merhaba yüzey üzerinde ideal serbest biçimli yapılandırmaları ses. Bunlar tooselect bir VM türüne izin ve rasgele bir düğümü sayısını sağlayın ve bu düğümler için diskleri ekli — ve bunu parametrelerinin tooa şablon olarak yapın. Ancak, bu yaklaşım bazı senaryolar için uygun değil.

İçinde [sanal makineler için Boyutlar](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)hello farklı VM türler ve kullanılabilir boyutları tanımlanır ve her dayanıklı hello sayısı (2, 4, 8, 16 veya 32), diskleri eklenebilir. Her bağlı disk 500 IOPS sağlar ve bu disklerin'ün katları IOPS bu sayının bir çarpanı havuza alınmış. Örneğin, 16 diskleri havuza alınmış tooprovide 8000 IOPS olabilir. Microsoft Windows depolama alanları veya pahalı olmayan (RAID) diskler yedek dizisi içinde Linux kullanarak hello işletim sistemi yapılandırmasına sahip havuzu yapılır.

Bir veya daha fazla tooconfigure hello VM içeriği komut dosyaları ve çeşitli VM türleri ve bu örneklerde, çeşitli diskler hello VM türü için boyutları hello seçimi serbest biçimli yapılandırması birkaç VM örnekleri sağlar.

Bu esneklik genellikle her düğüm türü için sağlanan şekilde bir dağıtım yöneticisi gibi düğümler ve veri düğümlerini birden çok tür olabilir yaygın bir durumdur.

Tüm anlamlı toodeploy kümeleri başlangıç olarak toowork bu karmaşık senaryolar ile başlar. Hadoop kümesi dağıtma, örneğin, 8 ana düğüm ve 200 veri düğümleri ve ana her düğümde havuza alınmış 4 ekli disk ve havuza alınmış 16 ekli disk başına veri düğümü ile 208 VM'ler ve 3,232 diskleri toomanage olurdu.

Bir depolama hesabı depolama hesabı bölümleme adresindeki arayın ve bu topoloji tooaccommodate toodetermine hello uygun sayıda depolama hesapları hesaplamalar kullanmanız gerekir böylece tanımlanan 20.000 işlemleri/saniye, sınırlamak istek yukarıdaki kısıtlama. Merhaba serbest biçimli yaklaşımı dinamik hesaplamalar desteklenen birleşimleri Hello çok sayıda verilen olan gerekli toodetermine hello uygun bölümleme. Bu hesaplamalar hello uygun ayrıntılarla benzersiz, sabit kodlanmış bir şablon oluşturma kodda, gerçekleştirmeniz gereken şekilde hello Azure Resource Manager şablonu dili matematik işlevleri, şu anda sağlamaz.

Kurumsal BT ve sı senaryoları, birisi hello şablonları korumak ve bir veya daha fazla kuruluşlar için dağıtılan hello topolojileri destekler. Bu ek yükü — farklı yapılandırmaları ve her bir müşteri için şablonlar — tercih gölgeden uzak olan.

Müşterinizin Azure aboneliğindeki bu şablonları toodeploy ortamları kullanabilirsiniz ancak kurumsal BT ekipleri ve CSV genellikle bunları kendi abonelikleri geri ödeme işlevi toobill kullanarak müşterilerine dağıtın. Bu senaryolarda hello toodeploy kapasite birden çok müşteri için abonelikleri ve canlı dağıtımları densely hello abonelikleri toominimize abonelik karmaşıklığını doldurulmuş havuzu genelinde hedeftir — diğer bir deyişle, daha fazla abonelik toomanage. Gerçekten dinamik dağıtım boyutlarıyla yoğunluğu bu tür elde dikkatli planlama ve ek geliştirme hello kuruluş adına askılama özelliğinin çalışması için gerektirir.

Ayrıca, bir API çağrısı aracılığıyla abonelikleri oluşturamazsınız ancak hello Portalı aracılığıyla el ile yapmanız gerekir. Abonelik Hello sayısı arttıkça, sonuçta ortaya çıkan tüm abonelik karmaşıklığını insan etkileşimi gerektirir — otomatik olamaz. Merhaba boyutlarda dağıtımlarını çok değişkenlik ile toopre sağlama abonelik sayısı el ile olurdu tooensure abonelikleri kullanılabilir.

Bu etkenler göz önünde bulundurularak bir gerçekten serbest biçimli en önce blush daha az çekici bir yapılandırmadır.

### <a name="known-configurations--hello-t-shirt-sizing-approach"></a>Yapılandırmaları bilinen — hello ısı boyutlandırma yaklaşımı
Bunun yerine toplam esneklik ve sayısız Çeşitlemeler sağlayan bir şablon teklif daha deneyimi bizim genel bir desen yapılandırmaları bilinen tooprovide hello özelliği tooselect olan — yürürlükte, küçük, Orta ve büyük sanal gibi standart ısı boyutları. Diğer ısı boyutları community edition veya enterprise edition gibi ürün teklifleri gösterilebilir.  Diğer durumlarda, harita azaltmak gibi iş yüküne özgü yapılandırmaları bir teknolojisi – olabilir veya hiç sql.

Birçok kuruluş BT kuruluşları, OSS satıcılar ve SIS tekliflerini kullanılabilir duruma bugün bu şekilde şirket içi, sanallaştırılmış ortamlarda (kuruluşların) veya hizmet olarak yazılım (SaaS) tekliflerini (csv ve OSVs).

Bu yaklaşım, müşteri için yapılandırılmış farklı boyutlarda iyi, bilinen yapılandırmaları sağlar. Bilinen yapılandırmaları son müşterilere gerekir küme boyutlandırma kendi başlarına belirlemek, platform kaynak kısıtlamaları faktörü ve depolama hesapları ve diğer kaynakları (son toocluster boyutu ve kaynak bölümleme matematik tooidentify hello kaynaklanan yapın kısıtlamaları). Yapılandırmaları etkinleştirmek müşteriler tooeasily select hello sağ ısı boyutu bilinen — diğer bir deyişle, belirli bir dağıtım. Ayrıca toomaking hello müşteri için daha iyi bir deneyim, bir küçük sayısı bilinen yapılandırmaları daha kolay toosupport ve yoğunluğu daha yüksek düzeyde sunmanıza yardımcı olabilir.

Isı boyutlarına odaklanmış bir bilinen yapılandırma yaklaşım değişen bir boyutu dahilindeki düğümlerin sayısını da sahip olabilirsiniz. Örneğin, bir küçük ısı boyutu 3 ve 10 düğümler arasında olabilir.  Hello ısı boyutu too10 düğümleri yukarı tasarlanmış tooaccommodate olması ve ancak tüketici hello özelliği toomake serbest biçimli seçimler tanımlanan toohello en büyük boyutu ayarlama hello sunar.  

İş yükü türüne göre bir ısı boyutu yapısı hello dağıtılabilir ancak iş yükü ayrı düğüm boyutu ve hello yazılımının yapılandırmasını hello düğümde sahip düğüm sayısı bakımından daha fazla serbest biçimli olabilir.

Topluluk veya kuruluş olabilir ayrı kaynak türleri ve dağıtılabilir, düğüm sayısı üst sınırı gibi ürün teklifleri üzerinde temel ısı boyutları genellikle toolicensing konuları veya Özellik kullanılabilirliği hello farklı teklifleri bağlı.

Merhaba JSON tabanlı şablonlar kullanarak benzersiz çeşitleri olan müşteriler de barındırabilir. Aykırı değerlerini ile ilgilenirken, hello uygun planlama ve geliştirme, destek ve maliyeti konuları dahil edebilirsiniz.

Hello Müşteri şablon tüketim senaryoları ve bu belgenin hello başlangıcında tanımlanan gereksinimler temelinde, şablon ayrıştırma için bir örüntü belirledik.

## <a name="capacity-and-capability-scoped-solution-templates"></a>Kapasite ve yetenek kapsamlı çözüm şablonları
Ayrıştırma yeniden, test ve tooling genişletilebilirlik destekleyen bir modüler yaklaşım tootemplate geliştirme sağlar. Bu bölümde, bir ayrıştırma yaklaşım kapasite ya da özellik kapsamlı uygulanan tootemplates nasıl olabilir ayrıntı sağlar.

Bu yaklaşım ana şablon şablon tüketiciden parametre değerlerini alır ve ardından aşağıda gösterildiği gibi şablonları ve komut dosyalarının tooseveral türleri aşağı bağlar. Parametreler, statik değişkenler ve oluşturulan değişkenleri bağlı hello şablonları ve kullanılan tooprovide değerlerdir.

![Şablon parametreleri](./media/best-practices-resource-manager-design-templates/template-parameters.png)

**Tooa ana şablon sonra toolinked şablonları parametreleri aktarıldı**

Şablonlar ve tek bir şablon içine ayrılmış betikleri hello türlerinde bölümleri odak aşağıdaki hello. Merhaba bölümleri durum bilgilerini hello şablonları arasında geçirme yaklaşımları sunar. Her şablon ve hello komut dosyası türlerini hello görüntüsündeki örnekleri ile birlikte açıklanmaktadır. Bağlamsal bir örnek için bkz: "araya getirilmesi: örnek uygulama" belgesinde.

### <a name="template-metadata"></a>Şablon meta verileri
Şablon meta verilerine (Merhaba metadata.json dosyası) insanlar ve yazılım sistemleri tarafından okunabilir JSON şablonunda tanımlayan anahtar/değer çiftleri içerir.

![Şablon meta verileri](./media/best-practices-resource-manager-design-templates/template-metadata.png)

**Şablon meta verilerine hello metadata.json dosyasında tanımlanan**

Yazılım aracılarının hello metadata.json dosyasını alın ve bir web sayfası veya dizinde hello bilgileri ve bağlantı toohello şablonu yayımlayın. Öğeleri dahil *ItemDisplayName*, *açıklama*, *Özet*, *githubUsername*, ve *dateUpdated*.

Bir örnek dosyası tamamının aşağıda gösterilmiştir.

    {
        "itemDisplayName": "PostgreSQL 9.3 on Ubuntu VMs",
        "description": "This template creates a PostgreSQL streaming-replication between a master and one or more slave servers each with 2 striped data disks. hello database servers are deployed into a private-only subnet with one publicly accessible jumpbox VM in a DMZ subnet with public IP.",
        "summary": "PostgreSQL stream-replication with multiple slave servers and a publicly accessible jumpbox VM",
        "githubUsername": "arsenvlad",
        "dateUpdated": "2015-04-24"
    }

### <a name="main-template"></a>Ana şablon
Hello ana şablon parametreleri bir kullanıcıdan alır, bu bilgileri toopopulate karmaşık nesne değişkenlerini kullanır ve bağlı hello şablonları yürütür.

![Ana şablon](./media/best-practices-resource-manager-design-templates/main-template.png)

**Merhaba ana şablon parametreleri bir kullanıcıdan alır.**

Sağlanan bir bilinen yapılandırma türü olarak da bilinen hello ısı boyutu parametresi nedeniyle standartlaştırılmış değerlerini gibi küçük, Orta veya büyük parametresidir. Uygulamada, bu parametre birden çok yolla kullanabilirsiniz. Ayrıntılar için bu belgenin sonraki bölümlerinde "bilinen yapılandırma kaynakları şablonu" konusuna bakın.

Bazı kaynaklar hello bilinen yapılandırma kullanıcı parametresi tarafından belirtilen bağımsız olarak dağıtılır. Bu kaynakları tek paylaşılan kaynak şablonu kullanılarak sağlanır ve hello paylaşılan kaynak şablonu ilk çalıştırma için diğer şablonları tarafından paylaşılır.

Bazı kaynaklar isteğe bağlı olarak hello belirtilen bilinen yapılandırma bağımsız olarak dağıtılır.

### <a name="shared-resources-template"></a>Paylaşılan kaynaklar şablonu
Bu şablon tüm bilinen yapılandırmalar arasında ortak olan kaynaklar sunar. Merhaba sanal ağ, kullanılabilirlik kümeleri ve dağıtılan hello bilinen yapılandırma şablonu bağımsız olarak gereken diğer kaynakları içerir.

![Şablon kaynakları](./media/best-practices-resource-manager-design-templates/template-resources.png)

**Paylaşılan kaynaklar şablonu**

Merhaba sanal ağ adı gibi kaynak adları hello ana şablona dayalı olarak. Bunları, kuruluşunuzun gerektirdiği şekilde hello kullanıcıdan bir parametre olarak almak veya bunları bu şablonu içindeki bir değişken olarak belirtin.

### <a name="optional-resources-template"></a>İsteğe bağlı kaynakları şablonu
Merhaba isteğe bağlı kaynakları şablon program aracılığıyla dağıtılan hello değerine göre bir parametre veya değişken kaynakları içerir.

![İsteğe bağlı kaynaklar](./media/best-practices-resource-manager-design-templates/optional-resources.png)

**İsteğe bağlı kaynakları şablonu**

Örneğin, bir isteğe bağlı kaynakları şablonu tooconfigure hello dağıtılan tooa ortamından dolaylı erişim sağlayan bir jumpbox kullanabileceğiniz genel Internet. Merhaba jumpbox etkinleştirilmesi gerekip gerekmediğini bir parametre veya değişken tooidentify kullanırsınız ve hello *concat* hello şablonu için toobuild hello hedef adı gibi işlev *jumpbox_enabled.json*. Şablon Bağlama hello sonuç değişken tooinstall hello jumpbox kullanırsınız.

Merhaba isteğe bağlı kaynakları birden fazla yerde şablondan bağlayabilirsiniz:

* Geçerli tooevery dağıtım hello paylaşılan kaynakları şablondan parametre tabanlı bir bağlantı oluşturun.
* Zaman yapılandırmaları bilinen geçerli tooselect — Örneğin, yalnızca büyük dağıtımlarında yükleyin — hello bilinen yapılandırma şablondan parametre tabanlı veya değişken güdümlü bir bağlantı oluştur.

Belirli bir kaynak isteğe bağlı olup hello şablon tüketici tarafından ancak bunun yerine hello şablon sağlayıcı tarafından yönlendirilen değil. Örneğin, belirli ürün gereksinim veya ürün eklenti (ortak csv) veya tooenforce ilkeleri toosatisfy gerekebilir (SIS ve kurumsal BT için yaygın grupları). Bu durumlarda, Hello kaynak dağıtılmalıdır olup olmadığını değişken tooidentify kullanabilirsiniz.

### <a name="known-configuration-resources-template"></a>Bilinen yapılandırma kaynakları şablonu
Merhaba ana şablonunda, bir parametre gösterilen tooallow hello şablon tüketici toospecify istenen bilinen yapılandırma toodeploy olabilir. Genellikle, bilinen bu yapılandırmayı sabit yapılandırma boyutları gibi korumalı alan, küçük, Orta ve büyük bir dizi ısı boyutu yaklaşımı kullanır.

![Yeni yapılandırma kaynakları](./media/best-practices-resource-manager-design-templates/known-config.png)

**Bilinen yapılandırma kaynakları şablonu**

Hello ısı boyutu yaklaşım yaygın olarak kullanılır, ancak herhangi bir bilinen yapılandırmaları kümesi hello parametreleri temsil edebilir. Örneğin, ortam geliştirme, Test ve ürün gibi kurumsal uygulama için bir dizi belirtebilirsiniz. Veya bir bulut hizmeti toorepresent için farklı kullanabilir ölçek birimleri, ürün sürümleri veya topluluk, geliştirici veya Enterprise gibi ürün yapılandırmaları.

Merhaba paylaşılan kaynak şablonuyla'de olduğu gibi değişkenleri toohello bilinen yapılandırmaları şablon herhangi birinden geçirilir:

* Bir son kullanıcı — diğer bir deyişle, hello parametreleri toohello ana şablon gönderilen.
* Bir kuruluş — diğer bir deyişle, iç gereksinimleri ve ilkeleri temsil eden hello ana şablon değişkenleri hello.

### <a name="member-resources-template"></a>Üye kaynakları şablonu
İçinde bilinen bir yapılandırma, bir veya daha fazla üye düğüm türleri genellikle dahil edilir. Örneğin, Hadoop ile ana düğüm ve veri düğümlerini vardır. MongoDB yüklüyorsanız, veri düğümlerini ve bir arbiter sahip. DataStax dağıtıyorsanız, veri düğümlerini ve yüklü OpsCenter'yle bir VM'yi sahip.

![Üye kaynakları](./media/best-practices-resource-manager-design-templates/member-resources.png)

**Üye kaynakları şablonu**

Her düğüm türünü VM'ler, bağlı diskler, komut dosyaları tooinstall sayıda farklı boyutlarda ve hello düğümleri, hello VM'ler için bağlantı noktası yapılandırmaları, örneklerinin sayısını ve diğer ayrıntılarını ayarlayın. Her düğüm türü kendi alır şekilde hello içeren üye kaynak şablonu dağıtma ve bir altyapının yanı sıra komut dosyaları toodeploy yürütme ayrıntıları ve yazılım hello VM içinde yapılandırın.

VM'ler için genellikle iki komut dosyaları kullanılan, yaygın olarak yeniden kullanılabilir ve özel komut dosyaları türleridir.

### <a name="widely-reusable-scripts"></a>Yaygın olarak yeniden kullanılabilir komut dosyaları
Yaygın olarak yeniden kullanılabilir komut dosyaları birden çok şablon türlerini kullanılabilir. Bu yaygın bir şekilde yeniden kullanılabilir komut dosyaları hello daha iyi örneklerinden birini Linux toopool disklerde RAID ayarlar ve daha fazla sayıda IOPS elde. Hello VM yüklenen hello yazılım bağımsız olarak bu komut dosyası için genel senaryolar kanıtlanmış yöntemleri kullanılmasını sağlar.

![Yeniden kullanılabilir komut dosyaları](./media/best-practices-resource-manager-design-templates/reusable-scripts.png)

**Üye kaynakları şablonları yaygın olarak yeniden kullanılabilir komut dosyaları çağırabilirsiniz**

### <a name="custom-scripts"></a>Özel komut dosyaları
Şablonları sık vm'lerde yazılımı yükleme ve yapılandırma bir veya daha fazla komut dosyalarını arayın. Genel bir desen bir veya daha fazla üye türleri birden çok örneğini dağıtıldığı büyük topolojileri ile görülür. Paralel olarak çalışan her VM için bir yükleme komut dosyası başlatılan tüm sanal makineleri (veya belirtilen üye türündeki tüm VM'ler) dağıtıldıktan sonra çağrılan bir kurulum komut dosyası tarafından izlenen.

![Özel komut dosyaları](./media/best-practices-resource-manager-design-templates/custom-scripts.png)

**Üye kaynakları şablonları VM yapılandırması gibi belirli bir amaç için komut dosyaları çağırın**

## <a name="capability-scoped-solution-template-example---redis"></a>Yetenek kapsamlı bir çözüm şablonu örnek - Redis
tooshow uygulaması çalışabilir nasıl bakalım pratik örneği hello dağıtım ve standart ısı boyutları Redis yapılandırmasında kolaylaştıran bir şablon oluşturma sırasında.  

Merhaba dağıtım için bir dizi paylaşılan kaynakları (sanal ağ, depolama hesabı, kullanılabilirlik kümeleri) ve isteğe bağlı bir kaynak (jumpbox) vardır. Isı boyutları (küçük, Orta, büyük) temsil birden çok bilinen yapılandırmaları vardır, ancak her tek bir düğüm ile yazın. İki amaca özel komut dosyaları (yükleme, yapılandırma) vardır.

### <a name="creating-hello-template-files"></a>Şablon dosyalarını Hello oluşturma
Azuredeploy.json adlı bir ana şablon oluşturursunuz.

Paylaşılan kaynaklar paylaşılan resources.json adlı şablonu oluşturma

Bir isteğe bağlı kaynak şablonu tooenable hello dağıtımını jumpbox_enabled.json adlı bir jumpbox oluşturun

Üye kaynak düğüm resources.json adlı tek bir şablon oluşturmak için redis yalnızca bir tek düğümlü türü kullanır.

Redis ile tek tek her düğüm tooinstall istediğiniz ve ardından hello kümesi.  Komut dosyaları tooaccommodate hello yükleme ve, redis küme install.sh ve redis küme setup.sh ayarlayın.

### <a name="linking-hello-templates"></a>Merhaba şablonları bağlama
Şablon bağlama kullanarak, hello ana şablon hello sanal ağ oluşturur toohello paylaşılan kaynakları şablonu kullanıma, bağlar.

Bir jumpbox dağıtılmalıdır olup olmadığını mantığı hello ana şablon tooenable tüketicileri hello şablonu toospecify içinde eklenir. Bir *etkin* hello için değer *EnableJumpbox* parametre, o hello Müşterinin istediği toodeploy bir jumpbox belirtir. Bu değer sağlandığında hello şablonunu art arda ekler *_enabled* hello jumpbox özelliği için bir sonek tooa temel şablonu adı olarak.

Merhaba ana şablonu geçerli hello *büyük* parametre değeri ısı boyutları ve ardından kullanımlar için soneki tooa temel şablonu adı olarak bir şablon bağlantı değeri çok*technology_on_os_large.json*.

Bu çizim Hello topoloji benzeyecektir.

![Şablon redis](./media/best-practices-resource-manager-design-templates/redis-template.png)

**Bir Redis şablonu için şablon yapısı**

### <a name="configuring-state"></a>Yapılandırma durumu
Merhaba kümedeki düğümlerin Merhaba, tooconfiguring hello durumu iki adımı vardır, her ikisi de amacı belirli komut dosyaları tarafından temsil edilen.  Redis "redis-küme-install.sh" yükler ve "redis-küme-setup.sh" Merhaba küme ayarlar.

### <a name="supporting-different-size-deployments"></a>Farklı boyutu dağıtımları destekleme
Değişkenleri hello ısı boyutu şablon hello her tür düğüm sayısını belirtir. toodeploy hello için belirtilen boyut (*büyük*). Ardından bu kaynak döngüleri sayısal sıra numarasına sahip bir düğüm adı eklenerek benzersiz adlar tooresources sağlama kullanarak VM örneklerinin sayısını dağıtır *copyındex ()*. Her iki veya çalışmıyorken bölge VM'ler için şu adımları hello ısı adı şablonunda tanımlandığı şekilde mevcut

## <a name="decomposition-and-end-to-end-solution-scoped-templates"></a>Ayrıştırma ve uçtan uca çözüm şablonları kapsamı
Uçtan uca çözüm kapsamlı bir çözüm şablonu bir uçtan uca çözüm sunduğunuzdan üzerinde odaklanmıştır.  Bu yaklaşım genellikle birden çok özellik kapsamlı Şablonları ek kaynaklar, mantığı ve durum ile oluşan bir bileşimdir.

Vurgulanmış olarak hello resimde, hello kapsamlı yetenek şablonları için kullanılan aynı modelin bir uçtan uca çözüm kapsamlı şablonları için genişletilir.

Paylaşılan kaynaklar şablon ve isteğe bağlı kaynakları şablonları hello kapasite ve yetenek olduğu gibi aynı işlevi şablon yaklaşımlar kapsamlı ancak hello son tooend çözüm için kapsamlı hello işlevi görür.

Son tooend çözüm kapsamlı olarak şablonları de genellikle ısı boyutları olabilir, bilinen hello çözüm yapılandırması verilen için gerekli nedir hello bilinen yapılandırma kaynakları şablonu yansıtır.

Merhaba bilinen yapılandırma kaynakları şablonu bağlantılar tooone veya daha fazla özelliği ilgili toohello son tooend çözüm gibi hello hello son tooend çözümü için gerekli olan bir üye kaynak şablonları çözüm şablonları kapsamlı.

Hello ısı hello çözüm boyutunu hello tek tek özellik kapsamlı şablonu farklı şekilde hello bilinen yapılandırma kaynakları şablonu değişkenler kullanılan tooprovide hello uygun aşağı akış özelliği kapsamı çözümünü değerler Şablonları toodeploy hello uygun ısı boyutu.

![Uçtan uca](./media/best-practices-resource-manager-design-templates/end-to-end.png)

**kapasiteyi Hello modeli kullanılan veya kapsamlı yetenek çözüm şablonları son tooend çözüm şablonu kapsamlar için kolayca genişletilebilir**

## <a name="preparing-templates-for-hello-marketplace"></a>Şablonları Market hello için hazırlama
yaklaşım taşımalarına önceki hello kuruluşlar, SIS ve CSV istediğiniz tooeither hello şablonları kendilerini dağıttığınız veya kendi müşteriler toodeploy kendi başlarına etkinleştirmek olduğu senaryolar düzenler.

Başka bir istenen senaryo hello Market üzerinden bir şablon dağıtıyor.  Bu ayrıştırma yaklaşım de hello Market bazı küçük değişikliklerle çalışır.

Daha önce belirtildiği gibi şablonları kullanılan toooffer farklı dağıtım türleri hello Market satışı olabilir. Farklı dağıtım türleri ısı boyutları (küçük, Orta, büyük), ürün/izleyici türü (topluluk, geliştirici, Kurumsal) ya da özellik türünü (Basit, yüksek kullanılabilirlik) olabilir.

Son tooend varolan aşağıda gösterilen hello çözüm ya da kapsamlı şablonları kolayca olabilir yetenek toolist hello farklı bilinen yapılandırmalarında hello Market kullanılan.

Merhaba parametreleri toohello ana şablon ilk değiştirildiğinde tooremove hello tshirtSize adlı gelen parametre.

Merhaba farklı dağıtım türleri toohello bilinen yapılandırma kaynakları şablonu eşleme, ayrıca ihtiyaç duydukları hello ortak kaynakları ve yapılandırma bulunan paylaşılan kaynakları şablonu ve potansiyel olarak isteğe bağlı kaynak şablonları de hello.

Şablon toohello Market toopublish istiyorsanız, farklı kopyalarını hello tshirtSize tooa değişkenin kullanılabilir gelen parametre hello şablonda katıştırılmış önceden yerini alır, ana şablon oluşturun.

![Market](./media/best-practices-resource-manager-design-templates/marketplace.png)

**Şablon hello Market için kapsamlı bir çözüm uyarlama**

## <a name="next-steps"></a>Sonraki adımlar
* toolearn içine ve dışına şablonları, durumu paylaşma hakkında bkz [Azure Resource Manager şablonları durumda paylaşımı](best-practices-resource-manager-state.md).
* Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).

