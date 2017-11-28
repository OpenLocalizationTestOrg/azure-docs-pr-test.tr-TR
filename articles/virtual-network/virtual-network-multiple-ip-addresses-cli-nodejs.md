---
title: "hello Azure CLI 1.0 kullanarak birden çok IP adresleriyle aaaVM | Microsoft Docs"
description: "Nasıl tooassign birden çok IP adresleri öğrenin tooa kullanarak sanal makine hello Azure CLI 1.0 | Resource Manager."
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
ms.openlocfilehash: 83ad48e67309fb21d5aca967d4f2c01afdc0b5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-azure-cli-10"></a><span data-ttu-id="73b23-103">Azure CLI 1.0 kullanarak toovirtual makineleri birden çok IP adresi atayın</span><span class="sxs-lookup"><span data-stu-id="73b23-103">Assign multiple IP addresses toovirtual machines using Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="73b23-104">Bu makalede nasıl toocreate hello Azure Resource Manager dağıtım modeli kullanılarak aracılığıyla sanal makine (VM) hello Azure CLI 1.0 açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="73b23-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using hello Azure CLI 1.0.</span></span> <span data-ttu-id="73b23-105">Birden çok IP adresi hello Klasik dağıtım modeli aracılığıyla oluşturulan tooresources atanamaz.</span><span class="sxs-lookup"><span data-stu-id="73b23-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="73b23-106">Merhaba okuma Azure dağıtım modelleri hakkında daha fazla toolearn [dağıtım modellerini anlama](../resource-manager-deployment-model.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="73b23-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="73b23-107"><a name = "create"></a>Birden çok IP adresiyle bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="73b23-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="73b23-108">Hello Azure CLI 1.0 (Bu makalede) veya hello kullanarak bu görevi tamamlayabilirsiniz [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span><span class="sxs-lookup"><span data-stu-id="73b23-108">You can complete this task using hello Azure CLI 1.0 (this article) or hello [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span></span> <span data-ttu-id="73b23-109">izleyin hello adımlarda hello senaryosunda açıklandığı şekilde nasıl toocreate örneği VM ile birden çok IP adresleri, açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="73b23-109">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="73b23-110">Değişken adları ve IP adresi türleri, uygulamanız için gerekli olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="73b23-110">Change variable names and IP address types as required for your implementation.</span></span>

1. <span data-ttu-id="73b23-111">Azure CLI 1.0 aşağıdaki hello tarafından adımları hello hello yükleyip [hello Azure CLI yükleyip](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) makalesi ve hello Azure hesabınızla oturum `azure-login` komutu.</span><span class="sxs-lookup"><span data-stu-id="73b23-111">Install and configure hello Azure CLI 1.0 by following hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account with hello `azure-login` command.</span></span>

2. <span data-ttu-id="73b23-112">Kaynak grubu oluşturun:</span><span class="sxs-lookup"><span data-stu-id="73b23-112">Create a resource group:</span></span>
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. <span data-ttu-id="73b23-113">Sanal ağ oluşturma:</span><span class="sxs-lookup"><span data-stu-id="73b23-113">Create a virtual network:</span></span>

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. <span data-ttu-id="73b23-114">Bir alt ağ hello sanal ağda oluşturun:</span><span class="sxs-lookup"><span data-stu-id="73b23-114">Create a subnet in hello virtual network:</span></span>

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. <span data-ttu-id="73b23-115">Merhaba VM için bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="73b23-115">Create  a storage account for hello VM.</span></span> <span data-ttu-id="73b23-116">Merhaba çalıştırmadan önce Değiştir komutu, aşağıdaki *mystorageaccount* benzersiz bir ada sahip.</span><span class="sxs-lookup"><span data-stu-id="73b23-116">Before running hello following command, replace *mystorageaccount* with a unique name.</span></span> <span data-ttu-id="73b23-117">Merhaba adının Azure'da benzersiz olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="73b23-117">hello name must be unique across Azure:</span></span>

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. <span data-ttu-id="73b23-118">Merhaba IP yapılandırmaları, bir NIC oluşturun ve hello IP yapılandırmaları toohello NIC atayın</span><span class="sxs-lookup"><span data-stu-id="73b23-118">Create hello IP configurations, a NIC, and assign hello IP configurations toohello NIC.</span></span> <span data-ttu-id="73b23-119">Eklemek, kaldırmak veya hello yapılandırmalarını gerektiği gibi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="73b23-119">You can add, remove, or change hello configurations as necessary.</span></span> <span data-ttu-id="73b23-120">aşağıdaki yapılandırmalar hello hello senaryoda açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="73b23-120">hello following configurations are described in hello scenario:</span></span>

    <span data-ttu-id="73b23-121">**Ipconfig-1**</span><span class="sxs-lookup"><span data-stu-id="73b23-121">**IPConfig-1**</span></span>

    <span data-ttu-id="73b23-122">Toocreate izleyin hello komutları girin:</span><span class="sxs-lookup"><span data-stu-id="73b23-122">Enter hello commands that follow toocreate:</span></span>

    - <span data-ttu-id="73b23-123">Bir statik genel IP adresi ile genel IP adresi kaynağı</span><span class="sxs-lookup"><span data-stu-id="73b23-123">A public IP address resource with a static public IP address</span></span>
    - <span data-ttu-id="73b23-124">Merhaba genel IP adresi ve statik bir özel IP adresi tooit atama bir NIC.</span><span class="sxs-lookup"><span data-stu-id="73b23-124">A NIC, assigning hello public IP address and a static private IP address tooit.</span></span>
    
    <span data-ttu-id="73b23-125">Değiştir *mypublicdns* hello Azure konumu içinde benzersiz bir ada sahip.</span><span class="sxs-lookup"><span data-stu-id="73b23-125">Replace *mypublicdns* with a name that is unique within hello Azure location.</span></span>

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > <span data-ttu-id="73b23-126">Nominal bir ücret ortak IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="73b23-126">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="73b23-127">IP hakkında daha fazla adres fiyatlandırma toolearn okuma hello [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses) sayfası.</span><span class="sxs-lookup"><span data-stu-id="73b23-127">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="73b23-128">Bir abonelikte kullanılabilir genel IP adresleri sınırı toohello sayısı yoktur.</span><span class="sxs-lookup"><span data-stu-id="73b23-128">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="73b23-129">Merhaba okuma hello sınırları hakkında daha fazla toolearn [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) makalesi.</span><span class="sxs-lookup"><span data-stu-id="73b23-129">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    <span data-ttu-id="73b23-130">**Ipconfig 2**</span><span class="sxs-lookup"><span data-stu-id="73b23-130">**IPConfig-2**</span></span>

     <span data-ttu-id="73b23-131">Yeni bir ortak IP adresi kaynağı ve bir statik genel IP adresi ve özel bir statik IP adresi ile yeni bir IP yapılandırması komutları toocreate aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="73b23-131">Enter hello following commands toocreate a new public IP address resource and a new IP configuration with a static public IP address and a static private IP address:</span></span>
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    <span data-ttu-id="73b23-132">**Ipconfig 3**</span><span class="sxs-lookup"><span data-stu-id="73b23-132">**IPConfig-3**</span></span>

    <span data-ttu-id="73b23-133">Aşağıdaki komutları toocreate özel bir statik IP adresi ve ortak IP adresi bir IP yapılandırmasıyla hello girin:</span><span class="sxs-lookup"><span data-stu-id="73b23-133">Enter hello following commands toocreate an IP configuration with a static private IP address and no public IP address:</span></span>

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    ><span data-ttu-id="73b23-134">Bu makalede tüm IP yapılandırmaları tooa atar ancak tek NIC, birden çok IP yapılandırmaları tooany bir sanal NIC de atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73b23-134">Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations tooany NIC in a VM.</span></span> <span data-ttu-id="73b23-135">toolearn toocreate birden çok NIC ile VM okuma nasıl oluşturma bir VM ile birden çok NIC makalesi hello.</span><span class="sxs-lookup"><span data-stu-id="73b23-135">toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs article.</span></span>

7. <span data-ttu-id="73b23-136">Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="73b23-136">Create a Linux VM</span></span> 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    <span data-ttu-id="73b23-137">toochange hello VM boyutu tooStandard DS2 v2, örneğin, özellik aşağıdaki hello eklemeniz yeterlidir `--vm-size Standard_DS3_v2` toohello `azure vm create` adım 6 komutu.</span><span class="sxs-lookup"><span data-stu-id="73b23-137">toochange hello VM size tooStandard DS2 v2, for example, simply add hello following property `--vm-size Standard_DS3_v2` toohello `azure vm create` command in step 6.</span></span>

8. <span data-ttu-id="73b23-138">Aşağıdaki komut tooview hello NIC hello girin ve ilişkili IP yapılandırmaları hello:</span><span class="sxs-lookup"><span data-stu-id="73b23-138">Enter hello following command tooview hello NIC and hello associated IP configurations:</span></span>

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. <span data-ttu-id="73b23-139">Ekle hello özel IP adresleri toohello VM işletim sistemi işletim sisteminizin hello hello adımları tamamlayarak [eklemek IP adresleri tooa VM işletim sistemi](#os-config) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="73b23-139">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="73b23-140"><a name="add"></a>IP adreslerini tooa VM ekleme</span><span class="sxs-lookup"><span data-stu-id="73b23-140"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="73b23-141">NIC izleyin hello adımları tamamlayarak varolan ek özel ve genel IP adresleri tooan ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73b23-141">You can add additional private and public IP addresses tooan existing NIC by completing hello steps that follow.</span></span> <span data-ttu-id="73b23-142">Hello örnekleri derleme sırasında hello [senaryo](#Scenario) bu makalede açıklanan.</span><span class="sxs-lookup"><span data-stu-id="73b23-142">hello examples build upon hello [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="73b23-143">Azure CLI ve bu bölümdeki adımları tek bir CLI oturumu içinde kalan tam hello açın.</span><span class="sxs-lookup"><span data-stu-id="73b23-143">Open Azure CLI and complete hello remaining steps in this section within a single CLI session.</span></span> <span data-ttu-id="73b23-144">Azure CLI yüklenmiş ve yapılandırılmış zaten sahip değilseniz, tam hello hello adımları [hello Azure CLI yükleyip](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) makalesi ve Azure hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="73b23-144">If you don't already have Azure CLI installed and configured, complete hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account.</span></span>

2. <span data-ttu-id="73b23-145">Aşağıdaki bölümlerde, gereksinimlerinize göre hello Hello adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="73b23-145">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    - <span data-ttu-id="73b23-146">**Özel bir IP adresi Ekle**</span><span class="sxs-lookup"><span data-stu-id="73b23-146">**Add a private IP address**</span></span>
    
        <span data-ttu-id="73b23-147">özel bir IP adresi tooa NIC tooadd, aşağıdaki hello komutu kullanarak IP yapılandırması oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="73b23-147">tooadd a private IP address tooa NIC, you must create an IP configuration using hello command below.</span></span> <span data-ttu-id="73b23-148">Merhaba statik adresi hello alt ağ için kullanılmayan bir adres olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="73b23-148">hello static address must be an unused address for hello subnet.</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        <span data-ttu-id="73b23-149">Benzersiz yapılandırma adları ve özel IP adresleri (yapılandırmaları statik IP adresleriyle) kullanarak gereksinim duyduğunuz kadar çok yapılandırmaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="73b23-149">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    - <span data-ttu-id="73b23-150">**Bir ortak IP adresi Ekle**</span><span class="sxs-lookup"><span data-stu-id="73b23-150">**Add a public IP address**</span></span>
    
        <span data-ttu-id="73b23-151">Bir ortak IP adresi tooeither ilişkilendirerek eklenen yeni bir IP yapılandırması veya var olan bir IP yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="73b23-151">A public IP address is added by associating it tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="73b23-152">Gereksinim duyduğunuz kadar izleyin, hello bölümlerden biri hello adımlarını tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="73b23-152">Complete hello steps in one of hello sections that follow, as you require.</span></span>

        > [!NOTE]
        > <span data-ttu-id="73b23-153">Nominal bir ücret ortak IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="73b23-153">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="73b23-154">IP hakkında daha fazla adres fiyatlandırma toolearn okuma hello [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses) sayfası.</span><span class="sxs-lookup"><span data-stu-id="73b23-154">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="73b23-155">Bir abonelikte kullanılabilir genel IP adresleri sınırı toohello sayısı yoktur.</span><span class="sxs-lookup"><span data-stu-id="73b23-155">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="73b23-156">Merhaba okuma hello sınırları hakkında daha fazla toolearn [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) makalesi.</span><span class="sxs-lookup"><span data-stu-id="73b23-156">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
        >

        <span data-ttu-id="73b23-157">**Merhaba kaynak tooa yeni IP yapılandırmasını ilişkilendirin**</span><span class="sxs-lookup"><span data-stu-id="73b23-157">**Associate hello resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="73b23-158">Yeni bir IP yapılandırmasında bir ortak IP adresi eklediğinizde, tüm IP yapılandırmalarının özel bir IP adresi olması gerektiği için özel bir IP adresi eklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="73b23-158">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="73b23-159">Varolan bir ortak IP adresi kaynağı ekleyin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="73b23-159">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="73b23-160">toocreate yeni bir hello aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="73b23-160">toocreate a new one, enter hello following command:</span></span>

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        <span data-ttu-id="73b23-161">Özel statik IP adresi ve ilişkili hello yeni bir IP yapılandırmasıyla toocreate *myPublicIP3* genel IP adresi kaynak, komutu aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="73b23-161">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIP3* public IP address resource, enter hello following command:</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        <span data-ttu-id="73b23-162">**Merhaba kaynak tooan var olan IP yapılandırmasını ilişkilendirin**</span><span class="sxs-lookup"><span data-stu-id="73b23-162">**Associate hello resource tooan existing IP configuration**</span></span>

        <span data-ttu-id="73b23-163">Genel bir IP adresi kaynağı yalnızca zaten ilişkili olmayan ilişkili tooan IP yapılandırması olabilir.</span><span class="sxs-lookup"><span data-stu-id="73b23-163">A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="73b23-164">Komutu aşağıdaki hello girerek bir IP yapılandırması ilişkili bir ortak IP adresi olup olmadığını belirleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="73b23-164">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        <span data-ttu-id="73b23-165">Bir satır benzer toohello IPConfig-3 için çıktı döndürülen hello izleyen bir arayın:</span><span class="sxs-lookup"><span data-stu-id="73b23-165">Look for a line similar toohello one that follows for IPConfig-3 in hello returned output:</span></span>

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        <span data-ttu-id="73b23-166">Merhaba itibaren **genel IP** sütunu için *IpConfig 3* olduğundan, hiçbir ortak IP adresi kaynağı şu anda ilişkili tooit boştur.</span><span class="sxs-lookup"><span data-stu-id="73b23-166">Since hello **Public IP** column for *IpConfig-3* is blank, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="73b23-167">Bir var olan ortak IP adresi kaynak tooIpConfig-3 ekleyin veya komut toocreate bir aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="73b23-167">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        <span data-ttu-id="73b23-168">Tooassociate hello ortak IP adresi adlı kaynak toohello mevcut IP yapılandırması komutu aşağıdaki hello girin *IPConfig 3*:</span><span class="sxs-lookup"><span data-stu-id="73b23-168">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IPConfig-3*:</span></span>
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. <span data-ttu-id="73b23-169">Görünüm hello özel IP adresleri ve ortak IP adresi atanmış kaynaklar toohello girerek NIC hello komutu aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="73b23-169">View hello private IP addresses and hello public IP address resources assigned toohello NIC by entering hello following command:</span></span>

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      <span data-ttu-id="73b23-170">Merhaba çıkış benzer toohello aşağıdaki döndürülür:</span><span class="sxs-lookup"><span data-stu-id="73b23-170">hello returned output is similar toohello following:</span></span>
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. <span data-ttu-id="73b23-171">Merhaba hello yönergeleri takip ederek toohello NIC toohello VM işletim sistemi eklenen hello özel IP adresleri ekleme [eklemek IP adresleri tooa VM işletim sistemi](#os-config) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="73b23-171">Add hello private IP addresses you added toohello NIC toohello VM operating system by following hello instructions in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="73b23-172">Merhaba ortak IP adresleri toohello işletim sistemi eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="73b23-172">Do not add hello public IP addresses toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
