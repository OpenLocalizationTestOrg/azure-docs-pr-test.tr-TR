---
title: bir statik genel IP adresi - Azure CLI 2.0'yle bir VM'yi aaaCreate | Microsoft Docs
description: "Nasıl toocreate ile bir statik genel IP adresini kullanarak bir VM hello Azure komut satırı arabirimi (CLI) 2.0 öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 55bc21b0-2a45-4943-a5e7-8d785d0d015c
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486060463486462dd8336734a7ad23c4a2cba452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-cli-20"></a><span data-ttu-id="d19cd-103">Hello Azure CLI 2.0 kullanarak bir statik genel IP adresiyle bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="d19cd-103">Create a VM with a static public IP address using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d19cd-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="d19cd-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="d19cd-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d19cd-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="d19cd-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d19cd-106">Azure CLI 2.0</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="d19cd-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d19cd-107">Azure CLI 1.0</span></span>](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [<span data-ttu-id="d19cd-108">Şablon</span><span class="sxs-lookup"><span data-stu-id="d19cd-108">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="d19cd-109">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="d19cd-109">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

<span data-ttu-id="d19cd-110">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d19cd-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="d19cd-111">Bu makalede, Microsoft hello Klasik dağıtım modeli yerine çoğu yeni dağıtımlar için önerir hello Resource Manager dağıtım modeli kullanılarak kapsar.</span><span class="sxs-lookup"><span data-stu-id="d19cd-111">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <span data-ttu-id="d19cd-112"><a name = "create"></a>Merhaba VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="d19cd-112"><a name = "create"></a>Create hello VM</span></span>

<span data-ttu-id="d19cd-113">Hello Azure CLI 2.0 (Bu makalede) veya hello kullanarak bu görevi tamamlayabilirsiniz [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d19cd-113">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span></span> <span data-ttu-id="d19cd-114">Merhaba değerleri "" Merhaba senaryodan ayarlarla kaynakları izleyin hello adımları hello değişkenleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d19cd-114">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="d19cd-115">Ortamınız için uygun şekilde Hello değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d19cd-115">Change hello values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="d19cd-116">Merhaba yüklemek [Azure CLI 2.0](/cli/azure/install-az-cli2) , zaten yüklü değilse.</span><span class="sxs-lookup"><span data-stu-id="d19cd-116">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="d19cd-117">Merhaba hello adımları tamamlayarak Linux VM'ler için bir SSH ortak ve özel anahtar çifti oluşturma [Linux VM'ler için bir SSH ortak ve özel anahtar çifti oluşturma](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d19cd-117">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="d19cd-118">Oturum açma hello komutuyla bir komut kabuğu'ndan `az login`.</span><span class="sxs-lookup"><span data-stu-id="d19cd-118">From a command shell, login with hello command `az login`.</span></span>
4. <span data-ttu-id="d19cd-119">Bir Linux veya Mac bilgisayarda aşağıdaki hello komut dosyası çalıştırarak Hello VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d19cd-119">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="d19cd-120">Hello Azure genel IP adresi, sanal ağ, ağ arabirimi ve VM kaynakları tüm bulunmalıdır hello aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="d19cd-120">hello Azure public IP address, virtual network, network interface, and VM resources must all exist in hello same location.</span></span> <span data-ttu-id="d19cd-121">Merhaba kaynakları tüm tooexist hello yok ancak aynı kaynak grubunda, yaptıkları komut dosyası izleyen hello.</span><span class="sxs-lookup"><span data-stu-id="d19cd-121">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

```bash
RgName="IaaSStory"
Location="westus"

# Create a resource group.

az group create \
--name $RgName \
--location $Location

# Create a public IP address resource with a static IP address using hello --allocation-method Static option.
# If you do not specify this option, hello address is allocated dynamically. hello address is assigned toothe
# resource from a pool of IP adresses unique tooeach Azure region. hello DnsName must be unique within the
# Azure location it's created in. Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653#
# that lists hello ranges for each region.

PipName="PIPWEB1"
DnsName="iaasstoryws1"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static \
--dns-name $DnsName

# Create a virtual network with one subnet

VnetName="TestVNet"
VnetPrefix="192.168.0.0/16"
SubnetName="FrontEnd"
SubnetPrefix="192.168.1.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $SubnetName \
--subnet-prefix $SubnetPrefix

# Create a network interface connected toohello VNet with a static private IP address and associate hello public IP address
# resource toohello NIC.

NicName="NICWEB1"
PrivateIpAddress="192.168.1.101"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $SubnetName \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress \
--public-ip-address $PipName

# Create a new VM with hello NIC

VmName="WEB1"

# Replace hello value for hello VmSize variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article.
VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable with a value for *urn* from hello output returned by entering
# hello `az vm image list` command. 

OsImage="credativ:Debian:8:latest"
Username='adminuser'

# Replace hello following value with hello path tooyour public key file.
SshKeyValue="~/.ssh/id_rsa.pub"

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $NicName \
--admin-username $Username \
--ssh-key-value $SshKeyValue
# If creating a Windows VM, remove hello previous line and you'll be prompted for hello password you want tooconfigure for hello VM.
```

<span data-ttu-id="d19cd-122">Ayrıca toocreating VM, hello komut dosyası oluşturur:</span><span class="sxs-lookup"><span data-stu-id="d19cd-122">In addition toocreating a VM, hello script creates:</span></span>
- <span data-ttu-id="d19cd-123">Tek bir premium disk varsayılan olarak yönetilen, ancak oluşturabileceğiniz hello disk türü için diğer seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="d19cd-123">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="d19cd-124">Okuma hello [hello Azure CLI 2.0 kullanarak bir Linux VM oluşturma](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="d19cd-124">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="d19cd-125">Sanal ağ, alt ağ, NIC ve ortak IP adresi kaynakları.</span><span class="sxs-lookup"><span data-stu-id="d19cd-125">Virtual network, subnet, NIC, and public IP address resources.</span></span> <span data-ttu-id="d19cd-126">Alternatif olarak, kullanabileceğiniz *varolan* sanal ağ, alt ağ, NIC veya ortak IP adresi kaynakları.</span><span class="sxs-lookup"><span data-stu-id="d19cd-126">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="d19cd-127">nasıl toouse varolan ağ kaynakları yerine ek kaynakları oluşturma girin toolearn `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="d19cd-127">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="d19cd-128"><a name = "validate"></a>VM oluşturma ve genel IP adresi doğrula</span><span class="sxs-lookup"><span data-stu-id="d19cd-128"><a name = "validate"></a>Validate VM creation and public IP address</span></span>

1. <span data-ttu-id="d19cd-129">Merhaba komutu girin `az resource list --resouce-group IaaSStory --output table` toosee hello komut dosyası tarafından oluşturulan hello kaynakların listesi.</span><span class="sxs-lookup"><span data-stu-id="d19cd-129">Enter hello command `az resource list --resouce-group IaaSStory --output table` toosee a list of hello resources created by hello script.</span></span> <span data-ttu-id="d19cd-130">Çıktı döndürülen hello beş kaynakları olmalıdır: ağ arabirimi, disk, genel IP adresi, sanal ağ ve bir sanal makine.</span><span class="sxs-lookup"><span data-stu-id="d19cd-130">There should be five resources in hello returned output: network interface, disk, public IP address, virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="d19cd-131">Merhaba komutu girin `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span><span class="sxs-lookup"><span data-stu-id="d19cd-131">Enter hello command `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span></span> <span data-ttu-id="d19cd-132">Çıktı döndürülen hello hello değeri Not **IPADDRESS** ve o hello değerini **Publicıpallocationmethod** olan *statik*.</span><span class="sxs-lookup"><span data-stu-id="d19cd-132">In hello returned output, note hello value of **IpAddress** and that hello value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="d19cd-133">Komutu aşağıdaki hello yürütmeden önce hello <> kaldırmak, değiştirmek *kullanıcıadı* hello için kullanılan hello adla **kullanıcı adı** hello komut dosyası ve değiştirme değişkeni *IPADDRESS* hello ile **IPADDRESS** hello önceki adımdaki.</span><span class="sxs-lookup"><span data-stu-id="d19cd-133">Before executing hello following command, remove hello <>, replace *Username* with hello name you used for hello **Username** variable in hello script, and replace *ipAddress* with hello **ipAddress** from hello previous step.</span></span> <span data-ttu-id="d19cd-134">Çalışma hello şu komutu tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span><span class="sxs-lookup"><span data-stu-id="d19cd-134">Run hello following command tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 

## <span data-ttu-id="d19cd-135"><a name= "clean-up"></a>Merhaba VM ve ilişkili kaynakları Kaldır</span><span class="sxs-lookup"><span data-stu-id="d19cd-135"><a name= "clean-up"></a>Remove hello VM and associated resources</span></span>

<span data-ttu-id="d19cd-136">Üretimde kullanmaz, bu alıştırmada oluşturulan hello kaynakları silmeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="d19cd-136">It's recommended that you delete hello resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="d19cd-137">Sağlanan sürece ücretler, VM, genel IP adresi ve disk kaynakları uygulanır.</span><span class="sxs-lookup"><span data-stu-id="d19cd-137">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="d19cd-138">Bu alıştırmada, aşağıdaki adımları tam hello sırasında oluşturulan tooremove hello kaynakları:</span><span class="sxs-lookup"><span data-stu-id="d19cd-138">tooremove hello resources created during this exercise, complete hello following steps:</span></span>

1. <span data-ttu-id="d19cd-139">Merhaba çalıştırmak hello kaynak grubunda tooview hello kaynakları `az resource list --resource-group IaaSStory` komutu.</span><span class="sxs-lookup"><span data-stu-id="d19cd-139">tooview hello resources in hello resource group, run hello `az resource list --resource-group IaaSStory` command.</span></span>
2. <span data-ttu-id="d19cd-140">Bu makalede hello komut dosyası tarafından oluşturulan hello kaynakları dışında hello kaynak grubunda hiç kaynak yok onaylayın.</span><span class="sxs-lookup"><span data-stu-id="d19cd-140">Confirm there are no resources in hello resource group, other than hello resources created by hello script in this article.</span></span> 
3. <span data-ttu-id="d19cd-141">tüm kaynaklar hello çalıştırmak Bu alıştırmada oluşturulan toodelete `az group delete -n IaaSStory` komutu.</span><span class="sxs-lookup"><span data-stu-id="d19cd-141">toodelete all resources created in this exercise, run hello `az group delete -n IaaSStory` command.</span></span> <span data-ttu-id="d19cd-142">Merhaba komut hello kaynak grubu ve içerdiği tüm hello kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="d19cd-142">hello command deletes hello resource group and all hello resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d19cd-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d19cd-143">Next steps</span></span>

<span data-ttu-id="d19cd-144">Herhangi bir ağ trafiği, bu makaledeki VM oluşturulan hello gelen tooand akabilir.</span><span class="sxs-lookup"><span data-stu-id="d19cd-144">Any network traffic can flow tooand from hello VM created in this article.</span></span> <span data-ttu-id="d19cd-145">Bir NSG içinde hello ağ arabirimi, hello alt ağ ya da her ikisini de tooand akabilir hello trafiğini sınırlandırmak gelen ve giden kurallar tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d19cd-145">You can define inbound and outbound rules within an NSG that limit hello traffic that can flow tooand from hello network interface, hello subnet, or both.</span></span> <span data-ttu-id="d19cd-146">Merhaba okuma Nsg'ler hakkında daha fazla toolearn [NSG genel bakış](virtual-networks-nsg.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="d19cd-146">toolearn more about NSGs, read hello [NSG overview](virtual-networks-nsg.md) article.</span></span>
