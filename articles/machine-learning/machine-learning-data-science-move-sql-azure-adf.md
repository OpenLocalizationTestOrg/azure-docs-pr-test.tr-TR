---
title: "bir şirket içi SQL Server tooSQL Azure Data Factory ile Azure aaaMove verilerden | Microsoft Docs"
description: "Merhaba bulutta içi veritabanları arasında verileri günlük olarak birlikte taşımak iki veri taşıma etkinlikleri oluşturur bir ADF ardışık ayarlayın."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 7f7e78c7a84a259539221d3235b76bb5a3cf9866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-sql-server-toosql-azure-with-azure-data-factory"></a>Bir şirket içi SQL server tooSQL Azure Azure Data Factory ile veri taşıma
Bu konu, Azure Blob Storage kullanarak aracılığıyla bir şirket içi SQL Server veritabanı tooa SQL Azure veritabanı toomove verileri Azure veri fabrikası (ADF) nasıl hello gösterir.

Taşıma veri tooan Azure SQL veritabanı için çeşitli seçenekler özetler bir tablo için bkz: [Azure Machine Learning için verileri tooan Azure SQL veritabanı taşıma](machine-learning-data-science-move-sql-azure.md).

## <a name="intro"></a>Giriş: ADF nedir ve ne zaman kullanılan toomigrate veriler olmalıdır?
Azure Data Factory düzenler ve hello taşınmasını ve dönüştürülmesini veri otomatikleştiren bir bulut tabanlı tam olarak yönetilen bir veri tümleştirme hizmetidir. Merhaba anahtar hello ADF modelinde ardışık düzen kavramdır. Bir ardışık düzen veri kümelerinde bulunan hello verileri üzerindeki hello Eylemler tooperform tanımlar, her biri bir mantıksal etkinlikleri gruplandırmasıdır. Bağlı hizmetler Data Factory tooconnect toohello veri kaynakları için gerekli kullanılan toodefine hello bilgilerdir.

ADF ile mevcut veri işleme Hizmetleri hello bulutta yüksek oranda kullanılabilir ve yönetilen veri ardışık içine birleştirilebilir. Bu veri ardışık zamanlanmış tooingest olması, hazırlamak, dönüştürmek, analiz ve verilerini yayımlamak ve ADF yönetir ve hello karmaşık veri ve işleme bağımlılıkları yönetir. Çözümleri hızla yerleşik ve içinde dağıtılan hello bulut, şirket içi artan sayıda bağlanma ve veri kaynakları bulut değiştirebilirsiniz.

ADF kullanmayı dikkate alın:

* ne zaman gereksinimlerini toobe sürekli olarak her ikisi de erişen bir karma senaryoda geçirilen verileri şirket içi ve bulut kaynakları
* ne zaman hello veri işlem yapılan işlem veya gereksinimlerini toobe değiştirilmiş veya iş mantığı sahip Geçirilmekte olan tooit eklenmesi.

Zamanlama ve düzenli aralıklarla veri hello hareketini yönetmek basit JSON komut dosyalarını kullanarak iş izleme hello ADF sağlar. ADF karmaşık işlemleri için destek gibi diğer özellikleri de vardır. Hello belgelerine ADF hakkında daha fazla bilgi için bkz: [Azure veri fabrikası (ADF)](https://azure.microsoft.com/services/data-factory/).

## <a name="scenario"></a>Merhaba senaryosu
İki veri taşıma etkinlikleri oluşturur bir ADF ardışık ayarlarız. Birlikte bunlar verileri günlük olarak bir şirket içi SQL database ve Azure SQL Database hello bulutta arasında taşıyın. Merhaba iki etkinlik şunlardır:

* bir şirket içi SQL Server veritabanı tooan Azure Blob Storage hesabı veri kopyalama
* verileri hello Azure Blob Storage hesabı tooan ' Azure SQL veritabanı kopyalayın.

> [!NOTE]
> Merhaba burada olmuştur hello ADF ekibi tarafından sağlanan öğretici ayrıntılı hello gelen uyarlanmış gösterilen adımlar: [şirket içi kaynakları ve veri yönetimi ağ geçidi ile bulut arasında veri taşıma](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) başvuran toohello bu konunun ilgili bölümleri uygun olduğunda sağlanır.
>
>

## <a name="prereqs"></a>Önkoşullar
Bu öğretici, sahip olduğunuz varsayılmaktadır:

* Bir **Azure aboneliği**. Bir aboneliğiniz yoksa [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.
* Bir **Azure depolama hesabı**. Bu öğreticide hello verileri depolamak için bir Azure depolama hesabı kullanın. Bir Azure depolama hesabınız yoksa, hello bkz [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) makalesi. Merhaba depolama hesabı oluşturduktan sonra anahtarı tooaccess hello depolama kullanılan tooobtain hello hesabınızın olması gerekir. Bkz: [depolama erişim tuşlarınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Erişim tooan **Azure SQL veritabanı**. Bir Azure SQL veritabanı ayarlanması, tpoic hello [Microsoft Azure SQL veritabanı ile çalışmaya başlama ](../sql-database/sql-database-get-started.md) ilgili bilgiler verilmektedir tooprovision bir Azure SQL veritabanına yeni bir örneğini.
* Yüklenmiş ve yapılandırılmış **Azure PowerShell** yerel olarak. Yönergeler için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

> [!NOTE]
> Bu yordam hello kullanır [Azure portal](https://portal.azure.com/).
>
>

## <a name="upload-data"></a>Karşıya yükleme hello veri tooyour içi SQL Server
Merhaba kullanırız [NYC ücreti dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) toodemonstrate hello geçiş işlemi. Merhaba NYC ücreti dataset Azure blob depolama o post belirtildiği gibi kullanılabilir [NYC ücreti verileri](http://www.andresmh.com/nyctaxitrips/). Hello veri iki dosya, seyahat ayrıntılarını içeren, hello trip_data.csv dosyası ve her seyahat için ücretli hello ücreti ayrıntılarını içeren hello trip_far.csv dosyası vardır. Bir örnek ve bu dosyaların açıklaması sağlanan [NYC ücreti dönüşleri veri kümesi tanımı](machine-learning-data-science-process-sql-walkthrough.md#dataset).

Burada, kendi veri kümesini tooa sağlanan hello yordamı uyarlamak veya hello NYC ücreti dataset kullanarak açıklandığı gibi hello adımları izleyin. tooupload Merhaba, şirket içi SQL Server veritabanınızın NYC ücreti kümesine özetlenen hello yordamı izleyin [toplu içeri aktarma verileri SQL Server veritabanına](machine-learning-data-science-process-sql-walkthrough.md#dbload). SQL Server üzerinde bir Azure sanal makine için bu yönergeleri bağlıdır, ancak şirket içi SQL Server toohello yüklemeyle hello yordamı hello aynı.

## <a name="create-adf"></a>Bir Azure Data Factory oluşturma
Merhaba hello yeni bir Azure Data Factory ve bir kaynak grubu oluşturmak için yönergeler [Azure portal](https://portal.azure.com/) sağlanan [bir Azure Data Factory oluşturmak](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory). Ad hello yeni ADF örnek *adfdsp* ve oluşturulan ad hello kaynak grubu *adfdsprg*.

## <a name="install-and-configure-up-hello-data-management-gateway"></a>Yükleme ve veri yönetimi ağ geçidi hello yapılandırma
tooenable hatlarınızı tooadd gereken bir şirket içi SQL Server ile bir Azure data factory toowork içinde bir bağlantılı hizmet toohello veri fabrikası olarak. Bağlantılı hizmeti bir şirket içi SQL Server için bir toocreate, şunları yapmalısınız:

* indirin ve Microsoft Veri Yönetimi ağ geçidi hello şirket içi bilgisayara yükleyin.
* Merhaba bağlantılı hizmeti hello şirket içi veri kaynağı toouse hello ağ geçidi için yapılandırın.

Veri Yönetimi ağ geçidi Hello serileştirir ve burada barındırılan hello bilgisayardaki hello kaynak ve havuz verileri seri durumdan çıkarır.

Kurulum yönergeleri ve veri yönetimi ağ geçidi hakkında ayrıntılar için bkz: [şirket içi kaynakları ve veri yönetimi ağ geçidi ile bulut arasında veri taşıma](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)

## <a name="adflinkedservices"></a>Bağlı hizmetler tooconnect toohello veri kaynakları oluşturun
Bağlı hizmet Azure Data Factory tooconnect tooa veri kaynağı için gerekli hello bilgilerini tanımlar. bağlı hizmetler oluşturmak için adım adım yordam hello sağlanır [bağlı hizmetler oluşturma](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).

Bağlı hizmetler gerekli olan bu senaryoda üç kaynakları sahibiz.

1. [Şirket içi SQL Server için bağlı hizmet](#adf-linked-service-onprem-sql)
2. [Azure Blob Storage için bağlı hizmet](#adf-linked-service-blob-store)
3. [Azure SQL database için bağlı hizmet](#adf-linked-service-azure-sql)

### <a name="adf-linked-service-onprem-sql"></a>Şirket içi SQL Server database için bağlı hizmet
toocreate hello bağlantılı hizmeti hello için SQL Server içi:

* Merhaba tıklatın **veri deposu** hello ADF giriş sayfasında Klasik Azure portalı üzerinde
* seçin **SQL** ve hello girin *kullanıcıadı* ve *parola* hello SQL Server şirket için kimlik bilgileri. Tooenter hello servername olarak gereken bir **tam servername ters eğik çizgi örnek adı (Sunucuadı\örnekadı)**. Ad hello bağlantılı hizmeti *adfonpremsql*.

### <a name="adf-linked-service-blob-store"></a>Blob için bağlı hizmet
toocreate hello Azure Blob Storage hesabı için bağlı hizmet hello:

* Merhaba tıklatın **veri deposu** hello ADF giriş sayfasında Klasik Azure portalı üzerinde
* seçin **Azure depolama hesabı**
* Merhaba, Azure Blob Depolama hesabı anahtarı ve kapsayıcı adı girin. Bağlantılı hizmet adı hello *adfds*.

### <a name="adf-linked-service-azure-sql"></a>Azure SQL database için bağlı hizmet
toocreate hello Azure SQL Database için bağlı hizmet hello:

* Merhaba tıklatın **veri deposu** hello ADF giriş sayfasında Klasik Azure portalı üzerinde
* seçin **Azure SQL** ve hello girin *kullanıcıadı* ve *parola* hello Azure SQL veritabanı için kimlik bilgileri. Merhaba *kullanıcıadı* olarak belirtilmelidir  *user@servername* .   

## <a name="adf-tables"></a>Tanımlayın ve tabloları toospecify oluşturun nasıl tooaccess veri kümeleri hello
Betik tabanlı yordamları izleyerek hello ile hello yapısı, konumu ve hello DataSet kullanılabilirliği belirtin tablolar oluşturun. Kullanılan toodefine hello tablolar JSON dosyalarıdır. Bu dosyaları hello yapısı hakkında daha fazla bilgi için bkz: [veri kümeleri](../data-factory/data-factory-create-datasets.md).

> [!NOTE]
> Merhaba yürütülecek `Add-AzureAccount` hello yürütmeden önce cmdlet [yeni AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) sağ Azure aboneliği hello cmdlet tooconfirm hello komutu yürütme için seçilen. Bu cmdlet belgeleri için bkz: [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).
>
>

Merhaba JSON tabanlı tanımları hello tablolardaki adlarından hello kullan:

* Merhaba **tablo adı** hello şirket içi SQL server, *nyctaxi_data*
* Merhaba **kapsayıcı adı** hello Azure Blob Depolama hesabıdır *kapsayıcı adı*  

Üç tablo tanımları bu ADF ardışık düzeni için gereklidir:

1. [SQL şirket içi tablosu](#adf-table-onprem-sql)
2. [BLOB tablosu](#adf-table-blob-store)
3. [SQL Azure tablo](#adf-table-azure-sql)

> [!NOTE]
> Bu yordamları Azure PowerShell toodefine kullanın ve ADF etkinlikleri hello oluşturun. Ancak bu görevleri hello Azure portalı kullanılarak da gerçekleştirilebilir. Ayrıntılar için bkz [veri kümeleri oluşturma](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).
>
>

### <a name="adf-table-onprem-sql"></a>SQL şirket içi tablosu
Merhaba tablo tanımı hello için SQL Server aşağıdaki JSON dosyasına hello belirtilen şirket içi:

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

Merhaba sütun adları buraya dahil değil. Merhaba sütun adlarına göre burada ekleyerek alt seçebilirsiniz (Merhaba ayrıntıları denetlemek için [ADF belgelerine](../data-factory/data-factory-data-movement-activities.md) konu.

Merhaba JSON tanımını Merhaba tablonun adlı bir dosyaya kopyalama *onpremtabledef.json* dosya ve konum bilinen tooa kaydedin (burada toobe kabul *C:\temp\onpremtabledef.json*). Merhaba tablo içinde ADF ile Azure PowerShell cmdlet'i aşağıdaki hello oluşturun:

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <a name="adf-table-blob-store"></a>BLOB tablosu
(Şirket içi tooAzure blob hello alınan verileri eşler) hello aşağıdaki blob konumdur tanımı hello tablosu hello için çıktı:

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

Merhaba JSON tanımını Merhaba tablonun adlı bir dosyaya kopyalama *bloboutputtabledef.json* dosya ve konum bilinen tooa kaydedin (burada toobe kabul *C:\temp\bloboutputtabledef.json*). Merhaba tablo içinde ADF ile Azure PowerShell cmdlet'i aşağıdaki hello oluşturun:

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <a name="adf-table-azure-sq"></a>SQL Azure tablo
Merhaba tablosu hello SQL Azure çıkışı için (Bu şemayı hello blobundan gelen hello veri eşlemeleri) hello aşağıdaki tanımıdır:

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

Merhaba JSON tanımını Merhaba tablonun adlı bir dosyaya kopyalama *AzureSqlTable.json* dosya ve konum bilinen tooa kaydedin (burada toobe kabul *C:\temp\AzureSqlTable.json*). Merhaba tablo içinde ADF ile Azure PowerShell cmdlet'i aşağıdaki hello oluşturun:

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <a name="adf-pipeline"></a>Tanımlama ve hello işlem hattı oluşturma
Toohello ait hello etkinlikleri kanal ve aşağıdaki komut dosyası tabanlı yordamlarını hello ile Merhaba işlem hattı oluşturma belirtin. Kullanılan toodefine hello ardışık düzen özellikleri bir JSON dosyasıdır.

* Merhaba betik varsayar bu hello **ardışık düzen adı** olan *AMLDSProcessPipeline*.
* Ayrıca, günlük olarak ve kullanım hello varsayılan yürütme süresi hello işi (00: 00 UTC) yürütülen hello ardışık düzen toobe hello periyodikliğini ayarlarız unutmayın.

> [!NOTE]
> Merhaba aşağıdaki yordamları Azure PowerShell toodefine kullanın ve hello ADF işlem hattını oluşturun. Ancak, bu görevi Azure Portalı'nı kullanarak da gerçekleştirilebilir. Ayrıntılar için bkz [oluşturma ardışık düzen](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).
>
>

Merhaba tablo tanımları kullanarak hello ardışık düzen tanımı ADF gibi belirtilir hello için daha önce sağlanan:

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL tooAzure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server tooblob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data tooSql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

Bu JSON tanımını hello ardışık olarak adlandırılan bir dosyaya kopyalayın *pipelinedef.json* dosya ve konum bilinen tooa kaydedin (burada toobe kabul *C:\temp\pipelinedef.json*). Merhaba ardışık düzen içinde ADF ile Azure PowerShell cmdlet'i aşağıdaki hello oluşturun:

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

(Merhaba diyagramı tıklattığınızda) hello ardışık düzen ADF hello Klasik Azure Portalı'nda gösterilmesi hello üzerinde aşağıdaki gibi gördüğünüzden onaylayın

![ADF ardışık düzen](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <a name="adf-pipeline-start"></a>Merhaba ardışık düzen Başlat
Merhaba ardışık düzen komutu aşağıdaki hello kullanarak şimdi çalıştırabilirsiniz:

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

Merhaba *startdate* ve *enddate* parametre değerlerini hello ardışık düzen toorun arasında istediğiniz hello gerçek tarihlerle yerini toobe gerekir.

Merhaba ardışık düzen yürütür sonra Itanium tabanlı sistemler için mümkün toosee hello veri Göster yukarı hello blob, günde bir dosya için seçtiğiniz hello kapsayıcıda olmalıdır.

Biz ADF toopipe verilerle artımlı olarak sağlanan hello işlevselliği işlevden olmayan olduğunu unutmayın. Bu ve diğer özellikleri ADF tarafından sağlanan toodo nasıl görürüm hakkında daha fazla bilgi için hello [ADF belgelerine](https://azure.microsoft.com/services/data-factory/).
