---
title: "Program aracılığıyla akış analizi işleri izleme | Microsoft Docs"
description: "Program aracılığıyla REST API'leri, Azure SDK'sı veya PowerShell oluşturulan akış analizi işleri izleme öğrenin."
keywords: ".NET izleme, iş izleme, izleme uygulaması"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 2ec02cc9-4ca5-4a25-ae60-c44be9ad4835
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 0d39e77316a03a705586af3ba970a7be1208ec85
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a><span data-ttu-id="a9073-104">Program aracılığıyla bir akış analizi işi İzleyicisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9073-104">Programmatically create a Stream Analytics job monitor</span></span>

<span data-ttu-id="a9073-105">Bu makalede, Stream Analytics işi için izlemeyi etkinleştirmek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a9073-105">This article demonstrates how to enable monitoring for a Stream Analytics job.</span></span> <span data-ttu-id="a9073-106">REST API'leri, Azure SDK'sı veya PowerShell oluşturulan stream Analytics işlerini izleme varsayılan olarak etkin gerekmez.</span><span class="sxs-lookup"><span data-stu-id="a9073-106">Stream Analytics jobs that are created via REST APIs, Azure SDK, or PowerShell do not have monitoring enabled by default.</span></span> <span data-ttu-id="a9073-107">El ile Azure portalında iş İzleyici sayfasına giderek ve etkinleştir düğmesine tıkladığınızda etkinleştirebilirsiniz veya bu makaledeki adımları izleyerek bu işlemi otomatikleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9073-107">You can manually enable it in the Azure portal by going to the job’s Monitor page and clicking the Enable button or you can automate this process by following the steps in this article.</span></span> <span data-ttu-id="a9073-108">İzleme verilerini Stream Analytics işiniz için Azure portal, ölçümleri alanında görünecektir.</span><span class="sxs-lookup"><span data-stu-id="a9073-108">The monitoring data will show up in the Metrics area of the Azure portal for your Stream Analytics job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9073-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a9073-109">Prerequisites</span></span>

<span data-ttu-id="a9073-110">Bu işlem başlamadan önce aşağıdakilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a9073-110">Before you begin this process, you must have the following:</span></span>

* <span data-ttu-id="a9073-111">Visual Studio 2017 veya 2015</span><span class="sxs-lookup"><span data-stu-id="a9073-111">Visual Studio 2017 or 2015</span></span>
* <span data-ttu-id="a9073-112">[Azure .NET SDK'sı](https://azure.microsoft.com/downloads/) indirilir ve yüklenir</span><span class="sxs-lookup"><span data-stu-id="a9073-112">[Azure .NET SDK](https://azure.microsoft.com/downloads/) downloaded and installed</span></span>
* <span data-ttu-id="a9073-113">İzleme etkin olması gerekiyorsa var olan bir akış analizi işi</span><span class="sxs-lookup"><span data-stu-id="a9073-113">An existing Stream Analytics job that needs to have monitoring enabled</span></span>

## <a name="create-a-project"></a><span data-ttu-id="a9073-114">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9073-114">Create a project</span></span>

1. <span data-ttu-id="a9073-115">Visual Studio C# .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a9073-115">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="a9073-116">Paket Yöneticisi Konsolu'nda NuGet paketlerini yüklemek için aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a9073-116">In the Package Manager Console, run the following commands to install the NuGet packages.</span></span> <span data-ttu-id="a9073-117">İlk Azure Stream Analytics yönetimi .NET SDK ' dir.</span><span class="sxs-lookup"><span data-stu-id="a9073-117">The first one is the Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="a9073-118">İzlemeyi etkinleştirmek için kullanılan Azure İzleyici SDK'sı ikinci adrestir.</span><span class="sxs-lookup"><span data-stu-id="a9073-118">The second one is the Azure Monitor SDK that will be used to enable monitoring.</span></span> <span data-ttu-id="a9073-119">Bir kimlik doğrulaması için kullanılacak Azure Active Directory istemcidir.</span><span class="sxs-lookup"><span data-stu-id="a9073-119">The last one is the Azure Active Directory client that will be used for authentication.</span></span>
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. <span data-ttu-id="a9073-120">Aşağıdaki appSettings bölümünü App.config dosyasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a9073-120">Add the following appSettings section to the App.config file.</span></span>
   
   ```
   <appSettings>
     <!--CSM Prod related values-->
     <add key="ResourceGroupName" value="RESOURCE GROUP NAME" />
     <add key="JobName" value="YOUR JOB NAME" />
     <add key="StorageAccountName" value="YOUR STORAGE ACCOUNT"/>
     <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
     <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
     <add key="WindowsManagementUri" value="https://management.core.windows.net/" />
     <add key="AsaClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
     <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
     <add key="SubscriptionId" value="YOUR AZURE SUBSCRIPTION ID" />
     <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
   </appSettings>
   ```
   <span data-ttu-id="a9073-121">İçin değerleri *Subscriptionıd* ve *ActiveDirectoryTenantId* Azure aboneliği ve Kiracı kimlikleri.</span><span class="sxs-lookup"><span data-stu-id="a9073-121">Replace values for *SubscriptionId* and *ActiveDirectoryTenantId* with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="a9073-122">Aşağıdaki PowerShell cmdlet'ini çalıştırarak bu değerleri alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a9073-122">You can get these values by running the following PowerShell cmdlet:</span></span>
   
   ```
   Get-AzureAccount
   ```
4. <span data-ttu-id="a9073-123">Aşağıdaki using deyimlerini projenin kaynak dosyasında (Program.cs).</span><span class="sxs-lookup"><span data-stu-id="a9073-123">Add the following using statements to the source file (Program.cs) in the project.</span></span>
   
   ```
     using System;
     using System.Configuration;
     using System.Threading;
     using Microsoft.Azure;
     using Microsoft.Azure.Management.Insights;
     using Microsoft.Azure.Management.Insights.Models;
     using Microsoft.Azure.Management.StreamAnalytics;
     using Microsoft.Azure.Management.StreamAnalytics.Models;
     using Microsoft.IdentityModel.Clients.ActiveDirectory;
   ```
5. <span data-ttu-id="a9073-124">Bir kimlik doğrulama yardımcı yöntemi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a9073-124">Add an authentication helper method.</span></span>
   
     <span data-ttu-id="a9073-125">ortak statik dizesi GetAuthorizationHeader()</span><span class="sxs-lookup"><span data-stu-id="a9073-125">public static string GetAuthorizationHeader()</span></span>
   
         {
             AuthenticationResult result = null;
             var thread = new Thread(() =>
             {
                 try
                 {
                     var context = new AuthenticationContext(
                         ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] +
                         ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
   
                     result = context.AcquireToken(
                         resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                         clientId: ConfigurationManager.AppSettings["AsaClientId"],
                         redirectUri: new Uri(ConfigurationManager.AppSettings["RedirectUri"]),
                         promptBehavior: PromptBehavior.Always);
                 }
                 catch (Exception threadEx)
                 {
                     Console.WriteLine(threadEx.Message);
                 }
             });
   
             thread.SetApartmentState(ApartmentState.STA);
             thread.Name = "AcquireTokenThread";
             thread.Start();
             thread.Join();
   
             if (result != null)
             {
                 return result.AccessToken;
             }
   
             throw new InvalidOperationException("Failed to acquire token");
     <span data-ttu-id="a9073-126">}</span><span class="sxs-lookup"><span data-stu-id="a9073-126">}</span></span>

## <a name="create-management-clients"></a><span data-ttu-id="a9073-127">Yönetim istemcileri oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9073-127">Create management clients</span></span>

<span data-ttu-id="a9073-128">Aşağıdaki kod, gerekli değişkenleri ve yönetim istemcilerin ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="a9073-128">The following code will set up the necessary variables and management clients.</span></span>

    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamAnalyticsJobName = "<YOUR STREAM ANALYTICS JOB NAME>";

    // Get authentication token
    TokenCloudCredentials aadTokenCredentials =
        new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader());

    Uri resourceManagerUri = new
    Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    // Create Stream Analytics and Insights management client
    StreamAnalyticsManagementClient streamAnalyticsClient = new
    StreamAnalyticsManagementClient(aadTokenCredentials, resourceManagerUri);
    InsightsManagementClient insightsClient = new
    InsightsManagementClient(aadTokenCredentials, resourceManagerUri);

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a><span data-ttu-id="a9073-129">Var olan bir akış analizi işi için izlemeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a9073-129">Enable monitoring for an existing Stream Analytics job</span></span>

<span data-ttu-id="a9073-130">Aşağıdaki kod için izlemeyi etkinleştirir bir **varolan** Stream Analytics işi.</span><span class="sxs-lookup"><span data-stu-id="a9073-130">The following code enables monitoring for an **existing** Stream Analytics job.</span></span> <span data-ttu-id="a9073-131">İlk kod parçası, belirli Stream Analytics işi hakkında bilgi almak için GET isteğini Stream Analytics Hizmeti'ne karşı gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="a9073-131">The first part of the code performs a GET request against the Stream Analytics service to retrieve information about the particular Stream Analytics job.</span></span> <span data-ttu-id="a9073-132">Kullandığı *kimliği* Put yöntemi PUT gönderir kod yarısı isteği Öngörüler hizmeti Stream Analytics işi için izlemeyi etkinleştirmek için ikinci bir parametre olarak özellik (GET isteği alındı).</span><span class="sxs-lookup"><span data-stu-id="a9073-132">It uses the *Id* property (retrieved from the GET request) as a parameter for the Put method in the second half of the code, which sends a PUT request to the Insights service to enable monitoring for the Stream Analytics job.</span></span>

>[!WARNING]
><span data-ttu-id="a9073-133">Daha önce farklı Stream Analytics işi, Azure Portalı aracılığıyla ya da program aracılığıyla yoluyla için izleme etkinleştirdiyseniz, kod, aşağıda **önceden izleme etkin olduğunda kullandığınız aynı depolama hesabı adı sağlamanızı öneririz.**</span><span class="sxs-lookup"><span data-stu-id="a9073-133">If you have previously enabled monitoring for a different Stream Analytics job, either through the Azure portal or programmatically via the below code, **we recommend that you provide the same storage account name that you used when you previously enabled monitoring.**</span></span>
> 
> <span data-ttu-id="a9073-134">Depolama hesabı bölgesine Stream Analytics işiniz oluşturduğunuz, iş için özel olarak bağlanır.</span><span class="sxs-lookup"><span data-stu-id="a9073-134">The storage account is linked to the region that you created your Stream Analytics job in, not specifically to the job itself.</span></span>
> 
> <span data-ttu-id="a9073-135">Tüm Stream Analytics işleri (ve tüm diğer Azure kaynakları) aynı bölgede paylaşmak izleme verilerini depolamak için bu depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="a9073-135">All Stream Analytics jobs (and all other Azure resources) in that same region share this storage account to store monitoring data.</span></span> <span data-ttu-id="a9073-136">Farklı bir depolama hesabı belirtirseniz, bu, bir akış analizi işleri veya diğer Azure kaynaklarına izlemede istenmeyen yan etkileri neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="a9073-136">If you provide a different storage account, it might cause unintended side effects in the monitoring of your other Stream Analytics jobs or other Azure resources.</span></span>
> 
> <span data-ttu-id="a9073-137">Değiştirmek için kullandığınız depolama hesabı adı `<YOUR STORAGE ACCOUNT NAME>` aşağıdaki kodda için izlemeyi etkinleştirme Stream Analytics işi ile aynı abonelikte olduğundan bir depolama hesabı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a9073-137">The storage account name that you use to replace `<YOUR STORAGE ACCOUNT NAME>` in the following code should be a storage account that is in the same subscription as the Stream Analytics job that you are enabling monitoring for.</span></span>
> 
> 

    // Get an existing Stream Analytics job
    JobGetParameters jobGetParameters = new JobGetParameters()
    {
        PropertiesToExpand = "inputs,transformation,outputs"
    };
    JobGetResponse jobGetResponse = streamAnalyticsClient.StreamingJobs.Get(resourceGroupName, streamAnalyticsJobName, jobGetParameters);

    // Enable monitoring
    ServiceDiagnosticSettingsPutParameters insightPutParameters = new ServiceDiagnosticSettingsPutParameters()
    {
            Properties = new ServiceDiagnosticSettings()
            {
                StorageAccountName = "<YOUR STORAGE ACCOUNT NAME>"
            }
    };
    insightsClient.ServiceDiagnosticSettingsOperations.Put(jobGetResponse.Job.Id, insightPutParameters);



## <a name="get-support"></a><span data-ttu-id="a9073-138">Destek alın</span><span class="sxs-lookup"><span data-stu-id="a9073-138">Get support</span></span>

<span data-ttu-id="a9073-139">Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="a9073-139">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9073-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a9073-140">Next steps</span></span>

* [<span data-ttu-id="a9073-141">Azure Stream Analytics'e giriş</span><span class="sxs-lookup"><span data-stu-id="a9073-141">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="a9073-142">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a9073-142">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="a9073-143">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="a9073-143">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="a9073-144">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="a9073-144">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="a9073-145">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="a9073-145">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

