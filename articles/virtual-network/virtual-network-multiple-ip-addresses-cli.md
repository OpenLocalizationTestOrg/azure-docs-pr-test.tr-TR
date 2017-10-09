---
title: "hello Azure CLI 2.0 kullanarak birden çok IP adresleriyle aaaVM | Microsoft Docs"
description: "Nasıl tooassign birden çok IP adresleri öğrenin tooa kullanarak sanal makine hello Azure CLI 2.0 | Resource Manager."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 15efd853cc7c31bacb64ed052dabedd3fe4d3079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-cli-20"></a><span data-ttu-id="84504-103">Hello Azure CLI 2.0 kullanarak toovirtual makineleri birden çok IP adresi atayın</span><span class="sxs-lookup"><span data-stu-id="84504-103">Assign multiple IP addresses toovirtual machines using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="84504-104">Bu makalede nasıl toocreate hello Azure Resource Manager dağıtım modeli kullanılarak aracılığıyla sanal makine (VM) hello Azure CLI 2.0 açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="84504-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using hello Azure CLI 2.0.</span></span> <span data-ttu-id="84504-105">Birden çok IP adresi hello Klasik dağıtım modeli aracılığıyla oluşturulan tooresources atanamaz.</span><span class="sxs-lookup"><span data-stu-id="84504-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="84504-106">Merhaba okuma Azure dağıtım modelleri hakkında daha fazla toolearn [dağıtım modellerini anlama](../resource-manager-deployment-model.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="84504-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="84504-107"><a name = "create"></a>Birden çok IP adresiyle bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="84504-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="84504-108">Hello Azure CLI 2.0 (Bu makalede) veya hello kullanarak bu görevi tamamlayabilirsiniz [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="84504-108">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span></span> <span data-ttu-id="84504-109">Ortamınız için uygun şekilde Hello değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="84504-109">Change hello values, as appropriate, for your environment.</span></span> <span data-ttu-id="84504-110">izleyin hello adımlarda hello senaryosunda açıklandığı şekilde nasıl toocreate örneği VM ile birden çok IP adresleri, açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="84504-110">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="84504-111">Değişken değerleri değiştirmek "" ve IP adresi türleri, uygulamanız için gerekli olarak.</span><span class="sxs-lookup"><span data-stu-id="84504-111">Change variable values in "" and IP address types as required for your implementation.</span></span> 

1. <span data-ttu-id="84504-112">Merhaba yüklemek [Azure CLI 2.0](/cli/azure/install-az-cli2) , zaten yüklü değilse.</span><span class="sxs-lookup"><span data-stu-id="84504-112">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="84504-113">Merhaba hello adımları tamamlayarak Linux VM'ler için bir SSH ortak ve özel anahtar çifti oluşturma [Linux VM'ler için bir SSH ortak ve özel anahtar çifti oluşturma](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="84504-113">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="84504-114">Oturum açma hello komutuyla bir komut kabuğu'ndan `az login` ve kullanmakta olduğunuz hello abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="84504-114">From a command shell, login with hello command `az login` and select hello subscription you're using.</span></span>
4. <span data-ttu-id="84504-115">Bir Linux veya Mac bilgisayarda aşağıdaki hello komut dosyası çalıştırarak Hello VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="84504-115">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="84504-116">Merhaba komut dosyası bir kaynak grubu, bir sanal ağ (VNet), bir NIC üç IP yapılandırmaları olan ve bir VM ile Merhaba iki bağlı NIC tooit oluşturur.</span><span class="sxs-lookup"><span data-stu-id="84504-116">hello script creates a resource group, one virtual network (VNet), one NIC with three IP configurations, and a VM with hello two NICs attached tooit.</span></span> <span data-ttu-id="84504-117">Merhaba NIC, ortak IP adresi, sanal ağ ve VM kaynakları tüm bulunmalıdır hello aynı konumu ve abonelik.</span><span class="sxs-lookup"><span data-stu-id="84504-117">hello NIC, public IP address, virtual network, and VM resources must all exist in hello same location and subscription.</span></span> <span data-ttu-id="84504-118">Merhaba kaynakları tüm tooexist hello yok ancak aynı kaynak grubunda, yaptıkları komut dosyası izleyen hello.</span><span class="sxs-lookup"><span data-stu-id="84504-118">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using hello `--allocation-method Static` option. If you
# do not specify this option, hello address is allocated dynamically. hello address is assigned toohello resource from a pool
# of IP adresses unique tooeach Azure region. Download and view hello file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists hello ranges for each region.

PipName="myPublicIP"

# This name must be unique within an Azure location.
DnsName="myDNSName"

az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--dns-name $DnsName\
--allocation-method Static

# Create a virtual network with one subnet

VnetName="myVnet"
VnetPrefix="10.0.0.0/16"
VnetSubnetName="mySubnet"
VnetSubnetPrefix="10.0.0.0/24"

az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnetName \
--subnet-prefix $VnetSubnetPrefix

# Create a network interface connected toohello subnet and associate hello public IP address tooit. Azure will create the
# first IP configuration with a static private IP address and will associate hello public IP address resource tooit.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it toohello NIC. This configuration has a
# static public IP address and a static private IP address.

az network public-ip create \
--resource-group $RgName \
--location $Location \
--name myPublicIP2 \
--dns-name mypublicdns2 \
--allocation-method Static

az network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--name IPConfig-2 \
--private-ip-address 10.0.0.5 \
--public-ip-name myPublicIP2

# Create a third IP configuration, and associate it toohello NIC. This configuration has  static private IP address and # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations
# tooany NIC in a VM. toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach hello NIC.

VmName="myVm"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. hello script fails if hello VM size
# is not supported in hello location you select. Run hello `azure vm sizes --location estcentralus` command tooget a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file. If you're creating a Windows VM, remove hello following
# line and you'll be prompted for hello password you want tooconfigure for hello VM.

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
```

<span data-ttu-id="84504-119">Ayrıca toocreating 3 IP yapılandırmaları olan bir NIC ile VM, hello komut dosyası oluşturur:</span><span class="sxs-lookup"><span data-stu-id="84504-119">In addition toocreating a VM with a NIC with 3 IP configurations, hello script creates:</span></span>

- <span data-ttu-id="84504-120">Tek bir premium disk varsayılan olarak yönetilen, ancak oluşturabileceğiniz hello disk türü için diğer seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="84504-120">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="84504-121">Okuma hello [hello Azure CLI 2.0 kullanarak bir Linux VM oluşturma](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="84504-121">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="84504-122">Bir alt ağı ve iki genel IP adresine sahip bir sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="84504-122">A virtual network with one subnet and two public IP addresses.</span></span> <span data-ttu-id="84504-123">Alternatif olarak, kullanabileceğiniz *varolan* sanal ağ, alt ağ, NIC veya ortak IP adresi kaynakları.</span><span class="sxs-lookup"><span data-stu-id="84504-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="84504-124">nasıl toouse varolan ağ kaynakları yerine ek kaynakları oluşturma girin toolearn `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="84504-124">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

<span data-ttu-id="84504-125">Nominal bir ücret ortak IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="84504-125">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="84504-126">IP hakkında daha fazla adres fiyatlandırma toolearn okuma hello [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses) sayfası.</span><span class="sxs-lookup"><span data-stu-id="84504-126">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="84504-127">Bir abonelikte kullanılabilir genel IP adresleri sınırı toohello sayısı yoktur.</span><span class="sxs-lookup"><span data-stu-id="84504-127">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="84504-128">Merhaba okuma hello sınırları hakkında daha fazla toolearn [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) makalesi.</span><span class="sxs-lookup"><span data-stu-id="84504-128">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

<span data-ttu-id="84504-129">Merhaba VM oluşturulduktan sonra hello girin `az network nic show --name MyNic1 --resource-group myResourceGroup` komut tooview hello NIC yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="84504-129">After hello VM is created, enter hello `az network nic show --name MyNic1 --resource-group myResourceGroup` command tooview hello NIC configuration.</span></span> <span data-ttu-id="84504-130">Merhaba girin `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview hello IP yapılandırmaları listesini ilişkili toohello NIC</span><span class="sxs-lookup"><span data-stu-id="84504-130">Enter hello `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview a list of hello IP configurations associated toohello NIC.</span></span>

<span data-ttu-id="84504-131">Ekle hello özel IP adresleri toohello VM işletim sistemi işletim sisteminizin hello hello adımları tamamlayarak [eklemek IP adresleri tooa VM işletim sistemi](#os-config) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="84504-131">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="84504-132"><a name="add"></a>IP adreslerini tooa VM ekleme</span><span class="sxs-lookup"><span data-stu-id="84504-132"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="84504-133">NIC izleyin hello adımları tamamlayarak varolan ek özel ve genel IP adresleri tooan ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84504-133">You can add additional private and public IP addresses tooan existing NIC by completing hello steps that follow.</span></span> <span data-ttu-id="84504-134">Hello örnekleri derleme sırasında hello [senaryo](#Scenario) bu makalede açıklanan.</span><span class="sxs-lookup"><span data-stu-id="84504-134">hello examples build upon hello [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="84504-135">Bir komut kabuğu ve bu bölümdeki adımları tek bir oturum içinde kalan tam hello açın.</span><span class="sxs-lookup"><span data-stu-id="84504-135">Open a command shell and complete hello remaining steps in this section within a single session.</span></span> <span data-ttu-id="84504-136">Azure CLI yüklenmiş ve yapılandırılmış zaten sahip değilseniz, tam hello hello adımları [Azure CLI 2.0 yüklemesi](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) makale ve oturum açma tooyour hello Azure hesabı `az-login` komutu.</span><span class="sxs-lookup"><span data-stu-id="84504-136">If you don't already have Azure CLI installed and configured, complete hello steps in hello [Azure CLI 2.0 installation](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) article and login tooyour Azure account with hello `az-login` command.</span></span>

2. <span data-ttu-id="84504-137">Aşağıdaki bölümlerde, gereksinimlerinize göre hello Hello adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="84504-137">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    <span data-ttu-id="84504-138">**Özel bir IP adresi Ekle**</span><span class="sxs-lookup"><span data-stu-id="84504-138">**Add a private IP address**</span></span>
    
    <span data-ttu-id="84504-139">özel bir IP adresi tooa NIC tooadd, izleyen hello komutunu kullanarak bir IP yapılandırması oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="84504-139">tooadd a private IP address tooa NIC, you must create an IP configuration using hello command that follows.</span></span> <span data-ttu-id="84504-140">Merhaba statik IP adresi hello alt ağ için kullanılmayan bir adres olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="84504-140">hello static IP address must be an unused address for hello subnet.</span></span>

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    <span data-ttu-id="84504-141">Benzersiz yapılandırma adları ve özel IP adresleri (yapılandırmaları statik IP adresleriyle) kullanarak gereksinim duyduğunuz kadar çok yapılandırmaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="84504-141">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="84504-142">**Bir ortak IP adresi Ekle**</span><span class="sxs-lookup"><span data-stu-id="84504-142">**Add a public IP address**</span></span>
    
    <span data-ttu-id="84504-143">Bir ortak IP adresi tooeither ilişkilendirerek eklenen yeni bir IP yapılandırması veya var olan bir IP yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="84504-143">A public IP address is added by associating it tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="84504-144">Gereksinim duyduğunuz kadar izleyin, hello bölümlerden biri hello adımlarını tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="84504-144">Complete hello steps in one of hello sections that follow, as you require.</span></span>

    <span data-ttu-id="84504-145">Nominal bir ücret ortak IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="84504-145">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="84504-146">IP hakkında daha fazla adres fiyatlandırma toolearn okuma hello [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses) sayfası.</span><span class="sxs-lookup"><span data-stu-id="84504-146">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="84504-147">Bir abonelikte kullanılabilir genel IP adresleri sınırı toohello sayısı yoktur.</span><span class="sxs-lookup"><span data-stu-id="84504-147">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="84504-148">Merhaba okuma hello sınırları hakkında daha fazla toolearn [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) makalesi.</span><span class="sxs-lookup"><span data-stu-id="84504-148">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    - <span data-ttu-id="84504-149">**Merhaba kaynak tooa yeni IP yapılandırmasını ilişkilendirin**</span><span class="sxs-lookup"><span data-stu-id="84504-149">**Associate hello resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="84504-150">Yeni bir IP yapılandırmasında bir ortak IP adresi eklediğinizde, tüm IP yapılandırmalarının özel bir IP adresi olması gerektiği için özel bir IP adresi eklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="84504-150">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="84504-151">Varolan bir ortak IP adresi kaynağı ekleyin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="84504-151">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="84504-152">toocreate yeni bir hello aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="84504-152">toocreate a new one, enter hello following command:</span></span>
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        <span data-ttu-id="84504-153">Özel statik IP adresi ve ilişkili hello yeni bir IP yapılandırmasıyla toocreate *myPublicIP3* genel IP adresi kaynak, komutu aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="84504-153">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIP3* public IP address resource, enter hello following command:</span></span>

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - <span data-ttu-id="84504-154">**İlişkilendirme hello kaynak tooan mevcut IP yapılandırması** genel bir IP adresi kaynağı yalnızca zaten ilişkili olmayan ilişkili tooan IP yapılandırması olabilir.</span><span class="sxs-lookup"><span data-stu-id="84504-154">**Associate hello resource tooan existing IP configuration** A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="84504-155">Komutu aşağıdaki hello girerek bir IP yapılandırması ilişkili bir ortak IP adresi olup olmadığını belirleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="84504-155">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        <span data-ttu-id="84504-156">Çıkış döndürdü:</span><span class="sxs-lookup"><span data-stu-id="84504-156">Returned output:</span></span>
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        <span data-ttu-id="84504-157">Merhaba itibaren **PublicIpAddressId** sütunu için *IpConfig 3* olan hello boş çıkış, hiçbir ortak IP adresi kaynağı şu anda ilişkili tooit.</span><span class="sxs-lookup"><span data-stu-id="84504-157">Since hello **PublicIpAddressId** column for *IpConfig-3* is blank in hello output, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="84504-158">Bir var olan ortak IP adresi kaynak tooIpConfig-3 ekleyin veya komut toocreate bir aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="84504-158">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        <span data-ttu-id="84504-159">Tooassociate hello ortak IP adresi adlı kaynak toohello mevcut IP yapılandırması komutu aşağıdaki hello girin *IPConfig 3*:</span><span class="sxs-lookup"><span data-stu-id="84504-159">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IPConfig-3*:</span></span>
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. <span data-ttu-id="84504-160">Girerek NIC hello komutu aşağıdaki toohello atanan kaynak kimlikleri görünüm hello özel IP adresleri ve hello genel IP adresi:</span><span class="sxs-lookup"><span data-stu-id="84504-160">View hello private IP addresses and hello public IP address resource Ids assigned toohello NIC by entering hello following command:</span></span>

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    <span data-ttu-id="84504-161">Çıkış döndürdü:</span><span class="sxs-lookup"><span data-stu-id="84504-161">Returned output:</span></span> <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. <span data-ttu-id="84504-162">Merhaba hello yönergeleri takip ederek toohello NIC toohello VM işletim sistemi eklenen hello özel IP adresleri ekleme [eklemek IP adresleri tooa VM işletim sistemi](#os-config) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="84504-162">Add hello private IP addresses you added toohello NIC toohello VM operating system by following hello instructions in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="84504-163">Merhaba ortak IP adresleri toohello işletim sistemi eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="84504-163">Do not add hello public IP addresses toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
