---
title: "Öğretici: bir Azure Data Factory işlem hattı toocopy veri (Azure portalı) oluşturma | Microsoft Docs"
description: "Bu öğreticide, Azure blob depolama tooan Azure SQL veritabanına bir kopyalama etkinliği toocopy verilerle Azure portal toocreate bir Azure Data Factory işlem hattı kullanın."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d9317652-0170-4fd3-b9b2-37711272162b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fadd840fe9a15cd8831cdb25dccbd10ac42fa161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-portal-toocreate-a-data-factory-pipeline-toocopy-data"></a>Öğretici: Kullanmak Azure portal toocreate Data Factory işlem hattı toocopy veri 
> [!div class="op_single_selector"]
> * [Genel bakış ve önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Kopyalama Sihirbazı](data-factory-copy-data-wizard-tutorial.md)
> * [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager şablonu](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API’si](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

Bu makalede, bilgi nasıl toouse [Azure portal](https://portal.azure.com) toocreate data factory Azure blob depolama tooan Azure SQL veritabanına verileri kopyalayan bir işlem hattı ile. Yeni tooAzure Data Factory varsa, hello okuma [giriş tooAzure Data Factory](data-factory-introduction.md) Bu öğretici yapmadan önce makalesi.   

Bu öğreticide, içinde bir etkinlik olan işlem hattı oluşturursunuz: Kopyalama Etkinliği. Merhaba kopyalama etkinliği bir desteklenen veri deposu tooa desteklenen havuz veri deposundan verileri kopyalar. Kaynak ve havuz olarak desteklenen veri depolarının listesi için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Merhaba etkinlik verileri güvenli, güvenilir ve ölçeklenebilir bir şekilde çeşitli veri depolamaları arasında kopyalayabilirsiniz genel olarak kullanılabilir bir hizmet tarafından desteklenir. Merhaba kopyalama etkinliği hakkında daha fazla bilgi için bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).

Bir işlem hattında birden fazla etkinlik olabilir. Ve hello çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir. Daha fazla bilgi için bkz. [bir işlem hattında birden fazla etkinlik](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

> [!NOTE] 
> Merhaba veri ardışık Bu öğreticide, bir kaynak veri deposu tooa hedef veri deposundan verileri kopyalar. Nasıl bir öğretici için Azure Data Factory kullanarak tootransform verileri görmek [Öğreticisi: Hadoop kümesi kullanarak bir ardışık düzen tootransform veri derleme](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Ön koşullar
Hello listelenen önkoşulları tamamlamanız [öğretici önkoşulları](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) Bu öğreticiyi gerçekleştirmeden önce makalesi.

## <a name="steps"></a>Adımlar
Bu öğretici bir parçası olarak gerçekleştirdiğiniz hello adımlar şunlardır:

1. Azure **veri fabrikası** oluşturma. Bu adımda, ADFTutorialDataFactory adlı bir veri fabrikası oluşturursunuz. 
2. Oluşturma **bağlantılı Hizmetleri** hello veri fabrikası'nda. Bu adımda Azure Depolama ve Azure SQL Veritabanı türünde iki bağlı hizmet oluşturursunuz. 
    
    Merhaba AzureStorageLinkedService Azure depolama hesabı toohello veri fabrikanıza bağlar. Bir kapsayıcı oluşturulur ve veri toothis depolama hesabı bir parçası olarak yüklenen [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    AzureSqlLinkedService Azure SQL veritabanı toohello veri fabrikanıza bağlar. Merhaba blob depolama biriminden kopyalanan hello veriler bu veritabanında depolanır. Bu veritabanındaki SQL tablosunu, [ön koşulların](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) parçası olarak oluşturdunuz.   
3. Giriş ve çıkış oluşturma **veri kümeleri** hello veri fabrikası'nda.  
    
    Hello Azure depolama bağlı hizmeti çalışma zamanı tooconnect tooyour Azure depolama hesabı Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir. Ve hello giriş blob dataset hello kapsayıcı ve hello giriş verisi içeren hello klasörü belirtir.  

    Benzer şekilde, hello Azure SQL veritabanı bağlantılı hizmet çalışma zamanı tooconnect tooyour Azure SQL veritabanını Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir. Ve hello veritabanı toowhich hello verileri hello blob depolama biriminden hello tabloda kopyalanır hello çıktı SQL tablosu veri kümesi belirtir.
4. Oluşturma bir **ardışık düzen** hello veri fabrikası'nda. Bu adımda, kopyalama etkinliği ile bir işlem hattı oluşturursunuz.   
    
    Merhaba kopyalama etkinliği hello Azure blob depolama tooa hello Azure SQL veritabanı tablosunda bir blob veri kopyalar. Kopyalama etkinliği herhangi bir desteklenen kaynak desteklenen tooany hedefin bir ardışık düzen toocopy verileri kullanabilirsiniz. Desteklenen veri depolarının bir listesi için [veri taşıma etkinlikleri](data-factory-data-movement-activities.md#supported-data-stores-and-formats) makalesine bakın. 
5. Merhaba işlem hattını izleme. Bu adımda, **İzleyici** hello girdi ve çıktı veri kümeleri dilimlerini Azure portal kullanarak. 

## <a name="create-data-factory"></a>Veri fabrikası oluşturma
> [!IMPORTANT]
> Tam [hello öğreticisi için Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) zaten yapmadıysanız.   

Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir. İşlem hattında bir veya daha fazla etkinlik olabilir. Örneğin, bir kopyalama etkinliği toocopy verilerinden bir kaynak tooa hedef veri deposu ve Hdınsight Hive etkinliği toorun bir Hive betiği tootransform veri tooproduct çıktı verileri girin. Bu adımda hello data factory oluşturmayla başlayalım.

1. Toohello içinde oturum sonra [Azure portal](https://portal.azure.com/), tıklatın **yeni** hello sol menüsünde **veri + analiz**, tıklatıp **Data Factory**. 
   
   ![Yeni->DataFactory](./media/data-factory-copy-activity-tutorial-using-azure-portal/NewDataFactoryMenu.png)    
2. Merhaba, **yeni data factory** dikey penceresinde:
   
   1. Girin **ADFTutorialDataFactory** hello için **adı**. 
      
         ![Yeni veri fabrikası dikey penceresi](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-new-data-factory.png)
      
       Merhaba adı'hello Azure data Factory olması **genel benzersiz**. Merhaba aşağıdaki hata alırsanız, hello veri fabrikası (örneğin, yournameADFTutorialDataFactory) ve oluşturmayı yeniden deneyin hello adını değiştirin. Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.
      
           Data factory name “ADFTutorialDataFactory” is not available  
      
       ![Data Factory adı yok](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-not-available.png)
   2. Azure seçin **abonelik** toocreate hello veri fabrikası istiyor. 
   3. Hello için **kaynak grubu**, aşağıdaki adımları hello birini yapın:
      
      - Seçin **var olanı kullan**, varolan bir kaynak grubu hello aşağı açılan listeden seçin. 
      - Seçin **Yeni Oluştur**ve hello bir kaynak grubu adını girin.   
         
          Bu öğreticideki hello adımlardan bazıları hello adı kullandığınızı varsayar: **ADFTutorialResourceGroup** hello kaynak grubu için. Kaynak grupları hakkında toolearn bkz [Azure kaynaklarınızı grupları toomanage kaynağı kullanan](../azure-resource-manager/resource-group-overview.md).  
   4. Select hello **konumu** hello veri fabrikası için. Yalnızca Hello Data Factory hizmeti tarafından desteklenen bölgeler hello aşağı açılan listesinde gösterilir.
   5. Seçin **PIN toodashboard**.     
   6. **Oluştur**'a tıklayın.
      
      > [!IMPORTANT]
      > toocreate Data Factory örnekleri hello üyesi olmalıdır [veri fabrikası katkıda bulunan](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello abonelik/kaynak grubu düzeyinde rol.
      > 
      > Merhaba veri fabrikasının Hello adı hello gelecekte bir DNS adı olarak kayıtlı ve bu nedenle herkese görünür hale gelmiştir.                
      > 
      > 
3. Merhaba Panoda durumuyla döşeme hello aşağıdakilere bakın: **dağıtma veri fabrikası**. 

    ![veri fabrikası dağıtılıyor kutucuğu](media/data-factory-copy-activity-tutorial-using-azure-portal/deploying-data-factory.png)
4. Merhaba oluşturma işlemi tamamlandıktan sonra hello bkz **Data Factory** hello görüntüde gösterildiği gibi dikey.
   
   ![Data factory giriş sayfası](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-home-page.png)

## <a name="create-linked-services"></a>Bağlı hizmetler oluşturma
Verilerinizi depolayan ve Hizmetleri toohello veri fabrikası işlem bir veri fabrikası toolink bağlı hizmetler oluşturma. Bu öğreticide, Azure HDInsight veya Azure Data Lake Analytics gibi herhangi bir işlem hizmeti kullanmazsınız. Azure Depolama (kaynak) ve Azure SQL Veritabanı (hedef) türünde iki veri deposu kullanırsınız. 

Bu nedenle, AzureStorage ve AzureSqlDatabase türlerinde AzureStorageLinkedService ve AzureSqlLinkedService adlı iki bağlı hizmet oluşturursunuz.  

Merhaba AzureStorageLinkedService Azure depolama hesabı toohello veri fabrikanıza bağlar. Bu depolama hesap hello biri, hangi, kapsayıcı oluşturuldu ve hello veri parçası olarak yüklenen [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

AzureSqlLinkedService Azure SQL veritabanı toohello veri fabrikanıza bağlar. Merhaba blob depolama biriminden kopyalanan hello veriler bu veritabanında depolanır. Bu veritabanında hello emp tablosunda bir parçası olarak oluşturulan [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).  

### <a name="create-azure-storage-linked-service"></a>Azure Storage bağlı hizmeti oluşturma
Bu adımda, Azure depolama hesabı tooyour veri fabrikanıza bağlayın. Bu bölümde hello adı ve Azure depolama hesabınızın anahtarı belirtin.  

1. Merhaba, **Data Factory** dikey penceresinde tıklatın **yazar ve dağıtma** döşeme.
   
   ![Geliştir ve Dağıt Kutucuğu](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-author-deploy-tile.png) 
2. Merhaba gördüğünüz **Data Factory düzenleyici** hello görüntü aşağıdaki gösterildiği gibi: 

    ![Data Factory Düzenleyicisi](./media/data-factory-copy-activity-tutorial-using-azure-portal/data-factory-editor.png)
3. Merhaba Düzenleyicisi'nde tıklatın **yeni veri deposu** hello araç ve Seç düğmesini **Azure depolama** hello açılan menüsünden. Merhaba sağ bölmede Azure depolama bağlı hizmeti oluşturmak için hello JSON şablonunu görmeniz gerekir. 
   
    ![Düzenleyici Yeni veri deposu düğmesi](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-newdatastore-button.png)    
3. Değiştir `<accountname>` ve `<accountkey>` hello hesap adı ve hesap anahtarı değerleriyle Azure depolama hesabınız ile. 
   
    ![Düzenleyici Blob Storage JSON](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-json.png)    
4. Tıklatın **dağıtma** hello araç. Dağıtılan hello görmelisiniz **AzureStorageLinkedService** hello ağacında şimdi görüntüleyin. 
   
    ![Düzenleyici Blob Storage Dağıtma](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-deploy.png)

    Merhaba bağlantılı hizmet tanımında JSON özellikleri hakkında daha fazla bilgi için bkz: [Azure Blob Storage bağlayıcı](data-factory-azure-blob-connector.md#linked-service-properties) makalesi.

### <a name="create-a-linked-service-for-hello-azure-sql-database"></a>Hello Azure SQL Database için bağlı hizmet oluşturma
Bu adımda, Azure SQL veritabanı tooyour veri fabrikanıza bağlayın. Bu bölümde hello Azure SQL sunucu adı, veritabanı adı, kullanıcı adı ve parola belirtin. 

1. Merhaba, **Data Factory düzenleyici**, tıklatın **yeni veri deposu** hello araç ve Seç düğmesini **Azure SQL veritabanı** hello açılan menüsünden. Merhaba sağ bölmede hello Azure SQL bağlı hizmeti oluşturmak için hello JSON şablonunu görmeniz gerekir.
2. `<servername>`, `<databasename>`, `<username>@<servername>` ve `<password>` öğesini Azure SQL sunucusu, veritabanı, kullanıcı hesabı ve parolası ile değiştirin. 
3. Tıklatın **dağıtma** araç toocreate hello ve hello dağıtmak **AzureSqlLinkedService**.
4. Gördüğünüzü onaylayın **AzureSqlLinkedService** altında hello ağaç görünümünde **bağlantılı Hizmetleri**.  

    Bu JSON özellikleri hakkında daha fazla bilgi için [Azure SQL Veritabanı bağlayıcısı](data-factory-azure-sql-connector.md#linked-service-properties) makalesine bakın.

## <a name="create-datasets"></a>Veri kümeleri oluşturma
Merhaba önceki adımda, Azure Storage hesabını ve Azure SQL veritabanı tooyour veri fabrikası bağlı hizmetler toolink oluşturuldu. Bu adımda, iki veri kümesi InputDataset ve giriş temsil OutputDataset ve sırasıyla AzureStorageLinkedService ve Azuresqllinkedservice'in başvurduğu hello veri depolarında depolanan çıktı verilerini adlı tanımlayın.

Hello Azure depolama bağlı hizmeti çalışma zamanı tooconnect tooyour Azure depolama hesabı Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir. Ve hello giriş blob veri kümesi (InputDataset) hello kapsayıcı ve hello giriş verisi içeren hello klasörü belirtir.  

Benzer şekilde, hello Azure SQL veritabanı bağlantılı hizmet çalışma zamanı tooconnect tooyour Azure SQL veritabanını Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir. Ve kopyalanan verileri hello blob depolama biriminden hello veritabanı toowhich hello SQL tablosu veri kümesi (OututDataset) hello tabloda hello çıktı. 

### <a name="create-input-dataset"></a>Girdi veri kümesi oluşturma
Bu adımda, tooa blob dosya (emp.txt) işaret InputDataset adlı bir veri hello kök klasöründe bir blob kapsayıcısını (adftutorial) hello Azure hello AzureStorageLinkedService bağlı hizmeti tarafından temsil edilen depolama oluşturun. Verme hello dosya adı için bir değer belirtin (veya atlayın) hello giriş klasöründeki tüm blob'lara ait veriler kopyalanan toohello hedef demektir. Bu öğreticide, hello dosya adı için bir değer belirtin. 

1. Merhaba, **Düzenleyicisi** hello Data Factory tıklatın **... Daha fazla**, tıklatın **yeni veri kümesi**, tıklatıp **Azure Blob Depolama** hello açılan menüsünden. 
   
    ![Yeni veri kümesi menüsü](./media/data-factory-copy-activity-tutorial-using-azure-portal/new-dataset-menu.png)
2. JSON hello sağ bölmedeki JSON parçacığı aşağıdaki hello ile değiştirin: 
   
    ```json
    {
      "name": "InputDataset",
      "properties": {
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
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
          "folderPath": "adftutorial/",
          "fileName": "emp.txt",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Hour",
          "interval": 1
        }
      }
    }
    ```   

    Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:

    | Özellik | Açıklama |
    |:--- |:--- |
    | type | Merhaba type özelliği çok ayarlamak**AzureBlob** verileri Azure blob depolama alanında bulunduğundan. |
    | linkedServiceName | Toohello başvuruyor **AzureStorageLinkedService** daha önce oluşturduğunuz. |
    | folderPath | Merhaba blob belirtir **kapsayıcı** ve hello **klasörü** giriş BLOB'ları içerir. Bu öğreticide adftutorial hello blob kapsayıcı ve hello kök klasör. | 
    | fileName | Bu özellik isteğe bağlıdır. Bu özelliği atarsanız, tüm dosyaları hello folderPath çekilir. Bu öğreticide **emp.txt** hello fileName, böylece yalnızca bu dosyanın işleme için kayıt için belirtilir. |
    | format -> type |Merhaba giriş dosyası kullanırız hello metin biçiminde olduğundan **TextFormat**. |
    | columnDelimiter | Merhaba giriş dosyası Hello sütunlarında tarafından ayrılmış **virgül karakteriyle (`,`)**. |
    | frequency/interval | Merhaba sıklığını çok ayarlamak**saat** ve aralığı çok ayarlamak**1**, o hello yani dilimler kullanılabilir giriş **saatlik**. Hello Data Factory hizmeti için giriş verileri saatte hello kök klasöründe blob kapsayıcısının diğer bir deyişle, görünüyor (**adftutorial**), belirtilen. Merhaba veri hello ardışık düzen başlangıç ve bitiş zamanları, değil önce veya sonra bu kez içinde arar.  |
    | external | Bu özellik çok ayarlanır**true** hello verileri bu ardışık düzen tarafından oluşturulmamış olması durumunda. Bu öğreticide girdi verileri Hello Biz bu özellik tootrue ayarlamak için bu ardışık düzen tarafından oluşturulmayan hello emp.txt, dosyasıdır. |

    Bu JSON özellikleri hakkında daha fazla bilgi için bkz. [Azure Blob bağlayıcısı makalesi](data-factory-azure-blob-connector.md#dataset-properties).      
3. Tıklatın **dağıtma** araç toocreate hello ve hello dağıtmak **InputDataset** veri kümesi. Merhaba gördüğünüzü onaylayın **InputDataset** hello ağaç görünümünde.

### <a name="create-output-dataset"></a>Çıktı veri kümesi oluşturma
Hello Azure SQL veritabanı bağlantılı hizmet çalışma zamanı tooconnect tooyour Azure SQL veritabanını Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir. Bu adımda oluşturduğunuz hello çıktı SQL tablosu veri kümesi (OututDataset) hello veritabanı toowhich hello verileri hello blob depolama biriminden hello tabloda kopyalanır belirtir.

1. Merhaba, **Düzenleyicisi** hello Data Factory tıklatın **... Daha fazla**, tıklatın **yeni veri kümesi**, tıklatıp **Azure SQL** hello açılan menüsünden. 
2. JSON hello sağ bölmedeki JSON parçacığı aşağıdaki hello ile değiştirin:

    ```json   
    {
      "name": "OutputDataset",
      "properties": {
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
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
          "tableName": "emp"
        },
        "availability": {
          "frequency": "Hour",
          "interval": 1
        }
      }
    }
    ```     

    Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:

    | Özellik | Açıklama |
    |:--- |:--- |
    | type | Merhaba type özelliği çok ayarlamak**AzureSqlTable** verileri bir Azure SQL veritabanı tablosunda kopyalanan tooa olduğundan. |
    | linkedServiceName | Toohello başvuruyor **AzureSqlLinkedService** daha önce oluşturduğunuz. |
    | tableName | Belirtilen hello **tablo** toowhich hello veri kopyalanır. | 
    | frequency/interval | Merhaba sıklığı çok ayarlı**saat** ve aralığı **1**, hello çıkış dilimler üretilir anlamına gelir **saatlik** hello ardışık düzen başlangıç ve bitiş zamanları, önce değil arasında veya Bu kez sonra.  |

    Üç sütun – **kimliği**, **FirstName**, ve **LastName** – hello veritabanındaki emp tablosunda hello. Kimliktir bir kimlik sütunu yalnızca toospecify gereken şekilde **FirstName** ve **LastName** burada.

    Bu JSON özellikleri hakkında daha fazla bilgi için bkz. [Azure SQL bağlayıcısı makalesi](data-factory-azure-sql-connector.md#dataset-properties).
3. Tıklatın **dağıtma** araç toocreate hello ve hello dağıtmak **OutputDataset** veri kümesi. Merhaba gördüğünüzü onaylayın **OutputDataset** altında hello ağaç görünümünde **veri kümeleri**. 

## <a name="create-pipeline"></a>İşlem hattı oluşturma
Bu adımda, girdi olarak **InputDataset** ve çıktı olarak **OutputDataset** kullanan **kopyalama etkinliğine** sahip bir işlem hattı oluşturursunuz.

Şu anda, hangi sürücü zamanlama hello çıktı veri kümesi değil. Bu öğreticide, çıktı veri kümesi yapılandırılmış tooproduce bir dilim saate birdir. bir başlangıç saati ve bir 24 saat olan günü birbirinden, bitiş zamanı Hello ardışık düzen vardır. Bu nedenle, çıktı veri kümesinin 24 dilim hello ardışık düzen tarafından oluşturulur. 

1. Merhaba, **Düzenleyicisi** hello Data Factory tıklatın **... Daha fazla** ve **Yeni işlem hattı** öğelerine tıklayın. Alternatif olarak, sağ tıklayarak **ardışık düzen** hello ağaç görünümünde ve tıklatın **yeni işlem hattı**.
2. JSON hello sağ bölmedeki JSON parçacığı aşağıdaki hello ile değiştirin: 

    ```json   
    {
      "name": "ADFTutorialPipeline",
      "properties": {
        "description": "Copy data from a blob tooAzure SQL table",
        "activities": [
          {
            "name": "CopyFromBlobToSQL",
            "type": "Copy",
            "inputs": [
              {
                "name": "InputDataset"
              }
            ],
            "outputs": [
              {
                "name": "OutputDataset"
              }
            ],
            "typeProperties": {
              "source": {
                "type": "BlobSource"
              },
              "sink": {
                "type": "SqlSink",
                "writeBatchSize": 10000,
                "writeBatchTimeout": "60:00:00"
              }
            },
            "Policy": {
              "concurrency": 1,
              "executionPriorityOrder": "NewestFirst",
              "retry": 0,
              "timeout": "01:00:00"
            }
          }
        ],
        "start": "2017-05-11T00:00:00Z",
        "end": "2017-05-12T00:00:00Z"
      }
    } 
    ```   
    
    Hello aşağıdaki noktaları göz önünde bulundurun:
   
    - Merhaba etkinlikler bölümünde, yalnızca bir etkinlik olduğundan, **türü** çok ayarlanır**kopya**. Merhaba kopyalama etkinliği hakkında daha fazla bilgi için bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md). Data Factory çözümlerinde, [veri dönüştürme etkinliklerini](data-factory-data-transformation-activities.md) de kullanabilirsiniz.
    - Merhaba etkinlik çok kümesi için giriş**InputDataset** ve hello etkinlik çok kümesi için çıkış**OutputDataset**. 
    - Merhaba, **typeProperties** bölümünde **BlobSource** hello kaynak türü olarak belirtilir ve **SqlSink** hello Havuz türü olarak belirtilir. Kaynakları ve havuzlarını olarak hello kopyalama etkinliği tarafından desteklenen veri depoları tam bir listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats). nasıl toouse belirli bir desteklenen veri depolayan bir kaynak/havuz toolearn hello tablosundaki hello bağlantısını tıklatın.
    - Başlangıç ve bitiş tarih saatleri [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601) olmalıdır. Örneğin: 2016-10-14T16:32:41Z. Merhaba **son** saati isteğe bağlıdır ancak biz Bu öğreticide kullanın. Hello için değer belirtmezseniz, **son** özelliği olarak hesaplanır "**start + 48 saat**". toorun hello ardışık kalıcı olarak belirtmek **9999-09-09** hello hello değeri olarak **son** özelliği.
     
    Örnek önceki hello vardır 24 veri dilimi her veri dilimi saatlik oluşturulduğundan.

    İşlem hattı tanımındaki JSON özelliklerinin açıklamaları için [işlem hatları oluşturma](data-factory-create-pipelines.md) makalesine bakın. Kopyalama etkinliği tanımındaki JSON özelliklerinin açıklamaları için bkz. [veri taşıma etkinlikleri](data-factory-data-movement-activities.md). BlobSource tarafından desteklenen JSON özelliklerinin açıklamaları için bkz. [Azure Blob bağlayıcısı makalesi](data-factory-azure-blob-connector.md). SqlSink tarafından desteklenen JSON özelliklerinin açıklamaları için bkz. [Azure SQL Veritabanı bağlayıcısı makalesi](data-factory-azure-sql-connector.md).
3. Tıklatın **dağıtma** araç toocreate hello ve hello dağıtmak **ADFTutorialPipeline**. Merhaba ardışık hello ağaç görünümünde gördüğünüzü onaylayın. 
4. Şimdi, hello kapatmak **Düzenleyicisi** dikey **X**. Tıklatın **X** yeniden toosee hello **Data Factory** hello için giriş sayfası **ADFTutorialDataFactory**.

**Tebrikler!** Bir Azure data factory, ardışık düzen toocopy verilerle bir Azure blob depolama tooan Azure SQL veritabanı başarıyla oluşturdunuz. 


## <a name="monitor-pipeline"></a>İşlem hattını izleme
Bu adımda, bir Azure data factory'de neler olduğunu Azure portal toomonitor hello kullanın.    

### <a name="monitor-pipeline-using-monitor--manage-app"></a>İzleme ve Yönetme Uygulamasını kullanarak işlem hattını izleme
Merhaba aşağıdaki adımlar, nasıl toomonitor data factory'nizi Merhaba izleme ve yönetme uygulaması kullanarak ardışık düzenleri gösterir: 

1. Tıklatın **İzleyici & Yönet** döşeme hello veri fabrikanızın giriş sayfasında.
   
    ![İzleme ve Yönetme kutucuğu](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-manage-tile.png) 
2. **İzleme ve Yönetme uygulaması** ayrı bir sekmede açılmalıdır. 

    > [!NOTE]
    > Bu hello web tarayıcısının "Yetkilendiriliyor..." takılmış görürseniz, hello aşağıdakilerden birini yapın: Temizle hello **üçüncü taraf tanımlama bilgilerini engelleyebilir ve site verileri** onay kutusunu (veya) için bir özel durum oluşturmak **login.microsoftonline.com**, tooopen hello uygulama yeniden deneyin.

    ![İzleme ve Yönetme Uygulaması](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-and-manage-app.png)
3. Değişiklik hello **başlangıç zamanı** ve **bitiş saati** tooinclude (2017-05-11) başlangıç ve bitiş zamanları (2017-05-12), ardışık ve tıklatın **Uygula**.     
3. Merhaba gördüğünüz **etkinlik windows** ardışık düzen başlangıç ve bitiş arasındaki her bir saat ile ilişkili kez hello Orta bölmesindeki hello listesinde. 
4. bir etkinlik penceresinde, seçin toosee ayrıntılarını hello etkinlik penceresinde hello **etkinlik Windows** listesi. 
    ![Etkinlik penceresi ayrıntıları](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)

    Etkinlik penceresini Gezgini'nde hello doğru o hello toohello geçerli UTC saat dilimi bakın (8:12 PM) tüm işlenir (yeşil renkte). Merhaba 8-9 PM, 9-10 PM, 10-11 PM, 23: 00 - 00: 00 dilimler henüz işlenmedi.

    Merhaba **denemeleri** bölümünde hello sağ bölmesinde hello veri dilimi için çalıştırın hello etkinliği hakkında bilgi sağlar. Bir hata varsa, hello hata hakkında ayrıntılar sağlar. Örneğin, klasör veya kapsayıcı hello giriş değil mevcut ve hello dilim işlem başarısız olursa, o hello kapsayıcısını belirten bir hata iletisine bakın veya klasörü yok.

    ![Etkinlik çalıştırma denemeleri](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-run-attempts.png) 
4. Başlatma **SQL Server Management Studio**toohello Azure SQL veritabanına bağlanma ve hello satır içinde toohello eklenen doğrulayın **emp** hello veritabanındaki tablo.
    
    ![sql sorgu sonuçları](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)

Bu uygulamanın kullanımına ilişkin ayrıntılı bilgi için bkz. [İzleme ve Yönetme Uygulamasını kullanarak Azure Data Factory işlem hatlarını izleme ve yönetme](data-factory-monitor-manage-app.md).

### <a name="monitor-pipeline-using-diagram-view"></a>Diyagram Görünümünü kullanarak işlem hattını izleme
İzleyici veri ardışık ayrıca hello diyagram görünümü kullanarak yapabilirsiniz.  

1. Merhaba, **Data Factory** dikey penceresinde tıklatın **diyagramı**.
   
    ![Data Factory Dikey Penceresi - Diyagram Kutucuğu](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datafactoryblade-diagramtile.png)
2. Merhaba diyagramı benzer toohello görüntü aşağıdaki görmeniz gerekir: 
   
    ![Diyagram görünümü](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-diagram-blade.png)  
5. Merhaba diyagram görünümünde çift **InputDataset** toosee dilimler hello veri kümesi için.  
   
    ![InputDataset seçiliyken veri kümeleri](./media/data-factory-copy-activity-tutorial-using-azure-portal/DataSetsWithInputDatasetFromBlobSelected.png)   
5. Tıklatın **daha fazla** toosee tüm hello veri dilimleri bağlantı. İşlem hattı başlangıç ve bitiş saatleri arasında 24 saatlik dilim göreceksiniz. 
   
    ![Tüm girdi veri dilimleri](./media/data-factory-copy-activity-tutorial-using-azure-portal/all-input-slices.png)  
   
    Tüm veri dilimleri toohello geçerli UTC zaman hello olduğuna dikkat edin **hazır** çünkü hello **emp.txt** dosyanın hello blob kapsayıcısında tüm hello zaman var: **adftutorial\input**. Merhaba dilimler hello gelecekteki saatler için hazır durumda henüz değildir. Hiç dilim hello gösterilmediğini onaylayın **en son başarısız olan dilimler** hello alt kısmına.
6. Kapat hello Kanatlar, kadar hello diyagramı görünümü (veya) kaydırma sol toosee hello diyagramını görüntülemek bakın. Ardından **OutputDataset** öğesine çift tıklayın. 
8. Tıklatın **daha fazla** hello bağlantıdaki **tablo** dikey **OutputDataset** toosee tüm dilimleri hello.

    ![veri dilimleri dikey penceresi](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslices-blade.png) 
9. Tüm dilimleri toohello geçerli UTC zaman hello bildirimi taşıma **yürütme bekleyen** durumu = > **devam eden** ==> **hazır** durumu. Merhaba hello son öğesinden dilimleri (önce geçerli saati) en son toooldest varsayılan olarak işlenir. Örneğin, Hello geçerli saat 8:12 PM UTC ise hello dilim 19: 00 - 8 PM için hello 6 PM - 19: 00 dilim öncesinde işlenir. Merhaba 8 PM - 9 PM dilim hello hello süre sonunda 9 PM sonra olan varsayılan olarak işlenir.  
10. Merhaba listeden herhangi bir veri dilimine tıklayın ve hello görmelisiniz **veri dilimi** dikey. Bir etkinlik penceresiyle ilişkilendirilmiş veri parçasına dilim adı verilir. Bir dilim bir veya birden çok dosya olabilir.  
    
     ![veri dilimi dikey penceresi](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslice-blade.png)
    
     Merhaba dilim hello değilse **hazır** durumu, hazır olmayan ve geçerli dilimin yürütülmesini hello hello engelleme hello Yukarı Akış dilimleri görebilirsiniz **hazır olmayan Yukarı Akış dilimleri** listesi.
11. Merhaba, **veri DİLİMİ** dikey penceresinde hello altındaki hello listesindeki tüm etkinlik çalıştırmalarını görmelisiniz. Tıklatın bir **etkinlik** toosee hello **etkinlik çalışma ayrıntıları** dikey. 
    
    ![Etkinlik Çalışma Ayrıntıları](./media/data-factory-copy-activity-tutorial-using-azure-portal/ActivityRunDetails.png)

    Bu dikey pencerede gördüğünüz uzun hello kopyalama işlemi sürdü nasıl hangi verimlilik, okuma ve yazılı, çalıştırma başlangıç zamanı, kaç tane veri baytı sayısı olan bitiş zamanı vb. çalıştırılır.  
12. Tıklatın **X** tooclose, kadar tüm hello dikey geri alma hello giriş dikey penceresine toohello **ADFTutorialDataFactory**.
13. (isteğe bağlı) hello **veri kümeleri** döşeme veya **ardışık düzen** görülen döşeme tooget hello Kanatlar hello önceki adımları. 
14. Başlatma **SQL Server Management Studio**toohello Azure SQL veritabanına bağlanma ve hello satır içinde toohello eklenen doğrulayın **emp** hello veritabanındaki tablo.
    
    ![sql sorgu sonuçları](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)


## <a name="summary"></a>Özet
Bu öğreticide, bir Azure veri fabrikası toocopy verileri Azure blob tooan Azure SQL veritabanından oluşturuldu. Hello Azure portal toocreate hello veri fabrikası, bağlı hizmetler, veri kümeleri ve işlem hattı kullanılır. Bu öğreticide gerçekleştirilen hello üst düzey adımlar şunlardır:  

1. Oluşturulan Azure **data factory**.
2. Oluşturulan **bağlı hizmetler**:
   1. Bir **Azure Storage** hizmet toolink girdi verilerini tutan Azure Storage hesabınıza bağlı.     
   2. Bir **Azure SQL** hizmet toolink hello çıktı verilerini tutan Azure SQL veritabanınızı bağlı. 
3. İşlem hatları için girdi verilerini ve çıktı verilerini açıklayan oluşturulan **veri kümeleri**.
4. Kaynak olarak **BlobSource**’u, havuz olarak da **SqlSink**’i kapsayan **Kopyalama Etkinliği**’ne sahip oluşturulan **işlem hattı**.  

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, bir kopyalama işleminde kaynak veri deposu olarak Azure blob depolama alanını ve hedef veri deposu olarak Azure SQL veritabanını kullandınız. Merhaba aşağıdaki tabloda kaynakları ve hedefleri hello kopyalama etkinliği tarafından desteklenen veri depoları listesi verilmiştir: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

nasıl bir veri öğesine/öğesinden toocopy veri deposu hakkında toolearn hello veri deposu hello tablosundaki hello bağlantısını tıklatın.
