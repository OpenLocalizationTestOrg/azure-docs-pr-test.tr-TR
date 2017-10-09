---
title: "aaaGuide toohello Net # sinir ağları belirtimi dili | Microsoft Docs"
description: "Merhaba Net # sinir söz diziminin nasıl toocreate özel bir sinir ağı model Net # kullanarak Microsoft Azure ML içinde örnekleri ile birlikte belirtimi dili ağları"
services: machine-learning
documentationcenter: 
author: jeannt
manager: jhubbard
editor: cgronlun
ms.assetid: cfd1454b-47df-4745-b064-ce5f9b3be303
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeannt
ms.openlocfilehash: 3493247ecc39ca3a1382510ad520d7017159ff62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toonet-neural-network-specification-language-for-azure-machine-learning"></a>Azure Machine Learning için tooNet # sinir ağı belirtimi dili Kılavuzu
## <a name="overview"></a>Genel Bakış
NET # kullanılan toodefine sinir ağı mimarileri olan Microsoft tarafından geliştirilen bir dildir. Microsoft Azure Machine Learning sinir ağı modüllerde Net # kullanabilirsiniz.

<!-- This function doesn't currentlyappear in hello MicrosoftML documentation. If it is added in a future update, we can uncomment this text.

, or in hello `rxNeuralNetwork()` function in [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml). 

-->

Bu makalede, temel kavramları toodevelop özel bir sinir ağı gerekli öğreneceksiniz: 

* Sinir ağı gereksinimleri ve nasıl toodefine hello birincil bileşenleri
* Merhaba sözdizimi ve hello Net # belirtimi dili anahtar sözcüklerini
* Net # kullanılarak oluşturulan özel sinir ağları örnekleri 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="neural-network-basics"></a>Sinir ağı temelleri
Sinir ağı yapısı oluşan ***düğümleri*** içinde düzenlenmiş ***katmanları***ve ağırlıklı ***bağlantıları*** (veya ***kenarları***) arasında Merhaba düğümleri. Merhaba bağlantıları yön ve her bağlantısı olan bir ***kaynak*** düğümü ve ***hedef*** düğümü.  

Her ***trainable katman*** (gizli veya bir çıkış katmanı) bir veya daha fazla sahip ***bağlantı paketleri***. Bir bağlantı paket kaynak katmanı ve kaynak katman hello bağlantılarından belirtimini oluşur. Belirtilen paket paylaşımında tüm hello bağlantıları aynı hello ***kaynak katman*** ve aynı hello ***hedef katman***. NET #'ta bir bağlantı pakete ait toohello paketin hedef katmanı olarak kabul edilir.  

NET # girişleri eşlenen toohidden katmanlardır hello özelleştirmenize olanak sağlayan çeşitli bağlantı paketleri destekler ve eşlenen toohello çıkartır.   

Merhaba varsayılan ya da standart paket bir **tam paket**, hello alanındaki her bir düğümünde hangi kaynak hello hedef katman bağlı tooevery düğümünde katmanıdır.  

Ayrıca, Gelişmiş bağlantı paketleri dört tür aşağıdaki hello Net # destekler:  

* **Filtre paketleri**. Merhaba kullanıcı hello kaynak katman ve hello hedef katman düğümlerini hello konumları kullanarak bir koşul tanımlayabilirsiniz. Merhaba koşul True olduğunda düğümleri bağlanır.
* **Convolutional paketleri**. Merhaba kullanıcı düğümlerinin küçük Semt hello kaynak katmanda tanımlayabilirsiniz. Her hello hedef katmanda bağlı tooone Komşuları hello kaynak katmanda düğümlerinin düğümdür.
* **Paket havuzu** ve **yanıt normalleştirme paketleri**. Bunlar benzer tooconvolutional paketlerdir bu hello kullanıcı hello kaynak katmanda düğümlerinin küçük Semt tanımlar. Merhaba fark bu paketleri hello kenarları hello ağırlıkları trainable olmamasıdır. Bunun yerine, önceden tanımlanmış bir işlev uygulanan toohello kaynak düğüm değerleri toodetermine hello hedef düğüm değeri.  

NET # kullanarak bir sinir ağı toodefine hello yapısı, derin sinir ağları veya görüntü, ses veya video gibi verileri tooimprove öğrenmeyi bilinen rasgele boyutlarının convolutions gibi karmaşık yapıları olası toodefine kolaylaştırır.  

## <a name="supported-customizations"></a>Desteklenen özelleştirme
Merhaba mimarisi, Azure Machine Learning ile oluşturduğunuz sinir ağı modelinin Net # kullanarak kapsamlı bir şekilde özelleştirilebilir. Şunları yapabilirsiniz:  

* Gizli katmanları ve denetim hello düğüm sayısı her katmanı oluşturun.
* Katmanlar diğer bağlı toobe tooeach şeklini belirtin.
* Convolutions ve paket paylaşımı ağırlık gibi özel bağlantı yapılarını tanımlar.
* Başka bir etkinleştirme işlevleri belirtin.  

Merhaba belirtimi dili sözdizimi Ayrıntılar için bkz [yapısı belirtimi](#Structure-specifications).  

Tek yönlü toocomplex görevlerden öğrenme bazı ortak makine sinir ağları tanımlayan örnekler için bkz: [örnekleri](#Examples-of-Net#-usage).  

## <a name="general-requirements"></a>Genel gereksinimler
* Tam olarak bir çıkış katman, en az bir giriş katman ve sıfır veya daha çok gizli katmanları olmalıdır. 
* Her katman rasgele boyutları dikdörtgen bir dizi kavramsal olarak düzenlenmiş düğümler, sabit bir sayısına sahip. 
* Giriş Katmanlar ilişkili eğitilen parametresiz olmalıdır ve başlangıç noktası burada örnek verileri hello ağ girer temsil eder. 
* (Gizli ve çıkış Katmanlar hello) trainable Katmanlar ağırlıkları ve stratejimizdeki bilinen eğitilen parametreler ilişkilendirdiniz. 
* Merhaba kaynak ve hedef düğümleri ayrı katmanda olmalıdır. 
* Bağlantıları Çevrimsiz olmalıdır; diğer bir deyişle, geri toohello ilk kaynak düğüm önde gelen bağlantılar zinciri olamaz.
* Merhaba çıkış katman bir bağlantı paketin kaynak katmanı olamaz.  

## <a name="structure-specifications"></a>Yapı belirtimleri
Sinir ağı yapısı belirtimi üç bölümlerini oluşur: Merhaba **Sabit bildiriminde**, hello **katman bildirimi**, hello **bağlantı bildirimi**. Ayrıca vardır isteğe bağlı bir **paylaşmak bildirimi** bölümü. Merhaba bölümleri herhangi bir sırada belirtilebilir.  

## <a name="constant-declaration"></a>Sabit bildirimi
Sabit bildiriminde isteğe bağlıdır. Bu yol toodefine hello sinir ağı tanımı'nda başka bir yerde kullanılan değerleri sağlar. ardından bir eşittir işareti ve değer ifadesi bir tanımlayıcı Hello bildirimi deyimi oluşur.   

Örneğin, bir sabit deyiminden hello tanımlar **x**:  

    Const X = 28;  

toodefine iki veya daha fazla sabitleri aynı anda hello tanımlayıcı adları ve değerleri ayraç içine alın ve bunları noktalı virgülle ayırın. Örneğin:  

    Const { X = 28; Y = 4; }  

Her atama ifadesi Hello sağında bir tamsayı, gerçek bir sayı, bir Boole değeri (True veya False) veya bir matematik ifadesindeki olabilir. Örneğin:  

    Const { X = 17 * 2; Y = true; }  

## <a name="layer-declaration"></a>Katman bildirimi
Merhaba katman bildirimi gereklidir. Merhaba boyutunu ve kaynak öznitelikleri ve bağlantı paketleri de dahil olmak üzere hello katmanın tanımlar. bildirim deyimi başlatır (giriş, gizli veya çıktı) hello katmanın hello adı ile Merhaba, hello katman (pozitif tamsayılar tuple) hello boyutlara göre ardından. Örneğin:  

    input Data auto;
    hidden Hidden[5,20] from Data all;
    output Result[2] from Hidden all;  

* Merhaba hello boyutları hello hello katmandaki düğüm sayısını ürünüdür. Bu örnekte, hello katmanda 100 düğümleri olduğu anlamına gelir iki boyut [5,20] vardır.
* bir istisna dışında herhangi bir sırada Hello Katmanlar bildirilebilir: birden fazla giriş katman tanımlanmış olması durumunda, bunlar bildirilen hello hello giriş verisi özelliklerinde hello sırasını eşleşmesi gerekir.  

Merhaba katmandaki düğüm sayısını olması toospecify belirlenen otomatik olarak kullan hello **otomatik** anahtar sözcüğü. Merhaba **otomatik** anahtar sözcüğü hello katman bağlı olarak farklı efektler vardır:  

* Bir giriş katman bildiriminde hello düğüm sayısını hello hello giriş verisi özelliklerinde sayısıdır.
* Gizli Katman bildiriminde hello sayısı düğümler için hello parametre değeri tarafından belirtilen hello sayısıdır **gizli düğüm sayısını**. 
* Bir çıkış katman bildiriminde hello düğüm sayısını iki sınıflı Sınıflandırma, regresyon ve çıktı düğüm için çok sınıflı sınıflandırma eşit toohello sayısı için 1 için 2'dir.   

Örneğin, hello aşağıdaki ağ tanımını otomatik olarak belirlenen tüm katmanlar toobe hello boyutunu sağlar:  

    input Data auto;
    hidden Hidden auto from Data all;
    output Result auto from Hidden all;  


Bir katman bildirimi trainable bir katman için (gizli veya çıkış katmanlarda hello) isteğe bağlı olarak çok varsayılan olarak (bir etkinleştirme işlevi de denir), hello çıkış işlevi içerebilir**sigmoid** sınıflandırma modelleri ve **doğrusal** regresyon modelleri için. (Merhaba varsayılan kullansanız bile, açıkça hello etkinleştirme işlevi, daha anlaşılır olması için isterseniz durumunu.)

Merhaba aşağıdaki çıkış işlevleri desteklenir:  

* sigmoid
* Doğrusal
* softmax
* rlinear
* Kare
* Sqrt
* srlinear
* Abs
* TANH 
* brlinear  

Örneğin, bildiriminin hello hello kullanır **softmax** işlevi:  

    output Result [100] softmax from Hidden all;  

## <a name="connection-declaration"></a>Bağlantı bildirimi
Merhaba trainable katman hemen tanımladıktan sonra tanımladığınız hello katmanlar arasında bağlantı bildirmeniz gerekir. Merhaba bağlantı paket bildirimi hello anahtar sözcüğüyle başlar **gelen**hello paketin kaynak katman ve hello tür bağlantı paket toocreate hello adını takiben.   

Şu anda beş bağlantı paket türleri desteklenir:  

* **Tam** hello anahtar sözcüğüyle belirtilen paket, **tüm**
* **Filtre** hello anahtar sözcüğüyle belirtilen paket, **burada**takip eden bir koşul ifadesi
* **Convolutional** hello anahtar sözcüğüyle belirtilen paket, **convolve**, ardından hello evrişim öznitelikleri
* **Havuzu** hello anahtar tarafından belirtilen paket, **en büyük havuz** veya **havuzu anlama**
* **Yanıt normalleştirme** hello anahtar sözcüğüyle belirtilen paket, **yanıt norm**      

## <a name="full-bundles"></a>Tam paketleri
Tam bağlantı paket hello kaynak katman tooeach düğüm hello hedef katmanda her düğümden bir bağlantı içerir. Merhaba varsayılan ağ bağlantısı türü budur.  

## <a name="filtered-bundles"></a>Filtrelenmiş paketler
Filtrelenmiş bağlantıda paket belirtimi, C# lambda ifadesi gibi koşul, ifade edilen sözdizimsel olarak, çok içerir. Merhaba aşağıdaki örnekte iki filtrelenmiş paketler tanımlar:  

    input Pixels [10, 20];
    hidden ByRow[10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol[5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;  

* İçin hello koşulunda *ByRow*, **s** dizin hello dikdörtgen hello giriş katmanın düğümleri diziye temsil eden bir parametre *piksel*, ve **d**  dizin hello gizli katmanın düğümlerinin hello diziye temsil eden bir parametre *ByRow*. Merhaba hem de türü **s** ve **d** iki uzunluğu tamsayıların bir tanımlama grubu değil. Kavramsal olarak, **s** aralıkları ile tamsayıların tüm çiftleri üzerinden *0 < = s [0] < 10* ve *0 < = s[1] < 20*, ve **d**  ile tamsayılar, tüm çiftlerini aralıkları *0 < = [0] d < 10* ve *0 < = d[1] < 12*. 
* Merhaba sağ tarafında hello koşul ifadesi, bir koşulu yoktur. Bu örnekte, her değeri için **s** ve **d** hello koşul doğru ise şekilde hello kaynak katman düğümü toohello hedef katman düğümünden bir sınır yoktur. Bu nedenle, bu filtre ifadesi, o hello paket bağlantı tarafından tanımlanan hello düğümünden içerip içermediğini belirtir **s** toohello düğümü tarafından tanımlanan **d** s [0] [0] eşit tood olduğu tüm durumlarda.  

İsteğe bağlı olarak, ağırlıkları filtre uygulanmış bir paket için bir dizi belirtebilirsiniz. Merhaba hello için değer **ağırlıkları** özniteliği, kayan nokta değerlerine hello paket tarafından tanımlanan bağlantı hello sayısı ile eşleşen bir uzunluğa sahip bir tanımlama grubu olmalıdır. Varsayılan olarak, ağırlıkları rastgele üretilir.  

Ağırlık değerleri hello hedef düğüm dizine göre gruplandırılır. Merhaba ilk hedef düğüm bağlıysa, diğer bir deyişle, kaynak düğüm sürdü ilk hello *K* hello öğeleri **ağırlıkları** tanımlama grubu olan hello ağırlıkları hello ilk hedef düğüm, kaynak dizin sırası için. Merhaba aynı hedef düğümleri kalan hello için geçerlidir.  

Bu olası toospecify ağırlıkları doğrudan sabit değerleri gösterir. Örneğin, hello ağırlıkları önceden öğrenilen varsa, bunları bu söz dizimini kullanarak sabitleri belirtebilirsiniz:

    const Weights_1 = [0.0188045055, 0.130500451, ...]


## <a name="convolutional-bundles"></a>Convolutional paketleri
Hello eğitim verileri homojen bir yapıya sahip olduğunda, convolutional bağlantıları yaygın olarak kullanılan toolearn üst düzey hello verilerin özellikleridir. Örneğin, ses veya video veriler, uzamsal veya zamana bağlı boyut görüntüde oldukça Tekdüzen olabilir.  

Convolutional paketleri uygulamadığınız dikdörtgen **tekrar** hello boyutları aracılığıyla slid. Esas olarak, her çekirdek yerel Semt başvurulan tooas uygulanan ağırlıkları kümesini tanımlayan **çekirdek uygulamaları**. Her bir çekirdek uygulama başvurulan tooas hello olduğu hello kaynak katman tooa düğümünde karşılık gelen **merkezi düğümü**. bir çekirdek Hello ağırlıkları birçok bağlantıları arasında paylaşılır. Convolutional bir pakette her çekirdek dikdörtgen ve tüm çekirdek uygulamalar aynı hello boyutu.  

Convolutional paketleri öznitelikleri aşağıdaki hello destekler:

**InputShape** hello boyut bu convolutional paket hello amacıyla hello kaynak katmanın tanımlar. Merhaba değeri pozitif tamsayılar tanımlama grubu olmalıdır. Merhaba ürün hello tamsayıların hello hello kaynak katmandaki düğüm sayısını eşit olmalıdır, ancak Aksi halde, hello kaynak katmanı için bildirilen toomatch hello boyut gerekmez. Bu tanımlama grubu Hello uzunluğu hale hello **parametre** hello convolutional paket için değer. (Genellikle parametre toohello sayıda bağımsız değişken veya işlev sürebilir işlenenler anlamına gelir.)  

toodefine hello şekli ve hello çekirdekleri konumlarını kullanın hello öznitelikleri **KernelShape**, **STRIDE**, **doldurma**, **LowerPad**, ve **UpperPad**:   

* **KernelShape**: Merhaba convolutional paketi için her çekirdek (gerekli) tanımlar hello işlenemez. Merhaba değeri pozitif tamsayılar hello paket hello kapsamalıdır eşittir bir uzunluğa sahip bir tanımlama grubu olmalıdır. Bu tanımlama grubu alanının her bileşeni hello karşılık gelen bileşeninin büyük olmaması **InputShape**. 
* **STRIDE**: (isteğe bağlı) tanımlar hello hello uzaklık hello merkezi düğümü arasında hello Evrişim (tek bir adımda boyutu) her boyut için adım boyutlarını kayan. Merhaba değeri pozitif tamsayılar hello paket hello kapsamalıdır olan uzunluğa sahip bir tanımlama grubu olmalıdır. Bu tanımlama grubu alanının her bileşeni hello karşılık gelen bileşeninin büyük olmaması **KernelShape**. tüm bileşenleri eşit tooone ile tanımlama grubu Hello varsayılan değerdir. 
* **Paylaşımı**: hello evrişim her boyut için paylaşımı (isteğe bağlı) tanımlar hello ağırlık. Merhaba değeri tek bir Boole değeri veya Boolean değeri hello paket hello kapsamalıdır olan uzunluğa sahip bir tanımlama grubu olabilir. Genişletilmiş toobe tüm bileşenlerle hello doğru uzunlukta bir tanımlama grubu tek bir Boole değeri olan eşit toohello belirtilen değeri. Tüm True değeri içeren bir tanımlama grubu Hello varsayılan değerdir. 
* **MapCount**: özelliği (isteğe bağlı) tanımlar hello sayısı hello convolutional paketi eşler. Merhaba değeri tek bir pozitif tamsayı veya bir tanımlama grubu pozitif tamsayılar hello paket hello kapsamalıdır olan uzunluğa sahip olabilir. Tek bir tamsayı değeri toobe genişletilmiş bir tanımlama grubu hello ilk bileşenleri eşit toohello ile Merhaba doğru uzunluğu belirtilen değeri ve tüm hello kalan bileşenleri eşit tooone. Merhaba varsayılan değer biridir. Özellik eşlemeleri Hello toplam sayısı, hello tuple hello bileşenlerinin hello üründür. Merhaba bu toplam sayısı hello bileşenlerinde Finansman hello özellik eşlemesi değerleri hello hedef düğümleri nasıl gruplandırılacağını belirler. 
* **Ağırlıkları**: (isteğe bağlı) tanımlar hello ilk ağırlıkları hello paket için. Merhaba değeri kayan nokta değerleri, bu makalenin sonraki bölümlerinde tanımlanan hello sayısının tekrar kez hello ağırlıkları çekirdek başına olan uzunluğa sahip bir tanımlama grubu olmalıdır. Merhaba varsayılan ağırlıkları rastgele üretilir.  

Doldurma, birbirini dışlayan olan hello özellikleri denetleyen özellikler iki kümesi vardır:

* **Doldurma**: (isteğe bağlı) belirler olup hello giriş doldurulan kullanarak bir **varsayılan doldurma düzenini**. Merhaba değeri, tek bir Boole değeri veya Boolean değeri hello paket hello kapsamalıdır olan uzunluğa sahip bir tanımlama grubu olabilir. Genişletilmiş toobe tüm bileşenlerle hello doğru uzunlukta bir tanımlama grubu tek bir Boole değeri olan eşit toohello belirtilen değeri. Bir boyut için Hello değeri True ise, sağlayacak şekilde hello ilk ve son düğümleri hello ilk ve son tekrar bu boyuttaki merkezi düğümleri hello olan hello kaynak mantıksal olarak sıfır değerli hücrelere toosupport ek çekirdek uygulamalarla o boyutundaki sıfır eklenir Bu boyutta hello kaynak katmanda. Bu nedenle, her boyutta "kukla" düğüm hello sayısı: otomatik olarak toofit tam olarak belirlenen *(InputShape [d] - 1) / [d] STRIDE + 1* tekrar doldurulan hello kaynak katmana. Bir boyut için Hello değeri False ise, böylece hello sol çıkışı her tarafında düğüm sayısını tekrar tanımlanan hello hello aynı (tooa farkını 1). Bu özniteliğin Hello varsayılan değeri tüm bileşenleri eşit tooFalse ile tanımlama grubu var.
* **UpperPad** ve **LowerPad**: (isteğe bağlı) sağlama doldurma toouse hello miktarını üzerinde daha fazla denetim. **Önemli:** bu öznitelikler bulunuyorsa ve yalnızca hello tanımlanabilir **doldurma** özelliği yukarıdaki ***değil*** tanımlanmış. Merhaba değerleri tamsayı değerli diziler hello paket hello kapsamalıdır olan uzunluklarına sahip olmalıdır. Bu öznitelikler belirtildiğinde, "kukla" düğümleri toohello alt eklenir ve katman hello her boyut üst ucunun giriş. Merhaba düğüm sayısını eklenen toohello alt ve her boyut üst sona eriyor belirlenir **LowerPad**[i] ve **UpperPad**[i] sırasıyla. tekrar "gerçek" yalnızca çok düğümleri ve değil çok "kukla" düğümleri hello koşullar aşağıdaki karşılık geldiğinden emin tooensure karşılanmalıdır:
  * Her bir bileşeninin **LowerPad** [d] KernelShape değerinden kesinlikle küçük olmalıdır / 2. 
  * Her bir bileşeninin **UpperPad** KernelShape [d] ' büyük olmalıdır / 2. 
  * Merhaba varsayılan bu özniteliklerin tüm bileşenleri eşit too0 ile tanımlama grubu değerdir. 

Merhaba ayarı **doldurma** = true olarak kadar doldurma tookeep hello hello çekirdek "Merkezi" hello "gerçek" giriş içinde gerektiğinde sağlar. Bu hello çıkış boyutu bilgi işlem için bir bit hello matematik değiştirir. Genellikle, hello çıktı boyutu *D* olarak hesaplanan *D = (ı - K) / S + 1*, burada *ı* hello giriş boyutu, *K* hello çekirdek boyutu, *S* hello STRIDE olduğu ve  */*  tamsayı bölme (sıfıra doğru yuvarlar) değil. UpperPad ayarlarsanız = [1, 1] hello giriş boyutu *ı* 29 etkin olduğunu ve bu nedenle *D = (29-5) / 2 + 1 = 13*. Ancak, ne zaman **doldurma** = true, aslında *ı* tarafından indirgenmesine *K - 1*; bu nedenle *D = ((28 + 4) - 5) / 2 + 1 = 27 / 2 + 1 = 13 + 1 = 14*. İçin değerler belirterek **UpperPad** ve **LowerPad** IF ayarladığınız doldurma hello üzerinde daha fazla denetim elde **doldurma** = true.

Convolutional ağları ve bunların uygulamaları hakkında daha fazla bilgi için bu makalelere bakın:  

* [http://deeplearning.NET/Tutorial/lenet.HTML](http://deeplearning.net/tutorial/lenet.html)
* [http://Research.microsoft.com/pubs/68920/icdar03.PDF](http://research.microsoft.com/pubs/68920/icdar03.pdf) 
* [http://People.csail.mit.edu/jvb/Papers/cnn_tutorial.PDF](http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf)  

## <a name="pooling-bundles"></a>Paket havuzu
A **paket havuzu** geometri benzer tooconvolutional bağlantı uygulanır ancak önceden tanımlanmış işlevleri toosource düğümü değerleri tooderive hello hedef düğüm değeri kullanır. Bu nedenle, havuzu paketleri trainable durum yok (ağırlıkları veya stratejimizdeki) sahip. Tüm hello dışında convolutional öznitelikleri paketleri destek havuzu **paylaşım**, **MapCount**, ve **ağırlıkları**.  

Genellikle, bitişik havuzu birimler tarafından özetlenen hello tekrar çakışmaz. STRIDE [d] her boyutundaki eşit tooKernelShape [d] ise, elde edilen hello katman hangi convolutional sinir ağlarda yaygın olarak kullanılan hello geleneksel yerel havuzu oluşturma, katmanıdır. Her hedef düğüm hello maksimum ya da kendi çekirdek hello kaynak katmanda hello etkinliklerini hello ortalaması hesaplar.  

Aşağıdaki örnek hello havuzu paket gösterilmektedir: 

    hidden P1 [5, 12, 12]
      from C1 max pool {
        InputShape  = [ 5, 24, 24];
        KernelShape = [ 1,  2,  2];
        Stride      = [ 1,  2,  2];
      }  

* Merhaba paket Hello kapsamalıdır: 3 (Merhaba hello diziler uzunluğu **InputShape**, **KernelShape**, ve **STRIDE**). 
* Merhaba hello kaynak katmandaki düğüm sayısı: *5 * 24 * 24 = 2880*. 
* Bunun nedeni geleneksel yerel havuzu katman, **KernelShape** ve **STRIDE** eşit. 
* Merhaba hello hedef katmandaki düğüm sayısı: *5 * 12 * 12 = 1440*.  

Havuzu katmanları hakkında daha fazla bilgi için bu makalelere bakın:  

* [http://www.cs.Toronto.edu/~hinton/absps/imagenet.PDF](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf) (Bölüm 3.4)
* [http://cs.nyu.edu/~koray/publis/lecun-iscas-10.PDF](http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf) 
* [http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.PDF](http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf)

## <a name="response-normalization-bundles"></a>Yanıt normalleştirme paketleri
**Yanıt normalleştirme** ilk Geoffrey Hinton tarafından sunulan bir yerel normalleştirme düzenidir hello yazıdaki et al [ImageNet Classiﬁcation Convolutional derin sinir ağları ile](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf). Yanıt normalleştirme sinir ağ içinde kullanılan tooaid Genelleştirme ' dir. Çok yüksek etkinleştirme düzeyinde bir neuron tetikleme, yerel yanıt normalleştirme katman hello etkinleştirme neurons çevreleyen hello düzeyini gizler. Bu üç parametre kullanılarak yapılır (***α***, ***β***, ve ***k***) ve bir convolutional yapısı (veya Komşuları Şekil). Merhaba hedef katmanda her neuron ***y*** tooa neuron karşılık gelen ***x*** hello kaynak katmanda. Merhaba etkinleştirme düzeyini ***y*** formülü aşağıdaki hello tarafından verilen nerede ***f*** bir neuron hello etkinleştirme düzeyi ve ***Nx*** hello çekirdek (veya hello içeren hello kümesidir Merhaba Komşuları neurons ***x***), convolutional yapı izlenerek hello tarafından tanımlanan:  

![][1]  

Yanıt normalleştirme paketleri destek dışındaki tüm hello convolutional öznitelikleri **paylaşım**, **MapCount**, ve **ağırlıkları**.  

* Merhaba çekirdek hello neurons içeriyorsa olarak aynı eşleme ***x***, hello normalleştirme düzenidir başvurulan tooas **aynı eşleme normalleştirme**. toodefine, aynı eşleme normalleştirme hello ilk koordinat içinde **InputShape** başlangıç değeri 1 olmalıdır.
* Merhaba çekirdek hello neurons içeriyorsa uzamsal aynı konumda ***x***, ancak hello neurons diğer eşlemeleri, hello normalleştirme düzeni çağrılır **normalleştirme'çapraz eşlemeleri**. Yanıt normalleştirme bu tür yanal inhibition farklı eşlemeleri hesaplanan neuron çıktılar arasında büyük etkinleştirme düzeyleri için rekabet oluşturma gerçek neurons içinde bulunan hello türüne göre esin biçimi uygular. normalleştirme arasında toodefine eşler, hello ilk koordinat birden büyük ve haritalar hello sayısından daha büyük bir tamsayı olmalıdır ve hello koordinatları hello kalan hello değeri 1 olmalıdır.  

Önceden tanımlanmış işlevi toosource düğümü değerleri toodetermine hello hedef düğüm değeri yanıt normalleştirme paketleri geçerli olduğundan, bunlar trainable durum yok (ağırlıkları veya stratejimizdeki) sahip.   

**Uyarı**: hello hedef katman hello düğümler hello tekrar merkezi düğümleri hello olan tooneurons karşılık gelir. Örneğin, KernelShape [d] tek, ise, *KernelShape [d] / 2* toohello merkezi çekirdek düğüm karşılık gelir. Varsa *KernelShape [d]* hello merkezi düğümü olduğu anda olsa bile, *KernelShape [d] / 2-1*. Bu nedenle, varsa **doldurma**[d] değeri: False, hello ilk ve son hello *KernelShape [d] / 2* düğümleri hello hedef katmanda ilgili düğümleri gerekmez. tooavoid bu durumu tanımlamak **doldurma** olarak [true, true,..., true].  

Ayrıca toohello dört öznitelikleri daha önce yanıt normalleştirme paketleri de öznitelikleri aşağıdaki Destek hello açıklanmaktadır:  

* **Alpha**: (gerekli) belirtir çok karşılık gelen bir kayan nokta değer***α*** hello önceki formülünde. 
* **Beta**: (gerekli) belirtir çok karşılık gelen bir kayan nokta değer***β*** hello önceki formülünde. 
* **Uzaklık**: (isteğe bağlı) belirtir çok karşılık gelen bir kayan nokta değer***k*** hello önceki formülünde. Too1 varsayar.  

Merhaba aşağıdaki örnekte bu öznitelikler kullanarak bir yanıt normalleştirme paketini tanımlar:  

    hidden RN1 [5, 10, 10]
      from P1 response norm {
        InputShape  = [ 5, 12, 12];
        KernelShape = [ 1,  3,  3];
        Alpha = 0.001;
        Beta = 0.75;
      }  

* Merhaba kaynak katmanın her 12 x 12, 1440 düğümler toplamda aof boyutla beş eşlemeleri içerir. 
* Merhaba değerini **KernelShape** bu hello Komşuları 3 x 3 dikdörtgen olduğu aynı bir harita normalleştirme katman olduğunu gösterir. 
* Merhaba varsayılan değerini **doldurma** false, böylece hello hedef katman her boyut yalnızca 10 düğüm yok. Doldurma eklemek hello kaynak katman tooevery düğümünde karşılık gelen hello hedef katman bir düğümünden tooinclude = [true, true, true]; ve çok RN1 hello boyutunu değiştirme [5, 12, 12].  

## <a name="share-declaration"></a>Paylaşım bildirimi
NET # isteğe bağlı olarak paylaşılan ağırlıklara sahip birden çok paket tanımlama destekler. kendi yapıları olan Merhaba, aynı herhangi iki paket hello ağırlıkları paylaşılabilir. sözdizimi aşağıdaki hello paylaşılan ağırlıklara sahip paketleri tanımlar:  

    share-declaration:
        share    {    layer-list    }
        share    {    bundle-list    }
       share    {    bias-list    }

    layer-list:
        layer-name    ,    layer-name
        layer-list    ,    layer-name

    bundle-list:
       bundle-spec    ,    bundle-spec
        bundle-list    ,    bundle-spec

    bundle-spec:
       layer-name    =>     layer-name

    bias-list:
        bias-spec    ,    bias-spec
        bias-list    ,    bias-spec

    bias-spec:
        1    =>    layer-name

    layer-name:
        identifier  

Örneğin, hello aşağıdaki paylaşım bildirimi ağırlıkları ve stratejimizdeki paylaşılan olduğunu gösteren hello katman adlarını belirtir:  

    Const {
      InputSize = 37;
      HiddenSize = 50;
    }
    input {
      Data1 [InputSize];
      Data2 [InputSize];
    }
    hidden {
      H1 [HiddenSize] from Data1 all;
      H2 [HiddenSize] from Data2 all;
    }
    output Result [2] {
      from H1 all;
      from H2 all;
    }
    share { H1, H2 } // share both weights and biases  

* Merhaba giriş özellikleri iki eşit boyutta giriş katmanlara bölümlenir. 
* Gizli hello Katmanlar sonra hello iki giriş katmanlardaki daha yüksek düzey özelliklerinin işlem. 
* Merhaba paylaşımı-bildirim belirtir *H1* ve *H2* hello hesaplanan kendi ilgili girişler aynı biçimde.  

Alternatif olarak, bu iki ayrı paylaşımı-bildirimlerle gibi belirtilebilir:  

    share { Data1 => H1, Data2 => H2 } // share weights  

<!-- -->

    share { 1 => H1, 1 => H2 } // share biases  

Yalnızca tek bir paket hello katmanları içerdiğinde hello kısa formu kullanabilirsiniz. Yalnızca hello ilgili yapısı aynı boyut, aynı convolutional geometri vb. hello sahip oldukları anlamına gelir, aynı genel olarak, paylaşımı mümkün olur.  

## <a name="examples-of-net-usage"></a>Net # kullanım örnekleri
Bu bölümde nasıl Net # kullanabileceğiniz bazı örnekler gizli tooadd katmanlar, gizli katmanları diğer katmanları ile etkileşim kurmanızı ve convolutional ağlar oluşturmak hello şekilde tanımlayın.   

### <a name="define-a-simple-custom-neural-network-hello-world-example"></a>Basit bir özel sinir ağı tanımlar: "Hello World" örnek
Bu basit örnekte, nasıl toocreate sinir bir ağ tek bir gizli katmana sahip modeli gösterilmektedir.  

    input Data auto;
    hidden H [200] from Data all;
    output Out [10] sigmoid from H all;  

Merhaba örneği aşağıdaki gibi bazı temel komutları gösterir:  

* Merhaba ilk satırı tanımlar hello giriş katman (adlı *veri*). Merhaba kullandığınızda **otomatik** anahtar sözcüğü, hello sinir ağı hello giriş örneklerde otomatik olarak tüm özellik sütunları içerir. 
* Merhaba ikinci satır hello gizli katman oluşturur. Merhaba adı *H* 200 düğüme sahip toohello Gizli Katman atanır. Bu katman tamamen bağlantılı toohello giriş katmanıdır.
* Merhaba üçüncü satır hello çıkış katman tanımlar (adlı *O*), 10 çıkış düğümlerini içerir. Merhaba sinir ağı için sınıflandırma kullanılırsa, bir çıktı düğüm başına sınıfı yok. anahtar sözcüğü hello **sigmoid** hello çıkış işlevi uygulanan toohello çıkış katman olduğunu gösterir.   

### <a name="define-multiple-hidden-layers-computer-vision-example"></a>Birden çok gizli katmanları tanımlayın: bilgisayar görme örneği
Merhaba aşağıdaki örnekte gösterilmiştir nasıl toodefine birden çok özel gizli katmanlarıyla biraz daha karmaşık bir sinir ağı.  

    // Define hello input layers 
    input Pixels [10, 20];
    input MetaData [7];

    // Define hello first two hidden layers, using data only from hello Pixels input
    hidden ByRow [10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol [5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;

    // Define hello third hidden layer, which uses as source hello hidden layers ByRow and ByCol
    hidden Gather [100] 
    {
      from ByRow all;
      from ByCol all;
    }

    // Define hello output layer and its sources
    output Result [10]  
    {
      from Gather all;
      from MetaData all;
    }  

Bu örnek hello sinir ağları belirtimi dil çeşitli özellikleri gösterir:  

* Merhaba yapısının iki giriş katman *piksel* ve *meta verileri*.
* Merhaba *piksel* katmanıdır hedef katmanlarıyla iki bağlantı paketleri için bir kaynak katman *ByRow* ve *ByCol*.
* Merhaba katmanları *toplamak* ve *sonuç* birden çok bağlantı paket hedef katmanlarda olan.
* Hello çıkış katman *sonuç*, bir hedef katmandaki iki bağlantı paketleri; biriyle hello ikinci düzey gizli (toplama) hedef katmanı olarak ve diğer hello giriş katman (meta verileri) ile bir hedef katman olarak hello.
* Gizli katmanları hello *ByRow* ve *ByCol*, filtrelenmiş bağlantı koşullu ifadeler kullanarak belirtin. Daha hassas bir şekilde hello düğümünde *ByRow* konumundaki [x, y] bağlı toohello düğümler *piksel* hello ilk dizin koordinat eşit toohello düğümün ilk koordinat, x sahip. Benzer şekilde, hello düğümünde *[x, y] konumundaki ByCol bağlı toohello düğümler _Pixels içinde* hello ikinci dizin koordinat hello düğümün ikinci koordinat biri içinde sahip y.  

### <a name="define-a-convolutional-network-for-multiclass-classification-digit-recognition-example"></a>Çok sınıflı sınıflandırma convolutional ağ tanımlayın: rakam tanıma örneği
Ağ aşağıdaki hello Hello tanımını tasarlanmış toorecognize sayıdır ve sinir ağı özelleştirmek için Gelişmiş bazı teknikleri göstermektedir.  

    input Image [29, 29];
    hidden Conv1 [5, 13, 13] from Image convolve 
    {
       InputShape  = [29, 29];
       KernelShape = [ 5,  5];
       Stride      = [ 2,  2];
       MapCount    = 5;
    }
    hidden Conv2 [50, 5, 5]
    from Conv1 convolve 
    {
       InputShape  = [ 5, 13, 13];
       KernelShape = [ 1,  5,  5];
       Stride      = [ 1,  2,  2];
       Sharing     = [false, true, true];
       MapCount    = 10;
    }
    hidden Hid3 [100] from Conv2 all;
    output Digit [10] from Hid3 all;  


* Merhaba yapısının tek bir giriş katman *görüntü*.
* anahtar sözcüğü hello **convolve** hello Katmanlar adlı gösterir *Conv1* ve *Conv2* convolutional katmanlardır. Bu katman bildirimleri her hello evrişim özniteliklerin bir listesi tarafından izlenir.
* Hello net üçüncü Gizli katmandaki *Hid3*, tam olarak olduğu toohello ikinci gizli katman, bağlı *Conv2*.
* Merhaba çıkış katman *basamaklı*, bağlı tek toohello üçüncü gizli katmanın, *Hid3*. anahtar sözcüğü hello **tüm** hello çıkış katman tam olarak bağlanmış çok gösterir*Hid3*.
* Merhaba hello evrişim kapsamalıdır üç olduğu (Merhaba hello diziler uzunluğu **InputShape**, **KernelShape**, **STRIDE**, ve **paylaşım**). 
* Çekirdek başına ağırlıkları Hello sayısıdır *1 + **KernelShape**\[0] * **KernelShape**\[1] * **KernelShape** \[2] = 1 + 1 * 5 * 5 = 26 oluşturun. Veya 26 * 50 = 1300*.
* Her Gizli katmandaki hello düğümleri gibi hesaplayabilirsiniz:
  * **NodeCount**\[0] = (5 - 1) / 1 + 1 = 5.
  * **NodeCount**\[= 1] (13-5) / 2 + 1 = 5. 
  * **NodeCount**\[2] (13-5) = / 2 + 1 = 5. 
* Merhaba toplam düğümlerin sayısının hello boyut bildirilen hello kullanılarak hesaplanabilir katman, [50, 5, 5], şu şekilde:  ***MapCount** * **NodeCount** \[ 0] * **NodeCount**\[1] * **NodeCount**\[= 2] 10 * 5 * 5 * 5*
* Çünkü **paylaşım**[d] değeri: False yalnızca *d 0 ==*, tekrar hello sayısıdır  ***MapCount** * **NodeCount** \[0] = 10 * 5 = 50*. 

## <a name="acknowledgements"></a>Katkıda Bulunanlar
Merhaba sinir ağları hello mimarisini özelleştirmek için Net # dili Microsoft'taki Shon Katzenberger (Mimarı, Machine Learning) ve Alexey Kamenev (yazılım mühendisi, Microsoft Research) tarafından geliştirilmiştir. Machine learning projeleri ve görüntü algılama tootext analytics'ten arasında değişen uygulamalar için dahili olarak kullanılır. Daha fazla bilgi için bkz: [sinir ağ Azure ML - giriş tooNet # içinde](http://blogs.technet.com/b/machinelearning/archive/2015/02/16/neural-nets-in-azure-ml-introduction-to-net.aspx)

[1]:./media/machine-learning-azure-ml-netsharp-reference-guide/formula_large.gif

