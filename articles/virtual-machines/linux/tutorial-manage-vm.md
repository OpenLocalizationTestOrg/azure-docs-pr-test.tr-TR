---
title: "aaaCreate ve Linux sanal makineleri yönetme hello Azure CLI | Microsoft Docs"
description: "Öğretici - oluşturmak ve yönetmek Linux VM'ler ile hello Azure CLI"
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
ms.openlocfilehash: 05f7c1cf860f809bc13f110778d3bddd619ac6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-linux-vms-with-hello-azure-cli"></a><span data-ttu-id="8d337-103">Oluşturma ve yönetme Linux VM'ler ile Azure CLI hello</span><span class="sxs-lookup"><span data-stu-id="8d337-103">Create and Manage Linux VMs with hello Azure CLI</span></span>

<span data-ttu-id="8d337-104">Azure sanal makineler tam olarak yapılandırılabilir ve esnek bir bilgi işlem ortamı sağlar.</span><span class="sxs-lookup"><span data-stu-id="8d337-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="8d337-105">Bu öğretici, bir VM boyutu seçerek, bir VM görüntüsü seçme ve bir VM dağıtma gibi temel Azure sanal makine dağıtım öğeleri kapsar.</span><span class="sxs-lookup"><span data-stu-id="8d337-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="8d337-106">Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8d337-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8d337-107">Oluştur ve tooa VM Bağlan</span><span class="sxs-lookup"><span data-stu-id="8d337-107">Create and connect tooa VM</span></span>
> * <span data-ttu-id="8d337-108">Seçin ve VM görüntüleri kullanmak</span><span class="sxs-lookup"><span data-stu-id="8d337-108">Select and use VM images</span></span>
> * <span data-ttu-id="8d337-109">Görüntüleme ve belirli VM boyutları kullanma</span><span class="sxs-lookup"><span data-stu-id="8d337-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="8d337-110">VM’yi yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="8d337-110">Resize a VM</span></span>
> * <span data-ttu-id="8d337-111">Görüntüleyin ve VM durumunu anlamak</span><span class="sxs-lookup"><span data-stu-id="8d337-111">View and understand VM state</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8d337-112">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="8d337-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="8d337-113">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="8d337-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8d337-114">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8d337-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-resource-group"></a><span data-ttu-id="8d337-115">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="8d337-115">Create resource group</span></span>

<span data-ttu-id="8d337-116">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="8d337-116">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="8d337-117">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="8d337-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="8d337-118">Bir kaynak grubu bir sanal makine önce oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8d337-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="8d337-119">Bu örnekte, bir kaynak grubu adında *myResourceGroupVM* hello oluşturulan *eastus* bölge.</span><span class="sxs-lookup"><span data-stu-id="8d337-119">In this example, a resource group named *myResourceGroupVM* is created in hello *eastus* region.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

<span data-ttu-id="8d337-120">Merhaba kaynak grubu oluştururken veya değiştirirken Bu öğretici görülebilir bir VM belirtilir.</span><span class="sxs-lookup"><span data-stu-id="8d337-120">hello resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="8d337-121">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="8d337-121">Create virtual machine</span></span>

<span data-ttu-id="8d337-122">Merhaba ile bir sanal makine oluşturmak [az vm oluşturma](https://docs.microsoft.com/cli/azure/vm#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="8d337-122">Create a virtual machine with hello [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="8d337-123">Bir sanal makine oluştururken, işletim sistemi görüntüsü, disk boyutlandırma ve yönetici kimlik bilgileri gibi birkaç seçenek bulunur.</span><span class="sxs-lookup"><span data-stu-id="8d337-123">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="8d337-124">Bu örnekte, bir sanal makine adı ile oluşturulan *myVM* Ubuntu Server çalıştıran.</span><span class="sxs-lookup"><span data-stu-id="8d337-124">In this example, a virtual machine is created with a name of *myVM* running Ubuntu Server.</span></span> 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="8d337-125">Bir kez hello VM oluşturulduktan sonra hello Azure CLI hello VM bilgilerini çıkarır.</span><span class="sxs-lookup"><span data-stu-id="8d337-125">Once hello VM has been created, hello Azure CLI outputs information about hello VM.</span></span> <span data-ttu-id="8d337-126">Merhaba not edin `publicIpAddress`, bu adres kullanılan tooaccess hello sanal makineye bağlanabilir...</span><span class="sxs-lookup"><span data-stu-id="8d337-126">Take note of hello `publicIpAddress`, this address can be used tooaccess hello virtual machine..</span></span> 

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

## <a name="connect-toovm"></a><span data-ttu-id="8d337-127">TooVM Bağlan</span><span class="sxs-lookup"><span data-stu-id="8d337-127">Connect tooVM</span></span>

<span data-ttu-id="8d337-128">Şimdi toohello VM bağlanabilir SSH kullanarak.</span><span class="sxs-lookup"><span data-stu-id="8d337-128">You can now connect toohello VM using SSH.</span></span> <span data-ttu-id="8d337-129">Merhaba örnek IP adresi ile hello yerine `publicIpAddress` hello önceki adımda not ettiğiniz.</span><span class="sxs-lookup"><span data-stu-id="8d337-129">Replace hello example IP address with hello `publicIpAddress` noted in hello previous step.</span></span>

```bash
ssh 52.174.34.95
```

<span data-ttu-id="8d337-130">Merhaba VM ile işlemi tamamladıktan sonra hello SSH oturumu kapatın.</span><span class="sxs-lookup"><span data-stu-id="8d337-130">Once finished with hello VM, close hello SSH session.</span></span> 

```bash
exit
```

## <a name="understand-vm-images"></a><span data-ttu-id="8d337-131">VM görüntüleri anlama</span><span class="sxs-lookup"><span data-stu-id="8d337-131">Understand VM images</span></span>

<span data-ttu-id="8d337-132">Hello Azure Market kullanılan toocreate VM'ler olabilecek çok sayıda görüntü içerir.</span><span class="sxs-lookup"><span data-stu-id="8d337-132">hello Azure marketplace includes many images that can be used toocreate VMs.</span></span> <span data-ttu-id="8d337-133">Merhaba önceki adımlarda, bir sanal makine bir Ubuntu görüntü kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="8d337-133">In hello previous steps, a virtual machine was created using an Ubuntu image.</span></span> <span data-ttu-id="8d337-134">Bu adımda, Azure CLI ise bir CentOS görüntü için kullanılan toosearch hello Market olduğu hello toodeploy ikinci bir sanal makinede kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8d337-134">In this step, hello Azure CLI is used toosearch hello marketplace for a CentOS image, which is then used toodeploy a second virtual machine.</span></span>  

<span data-ttu-id="8d337-135">toosee hello listesi en yaygın olarak kullanılan görüntüleri, hello kullan [az vm görüntü listesi](/cli/azure/vm/image#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="8d337-135">toosee a list of hello most commonly used images, use hello [az vm image list](/cli/azure/vm/image#list) command.</span></span>

```azurecli-interactive 
az vm image list --output table
```

<span data-ttu-id="8d337-136">Merhaba komutu çıktısı Azure'da hello en popüler VM görüntüleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="8d337-136">hello command output returns hello most popular VM images on Azure.</span></span>

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

<span data-ttu-id="8d337-137">Merhaba ekleyerek tam bir listesi görülebilir `--all` bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="8d337-137">A full list can be seen by adding hello `--all` argument.</span></span> <span data-ttu-id="8d337-138">Merhaba resim listesi ayrıca göre filtrelenmiş `--publisher` veya `–-offer`.</span><span class="sxs-lookup"><span data-stu-id="8d337-138">hello image list can also be filtered by `--publisher` or `–-offer`.</span></span> <span data-ttu-id="8d337-139">Bu örnekte, tüm görüntüleri için eşleşen bir teklif ile Merhaba listesi filtrelenir *CentOS*.</span><span class="sxs-lookup"><span data-stu-id="8d337-139">In this example, hello list is filtered for all images with an offer that matches *CentOS*.</span></span> 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

<span data-ttu-id="8d337-140">Kısmi çıktı:</span><span class="sxs-lookup"><span data-stu-id="8d337-140">Partial output:</span></span>

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

<span data-ttu-id="8d337-141">belirli bir görüntü kullanarak bir VM'i toodeploy hello hello değeri not alın *Urn* sütun.</span><span class="sxs-lookup"><span data-stu-id="8d337-141">toodeploy a VM using a specific image, take note of hello value in hello *Urn* column.</span></span> <span data-ttu-id="8d337-142">Merhaba görüntü belirtirken, hello görüntü sürüm numarası ile "son", hangi hello dağıtım en son sürümünü hello seçer değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="8d337-142">When specifying hello image, hello image version number can be replaced with “latest”, which selects hello latest version of hello distribution.</span></span> <span data-ttu-id="8d337-143">Bu örnekte, hello `--image` kullanılan toospecify hello en son sürümünü CentOS 6.5 görüntü değişkendir.</span><span class="sxs-lookup"><span data-stu-id="8d337-143">In this example, hello `--image` argument is used toospecify hello latest version of a CentOS 6.5 image.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="8d337-144">VM boyutları anlama</span><span class="sxs-lookup"><span data-stu-id="8d337-144">Understand VM sizes</span></span>

<span data-ttu-id="8d337-145">Bir sanal makine boyutu, kullanılabilir toohello sanal makine yapılan işlem kaynaklarını CPU, GPU ve bellek gibi hello miktarını belirler.</span><span class="sxs-lookup"><span data-stu-id="8d337-145">A virtual machine size determines hello amount of compute resources such as CPU, GPU, and memory that are made available toohello virtual machine.</span></span> <span data-ttu-id="8d337-146">Sanal makinelerin beklendiği hello iş yükü için uygun şekilde boyutlandırılmış toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="8d337-146">Virtual machines need toobe sized appropriately for hello expected work load.</span></span> <span data-ttu-id="8d337-147">İş yükü artarsa, var olan bir sanal makine yeniden boyutlandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="8d337-147">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="8d337-148">VM boyutları</span><span class="sxs-lookup"><span data-stu-id="8d337-148">VM Sizes</span></span>

<span data-ttu-id="8d337-149">Aşağıdaki tablonun hello boyutları kullanım örneklerine kategorilere ayırır.</span><span class="sxs-lookup"><span data-stu-id="8d337-149">hello following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="8d337-150">Tür</span><span class="sxs-lookup"><span data-stu-id="8d337-150">Type</span></span>                     | <span data-ttu-id="8d337-151">Boyutlar</span><span class="sxs-lookup"><span data-stu-id="8d337-151">Sizes</span></span>           |    <span data-ttu-id="8d337-152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8d337-152">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="8d337-153">Genel amaçlı</span><span class="sxs-lookup"><span data-stu-id="8d337-153">General purpose</span></span>](sizes-general.md)         |<span data-ttu-id="8d337-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="8d337-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="8d337-155">Dengeli CPU bellekten.</span><span class="sxs-lookup"><span data-stu-id="8d337-155">Balanced CPU-to-memory.</span></span> <span data-ttu-id="8d337-156">Geliştirme için ideal / test ve küçük toomedium uygulamaları ve verileri çözümler.</span><span class="sxs-lookup"><span data-stu-id="8d337-156">Ideal for dev / test and small toomedium applications and data solutions.</span></span>  |
| [<span data-ttu-id="8d337-157">İşlem için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="8d337-157">Compute optimized</span></span>](sizes-compute.md)   | <span data-ttu-id="8d337-158">FS, F</span><span class="sxs-lookup"><span data-stu-id="8d337-158">Fs, F</span></span>             | <span data-ttu-id="8d337-159">Yüksek CPU bellekten.</span><span class="sxs-lookup"><span data-stu-id="8d337-159">High CPU-to-memory.</span></span> <span data-ttu-id="8d337-160">Orta düzey trafik uygulamalar, ağ uygulamaları ve toplu işlemler için iyidir.</span><span class="sxs-lookup"><span data-stu-id="8d337-160">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| [<span data-ttu-id="8d337-161">Bellek için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="8d337-161">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)    | <span data-ttu-id="8d337-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="8d337-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="8d337-163">Yüksek bellek için-çekirdek.</span><span class="sxs-lookup"><span data-stu-id="8d337-163">High memory-to-core.</span></span> <span data-ttu-id="8d337-164">İlişkisel veritabanları, Orta toolarge önbellekleri ve bellek içi analizi için mükemmel.</span><span class="sxs-lookup"><span data-stu-id="8d337-164">Great for relational databases, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="8d337-165">Depolama için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="8d337-165">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)      | <span data-ttu-id="8d337-166">Ls</span><span class="sxs-lookup"><span data-stu-id="8d337-166">Ls</span></span>                | <span data-ttu-id="8d337-167">Yüksek disk aktarım hızı ve GÇ.</span><span class="sxs-lookup"><span data-stu-id="8d337-167">High disk throughput and IO.</span></span> <span data-ttu-id="8d337-168">Büyük Veri, SQL ve NoSQL veritabanları için ideal.</span><span class="sxs-lookup"><span data-stu-id="8d337-168">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="8d337-169">GPU</span><span class="sxs-lookup"><span data-stu-id="8d337-169">GPU</span></span>](sizes-gpu.md)          | <span data-ttu-id="8d337-170">NV, NC</span><span class="sxs-lookup"><span data-stu-id="8d337-170">NV, NC</span></span>            | <span data-ttu-id="8d337-171">Yoğun Grafik işleme ve video düzenleme için hedeflenen özel VM'ler.</span><span class="sxs-lookup"><span data-stu-id="8d337-171">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| [<span data-ttu-id="8d337-172">Yüksek performans</span><span class="sxs-lookup"><span data-stu-id="8d337-172">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="8d337-173">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="8d337-173">H, A8-11</span></span>          | <span data-ttu-id="8d337-174">Bizim en güçlü CPU VM'ler isteğe bağlı yüksek verimlilik ağ arabirimlerine (RDMA) sahip.</span><span class="sxs-lookup"><span data-stu-id="8d337-174">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="8d337-175">Kullanılabilir VM boyutları Bul</span><span class="sxs-lookup"><span data-stu-id="8d337-175">Find available VM sizes</span></span>

<span data-ttu-id="8d337-176">toosee VM listesi boyutları kullanılabilen belirli bir bölgede, hello kullan [az vm listesi-boyutları](/cli/azure/vm#list-sizes) komutu.</span><span class="sxs-lookup"><span data-stu-id="8d337-176">toosee a list of VM sizes available in a particular region, use hello [az vm list-sizes](/cli/azure/vm#list-sizes) command.</span></span> 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

<span data-ttu-id="8d337-177">Kısmi çıktı:</span><span class="sxs-lookup"><span data-stu-id="8d337-177">Partial output:</span></span>

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

### <a name="create-vm-with-specific-size"></a><span data-ttu-id="8d337-178">Belirli boyutuyla VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="8d337-178">Create VM with specific size</span></span>

<span data-ttu-id="8d337-179">Merhaba önceki VM oluşturma örnekte, bir boyut değil sağlanmadığından, varsayılan boyutu sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="8d337-179">In hello previous VM creation example, a size was not provided, which results in a default size.</span></span> <span data-ttu-id="8d337-180">Oluşturma zamanı kullanarak bir VM boyutu seçilebilir [az vm oluşturma](/cli/azure/vm#create) ve hello `--size` bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="8d337-180">A VM size can be selected at creation time using [az vm create](/cli/azure/vm#create) and hello `--size` argument.</span></span> 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a><span data-ttu-id="8d337-181">VM’yi yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="8d337-181">Resize a VM</span></span>

<span data-ttu-id="8d337-182">Bir VM dağıtıldıktan sonra onu yeniden boyutlandırılan tooincrease olması veya kaynak ayırma azaltın.</span><span class="sxs-lookup"><span data-stu-id="8d337-182">After a VM has been deployed, it can be resized tooincrease or decrease resource allocation.</span></span>

<span data-ttu-id="8d337-183">Merhaba istenen boyuta hello geçerli Azure kümede kullanılabilir durumdaysa bir VM'yi yeniden boyutlandırılırken önce denetleyin.</span><span class="sxs-lookup"><span data-stu-id="8d337-183">Before resizing a VM, check if hello desired size is available on hello current Azure cluster.</span></span> <span data-ttu-id="8d337-184">Merhaba [az vm listesi-vm-yeniden boyutlandırma-seçenekleri](/cli/azure/vm#list-vm-resize-options) döndürür hello boyutlarının listesi komutu.</span><span class="sxs-lookup"><span data-stu-id="8d337-184">hello [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options) command returns hello list of sizes.</span></span> 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
<span data-ttu-id="8d337-185">Merhaba boyutu kullanılabilir isterseniz, hello işlemi sırasında yeniden başlatılıncaya kadar ancak hello VM bir gücü açma durumundan yeniden boyutlandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="8d337-185">If hello desired size is available, hello VM can be resized from a powered-on state, however it is rebooted during hello operation.</span></span> <span data-ttu-id="8d337-186">Kullanım hello [az VM'yi yeniden boyutlandırın]( /cli/azure/vm#resize) komutu tooperform hello yeniden boyutlandırın.</span><span class="sxs-lookup"><span data-stu-id="8d337-186">Use hello [az vm resize]( /cli/azure/vm#resize) command tooperform hello resize.</span></span>

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

<span data-ttu-id="8d337-187">Merhaba istenen boyut hello geçerli kümede hello VM hello yeniden boyutlandırma önce işlemi serbest toobe oluşabilir gereksinimlerini değildir.</span><span class="sxs-lookup"><span data-stu-id="8d337-187">If hello desired size is not on hello current cluster, hello VM needs toobe deallocated before hello resize operation can occur.</span></span> <span data-ttu-id="8d337-188">Kullanım hello [az vm serbest bırakma]( /cli/azure/vm#deallocate) komut toostop ve hello VM serbest bırakma.</span><span class="sxs-lookup"><span data-stu-id="8d337-188">Use hello [az vm deallocate]( /cli/azure/vm#deallocate) command toostop and deallocate hello VM.</span></span> <span data-ttu-id="8d337-189">Merhaba, Not VM geri desteklenir, hello geçici diskteki tüm verilerin kaldırılmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="8d337-189">Note, when hello VM is powered back on, any data on hello temp disk may be removed.</span></span> <span data-ttu-id="8d337-190">Merhaba genel IP adresi statik bir IP adresi kullanılmadığı sürece da değişir.</span><span class="sxs-lookup"><span data-stu-id="8d337-190">hello public IP address also changes unless a static IP address is being used.</span></span> 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

<span data-ttu-id="8d337-191">Serbest sonra hello boyutlandırma ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="8d337-191">Once deallocated, hello resize can occur.</span></span> 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

<span data-ttu-id="8d337-192">Merhaba yeniden boyutlandırıldıktan sonra hello VM başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="8d337-192">After hello resize, hello VM can be started.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a><span data-ttu-id="8d337-193">VM güç durumları</span><span class="sxs-lookup"><span data-stu-id="8d337-193">VM power states</span></span>

<span data-ttu-id="8d337-194">Bir Azure VM birçok güç durumlarını birine sahip.</span><span class="sxs-lookup"><span data-stu-id="8d337-194">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="8d337-195">Bu durum hello hiper yönetici hello açısından hello VM hello geçerli durumunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="8d337-195">This state represents hello current state of hello VM from hello standpoint of hello hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="8d337-196">Güç durumları</span><span class="sxs-lookup"><span data-stu-id="8d337-196">Power states</span></span>

| <span data-ttu-id="8d337-197">Güç durumu</span><span class="sxs-lookup"><span data-stu-id="8d337-197">Power State</span></span> | <span data-ttu-id="8d337-198">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8d337-198">Description</span></span>
|----|----|
| <span data-ttu-id="8d337-199">Başlangıç</span><span class="sxs-lookup"><span data-stu-id="8d337-199">Starting</span></span> | <span data-ttu-id="8d337-200">Merhaba sanal makinenin başlatıldığı gösterir.</span><span class="sxs-lookup"><span data-stu-id="8d337-200">Indicates hello virtual machine is being started.</span></span> |
| <span data-ttu-id="8d337-201">Çalışıyor</span><span class="sxs-lookup"><span data-stu-id="8d337-201">Running</span></span> | <span data-ttu-id="8d337-202">Merhaba sanal makinenin çalışmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="8d337-202">Indicates that hello virtual machine is running.</span></span> |
| <span data-ttu-id="8d337-203">Durduruluyor</span><span class="sxs-lookup"><span data-stu-id="8d337-203">Stopping</span></span> | <span data-ttu-id="8d337-204">Bu hello sanal makinenin durdurulması gösterir.</span><span class="sxs-lookup"><span data-stu-id="8d337-204">Indicates that hello virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="8d337-205">Durduruldu</span><span class="sxs-lookup"><span data-stu-id="8d337-205">Stopped</span></span> | <span data-ttu-id="8d337-206">Bu hello sanal makine durdurulduğunda gösterir.</span><span class="sxs-lookup"><span data-stu-id="8d337-206">Indicates that hello virtual machine is stopped.</span></span> <span data-ttu-id="8d337-207">Sanal makineler hello durdurulmuş durumda hala işlem ücretleri.</span><span class="sxs-lookup"><span data-stu-id="8d337-207">Virtual machines in hello stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="8d337-208">Ayırmayı kaldırma</span><span class="sxs-lookup"><span data-stu-id="8d337-208">Deallocating</span></span> | <span data-ttu-id="8d337-209">Merhaba sanal makinenin serbest gösterir.</span><span class="sxs-lookup"><span data-stu-id="8d337-209">Indicates that hello virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="8d337-210">Serbest bırakıldı</span><span class="sxs-lookup"><span data-stu-id="8d337-210">Deallocated</span></span> | <span data-ttu-id="8d337-211">Merhaba sanal makinenin hello hiper Yöneticisi'nden kaldırıldı ancak hello denetim düzlemi hala kullanılabilir olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="8d337-211">Indicates that hello virtual machine is removed from hello hypervisor but still available in hello control plane.</span></span> <span data-ttu-id="8d337-212">Merhaba Deallocated durumu içindeki sanal makineler bilgi işlem ücretleri değil.</span><span class="sxs-lookup"><span data-stu-id="8d337-212">Virtual machines in hello Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="8d337-213">Merhaba güç hello sanal makinenin durumunu bilinmediğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="8d337-213">Indicates that hello power state of hello virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="8d337-214">Güç durumu Bul</span><span class="sxs-lookup"><span data-stu-id="8d337-214">Find power state</span></span>

<span data-ttu-id="8d337-215">belirli bir VM, kullanım hello tooretrieve hello durumu [az vm örnek görünümünü Al](/cli/azure/vm#get-instance-view) komutu.</span><span class="sxs-lookup"><span data-stu-id="8d337-215">tooretrieve hello state of a particular VM, use hello [az vm get instance-view](/cli/azure/vm#get-instance-view) command.</span></span> <span data-ttu-id="8d337-216">Emin toospecify bir sanal makine ve kaynak grubu için geçerli bir ad olabilir.</span><span class="sxs-lookup"><span data-stu-id="8d337-216">Be sure toospecify a valid name for a virtual machine and resource group.</span></span> 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

<span data-ttu-id="8d337-217">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="8d337-217">Output:</span></span>

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a><span data-ttu-id="8d337-218">Yönetim görevleri</span><span class="sxs-lookup"><span data-stu-id="8d337-218">Management tasks</span></span>

<span data-ttu-id="8d337-219">Merhaba yaşam döngüsü sırasında sanal makinenin, başlatma, durdurma veya bir sanal makine silme gibi yönetim görevleri toorun isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d337-219">During hello life-cycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="8d337-220">Ayrıca, toocreate, komut dosyaları tooautomate yineleyen veya karmaşık görevleri isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d337-220">Additionally, you may want toocreate scripts tooautomate repetitive or complex tasks.</span></span> <span data-ttu-id="8d337-221">Hello Azure CLI kullanarak, birçok ortak yönetim görevlerinin hello komut satırından veya komut dosyalarında çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d337-221">Using hello Azure CLI, many common management tasks can be run from hello command line or in scripts.</span></span> 

### <a name="get-ip-address"></a><span data-ttu-id="8d337-222">IP adresi al</span><span class="sxs-lookup"><span data-stu-id="8d337-222">Get IP address</span></span>

<span data-ttu-id="8d337-223">Bu komut, bir sanal makinenin hello özel ve genel IP adresleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="8d337-223">This command returns hello private and public IP addresses of a virtual machine.</span></span>  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a><span data-ttu-id="8d337-224">Sanal makineyi durdurma</span><span class="sxs-lookup"><span data-stu-id="8d337-224">Stop virtual machine</span></span>

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a><span data-ttu-id="8d337-225">Sanal makineyi Başlat</span><span class="sxs-lookup"><span data-stu-id="8d337-225">Start virtual machine</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="8d337-226">Kaynak grubunu silme</span><span class="sxs-lookup"><span data-stu-id="8d337-226">Delete resource group</span></span>

<span data-ttu-id="8d337-227">Bir kaynak grubunu silme içinde içerdiği tüm kaynaklar da siler.</span><span class="sxs-lookup"><span data-stu-id="8d337-227">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a><span data-ttu-id="8d337-228">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8d337-228">Next steps</span></span>

<span data-ttu-id="8d337-229">Bu öğreticide, temel VM oluşturmayı ve yönetmeyi nasıl gibi hakkında öğrenilen:</span><span class="sxs-lookup"><span data-stu-id="8d337-229">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8d337-230">Oluştur ve tooa VM Bağlan</span><span class="sxs-lookup"><span data-stu-id="8d337-230">Create and connect tooa VM</span></span>
> * <span data-ttu-id="8d337-231">Seçin ve VM görüntüleri kullanmak</span><span class="sxs-lookup"><span data-stu-id="8d337-231">Select and use VM images</span></span>
> * <span data-ttu-id="8d337-232">Görüntüleme ve belirli VM boyutları kullanma</span><span class="sxs-lookup"><span data-stu-id="8d337-232">View and use specific VM sizes</span></span>
> * <span data-ttu-id="8d337-233">VM’yi yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="8d337-233">Resize a VM</span></span>
> * <span data-ttu-id="8d337-234">Görüntüleyin ve VM durumunu anlamak</span><span class="sxs-lookup"><span data-stu-id="8d337-234">View and understand VM state</span></span>

<span data-ttu-id="8d337-235">Toohello sonraki öğretici toolearn VM disklerle ilgili ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="8d337-235">Advance toohello next tutorial toolearn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="8d337-236">Oluşturma ve yönetme VM diskleri</span><span class="sxs-lookup"><span data-stu-id="8d337-236">Create and Manage VM disks</span></span>](./tutorial-manage-disks.md)
