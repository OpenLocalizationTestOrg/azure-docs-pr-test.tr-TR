---
title: "aaaClean ve Azure Machine Learning için verileri hazırlama | Microsoft Docs"
description: "Önceden işlem ve temiz veri tooprepare, machine learning için."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: bdf659ec-4881-4324-8b9c-747cbfa0c3cd
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 3e3c3e4b0cfb9187f5820d7165e6ee1ea013ba02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tasks-tooprepare-data-for-enhanced-machine-learning"></a>Gelişmiş machine learning için görevler tooprepare veri
Ön işleme ve veri temizleme dataset machine learning için etkili bir şekilde kullanılabilmesi için önce genellikle gerçekleştirilmesi gereken önemli görevlerdir. Ham verileri gürültülü ve güvenilmeyen görülür ve değerleri eksik olabilir. Bu tür veriler için modelleme kullanarak yanıltıcı sonuçlara yol açabilir. Bu görevleri hello takım veri bilimi işlem (TDSP) parçası olan ve genellikle bir veri kümesi kullanılan toodiscover ve planı hello ön işleme gereken ilk incelenmesi izleyin. Hello özetlenen hello adımları daha ayrıntılı hello TDSP işlemi hakkında yönergeler için bkz [takım veri bilimi işlemi](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

Ön işleme ve temizleme görevlerini hello veri araştırması görev gibi çok çeşitli ortamlar, SQL veya Hive veya Azure Machine Learning Studio gibi ve çeşitli araçlar ve R veya Python, verilerinizin nerede olduğuna bağlı olarak, gibi dilleri içinde gerçekleştirilebilme depolanır ve nasıl biçimlendirilir. TDSP doğası gereği yinelemeli olduğundan, bu görevleri hello iş akışında hello işleminin çeşitli adımları sırasında gerçekleşebilir.

Bu makalede, çeşitli veri işleme kavramları ve önce veya sonra Azure Machine Learning veri alma üstlendiği görevleri tanıtır.

Merhaba veri keşfi ve Azure Machine Learning studio içinde yapılan ön işleme örneği için bkz: [Azure Machine Learning Studio'da verilerin önceden işlenmesi](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/) video.

## <a name="why-pre-process-and-clean-data"></a>Neden önceden işleyebilir ve veri temizleme?
Gerçek dünya veriler çeşitli kaynaklardan toplanır ve işlemleri ve sıradışı veya bozuk veri hello dataset hello kalitesini tehlikeye içerebilir. ortaya çıkan hello tipik veri kalitesi sorunları şunlardır:

* **Tamamlanmamış**: öznitelikleri veya eksik değerler içeren veri eksik.
* **Gürültülü**: verileri hatalı kayıtları veya aykırı değerlerini içerir.
* **Tutarsız**: çakışan kayıtları veya tutarsızlıklar veri içeriyor.

Kalite veri kalitesi Tahmine dayalı modelleri için bir önkoşuldur. tooavoid "Çöp girişi, atık" ve veri kalitesini geliştirmek ve bu nedenle performans model, kesinlik temelli tooconduct veri erken sorunları ve karşılık gelen veri işleme ve adımları temizleme hello üzerinde karar bir veri sistem durumu ekran toospot değildir.

## <a name="what-are-some-typical-data-health-screens-that-are-employed"></a>Çalışan bazı tipik veri sistem durumu ekranlar nelerdir?
Biz hello genel veri kalitesi denetleyerek denetleyebilirsiniz:

* Merhaba sayısı **kayıtları**.
* Merhaba sayısı **öznitelikleri** (veya **özellikleri**).
* Merhaba özniteliği **veri türleri** (nominal, sıralı veya sürekli).
* Merhaba sayısı **eksik değerleri**.
* **Doğru biçimlendirilmiş** hello veri.
  * Merhaba veri TSV veya CSV, hello sütun ayırıcılar ve satır ayırıcı sütunları ve satırları her zaman doğru ayrı kontrol edin.
  * Merhaba veri HTML veya XML biçiminde ise hello veri doğru kendi ilgili standartlarına göre biçimlendirildiğinden olup olmadığını denetleyin.
  * Ayrıştırma de bu kadar sipariş yapılandırılmış tooextract yarı yapılandırılmış veya yapılandırılmamış veriler bilgilerinden gerekli olabilir.
* **Tutarsız veri kayıtlarını**. Değer denetimi hello aralığı izin verilir. Örneğin Öğrenci GPA, aralığı, belirlenen hello hello GPA olup olmadığını denetleyin hello veri içeriyorsa, 0 söyleyin ~ 4.

Verileri ile ilgili sorunları bulduğunuzda **işleme adımları** genellikle temizleme eksik değerleri, veri normalleştirme, ayrılma, metin işleme tooremove kapsar gerekli ve/veya etkileyebilir katıştırılmış karakterler değiştirin Veri hizalama karma veri alanları ve diğerleri ortak yazar.

**Azure Machine Learning tüketir doğru biçimlendirilmiş tablo veri**.  Merhaba veriler tablo biçiminde ise, veri ön işleme doğrudan hello Machine Learning Studio, Azure Machine Learning ile gerçekleştirilebilir.  Veriler tablo biçiminde değilse, ayrıştırma XML'de olduğu say sipariş tooconvert hello veri tootabular formunda gerekebilir.  

## <a name="what-are-some-of-hello-major-tasks-in-data-pre-processing"></a>Verileri ön işleme hello önemli görevlerden bazılarını nelerdir?
* **Veri temizleme**: doldurun veya eksik değerleri algılamak ve gürültülü veri ve aykırı değerlerini kaldırın.
* **Veri dönüştürme**: veri tooreduce boyutları ve gürültü normalleştirin.
* **Veri azaltma**: örnek veri kayıtlarını ya da daha kolay veri işleme için öznitelikler.
* **Veri ayrılma**: dönüştürme sürekli belirli machine learning yöntemleriyle kullanım kolaylığı için toocategorical öznitelikleri öznitelikleri.
* **Metin Temizleme**: Örneğin, bir sekmeyle ayrılmış veri dosyasında katıştırılmış sekmeleri katıştırılmış için kayıtları, vb. kesilebilir yeni satırlar veri uyuşmazlığın neden olabilecek katıştırılmış karakterleri kaldırın.

Aşağıdaki bölümler Hello bazı veri işleme adımlar ayrıntılı olarak açıklanmaktadır.

## <a name="how-toodeal-with-missing-values"></a>Eksik olan toodeal nasıl değerleri?
toodeal eksik değerleri ile en iyi toofirst toobetter tanıtıcı hello sorun hello eksik değerler için hello neden tanımlayın. Tipik eksik değeri işleme yöntemler şunlardır:

* **Silme**: eksik değerleri ile kayıt kaldırma
* **Kukla değiştirme**: eksik değerleri bir kukla değer ile değiştirin: Örneğin, *bilinmeyen* kategorik veya 0 için sayısal değerler için.
* **Değiştirme anlamına**: hello eksik veri sayısal ise, hello eksik değerleri hello ortalama ile değiştirin.
* **Sık kullanılan alternatifi**: hello eksik veri kategorik ise, hello eksik değerleri hello en sık rastlanan öğeyle değiştirin.
* **Regresyon değiştirme**: regresyon yöntemi tooreplace eksik değerleri gerileyen değerlerle kullanılır.  

## <a name="how-toonormalize-data"></a>Nasıl toonormalize veri?
Veri normalleştirme yeniden ölçekler sayısal değerleri tooa aralığı belirtildi. Popüler veri normalleştirme yöntemler şunlardır:

* **Min-Max normalleştirme**: doğrusal olarak dönüştürme hello veri tooa aralığı, söyleyin 0 ile 1 arasında hello burada en küçük değerdir ölçeklendirilmiş too0 ve en büyük değer too1.
* **Z-score normalleştirme**: ölçeklendirme ortalama ve standart sapma göre verileri: hello veri hello ortalaması arasındaki hello fark hello standart sapma tarafından bölün.
* **Ondalık ölçeklendirme**: hello veri taşıma hello ondalık noktası tarafından hello öznitelik değerinin ölçeklendirin.  

## <a name="how-toodiscretize-data"></a>Nasıl toodiscretize veri?
Veri sürekli değerleri toonominal öznitelikleri veya aralıkları dönüştürerek ayrılmış. Bunun yapılması bazı yöntemler şunlardır:

* **Eşit genişlikte Binning**: bir özniteliğin tüm olası değerler hello aralığı aynı boyut ve kalmıyor hello bir depo hello depo numarasıyla atayabilmeniz hello N gruplar halinde bölün.
* **Eşittir yükseklikli Binning**: bölmek hello aralığı tüm olası değerler N gruplara bir özniteliğin örnekleri aynı sayıda hello her içeren sonra Ata hello kalan hello bir depo değerlerde bin numarası.  

## <a name="how-tooreduce-data"></a>Nasıl tooreduce veri?
Daha kolay veri işleme için çeşitli yöntemler tooreduce veri boyutu vardır. Veri boyutu ve hello etki alanına bağlı olarak, yöntemler aşağıdaki hello uygulanabilir:

* **Kayıt örnekleme**: örnek hello veri kayıtlarını ve yalnızca hello temsilcisi alt hello verileri seçin.
* **Öznitelik örnekleme**: yalnızca bir alt hello en önemli özniteliklerinin hello verileri seçin.  
* **Toplama**: hello veri gruplara ayırın ve her grup için hello numaraları depolamak. Örneğin, hello hello son 20 yılda üzerinden bir restoran zincirinin numaraları oluşturulabilir günlük gelir toomonthly gelir tooreduce hello hello verilerin boyutunu bir araya getirilir.  

## <a name="how-tooclean-text-data"></a>Nasıl tooclean metin veri?
**Tablo verisi metin alanlarında** sütunları hizalama ve/veya kaydı sınırları etkileyen karakter içerebilir. Örneğin, bir sekmeyle ayrılmış dosya neden sütun uyuşmazlığın içinde sekmeleri katıştırılmış ve katıştırılmış yeni satır karakterlerini kayıt satırları bölün. Hatalı metin okunurken yazma/metin işleme kodlama giriş okunamaz karakter, örn., null değerlere ve de etkiler metni ayrıştırma yanlışlıkla tooinformation kaybına yol açar. Dikkatli ayrıştırma ve düzenleme sipariş tooclean metin alanlarında doğru hizalama ve/veya yapılandırılmamış veya yarı yapılandırılmış metin verileri yapılandırılmış tooextract verileri için gerekli olabilir.

**Veri keşfi** hello veri erken bir görünüme sunar. Veri sorunları sayısı bu adım sırasında bitişik olabilir ve karşılık gelen yöntemleri için uygulanan tooaddress bu sorunları olabilir.  Merhaba sorunu hello kaynağı nedir ve nasıl hello sorunu tanıtılmıştır gibi önemli tooask soruları olur. Bu ayrıca hello veri işleme adımları tooresolve gerçekleştirilecek bu gereksinimi toobe karar vermenize yardımcı olan bunları. bir hello verilerden tooderive oranla Öngörüler Hello tür kullanılan tooprioritize hello veri işleme çaba de olabilir.

## <a name="references"></a>Başvurular
> *Veri araştırma: Kavramlar ve teknikler*, üçüncü baskı, Morgan Kaufmann 2011, Jiawei Han, Micheline Kamber ve Jian Pei
> 
> 

