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
# <a name="management-net-sdk-v1x-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a><span data-ttu-id="b2f14-106">Yönetim .NET SDK'sı v1.x: ayarlama ve çalıştırma analytics işleri kullanarak .NET için Azure Stream Analytics API hello</span><span class="sxs-lookup"><span data-stu-id="b2f14-106">Management .NET SDK v1.x: Set up and run analytics jobs using hello Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="b2f14-107">Yukarı tooset ve .NET için hello Stream Analytics API kullanarak çalışma analytics işleri yönetimi .NET SDK'sı nasıl hello öğrenin.</span><span class="sxs-lookup"><span data-stu-id="b2f14-107">Learn how tooset up and run analytics jobs using hello Stream Analytics API for .NET using hello Management .NET SDK.</span></span> <span data-ttu-id="b2f14-108">Bir projesi ayarlayın, giriş ve çıkış kaynakları, dönüştürme ve başlangıç oluşturun ve işleri durdurur.</span><span class="sxs-lookup"><span data-stu-id="b2f14-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="b2f14-109">Analytics işleriniz için Blob depolama biriminden veya event hub'ındaki veri akışını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2f14-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="b2f14-110">Merhaba bkz [.NET hello Stream Analytics API'si için yönetim başvuru belgelerine](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2f14-110">See hello [management reference documentation for hello Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="b2f14-111">Azure Stream Analytics hello bulutta veri akış üzerinden düşük gecikmeli, yüksek oranda kullanılabilir, ölçeklenebilir, karmaşık olay işleme sağlayan tam olarak yönetilen bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="b2f14-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="b2f14-112">Akış analizi işleri tooanalyze veri akışlarını akış yukarı müşteriler tooset etkinleştirir ve neredeyse gerçek zamanlı analiz toodrive sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2f14-112">Stream Analytics enables customers tooset up streaming jobs tooanalyze data streams, and allows them toodrive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="b2f14-113">Bu makaledeki örnek kod, yine Azure Stream Analytics yönetimi .NET SDK'ın eski (1.x) sürümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="b2f14-113">Sample code in this article still uses legacy (1.x) version of Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="b2f14-114">Merhaba güncel SDK sürümü kullanan örnek kod için lütfen bkz [kullanım hello akış analizi için yönetim .NET SDK'sı](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk).</span><span class="sxs-lookup"><span data-stu-id="b2f14-114">For sample code using hello up-to-date SDK version, please see [Use hello Management .NET SDK for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2f14-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b2f14-115">Prerequisites</span></span>
<span data-ttu-id="b2f14-116">Bu makaleye başlamadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="b2f14-116">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="b2f14-117">Visual Studio 2017 veya 2015 yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b2f14-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="b2f14-118">İndirme ve yükleme [Azure .NET SDK'sı](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="b2f14-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="b2f14-119">Aboneliğinizde Azure kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b2f14-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="b2f14-120">Merhaba, örnek bir Azure PowerShell komut dosyası aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="b2f14-120">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="b2f14-121">Azure PowerShell bilgi için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview);</span><span class="sxs-lookup"><span data-stu-id="b2f14-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="b2f14-122">Bir giriş kaynağı ayarlama ve hedef toouse çıktı.</span><span class="sxs-lookup"><span data-stu-id="b2f14-122">Set up an input source and output target toouse.</span></span> <span data-ttu-id="b2f14-123">Daha ayrıntılı yönergeler için bkz [girişleri eklemek](stream-analytics-add-inputs.md) tooset örnek giriş yukarı ve [eklemek çıkışları](stream-analytics-add-outputs.md) tooset örnek bir çıktı ayarlama.</span><span class="sxs-lookup"><span data-stu-id="b2f14-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) tooset up a sample input and [Add Outputs](stream-analytics-add-outputs.md) tooset up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="b2f14-124">Bir projesi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="b2f14-124">Set up a project</span></span>
<span data-ttu-id="b2f14-125">toocreate analytics işi kullanılmak hello Stream Analytics API .NET, ilk projenizi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b2f14-125">toocreate an analytics job use hello Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="b2f14-126">Visual Studio C# .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b2f14-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="b2f14-127">Hello Paket Yöneticisi konsolu, tooinstall hello NuGet paketlerini çalışma hello aşağıdaki komutları.</span><span class="sxs-lookup"><span data-stu-id="b2f14-127">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="b2f14-128">Merhaba ilk hello Azure Stream Analytics yönetimi .NET SDK'sı biridir.</span><span class="sxs-lookup"><span data-stu-id="b2f14-128">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="b2f14-129">Merhaba ikinci bir kimlik doğrulaması için kullanılacak hello Azure Active Directory istemcidir.</span><span class="sxs-lookup"><span data-stu-id="b2f14-129">hello second one is hello Azure Active Directory client that will be used for authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 1.8.3
        Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.28.4
3. <span data-ttu-id="b2f14-130">Merhaba aşağıdakileri ekleyin **appSettings** bölüm toohello App.config dosyası:</span><span class="sxs-lookup"><span data-stu-id="b2f14-130">Add hello following **appSettings** section toohello App.config file:</span></span>
   
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

    <span data-ttu-id="b2f14-131">İçin değerleri **Subscriptionıd** ve **ActiveDirectoryTenantId** Azure aboneliği ve Kiracı kimlikleri.</span><span class="sxs-lookup"><span data-stu-id="b2f14-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="b2f14-132">Merhaba aşağıdaki Azure PowerShell cmdlet'ini çalıştırarak bu değerleri alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b2f14-132">You can get these values by running hello following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="b2f14-133">Başvuru .csproj dosyanızda aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b2f14-133">Add hello following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

1. <span data-ttu-id="b2f14-134">Merhaba aşağıdakileri ekleyin **kullanarak** hello projesindeki deyimleri toohello kaynak dosyasını (Program.cs):</span><span class="sxs-lookup"><span data-stu-id="b2f14-134">Add hello following **using** statements toohello source file (Program.cs) in hello project:</span></span>
   
        using System;
        using System.Configuration;
        using System.Threading.Tasks;
        
        using Microsoft.Azure;
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
2. <span data-ttu-id="b2f14-135">Bir kimlik doğrulama yardımcı yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b2f14-135">Add an authentication helper method:</span></span>

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

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="b2f14-136">Stream Analytics Yönetimi istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2f14-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="b2f14-137">A **StreamAnalyticsManagementClient** nesne toomanage hello iş ve hello iş bileşenleri, giriş, çıkış ve dönüştürme gibi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2f14-137">A **StreamAnalyticsManagementClient** object allows you toomanage hello job and hello job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="b2f14-138">Kod toohello hello başlangıcını izleyen hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="b2f14-138">Add hello following code toohello beginning of hello **Main** method:</span></span>

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

<span data-ttu-id="b2f14-139">Merhaba **resourceGroupName** değişkenin değeri hello adı hello kaynak ile aynı grup oluşturan veya hello önkoşul adımlarını çekilen hello olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2f14-139">hello **resourceGroupName** variable's value should be hello same as hello name of hello resource group you created or picked in hello prerequisite steps.</span></span>

<span data-ttu-id="b2f14-140">tooautomate hello kimlik bilgisi sunu, iş oluşturma yönünü başvurmak çok[bir hizmet sorumlusu Azure Resource Manager ile kimlik doğrulaması](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="b2f14-140">tooautomate hello credential presentation aspect of job creation, refer too[Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="b2f14-141">Merhaba, bu makalenin kalan bölümleri bu kodu hello hello başında olduğunu varsayın **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="b2f14-141">hello remaining sections of this article assume that this code is at hello beginning of hello **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="b2f14-142">Akış Analizi işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2f14-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="b2f14-143">Merhaba aşağıdaki kod, tanımladığınız hello kaynak grubu altında Stream Analytics işi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b2f14-143">hello following code creates a Stream Analytics job under hello resource group that you have defined.</span></span> <span data-ttu-id="b2f14-144">Bir giriş, çıkış ve dönüştürme toohello işi daha sonra eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="b2f14-144">You will add an input, output, and transformation toohello job later.</span></span>

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


## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="b2f14-145">Stream Analytics giriş kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2f14-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="b2f14-146">Merhaba aşağıdaki kodu Stream Analytics giriş kaynağı hello blob giriş kaynağı türü ve CSV serileştirme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b2f14-146">hello following code creates a Stream Analytics input source with hello blob input source type and CSV serialization.</span></span> <span data-ttu-id="b2f14-147">toocreate bir olay hub'ı giriş kaynağı kullanmak **EventHubStreamInputDataSource** yerine **BlobStreamInputDataSource**.</span><span class="sxs-lookup"><span data-stu-id="b2f14-147">toocreate an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="b2f14-148">Benzer şekilde, hello giriş kaynağının hello seri hale getirme türü özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2f14-148">Similarly, you can customize hello serialization type of hello input source.</span></span>

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

<span data-ttu-id="b2f14-149">Giriş kaynağı, Blob Depolama veya bir event hub bağlı tooa belirli iş arasındadır.</span><span class="sxs-lookup"><span data-stu-id="b2f14-149">Input sources, whether from Blob storage or an event hub, are tied tooa specific job.</span></span> <span data-ttu-id="b2f14-150">toouse Merhaba farklı işleri için aynı giriş kaynağı, yeniden hello yöntemini çağırın ve başka bir iş adı belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2f14-150">toouse hello same input source for different jobs, you must call hello method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="b2f14-151">Stream Analytics giriş kaynağı test</span><span class="sxs-lookup"><span data-stu-id="b2f14-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="b2f14-152">Merhaba **TestConnection** hello Stream Analytics işi mümkün tooconnect toohello olup olmadığını giriş kaynağı, hem de diğer yönlerini belirli toohello yöntemi testleri giriş kaynak türü.</span><span class="sxs-lookup"><span data-stu-id="b2f14-152">hello **TestConnection** method tests whether hello Stream Analytics job is able tooconnect toohello input source as well as other aspects specific toohello input source type.</span></span> <span data-ttu-id="b2f14-153">Örneğin, bir önceki adımda oluşturduğunuz hello blob giriş kaynağı hello yöntemi hello depolama hesabı adı ve anahtar çifti kullanılan tooconnect toohello depolama hesabı olması yanı sıra, bu hello belirtilen kapsayıcı varlığını denetle kontrol eder.</span><span class="sxs-lookup"><span data-stu-id="b2f14-153">For example, in hello blob input source you created in an earlier step, hello method will check that hello Storage account name and key pair can be used tooconnect toohello Storage account as well as check that hello specified container exists.</span></span>

    // Test input source connection
    DataSourceTestConnectionResponse inputTestResponse =
        client.Inputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsInputName);

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="b2f14-154">Stream Analytics Çıkış hedefini oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2f14-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="b2f14-155">Bir çıkış hedefini oluşturma çok benzer toocreating Stream Analytics giriş kaynağına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b2f14-155">Creating an output target is very similar toocreating a Stream Analytics input source.</span></span> <span data-ttu-id="b2f14-156">Giriş gibi çıktı hedefleri bağlı tooa belirli iş kaynaklardır.</span><span class="sxs-lookup"><span data-stu-id="b2f14-156">Like input sources, output targets are tied tooa specific job.</span></span> <span data-ttu-id="b2f14-157">toouse farklı işleri için aynı çıkış hedefini Merhaba, yeniden hello yöntemini çağırın ve başka bir iş adı belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2f14-157">toouse hello same output target for different jobs, you must call hello method again and specify a different job name.</span></span>

<span data-ttu-id="b2f14-158">koddan hello Çıkış hedefini (Azure SQL veritabanı) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b2f14-158">hello following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="b2f14-159">Merhaba çıkış hedefin veri türüne ve/veya seri hale getirme türü özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2f14-159">You can customize hello output target's data type and/or serialization type.</span></span>

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

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="b2f14-160">Stream Analytics Çıkış hedefini test</span><span class="sxs-lookup"><span data-stu-id="b2f14-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="b2f14-161">Stream Analytics Çıkış hedefini hello de sahip **TestConnection** bağlantıları sınama yöntemi.</span><span class="sxs-lookup"><span data-stu-id="b2f14-161">A Stream Analytics output target also has hello **TestConnection** method for testing connections.</span></span>

    // Test output target connection
    DataSourceTestConnectionResponse outputTestResponse =
        client.Outputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsOutputName);

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="b2f14-162">Stream Analytics dönüşüm oluşturun</span><span class="sxs-lookup"><span data-stu-id="b2f14-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="b2f14-163">Merhaba aşağıdaki kod bir akış analizi dönüştürmesi hello sorguyla oluşturur "seçin * giriş öğesinden" Merhaba Stream Analytics işi için bir akış birimi tooallocate belirtir.</span><span class="sxs-lookup"><span data-stu-id="b2f14-163">hello following code creates a Stream Analytics transformation with hello query "select * from Input" and specifies tooallocate one streaming unit for hello Stream Analytics job.</span></span> <span data-ttu-id="b2f14-164">Akış birimleri ayarlama hakkında daha fazla bilgi için bkz: [ölçek Azure akış analizi işi](stream-analytics-scale-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="b2f14-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

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

<span data-ttu-id="b2f14-165">Giriş ve çıkış gibi bir dönüşüm de altında oluşturulduğu bağlı toohello belirli akış analizi işi ' dir.</span><span class="sxs-lookup"><span data-stu-id="b2f14-165">Like input and output, a transformation is also tied toohello specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="b2f14-166">Akış analizi işi Başlat</span><span class="sxs-lookup"><span data-stu-id="b2f14-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="b2f14-167">Akış analizi işi ve kendi input(s), çıkışa ve dönüştürme oluşturduktan sonra arama hello tarafından hello işi başlatabilir **Başlat** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="b2f14-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start hello job by calling hello **Start** method.</span></span>

<span data-ttu-id="b2f14-168">Aşağıdaki örnek kod hello başlatır Stream Analytics işi bir özel çıkış başlangıç saati kümesi tooDecember ile 12, 2012, 12:12:12 UTC:</span><span class="sxs-lookup"><span data-stu-id="b2f14-168">hello following sample code starts a Stream Analytics job with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC:</span></span>

    // Start a Stream Analytics job
    JobStartParameters jobStartParameters = new JobStartParameters
    {
        OutputStartMode = OutputStartMode.CustomTime,
        OutputStartTime = new DateTime(2012, 12, 12, 0, 0, 0, DateTimeKind.Utc)
    };

    LongRunningOperationResponse jobStartResponse = client.StreamingJobs.Start(resourceGroupName, streamAnalyticsJobName, jobStartParameters);

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="b2f14-169">Stream Analytics işini durdurma</span><span class="sxs-lookup"><span data-stu-id="b2f14-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="b2f14-170">Çalışan bir akış analizi işi tarafından arama hello durdurabilirsiniz **durdurmak** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="b2f14-170">You can stop a running Stream Analytics job by calling hello **Stop** method.</span></span>

    // Stop a Stream Analytics job
    LongRunningOperationResponse jobStopResponse = client.StreamingJobs.Stop(resourceGroupName, streamAnalyticsJobName);

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="b2f14-171">Akış analizi işi Sil</span><span class="sxs-lookup"><span data-stu-id="b2f14-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="b2f14-172">Merhaba **silmek** yöntemi input(s) ve çıkışa hello iş dönüşümü çeşitli alt kaynakları temel hello yanı sıra hello işi siler.</span><span class="sxs-lookup"><span data-stu-id="b2f14-172">hello **Delete** method will delete hello job as well as hello underlying sub-resources, including input(s), output(s), and transformation of hello job.</span></span>

    // Delete a Stream Analytics job
    LongRunningOperationResponse jobDeleteResponse = client.StreamingJobs.Delete(resourceGroupName, streamAnalyticsJobName);

## <a name="get-support"></a><span data-ttu-id="b2f14-173">Destek alın</span><span class="sxs-lookup"><span data-stu-id="b2f14-173">Get support</span></span>
<span data-ttu-id="b2f14-174">Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="b2f14-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2f14-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b2f14-175">Next steps</span></span>
<span data-ttu-id="b2f14-176">.NET SDK'sı toocreate kullanmanın hello temel konuları öğrendiğinize göre artık ve analytics işlerini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b2f14-176">You've learned hello basics of using a .NET SDK toocreate and run analytics jobs.</span></span> <span data-ttu-id="b2f14-177">toolearn daha hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="b2f14-177">toolearn more, see hello following:</span></span>

* [<span data-ttu-id="b2f14-178">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="b2f14-178">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="b2f14-179">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="b2f14-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="b2f14-180">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="b2f14-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="b2f14-181">[Azure Stream Analytics yönetimi .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2f14-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="b2f14-182">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="b2f14-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="b2f14-183">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="b2f14-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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
