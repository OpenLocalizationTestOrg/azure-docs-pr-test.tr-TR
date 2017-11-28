---
title: "aaaDevelop Media Services ile Azure işlevleri"
description: "Bu konu, nasıl Azure portal ile Media Services'i kullanarak Azure işlevleri geliştirme toostart hello gösterir."
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
ms.openlocfilehash: 3b2c2fb498fea399c862dfbdb63033d06cabf6d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
#<a name="develop-azure-functions-with-media-services"></a><span data-ttu-id="b88e6-103">Azure işlevleri Media Services ile geliştirme</span><span class="sxs-lookup"><span data-stu-id="b88e6-103">Develop Azure Functions with Media Services</span></span>

<span data-ttu-id="b88e6-104">Bu konuda tooget Media Services'i kullanma Azure işlevleri oluşturma ile çalışmaya nasıl gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b88e6-104">This topic shows you how tooget started with creating Azure Functions that use Media Services.</span></span> <span data-ttu-id="b88e6-105">Hello Azure Bu konu başlığı altında tanımlanan işlevi izler adlı bir depolama hesabı kapsayıcısının **giriş** yeni MP4 dosyaları için.</span><span class="sxs-lookup"><span data-stu-id="b88e6-105">hello Azure Function defined in this topic monitors a storage account container named **input** for new MP4 files.</span></span> <span data-ttu-id="b88e6-106">Bir dosya hello depolama kapsayıcıya bırakılan sonra hello blob tetikleyici hello işlevi yürütülür.</span><span class="sxs-lookup"><span data-stu-id="b88e6-106">Once a file is dropped into hello storage container, hello blob trigger will execute hello function.</span></span>

<span data-ttu-id="b88e6-107">Tooexplore istediğiniz ve Azure Media Services'i kullanma mevcut Azure işlevleri dağıtırsanız, kullanıma [medya Hizmetleri Azure işlevleri](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="b88e6-107">If you want tooexplore and deploy existing Azure Functions that use Azure Media Services, check out [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span> <span data-ttu-id="b88e6-108">Bu depo, Media Services tooshow iş akışları ilgili tooingesting doğrudan blob depolama alanından tooblob depolama kodlama ve içeriği yazma geri içerik kullanma örnekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b88e6-108">This repository contains examples that use Media Services tooshow workflows related tooingesting content directly from blob storage, encoding, and writing content back tooblob storage.</span></span> <span data-ttu-id="b88e6-109">Ayrıca nasıl toomonitor iş Web kancaları ve Azure kuyruklar üzerinden bildirimleri örnekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b88e6-109">It also includes examples of how toomonitor job notifications via WebHooks and Azure Queues.</span></span> <span data-ttu-id="b88e6-110">İşlevlerinizi hello hello örneklerde göre de geliştirebilirsiniz [medya Hizmetleri Azure işlevleri](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) deposu.</span><span class="sxs-lookup"><span data-stu-id="b88e6-110">You can also develop your Functions based on hello examples in hello [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repository.</span></span> <span data-ttu-id="b88e6-111">toodeploy hello İşlevler, basın hello **tooAzure dağıtmak** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b88e6-111">toodeploy hello functions, press hello **Deploy tooAzure** button.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b88e6-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b88e6-112">Prerequisites</span></span>

- <span data-ttu-id="b88e6-113">İlk işlevinizin oluşturmadan önce toohave etkin bir Azure hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="b88e6-113">Before you can create your first function, you need toohave an active Azure account.</span></span> <span data-ttu-id="b88e6-114">Bir Azure hesabınız yoksa [ücretsiz hesaplar kullanılabilir](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b88e6-114">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="b88e6-115">Azure Media Services (AMS) hesabınızdaki eylemleri gerçekleştirmek ya da Media Services tarafından gönderilen tooevents dinleme toocreate Azure işlevleri kullanacaksanız açıklandığı gibi bir AMS hesabının oluşturmalısınız [burada](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="b88e6-115">If you are going toocreate Azure Functions that perform actions on your Azure Media Services (AMS) account or listen tooevents sent by Media Services, you should create an AMS account, as described [here](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="b88e6-116">Anlayış [nasıl toouse Azure işlevleri](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b88e6-116">Understanding of [how toouse Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="b88e6-117">Ayrıca, gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="b88e6-117">Also, review:</span></span>
    - [<span data-ttu-id="b88e6-118">Azure işlevleri HTTP ve Web kancası bağlamaları</span><span class="sxs-lookup"><span data-stu-id="b88e6-118">Azure functions HTTP and webhook bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
    - [<span data-ttu-id="b88e6-119">Nasıl tooconfigure Azure işlevi uygulama ayarları</span><span class="sxs-lookup"><span data-stu-id="b88e6-119">How tooconfigure Azure Function app settings</span></span>](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a><span data-ttu-id="b88e6-120">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="b88e6-120">Considerations</span></span>

-  <span data-ttu-id="b88e6-121">Merhaba tüketim plan altında çalışan azure işlevlerinin 5 dakika zaman aşımı sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="b88e6-121">Azure Functions running under hello Consumption plan have 5 minutes timeout limit.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="b88e6-122">İşlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="b88e6-122">Create a function app</span></span>

1. <span data-ttu-id="b88e6-123">Toohello Git [Azure portal](http://portal.azure.com) ve Azure hesabınız ile oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b88e6-123">Go toohello [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="b88e6-124">Açıklandığı gibi işlev uygulaması oluşturma [burada](../azure-functions/functions-create-function-app-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b88e6-124">Create a function app as described [here](../azure-functions/functions-create-function-app-portal.md).</span></span>

>[!NOTE]
> <span data-ttu-id="b88e6-125">Hello belirttiğiniz bir depolama hesabı **StorageConnection** ortam değişkeni hello olmalıdır (Merhaba sonraki adıma bakın), uygulamanızın aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="b88e6-125">A storage account that you specify in hello **StorageConnection** environment variable (see hello next step) should be in hello same region as your app.</span></span>

## <a name="configure-function-app-settings"></a><span data-ttu-id="b88e6-126">İşlev uygulaması ayarlarını yapılandır</span><span class="sxs-lookup"><span data-stu-id="b88e6-126">Configure function app settings</span></span>

<span data-ttu-id="b88e6-127">Media Services işlevleri geliştirme işlevlerinizi kullanılan kullanışlı tooadd ortam değişkenleri olur.</span><span class="sxs-lookup"><span data-stu-id="b88e6-127">When developing Media Services functions, it is handy tooadd environment variables that will be used throughout your functions.</span></span> <span data-ttu-id="b88e6-128">tooconfigure uygulama ayarları, hello uygulama ayarlarını yapılandır bağlantısını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b88e6-128">tooconfigure app settings, click hello Configure App Settings link.</span></span> <span data-ttu-id="b88e6-129">Daha fazla bilgi için bkz: [nasıl tooconfigure Azure işlevi uygulama ayarları](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span><span class="sxs-lookup"><span data-stu-id="b88e6-129">For more information, see  [How tooconfigure Azure Function app settings](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span></span> 

<span data-ttu-id="b88e6-130">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b88e6-130">For example:</span></span>

![Ayarlar](./media/media-services-azure-functions/media-services-azure-functions001.png)

<span data-ttu-id="b88e6-132">Bu makalede, tanımlanan hello işlevi uygulama ayarlarınızı ortam değişkenleri aşağıdaki hello olduğu varsayılır:</span><span class="sxs-lookup"><span data-stu-id="b88e6-132">hello function, defined in this article, assumes you have hello following environment variables in your app settings:</span></span>

<span data-ttu-id="b88e6-133">**AMSAccount** : *AMS hesabının adını* (örneğin testams)</span><span class="sxs-lookup"><span data-stu-id="b88e6-133">**AMSAccount** : *AMS account name* (e.g. testams)</span></span>

<span data-ttu-id="b88e6-134">**AMSKey** : *AMS hesap anahtarı* (örneğin IHOySnH + XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM =)</span><span class="sxs-lookup"><span data-stu-id="b88e6-134">**AMSKey** : *AMS account key* (e.g. IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span></span>

<span data-ttu-id="b88e6-135">**MediaServicesStorageAccountName** : *depolama hesabı adı* (örn., testamsstorage)</span><span class="sxs-lookup"><span data-stu-id="b88e6-135">**MediaServicesStorageAccountName** : *storage account name* (e.g., testamsstorage)</span></span>

<span data-ttu-id="b88e6-136">**MediaServicesStorageAccountKey** : *depolama hesabı anahtarı* (örn., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX ==)</span><span class="sxs-lookup"><span data-stu-id="b88e6-136">**MediaServicesStorageAccountKey** : *storage account key* (e.g., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span></span>

<span data-ttu-id="b88e6-137">**StorageConnection** : *depolama bağlantısı* (örn., DefaultEndpointsProtocol = https; AccountName = testamsstorage; AccountKey xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX = ==)</span><span class="sxs-lookup"><span data-stu-id="b88e6-137">**StorageConnection** : *storage connection* (e.g., DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span></span>

## <a name="create-a-function"></a><span data-ttu-id="b88e6-138">İşlev oluşturma</span><span class="sxs-lookup"><span data-stu-id="b88e6-138">Create a function</span></span>

<span data-ttu-id="b88e6-139">İşlev Uygulamanız dağıtıldıktan sonra onu arasında bulabilirsiniz **uygulama hizmetleri** Azure işlevleri.</span><span class="sxs-lookup"><span data-stu-id="b88e6-139">Once your function app is deployed, you can find it among **App Services** Azure Functions.</span></span>

1. <span data-ttu-id="b88e6-140">İşlev uygulamanızı seçin ve'ı tıklatın **yeni işlev**.</span><span class="sxs-lookup"><span data-stu-id="b88e6-140">Select your function app and click **New Function**.</span></span>
2. <span data-ttu-id="b88e6-141">Merhaba seçin **C#** dil ve **veri işleme** senaryo.</span><span class="sxs-lookup"><span data-stu-id="b88e6-141">Choose hello **C#** language and **Data Processing** scenario.</span></span>
3. <span data-ttu-id="b88e6-142">Seçin **BlobTrigger** şablonu.</span><span class="sxs-lookup"><span data-stu-id="b88e6-142">Choose **BlobTrigger** template.</span></span> <span data-ttu-id="b88e6-143">Blob hello karşıya olduğunda bu işlev tetiklenen **giriş** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="b88e6-143">This function will be triggered whenever a blob is uploaded into hello **input** container.</span></span> <span data-ttu-id="b88e6-144">Merhaba **giriş** adı hello belirtilen **yolu**, hello sonraki adımda.</span><span class="sxs-lookup"><span data-stu-id="b88e6-144">hello **input** name is specified in hello **Path**, in hello next step.</span></span>

    ![Dosyaları](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. <span data-ttu-id="b88e6-146">Seçtiğinizde, bundan sonra **BlobTrigger**, daha fazla bazı denetimler hello sayfasında görünür.</span><span class="sxs-lookup"><span data-stu-id="b88e6-146">Once you select **BlobTrigger**, some more controls will appear on hello page.</span></span>

    ![Dosyaları](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. <span data-ttu-id="b88e6-148">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b88e6-148">Click **Create**.</span></span> 


## <a name="files"></a><span data-ttu-id="b88e6-149">Dosyalar</span><span class="sxs-lookup"><span data-stu-id="b88e6-149">Files</span></span>

<span data-ttu-id="b88e6-150">Azure işlevinizi ve bu bölümde açıklanan diğer dosyaları kod dosyaları ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="b88e6-150">Your Azure function is associated with code files and other files that are described in this section.</span></span> <span data-ttu-id="b88e6-151">Varsayılan olarak, bir işlev ilişkili olduğu **function.json** ve **run.csx** (C#) dosyaları.</span><span class="sxs-lookup"><span data-stu-id="b88e6-151">By default, a function is associated with **function.json** and **run.csx** (C#) files.</span></span> <span data-ttu-id="b88e6-152">Tooadd ihtiyacınız olacak bir **project.json** dosya.</span><span class="sxs-lookup"><span data-stu-id="b88e6-152">You will need tooadd a **project.json** file.</span></span> <span data-ttu-id="b88e6-153">Bu bölümde Hello kalan hello tanımlarını bu dosyalar için gösterir.</span><span class="sxs-lookup"><span data-stu-id="b88e6-153">hello rest of this section shows hello definitions for these files.</span></span>

![Dosyaları](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a><span data-ttu-id="b88e6-155">Function.JSON</span><span class="sxs-lookup"><span data-stu-id="b88e6-155">function.json</span></span>

<span data-ttu-id="b88e6-156">Merhaba function.json dosyası hello işlev bağlamaları ve diğer yapılandırma ayarlarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b88e6-156">hello function.json file defines hello function bindings and other configuration settings.</span></span> <span data-ttu-id="b88e6-157">Bu dosya toodetermine hello olayları toomonitor ve yürütme toopass verisine ve dönüş verileri nasıl işlev Hello çalışma zamanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="b88e6-157">hello runtime uses this file toodetermine hello events toomonitor and how toopass data into and return data from function execution.</span></span> <span data-ttu-id="b88e6-158">Daha fazla bilgi için bkz: [Azure işlevleri HTTP ve Web kancası bağlamaları](../azure-functions/functions-reference.md#function-code).</span><span class="sxs-lookup"><span data-stu-id="b88e6-158">For more information, see [Azure functions HTTP and webhook bindings](../azure-functions/functions-reference.md#function-code).</span></span>

>[!NOTE]
><span data-ttu-id="b88e6-159">Set hello **devre dışı** özelliği çok**true** çalıştırılmasını tooprevent hello işlevi.</span><span class="sxs-lookup"><span data-stu-id="b88e6-159">Set hello **disabled** property too**true** tooprevent hello function from being executed.</span></span> 


<span data-ttu-id="b88e6-160">Bir örneği burada verilmiştir **function.json** dosya.</span><span class="sxs-lookup"><span data-stu-id="b88e6-160">Here is an example of **function.json** file.</span></span>

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

### <a name="projectjson"></a><span data-ttu-id="b88e6-161">Project.JSON</span><span class="sxs-lookup"><span data-stu-id="b88e6-161">project.json</span></span>

<span data-ttu-id="b88e6-162">Merhaba project.json dosyası bağımlılıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="b88e6-162">hello project.json file contains dependencies.</span></span> <span data-ttu-id="b88e6-163">Bir örneği burada verilmiştir **project.json** gerekli hello .NET Azure Media Services içeren dosyası Nuget'ten paketler.</span><span class="sxs-lookup"><span data-stu-id="b88e6-163">Here is an example of **project.json** file that includes hello required .NET Azure Media Services packages from Nuget.</span></span> <span data-ttu-id="b88e6-164">Hello en son sürümleri onaylamalısınız şekilde hello sürüm numaraları toohello paketleri, en son güncelleştirmeleri ile değiştirmek olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b88e6-164">Note that hello version numbers will change with latest updates toohello packages, so you should confirm hello most recent versions.</span></span> 

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
    
### <a name="runcsx"></a><span data-ttu-id="b88e6-165">Run.csx</span><span class="sxs-lookup"><span data-stu-id="b88e6-165">run.csx</span></span>

<span data-ttu-id="b88e6-166">Bu hello C# işlevinizi kodudur.</span><span class="sxs-lookup"><span data-stu-id="b88e6-166">This is hello C# code for your function.</span></span>  <span data-ttu-id="b88e6-167">Merhaba işlevi adlı bir depolama hesabı kapsayıcısının izleyiciler tanımlanan **giriş** (ne hello yolunda belirtilen olan) yeni MP4 dosyaları için.</span><span class="sxs-lookup"><span data-stu-id="b88e6-167">hello function defined below monitors a storage account container named **input** (that is what was specified in hello path) for new MP4 files.</span></span> <span data-ttu-id="b88e6-168">Bir dosya hello depolama kapsayıcıya bırakılan sonra hello blob tetikleyici hello işlevi yürütülür.</span><span class="sxs-lookup"><span data-stu-id="b88e6-168">Once a file is dropped into hello storage container, hello blob trigger will execute hello function.</span></span>
    
<span data-ttu-id="b88e6-169">Bu bölümde tanımlanan hello örnek gösterir</span><span class="sxs-lookup"><span data-stu-id="b88e6-169">hello example defined in this section demonstrates</span></span> 

1. <span data-ttu-id="b88e6-170">nasıl tooingest bir varlığa bir medya hizmetleri hesabı (bir blobu bir AMS varlığa kopyalamayı göre) ve</span><span class="sxs-lookup"><span data-stu-id="b88e6-170">how tooingest an asset into a Media Services account (by coping a blob into an AMS asset) and</span></span> 
2. <span data-ttu-id="b88e6-171">nasıl toosubmit Medya Kodlayıcısı standart 's "Uyarlamalı akış" kullanan bir kodlama işi hazır.</span><span class="sxs-lookup"><span data-stu-id="b88e6-171">how toosubmit an encoding job that uses Media Encoder Standard's "Adaptive Streaming" preset .</span></span>

<span data-ttu-id="b88e6-172">Merhaba gerçek hayatta senaryosunda, büyük olasılıkla tootrack ilerleyişini istediğiniz ve kodlanmış Varlığınızı yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="b88e6-172">In hello real life scenario, you most likely want tootrack job progress and then publish your encoded asset.</span></span> <span data-ttu-id="b88e6-173">Daha fazla bilgi için bkz: [kullanım Azure Web Kancalarını toomonitor Media Services iş bildirimleri](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="b88e6-173">For more information, see [Use Azure WebHooks toomonitor Media Services job notifications](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> <span data-ttu-id="b88e6-174">Daha fazla örnek için bkz: [medya Hizmetleri Azure işlevleri](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="b88e6-174">For more examples, see [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>  

<span data-ttu-id="b88e6-175">Tamamladıktan sonra işlevinizi tanımlama tıklatın **kaydedip çalıştırın**.</span><span class="sxs-lookup"><span data-stu-id="b88e6-175">Once you are done defining your function click **Save and Run**.</span></span>

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
        // NOTE that hello variables {fileName} here come from hello path setting in function.json
        // and are passed into hello  Run method signature above. We can use this toomake decisions on what type of file
        // was dropped into hello input container for hello function. 

        // No need toodo any Retry strategy in this function, By default, hello SDK calls a function up too5 times for a 
        // given blob. If hello fifth try fails, hello SDK adds a message tooa queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used hello chached credentials toocreate CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy hello Blob into a new Input Asset for hello Job
        // ***NOTE: Ideally we would have a method tooingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with hello Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with hello encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify hello input asset toobe encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset toocontain hello results of hello job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means hello output asset is not encrypted. 
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
    /// Creates a new asset and copies blobs from hello specifed storage account.
    /// </summary>
    /// <param name="blob">hello specified blob.</param>
    /// <returns>hello new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference toohello storage account that is associated with hello Media Services account. 
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

        // Get hello destination asset container reference
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

        // Get hold of hello destination blob
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
##<a name="test-your-function"></a><span data-ttu-id="b88e6-176">İşlevinizi test</span><span class="sxs-lookup"><span data-stu-id="b88e6-176">Test your function</span></span>

<span data-ttu-id="b88e6-177">tootest, işlevi bir MP4 dosyası hello tooupload gerek **giriş** hello bağlantı dizesinde belirtilen depolama hesabının hello kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="b88e6-177">tootest your function, you need tooupload an MP4 file into hello **input** container of hello storage account that you specified in hello connection string.</span></span>  

## <a name="next-step"></a><span data-ttu-id="b88e6-178">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="b88e6-178">Next step</span></span>

<span data-ttu-id="b88e6-179">Bu noktada, Media Services uygulama geliştirme hazır toostart var.</span><span class="sxs-lookup"><span data-stu-id="b88e6-179">At this point, you are ready toostart developing a Media Services application.</span></span> 
 
<span data-ttu-id="b88e6-180">Daha fazla ayrıntı ve Azure işlevleri ve Logic Apps ile Azure Media Services toocreate özel içerik oluşturma iş akışı kullanarak tam örnekleri/çözümleri için hello bkz [Media Services .NET işlevleri tümleştirme örnek github'da](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span><span class="sxs-lookup"><span data-stu-id="b88e6-180">For more details and complete samples/solutions of using Azure Functions and Logic Apps with Azure Media Services toocreate custom content creation workflows, see hello [Media Services .NET Functions Integraiton Sample on GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span></span>

<span data-ttu-id="b88e6-181">Ayrıca bkz [kullanım Azure Web Kancalarını toomonitor Media Services .NET ile bildirimleri iş](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="b88e6-181">Also, see [Use Azure WebHooks toomonitor Media Services job notifications with .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="b88e6-182">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="b88e6-182">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b88e6-183">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="b88e6-183">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

