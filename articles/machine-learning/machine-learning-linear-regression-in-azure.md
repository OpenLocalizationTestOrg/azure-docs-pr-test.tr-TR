---
title: "aaaUsing Machine learning'de doğrusal regresyon | Microsoft Docs"
description: "Excel'de ve Azure Machine Learning Studio'da doğrusal regresyon modellerin karşılaştırması"
metakeywords: 
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 417ae6ab-de4f-4bdd-957a-d96133234656
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: kbaroni;garye
ms.openlocfilehash: 8716040ad296053a72fb06c7c9660a186123ac15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-linear-regression-in-azure-machine-learning"></a>Azure Machine Learning’de doğrusal regresyonu kullanma
> *Kate Baroni* ve *Ben Boatman* Microsoft'un veri Öngörüler mükemmel merkezi çözüm mimarları Kurumsal şunlardır. Bu makalede, bunlar Azure Machine Learning kullanarak varolan Regresyon çözümleme suite tooa bulut tabanlı bir çözümü geçirme deneyimlerini açıklanmaktadır. 
> 
> 

&nbsp; 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="goal"></a>Hedef
Projemizin iki hedefleri düşünerek kullanmaya: 

1. Tahmine dayalı analiz tooimprove hello bizim kuruluşun aylık gelir tahminleri doğruluğunu kullanın 
2. Azure Machine Learning tooconfirm kullanmak için en iyi duruma getirme, hız, artırma ve ölçek bizim sonuçları. 

Birçok işletme gibi kuruluşunuzun işlem tahmin aylık gelir gider. Küçük ekibimiz iş analistleri, Azure Machine Learning toosupport hello işlemi kullanarak görevli ve tahmin doğruluğunu artırmak. Merhaba takım birden fazla kaynaktan veri toplama ve istatistiksel çözümleme anahtar öznitelikleri ilgili tooservices satış tahmin tanımlayan hello veri öznitelikleri çalıştıran birkaç ay harcanan. Merhaba sonraki adıma toobegin prototipi oluşturulurken istatistiksel regresyon hello verileri Excel'de modellerinde oluştu. Birkaç hafta içinde hello geçerli alan ve işlemleri tahmin Finans outperforming bir Excel regresyon modeli vardı. Bu hello temel tahmin sonuç hale geldi. 

Biz sonra hello sonraki adım toomoving bizim Tahmine dayalı analiz nasıl Machine Learning Tahmine dayalı üzerinde performansı çıkışı tooAzure Machine Learning toofind üzerinden sürdü.

## <a name="achieving-predictive-performance-parity"></a>Tahmine dayalı performans eşlik elde
Bizim birinci öncelik tooachieve eşlik Machine Learning ve Excel regresyon modelleri arasında oluştu. Verilen hello aynı veri ve aynı eğitim ve test verileri için bölme Merhaba, biz Excel ve Machine Learning arasındaki tooachieve Tahmine dayalı performans eşlik istedik. Başlangıçta alamadık. Merhaba Excel outperformed modeli hello Machine Learning modeli. Machine Learning ayarı hello temel aracı anlayış tooa eksikliği nedeniyle Hello hatası oluştu. Bir eşitleme hello Machine Learning ürün ekibi ile sonra size daha iyi hello temel bizim veri kümeleri için gerekli ayarını anlamak kazanılan ve hello iki modelleri arasında eşlik elde. 

### <a name="create-regression-model-in-excel"></a>Regresyon modeli Excel'de oluşturun
Bizim Excel regresyon hello Excel çözümleme araç takımı bulunan hello standart doğrusal regresyon modeli kullanılır. 

Biz hesaplanan *ortalama mutlak % hata* ve hello model için hello performans ölçü olarak kullanılır. Excel kullanarak bir çalışma modeli 3 ay tooarrive sürdü. Biz hello öğrenme hello sonuçta anlama gereksinimleri açısından yararlı olan Machine Learning Studio'da deneme içine çoğunu duruma getirdi.

### <a name="create-comparable-experiment-in-azure-machine-learning"></a>Azure Machine Learning ile karşılaştırılabilir deneme oluşturma
Bu adımları toocreate bizim denemeyi Machine Learning Studio'da izlenen: 

1. Bir csv dosyası tooMachine Learning Studio (çok küçük dosyası) olarak karşıya yüklenen hello veri kümesi
2. Yeni bir deneme oluşturulur ve hello kullanılan [Select Columns in Dataset sütun] [ select-columns] modülü tooselect hello Excel'de kullanılan aynı veri özellikleri 
3. Kullanılan hello [bölünmüş veri] [ split] Modülü (ile *göreli ifade* modu) Excel'de yapıldığı şekilde toodivide hello verisine hello aynı eğitim veri kümeleri 
4. Merhaba ile experimented [doğrusal regresyon] [ linear-regression] Modülü (yalnızca varsayılan seçenekleri), belgelenmiş ve hello sonuçları tooour Excel regresyon modeli karşılaştırması

### <a name="review-initial-results"></a>İlk sonuçlarını gözden geçirin
İlk başta, hello Excel modeli açıkça hello Machine Learning Studio modeli outperformed: 

|  | Excel | Studio |
| --- |:---:|:---:|
| Performans | | |
| <ul style="list-style-type: none;"><li>R kare ayarlandı</li></ul> |0.96 |Yok |
| <ul style="list-style-type: none;"><li>Katsayısı <br />Belirleme</li></ul> |Yok |0.78<br />(düşük doğruluğu) |
| Mutlak hata anlama |$9. 5M |$ 19.4 M |
| Ortalama mutlak hata (%) |6.03% |12.2% |

Bizim işlemi ve sonuçları hello geliştiriciler ve veri bilimcilerine tarafından hello Machine Learning ekipte karşılaştık, hızlı bir şekilde bazı yararlı ipuçları sağladıkları. 

* Merhaba kullandığınızda [doğrusal regresyon] [ linear-regression] modülü Machine Learning Studio'da iki yöntem sağlanır:
  * Çevrimiçi gradyan düşüşü: büyük ölçekli sorunları için daha uygun olabilir
  * Sıradan kareler: Çoğu kişi doğrusal regresyon duyduğunuzda düşünmek hello yöntem budur. Küçük veri kümeleri için normal kareler daha uygun bir seçenek olabilir.
* Merhaba L2 Regularization ağırlık parametresi tooimprove performans uyguladıkça göz önünde bulundurun. Varsayılan olarak too0.001 ayarlanır, ancak bizim küçük veri kümesi için bunu too0.005 tooimprove performans ayarlarız. 

### <a name="mystery-solved"></a>Çözülen sırrı!
Biz hello önerileri uygulandığında elde Excel gibi ile aynı temel performans Machine Learning Studio'da hello: 

|  | Excel | Studio (Başlangıç) | Studio kareler içeren |
| --- |:---:|:---:|:---:|
| Etiketli değer |Fiili (sayı) |Aynı |Aynı |
| Öğrenen |Excel -> veri analizi regresyon -> |Doğrusal regresyon. |Doğrusal regresyon |
| Öğrenen seçenekleri |Yok |Varsayılan olarak |sıradan kareler<br />L2 0.005 = |
| Veri kümesi |26 satır, 3 özellikleri, 1 etiketi. Tüm sayısal. |Aynı |Aynı |
| Böl: eğitimi |Excel ilk 18 satır üzerinde hello eğitilmiş, son 8 satır üzerinde hello test. |Aynı |Aynı |
| Böl: Test |Excel uygulanan regresyon formülü toohello son 8 satır |Aynı |Aynı |
| **Performans** | | | |
| R kare ayarlandı |0.96 |Yok | |
| Katsayısı |Yok |0.78 |0.952049 |
| Mutlak hata anlama |$9. 5M |$ 19.4 M |$9. 5M |
| Ortalama mutlak hata (%) |<span style="background-color: 00FF00;"> 6.03%</span> |12.2% |<span style="background-color: 00FF00;"> 6.03%</span> |

Ayrıca, hello Excel katsayısını iyi toohello özelliği ağırlıkları hello Azure eğitilen model içinde karşılaştırıldığında:

|  | Excel katsayısını | Azure özellik ağırlıkları |
| --- |:---:|:---:|
| Intercept/sapması |19470209.88 |19328500 |
| Özelliği A |0.832653063 |0.834156 |
| Özellik B |11071967.08 |11007300 |
| Özellik C |25383318.09 |25140800 |

## <a name="next-steps"></a>Sonraki Adımlar
Biz tooconsume hello Machine Learning web hizmetini Excel içinde istedik. Bizim iş analistleri Excel ve biz şekilde toocall hello Machine Learning web hizmeti bir Excel veri satırı ile ve sahip dönüş kullanır hello tahmin değeri tooExcel. 

Biz de toooptimize bizim modeli hello seçenekleri ve Machine Learning Studio'da kullanılabilen algoritmaları kullanarak istedik.

### <a name="integration-with-excel"></a>Excel ile tümleştirme
Bizim Machine Learning regresyon modeli hello eğitilen modelden bir web hizmeti oluşturarak toooperationalize bizim çözüm bulunuyordu. Birkaç dakika içinde hello web hizmeti oluşturulmuş ve doğrudan Excel tooreturn tahmin edilen gelir değerini adlandırılır. 

Merhaba *Web Hizmetleri Pano* bölüm indirilebilir bir Excel çalışma kitabı içerir. Merhaba çalışma kitabı katıştırılmış hello web hizmeti API ve şema bilgileri ile önceden biçimlendirilmiş gelir. Tıkladığınızda *karşıdan Excel çalışma kitabı*hello çalışma kitabını açar ve tooyour yerel bilgisayara kaydedin. 

![][1]

Açık Hello çalışma ile önceden tanımlanmış parametrelerinizi aşağıda gösterildiği gibi hello mavi parametre bölüme kopyalayın. Merhaba parametreleri girildikten sonra Machine Learning web hizmeti toohello Excel çağırır ve hello tahmin edilen puanlanmış etiketler hello yeşil tahmin edilen değerler bölümünde görüntülenir. Merhaba çalışma kitabı toocreate tahminleri, eğitilen model parametreleri altında girilen tüm satır öğeleri için temel parametreler için devam eder. Nasıl toouse bu özelliği ile ilgili daha fazla bilgi için bkz: [bir Azure Machine Learning Web hizmeti Excel'den tüketen](machine-learning-consuming-from-excel.md). 

![][2]

### <a name="optimization-and-further-experiments"></a>En iyi duruma getirme ve daha fazla denemeleri
Biz temel Excel modelimizi vardı, biz bizim Machine Learning doğrusal regresyon modeli tamamlanan toooptimize taşındı. Merhaba modülü kullandık [filtre tabanlı özellik seçimi] [ filter-based-feature-selection] tooimprove bizim seçimini ilk veri öğeleri ve Yardım bize performans geliştirmesi %4.6 elde ortalama mutlak hata. Veri öznitelikleri toofind hello sağ kümesinin modelleme için özellikler toouse üzerinden yineleme bize hafta kaydedebilir bu özellik gelecekteki projeleri için kullanacağız. 

Sonraki biz tooinclude diğer algoritmalar gibi planlama [Bayesian] [ bayesian-linear-regression] veya [Boosted karar ağaçları] [ boosted-decision-tree-regression] bizim deneme toocompare içinde performans. 

Regresyon ile tooexperiment istiyorsanız, iyi dataset tootry çok sayıda sayısal özniteliklere sahip hello enerji verimliliği regresyon örnek veri kümesidir. Merhaba dataset hello örnek veri kümesi Machine Learning Studio'da bir parçası olarak sağlanır. Modülleri toopredict öğrenme çeşitli kullanabilirsiniz ısıtma yük ya da soğutma yük. Aşağıdaki Hello grafik hello hedeflemek için değişken soğutma yük hello enerji verimliliğine dataset tahmin etmeye karşı farklı regresyon performans karşılaştırması öğrenir şöyledir: 

| modeli | Mutlak hata anlama | Kök ortalama karesi alınmış hata | Göreli mutlak hata | Göreli karesi alınmış hata | Katsayısı |
| --- | --- | --- | --- | --- | --- |
| Artırılmış karar ağacı |0.930113 |1.4239 |0.106647 |0.021662 |0.978338 |
| Doğrusal regresyon (gradyan düşüşü) |2.035693 |2.98006 |0.233414 |0.094881 |0.905119 |
| Sinir ağı regresyon |1.548195 |2.114617 |0.177517 |0.047774 |0.952226 |
| Doğrusal regresyon (sıradan kareler) |1.428273 |1.984461 |0.163767 |0.042074 |0.957926 |

## <a name="key-takeaways"></a>Anahtar paketler
Biz çok tarafından çalışan Excel regresyon öğrenilen ve paralel olarak Azure Machine Learning denemelerini. Excel ve Machine Learning kullanarak toomodels karşılaştırma oluşturma hello temel model [doğrusal regresyon] [ linear-regression] Yardım biz fırsatları tooimprove veri bulunan ve bize Azure Machine Learning öğrenin Seçim ve model performans. 

Ayrıca önerilir toouse olduğunu bulduk [filtre tabanlı özellik seçimi] [ filter-based-feature-selection] tooaccelerate gelecekteki tahmin projeleri. Özellik Seçimi tooyour veri uygulayarak, geliştirilmiş bir model Machine Learning ile daha iyi genel performansı oluşturabilirsiniz. 

Merhaba özelliği tootransfer hello Tahmine dayalı analitik Machine Learning tooExcel systemically tahmin önemli bir artış hello özelliği toosuccessfully verir tooa geniş iş kullanıcı İzleyici sonuçları sağlar. 

## <a name="resources"></a>Kaynaklar
Regresyon ile çalışmanıza yardımcı olacak bazı kaynaklar aşağıda verilmiştir: 

* Excel'de regresyon. Excel'de regresyon hiçbir zaman denediyseniz, Bu öğretici kolaylaştırır: [http://www.excel-easy.com/examples/regression.html](http://www.excel-easy.com/examples/regression.html)
* Tahmin regresyon vs. Tyler Chessman toodo ne zaman serisi doğrusal regresyon iyi bir başlangıç açıklamasını içerir Excel'de tahmin açıklayan bir blog makale yazıldı. [http://sqlmag.com/SQL-Server-Analysis-Services/Understanding-Time-Series-forecasting-Concepts](http://sqlmag.com/sql-server-analysis-services/understanding-time-series-forecasting-concepts) 
* Sıradan kareler doğrusal regresyon: Açıkları, sorunları ve Tuzaklar. Bir giriş ve regresyon tartışması: [http://www.clockbackward.com/2009/06/18/ordinary-least-squares-linear-regression-flaws-problems-and-pitfalls/](http://www.clockbackward.com/2009/06/18/ordinary-least-squares-linear-regression-flaws-problems-and-pitfalls/)

[1]: ./media/machine-learning-linear-regression-in-azure/machine-learning-linear-regression-in-azure-1.png
[2]: ./media/machine-learning-linear-regression-in-azure/machine-learning-linear-regression-in-azure-2.png


<!-- Module References -->
[bayesian-linear-regression]: https://msdn.microsoft.com/library/azure/ee12de50-2b34-4145-aec0-23e0485da308/
[boosted-decision-tree-regression]: https://msdn.microsoft.com/library/azure/0207d252-6c41-4c77-84c3-73bdf1ac5960/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

