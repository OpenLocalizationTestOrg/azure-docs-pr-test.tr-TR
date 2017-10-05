---
title: "Linux VM'ler için Azure kullanılabilirlik kümeleri Öğreticisi | Microsoft Docs"
description: "Linux VM'ler için Azure kullanılabilirlik kümeleri hakkında bilgi edinin."
documentationcenter: 
services: virtual-machines-linux
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 63fe3f165864f06228604cac56d06cc061ab25f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-availability-sets"></a><span data-ttu-id="391bc-103">Kullanılabilirlik kümeleri kullanma</span><span class="sxs-lookup"><span data-stu-id="391bc-103">How to use availability sets</span></span>


<span data-ttu-id="391bc-104">Bu öğreticide, kullanılabilirlik ve kullanılabilirlik kümeleri adlı bir özelliği kullanarak azure'da sanal makine çözümlerinizi güvenilirliğini artırmak öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="391bc-104">In this tutorial, you will learn how to increase the availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="391bc-105">Kullanılabilirlik kümeleri, Azure üzerinde dağıttığınız VM'ler arasında birden fazla yalıtılmış donanım küme dağıtıldığından emin olmak.</span><span class="sxs-lookup"><span data-stu-id="391bc-105">Availability sets ensure that the VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="391bc-106">Bunun yapılması Azure içinde bir donanım veya yazılım hatası olur, alt kümesini, VM'ler etkilenir ve çözümünüzün genel kullanılabilir ve kullanmaya müşterilerinizin perspektifinden işletim kalacağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="391bc-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from the perspective of your customers using it.</span></span>

<span data-ttu-id="391bc-107">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="391bc-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="391bc-108">Kullanılabilirlik kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="391bc-108">Create an availability set</span></span>
> * <span data-ttu-id="391bc-109">Bir kullanılabilirlik kümesine bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="391bc-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="391bc-110">Kullanılabilir VM boyutları denetleyin</span><span class="sxs-lookup"><span data-stu-id="391bc-110">Check available VM sizes</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="391bc-111">Yüklemek ve CLI yerel olarak kullanmak seçerseniz, Bu öğretici, Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="391bc-111">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="391bc-112">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="391bc-112">Run `az --version` to find the version.</span></span> <span data-ttu-id="391bc-113">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="391bc-113">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="availability-set-overview"></a><span data-ttu-id="391bc-114">Kullanılabilirlik kümesi'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="391bc-114">Availability set overview</span></span>

<span data-ttu-id="391bc-115">Bir kullanılabilirlik kümesi Azure'da Azure veri merkezi içinde dağıtıldığında içine yerleştirin VM kaynakları birbirinden yalıtılmış olduğundan emin olmak için kullanabileceğiniz bir mantıksal bir gruplandırma bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="391bc-115">An Availability Set is a logical grouping capability that you can use in Azure to ensure that the VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="391bc-116">Azure birden çok fiziksel sunucuda çalıştırmak bir kullanılabilirlik kümesi içinde yerleştirin VM'ler sağlar, işlem rafları, depolama birimi ve ağ anahtarları.</span><span class="sxs-lookup"><span data-stu-id="391bc-116">Azure ensures that the VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="391bc-117">Bu bir donanım veya Azure yazılım başarısız olması durumunda yalnızca bir alt kümesini, VM'ler etkilenir ve genel uygulamanız kalması ve müşterileriniz için kullanılabilir olmaya devam sağlar.</span><span class="sxs-lookup"><span data-stu-id="391bc-117">This ensures that in the event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue to be available to your customers.</span></span> <span data-ttu-id="391bc-118">Kullanılabilirlik kümelerini kullanarak, güvenilir bulut çözümleri oluşturmak istediğinizde yararlanmak için gerekli bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="391bc-118">Using Availability Sets is an essential capability to leverage when you want to build reliable cloud solutions.</span></span>

<span data-ttu-id="391bc-119">Şimdi burada 4 ön uç web sunucusu ve bir veritabanı ana bilgisayar 2 arka uç VM kullanmak bir tipik VM tabanlı çözümünü göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="391bc-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="391bc-120">Azure ile Vm'leriniz dağıtmadan önce iki kullanılabilirlik kümesi tanımlamak istersiniz: bir kullanılabilirlik kümesi için "web" katmanı ve bir kullanılabilirlik kümesi için "veritabanı" katmanı.</span><span class="sxs-lookup"><span data-stu-id="391bc-120">With Azure, you’d want to define two availability sets before you deploy your VMs: one availability set for the “web” tier and one availability set for the “database” tier.</span></span> <span data-ttu-id="391bc-121">Ardından belirtebilirsiniz yeni bir VM oluştururken kullanılabilirlik kümesi az vm parametresi komut oluşturur ve Azure otomatik olarak kullanılabilir kümesi içinde oluşturduğunuz VM'ler ilişkilendirilmesini sağlar yalıtılmış birden çok fiziksel donanım kaynaklarına arasında.</span><span class="sxs-lookup"><span data-stu-id="391bc-121">When you create a new VM you can then specify the availability set as a parameter to the az vm create command, and Azure will automatically ensure that the VMs you create within the available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="391bc-122">Bu, bir Web sunucusu veya veritabanı sunucusu sanal makineleri çalıştıran fiziksel donanımı bir sorun varsa, çünkü bunlar üzerinde farklı donanım diğer örneklerini Web sunucusu ve veritabanı VM'ler düzgün çalışır durumda olduğunu bildiğinizden anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="391bc-122">This means that if the physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that the other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="391bc-123">Azure içinde güvenilir VM tabanlı çözümler dağıtmak istediğinizde kullanılabilirlik kümeleri her zaman kullanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="391bc-123">You should always use Availability Sets when you want to deploy reliable VM-based solutions within Azure.</span></span>


## <a name="create-an-availability-set"></a><span data-ttu-id="391bc-124">Kullanılabilirlik kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="391bc-124">Create an availability set</span></span>

<span data-ttu-id="391bc-125">Kullanılabilirlik kümesi kullanarak oluşturabileceğiniz [az vm kullanılabilirlik kümesi oluşturma](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="391bc-125">You can create an availability set using [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="391bc-126">Bu örnekte, her iki güncelleştirme ve hata etki alanlarının sayısı ayarlarız *2* kullanılabilirlik adlandırılmış kümesi için *myAvailabilitySet* içinde *myResourceGroupAvailability* kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="391bc-126">In this example, we set both the number of update and fault domains at *2* for the availability set named *myAvailabilitySet* in the *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="391bc-127">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="391bc-127">Create a resource group.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAvailability --location eastus
```


```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupAvailability \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

<span data-ttu-id="391bc-128">Kullanılabilirlik kümeleri kaynaklar "hata etki alanları" ve "güncelleme etki alanları" arasında yalıtmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="391bc-128">Availability Sets allow you to isolate resources across "fault domains" and "update domains".</span></span> <span data-ttu-id="391bc-129">A **hata etki alanı** sunucu, ağ + depolama yalıtılmış bir koleksiyonunu temsil eder kaynakları.</span><span class="sxs-lookup"><span data-stu-id="391bc-129">A **fault domain** represents an isolated collection of server + network + storage resources.</span></span> <span data-ttu-id="391bc-130">Önceki örnekte bizim kullanılabilirlik bizim VM'ler dağıtıldığında en az iki hata etki alanları arasında dağıtılacak kümesi istiyoruz gösterir.</span><span class="sxs-lookup"><span data-stu-id="391bc-130">In the preceding example, we indicate that we want our availability set to be distributed across at least two fault domains when our VMs are deployed.</span></span> <span data-ttu-id="391bc-131">Biz de iki arasında dağıtılmış kümesi bizim kullanılabilirlik istiyoruz belirtmek **güncelleştirme etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="391bc-131">We also indicate that we want our availability set distributed across two **update domains**.</span></span>  <span data-ttu-id="391bc-132">İki güncelleştirme etki alanı Azure yazılım güncelleştirmelerini gerçekleştirdiğinde VM KAYNAKLARIMIZI, aynı anda güncelleştirilmiş bizim VM altında çalışan tüm yazılım önleme, yalıtılmış olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="391bc-132">Two update domains ensure that when Azure performs software updates our VM resources are isolated, preventing all the software running underneath our VM from being updated at the same time.</span></span>

## <a name="configure-virtual-network"></a><span data-ttu-id="391bc-133">Sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="391bc-133">Configure virtual network</span></span>
<span data-ttu-id="391bc-134">Bazı sanal makineleri dağıtmak ve, dengeleyici sınayabilirsiniz önce destekleyici sanal ağ kaynakları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="391bc-134">Before you deploy some VMs and can test your balancer, create the supporting virtual network resources.</span></span> <span data-ttu-id="391bc-135">Sanal ağlar hakkında daha fazla bilgi için bkz: [Azure Sanal Ağları Yönet](tutorial-virtual-network.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="391bc-135">For more information about virtual networks, see the [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="391bc-136">Ağ kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="391bc-136">Create network resources</span></span>
<span data-ttu-id="391bc-137">Bir sanal ağ ile oluşturma [az ağ vnet oluşturma](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="391bc-137">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="391bc-138">Aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet* adlı bir alt ağ ile *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="391bc-138">The following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
<span data-ttu-id="391bc-139">Sanal NIC ile oluşturulan [az ağ NIC oluşturma](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="391bc-139">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="391bc-140">Aşağıdaki örnek, üç sanal NIC oluşturur.</span><span class="sxs-lookup"><span data-stu-id="391bc-140">The following example creates three virtual NICs.</span></span> <span data-ttu-id="391bc-141">(Her VM için bir sanal NIC için aşağıdaki adımları uygulamayı oluşturduğunuz).</span><span class="sxs-lookup"><span data-stu-id="391bc-141">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="391bc-142">Ek sanal NIC ve sanal makineleri herhangi bir zamanda oluşturabilir ve bunları yük dengeleyiciye ekleyin:</span><span class="sxs-lookup"><span data-stu-id="391bc-142">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupAvailability \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="391bc-143">VM'ler içinde bir kullanılabilirlik kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="391bc-143">Create VMs inside an availability set</span></span>

<span data-ttu-id="391bc-144">Sanal makineleri kullanılabilirlik donanım üzerinde doğru şekilde dağıtıldığından emin olmak için kümesini içinde oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="391bc-144">VMs must be created within the availability set to make sure they are correctly distributed across the hardware.</span></span> <span data-ttu-id="391bc-145">Kullanılabilirlik oluşturulduktan sonra kümesi için mevcut bir VM'yi ekleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="391bc-145">You can't add an existing VM to an availability set after it is created.</span></span> 

<span data-ttu-id="391bc-146">Kullanarak bir VM oluştururken [az vm oluşturma](/cli/azure/vm#create) kullanılarak ayarlanan kullanılabilirlik belirttiğiniz `--availability-set` kullanılabilirlik kümesinin adını belirtmek için parametre.</span><span class="sxs-lookup"><span data-stu-id="391bc-146">When you create a VM using [az vm create](/cli/azure/vm#create) you specify the availability set using the `--availability-set` parameter to specify the name of the availability set.</span></span>

```azurecli-interactive 
for i in `seq 1 2`; do
   az vm create \
     --resource-group myResourceGroupAvailability \
     --name myVM$i \
     --availability-set myAvailabilitySet \
     --nics myNic$i \
     --size Standard_DS1_v2  \
     --image Canonical:UbuntuServer:14.04.4-LTS:latest \
     --admin-username azureuser \
     --generate-ssh-keys \
     --no-wait
done 
```

<span data-ttu-id="391bc-147">Şimdi iki sanal makine, yeni oluşturulan kullanılabilirlik kümesinde sahibiz.</span><span class="sxs-lookup"><span data-stu-id="391bc-147">We now have two virtual machines within our newly created availability set.</span></span> <span data-ttu-id="391bc-148">Aynı kullanılabilirlik kümesinde olduklarından, Azure sanal makineleri ve tüm kaynaklarını (veri diskleri dahil), yalıtılmış fiziksel donanım üzerinde dağıtılmış güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="391bc-148">Because they are in the same availability set, Azure will ensure that the VMs and all their resources (including data disks) are distributed across isolated physical hardware.</span></span> <span data-ttu-id="391bc-149">Bu dağıtım kadar yüksek kullanılabilirlik bizim genel VM çözümünün sağlamaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="391bc-149">This distribution helps ensure much higher availability of our overall VM solution.</span></span>

<span data-ttu-id="391bc-150">Sanal makineleri ekledikçe karşılaşabileceğiniz bir belirli bir VM boyutu artık kullanılabilirlik kümesi içinde kullanmak için kullanılabilir olan şeydir.</span><span class="sxs-lookup"><span data-stu-id="391bc-150">One thing you may encounter as you add VMs is that a particular VM size is no longer available to use within your availability set.</span></span> <span data-ttu-id="391bc-151">Artık kullanılabilirlik kümesi zorlar yalıtım kuralları korurken eklemek için yeterli kapasitesi varsa bu sorun oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="391bc-151">This issue can happen if there is no longer enough capacity to add it while preserving the isolation rules the availability set enforces.</span></span> <span data-ttu-id="391bc-152">Hangi VM boyutları varolan kullanılabilirlik kullanarak kümesi içinde kullanmak için kullanılabilir olup olmadığını kontrol edebilirsiniz `--availability-set list-sizes` parametresi.</span><span class="sxs-lookup"><span data-stu-id="391bc-152">You can check to see what VM sizes are available to use within an existing availability set using the `--availability-set list-sizes` parameter.</span></span>

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="391bc-153">Kullanılabilir VM boyutları denetle</span><span class="sxs-lookup"><span data-stu-id="391bc-153">Check for available VM sizes</span></span> 

<span data-ttu-id="391bc-154">Daha fazla sanal makineleri daha sonra ayarlamak kullanılabilirlik ekleyebilirsiniz, ancak hangi VM boyutları donanımda kullanılabilir olduğunu bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="391bc-154">You can add more VMs to the availability set later, but you need to know what VM sizes are available on the hardware.</span></span> <span data-ttu-id="391bc-155">Kullanım [az vm kullanılabilirlik kümesi listesi-boyutları](/cli/azure/availability-set#list-sizes) tüm donanım üzerinde kullanılabilir boyutları küme için kullanılabilirlik kümesi listelemek için.</span><span class="sxs-lookup"><span data-stu-id="391bc-155">Use [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) to list all the available sizes on the hardware cluster for the availability set.</span></span>

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a><span data-ttu-id="391bc-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="391bc-156">Next steps</span></span>

<span data-ttu-id="391bc-157">Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="391bc-157">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="391bc-158">Kullanılabilirlik kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="391bc-158">Create an availability set</span></span>
> * <span data-ttu-id="391bc-159">Bir kullanılabilirlik kümesine bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="391bc-159">Create a VM in an availability set</span></span>
> * <span data-ttu-id="391bc-160">Kullanılabilir VM boyutları denetleyin</span><span class="sxs-lookup"><span data-stu-id="391bc-160">Check available VM sizes</span></span>

<span data-ttu-id="391bc-161">Sanal makine ölçek kümeleri hakkında bilgi edinmek için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="391bc-161">Advance to the next tutorial to learn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="391bc-162">VM ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="391bc-162">Create a VM scale set</span></span>](tutorial-create-vmss.md)

