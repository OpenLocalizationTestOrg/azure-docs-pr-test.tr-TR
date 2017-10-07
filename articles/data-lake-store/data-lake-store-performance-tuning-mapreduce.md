---
title: "Data Lake Store MapReduce performans ayarlama yönergeleri aaaAzure | Microsoft Docs"
description: "Azure Data Lake Store MapReduce performans kuralları ayarlama"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: e21414a23530e65613c85156af0209c88ec54d2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-mapreduce-on-hdinsight-and-azure-data-lake-store"></a>Performans MapReduce Hdınsight ve Azure Data Lake Store için yönergeler ayarlama


## <a name="prerequisites"></a>Ön koşullar

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).
* **Bir Azure Data Lake Store hesabı**. Yönergeler için toocreate bir, bkz: [Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md)
* **Azure Hdınsight kümesi** erişim tooa Data Lake Store hesabı ile. Bkz: [Data Lake Store ile bir Hdınsight kümesi oluşturmayı](data-lake-store-hdinsight-hadoop-use-portal.md). Merhaba küme için Uzak Masaüstü etkinleştirdiğinizden emin olun.
* **MapReduce kullanarak**.  Daha fazla bilgi için bkz: [hdınsight'ta Hadoop içinde kullanım MapReduce](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-mapreduce)  
* **Performans ayarlama yönergeleri ADLS**.  Genel performans için bkz [Data Lake deposu performans rehberi ayarlama](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)  

## <a name="parameters"></a>Parametreler

MapReduce işleri çalıştırırken tooincrease performans üzerinde ADLS yapılandırabilirsiniz hello en önemli Parametreler şunlardır:

* **Mapreduce.Map.Memory.MB** – hello miktarda bellek tooallocate tooeach Eşleyici
* **Mapreduce.job.Maps** – hello harita görevleri iş başına sayısı
* **Mapreduce.reduce.Memory.MB** – bellek tooallocate tooeach reducer hello miktarı
* **Mapreduce.job.reduces** – hello Küçült görevleri iş başına sayısı

**Mapreduce.Map.Memory / Mapreduce.reduce.memory** bu sayı ne kadar bellek hello harita için gereken temel ayarlanması gereken ve/veya görev azaltın.  Merhaba varsayılan değerleri mapreduce.map.memory ve mapreduce.reduce.memory Ambari hello Yarn yapılandırma görüntülenebilir.  Ambari, tooYARN gidin ve hello yapılandırmalar sekmesini görüntüleyin.  Merhaba YARN bellek görüntülenir.  

**Mapreduce.job.Maps / Mapreduce.job.reduces** bu oluşturulan mappers veya reducers toobe hello sayısını belirler.  kaç tane mappers hello MapReduce işi için oluşturulacak bölmelerini Hello sayısını belirler.  Bu nedenle, istenen mappers hello sayısından daha az bölmelerini olup olmadığını istenenden daha az mappers alabilirsiniz.       

## <a name="guidance"></a>Rehber

**1. adım: çalışan işlerin sayısını belirlemek** -varsayılan olarak, MapReduce, işiniz için hello tüm küme kullanır.  Merhaba kümesinin daha az kullanılabilir kapsayıcıları sayısından daha az mappers kullanarak kullanabilirsiniz.  Bu belgedeki Hello bilgiler, uygulamanız kümenizde çalışan hello yalnızca uygulama olduğunu varsayar.      

**2. adım: mapreduce.map.memory/mapreduce.reduce.memory ayarlama** – hello harita hello bellek boyutu ve azaltmak görevler belirli işinizde bağımlı olacaktır.  Tooincrease eşzamanlılık istiyorsanız hello bellek boyutunu azaltabilirsiniz.  eşzamanlı olarak çalışan görevlerin sayısı hello Merhaba kapsayıcılara sayısına bağlıdır.  Merhaba Eşleyici veya reducer başına bellek miktarını azaltarak daha fazla kapsayıcıları, hangi aynı anda daha fazla mappers veya reducers toorun etkinleştirmek oluşturulabilir.  Azalan hello miktarda bellek çok fazla bellek yetersiz bazı işlemler toorun neden olabilir.  İşinizi çalıştırırken bir yığın hata alırsanız, Eşleyici veya reducer başına hello bellek artırmanız gerekir.  Daha fazla kapsayıcı ekleme ekleyeceksiniz dikkate almanız gereken potansiyel olarak performansı düşürebilir her ek kapsayıcısı için fazladan genel gider.  Başka bir tooget daha fazla bellek daha yüksek miktarlarda bellek sahip bir küme kullanarak veya hello kümenizdeki düğümlerin sayısını artırmayı alternatiftir.  Daha fazla bellek daha fazla eşzamanlılık anlamı kullanıldığında, daha fazla kapsayıcıları toobe olanak sağlar.  

**3. adım: Toplam YARN bellek belirleme** -tootune mapreduce.job.maps/mapreduce.job.reduces hello belleğin toplam YARN kullanılabilir düşünmelisiniz.  Bu bilgiler, Ambari içinde kullanılabilir.  TooYARN gidin ve hello yapılandırmalar sekmesini görüntüleyin.  Merhaba YARN bellek Bu pencerede görüntülenir.  Küme tooget hello toplam YARN bellekte hello YARN bellek düğümleri hello sayısıyla çarpın.

    Total YARN memory = nodes * YARN memory per node
Boş bir küme kullanıyorsanız, bellek, kümeniz için toplam YARN bellek hello olabilir.  Merhaba kapsayıcılara mappers veya reducers toohello sayısı sayısını azaltarak kümenizin belleğin bir kısmını tooonly kullanım seçebilirsiniz sonra bellek, diğer uygulamalar kullanıyorsanız toouse istiyor.  

**4. adım: YARN kapsayıcıları sayısını hesaplayın** – YARN kapsayıcıları dikte hello miktarını eşzamanlılık hello işi için kullanılabilir.  Toplam YARN bellek alın ve mapreduce.map.memory tarafından bölün.  

    # of YARN containers = total YARN memory / mapreduce.map.memory

**5. adım: mapreduce.job.maps/mapreduce.job.reduces ayarlama** ayarlamak mapreduce.job.maps/mapreduce.job.reduces tooat kullanılabilir kapsayıcıları en az hello sayısı.  Denemeler yapabilirsiniz daha iyi performans alırsanız mappers ve reducers toosee hello sayısını artırmayı tarafından daha fazla.  Daha fazla mappers çok fazla mappers sahip performansı düşebilir şekilde ek yükü sahip olduğunuzu göz önünde bulundurun.  

YARN kapsayıcı Hello sayısı bellek tarafından sınırlandığı için CPU zamanlama ve CPU yalıtım varsayılan olarak kapalıdır.

## <a name="example-calculation"></a>Örnek hesaplama

Diyelim ki şu anda 8 D14 düğümden oluşan bir kümeniz olduğuna ve toorun bir g/ç yoğun iş istiyor.  Yapmanız gerektiğini hello hesaplamalar şunlardır:

**1. adım: çalışan işlerin sayısını belirlemek** -Bizim örneğimizde, biz bizim işi yalnızca bir çalışan hello olduğunu varsayın.  

**2. adım: mapreduce.map.memory/mapreduce.reduce.memory ayarlama** – bizim Örneğin, bir g/ç yoğun iş çalıştırıyorsanız ve 3 GB bellek eşlemesi görevler için yeterli olacağına karar verin.

    mapreduce.map.memory = 3GB
**3. adım: Toplam YARN bellek belirleme**

    total memory from hello cluster is 8 nodes * 96GB of YARN memory for a D14 = 768GB
**4. adım: Hesaplama YARN kapsayıcıları sayısı**

    # of YARN containers = 768GB of available memory / 3 GB of memory =   256

**5. adım: mapreduce.job.maps/mapreduce.job.reduces ayarlama**

    mapreduce.map.jobs = 256

## <a name="limitations"></a>Sınırlamalar

**ADLS azaltma**

Çok kiracılı bir hizmet ADLS hesabına düzey bant genişliği sınırlarını ayarlar.  Bu sınırlar isabet durumunda toosee görev hataları başlar. Bu görev günlüklerine gözlemci azaltma hataları tanımlanabilir.  Daha fazla bant genişliği, işiniz için ihtiyacınız varsa, lütfen bizimle iletişime geçin.   

Kısıtlanan durumunda toocheck tooenable hello hata ayıklama hello istemci tarafında günlüğü gerekir. İşte nasıl bunu yapabilirsiniz:

1. PUT hello özelliği hello log4j Ambari özelliklerinde aşağıdaki > YARN > Config > yarn log4j Gelişmiş: log4j.logger.com.microsoft.azure.datalake.store=DEBUG

2. Merhaba config tootake etkisi için tüm hello düğümleri/hizmetini yeniden başlatın.

3. Kısıtlanan hello YARN günlüğü dosyasındaki hello HTTP 429 hata kodunu görürsünüz. Merhaba YARN Günlüğü dosyasıdır, içinde /tmp/&lt;kullanıcı&gt;/yarn.log

## <a name="examples-toorun"></a>Örnekler tooRun

MapReduce Azure Data Lake Store üzerinde çalışan nasıl toodemonstrate bir kümede ayarları aşağıdaki hello ile çalışan bazı örnek kod aşağıda verilmiştir:

* 16 düğüm D14v2
* Hadoop kümesi HDI 3.6 çalıştırma

Bir başlangıç noktası için bazı örnek komutları toorun MapReduce Teragen, Terasort ve Teravalidate aşağıda verilmiştir.  Bu komutlar, kaynaklara göre ayarlayabilirsiniz.

**Teragen**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 10000000000 adl://example/data/1TB-sort-input

**Terasort**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 -Dmapreduce.job.reduces=512 -Dmapreduce.reduce.memory.mb=3072 adl://example/data/1TB-sort-input adl://example/data/1TB-sort-output

**Teravalidate**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapreduce.job.maps=512 -Dmapreduce.map.memory.mb=3072 adl://example/data/1TB-sort-output adl://example/data/1TB-sort-validate
