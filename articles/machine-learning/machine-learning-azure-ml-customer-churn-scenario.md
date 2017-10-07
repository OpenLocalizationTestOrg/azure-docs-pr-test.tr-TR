---
title: "aaaAnalyzing Machine Learning kullanarak müşteri karmaşıklığı | Microsoft Docs"
description: "Çözümleme ve müşteri karmaşası Puanlama için tümleşik bir model geliştirerek, örnek olay incelemesi"
services: machine-learning
documentationcenter: 
author: jeannt
manager: jhubbard
editor: cgronlun
ms.assetid: 1333ffe2-59b8-4f40-9be7-3bf1173fc38d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeannt
ms.openlocfilehash: 070e6a2ebe4f2fe439a42ffe1a3fa9d6d3788d62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyzing-customer-churn-by-using-azure-machine-learning"></a>Azure Machine Learning ile Müşteri Değişim Sıklığını Çözümleme
## <a name="overview"></a>Genel Bakış
Bu makalede, Azure Machine Learning kullanılarak oluşturulmuş bir müşteri karmaşası analiz proje başvurusu uyarlamasını gösterir. Bu makalede, bütünsel endüstriyel müşteri karmaşası hello sorununu çözmek için ilişkili genel modelleri tartışın. Biz de Machine Learning kullanılarak oluşturulan modelleri hello doğruluğunu ölçmek ve size daha fazla geliştirme için yol tarifi değerlendirin.  

### <a name="acknowledgements"></a>Katkıda Bulunanlar
Bu deneme geliştirilmiş ve Serge Berger, asıl veri Bilimcisi Microsoft'ta ve Roger Barga, önceden Microsoft Azure Machine Learning için ürün Yöneticisi test. Hello Azure belgelerine takım minnettar uzmanlara kabul ettikten ve bu teknik incelemede paylaşmak için teşekkürler.

> [!NOTE]
> Bu deneme için kullanılan hello verileri genel kullanıma açık değil. Nasıl toobuild machine learning modeli karmaşası çözümleme için bir örnek için bkz: [perakende karmaşıklığı model şablonunun](https://gallery.cortanaintelligence.com/Collection/Retail-Customer-Churn-Prediction-Template-1) içinde [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com/)
> 
> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-problem-of-customer-churn"></a>Müşteri karmaşası Hello sorunu
İşletmeler hello tüketici Pazar ve tüm kurumsal kesimler karmaşası ile toodeal sahip. Bazen karmaşası aşırı ve ilke kararlarını etkiler. Merhaba geleneksel çözüm yüksek propensity churners toopredict olduğu ve gereksinimlerine, pazarlama kampanyalarının bir danışman hizmeti aracılığıyla veya özel dispensations uygulayarak adres. Bu yaklaşım, endüstri tooindustry ve hatta belirli tüketici küme tooanother bir endüstri (örneğin, telekomünikasyon) içinde değişebilir.

Merhaba ortak işletmelerin bu özel müşteri bekletme çaba toominimize ihtiyacı faktördür. Bu nedenle, doğal yöntemi karmaşası hello olasılığını her müşteriyle tooscore olması ve bu hello ilk N olanları adresini. Merhaba üst müşteriler olması hello En Karlı olanları; Örneğin, daha karmaşık senaryolarda, kar işlevi özel dispensation için aday hello seçimi sırasında kullanılmaz. Ancak, bu noktalar hello bütünsel stratejisi karmaşası ilgilenmek için yalnızca bir parçası değildir. İşletmeler tootake hesabı risk (ve ilişkili risk toleransınıza) de hello düzeyi ve maliyetini hello müdahalesi ve yatkýn müşteri kesimleme.  

## <a name="industry-outlook-and-approaches"></a>Endüstri outlook ve yaklaşımlar
Karmaşası Gelişmiş şekilde işlenmesi, olgun sektör işaretidir. Merhaba Klasik örneği aboneleri bir sağlayıcı tooanother bilinen toofrequently anahtardan nerede hello telekomünikasyon endüstri standardıdır. Bu gönüllü karmaşası prime bir konudur. Ayrıca, sağlayıcıları önemli bilgi hakkında toplanan *sürücüleri karmaşıklığı*, hangi Bu sürücü müşteriler tooswitch hello faktörlerdir.

Örneğin, ahize veya aygıt karmaşası hello cep telefonu iş, iyi bilinen bir sürücü seçimdir. Sonuç olarak, bir popüler toosubsidize hello yeni aboneler ve müşteriler için bir yükseltme tam fiyat tooexisting şarj ahize bedelinin ilkesidir. Tarihsel olarak, bu ilke bir sağlayıcı tooanother tooget sağlayıcılar toorefine kendi stratejileri sırayla istenir yeni bir indirimi atlamalı toocustomers açmıştır.

Ahize teklifleri içinde yüksek volatilite karmaşası geçerli ahize modellerinde dayalı modelleri hızla geçersiz kılan bir faktördür. Ayrıca, cep telefonları yalnızca telekomünikasyon aygıtlar değildir; Bunlar ayrıca şekilde deyimleri (Merhaba iPhone göz önünde bulundurun), ve bu sosyal predictors normal telekomünikasyon veri kümeleri dışında hello kapsamı.

Merhaba net modelleme için bilinen nedenlerle karmaşıklığı ortadan kaldırarak bir ses İlkesi insanlara olamaz sonucudur. Aslında, (örneğin, karar ağaçları), kategorik değişkenleri ölçme Klasik modelleri de dahil olmak üzere bir sürekli modelleme, stratejidir **zorunlu**.

Büyük veri kümeleri müşterilerinin kullanarak, kuruluşlar büyük veri analytics'te (özellikle, büyük veri dayalı karmaşası algılama) etkin bir yaklaşım toohello sorunu yapıyorsunuz. Merhaba büyük veri yaklaşım toohello hello ETL bölümünde önerileri karmaşıklık sorununun hakkında daha fazla bilgi bulabilirsiniz.  

## <a name="methodology-toomodel-customer-churn"></a>Yöntemler toomodel müşteri karmaşası
Bir ortak sorun giderme işlemi toosolve müşteri karmaşası Şekil 1-3'te belirtilmiştir:  

1. Tooconsider sağlayan bir risk modeli Eylemler olasılık ve risk nasıl etkiler.
2. Bir araya model tooconsider sağlar araya hello düzeyini hello olasılık müşteri yaşam süresi değeri (CLV) karmaşası ve hello miktarının nasıl etkileyebilir.
3. Bu çözümleme kendisini Müşteri kesimleri toodeliver hello en iyi teklif hedefleyen ilerletilen tooa öngörülü pazarlama kampanyası olması tooa qualitative analiz uygundur.  

![][1]

İleri görünümlü bu yaklaşım hello en iyi şekilde tootreat karmaşası olmakla birlikte, karmaşıklık ile gelir: biz toodevelop hello modelleri arasında birden çok model bir archetype ve izleme bağımlılıkları vardır. Merhaba etkileşim modelleri arasında hello Aşağıdaki diyagramda gösterildiği gibi kapsüllenmiş:  

![][2]

*Şekil 4: çok model archetype birleşik*  

Biz toodeliver bütünsel bir yaklaşım toocustomer bekletme hello modelleri arasındaki etkileşim anahtar gerekli değildir. Her model mutlaka zamanla düşürür; Bu nedenle, hello örtük bir döngü mimarisidir (Merhaba NET-DM veri araştırma standardına göre ayarlamak benzer toohello archetype [***3***]).  

Merhaba genel döngü riski karar pazarlama kesimleme/ayrıştırma hala geçerli toomany iş sorunlarını olan bir genelleştirilmiş, yapısıdır. Basitleştirilmiş Tahmine dayalı bir çözüm izin vermeyen bir karmaşık iş sorunun tüm hello nitelikler sergilediğinden karmaşası analiz yalnızca bir güçlü, bu grubun sorunları temsilcisidir. Merhaba hello modern bir yaklaşım toochurn yönlerini özellikle hello yaklaşım vurgulanmış değil, ancak tüm modelde olduğu gibi hello sosyal yönlerini hello modelleme archetype içinde kapsüllenir sosyal.  

Bir ilginç burada büyük veri analizi ektir. Günümüzün telekomünikasyon ve perakende işletmeler müşterilerine hakkındaki ayrıntılı verileri toplamak ve biz kolayca bu hello birden çok model bağlantı eğilimleri gibi Gelişmekte olan verilen bir ortak eğilim olacağı için hello nesnelerin interneti öngörüyor ve İş tooemploy akıllı çözümleri birden çok katmanına izin bulunabilen cihazlar.  

 

## <a name="implementing-hello-modeling-archetype-in-machine-learning-studio"></a>Machine Learning Studio'da archetype modelleme hello uygulama
Yalnızca hello sorunun verildiğinde, hello en iyi şekilde tooimplement tümleşik bir model oluşturma ve puanlama yaklaşımı nedir? Bu bölümde, nasıl Biz bu Azure Machine Learning Studio kullanılarak başarılır gösterecek.  

Merhaba çok model şart karmaşası için genel bir archetype tasarlarken yaklaşımdır. Merhaba yaklaşım (Tahmine dayalı) parçası Puanlama bile hello çok model olmalıdır.  

Merhaba Aşağıdaki diyagramda hello prototip, hangi Machine Learning Studio toopredict karmaşası dört Puanlama algoritmalara kullanan oluşturduğumuz gösterilmektedir. birden çok model bir yaklaşım kullanarak için hello değil yalnızca toocreate ensemble sınıflandırıcı tooincrease doğruluğu, aynı zamanda tooprotect atlayarak sığdırma ve tooimprove Düzenleyici özellik seçimi karşı nedenidir.  

![][3]

*Şekil 5: Prototipi yaklaşım modelleme karmaşası*  

Merhaba aşağıdaki bölümler Machine Learning Studio kullanılarak uygulanan modeli Puanlama hello prototip hakkında daha fazla ayrıntı sağlar.  

### <a name="data-selection-and-preparation"></a>Veri seçimi ve hazırlık
Hello veri toobuild hello modelleri kullanılan ve puanı müşteriler hello gizlenmiş veri tooprotect müşteri gizliliği ile CRM dikey çözümden elde. Merhaba verileri içeren hello ABD 8.000 Aboneliklerde hakkında bilgi ve üç kaynağı birleştirir: verileri (abonelik meta verileri), etkinlik verileri (kullanım hello sisteminin) ve müşteri destek verileri sağlama. Merhaba veri herhangi bir işletme içermez ilgili hello müşteriler hakkında; bilgi Örneğin, bağlılık meta veriler veya kredi puanları içermez.  

Verileri hazırlama zaten olduğunu varsayıyoruz çünkü kolaylık sağlamak için ETL ve işlemler temizleme veri kapsamının dışında başka bir yerde yapılır.   

Modelleme için özellik seçimi başlangıç anlamlı hello rastgele orman modülü kullanan hello işlemine dahil predictors hello kümesinin Puanlama temel alır. Machine Learning Studio'da Hello uygulaması için hello ortalama, ORTANCA ve temsili özellikleri aralıklarını hesaplanır. Örneğin, kullanıcı etkinliği için minimum ve maksimum değerleri gibi hello nitel veriler için toplamalar eklendi.    

Biz de zamana bağlı bilgi hello için en son altı ay yakalandı. Verileri bir yıl için analiz ettik ve olmasa bile istatistiksel olarak önemli eğilimleri, karmaşıklık hello etkisini önemli ölçüde altı ay sonra düşer kuruldu.  

Merhaba en önemli nokta ETL, özellik seçimi de dahil olmak üzere bu hello tüm işlem ve modelleme kullanarak Microsoft Azure veri kaynaklarında Machine Learning Studio'daki uygulanmıştır.   

Merhaba aşağıdaki diyagramlarda kullanılan hello veri gösterilmektedir.  

![][4]

*Şekil 6: Alıntı (gizlenmiş) veri kaynağının*  

![][5]

*Şekil 7: veri kaynağından ayıklanan özellikleri*
 

> Bu veriler özeldir ve bu nedenle hello modeli ve veri paylaşılamaz unutmayın.
> Ancak, genel kullanıma açık verileri kullanarak bir benzer modeli için hello denemeler Bu örnek bkz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com/): [Telco müşteri karmaşıklığı](http://gallery.cortanaintelligence.com/Experiment/31c19425ee874f628c847f7e2d93e383).
> 
> Cortana Intelligence Suite kullanarak karmaşası analiz modeli nasıl uygulayacağınıza dair hakkında daha fazla toolearn, ayrıca öneririz [bu videoyu](https://info.microsoft.com/Webinar-Harness-Predictive-Customer-Churn-Model.html) üst düzey Program Yöneticisi Wee Hyong Tok tarafından. 
> 
> 

### <a name="algorithms-used-in-hello-prototype"></a>Merhaba prototip kullanılan algoritmaları
Dört makine öğrenimi algoritmalarını aşağıdaki hello kullandık toobuild hello prototip (özelleştirme yok):  

1. Lojistik regresyon (LR)
2. Artırılmış karar ağacı (BT)
3. Ortalama perceptron (AP)
4. Vektör makinesi (SVM) desteği  

Merhaba Aşağıdaki diyagramda bir kısmı hangi hello modelleri oluşturulan hello dizisini gösterir hello deneme tasarım yüzeyi gösterilmektedir:  

![][6]  

*Şekil 8: Machine Learning Studio'da modelleri oluşturma*  

### <a name="scoring-methods"></a>Puanlama yöntemleri
Biz, hello dört modelleri etiketli eğitim veri kümesi kullanarak skoru.  

Biz de hello Masaüstü SAS Kurumsal araştırıcısı 12 sürümü kullanılarak oluşturulmuş dataset tooa karşılaştırılabilir modeli Puanlama hello gönderildi. Biz hello doğruluğunu hello SAS modelini ve tüm dört Machine Learning Studio'da modelleri ölçülür.  

## <a name="results"></a>Sonuçlar
Bu bölümde, veri kümesi Puanlama hello üzerinde temel hello modellerin hello doğruluğu hakkında bizim bulgularını sunar.  

### <a name="accuracy-and-precision-of-scoring"></a>Doğruluk ve puanlama, duyarlık
Genellikle, Azure Machine Learning hello uygulamasında SAS doğruluğu yaklaşık 10-%15 (alanı altında eğri veya AUC) tarafından kullanılıyor.  

Ancak, hello en önemli ölçüm karmaşıklığı içinde hello misclassification oranıdır: diğer bir deyişle, tahmin edilen hello sınıflandırıcı tarafından olarak hello ilk N churners hangisinin gerçekte vermedi **değil** karmaşıklığı ve henüz özel işleme alınan? hello Aşağıdaki diyagramda bu misclassification oranı tüm hello modelleri için karşılaştırılır:  

![][7]

*Şekil 9: Passau prototip eğri alanında*

### <a name="using-auc-toocompare-results"></a>AUC toocompare sonuçları kullanma
Alanı altında eğri (AUC) olan genel bir ölçü temsil eden bir ölçüm *separability* pozitif ve negatif ortalamaya puanlarını hello dağıtımlarını arasında. Benzer toohello geleneksel alıcı işleci karakteristiğini (ROC) grafik, ancak bu hello AUC ölçüm toochoose bir eşik değeri gerektirmez önemli bir fark gelir. Bunun yerine, üzerinden hello sonuçları özetlenmektedir **tüm** olası seçenekler. Buna karşılık, hello dikey eksen ve yanlış pozitif oranına hello yatay eksen hello hello pozitif oranı hello geleneksel ROC grafik gösterir ve hello sınıflandırma eşik değişir.   

AUC değerlerine yoluyla karşılaştırıldığında modelleri toobe izin verdiğinden AUC genellikle oluşan bir ölçüyü olarak farklı algoritmalar (ya da farklı sistemleri) için kullanılır. Bu, endüstriler meteorology ve biosciences gibi popüler bir yaklaşımdır. Bu nedenle, AUC sınıflandırıcı performansını değerlendirmek için popüler bir araç temsil eder.  

### <a name="comparing-misclassification-rates"></a>Misclassification oranları karşılaştırma
Biz, hello misclassification hello dataset söz konusu oranlarına hello yaklaşık 8000 aboneliklerin CRM verileri kullanarak karşılaştırılan.  

* Merhaba SAS misclassification oranı % 10-15 oluştu.
* Merhaba Machine Learning Studio misclassification oranı hello ilk 200-300'ü churners 15-%20 oluştu.  

Danışman hizmetinin veya diğer özel işleme sunarak bu müşteriler yüksek risk toochurn hello yalnızca hello telekomünikasyon sektörün önemli tooaddress değil. Bu bakımdan hello Machine Learning Studio uygulaması hello SAS modelini ile eşit düzeye sonuçları elde eder.  

Biz çoğunlukla doğru olası churners sınıflandırma ilgilendiğiniz çünkü hello tarafından aynı, doğruluk duyarlık daha fazla önemlidir belirteci.  

Wikipedia diyagramı aşağıdaki hello canlı, kolay anlaşılır bir grafik hello ilişkisinde gösterilmektedir:  

![][8]

*Şekil 10: Kolaylığını doğruluğunu ve duyarlık arasında*

### <a name="accuracy-and-precision-results-for-boosted-decision-tree-model"></a>Artırılmış karar ağacı modeli için doğruluğunu ve duyarlık sonuçları
grafik görüntüler hello ham aşağıdaki hello toobe hello hello dört modelleri arasında en doğru olur boosted hello karar ağacı modeli için hello Machine Learning prototipi kullanarak Puanlama sonuçları:  

![][9]

*Şekil 11: Artırılmış karar ağacı model özellikleri*

## <a name="performance-comparison"></a>Performans karşılaştırma
Biz hello Machine Learning Studio'da modelleri ve hello Masaüstü SAS Kurumsal araştırıcısı 12,1 sürümü kullanılarak oluşturulmuş bir karşılaştırılabilir modeli kullanarak veri aktarılma skoru hello hızı karşılaştırılan.  

Aşağıdaki tablonun hello hello algoritmaları hello performansını özetlenmektedir:  

*Tablo 1. Genel performans (doğruluk) hello algoritmaları*

| LR | BT | AP | SVM |
| --- | --- | --- | --- |
| Ortalama modeli |Merhaba en iyi modeli |Underperforming |Ortalama modeli |

Machine Learning Studio'da büyük ölçüde nominal üzerinde yürütme ancak doğruluğu hızı için 15-25 oranında outperformed SAS olduğu barındırılan hello modeller.  

## <a name="discussion-and-recommendations"></a>Tartışma ve öneriler
Merhaba telekomünikasyon sektörün çeşitli yöntemler tooanalyze çıkmıştır dahil olmak üzere, karmaşıklığı:  

* Dört temel kategorileri için ölçümleri türetir.
  * **Varlık (örneğin, bir abonelik)**. Merhaba abonelik ve/veya hello konu karmaşası, müşteri hakkındaki temel bilgileri sağlayın.
  * **Etkinlik**. İlgili toohello varlık, örneğin, hello oturum açma sayısı tüm olası kullanım bilgilerini edinin.
  * **Müşteri desteği**. Destek sorunları veya müşteri ile etkileşim Hello aboneliğin var olup olmadığını müşteri destek günlükleri tooindicate bilgileri elde etme.
  * **Rekabet ve iş verileri**. Merhaba müşteri ile ilgili olası tüm bilgiler elde (örneğin, kullanılamıyor veya sabit tootrack olabilir).
* Önem toodrive özellik seçimi kullanın. Bu, bu boosted hello karar ağacı modeli taahhüdü yaklaşımını her zaman olduğu anlamına gelir.  

Hello kullan şu dört kategoriden hello görünümü oluşturan basit bir *belirleyici* her kategori, makul etkenlere biçimlendirilmiş dizinleri dayalı bir yaklaşım tooidentify müşteriler karmaşası için risk yeterli. Ne yazık ki, bu kavram yatkýn görünüyor rağmen yanlış anlama açıktır. Merhaba karmaşası zamana bağlı bir etkisidir ve toochurn katkıda bulunan hello Etkenler genellikle geçici durumda nedenidir. Bir müşteri tooconsider bugün bırakarak ne müşteri adayları yarın farklı olabilir ve bu kesinlikle altı ay şu andan itibaren farklı olacaktır. Bu nedenle, bir *probabilistic* zorunlu modelidir.  

Bu önemli gözlem genellikle genellikle bir iş zekası yönelimli bir yaklaşım tooanalytics tercih işletmede atlamış, çoğunlukla olduğu için daha kolay bir satış ve basit Otomasyon admits.  

Ancak, hello promise Self Servis analizi, Machine Learning Studio kullanarak, bilgi, bölüm veya departmanı tarafından türünden hello dört kategorilerini karmaşası hakkında machine learning için değerli bir kaynak olmasıdır.  

Azure Machine Learning ile gelen başka bir heyecan verici hello özelliği tooadd özel modülü toohello depo zaten kullanılabilen önceden tanımlanmış modüllerin bir özelliktir. Bu özelliği, aslında bir fırsat tooselect kitaplıkları oluşturur ve dikey pazarda için şablonlar oluşturma. Bir önemli Azure Machine Learning fark yaratan hello Pazar yerinde olur.  

Bu konuda hello gelecekteki, özellikle ilgili toobig veri analizi toocontinue umuyoruz.
  

## <a name="conclusion"></a>Sonuç
Bu yazı, genel framework kullanarak duyarlı bir yaklaşım tootackling hello yaygın sorun müşteri karmaşası açıklar. Biz modelleri Puanlama için prototip olarak kabul ve Azure Machine Learning kullanarak uygulanmadı. Son olarak, hello doğruluğunu ve hesaba toocomparable algoritmalar SAS'hello prototip çözümüyle performansını uygunluk.  

**Daha fazla bilgi için:**  

Bu makale size yardımcı? Lütfen görüşlerinizi bize bildirin. 1 (kötü) too5 (mükemmel) bir ölçekte bize nasıl bu kağıt oranı ve neden Bu derecelendirme verdiğiniz? Örneğin:  

* Bu son toohaving iyi örnek, Temizle yazma, mükemmel ekran görüntüleri veya başka bir nedenle yüksek derecelendirme?
* Bu son toopoor örnekler, benzer ekran görüntüleri veya belirsiz yazma düşük derecelendirme?  

Bu geri bildirim teknik incelemeler biz yayın hello kalitesini iyileştirmemize yardımcı olur.   

[Geri bildirim gönder](mailto:sqlfback@microsoft.com).
 

## <a name="references"></a>Başvurular
[1] Tahmine dayalı analiz: McKnight, bilgi yönetimi, Temmuz/Ağustos 2011, p.18-20 W. hello tahminleri ötesinde.  

[2] Wikipedia makale: [doğruluğunu ve duyarlılık](http://en.wikipedia.org/wiki/Accuracy_and_precision)

[3] [NET-DM 1.0: adım adım veri araştırma Kılavuzu](http://www.the-modeling-agency.com/crisp-dm.pdf)   

[4] [büyük veri pazarlama: müşterilerinize daha etkili bir şekilde gerçekleştirmesine ve sürücü değeri](http://www.amazon.com/Big-Data-Marketing-Customers-Effectively/dp/1118733894/ref=sr_1_12?ie=UTF8&qid=1387541531&sr=8-12&keywords=customer+churn)

[5] [Telco karmaşıklığı model şablonunun](http://gallery.cortanaintelligence.com/Experiment/Telco-Customer-Churn-5) içinde [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com/) 
 

## <a name="appendix"></a>Ek
![][10]

*Şekil 12: Anlık görüntüsünü karmaşası prototip sunu*

[1]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-1.png
[2]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-2.png
[3]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-3.png
[4]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-4.png
[5]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-5.png
[6]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-6.png
[7]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-7.png
[8]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-8.png
[9]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-9.png
[10]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-10.png
