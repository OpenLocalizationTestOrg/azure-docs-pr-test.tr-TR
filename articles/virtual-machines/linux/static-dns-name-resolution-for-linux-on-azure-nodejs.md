---
title: "aaaUsing VM için iç DNS ad çözümlemesi Azure üzerinde | Microsoft Docs"
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
ms.openlocfilehash: 94fd6577aa51ce5db4dc26649b415ddeeb410eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="92a02-103">Azure VM ad çözümlemesi için iç DNS kullanma</span><span class="sxs-lookup"><span data-stu-id="92a02-103">Using internal DNS for VM name resolution on Azure</span></span>

<span data-ttu-id="92a02-104">Bu makalede sanal NIC kartları (Vnıc) ve DNS etiket adları kullanarak nasıl tooset Linux VM'ler için statik iç DNS adlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="92a02-104">This article shows how tooset static internal DNS names for Linux VMs using Virtual NIC cards (VNic) and DNS label names.</span></span> <span data-ttu-id="92a02-105">Statik DNS adları, bu belge için kullanılan bir Jenkins yapı sunucusu veya Git sunucusu gibi kalıcı altyapı hizmetleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="92a02-105">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="92a02-106">Hello gereksinimleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="92a02-106">hello requirements are:</span></span>

* [<span data-ttu-id="92a02-107">Bir Azure hesabı</span><span class="sxs-lookup"><span data-stu-id="92a02-107">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="92a02-108">SSH ortak ve özel anahtar dosyaları</span><span class="sxs-lookup"><span data-stu-id="92a02-108">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="92a02-109">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="92a02-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="92a02-110">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="92a02-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="92a02-111">[Azure CLI 1.0](#quick-commands) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="92a02-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="92a02-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="92a02-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="92a02-113">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="92a02-113">Quick commands</span></span>

<span data-ttu-id="92a02-114">Tooquickly gerekiyorsa hello görevi, gerekli hello komutları bölümden hello ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="92a02-114">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="92a02-115">Her adım hello belgenin hello kalan bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="92a02-115">More detailed information and context for each step can be found hello rest of hello document, [starting here](#detailed-walkthrough).</span></span>  

<span data-ttu-id="92a02-116">Ön gereksinimlerini: SSH ile kaynak grubu, VNet, NSG gelen, alt ağ.</span><span class="sxs-lookup"><span data-stu-id="92a02-116">Pre-Requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span>

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a><span data-ttu-id="92a02-117">Statik iç DNS adı ile bir Vnıc'teki oluşturma</span><span class="sxs-lookup"><span data-stu-id="92a02-117">Create a VNic with a static internal DNS name</span></span>

<span data-ttu-id="92a02-118">Merhaba `-r` hello Vnıc hello statik DNS ad sağlar ayarı hello DNS etiketi CLI bayrağı içindir.</span><span class="sxs-lookup"><span data-stu-id="92a02-118">hello `-r` cli flag is for setting hello DNS label, which provides hello static DNS name for hello VNic.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-hello-vm-into-hello-vnet-nsg-and-connect-hello-vnic"></a><span data-ttu-id="92a02-119">Merhaba VNet, NSG içine Hello VM dağıtmak ve hello Vnıc bağlanın</span><span class="sxs-lookup"><span data-stu-id="92a02-119">Deploy hello VM into hello VNet, NSG and, connect hello VNic</span></span>

<span data-ttu-id="92a02-120">Merhaba `-N` hello Vnıc toohello bağlayan hello dağıtım tooAzure sırasında yeni VM.</span><span class="sxs-lookup"><span data-stu-id="92a02-120">hello `-N` connects hello VNic toohello new VM during hello deployment tooAzure.</span></span>

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

## <a name="detailed-walkthrough"></a><span data-ttu-id="92a02-121">Ayrıntılı kılavuz</span><span class="sxs-lookup"><span data-stu-id="92a02-121">Detailed walkthrough</span></span>

<span data-ttu-id="92a02-122">Bir tam sürekli tümleştirme ve sürekli dağıtımı (CiCd) altyapısı Azure ile ilgili belirli sunucuları toobe statik veya uzun süreli sunucuları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="92a02-122">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers toobe static or long-lived servers.</span></span>  <span data-ttu-id="92a02-123">Merhaba sanal ağlar (Vnet'ler) ve ağ güvenlik grupları (Nsg'ler) gibi Azure varlıklar statik olmalıdır ve nadiren dağıtılan kaynakları uzun ömürlü önerilir.</span><span class="sxs-lookup"><span data-stu-id="92a02-123">It is recommended that Azure assets like hello Virtual Networks (VNets) and Network Security Groups (NSGs), should be static and long lived resources that are rarely deployed.</span></span>  <span data-ttu-id="92a02-124">Bir VNet dağıtıldıktan sonra herhangi bir olumsuz etkiler toohello altyapı olmadan yeni dağıtımlar tarafından yeniden.</span><span class="sxs-lookup"><span data-stu-id="92a02-124">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span>  <span data-ttu-id="92a02-125">Toothis statik ağ Git ekleme deposu sunucusu ve Jenkins Otomasyon sunucusu sunar CiCd tooyour geliştirme veya test ortamları.</span><span class="sxs-lookup"><span data-stu-id="92a02-125">Adding toothis static network a Git repository server and a Jenkins automation server delivers CiCd tooyour development or test environments.</span></span>  

<span data-ttu-id="92a02-126">İç DNS adları, yalnızca bir Azure sanal ağı içinde çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="92a02-126">Internal DNS names are only resolvable inside an Azure virtual network.</span></span>  <span data-ttu-id="92a02-127">Merhaba DNS adlarını iç olduğundan, bunlar dışında ek güvenlik toohello altyapısı sağlayan Internet çözümlenebilir toohello değildir.</span><span class="sxs-lookup"><span data-stu-id="92a02-127">Because hello DNS names are internal, they are not resolvable toohello outside internet, providing additional security toohello infrastructure.</span></span>

<span data-ttu-id="92a02-128">_Tüm örnekleri kendi adlandırma ile değiştirin._</span><span class="sxs-lookup"><span data-stu-id="92a02-128">_Replace any examples with your own naming._</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="92a02-129">Merhaba kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="92a02-129">Create hello Resource group</span></span>

<span data-ttu-id="92a02-130">Bir kaynak grubu gerekli tooorganize bu kılavuzda oluşturuyoruz gereken her şey vardır.</span><span class="sxs-lookup"><span data-stu-id="92a02-130">A Resource Group is needed tooorganize everything we create in this walkthrough.</span></span>  <span data-ttu-id="92a02-131">Azure kaynak grupları hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="92a02-131">For more information on Azure Resource Groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-hello-vnet"></a><span data-ttu-id="92a02-132">Merhaba VNet oluşturma</span><span class="sxs-lookup"><span data-stu-id="92a02-132">Create hello VNet</span></span>

<span data-ttu-id="92a02-133">Merhaba ilk VNet toolaunch hello VM'ler içine toobuild adımdır.</span><span class="sxs-lookup"><span data-stu-id="92a02-133">hello first step is toobuild a VNet toolaunch hello VMs into.</span></span>  <span data-ttu-id="92a02-134">Merhaba VNet Bu izlenecek yol için bir alt ağ içerir.</span><span class="sxs-lookup"><span data-stu-id="92a02-134">hello VNet contains one subnet for this walkthrough.</span></span>  <span data-ttu-id="92a02-135">Azure sanal ağlar hakkında daha fazla bilgi için bkz: [hello Azure CLI kullanarak bir sanal ağ oluşturma](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="92a02-135">For more information on Azure VNets, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-hello-nsg"></a><span data-ttu-id="92a02-136">Merhaba NSG oluşturma</span><span class="sxs-lookup"><span data-stu-id="92a02-136">Create hello NSG</span></span>

<span data-ttu-id="92a02-137">Biz hello NSG önce hello alt ağ oluşturmak için varolan bir ağ güvenlik grubu hello alt oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="92a02-137">hello Subnet is built behind an existing Network Security Group so we build hello NSG before hello Subnet.</span></span>  <span data-ttu-id="92a02-138">Azure Nsg'ler hello ağ katmanında eşdeğer tooa Güvenlik Duvarı ' dir.</span><span class="sxs-lookup"><span data-stu-id="92a02-138">Azure NSGs are equivalent tooa firewall at hello network layer.</span></span>  <span data-ttu-id="92a02-139">Azure Nsg'ler hakkında daha fazla bilgi için bkz: [nasıl toocreate Nsg'ler Azure CLI hello](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="92a02-139">For more information on Azure NSGs, see [How toocreate NSGs in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="92a02-140">Gelen bir SSH izin ver Kuralı Ekle</span><span class="sxs-lookup"><span data-stu-id="92a02-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="92a02-141">Merhaba Linux VM gelen bağlantı noktası 22 trafiği toobe veren bir kural hello ağ tooport 22 hello Linux VM üzerinde geçirilen şekilde Internet gerekli hello erişimden gerekir.</span><span class="sxs-lookup"><span data-stu-id="92a02-141">hello Linux VM needs access from hello internet so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello Linux VM is needed.</span></span>

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

## <a name="add-a-subnet-toohello-vnet"></a><span data-ttu-id="92a02-142">Bir alt ağ toohello VNet ekleme</span><span class="sxs-lookup"><span data-stu-id="92a02-142">Add a subnet toohello VNet</span></span>

<span data-ttu-id="92a02-143">VM'ler hello VNet içindeki bir alt ağda bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="92a02-143">VMs within hello VNet must be located in a subnet.</span></span>  <span data-ttu-id="92a02-144">Her sanal ağ birden çok alt ağa sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="92a02-144">Each VNet can have multiple subnets.</span></span>  <span data-ttu-id="92a02-145">Merhaba alt ağı oluşturup hello NSG tooadd bir güvenlik duvarı toohello alt hello alt ağını ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="92a02-145">Create hello subnet and associate hello subnet with hello NSG tooadd a firewall toohello subnet.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

<span data-ttu-id="92a02-146">Merhaba alt şimdi hello VNet eklenir ve hello NSG ve hello NSG kuralı ile ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="92a02-146">hello Subnet is now added inside hello VNet and associated with hello NSG and hello NSG rule.</span></span>

## <a name="creating-static-dns-names"></a><span data-ttu-id="92a02-147">Statik DNS adları oluşturuluyor</span><span class="sxs-lookup"><span data-stu-id="92a02-147">Creating static DNS names</span></span>

<span data-ttu-id="92a02-148">Azure çok esnektir, ancak toouse DNS adlarını VM'ler ad çözümlemesi için sanal olarak etiketleme DNS kullanarak (VNics) ağ kartı toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="92a02-148">Azure is very flexible, but toouse DNS names for VMs name resolution, you need toocreate them as Virtual network cards (VNics) using DNS labeling.</span></span>  <span data-ttu-id="92a02-149">Bunları bağlantı kurarak toodifferent VM'ler hello VM'ler geçici olarak olabileceği, statik bir kaynak olarak hello Vnıc tutan yeniden kullanabileceğiniz gibi VNics önemlidir.</span><span class="sxs-lookup"><span data-stu-id="92a02-149">VNics are important as you can reuse them by connecting them toodifferent VMs, which keeps hello VNic as a static resource while hello VMs can be temporary.</span></span>  <span data-ttu-id="92a02-150">Merhaba VNic üzerinde etiketleme DNS kullanarak, mümkün tooenable basit ad çözümlemesi hello VNet içindeki diğer vm'lerden duyuyoruz.</span><span class="sxs-lookup"><span data-stu-id="92a02-150">By using DNS labeling on hello VNic, we are able tooenable simple name resolution from other VMs in hello VNet.</span></span>  <span data-ttu-id="92a02-151">Hello DNS adı tarafından sağlayan diğer VM'ler tooaccess hello Otomasyon sunucusu çözümlenebilir adları kullanarak `Jenkins` veya hello Git sunucusu olarak `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="92a02-151">Using resolvable names enables other VMs tooaccess hello automation server by hello DNS name `Jenkins` or hello Git server as `gitrepo`.</span></span>  <span data-ttu-id="92a02-152">Bir Vnıc'teki oluşturun ve alt ağ hello önceki adımda oluşturduğunuz hello ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="92a02-152">Create a VNic and associate it with hello Subnet created in hello previous step.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="92a02-153">Merhaba VM hello VNet içine ve NSG dağıtma</span><span class="sxs-lookup"><span data-stu-id="92a02-153">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="92a02-154">Şimdi bir sanal ağ, bir alt ağ, sanal ağ ve SSH için bağlantı noktası 22 dışındaki tüm gelen trafiği engelleyerek bizim alt ağ güvenlik duvarı tooprotect davranan bir NSG içinde sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="92a02-154">We now have a VNet, a subnet inside that VNet, and an NSG acting as a firewall tooprotect our subnet by blocking all inbound traffic except port 22 for SSH.</span></span>  <span data-ttu-id="92a02-155">Merhaba VM şimdi bu mevcut ağ altyapınızda içinde dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="92a02-155">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="92a02-156">Kullanarak Azure CLI hello ve hello `azure vm create` hello Linux VM olan Azure kaynak grubu, sanal ağ, alt ağ ve Vnıc varolan dağıtılan toohello komutu.</span><span class="sxs-lookup"><span data-stu-id="92a02-156">Using hello Azure CLI, and hello `azure vm create` command, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>  <span data-ttu-id="92a02-157">Hello CLI toodeploy tam VM kullanma hakkında daha fazla bilgi için bkz: [hello Azure CLI kullanarak eksiksiz bir Linux ortamı oluşturma](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="92a02-157">For more information on using hello CLI toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

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

<span data-ttu-id="92a02-158">Hello kullanarak CLI toocall var olan kaynakların çıkışı biz hello mevcut ağ içinde Azure toodeploy hello VM istemeniz işaretler.</span><span class="sxs-lookup"><span data-stu-id="92a02-158">By using hello CLI flags toocall out existing resources, we instruct Azure toodeploy hello VM inside hello existing network.</span></span>  <span data-ttu-id="92a02-159">bir VNet ve alt ağ dağıtıldıktan sonra tooreiterate, bunlar Azure bölgesi içinde statik veya kalıcı kaynaklar olarak bırakılabilir.</span><span class="sxs-lookup"><span data-stu-id="92a02-159">tooreiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="92a02-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="92a02-160">Next steps</span></span>
* [<span data-ttu-id="92a02-161">Azure CLI'si komutlarını doğrudan kullanarak bir Linux VM'si için kendi özel ortamınızı oluşturun</span><span class="sxs-lookup"><span data-stu-id="92a02-161">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="92a02-162">Şablonları kullanarak Azure'da bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="92a02-162">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
