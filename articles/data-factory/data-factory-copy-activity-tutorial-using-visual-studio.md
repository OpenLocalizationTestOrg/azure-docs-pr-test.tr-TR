---
title: "Öğretici: Visual Studio kullanarak Kopyalama Etkinliği ile işlem hattı oluşturma | Microsoft Belgeleri"
description: "Bu öğreticide, Visual Studio kullanarak Kopyalama Etkinliği ile bir Azure Data Factory işlem hattı oluşturursunuz."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: d99d8875807bab41f5122ab95a09f83f82923529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a>Öğretici: Visual Studio kullanarak Kopyalama Etkinliği ile işlem hattı oluşturma
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

Bu makalede, nasıl toouse hello Microsoft Visual Studio toocreate data factory Azure blob depolama tooan Azure SQL veritabanına verileri kopyalayan bir işlem hattı ile bilgi edinin. Yeni tooAzure Data Factory varsa, hello okuma [giriş tooAzure Data Factory](data-factory-introduction.md) Bu öğretici yapmadan önce makalesi.   

Bu öğreticide, içinde bir etkinlik olan işlem hattı oluşturursunuz: Kopyalama Etkinliği. Merhaba kopyalama etkinliği bir desteklenen veri deposu tooa desteklenen havuz veri deposundan verileri kopyalar. Kaynak ve havuz olarak desteklenen veri depolarının listesi için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Merhaba etkinlik verileri güvenli, güvenilir ve ölçeklenebilir bir şekilde çeşitli veri depolamaları arasında kopyalayabilirsiniz genel olarak kullanılabilir bir hizmet tarafından desteklenir. Merhaba kopyalama etkinliği hakkında daha fazla bilgi için bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).

Bir işlem hattında birden fazla etkinlik olabilir. Ve hello çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir. Daha fazla bilgi için bkz. [bir işlem hattında birden fazla etkinlik](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE] 
> Merhaba veri ardışık Bu öğreticide, bir kaynak veri deposu tooa hedef veri deposundan verileri kopyalar. Nasıl bir öğretici için Azure Data Factory kullanarak tootransform verileri görmek [Öğreticisi: Hadoop kümesi kullanarak bir ardışık düzen tootransform veri derleme](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Ön koşullar
1. Okuyun [öğreticiye genel bakış](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) makale ve tam hello **önkoşul** adımları.       
2. toocreate Data Factory örnekleri hello üyesi olmalıdır [veri fabrikası katkıda bulunan](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello abonelik/kaynak grubu düzeyinde rol.
3. Merhaba aşağıdakilerin yüklü olması gerekir: 
   * Visual Studio 2013 veya Visual Studio 2015
   * Visual Studio 2013 veya Visual Studio 2015 için Azure SDK’sını indirin. Çok gidin[Azure indirme sayfası](https://azure.microsoft.com/downloads/) tıklatıp **VS 2013** veya **VS 2015** hello içinde **.NET** bölümü.
   * Visual Studio için Hello en son Azure Data Factory eklentisini indirin: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) veya [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). Aşağıdaki adımları hello yaparak hello eklentisi güncelleştirebilirsiniz: hello menüsünde **Araçları** -> **Uzantılar ve güncelleştirmeler** -> **çevrimiçi**  ->  **Visual Studio Galerisi** -> **Visual Studio için Microsoft Azure Data Factory Araçları** -> **güncelleştirme**.

## <a name="steps"></a>Adımlar
Bu öğretici bir parçası olarak gerçekleştirdiğiniz hello adımlar şunlardır:

1. Oluşturma **bağlantılı Hizmetleri** hello veri fabrikası'nda. Bu adımda Azure Depolama ve Azure SQL Veritabanı türünde iki bağlı hizmet oluşturursunuz. 
    
    Merhaba AzureStorageLinkedService Azure depolama hesabı toohello veri fabrikanıza bağlar. Bir kapsayıcı oluşturulur ve veri toothis depolama hesabı bir parçası olarak yüklenen [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    AzureSqlLinkedService Azure SQL veritabanı toohello veri fabrikanıza bağlar. Merhaba blob depolama biriminden kopyalanan hello veriler bu veritabanında depolanır. Bu veritabanındaki SQL tablosunu, [ön koşulların](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) parçası olarak oluşturdunuz.     
2. Giriş ve çıkış oluşturma **veri kümeleri** hello veri fabrikası'nda.  
    
    Hello Azure depolama bağlı hizmeti çalışma zamanı tooconnect tooyour Azure depolama hesabı Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir. Ve hello giriş blob dataset hello kapsayıcı ve hello giriş verisi içeren hello klasörü belirtir.  

    Benzer şekilde, hello Azure SQL veritabanı bağlantılı hizmet çalışma zamanı tooconnect tooyour Azure SQL veritabanını Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir. Ve hello veritabanı toowhich hello verileri hello blob depolama biriminden hello tabloda kopyalanır hello çıktı SQL tablosu veri kümesi belirtir.
3. Oluşturma bir **ardışık düzen** hello veri fabrikası'nda. Bu adımda, kopyalama etkinliği ile bir işlem hattı oluşturursunuz.   
    
    Merhaba kopyalama etkinliği hello Azure blob depolama tooa hello Azure SQL veritabanı tablosunda bir blob veri kopyalar. Kopyalama etkinliği herhangi bir desteklenen kaynak desteklenen tooany hedefin bir ardışık düzen toocopy verileri kullanabilirsiniz. Desteklenen veri depolarının bir listesi için [veri taşıma etkinlikleri](data-factory-data-movement-activities.md#supported-data-stores-and-formats) makalesine bakın. 
4. Data Factory varlıklarını (bağlı hizmetler, veri kümeleri/tabloları ve işlem hatları) dağıtırken bir Azure **veri fabrikası** oluşturun. 

## <a name="create-visual-studio-project"></a>Visual Studio projesi oluşturma
1. **Visual Studio 2015**’i başlatın. Tıklatın **dosya**, çok noktası**yeni**, tıklatıp **proje**. Merhaba görmelisiniz **yeni proje** iletişim kutusu.  
2. Merhaba, **yeni proje** iletişim, select hello **DataFactory** şablonu ve tıklatın **boş Data Factory projesi**.  
   
    ![Yeni proje iletişim kutusu](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. Merhaba adını hello proje hello çözüm için konum ve hello çözüm adını belirtin ve ardından **Tamam**.
   
    ![Çözüm Gezgini](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a>Bağlı hizmetler oluşturma
Verilerinizi depolayan ve Hizmetleri toohello veri fabrikası işlem bir veri fabrikası toolink bağlı hizmetler oluşturma. Bu öğreticide, Azure HDInsight veya Azure Data Lake Analytics gibi herhangi bir işlem hizmeti kullanmazsınız. Azure Depolama (kaynak) ve Azure SQL Veritabanı (hedef) türünde iki veri deposu kullanırsınız. 

Bu nedenle, AzureStorage ve AzureSqlDatabase türünde iki bağlı hizmet oluşturursunuz.  

Hello Azure depolama hizmeti Azure depolama hesabı toohello data factory'nizi bağlı. Bu depolama hesap hello biri, hangi, kapsayıcı oluşturuldu ve hello veri parçası olarak yüklenen [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

Azure SQL Hizmeti Azure SQL veritabanı toohello data factory'nizi bağlı. Merhaba blob depolama biriminden kopyalanan hello veriler bu veritabanında depolanır. Bu veritabanında hello emp tablosunda bir parçası olarak oluşturulan [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Bağlı hizmetler veri depolarını veya hizmetleri tooan Azure data factory işlem. Bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tüm kaynakları ve kopyalama etkinliği hello tarafından desteklenen havuzlarını hello için. Bkz: [işlem bağlı Hizmetleri](data-factory-compute-linked-services.md) Data Factory ile desteklenen işlem Hizmetleri hello listesi. Bu öğreticide herhangi bir işlem hizmeti kullanmayın. 

### <a name="create-hello-azure-storage-linked-service"></a>Hello Azure Storage bağlı hizmeti oluşturma
1. İçinde **Çözüm Gezgini**, sağ **bağlı hizmetler**, çok noktası**Ekle**, tıklatıp **yeni öğe**.      
2. Merhaba, **Yeni Öğe Ekle** iletişim kutusunda **Azure depolama bağlı hizmeti** hello listesi ve tıklatın **Ekle**. 
   
    ![Yeni Bağlı Hizmet](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. Değiştir `<accountname>` ve `<accountkey>`* Azure storage hesabınızı ve anahtarını hello adı. 
   
    ![Azure Storage Bağlı Hizmeti](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. Merhaba Kaydet **AzureStorageLinkedService1.json** dosya.

    Merhaba bağlantılı hizmet tanımında JSON özellikleri hakkında daha fazla bilgi için bkz: [Azure Blob Storage bağlayıcı](data-factory-azure-blob-connector.md#linked-service-properties) makalesi.

### <a name="create-hello-azure-sql-linked-service"></a>Hello Azure SQL bağlı hizmeti oluşturma
1. Sağ tıklayın **bağlı hizmetler** hello düğümünde **Çözüm Gezgini** yeniden çok noktası**Ekle**, tıklatıp **yeni öğe**. 
2. Bu sefer, **Azure SQL Bağlı Hizmeti**’ni seçin ve **Ekle**’ye tıklayın. 
3. Merhaba, **AzureSqlLinkedService1.json dosyasında**, Değiştir `<servername>`, `<databasename>`, `<username@servername>`, ve `<password>` adlarıyla Azure SQL sunucunuza, veritabanı, kullanıcı hesabı ve parolası.    
4. Merhaba Kaydet **AzureSqlLinkedService1.json** dosya. 
    
    Bu JSON özellikleri hakkında daha fazla bilgi için [Azure SQL Veritabanı bağlayıcısı](data-factory-azure-sql-connector.md#linked-service-properties) makalesine bakın.


## <a name="create-datasets"></a>Veri kümeleri oluşturma
Merhaba önceki adımda, Azure Storage hesabını ve Azure SQL veritabanı tooyour veri fabrikası bağlı hizmetler toolink oluşturuldu. Bu adımda, iki veri kümesi InputDataset ve giriş temsil OutputDataset ve sırasıyla AzureStorageLinkedService1 ve AzureSqlLinkedService1 başvurduğu hello veri depolarında depolanan çıktı verilerini adlı tanımlayın.

Hello Azure depolama bağlı hizmeti çalışma zamanı tooconnect tooyour Azure depolama hesabı Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir. Ve hello giriş blob veri kümesi (InputDataset) hello kapsayıcı ve hello giriş verisi içeren hello klasörü belirtir.  

Benzer şekilde, hello Azure SQL veritabanı bağlantılı hizmet çalışma zamanı tooconnect tooyour Azure SQL veritabanını Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir. Ve kopyalanan verileri hello blob depolama biriminden hello veritabanı toowhich hello SQL tablosu veri kümesi (OututDataset) hello tabloda hello çıktı. 

### <a name="create-input-dataset"></a>Girdi veri kümesi oluşturma
Bu adımda, tooa blob dosya (emp.txt) işaret InputDataset adlı bir veri hello kök klasöründe bir blob kapsayıcısını (adftutorial) hello Azure hello AzureStorageLinkedService1 bağlı hizmeti tarafından temsil edilen depolama oluşturun. Verme hello dosya adı için bir değer belirtin (veya atlayın) hello giriş klasöründeki tüm blob'lara ait veriler kopyalanan toohello hedef demektir. Bu öğreticide, hello dosya adı için bir değer belirtin. 

Burada, "yerine"veri kümelerini hello terimi "Tablo" kullanın. Tablo dikdörtgen bir veri kümesidir ve hello yalnızca şu anda desteklenen veri kümesi türüdür. 

1. Sağ **tabloları** hello içinde **Çözüm Gezgini**, çok noktası**Ekle**, tıklatıp **yeni öğe**.
2. Merhaba, **Yeni Öğe Ekle** iletişim kutusunda **Azure Blob**, tıklatıp **Ekle**.   
3. Hello JSON metnini aşağıdaki metin hello ile değiştirin ve hello Kaydet **AzureBlobLocation1.json** dosya. 

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
      "linkedServiceName": "AzureStorageLinkedService1",
      "typeProperties": {
        "folderPath": "adftutorial/",
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

### <a name="create-output-dataset"></a>Çıktı veri kümesi oluşturma
Bu adımda **OutputDataset** adlı bir çıktı veri kümesi oluşturursunuz. Bu veri kümesi tarafından temsil edilen hello Azure SQL veritabanındaki tooa SQL tablosunu işaret **AzureSqlLinkedService1**. 

1. Sağ **tabloları** hello içinde **Çözüm Gezgini** yeniden çok noktası**Ekle**, tıklatıp **yeni öğe**.
2. Merhaba, **Yeni Öğe Ekle** iletişim kutusunda **Azure SQL**, tıklatıp **Ekle**. 
3. Merhaba JSON metnini aşağıdaki JSON hello ile değiştirin ve hello Kaydet **AzureSqlTableLocation1.json** dosya.

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
       "linkedServiceName": "AzureSqlLinkedService1",
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

## <a name="create-pipeline"></a>İşlem hattı oluşturma
Bu adımda, girdi olarak **InputDataset** ve çıktı olarak **OutputDataset** kullanan **kopyalama etkinliğine** sahip bir işlem hattı oluşturursunuz.

Şu anda, hangi sürücü zamanlama hello çıktı veri kümesi değil. Bu öğreticide, çıktı veri kümesi yapılandırılmış tooproduce bir dilim saate birdir. bir başlangıç saati ve bir 24 saat olan günü birbirinden, bitiş zamanı Hello ardışık düzen vardır. Bu nedenle, çıktı veri kümesinin 24 dilim hello ardışık düzen tarafından oluşturulur. 

1. Sağ **ardışık düzen** hello içinde **Çözüm Gezgini**, çok noktası**Ekle**, tıklatıp **yeni öğe**.  
2. Seçin **veri işlem hattı Kopyala** hello içinde **Yeni Öğe Ekle** iletişim kutusu ve tıklatın **Ekle**. 
3. Merhaba JSON hello aşağıdaki JSON ile değiştirin ve hello kaydedin **CopyActivity1.json** dosya.

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
             "style": "StartOfInterval",
             "retry": 0,
             "timeout": "01:00:00"
           }
         }
       ],
       "start": "2017-05-11T00:00:00Z",
       "end": "2017-05-12T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
    - Merhaba etkinlikler bölümünde, yalnızca bir etkinlik olduğundan, **türü** çok ayarlanır**kopya**. Merhaba kopyalama etkinliği hakkında daha fazla bilgi için bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md). Data Factory çözümlerinde, [veri dönüştürme etkinliklerini](data-factory-data-transformation-activities.md) de kullanabilirsiniz.
    - Merhaba etkinlik çok kümesi için giriş**InputDataset** ve hello etkinlik çok kümesi için çıkış**OutputDataset**. 
    - Merhaba, **typeProperties** bölümünde **BlobSource** hello kaynak türü olarak belirtilir ve **SqlSink** hello Havuz türü olarak belirtilir. Kaynakları ve havuzlarını olarak hello kopyalama etkinliği tarafından desteklenen veri depoları tam bir listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats). nasıl toouse belirli bir desteklenen veri depolayan bir kaynak/havuz toolearn hello tablosundaki hello bağlantısını tıklatın.  
     
    Merhaba Hello değerini değiştirin **Başlat** hello geçerli gün özelliğiyle ve **son** hello sonraki gün değeri. Yalnızca hello tarih bölümünü belirtip tarih saat hello hello saat bölümünü atlayın. Örneğin, "2016-02-çok eşdeğeri olan 03", "2016-02-03T00:00:00Z"
     
    Başlangıç ve bitiş tarih saatleri [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601) olmalıdır. Örneğin: 2016-10-14T16:32:41Z. Merhaba **son** saati isteğe bağlıdır ancak biz Bu öğreticide kullanın. 
     
    Hello için değer belirtmezseniz, **son** özelliği olarak hesaplanır "**start + 48 saat**". toorun hello ardışık kalıcı olarak belirtmek **9999-09-09** hello hello değeri olarak **son** özelliği.
     
    Örnek önceki hello vardır 24 veri dilimi her veri dilimi saatlik oluşturulduğundan.

    İşlem hattı tanımındaki JSON özelliklerinin açıklamaları için [işlem hatları oluşturma](data-factory-create-pipelines.md) makalesine bakın. Kopyalama etkinliği tanımındaki JSON özelliklerinin açıklamaları için bkz. [veri taşıma etkinlikleri](data-factory-data-movement-activities.md). BlobSource tarafından desteklenen JSON özelliklerinin açıklamaları için bkz. [Azure Blob bağlayıcısı makalesi](data-factory-azure-blob-connector.md). SqlSink tarafından desteklenen JSON özelliklerinin açıklamaları için bkz. [Azure SQL Veritabanı bağlayıcısı makalesi](data-factory-azure-sql-connector.md).

## <a name="publishdeploy-data-factory-entities"></a>Data Factory varlıklarını yayımlama/dağıtma
Bu adımda daha önce oluşturduğunuz Data Factory varlıklarını (bağlı hizmetler, veri kümeleri ve işlem hattı) yayımlayacaksınız. Ayrıca, bu varlıkları toohold hello yeni veri fabrikası toobe hello adını oluşturulan belirtin.  

1. Merhaba Çözüm Gezgini'nde projeye sağ tıklayın ve **Yayımla**. 
2. Görürseniz **tooyour Microsoft hesabı oturum** iletişim kutusunda, Azure aboneliği olan hello hesabı için kimlik bilgilerinizi girin ve tıklayın **oturum**.
3. İletişim kutusu aşağıdaki hello görmeniz gerekir:
   
   ![Yayımla iletişim kutusu](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. Merhaba data factory yapılandırma sayfasında içinde adımları hello: 
   
   1. **Yeni Data Factory Oluştur** seçeneğini seçin.
   2. **Ad** için **VSTutorialFactory** girin.  
      
      > [!IMPORTANT]
      > Merhaba hello Azure veri fabrikasının adı genel olarak benzersiz olması gerekir. Yayımlama sırasında veri fabrikasının hello adı hakkında bir hata alırsanız, hello veri fabrikası (örneğin, yournameVSTutorialFactory) yayımlamayı yeniden deneyin ve hello adını değiştirin. Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.        
      > 
      > 
   3. Azure aboneliğiniz için hello seçin **abonelik** alan.
      
      > [!IMPORTANT]
      > Herhangi bir abonelik görmüyorsanız, bir yönetici veya hello aboneliğin ortak yöneticisi olan bir hesabı kullanarak oturum emin olun.  
      > 
      > 
   4. Select hello **kaynak grubu** oluşturulan hello veri fabrikası toobe için. 
   5. Select hello **bölge** hello veri fabrikası için. Yalnızca Hello Data Factory hizmeti tarafından desteklenen bölgeler hello aşağı açılan listesinde gösterilir.
   6. Tıklatın **sonraki** tooswitch toohello **öğeleri Yayımla** sayfası.
      
       ![Veri fabrikası yapılandırma sayfası](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. Merhaba, **öğeleri Yayımla** sayfasında, tüm veri varlıkları seçilir ve tıklatın fabrikaları hello olun **sonraki** tooswitch toohello **Özet** sayfası.
   
   ![Öğe yayımlama sayfası](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. Merhaba özeti gözden geçirin ve tıklatın **sonraki** toostart, hello dağıtım işlemi ve görünüm hello **dağıtım durumu**.
   
   ![Özet yayımlama sayfası](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. Merhaba, **dağıtım durumu** sayfasında hello hello dağıtım işleminin durumunu görmeniz gerekir. Merhaba dağıtımını gerçekleştirdikten sonra Son'a tıklayın.
 
   ![Dağıtım durumu sayfası](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

Hello aşağıdaki noktaları göz önünde bulundurun: 

* Merhaba hatayı alırsanız: "Bu aboneliği değil Microsoft.DataFactory kayıtlı toouse ad", hello aşağıdakilerden birini yapın ve yeniden yayımlamayı deneyin: 
  
  * Azure PowerShell'de komut tooregister hello Data Factory sağlayıcısının aşağıdaki hello çalıştırın. 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    Bu Data Factory sağlayıcısının kayıtlı hello komutu tooconfirm aşağıdaki hello çalıştırabilirsiniz. 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Oturum açma kullanılarak hello hello Azure aboneliğinize [Azure portal](https://portal.azure.com) ve tooa Data Factory dikey penceresine gidin (veya) hello Azure portalında bir data factory oluşturun. Bu eylemin hello sağlayıcıyı sizin için otomatik olarak kaydeder.
* Merhaba veri fabrikasının Hello adı hello gelecekte bir DNS adı olarak kayıtlı ve bu nedenle herkese görünür hale gelmiştir.

> [!IMPORTANT]
> toocreate Data Factory örnekleri toobe bir yönetici/ortak yöneticisi olan hello Azure aboneliği gerekir

## <a name="monitor-pipeline"></a>İşlem hattını izleme
Veri fabrikanızın toohello giriş sayfasına gidin:

1. Çok oturum[Azure portal](https://portal.azure.com).
2. Tıklatın **daha fazla hizmet** üzerinde hello sol menü öğesini tıklatıp **veri fabrikaları**.

    ![Data factory’lere göz atma](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. Veri fabrikanızın Hello adını yazmaya başlayın.

    ![Veri fabrikasının adı](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. Veri fabrikanızın hello sonuçları listesi toosee hello giriş sayfasında, veri fabrikası'ı tıklatın.

    ![Data factory giriş sayfası](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. Makalesindeki yönergeleri izleyin [veri kümelerini ve ardışık düzen izleme](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello ardışık düzen ve veri kümeleri Bu öğreticide oluşturdunuz. Visual Studio şu anda Data Factory işlem hatlarını izlemeyi desteklememektedir. 

## <a name="summary"></a>Özet
Bu öğreticide, bir Azure veri fabrikası toocopy verileri Azure blob tooan Azure SQL veritabanından oluşturuldu. Visual Studio toocreate hello veri fabrikası, bağlı hizmetler, veri kümeleri ve işlem hattı kullanılır. Bu öğreticide gerçekleştirilen hello üst düzey adımlar şunlardır:  

1. Oluşturulan Azure **data factory**.
2. Oluşturulan **bağlı hizmetler**:
   1. Bir **Azure Storage** hizmet toolink girdi verilerini tutan Azure Storage hesabınıza bağlı.     
   2. Bir **Azure SQL** hizmet toolink hello çıktı verilerini tutan Azure SQL veritabanınızı bağlı. 
3. İşlem hatları için girdi ve çıktı verilerini açıklayan **veri kümeleri** oluşturuldu.
4. Kaynak olarak **BlobSource**’u, havuz olarak da **SqlSink**’i kapsayan **Kopyalama Etkinliği**’ne sahip oluşturulan **işlem hattı**. 

toouse Azure Hdınsight kümesi kullanarak bir Hdınsight Hive etkinliği tootransform veri nasıl görürüm toosee [ Öğreticisi: Hadoop kümesi kullanarak ilk ardışık düzen tootransform verilerinizi yapı](data-factory-build-your-first-pipeline.md).

Merhaba çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir. Ayrıntılı bilgi için bkz. [Data Factory’de zamanlama ve yürütme](data-factory-scheduling-and-execution.md). 

## <a name="view-all-data-factories-in-server-explorer"></a>Sunucu Gezgini’nde tüm veri fabrikalarını görüntüleme
Bu bölümde, nasıl toouse Sunucu Gezgini, Azure aboneliğinizin tüm hello data factory'leri Visual Studio tooview hello ve mevcut bir data factory'ye dayandırılan Visual Studio projesi oluşturma açıklanmaktadır. 

1. İçinde **Visual Studio**, tıklatın **Görünüm** üzerinde hello menü öğesini tıklatıp **Sunucu Gezgini**.
2. Merhaba Sunucu Gezgini penceresinde **Azure** ve genişletin **Data Factory**. Görürseniz **tooVisual Studio oturum**, hello girin **hesap** tıklatın ve Azure aboneliği ile ilişkili **devam**. **parola** girip **Oturum aç**’a tıklayın. Visual Studio, aboneliğinizdeki tüm Azure data factory'leri hakkında bilgi tooget çalışır. Bu işlemde hello hello durumunu görmek **Data Factoy görev listesi** penceresi.

    ![Sunucu Gezgini](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a>Var olan bir veri fabrikası için Visual Studio projesi oluşturma

- Sunucu Gezgininde veri fabrikası sağ tıklatın ve seçin **dışarı veri fabrikası tooNew proje** Visual Studio projesi dayalı mevcut bir data factory'ye toocreate.

    ![Veri Fabrikası tooa VS projesinde dışarı aktarma](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

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


## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, bir kopyalama işleminde kaynak veri deposu olarak Azure blob depolama alanını ve hedef veri deposu olarak Azure SQL veritabanını kullandınız. Merhaba aşağıdaki tabloda kaynakları ve hedefleri hello kopyalama etkinliği tarafından desteklenen veri depoları listesi verilmiştir: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

nasıl bir veri öğesine/öğesinden toocopy veri deposu hakkında toolearn hello veri deposu hello tablosundaki hello bağlantısını tıklatın.
