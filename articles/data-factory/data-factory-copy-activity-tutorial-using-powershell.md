---
title: "Öğretici: Azure PowerShell kullanarak bir ardışık düzen toomove veri oluşturma | Microsoft Docs"
description: "Bu öğreticide, Azure PowerShell kullanarak Kopyalama Etkinliği ile bir Azure Data Factory işlem hattı oluşturursunuz."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 71087349-9365-4e95-9847-170658216ed8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 21406d7dfaa0c555b2538fbb52839d761c140fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a>Öğretici: Azure PowerShell kullanarak verileri taşıyan bir Data Factory işlem hattı oluşturma
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

Bu makalede, bilgi nasıl toouse PowerShell toocreate data factory Azure blob depolama tooan Azure SQL veritabanına verileri kopyalayan bir işlem hattı ile. Yeni tooAzure Data Factory varsa, hello okuma [giriş tooAzure Data Factory](data-factory-introduction.md) Bu öğretici yapmadan önce makalesi.   

Bu öğreticide, içinde bir etkinlik olan işlem hattı oluşturursunuz: Kopyalama Etkinliği. Merhaba kopyalama etkinliği bir desteklenen veri deposu tooa desteklenen havuz veri deposundan verileri kopyalar. Kaynak ve havuz olarak desteklenen veri depolarının listesi için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Merhaba etkinlik verileri güvenli, güvenilir ve ölçeklenebilir bir şekilde çeşitli veri depolamaları arasında kopyalayabilirsiniz genel olarak kullanılabilir bir hizmet tarafından desteklenir. Merhaba kopyalama etkinliği hakkında daha fazla bilgi için bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).

Bir işlem hattında birden fazla etkinlik olabilir. Ve hello çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir. Daha fazla bilgi için bkz. [bir işlem hattında birden fazla etkinlik](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE]
> Bu makalede, tüm hello Data Factory cmdlet'lerini kapsamaz. Bu cmdlet’leri hakkında kapsamlı bilgi için bkz. [Data Factory Cmdlet Başvurusu](/powershell/module/azurerm.datafactories).
> 
> Merhaba veri ardışık Bu öğreticide, bir kaynak veri deposu tooa hedef veri deposundan verileri kopyalar. Nasıl bir öğretici için Azure Data Factory kullanarak tootransform verileri görmek [Öğreticisi: Hadoop kümesi kullanarak bir ardışık düzen tootransform veri derleme](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Ön koşullar
- Hello listelenen önkoşulları tamamlamanız [öğretici önkoşulları](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) makalesi.
- **Azure PowerShell**'i yükleyin. Merhaba yönergeleri izleyin [nasıl tooinstall Azure PowerShell'i ve yapılandırma](../powershell-install-configure.md).

## <a name="steps"></a>Adımlar
Bu öğretici bir parçası olarak gerçekleştirdiğiniz hello adımlar şunlardır:

1. Azure **veri fabrikası** oluşturma. Bu adımda, ADFTutorialDataFactoryPSH adlı bir veri fabrikası oluşturursunuz. 
2. Oluşturma **bağlantılı Hizmetleri** hello veri fabrikası'nda. Bu adımda Azure Depolama ve Azure SQL Veritabanı türünde iki bağlı hizmet oluşturursunuz. 
    
    Merhaba AzureStorageLinkedService Azure depolama hesabı toohello veri fabrikanıza bağlar. Bir kapsayıcı oluşturulur ve veri toothis depolama hesabı bir parçası olarak yüklenen [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    AzureSqlLinkedService Azure SQL veritabanı toohello veri fabrikanıza bağlar. Merhaba blob depolama biriminden kopyalanan hello veriler bu veritabanında depolanır. Bu veritabanındaki SQL tablosunu, [ön koşulların](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) parçası olarak oluşturdunuz.   
3. Giriş ve çıkış oluşturma **veri kümeleri** hello veri fabrikası'nda.  
    
    Hello Azure depolama bağlı hizmeti çalışma zamanı tooconnect tooyour Azure depolama hesabı Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir. Ve hello giriş blob dataset hello kapsayıcı ve hello giriş verisi içeren hello klasörü belirtir.  

    Benzer şekilde, hello Azure SQL veritabanı bağlantılı hizmet çalışma zamanı tooconnect tooyour Azure SQL veritabanını Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir. Ve hello veritabanı toowhich hello verileri hello blob depolama biriminden hello tabloda kopyalanır hello çıktı SQL tablosu veri kümesi belirtir.
4. Oluşturma bir **ardışık düzen** hello veri fabrikası'nda. Bu adımda, kopyalama etkinliği ile bir işlem hattı oluşturursunuz.   
    
    Merhaba kopyalama etkinliği hello Azure blob depolama tooa hello Azure SQL veritabanı tablosunda bir blob veri kopyalar. Kopyalama etkinliği herhangi bir desteklenen kaynak desteklenen tooany hedefin bir ardışık düzen toocopy verileri kullanabilirsiniz. Desteklenen veri depolarının bir listesi için [veri taşıma etkinlikleri](data-factory-data-movement-activities.md#supported-data-stores-and-formats) makalesine bakın. 
5. Merhaba işlem hattını izleme. Bu adımda, **İzleyici** hello girdi ve çıktı veri kümeleri dilimleri PowerShell kullanarak.

## <a name="create-a-data-factory"></a>Veri fabrikası oluşturma
> [!IMPORTANT]
> Tam [hello öğreticisi için Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) zaten yapmadıysanız.   

Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir. İşlem hattında bir veya daha fazla etkinlik olabilir. Örneğin, bir kopyalama etkinliği toocopy verilerinden bir kaynak tooa hedef veri deposu ve Hdınsight Hive etkinliği toorun bir Hive betiği tootransform veri tooproduct çıktı verileri girin. Bu adımda hello data factory oluşturmayla başlayalım.

1. **PowerShell**’i başlatın. Bu öğreticide hello sonuna kadar Azure PowerShell'i açık tutun. Kapatıp yeniden açın, toorun hello komutları yeniden gerekir.

    Hello aşağıdaki komutu çalıştırın ve hello kullanıcı adı ve parola toosign toohello Azure portalını kullanın girin:

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    Komut tooview aşağıdaki hello hello abonelikler bu hesap için çalıştırın:

    ```PowerShell
    Get-AzureRmSubscription
    ```

    Çalışma hello aşağıdaki toowork ile istediğiniz tooselect hello abonelik komutu. Değiştir  **&lt;NameOfAzureSubscription** &gt; , Azure aboneliğinizin hello adı:

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. Adlı bir Azure kaynak grubu oluşturma **ADFTutorialResourceGroup** hello aşağıdaki komutu çalıştırarak:

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    Bu öğreticideki hello adımlardan bazıları adlı hello kaynak grubunu kullandığınızı varsayar **ADFTutorialResourceGroup**. Farklı bir kaynak grubu kullanıyorsanız, toouse gerekir, bu öğreticide ADFTutorialResourceGroup yerine.
3. Merhaba çalıştırmak **New-AzureRmDataFactory** cmdlet toocreate adlı bir veri fabrikası **ADFTutorialDataFactoryPSH**:  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    Bu ad zaten alınmış olabilir. Bu nedenle, hello veri fabrikasının hello adı benzersiz bir önek veya sonek ekleyerek olun (örneğin: ADFTutorialDataFactoryPSH05152017) ve hello komutunu yeniden çalıştırın.  

Hello aşağıdaki noktaları göz önünde bulundurun:

* Merhaba hello Azure veri fabrikasının adı genel olarak benzersiz olması gerekir. Merhaba aşağıdaki hata alırsanız, hello adını (örneğin, yournameADFTutorialDataFactoryPSH) değiştirin. Bu öğreticide adımları uygularken ADFTutorialFactoryPSH yerine bu adı kullanın. Data Factory yapıtları için bkz. [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md).

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* toocreate Data Factory örnekleri, katkıda bulunan veya hello Azure abonelik yöneticisi olmanız gerekir.
* hello veri fabrikasının Hello adı hello gelecekte bir DNS adı olarak kayıtlı ve bu nedenle herkese görünür hale gelir.
* Aşağıdaki hata hello alabilirsiniz: "**Bu abonelik, Microsoft.DataFactory kayıtlı toouse ad değil.**" Merhaba aşağıdakilerden birini yapın ve yeniden yayımlamayı deneyin:

  * Azure PowerShell'de komut tooregister hello Data Factory sağlayıcısının aşağıdaki hello çalıştırın:

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    Data Factory sağlayıcısını hello komutu tooconfirm aşağıdaki çalışma hello kaydedilir:

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Azure aboneliği toohello hello kullanarak oturum açma [Azure portal](https://portal.azure.com). Tooa Data Factory dikey penceresine gidin veya hello Azure portalında bir data factory oluşturun. Bu eylemin hello sağlayıcıyı sizin için otomatik olarak kaydeder.

## <a name="create-linked-services"></a>Bağlı hizmetler oluşturma
Verilerinizi depolayan ve Hizmetleri toohello veri fabrikası işlem bir veri fabrikası toolink bağlı hizmetler oluşturma. Bu öğreticide, Azure HDInsight veya Azure Data Lake Analytics gibi herhangi bir işlem hizmeti kullanmazsınız. Azure Depolama (kaynak) ve Azure SQL Veritabanı (hedef) türünde iki veri deposu kullanırsınız. 

Bu nedenle, AzureStorage ve AzureSqlDatabase türlerinde AzureStorageLinkedService ve AzureSqlLinkedService adlı iki bağlı hizmet oluşturursunuz.  

Merhaba AzureStorageLinkedService Azure depolama hesabı toohello veri fabrikanıza bağlar. Bu depolama hesap hello biri, hangi, kapsayıcı oluşturuldu ve hello veri parçası olarak yüklenen [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

AzureSqlLinkedService Azure SQL veritabanı toohello veri fabrikanıza bağlar. Merhaba blob depolama biriminden kopyalanan hello veriler bu veritabanında depolanır. Bu veritabanında hello emp tablosunda bir parçası olarak oluşturulan [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a>Azure depolama hesabı için bağlı hizmet oluşturma
Bu adımda, Azure depolama hesabı tooyour veri fabrikanıza bağlayın.

1. Adlı bir JSON dosyası oluşturun **AzureStorageLinkedService.json** içinde **C:\ADFGetStartedPSH** içeriği aşağıdaki hello klasörüyle: (oluşturma hello zaten yoksa ADFGetStartedPSH klasörünü.)

    > [!IMPORTANT]
    > Değiştir &lt;accountname&gt; ve &lt;accountkey&gt; adı ve anahtar hello dosyayı kaydetmeden önce Azure depolama hesabınızın. 

    ```json
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
2. İçinde **Azure PowerShell**, toohello geçiş **ADFGetStartedPSH** klasör.
4. Merhaba çalıştırmak **New-AzureRmDataFactoryLinkedService** cmdlet toocreate hello bağlantılı hizmeti: **AzureStorageLinkedService**. Bu cmdlet ve diğer Data Factory cmdlet'leri Bu öğreticide kullandığınız gerektirir toopass değerleri Merhaba **ResourceGroupName** ve **DataFactoryName** parametreleri. Alternatif olarak, bir cmdlet'i her çalıştırdığınızda ResourceGroupName ve DataFactoryName yazmadan hello New-AzureRmDataFactory cmdlet tarafından döndürülen hello DataFactory nesnesini geçirebilirsiniz. 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    Merhaba örnek çıktı aşağıda verilmiştir:

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    Bu bağlı hizmeti oluşturma diğer toospecify kaynak grubu adı ve hello DataFactory nesnesini belirtme yerine veri fabrikası adı yoludur.  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a>Azure SQL veritabanı için bağlı hizmet oluşturma
Bu adımda, Azure SQL veritabanı tooyour veri fabrikanıza bağlayın.

1. İçerik aşağıdaki hello ile C:\ADFGetStartedPSH klasöründe AzureSqlLinkedService.json adlı bir JSON dosyası oluşturun:

    > [!IMPORTANT]
    > &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt; ve &lt;password&gt; sözcüklerini Azure SQL sunucunuzun, veritabanınızın, kullanıcı hesabınızın adlarıyla ve parolasıyla değiştirin.
    
    ```json
    {
        "name": "AzureSqlLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": "Server=tcp:<server>.database.windows.net,1433;Database=<databasename>;User ID=<user>@<server>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        }
     }
    ```
2. Komut toocreate aşağıdaki hello bağlı hizmet çalıştırın:

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    Merhaba örnek çıktı aşağıda verilmiştir:

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   Onaylayın **tooAzure Hizmetleri erişimine izin** ayarının açık SQL veritabanı sunucunuz için. tooverify ve açın, adımları hello:

    1. İçinde toohello oturum [Azure portalı](https://portal.azure.com)
    2. Tıklatın **daha fazla hizmet >** hello solda ve tıklatın **SQL sunucuları** hello içinde **veritabanları** kategorisi.
    3. Sunucunuzu hello SQL Server listesinde seçin.
    4. Merhaba SQL server dikey penceresinde **güvenlik duvarı ayarlarını göster** bağlantı.
    5. Merhaba, **Güvenlik Duvarı ayarları** dikey penceresinde tıklatın **ON** için **tooAzure Hizmetleri erişimine izin**.
    6. Tıklatın **kaydetmek** hello araç. 

## <a name="create-datasets"></a>Veri kümeleri oluşturma
Merhaba önceki adımda, Azure Storage hesabını ve Azure SQL veritabanı tooyour veri fabrikası bağlı hizmetler toolink oluşturuldu. Bu adımda, iki veri kümesi InputDataset ve giriş temsil OutputDataset ve sırasıyla AzureStorageLinkedService ve Azuresqllinkedservice'in başvurduğu hello veri depolarında depolanan çıktı verilerini adlı tanımlayın.

Hello Azure depolama bağlı hizmeti çalışma zamanı tooconnect tooyour Azure depolama hesabı Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir. Ve hello giriş blob veri kümesi (InputDataset) hello kapsayıcı ve hello giriş verisi içeren hello klasörü belirtir.  

Benzer şekilde, hello Azure SQL veritabanı bağlantılı hizmet çalışma zamanı tooconnect tooyour Azure SQL veritabanını Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir. Ve kopyalanan verileri hello blob depolama biriminden hello veritabanı toowhich hello SQL tablosu veri kümesi (OututDataset) hello tabloda hello çıktı. 

### <a name="create-an-input-dataset"></a>Girdi veri kümesi oluşturma
Bu adımda, tooa blob dosya (emp.txt) işaret InputDataset adlı bir veri hello kök klasöründe bir blob kapsayıcısını (adftutorial) hello Azure hello AzureStorageLinkedService bağlı hizmeti tarafından temsil edilen depolama oluşturun. Verme hello dosya adı için bir değer belirtin (veya atlayın) hello giriş klasöründeki tüm blob'lara ait veriler kopyalanan toohello hedef demektir. Bu öğreticide, hello dosya adı için bir değer belirtin.  

1. Adlı bir JSON dosyası oluşturun **Inputdataset.JSON** hello içinde **C:\ADFGetStartedPSH** klasörüyle içeriği aşağıdaki hello:

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
                "fileName": "emp.txt",
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
2. Komut toocreate hello Data Factory veri kümesi aşağıdaki hello çalıştırın.

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    Merhaba örnek çıktı aşağıda verilmiştir:

    ```
    DatasetName       : InputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureBlobDataset
    Policy            : Microsoft.Azure.Management.DataFactories.Common.Models.Policy
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

### <a name="create-an-output-dataset"></a>Çıktı veri kümesi oluşturma
Adlı bir çıktı veri kümesi oluşturma hello adımın bu bölümünde **OutputDataset**. Bu veri kümesi tarafından temsil edilen hello Azure SQL veritabanındaki tooa SQL tablosunu işaret **AzureSqlLinkedService**. 

1. Adlı bir JSON dosyası oluşturun **OutputDataset.json** hello içinde **C:\ADFGetStartedPSH** içeriği aşağıdaki hello klasörüyle:

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
2. Çalışma hello aşağıdaki toocreate hello data factory veri kümesi komutu.

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    Merhaba örnek çıktı aşağıda verilmiştir:

    ```
    DatasetName       : OutputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureSqlTableDataset
    Policy            :
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

## <a name="create-a-pipeline"></a>İşlem hattı oluşturma
Bu adımda, girdi olarak **InputDataset** ve çıktı olarak **OutputDataset** kullanan **kopyalama etkinliğine** sahip bir işlem hattı oluşturursunuz.

Şu anda, hangi sürücü zamanlama hello çıktı veri kümesi değil. Bu öğreticide, çıktı veri kümesi yapılandırılmış tooproduce bir dilim saate birdir. bir başlangıç saati ve bir 24 saat olan günü birbirinden, bitiş zamanı Hello ardışık düzen vardır. Bu nedenle, çıktı veri kümesinin 24 dilim hello ardışık düzen tarafından oluşturulur. 


1. Adlı bir JSON dosyası oluşturun **C:\adfgetstartedpsh** hello içinde **C:\ADFGetStartedPSH** klasörüyle içeriği aşağıdaki hello:

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
     
    Merhaba Hello değerini değiştirin **Başlat** hello geçerli gün özelliğiyle ve **son** hello sonraki gün değeri. Yalnızca hello tarih bölümünü belirtip tarih saat hello hello saat bölümünü atlayın. Örneğin, "2016-02-çok eşdeğeri olan 03", "2016-02-03T00:00:00Z"
     
    Başlangıç ve bitiş tarih saatleri [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601) olmalıdır. Örneğin: 2016-10-14T16:32:41Z. Merhaba **son** saati isteğe bağlıdır ancak biz Bu öğreticide kullanın. 
     
    Hello için değer belirtmezseniz, **son** özelliği olarak hesaplanır "**start + 48 saat**". toorun hello ardışık kalıcı olarak belirtmek **9999-09-09** hello hello değeri olarak **son** özelliği.
     
    Örnek önceki hello vardır 24 veri dilimi her veri dilimi saatlik oluşturulduğundan.

    İşlem hattı tanımındaki JSON özelliklerinin açıklamaları için [işlem hatları oluşturma](data-factory-create-pipelines.md) makalesine bakın. Kopyalama etkinliği tanımındaki JSON özelliklerinin açıklamaları için bkz. [veri taşıma etkinlikleri](data-factory-data-movement-activities.md). BlobSource tarafından desteklenen JSON özelliklerinin açıklamaları için bkz. [Azure Blob bağlayıcısı makalesi](data-factory-azure-blob-connector.md). SqlSink tarafından desteklenen JSON özelliklerinin açıklamaları için bkz. [Azure SQL Veritabanı bağlayıcısı makalesi](data-factory-azure-sql-connector.md).
2. Aşağıdaki komut toocreate hello veri fabrikası tablonun hello çalıştırın.

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    Merhaba örnek çıktı aşağıda verilmiştir: 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

**Tebrikler!** Bir Azure data factory, ardışık düzen toocopy verilerle bir Azure blob depolama tooan Azure SQL veritabanı başarıyla oluşturdunuz. 

## <a name="monitor-hello-pipeline"></a>Merhaba işlem hattını izleme
Bu adımda, bir Azure data factory'de neler olduğunu Azure PowerShell toomonitor kullanın.

1. Değiştir &lt;DataFactoryName&gt; veri fabrikası ve Çalıştır hello adıyla **Get-AzureRmDataFactory**ve değişken $df hello çıktı tooa atayın.

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    Örneğin:
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    Ardından, çıktı aşağıdaki $df toosee hello yazdırma hello içeriğini çalıştırın: 
    
    ```
    PS C:\ADFGetStartedPSH> $df
    
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DataFactoryId     : 6f194b34-03b3-49ab-8f03-9f8a7b9d3e30
    ResourceGroupName : ADFTutorialResourceGroup
    Location          : West US
    Tags              : {}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DataFactoryProperties
    ProvisioningState : Succeeded
    ```
2. Çalıştırma **Get-AzureRmDataFactorySlice** hello tüm dilimleri hakkında bilgi tooget **OutputDataset**, hello çıktı veri kümesi hello ardışık olduğu.  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   Bu ayar hello eşleşmelidir **Başlat** hello ardışık düzen JSON değeri. 24 dilim görmeniz gerekir ertesi gün 00: 00 hello geçerli gün too12, her saat için bir tane 'M Merhaba.

   Üç örnek dilimler hello çıktısından şunlardır: 

    ``` 
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 11:00:00 PM
    End               : 5/12/2017 12:00:00 AM
    RetryCount        : 0
    State             : Ready
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 9:00:00 PM
    End               : 5/11/2017 10:00:00 PM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0   

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 8:00:00 PM
    End               : 5/11/2017 9:00:00 PM
    RetryCount        : 0
    State             : Waiting
    SubState          : ConcurrencyLimit
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. Çalıştırma **Get-AzureRmDataFactoryRun** tooget hello etkinliğinin ayrıntılarını çalıştıran bir **belirli** dilim. Merhaba tarih-saat değeri hello önceki komutu toospecify hello hello StartDateTime parametresinin değeri hello çıktısını kopyalayın. 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   Merhaba örnek çıktı aşağıda verilmiştir: 

    ```
    Id                  : c0ddbd75-d0c7-4816-a775-704bbd7c7eab_636301332000000000_636301368000000000_OutputDataset
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : ADFTutorialDataFactoryPSH0516
    DatasetName         : OutputDataset
    ProcessingStartTime : 5/16/2017 8:00:33 PM
    ProcessingEndTime   : 5/16/2017 8:01:36 PM
    PercentComplete     : 100
    DataSliceStart      : 5/11/2017 9:00:00 PM
    DataSliceEnd        : 5/11/2017 10:00:00 PM
    Status              : Succeeded
    Timestamp           : 5/16/2017 8:00:33 PM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : CopyFromBlobToSQL
    PipelineName        : ADFTutorialPipeline
    Type                : Copy  
    ```

Data Factory cmdlet’leri hakkında kapsamlı bilgi için bkz. [Data Factory Cmdlet Başvurusu](/powershell/module/azurerm.datafactories).

## <a name="summary"></a>Özet
Bu öğreticide, bir Azure veri fabrikası toocopy verileri Azure blob tooan Azure SQL veritabanından oluşturuldu. PowerShell toocreate hello veri fabrikası, bağlı hizmetler, veri kümeleri ve işlem hattı kullanılır. Bu öğreticide gerçekleştirilen hello üst düzey adımlar şunlardır:  

1. Oluşturulan Azure **data factory**.
2. **Bağlı hizmetler** oluşturuldu:

   a. Bir **Azure Storage** hizmet toolink girdi verilerini tutan Azure depolama hesabınıza bağlı.     
   b. Bir **Azure SQL** hizmet toolink hello çıktı verilerini tutan SQL veritabanınız bağlı.
3. İşlem hatları için girdi verilerini ve çıktı verilerini açıklayan oluşturulan **veri kümeleri**.
4. Oluşturulan bir **ardışık düzen** ile **kopyalama etkinliği**, ile **BlobSource** hello kaynağı olarak ve **SqlSink** hello havuz olarak.

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, bir kopyalama işleminde kaynak veri deposu olarak Azure blob depolama alanını ve hedef veri deposu olarak Azure SQL veritabanını kullandınız. Merhaba aşağıdaki tabloda kaynakları ve hedefleri hello kopyalama etkinliği tarafından desteklenen veri depoları listesi verilmiştir: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

nasıl bir veri öğesine/öğesinden toocopy veri deposu hakkında toolearn hello veri deposu hello tablosundaki hello bağlantısını tıklatın. 

