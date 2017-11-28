---
title: "Stream Analytics aaaProgrammatically İzleyici işleri | Microsoft Docs"
description: "Nasıl tooprogrammatically izlemek REST API'leri, Azure SDK'sı veya PowerShell oluşturulan akış analizi işleri öğrenin."
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
ms.openlocfilehash: 44a9c29c2161ee81ea76ece4646a8691bf5d5b48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a><span data-ttu-id="f9675-104">Program aracılığıyla bir akış analizi işi İzleyicisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9675-104">Programmatically create a Stream Analytics job monitor</span></span>

<span data-ttu-id="f9675-105">Bu makalede gösterilir nasıl tooenable Stream Analytics işi için izleme.</span><span class="sxs-lookup"><span data-stu-id="f9675-105">This article demonstrates how tooenable monitoring for a Stream Analytics job.</span></span> <span data-ttu-id="f9675-106">REST API'leri, Azure SDK'sı veya PowerShell oluşturulan stream Analytics işlerini izleme varsayılan olarak etkin gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f9675-106">Stream Analytics jobs that are created via REST APIs, Azure SDK, or PowerShell do not have monitoring enabled by default.</span></span> <span data-ttu-id="f9675-107">El ile hello Azure portal toohello işin izleme sayfası giderek etkinleştirebilirsiniz ve hello tıklatarak düğmesini etkinleştirin veya bu makalede hello adımları izleyerek bu işlemi otomatikleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9675-107">You can manually enable it in hello Azure portal by going toohello job’s Monitor page and clicking hello Enable button or you can automate this process by following hello steps in this article.</span></span> <span data-ttu-id="f9675-108">izleme verilerini hello hello Stream Analytics işiniz için Azure portalı hello ölçümleri bölümünde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="f9675-108">hello monitoring data will show up in hello Metrics area of hello Azure portal for your Stream Analytics job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9675-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f9675-109">Prerequisites</span></span>

<span data-ttu-id="f9675-110">Bu işlem başlamadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f9675-110">Before you begin this process, you must have hello following:</span></span>

* <span data-ttu-id="f9675-111">Visual Studio 2017 veya 2015</span><span class="sxs-lookup"><span data-stu-id="f9675-111">Visual Studio 2017 or 2015</span></span>
* <span data-ttu-id="f9675-112">[Azure .NET SDK'sı](https://azure.microsoft.com/downloads/) indirilir ve yüklenir</span><span class="sxs-lookup"><span data-stu-id="f9675-112">[Azure .NET SDK](https://azure.microsoft.com/downloads/) downloaded and installed</span></span>
* <span data-ttu-id="f9675-113">Toohave izleme etkin gereken var olan bir akış analizi işi</span><span class="sxs-lookup"><span data-stu-id="f9675-113">An existing Stream Analytics job that needs toohave monitoring enabled</span></span>

## <a name="create-a-project"></a><span data-ttu-id="f9675-114">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9675-114">Create a project</span></span>

1. <span data-ttu-id="f9675-115">Visual Studio C# .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f9675-115">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="f9675-116">Hello Paket Yöneticisi konsolu, tooinstall hello NuGet paketlerini çalışma hello aşağıdaki komutları.</span><span class="sxs-lookup"><span data-stu-id="f9675-116">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="f9675-117">Merhaba ilk hello Azure Stream Analytics yönetimi .NET SDK'sı biridir.</span><span class="sxs-lookup"><span data-stu-id="f9675-117">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="f9675-118">Merhaba ikinci kullanılacak Azure İzleyici SDK hello olandır tooenable izleme.</span><span class="sxs-lookup"><span data-stu-id="f9675-118">hello second one is hello Azure Monitor SDK that will be used tooenable monitoring.</span></span> <span data-ttu-id="f9675-119">Merhaba son hello Azure Active Directory kimlik doğrulaması için kullanılacak bir istemci biridir.</span><span class="sxs-lookup"><span data-stu-id="f9675-119">hello last one is hello Azure Active Directory client that will be used for authentication.</span></span>
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. <span data-ttu-id="f9675-120">Merhaba aşağıdaki appSettings bölümünde toohello App.config dosyasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f9675-120">Add hello following appSettings section toohello App.config file.</span></span>
   
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
   <span data-ttu-id="f9675-121">İçin değerleri *Subscriptionıd* ve *ActiveDirectoryTenantId* Azure aboneliği ve Kiracı kimlikleri.</span><span class="sxs-lookup"><span data-stu-id="f9675-121">Replace values for *SubscriptionId* and *ActiveDirectoryTenantId* with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="f9675-122">Merhaba aşağıdaki PowerShell cmdlet'ini çalıştırarak bu değerleri alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f9675-122">You can get these values by running hello following PowerShell cmdlet:</span></span>
   
   ```
   Get-AzureAccount
   ```
4. <span data-ttu-id="f9675-123">Merhaba aşağıdakileri ekleyin hello projesindeki deyimleri toohello kaynak dosyasını (Program.cs) kullanarak.</span><span class="sxs-lookup"><span data-stu-id="f9675-123">Add hello following using statements toohello source file (Program.cs) in hello project.</span></span>
   
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
5. <span data-ttu-id="f9675-124">Bir kimlik doğrulama yardımcı yöntemi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f9675-124">Add an authentication helper method.</span></span>
   
     <span data-ttu-id="f9675-125">ortak statik dizesi GetAuthorizationHeader()</span><span class="sxs-lookup"><span data-stu-id="f9675-125">public static string GetAuthorizationHeader()</span></span>
   
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
   
             throw new InvalidOperationException("Failed tooacquire token");
     <span data-ttu-id="f9675-126">}</span><span class="sxs-lookup"><span data-stu-id="f9675-126">}</span></span>

## <a name="create-management-clients"></a><span data-ttu-id="f9675-127">Yönetim istemcileri oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9675-127">Create management clients</span></span>

<span data-ttu-id="f9675-128">Merhaba aşağıdaki kodu hello gerekli değişkenleri ve yönetim istemcilerin ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f9675-128">hello following code will set up hello necessary variables and management clients.</span></span>

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

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a><span data-ttu-id="f9675-129">Var olan bir akış analizi işi için izlemeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f9675-129">Enable monitoring for an existing Stream Analytics job</span></span>

<span data-ttu-id="f9675-130">Merhaba aşağıdaki kod için izlemeyi etkinleştirir bir **varolan** Stream Analytics işi.</span><span class="sxs-lookup"><span data-stu-id="f9675-130">hello following code enables monitoring for an **existing** Stream Analytics job.</span></span> <span data-ttu-id="f9675-131">Merhaba ilk bölümü hello kod hello Stream Analytics hizmeti tooretrieve hello belirli Stream Analytics işi bilgilerini bir GET isteği gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="f9675-131">hello first part of hello code performs a GET request against hello Stream Analytics service tooretrieve information about hello particular Stream Analytics job.</span></span> <span data-ttu-id="f9675-132">Merhaba kullanan *kimliği* (Merhaba GET isteğini alındı) özelliği hello hello Put yöntemi için bir parametre olarak toohello Öngörüler bir PUT İsteği gönderir hello kodu ikinci yarısında hizmet tooenable Merhaba Stream Analytics izleme İş.</span><span class="sxs-lookup"><span data-stu-id="f9675-132">It uses hello *Id* property (retrieved from hello GET request) as a parameter for hello Put method in hello second half of hello code, which sends a PUT request toohello Insights service tooenable monitoring for hello Stream Analytics job.</span></span>

>[!WARNING]
><span data-ttu-id="f9675-133">Daha önce farklı Stream Analytics işi, hello Azure portal aracılığıyla ya da program aracılığıyla yoluyla kod, aşağıda hello için izleme etkinleştirdiyseniz, **hello sağlamanızı öneririz ne zaman kullanılan aynı depolama hesabı adı, daha önce izleme etkin.**</span><span class="sxs-lookup"><span data-stu-id="f9675-133">If you have previously enabled monitoring for a different Stream Analytics job, either through hello Azure portal or programmatically via hello below code, **we recommend that you provide hello same storage account name that you used when you previously enabled monitoring.**</span></span>
> 
> <span data-ttu-id="f9675-134">Merhaba depolama hesabı, özellikle toohello işinde, kendisini Stream Analytics işiniz oluşturulan bağlantılı toohello bölgedir.</span><span class="sxs-lookup"><span data-stu-id="f9675-134">hello storage account is linked toohello region that you created your Stream Analytics job in, not specifically toohello job itself.</span></span>
> 
> <span data-ttu-id="f9675-135">Tüm Stream Analytics aynı bölgede işleri (ve tüm diğer Azure kaynakları) izleme verileri bu depolama hesabı toostore paylaşın.</span><span class="sxs-lookup"><span data-stu-id="f9675-135">All Stream Analytics jobs (and all other Azure resources) in that same region share this storage account toostore monitoring data.</span></span> <span data-ttu-id="f9675-136">Farklı bir depolama hesabı belirtirseniz, bu, bir akış analizi işleri veya diğer Azure kaynaklarına hello izlemede istenmeyen yan etkileri neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="f9675-136">If you provide a different storage account, it might cause unintended side effects in hello monitoring of your other Stream Analytics jobs or other Azure resources.</span></span>
> 
> <span data-ttu-id="f9675-137">hello depolama hesabı adı tooreplace kullandığınız `<YOUR STORAGE ACCOUNT NAME>` koddan hello hello olan bir depolama hesabını olmalıdır için izlemeyi etkinleştirme hello Stream Analytics işi aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="f9675-137">hello storage account name that you use tooreplace `<YOUR STORAGE ACCOUNT NAME>` in hello following code should be a storage account that is in hello same subscription as hello Stream Analytics job that you are enabling monitoring for.</span></span>
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



## <a name="get-support"></a><span data-ttu-id="f9675-138">Destek alın</span><span class="sxs-lookup"><span data-stu-id="f9675-138">Get support</span></span>

<span data-ttu-id="f9675-139">Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="f9675-139">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9675-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f9675-140">Next steps</span></span>

* [<span data-ttu-id="f9675-141">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="f9675-141">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f9675-142">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="f9675-142">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f9675-143">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="f9675-143">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f9675-144">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="f9675-144">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f9675-145">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="f9675-145">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

