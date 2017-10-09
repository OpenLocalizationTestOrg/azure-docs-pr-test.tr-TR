---
title: aaaBuild ilk data factory'nizi (Visual Studio) | Microsoft Docs
description: "Bu öğreticide Visual Studio kullanarak örnek bir Azure Data Factory işlem hattı oluşturursunuz."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7398c0c9-7a03-4628-94b3-f2aaef4a72c5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 0c5eb01b685d978d80916da0293cc2d3701b2d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-by-using-visual-studio"></a>Öğretici: Visual Studio kullanarak veri fabrikası oluşturma
> [!div class="op_single_selector" title="Tools/SDKs"]
> * [Genel bakış ve önkoşullar](data-factory-build-your-first-pipeline.md)
> * [Azure portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager Şablonu](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)

Bu öğretici şunların nasıl yapıldığını gösterir toocreate Visual Studio kullanarak Azure data factory. Hello Data Factory proje şablonunu kullanarak bir Visual Studio projesi oluşturmak, Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve işlem hattı) JSON biçiminde tanımlayın ve yayımlama/bu varlıkları toohello bulut dağıtırsınız. 

Bu öğreticide Hello ardışık bir etkinlik vardır: **Hdınsight Hive etkinliği**. Bu etkinlik dönüşümler veri tooproduce çıkış veri girişi bir Azure Hdınsight kümesinde bir hive betiği çalıştırır. Başlangıç ve bitiş zamanlarını hello arasında bir ay belirtilen sonra hello ardışık düzen zamanlanmış toorun ' dir. 

> [!NOTE]
> Bu öğreticide, Azure Data Factory kullanarak verilerin nasıl kopyalanacağı gösterilmemektedir. Nasıl bir öğretici için Azure Data Factory kullanarak toocopy verileri görmek [Öğreticisi: Blob Storage tooSQL veritabanı ' veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Bir işlem hattında birden fazla etkinlik olabilir. Ve hello çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir. Daha fazla bilgi için bkz. [Data Factory'de zamanlama ve yürütme](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).


## <a name="walkthrough-create-and-publish-data-factory-entities"></a>İzlenecek Yol: Data Factory varlıkları oluşturma ve yayımlama
Bu kılavuz kapsamında gerçekleştirme hello adımlar şunlardır:

1. İki bağlı hizmet oluşturun: **AzureStorageLinkedService1** ve **HDInsightOnDemandLinkedService1**. 
   
    Bu öğreticide, Hello hive etkinliği içinde için girdi ve çıktı verilerini aynı Azure Blob Storage hello. Bir isteğe bağlı Hdınsight kümesi tooprocess varolan giriş verisi tooproduce çıktı verileri kullanın. Merhaba isteğe bağlı Hdınsight kümesi otomatik olarak sizin için Azure Data Factory'nin hello giriş verisi işlenen hazır toobe olduğunda çalışma zamanında oluşturulur. Verilerinizi depolayan veya hello Data Factory hizmeti çalışma zamanında toothem bağlanabilmesi tooyour veri fabrikası hesaplar toolink gerekir. Bu nedenle, hello AzureStorageLinkedService1 kullanarak Azure depolama hesabı toohello veri fabrikanıza bağlamak ve isteğe bağlı Hdınsight kümesi hello HDInsightOnDemandLinkedService1 kullanarak bağlayın. Yayımlama sırasında oluşturulan hello veri fabrikası toobe hello adı veya mevcut bir veri fabrikasını belirtin.  
2. İki veri kümesi oluşturma: **InputDataset** ve **OutputDataset**, hello Azure blob depolamada depolanan hello girdi/çıktı verilerini temsil eder. 
   
    Bu veri kümesi tanımları hello önceki adımda oluşturduğunuz toohello Azure Storage bağlı hizmeti bakın. Hello InputDataset için hello blob kapsayıcıda (adfgetstarted) belirtin ve bir blob hello giriş verisi içeren klasörü (inptutdata) hello. Hello OutputDataset, hello blob kapsayıcıda (adfgetstarted) belirtin ve hello çıktı verilerini tutan hello klasörü (adfgetstarted). Yapı, kullanılabilirlik ve ilke gibi diğer özellikleri de belirtirsiniz.
3. **MyFirstPipeline** adlı bir işlem hattı oluşturun. 
  
    Bu kılavuzda, yalnızca bir etkinlik hello ardışık düzen vardır: **Hdınsight Hive etkinliği**. Bu etkinlik dönüştürme, bir isteğe bağlı Hdınsight kümesinde bir hive betiği çalıştırarak veri tooproduce çıktı verileri girin. toolearn hive etkinliği hakkında daha fazla bilgi görmek [Hive etkinliği](data-factory-hive-activity.md) 
4. **DataFactoryUsingVS** adlı bir veri fabrikası oluşturun. Merhaba veri fabrikası ve tüm Data Factory varlıkları (bağlı hizmetler, tablolar ve hello ardışık düzeni) dağıtın.
5. Yayımladığınızda, Azure portal dikey penceresi ve izleme ve yönetim uygulaması toomonitor hello ardışık düzen kullanın. 
  
### <a name="prerequisites"></a>Ön koşullar
1. Okuyun [öğreticiye genel bakış](data-factory-build-your-first-pipeline.md) makale ve tam hello **önkoşul** adımları. Merhaba öğesini de seçebilirsiniz **genel bakış ve önkoşulları** hello üst tooswitch toohello makale hello aşağı açılan listesinde seçeneği. Seçerek geri toothis makale hello önkoşulları tamamladıktan sonra geçiş **Visual Studio** hello aşağı açılan listesinden seçeneği.
2. toocreate Data Factory örnekleri hello üyesi olmalıdır [veri fabrikası katkıda bulunan](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello abonelik/kaynak grubu düzeyinde rol.  
3. Merhaba aşağıdakilerin yüklü olması gerekir:
   * Visual Studio 2013 veya Visual Studio 2015
   * Visual Studio 2013 veya Visual Studio 2015 için Azure SDK’sını indirin. Çok gidin[Azure indirme sayfası](https://azure.microsoft.com/downloads/) tıklatıp **VS 2013** veya **VS 2015** hello içinde **.NET** bölümü.
   * Visual Studio için Hello en son Azure Data Factory eklentisini indirin: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) veya [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). Aşağıdaki adımları hello yaparak hello eklentisi güncelleştirebilirsiniz: hello menüsünde **Araçları** -> **Uzantılar ve güncelleştirmeler** -> **çevrimiçi**  ->  **Visual Studio Galerisi** -> **Visual Studio için Microsoft Azure Data Factory Araçları** -> **güncelleştirme**.

Şimdi, Visual Studio toocreate bir Azure data factory kullanalım.

### <a name="create-visual-studio-project"></a>Visual Studio projesi oluşturma
1. **Visual Studio 2013** veya **Visual Studio 2015**’i başlatın. Tıklatın **dosya**, çok noktası**yeni**, tıklatıp **proje**. Merhaba görmelisiniz **yeni proje** iletişim kutusu.  
2. Merhaba, **yeni proje** iletişim, select hello **DataFactory** şablonu ve tıklatın **boş Data Factory projesi**.   

    ![Yeni proje iletişim kutusu](./media/data-factory-build-your-first-pipeline-using-vs/new-project-dialog.png)
3. Girin bir **adı** hello projesi için **konumu**ve hello için bir ad **çözüm**, tıklatıp **Tamam**.

    ![Çözüm Gezgini](./media/data-factory-build-your-first-pipeline-using-vs/solution-explorer.png)

### <a name="create-linked-services"></a>Bağlı hizmetler oluşturma
Bu adımda iki bağlı hizmet oluşturursunuz: **Azure Depolama** ve **İsteğe bağlı HDInsight**. 

Hello Azure depolama hizmeti bağlantıları hello bağlantı bilgilerini sağlayarak Azure depolama hesabı toohello data factory'nizi bağlı. Veri Fabrikası hizmetine bağlı hello hizmet ayarı tooconnect toohello Azure depolama bağlantı dizesinden hello çalışma zamanında kullanır. Bu depolama giriş tutar ve çıktı verilerini hello ardışık düzen ve hello için komut dosyası hello hive etkinlik tarafından kullanılan hive. 

İsteğe bağlı Hdınsight bağlı hizmeti ile Merhaba giriş verisi hazır tooprocessed olduğunda hello Hdınsight kümesi çalışma zamanında otomatik olarak oluşturulur. Merhaba küme hello belirtilen süre boyunca işlem yapma ve boşta bittikten sonra silinir. 

> [!NOTE]
> Veri Fabrikası adı ve ayarları Data Factory çözümünüzü yayımlama hello zamanında belirterek oluşturun.

#### <a name="create-azure-storage-linked-service"></a>Azure Storage bağlı hizmeti oluşturma
1. Sağ **bağlı hizmetler** hello Çözüm Gezgini'nde çok noktası**Ekle**, tıklatıp **yeni öğe**.      
2. Merhaba, **Yeni Öğe Ekle** iletişim kutusunda **Azure depolama bağlı hizmeti** hello listesi ve tıklatın **Ekle**.
    ![Azure Storage Bağlı Hizmeti](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)
3. Değiştir `<accountname>` ve `<accountkey>` Azure storage hesabınızı ve anahtarını hello adı. toolearn tooget depolama alanınızın erişim nasıl anahtar, hello bilgi nasıl tooview, kopyalama ve yeniden oluşturma depolama erişim anahtarları içinde hakkında [depolama hesabınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
    ![Azure Storage Bağlı Hizmeti](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)
4. Merhaba Kaydet **AzureStorageLinkedService1.json** dosya.

#### <a name="create-azure-hdinsight-linked-service"></a>Azure HDInsight bağlı hizmeti oluşturma
1. Merhaba, **Çözüm Gezgini**, sağ **bağlı hizmetler**, çok noktası**Ekle**, tıklatıp **yeni öğe**.
2. **İsteğe Bağlı HDInsight Bağlı Hizmeti**’ni seçin ve **Ekle**’ye tıklayın.
3. Hello yerine **JSON** JSON aşağıdaki hello ile:

     ```json
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
        "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService1"
            }
        }
    }
    ```

    Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:

    Özellik | Açıklama
    -------- | ----------- 
    ClusterSize | Merhaba Hdınsight Hadoop kümesi Hello boyutunu belirtir.
    TimeToLive | Silinmeden önce hello Hdınsight kümesi, o hello boşta kalma süresini belirtir.
    linkedServiceName | Hdınsight Hadoop kümesi tarafından oluşturulan kullanılan toostore hello günlükleri olan hello depolama hesabını belirtir. 

    > [!IMPORTANT]
    > Merhaba Hdınsight kümesi oluşturur bir **varsayılan kapsayıcı** hello blob depolamada hello JSON (linkedServiceName) belirtildi. Hdınsight Hello küme silindiğinde bu kapsayıcıyı silmez. Bu davranış tasarım gereğidir. İsteğe bağlı HDInsight bağlı hizmeti kullanıldığında, mevcut canlı bir küme olmadığı sürece bir dilim her işlendiğinde bir HDInsight kümesi oluşturulur (timeToLive). Merhaba işlem bittiğinde hello küme otomatik olarak silinir.
    > 
    > Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz. Bunları hello işlerin sorunları giderilmesi için ihtiyacınız yoksa, toodelete isteyebilirsiniz bunları tooreduce hello depolama maliyeti. Bu kapsayıcıların Hello adları izleyen bir desen: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`. Gibi araçlar kullanın [Microsoft Storage Gezgini](http://storageexplorer.com/) toodelete kapsayıcılarında Azure blob depolama.

    JSON özellikleri hakkında daha fazla bilgi için [İşlem bağlı hizmetleri](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) makalesine bakın. 
4. Merhaba Kaydet **Hdınsightondemandlinkedservice1.JSON** dosya.

### <a name="create-datasets"></a>Veri kümeleri oluşturma
Bu adımda, veri kümeleri toorepresent hello girişi oluşturun ve Hive işlenmesi için verileri çıktı. Bu veri kümeleri toohello başvuran **AzureStorageLinkedService1** Bu öğreticide daha önce oluşturduğunuz. bağlantılı hizmet noktaları tooan Azure depolama hesabı hello ve veri kümeleri, giriş tutan hello depolamada kapsayıcı, klasör, dosya adı belirtin ve çıktı verilerini.   

#### <a name="create-input-dataset"></a>Girdi veri kümesi oluşturma
1. Merhaba, **Çözüm Gezgini**, sağ **tabloları**, çok noktası**Ekle**, tıklatıp **yeni öğe**.
2. Seçin **Azure Blob** hello listeden hello hello dosyasının adını çok değiştirme**Inputdataset.JSON**, tıklatıp **Ekle**.
3. Hello yerine **JSON** hello düzenleyicisinde JSON parçacığı aşağıdaki hello ile:

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
            "typeProperties": {
                "fileName": "input.log",
                "folderPath": "adfgetstarted/inputdata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            },
            "external": true,
            "policy": {}
        }
    }
    ```
    Bu JSON parçacığı adlı veri kümesini tanımlamaktadır **Azureblobınput** hello ardışık düzen hello hive etkinliğin girdi verilerini temsil eden. Merhaba giriş verisi adlı hello blob kapsayıcısında bulunur belirttiğiniz `adfgetstarted` ve adlı hello klasör `inputdata`.

    Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:

    Özellik | Açıklama |
    -------- | ----------- |
    type |Merhaba type özelliği çok ayarlamak**AzureBlob** verileri Azure Blob depolamada yer aldığından.
    linkedServiceName | Daha önce oluşturduğunuz AzureStorageLinkedService1 toohello başvuruyor.
    fileName |Bu özellik isteğe bağlıdır. Bu özelliği atarsanız, hello folderPath tüm hello dosyalarından çekilir. Bu durumda, yalnızca hello input.log işlenir.
    type | Merhaba günlük dosyaları metin biçiminde olduğundan TextFormat kullanacağız. |
    columnDelimiter | Merhaba günlük dosyalarındaki sütunlar hello virgül karakteriyle ayrılmış (`,`)
    frequency/interval | tooMonth sıklığını ve aralığı hello girdi dilimlerinin aylık olarak kullanılabileceğini 1.
    external | Hello etkinlik için giriş verileri Hello hello ardışık düzen tarafından oluşturulmadıysa, bu özellik tootrue ayarlanır. Bu özellik yalnızca giriş veri kümelerinde belirtilir. Merhaba girdi veri kümesi hello ilk etkinlik için her zaman tootrue ayarlayın.
4. Merhaba Kaydet **Inputdataset.JSON** dosya.

#### <a name="create-output-dataset"></a>Çıktı veri kümesi oluşturma
Şimdi, hello Azure Blob Depolama depolanan hello çıkış veri kümesi toorepresent çıktı verileri oluşturun.

1. Merhaba, **Çözüm Gezgini**, sağ **tabloları**, çok noktası**Ekle**, tıklatıp **yeni öğe**.
2. Seçin **Azure Blob** hello listeden hello hello dosyasının adını çok değiştirme**OutputDataset.json**, tıklatıp **Ekle**.
3. Hello yerine **JSON** hello düzenleyicisinde JSON aşağıdaki hello ile:
    
    ```json
    {
        "name": "AzureBlobOutput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
            "typeProperties": {
                "folderPath": "adfgetstarted/partitioneddata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            }
        }
    }
    ```
    Merhaba JSON parçacığı tanımlar adlı bir veri kümesi **AzureBlobOutput** çıktı hello hive etkinliğiyle hello ardışık düzen tarafından üretilen verilerini temsil eder. Merhaba çıktı hello hive etkinliği tarafından üretilen veriler adlı hello blob kapsayıcısında yerleştirilir belirttiğiniz `adfgetstarted` ve adlı hello klasör `partitioneddata`. 
    
    Merhaba **kullanılabilirlik** bölümü belirtiyor bu hello çıktı veri kümesi, aylık olarak oluşturulur. Merhaba ardışık Hello çıkış veri kümesi sürücüleri hello zamanlama. Merhaba ardışık düzen aylık, başlangıç ve bitiş zamanları arasında çalışır. 

    Bkz: **hello girdi veri kümesi oluşturma** bu özelliklerin açıklamaları için bölüm. Merhaba dataset hello ardışık düzen tarafından oluşturulduğundan çıktı veri hello dış özelliği ayarlı değil.
4. Merhaba Kaydet **OutputDataset.json** dosya.

### <a name="create-pipeline"></a>İşlem hattı oluşturma
Hello Azure Storage bağlı hizmeti ve girdi ve çıktı veri kümelerini kadarki oluşturdunuz. Şimdi, **HDInsightHive** etkinliğiyle bir işlem hattı oluşturacaksınız. Merhaba **giriş** hello hive etkinliği çok ayarlanır**Azureblobınput** ve **çıkış** çok ayarlanır**AzureBlobOutput**. Bir dilim bir giriş veri kümesinin aylık kullanılabilir (sıklığı: Month, interval: 1), ve hello çıktı diliminin ayda bir oluşturulduğunu çok. 

1. Merhaba, **Çözüm Gezgini**, sağ **ardışık düzen**, çok noktası**Ekle**, tıklatıp **yeni öğe.**
2. Seçin **Hive dönüşüm işlem hattı** hello listesi ve tıklatın **Ekle**.
3. Hello yerine **JSON** parçacığını aşağıdaki hello ile:

    > [!IMPORTANT]
    > Değiştir `<storageaccountname>` depolama hesabınızın hello ada sahip.

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService1",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                        }
                    },
                    "inputs": [
                        {
                            "name": "AzureBlobInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobOutput"
                        }
                    ],
                    "policy": {
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2016-04-01T00:00:00Z",
            "end": "2016-04-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    > [!IMPORTANT]
    > Değiştir `<storageaccountname>` depolama hesabınızın hello ada sahip.

    Merhaba JSON parçacığı tek bir etkinliğin (Hive etkinliği) oluşan bir ardışık düzen tanımlar. Bu etkinlik bir Hive betiği tooprocess giriş verilerini bir isteğe bağlı Hdınsight kümesi tooproduce çıktı verileri üzerinde çalışır. Merhaba etkinlikler bölümünde hello ardışık JSON, çok kümesi türü ile yalnızca bir etkinlik hello dizisindeki bkz**Hdınsighthive**. 

    Belirli tooHDInsight Hive etkinliği olan hello türü özelliklerinde, hangi Azure Storage bağlı hizmeti hello hive betik dosyası, hello yolu toohello komut dosyası ve parametreleri toohello komut dosyasını belirtin. 

    Merhaba Hive betik dosyası **partitionweblogs.hql**, (Merhaba scriptLinkedService tarafından belirtilen) hello Azure depolama hesabı ve hello depolanan `script` hello kapsayıcı klasöründe `adfgetstarted`.

    Merhaba `defines` bölümdür toohello hive betiğini Hive yapılandırma değerleri olarak geçirilir kullanılan toospecify hello çalışma zamanı ayarları (örneğin `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.

    Merhaba **Başlat** ve **son** hello ardışık düzen özelliklerini hello etkin dönem hello ardışık belirtir. Merhaba dataset toobe (Merhaba ay başlangıç ve bitiş tarihleri aynı olduğu için) yalnızca dilim hello ardışık düzen tarafından üretilen sonra aylık, bu nedenle, üretilen yapılandırılmış.

    Bu hello Hive betiğini hello tarafından belirtilen hello işlem üzerinde çalıştığı belirtin Hello JSON etkinliğinde **linkedServiceName** – **Hdınsightondemandlinkedservice**.
4. Merhaba Kaydet **HiveActivity1.json** dosya.

### <a name="add-partitionweblogshql-and-inputlog-as-a-dependency"></a>partitionweblogs.hql ve input.log dosyalarını bağımlılık olarak ekleme
1. Sağ **bağımlılıkları** hello içinde **Çözüm Gezgini** penceresinde, çok noktası**Ekle**, tıklatıp **varolan öğeyi**.  
2. Toohello gidin **C:\ADFGettingStarted** seçip **partitionweblogs.hql**, **input.log** dosyaları ve tıklatın **Ekle**. Bu iki dosyayı hello önkoşulları bir parçası olarak oluşturulan [öğreticiye genel bakış](data-factory-build-your-first-pipeline.md).

Merhaba sonraki adımda hello çözümü yayımladığınızda hello **partitionweblogs.hql** dosyasıdır karşıya yüklenen toohello **betik** hello klasöründe `adfgetstarted` blob kapsayıcısı.   

### <a name="publishdeploy-data-factory-entities"></a>Data Factory varlıklarını yayımlama/dağıtma
Bu adımda, proje toohello Azure Data Factory hizmetine hello Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve işlem hattı) yayımlayın. Yayımlama Hello işleminde veri fabrikanızın hello adı belirtin. 

1. Merhaba Çözüm Gezgini'nde projeye sağ tıklayın ve **Yayımla**.
2. Görürseniz **tooyour Microsoft hesabı oturum** iletişim kutusunda, Azure aboneliği olan hello hesabı için kimlik bilgilerinizi girin ve tıklayın **oturum**.
3. İletişim kutusu aşağıdaki hello görmeniz gerekir:

   ![Yayımla iletişim kutusu](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
4. Merhaba, **data factory Yapılandır** sayfasında, adımları hello:

    ![Yayımlama - Yeni veri fabrikası ayarları](media/data-factory-build-your-first-pipeline-using-vs/publish-new-data-factory.png)

   1. **Yeni Data Factory Oluştur** seçeneğini seçin.
   2. Benzersiz bir girin **adı** hello veri fabrikası için. Örneğin: **DataFactoryUsingVS09152016**. Merhaba adı genel olarak benzersiz olmalıdır.
   3. Merhaba hello için doğru abonelik seçin **abonelik** alan. 
        > [!IMPORTANT]
        > Herhangi bir abonelik görmüyorsanız, bir yönetici veya hello aboneliğin ortak yöneticisi olan bir hesabı kullanarak oturum emin olun.
   4. Select hello **kaynak grubu** oluşturulan hello veri fabrikası toobe için.
   5. Select hello **bölge** hello veri fabrikası için.
   6. Tıklatın **sonraki** tooswitch toohello **öğeleri Yayımla** sayfası. (Tuşuna **sekmesini** hello ad alanı tooif hello dışında toomove **sonraki** düğmesi devre dışıdır.)

    > [!IMPORTANT]
    > Merhaba hata alırsanız **veri fabrikası adı "DataFactoryUsingVS" kullanılabilir değil** yayımlarken hello adını (örneğin, yournameDataFactoryUsingVS) değiştirin. Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.   
1. Merhaba, **öğeleri Yayımla** sayfasında, tüm veri varlıkları seçilir ve tıklatın fabrikaları hello olun **sonraki** tooswitch toohello **Özet** sayfası.

    ![Öğe yayımlama sayfası](media/data-factory-build-your-first-pipeline-using-vs/publish-items-page.png)     
2. Merhaba özeti gözden geçirin ve tıklatın **sonraki** toostart, hello dağıtım işlemi ve görünüm hello **dağıtım durumu**.

    ![Özet sayfası](media/data-factory-build-your-first-pipeline-using-vs/summary-page.png)
3. Merhaba, **dağıtım durumu** sayfasında hello hello dağıtım işleminin durumunu görmeniz gerekir. Merhaba dağıtımını gerçekleştirdikten sonra Son'a tıklayın.

Önemli noktaları toonote:

- Merhaba hatayı alırsanız: **Bu abonelik, Microsoft.DataFactory kayıtlı toouse ad değil**hello aşağıdakilerden birini yapın ve yeniden yayımlamayı deneyin:
    - Azure PowerShell'de komut tooregister hello Data Factory sağlayıcısının aşağıdaki hello çalıştırın.
        ```PowerShell   
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
        ```
        Bu Data Factory sağlayıcısının kayıtlı hello komutu tooconfirm aşağıdaki hello çalıştırabilirsiniz.

        ```PowerShell
        Get-AzureRmResourceProvider
        ```
    - Merhaba toohello Azure aboneliğinizde oturum açma kullanılarak [Azure portal](https://portal.azure.com) ve tooa Data Factory dikey penceresine gidin (veya) hello Azure portalında bir data factory oluşturun. Bu eylemin hello sağlayıcıyı sizin için otomatik olarak kaydeder.
- Merhaba veri fabrikasının Hello adı hello gelecekte bir DNS adı olarak kayıtlı ve bu nedenle herkese görünür hale gelmiştir.
- toocreate Data Factory örnekleri, toobe bir yönetici veya ortak yöneticisi olan hello Azure aboneliği gerekir

### <a name="monitor-pipeline"></a>İşlem hattını izleme
Bu adımda, diyagram görünümü hello data Factory kullanarak hello ardışık izleyin. 

#### <a name="monitor-pipeline-using-diagram-view"></a>Diyagram Görünümünü kullanarak işlem hattını izleme
1. İçinde toohello oturum [Azure portal](https://portal.azure.com/), adımları hello:
   1. **Diğer hizmetler** ve **Data factory’ler** öğesine tıklayın.
       
        ![Data factory’lere göz atma](./media/data-factory-build-your-first-pipeline-using-vs/browse-datafactories.png)
   2. Veri fabrikanızın SELECT hello adı (örneğin: **DataFactoryUsingVS09152016**) veri fabrikaları hello listesinden.
   
       ![Data factory’nizi seçme](./media/data-factory-build-your-first-pipeline-using-vs/select-first-data-factory.png)
2. Merhaba giriş sayfasında veri fabrikanızın tıklatın **diyagramı**.

    ![Diyagram kutucuğu](./media/data-factory-build-your-first-pipeline-using-vs/diagram-tile.png)
3. Hello diyagram görünümü, hello ardışık düzen ve Bu öğreticide kullanılan veri kümelerine genel bakış konusuna bakın.

    ![Diyagram Görünümü](./media/data-factory-build-your-first-pipeline-using-vs/diagram-view-2.png)
4. tooview hello düzenindeki hello sağ kanaldaki tüm etkinlikleri Diyagram ve ardışık düzeni Aç'ı tıklatın.

    ![İşlem hattı menüsünü açma](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-menu.png)
5. Merhaba ardışık düzeninde hello Hdınsighthive etkinliğini gördüğünüzü onaylayın.

    ![İşlem hattı görünümünü açma](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-view.png)

    toonavigate toohello önceki görünüme geri tıklatın **veri fabrikası** hello içerik haritası menüsünde hello üstünde.
6. Merhaba, **diyagram görünümü**, hello dataset çift **Azureblobınput**. Bu hello dilim onaylayın **hazır** durumu. Bu işlem birkaç dakika hello dilim tooshow için hazır durumda kadar sürebilir. Bir süre bekledikten sonra gerçekleştirilmez, hello doğru kapsayıcıda yerleştirilen hello girdi dosyasının (input.log) yüklü olup olmadığına bakın (`adfgetstarted`) ve klasör (`inputdata`). Ve o hello emin olun **dış** özelliği hello giriş veri kümesi üzerinde çok ayarlanmış**doğru**. 

   ![Girdi dilimi hazır durumda](./media/data-factory-build-your-first-pipeline-using-vs/input-slice-ready.png)
7. Tıklatın **X** tooclose **Azureblobınput** dikey.
8. Merhaba, **diyagram görünümü**, hello dataset çift **AzureBlobOutput**. İşlenmekte olan bu hello dilim bakın.

   ![Veri kümesi](./media/data-factory-build-your-first-pipeline-using-vs/dataset-blade.png)
9. İşlem bittiğinde hello dilimi bkz **hazır** durumu.

   > [!IMPORTANT]
   > İsteğe bağlı HDInsight kümesinin oluşturulması genellikle biraz zaman alır (yaklaşık 20 dakika). Bu nedenle, hello ardışık düzen tootake beklediğiniz **yaklaşık olarak 30 dakika** tooprocess hello dilim.  
   
    ![Veri kümesi](./media/data-factory-build-your-first-pipeline-using-vs/dataset-slice-ready.png)    
10. Merhaba dilim olduğunda **hazır** durum, hello denetleyin `partitioneddata` hello klasöründe `adfgetstarted` hello için blob depolama alanınızın kapsayıcısında çıkış verileri.  

    ![çıktı verileri](./media/data-factory-build-your-first-pipeline-using-vs/three-ouptut-files.png)
11. Merhaba dilim toosee ayrıntılarını içinde tıklatın bir **veri dilimi** dikey.

    ![Veri dilimi ayrıntıları](./media/data-factory-build-your-first-pipeline-using-vs/data-slice-details.png)  
12. Hello çalıştırmak bir etkinliği **etkinlik çalışır listesi** toosee etkinliği hakkında ayrıntılı bir çalıştır (Senaryomuzda Hive etkinliğiyle) bir **etkinlik çalışma ayrıntıları** penceresi. 
  
    ![Etkinlik çalışma ayrıntıları](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-blade.png)    

    Merhaba günlük dosyalarından yürütüldü hello Hive sorgusu ve durum bilgileri görebilirsiniz. Bu günlükler her türlü sorunu gidermek için kullanışlıdır.  

Bkz: [veri kümelerini ve ardışık düzen izleme](data-factory-monitor-manage-pipelines.md) nasıl toouse hello Azure portal toomonitor hello ardışık düzen ve veri kümeleri, bu öğreticide oluşturduğunuz hakkında yönergeler için.

#### <a name="monitor-pipeline-using-monitor--manage-app"></a>İzleme ve Yönetme Uygulamasını kullanarak işlem hattını izleme
İzleyicisi'ni kullanın ve uygulama toomonitor hatlarınızı yönetme. Bu uygulamanın kullanımına ilişkin ayrıntılı bilgi için bkz. [İzleme ve Yönetme Uygulamasını kullanarak Azure Data Factory işlem hatlarını izleme ve yönetme](data-factory-monitor-manage-app.md).

1. İzleme ve Yönetme kutucuğuna tıklayın.

    ![İzleme ve Yönetme kutucuğu](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-tile.png)
2. İzleme ve Yönetme uygulamasını görmeniz gerekir. Değişiklik hello **başlangıç zamanı** ve **bitiş saati** toomatch başlangıç (04 01 2016 12: 00'da) ve bitiş zamanları (04-02-2016 12: 00'da) ardışık düzen ve tıklatın **Uygula**.

    ![İzleme ve Yönetme Uygulaması](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-app.png)
3. bir etkinlik penceresi toosee ayrıntılarını seçin, hello **etkinlik Windows listesi** toosee ayrıntıları.
    ![Etkinlik penceresi ayrıntıları](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)

> [!IMPORTANT]
> Merhaba dilim başarıyla işlendiğinde hello girdi dosyası silinir. Merhaba girdi dosyasını (input.log) toohello toorerun hello dilim istediğiniz veya öğreticiyi yeniden Merhaba, bu nedenle, karşıya `inputdata` hello klasörünü `adfgetstarted` kapsayıcı.

### <a name="additional-notes"></a>Ek notlar
- Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir. İşlem hattında bir veya daha fazla etkinlik olabilir. Örneğin, bir kopyalama etkinliği toocopy verilerinden bir kaynak tooa hedef veri deposu ve Hdınsight Hive etkinliği toorun bir Hive betiği tootransform verileri girin. Bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tüm kaynakları ve kopyalama etkinliği hello tarafından desteklenen havuzlarını hello için. Bkz: [işlem bağlı Hizmetleri](data-factory-compute-linked-services.md) Data Factory ile desteklenen işlem Hizmetleri hello listesi.
- Bağlı hizmetler veri depolarını veya hizmetleri tooan Azure data factory işlem. Bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tüm kaynakları ve kopyalama etkinliği hello tarafından desteklenen havuzlarını hello için. Bkz: [işlem bağlı Hizmetleri](data-factory-compute-linked-services.md) Data Factory ile desteklenen işlem Hizmetleri hello listesi için ve [dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) , çalıştırabilirsiniz üzerlerinde.
- Bkz: [taşıma verilerden / tooAzure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) hello kullanılan JSON özellikleri hakkında ayrıntılı bilgi için Azure depolama bağlantılı hizmet tanımı.
- İsteğe bağlı HDInsight kümesi yerine kendi HDInsight kümenizi kullanabilirsiniz. Ayrıntılar için bkz. [İşlem Bağlı Hizmetleri](data-factory-compute-linked-services.md).
-  Merhaba Data Factory oluşturur bir **Linux tabanlı** JSON önceki hello ile Hdınsight kümesi. Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).
- Merhaba Hdınsight kümesi oluşturur bir **varsayılan kapsayıcı** hello blob depolamada hello JSON (linkedServiceName) belirtildi. Hdınsight Hello küme silindiğinde bu kapsayıcıyı silmez. Bu davranış tasarım gereğidir. İsteğe bağlı HDInsight bağlı hizmeti kullanıldığında, mevcut canlı bir küme olmadığı sürece bir dilim her işlendiğinde bir HDInsight kümesi oluşturulur (timeToLive). Merhaba işlem bittiğinde hello küme otomatik olarak silinir.
    
    Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz. Bunları hello işlerin sorunları giderilmesi için ihtiyacınız yoksa, toodelete isteyebilirsiniz bunları tooreduce hello depolama maliyeti. Bu kapsayıcıların Hello adları izleyen bir desen: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`. Gibi araçlar kullanın [Microsoft Storage Gezgini](http://storageexplorer.com/) toodelete kapsayıcılarında Azure blob depolama.
- Şu anda, çıktı veri kümesi hello etkinlik herhangi bir çıktı üretmez olsa bile bir çıkış veri kümesi oluşturmanız gerekir böylece hangi sürücüleri zamanlama, hello değil. Merhaba etkinlik herhangi bir girdi almazsa oluşturma hello girdi veri kümesi atlayabilirsiniz. 
- Bu öğreticide, Azure Data Factory kullanarak verilerin nasıl kopyalanacağı gösterilmemektedir. Nasıl bir öğretici için Azure Data Factory kullanarak toocopy verileri görmek [Öğreticisi: Blob Storage tooSQL veritabanı ' veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).


## <a name="use-server-explorer-tooview-data-factories"></a>Sunucu Gezgini tooview veri fabrikaları kullanın
1. İçinde **Visual Studio**, tıklatın **Görünüm** üzerinde hello menü öğesini tıklatıp **Sunucu Gezgini**.
2. Merhaba Sunucu Gezgini penceresinde **Azure** ve genişletin **Data Factory**. Görürseniz **tooVisual Studio oturum**, hello girin **hesap** tıklatın ve Azure aboneliği ile ilişkili **devam**. **parola** girip **Oturum aç**’a tıklayın. Visual Studio, aboneliğinizdeki tüm Azure data factory'leri hakkında bilgi tooget çalışır. Bu işlemde hello hello durumunu görmek **Data Factoy görev listesi** penceresi.

    ![Sunucu Gezgini](./media/data-factory-build-your-first-pipeline-using-vs/server-explorer.png)
3. Veri Fabrikası sağ tıklatın ve seçin **dışarı veri fabrikası tooNew proje** Visual Studio projesi dayalı mevcut bir data factory'ye toocreate.

    ![Data factory’yi dışarı aktarma](./media/data-factory-build-your-first-pipeline-using-vs/export-data-factory-menu.png)

## <a name="update-data-factory-tools-for-visual-studio"></a>Visual Studio için Data Factory araçlarını güncelleştirme
Visual Studio için tooupdate Azure Data Factory araçları hello adımları izleyin:

1. Tıklatın **Araçları** hello menü ve seçim **Uzantılar ve güncelleştirmeler**.
2. Seçin **güncelleştirmeleri** hello sol bölmesinde ve ardından **Visual Studio Galerisi**.
3. **Visual Studio için Azure Data Factory araçları**’nı seçin ve **Güncelleştir**’e tıklayın. Bu girişi görmüyorsanız hello hello Araçları'nın en son sürümü zaten sahip.

## <a name="use-configuration-files"></a>Yapılandırma dosyalarını kullanma
Bağlı hizmetler/tablolar/işlem hatları için her ortamda farklı için Visual Studio tooconfigure özelliklerinde yapılandırma dosyalarını kullanabilirsiniz.

Azure depolama bağlı hizmeti için JSON tanımı aşağıdaki hello göz önünde bulundurun. toospecify **connectionString** accountname ve accountkey hello ortam (Dev/Test/Production) toowhich üzerinde göre farklı değerleri olan Data Factory varlıklarını dağıttığınız. Her ortam için ayrı bir yapılandırma dosyası kullanarak bu davranışı elde edebilirsiniz.

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="add-a-configuration-file"></a>Yapılandırma dosyası ekleme
Merhaba aşağıdaki adımları uygulayarak her ortam için bir yapılandırma dosyası ekleyin:   

1. Visual Studio çözümünüzü Hello Data Factory projenize sağ tıklayın, çok gelin**Ekle**, tıklatıp **yeni öğe**.
2. Seçin **Config** hello soldaki yüklenmiş şablonlar hello listeden seçin **yapılandırma dosyası**, girin bir **adı** hello yapılandırması için dosya ve tıklatın**Eklemek**.

    ![Yapılandırma dosyasını ekleme](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. Biçim aşağıdaki hello yapılandırma parametrelerini ve değerlerini ekleyin:

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    Bu örnek, Azure Storage bağlı hizmetinin ve Azure SQL bağlı hizmetinin connectionString özelliğini yapılandırır. Adı belirtmek için hello sözdizimi olduğuna dikkat edin [JsonPath](http://goessner.net/articles/JsonPath/).   

    JSON hello kod aşağıdaki gösterildiği gibi bir dizi değere sahip özellik varsa:  

    ```json
    "structure": [
          {
              "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
        }
    ],
    ```

    Özellikler, aşağıdaki yapılandırma dosyasına (kullanımı sıfır tabanlı dizin) hello gösterildiği gibi yapılandırın:

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a>Boşluklu özellik adları
Özellik adında boşluklar varsa, hello aşağıdaki örneğine (veritabanı sunucu adı) gösterildiği gibi köşeli ayraç kullanın:

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a>Yapılandırma kullanarak çözümü dağıtma
Azure Data Factory varlıklarını vs'de toouse Bu yayımlama işlemi için istediğiniz hello yapılandırma belirtebilirsiniz.

yapılandırma dosyası kullanarak Azure Data Factory projesindeki varlıkları toopublish:   

1. Data Factory projesine sağ tıklatın ve **Yayımla** toosee hello **öğeleri Yayımla** iletişim kutusu.
2. Mevcut bir veri fabrikasını seçin veya üzerinde hello data factory oluşturmak için değerleri belirtin **data factory Yapılandır** sayfasında ve tıklayın **sonraki**.   
3. Merhaba üzerinde **öğeleri Yayımla** sayfa: hello için kullanılabilir yapılandırmaların açılan listesini görmek **Dağıtım Yapılandırması Seç** alan.

    ![Yapılandırma dosyası seçme](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. Select hello **yapılandırma dosyası** , gibi toouse ve'ı tıklatın, **sonraki**.
5. Merhaba hello JSON dosyasının adını gördüğünüzü onaylayın **Özet** sayfasında ve tıklayın **sonraki**.
6. Tıklatın **son** hello dağıtım işlemi tamamlandıktan sonra.

Dağıttığınızda, dağıtılan tooAzure Data Factory hizmetinin hello varlıklardır önce hello hello yapılandırma dosyasından hello JSON dosyalarında özellikler için kullanılan tooset değerler değerlerdir.   

## <a name="use-azure-key-vault"></a>Azure Key Vault kullanma
Şu önerilir ve genellikle karşı güvenlik ilkesi toocommit bağlantı dizeleri toohello kod deposu gibi hassas verileri değil. Bkz: [ADF güvenli yayımlama](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) Azure anahtar kasası hassas bilgilerini depolamak ve Data Factory varlıklarını yayımlanırken kullanmayla ilgili GitHub toolearn üzerinde örnek. Visual Studio uzantısı güvenli yayımlama Hello anahtar kasasında depolanan hello gizli toobe sağlar ve yalnızca başvuruları toothem bağlantılı Hizmetleri belirtilen / dağıtım yapılandırmaları. Data Factory varlıkları tooAzure yayımladığınızda, bu başvuruları çözümlenir. Bu dosyalar ardından tüm gizli gösterme olmadan kaydedilmiş toosource deposu olabilir.

## <a name="summary"></a>Özet
Bu öğreticide, bir Hdınsight hadoop kümesindeki Hive betiği çalıştıran bir Azure data factory tooprocess veri oluşturuldu. Hello Data Factory Düzenleyici'hello Azure portal toodo hello aşağıdaki adımları kullanılır:  

1. Oluşturulan Azure **data factory**.
2. Oluşturulan iki **bağlı hizmet**:
   1. **Azure depolama** hizmet toolink toohello veri fabrikası girdi/çıktı dosyalarını tutan Azure blob depolama alanınızın bağlı.
   2. **Azure Hdınsight** isteğe bağlı bir isteğe bağlı Hdınsight Hadoop küme toohello data factory hizmeti toolink bağlı. Azure Data Factory Hdınsight Hadoop küme yalnızca zaman tooprocess giriş verileri hem de üretim çıktı verilerini oluşturur.
3. Oluşturulan iki **veri kümeleri**, hello ardışık düzende Hdınsight Hive etkinliğiyle ilgili girdi ve çıktı verilerini açıklayan.
4. **HDInsight Hive** etkinliğine sahip oluşturulan bir **işlem hattı**.  

## <a name="next-steps"></a>Sonraki Adımlar
Bu makalede, isteğe bağlı HDInsight kümesinde bir Hive betiği çalıştıran dönüştürme etkinliğine (HDInsight Etkinliği) sahip işlem hattı oluşturdunuz. toouse Azure Blob tooAzure SQL, bir kopyalama etkinliği toocopy verileri nasıl görürüm toosee [öğretici: bir Azure blob tooAzure SQL veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Merhaba çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir. Ayrıntılı bilgi için bkz. [Data Factory’de zamanlama ve yürütme](data-factory-scheduling-and-execution.md). 


## <a name="see-also"></a>Ayrıca Bkz.
| Konu | Açıklama |
|:--- |:--- |
| [İşlem hatları](data-factory-create-pipelines.md) |Bu makalede, işlem hatlarının ve etkinliklerin Azure Data Factory anlamanıza yardımcı olur ve nasıl toouse bunları tooconstruct veri odaklı iş akışlarının senaryo veya iş. |
| [Veri kümeleri](data-factory-create-datasets.md) |Bu makale, Azure Data Factory’deki veri kümelerini anlamanıza yardımcı olur. |
| [Veri Dönüştürme Etkinlikleri](data-factory-data-transformation-activities.md) |Bu makalede, Azure Data Factory’nin desteklediği veri dönüştürme etkinliklerinin (bu öğreticide kullandığınız HDInsight Hive dönüştürmesi gibi) bir listesi sağlanmaktadır. |
| [Zamanlama ve yürütme](data-factory-scheduling-and-execution.md) |Bu makalede Azure Data Factory uygulama modelinin hello zamanlama ve yürütme yönleri açıklanmaktadır. |
| [İzleme Uygulaması kullanılarak işlem hatlarını izleme ve yönetme](data-factory-monitor-manage-app.md) |Bu makalede nasıl toomonitor, yönetme ve hatalarını ayıklama işlem hatlarını izleme ve yönetim uygulaması hello kullanarak. |
