---
title: "aaaUpload veya Azure CLI 2.0 ile özel bir Linux VM Kopyala | Microsoft Docs"
description: "Karşıya yükleme veya özelleştirilmiş bir sanal makine hello Resource Manager dağıtım modeli ve hello Azure CLI 2.0 kullanarak kopyalayın"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 79af897120a6ba7f4a427ba6c7d0c31b7b870bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a><span data-ttu-id="0c451-103">Hello Azure CLI 2.0 ile özel diskten bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="0c451-103">Create a Linux VM from custom disk with hello Azure CLI 2.0</span></span>

<!-- rename toocreate-vm-specialized -->

<span data-ttu-id="0c451-104">Bu makale size nasıl gösterir tooupload özelleştirilmiş bir sanal sabit disk (VHD) veya kopyalayın bir varolan bir VHD'yi azure'da hello özel diskten yeni Linux sanal makineleri (VM'ler) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0c451-104">This article shows you how tooupload a customized virtual hard disk (VHD) or copy a an existing VHD in Azure and create new Linux virtual machines (VMs) from hello custom disk.</span></span> <span data-ttu-id="0c451-105">Yükleme ve Linux distro tooyour gereksinimleri yapılandırabilir ve ardından bu VHD kullanmak tooquickly yeni bir Azure sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0c451-105">You can install and configure a Linux distro tooyour requirements and then use that VHD tooquickly create a new Azure virtual machine.</span></span>

<span data-ttu-id="0c451-106">Özelleştirilmiş diskinizden birden çok VM toocreate istiyorsanız, görüntü, VM veya VHD oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c451-106">If you want toocreate multiple VMs from your customized disk, you should create an image from your VM or VHD.</span></span> <span data-ttu-id="0c451-107">Daha fazla bilgi için bkz: [hello CLI kullanarak bir Azure VM özel bir görüntü oluşturun](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="0c451-107">For more information, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>

<span data-ttu-id="0c451-108">İki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="0c451-108">You have two options:</span></span>
* [<span data-ttu-id="0c451-109">Bir VHD’yi karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="0c451-109">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="0c451-110">Mevcut bir Azure VM'yi kopyalama</span><span class="sxs-lookup"><span data-stu-id="0c451-110">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a><span data-ttu-id="0c451-111">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="0c451-111">Quick commands</span></span>

<span data-ttu-id="0c451-112">Kullanarak yeni bir VM oluştururken [az vm oluşturma](/cli/azure/vm#create) özelleştirilmiş veya özelleştirilmiş bir diskten, **attach** hello disk (--attach-os-disk) yerine bir özel veya Market görüntüsü belirtme (--görüntü).</span><span class="sxs-lookup"><span data-stu-id="0c451-112">When creating a new VM using [az vm create](/cli/azure/vm#create) from a customized or specialized disk you **attach** hello disk (--attach-os-disk) instead of specifying a custom or marketplace image (--image).</span></span> <span data-ttu-id="0c451-113">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM* yönetilen adlı disk hello kullanarak *myManagedDisk* özelleştirilmiş VHD'den oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="0c451-113">hello following example creates a VM named *myVM* using hello managed disk named *myManagedDisk* created from your customized VHD:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a><span data-ttu-id="0c451-114">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="0c451-114">Requirements</span></span>
<span data-ttu-id="0c451-115">toocomplete hello adımları izleyerek gerekir:</span><span class="sxs-lookup"><span data-stu-id="0c451-115">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="0c451-116">Azure kullanıma hazır bir Linux sanal makine.</span><span class="sxs-lookup"><span data-stu-id="0c451-116">A Linux virtual machine that has been prepared for use in Azure.</span></span> <span data-ttu-id="0c451-117">Merhaba [hazırlama hello VM](#prepare-the-vm) bu makalenin ele alınmaktadır nasıl toofind distro belirli bilgiler yükleme Merhaba, toobe mümkün tooconnect ve düzgün şekilde azure'da hello VM toowork için gerekli olan Azure Linux Aracısı (waagent) SSH kullanarak tooit.</span><span class="sxs-lookup"><span data-stu-id="0c451-117">hello [Prepare hello VM](#prepare-the-vm) section of this article covers how toofind distro specific information on installing hello Azure Linux Agent (waagent) which is required for hello VM toowork properly in Azure and for you toobe able tooconnect tooit using SSH.</span></span>
* <span data-ttu-id="0c451-118">Mevcut bir kümeden hello VHD dosyasını [Linux Azure destekli dağıtım](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (veya bkz [desteklenmeyen dağıtımlarla bilgi](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa hello VHD biçiminde sanal disk.</span><span class="sxs-lookup"><span data-stu-id="0c451-118">hello VHD file from an existing [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="0c451-119">Birden çok araç, bir VM ve VHD toocreate mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="0c451-119">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="0c451-120">Yükleme ve yapılandırma [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) veya [KVM](http://www.linux-kvm.org/page/RunningKVM), toouse VHD, resim biçimi olarak ayırdığınız dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="0c451-120">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="0c451-121">Gerekirse, [bir görüntüyü dönüştürme](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) kullanarak **qemu img Dönüştür**.</span><span class="sxs-lookup"><span data-stu-id="0c451-121">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using **qemu-img convert**.</span></span>
  * <span data-ttu-id="0c451-122">Hyper-V de kullanabilirsiniz [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) veya [Windows Server 2012/2012 R2 üzerinde](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c451-122">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="0c451-123">Azure'da Hello yeni VHDX biçimi desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="0c451-123">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="0c451-124">Bir VM oluşturun, VHD'yi hello biçiminde belirtin.</span><span class="sxs-lookup"><span data-stu-id="0c451-124">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="0c451-125">Gerekirse, VHDX diskleri tooVHD kullanarak dönüştürebilirsiniz [qemu img Dönüştür](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) veya hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0c451-125">If needed, you can convert VHDX disks tooVHD using [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="0c451-126">Ayrıca, Azure tooconvert gerekir böylece dinamik VHD karşıya böyle diskleri toostatic VHD yüklemeden önce desteklemez.</span><span class="sxs-lookup"><span data-stu-id="0c451-126">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="0c451-127">Araçları gibi kullanabilir [Git için Azure VHD yardımcı programları](https://github.com/Microsoft/azure-vhd-utils-for-go) hello tooAzure karşıya yükleme işlemi sırasında tooconvert dinamik diskler.</span><span class="sxs-lookup"><span data-stu-id="0c451-127">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 


* <span data-ttu-id="0c451-128">Merhaba son olduğundan emin olun [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="0c451-128">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="0c451-129">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0c451-129">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="0c451-130">Örnek parametre adları dahil *myResourceGroup*, *mystorageaccount*, ve *mydisks*.</span><span class="sxs-lookup"><span data-stu-id="0c451-130">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *mydisks*.</span></span>

<span data-ttu-id="0c451-131"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="0c451-131"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-vm"></a><span data-ttu-id="0c451-132">Merhaba VM hazırlama</span><span class="sxs-lookup"><span data-stu-id="0c451-132">Prepare hello VM</span></span>

<span data-ttu-id="0c451-133">Azure çeşitli Linux dağıtımları destekler (bkz [destekli dağıtımlar](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="0c451-133">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="0c451-134">aşağıdaki makaleleri hello size nasıl tooprepare hello Azure üzerinde desteklenen çeşitli Linux dağıtımları yol:</span><span class="sxs-lookup"><span data-stu-id="0c451-134">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* [<span data-ttu-id="0c451-135">CentOS tabanlı dağıtımlar</span><span class="sxs-lookup"><span data-stu-id="0c451-135">CentOS-based Distributions</span></span>](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0c451-136">Debian Linux</span><span class="sxs-lookup"><span data-stu-id="0c451-136">Debian Linux</span></span>](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0c451-137">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="0c451-137">Oracle Linux</span></span>](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0c451-138">Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="0c451-138">Red Hat Enterprise Linux</span></span>](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0c451-139">SLES & openSUSE</span><span class="sxs-lookup"><span data-stu-id="0c451-139">SLES & openSUSE</span></span>](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0c451-140">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="0c451-140">Ubuntu</span></span>](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0c451-141">Diğer - desteklenmeyen dağıtımlarla</span><span class="sxs-lookup"><span data-stu-id="0c451-141">Other - Non-Endorsed Distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="0c451-142">Ayrıca bkz. hello [Linux yükleme notları](create-upload-generic.md#general-linux-installation-notes) için Azure Linux görüntüleri hazırlama hakkında daha fazla genel ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="0c451-142">Also see hello [Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="0c451-143">Merhaba [Azure platformu SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) içinde ne zaman hello birini destekli dağıtımlar 'Sürümleri desteklenir' altında belirtildiği gibi hello yapılandırma ayrıntıları ile kullanılan yalnızca Linux çalıştıran tooVMs geçerlidir [Azure destekli Linux'ta Dağıtımları](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0c451-143">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="option-1-upload-a-vhd"></a><span data-ttu-id="0c451-144">Seçenek 1: bir VHD yüklemek</span><span class="sxs-lookup"><span data-stu-id="0c451-144">Option 1: Upload a VHD</span></span>

<span data-ttu-id="0c451-145">Yerel makinede çalışıyor olması veya başka bir buluttan dışarı özelleştirilmiş bir VHD'yi yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c451-145">You can upload a customized VHD that you have running on a local machine or that you exported from another cloud.</span></span> <span data-ttu-id="0c451-146">toouse hello VHD toocreate yeni bir Azure VM, gereksinim duyduğunuz tooupload hello VHD tooa depolama hesabı ve VHD hello yönetilen bir disk oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0c451-146">toouse hello VHD toocreate a new Azure VM, you need tooupload hello VHD tooa storage account and create a managed disk from hello VHD.</span></span> 

### <a name="create-a-resource-group"></a><span data-ttu-id="0c451-147">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="0c451-147">Create a resource group</span></span>

<span data-ttu-id="0c451-148">Özel diskinizin karşıya yükleme ve sanal makineleri oluşturma önce ilk toocreate sahip bir kaynak grubu gerek [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="0c451-148">Before uploading your custom disk and creating VMs, you first need toocreate a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="0c451-149">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu: [Azure yönetilen diskleri genel bakış](../windows/managed-disks-overview.md)</span><span class="sxs-lookup"><span data-stu-id="0c451-149">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location: [Azure Managed Disks overview](../windows/managed-disks-overview.md)</span></span>
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a><span data-ttu-id="0c451-150">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0c451-150">Create a storage account</span></span>

<span data-ttu-id="0c451-151">Özel disk ve VM'lerin için depolama hesabı oluşturma [az depolama hesabı oluşturma](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="0c451-151">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> 

<span data-ttu-id="0c451-152">Merhaba aşağıdaki örnek adlı bir depolama hesabı oluşturur *mystorageaccount* daha önce oluşturduğunuz hello kaynak grubunda:</span><span class="sxs-lookup"><span data-stu-id="0c451-152">hello following example creates a storage account named *mystorageaccount* in hello resource group previously created:</span></span>

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a><span data-ttu-id="0c451-153">Depolama hesabı anahtarlarını Listele</span><span class="sxs-lookup"><span data-stu-id="0c451-153">List storage account keys</span></span>
<span data-ttu-id="0c451-154">Azure her depolama hesabı için iki 512 bit erişim tuşu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0c451-154">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="0c451-155">Bu erişim anahtarlarını yazma işlemleri gerçekleştirme gibi toohello depolama hesabı kimlik doğrulaması yapılırken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0c451-155">These access keys are used when authenticating toohello storage account, like carrying out write operations.</span></span> <span data-ttu-id="0c451-156">Daha fazla bilgi edinin [yönetme erişimi burada toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="0c451-156">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="0c451-157">İle Merhaba erişim tuşlarını görüntüleme [az depolama hesabı anahtarları listesi](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="0c451-157">You view hello access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="0c451-158">Görünüm hello erişim tuşları oluşturduğunuz hello depolama hesabı için:</span><span class="sxs-lookup"><span data-stu-id="0c451-158">View hello access keys for hello storage account you created:</span></span>

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

<span data-ttu-id="0c451-159">Merhaba çıkış benzer:</span><span class="sxs-lookup"><span data-stu-id="0c451-159">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="0c451-160">Not **key1** hello sonraki adımlarda depolama hesabınıza toointeract kullanacak şekilde.</span><span class="sxs-lookup"><span data-stu-id="0c451-160">Make a note of **key1** as you will use it toointeract with your storage account in hello next steps.</span></span>

### <a name="create-a-storage-container"></a><span data-ttu-id="0c451-161">Depolama kapsayıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0c451-161">Create a storage container</span></span>
<span data-ttu-id="0c451-162">Hello farklı dizinleri toologically oluşturduğunuz aynı şekilde düzenlemek, yerel dosya sistemi, disklerinizi bir depolama hesabı tooorganize kapsayıcılara oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0c451-162">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your disks.</span></span> <span data-ttu-id="0c451-163">Bir depolama hesabı kapsayıcıların herhangi bir sayı içerebilir.</span><span class="sxs-lookup"><span data-stu-id="0c451-163">A storage account can contain any number of containers.</span></span> <span data-ttu-id="0c451-164">İle bir kapsayıcı oluşturmak [az depolama kapsayıcısı oluşturmak](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="0c451-164">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="0c451-165">Merhaba aşağıdaki örnek adlı bir kapsayıcı oluşturur *mydisks*:</span><span class="sxs-lookup"><span data-stu-id="0c451-165">hello following example creates a container named *mydisks*:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a><span data-ttu-id="0c451-166">Merhaba VHD karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="0c451-166">Upload hello VHD</span></span>
<span data-ttu-id="0c451-167">Şimdi özel diskiniz ile karşıya [az depolama blob karşıya yükleme](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="0c451-167">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="0c451-168">Karşıya yükleme ve özel diskinizin bir sayfa blob'u olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="0c451-168">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="0c451-169">Erişim anahtarı, hello önceki adımda oluşturduğunuz hello kapsayıcısı belirtin ve yerel bilgisayarınızdaki yolu toohello özel diske hello:</span><span class="sxs-lookup"><span data-stu-id="0c451-169">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
<span data-ttu-id="0c451-170">Karşıya yükleme hello VHD biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="0c451-170">Uploading hello VHD may take a while.</span></span>

### <a name="create-a-managed-disk"></a><span data-ttu-id="0c451-171">Yönetilen bir disk oluşturma</span><span class="sxs-lookup"><span data-stu-id="0c451-171">Create a managed disk</span></span>


<span data-ttu-id="0c451-172">VHD hello kullanılarak yönetilen bir disk oluşturmak [az disketi](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="0c451-172">Create a managed disk from hello VHD using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="0c451-173">Merhaba aşağıdaki örnekte oluşturur adlı Yönetilen bir disk *myManagedDisk* VHD hello depolama hesabı ve kapsayıcı adlı tooyour karşıya:</span><span class="sxs-lookup"><span data-stu-id="0c451-173">hello following example creates a managed disk named *myManagedDisk* from hello VHD you uploaded tooyour named storage account and container:</span></span>

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a><span data-ttu-id="0c451-174">Seçenek 2: mevcut bir VM'yi kopyalama</span><span class="sxs-lookup"><span data-stu-id="0c451-174">Option 2: Copy an existing VM</span></span>

<span data-ttu-id="0c451-175">Ayrıca oluşturabilirsiniz hello Azure'ı ve ardından kopya hello işletim sistemi diski özelleştirilmiş VM ve tooa yeni VM toocreate attach başka bir kopyası.</span><span class="sxs-lookup"><span data-stu-id="0c451-175">You can also create hello customized VM in Azure and then copy hello OS disk and attach it tooa new VM toocreate another copy.</span></span> <span data-ttu-id="0c451-176">Bu test etmek için uygundur, ancak birden çok yeni VM'ler için hello model olarak toouse mevcut bir Azure VM'i istiyorsanız, gerçekten oluşturmalısınız bir **görüntü** yerine.</span><span class="sxs-lookup"><span data-stu-id="0c451-176">This is fine for testing, but if you want toouse an existing Azure VM as hello model for multiple new VMs, you really should create an **image** instead.</span></span> <span data-ttu-id="0c451-177">Var olan bir Azure sanal makineden bir görüntü oluşturma hakkında daha fazla bilgi için bkz: [hello CLI kullanarak bir Azure VM özel bir görüntü oluşturun](tutorial-custom-images.md)</span><span class="sxs-lookup"><span data-stu-id="0c451-177">For more information about creating an image from an existing Azure VM, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md)</span></span>

### <a name="create-a-snapshot"></a><span data-ttu-id="0c451-178">Bir anlık görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="0c451-178">Create a snapshot</span></span>

<span data-ttu-id="0c451-179">Bu örnek, adlandırılmış bir VM'nin bir anlık görüntü oluşturur *myVM* kaynak grubunda *myResourceGroup* ve adında bir anlık görüntü oluşturur *osDiskSnapshot*.</span><span class="sxs-lookup"><span data-stu-id="0c451-179">This example creates a snapshot of a VM named *myVM* in resource group *myResourceGroup* and creates a snapshot named *osDiskSnapshot*.</span></span>

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a><span data-ttu-id="0c451-180">Merhaba yönetilen disketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="0c451-180">Create hello managed disk</span></span>

<span data-ttu-id="0c451-181">Yeni bir yönetilen disk hello anlık görüntüden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0c451-181">Create a new managed disk from hello snapshot.</span></span>

<span data-ttu-id="0c451-182">Başlangıç anlık görüntü Hello Kimliğini alın.</span><span class="sxs-lookup"><span data-stu-id="0c451-182">Get hello ID of hello snapshot.</span></span> <span data-ttu-id="0c451-183">Bu örnekte, hello anlık görüntü adlı *osDiskSnapshot* ve hello *myResourceGroup* kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="0c451-183">In this example, hello snapshot is named *osDiskSnapshot* and it is in hello *myResourceGroup* resource group.</span></span>

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

<span data-ttu-id="0c451-184">Merhaba yönetilen diski oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0c451-184">Create hello managed disk.</span></span> <span data-ttu-id="0c451-185">Bu örnekte, adında yönetilen bir disk oluşturacağız *myManagedDisk* bizim anlık görüntüden 128 GB boyutunda standart depolama olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="0c451-185">In this example, we will create a managed disk named *myManagedDisk* from our snapshot, that is 128GB in size in standard storage.</span></span>

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a><span data-ttu-id="0c451-186">Merhaba VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="0c451-186">Create hello VM</span></span>

<span data-ttu-id="0c451-187">Şimdi, VM oluşturma [az vm oluşturma](/cli/azure/vm#create) ve ekleme (--attach-os-disk) hello yönetilen hello işletim sistemi diski olarak disk.</span><span class="sxs-lookup"><span data-stu-id="0c451-187">Now, create your VM with [az vm create](/cli/azure/vm#create) and attach (--attach-os-disk) hello managed disk as hello OS disk.</span></span> <span data-ttu-id="0c451-188">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myNewVM* hello kullanarak yönetilen karşıya yüklenen VHD'den oluşturduğunuz disk:</span><span class="sxs-lookup"><span data-stu-id="0c451-188">hello following example creates a VM named *myNewVM* using hello managed disk created from your uploaded VHD:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

<span data-ttu-id="0c451-189">Merhaba VM içine mümkün tooSSH olmalıdır VM hello kaynağından hello kimlik bilgilerini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="0c451-189">You should be able tooSSH into hello VM using hello credentials from hello source VM.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0c451-190">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0c451-190">Next steps</span></span>
<span data-ttu-id="0c451-191">Hazır ve özel sanal diskinizin karşıya sonra daha fazla bilgi edinebilirsiniz [Resource Manager ve şablonlar kullanarak](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0c451-191">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="0c451-192">Ayrıca çok isteyebilir[bir veri diski Ekle](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour yeni VM'ler.</span><span class="sxs-lookup"><span data-stu-id="0c451-192">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="0c451-193">Tooaccess gerekir, Vm'lerde çalışan uygulamalarınız varsa, mutlaka çok[açık bağlantı noktalarını ve uç noktaları](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0c451-193">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

