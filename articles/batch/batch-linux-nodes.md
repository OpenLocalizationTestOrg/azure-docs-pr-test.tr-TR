---
title: "Sanal makinedeki aaaRun Linux işlem düğümlerini - Azure Batch | Microsoft Docs"
description: "Nasıl tooprocess, paralel işlem iş yükleri hakkında bilgi edinin Linux sanal makinelerin Azure Batch havuzları."
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3daabd5c577baaafd0544f9f7913cb7b116d74d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-linux-compute-nodes-in-batch-pools"></a><span data-ttu-id="8891f-103">Batch havuzlarında Linux işlem düğümlerini sağlama</span><span class="sxs-lookup"><span data-stu-id="8891f-103">Provision Linux compute nodes in Batch pools</span></span>

<span data-ttu-id="8891f-104">Azure Batch toorun paralel işlem iş yükleri hem Linux hem de Windows sanal makinelerde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8891f-104">You can use Azure Batch toorun parallel compute workloads on both Linux and Windows virtual machines.</span></span> <span data-ttu-id="8891f-105">Bu makalede nasıl toocreate havuzları Linux hello Batch hizmetindeki her iki hello kullanarak işlem düğümleri ayrıntıları [Batch Python] [ py_batch_package] ve [Batch .NET] [ api_net] istemci kitaplıkları.</span><span class="sxs-lookup"><span data-stu-id="8891f-105">This article details how toocreate pools of Linux compute nodes in hello Batch service by using both hello [Batch Python][py_batch_package] and [Batch .NET][api_net] client libraries.</span></span>

> [!NOTE]
> <span data-ttu-id="8891f-106">Uygulama paketleri 5 Temmuz 2017’den sonra oluşturulmuş tüm Batch havuzlarında desteklenir.</span><span class="sxs-lookup"><span data-stu-id="8891f-106">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="8891f-107">Bunlar yalnızca hello havuzu, bir bulut Hizmeti Yapılandırması kullanılarak oluşturulduysa 10 Mart 2016 ve 5 Temmuz 2017 arasında oluşturulan Batch havuzu üzerinde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="8891f-107">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="8891f-108">Önceki too10 Mart 2016 oluşturulan batch havuzları, uygulama paketleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="8891f-108">Batch pools created prior too10 March 2016 do not support application packages.</span></span> <span data-ttu-id="8891f-109">Uygulama hakkında daha fazla bilgi toodeploy uygulamaları tooyour toplu düğümleriniz paketleri için bkz: [Batch uygulama paketleriyle uygulama toocompute düğümlerini dağıtmak](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="8891f-109">For more information about using application packages toodeploy your applications tooyour Batch nodes, see [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>
>
>

## <a name="virtual-machine-configuration"></a><span data-ttu-id="8891f-110">Sanal Makine Yapılandırması</span><span class="sxs-lookup"><span data-stu-id="8891f-110">Virtual machine configuration</span></span>
<span data-ttu-id="8891f-111">Toplu işlem düğümleri havuzu oluşturduğunuzda, hangi tooselect hello düğüm boyutu ve işletim sistemi iki seçeneğiniz vardır: Bulut Hizmetleri Yapılandırması ve sanal makine yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="8891f-111">When you create a pool of compute nodes in Batch, you have two options from which tooselect hello node size and operating system: Cloud Services Configuration and Virtual Machine Configuration.</span></span>

<span data-ttu-id="8891f-112">**Cloud Services Yapılandırması** *yalnızca* Windows işlem düğümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="8891f-112">**Cloud Services Configuration** provides Windows compute nodes *only*.</span></span> <span data-ttu-id="8891f-113">Kullanılabilir işlem düğümü boyutları içinde listelenen [Cloud Services boyutları](../cloud-services/cloud-services-sizes-specs.md), ve kullanılabilir işletim sistemlerine hello listelenen [Azure konuk işletim sistemi sürümleri ve SDK uyumluluk matrisi](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="8891f-113">Available compute node sizes are listed in [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md), and available operating systems are listed in hello [Azure Guest OS releases and SDK compatibility matrix](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> <span data-ttu-id="8891f-114">Azure Cloud Services düğümleri içeren bir havuz oluşturduğunuzda, hello düğüm boyutu belirtin ve hello hello açıklanan işletim sistemi ailesi önceden makaleleri belirtiliyor.</span><span class="sxs-lookup"><span data-stu-id="8891f-114">When you create a pool that contains Azure Cloud Services nodes, you specify hello node size and hello OS family, which are described in hello previously mentioned articles.</span></span> <span data-ttu-id="8891f-115">Bulut Hizmetleri, Windows havuzları işlem düğümleri için en yaygın olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8891f-115">For pools of Windows compute nodes, Cloud Services is most commonly used.</span></span>

<span data-ttu-id="8891f-116">**Sanal Makine Yapılandırması** işlem düğümleri için hem Linux hem de Windows görüntüleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="8891f-116">**Virtual Machine Configuration** provides both Linux and Windows images for compute nodes.</span></span> <span data-ttu-id="8891f-117">Kullanılabilir işlem düğümü boyutları içinde listelenen [azure'da sanal makineler için Boyutlar](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) ve [azure'da sanal makineler için Boyutlar](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span><span class="sxs-lookup"><span data-stu-id="8891f-117">Available compute node sizes are listed in [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) and [Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span></span> <span data-ttu-id="8891f-118">Sanal Makine Yapılandırması düğümleri içeren bir havuz oluşturduğunuzda hello düğümleri, hello sanal makine görüntü başvurusunu ve hello toplu işlem düğüm Aracısı SKU toobe hello düğümlerinde yüklü hello boyutunu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8891f-118">When you create a pool that contains Virtual Machine Configuration nodes, you must specify hello size of hello nodes, hello virtual machine image reference, and hello Batch node agent SKU toobe installed on hello nodes.</span></span>

### <a name="virtual-machine-image-reference"></a><span data-ttu-id="8891f-119">Sanal makine görüntü başvurusunu</span><span class="sxs-lookup"><span data-stu-id="8891f-119">Virtual machine image reference</span></span>
<span data-ttu-id="8891f-120">Batch hizmetini kullanan hello [sanal makine ölçek kümeleri](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux işlem düğümlerini.</span><span class="sxs-lookup"><span data-stu-id="8891f-120">hello Batch service uses [virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux compute nodes.</span></span> <span data-ttu-id="8891f-121">Merhaba görüntüden belirtebilirsiniz [Azure Marketi][vm_marketplace], veya hazırladığınız özel bir görüntü sağlayın.</span><span class="sxs-lookup"><span data-stu-id="8891f-121">You can specify an image from hello [Azure Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span> <span data-ttu-id="8891f-122">Özel görüntüler hakkında daha fazla ayrıntı için bkz. [Batch ile büyük ölçekli paralel işlem çözümleri geliştirme](batch-api-basics.md#pool).</span><span class="sxs-lookup"><span data-stu-id="8891f-122">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

<span data-ttu-id="8891f-123">Bir sanal makine görüntü başvurusunu yapılandırdığınızda hello sanal makine görüntüsünün hello özelliklerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="8891f-123">When you configure a virtual machine image reference, you specify hello properties of hello virtual machine image.</span></span> <span data-ttu-id="8891f-124">bir sanal makine görüntü başvurusunu oluşturduğunuzda, aşağıdaki özelliklere hello gereklidir:</span><span class="sxs-lookup"><span data-stu-id="8891f-124">hello following properties are required when you create a virtual machine image reference:</span></span>

| <span data-ttu-id="8891f-125">**Resim başvurusu özellikleri**</span><span class="sxs-lookup"><span data-stu-id="8891f-125">**Image reference properties**</span></span> | <span data-ttu-id="8891f-126">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="8891f-126">**Example**</span></span> |
| --- | --- |
| <span data-ttu-id="8891f-127">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="8891f-127">Publisher</span></span> |<span data-ttu-id="8891f-128">Canonical</span><span class="sxs-lookup"><span data-stu-id="8891f-128">Canonical</span></span> |
| <span data-ttu-id="8891f-129">Sunduğu</span><span class="sxs-lookup"><span data-stu-id="8891f-129">Offer</span></span> |<span data-ttu-id="8891f-130">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="8891f-130">UbuntuServer</span></span> |
| <span data-ttu-id="8891f-131">SKU</span><span class="sxs-lookup"><span data-stu-id="8891f-131">SKU</span></span> |<span data-ttu-id="8891f-132">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="8891f-132">14.04.4-LTS</span></span> |
| <span data-ttu-id="8891f-133">Sürüm</span><span class="sxs-lookup"><span data-stu-id="8891f-133">Version</span></span> |<span data-ttu-id="8891f-134">en son</span><span class="sxs-lookup"><span data-stu-id="8891f-134">latest</span></span> |

> [!TIP]
> <span data-ttu-id="8891f-135">Bu özellikler ve nasıl içinde toolist Market görüntüleri hakkında daha fazla bilgiyi [gidin ve Azure CLI veya PowerShell ile select Linux sanal makine görüntüleri](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8891f-135">You can learn more about these properties and how toolist Marketplace images in [Navigate and select Linux virtual machine images in Azure with CLI or PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="8891f-136">Tüm Market görüntülerini Batch ile şu anda uyumlu olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8891f-136">Note that not all Marketplace images are currently compatible with Batch.</span></span> <span data-ttu-id="8891f-137">Daha fazla bilgi için bkz: [düğümü aracı SKU'sunu](#node-agent-sku).</span><span class="sxs-lookup"><span data-stu-id="8891f-137">For more information, see [Node agent SKU](#node-agent-sku).</span></span>
>
>

### <a name="node-agent-sku"></a><span data-ttu-id="8891f-138">Düğüm Aracısı SKU</span><span class="sxs-lookup"><span data-stu-id="8891f-138">Node agent SKU</span></span>
<span data-ttu-id="8891f-139">Merhaba toplu işlem düğüm Aracısı hello havuzdaki her düğüme çalışır ve hello düğümü hello Batch hizmeti arasında hello komut ve denetim arabirimi sağlayan bir programdır.</span><span class="sxs-lookup"><span data-stu-id="8891f-139">hello Batch node agent is a program that runs on each node in hello pool and provides hello command-and-control interface between hello node and hello Batch service.</span></span> <span data-ttu-id="8891f-140">Farklı işletim sistemleri için SKU'ları bilinen hello düğüm Aracısı'nın farklı uygulamaları vardır.</span><span class="sxs-lookup"><span data-stu-id="8891f-140">There are different implementations of hello node agent, known as SKUs, for different operating systems.</span></span> <span data-ttu-id="8891f-141">Esas olarak, bir sanal makine yapılandırması oluşturduğunuzda, ilk hello sanal makine görüntü başvurusunu belirtin ve ardından hello görüntüde hello düğüm Aracısı tooinstall belirtin.</span><span class="sxs-lookup"><span data-stu-id="8891f-141">Essentially, when you create a Virtual Machine Configuration, you first specify hello virtual machine image reference, and then you specify hello node agent tooinstall on hello image.</span></span> <span data-ttu-id="8891f-142">Genellikle, her düğüm Aracısı SKU birden çok sanal makine görüntüsü ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="8891f-142">Typically, each node agent SKU is compatible with multiple virtual machine images.</span></span> <span data-ttu-id="8891f-143">Düğüm Aracısı SKU'ları bazı örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8891f-143">Here are a few examples of node agent SKUs:</span></span>

* <span data-ttu-id="8891f-144">Batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="8891f-144">batch.node.ubuntu 14.04</span></span>
* <span data-ttu-id="8891f-145">Batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="8891f-145">batch.node.centos 7</span></span>
* <span data-ttu-id="8891f-146">Batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="8891f-146">batch.node.windows amd64</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8891f-147">Merhaba Market kullanılabilir tüm sanal makine görüntülerini hello şu anda kullanılabilir toplu düğümü aracıları ile uyumlu değildir.</span><span class="sxs-lookup"><span data-stu-id="8891f-147">Not all virtual machine images that are available in hello Marketplace are compatible with hello currently available Batch node agents.</span></span> <span data-ttu-id="8891f-148">Sanal makine görüntülerini uyumlu oldukları hello ve Hello Batch SDK'ları toolist hello kullanılabilir düğüm Aracısı SKU'ları kullanın.</span><span class="sxs-lookup"><span data-stu-id="8891f-148">Use hello Batch SDKs toolist hello available node agent SKUs and hello virtual machine images with which they are compatible.</span></span> <span data-ttu-id="8891f-149">Hello bkz [listesi, sanal makine görüntülerini](#list-of-virtual-machine-images) daha fazla bilgi ve örnekler için bu makalenin sonraki tooretrieve çalışma zamanında geçerli görüntüleri listesi.</span><span class="sxs-lookup"><span data-stu-id="8891f-149">See hello [List of Virtual Machine images](#list-of-virtual-machine-images) later in this article for more information and examples of how tooretrieve a list of valid images at runtime.</span></span>
>
>

## <a name="create-a-linux-pool-batch-python"></a><span data-ttu-id="8891f-150">Bir Linux havuzu oluşturun: Batch Python</span><span class="sxs-lookup"><span data-stu-id="8891f-150">Create a Linux pool: Batch Python</span></span>
<span data-ttu-id="8891f-151">Merhaba aşağıdaki kod parçacığını bir örnek nasıl gösterir toouse hello [Python için Microsoft Azure Batch istemci Kitaplığı] [ py_batch_package] toocreate Ubuntu Server havuzu işlem düğümlerini.</span><span class="sxs-lookup"><span data-stu-id="8891f-151">hello following code snippet shows an example of how toouse hello [Microsoft Azure Batch Client Library for Python][py_batch_package] toocreate a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="8891f-152">Başvuru belgelerini Batch Python modülü bulunabilir hello için [azure.batch paket] [ py_batch_docs] okuma hello belgeleri üzerinde.</span><span class="sxs-lookup"><span data-stu-id="8891f-152">Reference documentation for hello Batch Python module can be found at [azure.batch package][py_batch_docs] on Read hello Docs.</span></span>

<span data-ttu-id="8891f-153">Bu kod parçacığında oluşturur bir [Imagereference] [ py_imagereference] açıkça ve her (yayımcı, teklif, SKU, sürüm) özelliklerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="8891f-153">This snippet creates an [ImageReference][py_imagereference] explicitly and specifies each of its properties (publisher, offer, SKU, version).</span></span> <span data-ttu-id="8891f-154">Üretim kodunda ancak hello kullanmanızı öneririz [list_node_agent_skus] [ py_list_skus] yöntemi toodetermine ve hello kullanılabilir görüntü ve düğüm Aracısı SKU birleşimlerini çalışma zamanında seçin.</span><span class="sxs-lookup"><span data-stu-id="8891f-154">In production code, however, we recommend that you use hello [list_node_agent_skus][py_list_skus] method toodetermine and select from hello available image and node agent SKU combinations at runtime.</span></span>

```python
# Import hello required modules from the
# Azure Batch Client Library for Python
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify Batch account credentials
account = "<batch-account-name>"
key = "<batch-account-key>"
batch_url = "<batch-account-url>"

# Pool settings
pool_id = "LinuxNodesSamplePoolPython"
vm_size = "STANDARD_A1"
node_count = 1

# Initialize hello Batch client
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create hello unbound pool
new_pool = batchmodels.PoolAddParameter(id = pool_id, vm_size = vm_size)
new_pool.target_dedicated = node_count

# Configure hello start task for hello pool
start_task = batchmodels.StartTask()
start_task.run_elevated = True
start_task.command_line = "printenv AZ_BATCH_NODE_STARTUP_DIR"
new_pool.start_task = start_task

# Create an ImageReference which specifies hello Marketplace
# virtual machine image tooinstall on hello nodes.
ir = batchmodels.ImageReference(
    publisher = "Canonical",
    offer = "UbuntuServer",
    sku = "14.04.2-LTS",
    version = "latest")

# Create hello VirtualMachineConfiguration, specifying
# hello VM image reference and hello Batch node agent to
# be installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign hello virtual machine configuration toohello pool
new_pool.virtual_machine_configuration = vmc

# Create pool in hello Batch service
client.pool.add(new_pool)
```

<span data-ttu-id="8891f-155">Daha önce belirtildiği gibi hello oluşturmak yerine öneririz [Imagereference] [ py_imagereference] hello açıkça kullandığınız [list_node_agent_skus] [ py_list_skus] hello yöntemi toodynamically seçin, düğüm Aracısı/Market görüntü birleşimleri şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="8891f-155">As mentioned previously, we recommend that instead of creating hello [ImageReference][py_imagereference] explicitly, you use hello [list_node_agent_skus][py_list_skus] method toodynamically select from hello currently supported node agent/Marketplace image combinations.</span></span> <span data-ttu-id="8891f-156">Python kod parçacığında gösterildiği nasıl aşağıdaki hello toouse bu yöntem.</span><span class="sxs-lookup"><span data-stu-id="8891f-156">hello following Python snippet shows how toouse this method.</span></span>

```python
# Get hello list of node agents from hello Batch service
nodeagents = client.account.list_node_agent_skus()

# Obtain hello desired node agent
ubuntu1404agent = next(agent for agent in nodeagents if "ubuntu 14.04" in agent.id)

# Pick hello first image reference from hello list of verified references
ir = ubuntu1404agent.verified_image_references[0]

# Create hello VirtualMachineConfiguration, specifying hello VM image
# reference and hello Batch node agent toobe installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = ubuntu1404agent.id)
```

## <a name="create-a-linux-pool-batch-net"></a><span data-ttu-id="8891f-157">Bir Linux havuzu oluşturun: Batch .NET</span><span class="sxs-lookup"><span data-stu-id="8891f-157">Create a Linux pool: Batch .NET</span></span>
<span data-ttu-id="8891f-158">Merhaba aşağıdaki kod parçacığını bir örnek nasıl gösterir toouse hello [Batch .NET] [ nuget_batch_net] istemci kitaplığı toocreate Ubuntu Server havuzu işlem düğümlerini.</span><span class="sxs-lookup"><span data-stu-id="8891f-158">hello following code snippet shows an example of how toouse hello [Batch .NET][nuget_batch_net] client library toocreate a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="8891f-159">Merhaba bulabilirsiniz [Batch .NET başvuru belgeleri] [ api_net] konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="8891f-159">You can find hello [Batch .NET reference documentation][api_net] on MSDN.</span></span>

<span data-ttu-id="8891f-160">Merhaba aşağıdaki kod parçacığını kullanan hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] şu anda desteklenen Market görüntü ve düğüm Aracısı SKU birleşimlerini hello listesinden yöntemi tooselect.</span><span class="sxs-lookup"><span data-stu-id="8891f-160">hello following code snippet uses hello [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method tooselect from hello list of currently supported Marketplace image and node agent SKU combinations.</span></span> <span data-ttu-id="8891f-161">Bu teknik arzu çünkü desteklenen birleşimlerin Hello listesi zaman tootime değişebilir.</span><span class="sxs-lookup"><span data-stu-id="8891f-161">This technique is desirable because hello list of supported combinations may change from time tootime.</span></span> <span data-ttu-id="8891f-162">En yaygın olarak desteklenen birleşimlerin eklenir.</span><span class="sxs-lookup"><span data-stu-id="8891f-162">Most commonly, supported combinations are added.</span></span>

```csharp
// Pool settings
const string poolId = "LinuxNodesSamplePoolDotNet";
const string vmSize = "STANDARD_A1";
const int nodeCount = 1;

// Obtain a collection of all available node agent SKUs.
// This allows us tooselect from a list of supported
// VM image/node agent combinations.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image
// that we wish toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. Note that there are one or more image
// references associated with this node agent SKU.
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello VirtualMachineConfiguration for use when actually
// creating hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

// Create hello unbound pool object using hello VirtualMachineConfiguration
// created above
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    virtualMachineSize: vmSize,
    virtualMachineConfiguration: virtualMachineConfiguration,
    targetDedicatedComputeNodes: nodeCount);

// Commit hello pool toohello Batch service
await pool.CommitAsync();
```

<span data-ttu-id="8891f-163">Merhaba önceki kod parçacığında hello kullansa [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] yöntemi toodynamically listesi ve arasından seçim desteklenmez (önerilen) görüntüsü ve düğüm Aracısı SKU birleşimleri, ayrıca yapılandırabilirsiniz bir [Imagereference] [ net_imagereference] açıkça:</span><span class="sxs-lookup"><span data-stu-id="8891f-163">Although hello previous snippet uses hello [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method toodynamically list and select from supported image and node agent SKU combinations (recommended), you can also configure an [ImageReference][net_imagereference] explicitly:</span></span>

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a><span data-ttu-id="8891f-164">Sanal makine görüntülerini listesi</span><span class="sxs-lookup"><span data-stu-id="8891f-164">List of virtual machine images</span></span>
<span data-ttu-id="8891f-165">Merhaba aşağıdaki tabloda bu makalenin en son güncelleştirildiği hello kullanılabilir toplu düğümü aracıları ile uyumlu olan hello Market sanal makine görüntüleri listeler.</span><span class="sxs-lookup"><span data-stu-id="8891f-165">hello following table lists hello Marketplace virtual machine images that are compatible with hello available Batch node agents when this article was last updated.</span></span> <span data-ttu-id="8891f-166">Önemli toonote görüntüleri ve aracılarını veya herhangi bir anda kaldırılamaz bu listeyi kesin olmadığından emin olur.</span><span class="sxs-lookup"><span data-stu-id="8891f-166">It is important toonote that this list is not definitive because images and node agents may be added or removed at any time.</span></span> <span data-ttu-id="8891f-167">Toplu işlem uygulamaları ve Hizmetleri zaman kullanmanızı öneririz [list_node_agent_skus] [ py_list_skus] (Python) ve [ListNodeAgentSkus] [ net_list_skus] Şu anda kullanılabilir SKU'ları (batch .NET) toodetermine ve arasından seçim hello.</span><span class="sxs-lookup"><span data-stu-id="8891f-167">We recommend that your Batch applications and services always use [list_node_agent_skus][py_list_skus] (Python) and [ListNodeAgentSkus][net_list_skus] (Batch .NET) toodetermine and select from hello currently available SKUs.</span></span>

> [!WARNING]
> <span data-ttu-id="8891f-168">liste aşağıdaki hello herhangi bir zamanda değişebilir.</span><span class="sxs-lookup"><span data-stu-id="8891f-168">hello following list may change at any time.</span></span> <span data-ttu-id="8891f-169">Her zaman hello kullan **listesi düğüm Aracısı SKU** hello Batch API'lerini toolist kullanılabilir yöntemleri, uyumlu bir sanal makine ve düğüm Aracısı SKU'ları, Batch işleriniz çalıştırdığınızda hello.</span><span class="sxs-lookup"><span data-stu-id="8891f-169">Always use hello **list node agent SKU** methods available in hello Batch APIs toolist hello compatible virtual machine and node agent SKUs when you run your Batch jobs.</span></span>
>
>

| <span data-ttu-id="8891f-170">**Yayımcı**</span><span class="sxs-lookup"><span data-stu-id="8891f-170">**Publisher**</span></span> | <span data-ttu-id="8891f-171">**Teklif**</span><span class="sxs-lookup"><span data-stu-id="8891f-171">**Offer**</span></span> | <span data-ttu-id="8891f-172">**Görüntü SKU**</span><span class="sxs-lookup"><span data-stu-id="8891f-172">**Image SKU**</span></span> | <span data-ttu-id="8891f-173">**Sürüm**</span><span class="sxs-lookup"><span data-stu-id="8891f-173">**Version**</span></span> | <span data-ttu-id="8891f-174">**Düğüm Aracısı SKU kimliği**</span><span class="sxs-lookup"><span data-stu-id="8891f-174">**Node agent SKU ID**</span></span> |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| <span data-ttu-id="8891f-175">Canonical</span><span class="sxs-lookup"><span data-stu-id="8891f-175">Canonical</span></span> | <span data-ttu-id="8891f-176">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="8891f-176">UbuntuServer</span></span> | <span data-ttu-id="8891f-177">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="8891f-177">14.04.5-LTS</span></span> | <span data-ttu-id="8891f-178">en son</span><span class="sxs-lookup"><span data-stu-id="8891f-178">latest</span></span> | <span data-ttu-id="8891f-179">Batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="8891f-179">batch.node.ubuntu 14.04</span></span> |
| <span data-ttu-id="8891f-180">Canonical</span><span class="sxs-lookup"><span data-stu-id="8891f-180">Canonical</span></span> | <span data-ttu-id="8891f-181">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="8891f-181">UbuntuServer</span></span> | <span data-ttu-id="8891f-182">16.04.0-LTS</span><span class="sxs-lookup"><span data-stu-id="8891f-182">16.04.0-LTS</span></span> | <span data-ttu-id="8891f-183">en son</span><span class="sxs-lookup"><span data-stu-id="8891f-183">latest</span></span> | <span data-ttu-id="8891f-184">Batch.node.ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="8891f-184">batch.node.ubuntu 16.04</span></span> |
| <span data-ttu-id="8891f-185">Credativ</span><span class="sxs-lookup"><span data-stu-id="8891f-185">Credativ</span></span> | <span data-ttu-id="8891f-186">Debian</span><span class="sxs-lookup"><span data-stu-id="8891f-186">Debian</span></span> | <span data-ttu-id="8891f-187">8</span><span class="sxs-lookup"><span data-stu-id="8891f-187">8</span></span> | <span data-ttu-id="8891f-188">en son</span><span class="sxs-lookup"><span data-stu-id="8891f-188">latest</span></span> | <span data-ttu-id="8891f-189">Batch.node.debian 8</span><span class="sxs-lookup"><span data-stu-id="8891f-189">batch.node.debian 8</span></span> |
| <span data-ttu-id="8891f-190">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="8891f-190">OpenLogic</span></span> | <span data-ttu-id="8891f-191">CentOS</span><span class="sxs-lookup"><span data-stu-id="8891f-191">CentOS</span></span> | <span data-ttu-id="8891f-192">7.0</span><span class="sxs-lookup"><span data-stu-id="8891f-192">7.0</span></span> | <span data-ttu-id="8891f-193">en son</span><span class="sxs-lookup"><span data-stu-id="8891f-193">latest</span></span> | <span data-ttu-id="8891f-194">Batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="8891f-194">batch.node.centos 7</span></span> |
| <span data-ttu-id="8891f-195">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="8891f-195">OpenLogic</span></span> | <span data-ttu-id="8891f-196">CentOS</span><span class="sxs-lookup"><span data-stu-id="8891f-196">CentOS</span></span> | <span data-ttu-id="8891f-197">7.1</span><span class="sxs-lookup"><span data-stu-id="8891f-197">7.1</span></span> | <span data-ttu-id="8891f-198">en son</span><span class="sxs-lookup"><span data-stu-id="8891f-198">latest</span></span> | <span data-ttu-id="8891f-199">Batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="8891f-199">batch.node.centos 7</span></span> |
| <span data-ttu-id="8891f-200">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="8891f-200">OpenLogic</span></span> | <span data-ttu-id="8891f-201">CentOS HPC</span><span class="sxs-lookup"><span data-stu-id="8891f-201">CentOS-HPC</span></span> | <span data-ttu-id="8891f-202">7.1</span><span class="sxs-lookup"><span data-stu-id="8891f-202">7.1</span></span> | <span data-ttu-id="8891f-203">en son</span><span class="sxs-lookup"><span data-stu-id="8891f-203">latest</span></span> | <span data-ttu-id="8891f-204">Batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="8891f-204">batch.node.centos 7</span></span> |
| <span data-ttu-id="8891f-205">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="8891f-205">OpenLogic</span></span> | <span data-ttu-id="8891f-206">CentOS</span><span class="sxs-lookup"><span data-stu-id="8891f-206">CentOS</span></span> | <span data-ttu-id="8891f-207">7.2</span><span class="sxs-lookup"><span data-stu-id="8891f-207">7.2</span></span> | <span data-ttu-id="8891f-208">en son</span><span class="sxs-lookup"><span data-stu-id="8891f-208">latest</span></span> | <span data-ttu-id="8891f-209">Batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="8891f-209">batch.node.centos 7</span></span> |
| <span data-ttu-id="8891f-210">Oracle</span><span class="sxs-lookup"><span data-stu-id="8891f-210">Oracle</span></span> | <span data-ttu-id="8891f-211">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="8891f-211">Oracle-Linux</span></span> | <span data-ttu-id="8891f-212">7.0</span><span class="sxs-lookup"><span data-stu-id="8891f-212">7.0</span></span> | <span data-ttu-id="8891f-213">en son</span><span class="sxs-lookup"><span data-stu-id="8891f-213">latest</span></span> | <span data-ttu-id="8891f-214">Batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="8891f-214">batch.node.centos 7</span></span> |
| <span data-ttu-id="8891f-215">Oracle</span><span class="sxs-lookup"><span data-stu-id="8891f-215">Oracle</span></span> | <span data-ttu-id="8891f-216">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="8891f-216">Oracle-Linux</span></span> | <span data-ttu-id="8891f-217">7.2</span><span class="sxs-lookup"><span data-stu-id="8891f-217">7.2</span></span> | <span data-ttu-id="8891f-218">en son</span><span class="sxs-lookup"><span data-stu-id="8891f-218">latest</span></span> | <span data-ttu-id="8891f-219">Batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="8891f-219">batch.node.centos 7</span></span> |
| <span data-ttu-id="8891f-220">SUSE</span><span class="sxs-lookup"><span data-stu-id="8891f-220">SUSE</span></span> | <span data-ttu-id="8891f-221">openSUSE</span><span class="sxs-lookup"><span data-stu-id="8891f-221">openSUSE</span></span> | <span data-ttu-id="8891f-222">13.2</span><span class="sxs-lookup"><span data-stu-id="8891f-222">13.2</span></span> | <span data-ttu-id="8891f-223">en son</span><span class="sxs-lookup"><span data-stu-id="8891f-223">latest</span></span> | <span data-ttu-id="8891f-224">Batch.node.opensuse 13.2</span><span class="sxs-lookup"><span data-stu-id="8891f-224">batch.node.opensuse 13.2</span></span> |
| <span data-ttu-id="8891f-225">SUSE</span><span class="sxs-lookup"><span data-stu-id="8891f-225">SUSE</span></span> | <span data-ttu-id="8891f-226">openSUSE artık</span><span class="sxs-lookup"><span data-stu-id="8891f-226">openSUSE-Leap</span></span> | <span data-ttu-id="8891f-227">42.1</span><span class="sxs-lookup"><span data-stu-id="8891f-227">42.1</span></span> | <span data-ttu-id="8891f-228">en son</span><span class="sxs-lookup"><span data-stu-id="8891f-228">latest</span></span> | <span data-ttu-id="8891f-229">Batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="8891f-229">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="8891f-230">SUSE</span><span class="sxs-lookup"><span data-stu-id="8891f-230">SUSE</span></span> | <span data-ttu-id="8891f-231">SLES</span><span class="sxs-lookup"><span data-stu-id="8891f-231">SLES</span></span> | <span data-ttu-id="8891f-232">12 SP1</span><span class="sxs-lookup"><span data-stu-id="8891f-232">12-SP1</span></span> | <span data-ttu-id="8891f-233">en son</span><span class="sxs-lookup"><span data-stu-id="8891f-233">latest</span></span> | <span data-ttu-id="8891f-234">Batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="8891f-234">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="8891f-235">SUSE</span><span class="sxs-lookup"><span data-stu-id="8891f-235">SUSE</span></span> | <span data-ttu-id="8891f-236">SLES HPC</span><span class="sxs-lookup"><span data-stu-id="8891f-236">SLES-HPC</span></span> | <span data-ttu-id="8891f-237">12 SP1</span><span class="sxs-lookup"><span data-stu-id="8891f-237">12-SP1</span></span> | <span data-ttu-id="8891f-238">en son</span><span class="sxs-lookup"><span data-stu-id="8891f-238">latest</span></span> | <span data-ttu-id="8891f-239">Batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="8891f-239">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="8891f-240">Microsoft reklam</span><span class="sxs-lookup"><span data-stu-id="8891f-240">microsoft-ads</span></span> | <span data-ttu-id="8891f-241">Linux veri bilimi vm</span><span class="sxs-lookup"><span data-stu-id="8891f-241">linux-data-science-vm</span></span> | <span data-ttu-id="8891f-242">linuxdsvm</span><span class="sxs-lookup"><span data-stu-id="8891f-242">linuxdsvm</span></span> | <span data-ttu-id="8891f-243">en son</span><span class="sxs-lookup"><span data-stu-id="8891f-243">latest</span></span> | <span data-ttu-id="8891f-244">Batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="8891f-244">batch.node.centos 7</span></span> |
| <span data-ttu-id="8891f-245">Microsoft reklam</span><span class="sxs-lookup"><span data-stu-id="8891f-245">microsoft-ads</span></span> | <span data-ttu-id="8891f-246">Standart veri bilimi vm</span><span class="sxs-lookup"><span data-stu-id="8891f-246">standard-data-science-vm</span></span> | <span data-ttu-id="8891f-247">Standart veri bilimi vm</span><span class="sxs-lookup"><span data-stu-id="8891f-247">standard-data-science-vm</span></span> | <span data-ttu-id="8891f-248">en son</span><span class="sxs-lookup"><span data-stu-id="8891f-248">latest</span></span> | <span data-ttu-id="8891f-249">Batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="8891f-249">batch.node.windows amd64</span></span> |
| <span data-ttu-id="8891f-250">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="8891f-250">MicrosoftWindowsServer</span></span> | <span data-ttu-id="8891f-251">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="8891f-251">WindowsServer</span></span> | <span data-ttu-id="8891f-252">2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="8891f-252">2008-R2-SP1</span></span> | <span data-ttu-id="8891f-253">en son</span><span class="sxs-lookup"><span data-stu-id="8891f-253">latest</span></span> | <span data-ttu-id="8891f-254">Batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="8891f-254">batch.node.windows amd64</span></span> |
| <span data-ttu-id="8891f-255">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="8891f-255">MicrosoftWindowsServer</span></span> | <span data-ttu-id="8891f-256">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="8891f-256">WindowsServer</span></span> | <span data-ttu-id="8891f-257">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="8891f-257">2012-Datacenter</span></span> | <span data-ttu-id="8891f-258">en son</span><span class="sxs-lookup"><span data-stu-id="8891f-258">latest</span></span> | <span data-ttu-id="8891f-259">Batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="8891f-259">batch.node.windows amd64</span></span> |
| <span data-ttu-id="8891f-260">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="8891f-260">MicrosoftWindowsServer</span></span> | <span data-ttu-id="8891f-261">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="8891f-261">WindowsServer</span></span> | <span data-ttu-id="8891f-262">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="8891f-262">2012-R2-Datacenter</span></span> | <span data-ttu-id="8891f-263">en son</span><span class="sxs-lookup"><span data-stu-id="8891f-263">latest</span></span> | <span data-ttu-id="8891f-264">Batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="8891f-264">batch.node.windows amd64</span></span> |
| <span data-ttu-id="8891f-265">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="8891f-265">MicrosoftWindowsServer</span></span> | <span data-ttu-id="8891f-266">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="8891f-266">WindowsServer</span></span> | <span data-ttu-id="8891f-267">2016 Datacenter</span><span class="sxs-lookup"><span data-stu-id="8891f-267">2016-Datacenter</span></span> | <span data-ttu-id="8891f-268">en son</span><span class="sxs-lookup"><span data-stu-id="8891f-268">latest</span></span> | <span data-ttu-id="8891f-269">Batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="8891f-269">batch.node.windows amd64</span></span> |
| <span data-ttu-id="8891f-270">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="8891f-270">MicrosoftWindowsServer</span></span> | <span data-ttu-id="8891f-271">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="8891f-271">WindowsServer</span></span> | <span data-ttu-id="8891f-272">Kapsayıcılar ile 2016 Datacenter</span><span class="sxs-lookup"><span data-stu-id="8891f-272">2016-Datacenter-with-Containers</span></span> | <span data-ttu-id="8891f-273">en son</span><span class="sxs-lookup"><span data-stu-id="8891f-273">latest</span></span> | <span data-ttu-id="8891f-274">Batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="8891f-274">batch.node.windows amd64</span></span> |

## <a name="connect-toolinux-nodes-using-ssh"></a><span data-ttu-id="8891f-275">SSH kullanarak tooLinux düğümler Bağlan</span><span class="sxs-lookup"><span data-stu-id="8891f-275">Connect tooLinux nodes using SSH</span></span>
<span data-ttu-id="8891f-276">Geliştirme sırasında veya sorun giderme sırasında bu gerekli toosign toohello düğümlerdeki havuzunuzdaki bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8891f-276">During development or while troubleshooting, you may find it necessary toosign in toohello nodes in your pool.</span></span> <span data-ttu-id="8891f-277">Windows işlem düğümleri, Uzak Masaüstü Protokolü (RDP) tooconnect tooLinux düğümleri kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="8891f-277">Unlike Windows compute nodes, you cannot use Remote Desktop Protocol (RDP) tooconnect tooLinux nodes.</span></span> <span data-ttu-id="8891f-278">Bunun yerine, hello Batch hizmeti uzak bağlantı için her düğümde SSH erişimini etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="8891f-278">Instead, hello Batch service enables SSH access on each node for remote connection.</span></span>

<span data-ttu-id="8891f-279">Merhaba aşağıdaki Python kod parçacığını bir kullanıcı uzak bağlantı için bir havuzdaki her düğümde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8891f-279">hello following Python code snippet creates a user on each node in a pool, which is required for remote connection.</span></span> <span data-ttu-id="8891f-280">Ardından, her düğüm için hello güvenli Kabuk (SSH) bağlantı bilgilerini yazdırır.</span><span class="sxs-lookup"><span data-stu-id="8891f-280">It then prints hello secure shell (SSH) connection information for each node.</span></span>

```python
import datetime
import getpass
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify your own account credentials
batch_account_name = ''
batch_account_key = ''
batch_account_url = ''

# Specify hello ID of an existing pool containing Linux nodes
# currently in hello 'idle' state
pool_id = ''

# Specify hello username and prompt for a password
username = 'linuxuser'
password = getpass.getpass()

# Create a BatchClient
credentials = batchauth.SharedKeyCredentials(
    batch_account_name,
    batch_account_key
)
batch_client = batch.BatchServiceClient(
        credentials,
        base_url=batch_account_url
)

# Create hello user that will be added tooeach node in hello pool
user = batchmodels.ComputeNodeUser(username)
user.password = password
user.is_admin = True
user.expiry_time = \
    (datetime.datetime.today() + datetime.timedelta(days=30)).isoformat()

# Get hello list of nodes in hello pool
nodes = batch_client.compute_node.list(pool_id)

# Add hello user tooeach node in hello pool and print
# hello connection information for hello node
for node in nodes:
    # Add hello user toohello node
    batch_client.compute_node.add_user(pool_id, node.id, user)

    # Obtain SSH login information for hello node
    login = batch_client.compute_node.get_remote_login_settings(pool_id,
                                                                node.id)

    # Print hello connection info for hello node
    print("{0} | {1} | {2} | {3}".format(node.id,
                                         node.state,
                                         login.remote_login_ip_address,
                                         login.remote_login_port))
```

<span data-ttu-id="8891f-281">Merhaba önceki kodu dört Linux düğümleri içeren bir havuz için örnek çıktı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="8891f-281">Here is sample output for hello previous code for a pool that contains four Linux nodes:</span></span>

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

<span data-ttu-id="8891f-282">Bir düğümde bir kullanıcı oluşturduğunuzda, bir parola yerine bir SSH ortak anahtarı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8891f-282">Instead of a password, you can specify an SSH public key when you create a user on a node.</span></span> <span data-ttu-id="8891f-283">Hello Python SDK'sı, hello kullan **ssh_public_key** parametresini [ComputeNodeUser][py_computenodeuser].</span><span class="sxs-lookup"><span data-stu-id="8891f-283">In hello Python SDK, use hello **ssh_public_key** parameter on [ComputeNodeUser][py_computenodeuser].</span></span> <span data-ttu-id="8891f-284">.NET içinde hello kullan [ComputeNodeUser][net_computenodeuser].[ SshPublicKey] [ net_ssh_key] özelliği.</span><span class="sxs-lookup"><span data-stu-id="8891f-284">In .NET, use hello [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key] property.</span></span>

## <a name="pricing"></a><span data-ttu-id="8891f-285">Fiyatlandırma</span><span class="sxs-lookup"><span data-stu-id="8891f-285">Pricing</span></span>
<span data-ttu-id="8891f-286">Azure Batch Azure Cloud Services ve Azure sanal makineleri teknolojisi üzerine kurulmuştur.</span><span class="sxs-lookup"><span data-stu-id="8891f-286">Azure Batch is built on Azure Cloud Services and Azure Virtual Machines technology.</span></span> <span data-ttu-id="8891f-287">Merhaba Batch hizmeti kendisi yalnızca hello için ücretlendirilirsiniz anlamına gelir işlem Batch hesaplarınızın kaynaklarını hiçbir ücret ödemeden sunulur.</span><span class="sxs-lookup"><span data-stu-id="8891f-287">hello Batch service itself is offered at no cost, which means you are charged only for hello compute resources that your Batch solutions consume.</span></span> <span data-ttu-id="8891f-288">Seçtiğinizde **Cloud Services Yapılandırması**, temel hello üzerinde ücretlendirilirsiniz [bulut Hizmetleri fiyatlandırma] [ cloud_services_pricing] yapısı.</span><span class="sxs-lookup"><span data-stu-id="8891f-288">When you choose **Cloud Services Configuration**, you are charged based on hello [Cloud Services pricing][cloud_services_pricing] structure.</span></span> <span data-ttu-id="8891f-289">Seçtiğinizde **sanal makine yapılandırması**, temel hello üzerinde ücretlendirilirsiniz [sanal makineler fiyatlandırma] [ vm_pricing] yapısı.</span><span class="sxs-lookup"><span data-stu-id="8891f-289">When you choose **Virtual Machine Configuration**, you are charged based on hello [Virtual Machines pricing][vm_pricing] structure.</span></span> 

<span data-ttu-id="8891f-290">Uygulamaları tooyour toplu işlem düğümleri kullanarak dağıtırsanız [uygulama paketleri](batch-application-packages.md), uygulama paketlerinizi kullandığını hello Azure Storage kaynakları için ücretlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8891f-290">If you deploy applications tooyour Batch nodes using [application packages](batch-application-packages.md), you are also charged for hello Azure Storage resources that your application packages consume.</span></span> <span data-ttu-id="8891f-291">Genel olarak, hello Azure Storage maliyetleri en az.</span><span class="sxs-lookup"><span data-stu-id="8891f-291">In general, hello Azure Storage costs are minimal.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8891f-292">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8891f-292">Next steps</span></span>
### <a name="batch-python-tutorial"></a><span data-ttu-id="8891f-293">Batch Python öğreticisi</span><span class="sxs-lookup"><span data-stu-id="8891f-293">Batch Python tutorial</span></span>
<span data-ttu-id="8891f-294">Konusunda daha ayrıntılı bir öğretici için Python, kullanıma kullanarak Batch ile toowork [hello Azure Batch Python istemcisini kullanmaya başlama](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="8891f-294">For a more in-depth tutorial about how toowork with Batch by using Python, check out [Get started with hello Azure Batch Python client](batch-python-tutorial.md).</span></span> <span data-ttu-id="8891f-295">Kendi yardımcı [kod örneği] [ github_samples_pyclient] yardımcı bir işlev içerir `get_vm_config_for_distro`, başka bir teknik tooobtain bir sanal makine yapılandırmasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="8891f-295">Its companion [code sample][github_samples_pyclient] includes a helper function, `get_vm_config_for_distro`, that shows another technique tooobtain a virtual machine configuration.</span></span>

### <a name="batch-python-code-samples"></a><span data-ttu-id="8891f-296">Batch Python kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="8891f-296">Batch Python code samples</span></span>
<span data-ttu-id="8891f-297">Merhaba [Python kod örnekleri] [ github_samples_py] hello içinde [azure-batch-samples] [ github_samples] github'daki nasıl Göster komut dosyaları içeren tooperform havuz, iş ve görev oluşturma gibi ortak toplu işlemleri.</span><span class="sxs-lookup"><span data-stu-id="8891f-297">hello [Python code samples][github_samples_py] in hello [azure-batch-samples][github_samples] repository on GitHub contain scripts that show you how tooperform common Batch operations, such as pool, job, and task creation.</span></span> <span data-ttu-id="8891f-298">Merhaba [Benioku] [ github_py_readme] hello Python örnekleri eşlik nasıl tooinstall hello paketleri gerekli hakkında ayrıntılar bulunur.</span><span class="sxs-lookup"><span data-stu-id="8891f-298">hello [README][github_py_readme] that accompanies hello Python samples has details about how tooinstall hello required packages.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="8891f-299">Toplu İşlem forumu</span><span class="sxs-lookup"><span data-stu-id="8891f-299">Batch forum</span></span>
<span data-ttu-id="8891f-300">Merhaba [Azure toplu işlem Forumu] [ forum] MSDN'de mükemmel toodiscuss toplu yerleştirin ve hello hizmeti hakkında soru sorun olduğunu.</span><span class="sxs-lookup"><span data-stu-id="8891f-300">hello [Azure Batch Forum][forum] on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="8891f-301">"Okuma yararlı sabitlenmiş" yazılarını ve Batch çözümlerinizi derleme sırasında çıktıkları anda sorularınızı gönderin.</span><span class="sxs-lookup"><span data-stu-id="8891f-301">Read helpful "pinned" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[cloud_services_pricing]: https://azure.microsoft.com/pricing/details/cloud-services/
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_py_readme]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/README.md
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_py]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[github_samples_pyclient]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/python_tutorial_client.py
[portal]: https://portal.azure.com
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_computenodeuser]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.aspx
[net_imagereference]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.imagereference.aspx
[net_list_skus]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listnodeagentskus.aspx
[net_pool_ops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.aspx
[net_ssh_key]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.sshpublickey.aspx
[nuget_batch_net]: https://www.nuget.org/packages/Azure.Batch/
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_list_skus]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
[vm_pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/
