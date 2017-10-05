---
title: "İşlem düğümlerinde - Azure Batch uygulama paketleri yükleme | Microsoft Docs"
description: "İşlem düğümlerini birden fazla uygulamaları ve sürümlerini toplu yükleme için kolayca yönetmek için Azure Batch uygulama paketleri özelliği kullanın."
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
ms.openlocfilehash: afcc04c80ec15872a22de5d5969a7ef6a583562f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-applications-to-compute-nodes-with-batch-application-packages"></a><span data-ttu-id="8548c-103">İşlem düğümleri Batch uygulama paketleri ile uygulamaları dağıtma</span><span class="sxs-lookup"><span data-stu-id="8548c-103">Deploy applications to compute nodes with Batch application packages</span></span>

<span data-ttu-id="8548c-104">Azure Batch uygulama paketleri özelliği kolay yönetim görev uygulamaları ve bunların dağıtımı havuzunuzdaki işlem düğümlerine sağlar.</span><span class="sxs-lookup"><span data-stu-id="8548c-104">The application packages feature of Azure Batch provides easy management of task applications and their deployment to the compute nodes in your pool.</span></span> <span data-ttu-id="8548c-105">Uygulama paketleri ile karşıya yükleyin ve bunların destekleyici dosyaları dahil olmak üzere, görevlerinizin çalışan uygulamaların birden fazla sürümünü yönetin.</span><span class="sxs-lookup"><span data-stu-id="8548c-105">With application packages, you can upload and manage multiple versions of the applications your tasks run, including their supporting files.</span></span> <span data-ttu-id="8548c-106">Ardından otomatik olarak bir veya daha fazla işlem düğümlerine bu uygulamaları havuzunuzdaki dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8548c-106">You can then automatically deploy one or more of these applications to the compute nodes in your pool.</span></span>

<span data-ttu-id="8548c-107">Bu makalede, karşıya yükleme ve uygulama paketleri Azure portalında yönetmek öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="8548c-107">In this article, you will learn how to upload and manage application packages in the Azure portal.</span></span> <span data-ttu-id="8548c-108">Ardından bunları bir havuzun işlem düğümleri ile yüklemek hakkında bilgi edineceksiniz [Batch .NET] [ api_net] kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="8548c-108">You will then learn how to install them on a pool's compute nodes with the [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="8548c-109">Uygulama paketleri 5 Temmuz 2017’den sonra oluşturulmuş tüm Batch havuzlarında desteklenir.</span><span class="sxs-lookup"><span data-stu-id="8548c-109">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="8548c-110">Bunların 10 Mart 2016 ve 5 Haziran 2017 arasında oluşturulmuş Batch havuzlarında desteklenebilmesi için, havuzun Bulut Hizmeti yapılandırması kullanılarak oluşturulmuş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8548c-110">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="8548c-111">10 Mart 2016’dan önce oluşturulan Batch havuzları uygulama paketlerini desteklemez.</span><span class="sxs-lookup"><span data-stu-id="8548c-111">Batch pools created prior to 10 March 2016 do not support application packages.</span></span>
>
> <span data-ttu-id="8548c-112">API'ları oluşturma ve uygulama paketlerini Yönetme [Batch yönetimi .NET] parçası olan [[api_net_mgmt]] kitaplık.</span><span class="sxs-lookup"><span data-stu-id="8548c-112">The APIs for creating and managing application packages are part of the [Batch Management .NET][[api_net_mgmt]] library.</span></span> <span data-ttu-id="8548c-113">Bir işlem düğümünde uygulama paketleri yüklemek için API'ler parçası olan [Batch .NET] [ api_net] kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="8548c-113">The APIs for installing application packages on a compute node are part of the [Batch .NET][api_net] library.</span></span>  
>
> <span data-ttu-id="8548c-114">Burada açıklanan uygulama paketleri özelliği, ' service'nın önceki sürümlerinde kullanılabilir toplu işlem uygulamaları özelliği yerini alır.</span><span class="sxs-lookup"><span data-stu-id="8548c-114">The application packages feature described here supersedes the Batch Apps feature available in previous versions of the service.</span></span>
> 
> 

## <a name="application-package-requirements"></a><span data-ttu-id="8548c-115">Uygulama paketi gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="8548c-115">Application package requirements</span></span>
<span data-ttu-id="8548c-116">Uygulama paketlerini kullanmak için gerek [bir Azure depolama hesabı bağlantı](#link-a-storage-account) Batch hesabınıza.</span><span class="sxs-lookup"><span data-stu-id="8548c-116">To use application packages, you need to [link an Azure Storage account](#link-a-storage-account) to your Batch account.</span></span>

<span data-ttu-id="8548c-117">Bu özellik sunulmuştur [Batch REST API'si] [ api_rest] sürüm 2015 12 01.2.2 ve karşılık gelen [Batch .NET] [ api_net] kitaplığı sürüm 3.1.0.</span><span class="sxs-lookup"><span data-stu-id="8548c-117">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and the corresponding [Batch .NET][api_net] library version 3.1.0.</span></span> <span data-ttu-id="8548c-118">Her zaman son API sürümü Batch ile çalışırken kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="8548c-118">We recommend that you always use the latest API version when working with Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="8548c-119">Uygulama paketleri 5 Temmuz 2017’den sonra oluşturulmuş tüm Batch havuzlarında desteklenir.</span><span class="sxs-lookup"><span data-stu-id="8548c-119">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="8548c-120">Bunların 10 Mart 2016 ve 5 Haziran 2017 arasında oluşturulmuş Batch havuzlarında desteklenebilmesi için, havuzun Bulut Hizmeti yapılandırması kullanılarak oluşturulmuş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8548c-120">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="8548c-121">10 Mart 2016’dan önce oluşturulan Batch havuzları uygulama paketlerini desteklemez.</span><span class="sxs-lookup"><span data-stu-id="8548c-121">Batch pools created prior to 10 March 2016 do not support application packages.</span></span>
>
>

## <a name="about-applications-and-application-packages"></a><span data-ttu-id="8548c-122">Uygulamalar ve uygulama paketleri hakkında</span><span class="sxs-lookup"><span data-stu-id="8548c-122">About applications and application packages</span></span>
<span data-ttu-id="8548c-123">Azure Batch içindeki bir *uygulama* havuzunuzdaki işlem düğümlerine otomatik olarak indirilebilir sürümü tutulan ikili dosyaları kümesine başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="8548c-123">Within Azure Batch, an *application* refers to a set of versioned binaries that can be automatically downloaded to the compute nodes in your pool.</span></span> <span data-ttu-id="8548c-124">Bir *uygulama paketi* başvurduğu bir *belirli* bu ikili dosyaları ve temsil bir verilen *sürüm* uygulamanın.</span><span class="sxs-lookup"><span data-stu-id="8548c-124">An *application package* refers to a *specific set* of those binaries and represents a given *version* of the application.</span></span>

<span data-ttu-id="8548c-125">![Uygulamalar ve uygulama paketleri üst düzey diyagramı][1]</span><span class="sxs-lookup"><span data-stu-id="8548c-125">![High-level diagram of applications and application packages][1]</span></span>

### <a name="applications"></a><span data-ttu-id="8548c-126">Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="8548c-126">Applications</span></span>
<span data-ttu-id="8548c-127">Toplu bir uygulamada içeriyor veya daha fazla uygulama paketleri ve uygulama için yapılandırma seçeneklerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="8548c-127">An application in Batch contains one or more application packages and specifies configuration options for the application.</span></span> <span data-ttu-id="8548c-128">Örneğin, uygulamanın işlem düğümlerini ve kendi paketleri olup güncelleştirilmiş veya silinebilir yüklemek için varsayılan uygulama paketi sürümü belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8548c-128">For example, an application can specify the default application package version to install on compute nodes and whether its packages can be updated or deleted.</span></span>

### <a name="application-packages"></a><span data-ttu-id="8548c-129">Uygulama paketleri</span><span class="sxs-lookup"><span data-stu-id="8548c-129">Application packages</span></span>
<span data-ttu-id="8548c-130">Bir uygulama paketi uygulama ikili dosyaları içeren bir .zip dosyası ve görevlerinizi uygulamayı çalıştırmak gerekli destek dosyaları ' dir.</span><span class="sxs-lookup"><span data-stu-id="8548c-130">An application package is a .zip file that contains the application binaries and supporting files that are required for your tasks to run the application.</span></span> <span data-ttu-id="8548c-131">Her uygulama paketi uygulamanın belirli bir sürümünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="8548c-131">Each application package represents a specific version of the application.</span></span>

<span data-ttu-id="8548c-132">Uygulama paketleri havuzu ve görev düzeylerde belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8548c-132">You can specify application packages at the pool and task levels.</span></span> <span data-ttu-id="8548c-133">Bir havuz veya görev oluşturduğunuzda, bir veya daha fazla bu paketleri ve (isteğe bağlı) bir sürüm belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8548c-133">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span></span>

* <span data-ttu-id="8548c-134">**Havuz uygulama paketleri** dağıtılan *her* havuzdaki düğüm.</span><span class="sxs-lookup"><span data-stu-id="8548c-134">**Pool application packages** are deployed to *every* node in the pool.</span></span> <span data-ttu-id="8548c-135">Bir düğüm bir havuzu katıldığında ve onu yeniden başlatıldığı ya da dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="8548c-135">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span></span>
  
    <span data-ttu-id="8548c-136">Bir havuzdaki tüm düğümlerin işe ait görevleri yürüttüğünüzde havuzu uygulama paketleri uygundur.</span><span class="sxs-lookup"><span data-stu-id="8548c-136">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span></span> <span data-ttu-id="8548c-137">Bir veya daha fazla uygulama paketlerini bir havuz oluşturduğunuzda ve ekleme veya güncelleştirme mevcut havuzun paketleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8548c-137">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span></span> <span data-ttu-id="8548c-138">Varolan bir havuzun uygulama paketleri güncelleştirirseniz, düğümlerinden yeni paketi yüklemek için yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8548c-138">If you update an existing pool's application packages, you must restart its nodes to install the new package.</span></span>
* <span data-ttu-id="8548c-139">**Görev uygulama paketleri** yalnızca görevin komut satırı çalıştırmadan önce bir görevi çalıştırmak için zamanlanan bir işlem düğümünde dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="8548c-139">**Task application packages** are deployed only to a compute node scheduled to run a task, just before running the task's command line.</span></span> <span data-ttu-id="8548c-140">Belirtilen uygulama paketinin ve sürüm ise zaten düğümde değil imzalanmasını ve var olan paketi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8548c-140">If the specified application package and version is already on the node, it is not redeployed and the existing package is used.</span></span>
  
    <span data-ttu-id="8548c-141">Görev uygulama paketleri Burada farklı işleri bir havuzu üzerinde çalışır ve bir iş tamamlandığında havuzu silinmez paylaşılan havuzu ortamlarında yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="8548c-141">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and the pool is not deleted when a job is completed.</span></span> <span data-ttu-id="8548c-142">İşinizin havuzdaki görevleri, düğümlerinden azsa uygulamanız yalnızca görevleri çalıştıran düğümlere dağıtıldığı için görev uygulama paketleri veri aktarımını azaltabilir.</span><span class="sxs-lookup"><span data-stu-id="8548c-142">If your job has fewer tasks than nodes in the pool, task application packages can minimize data transfer since your application is deployed only to the nodes that run tasks.</span></span>
  
    <span data-ttu-id="8548c-143">Büyük bir uygulamayı çalıştırma işleri görev uygulama paketi yararlanabilir diğer senaryolar verilmiştir ancak yalnızca birkaç görevler için.</span><span class="sxs-lookup"><span data-stu-id="8548c-143">Other scenarios that can benefit from task application packages are jobs that run a large application, but for only a few tasks.</span></span> <span data-ttu-id="8548c-144">Örneğin, önceden işlem aşamanın veya ön işleme veya birleştirme uygulama ağır olduğu, bir birleştirme görev görev uygulama paketlerini kullanma yararlı.</span><span class="sxs-lookup"><span data-stu-id="8548c-144">For example, a pre-processing stage or a merge task, where the pre-processing or merge application is heavyweight, may benefit from using task application packages.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8548c-145">Uygulamalar ve toplu işlem hesabı içindeki uygulama paketleri sayısını ve en fazla uygulama paket boyutu kısıtlamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="8548c-145">There are restrictions on the number of applications and application packages within a Batch account and on the maximum application package size.</span></span> <span data-ttu-id="8548c-146">Bkz: [Azure Batch hizmeti için kotalar ve sınırlar](batch-quota-limit.md) bu sınırları hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="8548c-146">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for details about these limits.</span></span>
> 
> 

### <a name="benefits-of-application-packages"></a><span data-ttu-id="8548c-147">Uygulama paketleri yararları</span><span class="sxs-lookup"><span data-stu-id="8548c-147">Benefits of application packages</span></span>
<span data-ttu-id="8548c-148">Uygulama paketleri, toplu Çözümünüzdeki kodu basitleştirmek ve görevlerinizi çalışan uygulamaları yönetmek için gerekli ek yükünü azaltın.</span><span class="sxs-lookup"><span data-stu-id="8548c-148">Application packages can simplify the code in your Batch solution and lower the overhead required to manage the applications that your tasks run.</span></span>

<span data-ttu-id="8548c-149">Uygulama paketleri ile uzun düğümlerine yüklemek için tek kaynak dosyaların listesini belirtmek, havuzun görev başlatma sahip değil.</span><span class="sxs-lookup"><span data-stu-id="8548c-149">With application packages, your pool's start task doesn't have to specify a long list of individual resource files to install on the nodes.</span></span> <span data-ttu-id="8548c-150">El ile uygulama dosyalarınızı Azure Storage veya düğümlerinizi birden fazla sürümünü yönetmek zorunda değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="8548c-150">You don't have to manually manage multiple versions of your application files in Azure Storage, or on your nodes.</span></span> <span data-ttu-id="8548c-151">Ve oluşturma hakkında endişelenmeniz gerekmez [SAS URL'leri](../storage/common/storage-dotnet-shared-access-signature-part-1.md) depolama hesabınızdaki dosyalarına erişim sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="8548c-151">And, you don't need to worry about generating [SAS URLs](../storage/common/storage-dotnet-shared-access-signature-part-1.md) to provide access to the files in your Storage account.</span></span> <span data-ttu-id="8548c-152">Batch uygulama paketleri depolamak ve bunlara işlem düğümleri dağıtmak için Azure Storage ile arka planda çalışır.</span><span class="sxs-lookup"><span data-stu-id="8548c-152">Batch works in the background with Azure Storage to store application packages and deploy them to compute nodes.</span></span>

> [!NOTE] 
> <span data-ttu-id="8548c-153">Bir başlangıç görevinin toplam boyutunun kaynak dosyaları ve ortam değişkenleri dahil olmak üzere 32.768 karakter veya daha az olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8548c-153">The total size of a start task must be less than or equal to 32768 characters, including resource files and environment variables.</span></span> <span data-ttu-id="8548c-154">Başlangıç görevi bu sınırı aşarsa, uygulama paketleri kullanarak başka bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="8548c-154">If your start task exceeds this limit, then using application packages is another option.</span></span> <span data-ttu-id="8548c-155">Ayrıca, kaynak dosyaları içeren bir sıkıştırılmış arşivi oluşturmak, bir BLOB Azure Storage olarak karşıya yükleme ve başlangıç görevinin komut satırından sıkıştırmasını açın.</span><span class="sxs-lookup"><span data-stu-id="8548c-155">You can also create a zipped archive containing your resource files, upload it as a blob to Azure Storage, and then unzip it from the command line of your start task.</span></span> 
>
>

## <a name="upload-and-manage-applications"></a><span data-ttu-id="8548c-156">Karşıya yükleme ve uygulamalarını yönetme</span><span class="sxs-lookup"><span data-stu-id="8548c-156">Upload and manage applications</span></span>
<span data-ttu-id="8548c-157">Kullanabileceğiniz [Azure portal] [ portal] veya [Batch yönetimi .NET](batch-management-dotnet.md) Batch hesabınızdaki uygulama paketlerini yönetmek için kitaplık.</span><span class="sxs-lookup"><span data-stu-id="8548c-157">You can use the [Azure portal][portal] or the [Batch Management .NET](batch-management-dotnet.md) library to manage the application packages in your Batch account.</span></span> <span data-ttu-id="8548c-158">Sonraki birkaç bölümlerde, biz öncelikle bir depolama hesabı bağlantı sonra ekleme uygulamaları ve paketleri ve portal ile yönetme ele gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8548c-158">In the next few sections, we first show how to link a Storage account, then discuss adding applications and packages and managing them with the portal.</span></span>

### <a name="link-a-storage-account"></a><span data-ttu-id="8548c-159">Bir depolama hesabı bağlantı</span><span class="sxs-lookup"><span data-stu-id="8548c-159">Link a Storage account</span></span>
<span data-ttu-id="8548c-160">Uygulama paketlerini kullanmak için bir Azure depolama hesabı toplu işlem hesabınıza bağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8548c-160">To use application packages, you must first link an Azure Storage account to your Batch account.</span></span> <span data-ttu-id="8548c-161">Henüz bir depolama hesabı yapılandırmadıysanız, Azure portal'ı ilk kez bir uyarı görüntüler **uygulamaları** parçasında **Batch hesabı** dikey.</span><span class="sxs-lookup"><span data-stu-id="8548c-161">If you have not yet configured a Storage account, the Azure portal displays a warning the first time you click the **Applications** tile in the **Batch account** blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8548c-162">Batch şu anda destekler *yalnızca* **genel amaçlı** 5. adımda açıklandığı gibi depolama hesabı türü [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account), [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="8548c-162">Batch currently supports *only* the **General-purpose** storage account type as described in step 5, [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="8548c-163">Batch hesabınıza bir Azure Storage hesabı bağladığınızda, bağlantı *yalnızca* bir **genel amaçlı** depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="8548c-163">When you link an Azure Storage account to your Batch account, link *only* a **General-purpose** storage account.</span></span>
> 
> 

<span data-ttu-id="8548c-164">![Azure portalında 'depolama hesabı yapılandırıldı' uyarısı][9]</span><span class="sxs-lookup"><span data-stu-id="8548c-164">!['No storage account configured' warning in Azure portal][9]</span></span>

<span data-ttu-id="8548c-165">Batch hizmeti, uygulama paketlerinizi depolamak için ilişkili depolama hesabı kullanır.</span><span class="sxs-lookup"><span data-stu-id="8548c-165">The Batch service uses the associated Storage account to store your application packages.</span></span> <span data-ttu-id="8548c-166">İki hesap bağladığınız sonra toplu işlem düğümleriniz bağlantılı depolama hesabına depolanan paketleri otomatik olarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8548c-166">After you've linked the two accounts, Batch can automatically deploy the packages stored in the linked Storage account to your compute nodes.</span></span> <span data-ttu-id="8548c-167">Bir depolama hesabı toplu işlem hesabınıza bağlamak için tıklatın **depolama hesabı ayarlarını** üzerinde **uyarı** dikey ve ardından **depolama hesabı** üzerinde **depolama hesabı** dikey.</span><span class="sxs-lookup"><span data-stu-id="8548c-167">To link a Storage account to your Batch account, click **Storage account settings** on the **Warning** blade, and then click **Storage Account** on the **Storage Account** blade.</span></span>

<span data-ttu-id="8548c-168">![Azure Portal'da depolama hesabı dikey seçin][10]</span><span class="sxs-lookup"><span data-stu-id="8548c-168">![Choose storage account blade in Azure portal][10]</span></span>

<span data-ttu-id="8548c-169">Bir depolama hesabı oluşturmanızı öneririz *özellikle* , toplu işlem hesabı ile kullanmak için ve burada seçin.</span><span class="sxs-lookup"><span data-stu-id="8548c-169">We recommend that you create a Storage account *specifically* for use with your Batch account, and select it here.</span></span> <span data-ttu-id="8548c-170">Bir depolama hesabının nasıl oluşturulacağı hakkında daha fazla ayrıntı için "Bir depolama hesabı oluşturma" görmek [hakkında Azure depolama hesapları](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="8548c-170">For details about how to create a storage account, see "Create a Storage account" in [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="8548c-171">Bir depolama hesabı oluşturduktan sonra daha sonra bu toplu işlem hesabınızı kullanarak bağlayabilirsiniz **depolama hesabı** dikey.</span><span class="sxs-lookup"><span data-stu-id="8548c-171">After you've created a Storage account, you can then link it to your Batch account by using the **Storage Account** blade.</span></span>

> [!WARNING]
> <span data-ttu-id="8548c-172">Batch hizmeti Azure Storage blok blobları, uygulama paketlerinizi depolamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="8548c-172">The Batch service uses Azure Storage to store your application packages as block blobs.</span></span> <span data-ttu-id="8548c-173">Olduğunuz [normal olarak ücretlendirilir] [ storage_pricing] blok blobu veri.</span><span class="sxs-lookup"><span data-stu-id="8548c-173">You are [charged as normal][storage_pricing] for the block blob data.</span></span> <span data-ttu-id="8548c-174">Uygulama paketlerinizi sayısı ve boyutu göz önünde bulundurun ve düzenli aralıklarla maliyetleri en aza indirmek için kullanım dışı paketleri kaldırmak emin olun.</span><span class="sxs-lookup"><span data-stu-id="8548c-174">Be sure to consider the size and number of your application packages, and periodically remove deprecated packages to minimize costs.</span></span>
> 
> 

### <a name="view-current-applications"></a><span data-ttu-id="8548c-175">Geçerli uygulamaları görüntüle</span><span class="sxs-lookup"><span data-stu-id="8548c-175">View current applications</span></span>
<span data-ttu-id="8548c-176">Batch hesabınızda uygulamaları görüntülemek için **uygulamaları** görüntüleme çalışırken soldaki menüde menü öğesi **Batch hesabı** dikey.</span><span class="sxs-lookup"><span data-stu-id="8548c-176">To view the applications in your Batch account, click the **Applications** menu item in the left menu while viewing the **Batch account** blade.</span></span>

<span data-ttu-id="8548c-177">![Uygulamaları döşeme][2]</span><span class="sxs-lookup"><span data-stu-id="8548c-177">![Applications tile][2]</span></span>

<span data-ttu-id="8548c-178">Bu menü seçeneğini seçerek açılır **uygulamaları** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="8548c-178">Selecting this menu option opens the **Applications** blade:</span></span>

<span data-ttu-id="8548c-179">![Uygulamaları listeleme][3]</span><span class="sxs-lookup"><span data-stu-id="8548c-179">![List applications][3]</span></span>

<span data-ttu-id="8548c-180">**Uygulamaları** dikey hesabınızı ve aşağıdaki özellikleri her uygulama Kimliğini görüntüler:</span><span class="sxs-lookup"><span data-stu-id="8548c-180">The **Applications** blade displays the ID of each application in your account and the following properties:</span></span>

* <span data-ttu-id="8548c-181">**Paketleri**: Bu uygulama ile ilişkili sürüm sayısı.</span><span class="sxs-lookup"><span data-stu-id="8548c-181">**Packages**: The number of versions associated with this application.</span></span>
* <span data-ttu-id="8548c-182">**Varsayılan sürüm**: uygulama havuzu için belirttiğinizde bir sürüm belirtmezseniz yüklü uygulama sürümü.</span><span class="sxs-lookup"><span data-stu-id="8548c-182">**Default version**: The application version installed if you do not indicate a version when you specify the application for a pool.</span></span> <span data-ttu-id="8548c-183">Bu ayar isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8548c-183">This setting is optional.</span></span>
* <span data-ttu-id="8548c-184">**Güncelleştirmelere izin**: olup paketini güncelleştirir, silme ve eklemeleri belirten değeri izin verilir.</span><span class="sxs-lookup"><span data-stu-id="8548c-184">**Allow updates**: The value that specifies whether package updates, deletions, and additions are allowed.</span></span> <span data-ttu-id="8548c-185">Bu ayarlanırsa **Hayır**, paket güncelleştirme ve silme işlemleri uygulama için devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="8548c-185">If this is set to **No**, package updates and deletions are disabled for the application.</span></span> <span data-ttu-id="8548c-186">Yalnızca yeni uygulama paketi sürümleri eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="8548c-186">Only new application package versions can be added.</span></span> <span data-ttu-id="8548c-187">Varsayılan değer **Evet**.</span><span class="sxs-lookup"><span data-stu-id="8548c-187">The default is **Yes**.</span></span>

### <a name="view-application-details"></a><span data-ttu-id="8548c-188">Uygulama Ayrıntıları görüntüle</span><span class="sxs-lookup"><span data-stu-id="8548c-188">View application details</span></span>
<span data-ttu-id="8548c-189">Bir uygulama ayrıntılarını içeren dikey penceresini açmak için uygulamada seçin **uygulamaları** dikey.</span><span class="sxs-lookup"><span data-stu-id="8548c-189">To open the blade that includes the details for an application, select the application in the **Applications** blade.</span></span>

<span data-ttu-id="8548c-190">![Uygulama Ayrıntıları][4]</span><span class="sxs-lookup"><span data-stu-id="8548c-190">![Application details][4]</span></span>

<span data-ttu-id="8548c-191">Uygulama Ayrıntıları dikey penceresinde, uygulamanız için aşağıdaki ayarları yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8548c-191">In the application details blade, you can configure the following settings for your application.</span></span>

* <span data-ttu-id="8548c-192">**Güncelleştirmelere izin**: uygulama paketlerinin güncelleştirilmiş veya silinebilir olup olmadığını belirtin.</span><span class="sxs-lookup"><span data-stu-id="8548c-192">**Allow updates**: Specify whether its application packages can be updated or deleted.</span></span> <span data-ttu-id="8548c-193">Bu makalenin sonraki bölümlerinde "Güncelleştirmek veya bir uygulama paketini silmeniz" bakın.</span><span class="sxs-lookup"><span data-stu-id="8548c-193">See "Update or Delete an application package" later in this article.</span></span>
* <span data-ttu-id="8548c-194">**Varsayılan sürüm**: işlem düğümleri dağıtmak için bir varsayılan uygulama paketi belirleyin.</span><span class="sxs-lookup"><span data-stu-id="8548c-194">**Default version**: Specify a default application package to deploy to compute nodes.</span></span>
* <span data-ttu-id="8548c-195">**Görünen ad**: Batch çözümünüzü uygulama hakkında bilgi Örneğin, Batch aracılığıyla müşterilerinize sağlayan bir hizmet UI gösterildiğinde kullanabileceğiniz bir kolay ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="8548c-195">**Display name**: Specify a friendly name that your Batch solution can use when it displays information about the application, for example, in the UI of a service that you provide to your customers through Batch.</span></span>

### <a name="add-a-new-application"></a><span data-ttu-id="8548c-196">Yeni bir uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="8548c-196">Add a new application</span></span>
<span data-ttu-id="8548c-197">Yeni bir uygulama oluşturmak için bir uygulama paketi eklemek ve yeni ve benzersiz uygulama kimliği belirtin.</span><span class="sxs-lookup"><span data-stu-id="8548c-197">To create a new application, add an application package and specify a new, unique application ID.</span></span> <span data-ttu-id="8548c-198">Yeni uygulama kimliği ile eklediğiniz ilk uygulama paketi, yeni uygulama da oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8548c-198">The first application package that you add with the new application ID also creates the new application.</span></span>

<span data-ttu-id="8548c-199">Tıklatın **Ekle** üzerinde **uygulamaları** açmak için dikey **yeni uygulama** dikey.</span><span class="sxs-lookup"><span data-stu-id="8548c-199">Click **Add** on the **Applications** blade to open the **New application** blade.</span></span>

<span data-ttu-id="8548c-200">![Azure portalında yeni uygulama dikey penceresi][5]</span><span class="sxs-lookup"><span data-stu-id="8548c-200">![New application blade in Azure portal][5]</span></span>

<span data-ttu-id="8548c-201">**Yeni uygulama** dikey yeni uygulama ve uygulama paketi ayarlarını belirlemek için aşağıdaki alanları sağlar.</span><span class="sxs-lookup"><span data-stu-id="8548c-201">The **New application** blade provides the following fields to specify the settings of your new application and application package.</span></span>

<span data-ttu-id="8548c-202">**Uygulama Kimliği**</span><span class="sxs-lookup"><span data-stu-id="8548c-202">**Application id**</span></span>

<span data-ttu-id="8548c-203">Bu alan tabi standart Azure toplu işlem kimliği doğrulama kuralları, yeni uygulama Kimliğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="8548c-203">This field specifies the ID of your new application, which is subject to the standard Azure Batch ID validation rules.</span></span> <span data-ttu-id="8548c-204">Bir uygulama kimliği sağlamak için kurallar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="8548c-204">The rules for providing an application ID are as follows:</span></span>

* <span data-ttu-id="8548c-205">Windows düğümlerinde kimlik alfasayısal karakterler, tire ve alt çizgi, herhangi bir birleşimini içerebilir.</span><span class="sxs-lookup"><span data-stu-id="8548c-205">On Windows nodes, the ID can contain any combination of alphanumeric characters, hyphens, and underscores.</span></span> <span data-ttu-id="8548c-206">Linux düğümleri üzerinde yalnızca alfasayısal karakterler ve alt çizgi izin verilir.</span><span class="sxs-lookup"><span data-stu-id="8548c-206">On Linux nodes, only alphanumeric characters and underscores are permitted.</span></span>
* <span data-ttu-id="8548c-207">Birden fazla 64 karakter içeremez.</span><span class="sxs-lookup"><span data-stu-id="8548c-207">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="8548c-208">Toplu işlem hesabı içinde benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8548c-208">Must be unique within the Batch account.</span></span>
* <span data-ttu-id="8548c-209">Servis talebi koruyarak ve büyük küçük harf duyarsız ' dir.</span><span class="sxs-lookup"><span data-stu-id="8548c-209">Is case-preserving and case-insensitive.</span></span>

<span data-ttu-id="8548c-210">**Sürüm**</span><span class="sxs-lookup"><span data-stu-id="8548c-210">**Version**</span></span>

<span data-ttu-id="8548c-211">Bu alan karşıya yüklemekte olduğunuz uygulama paketi sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="8548c-211">This field specifies the version of the application package you are uploading.</span></span> <span data-ttu-id="8548c-212">Sürüm dizelerini tabi aşağıdaki doğrulama kurallar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8548c-212">Version strings are subject to the following validation rules:</span></span>

* <span data-ttu-id="8548c-213">Windows düğümlerinde sürüm dizesi alfasayısal karakterler, tire, alt çizgi ve nokta herhangi bir birleşimini içerebilir.</span><span class="sxs-lookup"><span data-stu-id="8548c-213">On Windows nodes, the version string can contain any combination of alphanumeric characters, hyphens, underscores, and periods.</span></span> <span data-ttu-id="8548c-214">Linux düğümleri üzerinde sürüm dizesi yalnızca alfasayısal karakterler ve alt çizgi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="8548c-214">On Linux nodes, the version string can contain only alphanumeric characters and underscores.</span></span>
* <span data-ttu-id="8548c-215">Birden fazla 64 karakter içeremez.</span><span class="sxs-lookup"><span data-stu-id="8548c-215">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="8548c-216">Uygulama içinde benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8548c-216">Must be unique within the application.</span></span>
* <span data-ttu-id="8548c-217">Servis talebi koruyarak ve büyük küçük harf duyarsız'dır.</span><span class="sxs-lookup"><span data-stu-id="8548c-217">Are case-preserving and case-insensitive.</span></span>

<span data-ttu-id="8548c-218">**Uygulama paketi**</span><span class="sxs-lookup"><span data-stu-id="8548c-218">**Application package**</span></span>

<span data-ttu-id="8548c-219">Bu alan, uygulama yürütmek için gerekli destek dosyaları ve uygulama ikili dosyaları içeren .zip dosyasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="8548c-219">This field specifies the .zip file that contains the application binaries and supporting files that are required to execute the application.</span></span> <span data-ttu-id="8548c-220">Tıklatın **bir dosya seçin** kutusu veya göz atın ve uygulama dosyalarını içeren bir .zip dosyası seçmek için klasör simgesine.</span><span class="sxs-lookup"><span data-stu-id="8548c-220">Click the **Select a file** box or the folder icon to browse to and select a .zip file that contains your application's files.</span></span>

<span data-ttu-id="8548c-221">Bir dosyayı seçtikten sonra tıklayın **Tamam** Azure Storage yüklenecek başlamak için.</span><span class="sxs-lookup"><span data-stu-id="8548c-221">After you've selected a file, click **OK** to begin the upload to Azure Storage.</span></span> <span data-ttu-id="8548c-222">Karşıya yükleme işlemi tamamlandığında, portal bir bildirim görüntüler ve dikey penceresi kapanır.</span><span class="sxs-lookup"><span data-stu-id="8548c-222">When the upload operation is complete, the portal displays a notification and closes the blade.</span></span> <span data-ttu-id="8548c-223">Karşıya yüklemekte olduğunuz dosya boyutu ve ağ bağlantınızın hızına bağlı olarak, bu işlem biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="8548c-223">Depending on the size of the file that you are uploading and the speed of your network connection, this operation may take some time.</span></span>

> [!WARNING]
> <span data-ttu-id="8548c-224">Kapatmayın **yeni uygulama** karşıya yükleme işlemi tamamlanmadan önce dikey.</span><span class="sxs-lookup"><span data-stu-id="8548c-224">Do not close the **New application** blade before the upload operation is complete.</span></span> <span data-ttu-id="8548c-225">Bunun yapılması, karşıya yükleme işlemi durdurur.</span><span class="sxs-lookup"><span data-stu-id="8548c-225">Doing so will stop the upload process.</span></span>
> 
> 

### <a name="add-a-new-application-package"></a><span data-ttu-id="8548c-226">Yeni bir uygulama paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="8548c-226">Add a new application package</span></span>
<span data-ttu-id="8548c-227">Olan bir uygulamanın yeni bir uygulama Paket sürümü eklemek için bir uygulama seçin **uygulamaları** dikey penceresinde'ı tıklatın **paketleri**, ardından **Ekle** açmak için **Ekle paket** dikey.</span><span class="sxs-lookup"><span data-stu-id="8548c-227">To add a new application package version for an existing application, select an application in the **Applications** blade, click **Packages**, then click **Add** to open the **Add package** blade.</span></span>

<span data-ttu-id="8548c-228">![Azure portalında uygulama paketi dikey ekleme][8]</span><span class="sxs-lookup"><span data-stu-id="8548c-228">![Add application package blade in Azure portal][8]</span></span>

<span data-ttu-id="8548c-229">Gördüğünüz gibi alanların eşleşen **yeni uygulama** dikey penceresinde, ancak **uygulama kimliği** kutusu devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="8548c-229">As you can see, the fields match those of the **New application** blade, but the **Application id** box is disabled.</span></span> <span data-ttu-id="8548c-230">Yeni uygulama için yaptığınız gibi belirtin **sürüm** yeni paketiniz için göz atın, **uygulama paketi** .zip dosyası ve ardından **Tamam** paketini karşıya yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="8548c-230">As you did for the new application, specify the **Version** for your new package, browse to your **Application package** .zip file, then click **OK** to upload the package.</span></span>

### <a name="update-or-delete-an-application-package"></a><span data-ttu-id="8548c-231">Güncelleştirme veya uygulama paketi silme</span><span class="sxs-lookup"><span data-stu-id="8548c-231">Update or delete an application package</span></span>
<span data-ttu-id="8548c-232">Güncelleştirmek veya var olan uygulama paketini silmek için uygulama ayrıntıları dikey penceresini açmak, **paketleri** açmak için **paketleri** dikey penceresinde tıklatın **üç nokta** gerçekleştirmek istediğiniz eylemi seçin ve değiştirmek için istediğiniz uygulama paketi satırında.</span><span class="sxs-lookup"><span data-stu-id="8548c-232">To update or delete an existing application package, open the details blade for the application, click **Packages** to open the **Packages** blade, click the **ellipsis** in the row of the application package that you want to modify, and select the action that you want to perform.</span></span>

<span data-ttu-id="8548c-233">![Güncelleştirme veya Azure portalında paketi silme][7]</span><span class="sxs-lookup"><span data-stu-id="8548c-233">![Update or delete package in Azure portal][7]</span></span>

<span data-ttu-id="8548c-234">**Güncelleştirme**</span><span class="sxs-lookup"><span data-stu-id="8548c-234">**Update**</span></span>

<span data-ttu-id="8548c-235">Tıkladığınızda **güncelleştirme**, *güncelleştirme paketini* dikey penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8548c-235">When you click **Update**, the *Update package* blade is displayed.</span></span> <span data-ttu-id="8548c-236">Bu dikey benzer *yeni uygulama paketi* dikey penceresinde, ancak yalnızca karşıya yüklemek için yeni bir ZIP dosyası belirtmenize olanak sağlayan paket seçimi alan etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8548c-236">This blade is similar to the *New application package* blade, however only the package selection field is enabled, allowing you to specify a new ZIP file to upload.</span></span>

<span data-ttu-id="8548c-237">![Güncelleştirme paketi dikey Azure portalında][11]</span><span class="sxs-lookup"><span data-stu-id="8548c-237">![Update package blade in Azure portal][11]</span></span>

<span data-ttu-id="8548c-238">**Silme**</span><span class="sxs-lookup"><span data-stu-id="8548c-238">**Delete**</span></span>

<span data-ttu-id="8548c-239">Tıkladığınızda **silmek**, Paket sürümü silinmesini onaylaması istenir ve toplu Azure depolama biriminden paket siler.</span><span class="sxs-lookup"><span data-stu-id="8548c-239">When you click **Delete**, you are asked to confirm the deletion of the package version, and Batch deletes the package from Azure Storage.</span></span> <span data-ttu-id="8548c-240">Bir uygulamanın varsayılan sürümü silerseniz **varsayılan sürüm** ayarını, uygulama için kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="8548c-240">If you delete the default version of an application, the **Default version** setting is removed for the application.</span></span>

<span data-ttu-id="8548c-241">![Uygulama silme][12]</span><span class="sxs-lookup"><span data-stu-id="8548c-241">![Delete application ][12]</span></span>

## <a name="install-applications-on-compute-nodes"></a><span data-ttu-id="8548c-242">İşlem düğümlerinde uygulamaları yükleme</span><span class="sxs-lookup"><span data-stu-id="8548c-242">Install applications on compute nodes</span></span>
<span data-ttu-id="8548c-243">Azure portal ile uygulama paketlerini yönetmek nasıl öğrendiğinize göre bunları işlem düğümleri ve toplu görevleri çalıştırmak için dağıtma aşağıdakiler ele.</span><span class="sxs-lookup"><span data-stu-id="8548c-243">Now that you've learned how to manage application packages with the Azure portal, we can discuss how to deploy them to compute nodes and run them with Batch tasks.</span></span>

### <a name="install-pool-application-packages"></a><span data-ttu-id="8548c-244">Havuz uygulama paketlerini yükleme</span><span class="sxs-lookup"><span data-stu-id="8548c-244">Install pool application packages</span></span>
<span data-ttu-id="8548c-245">Bir havuzdaki tüm işlem düğümlerinde bir uygulama paketi yüklemek için bir veya daha fazla uygulama paketi belirleyin *başvuruları* havuzu için.</span><span class="sxs-lookup"><span data-stu-id="8548c-245">To install an application package on all compute nodes in a pool, specify one or more application package *references* for the pool.</span></span> <span data-ttu-id="8548c-246">Bir havuz için belirttiğiniz uygulama paketlerini her işlem düğümünde o düğüm havuza katıldığında ve düğümün yeniden başlatıldığı ya da yüklenir.</span><span class="sxs-lookup"><span data-stu-id="8548c-246">The application packages that you specify for a pool are installed on each compute node when that node joins the pool, and when the node is rebooted or reimaged.</span></span>

<span data-ttu-id="8548c-247">Batch .NET içinde bir veya daha fazla belirtin [CloudPool][net_cloudpool].[ ApplicationPackageReferences] [ net_cloudpool_pkgref] yeni bir havuz oluşturduğunuzda veya mevcut bir havuzu.</span><span class="sxs-lookup"><span data-stu-id="8548c-247">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span></span> <span data-ttu-id="8548c-248">[ApplicationPackageReference] [ net_pkgref] sınıfı, bir uygulama Kimliğini ve sürümünü bir havuzun üzerinde yüklemek için işlem düğümlerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="8548c-248">The [ApplicationPackageReference][net_pkgref] class specifies an application ID and version to install on a pool's compute nodes.</span></span>

```csharp
// Create the unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify the application and version to install on the compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit the pool so that it's created in the Batch service. As the nodes join
// the pool, the specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="8548c-249">Bir uygulama paketi dağıtım için herhangi bir nedenle başarısız olursa, Batch hizmeti düğüm işaretler [kullanılamaz][net_nodestate], ve bu düğümde yürütülmek zamanlanmış hiçbir görevler.</span><span class="sxs-lookup"><span data-stu-id="8548c-249">If an application package deployment fails for any reason, the Batch service marks the node [unusable][net_nodestate], and no tasks are scheduled for execution on that node.</span></span> <span data-ttu-id="8548c-250">Bu durumda, aşağıdakileri yapmalısınız **yeniden** paketi dağıtımı yeniden başlatmanız düğüme.</span><span class="sxs-lookup"><span data-stu-id="8548c-250">In this case, you should **restart** the node to reinitiate the package deployment.</span></span> <span data-ttu-id="8548c-251">Düğümü yeniden başlatmak, ayrıca görev düğümde yeniden zamanlamayı sağlar.</span><span class="sxs-lookup"><span data-stu-id="8548c-251">Restarting the node also enables task scheduling again on the node.</span></span>
> 
> 

### <a name="install-task-application-packages"></a><span data-ttu-id="8548c-252">Görev uygulama paketlerini yükleme</span><span class="sxs-lookup"><span data-stu-id="8548c-252">Install task application packages</span></span>
<span data-ttu-id="8548c-253">Benzer bir havuz için uygulama paketi belirttiğiniz *başvuruları* bir görev için.</span><span class="sxs-lookup"><span data-stu-id="8548c-253">Similar to a pool, you specify application package *references* for a task.</span></span> <span data-ttu-id="8548c-254">Bir görev, bir düğümü üzerinde çalışacak şekilde zamanlandığı paket indirilir ve yalnızca görevin komut satırı yürütülmeden önce ayıklanır.</span><span class="sxs-lookup"><span data-stu-id="8548c-254">When a task is scheduled to run on a node, the package is downloaded and extracted just before the task's command line is executed.</span></span> <span data-ttu-id="8548c-255">Belirtilen paket ve sürümü zaten yüklüyse, düğümde, paket yüklenmez ve var olan paketi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8548c-255">If a specified package and version is already installed on the node, the package is not downloaded and the existing package is used.</span></span>

<span data-ttu-id="8548c-256">Bir görev uygulama paketini yüklemek için görev yapılandırmanız [CloudTask][net_cloudtask].[ ApplicationPackageReferences] [ net_cloudtask_pkgref] özelliği:</span><span class="sxs-lookup"><span data-stu-id="8548c-256">To install a task application package, configure the task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span></span>

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

## <a name="execute-the-installed-applications"></a><span data-ttu-id="8548c-257">Yüklü uygulamalar yürütme</span><span class="sxs-lookup"><span data-stu-id="8548c-257">Execute the installed applications</span></span>
<span data-ttu-id="8548c-258">Bir havuz ya da görev için belirlediğiniz paketleri indirilir ve adlandırılmış bir dizin içinde ayıklanan `AZ_BATCH_ROOT_DIR` düğümün.</span><span class="sxs-lookup"><span data-stu-id="8548c-258">The packages that you've specified for a pool or task are downloaded and extracted to a named directory within the `AZ_BATCH_ROOT_DIR` of the node.</span></span> <span data-ttu-id="8548c-259">Toplu da adlandırılan bir dizin yolunu içeren bir ortam değişkeni oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8548c-259">Batch also creates an environment variable that contains the path to the named directory.</span></span> <span data-ttu-id="8548c-260">Görev komut satırları, düğümdeki uygulama başvururken bu ortam değişkenini kullanın.</span><span class="sxs-lookup"><span data-stu-id="8548c-260">Your task command lines use this environment variable when referencing the application on the node.</span></span> 

<span data-ttu-id="8548c-261">Windows düğümlerinde değişkeni şu biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="8548c-261">On Windows nodes, the variable is in the following format:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

<span data-ttu-id="8548c-262">Linux düğümleri üzerinde biçimi biraz farklıdır.</span><span class="sxs-lookup"><span data-stu-id="8548c-262">On Linux nodes, the format is slightly different.</span></span> <span data-ttu-id="8548c-263">Nokta (.), kısa çizgi (-) ve numara işareti (#) düzleştirilmiş ortam değişkeninde alt çizgi için.</span><span class="sxs-lookup"><span data-stu-id="8548c-263">Periods (.), hypens (-) and number signs (#) are flattened to underscores in the environment variable.</span></span> <span data-ttu-id="8548c-264">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8548c-264">For example:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

<span data-ttu-id="8548c-265">`APPLICATIONID`ve `version` dağıtımı için belirtilen uygulama ve Paket sürümü karşılık gelen değerler.</span><span class="sxs-lookup"><span data-stu-id="8548c-265">`APPLICATIONID` and `version` are values that correspond to the application and package version you've specified for deployment.</span></span> <span data-ttu-id="8548c-266">Örneğin, uygulama sürümünün 2.7 belirtilmişse *blender* yüklenmesi gereken Windows düğümlerinde, kendi dosyalarına erişmek için bu ortam değişkenini görev komut satırları kullanırsınız:</span><span class="sxs-lookup"><span data-stu-id="8548c-266">For example, if you specified that version 2.7 of application *blender* should be installed on Windows nodes, your task command lines would use this environment variable to access its files:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

<span data-ttu-id="8548c-267">Linux düğümleri üzerinde ortam değişkeni bu biçimde belirtin:</span><span class="sxs-lookup"><span data-stu-id="8548c-267">On Linux nodes, specify the environment variable in this format:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

<span data-ttu-id="8548c-268">Bir uygulama paketi yüklediğinizde, hesaplama düğümlerini dağıtmak için bir varsayılan sürümü belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8548c-268">When you upload an application package, you can specify a default version to deploy to your compute nodes.</span></span> <span data-ttu-id="8548c-269">Bir uygulama için varsayılan bir sürümünün belirtilirse, uygulama başvurduğunuzda Sürüm soneki atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8548c-269">If you have specified a default version for an application, you can omit the version suffix when you reference the application.</span></span> <span data-ttu-id="8548c-270">Varsayılan Uygulama sürümü Azure portalında uygulamalar dikey penceresinde gösterildiği gibi belirleyebilirsiniz [karşıya yükleyin ve uygulamalarını yönetin](#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="8548c-270">You can specify the default application version in the Azure portal, on the Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span></span>

<span data-ttu-id="8548c-271">Örneğin, "2.7" uygulaması için varsayılan sürüm olarak ayarlarsanız *blender*ve görevlerinizi aşağıdaki ortam değişkeni başvurusu, sonra Windows düğümleriniz sürüm 2.7 çalıştırır:</span><span class="sxs-lookup"><span data-stu-id="8548c-271">For example, if you set "2.7" as the default version for application *blender*, and your tasks reference the following environment variable, then your Windows nodes will execute version 2.7:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER`

<span data-ttu-id="8548c-272">Aşağıdaki kod parçacığını varsayılan sürümü başlatan bir örnek görev komut satırı gösterir *blender* uygulama:</span><span class="sxs-lookup"><span data-stu-id="8548c-272">The following code snippet shows an example task command line that launches the default version of the *blender* application:</span></span>

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> <span data-ttu-id="8548c-273">Bkz: [görevler için ortam ayarları](batch-api-basics.md#environment-settings-for-tasks) içinde [Batch özelliklerine genel bakış](batch-api-basics.md) işlem düğümü ortam ayarları hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="8548c-273">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in the [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span></span>
> 
> 

## <a name="update-a-pools-application-packages"></a><span data-ttu-id="8548c-274">Bir havuzun uygulama paketlerini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="8548c-274">Update a pool's application packages</span></span>
<span data-ttu-id="8548c-275">Var olan bir havuzu bir uygulama paketiyle yapılandırılmış havuzu için yeni bir paket belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8548c-275">If an existing pool has already been configured with an application package, you can specify a new package for the pool.</span></span> <span data-ttu-id="8548c-276">Aşağıdaki durumlardan bir havuz için yeni bir paket başvuru belirtirseniz:</span><span class="sxs-lookup"><span data-stu-id="8548c-276">If you specify a new package reference for a pool, the following apply:</span></span>

* <span data-ttu-id="8548c-277">Toplu işlem hizmeti yeni belirtilen paket havuzuna Katıl tüm yeni düğümler ve herhangi bir düğümde, yeniden başlatıldığı ya da varolan yükler.</span><span class="sxs-lookup"><span data-stu-id="8548c-277">The Batch service installs the newly specified package on all new nodes that join the pool and on any existing node that is rebooted or reimaged.</span></span>
* <span data-ttu-id="8548c-278">Paket referanslarını güncelleştirdiğinizde zaten havuzun düğümlerini otomatik olarak yeni uygulama paketi yükleme işlem.</span><span class="sxs-lookup"><span data-stu-id="8548c-278">Compute nodes that are already in the pool when you update the package references do not automatically install the new application package.</span></span> <span data-ttu-id="8548c-279">Bu, düğümler yeniden veya yeni paket almak için yeniden işlem.</span><span class="sxs-lookup"><span data-stu-id="8548c-279">These compute nodes must be rebooted or reimaged to receive the new package.</span></span>
* <span data-ttu-id="8548c-280">Yeni bir paket dağıtıldığında, oluşturulan ortam değişkenleri yeni uygulama paket referanslarını yansıtır.</span><span class="sxs-lookup"><span data-stu-id="8548c-280">When a new package is deployed, the created environment variables reflect the new application package references.</span></span>

<span data-ttu-id="8548c-281">Bu örnekte, var olan bir havuzu 2.7 sürümüne sahip *blender* biri olarak yapılandırılmış bir uygulama, [CloudPool][net_cloudpool].[ ApplicationPackageReferences][net_cloudpool_pkgref].</span><span class="sxs-lookup"><span data-stu-id="8548c-281">In this example, the existing pool has version 2.7 of the *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span></span> <span data-ttu-id="8548c-282">Havuzun düğümleri 2.76b sürümüyle güncelleştirmek için yeni bir belirtin [ApplicationPackageReference] [ net_pkgref] yeni sürümü ve yürütme Değiştir.</span><span class="sxs-lookup"><span data-stu-id="8548c-282">To update the pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with the new version, and commit the change.</span></span>

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

<span data-ttu-id="8548c-283">Yeni sürüm yapılandırılmış, Batch hizmeti sürüm 2.76b hiçbirine yükler *yeni* havuzuna katılır düğümü.</span><span class="sxs-lookup"><span data-stu-id="8548c-283">Now that the new version has been configured, the Batch service installs version 2.76b to any *new* node that joins the pool.</span></span> <span data-ttu-id="8548c-284">2.76b olan düğümlerine yüklemek için *zaten* havuzunda yeniden veya onları yeniden görüntü oluşturma.</span><span class="sxs-lookup"><span data-stu-id="8548c-284">To install 2.76b on the nodes that are *already* in the pool, reboot or reimage them.</span></span> <span data-ttu-id="8548c-285">Yeniden başlatılan düğümleri önceki paket dağıtımları dosyalarından korumak unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8548c-285">Note that rebooted nodes retain the files from previous package deployments.</span></span>

## <a name="list-the-applications-in-a-batch-account"></a><span data-ttu-id="8548c-286">Bir Batch hesabında uygulamaları Listele</span><span class="sxs-lookup"><span data-stu-id="8548c-286">List the applications in a Batch account</span></span>
<span data-ttu-id="8548c-287">Kullanarak uygulamalar ve bunların paketleri bir Batch hesabında listeleyebilirsiniz [ApplicationOperations][net_appops].[ ListApplicationSummaries] [ net_appops_listappsummaries] yöntemi.</span><span class="sxs-lookup"><span data-stu-id="8548c-287">You can list the applications and their packages in a Batch account by using the [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span></span>

```csharp
// List the applications and their application packages in the Batch account.
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

## <a name="wrap-up"></a><span data-ttu-id="8548c-288">Kaydırma</span><span class="sxs-lookup"><span data-stu-id="8548c-288">Wrap up</span></span>
<span data-ttu-id="8548c-289">Uygulama paketleri ile işlerini istediğiniz uygulamaları seçin ve Batch özellikli hizmetinizi işleriyle işlerken kullanılacak tam sürümünü belirtin, müşterilerinizin yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8548c-289">With application packages, you can help your customers select the applications for their jobs and specify the exact version to use when processing jobs with your Batch-enabled service.</span></span> <span data-ttu-id="8548c-290">Karşıya yükleme ve kendi uygulamalarında hizmetinizde izlemek müşterilerinize özelliği de sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="8548c-290">You might also provide the ability for your customers to upload and track their own applications in your service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8548c-291">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8548c-291">Next steps</span></span>
* <span data-ttu-id="8548c-292">[Batch REST API'si] [ api_rest] uygulama paketleri ile çalışmak için destek de sağlar.</span><span class="sxs-lookup"><span data-stu-id="8548c-292">The [Batch REST API][api_rest] also provides support to work with application packages.</span></span> <span data-ttu-id="8548c-293">Örneğin, [applicationPackageReferences] [ rest_add_pool_with_packages] öğesinde [bir havuz için bir hesap eklemek] [ rest_add_pool] REST API kullanarak yüklemek için paketler belirtme hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="8548c-293">For example, see the [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool to an account][rest_add_pool] for information about how to specify packages to install by using the REST API.</span></span> <span data-ttu-id="8548c-294">Bkz: [uygulamaları] [ rest_applications] Batch REST API'sini kullanarak uygulama bilgilerini elde etme hakkında ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="8548c-294">See [Applications][rest_applications] for details about how to obtain application information by using the Batch REST API.</span></span>
* <span data-ttu-id="8548c-295">Bilgi edinmek için nasıl programlı olarak [Azure Batch hesaplarını ve kotalarını Batch yönetimi .NET ile yönetme](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="8548c-295">Learn how to programmatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span></span> <span data-ttu-id="8548c-296">[Batch yönetimi .NET][api_net_mgmt] kitaplığı, toplu uygulama veya hizmet hesabı oluşturma ve silme özellikleri etkinleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="8548c-296">The [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span></span>

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
