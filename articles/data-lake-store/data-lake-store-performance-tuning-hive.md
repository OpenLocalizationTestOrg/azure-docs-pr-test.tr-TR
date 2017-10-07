---
title: "Data Lake Store Hive performans ayarlama yönergeleri aaaAzure | Microsoft Docs"
description: "Azure Data Lake Store'a Hive performans kuralları ayarlama"
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
ms.openlocfilehash: e44daeb6ad3b64e893c709df63b56444a330729f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-hive-on-hdinsight-and-azure-data-lake-store"></a>Performans Kılavuzu Hive Hdınsight ve Azure Data Lake Store için ayarlama

Merhaba varsayılan ayarları tooprovide iyi bir performans birçok farklı kullanım örnekleri arasında ayarlanmış.  G/ç yoğun sorgularında Hive bizi tooget daha iyi performans ADLS sahip olabilir.  

## <a name="prerequisites"></a>Ön koşullar

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).
* **Bir Azure Data Lake Store hesabı**. Yönergeler için toocreate bir, bkz: [Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md)
* **Azure Hdınsight kümesi** erişim tooa Data Lake Store hesabı ile. Bkz: [Data Lake Store ile bir Hdınsight kümesi oluşturmayı](data-lake-store-hdinsight-hadoop-use-portal.md). Merhaba küme için Uzak Masaüstü etkinleştirdiğinizden emin olun.
* **Hdınsight'ta Hive çalıştıran**.  Hdınsight üzerinde çalışan Hive işi hakkında toolearn bakın [Hive kullanma hdınsight'ta] (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)
* **Performans ayarlama yönergeleri ADLS**.  Genel performans için bkz [Data Lake deposu performans rehberi ayarlama](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)

## <a name="parameters"></a>Parametreler

Merhaba en önemli ayarları tootune ADLS performansı için şunlardır:

* **Hive.tez.Container.size** – hello her görevleri tarafından kullanılan bellek miktarı

* **Tez.Grouping.Min boyutu** – minimum boyutu her Eşleyici

* **Tez.Grouping.max boyutu** – maksimum boyutu her Eşleyici

* **Hive.Exec.reducer.bytes.Per.reducer** – her reducer boyutu

**Hive.tez.Container.size** -hello kapsayıcı boyutu belirler her görev için ne kadar kullanılabilir bellek yok.  Merhaba ana giriş denetleme hello eşzamanlılık kovanında için budur.  

**Tez.Grouping.Min boyutu** – Bu parametre, tooset hello en küçük boyut her Eşleyici sağlar.  Tez seçer mappers Hello sayısı bu parametre, başlangıç değerinden daha küçükse, Tez Burada ayarlanan hello değeri kullanır.  

**Tez.Grouping.max boyutu** – hello parametresi, tooset hello en büyük boyutu her Eşleyici verir.  Tez seçer mappers Hello sayısı bu parametre, başlangıç değerinden büyük olursa, Tez Burada ayarlanan hello değeri kullanır.  

**Hive.Exec.reducer.bytes.Per.reducer** – Bu parametre her reducer hello boyutunu ayarlar.  Varsayılan olarak, her reducer 256 MB'tır.  

## <a name="guidance"></a>Rehber

**Hive.Exec.reducer.bytes.Per.reducer ayarlamak** – hello veri sıkıştırılmamış olduğunda hello varsayılan değer iyi çalışır.  Sıkıştırılmış veri hello reducer hello boyutunu azaltmanız gerekir.  

**Hive.tez.Container.size ayarlamak** – her bir düğümündeki bellek yarn.nodemanager.resource.memory mb belirtilir ve HDI kümesi üzerinde varsayılan olarak doğru bir şekilde ayarlamanız gerekir.  YARN içinde hello uygun bellek ayarlama hakkında ek bilgi için bkz [sonrası](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom).

G/ç yoğun iş yükleri hello Tez kapsayıcı boyutu azaltarak daha fazla paralellik yararlı olabilir. Bu hello kullanıcı eşzamanlılık artıran daha fazla kapsayıcı sağlar.  Ancak, bazı Hive sorguları önemli miktarda belleği (örneğin MapJoin) gerektirir.  Merhaba görev yeterli belleğe sahip değil bir yetersiz bellek özel durumu çalışma zamanı sırasında alırsınız.  Yetersiz bellek özel durumları alırsanız, hello bellek artırmanız gerekir.   

çalışan görevler veya paralellik eşzamanlı sayısını Hello hello toplam YARN bellek tarafından sınırlanmış.  YARN kapsayıcı Hello sayısı, kaç tane eş zamanlı görevleri çalıştırabilir benimsendiği belirler.  Düğüm başına toofind hello YARN bellek, tooAmbari gidebilirsiniz.  TooYARN gidin ve hello yapılandırmalar sekmesini görüntüleyin.  Merhaba YARN bellek Bu pencerede görüntülenir.  

        Total YARN memory = nodes * YARN memory per node
        # of YARN containers = Total YARN memory / Tez container size
ADLS kullanarak hello anahtar tooimproving performansını tooincrease hello eşzamanlılık mümkün olduğunca ' dir.  Tez tooset gerek yoktur, oluşturulması gereken görevlerin hello sayısını otomatik olarak hesaplar.   

## <a name="example-calculation"></a>Örnek hesaplama

Bir 8 düğüm D14 küme sahip varsayalım.  

    Total YARN memory = nodes * YARN memory per node
    Total YARN memory = 8 nodes * 96GB = 768GB
    # of YARN containers = 768GB / 3072MB = 256

## <a name="limitations"></a>Sınırlamalar
**ADLS azaltma** 

ADLS tarafından toosee görev hataları başlarsınız sağlanan hello isabet UIf bant genişliği sınırlar. Bu görev günlükleri gözlemci azaltma hatalar nedeniyle tanımlanamadı.  Tez kapsayıcı boyutu artırarak hello paralellik düşürebilir.  Daha fazla eşzamanlılık işiniz için ihtiyacınız varsa, lütfen bizimle iletişime geçin.   

Kısıtlanan durumunda toocheck tooenable hello hata ayıklama hello istemci tarafında günlüğü gerekir. İşte nasıl bunu yapabilirsiniz:

1. Merhaba log4j Hive yapılandırma özelliklerinde bir özellik aşağıdaki hello yerleştirin. Bu Ambari görünümünden yapılabilir: log4j.logger.com.microsoft.azure.datalake.store=DEBUG hello config tootake efekti için tüm hello düğümleri/hizmetini yeniden başlatın.

2. Kısıtlanan hello HTTP 429 hata kodunu hello hive günlük dosyasında görürsünüz. Merhaba hive günlük dosyası, içinde /tmp/&lt;kullanıcı&gt;/hive.log

## <a name="further-information-on-hive-tuning"></a>Hive ayarlama hakkında daha fazla bilgi

Hive sorgularınızı ince ayar yardımcı olacak birkaç Web günlükleri şunlardır:
* [Hdınsight'ta Hadoop için Hive sorguları en iyi duruma getirme](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-optimize-hive-query/)
* [Hive sorgusu performans sorunlarını giderme](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/)
* [Konuşma göz atın üzerinde hdınsight'ta Hive en iyi duruma getirme](https://channel9.msdn.com/events/Machine-Learning-and-Data-Sciences-Conference/Data-Science-Summit-2016/MSDSS25)
