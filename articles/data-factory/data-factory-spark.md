---
title: "aaaInvoke Spark Azure veri fabrikası'ndan programlar | Microsoft Docs"
description: "MapReduce etkinliği kullanılarak bir Azure data factory tooinvoke Spark programların nasıl hello öğrenin."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: f88943ece7ee3d21dedbd857609f1b2713b62741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a>Azure Data Factory işlem hatlarını Spark programlardan çağırma

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive etkinliği](data-factory-hive-activity.md)
> * [Pig etkinliği](data-factory-pig-activity.md)
> * [MapReduce etkinliği](data-factory-map-reduce.md)
> * [Hadoop akış etkinliği](data-factory-hadoop-streaming-activity.md)
> * [Spark etkinliği](data-factory-spark.md)
> * [Machine Learning Batch Yürütme Etkinliği](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning Kaynak Güncelleştirme Etkinliği](data-factory-azure-ml-update-resource-activity.md)
> * [Saklı Yordam Etkinliği](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL Etkinliği](data-factory-usql-activity.md)
> * [.NET özel etkinlik](data-factory-use-custom-activities.md)

## <a name="introduction"></a>Giriş
Spark etkinlik hello biridir [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) Azure Data Factory tarafından desteklenir. Bu etkinlik belirtilen hello çalıştıran Azure hdınsight'ta Apache Spark kümenizin üzerinde Spark program.    

> [!IMPORTANT]
> - Spark etkinliği Azure Data Lake Store birincil depolama alanı olarak kullanın Hdınsight Spark kümeleri desteklemez.
> - Spark etkinlik (kendi) Hdınsight Spark kümeleri yalnızca varolan destekler. Bir isteğe bağlı Hdınsight bağlı hizmeti desteklemiyor.

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a>İzlenecek yol: Spark etkinliği ile işlem hattı oluşturma
Merhaba tipik adımları toocreate Data Factory işlem hattı Spark aktivitesiyle şunlardır.  

1. Veri Fabrikası oluşturun.
2. Bir Azure Storage bağlı hizmeti toolink Hdınsight Spark küme toohello data factory ile ilişkili Azure depolama alanınızı oluşturun.     
2. Azure Hdınsight bağlı hizmeti toolink Azure Hdınsight toohello veri fabrikasında Apache Spark kümesi oluşturun.
3. Toohello Azure Storage bağlı hizmeti başvuran bir veri kümesi oluşturun. Şu anda, üretilen hiçbir çıktı olsa bile bir çıkış veri kümesi bir etkinlik için belirtmeniz gerekir.  
4. #2'de oluşturduğunuz toohello Hdınsight bağlı hizmeti başvuruyor Spark etkinliği ile işlem hattı oluşturacaksınız. Merhaba etkinliği bir çıkış veri kümesi olarak hello önceki adımda oluşturduğunuz hello veri kümesi ile yapılandırılır. Merhaba çıktı veri kümesi, zamanlama (saatlik, günlük, vs.) hangi sürücüleri hello ' dir. Bu nedenle, Hello etkinlik gerçekten bir çıktı üretmez olsa bile hello çıktı veri kümesi belirtmeniz gerekir.

### <a name="prerequisites"></a>Ön koşullar
1. Create bir **genel amaçlı Azure depolama hesabı** hello gözden geçirme yönergeleri izleyerek tarafından: [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account).  
2. Create bir **Azure hdınsight'ta Apache Spark kümesi** hello öğreticideki yönergeler aşağıdaki tarafından: [Azure hdınsight'ta Apache Spark oluşturma küme](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). Bu kümeyle #1. adımda oluşturduğunuz hello Azure depolama hesabı ilişkilendirin.  
3. Karşıdan yükle ve hello python komut dosyasını gözden **test.py** konumunda bulunan: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).  
3.  Karşıya yükleme **test.py** toohello **pyFiles** hello klasöründe **adfspark** , Azure Blob depolamada kapsayıcı. Bunlar yoksa hello kapsayıcı ve başlangıç klasörü oluşturun.

### <a name="create-data-factory"></a>Veri fabrikası oluşturma
Bu adımda hello data factory oluşturmayla başlayalım.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Tıklatın **yeni** hello sol menüsünde **veri + analiz**, tıklatıp **Data Factory**.
3. Merhaba, **yeni data factory** dikey penceresinde girin **SparkDF** hello adı için.

   > [!IMPORTANT]
   > Merhaba adı'hello Azure data Factory olması **genel benzersiz**. Merhaba hata görürseniz: **veri fabrikası adı "SparkDF" kullanılabilir değil**. Merhaba veri fabrikası (örneğin, yournameSparkDFdate ve oluşturmayı yeniden deneyin. Hello adını değiştirin Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.   
4. Select hello **Azure aboneliği** oluşturulan hello veri fabrikası toobe istediğiniz.
5. Var olan seçin **kaynak grubu** veya bir Azure kaynak grubu oluşturun.
6. Seçin **PIN toodashboard** seçeneği.  
6. Tıklatın **oluşturma** hello üzerinde **yeni data factory** dikey.

   > [!IMPORTANT]
   > toocreate Data Factory örnekleri hello üyesi olmalıdır [veri fabrikası katkıda bulunan](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello abonelik/kaynak grubu düzeyinde rol.
7. Hello oluşturulmakta hello veri fabrikası gördüğünüz **Pano** hello şekilde Azure portal'ın:   
8. Merhaba veri fabrikası başarıyla oluşturulduktan sonra gösterir hello veri fabrikası sayfasına bakın hello hello data Factory içeriği. Merhaba data factory sayfasını görmüyorsanız hello Panoda veri fabrikanızın hello kutucuğa tıklayın.

    ![Data Factory dikey penceresi](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a>Bağlı hizmetler oluşturma
Bu adımda, iki bağlı hizmet, bir toolink Spark küme tooyour data factory'nizi oluşturmak ve diğer toolink Azure depolama tooyour data factory'nizi hello.  

#### <a name="create-azure-storage-linked-service"></a>Azure Storage bağlı hizmeti oluşturma
Bu adımda, Azure depolama hesabı tooyour veri fabrikanıza bağlayın. Bu kılavuzda daha sonra bir adımda oluşturduğunuz bir veri kümesi toothis bağlantılı hizmeti anlamına gelmektedir. Hello hello sonraki adımda tanımladığınız Hdınsight bağlı hizmeti toothis bağlantılı hizmeti çok ifade eder.  

1. Tıklatın **yazar ve dağıtma** hello üzerinde **Data Factory** veri fabrikanızın dikey. Merhaba Data Factory Düzenleyici görmeniz gerekir.
2. **Yeni data store**’a tıklayın ve **Azure depolama**’yı seçin.

   ![Yeni veri deposu - Azure Depolama - menü](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. Merhaba görmelisiniz **JSON betiği** bağlantılı hizmetinin hello Düzenleyicisi'nde bir Azure depolama alanı oluşturmak için.

   ![Azure Storage bağlı hizmeti](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. Değiştir **hesap adı** ve **hesap anahtarı** Azure depolama hesabınızın hello adı ve erişim anahtarına sahip. toolearn tooget depolama alanınızın erişim nasıl anahtar, hello bilgi nasıl tooview, kopyalama ve yeniden oluşturma depolama erişim anahtarları içinde hakkında [depolama hesabınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
5. toodeploy Merhaba bağlantılı hizmeti,'ı tıklatın **dağıtma** hello komut çubuğunda. Merhaba bağlı hizmet başarıyla dağıtıldıktan sonra hello **taslak-1** penceresi görünmemelidir; gördüğünüz **AzureStorageLinkedService** hello hello soldaki ağaç görünümünde.

#### <a name="create-hdinsight-linked-service"></a>Hdınsight bağlı hizmeti oluşturma
Bu adımda, Hdınsight Spark küme toohello data factory'nizi Azure Hdınsight bağlı hizmeti toolink oluşturun. Merhaba Hdınsight kümesi hello ardışık bu örnekteki hello Spark etkinliğinde belirtilen kullanılan toorun hello Spark programdır.  

1. Düğmeyi görmüyorsanız araç çubuğunda **... Daha fazla** hello araç çubuğundan, **yeni işlem**ve ardından **Hdınsight kümesi**.

    ![Hdınsight bağlı hizmeti oluşturma](media/data-factory-spark/new-hdinsight-linked-service.png)
2. Aşağıdaki kod parçacığında toohello hello kopyalayıp **taslak-1** penceresi. Merhaba JSON Düzenleyicisi'nde, şu adımları hello:
    1. Merhaba belirtin **URI** Merhaba Hdınsight Spark küme. Örneğin: `https://<sparkclustername>.azurehdinsight.net/`.
    2. Merhaba Hello adını belirtin **kullanıcı** erişim toohello Spark kümesi vardır.
    3. Merhaba belirtin **parola** kullanıcı için.
    4. Merhaba belirtin **Azure depolama bağlantılı hizmeti** hello Hdınsight Spark kümesi ile ilişkili. Bu örnek,: **AzureStorageLinkedService**.

    ```json
    {
        "name": "HDInsightLinkedService",
        "properties": {
            "type": "HDInsight",
            "typeProperties": {
                "clusterUri": "https://<sparkclustername>.azurehdinsight.net/",
                "userName": "admin",
                "password": "**********",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    > [!IMPORTANT]
    > - Spark etkinliği Azure Data Lake Store birincil depolama alanı olarak kullanın Hdınsight Spark kümeleri desteklemez.
    > - Yalnızca (kendi) Hdınsight Spark kümesinde varolan Spark etkinlik destekler. Bir isteğe bağlı Hdınsight bağlı hizmeti desteklemiyor.

    Bkz: [Hdınsight bağlı hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) hello hakkındaki ayrıntılar için hizmet Hdınsight bağlı.
3.  toodeploy Merhaba bağlantılı hizmeti,'ı tıklatın **dağıtma** hello komut çubuğunda.  

### <a name="create-output-dataset"></a>Çıktı veri kümesi oluşturma
Merhaba çıktı veri kümesi, zamanlama (saatlik, günlük, vs.) hangi sürücüleri hello ' dir. Bu nedenle, Hello etkinlik gerçekten herhangi bir çıktı üretmez olsa bile hello ardışık düzeninde bir çıkış veri kümesi hello spark etkinliğinin belirtmeniz gerekir. Bir giriş veri kümesi hello etkinlik için belirtme isteğe bağlıdır.

1. Merhaba, **Data Factory düzenleyici**, tıklatın **... Daha fazla** hello komut çubuğunda **yeni veri kümesi**seçip **Azure Blob Depolama**.  
2. Aşağıdaki kod parçacığında toohello taslak-1 penceresinde hello kopyalayıp yeniden açın. Merhaba JSON parçacığı tanımlar adlı bir veri kümesi **OutputDataset**. Ayrıca, hello sonuçları adlı hello blob kapsayıcısında depolanır belirttiğiniz **adfspark** ve adlı hello klasör **pyFiles/çıkış**. Daha önce belirtildiği gibi bu veri kümesi kukla bir veri kümesi gereklidir. Bu örnekte Hello Spark program herhangi bir çıktı üretmez. Merhaba **kullanılabilirlik** bölümü belirtiyor bu hello çıktı veri kümesi günlük oluşturulur.  

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "sparkoutput.txt",
                "folderPath": "adfspark/pyFiles/output",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": "\t"
                }
            },
            "availability": {
                "frequency": "Day",
                "interval": 1
            }
        }
    }
    ```
3. toodeploy dataset Merhaba, tıklatın **dağıtma** hello komut çubuğunda.


### <a name="create-pipeline"></a>İşlem hattı oluşturma
Bu adımda oluşturduğunuz sahip işlem hattı bir **HDInsightSpark** etkinlik. Şu anda, çıktı veri kümesi hello etkinlik herhangi bir çıktı üretmez olsa bile bir çıkış veri kümesi oluşturmanız gerekir böylece hangi sürücüleri zamanlama, hello değil. Merhaba etkinlik herhangi bir girdi almazsa oluşturma hello girdi veri kümesi atlayabilirsiniz. Bu nedenle, hiçbir girdi veri kümesi bu örnekte belirtilir.

1. Merhaba, **Data Factory düzenleyici**, tıklatın **... Daha fazla** hello komut çubuğunda ve ardından **yeni işlem hattı**.
2. Merhaba taslak-1 penceresinde Hello komut dosyası komut dosyası izleyen hello ile değiştirin:

    ```json
    {
        "name": "SparkPipeline",
        "properties": {
            "activities": [
                {
                    "type": "HDInsightSpark",
                    "typeProperties": {
                        "rootPath": "adfspark\\pyFiles",
                        "entryFilePath": "test.py",
                        "getDebugInfo": "Always"
                    },
                    "outputs": [
                        {
                            "name": "OutputDataset"
                        }
                    ],
                    "name": "MySparkActivity",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-02-05T00:00:00Z",
            "end": "2017-02-06T00:00:00Z"
        }
    }
    ```
    Hello aşağıdaki noktaları göz önünde bulundurun:
    - Merhaba **türü** özelliği çok ayarlanmış**HDInsightSpark**.
    - Merhaba **rootPath** çok ayarlanır**adfspark\\pyFiles** adfspark hello Azure Blob kapsayıcısı ve pyFiles olduğu ince kapsayıcıdaki klasörüdür. Bu örnekte, hello Azure Blob Storage hello hello Spark kümesi ile ilişkili olan bir ' dir. Merhaba dosya tooa yükleyebilirsiniz farklı Azure depolama. Bunu yaparsanız, bir Azure Storage bağlı hizmeti toolink bu depolama hesabı toohello veri fabrikası oluşturun. Ardından, hello için bir değer olarak hello hello bağlı hizmetin adını belirtin **sparkJobLinkedService** özelliği. Bkz: [Spark etkinlik özellikleri](#spark-activity-properties) bu özellik ve Spark etkinlik hello tarafından desteklenen diğer özellikleri hakkında ayrıntılı bilgi için.  
    - Merhaba **entryFilePath** toohello ayarlamak **test.py**, hello python dosyası değil.
    - Merhaba **Getdebugınfo** özelliği çok ayarlanmış**her zaman**, yani hello günlük dosyaları her zaman oluşturulan (başarılı veya başarısız).

        > [!IMPORTANT]
        > Bu özellik çok ayarlamayın öneririz`Always` bir üretim ortamında bir sorunu gidermeye çalışıyor değilseniz.
    - Merhaba **çıkarır** bölümü bir çıkış veri kümesi yok. Merhaba spark program herhangi bir çıktı üretmez olsa bile bir çıkış veri kümesi belirtmeniz gerekir. Merhaba çıkış veri kümesi sürücüleri hello zamanlama hello ardışık düzen (saatlik, günlük, vs.).  

        Spark etkinliği tarafından desteklenen hello özellikleri hakkında daha fazla ayrıntı için bkz: [Spark etkinlik özellikleri](#spark-activity-properties) bölümü.
3. toodeploy hello ardışık tıklatın **dağıtma** hello komut çubuğunda.

### <a name="monitor-pipeline"></a>İşlem hattını izleme
1. Tıklatın **X** tooclose Data Factory Düzenleyici dikey ve toonavigate toohello Data Factory giriş sayfasında yedekleyin. Tıklatın **izleme ve yönetme** toolaunch hello başka bir sekmesinde uygulama izleme.

    ![İzleme ve yönetme bölmesi](media/data-factory-spark/monitor-and-manage-tile.png)
2. Değişiklik hello **başlangıç zamanı** hello üstünde çok filtre**1/2/2017**, tıklatıp **Uygula**.
3. Hello arasında yalnızca bir gününü (2017-02-01) başlangıç ve bitiş saatlerini (2017-02-02) hello ardışık olduğundan yalnızca bir etkinlik penceresini görmeniz gerekir. Bu hello veri dilim onaylayın **hazır** durumu.

    ![Merhaba işlem hattını izleme](media/data-factory-spark/monitor-and-manage-app.png)    
4. Select hello **etkinlik penceresini** toosee etkinliği hakkında ayrıntılı bilgi çalıştırmak hello. Bir hata varsa, hello sağ bölmedeki hakkındaki ayrıntıları bakın.

### <a name="verify-hello-results"></a>Merhaba sonuçlarını doğrulayın

1. Başlatma **Jupyter not defteri** giderek Hdınsight Spark kümenizin: https://CLUSTERNAME.azurehdinsight.net/jupyter. Ayrıca, Hdınsight Spark kümeniz için küme Panosu başlatın ve sonra başlatın **Jupyter not defteri**.
2. Tıklatın **yeni** -> **PySpark** toostart yeni bir not defteri.

    ![Yeni Jupyter not defteri](media/data-factory-spark/jupyter-new-book.png)
3. Çalışma hello komutu aşağıdaki hello metin kopyalama/yapıştırma ve tuşlarına basarak **SHIFT + ENTER** hello ikinci ifade hello sonunda.  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. Merhaba hvac tablodan hello veri gördüğünüzü onaylayın:  

    ![Jupyter sorgu sonuçları](media/data-factory-spark/jupyter-notebook-results.png)

Bkz: [bir Spark SQL sorgusu çalıştırmanız](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) bölüm ayrıntılı yönergeler için. 

### <a name="troubleshooting"></a>Sorun giderme
Ayarladığınız bu yana **Getdebugınfo** çok**her zaman**, gördüğünüz bir **günlük** hello alt **pyFiles** klasörü, Azure Blob kapsayıcısında. Merhaba Günlük klasörü Hello günlük dosyasına ek ayrıntılar sağlar. Bu günlük dosyası bir hata olduğunda özellikle yararlıdır. Bir üretim ortamında tooset isteyebilirsiniz, çok**hatası**.

Daha fazla sorun giderme için aşağıdaki adımları hello:


1. Çok gidin`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.

    ![YARN kullanıcı arabirimini uygulama](media/data-factory-spark/yarnui-application.png)  
2. Tıklatın **günlükleri** hello birini denemeleri çalıştırın.

    ![Uygulama sayfası](media/data-factory-spark/yarn-applications.png)
3. Merhaba günlük sayfasındaki ek hata bilgileri görmeniz gerekir.

    ![Günlük hatası](media/data-factory-spark/yarnui-application-error.png)

Aşağıdaki bölümlerde hello Data Factory varlıkları toouse Apache Spark kümesi ve data factory'nizi Spark etkinliğinde hakkında bilgi sağlar.

## <a name="spark-activity-properties"></a>Spark etkinlik özellikleri
Spark etkinliği ile işlem hattı hello örnek JSON tanımını şöyledir:    

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "arguments": [ "arg1", "arg2" ],
                    "sparkConfig": {
                        "spark.python.worker.memory": "512m"
                    }
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "description": "This activity invokes hello Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

Merhaba aşağıdaki tabloda hello JSON tanımını kullanılan hello JSON özellikleri açıklanmaktadır:

| Özellik | Açıklama | Gerekli |
| -------- | ----------- | -------- |
| ad | Hello etkinliğinde hello ardışık düzen adı. | Evet |
| Açıklama | Hangi hello etkinliği açıklayan metin yapar. | Hayır |
| type | Bu özellik tooHDInsightSpark ayarlamanız gerekir. | Evet |
| linkedServiceName | Merhaba Hdınsight adını bağlantılı hizmetinin hangi hello Spark programı çalıştırır. | Evet |
| rootPath | Hello Azure Blob kapsayıcısı ve hello Spark dosyasını içeren klasör. Merhaba dosya adı büyük/küçük harf duyarlıdır. | Evet |
| entryFilePath | Göreli yol toohello kök klasöründe hello Spark kod/paketi. | Evet |
| className | Uygulamanın Java/Spark ana sınıfı | Hayır |
| Bağımsız değişkenler | Komut satırı bağımsız değişkenleri toohello Spark program listesi. | Hayır |
| proxyUser | Merhaba kullanıcı hesabı tooimpersonate tooexecute hello Spark programı | Hayır |
| sparkConfig | Merhaba konu başlığı altında listelenen Spark yapılandırma özellikleri için değerleri belirtin: [Spark yapılandırması - uygulama özellikleri](https://spark.apache.org/docs/latest/configuration.html#available-properties). | Hayır |
| Getdebugınfo | Merhaba Spark günlük dosyalarını kopyalanan toohello Hdınsight küme tarafından kullanılan Azure depolama olduğunda belirtir (veya) sparkJobLinkedService tarafından belirtilen. İzin verilen değerler: None, her zaman veya hata. Varsayılan değer: yok. | Hayır |
| sparkJobLinkedService | Merhaba hello Spark iş dosyası, bağımlılıklar ve günlükleri tutan Azure Storage bağlı hizmeti.  Bu özellik için bir değer belirtmezseniz, Hdınsight kümesi ile ilişkili hello depolama kullanılır. | Hayır |

## <a name="folder-structure"></a>Klasör yapısı
Merhaba Spark etkinliği bir satır içi komut dosyası Pig olarak desteklemez ve Hive etkinlikleri yapın. Spark işleri de Pig/Hive işleri daha fazla genişletilebilir. Spark işleri, birden çok bağımlılıkları gibi sağlayabilirsiniz jar (Merhaba java sınıf yerleştirilen) paketleri, python dosyaları (PYTHONPATH hello yerleştirilmiş) ve diğer dosyaları.

Merhaba hello Hdınsight bağlı hizmeti tarafından başvurulan Azure Blob Depolama Klasör yapısındaki aşağıdaki hello oluşturun. Ardından, bağımlı dosyaları toohello uygun alt klasörleri tarafından temsil edilen hello kök klasöründe karşıya **entryFilePath**. Örneğin, python dosyalar toohello pyFiles alt ve jar dosyalarını toohello Kavanoz hello kök klasörünün alt karşıya yükleyin. Çalışma zamanında Data Factory hizmetinin hello Azure Blob Depolama Klasör yapısındaki aşağıdaki hello bekler:     

| Yol | Açıklama | Gerekli | Tür |
| ---- | ----------- | -------- | ---- |
| . | Merhaba Spark hello depolama bağlı hizmeti işinde Hello kök yolu    | Evet | Klasör |
| &lt;Kullanıcı tanımlı&gt; | toohello girdi dosyası hello Spark işin işaret eden hello yolu | Evet | Dosya |
| . / jar'lar | Bu klasörü altındaki tüm dosyaları karşıya ve üzerinde hello kümesinin hello java sınıf yerleştirilmiş | Hayır | Klasör |
| . / pyFiles | Bu klasörü altındaki tüm dosyaları karşıya ve hello kümesinin PYTHONPATH hello üzerinde yerleştirilmiş | Hayır | Klasör |
| . / dosyaları | Bu klasörü altındaki tüm dosyaları karşıya ve yürütücü çalışma dizini yerleştirilmiş | Hayır | Klasör |
| . / arşivler | Bu klasörü altındaki tüm dosyaları sıkıştırılmamış | Hayır | Klasör |
| . / günlükleri | Merhaba Spark kümesi günlüklerinden depolandığı hello klasör.| Hayır | Klasör |

Hello Azure Blob Storage Hdınsight bağlı hizmeti hello tarafından başvurulan iki Spark iş dosyaları içeren bir depolama için örnek aşağıda verilmiştir.

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs
```
