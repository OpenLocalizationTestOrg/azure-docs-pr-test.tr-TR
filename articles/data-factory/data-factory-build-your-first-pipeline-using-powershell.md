---
title: aaaBuild ilk data factory'nizi (PowerShell) | Microsoft Docs
description: "Bu öğreticide Azure PowerShell kullanarak örnek bir Azure Data Factory işlem hattı oluşturursunuz."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 22ec1236-ea86-4eb7-b903-0e79a58b90c7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 626260798b56d590577b3c4b24f7cf52873c9f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a>Öğretici: Azure PowerShell kullanarak ilk Azure data factory’nizi derleme
> [!div class="op_single_selector"]
> * [Genel bakış ve önkoşullar](data-factory-build-your-first-pipeline.md)
> * [Azure portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager Şablonu](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

Bu makalede, ilk Azure data factory'nizi Azure PowerShell toocreate kullanın. diğer araçlar/SDK, kullanarak toodo hello öğretici seçin hello seçeneklerden birini hello aşağı açılan listeden.

Bu öğreticide Hello ardışık bir etkinlik vardır: **Hdınsight Hive etkinliği**. Bu etkinlik dönüşümler veri tooproduce çıkış veri girişi bir Azure Hdınsight kümesinde bir hive betiği çalıştırır. Başlangıç ve bitiş zamanlarını hello arasında bir ay belirtilen sonra hello ardışık düzen zamanlanmış toorun ' dir. 

> [!NOTE]
> Bu öğreticide Hello veri ardışık giriş verisi tooproduce çıktı verilerini dönüştürür. Bir kaynak veri deposu tooa hedef veri deposundan veri kopyalamaz. Nasıl bir öğretici için Azure Data Factory kullanarak toocopy verileri görmek [Öğreticisi: Blob Storage tooSQL veritabanı ' veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Bir işlem hattında birden fazla etkinlik olabilir. Ve hello çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir. Daha fazla bilgi için bkz. [Data Factory'de zamanlama ve yürütme](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

## <a name="prerequisites"></a>Ön koşullar
* Okuyun [öğreticiye genel bakış](data-factory-build-your-first-pipeline.md) makale ve tam hello **önkoşul** adımları.
* ' Ndaki yönergeleri izleyin [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) makale tooinstall en son sürümü Azure PowerShell, bilgisayarınızda.
* (isteğe bağlı) Bu makalede, tüm hello Data Factory cmdlet'lerini kapsamaz. Data Factory cmdlet’leri hakkında kapsamlı bilgi için bkz. [Data Factory Cmdlet Başvurusu](/powershell/module/azurerm.datafactories).

## <a name="create-data-factory"></a>Veri fabrikası oluşturma
Bu adımda, Azure PowerShell toocreate adlı bir Azure Data Factory kullandığınız **FirstDataFactoryPSH**. Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir. İşlem hattında bir veya daha fazla etkinlik olabilir. Örneğin, bir kopyalama etkinliği toocopy verilerinden bir kaynak tooa hedef veri deposu ve Hdınsight Hive etkinliği toorun bir Hive betiği tootransform verileri girin. Bu adımda hello data factory oluşturmayla başlayalım.

1. Azure PowerShell'i başlatın ve hello aşağıdaki komutu çalıştırın. Bu öğreticide hello sonuna kadar Azure PowerShell'i açık tutun. Kapatıp yeniden açın, toorun bu komutları yeniden gerekir.
   * Merhaba aşağıdaki komutu çalıştırın ve hello kullanıcı adı ve parola toosign toohello Azure portal kullanın girin.
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * Bu hesap için tüm hello abonelikleri komutu tooview aşağıdaki hello çalıştırın.
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * Çalışma hello aşağıdaki toowork ile istediğiniz tooselect hello abonelik komutu. Bu abonelik olması hello hello Azure portalında kullanılanla hello gibi aynı.
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. Adlı bir Azure kaynak grubu oluşturma **ADFTutorialResourceGroup** hello aşağıdaki komutu çalıştırarak:
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    Merhaba bu öğreticideki adımlardan bazıları ADFTutorialResourceGroup adlı hello kaynak grubunu kullandığınızı varsayar. Farklı bir kaynak grubu kullanıyorsanız, toouse gerekir, bu öğreticide ADFTutorialResourceGroup yerine.
3. Merhaba çalıştırmak **New-AzureRmDataFactory** adlı bir veri fabrikası oluşturur cmdlet **FirstDataFactoryPSH**.

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
Hello aşağıdaki noktaları göz önünde bulundurun:

* Merhaba hello Azure Data Factory adı küresel olarak benzersiz olmalıdır. Merhaba hata alırsanız **veri fabrikası adı "FirstDataFactoryPSH" kullanılabilir değil**, hello adını (örneğin, yournameFirstDataFactoryPSH) değiştirin. Bu öğreticide adımları uygularken ADFTutorialFactoryPSH yerine bu adı kullanın. Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.
* toocreate Data Factory örnekleri toobe katılımcı/yönetici rolünüz hello Azure aboneliği gerekir
* Merhaba veri fabrikasının Hello adı hello gelecekte bir DNS adı olarak kayıtlı ve bu nedenle herkese görünür hale gelmiştir.
* Merhaba hatayı alırsanız: "**Bu abonelik, Microsoft.DataFactory kayıtlı toouse ad değil**" Merhaba aşağıdakilerden birini yapın ve yeniden yayımlamayı deneyin:

  * Azure PowerShell'de komut tooregister hello Data Factory sağlayıcısının aşağıdaki hello çalıştırın:

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      Bu Data Factory sağlayıcısının kayıtlı hello komutu tooconfirm aşağıdaki hello çalıştırabilirsiniz:

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Oturum açma kullanılarak hello hello Azure aboneliğinize [Azure portal](https://portal.azure.com) ve tooa Data Factory dikey penceresine gidin (veya) hello Azure portalında bir data factory oluşturun. Bu eylemin hello sağlayıcıyı sizin için otomatik olarak kaydeder.

Bir işlem hattı oluşturmadan önce toocreate birkaç Data Factory varlıklarını önce gerekir. Bağlı hizmetler toolink veri depolarını/işlemlerini tooyour veri depolamak, giriş tanımlayın ve çıktı veri kümeleri toorepresent girdi/çıktı verilerini bağlı veri depolarında ve ardından bu veri kümeleri kullanan bir etkinlik hello işlem hattı oluşturma ilk oluşturduğunuzda.

## <a name="create-linked-services"></a>Bağlı hizmetler oluşturma
Bu adımda, Azure Storage hesabınızı ve bir isteğe bağlı Azure Hdınsight küme tooyour data factory bağlayın. Azure depolama hesabı bu örnekteki hello ardışık düzeni için girdi ve çıktı verilerini ayrı tutma hello hello. Merhaba Hdınsight bağlı hizmeti kullanılan toorun hello ardışık bu örnekteki hello etkinliğinde belirtilen Hive betiği ' dir. Hangi veri deposu/işlem Hizmetleri senaryonuzda kullanılır ve bağlı hizmetler oluşturarak bu hizmetleri toohello veri fabrikası bağlantı.

### <a name="create-azure-storage-linked-service"></a>Azure Storage bağlı hizmeti oluşturma
Bu adımda, Azure depolama hesabı tooyour veri fabrikanıza bağlayın. Merhaba kullandığınız aynı Azure Storage hesabı toostore girdi/çıktı verilerin ve HQL hello komut dosyası.

1. İçerik C:\adfgetstartedpsh hello C:\ADFGetStarted klasöründe aşağıdaki hello ile adlı bir JSON dosyası oluşturun. Zaten yoksa ADFGetStarted hello klasörünü oluşturun.

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
    Değiştir **hesap adı** hello Azure depolama hesabınızın adını içeren ve **hesap anahtarı** hello erişim anahtarı hello Azure depolama hesabı olan. toolearn tooget depolama alanınızın erişim nasıl anahtar, hello bilgi nasıl tooview, kopyalama ve yeniden oluşturma depolama erişim anahtarları içinde hakkında [depolama hesabınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
2. Azure PowerShell'de toohello ADFGetStarted klasörüne geçin.
3. Merhaba kullanabilirsiniz **New-AzureRmDataFactoryLinkedService** bağlı hizmet oluşturur cmdlet'i. Bu cmdlet ve diğer Data Factory cmdlet'leri Bu öğreticide kullandığınız gerektirir toopass değerleri Merhaba *ResourceGroupName* ve *DataFactoryName* parametreleri. Alternatif olarak, kullanabileceğiniz **Get-AzureRmDataFactory** tooget bir **DataFactory** nesne ve hello nesne yazmadan nesneyi geçirmek *ResourceGroupName* ve  *DataFactoryName* her bir cmdlet'i çalıştırın. Çalışma hello şu komutu tooassign hello hello çıktısını **Get-AzureRmDataFactory** cmdlet tooa **$df** değişkeni.

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. Şimdi, hello çalıştırın **New-AzureRmDataFactoryLinkedService** hello oluşturur cmdlet bağlı **StorageLinkedService** hizmet.

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    Merhaba çalıştırırsanız çalıştırmadıysanız **Get-AzureRmDataFactory** cmdlet'i ve atanan hello çıkış toohello **$df** hello toospecify değerlerini olurdu değişken, *ResourceGroupName*ve *DataFactoryName* aşağıdaki gibi parametreleri.

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    Başlangıç Öğreticisi hello ortadaki Azure PowerShell'i kapatırsanız, toorun hello sahip **Get-AzureRmDataFactory** cmdlet, Azure PowerShell toocomplete hello öğreticinin sonraki başlatışınızda.

### <a name="create-azure-hdinsight-linked-service"></a>Azure HDInsight bağlı hizmeti oluşturma
Bu adımda, bir isteğe bağlı Hdınsight kümesi tooyour data factory bağlayın. Merhaba Hdınsight küme otomatik olarak çalışma zamanında oluşturulur ve hello belirtilen süre boyunca işlem yapma ve boşta bittikten sonra silinir. İsteğe bağlı HDInsight kümesi yerine kendi HDInsight kümenizi kullanabilirsiniz. Ayrıntılar için bkz. [İşlem Bağlı Hizmetleri](data-factory-compute-linked-services.md).

1. Adlı bir JSON dosyası oluşturun **Hdınsightondemandlinkedservice**hello .json **C:\ADFGetStarted** içeriği aşağıdaki hello klasörüyle.

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
                "linkedServiceName": "StorageLinkedService"
            }
        }
    }
    ```
    Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:

   | Özellik | Açıklama |
   |:--- |:--- |
   | ClusterSize |Merhaba Hdınsight kümesi Hello boyutunu belirtir. |
   | TimeToLive |Silinmeden önce hello Hdınsight kümesi, o hello boşta kalma süresini belirtir. |
   | linkedServiceName |Hdınsight tarafından oluşturulan kullanılan toostore hello günlükleri olan hello depolama hesabını belirtir |

    Hello aşağıdaki noktaları göz önünde bulundurun:

   * Merhaba Data Factory oluşturur bir **Linux tabanlı** hello JSON ile sizin için Hdınsight kümesi. Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).
   * İsteğe bağlı HDInsight kümesi yerine **kendi HDInsight kümenizi** kullanabilirsiniz. Ayrıntılar için bkz. [HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).
   * Merhaba Hdınsight kümesi oluşturur bir **varsayılan kapsayıcı** hello JSON belirtilen hello blob depolamada (**linkedServiceName**). Hdınsight Hello küme silindiğinde bu kapsayıcıyı silmez. Bu davranış tasarım gereğidir. İsteğe bağlı HDInsight bağlı hizmeti kullanıldığında, mevcut canlı bir küme olmadığı sürece bir dilim her işlendiğinde bir HDInsight kümesi oluşturulur (**timeToLive**). Merhaba işlem bittiğinde hello küme otomatik olarak silinir.

       Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz. Bunları hello işlerin sorunları giderilmesi için ihtiyacınız yoksa, toodelete isteyebilirsiniz bunları tooreduce hello depolama maliyeti. Bu kapsayıcıların Hello adları izleyen bir desen: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Gibi araçlar kullanın [Microsoft Storage Gezgini](http://storageexplorer.com/) toodelete kapsayıcılarında Azure blob depolama.

     Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).
2. Merhaba çalıştırmak **New-AzureRmDataFactoryLinkedService** hello oluşturur cmdlet bağlantılı Hdınsightondemandlinkedservice adlı hizmeti.
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a>Veri kümeleri oluşturma
Bu adımda, veri kümeleri toorepresent hello girişi oluşturun ve Hive işlenmesi için verileri çıktı. Bu veri kümeleri toohello başvuran **StorageLinkedService** Bu öğreticide daha önce oluşturduğunuz. bağlantılı hizmet noktaları tooan Azure depolama hesabı hello ve veri kümeleri, giriş tutan hello depolamada kapsayıcı, klasör, dosya adı belirtin ve çıktı verilerini.

### <a name="create-input-dataset"></a>Girdi veri kümesi oluşturma
1. Adlı bir JSON dosyası oluşturun **C:\adfgetstarted** hello içinde **C:\ADFGetStarted** içeriği aşağıdaki hello klasörüyle:

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "StorageLinkedService",
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
    Merhaba JSON adlı veri kümesini tanımlayan **Azureblobınput**, hello ardışık düzeninde bir etkinliğin girdi verilerini temsil eder. Ayrıca, hello giriş verisi adlı hello blob kapsayıcısında bulunur belirtir **adfgetstarted** ve adlı hello klasör **inputdata**.

    Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:

   | Özellik | Açıklama |
   |:--- |:--- |
   | type |verileri Azure blob depolamada yer aldığından hello type özelliği tooAzureBlob ayarlanır. |
   | linkedServiceName |daha önce oluşturduğunuz StorageLinkedService toohello başvuruyor. |
   | fileName |Bu özellik isteğe bağlıdır. Bu özelliği atarsanız, hello folderPath tüm hello dosyalarından çekilir. Bu durumda, yalnızca hello input.log işlenir. |
   | type |Merhaba günlük dosyaları metin biçiminde olduğundan TextFormat kullanacağız. |
   | columnDelimiter |Merhaba günlük dosyalarındaki sütunlar hello virgül karakteriyle (,) sınırlandırılmıştır. |
   | frequency/interval |tooMonth sıklığını ve aralığı hello girdi dilimlerinin aylık olarak kullanılabileceğini 1. |
   | external |Merhaba giriş verisi hello Data Factory hizmetiyle oluşturulmadıysa, bu özellik tootrue ayarlanır. |
2. Azure PowerShell toocreate hello Data Factory veri kümesi komutunda aşağıdaki hello çalıştırın:

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a>Çıktı veri kümesi oluşturma
Şimdi, hello çıkış veri kümesi toorepresent hello çıktı verilerini hello Azure Blob Depolama depolanan oluşturun.

1. Adlı bir JSON dosyası oluşturun **C:\adfgetstarted** hello içinde **C:\ADFGetStarted** içeriği aşağıdaki hello klasörüyle:

    ```json
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
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
    Merhaba JSON adlı veri kümesini tanımlayan **AzureBlobOutput**, hello ardışık düzeninde bir etkinliğin çıktı verilerini temsil eder. Ayrıca, hello sonuçları adlı hello blob kapsayıcısında depolanır belirtir **adfgetstarted** ve adlı hello klasör **partitioneddata**. Merhaba **kullanılabilirlik** bölümü belirtiyor bu hello çıktı veri kümesi, aylık olarak oluşturulur.
2. Azure PowerShell toocreate hello Data Factory veri kümesi komutunda aşağıdaki hello çalıştırın:

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a>İşlem hattı oluşturma
Bu adımda, **HDInsightHive** etkinliğiyle ilk işlem hattınızı oluşturursunuz. Girdi dilimi kullanılabilir aylık (sıklığı: Month, interval: 1), çıktı diliminin ayda bir oluşturulduğunu ve hello etkinlik hello Zamanlayıcı özelliğinin de toomonthly ayarlayın. Merhaba çıktı veri kümesi ve hello etkinlik Zamanlayıcı Hello ayarlarının eşleşmesi gerekir. Şu anda, çıktı veri kümesi hello etkinlik herhangi bir çıktı üretmez olsa bile bir çıkış veri kümesi oluşturmanız gerekir böylece hangi sürücüleri zamanlama, hello değil. Merhaba etkinlik herhangi bir girdi almazsa oluşturma hello girdi veri kümesi atlayabilirsiniz. JSON aşağıdaki hello kullanılan hello özellikleri hello bu bölümün sonuna açıklanmıştır.

1. İçerik aşağıdaki hello ile Merhaba C:\ADFGetStarted klasöründe MyFirstPipelinePSH.json adlı bir JSON dosyası oluşturun:

   > [!IMPORTANT]
   > Değiştir **storageaccountname** depolama hesabınızdaki hello JSON hello adı.
   >
   >

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
                        "scriptLinkedService": "StorageLinkedService",
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

    Merhaba Hive betik dosyası **partitionweblogs.hql**, hello Azure depolama hesabı depolanır (adlı hello scriptLinkedService tarafından belirtilen **StorageLinkedService**) ve **komut dosyası**  hello kapsayıcı klasöründe **adfgetstarted**.

    Merhaba **tanımlar** bölümdür olması kullanılan toospecify hello çalışma zamanı ayarları toohello hive betiğini Hive yapılandırma değerleri olarak geçirilen (örn., ${hiveconf: inputtable}, ${hiveconf}).

    Merhaba **Başlat** ve **son** hello ardışık düzen özelliklerini hello etkin dönem hello ardışık belirtir.

    Bu hello Hive betiğini hello tarafından belirtilen hello işlem üzerinde çalıştığı belirtin Hello JSON etkinliğinde **linkedServiceName** – **Hdınsightondemandlinkedservice**.

   > [!NOTE]
   > "Ardışık düzen JSON" bölümüne bakın [işlem hatlarının ve etkinliklerin Azure Data Factory](data-factory-create-pipelines.md) hello örnekte kullanılan JSON özellikleri hakkında ayrıntılı bilgi için.

2. Merhaba gördüğünüzü onaylayın **input.log** hello dosyasında **adfgetstarted/inputdata** hello Azure blob depolama ve komut toodeploy hello ardışık aşağıdaki çalışma hello klasöründe. Merhaba itibaren **Başlat** ve **son** hello son kez ayarlanır ve **isPaused** dağıtıldıktan hemen sonra kümesi toofalse, hello ardışık düzen (Merhaba ardışık düzeninde etkinlik) çalışması olduğu.

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. Tebrikler, Azure PowerShell kullanarak ilk işlem hattınızı başarıyla oluşturdunuz.

## <a name="monitor-pipeline"></a>İşlem hattını izleme
Bu adımda, bir Azure data factory'de neler olduğunu Azure PowerShell toomonitor kullanın.

1. Çalıştırma **Get-AzureRmDataFactory** ve hello çıktı tooa Ata **$df** değişkeni.

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. Çalıştırma **Get-AzureRmDataFactorySlice** hello tüm dilimleri hakkında bilgi tooget **EmpSQLTable**, hello ardışık hello çıktı tablosu.

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    Bu hello burada belirttiğiniz StartDateTime aynı hello ile JSON işlem hattında belirtilen başlangıç zamanıyla hello olduğuna dikkat edin. Merhaba örnek çıktı aşağıda verilmiştir:

    ```PowerShell
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : FirstDataFactoryPSH
    DatasetName       : AzureBlobOutput
    Start             : 7/1/2017 12:00:00 AM
    End               : 7/2/2017 12:00:00 AM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. Çalıştırma **Get-AzureRmDataFactoryRun** tooget hello etkinliğinin ayrıntılarını belirli bir dilimle ilgili çalıştırır.

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    Merhaba örnek çıktı aşağıda verilmiştir: 

    ```PowerShell
    Id                  : 0f6334f2-d56c-4d48-b427-d4f0fb4ef883_635268096000000000_635292288000000000_AzureBlobOutput
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : FirstDataFactoryPSH
    DatasetName         : AzureBlobOutput
    ProcessingStartTime : 12/18/2015 4:50:33 AM
    ProcessingEndTime   : 12/31/9999 11:59:59 PM
    PercentComplete     : 0
    DataSliceStart      : 7/1/2017 12:00:00 AM
    DataSliceEnd        : 7/2/2017 12:00:00 AM
    Status              : AllocatingResources
    Timestamp           : 12/18/2015 4:50:33 AM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : RunSampleHiveActivity
    PipelineName        : MyFirstPipeline
    Type                : Script
    ```
    Merhaba dilimi görene kadar bu cmdlet çalışmaya devam **hazır** durumu veya **başarısız** durumu. Merhaba dilim hazır durumunda olduğunda hello denetleyin **partitioneddata** hello klasöründe **adfgetstarted** hello için blob depolama alanınızın kapsayıcısında çıkış verileri.  İsteğe bağlı HDInsight kümesinin oluşturulması genellikle biraz zaman alır.

    ![çıktı verileri](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> İsteğe bağlı HDInsight kümesinin oluşturulması genellikle biraz zaman alır (yaklaşık 20 dakika). Bu nedenle, hello ardışık düzen tootake beklediğiniz **yaklaşık olarak 30 dakika** tooprocess hello dilim.
>
> Merhaba dilim başarıyla işlendiğinde hello girdi dosyası silinir. Bu nedenle, toorerun hello dilim istediğiniz veya öğreticiyi yeniden Merhaba, hello adfgetstarted kapsayıcısının hello girdi dosyasını (input.log) toohello inputdata klasörüne yükleyin.
>
>

## <a name="summary"></a>Özet
Bu öğreticide, bir Hdınsight hadoop kümesindeki Hive betiği çalıştıran bir Azure data factory tooprocess veri oluşturuldu. Hello Data Factory Düzenleyici'hello Azure portal toodo hello aşağıdaki adımları kullanılır:

1. Oluşturulan Azure **data factory**.
2. Oluşturulan iki **bağlı hizmet**:
   1. **Azure depolama** hizmet toolink toohello veri fabrikası girdi/çıktı dosyalarını tutan Azure blob depolama alanınızın bağlı.
   2. **Azure Hdınsight** isteğe bağlı bir isteğe bağlı Hdınsight Hadoop küme toohello data factory hizmeti toolink bağlı. Azure Data Factory Hdınsight Hadoop küme yalnızca zaman tooprocess giriş verileri hem de üretim çıktı verilerini oluşturur.
3. Oluşturulan iki **veri kümeleri**, hello ardışık düzende Hdınsight Hive etkinliğiyle ilgili girdi ve çıktı verilerini açıklayan.
4. **HDInsight Hive** etkinliğine sahip oluşturulan bir **işlem hattı**.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, isteğe bağlı Azure HDInsight kümesinde bir Hive betiği çalıştıran dönüştürme etkinliğine (HDInsight Etkinliği) sahip işlem hattı oluşturdunuz. toouse Azure Blob tooAzure SQL, bir kopyalama etkinliği toocopy verileri nasıl görürüm toosee [öğretici: bir Azure Blob tooAzure SQL veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="see-also"></a>Ayrıca Bkz.
| Konu | Açıklama |
|:--- |:--- |
| [Data Factory Cmdlet Başvurusu](/powershell/module/azurerm.datafactories) |Data Factory cmdlet'leri hakkında kapsamlı belgelere bakma |
| [İşlem hatları](data-factory-create-pipelines.md) |Bu makalede, işlem hatlarının ve etkinliklerin Azure Data Factory anlamanıza yardımcı olur ve nasıl toouse bunları tooconstruct uçtan uca veri odaklı iş akışlarının senaryo veya iş. |
| [Veri kümeleri](data-factory-create-datasets.md) |Bu makale, Azure Data Factory’deki veri kümelerini anlamanıza yardımcı olur. |
| [Zamanlama ve Yürütme](data-factory-scheduling-and-execution.md) |Bu makalede Azure Data Factory uygulama modelinin hello zamanlama ve yürütme yönleri açıklanmaktadır. |
| [İzleme Uygulaması kullanılarak işlem hatlarını izleme ve yönetme](data-factory-monitor-manage-app.md) |Bu makalede nasıl toomonitor, yönetme ve hatalarını ayıklama işlem hatlarını izleme ve yönetim uygulaması hello kullanarak. |
