---
title: "aaaCreate Hive tabloları ve Azure Blob depolama alanından veri yükleme | Microsoft Docs"
description: "Hive tabloları oluşturma ve blob toohive tablolarındaki verileri yükleme"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a>Hive tabloları oluşturma ve Azure Blob depolama alanından veri yükleme
Bu konu, Hive tabloları oluşturma ve Azure blob depolama alanından veri yükleme genel Hive sorguları gösterir. Bazı yönergeler de Hive tablolarını bölümlendirme ve hello en iyi duruma getirilmiş satır sütunlu (ORC) biçimlendirme tooimprove sorgu performansı kullanılarak sağlanır.

Bu **menü** nasıl burada hello veri depolanabilir ve sırasında işlenen hedef ortamları tooingest verisine takım veri bilimi işlem (TDSP) hello açıklamak tootopics bağlar.

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a>Ön koşullar
Bu makalede, sahip olduğunuz varsayılmaktadır:

* Bir Azure depolama hesabı oluşturuldu. Yönergeler gerekiyorsa bkz [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md).
* Özelleştirilmiş bir Hadoop kümesine hello Hdınsight hizmeti ile sağlandı.  Yönergeler gerekiyorsa bkz [özelleştirme Azure Hdınsight Hadoop kümeleri için Gelişmiş analiz](machine-learning-data-science-customize-hadoop-cluster.md).
* Etkin uzaktan erişim toohello küme, oturum açmış ve hello Hadoop komut satırı konsolu açılır. Yönergeler gerekiyorsa bkz [erişim hello Hadoop kümesi, baş düğüm](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

## <a name="upload-data-tooazure-blob-storage"></a>Veri tooAzure blob depolama yükleme
Sağlanan hello yönergeleri izleyerek bir Azure sanal makinesi oluşturduysanız [Gelişmiş analiz için Azure sanal makinesi ayarlama](machine-learning-data-science-setup-virtual-machine.md), bu komut dosyası indirilen toohello olması gereken *C:\\ Kullanıcıların\\\<kullanıcı adı\>\\belgeleri\\veri bilimi betikleri* hello sanal makine üzerinde dizin. Bu Hive sorguları yalnızca kendi veri şeması ve Azure blob depolama hello uygun alanları toobe gönderimi için hazır yapılandırmasında takın gerektirir.

Hive tablolarını hello veri olduğunu varsayıyoruz bir **sıkıştırılmamış** tablo biçiminde ve hello verileri karşıya yüklenen toohello varsayılan (veya tooan ek) kaldırıldı hello Hadoop küme tarafından kullanılan hello depolama hesabının kapsayıcı.

Merhaba üzerinde toopractice istiyorsanız **NYC ücreti seyahat veri**, gerekir:

* **karşıdan** hello 24 [NYC ücreti seyahat veri](http://www.andresmh.com/nyctaxitrips) (12 seyahat dosyalar ve 12 ücreti dosyaları)
* **Unzip** .csv dosyalarına tüm dosyaları ve ardından
* **karşıya yükleme** bunları toohello varsayılan (veya uygun bir kapsayıcı) hello hello özetlenen hello yordamı tarafından oluşturulan Azure depolama hesabı [özelleştirme Azure Hdınsight Hadoop kümeleri Advanced Analytics işlem ve teknoloji ](machine-learning-data-science-customize-hadoop-cluster.md) konu. Bu bilgisayarda Hello işlem tooupload hello .csv dosyaları toohello varsayılan kapsayıcı hello depolama hesabında bulunabilir [sayfa](machine-learning-data-science-process-hive-walkthrough.md#upload).

## <a name="submit"></a>Nasıl toosubmit Hive sorguları
Hive sorgularını kullanarak gönderilebilir:

1. [Hadoop kümesi headnode Hive sorguları Hadoop komut satırı aracılığıyla gönderme](#headnode)
2. [Hive sorguları hello Hive Düzenleyicisi ile gönderme](#hive-editor)
3. [Azure PowerShell komutlarıyla Hive sorguları gönderme](#ps)

Hive sorguları SQL benzeri. SQL ile bilginiz varsa, hello bulabilirsiniz [Hive SQL kullanıcılar kopya sayfası](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) yararlıdır.

Bir Hive sorgusu gönderirken, ayrıca hello hedef Hive sorguları hello çıktısı, dosyada Merhaba ekranında veya tooa yerel hello baş düğüme veya tooan Azure blob olması olup olmadığını kontrol edebilirsiniz.

### <a name="headnode"></a> 1. Hadoop kümesi headnode Hive sorguları Hadoop komut satırı aracılığıyla gönderme
Sorgu doğrudan hello Hadoop küme baş düğümüne hello içinde genellikle bir Hive düzenleyicisinde veya Azure PowerShell komut dosyaları ile gönderme daha toofaster dönüş müşteri adayları gönderme karmaşık ise Hello yığını.

Toohello baş hello Hadoop küme düğümünde oturum, hello baş düğümü hello masaüstünde hello Hadoop komut satırı açın ve komutu girin `cd %hive_home%\bin`.

Üç yolu toosubmit Hive sorguları hello Hadoop komut satırı vardır:

* doğrudan
* .hql dosyalarını kullanma
* komut konsolundan ile Merhaba yığını

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a>Hive sorguları doğrudan içinde Hadoop komut satırı gönderin.
Komutu gibi çalıştırabilirsiniz `hive -e "<your hive query>;` toosubmit basit Hive sorguları doğrudan içinde Hadoop komut satırı. Burada, burada hello kırmızı kutusunu ana hatlarını hello Hive sorgusu gönderdiğinde komutu hello ve yeşil kutusu anahatları hello hello Hive sorgusu çıktısını hello bir örnek verilmiştir.

![Çalışma alanı oluşturma](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a>Hive sorguları .hql dosyalarında gönderme
Komut satırı ya da Hive komut konsolundan sorguları düzenleme, Hello Hive sorgusu daha karmaşık ve birden fazla satır olduğunda, pratik değil. Bir metin düzenleyicisi toouse hello Hadoop küme toosave hello Hive sorguları hello baş düğümü yerel bir dizine .hql dosyasında baş düğümünde hello alternatiftir. Hello Hive sorgusu hello .hql dosyasında hello kullanarak gönderilebilir sonra `-f` bağımsız değişken olarak aşağıdadır:

    hive -f "<path toohello .hql file>"

![Çalışma alanı oluşturma](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

**İlerleme durumu ekranı yazdırma Hive sorgularının gösterme**

Hive sorgusu Hadoop komutu gönderildikten sonra varsayılan olarak, hello işinin ilerleme durumunu hello harita/azaltın ekranda yazdırılır. toosuppress Merhaba hello harita/azaltın ilerleyişini ekran Yazdır, bağımsız değişken kullanabilirsiniz `-S` (büyük harflerle "S") gibi komut satırı hello:

    hive -S -f "<path toohello .hql file>"
.    -S -e hive "<Hive queries>"

#### <a name="submit-hive-queries-in-hive-command-console"></a>Hive komut konsolunda Hive sorguları göndermek.
Komutunu çalıştırarak da ilk hello Hive komut konsolundan girebilirsiniz `hive` Hadoop komut satırı ve Hive komut konsolunda Hive sorguları göndermek. Bir örnek verilmiştir. Bu örnekte, hello iki kırmızı kutuları Vurgu hello kullanılan komutlar tooenter Hive komut konsolundan hello ve Hive sorgusu Hive komut konsolunda sırasıyla gönderilen Merhaba. Merhaba yeşil kutusunu hello Hive sorgusu hello çıktısını vurgular.

![Çalışma alanı oluşturma](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

Önceki örneklerde Hello doğrudan hello Hive sorgu sonuçları ekranda çıktı. Merhaba çıktı tooa yerel dosya hello baş düğüme veya tooan Azure blob de yazabilirsiniz. Sonra diğer araçlarını kullanabilirsiniz toofurther analiz Hive sorguları hello çıktısı.

**Hive sorgusu sonuçları tooa yerel dosya çıktı.**
toooutput Hive sorgusu sonuçları tooa yerel dizin hello baş düğümünde, toosubmit hello Hive sorgusu hello Hadoop komut satırı aşağıdaki gibi vardır:

    hive -e "<hive query>" > <local path in hello head node>

Aşağıdaki örneğine hello Hive sorgusu hello çıktısını bir dosyaya yazılır `hivequeryoutput.txt` dizininde `C:\apps\temp`.

![Çalışma alanı oluşturma](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

**Hive sorgusu sonuçları tooan Azure blob çıkış**

Ayrıca hello Hive sorgusu sonuçları tooan hello varsayılan kapsayıcı hello Hadoop kümesi içindeki Azure blob çıkarabilirsiniz. Bu Hello Hive sorgusu aşağıdaki gibidir:

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

Aşağıdaki örneğine hello Hive sorgusu hello çıktısını tooa blob dizin yazılır `queryoutputdir` hello varsayılan kapsayıcı hello Hadoop kümesi içinde. Burada, yalnızca hello blob adı olmadan tooprovide hello dizin adı gerekir. Dizin ve blob adları gibi sağlarsanız, bir hata atılır `wasb:///queryoutputdir/queryoutput.txt`.

![Çalışma alanı oluşturma](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

Azure Storage Gezgini kullanarak hello Hadoop kümesi hello varsayılan kapsayıcı açarsanız, hello aşağıdaki şekilde gösterildiği gibi hello Hive sorgusu hello çıktısını görebilirsiniz. Merhaba (kırmızı kutu ile vurgulanan) filtre tooonly alma hello blob adlarındaki belirtilen harflerle uygulayabilirsiniz.

![Çalışma alanı oluşturma](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <a name="hive-editor"></a> 2. Hive sorguları hello Hive Düzenleyicisi ile gönderme
Merhaba form URL'sini girerek hello sorgu konsol (Düzenleyicisi Hive) de kullanabilirsiniz *https://&#60; Hadoop küme adı >.azurehdinsight.net/Home/HiveEditor* bir web tarayıcısı içine. Olması gerekir bu konsolu hello bakın oturum ve gereken şekilde, Hadoop küme kimlik.

### <a name="ps"></a> 3. Azure PowerShell komutlarıyla Hive sorguları gönderme
PowerShell toosubmit Hive sorguları de kullanabilirsiniz. Yönergeler için bkz: [gönderme Hive işleri PowerShell kullanarak](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).

## <a name="create-tables"></a>Hive veritabanı ve tablo oluşturma
Merhaba Hive sorguları hello paylaşılan [GitHub deposunu](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) ve buradan yüklenebilir.

Bir Hive tablosu oluşturur hello Hive sorgusu aşağıdadır.

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

Merhaba, tooplug gereken hello alanlarının açıklamaları ve diğer yapılandırmalar şunlardır:

* **&#60; veritabanı adı >**: toocreate istediğiniz hello veritabanının hello adı. Yalnızca toouse hello varsayılan veritabanı istiyorsanız, sorgu hello *veritabanı oluştur...*  atlanabilir.
* **&#60; tablo adı >**: hello belirtilen veritabanı içinde toocreate istediğiniz Merhaba tablonun hello adı. Toouse hello varsayılan veritabanı istiyorsanız hello tablo doğrudan göre başvurulabilen *&#60; tablo adı >* olmadan &#60; veritabanı adı >.
* **&#60; alan ayırıcı >**: hello veri dosyası toobe alanlarında sınırlandıran hello ayırıcı karşıya toohello Hive tablosu.
* **&#60; satır ayırıcı >**: hello veri dosyasındaki satır sınırlandıran hello ayırıcı.
* **&#60; depolama konumu >**: Azure depolama konumu toosave hello veri Hive tablolarını hello. Belirtmezseniz, *konum &#60; depolama konumu >*hello veritabanı ve hello tabloları depolanmış *hive/ambarı/* hello varsayılan kapsayıcısında hello Hive kümenin varsayılan dizin. Merhaba depolama konumu hello varsayılan kapsayıcı hello veritabanı ve tablo içindeki toobe içeriyor, bu toospecify hello depolama konumu istiyorsanız. Bu konum hello biçiminde hello kümesinin konumu göreli toohello varsayılan kapsayıcı olarak adlandırılan toobe sahip *' wasb: / / / &#60; 1 dizini > /'* veya *' wasb: / / / &#60; 1 dizini > / &#60; 2 dizini > /'*, vb.. Merhaba sorgu yürütüldükten sonra hello göreli dizinleri hello varsayılan kapsayıcı içinde oluşturulur.
* **TBLPROPERTIES("Skip.header.Line.Count"="1")**: hello veri dosyası bir başlık satırı varsa, bu özellik tooadd sahip **hello sonunda** Merhaba, *tablo oluşturma* sorgu. Aksi takdirde hello başlık satırı kayıt toohello tablo olarak yüklenir. Merhaba veri dosyası bir başlık satırı yok, bu yapılandırma hello Sorguda atlanabilir.

## <a name="load-data"></a>Yük veri tooHive tabloları
Burada, Hive tabloya veri yükler hello Hive sorgusu verilmiştir.

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* **&#60; yolu tooblob veri >**: hello blob dosya karşıya toobe toohello Hive tablosu hello varsayılan kapsayıcının hello Hdınsight Hadoop kümesi içinde ise, hello *&#60; yolu tooblob veri >* hello biçiminde olmalıdır *' wasb: / / / &#60; bu kapsayıcıda dizini > / &#60; blob dosya adı >'*. Merhaba blob dosya da hello Hdınsight Hadoop kümesi ek bir kapsayıcı olabilir. Bu durumda, *&#60; yolu tooblob veri >* hello biçiminde olmalıdır *' wasb: / / &#60; kapsayıcı adı > @&#60; depolama hesabı adı >.blob.core.windows.net/ &#60; blob dosya adı >'*.

  > [!NOTE]
  > Merhaba blob veri karşıya toobe tooHive tablosu toobe hello varsayılan veya hello depolama hesabının hello Hadoop kümesi için ek kapsayıcı vardır. Aksi takdirde hello *veri yükleme* sorgu başarısız şikayetçi hello veri erişemiyor.
  >
  >

## <a name="partition-orc"></a>Gelişmiş konular: Tablo ve Depolama yığını verileri ORC biçiminde bölümlenmiş
Merhaba veri büyükse hello tablo bölümleme yalnızca birkaç bölümleri Merhaba tablonun tooscan gerektiren sorgular için faydalıdır. Örneğin, tarih tarafından makul toopartition hello günlük verileri bir web sitesinin olabilir.

Toplama toopartitioning tabloları Hive, ayrıca yararlı toostore hello Hive verileri hello en iyi duruma getirilmiş satır sütunlu (ORC) biçiminde olur. ORC biçimlendirme daha fazla bilgi için bkz: <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">kullanarak ORC dosyaları Hive okuma, yazma ve verileri işlerken performansını artırır</a>.

### <a name="partitioned-table"></a>Bölümlenmiş bir tablo
Bölümlenmiş bir tablo oluşturur ve veri içine yükler hello Hive sorgusu aşağıdadır.

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

Bölümlenmiş tablolar sorgulanırken tooadd hello bölüm hello koşulunda önerilir **başına** Merhaba, `where` yan tümcesi bu olarak önemli ölçüde arama hello sürecinin artırır.

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <a name="orc"></a>Hive verileri ORC biçiminde depolayan
Merhaba ORC biçiminde depolanan Hive tablolara blob depolama alanından verileri doğrudan yüklenemiyor. Merhaba adımlar şunlardır tootake tooload verileri azure'dan ihtiyacınız o hello ORC biçiminde depolanan tooHive tabloları BLOB '.

Bir dış tablo oluşturma **DEPOLANAN AS TEXTFILE** ve blob depolama toohello tablodan veri yükleme.

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

Bir iç tablosu oluşturma hello ile aynı alan sınırlayıcı ve depolamak hello ile adım 1 ' hello dış tablo olarak aynı şema hello hello ORC biçiminde Hive veri.

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

1. adımda hello dış tablodan veri seçin ve hello ORC tablosuna Ekle

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> Varsa hello TEXTFILE tablo *&#60; veritabanı adı >. &#60; dış textfile tablo adı >* bölümler, adım 3'te hello içeren `SELECT * FROM <database name>.<external textfile table name>` seçer hello bölüm değişken veri kümesi hello alanında döndürülen komutu. Merhaba ekleme *&#60; veritabanı adı >. &#60; ORC tablo adı >* bu yana başarısız *&#60; veritabanı adı >. &#60; ORC tablo adı >* hello bölüm değişken olarak yok bir Merhaba tablo şemasını alanında. Bu durumda, çok eklenen toospecifically select hello alanları toobe gerek*&#60; veritabanı adı >. &#60; ORC tablo adı >* gibi:
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

Güvenli toodrop hello olan *&#60; dış textfile tablo adı >* zaman sorgu tüm veri sonra aşağıdaki hello kullanarak ekledi içine *&#60; veritabanı adı >. &#60; ORC tablo adı >*:

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

Bu yordamı tamamladıktan sonra hello ORC biçimi hazır toouse verileri içeren bir tablo olması gerekir.  
