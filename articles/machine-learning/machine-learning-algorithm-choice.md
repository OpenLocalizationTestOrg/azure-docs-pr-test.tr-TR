---
title: "aaaHow toochoose machine learning algoritmaları | Microsoft Docs"
description: "Nasıl toochoose Azure Machine Learning algoritmaları kümelemesindeki denetimli ve Denetimsiz öğrenme için sınıflandırma veya regresyon denemelerini."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: a3b23d7f-f083-49c4-b6b1-3911cd69f1b4
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/25/2017
ms.author: garye
ms.openlocfilehash: 367b2278acc2435f27f9d24ead8199db58aca283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-algorithms-for-microsoft-azure-machine-learning"></a>Nasıl Microsoft Azure Machine Learning için toochoose algoritmaları
Merhaba yanıt toohello Soru "hangi makine kullanması gereken öğrenme algoritmasının?" her zaman "Bu bağlıdır." olur Merhaba boyutu, kalite ve hello veri yapısını bağlıdır. İstediğiniz üzerinde bağlıdır toodo hello yanıt. Bu, nasıl hello matematik hello algoritmasının yönergeler için kullanmakta olduğunuz hello bilgisayar içine çevrilmiştir üzerinde bağlıdır. Ve bağlı olduğu üzerinde ne kadar süre sahip. Hatta en deneyimli hello veri bilimcilerine algoritmayı en iyi denemeden önce gerçekleştirecek bildiremez.

## <a name="hello-machine-learning-algorithm-cheat-sheet"></a>Merhaba makine öğrenme algoritmasını kopya sayfası
Merhaba **Microsoft Azure Machine Learning algoritmasını kopya sayfası** hello sağ seçtiğiniz yardımcı makine öğrenme algoritmasını algoritmalarının hello Microsoft Azure Machine Learning'de kitaplığından Tahmine dayalı analiz çözümleriniz için.
Bu makalede nasıl anlatılmaktadır toouse onu.

> [!NOTE]
> toodownload hello kopya sayfası ve bu makale boyunca izleyin Git çok[makine için Microsoft Azure Machine Learning Studio'da algoritması bilgi sayfası öğrenme](machine-learning-algorithm-cheat-sheet.md).
> 
> 

Bu kopya sayfası çok belirli bir hedef kitle göz önünde vardır: toochoose Azure Machine Learning Studio'da bir algoritma toostart ile çalışırken başına veri Bilimcisi lisans Öğrencisi düzeyi machine learning ile. Bazı Genelleştirme ve oversimplifications kolaylaştırır, ancak güvenli bir yönde işaret eden anlamına gelir. Ayrıca, çok sayıda burada listelenmeyen algoritmaları olduğu anlamına gelir. Azure Machine Learning tooencompass kullanılabilir yöntemleri daha eksiksiz bir kümesini büyüdükçe, bunları ekleyeceğiz.

Bu, derlenmiş geri bildirim ve çok sayıda veri bilimcilerine ve makine öğrenme uzmanlar ipuçlarından önerilerdir. Biz her şeyi kabul oldu, ancak ı tooharmonize kaba anlaşma bizim görüşlerini çalıştınız. "Bağlı olduğu ile..." çözünürlüğünün hello bilgilerinin çoğunu başlayın

### <a name="how-toouse-hello-cheat-sheet"></a>Nasıl toouse hello kopya sayfası
Merhaba yolu ve algoritma etiketleri hello grafik okuma "için  *&lt;yol etiketinin&gt;*, kullanın  *&lt;algoritması&gt;*." Örneğin, "için *hızı*, kullanın *iki Lojistik regresyon sınıf*." Bazen birden fazla dalı geçerlidir.
Bazen bunları bir mükemmel yok. Bunlar hedeflenen toobe Flash kural önerileri dileriz, bu nedenle tam olan bu konuda endişelenmeyin.
Bu hello şekilde hello en iyi algoritmasıdır tootry bulmak yalnızca emin ı açıklandı ile çeşitli veri bilimcilerine denirse bunların tümünün.

Merhaba bir örnek şudur [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com/) birkaç algoritmaları hello karşı çalışır bir deneme sonuçları verilere ve karşılaştırır hello: [çok sınıfı sınıflandırıcı karşılaştırın: Harf tanıma ](http://gallery.cortanaintelligence.com/Details/a635502fc98b402a890efe21cec65b92).

> [!TIP]
> Machine Learning Studio'nun hello özelliklerine genel bakış sağlayan bir diyagram toodownload ve yazdırma bkz [Azure Machine Learning Studio işlevlerine genel bakış diyagramı](machine-learning-studio-overview-diagram.md).
> 
> 

## <a name="flavors-of-machine-learning"></a>Machine learning özellikleri
### <a name="supervised"></a>Denetimli
Denetimli öğrenme algoritmaları örnekler kümesine göre tahminlerde. Örneğin, geçmiş hisse senedi fiyatları kullanılan toohazard tahmin gelecekteki fiyatlarla olabilir. Eğitim için kullanılan her örnek hello ilgi değeriyle etiketli — bu durumda, hisse senedi fiyatı hello. Bu değer etiketleri düzenleri denetimli öğrenme algoritmasını arar. İlgili olabilecek herhangi bir bilgi kullanabilirsiniz — hello hafta hello sezonu, hello şirketin finansal verileri, sektör hello türü, kesintiye uğratan jeopolitik olayları hello varlığını hello gün — ve her algoritması desenleri farklı türleri için görünür. Hello algoritması hello en iyi düzeni dağıtabilirsiniz bulduktan sonra düzeni toomake tahminleri için test verilerinin etiketlenmemiş olduğunu kullanan — yarın'ın fiyatlar.

Denetimli öğrenme machine learning popüler ve kullanışlı bir türde değil. Bunun tek istisnası tüm hello modüllerdeki Azure Machine Learning algoritmaları öğrenme denetimli. Azure Machine Learning içinde temsil birkaç belirli denetimli öğrenme tür vardır: Sınıflandırma, regresyon ve anomali algılama.

* **Sınıflandırma**. Merhaba veri kullanılan toopredict bir kategori yükleniyor, denetimli öğrenme sınıflandırma da adlandırılır. Bu hello görüntüyü 'Kat' veya 'köpek' resim olarak atarken durumdur. Yalnızca iki seçenek olduğunda çağrılır **iki sınıflı** veya **iki terimli sınıflandırma**. Olarak olduğunda daha fazla kategori hello NCAA Mart Madness TURNUVASI hello kazanan tahmin etmeye olduğunda, bu sorunu olarak bilinir **çok sınıfı sınıflandırma**.
* **Regresyon**. Bir değer, gibi stok fiyatlarla tahmin denetimli öğrenme regresyon denir.
* **Anomali algılama**. Bazen hello yalnızca olağan dışı tooidentify veri noktaları hedeftir. Sahtekarlık algılama, örneğin, şüpheli tüm oldukça olağandışıdır kredi kartı harcama desenleri alır. Merhaba olası değişimler kadar çok sayıda ve bu nedenle birkaç, sahte hangi etkinlik benzer olmayan uygun toolearn olduğunu eğitim örnekleri hello. Anomali algılama alan toosimply yaklaşımdır (Geçmiş sahte olmayan işlemleri kullanarak gibi) hangi normal etkinlik arar öğrenin ve önemli ölçüde farklı olan her şeyi belirleyin.

### <a name="unsupervised"></a>Denetimsiz
Denetimsiz öğrenme içinde veri noktaları ilişkili hiçbir etiket vardır. Bunun yerine, bazı yolu veya toodescribe hello verileri yapısını düzenlemek için algoritmasıdır hello hedefi bir Denetimsiz öğrenme. Kümeler halinde gruplandırmak veya basit ya da daha düzenli görünmesi karmaşık veri arayan farklı yöntemler bulma anlamına gelebilir.

### <a name="reinforcement-learning"></a>Öğrenmeyi öğrenme
Öğrenmeyi öğrenmede hello algoritması toochoose yanıt tooeach veri noktasında bir eylemi alır. Merhaba öğrenme algoritmasını ayrıca bir kısa ne kadar iyi hello karar belirten süresi daha sonra bir ödül sinyali alır.
Bunu temel alarak, sipariş tooachieve hello yüksek ödül kendi stratejinize hello algoritması değiştirir. Şu anda Azure Machine Learning'de algoritma modülleri öğrenme hiçbir öğrenmeyi vardır. Burada hello zaman içinde bir noktada sensör okumaları kümesi, veri noktası ve hello algoritması hello robot'ın bir sonraki eylem seçmelisiniz robotics öğrenmeyi öğrenme yaygındır. Ayrıca, bir doğal uygulamaları şeyler Internet için uygun değildir.

## <a name="considerations-when-choosing-an-algorithm"></a>Bir algoritma seçerken dikkat edilecek noktalar
### <a name="accuracy"></a>Doğruluk
Merhaba en doğru yanıt olası alma her zaman gerekli değildir.
Bazen yaklaşık kullanmak istediğinize bağlı olarak, yeterlidir. Merhaba durum söz konusuysa mümkün toocut olabilir, işleme süresini önemli ölçüde daha fazla yaklaşık yöntemleriyle kalmanız tarafından. Daha fazla yaklaşık yöntemleri başka bir avantajı bunlar doğal olarak önlemek için eğilimindedir olan [overfitting](https://youtu.be/DQWI1kvmwRg).

### <a name="training-time"></a>Eğitim süresini
dakika sayısını hello veya saat gerekli tootrain bir model büyük miktarda algoritmaları arasında değişir. Zaman eğitim genellikle yakından bağlı tutarlılık — bir genellikle eşlik hello diğer. Ayrıca, bazı algoritmaları daha hassas toohello veri noktası sayısı diğerlerinden şunlardır.
Zaman sınırlı olduğunda özellikle hello veri kümesi büyük olduğunda hello seçim algoritmasının sürücü.

### <a name="linearity"></a>Doğrusallık
Machine learning algoritmaları çok sayıda olun Doğrusallık kullanın. Doğrusal sınıflandırma algoritmaları bir çizgide (veya daha yüksek boyutlu analog) sınıfları ayrılabilir varsayalım. Bunlar Lojistik regresyon ve vektör makineler (Azure Machine Learning ile uygulanan gibi) destek içerir.
Doğrusal regresyon algoritması, veri eğilimleri bir çizgide izleyin varsayalım. Bu varsayımları bazı sorunlar için hatalı değildir, ancak bazılarında bunlar doğruluğu getir.

![Doğrusal Dışı sınıfı sınır][1]

***Doğrusal Dışı sınıfı sınır*** *-bir doğrusal sınıflandırma algoritmasıdır bağlı olan düşük doğruluk sonuçlanacak*

![Doğrusal eğilim verileri][2]

***Doğrusal eğilim verilerle*** *-doğrusal regresyon yöntemini kullanarak gereken daha büyük kadar hataları oluşturmak*

Kendi tehlikeleri rağmen doğrusal algoritmaları çok saldırı ilk satır yaygındır. Bunlar toobe algorithmically basit ve hızlı eğitmek için eğilimi gösterir.

### <a name="number-of-parameters"></a>Parametre sayısı
Parametreleridir hello düğmelerini bir algoritma ayarlarken veri Bilimcisi tooturn alır. Bunlar hata toleransı veya yineleme veya hello algoritması nasıl davranacağını, çeşitler arasında seçenekleri sayısı gibi hello algoritması'nin davranışını etkilemek numaralarıdır. Bazen Hello eğitim süresini ve hello algoritması doğruluğunu oldukça önemli toogetting yalnızca hello doğru ayarları olabilir. Genellikle, çok sayıda parametre algoritmalarıyla hello en deneme ve hata toofind iyi bir birleşimi gerektirir.

Alternatif olarak, var olan bir [parametresi Süpürme](machine-learning-algorithm-parameters-optimize.md) modülü bloğunda Azure Machine Learning'de, seçtiğiniz herhangi bir ayrıntı düzeyi, tüm parametresi birleşimleri otomatik olarak çalışır. Bu harika bir şekilde toomake olmakla birlikte emin hello parametre alan yayılmış, hello gereken süre tootrain bir model katlanarak hello sayıda parametre ile artırır.

Merhaba baş fazla parametre genellikle sahip bir algoritma esneklik sahip olduğunu gösterir olur. Genellikle çok iyi doğruluğu elde edebilirsiniz. Sağlanan parametre ayarları doğru bileşimini hello bulabilirsiniz.

### <a name="number-of-features"></a>Özellikleri sayısı
Belirli veri türlerini hello birçok özellik veri noktası sayısı çok büyük karşılaştırılan toohello olabilir. Bu genellikle hello genetics veya metin veri durumdur. Özellikler Hello sayıda unfeasibly uzun zaman eğitim yapmadan bazı learning algoritmaları bog. Destek vektör makinelerdir özellikle uygun toothis çalışması (aşağıya bakın).

### <a name="special-cases"></a>Özel durumlar
Bazı learning algoritmaları hello veri ya da istenen hello sonuçları hello yapısını hakkında belirli varsayımlar olun. Gereksinimlerinize uyan bir fark ederseniz, bu, daha yararlı sonuçlar, daha doğru tahminleri ya da daha hızlı eğitim süreleri verebilirsiniz.

| **Algoritması** | **Doğruluk** | **Eğitim süresini** | **Doğrusallık** | **Parametreler** | **Notlar** |
| --- |:---:|:---:|:---:|:---:| --- |
| **İki sınıflı sınıflandırma** | | | | | |
| [Lojistik regresyon](https://msdn.microsoft.com/library/azure/dn905994.aspx) | |● |● |5 | |
| [karar orman](https://msdn.microsoft.com/library/azure/dn906008.aspx) |● |○ | |6 | |
| [karar jungle](https://msdn.microsoft.com/library/azure/dn905976.aspx) |● |○ | |6 |Düşük bellek alanı |
| [Artırılmış karar ağacı](https://msdn.microsoft.com/library/azure/dn906025.aspx) |● |○ | |6 |Büyük bellek alanı |
| [sinir ağı](https://msdn.microsoft.com/library/azure/dn905947.aspx) |● | | |9 |[Ek özelleştirme mümkündür](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [Ortalama perceptron](https://msdn.microsoft.com/library/azure/dn906036.aspx) |○ |○ |● |4 | |
| [vektör makinesi desteği](https://msdn.microsoft.com/library/azure/dn905835.aspx) | |○ |● |5 |Büyük özellik kümeleri için iyi |
| [yerel olarak ayrıntılı destek vektör makinesi](https://msdn.microsoft.com/library/azure/dn913070.aspx) |○ | | |8 |Büyük özellik kümeleri için iyi |
| [Bayes noktası makinesinin](https://msdn.microsoft.com/library/azure/dn905930.aspx) | |○ |● |3 | |
| **Birden çok sınıf sınıflandırma** | | | | | |
| [Lojistik regresyon](https://msdn.microsoft.com/library/azure/dn905853.aspx) | |● |● |5 | |
| [karar orman](https://msdn.microsoft.com/library/azure/dn906015.aspx) |● |○ | |6 | |
| [karar jungle](https://msdn.microsoft.com/library/azure/dn905963.aspx) |● |○ | |6 |Düşük bellek alanı |
| [sinir ağı](https://msdn.microsoft.com/library/azure/dn906030.aspx) |● | | |9 |[Ek özelleştirme mümkündür](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [biri v tümü](https://msdn.microsoft.com/library/azure/dn905887.aspx) |- |- |- |- |Seçilen hello iki sınıflı yöntemi özelliklerini bakın |
| **Regresyon** | | | | | |
| [Doğrusal](https://msdn.microsoft.com/library/azure/dn905978.aspx) | |● |● |4 | |
| [Bayesian doğrusal](https://msdn.microsoft.com/library/azure/dn906022.aspx) | |○ |● |2 | |
| [karar orman](https://msdn.microsoft.com/library/azure/dn905862.aspx) |● |○ | |6 | |
| [Artırılmış karar ağacı](https://msdn.microsoft.com/library/azure/dn905801.aspx) |● |○ | |5 |Büyük bellek alanı |
| [Hızlı orman quantile](https://msdn.microsoft.com/library/azure/dn913093.aspx) |● |○ | |9 |Noktası tahminleri yerine dağıtımları |
| [sinir ağı](https://msdn.microsoft.com/library/azure/dn905924.aspx) |● | | |9 |[Ek özelleştirme mümkündür](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [Poisson](https://msdn.microsoft.com/library/azure/dn905988.aspx) | | |● |5 |Teknik olarak günlük doğrusal. Sayıları etmede |
| [sıra sayısı](https://msdn.microsoft.com/library/azure/dn906029.aspx) | | | |0 |RANK sıralama etmede |
| **Anormallik algılama** | | | | | |
| [vektör makinesi desteği](https://msdn.microsoft.com/library/azure/dn913103.aspx) |○ |○ | |2 |Büyük özellik kümeleri için özellikle iyi |
| [PCA tabanlı anomali algılama](https://msdn.microsoft.com/library/azure/dn913102.aspx) | |○ |● |3 | |
| [K-ortalamaları](https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/) | |○ |● |4 |Bir kümeleme algoritması |

**Algoritma özellikleri:**

**●** -mükemmel doğruluğu, hızlı eğitim kez ve Doğrusallık hello kullanımını gösterir

**○** -iyi doğruluk ve orta eğitim süreleri gösterir

## <a name="algorithm-notes"></a>Algoritma notları
### <a name="linear-regression"></a>Çizgisel regresyon
Daha önce belirtildiği gibi [doğrusal regresyon](https://msdn.microsoft.com/library/azure/dn905978.aspx) uygun bir satırı (veya düzlemi veya hyperplane) toohello veri kümesi. Basit ve hızlı, workhorse olduğu, ancak bazı sorunlar için aşırı simplistic olabilir.
Burada denetle bir [doğrusal regresyon Öğreticisi](machine-learning-linear-regression-in-azure.md).

![Doğrusal eğilim verileri][3]

***Doğrusal eğilim verileri***

### <a name="logistic-regression"></a>Lojistik regresyon
Confusingly hello adlarında 'regresyon' içeren Lojistik regresyon gerçekten güçlü bir araç için olsa da [iki sınıflı](https://msdn.microsoft.com/library/azure/dn905994.aspx) ve [veya çoklu sınıflar](https://msdn.microsoft.com/library/azure/dn905853.aspx) sınıflandırma. Hızlı ve kolay bir işlemdir. Merhaba kullandığı gerçek bir kişinin '-şekilli eğri bir çizgide yerine gruplar halinde veri bölmek için doğal bir uyum sağlar. Kullandığınızda Lojistik regresyon verir doğrusal sınıfı sınırlar, bu nedenle doğrusal yaklaşık ile canlı bir şey olduğundan emin olun.

![Tek bir özellik Lojistik regresyon tootwo sınıfı verilerle][4]

***Tek bir özellik Lojistik regresyon tootwo sınıfı verilerle*** *-hangi hello Lojistik eğri olduğundan yalnızca yakın tooboth sınıfları başlangıç noktası sınıf sınırıdır*

### <a name="trees-forests-and-jungles"></a>Ağaçları, ormanlar ve ormanları
Karar ormanları ([regresyon](https://msdn.microsoft.com/library/azure/dn905862.aspx), [iki sınıflı](https://msdn.microsoft.com/library/azure/dn906008.aspx), ve [veya çoklu sınıflar](https://msdn.microsoft.com/library/azure/dn906015.aspx)), karar ormanları ([iki sınıflı](https://msdn.microsoft.com/library/azure/dn905976.aspx) ve [ veya çoklu sınıflar](https://msdn.microsoft.com/library/azure/dn905963.aspx)) ve karar ağaçları boosted ([regresyon](https://msdn.microsoft.com/library/azure/dn905801.aspx) ve [iki sınıflı](https://msdn.microsoft.com/library/azure/dn906025.aspx)) tüm karar ağaçları, temel machine learning kavram temel alır. Karar ağaçları, çok sayıda çeşitlemesi vardır, ancak bunların tümü aynı işlevi görür — çoğunlukla hello bölgesiyle içine hello özellik alanı ayırabilir aynı etiketi. Bu bölgeler tutarlı kategori veya sınıflandırma veya regresyon yapmakta olduğunuz bağlı olarak sabit değer olabilir.

![Karar ağacında bir özellik alanı subdivides][5]

***Karar ağacında bir özellik alanı kabaca Tekdüzen değerleri bölgelere subdivides***

Bir özellik alanı rasgele küçük bölgelere bölünmüştür, ortamınızdaki yeterli toohave veri noktası her bölge bölerek kolay tooimagine demektir. Bu aşırı overfitting örneğidir. Sipariş tooavoid Bu, çok sayıda ağaçları oluşturulur geçen özel matematiksel dikkatli hello ağaçları değil bağıntılı. Bu "karar ormanın" Merhaba ortalama overfitting engelleyen bir ağacıdır. Karar ormanları çok miktarda bellek kullanabilir. Karar ormanları hello gider biraz daha uzun bir eğitim süre en az bellek tüketir bir VARIANT ' dir.

Artırılmış karar ağaçları kaç kez ayırabilir ve her bölgede nasıl birkaç veri noktası izin verilir sınırlayarak overfitting kaçının. Algoritma ağaçları, her biri için önce hello ağacı tarafından sol hello hata dengelemek için öğrenir dizisi oluşturur. Merhaba, toouse çok miktarda bellek eğilimlidir çok doğruysa bir öğrenen sonucudur. Merhaba tam teknik açıklamasını kullanıma [Friedman'ın özgün kağıt](http://www-stat.stanford.edu/~jhf/ftp/trebst.pdf).

[Hızlı orman quantile regresyon](https://msdn.microsoft.com/library/azure/dn913093.aspx) hello özel durum (yalnızca hello tipik ORTANCA) değerini bir bölge, aynı zamanda, dağıtım quantiles hello biçiminde hello verileri bilmek istediğiniz yere karar ağaçları çeşididir.

### <a name="neural-networks-and-perceptrons"></a>Sinir ağları ve perceptrons
Sinir ağları beyin-neden olacak kapsayan algoritmaları öğrenme [veya çoklu sınıflar](https://msdn.microsoft.com/library/azure/dn906030.aspx), [iki sınıflı](https://msdn.microsoft.com/library/azure/dn905947.aspx), ve [regresyon](https://msdn.microsoft.com/library/azure/dn905924.aspx) sorunları. Sonsuz bir çeşitlilik gelir ancak hello sinir ağları Azure Machine Learning içinde yönlendirilmiş Çevrimsiz grafik hello biçiminde tümü. Giriş özellikleri ileri (hiçbir zaman geri) katmanları bir dizi çıkışları açık önce aktarılmasını anlamına gelir. Her katmanda toplanır ve hello sonraki katmana geçirildi çeşitli bileşimlerini girişleri ağırlıklı. Bu özelliği toolearn basit hesaplamalar sonuçlarında bileşimi sınıfı sınırları ve veri eğilimleri görünen magic ile Gelişmiş. Çok katmanlı ağlar bu tür "çok teknik raporlama fuels derin öğrenme" Merhaba ve Bilim Kurgu gerçekleştirin.

Bu yüksek performanslı ücretsiz, ancak gelmez. Sinir ağları özelliklerinin çok büyük veri kümeleri için özellikle bir uzun süre tootrain alabilir. Bunlar ayrıca parametre Süpürme hello eğitim süresini büyük miktarda genişletir anlamına gelir çoğu algoritmaları sayısından daha fazla parametre vardır.
Ve çok istediğiniz bu overachievers[kendi ağ yapısı belirtmek](http://go.microsoft.com/fwlink/?LinkId=402867), olanakları inexhaustible.

![Sınırları öğrenilen sinir ağları tarafından][6]
***sinir ağları tarafından öğrenilen hello sınırları karmaşık ve düzensiz olabilir***

Merhaba [perceptron iki sınıflı ortalaması](https://msdn.microsoft.com/library/azure/dn906036.aspx) sinir ağları yanıt tooskyrocketing eğitim katıdır. Doğrusal sınıfı sınırları sağlayan bir ağ yapısını kullanır. Günümüzün standartlarıyla neredeyse ilkel, ancak yerine çalışma uzun bir geçmişi vardır ve küçük toolearn hızla olduğu.

### <a name="svms"></a>SVMs
Destek vektör makineleri (SVMs) geniş bir kenar boşluğu mümkün olduğunca olarak sınıfları tarafından ayıran hello sınır bulun. Merhaba iki sınıf açıkça ayrılmış olamaz hello algoritmaları hello en iyi sınır yapabilir bulur. Azure Machine Learning ile yazılmış gibi hello [iki sınıflı SVM](https://msdn.microsoft.com/library/azure/dn905835.aspx) bunu yalnızca düz bir çizgi ile yapar. (SVM seslendir içinde doğrusal çekirdek kullandığı.) Bu Doğrusal benzetimini yapar, mümkün toorun oldukça hızlı bir şekilde demektir. Burada gerçekten inanılmaz özelliği yoğun metin gibi veya genomic ile veridir. Bu durumlarda SVMs mümkün tooseparate daha hızlı ve daha az çoğu diğer algoritmalar, ayrıca toorequiring yalnızca uygun miktarda bellek overfitting ile sınıflarıdır.

![Destek vektör makinesi sınıfı sınır][7]

***Normal destek vektör makinesi sınıfı sınır iki sınıf ayırarak başlangıç kenar boşluğu en üst düzeye çıkarır.***

Başka bir ürün Microsoft Research hello [iki sınıflı yerel olarak derin SVM](https://msdn.microsoft.com/library/azure/dn913070.aspx) doğrusal olmayan bir hello doğrusal sürüm hello hızı ve bellek verimliliğini çoğunu korur SVM çeşididir. Merhaba doğrusal yaklaşım yeterince doğru yanıtlar burada vermediğinin durumları için idealdir. Merhaba geliştiriciler küçük doğrusal SVM sorunları bir grup hello sorunla hızlı bölmek tarafından tutulur. Okuma hello [tam açıklama](http://research.microsoft.com/um/people/manik/pubs/Jose13.pdf) nasıl bunlar bu eli çekilen hello hakkındaki ayrıntılar için.

Doğrusal SVMs, akıllı bir uzantısını kullanarak, hello [bir sınıf SVM](https://msdn.microsoft.com/library/azure/dn913103.aspx) sıkı bir şekilde hello tüm veri kümesinin özetlenmektedir bir sınır çizer. Anomali algılama için yararlı olacaktır. Şu ana kadar bu sınırının dışında kalan herhangi yeni veri olağan dışı yeterince toobe önemli noktalardır.

### <a name="bayesian-methods"></a>Bayesian yöntemleri
Bayesian yöntemlerine sahip yükseltebilirsiniz kalitesi: overfitting kaçının. Önceden hello büyük olasılıkla hello yanıt dağıtılması hakkında bazı varsayımlar yaparak bunu. Bu yaklaşımın başka bir byproduct çok az parametrelere sahip olur. Azure Machine Learning sahip iki sınıflandırma için her iki Bayesian algoritmalar ([iki sınıflı Bayes noktası makinesi](https://msdn.microsoft.com/library/azure/dn905930.aspx)) ve gerileme ([Bayesian doğrusal regresyon](https://msdn.microsoft.com/library/azure/dn906022.aspx)).
Bunlar hello veri yüklenebilir bölme veya bir çizgide uygun olduğunu varsayın unutmayın.

Geçmiş bir not üzerinde Bayes noktası makineler Microsoft Research'te geliştirilen. Bazı olağanüstü güzel teorik iş arkasına sahiptirler. Merhaba ilgilenen Öğrenci olan yönlendirilmiş toohello [JMLR özgün makaleye](http://jmlr.org/papers/volume1/herbrich01a/herbrich01a.pdf) ve bir [Chris Güneş tarafından ayrıntılı blog](http://blogs.technet.com/b/machinelearning/archive/2014/10/30/embracing-uncertainty-probabilistic-inference.aspx).

### <a name="specialized-algorithms"></a>Özelleştirilmiş algoritmaları
Belirli bir hedefe sahip değilse Şanslar olabilir. Hello Azure Machine Learning koleksiyonu içinde içinde specialize algoritmaları vardır:

- RANK tahmin ([sıralı regresyon](https://msdn.microsoft.com/library/azure/dn906029.aspx)),
- Tahmin sayısı ([Poisson regresyon](https://msdn.microsoft.com/library/azure/dn905988.aspx)),
- anomali algılama (birini temel alarak [asıl bileşenlerini analiz](https://msdn.microsoft.com/library/azure/dn913102.aspx) ve temel bir [destek vektör makinesi](https://msdn.microsoft.com/library/azure/dn913103.aspx)s)
- Kümeleme ([K-ortalamaları](https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/))

![PCA tabanlı anomali algılama][8]

***PCA tabanlı anomali algılama*** *-hello veri hello çoğunluğu stereotipik dağıtım döner; bu dağıtım noktasından önemli ölçüde deviating şüpheli noktalarıdır*

![Veri kümesi K-ortalamaları kullanarak gruplandırılmış][9]

***Bir veri kümesi K-ortalamaları kullanarak beş kümeler halinde gruplandırılır***

Ayrıca bir ensemble olan [biri v tümü çok sınıflı sınıflandırıcı](https://msdn.microsoft.com/library/azure/dn905887.aspx), hangi sonları hello N sınıfı sınıflandırma sorunla N-1 iki sınıflı sınıflandırma sorunları. Merhaba doğruluğu, eğitim süresini ve Doğrusallık özellikleri kullanılan hello iki sınıflı sınıflandırıcı tarafından belirlenir.

![İki sınıflı sınıflandırıcı tooform üç sınıfı sınıflandırıcı birleştirilmiş][10]

***İki sınıflı sınıflandırıcı çifti tooform üç sınıfı sınıflandırıcı birleştirin***

Azure Machine Learning de içeren erişim tooa güçlü machine learning framework hello başlığı altında [Vowpal Wabbit](https://msdn.microsoft.com/library/azure/8383eb49-c0a3-45db-95c8-eb56a1fef5bf).
Sınıflandırma ve regresyon sorunları öğrenebilirsiniz ve kısmen etiketlenmemiş verilerden bile öğrenebilirsiniz VW burada kategori Koşullarımız. Toouse algoritmalar, kaybı işlevleri ve en iyi duruma getirme algoritmaları öğrenme sayısı birini yapılandırabilirsiniz. Verimli, paralel ve son derece hızlı toobe plan hello gelen tasarlanmıştır. Gerçekten büyük özellik kümeleri az belirgin çabayla işler.
Başlatıldı ve Microsoft Research's kendi John Langford tarafından neden VW hisse senedi araba algoritmalarının bir alandaki formülü tek bir giriştir. Her sorun VW uygun ancak sizin varsa, bu, while olabilir tooclimb arabiriminde öğrenme eğrisi. Ayrıca olarak kullanılabilir [tek başına açık kaynak kodu](https://github.com/JohnLangford/vowpal_wabbit) çeşitli dillerde.

## <a name="more-help-with-algorithms"></a>Daha fazla yardıma algoritmaları
* Algoritmaları açıklar ve örnekler sağlayan bir indirilebilir bilgi grafiği için bkz: [indirilebilir bilgi grafiği: Makine öğrenme algoritmasını örneklerle temel](machine-learning-basics-infographic-with-algorithm-examples.md).
* Azure Machine Learning Studio'da kullanılabilen tüm hello machine learning algoritmaları kategoriye göre bir listesi için bkz: [modeli Başlat] [ initialize-model] hello Machine Learning Studio algoritması ve modülü Yardımı'nda.
* Bir tam alfabetik listesi algoritmaları ve Azure Machine Learning Studio'daki modüller için bkz: [Machine Learning Studio modülleri A-Z listesi] [ a-z-list] Machine Learning Studio algoritması ve modülü Yardımı'nda.
* Azure Machine Learning Studio'nun hello özelliklerine genel bakış sağlayan bir diyagram toodownload ve yazdırma bkz [Azure Machine Learning Studio işlevlerine genel bakış diyagramı](machine-learning-studio-overview-diagram.md).


<!-- Reference links -->
[initialize-model]: https://msdn.microsoft.com/library/azure/dn905812.aspx
[a-z-list]: https://msdn.microsoft.com/library/azure/dn906033.aspx

<!-- Media -->

[1]: ./media/machine-learning-algorithm-choice/image1.png
[2]: ./media/machine-learning-algorithm-choice/image2.png
[3]: ./media/machine-learning-algorithm-choice/image3.png
[4]: ./media/machine-learning-algorithm-choice/image4.png
[5]: ./media/machine-learning-algorithm-choice/image5.png
[6]: ./media/machine-learning-algorithm-choice/image6.png
[7]: ./media/machine-learning-algorithm-choice/image7.png
[8]: ./media/machine-learning-algorithm-choice/image8.png
[9]: ./media/machine-learning-algorithm-choice/image9.png
[10]: ./media/machine-learning-algorithm-choice/image10.png
