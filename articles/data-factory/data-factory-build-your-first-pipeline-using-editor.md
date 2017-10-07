---
title: "aaaBuild ilk data factory'nizi (Azure portalı) | Microsoft Docs"
description: "Bu öğreticide Data Factory Düzenleyici'hello Azure portal kullanarak örnek bir Azure Data Factory işlem hattı oluşturacaksınız."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fc80776001b181a59c04d80d2e05c20b107a63f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a>Öğretici: Azure portal kullanarak ilk Azure data factory’nizi derleme
> [!div class="op_single_selector"]
> * [Genel bakış ve önkoşullar](data-factory-build-your-first-pipeline.md)
> * [Azure portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager Şablonu](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)


Bu makalede, bilgi nasıl toouse [Azure portal](https://portal.azure.com/) toocreate ilk Azure data factory'nizi. diğer araçlar/SDK, kullanarak toodo hello öğretici seçin hello seçeneklerden birini hello aşağı açılan listeden. 

Bu öğreticide Hello ardışık bir etkinlik vardır: **Hdınsight Hive etkinliği**. Bu etkinlik dönüşümler veri tooproduce çıkış veri girişi bir Azure Hdınsight kümesinde bir hive betiği çalıştırır. Başlangıç ve bitiş zamanlarını hello arasında bir ay belirtilen sonra hello ardışık düzen zamanlanmış toorun ' dir. 

> [!NOTE]
> Bu öğreticide Hello veri ardışık giriş verisi tooproduce çıktı verilerini dönüştürür. Nasıl bir öğretici için Azure Data Factory kullanarak toocopy verileri görmek [Öğreticisi: Blob Storage tooSQL veritabanı ' veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Bir işlem hattında birden fazla etkinlik olabilir. Ve hello çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir. Daha fazla bilgi için bkz. [Data Factory'de zamanlama ve yürütme](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

## <a name="prerequisites"></a>Ön koşullar
1. Okuyun [öğreticiye genel bakış](data-factory-build-your-first-pipeline.md) makale ve tam hello **önkoşul** adımları.
2. Bu makalede hello Azure Data Factory hizmetine kavramsal bir genel bakış sağlamaz. Gitmenizi öneririz [giriş tooAzure Data Factory](data-factory-introduction.md) hello hizmetinin makale için ayrıntılı bir genel bakış.  

## <a name="create-data-factory"></a>Veri fabrikası oluşturma
Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir. İşlem hattında bir veya daha fazla etkinlik olabilir. Örneğin, bir kopyalama etkinliği toocopy verilerinden bir kaynak tooa hedef veri deposu ve Hdınsight Hive etkinliği toorun bir Hive betiği tootransform veri tooproduct çıktı verileri girin. Bu adımda hello data factory oluşturmayla başlayalım.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Tıklatın **yeni** hello sol menüsünde **veri + analiz**, tıklatıp **Data Factory**.

   ![Dikey pencere oluşturma](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. Merhaba, **yeni data factory** dikey penceresinde girin **GetStartedDF** hello adı için.

   ![Yeni veri fabrikası dikey penceresi](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > Merhaba adı'hello Azure data Factory olması **genel benzersiz**. Merhaba hatayı alırsanız: **veri fabrikası adı "GetStartedDF" kullanılabilir değil**. Hello veri fabrikası (örneğin, yournameGetStartedDF) Hello adını değiştirin ve oluşturmayı yeniden deneyin. Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.
   >
   > Merhaba veri fabrikasının Hello adı olarak kaydedilmesi bir **DNS** hello gelecekte olarak adlandırın ve bu nedenle herkese görünür hale gelmiştir.
   >
   >
4. Select hello **Azure aboneliği** oluşturulan hello veri fabrikası toobe istediğiniz.
5. Mevcut bir **kaynak grubu** seçin ya da bir kaynak grubu oluşturun. Merhaba öğretici için adlı bir kaynak grubu oluşturun: **ADFGetStartedRG**.
6. Select hello **konumu** hello veri fabrikası için. Yalnızca Hello Data Factory hizmeti tarafından desteklenen bölgeler hello aşağı açılan listesinde gösterilir.
7. Seçin **PIN toodashboard**. 
8. Tıklatın **oluşturma** hello üzerinde **yeni data factory** dikey.

   > [!IMPORTANT]
   > toocreate Data Factory örnekleri hello üyesi olmalıdır [veri fabrikası katkıda bulunan](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello abonelik/kaynak grubu düzeyinde rol.
   >
   >
7. Merhaba Panoda durumuyla döşeme hello aşağıdakilere bakın: dağıtma veri fabrikası.    

   ![Data factory durumu oluşturma](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. Tebrikler! İlk data factory’nizi başarıyla oluşturdunuz. Merhaba veri fabrikası başarıyla oluşturulduktan sonra gösterir hello veri fabrikası sayfasına bakın hello hello data Factory içeriği.     

    ![Data Factory dikey penceresi](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

Merhaba data factory'de işlem hattı oluşturmadan önce toocreate birkaç Data Factory varlıklarını önce gerekir. Bağlı hizmetler toolink veri depolarını/işlemlerini tooyour veri depolamak, giriş tanımlayın ve çıktı veri kümeleri toorepresent girdi/çıktı verilerini bağlı veri depolarında ve ardından bu veri kümeleri kullanan bir etkinlik hello işlem hattı oluşturma ilk oluşturduğunuzda.

## <a name="create-linked-services"></a>Bağlı hizmetler oluşturma
Bu adımda, Azure Storage hesabınızı ve bir isteğe bağlı Azure Hdınsight küme tooyour data factory bağlayın. Azure depolama hesabı bu örnekteki hello ardışık düzeni için girdi ve çıktı verilerini ayrı tutma hello hello. Merhaba Hdınsight bağlı hizmeti kullanılan toorun hello ardışık bu örnekteki hello etkinliğinde belirtilen Hive betiği ' dir. Ne tanımlamak [veri deposu](data-factory-data-movement-activities.md)/[işlem Hizmetleri](data-factory-compute-linked-services.md) senaryonuzda kullanılır ve bağlı hizmetler oluşturarak bu hizmetleri toohello veri fabrikası bağlayın.  

### <a name="create-azure-storage-linked-service"></a>Azure Storage bağlı hizmeti oluşturma
Bu adımda, Azure depolama hesabı tooyour veri fabrikanıza bağlayın. Bu öğreticide kullandığınız hello toostore girdi/çıktı verilerin ve HQL hello komut dosyasını aynı Azure depolama hesabı.

1. Tıklatın **yazar ve dağıtma** hello üzerinde **DATA FACTORY** dikey **GetStartedDF**. Merhaba Data Factory Düzenleyici görmeniz gerekir.

   ![Geliştir ve dağıt kutucuğu](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. **Yeni data store**’a tıklayın ve **Azure depolama**’yı seçin.

   ![Yeni veri deposu - Azure Depolama - menü](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. Görmeniz gerekir hello Azure depolama alanı oluşturmak için JSON betiği bağlantılı hizmeti hello düzenleyicisinde.

   ![Azure Storage bağlı hizmeti](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. Değiştir **hesap adı** hello Azure depolama hesabınızın adını içeren ve **hesap anahtarı** hello erişim anahtarı hello Azure depolama hesabı olan. toolearn tooget depolama alanınızın erişim nasıl anahtar, hello bilgi nasıl tooview, kopyalama ve yeniden oluşturma depolama erişim anahtarları içinde hakkında [depolama hesabınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
5. Tıklatın **dağıtma** toodeploy hello bağlantılı hizmet çubuğu hello komutu.

    ![Dağıt düğmesi](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   Merhaba bağlı hizmet başarıyla dağıtıldıktan sonra hello **taslak-1** penceresi görünmemelidir; gördüğünüz **AzureStorageLinkedService** hello hello soldaki ağaç görünümünde.

    ![Menüde Storage Bağlı Hizmeti](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a>Azure HDInsight bağlı hizmeti oluşturma
Bu adımda, bir isteğe bağlı Hdınsight kümesi tooyour data factory bağlayın. Merhaba Hdınsight küme otomatik olarak çalışma zamanında oluşturulur ve hello belirtilen süre boyunca işlem yapma ve boşta bittikten sonra silinir.

1. Merhaba, **Data Factory düzenleyici**, tıklatın **... Diğer**, **Yeni işlem** öğelerine tıklayın ve **İsteğe bağlı HDInsight kümesi**’ni seçin.

    ![Yeni işlem](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. Aşağıdaki kod parçacığında toohello hello kopyalayıp **taslak-1** penceresi. Merhaba JSON parçacığında kullanılan toocreate hello Hdınsight küme isteğe bağlı hello özellikleri açıklar.

    ```JSON
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:

   | Özellik | Açıklama |
   |:--- |:--- |
   | ClusterSize |Merhaba Hdınsight kümesi Hello boyutunu belirtir. |
   | TimeToLive | Silinmeden önce hello Hdınsight kümesi, o hello boşta kalma süresini belirtir. |
   | linkedServiceName | Hdınsight tarafından oluşturulan kullanılan toostore hello günlükleri olan hello depolama hesabını belirtir. |

    Hello aşağıdaki noktaları göz önünde bulundurun:

   * Merhaba Data Factory oluşturur bir **Linux tabanlı** hello JSON ile sizin için Hdınsight kümesi. Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).
   * İsteğe bağlı HDInsight kümesi yerine **kendi HDInsight kümenizi** kullanabilirsiniz. Ayrıntılar için bkz. [HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).
   * Merhaba Hdınsight kümesi oluşturur bir **varsayılan kapsayıcı** hello JSON belirtilen hello blob depolamada (**linkedServiceName**). Hdınsight Hello küme silindiğinde bu kapsayıcıyı silmez. Bu davranış tasarım gereğidir. İsteğe bağlı HDInsight bağlı hizmeti kullanıldığında, mevcut canlı bir küme olmadığı sürece bir dilim her işlendiğinde bir HDInsight kümesi oluşturulur (**timeToLive**). Merhaba işlem bittiğinde hello küme otomatik olarak silinir.

       Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz. Bunları hello işlerin sorunları giderilmesi için ihtiyacınız yoksa, toodelete isteyebilirsiniz bunları tooreduce hello depolama maliyeti. Bu kapsayıcıların Hello adları izleyen bir desen: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Gibi araçlar kullanın [Microsoft Storage Gezgini](http://storageexplorer.com/) toodelete kapsayıcılarında Azure blob depolama.

     Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).
3. Tıklatın **dağıtma** toodeploy hello bağlantılı hizmet çubuğu hello komutu.

    ![İsteğe bağlı HDInsight bağlı hizmetini dağıtma](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. Her ikisi de gördüğünüzü onaylayın **AzureStorageLinkedService** ve **Hdınsightondemandlinkedservice** hello hello soldaki ağaç görünümünde.

    ![Bağlı hizmetlerin bulunduğu ağaç görünümü](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a>Veri kümeleri oluşturma
Bu adımda, veri kümeleri toorepresent hello girişi oluşturun ve Hive işlenmesi için verileri çıktı. Bu veri kümeleri toohello başvuran **AzureStorageLinkedService** Bu öğreticide daha önce oluşturduğunuz. bağlantılı hizmet noktaları tooan Azure depolama hesabı hello ve veri kümeleri, giriş tutan hello depolamada kapsayıcı, klasör, dosya adı belirtin ve çıktı verilerini.   

### <a name="create-input-dataset"></a>Girdi veri kümesi oluşturma
1. Merhaba, **Data Factory düzenleyici**, tıklatın **... Daha fazla** hello komut çubuğunda **yeni veri kümesi**seçip **Azure Blob Depolama**.

    ![Yeni veri kümesi](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. Aşağıdaki kod parçacığında toohello taslak-1 penceresinde hello kopyalayıp yeniden açın. Merhaba JSON parçacığında adlı bir veri kümesi oluşturmakta olduğunuz **Azureblobınput** hello ardışık düzeninde bir etkinliğin girdi verilerini temsil eden. Ayrıca, hello giriş verisi adlı hello blob kapsayıcısında bulunur belirttiğiniz **adfgetstarted** ve adlı hello klasör **inputdata**.

    ```JSON
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
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
    Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:

   | Özellik | Açıklama |
   |:--- |:--- |
   | type |Merhaba type özelliği çok ayarlamak**AzureBlob** verileri Azure blob depolama alanında bulunduğundan. |
   | linkedServiceName |Toohello başvuruyor **AzureStorageLinkedService** daha önce oluşturduğunuz. |
   | folderPath | Merhaba blob belirtir **kapsayıcı** ve hello **klasörü** giriş BLOB'ları içerir. | 
   | fileName |Bu özellik isteğe bağlıdır. Bu özelliği atarsanız, hello folderPath tüm hello dosyalarından çekilir. Bu öğreticide, yalnızca hello **input.log** işlenir. |
   | type |Merhaba günlük dosyaları metin biçiminde kullandığımız için olan **TextFormat**. |
   | columnDelimiter |Merhaba günlük dosyalarındaki sütunlar tarafından ayrılmış **virgül karakteriyle (`,`)** |
   | frequency/interval |sıklığını çok**ay** ve aralığı **1**, kullanılabilir aylık olan dilimler giriş o hello anlamına gelir. |
   | external | Bu özellik çok ayarlanır**true** hello giriş verileri bu ardışık düzen tarafından oluşturulmamış olması durumunda. Bu öğreticide, hello özelliği tootrue ayarlarız şekilde hello input.log dosyası bu ardışık düzen tarafından oluşturulmaz. |

    Bu JSON özellikleri hakkında daha fazla bilgi için bkz. [Azure Blob bağlayıcısı makalesi](data-factory-azure-blob-connector.md#dataset-properties).
3. Tıklatın **dağıtma** toodeploy yeni oluşturulan hello dataset çubuğu hello komutu. Merhaba dataset hello hello soldaki ağaç görünümünde görmeniz gerekir.

### <a name="create-output-dataset"></a>Çıktı veri kümesi oluşturma
Şimdi, hello çıkış veri kümesi toorepresent hello çıktı verilerini hello Azure Blob Depolama depolanan oluşturun.

1. Merhaba, **Data Factory düzenleyici**, tıklatın **... Daha fazla** hello komut çubuğunda **yeni veri kümesi**seçip **Azure Blob Depolama**.  
2. Aşağıdaki kod parçacığında toohello taslak-1 penceresinde hello kopyalayıp yeniden açın. Merhaba JSON parçacığında adlı bir veri kümesi oluşturmakta olduğunuz **AzureBlobOutput**ve hello Hive betiği tarafından üretilen hello verilerin hello yapısını belirtme. Ayrıca, hello sonuçları adlı hello blob kapsayıcısında depolanır belirttiğiniz **adfgetstarted** ve adlı hello klasör **partitioneddata**. Merhaba **kullanılabilirlik** bölümü belirtiyor bu hello çıktı veri kümesi, aylık olarak oluşturulur.

    ```JSON
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
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
    Bkz: **hello girdi veri kümesi oluşturma** bu özelliklerin açıklamaları için bölüm. Merhaba dataset hello Data Factory hizmeti tarafından oluşturulduğundan çıktı veri hello dış özelliği ayarlı değil.
3. Tıklatın **dağıtma** toodeploy yeni oluşturulan hello dataset çubuğu hello komutu.
4. Bu hello veri kümesi başarıyla oluşturuldu doğrulayın.

    ![Bağlı hizmetlerin bulunduğu ağaç görünümü](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a>İşlem hattı oluşturma
Bu adımda, **HDInsightHive** etkinliğiyle ilk işlem hattınızı oluşturursunuz. Girdi dilimi kullanılabilir aylık (sıklığı: Month, interval: 1), çıktı diliminin ayda bir oluşturulduğunu ve hello etkinlik hello Zamanlayıcı özelliğinin de toomonthly ayarlayın. Merhaba çıktı veri kümesi ve hello etkinlik Zamanlayıcı Hello ayarlarının eşleşmesi gerekir. Şu anda, çıktı veri kümesi hello etkinlik herhangi bir çıktı üretmez olsa bile bir çıkış veri kümesi oluşturmanız gerekir böylece hangi sürücüleri zamanlama, hello değil. Merhaba etkinlik herhangi bir girdi almazsa oluşturma hello girdi veri kümesi atlayabilirsiniz. JSON aşağıdaki hello kullanılan hello özellikleri hello bu bölümün sonuna açıklanmıştır.

1. Merhaba, **Data Factory düzenleyici**, tıklatın **üç nokta (...) Daha fazla komut** ve ardından **yeni işlem hattı**.

    ![yeni işlem hattı düğmesi](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. Aşağıdaki kod parçacığında toohello taslak-1 penceresinde hello kopyalayıp yeniden açın.

   > [!IMPORTANT]
   > Değiştir **storageaccountname** depolama hesabınızdaki hello JSON hello adı.
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService",
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
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    Merhaba JSON parçacığında, Hdınsight kümesinde Hive tooprocess veri kullanan tek bir etkinlik oluşan bir işlem hattı oluşturuyorsunuz.

    Merhaba Hive betik dosyası **partitionweblogs.hql**, hello Azure depolama hesabı depolanır (adlı hello scriptLinkedService tarafından belirtilen **AzureStorageLinkedService**) ve  **komut dosyası** hello kapsayıcı klasöründe **adfgetstarted**.

    Merhaba **tanımlar** bölümdür toohello hive betiğini Hive yapılandırma değerleri olarak geçirilir kullanılan toospecify hello çalışma zamanı ayarları (örn., ${hiveconf: inputtable}, ${hiveconf}).

    Merhaba **Başlat** ve **son** hello ardışık düzen özelliklerini hello etkin dönem hello ardışık belirtir.

    Bu hello Hive betiğini hello tarafından belirtilen hello işlem üzerinde çalıştığı belirtin Hello JSON etkinliğinde **linkedServiceName** – **Hdınsightondemandlinkedservice**.

   > [!NOTE]
   > "Ardışık düzen JSON" bölümüne bakın [işlem hatlarının ve etkinliklerin Azure Data Factory](data-factory-create-pipelines.md) hello örnekte kullanılan JSON özellikleri hakkında ayrıntılı bilgi için.
   >
   >
3. Merhaba aşağıdakileri doğrulayın:

   1. **input.log** dosyasından hello **inputdata** hello klasörünü **adfgetstarted** hello Azure blob depolama kapsayıcısında
   2. **partitionweblogs.hql** dosyasından hello **betik** hello klasörünü **adfgetstarted** hello Azure blob depolama kapsayıcısında. Tam hello önkoşul adımları hello [öğreticiye genel bakış](data-factory-build-your-first-pipeline.md) bu dosyaları görmüyorsanız.
   3. Değiştirdiğinizi onaylayın **storageaccountname** depolama hesabınızdaki hello hello adıyla JSON kanalı.
4. Tıklatın **dağıtma** toodeploy hello ardışık çubuğu hello komutu. Merhaba itibaren **Başlat** ve **son** hello son kez ayarlanır ve **isPaused** dağıtıldıktan hemen sonra kümesi toofalse, hello ardışık düzen (Merhaba ardışık düzeninde etkinlik) çalışması olduğu.
5. Merhaba ardışık hello ağaç görünümünde gördüğünüzü onaylayın.

    ![İşlem hattının bulunduğu ağaç görünümü](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. Tebrikler, ilk işlem hattınızı başarıyla oluşturdunuz.

## <a name="monitor-pipeline"></a>İşlem hattını izleme
### <a name="monitor-pipeline-using-diagram-view"></a>Diyagram Görünümünü kullanarak işlem hattını izleme
1. Tıklatın **X** tooclose Data Factory Düzenleyici dikey toonavigate toohello Data Factory dikey penceresine geri tıklatın ve **diyagramı**.

    ![Diyagram kutucuğu](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. Hello diyagram görünümü, hello ardışık düzen ve Bu öğreticide kullanılan veri kümelerine genel bakış konusuna bakın.

    ![Diyagram Görünümü](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. tooview hello düzenindeki hello sağ kanaldaki tüm etkinlikleri Diyagram ve ardışık düzeni Aç'ı tıklatın.

    ![İşlem hattı menüsünü açma](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. Merhaba ardışık düzeninde hello Hdınsighthive etkinliğini gördüğünüzü onaylayın.

    ![İşlem hattı görünümünü açma](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    toonavigate toohello önceki görünüme geri tıklatın **veri fabrikası** hello içerik haritası menüsünde hello üstünde.
5. Merhaba, **diyagram görünümü**, hello dataset çift **Azureblobınput**. Bu hello dilim onaylayın **hazır** durumu. Bu işlem birkaç dakika hello dilim tooshow için hazır durumda kadar sürebilir. Bir süre bekledikten sonra gerçekleşmez hello doğru kapsayıcıda (adfgetstarted) ve klasörde (inputdata) yerleştirilen hello girdi dosyasının (input.log) yüklü olup olmadığına bakın.

   ![Girdi dilimi hazır durumda](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. Tıklatın **X** tooclose **Azureblobınput** dikey.
7. Merhaba, **diyagram görünümü**, hello dataset çift **AzureBlobOutput**. İşlenmekte olan bu hello dilim bakın.

   ![Veri kümesi](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. İşlem bittiğinde hello dilimi bkz **hazır** durumu.

   ![Veri kümesi](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > İsteğe bağlı HDInsight kümesinin oluşturulması genellikle biraz zaman alır (yaklaşık 20 dakika). Bu nedenle, hello ardışık düzen beklediğiniz çok ele **yaklaşık olarak 30 dakika** tooprocess hello dilim.
   >
   >

9. Merhaba dilim olduğunda **hazır** durum, hello denetleyin **partitioneddata** hello klasöründe **adfgetstarted** hello için blob depolama alanınızın kapsayıcısında çıkış verileri.  

   ![çıktı verileri](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. Merhaba dilim toosee ayrıntılarını içinde tıklatın bir **veri dilimi** dikey.

   ![Veri dilimi ayrıntıları](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. Hello çalıştırmak bir etkinliği **etkinlik çalışır listesi** toosee etkinliği hakkında ayrıntılı bir çalıştır (Senaryomuzda Hive etkinliğiyle) bir **etkinlik çalışma ayrıntıları** penceresi.   

   ![Etkinlik çalışma ayrıntıları](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   Merhaba günlük dosyalarından yürütüldü hello Hive sorgusu ve durum bilgileri görebilirsiniz. Bu günlükler her türlü sorunu gidermek için kullanışlıdır.
   Daha fazla ayrıntı için [Azure portal dikey penceresi kullanılarak işlem hatlarını izleme ve yönetme](data-factory-monitor-manage-pipelines.md) makalesine bakın.

> [!IMPORTANT]
> Merhaba dilim başarıyla işlendiğinde hello girdi dosyası silinir. Bu nedenle, toorerun hello dilim istediğiniz veya öğreticiyi yeniden Merhaba, hello adfgetstarted kapsayıcısının hello girdi dosyasını (input.log) toohello inputdata klasörüne yükleyin.
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a>İzleme ve Yönetme Uygulamasını kullanarak işlem hattını izleme
İzleyicisi'ni kullanın ve uygulama toomonitor hatlarınızı yönetme. Bu uygulamanın kullanımına ilişkin ayrıntılı bilgi için bkz. [İzleme ve Yönetme Uygulamasını kullanarak Azure Data Factory işlem hatlarını izleme ve yönetme](data-factory-monitor-manage-app.md).

1. Tıklatın **İzleyici & Yönet** döşeme hello veri fabrikanızın giriş sayfasında.

    ![İzleme ve Yönetme kutucuğu](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. **İzleme ve Yönetme uygulaması**’nı görmeniz gerekir. Değişiklik hello **başlangıç zamanı** ve **bitiş saati** toomatch başlangıç ve bitiş zamanları, ardışık ve tıklatın **Uygula**.

    ![İzleme ve Yönetme Uygulaması](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. Bir etkinlik penceresinde hello seçin **etkinlik Windows** toosee ayrıntılarını listeler.

    ![Etkinlik penceresi ayrıntıları](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

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

## <a name="see-also"></a>Ayrıca Bkz.
| Konu | Açıklama |
|:--- |:--- |
| [İşlem hatları](data-factory-create-pipelines.md) |Bu makalede, işlem hatlarının ve etkinliklerin Azure Data Factory anlamanıza yardımcı olur ve nasıl toouse bunları tooconstruct uçtan uca veri odaklı iş akışlarının senaryo veya iş. |
| [Veri kümeleri](data-factory-create-datasets.md) |Bu makale, Azure Data Factory’deki veri kümelerini anlamanıza yardımcı olur. |
| [Zamanlama ve yürütme](data-factory-scheduling-and-execution.md) |Bu makalede Azure Data Factory uygulama modelinin hello zamanlama ve yürütme yönleri açıklanmaktadır. |
| [İzleme Uygulaması kullanılarak işlem hatlarını izleme ve yönetme](data-factory-monitor-manage-app.md) |Bu makalede nasıl toomonitor, yönetme ve hatalarını ayıklama işlem hatlarını izleme ve yönetim uygulaması hello kullanarak. |
