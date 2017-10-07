---
title: "aaaAzure takım veri bilimi işlem ömrü | Microsoft Docs"
description: "Adımlar tooexecute veri bilimi projelerinizi gerekir."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b1f677bb-eef5-4acb-9b3b-8a5819fb0e78
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev;
ms.openlocfilehash: 58114a1c2d3289d1c4b2781219d0bf9647dbccd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="team-data-science-process-lifecycle"></a>Takım veri bilimi işlemi yaşam döngüsü

Merhaba takım veri bilimi işlem (TDSP), önerilen yaşam döngüsü sağlar, veri bilimi projelerinizi toostructure kullanabilirsiniz. Merhaba yaşam döngüsü hello adımları, bunlar çalıştırıldığında izleyen projeleri genellikle başlangıç toofinish özetlenmektedir. Başka bir veri bilimi yaşam döngüsü, gibi kullanıyorsanız [NET-DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) veya, kuruluşun kendi özel işlem kullanmaya devam edebilirsiniz görev tabanlı TDSP bu geliştirme süreçleri ile Merhaba. 

Bu yaşam döngüsü, akıllı uygulamaların bir parçası hedeflenen tooship olan veri bilimi projeler için tasarlanmıştır. Bu uygulamalar, Tahmine dayalı analiz için makine öğrenme veya yapay zeka modelleri dağıtın. Ayrıca keşif veri bilimi projeleri ve geçici analytics projeleri bu işlemi kullanmak yararlı olabilir. Ancak bu gibi durumlarda açıklanan bazı adımlar gerekli.    

Görsel bir hello işte **takım veri bilimi işlemi yaşam döngüsü**. 

![TDSP yaşam döngüsü](./media/data-science-process-overview/tdsp-lifecycle.png) 

Merhaba TDSP yaşam döngüsü yinelemeli olarak yürütülen beş temel aşamadan oluşur. Bunlar:

* **İş anlama**
* **Veri alımı ve anlama**
* **Modelleme**
* **Dağıtım**
* **Müşteri kabulü**

Her aşama için aşağıdaki bilgilerle hello sunuyoruz:

* **Hedefleri**: belirli hedefler hello.
* **Nasıl toodo,**: ana hatlarıyla belirli görevleri ve bunları Tamamlanıyor sağlanan yönergeleri hello.
* **Yapıları**: hello sonuçlara ve hello desteği üretmek için.


## <a name="1-business-understanding"></a>1. Kurumsal yaklaşım

### <a name="goals"></a>Hedefleri
* Merhaba **anahtar değişkenleri** hello olarak tooserve olan belirtilen **model hedefleri** ve ilgili olan ölçümleri kullanılır hello başarı hello projesi için belirleyin.
* Merhaba ilgili **veri kaynakları** hello iş erişim tooor gereksinimlerini tooobtain olduğunu tanımlanır.

### <a name="how-toodo-it"></a>Nasıl toodo,
Bu aşamada ele iki ana görevleri şunlardır: 

* **Hedefleri tanımlayın**: İş Müşteri ve diğer Paydaşlar toounderstand ve hello iş sorunlarını tanımlayın. Merhaba iş hedeflerine ve veri bilimi teknikleri yöneltebilirsiniz tanımlamak soruları oluşturmak.
* **Veri kaynaklarını tanımlama**: yardımcı olan Bul hello ilgili verileri hello proje hello amaçlarını tanımlama hello soruları yanıtlayın.

#### <a name="11-define-objectives"></a>1.1 hedefleri tanımlayın

1. Bu adımın merkezi bir hedefi tooidentify hello anahtarıdır **iş değişkenleri** hello analiz toopredict gerekiyor. Başvurulan tooas hello bu değişkenlerdir **model hedefleri** ve bunlarla ilişkilendirilmiş hello ölçümleri hello projesinin kullanılan toodetermine hello başarılı. İki tür hedefleri sahte olan sipariş satış tahmin veya hello olasılığını gösterilebilir.

2. Merhaba tanımlamak **Proje hedefleri** soran ve ilgili ve belirli ve anlaşılır "diyez" soruları iyileştirme. Veri bilimi adlarını kullanarak hello ve işlemidir gibi soruları tooanswer numaralandırır. Sharp sorular sormak daha fazla bilgi için bkz: [nasıl toodo veri bilimi](https://blogs.technet.microsoft.com/machinelearning/2016/03/28/how-to-do-data-science/) blogu. Veri bilimi / machine learning, genellikle kullanılan tooanswer beş türden sorular:
 
   * Ne kadar veya kaç tane? (regresyon)
   * Hangi kategori? (sınıflandırma)
   * Hangi Grup? (kümeleme)
   * Bu tuhaf mi? (anomali algılama)
   * Hangi seçeneği yapılması gerekir? (öneri)

    Hangi soruları istiyoruz ve nasıl yanıtlama, iş hedeflerinize başarır belirler.

3. Merhaba tanımlamak **takım projesi** hello roller ve sorumluluklar üyeleri belirterek. Daha fazla bilgi keşfedilen üzerinde yinelemek bir üst düzey kilometre taşı planı geliştirin.  

4. **Başarı ölçümlerini tanımlayın**. Örneğin: promosyonlar tooreduce karmaşası sunuyoruz böylece Itanium tabanlı sistemler için müşteri karmaşası tahmin doğruluğu, %x hello sonuna kadar bu 3 aylık proje elde etmek. Merhaba ölçümleri olmalıdır **akıllı**: 
   * **S**elirli 
   * **M**easurable
   * **A**chievable 
   * **R**elevant 
   * **T**IME bağlama 

#### <a name="12-identify-data-sources"></a>1.2 veri kaynaklarını tanımlama
Yanıtlar tooyour sharp sorular bilinen örnekleri içeren veri kaynakları belirleyin. Veri aşağıdaki hello arayın:

* Verileri **Relevant** toohello soru. Merhaba hedef ve ilgili toohello hedef özellikleri ölçülerin sahibiz?
* Verileri bir **doğru ölçü** bizim modeli hedef ve özelliklerinin hello ilgi.

Seyrek değil, örneğin, varolan sistemleri toocollect gerekir ve veri tooaddress ek tür oturum toofind sorun hello ve hello proje hedeflerinize ulaşmak. Bu durumda, dış veri kaynakları için toolook istediğiniz veya sistemleri toocollect yeni verileri güncelleştirin.

### <a name="artifacts"></a>Yapıtlar
Bu aşamada hello sonuçlara şunlardır:

* [**Kurucu belge**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Charter.md): standart şablon hello TDSP Proje yapısı tanımını sağlanır. Bu yeni bulmaları yapılan ve iş gereksinimleri değiştikçe hello proje boyunca güncelleştirilen bir yaşam belgedir. Merhaba, hello bulma işlemi ilerlemeyi olarak daha fazla ayrıntı ekleme, bu belgedeki bağlı tooiterate anahtardır. Canlı hello müşteri ve diğer Paydaşlar hello değişiklik yapmadan söz konusu ve açık bir şekilde hello değişiklikleri toothem hello nedenlerle iletir.  
* [**Veri kaynakları**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#raw-data-sources): hello budur **ham veri kaynakları** hello bölümünü **veri tanımlarını** hello TDSP projesinde bulunan rapor **veri raporu**  klasörü. Merhaba özgün ve hello ham verileri hedef konumları belirtir. Sonraki aşamalarda, komut dosyaları toomove hello veri tooyour analitik ortamı gibi ek ayrıntıları doldurun.  
* [**Veri sözlükler**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/tree/master/Docs/DataDictionaries): Bu belgede hello istemci tarafından sağlanan hello veri açıklamalarını sağlar. Bu açıklamalar ve varlık ilişkisi diyagramları varsa hello hello şeması (veri türleri, doğrulama kuralları, varsa hakkında bilgi) hakkında bilgi içerir.


## <a name="2-data-acquisition-and-understanding"></a>2. Veri edinme ve anlama

### <a name="goals"></a>Hedefleri
* Merhaba uygun analytics ortamı hazır toomodel bulunan olan ilişkileri toohello hedef değişkenleri anlaşılır bir temiz, yüksek kaliteli veri kümesi.
* Merhaba veri ardışık düzen toorefresh ve puanı çözüm mimarisini veri düzenli olarak geliştirilmiştir.

### <a name="how-toodo-it"></a>Nasıl toodo,
Bu aşamada ele üç ana görevleri şunlardır:

* **Merhaba veri alma** hello hedef analitik ortamına.
* **Merhaba verileri araştırmak** hello veri kalitesini yeterli tooanswer hello soru ise toodetermine. 
* **Veri ardışık ayarlamak** tooscore yeni veya düzenli aralıklarla veri yenilenir.

#### <a name="21-ingest-hello-data"></a>2.1 hello veri alma
Merhaba işlem toomove hello verileri kaynak konumlardan tahminleri yürütülen toobe olan ve burada analizi işlemlerini eğitim gibi toohello hedef konumları ayarlayın. Teknik Ayrıntılar ve toodo nasıl çeşitli Azure veri hizmetleriyle bakın on seçenekleri için [veri analizi için depolama ortamlara yükleme](machine-learning-data-science-ingest-data.md). 

#### <a name="22-explore-hello-data"></a>2.2 hello veri keşfedin
Modellerinizi eğitmek önce toodevelop hello veri ses bir anlayış gerekir. Gerçek veri kümeleri genellikle gürültülü veya değerleri eksik veya diğer tutarsızlıklar barındırmasını. Veri özetleme ve görselleştirme, verilerinizin kullanılan tooaudit hello kalite olması ve modelleme için hazır hale gelmeden önce tooprocess veri hello hello bilgileri sağlayın. Bu işlem genellikle yinelemelidir.

TDSP sağlar adlı otomatik bir yardımcı program [IDEAR](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/DataReport-Utils) toohelp hello veri Görselleştirme ve veri Özet raporları hazırlayın. IDEAR ilk tooexplore hello veri toohelp ile başlayan öneririz hiçbir kodlama ile etkileşimli olarak ilk veri anlamak ve ardından veri keşfi ve görselleştirme için özel kod yazın. Merhaba veri temizleme ile ilgili yönergeler için bkz: [görevleri tooprepare veri Gelişmiş machine learning için](machine-learning-data-science-prepare-data.md).  

Merhaba cleansed hello veri kalitesiyle memnun olduktan sonra hello sonraki toobetter adımdır yardımcı hello verileri devredilen hello desenleri seçin ve hedef için uygun bir Tahmine dayalı modeli geliştirmek anlayın. Kanıt için ne kadar iyi bağlantılı hello veri toohello hedefidir ve yeterli veri toomove İleri hello sonraki modelleme adımlara olup arayın. Yeniden, bu işlem genellikle yinelemelidir. Başlangıçta hello önceki aşamasında tanımlanan daha doğru ya da daha çok ilgili veri tooaugment hello veri kümesi ile toofind yeni veri kaynakları gerekebilir.  

#### <a name="23-set-up-a-data-pipeline"></a>2.3 veri ardışık ayarlayın
Ayrıca veri toohello ilk alımı ve temizlenmesinden Merhaba, genelde bir işlem tooscore yeni verileri veya yenileme hello veri tooset düzenli olarak devam eden öğrenme işleminin bir parçası gerekir. Bu, bir veri ardışık veya iş akışı ayarlayarak yapılabilir. Burada bir [örnek](machine-learning-data-science-move-sql-azure-adf.md) nasıl tooset sahip işlem hattı yukarı [Azure Data Factory](https://azure.microsoft.com/services/data-factory/). 

Çözüm mimarisi hello veri ardışık bu aşamada geliştirilir. Hello ardışık düzen aşamaları hello veri bilimi projesinin aşağıdaki hello ile paralel de geliştirilir. Merhaba ardışık düzen toplu tabanlı olabilir veya akış/real-zamanlı veya işletmenizin bağlı olarak bir karma gerekir ve bu çözümü tümleştirilmekte mevcut sistemlerinizi kısıtlamaları hello. 

### <a name="artifacts"></a>Yapıtlar
Merhaba hello sonuçlara bu aşamada verilmiştir.

* [**Veri Kalitesi raporu**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/DataSummaryReport.md): Bu rapor, veri özetleri, her özniteliği ve hedef, vb. hello sıralaması değişkeni arasındaki ilişkileri içerir [IDEAR](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/DataReport-Utils) TDSP bir parçası olarak hemen oluşturabilirsiniz olarak sağlanan aracı Bu rapor bir CSV dosyası veya ilişkisel bir tablo gibi herhangi bir tablo veri kümesi üzerinde. 
* **Çözüm mimarisi**: bir model oluşturduktan sonra bu diyagrama veya veri kullanılan ardışık düzen toorun Puanlama veya tahminleri yeni verilerin açıklamasını olabilir. Ayrıca, yeni veri modelinizi dayalı hello ardışık düzen tooretrain içerir. Merhaba belge hello depolanan [proje](https://github.com/Azure/Azure-TDSP-ProjectTemplate/tree/master/Docs/Project) hello TDSP dizin yapısı şablon kullanırken dizin.
* **Denetim noktası karar**: tam özellik mühendislik ve model oluşturmanın başlamadan önce Bunun yapılması yeterli toocontinue hello değeri bekleniyor olup olmadığını hello proje toodetermine değerlendirene. , Örneğin, daha fazla veri hazır tooproceed, gerek toocollect olmalıdır, veya hello veri tooanswer hello soru yok gibi hello proje bırakın.


## <a name="3-modeling"></a>3. Modelleme

### <a name="goals"></a>Hedefleri
* Merhaba makine öğrenimi modeline en iyi veri özellikleri.
* Merhaba hedef en doğru tahmin bilgilendirici bir ML model.
* Üretim için uygun bir ML model.

### <a name="how-toodo-it"></a>Nasıl toodo,
Bu aşamada ele üç ana görevleri şunlardır:

* **Özellik Mühendisliği**: hello ham verileri toofacilitate model eğitim gelen veri özellikleri oluşturun.
* **Model Eğitimi**: hello modeli yanıtlar hello soruya en doğru kendi başarı ölçümlerini karşılaştırarak bulmak.
* Modelinizi olup olmadığını belirlemek **üretim için uygun**.

#### <a name="31-feature-engineering"></a>3.1 özellik Mühendisliği
Özellik Mühendisliği ekleme, toplama ve raw değişkenleri toocreate dönüşümü ilgilidir hello hello çözümlemede kullanılan özellikler. Bir model yönlendiren içine Insight istiyorsanız, daha sonra toounderstand diğer ilgili tooeach özellikleridir nasıl ve hello machine learning algoritmaları toouse nasıl bu özellikleri gerekir. Bu adım, etki alanı uzmanlık ve hello veri araştırması adımda elde edilen Öngörüler yaratıcı bir birleşimini gerektirir. Bu, bulma ve çok sayıda ilgisiz değişkenleri kaçınarak bilgilendirici değişkenleri dahil, bir dengeleme işidir. Bilgilendirici değişkenleri bizim sonucunu iyileştirmek; İlişkisiz değişkenleri gereksiz bir gürültü hello modeline tanıtır. Ayrıca Puanlama sırasında elde edilen yeni veriler için toogenerate bu özellikleri gerekir. Bu nedenle bu özelliklerin hello nesil yalnızca Puanlama hello zamanında mevcut olan verileri üzerinde bağlı olabilir. Azure veri teknolojiler kullanılırken özellik Mühendisliği hakkında teknik yönergeler için bkz [özellik Mühendisliği hello veri bilimi işlemi içinde](machine-learning-data-science-create-features.md). 

#### <a name="32-model-training"></a>3.2 model eğitimi
Yanıt çalıştığınız sorusunu türüne bağlı olarak, kullanılabilir birçok modelleme algoritması vardır. Merhaba algoritmaları seçme ile ilgili yönergeler için bkz: [nasıl Microsoft Azure Machine Learning için toochoose algoritmaları](machine-learning-algorithm-choice.md). Bu makale, Azure Machine Learning için yazılmıştır rağmen projeleri öğrenme herhangi bir makine için yararlıdır sağlar Kılavuzu hello. 

Merhaba işlem modeli eğitim hello aşağıdaki adımları içerir: 

* **Bölünmüş hello giriş verileri** rastgele bir eğitim veri kümesi ve bir sınama veri kümesi modelleme için.
* **Merhaba modelleri oluşturabilir** hello eğitim veri kümesi kullanma.
* **Değerlendirme** (eğitim ve sınama veri kümesi) bir dizi rakip makine hello birlikte algoritmaları hello ile ilgi hello soruyu yanıtlarken doğru sağlamıştır (parametre tarama da bilinir) çeşitli ilişkili ayarlama parametreleri öğrenme Geçerli veri.
* **Merhaba "en iyi" çözümü belirlemenize** hello başarı ölçüm alternatif yöntemler arasında karşılaştırarak tooanswer hello soru.

> [!NOTE]
> **Sızıntısını önlemek**: veri sızıntısını neden veri hello ekleme tarafından izin veren bir model ya da makine öğrenme algoritmasını toomake unrealistically iyi tahminleri dış hello eğitim kümesinden. Sızıntısını veri bilimcilerine çok iyi toobe göründüğü Tahmine dayalı sonuçları true adımına geldiğinizde neden tedirgin yaygın bir nedenidir. Bu bağımlılıklar sabit toodetect olabilir. tooavoid sızıntısını, genellikle bir analiz veri kümesi oluşturma, bir model oluşturma ve hello doğruluğu değerlendirme arasında yineleme gerektirir. 
> 
> 

Sağladığımız bir [otomatik modelleme ve Raporlama Aracı](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/Modeling) TDSP ile birden çok algoritmaları aracılığıyla mümkün toorun ve parametre taramalar tooproduce temel model. Ayrıca, rapor değişken önem dahil olmak üzere her modeli ve parametre birleşimi performansını özetlemeye modelleme bir temel oluşturur. Bu işlem ayrıca, daha fazla özellik Mühendisliği sürücüsü olarak yinelemelidir. 

### <a name="artifacts"></a>Yapıtlar
Bu aşamada üretilen hello yapılar içerir:

* [**Özellik kümeleri**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#feature-sets): hello modelleme için geliştirilen hello özellikleri hello açıklanan **özellik kümeleri** hello bölümünü **veri tanımı** rapor. İşaretçileri toohello kodu toogenerate hello özellikleri ve hello özelliği nasıl oluşturulan üzerinde açıklama içerir.
* [**Rapor modeli**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Model/Model%201/Model%20Report.md): denenir, her model için bir standart her deneme hakkında ayrıntılar sağlayan şablon tabanlı rapor üretilir.
* **Denetim noktası karar**: hello modeli de yeterli toodeploy gerçekleştiriyor olup olmadığını değerlendirmek, tooa üretim sistem. Bazı önemli sorular tooask şunlardır:
  * Mu hello modeli yanıt hello soru yeterli güvenle hello test verileri verilen? 
  * Herhangi bir alternatif yaklaşımlar denemelisiniz: ek veri toplamak, daha fazla özellik Mühendisliği yapın ya da diğer algoritmalarıyla denemeler?


## <a name="4-deployment"></a>4. Dağıtım

### <a name="goal"></a>Hedef
* Veri ardışık modelleriyle dağıtılan tooa üretim veya üretim benzeri bir ortam için son kullanıcı kabul markalarıdır. 

### <a name="how-toodo-it"></a>Nasıl toodo,
Bu aşamada ele ana görev hello:

* **Merhaba modeli faaliyete**: hello modeli ve ardışık düzen tooa üretim veya uygulama tüketimi için üretim benzeri bir ortam dağıtın.

#### <a name="41-operationalize-a-model"></a>4.1 bir model faaliyete
İyi gerçekleştirmek modelleri kümesi oluşturduktan sonra bunlar için diğer uygulamaları tooconsume operationalized. Merhaba iş gereksinimlerine bağlı olarak, tahminlerin gerçek zamanlı veya toplu olarak yapılır. kullanıma hazır hale getirilmiş toobe, çevrimiçi Web siteleri, elektronik tablolar, panolar veya iş ve arka uç uygulamalarının satır gibi çeşitli uygulamalardan kolayca tüketilen açık bir API arabirimi ile kullanıma sunulan toobe hello modelleri vardır. Bir Azure Machine Learning web hizmeti ile modeli operationalization örnekleri için bkz: [bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md). Ayrıca bir en iyi yöntem toobuild telemetri olan ve üretim modeli hello içine izleme ve raporlama ve sorun giderme sonraki sistem durumuyla veri dağıtılan ardışık düzen toohelp hello.  

### <a name="artifacts"></a>Yapıtlar
* Sistem durumu ve anahtar ölçümleri durum Panosu.
* Dağıtım ayrıntıları raporla son modelleme.
* Son çözüm mimarisi belgesi.

## <a name="5-customer-acceptance"></a>5. Müşteri kabulü

### <a name="goal"></a>Hedef
* **Merhaba proje sonuçlara Sonlandır**: hello ardışık düzen, hello modeli ve bunların dağıtım bir üretim ortamında çağıran müşteri hedefleri olduğundan emin olun.

### <a name="how-toodo-it"></a>Nasıl toodo,
Bu aşamada ele iki ana görevleri şunlardır:

* **Sistem doğrulama**: dağıtılan hello modeli ve ardışık düzen müşteri gereksinimlerine toplantı onaylayın.
* **Proje el dışı**: toorun Merhaba sistemdir üretimde toohello varlık.

Merhaba müşteri hello sistem iş gereksinimlerini karşıladığından ve hello yanıtlar soruları kabul edilebilir doğruluğu toodeploy hello sistem tooproduction kullanmak için kendi istemci uygulaması tarafından hello doğrulamalıdır. Tüm hello belgeleri sonlandırılır ve gözden. Bir yandan dışı hello proje toohello varlığın işlemleri için sorumlu tamamlanır. Bu varlık, örneğin, bir BT veya müşteri veri bilimi ekibi veya üretim hello sistem çalıştırmaktan sorumludur hello müşterinin bir aracı olabilir. 

### <a name="artifacts"></a>Yapıtlar
Bu Son aşamada üretilen hello ana yapıdır hello **çıkış proje rapor müşteri için**. Bu hello teknik rapor hakkında yararlı bu toolearn hello proje tüm ayrıntılarını içeren ve hello sistem çalışmayabilir. Bir [çıkış rapor](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Exit%20Report.md) şablon olarak kullanılan veya gereken belirli istemci için özelleştirilmiş TDSP tarafından sağlanır. 

## <a name="summary"></a>Özet
Merhaba [takım veri bilimi işlemi yaşam döngüsü](http://aka.ms/datascienceprocess) hello görevlerde kılavuzluk tekrarlayan adımların sırasını toouse Tahmine dayalı modelleri gerektiğinde modellenir. Bu modeller, bir üretim ortamında işlevden toobe toobuild akıllı uygulamalarda dağıtılabilir. Merhaba bu işlem yaşam döngüsü toocontinue toomove veri bilimi proje İleri Temizle katılım uç noktası doğrultusunda hedefidir. Bir araştırma alıştırmada veri bilimi olduğu ve bu görevler tooyour takım ve çalışanlar standartlaştırılmış şablonları yardımcı olabilecek yapıları iyi tanımlanmış bir dizi kullanılarak müşterileriniz mümkün tooclearly olan bulma iletişim doğru iken yanlış anlama kaçının ve karmaşık veri bilimi projesinin Başarılı tamamlama hello olasılığı artar.

## <a name="next-steps"></a>Sonraki adımlar
Tam için hello işlemdeki tüm hello adımları gösteren uçtan uca talimatlara **belirli senaryolar** de sağlanır. Listelenen ve küçük resim Merhaba açıklamalarına ile bağlantılı [takım veri bilimi süreci gözden geçirmeleri](data-science-process-walkthroughs.md) konu.

