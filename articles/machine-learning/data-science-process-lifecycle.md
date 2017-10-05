---
title: "Azure ekibi veri bilimi işlem ömrü | Microsoft Docs"
description: "Veri bilimi projelerinizi yürütmek için gerekli adımları."
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
ms.openlocfilehash: 9b8ef4f1165a89fa6ed1b64b44d58bb45f08f232
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="team-data-science-process-lifecycle"></a>Takım veri bilimi işlemi yaşam döngüsü

Takım veri bilimi işlem (TDSP) veri bilimi projelerinizi yapısı için kullanabileceğiniz önerilen bir yaşam döngüsü sağlar. Yaşam döngüsü başlangıçtan bitişe kadar bunlar çalıştırıldığında projeleri genellikle izlemeniz gereken adımları özetler. Başka bir veri bilimi yaşam döngüsü, gibi kullanıyorsanız [NET-DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) veya, kuruluşun kendi özel işlem görev tabanlı TDSP bu geliştirme süreçleri ile kullanmaya devam edebilirsiniz. 

Bu yaşam döngüsü, akıllı uygulamaların bir parçası dağıtmayı yönelik veri bilimi projeleri için tasarlanmıştır. Bu uygulamalar, Tahmine dayalı analiz için makine öğrenme veya yapay zeka modelleri dağıtın. Ayrıca keşif veri bilimi projeleri ve geçici analytics projeleri bu işlemi kullanmak yararlı olabilir. Ancak bu gibi durumlarda açıklanan bazı adımlar gerekli.    

Görsel gösterimi işte **takım veri bilimi işlemi yaşam döngüsü**. 

![TDSP yaşam döngüsü](./media/data-science-process-overview/tdsp-lifecycle.png) 

TDSP yaşam döngüsü yinelemeli olarak yürütülen beş temel aşamadan oluşur. Bunlar:

* **İş anlama**
* **Veri alımı ve anlama**
* **Modelleme**
* **Dağıtım**
* **Müşteri kabulü**

Her aşama için aşağıdaki bilgileri sağlayın:

* **Hedefleri**: belirli hedefler.
* **Bunu nasıl**: Tamamlanıyor üzerinde sağlanan yönergeleri ve ana hatlarıyla belirli görevleri.
* **Yapıları**: sonuçlara ve bunları oluşturan desteği.


## <a name="1-business-understanding"></a>1. Kurumsal yaklaşım

### <a name="goals"></a>Hedefleri
* **Anahtar değişkenleri** olarak hizmet verecek olan belirtilen **model hedefleri** ve ilgili olan ölçümleri kullanılır projesi için başarı belirleyin.
* İlgili **veri kaynakları** iş erişimi veya almak gereken tanımlanır.

### <a name="how-to-do-it"></a>Bunu nasıl
Bu aşamada ele iki ana görevleri şunlardır: 

* **Hedefleri tanımlayın**: anlamak ve iş sorunlarını belirlemek için müşteri ve diğer Paydaşlar ile çalışır. İş hedefleri tanımlayın ve veri bilimi teknikleri hedefleyebilirsiniz soruları formüle.
* **Veri kaynaklarını tanımlama**: Bul yardımcı olan ilgili verilerin proje amaçlarını tanımlama soruları yanıtlayın.

#### <a name="11-define-objectives"></a>1.1 hedefleri tanımlayın

1. Anahtar tanımlamak için bu adımın merkezi bir hedefi olan **iş değişkenleri** tahmin etmek analiz gereken. Bu değişkenler denir **model hedefleri** ve bunlarla ilişkilendirilmiş ölçümleri proje başarısını belirlemek için kullanılır. İki tür hedefleri satış tahmini veya sahte olan bir sırayı olasılığını gösterilebilir.

2. Tanımlamak **Proje hedefleri** soran ve ilgili ve belirli ve anlaşılır "diyez" soruları iyileştirme. Veri bilimi gibi soruları yanıtlamak için adlarını ve numaralarını kullanarak işlemidir. Sharp sorular sormak daha fazla bilgi için bkz: [veri bilimi nasıl](https://blogs.technet.microsoft.com/machinelearning/2016/03/28/how-to-do-data-science/) blogu. Veri bilimi / machine learning genellikle beş tür soruları yanıtlamak için kullanılır:
 
   * Ne kadar veya kaç tane? (regresyon)
   * Hangi kategori? (sınıflandırma)
   * Hangi Grup? (kümeleme)
   * Bu tuhaf mi? (anomali algılama)
   * Hangi seçeneği yapılması gerekir? (öneri)

    Hangi soruları istiyoruz ve nasıl yanıtlama, iş hedeflerinize başarır belirler.

3. Tanımlamak **takım projesi** roller ve sorumluluklar üyeleri belirterek. Daha fazla bilgi keşfedilen üzerinde yinelemek bir üst düzey kilometre taşı planı geliştirin.  

4. **Başarı ölçümlerini tanımlayın**. Örneğin: karmaşıklığını azaltmak için promosyon sunuyoruz böylece Itanium tabanlı sistemler için müşteri karmaşası tahmin doğruluğu, %x bu 3 aylık proje ucu tarafından elde etmek. Ölçümleri olmalıdır **akıllı**: 
   * **S**elirli 
   * **M**easurable
   * **A**chievable 
   * **R**elevant 
   * **T**IME bağlama 

#### <a name="12-identify-data-sources"></a>1.2 veri kaynaklarını tanımlama
Sharp sorularınıza bilinen örnekleri içeren veri kaynakları belirleyin. Aşağıdaki veriler için bakın:

* Verileri **Relevant** soruya. Hedef ve hedef ilgili özelliklerin ölçüleri sahibiz?
* Verileri bir **doğru ölçü** bizim modeli hedef ve ilgi özellikleri.

Örneğin, varolan sistemler toplamak ve sorun gidermek ve proje hedeflerinize ulaşmak için veri ek türlerini oturum gerektiğini bulmak için genel olarak görülmez, değil. Bu durumda, dış veri kaynakları için konum veya yeni verileri toplamak için sistemlerinizi güncelleştirme isteyebilirsiniz.

### <a name="artifacts"></a>Yapıtlar
Bu aşamada teslim edilebilir öğeler şunlardır:

* [**Kurucu belge**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Charter.md): standart şablon TDSP Proje yapısı tanımında sağlanır. Bu proje boyunca yeni bulmaları yapılan ve iş gereksinimleri değiştikçe güncelleştirilen bir yaşam belgedir. Daha fazla ayrıntı, bulma işlemi ilerlemeyi olarak ekleme, bu belgedeki bağlı yinelemek için kullanılan anahtardır. Müşteri tutmak ve diğer Paydaşlar değişiklikler yaparken söz konusu ve bunları değişiklikler nedeniyle açık bir şekilde iletir.  
* [**Veri kaynakları**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#raw-data-sources): Bu **ham veri kaynakları** bölümünü **veri tanımlarını** TDSP projesinde bulunan rapor **veri raporu** klasör. Ham verileri için özgün ve hedef konumları belirtir. Sonraki aşamalarda, analitik ortamınız için verileri taşımak için komut dosyaları gibi ek ayrıntıları doldurun.  
* [**Veri sözlükler**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/tree/master/Docs/DataDictionaries): Bu belgede istemci tarafından sağlanan veri açıklamalarını sağlar. Bu açıklamalar şemanın (veri türleri, bilgi doğrulama kuralları, eğer varsa) ve varlık ilişkisi diyagramları varsa hakkındaki bilgileri içerir.


## <a name="2-data-acquisition-and-understanding"></a>2. Veri edinme ve anlama

### <a name="goals"></a>Hedefleri
* Uygun analytics ortamında, model oluşturmak hazır bulunan hedef değişkenleri olan ilişkileri anlaşılır bir temiz, yüksek kaliteli veri kümesi.
* Çözüm mimarisi yenileyip verileri düzenli olarak puan veri ardışık geliştirilmiştir.

### <a name="how-to-do-it"></a>Bunu nasıl
Bu aşamada ele üç ana görevleri şunlardır:

* **Veri alma** hedef analitik ortamına.
* **Verileri araştırmak** veri kalitesini soruyu yanıtlamak yeterli olup olmadığını belirlemek için. 
* **Veri ardışık ayarlamak** yeni ya da düzenli olarak Puanlama amacıyla verilerin yenilenmesi.

#### <a name="21-ingest-the-data"></a>2.1 veri alma
Veri kaynağı konumlardan tahminleri yürütülecek olan ve burada analizi işlemlerini eğitim gibi hedef konumlara taşımak için işlemini ayarlayın. Teknik Ayrıntılar ve bunun çeşitli Azure Veri Hizmetleri ile nasıl seçenekleri için bkz: [veri analizi için depolama ortamlara yükleme](machine-learning-data-science-ingest-data.md). 

#### <a name="22-explore-the-data"></a>2.2 verileri keşfedin
Modellerinizi eğitmek önce verileri ses bir anlayış geliştirmek gerekir. Gerçek veri kümeleri genellikle gürültülü veya değerleri eksik veya diğer tutarsızlıklar barındırmasını. Veri özetleme ve görselleştirme, verilerinizin kalitesini denetleme ve modelleme için hazır hale gelmeden önce verileri işlemek için gerekli bilgileri sağlamak için kullanılabilir. Bu işlem genellikle yinelemelidir.

TDSP sağlar adlı otomatik bir yardımcı program [IDEAR](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/DataReport-Utils) görselleştirmek ve veri Özet Raporları Hazırlama yardımcı olacak. İlk hiçbir kodlama ile etkileşimli olarak ilk veri anlamak ve ardından veri keşfi ve görselleştirme için özel kod yazmanıza yardımcı olmak için verileri araştırmak için IDEAR ile başlamanızı öneririz. Veri temizleme ile ilgili yönergeler için bkz: [veri Gelişmiş için hazırlamak üzere görevleri makine öğrenme](machine-learning-data-science-prepare-data.md).  

Cleansed veri kalitesi memnun olduktan sonra sonraki adıma daha iyi yardımcı verileri devredilen desenleri seçin ve hedef için uygun bir Tahmine dayalı modeli geliştirmek anlamaktır. Bulgu verileri ne kadar iyi bağlı hedef için ve sonraki modelleme adımlara ilerlemek için yeterli veri olup arayın. Yeniden, bu işlem genellikle yinelemelidir. Başlangıçta önceki aşamasında tanımlanan veri kümesi artırmak için daha doğru veya daha çok ilgili veriler yeni veri kaynaklarıyla bulmak gerekebilir.  

#### <a name="23-set-up-a-data-pipeline"></a>2.3 veri ardışık ayarlayın
İlk alımı ve verilerini temizleme ek olarak, genellikle yeni verilerinizi puanlamada veya devam eden öğrenme işleminin bir parçası düzenli aralıklarla verileri yenilemek için bir işlem ayarlamanız gerekir. Bu, bir veri ardışık veya iş akışı ayarlayarak yapılabilir. Burada bir [örnek](machine-learning-data-science-move-sql-azure-adf.md) sahip işlem hattı ayarlama konusunda [Azure Data Factory](https://azure.microsoft.com/services/data-factory/). 

Bu aşamada veri ardışık çözüm mimarisini geliştirilir. Ardışık Düzen veri bilimi projesi aşağıdaki aşamaları ile paralel de geliştirilir. Ardışık Düzen toplu tabanlı veya akış/real-zamanlı veya iş gereksinimlerinize ve bu çözümü tümleştirilmekte mevcut sistemlerinizi kısıtlamaları bağlı olarak karma olabilir. 

### <a name="artifacts"></a>Yapıtlar
Sonuçlara bu aşamada verilmiştir.

* [**Veri Kalitesi raporu**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/DataSummaryReport.md): Bu rapor, veri özetleri, her özniteliği ve hedef arasındaki ilişkileri içerir değişken derecelendirme vs. [IDEAR](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/DataReport-Utils) TDSP parçası hızlı bir şekilde bir CSV dosyası veya ilişkisel bir tablo gibi herhangi bir tablo veri kümesi üzerinde bu raporu oluşturabilmesi olarak sağlanan aracı. 
* **Çözüm mimarisi**: bir model oluşturduktan sonra bu diyagramı veya Puanlama çalıştırmak için kullanılan veri ardışık veya tahminleri yeni verilerin açıklaması olabilir. Ayrıca, yeni verilere dayalı modelinizi yeniden eğitme için ardışık düzeni içerir. Belge depolanan [proje](https://github.com/Azure/Azure-TDSP-ProjectTemplate/tree/master/Docs/Project) TDSP dizin yapısı şablon kullanırken dizin.
* **Denetim noktası karar**: tam özellik mühendislik ve model oluşturmanın başlamadan önce beklenen değeri Bunun yapılması devam etmek yeterli olup olmadığını belirlemek için projeyi yeniden değerlendirene. Örneğin, devam etmek için daha fazla veri toplamak veya soruyu yanıtlamak için veri yok gibi proje abandon gerek hazır olması olabilir.


## <a name="3-modeling"></a>3. Modelleme

### <a name="goals"></a>Hedefleri
* Machine learning modelini en iyi veri özellikleri.
* Hedef en doğru tahmin bilgilendirici bir ML model.
* Üretim için uygun bir ML model.

### <a name="how-to-do-it"></a>Bunu nasıl
Bu aşamada ele üç ana görevleri şunlardır:

* **Özellik Mühendisliği**: model eğitim kolaylaştırmak için ham verileri veri özellikleri oluşturun.
* **Model Eğitimi**: kendi başarı ölçümlerini karşılaştırarak soru en doğru bir şekilde yanıtlar modeli bulunamadı.
* Modelinizi olup olmadığını belirlemek **üretim için uygun**.

#### <a name="31-feature-engineering"></a>3.1 özellik Mühendisliği
Özellik Mühendisliği ekleme, toplama ve analiz kullanılan özellikler oluşturmak için ham değişkenleri dönüşümü içerir. Bir model yönlendiren içine Insight istiyorsanız, özellikleri birbirleriyle nasıl ilişkili olduğunu ve bu özellikleri kullanmak için machine learning algoritmaları şeklini anlamanız gerekir. Bu adım, etki alanı uzmanlık ve veri araştırması adımda elde edilen Öngörüler yaratıcı bir birleşimini gerektirir. Bu, bulma ve çok sayıda ilgisiz değişkenleri kaçınarak bilgilendirici değişkenleri dahil, bir dengeleme işidir. Bilgilendirici değişkenleri bizim sonucunu iyileştirmek; İlişkisiz değişkenleri gereksiz bir gürültü modeline tanıtır. Puanlama sırasında elde edilen yeni veriler için bu özellikleri oluşturmak gerekir. Bu nedenle bu özellikler nesil yalnızca Puanlama zamanında mevcut olan verileri üzerinde bağlı olabilir. Azure veri teknolojiler kullanılırken özellik Mühendisliği hakkında teknik yönergeler için bkz [özellik Mühendisliği veri bilimi işleminde](machine-learning-data-science-create-features.md). 

#### <a name="32-model-training"></a>3.2 model eğitimi
Yanıt çalıştığınız sorusunu türüne bağlı olarak, kullanılabilir birçok modelleme algoritması vardır. Algoritmalar seçme ile ilgili yönergeler için bkz: [için Microsoft Azure Machine Learning algoritmaları seçme](machine-learning-algorithm-choice.md). Bu makale, Azure Machine Learning için yazılmıştır rağmen sağladığı Kılavuzu projeleri öğrenme herhangi bir makine için yararlıdır. 

İşlem modeli eğitim için aşağıdaki adımları içerir: 

* **Giriş verisi bölme** rastgele bir eğitim veri kümesi ve bir sınama veri kümesi modelleme için.
* **Modelleri oluşturabilir** eğitim veri kümesi kullanma.
* **Değerlendirme** (eğitim ve sınama veri kümesi) rakip machine learning algoritmaları çeşitli yanı sıra, bir dizi ilişkili geçerli verilerle ilgi soruyu yanıtlarken doğru sağlamıştır (parametre tarama da bilinir) parametreleri ayarlama.
* **"En iyi" çözümü belirlemenize** alternatif yöntemler arasında başarı ölçüm karşılaştırarak soruyu yanıtlamak için.

> [!NOTE]
> **Sızıntısını önlemek**: veri sızıntısını neden bir model veya unrealistically iyi tahminlerde için makine öğrenme algoritmasını sağlayan eğitim veri kümesi dışından verileri ekleme. Sızıntısını neden, Tahmine dayalı sonuçlar almak zaman bilimcilerine tedirgin veri doğru olması iyi göründüğü ortak bir nedeni. Bu bağımlılıklar algılamak zor olabilir. Genellikle sızıntısını önlemek için bir çözümleme veri kümesi oluşturma, bir model oluşturma ve doğruluk değerlendirme arasında yineleme gerektirir. 
> 
> 

Sağladığımız bir [otomatik modelleme ve Raporlama Aracı](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/Modeling) birden çok algoritmaları ve parametre bir taban çizgisi modeli oluşturmak üzere dağılımlarında çalıştırabilir TDSP ile. Ayrıca, rapor değişken önem dahil olmak üzere her modeli ve parametre birleşimi performansını özetlemeye modelleme bir temel oluşturur. Bu işlem ayrıca, daha fazla özellik Mühendisliği sürücüsü olarak yinelemelidir. 

### <a name="artifacts"></a>Yapıtlar
Bu aşamada üretilen yapılar içerir:

* [**Özellik kümeleri**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#feature-sets): modelleme için geliştirilen özellikleri açıklanan **özellik kümeleri** bölümünü **veri tanımı** rapor. Özellikler ve özellik nasıl oluşturulan üzerinde açıklama oluşturmak için kodu işaretçiler içerir.
* [**Rapor modeli**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Model/Model%201/Model%20Report.md): denenir, her model için bir standart her deneme hakkında ayrıntılar sağlayan şablon tabanlı rapor üretilir.
* **Denetim noktası karar**: model üretim sisteme dağıtmak için yeterli düzgün çalışıp olup olmadığını değerlendirin. Sorulacak anahtar bazı sorular şunlardır:
  * Modeli belirtilen test veri yeterli güvenle soruyu yanıtlamak mu? 
  * Herhangi bir alternatif yaklaşımlar denemelisiniz: ek veri toplamak, daha fazla özellik Mühendisliği yapın ya da diğer algoritmalarıyla denemeler?


## <a name="4-deployment"></a>4. Dağıtım

### <a name="goal"></a>Hedef
* Veri ardışık modelleriyle, bir üretim veya üretim benzeri bir ortam için son kullanıcı kabul dağıtılır. 

### <a name="how-to-do-it"></a>Bunu nasıl
Bu aşamada ele ana görevi:

* **Model faaliyete**: bir üretim veya uygulama tüketimi için üretim benzeri bir ortam modeli ve ardışık düzen dağıtın.

#### <a name="41-operationalize-a-model"></a>4.1 bir model faaliyete
İyi gerçekleştirmek modelleri kümesi oluşturduktan sonra bunlar kullanacak diğer uygulamalar için operationalized. İş gereksinimlerine bağlı olarak, tahminlerin gerçek zamanlı veya toplu olarak yapılır. Kullanıma hazır hale getirilmiş için çevrimiçi Web siteleri, elektronik tablolar, panolar veya iş ve arka uç uygulamalarının satır gibi çeşitli uygulamalardan kolayca tüketilen açık bir API arabirimi ile açığa çıkarılması modelleri vardır. Bir Azure Machine Learning web hizmeti ile modeli operationalization örnekleri için bkz: [bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md). Bu ayrıca telemetri ve üretim modeline izleme oluşturmak için en iyi uygulamadır ve raporlamada ve sorun giderme sonraki sistem durumuyla yardımcı olmak için veri ardışık dağıtılır.  

### <a name="artifacts"></a>Yapıtlar
* Sistem durumu ve anahtar ölçümleri durum Panosu.
* Dağıtım ayrıntıları raporla son modelleme.
* Son çözüm mimarisi belgesi.

## <a name="5-customer-acceptance"></a>5. Müşteri kabulü

### <a name="goal"></a>Hedef
* **Proje sonuçlara Sonlandır**: ardışık düzen, model ve bunların dağıtım bir üretim ortamında çağıran müşteri hedefleri olduğundan emin olun.

### <a name="how-to-do-it"></a>Bunu nasıl
Bu aşamada ele iki ana görevleri şunlardır:

* **Sistem doğrulama**: dağıtılan modeli ve ardışık düzen müşteri gereksinimlerine toplantı onaylayın.
* **Proje el dışı**: üretimde sistem çalıştırmaktır varlığa.

Müşteri, sistem iş gereksinimlerine ve üretim için sistemi dağıtmak için kabul edilebilir doğruluğu sorularla kendi istemci uygulama tarafından kullanılıyor yanıtlar karşıladığını doğrulamalıdır. Tüm belgeleri sonlandırılır ve gözden. Bir yandan dışı işlemleri için sorumlu varlığa projenin tamamlanır. Bu varlık, örneğin, bir BT veya müşteri veri bilimi ekibi veya sistem üretimde çalıştırmaktan sorumludur müşterinin bir aracı olabilir. 

### <a name="artifacts"></a>Yapıtlar
Bu Son aşamada üretilen ana yapay **çıkış proje rapor müşteri için**. Bu projenin hakkında bilgi edinin ve sistemi çalıştırmak bu kullanışlı tüm ayrıntılarını içeren teknik rapor eder. Bir [çıkış rapor](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Exit%20Report.md) şablon olarak kullanılan veya gereken belirli istemci için özelleştirilmiş TDSP tarafından sağlanır. 

## <a name="summary"></a>Özet
[Takım veri bilimi işlemi yaşam döngüsü](http://aka.ms/datascienceprocess) Tahmine dayalı modelleri kullanmak için gereken görevleri kılavuzluk tekrarlayan adımları dizisi olarak modellenir. Bu modeller, bir üretim ortamında akıllı uygulamaları geliştirmek için de dağıtılabilir. Bu işlem yaşam döngüsü veri bilimi proje İleri Temizle katılım uç noktası doğrultusunda taşımak devam etmek için hedefidir. Veri bilimi bir araştırma ve bulma alıştırmada olduğunu doğru olsa da, açıkça ekibinizin ve çalışanlar standartlaştırılmış şablonları yardımcı olabilecek yapıları iyi tanımlanmış bir dizi kullanılarak müşterileriniz için bu görevlerin iletişim kurması için kaçının yanlış anlama ve karmaşık veri bilimi projesinin Başarılı tamamlama olasılığını artırın.

## <a name="next-steps"></a>Sonraki adımlar
Tam işlem için tüm adımları gösteren uçtan uca talimatlara **belirli senaryolar** de sağlanır. Listelenen ve küçük resim açıklamasında ile bağlantılı [takım veri bilimi süreci gözden geçirmeleri](data-science-process-walkthroughs.md) konu.

