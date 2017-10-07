---
title: "Azure üzerinde aaaIntroduction toomicroservices | Microsoft Docs"
description: "Bir genel bakış neden mikro yaklaşım ile bulut uygulamaları derleme modern uygulama geliştirme için önemlidir ve nasıl Azure Service Fabric platform tooachieve bu sağlar."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: fae2be85-0ab4-4cd3-9d1f-e0d95fe1959b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell
ms.openlocfilehash: b11920b9105e7575390e8fcf0d1ef6ab3c632978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="why-a-microservices-approach-toobuilding-applications"></a>Neden bir mikro toobuilding uygulamaları yaklaşımını?
Yazılım geliştiricileri yoktur nasıl bir uygulama bileşeni parçalara Finansman hakkında düşünüyoruz içinde yeni bir şey. Bunu hello merkezi nesne yönü, yazılım soyutlamalar ve temsilinde bir örnektir. Günümüzde, bu factorization tootake hello form sınıflar ve arabirimler paylaşılan kitaplıklar ve teknoloji katmanlar arasında eğilimi gösterir. Genellikle, katmanlı bir yaklaşım bir arka uç depolama, Orta katmanda iş mantığı ve bir ön uç kullanıcı arabirimi (UI) ile alınır. Ne *sahip* biz geliştiriciler oluşturmakta olduğunuz son birkaç yıl içinde hello değiştirilmiş olan dağıtılmış hello bulut için olan uygulamaları ve hello iş tarafından yönlendirilen.

Merhaba değişen iş gereksinimleri şunlardır:

* Yerleşik olarak bulunur ve ölçek tooreach müşterilerin yeni coğrafi bölgelerde adresindeki (örneğin) çalışır bir hizmet.
* Özellik ve yetenekler toobe mümkün toorespond toocustomer taleplerini Çevik bir şekilde daha hızlı teslimini.
* Geliştirilmiş kaynak kullanımı tooreduce maliyetleri.

Bu iş ihtiyaçları etkileyen *nasıl* biz uygulamaları oluşturun.

Azure toomicroservices hello yaklaşımı hakkında daha fazla bilgi için okuma [mikro: hello bulut tarafından desteklenen bir uygulama revolution](https://azure.microsoft.com/blog/microservices-an-application-revolution-powered-by-the-cloud/).

## <a name="monolithic-vs-microservice-design-approach"></a>Tek yapılı mikro hizmet tasarım yaklaşımı karşılaştırması
Zaman içinde tüm uygulamaları geliştirin. Yararlı toopeople olma yoluyla başarılı uygulamaları geliştirin. Başarısız uygulamalar değil gelişmesi ve sonunda kullanım dışı bırakılmıştır. Merhaba soru olur: ne kadar gereksinimleriniz hakkında bugün biliyor musunuz ve bunlar hello gelecekteki ne olacağını? Örneğin, bir bölüm için bir raporlama uygulaması oluşturduğunuzu varsayalım. Merhaba uygulaması, şirketinizin hello kapsamı içinde kalmasını ve hello raporları kısa süreli emin misiniz? Tercih ettiğiniz yaklaşımın söyleyin, farklıdır, müşterilerin milyonlarca video içerik tootens sunan bir hizmet oluşturma. 

Bildiğiniz hello uygulama daha sonra tasarlanması ancak bazı durumlarda, kavram kanıtı olarak hello kapı çıkışı erişmesini hello yönlendirmeli, faktördür. Hiçbir zaman kullanılan bir şey aşırı mühendislik içinde çok az noktası yoktur. Merhaba normal mühendislik dengelemeyi kullanıcının. Üzerinde şirketler Hello bulut, hello Beklenti büyüme ve kullanım için yapı hakkında konuşurken diğer yandan hello. Merhaba büyüme ve ölçek öngörülemeyen bir sorundur. Toobe mümkün tooprototype hızlı bir yolu toodeal gelecekteki başarı ile üzerindeki duyuyoruz da bilerek isteriz. Bu hello yalın başlangıç yaklaşımdır: oluşturma, ölçmek, öğrenin ve yineleme.

Merhaba istemci-sunucu dönemi sırasında her katmanında belirli teknolojileri kullanarak katmanlı uygulamaları derleme üzerinde toofocus tended. Merhaba terim *tek yapılı* uygulama için bu yaklaşım ortaya çıktı. Merhaba arabirimleri hello katmanları arasında toobe tended ve daha sıkı şekilde bağlı tasarım her katman içinde bileşenler arasındaki kullanıldı. Geliştiriciler tasarlanmış ve kitaplıklara derlenmiş ve birkaç yürütülebilir dosyaları ve DLL'ler birbirine sınıfları oluşturmak. 

Tek yapılı bir tasarım yaklaşımı avantajları toosuch vardır. Genellikle daha basit toodesign olur ve bu çağrıları genellikle işlemler arası iletişim (IPC) olduğundan bileşenleri arasında daha hızlı çağrıları vardır. Ayrıca, herkesin toobe daha fazla kişi-kaynak verimli eğilimlidir tek bir ürün sınar. Merhaba dezavantajı, katmanlı katmanlar arasında sıkı bir ilişki yoktur ve bileşenleri tek tek ölçeği olamaz ' dir. Tooperform düzeltmeleri veya yükseltmeler gereksinim toowait başkaları için varsa toofinish kendi test etme. Çevik daha zor toobe olur.

Bu downsides mikro adres ve daha yakından iş gereksinimlerini önceki hello ile Hizala, ancak ayrıca avantajları ve Borçları vardır. mikro Hello avantajları, her biri genellikle yukarı veya aşağı, test ölçeklendirme, dağıtmak ve bağımsız olarak yönetirsiniz daha basit iş işlevselliğini yalıtır ' dir. Mikro hizmet yaklaşımın önemli avantajı takımlar daha iş senaryolarını tarafından katmanlı yaklaşımın hello teknolojisiyle güdümlü biri önerir. Uygulamada, daha küçük ekipleri müşteri senaryoyu temel mikro hizmet geliştirin ve tercih ettikleri teknolojileri kullanır. 

Diğer bir deyişle, hello kuruluş toostandardize teknik toomaintain mikro hizmet uygulamaları gerekmez. Tek tek ekipler kendi Hizmetleri ne takım uzmanlık göre için mantıklı veya en uygun toosolve hello sorun ne yapabilirsiniz. Uygulamada, belirli bir NoSQL gibi önerilen teknoloji depolayan veya web uygulama çerçevesi, tercih edilir.

mikro Hello dezavantajı, artan hello sayısı ayrı varlıkları ve daha karmaşık dağıtımlar ve sürüm oluşturma postalarla yönetilmesindeki gelir. Merhaba karşılık gelen ağ gecikmeleri yanı sıra hello mikro arasındaki ağ trafiğini artırır. Çok sayıda chatty, ayrıntılı Hizmetleri performans onarımı kabus için tarif ' dir. Bu bağımlılıklar araçları toohelp görüntülemek, çok "Merhaba tüm sisteme bkz" sabit. 

Standartları tarafından iş hello mikro hizmet yaklaşım olun kabul ettiğinizi belirten nasıl toocommunicate ve yalnızca hello şey dayanıklı katı sözleşmeleri yerine bir hizmet ihtiyacınız üzerinde. Güncelleştirme Hizmetleri diğer bağımsız olarak bu sözleşmelere Önden hello tasarım, önemli toodefine demektir. Mikro yaklaşımı tasarlama "ayrıntılı hizmet odaklı mimari (SOA)." için de başka bir açıklaması

***En basit haliyle, hello mikro tasarım yaklaşımı hizmetlerinin bağımsız değişiklikleri tooeach ve anlaşılan standartları ile iletişim için ayrılmış bir Federasyon hakkındadır.***

Daha fazla bulut uygulamalarını üretilen, kişiler, bulabilir bu ayrıştırma Merhaba genel bağımsız, senaryo odaklı Hizmetleri uygulamaya daha iyi uzun vadeli bir yaklaşımdır.

## <a name="comparison-between-application-development-approaches"></a>Uygulama Geliştirme yaklaşımları karşılaştırması
![Service Fabric platform uygulama geliştirme][Image1]

1) Tek yapılı bir uygulama etki alanına özgü işlevselliği içeriyor ve normal web, iş ve veriler gibi işlev Katmanlar bölünür.

2) Birden çok sunucu/sanal makinelerde kopyalanarak tek yapılı bir uygulama ölçeklendirme/kapsayıcıları.

3) Mikro hizmet uygulaması ayrı küçük Hizmetleri işlevsellik ayırır.

4) Merhaba dağıtarak out mikro yaklaşım ölçekler her bağımsız olarak sunucuları/sanal makinelerde hizmetlerin örneklerini oluşturmaya hizmet/kapsayıcıları.

Mikro hizmet ile tasarlama yaklaşım panacea tüm projeleri için değil, ancak daha önce açıklanan hello iş hedeflerini daha yakından hizalayın. Tek yapılı bir yaklaşım ile başlayarak, hello fırsat toorework hello koda daha sonra mikro tasarım gerekir biliyorsanız, kabul edilebilir olabilir. Daha yaygın olarak, tek yapılı bir uygulama ile başlar ve daha ölçeklenebilir veya Çevik toobe gereken hello işlevsel ile başlangıç aşamasında, yavaş bölün.

toosummarize, hello mikro hizmet yaklaşımdır toocompose uygulamanızın veya çok sayıda küçük Hizmetleri. Makine bir kümede dağıtılan kapsayıcılarında Hello Hizmetleri çalıştırın. Küçük ekipleri senaryoyu odaklanan bir hizmeti geliştirmek ve test bağımsız olarak sürüm, dağıtmak ve böylece hello tüm uygulama gelişmesi her hizmet ölçeği.

## <a name="what-is-a-microservice"></a>Bir mikro hizmet nedir?
Mikro farklı tanımlarını vardır. Merhaba Internet arama yaparsanız, kendi görüşlerini ve tanımları sağlayan çok sayıda kullanışlı kaynaklar bulabilirsiniz. Ancak, mikro özelliklerini aşağıdaki hello çoğunu yaygın olarak üzerinde anlaşmaya varılan:

* Bir müşteriyi veya iş senaryosu kapsüller. Merhaba sorun çözme nedir?
* Küçük mühendislik ekibi tarafından geliştirilmiştir.
* Birinde yazılmış programlama dili ve tüm framework kullanın.
* (İsteğe bağlı) durum her ikisi de dağıtılır ve ölçeklendirilmiş bağımsız olarak sürümlü ve kodu oluşur.
* Diğer mikro ile iyi tanımlanmış arabirimleri ve protokolleri etkileşimde bulunur.
* Benzersiz adlar (URL) tooresolve konumlarını kullandınız.
* Tutarlı ve hataları hello varlığını kullanılabilir kalır.

Bu özelliklere içine özetlemek:

***Mikro hizmet uygulamaları iyi tanımlanmış arabirimlerle standart protokoller üzerinden birbirleri ile iletişim kuran küçük, bağımsız olarak sürümlü ve ölçeklenebilir müşteri odaklı hizmetler oluşur.***

Biz hello bölüm önceki hello ilk iki zaman noktası ele ve üzerinde genişletin ve açıklamak artık başkalarının hello.

### <a name="written-in-any-programming-language-and-use-any-framework"></a>Birinde yazılmış programlama dili ve tüm framework kullanın
Geliştiriciler, size ücretsiz toochoose, bizim becerileri veya hello hello hizmet gereksinimlerine bağlı olarak istiyoruz bir dil veya framework olmalıdır. Bazı hizmetler, sonraki tüm başka C++ hello performans yararlarını değeri. Diğer hizmetler, C# veya Java yönetilen geliştirme kolaylığı hello en önemli olabilir. Bazı durumlarda, toouse belirli iş ortağı kitaplığı veri depolama teknolojisi gerekebilir veya service tooclients gösterme anlamına gelir hello.

Bir teknoloji seçtikten sonra toohello işlemsel veya yaşam döngüsü yönetimi ve hello hizmeti ölçeklendirme gelir.

### <a name="allows-code-and-state-toobe-independently-versioned-deployed-and-scaled"></a>Kodu ve durum toobe bağımsız olarak sürümlü dağıtılır ve ölçeklendirilmiş sağlar
Mikro, hello kodunuz ve isteğe bağlı olarak hello durumu toowrite ancak tercih bağımsız olarak dağıtma, yükseltme ölçekleme ve. Teknolojileri tooyour seçimine geldiğinden bu gerçekte hello daha zor sorunlar toosolve biridir. Ölçeklendirme için nasıl toopartition (veya parça) hem de kodu ve durum hello anlamak zor olabilir. Hello kodu ve durum bugün yaygın bir durumdur, ayrı teknolojiler kullandığınızda, mikro hizmet için dağıtım betikleri hello her ikisinin de ölçeklendirme yapabilir toocope toobe gerekir. Merhaba mikro bazıları tooupgrade gerek kalmadan yükseltebilmek için aynı zamanda çevikliği ve esnekliği, hakkında budur tümünün aynı anda.

Toohello mikro hizmet yaklaşım karşı tek yapılı bir süre döndürme, hello Aşağıdaki diyagramda hello yaklaşım toostoring durumda hello farklar gösterilmektedir.

#### <a name="state-storage-between-application-styles"></a>Uygulama stilleri arasında durum depolama
![Service Fabric platform durumu depolama][Image2]

***Merhaba tek yapılı yaklaşım hello sol taraftaki tek bir veritabanı ve belirli teknolojileri katmanlarını vardır.***

***Merhaba mikro yaklaşımın hello sağ üzerinde bir grafiğini burada durumu genellikle kapsamlı toohello mikro hizmet ve kullanılan çeşitli teknolojiler birbirine mikro vardır.***

Tek yapılı bir yaklaşım Merhaba uygulaması genellikle tek bir veritabanı kullanır. Merhaba avantajı kolay toodeploy kolaylaştırır tek bir konum olmasıdır. Her bileşen tek tablo toostore durumuna sahip olabilir. Takımlar zor olduğu toostrictly ayrı durumu gerekir. Kaçınılmaz olarak vardır temptations tooadd yeni bir sütun tooan varolan müşteri tablosu, tablolar arasında birleştirme yapın ve bağımlılıkları hello depolama katmanında oluşturun. Bu gerçekleştikten sonra tek bileşenlerin ölçeklendirme olamaz. 

Merhaba mikro yaklaşımda, her bir hizmet yöneten ve kendi durumu depolar. Her hizmet, hem kod hem de durum birlikte toomeet hello taleplerini hello hizmetinin ölçekleme için sorumludur. Bir gereksinim toocreate olduğunda olan bir dezavantajı görünümleri ya da sorgular, uygulamanızın verilerinin farklı durumu mağazada tooquery gerekir. Genellikle, bu görünüm mikro koleksiyonunda derlemeler ayrı bir mikro hizmet sağlayarak çözülür. Merhaba verileri birden çok hazırlıksız sorgu tooperform ihtiyacınız varsa, her mikro veri kendi tooa veri ambarı hizmeti çevrimdışı analiz için yazma düşünmelisiniz.

Sürüm oluşturma sürümüdür belirli toohello dağıtılan bir mikro hizmet bu nedenle bu birden çok farklı sürümlerini dağıtma ve yan yana çalıştırma. Sürüm oluşturma adresleri bir mikro hizmet, yeni bir sürümünü yükseltme sırasında başarısız olduğu ve tooroll geri tooan gereken hello senaryolar önceki sürümü. Merhaba diğer senaryo sürüm oluşturma için A/B-style sınama, burada hello hizmeti farklı sürümlerini farklı kullanıcılar deneyimi gerçekleştiriyor. Örneğin, bunu daha yaygın olarak çalışırken önce ortak tooupgrade mikro hizmet müşteriler tootest yeni işlevsellik belirli bir dizi için olur. Mikro yaşam döngüsü yönetimi sonra bunu şimdi bize aralarında toocommunication getirir.

### <a name="interacts-with-other-microservices-over-well-defined-interfaces-and-protocols"></a>İyi tanımlanmış arabirimleri ve protokolleri diğer mikro ile etkileşim
Merhaba son 10 yılda yayımlanan hizmet odaklı mimari hakkında kapsamlı belgeleri iletişim düzenleri açıkladığı için bu konuda burada az kontrol edilmesi gerekiyor. Genellikle, hizmet iletişimi bir REST yaklaşım HTTP ve TCP protokollerini ve XML veya JSON ile hello seri hale getirme biçimi kullanır. Arabirim açısından bakıldığında, bu hello web tasarım yaklaşımı benimsemenin hakkında olur. Ancak hiçbir şey, ikili protokolleri veya kendi veri biçimleri kullanarak durdurur. Kişiler toohave için açık yayımlanmaması varsa, mikro kullanarak daha zor bir kez hazır olun.

### <a name="has-a-unique-name-url-used-tooresolve-its-location"></a>Benzersiz bir ad (URL) tooresolve konumunu kullandı
Nasıl biz hello mikro hizmet yaklaşım gibi hello web olduğunu söyleyen tutmak hatırlıyor? Çalıştığı her yerde hello web gibi mikro hizmet toobe adreslenebilir gerekir. Makineler hakkında düşünüyor ve hangisinin belirli mikro hizmet çalıştırıyorsa şeyler hızla hatalı gidin. 

Hello aynı şekilde bu DNS belirli URL tooa belirli bir makine çözümler, böylece geçerli konumuna bulunabilir olduğundan, mikro hizmet toohave benzersiz bir ad gerekiyor. Mikro bunlar çalıştıran hello altyapısından bağımsız duruma adreslenebilir adları olması gerekir. Bu çünkü hizmetinizin nasıl dağıtıldığını ve nasıl bulunduğundan, arasındaki etkileşim olduğunu gelir toobe hizmet kayıt defteri gerekir. Bir makine başarısız olduğunda, eşit, hello kayıt defteri hizmeti, hello hizmeti şimdi çalıştığı bildirmeniz gerekir. 

Bu bize toohello sonraki konuyu getirir: esnekliği ve tutarlılık.

### <a name="remains-consistent-and-available-in-hello-presence-of-failures"></a>Tutarlı ve hataları hello varlığını kullanılabilir kalır
Beklenmeyen hatalar postalarla hello en zor sorunlar toosolve, özellikle dağıtılmış bir sistemde biridir. Biz geliştiricileri de yazma hello kod çoğunu özel durumları işleme ve bu da burada hello çoğu testinde harcanan zaman. Merhaba sorun toohandle hataları kod yazmaktan daha karmaşıktır. Merhaba mikro çalıştığı hello makine başarısız olduğunda ne olur? Yalnızca bu mikro hizmet hatası (sabit kendi başına bir sorun) toodetect gerekir, ancak bir şey de gerek toorestart, mikro hizmet. 

Bir mikro hizmet toobe dayanıklı toofailures gerekir ve genellikle başka bir makinede kullanılabilirlik nedenlerle yeniden başlatın. Bu da aşağı hello mikro hizmet adına hello mikro hizmet bu durumdan kurtarabilir ve hello mikro mümkün toorestart başarıyla olup kaydedilmiş toohello durumu gelir. Diğer bir deyişle, toobe esnekliği hello işlem (Merhaba işlem yeniden başlatma) içinde ve aynı zamanda esnekliği hello durumu (hiçbir veri kaybı ve hello verileri tutarlı kalır) verileri de gerekir.

dayanıklılık Hello sorunları zaman uygulama yükseltme sırasında hatalar meydana gibi diğer senaryolar sırasında araya geldiğinde. Merhaba Merhaba dağıtım sistemiyle çalışma mikro toorecover gerekmez. Ayrıca toothen gerekir, toomove İleri toohello daha yeni sürüm devam edebilir veya bunun yerine tooa önceki sürüm toomaintain tutarlı bir duruma geri olup olmadığını karar verin. Sorular gibi yetecek sayıda makine ilerleyen kullanılabilir tookeep ve nasıl hello mikro önceki sürümlerini toorecover kabul toobe gerek olup olmadığı. Bu, bu kararların hello mikro hizmet tooemit sistem durumu bilgileri toobe mümkün toomake gerektirir.

### <a name="reports-health-and-diagnostics"></a>Raporları durum ve tanılama
Açıktır, görünebilir ve genellikle atlamış, ancak bir mikro hizmet, durum ve tanılama raporu gerekir. Aksi takdirde işlemleri açısından biraz Insight yoktur. Tanılama Olayları kümesi bağımsız Hizmetleri ve makine saat eğriltir hello olayı sırası toomake duygusu zor postalarla boyunca birleştiriliyor. Merhaba, üzerinde anlaşılan protokolleri ve veri mikro hizmet ile etkileşim aynı şekilde biçimleri, vardır, sorgulama ve görüntülemek için nasıl toolog sistem durumu ve sonuçta olayda şunun tanılama olayları depolamak içinde standartlaştırma gereksinimi görünür. İsteğe bağlı olarak bir mikro yaklaşım anahtarı olan farklı ekipler'in tek günlük biçimi kabul etmiş olursunuz. Tutarlı bir yaklaşım tooviewing tanılama olayları bir bütün olarak hello uygulamada toobe gerekir.

Sistem durumu tanılama farklıdır. Sistem durumu, geçerli durumu tootake uygun eylemlerini raporlama hello mikro hizmet hakkında ' dir. İyi bir örnek, yükseltme ve dağıtım mekanizmaları toomaintain kullanılabilirlik ile çalışmaktadır. Bir hizmet tooa işlem kilitlenme şu anda sağlam veya yeniden başlatma makine rağmen hello hizmet işletimsel olabilir. gereksinim duyduğunuz hello son şey yükseltme gerçekleştirerek bu daha da kötüsü toomake olduğu. Merhaba en iyi yaklaşımdır toodo bir araştırma ilk veya hello mikro hizmet toorecover için zaman tanıyın. Bir mikro hizmet sistem durumu olayları bilinçli kararlar almanıza ve etkili, kendini onarma hizmetleri oluşturmanıza yardımcı yardımcı olur.

## <a name="service-fabric-as-a-microservices-platform"></a>Service Fabric mikro platform olarak
Azure Service Fabric Microsoft tarafından bir geçiş gelen stili, toodelivering Hizmetleri genellikle tek yapılı kutusunu ürünleri teslim ortaya çıktı. derleme ve Azure SQL Database ve Azure Cosmos DB şeklinde Service Fabric gibi büyük Hizmetleri işletim hello deneyimi. Bu daha da fazla Hizmetleri benimsenen gibi hello platform zamanla gelişen. Önemlisi, Service Fabric yalnızca azure'da aynı zamanda tek başına Windows Server dağıtımları toorun vardı.

***Service Fabric Hello amacı oluşturma ve bir hizmeti çalıştıran hello sabit sorunları toosolve olduğunu ve böylece takımlar mikro yaklaşımı kullanarak iş sorunlarını çözebilir altyapı kaynaklarını verimli bir şekilde kullanma biçimleridir.***

Service Fabric sağlayan üç mikro yaklaşım kullanan uygulamalar oluşturmak ve geniş alanlara toohelp:

* Sistem Hizmetleri toodeploy sağlayan bir platform yükseltme, algılamak, başarısız hizmetlerini yeniden başlatın, hizmetleri bulmak, iletileri yönlendirmek, durumunu yönetme ve durumunu izleyin. Bu sistem hizmetleri yürürlükte birçok daha önce açıklanan mikro hello özelliklerini etkinleştirin.
* Özelliği toodeploy uygulamaları ya da çalışan kapsayıcılar veya olarak işler. Service Fabric bir kapsayıcı ve işlem orchestrator ' dir.
* Üretken programlama API'leri, uygulamaları mikro olarak yapı toohelp: [ASP.NET Core, Reliable Actors ve güvenilir hizmetler](service-fabric-choose-framework.md). Tüm kod toobuild, mikro hizmet seçebilirsiniz. Ancak bu API'leri hello iş daha kolay hale getirin ve daha ayrıntılı bir düzeyde hello platform tümleştirileceğini. Bu şekilde, örneğin, durum ve tanılama bilgileri elde edebilirsiniz veya yerleşik yüksek kullanılabilirlik yararlanabilir.

***Service Fabric hizmetinizin nasıl oluşturulacağına bağımsızdır ve herhangi bir teknoloji kullanabilirsiniz. Ancak, daha kolay toobuild mikro olun yerleşik programlama API'ler sağlar.***

### <a name="migrating-existing-applications-tooservice-fabric"></a>Var olan uygulamaları tooService doku geçirme
Anahtar yaklaşım tooService doku sonra ile yeni mikro modernized tooreuse var olan kodu ' dir. Tooapplication modernization beş aşama vardır ve başlatma ve herhangi bir hello aşamaları sırasında durdurma. Bunlar;

1) Geleneksel tek yapılı uygulamayı yap
2) Kaldırın ve Shift - kapsayıcıları veya konuk yürütülebilir dosyalar toohost var olan kodu Service Fabric kullanın.
3) Modernization - yeni mikro yanı sıra var olan kapsayıcılı kodu eklendi. 
4) Yenilik - başlangıç zamanıyla ilgili gereksinimleri temelinde mikro içine tek yapılı bölün.
5) Mikro - tek yapılı uygulamaları mevcut veya yeni greenfield uygulamaları derleme hello dönüştürme dönüştürüldüğünde.

![Geçiş tooMicroservices][Image3]

Yapabileceğiniz önemli tooemphasis yeniden olan **başlatmak ve durdurmak bu aşamalar hiçbirini**, yerel Yönetici değilseniz toomoved toohello sonraki aşamaya mecbur. Şimdi örnekler her Bu aşamalar için bakalım.

**Kaldırın ve Shift** - çok sayıda şirketler kaldırma ve kapsayıcıları toofor tek yapılı uygulamalarınız kaydırma iki nedenleri;

- Maliyet azaltma ya da son tooconsolidation ve daha yüksek yoğunluk mevcut donanım ya da çalışan uygulamaları kaldırma. 
- Geliştirme ve işlemler arasında tutarlı bir dağıtım sözleşme.

Maliyet azaltması anlaşılabilir ve Microsoft içinde çok sayıda mevcut uygulamaları yükleniyor yalnızca toomillions Doları kapsayıcılı. Eşit oranda önemli ancak daha zor tooevaluate tutarlı dağıtımıdır. Geliştiricileri yine olduğunu söylüyor ücretsiz toochoose hello teknolojisi bu paketleri olması bunları ancak hello işlemleri yalnızca tek bir yolu toodeploy kabul etmek ve bu uygulamaları yönetme. Birçok farklı teknolojiler hello karmaşıklığını ile toodeal sahip gelen hello işlemlerini azaltır veya geliştiricilerin tooonly zorlama belirli olanları seçin. Temelde her uygulamanın kendi içinde bulunan dağıtım görüntülere kapsayıcılı.

Birçok kuruluş burada durdurun. Zaten sahip oldukları Merhaba kapsayıcılara avantajları ve Service Fabric dağıtım, yükseltmeler, sürüm oluşturma, alma, sistem durumu izleme vb. hello tam yönetim deneyimi sağlar.

**Modernization** -varolan kapsayıcılı kodu yanı sıra yeni hizmetleri hello ektir. Toowrite yeni kod kullanacaksanız, en iyi toodecide tootake küçük adımları hello mikro yoldan var. Bu, yeni REST API uç noktası veya yeni bir iş mantığı ekleme. Bu şekilde, üzerinde yeni mikro hizmetler oluşturma ve uygulama geliştirme ve bunları dağıtma hello gezisine başlatın.

**Yenilik** -hello mikro yaklaşım yürüten bu özgün değişen iş gereksinimlerini hello başlangıç bu makalenin unutmayın? Bu aşama hello karardır, bunlar oluşmasını toomy geçerli uygulama ve bu durumda, bölme hello monolith veya innovating toostart gerekir. Bir iş akışı sırası olarak kullanılmakta olduğundan bir veritabanı işleme tıkanıklık olduğunda burada örneğidir. İş akışı Hello sayıda hello artırma istekleri için ölçek dağıtılmış gereksinimlerini toobe çalışır. Bu nedenle bu belirli parçası değil, ölçeklendirme Merhaba uygulaması veya için daha sık, bu çıkışı mikro hizmet bölme ve yenilik tooupdate gerekir. 

**Mikro dönüştürülmüş** -Bu, uygulamanızın tümüyle oluştuğundan, (veya içine ayrıştırılmış) olduğu mikro. Burada tooreach, hello mikro gezisine yaptınız. Burada, toodo Bu mikro platform toohelp başlatabilirsiniz önemli yatırım değil. 

### <a name="are-microservices-right-for-my-application"></a>Mikro sağ Uygulamam için misiniz?
Olabilir. Biz ne yaşadığı toobuild iş nedenleri hello bulut için Microsoft daha da fazla ekiplerde başlangıcından gibi bunların çoğu, mikro hizmet benzeri yaklaşımı hello avantajları gerçekleşen oluştu. Bing, örneğin, arama yıllık mikro geliştirme. Diğer ekipler için hello mikro yaklaşım yeni. Takımlar sabit sorunları toosolve gücü kendi çekirdek alanları dışında kayıt bulundu. Service Fabric hizmetleri oluşturmak için tercih ettiğiniz hello teknoloji olarak traction kazanılan nedeni budur.

Service Fabric Hello amacı tooreduce hello karmaşıklık mikro hizmet yaklaşımı uygulamaları oluşturma, böylece aracılığıyla toogo olarak olmayan birçok pahalı redesigns. Küçük başlayın, ölçeklendirme gerektiğinde, hizmetleri itiraz etme, yenilerini ekleyin ve gelişmesi müşteriyle kullanım hello yaklaşımdır. Çoğu geliştiricileri için fazla ulaşılabilirdir toomake mikro toobe Çözüldü henüz birçok diğer sorunlar olduğunu biliyoruz. Kapsayıcılar ve hello aktör programlama modeli bu yönde küçük adımları örnekleri ve size daha fazla yenilikleri toomake bu ortaya çıkacaktır olduğundan eminseniz daha kolay.
 
<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Sonraki adımlar
* [Service Fabric terminolojisi genel bakış](service-fabric-technical-overview.md)
* [Mikro: hello bulut tarafından desteklenen bir uygulama devrim](https://azure.microsoft.com/en-us/blog/microservices-an-application-revolution-powered-by-the-cloud/)

[Image1]: media/service-fabric-overview-microservices/monolithic-vs-micro.png
[Image2]: media/service-fabric-overview-microservices/statemonolithic-vs-micro.png
[Image3]: media/service-fabric-overview-microservices/microservices-migration.png
