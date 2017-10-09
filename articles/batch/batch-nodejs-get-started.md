---
title: "aaaTutorial - Node.js için kullanım hello Azure Batch istemci kitaplığı | Microsoft Docs"
description: "Azure Batch temel kavramlarını Hello öğrenin ve Node.js kullanarak basit bir çözüm oluşturun."
services: batch
author: shwetams
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: nodejs
ms.topic: hero-article
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: shwetams
ms.openlocfilehash: d2b0ecbe764e7100affd7b02839aef3077b073cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-batch-sdk-for-nodejs"></a><span data-ttu-id="02207-103">Node.js için Batch SDK'sını kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="02207-103">Get started with Batch SDK for Node.js</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="02207-104">.NET</span><span class="sxs-lookup"><span data-stu-id="02207-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="02207-105">Python</span><span class="sxs-lookup"><span data-stu-id="02207-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="02207-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="02207-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="02207-107">Node.js kullanarak Batch istemci oluşturmanın hello temellerini öğrenin [Azure Batch Node.js SDK'sı](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span><span class="sxs-lookup"><span data-stu-id="02207-107">Learn hello basics of building a Batch client in Node.js using [Azure Batch Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span></span> <span data-ttu-id="02207-108">Batch uygulaması için bir senaryoyu anlayıp ardından bir Node.js istemcisi kullanarak bu senaryoyu ayarlama adımlarından oluşan bir yaklaşım uyguluyoruz.</span><span class="sxs-lookup"><span data-stu-id="02207-108">We take a step by step approach of understanding a scenario for a batch application and then setting it up using a Node.js client.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="02207-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="02207-109">Prerequisites</span></span>
<span data-ttu-id="02207-110">Bu makalede, Node.js hakkında bilgi sahibi olduğunuz ve Linux kullanmaya alışkın olduğunuz varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="02207-110">This article assumes that you have a working knowledge of Node.js and familiarity with Linux.</span></span> <span data-ttu-id="02207-111">Ayrıca, erişim hakları toocreate toplu işlem ve depolama hizmetleri ile bir Azure hesabı kurulumu sahip olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="02207-111">It also assumes that you have an Azure account setup with access rights toocreate Batch and Storage services.</span></span>

<span data-ttu-id="02207-112">Okuma öneririz [Azure Batch teknik genel bakış](batch-technical-overview.md) geçmeden önce hello adımları bu makalede açıklanan.</span><span class="sxs-lookup"><span data-stu-id="02207-112">We recommend reading [Azure Batch Technical Overview](batch-technical-overview.md) before you go through hello steps outlined this article.</span></span>

## <a name="hello-tutorial-scenario"></a><span data-ttu-id="02207-113">Merhaba öğretici senaryo</span><span class="sxs-lookup"><span data-stu-id="02207-113">hello tutorial scenario</span></span>
<span data-ttu-id="02207-114">Bize hello toplu iş akışı senaryo anlayın.</span><span class="sxs-lookup"><span data-stu-id="02207-114">Let us understand hello batch workflow scenario.</span></span> <span data-ttu-id="02207-115">Tüm csv tooJSON dönüştürür ve bir Azure Blob Depolama kapsayıcıdan dosyaları indirir Python içinde yazılmış basit bir komut dosyası sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="02207-115">We have a simple script written in Python that downloads all csv files from an Azure Blob storage container and converts them tooJSON.</span></span> <span data-ttu-id="02207-116">tooprocess birden çok depolama hesabı paralel kapsayıcılar, biz hello betik bir Azure toplu iş olarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02207-116">tooprocess multiple storage account containers in parallel, we can deploy hello script as an Azure Batch job.</span></span>

## <a name="azure-batch-architecture"></a><span data-ttu-id="02207-117">Azure Batch Mimarisi</span><span class="sxs-lookup"><span data-stu-id="02207-117">Azure Batch Architecture</span></span>
<span data-ttu-id="02207-118">Merhaba Aşağıdaki diyagramda nasıl biz Azure Batch ve Node.js istemci kullanılarak hello Python komut ölçeklendirebilirsiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="02207-118">hello following diagram depicts how we can scale hello Python script using Azure Batch and a Node.js client.</span></span>

![Azure Batch Senaryosu](./media/batch-nodejs-get-started/BatchScenario.png)

<span data-ttu-id="02207-120">Merhaba node.js istemci toplu iş hazırlama göreve (daha sonra ayrıntılı olarak açıklanmıştır) ve bir dizi görevi hello depolama hesabı kapsayıcı hello sayısı bağlı olarak dağıtır.</span><span class="sxs-lookup"><span data-stu-id="02207-120">hello node.js client deploys a batch job with a preparation task (explained in detail later) and a set of tasks depending on hello number of containers in hello storage account.</span></span> <span data-ttu-id="02207-121">Merhaba github'da depodan hello betikleri indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02207-121">You can download hello scripts from hello github repository.</span></span>

* [<span data-ttu-id="02207-122">Node.js istemcisi</span><span class="sxs-lookup"><span data-stu-id="02207-122">Node.js client</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [<span data-ttu-id="02207-123">Hazırlık görevi kabuk betikleri</span><span class="sxs-lookup"><span data-stu-id="02207-123">Preparation task shell scripts</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [<span data-ttu-id="02207-124">Python csv tooJSON işlemci</span><span class="sxs-lookup"><span data-stu-id="02207-124">Python csv tooJSON processor</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> <span data-ttu-id="02207-125">Merhaba Node.js istemci belirtilen hello bağlantısında bir Azure işlevi uygulama olarak dağıtılan belirli bir kod toobe içermiyor.</span><span class="sxs-lookup"><span data-stu-id="02207-125">hello Node.js client in hello link specified does not contain specific code toobe deployed as an Azure function app.</span></span> <span data-ttu-id="02207-126">Bağlantıları yönergeleri toocreate biri için aşağıdaki toohello başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="02207-126">You can refer toohello following links for instructions toocreate one.</span></span>
> - [<span data-ttu-id="02207-127">İşlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="02207-127">Create function app</span></span>](../azure-functions/functions-create-first-azure-function.md)
> - [<span data-ttu-id="02207-128">Zamanlayıcı tetikleyicisi işlevi oluşturma</span><span class="sxs-lookup"><span data-stu-id="02207-128">Create timer trigger function</span></span>](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-hello-application"></a><span data-ttu-id="02207-129">Merhaba uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="02207-129">Build hello application</span></span>

<span data-ttu-id="02207-130">Şimdi, bize hello işlemi adım adım hello Node.js istemci oluşturmakla izleyin:</span><span class="sxs-lookup"><span data-stu-id="02207-130">Now, let us follow hello process step by step into building hello Node.js client:</span></span>

### <a name="step-1-install-azure-batch-sdk"></a><span data-ttu-id="02207-131">1. Adım: Azure Batch SDK’sını yükleme</span><span class="sxs-lookup"><span data-stu-id="02207-131">Step 1: Install Azure Batch SDK</span></span>

<span data-ttu-id="02207-132">Merhaba npm yükleme komutunu kullanarak Node.js için Azure Batch SDK'sı yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02207-132">You can install Azure Batch SDK for Node.js using hello npm install command.</span></span>

`npm install azure-batch`

<span data-ttu-id="02207-133">Bu komut hello azure toplu işlem düğüm SDK en son sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="02207-133">This command installs hello latest version of azure-batch node SDK.</span></span>

>[!Tip]
> <span data-ttu-id="02207-134">Bir Azure işlevi uygulamada gittiğiniz çok "Kudu konsolunda" Merhaba Azure işlevi ait ayarları sekmesinde toorun hello npm yükleme komutlarını.</span><span class="sxs-lookup"><span data-stu-id="02207-134">In an Azure Function app, you can go too"Kudu Console" in hello Azure function's Settings tab toorun hello npm install commands.</span></span> <span data-ttu-id="02207-135">Bu örneği tooinstall Node.js için Azure Batch SDK.</span><span class="sxs-lookup"><span data-stu-id="02207-135">In this case tooinstall Azure Batch SDK for Node.js.</span></span>
>
>

### <a name="step-2-create-an-azure-batch-account"></a><span data-ttu-id="02207-136">2. Adım: Azure Batch hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="02207-136">Step 2: Create an Azure Batch account</span></span>

<span data-ttu-id="02207-137">Hello oluşturma [Azure portal](batch-account-create-portal.md) veya komut satırından ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure CLI](https://docs.microsoft.com/cli/azure/overview)).</span><span class="sxs-lookup"><span data-stu-id="02207-137">You can create it from hello [Azure portal](batch-account-create-portal.md) or from command line ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).</span></span>

<span data-ttu-id="02207-138">Merhaba komutları toocreate bir Azure CLI aracılığıyla aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="02207-138">Following are hello commands toocreate one through Azure CLI.</span></span>

<span data-ttu-id="02207-139">Bir kaynak grubu oluşturmak, bir toplu işlem hesabı toocreate hello istediğiniz zaten varsa bu adımı atlayın:</span><span class="sxs-lookup"><span data-stu-id="02207-139">Create a Resource Group, skip this step if you already have one where you want toocreate hello Batch Account:</span></span>

`az group create -n "<resource-group-name>" -l "<location>"`

<span data-ttu-id="02207-140">Ardından bir Azure Batch hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="02207-140">Next, create an Azure Batch account.</span></span>

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="02207-141">Her Batch hesabının ilgili erişim anahtarları vardır.</span><span class="sxs-lookup"><span data-stu-id="02207-141">Each Batch account has its corresponding access keys.</span></span> <span data-ttu-id="02207-142">Bu anahtarları gerekli toocreate başka Azure batch hesabında kaynaklardır.</span><span class="sxs-lookup"><span data-stu-id="02207-142">These keys are needed toocreate further resources in Azure batch account.</span></span> <span data-ttu-id="02207-143">Üretim ortamı için iyi bir uygulama bu anahtarları toouse Azure anahtar kasası toostore değil.</span><span class="sxs-lookup"><span data-stu-id="02207-143">A good practice for production environment is toouse Azure Key Vault toostore these keys.</span></span> <span data-ttu-id="02207-144">Bir hizmet asıl hello uygulama için daha sonra oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02207-144">You can then create a Service principal for hello application.</span></span> <span data-ttu-id="02207-145">Bu hizmet asıl hello uygulamasını kullanarak bir OAuth belirteç tooaccess anahtarları hello anahtar Kasası'nı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02207-145">Using this service principal hello application can create an OAuth token tooaccess keys from hello key vault.</span></span>

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="02207-146">Kopyalayın ve hello anahtar toobe hello sonraki adımlarda kullanılan saklayın.</span><span class="sxs-lookup"><span data-stu-id="02207-146">Copy and store hello key toobe used in hello subsequent steps.</span></span>

### <a name="step-3-create-an-azure-batch-service-client"></a><span data-ttu-id="02207-147">3. Adım: Azure Batch hizmet istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="02207-147">Step 3: Create an Azure Batch service client</span></span>
<span data-ttu-id="02207-148">Aşağıdaki kod parçacığını ilk hello azure-batch Node.js modülü içe aktarır ve ardından bir Batch hizmeti istemci oluşturur.</span><span class="sxs-lookup"><span data-stu-id="02207-148">Following code snippet first imports hello azure-batch Node.js module and then creates a Batch Service client.</span></span> <span data-ttu-id="02207-149">Toofirst ihtiyacınız hello önceki adımda kopyaladığınız hello Batch hesabınızın anahtarıyla SharedKeyCredentials nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="02207-149">You need toofirst create a SharedKeyCredentials object with hello Batch account key copied from hello previous step.</span></span>

```nodejs
// Initializing Azure Batch variables

var batch = require('azure-batch');

var accountName = '<azure-batch-account-name>';

var accountKey = '<account-key-downloaded>';

var accountUrl = '<account-url>'

// Create Batch credentials object using account name and account key

var credentials = new batch.SharedKeyCredentials(accountName,accountKey);

// Create Batch service client

var batch_client = new batch.ServiceClient(credentials,accountUrl);

```

<span data-ttu-id="02207-150">Hello Azure Batch URI'hello Azure portal hello genel bakış sekmesinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="02207-150">hello Azure Batch URI can be found in hello Overview tab of hello Azure portal.</span></span> <span data-ttu-id="02207-151">Merhaba biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="02207-151">It is of hello format:</span></span>

`https://accountname.location.batch.azure.com`

<span data-ttu-id="02207-152">Toohello ekran bakın:</span><span class="sxs-lookup"><span data-stu-id="02207-152">Refer toohello screenshot:</span></span>

![Azure batch uri](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a><span data-ttu-id="02207-154">4. Adım: Azure Batch havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="02207-154">Step 4: Create an Azure Batch pool</span></span>
<span data-ttu-id="02207-155">Bir Azure Batch havuzu birden çok VM’den (Batch Düğümleri olarak da bilinir) oluşur.</span><span class="sxs-lookup"><span data-stu-id="02207-155">An Azure Batch pool consists of multiple VMs (also known as Batch Nodes).</span></span> <span data-ttu-id="02207-156">Azure Batch hizmeti hello görevler bu düğümler üzerinde dağıtır ve bunları yönetir.</span><span class="sxs-lookup"><span data-stu-id="02207-156">Azure Batch service deploys hello tasks on these nodes and manages them.</span></span> <span data-ttu-id="02207-157">Havuzunuz için yapılandırma parametreleri aşağıdaki hello tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02207-157">You can define hello following configuration parameters for your pool.</span></span>

* <span data-ttu-id="02207-158">Sanal Makine Türü görüntüsü</span><span class="sxs-lookup"><span data-stu-id="02207-158">Type of Virtual Machine image</span></span>
* <span data-ttu-id="02207-159">Sanal Makine düğümlerinin boyutu</span><span class="sxs-lookup"><span data-stu-id="02207-159">Size of Virtual Machine nodes</span></span>
* <span data-ttu-id="02207-160">Sanal Makine düğümlerinin sayısı</span><span class="sxs-lookup"><span data-stu-id="02207-160">Number of Virtual Machine nodes</span></span>

> [!Tip]
> <span data-ttu-id="02207-161">Merhaba boyutu ve sanal makine düğüm sayısını büyük ölçüde toorun içinde paralel ve ayrıca hello görev kendisini istediğiniz görevlerin hello sayısına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="02207-161">hello size and number of Virtual Machine nodes largely depend on hello number of tasks you want toorun in parallel and also hello task itself.</span></span> <span data-ttu-id="02207-162">Toodetermine hello ideal sayısını ve boyutunu sınama öneririz.</span><span class="sxs-lookup"><span data-stu-id="02207-162">We recommend testing toodetermine hello ideal number and size.</span></span>
>
>

<span data-ttu-id="02207-163">Merhaba aşağıdaki kod parçacığını hello yapılandırma parametresi nesneleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="02207-163">hello following code snippet creates hello configuration parameter objects.</span></span>

```nodejs
// Creating Image reference configuration for Ubuntu Linux VM
var imgRef = {publisher:"Canonical",offer:"UbuntuServer",sku:"14.04.2-LTS",version:"latest"}

// Creating hello VM configuration object with hello SKUID
var vmconfig = {imageReference:imgRef,nodeAgentSKUId:"batch.node.ubuntu 14.04"}

// Setting hello VM size tooStandard F4
var vmSize = "STANDARD_F4"

//Setting number of VMs in hello pool too4
var numVMs = 4
```

> [!Tip]
> <span data-ttu-id="02207-164">Linux VM görüntüleri Azure Batch ve SKU kimlikleri için kullanılabilir Hello listesi için bkz [sanal makine görüntülerini listesi](batch-linux-nodes.md#list-of-virtual-machine-images).</span><span class="sxs-lookup"><span data-stu-id="02207-164">For hello list of Linux VM images available for Azure Batch and their SKU IDs, see [List of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images).</span></span>
>
>

<span data-ttu-id="02207-165">Merhaba havuzu yapılandırması tanımlandığında hello Azure Batch havuzu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02207-165">Once hello pool configuration is defined, you can create hello Azure Batch pool.</span></span> <span data-ttu-id="02207-166">Merhaba Batch havuzu komutu Azure sanal makine düğümleri oluşturur ve toobe hazır tooreceive görevleri tooexecute hazırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02207-166">hello Batch pool command creates Azure Virtual Machine nodes and prepares them toobe ready tooreceive tasks tooexecute.</span></span> <span data-ttu-id="02207-167">Her havuz, sonraki adımlarda başvuru için benzersiz bir kimliğe sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="02207-167">Each pool should have a unique ID for reference in subsequent steps.</span></span>

<span data-ttu-id="02207-168">Aşağıdaki kod parçacığını hello bir Azure Batch havuzu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="02207-168">hello following code snippet creates an Azure Batch pool.</span></span>

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating hello Pool for hello specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

<span data-ttu-id="02207-169">Oluşturulan hello havuzu hello durumunu denetleyin ve bir iş toothat havuzu teslimini ile devam geçmeden önce hello durumu "etkin" olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="02207-169">You can check hello status of hello pool created and ensure that hello state is in "active" before going ahead with submission of a Job toothat pool.</span></span>

```nodejs
var cloudPool = batch_client.pool.get(poolid,function(error,result,request,response){
        if(error == null)
        {

            if(result.state == "active")
            {
                console.log("Pool is active");
            }
        }
        else
        {
            if(error.statusCode==404)
            {
                console.log("Pool not found yet returned 404...");    

            }
            else
            {
                console.log("Error occurred while retrieving pool data");
            }
        }
        });
```

<span data-ttu-id="02207-170">Merhaba pool.get işlevi tarafından döndürülen örnek bir sonuç nesnesi aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="02207-170">Following is a sample result object returned by hello pool.get function.</span></span>

```
{ id: 'processcsv_201721152',
  displayName: 'processcsv_201721152',
  url: 'https://<batch-account-name>.centralus.batch.azure.com/pools/processcsv_201721152',
  eTag: '<eTag>',
  lastModified: 2017-03-27T10:28:02.398Z,
  creationTime: 2017-03-27T10:28:02.398Z,
  state: 'active',
  stateTransitionTime: 2017-03-27T10:28:02.398Z,
  allocationState: 'resizing',
  allocationStateTransitionTime: 2017-03-27T10:28:02.398Z,
  vmSize: 'standard_a1',
  virtualMachineConfiguration:
   { imageReference:
      { publisher: 'Canonical',
        offer: 'UbuntuServer',
        sku: '14.04.2-LTS',
        version: 'latest' },
     nodeAgentSKUId: 'batch.node.ubuntu 14.04' },
  resizeTimeout:
   { [Number: 900000]
     _milliseconds: 900000,
     _days: 0,
     _months: 0,
     _data:
      { milliseconds: 0,
        seconds: 0,
        minutes: 15,
        hours: 0,
        days: 0,
        months: 0,
        years: 0 },
     _locale:
      Locale {
        _calendar: [Object],
        _longDateFormat: [Object],
        _invalidDate: 'Invalid date',
        ordinal: [Function: ordinal],
        _ordinalParse: /\d{1,2}(th|st|nd|rd)/,
        _relativeTime: [Object],
        _months: [Object],
        _monthsShort: [Object],
        _week: [Object],
        _weekdays: [Object],
        _weekdaysMin: [Object],
        _weekdaysShort: [Object],
        _meridiemParse: /[ap]\.?m?\.?/i,
        _abbr: 'en',
        _config: [Object],
        _ordinalParseLenient: /\d{1,2}(th|st|nd|rd)|\d{1,2}/ } },
  currentDedicated: 0,
  targetDedicated: 4,
  enableAutoScale: false,
  enableInterNodeCommunication: false,
  maxTasksPerNode: 1,
  taskSchedulingPolicy: { nodeFillType: 'Spread' } }
```


### <a name="step-4-submit-an-azure-batch-job"></a><span data-ttu-id="02207-171">4. Adım: Azure Batch işi gönderme</span><span class="sxs-lookup"><span data-stu-id="02207-171">Step 4: Submit an Azure Batch job</span></span>
<span data-ttu-id="02207-172">Azure Batch işi, benzer görevlerden oluşan bir mantıksal gruptur.</span><span class="sxs-lookup"><span data-stu-id="02207-172">An Azure Batch job is a logical group of similar tasks.</span></span> <span data-ttu-id="02207-173">Senaryomuzda olmasından "İşlem csv tooJSON."</span><span class="sxs-lookup"><span data-stu-id="02207-173">In our scenario, it is "Process csv tooJSON."</span></span> <span data-ttu-id="02207-174">Burada her görev her Azure Depolama kapsayıcısında bulunan csv dosyalarını işliyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="02207-174">Each task here could be processing csv files present in each Azure Storage container.</span></span>

<span data-ttu-id="02207-175">Bu görevleri paralel olarak çalışır ve hello Azure Batch hizmeti tarafından düzenlenmiş birden çok düğüm arasında dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="02207-175">These tasks would run in parallel and deployed across multiple nodes, orchestrated by hello Azure Batch service.</span></span>

> [!Tip]
> <span data-ttu-id="02207-176">Merhaba kullanabilirsiniz [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) özelliği toospecify en fazla sayıda eşzamanlı olarak tek bir düğümde çalışan görev.</span><span class="sxs-lookup"><span data-stu-id="02207-176">You can use hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property toospecify maximum number of tasks that can run concurrently on a single node.</span></span>
>
>

#### <a name="preparation-task"></a><span data-ttu-id="02207-177">Hazırlık görevi</span><span class="sxs-lookup"><span data-stu-id="02207-177">Preparation task</span></span>

<span data-ttu-id="02207-178">oluşturulan hello VM düğümleri boş Ubuntu düğümler var.</span><span class="sxs-lookup"><span data-stu-id="02207-178">hello VM nodes created are blank Ubuntu nodes.</span></span> <span data-ttu-id="02207-179">Genellikle, önkoşul olarak tooinstall programlar kümesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="02207-179">Often, you need tooinstall a set of programs as prerequisites.</span></span>
<span data-ttu-id="02207-180">Genellikle, Linux düğümleri için çalışan hello gerçek görevler önce hello Önkoşullar yükleyen bir kabuk betiği olabilir.</span><span class="sxs-lookup"><span data-stu-id="02207-180">Typically, for Linux nodes you can have a shell script that installs hello prerequisites before hello actual tasks run.</span></span> <span data-ttu-id="02207-181">Ancak bu, programlanabilir herhangi bir yürütülebilir dosya da olabilir.</span><span class="sxs-lookup"><span data-stu-id="02207-181">However it could be any programmable executable.</span></span>
<span data-ttu-id="02207-182">Merhaba [Kabuk komut dosyası](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) Bu örnekte, Python için Python PIP ve hello Azure depolama SDK'sını yükler.</span><span class="sxs-lookup"><span data-stu-id="02207-182">hello [shell script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) in this example installs Python-pip and hello Azure Storage SDK for Python.</span></span>

<span data-ttu-id="02207-183">Azure Storage hesabını hello komut dosyasını karşıya yükleyin ve bir SAS URI'sini tooaccess hello komut dosyası oluştur.</span><span class="sxs-lookup"><span data-stu-id="02207-183">You can upload hello script on an Azure Storage Account and generate a SAS URI tooaccess hello script.</span></span> <span data-ttu-id="02207-184">Bu işlem ayrıca hello Azure depolama Node.js SDK'sını kullanarak otomatik olarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="02207-184">This process can also be automated using hello Azure Storage Node.js SDK.</span></span>

> [!Tip]
> <span data-ttu-id="02207-185">Bir iş hazırlama görevi burada hello belirli görev toorun gereken yalnızca hello VM düğümler üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="02207-185">A preparation task for a job runs only on hello VM nodes where hello specific task needs toorun.</span></span> <span data-ttu-id="02207-186">Üzerinde çalışan hello görevler bağımsız olarak tüm düğümlerde yüklü Önkoşullar toobe istiyorsanız hello kullanabilirsiniz [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) sırasında bir havuzu ekleme özelliği.</span><span class="sxs-lookup"><span data-stu-id="02207-186">If you want prerequisites toobe installed on all nodes irrespective of hello tasks that run on it, you can use hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property while adding a pool.</span></span> <span data-ttu-id="02207-187">Başvuru için hazırlık görevi tanımı aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02207-187">You can use hello following preparation task definition for reference.</span></span>
>
>

<span data-ttu-id="02207-188">Hazırlık görevi Azure toplu işlem hello gönderme sırasında belirtilir.</span><span class="sxs-lookup"><span data-stu-id="02207-188">A preparation task is specified during hello submission of Azure Batch job.</span></span> <span data-ttu-id="02207-189">Aşağıdaki hazırlık görevi yapılandırma parametreleri hello:</span><span class="sxs-lookup"><span data-stu-id="02207-189">Following are hello preparation task configuration parameters:</span></span>

* <span data-ttu-id="02207-190">**Kimliği**: hello hazırlık görev için benzersiz bir tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="02207-190">**ID**: A unique identifier for hello preparation task</span></span>
* <span data-ttu-id="02207-191">**komut satırı**: komut satırı tooexecute hello görev çalıştırılabilir</span><span class="sxs-lookup"><span data-stu-id="02207-191">**commandLine**: Command line tooexecute hello task executable</span></span>
* <span data-ttu-id="02207-192">**resourceFiles**: dosyaları ayrıntılarını sağlayın nesneler dizisi gerektiği için bu görev toorun indirilen toobe.</span><span class="sxs-lookup"><span data-stu-id="02207-192">**resourceFiles**: Array of objects that provide details of files needed toobe downloaded for this task toorun.</span></span>  <span data-ttu-id="02207-193">Seçenekleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="02207-193">Following are its options</span></span>
    - <span data-ttu-id="02207-194">blobSource: hello dosya SAS URI'sini hello</span><span class="sxs-lookup"><span data-stu-id="02207-194">blobSource: hello SAS URI of hello file</span></span>
    - <span data-ttu-id="02207-195">filePath: yerel yol toodownload ve hello dosyasını kaydedin</span><span class="sxs-lookup"><span data-stu-id="02207-195">filePath: Local path toodownload and save hello file</span></span>
    - <span data-ttu-id="02207-196">fileMode: Yalnızca Linux düğümlerinde kullanılan fileMode, sekizli biçimdedir ve varsayılan değeri 0770’tir.</span><span class="sxs-lookup"><span data-stu-id="02207-196">fileMode: Only applicable for Linux nodes, fileMode is in octal format with a default value of 0770</span></span>
* <span data-ttu-id="02207-197">**waitForSuccess**: kümesi tootrue, hello görev hazırlık görevi hatalarında çalışmazsa</span><span class="sxs-lookup"><span data-stu-id="02207-197">**waitForSuccess**: If set tootrue, hello task does not run on preparation task failures</span></span>
* <span data-ttu-id="02207-198">**runElevated**: yükseltilmiş ayrıcalıklar gerekli toorun hello görev varsa tootrue ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="02207-198">**runElevated**: Set it tootrue if elevated privileges are needed toorun hello task.</span></span>

<span data-ttu-id="02207-199">Aşağıdaki kod parçacığını hello hazırlık görev komut dosyası yapılandırma örneği gösterilir:</span><span class="sxs-lookup"><span data-stu-id="02207-199">Following code snippet shows hello preparation task script configuration sample:</span></span>

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

<span data-ttu-id="02207-200">Varsa, görevleri toorun için yüklü hiçbir Önkoşullar toobe hello hazırlama görevleri atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02207-200">If there are no prerequisites toobe installed for your tasks toorun, you can skip hello preparation tasks.</span></span> <span data-ttu-id="02207-201">Aşağıdaki kod görünen adı "process csv files" olan bir iş oluşturur.</span><span class="sxs-lookup"><span data-stu-id="02207-201">Following code creates a job with display name "process csv files."</span></span>

 ```nodejs
 // Setting up Batch pool configuration
 var pool_config = {poolId:poolid}
 // Setting up Job configuration along with preparation task
 var jobId = "processcsvjob"
 var job_config = {id:jobId,displayName:"process csv files",jobPreparationTask:job_prep_task_config,poolInfo:pool_config}
 // Adding Azure batch job toohello pool
 var job = batch_client.job.add(job_config,function(error,result){
     if(error != null)
     {
         console.log("Error submitting job : " + error.response);
     }});
```


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a><span data-ttu-id="02207-202">5. Adım: Bir iş için Azure Batch görevlerini gönderme</span><span class="sxs-lookup"><span data-stu-id="02207-202">Step 5: Submit Azure Batch tasks for a job</span></span>

<span data-ttu-id="02207-203">İşlem csv işimiz oluşturulduğuna göre bu iş için görevleri oluşturabiliriz.</span><span class="sxs-lookup"><span data-stu-id="02207-203">Now that our process csv job is created, let us create tasks for that job.</span></span> <span data-ttu-id="02207-204">Dört kapsayıcıları sahibiz varsayıldığında, biz toocreate dört görevleri, her kapsayıcı için bir tane vardır.</span><span class="sxs-lookup"><span data-stu-id="02207-204">Assuming we have four containers, we have toocreate four tasks, one for each container.</span></span>

<span data-ttu-id="02207-205">Şu hello bakarsanız [Python betiği](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), iki parametre kabul eder:</span><span class="sxs-lookup"><span data-stu-id="02207-205">If we look at hello [Python script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), it accepts two parameters:</span></span>

* <span data-ttu-id="02207-206">kapsayıcı adı: depolama kapsayıcısı toodownload dosyalarından hello</span><span class="sxs-lookup"><span data-stu-id="02207-206">container name: hello Storage container toodownload files from</span></span>
* <span data-ttu-id="02207-207">desen: Dosya adı için isteğe bağlı bir desen parametresi</span><span class="sxs-lookup"><span data-stu-id="02207-207">pattern: An optional parameter of file name pattern</span></span>

<span data-ttu-id="02207-208">Biz dört kapsayıcıları "con1", "con2", "con3" varsayarak, "con4" aşağıdaki "daha önce oluşturduğumuz görevleri toohello Azure toplu iş işlem için csv" gönderme gösterir kod.</span><span class="sxs-lookup"><span data-stu-id="02207-208">Assuming we have four containers "con1", "con2", "con3","con4" following code shows submitting for tasks toohello Azure batch job "process csv" we created earlier.</span></span>

```nodejs
// storing container names in an array
var container_list = ["con1","con2","con3","con4"]
    container_list.forEach(function(val,index){           

           var container_name = val;
           var taskID = container_name + "_process";
           var task_config = {id:taskID,displayName:'process csv in ' + container_name,commandLine:'python processcsv.py --container ' + container_name,resourceFiles:[{'blobSource':'<blob SAS URI>','filePath':'processcsv.py'}]}
           var task = batch_client.task.add(poolid,task_config,function(error,result){
                if(error != null)
                {
                    console.log(error.response);     
                }
                else
                {
                    console.log("Task for container : " + container_name + "submitted successfully");
                }



           });

    });
```

<span data-ttu-id="02207-209">Merhaba kod birden çok görevleri toohello havuzu ekler.</span><span class="sxs-lookup"><span data-stu-id="02207-209">hello code adds multiple tasks toohello pool.</span></span> <span data-ttu-id="02207-210">Ve her bir hello görev oluşturulan VM'ler hello havuzu düğümünde çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="02207-210">And each of hello tasks is executed on a node in hello pool of VMs created.</span></span> <span data-ttu-id="02207-211">Hello sayıda görev havuzu veya hello maxTasksPerNode özelliğinde hello VM'lerin sayısını aşarsa, bir düğüm kullanılabilir duruma getirilene kadar hello görevleri bekleyin.</span><span class="sxs-lookup"><span data-stu-id="02207-211">If hello number of tasks exceeds hello number of VMs in a pool or hello maxTasksPerNode property, hello tasks wait until a node is made available.</span></span> <span data-ttu-id="02207-212">Bu düzenleme Azure Batch tarafından otomatik olarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="02207-212">This orchestration is handled by Azure Batch automatically.</span></span>

<span data-ttu-id="02207-213">Merhaba portal hello görevleri ve iş durumlar görünümleri açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="02207-213">hello portal has detailed views on hello tasks and job statuses.</span></span> <span data-ttu-id="02207-214">Merhaba listesini kullanın ve işlevleri hello Azure düğümü SDK'sını alın.</span><span class="sxs-lookup"><span data-stu-id="02207-214">You can also use hello list and get functions in hello Azure Node SDK.</span></span> <span data-ttu-id="02207-215">Ayrıntılar hello belgelerde sağlanan [bağlantı](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span><span class="sxs-lookup"><span data-stu-id="02207-215">Details are provided in hello documentation [link](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="02207-216">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="02207-216">Next steps</span></span>

- <span data-ttu-id="02207-217">Gözden geçirme hello [genel bakış Azure Batch özelliklerine](batch-api-basics.md) yeni toohello hizmeti olup olmadığınızı öneririz makalesi.</span><span class="sxs-lookup"><span data-stu-id="02207-217">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
- <span data-ttu-id="02207-218">Merhaba bkz [toplu Node.js başvuru](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore hello toplu API.</span><span class="sxs-lookup"><span data-stu-id="02207-218">See hello [Batch Node.js reference](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore hello Batch API.</span></span>

