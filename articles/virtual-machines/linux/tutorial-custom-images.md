---
title: "hello Azure CLI ile özel VM görüntüleri aaaCreate | Microsoft Docs"
description: "Öğretici - hello Azure CLI kullanarak özel bir VM görüntüsü oluşturun."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/21/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 217a993c0c1d48939b74108ac6c5f7a1a619416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-hello-cli"></a><span data-ttu-id="ccb0f-103">Özel bir hello CLI kullanarak bir Azure VM görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="ccb0f-103">Create a custom image of an Azure VM using hello CLI</span></span>

<span data-ttu-id="ccb0f-104">Özel resimler gibi Market görüntülerini olsa da, bunları kendiniz oluşturmanız.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="ccb0f-105">Özel resimler gibi uygulamalar, uygulama yapılandırmaları ve diğer işletim sistemi yapılandırmalarını önceden kullanılan toobootstrap yapılandırmaları olabilir.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="ccb0f-106">Bu öğreticide, kendi özel görüntünüzü bir Azure sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="ccb0f-107">Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ccb0f-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ccb0f-108">Yetkisini kaldırma ve sanal makineleri generalize</span><span class="sxs-lookup"><span data-stu-id="ccb0f-108">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="ccb0f-109">Özel görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="ccb0f-109">Create a custom image</span></span>
> * <span data-ttu-id="ccb0f-110">Özel bir görüntüden bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="ccb0f-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="ccb0f-111">Aboneliğinizdeki tüm hello görüntüler liste</span><span class="sxs-lookup"><span data-stu-id="ccb0f-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="ccb0f-112">Bir görüntü Sil</span><span class="sxs-lookup"><span data-stu-id="ccb0f-112">Delete an image</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ccb0f-113">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="ccb0f-114">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ccb0f-115">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ccb0f-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="ccb0f-116">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="ccb0f-116">Before you begin</span></span>

<span data-ttu-id="ccb0f-117">Merhaba adımları tootake mevcut bir VM'yi ve onu yeniden kullanılabilir özel bir görüntü, etkinleştirin toocreate yeni VM örnekleri nasıl kullanabileceğinizi ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="ccb0f-118">Bu öğreticide toocomplete hello örnek, mevcut bir sanal makine olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="ccb0f-119">Gerekirse, bu [komut dosyası örneği](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) sizin için bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-119">If needed, this [script sample](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) can create one for you.</span></span> <span data-ttu-id="ccb0f-120">Çalışma hello öğretici aracılığıyla değiştirdiğinizde hello kaynak grubu VM adları ve gerektiğinde.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="create-a-custom-image"></a><span data-ttu-id="ccb0f-121">Özel görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="ccb0f-121">Create a custom image</span></span>

<span data-ttu-id="ccb0f-122">bir sanal makine görüntüsü toocreate, tooprepare hello VM sağlama kaldırmayı, serbest bırakma ve hello kaynak VM genelleştirilmiş olarak işaretleme gerekir.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-122">toocreate an image of a virtual machine, you need tooprepare hello VM by deprovisioning, deallocating, and then marking hello source VM as generalized.</span></span> <span data-ttu-id="ccb0f-123">Bir kez hello VM hazırlandı, bir görüntü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-123">Once hello VM has been prepared, you can create an image.</span></span>

### <a name="deprovision-hello-vm"></a><span data-ttu-id="ccb0f-124">Merhaba VM yetkisini kaldırma</span><span class="sxs-lookup"><span data-stu-id="ccb0f-124">Deprovision hello VM</span></span> 

<span data-ttu-id="ccb0f-125">Sağlamayı kaldırmayı hello VM makineye özgü bilgiler kaldırarak genelleştirir.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-125">Deprovisioning generalizes hello VM by removing machine-specific information.</span></span> <span data-ttu-id="ccb0f-126">İsteğe bağlı olarak bu Genelleştirme olası toodeploy yapar tek bir görüntüden birçok VM.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-126">This generalization makes it possible toodeploy many VMs from a single image.</span></span> <span data-ttu-id="ccb0f-127">Sağlama kaldırma sırasında hello ana bilgisayar adı çok sıfırlanır*localhost.localdomain*.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-127">During deprovisioning, hello host name is reset too*localhost.localdomain*.</span></span> <span data-ttu-id="ccb0f-128">SSH ana bilgisayar anahtarları, ad sunucusu yapılandırmaları, kök parolasını ve önbelleğe alınan DHCP kiralarını de silinir.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-128">SSH host keys, nameserver configurations, root password, and cached DHCP leases are also deleted.</span></span>

<span data-ttu-id="ccb0f-129">toodeprovision hello VM hello Azure VM Aracısı'nı (waagent) kullanın.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-129">toodeprovision hello VM, use hello Azure VM agent (waagent).</span></span> <span data-ttu-id="ccb0f-130">Hello Azure VM Aracısı VM hello üzerinde yüklü olduğundan ve sağlama ve Azure yapı denetleyicisi hello ile etkileşim yönetir.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-130">hello Azure VM agent is installed on hello VM and manages provisioning and interacting with hello Azure Fabric Controller.</span></span> <span data-ttu-id="ccb0f-131">Daha fazla bilgi için bkz: Merhaba [Azure Linux Aracısı Kullanıcı Kılavuzu](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="ccb0f-131">For more information, see hello [Azure Linux Agent user guide](agent-user-guide.md).</span></span>

<span data-ttu-id="ccb0f-132">Tooyour VM bağlanmak SSH ve çalışma hello komutu toodeprovision hello VM kullanma.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-132">Connect tooyour VM using SSH and run hello command toodeprovision hello VM.</span></span> <span data-ttu-id="ccb0f-133">Merhaba ile `+user` bağımsız değişkeni, hello son sağlanan kullanıcı hesabı ve tüm ilişkili veriler de silinir.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-133">With hello `+user` argument, hello last provisioned user account and any associated data are also deleted.</span></span> <span data-ttu-id="ccb0f-134">Merhaba örnek IP adresinin hello ortak IP adresini, VM ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-134">Replace hello example IP address with hello public IP address of your VM.</span></span>

<span data-ttu-id="ccb0f-135">SSH toohello VM.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-135">SSH toohello VM.</span></span>
```bash
ssh azureuser@52.174.34.95
```
<span data-ttu-id="ccb0f-136">Merhaba VM sağlamayı sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-136">Deprovision hello VM.</span></span>

```bash
sudo waagent -deprovision+user -force
```
<span data-ttu-id="ccb0f-137">Merhaba SSH oturumu kapatın.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-137">Close hello SSH session.</span></span>

```bash
exit
```

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="ccb0f-138">Deallocate ve hello VM genelleştirilmiş olarak işaretleyin</span><span class="sxs-lookup"><span data-stu-id="ccb0f-138">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="ccb0f-139">bir görüntü toocreate hello VM serbest toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-139">toocreate an image, hello VM needs toobe deallocated.</span></span> <span data-ttu-id="ccb0f-140">VM Hello kullanarak ayırması [az vm serbest bırakma](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="ccb0f-140">Deallocate hello VM using [az vm deallocate](/cli//azure/vm#deallocate).</span></span> 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="ccb0f-141">Son olarak, ayarlamak hello VM hello durumu ile genelleştirilmiş gibi [az vm generalize](/cli//azure/vm#generalize) hello Azure platformu VM genelleştirilmiş hello bilmesi için.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-141">Finally, set hello state of hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize) so hello Azure platform knows hello VM has been generalized.</span></span> <span data-ttu-id="ccb0f-142">Yalnızca genelleştirilmiş bir sanal makineden bir görüntü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-142">You can only create an image from a generalized VM.</span></span>
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-hello-image"></a><span data-ttu-id="ccb0f-143">Merhaba görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="ccb0f-143">Create hello image</span></span>

<span data-ttu-id="ccb0f-144">Merhaba VM görüntüsünü kullanarak oluşturabileceğiniz artık [az görüntü oluşturma](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="ccb0f-144">Now you can create an image of hello VM by using [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="ccb0f-145">Merhaba aşağıdaki örnekte oluşturur adlı bir resim *myImage* adlı bir VM'den *myVM*.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-145">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="ccb0f-146">Sanal makineleri hello görüntüden oluşturma</span><span class="sxs-lookup"><span data-stu-id="ccb0f-146">Create VMs from hello image</span></span>

<span data-ttu-id="ccb0f-147">Görüntüyü sahip olduğunuza göre bir veya daha fazla yeni VM'ler görüntü hello kullanarak oluşturabileceğiniz [az vm oluşturma](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="ccb0f-147">Now that you have an image, you can create one or more new VMs from hello image using [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="ccb0f-148">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVMfromImage* adlı hello görüntüden *myImage*.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-148">hello following example creates a VM named *myVMfromImage* from hello image named *myImage*.</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a><span data-ttu-id="ccb0f-149">Görüntü Yönetimi</span><span class="sxs-lookup"><span data-stu-id="ccb0f-149">Image management</span></span> 

<span data-ttu-id="ccb0f-150">İşte bazı örnekler ortak görüntü yönetim görevlerinin nasıl ve ne toocomplete bunları hello Azure CLI kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-150">Here are some examples of common image management tasks and how toocomplete them using hello Azure CLI.</span></span>

<span data-ttu-id="ccb0f-151">Tablo biçiminde ada göre tüm görüntüleri listeleyin.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-151">List all images by name in a table format.</span></span>

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

<span data-ttu-id="ccb0f-152">Görüntüyü silin.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-152">Delete an image.</span></span> <span data-ttu-id="ccb0f-153">Bu örnek siler hello adlı görüntü *myOldImage* hello gelen *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-153">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="ccb0f-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ccb0f-154">Next steps</span></span>

<span data-ttu-id="ccb0f-155">Bu öğreticide, özel bir VM görüntüsü oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-155">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="ccb0f-156">Size nasıl öğrenilen için:</span><span class="sxs-lookup"><span data-stu-id="ccb0f-156">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ccb0f-157">Yetkisini kaldırma ve sanal makineleri generalize</span><span class="sxs-lookup"><span data-stu-id="ccb0f-157">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="ccb0f-158">Özel görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="ccb0f-158">Create a custom image</span></span>
> * <span data-ttu-id="ccb0f-159">Özel bir görüntüden bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="ccb0f-159">Create a VM from a custom image</span></span>
> * <span data-ttu-id="ccb0f-160">Aboneliğinizdeki tüm hello görüntüler liste</span><span class="sxs-lookup"><span data-stu-id="ccb0f-160">List all hello images in your subscription</span></span>
> * <span data-ttu-id="ccb0f-161">Bir görüntü Sil</span><span class="sxs-lookup"><span data-stu-id="ccb0f-161">Delete an image</span></span>

<span data-ttu-id="ccb0f-162">Yüksek oranda kullanılabilir sanal makineler hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="ccb0f-162">Advance toohello next tutorial toolearn about highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="ccb0f-163">[Yüksek oranda kullanılabilir sanal makineleri oluşturmak](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="ccb0f-163">[Create highly available VMs](tutorial-availability-sets.md).</span></span>

