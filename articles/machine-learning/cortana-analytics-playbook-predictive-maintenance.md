---
title: "Azure - Cortana Intelligence çözüm şablonu ile Havacılık aaaPredictive bakım | Microsoft Docs"
description: "Microsoft Cortana Intelligence Tahmine dayalı bakım Havacılık, yardımcı programlar ve taşıma için bulunduğu bir çözüm şablonu."
services: cortana-analytics
documentationcenter: 
author: fboylu
manager: jhubbard
editor: cgronlun
ms.assetid: 2e8b66db-91eb-432b-b305-6abccca25620
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: fboylu
ms.openlocfilehash: da863a89d2409a8b56b23066f15b4da13e1cd3d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-template-playbook-for-predictive-maintenance-in-aerospace-and-other-businesses"></a>Cortana Intelligence çözüm şablonu Playbook Havacılık ve diğer işletmelerin Tahmine dayalı bakım
## <a name="executive-summary"></a>Özet
Tahmine dayalı bakım hello biridir maliyet tasarrufu inanılmaz miktarı gibi unarguable avantaj talep Tahmine dayalı analiz uygulamalarının en. Bu playbook önemli kullanım örneklerini hello vurguyu ile Tahmine dayalı bakım çözümler için bir başvuru sağlamaya amaçlar.
Hazırlanan toogive hello okuyucu hello en yaygın iş senaryolarına Tahmine dayalı bakım, bu tür çözümler için iş sorunlarını uygun zorluklar anlaşılması, veri gerekli toosolve bu iş sorunlarını Tahmine dayalı modelleme Bu tür veri ve en iyi uygulamaları örnek çözüm mimarileri ile kullanan teknikleri toobuild çözümler.
Ayrıca hello özellikleri açıklanır özellik mühendisliği gibi geliştirilen hello Tahmine dayalı modelleri, geliştirme ve performans değerlendirme model. Esas olarak, bu playbook birlikte hello iş ve başarılı geliştirme ve Tahmine dayalı bakım Çözüm dağıtımı için gerekli analitik yönergeleri getirir. Hazırlanan toohelp hello İzleyici Cortana Intelligence Suite kullanarak ilk çözümünü oluşturun ve özellikle Azure Machine başlangıç olarak Learning noktası kendi uzun vadeli Tahmine dayalı bakım stratejisi bu yönergeleri. Merhaba Cortana Intelligence Suite ve Azure Machine Learning ile ilgili belgeler bulunabilir [Cortana Analytics](http://www.microsoft.com/server-cloud/cortana-analytics-suite/overview.aspx) ve [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) sayfaları.

> [!TIP]
> Bu çözüm şablonu tooimplementing teknik kılavuzu için bkz: [Tahmine dayalı bakım için teknik Kılavuzu toohello Cortana Intelligence çözüm şablonu](cortana-analytics-technical-guide-predictive-maintenance.md).
> Bu şablon mimari bir genel bakış sağlayan bir diyagram toodownload bkz [hello Cortana Intelligence çözüm şablonu Tahmine dayalı bakım mimarisini](cortana-analytics-architecture-predictive-maintenance.md).
> 
> 

## <a name="playbook-overview-and-target-audience"></a>Playbook genel bakış ve hedef kitle
Bu playbook düzenli toobenefit olan çeşitli arka planlar ve Tahmine dayalı bakım alanı ilgi teknik ve teknik olmayan İzleyici. Merhaba playbook kapsayan iki üst düzey boyutlarının hello farklı Tahmine dayalı bakım çözümü türleri ve nasıl ayrıntılarını tooimplement bunları. Merhaba içeriği, yalnızca uygulamalar hem de tooimplement arayan çözüm alanı ve hello türü bu çözümleri anlamak isteyen ve bu nedenle teknik ayrıntılara ilgilendiğiniz hem toohello İzleyici karşılamak amacıyla dengelenir.

Bu playbook hello içeriği çoğunluğu önceki veri bilimi bilgi veya uzmanlığı varsaymaz. Ancak, bazı bölümleri hello playbook biraz veri bilimi kavramları toobe uygulama ayrıntılarını uygulayabilmek için aşina gerektirir. Giriş düzeyinde veri bilimi yetenekleri olan gerekli hello malzeme Bu bölümlerdeki düzeyinden toofully yararlanın.

Merhaba ilk hello playbook yarısı bir giriş toopredictive bakım uygulamalarını kapsamaktadır, iş sorununu hello ayrıntılarla tooqualify Tahmine dayalı bakım çözümü, ortak kullanım koleksiyonu durumlarda nasıl bu kullanma çevreleyen veri hello durumları ve hello iş avantajları, bu Tahmine dayalı bakım çözümleri uygulamak. Bu bölümler hello Tahmine dayalı analiz etki alanındaki tüm teknik bilgi gerektirmez.

Merhaba ikinci yarısında hello playbook hello Tahmine dayalı modelleme teknikleri Tahmine dayalı bakım uygulamalar ve bu modeller hello ilk hello playbook yarısında özetlenen hello kullanım örnekleri örneklerinden aracılığıyla uygulama türlerini kapsar. Bu model verileri etiketleme ve mühendislik, özellik seçimi, eğitim ve sınama ve performansı en iyi yöntemler değerlendirme gibi verileri ön işleme adımları boyunca giderek gösterilmiştir. Bu bölüm, teknik İzleyici için uygundur.

## <a name="predictive-maintenance-in-iot"></a>IOT Tahmine dayalı bakım
Merhaba zamanlanmamış ekipman kapalı kalma süresi etkisi işletmeler için son derece zararlı olabilir. Bu sipariş toomaximize kullanımı ve performans ve pahalı, zamanlanmamış kapalı kalma süresini en aza çalıştırmaya kritik tookeep alan ekipman olur. Yalnızca hello hatası toooccur bekleniyor bugünün iş işlemleri Sahne uygun maliyetli değildir. tooremain rekabet, şirketler aramak için yeni yollar toomaximize varlık performans yaparak hello verilerin kullanımını toplanan çeşitli kanaldan. Bir önemli yolu tooanalyze geçmiş desenleri toopredict gelecekteki sonuçları kullanan tooutilize Tahmine dayalı analitik teknikleri gibi bilgilerdir. Merhaba bu çözümlerin en popüler birini hangi olarak genellikle tanımlanabilir, ancak bunlarla sınırlı toopredicting hello varlıklar olabilir, hello tooproactively izlenen şekilde yakın bir varlığı hata olasılığını belirlemek Tahmine dayalı bakım çağrılır hataları ve hello hataları oluşmadan önce eylemi gerçekleştirin. Bu çözümlerin hatanın hello en yüksek risk altındadır hatası desenleri toodetermine varlıklar algıla. Bu sorunların erken kimliği sınırlı bakım kaynakları daha düşük maliyetli bir şekilde dağıtmasını ve kalitesini geliştirmek ve tedarik zinciri süreçlerinin yardımcı olur.

Hello neden hello nesnelerin interneti (IOT) uygulamalar, bakım hello dünyasında hello veri toplama olarak artan dikkat kazanmasını ve teknolojileri işleme yeterli toogenerate olgunlaştığından Tahmine dayalı ile iletme, depolamak ve tüm Çözümle Toplu veya gerçek zamanlı veri türleri. Kolay geliştirme gibi teknolojiler etkinleştirin ve tartışmaya açık bir şekilde hello en büyük avantajı sağlama Tahmine dayalı bakım çözümleriyle analiz çözümleri ile uçtan uca çözümler dağıtımını Gelişmiş.

İş sorunlarını hello Tahmine dayalı bakım etki alanı aralığında işletimsel yüksek risk toounexpected hatalarını ve sorunlarını karmaşık iş ortamlarında hello kök nedenini sınırlı bir anlayış son. Bu sorunları Hello çoğunluğu kategorilere ayrılmış toofall iş sorularını aşağıdaki hello altında olabilir:

* Merhaba yakın bir ekipman parçasını başarısız hello olasılık nedir?
* Merhaba kalan kullanım ömrü hello donanımların nedir?
* Hello nelerdir hataları ve Bakım eylemleri gerçekleştirilen toofix olmalıdır bu sorunların neden olur?

Tahmine dayalı bakım tooanswer yararlanarak bu soruları işletmeler yapabilirsiniz:

* İşletimsel riskini azaltmak ve bunlar oluşmadan önce hataları belirleme varlıklar üzerinde geri dönüş oranını artırmak
* Gereksiz zamana dayalı bakım işlemlerini azaltmak ve bakım maliyetini denetleme
* Genel marka görüntü geliştirmek, hatalı tanıtım ve sonuçta elde edilen kayıp satış müşteri attrition ortadan kaldırmak.
* Stok düzeylerini sipariş noktayı tahmin ederek çalışmasını azaltarak stok maliyetleri
* Desenler bağlı toovarious bakım sorunları bulma

Tahmine dayalı bakım çözüm durumu puanları toomonitor gerçek zamanlı varlık koşul hello varlıklar, ileriye dönük bakım etkinlikler için öneri Sysprep'in kalan tahmini gibi anahtar performans göstergelerinin işletmeler sağlayabilir ve yedek parçaların tahmini sipariş tarihleri.

## <a name="qualification-criteria-for-predictive-maintenance"></a>Tahmine dayalı bakım için nitelik ölçütleri
Tüm kullanım veya iş sorunlarını tarafından Tahmine dayalı bakım etkili bir şekilde çözülebilir önemli tooemphasize olur. Önemli hello sorun önceden ve en önemlisi, algılandığında, sipariş tooprevent başarısızlık eyleminin düz bir yolu var doğası gereği Tahmine dayalı olup niteliği ölçütünü dahil yeterli kalite toosupport hello verilerle kullanım örneği kullanılabilir. Burada, biz başarılı Tahmine dayalı bakım çözümü oluşturmak için hello veri gereksinimlerine odaklanır.

Tahmine dayalı modeller oluştururken, gizli desenleri tanıyabilir ve daha fazla hello gelecekteki verilerdeki bu düzenleri tanımlamak geçmiş verileri tootrain hello modeli kullanırız. Bu modeller, özelliklerini ve tahmin hello hedefi tarafından açıklanan örnekleriyle eğitilmiş olup. Merhaba eğitilen beklenen toomake tahminleri hello hedefte hello yeni örneklerin hello özellikleri yalnızca bakarak modelidir. Merhaba modeli yakalama hello ilişkisi bulunduğunu çok önemlidir ve tahmin hedefinin hello. Düzende etkili makine öğrenimi modeli bağımsız olarak bir tahmin anlamı hello veri hello hedef doğrultusunda Tahmine dayalı güç olan özellikler içeren eğitim verilerini ihtiyacımız tootrain ilgili toohello tahmin hedef tooexpect doğru olması gerekir tahminleri.

Örneğin, Hello hedef tren Tekerlek toopredict hatalarının ise, verileri eğitim hello tekerleği ilgili özelliklerin (Merhaba sistem durumunu tekerlek, hello mesafe, car yük vb. yansıtma örneğin telemetri.) içermelidir. Merhaba hedef toopredict tren altyapısı hataları ise, ancak biz büyük olasılıkla başka bir altyapısı güvenlikle ilgili özellikler sahip eğitim veri kümesi gerekir. Tahmine dayalı modeller oluşturmanın önce hello iş Uzman toounderstand hello veri ilgi gereksinimi beklediğiniz ve gerekli tooselect ilgili veri alt kümesi hello çözümleme için olan hello etki alanı bilgi sağlayın.

Biz Tahmine dayalı bakım çözümü için uygun bir iş sorunu toobe uygun olduğunda aramak için üç temel veri kaynağı vardır:

1. Hata geçmişi: Genellikle, Tahmine dayalı bakım uygulamalarda hata çok nadir olaylardır. Ancak, hataları tahmin Tahmine dayalı modeller oluştururken, hello hatası düzeni hello eğitim işlemiyle yanı sıra toolearn hello normal işlem düzeni hello algoritması gerektiriyor. Bu nedenle, hello eğitim verileri bu iki farklı desenleri sipariş toolearn iki kategoride örneklerde yeterli sayıda içeren gereklidir. Bu nedenle, veri hatası olaylarının yeterli sayıda olmasını gerektirir. Hata olayları bakım kayıtları ve bölümleri değiştirme geçmişi veya veri hello etki alanı uzmanlar tarafından tanımlandığı gibi hataları olarak da kullanılabilir hello eğitim daha fazla bilgi bulunabilir.
2. Bakım/onarma geçmişi: Temel bir Tahmine dayalı bakım çözümleri için veri kaynağı olan Merhaba yerini hello bileşenler hakkında bilgi içeren hello varlık ayrıntılı bakım geçmişini, önleyici bakım gerçekleştirilen, vb. etkinleştirir. Bu olaylar bu etkileyen hello düşüşü desenleri ve bu bilgileri yokluğu olarak neden yanıltıcı toocapture sonuçları son derece önemlidir.
3. Makine koşullar: başarısız önce sipariş toopredict kaç daha fazla gün (saat, mil, işlemler, vb.) bir makine sürer hello makinenin sistem durumu düşürür çalışması sırasında zamanla varsayıyoruz. Bu nedenle, bu eskime deseni yakalayan hello veri toocontain zaman değişen özellikleri ve toodegradation müşteri adayları anormallikleri bekliyoruz. IOT uygulamalarında iyi bir örnek farklı algılayıcılar hello telemetri verilerini temsil eder. Bir makine toofail bir zaman çerçevesinde edecekse sipariş toopredict ideal hello verilerini düşürmesini eğilimi bu zaman dilimi önce hello gerçek hata olayı sırasında yakalama.

Ayrıca, doğrudan veri hello hedef varlık öngörme koşullarını işletim toohello ilgili gerektirir. Merhaba karar hedef hem de iş gereksinimlerinize ve veri kullanılabilirliğine bağlıdır. Alma hello eğitmek tekerleği hatası tahmin örnek olarak, biz tahmin "Merhaba tekerleği giderek toohave hata ise" veya "Merhaba tüm tren bir sorununuz edecekse". İkincisi hello tren başarısızlığını hedefler ancak hello ilk biri daha belirli bir bileşeni hedefler. Merhaba ikinci birinci daha zor toobuild bir model kolaylaştırarak hello daha çok daha fazla dağınık veri öğeleri gerektirir daha genel bir soru olabilir. Merhaba bileşen düzeyinde bilgi içermiyor olarak buna karşılık, yalnızca hello üst düzey tren koşul veri bakarak toopredict Tekerlek hataları çalışırken uygun olmayabilir. Genel olarak, bu daha genel olanları daha fazla duyarlı toopredict belirli hata olayları gösterir.

Genellikle hatası geçmiş verileri hakkında sorular bir ortak Soru "nasıl gerekli tootrain bir model ve kaç tane"yeterli"kabul edilen birçok hata olayları misiniz? Hiçbir açık yanıt toothat soru birçok Tahmine dayalı analiz senaryolarında olduğu gibi genellikle kabul edilebilir nedir belirleyen hello veri hello kalitesini olur. Merhaba dataset ilgili toofailure tahmin özellikleri içermiyorsa, birçok hata olayları olsa bile sonra iyi bir model oluşturmak mümkün olmayabilir. Ancak, hello hello daha fazla hello hata olayları hello daha iyi hello modeli ve kaç tane hata örnekleri gereklidir, kabaca bir tahmin çok bağlamını ve veri bağımlı ölçü olduğunu udur. Bu sorunun nerede biz yöntemleri toocope yeterli hataları olmaması, hello sorunla önermek imbalanced veri kümeleri işlemek için hello bölümünde ele alınmıştır.

## <a name="sample-use-cases"></a>Örnek kullanım durumları
Bu bölümde, Tahmine dayalı bakım kullanım örneklerinden Havacılık, yardımcı programlar ve taşıma gibi birkaç sektörlerde koleksiyonu odaklanır. Her alt ayrıntısına hello kullanım örnekleri içine bu alanlarından toplanır ve bir iş sorununu, hello veri çevresindeki hello iş sorununu ve Tahmine dayalı bakım çözümü hello yararları anlatılmaktadır.

### <a name="aerospace"></a>Havacılık
#### <a name="use-case-1-flight-delay-and-cancellations"></a>Kullanım örneği 1: Uçuş gecikmesi ve iptalleri
##### <a name="business-problem-and-data-sources"></a>*İş sorun ve veri kaynakları*
Merhaba önemli iş sorunlarını bu airlines yüz toomechanical sorunları erteleniyor uçuşlar ilişkilendirilmiş hello önemli maliyetleri biridir. Merhaba mekanik hatası onarılamıyorsa uçuşlar bile iptal edilebilir. Bu, son derece gecikmeler zamanlama ve işlemleri, nedenleri hatalı saygınlığı ve diğer birçok sorunu birlikte müşteri memnuniyetsizliği sorunları oluştururken maliyetlidir. Airlines, özellikle, böylece uçuş gecikmeler veya iptalleri azaltabilir böyle mekanik hataları önceden tahmin ilgilendiğiniz. Merhaba amacı hello Tahmine dayalı bakım çözümü bu durumlarda, uçak olma toopredict hello olasılıktır Gecikmeli veya iptal edilen, ilgili veri kaynaklarına bakım geçmişi ve uçuş rota bilgilerini gibi temel. Bu kullanım durumu için iki önemli veri kaynaklarını Hello hello uçuş ayaktan ve sayfa günlükleri ' dir. Uçuş leg veri hello uçuş rota ayrıntıları hello tarih ve saat ayrılma ve varış, ayrılma ve varış havaalanları, vb. gibi ilgili veriler içerir. Sayfa günlük verileri bir dizi hello bakım personeli tarafından kaydedilen hata ve bakım kodları içerir.

##### <a name="business-value-of-hello-predictive-model"></a>*Merhaba Tahmine dayalı bir model iş değeri*
Merhaba kullanılabilir geçmiş verileri kullanarak Tahmine dayalı bir model sonraki 24 saat gecikmesini ya da uçuş hello içinde iptal edilir mekanik sorunu çok sınıflandırma algoritmasıdır toopredict hello türü kullanılarak oluşturuldu. Bu tahmin yaparak, gerekli bakım Eylemler Uçağın hizmet ederken toomitigate hello risk alınabilir ve böylece olası gecikmeler veya iptalleri engelleyebilirsiniz. Azure Machine Learning web hizmetini kullanarak, hello Tahmine dayalı modelleri sorunsuz bir şekilde ve kolayca airlines var olan işletim platformlarında tümleştirilebilir. 

#### <a name="use-case-2-aircraft-component-failure"></a>Kullanım örneği 2: Uçak bileşeni hatası
##### <a name="business-problem-and-data-sources"></a>*İş sorun ve veri kaynakları*
Uçak motorları ekipman çok hassas ve pahalı parçası olan ve hello en sık kullanılan bakım görevlerini hello uçak sektörünün altyapısı bölümü değişikliklerini arasındadır. Bakım çözümleri airlines için bileşen stok kullanılabilirliği, teslim ve planlama dikkatli yönetim gerektirir. Bileşen güvenilirlik üzerinde mümkün toogather gösterimi olan toosubstantial azaltma yatırım maliyetler doğurur. Bu kullanım durumu için Hello ana veri kaynağı Algılayıcılar'daki hello uçak bilgi sağlayan bir dizi hello uçak hello koşula toplanan telemetri verileri ' dir. Bakım kayıtları da bileşen hatalar oluştu ve değişiklik yapıldı kullanılan tooidentify yoktu.

##### <a name="business-value-of-hello-predictive-model"></a>Merhaba Tahmine dayalı bir model iş değeri
Birden çok sınıf sınıflandırma modeli, bir hata olasılığını tahmin oluşturulan son tooa hello sonraki ay içinde belirli bir bileşen. Bu çözümlerin mimarisi kullanarak airlines bileşen onarım maliyetleri azaltmak, bileşen stok kullanılabilirliğini artırın, ilgili varlıklar stok düzeylerini küçültmek ve Bakım planlama geliştirmek.

### <a name="utilities"></a>Yardımcı programlar
#### <a name="use-case-1-atm-cash-dispense-failure"></a>Kullanım örneği 1: ATM nakit hatası etiket.
##### <a name="business-problem-and-data-sources"></a>*İş sorun ve veri kaynakları*
Birincil işletimsel risk tootheir işletmeler olduğunu varlıklarına beklenmeyen hatalarının Yöneticiler varlık yoğun sektörlerde genellikle durum içinde. Örnek olarak, endüstri bankacılık içinde makineler ATM gibi başarısızlığını sıklıkla ortaya çok yaygın bir sorundur. Bu tür sorunları gibi makine işleçler için Tahmine dayalı bakım çözüm çok istenen olun. Bu kullanım örneğinde tahmin sorun ATM nakit mevzuatı işlem kağıt sıkıştı gibi hello nakit dağıtıcısının tooa hatası veya bir bölümü hatası kesintiye uğrarsa toocalculate hello olasılıktır. Ana veri bu durumda nakit notları dispensed sırada ölçümleri toplamak sensör okumaları ve aynı zamanda bakım kayıtları toplanan zamanla kaynaklarıdır. Tamamlanan her işlem başına sensör okumaları ve ayrıca sensör okumaları dispensed her Not başına algılayıcı verilerini dahil. Notlar, kalınlığı arasındaki boşlukları gibi Hello algılayıcı sağlanan okumalar ölçümleri varış uzaklığı vb. unutmayın. Bakım veri, hata kodları ve onarım bilgileri dahil. Bu, kullanılan tooidentify hata durumları olan.

##### <a name="business-value-of-hello-predictive-model"></a>*Merhaba Tahmine dayalı bir model iş değeri*
İki tahmine dayalı modelleri hello nakit mevzuatı işlemlerde toopredict hataları ve hello notları tek tek bir işlem sırasında dispensed başarısızlık oluşturulmuştur. Mümkün toopredict işlem hataları önceden olma yoluyla, ATM olabilir proaktif olarak oluşmasını tooprevent hataları hizmet. Ayrıca, Not hatası tahmin, bir işlem olasılığı varsa tooa Not tamamlanmadan toofail barkod hata, en iyi toostop hello işlemi ve tamamlanmamış işlem hello müşteri yerine hello Bakım hizmeti bekleniyor uyar toolarger müşteri memnuniyetsizliği neden olabilir Hello hata oluştuktan sonra tooarrive.

#### <a name="use-case-2-wind-turbine-failures"></a>Kullanım örneği 2: Rüzgar Türbin hataları
##### <a name="business-problem-and-data-sources"></a>*İş sorun ve veri kaynakları*
Ortam tanıma hello olursa, Rüzgar turbines enerji nesil hello başlıca kaynaklarından biri duruma gelmiş ve bunlar genellikle milyonlarca dolar maliyeti. Merhaba anahtar Rüzgar turbines bileşenlerinin bulunur hello Oluşturucu motor toomonitor Türbin koşullar ve durum yardımcı olacak birçok algılayıcılar ile biridir. Merhaba sensör okumaları kullanılan toobuild Tahmine dayalı bir model toopredict olabilen değerli bilgiler içeren hello Rüzgar Türbin bileşenleri için ortalama zamanı toofailure gibi kritik anahtar performans göstergelerini (KPI'lar). Bu kullanım örneği için veriler üç farklı grubu konumda bulunan birden çok Rüzgar turbines gelir. Ölçümler her Türbin gelen yüz algılayıcılar 10 dakikada bir yıl için kaydedilmiş bir tooa kapatın. Bu okumalar sıcaklık, oluşturucu hızı, Türbin güç ve oluşturucu sargı gibi ölçüleri içerir.

##### <a name="business-value-of-hello-predictive-model"></a>*Merhaba Tahmine dayalı bir model iş değeri*
Tahmine dayalı modelleri tooestimate kalan kullanım ömrü oluşturucuları ve sıcaklık algılayıcıları için oluşturulmuştur. Hata, teknisyenleri büyük olasılıkla toofail yakında olan şüpheli turbines üzerinde odaklanabilirsiniz bakım Hello olasılık toocomplement zamana dayalı bakım regimes tahmin ederek çalışmasını.
Ayrıca, Tahmine dayalı modelleri Insight toohello farklı Etkenler toohello sorunların temel nedeni iş toohave hello kök daha iyi anlamasına yardımcı olan bir hata olasılığını katkısı düzeyini duruma getirin.

#### <a name="use-case-3-circuit-breaker-failures"></a>Kullanım örneği 3: devre kesici hataları
##### <a name="business-problem-and-data-sources"></a>*İş sorun ve veri kaynakları*
Oluşturma, dağıtım ve elektrik enerji satışının dahil elektrik ve gaz işlemler enerji toohouseholds tooguarantee teslimini güç satırları hiç işletimsel olduğundan emin olmak için bakım önemli miktarda zaman gerektirir. Bu tür işlemler başarısız neredeyse her varlık güç sorunları ortaya hello bölgelerde parametreden gibi kritik öneme sahiptir. Bağlantı hattı ayırıcıları bir elektrik geçerli sorunları ve kısa devreler tooprevent durumunda tüm oluşmasını zarar toopower satırlarından Kes ekipman parçasını oldukları gibi bu tür işlemler için kritik öneme sahiptir. Verilen bakım günlükleri, komut geçmişi ve teknik belirtimler toopredict devre kesici hataları bu kullanım örneği için iş sorunudur.

Bu durumda üç ana veri kaynağı düzeltme, önleyici ve sistematik eylemlerini içeren bakım günlüklerin, açma ve kapama eylemler ve teknik toocircuit ayırıcıları gibi otomatik ve el ile komutları içeren işletimsel verileri gönder Her devre kesici yıl yaptığınız gibi konum, model, vb. özelliklerini ilgili belirtimi verileri.

##### <a name="business-value-of-hello-predictive-model"></a>*Merhaba Tahmine dayalı bir model iş değeri*
Tahmine dayalı bakım çözüm onarım maliyetleri azaltmak ve donanımların hattı ayırıcıları gibi hello yaşam döngüsü artırmak yardımcı olur. Bu modeller de toofewer kesintiler toohello hizmet sağlama beklenmeyen hataları azaltır uyarıları önceden modelleri sağlayan bu yana hello güç ağ hello kalitesini geliştirilmesine yardımcı olun.

#### <a name="use-case-4-elevator-door-failures"></a>Kullanım örneği 4: Fırsatınızdır kapı hataları
##### <a name="business-problem-and-data-sources"></a>*İş sorun ve veri kaynakları*
En büyük fırsatınızdır şirketlerin tipik olarak Merhaba Dünya çalıştıran asansörler milyonlarca vardır. toogain rekabet, bunlar ne tootheir müşterilerin çoğu önemli olan güvenilirlik odaklanın. Asansörler toohello bulut bağlayarak ve fırsatınızdır algılayıcılar ve sistemlerden, veri toplamayı hello nesnelerin interneti, Hello potansiyelinin çizim işlemleri tarafından çok artıran değerli iş zekası uygulamasına mümkün tootransform veri oldukları henüz kullanılabilir toohello rakiplere olan şey olmayan Tahmine dayalı ve PreEmptive tarafından bakım sunar. Bu durumda Hello iş gerekliliği kapı hatalarının olası hello tahmin bir Bilgi Bankası Tahmine dayalı uygulamanın neden tooprovide olduğu. Merhaba gerekli bu uygulama için verileri kullanım bilgilerini (örneğin sayısı kapı döngüleri, ortalama kapı Kapat zaman, vb.) (örneğin tanımlayıcıları sözleşme bakım sıklığı, yapı türü, vb.) fırsatınızdır statik özellikleri olan üç bölümden oluşur ve hata geçmişi (yani geçmiş hata kaydeder ve bunların nedenleri).

Çok sınıflı Lojistik regresyon modeli Azure Machine Learning toosolve hello tahmin sorun oluşturuldu, statik özellikleri ve kullanım verileri özellikler ve geçmiş başarısızlığı kayıtları sınıfı etiket olarak hello nedenleri olarak hello ile tümleşiktir. Bu Tahmine dayalı bir model tüketilen toohelp alan teknisyen tarafından kullanılan bir mobil cihazda bir uygulama tarafından çalışma verimliliği artırmak. Bir teknisyen site toorepair üzerinde bir fırsatınızdır gittiğinde klasöründe önerilen neden olur ve en iyi kurslar bakım eylemleri toofix hello fırsatınızdır kapı kadar hızlı toothis uygulama başvurabilir.

### <a name="transportation-and-logistics"></a>Taşıma ve lojistik
#### <a name="use-case-1-brake-disc-failures"></a>Kullanım örneği 1: Fren disk hataları
##### <a name="business-problem-and-data-sources"></a>*İş sorun ve veri kaynakları*
Tipik bakım araçları için düzeltme ve önleyici bakım ilkelerdir. Düzeltme bakım ciddi rahatsızlıktan toohello sürücü üzerinde ziyaret toomechanic küçülttüğü iyi bir şekilde beklenmeyen bir arıza ve hello zaman sonucunda neden olabilir bir hata gerçekleştikten sonra o hello araç onarılana anlamına gelir. Çoğu araçları Ayrıca belirli incelemeleri hesap hello gerçek koşulu hello araba alt sistemleri almaz bir zamanlamasında gerçekleştirilmesi konu tooa önleyici bakım İlkesi değildir. Bu yaklaşım hiçbiri tam olarak sorunların giderilmesinde başarılı. Merhaba belirli kullanım burada Fren disk hatası tahmin geçmiş yönlendirmeli desenleri ve bir araba lastiği sistem hello yüklü algılayıcılar yoluyla toplanan verileri temel alan bir durumdur ve araba hello başka koşullar gösterilir. Merhaba en önemli verileri bu durumda, örneğin, yürüten uzaklıkları, hız, vb. düzenleri braking ivmelerini ölçmek hello algılayıcı verilerini kaynağıdır. Bu bilgiler, bağlı diğer statik gibi bilgiler araba özellikleri iyi bir Tahmine dayalı bir model kullanılabilir predictors kümesi Yardım derleme. Başka bir önemli bilgi bölümü sipariş veritabanından olayla hello hatası verileri kümesidir (kullanılan tookeep hello yedek parça sipariş tarihleri ve sayıları araba hello dealerships işlendikçe).

##### <a name="business-value-of-hello-predictive-model"></a>*Merhaba Tahmine dayalı bir model iş değeri*
Merhaba iş burada Tahmine dayalı bir yaklaşım önemli değeridir. Tahmine dayalı bakım sistem Tahmine dayalı bir modeli temelinde ziyaret toohello dağıtıcı zamanlayabilirsiniz. Merhaba modeli hello araba ve geçmiş yürüten hello geçerli durumunu hello temsil eden sensory bilgileri bağlı olabilir. Bu yaklaşım hello sonraki düzenli bakım önce de oluşabilir beklenmeyen hatalar hello riskini en aza indirebilirsiniz.
Ayrıca, gereksiz önleyici bakım hello miktarını da azaltabilirsiniz. Sürücü bölümleri, bir değişiklik birkaç hafta ve bu bilgilerle tedarik hello dağıtıcı gerekli olabileceğini proaktif olarak haberdar olmak. Merhaba dağıtıcı sonra hello sürücü için bir bireysel bakım paket önceden hazırlayın.

#### <a name="use-case-2-subway-train-door-failures"></a>Kullanım örneği 2: Yeraltı treni tren kapı hataları
##### <a name="business-problem-and-data-sources"></a>*İş sorun ve veri kaynakları*
Merhaba önemli nedenlerinden gecikmeleri ve sorunları Yeraltı treni işlemlerini tren araba kapı hatalarının biridir. Tren araba kapı hatası veya mümkün tooforecast hello hello sonraki door hatası, kasa gün sayısı olması gerekecekse tahmin etmeye son derece önemli öngörü olur. Merhaba fırsat toooptimize tren kapı bakım sağlar ve hello eğitimi kullanıcının kesinti azaltın.

#### <a name="data-sources"></a>Veri kaynakları
Bu kullanım örneğindeki verilerin üç kaynakları 

* **Olay verileri eğitmek**, hello geçmiş kayıtlarını tren olayların olduğu 
* **Bakım verileri** bakım türleri, iş emri türleri ve öncelik kodları gibi  
* **hataları kayıtlarını**.

##### <a name="business-value-of-hello-predictive-model"></a>*Merhaba Tahmine dayalı bir model iş değeri*
İki modeli ikili sınıflandırma ve gün regresyon kullanarak hatanın kasa kullanarak toopredict sonraki gün hatası olasılığını oluşturulmuştur. Benzer şekilde hello önceki durumlarda, hello modelleri inanılmaz fırsat tooimprove hizmet kalitesi oluşturun ve hello düzenli bakım regimes depolamanın tarafından müşteri memnuniyetini artırın.

## <a name="data-preparation"></a>Veri hazırlama
### <a name="data-sources"></a>Veri kaynakları
Tahmine dayalı bakım sorunları için ortak veri öğeleri Hello şu şekilde özetlenebilir:

* Hata geçmiş: Merhaba makine ya da hello makine içinde bileşen hatası geçmişi.
* Bakım geçmişi: Merhaba örneğin hata kodları, önceki bakım etkinlikleri veya bileşen değişikliklerini makinenin onarım geçmişi.
* Makine koşullar ve Kullanım: Makine Örneğin veri koşullarını işletim hello toplanan algılayıcı.
* Makine özellikler: hello özellikleri makinenin, örneğin altyapısı boyutu, marka ve model, konumu.
* İşleç özellikleri: Merhaba özelliklerini hello işleci, örneğin, cinsiyetiniz, geçmiş deneyimi.

Bu olası ve genellikle özel hata kodları veya yedek parça sipariş tarihleri hello biçiminde bakım geçmişi gibi hata geçmişi bulunan hello durumda olur. Bu gibi durumlarda hataları hello bakım verilerden ayıklanabilir. Ayrıca, farklı iş etki alanı burada ayrıntısına listelenmeyen hatası desenleri etkileyen diğer veri kaynaklarının çeşitli olabilir. Bunlar, Tahmine dayalı modeller oluştururken hello etki alanı uzmanlar danışmanlık tanımlanmalıdır.

Bazı veri öğeleri yukarıda kullanım örneklerinden örnekler:

Hata geçmiş: gecikme tarihleri, uçak bileşen hatası tarihleri ve türleri, ATM nakit mevzuatı işlem hataları, tren/fırsatınızdır kapı hataları, Fren disk değiştirme sipariş tarihleri, Rüzgar Türbin hatası tarihleri ve devre kesici komutu hataları mücadele.

Bakım geçmişi: uçuş hata günlükleri, ATM işlem hata günlüklerini, eğitmek bakım türü, kısa bir açıklama vb. ve devre kesici bakım kayıtları dahil olmak üzere bakım kaydeder.

Makine koşullar ve Kullanım: uçuş yönlendirir ve uçak motorları, ATM işlemleri ait sensör okumaları toplanan algılayıcı verilerini kez, olaylar verilerini, Rüzgar turbines, asansörler ve bağlı araba ait sensör okumaları eğitmek.

Makine özellikler: Voltaj düzeyleri gibi devre kesici teknik özellikler, marka, model, altyapı gibi coğrafi konuma veya araba özellikleri boyut, lastiği türleri, üretim tesis vb..

Merhaba veri kaynakları verilen, biz Tahmine dayalı bakım etki alanında gözlemlemek hello iki ana veri zamana bağlı veri ve statik veri türleridir.
Onarım geçmişi, kullanım geçmişini neredeyse her zaman zaman damgalarını ile gelen hata geçmişi, makine koşullar, her veri parçası için koleksiyon hello saati gösteren. Bunlar genellikle hello teknik özellikleri makineler veya işlecin özelliklerini açıklayan bu yana makine özellikler ve işleci özellikler genel statik. Saat ve bu nedenle bunlar zaman damgalı veri kaynakları olarak değerlendirilip değerlendirilmeyeceğini üzerinden bu özellikleri toochange için mümkündür.

### <a name="merging-data-sources"></a>Veri Kaynakları birleştirme
Herhangi bir türde özellik Mühendisliği veya etiketleme işlem almadan önce toofirst ihtiyacımız hello gerekli form toocreate özelliklerinden bizim verilerde hazırlayın. Merhaba ultimate özellikleri ve etiketleri toobe ile her varlık için her zaman birimi için bir kayıt hello makine öğrenme algoritmasını sat toogenerate hedefidir. Son veri kümesi temiz sipariş tooprepare içinde önceden işlem bazı adımlar gerçekleştirilmelidir. Veri toplama her kayıt tooa zaman birimi bir varlık için ait olduğu zaman birimlerine toodivide hello süresi ilk adımdır. Kolaylık sağlamak için zaman birimlerini hello açıklamaları hello kalanı için kullandığımız ancak veri toplama aynı zamanda diğer birimler gibi eylemler, bölünebilir.

Merhaba ölçü birimi kez saniye, dakika, saat, gün, ay, döngüler, mil veya veri hazırlığı ve diğer veya diğer, zaman birimi toohello hello varlığından hello koşulları gözlenen hello değişiklikleri hello verimliliği bağlı olarak hareket içinde olabilir Etkenler belirli toohello etki alanı. Diğer bir deyişle, hello zaman birimi birçok durumda veri olduğu gibi veri toplama hello sıklığını herhangi bir birimi toohello farkı diğer gösterilmeyebilir gibi aynı hello toobe yok. Sıcaklık değerleri 10 saniyede toplanmakta, örneğin, bir zaman birimi hello tüm çözümleme için 10 saniye çekme örnekler hello sayısı ek bilgileri sağlamadan Şişir. Daha iyi stratejisi toouse ortalama bir örnek olarak bir saat içinde olacaktır.

Örnek genel veri şemaları hello olası veri kaynakları için hello açıklandığı önceki bölümde şunlardır:

Bakım kayıtları: hello kayıtları gerçekleştirilen bakım işlemleri, bunlar. Merhaba bakım veriler genellikle bir varlık kimliği ile gelir ve o anda bakım etkinlikleri hakkında bilgi içeren zaman damgası gerçekleştirilmiş ham. Bu tür ham veriler durumunda bakım etkinlikleri kategorik sütunlara her kategori karşılık gelen tooa bakım eylemi türü ile çevrilmiş toobe gerekir. Merhaba temel veri şeması bakım kayıtları için varlık kimliği, saati ve Bakım eylemi sütunları içerir.

Hata kaydeder: Bu hataları veya hata nedeni dediğimiz tahmin toohello hedefinin ait hello kayıtlardır. Bu, belirli hata kodları veya hatalar belirli iş koşul tarafından tanımlanan olayları olabilir. Bazı durumlarda, verileri bazıları ilgi toofailures karşılık gelen birden çok hata kodları içerir. Diğer hatalar genellikle; bu nedenle tahmin hedefinin ilişkilendirilebilir tooconstruct özellikleri hatalarıyla kullanılan tüm hatalardır. neden olup olmadığını hello temel veri Şeması hatası kayıtlar için varlık kimliği, zaman ve hata veya başarısızlık nedeni sütunları içerir.

Makine koşullar: hello veri koşullarını işletim hello ilgili verilerin izlenmesi tercihen gerçek zamanlı bunlar. Örneğin, kapı hataları için Kapak açma ve kapatma süreleri iyi kapıları hello geçerli durumu hakkında göstergesidir. Merhaba temel veri şeması makine koşulları için varlık kimliği, saati ve durum değeri sütunları içerir.

Makine and işleci veri: Makine and işleci veri birleştirilmiş bir şema tooidentify hangi varlık varlık ve işleci özelliklerinin yanı sıra hangi işleci tarafından işletilen içine. Örneğin, bir araba genellikle yaşı gibi deneyimi vb. yürüten özniteliklere sahip bir sürücü aittir. Bu veriler zamanla değişirse, bu veriler ayrıca bir saat sütunu içermelidir ve özellik oluşturma için veri değişen zaman olarak değerlendirilmelidir. Merhaba temel veri şeması makine koşulları için varlık kimliği, varlık özellikleri, operatör kodu ve işleci özellikler içerir.

etiketleme ve özellik oluşturma hatası kayıtlarda varlık kimliği ve zaman alanları makine koşullar tabloyla birleştirme sol tarafından oluşturulmadan önce hello son tablo. Bu tabloda ardından varlık kimliği üzerinde bakım kayıtlarla katılabilir ve zaman alanları ve son olarak makine ve işleçle birlikte varlık kimliği temel özellikleri Makine normal işlemde olduğunda hello ilk sol birleştirme hatası sütunu için null değerler bırakır, bunlar normal işlem için bir gösterge değeri tarafından imputed. Bu hata hello Tahmine dayalı bir model için kullanılan toocreate etiketleri bir sütundur.

### <a name="feature-engineering"></a>Özellik mühendisliği
Merhaba ilk modelleme özellik Mühendisliği adımdır. Merhaba özelliği nesil fikirdir tooconceptually toothat noktası zamanında toplanan geçmiş verileri kullanarak belirli bir zamanda bir makinenin sistem durumu koşulu soyut ve açıklanmıştır. Merhaba sonraki bölümde, Tahmine dayalı Bakım ve hello etiketleme için her tekniği nasıl yapıldığını için kullanılan teknikleri hello tür genel bir bakış sağlar. kullanılması gereken tam bir teknik hello hello verileri ve iş soruna bağlıdır. Ancak, hello özelliği mühendislik yöntemleri aşağıda açıklanan taban çizgisi olarak özellikleri oluşturmak için kullanılır. Aşağıda, biz, zaman damgaları ve ayrıca statik veri kaynaklarından oluşturulan statik özellikler gelir ve hello örneklerinden kullanım sağlayan veri kaynaklarından oluşturulan öteleme ele alınmaktadır.

#### <a name="lag-features"></a>Gecikme özellikleri
Tahmine dayalı Bakım'ın daha önce belirtildiği gibi geçmiş verileri genellikle her veri parçası için koleksiyon hello saati gösteren tarih damgası ile birlikte gelir. Zaman damgalı veriyle gelir hello verilerden özellikleri oluşturma, birçok yolu vardır. Bu bölümde, Tahmine dayalı bakım için kullanılan bu yöntemlerden bazıları aşağıdakiler ele. Ancak, biz bu yöntemleri sınırlı değildir. Özellik Mühendisliği toobe hello en yaratıcı alanları birini Tahmine dayalı modelleme olarak kabul edilir bu yana birçok yolu toocreate özelliği olabilir. Burada, bazı genel teknikleri sunuyoruz.

##### <a name="rolling-aggregates"></a>*Toplamalar alınıyor*
Her bir varlık kayıt için çalışırken penceresinde hello toocompute geçmiş Toplamalar için isteriz zaman birimlerinin sayısı olan "w" harfinin boyutunu seçin. Merhaba W dönemlerini başlangıç tarihinden önce bu kayıt kullanarak toplama özellik çalışırken sonra işlem. Toplamalar çalışırken bazı örnek çalışırken sayıları, anlamına gelir, Standart sapmanın, Standart sapmanın dayalı aykırı değerlerini, CUSUM ölçer, pencere için minimum ve maksimum değerleri. Başka bir ilginç toocapture eğilim değişiklikler, ani ve anomali algılama algoritmalarını kullanarak verileri anormallikleri algılama algoritmalarını kullanarak düzeyi değişikliklerini tekniğidir.

Tanıtımı için bkz: Şekil süre ile her birim için bir varlık için kaydedilen algılayıcı değerlerini temsil eden burada biz hello mavi çizgiler ve işaretlemek hello kayıtlar için ortalama özellik hesaplama W = 3 t çalışırken hello 1<sub>1</sub> ve t<sub>2 </sub> turuncu tarafından belirtilir ve gruplandırmaları sırasıyla yeşil.

![Şekil 1 '. Toplama özellikleri alınıyor](media/cortana-analytics-playbook-predictive-maintenance/rolling-aggregate-features.png)

Şekil 1 '. Toplama özellikleri alınıyor

Uçak bileşeni hatası için örnek olarak kullanılan toocreate anlamına gelir, standart sapma ve toplam özellikler çalışırken geçen hafta, son üç günde ve son günü algılayıcı değerlerini yoktu. Benzer şekilde, üç Standart sapmanın, üst ve alt CUMSUM özellikleri ötesinde aykırı değerlerini sayısı için ATM hataları, ham algılayıcı değerlerini ve çalışırken anlamına gelir, Orta, aralığı, Standart sapmanın kullanılmıştır.

Uçuş gecikme tahmin için kullanılan toocreate özellikleri hata kodlarından geçen hafta sayısı yoktu. Tren kapı hataları için hello hello olaylarına sayısı son günü önceki 2 hafta hello olayları sayar ve hello olayların sayısını önceki 15 gün varyansını olan kullanılan toocreate öteleme özellikleri. Aynı sayım bakım ilgili olayları için kullanıldı.

Ayrıca, bir W çekme tarafından çok büyük (örn. Yıl), olası tüm bakım sayım gibi bir varlık tam geçmişini hello adresindeki toolook kaydeder, hataları vs. Merhaba kayıt Hello zamanı kadar. Bu yöntem devre kesici hataları hello için son üç yıl sayım için kullanıldı. Tren hataları için toocreate tüm bakım olaylar ayrıca sayılan özelliği toocapture hello uzun süreli bakım etkiler.

##### <a name="tumbling-aggregates"></a>*Dönen toplar*
Bir varlık etiketli her kayıt için kimliğinizi bir pencere boyutunu çekme "W -<sub>k</sub>" k hello numarası veya toocreate istiyoruz boyutu "W" windows olduğu öteleme özellikleri. "k" bir büyük sayı toocapture uzun vadeli düşüşü desenleri veya küçük bir sayı toocapture kısa vadeli etkileri çekilebilir. Ardından k dönen windows W - kullanırız<sub>k</sub> , W -<sub>(k-1)</sub>,..., W -<sub>2</sub> , W -<sub>1</sub> hello kaydından önce hello süreyle toocreate toplama özellikleri (bkz: Şekil 2) tarih ve saat. Bunlar ayrıca windows hello kayıt düzeyinde yakalanmaz için bir zaman birimi Şekil 2'de geri ancak hello fikirdir aynı Şekil 1 olduğu gibi hello burada t<sub>2</sub> da kullanılan toodemonstrate hello alınıyor etkisi.

![Şekil 2. Toplama özellikleri dönen](media/cortana-analytics-playbook-predictive-maintenance/tumbling-aggregate-features.png)

Şekil 2. Toplama özellikleri dönen

Örnek olarak, Rüzgar turbines, W = 1 k = ve için 3 ay kullanılan toocreate öteleme özellikleri her hello için üst ve alt aykırı değerlerini kullanarak son 3 ay yoktu.

#### <a name="static-features"></a>Statik özellikler
Üretim tarihi, model numarası, konum vb. gibi hello ekipmanının teknik özellikleri şunlardır. Öteleme özellikleri genellikle doğası gereği sayısal olsa da, statik özellikleri genellikle hello modellerde kategorik değişkenleri duruma gelir. Bir örnek, voltaj, geçerli gibi devre kesici özellikleri ve güç belirtimleri transformer türleri ile birlikte, güç kaynakları vb. kullanılmıştır. Fren disk hataları için karışımı oldukları veya çelik hello statik özelliklerden bazıları kullanılmış gibi böyle lastiği Tekerlek türünü hello.

Özellik oluşturma sırasında eksik değerleri ve normalleştirme işleme gibi bazı diğer önemli adımlar gerçekleştirilmelidir. Eksik değeri imputation ve ayrıca burada ele alınmamıştır veri normalleştirme çeşitli yöntemler vardır. Ancak, tahmini performans artışı mümkün ise faydalı tootry farklı yöntemler toosee olur.

Merhaba son özellik tablosu hello açıklanan adımları mühendislik özelliği sonra önceki bölümde örnek veri şeması zaman birimi bir gün olduğunda aşağıdaki hello benzemelidir:

| Varlık Kimliği | Zaman | Özellik sütunları | Etiket |
| --- | --- | --- | --- |
| 1 |Günde 1 | | |
| 1 |Gün 2 | | |
| ... |... | | |
| 2 |Günde 1 | | |
| 2 |Gün 2 | | |
| ... |... | | |

## <a name="modeling-techniques"></a>Modelleme teknikleri
Tahmine dayalı bakım genellikle birçok farklı açılarını hello perspektif modelleme Tahmine dayalı yaklaşıldığında iş sorularını kullanan çok zengin bir etki alanıdır. Merhaba sonraki bölümlerde, Tahmine dayalı bakım çözümleriyle yanıtlanması kullanılan toomodel farklı iş sorularını olan ana teknikleri sunuyoruz. Benzerlikler olsa da, her modeli kendi yolunu ayrıntılı olarak açıklanan oluşturma etiket vardır. Eşlik eden bir kaynak olarak Azure Machine Learning içinde sağlanan hello örnek denemeleri dahil toohello Tahmine dayalı bakım şablonu başvurabilir. Bu şablon için Hello bağlantılar toohello çevrimiçi malzemesi hello kaynaklar bölümünde sağlanır. Yukarıda açıklanan teknikleri mühendislik hello özellik ve hello sonraki bölümlerde açıklanan teknikleri modelleme hello bazıları nasıl uygulandığını görebilirsiniz toopredict uçak motoru Azure Machine Learning kullanarak hataları.

### <a name="binary-classification-for-predictive-maintenance"></a>Tahmine dayalı bakım için ikili sınıflandırma
Tahmine dayalı bakım için ikili sınıflandırma ekipman gelecekteki bir süre içinde başarısız olan kullanılan toopredict hello olasılıktır. Merhaba süre tarafından belirlenir ve iş kurallarını ve elinizdeki hello veriler temel alınarak. Bazı ortak dönemleri minimum sağlama gereken süre toopurchase yedek parçaların tooreplace büyük olasılıkla toodamage bileşenleri veya içindeki büyük olasılıkla toooccur zaman gerekli toodeploy bakım kaynakları tooperform bakım yordamları toofix hello sorunu olan süre. Bu gelecekteki yatay süresi "X" diyoruz.

İçinde sipariş toouse ikili Sınıflandırma, pozitif ve negatif dediğimiz örnekler iki tür tooidentify gerekir. Her örneğin tooa zaman birimi kavramsal olarak açıklayan ve toothat zaman birimi daha önce açıklanan geçmiş ve diğer veri kaynakları kullanarak özellik Mühendisliği aracılığıyla kendi işletim durumları özetleyen bir varlık için ait olduğu bir kayıttır. Tahmine dayalı bakım için ikili sınıflandırma Hello bağlamda hataları (etiketi 1) pozitif türde gösterir ve negatif tür normal işlemleri gösterir (etiket = 0) etiketleri türü kategorik olduğu. Merhaba, toofind her yeni örnek büyük olasılıkla toofail olarak tanımlayan veya sonraki zaman birimleri X hello içinde normal şekilde işlem modeli hedeftir.

#### <a name="label-construction"></a>Etiket oluşturma
Sipariş toocreate Tahmine dayalı bir model tooanswer hello "Merhaba zaman birimlerinin yanındaki X varlık başarısız hello hello olasılık nedir?" sorusu, etiketleme alma X kayıtları önceki toohello başarısızlığını bir varlık ve bunları "ilgili olarak toofail" etiketleme tarafından yapılır (Etiket = 1) diğer tüm kayıtları "normal" olarak etiketleme sırasında (etiket = 0). Bu yöntemde, etiketleri (bkz: Şekil 3) kategorik değişkenlerdir.

![Şekil 3 '. İkili sınıflandırma etiketleme](media/cortana-analytics-playbook-predictive-maintenance/labelling-for-binary-classification.png)

Şekil 3 '. İkili sınıflandırma etiketleme

Uçuş gecikmeleri ve iptalleri için X hello toopredict gecikme bir gün olarak sonraki 24 saat çekilir. Hataları önce 24 saat içinde olan tüm uçuşları 1'ler etiketlenmiş. ATM nakit hataları etiket için iki ikili sınıflandırma modelleri hello işlemde toopredict hello hatası olasılığını sonraki 10 dakika oluşturulan ve ayrıca toopredict hello hatası olasılığını hello dispensed sonraki 100 notları. Son 10 dakika hello hatanın hello içinde gerçekleşen tüm işlemleri hello ilk modeli için 1 olarak etiketlenir. Ve bir hatanın 100 notları hello içinde dispensed tüm notları son hello ikinci modeli için 1 olarak etiketlenmiş. Devre kesici hataları için hello görev X toobe bir sonraki komut; bu durumda seçilen sonraki devre kesici komutu hello toopredict hello olasılık başarısız olur. Tren kapı hataları için hello ikili sınıflandırma modeli sonraki 7 gün toopredict hataları hello içinde oluşturuldu. Rüzgar Türbin hataları için X 3 ay seçildi.

Rüzgar Türbin ve tren kapı çalışmaları regresyon analizi toopredict kalan kullanım ömrü kullanan hello için aynı veri ancak hangi hello sonraki bölümde anlatılmıştır farklı bir etiketleme stratejisi aynı kullanarak de kullanılır.

### <a name="regression-for-predictive-maintenance"></a>Tahmine dayalı bakım regresyon
Tahmine dayalı bakım regresyon modeller kullanılan toocompute kalan kullanım ömrü (RUL) hello sonraki hata gerçekleşmeden önce hello süreyi varlık hello işletimsel olduğu gibi tanımlı bir varlık içindedir. İkili sınıflandırma aynı, her bir varlık için tooa zaman birimi "Y" ait bir kayıt örnektir. Ancak, regresyon hello bağlamda hello toofind her yeni örnek kullanım ömrü hello hatasından önce kalan hello süre olan sürekli bir sayı olarak kalan hello hesaplar bir model hedeftir. Bu süre içinde bazı birden çok y diyoruz. Her örneğin de hello süreyi kalan hello sonraki hata vermeden önce bu örneğin ölçerek hesaplanan bir kalan kullanım ömrü vardır.

#### <a name="label-construction"></a>Etiket oluşturma
Verilen hello Soru "Merhaba kalan kullanım ömrü hello donanımların nedir?
", hello regresyon modeli her kayıt önceki toohello hatası alma ve hello sonraki hatasından önce kaç saat biriminin kalır hesaplayarak etiketleme tarafından oluşturulan için etiketler. Bu yöntemde, etiketleri sürekli (bkz: Şekil 4) değişkenlerdir.

![Şekil 4 '. Regresyon için etiketleme](media/cortana-analytics-playbook-predictive-maintenance/labelling-for-regression.png)

Şekil 4 '. Regresyon için etiketleme

İkili Sınıflandırma, regresyon, farklı varlıklar hello verilerdeki herhangi bir hata olmadan etiketleme referans tooa hata noktası yapılır ve kendi hesaplama önce derdi bitti ne kadar süreyle hello varlık bilmeden olası değil olarak modelleme için kullanılamaz hata oluştu. Bu sorunu en iyi hayatta analiz adında başka bir istatistik teknik tarafından ele.
Toodiscuss hayatta analiz hello teknik toopredictive bakım uygularken kaynaklanabilecek hello olası karışıklıklardan dolayı bu playbook içinde sık aralıklarla zaman değişen verilerle ilgili kullanım yapmayacağınız.

### <a name="multi-class-classification-for-predictive-maintenance"></a>Tahmine dayalı bakım için birden çok sınıf sınıflandırma
Tahmine dayalı bakım için birden çok sınıf sınıflandırma iki gelecekteki sonuçları öngörmek için kullanılabilir. Merhaba ilk tooassign Merhaba, bir varlık tooone zaman toogive zaman toofailure her varlık için bir aralığı birden fazla olası dönemlerini biridir. Merhaba ikincisi olan tooidentify hello gelecekteki bir dönem son hata olasılığını hello tooone birden çok kök neden olur. Bu bilgiyle hello sorunları önceden işlemek için donatılmıştır bakım personeli sağlayan. Başka bir çok sınıfı modelleme teknikleri hello olasılıkla kök nedenini belirlemeye odaklanır bir hata verilir. Bu öneriler toobe hello üst bakım eylemleri toobe sipariş toofix hata gerçekleştirilecek için verilen sağlar.
Sahip tarafından kök sıralı bir listesini neden olur ve ilişkili onarım Eylemler,  
teknisyenler arızalarının ardından ilk onarım eylemlerini alırken daha etkili olabilir.

#### <a name="label-construction"></a>Etiket oluşturma
Olan hello iki soruları verilen "Merhaba sonraki"aZ"zaman birimi olarak bir varlık başarısız hello olasılık nedir"a"Merhaba dönem sayısı burada" ve "hello zaman birimlerinin yanındaki X varlık hello hello olasılık nedir başarısız son tooproblem" P<sub>t </sub>"burada"i"Merhaba etiketleme, olası nedenlerini sayısıdır bu tootechniques yol aşağıdaki hello yapılır.

Merhaba ilk soru etiketleme bir malın hello arıza öncesinde aZ kayıtları almak ve bunları etiketleme yapılır "normal" olarak diğer tüm kayıtları etiketleme sırasında etiketlerine süre (3Z, 2Z, Z) demet kullanarak (etiket = 0). Bu yöntemde, etiket kategorik (bkz: Şekil 5) değişkendir.

![Şekil 5. İçin hata zaman tahmini çok sınıflı sınıflandırma etiketleme](media/cortana-analytics-playbook-predictive-maintenance/labelling-for-multiclass-classification-for-failure-time-prediction.png)

Şekil 5. İçin hata zaman tahmini çok sınıflı sınıflandırma etiketleme

Hello ikinci soruyu etiketleme alma X kayıtları bir varlık ve bunları olarak etiketleme hello arıza öncesinde gerçekleştirilir "P sorunu nedeniyle toofail hakkında<sub>ı</sub>" (etiket = P<sub>ı</sub>) diğer tüm kayıtları olarak etiketleme sırasında " Normal"(etiket = 0). Bu yöntemde, etiketleri kategorik (bkz: Şekil 6) değişkenlerdir.

![Şekil 6. İçin kök nedeni tahmin çok sınıflı sınıflandırma etiketleme](media/cortana-analytics-playbook-predictive-maintenance/labelling-for-multiclass-classification-for-root-cause-prediction.png)

Şekil 6. İçin kök nedeni tahmin çok sınıflı sınıflandırma etiketleme

Merhaba modeli atar hata olasılığını son tooeach P<sub>ı</sub> hello hiçbir hata olasılığını yanı sıra. Bu olasılıklar büyüklük tooallow tahmin hello gelecekteki, büyük olasılıkla toooccur olan hello sorunları göre sıralanabilir. Uçak bileşen hatası kullanım örneği çok sınıflı sınıflandırma sorunu yapılandırılmış. Bu, bir sonraki ay içinde hello gerçekleşen tootwo farklı baskısı vana bileşenleri son hatanın hello olasılıklar hello tahminini sağlar.

Bakım işlemleri arızalarının ardından önermek için etiketleme çekilen gelecekteki yatay toobe gerektirmez. Merhaba modeli hello gelecekteki hatası tahmin etmeye değil ancak hello hatası zaten gerçekleştirilmedi sonra hello en olası kök nedeni yalnızca tahmin etmeye budur. Fırsatınızdır kapı hataları hello hedef toopredict olduğu hello üçüncü durumuna çalışma koşulları hakkında geçmiş verileri verilen hello hatanın nedenini ayrılır. Bu model sonra kullanılan bir hata gerçekleştikten sonra toopredict hello olasılıkla kök neden olur. Bu model önemli yararlarından biri, aksi takdirde yıllık deneyimi gerekir sorunları tanılayıp deneyimsiz teknisyenleri tooeasily yardımcı olur.

## <a name="training-validation-and-testing-methods-in-predictive-maintenance"></a>Eğitim, doğrulama ve Tahmine dayalı bakım test yöntemleri
Tahmine dayalı bakımda benzer tooany zaman damgalı verilerini içeren, başka bir çözüm alanın hello tipik eğitim ve rutin gereksinimlerini tootake hesap hello süresi yönlerini toobetter değişen test üzerinde görünmeyen gelecekteki veri generalize.

### <a name="cross-validation"></a>Çapraz doğrulama
Çok sayıda makine öğrenimi algoritmalarını modeli performansını önemli ölçüde değiştirebilirsiniz hyperparameters sayısına bağlıdır. Merhaba bu hyperparameters en iyi değerlerini otomatik olarak hello modeli eğitimindeki hesaplanır değil veri Bilimcisi tarafından belirtilmesi gerekir, ancak. Hyperparameters iyi değerlerini bulma birkaç yolu vardır. Merhaba en yaygın bir "k-Katlama çapraz hangi hello örnekler rastgele"k"Katlama böler doğrulama" dir. Her hyperparameters değer kümesi öğrenme algoritmasını çalışma k katıdır. Her yinelemesinde hello geçerli Katlama hello örneklerde doğrulama kümesi olarak kullanılan, hello rest hello örneklerin Eğitim kümesi olarak kullanılır. Eğitim örnekler Hello algoritması eğitir ve hello performans ölçümleri doğrulama örnekler hesaplanır. Sonunda hello her hyperparameter değer kümesi için bu döngü, hello k performans ölçümü değerlerinin ortalamasını işlem ve hello en iyi ortalama performans sahip hyperparameter değerleri seçin.

Tahmine dayalı bakım sorunları, daha önce belirtildiği gibi verileri çeşitli veri kaynaklarından gelen olayların zaman serisi olarak kaydedilir. Bu kayıtlar, kayıt veya bir örnek etiketleme toohello zaman göre sıralanabilir. Hangi hello dataset rasgele olarak eğitim ve doğrulama kümesi olarak bölme biz, bu nedenle, bazı hello eğitim örnekleri zamanında doğrulama örnekler bazıları sonraki demektir. Bu model eğitilmiş önce gelen hello verilerine dayalı hyperparameter değerlerin gelecekte performans tahmininde sonuçlanır. Bu tahminler özellikle zaman serisi sabit değildir ve zaman içinde davranışlarını değiştirme aşırı iyimser olabilir. Sonuç olarak, seçilen hyperparameter değerleri iyinin olabilir.

Tüm doğrulama örnekler tüm eğitim örnekleri zamanında sonraki şekilde hyperparameters iyi değerlerini bulma bir daha iyi toosplit hello örnekler eğitim ve bir zamana bağımlı şekilde ayarlanması doğrulama yoludur. Ardından, her hyperparameters değer kümesi biz Eğitim kümesi üzerinden hello algoritması eğitmek, aynı doğrulama ayarlamak ve hello en iyi performansı göstermek hyperparameter değerleri seçin hello modelinin performansını ölçmek. Zaman serisi veri sabit değildir ve zaman içinde dönüşmesi tren/doğrulama sağlama tooa daha iyi gelecekteki "modelinin daha performans rastgele çapraz doğrulama tarafından seçilen hello değerlerle. bölme tarafından seçilen hyperparameter değerleri hello

Merhaba son model, eğitim/doğrulama Böl veya çapraz doğrulama kullanarak bulunan hello en iyi hyperparameter değerleri kullanarak tüm veriler üzerinde bir öğrenme algoritması eğitim tarafından oluşturulur.

### <a name="testing-for-model-performance"></a>Model performansını test etme
Bir model oluşturduktan sonra tooestimate gelecekteki performansını yeni verilerin ihtiyacımız var. Merhaba basit tahmin hello modeli hello performansını hello eğitim verileri üzerinde olabilir. Ancak kullanılan tooestimate performansı uyarlanmış toohello veri modeli olduğu için bu tahmin aşırı iyimser. Daha iyi tahmini performans ölçüm hyperparameter değerlerin hello doğrulama küme üzerinde hesaplanan veya bir ortalama performans ölçümü çapraz doğrulama hesaplanan olabilir. Ancak bu tahminler aynı daha önce belirtildiği nedenleri hello için hala aşırı iyimser. Model performansını ölçmek için daha gerçekçi yaklaşımlar ihtiyacımız var.

Eğitim, doğrulama ve test kümeleri toosplit hello verilerini rasgele bir yoludur. Merhaba eğitim ve doğrulama kümeleri, bunlarla hyperparameters ve tren hello modelinin kullanılan tooselect değerlerdir. modelin Hello performansı hello test küme üzerinde ölçülür.

Toosplit ilgili toopredictive bakım, başka bir yolu sağlayacak şekilde tüm örnekleri test eğitim, zamana bağlı şekilde, doğrulama ve test kümeleri içine tüm eğitim ve doğrulama örnekler zamanında sonraki örnektir. Merhaba bölme sonra model oluşturma ve performans ölçüm yapılır aynı daha önce açıklandığı gibi hello.

Zaman serisi sabit ve kolay toopredict olduğunda her iki yaklaşımın gelecekteki performansını benzer tahminler oluşturur. Ancak zaman serisi ileti örneği olmayan ve/veya sabit toopredict olduğunda hello İkinci yaklaşımı gelecekteki performansı birinci hello daha fazla gerçekçi tahminlerini oluşturur.

### <a name="time-dependent-split"></a>Zamana bağlı Böl
En iyi uygulama, bu bölümde biz yakın nasıl zamana bağımlı bölünmüş uygulanacağını göz atın. Biz, ancak tam olarak hello aynı mantığı zamana bağımlı için eğitim ve doğrulama kümesi bölmek için uygulanması gereken, eğitim ve test kümeleri arasındaki zamana bağımlı iki yönlü bölme açıklanmaktadır.

Bir akış gibi çeşitli algılayıcılar ölçümler zaman damgalı olayların sahibiz varsayalım. Eğitim ve test örnekleri yanı sıra, bunların etiketlerini özelliklerini birden çok olay içeren üretildikten tanımlanır.
Örneğin, ikili sınıflandırma için özellik Mühendisliği ve modelleme teknikleri bölümlerinde açıklandığı gibi özellikleri hello son temel alınarak oluşturulur olayları ve etiketler oluşturulur "X" Merhaba zaman birimleri içinde gelecekteki olayları göre gelecekte. Bu nedenle, bir örneğin bir zaman çerçevesi etiketleme hello daha sonra gelen ardından zaman çerçevesi özelliklerinin hello. Zamana bağlı bölme için hangi biz bizi hyperparameters ile bir model toothat noktası geçmiş verileri kullanarak eğitmek zaman içinde bir nokta seçin. Eğitim verileri içinde hello eğitim sonlandırma ötesinde gelecekteki etiketler tooprevent sızıntısını, biz hello son zaman çerçevesi toolabel eğitim örnekler toobe X birimleri hello eğitim sonlandırma tarihinden önce seçin. Şekil 7'de bir satır için hangi hello özellikleri ve etiketleri yukarıda açıklanan toothe yöntemi göre hesaplanır hello son özellik veri kümesindeki her dolu daire temsil eder. Verilen, eğitim ve ayarlar zamana bağımlı bölünmüş X = 2 ve W = 3 için uygularken test gitmesi hello kayıtları hello şekilde gösterilmektedir:

![Şekil 7. Zamana bağlı için ikili sınıflandırma bölme](media/cortana-analytics-playbook-predictive-maintenance/time-dependent-split-for-binary-classification.png)

Şekil 7. Zamana bağlı için ikili sınıflandırma bölme

Merhaba yeşil kareler için eğitim kullanılabilir toohello zaman birimleri ait hello kayıtları temsil eder. Daha önce her son hello eğitim örnekte açıklandığı gibi özellik tablosu bakarak oluşturulur özellik oluşturma ve eğitim gün sonlandırma önce etiketleme 2 gelecekteki dönem için 3 nokta geçti. Biz örnekler kümesini biz eğitim sonlandırma ötesinde görünürlük olmayan varsayıyoruz hello herhangi bir kısmını o örneğin 2 gelecekteki dönem hello eğitim sonlandırma dışında olduğu zaman hello eğitim kullanmayın. Toothat kısıtlama siyah örnekleri hello son hello eğitim veri kümesinde kullanılmamalıdır dataset etiketli hello kayıtları temsil eder. Bu kayıtları için üretildikten etiketleme hello eğitim sonlandırma önce oldukları ve bunların etiketleme üretildikten kısmen toocompletely isteriz olarak hangi hello çalışması olmamalıdır hello eğitim dilimini üzerinde bağımlı olduğundan ya da ayrı veri testinde kullanılmayacak. Eğitim ve tooprevent etiket bilgi sızıntısı test etme.

Bu teknik eğitim ve test Kapat toothe eğitim sonlandırma olan örnekler arasında özellik oluşturma için kullanılan hello verileri örtüşme sağlar. Veri kullanılabilirliğine bağlı olarak daha ciddi bir ayırma herhangi birini hello W zaman hello eğitim sonlandırma içinde birimleridir sınama kümesi örneklerde kullanarak değildir gerçekleştirilebilir.

Bizim işten kalan kullanım ömrü etmede kullanılan regresyon modeli daha ciddi bir şekilde hello sızıntısını sorundan etkilenen ve rastgele bölme kullanarak tooextreme overfitting müşteri adayları bulduk. Benzer şekilde, varlıklar kesilmiş eğitim önce hatalarıyla ait kayıtları Eğitim kümesi ve hataları hello sonlandırma kümesi test etmek için kullanılması gereken sonra olan varlıklar için kullanılması gereken şekilde regresyon sorunlarını hello bölünmüş olmalıdır.

Genel bir yöntem olarak eğitim ve test için veri bölmek için başka bir önemli en iyi uygulamadır toouse varlık Kimliğine göre bölünmüş olarak, böylelikle eğitim kullanılan hello varlıklar hiçbiri sınama fikir toomake emin olduğundan test etmek için kullanılır, yeni bir varlık ne zaman kullanılır  toomake tahminleri üzerinde gerçekçi sonuçları hello modeli sağlar.

### <a name="handling-imbalanced-data"></a>İmbalanced verileri işleme
Sınıfının bir hello daha fazla örnek varsa sınıflandırma sorunlarını diğer veriler hello toobe imbalanced belirtti. İdeal olarak, toohave isteriz hello eğitim veri toobe mümkün toodifferentiate farklı sınıflar arasında her sınıfının yeterli temsilcileri. Bir sınıf hello verilerin % 10'dan az ise, biz hello verilerinin imbalanced ve underrepresented hello dataset azınlık sınıfı diyoruz söyleyebilirsiniz. Büyük ölçüde, çoğu durumda biz imbalanced veri kümeleri bir sınıf ciddi bir şekilde underrepresented karşılaştırılan tooothers örneğin yalnızca %0,001 hello veri noktalarının oluşturan tarafından olduğu bulun. Sınıf dengesizliği hataları genellikle nadir oluşum hello azınlık sınıfı örnekleri oluşturan hello varlıklar hello ömrü içinde nerede sahtekarlık algılama, ağ yetkisiz erişim ve Tahmine dayalı bakım gibi birden çok etki alanı içinde bir sorundur.

Toominimize hedeflenir gibi birçok standart learning algoritmaları performansını sınıfı dengesizliği durumunda tehlikeye hello genel hata oranı. Örneğin, % 99 negatif sınıfı örnekleri ve %1 pozitif sınıfı örnekleri ile bir veri kümesi için yalnızca negatif olarak tüm örneklerini etiketleme tarafından biz % 99 doğruluğu alabilirsiniz. Ancak, Hello doğruluğu ölçüm çok yüksek olmasına rağmen hello algoritması yararlı bir nedenle bunu tüm olumlu örnekler misclassifies. Sonuç olarak, hata oranı üzerinde genel doğruluğu gibi geleneksel değerlendirme ölçümleri olmayan durumunda imbalanced öğrenme yeterli. Duyarlık, geri çağırma, F1 puanlarını ve ayarlanmış ROC Eğriler hello değerlendirme ölçümleri bölümde tartışılan imbalanced veri kümeleri halinde değerlendirmeleri için kullanılan maliyet gibi diğer ölçümleri.

Ancak, sınıf düzeltmek Yardım bazı yöntemler vardır dengesizliği sorun. Merhaba iki önemli olanları teknikleri örnekleme ve hassas öğrenme maliyeti.

#### <a name="sampling-methods"></a>Örnekleme yöntemleri
Merhaba kullanımını imbalanced öğrenme yöntemlerinde örnekleme hello dataset değiştirilmesini dengeli bir veri kümesi bazı mekanizmaları emri tooprovide içinde tarafından oluşur. Çok sayıda farklı örnekleme teknikleri olsa da, çoğu düz iletme rastgele olanlardır oversampling ve altında örnekleme.

Yalnızca belirtilen, rastgele oversampling rasgele bir örnek bu örnekler çoğaltmak ve tootraining veri kümesi ekleme azınlık sınıfından seçmektir. Bu toplam örneklerde azınlık sınıfı hello sayısını artırır ve sonunda farklı sınıfların örnekleri hello sayısı dengeleyin. Bir tehlike oversampling, belirli örnekleri birden çok örneğini hello sınıflandırıcı toobecome çok belirli başında toooverfitting neden olabilir ' dir.
Bu yüksek eğitim doğruluk neden olur, ancak performans verileri test etme görünmeyen üzerinde çok düşük olabilir. Buna karşılık, rastgele örnekleme altında rasgele bir örnek çoğunluğu sınıfı ve bu örnekleri eğitim veri kümesinden kaldırma seçmektir. Ancak, çoğu sınıfından örnekler kaldırma hello sınıflandırıcı toomiss önemli kavramları toohello çoğunluğu sınıfı ilgili neden olabilir. Burada azınlık sınıfı fazla örneklenen ve çoğu sınıf altında örneklenen karma örnekleme Merhaba aynı zamanda başka bir uygun bir yaklaşımdır. Varsa diğer birçok daha karmaşık örnekleme teknikler kullanılabilir ve etkili örnekleme yöntemleri sınıfı dengesizliği için sabit dikkat ve katkı pek çok kanaldan alma bir popüler araştırma alanı. Genellikle sol toohello veri Bilimcisi tooresearch olanları ve denemeler ve hello veri özellikleri yüksek oranda bağımlı hello en etkili karar vermek için farklı tekniklerini kullanın. Ayrıca, toomake örnekleme yöntemleri uygulanan yalnızca toohello eğitim olmasını ayarlar, ancak sınama kümesi hello değil önemlidir.

#### <a name="cost-sensitive-learning"></a>Hassas öğrenme maliyet
Tahmine dayalı bakım hello azınlık sınıfı oluşturan hataları normal örnekler'den daha fazla ilgi ve böylece hello odak performansı üzerinde ise hello hatalarda genellikle hello odak algoritmasıdır. Bu genellikle eşit olmayan kaybı veya öğeleri; burada görüntülerle hatalı pozitif negatif olarak tahmin maliyet farklı sınıfların misclassifying asimetrik maliyetlerini denir birden fazla tersi. Merhaba sınıflandırıcı mümkün toogive yüksek tahmin doğruluğunu hello doğruluk hello çoğunluğu sınıfı için üzerinde ciddi bir şekilde tehlikeye olmadan hello azınlık sınıfı edilmelidir istenen.

Bu elde birkaç yolu vardır. Merhaba azınlık misclassification için yüksek maliyet atayarak sınıfı ve eşit olmayan hello sorununun masraflar kaybederse çalışırken toominimize etkili bir şekilde ile ele alınabilir. Pozitif ve negatif örnekler maliyetini eğitim süre boyunca burada birleştirilebilir bu fikir kendiliğinden SVMs (Destek vektör makineler) gibi bazı machine learning algoritmaları kullanın. Benzer şekilde, artırma yöntemleri kullanılır ve genellikle ağaç algoritmalar gibi boosted imbalanced veri karar durumunda iyi bir performans gösterir.

## <a name="evaluation-metrics"></a>Değerlendirme ölçümleri
Daha önce belirtildiği gibi sınıfı dengesizliği algoritmaları tooclassify çoğunluğu sınıfı örnekleri çoğu sınıf doğru etiketli hello toplam misclassification hata çok artırıldı gibi daha iyi azınlık sınıf örneklerinin gider içinde eğilimindedir gibi düşük performans neden olur. Bu, düşük geri çağırma oranları neden olur ve yanlış alarmlar toohello iş hello maliyeti oldukça yüksek olduğunda daha büyük bir sorun haline gelir. Doğruluk sınıflandırıcı 's performans tanımlamak için kullanılan hello en popüler ölçümüdür. Yukarıda açıklandığı şekilde doğruluğu etkisiz ancak ve çok önemli toodata dağıtımları olduğu gibi hello gerçek performans sınıflandırıcı 's işlevlerin yansıtmaz. Bunun yerine, diğer değerlendirme ölçümleri kullanılan tooassess imbalanced öğrenme sorunlardır. Bu gibi durumlarda, kesinlik, geri çağırma ve F1 puanları hello ilk ölçümleri toolook adresindeki Tahmine dayalı bakım modeli performansını değerlendirirken olmalıdır. Tahmine dayalı bakım geri çağırma oranları hello sınama kümesi hatalarına doğru hello modeli tarafından tanımlanan hello kaç gösterir. Yüksek geri çağırma hızları hello modeli hello true hatalarını yakalama başarılı olduğu anlamına gelir. Duyarlık ölçüm false nerede yüksek yanlış alarmlar düşük duyarlılık ücretlerin karşılık gelen uyarılar hello oranı ile ilgilidir. F1 puan hem duyarlık hem de geri çağırma oranları 1 olan ve en kötü 0 olan en iyi değerle göz önünde bulundurur.

Ayrıca, ikili Sınıflandırma, decile tabloları ve yükseltme grafikleri performansını değerlendirirken çok bilgilendirici içindir. Bunlar yalnızca pozitif sınıfında (hata) odaklanmanıza ve ne hello (alıcı işletim karakteristiğini) ROC eğrisi üzerinde yalnızca sabit işletim bir noktada bakarak görülür değerinden daha karmaşık bir resim algoritması performans sağlar.
Decile tabloları hello test örnekleri kendi tahmin edilen olasılıklar hello son etiketini eşik toodecide önce hello modeli tarafından hesaplanan hatalar göre sıralama tarafından elde edilir. Merhaba sipariş edilen örnekleri deciles (yani hello % 10 örnekleri ile büyük olasılık ve sonra % 20, % 30 vb.) içinde gruplandırılır. Merhaba oranı her decile true pozitif oranını ve rastgele taban (yani 0.1, 0.2..) arasında bilgi işlem tarafından bir hello algoritması performans her decile nasıl değiştiğini tahmin edebilirsiniz. Yükseltme grafikleri kullanılan tooplot decile decile true pozitif oranı tüm deciles için rastgele true pozitif oranı çiftleri karşı Çizdirmek tarafından değerlerdir. Genellikle, burada en büyük kazançlar gösteriliyor beri hello ilk deciles hello sonuçlarının hello odak ' dir. İlk deciles, Tahmine dayalı bakım için kullanıldığında temsili için "riskli" olarak da görülebilir.

## <a name="sample-solution-architecture"></a>Örnek çözüm mimarisi
Tahmine dayalı bakım çözümünü dağıtırken, biz veri alımı, veri depolama sürekli döngüsü model eğitim, özellik oluşturma, tahmin ve birlikte hello sonuçlarını görselleştirme sağlayan son tooend çözümünü ilgilendiğiniz bir uyarı mekanizması Pano izleme bir varlık gibi oluşturuluyor. Sürekli bir otomatik şekilde gelecekteki Öngörüler toohello kullanıcı sağlayan veri ardışık istiyoruz. Bu tür bir IOT veri ardışık düzeni için bir örnek Tahmine dayalı bakım mimari Şekil 8'de gösterilmiştir. Mimarisinde, gerçek zamanlı telemetri akış verilerini depolayan bir Event Hub toplanır. Bu veriler, gerçek zamanlı işleme özelliğini oluşturma gibi veri akış analizi tarafından alınan. Merhaba özellikleri sonra kullanılan toocall hello Tahmine dayalı bir model web hizmeti ve sonuçları hello panosunda görüntülenir. AT hello aynı zaman, alınan veri ayrıca geçmiş bir veritabanında depolanan ve şirket içi veri toocreate eğitim örnekleri modelleme için taban gibi dış veri kaynakları ile birleştirilir.
Aynı veri ambarlarında hello örnekleri Puanlama ve hello Pano Tahmine dayalı raporlarda kullanılan tooprovide yeniden olabilen hello sonuçlarının depolama toplu işlemi için kullanılabilir.

![Şekil 8'de. Tahmine dayalı bakım için örnek çözümü mimarisi](media/cortana-analytics-playbook-predictive-maintenance/example-solution-architecture-for-predictive-maintenance.png)

Şekil 8'de. Tahmine dayalı bakım için örnek çözümü mimarisi

Hakkında daha fazla bilgi hello mimarisi için hello bileşenlerinden her biri çok başvurun[Azure](https://azure.microsoft.com/) belgeleri.

