---
title: "aaaAzure sanal ağlar ve Linux sanal makineleri | Microsoft Docs"
description: "Öğretici - Azure sanal ağlar ve Linux sanal makineleri hello Azure CLI ile yönetme"
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
ms.openlocfilehash: 57e6bd4de16f0e31d53dc67bf50dc5730d43712b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-hello-azure-cli"></a><span data-ttu-id="25489-103">Azure sanal ağlar ve Linux sanal makineleri hello Azure CLI ile yönetme</span><span class="sxs-lookup"><span data-stu-id="25489-103">Manage Azure Virtual Networks and Linux Virtual Machines with hello Azure CLI</span></span>

<span data-ttu-id="25489-104">Azure sanal makineler, iç ve dış ağ iletişimi için Azure ağ kullanın.</span><span class="sxs-lookup"><span data-stu-id="25489-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="25489-105">Bu öğreticide iki sanal makine dağıtma ve bu VM'ler için Azure ağı yapılandırma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="25489-105">This tutorial walks through deploying two virtual machines and configuring Azure networking for these VMs.</span></span> <span data-ttu-id="25489-106">bir uygulama hello öğreticide dağıtılmamış ancak bu öğreticide hello örnekler hello VM'ler bir veritabanı arka uç, web uygulamasıyla barındırıyorsanız varsayar.</span><span class="sxs-lookup"><span data-stu-id="25489-106">hello examples in this tutorial assume that hello VMs are hosting a web application with a database back-end, however an application is not deployed in hello tutorial.</span></span> <span data-ttu-id="25489-107">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="25489-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="25489-108">Sanal ağ dağıtma</span><span class="sxs-lookup"><span data-stu-id="25489-108">Deploy a virtual network</span></span>
> * <span data-ttu-id="25489-109">Bir alt ağ içinde bir sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="25489-109">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="25489-110">Sanal makineler tooa alt ağ ekleme</span><span class="sxs-lookup"><span data-stu-id="25489-110">Attach virtual machines tooa subnet</span></span>
> * <span data-ttu-id="25489-111">Sanal makine ortak IP adreslerini yönetin</span><span class="sxs-lookup"><span data-stu-id="25489-111">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="25489-112">Gelen Internet trafiği güvenli</span><span class="sxs-lookup"><span data-stu-id="25489-112">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="25489-113">VM tooVM trafiği güvenli</span><span class="sxs-lookup"><span data-stu-id="25489-113">Secure VM tooVM traffic</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="25489-114">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="25489-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="25489-115">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="25489-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="25489-116">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="25489-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="vm-networking-overview"></a><span data-ttu-id="25489-117">VM ağ genel bakış</span><span class="sxs-lookup"><span data-stu-id="25489-117">VM networking overview</span></span>

<span data-ttu-id="25489-118">Azure sanal ağları sanal makineler arasında güvenli ağ bağlantıları etkinleştirmek için Internet ve Azure SQL veritabanı gibi diğer Azure hizmetleriyle hello.</span><span class="sxs-lookup"><span data-stu-id="25489-118">Azure virtual networks enable secure network connections between virtual machines, hello internet, and other Azure services such as Azure SQL database.</span></span> <span data-ttu-id="25489-119">Sanal ağlar alt ağ olarak adlandırılan mantıksal parçalara bölünür.</span><span class="sxs-lookup"><span data-stu-id="25489-119">Virtual networks are broken down into logical segments called subnets.</span></span> <span data-ttu-id="25489-120">Alt ağlar kullanılır toocontrol ağ akışı ve güvenlik sınırı.</span><span class="sxs-lookup"><span data-stu-id="25489-120">Subnets are used toocontrol network flow, and as a security boundary.</span></span> <span data-ttu-id="25489-121">VM dağıtırken, genellikle ekli tooa alt ağ olan bir sanal ağ arabirimi içerir.</span><span class="sxs-lookup"><span data-stu-id="25489-121">When deploying a VM, it generally includes a virtual network interface, which is attached tooa subnet.</span></span>

## <a name="deploy-virtual-network"></a><span data-ttu-id="25489-122">Sanal ağ dağıtma</span><span class="sxs-lookup"><span data-stu-id="25489-122">Deploy virtual network</span></span>

<span data-ttu-id="25489-123">Bu öğreticide, tek bir sanal ağı iki alt ağ ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="25489-123">For this tutorial, a single virtual network is created with two subnets.</span></span> <span data-ttu-id="25489-124">Bir web uygulamasını barındırmak için bir ön uç alt ağı ve bir veritabanı sunucusunu barındırmak için bir arka uç alt ağ.</span><span class="sxs-lookup"><span data-stu-id="25489-124">A front-end subnet for hosting a web application, and a back-end subnet for hosting a database server.</span></span>

<span data-ttu-id="25489-125">Bir sanal ağ oluşturmadan önce bir kaynak grubuyla oluşturmanız [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="25489-125">Before you can create a virtual network, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="25489-126">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myRGNetwork* hello eastus konumda.</span><span class="sxs-lookup"><span data-stu-id="25489-126">hello following example creates a resource group named *myRGNetwork* in hello eastus location.</span></span>

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a><span data-ttu-id="25489-127">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="25489-127">Create virtual network</span></span>

<span data-ttu-id="25489-128">Bize hello [az ağ vnet oluşturma](/cli/azure/network/vnet#create) komutu toocreate bir sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="25489-128">Us hello [az network vnet create](/cli/azure/network/vnet#create) command toocreate a virtual network.</span></span> <span data-ttu-id="25489-129">Bu örnekte, adlandırılmış hello ağ *mvVnet* ve bir adres öneki belirtilen *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="25489-129">In this example, hello network is named *mvVnet* and is given an address prefix of *10.0.0.0/16*.</span></span> <span data-ttu-id="25489-130">Bir alt ağ da bir ad oluşturulur *mySubnetFrontEnd* ve bir önek *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="25489-130">A subnet is also created with a name of *mySubnetFrontEnd* and a prefix of *10.0.1.0/24*.</span></span> <span data-ttu-id="25489-131">Daha sonra Bu öğreticide bir ön uç VM bağlı toothis alt'dir.</span><span class="sxs-lookup"><span data-stu-id="25489-131">Later in this tutorial a front-end VM is connected toothis subnet.</span></span> 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a><span data-ttu-id="25489-132">Alt ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="25489-132">Create subnet</span></span>

<span data-ttu-id="25489-133">Yeni bir alt ağ hello kullanarak toohello sanal ağ eklenir [az ağ sanal alt oluşturmak](/cli/azure/network/vnet/subnet#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="25489-133">A new subnet is added toohello virtual network using hello [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command.</span></span> <span data-ttu-id="25489-134">Bu örnekte, hello alt adlı *mySubnetBackEnd* ve bir adres öneki belirtilen *10.0.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="25489-134">In this example, hello subnet is named *mySubnetBackEnd* and is given an address prefix of *10.0.2.0/24*.</span></span> <span data-ttu-id="25489-135">Bu alt ağ ile tüm arka uç hizmetlerini kullanılır.</span><span class="sxs-lookup"><span data-stu-id="25489-135">This subnet is used with all back-end services.</span></span>

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

<span data-ttu-id="25489-136">Bu noktada, ağ oluşturulduğundan ve iki alt ağ, ön uç Hizmetleri için bir tane ve arka uç hizmetlerini için başka bir içine bölümlenmiş.</span><span class="sxs-lookup"><span data-stu-id="25489-136">At this point, a network has been created and segmented into two subnets, one for front-end services, and another for back-end services.</span></span> <span data-ttu-id="25489-137">Merhaba sonraki bölümde, sanal makine oluşturulur ve toothese alt bağlı.</span><span class="sxs-lookup"><span data-stu-id="25489-137">In hello next section, virtual machines are created and connected toothese subnets.</span></span>

## <a name="understand-public-ip-address"></a><span data-ttu-id="25489-138">Genel IP adresi anlama</span><span class="sxs-lookup"><span data-stu-id="25489-138">Understand public IP address</span></span>

<span data-ttu-id="25489-139">Azure kaynaklarını toobe genel bir IP adresi üzerinde erişilebilir sağlayan Internet hello.</span><span class="sxs-lookup"><span data-stu-id="25489-139">A public IP address allows Azure resources toobe accessible on hello internet.</span></span> <span data-ttu-id="25489-140">Merhaba öğreticinin bu bölümünde, bir VM nasıl toowork ortak IP adresleri toodemonstrate oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="25489-140">In this section of hello tutorial, a VM is created toodemonstrate how toowork with public IP addresses.</span></span>

### <a name="allocation-method"></a><span data-ttu-id="25489-141">Ayırma yöntemi</span><span class="sxs-lookup"><span data-stu-id="25489-141">Allocation method</span></span>

<span data-ttu-id="25489-142">Bir ortak IP adresi dinamik veya statik olarak ayrılabilir.</span><span class="sxs-lookup"><span data-stu-id="25489-142">A public IP address can be allocated as either dynamic or static.</span></span> <span data-ttu-id="25489-143">Varsayılan olarak, dinamik olarak ayrılan ortak IP adresi.</span><span class="sxs-lookup"><span data-stu-id="25489-143">By default, public IP address dynamically allocated.</span></span> <span data-ttu-id="25489-144">Bir VM serbest bırakıldığında dinamik IP adresleri serbest bırakılır.</span><span class="sxs-lookup"><span data-stu-id="25489-144">Dynamic IP addresses are released when a VM is deallocated.</span></span> <span data-ttu-id="25489-145">Bu davranış, VM ayırmayı kaldırma içeren herhangi bir işlem sırasında hello IP adresi toochange neden olur.</span><span class="sxs-lookup"><span data-stu-id="25489-145">This behavior causes hello IP address toochange during any operation that includes a VM deallocation.</span></span>

<span data-ttu-id="25489-146">Merhaba ayırma yöntemi toostatic, ayarlanabilir tooa VM bile deallocated durumundayken atanan başlangıç IP adresi kalmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="25489-146">hello allocation method can be set toostatic, which ensures that hello IP address remain assigned tooa VM, even during a deallocated state.</span></span> <span data-ttu-id="25489-147">Statik olarak ayrılmış bir IP adresi kullanırken, başlangıç IP adresi kendisini belirtilemez.</span><span class="sxs-lookup"><span data-stu-id="25489-147">When using a statically allocated IP address, hello IP address itself cannot be specified.</span></span> <span data-ttu-id="25489-148">Bunun yerine, kullanılabilir adresler havuzundan tahsis edilir.</span><span class="sxs-lookup"><span data-stu-id="25489-148">Instead, it is allocated from a pool of available addresses.</span></span>

### <a name="dynamic-allocation"></a><span data-ttu-id="25489-149">Dinamik ayırma</span><span class="sxs-lookup"><span data-stu-id="25489-149">Dynamic allocation</span></span>

<span data-ttu-id="25489-150">Bir VM ile Merhaba oluşturulurken [az vm oluşturma](/cli/azure/vm#create) hello varsayılan genel IP adresi ayırma yöntemi dinamik komutu.</span><span class="sxs-lookup"><span data-stu-id="25489-150">When creating a VM with hello [az vm create](/cli/azure/vm#create) command, hello default public IP address allocation method is dynamic.</span></span> <span data-ttu-id="25489-151">Aşağıdaki örneğine hello VM dinamik bir IP adresi ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="25489-151">In hello following example, a VM is created with a dynamic IP address.</span></span> 

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

### <a name="static-allocation"></a><span data-ttu-id="25489-152">Statik ayırma</span><span class="sxs-lookup"><span data-stu-id="25489-152">Static allocation</span></span>

<span data-ttu-id="25489-153">Hello kullanarak bir sanal makine oluştururken [az vm oluşturma](/cli/azure/vm#create) hello içeriyor, komut `--public-ip-address-allocation static` bağımsız değişkeni tooassign bir statik genel IP adresi.</span><span class="sxs-lookup"><span data-stu-id="25489-153">When creating a virtual machine using hello [az vm create](/cli/azure/vm#create) command, include hello `--public-ip-address-allocation static` argument tooassign a static public IP address.</span></span> <span data-ttu-id="25489-154">Bu işlem değil gösterilmiştir Bu öğreticide, ancak hello sonraki bölümde dinamik olarak ayrılan bir IP adresi değiştirilen tooa statik adresi ayrılır.</span><span class="sxs-lookup"><span data-stu-id="25489-154">This operation is not demonstrated in this tutorial, however in hello next section a dynamically allocated IP address is changed tooa statically allocated address.</span></span> 

### <a name="change-allocation-method"></a><span data-ttu-id="25489-155">Ayırma yöntemini değiştirme</span><span class="sxs-lookup"><span data-stu-id="25489-155">Change allocation method</span></span>

<span data-ttu-id="25489-156">Başlangıç IP adresi ayırma yöntemi hello kullanılarak değiştirilebilir [az ağ ortak IP güncelleştirmesi](/cli/azure/network/public-ip#update) komutu.</span><span class="sxs-lookup"><span data-stu-id="25489-156">hello IP address allocation method can be changed using hello [az network public-ip update](/cli/azure/network/public-ip#update) command.</span></span> <span data-ttu-id="25489-157">Bu örnekte, IP adresi ayırma yöntemini ön uç VM değiştirildiğinde hello hello toostatic.</span><span class="sxs-lookup"><span data-stu-id="25489-157">In this example, hello IP address allocation method of hello front-end VM is changed toostatic.</span></span>

<span data-ttu-id="25489-158">İlk olarak, hello VM serbest bırakma.</span><span class="sxs-lookup"><span data-stu-id="25489-158">First, deallocate hello VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

<span data-ttu-id="25489-159">Kullanım hello [az ağ ortak IP güncelleştirmesi](/cli/azure/network/public-ip#update) tooupdate hello ayırma yöntemi komutu.</span><span class="sxs-lookup"><span data-stu-id="25489-159">Use hello [az network public-ip update](/cli/azure/network/public-ip#update) command tooupdate hello allocation method.</span></span> <span data-ttu-id="25489-160">Bu durumda, hello `--allocation-method` çok ayarlı*statik*.</span><span class="sxs-lookup"><span data-stu-id="25489-160">In this case, hello `--allocation-method` is being set too*static*.</span></span>

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

<span data-ttu-id="25489-161">Merhaba VM başlatın.</span><span class="sxs-lookup"><span data-stu-id="25489-161">Start hello VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a><span data-ttu-id="25489-162">Ortak IP adresi yok</span><span class="sxs-lookup"><span data-stu-id="25489-162">No public IP address</span></span>

<span data-ttu-id="25489-163">Genellikle, bir VM toobe üzerinden erişilebilir gerekmez Internet hello.</span><span class="sxs-lookup"><span data-stu-id="25489-163">Often, a VM does not need toobe accessible over hello internet.</span></span> <span data-ttu-id="25489-164">toocreate genel bir IP adresi kullanım hello olmadan bir VM `--public-ip-address ""` bağımsız değişkeni çift tırnak işareti boş dizi.</span><span class="sxs-lookup"><span data-stu-id="25489-164">toocreate a VM without a public IP address, use hello `--public-ip-address ""` argument with an empty set of double quotes.</span></span> <span data-ttu-id="25489-165">Bu yapılandırma Bu öğreticinin ilerleyen bölümlerinde gösterilmektedir</span><span class="sxs-lookup"><span data-stu-id="25489-165">This configuration is demonstrated later in this tutorial</span></span>

## <a name="secure-network-traffic"></a><span data-ttu-id="25489-166">Ağ trafiğinin güvenliğini sağlayın</span><span class="sxs-lookup"><span data-stu-id="25489-166">Secure network traffic</span></span>

<span data-ttu-id="25489-167">Bir ağ güvenlik grubu (NSG) izin veren veya reddeden ağ trafiği tooresources tooAzure sanal ağ (VNet) bağlı güvenlik kurallarının bir listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="25489-167">A network security group (NSG) contains a list of security rules that allow or deny network traffic tooresources connected tooAzure Virtual Networks (VNet).</span></span> <span data-ttu-id="25489-168">Nsg'ler ilişkili toosubnets veya tek tek ağ arabirimleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="25489-168">NSGs can be associated toosubnets or individual network interfaces.</span></span> <span data-ttu-id="25489-169">Bir NSG'yi bir ağ arabirimi ile ilişkili olduğunda, yalnızca VM hello ilişkilendirilen geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="25489-169">When an NSG is associated with a network interface, it applies only hello associated VM.</span></span> <span data-ttu-id="25489-170">Bir NSG'yi ilişkili tooa alt olduğunda hello kuralları tooall kaynaklara bağlı toohello alt uygulayın.</span><span class="sxs-lookup"><span data-stu-id="25489-170">When an NSG is associated tooa subnet, hello rules apply tooall resources connected toohello subnet.</span></span> 

### <a name="network-security-group-rules"></a><span data-ttu-id="25489-171">Ağ güvenlik grubu kuralları</span><span class="sxs-lookup"><span data-stu-id="25489-171">Network security group rules</span></span>

<span data-ttu-id="25489-172">NSG kuralları üzerinden trafik izin verilen veya reddedilen ağ bağlantı noktalarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="25489-172">NSG rules define networking ports over which traffic is allowed or denied.</span></span> <span data-ttu-id="25489-173">böylece belirli sistemleri veya alt ağlar arasında trafiği denetlenir hello kuralları kaynak ve hedef IP adresi aralıklarını içerebilir.</span><span class="sxs-lookup"><span data-stu-id="25489-173">hello rules can include source and destination IP address ranges so that traffic is controlled between specific systems or subnets.</span></span> <span data-ttu-id="25489-174">NSG kuralları da dahil bir öncelik (1 arasında — ve 4096).</span><span class="sxs-lookup"><span data-stu-id="25489-174">NSG rules also include a priority (between 1—and 4096).</span></span> <span data-ttu-id="25489-175">Kuralları hello öncelik sırasına göre değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="25489-175">Rules are evaluated in hello order of priority.</span></span> <span data-ttu-id="25489-176">100 önceliğine sahip bir kural 200 önceliğine sahip bir kural önce değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="25489-176">A rule with a priority of 100 is evaluated before a rule with priority 200.</span></span>

<span data-ttu-id="25489-177">Tüm NSG'ler bir varsayılan kurallar kümesini içerir.</span><span class="sxs-lookup"><span data-stu-id="25489-177">All NSGs contain a set of default rules.</span></span> <span data-ttu-id="25489-178">Merhaba varsayılan kurallar silinemez ancak hello en düşük öncelik atandığı için oluşturduğunuz hello kurallarıyla kılınabilir.</span><span class="sxs-lookup"><span data-stu-id="25489-178">hello default rules cannot be deleted, but because they are assigned hello lowest priority, they can be overridden by hello rules that you create.</span></span>

- <span data-ttu-id="25489-179">**Sanal ağ** - kaynaklanan trafiği ve sanal ağ içinde bitiş hem gelen ve giden yönlerde izin verilir.</span><span class="sxs-lookup"><span data-stu-id="25489-179">**Virtual network** - Traffic originating and ending in a virtual network is allowed both in inbound and outbound directions.</span></span>
- <span data-ttu-id="25489-180">**Internet** - giden trafiğe izin verilir, ancak gelen trafik engellenir.</span><span class="sxs-lookup"><span data-stu-id="25489-180">**Internet** - Outbound traffic is allowed, but inbound traffic is blocked.</span></span>
- <span data-ttu-id="25489-181">**Yük Dengeleyici** -izin Azure'nın yük dengeleyici tooprobe hello durumunu VM'ler ve rol örnekleri.</span><span class="sxs-lookup"><span data-stu-id="25489-181">**Load balancer** - Allow Azure’s load balancer tooprobe hello health of your VMs and role instances.</span></span> <span data-ttu-id="25489-182">Yük dengelenmiş bir küme kullanmıyorsanız bu kuralı geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="25489-182">If you are not using a load balanced set, you can override this rule.</span></span>

### <a name="create-network-security-groups"></a><span data-ttu-id="25489-183">Ağ güvenlik grupları oluşturma</span><span class="sxs-lookup"><span data-stu-id="25489-183">Create network security groups</span></span>

<span data-ttu-id="25489-184">Merhaba aynı ağ güvenlik grubu oluşturulan hello kullanarak bir VM olarak zaman [az vm oluşturma](/cli/azure/vm#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="25489-184">A network security group can be created at hello same time as a VM using hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="25489-185">Bunu yaparken hello NSG hello VM'ler ağ arabirimiyle ilişkilendirilmiş ve bir NSG kuralı bağlantı noktası otomatik olarak oluşturulan tooallow trafiğine *22* herhangi bir kaynaktan.</span><span class="sxs-lookup"><span data-stu-id="25489-185">When doing so, hello NSG is associated with hello VMs network interface and an NSG rule is auto created tooallow traffic on port *22* from any source.</span></span> <span data-ttu-id="25489-186">Bu öğreticide daha önce ön uç VM ile otomatik olarak oluşturulan ön uç NSG hello hello.</span><span class="sxs-lookup"><span data-stu-id="25489-186">Earlier in this tutorial, hello front-end NSG was auto-created with hello front-end VM.</span></span> <span data-ttu-id="25489-187">Bir NSG kuralı da otomatik olarak oluşturulan için bağlantı noktası 22 oluştu.</span><span class="sxs-lookup"><span data-stu-id="25489-187">An NSG rule was also auto created for port 22.</span></span> 

<span data-ttu-id="25489-188">Bazı durumlarda yararlı toopre olabilir-zaman varsayılan SSH kuralları oluşturulmaması gerektiğini veya hello NSG ekli tooa alt zaman olmalıdır gibi bir NSG oluşturun.</span><span class="sxs-lookup"><span data-stu-id="25489-188">In some cases, it may be helpful toopre-create an NSG, such as when default SSH rules should not be created, or when hello NSG should be attached tooa subnet.</span></span> 

<span data-ttu-id="25489-189">Kullanım hello [az ağ nsg oluşturma](/cli/azure/network/nsg#create) komutu toocreate bir ağ güvenlik grubu.</span><span class="sxs-lookup"><span data-stu-id="25489-189">Use hello [az network nsg create](/cli/azure/network/nsg#create) command toocreate a network security group.</span></span>

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

<span data-ttu-id="25489-190">Merhaba NSG tooa ağ arabirimi ilişkilendirme yerine bir alt ağ ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="25489-190">Instead of associating hello NSG tooa network interface, it is associated with a subnet.</span></span> <span data-ttu-id="25489-191">Bu yapılandırmada, ekli toohello alt VM hello NSG kuralları devralır.</span><span class="sxs-lookup"><span data-stu-id="25489-191">In this configuration, any VM that is attached toohello subnet inherits hello NSG rules.</span></span>

<span data-ttu-id="25489-192">Merhaba mevcut alt adlı güncelleştirme *mySubnetBackEnd* ile yeni NSG hello.</span><span class="sxs-lookup"><span data-stu-id="25489-192">Update hello existing subnet named *mySubnetBackEnd* with hello new NSG.</span></span>

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

<span data-ttu-id="25489-193">Ekli toohello olan bir sanal makine, şimdi oluşturmak *mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="25489-193">Now create a virtual machine, which is attached toohello *mySubnetBackEnd*.</span></span> <span data-ttu-id="25489-194">Bu hello fark `--nsg` bağımsız değişkeni boş çift tırnak işareti değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="25489-194">Notice that hello `--nsg` argument has a value of empty double quotes.</span></span> <span data-ttu-id="25489-195">Bir NSG'yi hello VM ile oluşturulan toobe gerekmez.</span><span class="sxs-lookup"><span data-stu-id="25489-195">An NSG does not need toobe created with hello VM.</span></span> <span data-ttu-id="25489-196">Merhaba VM ile arka uç NSG önceden oluşturulmuş hello korumalı ekli toohello arka uç alt ağıdır.</span><span class="sxs-lookup"><span data-stu-id="25489-196">hello VM is attached toohello back-end subnet, which is protected with hello pre-created back-end NSG.</span></span> <span data-ttu-id="25489-197">Bu NSG toohello VM geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="25489-197">This NSG applies toohello VM.</span></span> <span data-ttu-id="25489-198">Ayrıca, bu hello burada fark `--public-ip-address` bağımsız değişkeni boş çift tırnak işareti değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="25489-198">Also, notice here that hello `--public-ip-address` argument has a value of empty double quotes.</span></span> <span data-ttu-id="25489-199">Bu yapılandırma, bir ortak IP adresi olmadan bir VM oluşturur.</span><span class="sxs-lookup"><span data-stu-id="25489-199">This configuration creates a VM without a public IP address.</span></span> 

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

### <a name="secure-incoming-traffic"></a><span data-ttu-id="25489-200">Gelen trafiği güvenli</span><span class="sxs-lookup"><span data-stu-id="25489-200">Secure incoming traffic</span></span>

<span data-ttu-id="25489-201">Merhaba ön uç VM oluşturulduğunda, bir NSG kuralı bağlantı noktası 22 tooallow gelen trafiği oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="25489-201">When hello front-end VM was created, an NSG rule was created tooallow incoming traffic on port 22.</span></span> <span data-ttu-id="25489-202">Bu kural, SSH bağlantıları toohello VM sağlar.</span><span class="sxs-lookup"><span data-stu-id="25489-202">This rule allows SSH connections toohello VM.</span></span> <span data-ttu-id="25489-203">Bu örnekte, trafiğin de bağlantı noktası izin verilmesi gerektiğini *80*.</span><span class="sxs-lookup"><span data-stu-id="25489-203">For this example, traffic should also be allowed on port *80*.</span></span> <span data-ttu-id="25489-204">Bu yapılandırma VM hello üzerinde erişilen web uygulama toobe sağlar.</span><span class="sxs-lookup"><span data-stu-id="25489-204">This configuration allows a web application toobe accessed on hello VM.</span></span>

<span data-ttu-id="25489-205">Kullanım hello [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create) komutu toocreate bağlantı noktası için bir kural *80*.</span><span class="sxs-lookup"><span data-stu-id="25489-205">Use hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command toocreate a rule for port *80*.</span></span>

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

<span data-ttu-id="25489-206">Merhaba ön uç VM artık yalnızca bağlantı noktası üzerinde erişilebilir *22* ve bağlantı noktası *80*.</span><span class="sxs-lookup"><span data-stu-id="25489-206">hello front-end VM is now only accessible on port *22* and port *80*.</span></span> <span data-ttu-id="25489-207">Diğer tüm gelen trafiği hello ağ güvenlik grubu engellendi.</span><span class="sxs-lookup"><span data-stu-id="25489-207">All other incoming traffic is blocked at hello network security group.</span></span> <span data-ttu-id="25489-208">Yararlı toovisualize hello NSG kuralı yapılandırmaları olabilir.</span><span class="sxs-lookup"><span data-stu-id="25489-208">It may be helpful toovisualize hello NSG rule configurations.</span></span> <span data-ttu-id="25489-209">Dönüş hello NSG kural hello yapılandırmayla [az ağ kuralı listesi](/cli/azure/network/nsg/rule#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="25489-209">Return hello NSG rule configuration with hello [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

<span data-ttu-id="25489-210">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="25489-210">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-toovm-traffic"></a><span data-ttu-id="25489-211">VM tooVM trafiği güvenli</span><span class="sxs-lookup"><span data-stu-id="25489-211">Secure VM tooVM traffic</span></span>

<span data-ttu-id="25489-212">Ağ güvenlik grubu kuralları da VM'ler arasında uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="25489-212">Network security group rules can also apply between VMs.</span></span> <span data-ttu-id="25489-213">Bu örnekte, ön uç VM ile toocommunicate gereken hello hello arka uç VM bağlantı noktasında *22* ve *3306*.</span><span class="sxs-lookup"><span data-stu-id="25489-213">For this example, hello front-end VM needs toocommunicate with hello back-end VM on port *22* and *3306*.</span></span> <span data-ttu-id="25489-214">Bu yapılandırma SSH bağlantılara izin ön uç VM hello ve ayrıca hello ön uç VM toocommunicate arka uç MySQL veritabanına sahip bir uygulama ver.</span><span class="sxs-lookup"><span data-stu-id="25489-214">This configuration allows SSH connections from hello front-end VM, and also allow an application on hello front-end VM toocommunicate with a back-end MySQL database.</span></span> <span data-ttu-id="25489-215">Diğer tüm trafik hello ön uç ve arka uç sanal makineler arasında engellenmelidir.</span><span class="sxs-lookup"><span data-stu-id="25489-215">All other traffic should be blocked between hello front-end and back-end virtual machines.</span></span>

<span data-ttu-id="25489-216">Kullanım hello [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create) komutu toocreate bağlantı noktası 22 için bir kural.</span><span class="sxs-lookup"><span data-stu-id="25489-216">Use hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command toocreate a rule for port 22.</span></span> <span data-ttu-id="25489-217">Bu hello fark `--source-address-prefix` bağımsız değişken değerini belirtir *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="25489-217">Notice that hello `--source-address-prefix` argument specifies a value of *10.0.1.0/24*.</span></span> <span data-ttu-id="25489-218">Bu yapılandırma, yalnızca hello ön uç alt ağından gelen trafiği NSG hello izin verildiğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="25489-218">This configuration ensures that only traffic from hello front-end subnet is allowed through hello NSG.</span></span>

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

<span data-ttu-id="25489-219">Şimdi 3306 noktasından MySQL trafiği için bir kural ekleyin.</span><span class="sxs-lookup"><span data-stu-id="25489-219">Now add a rule for MySQL traffic on port 3306.</span></span>

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

<span data-ttu-id="25489-220">Nsg'ler bir varsayılan kural izin verme olduğundan son olarak, tüm hello VM'ler arasında aynı trafiği sanal ağ, bir kural oluşturulabilir hello arka uç Nsg'ler tooblock için tüm trafiği.</span><span class="sxs-lookup"><span data-stu-id="25489-220">Finally, because NSGs have a default rule allowing all traffic between VMs in hello same VNet, a rule can be created for hello back-end NSGs tooblock all traffic.</span></span> <span data-ttu-id="25489-221">Burada bu hello fark `--priority` değerini verilen *300*, her ikisi de NSG ve MySQL kuralları hello daha düşük olduğu.</span><span class="sxs-lookup"><span data-stu-id="25489-221">Notice here that hello `--priority` is given a value of *300*, which is lower that both hello NSG and MySQL rules.</span></span> <span data-ttu-id="25489-222">Bu yapılandırma, SSH ve MySQL trafiği NSG hello izin verilir sağlar.</span><span class="sxs-lookup"><span data-stu-id="25489-222">This configuration ensures that SSH and MySQL traffic is still allowed through hello NSG.</span></span>

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

<span data-ttu-id="25489-223">Merhaba arka uç VM artık yalnızca bağlantı noktası üzerinde erişilebilir *22* ve bağlantı noktası *3306* hello ön uç alt ağından.</span><span class="sxs-lookup"><span data-stu-id="25489-223">hello back-end VM is now only accessible on port *22* and port *3306* from hello front-end subnet.</span></span> <span data-ttu-id="25489-224">Diğer tüm gelen trafiği hello ağ güvenlik grubu engellendi.</span><span class="sxs-lookup"><span data-stu-id="25489-224">All other incoming traffic is blocked at hello network security group.</span></span> <span data-ttu-id="25489-225">Yararlı toovisualize hello NSG kuralı yapılandırmaları olabilir.</span><span class="sxs-lookup"><span data-stu-id="25489-225">It may be helpful toovisualize hello NSG rule configurations.</span></span> <span data-ttu-id="25489-226">Dönüş hello NSG kural hello yapılandırmayla [az ağ kuralı listesi](/cli/azure/network/nsg/rule#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="25489-226">Return hello NSG rule configuration with hello [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

<span data-ttu-id="25489-227">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="25489-227">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a><span data-ttu-id="25489-228">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="25489-228">Next steps</span></span>

<span data-ttu-id="25489-229">Bu öğreticide oluşturduğunuz ve Azure ağları ilgili toovirtual makineler olarak güvenli.</span><span class="sxs-lookup"><span data-stu-id="25489-229">In this tutorial, you created and secured Azure networks as related toovirtual machines.</span></span> <span data-ttu-id="25489-230">Şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="25489-230">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="25489-231">Sanal ağ dağıtma</span><span class="sxs-lookup"><span data-stu-id="25489-231">Deploy a virtual network</span></span>
> * <span data-ttu-id="25489-232">Bir alt ağ içinde bir sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="25489-232">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="25489-233">Sanal makineler tooa alt ağ ekleme</span><span class="sxs-lookup"><span data-stu-id="25489-233">Attach virtual machines tooa subnet</span></span>
> * <span data-ttu-id="25489-234">Sanal makine ortak IP adreslerini yönetin</span><span class="sxs-lookup"><span data-stu-id="25489-234">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="25489-235">Gelen Internet trafiği güvenli</span><span class="sxs-lookup"><span data-stu-id="25489-235">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="25489-236">VM tooVM trafiği güvenli</span><span class="sxs-lookup"><span data-stu-id="25489-236">Secure VM tooVM traffic</span></span>

<span data-ttu-id="25489-237">Azure Yedekleme'yi kullanarak sanal makinelerde verilerin güvenliğini sağlama hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="25489-237">Advance toohello next tutorial toolearn about securing data on virtual machines using Azure backup.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="25489-238">Azure'daki Linux sanal makineleri yedekleyin</span><span class="sxs-lookup"><span data-stu-id="25489-238">Back up Linux virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
