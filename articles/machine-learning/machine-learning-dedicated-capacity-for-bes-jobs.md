---
title: "Machine Learning toplu yürütme hizmeti işleri için kapasite aaaDedicated | Microsoft Docs"
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
ms.openlocfilehash: bba7970bb31c50e5b0b9d5f4ff4f0d2dacf942e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a><span data-ttu-id="29868-103">Machine Learning işleri için Azure Batch hizmeti</span><span class="sxs-lookup"><span data-stu-id="29868-103">Azure Batch service for Machine Learning jobs</span></span>

<span data-ttu-id="29868-104">Machine Learning Batch havuzundaki işlem müşteri tarafından yönetilen ölçek hello Azure Machine Learning toplu yürütme hizmeti sağlar.</span><span class="sxs-lookup"><span data-stu-id="29868-104">Machine Learning Batch Pool processing provides customer-managed scale for hello Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="29868-105">Klasik toplu işleme Machine learning için ilk olarak ilk çıkar temelinde kuyruğa alınan hangi sınırları hello gönderebilir ve işleri eşzamanlı iş sayısı bir ortamda çok kiracılı, gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="29868-105">Classic batch processing for machine learning takes place in a multi-tenant environment, which limits hello number of concurrent jobs you can submit, and jobs are queued on a first-in-first-out basis.</span></span> <span data-ttu-id="29868-106">Bu belirsizlik, doğru şekilde işinizi ne zaman çalışacağını tahmin edilemez olduğunu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="29868-106">This uncertainty means that you can't accurately predict when your job will run.</span></span>

<span data-ttu-id="29868-107">Batch havuzu işleme toocreate havuzları toplu işleri gönderme sağlar.</span><span class="sxs-lookup"><span data-stu-id="29868-107">Batch Pool processing allows you toocreate pools on which you can submit batch jobs.</span></span> <span data-ttu-id="29868-108">Merhaba havuzu hello boyutunu denetlemek ve toowhich havuzu hello iş gönderilir.</span><span class="sxs-lookup"><span data-stu-id="29868-108">You control hello size of hello pool, and toowhich pool hello job is submitted.</span></span> <span data-ttu-id="29868-109">BES işinizi kendi alanı sağlamak işleme tahmin edilebilir işlem performansı ve gönderdiğiniz toohello işleme yükünü karşılık hello özelliği toocreate kaynak havuzları çalışır.</span><span class="sxs-lookup"><span data-stu-id="29868-109">Your BES job runs in its own processing space providing predictable processing performance and hello ability toocreate resource pools that correspond toohello processing load that you submit.</span></span>

## <a name="how-toouse-batch-pool-processing"></a><span data-ttu-id="29868-110">Nasıl toouse Batch havuzu işleme</span><span class="sxs-lookup"><span data-stu-id="29868-110">How toouse Batch Pool processing</span></span>

<span data-ttu-id="29868-111">Havuz toplu işleme yapılandırması hello Azure portal şu anda kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="29868-111">Configuration of Batch Pool Processing is not currently available through hello Azure portal.</span></span> <span data-ttu-id="29868-112">toouse Batch havuzundaki işlem yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="29868-112">toouse Batch Pool processing, you must:</span></span>

-   <span data-ttu-id="29868-113">Batch havuzu hesabı CSS toocreate çağırın ve bir havuz hizmet URL'si ve bir yetkilendirme anahtarı edinin</span><span class="sxs-lookup"><span data-stu-id="29868-113">Call CSS toocreate a Batch Pool Account and obtain a Pool Service URL and an authorization key</span></span>
-   <span data-ttu-id="29868-114">Yeni kaynak tabanlı Manager web hizmeti ve fatura planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="29868-114">Create a New Resource Manager based web service and billing plan</span></span>

<span data-ttu-id="29868-115">toocreate hesabınızı Microsoft Müşteri Hizmetleri ve desteği (CSS) arayın ve abonelik kimliğinizi girin</span><span class="sxs-lookup"><span data-stu-id="29868-115">toocreate your account, call Microsoft Customer Service and Support (CSS) and provide your Subscription ID.</span></span> <span data-ttu-id="29868-116">CSS, toodetermine hello uygun kapasiteli senaryonuz için çalışır.</span><span class="sxs-lookup"><span data-stu-id="29868-116">CSS will work with you toodetermine hello appropriate capacity for your scenario.</span></span> <span data-ttu-id="29868-117">CSS hesabınızı oluşturun ve her havuzda yerleştirebilirsiniz sanal makineler (VM) sayısı hello havuzları hello sayısı ardından yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="29868-117">CSS then configures your account with hello maximum number of pools you can create and hello maximum number of virtual machines (VMs) that you can place in each pool.</span></span> <span data-ttu-id="29868-118">Hesabınızı yapılandırıldıktan sonra havuzu hizmet URL'niz ve bir yetkilendirme anahtarı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="29868-118">Once your account is configured, you are provided your Pool Service URL and an authorization key.</span></span>

<span data-ttu-id="29868-119">Hesabınızı oluşturduktan sonra hello havuz hizmet URL'si ve yetkilendirme anahtar tooperform havuzu yönetim işlemlerini Batch havuzu kullanın.</span><span class="sxs-lookup"><span data-stu-id="29868-119">After your account is created, you use hello Pool Service URL and authorization key tooperform pool management operations on your Batch Pool.</span></span>

![Batch havuzu hizmet mimarisi.](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

<span data-ttu-id="29868-121">Bu sağlanan CSS tooyou hello havuzu hizmeti URL'si hello havuzu oluştur işlemi çağırarak havuzları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="29868-121">You create pools by calling hello Create Pool operation on hello pool service URL that CSS provided tooyou.</span></span> <span data-ttu-id="29868-122">Bir havuz oluşturduğunuzda, Machine Learning web hizmeti VM'ler ve hello swagger.json Yeni Kaynak Yöneticisi'nin hello URL'sini hello sayısına dayalı belirtin.</span><span class="sxs-lookup"><span data-stu-id="29868-122">When you create a pool, specify hello number of VMs and hello URL of hello swagger.json of a New Resource Manager based Machine Learning web service.</span></span> <span data-ttu-id="29868-123">Bu web Hizmeti'nin tooestablish hello fatura ilişkilendirme sağlanır.</span><span class="sxs-lookup"><span data-stu-id="29868-123">This web service is provided tooestablish hello billing association.</span></span> <span data-ttu-id="29868-124">Hello Batch havuzu hizmeti ile bir faturalandırma planı hello swagger.json tooassociate hello havuzu kullanır.</span><span class="sxs-lookup"><span data-stu-id="29868-124">hello Batch Pool service uses hello swagger.json tooassociate hello pool with a billing plan.</span></span> <span data-ttu-id="29868-125">Klasik, hello havuzunda seçtiğiniz ve web hizmeti, iki yeni Resource Manager temelli herhangi BES çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29868-125">You can run any BES web service, both New Resource Manager based and classic, you choose on hello pool.</span></span>

<span data-ttu-id="29868-126">Tüm yeni Resource Manager temelli web hizmetini kullanır, ancak hello faturalama hello işleri için ücretlendirilirsiniz, hizmetle ilişkili hello fatura planı karşı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="29868-126">You can use any New Resource Manager based web service, but be aware that hello billing for hello jobs are charged against hello billing plan associated with that service.</span></span> <span data-ttu-id="29868-127">Özellikle Batch havuzu işlerini çalıştırmak için bir web hizmeti ve yeni faturalandırma planı toocreate isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29868-127">You may want toocreate a web service and new billing plan specifically for running Batch Pool jobs.</span></span>

<span data-ttu-id="29868-128">Web hizmetleri oluşturma hakkında daha fazla bilgi için bkz: [bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="29868-128">For more information on creating web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="29868-129">Bir havuzu oluşturduktan sonra hello BES gönderme işlemini kullanarak toplu istekleri URL hello web hizmeti için hello.</span><span class="sxs-lookup"><span data-stu-id="29868-129">Once you have created a pool, you submit hello BES job using hello Batch Requests URL for hello web service.</span></span> <span data-ttu-id="29868-130">Toosubmit seçebilirsiniz, tooa havuzu veya tooclassic toplu işleme.</span><span class="sxs-lookup"><span data-stu-id="29868-130">You can choose toosubmit it tooa pool or tooclassic batch processing.</span></span> <span data-ttu-id="29868-131">bir iş tooBatch havuzu işleme toosubmit, parametre toohello iş gönderme istek gövdesi aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="29868-131">toosubmit a job tooBatch Pool processing, you add hello following parameter toohello job submission request body:</span></span>

<span data-ttu-id="29868-132">"AzureBatchPoolId": "&lt;kimliği havuzu&gt;"</span><span class="sxs-lookup"><span data-stu-id="29868-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span></span>

<span data-ttu-id="29868-133">Merhaba parametresini eklemezseniz hello iş hello Klasik toplu işlem ortamında çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="29868-133">If you do not add hello parameter, hello job is run in hello classic batch process environment.</span></span> <span data-ttu-id="29868-134">Merhaba havuzu kullanılabilir kaynakları varsa hello iş çalıştırdıktan hemen başlar.</span><span class="sxs-lookup"><span data-stu-id="29868-134">If hello pool has available resources, hello job starts running immediately.</span></span> <span data-ttu-id="29868-135">Merhaba havuzu kaynakları serbest bırakmak yoksa, bir kaynak kullanılabilir hale gelene kadar işinizi sıraya alındı.</span><span class="sxs-lookup"><span data-stu-id="29868-135">If hello pool does not have free resources, your job is queued until a resource is available.</span></span>

<span data-ttu-id="29868-136">Düzenli olarak, havuzlarınızı hello kapasitesini ulaşmak ve artan kapasite gerektiğini fark ederseniz, CSS çağırın ve, kotaları temsilcisi tooincrease ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="29868-136">If you find that you regularly reach hello capacity of your pools, and you need increased capacity, you can call CSS and work with a representative tooincrease your quotas.</span></span>

<span data-ttu-id="29868-137">Örnek isteği:</span><span class="sxs-lookup"><span data-stu-id="29868-137">Example Request:</span></span>

<span data-ttu-id="29868-138">https://ussouthcentral.Services.azureml.NET/Subscriptions/80c77c7674ba4c8c82294c3b2957990c/Services/9fe659022c9747e3b9b7b923c3830623/Jobs?api-Version=2.0</span><span class="sxs-lookup"><span data-stu-id="29868-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span></span>

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

## <a name="considerations-when-using-batch-pool-processing"></a><span data-ttu-id="29868-139">Batch havuzundaki işlem kullanmayla ilgili konular</span><span class="sxs-lookup"><span data-stu-id="29868-139">Considerations when using Batch Pool processing</span></span>

<span data-ttu-id="29868-140">Havuz toplu işleme bir her zaman açık Faturalanabilir hizmetidir ve Resource Manager ile fatura planı temel tooassociate olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="29868-140">Batch Pool Processing is an always-on billable service and that requires you tooassociate it with a Resource Manager based billing plan.</span></span> <span data-ttu-id="29868-141">İşlem saatleri hello havuzu çalıştıran hello sayısı için yalnızca faturalandırılır; o zaman havuzunu sırasında çalıştırmak işlerin sayısı Hello bağımsız olarak.</span><span class="sxs-lookup"><span data-stu-id="29868-141">You are only billed for hello number of compute hours hello pool is running; regardless of hello number of jobs run during that time pool.</span></span> <span data-ttu-id="29868-142">Bir havuzu oluşturursanız, hello havuzu silinene kadar toplu iş hello havuzunda çalıştırıyor olsanız bile, her sanal makinenin hello havuzunda hello işlem saatleri için faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="29868-142">If you create a pool, you are billed for hello compute hours of each virtual machine in hello pool until hello pool is deleted, even if no batch jobs are running in hello pool.</span></span> <span data-ttu-id="29868-143">Merhaba sanal makineler için fatura sağlama bittiğinde, başlatır ve silinmiş zaman durdurur.</span><span class="sxs-lookup"><span data-stu-id="29868-143">Billing for hello virtual machines starts when they have finished provisioning and stops when they have been deleted.</span></span> <span data-ttu-id="29868-144">Merhaba planı üzerinde hello bulunamadı birini kullanabilirsiniz [Machine Learning fiyatlandırması sayfa](https://azure.microsoft.com/pricing/details/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="29868-144">You can use any of hello plans found on hello [Machine Learning Pricing page](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span>

<span data-ttu-id="29868-145">Faturalama örnek:</span><span class="sxs-lookup"><span data-stu-id="29868-145">Billing example:</span></span>

<span data-ttu-id="29868-146">2 sanal makinelerle Batch havuzu oluşturma ve 24 saat sonra silerseniz, faturalandırma planınıza 48 işlem saatleri düşülür; kaç tane işleri bağımsız olarak, bu süre boyunca çalıştırılmadı.</span><span class="sxs-lookup"><span data-stu-id="29868-146">If you create a Batch Pool with 2 virtual machines and delete it after 24 hours your billing plan is debited 48 compute hours; regardless of how many jobs were run during that period.</span></span>

<span data-ttu-id="29868-147">4 sanal makinelerle Batch havuzu oluşturma ve 12 saat sonra silerseniz, faturalandırma planınıza ayrıca borç kaydedilen 48 işlem saattir.</span><span class="sxs-lookup"><span data-stu-id="29868-147">If you create a Batch Pool with 4 virtual machines and delete it after 12 hours, your billing plan is also debited 48 compute hours.</span></span>

<span data-ttu-id="29868-148">İşlerini tamamladığınızda hello iş durumu toodetermine yoklamak öneririz.</span><span class="sxs-lookup"><span data-stu-id="29868-148">We recommend that you poll hello job status toodetermine when jobs complete.</span></span> <span data-ttu-id="29868-149">Çalışan tüm işleri tamamladığınızda hello boyutlandırma havuzu işlemi tooset hello sanal makine sayısı hello havuzu toozero çağırın.</span><span class="sxs-lookup"><span data-stu-id="29868-149">When all your jobs have finished running, call hello Resize Pool operation tooset hello number of virtual machines in hello pool toozero.</span></span> <span data-ttu-id="29868-150">Çalışan tüm işleri tamamladığınızda havuzu kaynaklardaki kısa ve toocreate yeni bir havuz örneğin farklı bir fatura planı karşı toobill ihtiyacınız varsa hello havuzu yerine silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29868-150">If you are short on pool resources and you need toocreate a new pool, for example toobill against a different billing plan, you can delete hello pool instead when all your jobs have finished running.</span></span>


| <span data-ttu-id="29868-151">**Batch havuzundaki işlemesini kullanın**</span><span class="sxs-lookup"><span data-stu-id="29868-151">**Use Batch Pool Processing when**</span></span>    | <span data-ttu-id="29868-152">**Klasik toplu ne zaman işleme kullanın**</span><span class="sxs-lookup"><span data-stu-id="29868-152">**Use classic batch processing when**</span></span>  |
|---|---|
|<span data-ttu-id="29868-153">Toorun çok sayıda işleri gerekir</span><span class="sxs-lookup"><span data-stu-id="29868-153">You need toorun a large number of jobs</span></span><br><span data-ttu-id="29868-154">Veya</span><span class="sxs-lookup"><span data-stu-id="29868-154">Or</span></span><br/><span data-ttu-id="29868-155">İşleriniz hemen çalışacak tooknow gerekir</span><span class="sxs-lookup"><span data-stu-id="29868-155">You need tooknow that your jobs will run immediately</span></span><br/><span data-ttu-id="29868-156">Veya</span><span class="sxs-lookup"><span data-stu-id="29868-156">Or</span></span><br/><span data-ttu-id="29868-157">Garantili işleme gerekir.</span><span class="sxs-lookup"><span data-stu-id="29868-157">You need guaranteed throughput.</span></span> <span data-ttu-id="29868-158">Örneğin, toorun işleri belirli bir zaman çerçevesi içinde bir dizi gereksinim ve tooscale, işlem kaynakları toomeet gereksinimlerinizi istiyor.</span><span class="sxs-lookup"><span data-stu-id="29868-158">For example, you need toorun a number of jobs in a given time frame, and want tooscale out your compute resources toomeet your needs.</span></span>    | <span data-ttu-id="29868-159">Yalnızca birkaç işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="29868-159">You are running just a few jobs</span></span><br/><span data-ttu-id="29868-160">Ve</span><span class="sxs-lookup"><span data-stu-id="29868-160">And</span></span><br/> <span data-ttu-id="29868-161">Merhaba işleri toorun hemen gerekmez</span><span class="sxs-lookup"><span data-stu-id="29868-161">You don’t need hello jobs toorun immediately</span></span> |
