---
title: "Yönetim .NET SDK v1.x Azure akış analizi için | Microsoft Docs"
description: "Stream Analytics yönetimi .NET SDK ile çalışmaya başlayın. Ayarlama ve analytics işleri çalıştırma hakkında bilgi edinin. Proje, giriş, çıkış ve dönüşümleri oluşturun."
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
ms.openlocfilehash: c75322ba53a447b8529023482945051caaf61bb2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="management-net-sdk-v1x-set-up-and-run-analytics-jobs-using-the-azure-stream-analytics-api-for-net"></a><span data-ttu-id="0ab1b-106">Yönetim .NET SDK'sı v1.x: ayarlamak ayarlama ve .NET için Azure Stream Analytics API'sini kullanarak analytics işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="0ab1b-106">Management .NET SDK v1.x: Set up and run analytics jobs using the Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="0ab1b-107">Ayarlamak ve yönetim .NET SDK kullanarak .NET için Stream Analytics API kullanarak analytics işleri çalıştırma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-107">Learn how to set up and run analytics jobs using the Stream Analytics API for .NET using the Management .NET SDK.</span></span> <span data-ttu-id="0ab1b-108">Bir projesi ayarlayın, giriş ve çıkış kaynakları, dönüştürme ve başlangıç oluşturun ve işleri durdurur.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="0ab1b-109">Analytics işleriniz için Blob depolama biriminden veya event hub'ındaki veri akışını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="0ab1b-110">Bkz: [.NET Stream Analytics API'si için yönetim başvuru belgelerine](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="0ab1b-110">See the [management reference documentation for the Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="0ab1b-111">Azure Stream Analytics akış verileri bulutta üzerinden düşük gecikmeli, yüksek oranda kullanılabilir, ölçeklenebilir, karmaşık olay işleme sağlayan tam olarak yönetilen bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in the cloud.</span></span> <span data-ttu-id="0ab1b-112">Akış analizi veri akışlarını çözümlemek için akış işlerinin ayarlamak müşteriler etkinleştirir ve gerçek zamanlı analiz sürücü almalarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-112">Stream Analytics enables customers to set up streaming jobs to analyze data streams, and allows them to drive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="0ab1b-113">Bu makaledeki örnek kod, yine Azure Stream Analytics yönetimi .NET SDK'ın eski (1.x) sürümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-113">Sample code in this article still uses legacy (1.x) version of Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="0ab1b-114">Güncel SDK sürümü kullanan örnek kod için lütfen bkz [akış analizi için yönetim .NET SDK'sını kullanma](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk).</span><span class="sxs-lookup"><span data-stu-id="0ab1b-114">For sample code using the up-to-date SDK version, please see [Use the Management .NET SDK for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ab1b-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0ab1b-115">Prerequisites</span></span>
<span data-ttu-id="0ab1b-116">Bu makaleye başlamadan önce aşağıdakilere sahip olmanız ve aşağıdaki işlemleri yapmış olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0ab1b-116">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="0ab1b-117">Visual Studio 2017 veya 2015 yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="0ab1b-118">İndirme ve yükleme [Azure .NET SDK'sı](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="0ab1b-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="0ab1b-119">Aboneliğinizde Azure kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="0ab1b-120">Örnek bir Azure PowerShell komut dosyası verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-120">The following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="0ab1b-121">Azure PowerShell bilgi için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview);</span><span class="sxs-lookup"><span data-stu-id="0ab1b-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in to your Azure account
        Add-AzureAccount

        # Select the Azure subscription you want to use to create the resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered to the subscription, remove the remark symbol (#) to run the Register-AzureRMProvider cmdlet to register the provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="0ab1b-122">Kullanmak için bir giriş kaynağı ve Çıkış hedefini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-122">Set up an input source and output target to use.</span></span> <span data-ttu-id="0ab1b-123">Daha ayrıntılı yönergeler için bkz [eklemek girişleri](stream-analytics-add-inputs.md) örnek giriş ayarlamak için ve [eklemek çıkışları](stream-analytics-add-outputs.md) örnek bir çıktı ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) to set up a sample input and [Add Outputs](stream-analytics-add-outputs.md) to set up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="0ab1b-124">Bir projesi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="0ab1b-124">Set up a project</span></span>
<span data-ttu-id="0ab1b-125">Bir analiz işi oluşturmak için .NET, ilk projenizi ayarlamak için Stream Analytics API kullanın.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-125">To create an analytics job use the Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="0ab1b-126">Visual Studio C# .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="0ab1b-127">Paket Yöneticisi Konsolu'nda NuGet paketlerini yüklemek için aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-127">In the Package Manager Console, run the following commands to install the NuGet packages.</span></span> <span data-ttu-id="0ab1b-128">İlk Azure Stream Analytics yönetimi .NET SDK ' dir.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-128">The first one is the Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="0ab1b-129">İkinci bir kimlik doğrulaması için kullanılacak Azure Active Directory istemcidir.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-129">The second one is the Azure Active Directory client that will be used for authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 1.8.3
        Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.28.4
3. <span data-ttu-id="0ab1b-130">Aşağıdakileri ekleyin **appSettings** App.config dosyasını bölümüne:</span><span class="sxs-lookup"><span data-stu-id="0ab1b-130">Add the following **appSettings** section to the App.config file:</span></span>
   
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

    <span data-ttu-id="0ab1b-131">İçin değerleri **Subscriptionıd** ve **ActiveDirectoryTenantId** Azure aboneliği ve Kiracı kimlikleri.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="0ab1b-132">Aşağıdaki Azure PowerShell cmdlet'ini çalıştırarak bu değerleri alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0ab1b-132">You can get these values by running the following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="0ab1b-133">Aşağıdaki başvuru .csproj dosyanızda ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0ab1b-133">Add the following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

1. <span data-ttu-id="0ab1b-134">Aşağıdakileri ekleyin **kullanarak** deyimleri projenin kaynak dosyasında (Program.cs):</span><span class="sxs-lookup"><span data-stu-id="0ab1b-134">Add the following **using** statements to the source file (Program.cs) in the project:</span></span>
   
        using System;
        using System.Configuration;
        using System.Threading.Tasks;
        
        using Microsoft.Azure;
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
2. <span data-ttu-id="0ab1b-135">Bir kimlik doğrulama yardımcı yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0ab1b-135">Add an authentication helper method:</span></span>

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

       throw new InvalidOperationException("Failed to acquire token");
   }
   ```  

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="0ab1b-136">Stream Analytics Yönetimi istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ab1b-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="0ab1b-137">A **StreamAnalyticsManagementClient** nesnesi, iş ve giriş, çıkış ve dönüştürme gibi iş bileşenlerini yönetmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-137">A **StreamAnalyticsManagementClient** object allows you to manage the job and the job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="0ab1b-138">Aşağıdaki kodu başlangıcına ekleyin **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="0ab1b-138">Add the following code to the beginning of the **Main** method:</span></span>

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

<span data-ttu-id="0ab1b-139">**ResourceGroupName** değişkenin değeri oluşturulduğunda veya bölümündeki önkoşul adımlarını çekilen kaynak grubunun adı ile aynı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-139">The **resourceGroupName** variable's value should be the same as the name of the resource group you created or picked in the prerequisite steps.</span></span>

<span data-ttu-id="0ab1b-140">Proje oluşturma kimlik bilgisi sunu yönünü otomatikleştirmek için başvurmak [bir hizmet sorumlusu Azure Resource Manager ile kimlik doğrulaması](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="0ab1b-140">To automate the credential presentation aspect of job creation, refer to [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="0ab1b-141">Bu makalenin kalan bölümlerinde Bu kod, başında olduğunu varsayın **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-141">The remaining sections of this article assume that this code is at the beginning of the **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="0ab1b-142">Akış Analizi işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ab1b-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="0ab1b-143">Aşağıdaki kod, tanımladığınız kaynak grubu altında Stream Analytics işi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-143">The following code creates a Stream Analytics job under the resource group that you have defined.</span></span> <span data-ttu-id="0ab1b-144">İş için bir giriş, çıkış ve dönüştürme daha sonra eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-144">You will add an input, output, and transformation to the job later.</span></span>

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


## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="0ab1b-145">Stream Analytics giriş kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ab1b-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="0ab1b-146">Aşağıdaki kod blob giriş kaynağı türü ve CSV serileştirme Stream Analytics giriş kaynağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-146">The following code creates a Stream Analytics input source with the blob input source type and CSV serialization.</span></span> <span data-ttu-id="0ab1b-147">Bir olay hub'ı giriş kaynağı oluşturmak için kullanın **EventHubStreamInputDataSource** yerine **BlobStreamInputDataSource**.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-147">To create an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="0ab1b-148">Benzer şekilde, giriş kaynağı seri hale getirme türü özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-148">Similarly, you can customize the serialization type of the input source.</span></span>

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

<span data-ttu-id="0ab1b-149">Giriş kaynağı, varsayılan olarak, belirli bir iş için Blob Depolama veya bir event hub bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-149">Input sources, whether from Blob storage or an event hub, are tied to a specific job.</span></span> <span data-ttu-id="0ab1b-150">Farklı projeler için aynı giriş kaynağı kullanmak için yeniden yöntemini çağırın ve başka bir iş adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-150">To use the same input source for different jobs, you must call the method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="0ab1b-151">Stream Analytics giriş kaynağı test</span><span class="sxs-lookup"><span data-stu-id="0ab1b-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="0ab1b-152">**TestConnection** yöntemi, Stream Analytics işi giriş kaynağına giriş kaynağı türüne özel sair yönlerini bağlanabiliyor olup olmadığını sınar.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-152">The **TestConnection** method tests whether the Stream Analytics job is able to connect to the input source as well as other aspects specific to the input source type.</span></span> <span data-ttu-id="0ab1b-153">Örneğin, bir önceki adımda oluşturduğunuz blob giriş kaynağında yanı sıra depolama hesabına bağlanmak için belirtilen kapsayıcının var olup olmadığını denetleyin depolama hesabı adı ve anahtar çifti kullanılabilir yöntem kontrol eder.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-153">For example, in the blob input source you created in an earlier step, the method will check that the Storage account name and key pair can be used to connect to the Storage account as well as check that the specified container exists.</span></span>

    // Test input source connection
    DataSourceTestConnectionResponse inputTestResponse =
        client.Inputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsInputName);

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="0ab1b-154">Stream Analytics Çıkış hedefini oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ab1b-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="0ab1b-155">Bir çıkış hedefini oluşturma, Stream Analytics giriş kaynağı oluşturmak için çok benzer.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-155">Creating an output target is very similar to creating a Stream Analytics input source.</span></span> <span data-ttu-id="0ab1b-156">Giriş kaynaklarıyla gibi belirli bir iş çıktı hedefleri bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-156">Like input sources, output targets are tied to a specific job.</span></span> <span data-ttu-id="0ab1b-157">Aynı çıktı hedefi olarak farklı işler için kullanmak üzere yeniden yöntemini çağırın ve başka bir iş adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-157">To use the same output target for different jobs, you must call the method again and specify a different job name.</span></span>

<span data-ttu-id="0ab1b-158">Aşağıdaki kod bir çıkış hedefini (Azure SQL veritabanı) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-158">The following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="0ab1b-159">Çıktı hedefin veri türüne ve/veya seri hale getirme türü özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-159">You can customize the output target's data type and/or serialization type.</span></span>

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

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="0ab1b-160">Stream Analytics Çıkış hedefini test</span><span class="sxs-lookup"><span data-stu-id="0ab1b-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="0ab1b-161">Stream Analytics Çıkış hedefini de sahip **TestConnection** bağlantıları sınama yöntemi.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-161">A Stream Analytics output target also has the **TestConnection** method for testing connections.</span></span>

    // Test output target connection
    DataSourceTestConnectionResponse outputTestResponse =
        client.Outputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsOutputName);

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="0ab1b-162">Stream Analytics dönüşüm oluşturun</span><span class="sxs-lookup"><span data-stu-id="0ab1b-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="0ab1b-163">Aşağıdaki kod bir akış analizi dönüştürmesi sorguyla oluşturur "seçin * giriş öğesinden" ve akış analizi işi için bir akış birimi ayırmak için belirtir.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-163">The following code creates a Stream Analytics transformation with the query "select * from Input" and specifies to allocate one streaming unit for the Stream Analytics job.</span></span> <span data-ttu-id="0ab1b-164">Akış birimleri ayarlama hakkında daha fazla bilgi için bkz: [ölçek Azure akış analizi işi](stream-analytics-scale-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="0ab1b-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

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

<span data-ttu-id="0ab1b-165">Giriş ve çıkış gibi bir dönüşüm de altında oluşturulan belirli Stream Analytics işi bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-165">Like input and output, a transformation is also tied to the specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="0ab1b-166">Akış analizi işi Başlat</span><span class="sxs-lookup"><span data-stu-id="0ab1b-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="0ab1b-167">Akış analizi işi ve kendi input(s), çıkışa ve dönüştürme oluşturduktan sonra iş çağırarak başlatabilirsiniz **Başlat** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start the job by calling the **Start** method.</span></span>

<span data-ttu-id="0ab1b-168">Aşağıdaki örnek kod başlatır Stream Analytics işi özel çıkış başlangıç saati ile 12:12:12 12 Kasım 2012 için ayarlanmış UTC:</span><span class="sxs-lookup"><span data-stu-id="0ab1b-168">The following sample code starts a Stream Analytics job with a custom output start time set to December 12, 2012, 12:12:12 UTC:</span></span>

    // Start a Stream Analytics job
    JobStartParameters jobStartParameters = new JobStartParameters
    {
        OutputStartMode = OutputStartMode.CustomTime,
        OutputStartTime = new DateTime(2012, 12, 12, 0, 0, 0, DateTimeKind.Utc)
    };

    LongRunningOperationResponse jobStartResponse = client.StreamingJobs.Start(resourceGroupName, streamAnalyticsJobName, jobStartParameters);

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="0ab1b-169">Stream Analytics işini durdurma</span><span class="sxs-lookup"><span data-stu-id="0ab1b-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="0ab1b-170">Çağırarak çalışan bir akış analizi işi durdurabilirsiniz **durdurmak** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-170">You can stop a running Stream Analytics job by calling the **Stop** method.</span></span>

    // Stop a Stream Analytics job
    LongRunningOperationResponse jobStopResponse = client.StreamingJobs.Stop(resourceGroupName, streamAnalyticsJobName);

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="0ab1b-171">Akış analizi işi Sil</span><span class="sxs-lookup"><span data-stu-id="0ab1b-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="0ab1b-172">**Silmek** yöntemi input(s), çıkışa ve dönüşüm işinin dahil olmak üzere temel alınan bir alt kaynaklara yanı sıra iş siler.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-172">The **Delete** method will delete the job as well as the underlying sub-resources, including input(s), output(s), and transformation of the job.</span></span>

    // Delete a Stream Analytics job
    LongRunningOperationResponse jobDeleteResponse = client.StreamingJobs.Delete(resourceGroupName, streamAnalyticsJobName);

## <a name="get-support"></a><span data-ttu-id="0ab1b-173">Destek alın</span><span class="sxs-lookup"><span data-stu-id="0ab1b-173">Get support</span></span>
<span data-ttu-id="0ab1b-174">Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="0ab1b-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ab1b-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0ab1b-175">Next steps</span></span>
<span data-ttu-id="0ab1b-176">Oluşturmak ve analytics işlerini çalıştırmak için .NET SDK kullanarak temelleri öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="0ab1b-176">You've learned the basics of using a .NET SDK to create and run analytics jobs.</span></span> <span data-ttu-id="0ab1b-177">Daha fazla bilgi edinmek için şunlara bakın:</span><span class="sxs-lookup"><span data-stu-id="0ab1b-177">To learn more, see the following:</span></span>

* [<span data-ttu-id="0ab1b-178">Azure Stream Analytics'e giriş</span><span class="sxs-lookup"><span data-stu-id="0ab1b-178">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="0ab1b-179">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="0ab1b-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="0ab1b-180">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="0ab1b-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="0ab1b-181">[Azure Stream Analytics yönetimi .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="0ab1b-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="0ab1b-182">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="0ab1b-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="0ab1b-183">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="0ab1b-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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
