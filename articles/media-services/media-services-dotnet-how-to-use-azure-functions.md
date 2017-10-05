---
title: "Azure işlevleri Media Services ile geliştirme"
description: "Bu konu Azure işlevleri Media Services ile geliştirmeye başlamak Azure portalını kullanarak gösterilmiştir."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 51bdcb01-1846-4e1f-bd90-70020ab471b0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/21/2017
ms.author: juliako
ms.openlocfilehash: 35d539855572fef6c00de614a4e57738a8abd075
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
#<a name="develop-azure-functions-with-media-services"></a><span data-ttu-id="e6f87-103">Azure işlevleri Media Services ile geliştirme</span><span class="sxs-lookup"><span data-stu-id="e6f87-103">Develop Azure Functions with Media Services</span></span>

<span data-ttu-id="e6f87-104">Bu konu, Media Services'i kullanma Azure işlevleri oluşturmaya başlamak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e6f87-104">This topic shows you how to get started with creating Azure Functions that use Media Services.</span></span> <span data-ttu-id="e6f87-105">Bu konu başlığı altında tanımlanan Azure işlevi adlı bir depolama hesabı kapsayıcısının izler **giriş** yeni MP4 dosyaları için.</span><span class="sxs-lookup"><span data-stu-id="e6f87-105">The Azure Function defined in this topic monitors a storage account container named **input** for new MP4 files.</span></span> <span data-ttu-id="e6f87-106">Bir dosya depolama kapsayıcıya bırakılan sonra blob tetikleyici işlevi yürütülür.</span><span class="sxs-lookup"><span data-stu-id="e6f87-106">Once a file is dropped into the storage container, the blob trigger will execute the function.</span></span>

<span data-ttu-id="e6f87-107">Keşfetmek ve Azure Media Services'i kullanma mevcut Azure işlevleri dağıtmak istiyorsanız, kullanıma [medya Hizmetleri Azure işlevleri](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="e6f87-107">If you want to explore and deploy existing Azure Functions that use Azure Media Services, check out [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span> <span data-ttu-id="e6f87-108">Bu depo alma için ilgili iş akışları doğrudan blob depolama alanından blob depolama alanına kodlama ve içeriği yazma geri içeriğini göstermek için Media Services'i kullanma örnekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="e6f87-108">This repository contains examples that use Media Services to show workflows related to ingesting content directly from blob storage, encoding, and writing content back to blob storage.</span></span> <span data-ttu-id="e6f87-109">Ayrıca Web kancaları ve Azure kuyrukları aracılığıyla iş bildirimleri izleme örnekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="e6f87-109">It also includes examples of how to monitor job notifications via WebHooks and Azure Queues.</span></span> <span data-ttu-id="e6f87-110">İşlevlerinizi örneklerde göre de geliştirebilirsiniz [medya Hizmetleri Azure işlevleri](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) deposu.</span><span class="sxs-lookup"><span data-stu-id="e6f87-110">You can also develop your Functions based on the examples in the [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repository.</span></span> <span data-ttu-id="e6f87-111">İşlevler dağıtmak için basın **Azure'a Dağıt** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e6f87-111">To deploy the functions, press the **Deploy to Azure** button.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6f87-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e6f87-112">Prerequisites</span></span>

- <span data-ttu-id="e6f87-113">İlk işlevinizin oluşturmadan önce etkin bir Azure hesabınız olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6f87-113">Before you can create your first function, you need to have an active Azure account.</span></span> <span data-ttu-id="e6f87-114">Bir Azure hesabınız yoksa [ücretsiz hesaplar kullanılabilir](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="e6f87-114">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="e6f87-115">Azure Media Services (AMS) hesabınızdaki eylemleri gerçekleştirmek veya Media Services tarafından gönderilen olayları dinleme Azure işlevleri oluşturmak için kullanacaksanız, açıklandığı gibi bir AMS hesabının oluşturmalısınız [burada](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="e6f87-115">If you are going to create Azure Functions that perform actions on your Azure Media Services (AMS) account or listen to events sent by Media Services, you should create an AMS account, as described [here](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="e6f87-116">Anlayış [Azure işlevlerinin nasıl kullanılacağı](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e6f87-116">Understanding of [how to use Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="e6f87-117">Ayrıca, gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="e6f87-117">Also, review:</span></span>
    - [<span data-ttu-id="e6f87-118">Azure işlevleri HTTP ve Web kancası bağlamaları</span><span class="sxs-lookup"><span data-stu-id="e6f87-118">Azure functions HTTP and webhook bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
    - [<span data-ttu-id="e6f87-119">Azure işlevi uygulama ayarlarının nasıl yapılandırılacağı</span><span class="sxs-lookup"><span data-stu-id="e6f87-119">How to configure Azure Function app settings</span></span>](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a><span data-ttu-id="e6f87-120">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="e6f87-120">Considerations</span></span>

-  <span data-ttu-id="e6f87-121">Tüketim plan altında çalışan azure işlevlerinin 5 dakika zaman aşımı sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="e6f87-121">Azure Functions running under the Consumption plan have 5 minutes timeout limit.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="e6f87-122">İşlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6f87-122">Create a function app</span></span>

1. <span data-ttu-id="e6f87-123">[Azure portalına](http://portal.azure.com) gidip Azure hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e6f87-123">Go to the [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="e6f87-124">Açıklandığı gibi işlev uygulaması oluşturma [burada](../azure-functions/functions-create-function-app-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e6f87-124">Create a function app as described [here](../azure-functions/functions-create-function-app-portal.md).</span></span>

>[!NOTE]
> <span data-ttu-id="e6f87-125">Belirttiğiniz bir depolama hesabı **StorageConnection** ortam değişkeni, uygulamanız ile aynı bölgede olmalıdır (sonraki adıma bakın).</span><span class="sxs-lookup"><span data-stu-id="e6f87-125">A storage account that you specify in the **StorageConnection** environment variable (see the next step) should be in the same region as your app.</span></span>

## <a name="configure-function-app-settings"></a><span data-ttu-id="e6f87-126">İşlev uygulaması ayarlarını yapılandır</span><span class="sxs-lookup"><span data-stu-id="e6f87-126">Configure function app settings</span></span>

<span data-ttu-id="e6f87-127">Media Services işlevleri geliştirirken işlevlerinizi kullanılan ortam değişkenleri eklemek için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="e6f87-127">When developing Media Services functions, it is handy to add environment variables that will be used throughout your functions.</span></span> <span data-ttu-id="e6f87-128">Uygulama ayarlarını yapılandırmak için uygulama ayarlarını yapılandır bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e6f87-128">To configure app settings, click the Configure App Settings link.</span></span> <span data-ttu-id="e6f87-129">Daha fazla bilgi için bkz: [Azure işlevi uygulama ayarlarının nasıl yapılandırılacağı](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span><span class="sxs-lookup"><span data-stu-id="e6f87-129">For more information, see  [How to configure Azure Function app settings](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span></span> 

<span data-ttu-id="e6f87-130">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="e6f87-130">For example:</span></span>

![Ayarlar](./media/media-services-azure-functions/media-services-azure-functions001.png)

<span data-ttu-id="e6f87-132">Bu makalede, tanımlanmış işlevi, aşağıdaki ortam değişkenleri, uygulama ayarlarınızı olduğu varsayılır:</span><span class="sxs-lookup"><span data-stu-id="e6f87-132">The function, defined in this article, assumes you have the following environment variables in your app settings:</span></span>

<span data-ttu-id="e6f87-133">**AMSAccount** : *AMS hesabının adını* (örneğin testams)</span><span class="sxs-lookup"><span data-stu-id="e6f87-133">**AMSAccount** : *AMS account name* (e.g. testams)</span></span>

<span data-ttu-id="e6f87-134">**AMSKey** : *AMS hesap anahtarı* (örneğin IHOySnH + XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM =)</span><span class="sxs-lookup"><span data-stu-id="e6f87-134">**AMSKey** : *AMS account key* (e.g. IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span></span>

<span data-ttu-id="e6f87-135">**MediaServicesStorageAccountName** : *depolama hesabı adı* (örn., testamsstorage)</span><span class="sxs-lookup"><span data-stu-id="e6f87-135">**MediaServicesStorageAccountName** : *storage account name* (e.g., testamsstorage)</span></span>

<span data-ttu-id="e6f87-136">**MediaServicesStorageAccountKey** : *depolama hesabı anahtarı* (örn., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX ==)</span><span class="sxs-lookup"><span data-stu-id="e6f87-136">**MediaServicesStorageAccountKey** : *storage account key* (e.g., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span></span>

<span data-ttu-id="e6f87-137">**StorageConnection** : *depolama bağlantısı* (örn., DefaultEndpointsProtocol = https; AccountName = testamsstorage; AccountKey xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX = ==)</span><span class="sxs-lookup"><span data-stu-id="e6f87-137">**StorageConnection** : *storage connection* (e.g., DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span></span>

## <a name="create-a-function"></a><span data-ttu-id="e6f87-138">İşlev oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6f87-138">Create a function</span></span>

<span data-ttu-id="e6f87-139">İşlev Uygulamanız dağıtıldıktan sonra onu arasında bulabilirsiniz **uygulama hizmetleri** Azure işlevleri.</span><span class="sxs-lookup"><span data-stu-id="e6f87-139">Once your function app is deployed, you can find it among **App Services** Azure Functions.</span></span>

1. <span data-ttu-id="e6f87-140">İşlev uygulamanızı seçin ve'ı tıklatın **yeni işlev**.</span><span class="sxs-lookup"><span data-stu-id="e6f87-140">Select your function app and click **New Function**.</span></span>
2. <span data-ttu-id="e6f87-141">Seçin **C#** dil ve **veri işleme** senaryo.</span><span class="sxs-lookup"><span data-stu-id="e6f87-141">Choose the **C#** language and **Data Processing** scenario.</span></span>
3. <span data-ttu-id="e6f87-142">Seçin **BlobTrigger** şablonu.</span><span class="sxs-lookup"><span data-stu-id="e6f87-142">Choose **BlobTrigger** template.</span></span> <span data-ttu-id="e6f87-143">Bir blob hizmetine yüklendikten olduğunda bu işlev tetiklenen **giriş** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="e6f87-143">This function will be triggered whenever a blob is uploaded into the **input** container.</span></span> <span data-ttu-id="e6f87-144">**Giriş** adı belirtilen **yolu**, sonraki adımda.</span><span class="sxs-lookup"><span data-stu-id="e6f87-144">The **input** name is specified in the **Path**, in the next step.</span></span>

    ![Dosyaları](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. <span data-ttu-id="e6f87-146">Seçtiğinizde, bundan sonra **BlobTrigger**, daha fazla bazı denetimler sayfasında görünür.</span><span class="sxs-lookup"><span data-stu-id="e6f87-146">Once you select **BlobTrigger**, some more controls will appear on the page.</span></span>

    ![Dosyaları](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. <span data-ttu-id="e6f87-148">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e6f87-148">Click **Create**.</span></span> 


## <a name="files"></a><span data-ttu-id="e6f87-149">Dosyalar</span><span class="sxs-lookup"><span data-stu-id="e6f87-149">Files</span></span>

<span data-ttu-id="e6f87-150">Azure işlevinizi ve bu bölümde açıklanan diğer dosyaları kod dosyaları ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="e6f87-150">Your Azure function is associated with code files and other files that are described in this section.</span></span> <span data-ttu-id="e6f87-151">Varsayılan olarak, bir işlev ilişkili olduğu **function.json** ve **run.csx** (C#) dosyaları.</span><span class="sxs-lookup"><span data-stu-id="e6f87-151">By default, a function is associated with **function.json** and **run.csx** (C#) files.</span></span> <span data-ttu-id="e6f87-152">Eklemeniz gerekir bir **project.json** dosya.</span><span class="sxs-lookup"><span data-stu-id="e6f87-152">You will need to add a **project.json** file.</span></span> <span data-ttu-id="e6f87-153">Bu bölümün geri kalanında bu dosyaları tanımlarında gösterir.</span><span class="sxs-lookup"><span data-stu-id="e6f87-153">The rest of this section shows the definitions for these files.</span></span>

![Dosyaları](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a><span data-ttu-id="e6f87-155">Function.JSON</span><span class="sxs-lookup"><span data-stu-id="e6f87-155">function.json</span></span>

<span data-ttu-id="e6f87-156">Function.json dosyası, işlev bağlamaları ve diğer yapılandırma ayarlarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e6f87-156">The function.json file defines the function bindings and other configuration settings.</span></span> <span data-ttu-id="e6f87-157">Çalışma zamanı izlenecek olaylar belirlemek için bu dosyaya ve verilerini geçirin ve işlev yürütülmesini veri dönmek nasıl kullanır.</span><span class="sxs-lookup"><span data-stu-id="e6f87-157">The runtime uses this file to determine the events to monitor and how to pass data into and return data from function execution.</span></span> <span data-ttu-id="e6f87-158">Daha fazla bilgi için bkz: [Azure işlevleri HTTP ve Web kancası bağlamaları](../azure-functions/functions-reference.md#function-code).</span><span class="sxs-lookup"><span data-stu-id="e6f87-158">For more information, see [Azure functions HTTP and webhook bindings](../azure-functions/functions-reference.md#function-code).</span></span>

>[!NOTE]
><span data-ttu-id="e6f87-159">Ayarlama **devre dışı** özelliğine **true** işlevi çalıştırılmasını engellemek için.</span><span class="sxs-lookup"><span data-stu-id="e6f87-159">Set the **disabled** property to **true** to prevent the function from being executed.</span></span> 


<span data-ttu-id="e6f87-160">Bir örneği burada verilmiştir **function.json** dosya.</span><span class="sxs-lookup"><span data-stu-id="e6f87-160">Here is an example of **function.json** file.</span></span>

    {
    "bindings": [
      {
        "name": "myBlob",
        "type": "blobTrigger",
        "direction": "in",
        "path": "input/{fileName}.mp4",
        "connection": "StorageConnection"
      }
    ],
    "disabled": false
    }

### <a name="projectjson"></a><span data-ttu-id="e6f87-161">Project.JSON</span><span class="sxs-lookup"><span data-stu-id="e6f87-161">project.json</span></span>

<span data-ttu-id="e6f87-162">Project.json dosyası bağımlılıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="e6f87-162">The project.json file contains dependencies.</span></span> <span data-ttu-id="e6f87-163">Bir örneği burada verilmiştir **project.json** Nuget gerekli .NET Azure Media Services'i paketlerinden içeren dosya.</span><span class="sxs-lookup"><span data-stu-id="e6f87-163">Here is an example of **project.json** file that includes the required .NET Azure Media Services packages from Nuget.</span></span> <span data-ttu-id="e6f87-164">Sürüm numaraları, en son sürümleri onaylamanız böylece paketler için en son güncelleştirmeleri ile değişir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e6f87-164">Note that the version numbers will change with latest updates to the packages, so you should confirm the most recent versions.</span></span> 

    {
      "frameworks": {
        "net46":{
          "dependencies": {
        "windowsazure.mediaservices": "3.8.0.5",
        "windowsazure.mediaservices.extensions": "3.8.0.3"
          }
        }
       }
    }
    
### <a name="runcsx"></a><span data-ttu-id="e6f87-165">Run.csx</span><span class="sxs-lookup"><span data-stu-id="e6f87-165">run.csx</span></span>

<span data-ttu-id="e6f87-166">C# kodunu işlevinizi budur.</span><span class="sxs-lookup"><span data-stu-id="e6f87-166">This is the C# code for your function.</span></span>  <span data-ttu-id="e6f87-167">İşlevi izleyiciler adlı bir depolama hesabı kapsayıcısının tanımlanan **giriş** (ne yolu belirtildi olan) yeni MP4 dosyaları için.</span><span class="sxs-lookup"><span data-stu-id="e6f87-167">The function defined below monitors a storage account container named **input** (that is what was specified in the path) for new MP4 files.</span></span> <span data-ttu-id="e6f87-168">Bir dosya depolama kapsayıcıya bırakılan sonra blob tetikleyici işlevi yürütülür.</span><span class="sxs-lookup"><span data-stu-id="e6f87-168">Once a file is dropped into the storage container, the blob trigger will execute the function.</span></span>
    
<span data-ttu-id="e6f87-169">Bu bölümde tanımlanan örnek gösterir</span><span class="sxs-lookup"><span data-stu-id="e6f87-169">The example defined in this section demonstrates</span></span> 

1. <span data-ttu-id="e6f87-170">bir Media Services hesabına (blob bir AMS varlığa kopyalamayı tarafından) varlık alma konusunda ve</span><span class="sxs-lookup"><span data-stu-id="e6f87-170">how to ingest an asset into a Media Services account (by coping a blob into an AMS asset) and</span></span> 
2. <span data-ttu-id="e6f87-171">bir kodlama işi göndermek için Medya Kodlayıcısı standart 's kullanan nasıl "Uyarlamalı akış" hazır.</span><span class="sxs-lookup"><span data-stu-id="e6f87-171">how to submit an encoding job that uses Media Encoder Standard's "Adaptive Streaming" preset .</span></span>

<span data-ttu-id="e6f87-172">Gerçek Hayatta senaryosunda, büyük olasılıkla iş ilerleme durumunu izlemek ve kodlanmış Varlığınızı yayımlamak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="e6f87-172">In the real life scenario, you most likely want to track job progress and then publish your encoded asset.</span></span> <span data-ttu-id="e6f87-173">Daha fazla bilgi için bkz: [kullanım Azure Media Services iş bildirimleri izlemek için Web kancası](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="e6f87-173">For more information, see [Use Azure WebHooks to monitor Media Services job notifications](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> <span data-ttu-id="e6f87-174">Daha fazla örnek için bkz: [medya Hizmetleri Azure işlevleri](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="e6f87-174">For more examples, see [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>  

<span data-ttu-id="e6f87-175">Tamamladıktan sonra işlevinizi tanımlama tıklatın **kaydedip çalıştırın**.</span><span class="sxs-lookup"><span data-stu-id="e6f87-175">Once you are done defining your function click **Save and Run**.</span></span>

    #r "Microsoft.WindowsAzure.Storage"
    #r "Newtonsoft.Json"
    #r "System.Web"

    using System;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Net;
    using System.Threading;
    using System.Threading.Tasks;
    using System.IO;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Auth;

    private static readonly string _mediaServicesAccountName = Environment.GetEnvironmentVariable("AMSAccount");
    private static readonly string _mediaServicesAccountKey = Environment.GetEnvironmentVariable("AMSKey");

    static string _storageAccountName = Environment.GetEnvironmentVariable("MediaServicesStorageAccountName");
    static string _storageAccountKey = Environment.GetEnvironmentVariable("MediaServicesStorageAccountKey");

    private static CloudStorageAccount _destinationStorageAccount = null;

    // Field for service context.
    private static CloudMediaContext _context = null;
    private static MediaServicesCredentials _cachedCredentials = null;

    public static void Run(CloudBlockBlob myBlob, string fileName, TraceWriter log)
    {
        // NOTE that the variables {fileName} here come from the path setting in function.json
        // and are passed into the  Run method signature above. We can use this to make decisions on what type of file
        // was dropped into the input container for the function. 

        // No need to do any Retry strategy in this function, By default, the SDK calls a function up to 5 times for a 
        // given blob. If the fifth try fails, the SDK adds a message to a queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used the chached credentials to create CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy the Blob into a new Input Asset for the Job
        // ***NOTE: Ideally we would have a method to ingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with the Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass to it the name of the 
        // processor to use for the specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with the encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify the input asset to be encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset to contain the results of the job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means the output asset is not encrypted. 
        task.OutputAssets.AddNew(fileName, AssetCreationOptions.None);

        job.Submit();
        log.Info("Job Submitted");

        }
        catch (Exception ex)
        {
        log.Error("ERROR: failed.");
        log.Info($"StackTrace : {ex.StackTrace}");
        throw ex;
        }
    }

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


    public static async Task<IAsset> CreateAssetFromBlob(CloudBlockBlob blob, string assetName, TraceWriter log){
        IAsset newAsset = null;

        try{
            Task<IAsset> copyAssetTask = CreateAssetFromBlobAsync(blob, assetName, log);
            newAsset = await copyAssetTask;
            log.Info($"Asset Copied : {newAsset.Id}");
        }
        catch(Exception ex){
            log.Info("Copy Failed");
            log.Info($"ERROR : {ex.Message}");
            throw ex;
        }

        return newAsset;
    }

    /// <summary>
    /// Creates a new asset and copies blobs from the specifed storage account.
    /// </summary>
    /// <param name="blob">The specified blob.</param>
    /// <returns>The new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference to the storage account that is associated with the Media Services account. 
        StorageCredentials mediaServicesStorageCredentials =
        new StorageCredentials(_storageAccountName, _storageAccountKey);
        _destinationStorageAccount = new CloudStorageAccount(mediaServicesStorageCredentials, false);

        // Create a new asset. 
        var asset = _context.Assets.Create(blob.Name, AssetCreationOptions.None);
        log.Info($"Created new asset {asset.Name}");

        IAccessPolicy writePolicy = _context.AccessPolicies.Create("writePolicy",
        TimeSpan.FromHours(4), AccessPermissions.Write);
        ILocator destinationLocator = _context.Locators.CreateLocator(LocatorType.Sas, asset, writePolicy);
        CloudBlobClient destBlobStorage = _destinationStorageAccount.CreateCloudBlobClient();

        // Get the destination asset container reference
        string destinationContainerName = (new Uri(destinationLocator.Path)).Segments[1];
        CloudBlobContainer assetContainer = destBlobStorage.GetContainerReference(destinationContainerName);

        try{
        assetContainer.CreateIfNotExists();
        }
        catch (Exception ex)
        {
        log.Error ("ERROR:" + ex.Message);
        }

        log.Info("Created asset.");

        // Get hold of the destination blob
        CloudBlockBlob destinationBlob = assetContainer.GetBlockBlobReference(blob.Name);

        // Copy Blob
        try
        {
        using (var stream = await blob.OpenReadAsync()) 
        {            
            await destinationBlob.UploadFromStreamAsync(stream);          
        }

        log.Info("Copy Complete.");

        var assetFile = asset.AssetFiles.Create(blob.Name);
        assetFile.ContentFileSize = blob.Properties.Length;
        assetFile.IsPrimary = true;
        assetFile.Update();
        asset.Update();
        }
        catch (Exception ex)
        {
        log.Error(ex.Message);
        log.Info (ex.StackTrace);
        log.Info ("Copy Failed.");
        throw;
        }

        destinationLocator.Delete();
        writePolicy.Delete();

        return asset;
    }
##<a name="test-your-function"></a><span data-ttu-id="e6f87-176">İşlevinizi test</span><span class="sxs-lookup"><span data-stu-id="e6f87-176">Test your function</span></span>

<span data-ttu-id="e6f87-177">İşlevinizi test etmek için bir MP4 dosyasına karşıya yüklemek gereken **giriş** bağlantı dizesinde belirtilen depolama hesabının kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="e6f87-177">To test your function, you need to upload an MP4 file into the **input** container of the storage account that you specified in the connection string.</span></span>  

## <a name="next-step"></a><span data-ttu-id="e6f87-178">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="e6f87-178">Next step</span></span>

<span data-ttu-id="e6f87-179">Bu noktada, Media Services uygulama geliştirmeye başlamak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="e6f87-179">At this point, you are ready to start developing a Media Services application.</span></span> 
 
<span data-ttu-id="e6f87-180">Daha fazla ayrıntı ve Azure işlevleri ve Logic Apps özel içerik oluşturma iş akışı oluşturmak üzere Azure Media Services ile kullanma tam örnekleri/çözümler için bkz: [Media Services .NET işlevleri tümleştirme örnek github'da](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span><span class="sxs-lookup"><span data-stu-id="e6f87-180">For more details and complete samples/solutions of using Azure Functions and Logic Apps with Azure Media Services to create custom content creation workflows, see the [Media Services .NET Functions Integraiton Sample on GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span></span>

<span data-ttu-id="e6f87-181">Ayrıca bkz [.NET ile Media Services iş bildirimleri izlemek için kullanım Azure Kancalarını](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="e6f87-181">Also, see [Use Azure WebHooks to monitor Media Services job notifications with .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="e6f87-182">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="e6f87-182">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e6f87-183">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="e6f87-183">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

