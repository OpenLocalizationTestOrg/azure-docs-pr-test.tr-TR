---
title: Machine Learning Studio'da basit deneme aaaA | Microsoft Docs
description: "Bu makine öğrenimi öğreticisi kolay bir veri bilimi deneyinde size kılavuzluk etmektedir. Biz hello regresyon algoritması kullanılarak bir araba fiyatını tahmin."
keywords: "deneme,doğrusal regresyon,makine öğrenimi algoritmaları,makine öğrenimi öğreticisi,tahmine dayalı modelleme teknikleri,veri bilimi deneyi"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b6176bb2-3bb6-4ebf-84d1-3598ee6e01c6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: fb215851d380acf7d0f4934a426283369f9c4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a>Makine öğrenimi öğreticisi: Azure Machine Learning Studio'da ilk veri bilimi denemenizi oluşturma

Daha önce **Azure Machine Learning Studio** kullanmadıysanız, bu öğretici sizin için hazırlanmıştır.

Bu öğreticide, biz nasıl adım geçireceğiz toouse Studio hello için bir makine öğrenimi denemesinin ilk toocreate saat. Merhaba deneme hello marka ve teknik belirtimler gibi farklı değişkenleri alarak otomobil fiyatını tahmin analitik bir modeli test edeceğiz.

> [!NOTE]
> Bu öğretici, denemenize üzerine nasıl toodrag ve bırak modülleri hello temelleri birbirine bağlamak, hello denemeyi çalıştırın ve hello sonuçlarına bakın gösterir. Makine öğrenme genel konu veya nasıl tooselect ve kullanım Studio'daki 100 + yerleşik algoritmaları ve veri işleme modülleri hello toodiscuss hello yapacağız değil.
>
>Yeni toomachine öğrenme değilseniz, video serisi hello [yeni başlayanlar için veri bilimi](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) iyi toostart olabilir. Her gün dilini ve kavramları kullanarak harika giriş toomachine öğrenme bu video serisidir.
>
>Machine learning ile benzer, ancak Machine Learning Studio ve hello machine learning algoritmaları içerdiği hakkında daha fazla genel bilgi arıyorsanız, iyi bazı kaynaklar aşağıda verilmiştir:
>
- [Machine Learning Studio nedir?](machine-learning-what-is-ml-studio.md) - Bu Studio’ya yönelik ileri seviye bir genel bakıştır.
- [Makine öğrenme algoritmasını örneklerle temel](machine-learning-basics-infographic-with-algorithm-examples.md) -bu bilgi grafiği toolearn Machine Learning Studio ile dahil machine learning algoritmaları hello farklı türleri hakkında daha fazla bilgi istiyorsanız kullanışlıdır.
- [Machine Learning Kılavuzu](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) -bu kılavuz hello bilgi grafiği yukarıdaki, ancak etkileşimli bir biçimde benzer bilgileri kapsar.
- [Makine öğrenimi algoritması bilgi sayfası](machine-learning-algorithm-cheat-sheet.md) ve [nasıl Microsoft Azure Machine Learning için toochoose algoritmaları](machine-learning-algorithm-choice.md) -bu indirilebilir posteri ve eşlik eden makale hello Studio algoritmaları derinlemesine ele alınmıştır.
- [Machine Learning Studio: Algoritması ve modül Yardım](https://msdn.microsoft.com/library/azure/dn905974.aspx) -hello tam başvuru için makine öğrenimi algoritması da dahil olmak üzere tüm Studio modülleri budur

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a>Machine Learning Studio yardımı nasıl çalışır?

Machine Learning Studio'da Tahmine dayalı modelleme teknikleri ile önceden programlanmış sürükle ve bırak modüllerini kullanan bir denemeyi yukarı kolay tooset kolaylaştırır.

Etkileşimli, görsel bir çalışma alanı kullanarak ***veri kümeleri*** ve analiz ***modüllerini*** etkileşimli bir tuvale sürükleyip bırakın. Birlikte tooform bağlanmak bir ***denemeler*** , Machine Learning Studio'da çalıştırın.
***Bir model oluşturmak***, ***hello modeli eğitmek***, ve ***puanı ve test hello modeli***.

Model tasarımınızı hello deneme düzenleme yineleyebilirsiniz ve kadar verir çalıştıran Aradığınız sonuçları hello. Modeliniz hazır olduğunda, başkalarının yeni veriler göndererek tahminler alabilmesi için bir ***web hizmeti*** olarak yayımlayabilirsiniz.

## <a name="open-machine-learning-studio"></a>Machine Learning Studio’yu açma

Studio ile çalışmaya tooget Git çok[https://studio.azureml.net](https://studio.azureml.net). Machine Learning Studio’da daha önce oturum açtıysanız **Oturum Aç**’a tıklayın. Veya **Buradan kaydolun**’a tıklayıp ücretsiz ve ücretli seçenekler arasından seçim yapın.

![TooMachine Learning Studio'da oturum açın][sign-in-to-studio]
<br/>
***TooMachine Learning Studio'da oturum açın***

## <a name="five-steps-toocreate-an-experiment"></a>Beş adımı toocreate bir deneme

Bu makine öğrenimi öğreticisinde, beş temel adımı toobuild Machine Learning Studio toocreate, eğitme, bir deneme izleyin ve modelinizi puan:

- **Bir model oluşturma**
    - [1. Adım: Verileri alma]
    - [2. adım: hello verileri hazırlama]
    - [3. Adım: Özellikleri tanımlama]
- **Tren hello modeli**
    - [4. Adım: Bir öğrenme algoritması seçme ve uygulama]
- **Puan ve test modeli hello**
    - [5. Adım: Yeni otomobil fiyatlarını tahmin etme]

[1. Adım: Verileri alma]: #step-1-get-data
[2. adım: hello verileri hazırlama]: #step-2-prepare-the-data
[3. Adım: Özellikleri tanımlama]: #step-3-define-features
[4. Adım: Bir öğrenme algoritması seçme ve uygulama]: #step-4-choose-and-apply-a-learning-algorithm
[5. Adım: Yeni otomobil fiyatlarını tahmin etme]: #step-5-predict-new-automobile-prices

> [!TIP] 
> Merhaba çalışan bir kopyasını bulabilirsiniz hello denemesinde aşağıdaki [Cortana Intelligence Galerisi](https://gallery.cortanaintelligence.com). Çok Git**[ilk veri bilimi denemeler - otomobil fiyat tahmini](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)**  tıklatıp **Studio'da Aç** toodownload hello denemeyi Machine Learning içine bir kopyasını Studio çalışma alanı.


## <a name="step-1-get-data"></a>1. Adım: Verileri alma

tooperform machine learning gereken ilk şey hello verilerdir.
Machine Learning Studio'da kullanabileceğiniz birçok örnek veri kümesi bulunur ve birçok kaynaktan verileri içeri aktarabilirsiniz. Bu örnekte, hello örnek veri kümesini kullanacağız **otomobil fiyat verileri (ham)**, çalışma alanınızda bulunur.
Bu veri kümesi; marka, model, teknik belirtimler ve fiyat gibi bilgiler dahil olmak üzere birçok ayrı otomobil için giriş içerir.

İşte nasıl tooget hello dataset denemenize.

1. Tıklayarak yeni bir deneme oluşturma **+ yeni** hello Machine Learning Studio penceresinin hello altında seçin **DENEMELER**ve ardından **boş denemeler**.

2. Merhaba deneme hello tuvale hello üstünde görebilirsiniz varsayılan adı verilir. Bu metin seçin ve toosomething anlamlı, örneğin, yeniden adlandırma **otomobil fiyat tahmini**. Merhaba adı toobe benzersiz gerek yoktur.

    ![Merhaba deneme yeniden adlandırma][rename-experiment]

2. Merhaba deneme tuvalinin toohello solundaki veri kümelerini ve modülleri paletini ' dir. Tür **otomobil** hello arama kutusuna etiketli bu palet toofind hello dataset hello üstündeki **otomobil fiyat verileri (ham)**. Bu veri kümesi toohello deneme tuvaline sürükleyin.

    ![Merhaba otomobil veri kümesi bulma ve hello deneme tuvaline sürükleyin][type-automobile]
    <br/>
    ***Merhaba otomobil veri kümesi bulma ve hello deneme tuvaline sürükleyin***

toosee bu verileri hello otomobil veri kümesinin hello altındaki hello çıkış bağlantı noktasına tıklayın ve ardından gibi göründüğünü **Görselleştir**.

![Merhaba çıkış bağlantı noktasına tıklayın ve "Görselleştir" seçin][select-visualize]
<br/>
***Merhaba çıkış bağlantı noktasına tıklayın ve "Görselleştir" seçin***

> [!TIP]
> Veri kümelerini ve modülleri giriş ve bağlantı noktaları hello altındaki çıkış bağlantı noktaları küçük daireler - hello üstünde, giriş bağlantı noktaları tarafından temsil edilen çıkış.
toocreate denemenizi üzerinden veri akışı, bir modül tooan giriş bağlantı noktası başka bir çıkış bağlantı noktasına bağlanırsınız.
Herhangi bir zamanda hello verileri bu noktada hello veri akışında benzer bir veri kümesi veya modülü toosee hello çıkış bağlantı noktasına tıklatabilirsiniz.

Bu örnek veri kümesi her bir otomobil örneği de satır olarak görünür ve her otomobil ile ilişkili hello değişkenleri sütun olarak görünür. Merhaba değişkenleri için belirli bir otomobil verildiğinde, tootry toopredict hello fiyat sağdaki sütun (sütun başlıklı 26, "Fiyat") yapacağız.

![Merhaba veri görselleştirme penceresinde Hello otomobil veri görüntüle][visualize-auto-data]
<br/>
***Merhaba veri görselleştirme penceresinde Hello otomobil veri görüntüle***

Merhaba tıklayarak görselleştirme penceresini kapat hello "**x**" Merhaba sağ üst köşedeki.

## <a name="step-2-prepare-hello-data"></a>2. adım: hello verileri hazırlama

Genellikle bir veri kümesi analiz edilmeden önce biraz ön işleme gerekir. Örneğin, değerleri hello çeşitli satırların sütunlarında mevcut eksik hello fark. Bu eksik değerlerin toobe hello modeli hello verileri doğru şekilde analiz edebilmesi temizlenmesi gerekir. Örneğimizde eksik değerleri olan satırları kaldıracağız. Ayrıca, hello **normalleştirilmiş kayıplar** sütununda eksik değerleri büyük bir kısmının Biz bu sütun hello modelin tamamen dışında şekilde.

> [!TIP]
> Değerleri giriş verilerinden eksik temizleme hello hello modüllerin çoğu kullanmak için bir önkoşuldur.

Merhaba kaldıran bir modül önce eklediğimiz **normalleştirilmiş kayıplar** sütun tamamen ve ardından eksik verileri olan herhangi bir satırın kaldırır başka bir modül ekleriz.

1. Tür **sütunları seçin** hello arama kutusuna hello modül paleti toofind hello hello üstündeki [Select Columns in Dataset sütun] [ select-columns] modül toohello deneme tuvaline sürükleyin . Bu modül bize modeli tooinclude istediğiniz veya dışarıda verilerin hangi sütunların hello tooselect sağlar.

2. Merhaba Hello çıkış bağlantı noktasına bağlanmak **otomobil fiyat verileri (ham)** dataset toohello giriş bağlantı noktası hello [Select Columns in Dataset sütun] [ select-columns] modülü.

    ![Merhaba "Sütun Dataset içinde seçin" modülü toohello deneme tuvalinin ekleyin ve bunu bağlayın][type-select-columns]
    <br/>
    ***Merhaba "Sütun Dataset içinde seçin" modülü toohello deneme tuvalinin ekleyin ve bunu bağlayın***

3. Merhaba tıklatın [Select Columns in Dataset sütun] [ select-columns] modülü ve tıklatın **başlatma Sütun seçiciyi** hello içinde **özellikleri** bölmesi.

    - Hello solda tıklatın **kurallarla**
    - **Şununla Başla** altında **Tüm sütunlar**’a tıklayın. Bu yönlendirir [Select Columns in Dataset sütun] [ select-columns] tüm hello sütunlar (dışında hakkında tooexclude ki bu sütunları) aracılığıyla toopass.
    - Merhaba aşağı açılan listeler, seçin **hariç** ve **sütun adları**ve ardından hello metin kutusunun içine tıklayın. Sütun listesi görüntülenir. Seçin **normalleştirilmiş kayıplar**, ve eklenen toohello metin kutusu olur.
    - Merhaba onay işareti (Tamam) düğmesine tooclose hello Sütun seçiciyi (üzerinde hello sağ alt köşedeki) tıklayın.

    ![Merhaba Sütun seçiciyi Başlat ve "normalleştirilmiş kayıplar" Merhaba sütununu hariç tutmak][launch-column-selector]
    <br/>
    ***Merhaba Sütun seçiciyi Başlat ve "normalleştirilmiş kayıplar" Merhaba sütununu hariç tutmak***

    Şimdi hello Özellikler bölmesi için **Select Columns in Dataset sütun** , tüm sütunlardan dışında hello kümesinden geçeceğini belirtir **normalleştirilmiş kayıplar**.

    ![Merhaba "normalleştirilmiş kayıplar" sütunun dışarıda Hello Özellikler bölmesi gösterir][showing-excluded-column]
    <br/>
    ***Merhaba "normalleştirilmiş kayıplar" sütunun dışarıda Hello Özellikler bölmesi gösterir***

    > [!TIP]
    Bir yorum tooa modülü bağlantısındaki hello modülü ve metin girme tarafından ekleyebilirsiniz. Bu, bir bakışta görmenize yardımcı hangi hello modülün denemenizde yapıyor. Bu durumda, hello çift [Select Columns in Dataset sütun] [ select-columns] modülü ve türü hello Açıklama "Dışlama normalleştirilmiş kayıplar."
    >
    >


    ![Bir modül tooadd yorum çift tıklatın][add-comment]
    <br/>
    ***Bir modül tooadd yorum çift tıklatın***

3. Sürükleme hello [Clean Missing Data] [ clean-missing-data] modülü toohello tuvale denemek ve toohello bağlanmak [Select Columns in Dataset sütun] [ select-columns] modülü. Merhaba, **özellikleri** bölmesinde, **tüm satırı Kaldır** altında **temizleme modu**. Bu yönlendirir [Clean Missing Data] [ clean-missing-data] tüm eksik değerleri olan satırları kaldırarak tooclean hello veri. Merhaba modüle çift tıklayın ve "eksik değerli satırları Kaldır" Merhaba yorum yazın

    ![Merhaba temizleme modunu ayarlama çok "Kaldır tüm satırı" hello "Clean Missing Data" modülü][set-remove-entire-row]
    <br/>
    ***Merhaba temizleme modunu ayarlama çok "Kaldır tüm satırı" hello "Clean Missing Data" modülü***

4. Tıklayarak Hello denemeyi çalıştırın **çalıştırmak** hello sayfanın hello sonundaki.

    Merhaba deneme çalışması sona erdi, tüm hello modülleri başarıyla tamamlandı yeşil onay işareti tooindicate vardır. Ayrıca hello fark **çalıştırma tamamlandı** hello sağ üst köşesinde durumunda.

![Çalıştırdıktan sonra hello deneme aşağıdakine benzer görünmelidir][early-experiment-run]
<br/>
***Çalıştırdıktan sonra hello deneme aşağıdakine benzer görünmelidir***

> [!TIP]
> Neden hello denemeyi şimdi karşılaştınız? Çalışan hello deney tarafından hello aracılığıyla hello dataset hello sütun tanımları veri geçirmek [Select Columns in Dataset sütun] [ select-columns] modülü ile Merhaba [Clean Missing Data] [ clean-missing-data] modülü. Biz bağlanmak çok herhangi bir modül buna[Clean Missing Data] [ clean-missing-data] aynı bilgiler da sahip olur.

Tüm hello deneme toothis noktası yukarı içinde yaptığınızdan temiz hello veri olabilir. Tooview temizlenmesi hello dataset isterseniz, sol çıkış bağlantı noktasına hello hello tıklatın [Clean Missing Data] [ clean-missing-data] modülü ve select **Görselleştir**. Bu hello fark **normalleştirilmiş kayıplar** sütun dahil olduğunu artık ve eksik değerlerin yok.

Merhaba veri temiz olduğunu, hangi özellikler biz hazır toospecify dileriz toouse hello Tahmine dayalı modelde oluşturacağız.

## <a name="step-3-define-features"></a>3. Adım: Özellikleri tanımlama

Machine learning'de *özellikler*, ilgilendiğiniz bir şeyin tek tek ölçülebilir özellikleridir. Veri kümemizde her bir satır bir otomobili temsil eder ve her bir sütun da bu otomobilin bir özelliğidir.

Tahmine dayalı bir model oluşturmak için özellikleri iyi bir dizi deney ve hello sorun hakkında bilgi gerektirir bulma toosolve istiyor. Bazı özellikleri diğerlerinden hello hedefi tahmin etmede daha uygundur. Ayrıca, bazı özelliklerin diğer özelliklerle güçlü bir bağıntısı vardır ve kaldırılabilirler. Biz bir tutmak ve hello tahmin önemli ölçüde etkilemeden hello diğer kaldırmak için örneğin, şehir-mpg ile otoban-mpg yakından ilişkilendirilir.

Şimdi kümemize hello özelliklerinin bir alt kümesi kullanan bir model oluşturalım. Daha sonra dönmek ve farklı özellikler seçebilir, hello denemeyi tekrar çalıştırabilir ve daha iyi sonuçlar alırsanız bkz. Ancak toostart, özellikler aşağıdaki hello deneyelim:

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. Başka bir sürükleyin [Select Columns in Dataset sütun] [ select-columns] modülü toohello deneme tuvaline. Merhaba çıkış bağlantı noktasına sol hello bağlanmak [Clean Missing Data] [ clean-missing-data] hello modülü toohello girişi [Select Columns in Dataset sütun] [ select-columns] modülü.

    ![Merhaba "Sütun Dataset içinde seçin" modülü toohello "Clean Missing Data" modülünü bağlama][connect-clean-to-select]
    <br/>
    ***Merhaba "Sütun Dataset içinde seçin" modülü toohello "Clean Missing Data" modülünü bağlama***

2. Merhaba modüle çift tıklayın ve "Tahmin için özellik seç." yazın

2. Tıklatın **başlatma Sütun seçiciyi** hello içinde **özellikleri** bölmesi.

3. **Kurallar ile**’ye tıklayın.

4. **Şununla Başla** altında **Sütun yok**’a tıklayın. Merhaba filtre satırını seçin **INCLUDE** ve **sütun adları** ve sütun adları listesi hello metin kutusunda seçin. Belirttiğimiz olanları hello dışında herhangi bir sütundan (Özellikler) hello modülü toonot geçiş yönlendirir.

5. Merhaba onay işareti (Tamam) düğmesine tıklayın.

    ![Merhaba sütunlar (Özellikler) tooinclude hello öngörü seçin][select-columns-to-include]
    <br/>
    ***Merhaba sütunlar (Özellikler) tooinclude hello öngörü seçin***

Bu öğrenme algoritmasının hello sonraki adımda kullanacağız toopass toohello istiyoruz yalnızca hello özellikleri içeren filtrelenmiş bir veri kümesini oluşturur. Daha sonra geri dönüp farklı özellikler seçerek yeniden deneyebilirsiniz.

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a>4. Adım: Bir öğrenme algoritması seçme ve uygulama

Merhaba veriler hazır olduğuna göre Tahmine dayalı bir model oluşturmak eğitim ve sınama oluşur. Veri tootrain hello modelimizi kullanacağız ve ardından biz hello modeli toosee test edeceksiniz ne kadar yakından mümkün toopredict fiyatlar değil.
<!-- For now, don't worry about *why* we need tootrain and then test a model.-->

*Sınıflandırma* ve *regresyon*, denetimli makine öğrenimi algoritmasının iki türüdür. Sınıflandırma; renk gibi (kırmızı, mavi veya yeşil) tanımlanmış bir kategori kümesinden yanıt tahmin eder. Regresyon kullanılan toopredict bir sayı değil.

Bir sayıdır toopredict price istediğimiz çünkü bir regresyon algoritmasıdır. kullanacağız. Bu örnek için, basit bir *çizgisel regresyon* modeli kullanacağız.

> [!TIP]
> Machine learning algoritmaları farklı türleri hakkında daha fazla toolearn istiyorsanız ve ne zaman toouse onları, yeni başlayanlar seri için veri bilimi hello içinde hello ilk video görebileceği [hello beş veri bilimi yanıtlar sorular](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md). Merhaba bilgi grafiği ayrıca görünebilir [makine öğrenme algoritmasını örneklerle temel](machine-learning-basics-infographic-with-algorithm-examples.md), veya hello denetleyin [makine öğrenimi algoritması bilgi sayfası](machine-learning-algorithm-cheat-sheet.md).

Biz hello fiyatına dahildir veri kümesini vererek hello modeli eğitmek. Merhaba modeli hello veri ve otomobil ait özellikler ve onun fiyat arasındaki bağıntıları arayın tarar. Ardından hello modeli test edeceksiniz - biz aşina ki otomobiller için bir özellikler kümesi sağlar ve ne kadar yakın hello modeli toopredicting hello bilinen fiyat geldiğini görmek.

Merhaba model eğitim hem de ayrı eğitim ve test veri kümeleri halinde hello veri bölerek sınama için verilerimizi kullanacağız.

1. Seçin ve hello sürükleyin [bölünmüş veri] [ split] modülü toohello tuvale denemek ve son toohello bağlantı [Select Columns in Dataset sütun] [ select-columns] Modül.

2. Merhaba tıklatın [bölünmüş veri] [ split] modülü tooselect. Hello bulur **hello satırlar için kesir değerini ilk çıkış veri kümesi** (Merhaba içinde **özellikleri** bölmesinde toohello hello tuvalin sağındaki) ve too0.75 ayarlayın. Bu şekilde, biz hello veri tootrain hello modeli yüzde 75'ini kullanın ve geri test etmek için yüzde 25 tutun (daha sonra farklı yüzdeleri kullanarak ile deneyebilirsiniz).

    ![Set hello hello "Böl verileri" modülü too0.75 kesir bölme][set-split-data-percentage]
    <br/>
    ***Set hello hello "Böl verileri" modülü too0.75 kesir bölme***

    > [!TIP]
    > Merhaba değiştirerek **rastgele doldurma** parametresi, eğitim ve test etme için farklı rastgele örnekler oluşturabilirsiniz. Bu parametre hello hello sözde rastgele sayı üreticisinin doldurulmasını denetler.

2. Merhaba denemeyi çalıştırın. Merhaba deneme çalıştırdığınızda hello [Select Columns in Dataset sütun] [ select-columns] ve [bölünmüş veri] [ split] modüllerinin sütun tanımlarını toohello geçirin Modül biz sonraki ekleme.  

3. algoritma, öğrenme tooselect hello hello genişletin **Machine Learning** hello modül paleti toohello sol kategorisinde hello tuvale ve ardından genişletin **modeli Başlat**. Bu, kullanılan tooinitialize machine learning algoritmaları olabilir modülleri çeşitli kategorileri görüntüler. Bu deneme için hello seçin [doğrusal regresyon] [ linear-regression] hello altında Modülü **regresyon** kategori ve toohello deneme tuvaline sürükleyin.
(Ayrıca hello modülü hello palet arama kutusuna "doğrusal regresyon" yazarak bulabilirsiniz.)

4. Bulma ve hello sürükleyin [Train Model] [ train-model] modülü toohello deneme tuvaline. Merhaba Hello çıkışına bağlayın [doğrusal regresyon] [ linear-regression] modülü toohello sol hello girişi [Train Model] [ train-model] modül ve hello bağlanın Eğitim verileri çıkışına (sol bağlantı noktası) hello [bölünmüş veri] [ split] modülü toohello sağ girişi hello [Train Model] [ train-model] Modül.

    !["Doğrusal regresyon" ve "Böl verileri" Hello "Train Model" modülü tooboth hello modülleri Bağlan][connect-train-model]
    <br/>
    ***"Doğrusal regresyon" ve "Böl verileri" Hello "Train Model" modülü tooboth hello modülleri Bağlan***

5. Merhaba tıklatın [Train Model] [ train-model] modülü,'ı tıklatın **başlatma Sütun seçiciyi** hello içinde **özellikleri** bölmesinde ve ardından hello **fiyat** sütun. Bu bizim modeli giderek toopredict olduğunu hello değerdir.

    Merhaba seçin **fiyat** hello taşıyarak hello Sütun seçiciyi sütununda **kullanılabilir sütunlar** toohello listesinde **seçili sütunların** listesi.

    ![Merhaba "Train Model" modülü için Hello fiyat sütun seçin][select-price-column]
    <br/>
    ***Merhaba "Train Model" modülü için Hello fiyat sütun seçin***

6. Merhaba denemeyi çalıştırın.

Şimdi kullanılan tooscore yeni otomobil veri toomake fiyat tahminleri olabilir eğitilen regresyon modeli sahibiz.

![Çalıştırdıktan sonra hello deneme aşağıdakine benzer görünmelidir][second-experiment-run]
<br/>
***Çalıştırdıktan sonra hello deneme aşağıdakine benzer görünmelidir***

## <a name="step-5-predict-new-automobile-prices"></a>5. Adım: Yeni otomobil fiyatlarını tahmin etme

Biz verilerimizi yüzde 75'ini kullanarak hello modeli eğittiğimize göre biz kullanabileceği tooscore hello diğer yüzde 25'i hello veri toosee ne kadar iyi verilerimizin.

1. Bulma ve hello sürükleyin [Score Model] [ score-model] modülü toohello deneme tuvaline. Merhaba Hello çıkışına bağlayın [Train Model] [ train-model] sol giriş bağlantı noktası modülü toohello [Score Model][score-model]. Merhaba test etme verileri çıkışına (sağ bağlantı noktası) hello bağlanmak [bölünmüş veri] [ split] modülü toohello sağ giriş bağlantı noktası [Score Model][score-model].

    !["Train Model" ve "Böl verileri" Hello "Score Model" modülü tooboth hello modülleri Bağlan][connect-score-model]
    <br/>
    ***"Train Model" ve "Böl verileri" Hello "Score Model" modülü tooboth hello modülleri Bağlan***

2. Merhaba denemeyi çalıştırın ve hello hello çıktısını görüntüleyin [Score Model] [ score-model] Modülü (Merhaba çıkış bağlantı noktasına tıklayın [Score Model] [ score-model] ve seçin **Görselleştirmek**). Fiyat için tahmin edilen değerler hello ve hello test verileri bilinen değerleri hello Hello çıkış gösterir.  

    ![Çıktı hello "Score Model" modülü][score-model-output]
    <br/>
    ***Çıktı hello "Score Model" modülü***

3. Son olarak, hello sonuçları hello kalitesini sınayın. Seçin ve hello sürükleyin [Evaluate Model] [ evaluate-model] modülü toohello tuvale denemek ve hello hello çıkışına bağlayın [Score Model] [ score-model] girişi sol modülü toohello [Evaluate Model][evaluate-model].

    > [!TIP]
    > Merhaba üzerinde iki giriş bağlantı noktaları olduğundan [Evaluate Model] [ evaluate-model] modülü kullanılan toocompare iki modeli yan yana olabileceğinden. Daha sonra başka bir algoritma toohello deneme ekleyin ve kullanmak [Evaluate Model] [ evaluate-model] toosee hangisinin daha iyi sonuçlar verir.

4. Merhaba denemeyi çalıştırın.

Merhaba tooview hello çıktısını [Evaluate Model] [ evaluate-model] modül hello çıkış bağlantı noktasına tıklayın ve ardından **Görselleştir**.

![Merhaba deneme değerlendirme sonuçları][evaluation-results]
<br/>
***Merhaba deneme değerlendirme sonuçları***

modelimiz için istatistikleri aşağıdaki hello gösterilmektedir:

- **Mutlak hata anlamına** (MAE): Merhaba mutlak hataların ortalaması (bir *hata* hello arasındaki farktır hello tahmin değeri ve hello gerçek değer).
- **Kök ortalama karesi alınmış hata** (RMSE): hello karekökünü hello hello test veri kümesinde yapılan tahminlerin karesi alınmış hataların ortalaması.
- **Göreli mutlak hata**: Merhaba gerçek değerler ve hello tüm gerçek değerlerin ortalaması arasındaki mutlak hataların göreli toohello mutlak fark ortalaması.
- **Göreli karesi alınmış hata**: karesi göreli toohello hello Ortalama kare hello gerçek değerler ve tüm gerçek değerlerin ortalaması hello arasındaki fark.
- **Katsayısı**: olarak da bilinen hello **R karesi alınmış değer**, bir model hello verileri ne kadar iyi uyumlu olduğunu gösteren istatistik ölçümleridir budur.

Her hello hata istatistikleri, daha küçük iyidir. Daha küçük bir değer hello tahminleri hello gerçek değerler daha yakından eşleştiğini gösterir. İçin **Coefficient of Determination**, hello yakın değeri tooone (1.0) hello daha iyi hello tahminleri'dır.

## <a name="final-experiment"></a>Son deneme

Merhaba son deneme aşağıdakine benzer görünmelidir:

![Merhaba son deneme][complete-linear-regression-experiment]
<br/>
***Merhaba son deneme***

## <a name="next-steps"></a>Sonraki adımlar

Merhaba ilk makine öğrenimi öğreticinizi tamamladığınıza ve denemenizi sahip olduğunuza tooimprove hello modeli devam et ve Tahmine dayalı web hizmeti olarak dağıtın.

- **Tootry tooimprove hello modeli yinelemek** -Örneğin, tahmin kullandığınız hello özelliklerini değiştirebilirsiniz. Veya hello hello özelliklerini değiştirebilirsiniz [doğrusal regresyon] [ linear-regression] algoritması veya tamamen farklı bir algoritma deneyebilirsiniz. Hatta birden çok makine öğrenimi algoritmaları tooyour denemesinin aynı anda eklemek ve ikisi hello kullanarak karşılaştırın [Evaluate Model] [ evaluate-model] modülü.
Bir örneği nasıl toocompare tek bir deneme birden çok modellerinde görmek için [karşılaştırmak Regresör](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) hello içinde [Cortana Intelligence Galerisi](https://gallery.cortanaintelligence.com).

    > [!TIP]
    > toocopy kullanım hello denemenizi herhangi bir yinelemesini **SAVE AS** hello altındaki hello sayfasının düğmesini. Tıklayarak denemenizin tüm hello yinelemelerini görebilirsiniz **ÇALIŞTIRMA GEÇMİŞİNİ GÖRÜNTÜLE** hello sayfanın hello sonundaki. Daha fazla ayrıntı için bkz. [Azure Machine Learning Studio'da deneme yinelemelerini yönetme][runhistory].

[runhistory]: machine-learning-manage-experiment-iterations.md

- **Merhaba modeli tahmine dayalı web hizmeti olarak dağıtma** - modelinizi ile memnun kaldığınızda yeni verileri kullanarak bir web hizmeti toobe toopredict otomobil fiyatlarını kullanılan olarak dağıtabilirsiniz. Daha fazla ayrıntı için bkz. [Bir Azure Machine Learning web hizmetini dağıtma][publish].

[publish]: machine-learning-publish-a-machine-learning-web-service.md

Daha fazla toolearn istiyorsunuz? Oluşturma, eğitim, Puanlama ve model dağıtma hello işleminin daha kapsamlı ve Ayrıntılı Kılavuzu için bkz: [Azure Machine Learning kullanarak Tahmine dayalı bir çözüm geliştirmek][walkthrough].

[walkthrough]: machine-learning-walkthrough-develop-predictive-solution.md

<!-- Images -->
[sign-in-to-studio]: ./media/machine-learning-create-experiment/sign-in-to-studio.png
[rename-experiment]: ./media/machine-learning-create-experiment/rename-experiment.png
[visualize-auto-data]:./media/machine-learning-create-experiment/visualize-auto-data.png
[select-visualize]: ./media/machine-learning-create-experiment/select-visualize.png
[showing-excluded-column]:./media/machine-learning-create-experiment/showing-excluded-column.png
[set-remove-entire-row]:./media/machine-learning-create-experiment/set-remove-entire-row.png
[early-experiment-run]:./media/machine-learning-create-experiment/early-experiment-run.png
[select-columns-to-include]:./media/machine-learning-create-experiment/select-columns-to-include.png
[second-experiment-run]:./media/machine-learning-create-experiment/second-experiment-run.png
[connect-score-model]:./media/machine-learning-create-experiment/connect-score-model.png
[evaluation-results]:./media/machine-learning-create-experiment/evaluation-results.png
[complete-linear-regression-experiment]:./media/machine-learning-create-experiment/complete-linear-regression-experiment.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[connect-train-model]:./media/machine-learning-create-experiment/connect-train-model.png
[select-price-column]:./media/machine-learning-create-experiment/select-price-column.png

[score-model-output]:./media/machine-learning-create-experiment/score-model-output.png

<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
