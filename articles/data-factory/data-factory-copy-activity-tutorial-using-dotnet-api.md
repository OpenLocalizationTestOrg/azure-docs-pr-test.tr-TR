---
title: "Öğretici: .NET API kullanarak Kopyalama Etkinlikli bir işlem hattı oluşturma | Microsoft Belgeleri"
description: "Bu öğreticide, .NET API kullanarak Kopyalama Etkinlikli bir Azure Data Factory işlem hattı oluşturursunuz."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 58fc4007-b46d-4c8e-a279-cb9e479b3e2b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 52f72da54cdd80691e09d7453bf6730454c4089e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a>Öğretici: .NET API kullanarak Kopyalama Etkinlikli bir işlem hattı oluşturma
> [!div class="op_single_selector"]
> * [Genel bakış ve önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Kopyalama Sihirbazı](data-factory-copy-data-wizard-tutorial.md)
> * [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager şablonu](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API’si](data-factory-copy-activity-tutorial-using-dotnet-api.md)

Bu makalede, bilgi nasıl toouse [.NET API](https://portal.azure.com) toocreate data factory Azure blob depolama tooan Azure SQL veritabanına verileri kopyalayan bir işlem hattı ile. Yeni tooAzure Data Factory varsa, hello okuma [giriş tooAzure Data Factory](data-factory-introduction.md) Bu öğretici yapmadan önce makalesi.   

Bu öğreticide, içinde bir etkinlik olan işlem hattı oluşturursunuz: Kopyalama Etkinliği. Merhaba kopyalama etkinliği bir desteklenen veri deposu tooa desteklenen havuz veri deposundan verileri kopyalar. Kaynak ve havuz olarak desteklenen veri depolarının listesi için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Merhaba etkinlik verileri güvenli, güvenilir ve ölçeklenebilir bir şekilde çeşitli veri depolamaları arasında kopyalayabilirsiniz genel olarak kullanılabilir bir hizmet tarafından desteklenir. Merhaba kopyalama etkinliği hakkında daha fazla bilgi için bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).

Bir işlem hattında birden fazla etkinlik olabilir. Ve hello çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir. Daha fazla bilgi için bkz. [bir işlem hattında birden fazla etkinlik](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

> [!NOTE] 
> .NET API’deki Data Factory ile ilgili tüm belgeleri görmek için bkz. [Data Factory .NET API Başvurusu](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).
> 
> Merhaba veri ardışık Bu öğreticide, bir kaynak veri deposu tooa hedef veri deposundan verileri kopyalar. Nasıl bir öğretici için Azure Data Factory kullanarak tootransform verileri görmek [Öğreticisi: Hadoop kümesi kullanarak bir ardışık düzen tootransform veri derleme](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Ön koşullar
* Git üzerinden [öğreticiye genel bakış ve ön koşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget hello öğretici ve tam hello genel bakış **önkoşul** adımları.
* Visual Studio 2012 veya 2013 veya 2015
* [Azure .NET SDK](http://azure.microsoft.com/downloads/)’yı indirip yükleyin
* Azure PowerShell. ' Ndaki yönergeleri izleyin [nasıl tooinstall Azure PowerShell'i ve yapılandırma](../powershell-install-configure.md) tooinstall Azure PowerShell, bilgisayarınızda makalesi. Azure PowerShell toocreate bir Azure Active Directory uygulamasını kullanın.

### <a name="create-an-application-in-azure-active-directory"></a>Azure Active Directory’de uygulama oluşturma
Bir Azure Active Directory uygulaması oluşturmak, Merhaba uygulaması için bir hizmet sorumlusu oluşturmak ve toohello atamak **veri fabrikası katkıda bulunan** rol.

1. **PowerShell**’i başlatın.
2. Merhaba aşağıdaki komutu çalıştırın ve hello kullanıcı adı ve parola toosign toohello Azure portal kullanın girin.

    ```PowerShell
    Login-AzureRmAccount
    ```
3. Bu hesap için tüm hello abonelikleri komutu tooview aşağıdaki hello çalıştırın.

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. Çalışma hello aşağıdaki toowork ile istediğiniz tooselect hello abonelik komutu. Değiştir  **&lt;NameOfAzureSubscription** &gt; , Azure aboneliğinizin hello adı.

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > Aşağı Not **Subscriptionıd** ve **Tenantıd** bu komutun hello çıktısından.

5. Adlı bir Azure kaynak grubu oluşturma **ADFTutorialResourceGroup** hello PowerShell komutunda aşağıdaki hello çalıştırarak.

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    Belirttiğiniz Hello kaynak grubu zaten varsa, olup olmadığını tooupdate bunu (Y) veya (N) tutun.

    Farklı bir kaynak grubu kullanıyorsanız, bu öğreticide ADFTutorialResourceGroup yerine, kaynak grubunun toouse hello adı gerekir.
6. Bir Azure Active Directory uygulaması oluşturun.

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
    ```

    Merhaba aşağıdaki hata alırsanız, farklı bir URL belirtin ve hello komutunu yeniden çalıştırın.
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. Merhaba AD hizmet sorumlusu oluşturun.

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. Hizmet asıl toohello ekleme **veri fabrikası katkıda bulunan** rol.

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. Merhaba uygulama kimliği alma

    ```PowerShell
    $azureAdApplication 
    ```
    Merhaba çıktısından hello uygulama kimliği (ApplicationId) aşağı unutmayın.

Bu adımlardan sonra aşağıdaki dört değere sahip olmanız gerekir:

* Kiracı Kimliği
* Abonelik Kimliği
* Uygulama Kimliği
* Parola (Merhaba ilk komutunda belirtilen)

## <a name="walkthrough"></a>Kılavuz
1. Visual Studio 2012/2013/2015'i kullanarak bir C# .NET konsol uygulaması oluşturun.
   1. **Visual Studio** 2012/2013/2015’i başlatın.
   2. Tıklatın **dosya**, çok noktası**yeni**, tıklatıp **proje**.
   3. **Şablonlar**’ı genişletin ve **Visual C#** seçeneğini belirleyin. Bu kılavuzda C# kullanıyor olsanız da dilediğiniz .NET dilini kullanabilirsiniz.
   4. Seçin **konsol uygulaması** hello sağ proje türlerinde hello listesinden.
   5. Girin **DataFactoryAPITestApp** hello adı için.
   6. Seçin **C:\ADFGetStarted** için başlangıç konumu.
   7. Tıklatın **Tamam** toocreate hello projesi.
2. Tıklatın **Araçları**, çok noktası**NuGet Paket Yöneticisi**, tıklatıp **Paket Yöneticisi Konsolu**.
3. Merhaba, **Paket Yöneticisi Konsolu**, adımları hello:
   1. Komut tooinstall Data Factory paketi aşağıdaki hello çalıştırın:`Install-Package Microsoft.Azure.Management.DataFactories`
   2. (Active Directory API hello kodda kullandığınız) komutu tooinstall Azure Active Directory paketi aşağıdaki hello çalıştırın:`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`
4. Merhaba aşağıdakileri ekleyin **appSetttings** bölüm toohello **App.config** dosya. Bu ayarlar hello yardımcı yöntemi tarafından kullanılır: **GetAuthorizationHeader**.

    **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;** ve **&lt;tenant ID&gt;** değerlerini kendi değerlerinizle değiştirin.

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating hello AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```

5. Merhaba aşağıdakileri ekleyin **kullanarak** hello projesindeki deyimleri toohello kaynak dosyasını (Program.cs).

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```

6. Bir örneği oluşturan kodu aşağıdaki hello eklemek **DataPipelineManagementClient** sınıfı toohello **ana** yöntemi. Bu nesne toocreate data factory, bağlı hizmet, girdi ve çıktı veri kümelerini ve işlem hattı kullanın. Bu nesne toomonitor dilimler bir veri kümesinin ayrıca çalışma zamanında kullanın.

    ```csharp
    // create data factory management client
    string resourceGroupName = "ADFTutorialResourceGroup";
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > Merhaba değerini **resourceGroupName** hello Azure kaynak grubu adı.
   >
   > Merhaba veri fabrikası (dataFactoryName) toobe benzersiz adını güncelleştirin. Merhaba veri fabrikasının adı genel olarak benzersiz olması gerekir. Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.

7. Oluşturan kod aşağıdaki hello eklemek bir **veri fabrikası** toohello **ana** yöntemi.

    ```csharp
    // create a data factory
    Console.WriteLine("Creating a data factory");
    client.DataFactories.CreateOrUpdate(resourceGroupName,
        new DataFactoryCreateOrUpdateParameters()
        {
            DataFactory = new DataFactory()
            {
                Name = dataFactoryName,
                Location = "westus",
                Properties = new DataFactoryProperties()
            }
        }
    );
    ```

    Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir. İşlem hattında bir veya daha fazla etkinlik olabilir. Örneğin, bir kopyalama etkinliği toocopy verilerinden bir kaynak tooa hedef veri deposu ve Hdınsight Hive etkinliği toorun bir Hive betiği tootransform veri tooproduct çıktı verileri girin. Bu adımda hello data factory oluşturmayla başlayalım.
8. Oluşturan kod aşağıdaki hello eklemek bir **Azure depolama bağlantılı hizmeti** toohello **ana** yöntemi.

   > [!IMPORTANT]
   > **storageaccountname** ve **accountkey** sözcüklerini Azure Depolama hesabınızın adı ve anahtarıyla değiştirin.

    ```csharp
    // create a linked service for input data store: Azure Storage
    Console.WriteLine("Creating Azure Storage linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureStorageLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```

    Verilerinizi depolayan ve Hizmetleri toohello veri fabrikası işlem bir veri fabrikası toolink bağlı hizmetler oluşturma. Bu öğreticide, Azure HDInsight veya Azure Data Lake Analytics gibi herhangi bir işlem hizmeti kullanmazsınız. Azure Depolama (kaynak) ve Azure SQL Veritabanı (hedef) türünde iki veri deposu kullanırsınız. 

    Bu nedenle, AzureStorage ve AzureSqlDatabase türlerinde AzureStorageLinkedService ve AzureSqlLinkedService adlı iki bağlı hizmet oluşturursunuz.  

    Merhaba AzureStorageLinkedService Azure depolama hesabı toohello veri fabrikanıza bağlar. Bu depolama hesap hello biri, hangi, kapsayıcı oluşturuldu ve hello veri parçası olarak yüklenen [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
9. Oluşturan kod aşağıdaki hello eklemek bir **Azure SQL bağlı hizmeti** toohello **ana** yöntemi.

   > [!IMPORTANT]
   > **servername**, **databasename**, **username** ve **password** sözcüklerini Azure SQL sunucunuzun, veritabanınızın, kullanıcınızın adlarıyla ve parolasıyla değiştirin.

    ```csharp
    // create a linked service for output data store: Azure SQL Database
    Console.WriteLine("Creating Azure SQL Database linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureSqlLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureSqlDatabaseLinkedService("Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30")
                )
            }
        }
    );
    ```

    AzureSqlLinkedService Azure SQL veritabanı toohello veri fabrikanıza bağlar. Merhaba blob depolama biriminden kopyalanan hello veriler bu veritabanında depolanır. Bu veritabanında hello emp tablosunda bir parçası olarak oluşturulan [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
10. Oluşturan kod aşağıdaki hello eklemek **giriş ve çıkış veri kümeleri** toohello **ana** yöntemi.

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "InputDataset";
    string Dataset_Destination = "OutputDataset";

    Console.WriteLine("Creating input dataset of type: Azure Blob");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                Structure = new List<DataElement>()
                {
                    new DataElement() { Name = "FirstName", Type = "String" },
                    new DataElement() { Name = "LastName", Type = "String" }
                },
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },

                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });

    Console.WriteLine("Creating output dataset of type: Azure SQL");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new DatasetCreateOrUpdateParameters()
        {
            Dataset = new Dataset()
            {
                Name = Dataset_Destination,
                Properties = new DatasetProperties()
                {
                    Structure = new List<DataElement>()
                    {
                        new DataElement() { Name = "FirstName", Type = "String" },
                        new DataElement() { Name = "LastName", Type = "String" }
                    },
                    LinkedServiceName = "AzureSqlLinkedService",
                    TypeProperties = new AzureSqlTableDataset()
                    {
                        TableName = "emp"
                    },
                    Availability = new Availability()
                    {
                        Frequency = SchedulePeriod.Hour,
                        Interval = 1,
                    },
                }
            }
        });
    ```
    
    Merhaba önceki adımda, Azure Storage hesabını ve Azure SQL veritabanı tooyour veri fabrikası bağlı hizmetler toolink oluşturuldu. Bu adımda, iki veri kümesi InputDataset ve giriş temsil OutputDataset ve sırasıyla AzureStorageLinkedService ve Azuresqllinkedservice'in başvurduğu hello veri depolarında depolanan çıktı verilerini adlı tanımlayın.

    Hello Azure depolama bağlı hizmeti çalışma zamanı tooconnect tooyour Azure depolama hesabı Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir. Ve hello giriş blob veri kümesi (InputDataset) hello kapsayıcı ve hello giriş verisi içeren hello klasörü belirtir.  

    Benzer şekilde, hello Azure SQL veritabanı bağlantılı hizmet çalışma zamanı tooconnect tooyour Azure SQL veritabanını Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir. Ve kopyalanan verileri hello blob depolama biriminden hello veritabanı toowhich hello SQL tablosu veri kümesi (OututDataset) hello tabloda hello çıktı.

    Bu adımda, tooa blob dosya (emp.txt) işaret InputDataset adlı bir veri hello kök klasöründe bir blob kapsayıcısını (adftutorial) hello Azure hello AzureStorageLinkedService bağlı hizmeti tarafından temsil edilen depolama oluşturun. Verme hello dosya adı için bir değer belirtin (veya atlayın) hello giriş klasöründeki tüm blob'lara ait veriler kopyalanan toohello hedef demektir. Bu öğreticide, hello dosya adı için bir değer belirtin.    

    Bu adımda **OutputDataset** adlı bir çıktı veri kümesi oluşturursunuz. Bu veri kümesi tarafından temsil edilen hello Azure SQL veritabanındaki tooa SQL tablosunu işaret **AzureSqlLinkedService**.
11. Merhaba aşağıdaki kod ekleme **oluşturur ve bir ardışık düzen etkinleştirir** toohello **ana** yöntemi. Bu adımda, girdi olarak **InputDataset** ve çıktı olarak **OutputDataset** kullanan **kopyalama etkinliğine** sahip bir işlem hattı oluşturursunuz.

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2017, 5, 11, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = new DateTime(2017, 5, 12, 0, 0, 0, 0, DateTimeKind.Utc);
    string PipelineName = "ADFTutorialPipeline";

    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new PipelineCreateOrUpdateParameters()
        {
            Pipeline = new Pipeline()
            {
                Name = PipelineName,
                Properties = new PipelineProperties()
                {
                    Description = "Demo Pipeline for data transfer between blobs",

                    // Initial value for pipeline's active period. With this, you won't need tooset slice status
                    Start = PipelineActivePeriodStartTime,
                    End = PipelineActivePeriodEndTime,

                    Activities = new List<Activity>()
                    {
                        new Activity()
                        {
                            Name = "BlobToAzureSql",
                            Inputs = new List<ActivityInput>()
                            {
                                new ActivityInput() {
                                    Name = Dataset_Source
                                }
                            },
                            Outputs = new List<ActivityOutput>()
                            {
                                new ActivityOutput()
                                {
                                    Name = Dataset_Destination
                                }
                            },
                            TypeProperties = new CopyActivity()
                            {
                                Source = new BlobSource(),
                                Sink = new BlobSink()
                                {
                                    WriteBatchSize = 10000,
                                    WriteBatchTimeout = TimeSpan.FromMinutes(10)
                                }
                            }
                        }
                    }
                }
            }
        });
    ```

    Hello aşağıdaki noktaları göz önünde bulundurun:
   
    - Merhaba etkinlikler bölümünde, yalnızca bir etkinlik olduğundan, **türü** çok ayarlanır**kopya**. Merhaba kopyalama etkinliği hakkında daha fazla bilgi için bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md). Data Factory çözümlerinde, [veri dönüştürme etkinliklerini](data-factory-data-transformation-activities.md) de kullanabilirsiniz.
    - Merhaba etkinlik çok kümesi için giriş**InputDataset** ve hello etkinlik çok kümesi için çıkış**OutputDataset**. 
    - Merhaba, **typeProperties** bölümünde **BlobSource** hello kaynak türü olarak belirtilir ve **SqlSink** hello Havuz türü olarak belirtilir. Kaynakları ve havuzlarını olarak hello kopyalama etkinliği tarafından desteklenen veri depoları tam bir listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats). nasıl toouse belirli bir desteklenen veri depolayan bir kaynak/havuz toolearn hello tablosundaki hello bağlantısını tıklatın.  
   
    Şu anda, hangi sürücü zamanlama hello çıktı veri kümesi değil. Bu öğreticide, çıktı veri kümesi yapılandırılmış tooproduce bir dilim saate birdir. bir başlangıç saati ve bir 24 saat olan günü birbirinden, bitiş zamanı Hello ardışık düzen vardır. Bu nedenle, çıktı veri kümesinin 24 dilim hello ardışık düzen tarafından oluşturulur.
12. Aşağıdaki kodu toohello hello eklemek **ana** yöntemi tooget hello hello bir veri dilimin durumunu çıkış veri kümesi. Bu örnekte beklenen yalnızca bir dilim vardır.

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;

    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling hello slice status");        
        // wait before hello next status check
        Thread.Sleep(1000 * 12);

        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });

        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```

13. Aşağıdaki kodu çalıştırmak tooget ayrıntılara veri dilimi toohello için hello eklemek **ana** yöntemi.

    ```csharp
    Console.WriteLine("Getting run details of a data slice");

    // give it a few minutes for hello output slice toobe ready
    Console.WriteLine("\nGive it a few minutes for hello output slice toobe ready and press any key.");
    Console.ReadKey();

    var datasliceRunListResponse = client.DataSliceRuns.List(
            resourceGroupName,
            dataFactoryName,
            Dataset_Destination,
            new DataSliceRunListParameters()
            {
                DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
            }
        );

    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }

    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```

14. Merhaba tarafından kullanılan yardımcı yöntemini aşağıdaki hello eklemek **ana** yöntemi toohello **Program** sınıfı.

    > [!NOTE] 
    > Hello aşağıdaki kodu kopyalayıp, o hello emin olun kopyalanan kodu aynı düzeydeki hello ana yöntem hello adresindeki.

    ```csharp
    public static async Task<string> GetAuthorizationHeader()
    {
        AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
        ClientCredential credential = new ClientCredential(
            ConfigurationManager.AppSettings["ApplicationId"],
            ConfigurationManager.AppSettings["Password"]);
        AuthenticationResult result = await context.AcquireTokenAsync(
            resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
            clientCredential: credential);

        if (result != null)
            return result.AccessToken;

        throw new InvalidOperationException("Failed tooacquire token");
    }
    ```

15. Buna Çözüm Gezgini Merhaba, Merhaba projeyi (DataFactoryAPITestApp) genişletin, sağ **başvuruları**, tıklatıp **Başvuru Ekle**. **System.Configuration** derlemesinin onay kutusunu işaretleyin. **Tamam**'a tıklayın.
16. Merhaba konsol uygulaması oluşturun. Tıklatın **yapı** hello menüsüne ve ardından üzerinde **yapı çözümü**.
17. Hello en az bir dosya olduğundan emin olun **adftutorial** , Azure blob depolamada kapsayıcı. Değilse, oluşturmak **Emp.txt** Not Defteri'nde içeriği aşağıdaki hello ile dosya ve toohello adftutorial kapsayıcı yükleyin.

    ```
    John, Doe
    Jane, Doe
    ```
18. Tıklayarak Hello örneği çalıştırmak **hata ayıklama** -> **hata ayıklamayı Başlat** başlangıç menüsünde. Merhaba gördüğünüzde **veri dilimi ayrıntılarını çalıştırmak**, birkaç dakika basın için bekleyin ve **ENTER**.
19. Kullanım hello Azure portal tooverify bu hello veri fabrikası **APITutorialFactory** yapıları aşağıdaki hello ile oluşturulur:
   * Bağlı hizmet: **LinkedService_AzureStorage**
   * Veri kümesi: **InputDataset** ve **OutputDataset**.
   * İşlem hattı: **PipelineBlobSample**
20. Merhaba iki çalışan kayıtları hello oluşturulduğunu doğrulayın **emp** hello tablosunda belirtilen Azure SQL veritabanı.

## <a name="next-steps"></a>Sonraki adımlar
.NET API’deki Data Factory ile ilgili tüm belgeleri görmek için bkz. [Data Factory .NET API Başvurusu](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).

Bu öğreticide, bir kopyalama işleminde kaynak veri deposu olarak Azure blob depolama alanını ve hedef veri deposu olarak Azure SQL veritabanını kullandınız. Merhaba aşağıdaki tabloda kaynakları ve hedefleri hello kopyalama etkinliği tarafından desteklenen veri depoları listesi verilmiştir: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

nasıl bir veri öğesine/öğesinden toocopy veri deposu hakkında toolearn hello veri deposu hello tablosundaki hello bağlantısını tıklatın.

