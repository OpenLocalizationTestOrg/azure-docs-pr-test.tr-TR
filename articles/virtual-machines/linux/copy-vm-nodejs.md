---
title: "aaaCreate hello Azure CLI 1.0 ile Linux VM kopyasını | Microsoft Docs"
description: "Nasıl bir Azure Linux sanal makineniz ile kopyasını toocreate hello Azure CLI 1.0 hello Resource Manager dağıtım modelinde öğrenin"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 997a2c8109e7083ececd76fd1013e9ed4d3e6afd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-hello-azure-cli-10"></a><span data-ttu-id="2308d-103">Azure CLI 1.0 hello ile Azure üzerinde çalışan Linux sanal makine bir kopyasını oluşturun</span><span class="sxs-lookup"><span data-stu-id="2308d-103">Create a copy of a Linux virtual machine running on Azure with hello Azure CLI 1.0</span></span>
<span data-ttu-id="2308d-104">Bu makalede nasıl toocreate Azure sanal makine (VM) çalışan Linux kullanarak bir kopyasını hello Resource Manager dağıtım modeli gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="2308d-104">This article shows you how toocreate a copy of your Azure virtual machine (VM) running Linux using hello Resource Manager deployment model.</span></span> <span data-ttu-id="2308d-105">İlk olarak, hello işletim sistemi ve veri diskleri tooa yeni kapsayıcı, kopyalayın sonra hello ağ kaynakları ayarlamak ve hello yeni sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2308d-105">First you copy over hello operating system and data disks tooa new container, then set up hello network resources and create hello new virtual machine.</span></span>

<span data-ttu-id="2308d-106">Ayrıca [karşıya yükleme ve özel disk görüntüsünden bir VM oluşturma](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2308d-106">You can also [upload and create a VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="2308d-107">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="2308d-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="2308d-108">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="2308d-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="2308d-109">Azure CLI 1.0 – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="2308d-109">Azure CLI 1.0 – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="2308d-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="2308d-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2308d-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="2308d-111">Before you begin</span></span>
<span data-ttu-id="2308d-112">Merhaba hello adımları başlamadan önce aşağıdaki önkoşulları karşıladığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="2308d-112">Ensure that you meet hello following prerequisites before you start hello steps:</span></span>

* <span data-ttu-id="2308d-113">Merhaba sahip [Azure CLI](../../cli-install-nodejs.md) makinenizde yüklenip.</span><span class="sxs-lookup"><span data-stu-id="2308d-113">You have hello [Azure CLI](../../cli-install-nodejs.md) downloaded and installed on your machine.</span></span> 
* <span data-ttu-id="2308d-114">Ayrıca, mevcut bir Azure Linux VM'i hakkında bazı bilgiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="2308d-114">You also need some information about your existing Azure Linux VM:</span></span>

| <span data-ttu-id="2308d-115">Kaynak VM bilgileri</span><span class="sxs-lookup"><span data-stu-id="2308d-115">Source VM information</span></span> | <span data-ttu-id="2308d-116">Burada tooget,</span><span class="sxs-lookup"><span data-stu-id="2308d-116">Where tooget it</span></span> |
| --- | --- |
| <span data-ttu-id="2308d-117">VM adı</span><span class="sxs-lookup"><span data-stu-id="2308d-117">VM name</span></span> |`azure vm list` |
| <span data-ttu-id="2308d-118">Kaynak grubu adı</span><span class="sxs-lookup"><span data-stu-id="2308d-118">Resource Group name</span></span> |`azure vm list` |
| <span data-ttu-id="2308d-119">Konum</span><span class="sxs-lookup"><span data-stu-id="2308d-119">Location</span></span> |`azure vm list` |
| <span data-ttu-id="2308d-120">Depolama hesabı adı</span><span class="sxs-lookup"><span data-stu-id="2308d-120">Storage Account name</span></span> |`azure storage account list -g <resourceGroup>` |
| <span data-ttu-id="2308d-121">Kapsayıcı adı</span><span class="sxs-lookup"><span data-stu-id="2308d-121">Container name</span></span> |`azure storage container list -a <sourcestorageaccountname>` |
| <span data-ttu-id="2308d-122">Kaynak VM VHD dosya adı</span><span class="sxs-lookup"><span data-stu-id="2308d-122">Source VM VHD file name</span></span> |`azure storage blob list --container <containerName>` |

* <span data-ttu-id="2308d-123">Yeni VM'nin hakkında bazı seçenekleri toomake gerekir:   </span><span class="sxs-lookup"><span data-stu-id="2308d-123">You will need toomake some choices about your new VM:    </span></span><br> <span data-ttu-id="2308d-124">-Kapsayıcı adı   </span><span class="sxs-lookup"><span data-stu-id="2308d-124">-Container name    </span></span><br> <span data-ttu-id="2308d-125">-VM adı   </span><span class="sxs-lookup"><span data-stu-id="2308d-125">-VM name    </span></span><br> <span data-ttu-id="2308d-126">-VM boyutu   </span><span class="sxs-lookup"><span data-stu-id="2308d-126">-VM size    </span></span><br> <span data-ttu-id="2308d-127">-vNet adı   </span><span class="sxs-lookup"><span data-stu-id="2308d-127">-vNet name    </span></span><br> <span data-ttu-id="2308d-128">-Alt ağ adı   </span><span class="sxs-lookup"><span data-stu-id="2308d-128">-SubNet name    </span></span><br> <span data-ttu-id="2308d-129">-IP adı   </span><span class="sxs-lookup"><span data-stu-id="2308d-129">-IP Name    </span></span><br> <span data-ttu-id="2308d-130">-NIC adı</span><span class="sxs-lookup"><span data-stu-id="2308d-130">-NIC name</span></span>

## <a name="login-and-set-your-subscription"></a><span data-ttu-id="2308d-131">Oturum açma ve aboneliğinizi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="2308d-131">Login and set your subscription</span></span>
1. <span data-ttu-id="2308d-132">Oturum açma toohello CLI.</span><span class="sxs-lookup"><span data-stu-id="2308d-132">Login toohello CLI.</span></span>

    ```azurecli
    azure login
    ```
2. <span data-ttu-id="2308d-133">Kaynak Yöneticisi modunda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="2308d-133">Make sure you are in Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="2308d-134">Merhaba doğru aboneliğin ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2308d-134">Set hello correct subscription.</span></span> <span data-ttu-id="2308d-135">'Azure hesabı listesi' toosee kullanabileceğiniz tüm aboneliklerinizi.</span><span class="sxs-lookup"><span data-stu-id="2308d-135">You can use 'azure account list' toosee all of your subscriptions.</span></span>

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-hello-vm"></a><span data-ttu-id="2308d-136">Merhaba VM Durdur</span><span class="sxs-lookup"><span data-stu-id="2308d-136">Stop hello VM</span></span>
<span data-ttu-id="2308d-137">Durdurun ve hello kaynak VM serbest bırakma.</span><span class="sxs-lookup"><span data-stu-id="2308d-137">Stop and deallocate hello source VM.</span></span> <span data-ttu-id="2308d-138">Aboneliğiniz ve kaynak grubu adları 'azure vm listesi' tooget hello VM'ler tümünün listesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2308d-138">You can use 'azure vm list' tooget a list of all of hello VMs in your subscription and their resource group names.</span></span>

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-hello-vhd"></a><span data-ttu-id="2308d-139">Merhaba VHD kopyalayın</span><span class="sxs-lookup"><span data-stu-id="2308d-139">Copy hello VHD</span></span>
<span data-ttu-id="2308d-140">Merhaba kaynak depolama toohello hedef hello kullanarak hello VHD kopyalayabilirsiniz `azure storage blob copy start`.</span><span class="sxs-lookup"><span data-stu-id="2308d-140">You can copy hello VHD from hello source storage toohello destination using hello `azure storage blob copy start`.</span></span> <span data-ttu-id="2308d-141">Bu örnekte, biz toocopy hello VHD toohello kalacaklarını aynı depolama hesabı, ancak farklı bir kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="2308d-141">In this example, we are going toocopy hello VHD toohello same storage account, but a different container.</span></span>

<span data-ttu-id="2308d-142">toocopy hello VHD tooanother hello kapsayıcısında aynı depolama hesabı, türü:</span><span class="sxs-lookup"><span data-stu-id="2308d-142">toocopy hello VHD tooanother container in hello same storage account, type:</span></span>

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-hello-virtual-network-for-your-new-vm"></a><span data-ttu-id="2308d-143">Yeni VM için Hello sanal ağ kur ayarlama</span><span class="sxs-lookup"><span data-stu-id="2308d-143">Set up hello virtual network for your new VM</span></span>
<span data-ttu-id="2308d-144">Yeni VM için bir sanal ağ ve NIC ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2308d-144">Set up a virtual network and NIC for your new VM.</span></span> 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-hello-new-vm"></a><span data-ttu-id="2308d-145">Oluşturma yeni VM hello</span><span class="sxs-lookup"><span data-stu-id="2308d-145">Create hello new VM</span></span>
<span data-ttu-id="2308d-146">Karşıya yüklenen sanal diskten bir VM artık oluşturabilirsiniz [resource manager şablonu kullanarak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) veya hello hello URI tooyour belirterek CLI disk yazarak kopyalanan:</span><span class="sxs-lookup"><span data-stu-id="2308d-146">You can now create a VM from your uploaded virtual disk [using a resource manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) or through hello CLI by specifying hello URI tooyour copied disk by typing:</span></span>

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a><span data-ttu-id="2308d-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2308d-147">Next steps</span></span>
<span data-ttu-id="2308d-148">toolearn nasıl toouse Azure CLI toomanage, yeni bir sanal makine bkz [hello Azure Resource Manager için Azure CLI komutları](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="2308d-148">toolearn how toouse Azure CLI toomanage your new virtual machine, see [Azure CLI commands for hello Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>

