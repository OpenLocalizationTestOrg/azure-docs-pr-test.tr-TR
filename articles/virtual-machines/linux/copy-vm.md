---
title: Azure CLI 2.0 kullanarak bir Linux VM aaaCopy | Microsoft Docs
description: "Bilgi nasıl toocreate Azure CLI 2.0 ve yönetilen diskleri kullanarak Azure Linux VM bir kopyası."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/10/2017
ms.author: cynthn
ms.openlocfilehash: ee34a4259dd0c1e7bf49312fe3fe3ba809bf69e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a><span data-ttu-id="349fb-103">Azure CLI 2.0 ve yönetilen diskleri kullanarak bir Linux VM bir kopyasını oluşturun</span><span class="sxs-lookup"><span data-stu-id="349fb-103">Create a copy of a Linux VM by using Azure CLI 2.0 and Managed Disks</span></span>


<span data-ttu-id="349fb-104">Bu makalede toocreate bir kopyasını kullanarak Linux çalıştıran, Azure sanal makine (VM) nasıl hello Azure CLI 2.0 ve hello Azure Resource Manager dağıtım modeli gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="349fb-104">This article shows you how toocreate a copy of your Azure virtual machine (VM) running Linux using hello Azure CLI 2.0 and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="349fb-105">Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="349fb-105">You can also perform these steps with hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="349fb-106">Ayrıca [karşıya yükleyin ve bir VHD'den bir VM oluşturma](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="349fb-106">You can also [upload and create a VM from a VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="349fb-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="349fb-107">Prerequisites</span></span>


-   <span data-ttu-id="349fb-108">Yükleme [Azure CLI 2.0](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="349fb-108">Install [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

-   <span data-ttu-id="349fb-109">İçinde tooan Azure hesabı ile oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="349fb-109">Sign in tooan Azure account with [az login](/cli/azure/#login).</span></span>

-   <span data-ttu-id="349fb-110">Kopyanızı hello kaynağı olarak bir Azure VM toouse sahip.</span><span class="sxs-lookup"><span data-stu-id="349fb-110">Have an Azure VM toouse as hello source for your copy.</span></span>

## <a name="step-1-stop-hello-source-vm"></a><span data-ttu-id="349fb-111">1. adım: hello kaynak VM Durdur</span><span class="sxs-lookup"><span data-stu-id="349fb-111">Step 1: Stop hello source VM</span></span>


<span data-ttu-id="349fb-112">Kullanarak Hello kaynak VM serbest bırakma [az vm serbest bırakma](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="349fb-112">Deallocate hello source VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span>
<span data-ttu-id="349fb-113">Merhaba aşağıdaki örnek kaldırır hello adlı VM **myVM** hello kaynak grubunda **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="349fb-113">hello following example deallocates hello VM named **myVM** in hello resource group **myResourceGroup**:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-hello-source-vm"></a><span data-ttu-id="349fb-114">2. adım: hello kaynak VM kopyalama</span><span class="sxs-lookup"><span data-stu-id="349fb-114">Step 2: Copy hello source VM</span></span>


<span data-ttu-id="349fb-115">bir VM toocopy, hello alttaki sanal sabit diskin bir kopyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="349fb-115">toocopy a VM, you create a copy of hello underlying virtual hard disk.</span></span> <span data-ttu-id="349fb-116">Bu işlem, özel bir VHD yönetilen hello içeren bir Disk oluşturur. kaynak VM aynı yapılandırma ve hello olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="349fb-116">This process creates a specialized VHD as a Managed Disk that contains hello same configuration and settings as hello source VM.</span></span>

<span data-ttu-id="349fb-117">Azure Yönetilen Diskler hakkında daha fazla bilgi için bkz. [Azure Yönetilen Disklere genel bakış](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="349fb-117">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span> 

1.  <span data-ttu-id="349fb-118">Her VM hello adı ve kendi işletim sistemi diski ile listesinde [az vm listesi](/cli/azure/vm#list).</span><span class="sxs-lookup"><span data-stu-id="349fb-118">List each VM and hello name of its OS disk with [az vm list](/cli/azure/vm#list).</span></span> <span data-ttu-id="349fb-119">Merhaba aşağıdaki örnek listeler adlı kaynak grubundaki tüm sanal makineleri **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="349fb-119">hello following example lists all VMs in the resource group named **myResourceGroup**:</span></span>
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    <span data-ttu-id="349fb-120">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="349fb-120">hello output is similar toohello following example:</span></span>

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  <span data-ttu-id="349fb-121">Yeni bir oluşturarak hello disk Kopyala yönetilen diski kullanarak [az disketi](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="349fb-121">Copy hello disk by creating a new managed disk using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="349fb-122">Merhaba aşağıdaki örnekte oluşturur adlı bir disk **myCopiedDisk** adlı disk hello yönetilen **myDisk**:</span><span class="sxs-lookup"><span data-stu-id="349fb-122">hello following example creates a disk named **myCopiedDisk** from hello managed disk named **myDisk**:</span></span>

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  <span data-ttu-id="349fb-123">Artık kaynak grubunuzdaki yönetilen hello diskleri kullanarak doğrulayın [az disk listesi](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="349fb-123">Verify hello managed disks now in your resource group by using [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="349fb-124">Merhaba aşağıdaki örnek listeler adlı hello kaynak grubundaki yönetilen hello diskler **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="349fb-124">hello following example lists hello managed disks in hello resource group named **myResourceGroup**:</span></span>

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  <span data-ttu-id="349fb-125">Çok atla["3. adım: sanal ağ kurma"](#step-3-set-up-a-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="349fb-125">Skip too["Step 3: Set up a virtual network"](#step-3-set-up-a-virtual-network).</span></span>


## <a name="step-3-set-up-a-virtual-network"></a><span data-ttu-id="349fb-126">3. adım: Sanal ağ ayarlama</span><span class="sxs-lookup"><span data-stu-id="349fb-126">Step 3: Set up a virtual network</span></span>


<span data-ttu-id="349fb-127">Merhaba aşağıdaki isteğe bağlı adımlar yeni bir sanal ağ, alt ağ, genel IP adresi ve sanal ağ arabirim kartı (NIC) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="349fb-127">hello following optional steps create a new virtual network, subnet, public IP address, and virtual network interface card (NIC).</span></span>

<span data-ttu-id="349fb-128">Bir VM amacıyla ya da başka dağıtımlar sorun giderme için kopyalıyorsanız toouse, varolan bir sanal ağda bir VM istemeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="349fb-128">If you are copying a VM for troubleshooting purposes or additional deployments, you might not want toouse a VM in an existing virtual network.</span></span>

<span data-ttu-id="349fb-129">Kopyalanan Vm'leriniz için toocreate bir sanal ağ altyapısı istiyorsanız izleyin hello sonraki birkaç adımda.</span><span class="sxs-lookup"><span data-stu-id="349fb-129">If you want toocreate a virtual network infrastructure for your copied VMs, follow hello next few steps.</span></span> <span data-ttu-id="349fb-130">Bir sanal ağ toocreate istemiyorsanız, çok atla[4. adım: bir VM oluşturma](#step-4-create-a-vm).</span><span class="sxs-lookup"><span data-stu-id="349fb-130">If you don't want toocreate a virtual network, skip too[Step 4: Create a VM](#step-4-create-a-vm).</span></span>

1.  <span data-ttu-id="349fb-131">Kullanarak Hello sanal ağ oluşturma [az ağ vnet oluşturma](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="349fb-131">Create hello virtual network by using [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="349fb-132">Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur **myVnet** ve adlı bir alt ağ **mySubnet**:</span><span class="sxs-lookup"><span data-stu-id="349fb-132">hello following example creates a virtual network named **myVnet** and a subnet named **mySubnet**:</span></span>

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  <span data-ttu-id="349fb-133">Kullanarak bir genel IP oluşturun [az ağ genel IP oluşturun](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="349fb-133">Create a public IP by using [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="349fb-134">Merhaba aşağıdaki örnekte oluşturur adlı ortak IP **myPublicIP** hello DNS adı ile **mypublicdns**.</span><span class="sxs-lookup"><span data-stu-id="349fb-134">hello following example creates a public IP named **myPublicIP** with hello DNS name of **mypublicdns**.</span></span> <span data-ttu-id="349fb-135">(Merhaba DNS adı gerekir benzersiz olması, dolayısıyla benzersiz bir ad sağlayın.)</span><span class="sxs-lookup"><span data-stu-id="349fb-135">(hello DNS name must be unique, so provide a unique name.)</span></span>

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  <span data-ttu-id="349fb-136">NIC Hello kullanarak oluşturduğunuz [az ağ NIC oluşturma](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="349fb-136">Create hello NIC using [az network nic create](/cli/azure/network/nic#create).</span></span>
    <span data-ttu-id="349fb-137">Merhaba aşağıdaki örnekte oluşturur adlı bir NIC **myNic** o ekli toothe **mySubnet** alt ağ:</span><span class="sxs-lookup"><span data-stu-id="349fb-137">hello following example creates a NIC named **myNic** that's attached toothe **mySubnet** subnet:</span></span>

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a><span data-ttu-id="349fb-138">4. adım: bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="349fb-138">Step 4: Create a VM</span></span>

<span data-ttu-id="349fb-139">Kullanarak bir VM şimdi oluşturabilirsiniz [az vm oluşturma](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="349fb-139">You can now create a VM by using [az vm create](/cli/azure/vm#create).</span></span>

<span data-ttu-id="349fb-140">Merhaba kopyalanan hello işletim sistemi diski olarak yönetilen disk toouse belirtin (--attach-os-disk) aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="349fb-140">Specify hello copied managed disk toouse as hello OS disk (--attach-os-disk), as follows:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a><span data-ttu-id="349fb-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="349fb-141">Next steps</span></span>

<span data-ttu-id="349fb-142">toolearn nasıl toouse Azure CLI toomanage, yeni VM bkz [hello Azure Resource Manager için Azure CLI komutları](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="349fb-142">toolearn how toouse Azure CLI toomanage your new VM, see [Azure CLI commands for hello Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>
