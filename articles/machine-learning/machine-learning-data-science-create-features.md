---
title: "Veri bilimi aaaFeature Mühendisliği | Microsoft Docs"
description: "Özellik Mühendisliği Hello amaçları açıklar ve makine öğrenme hello veri geliştirme sürecinde rolü örnekleri sağlar."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 3fde69e8-5e7b-49ad-b3fb-ab8ef6503a4d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: zhangya;bradsev
ms.openlocfilehash: af40ea9cc9395bc87fe695eeaef26aa71e0ec9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="feature-engineering-in-data-science"></a>Veri bilimi özellik Mühendisliği
Bu konu özellik Mühendisliği hello amaçları açıklar ve makine öğrenme hello veri geliştirme sürecinde rolü örnekleri sağlar. Bu işlem, Azure Machine Learning Studio'dan çizilir tooillustrate Hello örnekler kullanılır. 

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Bu **menü** nasıl toocreate çeşitli ortamlarda veri özellikleri açıklamak tootopics bağlar. Bu görev bir hello adımdır [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

İşlem öğrenme hello kolaylaştırmak ham verilerden özellikler oluşturarak algoritmaları öğrenme mühendislik denemeleri tooincrease hello Tahmine dayalı güç özelliği. Mühendislik hello ve çeşitli özellikler ürününün bir parçasıdır TDSP özetlenen hello hello [hello takım veri bilimi işlemi yaşam döngüsü nedir?](data-science-process-overview.md) Özellik Mühendisliği ve seçim olan hello bölümlerini **geliştirmek özellikleri** hello TDSP adımında. 

* **özellik Mühendisliği**: Bu işlem toocreate ek ilgili özellikleri özelliklerinden hello varolan ham hello verilerdeki çalışır ve tooincrease hello hello öğrenme algoritmasının Tahmine dayalı güç.
* **Özellik Seçimi**: Bu işlem bir girişim tooreduce hello boyut hello eğitim sorununun içinde hello anahtar özelliklerin alt kümesini özgün veri seçer.

Normalde **özellik Mühendisliği** uygulanan ilk toogenerate ek özellikler ve hello **özellik seçimi** adımdır gerçekleştirilen tooeliminate ilgisiz, artık ya da son derece bağıntılı Özellikler.

Machine learning'de kullanılan hello eğitim verileri genellikle özellikleri ayıklama hello ham verilerden toplanan tarafından geliştirilebilir. Nasıl tooclassify hello görüntüleri el yazısı karakter olan bir bit hello ham bit dağıtım verilerinden oluşturulan yoğunluğu harita oluşturulmasını öğrenme hello bağlamda tasarlanan bir özellik örneği. Bu haritada hello karakter hello kenarlarına yalnızca hello ham dağıtım doğrudan kullanımına kıyasla daha verimli bir şekilde belirlemeye yardımcı olabilir.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="creating-features-from-your-data---feature-engineering"></a>Özellikleri oluşturma verilerinizden - mühendislik özelliği
Merhaba eğitim verilerini her biri bir dizi özellik (değişkenleri veya sütunlarında depolanan alanları) sahip örnekleri (kayıtları veya satır depolanan gözlemleri) oluşan bir matris oluşur. Merhaba Deneysel tasarımında belirtilen hello hello veri beklenen toocharacterize hello düzenleri özellikleridir. Merhaba ham verileri alanları doğrudan eklenebilir çoğunu seçilen özelliği kullanılan kümesini tootrain bir model Merhaba, genellikle hello ham verileri toogenerate geliştirilmiş hello özelliklerinden oluşturulan toobe ek (tasarlanan) özelliklerine ihtiyaç hello durumda olsa da Eğitim veri kümesi.

Ne tür bir özellikler tooenhance hello dataset bir modeli eğitimindeki oluşturulsun mu? Merhaba eğitim geliştirmek tasarlanan özellikleri daha iyi hello veri hello düzenleri ayıran bilgi sağlar. Açıkça yakalanan veya kolayca görünen hello özgün veya var olan özellik kümesi olup olmadığını hello yeni özellikler tooprovide ek bilgileri bekliyoruz. Ancak bu işlem bir resimler bir şeydir. Ses ve üretken kararları genellikle bazı etki alanı uzmanlık gerektirir.

Azure Machine Learning ile başlayan concretely örnekleri kullanarak bu işlemi hello Studio sağlanan kolay toograsp olur. İki örnek burada sunulur:

* Regresyon örnek [bisiklet kiralamaları hello sayısını tahmin](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4) hello hedef değerleri nerede bilinir denetimli bir deney olarak
* Bir metin araştırma sınıflandırma örneği kullanarak [özellik karma](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/)

## <a name="example-1-adding-temporal-features-for-regression-model"></a>Örnek 1: Zamana bağlı özellikler için regresyon modeli ekleme
Hello deneme "isteğe bağlı bisiklet tahmin" Azure Machine Learning Studio toodemonstrate nasıl tooengineer özellikleri için bir regresyon görev kullanalım. Bu deneme Hello amacı toopredict hello hello bisiklet, diğer bir deyişle, hello sayısı belirli bir ay/gün/saati içinde bisiklet kiralama olanağı için taleptir. veri kümesi hello "bisiklet kiralama UCI dataset" Merhaba ham girdi verisi olarak kullanılır. Bu veri kümesi hello Washington DC bisiklet kiralama ağında hello Amerika Birleşik Devletleri içinde tutar sermaye Bikeshare şirket gerçek verileri temel alır. Merhaba dataset hello yıllarda 2011 ve yıl 2012 günün belirli bir saat içinde bisiklet kiralamaları hello sayısını temsil eder ve 17379 satırları ve 17 sütunları içerir. Merhaba ham özellik kümesi (nem/sıcaklık/Rüzgar hızı) hava koşulları ve hello gün (tatil/hafta içi günü) hello türünü içerir. Merhaba alan toopredict "cnt", belirli bir saat içinde hello bisiklet kiralamaları temsil eden ve hangi 1 too977 aralığından aralıkları sayısı ' dir.

Merhaba eğitim verileri etkin özellikleri oluşturma hello amacı ile dört regresyon modeli hello kullanılarak oluşturulan aynı algoritmanın ancak dört farklı eğitim veri kümeleri ile. Hello dört veri kümeleri temsil aynı ham giriş verisi Merhaba, ancak özellikleri artan sayıda ile ayarlayın. Bu özellikler, dört kategorilerde gruplanır:

1. A = hava durumu, tatil + haftanın günü + hafta özellikleri hello tahmin edilen gün için
2. B = her hello önceki 12 saat rented bisiklet sayısı
3. C = her hello hello önceki 12 günde aynı rented bisiklet sayısı saat
4. D = her hello hello adresindeki önceki 12 hafta aynı rented bisiklet sayısı saat ve hello aynı gün

Merhaba özgün ham verileri zaten, özellik kümesi A yanı sıra, hello diğer üç özellik kümesi işlemi mühendislik hello özelliği kullanılarak oluşturulur. Özellik B yakalamaları hello bisiklet için çok yeni talep ayarlayın. Özellik C yakalamaları hello talep bisiklet için belirli bir saatte ayarlayın. Özellik D yakalamaları talep bisiklet için belirli saat ve belirli hello haftanın günü ayarlayın. Merhaba dört eğitim veri kümeleri her içeren özellik kümesi A, A + B, A + B + C ve A + B + C + D, sırasıyla.

Hello Azure Machine Learning deneme, dört dalları hello önceden işlenen giriş kümesinden aracılığıyla bu dört eğitim veri kümeleri oluşturulur. Sol çoğu şube hello dışında her bu dallar içeren bir [R betiği yürütün](https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/) türetilen özellikler (özellik kümesinin B, C ve D) kümesini içeri sırasıyla oluşturulan ve eklenmiş toohello dataset olan modülü. Aşağıdaki şekilde hello hello R betiği toocreate özellik kümesi B hello ikinci sol dalında kullandığınız gösterir.

![özellikleri oluşturma](./media/machine-learning-data-science-create-features/addFeature-Rscripts.png)

Merhaba hello performans sonuçları hello dört modellerin karşılaştırması aşağıdaki tablonun hello özetlenir. Merhaba en iyi sonuçlar özellikleri tarafından A + B + C gösterilmektedir. Ek özellik kümesi eklenir, hello eğitim verileri içinde hata oranı düşüşleri hello unutmayın. Merhaba özellik kümesi B, C sağlamasını hello regresyon görev için ek ilgili bilgileri bizim presumption doğrular. Ancak ekleme hello D özelliği hello hata oranı, ek herhangi azalma tooprovide görünmüyor.

![Sonuç karşılaştırma](./media/machine-learning-data-science-create-features/result1.png)

## <a name="example2"></a>Örnek 2: Özellikleri metin araştırma oluşturma
Özellik Mühendisliği yaygın görevleri ilgili tootext, belge sınıflandırma ve düşünceleri analiz gibi araştırma içinde uygulanır. Tooclassify belgeleri birkaç kategoride istediğinizde örneğin, tipik bir varsayım hello word/tümcecikleri bir belge kategoride yer alan başka bir belge kategoride olasılığını toooccur olmasıdır. Başka bir sözcükleri hello hello sözcükler/tümcecikleri dağıtım mümkün toocharacterize farklı Belge kategorileri sıklığıdır. Metin içeriği tek tek parçaları genellikle hello girdi verisi olarak gördükleri için metin araştırma uygulamalarda işlem mühendislik hello sözcük/tümcecik sıklıklarını içeren gerekli toocreate hello özellikleri özelliğidir.

tooachieve bu görev, adında bir teknik **özellik karma** uygulanan tooefficiently dizinlerini Aç rastgele metin özelliklerini olduğu. Her metin (sözcük/tümceleri) özellik tooa belirli dizini, karma işlevi toohello Özellikler uygulama ve karma değerlerini dizinlerini doğrudan kullanarak bu yöntem işlevleri ilişkilendirme yerine.

Azure Machine Learning ile var olan bir [özellik karma](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/) bunlar oluşturur modülü sözcük/tümcecik özelliklerini kolayca. Aşağıdaki şekilde bu modülü kullanmanın bir örneği gösterilmektedir. Merhaba girdi veri kümesi, iki sütunları içerir: Merhaba 1 too5 arasında değişen kitap derecelendirme ve hello gerçek gözden geçirme içeriği. Bu Hello amacı [özellik karma](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/) modülü tooretrieve hello oluşumu sözcükler karşılık gelen hello sıklığını Göster yeni özelliklerin bir grup veya phrase(s) içinde hello belirli kitap gözden geçirin. toouse bu modül ihtiyacımız aşağıdaki adımları toocomplete hello:

* İlk olarak, hello giriş metni içeren hello sütunu seçin (Bu örnekte "Col2").
* İkinci olarak, 2 anlamı hello "Hashing bitsize" too8'ı ayarlamak ^ 8 = 256 özellikleri oluşturulacak. Hello word/aşamasında tüm hello metin karma too256 dizinlerini olacaktır. Merhaba parametresi "Hashing bitsize" 1 too31 aralıkları. Merhaba sözcükler / phrase(s) aynı dizin toobe daha büyük bir sayı ayarlıyorsanız hello karma olasılığını toobe.
* Üçüncü hello parametresi "N-gram" too2 ayarlayın. Bu, hello giriş metinden hello oluşumu sıklığı unigrams (özelliği her tek word için) ve bigrams (bitişik sözcüklerin her çifti için bir özellik) alır. Merhaba parametresi "N-gram" hello en çok sıralı sözcükleri toobe sayısını gösteren 0 too10 aralığından bir özelliği dahil.  

!["Hashing özelliği" modülü](./media/machine-learning-data-science-create-features/feature-Hashing1.png)

Merhaba aşağıdaki şekilde bu hello yeni gösterilmektedir özelliği görünümlü.

!["Hashing özelliği" örnek](./media/machine-learning-data-science-create-features/feature-Hashing2.png)

## <a name="conclusion"></a>Sonuç
Tasarlanan ve seçilen özelliklerin hello tooextract hello anahtar bilgileri hello verilerde bulunan çalışır hello eğitim işlem verimliliğini artırmak. Bunlar ayrıca bu modeller tooclassify hello giriş verisi hello gücünü doğru şekilde artırmak ve toopredict sonuçlarını ilgi daha fazla yerine. Ayrıca özellik mühendislik ve seçim toomake hello öğrenme daha pkı'ya tractable birleştirebilirsiniz. Bunu geliştirme tarafından yapar ve sonra Özellikler hello sayısının azaltılması toocalibrate veya train model gerekli. Matematiksel konuşarak hello özellikleri seçili tootrain hello modeli hello veri hello düzenleri açıklayabilir ve sonuçları başarıyla tahmin bağımsız değişkenlerini en az sayıda vardır.

Bu her zaman mutlaka tooperform özellik Mühendisliği veya özellik seçimi olmadığını unutmayın. Olup olmadığını veya gerekli biz sahip veya, biz çekme, hello algoritması toplamak ve hello deneme amacı hello hello verilere bağlıdır.

