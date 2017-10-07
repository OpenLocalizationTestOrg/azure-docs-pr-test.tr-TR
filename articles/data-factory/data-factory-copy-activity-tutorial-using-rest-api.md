---
title: "Öğretici: Kullanım REST API'si toocreate bir Azure Data Factory işlem hattı | Microsoft Docs"
description: "Bu öğreticide, Azure blob depolamadan Azure SQL veritabanını kopyalama etkinliği toocopy verilerle REST API toocreate bir Azure Data Factory işlem hattı kullanın."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1704cdf8-30ad-49bc-a71c-4057e26e7350
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: aa6c9b035101c4ff9acff90117ca6e3e7067f418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-rest-api-toocreate-an-azure-data-factory-pipeline-toocopy-data"></a>Öğretici: Kullanım REST API'si toocreate bir Azure Data Factory işlem hattı toocopy veri 
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

Bu makalede, nasıl toouse REST API toocreate data factory Azure blob depolama tooan Azure SQL veritabanına verileri kopyalayan bir işlem hattı ile bilgi edinin. Yeni tooAzure Data Factory varsa, hello okuma [giriş tooAzure Data Factory](data-factory-introduction.md) Bu öğretici yapmadan önce makalesi.   

Bu öğreticide, içinde bir etkinlik olan işlem hattı oluşturursunuz: Kopyalama Etkinliği. Merhaba kopyalama etkinliği bir desteklenen veri deposu tooa desteklenen havuz veri deposundan verileri kopyalar. Kaynak ve havuz olarak desteklenen veri depolarının listesi için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Merhaba etkinlik verileri güvenli, güvenilir ve ölçeklenebilir bir şekilde çeşitli veri depolamaları arasında kopyalayabilirsiniz genel olarak kullanılabilir bir hizmet tarafından desteklenir. Merhaba kopyalama etkinliği hakkında daha fazla bilgi için bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).

Bir işlem hattında birden fazla etkinlik olabilir. Ve hello çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir. Daha fazla bilgi için bkz. [bir işlem hattında birden fazla etkinlik](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE]
> Bu makalede, tüm hello veri fabrikası REST API kapsamaz. Data Factory cmdlet’leri hakkında kapsamlı belgeler için bkz. [Data Factory REST API Başvurusu](/rest/api/datafactory/).
>  
> Merhaba veri ardışık Bu öğreticide, bir kaynak veri deposu tooa hedef veri deposundan verileri kopyalar. Nasıl bir öğretici için Azure Data Factory kullanarak tootransform verileri görmek [Öğreticisi: Hadoop kümesi kullanarak bir ardışık düzen tootransform veri derleme](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Ön koşullar
* Git üzerinden [öğreticiye genel bakış](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) ve tam hello **önkoşul** adımları.
* [Curl](https://curl.haxx.se/dlwiz/) aracını makinenize yükleyin. REST komutları toocreate data factory hello Curl aracını kullanın. 
* Aşağıdakileri yapmak için [bu makaledeki](../azure-resource-manager/resource-group-create-service-principal-portal.md) yönergeleri izleyin: 
  1. Azure Active Directory’de **ADFCopyTutorialApp** adlı bir Web uygulaması oluşturun.
  2. **İstemci kimliği** ve **gizli anahtarı** alın. 
  3. **İstemci kimliğini** alın. 
  4. Merhaba atamak **ADFCopyTutorialApp** uygulama toohello **veri fabrikası katkıda bulunan** rol.  
* [Azure PowerShell](/powershell/azure/overview)'i yükleyin.  
* Başlatma **PowerShell** ve adımları izleyerek hello. Bu öğreticide hello sonuna kadar Azure PowerShell'i açık tutun. Kapatıp yeniden açın, toorun hello komutları yeniden gerekir.
  
  1. Merhaba aşağıdaki komutu çalıştırın ve hello kullanıcı adı ve parola toosign toohello Azure portalını kullanın girin:
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. Komut tooview aşağıdaki hello hello abonelikler bu hesap için çalıştırın:

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. Çalışma hello aşağıdaki toowork ile istediğiniz tooselect hello abonelik komutu. Değiştir  **&lt;NameOfAzureSubscription** &gt; , Azure aboneliğinizin hello adı. 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. Adlı bir Azure kaynak grubu oluşturma **ADFTutorialResourceGroup** hello PowerShell komutunda aşağıdaki hello çalıştırarak:  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      Belirttiğiniz Hello kaynak grubu zaten varsa, olup olmadığını tooupdate bunu (Y) veya (N) tutun. 
     
      Merhaba bu öğreticideki adımlardan bazıları ADFTutorialResourceGroup adlı hello kaynak grubunu kullandığınızı varsayar. Farklı bir kaynak grubu kullanıyorsanız, bu öğreticide ADFTutorialResourceGroup yerine, kaynak grubunun toouse hello adı gerekir.

## <a name="create-json-definitions"></a>JSON tanımları oluşturma
JSON dosyaları curl.exe bulunduğu hello klasöründe aşağıdaki oluşturun. 

### <a name="datafactoryjson"></a>datafactory.json
> [!IMPORTANT]
> Tooprefix/sonek ADFCopyTutorialDF toomake isteyebilirsiniz adı genel olarak benzersiz olmalıdır, benzersiz bir ad. 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a>azurestoragelinkedservice.json
> [!IMPORTANT]
> **accountname** ve **accountkey** sözcüklerini Azure depolama hesabınızın adı ve anahtarıyla değiştirin. toolearn tooget depolama alanınızın nasıl erişim anahtar, bkz: [erişim anahtarlarını görüntüleme, kopyalama ve yeniden oluşturma depolama](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

JSON özellikleri hakkındaki ayrıntılar için bkz. [Azure Depolama bağlı hizmeti](data-factory-azure-blob-connector.md#azure-storage-linked-service).

### <a name="azuersqllinkedservicejson"></a>azuersqllinkedservice.json
> [!IMPORTANT]
> Değiştir **servername**, **databasename**, **kullanıcıadı**, ve **parola** , SQL veritabanı adını, Azure SQL sunucunuzun adıyla kullanıcı Hesap ve hello hesabının parolası.  
> 
>

```JSON
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

JSON özellikleri hakkındaki ayrıntılar için bkz. [Azure SQL bağlı hizmeti](data-factory-azure-sql-connector.md#linked-service-properties).

### <a name="inputdatasetjson"></a>inputdataset.json

```JSON
{
  "name": "AzureBlobInput",
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

### <a name="outputdatasetjson"></a>outputdataset.json

```JSON
{
  "name": "AzureSqlOutput",
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

### <a name="pipelinejson"></a>pipeline.json

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data tooAzure SQL database",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
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
- Merhaba etkinlik çok kümesi için giriş**Azureblobınput** ve hello etkinlik çok kümesi için çıkış**AzureSqlOutput**. 
- Merhaba, **typeProperties** bölümünde **BlobSource** hello kaynak türü olarak belirtilir ve **SqlSink** hello Havuz türü olarak belirtilir. Kaynakları ve havuzlarını olarak hello kopyalama etkinliği tarafından desteklenen veri depoları tam bir listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats). nasıl toouse belirli bir desteklenen veri depolayan bir kaynak/havuz toolearn hello tablosundaki hello bağlantısını tıklatın.  
 
Merhaba Hello değerini değiştirin **Başlat** hello geçerli gün özelliğiyle ve **son** hello sonraki gün değeri. Yalnızca hello tarih bölümünü belirtip tarih saat hello hello saat bölümünü atlayın. Örneğin, "2017-02-çok eşdeğeri olan 03", "2017-02-03T00:00:00Z"
 
Başlangıç ve bitiş tarih saatleri [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601) olmalıdır. Örneğin: 2016-10-14T16:32:41Z. Merhaba **son** saati isteğe bağlıdır ancak biz Bu öğreticide kullanın. 
 
Hello için değer belirtmezseniz, **son** özelliği olarak hesaplanır "**start + 48 saat**". toorun hello ardışık kalıcı olarak belirtmek **9999-09-09** hello hello değeri olarak **son** özelliği.
 
Örnek önceki hello vardır 24 veri dilimi her veri dilimi saatlik oluşturulduğundan.

İşlem hattı tanımındaki JSON özelliklerinin açıklamaları için [işlem hatları oluşturma](data-factory-create-pipelines.md) makalesine bakın. Kopyalama etkinliği tanımındaki JSON özelliklerinin açıklamaları için bkz. [veri taşıma etkinlikleri](data-factory-data-movement-activities.md). BlobSource tarafından desteklenen JSON özelliklerinin açıklamaları için bkz. [Azure Blob bağlayıcısı makalesi](data-factory-azure-blob-connector.md). SqlSink tarafından desteklenen JSON özelliklerinin açıklamaları için bkz. [Azure SQL Veritabanı bağlayıcısı makalesi](data-factory-azure-sql-connector.md).

## <a name="set-global-variables"></a>Genel değişkenleri ayarlama
Azure PowerShell'de komutları hello değerleri kendi değerlerinizle değiştirerek sonra aşağıdaki hello yürütün:

> [!IMPORTANT]
> İstemci kimliği, istemci parolası, kiracı kimliği ve abonelik kimliğini edinme konusunda yönergeler için [Önkoşullar](#prerequisites) bölümüne bakın.   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

Kullanmakta olduğunuz hello veri fabrikasının hello adı güncelleştirdikten sonra komut aşağıdaki hello çalıştırın: 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a>AAD ile kimlik doğrulama
Komut tooauthenticate ile Azure Active Directory (AAD) aşağıdaki hello çalıştırın: 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a>Veri fabrikası oluşturma
Bu adımda, **ADFCopyTutorialDF** adlı bir Azure Data Factory oluşturacaksınız. Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir. İşlem hattında bir veya daha fazla etkinlik olabilir. Örneğin, bir kopyalama etkinliği toocopy veri kaynağı tooa hedef veri deposu. Hdınsight Hive etkinliği toorun bir Hive betiği tootransform veri tooproduct çıktı verileri girin. Aşağıdaki komutları toocreate hello veri fabrikası hello çalıştırın: 

1. Adlı hello komutu toovariable Ata **cmd**. 
   
    > [!IMPORTANT]
    > Burada belirttiğiniz (ADFCopyTutorialDF) eşleşmeleri hello hello belirtilen adı hello veri fabrikası bu hello adını onaylayın **datafactory.json**. 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Merhaba sonuçları görüntüleyin. Merhaba veri fabrikası başarıyla oluşturuldu, hello JSON hello hello veri fabrikasında için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.  
   
    ```
    Write-Host $results
    ```

Hello aşağıdaki noktaları göz önünde bulundurun:

* Merhaba hello Azure Data Factory adı küresel olarak benzersiz olmalıdır. Sonuçları hello hata görürseniz: **veri fabrikası adı "ADFCopyTutorialDF" kullanılabilir değil**, adımları hello:  
  
  1. Merhaba değişiklik hello adı (örneğin, yournameADFCopyTutorialDF) **datafactory.json** dosya.
  2. Merhaba ilk komutta burada hello **$cmd** değişken değeri atanır, ADFCopyTutorialDF hello yeni adıyla değiştirin ve hello komutunu çalıştırın. 
  3. Merhaba sonraki iki komutları tooinvoke hello REST API toocreate hello veri fabrikası ve yazdırma hello sonuçlarını hello işlemi çalıştırın. 
     
     Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.
* toocreate Data Factory örnekleri toobe katılımcı/yönetici rolünüz hello Azure aboneliği gerekir
* hello veri fabrikası Hello adı hello gelecekte bir DNS adı olarak kayıtlı ve bu nedenle herkese görünür hale gelir.
* Merhaba hatayı alırsanız: "**Bu abonelik, Microsoft.DataFactory kayıtlı toouse ad değil**" Merhaba aşağıdakilerden birini yapın ve yeniden yayımlamayı deneyin: 
  
  * Azure PowerShell'de komut tooregister hello Data Factory sağlayıcısının aşağıdaki hello çalıştırın: 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    Bu Data Factory sağlayıcısının kayıtlı hello komutu tooconfirm aşağıdaki hello çalıştırabilirsiniz. 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Oturum açma kullanılarak hello hello Azure aboneliğinize [Azure portal](https://portal.azure.com) ve tooa Data Factory dikey penceresine gidin (veya) hello Azure portalında bir data factory oluşturun. Bu eylemin hello sağlayıcıyı sizin için otomatik olarak kaydeder.

Bir işlem hattı oluşturmadan önce toocreate birkaç Data Factory varlıklarını önce gerekir. İlk bağlı hizmetler toolink kaynağı oluşturun ve hedef veri depolayan tooyour veri depolayın. Ardından, girdi ve çıktı veri kümeleri toorepresent verileri bağlı veri depolarında tanımlar. Son olarak, bu veri kümeleri kullanan bir etkinlik hello ardışık düzen oluşturun.

## <a name="create-linked-services"></a>Bağlı hizmetler oluşturma
Verilerinizi depolayan ve Hizmetleri toohello veri fabrikası işlem bir veri fabrikası toolink bağlı hizmetler oluşturma. Bu öğreticide, Azure HDInsight veya Azure Data Lake Analytics gibi herhangi bir işlem hizmeti kullanmazsınız. Azure Depolama (kaynak) ve Azure SQL Veritabanı (hedef) türünde iki veri deposu kullanırsınız. Bu nedenle, AzureStorage ve AzureSqlDatabase türlerinde AzureStorageLinkedService ve AzureSqlLinkedService adlı iki bağlı hizmet oluşturursunuz.  

Merhaba AzureStorageLinkedService Azure depolama hesabı toohello veri fabrikanıza bağlar. Bu depolama hesap hello biri, hangi, kapsayıcı oluşturuldu ve hello veri parçası olarak yüklenen [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

AzureSqlLinkedService Azure SQL veritabanı toohello veri fabrikanıza bağlar. Merhaba blob depolama biriminden kopyalanan hello veriler bu veritabanında depolanır. Bu veritabanında hello emp tablosunda bir parçası olarak oluşturulan [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).  

### <a name="create-azure-storage-linked-service"></a>Azure Storage bağlı hizmeti oluşturma
Bu adımda, Azure depolama hesabı tooyour veri fabrikanıza bağlayın. Bu bölümde hello adı ve Azure depolama hesabınızın anahtarı belirtin. Bkz: [Azure depolama bağlantılı hizmeti](data-factory-azure-blob-connector.md#azure-storage-linked-service) JSON kullanılan özellikler toodefine hakkında ayrıntılı bilgi için bir Azure Storage bağlı hizmeti.  

1. Adlı hello komutu toovariable Ata **cmd**. 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Merhaba sonuçları görüntüleyin. Merhaba bağlı hizmet başarıyla oluşturuldu, hello JSON hello hello bağlantılı hizmeti için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a>Azure SQL bağlı hizmeti oluşturma
Bu adımda, Azure SQL veritabanı tooyour veri fabrikanıza bağlayın. Bu bölümde hello Azure SQL sunucu adı, veritabanı adı, kullanıcı adı ve parola belirtin. Bkz: [Azure SQL bağlı hizmeti](data-factory-azure-sql-connector.md#linked-service-properties) JSON kullanılan özellikler toodefine hakkındaki ayrıntılar için hizmeti bir Azure SQL bağlı.

1. Adlı hello komutu toovariable Ata **cmd**. 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Merhaba sonuçları görüntüleyin. Merhaba bağlı hizmet başarıyla oluşturuldu, hello JSON hello hello bağlantılı hizmeti için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a>Veri kümeleri oluşturma
Merhaba önceki adımda, Azure Storage hesabını ve Azure SQL veritabanı tooyour veri fabrikası bağlı hizmetler toolink oluşturuldu. Bu adımda, iki veri kümesi Azureblobınput ve giriş temsil AzureSqlOutput ve sırasıyla AzureStorageLinkedService ve Azuresqllinkedservice'in başvurduğu hello veri depolarında depolanan çıktı verilerini adlı tanımlayın.

Hello Azure depolama bağlı hizmeti çalışma zamanı tooconnect tooyour Azure depolama hesabı Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir. Ve hello giriş blob veri kümesi (Azureblobınput) hello kapsayıcı ve hello giriş verisi içeren hello klasörü belirtir.  

Benzer şekilde, hello Azure SQL veritabanı bağlantılı hizmet çalışma zamanı tooconnect tooyour Azure SQL veritabanını Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir. Ve kopyalanan verileri hello blob depolama biriminden hello veritabanı toowhich hello SQL tablosu veri kümesi (OututDataset) hello tabloda hello çıktı. 

### <a name="create-input-dataset"></a>Girdi veri kümesi oluşturma
Bu adımda, tooa blob dosya (emp.txt) işaret Azureblobınput adlı bir veri hello kök klasöründe bir blob kapsayıcısını (adftutorial) hello Azure hello AzureStorageLinkedService bağlı hizmeti tarafından temsil edilen depolama oluşturun. Verme hello dosya adı için bir değer belirtin (veya atlayın) hello giriş klasöründeki tüm blob'lara ait veriler kopyalanan toohello hedef demektir. Bu öğreticide, hello dosya adı için bir değer belirtin. 

1. Adlı hello komutu toovariable Ata **cmd**. 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Merhaba sonuçları görüntüleyin. Merhaba veri kümesi başarıyla oluşturuldu, hello JSON hello hello kümesinde için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a>Çıktı veri kümesi oluşturma
Hello Azure SQL veritabanı bağlantılı hizmet çalışma zamanı tooconnect tooyour Azure SQL veritabanını Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir. Bu adımda oluşturduğunuz hello çıktı SQL tablosu veri kümesi (OututDataset) hello veritabanı toowhich hello verileri hello blob depolama biriminden hello tabloda kopyalanır belirtir.

1. Adlı hello komutu toovariable Ata **cmd**.

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Merhaba sonuçları görüntüleyin. Merhaba veri kümesi başarıyla oluşturuldu, hello JSON hello hello kümesinde için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a>İşlem hattı oluşturma
Bu adımda, girdi olarak **AzureBlobInput**, çıktı olaraksa **AzureSqlOutput** kullanan bir **kopyalama etkinliğine** sahip bir işlem hattı oluşturursunuz.

Şu anda, hangi sürücü zamanlama hello çıktı veri kümesi değil. Bu öğreticide, çıktı veri kümesi yapılandırılmış tooproduce bir dilim saate birdir. bir başlangıç saati ve bir 24 saat olan günü birbirinden, bitiş zamanı Hello ardışık düzen vardır. Bu nedenle, çıktı veri kümesinin 24 dilim hello ardışık düzen tarafından oluşturulur. 

1. Adlı hello komutu toovariable Ata **cmd**.

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Merhaba sonuçları görüntüleyin. Merhaba veri kümesi başarıyla oluşturuldu, hello JSON hello hello kümesinde için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.  

    ```PowerShell   
    Write-Host $results
    ```

**Tebrikler!** Azure Blob Storage tooAzure SQL veritabanından verileri kopyalayan bir işlem hattı ile bir Azure data factory başarıyla oluşturdunuz.

## <a name="monitor-pipeline"></a>İşlem hattını izleme
Bu adımda, veri fabrikası REST API toomonitor dilimler hello ardışık düzen tarafından üretilen kullanın.

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> Merhaba başlangıç ve bitiş aşağıdaki belirtilen hello kez eşleşme hello başlangıç komut ve bitiş saatlerini hello ardışık emin olun. 

```PowerShell
$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=2017-05-11T00%3a00%3a00.0000000Z"&"end=2017-05-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};
```

```PowerShell
$results2 = Invoke-Command -scriptblock $cmd;
```

```PowerShell
IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

Bir dilim görene kadar bir sonraki hello Invoke-Command ve hello çalıştıran **hazır** durumu veya **başarısız** durumu. Merhaba dilim hazır durumunda olduğunda hello denetleyin **emp** hello çıktı verileri için Azure SQL veritabanı tablosunda. 

Her dilim için iki hello kaynak dosyadan veri satırı kopyalanan toohello emp tablosunda hello Azure SQL veritabanı ' dir. Bu nedenle, tüm hello dilimleri (hazır durumda) başarıyla işlendiğinde hello emp tablosunda 24 yeni kayıtlar bakın. 

## <a name="summary"></a>Özet
Bu öğreticide, REST API toocreate bir Azure veri fabrikası toocopy verileri Azure blob tooan Azure SQL veritabanından kullanılır. Bu öğreticide gerçekleştirilen hello üst düzey adımlar şunlardır:  

1. Oluşturulan Azure **data factory**.
2. Oluşturulan **bağlı hizmetler**:
   1. Bir Azure depolama hizmeti toolink girdi verilerini tutan Azure Storage hesabınıza bağlı.     
   2. Bir Azure SQL Hizmeti toolink hello çıktı verilerini tutan Azure SQL veritabanınızı bağlı. 
3. İşlem hatları için girdi ve çıktı verilerini açıklayan **veri kümeleri** oluşturuldu.
4. Kaynak olarak BlobSource’u, havuz olarak SqlSink’i kapsayan bir Kopyalama Etkinliği’ne sahip bir **işlem hattı** oluşturuldu. 

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, bir kopyalama işleminde kaynak veri deposu olarak Azure blob depolama alanını ve hedef veri deposu olarak Azure SQL veritabanını kullandınız. Merhaba aşağıdaki tabloda kaynakları ve hedefleri hello kopyalama etkinliği tarafından desteklenen veri depoları listesi verilmiştir: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

nasıl bir veri öğesine/öğesinden toocopy veri deposu hakkında toolearn hello veri deposu hello tablosundaki hello bağlantısını tıklatın.
