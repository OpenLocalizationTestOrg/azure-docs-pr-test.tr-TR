---
title: "Öğretici - .NET için Azure Batch istemci kitaplığını kullanma | Microsoft Docs"
description: "Temel Azure Batch kavramlarını öğrenin ve .NET kullanarak basit bir çözüm derleyin."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 76cb9807-cbc1-405a-8136-d1e53e66e82b
ms.service: batch
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf8fdca51a6a4ad1b7cd4fe6980543199f6b36e0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-building-solutions-with-the-batch-client-library-for-net"></a><span data-ttu-id="c624f-103">.NET için Batch istemci kitaplığıyla çözüm derlemeye başlama</span><span class="sxs-lookup"><span data-stu-id="c624f-103">Get started building solutions with the Batch client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c624f-104">.NET</span><span class="sxs-lookup"><span data-stu-id="c624f-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="c624f-105">Python</span><span class="sxs-lookup"><span data-stu-id="c624f-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="c624f-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="c624f-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="c624f-107">Adım adım C# örnek uygulamasında tartıştığımız gibi, bu makalede [Azure Batch][azure_batch] ve [Batch .NET][net_api] kitaplığı hakkında temel bilgileri öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c624f-107">Learn the basics of [Azure Batch][azure_batch] and the [Batch .NET][net_api] library in this article as we discuss a C# sample application step by step.</span></span> <span data-ttu-id="c624f-108">Bu örnek uygulamanın dosya hazırlığı ve alımı için [Azure Depolama](../storage/common/storage-introduction.md) ile nasıl etkileşime girdiğinin yanı sıra bulutta paralel bir iş yükünü işlemek için Batch hizmetinden nasıl yararlandığını da göreceğiz.</span><span class="sxs-lookup"><span data-stu-id="c624f-108">We look at how the sample application leverages the Batch service to process a parallel workload in the cloud, and how it interacts with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="c624f-109">Ortak Batch uygulama iş akışını öğrenmenin yanı sıra işler, görevler, havuzlar ve işlem düğümü gibi başlıca Batch bileşenleri hakkında da temel bir anlayış kazanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c624f-109">You'll learn a common Batch application workflow and gain a base understanding of the major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="c624f-110">![Batch çözümü iş akışı (temel)][11]</span><span class="sxs-lookup"><span data-stu-id="c624f-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="c624f-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c624f-111">Prerequisites</span></span>
<span data-ttu-id="c624f-112">Bu makalede, C# ve Visual Studio deneyimine sahip olduğunuz varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c624f-112">This article assumes that you have a working knowledge of C# and Visual Studio.</span></span> <span data-ttu-id="c624f-113">Azure’ün yanı sıra Batch ve Storage hizmetleri için aşağıda belirtilen hesap oluşturma gerekliliklerini karşılayabildiğiniz de varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c624f-113">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="c624f-114">Hesaplar</span><span class="sxs-lookup"><span data-stu-id="c624f-114">Accounts</span></span>
* <span data-ttu-id="c624f-115">**Azure hesabı**: Henüz bir Azure aboneliğiniz yoksa, [ücretsiz Azure hesabı oluşturun][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="c624f-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="c624f-116">**Batch hesabı**: Azure aboneliğiniz olduktan sonra, [Azure Batch hesabı oluşturun](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c624f-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="c624f-117">**Storage hesabı**: Bkz. [Azure Storage hesapları hakkında](../storage/common/storage-create-storage-account.md) sayfası, [Storage hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) bölümü.</span><span class="sxs-lookup"><span data-stu-id="c624f-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c624f-118">Batch şu anda *yalnızca*, [Azure Depolama hesapları hakkında](../storage/common/storage-create-storage-account.md) belgesinin [Depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) adlı 5. adımında açıklanan **genel amaçlı** depolama hesabı türünü desteklemektedir.</span><span class="sxs-lookup"><span data-stu-id="c624f-118">Batch currently supports *only* the **general-purpose** storage account type, as described in step #5 [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

### <a name="visual-studio"></a><span data-ttu-id="c624f-119">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c624f-119">Visual Studio</span></span>
<span data-ttu-id="c624f-120">Örnek projeyi oluşturmak için **Visual Studio 2015 veya sonraki** bir sürüme sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c624f-120">You must have **Visual Studio 2015 or newer** to build the sample project.</span></span> <span data-ttu-id="c624f-121">Visual Studio'nun ücretsiz ve deneme sürümlerini [Visual Studio ürünlerine genel bakış][visual_studio] sayfasında bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c624f-121">You can find free and trial versions of Visual Studio in the [overview of Visual Studio products][visual_studio].</span></span>

### <a name="dotnettutorial-code-sample"></a><span data-ttu-id="c624f-122">*DotNetTutorial* kodu örneği</span><span class="sxs-lookup"><span data-stu-id="c624f-122">*DotNetTutorial* code sample</span></span>
<span data-ttu-id="c624f-123">[DotNetTutorial][github_dotnettutorial] örneği GitHub’daki [azure-batch-samples][github_samples] deposunda bulunan çok sayıda Batch kodu örneğinden biridir.</span><span class="sxs-lookup"><span data-stu-id="c624f-123">The [DotNetTutorial][github_dotnettutorial] sample is one of the many Batch code samples found in the [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="c624f-124">Örneklerin tümünü, depo giriş sayfasındaki **Kopyala veya indir > ZIP’i İndir**’e veya [azure-batch-samples-master.zip][github_samples_zip] doğrudan indirme bağlantısına tıklayarak indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c624f-124">You can download all the samples by clicking  **Clone or download > Download ZIP** on the repository home page, or by clicking the [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="c624f-125">ZIP dosyasının içeriğini ayıkladıktan sonra çözümü aşağıdaki klasörde bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c624f-125">Once you've extracted the contents of the ZIP file, you can find the solution in the following folder:</span></span>

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a><span data-ttu-id="c624f-126">Azure Batch Gezgini (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="c624f-126">Azure Batch Explorer (optional)</span></span>
<span data-ttu-id="c624f-127">[Azure Batch Gezgini][github_batchexplorer], GitHub’daki [azure-batch-samples][github_samples] deposunda yer alan ücretsiz bir yardımcı programdır.</span><span class="sxs-lookup"><span data-stu-id="c624f-127">The [Azure Batch Explorer][github_batchexplorer] is a free utility that is included in the [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="c624f-128">Bu öğreticiyi tamamlamak için gerekli olmasa da, Batch çözümlerinizi geliştirirken ve hatalarını ayıklarken yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="c624f-128">While not required to complete this tutorial, it can be useful while developing and debugging your Batch solutions.</span></span>

## <a name="dotnettutorial-sample-project-overview"></a><span data-ttu-id="c624f-129">DotNetTutorial örnek projesine genel bakış</span><span class="sxs-lookup"><span data-stu-id="c624f-129">DotNetTutorial sample project overview</span></span>
<span data-ttu-id="c624f-130">*DotNetTutorial* kod örneği buradaki iki projeden oluşan bir Visual Studio çözümüdür: **DotNetTutorial** ve **TaskApplication**.</span><span class="sxs-lookup"><span data-stu-id="c624f-130">The *DotNetTutorial* code sample is a Visual Studio solution that consists of two projects: **DotNetTutorial** and **TaskApplication**.</span></span>

* <span data-ttu-id="c624f-131">**DotNetTutorial**, işlem düğümlerinde paralel iş yükünü yürütmek için Batch ve Storage hizmetleriyle etkileşime giren istemci uygulamasıdır (sanal makineler).</span><span class="sxs-lookup"><span data-stu-id="c624f-131">**DotNetTutorial** is the client application that interacts with the Batch and Storage services to execute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="c624f-132">DotNetTutorial yerel iş istasyonunuzda çalışır.</span><span class="sxs-lookup"><span data-stu-id="c624f-132">DotNetTutorial runs on your local workstation.</span></span>
* <span data-ttu-id="c624f-133">**TaskApplication**, asıl işi gerçekleştirmek için Azure’deki işlem düğümlerinde çalışan programdır.</span><span class="sxs-lookup"><span data-stu-id="c624f-133">**TaskApplication** is the program that runs on compute nodes in Azure to perform the actual work.</span></span> <span data-ttu-id="c624f-134">Örnekte, `TaskApplication.exe` metni (girdi dosyası), Azure Storage’dan indirilen dosyada ayrıştırıyor.</span><span class="sxs-lookup"><span data-stu-id="c624f-134">In the sample, `TaskApplication.exe` parses the text in a file downloaded from Azure Storage (the input file).</span></span> <span data-ttu-id="c624f-135">Ardından, girdi dosyasında ilk üç sözcüğün göründüğü listenin bulunduğu bir metin dosyası (çıktı dosyası) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c624f-135">Then it produces a text file (the output file) that contains a list of the top three words that appear in the input file.</span></span> <span data-ttu-id="c624f-136">TaskApplication, çıktı dosyasını oluşturduktan sonra dosyayı Azure Storage’a yükler.</span><span class="sxs-lookup"><span data-stu-id="c624f-136">After it creates the output file, TaskApplication uploads the file to Azure Storage.</span></span> <span data-ttu-id="c624f-137">Böylece, indirmek üzere istemci uygulamasının kullanımına hazır hale getirir.</span><span class="sxs-lookup"><span data-stu-id="c624f-137">This makes it available to the client application for download.</span></span> <span data-ttu-id="c624f-138">TaskApplication, Batch hizmetinde paralel olarak birden çok işlem düğümünde çalışır.</span><span class="sxs-lookup"><span data-stu-id="c624f-138">TaskApplication runs in parallel on multiple compute nodes in the Batch service.</span></span>

<span data-ttu-id="c624f-139">Aşağıdaki diyagram, istemci uygulaması tarafından gerçekleştirilen birincil işlemleri, *DotNetTutorial* ve görevler tarafından yürütülen uygulamayı, *TaskApplication* göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="c624f-139">The following diagram illustrates the primary operations that are performed by the client application, *DotNetTutorial*, and the application that is executed by the tasks, *TaskApplication*.</span></span> <span data-ttu-id="c624f-140">Bu temel iş akışı, Batch’le oluşturulan çok sayıda işlem çözümünün tipik halidir.</span><span class="sxs-lookup"><span data-stu-id="c624f-140">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="c624f-141">Batch hizmetinde erişilebilir olan özelliklerin hepsini göstermese de, neredeyse tüm Batch senaryoları bu iş akışının bölümlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="c624f-141">While it does not demonstrate every feature available in the Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="c624f-142">![Batch örnek iş akışı][8]</span><span class="sxs-lookup"><span data-stu-id="c624f-142">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="c624f-143">**1. Adım.**</span><span class="sxs-lookup"><span data-stu-id="c624f-143">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="c624f-144">Azure Blob Storage’da **kapsayıcılar** oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c624f-144">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="c624f-145">
[**2. Adım.**](#step-2-upload-task-application-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="c624f-145">
[**Step 2.**](#step-2-upload-task-application-and-data-files)</span></span> <span data-ttu-id="c624f-146">Kapsayıcılara görev uygulaması dosyalarını ve girdi dosyalarını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c624f-146">Upload task application files and input files to containers.</span></span><br/><span data-ttu-id="c624f-147">
[**3. Adım.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="c624f-147">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="c624f-148">Batch **havuzu** oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c624f-148">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="c624f-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="c624f-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="c624f-150">**StartTask** havuzu görev ikili dosyalarını (TaskApplication), göreve katıldıkları için düğümlere indirir.</span><span class="sxs-lookup"><span data-stu-id="c624f-150">The pool **StartTask** downloads the task binary files (TaskApplication) to nodes as they join the pool.</span></span><br/><span data-ttu-id="c624f-151">
[**4. Adım.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="c624f-151">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="c624f-152">Batch **işi** oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c624f-152">Create a Batch **job**.</span></span><br/><span data-ttu-id="c624f-153">
[**5. Adım**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="c624f-153">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="c624f-154">İşe **görevler** ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c624f-154">Add **tasks** to the job.</span></span><br/>
  <span data-ttu-id="c624f-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="c624f-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="c624f-156">Görevler, düğümlerde yürütmek üzere zamanlanır.</span><span class="sxs-lookup"><span data-stu-id="c624f-156">The tasks are scheduled to execute on nodes.</span></span><br/>
    <span data-ttu-id="c624f-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="c624f-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="c624f-158">Her görev kendi girdi verilerini Azure Storage’dan indirip yürütmeye başlar.</span><span class="sxs-lookup"><span data-stu-id="c624f-158">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="c624f-159">
[**6. Adım**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="c624f-159">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="c624f-160">Görevleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="c624f-160">Monitor tasks.</span></span><br/>
  <span data-ttu-id="c624f-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="c624f-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="c624f-162">Görevlerin tamamlanmasıyla, kendi çıktı verilerini Azure Storage’a yükler.</span><span class="sxs-lookup"><span data-stu-id="c624f-162">As tasks are completed, they upload their output data to Azure Storage.</span></span><br/><span data-ttu-id="c624f-163">
[**7. Adım**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="c624f-163">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="c624f-164">Storage’dan görev çıktısını indirin.</span><span class="sxs-lookup"><span data-stu-id="c624f-164">Download task output from Storage.</span></span>

<span data-ttu-id="c624f-165">Yukarıda belirtildiği gibi, her Batch çözümü tam olarak bu adımları gerçekleştirmese ve çok daha fazlasını içerebilse de; *DotNetTutorial* örnek uygulaması, Batch çözümünde bulunan ortak işlemleri göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="c624f-165">As mentioned, not every Batch solution performs these exact steps, and may include many more, but the *DotNetTutorial* sample application demonstrates common processes found in a Batch solution.</span></span>

## <a name="build-the-dotnettutorial-sample-project"></a><span data-ttu-id="c624f-166">*DotNetTutorial* örnek projesini derleme</span><span class="sxs-lookup"><span data-stu-id="c624f-166">Build the *DotNetTutorial* sample project</span></span>
<span data-ttu-id="c624f-167">Örneği sorunsuz çalıştırmadan önce, *DotNetTutorial* projesinin `Program.cs` dosyasında Batch ve Storage hesabı kimlik bilgilerini belirtmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="c624f-167">Before you can successfully run the sample, you must specify both Batch and Storage account credentials in the *DotNetTutorial* project's `Program.cs` file.</span></span> <span data-ttu-id="c624f-168">Henüz bunu yapmadıysanız, Visual Studio'da `DotNetTutorial.sln` çözüm dosyasına çift tıklayarak çözümü açın.</span><span class="sxs-lookup"><span data-stu-id="c624f-168">If you have not done so already, open the solution in Visual Studio by double-clicking the `DotNetTutorial.sln` solution file.</span></span> <span data-ttu-id="c624f-169">Bunun yerine, **Dosya > Aç > Proje/Çözüm** menüsünü kullanarak Visual Studio'da da açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c624f-169">Or open it from within Visual Studio by using the **File > Open > Project/Solution** menu.</span></span>

<span data-ttu-id="c624f-170">*DotNetTutorial* projesinin içinde `Program.cs` öğesini açın.</span><span class="sxs-lookup"><span data-stu-id="c624f-170">Open `Program.cs` within the *DotNetTutorial* project.</span></span> <span data-ttu-id="c624f-171">Sonra da kimlik bilgilerinizi belirtildiği gibi dosyanın en üstüne yakın bir yere ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c624f-171">Then add your credentials as specified near the top of the file:</span></span>

```csharp
// Update the Batch and Storage account credential strings below with the values
// unique to your accounts. These are used when constructing connection strings
// for the Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> <span data-ttu-id="c624f-172">Yukarıda da belirtildiği gibi, şu an için Azure Depolama’da **genel amaçlı** bir depolama hesabının kimlik bilgilerini belirtmeniz gerekmektedir.</span><span class="sxs-lookup"><span data-stu-id="c624f-172">As mentioned above, you must currently specify the credentials for a **general-purpose** storage account in Azure Storage.</span></span> <span data-ttu-id="c624f-173">Batch uygulamalarınız, **genel amaçlı** depolama hesabı içinde blob depolama kullanır.</span><span class="sxs-lookup"><span data-stu-id="c624f-173">Your Batch applications use blob storage within the **general-purpose** storage account.</span></span> <span data-ttu-id="c624f-174">*Blob depolama* hesap türünü seçerek oluşturulmuş Storage hesabı için kimlik bilgilerini belirtmeyin.</span><span class="sxs-lookup"><span data-stu-id="c624f-174">Do not specify the credentials for a Storage account that was created by selecting the *Blob storage* account type.</span></span>
>
>

<span data-ttu-id="c624f-175">Batch ve Depolama hesabı kimlik bilgilerinizi [Azure portalındaki][azure_portal] hizmetlere ilişkin hesap dikey pencerelerinde bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c624f-175">You can find your Batch and Storage account credentials within the account blade of each service in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="c624f-176">![Portalda Batch kimlik bilgileri][9]
![Portalda Depolama kimlik bilgileri][10]</span><span class="sxs-lookup"><span data-stu-id="c624f-176">![Batch credentials in the portal][9]
![Storage credentials in the portal][10]</span></span><br/>

<span data-ttu-id="c624f-177">Kimlik bilgilerinizle projeyi güncelleştirdiğinizden, Çözüm Gezgini'ndeki çözüme sağ tıklayıp **Çözümü Derle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c624f-177">Now that you've updated the project with your credentials, right-click the solution in Solution Explorer and click **Build Solution**.</span></span> <span data-ttu-id="c624f-178">İstenirse, herhangi bir NuGet paketinin geri yüklenmesini onaylayın.</span><span class="sxs-lookup"><span data-stu-id="c624f-178">Confirm the restoration of any NuGet packages, if you're prompted.</span></span>

> [!TIP]
> <span data-ttu-id="c624f-179">NuGet paketleri otomatik olarak geri yüklemezse ya da paketlerin geri yüklenmesiyle ilgili hatalar görürseniz, [NuGet Paket Yöneticisi][nuget_packagemgr]’sinin yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c624f-179">If the NuGet packages are not automatically restored, or if you see errors about a failure to restore the packages, ensure that you have the [NuGet Package Manager][nuget_packagemgr] installed.</span></span> <span data-ttu-id="c624f-180">Sonra da eksik paketleri indirilmesini etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c624f-180">Then enable the download of missing packages.</span></span> <span data-ttu-id="c624f-181">Paket indirilmesini etkinleştirmek için bkz. [Derleme sırasında paket Geri Yüklemeyi Etkinleştirme][nuget_restore].</span><span class="sxs-lookup"><span data-stu-id="c624f-181">See [Enabling Package Restore During Build][nuget_restore] to enable package download.</span></span>
>
>

<span data-ttu-id="c624f-182">Aşağıdaki bölümlerde, Batch hizmetinde iş yükünü işlemeyi gerçekleştiren örnek uygulamayı adımlara ayırdık ve bu adımlar üzerine ayrıntılı tartıştık.</span><span class="sxs-lookup"><span data-stu-id="c624f-182">In the following sections, we break down the sample application into the steps that it performs to process a workload in the Batch service, and discuss those steps in detail.</span></span> <span data-ttu-id="c624f-183">Örneğin her kod satırı tartışılmadığından, bu makalenin kalanında kendi işinizi yaparken Visual Studio’da çözüm açmak için başvurmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="c624f-183">We encourage you to refer to the open solution in Visual Studio while you work your way through the rest of this article, since not every line of code in the sample is discussed.</span></span>

<span data-ttu-id="c624f-184">1. Adımla başlamak için *DotNetTutorial* projesinin `Program.cs` dosyasındaki `MainAsync` yönteminin en üstüne gidin.</span><span class="sxs-lookup"><span data-stu-id="c624f-184">Navigate to the top of the `MainAsync` method in the *DotNetTutorial* project's `Program.cs` file to start with Step 1.</span></span> <span data-ttu-id="c624f-185">Aşağıdaki her adım bundan sonra kabaca `MainAsync` içindeki yöntem çağrılarının ilerleyişini izler.</span><span class="sxs-lookup"><span data-stu-id="c624f-185">Each step below then roughly follows the progression of method calls in `MainAsync`.</span></span>

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="c624f-186">1. Adım: Storage kapsayıcıları oluşturma</span><span class="sxs-lookup"><span data-stu-id="c624f-186">Step 1: Create Storage containers</span></span>
<span data-ttu-id="c624f-187">![Azure Depolama'da kapsayıcı oluşturma][1]
</span><span class="sxs-lookup"><span data-stu-id="c624f-187">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="c624f-188">Azure Storage ilet etkileşimde bulunmak için Batch’te yerleşik destek bulunur.</span><span class="sxs-lookup"><span data-stu-id="c624f-188">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="c624f-189">Storage hesabınızdaki kapsayıcılar, Batch hesabınızda çalışan görevler için gerekli dosyaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="c624f-189">Containers in your Storage account will provide the files needed by the tasks that run in your Batch account.</span></span> <span data-ttu-id="c624f-190">Kapsayıcılar ayrıca görevlerin oluşturduğu çıktı verilerini depolamak için bir yer sağlar.</span><span class="sxs-lookup"><span data-stu-id="c624f-190">The containers also provide a place to store the output data that the tasks produce.</span></span> <span data-ttu-id="c624f-191">*DotNetTutorial* istemci uygulamasının yapacağı ilk şey [Azure Blob Storage](../storage/common/storage-introduction.md)’da üç kapsayıcı oluşturmaktır:</span><span class="sxs-lookup"><span data-stu-id="c624f-191">The first thing the *DotNetTutorial* client application does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md):</span></span>

* <span data-ttu-id="c624f-192">**uygulama**: Bu kapsayıcı, DLL’ler gibi birçok bağlantının yanı sıra görevlerin yürüttüğü uygulamayı da depolar.</span><span class="sxs-lookup"><span data-stu-id="c624f-192">**application**: This container will store the application run by the tasks, as well as any of its dependencies, such as DLLs.</span></span>
* <span data-ttu-id="c624f-193">**girdi**: Görevler, işlemek için veri dosyalarını *girdi* kapsayıcısından yükleyecektir.</span><span class="sxs-lookup"><span data-stu-id="c624f-193">**input**: Tasks will download the data files to process from the *input* container.</span></span>
* <span data-ttu-id="c624f-194">**çıktı**: Görevler girdi dosyası işlemeyi tamamladıklarında, sonuçları*çıktı* kapsayıcısına yüklerler.</span><span class="sxs-lookup"><span data-stu-id="c624f-194">**output**: When tasks complete input file processing, they will upload the results to the *output* container.</span></span>

<span data-ttu-id="c624f-195">Bir Depolama hesabıyla etkileşime geçmek ve kapsayıcılar oluşturmak için, [.NET için Azure Depolama İstemci Kitaplığı][net_api_storage] kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="c624f-195">In order to interact with a Storage account and create containers, we use the [Azure Storage Client Library for .NET][net_api_storage].</span></span> <span data-ttu-id="c624f-196">[CloudStorageAccount][net_cloudstorageaccount] ile hesaba bir başvuru oluşturuyoruz ve buradan da bir [CloudBlobClient][net_cloudblobclient] oluşturuyoruz:</span><span class="sxs-lookup"><span data-stu-id="c624f-196">We create a reference to the account with [CloudStorageAccount][net_cloudstorageaccount], and from that create a [CloudBlobClient][net_cloudblobclient]:</span></span>

```csharp
// Construct the Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve the storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create the blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

<span data-ttu-id="c624f-197">Uygulamanın tamamında `blobClient` başvurusunu kullanıyor ve bunu bir dizi yönteme parametre olarak geçiriyoruz.</span><span class="sxs-lookup"><span data-stu-id="c624f-197">We use the `blobClient` reference throughout the application and pass it as a parameter to several methods.</span></span> <span data-ttu-id="c624f-198">Bu, hemen yukarıdakini izleyen kod bloğundadır, burada gerçekten de kapsayıcı oluşturmak için buna `CreateContainerIfNotExistAsync` diyoruz.</span><span class="sxs-lookup"><span data-stu-id="c624f-198">An example of this is in the code block that immediately follows the above, where we call `CreateContainerIfNotExistAsync` to actually create the containers.</span></span>

```csharp
// Use the blob client to create the containers in Azure Storage if they don't
// yet exist
const string appContainerName    = "application";
const string inputContainerName  = "input";
const string outputContainerName = "output";
await CreateContainerIfNotExistAsync(blobClient, appContainerName);
await CreateContainerIfNotExistAsync(blobClient, inputContainerName);
await CreateContainerIfNotExistAsync(blobClient, outputContainerName);
```

```csharp
private static async Task CreateContainerIfNotExistAsync(
    CloudBlobClient blobClient,
    string containerName)
{
        CloudBlobContainer container =
            blobClient.GetContainerReference(containerName);

        if (await container.CreateIfNotExistsAsync())
        {
                Console.WriteLine("Container [{0}] created.", containerName);
        }
        else
        {
                Console.WriteLine("Container [{0}] exists, skipping creation.",
                    containerName);
        }
}
```

<span data-ttu-id="c624f-199">Kapsayıcılar oluşturulduktan sonra uygulama artık görevler tarafından kullanılacak dosyaları karşıya yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="c624f-199">Once the containers have been created, the application can now upload the files that will be used by the tasks.</span></span>

> [!TIP]
> <span data-ttu-id="c624f-200">[Net'ten Blob Storage kullanma](../storage/blobs/storage-dotnet-how-to-use-blobs.md), Azure depolama kapsayıcıları ve blob'larla çalışma hakkında kapsamlı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="c624f-200">[How to use Blob Storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="c624f-201">Batch’le çalışmaya başladığınızda okuma listenizin en üstüne yakın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c624f-201">It should be near the top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-application-and-data-files"></a><span data-ttu-id="c624f-202">2. Adım: Görev uygulamasını ve veri dosyalarını karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="c624f-202">Step 2: Upload task application and data files</span></span>
<span data-ttu-id="c624f-203">![Görev uygulamasını ve girdi (veriler) dosyalarını kapsayıcılara yükleme][2]
</span><span class="sxs-lookup"><span data-stu-id="c624f-203">![Upload task application and input (data) files to containers][2]
</span></span><br/>

<span data-ttu-id="c624f-204">Dosyayı karşıya yükleme işleminde, *DotNetTutorial* önce **uygulama** ve **girdi** dosya yolları koleksiyonunu yerel makinede oldukları gibi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c624f-204">In the file upload operation, *DotNetTutorial* first defines collections of **application** and **input** file paths as they exist on the local machine.</span></span> <span data-ttu-id="c624f-205">Sonra da, bir önceki adımda oluşturduğunuz kapsayıcılara bu dosyaları yükler.</span><span class="sxs-lookup"><span data-stu-id="c624f-205">Then it uploads these files to the containers that you created in the previous step.</span></span>

```csharp
// Paths to the executable and its dependencies that will be executed by the tasks
List<string> applicationFilePaths = new List<string>
{
    // The DotNetTutorial project includes a project reference to TaskApplication,
    // allowing us to determine the path of the task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// The collection of data files that are to be processed by the tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload the application and its dependencies to Azure Storage. This is the
// application that will process the data files, and will be executed by each
// of the tasks on the compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload the data files. This is the data that will be processed by each of
// the tasks that are executed on the compute nodes within the pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

<span data-ttu-id="c624f-206">Karşıya yükleme işlemini oluşturan `Program.cs` öğesinde iki yöntem vardır:</span><span class="sxs-lookup"><span data-stu-id="c624f-206">There are two methods in `Program.cs` that are involved in the upload process:</span></span>

* <span data-ttu-id="c624f-207">`UploadFilesToContainerAsync`: Bu yöntem, [ResourceFile][net_resourcefile] nesnelerinin bir koleksiyonunu döndürür (aşağıda açıklanmıştır) ve *filePaths* parametresine geçirilen her dosyayı karşıya yüklemek için `UploadFileToContainerAsync` çağrısı yapar.</span><span class="sxs-lookup"><span data-stu-id="c624f-207">`UploadFilesToContainerAsync`: This method returns a collection of [ResourceFile][net_resourcefile] objects (discussed below) and internally calls `UploadFileToContainerAsync` to upload each file that is passed in the *filePaths* parameter.</span></span>
* <span data-ttu-id="c624f-208">`UploadFileToContainerAsync`: Dosyayı gerçekten karşıya yüklemeyi gerçekleştiren ve [ResourceFile][net_resourcefile] nesnelerini oluşturan yöntem budur.</span><span class="sxs-lookup"><span data-stu-id="c624f-208">`UploadFileToContainerAsync`: This is the method that actually performs the file upload and creates the [ResourceFile][net_resourcefile] objects.</span></span> <span data-ttu-id="c624f-209">Dosyayı karşıya yükledikten sonra, dosya için paylaşılan erişim imzasını (SAS) alır ve temsil ettiği bir ResourceFile nesnesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="c624f-209">After uploading the file, it obtains a shared access signature (SAS) for the file and returns a ResourceFile object that represents it.</span></span> <span data-ttu-id="c624f-210">Paylaşılan erişim imzaları aşağıda da açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c624f-210">Shared access signatures are also discussed below.</span></span>

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} to container [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set the expiry time and permissions for the blob shared access signature.
        // In this case, no start time is specified, so the shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct the SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a><span data-ttu-id="c624f-211">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="c624f-211">ResourceFiles</span></span>
<span data-ttu-id="c624f-212">[ResourceFile][net_resourcefile], görev çalıştırılmadan önce işlem düğümüne yüklenecek, Azure Depolama’da yer alan bir dosyaya bağlantısı olan URL’ye sahip Batch’teki görevleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="c624f-212">A [ResourceFile][net_resourcefile] provides tasks in Batch with the URL to a file in Azure Storage that is downloaded to a compute node before that task is run.</span></span> <span data-ttu-id="c624f-213">[ResourceFile.BlobSource][net_resourcefile_blobsource] özelliği, Azure Depolama’da olduğu gibi dosyanın tam URL'sini belirtir.</span><span class="sxs-lookup"><span data-stu-id="c624f-213">The [ResourceFile.BlobSource][net_resourcefile_blobsource] property specifies the full URL of the file as it exists in Azure Storage.</span></span> <span data-ttu-id="c624f-214">URL’de, dosyaya güvenli erişim sağlayan bir paylaşılan erişim imzası da (SAS) bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="c624f-214">The URL may also include a shared access signature (SAS) that provides secure access to the file.</span></span> <span data-ttu-id="c624f-215">Batch .NET’teki çoğu görev türünde *ResourceFiles* özelliği vardır; bu özellikte şunlar bulunur:</span><span class="sxs-lookup"><span data-stu-id="c624f-215">Most tasks types within Batch .NET include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="c624f-216">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="c624f-216">[CloudTask][net_task]</span></span>
* <span data-ttu-id="c624f-217">[StartTask][net_pool_starttask]</span><span class="sxs-lookup"><span data-stu-id="c624f-217">[StartTask][net_pool_starttask]</span></span>
* <span data-ttu-id="c624f-218">[JobPreparationTask][net_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="c624f-218">[JobPreparationTask][net_jobpreptask]</span></span>
* <span data-ttu-id="c624f-219">[JobReleaseTask][net_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="c624f-219">[JobReleaseTask][net_jobreltask]</span></span>

<span data-ttu-id="c624f-220">DotNetTutorial örnek uygulaması JobPreparationTask veya JobReleaseTask görev türlerini kullanmaz; ancak, bununla ilgili daha fazla bilgiyi [Azure Batch işlem düğümlerinde iş hazırlama ve tamamlama görevlerini çalıştırma](batch-job-prep-release.md) makalesinden edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c624f-220">The DotNetTutorial sample application does not use the JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="c624f-221">Paylaşılan erişim imzası (SAS)</span><span class="sxs-lookup"><span data-stu-id="c624f-221">Shared access signature (SAS)</span></span>
<span data-ttu-id="c624f-222">Paylaşılan erişim imzalar, URL parçası olarak eklendiğinde Azure Storage'da kapsayıcılara ve blob’lara güvenli erişim sağlayan dizelerdir.</span><span class="sxs-lookup"><span data-stu-id="c624f-222">Shared access signatures are strings which—when included as part of a URL—provide secure access to containers and blobs in Azure Storage.</span></span> <span data-ttu-id="c624f-223">DotNetTutorial uygulaması hem blob, hem de kapsayıcı paylaşılan erişim imzası URL’lerini kullanır ve Storage hizmetinden bu paylaşılan erişim imzalarının nasıl alındığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c624f-223">The DotNetTutorial application uses both blob and container shared access signature URLs, and demonstrates how to obtain these shared access signature strings from the Storage service.</span></span>

* <span data-ttu-id="c624f-224">**Blob paylaşılan erişim imzaları**: DotNetTutorial’daki havuza ait StartTask, Storage’dan uygulama ikililerini ve girdi veri dosyalarını indirdiğinde blob paylaşılan erişim imzalarını kullanır (bkz. 3. Adım; aşağıda).</span><span class="sxs-lookup"><span data-stu-id="c624f-224">**Blob shared access signatures**: The pool's StartTask in DotNetTutorial uses blob shared access signatures when it downloads the application binaries and input data files from Storage (see Step #3 below).</span></span> <span data-ttu-id="c624f-225">DotNetTutorial'ın `Program.cs` içindeki `UploadFileToContainerAsync` yönteminde her blob'un paylaşılan erişim imzasını alan kod bulunur.</span><span class="sxs-lookup"><span data-stu-id="c624f-225">The `UploadFileToContainerAsync` method in DotNetTutorial's `Program.cs` contains the code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="c624f-226">Bu işlemi [CloudBlob.GetSharedAccessSignature][net_sas_blob] çağırarak gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="c624f-226">It does so by calling [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span></span>
* <span data-ttu-id="c624f-227">**Kapsayıcı paylaşılan erişim imzaları**: Hesaplama düğümünde her görev işini bitirdiğinde, kendi çıktı dosyasını Azure Storage’daki *çıktı* kapsayıcısına yükler.</span><span class="sxs-lookup"><span data-stu-id="c624f-227">**Container shared access signatures**: As each task finishes its work on the compute node, it uploads its output file to the *output* container in Azure Storage.</span></span> <span data-ttu-id="c624f-228">Bunu yapmak için, TaskApplication dosyayı karşıya yüklediğinde yolun parçası olarak kapsayıcıya yazma izni sağlayan kapsayıcı paylaşılan erişim imzasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="c624f-228">To do so, TaskApplication uses a container shared access signature that provides write access to the container as part of the path when it uploads the file.</span></span> <span data-ttu-id="c624f-229">Kapsayıcı paylaşılan erişim imzası blob paylaşılan erişim imzası alındığında yapılan işleme benzer.</span><span class="sxs-lookup"><span data-stu-id="c624f-229">Obtaining the container shared access signature is done in a similar fashion as when obtaining the blob shared access signature.</span></span> <span data-ttu-id="c624f-230">DotNetTutorial’de, bunu yapmak için `GetContainerSasUrl` yardımcı yönteminin [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] çağırdığını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c624f-230">In DotNetTutorial, you will find that the `GetContainerSasUrl` helper method calls [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] to do so.</span></span> <span data-ttu-id="c624f-231">TaskApplication’ın kapsayıcı paylaşılan erişim imzasını kullanması hakkında daha fazla bilgi için "6. Adım: İzleme Görevleri" başlığı altındakileri okuyacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c624f-231">You'll read more about how TaskApplication uses the container shared access signature in "Step 6: Monitor Tasks."</span></span>

> [!TIP]
> <span data-ttu-id="c624f-232">Storage hesabınızdaki verilere güvenli erişim sağlama hakkında daha fazla bilgi için paylaşılan erişim imzalarındaki iki parçalı seriyi kullanıma alın, [1. Bölüm: Paylaşılan erişim imzası (SAS) modelini anlama](../storage/common/storage-dotnet-shared-access-signature-part-1.md) ve [2. Bölüm: Blob depolama ile paylaşılan erişim imzasını (SAS) oluşturma ve kullanma](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="c624f-232">Check out the two-part series on shared access signatures, [Part 1: Understanding the shared access signature (SAS) model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a shared access signature (SAS) with Blob storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), to learn more about providing secure access to data in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="c624f-233">3. Adım: Batch havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="c624f-233">Step 3: Create Batch pool</span></span>
<span data-ttu-id="c624f-234">![Batch havuzu oluşturma][3]
</span><span class="sxs-lookup"><span data-stu-id="c624f-234">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="c624f-235">Batch **havuzu**, Batch’in işe ait görevleri yürüttüğü işlem düğümlerinin (sanal makineler) koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="c624f-235">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="c624f-236">Uygulama ve veri dosyaları Azure Depolama API'leri ile birlikte Depolama hesabına yüklendikten sonra *DotNetTutorial*, Batch .NET kitaplığı tarafından sağlanan API'ler ile Batch hizmetine çağrı yapmaya başlar.</span><span class="sxs-lookup"><span data-stu-id="c624f-236">After uploading the application and data files to the Storage account with Azure Storage APIs, *DotNetTutorial* begins making calls to the Batch service with APIs provided by the Batch .NET library.</span></span> <span data-ttu-id="c624f-237">Kod öncelikle bir [BatchClient][net_batchclient] oluşturur:</span><span class="sxs-lookup"><span data-stu-id="c624f-237">The code first creates a [BatchClient][net_batchclient]:</span></span>

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

<span data-ttu-id="c624f-238">Ardından örnek, `CreatePoolIfNotExistsAsync` çağrısıyla Batch hesabında bir işlem düğümü havuzu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c624f-238">Next, the sample creates a pool of compute nodes in the Batch account with a call to `CreatePoolIfNotExistsAsync`.</span></span> <span data-ttu-id="c624f-239">`CreatePoolIfNotExistsAsync`, [BatchClient.PoolOperations.CreatePool][net_pool_create] yöntemini kullanarak Batch hizmetinde yeni bir havuz oluşturur:</span><span class="sxs-lookup"><span data-stu-id="c624f-239">`CreatePoolIfNotExistsAsync` uses the [BatchClient.PoolOperations.CreatePool][net_pool_create] method to create a new pool in the Batch service:</span></span>

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create the unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign the StartTask that will be executed when compute nodes join the pool.
        // In this case, we copy the StartTask's resource files (that will be automatically downloaded
        // to the node by the StartTask) into the shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for the StartTask that copies the task application files to the
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need to manually exit with a 0 for Batch to recognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow the specific error code PoolExists since that is expected if the pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("The pool {0} already existed when we tried to create it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

<span data-ttu-id="c624f-240">[CreatePool][net_pool_create] ile havuz oluşturduğunuzda, işlem düğümlerinin sayısı, [düğümlerin boyutu](../cloud-services/cloud-services-sizes-specs.md) ve düğümlerin işletim sistemi gibi parametreleri belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c624f-240">When you create a pool with [CreatePool][net_pool_create], you specify several parameters such as the number of compute nodes, the [size of the nodes](../cloud-services/cloud-services-sizes-specs.md), and the nodes' operating system.</span></span> <span data-ttu-id="c624f-241">*DotNetTutorial* ’da, [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md)’dan Windows Server 2012 R2'yi belirtmek için [CloudServiceConfiguration][net_cloudserviceconfiguration] kullanırız.</span><span class="sxs-lookup"><span data-stu-id="c624f-241">In *DotNetTutorial*, we use [CloudServiceConfiguration][net_cloudserviceconfiguration] to specify Windows Server 2012 R2 from [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> 

<span data-ttu-id="c624f-242">Ayrıca, havuzunuz için [VirtualMachineConfiguration][net_virtualmachineconfiguration] değerini belirterek Azure Sanal Makineleri (VM) olan işlem düğümü havuzları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c624f-242">You can also create pools of compute nodes that are Azure Virtual Machines (VMs) by specifying the [VirtualMachineConfiguration][net_virtualmachineconfiguration] for your pool.</span></span> <span data-ttu-id="c624f-243">VM işlem düğümü havuzlarını Windows veya [Linux görüntülerinden](batch-linux-nodes.md) oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c624f-243">You can create a pool of VM compute nodes from either Windows or [Linux images](batch-linux-nodes.md).</span></span> <span data-ttu-id="c624f-244">VM görüntüleriniz için kaynaklar şunlar olabilir:</span><span class="sxs-lookup"><span data-stu-id="c624f-244">The source for your VM images can be either:</span></span>

- <span data-ttu-id="c624f-245">Hem Windows hem de Linux için kullanıma hazır görüntüler bulabileceğiniz [Microsoft Azure Sanal Makineler Market görüntüleri][vm_marketplace].</span><span class="sxs-lookup"><span data-stu-id="c624f-245">The [Azure Virtual Machines Marketplace][vm_marketplace], which provides both Windows and Linux images that are ready-to-use.</span></span> 
- <span data-ttu-id="c624f-246">Hazırlayıp sağlayacağınız bir özel görüntü.</span><span class="sxs-lookup"><span data-stu-id="c624f-246">A custom image that you prepare and provide.</span></span> <span data-ttu-id="c624f-247">Özel görüntüler hakkında daha fazla ayrıntı için bkz. [Batch ile büyük ölçekli paralel işlem çözümleri geliştirme](batch-api-basics.md#pool).</span><span class="sxs-lookup"><span data-stu-id="c624f-247">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c624f-248">Batch’teki işlem kaynakları ücretlidir.</span><span class="sxs-lookup"><span data-stu-id="c624f-248">You are charged for compute resources in Batch.</span></span> <span data-ttu-id="c624f-249">Maliyetleri en aza indirmek için, örneği çalıştırmadan önce `targetDedicatedComputeNodes` değerini 1 olarak düşürün.</span><span class="sxs-lookup"><span data-stu-id="c624f-249">To minimize costs, you can lower `targetDedicatedComputeNodes` to 1 before you run the sample.</span></span>
>
>

<span data-ttu-id="c624f-250">Bu fiziksel düğüm özellikleriyle birlikte, havuz için ayrıca bir [StartTask][net_pool_starttask] belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c624f-250">Along with these physical node properties, you may also specify a [StartTask][net_pool_starttask] for the pool.</span></span> <span data-ttu-id="c624f-251">StartTask, her düğümü havuza katıldığında ve her yeniden başlatıldığında yürütecektir.</span><span class="sxs-lookup"><span data-stu-id="c624f-251">The StartTask executes on each node as that node joins the pool, and each time a node is restarted.</span></span> <span data-ttu-id="c624f-252">StartTask özellikle, görevler yürütülmeden önce işlem düğümlerine uygulamaların yüklenmesi için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="c624f-252">The StartTask is especially useful for installing applications on compute nodes prior to the execution of tasks.</span></span> <span data-ttu-id="c624f-253">Örneğin, görevleriniz verileri Python betiklerini kullanarak işliyorsa, işlem düğümlerine Python yüklemek için StartTask kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c624f-253">For example, if your tasks process data by using Python scripts, you could use a StartTask to install Python on the compute nodes.</span></span>

<span data-ttu-id="c624f-254">Bu örnek uygulamasında StartTask, Depolama’dan indirilen dosyaları ([StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles] özelliği kullanılarak belirtilir), StartTask çalışma dizininden, erişilebilir düğümdeki *tüm* görevlerin çalıştığı paylaşılan dizine kopyalar.</span><span class="sxs-lookup"><span data-stu-id="c624f-254">In this sample application, the StartTask copies the files that it downloads from Storage (which are specified by using the [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles] property) from the StartTask working directory to the shared directory that *all* tasks running on the node can access.</span></span> <span data-ttu-id="c624f-255">Aslında, `TaskApplication.exe` uygulamasını ve bağlantılarını, düğüm havuza katılmış olduğundan her düğüme kopyalar; bu nedenle düğümde çalışan görevler buna erişebilir.</span><span class="sxs-lookup"><span data-stu-id="c624f-255">Essentially, this copies `TaskApplication.exe` and its dependencies to the shared directory on each node as the node joins the pool, so that any tasks that run on the node can access it.</span></span>

> [!TIP]
> <span data-ttu-id="c624f-256">Azure Batch’in **uygulama paketleri** özelliği, havuzdaki işlem düğümlerinin uygulamanızı almasının başka bir yolunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="c624f-256">The **application packages** feature of Azure Batch provides another way to get your application onto the compute nodes in a pool.</span></span> <span data-ttu-id="c624f-257">Ayrıntılar için [Batch uygulama paketleriyle işlem düğümleri için uygulama dağıtımı](batch-application-packages.md) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="c624f-257">See [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md) for details.</span></span>
>
>

<span data-ttu-id="c624f-258">Yukarıdaki kod parçacığında dikkat çeken bir şey de, StartTask’ın *CommandLine* özelliğinde iki ortam değişkenin kullanılmasıdır: `%AZ_BATCH_TASK_WORKING_DIR%` ve `%AZ_BATCH_NODE_SHARED_DIR%`.</span><span class="sxs-lookup"><span data-stu-id="c624f-258">Also notable in the code snippet above is the use of two environment variables in the *CommandLine* property of the StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` and `%AZ_BATCH_NODE_SHARED_DIR%`.</span></span> <span data-ttu-id="c624f-259">Batch havuzundaki her işlem düğümü, Batch’e özel bazı ortam değişkenleriyle yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="c624f-259">Each compute node within a Batch pool is automatically configured with several environment variables that are specific to Batch.</span></span> <span data-ttu-id="c624f-260">Görev tarafından yürütülen işlemlerin bu ortam değişkenlerine erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="c624f-260">Any process that is executed by a task has access to these environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="c624f-261">Batch havuzundaki işlem düğümlerinde bulunan ortam değişkenleri ve görev çalışma dizinleri hakkında daha fazla bilgi almak için [Geliştiriciler için Batch özelliğine genel bakış](batch-api-basics.md) içindeki [Görevler için ortam değişkenleri](batch-api-basics.md#environment-settings-for-tasks) ve [Dosya ve dizinler](batch-api-basics.md#files-and-directories) bölümlerine bakın.</span><span class="sxs-lookup"><span data-stu-id="c624f-261">To find out more about the environment variables that are available on compute nodes in a Batch pool, and information on task working directories, see the [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) and [Files and directories](batch-api-basics.md#files-and-directories) sections in the [Batch feature overview for developers](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="c624f-262">4. Adım: Batch işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c624f-262">Step 4: Create Batch job</span></span>
<span data-ttu-id="c624f-263">![Batch işi oluşturma][4]</span><span class="sxs-lookup"><span data-stu-id="c624f-263">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="c624f-264">Batch **işi**, görevler koleksiyonudur ve işlem düğümlerinin bir havuzuyla ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="c624f-264">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="c624f-265">İşteki görevler ilişkili havuzunun işlem düğümlerini yürütür.</span><span class="sxs-lookup"><span data-stu-id="c624f-265">The tasks in a job execute on the associated pool's compute nodes.</span></span>

<span data-ttu-id="c624f-266">İşi yalnızca ilgili iş yüklerinde görevlerin düzenlenmesi ve izlenmesi için değil, aynı zamanda işin (ve buna bağlı olarak görevlerin) en uzun çalışma süresinin yanı sıra Batch hesabındaki diğer işlerle bağlantılı olarak iş önceliği gibi bazı kısıtlamalar getirmek için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c624f-266">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as the maximum runtime for the job (and by extension, its tasks) as well as job priority in relation to other jobs in the Batch account.</span></span> <span data-ttu-id="c624f-267">Ancak bu örnekte, iş yalnızca 3. adımda oluşturulan havuzla ilişkilendirilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c624f-267">In this example, however, the job is associated only with the pool that was created in step #3.</span></span> <span data-ttu-id="c624f-268">Yapılandırılmış başka ek özellik yoktur.</span><span class="sxs-lookup"><span data-stu-id="c624f-268">No additional properties are configured.</span></span>

<span data-ttu-id="c624f-269">Tüm Batch işleri belirli bir havuzla ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="c624f-269">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="c624f-270">Bu ilişkilendirme, iş görevlerinin hangi düğümleri yürüteceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="c624f-270">This association indicates which nodes the job's tasks will execute on.</span></span> <span data-ttu-id="c624f-271">Bunu, aşağıdaki kod parçacığında gösterildiği gibi [CloudJob.PoolInformation][net_job_poolinfo] özelliğini kullanarak belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c624f-271">You specify this by using the [CloudJob.PoolInformation][net_job_poolinfo] property, as shown in the code snippet below.</span></span>

```csharp
private static async Task CreateJobAsync(
    BatchClient batchClient,
    string jobId,
    string poolId)
{
    Console.WriteLine("Creating job [{0}]...", jobId);

    CloudJob job = batchClient.JobOperations.CreateJob();
    job.Id = jobId;
    job.PoolInformation = new PoolInformation { PoolId = poolId };

    await job.CommitAsync();
}
```

<span data-ttu-id="c624f-272">İş oluşturulduğuna göre, artık çalışmak için görevler eklenir.</span><span class="sxs-lookup"><span data-stu-id="c624f-272">Now that a job has been created, tasks are added to perform the work.</span></span>

## <a name="step-5-add-tasks-to-job"></a><span data-ttu-id="c624f-273">5. Adım: İşe görev ekleme</span><span class="sxs-lookup"><span data-stu-id="c624f-273">Step 5: Add tasks to job</span></span>
<span data-ttu-id="c624f-274">![İşe görev ekleme][5]</span><span class="sxs-lookup"><span data-stu-id="c624f-274">![Add tasks to job][5]</span></span><br/><span data-ttu-id="c624f-275">
*(1) Görevler işe eklenir, (2) görevler düğümlerde çalışmak üzere zamanlanır ve (3) görevler işlemek üzere veri dosyalarını indirir*</span><span class="sxs-lookup"><span data-stu-id="c624f-275">
*(1) Tasks are added to the job, (2) the tasks are scheduled to run on nodes, and (3) the tasks download the data files to process*</span></span>

<span data-ttu-id="c624f-276">Batch **görevleri**, işlem düğümlerinde yürütülen tek tek iş birimleridir.</span><span class="sxs-lookup"><span data-stu-id="c624f-276">Batch **tasks** are the individual units of work that execute on the compute nodes.</span></span> <span data-ttu-id="c624f-277">Görevde bir komut satırı vardır; bu komut satırında belirttiğiniz betikleri veya yürütülebilir dosyaları çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="c624f-277">A task has a command line and runs the scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="c624f-278">Aslına bakılırsa, çalışmayı gerçekleştirmek için görevlerin işe eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c624f-278">To actually perform work, tasks must be added to a job.</span></span> <span data-ttu-id="c624f-279">Her [CloudTask][net_task], bir komut satırı özelliği ve komut satırı otomatik olarak yürütülmeden önce görevin düğüme yüklediği [ResourceFiles][net_task_resourcefiles] (havuzdaki StartTask gibi) kullanılarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="c624f-279">Each [CloudTask][net_task] is configured by using a command-line property and [ResourceFiles][net_task_resourcefiles] (as with the pool's StartTask) that the task downloads to the node before its command line is automatically executed.</span></span> <span data-ttu-id="c624f-280">*DotNetTutorial* örnek projesinde her görev yalnızca tek bir dosya işler.</span><span class="sxs-lookup"><span data-stu-id="c624f-280">In the *DotNetTutorial* sample project, each task processes only one file.</span></span> <span data-ttu-id="c624f-281">Bu nedenle, kendi ResourceFiles koleksiyonunda tek bir öğe bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c624f-281">Thus, its ResourceFiles collection contains a single element.</span></span>

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks to job [{1}]...", inputFiles.Count, jobId);

    // Create a collection to hold the tasks that we'll be adding to the job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of the tasks. Because we copied the task application to the
    // node's shared directory with the pool's StartTask, we can access it via
    // the shared directory on the node that the task runs on.
    foreach (ResourceFile inputFile in inputFiles)
    {
        string taskId = "topNtask" + inputFiles.IndexOf(inputFile);
        string taskCommandLine = String.Format(
            "cmd /c %AZ_BATCH_NODE_SHARED_DIR%\\TaskApplication.exe {0} 3 \"{1}\"",
            inputFile.FilePath,
            outputContainerSasUrl);

        CloudTask task = new CloudTask(taskId, taskCommandLine);
        task.ResourceFiles = new List<ResourceFile> { inputFile };
        tasks.Add(task);
    }

    // Add the tasks as a collection, as opposed to issuing a separate AddTask call
    // for each. Bulk task submission helps to ensure efficient underlying API calls
    // to the Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> <span data-ttu-id="c624f-282">`%AZ_BATCH_NODE_SHARED_DIR%` gibi ortam değişkenlerine eriştiklerinde veya düğüme ait `PATH` öğesinde bulunmayan bir uygulama yürüttüklerinde görev komut satırları `cmd /c` önekini almalıdır.</span><span class="sxs-lookup"><span data-stu-id="c624f-282">When they access environment variables such as `%AZ_BATCH_NODE_SHARED_DIR%` or execute an application not found in the node's `PATH`, task command lines must be prefixed with `cmd /c`.</span></span> <span data-ttu-id="c624f-283">Bunu kesinlikle komut yorumlayıcı yürütecek ve komutunuzu uyguladıktan sonra sonlandırması talimatını verecektir.</span><span class="sxs-lookup"><span data-stu-id="c624f-283">This will explicitly execute the command interpreter and instruct it to terminate after carrying out your command.</span></span> <span data-ttu-id="c624f-284">Görevleriniz düğümün `PATH` öğesinde (*robocopy.exe* veya *powershell.exe* gibi) bir uygulama yürütüyorsa ve hiç ortam değişkeni kullanılmıyorsa bu gereksinim gereksizdir.</span><span class="sxs-lookup"><span data-stu-id="c624f-284">This requirement is unnecessary if your tasks execute an application in the node's `PATH` (such as *robocopy.exe* or *powershell.exe*) and no environment variables are used.</span></span>
>
>

<span data-ttu-id="c624f-285">Yukarıdaki kod parçacığında, `foreach` döngüsü içinde görevle ilgili komut satırının, üç komut satırı bağımsız değişkeni *TaskApplication.exe* dosyasına geçirilecek şekilde oluşturulduğunu görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="c624f-285">Within the `foreach` loop in the code snippet above, you can see that the command line for the task is constructed such that three command-line arguments are passed to *TaskApplication.exe*:</span></span>

1. <span data-ttu-id="c624f-286">**İlk bağımsız değişken** işlenecek dosyanın yoludur.</span><span class="sxs-lookup"><span data-stu-id="c624f-286">The **first argument** is the path of the file to process.</span></span> <span data-ttu-id="c624f-287">Düğümde yer aldığından dosyanın yerel yolu budur.</span><span class="sxs-lookup"><span data-stu-id="c624f-287">This is the local path to the file as it exists on the node.</span></span> <span data-ttu-id="c624f-288">`UploadFileToContainerAsync` ResourceFile nesnesi ilk oluşturulduğunda dosya adı bu özellik için kullanılır (parametrenin ResourceFile oluşturucuda yaptığı gibi).</span><span class="sxs-lookup"><span data-stu-id="c624f-288">When the ResourceFile object in `UploadFileToContainerAsync` was first created above, the file name was used for this property (as a parameter to the ResourceFile constructor).</span></span> <span data-ttu-id="c624f-289">Dosyanın *TaskApplication.exe* ile aynı dizinde bulunabileceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="c624f-289">This indicates that the file can be found in the same directory as *TaskApplication.exe*.</span></span>
2. <span data-ttu-id="c624f-290">**İkinci bağımsız değişken** ilk *N* sayıda sözcüğün çıktı dosyasına yazılması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="c624f-290">The **second argument** specifies that the top *N* words should be written to the output file.</span></span> <span data-ttu-id="c624f-291">Bu, örnekte sabit kodlanmıştır; bu nedenle çıktı dosyasına ilk üç sözcük yazılır.</span><span class="sxs-lookup"><span data-stu-id="c624f-291">In the sample, this is hard-coded so that the top three words are written to the output file.</span></span>
3. <span data-ttu-id="c624f-292">**Üçüncü bağımsız değişken**, Azure Storage’da **çıktı** kapsayıcısına yazma erişimi sağlayan paylaşılan erişim imzasıdır (SAS).</span><span class="sxs-lookup"><span data-stu-id="c624f-292">The **third argument** is the shared access signature (SAS) that provides write access to the **output** container in Azure Storage.</span></span> <span data-ttu-id="c624f-293">*TaskApplication.exe*, çıktı dosyasını Azure Storage’a yüklediğinde paylaşılan erişim imzası URL'sini kullanır.</span><span class="sxs-lookup"><span data-stu-id="c624f-293">*TaskApplication.exe* uses this shared access signature URL when it uploads the output file to Azure Storage.</span></span> <span data-ttu-id="c624f-294">Bunun için kodu, TaskApplication projesinin `Program.cs` dosyasındaki `UploadFileToContainer` yönteminde bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c624f-294">You can find the code for this in the `UploadFileToContainer` method in the TaskApplication project's `Program.cs` file:</span></span>

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference to the container using the SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload the file (as a new blob) to the container
        try
        {
                CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
                blob.UploadFromFile(filePath);

                Console.WriteLine("Write operation succeeded for SAS URL " + containerSas);
                Console.WriteLine();
        }
        catch (StorageException e)
        {

                Console.WriteLine("Write operation failed for SAS URL " + containerSas);
                Console.WriteLine("Additional error information: " + e.Message);
                Console.WriteLine();

                // Indicate that a failure has occurred so that when the Batch service
                // sets the CloudTask.ExecutionInformation.ExitCode for the task that
                // executed this application, it properly indicates that there was a
                // problem with the task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="c624f-295">6. Adım: Görevleri izleme</span><span class="sxs-lookup"><span data-stu-id="c624f-295">Step 6: Monitor tasks</span></span>
<span data-ttu-id="c624f-296">![Görevleri izleme][6]</span><span class="sxs-lookup"><span data-stu-id="c624f-296">![Monitor tasks][6]</span></span><br/><span data-ttu-id="c624f-297">
*İstemci uygulaması (1) tamamlama ve başarı durumu için görevleri izler, (2) görevler de sonuç verilerini Azure Depolama’ya yükler.*</span><span class="sxs-lookup"><span data-stu-id="c624f-297">
*The client application (1) monitors the tasks for completion and success status, and (2) the tasks upload result data to Azure Storage*</span></span>

<span data-ttu-id="c624f-298">Görevler bir projeye eklendiğinde, otomatik olarak kuyruğa alınır ve işle ilişkili havuzun içindeki işlem düğümlerinde zamanlanırlar.</span><span class="sxs-lookup"><span data-stu-id="c624f-298">When tasks are added to a job, they are automatically queued and scheduled for execution on compute nodes within the pool associated with the job.</span></span> <span data-ttu-id="c624f-299">Belirttiğiniz ayarlar temelinde, Batch tüm kuyruğa alınan, zamanlanan, yeniden denenen ve sizle ilgili diğer görev yönetimi görevlerini işler.</span><span class="sxs-lookup"><span data-stu-id="c624f-299">Based on the settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="c624f-300">Görevin yürütülüşünün izlenmesi için birçok yaklaşım vardır.</span><span class="sxs-lookup"><span data-stu-id="c624f-300">There are many approaches to monitoring task execution.</span></span> <span data-ttu-id="c624f-301">DotNetTutorial, yalnızca tamamlama, görev başarılı veya başarısız durumlarını raporlayan basit bir örnek gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c624f-301">DotNetTutorial shows a simple example that reports only on completion and task failure or success states.</span></span> <span data-ttu-id="c624f-302">DotNetTutorial'in `Program.cs` konumundaki `MonitorTasks` yönteminde tartışmayı destekleyen üç Batch .NET kavramı vardır.</span><span class="sxs-lookup"><span data-stu-id="c624f-302">Within the `MonitorTasks` method in DotNetTutorial's `Program.cs`, there are three Batch .NET concepts that warrant discussion.</span></span> <span data-ttu-id="c624f-303">Görüntülenme sırasıyla aşağıda listelenmişlerdir:</span><span class="sxs-lookup"><span data-stu-id="c624f-303">They are listed below in their order of appearance:</span></span>

1. <span data-ttu-id="c624f-304">**ODATADetailLevel**: Liste işlemlerinde [ODATADetailLevel][net_odatadetaillevel] belirtilmesi (iş görevlerinin listesini almak gibi) Batch uygulaması performansını sağlamak için önemlidir.</span><span class="sxs-lookup"><span data-stu-id="c624f-304">**ODATADetailLevel**: Specifying [ODATADetailLevel][net_odatadetaillevel] in list operations (such as obtaining a list of a job's tasks) is essential in ensuring Batch application performance.</span></span> <span data-ttu-id="c624f-305">Batch uygulamanızda durum izlemenin herhangi bir biçimini yapmak için hazırlık yapıyorsanız okuma listenize [Azure Batch hizmetini etkin bir şekilde sorgulama](batch-efficient-list-queries.md) makalesini de ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c624f-305">Add [Query the Azure Batch service efficiently](batch-efficient-list-queries.md) to your reading list if you plan on doing any sort of status monitoring within your Batch applications.</span></span>
2. <span data-ttu-id="c624f-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor], görev durumlarının izlenmesi için yardımcı programlara sahip Batch .NET uygulamalarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="c624f-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] provides Batch .NET applications with helper utilities for monitoring task states.</span></span> <span data-ttu-id="c624f-307">`MonitorTasks` konumunda, *DotNetTutorial* tüm görevler için sınırlı bir süre içinde [TaskState.Completed][net_taskstate] konumuna ulaşmak için bekler.</span><span class="sxs-lookup"><span data-stu-id="c624f-307">In `MonitorTasks`, *DotNetTutorial* waits for all tasks to reach [TaskState.Completed][net_taskstate] within a time limit.</span></span> <span data-ttu-id="c624f-308">Sonra da işi sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="c624f-308">Then it terminates the job.</span></span>
3. <span data-ttu-id="c624f-309">**TerminateJobAsync**: İşin [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] ile sonlandırılması (veya JobOperations.TerminateJob’un engellenmesi) bu işin tamamlandı olarak işaretlenmesine yol açar.</span><span class="sxs-lookup"><span data-stu-id="c624f-309">**TerminateJobAsync**: Terminating a job with [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (or the blocking JobOperations.TerminateJob) marks that job as completed.</span></span> <span data-ttu-id="c624f-310">Batch çözümünüz [JobReleaseTask][net_jobreltask] kullanıyorsa bunun yapılması gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c624f-310">It is essential to do so if your Batch solution uses a [JobReleaseTask][net_jobreltask].</span></span> <span data-ttu-id="c624f-311">[İş hazırlama ve tamamlama görevleri](batch-job-prep-release.md)’nde açıklanan özel tür bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="c624f-311">This is a special type of task, which is described in [Job preparation and completion tasks](batch-job-prep-release.md).</span></span>

<span data-ttu-id="c624f-312">*DotNetTutorial*'ın `Program.cs` öğesine ait `MonitorTasks` yöntemi aşağıda görüntülenmektedir:</span><span class="sxs-lookup"><span data-stu-id="c624f-312">The `MonitorTasks` method from *DotNetTutorial*'s `Program.cs` appears below:</span></span>

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed to reach the Completed state within the timeout period.";

    // Obtain the collection of tasks currently managed by the job. Note that we use
    // a detail level to  specify that only the "id" property of each task should be
    // populated. Using a detail level for all list operations helps to lower
    // response time from the Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor to monitor the state of our tasks. In this case, we
    // will wait for all tasks to reach the Completed state.
    TaskStateMonitor taskStateMonitor
        = batchClient.Utilities.CreateTaskStateMonitor();

    try
    {
        await taskStateMonitor.WhenAll(tasks, TaskState.Completed, timeout);
    }
    catch (TimeoutException)
    {
        await batchClient.JobOperations.TerminateJobAsync(jobId, failureMessage);
        Console.WriteLine(failureMessage);
        return false;
    }

    await batchClient.JobOperations.TerminateJobAsync(jobId, successMessage);

    // All tasks have reached the "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property to ensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update the detail level to populate only the task id and executionInfo
    // properties. We refresh the tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate the task's properties with the latest info from the Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with the task. It is important to note that
            // the task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that the application executed by the task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within the specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="c624f-313">7. Adım: Görev çıktısı indirme</span><span class="sxs-lookup"><span data-stu-id="c624f-313">Step 7: Download task output</span></span>
<span data-ttu-id="c624f-314">![Storage'dan görev çıktısını indirme][7]</span><span class="sxs-lookup"><span data-stu-id="c624f-314">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="c624f-315">Artık iş tamamlandı, görevlere ait çıktı Azure Storage’dan indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="c624f-315">Now that the job is completed, the output from the tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="c624f-316">*DotNetTutorial*'a ait `Program.cs` içinde `DownloadBlobsFromContainerAsync` çağrısıyla yapılır:</span><span class="sxs-lookup"><span data-stu-id="c624f-316">This is done with a call to `DownloadBlobsFromContainerAsync` in *DotNetTutorial*'s `Program.cs`:</span></span>

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference to a previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all the block blobs in the specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference to the current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents to a file in the specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded to {0}", directoryPath);
}
```

> [!NOTE]
> <span data-ttu-id="c624f-317">*DotNetTutorial* uygulamasındaki `DownloadBlobsFromContainerAsync` çağrısı dosyaların `%TEMP%` klasörünüze yüklenmiş olması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="c624f-317">The call to `DownloadBlobsFromContainerAsync` in the *DotNetTutorial* application specifies that the files should be downloaded to your `%TEMP%` folder.</span></span> <span data-ttu-id="c624f-318">Bu çıktı konumunu değiştirmekten çekinmeyin.</span><span class="sxs-lookup"><span data-stu-id="c624f-318">Feel free to modify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="c624f-319">8. Adım: Sil kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="c624f-319">Step 8: Delete containers</span></span>
<span data-ttu-id="c624f-320">Azure Storage’da yer alan veriler için ücretlendirildiğinizden, Batch işleriniz için artık gerekmeyen blobları kaldırmak iyi bir fikirdir.</span><span class="sxs-lookup"><span data-stu-id="c624f-320">Because you are charged for data that resides in Azure Storage, it's always a good idea to remove blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="c624f-321">DotNetTutorial'ın `Program.cs` öğesinde, `DeleteContainerAsync` yardımcı yöntemine yönelik üç çağrı yapılır:</span><span class="sxs-lookup"><span data-stu-id="c624f-321">In DotNetTutorial's `Program.cs`, this is done with three calls to the helper method `DeleteContainerAsync`:</span></span>

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

<span data-ttu-id="c624f-322">Yöntemin kendisi yalnızca kapsayıcıya başvuru alır ve ardından [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete] öğesini çağırır:</span><span class="sxs-lookup"><span data-stu-id="c624f-322">The method itself merely obtains a reference to the container, and then calls [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span></span>

```csharp
private static async Task DeleteContainerAsync(
    CloudBlobClient blobClient,
    string containerName)
{
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);

    if (await container.DeleteIfExistsAsync())
    {
        Console.WriteLine("Container [{0}] deleted.", containerName);
    }
    else
    {
        Console.WriteLine("Container [{0}] does not exist, skipping deletion.",
            containerName);
    }
}
```

## <a name="step-9-delete-the-job-and-the-pool"></a><span data-ttu-id="c624f-323">9. Adım: İşi ve havuzu silme</span><span class="sxs-lookup"><span data-stu-id="c624f-323">Step 9: Delete the job and the pool</span></span>
<span data-ttu-id="c624f-324">Son adımda, DotNetTutorial uygulaması tarafından oluşturulan işi ve havuzu silmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="c624f-324">In the final step, you're prompted to delete the job and the pool that were created by the DotNetTutorial application.</span></span> <span data-ttu-id="c624f-325">İşlerin ve görevlerin kendileri için sizden ücret alınmasa da işlem düğümleri için *ücret alınır*.</span><span class="sxs-lookup"><span data-stu-id="c624f-325">Although you're not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="c624f-326">Bu nedenle, düğümleri yalnızca gerektiğinde ayırmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="c624f-326">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="c624f-327">Kullanılmayan havuzların silinmesi bakım işleminizin bir parçası olabilir.</span><span class="sxs-lookup"><span data-stu-id="c624f-327">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="c624f-328">BatchClient'ın [JobOperations][net_joboperations] ve [PoolOperations][net_pooloperations] öğelerinin her ikisine de, kullanıcının silmeyi onaylaması durumunda karşılık gelecek silme yöntemleri vardır:</span><span class="sxs-lookup"><span data-stu-id="c624f-328">The BatchClient's [JobOperations][net_joboperations] and [PoolOperations][net_pooloperations] both have corresponding deletion methods, which are called if the user confirms deletion:</span></span>

```csharp
// Clean up the resources we've created in the Batch account if the user so chooses
Console.WriteLine();
Console.WriteLine("Delete job? [yes] no");
string response = Console.ReadLine().ToLower();
if (response != "n" && response != "no")
{
    await batchClient.JobOperations.DeleteJobAsync(JobId);
}

Console.WriteLine("Delete pool? [yes] no");
response = Console.ReadLine();
if (response != "n" && response != "no")
{
    await batchClient.PoolOperations.DeletePoolAsync(PoolId);
}
```

> [!IMPORTANT]
> <span data-ttu-id="c624f-329">İşlem kaynaklarının ücretli olduğunu unutmayın; kullanılmayan havuzların silinmesi masrafları azaltacaktır.</span><span class="sxs-lookup"><span data-stu-id="c624f-329">Keep in mind that you are charged for compute resources—deleting unused pools will minimize cost.</span></span> <span data-ttu-id="c624f-330">Bunun yanı sıra, bir havuzun silinmesinin, bu havuz içindeki tüm işlem düğümlerini de sileceğini unutmayın; bu nedenle, düğümlerdeki veriler de havuz silindikten sonra kurtarılamayacaktır.</span><span class="sxs-lookup"><span data-stu-id="c624f-330">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on the nodes will be unrecoverable after the pool is deleted.</span></span>
>
>

## <a name="run-the-dotnettutorial-sample"></a><span data-ttu-id="c624f-331">*DotNetTutorial* örneğini çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c624f-331">Run the *DotNetTutorial* sample</span></span>
<span data-ttu-id="c624f-332">Örnek uygulamayı çalıştırdığınızda, konsol çıktısı aşağıdakine benzer.</span><span class="sxs-lookup"><span data-stu-id="c624f-332">When you run the sample application, the console output will be similar to the following.</span></span> <span data-ttu-id="c624f-333">Yürütme sırasında, havuzun işlem düğümleri başlatıldığı sırada `Awaiting task completion, timeout in 00:30:00...` öğesiyle karşılaşacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c624f-333">During execution, you will experience a pause at `Awaiting task completion, timeout in 00:30:00...` while the pool's compute nodes are started.</span></span> <span data-ttu-id="c624f-334">Havuzunuzu, işlem düğümlerinizi, işinizi ve görevlerinizi yürütme sırasında ve sonrasında izlemek için [Azure portalını][azure_portal] kullanın.</span><span class="sxs-lookup"><span data-stu-id="c624f-334">Use the [Azure portal][azure_portal] to monitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="c624f-335">Uygulamanın oluşturduğu Depolama kaynaklarını (kapsayıcılar ve bloblar) görüntülemek için [Azure portalını][azure_portal] veya [Azure Depolama Gezgini’ni][storage_explorers] kullanın.</span><span class="sxs-lookup"><span data-stu-id="c624f-335">Use the [Azure portal][azure_portal] or the [Azure Storage Explorer][storage_explorers] to view the Storage resources (containers and blobs) that are created by the application.</span></span>

<span data-ttu-id="c624f-336">Varsayılan yapılandırmasında uygulama çalıştırıldığında tipik yürütme süresi **yaklaşık 5 dakikadır**.</span><span class="sxs-lookup"><span data-stu-id="c624f-336">Typical execution time is **approximately 5 minutes** when you run the application in its default configuration.</span></span>

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe to container [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll to container [application]...
Uploading file ..\..\taskdata1.txt to container [input]...
Uploading file ..\..\taskdata2.txt to container [input]...
Uploading file ..\..\taskdata3.txt to container [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks to job [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within the specified timeout period.
Downloading all files from container [output]...
All files downloaded to C:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="c624f-337">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c624f-337">Next steps</span></span>
<span data-ttu-id="c624f-338">Farklı işlem senaryolarıyla denemeler yapmak için *DotNetTutorial* ve *TaskApplication* öğelerinde değişiklik yapmaktan çekinmeyin.</span><span class="sxs-lookup"><span data-stu-id="c624f-338">Feel free to make changes to *DotNetTutorial* and *TaskApplication* to experiment with different compute scenarios.</span></span> <span data-ttu-id="c624f-339">Örneğin, uzun soluklu görevlerin benzetimini gerçekleştirmek ve bunları portalda izlemek için [Thread.Sleep][net_thread_sleep] ile olduğu gibi *TaskApplication*’a bir yürütme gecikmesi eklemeye çalışın.</span><span class="sxs-lookup"><span data-stu-id="c624f-339">For example, try adding an execution delay to *TaskApplication*, such as with [Thread.Sleep][net_thread_sleep], to simulate long-running tasks and monitor them in the portal.</span></span> <span data-ttu-id="c624f-340">Daha fazla görev eklemeye veya işlem düğüm sayısını ayarlamaya çalışın.</span><span class="sxs-lookup"><span data-stu-id="c624f-340">Try adding more tasks or adjusting the number of compute nodes.</span></span> <span data-ttu-id="c624f-341">Yürütme süresini hızlandırmak için mevcut havuzun kullanımını denetleyip izin vermek için mantık ekleyin (*ipucu*: [azure-batch-samples][github_samples] içindeki [Microsoft.Azure.Batch.Samples.Common][github_samples_common] projesinde `ArticleHelpers.cs` öğesini kullanıma alın).</span><span class="sxs-lookup"><span data-stu-id="c624f-341">Add logic to check for and allow the use of an existing pool to speed execution time (*hint*: check out `ArticleHelpers.cs` in the [Microsoft.Azure.Batch.Samples.Common][github_samples_common] project in [azure-batch-samples][github_samples]).</span></span>

<span data-ttu-id="c624f-342">Batch çözümünün temel iş akışı hakkında artık bilginiz olduğuna göre, Batch hizmetinin ek özelliklerinin derinliklerine dalma zamanı gelmiştir.</span><span class="sxs-lookup"><span data-stu-id="c624f-342">Now that you're familiar with the basic workflow of a Batch solution, it's time to dig in to the additional features of the Batch service.</span></span>

* <span data-ttu-id="c624f-343">Hizmetle yeni tanışıyorsanız önerdiğimiz [Azure Batch özelliklerine genel bakış](batch-api-basics.md) makalesini gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="c624f-343">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span></span>
* <span data-ttu-id="c624f-344">[Batch öğrenme yolu][batch_learning_path]’ndaki **Ayrıntılı geliştirme** altında diğer Batch geliştirmesi makalelerine başlayın.</span><span class="sxs-lookup"><span data-stu-id="c624f-344">Start on the other Batch development articles under **Development in-depth** in the [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="c624f-345">[TopNWords][github_topnwords] örneğinde Batch tarafından kullanılan "ilk N sözcük" iş yükünü işlemenin farklı uygulamalarını kullanıma alın.</span><span class="sxs-lookup"><span data-stu-id="c624f-345">Check out a different implementation of processing the "top N words" workload by using Batch in the [TopNWords][github_topnwords] sample.</span></span>
* <span data-ttu-id="c624f-346">Kitaplıktaki son değişiklikler için Batch .NET [sürüm notlarını](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) inceleyin.</span><span class="sxs-lookup"><span data-stu-id="c624f-346">Review the Batch .NET [release notes](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) for the latest changes in the library.</span></span>

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[github_dotnettutorial]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/DotNetTutorial
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_common]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/Common
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[net_api]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[net_api_storage]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudblobclient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobclient.aspx
[net_cloudblobcontainer]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudserviceconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudserviceconfiguration.aspx
[net_container_delete]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.deleteifexistsasync.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_poolinfo]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.protocol.models.cloudjob.poolinformation.aspx
[net_joboperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.joboperations
[net_joboperations_terminatejob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_jobpreptask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_jobreltask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_odatadetaillevel]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_pooloperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.pooloperations
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_resourcefile_blobsource]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.blobsource.aspx
[net_sas_blob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblob.getsharedaccesssignature.aspx
[net_sas_container]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblobcontainer.getsharedaccesssignature.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.resourcefiles.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_task_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.resourcefiles.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_taskstatemonitor]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskstatemonitor.aspx
[net_thread_sleep]: https://msdn.microsoft.com/library/274eh01d(v=vs.110).aspx
[net_virtualmachineconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.virtualmachineconfiguration.aspx
[nuget_packagemgr]: https://docs.nuget.org/consume/installing-nuget
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build
[storage_explorers]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/vs/
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-dotnet-get-started/batch_workflow_01_sm.png "Azure Depolama’da kapsayıcı oluşturma"
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "Görev uygulamasını ve girdi (veriler) dosyalarını kapsayıcılara yükleme"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Batch havuzu oluşturma"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Batch işi oluşturma"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "İşe görev ekleme"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "Görevleri izleme"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Depolama’dan görev çıkışını indirme"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Batch çözümü iş akışı (tam diyagram)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "Portalda Batch kimlik bilgileri"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "Portalda Depolama kimlik bilgileri"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Batch çözümü iş akışı (minimal diyagram)"
