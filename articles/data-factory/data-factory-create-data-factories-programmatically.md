---
title: "Azure .NET SDK kullanarak aaaCreate veri ardışık | Microsoft Docs"
description: "Nasıl tooprogrammatically oluşturmak, izlemek ve Data Factory SDK'yı kullanarak Azure data factory'leri yönetmek öğrenin."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 190b5f99edbb3c27e1e8efb8990b9e601b22458f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a>Oluşturma, izlemek ve Azure Data Factory .NET SDK kullanarak Azure data factory'leri yönetme
## <a name="overview"></a>Genel Bakış
Oluşturun, izlemek ve program aracılığıyla Data Factory .NET SDK kullanarak Azure data factory'leri yönetin. Bu makalede toocreate oluşturan ve veri fabrikası izler örnek bir .NET konsol uygulaması izleyebileceğiniz bir kılavuz içerir. 

> [!NOTE]
> Bu makalede, tüm hello veri fabrikası .NET API kapsamaz. Bkz: [Data Factory .NET API Başvurusu](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) hakkında kapsamlı bilgi için .NET API veri fabrikası için. 

## <a name="prerequisites"></a>Ön koşullar
* Visual Studio 2012 veya 2013 veya 2015
* İndirme ve yükleme [Azure .NET SDK'sı](http://azure.microsoft.com/downloads/).
* Azure PowerShell. ' Ndaki yönergeleri izleyin [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) tooinstall Azure PowerShell, bilgisayarınızda makalesi. Azure PowerShell toocreate bir Azure Active Directory uygulamasını kullanın.

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
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
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
Merhaba kılavuzda data factory kopyalama etkinliği içeren sahip işlem hattı oluşturun. Merhaba kopyalama etkinliği verileri kopyalar aynı blob depolama Merhaba, Azure blob depolama tooanother klasöründe bir klasörden. 

Merhaba kopya etkinliği Azure Data Factory'de hello veri taşımayı gerçekleştirir. Merhaba etkinlik verileri güvenli, güvenilir ve ölçeklenebilir bir şekilde çeşitli veri depolamaları arasında kopyalayabilirsiniz genel olarak kullanılabilir bir hizmet tarafından desteklenir. Bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale hello kopyalama etkinliği hakkında ayrıntılı bilgi için.

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
4. Merhaba Değiştir **App.config** içeriği aşağıdaki hello hello projeyle dosyasında: 
    
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
5. Merhaba App.Config dosyasında değerlerini güncelleştirin  **&lt;uygulama kimliği&gt;**,  **&lt;parola&gt;**,  **&lt; Abonelik kimliği&gt;**, ve  **&lt;kimliği Kiracı&gt;**  kendi değerlere sahip.
6. Merhaba aşağıdakileri ekleyin **kullanarak** deyimleri toohello **Program.cs** hello proje dosyasında.

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

    //IMPORTANT: specify hello name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: hello name of hello data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > Merhaba değerini **resourceGroupName** hello Azure kaynak grubu adı. Hello kullanarak bir kaynak grubu oluşturabilirsiniz [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet'i.
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
9. Oluşturan kod aşağıdaki hello eklemek **giriş ve çıkış veri kümeleri** toohello **ana** yöntemi.

    Merhaba **FolderPath** hello giriş blob çok ayarlamak için**adftutorial /** nerede **adftutorial** hello kapsayıcıda blob depolama alanınızın hello adıdır. Bu kapsayıcı, Azure blob depolamada mevcut değilse, bu ada sahip bir kapsayıcı oluşturmak: **adftutorial** ve bir metin dosyası toohello kapsayıcı yükleyin.

    Merhaba FolderPath hello için çıktı blob ayarlanır: **adftutorial/apifactoryoutput / {dilim}** nerede **dilim** dinamik olarak hesaplanan göre hello değeri **SliceStart**(tarih-saat her dilimin başlatın.)

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
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
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Destination,
            Properties = new DatasetProperties()
            {
    
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
                            }
                        }
                    }
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
10. Merhaba aşağıdaki kod ekleme **oluşturur ve bir ardışık düzen etkinleştirir** toohello **ana** yöntemi. Bu işlem hattının **BlobSource**’u bir kaynak olarak, **BlobSink**’i ise bir havuz olarak alan bir **CopyActivity** etkinliği vardır.

    Merhaba kopya etkinliği Azure Data Factory'de hello veri taşımayı gerçekleştirir. Merhaba etkinlik verileri güvenli, güvenilir ve ölçeklenebilir bir şekilde çeşitli veri depolamaları arasında kopyalayabilirsiniz genel olarak kullanılabilir bir hizmet tarafından desteklenir. Bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale hello kopyalama etkinliği hakkında ayrıntılı bilgi için.

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
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
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
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
    
                },
            }
        }
    });
    ```
12. Aşağıdaki kodu toohello hello eklemek **ana** yöntemi tooget hello hello bir veri dilimin durumunu çıkış veri kümesi. Bu örnekte beklenen yalnızca bir dilim yoktur.

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
13. **(isteğe bağlı)**  Ekle hello aşağıdaki kod bir veri dilimi toohello çalıştırmak tooget ayrıntılarını **ana** yöntemi.

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
        });
    
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
14. Merhaba tarafından kullanılan yardımcı yöntemini aşağıdaki hello eklemek **ana** yöntemi toohello **Program** sınıfı. Bu yöntem sağlamanıza olanak tanıyan bir iletişim kutusu açılır **kullanıcı adı** ve **parola** tooAzure Portalı'nda toolog kullanın.

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

15. Merhaba projeyi Hello Çözüm Gezgini, genişletin: **DataFactoryAPITestApp**, sağ **başvuruları**, tıklatıp **Başvuru Ekle**. İçin bu onay kutusunu işaretleyin `System.Configuration` derleme ve tıklatın **Tamam**.
15. Merhaba konsol uygulaması oluşturun. Tıklatın **yapı** hello menüsüne ve ardından üzerinde **yapı çözümü**.
16. Olduğunu en az bir dosya hello adftutorial kapsayıcısında Azure blob depolama alanınızın onaylayın. Aksi durumda, Emp.txt dosyasını Not Defteri'nde aşağıdaki hello ile içerik oluşturun ve toohello adftutorial kapsayıcı yükleyin.

    ```
    John, Doe
    Jane, Doe
    ```
17. Tıklayarak Hello örneği çalıştırmak **hata ayıklama** -> **hata ayıklamayı Başlat** başlangıç menüsünde. Merhaba gördüğünüzde **veri dilimi ayrıntılarını çalıştırmak**, birkaç dakika basın için bekleyin ve **ENTER**.
18. Kullanım hello Azure portal tooverify bu hello veri fabrikası **APITutorialFactory** yapıları aşağıdaki hello ile oluşturulur:
    * Bağlantılı hizmeti: **AzureStorageLinkedService**
    * Veri kümesi: **DatasetBlobSource** ve **DatasetBlobDestination**.
    * İşlem hattı: **PipelineBlobSample**
19. Bir çıkış dosyası hello oluşturulduğunu doğrulayın **apifactoryoutput** hello klasöründe **adftutorial** kapsayıcı.

## <a name="get-a-list-of-failed-data-slices"></a>Başarısız olan veri dilimlerinin listesini al 

```csharp
// Parse hello resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a>Sonraki adımlar
Örnek verileri Azure blob depolama tooan Azure SQL veritabanından kopyalar .NET SDK kullanarak bir işlem hattı oluşturmak için aşağıdaki hello bakın: 

- [Blob Storage tooSQL veritabanı ' bir ardışık düzen toocopy verileri oluşturma](data-factory-copy-activity-tutorial-using-dotnet-api.md)
