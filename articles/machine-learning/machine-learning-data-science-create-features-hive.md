---
title: "bir Hadoop kümesindeki Hive sorgularını kullanarak veri aaaCreate özellikleri | Microsoft Docs"
description: "Bir Azure Hdınsight Hadoop kümesinde depolanan verilerin özelliklerini Oluştur Hive sorguları örnekleri."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8a94c71-979b-4707-b8fd-85b47d309a30
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 686282bf0fb84ea82758d3c5b7de2bd90f0cf159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a>Hive sorgularını kullanarak bir Hadoop kümesindeki verilerin özelliklerini oluşturma
Bu belge nasıl veri toocreate özellikleri Hive sorgularını kullanarak, Azure Hdınsight Hadoop kümesi depolanan gösterir. Bu Hive sorguları katıştırılmış Hive kullanıcı tanımlı işlevler (UDF'ler) kullanmak, hello betikler kendisi için sağlanmıştır.

Merhaba gereken işlem toocreate özellikleri yoğun olabilir. Hive sorguları Hello performansını bu gibi durumlarda daha önemli hale gelir ve belirli parametreleri ayarlama tarafından geliştirilebilir. Bu parametreleri Hello ayarlama hello son bölümünde ele alınmıştır.

Sunulan hello sorguları örnekleri olan belirli toohello [NYC ücreti seyahat veri](http://chriswhong.com/open-data/foil_nyc_taxi/) senaryoları burada da sunulmaktadır [GitHub deposunu](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts). Bu sorgular zaten belirtilen veri şeması varsa ve gönderilen hazır toobe toorun. Merhaba son bölümünde, kullanıcıların ayarlayabilirsiniz ve böylece Hive sorguları hello performansı artırılabilir parametreleri de ele alınmıştır.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Bu **menü** nasıl toocreate çeşitli ortamlarda veri özellikleri açıklamak tootopics bağlar. Bu görev bir hello adımdır [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="prerequisites"></a>Ön koşullar
Bu makalede, sahip olduğunuz varsayılmaktadır:

* Bir Azure depolama hesabı oluşturuldu. Yönergeler gerekiyorsa bkz [bir Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Özelleştirilmiş bir Hadoop kümesine hello Hdınsight hizmeti ile sağlandı.  Yönergeler gerekiyorsa bkz [Advanced Analytics için Azure Hdınsight Hadoop kümeleri özelleştirme](machine-learning-data-science-customize-hadoop-cluster.md).
* Merhaba veri Azure Hdınsight Hadoop kümeleri karşıya yüklenen tooHive tablolarda olmuştur. Bunu henüz yoksa, lütfen izleyin [oluşturma ve yük veri tooHive tabloları](machine-learning-data-science-move-hive-tables.md) tooupload veri tooHive tabloları ilk.
* Uzaktan erişim toohello küme etkin. Yönergeler gerekiyorsa bkz [erişim hello Hadoop kümesi, baş düğüm](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

## <a name="hive-featureengineering"></a>Özellik oluşturma
Bu bölümde, hangi özellikler Hive sorguları oluşturarak hello yolları bazı örnekleri açıklanmaktadır. Ek özellikler oluşturduktan sonra sütunları toohello var olan tablo olarak ekleyin veya hello ek özellikler ve ardından hello özgün tabloyla katılabilir birincil anahtarı ile yeni bir tablo oluşturun. Sunulan hello örnekler şunlardır:

1. [Özellik oluşturma sıklığı alarak](#hive-frequencyfeature)
2. [İkili sınıflandırma kategorik değişkenlerin riskleri](#hive-riskfeature)
3. [Datetime alanından özellikleri Ayıkla](#hive-datefeatures)
4. [Metin alanından özellikleri Ayıkla](#hive-textfeatures)
5. [GPS koordinatları arasındaki uzaklığı Hesapla](#hive-gpsdistance)

### <a name="hive-frequencyfeature"></a>Özellik oluşturma sıklığı alarak
Genellikle, yararlı toocalculate hello sıklıkları hello düzeyleri Kategorik bir değişkenin veya birden çok kategorik değişkenleri düzeylerinden belirli birleşimlerini hello sıklıkları olur. Kullanıcılar bu sıklıklarını betik toocalculate aşağıdaki hello kullanabilirsiniz:

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <a name="hive-riskfeature"></a>İkili sınıflandırma kategorik değişkenlerin riskleri
Yalnızca kullanılan hello modelleri sayısal özellikleri zaman ikili sınıflandırmasında tooconvert sayısal olmayan kategorik değişkenleri sayısal özelliklerini ihtiyacımız var. Bu, her bir sayısal olmayan düzeyi ile sayısal bir risk değiştirerek gerçekleştirilir. Bu bölümde, bir kategorik değişkenin hello risk değerleri (günlük büyük olasılıkla) hesaplama bazı genel Hive sorguları gösterir.

        set smooth_param1=1;
        set smooth_param2=20;
        select
            <column_name1>,<column_name2>,
            ln((sum_target+${hiveconf:smooth_param1})/(record_count-sum_target+${hiveconf:smooth_param2}-${hiveconf:smooth_param1})) as risk
        from
            (
            select
                <column_nam1>, <column_name2>, sum(binary_target) as sum_target, sum(1) as record_count
            from
                (
                select
                    <column_name1>, <column_name2>, if(target_column>0,1,0) as binary_target
                from <databasename>.<tablename>
                )a
            group by <column_name1>, <column_name2>
            )b

Bu örnekte, değişkenleri `smooth_param1` ve `smooth_param2` ayarlanmış toosmooth hello risk değerlerinin hello verilerden hesaplanır. Risk -INF INF arasındaki aralığı yok. Riskleri > 0 hello hedefleyen eşit too1 olma hello olasılığı 0,5 büyük olduğunu gösterir.

Hesaplanan Hello risk tablo sonra kullanıcılar hello risk tabloyla birleştirerek risk değerler tooa tablosu atayabilirsiniz. Merhaba Hive katılma sorgusu, önceki bölümde sağlandı.

### <a name="hive-datefeatures"></a>Datetime alanlardan özellikleri Ayıkla
Hive, datetime alanları işlemek için UDF'ler kümesiyle birlikte gelir. Kovanında, hello varsayılan tarih/saat biçimi olan ' yyyy-aa-gg 00:00:00 ' (' 1970'ten-01-01 12:21:32 ' gibi). Bu bölümde, hello gün, ay, bir datetime alanı hello month ayıklamak örnekler ve varsayılan biçim hello varsayılan biçimi tooa datetime dizesi dışında tarih saat biçiminde bir dize olarak bir dönüştürme diğer örnekleri göster.

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

Bu Hive sorgusu o hello varsayar *&#60; datetime alan >* hello varsayılan tarih/saat biçimi.

Bir datetime alanı hello varsayılan biçiminde değil, tooconvert hello datetime alanı UNIX zaman damgası önce gerekir ve ardından damga tooa datetime dize dönüştürme hello UNIX süresi hello varsayılan olarak ise biçimi. Merhaba datetime biçim varsayılan olduğunda, kullanıcılar katıştırılmış hello datetime UDF'ler tooextract özellikleri uygulayabilirsiniz.

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of hello datetime field>'))
        from <databasename>.<tablename>;

Merhaba, bu sorgu *&#60; datetime alanı >* gibi hello düzeni sahip *03/26/2015 12:04:39*, hello *' &#60; hello datetime alanı desenini >'* olmalıdır `'MM/dd/yyyy HH:mm:ss'`. tootest, kullanıcıların çalıştırabileceği

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

Merhaba *hivesampletable* hello kümeleri sağlandığında bu sorguda tüm Azure Hdınsight Hadoop kümeleri üzerinde varsayılan olarak önceden yüklenmiş olarak gelir.

### <a name="hive-textfeatures"></a>Metin alanları özellikleri Ayıkla
Merhaba Hive tablosu boşluklarla ayrılmış sözcükler dizesi içeren bir metin alanı olduğunda, hello aşağıdaki sorguyu hello dize ve sözcük hello dizesinde hello sayısını hello uzunluğu ayıklar.

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <a name="hive-gpsdistance"></a>GPS koordinat kümeleri arasındaki uzaklıkları Hesapla
Bu bölümde verilen hello sorgu doğrudan uygulanan toohello NYC ücreti seyahat veri olabilir. Bu sorgu Hello amacı tooshow nasıl tooapply katıştırılmış matematik işlevleri Hive toogenerate özellikleri.

Merhaba bu sorguda kullanılan adlı, toplama ve dropoff konumları hello GPS koordinatları alanları *toplama\_boylam*, *toplama\_enlem*,  *dropoff\_boylam*, ve *dropoff\_enlem*. Merhaba alımı ve dropoff koordinatları arasındaki hello doğrudan uzaklığı hesaplamak hello sorgular şunlardır:

        set R=3959;
        set pi=radians(180);
        select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude,
            ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
            *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
            *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
            /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
            +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
            pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
        from nyctaxi.trip
        where pickup_longitude between -90 and 0
        and pickup_latitude between 30 and 90
        and dropoff_longitude between -90 and 0
        and dropoff_latitude between 30 and 90
        limit 10;

iki GPS koordinatları arasındaki hello uzaklığı hesaplamak hello matematiksel denklemini hello üzerinde bulunabilir <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">taşınabilir tür betikleri</a> Peter Lapisu tarafından yazılan site. Kendi JavaScript'te işlevi hello `toRad()` tıpkı *lat_or_lon*pi/180 *, derece tooradians dönüştürür. Burada, *lat_or_lon* hello enlem veya boylam. Hive hello işlevi sağlamadığından `atan2`, ancak hello işlevi sağlar `atan`, hello `atan2` işlevi tarafından gerçekleştirilir `atan` sağlanan hello tanımı kullanılarak Hive sorgusu yukarıda hello işlevinde <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank"> Wikipedia</a>.

![Çalışma alanı oluşturma](./media/machine-learning-data-science-create-features-hive/atan2new.png)

Katıştırılmış UDF'ler hello bulunabilir Hive tam listesi **yerleşik işlevler** hello bölüm <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).  

## <a name="tuning"></a>Gelişmiş konular: ayarlama Hive parametreleri tooImprove sorgu hızı
Merhaba varsayılan parametre ayarları Hive kümesinin hello Hive sorguları ve hello sorguları işlerken hello veri için uygun olmayabilir. Bu bölümde, Hive sorguları hello performansını kullanıcılar ayarlayabilirsiniz bazı parametreler açıklanmaktadır. Kullanıcıların veri işleme hello sorguları önce sorguları ayarlama tooadd hello parametresi gerekir.

1. **Java yığın alanı**: büyük veri kümeleri katılma veya uzun kayıtlarının işlenmesinden içeren sorgular için **yığın alana sahip** hello sık karşılaşılan hatalardan biri. Bu parametreleri ayarlayarak ayarlanabilecek *mapreduce.map.java.opts* ve *mapreduce.task.io.sort.mb* toodesired değerleri. Örnek aşağıda verilmiştir:
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    Bu parametre, 4 GB bellek tooJava yığın alan ayırır ve ayrıca sıralama daha verimli daha fazla bellek ayırarak hale getirir. Herhangi bir işi hatası hataları ilgili tooheap alanı olduğunda iyi bir fikir tooplay Bu ayırmaları sahip olur.

1. **DFS bloğu boyutunu** : Bu parametre hello en küçük birim dosya sistemi depoları hello veri ayarlar. Hello DFS blok boyutu 128 MB ise örnek olarak, daha sonra herhangi bir veri boyutu küçüktür ve too128MB yedekleme 128 MB ek blokları ayrılan büyük veriler tek bir blok depolanır. Tooprocess toohello dosya ilgili pek çok daha fazla istekleri toofind hello ilgili blok Hello adı düğümü olduğu için çok küçük blok boyutu seçme büyük ek yüklerini Hadoop neden olur. Bir önerilen ilgilenme gigabayt ile (veya daha büyük olduğunda) ayarı veriler:
   
        set dfs.block.size=128m;
2. **Hive katılma işleminde en iyi duruma getirme** : hello eşleme ve azaltma Framework'te birleştirme işlemleri genellikle hello yerinde alırken aşamasında, bazen azaltmak, muazzam kazanç elde edilebilir ("mapjoins" olarak da bilinir) hello harita aşamasında birleştirmeler zamanlayarak. toodirect Hive toodo bu mümkün olduğunda, biz ayarlayabilirsiniz:
   
        set hive.auto.convert.join=true;
3. **Mappers tooHive Hello sayısını belirterek** : mappers hello sayısı sırada Hadoop hello kullanıcı tooset hello reducers sayısını sağlar, genellikle hello kullanıcı tarafından değil ayarlanabilir. Bu sayı denetiminde bazı derecesini veren el toochoose hello Hadoop değişkenleri olan *mapred.min.split.size* ve *mapred.max.split.size* her eşleme hello boyutu olarak görev tarafından belirlenir:
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    Genellikle, varsayılan değeri hello *mapred.min.split.size* 0 ' dır, *mapred.max.split.size* olan **Long.MAX** ve *dfs.block.size* 64 MB'tır. Verilen hello veri boyutu görebiliriz gibi "ayarlayarak" Bu parametreleri ayarlama sağlar bize tootune hello kullanılan mappers sayısı.
4. Diğer birkaç daha **Gelişmiş Seçenekler** Hive en iyi duruma getirme için performans belirtilen aşağıda. Bunlar tooset hello ayrılmış bellek toomap izin ver ve görevleri azaltır ve performans uyguladıkça yararlı olabilir. Lütfen bu hello göz önünde bulundurmanız *mapreduce.reduce.memory.mb* hello Hadoop kümedeki her alt düğümün hello fiziksel bellek boyutundan büyük olamaz.
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

