---
title: "aaaExecute Python makine betikleri öğrenme | Microsoft Docs"
description: "Anahatları Azure Machine Learning ve temel kullanım senaryoları, özellikleri ve sınırlamaları Python komut dosyaları için destek temel ilkeleri tasarlayın."
keywords: "python makine öğrenimi, pandas, python pandas, python komut dosyaları, python betiği yürütme"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ee9eb764-0d3e-4104-a797-19fc29345d39
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bradsev
ms.openlocfilehash: 8d23aaa972a46cb1a07ea0f18cc1e24933fe3e6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="execute-python-machine-learning-scripts-in-azure-machine-learning-studio"></a>Azure Machine Learning Studio’da Python machine learning betikleri yürütme

Bu konuda, Azure Machine Learning Python komut dosyalarını hello geçerli desteği için temel alınan hello tasarım ilkeleri açıklanmaktadır. sağlanan hello ana özellikleri de, dahil olmak üzere özetlenmiştir:

- Temel kullanım senaryoları yürütme
- bir web hizmeti bir denemeyi puan
- Varolan kod içeri aktarma desteği
- görselleştirmeleri dışarı aktarma
- denetimli özellik seçimi gerçekleştirin
- bazı sınırlamalar anlama

[Python](https://www.python.org/) hello aracı Üstten kapaklı birçok veri bilimcilerine, içinde vazgeçilmez bir araçtır. Şunları içerir:

* bir zarif ve kısa sözdizimi 
* platformlar arası desteği 
* çok miktarda güçlü kitaplıkları ve 
* Olgun geliştirme araçları. 

Python makine öğrenimi modelleme genelde kullanılan bir iş akışının tüm aşamaları kullanılıyor:

- veri alma ve işleme 
- özellik oluşturma
- Model eğitimi 
- Model doğrulama
- Merhaba modelleri dağıtımı

Azure Machine Learning Studio, bir makine öğrenimi denemesinin ve aynı zamanda sorunsuz bir şekilde Microsoft Azure web Hizmetleri olarak yayımlama çeşitli parçalara katıştırma Python komut dosyalarını destekler.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


## <a name="design-principles-of-python-scripts-in-machine-learning"></a>Machine Learning Python betiklerde tasarım ilkeleri

Azure Machine Learning Studio'da Hello birincil arabirim tooPython olan hello [Python betiği yürütme] [ execute-python-script] Şekil 1'de gösterilen modülü.

![image1](./media/machine-learning-execute-python-scripts/execute-machine-learning-python-scripts-module.png)

![image2](./media/machine-learning-execute-python-scripts/embedded-machine-learning-python-script.png)

Şekil 1 '. Merhaba **Python betiği yürütme** modülü.

Merhaba [Python betiği yürütme] [ execute-python-script] modül Azure ML Studio'da toothree girişleri kabul eder ve tootwo çıkışları (bölümden hello açıklanmıştır), kendi R analog gibi hello üretir [ R betiği yürütün] [ execute-r-script] modülü. Merhaba yürütülen Python kodu toobe özel olarak adlandırılmış olarak hello parametre kutusuna girilen giriş noktası olarak adlandırılan işlevi `azureml_main`. İlkeleri bu modül tooimplement kullanılan hello temel tasarım şunlardır:

1. *Python kullanıcılar için kullanılan deyimsel olması gerekir.* Çoğu Python kullanıcılar kendi kod modülleri içinde işlevler olarak öğeli. Bu nedenle executable deyimleri çok üst düzey bir modüle koyma görece olarak daha ender. Sonuç olarak, hello betik kutusu ayrıca özel olarak adlandırılmış bir Python işlevi karşılıklı toojust ifadeler alır. Merhaba hello işlevinde sunulan standart Python kitaplığı türleri gibi nesneleridir [Pandas](http://pandas.pydata.org/) veri çerçevelerini ve [NumPy](http://www.numpy.org/) dizileri.
2. *Yüksek kaliteli yerel arasında olmalıdır ve bulut yürütmeleri.* Merhaba kullanılan arka uç tooexecute hello Python kodu dayanır [Anaconda](https://store.continuum.io/cshop/anaconda/), platformlar arası bilimsel Python dağıtım yaygın olarak kullanılır. Merhaba en yaygın Python paketlerini Kapat too200 ile gelir. Bu nedenle, veri bilimcileri hata ayıklama ve yerel Azure Machine Learning uyumlu Anaconda ortamlarına kendi kodlarına hakkını kullanmaya devam eder. Varolan bir geliştirme ortamı gibi kullandığınız [IPython](http://ipython.org/) dizüstü bilgisayar veya [Visual Studio için Python Araçları](http://aka.ms/ptvs), toorun Azure ML deneme parçası olarak. Merhaba `azureml_main` giriş noktasıdır temel alınan bir Python işlevi ve bu nedenle *** Azure ML özgü kodu olmadan yazılabilir veya yüklü SDK hello.
3. *Diğer Azure Machine Learning modüller ile sorunsuz bir şekilde birleştirilebilir olması gerekir.* Merhaba [Python betiği yürütme] [ execute-python-script] modülü kabul eder, girişleri ve çıkışları, standart Azure Machine Learning veri kümeleri. Merhaba temel çerçevesinde saydam ve verimli bir şekilde hello Azure ML ve Python çalışma zamanları arasında köprü. Bu nedenle Python R ve SQLite çağıran dahil olmak üzere var olan Azure ML iş akışları ile birlikte kullanılabilir. Sonuç veri Bilimcisi iş akışları oluşturma:
   * Python ve Pandas önceden işlenmesi ve temizleme verileri için kullanın
   * birden çok veri kümeleri tooform özelliklerini birleştirme akış hello veri tooa SQL dönüşümü
   * Azure Machine Learning ile Merhaba algoritmaları kullanarak modelleri eğitme 
   * değerlendirin ve hello sonuçları r kullanarak işlem sonrası


## <a name="basic-usage-scenarios-in-ml-for-python-scripts"></a>ML Python komut dosyaları için temel kullanım senaryosu

Bu bölümde, biz hello temel hello kullanımlarını bazıları anket [Python betiği yürütme] [ execute-python-script] modülü. Girişleri toohello Python modülü Pandas veri çerçevelerini sunulur. Merhaba işlevi bir Python içinde paketlenmiş tek bir Pandas veri çerçevesi döndürmelidir [dizisi](https://docs.python.org/2/c-api/sequence.html) dizi, liste veya NumPy dizi gibi. Bu dizisinin ilk öğesi Hello sonra hello ilk çıkış bağlantı noktasına hello modülünün döndürülür. Şekil 2'de bu düzeni gösterilir.

![image3](./media/machine-learning-execute-python-scripts/map-of-python-script-inputs-outputs.png)

Şekil 2. Giriş bağlantı noktaları tooparameters ve dönüş değeri toooutput bağlantı noktası eşleme.

Merhaba, eşlenen tooparameters nasıl hello giriş bağlantı noktaları alır, semantiği ayrıntılı `azureml_main` işlevi, Tablo 1'de gösterilir:

![image1T](./media/machine-learning-execute-python-scripts/python-script-inputs-mapped-to-parameters.png)

Tablo 1. Giriş bağlantı noktaları toofunction parametrelerinin eşleme.

Giriş bağlantı noktaları ve işlev parametreleri arasında Hello eşleme konumsal şöyledir:

- Merhaba işlevinin ilk parametresi eşlenen toohello Hello ilk bağlı giriş bağlantı noktasıdır. 
- (bağlı değilse) hello ikinci giriş hello işlevinin ikinci parametresi eşlenen toohello olabilir.

Bkz: *veri analizi için Python* (O'Reilly, 2012) tarafından Batı McKinney daha fazla bilgi Python Pandas ve nasıl bu kullanılan toomanipulate veri etkili ve verimli şekilde olabilir. 


## <a name="translation-of-input-and-output-types"></a>Çeviri girdi ve çıktı türü 
Azure ML giriş veri kümelerinde Pandas dönüştürülmüş toodata çerçevelere ' dir. Çıktı veri çerçevelerini geri tooAzure ML veri kümeleri dönüştürülür. dönüşümler aşağıdaki hello gerçekleştirilir:

1. Dize ve sayısal sütunlar olarak dönüştürülür-olduğundan ve bir veri kümesinde eksik değerleri dönüştürülen too'NA' Pandas değerleri. Merhaba aynı dönüştürme olacağı şekilde geri hello üzerinde (NA Pandas değerler Azure ML dönüştürülmüş toomissing değerleri).
2. Azure ML dizin vektörlerinin Pandas içinde desteklenmiyor. Tüm giriş verilerini çerçeveleri hello Python işlevinde her zaman 0 toohello sayısı eksi 1 satırları 64-bit sayısal dizinden sahiptir. 
3. Azure ML veri kümeleri, yinelenen sütun adları ve dize olmayan sütun adları olamaz. Bir çıkış veri çerçevesi sayısal olmayan sütunları içeriyorsa, hello framework çağrıları `str` hello sütun adları. Benzer şekilde, otomatik olarak karıştırılmış tooinsure yinelenen sütun adları olan hello adları benzersizdir. Merhaba soneki (2) toohello ilk yinelenen, (3) toohello ikinci yinelenen ve benzeri eklenir.


## <a name="operationalizing-python-scripts"></a>Faaliyete geçirmeye yönelik Python komut dosyaları

Tüm [Python betiği yürütme] [ execute-python-script] bir Puanlama deneme kullanılan modülleri, bir web hizmeti olarak yayımlandığında çağrılır. Örneğin, Şekil 3'hello kod tooevaluate tek bir Python ifade içeren bir Puanlama deneme gösterir. 

![image4](./media/machine-learning-execute-python-scripts/figure3a.png)

![image5](./media/machine-learning-execute-python-scripts/python-script-with-python-pandas.png)

Şekil 3 '. Python ifade değerlendirme için web hizmeti.

Bu deneme oluşturulan web hizmeti:

- Python ifade (bir dize olarak) giriş olarak alır
- toohello Python yorumlayıcı gönderir 
- Merhaba ifade ve hesaplanan hello sonuç içeren bir tablo döndürür.


## <a name="importing-existing-python-script-modules"></a>Varolan Python betik modüllerini içeri aktarma

Birçok veri bilimcilerine için ortak bir kullanım örneği tooincorporate varolan Python komut dosyalarına Azure ML denemeler ' dir. Tüm kod birleştirilmiş ve tek bir komut dosyası kutusuna yapıştırılan istemek yerine hello [Python betiği yürütme] [ execute-python-script] modülü Python modülleri hello üçüncü giriş bağlantı noktası içeren bir zip dosyası kabul eder. Merhaba dosya çalışma zamanında hello yürütme framework tarafından sıkıştırması açılmış ve Merhaba içeriğine toohello kitaplık yolu hello Python yorumlayıcısı eklenir. Merhaba `azureml_main` işlevi aktarabilirsiniz bu modülleri doğrudan giriş noktası.

Örnek olarak, hello dosya basit bir "Hello, World" işlevini içeren Hello.py göz önünde bulundurun.

![image6](./media/machine-learning-execute-python-scripts/figure4.png)

Şekil 4 '. Kullanıcı tanımlı işlev Hello.py dosyasında.

Ardından, bir dosya Hello.py içeren Hello.zip oluşturun:

![image7](./media/machine-learning-execute-python-scripts/figure5.png)

Şekil 5. Kullanıcı tanımlı Python kodu içeren zip dosyası.

Merhaba zip dosyası bir veri kümesi Azure Machine Learning Studio'ya yükleyin. Ardından oluşturup toohello üçüncü giriş bağlantı noktası hello ekleyerek hello Hello.zip dosyasında hello Python kodu kullanan bir denemeyi çalıştırın **Python betiği yürütme** bu şekilde gösterildiği gibi modülü.

![image8](./media/machine-learning-execute-python-scripts/figure6a.png)

![image9](./media/machine-learning-execute-python-scripts/figure6b.png)

Şekil 6. Kullanıcı tanımlı Python kodu ile örnek deneme bir zip dosyası olarak karşıya yüklendi.

Merhaba modülü çıktısını gösterir, hello zip dosyası paketlenmemiş taleplere yapılmış ve bu hello işlevi `print_hello` çalıştırılmış olabilir.
 
![image10](./media/machine-learning-execute-python-scripts/figure7.png)

Şekil 7. Kullanıcı tanımlı işlev hello içinde kullanımda [Python betiği yürütme] [ execute-python-script] modülü.


## <a name="working-with-visualizations"></a>Görsel öğeleri ile çalışma

Merhaba tarayıcıda canlandırılabilir MatplotLib kullanılarak oluşturulan çizimler hello tarafından döndürülen [Python betiği yürütme][execute-python-script]. Ancak r kullanırken oldukları gibi hello çizimleri otomatik olarak yeniden yönlendirilen tooimages Olmaları durumunda hello kullanıcı açıkça herhangi çizimleri tooPNG dosyaları kaydetmeniz gerekir böylece toobe geri tooAzure Machine Learning döndürdü. 

MatplotLib toogenerate görüntülerden hello aşağıdaki yordamı tamamlamanız gerekir:

* Merhaba arka uç geçiş çok Qt tabanlı Oluşturucu "AGG" Merhaba gelen varsayılan 
* Yeni bir şekil nesnesi oluşturun 
* Merhaba eksen alın ve tüm çizimleri içine oluştur 
* Merhaba şekil tooa PNG dosyası kaydedin 

Bu işlem Şekil 8 ' Pandas hello scatter_matrix işlevini kullanarak bir dağılım çizim matris oluşturan aşağıdaki hello gösterilmiştir.

![image1v](./media/machine-learning-execute-python-scripts/figure-v1-8.png)

Şekil 8'de. MatplotLib tooimages rakamları toosave kodu.

Şekil 9'hello ikinci çıkış bağlantı noktasına tooreturn çizer daha önce gösterilen hello komut dosyası kullanan bir denemeyi gösterilir.

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9a.png) 

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9b.png) 

Şekil 9. Python koddan oluşturulan çizimleri görselleştirme.

Farklı görüntülere kaydederek birden çok rakamları olası tooreturn olduğundan, Azure Machine Learning çalışma zamanı çekmeleri tüm görüntüleri yukarı hello ve görselleştirme için art arda ekler.


## <a name="advanced-examples"></a>Gelişmiş örnekleri

Azure Machine Learning yüklü hello Anaconda ortamı NumPy, SciPy ve Scikits öğrenin gibi ortak paketleri içerir. Bu paketleri, machine learning ardışık düzen çeşitli veri işleme görevler için etkili bir şekilde kullanılabilir. Örnek olarak, hello aşağıdaki deneme ve komut dosyası hello kullanımını ensemble öğrencileriyle toocompute özelliği önem puanları Scikits öğrenmek, bir veri kümesi için gösterir. Merhaba puanları denetimli kullanılan tooperform özellik seçimi önce başka bir ML modeline sat olabilir.

Merhaba Python kullanılan işlev toocompute hello önem puanlarını ve hello puanları temel alarak sipariş hello özelliklerinin şöyledir:

![image11](./media/machine-learning-execute-python-scripts/figure8.png)

Şekil 10. Puanları göre işlevi toorank özellikler.
 Merhaba aşağıdaki deneme ardından hesaplar ve Azure Machine Learning hello "Pima Hint Diabetes" kümesinde hello önem puanları özelliklerinin döndürür:

![image12](./media/machine-learning-execute-python-scripts/figure9a.png)
![image13](./media/machine-learning-execute-python-scripts/figure9b.png)    

Şekil 11. Merhaba Pima Hint Diabetes kümesindeki deneme toorank özellikleri.

## <a name="limitations"></a>Sınırlamalar
Merhaba [Python betiği yürütme] [ execute-python-script] şu anda hello aşağıdaki sınırlamalar vardır:

1. *Korumalı yürütme.* Merhaba Python çalışma zamanı şu anda korumalı ve sonuç olarak, erişim toohello ağ veya toohello yerel dosya sistemi kalıcı bir biçimde izin vermiyor. Yerel olarak kaydedilen tüm dosyaları yalıtılmış ve hello modülü tamamlandıktan sonra silinir. Merhaba Python kodu, üzerinde çalıştığı hello makinedeki çoğu dizinlerde erişemiyor, geçerli dizin ve alt dizinlerinde hello hello özel durumu olan.
2. *Gelişmiş geliştirme ve hata ayıklama desteği eksiği.* Merhaba Python modülü IntelliSense ve hata ayıklama gibi IDE özellikleri şu anda desteklemiyor. Çalışma zamanında Hello modülü başarısız olursa, ayrıca, hello tam Python yığın izlemesi mevcuttur. Ancak hello modülü için hello çıktı günlüğüne görüntülenmelidir. Şu anda, geliştirmek ve Python komut dosyaları IPython gibi bir ortamda hata ayıklama ve hello modüle hello kod içeri aktarma öneririz.
3. *Tek bir veri çıkışı çerçevesi.* Merhaba Python giriş yalnızca izin verilen tooreturn bir tek veri çerçevesi çıkış olarak noktasıdır. Eğitilmiş modeller doğrudan toohello Azure Machine Learning çalışma zamanı geri gibi rasgele Python nesneleri şu anda olası tooreturn değil. Gibi [R betiği yürütün][execute-r-script], hello sahip olduğu aynı sınırlama, bu mümkündür toopickle nesneleri bir bayt dizisi ve ardından, veri çerçevesi içinde dönün birçok durumda.
4. *Bağlanamama toocustomize Python yükleme*. Şu anda hello yalnızca yolu tooadd özel Python modülleri mekanizmasıdır daha önce açıklanan hello zip dosyası. Bu küçük modülleri için uygun olmakla birlikte, büyük modülleri (özellikle de yerel DLL'leri ile) veya çok sayıda modülleri için sıkıcı. 

## <a name="conclusions"></a>Sonuçları
Merhaba [Python betiği yürütme] [ execute-python-script] modülü bulutta barındırılan machine learning akışlarında Azure Machine Learning ve tooseamlessly içine tooincorporate varolan Python kodu bir veri Bilimcisi sağlar web hizmetinin bir parçası olarak faaliyete. Merhaba Python komut satırı modülü, doğal olarak Azure Machine Learning diğer modülleri ile birlikte çalışır. Merhaba modülü, bir dizi göreve veri araştırması toopre-işleme ve özellik ayıklama'i ve tooevaluation ve hello sonuçlarının sonrası işlemler için kullanılabilir. Merhaba arka uç çalışma zamanı yürütme için kullanılan iyi test edilmiş ve yaygın olarak kullanılan bir Python dağıtımı Anaconda üzerinde temel alır. Bu arka uç onu sizin için tooon Panosu varolan kod varlıklarına hello bulutunu kolaylaştırır.

Tooprovide ek işlevler toohello bekliyoruz [Python betiği yürütme] [ execute-python-script] modülü gibi özelliği tootrain hello ve Python modellerinde faaliyete ve tooadd daha iyi hello için destek geliştirme ve Azure Machine Learning Studio'da kodda hata ayıklama.

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için bkz: Merhaba [Python Geliştirici Merkezi](https://azure.microsoft.com/develop/python/).

<!-- Module References -->
[execute-python-script]: https://msdn.microsoft.com/library/azure/cdb56f95-7f4c-404d-bde7-5bb972e6f232/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
