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
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a>Program aracılığıyla bir akış analizi işi İzleyicisi oluşturma

Bu makalede gösterilir nasıl tooenable Stream Analytics işi için izleme. REST API'leri, Azure SDK'sı veya PowerShell oluşturulan stream Analytics işlerini izleme varsayılan olarak etkin gerekmez. El ile hello Azure portal toohello işin izleme sayfası giderek etkinleştirebilirsiniz ve hello tıklatarak düğmesini etkinleştirin veya bu makalede hello adımları izleyerek bu işlemi otomatikleştirebilirsiniz. izleme verilerini hello hello Stream Analytics işiniz için Azure portalı hello ölçümleri bölümünde gösterilir.

## <a name="prerequisites"></a>Ön koşullar

Bu işlem başlamadan önce hello şunlara sahip olmanız gerekir:

* Visual Studio 2017 veya 2015
* [Azure .NET SDK'sı](https://azure.microsoft.com/downloads/) indirilir ve yüklenir
* Toohave izleme etkin gereken var olan bir akış analizi işi

## <a name="create-a-project"></a>Proje oluşturma

1. Visual Studio C# .NET konsol uygulaması oluşturun.
2. Hello Paket Yöneticisi konsolu, tooinstall hello NuGet paketlerini çalışma hello aşağıdaki komutları. Merhaba ilk hello Azure Stream Analytics yönetimi .NET SDK'sı biridir. Merhaba ikinci kullanılacak Azure İzleyici SDK hello olandır tooenable izleme. Merhaba son hello Azure Active Directory kimlik doğrulaması için kullanılacak bir istemci biridir.
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. Merhaba aşağıdaki appSettings bölümünde toohello App.config dosyasına ekleyin.
   
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
   İçin değerleri *Subscriptionıd* ve *ActiveDirectoryTenantId* Azure aboneliği ve Kiracı kimlikleri. Merhaba aşağıdaki PowerShell cmdlet'ini çalıştırarak bu değerleri alabilirsiniz:
   
   ```
   Get-AzureAccount
   ```
4. Merhaba aşağıdakileri ekleyin hello projesindeki deyimleri toohello kaynak dosyasını (Program.cs) kullanarak.
   
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
5. Bir kimlik doğrulama yardımcı yöntemi ekleyin.
   
     ortak statik dizesi GetAuthorizationHeader()
   
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
     }

## <a name="create-management-clients"></a>Yönetim istemcileri oluşturma

Merhaba aşağıdaki kodu hello gerekli değişkenleri ve yönetim istemcilerin ayarlar.

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

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a>Var olan bir akış analizi işi için izlemeyi etkinleştir

Merhaba aşağıdaki kod için izlemeyi etkinleştirir bir **varolan** Stream Analytics işi. Merhaba ilk bölümü hello kod hello Stream Analytics hizmeti tooretrieve hello belirli Stream Analytics işi bilgilerini bir GET isteği gerçekleştirir. Merhaba kullanan *kimliği* (Merhaba GET isteğini alındı) özelliği hello hello Put yöntemi için bir parametre olarak toohello Öngörüler bir PUT İsteği gönderir hello kodu ikinci yarısında hizmet tooenable Merhaba Stream Analytics izleme İş.

>[!WARNING]
>Daha önce farklı Stream Analytics işi, hello Azure portal aracılığıyla ya da program aracılığıyla yoluyla kod, aşağıda hello için izleme etkinleştirdiyseniz, **hello sağlamanızı öneririz ne zaman kullanılan aynı depolama hesabı adı, daha önce izleme etkin.**
> 
> Merhaba depolama hesabı, özellikle toohello işinde, kendisini Stream Analytics işiniz oluşturulan bağlantılı toohello bölgedir.
> 
> Tüm Stream Analytics aynı bölgede işleri (ve tüm diğer Azure kaynakları) izleme verileri bu depolama hesabı toostore paylaşın. Farklı bir depolama hesabı belirtirseniz, bu, bir akış analizi işleri veya diğer Azure kaynaklarına hello izlemede istenmeyen yan etkileri neden olabilir.
> 
> hello depolama hesabı adı tooreplace kullandığınız `<YOUR STORAGE ACCOUNT NAME>` koddan hello hello olan bir depolama hesabını olmalıdır için izlemeyi etkinleştirme hello Stream Analytics işi aynı abonelik.
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



## <a name="get-support"></a>Destek alın

Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Sonraki adımlar

* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)

