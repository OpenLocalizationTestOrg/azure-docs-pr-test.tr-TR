---
title: "aaaCreate PowerShell kullanarak birden çok NIC'yle bir VM'yi (Klasik) | Microsoft Docs"
description: "Bilgi nasıl toocreate ve PowerShell kullanarak birden çok NIC VM'ler yapılandırın."
services: virtual-network, virtual-machines
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a1a3952c-2dcc-4977-bd7a-52d623c1fb07
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 8ef35bd4cfd7e6a527080f1cfc541275ca86f5e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a><span data-ttu-id="d0d47-103">Birden çok NIC ile VM (Klasik) oluşturun</span><span class="sxs-lookup"><span data-stu-id="d0d47-103">Create a VM (Classic) with multiple NICs</span></span>
<span data-ttu-id="d0d47-104">Sanal makineler (VM'ler) oluşturma ve birden çok ağ arabirimlerine (NIC'ler) tooeach, VM'lerin ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d0d47-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="d0d47-105">Birden çok NIC uygulama sunma ve WAN iyileştirmesi çözümleri gibi birçok ağ sanal Gereçleri gereksinimi var.</span><span class="sxs-lookup"><span data-stu-id="d0d47-105">Multiple NICs are a requirement for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span> <span data-ttu-id="d0d47-106">Birden çok NIC de NIC'ler arasında trafik yalıtımı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0d47-106">Multiple NICs also provide isolation of traffic between NICs.</span></span>

![VM için multi NIC](./media/virtual-networks-multiple-nics/IC757773.png)

<span data-ttu-id="d0d47-108">üç NIC ile VM Hello şekil gösterir, her tooa farklı alt bağlı.</span><span class="sxs-lookup"><span data-stu-id="d0d47-108">hello figure shows a VM with three NICs, each connected tooa different subnet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d0d47-109">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d0d47-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d0d47-110">Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="d0d47-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="d0d47-111">Microsoft, en yeni dağıtımların Resource Manager kullanmanızı önerir.</span><span class="sxs-lookup"><span data-stu-id="d0d47-111">Microsoft recommends that most new deployments use Resource Manager.</span></span>

* <span data-ttu-id="d0d47-112">Internet'e yönelik VIP (Klasik dağıtımlar) yalnızca hello "varsayılan" NIC üzerinde desteklenir</span><span class="sxs-lookup"><span data-stu-id="d0d47-112">Internet-facing VIP (classic deployments) is only supported on hello "default" NIC.</span></span> <span data-ttu-id="d0d47-113">Merhaba varsayılan NIC yalnızca bir VIP toohello IP'si yok</span><span class="sxs-lookup"><span data-stu-id="d0d47-113">There is only one VIP toohello IP of hello default NIC.</span></span>
* <span data-ttu-id="d0d47-114">Şu anda örnek düzeyinde ortak IP (LPIP) adresleri (Klasik dağıtımlar) birden çok NIC sanal makineleri için desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="d0d47-114">At this time, Instance Level Public IP (LPIP) addresses (classic deployments) are not supported for multi NIC VMs.</span></span>
* <span data-ttu-id="d0d47-115">Merhaba hello NIC'ler sırasını VM rastgele olur ve ayrıca Azure altyapı güncelleştirmeleri arasında değişebilir hello içinde.</span><span class="sxs-lookup"><span data-stu-id="d0d47-115">hello order of hello NICs from inside hello VM will be random, and could also change across Azure infrastructure updates.</span></span> <span data-ttu-id="d0d47-116">Ancak, hello IP adresleri ve karşılık gelen ethernet MAC hello adresleri kalacak aynı hello.</span><span class="sxs-lookup"><span data-stu-id="d0d47-116">However, hello IP addresses, and hello corresponding ethernet MAC addresses will remain hello same.</span></span> <span data-ttu-id="d0d47-117">Örneğin, varsayın **Eth1** bir Azure Altyapı güncelleştirme ve yeniden başlatma çok değiştirilemedi; IP adresi 10.1.0.100 ve 00-0D-3A-B0-39-0D MAC adresi var.**Eth2**, ancak işlem eşleştirme IP ve MAC hello Kalan aynı hello.</span><span class="sxs-lookup"><span data-stu-id="d0d47-117">For example, assume **Eth1** has IP address 10.1.0.100 and MAC address 00-0D-3A-B0-39-0D; after an Azure infrastructure update and reboot, it could be changed too**Eth2**, but hello IP and MAC pairing will remain hello same.</span></span> <span data-ttu-id="d0d47-118">Müşteri tarafından başlatılan yeniden başlatma olduğunda hello NIC sipariş kalacak aynı hello.</span><span class="sxs-lookup"><span data-stu-id="d0d47-118">When a restart is customer-initiated, hello NIC order will remain hello same.</span></span>
* <span data-ttu-id="d0d47-119">Merhaba adresi her NIC'nin her VM için bir alt ağda bulunması gerekir, tek bir birden çok NIC VM her atanabilir içinde adreslerinin aynı alt ağda hello.</span><span class="sxs-lookup"><span data-stu-id="d0d47-119">hello address for each NIC on each VM must be located in a subnet, multiple NICs on a single VM can each be assigned addresses that are in hello same subnet.</span></span>
* <span data-ttu-id="d0d47-120">Hello VM boyutu için bir VM oluşturun NIC hello sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="d0d47-120">hello VM size determines hello number of NICS that you can create for a VM.</span></span> <span data-ttu-id="d0d47-121">Başvuru hello [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ve [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM boyutları makaleleri toodetermine kaç NIC her VM boyutunu destekler.</span><span class="sxs-lookup"><span data-stu-id="d0d47-121">Reference hello [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM sizes articles toodetermine how many NICS each VM size supports.</span></span> 

## <a name="network-security-groups-nsgs"></a><span data-ttu-id="d0d47-122">Ağ güvenlik grupları (Nsg'ler)</span><span class="sxs-lookup"><span data-stu-id="d0d47-122">Network Security Groups (NSGs)</span></span>
<span data-ttu-id="d0d47-123">Resource Manager dağıtımında, bir VM üzerinde herhangi bir NIC ile ağ güvenlik grubu (birden çok NIC etkin olan bir VM üzerinde herhangi bir NIC içeren NSG), ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="d0d47-123">In a Resource Manager deployment, any NIC on a VM may be associated with a Network Security Group (NSG), including any NICs on a VM that has multiple NICs enabled.</span></span> <span data-ttu-id="d0d47-124">Bir NIC hello alt ağa bir NSG ile ilişkili olduğu bir alt ağ içinden bir adres atanırsa, ardından hello kuralları hello alt ağın NSG de toothat NIC Uygula</span><span class="sxs-lookup"><span data-stu-id="d0d47-124">If a NIC is assigned an address within a subnet where hello subnet is associated with an NSG, then hello rules in hello subnet’s NSG also apply toothat NIC.</span></span> <span data-ttu-id="d0d47-125">Nsg'ler ile toplama tooassociating alt ağlarında bir NSG'yi bir NIC de ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0d47-125">In addition tooassociating subnets with NSGs, you can also associate a NIC with an NSG.</span></span>

<span data-ttu-id="d0d47-126">Bir alt ağa bir NSG ve içinde bir NIC ile ilişkili ise bu alt ağ ile bir NSG tek tek ilişkilidir, ilişkili hello NSG kuralları uygulanır **akış sırası** toohello trafiğin yönü, içinde veya dışında geçirilen hello göre Merhaba NIC:</span><span class="sxs-lookup"><span data-stu-id="d0d47-126">If a subnet is associated with an NSG, and a NIC within that subnet is individually associated with an NSG, hello associated NSG rules are applied in **flow order** according toohello direction of hello traffic being passed into or out of hello NIC:</span></span>

* <span data-ttu-id="d0d47-127">**Gelen trafiği** hello NIC soru, hedefi olan akışlar ilk NIC hello geçirme sonra hello NIC'ın NSG kuralları tetiklemeden önce hello alt ağın NSG kuralları tetikleme hello alt ağ üzerinden.</span><span class="sxs-lookup"><span data-stu-id="d0d47-127">**Incoming traffic** whose destination is hello NIC in question flows first through hello subnet, triggering hello subnet’s NSG rules, before passing into hello NIC, then triggering hello NIC’s NSG rules.</span></span>
* <span data-ttu-id="d0d47-128">**Giden trafik** akar hello hello alt ağa geçirmeden sonra hello alt ağın NSG kuralları tetiklemeden önce hello NIC'ın NSG kuralları tetikleme NIC ilk out hello NIC söz konusu olan kaynağıdır.</span><span class="sxs-lookup"><span data-stu-id="d0d47-128">**Outgoing traffic** whose source is hello NIC in question flows first out from hello NIC, triggering hello NIC’s NSG rules, before passing through hello subnet, then triggering hello subnet’s NSG rules.</span></span>

<span data-ttu-id="d0d47-129">Daha fazla bilgi edinmek [ağ güvenlik grupları](virtual-networks-nsg.md) ve nasıl uygulandığını ilişkilendirmeleri toosubnets, sanal makineleri ve NIC göre...</span><span class="sxs-lookup"><span data-stu-id="d0d47-129">Learn more about [Network Security Groups](virtual-networks-nsg.md) and how they are applied based on associations toosubnets, VMs, and NICs..</span></span>

## <a name="how-tooconfigure-a-multi-nic-vm-in-a-classic-deployment"></a><span data-ttu-id="d0d47-130">Nasıl tooConfigure klasik bir dağıtımda birden çok NIC VM</span><span class="sxs-lookup"><span data-stu-id="d0d47-130">How tooConfigure a multi NIC VM in a classic deployment</span></span>
<span data-ttu-id="d0d47-131">Merhaba yönergelerde birden çok NIC 3 NIC içeren VM oluşturmanıza yardımcı olur: varsayılan bir NIC ve iki ek NIC.</span><span class="sxs-lookup"><span data-stu-id="d0d47-131">hello instructions below will help you create a multi NIC VM containing 3 NICs: a default NIC and two additional NICs.</span></span> <span data-ttu-id="d0d47-132">Merhaba yapılandırma adımları toohello hizmet yapılandırma dosyası parça aşağıdaki göre yapılandırılmış bir VM oluşturacak:</span><span class="sxs-lookup"><span data-stu-id="d0d47-132">hello configuration steps will create a VM that will be configured according toohello service configuration file fragment below:</span></span>

    <VirtualNetworkSite name="MultiNIC-VNet" Location="North Europe">
    <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
    … Skip over hello remainder section …
    </VirtualNetworkSite>


<span data-ttu-id="d0d47-133">Önkoşullar toorun hello PowerShell komutlarını hello örnekte denemeden önce aşağıdaki hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0d47-133">You need hello following prerequisites before trying toorun hello PowerShell commands in hello example.</span></span>

* <span data-ttu-id="d0d47-134">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="d0d47-134">An Azure subscription.</span></span>
* <span data-ttu-id="d0d47-135">Yapılandırılmış bir sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="d0d47-135">A configured virtual network.</span></span> <span data-ttu-id="d0d47-136">Bkz: [Virtual Network'e genel bakış](virtual-networks-overview.md) sanal ağlar hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="d0d47-136">See [Virtual Network Overview](virtual-networks-overview.md) for more information about VNets.</span></span>
* <span data-ttu-id="d0d47-137">Azure PowerShell'in en son sürümünü Hello indirilir ve yüklenir.</span><span class="sxs-lookup"><span data-stu-id="d0d47-137">hello latest version of Azure PowerShell downloaded and installed.</span></span> <span data-ttu-id="d0d47-138">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d0d47-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="d0d47-139">birden çok NIC, aşağıdaki adımları tek bir PowerShell oturumunda her komutunu girerek tam hello'yle bir VM'yi toocreate:</span><span class="sxs-lookup"><span data-stu-id="d0d47-139">toocreate a VM with multiple NICs, complete hello following steps by entering each command within a single PowerShell session:</span></span>

1. <span data-ttu-id="d0d47-140">Azure VM görüntü Galeriden bir VM görüntüsü seçin.</span><span class="sxs-lookup"><span data-stu-id="d0d47-140">Select a VM image from Azure VM image gallery.</span></span> <span data-ttu-id="d0d47-141">Görüntüleri sık sık değişen ve bölgeye göre kullanılabilir olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d0d47-141">Note that images change frequently and are available by region.</span></span> <span data-ttu-id="d0d47-142">Hello hello aşağıdaki örnekte belirtilen görüntüsü değiştirmek veya değil bölgenizde olması, bu nedenle emin olun ihtiyacınız toospecify hello görüntü.</span><span class="sxs-lookup"><span data-stu-id="d0d47-142">hello image specified in hello example below may change or might not be in your region, so be sure toospecify hello image you need.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. <span data-ttu-id="d0d47-143">Bir VM yapılandırması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d0d47-143">Create a VM configuration.</span></span>

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. <span data-ttu-id="d0d47-144">Merhaba varsayılan yönetici oturum açma oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d0d47-144">Create hello default administrator login.</span></span>

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. <span data-ttu-id="d0d47-145">Ek NIC toohello VM yapılandırmasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d0d47-145">Add additional NICs toohello VM configuration.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. <span data-ttu-id="d0d47-146">Merhaba varsayılan NIC için Hello alt ağ ve IP adresi belirtin</span><span class="sxs-lookup"><span data-stu-id="d0d47-146">Specify hello subnet and IP address for hello default NIC.</span></span>

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. <span data-ttu-id="d0d47-147">Merhaba VM sanal ağınızda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d0d47-147">Create hello VM in your virtual network.</span></span>

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > <span data-ttu-id="d0d47-148">Hello burada belirttiğiniz VNet (Merhaba önkoşullarını belirtildiği gibi) olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0d47-148">hello VNet that you specify here must already exist (as mentioned in hello prerequisites).</span></span> <span data-ttu-id="d0d47-149">Aşağıdaki örnek Hello belirtir adlı bir sanal ağ **MultiNIC VNet**.</span><span class="sxs-lookup"><span data-stu-id="d0d47-149">hello example below specifies a virtual network named **MultiNIC-VNet**.</span></span>
    >

## <a name="limitations"></a><span data-ttu-id="d0d47-150">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="d0d47-150">Limitations</span></span>
<span data-ttu-id="d0d47-151">birden çok NIC kullanırken aşağıdaki sınırlamalar hello geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="d0d47-151">hello following limitations are applicable when using multiple NICs:</span></span>

* <span data-ttu-id="d0d47-152">Birden çok NIC içeren VM'ler Azure sanal ağlar (Vnet'ler) içinde oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0d47-152">VMs with multiple NICs must be created in Azure virtual networks (VNets).</span></span> <span data-ttu-id="d0d47-153">Non-VNet VM'ler ile birden çok NIC yapılandırılamaz.</span><span class="sxs-lookup"><span data-stu-id="d0d47-153">Non-VNet VMs cannot be configured with multiple NICs.</span></span>
* <span data-ttu-id="d0d47-154">Birden çok NIC veya tek bir NIC gerek toouse tüm sanal makineleri bir kullanılabilirlik kümesi</span><span class="sxs-lookup"><span data-stu-id="d0d47-154">All VMs in an availability set need toouse either multiple NICs or a single NIC.</span></span> <span data-ttu-id="d0d47-155">Birden çok NIC VM'ler ve bir kullanılabilirlik kümesi içinde tek NIC VM'ler bileşimi olamaz.</span><span class="sxs-lookup"><span data-stu-id="d0d47-155">There cannot be a mixture of multiple NIC VMs and single NIC VMs within an availability set.</span></span> <span data-ttu-id="d0d47-156">Aynı kuralları, bir bulut hizmetinde VM'ler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d0d47-156">Same rules apply for VMs in a cloud service.</span></span> <span data-ttu-id="d0d47-157">Gerekli olmayan birden çok NIC VM'ler için en az iki sahip oldukları her sürece toohave hello NIC'ler, aynı sayıda.</span><span class="sxs-lookup"><span data-stu-id="d0d47-157">For multiple NIC VMs, they aren't required toohave hello same number of NICs, as long as they each have at least two.</span></span>
* <span data-ttu-id="d0d47-158">Birden çok NIC (ve tersi) ile tek bir NIC ile VM yapılandırılamaz, silme ve yeniden oluşturulması dağıtıldıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="d0d47-158">A VM with a single NIC cannot be configured with multi NICs (and vice-versa) once it is deployed, without deleting and re-creating it.</span></span>

## <a name="secondary-nics-access-tooother-subnets"></a><span data-ttu-id="d0d47-159">İkincil NIC'ler erişim tooother alt</span><span class="sxs-lookup"><span data-stu-id="d0d47-159">Secondary NICs access tooother subnets</span></span>
<span data-ttu-id="d0d47-160">İkincil NIC'ler bir varsayılan ağ geçidi ile değil yapılandırılacak varsayılan olarak, toowhich hello trafik akışını hello son ikincil NIC sınırlı toobe hello içinde olacaktır aynı alt ağ.</span><span class="sxs-lookup"><span data-stu-id="d0d47-160">By default secondary NICs will not be configured with a default gateway, due toowhich hello traffic flow on hello secondary NICs will be limited toobe within hello same subnet.</span></span> <span data-ttu-id="d0d47-161">Merhaba kullanıcıların tooenable ikincil NIC'ler tootalk kendi alt ağı dışından istiyorsanız, bunlar hello yönlendirme tablosu tooconfigure hello ağ geçidi olarak bir giriş aşağıda açıklanan tooadd gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0d47-161">If hello users want tooenable secondary NICs tootalk outside their own subnet, they will need tooadd an entry in hello routing table tooconfigure hello gateway as described below.</span></span>

> [!NOTE]
> <span data-ttu-id="d0d47-162">Temmuz 2015 tüm NIC'ler için yapılandırılmış bir varsayılan ağ geçidi olabilir önce oluşturulan VM'ler.</span><span class="sxs-lookup"><span data-stu-id="d0d47-162">VMs created before July 2015 may have a default gateway configured for all NICs.</span></span> <span data-ttu-id="d0d47-163">Bu sanal makineleri yeniden kadar ikincil NIC'ler için hello varsayılan ağ geçidi kaldırılmaz.</span><span class="sxs-lookup"><span data-stu-id="d0d47-163">hello default gateway for secondary NICs will not be removed until these VMs are rebooted.</span></span> <span data-ttu-id="d0d47-164">İşletim sistemlerindeki hello zayıf ana bilgisayar yönlendirme modeli, Linux gibi kullanın Hello giriş ve çıkış trafiği farklı NIC'ler kullanırsanız Internet bağlantısını kesebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0d47-164">In Operating systems that use hello weak host routing model, such as Linux, Internet connectivity can break if hello ingress and egress traffic use different NICs.</span></span>
> 

### <a name="configure-windows-vms"></a><span data-ttu-id="d0d47-165">Windows sanal makineleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d0d47-165">Configure Windows VMs</span></span>
<span data-ttu-id="d0d47-166">İki NIC içeren bir Windows VM gibi olduğunu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="d0d47-166">Suppose that you have a Windows VM with two NICs as follows:</span></span>

* <span data-ttu-id="d0d47-167">Birincil NIC IP adresi: 192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="d0d47-167">Primary NIC IP address: 192.168.1.4</span></span>
* <span data-ttu-id="d0d47-168">İkincil NIC IP adresi: 192.168.2.5</span><span class="sxs-lookup"><span data-stu-id="d0d47-168">Secondary NIC IP address: 192.168.2.5</span></span>

<span data-ttu-id="d0d47-169">Bu VM için Hello IPv4 yol tablosu şöyle olabilir:</span><span class="sxs-lookup"><span data-stu-id="d0d47-169">hello IPv4 route table for this VM would look like this:</span></span>

    IPv4 Route Table
    ===========================================================================
    Active Routes:
    Network Destination        Netmask          Gateway       Interface  Metric
              0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
            127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
            127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
      127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        168.63.129.16  255.255.255.255      192.168.1.1      192.168.1.4      6
          192.168.1.0    255.255.255.0         On-link       192.168.1.4    261
          192.168.1.4  255.255.255.255         On-link       192.168.1.4    261
        192.168.1.255  255.255.255.255         On-link       192.168.1.4    261
          192.168.2.0    255.255.255.0         On-link       192.168.2.5    261
          192.168.2.5  255.255.255.255         On-link       192.168.2.5    261
        192.168.2.255  255.255.255.255         On-link       192.168.2.5    261
            224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
            224.0.0.0        240.0.0.0         On-link       192.168.1.4    261
            224.0.0.0        240.0.0.0         On-link       192.168.2.5    261
      255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
      255.255.255.255  255.255.255.255         On-link       192.168.1.4    261
      255.255.255.255  255.255.255.255         On-link       192.168.2.5    261
    ===========================================================================

<span data-ttu-id="d0d47-170">Bu hello varsayılan yol (0.0.0.0) yalnızca kullanılabilir toohello birincil NIC olduğuna dikkat edin</span><span class="sxs-lookup"><span data-stu-id="d0d47-170">Notice that hello default route (0.0.0.0) is only available toohello primary NIC.</span></span> <span data-ttu-id="d0d47-171">Merhaba ikincil için hello alt dışındaki mümkün tooaccess kaynaklar olmaz aşağıda görüldüğü gibi NIC:</span><span class="sxs-lookup"><span data-stu-id="d0d47-171">You will not be able tooaccess resources outside hello subnet for hello secondary NIC, as seen below:</span></span>

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

<span data-ttu-id="d0d47-172">Varsayılan rota tooadd hello ikincil NIC, aşağıdaki hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d0d47-172">tooadd a default route on hello secondary NIC, follow hello steps below:</span></span>

1. <span data-ttu-id="d0d47-173">Merhaba tooidentify hello dizin numarasını aşağıdaki hello komutunu bir komut isteminden çalıştırın ikincil NIC:</span><span class="sxs-lookup"><span data-stu-id="d0d47-173">From a command prompt, run hello command below tooidentify hello index number for hello secondary NIC:</span></span>
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. <span data-ttu-id="d0d47-174">(Bu örnekte) 27 dizini ile Merhaba tablosunda ikinci girişi Hello dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d0d47-174">Notice hello second entry in hello table, with an index of 27 (in this example).</span></span>
3. <span data-ttu-id="d0d47-175">Merhaba Hello komut isteminden çalıştırın **yolu Ekle** komutunu aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="d0d47-175">From hello command prompt, run hello **route add** command as shown below.</span></span> <span data-ttu-id="d0d47-176">Bu örnekte, hello için hello varsayılan ağ geçidi olarak 192.168.2.1 belirtiyorsanız ikincil NIC:</span><span class="sxs-lookup"><span data-stu-id="d0d47-176">In this example, you are specifying 192.168.2.1 as hello default gateway for hello secondary NIC:</span></span>
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. <span data-ttu-id="d0d47-177">tootest bağlantısı toohello komut istemi geri dönün ve farklı bir alt ağdan hello ikincil NIC gösterilen int eh aşağıdaki örnekte tooping deneyin:</span><span class="sxs-lookup"><span data-stu-id="d0d47-177">tootest connectivity, go back toohello command prompt and try tooping a different subnet from hello secondary NIC as shown int eh example below:</span></span>
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. <span data-ttu-id="d0d47-178">Ayrıca, rota tablosu toocheck hello yolu, yeni eklenen aşağıda gösterildiği gibi kontrol edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d0d47-178">You can also check your route table toocheck hello newly added route, as shown below:</span></span>
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a><span data-ttu-id="d0d47-179">Linux sanal makineleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d0d47-179">Configure Linux VMs</span></span>
<span data-ttu-id="d0d47-180">Merhaba varsayılan davranışı yönlendirme, zayıf konak kullandığından Linux VM'ler için o hello ikincil NIC'ler öneririz hello içinde yalnızca kısıtlı tootraffic akışları olan aynı alt ağ.</span><span class="sxs-lookup"><span data-stu-id="d0d47-180">For Linux VMs, since hello default behavior uses weak host routing, we recommend that hello secondary NICs are restricted tootraffic flows only within hello same subnet.</span></span> <span data-ttu-id="d0d47-181">Ancak bazı senaryolar hello alt dışında bağlantı istiyorsa, kullanıcıların giriş hello İlkesi tabanlı yönlendirme tooensure etkinleştirmeniz gerekir ve çıkış trafiği kullandığı aynı NIC hello</span><span class="sxs-lookup"><span data-stu-id="d0d47-181">However if certain scenarios demand connectivity outside hello subnet, users should enable policy based routing tooensure that hello ingress and egress traffic uses hello same NIC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0d47-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d0d47-182">Next steps</span></span>
* <span data-ttu-id="d0d47-183">Dağıtma [MultiNIC VM'ler 2 katmanlı uygulama senaryosunda bir Resource Manager dağıtımında](virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="d0d47-183">Deploy [MultiNIC VMs in a 2-tier application scenario in a Resource Manager deployment](virtual-network-deploy-multinic-arm-template.md).</span></span>
* <span data-ttu-id="d0d47-184">Dağıtma [Klasik dağıtım 2 katmanlı uygulama senaryoda MultiNIC Vm'lerde](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d0d47-184">Deploy [MultiNIC VMs in a 2-tier application scenario in a classic deployment](virtual-network-deploy-multinic-classic-ps.md).</span></span>

