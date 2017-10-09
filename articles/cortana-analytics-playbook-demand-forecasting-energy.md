---
title: "İsteğe bağlı enerji tahmin için Intelligence çözüm şablonu Playbook aaaCortana | Microsoft Docs"
description: "Bir çözüm şablonu ile Microsoft Cortana Intelligence'de, isteğe bağlı bir enerji yardımcı şirket için tahmini yardımcı olur."
services: cortana-analytics
documentationcenter: 
author: ilanr9
manager: ilanr9
editor: yijichen
ms.assetid: 8855dbb9-8543-45b9-b4c6-aa743a04d547
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2016
ms.author: ilanr9;yijichen;garye
ms.openlocfilehash: 32fc6ece7e24ced34282baf107548039694a38b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-template-playbook-for-demand-forecasting-of-energy"></a>İsteğe bağlı enerji tahmin için Cortana Intelligence çözüm şablonu Playbook
## <a name="executive-summary"></a>Yönetici Özeti
Merhaba birkaç yılda, nesnelerin interneti (IOT) geçmiş alternatif enerji kaynakları ve büyük veri toocreate büyük fırsatlar hello yardımcı programı ve enerji etki alanında birleştirilmiş. Merhaba aynı zamanda, hello yardımcı programı ve hello tüm enerji kesim enerji kullanımını daha iyi şekilde toocontrol yoğun tüketicileri düzleştirme tüketim gördünüz. Bu nedenle, yardımcı programı ve akıllı kılavuz şirketler harika gerek tooinnovate ve kendilerini yenileme hello. Ayrıca, birçok gücü ve yardımcı Kılavuzlar süresi dolmuş ve çok yüksek maliyetli toomaintain gelmektedir ve yönetin. Geçen yıl Hello sırasında hello takım katılımlar hello enerji etki alanı içindeki bir dizi çalışmakta olduğu. Hangi hello yardımcı programları veya ISV (bağımsız yazılım satıcıları) gelecekteki enerji talebi tahmin içine arayan çoğu durumda bu katılımlar sırasında karşılaştık. Bu tahminleri kendi güncel ve gelecekteki iş önemli bir rol oynar ve çeşitli kullanım örnekleri için hello foundation oldunuz. Bunlar kısa ve uzun vadeli güç yük tahmin, ticaret, Yük Dengeleme, kılavuz iyileştirme vb. içerir. Büyük veri ve Gelişmiş Analytics (AA) yöntemleri Machine Learning (ML) gibi hello anahtar etkinleştiricilerden doğru ve güvenilir tahminleri üretmek için durumdadır.  

Bu playbook biz hello iş ve analitik yönergeleri başarılı bir geliştirme için gereken bir araya getirin ve çözüm enerji talep dağıtımını tahmin. Bu önerilen yönergeleri, yardımcı programlar, veri bilimcilerine ve tam olarak kullanıma hazır hale getirilmiş, bulut tabanlı, isteğe bağlı tahmin çözümleri oluşturma, veri mühendisleri yardımcı olabilir. Yalnızca kendi büyük veri ve gelişmiş analizler gezisine başlangıç şirketler için bu tür bir çözüm, uzun vadeli akıllı kılavuz strateji ilk projeksiyondaki hello temsil edebilir.

> [!TIP]
> Bu şablon mimari bir genel bakış sağlayan bir diyagram toodownload bkz [isteğe bağlı enerji tahmin Cortana Intelligence çözüm şablonu mimarisi](cortana-analytics-architecture-demand-forecasting-energy.md).  
> 
> 

## <a name="overview"></a>Genel Bakış
Bu belge hello iş, veri ve Cortana Intelligence kullanma ve içinde belirli Azure Machine Learning (AML) hello uygulama ve enerji tahmin çözümleri dağıtımı için teknik unsurlarınızın kapsar. Merhaba belge üç ana bölümden oluşur:  

1. Kurumsal yaklaşım  
2. Veri anlama  
3. Teknik uygulama

Merhaba **iş anlama** bölümü anahatları iş en boy bir gereksinimlerini toounderstand hello ve yatırım karar önceki toomaking göz önünde bulundurun. Bunu nasıl tooqualify hello problemini Tahmine dayalı analiz ve makine öğrenme gerçekten etkili ve geçerli el tooensure adresindeki açıklanmaktadır. Daha fazla Hello belge hello temelleri machine learning ve nasıl kullanılan tooaddress enerji tahmin sorunlar olduğunu açıklar. Merhaba önkoşulları ve kullanım hello niteliği ölçütünü özetlenmektedir. Bazı örnek senaryolar da sağlanır durumları ve iş durumu kullanın.

Çözüm öğrenme herhangi bir makine için ana tarifi hello verilerdir. Merhaba **veri anlama** bu belgenin bölümü hello veri önemli bazı yönlerini kapsar. Merhaba tür enerji tahmin, veri kalitesi gereksinimleri ve hangi veri kaynaklarına genellikle mevcut için gerekli verileri özetler. Merhaba ham verileri gerçekten bölümü modelleme hello sürücü kullanılan tooprepare veri özellikleri nasıl olduğunu da açıklanmaktadır.

Merhaba belgenin Hello üçüncü bölümü kapsayan hello **teknik uygulamanın** bir çözüm yönü. Özellik Mühendisliği ve modelleme hello veri bilimi işlemi hello özünde ve biraz ayrıntılı olarak bu nedenle açıklanır. Bulut dağıtım Tahmine dayalı analiz çözümleri için önemli bir platformdur web hizmetleri hello kavramı kapsar. Biz de tipik bir uçtan uca kullanıma hazır hale getirilmiş çözüm mimarisi verilmiştir.

Ayrıca, hello belge hello etki alanı ve teknoloji daha fazla anlama toogain kullanabileceğiniz başvuru bilgileri içerir.

Biz toocover bu belge hello daha derin veri bilimi işleminde, matematiksel ve teknik yönlerini düşünmüyorsanız, önemli toonote olur. Bu ayrıntılar bulunabilir [Azure ML belgelerine](http://azure.microsoft.com/services/machine-learning/) ve [bloglar](http://blogs.microsoft.com/blog/tag/azure-machine-learning/).

### <a name="target-audience"></a>Hedef kitle
Bu belgenin hedef kitlesi Hello iş ve toogain bilgi ister misiniz teknik personeli olduğundan ve Machine Learning anlayış çözümleri ve özellikle hello enerji tahmin etki alanı içinde bu nasıl kullanıldığını temel.

Veri bilimcilerine sürücüleri çözüm tahmin enerji dağıtımını hello daha iyi anlamasına yardımcı hello yüksek düzeyli işlem bu belgeyi toogain okuma da yararlı olabilir. Bu bağlamda iyi temel ve daha fazla bilgi için başlangıç noktası ayrıntılı ve malzeme Gelişmiş kullanılan tooestablish da olabilir.

### <a name="industry-trends"></a>Endüstri eğilimleri
Birkaç yıl geçmiş Hello IOT, alternatif enerji kaynakları ve büyük veri toocreate büyük fırsatlar hello yardımcı programı ve enerji alanı birleştirilmiş sahip. Merhaba aynı zamanda, hello yardımcı programı ve hello tüm enerji kesimler enerji kullanımını daha iyi şekilde toocontrol yoğun tüketicileri düzleştirme tüketim gördünüz.

Çok sayıda yardımcı programı ve akıllı enerji şirketleri hello pioneering [akıllı kılavuz](https://en.wikipedia.org/wiki/Smart_grid) kullanım sayısı dağıtarak hale hello kılavuz tarafından oluşturulan hello veri kullanım. Birçok kullanım örnekleri hello devralınmış özelliklerini elektrik üretim Uzayda Döndür: Bu olamaz toplanan ya da kenara envanter olarak depolanan. Bu nedenle, ne üretilen kullanılması gerekir. Toobecome daha verimli istediğiniz yardımcı programlar gereksinim tooforecast güç tüketimini yalnızca, bunları daha yüksek bir beceri çok verir çünkü**dengelemek tedarik ve talep**, böylece enerji atık önleme **greenhouse azaltın Benzinli çıkması**ve denetim maliyeti.

Maliyetleri konuşurken fiyatıdır başka bir önemli boy yoktur. Yardımcı programlar arasında yeni yeteneklerini tootrade güç duruma harika bir ihtiyaç çok**gelecekteki isteğe bağlı ve elektrik gelecekteki fiyatını tahmin**. Bu, üretim birimleri belirlemek şirketler yardımcı olabilir.

Biz 'Akıllı' hello word kullandığınızda, biz gerçekte öğrenin ve ardından tahminlerde tooa kılavuzuna bakın. Tüketim Mevsimlik değişiklikler tahmin yanı **geçici aşırı durumlarda öngörüyor ve bunun için otomatik olarak ayarla**. Uzaktan tüketimiyle (Akıllı Bu ölçümler hello Yardımı) düzenleyerek yerelleştirilmiş aşırı durumlarda işlenebilir. **İlk tahmin etmeye ve ardından hareket**, hello kılavuz yapar kendisini Akıllı zaman içinde.

Biz belirli geleceği, tahmin kapak kullanım örnekleri ailesinde odaklanmak, bu belgenin hello rest için kısa vadeli ve uzun vadeli enerji isteğe bağlı. Biz bu alandaki birkaç ay için çalışmakta ve bazı bilgi ve bize tooproduce endüstri düzeyde sonuçları izin yetenek elde etmiştir. Diğer kullanım örnekleri de yakın gelecekte hello hello belgede ele alınacaktır.

## <a name="business-understanding"></a>İşin Gereksinimlerini Anlama
### <a name="business-goals"></a>İş hedefleri
Merhaba **enerji Demo** hedeftir toodemonstrate tipik Tahmine dayalı bir analiz ve makine öğrenimi çok kısa bir zaman dilimi içinde dağıtılabilir çözümü. Özellikle, böylece iş değeri kullanılabilir hızla gerçekleşen ve bağlı işlevden enerji talep tahmin çözümleri etkinleştirmek için geçerli bizim odak noktasıdır. Bu playbook Hello bilgiler hello müşteri hedeflerini izleyerek hello gerçekleştirmeye yardımcı olabilir:

* Kısa bir süre toovalue makine öğrenme tabanlı çözümün
* Özelliği tooexpand pilot kullanım örneği tooother durumlarda veya kendi iş gereksinimleri temelinde tooa daha geniş kapsam kullanın
* Hızlı bir şekilde Cortana Intelligence Suite ürün bilgisi elde

Bu hedefleri düşünerek hello iş ve bu hedeflere elde etmeye yardımcı olacak teknik bilgi teslim etmek bu playbook amaçlar.

### <a name="power-load-and-demand-forecasting"></a>Güç yük ve isteğe bağlı tahmin
Merhaba enerji kesim içinde hangi isteğe bağlı olarak tahmin kritik iş sorunlarını çözmenize yardımcı olabilecek birçok yolu olabilir. Aslında, isteğe bağlı tahmin hello foundation hello endüstri pek çok çekirdek kullanım durumlarında için kabul edilebilir. Genel olarak, biz enerji isteğe bağlı tahminleri iki tür düşünün: kısa vadeli ve uzun süreli. Her biri farklı bir amaca ve farklı bir yaklaşım kullanmak olabilir. Merhaba hello ikisi arasındaki temel fark, biz tahmin zaman hello gelecekteki içine hello aralığı anlamına yatay tahmin hello ' dir.

#### <a name="short-term-load-forecasting"></a>Kısa vadeli yük tahmin
Enerji talep Hello bağlamında, kısa vadeli yük tahmin (STLF) çeşitli bölümlerini hello kılavuz (veya bir bütün olarak hello kılavuz) üzerinde yakın hello tahmini hello toplanmış yük olarak tanımlanır. Bu bağlamda, kısa vadeli hello aralığı 1 saat too24 saat içinde tanımlanan toobe süresini ' dir. Bazı durumlarda, 48 saat kapsamını da mümkündür. Bu nedenle, STLF hello kılavuz işlemsel kullanım durumda çok yaygın bir durumdur. Kullanım örnekleri güdümlü STLF bazı örnekleri şunlardır:

* Tedarik ve talep Dengeleme
* Güç ticaret desteği
* Pazar yapma (ayar güç Fiyat)
* Kılavuz işletimsel en iyi duruma getirme
* [İsteğe yanıt](https://en.wikipedia.org/wiki/Demand_response)
* İsteğe bağlı tahmin en yüksek
* İsteğe bağlı tarafı Yönetimi
* Yük Dengeleme ve önleme aşırı yükleme
* Uzun süreli yük tahmin
* Hataya ve anomali algılama
* Yoğun curtailment/Dengeleme 

STLF modeli çoğunlukla hello üzerinde temel yakınında (son gün veya hafta) Tüketim verileri ve kullanım tahmini sıcaklık önemli bir göstergesi olduğu olarak. Merhaba sonraki saat ve too24 saatleri tahmin doğru sıcaklık alma daha az bir sınama şimdi gün durumundadır. Bu modeller, daha az hassas tooseasonal desenleri veya uzun vadeli tüketimi eğilimlerini markalarıdır.

SLTF çözümdür de büyük olasılıkla toogenerate hacmi yüksek tahmin çağrıları (hizmet istekleri), saatlik düzenli olarak ve bazı durumlarda bile yüksek sıklığı ile çağrılmakta bu yana. Ayrıca, burada her tek tek alt istasyon veya transformer tek başına model olarak temsil edilir ve bu nedenle tahmin istekleri hello hacmi daha yaygın toosee implantation unutulmamalıdır.

#### <a name="long-term-load-forecasting"></a>Uzun süreli yük tahmin
Merhaba, uzun vadeli yük tahmin (LTLF) tooforecast güç 1 hafta toomultiple aylarda (ve bazı durumlarda yıl sayısı için) arasında değişen bir süresini taleple hedeftir. Bu aralığı yatay çoğunlukla planlama için geçerlidir ve yatırım durumlarda kullanın.

Uzun vadeli senaryoları için onu birden çok yıl (en az 3 yıl) aralığını kapsayan önemli toohave yüksek kaliteli verilerdir. Bu modeller genellikle mevsimselliğin desenleri hello geçmiş verileri ayıklamak ve, dış predicators gibi kullanan hava durumu ve iklim desenleri olarak.

Yatay tahmin uzun hello hello tooclarify olduğundan, doğru hello tahmin daha az hello olabilir önemlidir. Bu nedenle, insanlar toofactor hello olası değişim kendi planlama işlemine izin hello gerçek birlikte bazı güvenirlik aralıkları tahmin önemli tooproduce olur.

Merhaba tüketim senaryo LTLF için çoğunlukla planlama olduğundan, daha düşük tahmin birimler (karşılaştırılan tooSTLF) bekleyebilirsiniz. Biz Excel veya Power BI gibi görselleştirme araçları içine katıştırılmış bu Öngörüler genellikle görürsünüz ve el ile Merhaba kullanıcı tarafından çağrılan.

### <a name="short-term-vs-long-term-prediction"></a>Kısa vadeli vs. Uzun vadeli tahmin
Aşağıdaki tablonun hello STLF ve LTLF saygı toohello en önemli öznitelikleri karşılaştırılır:

| Öznitelik | Kısa vadeli yük tahmin | Yük tahmin'uzun süreli |
| --- | --- | --- |
| Yatay tahmin |1 saat too48 saat |1 too6 ay veya daha fazla bilgi |
| Veri ayrıntı düzeyi |Saatlik |Saatlik veya günlük |
| Tipik kullanım durumları |<ul><li>Talep/tedarik dengeleme</li><li>Saat tahmin seçin</li><li>İsteğe yanıt</li></ul> |<ul><li>Uzun süreli planlama</li><li>Planlama Kılavuzu varlıklar</li><li>Kaynak planlama</li></ul> |
| Tipik predictors |<ul><li>Gün veya hafta</li><li>Günün saati</li><li>Saatlik sıcaklık</li></ul> |<ul><li>Yılın ayı</li><li>Ayın günü</li><li>Uzun vadeli sıcaklık ve iklim</li></ul> |
| Geçmiş verileri aralığı |İki toothree yıllık veri |Beş too10 yıllık veri |
| Tipik doğruluğu |MAPE * %5 veya daha düşük |MAPE * % 25 veya daha düşük |
| Tahmin sıklığı |Her saat veya 24 saatte oluşturulan |Aylık, üç aylık veya yıllık sonra üretilen |

\*[MAPE](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error) – ortalama yüzde hata anlama

Bu tablodan görüldüğü gibi hello kısa ve bunlar farklı iş gereksinimlerini temsil eden ve farklı dağıtım ve kullanım düzenlerini olabilir senaryoları tahmin hello uzun vadeli arasında oldukça önemli toodistinguish gereklidir.

### <a name="example-use-case-1-esmart-systems--overload-optimization"></a>Örnek Kullanım örneği 1: eSmart sistemleri – aşırı en iyi duruma getirme
Önemli bir rol, bir [akıllı kılavuz](https://en.wikipedia.org/wiki/Smart_grid) toodynamically ve sürekli olarak en iyi duruma getirme ve kullanım desenlerini değiştirme Merhaba ayarlayın. Güç tüketimini sıcaklık dalgalanmaları tarafından çoğunlukla neden kısa vadeli değişikliklerden etkilenebilir (*ör*, daha fazla güç hava durumu veya ısıtma kullanılır). AT hello aynı süre, güç tüketimi tarafından uzun vadeli eğilimleri de etkiler. Bunlar mevsimselliğin efektler, Ulusal tatilleri, uzun vadeli tüketim büyüme ve tüketici dizin, Petrol fiyat ve GDP gibi bile ekonomik etkenler olabilir.

Bu kullanım örneğindeki [eSmart](http://www.esmartsystems.com/) tahmin etmeye hello propensity verilen tüm alt istasyon üzerinde aşırı durumun hello kılavuzunun olanak tanıyan toodeploy bulut tabanlı çözümü istedik. Özellikle, eSmart Acil eylem tooavoid gerçekleştirilecek veya bu sorunu çözmek için sonraki bir saat içinde hello büyük olasılıkla toooverload olan tooidentify substations istedik.

Doğru bir ve hızlı tahmin gerçekleştirme üç Tahmine dayalı modelleri uyarlamasını gerektirir:

* Uzun güç tüketiminin her alt istasyon sırasında etkinleştirir tahmin sonraki birkaç hafta veya ay hello olduğunu terim modeli
* Belirli bir alt istasyon aşırı durumunuza hello sonraki saat sırasında tahminini sağlar kısa vadeli modeli
* Birden çok senaryolar gelecekteki sıcaklığını tahmin sağlar sıcaklık modeli

Merhaba uzun vadeli modeli Hello amacı toorank hello substations (Güç iletim kapasitelerine verilir) kendi propensity toooverload tarafından hello sonraki hafta veya ay içinde ' dir. Bu kısa listesini hello kısa vadeli tahmin için bir giriş olarak hizmet sunar substations hello oluşturulmasına izin verir. Sıcaklık hello uzun vadeli modeli için önemli bir göstergesi olduğu gibi var. gerek tooconstantly ürettiği çok senaryo sıcaklık tahminleri ve bunları toohello uzun vadeli modeline giriş olarak akış. Merhaba kısa vadeli tahmin çağrılır sonra hangi alt istasyon hello büyük olasılıkla toooverload sonraki saat olan toopredict.

Merhaba kısa vadeli ve uzun vadeli modelleri tek tek her alt istasyon dağıtılır. Bu nedenle, bu modeller pratik yürütülmesi hello kapsamlı orchestration gerektirir. toogain daha yüksek tahmin doğruluğunu hello kısa vadeli, daha ayrıntılı bir model, her saat hello için ayrılmış. Bu modeller saatte yürütülür ve birkaç dakika tooallow yeterli zaman toorespond içinde yürütülmesi biter ve gerekirse önleyici eylemleri gerçekleştirin. Bu koleksiyon modellerin dönemsel hello en son verileri kullanarak yeniden eğitme tarafından güncel tutulur.

Bu kullanım durumu hakkında daha fazla bilgi bulunabilir [burada](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18945).

#### <a name="use-case-qualification-criteria--prerequisites"></a>Servis talebi niteliği ölçütünü – Önkoşullar kullanın
Merhaba ana Cortana Intelligence gücünü kendi güçlü özelliği toodeploy ve ölçek machine learning merkezli çözümleri gerçekleştirilir. Bu, tasarlanmış toosupport binlerce eşzamanlı olarak yürütülen tahminleri olur. Ayrıca, toomeet değişen tüketim deseni otomatik olarak ölçeklendirebilirsiniz. Çözümün bu nedenle, doğruluk ve hesaplama performansı sağlamaktır. Örneğin, bir yardımcı programı şirket hello sonraki saat ve her saat hello tahmin doğru enerji talep üretmek ilgileniyor. Üzerindeki diğer yandan Merhaba, biz olduğu gibi neden hello tahmin edilen toobe taleptir hello soruyu yanıtlarken daha az ilgilendiğiniz (Merhaba modeli kendisini dikkatli olun,).

Bu nedenle, tüm kullanım örnekleri ve iş sorunlarını etkili bir şekilde machine learning kullanarak çözülebilir önemli toorealize olur.

Cortana Intelligence ve makine öğrenme ölçütleri aşağıdaki hello karşılandığında belirli iş sorununu çözme konusunda son derece verimli olabilir:

* Merhaba iş el sorunudur **Tahmine dayalı** yapısı. Tahmine dayalı kullanım örneği örnek belirli bir alt istasyon toopredict güç yükünü sonraki saat hello sırasında istediğiniz yardımcı programı bir şirkettir. Üzerindeki diğer yandan Merhaba, çözümleme ve geçmiş isteğe bağlı sürücülerin sıralaması olacaktır **açıklayıcı** yapısı ve bu nedenle daha az uygulanabilir.
* Açık olduğundan **eylemin yolunu** kez hello tahmin gerçekleştirilecek toobe kullanılabilir. Örneğin, bir alt istasyon üzerinde bir aşırı sonraki saat hello sırasında tahmin etmeye o alt istasyon ile ilişkili yük azaltır ve bu nedenle bir aşırı büyük olasılıkla önleme öngörülü bir eylem tetikleyebilir.
* Merhaba kullanım örneğini temsil eder bir **sorunun tipik türü** şekilde Çözüldü zaman onu hello yolu toosolving benzer diğer kullanım örnekleri pave.
* Merhaba müşteri ayarlayabilirsiniz **nicel ve nitel hedeflerini** toodemonstrate başarılı çözüm uygulaması. Örneğin, enerji talep tahmin için iyi bir nicel hedefi hello gerekli doğruluğu eşik olur (*örn*, too5% hata izin verilir) veya alt istasyon aşırı sonra hello duyarlık (doğru pozitif sonuç oranı) tahmin etmeye ve geri çağırma (doğru pozitif sonuç kapsamını) belirli bir eşiğin üzerinde olmalıdır. Bu hedefleri hello müşterinin iş hedeflerden türetilmesi.
* Açık olduğundan **tümleştirme senaryosunun** hello şirketin iş akışıyla. Örneğin, hello alt istasyon yük tahmin hello kılavuz denetim merkezi tooallow aşırı önleme etkinliklerine tümleştirilebilir.
* Hello müşterinin hazır toouse **yeterli kalite verilerle** toosupport hello kullanım örneği (Merhaba sonraki bölümde, daha fazla **veri kalitesini**, bu playbook olarak).
* Merhaba müşteri kapsayan bulut merkezli veri mimarisi veya **bulut tabanlı makine öğrenme**Azure ML ve diğer Cortana Intelligence Suite bileşenleri dahil olmak üzere.
* Merhaba müşteri mi istekli tooestablish **son tooend veri akışı** tesis hello veri teslimini hello buluta düzenli olarak ve istekli olup çok**faaliyete** hello çözümü.
* Merhaba müşteri hazır çok**kaynak ayırması** aktarılan toohello müşteri başarılı üzerine bilgi ve hello çözüm sahipliğini olabilmesi kimin etkin şekilde hello ilk pilot uygulaması sırasında gerçekleştiriliyor olmamalıdır tamamlama.
* Merhaba müşteri kaynak olmalıdır bir **becerikli veri professional**, tercihen veri Bilimcisi.

Niteliğe hello yukarıdaki ölçütlere göre kullanım örneğinin büyük ölçüde kullanım hello başarı oranları artırmak ve gelecekteki kullanım örnekleri hello uygulama için iyi bir beachhead oluşturun.

### <a name="cloud-based-solutions"></a>Bulut tabanlı çözümler
Cortana Intelligence Suite azure'da hello bulutta bulunan tümleşik bir ortam ' dir. Bulut ortamında bulunan bir Gelişmiş analiz çözümü Hello dağıtımını işletmeler için önemli faydaları tutan ve Merhaba aynı anda şirketler için büyük değişiklik hala kullanım BT çözümleri şirket içi olduğunu olduğu anlamına gelebilir. Merhaba enerji kesim içinde aşamalı geçiş hello buluta işlemlerinin Temizle eğilimini yoktur. Bu eğilimin el ele, yukarıda açıklandığı gibi hello akıllı kılavuz hello geliştirme birlikte gider **endüstri eğilimleri**. Bu playbook, bulut tabanlı bir çözüme hello enerji etki alanındaki odaklanan gibi önemli tooexplain hello avantajları ve bulut tabanlı bir çözüm dağıtma diğer durumlar olur.

Belki de hello bulut tabanlı bir çözüme en büyük avantajlarından hello maliyetidir. Bir çözümü olarak kullanır buluta dağıtılan bileşenlerinin ön maliyetleri veya ilişkili SMM (maliyet mal satılan) bileşeni giderleri yoktur. Donanım, yazılım ve BT bakım hiçbir gerek tooinvest yoktur ve bu nedenle iş riskinin önemli ölçüde azalma yoktur anlamına gelir.

Başka bir önemli avantajı hello Kullandıkça Öde maliyet bulut tabanlı çözümlerinin yapısıdır. Bulut tabanlı sunucular bilgi işlem ve depolama için dağıtılan ve gerekli yeni bir temelinde ölçeklendirilmiş. Bu, bulut tabanlı bir çözüme hello maliyet verimliliği avantajlarından temsil eder.

Son olarak, tüm bu hello bulut tabanlı teklif parçası olarak BT Bakım veya gelecekteki altyapı geliştirme yatırım yapmak için gerek yoktur. toothat azami ölçüde, Cortana Intelligence Suite hello en iyi sınıf Hizmetleri'nde içerir ve yol haritası gelişen tutar. Yeni özellik, bileşenleri ve yetenekler sürekli eklenen ve geliştirin.

Yalnızca kendi geçiş hello buluta başlayarak bir şirket için yüksek oranda tootake aşamalı bir yaklaşım bulut geçiş yol haritası uygulayarak öneriyoruz. Yardımcı programlar ve hello enerji etki alanındaki şirketler için bu playbook ele alınan hello kullanım örnekleri hello bulutta Tahmine dayalı analiz çözümlerini Pilot uygulaması için mükemmel bir fırsat temsil eden inanıyoruz.

#### <a name="business-case-justification-considerations"></a>İş örneği doğrulama konuları
Çoğu durumda, hello müşteri bir bulut tabanlı çözümü ve Machine Learning önemli bileşenleri olduğu belirli kullanım örneği için bir iş gerekçesinin yaparken ilgilenebilirsiniz. Bir bulut tabanlı çözümün hello durumda bir şirket içi çözüm aksine hello ön maliyet en az bileşenidir ve hello maliyet öğelerin çoğu gerçek kullanımı ile ilişkilendirilmiş. Cortana Intelligence Suite çözümünü tahmin enerji toodeploying geldiğinde, birden fazla hizmet, tek bir ortak maliyet yapısı ile tümleştirilebilir. Örneğin, veritabanları (*ör*, SQL Azure) kullanılan toostore hello ham verileri olabilir ve ardından Azure ML hello gerçek tahminleri için olan kullanılan toohost hello tahmin Hizmetleri. Bu örnekte, depolama ve işlemsel bileşenlerini yapısı maliyet hello dahil olabilir.

Merhaba diğer yandan, bir (kısa veya uzun süreli) tahmin enerji isteğe bağlı işletim hello iş değerini iyi anlamış olmalıdır. Aslında, bu önemli toorealize hello iş tahmin her işlemin değerdir. Örneğin, doğru şekilde güç yük hello için sonraki 24 saat tahmin overproduction engelleyebilir veya aşırı hello kılavuza önlenmesine yardımcı olabilir ve bu günlük olarak finansal tasarrufları bakımından quantified.

Çözüm olacaktır hello finansal avantajı talebin hesaplamak için temel bir formül tahmin: ![hello finansal avantajı talebin hesaplamak için temel formülü tahmin çözümü](media/cortana-analytics-playbook-demand-forecasting-energy/financial-benefit-formula.png)

Cortana Intelligence Suite Kullandıkça Öde bir fiyatlandırma modelini sağlar olduğundan, bir sabit maliyet bileşen toothis formül yansıtılmasını için gerek yoktur. Bu formülü bir günlük, aylık veya yıllık temelinde hesaplanabilir.

Geçerli Cortana Intelligence Suite ve Azure fiyatlandırma planı ML bulunabilir [burada](http://azure.microsoft.com/pricing/details/machine-learning/).

### <a name="solution-development-process"></a>Çözüm geliştirme işlemi
Cortana Intelligence Suite içindeki Hizmetler hello ve çözüm genellikle her biri vermiyoruz 4 aşamaları içerir tahmin enerji talebin Hello geliştirme döngüsü bulut tabanlı teknoloji kullanın.

Bu diyagramda aşağıdaki hello gösterilmiştir:

![Akıllı kılavuz döngüsü](media/cortana-analytics-playbook-demand-forecasting-energy/smart-grid-cycle.png)

Sonraki Paragraf hello bu 4 adım işlemi açıklanmaktadır:

1. **Veri toplama** – her Gelişmiş dayalı analiz çözümü verileri kullanır (bkz **veri anlama**). Özellikle, toopredictive analizi ve tahmin geldiğinde, biz devam eden, dinamik veri akışını kullanır. İsteğe bağlı enerji tahmin, hello durumda, bu verileri doğrudan akıllı ölçümler kaynaklanan veya bir şirket içi veritabanında zaten toplanması. Biz de verilerin hava durumu ve sıcaklık gibi diğer dış kaynaklarını kullanır. Devam eden bu veri akışını düzenlenmiş, zamanlanmış depolanan ve gerekir. [Azure Data Factory](http://azure.microsoft.com/services/data-factory/) (ADF), bu görevi gerçekleştirmeye için ana bizim workhorse olduğu.
2. **Modelleme** – doğru ve güvenilir enerji tahminleri biri gerekir (tren) geliştirmek ve yapar harika bir modeli hello geçmiş verileri kullanır ve ayıklar hello anlamlı korumak ve Tahmine dayalı modelleri hello veri. Merhaba alanı Machine Learning (ML) düzenli olarak geliştirilen daha gelişmiş algoritmalarıyla hızla büyüyor. Azure ML Studio ML algoritmaları tam iş akışı içinde en gelişmiş hello kullanmasına yardımcı olan bir iyi kullanıcı deneyimi sağlar. İş akışının sezgisel bir akış şemada gösterilmiştir ve hello veri hazırlığı, özelliği ayıklama, model ve model değerlendirme içerir. Merhaba kullanıcı bu ortamda dahil çeşitli modellerin yüzlerce çeker. Bu aşama Hello ucu tarafından tam olarak değerlendirilen ve dağıtım için hazır bir çalışma modeli veri Bilimcisi sahip olur.
   
   Aşağıdaki diyagramda hello normal bir iş akışı bir çizimi şöyledir:
   
   ![İş akışı modelleme](media/cortana-analytics-playbook-demand-forecasting-energy/modeling-workflow.png)
3. **Dağıtım** – çalışma modeli yandan, hello sonraki adıma dağıtımıdır. Burada hello modeli çeşitli tüketim istemcilerden hello Internet üzerinden eşzamanlı olarak çağrılabilen bir RESTful API'si gösteren bir web hizmeti dönüştürülür. Azure ML hello Azure ML Studio'da bir düğmeye tek bir tıklatmayla modelden doğrudan dağıtma basit bir yol sağlar. Merhaba tüm dağıtım işlemi hello başlık altında olur. Bu çözüm otomatik olarak toomeet gerekli hello tüketim ölçeklendirebilirsiniz.
4. **Tüketim** – bu aşamasında, aslında vermiyoruz modeli tooproduce tahminleri tahmin hello kullanın. Merhaba tüketim bir kullanıcı uygulamadan güdümlü (*ör*, Pano) veya doğrudan gibi bir işletim sisteminden talep/tedarik sistem ya da bir kılavuz iyileştirme çözümün Dengeleme. Birden çok kullanım durumu tek bir modelden güdümlü.

## <a name="data-understanding"></a>Veri anlama
Merhaba iş konuları kapsayan sonra (bkz **iş anlama**) veri bölümü hazır toodiscuss hello artık gerçekleştiriyoruz, çözüm tahmin bir enerji talebi. Herhangi bir Tahmine dayalı analiz çözümü güvenilir verileri kullanır. İsteğe bağlı enerji tahmin için size çeşitli ayrıntı düzeyleri ile geçmiş verilere kullanır. Geçmiş verilerin hello ham madde kullanılır. Hangi hello veri Bilimcisi, gerekli hello tahminleri sonunda oluşturacak bir modeli koyabilirsiniz (Ayrıca başvurulan tooas özellikleri) predictors tanımlayacak dikkatli bir çözümlemesini yapılacaktır.

Bu bölümün Hello kalan biz anlatmaktadır çeşitli adımları ve hello veri anlama konuları hello ve nasıl toobring, tooa kullanılabilir biçime.

### <a name="hello-model-development-cycle"></a>Merhaba modeli geliştirme döngüsü
İyi tahmin modelleri bazı dikkatli hazırlık gerekir ve planlama notlarının oluşturulması. İşlem içine birden çok adımı modelleme ve aynı anda tek bir adımda odaklanan hello bölmek hello hello tüm işleminin sonucunu önemli ölçüde arttırabilir.

Merhaba Aşağıdaki diyagramda işlem modelleme hello içine birden çok adımı nasıl bölünebilir gösterilmektedir:

![Model geliştirme döngüsü](media/cortana-analytics-playbook-demand-forecasting-energy/model-development-cycle.png)

Gibi hello döngüsü altı adımlardan oluşur görülebilir:

* Sorun formülasyonu
* Veri alımı ve veri araştırması
* Veri hazırlama ve özellik Mühendisliği
* Modelleme
* Model değerlendirme
* Geliştirme

Bu bölümün Hello kalanında biz hello tek tek adımları ve her adımında öğeleri tooconsider anlatmaktadır.

### <a name="problem-formulation"></a>Sorun Formülasyonu
Merhaba en önemli adım bir tootake önceki tooimplementing herhangi bir Tahmine dayalı analiz çözümü gereksinimleriniz değiştikçe biz hello sorun formülasyonu düşünebilirsiniz. Burada size dönüştürme hello problemini ve verileri kullanarak ve teknikleri modelleme çözülebilir toospecific öğelerinin parçalayın. İyi bir uygulama tooformulate hello sorunun bulunduğunu soruları bir dizi tooanswer isteriz. İsteğe bağlı enerji tahmin hello kapsamını içinde geçerli olabilecek bazı olası sorular şunlardır:

* Merhaba sonraki saat veya gün içinde ayrı bir alt istasyon hello beklenen yükü nedir?
* Merhaba günün hangi saatinde my kılavuz en yüksek talebi yaşar?
* Büyük olasılıkla nasıl my kılavuz toosustain beklenen hello yoğun yük mi?
* Ne kadar güç hello güç istasyon her saat hello sırasında oluşturmalı mı?

Bu soruları formulating bize hello doğru verileri alma ve elinizdeki hello iş sorununu ile tam olarak hizalanır bir çözüm uygulama toofocus sağlar. Ayrıca, biz bize tooevaluate hello performans hello modelinin izin bazı önemli metrikleri sonra ayarlayabilirsiniz. Örneğin, ne kadar doğru hello olması ve ne hello hala hello iş tarafından kabul edilebilir olacak hata aralığı tahmin mı?

### <a name="data-sources"></a>Veri Kaynakları
Merhaba modern akıllı kılavuz çeşitli bölümleri ve bileşenleri hello kılavuzunun verileri toplar. Bu veriler hello işleminin çeşitli yönlerini ve hello güç kılavuz hello kullanımını temsil eder. Tahmin hello enerji talep Hello kapsamında, biz hello tartışma hello gerçek talep tüketim yansıtacak veri kaynaklarında kısıtlayan. Akıllı ölçümler enerji tüketimi önemli bir kaynağı var. Merhaba Dünya çevresinde yardımcı programlar, hızlı bir şekilde kendi Tüketiciler için akıllı ölçümler dağıtıyorsanız. Akıllı ölçümler hello gerçek güç tüketimi kaydedebilir ve bu verileri geri toohello yardımcı şirket sürekli geçiş. Veriler toplanır ve 5 dakika too1 saatte arasında değişen geri sabit bir aralık, gönderilir. Daha gelişmiş akıllı ölçümler programlanmış uzaktan toocontrol ve Bakiye hello bir evin içindeki gerçek tüketim. Akıllı ölçüm verileri görece güvenilirdir ve zaman damgası içerir. Bu tahmin talep için önemli bir malzeme kolaylaştırır. Ölçer veri bir araya getirilir (yukarı toplanan) hello kılavuz topoloji içindeki çeşitli düzeylerde: transformer, alt istasyon, bölge, *vb.*. Biz sonra gerekli hello toplama düzeyi toobuild bir tahmin modeli de seçebilirsiniz. Örneğin, hello yardımcı şirket tooforecast gelecekteki gibi her kılavuz substations yüklerseniz sonra tüm ölçümler veriler için tek tek her alt istasyon bir araya getirilir ve modeli tahmin hello için girdi olarak kullanılır. Biz toosmart ölçümler bir iç veri kaynağı olarak bakın.

Bir güvenilir enerji talep tahmin ayrıca diğer dış veri kaynaklarına bağlıdır. Güç tüketimini etkileyen bir önemli hello hava durumu ya da daha hassas bir şekilde hello sıcaklık faktördür. Geçmiş verileri dış sıcaklık ve güç tüketimini arasında güçlü bağıntı gösterir. Tüketiciler sıcak Yaz gün boyunca olun kendi hava bağıntıyı ve sistemler ısıtma üzerinde hello Kış güç sırasında kullanın. Güvenilir bir kaynak hello kılavuz konumda geçmiş etme, bu nedenle anahtardır. Ayrıca, biz de sıcaklık doğru tahmin üzerinde bir göstergesi olduğu güç tüketimini kullanır.

Diğer dış veri kaynaklarına enerji talep tahmin modelleri oluşturmaya da yardımcı olur. Bu uzun vadeli iklim değişiklikleri, ekonomik dizinleri içerebilir (*ör*, GDP) ve diğerleri. Bu belgede Biz bu diğer veri kaynakları dahil edilmez.

### <a name="data-structure"></a>Veri yapısı
Veri kaynakları gerekli Hello tanımlayan sonra toplanan ham verileri hello içeren tooensure gibi veri özellikleri düzeltilebilir. toobuild güvenilir bir isteğe bağlı tahmin modeli, biz gerekir toplanan verileri hello tooensure hello gelecekteki talep tahmin etmeye yardımcı olması veri öğeleri içerir. Merhaba ham verileri hello veri yapısı (şema) ile ilgili bazı temel gereksinimleri aşağıda verilmiştir.

Merhaba ham verileri satırları ve sütunları oluşur. Her ölçüm verileri tek bir satır temsil edilir. Her veri satırının birden çok sütun (Ayrıca başvurulan tooas özellikler veya alanlar) içerir.

1. **Zaman damgası** – hello zaman damgası alanı hello gerçek zaman zaman hello ölçüm kaydedilen temsil eder. Merhaba ortak tarih/saat biçimlerinden biri ile uyumlu. Tarih ve saat bölümleri eklenmelidir. Çoğu durumda, gerek yoktur kasa hello zaman toobe kaydedilen için hello ikinci düzeyde ayrıntı düzeyi. Önemli toospecify hello saat dilimi hello veri kaydedilen olur.
2. **Ölçüm kimliği** -Bu alan hello ölçer veya hello ölçüm aygıt tanımlar. Kategorik bir değişkendir ve basamak ve karakter bir bileşimi olabilir.
3. **Tüketim değeri** – belirli bir tarih/zaman hello gerçek tüketim budur. Merhaba tüketim kWh (kilowatt-hour) ölçülen veya diğer tercih edilen birimleri. Ölçü birimi hello toonote hello veri tüm ölçüleri arasında tutarlı kalması gerekir önemlidir. Bazı durumlarda, tüketim üzerinde 3 güç aşamaları sağlanabilir. Bu durumda biz tüm hello bağımsız tüketim aşamaları toocollect gerekir.
4. **Sıcaklık** – hello sıcaklık bağımsız bir kaynaktan genellikle toplanır. Ancak, hello tüketim veri türüyle uyumlu olmalıdır. İzin veren yukarıda açıklandığı gibi bir zaman damgası içermelidir toobe hello gerçek tüketim verilerle eşitlenmiş. Hello sıcaklık değer derece derece veya Fahrenhayt belirtilebilir ancak tüm ölçümler arasında tutarlı kalmasını.
5. **Konum –** hello konum alanı, burada hello sıcaklık toplanan veriler hello yer genellikle ilişkilendirilmiş. Bir posta kodu sayı olarak veya enlem/boylam (lat/uzun) biçiminde gösterilebilir.

Aşağıdaki tablolar hello iyi kullanım ve sıcaklık veri biçimi örnekler gösterilmektedir:

| **Tarih** | **Saat** | **Ölçer kimliği** | **Aşama 1** | **Aşama 2** | **3. Aşama** |
| --- | --- | --- | --- | --- | --- |
| 7/1/2015 |10:00:00 |ABC1234 |7.0 |2.1 |5.3 |
| 7/1/2015 |10:00:01 |ABC1234 |7.1 |2.2 |4.3 |
| 7/1/2015 |10:00:02 |ABC1234 |6.0 |2.1 |4.0 |

| **Tarih** | **Saat** | **Konum** | **Sıcaklık** |
| --- | --- | --- | --- |
| 7/1/2015 |10:00:00 |11242 |24.4 |
| 7/1/2015 |10:00:01 |11242 |24.4 |
| 7/1/2015 |10:00:02 |11242 |24.5 |

Yukarıdaki görüldüğü gibi bu örnek 3 güç aşaması olan ilişkili tüketimi için 3 farklı değerler içerir. Ayrıca, başlangıç tarihi ve saati alanları ayrılmış olduğunu, ancak bunlar da tek bir sütun halinde birleştirilebilir unutmayın. Bu durumda hello konum sütunu bir derece derece biçiminde hello sıcaklık ve 5 rakamlı posta kodu biçimi gösterilir.

### <a name="data-format"></a>Veri biçimi
Cortana Intelligence Suite, CSV, TSV, JSON, gibi en yaygın veri biçimleri hello destekleyebilmesi *vb.*. Bu hello veri biçimi hello için tüm yaşam döngüsünü hello projesinin tutarlı kalmasını önemlidir.

### <a name="data-ingestion"></a>Veri Alımı
Enerji talep tahmin sürekli ve sık tahmin olduğundan, biz hello ham verileri düz ve güvenilir veri alım işlemi yoluyla akan emin olmanız gerekir. Merhaba alım işlem hello ham verileri işlem gerekli hello zaman tahmin hello için kullanılabilir olduğunu güvence altına almalıdır. Merhaba veri alım frekansı sıklığı tahmin hello büyük olmalıdır anlamına gelir.

Örneğin: Çözüm 8: 00'da her gün yeni bir tahmin oluşturmak sonra sırasında toplanan tüm hello verileri son hello tooensure ihtiyacımız tahmin bizim isteğe bağlı 24 saat kadar o noktadan tam olarak alınan olmadığını ve hello dahil tooeven olup verilerin son bir saat.

İçinde tooaccomplish Bu, sipariş Cortana Intelligence Suite çeşitli yolları toosupport güvenilir veri alım işlemi sunar. Daha fazla hello incelenecektir **dağıtım** bu belgenin bölüm.

### <a name="data-quality"></a>Veri Kalitesi
güvenilir ve doğru bir talebi tahmin gerçekleştirmek için gerekli olan hello ham veri kaynağı bazı temel veri kalite ölçütlerini karşılamalıdır. Gelişmiş istatistiksel yöntemler bazı olası veri kalite sorunu için kullanılan toocompensate olabilse de, biz yine biz bazı temel veri kalitesi eşik yeni veri alma zaman geçmesinden olduğunu tooensure gerekir. Ham veri kalitesini ilgili birkaç dikkat edilecek noktalar şunlardır:

* **Eksik değeri** – belirli bir ölçü değil toplanan olduğunda bu toohello durum başvuruyor. Merhaba temel burada değer oranı eksik o hello belirli bir süre için % 10 ' büyük olmamalıdır gereksinimdir. Durumda, tek bir değer eksik önceden tanımlanmış bir değer kullanarak belirtilmesi (örneğin: '9999') ve 'geçerli bir ölçü olabilen 0'.
* **Ölçüm doğruluğu** – tüketimi veya sıcaklık gerçek değerini hello doğru bir şekilde kaydedilmiş. Yanlış ölçümleri yanlış tahminleri oluşturur. Genellikle, hello ölçüm hata %1 göreli toohello true değerden daha düşük olması gerekir.
* **Ölçüm zaman** – gerekli toplanan hello veri hello gerçek zaman damgası tarafından birden çok 10 saniye göreli toohello doğru zamanı hello gerçek ölçü sapma değil.
* **Eşitleme** – birden çok veri kaynağı kullanıldığında (*ör*, kullanım ve sıcaklık) biz hiçbir zaman eşitleme olduğundan emin olun aralarında sorunları. Bunun anlamı hello bundan herhangi iki bağımsız veri kaynaklarından toplanan hello zaman damgası arasındaki farkı 10 saniyeden fazla aşamaz.
* **Gecikme süresi** - de, yukarıda açıklanan şekilde **veri alımı**, bir güvenilir veri akışı ve alım işleme bağımlı duyuyoruz. toocontrol biz biz hello veri gecikmesi kontrol emin olmalısınız. Bu, hello gerçek ölçüm alındığı hello zaman ve veren Cortana Intelligence Suite depolama hello yüklendi ve kullanıma hazırdır hello saat arasındaki zaman farkı hello olarak belirtilir. Kısa vadeli yükü için tahmin hello toplam gecikme süresi 30 dakikadan fazla olmamalıdır. Uzun vadeli yükü için tahmin hello toplam gecikme süresi 1 günden daha büyük olmamalıdır.

### <a name="data-preparation-and-feature-engineering"></a>Veri hazırlama ve özellik Mühendisliği
Hello ham verileri alınan sonra (bkz **veri alımı**) ve güvenli bir şekilde depolanır; işlenen hazır toobe olduğu. Merhaba veri hazırlık aşamasının temel alarak hello ham verileri ve (, yeniden şekillendirmek dönüştürme) dönüştürme aşaması modelleme hello için bir form içine. Örneğin, gerçek ölçülen değeri, standartlaştırılmış değerleri, daha karmaşık işlemleri gibi olduğu gibi hello ham veri sütunu kullanarak basit işlemleri içerebilir [zaman İzolasyonu](https://en.wikipedia.org/wiki/Lag_operator)ve diğerleri. Yeni oluşturulan hello veri sütunlarını başvurulan tooas veri özellikleri ve bu oluşturma işleminin hello başvurulan tooas özellik Mühendisliği. Bu işlem Hello ucu tarafından biz hello ham verilerden türetilmiş ve model için kullanılacak yeni bir veri kümesi gerekir. Buna ek olarak, hello veri hazırlık aşamasının eksik değerleri care of tootake gerekir (bkz **veri kalitesini**) ve bunlar için dengelemek. Bazı durumlarda, biz de tüm değerleri temsil edildiğini toonormalize hello veri tooensure gerekir hello aynı ölçek.

Bu bölümde biz hello enerji dahil edilen hello ortak veri özelliklerin bir listesi tahmin modelleri isteğe bağlı.

**Özellikler güdümlü saat:** bu özellikleri hello tarih/zaman damgası verilerden türetilir. Bunlar ayıklanan ve gibi kategorik özellikleri dönüştürülür:

* Zaman hello saat değerleri 0 too23 alan hello budur – günü
* Gün haftanın – bu hello haftanın başlangıç günü temsil eder ve 1 (Pazar) too7 (Cumartesi) değerleri alır
* Gün ayın – bu hello gerçek tarihini temsil eder ve 1 too31 değerleri alabilir
* Ay yıl – bu hello ay temsil eder ve 1 (Ocak) too12 (aralık) değerleri alır
* Hafta sonu – bu hello değeri 0 haftanın günlerini veya 1 hafta sonu için gereken bir ikili değer özelliğidir
* Tatil - bu hello değeri 0 tatil için normal bir gün veya 1 için gereken bir ikili değer özelliğidir
* Fourier koşulları – hello zaman damgası türetilen ağırlıkları terimler Fourier hello ve hello verilerinde kullanılan toocapture hello mevsimselliğin (döngü) gelir. Birden çok dönemleri bizim verilerde olabilir beri birden çok Fourier koşulları ihtiyacımız. Örneğin, talep değerleri yıllık, haftalık ve günlük dönemleri/3 Fourier koşullarını neden olacak döngüleri olabilir.

**Bağımsız ölçüm özellikleri:** hello bağımsız özellikleri toouse predictors bizim modelinde isteriz olduğunu tüm hello veri öğeleri içerir. Burada size ihtiyacımız hello bağımlı özelliğini hariç toopredict.

* Gecikme özelliği – bunlar gölgeye zaman hello gerçek talep değerleri. Örneğin, öteleme 1 özellikleri hello talep değeri hello (saatlik veri varsayılarak) önceki saat göreli toohello geçerli zaman damgası içinde tutar. Benzer şekilde, biz öteleme 2 eklemek için 3, öteleme *vb.*. hello gerçek kullanılan öteleme özellik bileşimi aşaması modelleme hello sırasında hello modeli sonuçları değerlendirme tarafından belirlenir.
* Uzun süreli oluşturan eğilim – bu özellik hello doğrusal büyüme yıl arasında isteğe bağlı olarak temsil eder.

**Bağımlı özellik:** hello bağımlı özelliktir isteriz hello veri sütunu bizim modeli toopredict. İle [denetimli makine öğrenme](https://en.wikipedia.org/wiki/Supervised_learning), ilk (aynı zamanda olan başvurulan tooas etiketleri) hello bağımlı özelliklerini kullanarak hello modeli eğitmek ihtiyacımız. Bu hello model toolearn hello deseni hello bağımlı özellik ile ilişkilendirilmiş hello verileri sağlar. Tahmin enerji talep genellikle toopredict hello gerçek talep istiyoruz ve bu nedenle biz bunu hello bağımlı özellik olarak kullanırsınız.

**Eksik değerleri işleme:** hello verileri hazırlama aşamasında, biz toodetermine hello en iyi strateji toohandle eksik değerleri gerekir. Çoğunlukla budur kullanarak çeşitli istatistik hello [veri imputation yöntemleri](https://en.wikipedia.org/wiki/Imputation_\(statistics\)). Tahmin enerji talep Hello durumda biz genellikle eksik değerleri önceki kullanılabilir veri noktalarından hareketli ortalama kullanarak impute.

**Veri normalleştirme:** veri normalleştirme isteğe bağlı gibi tüm sayısal verileri tahmin benzer bir ölçekte kullanılan toobring olan dönüşümünün başka bir türüdür. Bu, genellikle hello model doğruluğundan ve duyarlık artırılmasına yardımcı olur. Biz genellikle hello veri hello aralığına göre hello gerçek değer bölerek yaparsınız.
Bu hello özgün değeri -1 ile 1 arasında genellikle daha küçük bir aralık içinde ölçeklenir.

## <a name="modeling"></a>Modelleme
Aşama modelleme hello hello verileri hello dönüştürme bir modeline gerçekleştiği ' dir. Hello çekirdek var. Bu işlemin Gelişmiş hello geçmiş verileri (eğitim) tarayın, desenleri ayıklamak ve bir model oluşturma algoritmaları. Bu model, kullanılan toopredict kullanılan toobuild hello modeli yapılmamış yeni verilerin daha sonra olabilir.

Güvenilir bir çalışma sahibiz sonra biz ardından yapılandırılmış tooinclude hello tooscore yeni verileri kullanabilmesi model özellikleri (X) gereklidir. Puanlama sürecinde hello hello kalıcı modelinin (Merhaba eğitim aşaması nesnesinden) kullanın ve Ŷ tarafından gösterilen hello hedef değişkeni tahmin hale getirir.

### <a name="demand-forecasting-modeling-techniques"></a>Tahmin modelleme teknikleri talep
Merhaba durumda vermiyoruz tahmin talebin zamanına göre sıralanmış geçmiş verilerin kullanın. Biz genellikle hello zaman boyutu olarak içeren toodata başvuran [zaman serisi](https://en.wikipedia.org/wiki/Time_series). Merhaba hedef zaman serisi modelleme ilgili toofind zaman içinde eğilimlerin, mevsimselliğin, otomatik bağıntı (bağıntı zaman içinde) ve bu bir modeline formüle.

Son yıllarda gelişmiş algoritmalar geliştirilmiş tooaccommodate zaman serisi tahmin ve doğruluk tahmin tooimprove olmuştur. Biz kısaca birkaç tanesi aşağıda ele alınmıştır.

> [!NOTE]
> Bu bölümde bir makine öğrenme ve genel bakış tahmin olarak ancak bunun yerine isteğe bağlı tahmin için yaygın olarak kullanılan teknikleri modelleme kısa anket olarak kullanılan hedeflenen toobe değil. Daha fazla bilgi ve eğitim malzemesi zaman serisi tahmin hakkında hello çevrimiçi kitap öneririz [tahmin: ilkeleri ve uygulama](https://www.otexts.org/book/fpp).
> 
> 

#### <a name="ma-moving-averagehttpswwwotextsorgfpp62"></a>[**MA (hareketli ortalama)**](https://www.otexts.org/fpp/6/2)
Hareketli ortalama zaman serisi tahmin için kullanılan hello ilk analitik teknikleri biridir ve hala hello en sık kullanılan teknikleri bugünden itibaren biridir. Bu ayrıca hello teknikleri tahmin daha gelişmiş temelidir. Hareketli Ortalama biz burada K hareketli ortalama hello hello sırasını gösterir hello K en son noktaları ortalayarak hello sonraki veri noktası tahmin.

Hello hareketli ortalama teknik tahmin hello düzgünleştirme hello etkisi yoktur ve bu nedenle de büyük volatilite hello veri işleyebilir değil.

#### <a name="ets-exponential-smoothinghttpswwwotextsorgfpp75"></a>[**Madde işaretleri (Üstel düzeltme)**](https://www.otexts.org/fpp/7/5)
Üstel yumuşatma (madde işaretleri) son veri noktaları Ağırlıklı ortalama sipariş toopredict hello sonraki veri noktası kullanan çeşitli yöntemlerle ailesi ' dir. tooassign daha yüksek ağırlığı toomore son değerleri olan ve bu ağırlık eski ölçülen değerler için giderek azaltmak Hello uygulamadır. Birkaç farklı yöntemle bu aile, bunlardan bazıları mevsimselliğin hello verilerdeki, gibi işleme dahil [Holt Winters Mevsimlik yöntemi](https://www.otexts.org/fpp/7/5).

Bu yöntemlerin bazıları da hello veri hello mevsimselliğin içinde öğeli.

#### <a name="arima-auto-regression-integrated-moving-averagehttpswwwotextsorgfpp8"></a>[**ARIMA (otomatik gerileme tümleşik hareketli ortalama)**](https://www.otexts.org/fpp/8)
Otomatik gerileme tümleşik hareketli ortalama (ARIMA) zaman serisi tahmin için yaygın olarak kullanılan başka bir yöntem ailesi ' dir. Pratikte, otomatik gerileme yöntemleri'nin hareketli ortalama ile birleştirir. Otomatik gerileme yöntemler, sipariş toocompute hello sonraki tarih noktasında önceki zaman serisi değerleri gerçekleştirerek regresyon modeli kullanır. ARIMA yöntemleri de veri noktalarının hello birbirinden hesaplama ve bu hello özgün ölçülen değeri yerine kullanarak içeren fark kayıt yöntemleri için geçerlidir. Son olarak, ARIMA Ayrıca, yukarıda açıklanan ortalama teknikleri taşıma hello kullanır. Merhaba çeşitli şekillerde bu yöntemlerin tümü, ne yapıları ARIMA yöntemleri ailesi hello birleşimidir.

Madde işaretleri ve ARIMA yaygın olarak bugün enerji talep tahmin ve diğer birçok tahmin sorunları için kullanılır. Çoğu durumda bunlar toodeliver çok doğru sonuçlar birlikte birleştirilir.

**Genel çoklu regresyon** regresyon modeli hello en önemli modelleme yaklaşım machine learning ve istatistikleri hello etki alanı içinde olabilir. Zaman serisi Hello bağlamında regresyon toopredict hello gelecekteki değerleri kullandığımız (*ör*, isteğe bağlı olarak). Regresyon içinde hello predictors doğrusal bileşimini alın ve bu predictors hello ağırlıkları (Ayrıca başvurulan tooas katsayısını) hello eğitim işlemi sırasında öğrenin. Merhaba, tooproduce bizim tahmin edilen bir değer tahmin regresyon satır hedeftir. Merhaba hedef değişkeni sayısal olduğunda ve bu nedenle de zaman serisi tahmin uygun regresyon yöntemleri uygundur. Regresyon yöntemleri çok basit regresyon modeller gibi çeşitli yoktur [doğrusal regresyon](https://en.wikipedia.org/wiki/Linear_regression) ve olanları karar ağaçları gibi daha gelişmiş [rastgele ormanlar](https://en.wikipedia.org/wiki/Random_forest), [Neural Ağları](https://en.wikipedia.org/wiki/Artificial_neural_network)ve karar ağaçları Boosted.

Enerji isteğe bağlı bir regresyon sorun tahmin oluşturma bize büyük bir hello gerçek talep zaman serisi veri ve sıcaklık gibi dış etkenler birleştirilebilir bizim veri özellikleri seçerek esneklik sağlar. Seçili hello özellikleri hakkında daha fazla bilgi hello özellik Mühendisliği ele alınmıştır (bkz **veri hazırlığı ve özellik Mühendisliği**) bu playbook bölümü.

Uygulama ve enerji isteğe bağlı tahminleri pilot dağıtımı ile bizim deneyimlerden hello Azure ML kullanılabilen gelişmiş regresyon modeli eğilimindedir tooproduce hello en iyi sonuçlar ve vermiyoruz bulduk bunları kullanın.

## <a name="model-evaluation"></a>Model değerlendirme
Model değerlendirme sahip kritik bir rol hello içinde **modeli geliştirme döngüsü**. Bu adımda hello modeli ve performansını gerçek verilerle doğrulama içine bakın. Adım modelleme hello sırasında hello kullanılabilir veri parçası hello modeli eğitmek için kullanırız. Merhaba değerlendirme aşaması sırasında hello veri tootest hello modeli hello kalanı alın. Pratikte biz yeniden oluşturulamaz ve aynı hello eğitim veri kümesi özellikleri hello içeren hello model yeni verileri besleme anlamına gelir. Ancak, hello doğrulama işlemi sırasında biz hello modeli toopredict hello hedef değişkeni kullanmak yerine hello kullanılabilir hedef değişkeni sağlayın. Biz genellikle toothis işlem modeli Puanlama olarak bakın. Biz sonra hello doğru hedef değerler ve bunları hello olanları tahmin karşılaştırın kullanırsınız. Burada amaç Hello toomeasure olan ve hello tahminleri hello true değeri arasındaki hello fark anlamına hello tahmin hata en aza indirmek. Biz toofine ayarlama hello modeli ister ve hello hata gerçekte azalan olup olmadığını doğrulamak beri hello hata ölçüm niceleme anahtardır. İşlem öğrenme hello denetim modeli parametreleri değiştirerek veya ekleyerek veya kaldırarak veri özellikleri ince ayar yapma hello modeli yapılabilir (tooas başvurulan [parametreleri tarama](https://channel9.msdn.com/Blogs/Azure/Data-Science-Series-Building-an-Optimal-Model-With-Parameter-Sweep)). Pratikte, biz modelleme, hello özellik Mühendisliği arasında tooiterate gerekir ve mümkün tooreduce hello hata gerekli toohello düzey gerçekleştirildiğine kadar Değerlendirme Aşaması birden çok kez model anlamına gelir.

Merhaba tahmin hata hiçbir zaman sıfır olarak var olmaz tooemphasis hiçbir zaman, her sonucu mükemmel tahmin edebilirsiniz bir modelidir önemlidir. Ancak, belirli büyüklüğünü hello iş tarafından kabul edilebilir hata yoktur. Bizim modeli tahmin hata Merhaba düzey veya hello iş dayanıklılık daha iyi düzey tooensure Hello doğrulama işlemi sırasında isteriz. Bu nedenle tooset hello hello tolerable hata hello hello başında düzeyini döngüsü sırasında hello önemlidir **sorun Formülasyonu** aşaması.

### <a name="typical-evaluation-techniques"></a>Tipik değerlendirme teknikleri
Hangi tahmin hata ölçülen quantified ve çeşitli yolları vardır. Bu bölümde değerlendirme teknikleri ilgili tootime serisi ve tahmin enerji talep için özel biz hello tartışma odaklanır.

#### <a name="mapehttpsenwikipediaorgwikimeanabsolutepercentageerror"></a>[**MAPE**](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
MAPE ortalama mutlak yüzdesi hata anlamına gelir. İle MAPE biz hello fark her tahmini noktası ve o noktasının hello gerçek değer arasında bilgi işlem. Biz sonra hello hata noktası başına hello fark göreli toohello gerçek değer hello oranını hesaplayarak ölçme. Son adımda bu değerleri ortalama. MAPE için kullanılan hello matematiksel formül hello aşağıda verilmiştir:

![MAPE formülü](media/cortana-analytics-playbook-demand-forecasting-energy/mape-formula.png)
*burada A<sub>t</sub> hello gerçek değer, F<sub>t</sub> hello tahmin edilen bir değer ve n hello yatay tahmin.*

## <a name="deployment"></a>Dağıtım
Biz aşaması modelleme hello nailed ve hello modeli performans doğrulanmış sonra hello dağıtım aşaması içine hazır toogo duyuyoruz. Bu bağlamda dağıtım hello müşteri tooconsume hello modeli gerçek tahminleri üzerinde büyük ölçekte çalıştırarak anlamına gelir. Merhaba dağıtımının kavramdır Azure ML anahtarında ana Amacımız tooconstantly olduğundan hello Insight hello verilerden alma karşılıklı toojust olarak tahminleri çağırma. Merhaba dağıtım aşaması hello burada büyük ölçekte tüketilen hello modeli toobe etkinleştirme bir parçasıdır.

Tahmin enerji talep Hello bağlamında, bizim AIM tooinvoke sürekli ve düzenli tahminleri hello model için yeni veriler kullanılabilir ve bu hello geri toohello tüketim istemci gönderilen veri tahmini sağlarken ' dir.

### <a name="web-services-deployment"></a>Web Hizmetleri dağıtımı
Merhaba ana dağıtılabilir yapı taşıdır Azure ML hello web hizmetidir. Merhaba en etkili şekilde tooenable tüketimini hello bulutta Tahmine dayalı bir modeli budur. Merhaba Web hizmeti hello modeli yalıtır ve ile sarmalar bir [RESTful](http://www.restapitutorial.com/) API (uygulama programlama arabirimi). Merhaba API hello diyagramda gösterildiği gibi herhangi bir istemci kod parçası olarak kullanılabilir.

![Hizmet dağıtımı ve kullanımı](media/cortana-analytics-playbook-demand-forecasting-energy/web-service-deployment-and-consumption.png)

Görüldüğü gibi hello web hizmeti hello Cortana Intelligence Suite bulut dağıtılır ve kullanıma sunulan, REST API uç noktası üzerinden çağrılabilir. Çeşitli etki alanlarında istemciler farklı türde hello hizmeti hello Web API aracılığıyla aynı anda çalıştırabilirsiniz. Hello web hizmeti ayrıca eş zamanlı çağrıları binlerce destekleyecek şekilde ölçeklendirebilirsiniz.

### <a name="a-typical-solution-architecture"></a>Tipik çözüm mimarisi
Çözüm tahmin enerji isteğe bağlı dağıtırken, hello tahmin web hizmeti gider ve hello tüm veri akışı kolaylaştıran bir bitiş tooend Çözüm dağıtımı konusuna ilgi duyan duyuyoruz. Size yeni bir tahmini çağırma hello zaman, biz toomake hello modelin güncel verileri özelliklerle sat emin gerekir. Bu, toplanan ham verileri sürekli alınan, işlenen ve hangi hello model oluşturulmuş hello gerekli özelliğini içine dönüştürülen bu hello yeni anlamına gelir. AT hello aynı zaman, hello için kullanılabilir veri kaybı istemcileri sona toomake hello tahmini gibi biz gerekir. Bir örnek veri akışı döngüsü (veya veri ardışık) hello şemada aşağıda gösterilmiştir:

![Enerji talep tahmin son tooEnd veri akışı](media/cortana-analytics-playbook-demand-forecasting-energy/energy-demand-forecase-end-data-flow.png)

Merhaba enerji talep tahmin döngüsü bir parçası olarak gerçekleşmesi hello adımları şunlardır:

1. Dağıtılan veri ölçümler milyonlarca sürekli güç tüketimi verilerinin gerçek zamanlı olarak veren.
2. Bu veri okunduğunu toplanır ve bir bulut depoya karşıya (*ör*, Azure Blob).
3. İşlenmeden önce hello ham toplanmış tooa alt istasyon veya bölgesel düzeyinde hello iş tarafından tanımlanan verilerdir.
4. Merhaba özelliği işleme (bkz **veri hazırlığı ve özellik işleme**) sonra gerçekleşir ve üretir hello için gerekli olan bir veri modeli eğitim veya Puanlama – hello özellik kümesi verilerinin bir veritabanında depolanan (*ör*, SQL Azure).
5. Hizmet yeniden eğitim hello çağrıldığında toore tren hello hello modeli sürümüne güncelleştirilmiş model – tahmin, böylece web hizmeti Puanlama hello tarafından kullanılabilir kalıcıdır.
6. Web hizmeti Puanlama hello gerekli hello tahmin sıklığı uygun bir zamanlamaya göre çağrılır.
7. Merhaba, veri hello son tüketim istemci tarafından erişilebilir bir veritabanında depolanan tahmini.
8. Merhaba tüketim istemci hello tahminleri alır, geri hello kılavuza uygular ve gerekli hello kullanım örneği uygun olarak kullanır.

Bu, tüm bu döngüsünü tamamen otomatik ve bir zamanlamaya göre çalışan önemli toonote olur. Bu veri döngüsü Hello tüm orchestration gibi araçları kullanarak yapılabilir [Azure Data Factory](http://azure.microsoft.com/services/data-factory/).

### <a name="end-tooend-deployment-architecture"></a>End tooEnd dağıtım mimarisi
Sipariş toopractically enerji talep tahmin çözümünü Cortana Intelligence üzerinde dağıtmak, gerekli hello bileşenleri kurulmuş ve doğru şekilde yapılandırıldığını tooensure ihtiyacımız.

Merhaba Aşağıdaki diyagramda uygulayan ve yukarıda açıklanan hello veri akışı döngüsü düzenler tipik bir Cortana Intelligence tabanlı mimari gösterilir:

![End tooEnd dağıtım mimarisi](media/cortana-analytics-playbook-demand-forecasting-energy/architecture.png)

Her bir hello bileşenleri ve hello tüm mimarisi hakkında daha fazla bilgi için lütfen toohello enerji çözüm şablonu bakın.

