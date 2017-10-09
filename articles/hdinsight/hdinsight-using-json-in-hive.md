---
title: "hdınsight'ta Hive aaaAnalyze ve işlem JSON belgeleri | Microsoft Docs"
description: "Nasıl toouse JSON belgeleri ve bunları analiz öğrenin hdınsight'ta Hive kullanma."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e17794e8-faae-4264-9434-67f61ea78f13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2017
ms.author: jgao
ms.openlocfilehash: b4b20172e8553f91a446615dc52f2ea2ef24cd04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a>İşlem ve hdınsight'ta Hive kullanarak JSON belgeleri analiz

Bilgi nasıl tooprocess ve hdınsight'ta Hive kullanarak JSON dosyaları çözümleyebilirsiniz. JSON belgesini aşağıdaki hello hello öğreticide kullanılır:

    {
        "StudentId": "trgfg-5454-fdfdg-4346",
        "Grade": 7,
        "StudentDetails": [
            {
                "FirstName": "Peggy",
                "LastName": "Williams",
                "YearJoined": 2012
            }
        ],
        "StudentClassCollection": [
            {
                "ClassId": "89084343",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "High",
                "Score": 93,
                "PerformedActivity": false
            },
            {
                "ClassId": "78547522",
                "ClassParticipation": "NotSatisfied",
                "ClassParticipationRank": "None",
                "Score": 74,
                "PerformedActivity": false
            },
            {
                "ClassId": "78675563",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "Low",
                "Score": 83,
                "PerformedActivity": true
            }
        ]
    }

Merhaba dosya bulunabilir wasb://processjson@hditutorialdata.blob.core.windows.net/. Hdınsight ile Azure Blob storage kullanma hakkında daha fazla bilgi için bkz: [HDFS uyumlu Azure Blob storage kullanma hdınsight'ta Hadoop ile](hdinsight-hadoop-use-blob-storage.md). Merhaba dosya toohello varsayılan kapsayıcı kümenizin kopyalayabilirsiniz.

Bu öğreticide, hello Hive konsolunu kullanın.  Merhaba Hive konsolunu açma yönergeleri için bkz: [Uzak Masaüstü kullanarak hdınsight'ta Hadoop ile Hive kullanma](hdinsight-hadoop-use-hive-remote-desktop.md).

## <a name="flatten-json-documents"></a>JSON belgeleri düzleştirmek
Merhaba sonraki bölümde listelenen hello yöntemleri hello JSON belgesi tek bir satırı gerektirir. Bu nedenle hello JSON belgesi tooa dize düzleştirmek gerekir. JSON belgenizi zaten düzleştirilmiş, bu adımı atlayın ve analiz etme JSON verilerini düz toohello sonraki bölümüne gidin.

    DROP TABLE IF EXISTS StudentsRaw;
    CREATE EXTERNAL TABLE StudentsRaw (textcol string) STORED AS TEXTFILE LOCATION "wasb://processjson@hditutorialdata.blob.core.windows.net/";

    DROP TABLE IF EXISTS StudentsOneLine;
    CREATE EXTERNAL TABLE StudentsOneLine
    (
      json_body string
    )
    STORED AS TEXTFILE LOCATION '/json/students';

    INSERT OVERWRITE TABLE StudentsOneLine
    SELECT CONCAT_WS(' ',COLLECT_LIST(textcol)) AS singlelineJSON
          FROM (SELECT INPUT__FILE__NAME,BLOCK__OFFSET__INSIDE__FILE, textcol FROM StudentsRaw DISTRIBUTE BY INPUT__FILE__NAME SORT BY BLOCK__OFFSET__INSIDE__FILE) x
          GROUP BY INPUT__FILE__NAME;

    SELECT * FROM StudentsOneLine

Merhaba ham JSON dosyası şu konumdadır  **wasb://processjson@hditutorialdata.blob.core.windows.net/** . Merhaba *StudentsRaw* Hive tablosu toohello ham düzleştirilmemiş JSON belgesini işaret eder.

Merhaba *StudentsOneLine* Hive tablosu hello Hdınsight varsayılan dosya sistemi hello altında hello veri depolayan */json/Öğrenciler/* yolu.

Merhaba INSERT deyiminin hello StudentOneLine tablo düzleştirilmiş hello JSON verileri ile doldurur.

Merhaba SELECT deyimi yalnızca bir satır geri.

Merhaba SELECT deyimi hello çıktısı şöyledir:

![Merhaba JSON belgesini düzleştirme.][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a>Hive JSON belgelerde Çözümle
Hive, JSON belgelerde toorun sorguları üç farklı mekanizma sağlar:

* Merhaba GET kullanmak\_JSON\_nesne UDF (kullanıcı tanımlı işlev)
* Merhaba JSON_TUPLE UDF kullanın
* Özel SerDe kullanın
* Python veya diğer diller kullanılarak UDF kendi yazma. Bkz: [bu makalede] [ hdinsight-python] ile Hive kendi Python kodu çalıştırma.

### <a name="use-hello-getjsonobject-udf"></a>Kullanım hello GET\_JSON_OBJECT UDF
Hive sağlar olarak adlandırılan yerleşik bir UDF [json nesnesini almak](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), hangi çalışma zamanı sırasında JSON sorgulama gerçekleştirebilir. Bu yöntem iki bağımsız değişken almayan – hello tablo adı ve sahip yöntemi adı Ayrıştırılan toobe gereken düzleştirilmiş JSON belgesi ve hello JSON alanı hello. Bu UDF nasıl çalıştığı bir örnek toosee bakalım.

Merhaba ilk ad ve Soyadı her Öğrenci için alma

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

Burada, bu sorgu konsol penceresinde çalıştırırken hello çıktı verilmiştir.

![get_json_object UDF][image-hdi-hivejson-getjsonobject]

Merhaba get-json_object birkaç sınırlamaları vardır UDF.

* Her bir alan hello sorgusunda hello sorgu yeniden ayrıştırmayı gerektirdiğinden, hello performansı etkiler.
* Alma\_JSON_OBJECT() bir dizi hello dize gösterimini döndürür. tooconvert bu dizi tooa Hive dizi kare ayraçlar hello toouse normal ifadeler tooreplace olan ' [' ve ']' ve çağrı tooget hello dizi de Böl.

Merhaba Hive wiki json_tuple kullanılmasını önerir nedeni budur.  

### <a name="use-hello-jsontuple-udf"></a>Merhaba JSON_TUPLE UDF kullanın
Hive tarafından sağlanan başka bir UDF adlı [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), gerçekleştirir daha iyi [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object). Bu yöntem, bir dizi anahtarları ve bir JSON dizesinde alır ve bir işlevini kullanarak değerlerin bir tanımlama grubu döndürür. Merhaba aşağıdaki sorguyu hello Öğrenci Kimliği ve hello düzeyde hello JSON belgesinden döndürür:

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

Bu komut dosyası hello Hive konsolunda Hello çıktısı:

![json_tuple UDF][image-hdi-hivejson-jsontuple]

JSON\_tanımlama grubu kullanır hello [yanal Görünüm](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) json verir Hive sözdiziminde\_tanımlama grubu toocreate hello UDT işlevi tooeach hello özgün tablo satırının uygulayarak sanal bir tablo.  Yinelenen hello nedeniyle kullanılması çok zor hale karmaşık JSONs YANAL görünümünü kullanın. Ayrıca, JSON_TUPLE iç içe geçmiş JSONs işleyemez.

### <a name="use-custom-serde"></a>Özel SerDe kullanın
SerDe iç içe geçmiş JSON belgelerini ayrıştırma hello en iyi seçimdir, toodefine hello JSON şeması ve kullanım hello şema tooparse hello belgeler sağlar. Bu öğreticide, birini hello kullanmanız tarafından geliştirilen diğer popüler SerDe [Roberto Congiu](https://github.com/rcongiu).

**toouse özel SerDe hello:**

1. Yükleme [Java SE Geliştirme Seti 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR). Hdınsight hello Windows Dağıtım kullanarak toobe kullanacaksanız hello X64 Windows hello JDK sürümünü seçin
   
   > [!WARNING]
   > JDK 1.8 ile bu SerDe işe yaramaz.
   > 
   > 
   
    Merhaba yükleme tamamlandıktan sonra yeni bir kullanıcı ortam değişkeni ekleyin:
   
   1. Açık **görünüm Gelişmiş Sistem ayarları** hello Windows ekranından.
   2. Tıklatın **ortam değişkenleri**.  
   3. Yeni bir ekleme **JAVA_HOME** ortam değişkeni çok işaret**C:\Program Files\Java\jdk1.7.0_55** veya yerlerde, JDK yüklenir.
      
      ![JDK için doğru yapılandırma değerleri ayarlama][image-hdi-hivejson-jdk]
2. Yükleme [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)
   
    Merhaba bin klasörü tooyour yolu Ekle tooControl Masası--> giderek düzenleme hello sistem değişkenleri hesap ortam değişkenleri için. Merhaba aşağıdaki ekran görüntüsünde, nasıl gösterir toodo bu.
   
    ![Maven ayarlama][image-hdi-hivejson-maven]
3. Kopya hello projeden [Hive JSON SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github site. Hello ekran aşağıdaki gösterildiği gibi hello "Zıp'i indir" düğmesine tıklayarak bunu yapabilirsiniz.
   
    ![Merhaba proje kopyalama][image-hdi-hivejson-serde]

4: indirdiğiniz bu paket ve ardından mvn türü "paketi" Git toohello klasör. Bu, daha sonra toohello küme kopyalayabilirsiniz gerekli jar dosyalarını hello oluşturmanız gerekir.

5: Git toohello hedef klasör hello paketi indirdiğiniz hello kök klasörü altında. Merhaba json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar dosya toohead-düğümü kümenizin karşıya yükleyin. I genellikle bu hello hive ikili klasörünün altına yerleştirin: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin veya buna benzer.

6: "jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar Ekle" Merhaba hive istemine yazın. My durumda hello C:\apps\dist\hive-0.13.x\bin klasöründe hello jar olduğundan, gösterildiği gibi hello adla hello jar doğrudan ekleyebilirim:

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![JAR tooyour projesi ekleme][image-hdi-hivejson-addjar]

Artık, hazır toouse hello SerDe toorun sorguları hello JSON belgesi bulunur.

Aşağıdaki ifadeyi hello tanımlı bir şeması ile bir tablo oluşturur:

    DROP TABLE json_table;
    CREATE EXTERNAL TABLE json_table (
      StudentId string,
      Grade int,
      StudentDetails array<struct<
          FirstName:string,
          LastName:string,
          YearJoined:int
          >
      >,
      StudentClassCollection array<struct<
          ClassId:string,
          ClassParticipation:string,
          ClassParticipationRank:string,
          Score:int,
          PerformedActivity:boolean
          >
      >
    ) ROW FORMAT SERDE 'org.openx.data.jsonserde.JsonSerDe'
    LOCATION '/json/students';

toolist hello ilk ad ve Soyadı hello öğrencinin

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

Burada, hello Hive konsolundan hello sonuç verilmiştir.

![SerDe sorgu 1][image-hdi-hivejson-serde_query1]

puanları hello JSON belgesinin toocalculate hello toplamı

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

Sorgu kullanan önceki hello [yanal görünümü Aç](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF tooexpand hello puanları dizisi böylece bunlar toplanabilir.

Merhaba hello Hive konsol çıktısı şöyledir.

![SerDe sorgu 2][image-hdi-hivejson-serde_query2]

belirli bir öğrenci konuları toofind birden fazla 80 noktaları skoru:

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

Merhaba önceki sorgunun döndürdüğü Hive dizi get aksine\_json\_nesnesinin bir dize döndürür.

![SerDe sorgu 3][image-hdi-hivejson-serde_query3]

Tooskil istiyorsanız sonra içinde anlatıldığı hello olarak hatalı biçimlendirilmiş JSON [wiki sayfa](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) bu SerDe, bu kod aşağıdaki hello yazarak elde edebilirsiniz:  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a>Özet
Conclusion, seçtiğiniz Hive JSON işlecinde hello türü, senaryoya bağlıdır. Basit bir JSON belge olması ve yalnızca bir alan toolook üzerinde çalışır duruma getirdikten – toouse hello Hive UDF get seçebilirsiniz,\_json\_nesnesi. Daha sonra birden fazla anahtar toolook varsa, json_tuple kullanabilirsiniz. İç içe geçmiş bir belgeniz varsa hello JSON SerDe kullanmanız gerekir.

## <a name="next-steps"></a>Sonraki adımlar

Diğer ilgili makaleler için bkz:

* [Hadoop ile Hive ve HiveQL Hdınsight tooanalyze bir örnek Apache log4j dosyasını kullanma](hdinsight-use-hive.md)
* [Hdınsight'ta Hive kullanarak uçuş gecikme verilerini çözümleme](hdinsight-analyze-flight-delay-data.md)
* [Twitter verilerini hdınsight'ta Hive kullanma çözümleme](hdinsight-analyze-twitter-data.md)
* [Azure Cosmos DB ile Hdınsight Hadoop işini çalıştır](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

[hdinsight-python]: hdinsight-python.md

[image-hdi-hivejson-flatten]: ./media/hdinsight-using-json-in-hive/flatten.png
[image-hdi-hivejson-getjsonobject]: ./media/hdinsight-using-json-in-hive/getjsonobject.png
[image-hdi-hivejson-jsontuple]: ./media/hdinsight-using-json-in-hive/jsontuple.png
[image-hdi-hivejson-jdk]: ./media/hdinsight-using-json-in-hive/jdk.png
[image-hdi-hivejson-maven]: ./media/hdinsight-using-json-in-hive/maven.png
[image-hdi-hivejson-serde]: ./media/hdinsight-using-json-in-hive/serde.png
[image-hdi-hivejson-addjar]: ./media/hdinsight-using-json-in-hive/addjar.png
[image-hdi-hivejson-serde_query1]: ./media/hdinsight-using-json-in-hive/serde_query1.png
[image-hdi-hivejson-serde_query2]: ./media/hdinsight-using-json-in-hive/serde_query2.png
[image-hdi-hivejson-serde_query3]: ./media/hdinsight-using-json-in-hive/serde_query3.png
[image-hdi-hivejson-serde_result]: ./media/hdinsight-using-json-in-hive/serde_result.png
