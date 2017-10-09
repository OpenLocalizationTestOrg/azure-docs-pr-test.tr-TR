---
title: "aaaFeature mühendislik ve Azure Machine Learning seçimde | Microsoft Docs"
description: "Özellik Seçimi ve özellik Mühendisliği Hello amaçları açıklar ve machine learning hello verileri geliştirme sürecinin içindeki rollerine örnekler sağlar."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ceb524d-842e-4f77-9eae-a18e599442d6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2017
ms.author: zhangya;bradsev
ROBOTS: NOINDEX
redirect_url: machine-learning-data-science-create-features
redirect_document_id: True
ms.openlocfilehash: e3e59329bf46f334396f5975b4e656137362d7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="feature-engineering-and-selection-in-azure-machine-learning"></a>Azure Machine Learning’de özellik mühendisliği ve seçimi
Bu konuda hello amaçları özelliği mühendislik ve makine öğrenme hello verileri geliştirme sürecinde özellik seçimi açıklanmaktadır. Bu, hangi Azure Machine Learning Studio tarafından sağlanan örnekleri kullanarak bu işlemleri içeren gösterilmektedir.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Machine learning'de kullanılan hello eğitim verileri genellikle hello seçimi veya özellikleri ayıklama hello ham verilerden toplanan tarafından geliştirilebilir. Örnek tasarlanan bir özelliğin nasıl tooclassify hello görüntüleri el yazısı karakter olduğunu öğrenme hello bağlamda yoğunluğunu bit eşlemi hello ham bit dağıtım verilerinden oluşturulan. Bu haritada hello karakter hello kenarlarına hello ham dağıtım daha verimli belirlemeye yardımcı olabilir.

Tasarlanan ve seçilen özelliklerin hello tooextract hello anahtar bilgileri hello verilerde bulunan çalışır hello eğitim işlem verimliliğini artırmak. Bunlar ayrıca bu modeller tooclassify hello giriş verisi hello gücünü doğru şekilde artırmak ve toopredict sonuçlarını ilgi daha fazla yerine. Ayrıca özellik mühendislik ve seçim toomake hello öğrenme daha pkı'ya tractable birleştirebilirsiniz. Bunu geliştirme tarafından yapar ve sonra Özellikler hello sayısının azaltılması toocalibrate veya train model gerekli. Matematiksel konuşarak hello özellikleri seçili tootrain hello modeli hello veri hello düzenleri açıklayabilir ve sonuçları başarıyla tahmin bağımsız değişkenlerini en az sayıda vardır.

Merhaba mühendislik ve çeşitli özellikler genellikle dört adımdan oluşur daha büyük bir işlemin bir parçası olduğu:

* Veri toplama
* Verileri geliştirme
* Model oluşturma
* Son işlem

Mühendislik ve seçim hello veri geliştirme adım makine öğrenme olun. Bu işlem üç yönlerini bizim amaçlar için ayırt edilen:

* **Verileri ön işleme**: Bu işlem toplanan verileri hello çalıştığında tooensure temiz ve tutarlı. Birden çok veri kümeleri, eksik verileri işleme, işleme tutarsız veri tümleştirme ve veri türlerini dönüştürme gibi görevleri içerir.
* **Özellik Mühendisliği**: Bu işlem toocreate ek ilgili özelliklerinden varolan Ham Özellikler öğrenme algoritmasının hello veri ve tooincrease Tahmine dayalı güç toohello hello çalışır.
* **Özellik Seçimi**: Bu işlem özgün veri özellikleri tooreduce hello boyut hello eğitim sorununun anahtar kısmı hello seçer.

Bu konu yalnızca hello özelliği mühendislik ve özellik seçimi yönlerini hello veri geliştirme işlemi kapsar. Merhaba veri ön-işleme adımı hakkında daha fazla bilgi için bkz: [Azure Machine Learning Studio'da verilerin önceden işlenmesi](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/).

## <a name="creating-features-from-your-data--feature-engineering"></a>Özellikleri oluşturma verilerinizden--özellik Mühendisliği
Merhaba eğitim verilerini her biri bir dizi özellik (değişkenleri veya sütunlarında depolanan alanları) sahip örnekleri (kayıtları veya satır depolanan gözlemleri) oluşan bir matris oluşur. Merhaba Deneysel tasarımında belirtilen hello hello veri beklenen toocharacterize hello düzenleri özellikleridir. Merhaba ham verileri alanları doğrudan eklenebilir çoğunu seçilen özelliği kullanılan kümesini tootrain bir model hello rağmen ek tasarlanan özellikleri genellikle hello ham verileri toogenerate Gelişmiş eğitim veri kümesi hello özelliklerinden oluşturulan toobe gerekir.

Ne tür bir özellikler tooenhance hello veri kümesi bir modeli eğitimindeki oluşturulsun mu? Merhaba eğitim geliştirmek tasarlanan özellikleri daha iyi hello veri hello düzenleri ayıran bilgi sağlar. Açıkça yakalanan ya da özgün hello kolayca görünen hello yeni özellikler tooprovide ek bilgileri beklediğiniz veya varolan özelliği ayarlanmış ancak bu işlem bir resimler bir şeydir. Ses ve üretken kararları genellikle bazı etki alanı uzmanlık gerektirir.

Azure Machine Learning ile başlayan Machine Learning Studio'da örnekleri kullanarak concretely bu işlem sağlanan kolay toograsp olur. İki örnek burada sunulur:

* Regresyon örnek ([bisiklet kiralamaları hello sayısını tahmin](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4)) hello hedef değerleri nerede bilinir denetimli bir deney olarak
* Bir metin araştırma sınıflandırma örneği kullanarak [özellik karma][feature-hashing]

### <a name="example-1-adding-temporal-features-for-a-regression-model"></a>Örnek 1: bir regresyon modeli için zamana bağlı özellik ekleme
toodemonstrate tooengineer regresyon görev için özellikleri nasıl kullanalım hello deneme "isteğe bağlı bisiklet tahmin" Azure Machine Learning Studio'da. Bu deneme Hello amacı toopredict hello hello bisiklet, diğer bir deyişle, hello sayısı belirli bir ay, gün veya saat içinde bisiklet kiralama olanağı için taleptir. Merhaba veri kümesi **bisiklet kiralama UCI veri kümesi** hello ham girdi verisi olarak kullanılır.

Bu veri kümesi hello Washington DC bisiklet kiralama ağında hello Amerika Birleşik Devletleri içinde tutar sermaye Bikeshare şirket gerçek verileri temel alır. Merhaba veri kümesi bisiklet kiralamaları hello sayısı belirli bir günde bir saat içinde 2011 too2012 temsil eder ve 17379 satırları ve 17 sütunları içerir. Merhaba ham özellik kümesi (sıcaklık, nem, Rüzgar hızı) hava koşulları ve hello gün (tatil veya hafta içi günü) hello türünü içerir. Merhaba alan toopredict olan **cnt**, belirli bir saat içinde hello bisiklet kiralamaları temsil eden ve 1 too977 aralıkları sayısı.

tooconstruct etkili hello eğitim verilerini özelliklerinde, dört regresyon modeli yerleşiktir hello kullanarak aynı algoritmanın ancak dört farklı eğitim verilerini ayarlar. Hello dört veri kümelerini temsil aynı ham giriş verisi Merhaba, ancak özellikleri artan sayıda ile ayarlayın. Bu özellikler, dört kategorilerde gruplanır:

1. A = hava durumu, tatil + haftanın günü + hafta özellikleri hello tahmin edilen gün için
2. B = her hello önceki 12 saat rented bisiklet sayısı
3. C = her hello hello önceki 12 günde aynı rented bisiklet sayısı saat
4. D = her hello hello adresindeki önceki 12 hafta aynı rented bisiklet sayısı saat ve hello aynı gün

Merhaba özgün ham verileri zaten, özellik kümesi A yanı sıra, hello diğer üç özellik kümesi işlemi mühendislik hello özelliği kullanılarak oluşturulur. Özellik B yakalamaları hello son talep hello bisiklet ayarlayın. Özellik C yakalamaları hello talep bisiklet için belirli bir saatte ayarlayın. Özellik D yakalamaları talep bisiklet için belirli saat ve belirli hello haftanın günü ayarlayın. Özellik kümeleri her hello dört eğitim veri kümesini içeren bir, A + B, A + B + C ve A + B + C + D, sırasıyla.

Hello Azure Machine Learning deneme'da, bu dört eğitim veri kümesi hello önceden işlenen giriş veri kümesinde dört dalları aracılığıyla oluşturulur. Merhaba soldaki şube dışında her bu dallar içeren bir [R betiği yürütün] [ execute-r-script] bir dizi (özelliği ayarlar B, C ve D) özellikleri türetilmiş modülü sırasıyla oluşturulur ve eklenmiş veri kümesi toohello alındı. Aşağıdaki şekilde hello hello R betiği toocreate özellik kümesi B hello ikinci sol dalında kullandığınız gösterir.

![Bir özellik kümesi oluşturma](./media/machine-learning-feature-selection-and-engineering/addFeature-Rscripts.png)

Merhaba aşağıdaki tabloda hello hello performans sonuçları hello dört modellerin karşılaştırması özetlenmektedir. Merhaba en iyi sonuçlar özellikleri tarafından A + B + C gösterilmektedir. Ek özellik kümeleri hello eğitim verileri eklendiğinde o hello hata oranı azaltır unutmayın. Bu özellik kümeleri B ve C hello regresyon görev için ilgili ek bilgileri sağlayın hello bizim presumption doğrular. Merhaba D özellik kümesi ekleme tooprovide hello hata oranı, ek herhangi azalma görünmüyor.

![Performans Sonuçları karşılaştırma](./media/machine-learning-feature-selection-and-engineering/result1.png)

### <a name="example2"></a>Örnek 2: özellikleri metin araştırma oluşturma
Özellik Mühendisliği yaygın görevleri ilgili tootext, belge sınıflandırma ve düşünceleri analiz gibi araştırma içinde uygulanır. Çeşitli kategorilerde tooclassify belgeleri istediğinizde, örneğin, tipik bir varsayım hello kelimeler ve ifadeler bir belge kategoride yer alan başka bir belge kategoride olasılığını toooccur olmasıdır. Diğer bir deyişle, hello hello sözcük veya tümcecik dağıtım mümkün toocharacterize farklı Belge kategorileri sıklığıdır. Metin araştırma uygulamalarda işlem mühendislik hello gerekli toocreate hello özellikleri giriş verisi hello gibi metin içeriği tek tek parçaları genellikle gördükleri için sözcük veya tümcecik sıklıklarını içeren bir özelliktir.

tooachieve bu görev, adında bir teknik *özellik karma* uygulanan tooefficiently dizinlerini Aç rastgele metin özelliklerini olduğu. Her metin özelliği (kelimeler ve ifadeler) tooa belirli dizini, bir karma işlevi toohello özellikleri uygulayarak ve karma değerlerini dizinlerini doğrudan kullanarak bu yöntemi işlevleri ilişkilendirme yerine.

Azure Machine Learning ile var olan bir [özellik karma] [ feature-hashing] bu sözcük veya tümcecik özellikleri oluşturur modülü. Merhaba aşağıdaki şekilde bu modülü kullanmanın bir örneği gösterilmektedir. Merhaba giriş veri kümesi, iki sütunları içerir: 1 too5 hello gerçek gözden geçirme ve içerik arasında değişen hello kitap derecesi. Bu Hello amacı [özellik karma] [ feature-hashing] modülüdür hello oluşum sıklığını hello karşılık gelen kelimeler ve ifadeler hello belirli kitap gözden içinde Göster tooretrieve yeni özellikler. toouse bu modül aşağıdaki adımları toocomplete hello gerekir:

1. Merhaba giriş metin içeren bir select hello sütun (**Col2** Bu örnekte).
2. Ayarlama *bitsize karma* 2 gelir too8 ^ 8 = 256 özellikleri oluşturulur. Merhaba sözcük veya tümcecik hello metin ise too256 dizinlerini karma. parametre hello *bitsize karma* 1 too31 aralığından. Merhaba parametresini tooa büyük number, hello sözcükler ayarlayın ya da tümcecikleri olasılığını toobe hello aynı karma dizini.
3. Merhaba parametre kümesi *N-gram* too2. Bu, hello giriş metinden hello oluşumu sıklığı unigrams (özelliği her tek word için) ve bigrams (bitişik sözcüklerin her çifti için bir özellik) alır. parametre hello *N-gram* hello en çok bir özelliği dahil sıralı sözcükleri toobe sayısını gösteren 0 too10 aralığından.  

![Karma modülü özelliği](./media/machine-learning-feature-selection-and-engineering/feature-Hashing1.png)

Merhaba aşağıdaki şekilde bu yeni özellikleri nasıl göründüğünü gösterir.

![Karma örnek özellik](./media/machine-learning-feature-selection-and-engineering/feature-Hashing2.png)

## <a name="filtering-features-from-your-data--feature-selection"></a>Verilerinizi--özellik seçimi özelliklerinden filtreleme
*Özellik Seçimi* olan yaygın olduğu bir işlemi uygulanan toohello yapımı sınıflandırma veya regresyon görevler gibi Tahmine dayalı modelleme görevleri için eğitim veri kümesi. Merhaba, tooselect kümesinden hello özgün veri boyutları hello verilerde özellikleri toorepresent hello maksimum farkı en az sayıda kullanarak azaltan hello özelliklerinin bir kısmı hedeftir. Bu alt özellikler kümesini hello yalnızca özellikler dahil toobe tootrain hello modeli içerir. Özellik Seçimi iki ana amaca hizmet eder:

* Özellik Seçimi sıklıkla ortadan kaldırarak ilgisiz, yedekli sınıflandırma doğruluğu artırır veya özellikleri son derece bağıntılı.
* Merhaba model Eğitim işlemini daha verimli hale getirir özellik seçimi düşüşleri hello sayısı özellikleri. Bu destek vektör makineleri gibi pahalı tootrain olan öğrencileriyle için özellikle önemlidir.

Özellik Seçimi tooreduce hello birçok özellik hello kullanılan veri kümesini tootrain hello modelinde aradığı rağmen değil genellikle, tooby hello terim başvurulan *boyut azaltma.* Özellik Seçimi yöntemleri, bunları değiştirmeden hello verilerdeki özgün özelliklerinin bir kısmı ayıklayın.  Boyut azaltma yöntemleri hello özgün özellikler dönüştürmek ve bu nedenle bunlarda değişiklik tasarlanan özellikleri kullanın. Asıl bileşen analiz, kurallı bağıntı analiz ve tekil değer ayrıştırma boyut azaltma yöntemler örnekleridir.

Denetimli bağlamda özellik seçimi yöntemlerin yaygın olarak uygulanan bir kategori filtresi tabanlı özelliği seçimdir. Her özellik ve hello target özniteliği arasında Hello bağıntı değerlendirerek istatistiksel ölçü tooassign bir puan tooeach özelliği bu yöntemleri uygulayın. Merhaba özellikleri sonra kullanabileceğiniz hello puana göre sıralanır tooset hello eşiğini tutma veya belirli bir özellik ortadan kaldırır. Pearson bağıntı, karşılıklı bilgileri ve hello kikare testi hello istatistiksel ölçümler bu yöntemlerinde kullanılan örneklerindendir.

Azure Machine Learning Studio modülleri için özellik seçimi sağlar. Hello aşağıdaki şekilde gösterildiği gibi bu modülleri dahil [filtre tabanlı özellik seçimi] [ filter-based-feature-selection] ve [Fisher doğrusal Discriminant analiz] [ fisher-linear-discriminant-analysis].

![Özellik Seçimi örneği](./media/machine-learning-feature-selection-and-engineering/feature-Selection.png)

Örneğin, hello kullan [filtre tabanlı özellik seçimi] [ filter-based-feature-selection] yukarıda özetlenen hello metni araştırma örneği modülüyle. Merhaba 256 özellikler kümesi oluşturulduktan sonra toobuild bir regresyon modeli istediğinizi varsayalım [özellik karma] [ feature-hashing] modülü ve bu hello yanıt değişken **Col1**ve kitap temsil eder gözden derecelendirme 1 too5 arasında değişen. Ayarlama **Puanlama yöntemi özellik** çok**Pearson bağıntı**, **hedef sütun** çok**Col1**, ve **sayısı istenen Özellikler** çok**50**. Merhaba Modülü [filtre tabanlı özellik seçimi] [ filter-based-feature-selection] hello target özniteliği ile birlikte 50 özellikleri içeren bir veri kümesini üreten **Col1**. Hello aşağıdakiler, bu deneme gösterir hello akışını şekil ve giriş parametreleri hello.

![Özellik Seçimi örneği](./media/machine-learning-feature-selection-and-engineering/feature-Selection1.png)

Merhaba aşağıdaki şekilde hello sonuçta elde edilen veri kümeleri gösterilmektedir. Her bir özelliğin tabanlı hello kendisi ve hello arasında Pearson bağıntı üzerinde puanlanır target özniteliği **Col1**. üst puanları Hello özelliklerle tutulur.

![Filtre tabanlı özellik seçimi veri kümeleri](./media/machine-learning-feature-selection-and-engineering/feature-Selection2.png)

Şekil gösterir aşağıdaki hello hello seçili özelliklerin karşılık gelen puanları hello.

![Seçilen özellik puanları](./media/machine-learning-feature-selection-and-engineering/feature-Selection3.png)

Bu uygulama tarafından [filtre tabanlı özellik seçimi] [ filter-based-feature-selection] modülü, 50 dışında özellikleri seçili özelliklerinin çoğu hello hedef değişkeni ile ilişkili hello sahip oldukları için 256 **Col1** yöntemi Puanlama hello üzerinde temel **Pearson bağıntı**.

## <a name="conclusion"></a>Sonuç
Özellik Mühendisliği ve özellik seçimi iki adımı genellikle bir machine learning modelini oluştururken tooprepare hello eğitim verilerini gerçekleştirilen markalarıdır. Normalde, özellik Mühendisliği uygulanan ilk toogenerate ek özellikler, ve ardından hello özellik seçimi adım gerçekleştirilen tooeliminate ilgisiz, yedekli ya da yüksek oranda ilişkili özellikler.

Her zaman mutlaka tooperform özellik Mühendisliği veya özellik seçimi değildir. Gerekli olup olmadığını sahip veya, hello algoritması, çekme, toplamak ve hello deneme amacı hello hello verilere bağlıdır.

<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/
