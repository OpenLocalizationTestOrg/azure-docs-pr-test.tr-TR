---
title: "Machine Learning toplu yürütme hizmeti işleri için kapasite ayrılmış | Microsoft Docs"
description: "Machine Learning işleri için Azure Batch hizmetlerine genel bakış."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 3879eb3d0c6fa9d74fff01b07f5c07d3991dfbbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a><span data-ttu-id="5223a-103">Machine Learning işleri için Azure Batch hizmeti</span><span class="sxs-lookup"><span data-stu-id="5223a-103">Azure Batch service for Machine Learning jobs</span></span>

<span data-ttu-id="5223a-104">Machine Learning Batch havuzundaki işlem Azure Machine Learning toplu yürütme hizmeti için müşteri tarafından yönetilen ölçek sağlar.</span><span class="sxs-lookup"><span data-stu-id="5223a-104">Machine Learning Batch Pool processing provides customer-managed scale for the Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="5223a-105">Machine learning eşzamanlı iş sayısını sınırlayan bir çok kiracılı ortamında, gerçekleşir için Klasik toplu işleme gönderebilir ve işler ilk olarak ilk çıkar temelinde kuyruğa alınır.</span><span class="sxs-lookup"><span data-stu-id="5223a-105">Classic batch processing for machine learning takes place in a multi-tenant environment, which limits the number of concurrent jobs you can submit, and jobs are queued on a first-in-first-out basis.</span></span> <span data-ttu-id="5223a-106">Bu belirsizlik, doğru şekilde işinizi ne zaman çalışacağını tahmin edilemez olduğunu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="5223a-106">This uncertainty means that you can't accurately predict when your job will run.</span></span>

<span data-ttu-id="5223a-107">Batch havuzu işleme toplu işleri gönderebilmek için havuzları oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="5223a-107">Batch Pool processing allows you to create pools on which you can submit batch jobs.</span></span> <span data-ttu-id="5223a-108">Havuz boyutunu denetlemek ve hangi havuz iş gönderildiğinde.</span><span class="sxs-lookup"><span data-stu-id="5223a-108">You control the size of the pool, and to which pool the job is submitted.</span></span> <span data-ttu-id="5223a-109">BES işinizi tahmin edilebilir işlem performansı ve gönderdiğiniz işleme yükünü karşılık gelen kaynak havuzları oluşturmanıza olanak sağlayan kendi işleme alan çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="5223a-109">Your BES job runs in its own processing space providing predictable processing performance and the ability to create resource pools that correspond to the processing load that you submit.</span></span>

## <a name="how-to-use-batch-pool-processing"></a><span data-ttu-id="5223a-110">Batch havuzundaki işlem kullanma</span><span class="sxs-lookup"><span data-stu-id="5223a-110">How to use Batch Pool processing</span></span>

<span data-ttu-id="5223a-111">Azure portalı üzerinden yapılandırma havuzu toplu işlem şu anda kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="5223a-111">Configuration of Batch Pool Processing is not currently available through the Azure portal.</span></span> <span data-ttu-id="5223a-112">Batch havuzundaki işlem kullanmak için şunları yapmalısınız:</span><span class="sxs-lookup"><span data-stu-id="5223a-112">To use Batch Pool processing, you must:</span></span>

-   <span data-ttu-id="5223a-113">Batch havuzu hesabı oluşturmak ve bir havuz hizmet URL'sini ve bir yetkilendirme anahtarını elde etmek için CSS çağırın</span><span class="sxs-lookup"><span data-stu-id="5223a-113">Call CSS to create a Batch Pool Account and obtain a Pool Service URL and an authorization key</span></span>
-   <span data-ttu-id="5223a-114">Yeni kaynak tabanlı Manager web hizmeti ve fatura planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5223a-114">Create a New Resource Manager based web service and billing plan</span></span>

<span data-ttu-id="5223a-115">Hesabınızı oluşturmak için Microsoft Müşteri Hizmetleri ve desteği (CSS) arayın ve abonelik kimliğinizi sağlayın</span><span class="sxs-lookup"><span data-stu-id="5223a-115">To create your account, call Microsoft Customer Service and Support (CSS) and provide your Subscription ID.</span></span> <span data-ttu-id="5223a-116">CSS senaryonuz için uygun kapasitesini belirlemek için sizinle birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="5223a-116">CSS will work with you to determine the appropriate capacity for your scenario.</span></span> <span data-ttu-id="5223a-117">CSS sonra hesabınızı maksimum sayısı havuzu oluşturabilirsiniz ve her havuzda yerleştirebilirsiniz sanal makineler (VM'ler) üst sınırını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="5223a-117">CSS then configures your account with the maximum number of pools you can create and the maximum number of virtual machines (VMs) that you can place in each pool.</span></span> <span data-ttu-id="5223a-118">Hesabınızı yapılandırıldıktan sonra havuzu hizmet URL'niz ve bir yetkilendirme anahtarı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="5223a-118">Once your account is configured, you are provided your Pool Service URL and an authorization key.</span></span>

<span data-ttu-id="5223a-119">Hesabınızı oluşturduktan sonra Batch havuzundaki havuzu yönetim işlemlerini gerçekleştirmek için havuz hizmet URL'sini ve yetkilendirme tuşunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="5223a-119">After your account is created, you use the Pool Service URL and authorization key to perform pool management operations on your Batch Pool.</span></span>

![Batch havuzu hizmet mimarisi.](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

<span data-ttu-id="5223a-121">CSS size sağlanan havuz hizmet URL'si havuzu oluştur işlemi çağırarak havuzları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5223a-121">You create pools by calling the Create Pool operation on the pool service URL that CSS provided to you.</span></span> <span data-ttu-id="5223a-122">Bir havuz oluşturduğunuzda, Machine Learning web hizmeti VM'ler ve Yeni Kaynak Yöneticisi'nin swagger.json URL'sini sayısına dayalı belirtin.</span><span class="sxs-lookup"><span data-stu-id="5223a-122">When you create a pool, specify the number of VMs and the URL of the swagger.json of a New Resource Manager based Machine Learning web service.</span></span> <span data-ttu-id="5223a-123">Bu web Hizmeti'nin, fatura ilişkisi kurmak için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="5223a-123">This web service is provided to establish the billing association.</span></span> <span data-ttu-id="5223a-124">Batch havuzu hizmeti swagger.json havuzunu bir faturalandırma planı ile ilişkilendirmek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="5223a-124">The Batch Pool service uses the swagger.json to associate the pool with a billing plan.</span></span> <span data-ttu-id="5223a-125">Web hizmeti, iki yeni Resource Manager temelli herhangi BES çalıştırabilir ve klasik, havuzu seçin.</span><span class="sxs-lookup"><span data-stu-id="5223a-125">You can run any BES web service, both New Resource Manager based and classic, you choose on the pool.</span></span>

<span data-ttu-id="5223a-126">Tüm yeni Resource Manager temelli web hizmetini kullanır, ancak işleri için fatura ücretlendirilirsiniz, hizmetle ilişkili faturalandırma planı karşı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5223a-126">You can use any New Resource Manager based web service, but be aware that the billing for the jobs are charged against the billing plan associated with that service.</span></span> <span data-ttu-id="5223a-127">Bir web hizmeti ve özellikle Batch havuzu işlerini çalıştırmak için yeni fatura planı oluşturmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5223a-127">You may want to create a web service and new billing plan specifically for running Batch Pool jobs.</span></span>

<span data-ttu-id="5223a-128">Web hizmetleri oluşturma hakkında daha fazla bilgi için bkz: [bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="5223a-128">For more information on creating web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="5223a-129">Bir havuzu oluşturduktan sonra toplu iş isteklerini URL için web hizmetini kullanarak BES işi gönderin.</span><span class="sxs-lookup"><span data-stu-id="5223a-129">Once you have created a pool, you submit the BES job using the Batch Requests URL for the web service.</span></span> <span data-ttu-id="5223a-130">Bir havuz veya Klasik toplu işleme göndermek seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5223a-130">You can choose to submit it to a pool or to classic batch processing.</span></span> <span data-ttu-id="5223a-131">Toplu işlem havuzu için bir işi göndermek için iş gönderme istek gövdesi aşağıdaki parametresini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5223a-131">To submit a job to Batch Pool processing, you add the following parameter to the job submission request body:</span></span>

<span data-ttu-id="5223a-132">"AzureBatchPoolId": "&lt;kimliği havuzu&gt;"</span><span class="sxs-lookup"><span data-stu-id="5223a-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span></span>

<span data-ttu-id="5223a-133">Parametresini eklemezseniz iş Klasik toplu işlem ortamında çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="5223a-133">If you do not add the parameter, the job is run in the classic batch process environment.</span></span> <span data-ttu-id="5223a-134">Kullanılabilir kaynak havuzu varsa, iş çalıştırdıktan hemen başlar.</span><span class="sxs-lookup"><span data-stu-id="5223a-134">If the pool has available resources, the job starts running immediately.</span></span> <span data-ttu-id="5223a-135">Havuz kaynakları serbest bırakmak yoksa, bir kaynak kullanılabilir hale gelene kadar işinizi sıraya alındı.</span><span class="sxs-lookup"><span data-stu-id="5223a-135">If the pool does not have free resources, your job is queued until a resource is available.</span></span>

<span data-ttu-id="5223a-136">Düzenli olarak, havuzlarınızı kapasitesini ulaşmak ve artan kapasite gerektiğini fark ederseniz, CSS çağırın ve, kotalar artırmak için bir temsilcisi ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="5223a-136">If you find that you regularly reach the capacity of your pools, and you need increased capacity, you can call CSS and work with a representative to increase your quotas.</span></span>

<span data-ttu-id="5223a-137">Örnek isteği:</span><span class="sxs-lookup"><span data-stu-id="5223a-137">Example Request:</span></span>

<span data-ttu-id="5223a-138">https://ussouthcentral.Services.azureml.NET/Subscriptions/80c77c7674ba4c8c82294c3b2957990c/Services/9fe659022c9747e3b9b7b923c3830623/Jobs?api-Version=2.0</span><span class="sxs-lookup"><span data-stu-id="5223a-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span></span>

```json
{

    "Input":{
    
        "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpoint
        =https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://zhguim
        l.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;;",
        
        "BaseLocation":null,
        
        "RelativeLocation":"testint/AdultCensusIncomeBinaryClassificationDataset.csv",
        
        "SasBlobToken":null
    
    },
    
    "GlobalParameters":{ },
    
    "Outputs":{
    
        "output1":{
        
            "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpo
            int=https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://sampleaccount.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;",
            "BaseLocation":null,
            "RelativeLocation":"testintoutput/testint\_results.csv",
            
            "SasBlobToken":null
        
        }
    
    },
    
    "AzureBatchPoolId":"8dfc151b0d3e446497b845f3b29ef53b"

}
```

## <a name="considerations-when-using-batch-pool-processing"></a><span data-ttu-id="5223a-139">Batch havuzundaki işlem kullanmayla ilgili konular</span><span class="sxs-lookup"><span data-stu-id="5223a-139">Considerations when using Batch Pool processing</span></span>

<span data-ttu-id="5223a-140">Havuz toplu işleme bir her zaman açık Faturalanabilir hizmetidir ve bir Resource Manager temelli fatura planı ile ilişkilendirmenizi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5223a-140">Batch Pool Processing is an always-on billable service and that requires you to associate it with a Resource Manager based billing plan.</span></span> <span data-ttu-id="5223a-141">Havuz çalışan saat tutarında işlem için yalnızca faturalandırılır; o zaman havuzunu sırasında çalıştırmak işlerin sayısı ne olursa olsun.</span><span class="sxs-lookup"><span data-stu-id="5223a-141">You are only billed for the number of compute hours the pool is running; regardless of the number of jobs run during that time pool.</span></span> <span data-ttu-id="5223a-142">Bir havuzu oluşturursanız, havuzu silinene kadar toplu iş havuzda çalıştırıyor olsanız bile, her bir sanal makine havuzundaki işlem saatlik için faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="5223a-142">If you create a pool, you are billed for the compute hours of each virtual machine in the pool until the pool is deleted, even if no batch jobs are running in the pool.</span></span> <span data-ttu-id="5223a-143">Sanal makineler için fatura sağlama bittiğinde, başlatır ve silinmiş zaman durdurur.</span><span class="sxs-lookup"><span data-stu-id="5223a-143">Billing for the virtual machines starts when they have finished provisioning and stops when they have been deleted.</span></span> <span data-ttu-id="5223a-144">Bulunan planları birini kullanabilirsiniz [Machine Learning fiyatlandırması sayfa](https://azure.microsoft.com/pricing/details/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="5223a-144">You can use any of the plans found on the [Machine Learning Pricing page](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span>

<span data-ttu-id="5223a-145">Faturalama örnek:</span><span class="sxs-lookup"><span data-stu-id="5223a-145">Billing example:</span></span>

<span data-ttu-id="5223a-146">2 sanal makinelerle Batch havuzu oluşturma ve 24 saat sonra silerseniz, faturalandırma planınıza 48 işlem saatleri düşülür; kaç tane işleri bağımsız olarak, bu süre boyunca çalıştırılmadı.</span><span class="sxs-lookup"><span data-stu-id="5223a-146">If you create a Batch Pool with 2 virtual machines and delete it after 24 hours your billing plan is debited 48 compute hours; regardless of how many jobs were run during that period.</span></span>

<span data-ttu-id="5223a-147">4 sanal makinelerle Batch havuzu oluşturma ve 12 saat sonra silerseniz, faturalandırma planınıza ayrıca borç kaydedilen 48 işlem saattir.</span><span class="sxs-lookup"><span data-stu-id="5223a-147">If you create a Batch Pool with 4 virtual machines and delete it after 12 hours, your billing plan is also debited 48 compute hours.</span></span>

<span data-ttu-id="5223a-148">İşlerini tamamlandığında belirlemek için işin durumunu yoklama öneririz.</span><span class="sxs-lookup"><span data-stu-id="5223a-148">We recommend that you poll the job status to determine when jobs complete.</span></span> <span data-ttu-id="5223a-149">Çalışan tüm işleri tamamladığınızda, sanal makine sayısı sıfır havuzuna ayarlamak için havuzu yeniden boyutlandırma işlemi çağırın.</span><span class="sxs-lookup"><span data-stu-id="5223a-149">When all your jobs have finished running, call the Resize Pool operation to set the number of virtual machines in the pool to zero.</span></span> <span data-ttu-id="5223a-150">Çalışan tüm işleri tamamladığınızda havuzu kaynaklardaki kısa ve örneğin farklı bir fatura planı karşı faturalandırmak yeni bir havuz oluşturmak ihtiyacınız varsa havuzu yerine silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5223a-150">If you are short on pool resources and you need to create a new pool, for example to bill against a different billing plan, you can delete the pool instead when all your jobs have finished running.</span></span>


| <span data-ttu-id="5223a-151">**Batch havuzundaki işlemesini kullanın**</span><span class="sxs-lookup"><span data-stu-id="5223a-151">**Use Batch Pool Processing when**</span></span>    | <span data-ttu-id="5223a-152">**Klasik toplu ne zaman işleme kullanın**</span><span class="sxs-lookup"><span data-stu-id="5223a-152">**Use classic batch processing when**</span></span>  |
|---|---|
|<span data-ttu-id="5223a-153">Çok sayıda işlerini çalıştırmanız gerekir</span><span class="sxs-lookup"><span data-stu-id="5223a-153">You need to run a large number of jobs</span></span><br><span data-ttu-id="5223a-154">Veya</span><span class="sxs-lookup"><span data-stu-id="5223a-154">Or</span></span><br/><span data-ttu-id="5223a-155">İşleriniz hemen çalışacağını bilmeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="5223a-155">You need to know that your jobs will run immediately</span></span><br/><span data-ttu-id="5223a-156">Veya</span><span class="sxs-lookup"><span data-stu-id="5223a-156">Or</span></span><br/><span data-ttu-id="5223a-157">Garantili işleme gerekir.</span><span class="sxs-lookup"><span data-stu-id="5223a-157">You need guaranteed throughput.</span></span> <span data-ttu-id="5223a-158">Örneğin, belirli bir zaman dilimi içinde iş sayısı çalıştırın ve ihtiyaçlarınızı karşılamak için işlem kaynaklarınızı ölçeklendirmek istediğiniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5223a-158">For example, you need to run a number of jobs in a given time frame, and want to scale out your compute resources to meet your needs.</span></span>    | <span data-ttu-id="5223a-159">Yalnızca birkaç işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5223a-159">You are running just a few jobs</span></span><br/><span data-ttu-id="5223a-160">Ve</span><span class="sxs-lookup"><span data-stu-id="5223a-160">And</span></span><br/> <span data-ttu-id="5223a-161">İşlerin hemen çalıştırmanız gerekmez</span><span class="sxs-lookup"><span data-stu-id="5223a-161">You don’t need the jobs to run immediately</span></span> |
