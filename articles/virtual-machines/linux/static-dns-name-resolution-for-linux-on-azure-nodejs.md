---
title: "Azure VM ad çözümlemesi için iç DNS kullanarak | Microsoft Docs"
description: "Azure VM ad çözümlemesi için iç DNS kullanarak."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: bfba2cf38a0624e8480a32bf153f391d820da5a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="942c8-103">Azure VM ad çözümlemesi için iç DNS kullanma</span><span class="sxs-lookup"><span data-stu-id="942c8-103">Using internal DNS for VM name resolution on Azure</span></span>

<span data-ttu-id="942c8-104">Bu makalede, sanal NIC kartları (Vnıc) ve DNS etiket adları kullanarak Linux VM'ler için statik iç DNS adlarını ayarlamak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="942c8-104">This article shows how to set static internal DNS names for Linux VMs using Virtual NIC cards (VNic) and DNS label names.</span></span> <span data-ttu-id="942c8-105">Statik DNS adları, bu belge için kullanılan bir Jenkins yapı sunucusu veya Git sunucusu gibi kalıcı altyapı hizmetleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="942c8-105">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="942c8-106">Gereksinimler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="942c8-106">The requirements are:</span></span>

* [<span data-ttu-id="942c8-107">Bir Azure hesabı</span><span class="sxs-lookup"><span data-stu-id="942c8-107">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="942c8-108">SSH ortak ve özel anahtar dosyaları</span><span class="sxs-lookup"><span data-stu-id="942c8-108">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="942c8-109">Görevi tamamlamak için kullanılacak CLI sürümleri</span><span class="sxs-lookup"><span data-stu-id="942c8-109">CLI versions to complete the task</span></span>
<span data-ttu-id="942c8-110">Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="942c8-110">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="942c8-111">[Azure CLI 1.0](#quick-commands) – bizim CLI Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="942c8-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="942c8-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): Kaynak yönetimi dağıtım modeline yönelik yeni nesil CLI'mız</span><span class="sxs-lookup"><span data-stu-id="942c8-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="942c8-113">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="942c8-113">Quick commands</span></span>

<span data-ttu-id="942c8-114">Hızlı bir şekilde görevi gerçekleştirmek gerekiyorsa, aşağıdaki bölümde gerekli komutları ayrıntıları verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="942c8-114">If you need to quickly accomplish the task, the following section details the commands needed.</span></span> <span data-ttu-id="942c8-115">Her adım, belgenin geri kalanında bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="942c8-115">More detailed information and context for each step can be found the rest of the document, [starting here](#detailed-walkthrough).</span></span>  

<span data-ttu-id="942c8-116">Ön gereksinimlerini: SSH ile kaynak grubu, VNet, NSG gelen, alt ağ.</span><span class="sxs-lookup"><span data-stu-id="942c8-116">Pre-Requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span>

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a><span data-ttu-id="942c8-117">Statik iç DNS adı ile bir Vnıc'teki oluşturma</span><span class="sxs-lookup"><span data-stu-id="942c8-117">Create a VNic with a static internal DNS name</span></span>

<span data-ttu-id="942c8-118">`-r` CLI bayrağı olduğundan statik Vnıc DNS adını sağlayan DNS etiketi ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="942c8-118">The `-r` cli flag is for setting the DNS label, which provides the static DNS name for the VNic.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-the-vm-into-the-vnet-nsg-and-connect-the-vnic"></a><span data-ttu-id="942c8-119">VNet, NSG VM dağıtmak ve Vnıc bağlanın</span><span class="sxs-lookup"><span data-stu-id="942c8-119">Deploy the VM into the VNet, NSG and, connect the VNic</span></span>

<span data-ttu-id="942c8-120">`-N` Vnıc Azure'a dağıtımı sırasında yeni VM bağlanır.</span><span class="sxs-lookup"><span data-stu-id="942c8-120">The `-N` connects the VNic to the new VM during the deployment to Azure.</span></span>

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="942c8-121">Ayrıntılı kılavuz</span><span class="sxs-lookup"><span data-stu-id="942c8-121">Detailed walkthrough</span></span>

<span data-ttu-id="942c8-122">Bir tam sürekli tümleştirme ve sürekli dağıtımı (CiCd) altyapısı Azure ile ilgili belirli sunucuların statik veya uzun süreli sunucusu olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="942c8-122">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers to be static or long-lived servers.</span></span>  <span data-ttu-id="942c8-123">Sanal ağlar (Vnet'ler) ve ağ güvenlik grupları (Nsg'ler) gibi Azure varlıklar statik olmalıdır ve nadiren dağıtılan kaynakları uzun ömürlü önerilir.</span><span class="sxs-lookup"><span data-stu-id="942c8-123">It is recommended that Azure assets like the Virtual Networks (VNets) and Network Security Groups (NSGs), should be static and long lived resources that are rarely deployed.</span></span>  <span data-ttu-id="942c8-124">Bir VNet dağıtıldıktan sonra hiçbir olumsuz etkiler altyapısı olmadan yeni dağıtımlar tarafından yeniden.</span><span class="sxs-lookup"><span data-stu-id="942c8-124">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span>  <span data-ttu-id="942c8-125">Bu statik ağa bir Git deposu sunucusu ve Jenkins Otomasyon sunucusu ekleme CiCd geliştirme veya test ortamınızı sunar.</span><span class="sxs-lookup"><span data-stu-id="942c8-125">Adding to this static network a Git repository server and a Jenkins automation server delivers CiCd to your development or test environments.</span></span>  

<span data-ttu-id="942c8-126">İç DNS adları, yalnızca bir Azure sanal ağı içinde çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="942c8-126">Internal DNS names are only resolvable inside an Azure virtual network.</span></span>  <span data-ttu-id="942c8-127">DNS adları iç olduğundan, bunlar altyapısına ek güvenlik sağlamaya dış internet çözülebilir değildir.</span><span class="sxs-lookup"><span data-stu-id="942c8-127">Because the DNS names are internal, they are not resolvable to the outside internet, providing additional security to the infrastructure.</span></span>

<span data-ttu-id="942c8-128">_Tüm örnekleri kendi adlandırma ile değiştirin._</span><span class="sxs-lookup"><span data-stu-id="942c8-128">_Replace any examples with your own naming._</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="942c8-129">Kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="942c8-129">Create the Resource group</span></span>

<span data-ttu-id="942c8-130">Bir kaynak grubu, bu kılavuzda oluşturuyoruz her şeyi düzenlemek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="942c8-130">A Resource Group is needed to organize everything we create in this walkthrough.</span></span>  <span data-ttu-id="942c8-131">Azure kaynak grupları hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="942c8-131">For more information on Azure Resource Groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-the-vnet"></a><span data-ttu-id="942c8-132">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="942c8-132">Create the VNet</span></span>

<span data-ttu-id="942c8-133">İlk adım, içine sanal makineleri başlatmak için bir VNet oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="942c8-133">The first step is to build a VNet to launch the VMs into.</span></span>  <span data-ttu-id="942c8-134">Sanal ağ Bu izlenecek yol için bir alt ağ içerir.</span><span class="sxs-lookup"><span data-stu-id="942c8-134">The VNet contains one subnet for this walkthrough.</span></span>  <span data-ttu-id="942c8-135">Azure sanal ağlar hakkında daha fazla bilgi için bkz: [Azure CLI kullanarak bir sanal ağ oluşturma](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="942c8-135">For more information on Azure VNets, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-the-nsg"></a><span data-ttu-id="942c8-136">NSG oluşturma</span><span class="sxs-lookup"><span data-stu-id="942c8-136">Create the NSG</span></span>

<span data-ttu-id="942c8-137">Biz NSG önce alt ağ oluşturmak için varolan bir ağ güvenlik grubu alt oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="942c8-137">The Subnet is built behind an existing Network Security Group so we build the NSG before the Subnet.</span></span>  <span data-ttu-id="942c8-138">Azure Nsg'ler bir Güvenlik Duvarı'nı ağ katmanında eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="942c8-138">Azure NSGs are equivalent to a firewall at the network layer.</span></span>  <span data-ttu-id="942c8-139">Azure Nsg'ler hakkında daha fazla bilgi için bkz: [Nsg'ler Azure CLI oluşturma](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="942c8-139">For more information on Azure NSGs, see [How to create NSGs in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="942c8-140">Gelen bir SSH izin ver Kuralı Ekle</span><span class="sxs-lookup"><span data-stu-id="942c8-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="942c8-141">Gelen bağlantı noktası 22 trafiği ağ üzerinden bağlantı noktası 22 Linux VM'de geçirilmesine izin veren bir kural gerektiği şekilde Linux VM internet erişimi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="942c8-141">The Linux VM needs access from the internet so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the Linux VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-to-the-vnet"></a><span data-ttu-id="942c8-142">Sanal ağ için bir alt ağ Ekle</span><span class="sxs-lookup"><span data-stu-id="942c8-142">Add a subnet to the VNet</span></span>

<span data-ttu-id="942c8-143">Sanal ağ içindeki VM'ler bir alt ağda bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="942c8-143">VMs within the VNet must be located in a subnet.</span></span>  <span data-ttu-id="942c8-144">Her sanal ağ birden çok alt ağa sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="942c8-144">Each VNet can have multiple subnets.</span></span>  <span data-ttu-id="942c8-145">Alt ağ oluşturmak ve alt ağ alt ağı için bir Güvenlik Duvarı'nı eklemek için NSG ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="942c8-145">Create the subnet and associate the subnet with the NSG to add a firewall to the subnet.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

<span data-ttu-id="942c8-146">Alt ağ içinde VNet eklenen ve NSG ve NSG kuralı ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="942c8-146">The Subnet is now added inside the VNet and associated with the NSG and the NSG rule.</span></span>

## <a name="creating-static-dns-names"></a><span data-ttu-id="942c8-147">Statik DNS adları oluşturuluyor</span><span class="sxs-lookup"><span data-stu-id="942c8-147">Creating static DNS names</span></span>

<span data-ttu-id="942c8-148">Azure çok esnektir, ancak sanal makineleri ad çözümlemesi için DNS adlarını kullanmak için DNS etiketleme kullanarak sanal ağ kartları (VNics) oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="942c8-148">Azure is very flexible, but to use DNS names for VMs name resolution, you need to create them as Virtual network cards (VNics) using DNS labeling.</span></span>  <span data-ttu-id="942c8-149">Bunları bunları farklı VM'ler için sanal makineleri geçici olarak olabileceği, statik bir kaynak olarak Vnıc tutan bağlanarak yeniden gibi VNics önemlidir.</span><span class="sxs-lookup"><span data-stu-id="942c8-149">VNics are important as you can reuse them by connecting them to different VMs, which keeps the VNic as a static resource while the VMs can be temporary.</span></span>  <span data-ttu-id="942c8-150">VNic üzerinde etiketleme DNS kullanarak, biz basit ad çözümlemesi VNet içindeki diğer vm'lerden etkinleştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="942c8-150">By using DNS labeling on the VNic, we are able to enable simple name resolution from other VMs in the VNet.</span></span>  <span data-ttu-id="942c8-151">Çözümlenebilir adları kullanarak sağlayan Otomasyon sunucusu DNS adı tarafından erişmek diğer VM'ler `Jenkins` veya Git sunucusu olarak `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="942c8-151">Using resolvable names enables other VMs to access the automation server by the DNS name `Jenkins` or the Git server as `gitrepo`.</span></span>  <span data-ttu-id="942c8-152">Bir Vnıc'teki oluşturun ve önceki adımda oluşturduğunuz alt ağ ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="942c8-152">Create a VNic and associate it with the Subnet created in the previous step.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="942c8-153">VNet ve NSG halinde VM dağıtma</span><span class="sxs-lookup"><span data-stu-id="942c8-153">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="942c8-154">Şimdi bir sanal ağ, bir alt ağ için SSH bağlantı noktası 22 dışındaki tüm gelen trafiği engelleyerek bizim alt korumak için bu sanal ağ ve güvenlik duvarı olarak davranan bir NSG içinde sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="942c8-154">We now have a VNet, a subnet inside that VNet, and an NSG acting as a firewall to protect our subnet by blocking all inbound traffic except port 22 for SSH.</span></span>  <span data-ttu-id="942c8-155">VM şimdi bu mevcut ağ altyapınızda içinde dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="942c8-155">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="942c8-156">Azure CLI kullanarak ve `azure vm create` komutu, var olan Azure kaynak grubu, sanal ağ, alt ağ ve Vnıc için Linux VM dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="942c8-156">Using the Azure CLI, and the `azure vm create` command, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>  <span data-ttu-id="942c8-157">Tam bir VM'yi dağıtmak için CLI kullanma ile ilgili daha fazla bilgi için bkz: [Azure CLI kullanarak eksiksiz bir Linux ortamı oluşturma](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="942c8-157">For more information on using the CLI to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

<span data-ttu-id="942c8-158">Var olan kaynakları çağırmak için CLI bayrakları kullanarak, biz VM mevcut bir ağ içinde dağıtmak için Azure isteyin.</span><span class="sxs-lookup"><span data-stu-id="942c8-158">By using the CLI flags to call out existing resources, we instruct Azure to deploy the VM inside the existing network.</span></span>  <span data-ttu-id="942c8-159">Bir VNet ve alt ağ dağıtıldıktan sonra yinelemek için bunlar Azure bölgesi içinde statik veya kalıcı kaynaklar olarak bırakılabilir.</span><span class="sxs-lookup"><span data-stu-id="942c8-159">To reiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="942c8-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="942c8-160">Next steps</span></span>
* [<span data-ttu-id="942c8-161">Azure CLI'si komutlarını doğrudan kullanarak bir Linux VM'si için kendi özel ortamınızı oluşturun</span><span class="sxs-lookup"><span data-stu-id="942c8-161">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="942c8-162">Şablonları kullanarak Azure'da bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="942c8-162">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
