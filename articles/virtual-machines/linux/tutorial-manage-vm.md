---
title: "Oluşturma ve Azure CLI ile Linux sanal makineleri yönetme | Microsoft Docs"
description: "Öğretici - oluşturma ve Linux VM'ler Azure CLI ile yönetme"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c163c715eb1438a0d6b0ab53cbb43816ca8dbbb4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-manage-linux-vms-with-the-azure-cli"></a><span data-ttu-id="b2dc2-103">Oluşturma ve Linux VM'ler Azure CLI ile yönetme</span><span class="sxs-lookup"><span data-stu-id="b2dc2-103">Create and Manage Linux VMs with the Azure CLI</span></span>

<span data-ttu-id="b2dc2-104">Azure sanal makineler tam olarak yapılandırılabilir ve esnek bir bilgi işlem ortamı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="b2dc2-105">Bu öğretici, bir VM boyutu seçerek, bir VM görüntüsü seçme ve bir VM dağıtma gibi temel Azure sanal makine dağıtım öğeleri kapsar.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="b2dc2-106">Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b2dc2-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b2dc2-107">Oluşturma ve bir VM'ye bağlanın</span><span class="sxs-lookup"><span data-stu-id="b2dc2-107">Create and connect to a VM</span></span>
> * <span data-ttu-id="b2dc2-108">Seçin ve VM görüntüleri kullanmak</span><span class="sxs-lookup"><span data-stu-id="b2dc2-108">Select and use VM images</span></span>
> * <span data-ttu-id="b2dc2-109">Görüntüleme ve belirli VM boyutları kullanma</span><span class="sxs-lookup"><span data-stu-id="b2dc2-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="b2dc2-110">VM’yi yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="b2dc2-110">Resize a VM</span></span>
> * <span data-ttu-id="b2dc2-111">Görüntüleyin ve VM durumunu anlamak</span><span class="sxs-lookup"><span data-stu-id="b2dc2-111">View and understand VM state</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b2dc2-112">Yüklemek ve CLI yerel olarak kullanmak seçerseniz, Bu öğretici, Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-112">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="b2dc2-113">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="b2dc2-114">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b2dc2-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-resource-group"></a><span data-ttu-id="b2dc2-115">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2dc2-115">Create resource group</span></span>

<span data-ttu-id="b2dc2-116">[az group create](https://docs.microsoft.com/cli/azure/group#create) komutuyla bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-116">Create a resource group with the [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="b2dc2-117">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="b2dc2-118">Bir kaynak grubu bir sanal makine önce oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="b2dc2-119">Bu örnekte, bir kaynak grubu adında *myResourceGroupVM* oluşturulan *eastus* bölge.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-119">In this example, a resource group named *myResourceGroupVM* is created in the *eastus* region.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

<span data-ttu-id="b2dc2-120">Kaynak grubu oluştururken veya değiştirirken Bu öğretici görülebilir bir VM belirtilir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-120">The resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="b2dc2-121">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2dc2-121">Create virtual machine</span></span>

<span data-ttu-id="b2dc2-122">Bir sanal makine oluşturma [az vm oluşturma](https://docs.microsoft.com/cli/azure/vm#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-122">Create a virtual machine with the [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="b2dc2-123">Bir sanal makine oluştururken, işletim sistemi görüntüsü, disk boyutlandırma ve yönetici kimlik bilgileri gibi birkaç seçenek bulunur.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-123">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="b2dc2-124">Bu örnekte, bir sanal makine adı ile oluşturulan *myVM* Ubuntu Server çalıştıran.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-124">In this example, a virtual machine is created with a name of *myVM* running Ubuntu Server.</span></span> 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="b2dc2-125">VM oluşturulduktan sonra Azure CLI VM hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-125">Once the VM has been created, the Azure CLI outputs information about the VM.</span></span> <span data-ttu-id="b2dc2-126">Not edin `publicIpAddress`, bu adres sanal makine erişmek için kullanılan...</span><span class="sxs-lookup"><span data-stu-id="b2dc2-126">Take note of the `publicIpAddress`, this address can be used to access the virtual machine..</span></span> 

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroupVM"
}
```

## <a name="connect-to-vm"></a><span data-ttu-id="b2dc2-127">VM'ye bağlanın</span><span class="sxs-lookup"><span data-stu-id="b2dc2-127">Connect to VM</span></span>

<span data-ttu-id="b2dc2-128">SSH kullanarak VM şimdi bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-128">You can now connect to the VM using SSH.</span></span> <span data-ttu-id="b2dc2-129">Örnek IP adresiyle değiştirin `publicIpAddress` önceki adımda not ettiğiniz.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-129">Replace the example IP address with the `publicIpAddress` noted in the previous step.</span></span>

```bash
ssh 52.174.34.95
```

<span data-ttu-id="b2dc2-130">VM ile işlemi tamamladıktan sonra SSH oturumu kapatın.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-130">Once finished with the VM, close the SSH session.</span></span> 

```bash
exit
```

## <a name="understand-vm-images"></a><span data-ttu-id="b2dc2-131">VM görüntüleri anlama</span><span class="sxs-lookup"><span data-stu-id="b2dc2-131">Understand VM images</span></span>

<span data-ttu-id="b2dc2-132">Azure Market VM'ler oluşturmak için kullanılan çok sayıda görüntü içerir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-132">The Azure marketplace includes many images that can be used to create VMs.</span></span> <span data-ttu-id="b2dc2-133">Önceki adımlarda, bir sanal makine bir Ubuntu görüntü kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-133">In the previous steps, a virtual machine was created using an Ubuntu image.</span></span> <span data-ttu-id="b2dc2-134">Bu adımda, Azure CLI sonra ikinci bir sanal makineyi dağıtmak için kullanılan bir CentOS görüntüsü Market aramak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-134">In this step, the Azure CLI is used to search the marketplace for a CentOS image, which is then used to deploy a second virtual machine.</span></span>  

<span data-ttu-id="b2dc2-135">Bir liste en yaygın olarak kullanılan görüntüleri görmek için [az vm görüntü listesi](/cli/azure/vm/image#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-135">To see a list of the most commonly used images, use the [az vm image list](/cli/azure/vm/image#list) command.</span></span>

```azurecli-interactive 
az vm image list --output table
```

<span data-ttu-id="b2dc2-136">Komut çıktısı Azure üzerinde en popüler VM görüntüleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-136">The command output returns the most popular VM images on Azure.</span></span>

```bash
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

<span data-ttu-id="b2dc2-137">Ekleyerek tam bir listesi görülebilir `--all` bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-137">A full list can be seen by adding the `--all` argument.</span></span> <span data-ttu-id="b2dc2-138">Resim listesi de göre filtrelenebilir `--publisher` veya `–-offer`.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-138">The image list can also be filtered by `--publisher` or `–-offer`.</span></span> <span data-ttu-id="b2dc2-139">Bu örnekte, tüm görüntüleri için eşleşen bir teklif ile listesi filtrelenir *CentOS*.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-139">In this example, the list is filtered for all images with an offer that matches *CentOS*.</span></span> 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

<span data-ttu-id="b2dc2-140">Kısmi çıktı:</span><span class="sxs-lookup"><span data-stu-id="b2dc2-140">Partial output:</span></span>

```azurecli-interactive 
Offer             Publisher         Sku   Urn                                     Version
----------------  ----------------  ----  --------------------------------------  -----------
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201501         6.5.201501
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201503         6.5.201503
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201506         6.5.201506
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20150904       6.5.20150904
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20160309       6.5.20160309
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20170207       6.5.20170207
```

<span data-ttu-id="b2dc2-141">Belirli bir görüntüsünü kullanan bir VM'yi dağıtmak için değeri not edin *Urn* sütun.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-141">To deploy a VM using a specific image, take note of the value in the *Urn* column.</span></span> <span data-ttu-id="b2dc2-142">Görüntü belirtirken, görüntü sürüm numarası ile "son", hangi dağıtım en son sürümünü seçer değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-142">When specifying the image, the image version number can be replaced with “latest”, which selects the latest version of the distribution.</span></span> <span data-ttu-id="b2dc2-143">Bu örnekte, `--image` bağımsız değişkeni bir CentOS 6.5 görüntüsü en son sürümünü belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-143">In this example, the `--image` argument is used to specify the latest version of a CentOS 6.5 image.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="b2dc2-144">VM boyutları anlama</span><span class="sxs-lookup"><span data-stu-id="b2dc2-144">Understand VM sizes</span></span>

<span data-ttu-id="b2dc2-145">Bir sanal makine boyutu, sanal makine için kullanılabilir hale getirilir işlem kaynaklarını CPU, GPU ve bellek gibi miktarını belirler.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-145">A virtual machine size determines the amount of compute resources such as CPU, GPU, and memory that are made available to the virtual machine.</span></span> <span data-ttu-id="b2dc2-146">Sanal makineler, beklenen iş yükü için uygun boyutta olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-146">Virtual machines need to be sized appropriately for the expected work load.</span></span> <span data-ttu-id="b2dc2-147">İş yükü artarsa, var olan bir sanal makine yeniden boyutlandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-147">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="b2dc2-148">VM boyutları</span><span class="sxs-lookup"><span data-stu-id="b2dc2-148">VM Sizes</span></span>

<span data-ttu-id="b2dc2-149">Aşağıdaki tabloda, kullanım örneklerine boyutları kategorilere ayırır.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-149">The following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="b2dc2-150">Tür</span><span class="sxs-lookup"><span data-stu-id="b2dc2-150">Type</span></span>                     | <span data-ttu-id="b2dc2-151">Boyutlar</span><span class="sxs-lookup"><span data-stu-id="b2dc2-151">Sizes</span></span>           |    <span data-ttu-id="b2dc2-152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b2dc2-152">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="b2dc2-153">Genel amaçlı</span><span class="sxs-lookup"><span data-stu-id="b2dc2-153">General purpose</span></span>](sizes-general.md)         |<span data-ttu-id="b2dc2-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="b2dc2-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="b2dc2-155">Dengeli CPU bellekten.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-155">Balanced CPU-to-memory.</span></span> <span data-ttu-id="b2dc2-156">Geliştirme için ideal / test ve küçük ve orta uygulamaları ve verileri çözümler.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-156">Ideal for dev / test and small to medium applications and data solutions.</span></span>  |
| [<span data-ttu-id="b2dc2-157">İşlem için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="b2dc2-157">Compute optimized</span></span>](sizes-compute.md)   | <span data-ttu-id="b2dc2-158">FS, F</span><span class="sxs-lookup"><span data-stu-id="b2dc2-158">Fs, F</span></span>             | <span data-ttu-id="b2dc2-159">Yüksek CPU bellekten.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-159">High CPU-to-memory.</span></span> <span data-ttu-id="b2dc2-160">Orta düzey trafik uygulamalar, ağ uygulamaları ve toplu işlemler için iyidir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-160">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| [<span data-ttu-id="b2dc2-161">Bellek için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="b2dc2-161">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)    | <span data-ttu-id="b2dc2-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="b2dc2-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="b2dc2-163">Yüksek bellek için-çekirdek.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-163">High memory-to-core.</span></span> <span data-ttu-id="b2dc2-164">İlişkisel veritabanları, Orta ve büyük önbellekler ve bellek içi analizi için mükemmel.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-164">Great for relational databases, medium to large caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="b2dc2-165">Depolama için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="b2dc2-165">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)      | <span data-ttu-id="b2dc2-166">Ls</span><span class="sxs-lookup"><span data-stu-id="b2dc2-166">Ls</span></span>                | <span data-ttu-id="b2dc2-167">Yüksek disk aktarım hızı ve GÇ.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-167">High disk throughput and IO.</span></span> <span data-ttu-id="b2dc2-168">Büyük Veri, SQL ve NoSQL veritabanları için ideal.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-168">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="b2dc2-169">GPU</span><span class="sxs-lookup"><span data-stu-id="b2dc2-169">GPU</span></span>](sizes-gpu.md)          | <span data-ttu-id="b2dc2-170">NV, NC</span><span class="sxs-lookup"><span data-stu-id="b2dc2-170">NV, NC</span></span>            | <span data-ttu-id="b2dc2-171">Yoğun Grafik işleme ve video düzenleme için hedeflenen özel VM'ler.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-171">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| [<span data-ttu-id="b2dc2-172">Yüksek performans</span><span class="sxs-lookup"><span data-stu-id="b2dc2-172">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="b2dc2-173">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="b2dc2-173">H, A8-11</span></span>          | <span data-ttu-id="b2dc2-174">Bizim en güçlü CPU VM'ler isteğe bağlı yüksek verimlilik ağ arabirimlerine (RDMA) sahip.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-174">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="b2dc2-175">Kullanılabilir VM boyutları Bul</span><span class="sxs-lookup"><span data-stu-id="b2dc2-175">Find available VM sizes</span></span>

<span data-ttu-id="b2dc2-176">Belirli bir bölgede kullanılabilir VM boyutlarının listesini görmek için [az vm listesi-boyutları](/cli/azure/vm#list-sizes) komutu.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-176">To see a list of VM sizes available in a particular region, use the [az vm list-sizes](/cli/azure/vm#list-sizes) command.</span></span> 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

<span data-ttu-id="b2dc2-177">Kısmi çıktı:</span><span class="sxs-lookup"><span data-stu-id="b2dc2-177">Partial output:</span></span>

```azurecli-interactive 
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          3584  Standard_DS1                          1           1047552                    7168
                 4          7168  Standard_DS2                          2           1047552                   14336
                 8         14336  Standard_DS3                          4           1047552                   28672
                16         28672  Standard_DS4                          8           1047552                   57344
                 4         14336  Standard_DS11                         2           1047552                   28672
                 8         28672  Standard_DS12                         4           1047552                   57344
                16         57344  Standard_DS13                         8           1047552                  114688
                32        114688  Standard_DS14                        16           1047552                  229376
                 1           768  Standard_A0                           1           1047552                   20480
                 2          1792  Standard_A1                           1           1047552                   71680
                 4          3584  Standard_A2                           2           1047552                  138240
                 8          7168  Standard_A3                           4           1047552                  291840
                 4         14336  Standard_A5                           2           1047552                  138240
                16         14336  Standard_A4                           8           1047552                  619520
                 8         28672  Standard_A6                           4           1047552                  291840
                16         57344  Standard_A7                           8           1047552                  619520
```

### <a name="create-vm-with-specific-size"></a><span data-ttu-id="b2dc2-178">Belirli boyutuyla VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2dc2-178">Create VM with specific size</span></span>

<span data-ttu-id="b2dc2-179">Önceki VM oluşturma örnekte, bir boyut değil sağlanmadığından, varsayılan boyutu sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-179">In the previous VM creation example, a size was not provided, which results in a default size.</span></span> <span data-ttu-id="b2dc2-180">Oluşturma zamanı kullanarak bir VM boyutu seçilebilir [az vm oluşturma](/cli/azure/vm#create) ve `--size` bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-180">A VM size can be selected at creation time using [az vm create](/cli/azure/vm#create) and the `--size` argument.</span></span> 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a><span data-ttu-id="b2dc2-181">VM’yi yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="b2dc2-181">Resize a VM</span></span>

<span data-ttu-id="b2dc2-182">Bir VM dağıtıldıktan sonra artırmak veya kaynak ayırma azaltmak için yeniden boyutlandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-182">After a VM has been deployed, it can be resized to increase or decrease resource allocation.</span></span>

<span data-ttu-id="b2dc2-183">Bir VM'yi yeniden boyutlandırılırken önce istenen boyut geçerli Azure kümede kullanılabilir olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-183">Before resizing a VM, check if the desired size is available on the current Azure cluster.</span></span> <span data-ttu-id="b2dc2-184">[Az vm listesi-vm-yeniden boyutlandırma-seçenekleri](/cli/azure/vm#list-vm-resize-options) komut boyutlarının listesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-184">The [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options) command returns the list of sizes.</span></span> 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
<span data-ttu-id="b2dc2-185">İstenen boyut varsa, işlemi sırasında yeniden başlatılıncaya kadar ancak VM bir gücü açma durumundan boyutlandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-185">If the desired size is available, the VM can be resized from a powered-on state, however it is rebooted during the operation.</span></span> <span data-ttu-id="b2dc2-186">Kullanım [az VM'yi yeniden boyutlandırın]( /cli/azure/vm#resize) boyutlandırma gerçekleştirmek için komutu.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-186">Use the [az vm resize]( /cli/azure/vm#resize) command to perform the resize.</span></span>

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

<span data-ttu-id="b2dc2-187">İstenen boyut geçerli kümede değilse, VM yeniden boyutlandırma işlemi oluşabilmesi için öncelikle serbest gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-187">If the desired size is not on the current cluster, the VM needs to be deallocated before the resize operation can occur.</span></span> <span data-ttu-id="b2dc2-188">Kullanım [az vm serbest bırakma]( /cli/azure/vm#deallocate) durdurun ve VM serbest bırakma için komutu.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-188">Use the [az vm deallocate]( /cli/azure/vm#deallocate) command to stop and deallocate the VM.</span></span> <span data-ttu-id="b2dc2-189">Not, VM geri açık olduğundan, geçici diskteki tüm verilerin kaldırılmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-189">Note, when the VM is powered back on, any data on the temp disk may be removed.</span></span> <span data-ttu-id="b2dc2-190">Genel IP adresini de statik IP adresi kullanılmadığı sürece değiştirir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-190">The public IP address also changes unless a static IP address is being used.</span></span> 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

<span data-ttu-id="b2dc2-191">Yeniden boyutlandırma, serbest sonra ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-191">Once deallocated, the resize can occur.</span></span> 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

<span data-ttu-id="b2dc2-192">Sonra yeniden boyutlandırmak, VM başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-192">After the resize, the VM can be started.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a><span data-ttu-id="b2dc2-193">VM güç durumları</span><span class="sxs-lookup"><span data-stu-id="b2dc2-193">VM power states</span></span>

<span data-ttu-id="b2dc2-194">Bir Azure VM birçok güç durumlarını birine sahip.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-194">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="b2dc2-195">Bu durum, hiper yönetici açısından VM geçerli durumunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-195">This state represents the current state of the VM from the standpoint of the hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="b2dc2-196">Güç durumları</span><span class="sxs-lookup"><span data-stu-id="b2dc2-196">Power states</span></span>

| <span data-ttu-id="b2dc2-197">Güç durumu</span><span class="sxs-lookup"><span data-stu-id="b2dc2-197">Power State</span></span> | <span data-ttu-id="b2dc2-198">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b2dc2-198">Description</span></span>
|----|----|
| <span data-ttu-id="b2dc2-199">Başlangıç</span><span class="sxs-lookup"><span data-stu-id="b2dc2-199">Starting</span></span> | <span data-ttu-id="b2dc2-200">Sanal makinenin başlatıldığı gösterir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-200">Indicates the virtual machine is being started.</span></span> |
| <span data-ttu-id="b2dc2-201">Çalışıyor</span><span class="sxs-lookup"><span data-stu-id="b2dc2-201">Running</span></span> | <span data-ttu-id="b2dc2-202">Sanal makinenin çalıştığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-202">Indicates that the virtual machine is running.</span></span> |
| <span data-ttu-id="b2dc2-203">Durduruluyor</span><span class="sxs-lookup"><span data-stu-id="b2dc2-203">Stopping</span></span> | <span data-ttu-id="b2dc2-204">Sanal makinenin durdurulması olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-204">Indicates that the virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="b2dc2-205">Durduruldu</span><span class="sxs-lookup"><span data-stu-id="b2dc2-205">Stopped</span></span> | <span data-ttu-id="b2dc2-206">Sanal makine durdurulduğunda gösterir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-206">Indicates that the virtual machine is stopped.</span></span> <span data-ttu-id="b2dc2-207">Sanal makine durdurulmuş durumunda hala işlem ücretleri.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-207">Virtual machines in the stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="b2dc2-208">Ayırmayı kaldırma</span><span class="sxs-lookup"><span data-stu-id="b2dc2-208">Deallocating</span></span> | <span data-ttu-id="b2dc2-209">Sanal makine ayırması olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-209">Indicates that the virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="b2dc2-210">Serbest bırakıldı</span><span class="sxs-lookup"><span data-stu-id="b2dc2-210">Deallocated</span></span> | <span data-ttu-id="b2dc2-211">Sanal makine hiper yönetici alanından kaldırılacak, ancak denetim düzeyi hala kullanılabilir olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-211">Indicates that the virtual machine is removed from the hypervisor but still available in the control plane.</span></span> <span data-ttu-id="b2dc2-212">Deallocated durumunda sanal makineler bilgi işlem ücretleri değil.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-212">Virtual machines in the Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="b2dc2-213">Sanal makinenin güç durumunun bilinmediğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-213">Indicates that the power state of the virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="b2dc2-214">Güç durumu Bul</span><span class="sxs-lookup"><span data-stu-id="b2dc2-214">Find power state</span></span>

<span data-ttu-id="b2dc2-215">Belirli bir VM durumunu almak için kullanın [az vm örnek görünümünü Al](/cli/azure/vm#get-instance-view) komutu.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-215">To retrieve the state of a particular VM, use the [az vm get instance-view](/cli/azure/vm#get-instance-view) command.</span></span> <span data-ttu-id="b2dc2-216">Bir sanal makine ve kaynak grubu için geçerli bir ad belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-216">Be sure to specify a valid name for a virtual machine and resource group.</span></span> 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

<span data-ttu-id="b2dc2-217">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="b2dc2-217">Output:</span></span>

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a><span data-ttu-id="b2dc2-218">Yönetim görevleri</span><span class="sxs-lookup"><span data-stu-id="b2dc2-218">Management tasks</span></span>

<span data-ttu-id="b2dc2-219">Yaşam döngüsü sırasında sanal makinenin, başlatma, durdurma veya bir sanal makine silme gibi yönetim görevleri çalıştırmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-219">During the life-cycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="b2dc2-220">Ayrıca, yinelenen veya karmaşık görevleri otomatikleştirmek için komut dosyaları oluşturmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-220">Additionally, you may want to create scripts to automate repetitive or complex tasks.</span></span> <span data-ttu-id="b2dc2-221">Azure CLI kullanarak, birçok ortak yönetim görevlerinin komut satırından veya komut dosyalarında çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-221">Using the Azure CLI, many common management tasks can be run from the command line or in scripts.</span></span> 

### <a name="get-ip-address"></a><span data-ttu-id="b2dc2-222">IP adresi al</span><span class="sxs-lookup"><span data-stu-id="b2dc2-222">Get IP address</span></span>

<span data-ttu-id="b2dc2-223">Bu komut, bir sanal makine özel ve genel IP adreslerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-223">This command returns the private and public IP addresses of a virtual machine.</span></span>  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a><span data-ttu-id="b2dc2-224">Sanal makineyi durdurma</span><span class="sxs-lookup"><span data-stu-id="b2dc2-224">Stop virtual machine</span></span>

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a><span data-ttu-id="b2dc2-225">Sanal makineyi Başlat</span><span class="sxs-lookup"><span data-stu-id="b2dc2-225">Start virtual machine</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="b2dc2-226">Kaynak grubunu silme</span><span class="sxs-lookup"><span data-stu-id="b2dc2-226">Delete resource group</span></span>

<span data-ttu-id="b2dc2-227">Bir kaynak grubunu silme içinde içerdiği tüm kaynaklar da siler.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-227">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a><span data-ttu-id="b2dc2-228">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b2dc2-228">Next steps</span></span>

<span data-ttu-id="b2dc2-229">Bu öğreticide, temel VM oluşturmayı ve yönetmeyi nasıl gibi hakkında öğrenilen:</span><span class="sxs-lookup"><span data-stu-id="b2dc2-229">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b2dc2-230">Oluşturma ve bir VM'ye bağlanın</span><span class="sxs-lookup"><span data-stu-id="b2dc2-230">Create and connect to a VM</span></span>
> * <span data-ttu-id="b2dc2-231">Seçin ve VM görüntüleri kullanmak</span><span class="sxs-lookup"><span data-stu-id="b2dc2-231">Select and use VM images</span></span>
> * <span data-ttu-id="b2dc2-232">Görüntüleme ve belirli VM boyutları kullanma</span><span class="sxs-lookup"><span data-stu-id="b2dc2-232">View and use specific VM sizes</span></span>
> * <span data-ttu-id="b2dc2-233">VM’yi yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="b2dc2-233">Resize a VM</span></span>
> * <span data-ttu-id="b2dc2-234">Görüntüleyin ve VM durumunu anlamak</span><span class="sxs-lookup"><span data-stu-id="b2dc2-234">View and understand VM state</span></span>

<span data-ttu-id="b2dc2-235">VM diskleri hakkında bilgi edinmek için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="b2dc2-235">Advance to the next tutorial to learn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="b2dc2-236">Oluşturma ve yönetme VM diskleri</span><span class="sxs-lookup"><span data-stu-id="b2dc2-236">Create and Manage VM disks</span></span>](./tutorial-manage-disks.md)
