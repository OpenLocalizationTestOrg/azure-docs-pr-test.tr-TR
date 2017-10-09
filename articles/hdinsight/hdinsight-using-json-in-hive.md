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
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a><span data-ttu-id="f17a0-103">İşlem ve hdınsight'ta Hive kullanarak JSON belgeleri analiz</span><span class="sxs-lookup"><span data-stu-id="f17a0-103">Process and analyze JSON documents using Hive in HDInsight</span></span>

<span data-ttu-id="f17a0-104">Bilgi nasıl tooprocess ve hdınsight'ta Hive kullanarak JSON dosyaları çözümleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f17a0-104">Learn how tooprocess and analyze JSON files using Hive in HDInsight.</span></span> <span data-ttu-id="f17a0-105">JSON belgesini aşağıdaki hello hello öğreticide kullanılır:</span><span class="sxs-lookup"><span data-stu-id="f17a0-105">hello following JSON document is used in hello tutorial:</span></span>

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

<span data-ttu-id="f17a0-106">Merhaba dosya bulunabilir wasb://processjson@hditutorialdata.blob.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="f17a0-106">hello file can be found at wasb://processjson@hditutorialdata.blob.core.windows.net/.</span></span> <span data-ttu-id="f17a0-107">Hdınsight ile Azure Blob storage kullanma hakkında daha fazla bilgi için bkz: [HDFS uyumlu Azure Blob storage kullanma hdınsight'ta Hadoop ile](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="f17a0-107">For more information on using Azure Blob storage with HDInsight, see [Use HDFS-compatible Azure Blob storage with Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="f17a0-108">Merhaba dosya toohello varsayılan kapsayıcı kümenizin kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f17a0-108">You can copy hello file toohello default container of your cluster.</span></span>

<span data-ttu-id="f17a0-109">Bu öğreticide, hello Hive konsolunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="f17a0-109">In this tutorial, you use hello Hive console.</span></span>  <span data-ttu-id="f17a0-110">Merhaba Hive konsolunu açma yönergeleri için bkz: [Uzak Masaüstü kullanarak hdınsight'ta Hadoop ile Hive kullanma](hdinsight-hadoop-use-hive-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="f17a0-110">For instructions of opening hello Hive console, see [Use Hive with Hadoop on HDInsight with Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md).</span></span>

## <a name="flatten-json-documents"></a><span data-ttu-id="f17a0-111">JSON belgeleri düzleştirmek</span><span class="sxs-lookup"><span data-stu-id="f17a0-111">Flatten JSON documents</span></span>
<span data-ttu-id="f17a0-112">Merhaba sonraki bölümde listelenen hello yöntemleri hello JSON belgesi tek bir satırı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f17a0-112">hello methods listed in hello next section require hello JSON document in a single row.</span></span> <span data-ttu-id="f17a0-113">Bu nedenle hello JSON belgesi tooa dize düzleştirmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="f17a0-113">So you must flatten hello JSON document tooa string.</span></span> <span data-ttu-id="f17a0-114">JSON belgenizi zaten düzleştirilmiş, bu adımı atlayın ve analiz etme JSON verilerini düz toohello sonraki bölümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="f17a0-114">If your JSON document is already flattened, you can skip this step and go straight toohello next section on Analyzing JSON data.</span></span>

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

<span data-ttu-id="f17a0-115">Merhaba ham JSON dosyası şu konumdadır  **wasb://processjson@hditutorialdata.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="f17a0-115">hello raw JSON file is located at **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span></span> <span data-ttu-id="f17a0-116">Merhaba *StudentsRaw* Hive tablosu toohello ham düzleştirilmemiş JSON belgesini işaret eder.</span><span class="sxs-lookup"><span data-stu-id="f17a0-116">hello *StudentsRaw* Hive table points toohello raw unflattened JSON document.</span></span>

<span data-ttu-id="f17a0-117">Merhaba *StudentsOneLine* Hive tablosu hello Hdınsight varsayılan dosya sistemi hello altında hello veri depolayan */json/Öğrenciler/* yolu.</span><span class="sxs-lookup"><span data-stu-id="f17a0-117">hello *StudentsOneLine* Hive table stores hello data in hello HDInsight default file system under hello */json/students/* path.</span></span>

<span data-ttu-id="f17a0-118">Merhaba INSERT deyiminin hello StudentOneLine tablo düzleştirilmiş hello JSON verileri ile doldurur.</span><span class="sxs-lookup"><span data-stu-id="f17a0-118">hello INSERT statement populates hello StudentOneLine table with hello flattened JSON data.</span></span>

<span data-ttu-id="f17a0-119">Merhaba SELECT deyimi yalnızca bir satır geri.</span><span class="sxs-lookup"><span data-stu-id="f17a0-119">hello SELECT statement shall only return one row.</span></span>

<span data-ttu-id="f17a0-120">Merhaba SELECT deyimi hello çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="f17a0-120">Here is hello output of hello SELECT statement:</span></span>

![Merhaba JSON belgesini düzleştirme.][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a><span data-ttu-id="f17a0-122">Hive JSON belgelerde Çözümle</span><span class="sxs-lookup"><span data-stu-id="f17a0-122">Analyze JSON documents in Hive</span></span>
<span data-ttu-id="f17a0-123">Hive, JSON belgelerde toorun sorguları üç farklı mekanizma sağlar:</span><span class="sxs-lookup"><span data-stu-id="f17a0-123">Hive provides three different mechanisms toorun queries on JSON documents:</span></span>

* <span data-ttu-id="f17a0-124">Merhaba GET kullanmak\_JSON\_nesne UDF (kullanıcı tanımlı işlev)</span><span class="sxs-lookup"><span data-stu-id="f17a0-124">use hello GET\_JSON\_OBJECT UDF (User-defined function)</span></span>
* <span data-ttu-id="f17a0-125">Merhaba JSON_TUPLE UDF kullanın</span><span class="sxs-lookup"><span data-stu-id="f17a0-125">use hello JSON_TUPLE UDF</span></span>
* <span data-ttu-id="f17a0-126">Özel SerDe kullanın</span><span class="sxs-lookup"><span data-stu-id="f17a0-126">use custom SerDe</span></span>
* <span data-ttu-id="f17a0-127">Python veya diğer diller kullanılarak UDF kendi yazma.</span><span class="sxs-lookup"><span data-stu-id="f17a0-127">write you own UDF using Python or other languages.</span></span> <span data-ttu-id="f17a0-128">Bkz: [bu makalede] [ hdinsight-python] ile Hive kendi Python kodu çalıştırma.</span><span class="sxs-lookup"><span data-stu-id="f17a0-128">See [this article][hdinsight-python] on running your own Python code with Hive.</span></span>

### <a name="use-hello-getjsonobject-udf"></a><span data-ttu-id="f17a0-129">Kullanım hello GET\_JSON_OBJECT UDF</span><span class="sxs-lookup"><span data-stu-id="f17a0-129">Use hello GET\_JSON_OBJECT UDF</span></span>
<span data-ttu-id="f17a0-130">Hive sağlar olarak adlandırılan yerleşik bir UDF [json nesnesini almak](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), hangi çalışma zamanı sırasında JSON sorgulama gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="f17a0-130">Hive provides a built-in UDF called [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), which can perform JSON querying during run time.</span></span> <span data-ttu-id="f17a0-131">Bu yöntem iki bağımsız değişken almayan – hello tablo adı ve sahip yöntemi adı Ayrıştırılan toobe gereken düzleştirilmiş JSON belgesi ve hello JSON alanı hello.</span><span class="sxs-lookup"><span data-stu-id="f17a0-131">This method takes two arguments – hello table name and method name, which has hello flattened JSON document and hello JSON field that needs toobe parsed.</span></span> <span data-ttu-id="f17a0-132">Bu UDF nasıl çalıştığı bir örnek toosee bakalım.</span><span class="sxs-lookup"><span data-stu-id="f17a0-132">Let’s look at an example toosee how this UDF works.</span></span>

<span data-ttu-id="f17a0-133">Merhaba ilk ad ve Soyadı her Öğrenci için alma</span><span class="sxs-lookup"><span data-stu-id="f17a0-133">Get hello first name and last name for each student</span></span>

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

<span data-ttu-id="f17a0-134">Burada, bu sorgu konsol penceresinde çalıştırırken hello çıktı verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f17a0-134">Here is hello output when running this query in console window.</span></span>

![get_json_object UDF][image-hdi-hivejson-getjsonobject]

<span data-ttu-id="f17a0-136">Merhaba get-json_object birkaç sınırlamaları vardır UDF.</span><span class="sxs-lookup"><span data-stu-id="f17a0-136">There are a few limitations of hello get-json_object UDF.</span></span>

* <span data-ttu-id="f17a0-137">Her bir alan hello sorgusunda hello sorgu yeniden ayrıştırmayı gerektirdiğinden, hello performansı etkiler.</span><span class="sxs-lookup"><span data-stu-id="f17a0-137">Because each field in hello query requires reparsing hello query, it affects hello performance.</span></span>
* <span data-ttu-id="f17a0-138">Alma\_JSON_OBJECT() bir dizi hello dize gösterimini döndürür.</span><span class="sxs-lookup"><span data-stu-id="f17a0-138">GET\_JSON_OBJECT() returns hello string representation of an array.</span></span> <span data-ttu-id="f17a0-139">tooconvert bu dizi tooa Hive dizi kare ayraçlar hello toouse normal ifadeler tooreplace olan ' [' ve ']' ve çağrı tooget hello dizi de Böl.</span><span class="sxs-lookup"><span data-stu-id="f17a0-139">tooconvert this array tooa Hive array, you have toouse regular expressions tooreplace hello square brackets ‘[‘ and ‘]’ and then also call split tooget hello array.</span></span>

<span data-ttu-id="f17a0-140">Merhaba Hive wiki json_tuple kullanılmasını önerir nedeni budur.</span><span class="sxs-lookup"><span data-stu-id="f17a0-140">This is why hello Hive wiki recommends using json_tuple.</span></span>  

### <a name="use-hello-jsontuple-udf"></a><span data-ttu-id="f17a0-141">Merhaba JSON_TUPLE UDF kullanın</span><span class="sxs-lookup"><span data-stu-id="f17a0-141">Use hello JSON_TUPLE UDF</span></span>
<span data-ttu-id="f17a0-142">Hive tarafından sağlanan başka bir UDF adlı [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), gerçekleştirir daha iyi [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span><span class="sxs-lookup"><span data-stu-id="f17a0-142">Another UDF provided by Hive is called [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), which performs better than [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span></span> <span data-ttu-id="f17a0-143">Bu yöntem, bir dizi anahtarları ve bir JSON dizesinde alır ve bir işlevini kullanarak değerlerin bir tanımlama grubu döndürür.</span><span class="sxs-lookup"><span data-stu-id="f17a0-143">This method takes a set of keys and a JSON string, and returns a tuple of values using one function.</span></span> <span data-ttu-id="f17a0-144">Merhaba aşağıdaki sorguyu hello Öğrenci Kimliği ve hello düzeyde hello JSON belgesinden döndürür:</span><span class="sxs-lookup"><span data-stu-id="f17a0-144">hello following query returns hello student id and hello grade from hello JSON document:</span></span>

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

<span data-ttu-id="f17a0-145">Bu komut dosyası hello Hive konsolunda Hello çıktısı:</span><span class="sxs-lookup"><span data-stu-id="f17a0-145">hello output of this script in hello Hive console:</span></span>

![json_tuple UDF][image-hdi-hivejson-jsontuple]

<span data-ttu-id="f17a0-147">JSON\_tanımlama grubu kullanır hello [yanal Görünüm](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) json verir Hive sözdiziminde\_tanımlama grubu toocreate hello UDT işlevi tooeach hello özgün tablo satırının uygulayarak sanal bir tablo.</span><span class="sxs-lookup"><span data-stu-id="f17a0-147">JSON\_TUPLE uses hello [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntax in Hive, which allows json\_tuple toocreate a virtual table by applying hello UDT function tooeach row of hello original table.</span></span>  <span data-ttu-id="f17a0-148">Yinelenen hello nedeniyle kullanılması çok zor hale karmaşık JSONs YANAL görünümünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="f17a0-148">Complex JSONs become too unwieldy because of hello repeated use of LATERAL VIEW.</span></span> <span data-ttu-id="f17a0-149">Ayrıca, JSON_TUPLE iç içe geçmiş JSONs işleyemez.</span><span class="sxs-lookup"><span data-stu-id="f17a0-149">Furthermore, JSON_TUPLE cannot handle nested JSONs.</span></span>

### <a name="use-custom-serde"></a><span data-ttu-id="f17a0-150">Özel SerDe kullanın</span><span class="sxs-lookup"><span data-stu-id="f17a0-150">Use custom SerDe</span></span>
<span data-ttu-id="f17a0-151">SerDe iç içe geçmiş JSON belgelerini ayrıştırma hello en iyi seçimdir, toodefine hello JSON şeması ve kullanım hello şema tooparse hello belgeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="f17a0-151">SerDe is hello best choice for parsing nested JSON documents, it allows you toodefine hello JSON schema, and use hello schema tooparse hello documents.</span></span> <span data-ttu-id="f17a0-152">Bu öğreticide, birini hello kullanmanız tarafından geliştirilen diğer popüler SerDe [Roberto Congiu](https://github.com/rcongiu).</span><span class="sxs-lookup"><span data-stu-id="f17a0-152">In this tutorial, you use one of hello more popular SerDe that has been developed by [Roberto Congiu](https://github.com/rcongiu).</span></span>

<span data-ttu-id="f17a0-153">**toouse özel SerDe hello:**</span><span class="sxs-lookup"><span data-stu-id="f17a0-153">**toouse hello custom SerDe:**</span></span>

1. <span data-ttu-id="f17a0-154">Yükleme [Java SE Geliştirme Seti 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span><span class="sxs-lookup"><span data-stu-id="f17a0-154">Install [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span></span> <span data-ttu-id="f17a0-155">Hdınsight hello Windows Dağıtım kullanarak toobe kullanacaksanız hello X64 Windows hello JDK sürümünü seçin</span><span class="sxs-lookup"><span data-stu-id="f17a0-155">Choose hello Windows X64 version of hello JDK if you are going toobe using hello Windows deployment of HDInsight</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="f17a0-156">JDK 1.8 ile bu SerDe işe yaramaz.</span><span class="sxs-lookup"><span data-stu-id="f17a0-156">JDK 1.8 doesn't work with this SerDe.</span></span>
   > 
   > 
   
    <span data-ttu-id="f17a0-157">Merhaba yükleme tamamlandıktan sonra yeni bir kullanıcı ortam değişkeni ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f17a0-157">After hello installation is completed, add a new user environment variable:</span></span>
   
   1. <span data-ttu-id="f17a0-158">Açık **görünüm Gelişmiş Sistem ayarları** hello Windows ekranından.</span><span class="sxs-lookup"><span data-stu-id="f17a0-158">Open **View advanced system settings** from hello Windows screen.</span></span>
   2. <span data-ttu-id="f17a0-159">Tıklatın **ortam değişkenleri**.</span><span class="sxs-lookup"><span data-stu-id="f17a0-159">Click **Environment Variables**.</span></span>  
   3. <span data-ttu-id="f17a0-160">Yeni bir ekleme **JAVA_HOME** ortam değişkeni çok işaret**C:\Program Files\Java\jdk1.7.0_55** veya yerlerde, JDK yüklenir.</span><span class="sxs-lookup"><span data-stu-id="f17a0-160">Add a new **JAVA_HOME** environment variable is pointing too**C:\Program Files\Java\jdk1.7.0_55** or wherever your JDK is installed.</span></span>
      
      ![JDK için doğru yapılandırma değerleri ayarlama][image-hdi-hivejson-jdk]
2. <span data-ttu-id="f17a0-162">Yükleme [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span><span class="sxs-lookup"><span data-stu-id="f17a0-162">Install [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span></span>
   
    <span data-ttu-id="f17a0-163">Merhaba bin klasörü tooyour yolu Ekle tooControl Masası--> giderek düzenleme hello sistem değişkenleri hesap ortam değişkenleri için.</span><span class="sxs-lookup"><span data-stu-id="f17a0-163">Add hello bin folder tooyour path by going tooControl Panel-->Edit hello System Variables for your account Environment variables.</span></span> <span data-ttu-id="f17a0-164">Merhaba aşağıdaki ekran görüntüsünde, nasıl gösterir toodo bu.</span><span class="sxs-lookup"><span data-stu-id="f17a0-164">hello following screenshot shows you how toodo this.</span></span>
   
    ![Maven ayarlama][image-hdi-hivejson-maven]
3. <span data-ttu-id="f17a0-166">Kopya hello projeden [Hive JSON SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github site.</span><span class="sxs-lookup"><span data-stu-id="f17a0-166">Clone hello project from [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github site.</span></span> <span data-ttu-id="f17a0-167">Hello ekran aşağıdaki gösterildiği gibi hello "Zıp'i indir" düğmesine tıklayarak bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f17a0-167">You can do this by clicking on hello “Download Zip” button as shown in hello following screenshot.</span></span>
   
    ![Merhaba proje kopyalama][image-hdi-hivejson-serde]

<span data-ttu-id="f17a0-169">4: indirdiğiniz bu paket ve ardından mvn türü "paketi" Git toohello klasör.</span><span class="sxs-lookup"><span data-stu-id="f17a0-169">4: Go toohello folder where you have downloaded this package and then type “mvn package”.</span></span> <span data-ttu-id="f17a0-170">Bu, daha sonra toohello küme kopyalayabilirsiniz gerekli jar dosyalarını hello oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f17a0-170">This should create hello necessary jar files that you can then copy over toohello cluster.</span></span>

<span data-ttu-id="f17a0-171">5: Git toohello hedef klasör hello paketi indirdiğiniz hello kök klasörü altında.</span><span class="sxs-lookup"><span data-stu-id="f17a0-171">5: Go toohello target folder under hello root folder where you downloaded hello package.</span></span> <span data-ttu-id="f17a0-172">Merhaba json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar dosya toohead-düğümü kümenizin karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f17a0-172">Upload hello json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar file toohead-node of your cluster.</span></span> <span data-ttu-id="f17a0-173">I genellikle bu hello hive ikili klasörünün altına yerleştirin: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin veya buna benzer.</span><span class="sxs-lookup"><span data-stu-id="f17a0-173">I usually put it under hello hive binary folder: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin or something similar.</span></span>

<span data-ttu-id="f17a0-174">6: "jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar Ekle" Merhaba hive istemine yazın.</span><span class="sxs-lookup"><span data-stu-id="f17a0-174">6: In hello hive prompt, type “add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar”.</span></span> <span data-ttu-id="f17a0-175">My durumda hello C:\apps\dist\hive-0.13.x\bin klasöründe hello jar olduğundan, gösterildiği gibi hello adla hello jar doğrudan ekleyebilirim:</span><span class="sxs-lookup"><span data-stu-id="f17a0-175">Since in my case, hello jar is in hello C:\apps\dist\hive-0.13.x\bin folder, I can directly add hello jar with hello name as shown:</span></span>

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![JAR tooyour projesi ekleme][image-hdi-hivejson-addjar]

<span data-ttu-id="f17a0-177">Artık, hazır toouse hello SerDe toorun sorguları hello JSON belgesi bulunur.</span><span class="sxs-lookup"><span data-stu-id="f17a0-177">Now, you are ready toouse hello SerDe toorun queries against hello JSON document.</span></span>

<span data-ttu-id="f17a0-178">Aşağıdaki ifadeyi hello tanımlı bir şeması ile bir tablo oluşturur:</span><span class="sxs-lookup"><span data-stu-id="f17a0-178">hello following statement creates a table with a defined schema:</span></span>

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

<span data-ttu-id="f17a0-179">toolist hello ilk ad ve Soyadı hello öğrencinin</span><span class="sxs-lookup"><span data-stu-id="f17a0-179">toolist hello first name and last name of hello student</span></span>

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

<span data-ttu-id="f17a0-180">Burada, hello Hive konsolundan hello sonuç verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f17a0-180">Here is hello result from hello Hive console.</span></span>

![SerDe sorgu 1][image-hdi-hivejson-serde_query1]

<span data-ttu-id="f17a0-182">puanları hello JSON belgesinin toocalculate hello toplamı</span><span class="sxs-lookup"><span data-stu-id="f17a0-182">toocalculate hello sum of scores of hello JSON document</span></span>

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

<span data-ttu-id="f17a0-183">Sorgu kullanan önceki hello [yanal görünümü Aç](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF tooexpand hello puanları dizisi böylece bunlar toplanabilir.</span><span class="sxs-lookup"><span data-stu-id="f17a0-183">hello preceding query uses [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF tooexpand hello array of scores so that they can be summed.</span></span>

<span data-ttu-id="f17a0-184">Merhaba hello Hive konsol çıktısı şöyledir.</span><span class="sxs-lookup"><span data-stu-id="f17a0-184">Here is hello output from hello Hive console.</span></span>

![SerDe sorgu 2][image-hdi-hivejson-serde_query2]

<span data-ttu-id="f17a0-186">belirli bir öğrenci konuları toofind birden fazla 80 noktaları skoru:</span><span class="sxs-lookup"><span data-stu-id="f17a0-186">toofind which subjects a given student has scored more than 80 points:</span></span>

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

<span data-ttu-id="f17a0-187">Merhaba önceki sorgunun döndürdüğü Hive dizi get aksine\_json\_nesnesinin bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="f17a0-187">hello preceding query returns a Hive array unlike get\_json\_object, which returns a string.</span></span>

![SerDe sorgu 3][image-hdi-hivejson-serde_query3]

<span data-ttu-id="f17a0-189">Tooskil istiyorsanız sonra içinde anlatıldığı hello olarak hatalı biçimlendirilmiş JSON [wiki sayfa](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) bu SerDe, bu kod aşağıdaki hello yazarak elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f17a0-189">If you want tooskil malformed JSON, then as explained in hello [wiki page](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) of this SerDe you can achieve that by typing hello following code:</span></span>  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a><span data-ttu-id="f17a0-190">Özet</span><span class="sxs-lookup"><span data-stu-id="f17a0-190">Summary</span></span>
<span data-ttu-id="f17a0-191">Conclusion, seçtiğiniz Hive JSON işlecinde hello türü, senaryoya bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="f17a0-191">In conclusion, hello type of JSON operator in Hive that you choose depends on your scenario.</span></span> <span data-ttu-id="f17a0-192">Basit bir JSON belge olması ve yalnızca bir alan toolook üzerinde çalışır duruma getirdikten – toouse hello Hive UDF get seçebilirsiniz,\_json\_nesnesi.</span><span class="sxs-lookup"><span data-stu-id="f17a0-192">If you have a simple JSON document and you only have one field toolook up on – you can choose toouse hello Hive UDF get\_json\_object.</span></span> <span data-ttu-id="f17a0-193">Daha sonra birden fazla anahtar toolook varsa, json_tuple kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f17a0-193">If you have more than one key toolook up on, then you can use json_tuple.</span></span> <span data-ttu-id="f17a0-194">İç içe geçmiş bir belgeniz varsa hello JSON SerDe kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f17a0-194">If you have a nested document, then you should use hello JSON SerDe.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f17a0-195">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f17a0-195">Next steps</span></span>

<span data-ttu-id="f17a0-196">Diğer ilgili makaleler için bkz:</span><span class="sxs-lookup"><span data-stu-id="f17a0-196">For other related articles, see</span></span>

* [<span data-ttu-id="f17a0-197">Hadoop ile Hive ve HiveQL Hdınsight tooanalyze bir örnek Apache log4j dosyasını kullanma</span><span class="sxs-lookup"><span data-stu-id="f17a0-197">Use Hive and HiveQL with Hadoop in HDInsight tooanalyze a sample Apache log4j file</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="f17a0-198">Hdınsight'ta Hive kullanarak uçuş gecikme verilerini çözümleme</span><span class="sxs-lookup"><span data-stu-id="f17a0-198">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="f17a0-199">Twitter verilerini hdınsight'ta Hive kullanma çözümleme</span><span class="sxs-lookup"><span data-stu-id="f17a0-199">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="f17a0-200">Azure Cosmos DB ile Hdınsight Hadoop işini çalıştır</span><span class="sxs-lookup"><span data-stu-id="f17a0-200">Run a Hadoop job using Azure Cosmos DB and HDInsight</span></span>](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

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
