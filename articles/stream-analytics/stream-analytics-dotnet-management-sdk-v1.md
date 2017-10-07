---
title: "Azure akış analizi için aaaManagement .NET SDK'sı v1.x | Microsoft Docs"
description: "Stream Analytics yönetimi .NET SDK ile çalışmaya başlayın. Bilgi nasıl tooset yukarı ve analytics işlerini çalıştırın. Proje, giriş, çıkış ve dönüşümleri oluşturun."
keywords: .NET SDK, API analizi
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5e93de87-0c6f-4f4b-be98-08d63f832897
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/06/2017
ms.author: jeffstok
ms.openlocfilehash: d205c388880e3d9c2ca5df218f4b68abac8c9780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="management-net-sdk-v1x-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a>Yönetim .NET SDK'sı v1.x: ayarlama ve çalıştırma analytics işleri kullanarak .NET için Azure Stream Analytics API hello
Yukarı tooset ve .NET için hello Stream Analytics API kullanarak çalışma analytics işleri yönetimi .NET SDK'sı nasıl hello öğrenin. Bir projesi ayarlayın, giriş ve çıkış kaynakları, dönüştürme ve başlangıç oluşturun ve işleri durdurur. Analytics işleriniz için Blob depolama biriminden veya event hub'ındaki veri akışını sağlayabilirsiniz.

Merhaba bkz [.NET hello Stream Analytics API'si için yönetim başvuru belgelerine](https://msdn.microsoft.com/library/azure/dn889315.aspx).

Azure Stream Analytics hello bulutta veri akış üzerinden düşük gecikmeli, yüksek oranda kullanılabilir, ölçeklenebilir, karmaşık olay işleme sağlayan tam olarak yönetilen bir hizmettir. Akış analizi işleri tooanalyze veri akışlarını akış yukarı müşteriler tooset etkinleştirir ve neredeyse gerçek zamanlı analiz toodrive sağlar.  

> [!NOTE]
> Bu makaledeki örnek kod, yine Azure Stream Analytics yönetimi .NET SDK'ın eski (1.x) sürümünü kullanır. Merhaba güncel SDK sürümü kullanan örnek kod için lütfen bkz [kullanım hello akış analizi için yönetim .NET SDK'sı](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk).

## <a name="prerequisites"></a>Ön koşullar
Bu makaleye başlamadan önce hello şunlara sahip olmanız gerekir:

* Visual Studio 2017 veya 2015 yükleyin.
* İndirme ve yükleme [Azure .NET SDK'sı](https://azure.microsoft.com/downloads/).
* Aboneliğinizde Azure kaynak grubu oluşturun. Merhaba, örnek bir Azure PowerShell komut dosyası aşağıdadır. Azure PowerShell bilgi için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview);  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* Bir giriş kaynağı ayarlama ve hedef toouse çıktı. Daha ayrıntılı yönergeler için bkz [girişleri eklemek](stream-analytics-add-inputs.md) tooset örnek giriş yukarı ve [eklemek çıkışları](stream-analytics-add-outputs.md) tooset örnek bir çıktı ayarlama.

## <a name="set-up-a-project"></a>Bir projesi ayarlayın
toocreate analytics işi kullanılmak hello Stream Analytics API .NET, ilk projenizi ayarlayın.

1. Visual Studio C# .NET konsol uygulaması oluşturun.
2. Hello Paket Yöneticisi konsolu, tooinstall hello NuGet paketlerini çalışma hello aşağıdaki komutları. Merhaba ilk hello Azure Stream Analytics yönetimi .NET SDK'sı biridir. Merhaba ikinci bir kimlik doğrulaması için kullanılacak hello Azure Active Directory istemcidir.
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 1.8.3
        Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.28.4
3. Merhaba aşağıdakileri ekleyin **appSettings** bölüm toohello App.config dosyası:
   
        <appSettings>
          <!--CSM Prod related values-->
          <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
          <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
          <add key="WindowsManagementUri" value="https://management.core.windows.net/" />
          <add key="AsaClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR AZURE SUBSCRIPTION" />
          <add key="ActiveDirectoryTenantId" value="YOU TENANT ID" />
        </appSettings>

    İçin değerleri **Subscriptionıd** ve **ActiveDirectoryTenantId** Azure aboneliği ve Kiracı kimlikleri. Merhaba aşağıdaki Azure PowerShell cmdlet'ini çalıştırarak bu değerleri alabilirsiniz:

        Get-AzureAccount

4. Başvuru .csproj dosyanızda aşağıdaki hello ekleyin:

        <Reference Include="System.Configuration" />

1. Merhaba aşağıdakileri ekleyin **kullanarak** hello projesindeki deyimleri toohello kaynak dosyasını (Program.cs):
   
        using System;
        using System.Configuration;
        using System.Threading.Tasks;
        
        using Microsoft.Azure;
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
2. Bir kimlik doğrulama yardımcı yöntemi ekleyin:

   ```   
   private static async Task<string> GetAuthorizationHeader()
   {
       var context = new AuthenticationContext(
           ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] +
           ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);

        AuthenticationResult result = await context.AcquireTokenASync(
           resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
           clientId: ConfigurationManager.AppSettings["AsaClientId"],
           redirectUri: new Uri(ConfigurationManager.AppSettings["RedirectUri"]),
           promptBehavior: PromptBehavior.Always);

        if (result != null)
            return result.AccessToken;

       throw new InvalidOperationException("Failed tooacquire token");
   }
   ```  

## <a name="create-a-stream-analytics-management-client"></a>Stream Analytics Yönetimi istemcisi oluşturma
A **StreamAnalyticsManagementClient** nesne toomanage hello iş ve hello iş bileşenleri, giriş, çıkış ve dönüştürme gibi sağlar.

Kod toohello hello başlangıcını izleyen hello eklemek **ana** yöntemi:

    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamAnalyticsJobName = "<YOUR STREAM ANALYTICS JOB NAME>";
    string streamAnalyticsInputName = "<YOUR JOB INPUT NAME>";
    string streamAnalyticsOutputName = "<YOUR JOB OUTPUT NAME>";
    string streamAnalyticsTransformationName = "<YOUR JOB TRANSFORMATION NAME>";

    // Get authentication token
    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
        ConfigurationManager.AppSettings["SubscriptionId"],
        GetAuthorizationHeader().Result);

    // Create Stream Analytics management client
    StreamAnalyticsManagementClient client = new StreamAnalyticsManagementClient(aadTokenCredentials);

Merhaba **resourceGroupName** değişkenin değeri hello adı hello kaynak ile aynı grup oluşturan veya hello önkoşul adımlarını çekilen hello olması gerekir.

tooautomate hello kimlik bilgisi sunu, iş oluşturma yönünü başvurmak çok[bir hizmet sorumlusu Azure Resource Manager ile kimlik doğrulaması](../azure-resource-manager/resource-group-authenticate-service-principal.md).

Merhaba, bu makalenin kalan bölümleri bu kodu hello hello başında olduğunu varsayın **ana** yöntemi.

## <a name="create-a-stream-analytics-job"></a>Akış Analizi işi oluşturma
Merhaba aşağıdaki kod, tanımladığınız hello kaynak grubu altında Stream Analytics işi oluşturur. Bir giriş, çıkış ve dönüştürme toohello işi daha sonra eklersiniz.

    // Create a Stream Analytics job
    JobCreateOrUpdateParameters jobCreateParameters = new JobCreateOrUpdateParameters()
    {
        Job = new Job()
        {
            Name = streamAnalyticsJobName,
            Location = "<LOCATION>",
            Properties = new JobProperties()
            {
                EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Adjust,
                Sku = new Sku()
                {
                    Name = "Standard"
                }
            }
        }
    };

    JobCreateOrUpdateResponse jobCreateResponse = client.StreamingJobs.CreateOrUpdate(resourceGroupName, jobCreateParameters);


## <a name="create-a-stream-analytics-input-source"></a>Stream Analytics giriş kaynağı oluşturma
Merhaba aşağıdaki kodu Stream Analytics giriş kaynağı hello blob giriş kaynağı türü ve CSV serileştirme oluşturur. toocreate bir olay hub'ı giriş kaynağı kullanmak **EventHubStreamInputDataSource** yerine **BlobStreamInputDataSource**. Benzer şekilde, hello giriş kaynağının hello seri hale getirme türü özelleştirebilirsiniz.

    // Create a Stream Analytics input source
    InputCreateOrUpdateParameters jobInputCreateParameters = new InputCreateOrUpdateParameters()
    {
        Input = new Input()
        {
            Name = streamAnalyticsInputName,
            Properties = new StreamInputProperties()
            {
                Serialization = new CsvSerialization
                {
                    Properties = new CsvSerializationProperties
                    {
                        Encoding = "UTF8",
                        FieldDelimiter = ","
                    }
                },
                DataSource = new BlobStreamInputDataSource
                {
                    Properties = new BlobStreamInputDataSourceProperties
                    {
                        StorageAccounts = new StorageAccount[]
                        {
                            new StorageAccount()
                            {
                                AccountName = "<YOUR STORAGE ACCOUNT NAME>",
                                AccountKey = "<YOUR STORAGE ACCOUNT KEY>"
                            }
                        },
                        Container = "samples",
                        PathPattern = ""
                    }
                }
            }
        }
    };

    InputCreateOrUpdateResponse inputCreateResponse =
        client.Inputs.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, jobInputCreateParameters);

Giriş kaynağı, Blob Depolama veya bir event hub bağlı tooa belirli iş arasındadır. toouse Merhaba farklı işleri için aynı giriş kaynağı, yeniden hello yöntemini çağırın ve başka bir iş adı belirtmeniz gerekir.

## <a name="test-a-stream-analytics-input-source"></a>Stream Analytics giriş kaynağı test
Merhaba **TestConnection** hello Stream Analytics işi mümkün tooconnect toohello olup olmadığını giriş kaynağı, hem de diğer yönlerini belirli toohello yöntemi testleri giriş kaynak türü. Örneğin, bir önceki adımda oluşturduğunuz hello blob giriş kaynağı hello yöntemi hello depolama hesabı adı ve anahtar çifti kullanılan tooconnect toohello depolama hesabı olması yanı sıra, bu hello belirtilen kapsayıcı varlığını denetle kontrol eder.

    // Test input source connection
    DataSourceTestConnectionResponse inputTestResponse =
        client.Inputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsInputName);

## <a name="create-a-stream-analytics-output-target"></a>Stream Analytics Çıkış hedefini oluşturma
Bir çıkış hedefini oluşturma çok benzer toocreating Stream Analytics giriş kaynağına bağlıdır. Giriş gibi çıktı hedefleri bağlı tooa belirli iş kaynaklardır. toouse farklı işleri için aynı çıkış hedefini Merhaba, yeniden hello yöntemini çağırın ve başka bir iş adı belirtmeniz gerekir.

koddan hello Çıkış hedefini (Azure SQL veritabanı) oluşturur. Merhaba çıkış hedefin veri türüne ve/veya seri hale getirme türü özelleştirebilirsiniz.

    // Create a Stream Analytics output target
    OutputCreateOrUpdateParameters jobOutputCreateParameters = new OutputCreateOrUpdateParameters()
    {
        Output = new Output()
        {
            Name = streamAnalyticsOutputName,
            Properties = new OutputProperties()
            {
                DataSource = new SqlAzureOutputDataSource()
                {
                    Properties = new SqlAzureOutputDataSourceProperties()
                    {
                        Server = "<YOUR DATABASE SERVER NAME>",
                        Database = "<YOUR DATABASE NAME>",
                        User = "<YOUR DATABASE LOGIN>",
                        Password = "<YOUR DATABASE LOGIN PASSWORD>",
                        Table = "<YOUR DATABASE TABLE NAME>"
                    }
                }
            }
        }
    };

    OutputCreateOrUpdateResponse outputCreateResponse =
        client.Outputs.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, jobOutputCreateParameters);

## <a name="test-a-stream-analytics-output-target"></a>Stream Analytics Çıkış hedefini test
Stream Analytics Çıkış hedefini hello de sahip **TestConnection** bağlantıları sınama yöntemi.

    // Test output target connection
    DataSourceTestConnectionResponse outputTestResponse =
        client.Outputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsOutputName);

## <a name="create-a-stream-analytics-transformation"></a>Stream Analytics dönüşüm oluşturun
Merhaba aşağıdaki kod bir akış analizi dönüştürmesi hello sorguyla oluşturur "seçin * giriş öğesinden" Merhaba Stream Analytics işi için bir akış birimi tooallocate belirtir. Akış birimleri ayarlama hakkında daha fazla bilgi için bkz: [ölçek Azure akış analizi işi](stream-analytics-scale-jobs.md).

    // Create a Stream Analytics transformation
    TransformationCreateOrUpdateParameters transformationCreateParameters = new TransformationCreateOrUpdateParameters()
    {
        Transformation = new Transformation()
        {
            Name = streamAnalyticsTransformationName,
            Properties = new TransformationProperties()
            {
                StreamingUnits = 1,
                Query = "select * from Input"
            }
        }
    };

    var transformationCreateResp =
        client.Transformations.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, transformationCreateParameters);

Giriş ve çıkış gibi bir dönüşüm de altında oluşturulduğu bağlı toohello belirli akış analizi işi ' dir.

## <a name="start-a-stream-analytics-job"></a>Akış analizi işi Başlat
Akış analizi işi ve kendi input(s), çıkışa ve dönüştürme oluşturduktan sonra arama hello tarafından hello işi başlatabilir **Başlat** yöntemi.

Aşağıdaki örnek kod hello başlatır Stream Analytics işi bir özel çıkış başlangıç saati kümesi tooDecember ile 12, 2012, 12:12:12 UTC:

    // Start a Stream Analytics job
    JobStartParameters jobStartParameters = new JobStartParameters
    {
        OutputStartMode = OutputStartMode.CustomTime,
        OutputStartTime = new DateTime(2012, 12, 12, 0, 0, 0, DateTimeKind.Utc)
    };

    LongRunningOperationResponse jobStartResponse = client.StreamingJobs.Start(resourceGroupName, streamAnalyticsJobName, jobStartParameters);

## <a name="stop-a-stream-analytics-job"></a>Stream Analytics işini durdurma
Çalışan bir akış analizi işi tarafından arama hello durdurabilirsiniz **durdurmak** yöntemi.

    // Stop a Stream Analytics job
    LongRunningOperationResponse jobStopResponse = client.StreamingJobs.Stop(resourceGroupName, streamAnalyticsJobName);

## <a name="delete-a-stream-analytics-job"></a>Akış analizi işi Sil
Merhaba **silmek** yöntemi input(s) ve çıkışa hello iş dönüşümü çeşitli alt kaynakları temel hello yanı sıra hello işi siler.

    // Delete a Stream Analytics job
    LongRunningOperationResponse jobDeleteResponse = client.StreamingJobs.Delete(resourceGroupName, streamAnalyticsJobName);

## <a name="get-support"></a>Destek alın
Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Sonraki adımlar
.NET SDK'sı toocreate kullanmanın hello temel konuları öğrendiğinize göre artık ve analytics işlerini çalıştırın. toolearn daha hello aşağıdaki bakın:

* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics yönetimi .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->
[5]: ./media/markdown-template-for-new-articles/octocats.png
[6]: ./media/markdown-template-for-new-articles/pretty49.png
[7]: ./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[azure.blob.storage]: http://azure.microsoft.com/documentation/services/storage/
[azure.blob.storage.use]: http://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/

[azure.event.hubs]: http://azure.microsoft.com/services/event-hubs/
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.forum]: http://go.microsoft.com/fwlink/?LinkId=512151

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
