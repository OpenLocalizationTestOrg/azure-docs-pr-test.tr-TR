---
title: "işlem düğümlerinde - Azure Batch uygulama paketleri aaaInstall | Microsoft Docs"
description: "Toplu yükleme için sürümler işlem düğümleri ve kullanım hello uygulama paketleri Özelliği Azure Batch tooeasily birden çok uygulama yönetin."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 3b6044b7-5f65-4a27-9d43-71e1863d16cf
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 683be7b7f1bd5db7835332016f6dccb72f45c3b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-applications-toocompute-nodes-with-batch-application-packages"></a><span data-ttu-id="9a647-103">Uygulamaları toocompute düğümleri Batch uygulama paketleri ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="9a647-103">Deploy applications toocompute nodes with Batch application packages</span></span>

<span data-ttu-id="9a647-104">Azure Batch uygulama paketleri özelliği Hello görev uygulamaları kolay yönetim sağlar ve bunların dağıtım toohello işlem düğümlerini havuzunuzdaki.</span><span class="sxs-lookup"><span data-stu-id="9a647-104">hello application packages feature of Azure Batch provides easy management of task applications and their deployment toohello compute nodes in your pool.</span></span> <span data-ttu-id="9a647-105">Uygulama paketleri ile karşıya yükleyin ve birden fazla sürümünü de dahil olmak üzere destek dosyalarını, görevleri çalıştırmak hello uygulamaları yönetin.</span><span class="sxs-lookup"><span data-stu-id="9a647-105">With application packages, you can upload and manage multiple versions of hello applications your tasks run, including their supporting files.</span></span> <span data-ttu-id="9a647-106">Ardından otomatik olarak bir dağıtabilirsiniz veya bu uygulamaları toohello fazlasını havuzunuzdaki düğümlerden işlem.</span><span class="sxs-lookup"><span data-stu-id="9a647-106">You can then automatically deploy one or more of these applications toohello compute nodes in your pool.</span></span>

<span data-ttu-id="9a647-107">Bu makalede, öğreneceksiniz nasıl tooupload ve hello Azure portal'ın uygulama paketlerini yönetin.</span><span class="sxs-lookup"><span data-stu-id="9a647-107">In this article, you will learn how tooupload and manage application packages in hello Azure portal.</span></span> <span data-ttu-id="9a647-108">Ardından nasıl tooinstall bir havuzun üzerlerinde ile işlem düğümleri öğreneceksiniz hello [Batch .NET] [ api_net] kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="9a647-108">You will then learn how tooinstall them on a pool's compute nodes with hello [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="9a647-109">Uygulama paketleri 5 Temmuz 2017’den sonra oluşturulmuş tüm Batch havuzlarında desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9a647-109">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="9a647-110">Bunlar yalnızca hello havuzu, bir bulut Hizmeti Yapılandırması kullanılarak oluşturulduysa 10 Mart 2016 ve 5 Temmuz 2017 arasında oluşturulan Batch havuzu üzerinde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9a647-110">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="9a647-111">Önceki too10 Mart 2016 oluşturulan batch havuzları, uygulama paketleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="9a647-111">Batch pools created prior too10 March 2016 do not support application packages.</span></span>
>
> <span data-ttu-id="9a647-112">Merhaba oluşturmak ve uygulama paketleri yönetmek için API hello [Batch yönetimi .NET] parçasıdır [[api_net_mgmt]] kitaplık.</span><span class="sxs-lookup"><span data-stu-id="9a647-112">hello APIs for creating and managing application packages are part of hello [Batch Management .NET][[api_net_mgmt]] library.</span></span> <span data-ttu-id="9a647-113">Merhaba bir işlem düğümünde uygulama paketleri yüklemek için API hello parçasıdır [Batch .NET] [ api_net] kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="9a647-113">hello APIs for installing application packages on a compute node are part of hello [Batch .NET][api_net] library.</span></span>  
>
> <span data-ttu-id="9a647-114">Burada açıklanan hello uygulama paketleri özelliği hello toplu işlem uygulamaları özelliği hello hizmet önceki sürümlerinde kullanılabilir yerini alır.</span><span class="sxs-lookup"><span data-stu-id="9a647-114">hello application packages feature described here supersedes hello Batch Apps feature available in previous versions of hello service.</span></span>
> 
> 

## <a name="application-package-requirements"></a><span data-ttu-id="9a647-115">Uygulama paketi gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="9a647-115">Application package requirements</span></span>
<span data-ttu-id="9a647-116">toouse uygulama paketleri, gereksinim duyduğunuz çok[bir Azure depolama hesabı bağlantı](#link-a-storage-account) tooyour toplu işlem hesabı.</span><span class="sxs-lookup"><span data-stu-id="9a647-116">toouse application packages, you need too[link an Azure Storage account](#link-a-storage-account) tooyour Batch account.</span></span>

<span data-ttu-id="9a647-117">Bu özellik sunulmuştur [Batch REST API'si] [ api_rest] sürüm 2015 12 01.2.2 ve hello karşılık gelen [Batch .NET] [ api_net] kitaplığı sürümü 3.1.0.</span><span class="sxs-lookup"><span data-stu-id="9a647-117">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and hello corresponding [Batch .NET][api_net] library version 3.1.0.</span></span> <span data-ttu-id="9a647-118">Her zaman hello son API sürümü Batch ile çalışırken kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="9a647-118">We recommend that you always use hello latest API version when working with Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="9a647-119">Uygulama paketleri 5 Temmuz 2017’den sonra oluşturulmuş tüm Batch havuzlarında desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9a647-119">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="9a647-120">Bunlar yalnızca hello havuzu, bir bulut Hizmeti Yapılandırması kullanılarak oluşturulduysa 10 Mart 2016 ve 5 Temmuz 2017 arasında oluşturulan Batch havuzu üzerinde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9a647-120">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="9a647-121">Önceki too10 Mart 2016 oluşturulan batch havuzları, uygulama paketleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="9a647-121">Batch pools created prior too10 March 2016 do not support application packages.</span></span>
>
>

## <a name="about-applications-and-application-packages"></a><span data-ttu-id="9a647-122">Uygulamalar ve uygulama paketleri hakkında</span><span class="sxs-lookup"><span data-stu-id="9a647-122">About applications and application packages</span></span>
<span data-ttu-id="9a647-123">Azure Batch içindeki bir *uygulama* havuzunuzdaki işlem düğümlerine otomatik olarak indirilen toohello olabilir sürümlü ikili dosyaları tooa kümesini ifade eder.</span><span class="sxs-lookup"><span data-stu-id="9a647-123">Within Azure Batch, an *application* refers tooa set of versioned binaries that can be automatically downloaded toohello compute nodes in your pool.</span></span> <span data-ttu-id="9a647-124">Bir *uygulama paketi* tooa başvuruyor *belirli* bu ikili dosyaları ve temsil bir verilen *sürüm* hello uygulamasının.</span><span class="sxs-lookup"><span data-stu-id="9a647-124">An *application package* refers tooa *specific set* of those binaries and represents a given *version* of hello application.</span></span>

<span data-ttu-id="9a647-125">![Uygulamalar ve uygulama paketleri üst düzey diyagramı][1]</span><span class="sxs-lookup"><span data-stu-id="9a647-125">![High-level diagram of applications and application packages][1]</span></span>

### <a name="applications"></a><span data-ttu-id="9a647-126">Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="9a647-126">Applications</span></span>
<span data-ttu-id="9a647-127">Toplu bir uygulamada içeriyor veya daha fazla uygulama paketleri ve Merhaba uygulaması için yapılandırma seçeneklerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="9a647-127">An application in Batch contains one or more application packages and specifies configuration options for hello application.</span></span> <span data-ttu-id="9a647-128">Örneğin, bir uygulama üzerinde işlem düğümlerini ve kendi paketleri olup güncelleştirilmiş veya silinebilir hello varsayılan uygulama paketi sürümü tooinstall belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a647-128">For example, an application can specify hello default application package version tooinstall on compute nodes and whether its packages can be updated or deleted.</span></span>

### <a name="application-packages"></a><span data-ttu-id="9a647-129">Uygulama paketleri</span><span class="sxs-lookup"><span data-stu-id="9a647-129">Application packages</span></span>
<span data-ttu-id="9a647-130">Bir uygulama paketi hello uygulama ikili dosyaları içeren bir .zip dosyası ve görevleri toorun hello uygulamanız için gerekli destek dosyaları ' dir.</span><span class="sxs-lookup"><span data-stu-id="9a647-130">An application package is a .zip file that contains hello application binaries and supporting files that are required for your tasks toorun hello application.</span></span> <span data-ttu-id="9a647-131">Her uygulama paketi hello uygulamanın belirli bir sürümünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="9a647-131">Each application package represents a specific version of hello application.</span></span>

<span data-ttu-id="9a647-132">Uygulama paketleri hello havuzu ve görev düzeylerinde belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a647-132">You can specify application packages at hello pool and task levels.</span></span> <span data-ttu-id="9a647-133">Bir havuz veya görev oluşturduğunuzda, bir veya daha fazla bu paketleri ve (isteğe bağlı) bir sürüm belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a647-133">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span></span>

* <span data-ttu-id="9a647-134">**Havuz uygulama paketleri** çok dağıtılan*her* hello havuzdaki düğüm.</span><span class="sxs-lookup"><span data-stu-id="9a647-134">**Pool application packages** are deployed too*every* node in hello pool.</span></span> <span data-ttu-id="9a647-135">Bir düğüm bir havuzu katıldığında ve onu yeniden başlatıldığı ya da dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="9a647-135">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span></span>
  
    <span data-ttu-id="9a647-136">Bir havuzdaki tüm düğümlerin işe ait görevleri yürüttüğünüzde havuzu uygulama paketleri uygundur.</span><span class="sxs-lookup"><span data-stu-id="9a647-136">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span></span> <span data-ttu-id="9a647-137">Bir veya daha fazla uygulama paketlerini bir havuz oluşturduğunuzda ve ekleme veya güncelleştirme mevcut havuzun paketleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a647-137">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span></span> <span data-ttu-id="9a647-138">Varolan bir havuzun uygulama paketleri güncelleştirirseniz, alt düğümleri tooinstall hello yeni paketi yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a647-138">If you update an existing pool's application packages, you must restart its nodes tooinstall hello new package.</span></span>
* <span data-ttu-id="9a647-139">**Görev uygulama paketleri** tooa işlem düğümü toorun hello görevin komut satırı çalıştırmadan önce bir görev zamanlanan yalnızca dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="9a647-139">**Task application packages** are deployed only tooa compute node scheduled toorun a task, just before running hello task's command line.</span></span> <span data-ttu-id="9a647-140">Uygulama paketi ve sürümü olduğundan zaten hello düğümde Hello belirtilmişse değil imzalanmasını ve hello varolan paket kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9a647-140">If hello specified application package and version is already on hello node, it is not redeployed and hello existing package is used.</span></span>
  
    <span data-ttu-id="9a647-141">Görev uygulama paketleri Burada farklı işleri bir havuzu üzerinde çalışır ve bir iş tamamlandığında hello havuzu silinmez paylaşılan havuzu ortamlarında yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="9a647-141">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and hello pool is not deleted when a job is completed.</span></span> <span data-ttu-id="9a647-142">İşinizi hello havuzunda düğümleri'den daha az görev varsa, görev uygulama paketleri bir uygulamanız görevleri çalıştırmak dağıtılan yalnızca toohello düğümleri olduğundan veri aktarımını en aza indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a647-142">If your job has fewer tasks than nodes in hello pool, task application packages can minimize data transfer since your application is deployed only toohello nodes that run tasks.</span></span>
  
    <span data-ttu-id="9a647-143">Büyük bir uygulamayı çalıştırma işleri görev uygulama paketi yararlanabilir diğer senaryolar verilmiştir ancak yalnızca birkaç görevler için.</span><span class="sxs-lookup"><span data-stu-id="9a647-143">Other scenarios that can benefit from task application packages are jobs that run a large application, but for only a few tasks.</span></span> <span data-ttu-id="9a647-144">Örneğin, önceden işlem aşama veya hello ön işleme veya birleştirme uygulama ağır olduğu, bir birleştirme görev görev uygulama paketlerini kullanarak yararlanabilir.</span><span class="sxs-lookup"><span data-stu-id="9a647-144">For example, a pre-processing stage or a merge task, where hello pre-processing or merge application is heavyweight, may benefit from using task application packages.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a647-145">Uygulamalar ve toplu işlem hesabı içindeki uygulama paketleri hello sayısını ve hello en fazla uygulama paket boyutu kısıtlamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="9a647-145">There are restrictions on hello number of applications and application packages within a Batch account and on hello maximum application package size.</span></span> <span data-ttu-id="9a647-146">Bkz: [hello Azure Batch hizmeti için kotalar ve sınırlar](batch-quota-limit.md) bu sınırları hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="9a647-146">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for details about these limits.</span></span>
> 
> 

### <a name="benefits-of-application-packages"></a><span data-ttu-id="9a647-147">Uygulama paketleri yararları</span><span class="sxs-lookup"><span data-stu-id="9a647-147">Benefits of application packages</span></span>
<span data-ttu-id="9a647-148">Uygulama paketleri hello kodu Batch çözümü ve görevlerinizi çalıştırmak alt hello genel gider gerekli toomanage hello uygulamalarınızdaki basitleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a647-148">Application packages can simplify hello code in your Batch solution and lower hello overhead required toomanage hello applications that your tasks run.</span></span>

<span data-ttu-id="9a647-149">Uygulama paketleri ile havuzun görev başlatma toospecify hello düğümler üzerinde tek tek kaynak dosyaları tooinstall uzun bir listesi sahip değil.</span><span class="sxs-lookup"><span data-stu-id="9a647-149">With application packages, your pool's start task doesn't have toospecify a long list of individual resource files tooinstall on hello nodes.</span></span> <span data-ttu-id="9a647-150">Uygulama dosyalarınızı Azure Storage veya düğümlerinizi birden fazla sürümünü yönetmek toomanually yok.</span><span class="sxs-lookup"><span data-stu-id="9a647-150">You don't have toomanually manage multiple versions of your application files in Azure Storage, or on your nodes.</span></span> <span data-ttu-id="9a647-151">Ve oluşturma hakkında tooworry gerekmeyen [SAS URL'leri](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide depolama hesabınızdaki toohello dosyalara erişim.</span><span class="sxs-lookup"><span data-stu-id="9a647-151">And, you don't need tooworry about generating [SAS URLs](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide access toohello files in your Storage account.</span></span> <span data-ttu-id="9a647-152">Merhaba arka planda Azure Storage toostore uygulama paketleri ile Works toplu ve bunları toocompute düğümleri dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a647-152">Batch works in hello background with Azure Storage toostore application packages and deploy them toocompute nodes.</span></span>

> [!NOTE] 
> <span data-ttu-id="9a647-153">Merhaba toplam boyutu bir başlangıç görevi küçük veya buna eşit olmalıdır kaynak dosyaları ve ortam değişkenleri dahil, too32768 karakteri.</span><span class="sxs-lookup"><span data-stu-id="9a647-153">hello total size of a start task must be less than or equal too32768 characters, including resource files and environment variables.</span></span> <span data-ttu-id="9a647-154">Başlangıç görevi bu sınırı aşarsa, uygulama paketleri kullanarak başka bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="9a647-154">If your start task exceeds this limit, then using application packages is another option.</span></span> <span data-ttu-id="9a647-155">Ayrıca, kaynak dosyaları içeren bir sıkıştırılmış arşivi oluşturma blob tooAzure depolama karşıya yükleme ve hello komut satırından, başlangıç görevinin sıkıştırmasını açın.</span><span class="sxs-lookup"><span data-stu-id="9a647-155">You can also create a zipped archive containing your resource files, upload it as a blob tooAzure Storage, and then unzip it from hello command line of your start task.</span></span> 
>
>

## <a name="upload-and-manage-applications"></a><span data-ttu-id="9a647-156">Karşıya yükleme ve uygulamalarını yönetme</span><span class="sxs-lookup"><span data-stu-id="9a647-156">Upload and manage applications</span></span>
<span data-ttu-id="9a647-157">Merhaba kullanabilirsiniz [Azure portal] [ portal] veya hello [Batch yönetimi .NET](batch-management-dotnet.md) kitaplığı toomanage hello uygulama paketleri Batch hesabınızdaki.</span><span class="sxs-lookup"><span data-stu-id="9a647-157">You can use hello [Azure portal][portal] or hello [Batch Management .NET](batch-management-dotnet.md) library toomanage hello application packages in your Batch account.</span></span> <span data-ttu-id="9a647-158">Buna birkaç bölümler sonraki Merhaba, ilk nasıl toolink bir depolama hesabı sonra uygulamalarını ekleyerek ele almaktadır ve paketleri ve bunları yönetme portal hello gösteriyoruz.</span><span class="sxs-lookup"><span data-stu-id="9a647-158">In hello next few sections, we first show how toolink a Storage account, then discuss adding applications and packages and managing them with hello portal.</span></span>

### <a name="link-a-storage-account"></a><span data-ttu-id="9a647-159">Bir depolama hesabı bağlantı</span><span class="sxs-lookup"><span data-stu-id="9a647-159">Link a Storage account</span></span>
<span data-ttu-id="9a647-160">toouse uygulama paketleri, ilk Azure Storage hesabı tooyour toplu işlem hesabı bağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a647-160">toouse application packages, you must first link an Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="9a647-161">Henüz bir depolama hesabı yapılandırmadıysanız hello Azure portal uyarı hello hello'ı ilk kez görüntüler **uygulamaları** döşeme hello **Batch hesabı** dikey.</span><span class="sxs-lookup"><span data-stu-id="9a647-161">If you have not yet configured a Storage account, hello Azure portal displays a warning hello first time you click hello **Applications** tile in hello **Batch account** blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a647-162">Batch şu anda destekler *yalnızca* hello **genel amaçlı** 5. adımda açıklandığı gibi depolama hesabı türü [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account), [Azure hakkında Depolama hesapları](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="9a647-162">Batch currently supports *only* hello **General-purpose** storage account type as described in step 5, [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="9a647-163">Bir Azure depolama hesabı tooyour toplu işlem hesabı bağladığınızda, bağlantı *yalnızca* bir **genel amaçlı** depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="9a647-163">When you link an Azure Storage account tooyour Batch account, link *only* a **General-purpose** storage account.</span></span>
> 
> 

<span data-ttu-id="9a647-164">![Azure portalında 'depolama hesabı yapılandırıldı' uyarısı][9]</span><span class="sxs-lookup"><span data-stu-id="9a647-164">!['No storage account configured' warning in Azure portal][9]</span></span>

<span data-ttu-id="9a647-165">Merhaba Batch hizmetini kullanan hello depolama hesabı toostore, uygulama paketlerinizi ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="9a647-165">hello Batch service uses hello associated Storage account toostore your application packages.</span></span> <span data-ttu-id="9a647-166">Merhaba iki hesap bağladığınız sonra toplu hello bağlantılı depolama hesabı tooyour işlem düğümlerine depolanan hello paketleri otomatik olarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a647-166">After you've linked hello two accounts, Batch can automatically deploy hello packages stored in hello linked Storage account tooyour compute nodes.</span></span> <span data-ttu-id="9a647-167">toolink bir depolama hesabı tooyour Batch hesabını tıklatın **depolama hesabı ayarlarını** hello üzerinde **uyarı** dikey ve ardından **depolama hesabı** hello üzerinde**Depolama hesabı** dikey.</span><span class="sxs-lookup"><span data-stu-id="9a647-167">toolink a Storage account tooyour Batch account, click **Storage account settings** on hello **Warning** blade, and then click **Storage Account** on hello **Storage Account** blade.</span></span>

<span data-ttu-id="9a647-168">![Azure Portal'da depolama hesabı dikey seçin][10]</span><span class="sxs-lookup"><span data-stu-id="9a647-168">![Choose storage account blade in Azure portal][10]</span></span>

<span data-ttu-id="9a647-169">Bir depolama hesabı oluşturmanızı öneririz *özellikle* , toplu işlem hesabı ile kullanmak için ve burada seçin.</span><span class="sxs-lookup"><span data-stu-id="9a647-169">We recommend that you create a Storage account *specifically* for use with your Batch account, and select it here.</span></span> <span data-ttu-id="9a647-170">Hakkında ayrıntılar için toocreate bir depolama hesabı bkz "Bir depolama hesabı oluşturma" [hakkında Azure depolama hesapları](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="9a647-170">For details about how toocreate a storage account, see "Create a Storage account" in [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="9a647-171">Bir depolama hesabı oluşturduktan sonra daha sonra onu tooyour toplu işlem hesabı hello kullanarak bağlayabilirsiniz **depolama hesabı** dikey.</span><span class="sxs-lookup"><span data-stu-id="9a647-171">After you've created a Storage account, you can then link it tooyour Batch account by using hello **Storage Account** blade.</span></span>

> [!WARNING]
> <span data-ttu-id="9a647-172">Merhaba Batch hizmeti Azure Storage toostore, uygulama paketlerinizi blok blobları kullanır.</span><span class="sxs-lookup"><span data-stu-id="9a647-172">hello Batch service uses Azure Storage toostore your application packages as block blobs.</span></span> <span data-ttu-id="9a647-173">Olduğunuz [normal olarak ücretlendirilir] [ storage_pricing] hello blok blobu veri.</span><span class="sxs-lookup"><span data-stu-id="9a647-173">You are [charged as normal][storage_pricing] for hello block blob data.</span></span> <span data-ttu-id="9a647-174">Emin tooconsider hello boyutu ve uygulama paketlerinizi sayısı ve düzenli olarak kullanım dışı paketleri toominimize maliyetleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="9a647-174">Be sure tooconsider hello size and number of your application packages, and periodically remove deprecated packages toominimize costs.</span></span>
> 
> 

### <a name="view-current-applications"></a><span data-ttu-id="9a647-175">Geçerli uygulamaları görüntüle</span><span class="sxs-lookup"><span data-stu-id="9a647-175">View current applications</span></span>
<span data-ttu-id="9a647-176">Batch hesabınızdaki tooview hello Uygulamalar'a tıklayın hello **uygulamaları** hello görüntülerken hello soldaki menüde menü öğesi **Batch hesabı** dikey.</span><span class="sxs-lookup"><span data-stu-id="9a647-176">tooview hello applications in your Batch account, click hello **Applications** menu item in hello left menu while viewing hello **Batch account** blade.</span></span>

<span data-ttu-id="9a647-177">![Uygulamaları döşeme][2]</span><span class="sxs-lookup"><span data-stu-id="9a647-177">![Applications tile][2]</span></span>

<span data-ttu-id="9a647-178">Bu menü seçeneğini seçerek açar hello **uygulamaları** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="9a647-178">Selecting this menu option opens hello **Applications** blade:</span></span>

<span data-ttu-id="9a647-179">![Uygulamaları listeleme][3]</span><span class="sxs-lookup"><span data-stu-id="9a647-179">![List applications][3]</span></span>

<span data-ttu-id="9a647-180">Merhaba **uygulamaları** hesabınızdaki her bir uygulama Kimliğini hello ve aşağıdaki özelliklere hello dikey penceresinde görüntüler:</span><span class="sxs-lookup"><span data-stu-id="9a647-180">hello **Applications** blade displays hello ID of each application in your account and hello following properties:</span></span>

* <span data-ttu-id="9a647-181">**Paketleri**: Merhaba bu uygulamayla ilişkili sürüm sayısı.</span><span class="sxs-lookup"><span data-stu-id="9a647-181">**Packages**: hello number of versions associated with this application.</span></span>
* <span data-ttu-id="9a647-182">**Varsayılan sürüm**: hello uygulama havuzu için belirttiğinizde bir sürüm belirtmezseniz yüklü hello uygulama sürümü.</span><span class="sxs-lookup"><span data-stu-id="9a647-182">**Default version**: hello application version installed if you do not indicate a version when you specify hello application for a pool.</span></span> <span data-ttu-id="9a647-183">Bu ayar isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="9a647-183">This setting is optional.</span></span>
* <span data-ttu-id="9a647-184">**Güncelleştirmelere izin**: olup paketini güncelleştirir, silme ve eklemeleri belirten hello değeri izin verilir.</span><span class="sxs-lookup"><span data-stu-id="9a647-184">**Allow updates**: hello value that specifies whether package updates, deletions, and additions are allowed.</span></span> <span data-ttu-id="9a647-185">Bu çok ayarlanırsa**Hayır**, paket güncelleştirme ve silme işlemleri hello uygulama için devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="9a647-185">If this is set too**No**, package updates and deletions are disabled for hello application.</span></span> <span data-ttu-id="9a647-186">Yalnızca yeni uygulama paketi sürümleri eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="9a647-186">Only new application package versions can be added.</span></span> <span data-ttu-id="9a647-187">Merhaba varsayılandır **Evet**.</span><span class="sxs-lookup"><span data-stu-id="9a647-187">hello default is **Yes**.</span></span>

### <a name="view-application-details"></a><span data-ttu-id="9a647-188">Uygulama Ayrıntıları görüntüle</span><span class="sxs-lookup"><span data-stu-id="9a647-188">View application details</span></span>
<span data-ttu-id="9a647-189">bir uygulama, select hello uygulama hello ayrıntılarını hello içerir tooopen hello dikey **uygulamaları** dikey.</span><span class="sxs-lookup"><span data-stu-id="9a647-189">tooopen hello blade that includes hello details for an application, select hello application in hello **Applications** blade.</span></span>

<span data-ttu-id="9a647-190">![Uygulama Ayrıntıları][4]</span><span class="sxs-lookup"><span data-stu-id="9a647-190">![Application details][4]</span></span>

<span data-ttu-id="9a647-191">Merhaba uygulama ayrıntıları dikey penceresinde, uygulamanızın ayarlarını aşağıdaki hello yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a647-191">In hello application details blade, you can configure hello following settings for your application.</span></span>

* <span data-ttu-id="9a647-192">**Güncelleştirmelere izin**: uygulama paketlerinin güncelleştirilmiş veya silinebilir olup olmadığını belirtin.</span><span class="sxs-lookup"><span data-stu-id="9a647-192">**Allow updates**: Specify whether its application packages can be updated or deleted.</span></span> <span data-ttu-id="9a647-193">Bu makalenin sonraki bölümlerinde "Güncelleştirmek veya bir uygulama paketini silmeniz" bakın.</span><span class="sxs-lookup"><span data-stu-id="9a647-193">See "Update or Delete an application package" later in this article.</span></span>
* <span data-ttu-id="9a647-194">**Varsayılan sürüm**: varsayılan uygulama paketi toodeploy toocompute düğüm belirtin.</span><span class="sxs-lookup"><span data-stu-id="9a647-194">**Default version**: Specify a default application package toodeploy toocompute nodes.</span></span>
* <span data-ttu-id="9a647-195">**Görünen ad**: kolay bir çözüm hello uygulamayla ilgili bilgileri gibi hello tooyour müşterileri toplu ile sağlayan bir hizmet UI gösterildiğinde kullanabilir, Batch ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="9a647-195">**Display name**: Specify a friendly name that your Batch solution can use when it displays information about hello application, for example, in hello UI of a service that you provide tooyour customers through Batch.</span></span>

### <a name="add-a-new-application"></a><span data-ttu-id="9a647-196">Yeni bir uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="9a647-196">Add a new application</span></span>
<span data-ttu-id="9a647-197">toocreate yeni bir uygulama bir uygulama paketi eklemek ve yeni ve benzersiz uygulama kimliği belirtin.</span><span class="sxs-lookup"><span data-stu-id="9a647-197">toocreate a new application, add an application package and specify a new, unique application ID.</span></span> <span data-ttu-id="9a647-198">Merhaba yeni uygulama kimliği ile eklediğiniz hello ilk uygulama paketi de hello yeni bir uygulama oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9a647-198">hello first application package that you add with hello new application ID also creates hello new application.</span></span>

<span data-ttu-id="9a647-199">Tıklatın **Ekle** hello üzerinde **uygulamaları** dikey tooopen hello **yeni uygulama** dikey.</span><span class="sxs-lookup"><span data-stu-id="9a647-199">Click **Add** on hello **Applications** blade tooopen hello **New application** blade.</span></span>

<span data-ttu-id="9a647-200">![Azure portalında yeni uygulama dikey penceresi][5]</span><span class="sxs-lookup"><span data-stu-id="9a647-200">![New application blade in Azure portal][5]</span></span>

<span data-ttu-id="9a647-201">Merhaba **yeni uygulama** dikey penceresinde hello aşağıdaki alanlar yeni uygulama ve uygulama paketi toospecify hello ayarlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a647-201">hello **New application** blade provides hello following fields toospecify hello settings of your new application and application package.</span></span>

<span data-ttu-id="9a647-202">**Uygulama Kimliği**</span><span class="sxs-lookup"><span data-stu-id="9a647-202">**Application id**</span></span>

<span data-ttu-id="9a647-203">Bu alan konu toohello standart Azure toplu işlem kimliği doğrulama kuralları, yeni uygulama hello Kimliğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="9a647-203">This field specifies hello ID of your new application, which is subject toohello standard Azure Batch ID validation rules.</span></span> <span data-ttu-id="9a647-204">bir uygulama kimliği sağlamak için hello kurallar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9a647-204">hello rules for providing an application ID are as follows:</span></span>

* <span data-ttu-id="9a647-205">Windows düğümlerinde hello kimlik alfasayısal karakterler, tire ve alt çizgi, herhangi bir birleşimini içerebilir.</span><span class="sxs-lookup"><span data-stu-id="9a647-205">On Windows nodes, hello ID can contain any combination of alphanumeric characters, hyphens, and underscores.</span></span> <span data-ttu-id="9a647-206">Linux düğümleri üzerinde yalnızca alfasayısal karakterler ve alt çizgi izin verilir.</span><span class="sxs-lookup"><span data-stu-id="9a647-206">On Linux nodes, only alphanumeric characters and underscores are permitted.</span></span>
* <span data-ttu-id="9a647-207">Birden fazla 64 karakter içeremez.</span><span class="sxs-lookup"><span data-stu-id="9a647-207">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="9a647-208">Toplu işlem hesabı Hello içinde benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9a647-208">Must be unique within hello Batch account.</span></span>
* <span data-ttu-id="9a647-209">Servis talebi koruyarak ve büyük küçük harf duyarsız ' dir.</span><span class="sxs-lookup"><span data-stu-id="9a647-209">Is case-preserving and case-insensitive.</span></span>

<span data-ttu-id="9a647-210">**Sürüm**</span><span class="sxs-lookup"><span data-stu-id="9a647-210">**Version**</span></span>

<span data-ttu-id="9a647-211">Bu alan hello uygulama paketini karşıya yüklediğiniz hello sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="9a647-211">This field specifies hello version of hello application package you are uploading.</span></span> <span data-ttu-id="9a647-212">Sürüm dizelerini doğrulama kuralları aşağıdaki konu toohello şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9a647-212">Version strings are subject toohello following validation rules:</span></span>

* <span data-ttu-id="9a647-213">Windows düğümlerinde hello sürüm dizesi alfasayısal karakterler, tire, alt çizgi ve nokta herhangi bir birleşimini içerebilir.</span><span class="sxs-lookup"><span data-stu-id="9a647-213">On Windows nodes, hello version string can contain any combination of alphanumeric characters, hyphens, underscores, and periods.</span></span> <span data-ttu-id="9a647-214">Linux düğümleri üzerinde hello sürüm dizesi yalnızca alfasayısal karakterler ve alt çizgi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="9a647-214">On Linux nodes, hello version string can contain only alphanumeric characters and underscores.</span></span>
* <span data-ttu-id="9a647-215">Birden fazla 64 karakter içeremez.</span><span class="sxs-lookup"><span data-stu-id="9a647-215">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="9a647-216">Merhaba uygulama içinde benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9a647-216">Must be unique within hello application.</span></span>
* <span data-ttu-id="9a647-217">Servis talebi koruyarak ve büyük küçük harf duyarsız'dır.</span><span class="sxs-lookup"><span data-stu-id="9a647-217">Are case-preserving and case-insensitive.</span></span>

<span data-ttu-id="9a647-218">**Uygulama paketi**</span><span class="sxs-lookup"><span data-stu-id="9a647-218">**Application package**</span></span>

<span data-ttu-id="9a647-219">Bu alan hello uygulama ikili dosyaları içeren hello .zip dosyası ve gerekli tooexecute Merhaba uygulaması destekleyici dosyaları belirtir.</span><span class="sxs-lookup"><span data-stu-id="9a647-219">This field specifies hello .zip file that contains hello application binaries and supporting files that are required tooexecute hello application.</span></span> <span data-ttu-id="9a647-220">Merhaba tıklatın **bir dosya seçin** kutusu veya hello klasör simgesine toobrowse tooand uygulamanızın dosyaları içeren bir .zip dosyası seçin.</span><span class="sxs-lookup"><span data-stu-id="9a647-220">Click hello **Select a file** box or hello folder icon toobrowse tooand select a .zip file that contains your application's files.</span></span>

<span data-ttu-id="9a647-221">Bir dosyayı seçtikten sonra tıklayın **Tamam** toobegin hello karşıya yükleme tooAzure depolama.</span><span class="sxs-lookup"><span data-stu-id="9a647-221">After you've selected a file, click **OK** toobegin hello upload tooAzure Storage.</span></span> <span data-ttu-id="9a647-222">Merhaba karşıya yükleme işlemi tamamlandığında hello portalı bir bildirim görüntüler ve hello dikey penceresi kapanır.</span><span class="sxs-lookup"><span data-stu-id="9a647-222">When hello upload operation is complete, hello portal displays a notification and closes hello blade.</span></span> <span data-ttu-id="9a647-223">Merhaba dosya karşıya yükleme ve başlangıç hızı ağ bağlantınızın olduğunu Hello boyutuna bağlı olarak bu işlem biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="9a647-223">Depending on hello size of hello file that you are uploading and hello speed of your network connection, this operation may take some time.</span></span>

> [!WARNING]
> <span data-ttu-id="9a647-224">Merhaba kapatmayın **yeni uygulama** hello karşıya yükleme işlemi tamamlanmadan önce dikey.</span><span class="sxs-lookup"><span data-stu-id="9a647-224">Do not close hello **New application** blade before hello upload operation is complete.</span></span> <span data-ttu-id="9a647-225">Bunun yapılması hello karşıya yükleme işlemi durdurulacak.</span><span class="sxs-lookup"><span data-stu-id="9a647-225">Doing so will stop hello upload process.</span></span>
> 
> 

### <a name="add-a-new-application-package"></a><span data-ttu-id="9a647-226">Yeni bir uygulama paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="9a647-226">Add a new application package</span></span>
<span data-ttu-id="9a647-227">tooadd olan bir uygulamanın yeni bir uygulama Paket sürümü hello bir uygulama seçin **uygulamaları** dikey penceresinde tıklatın **paketleri**, ardından **Ekle** tooopen Merhaba **Ekle paket** dikey.</span><span class="sxs-lookup"><span data-stu-id="9a647-227">tooadd a new application package version for an existing application, select an application in hello **Applications** blade, click **Packages**, then click **Add** tooopen hello **Add package** blade.</span></span>

<span data-ttu-id="9a647-228">![Azure portalında uygulama paketi dikey ekleme][8]</span><span class="sxs-lookup"><span data-stu-id="9a647-228">![Add application package blade in Azure portal][8]</span></span>

<span data-ttu-id="9a647-229">Gördüğünüz gibi hello alanları hello eşleşen **yeni uygulama** dikey ancak hello **uygulama kimliği** kutusu devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="9a647-229">As you can see, hello fields match those of hello **New application** blade, but hello **Application id** box is disabled.</span></span> <span data-ttu-id="9a647-230">Merhaba yeni uygulaması için yaptığınız gibi hello belirtin **sürüm** tooyour yeni paketiniz için Gözat **uygulama paketi** .zip dosyası ve ardından **Tamam** tooupload hello Paket.</span><span class="sxs-lookup"><span data-stu-id="9a647-230">As you did for hello new application, specify hello **Version** for your new package, browse tooyour **Application package** .zip file, then click **OK** tooupload hello package.</span></span>

### <a name="update-or-delete-an-application-package"></a><span data-ttu-id="9a647-231">Güncelleştirme veya uygulama paketi silme</span><span class="sxs-lookup"><span data-stu-id="9a647-231">Update or delete an application package</span></span>
<span data-ttu-id="9a647-232">var olan bir uygulama paketini, açık hello ayrıntıları dikey penceresinde hello uygulama tooupdate veya Sil'i tıklatın **paketleri** tooopen hello **paketleri** dikey penceresinde hello tıklatın **üç nokta**toomodify istediğiniz ve seçin tooperform istediğiniz hello eylem hello uygulama paketini hello satırda.</span><span class="sxs-lookup"><span data-stu-id="9a647-232">tooupdate or delete an existing application package, open hello details blade for hello application, click **Packages** tooopen hello **Packages** blade, click hello **ellipsis** in hello row of hello application package that you want toomodify, and select hello action that you want tooperform.</span></span>

<span data-ttu-id="9a647-233">![Güncelleştirme veya Azure portalında paketi silme][7]</span><span class="sxs-lookup"><span data-stu-id="9a647-233">![Update or delete package in Azure portal][7]</span></span>

<span data-ttu-id="9a647-234">**Güncelleştirme**</span><span class="sxs-lookup"><span data-stu-id="9a647-234">**Update**</span></span>

<span data-ttu-id="9a647-235">Tıkladığınızda **güncelleştirme**, hello *güncelleştirme paketini* dikey penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9a647-235">When you click **Update**, hello *Update package* blade is displayed.</span></span> <span data-ttu-id="9a647-236">Bu dikey benzer toohello olan *yeni uygulama paketi* toospecify yeni bir ZIP dosyası tooupload izin vererek, ancak yalnızca hello paket seçimi alanını etkin, dikey.</span><span class="sxs-lookup"><span data-stu-id="9a647-236">This blade is similar toohello *New application package* blade, however only hello package selection field is enabled, allowing you toospecify a new ZIP file tooupload.</span></span>

<span data-ttu-id="9a647-237">![Güncelleştirme paketi dikey Azure portalında][11]</span><span class="sxs-lookup"><span data-stu-id="9a647-237">![Update package blade in Azure portal][11]</span></span>

<span data-ttu-id="9a647-238">**Silme**</span><span class="sxs-lookup"><span data-stu-id="9a647-238">**Delete**</span></span>

<span data-ttu-id="9a647-239">Tıkladığınızda **silmek**tooconfirm hello hello Paket sürümü silinmesini sorulur ve toplu Azure depolama biriminden hello paketini siler.</span><span class="sxs-lookup"><span data-stu-id="9a647-239">When you click **Delete**, you are asked tooconfirm hello deletion of hello package version, and Batch deletes hello package from Azure Storage.</span></span> <span data-ttu-id="9a647-240">Bir uygulamanın hello varsayılan sürümü silerseniz, hello **varsayılan sürüm** ayarı Merhaba uygulaması kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="9a647-240">If you delete hello default version of an application, hello **Default version** setting is removed for hello application.</span></span>

<span data-ttu-id="9a647-241">![Uygulama silme][12]</span><span class="sxs-lookup"><span data-stu-id="9a647-241">![Delete application ][12]</span></span>

## <a name="install-applications-on-compute-nodes"></a><span data-ttu-id="9a647-242">İşlem düğümlerinde uygulamaları yükleme</span><span class="sxs-lookup"><span data-stu-id="9a647-242">Install applications on compute nodes</span></span>
<span data-ttu-id="9a647-243">Artık nasıl hello Azure portal ile toomanage uygulama paketleri öğrendiğinize göre aşağıdakiler ele nasıl toodeploy bunları toocompute düğümleri ve toplu işlem görevleri ile çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9a647-243">Now that you've learned how toomanage application packages with hello Azure portal, we can discuss how toodeploy them toocompute nodes and run them with Batch tasks.</span></span>

### <a name="install-pool-application-packages"></a><span data-ttu-id="9a647-244">Havuz uygulama paketlerini yükleme</span><span class="sxs-lookup"><span data-stu-id="9a647-244">Install pool application packages</span></span>
<span data-ttu-id="9a647-245">tooinstall bir uygulama paketi tüm işlem düğümleri havuzunda, bir veya daha fazla uygulama paketi belirleyin *başvuruları* hello havuzu için.</span><span class="sxs-lookup"><span data-stu-id="9a647-245">tooinstall an application package on all compute nodes in a pool, specify one or more application package *references* for hello pool.</span></span> <span data-ttu-id="9a647-246">için bir havuz belirtin hello uygulama paketlerini her işlem düğümünde bu düğüme hello havuzu katıldığında ve hello düğümün yeniden başlatıldığı ya da zaman yüklenir.</span><span class="sxs-lookup"><span data-stu-id="9a647-246">hello application packages that you specify for a pool are installed on each compute node when that node joins hello pool, and when hello node is rebooted or reimaged.</span></span>

<span data-ttu-id="9a647-247">Batch .NET içinde bir veya daha fazla belirtin [CloudPool][net_cloudpool].[ ApplicationPackageReferences] [ net_cloudpool_pkgref] yeni bir havuz oluşturduğunuzda veya mevcut bir havuzu.</span><span class="sxs-lookup"><span data-stu-id="9a647-247">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span></span> <span data-ttu-id="9a647-248">Merhaba [ApplicationPackageReference] [ net_pkgref] sınıfı, bir uygulama kimliği ve sürüm tooinstall bulunan bir havuzdaki işlem düğümleri belirtir.</span><span class="sxs-lookup"><span data-stu-id="9a647-248">hello [ApplicationPackageReference][net_pkgref] class specifies an application ID and version tooinstall on a pool's compute nodes.</span></span>

```csharp
// Create hello unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify hello application and version tooinstall on hello compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit hello pool so that it's created in hello Batch service. As hello nodes join
// hello pool, hello specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="9a647-249">Bir uygulama paketi dağıtım için herhangi bir nedenle başarısız olursa, düğümün hello Batch hizmeti işaretleri hello [kullanılamaz][net_nodestate], ve bu düğümde yürütülmek zamanlanmış hiçbir görevler.</span><span class="sxs-lookup"><span data-stu-id="9a647-249">If an application package deployment fails for any reason, hello Batch service marks hello node [unusable][net_nodestate], and no tasks are scheduled for execution on that node.</span></span> <span data-ttu-id="9a647-250">Bu durumda, aşağıdakileri yapmalısınız **yeniden** hello düğümü tooreinitiate hello paketi dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="9a647-250">In this case, you should **restart** hello node tooreinitiate hello package deployment.</span></span> <span data-ttu-id="9a647-251">Görev hello düğümde yeniden zamanlamayı yeniden başlatmayı hello düğümü de sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a647-251">Restarting hello node also enables task scheduling again on hello node.</span></span>
> 
> 

### <a name="install-task-application-packages"></a><span data-ttu-id="9a647-252">Görev uygulama paketlerini yükleme</span><span class="sxs-lookup"><span data-stu-id="9a647-252">Install task application packages</span></span>
<span data-ttu-id="9a647-253">Benzer tooa havuzu, belirttiğiniz uygulama paketi *başvuruları* bir görev için.</span><span class="sxs-lookup"><span data-stu-id="9a647-253">Similar tooa pool, you specify application package *references* for a task.</span></span> <span data-ttu-id="9a647-254">Bir görev bir düğüm üzerinde zamanlanmış toorun olduğunda hello paket indirilir ve yalnızca hello görevin komut satırı yürütülmeden önce ayıklanan.</span><span class="sxs-lookup"><span data-stu-id="9a647-254">When a task is scheduled toorun on a node, hello package is downloaded and extracted just before hello task's command line is executed.</span></span> <span data-ttu-id="9a647-255">Belirtilen paket ve sürümü zaten yüklüyse hello düğümde, hello paket yüklenmez ve hello mevcut paketi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9a647-255">If a specified package and version is already installed on hello node, hello package is not downloaded and hello existing package is used.</span></span>

<span data-ttu-id="9a647-256">tooinstall bir görev uygulama paketi yapılandırma hello görevin [CloudTask][net_cloudtask].[ ApplicationPackageReferences] [ net_cloudtask_pkgref] özelliği:</span><span class="sxs-lookup"><span data-stu-id="9a647-256">tooinstall a task application package, configure hello task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span></span>

```csharp
CloudTask task =
    new CloudTask(
        "litwaretask001",
        "cmd /c %AZ_BATCH_APP_PACKAGE_LITWARE%\\litware.exe -args -here");

task.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference
    {
        ApplicationId = "litware",
        Version = "1.1001.2b"
    }
};
```

## <a name="execute-hello-installed-applications"></a><span data-ttu-id="9a647-257">Merhaba yüklü uygulamaları yürütme</span><span class="sxs-lookup"><span data-stu-id="9a647-257">Execute hello installed applications</span></span>
<span data-ttu-id="9a647-258">Merhaba, bir havuz ya da görev için belirttiğiniz paketleri karşıdan yüklenir ve hello dizininde adlı tooa ayıklanan `AZ_BATCH_ROOT_DIR` hello düğümü.</span><span class="sxs-lookup"><span data-stu-id="9a647-258">hello packages that you've specified for a pool or task are downloaded and extracted tooa named directory within hello `AZ_BATCH_ROOT_DIR` of hello node.</span></span> <span data-ttu-id="9a647-259">Toplu dizin adlı hello yolu toohello içeren bir ortam değişkeni de oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9a647-259">Batch also creates an environment variable that contains hello path toohello named directory.</span></span> <span data-ttu-id="9a647-260">Görev komut satırları Merhaba uygulaması hello düğümde başvururken bu ortam değişkenini kullanın.</span><span class="sxs-lookup"><span data-stu-id="9a647-260">Your task command lines use this environment variable when referencing hello application on hello node.</span></span> 

<span data-ttu-id="9a647-261">Windows düğümlerinde hello biçimini izleyen hello değişkenidir:</span><span class="sxs-lookup"><span data-stu-id="9a647-261">On Windows nodes, hello variable is in hello following format:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

<span data-ttu-id="9a647-262">Linux düğümleri üzerinde hello biçimi biraz farklıdır.</span><span class="sxs-lookup"><span data-stu-id="9a647-262">On Linux nodes, hello format is slightly different.</span></span> <span data-ttu-id="9a647-263">Nokta (.), kısa çizgi (-) ve numara işareti (#) olduğundan hello ortam değişkeninde düzleştirilmiş toounderscores.</span><span class="sxs-lookup"><span data-stu-id="9a647-263">Periods (.), hypens (-) and number signs (#) are flattened toounderscores in hello environment variable.</span></span> <span data-ttu-id="9a647-264">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="9a647-264">For example:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

<span data-ttu-id="9a647-265">`APPLICATIONID`ve `version` toohello uygulama ve Paket sürümü dağıtımı için belirtilen karşılık gelen değerler.</span><span class="sxs-lookup"><span data-stu-id="9a647-265">`APPLICATIONID` and `version` are values that correspond toohello application and package version you've specified for deployment.</span></span> <span data-ttu-id="9a647-266">Örneğin, uygulama sürümünün 2.7 belirtilmişse *blender* yüklenmesi gereken Windows düğümlerinde dosyalarından bu ortam değişkeni tooaccess görev komut satırları kullanır:</span><span class="sxs-lookup"><span data-stu-id="9a647-266">For example, if you specified that version 2.7 of application *blender* should be installed on Windows nodes, your task command lines would use this environment variable tooaccess its files:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

<span data-ttu-id="9a647-267">Linux düğümleri üzerinde hello ortam değişkeni bu biçimde belirtin:</span><span class="sxs-lookup"><span data-stu-id="9a647-267">On Linux nodes, specify hello environment variable in this format:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

<span data-ttu-id="9a647-268">Bir uygulama paketini karşıya yüklediğinizde, varsayılan sürüm toodeploy tooyour işlem düğümlerini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a647-268">When you upload an application package, you can specify a default version toodeploy tooyour compute nodes.</span></span> <span data-ttu-id="9a647-269">Bir uygulama için varsayılan bir sürümünün belirtilmişse Merhaba uygulaması başvurduğunuzda hello Sürüm soneki atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a647-269">If you have specified a default version for an application, you can omit hello version suffix when you reference hello application.</span></span> <span data-ttu-id="9a647-270">Merhaba varsayılan uygulama sürümü hello hello uygulamalar dikey penceresinde, Azure portal gösterildiği gibi belirleyebilirsiniz [karşıya yükleyin ve uygulamalarını yönetin](#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="9a647-270">You can specify hello default application version in hello Azure portal, on hello Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span></span>

<span data-ttu-id="9a647-271">Örneğin, "2.7" Merhaba uygulama için varsayılan sürüm olarak ayarlarsanız *blender*ve görevlerinizi ortam değişkeni aşağıdaki hello başvuru, sonra Windows düğümleriniz sürüm 2.7 çalıştırır:</span><span class="sxs-lookup"><span data-stu-id="9a647-271">For example, if you set "2.7" as hello default version for application *blender*, and your tasks reference hello following environment variable, then your Windows nodes will execute version 2.7:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER`

<span data-ttu-id="9a647-272">Merhaba aşağıdaki kod parçacığını gösterir hello hello varsayılan sürümü başlatan bir örnek görev komut satırı *blender* uygulama:</span><span class="sxs-lookup"><span data-stu-id="9a647-272">hello following code snippet shows an example task command line that launches hello default version of hello *blender* application:</span></span>

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> <span data-ttu-id="9a647-273">Bkz: [görevler için ortam ayarları](batch-api-basics.md#environment-settings-for-tasks) hello içinde [Batch özelliklerine genel bakış](batch-api-basics.md) işlem düğümü ortam ayarları hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="9a647-273">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in hello [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span></span>
> 
> 

## <a name="update-a-pools-application-packages"></a><span data-ttu-id="9a647-274">Bir havuzun uygulama paketlerini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="9a647-274">Update a pool's application packages</span></span>
<span data-ttu-id="9a647-275">Var olan bir havuzu bir uygulama paketiyle yapılandırılmış hello havuzu için yeni bir paket belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a647-275">If an existing pool has already been configured with an application package, you can specify a new package for hello pool.</span></span> <span data-ttu-id="9a647-276">Bir havuz için yeni bir paket başvuru belirtirseniz, hello aşağıdakileri uygulayın:</span><span class="sxs-lookup"><span data-stu-id="9a647-276">If you specify a new package reference for a pool, hello following apply:</span></span>

* <span data-ttu-id="9a647-277">Hello Batch hizmeti hello havuzuna Katıl tüm yeni düğümler ve herhangi bir düğümde, yeniden başlatıldığı ya da varolan hello yeni belirtilen paketi yükler.</span><span class="sxs-lookup"><span data-stu-id="9a647-277">hello Batch service installs hello newly specified package on all new nodes that join hello pool and on any existing node that is rebooted or reimaged.</span></span>
* <span data-ttu-id="9a647-278">Merhaba paket referanslarını güncelleştirdiğinizde zaten hello havuzunda düğümlerini hello yeni uygulama paketi otomatik olarak yüklemeyin işlem.</span><span class="sxs-lookup"><span data-stu-id="9a647-278">Compute nodes that are already in hello pool when you update hello package references do not automatically install hello new application package.</span></span> <span data-ttu-id="9a647-279">Bu, düğümlerin yeniden başlatılması gerekiyor veya görüntülenen tooreceive hello yeni paket işlem.</span><span class="sxs-lookup"><span data-stu-id="9a647-279">These compute nodes must be rebooted or reimaged tooreceive hello new package.</span></span>
* <span data-ttu-id="9a647-280">Yeni bir paket dağıtıldığında, ortam değişkenleri oluşturulan hello hello yeni uygulama paket referanslarını yansıtır.</span><span class="sxs-lookup"><span data-stu-id="9a647-280">When a new package is deployed, hello created environment variables reflect hello new application package references.</span></span>

<span data-ttu-id="9a647-281">Bu örnekte, hello varolan havuzu hello 2.7 sürümüne sahip *blender* biri olarak yapılandırılmış bir uygulama, [CloudPool][net_cloudpool].[ ApplicationPackageReferences][net_cloudpool_pkgref].</span><span class="sxs-lookup"><span data-stu-id="9a647-281">In this example, hello existing pool has version 2.7 of hello *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span></span> <span data-ttu-id="9a647-282">Yeni bir sürümle 2.76b, tooupdate hello havuzun düğümleri belirtin [ApplicationPackageReference] [ net_pkgref] hello yeni sürümü ve yürütme hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9a647-282">tooupdate hello pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with hello new version, and commit hello change.</span></span>

```csharp
string newVersion = "2.76b";
CloudPool boundPool = await batchClient.PoolOperations.GetPoolAsync("myPool");
boundPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "blender",
        Version = newVersion }
};
await boundPool.CommitAsync();
```

<span data-ttu-id="9a647-283">Merhaba yeni sürümü yapılandırıldı, hello Batch hizmeti sürüm 2.76b tooany yükler *yeni* hello havuzuna katılır düğümü.</span><span class="sxs-lookup"><span data-stu-id="9a647-283">Now that hello new version has been configured, hello Batch service installs version 2.76b tooany *new* node that joins hello pool.</span></span> <span data-ttu-id="9a647-284">Merhaba düğümleri üzerinde tooinstall 2.76b *zaten* hello havuzundaki yeniden veya onları yeniden görüntü oluşturma.</span><span class="sxs-lookup"><span data-stu-id="9a647-284">tooinstall 2.76b on hello nodes that are *already* in hello pool, reboot or reimage them.</span></span> <span data-ttu-id="9a647-285">Yeniden başlatılan düğümleri önceki paket dağıtımlarından hello dosyaları korumak unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9a647-285">Note that rebooted nodes retain hello files from previous package deployments.</span></span>

## <a name="list-hello-applications-in-a-batch-account"></a><span data-ttu-id="9a647-286">Bir Batch hesabında hello uygulamaları listeleme</span><span class="sxs-lookup"><span data-stu-id="9a647-286">List hello applications in a Batch account</span></span>
<span data-ttu-id="9a647-287">Hello kullanarak hello uygulamaları ve bunların paketleri bir Batch hesabında listeleyebilirsiniz [ApplicationOperations][net_appops].[ ListApplicationSummaries] [ net_appops_listappsummaries] yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9a647-287">You can list hello applications and their packages in a Batch account by using hello [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span></span>

```csharp
// List hello applications and their application packages in hello Batch account.
List<ApplicationSummary> applications = await batchClient.ApplicationOperations.ListApplicationSummaries().ToListAsync();
foreach (ApplicationSummary app in applications)
{
    Console.WriteLine("ID: {0} | Display Name: {1}", app.Id, app.DisplayName);

    foreach (string version in app.Versions)
    {
        Console.WriteLine("  {0}", version);
    }
}
```

## <a name="wrap-up"></a><span data-ttu-id="9a647-288">Kaydırma</span><span class="sxs-lookup"><span data-stu-id="9a647-288">Wrap up</span></span>
<span data-ttu-id="9a647-289">Uygulama paketleri ile işlerini hello uygulamaları seçin ve Batch özellikli hizmetinizi işleriyle işlerken hello tam sürümünü toouse belirtin, müşterilerinizin yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="9a647-289">With application packages, you can help your customers select hello applications for their jobs and specify hello exact version toouse when processing jobs with your Batch-enabled service.</span></span> <span data-ttu-id="9a647-290">Ayrıca, hizmetinizi kendi uygulamaları izlemek için müşteriler tooupload hello olanağı sunar. ve.</span><span class="sxs-lookup"><span data-stu-id="9a647-290">You might also provide hello ability for your customers tooupload and track their own applications in your service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a647-291">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9a647-291">Next steps</span></span>
* <span data-ttu-id="9a647-292">Merhaba [Batch REST API'si] [ api_rest] destek toowork ile uygulama paketleri de sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a647-292">hello [Batch REST API][api_rest] also provides support toowork with application packages.</span></span> <span data-ttu-id="9a647-293">Örneğin, hello bkz [applicationPackageReferences] [ rest_add_pool_with_packages] öğesinde [bir havuz tooan hesabı eklemek] [ rest_add_pool] hakkında bilgi için toospecify tooinstall hello REST API kullanarak paketler.</span><span class="sxs-lookup"><span data-stu-id="9a647-293">For example, see hello [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool tooan account][rest_add_pool] for information about how toospecify packages tooinstall by using hello REST API.</span></span> <span data-ttu-id="9a647-294">Bkz: [uygulamaları] [ rest_applications] nasıl tooobtain uygulama bilgilerini kullanarak hello Batch REST API'si hakkında ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="9a647-294">See [Applications][rest_applications] for details about how tooobtain application information by using hello Batch REST API.</span></span>
* <span data-ttu-id="9a647-295">Bilgi nasıl tooprogrammatically [Azure Batch hesaplarını ve kotalarını Batch yönetimi .NET ile yönetme](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="9a647-295">Learn how tooprogrammatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span></span> <span data-ttu-id="9a647-296">Merhaba [Batch yönetimi .NET][api_net_mgmt] kitaplığı, toplu uygulama veya hizmet hesabı oluşturma ve silme özellikleri etkinleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="9a647-296">hello [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span></span>

[api_net]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/client?view=azure-dotnet
[api_net_mgmt]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/management?view=azure-dotnet
[api_rest]: https://docs.microsoft.com/en-us/rest/api/batchservice/
[batch_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[github_samples]: https://github.com/Azure/azure-batch-samples
[storage_pricing]: https://azure.microsoft.com/pricing/details/storage/
[net_appops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.aspx
[net_appops_listappsummaries]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.listapplicationsummaries.aspx
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_cloudpool_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.applicationpackagereferences.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.aspx
[net_cloudtask_pkgref]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.applicationpackagereferences.aspx
[net_nodestate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.state.aspx
[net_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationpackagereference.aspx
[portal]: https://portal.azure.com
[rest_applications]: https://msdn.microsoft.com/library/azure/mt643945.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_pool_with_packages]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_apkgreference

[1]: ./media/batch-application-packages/app_pkg_01.png "Uygulama paketleri üst düzey diyagramı"
[2]: ./media/batch-application-packages/app_pkg_02.png "Azure portalında uygulamaları kutucuğu"
[3]: ./media/batch-application-packages/app_pkg_03.png "Azure portalında uygulamalar dikey penceresi"
[4]: ./media/batch-application-packages/app_pkg_04.png "Uygulama Ayrıntıları dikey Azure portalında"
[5]: ./media/batch-application-packages/app_pkg_05.png "Azure portalında yeni uygulama dikey penceresi"
[7]: ./media/batch-application-packages/app_pkg_07.png "Update veya delete paketleri açılan Azure portalında"
[8]: ./media/batch-application-packages/app_pkg_08.png "Azure portalında yeni uygulama paketi dikey penceresi"
[9]: ./media/batch-application-packages/app_pkg_09.png "Bağlantılı Depolama hesabı uyarı"
[10]: ./media/batch-application-packages/app_pkg_10.png "Azure Portal'da depolama hesabı dikey seçin"
[11]: ./media/batch-application-packages/app_pkg_11.png "Güncelleştirme paketi dikey Azure portalında"
[12]: ./media/batch-application-packages/app_pkg_12.png "Azure portalında paket onay iletişim Sil"
