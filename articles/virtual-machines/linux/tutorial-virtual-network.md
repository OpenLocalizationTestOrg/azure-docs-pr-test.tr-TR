---
title: "Azure sanal ağlar ve Linux sanal makineleri | Microsoft Docs"
description: "Öğretici - Azure sanal ağlar ve Azure CLI ile Linux sanal makineleri yönetme"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2366905b8160675f77cbc41ba97540af70be8c01
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-the-azure-cli"></a><span data-ttu-id="ec5e7-103">Azure sanal ağlar ve Azure CLI ile Linux sanal makineleri yönetme</span><span class="sxs-lookup"><span data-stu-id="ec5e7-103">Manage Azure Virtual Networks and Linux Virtual Machines with the Azure CLI</span></span>

<span data-ttu-id="ec5e7-104">Azure sanal makineler, iç ve dış ağ iletişimi için Azure ağ kullanın.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="ec5e7-105">Bu öğreticide iki sanal makine dağıtma ve bu VM'ler için Azure ağı yapılandırma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-105">This tutorial walks through deploying two virtual machines and configuring Azure networking for these VMs.</span></span> <span data-ttu-id="ec5e7-106">Bir uygulama öğreticide dağıtılmamış ancak bu öğreticide örneklerde, sanal makineleri bir veritabanı arka uç, web uygulamasıyla barındırıyorsanız varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-106">The examples in this tutorial assume that the VMs are hosting a web application with a database back-end, however an application is not deployed in the tutorial.</span></span> <span data-ttu-id="ec5e7-107">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="ec5e7-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ec5e7-108">Sanal ağ dağıtma</span><span class="sxs-lookup"><span data-stu-id="ec5e7-108">Deploy a virtual network</span></span>
> * <span data-ttu-id="ec5e7-109">Bir alt ağ içinde bir sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="ec5e7-109">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="ec5e7-110">Sanal makineler için bir alt ağ ekleme</span><span class="sxs-lookup"><span data-stu-id="ec5e7-110">Attach virtual machines to a subnet</span></span>
> * <span data-ttu-id="ec5e7-111">Sanal makine ortak IP adreslerini yönetin</span><span class="sxs-lookup"><span data-stu-id="ec5e7-111">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="ec5e7-112">Gelen Internet trafiği güvenli</span><span class="sxs-lookup"><span data-stu-id="ec5e7-112">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="ec5e7-113">VM VM trafiğinin güvenliğini</span><span class="sxs-lookup"><span data-stu-id="ec5e7-113">Secure VM to VM traffic</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ec5e7-114">Yüklemek ve CLI yerel olarak kullanmak seçerseniz, Bu öğretici, Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-114">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="ec5e7-115">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="ec5e7-116">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ec5e7-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="vm-networking-overview"></a><span data-ttu-id="ec5e7-117">VM ağ genel bakış</span><span class="sxs-lookup"><span data-stu-id="ec5e7-117">VM networking overview</span></span>

<span data-ttu-id="ec5e7-118">Azure sanal ağlar arasında sanal makineleri, internet ve diğer Azure hizmetleriyle Azure SQL veritabanı gibi güvenli ağ bağlantıları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-118">Azure virtual networks enable secure network connections between virtual machines, the internet, and other Azure services such as Azure SQL database.</span></span> <span data-ttu-id="ec5e7-119">Sanal ağlar alt ağ olarak adlandırılan mantıksal parçalara bölünür.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-119">Virtual networks are broken down into logical segments called subnets.</span></span> <span data-ttu-id="ec5e7-120">Alt ağ akış denetimi ve güvenlik sınırı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-120">Subnets are used to control network flow, and as a security boundary.</span></span> <span data-ttu-id="ec5e7-121">Bir VM dağıtırken, genellikle bir alt ağa bağlı bir sanal ağ arabirimi içerir.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-121">When deploying a VM, it generally includes a virtual network interface, which is attached to a subnet.</span></span>

## <a name="deploy-virtual-network"></a><span data-ttu-id="ec5e7-122">Sanal ağ dağıtma</span><span class="sxs-lookup"><span data-stu-id="ec5e7-122">Deploy virtual network</span></span>

<span data-ttu-id="ec5e7-123">Bu öğreticide, tek bir sanal ağı iki alt ağ ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-123">For this tutorial, a single virtual network is created with two subnets.</span></span> <span data-ttu-id="ec5e7-124">Bir web uygulamasını barındırmak için bir ön uç alt ağı ve bir veritabanı sunucusunu barındırmak için bir arka uç alt ağ.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-124">A front-end subnet for hosting a web application, and a back-end subnet for hosting a database server.</span></span>

<span data-ttu-id="ec5e7-125">Bir sanal ağ oluşturmadan önce bir kaynak grubuyla oluşturmanız [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="ec5e7-125">Before you can create a virtual network, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="ec5e7-126">Aşağıdaki örnek, bir kaynak grubu oluşturur *myRGNetwork* eastus konumda.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-126">The following example creates a resource group named *myRGNetwork* in the eastus location.</span></span>

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a><span data-ttu-id="ec5e7-127">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="ec5e7-127">Create virtual network</span></span>

<span data-ttu-id="ec5e7-128">Bize [az ağ vnet oluşturma](/cli/azure/network/vnet#create) bir sanal ağ oluşturmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-128">Us the [az network vnet create](/cli/azure/network/vnet#create) command to create a virtual network.</span></span> <span data-ttu-id="ec5e7-129">Bu örnekte, adlandırılmış ağ *mvVnet* ve bir adres öneki belirtilen *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-129">In this example, the network is named *mvVnet* and is given an address prefix of *10.0.0.0/16*.</span></span> <span data-ttu-id="ec5e7-130">Bir alt ağ da bir ad oluşturulur *mySubnetFrontEnd* ve bir önek *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-130">A subnet is also created with a name of *mySubnetFrontEnd* and a prefix of *10.0.1.0/24*.</span></span> <span data-ttu-id="ec5e7-131">Daha sonra Bu öğreticide bir ön uç VM bu alt ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-131">Later in this tutorial a front-end VM is connected to this subnet.</span></span> 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a><span data-ttu-id="ec5e7-132">Alt ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="ec5e7-132">Create subnet</span></span>

<span data-ttu-id="ec5e7-133">Sanal ağ kullanmaya yeni bir alt ağ eklenen [az ağ sanal alt oluşturmak](/cli/azure/network/vnet/subnet#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-133">A new subnet is added to the virtual network using the [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command.</span></span> <span data-ttu-id="ec5e7-134">Bu örnekte, alt ağ olarak adlandırılır *mySubnetBackEnd* ve bir adres öneki belirtilen *10.0.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-134">In this example, the subnet is named *mySubnetBackEnd* and is given an address prefix of *10.0.2.0/24*.</span></span> <span data-ttu-id="ec5e7-135">Bu alt ağ ile tüm arka uç hizmetlerini kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-135">This subnet is used with all back-end services.</span></span>

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

<span data-ttu-id="ec5e7-136">Bu noktada, ağ oluşturulduğundan ve iki alt ağ, ön uç Hizmetleri için bir tane ve arka uç hizmetlerini için başka bir içine bölümlenmiş.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-136">At this point, a network has been created and segmented into two subnets, one for front-end services, and another for back-end services.</span></span> <span data-ttu-id="ec5e7-137">Sonraki bölümde, sanal makineleri oluşturulur ve bu alt ağlara bağlı.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-137">In the next section, virtual machines are created and connected to these subnets.</span></span>

## <a name="understand-public-ip-address"></a><span data-ttu-id="ec5e7-138">Genel IP adresi anlama</span><span class="sxs-lookup"><span data-stu-id="ec5e7-138">Understand public IP address</span></span>

<span data-ttu-id="ec5e7-139">Bir ortak IP adresi Internet üzerinden erişilebilir olması Azure kaynaklarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-139">A public IP address allows Azure resources to be accessible on the internet.</span></span> <span data-ttu-id="ec5e7-140">Öğreticinin bu bölümünde, ortak IP adresleri ile çalışmaya nasıl göstermek için bir VM oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-140">In this section of the tutorial, a VM is created to demonstrate how to work with public IP addresses.</span></span>

### <a name="allocation-method"></a><span data-ttu-id="ec5e7-141">Ayırma yöntemi</span><span class="sxs-lookup"><span data-stu-id="ec5e7-141">Allocation method</span></span>

<span data-ttu-id="ec5e7-142">Bir ortak IP adresi dinamik veya statik olarak ayrılabilir.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-142">A public IP address can be allocated as either dynamic or static.</span></span> <span data-ttu-id="ec5e7-143">Varsayılan olarak, dinamik olarak ayrılan ortak IP adresi.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-143">By default, public IP address dynamically allocated.</span></span> <span data-ttu-id="ec5e7-144">Bir VM serbest bırakıldığında dinamik IP adresleri serbest bırakılır.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-144">Dynamic IP addresses are released when a VM is deallocated.</span></span> <span data-ttu-id="ec5e7-145">Bu davranış VM ayırmayı kaldırma içeren herhangi bir işlem sırasında değiştirmek IP adresi neden olur.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-145">This behavior causes the IP address to change during any operation that includes a VM deallocation.</span></span>

<span data-ttu-id="ec5e7-146">Ayırma yöntemi, IP sağlar çok statik ayarlanabilir adres kalır bir VM için atanan bile deallocated aşamasında.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-146">The allocation method can be set to static, which ensures that the IP address remain assigned to a VM, even during a deallocated state.</span></span> <span data-ttu-id="ec5e7-147">Statik olarak ayrılmış bir IP adresi kullanıldığında, IP adresi belirtilemez.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-147">When using a statically allocated IP address, the IP address itself cannot be specified.</span></span> <span data-ttu-id="ec5e7-148">Bunun yerine, kullanılabilir adresler havuzundan tahsis edilir.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-148">Instead, it is allocated from a pool of available addresses.</span></span>

### <a name="dynamic-allocation"></a><span data-ttu-id="ec5e7-149">Dinamik ayırma</span><span class="sxs-lookup"><span data-stu-id="ec5e7-149">Dynamic allocation</span></span>

<span data-ttu-id="ec5e7-150">Bir VM oluştururken [az vm oluşturma](/cli/azure/vm#create) varsayılan genel IP adresi ayırma yöntemi dinamik komutu.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-150">When creating a VM with the [az vm create](/cli/azure/vm#create) command, the default public IP address allocation method is dynamic.</span></span> <span data-ttu-id="ec5e7-151">Aşağıdaki örnekte, bir VM dinamik bir IP adresi ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-151">In the following example, a VM is created with a dynamic IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a><span data-ttu-id="ec5e7-152">Statik ayırma</span><span class="sxs-lookup"><span data-stu-id="ec5e7-152">Static allocation</span></span>

<span data-ttu-id="ec5e7-153">Kullanarak bir sanal makine oluştururken [az vm oluşturma](/cli/azure/vm#create) içeriyor, komut `--public-ip-address-allocation static` bir statik genel IP adresi atamak için bağımsız değişken.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-153">When creating a virtual machine using the [az vm create](/cli/azure/vm#create) command, include the `--public-ip-address-allocation static` argument to assign a static public IP address.</span></span> <span data-ttu-id="ec5e7-154">Sonraki bölümde dinamik olarak ayrılan bir IP adresi statik olarak ayrılan adresine değiştirilir ancak bu öğreticide, bu işlem gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-154">This operation is not demonstrated in this tutorial, however in the next section a dynamically allocated IP address is changed to a statically allocated address.</span></span> 

### <a name="change-allocation-method"></a><span data-ttu-id="ec5e7-155">Ayırma yöntemini değiştirme</span><span class="sxs-lookup"><span data-stu-id="ec5e7-155">Change allocation method</span></span>

<span data-ttu-id="ec5e7-156">IP adresi ayırma yöntemi kullanılarak değiştirilebilir [az ağ ortak IP güncelleştirmesi](/cli/azure/network/public-ip#update) komutu.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-156">The IP address allocation method can be changed using the [az network public-ip update](/cli/azure/network/public-ip#update) command.</span></span> <span data-ttu-id="ec5e7-157">Bu örnekte, ön uç sanal IP adresi ayırma yöntemi statik olarak değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-157">In this example, the IP address allocation method of the front-end VM is changed to static.</span></span>

<span data-ttu-id="ec5e7-158">İlk olarak, VM serbest bırakma.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-158">First, deallocate the VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

<span data-ttu-id="ec5e7-159">Kullanım [az ağ ortak IP güncelleştirmesi](/cli/azure/network/public-ip#update) ayırma yöntemi güncelleştirmek için komutu.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-159">Use the [az network public-ip update](/cli/azure/network/public-ip#update) command to update the allocation method.</span></span> <span data-ttu-id="ec5e7-160">Bu durumda, `--allocation-method` ayarlanmış *statik*.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-160">In this case, the `--allocation-method` is being set to *static*.</span></span>

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

<span data-ttu-id="ec5e7-161">VM Başlat.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-161">Start the VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a><span data-ttu-id="ec5e7-162">Ortak IP adresi yok</span><span class="sxs-lookup"><span data-stu-id="ec5e7-162">No public IP address</span></span>

<span data-ttu-id="ec5e7-163">Genellikle, bir VM Internet üzerinden erişilebilir olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-163">Often, a VM does not need to be accessible over the internet.</span></span> <span data-ttu-id="ec5e7-164">Bir ortak IP adresi olmadan bir VM oluşturmak için kullanmak `--public-ip-address ""` bağımsız değişkeni çift tırnak işareti boş dizi.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-164">To create a VM without a public IP address, use the `--public-ip-address ""` argument with an empty set of double quotes.</span></span> <span data-ttu-id="ec5e7-165">Bu yapılandırma Bu öğreticinin ilerleyen bölümlerinde gösterilmektedir</span><span class="sxs-lookup"><span data-stu-id="ec5e7-165">This configuration is demonstrated later in this tutorial</span></span>

## <a name="secure-network-traffic"></a><span data-ttu-id="ec5e7-166">Ağ trafiğinin güvenliğini sağlayın</span><span class="sxs-lookup"><span data-stu-id="ec5e7-166">Secure network traffic</span></span>

<span data-ttu-id="ec5e7-167">Ağ güvenlik grubu (NSG), Azure Sanal Ağlara (VNet) bağlı kaynaklara ağ trafiğine izin veren veya reddeden güvenlik kurallarının listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-167">A network security group (NSG) contains a list of security rules that allow or deny network traffic to resources connected to Azure Virtual Networks (VNet).</span></span> <span data-ttu-id="ec5e7-168">Nsg'ler alt ağları veya tek tek ağ arabirimleri için ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-168">NSGs can be associated to subnets or individual network interfaces.</span></span> <span data-ttu-id="ec5e7-169">Bir NSG'yi bir ağ arabirimi ile ilişkili olduğunda, yalnızca ilişkili VM geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-169">When an NSG is associated with a network interface, it applies only the associated VM.</span></span> <span data-ttu-id="ec5e7-170">Bir NSG bir alt ağ ile ilişkilendirildiğinde kurallar alt ağa bağlı tüm kaynaklar için geçerli olur.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-170">When an NSG is associated to a subnet, the rules apply to all resources connected to the subnet.</span></span> 

### <a name="network-security-group-rules"></a><span data-ttu-id="ec5e7-171">Ağ güvenlik grubu kuralları</span><span class="sxs-lookup"><span data-stu-id="ec5e7-171">Network security group rules</span></span>

<span data-ttu-id="ec5e7-172">NSG kuralları üzerinden trafik izin verilen veya reddedilen ağ bağlantı noktalarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-172">NSG rules define networking ports over which traffic is allowed or denied.</span></span> <span data-ttu-id="ec5e7-173">Böylece belirli sistemleri veya alt ağlar arasında trafiği denetlenir kuralları kaynak ve hedef IP adresi aralıklarını içerebilir.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-173">The rules can include source and destination IP address ranges so that traffic is controlled between specific systems or subnets.</span></span> <span data-ttu-id="ec5e7-174">NSG kuralları da dahil bir öncelik (1 arasında — ve 4096).</span><span class="sxs-lookup"><span data-stu-id="ec5e7-174">NSG rules also include a priority (between 1—and 4096).</span></span> <span data-ttu-id="ec5e7-175">Kurallar öncelik sırasına göre değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-175">Rules are evaluated in the order of priority.</span></span> <span data-ttu-id="ec5e7-176">100 önceliğine sahip bir kural 200 önceliğine sahip bir kural önce değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-176">A rule with a priority of 100 is evaluated before a rule with priority 200.</span></span>

<span data-ttu-id="ec5e7-177">Tüm NSG'ler bir varsayılan kurallar kümesini içerir.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-177">All NSGs contain a set of default rules.</span></span> <span data-ttu-id="ec5e7-178">Varsayılan kurallar silinemez ancak en düşük önceliğe atanmış oldukları için sizin oluşturduğunuz kurallar tarafından geçersiz kılınabilirler.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-178">The default rules cannot be deleted, but because they are assigned the lowest priority, they can be overridden by the rules that you create.</span></span>

- <span data-ttu-id="ec5e7-179">**Sanal ağ** - kaynaklanan trafiği ve sanal ağ içinde bitiş hem gelen ve giden yönlerde izin verilir.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-179">**Virtual network** - Traffic originating and ending in a virtual network is allowed both in inbound and outbound directions.</span></span>
- <span data-ttu-id="ec5e7-180">**Internet** - giden trafiğe izin verilir, ancak gelen trafik engellenir.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-180">**Internet** - Outbound traffic is allowed, but inbound traffic is blocked.</span></span>
- <span data-ttu-id="ec5e7-181">**Yük Dengeleyici** -VM'ler ve rol örneklerinin durumunu araştırma için izin Azure'nın yük dengeleyici.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-181">**Load balancer** - Allow Azure’s load balancer to probe the health of your VMs and role instances.</span></span> <span data-ttu-id="ec5e7-182">Yük dengelenmiş bir küme kullanmıyorsanız bu kuralı geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-182">If you are not using a load balanced set, you can override this rule.</span></span>

### <a name="create-network-security-groups"></a><span data-ttu-id="ec5e7-183">Ağ güvenlik grupları oluşturma</span><span class="sxs-lookup"><span data-stu-id="ec5e7-183">Create network security groups</span></span>

<span data-ttu-id="ec5e7-184">Kullanarak bir VM olarak aynı zamanda bir ağ güvenlik grubu oluşturulabilir [az vm oluşturma](/cli/azure/vm#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-184">A network security group can be created at the same time as a VM using the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="ec5e7-185">Bunun yapılması, NSG VM'ler ağ arabirimiyle ilişkilendirilmiş ve bir NSG kuralı otomatik olarak bağlantı noktası üzerinde trafiğe izin vermek için oluşturulan *22* herhangi bir kaynaktan.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-185">When doing so, the NSG is associated with the VMs network interface and an NSG rule is auto created to allow traffic on port *22* from any source.</span></span> <span data-ttu-id="ec5e7-186">Bu öğreticide daha önce ön uç VM ile otomatik olarak oluşturulan ön uç NSG.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-186">Earlier in this tutorial, the front-end NSG was auto-created with the front-end VM.</span></span> <span data-ttu-id="ec5e7-187">Bir NSG kuralı da otomatik olarak oluşturulan için bağlantı noktası 22 oluştu.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-187">An NSG rule was also auto created for port 22.</span></span> 

<span data-ttu-id="ec5e7-188">Bazı durumlarda, ne zaman varsayılan SSH kuralları oluşturulmaması gerektiğini veya ne zaman NSG bir alt ağa bağlı olması gibi bir NSG önceden oluşturmak yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-188">In some cases, it may be helpful to pre-create an NSG, such as when default SSH rules should not be created, or when the NSG should be attached to a subnet.</span></span> 

<span data-ttu-id="ec5e7-189">Kullanım [az ağ nsg oluşturma](/cli/azure/network/nsg#create) bir ağ güvenlik grubu oluşturmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-189">Use the [az network nsg create](/cli/azure/network/nsg#create) command to create a network security group.</span></span>

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

<span data-ttu-id="ec5e7-190">Bir ağ arabirimi NSG'yi ilişkilendirme yerine bir alt ağ ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-190">Instead of associating the NSG to a network interface, it is associated with a subnet.</span></span> <span data-ttu-id="ec5e7-191">Bu yapılandırmada alt ağına bağlı olduğu VM NSG kuralları devralır.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-191">In this configuration, any VM that is attached to the subnet inherits the NSG rules.</span></span>

<span data-ttu-id="ec5e7-192">Adlı mevcut alt güncelleştirme *mySubnetBackEnd* yeni NSG ile.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-192">Update the existing subnet named *mySubnetBackEnd* with the new NSG.</span></span>

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

<span data-ttu-id="ec5e7-193">Şimdi eklendiği bir sanal makine, oluşturmak *mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-193">Now create a virtual machine, which is attached to the *mySubnetBackEnd*.</span></span> <span data-ttu-id="ec5e7-194">Dikkat `--nsg` bağımsız değişkeni boş çift tırnak işareti değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-194">Notice that the `--nsg` argument has a value of empty double quotes.</span></span> <span data-ttu-id="ec5e7-195">Bir NSG'yi VM ile oluşturulmuş gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-195">An NSG does not need to be created with the VM.</span></span> <span data-ttu-id="ec5e7-196">VM ile önceden oluşturulmuş arka uç NSG korumalı arka uç alt ağına bağlı.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-196">The VM is attached to the back-end subnet, which is protected with the pre-created back-end NSG.</span></span> <span data-ttu-id="ec5e7-197">Bu NSG VM için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-197">This NSG applies to the VM.</span></span> <span data-ttu-id="ec5e7-198">Ayrıca, burada dikkat `--public-ip-address` bağımsız değişkeni boş çift tırnak işareti değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-198">Also, notice here that the `--public-ip-address` argument has a value of empty double quotes.</span></span> <span data-ttu-id="ec5e7-199">Bu yapılandırma, bir ortak IP adresi olmadan bir VM oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-199">This configuration creates a VM without a public IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a><span data-ttu-id="ec5e7-200">Gelen trafiği güvenli</span><span class="sxs-lookup"><span data-stu-id="ec5e7-200">Secure incoming traffic</span></span>

<span data-ttu-id="ec5e7-201">Ön uç VM oluşturulduğunda, bir NSG kuralı bağlantı noktası 22 gelen trafiğe izin verecek şekilde oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-201">When the front-end VM was created, an NSG rule was created to allow incoming traffic on port 22.</span></span> <span data-ttu-id="ec5e7-202">Bu kural, VM SSH bağlantılara izin verir.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-202">This rule allows SSH connections to the VM.</span></span> <span data-ttu-id="ec5e7-203">Bu örnekte, trafiğin de bağlantı noktası izin verilmesi gerektiğini *80*.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-203">For this example, traffic should also be allowed on port *80*.</span></span> <span data-ttu-id="ec5e7-204">Bu yapılandırma VM erişilecek bir web uygulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-204">This configuration allows a web application to be accessed on the VM.</span></span>

<span data-ttu-id="ec5e7-205">Kullanım [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create) bağlantı noktası için bir kural oluşturmak için komutu *80*.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-205">Use the [az network nsg rule create](/cli/azure/network/nsg/rule#create) command to create a rule for port *80*.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

<span data-ttu-id="ec5e7-206">Ön uç VM artık yalnızca bağlantı noktası üzerinde erişilebilir *22* ve bağlantı noktası *80*.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-206">The front-end VM is now only accessible on port *22* and port *80*.</span></span> <span data-ttu-id="ec5e7-207">Diğer tüm gelen trafiği ağ güvenlik grubu engellendi.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-207">All other incoming traffic is blocked at the network security group.</span></span> <span data-ttu-id="ec5e7-208">NSG kuralı yapılandırmaları görselleştirmek yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-208">It may be helpful to visualize the NSG rule configurations.</span></span> <span data-ttu-id="ec5e7-209">NSG kuralının yapılandırmayla dönmek [az ağ kuralı listesi](/cli/azure/network/nsg/rule#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-209">Return the NSG rule configuration with the [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

<span data-ttu-id="ec5e7-210">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="ec5e7-210">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-to-vm-traffic"></a><span data-ttu-id="ec5e7-211">VM VM trafiğinin güvenliğini</span><span class="sxs-lookup"><span data-stu-id="ec5e7-211">Secure VM to VM traffic</span></span>

<span data-ttu-id="ec5e7-212">Ağ güvenlik grubu kuralları da VM'ler arasında uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-212">Network security group rules can also apply between VMs.</span></span> <span data-ttu-id="ec5e7-213">Bu örnekte, ön uç VM arka uç VM bağlantı noktası ile iletişim kurması gereken *22* ve *3306*.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-213">For this example, the front-end VM needs to communicate with the back-end VM on port *22* and *3306*.</span></span> <span data-ttu-id="ec5e7-214">Bu yapılandırma, ön uç sanal makineden SSH bağlantılarına izin veren ve bir uygulama bir arka uç MySQL veritabanı ile iletişim kurmak için ön uç VM'de de olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-214">This configuration allows SSH connections from the front-end VM, and also allow an application on the front-end VM to communicate with a back-end MySQL database.</span></span> <span data-ttu-id="ec5e7-215">Diğer tüm trafik ön uç ve arka uç sanal makineler arasında engellenmelidir.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-215">All other traffic should be blocked between the front-end and back-end virtual machines.</span></span>

<span data-ttu-id="ec5e7-216">Kullanım [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create) bağlantı noktası 22 için bir kural oluşturmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-216">Use the [az network nsg rule create](/cli/azure/network/nsg/rule#create) command to create a rule for port 22.</span></span> <span data-ttu-id="ec5e7-217">Dikkat `--source-address-prefix` bağımsız değişken değerini belirtir *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-217">Notice that the `--source-address-prefix` argument specifies a value of *10.0.1.0/24*.</span></span> <span data-ttu-id="ec5e7-218">Bu yapılandırma, NSG yalnızca ön uç alt ağından gelen trafiğe izin verildiğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-218">This configuration ensures that only traffic from the front-end subnet is allowed through the NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

<span data-ttu-id="ec5e7-219">Şimdi 3306 noktasından MySQL trafiği için bir kural ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-219">Now add a rule for MySQL traffic on port 3306.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

<span data-ttu-id="ec5e7-220">Son olarak, aynı sanal ağ içindeki VM'ler arasında tüm trafiğe izin veren bir varsayılan kuralı Nsg'ler sahip olduğundan, bir kural tüm trafiği engellemek arka uç Nsg'ler için oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-220">Finally, because NSGs have a default rule allowing all traffic between VMs in the same VNet, a rule can be created for the back-end NSGs to block all traffic.</span></span> <span data-ttu-id="ec5e7-221">Burada dikkat `--priority` değerini verilen *300*, hangi, NSG ve MySQL kuralları alt olduğu.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-221">Notice here that the `--priority` is given a value of *300*, which is lower that both the NSG and MySQL rules.</span></span> <span data-ttu-id="ec5e7-222">Bu yapılandırma, SSH ve MySQL trafiği NSG izin verilir sağlar.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-222">This configuration ensures that SSH and MySQL traffic is still allowed through the NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

<span data-ttu-id="ec5e7-223">Arka uç VM artık yalnızca bağlantı noktası üzerinde erişilebilir *22* ve bağlantı noktası *3306* ön uç alt ağından.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-223">The back-end VM is now only accessible on port *22* and port *3306* from the front-end subnet.</span></span> <span data-ttu-id="ec5e7-224">Diğer tüm gelen trafiği ağ güvenlik grubu engellendi.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-224">All other incoming traffic is blocked at the network security group.</span></span> <span data-ttu-id="ec5e7-225">NSG kuralı yapılandırmaları görselleştirmek yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-225">It may be helpful to visualize the NSG rule configurations.</span></span> <span data-ttu-id="ec5e7-226">NSG kuralının yapılandırmayla dönmek [az ağ kuralı listesi](/cli/azure/network/nsg/rule#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-226">Return the NSG rule configuration with the [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

<span data-ttu-id="ec5e7-227">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="ec5e7-227">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a><span data-ttu-id="ec5e7-228">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ec5e7-228">Next steps</span></span>

<span data-ttu-id="ec5e7-229">Bu öğreticide oluşturduğunuz ve Azure ağları sanal makinelerle ilgili olarak güvenli.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-229">In this tutorial, you created and secured Azure networks as related to virtual machines.</span></span> <span data-ttu-id="ec5e7-230">Size nasıl öğrenilen için:</span><span class="sxs-lookup"><span data-stu-id="ec5e7-230">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ec5e7-231">Sanal ağ dağıtma</span><span class="sxs-lookup"><span data-stu-id="ec5e7-231">Deploy a virtual network</span></span>
> * <span data-ttu-id="ec5e7-232">Bir alt ağ içinde bir sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="ec5e7-232">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="ec5e7-233">Sanal makineler için bir alt ağ ekleme</span><span class="sxs-lookup"><span data-stu-id="ec5e7-233">Attach virtual machines to a subnet</span></span>
> * <span data-ttu-id="ec5e7-234">Sanal makine ortak IP adreslerini yönetin</span><span class="sxs-lookup"><span data-stu-id="ec5e7-234">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="ec5e7-235">Gelen Internet trafiği güvenli</span><span class="sxs-lookup"><span data-stu-id="ec5e7-235">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="ec5e7-236">VM VM trafiğinin güvenliğini</span><span class="sxs-lookup"><span data-stu-id="ec5e7-236">Secure VM to VM traffic</span></span>

<span data-ttu-id="ec5e7-237">Azure Yedekleme'yi kullanarak sanal makinelerde verilerin güvenliğini sağlama hakkında bilgi edinmek için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-237">Advance to the next tutorial to learn about securing data on virtual machines using Azure backup.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="ec5e7-238">Azure'daki Linux sanal makineleri yedekleyin</span><span class="sxs-lookup"><span data-stu-id="ec5e7-238">Back up Linux virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
