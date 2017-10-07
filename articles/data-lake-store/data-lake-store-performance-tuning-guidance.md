---
title: "Data Lake Store performans ayarlama yönergeleri aaaAzure | Microsoft Docs"
description: "Azure Data Lake Store performans ayarlama yönergeleri"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: cgronlun
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: stewu
ms.openlocfilehash: 939faa068c0f81d18d9533956f4d336bc4d0cbe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-azure-data-lake-store-for-performance"></a>Azure Data Lake Store için performans ayarlama

Data Lake Store, g/ç yoğun analizi ve veri taşıma için yüksek verimlilik destekler.  Azure Data Lake Store'da kullanılabilir tüm işleme – okunan veya saniye başına yazılan veri miktarı hello – önemli tooget hello en iyi performansı kullanmaktır.  Bu sayıda okuma gerçekleştirerek elde edilir ve mümkün olduğunca paralel yazar.

![Data Lake Store performans](./media/data-lake-store-performance-tuning-guidance/throughput.png)

Azure Data Lake Store tüm analytics senaryo için tooprovide hello gerekli işleme ölçeklendirebilirsiniz. Varsayılan olarak, bir Azure Data Lake Store hesabı toomeet hello kullanım durumlarının geniş bir kullanıcı kategorisi ihtiyaçlarını otomatik olarak yeterli verimlilik sağlar. Müşteriler hello varsayılan sınır çalıştırdığı hello durumlarda, ADLS hesabına hello yapılandırılmış tooprovide Microsoft Destek ile iletişim kurarak daha fazla verimlilik olabilir.

## <a name="data-ingestion"></a>Veri alımı

Bir kaynak sistem tooADLS verilerden alma, kaynak donanım, kaynak ağ donanım ve ağ bağlantısı tooADLS hello tooconsider hello performans sorunu olabilir önemlidir.  

![Data Lake Store performans](./media/data-lake-store-performance-tuning-guidance/bottleneck.png)

Veri taşıma hello tooensure faktörlerin tarafından etkilenmez önemlidir.

### <a name="source-hardware"></a>Kaynak donanım

Şirket içi makineler veya sanal makineleri Azure'da kullanıp kullanmadığınızı hello uygun donanım dikkatli seçmeniz gerekir. Kaynak Disk donanımı için SSD tooHDDs tercih ve daha hızlı dağılımı ile disk donanımı seçin. Kaynak ağ donanımını hello hızlı NIC'ler olası kullanın.  Azure üzerinde hello uygun şekilde güçlü disk ve ağ donanımı olan Azure D14 VM'ler öneririz.

### <a name="network-connectivity-tooazure-data-lake-store"></a>Ağ bağlantısı tooAzure Data Lake Store

veri kaynağı ile Azure Data Lake store arasında ağ bağlantısı Hello bazen hello performans sorunu olabilir. Veri kaynağınızı şirket içi olduğunda, ile ayrılmış bir bağlantı kullanmayı [Azure ExpressRoute](https://azure.microsoft.com/en-us/services/expressroute/) . Veri kaynağınızı Azure içinde ise, hello veri hello olduğunda hello performansı en iyi olacaktır hello Data Lake Store olduğu Azure bölgesinin.

### <a name="configure-data-ingestion-tools-for-maximum-parallelization"></a>Veri alımı araçları maksimum paralelleştirme için yapılandırma

Merhaba kaynak donanım ele ve ağ bağlantısı sorunlarını yukarıdaki verdikten sonra hazır tooconfigure demektir alım araçlarınızı. Merhaba aşağıdaki tabloda çeşitli popüler alım Araçlar hello anahtar ayarları özetler ve ayrıntılı performans makaleler için ayarlama sağlar.  hangi hakkında daha fazla aracı senaryonuz, toouse toolearn bu ziyaret [makale](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-data-scenarios).

| Aracı               | Ayarlar     | Daha fazla ayrıntı                                                                 |
|--------------------|------------------------------------------------------|------------------------------|
| PowerShell       | PerFileThreadCount, ConcurrentFileCount |  [Bağlantı](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-powershell#performance-guidance-while-using-powershell)   |
| AdlCopy    | Azure Data Lake Analytics birimleri  |   [Bağlantı](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob#performance-considerations-for-using-adlcopy)         |
| Distcp'yi            | -m (Eşleyici)   | [Bağlantı](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-copy-data-wasb-distcp#performance-considerations-while-using-distcp)                             |
| Azure Data Factory| parallelCopies    | [Bağlantı](../data-factory/data-factory-copy-activity-performance.md)                          |
| Sqoop           | FS.Azure.Block.size, -m (Eşleyici)    |   [Bağlantı](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/)        |

## <a name="structure-your-data-set"></a>Veri kümenizi yapısı

Data Lake Store hello dosya boyutu, veriler, dosya ve klasör yapısı sayısı bir performansı etkiler.  Merhaba aşağıdaki bölümde bu alanlarda en iyi uygulamaları açıklar.  

### <a name="file-size"></a>Dosya boyutu

Genellikle, analiz altyapıları Hdınsight ve Azure Data Lake Analytics gibi dosya başına ek yükleri vardır.  Verilerinizi kadar küçük dosyalarını depoluyorsa, bu performans olumsuz yönde etkileyebilir.  

Genel olarak, verilerinizin daha iyi performans için daha büyük boyutlu dosyalar halinde düzenleyin.  Altın kural, dosyalar 256 MB veya daha büyük veri kümelerinde düzenleyin. Görüntüleri ve ikili veriler gibi bazı durumlarda, olası tooprocess değil paralel bunları.  Bu durumlarda, tookeep tek tek dosyaların altında 2 GB önerilir.

Bazı durumlarda, veri ardışık çok sayıda küçük dosya olan hello ham veriler üzerinde denetim sınırlı.  Toohave önerilen büyük oluşturan bir "pişirme" aşağı akış uygulamaları için toouse dosyalara işlemi.  

### <a name="organizing-time-series-data-in-folders"></a>Zaman serisi veri klasörlerde düzenleme

Hive ve ADLA iş yükleri için yalnızca bir veri alt kümesini performansını artıran hello okuma bazı sorgular zaman serisi veri bölümü ayıklanmasına yardımcı olabilir.    

Zaman serisi veri alma bu ardışık düzen genellikle dosya ve klasörler için çok yapılandırılmış adlandırma ile dosyalarına yerleştirin. Biz tarihe göre yapılandırılmış veriler için bkz: çok yaygın bir örneği aşağıdadır:

    \DataSet\YYYY\MM\DD\datafile_YYYY_MM_DD.tsv

Merhaba datetime bilgi klasörler olarak hem hello filename görüntülendiğine dikkat edin.

Tarih ve saat için genel bir desen hello aşağıda verilmiştir

    \DataSet\YYYY\MM\DD\HH\mm\datafile_YYYY_MM_DD_HH_mm.tsv

Yeniden hello klasör ve dosya kuruluşla yaptığınız hello seçim hello daha büyük dosya boyutlarına ve her klasördeki dosyaları makul bir dizi iyileştirmeniz gerekir.

## <a name="optimizing-io-intensive-jobs-on-hadoop-and-spark-workloads-on-hdinsight"></a>Hdınsight'ta Hadoop ve Spark iş yükleri üzerindeki g/ç yoğun işleri en iyi duruma getirme

İşlerini aşağıdaki üç kategoride hello birine ayrılır:

* **CPU yoğun.**  Bu işleri en az g/ç sürelerinin uzun hesaplama zamanlarında vardır.  Örnek makine öğrenme ve doğal dil işleri işleme verilebilir.  
* **Yoğun bellek.**  Bu işlemler büyük miktarda bellek kullanır.  Örnek PageRank ve gerçek zamanlı analytics işleri verilebilir.  
* **G/ç yoğun.**  Bu işleri çoğu g/ç yapılması kendi zaman ayırın.  Yalnızca okuma ve yazma işlemlerinin bir kopya iş buna ortak bir örnektir.  Çok miktarda veri okuma, bazı veri dönüştürme gerçekleştirdiği veri hazırlık işleri diğer örnekler ve ardından veri geri toohello deposu yazma hello.  

yönergeleri izleyerek hello yalnızca geçerli tooI/O yoğun işler ' dir.

### <a name="general-considerations-for-an-hdinsight-cluster"></a>Hdınsight kümesi için genel konular

* **Hdınsight sürümleri.** En iyi performans için Hdınsight hello en son sürümünü kullanın.
* **Bölgeleri.** Merhaba Data Lake Store hello yerleştirin hello Hdınsight kümesi ile aynı bölgeye.  

Hdınsight kümesi iki baş düğümler ve bazı çalışan düğümleri oluşur. Her bir çalışan düğümünün belirli sayıda çekirdek ve hello VM türü tarafından belirlenir bellek sağlar.  Bir iş çalışırken YARN hello kullanılabilir bellek ve çekirdek toocreate kapsayıcıları ayırır hello kaynak uzlaştırıcı ' dir.  Her kapsayıcı hello görevleri gerekli toocomplete hello işi çalıştırır.  Kapsayıcıları paralel tooprocess görevleri hızla çalıştırın. Bu nedenle, performans mümkün olduğu kadar paralel kapsayıcılar çalıştırarak geliştirildi.

Bizi tooincrease olabilecek Hdınsight kümesi içinde üç katmanı Merhaba kapsayıcılara sayısı ve kullanılabilir tüm işleme kullanmak vardır.  

* **Fiziksel katman**
* **YARN katmanı**
* **İş yükü katmanı**

### <a name="physical-layer"></a>Fiziksel katman

**Küme, daha fazla düğüm ve/veya daha büyük boyutlu VM'ler ile çalıştırın.**  Daha büyük bir küme, toorun hello resimde gösterildiği gibi daha fazla YARN kapsayıcıları olanak sağlar.

![Data Lake Store performans](./media/data-lake-store-performance-tuning-guidance/VM.png)

**VM'ler daha fazla ağ bant genişliği ile kullanın.**  Data Lake Store verimlilik daha az ağ bant genişliği ise hello miktarda ağ bant genişliği bir performans sorunu olabilir.  Farklı sanal makineleri, ağ bant genişliği boyutları değişen sahip olur.  Merhaba en büyük olası ağ bant genişliği olan bir VM-türü seçin.

### <a name="yarn-layer"></a>YARN katmanı

**Daha küçük YARN kapsayıcıları kullanın.**  Daha fazla kapsayıcılarını hello ile her YARN kapsayıcı toocreate Hello boyutunu küçültmek aynı miktarda kaynak.

![Data Lake Store performans](./media/data-lake-store-performance-tuning-guidance/small-containers.png)

İş yükünüz bağlı olarak, her zaman olacaktır gereken en az bir YARN kapsayıcı boyutu. Çok küçük bir kapsayıcı seçerseniz, işlerinizi bellek yetersiz sorunla çalıştırın. Genellikle YARN kapsayıcıları Hayır 1 GB'den daha küçük olması gerekir. Ortak toosee 3 GB YARN kapsayıcıları olur. Bazı iş yükleri için daha büyük YARN kapsayıcıları gerekebilir.  

**YARN kapsayıcı başına çekirdek artırın.**  Merhaba tooeach kapsayıcı tooincrease hello her kapsayıcıda çalıştırılan Paralel Görevler sayısı ayrılan çekirdek sayısını artırın.  Bu, kapsayıcı başına birden çok görevi çalıştır Spark gibi uygulamalar için çalışır.  Tek bir iş parçacığı her kapsayıcısında hangi çalışma, Hive gibi uygulamalar için kapsayıcı başına daha fazla çekirdek yerine daha fazla kapsayıcı toohave daha iyi.   

### <a name="workload-layer"></a>İş yükü katmanı

**Tüm kullanılabilir kapsayıcıları kullanın.**  Görevleri toobe hello sayısı kullanılabilir kapsayıcıları hello sayısından büyük veya eşit tüm kaynakları yararlanılmıştır şekilde ayarlayın.

![Data Lake Store performans](./media/data-lake-store-performance-tuning-guidance/use-containers.png)

**Başarısız görevlerin maliyetlidir.** Her görev çok miktarda veri tooprocess varsa, bir görev hatasını içinde pahalı bir yeniden deneme sonuçlanır.  Bu nedenle, daha iyi toocreate olduğundan daha fazla görev, her biri çok küçük miktarda veri işler.

Toplama toohello genel yönergeleri'yukarıdaki her uygulamanın bu belirli bir uygulama için farklı parametreler kullanılabilir tootune vardır. Merhaba tabloda her uygulama için performans ayarlama ile başlatılan hello parametreleri ve bağlantıları tooget bazıları listelenmiştir.

| İş yükü               | Parametre tooset görevleri                                                         |
|--------------------|-------------------------------------------------------------------------------------|
| [HDInisight Spark](data-lake-store-performance-tuning-spark.md)       | <ul><li>NUM yürütücüler</li><li>Bellek içi Yürütücü</li><li>Yürütücü çekirdek</li></ul> |
| [Hdınsight'ta hive](data-lake-store-performance-tuning-hive.md)    | <ul><li>Hive.tez.Container.size</li></ul>         |
| [Hdınsight üzerinde MapReduce](data-lake-store-performance-tuning-mapreduce.md)            | <ul><li>Mapreduce.Map.Memory</li><li>Mapreduce.job.Maps</li><li>Mapreduce.reduce.Memory</li><li>Mapreduce.job.reduces</li></ul> |
| [Hdınsight üzerinde Storm](data-lake-store-performance-tuning-storm.md)| <ul><li>Çalışan işlem sayısı</li><li>Spout Yürütücü örneği sayısı</li><li>Cıvata Yürütücü örneği sayısı </li><li>Spout görev sayısı</li><li>Cıvata görev sayısı</li></ul>|

## <a name="see-also"></a>Ayrıca bkz.
* [Azure Data Lake Store'a Genel Bakış](data-lake-store-overview.md)
* [Azure Data Lake Analytics ile Çalışmaya Başlama](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
