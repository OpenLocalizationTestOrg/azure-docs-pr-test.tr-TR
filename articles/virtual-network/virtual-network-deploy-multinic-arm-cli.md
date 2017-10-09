---
title: "birden çok NIC - Azure CLI 2.0'yle bir VM'yi aaaCreate | Microsoft Docs"
description: "Nasıl toocreate kullanarak birden çok NIC ile VM hello Azure CLI 2.0 öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac0291a978e2c8682c69104915196cc6c4fcf8dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-20"></a><span data-ttu-id="d0267-103">Bir VM ile birden çok NIC hello Azure CLI 2.0 kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0267-103">Create a VM with multiple NICs using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="d0267-104">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d0267-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="d0267-105">Bu makalede, kullanarak yer almaktadır hello yerine çoğu yeni dağıtımlar için Microsoft önerir hello Resource Manager dağıtım modeli [Klasik dağıtım modeli](virtual-network-deploy-multinic-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d0267-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

## <span data-ttu-id="d0267-106"><a name="create"></a>Merhaba VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0267-106"><a name="create"></a>Create hello VM</span></span>

<span data-ttu-id="d0267-107">Hello Azure CLI 2.0 (Bu makalede) veya hello kullanarak bu görevi tamamlayabilirsiniz [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d0267-107">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md).</span></span> <span data-ttu-id="d0267-108">Merhaba değerleri "" Merhaba senaryodan ayarlarla kaynakları izleyin hello adımları hello değişkenleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d0267-108">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="d0267-109">Ortamınız için uygun şekilde Hello değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d0267-109">Change hello values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="d0267-110">Merhaba yüklemek [Azure CLI 2.0](/cli/azure/install-az-cli2) , zaten yüklü değilse.</span><span class="sxs-lookup"><span data-stu-id="d0267-110">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="d0267-111">Merhaba hello adımları tamamlayarak Linux VM'ler için bir SSH ortak ve özel anahtar çifti oluşturma [Linux VM'ler için bir SSH ortak ve özel anahtar çifti oluşturma](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d0267-111">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="d0267-112">Oturum açma hello komutuyla bir komut kabuğu'ndan `az login`.</span><span class="sxs-lookup"><span data-stu-id="d0267-112">From a command shell, login with hello command `az login`.</span></span>
4. <span data-ttu-id="d0267-113">Bir Linux veya Mac bilgisayarda aşağıdaki hello komut dosyası çalıştırarak Hello VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d0267-113">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="d0267-114">Merhaba betiği oluşturur bir kaynak grubu, bir sanal ağ (VNet) iki alt ağı, iki NIC ve hello iki NIC ile VM ile bağlı tooit.</span><span class="sxs-lookup"><span data-stu-id="d0267-114">hello script creates a resource group, one virtual network (VNet) with two subnets, two NICs, and a VM with hello two NICs attached tooit.</span></span> <span data-ttu-id="d0267-115">Merhaba NIC'ler biri bağlı tooone alt ağı ve bir statik genel ve özel IP adresi atanır.</span><span class="sxs-lookup"><span data-stu-id="d0267-115">One of hello NICs is connected tooone subnet and is assigned a static public and private IP address.</span></span> <span data-ttu-id="d0267-116">Merhaba diğer NIC bağlı toohello diğer alt ağıdır ve özel bir statik IP adresi ve ortak IP adresi atanır.</span><span class="sxs-lookup"><span data-stu-id="d0267-116">hello other NIC is connected toohello other subnet and is assigned a static private IP address and no public IP address.</span></span> <span data-ttu-id="d0267-117">Merhaba NIC, ortak IP adresi, sanal ağ ve VM kaynakları tüm bulunmalıdır hello aynı konumu ve abonelik.</span><span class="sxs-lookup"><span data-stu-id="d0267-117">hello NIC, public IP address, virtual network, and VM resources must all exist in hello same location and subscription.</span></span> <span data-ttu-id="d0267-118">Merhaba kaynakları tüm tooexist hello yok ancak aynı kaynak grubunda, yaptıkları komut dosyası izleyen hello.</span><span class="sxs-lookup"><span data-stu-id="d0267-118">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

```bash
#!/bin/sh

RgName="Multi-NIC-VM"
Location="westus"

# Create a resource group.
az group create \
--name $RgName \
--location $Location

# hello address is assigned toohello resource from a pool of IP adresses unique tooeach Azure region. 
# Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists
# hello ranges for each region.

PipName="PIP-WEB"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static

# Create a virtual network with one subnet

VnetName="VNet1"
VnetPrefix="10.0.0.0/16"
VnetSubnet1Name="Front-End"
VnetSubnet1Prefix="10.0.0.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnet1Name \
--subnet-prefix $VnetSubnet1Prefix

# Create a second subnet within hello VNet

VnetSubnet2Name="Back-end"
VnetSubnet2Prefix="10.0.1.0/24"
az network vnet subnet create \
--vnet-name $VnetName \
--resource-group $RgName \
--name $VnetSubnet2Name \
--address-prefix $VnetSubnet2Prefix

# Create a network interface connected tooone of hello subnets. hello NIC is assigned a single dynamic private and
# public IP address by default, but you can instead, assign static addresses, or no public IP address at all.
# You can also assign multiple private or public IP addresses tooeach NIC. toolearn more about IP addressing
# options for NICs, enter hello az network nic create -h command.

Nic1Name="NIC-FE"
PrivateIpAddress1="10.0.0.5"

az network nic create \
--name $Nic1Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress1 \
--public-ip-address $PipName

# Create a second network interface and connect it toohello other subnet. Though multiple NICs attached toohello same
# VM can be connected toodifferent subnets, hello subnets must all be within hello same VNet. Add additional NICs as necessary.

Nic2Name="NIC-BE"
PrivateIpAddress2="10.0.1.5"

az network nic create \
--name $Nic2Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet2Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress2

# Create a VM and attach hello two NICs.

VmName="WEB"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article. Not all VM sizes support
# more than one NIC, so be sure tooselect a VM size that supports hello number of NICs you want tooattach toohello VM.
# You must create hello VM with at least two NICs if you want tooadd more after VM creation. If you create a VM with
# only one NIC, you can't add additional NICs toohello VM after VM creation, regardless of how many NICs hello VM supports.
# hello VM size specified in hello following variable supports two NICs.

VmSize="Standard_DS2"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello output returned by entering the
# az vm image list command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file.

SshKeyValue="~/.ssh/id_rsa.pub"

# Before executing hello following command, add variable names of additional NICs you may have added toohello script that
# you want tooattach toohello VM. If creating a Windows VM, remove hello **ssh-key-value** line and you'll be prompted for
# hello password you want tooconfigure for hello VM.

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $Nic1Name $Nic2Name \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

<span data-ttu-id="d0267-119">Ayrıca toocreating iki NIC ile VM, hello komut dosyası oluşturur:</span><span class="sxs-lookup"><span data-stu-id="d0267-119">In addition toocreating a VM with two NICs, hello script creates:</span></span>
- <span data-ttu-id="d0267-120">Tek bir premium disk varsayılan olarak yönetilen, ancak oluşturabileceğiniz hello disk türü için diğer seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="d0267-120">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="d0267-121">Okuma hello [hello Azure CLI 2.0 kullanarak bir Linux VM oluşturma](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="d0267-121">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="d0267-122">Sanal ağı iki alt ağ ve tek bir ortak IP adresi.</span><span class="sxs-lookup"><span data-stu-id="d0267-122">A virtual network with two subnets and a single public IP address.</span></span> <span data-ttu-id="d0267-123">Alternatif olarak, kullanabileceğiniz *varolan* sanal ağ, alt ağ, NIC veya ortak IP adresi kaynakları.</span><span class="sxs-lookup"><span data-stu-id="d0267-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="d0267-124">nasıl toouse varolan ağ kaynakları yerine ek kaynakları oluşturma girin toolearn `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="d0267-124">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="d0267-125"><a name = "validate"></a>VM oluşturma ve NIC doğrula</span><span class="sxs-lookup"><span data-stu-id="d0267-125"><a name = "validate"></a>Validate VM creation and NICs</span></span>

1. <span data-ttu-id="d0267-126">Merhaba komutu girin `az resource list --resouce-group Multi-NIC-VM --output table` toosee hello komut dosyası tarafından oluşturulan hello kaynakların listesi.</span><span class="sxs-lookup"><span data-stu-id="d0267-126">Enter hello command `az resource list --resouce-group Multi-NIC-VM --output table` toosee a list of hello resources created by hello script.</span></span> <span data-ttu-id="d0267-127">Çıktı döndürülen hello altı kaynakları olmalıdır: iki NIC, bir disk, bir ortak IP adresi, bir sanal ağ ve bir sanal makine.</span><span class="sxs-lookup"><span data-stu-id="d0267-127">There should be six resources in hello returned output: Two NICs, one disk, one public IP address, one virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="d0267-128">Merhaba komutu girin `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`.</span><span class="sxs-lookup"><span data-stu-id="d0267-128">Enter hello command `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`.</span></span> <span data-ttu-id="d0267-129">Çıktı döndürülen hello hello değeri Not **IPADDRESS** ve o hello değerini **Publicıpallocationmethod** olan *statik*.</span><span class="sxs-lookup"><span data-stu-id="d0267-129">In hello returned output, note hello value of **IpAddress** and that hello value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="d0267-130">Merhaba <> kaldırmak komutu aşağıdaki hello çalıştırmadan önce değiştirmek *kullanıcı adı* hello için kullanılan hello adla **kullanıcı adı** hello komut dosyası ve değiştirme değişkeni *IPADDRESS* hello ile **IPADDRESS** hello önceki adımdaki.</span><span class="sxs-lookup"><span data-stu-id="d0267-130">Before running hello following command, remove hello <>, replace *Username* with hello name you used for hello **Username** variable in hello script, and replace *ipAddress* with hello **ipAddress** from hello previous step.</span></span> <span data-ttu-id="d0267-131">Çalışma hello şu komutu tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span><span class="sxs-lookup"><span data-stu-id="d0267-131">Run hello following command tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 
4. <span data-ttu-id="d0267-132">Merhaba toohello VM bağlandıktan sonra çalıştırmak `sudo ifconfig` komutu toosee *eth0* ve *eth1* arabirimleri.</span><span class="sxs-lookup"><span data-stu-id="d0267-132">Once connected toohello VM, run hello `sudo ifconfig` command toosee *eth0* and *eth1* interfaces.</span></span> <span data-ttu-id="d0267-133">Her NIC'nin hello Azure DHCP sunucuları tarafından hello komut dosyasında belirtilen hello statik özel IP adresleri atanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d0267-133">Each NIC has been assigned hello static private IP addresses specified in hello script by hello Azure DHCP servers.</span></span> <span data-ttu-id="d0267-134">Merhaba toohello NIC'ler atanan IP ve MAC adreslerinin VM silinmiş hello kadar değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="d0267-134">hello IP and MAC addresses assigned toohello NICs do not change until hello VM is deleted.</span></span> <span data-ttu-id="d0267-135">Bağlantı toohello bilgisayar devre dışı bırakabilirsiniz gibi bir işletim sistemi içinde IP adresleme değiştirmemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="d0267-135">We recommend that you do not change IP addressing within an operating system, as it can disable connectivity toohello computer.</span></span> <span data-ttu-id="d0267-136">Ağ adresi çevrilen tooand hello özel IP adresinden hello Azure altyapısı tarafından oldukları gibi ortak IP adresleri hello işletim sistemi içinde görünmez.</span><span class="sxs-lookup"><span data-stu-id="d0267-136">Public IP addresses do not appear within hello operating system, as they are network address translated tooand from hello private IP address by hello Azure infrastructure.</span></span>

## <span data-ttu-id="d0267-137"><a name= "clean-up"></a>Merhaba VM ve ilişkili kaynakları Kaldır</span><span class="sxs-lookup"><span data-stu-id="d0267-137"><a name= "clean-up"></a>Remove hello VM and associated resources</span></span>

<span data-ttu-id="d0267-138">Üretimde kullanmaz, bu alıştırmada oluşturulan hello kaynakları silmeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="d0267-138">It's recommended that you delete hello resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="d0267-139">Sağlanan sürece ücretler, VM, genel IP adresi ve disk kaynakları uygulanır.</span><span class="sxs-lookup"><span data-stu-id="d0267-139">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="d0267-140">Bu alıştırmada, aşağıdaki adımları tam hello sırasında oluşturulan tooremove hello kaynakları:</span><span class="sxs-lookup"><span data-stu-id="d0267-140">tooremove hello resources created during this exercise, complete hello following steps:</span></span>
1. <span data-ttu-id="d0267-141">Merhaba çalıştırmak hello kaynak grubunda tooview hello kaynakları `az resource list --resource-group Multi-NIC-VM` komutu.</span><span class="sxs-lookup"><span data-stu-id="d0267-141">tooview hello resources in hello resource group, run hello `az resource list --resource-group Multi-NIC-VM` command.</span></span>
2. <span data-ttu-id="d0267-142">Bu makalede hello komut dosyası tarafından oluşturulan hello kaynakları dışında hello kaynak grubunda hiç kaynak yok onaylayın.</span><span class="sxs-lookup"><span data-stu-id="d0267-142">Confirm there are no resources in hello resource group, other than hello resources created by hello script in this article.</span></span> 
3. <span data-ttu-id="d0267-143">tüm kaynaklar hello çalıştırmak Bu alıştırmada oluşturulan toodelete `az group delete --name Multi-NIC-VM` komutu.</span><span class="sxs-lookup"><span data-stu-id="d0267-143">toodelete all resources created in this exercise, run hello `az group delete --name Multi-NIC-VM` command.</span></span> <span data-ttu-id="d0267-144">Merhaba komut hello kaynak grubu ve içerdiği tüm hello kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="d0267-144">hello command deletes hello resource group and all hello resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0267-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d0267-145">Next steps</span></span>

<span data-ttu-id="d0267-146">Herhangi bir ağ trafiği, bu makaledeki VM oluşturulan hello gelen tooand akabilir.</span><span class="sxs-lookup"><span data-stu-id="d0267-146">Any network traffic can flow tooand from hello VM created in this article.</span></span> <span data-ttu-id="d0267-147">Bir NSG içinde her ağ arabirimi, her alt ağ ya da her ikisini de tooand akabilir hello trafiğini sınırlandırmak gelen ve giden kurallar tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0267-147">You can define inbound and outbound rules within an NSG that limit hello traffic that can flow tooand from each network interface, each subnet, or both.</span></span> <span data-ttu-id="d0267-148">Merhaba okuma Nsg'ler hakkında daha fazla toolearn [NSG genel bakış](virtual-networks-nsg.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="d0267-148">toolearn more about NSGs, read hello [NSG overview](virtual-networks-nsg.md) article.</span></span>
