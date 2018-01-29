---
title: "Azure Data Factory ile birden fazla tabloyu artımlı olarak kopyalama | Microsoft Docs"
description: "Bu öğreticide, değişim verileri şirket içi SQL Server veritabanındaki birden çok tablodan Azure SQL veritabanına artımlı olarak kopyalayan bir Azure Data Factory işlem hattı oluşturacaksınız."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/22/2018
ms.author: jingwang
ms.openlocfilehash: 9eeb265e063e6642b90dd641d41d0a54cbc6951e
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/23/2018
---
# <a name="incrementally-load-data-from-multiple-tables-in-sql-server-to-an-azure-sql-database"></a>SQL Server’daki birden fazla tablodan Azure SQL veritabanı’na artımlı olarak veri yükleme
Bu öğreticide, değişim verileri şirket içi SQL Server’daki birden çok tablodan Azure SQL Veritabanına yükleyen bir Azure veri fabrikası işlem hattı oluşturacaksınız.    

Bu öğreticide aşağıdaki adımları gerçekleştireceksiniz:

> [!div class="checklist"]
> * Kaynak ve hedef veri depolarını hazırlayın.
> * Veri fabrikası oluşturma.
> * Şirket içinde barındırılan tümleştirme çalışma zamanı oluşturma.
> * Tümleştirme çalışma zamanını yükleyin. 
> * Bağlı hizmet oluşturma. 
> * Kaynak, havuz ve eşik veri kümeleri oluşturun.
> * İşlem hattını oluşturma, çalıştırma ve izleme.
> * Sonuçları gözden geçirin.
> * Kaynak tablolarına veri ekleyin veya bu verileri güncelleştirin.
> * İşlem hattını yeniden çalıştırın ve izleyin.
> * Son sonuçları gözden geçirin.

> [!NOTE]
> Bu makale, şu anda önizleme sürümünde olan Azure Data Factory sürüm 2 için geçerlidir. Data Factory hizmetinin genel kullanıma açık 1. sürümünü kullanıyorsanız [Data Factory sürüm 1 belgeleri](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) konusunu inceleyin.

## <a name="overview"></a>Genel Bakış
Bu çözümü oluşturmak için önemli adımlar şunlardır: 

1. **Eşit sütununu seçin**.
    Kaynak veri deposunda her çalıştırma için yeni veya güncelleştirilmiş kayıtları tanımlamak için her tablodan kullanılabilen bir sütun seçin. Normalde, satırlar oluşturulduğunda veya güncelleştirildiğinde seçilen bu sütundaki veriler (örneğin, last_modify_time veya kimlik) artmaya devam eder. Bu sütundaki en büyük değer eşik olarak kullanılır.

2. **Eşik değerini depolamak için veri deposunu hazırlayın**.   
    Bu öğreticide, eşik değerini bir SQL veritabanında depolayacaksınız.

3. **Aşağıdaki eylemler ile bir işlem hattı oluşturun**: 
    
    a. İşlem hattına parametre olarak geçen kaynak tablosu adlarının bir listesi üzerinden yinelenen bir ForEach eylemi oluşturun. Her kaynak tablosunda, bu tabloya yönelik olarak yüklenen değişiklikleri gerçekleştirmek için aşağıdaki eylemleri çağırır.

    b. İki arama etkinliği oluşturun. Son eşik değerini almak için ilk Arama etkinliğini kullanın. Yeni eşik değerini almak için ikinci Arama etkinliğini kullanın. Bu eşik değerleri, Kopyalama etkinliğine geçirilir.

    c. Eşik sütununun değeri eski eşik değerinden büyük ve yeni eşik değerinden küçük olacak şekilde, satırları kaynak veri deposundan kopyalayan bir Kopyalama etkinliği oluşturun. Ardından, delta veriler kaynak veri deposundan Azure Blob depolama alanına yeni bir dosya olarak kopyalanır.

    d. Sonraki seferde çalışan işlem hattı için eşik değerini güncelleştiren bir StoredProcedure etkinliği oluşturun. 

    Yüksek düzeyli çözüm diyagramı aşağıdaki gibidir: 

    ![Artımlı olarak veri yükleme](media\tutorial-incremental-copy-multiple-tables-powershell\high-level-solution-diagram.png)


Azure aboneliğiniz yoksa başlamadan önce [ücretsiz](https://azure.microsoft.com/free/) bir hesap oluşturun.

## <a name="prerequisites"></a>Ön koşullar
* **SQL Server**. Bu öğreticide şirket içi SQL Server veritabanını kaynak veri deposu olarak kullanırsınız. 
* **Azure SQL Veritabanı**. SQL veritabanını havuz veri deposu olarak kullanırsınız. SQL veritabanınız yoksa, oluşturma adımları için bkz. [Azure SQL veritabanı oluşturma](../sql-database/sql-database-get-started-portal.md). 

### <a name="create-source-tables-in-your-sql-server-database"></a>SQL Server veritabanınızda kaynak tabloları oluşturma

1. SQL Server Management Studio’yu açın ve şirket içi SQL Server veritabanınıza bağlanın.

2. **Sunucu Gezgini**’nde veritabanına sağ tıklayın ve **Yeni Sorgu**’yu seçin.

3. `customer_table` ve `project_table` adlı tabloları oluşturmak için aşağıdaki SQL komutunu veritabanınızda çalıştırın:

    ```sql
    create table customer_table
    (
        PersonID int,
        Name varchar(255),
        LastModifytime datetime
    );
    
    create table project_table
    (
        Project varchar(255),
        Creationtime datetime
    );
        
    INSERT INTO customer_table
    (PersonID, Name, LastModifytime)
    VALUES
    (1, 'John','9/1/2017 12:56:00 AM'),
    (2, 'Mike','9/2/2017 5:23:00 AM'),
    (3, 'Alice','9/3/2017 2:36:00 AM'),
    (4, 'Andy','9/4/2017 3:21:00 AM'),
    (5, 'Anny','9/5/2017 8:06:00 AM');
    
    INSERT INTO project_table
    (Project, Creationtime)
    VALUES
    ('project1','1/1/2015 0:00:00 AM'),
    ('project2','2/2/2016 1:23:00 AM'),
    ('project3','3/4/2017 5:16:00 AM');
    
    ```

### <a name="create-destination-tables-in-your-sql-database"></a>SQL veritabanınızda hedef tablo oluşturma
1. SQL Server Management Studio’yu açın ve SQL Server veritabanınıza bağlanın.

2. **Sunucu Gezgini**’nde veritabanına sağ tıklayın ve **Yeni Sorgu**’yu seçin.

3. `customer_table` ve `project_table` adlı tabloları oluşturmak için aşağıdaki SQL komutunu SQL veritabanınızda çalıştırın:  
    
    ```sql
    create table customer_table
    (
        PersonID int,
        Name varchar(255),
        LastModifytime datetime
    );
    
    create table project_table
    (
        Project varchar(255),
        Creationtime datetime
    );

    ```

### <a name="create-another-table-in-the-sql-database-to-store-the-high-watermark-value"></a>Üst eşik değerini depolamak için SQL veritabanında başka bir tablo oluşturma
1. SQL veritabanınızda aşağıdaki SQL komutunu çalıştırarak eşik değerini depolamak için `watermarktable` adlı bir tablo oluşturun: 
    
    ```sql
    create table watermarktable
    (
    
        TableName varchar(255),
        WatermarkValue datetime,
    );
    ```
2. Her iki kaynak tablonun ilk eşik değerlerini eşik tablosuna ekleyin.

    ```sql

    INSERT INTO watermarktable
    VALUES 
    ('customer_table','1/1/2010 12:00:00 AM'),
    ('project_table','1/1/2010 12:00:00 AM');
    
    ```

### <a name="create-a-stored-procedure-in-the-sql-database"></a>SQL veritabanında bir saklı yordam oluşturma 

SQL veritabanınızda bir saklı yordam oluşturmak için aşağıdaki komutu çalıştırın. Bu saklı yordam, her işlem hattı çalıştırmasından sonra eşik değerini güncelleştirir. 

```sql
CREATE PROCEDURE sp_write_watermark @LastModifiedtime datetime, @TableName varchar(50)
AS

BEGIN

    UPDATE watermarktable
    SET [WatermarkValue] = @LastModifiedtime 
WHERE [TableName] = @TableName

END

```

### <a name="create-data-types-and-additional-stored-procedures"></a>Veri türleri ve ek saklı yordamlar oluşturma
SQL veritabanınızda iki saklı yordam ve iki veri türü oluşturmak için aşağıdaki sorguyu çalıştırın. Bunlar, kaynak tablodaki verileri hedef tablolarla birleştirmek için kullanılır.

```sql
CREATE TYPE DataTypeforCustomerTable AS TABLE(
    PersonID int,
    Name varchar(255),
    LastModifytime datetime
);

GO

CREATE PROCEDURE sp_upsert_customer_table @customer_table DataTypeforCustomerTable READONLY
AS

BEGIN
  MERGE customer_table AS target
  USING @customer_table AS source
  ON (target.PersonID = source.PersonID)
  WHEN MATCHED THEN
      UPDATE SET Name = source.Name,LastModifytime = source.LastModifytime
  WHEN NOT MATCHED THEN
      INSERT (PersonID, Name, LastModifytime)
      VALUES (source.PersonID, source.Name, source.LastModifytime);
END

GO

CREATE TYPE DataTypeforProjectTable AS TABLE(
    Project varchar(255),
    Creationtime datetime
);

GO

CREATE PROCEDURE sp_upsert_project_table @project_table DataTypeforProjectTable READONLY
AS

BEGIN
  MERGE project_table AS target
  USING @project_table AS source
  ON (target.Project = source.Project)
  WHEN MATCHED THEN
      UPDATE SET Creationtime = source.Creationtime
  WHEN NOT MATCHED THEN
      INSERT (Project, Creationtime)
      VALUES (source.Project, source.Creationtime);
END

```

### <a name="azure-powershell"></a>Azure PowerShell
[Azure PowerShell’i yükleme ve yapılandırma](/powershell/azure/install-azurerm-ps) konusundaki yönergeleri izleyerek en güncel Azure PowerShell modüllerini yükleyin.

## <a name="create-a-data-factory"></a>Veri fabrikası oluşturma
1. Daha sonra PowerShell komutlarında kullanacağınız kaynak grubu adı için bir değişken tanımlayın. Aşağıdaki komut metnini PowerShell'e kopyalayın [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) için tırnak işaretleri içinde bir ad belirtin ve ardından komutu çalıştırın. `"adfrg"` bunun bir örneğidir. 
   
     ```powershell
    $resourceGroupName = "ADFTutorialResourceGroup";
    ```

    Kaynak grubu zaten varsa, üzerine yazılmasını istemeyebilirsiniz. `$resourceGroupName` değişkenine farklı bir değer atayın ve komutu yeniden çalıştırın.

2. Veri fabrikasının konumu için bir değişken tanımlayın. 

    ```powershell
    $location = "East US"
    ```
3. Azure kaynak grubunu oluşturmak için aşağıdaki komutu çalıştırın: 

    ```powershell
    New-AzureRmResourceGroup $resourceGroupName $location
    ``` 
    Kaynak grubu zaten varsa, üzerine yazılmasını istemeyebilirsiniz. `$resourceGroupName` değişkenine farklı bir değer atayın ve komutu yeniden çalıştırın.

4. Veri fabrikasının adı için bir değişken tanımlayın. 

    > [!IMPORTANT]
    >  Veri fabrikasının adını genel olarak benzersiz olacak şekilde güncelleştirin. ADFIncMultiCopyTutorialFactorySP1127 bunun bir örneğidir. 

    ```powershell
    $dataFactoryName = "ADFIncMultiCopyTutorialFactory";
    ```
5. Veri fabrikası oluşturmak için aşağıdaki **Set-AzureRmDataFactoryV2** cmdlet’ini çalıştırın: 
    
    ```powershell       
    Set-AzureRmDataFactoryV2 -ResourceGroupName $resourceGroupName -Location $location -Name $dataFactoryName 
    ```

Aşağıdaki noktalara dikkat edin:

* Veri fabrikasının adı genel olarak benzersiz olmalıdır. Aşağıdaki hata iletisini alırsanız adı değiştirip yeniden deneyin:

    ```
    The specified Data Factory name 'ADFIncMultiCopyTutorialFactory' is already in use. Data Factory names must be globally unique.
    ```
* Data Factory örnekleri oluşturmak için, Azure’da oturum açarken kullandığınız kullanıcı hesabı, katkıda bulunan veya sahip rollerinin üyesi ya da bir Azure aboneliğinin yöneticisi olmalıdır.
* Data Factory sürüm 2 şu anda Doğu ABD, Doğu ABD2 ve Batı Avrupa bölgelerinde veri fabrikası oluşturmanıza olanak sağlar. Veri fabrikası tarafından kullanılan verileri depoları (Azure Depolama, SQL Veritabanı vb.) ve işlemler (Azure HDInsight vb.) başka bölgelerde olabilir.

[!INCLUDE [data-factory-create-install-integration-runtime](../../includes/data-factory-create-install-integration-runtime.md)]



## <a name="create-linked-services"></a>Bağlı hizmetler oluşturma
Veri depolarınızı ve işlem hizmetlerinizi veri fabrikasına bağlamak için veri fabrikasında bağlı hizmetler oluşturursunuz. Bu bölümde, şirket içi SQL Server veritabanı ve SQL veritabanı hesabınızla bağlı hizmetler oluşturacaksınız. 

### <a name="create-the-sql-server-linked-service"></a>SQL Server bağlı hizmet oluşturma
Bu adımda, şirket içi SQL Server veritabanınızı veri fabrikasına bağlarsınız.

1. C:\ADFTutorials\IncCopyMultiTableTutorial klasöründe aşağıdaki içerikle SqlServerLinkedService.json adlı bir JSON dosyası oluşturun. SQL Server’a bağlanmak için kullandığınız kimlik doğrulaması yöntemine göre doğru bölümü seçin. Yerel klasörler zaten mevcut değilse bunları oluşturun. 

    > [!IMPORTANT]
    > SQL Server’a bağlanmak için kullandığınız kimlik doğrulaması yöntemine göre doğru bölümü seçin.

    SQL kimlik doğrulaması kullanıyorsanız aşağıdaki JSON tanımını kopyalayın:

    ```json
    {
        "properties": {
            "type": "SqlServer",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "Server=<servername>;Database=<databasename>;User ID=<username>;Password=<password>;Timeout=60"
                }
            },
            "connectVia": {
                "type": "integrationRuntimeReference",
                "referenceName": "<integration runtime name>"
            }
        },
        "name": "SqlServerLinkedService"
    }
   ```    
    Windows kimlik doğrulaması kullanıyorsanız aşağıdaki JSON tanımını kopyalayın:

    ```json
    {
        "properties": {
            "type": "SqlServer",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "Server=<server>;Database=<database>;Integrated Security=True"
                },
                "userName": "<user> or <domain>\\<user>",
                "password": {
                    "type": "SecureString",
                    "value": "<password>"
                }
            },
            "connectVia": {
                "type": "integrationRuntimeReference",
                "referenceName": "<integration runtime name>"
            }
        },
        "name": "SqlServerLinkedService"
    }    
    ```
    > [!IMPORTANT]
    > - SQL Server’a bağlanmak için kullandığınız kimlik doğrulaması yöntemine göre doğru bölümü seçin.
    > - &lt;integration runtime name> değerini tümleştirme çalışma zamanınızın adıyla değiştirin.
    > - Dosyayı kaydetmeden önce &lt;servername>, &lt;databasename>, &lt;username> ve &lt;password> değerlerini SQL Server veritabanınızın değerleriyle değiştirin.
    > - Kullanıcı hesabınızda veya sunucu adında eğik çizgi karakteri (`\`) kullanmanız gerekirse kaçış karakterini (`\`) kullanın. `mydomain\\myuser` bunun bir örneğidir.

2. PowerShell’de C:\ADFTutorials\IncCopyMultiTableTutorial klasörüne geçiş yapın.

3. AzureStorageLinkedService bağlı hizmetini oluşturmak için **Set-AzureRmDataFactoryV2LinkedService** cmdlet’ini çalıştırın. Aşağıdaki örnekte, *ResourceGroupName* ve *DataFactoryName* parametrelerinin değerlerini geçirirsiniz: 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SqlServerLinkedService" -File ".\SqlServerLinkedService.json"
    ```

    Örnek çıktı aşağıdaki gibidir:

    ```json
    LinkedServiceName : SqlServerLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFIncMultiCopyTutorialFactory1201
    Properties        : Microsoft.Azure.Management.DataFactory.Models.SqlServerLinkedService
    ```

### <a name="create-the-sql-database-linked-service"></a>SQL veritabanı bağlı hizmeti oluşturma
1. C:\ADFTutorials\IncCopyMultiTableTutorial klasöründe aşağıdaki içerikle AzureSQLDatabaseLinkedService.json adlı bir JSON dosyası oluşturun. (Henüz yoksa ADF klasörünü oluşturun.) Dosyayı kaydetmeden önce &lt;server&gt;, &lt;database name&gt;, &lt;user id&gt; ve &lt;password&gt; değerlerini SQL Server veritabanınızın adı, veritabanınızın adı, kullanıcı kimliği ve parola ile değiştirin. 

    ```json
    {
        "name": "AzureSQLDatabaseLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": {
                    "value": "Server = tcp:<server>.database.windows.net,1433;Initial Catalog=<database name>; Persist Security Info=False; User ID=<user name>; Password=<password>; MultipleActiveResultSets = False; Encrypt = True; TrustServerCertificate = False; Connection Timeout = 30;",
                    "type": "SecureString"
                }
            }
        }
    }
    ```
2. PowerShell’de AzureSQLDatabaseLinkedService bağlı hizmetini oluşturmak için **Set-AzureRmDataFactoryV2LinkedService** cmdlet’ini çalıştırın. 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureSQLDatabaseLinkedService" -File ".\AzureSQLDatabaseLinkedService.json"
    ```

    Örnek çıktı aşağıdaki gibidir:

    ```json
    LinkedServiceName : AzureSQLDatabaseLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFIncMultiCopyTutorialFactory1201
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlDatabaseLinkedService
    ```

## <a name="create-datasets"></a>Veri kümeleri oluşturma
Bu adımda veri kaynağı, veri hedefi ve eşiğin depolanacağı yeri temsil eden veri kümeleri oluşturacaksınız.

### <a name="create-a-source-dataset"></a>Kaynak veri kümesi oluşturma

1. Aşağıdaki içeriğe sahip klasörde SourceDataset.json adlı bir JSON dosyası oluşturun: 

    ```json
    {
        "name": "SourceDataset",
        "properties": {
            "type": "SqlServerTable",
            "typeProperties": {
                "tableName": "dummyName"
            },
            "linkedServiceName": {
                "referenceName": "SqlServerLinkedService",
                "type": "LinkedServiceReference"
            }
        }
    }
   
    ```

    Tablo adı işlevsiz bir addır. İşlem hattındaki Kopyalama etkinliği, tüm tabloyu yüklemek yerine verileri yüklemek için bir SQL sorgusu kullanır.

2. SourceDataset veri kümesini oluşturmak için **Set-AzureRmDataFactoryV2Dataset** cmdlet’ini çalıştırın.
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SourceDataset" -File ".\SourceDataset.json"
    ```

    Cmdlet’in örnek çıktısı aşağıdaki gibidir:
    
    ```json
    DatasetName       : SourceDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFIncMultiCopyTutorialFactory1201
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.SqlServerTableDataset
    ```

### <a name="create-a-sink-dataset"></a>Havuz veri kümesi oluşturma

1. Aşağıdaki içeriğe sahip klasörde SinkDataset.json adlı bir JSON dosyası oluşturun. TableName öğesi, çalışma zamanında dinamik olarak işlem hattı tarafından ayarlanır. İşlem hattındaki ForEach etkinliği, tablo adlarının bir listesi üzerinden yinelenir ve her yinelemede tablo adını bu veri kümesine geçirir. 

    ```json
    {
        "name": "SinkDataset",
        "properties": {
            "type": "AzureSqlTable",
            "typeProperties": {
                "tableName": {
                    "value": "@{dataset().SinkTableName}",
                    "type": "Expression"
                }
            },
            "linkedServiceName": {
                "referenceName": "AzureSQLDatabaseLinkedService",
                "type": "LinkedServiceReference"
            },
            "parameters": {
                "SinkTableName": {
                    "type": "String"
                }
            }
        }
    }
    ```

2. SinkDataset veri kümesini oluşturmak için **Set-AzureRmDataFactoryV2Dataset** cmdlet’ini çalıştırın.
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SinkDataset" -File ".\SinkDataset.json"
    ```

    Cmdlet’in örnek çıktısı aşağıdaki gibidir:
    
    ```json
    DatasetName       : SinkDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFIncMultiCopyTutorialFactory1201
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlTableDataset
    ```

### <a name="create-a-dataset-for-a-watermark"></a>Eşik için veri kümesi oluşturma
Bu adımda üst eşik değerini depolamak için bir veri kümesi oluşturacaksınız. 

1. Aşağıdaki içeriğe sahip klasörde WatermarkDataset.json adlı bir JSON dosyası oluşturun: 

    ```json
    {
        "name": " WatermarkDataset ",
        "properties": {
            "type": "AzureSqlTable",
            "typeProperties": {
                "tableName": "watermarktable"
            },
            "linkedServiceName": {
                "referenceName": "AzureSQLDatabaseLinkedService",
                "type": "LinkedServiceReference"
            }
        }
    }    
    ```
2. WatermarkDataset veri kümesini oluşturmak için **Set-AzureRmDataFactoryV2Dataset** cmdlet’ini çalıştırın.
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "WatermarkDataset" -File ".\WatermarkDataset.json"
    ```

    Cmdlet’in örnek çıktısı aşağıdaki gibidir:
    
    ```json
    DatasetName       : WatermarkDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : <data factory name>
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlTableDataset    
    ```

## <a name="create-a-pipeline"></a>İşlem hattı oluşturma
Bu işlem hattı parametre olarak tablo adları listesini alır. ForEach etkinliği, tablo adları listesi üzerinden yinelenir ve aşağıdaki işlemleri gerçekleştirir: 

1. Eski eşik değerini (ilk değer veya son yinelemede kullanılan değer) almak için Arama etkinliğini kullanın.

2. Yeni eşik değerini (kaynak tablodaki eşik sütununda bulunan en yüksek değer) almak için Arama etkinliğini kullanın.

3. Bu iki eşik değeri arasında kaynak veritabanından hedef veritabanına veri kopyalamak için Kopyalama etkinliğini kullanın.

4. Bir sonraki yinelemede kullanılacak eski eşik değerini güncelleştirmek için StoredProcedure etkinliğini kullanın. 

### <a name="create-the-pipeline"></a>İşlem hattını oluşturma
1. Aynı klasörde aşağıdaki içerikle IncrementalCopyPipeline.json adlı bir JSON dosyası oluşturun: 

    ```json
    {
        "name": "IncrementalCopyPipeline",
        "properties": {
            "activities": [{
    
                "name": "IterateSQLTables",
                "type": "ForEach",
                "typeProperties": {
                    "isSequential": "false",
                    "items": {
                        "value": "@pipeline().parameters.tableList",
                        "type": "Expression"
                    },
    
                    "activities": [
                        {
                            "name": "LookupOldWaterMarkActivity",
                            "type": "Lookup",
                            "typeProperties": {
                                "source": {
                                    "type": "SqlSource",
                                    "sqlReaderQuery": "select * from watermarktable where TableName  =  '@{item().TABLE_NAME}'"
                                },
    
                                "dataset": {
                                    "referenceName": "WatermarkDataset",
                                    "type": "DatasetReference"
                                }
                            }
                        },
                        {
                            "name": "LookupNewWaterMarkActivity",
                            "type": "Lookup",
                            "typeProperties": {
                                "source": {
                                    "type": "SqlSource",
                                    "sqlReaderQuery": "select MAX(@{item().WaterMark_Column}) as NewWatermarkvalue from @{item().TABLE_NAME}"
                                },
    
                                "dataset": {
                                    "referenceName": "SourceDataset",
                                    "type": "DatasetReference"
                                }
                            }
                        },
    
                        {
                            "name": "IncrementalCopyActivity",
                            "type": "Copy",
                            "typeProperties": {
                                "source": {
                                    "type": "SqlSource",
                                    "sqlReaderQuery": "select * from @{item().TABLE_NAME} where @{item().WaterMark_Column} > '@{activity('LookupOldWaterMarkActivity').output.firstRow.WatermarkValue}' and @{item().WaterMark_Column} <= '@{activity('LookupNewWaterMarkActivity').output.firstRow.NewWatermarkvalue}'"
                                },
                                "sink": {
                                    "type": "SqlSink",
                                    "SqlWriterTableType": "@{item().TableType}",
                                    "SqlWriterStoredProcedureName": "@{item().StoredProcedureNameForMergeOperation}"
                                }
                            },
                            "dependsOn": [{
                                    "activity": "LookupNewWaterMarkActivity",
                                    "dependencyConditions": [
                                        "Succeeded"
                                    ]
                                },
                                {
                                    "activity": "LookupOldWaterMarkActivity",
                                    "dependencyConditions": [
                                        "Succeeded"
                                    ]
                                }
                            ],
    
                            "inputs": [{
                                "referenceName": "SourceDataset",
                                "type": "DatasetReference"
                            }],
                            "outputs": [{
                                "referenceName": "SinkDataset",
                                "type": "DatasetReference",
                                "parameters": {
                                    "SinkTableName": "@{item().TABLE_NAME}"
                                }
                            }]
                        },
    
                        {
                            "name": "StoredProceduretoWriteWatermarkActivity",
                            "type": "SqlServerStoredProcedure",
                            "typeProperties": {
    
                                "storedProcedureName": "sp_write_watermark",
                                "storedProcedureParameters": {
                                    "LastModifiedtime": {
                                        "value": "@{activity('LookupNewWaterMarkActivity').output.firstRow.NewWatermarkvalue}",
                                        "type": "datetime"
                                    },
                                    "TableName": {
                                        "value": "@{activity('LookupOldWaterMarkActivity').output.firstRow.TableName}",
                                        "type": "String"
                                    }
                                }
                            },
    
                            "linkedServiceName": {
                                "referenceName": "AzureSQLDatabaseLinkedService",
                                "type": "LinkedServiceReference"
                            },
    
                            "dependsOn": [{
                                "activity": "IncrementalCopyActivity",
                                "dependencyConditions": [
                                    "Succeeded"
                                ]
                            }]
                        }
    
                    ]
    
                }
            }],
    
            "parameters": {
                "tableList": {
                    "type": "Object"
                }
            }
        }
    }
    ```
2. IncrementalCopyPipeline işlem hattını oluşturmak için **Set-AzureRmDataFactoryV2Pipeline** cmdlet'ini çalıştırın.
    
   ```powershell
   Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "IncrementalCopyPipeline" -File ".\IncrementalCopyPipeline.json"
   ``` 

   Örnek çıktı aşağıdaki gibidir: 

   ```json
    PipelineName      : IncrementalCopyPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFIncMultiCopyTutorialFactory1201
    Activities        : {IterateSQLTables}
    Parameters        : {[tableList, Microsoft.Azure.Management.DataFactory.Models.ParameterSpecification]}
   ```
 
## <a name="run-the-pipeline"></a>İşlem hattını çalıştırma

1. Aynı klasörde aşağıdaki içerikle Parameters.json adlı bir parametre dosyası oluşturun:

    ```json
    {
        "tableList": 
        [
            {
                "TABLE_NAME": "customer_table",
                "WaterMark_Column": "LastModifytime",
                "TableType": "DataTypeforCustomerTable",
                "StoredProcedureNameForMergeOperation": "sp_upsert_customer_table"
            },
            {
                "TABLE_NAME": "project_table",
                "WaterMark_Column": "Creationtime",
                "TableType": "DataTypeforProjectTable",
                "StoredProcedureNameForMergeOperation": "sp_upsert_project_table"
            }
        ]
    }
    ```
2. **Invoke-AzureRmDataFactoryV2Pipeline** cmdlet’ini kullanarak IncrementalCopyPipeline işlem hattını çalıştırın. Yer tutucuları kendi kaynak grubu ve veri fabrikası adınızla değiştirin.

    ```powershell
    $RunId = Invoke-AzureRmDataFactoryV2Pipeline -PipelineName "IncrementalCopyPipeline" -ResourceGroup $resourceGroupName -dataFactoryName $dataFactoryName -ParameterFile ".\Parameters.json"        
    ``` 

## <a name="monitor-the-pipeline"></a>İşlem hattını izleme

1. [Azure Portal](https://portal.azure.com) oturum açın.

2. **Diğer hizmetler**’i seçin, *Veri fabrikaları* anahtar sözcüğüyle arama yapın ve **Veri fabrikaları** seçeneğini belirleyin. 

    ![Veri fabrikaları menüsü](media\tutorial-incremental-copy-multiple-tables-powershell\monitor-data-factories-menu-1.png)

3. Veri fabrikaları listesinde veri fabrikanızı arayın ve seçerek **Veri fabrikası** sayfasını açın. 

    ![Veri fabrikanızı arama](media\tutorial-incremental-copy-multiple-tables-powershell\monitor-search-data-factory-2.png)

4. **Veri fabrikası** sayfasında **İzleme ve Yönetme** öğesini seçin. 

    ![İzleme ve Yönetme kutucuğu](media\tutorial-incremental-copy-multiple-tables-powershell\monitor-monitor-manage-tile-3.png)

5. **Veri Tümleştirme Uygulaması** ayrı bir sekmede açılır. Tüm işlem hattı çalıştırmalarını ve bunların durumunu görebilirsiniz. Aşağıdaki örnekte işlem hattı çalıştırmasının durumunun **Başarılı** olarak belirtildiğini görebilirsiniz. İşlem hattına geçirilen parametreleri denetlemek için **Parametreler** sütunundaki bağlantıyı seçin. Bir hata oluştuysa, **Hata** sütununda bir bağlantı görürsünüz. **Eylemler** sütunundaki bağlantıyı seçin. 

    ![İşlem Hattı Çalıştırmaları](media\tutorial-incremental-copy-multiple-tables-powershell\monitor-pipeline-runs-4.png)    
6. **Eylemler** sütunundaki bağlantıyı seçtiğinizde, işlem hattına yönelik tüm eylem çalıştırmalarını gösteren sayfayı görürsünüz: 

    ![Etkinlik Çalıştırmaları](media\tutorial-incremental-copy-multiple-tables-powershell\monitor-activity-runs-5.png)

7. **İşlem Hattı Çalıştırmaları** görünümüne dönmek için, resimde gösterildiği gibi **İşlem Hatları**’nı seçin. 

## <a name="review-the-results"></a>Sonuçları gözden geçirin
Verilerin kaynak tablolardan hedef tablolara kopyalandığını doğrulamak için, SQL Server Management Studio’da SQL veritabanında aşağıdaki sorguları çalıştırın: 

**Sorgu** 
```sql
select * from customer_table
```

**Çıktı**
```
===========================================
PersonID    Name    LastModifytime
===========================================
1           John    2017-09-01 00:56:00.000
2           Mike    2017-09-02 05:23:00.000
3           Alice   2017-09-03 02:36:00.000
4           Andy    2017-09-04 03:21:00.000
5           Anny    2017-09-05 08:06:00.000
```

**Sorgu**

```sql
select * from project_table
```

**Çıktı**

```
===================================
Project     Creationtime
===================================
project1    2015-01-01 00:00:00.000
project2    2016-02-02 01:23:00.000
project3    2017-03-04 05:16:00.000
```

**Sorgu**

```sql
select * from watermarktable
```

**Çıktı**

```
======================================
TableName       WatermarkValue
======================================
customer_table  2017-09-05 08:06:00.000
project_table   2017-03-04 05:16:00.000
```

Her iki tablonun da eşik değerlerinin güncelleştirildiğine dikkat edin. 

## <a name="add-more-data-to-the-source-tables"></a>Kaynak tablolara daha fazla veri ekleme

customer_table içerisindeki mevcut bir satırı güncelleştirmek için aşağıdaki sorguyu kaynak SQL Server veritabanında çalıştırın. Project_table içine yeni bir satır ekleyin. 

```sql
UPDATE customer_table
SET [LastModifytime] = '2017-09-08T00:00:00Z', [name]='NewName' where [PersonID] = 3

INSERT INTO project_table
(Project, Creationtime)
VALUES
('NewProject','10/1/2017 0:00:00 AM');
``` 

## <a name="rerun-the-pipeline"></a>İşlem hattını yeniden çalıştırma

1. Şimdi aşağıdaki PowerShell komutunu çalıştırarak işlem hattını yeniden çalıştırın:

    ```powershell
    $RunId = Invoke-AzureRmDataFactoryV2Pipeline -PipelineName "IncrementalCopyPipeline" -ResourceGroup $resourceGroupname -dataFactoryName $dataFactoryName -ParameterFile ".\Parameters.json"
    ```
2. [İşlem hattını izleme](#monitor-the-pipeline) bölümündeki yönergeleri uygulayarak işlem hattı çalıştırmalarını izleyin. İşlem hattı **Sürüyor** durumunda olduğundan, **Eylemler** bölümünde işlem hattını iptal etmenizi sağlayan bir bağlantı daha görürsünüz. 

    ![Devam eden işlem hattı çalıştırmaları](media\tutorial-incremental-copy-multiple-tables-powershell\monitor-pipeline-runs-6.png)

3. İşlem hattı başarılı olana kadar listeyi yenilemek için **Yenile**’yi seçin. 

    ![İşlem hattı çalıştırmalarını yenileme](media\tutorial-incremental-copy-multiple-tables-powershell\monitor-pipeline-runs-succeded-7.png)

4. İsteğe bağlı olarak, bu işlem hattıyla ilişkili tüm eylem çalıştırmalarını görüntülemek için **Eylemler** bölümündeki **Eylem Çalıştırmalarını Göster** bağlantısını seçin. 

## <a name="review-the-final-results"></a>Son sonuçları gözden geçirme
Güncelleştirilen/yeni verilerin kaynak tablolardan hedef tablolara kopyalandığını doğrulamak için, SQL Server Management Studio’da veritabanında aşağıdaki sorguları çalıştırın. 

**Sorgu** 
```sql
select * from customer_table
```

**Çıktı**
```
===========================================
PersonID    Name    LastModifytime
===========================================
1           John    2017-09-01 00:56:00.000
2           Mike    2017-09-02 05:23:00.000
3           NewName 2017-09-08 00:00:00.000
4           Andy    2017-09-04 03:21:00.000
5           Anny    2017-09-05 08:06:00.000
```

3 numaraya ait **PersonID** için yeni **Name** ve **LastModifytime** değerlerine dikkat edin. 

**Sorgu**

```sql
select * from project_table
```

**Çıktı**

```
===================================
Project     Creationtime
===================================
project1    2015-01-01 00:00:00.000
project2    2016-02-02 01:23:00.000
project3    2017-03-04 05:16:00.000
NewProject  2017-10-01 00:00:00.000
```

**NewProject** girişinin project_table tablosuna eklendiğine dikkat edin. 

**Sorgu**

```sql
select * from watermarktable
```

**Çıktı**

```
======================================
TableName       WatermarkValue
======================================
customer_table  2017-09-08 00:00:00.000
project_table   2017-10-01 00:00:00.000
```

Her iki tablonun da eşik değerlerinin güncelleştirildiğine dikkat edin.
     
## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide aşağıdaki adımları gerçekleştirdiniz: 

> [!div class="checklist"]
> * Kaynak ve hedef veri depolarını hazırlayın.
> * Veri fabrikası oluşturma.
> * Şirket içinde barındırılan tümleştirme çalışma (IR) zamanı oluşturun.
> * Tümleştirme çalışma zamanını yükleyin.
> * Bağlı hizmet oluşturma. 
> * Kaynak, havuz ve eşik veri kümeleri oluşturun.
> * İşlem hattını oluşturma, çalıştırma ve izleme.
> * Sonuçları gözden geçirin.
> * Kaynak tablolarına veri ekleyin veya bu verileri güncelleştirin.
> * İşlem hattını yeniden çalıştırın ve izleyin.
> * Son sonuçları gözden geçirin.

Azure üzerinde bir Spark kümesi kullanarak veri dönüştürme hakkında bilgi edinmek için aşağıdaki öğreticiye geçin:

> [!div class="nextstepaction"]
>[Değişiklik İzleme teknolojisini kullanarak Azure SQL Veritabanından Azure Blob depolama alanına verileri artımlı olarak yükleme](tutorial-incremental-copy-change-tracking-feature-powershell.md)


