---
title: "aaaTutorial - .NET için kullanım hello Azure Batch istemci kitaplığı | Microsoft Docs"
description: "Azure Batch temel kavramlarını Hello öğrenin ve .NET kullanarak basit bir çözüm oluşturun."
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
ms.openlocfilehash: 06062b3886a8081bd9a831824a981503ef55f9b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-building-solutions-with-hello-batch-client-library-for-net"></a><span data-ttu-id="03e35-103">.NET için hello toplu istemci kitaplığı ile çözümler derleme kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="03e35-103">Get started building solutions with hello Batch client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="03e35-104">.NET</span><span class="sxs-lookup"><span data-stu-id="03e35-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="03e35-105">Python</span><span class="sxs-lookup"><span data-stu-id="03e35-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="03e35-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="03e35-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="03e35-107">Merhaba temel bilgileri öğrenmek [Azure Batch] [ azure_batch] ve hello [Batch .NET] [ net_api] kitaplığı bu makalede bir C# örnek uygulama adımı tarafından aşağıdakiler ele gibi adım.</span><span class="sxs-lookup"><span data-stu-id="03e35-107">Learn hello basics of [Azure Batch][azure_batch] and hello [Batch .NET][net_api] library in this article as we discuss a C# sample application step by step.</span></span> <span data-ttu-id="03e35-108">Biz Merhaba örnek uygulaması hello Batch hizmeti tooprocess nasıl geliştirdiğini de paralel iş yükünü hello Bulut ve onu ile nasıl etkileşim kurduğu bakın [Azure Storage](../storage/common/storage-introduction.md) dosya hazırlığı ve alımı için.</span><span class="sxs-lookup"><span data-stu-id="03e35-108">We look at how hello sample application leverages hello Batch service tooprocess a parallel workload in hello cloud, and how it interacts with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="03e35-109">Ortak Batch uygulama iş akışı öğrenin ve hello başlıca Batch bileşenleri işler, görevler, havuzlar gibi temel bir anlayış edinmek ve işlem düğümleri.</span><span class="sxs-lookup"><span data-stu-id="03e35-109">You'll learn a common Batch application workflow and gain a base understanding of hello major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="03e35-110">![Batch çözümü iş akışı (temel)][11]</span><span class="sxs-lookup"><span data-stu-id="03e35-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="03e35-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="03e35-111">Prerequisites</span></span>
<span data-ttu-id="03e35-112">Bu makalede, C# ve Visual Studio deneyimine sahip olduğunuz varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="03e35-112">This article assumes that you have a working knowledge of C# and Visual Studio.</span></span> <span data-ttu-id="03e35-113">Aşağıda Azure ve hello toplu işlem ve depolama hizmetleri için belirtilen mümkün toosatisfy hello hesap oluşturma gerekliliklerini olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="03e35-113">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="03e35-114">Hesaplar</span><span class="sxs-lookup"><span data-stu-id="03e35-114">Accounts</span></span>
* <span data-ttu-id="03e35-115">**Azure hesabı**: Henüz bir Azure aboneliğiniz yoksa, [ücretsiz Azure hesabı oluşturun][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="03e35-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="03e35-116">**Batch hesabı**: Azure aboneliğiniz olduktan sonra, [Azure Batch hesabı oluşturun](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="03e35-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="03e35-117">**Storage hesabı**: Bkz. [Azure Storage hesapları hakkında](../storage/common/storage-create-storage-account.md) sayfası, [Storage hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) bölümü.</span><span class="sxs-lookup"><span data-stu-id="03e35-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="03e35-118">Batch şu anda destekler *yalnızca* hello **genel amaçlı** #5. adımda açıklandığı gibi depolama hesabı türü, [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) içinde [Azure hakkında Depolama hesapları](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="03e35-118">Batch currently supports *only* hello **general-purpose** storage account type, as described in step #5 [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

### <a name="visual-studio"></a><span data-ttu-id="03e35-119">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="03e35-119">Visual Studio</span></span>
<span data-ttu-id="03e35-120">Bilmeniz gereken **Visual Studio 2015 veya daha yeni** toobuild hello örnek proje.</span><span class="sxs-lookup"><span data-stu-id="03e35-120">You must have **Visual Studio 2015 or newer** toobuild hello sample project.</span></span> <span data-ttu-id="03e35-121">Visual Studio'nun Ücretsiz ve deneme sürümlerini hello bulabilirsiniz [Visual Studio ürün genel bakış][visual_studio].</span><span class="sxs-lookup"><span data-stu-id="03e35-121">You can find free and trial versions of Visual Studio in hello [overview of Visual Studio products][visual_studio].</span></span>

### <a name="dotnettutorial-code-sample"></a><span data-ttu-id="03e35-122">*DotNetTutorial* kodu örneği</span><span class="sxs-lookup"><span data-stu-id="03e35-122">*DotNetTutorial* code sample</span></span>
<span data-ttu-id="03e35-123">Merhaba [DotNetTutorial] [ github_dotnettutorial] örnek birçok Batch kod örnekleri bulunan hello hello biridir [azure-batch-samples] [ github_samples] havuzda GitHub.</span><span class="sxs-lookup"><span data-stu-id="03e35-123">hello [DotNetTutorial][github_dotnettutorial] sample is one of hello many Batch code samples found in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="03e35-124">Tüm hello örnekleri tıklayarak indirebileceğiniz **Kopyala veya indir > ZIP'i indir** hello depo giriş sayfasındaki veya hello tıklatarak [azure-batch-samples-master.zip] [ github_samples_zip]doğrudan indirme bağlantısına.</span><span class="sxs-lookup"><span data-stu-id="03e35-124">You can download all hello samples by clicking  **Clone or download > Download ZIP** on hello repository home page, or by clicking hello [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="03e35-125">Merhaba hello ZIP dosyasının içeriğini ayıkladıktan sonra klasör aşağıdaki hello hello çözüm bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="03e35-125">Once you've extracted hello contents of hello ZIP file, you can find hello solution in hello following folder:</span></span>

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a><span data-ttu-id="03e35-126">Azure Batch Gezgini (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="03e35-126">Azure Batch Explorer (optional)</span></span>
<span data-ttu-id="03e35-127">Merhaba [Azure Batch Gezgini] [ github_batchexplorer] hello dahil ücretsiz bir yardımcı programdır [azure-batch-samples] [ github_samples] github'daki.</span><span class="sxs-lookup"><span data-stu-id="03e35-127">hello [Azure Batch Explorer][github_batchexplorer] is a free utility that is included in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="03e35-128">Gerekli değil toocomplete sırasında Bu öğretici, geliştirirken ve Batch çözümlerinizi hatalarını ayıklarken yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="03e35-128">While not required toocomplete this tutorial, it can be useful while developing and debugging your Batch solutions.</span></span>

## <a name="dotnettutorial-sample-project-overview"></a><span data-ttu-id="03e35-129">DotNetTutorial örnek projesine genel bakış</span><span class="sxs-lookup"><span data-stu-id="03e35-129">DotNetTutorial sample project overview</span></span>
<span data-ttu-id="03e35-130">Merhaba *DotNetTutorial* kod örneği buradaki iki projeden oluşan bir Visual Studio çözümü: **DotNetTutorial** ve **TaskApplication**.</span><span class="sxs-lookup"><span data-stu-id="03e35-130">hello *DotNetTutorial* code sample is a Visual Studio solution that consists of two projects: **DotNetTutorial** and **TaskApplication**.</span></span>

* <span data-ttu-id="03e35-131">**DotNetTutorial** (sanal makineler) işlem düğümlerinde paralel iş yükünü hello toplu işlem ve depolama hizmetleri tooexecute ile etkileşim kuran hello istemci uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="03e35-131">**DotNetTutorial** is hello client application that interacts with hello Batch and Storage services tooexecute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="03e35-132">DotNetTutorial yerel iş istasyonunuzda çalışır.</span><span class="sxs-lookup"><span data-stu-id="03e35-132">DotNetTutorial runs on your local workstation.</span></span>
* <span data-ttu-id="03e35-133">**TaskApplication** Azure tooperform hello asıl işi işlem düğümlerinde çalışan hello programdır.</span><span class="sxs-lookup"><span data-stu-id="03e35-133">**TaskApplication** is hello program that runs on compute nodes in Azure tooperform hello actual work.</span></span> <span data-ttu-id="03e35-134">Merhaba örnekteki `TaskApplication.exe` hello metni (girdi dosyası hello) Azure Storage'dan indirilen dosyada ayrıştırıyor.</span><span class="sxs-lookup"><span data-stu-id="03e35-134">In hello sample, `TaskApplication.exe` parses hello text in a file downloaded from Azure Storage (hello input file).</span></span> <span data-ttu-id="03e35-135">Bir metin dosyası oluşturur sonra (Merhaba çıktı dosyası) hello giriş dosyasında görünen hello ilk üç sözcük listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="03e35-135">Then it produces a text file (hello output file) that contains a list of hello top three words that appear in hello input file.</span></span> <span data-ttu-id="03e35-136">Merhaba çıktı dosyasını oluşturduktan sonra TaskApplication hello dosya tooAzure depolama yükler.</span><span class="sxs-lookup"><span data-stu-id="03e35-136">After it creates hello output file, TaskApplication uploads hello file tooAzure Storage.</span></span> <span data-ttu-id="03e35-137">Bu yükleme için kullanılabilir toohello istemci uygulaması hale getirir.</span><span class="sxs-lookup"><span data-stu-id="03e35-137">This makes it available toohello client application for download.</span></span> <span data-ttu-id="03e35-138">TaskApplication hello Batch hizmeti birden çok işlem düğümünde paralel olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="03e35-138">TaskApplication runs in parallel on multiple compute nodes in hello Batch service.</span></span>

<span data-ttu-id="03e35-139">Merhaba Aşağıdaki diyagramda gösterilmektedir hello istemci uygulaması tarafından gerçekleştirilen birincil işlemleri hello *DotNetTutorial*ve hello görevler tarafından yürütülen hello uygulama *TaskApplication*.</span><span class="sxs-lookup"><span data-stu-id="03e35-139">hello following diagram illustrates hello primary operations that are performed by hello client application, *DotNetTutorial*, and hello application that is executed by hello tasks, *TaskApplication*.</span></span> <span data-ttu-id="03e35-140">Bu temel iş akışı, Batch’le oluşturulan çok sayıda işlem çözümünün tipik halidir.</span><span class="sxs-lookup"><span data-stu-id="03e35-140">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="03e35-141">Bu her özelliğe hello Batch hizmeti uygun olmadığı belirtilirken, neredeyse her Batch senaryosu iş akışının bölümlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="03e35-141">While it does not demonstrate every feature available in hello Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="03e35-142">![Batch örnek iş akışı][8]</span><span class="sxs-lookup"><span data-stu-id="03e35-142">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="03e35-143">**1. Adım.**</span><span class="sxs-lookup"><span data-stu-id="03e35-143">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="03e35-144">Azure Blob Storage’da **kapsayıcılar** oluşturun.</span><span class="sxs-lookup"><span data-stu-id="03e35-144">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="03e35-145">
[**2. Adım.**](#step-2-upload-task-application-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="03e35-145">
[**Step 2.**](#step-2-upload-task-application-and-data-files)</span></span> <span data-ttu-id="03e35-146">Karşıya yükleme görev uygulaması dosyalarını ve girdi dosyalarını toocontainers.</span><span class="sxs-lookup"><span data-stu-id="03e35-146">Upload task application files and input files toocontainers.</span></span><br/><span data-ttu-id="03e35-147">
[**3. Adım.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="03e35-147">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="03e35-148">Batch **havuzu** oluşturun.</span><span class="sxs-lookup"><span data-stu-id="03e35-148">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="03e35-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="03e35-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="03e35-150">Merhaba havuzu **StartTask** yüklemeleri hello görev ikili dosyalarını (TaskApplication) toonodes hello havuzuna Katıl gibi.</span><span class="sxs-lookup"><span data-stu-id="03e35-150">hello pool **StartTask** downloads hello task binary files (TaskApplication) toonodes as they join hello pool.</span></span><br/><span data-ttu-id="03e35-151">
[**4. Adım.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="03e35-151">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="03e35-152">Batch **işi** oluşturun.</span><span class="sxs-lookup"><span data-stu-id="03e35-152">Create a Batch **job**.</span></span><br/><span data-ttu-id="03e35-153">
[**5. Adım**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="03e35-153">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="03e35-154">Ekleme **görevleri** toohello işi.</span><span class="sxs-lookup"><span data-stu-id="03e35-154">Add **tasks** toohello job.</span></span><br/>
  <span data-ttu-id="03e35-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="03e35-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="03e35-156">Merhaba, düğümlerde zamanlanmış tooexecute görevlerdir.</span><span class="sxs-lookup"><span data-stu-id="03e35-156">hello tasks are scheduled tooexecute on nodes.</span></span><br/>
    <span data-ttu-id="03e35-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="03e35-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="03e35-158">Her görev kendi girdi verilerini Azure Storage’dan indirip yürütmeye başlar.</span><span class="sxs-lookup"><span data-stu-id="03e35-158">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="03e35-159">
[**6. Adım**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="03e35-159">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="03e35-160">Görevleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="03e35-160">Monitor tasks.</span></span><br/>
  <span data-ttu-id="03e35-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="03e35-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="03e35-162">Görevlerin tamamlanmasıyla, kendi çıktı veri tooAzure depolama karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="03e35-162">As tasks are completed, they upload their output data tooAzure Storage.</span></span><br/><span data-ttu-id="03e35-163">
[**7. Adım**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="03e35-163">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="03e35-164">Storage’dan görev çıktısını indirin.</span><span class="sxs-lookup"><span data-stu-id="03e35-164">Download task output from Storage.</span></span>

<span data-ttu-id="03e35-165">Belirtildiği gibi her Batch çözümü tam adımları gerçekleştirir ve çok daha fazlasını içerir, ancak hello *DotNetTutorial* örnek uygulaması Batch çözümde bulunan ortak işlemleri göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="03e35-165">As mentioned, not every Batch solution performs these exact steps, and may include many more, but hello *DotNetTutorial* sample application demonstrates common processes found in a Batch solution.</span></span>

## <a name="build-hello-dotnettutorial-sample-project"></a><span data-ttu-id="03e35-166">Merhaba yapı *DotNetTutorial* örnek proje</span><span class="sxs-lookup"><span data-stu-id="03e35-166">Build hello *DotNetTutorial* sample project</span></span>
<span data-ttu-id="03e35-167">Merhaba örnek başarıyla çalıştırabilmeniz için önce Batch ve Storage hesabı kimlik bilgileri hello belirtmelisiniz *DotNetTutorial* projenin `Program.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="03e35-167">Before you can successfully run hello sample, you must specify both Batch and Storage account credentials in hello *DotNetTutorial* project's `Program.cs` file.</span></span> <span data-ttu-id="03e35-168">Henüz yapmadıysanız, hello çözümü Visual Studio'da hello çift tıklatarak açın `DotNetTutorial.sln` çözüm dosyası.</span><span class="sxs-lookup"><span data-stu-id="03e35-168">If you have not done so already, open hello solution in Visual Studio by double-clicking hello `DotNetTutorial.sln` solution file.</span></span> <span data-ttu-id="03e35-169">Veya ondan hello kullanarak Visual Studio'da açın **Dosya > Aç > Proje/çözüm** menüsü.</span><span class="sxs-lookup"><span data-stu-id="03e35-169">Or open it from within Visual Studio by using hello **File > Open > Project/Solution** menu.</span></span>

<span data-ttu-id="03e35-170">Açık `Program.cs` hello içinde *DotNetTutorial* projesi.</span><span class="sxs-lookup"><span data-stu-id="03e35-170">Open `Program.cs` within hello *DotNetTutorial* project.</span></span> <span data-ttu-id="03e35-171">Daha sonra kimlik bilgilerinizi belirtildiği gibi hello dosyasının hello üstüne yakın ekleyin:</span><span class="sxs-lookup"><span data-stu-id="03e35-171">Then add your credentials as specified near hello top of hello file:</span></span>

```csharp
// Update hello Batch and Storage account credential strings below with hello values
// unique tooyour accounts. These are used when constructing connection strings
// for hello Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> <span data-ttu-id="03e35-172">Şu anda yukarıda belirtildiği gibi hello kimlik bilgilerini belirtmelisiniz bir **genel amaçlı** Azure depolama hesabında depolama.</span><span class="sxs-lookup"><span data-stu-id="03e35-172">As mentioned above, you must currently specify hello credentials for a **general-purpose** storage account in Azure Storage.</span></span> <span data-ttu-id="03e35-173">Toplu iş uygulamalarınız hello içinde blob storage kullanma **genel amaçlı** depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="03e35-173">Your Batch applications use blob storage within hello **general-purpose** storage account.</span></span> <span data-ttu-id="03e35-174">Merhaba seçerek oluşturulmuş bir depolama hesabı için Hello kimlik bilgilerini belirtmeyin *Blob storage* hesap türü.</span><span class="sxs-lookup"><span data-stu-id="03e35-174">Do not specify hello credentials for a Storage account that was created by selecting hello *Blob storage* account type.</span></span>
>
>

<span data-ttu-id="03e35-175">Batch ve Storage hesabı kimlik bilgilerinizi her hizmetin hesap dikey hello hello bulabilirsiniz [Azure portal][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="03e35-175">You can find your Batch and Storage account credentials within hello account blade of each service in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="03e35-176">![Merhaba portalda batch kimlik bilgileri][9]
![hello portalda Storage kimlik bilgileri][10]</span><span class="sxs-lookup"><span data-stu-id="03e35-176">![Batch credentials in hello portal][9]
![Storage credentials in hello portal][10]</span></span><br/>

<span data-ttu-id="03e35-177">Kimlik bilgilerinizle hello proje güncelleştirildi, Çözüm Gezgini'ndeki hello çözüme sağ tıklatın ve **yapı çözümü**.</span><span class="sxs-lookup"><span data-stu-id="03e35-177">Now that you've updated hello project with your credentials, right-click hello solution in Solution Explorer and click **Build Solution**.</span></span> <span data-ttu-id="03e35-178">İstenirse, herhangi bir NuGet paketinin geri yüklenmesi hello onaylayın.</span><span class="sxs-lookup"><span data-stu-id="03e35-178">Confirm hello restoration of any NuGet packages, if you're prompted.</span></span>

> [!TIP]
> <span data-ttu-id="03e35-179">Merhaba NuGet paketleri otomatik olarak geri yüklenmez veya bir hata toorestore hello paketlerle ilgili hatalar görürseniz, hello sahip olduğundan emin olun [NuGet Paket Yöneticisi] [ nuget_packagemgr] yüklü.</span><span class="sxs-lookup"><span data-stu-id="03e35-179">If hello NuGet packages are not automatically restored, or if you see errors about a failure toorestore hello packages, ensure that you have hello [NuGet Package Manager][nuget_packagemgr] installed.</span></span> <span data-ttu-id="03e35-180">Sonra da eksik paketleri hello indirilmesini etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="03e35-180">Then enable hello download of missing packages.</span></span> <span data-ttu-id="03e35-181">Bkz: [etkinleştirme paket geri yükleme sırasında yapı] [ nuget_restore] tooenable paket yükleme.</span><span class="sxs-lookup"><span data-stu-id="03e35-181">See [Enabling Package Restore During Build][nuget_restore] tooenable package download.</span></span>
>
>

<span data-ttu-id="03e35-182">Merhaba, aşağıdaki bölümlerde, biz Merhaba örnek uygulaması tooprocess gerçekleştirir hello adımları hello Batch hizmeti iş yükünü bölme ve bu adımlar üzerine ayrıntılı tartıştık.</span><span class="sxs-lookup"><span data-stu-id="03e35-182">In hello following sections, we break down hello sample application into hello steps that it performs tooprocess a workload in hello Batch service, and discuss those steps in detail.</span></span> <span data-ttu-id="03e35-183">Her hello örnek kod satırı ele alınan bu yana yolunuzu bu makalenin hello rest aracılığıyla çalışırken toorefer toohello açık çözümü Visual Studio'da öneririz.</span><span class="sxs-lookup"><span data-stu-id="03e35-183">We encourage you toorefer toohello open solution in Visual Studio while you work your way through hello rest of this article, since not every line of code in hello sample is discussed.</span></span>

<span data-ttu-id="03e35-184">Merhaba toohello üstündeki gidin `MainAsync` hello yönteminde *DotNetTutorial* projenin `Program.cs` toostart 1. adım ile dosya.</span><span class="sxs-lookup"><span data-stu-id="03e35-184">Navigate toohello top of hello `MainAsync` method in hello *DotNetTutorial* project's `Program.cs` file toostart with Step 1.</span></span> <span data-ttu-id="03e35-185">Her adım aşağıda kabaca yöntemini aşağıdaki şekilde hello ilerleyişini çağrıları sonra `MainAsync`.</span><span class="sxs-lookup"><span data-stu-id="03e35-185">Each step below then roughly follows hello progression of method calls in `MainAsync`.</span></span>

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="03e35-186">1. Adım: Storage kapsayıcıları oluşturma</span><span class="sxs-lookup"><span data-stu-id="03e35-186">Step 1: Create Storage containers</span></span>
<span data-ttu-id="03e35-187">![Azure Depolama'da kapsayıcı oluşturma][1]
</span><span class="sxs-lookup"><span data-stu-id="03e35-187">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="03e35-188">Azure Storage ilet etkileşimde bulunmak için Batch’te yerleşik destek bulunur.</span><span class="sxs-lookup"><span data-stu-id="03e35-188">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="03e35-189">Storage hesabınızdaki kapsayıcılar, Batch hesabınızda çalışan hello görevler için gerekli hello dosyaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="03e35-189">Containers in your Storage account will provide hello files needed by hello tasks that run in your Batch account.</span></span> <span data-ttu-id="03e35-190">Merhaba kapsayıcılara hello görevlerin oluşturduğu bir yerde toostore hello çıktı verilerini de sağlar.</span><span class="sxs-lookup"><span data-stu-id="03e35-190">hello containers also provide a place toostore hello output data that hello tasks produce.</span></span> <span data-ttu-id="03e35-191">ilk şey hello hello *DotNetTutorial* istemci uygulamasının yapacağı üç kapsayıcı oluşturmaktır [Azure Blob Storage](../storage/common/storage-introduction.md):</span><span class="sxs-lookup"><span data-stu-id="03e35-191">hello first thing hello *DotNetTutorial* client application does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md):</span></span>

* <span data-ttu-id="03e35-192">**Uygulama**: Bu kapsayıcı hello görevlerin yanı sıra DLL'ler gibi birçok bağlantının tarafından çalıştırılan hello uygulamayı da depolar.</span><span class="sxs-lookup"><span data-stu-id="03e35-192">**application**: This container will store hello application run by hello tasks, as well as any of its dependencies, such as DLLs.</span></span>
* <span data-ttu-id="03e35-193">**Giriş**: görevler hello hello veri dosyaları tooprocess yükleyecek *giriş* kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="03e35-193">**input**: Tasks will download hello data files tooprocess from hello *input* container.</span></span>
* <span data-ttu-id="03e35-194">**Çıktı**: görevler girdi dosyası işlemeyi tamamladıklarında hello sonuçları toohello karşıya yükleyecek *çıkış* kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="03e35-194">**output**: When tasks complete input file processing, they will upload hello results toohello *output* container.</span></span>

<span data-ttu-id="03e35-195">Sipariş toointeract bir depolama hesabı ve kapsayıcı, oluşturma hello kullanırız [.NET için Azure Storage istemci Kitaplığı][net_api_storage].</span><span class="sxs-lookup"><span data-stu-id="03e35-195">In order toointeract with a Storage account and create containers, we use hello [Azure Storage Client Library for .NET][net_api_storage].</span></span> <span data-ttu-id="03e35-196">Bir başvuru toohello hesabıyla oluşturuyoruz [CloudStorageAccount][net_cloudstorageaccount]ve oluşturan bir [CloudBlobClient][net_cloudblobclient]:</span><span class="sxs-lookup"><span data-stu-id="03e35-196">We create a reference toohello account with [CloudStorageAccount][net_cloudstorageaccount], and from that create a [CloudBlobClient][net_cloudblobclient]:</span></span>

```csharp
// Construct hello Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve hello storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create hello blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

<span data-ttu-id="03e35-197">Merhaba kullanırız `blobClient` başvuru hello uygulama genelinde ve tooseveral yöntemleri parametre olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="03e35-197">We use hello `blobClient` reference throughout hello application and pass it as a parameter tooseveral methods.</span></span> <span data-ttu-id="03e35-198">Bu, burada diyoruz hello yukarıdaki hemen izleyen hello kod bloğunda örneğidir `CreateContainerIfNotExistAsync` tooactually Merhaba kapsayıcılara oluşturun.</span><span class="sxs-lookup"><span data-stu-id="03e35-198">An example of this is in hello code block that immediately follows hello above, where we call `CreateContainerIfNotExistAsync` tooactually create hello containers.</span></span>

```csharp
// Use hello blob client toocreate hello containers in Azure Storage if they don't
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

<span data-ttu-id="03e35-199">Merhaba kapsayıcılara oluşturduktan sonra Merhaba uygulaması artık hello görevler tarafından kullanılacak hello dosyaları karşıya yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="03e35-199">Once hello containers have been created, hello application can now upload hello files that will be used by hello tasks.</span></span>

> [!TIP]
> <span data-ttu-id="03e35-200">[Nasıl toouse Blob depolama alanından .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) Azure Storage kapsayıcıları ve blob'larla çalışma hakkında kapsamlı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="03e35-200">[How toouse Blob Storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="03e35-201">Batch ile çalışmaya başladığınızda okuma listenizin hello yukarıya yakın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="03e35-201">It should be near hello top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-application-and-data-files"></a><span data-ttu-id="03e35-202">2. Adım: Görev uygulamasını ve veri dosyalarını karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="03e35-202">Step 2: Upload task application and data files</span></span>
<span data-ttu-id="03e35-203">![Karşıya yükleme görev uygulamasını ve girdi (veri) toocontainers dosyaları][2]
</span><span class="sxs-lookup"><span data-stu-id="03e35-203">![Upload task application and input (data) files toocontainers][2]
</span></span><br/>

<span data-ttu-id="03e35-204">Merhaba dosyayı karşıya yükleme işlemi, *DotNetTutorial* ilk tanımlar **uygulama** ve **giriş** hello yerel makinede oldukları gibi dosya yolları.</span><span class="sxs-lookup"><span data-stu-id="03e35-204">In hello file upload operation, *DotNetTutorial* first defines collections of **application** and **input** file paths as they exist on hello local machine.</span></span> <span data-ttu-id="03e35-205">Sonra hello önceki adımda oluşturduğunuz bu dosyaları toohello kapsayıcıları yükler.</span><span class="sxs-lookup"><span data-stu-id="03e35-205">Then it uploads these files toohello containers that you created in hello previous step.</span></span>

```csharp
// Paths toohello executable and its dependencies that will be executed by hello tasks
List<string> applicationFilePaths = new List<string>
{
    // hello DotNetTutorial project includes a project reference tooTaskApplication,
    // allowing us toodetermine hello path of hello task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// hello collection of data files that are toobe processed by hello tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload hello application and its dependencies tooAzure Storage. This is the
// application that will process hello data files, and will be executed by each
// of hello tasks on hello compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload hello data files. This is hello data that will be processed by each of
// hello tasks that are executed on hello compute nodes within hello pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

<span data-ttu-id="03e35-206">İçinde iki yöntem vardır `Program.cs` hello karşıya yükleme işlemini oluşturan:</span><span class="sxs-lookup"><span data-stu-id="03e35-206">There are two methods in `Program.cs` that are involved in hello upload process:</span></span>

* <span data-ttu-id="03e35-207">`UploadFilesToContainerAsync`: Bu yöntem koleksiyonu döndürür [ResourceFile] [ net_resourcefile] (aşağıda açıklanmıştır) nesneleri ve dahili olarak çağrıları `UploadFileToContainerAsync` dosya almak için diğer bir deyişle, her tooupload geçirilen hello *filePaths* parametresi.</span><span class="sxs-lookup"><span data-stu-id="03e35-207">`UploadFilesToContainerAsync`: This method returns a collection of [ResourceFile][net_resourcefile] objects (discussed below) and internally calls `UploadFileToContainerAsync` tooupload each file that is passed in hello *filePaths* parameter.</span></span>
* <span data-ttu-id="03e35-208">`UploadFileToContainerAsync`: Bu, aslında hello dosyayı karşıya yüklemeyi gerçekleştiren ve hello oluşturan hello yöntemdir [ResourceFile] [ net_resourcefile] nesneleri.</span><span class="sxs-lookup"><span data-stu-id="03e35-208">`UploadFileToContainerAsync`: This is hello method that actually performs hello file upload and creates hello [ResourceFile][net_resourcefile] objects.</span></span> <span data-ttu-id="03e35-209">Merhaba dosyayı karşıya yükledikten sonra bu hello dosya için paylaşılan erişim imzası (SAS) alır ve temsil ettiği bir ResourceFile nesnesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="03e35-209">After uploading hello file, it obtains a shared access signature (SAS) for hello file and returns a ResourceFile object that represents it.</span></span> <span data-ttu-id="03e35-210">Paylaşılan erişim imzaları aşağıda da açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="03e35-210">Shared access signatures are also discussed below.</span></span>

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} toocontainer [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set hello expiry time and permissions for hello blob shared access signature.
        // In this case, no start time is specified, so hello shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct hello SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a><span data-ttu-id="03e35-211">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="03e35-211">ResourceFiles</span></span>
<span data-ttu-id="03e35-212">A [ResourceFile] [ net_resourcefile] hello URL tooa indirilen tooa Azure depolama alanı dosyasında toplu görevlerle işlem düğümü, görev çalıştırılmadan önce sağlar.</span><span class="sxs-lookup"><span data-stu-id="03e35-212">A [ResourceFile][net_resourcefile] provides tasks in Batch with hello URL tooa file in Azure Storage that is downloaded tooa compute node before that task is run.</span></span> <span data-ttu-id="03e35-213">Merhaba [ResourceFile.BlobSource] [ net_resourcefile_blobsource] özelliği, Azure Storage'da yer aldığından hello hello dosyanın tam URL'sini belirtir.</span><span class="sxs-lookup"><span data-stu-id="03e35-213">hello [ResourceFile.BlobSource][net_resourcefile_blobsource] property specifies hello full URL of hello file as it exists in Azure Storage.</span></span> <span data-ttu-id="03e35-214">Merhaba URL ayrıca güvenli erişim toohello dosya sağlayan bir paylaşılan erişim imzası (SAS) içerebilir.</span><span class="sxs-lookup"><span data-stu-id="03e35-214">hello URL may also include a shared access signature (SAS) that provides secure access toohello file.</span></span> <span data-ttu-id="03e35-215">Batch .NET’teki çoğu görev türünde *ResourceFiles* özelliği vardır; bu özellikte şunlar bulunur:</span><span class="sxs-lookup"><span data-stu-id="03e35-215">Most tasks types within Batch .NET include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="03e35-216">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="03e35-216">[CloudTask][net_task]</span></span>
* <span data-ttu-id="03e35-217">[StartTask][net_pool_starttask]</span><span class="sxs-lookup"><span data-stu-id="03e35-217">[StartTask][net_pool_starttask]</span></span>
* <span data-ttu-id="03e35-218">[JobPreparationTask][net_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="03e35-218">[JobPreparationTask][net_jobpreptask]</span></span>
* <span data-ttu-id="03e35-219">[JobReleaseTask][net_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="03e35-219">[JobReleaseTask][net_jobreltask]</span></span>

<span data-ttu-id="03e35-220">DotNetTutorial örnek uygulaması Hello hello JobPreparationTask veya JobReleaseTask görev türlerini kullanmaz, ancak daha fazla bilgiyi ilgili [iş hazırlama ve tamamlama görevlerini çalıştırma Azure Batch işlem düğümlerinde](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="03e35-220">hello DotNetTutorial sample application does not use hello JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="03e35-221">Paylaşılan erişim imzası (SAS)</span><span class="sxs-lookup"><span data-stu-id="03e35-221">Shared access signature (SAS)</span></span>
<span data-ttu-id="03e35-222">Paylaşılan erişim imzalar dizelerdir — bir URL bir parçası olarak dahil olduğunda — güvenli erişim toocontainers ve Azure Storage blobları sağlar.</span><span class="sxs-lookup"><span data-stu-id="03e35-222">Shared access signatures are strings which—when included as part of a URL—provide secure access toocontainers and blobs in Azure Storage.</span></span> <span data-ttu-id="03e35-223">Merhaba DotNetTutorial uygulaması hem blob kullanır ve kapsayıcı paylaşılan erişim imzası URL'lerini ve nasıl tooobtain bu paylaşılan erişim imzası dizeleri depolama hizmeti hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="03e35-223">hello DotNetTutorial application uses both blob and container shared access signature URLs, and demonstrates how tooobtain these shared access signature strings from hello Storage service.</span></span>

* <span data-ttu-id="03e35-224">**Blob paylaşılan erişim imzaları**: DotNetTutorial hello havuza ait StartTask, Storage'dan hello uygulama ikililerini ve girdi veri dosyalarını indirdiğinde blob paylaşılan erişim imzalarını kullanır (3. adım aşağıya bakın).</span><span class="sxs-lookup"><span data-stu-id="03e35-224">**Blob shared access signatures**: hello pool's StartTask in DotNetTutorial uses blob shared access signatures when it downloads hello application binaries and input data files from Storage (see Step #3 below).</span></span> <span data-ttu-id="03e35-225">Merhaba `UploadFileToContainerAsync` Dotnettutorial'in yönteminde `Program.cs` her blob'un paylaşılan erişim imzasını alan hello kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="03e35-225">hello `UploadFileToContainerAsync` method in DotNetTutorial's `Program.cs` contains hello code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="03e35-226">Bu işlemi [CloudBlob.GetSharedAccessSignature][net_sas_blob] çağırarak gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="03e35-226">It does so by calling [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span></span>
* <span data-ttu-id="03e35-227">**Kapsayıcı paylaşılan erişim imzaları**: her görev hello işlem düğümü işini bitirdiğinde, kendi çıktı dosyasını toohello yükler *çıkış* Azure storage'da kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="03e35-227">**Container shared access signatures**: As each task finishes its work on hello compute node, it uploads its output file toohello *output* container in Azure Storage.</span></span> <span data-ttu-id="03e35-228">toodo, TaskApplication hello dosyayı karşıya yüklediğinde hello yolu bir parçası olarak yazma erişimi toohello kapsayıcı sağlayan kapsayıcı paylaşılan erişim imzasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="03e35-228">toodo so, TaskApplication uses a container shared access signature that provides write access toohello container as part of hello path when it uploads hello file.</span></span> <span data-ttu-id="03e35-229">Alma hello kapsayıcı paylaşılan erişim imzası zaman erişim imzası alma hello blob paylaşılan olarak benzer bir şekilde gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="03e35-229">Obtaining hello container shared access signature is done in a similar fashion as when obtaining hello blob shared access signature.</span></span> <span data-ttu-id="03e35-230">DotNetTutorial ' Bu hello bulacaksınız `GetContainerSasUrl` yardımcı yöntem çağrılarını [CloudBlobContainer.GetSharedAccessSignature] [ net_sas_container] toodo şekilde.</span><span class="sxs-lookup"><span data-stu-id="03e35-230">In DotNetTutorial, you will find that hello `GetContainerSasUrl` helper method calls [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] toodo so.</span></span> <span data-ttu-id="03e35-231">Okuyacaksınız TaskApplication hello kapsayıcı nasıl kullandığı hakkında daha fazla paylaşılan erişim imzasını "6. adım: izleme görevleri."</span><span class="sxs-lookup"><span data-stu-id="03e35-231">You'll read more about how TaskApplication uses hello container shared access signature in "Step 6: Monitor Tasks."</span></span>

> [!TIP]
> <span data-ttu-id="03e35-232">Hello iki parçalı seriyi kullanıma paylaşılan erişim imzalarındaki [Kısım 1: paylaşılan erişim imzası (SAS) modelini anlama hello](../storage/common/storage-dotnet-shared-access-signature-part-1.md) ve [2. parça: oluşturma ve paylaşılan erişim imzası (SAS) ileBlobstoragekullanma](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn depolama hesabınızdaki toodata güvenli erişim sağlama hakkında daha fazla.</span><span class="sxs-lookup"><span data-stu-id="03e35-232">Check out hello two-part series on shared access signatures, [Part 1: Understanding hello shared access signature (SAS) model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a shared access signature (SAS) with Blob storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn more about providing secure access toodata in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="03e35-233">3. Adım: Batch havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="03e35-233">Step 3: Create Batch pool</span></span>
<span data-ttu-id="03e35-234">![Batch havuzu oluşturma][3]
</span><span class="sxs-lookup"><span data-stu-id="03e35-234">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="03e35-235">Batch **havuzu**, Batch’in işe ait görevleri yürüttüğü işlem düğümlerinin (sanal makineler) koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="03e35-235">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="03e35-236">Merhaba uygulama ve veri dosyalarını toohello depolama hesabı Azure depolama API'leri ile karşıya yüklenmesini sonra *DotNetTutorial* hello Batch .NET kitaplığı tarafından sağlanan API'leri ile çağrıları toohello Batch hizmeti yapmadan başlar.</span><span class="sxs-lookup"><span data-stu-id="03e35-236">After uploading hello application and data files toohello Storage account with Azure Storage APIs, *DotNetTutorial* begins making calls toohello Batch service with APIs provided by hello Batch .NET library.</span></span> <span data-ttu-id="03e35-237">Merhaba kod ilk oluşturur bir [BatchClient][net_batchclient]:</span><span class="sxs-lookup"><span data-stu-id="03e35-237">hello code first creates a [BatchClient][net_batchclient]:</span></span>

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

<span data-ttu-id="03e35-238">Ardından, hello örnek bir işlem düğümü havuzu oluşturacak çağrısıyla hello Batch hesabında çok oluşturur`CreatePoolIfNotExistsAsync`.</span><span class="sxs-lookup"><span data-stu-id="03e35-238">Next, hello sample creates a pool of compute nodes in hello Batch account with a call too`CreatePoolIfNotExistsAsync`.</span></span> <span data-ttu-id="03e35-239">`CreatePoolIfNotExistsAsync`kullandığı hello [BatchClient.PoolOperations.CreatePool] [ net_pool_create] yöntemi toocreate hello toplu işlem hizmeti yeni bir havuzda:</span><span class="sxs-lookup"><span data-stu-id="03e35-239">`CreatePoolIfNotExistsAsync` uses hello [BatchClient.PoolOperations.CreatePool][net_pool_create] method toocreate a new pool in hello Batch service:</span></span>

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create hello unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign hello StartTask that will be executed when compute nodes join hello pool.
        // In this case, we copy hello StartTask's resource files (that will be automatically downloaded
        // toohello node by hello StartTask) into hello shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for hello StartTask that copies hello task application files toothe
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need toomanually exit with a 0 for Batch toorecognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow hello specific error code PoolExists since that is expected if hello pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("hello pool {0} already existed when we tried toocreate it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

<span data-ttu-id="03e35-240">Bir havuzu oluştururken [CreatePool][net_pool_create], işlem düğümleri hello sayısı gibi çeşitli parametreleri hello belirttiğiniz [hello düğümlerin boyutu](../cloud-services/cloud-services-sizes-specs.md), ve düğümlerin işletim hello Sistem.</span><span class="sxs-lookup"><span data-stu-id="03e35-240">When you create a pool with [CreatePool][net_pool_create], you specify several parameters such as hello number of compute nodes, hello [size of hello nodes](../cloud-services/cloud-services-sizes-specs.md), and hello nodes' operating system.</span></span> <span data-ttu-id="03e35-241">İçinde *DotNetTutorial*, kullandığımız [CloudServiceConfiguration] [ net_cloudserviceconfiguration] toospecify Windows Server 2012 R2'den [bulut Hizmetleri](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="03e35-241">In *DotNetTutorial*, we use [CloudServiceConfiguration][net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 from [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> 

<span data-ttu-id="03e35-242">Azure sanal makineleri (VM'ler) işlem düğümleri havuzlarının hello belirterek oluşturabilirsiniz [VirtualMachineConfiguration] [ net_virtualmachineconfiguration] havuzunuz için.</span><span class="sxs-lookup"><span data-stu-id="03e35-242">You can also create pools of compute nodes that are Azure Virtual Machines (VMs) by specifying hello [VirtualMachineConfiguration][net_virtualmachineconfiguration] for your pool.</span></span> <span data-ttu-id="03e35-243">VM işlem düğümü havuzlarını Windows veya [Linux görüntülerinden](batch-linux-nodes.md) oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03e35-243">You can create a pool of VM compute nodes from either Windows or [Linux images](batch-linux-nodes.md).</span></span> <span data-ttu-id="03e35-244">VM görüntüleri için Hello kaynağı ya da olabilir:</span><span class="sxs-lookup"><span data-stu-id="03e35-244">hello source for your VM images can be either:</span></span>

- <span data-ttu-id="03e35-245">Merhaba [Azure Virtual Machines Marketi][vm_marketplace], kullanıma hazır hem Windows hem de Linux görüntüleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="03e35-245">hello [Azure Virtual Machines Marketplace][vm_marketplace], which provides both Windows and Linux images that are ready-to-use.</span></span> 
- <span data-ttu-id="03e35-246">Hazırlayıp sağlayacağınız bir özel görüntü.</span><span class="sxs-lookup"><span data-stu-id="03e35-246">A custom image that you prepare and provide.</span></span> <span data-ttu-id="03e35-247">Özel görüntüler hakkında daha fazla ayrıntı için bkz. [Batch ile büyük ölçekli paralel işlem çözümleri geliştirme](batch-api-basics.md#pool).</span><span class="sxs-lookup"><span data-stu-id="03e35-247">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="03e35-248">Batch’teki işlem kaynakları ücretlidir.</span><span class="sxs-lookup"><span data-stu-id="03e35-248">You are charged for compute resources in Batch.</span></span> <span data-ttu-id="03e35-249">toominimize maliyetleri alt `targetDedicatedComputeNodes` hello örneği çalıştırmadan önce too1.</span><span class="sxs-lookup"><span data-stu-id="03e35-249">toominimize costs, you can lower `targetDedicatedComputeNodes` too1 before you run hello sample.</span></span>
>
>

<span data-ttu-id="03e35-250">Bu fiziksel düğüm özellikleriyle birlikte, de belirtebilir bir [StartTask] [ net_pool_starttask] hello havuzu için.</span><span class="sxs-lookup"><span data-stu-id="03e35-250">Along with these physical node properties, you may also specify a [StartTask][net_pool_starttask] for hello pool.</span></span> <span data-ttu-id="03e35-251">Bu düğüme hello havuzuna katılır ve her bir düğümü yeniden Hello StartTask her düğümde yürütür.</span><span class="sxs-lookup"><span data-stu-id="03e35-251">hello StartTask executes on each node as that node joins hello pool, and each time a node is restarted.</span></span> <span data-ttu-id="03e35-252">Merhaba StartTask Itanium tabanlı sistemler için işlem düğümleri önceki toohello yürütme görevlerin üzerinde uygulamaları yüklemek için özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="03e35-252">hello StartTask is especially useful for installing applications on compute nodes prior toohello execution of tasks.</span></span> <span data-ttu-id="03e35-253">Örneğin, görevleriniz verileri Python betiklerini kullanarak işlemek, StartTask tooinstall Python hello işlem düğümlerinde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03e35-253">For example, if your tasks process data by using Python scripts, you could use a StartTask tooinstall Python on hello compute nodes.</span></span>

<span data-ttu-id="03e35-254">Bu örnek uygulamasında hello StartTask, Storage'dan indirilen hello dosyaları kopyalar (hangi belirtilen hello kullanarak [StartTask][net_starttask].[ ResourceFiles] [ net_starttask_resourcefiles] özelliği) dizininden hello StartTask çalışma dizini toohello paylaşılan, *tüm* hello düğümde çalışan görevler erişebilir.</span><span class="sxs-lookup"><span data-stu-id="03e35-254">In this sample application, hello StartTask copies hello files that it downloads from Storage (which are specified by using hello [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles] property) from hello StartTask working directory toohello shared directory that *all* tasks running on hello node can access.</span></span> <span data-ttu-id="03e35-255">Esas olarak, bu kopyalar `TaskApplication.exe` ve onun bağımlılıklarını toohello paylaşılan her düğüme hello düğümü hello havuza katılmış olduğundan hello düğümü üzerinde çalışacak herhangi bir görevi erişebilmesi.</span><span class="sxs-lookup"><span data-stu-id="03e35-255">Essentially, this copies `TaskApplication.exe` and its dependencies toohello shared directory on each node as hello node joins hello pool, so that any tasks that run on hello node can access it.</span></span>

> [!TIP]
> <span data-ttu-id="03e35-256">Merhaba **uygulama paketleri** Azure batch özelliği, uygulamanızı bir havuzdaki işlem düğümleri hello üzerine başka bir şekilde tooget sağlar.</span><span class="sxs-lookup"><span data-stu-id="03e35-256">hello **application packages** feature of Azure Batch provides another way tooget your application onto hello compute nodes in a pool.</span></span> <span data-ttu-id="03e35-257">Bkz: [Batch uygulama paketleriyle uygulama toocompute düğümlerini dağıtmak](batch-application-packages.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="03e35-257">See [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md) for details.</span></span>
>
>

<span data-ttu-id="03e35-258">Ayrıca içinde yukarıdaki hello kod parçacığında dikkat çeken bir şey hello hello iki ortam değişkenleri kullanımıdır *CommandLine* hello StartTask özelliğinin: `%AZ_BATCH_TASK_WORKING_DIR%` ve `%AZ_BATCH_NODE_SHARED_DIR%`.</span><span class="sxs-lookup"><span data-stu-id="03e35-258">Also notable in hello code snippet above is hello use of two environment variables in hello *CommandLine* property of hello StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` and `%AZ_BATCH_NODE_SHARED_DIR%`.</span></span> <span data-ttu-id="03e35-259">Batch havuzundaki her işlem düğümü belirli tooBatch olan birkaç ortam değişkenlerini otomatik olarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="03e35-259">Each compute node within a Batch pool is automatically configured with several environment variables that are specific tooBatch.</span></span> <span data-ttu-id="03e35-260">Bir görev tarafından yürütülen herhangi bir işlem toothese ortam değişkenlerine erişim vardır.</span><span class="sxs-lookup"><span data-stu-id="03e35-260">Any process that is executed by a task has access toothese environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="03e35-261">bir Batch havuzu ve görev çalışma dizinleri hakkında bilgilerin işlem düğümlerinde bulunan hello ortam değişkenleri hakkında daha fazla toofind bkz hello [görevler için ortam ayarları](batch-api-basics.md#environment-settings-for-tasks) ve [dosyalar ve dizinler ](batch-api-basics.md#files-and-directories) hello bölümlerde [geliştiriciler için Batch özelliklerine genel bakış](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="03e35-261">toofind out more about hello environment variables that are available on compute nodes in a Batch pool, and information on task working directories, see hello [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) and [Files and directories](batch-api-basics.md#files-and-directories) sections in hello [Batch feature overview for developers](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="03e35-262">4. Adım: Batch işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="03e35-262">Step 4: Create Batch job</span></span>
<span data-ttu-id="03e35-263">![Batch işi oluşturma][4]</span><span class="sxs-lookup"><span data-stu-id="03e35-263">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="03e35-264">Batch **işi**, görevler koleksiyonudur ve işlem düğümlerinin bir havuzuyla ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="03e35-264">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="03e35-265">Merhaba görevleri bir işlemle ilişkili hello havuzun işlem düğümleri üzerinde yürütün.</span><span class="sxs-lookup"><span data-stu-id="03e35-265">hello tasks in a job execute on hello associated pool's compute nodes.</span></span>

<span data-ttu-id="03e35-266">Bir işi yalnızca ilgili iş yüklerinde görevlerin düzenlenmesi ve, ancak aynı zamanda yanı sıra, ilişkisi tooother işlerini hello toplu olarak iş önceliği hello en fazla çalışma hello işin (ve uzantılarının, görevleri) gibi bazı kısıtlamalar etkileyici kullanabilirsiniz hesabı.</span><span class="sxs-lookup"><span data-stu-id="03e35-266">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as hello maximum runtime for hello job (and by extension, its tasks) as well as job priority in relation tooother jobs in hello Batch account.</span></span> <span data-ttu-id="03e35-267">Bu örnekte, ancak hello iş #3. adımda oluşturulan hello havuzu ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="03e35-267">In this example, however, hello job is associated only with hello pool that was created in step #3.</span></span> <span data-ttu-id="03e35-268">Yapılandırılmış başka ek özellik yoktur.</span><span class="sxs-lookup"><span data-stu-id="03e35-268">No additional properties are configured.</span></span>

<span data-ttu-id="03e35-269">Tüm Batch işleri belirli bir havuzla ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="03e35-269">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="03e35-270">Bu ilişkilendirme hello işin görevlerinin hangi düğümleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="03e35-270">This association indicates which nodes hello job's tasks will execute on.</span></span> <span data-ttu-id="03e35-271">Bu hello kullanarak belirttiğiniz [Cloudjob.poolınformation] [ net_job_poolinfo] hello aşağıdaki kod parçacığında gösterildiği gibi özelliği.</span><span class="sxs-lookup"><span data-stu-id="03e35-271">You specify this by using hello [CloudJob.PoolInformation][net_job_poolinfo] property, as shown in hello code snippet below.</span></span>

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

<span data-ttu-id="03e35-272">Bir işi oluşturuldu, görevler tooperform hello iş eklenir.</span><span class="sxs-lookup"><span data-stu-id="03e35-272">Now that a job has been created, tasks are added tooperform hello work.</span></span>

## <a name="step-5-add-tasks-toojob"></a><span data-ttu-id="03e35-273">5. adım: görevleri toojob ekleme</span><span class="sxs-lookup"><span data-stu-id="03e35-273">Step 5: Add tasks toojob</span></span>
<span data-ttu-id="03e35-274">![Görevleri toojob Ekle][5]</span><span class="sxs-lookup"><span data-stu-id="03e35-274">![Add tasks toojob][5]</span></span><br/><span data-ttu-id="03e35-275">
*(1) görevler toohello iş eklenir, düğümlerde zamanlanmış toorun (2) hello görevlerdir ve (3) hello görevleri hello veri dosyaları tooprocess indirme*</span><span class="sxs-lookup"><span data-stu-id="03e35-275">
*(1) Tasks are added toohello job, (2) hello tasks are scheduled toorun on nodes, and (3) hello tasks download hello data files tooprocess*</span></span>

<span data-ttu-id="03e35-276">Toplu **görevleri** hello üzerinde yürütülen hello tek tek iş birimleri işlem düğümlerini şunlardır.</span><span class="sxs-lookup"><span data-stu-id="03e35-276">Batch **tasks** are hello individual units of work that execute on hello compute nodes.</span></span> <span data-ttu-id="03e35-277">Bir görev, bir komut satırı ve hello komut dosyaları veya bu komut satırında belirttiğiniz yürütülebilir dosyaları çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="03e35-277">A task has a command line and runs hello scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="03e35-278">tooactually gerçekleştirmek iş, görevleri tooa iş eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="03e35-278">tooactually perform work, tasks must be added tooa job.</span></span> <span data-ttu-id="03e35-279">Her [CloudTask] [ net_task] bir komut satırı özelliği kullanılarak yapılandırılır ve [ResourceFiles] [ net_task_resourcefiles] (Merhaba havuza ait startTask gibi), komut satırı otomatik olarak yürütülmeden önce hello görev toohello düğümü indirir.</span><span class="sxs-lookup"><span data-stu-id="03e35-279">Each [CloudTask][net_task] is configured by using a command-line property and [ResourceFiles][net_task_resourcefiles] (as with hello pool's StartTask) that hello task downloads toohello node before its command line is automatically executed.</span></span> <span data-ttu-id="03e35-280">Merhaba, *DotNetTutorial* örnek projesinde her görev yalnızca bir dosya işler.</span><span class="sxs-lookup"><span data-stu-id="03e35-280">In hello *DotNetTutorial* sample project, each task processes only one file.</span></span> <span data-ttu-id="03e35-281">Bu nedenle, kendi ResourceFiles koleksiyonunda tek bir öğe bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="03e35-281">Thus, its ResourceFiles collection contains a single element.</span></span>

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks toojob [{1}]...", inputFiles.Count, jobId);

    // Create a collection toohold hello tasks that we'll be adding toohello job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of hello tasks. Because we copied hello task application toothe
    // node's shared directory with hello pool's StartTask, we can access it via
    // hello shared directory on hello node that hello task runs on.
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

    // Add hello tasks as a collection, as opposed tooissuing a separate AddTask call
    // for each. Bulk task submission helps tooensure efficient underlying API calls
    // toohello Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> <span data-ttu-id="03e35-282">Ortam değişkenlerine eriştiklerinde gibi `%AZ_BATCH_NODE_SHARED_DIR%` veya hello düğümün bulunmayan bir uygulama yürüttüklerinde `PATH`, görev komut satırları öneki, ile `cmd /c`.</span><span class="sxs-lookup"><span data-stu-id="03e35-282">When they access environment variables such as `%AZ_BATCH_NODE_SHARED_DIR%` or execute an application not found in hello node's `PATH`, task command lines must be prefixed with `cmd /c`.</span></span> <span data-ttu-id="03e35-283">Bu açıkça hello komut yorumlayıcı yürütecek ve komutunuzu uyguladıktan sonra tooterminate isteyin.</span><span class="sxs-lookup"><span data-stu-id="03e35-283">This will explicitly execute hello command interpreter and instruct it tooterminate after carrying out your command.</span></span> <span data-ttu-id="03e35-284">Bu gereksinim, görevlerinizin hello düğümün bir uygulama yürütüyorsa gereksizdir `PATH` (gibi *robocopy.exe* veya *powershell.exe*) ve hiç ortam değişkeni kullanılır.</span><span class="sxs-lookup"><span data-stu-id="03e35-284">This requirement is unnecessary if your tasks execute an application in hello node's `PATH` (such as *robocopy.exe* or *powershell.exe*) and no environment variables are used.</span></span>
>
>

<span data-ttu-id="03e35-285">Merhaba içinde `foreach` Yukarıdaki kod parçacığında hello döngüde, üç komut satırı bağımsız değişkenleri çok geçirilen şekilde hello komut satırı hello görev için oluşturulan görebilirsiniz*TaskApplication.exe*:</span><span class="sxs-lookup"><span data-stu-id="03e35-285">Within hello `foreach` loop in hello code snippet above, you can see that hello command line for hello task is constructed such that three command-line arguments are passed too*TaskApplication.exe*:</span></span>

1. <span data-ttu-id="03e35-286">Merhaba **ilk bağımsız değişken** hello dosya tooprocess hello yoludur.</span><span class="sxs-lookup"><span data-stu-id="03e35-286">hello **first argument** is hello path of hello file tooprocess.</span></span> <span data-ttu-id="03e35-287">Merhaba düğümde yer aldığından bu hello yerel yol toohello dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="03e35-287">This is hello local path toohello file as it exists on hello node.</span></span> <span data-ttu-id="03e35-288">ResourceFile nesnesi'ne zaman hello `UploadFileToContainerAsync` ilk oluşturulduğunda yukarıdaki hello dosya adı bu özellik için (bir parametre toohello ResourceFile oluşturucuda) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="03e35-288">When hello ResourceFile object in `UploadFileToContainerAsync` was first created above, hello file name was used for this property (as a parameter toohello ResourceFile constructor).</span></span> <span data-ttu-id="03e35-289">Bu, hello dosya bulunabilir hello aynı gösterir olarak dizin *TaskApplication.exe*.</span><span class="sxs-lookup"><span data-stu-id="03e35-289">This indicates that hello file can be found in hello same directory as *TaskApplication.exe*.</span></span>
2. <span data-ttu-id="03e35-290">Merhaba **ikinci bağımsız değişken** bu hello üst belirtir *N* sözcükler toohello çıktı dosyasına yazılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="03e35-290">hello **second argument** specifies that hello top *N* words should be written toohello output file.</span></span> <span data-ttu-id="03e35-291">Merhaba örnekte bu hello ilk üç sözcük toohello çıktı dosyasına yazılır böylece kodlanmış.</span><span class="sxs-lookup"><span data-stu-id="03e35-291">In hello sample, this is hard-coded so that hello top three words are written toohello output file.</span></span>
3. <span data-ttu-id="03e35-292">Merhaba **üçüncü bağımsız değişken** yazma erişimi toohello sağlayan hello paylaşılan erişim imzası (SAS) **çıkış** Azure storage'da kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="03e35-292">hello **third argument** is hello shared access signature (SAS) that provides write access toohello **output** container in Azure Storage.</span></span> <span data-ttu-id="03e35-293">*TaskApplication.exe* hello çıktı dosyası tooAzure depolama yüklediğinde erişim imzası URL'sini bu paylaşılan kullanır.</span><span class="sxs-lookup"><span data-stu-id="03e35-293">*TaskApplication.exe* uses this shared access signature URL when it uploads hello output file tooAzure Storage.</span></span> <span data-ttu-id="03e35-294">Bunun için hello kod hello bulabilirsiniz `UploadFileToContainer` hello TaskApplication projesinin yönteminde `Program.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="03e35-294">You can find hello code for this in hello `UploadFileToContainer` method in hello TaskApplication project's `Program.cs` file:</span></span>

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference toohello container using hello SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload hello file (as a new blob) toohello container
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

                // Indicate that a failure has occurred so that when hello Batch service
                // sets hello CloudTask.ExecutionInformation.ExitCode for hello task that
                // executed this application, it properly indicates that there was a
                // problem with hello task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="03e35-295">6. Adım: Görevleri izleme</span><span class="sxs-lookup"><span data-stu-id="03e35-295">Step 6: Monitor tasks</span></span>
<span data-ttu-id="03e35-296">![Görevleri izleme][6]</span><span class="sxs-lookup"><span data-stu-id="03e35-296">![Monitor tasks][6]</span></span><br/><span data-ttu-id="03e35-297">
*Merhaba istemci uygulaması (1) izleyiciler tamamlama ve başarı durumu için görevleri hello ve (2) görevler karşıya yükleme sonuç veri tooAzure depolama hello*</span><span class="sxs-lookup"><span data-stu-id="03e35-297">
*hello client application (1) monitors hello tasks for completion and success status, and (2) hello tasks upload result data tooAzure Storage*</span></span>

<span data-ttu-id="03e35-298">Görevleri tooa iş eklendiğinde bunlar otomatik olarak kuyruğa ve hello işle ilişkili hello havuzundaki işlem düğümlerinde yürütülmesi için zamanlanan.</span><span class="sxs-lookup"><span data-stu-id="03e35-298">When tasks are added tooa job, they are automatically queued and scheduled for execution on compute nodes within hello pool associated with hello job.</span></span> <span data-ttu-id="03e35-299">Belirttiğiniz hello ayarlarına bağlı olarak, Batch tüm kuyruğa alınan, zamanlama, yeniden deneniyor ve diğer görev yönetimi görevlerini işler.</span><span class="sxs-lookup"><span data-stu-id="03e35-299">Based on hello settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="03e35-300">Toomonitoring görev yürütme birçok yaklaşım vardır.</span><span class="sxs-lookup"><span data-stu-id="03e35-300">There are many approaches toomonitoring task execution.</span></span> <span data-ttu-id="03e35-301">DotNetTutorial, yalnızca tamamlama, görev başarılı veya başarısız durumlarını raporlayan basit bir örnek gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="03e35-301">DotNetTutorial shows a simple example that reports only on completion and task failure or success states.</span></span> <span data-ttu-id="03e35-302">Merhaba içinde `MonitorTasks` Dotnettutorial'in yönteminde `Program.cs`, tartışmayı destekleyen üç Batch .NET kavramı vardır.</span><span class="sxs-lookup"><span data-stu-id="03e35-302">Within hello `MonitorTasks` method in DotNetTutorial's `Program.cs`, there are three Batch .NET concepts that warrant discussion.</span></span> <span data-ttu-id="03e35-303">Görüntülenme sırasıyla aşağıda listelenmişlerdir:</span><span class="sxs-lookup"><span data-stu-id="03e35-303">They are listed below in their order of appearance:</span></span>

1. <span data-ttu-id="03e35-304">**ODATADetailLevel**: Liste işlemlerinde [ODATADetailLevel][net_odatadetaillevel] belirtilmesi (iş görevlerinin listesini almak gibi) Batch uygulaması performansını sağlamak için önemlidir.</span><span class="sxs-lookup"><span data-stu-id="03e35-304">**ODATADetailLevel**: Specifying [ODATADetailLevel][net_odatadetaillevel] in list operations (such as obtaining a list of a job's tasks) is essential in ensuring Batch application performance.</span></span> <span data-ttu-id="03e35-305">Ekleme [hello Azure Batch hizmetinin verimli bir şekilde sorgu](batch-efficient-list-queries.md) toplu iş uygulamalarınız içinde durum izlemenin herhangi sıralama yapmayı planlıyorsanız, liste okuma tooyour.</span><span class="sxs-lookup"><span data-stu-id="03e35-305">Add [Query hello Azure Batch service efficiently](batch-efficient-list-queries.md) tooyour reading list if you plan on doing any sort of status monitoring within your Batch applications.</span></span>
2. <span data-ttu-id="03e35-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor], görev durumlarının izlenmesi için yardımcı programlara sahip Batch .NET uygulamalarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="03e35-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] provides Batch .NET applications with helper utilities for monitoring task states.</span></span> <span data-ttu-id="03e35-307">İçinde `MonitorTasks`, *DotNetTutorial* için tüm görevleri tooreach bekler [TaskState.Completed] [ net_taskstate] zaman sınırı içinde.</span><span class="sxs-lookup"><span data-stu-id="03e35-307">In `MonitorTasks`, *DotNetTutorial* waits for all tasks tooreach [TaskState.Completed][net_taskstate] within a time limit.</span></span> <span data-ttu-id="03e35-308">Ardından hello işi sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="03e35-308">Then it terminates hello job.</span></span>
3. <span data-ttu-id="03e35-309">**TerminateJobAsync**: bir işlemle sonlandırma [JobOperations.TerminateJobAsync] [ net_joboperations_terminatejob] (veya hello engelleme JobOperations.TerminateJob) bu işin tamamlandı olarak işaretler.</span><span class="sxs-lookup"><span data-stu-id="03e35-309">**TerminateJobAsync**: Terminating a job with [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (or hello blocking JobOperations.TerminateJob) marks that job as completed.</span></span> <span data-ttu-id="03e35-310">Temel toodo olduğundan bunu Batch çözümünüzü kullanıyorsa, bir [JobReleaseTask][net_jobreltask].</span><span class="sxs-lookup"><span data-stu-id="03e35-310">It is essential toodo so if your Batch solution uses a [JobReleaseTask][net_jobreltask].</span></span> <span data-ttu-id="03e35-311">[İş hazırlama ve tamamlama görevleri](batch-job-prep-release.md)’nde açıklanan özel tür bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="03e35-311">This is a special type of task, which is described in [Job preparation and completion tasks](batch-job-prep-release.md).</span></span>

<span data-ttu-id="03e35-312">Merhaba `MonitorTasks` yönteminden *DotNetTutorial*'s `Program.cs` aşağıda yer almaktadır:</span><span class="sxs-lookup"><span data-stu-id="03e35-312">hello `MonitorTasks` method from *DotNetTutorial*'s `Program.cs` appears below:</span></span>

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed tooreach hello Completed state within hello timeout period.";

    // Obtain hello collection of tasks currently managed by hello job. Note that we use
    // a detail level too specify that only hello "id" property of each task should be
    // populated. Using a detail level for all list operations helps toolower
    // response time from hello Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor toomonitor hello state of our tasks. In this case, we
    // will wait for all tasks tooreach hello Completed state.
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

    // All tasks have reached hello "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property tooensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update hello detail level toopopulate only hello task id and executionInfo
    // properties. We refresh hello tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate hello task's properties with hello latest info from hello Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with hello task. It is important toonote that
            // hello task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that hello application executed by hello task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within hello specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="03e35-313">7. Adım: Görev çıktısı indirme</span><span class="sxs-lookup"><span data-stu-id="03e35-313">Step 7: Download task output</span></span>
<span data-ttu-id="03e35-314">![Storage'dan görev çıktısını indirme][7]</span><span class="sxs-lookup"><span data-stu-id="03e35-314">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="03e35-315">Merhaba iş tamamlandığında, hello görevleri hello çıktısını Azure Storage'dan indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="03e35-315">Now that hello job is completed, hello output from hello tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="03e35-316">Bu çağrı çok yapılır`DownloadBlobsFromContainerAsync` içinde *DotNetTutorial*'s `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="03e35-316">This is done with a call too`DownloadBlobsFromContainerAsync` in *DotNetTutorial*'s `Program.cs`:</span></span>

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference tooa previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all hello block blobs in hello specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference toohello current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents tooa file in hello specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded too{0}", directoryPath);
}
```

> [!NOTE]
> <span data-ttu-id="03e35-317">Çağrı çok hello`DownloadBlobsFromContainerAsync` hello içinde *DotNetTutorial* uygulama belirtir hello dosyaları indirilen tooyour olmalıdır `%TEMP%` klasör.</span><span class="sxs-lookup"><span data-stu-id="03e35-317">hello call too`DownloadBlobsFromContainerAsync` in hello *DotNetTutorial* application specifies that hello files should be downloaded tooyour `%TEMP%` folder.</span></span> <span data-ttu-id="03e35-318">Ücretsiz toomodify düşünüyorsanız bu konumu çıktı.</span><span class="sxs-lookup"><span data-stu-id="03e35-318">Feel free toomodify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="03e35-319">8. Adım: Sil kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="03e35-319">Step 8: Delete containers</span></span>
<span data-ttu-id="03e35-320">Azure Storage'da yer alan veriler için ücretlendirildiğinizden, Batch işleriniz için artık gerekli olmayan bir fikir tooremove BLOB her zaman sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="03e35-320">Because you are charged for data that resides in Azure Storage, it's always a good idea tooremove blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="03e35-321">Dotnettutorial'ın `Program.cs`, bu üç çağrı toohello yardımcı yöntemi ile yapılır `DeleteContainerAsync`:</span><span class="sxs-lookup"><span data-stu-id="03e35-321">In DotNetTutorial's `Program.cs`, this is done with three calls toohello helper method `DeleteContainerAsync`:</span></span>

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

<span data-ttu-id="03e35-322">Merhaba yöntemin kendisi yalnızca başvuru toohello kapsayıcı edinir ve ardından çağırır [Cloudblobcontainer.deleteıfexistsasync][net_container_delete]:</span><span class="sxs-lookup"><span data-stu-id="03e35-322">hello method itself merely obtains a reference toohello container, and then calls [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span></span>

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

## <a name="step-9-delete-hello-job-and-hello-pool"></a><span data-ttu-id="03e35-323">9. adım: hello işi ve hello havuzu silme</span><span class="sxs-lookup"><span data-stu-id="03e35-323">Step 9: Delete hello job and hello pool</span></span>
<span data-ttu-id="03e35-324">Merhaba son adımda Merhaba DotNetTutorial uygulaması tarafından oluşturulan istendiğinde toodelete hello iş ve hello havuzu demektir.</span><span class="sxs-lookup"><span data-stu-id="03e35-324">In hello final step, you're prompted toodelete hello job and hello pool that were created by hello DotNetTutorial application.</span></span> <span data-ttu-id="03e35-325">İşlerin ve görevlerin kendileri için sizden ücret alınmasa da işlem düğümleri için *ücret alınır*.</span><span class="sxs-lookup"><span data-stu-id="03e35-325">Although you're not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="03e35-326">Bu nedenle, düğümleri yalnızca gerektiğinde ayırmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="03e35-326">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="03e35-327">Kullanılmayan havuzların silinmesi bakım işleminizin bir parçası olabilir.</span><span class="sxs-lookup"><span data-stu-id="03e35-327">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="03e35-328">Merhaba BatchClient's [JobOperations] [ net_joboperations] ve [PoolOperations] [ net_pooloperations] her ikisi de varsa adlı ilgili silme yöntemleri vardır Merhaba kullanıcı silme onaylar:</span><span class="sxs-lookup"><span data-stu-id="03e35-328">hello BatchClient's [JobOperations][net_joboperations] and [PoolOperations][net_pooloperations] both have corresponding deletion methods, which are called if hello user confirms deletion:</span></span>

```csharp
// Clean up hello resources we've created in hello Batch account if hello user so chooses
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
> <span data-ttu-id="03e35-329">İşlem kaynaklarının ücretli olduğunu unutmayın; kullanılmayan havuzların silinmesi masrafları azaltacaktır.</span><span class="sxs-lookup"><span data-stu-id="03e35-329">Keep in mind that you are charged for compute resources—deleting unused pools will minimize cost.</span></span> <span data-ttu-id="03e35-330">Ayrıca, bir havuzun silinmesinin Bu havuz içindeki tüm işlem düğümlerini siler ve hello havuz silindikten sonra hello düğümlerinde tüm veriler kurtarılamaz olacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="03e35-330">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on hello nodes will be unrecoverable after hello pool is deleted.</span></span>
>
>

## <a name="run-hello-dotnettutorial-sample"></a><span data-ttu-id="03e35-331">Merhaba çalıştırmak *DotNetTutorial* örnek</span><span class="sxs-lookup"><span data-stu-id="03e35-331">Run hello *DotNetTutorial* sample</span></span>
<span data-ttu-id="03e35-332">Merhaba örnek uygulamayı çalıştırdığınızda, hello konsol çıktısı benzer toohello aşağıdaki olacaktır.</span><span class="sxs-lookup"><span data-stu-id="03e35-332">When you run hello sample application, hello console output will be similar toohello following.</span></span> <span data-ttu-id="03e35-333">Yürütme sırasında bir öğesiyle karşılaşacaksınız `Awaiting task completion, timeout in 00:30:00...` hello havuzun işlem düğümleri başlatıldığı sırada.</span><span class="sxs-lookup"><span data-stu-id="03e35-333">During execution, you will experience a pause at `Awaiting task completion, timeout in 00:30:00...` while hello pool's compute nodes are started.</span></span> <span data-ttu-id="03e35-334">Kullanım hello [Azure portal] [ azure_portal] toomonitor havuzu, işlem düğümleri, işi ve görevleri yürütme sırasında ve sonrasında.</span><span class="sxs-lookup"><span data-stu-id="03e35-334">Use hello [Azure portal][azure_portal] toomonitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="03e35-335">Kullanım hello [Azure portal] [ azure_portal] veya hello [Azure Storage Gezgini] [ storage_explorers] olan tooview hello depolama kaynaklarını (kapsayıcılar ve bloblar) Merhaba uygulama tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="03e35-335">Use hello [Azure portal][azure_portal] or hello [Azure Storage Explorer][storage_explorers] tooview hello Storage resources (containers and blobs) that are created by hello application.</span></span>

<span data-ttu-id="03e35-336">Tipik yürütme süresi **yaklaşık 5 dakika** varsayılan yapılandırmasında hello uygulama çalıştırıldığında.</span><span class="sxs-lookup"><span data-stu-id="03e35-336">Typical execution time is **approximately 5 minutes** when you run hello application in its default configuration.</span></span>

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe toocontainer [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll toocontainer [application]...
Uploading file ..\..\taskdata1.txt toocontainer [input]...
Uploading file ..\..\taskdata2.txt toocontainer [input]...
Uploading file ..\..\taskdata3.txt toocontainer [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks toojob [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within hello specified timeout period.
Downloading all files from container [output]...
All files downloaded tooC:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="03e35-337">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="03e35-337">Next steps</span></span>
<span data-ttu-id="03e35-338">Ücretsiz toomake değişiklikleri çok eşitleyerek*DotNetTutorial* ve *TaskApplication* tooexperiment farklı olan işlem senaryoları.</span><span class="sxs-lookup"><span data-stu-id="03e35-338">Feel free toomake changes too*DotNetTutorial* and *TaskApplication* tooexperiment with different compute scenarios.</span></span> <span data-ttu-id="03e35-339">Örneğin, bir yürütme gecikmesi çok eklemeyi deneyin*TaskApplication*gibi bir durumda olduğu gibi [Thread.Sleep][net_thread_sleep], uzun süre çalışan toosimulate görevler ve bunları hello Portalı'nda izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03e35-339">For example, try adding an execution delay too*TaskApplication*, such as with [Thread.Sleep][net_thread_sleep], toosimulate long-running tasks and monitor them in hello portal.</span></span> <span data-ttu-id="03e35-340">Deneyin daha fazla görev eklemeye veya işlem düğümleri hello sayısını ayarlama.</span><span class="sxs-lookup"><span data-stu-id="03e35-340">Try adding more tasks or adjusting hello number of compute nodes.</span></span> <span data-ttu-id="03e35-341">İçin mantığı toocheck eklemek ve varolan bir havuzu toospeed yürütme saati hello kullanılmasına izin verin (*İpucu*: kullanıma `ArticleHelpers.cs` hello içinde [öğesini kullanıma alın] [ github_samples_common] proje [azure-batch-samples][github_samples]).</span><span class="sxs-lookup"><span data-stu-id="03e35-341">Add logic toocheck for and allow hello use of an existing pool toospeed execution time (*hint*: check out `ArticleHelpers.cs` in hello [Microsoft.Azure.Batch.Samples.Common][github_samples_common] project in [azure-batch-samples][github_samples]).</span></span>

<span data-ttu-id="03e35-342">Merhaba temel iş akışı Batch çözümünün ile tanıdık, zaman toodig hello Batch hizmetinin ek özelliklerinin toohello içinde olduğu.</span><span class="sxs-lookup"><span data-stu-id="03e35-342">Now that you're familiar with hello basic workflow of a Batch solution, it's time toodig in toohello additional features of hello Batch service.</span></span>

* <span data-ttu-id="03e35-343">Gözden geçirme hello [genel bakış Azure Batch özelliklerine](batch-api-basics.md) yeni toohello hizmeti olup olmadığınızı öneririz makalesi.</span><span class="sxs-lookup"><span data-stu-id="03e35-343">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
* <span data-ttu-id="03e35-344">Başlat'hello altında diğer Batch geliştirmesi makalelerine **geliştirme ayrıntılı** hello içinde [Batch öğrenme yolu][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="03e35-344">Start on hello other Batch development articles under **Development in-depth** in hello [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="03e35-345">Hello toplu kullanarak hello "ilk N sözcük" iş yükünü işlemenin farklı bir uygulama kullanıma [TopNWords] [ github_topnwords] örnek.</span><span class="sxs-lookup"><span data-stu-id="03e35-345">Check out a different implementation of processing hello "top N words" workload by using Batch in hello [TopNWords][github_topnwords] sample.</span></span>
* <span data-ttu-id="03e35-346">Gözden geçirme hello Batch .NET [sürüm notları](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) hello en son değişiklikleri hello Kitaplığı'nda.</span><span class="sxs-lookup"><span data-stu-id="03e35-346">Review hello Batch .NET [release notes](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) for hello latest changes in hello library.</span></span>

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
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "Karşıya yükleme görev uygulamasını ve girdi (veri) toocontainers dosyaları"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Batch havuzu oluşturma"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Batch işi oluşturma"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "Görevleri toojob Ekle"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "Görevleri izleme"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Depolama’dan görev çıkışını indirme"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Batch çözümü iş akışı (tam diyagram)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "Portalda Batch kimlik bilgileri"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "Portalda Depolama kimlik bilgileri"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Batch çözümü iş akışı (minimal diyagram)"
