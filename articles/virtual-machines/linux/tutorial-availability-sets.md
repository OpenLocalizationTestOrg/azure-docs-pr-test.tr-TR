---
title: "aaaAvailability öğretici Azure Linux VM'ler için ayarlar | Microsoft Docs"
description: "Azure Linux VM'ler için Hello kullanılabilirlik kümeleri hakkında bilgi edinin."
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
ms.openlocfilehash: 2a91e4a6057180035ec51410d9fffccaca343758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a><span data-ttu-id="1e9e0-103">Nasıl toouse kullanılabilirlik kümeleri</span><span class="sxs-lookup"><span data-stu-id="1e9e0-103">How toouse availability sets</span></span>


<span data-ttu-id="1e9e0-104">Bu öğreticide, nasıl tooincrease hello kullanılabilirliği ve güvenilirliği bir özelliği kullanarak azure'da sanal makine çözümlerinizi kullanılabilirlik kümeleri adlı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-104">In this tutorial, you will learn how tooincrease hello availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="1e9e0-105">Kullanılabilirlik kümeleri, Azure üzerinde dağıttığınız VM'lerin birden çok yalıtılmış donanım kümeler arasında dağıtılır, hello emin olun.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-105">Availability sets ensure that hello VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="1e9e0-106">Bunun yapılması Azure içinde bir donanım veya yazılım hatası olur, alt kümesini, VM'ler etkilenir ve çözümünüzün genel kullanılabilir ve işletimsel kullanmadan müşterilerinizin hello açısından kalacak sağlar.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from hello perspective of your customers using it.</span></span>

<span data-ttu-id="1e9e0-107">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="1e9e0-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1e9e0-108">Kullanılabilirlik kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e9e0-108">Create an availability set</span></span>
> * <span data-ttu-id="1e9e0-109">Bir kullanılabilirlik kümesine bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e9e0-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="1e9e0-110">Kullanılabilir VM boyutları denetleyin</span><span class="sxs-lookup"><span data-stu-id="1e9e0-110">Check available VM sizes</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1e9e0-111">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="1e9e0-112">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1e9e0-113">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1e9e0-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="availability-set-overview"></a><span data-ttu-id="1e9e0-114">Kullanılabilirlik kümesi'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="1e9e0-114">Availability set overview</span></span>

<span data-ttu-id="1e9e0-115">Bir kullanılabilirlik kümesi kullanabileceğiniz bir mantıksal bir gruplandırma bir Azure veri merkezi içinde dağıtıldığında içine yerleştirin hello VM kaynakları birbirinden yalıtılmış Azure tooensure içinde bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-115">An Availability Set is a logical grouping capability that you can use in Azure tooensure that hello VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="1e9e0-116">Bu hello VM'ler arasında birden fazla fiziksel sunucu çalıştırmak bir kullanılabilirlik kümesi içinde yerleştirin Azure sağlar, işlem rafları, depolama birimi ve ağ anahtarları.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-116">Azure ensures that hello VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="1e9e0-117">Bu hello olay bir donanım ya da Azure yazılım hatası yalnızca bir alt kümesini, VM'ler etkilenir ve genel uygulamanız kalması ve toobe kullanılabilir tooyour müşteriler devam sağlar.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-117">This ensures that in hello event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue toobe available tooyour customers.</span></span> <span data-ttu-id="1e9e0-118">Toobuild güvenilir bulut çözümleri istediğiniz kullanılabilirlik kümelerini kullanarak bir önemli özelliği tooleverage durumdur.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-118">Using Availability Sets is an essential capability tooleverage when you want toobuild reliable cloud solutions.</span></span>

<span data-ttu-id="1e9e0-119">Şimdi burada 4 ön uç web sunucusu ve bir veritabanı ana bilgisayar 2 arka uç VM kullanmak bir tipik VM tabanlı çözümünü göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="1e9e0-120">Azure ile Vm'leriniz dağıtmadan önce toodefine iki kullanılabilirlik kümeleri istiyor: hello "web" katmanı ve bir kullanılabilirlik kümesi için hello "veritabanı" katmanı için bir kullanılabilirlik kümesi.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-120">With Azure, you’d want toodefine two availability sets before you deploy your VMs: one availability set for hello “web” tier and one availability set for hello “database” tier.</span></span> <span data-ttu-id="1e9e0-121">Ardından, bir parametre toohello az vm komutu oluşturun ve Azure otomatik olarak o hello hello içinde oluşturduğunuz VM'ler sağlayacak şekilde ayarlayın hello kullanılabilirlik belirtebilirsiniz yeni bir VM oluştururken kümesi yalıtılmış birden çok fiziksel donanım kaynaklarına arasında.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-121">When you create a new VM you can then specify hello availability set as a parameter toohello az vm create command, and Azure will automatically ensure that hello VMs you create within hello available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="1e9e0-122">Bir Web sunucusu veya veritabanı sunucusu VM'ler üzerinde çalıştığı hello fiziksel donanım bir sorun varsa, o hello bilmeniz yani farklı donanıma olduğundan Web sunucusu ve veritabanı VM'ler diğer örneklerini düzgün çalışır durumda.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-122">This means that if hello physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that hello other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="1e9e0-123">Toodeploy güvenilir VM tabanlı çözümler Azure içinde istediğinizde kullanılabilirlik kümeleri her zaman kullanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-123">You should always use Availability Sets when you want toodeploy reliable VM-based solutions within Azure.</span></span>


## <a name="create-an-availability-set"></a><span data-ttu-id="1e9e0-124">Kullanılabilirlik kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e9e0-124">Create an availability set</span></span>

<span data-ttu-id="1e9e0-125">Kullanılabilirlik kümesi kullanarak oluşturabileceğiniz [az vm kullanılabilirlik kümesi oluşturma](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="1e9e0-125">You can create an availability set using [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="1e9e0-126">Bu örnekte, güncelleştirme ve hata etki alanları iki hello sayısı ayarlarız *2* hello kullanılabilirlik adlandırılmış kümesi için *myAvailabilitySet* hello içinde *myResourceGroupAvailability*kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-126">In this example, we set both hello number of update and fault domains at *2* for hello availability set named *myAvailabilitySet* in hello *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="1e9e0-127">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-127">Create a resource group.</span></span>

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

<span data-ttu-id="1e9e0-128">Kullanılabilirlik kümeleri "hata etki alanları" ve "güncelleme etki alanları" arasında tooisolate kaynaklar sağlar.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-128">Availability Sets allow you tooisolate resources across "fault domains" and "update domains".</span></span> <span data-ttu-id="1e9e0-129">A **hata etki alanı** sunucu, ağ + depolama yalıtılmış bir koleksiyonunu temsil eder kaynakları.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-129">A **fault domain** represents an isolated collection of server + network + storage resources.</span></span> <span data-ttu-id="1e9e0-130">Örnek önceki hello bizim VM'ler dağıtıldığında en az iki hata etki alanları arasında dağıtılan toobe bizim kullanılabilirlik kümesi istiyoruz gösterir.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-130">In hello preceding example, we indicate that we want our availability set toobe distributed across at least two fault domains when our VMs are deployed.</span></span> <span data-ttu-id="1e9e0-131">Biz de iki arasında dağıtılmış kümesi bizim kullanılabilirlik istiyoruz belirtmek **güncelleştirme etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-131">We also indicate that we want our availability set distributed across two **update domains**.</span></span>  <span data-ttu-id="1e9e0-132">İki güncelleştirme etki alanı Azure yazılım güncelleştirmelerini gerçekleştirdiğinde VM KAYNAKLARIMIZI, hello güncelleştirilmiş bizim VM altında çalışan tüm hello yazılım önleme, yalıtılmış olduğundan emin olun aynı anda.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-132">Two update domains ensure that when Azure performs software updates our VM resources are isolated, preventing all hello software running underneath our VM from being updated at hello same time.</span></span>

## <a name="configure-virtual-network"></a><span data-ttu-id="1e9e0-133">Sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1e9e0-133">Configure virtual network</span></span>
<span data-ttu-id="1e9e0-134">Bazı sanal makineleri dağıtmak ve, dengeleyici sınayabilirsiniz önce sanal ağ kaynaklarına destekleme hello oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-134">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="1e9e0-135">Sanal ağlar hakkında daha fazla bilgi için bkz: Merhaba [Azure Sanal Ağları Yönet](tutorial-virtual-network.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-135">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="1e9e0-136">Ağ kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="1e9e0-136">Create network resources</span></span>
<span data-ttu-id="1e9e0-137">Bir sanal ağ ile oluşturma [az ağ vnet oluşturma](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="1e9e0-137">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="1e9e0-138">Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet* adlı bir alt ağ ile *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="1e9e0-138">hello following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
<span data-ttu-id="1e9e0-139">Sanal NIC ile oluşturulan [az ağ NIC oluşturma](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="1e9e0-139">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="1e9e0-140">Merhaba aşağıdaki örnek üç sanal NIC oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-140">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="1e9e0-141">(Bir sanal NIC aşağıdaki hello uygulamanızda adımları için oluşturduğunuz her VM için).</span><span class="sxs-lookup"><span data-stu-id="1e9e0-141">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="1e9e0-142">Ek sanal NIC ve sanal makineleri herhangi bir zamanda oluşturmak ve bunları toohello yük dengeleyici Ekle:</span><span class="sxs-lookup"><span data-stu-id="1e9e0-142">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

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

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="1e9e0-143">VM'ler içinde bir kullanılabilirlik kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="1e9e0-143">Create VMs inside an availability set</span></span>

<span data-ttu-id="1e9e0-144">Sanal makineleri hello kullanılabilirlik kümesi toomake hello donanım üzerinde doğru şekilde dağıtıldığından emin içinde oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-144">VMs must be created within hello availability set toomake sure they are correctly distributed across hello hardware.</span></span> <span data-ttu-id="1e9e0-145">Var olan VM tooan kullanılabilirlik kümesi oluşturulduktan sonra eklenemez.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-145">You can't add an existing VM tooan availability set after it is created.</span></span> 

<span data-ttu-id="1e9e0-146">Kullanarak bir VM oluştururken [az vm oluşturma](/cli/azure/vm#create) hello kullanılarak ayarlanan hello kullanılabilirlik belirttiğiniz `--availability-set` parametresi toospecify hello hello kullanılabilirlik kümesi adını.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-146">When you create a VM using [az vm create](/cli/azure/vm#create) you specify hello availability set using hello `--availability-set` parameter toospecify hello name of hello availability set.</span></span>

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

<span data-ttu-id="1e9e0-147">Şimdi iki sanal makine, yeni oluşturulan kullanılabilirlik kümesinde sahibiz.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-147">We now have two virtual machines within our newly created availability set.</span></span> <span data-ttu-id="1e9e0-148">İçinde olduklarından aynı hello kullanılabilirlik kümesi, Azure uyduğundan emin olabilirsiniz, hello VM'ler ve tüm kaynaklarını (veri diskleri dahil), yalıtılmış fiziksel donanım arasında dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-148">Because they are in hello same availability set, Azure will ensure that hello VMs and all their resources (including data disks) are distributed across isolated physical hardware.</span></span> <span data-ttu-id="1e9e0-149">Bu dağıtım kadar yüksek kullanılabilirlik bizim genel VM çözümünün sağlamaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-149">This distribution helps ensure much higher availability of our overall VM solution.</span></span>

<span data-ttu-id="1e9e0-150">Bir şey VM'ler ekledikçe karşılaşabileceğiniz belirli bir VM boyutu artık kullanılabilirlik kümesi içinde kullanılabilir toouse olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-150">One thing you may encounter as you add VMs is that a particular VM size is no longer available toouse within your availability set.</span></span> <span data-ttu-id="1e9e0-151">Artık varsa onu hello yalıtım kuralları hello kullanılabilirlik kümesini korurken zorlar yeterli kapasitesi tooadd Bu sorun oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-151">This issue can happen if there is no longer enough capacity tooadd it while preserving hello isolation rules hello availability set enforces.</span></span> <span data-ttu-id="1e9e0-152">Var olan kullanılabilirlik hello kullanarak kümesi içinde kullanılabilir toouse hangi VM boyutları: toosee denetleyebilirsiniz `--availability-set list-sizes` parametresi.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-152">You can check toosee what VM sizes are available toouse within an existing availability set using hello `--availability-set list-sizes` parameter.</span></span>

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="1e9e0-153">Kullanılabilir VM boyutları denetle</span><span class="sxs-lookup"><span data-stu-id="1e9e0-153">Check for available VM sizes</span></span> 

<span data-ttu-id="1e9e0-154">Daha fazla sanal makineleri toohello kullanılabilirlik kümesi daha sonra ekleyebilirsiniz, ancak hangi VM boyutları hello donanımda kullanılabilir tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-154">You can add more VMs toohello availability set later, but you need tooknow what VM sizes are available on hello hardware.</span></span> <span data-ttu-id="1e9e0-155">Kullanım [az vm kullanılabilirlik kümesi listesi-boyutları](/cli/azure/availability-set#list-sizes) tüm hello kullanılabilir boyutları hello donanımda hello kullanılabilirlik kümesi için küme toolist.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-155">Use [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) toolist all hello available sizes on hello hardware cluster for hello availability set.</span></span>

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a><span data-ttu-id="1e9e0-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1e9e0-156">Next steps</span></span>

<span data-ttu-id="1e9e0-157">Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="1e9e0-157">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1e9e0-158">Kullanılabilirlik kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e9e0-158">Create an availability set</span></span>
> * <span data-ttu-id="1e9e0-159">Bir kullanılabilirlik kümesine bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e9e0-159">Create a VM in an availability set</span></span>
> * <span data-ttu-id="1e9e0-160">Kullanılabilir VM boyutları denetleyin</span><span class="sxs-lookup"><span data-stu-id="1e9e0-160">Check available VM sizes</span></span>

<span data-ttu-id="1e9e0-161">Sanal makine ölçek kümeleri hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="1e9e0-161">Advance toohello next tutorial toolearn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1e9e0-162">VM ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e9e0-162">Create a VM scale set</span></span>](tutorial-create-vmss.md)

