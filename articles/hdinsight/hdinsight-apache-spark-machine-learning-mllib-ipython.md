---
title: "hdınsight'ta - Azure Spark Mllib'i örnekle öğrenme aaaMachine | Microsoft Docs"
description: "Bilgi nasıl toouse Spark Mllib'i toocreate Lojistik regresyon aracılığıyla sınıflandırmasını kullanan bir veri kümesi analiz bir makine öğrenme uygulaması."
keywords: "spark machine Learning, spark machine learning örneği"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c0fd4baa-946d-4e03-ad2c-a03491bd90c8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 5c3b83482de5d8fba224398aaafe07fa67ec1fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-mllib-toobuild-a-machine-learning-application-and-analyze-a-dataset"></a>Machine learning uygulama Spark Mllib'i toobuild kullanın ve bir veri kümesi analiz

Bilgi nasıl toouse Spark **Mllib'i** toocreate uygulama toodo basit Tahmine dayalı analiz açık bir veri kümesi üzerinde öğrenme makine. Bu örnek kitaplıkları öğrenme Spark'ın yerleşik makineden kullanır *sınıflandırma* Lojistik regresyon aracılığıyla. 

> [!TIP]
> Bu örnek, Hdınsight'ta oluşturma (Linux) Spark kümesinde Jupyter not defteri olarak da kullanılabilir. Merhaba not defteri deneyimi hello Python parçacıkları hello dizüstü bilgisayarınızı kendisini çalıştırmadan olanak sağlar. bir not defteri içinde toofollow hello öğretici bir Spark kümesi ve başlatma Jupyter not defteri oluşturma (`https://CLUSTERNAME.azurehdinsight.net/jupyter`). Daha sonra hello dizüstü çalıştırın **Spark Machine Learning - yemek İnceleme verileri MLlib.ipynb kullanarak Tahmine dayalı analiz** hello altında **Python** klasör.
>
>

Mllib'i makine öğrenimi görevlerini uygun yardımcı programlar da dahil olmak üzere, birçok yardımcı programını yararlı sağlayan bir çekirdek Spark kitaplığıdır:

* Sınıflandırma
* regresyon
* Kümeleme
* Konu modelleme
* Tekil değer ayrıştırma (SVD) ve asıl bileşen çözümlemesi (PCA)
* Test etme ve örnek istatistikleri hesaplama varsayımınızın

## <a name="what-are-classification-and-logistic-regression"></a>Sınıflandırma ve lojistik regresyon nelerdir?
*Sınıflandırma*, görev, öğrenme popüler bir makine kategoriye giriş verileri sıralama hello işlemidir. Bu, sınıflandırma algoritması toofigure nasıl tooassign "sağladığınız tooinput veri etiketler" Merhaba iş olur. Örneğin, giriş olarak hisse bilgilerini kabul eden bir makine öğrenme algoritmasını düşünüyorsunuz ve böler iki kategoride hisse senedi hello: satmak stoklar ve hisse tutmanız gerekir.

Lojistik regresyon sınıflandırma için kullandığınız hello algoritmasıdır. Spark'ın Lojistik regresyon API için yararlıdır *ikili sınıflandırma*, veya iki gruplarının biri giriş verileri sınıflandırmaya. Lojistik gerileme hakkında daha fazla bilgi için bkz: [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).

Özet olarak, lojistik regresyon hello işlemi üreten bir *Lojistik işlevi* kullanılan toopredict hello olasılık bir giriş vektörü bir grup veya hello diğer ait olabilir.  

## <a name="predictive-analysis-example-on-food-inspection-data"></a>Tahmine dayalı analiz örnek yemek İnceleme verileri
Bu örnekte, Spark tooperform bazı Tahmine dayalı analiz yemek İnceleme verileri kullandığınız (**Food_Inspections1.csv**) hello elde [Şehir, Chicago veri portalı](https://data.cityofchicago.org/). Bu veri kümesi her kurma hakkında bilgiler dahil olmak üzere Chicago'da gerçekleştirildi yemek kurma incelemeleri hakkında bilgi içerir, hello ihlalleri (varsa) bulunan ve hello İnceleme sonuçlarını hello. Merhaba CSV veri dosyası kullanılabilir zaten hello kümesine ilişkili hello depolama hesabındaki **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.

Merhaba adımları, model toosee toopass neler geliştirmek veya yemek İnceleme başarısız.

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a>Spark MMLib machine learning uygulama oluşturmaya başlayın
1. Merhaba gelen [Azure portal](https://portal.azure.com/), (, onu toohello Sabitle) hello Panosu'ndan hello kutucuğuna Spark kümenizin tıklayın. Tooyour küme altında da gidebilirsiniz **tümüne Gözat** > **Hdınsight kümeleri**.   
1. Merhaba Spark kümesi dikey penceresinden tıklatın **küme Panosu**ve ardından **Jupyter not defteri**. İstenirse, hello küme için hello yönetici kimlik bilgilerini girin.

   > [!NOTE]
   > Kümenizin açma hello tarayıcınızda URL aşağıdaki tarafından hello Jupyter Not Defteri de ulaşabilir. Değiştir **CLUSTERNAME** kümenizi hello adı:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. Bir not defteri oluşturun. **Yeni** ve ardından **PySpark** seçeneğine tıklayın.

    ![Jupyter not defteri oluşturma](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "yeni bir Jupyter not defteri oluşturma")
1. Yeni bir not defteri oluşturulur ve Untitled.pynb hello adı ile. Merhaba üstünde Hello dizüstü bilgisayar adına tıklayın ve kolay bir ad girin.

    ![Merhaba dizüstü bilgisayar için bir ad](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "hello dizüstü bilgisayar için bir ad sağlayın")
1. Merhaba PySpark çekirdeği kullanarak bir not defteri oluşturduğunuz için siz toocreate bir bağlam açıkça gerekmez. hello birinci kod hücresini çalıştırdığınızda hello Spark ve Hive bağlamları sizin için otomatik olarak oluşturulur. Uygulamanın bu senaryo için gerekli hello türleri içeri aktararak öğrenme makinenizi oluşturmaya başlayabilirsiniz. toodo hello hücre ve tuşuna hello imleç, yerleştirin **SHIFT + ENTER**.

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a>Bir giriş dataframe oluşturun
Biz kullanabilirsiniz `sqlContext` yapılandırılmış veri tooperform dönüşümler. Merhaba ilk görevdir tooload hello örnek verileri ((**Food_Inspections1.csv**)) bir Spark SQL içine *dataframe*.

1. Merhaba ham verileri bir CSV biçiminde olduğundan toouse hello Spark bağlam toopull her satırı hello dosyasının belleğe yapılandırılmamış metin olarak ihtiyacımız; Ardından, Python'un CSV kitaplığı tooparse her satır ayrı ayrı kullanın.

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. Şimdi hello CSV dosyası bir RDD sahibiz.  toounderstand hello şema hello veri RDD hello bir satır alıyoruz.

        inspections.take(1)

    Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [['413707',
          'LUNA PARK INC',
          'LUNA PARK  DAY CARE',
          '2049789',
          "Children's Services Facility",
          'Risk 1 (High)',
          '3250 W FOSTER AVE ',
          'CHICAGO',
          'IL',
          '60625',
          '09/21/2010',
          'License-Task Force',
          'Fail',
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of hello plumbing section of hello Municipal Code of Chicago and Rules and Regulation of hello Board of Health. OBSEVERD hello 3 COMPARTMENT SINK BACKING UP INTO hello 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding tooprotect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED tooREPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN hello REAR CHILDREN AREA,IN hello KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED tooREPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY hello 15MOS AREA. NEED tooBE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY hello EXPOSED HAND SINK IN hello KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: hello floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED tooELEVATE ALL FOOD ITEMS 6INCH OFF hello FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. Merhaba önceki çıkış bize hello giriş dosyası hello şeması hakkında bir fikir verir. Her kuruluş, kurma, başlangıç adresi, hello veri hello incelemeleri ve başka şeylerin hello konum hello türü hello adını içerir. Şimdi bizim Tahmine dayalı analiz için yararlı olan ve bir dataframe, hangi biz Grup hello sonuçları sonra toocreate geçici bir tablo kullanın birkaç sütunları seçin.

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. Şimdi sahip olduğumuz bir *dataframe*, `df` üzerinde biz gerçekleştirebilir bizim çözümleme. Ayrıca bir geçici tablo çağrı sahibiz **CountResults**. Merhaba dataframe ilgi dört sütun dahil ettiğiniz: **kimliği**, **adı**, **sonuçları**, ve **ihlalleri**.

    Şimdi hello verilerin küçük bir örnek alın:

        df.show(5)

    Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES too...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-hello-data"></a>Merhaba veri anlama
1. Tooget ne kümemize içeren bir fikir başlayalım. Örneğin, ne hello farklı hello değerler **sonuçları** sütun?

        df.select('results').distinct().show()

    Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +--------------------+
        |             results|
        +--------------------+
        |                Fail|
        |Business Not Located|
        |                Pass|
        |  Pass w/ Conditions|
        |     Out of Business|
        +--------------------+
1. Hızlı görselleştirme bize yardımcı olabilecek neden hello bu sonuçlar dağıtılması hakkında. Biz hello veriler geçici bir tablo zaten **CountResults**. Daha iyi hello sonuçları nasıl dağıtıldığını anlamak hello tablo tooget SQL sorgusunu aşağıdaki hello çalıştırabilirsiniz.

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    Merhaba `%%sql` Sihirli arkasından `-o countResultsdf` hello sorgu hello çıktısını (genellikle hello kümesinin hello headnode) hello Jupyter sunucuda yerel olarak kalıcı olmasını sağlar. Merhaba çıkış kalıcı olarak bir [Pandas](http://pandas.pydata.org/) dataframe hello ile belirtilen adı **countResultsdf**.

    Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:

    ![SQL sorgu çıktısı](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL sorgu çıktısı")

    Merhaba hakkında daha fazla bilgi için `%%sql` Sihirli ve hello PySpark çekirdeği kullanılabilen diğer sihirler bkz [Spark Hdınsight kümeleri ile Jupyter not defterlerinde kullanılabilen çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).
1. Verilerin toocreate bir çizim tooconstruct görselleştirme kitaplığı kullanılan Matplotlib de kullanabilirsiniz. Yerel olarak hello Hello çizim oluşturulması gerekir çünkü kalıcı **countResultsdf** dataframe, hello kod parçacığını hello ile başlamalıdır `%%local` Sihirli. Bu, hello kod hello Jupyter sunucusunda yerel olarak çalıştırın sağlar.

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:

    ![Spark machine learning uygulama çıktı - beş farklı İnceleme sonuçlarını içeren pasta grafik](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning sonuç çıktısı")
1. Bir inceleme olabilir 5 ayrı sonuçları olduğunu görebilirsiniz:

   * Değil bulunan iş
   * Başarısız
   * Geçişi
   * Koşulları içeren PSS
   * İş dışı

     Bize yemek inceleme, verilen hello ihlalleri hello sonucunu tahmin edebilirsiniz bir model geliştirin. Lojistik regresyon ikili sınıflandırma yöntemi olduğundan, algılama toogroup verilerimizi iki kategoride kolaylaştırır: **başarısız** ve **geçirmek**. Bir "geçirmek içeren koşullara" hala bir geçişi, biz hello modeli eğitmek, biz hello göz önünde şekilde iki eşdeğer sonuçlanır. Veri biz bizim eğitim kümesinden kaldırmak için hello ile diğer sonuçları ("İş değil bulunan" veya "İş dışı") kullanışlı değildir. Bu iki kategoriye hello sonuçları küçük bir yüzdesi yine de yapmak beri bu uygun olmalıdır.
1. Bize bir tane var olan bizim dataframe dönüştürme (`df`) burada her denetleme temsil edildiği bir etiket ihlalleri çifti olarak yeni bir dataframe içine. Bu örnekte bir etiketin `0.0` hata, bir etiketi temsil eder `1.0` başarı ve bir etiketi temsil eden `-1.0` bu iki yanı sıra bazı sonuçlarını temsil eder. Biz bu diğer sonuçlar hello yeni veri çerçevesi hesaplanırken filtreleme.

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    toosee hangi hello gibi görünüyor veri etiketli, şimdi bir satır alın.

        labeledData.take(1)

    Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of hello food establishment and all parts of hello property used in connection with hello operation of hello establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF hello FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: hello flow of air discharged from kitchen fans shall always be through a duct tooa point above hello roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT tooDINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT tooOFFICE.")]

## <a name="create-a-logistic-regression-model-from-hello-input-dataframe"></a>Merhaba giriş dataframe Lojistik regresyon modeli oluşturma
Bizim son tooconvert hello Lojistik regresyon tarafından çözümlenebilir bir biçime veri etiketli bir görevdir. Merhaba giriş tooa Lojistik regresyon algoritması, bir dizi olmalıdır *etiket özelliği vektör çiftleri*hello "özelliği vektör" hello giriş noktasını temsil eden sayı vektör eder. Bu nedenle, yarı yapılandırılmış ve bir makine kolayca anlayabileceği gerçek sayılar serbest metin, tooan dizisi birçok açıklamaları içeren tooconvert hello "ihlalleri" sütun gerekir.

İşleme doğal dil için bir standart machine learning yaklaşım tooassign her ayrı bir "dizin" sözcüktür ve sağlayacak şekilde hello göreli sıklığı hello metin sözcüğün her dizinin değerini içeren öğrenme algoritmasının bir vektör toohello makine geçirin dize.

Mllib'i kolay bir yolu tooperform bu işlemi sağlar. İlk olarak, "her ihlalleri dize tooget hello sözcükleri tek tek her dizesinde simgeleştirilecek". Ardından, bir `HashingTF` her kümesi tooconvert belirteçler geçirilen toohello Lojistik regresyon algoritması tooconstruct sonra olabilir özelliği vektör bir model. Biz bu adımların tümü "ardışık düzen" kullanılarak sırayla gerçekleştirin.

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-hello-model-on-a-separate-test-dataset"></a>Ayrı bir test veri kümesi üzerinde Hello modelini değerlendir
Daha önce oluşturduğumuz hello modeli kullanırız çok*tahmin* yeni incelemeleri sonuçlarını olacaktır, gözlenen hello ihlalleri üzerinde göre hangi hello. Biz bu model hello dataset üzerinde eğitilmiş **Food_Inspections1.csv**. Bize ikinci bir veri kümesini kullan **Food_Inspections2.csv**, çok*değerlendirmek* hello bu modeli yeni verilere gücünü. Bu ikinci veri kümesi (**Food_Inspections2.csv**) hello varsayılan depolama kapsayıcısında hello kümesi ile ilişkili olması gerekir.

1. Merhaba aşağıdaki kod parçacığında oluşturur Yeni dataframe **predictionsDf** hello modeli tarafından oluşturulan hello öngörü içerir. Merhaba parçacığı da adlı geçici bir tablo oluşturur **tahminleri** hello dataframe üzerinde temel.

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        ['id',
         'name',
         'results',
         'violations',
         'words',
         'features',
         'rawPrediction',
         'probability',
         'prediction']
1. Merhaba tahminleri birini arayın. Bu kod parçacığında çalıştırın:

        predictionsDf.take(1)

   Merhaba ilk giriş hello sınama veri kümesi için tahmini yoktur.
1. Hello `model.transform()` yöntemi hello uygular aynı dönüştürme tooany yeni verilerle hello aynı şema ve nasıl tooclassify hello verileri, bir tahmini ulaşır. Bizim tahminleri ne kadar doğru olan bir fikir bazı basit istatistikleri tooget yapabiliriz:

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    Merhaba çıktı hello aşağıdaki gibi görünür:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    Lojistik regresyon ile Spark kullanarak bize hello ilişkisinin ihlalleri açıklamaları İngilizce ve belirli bir iş veya geçirmek yemek İnceleme başarısız arasında doğru bir modeli sağlar.

## <a name="create-a-visual-representation-of-hello-prediction"></a>Görsel bir hello tahmin oluşturma
Biz, artık bize bu test hello sonuçları hakkında neden son görselleştirme toohelp oluşturabilirsiniz.

1. Merhaba farklı tahminleri çıkartarak başlatmak ve sonuçlarından hello **tahminleri** daha önce oluşturulan geçici bir tablo. Merhaba aşağıdaki sorguları ayrı hello çıkış olarak *true_positive*, *false_positive*, *true_negative*, ve *false_negative*. Merhaba sorgularda aşağıdaki biz görselleştirme kullanarak kapatmanız `-q` ve ayrıca hello çıkış kaydedin (kullanarak `-o`) ile Merhaba sonra kullanılabilir dataframes olarak `%%local` Sihirli.

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. Son olarak, aşağıdaki kod parçacığında toogenerate hello çizim kullanarak hello kullan **Matplotlib**.

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    Çıktı aşağıdaki hello görmeniz gerekir:

    ![Uygulama çıkış - başarısız yemek incelemeleri pasta grafik yüzdelerini öğrenme Spark makine. ] (./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning sonuç çıktısı")

    Negatif bir sonuç denetleme geçirilen tooa başvuruyor ancak bu grafikte başarısız toohello yemek inceleme, sonuç "sıfırdan" anlamına gelir.

## <a name="shut-down-hello-notebook"></a>Hello dizüstü bilgisayarı
Merhaba uygulaması çalıştıran bitirdikten sonra hello not defteri toorelease hello kaynakları kapatmanız gerekir. toodo çok hello **dosya** hello dizüstü menüsünde **Kapat ve Durdur**. Bu kapanır ve not defterini kapatır hello.

## <a name="seealso"></a>Ayrıca bkz.
* [Genel Bakış: Azure HDInsight’ta Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Senaryolar
* [BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme](hdinsight-apache-spark-use-bi-tools.md)
* [Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma](hdinsight-apache-spark-eventhub-streaming.md)
* [HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Uygulamaları oluşturma ve çalıştırma
* [Scala kullanarak tek başına uygulama oluşturma](hdinsight-apache-spark-create-standalone-application.md)
* [Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Araçlar ve uzantılar
* [Intellij Idea toocreate için Hdınsight araçları eklentisi kullanma ve Spark Scala uygulamaları gönderin](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Uzaktan Intellij Idea toodebug Spark uygulamaları için Hdınsight araçları eklentisi kullanma](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter not defterleri ile dış paketleri kullanma](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Kaynakları yönetme
* [Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme](hdinsight-apache-spark-resource-manager.md)
* [HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama](hdinsight-apache-spark-job-debugging.md)
