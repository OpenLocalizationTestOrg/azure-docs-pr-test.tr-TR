---
title: "Azure CLI 2.0 ile özel bir Linux disk aaaUpload | Microsoft Docs"
description: "Oluşturun ve hello Resource Manager dağıtım modeli ve hello Azure CLI 2.0 kullanarak bir sanal sabit disk (VHD) tooAzure yükleyin"
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
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: cf8556ab4dfe6c4e5eff4e99fe1ddc44393f774c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a><span data-ttu-id="55713-103">Karşıya yükleme ve hello Azure CLI 2.0 ile özel diskten bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="55713-103">Upload and create a Linux VM from custom disk with hello Azure CLI 2.0</span></span>
<span data-ttu-id="55713-104">Bu makalede nasıl tooupload bir sanal sabit disk (VHD) tooan Azure depolama hesabı hello Azure CLI 2.0 ile gösterir ve bu özel diskten Linux VM'ler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="55713-104">This article shows you how tooupload a virtual hard disk (VHD) tooan Azure storage account with hello Azure CLI 2.0 and create Linux VMs from this custom disk.</span></span> <span data-ttu-id="55713-105">Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="55713-105">You can also perform these steps with hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="55713-106">Bu işlev tooinstall sağlar ve Linux distro tooyour gereksinimlerini yapılandırmak ve ardından bu VHD tooquickly Azure sanal makineleri (VM'ler) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="55713-106">This functionality allows you tooinstall and configure a Linux distro tooyour requirements and then use that VHD tooquickly create Azure virtual machines (VMs).</span></span>

<span data-ttu-id="55713-107">Hello son VHD'ler, ancak aynı zamanda aşağıdaki adımları kullanarak yapabilirsiniz için bu konuda depolama hesapları kullanan [yönetilen diskleri](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="55713-107">This topic uses storage accounts for hello final VHDs, but you can also do these steps using [managed disks](upload-vhd.md).</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="55713-108">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="55713-108">Quick commands</span></span>
<span data-ttu-id="55713-109">Tooquickly gerekiyorsa hello görevi, hello bölüm ayrıntıları hello aşağıdaki komutları tooupload VHD tooAzure temel.</span><span class="sxs-lookup"><span data-stu-id="55713-109">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VHD tooAzure.</span></span> <span data-ttu-id="55713-110">Her adım hello belgenin hello kalan bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](#requirements).</span><span class="sxs-lookup"><span data-stu-id="55713-110">More detailed information and context for each step can be found hello rest of hello document, [starting here](#requirements).</span></span>

<span data-ttu-id="55713-111">Merhaba son olduğundan emin olun [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="55713-111">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="55713-112">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="55713-112">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="55713-113">Örnek parametre adları dahil `myResourceGroup`, `mystorageaccount`, ve `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="55713-113">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="55713-114">İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="55713-114">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="55713-115">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `WestUs` konumu:</span><span class="sxs-lookup"><span data-stu-id="55713-115">hello following example creates a resource group named `myResourceGroup` in hello `WestUs` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="55713-116">Sanal diskler ile depolama hesabı toohold oluşturma [az depolama hesabı oluşturma](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="55713-116">Create a storage account toohold your virtual disks with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="55713-117">Merhaba aşağıdaki örnek adlı bir depolama hesabı oluşturur `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="55713-117">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

<span data-ttu-id="55713-118">Liste hello erişim anahtarları depolama hesabınız için [az depolama hesabı anahtarları listesi](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="55713-118">List hello access keys for your storage account with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="55713-119">Not `key1`:</span><span class="sxs-lookup"><span data-stu-id="55713-119">Make a note of `key1`:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="55713-120">Aldığınız ile Merhaba depolama anahtarı kullanarak depolama hesabınıza içinde bir kapsayıcı oluşturmak [az depolama kapsayıcısı oluşturmak](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="55713-120">Create a container within your storage account using hello storage key you obtained with [az storage container create](/cli/azure/storage/container#create).</span></span> <span data-ttu-id="55713-121">Merhaba aşağıdaki örnek adlı bir kapsayıcı oluşturur `mydisks` hello depolama anahtarı değerini kullanarak `key1`:</span><span class="sxs-lookup"><span data-stu-id="55713-121">hello following example creates a container named `mydisks` using hello storage key value from `key1`:</span></span>

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

<span data-ttu-id="55713-122">Son olarak, oluşturduğunuz, VHD toohello kapsayıcı karşıya [az depolama blob karşıya yükleme](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="55713-122">Finally, upload your VHD toohello container you created with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="55713-123">Merhaba yerel yol tooyour VHD belirtin altında `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="55713-123">Specify hello local path tooyour VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

<span data-ttu-id="55713-124">Merhaba URI tooyour disk belirtin (`--image`) ile [az vm oluşturma](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="55713-124">Specify hello URI tooyour disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="55713-125">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM` daha önce karşıya hello sanal diski kullanarak:</span><span class="sxs-lookup"><span data-stu-id="55713-125">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="55713-126">Merhaba hedef depolama hesabının aynı sanal diskinizin burada karşıya olarak hello toobe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="55713-126">hello destination storage account has toobe hello same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="55713-127">Ayrıca toospecify gerekir veya yanıt ister, tüm hello tarafından gerekli ek parametreler hello **az vm oluşturma** sanal ağ, genel IP adresi, kullanıcı adı ve SSH anahtarları gibi komutu.</span><span class="sxs-lookup"><span data-stu-id="55713-127">You also need toospecify, or answer prompts for, all hello additional parameters required by hello **az vm create** command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="55713-128">Daha fazla bilgiyi hello hakkında [kullanılabilir CLI Resource Manager parametreleri](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="55713-128">You can read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="55713-129">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="55713-129">Requirements</span></span>
<span data-ttu-id="55713-130">toocomplete hello adımları izleyerek gerekir:</span><span class="sxs-lookup"><span data-stu-id="55713-130">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="55713-131">**Bir .vhd dosyası yüklü Linux işletim sistemi** -yüklemek bir [Linux Azure destekli dağıtım](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (veya bkz [desteklenmeyen dağıtımlarla bilgi](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) hello VHD tooa sanal diski biçimi.</span><span class="sxs-lookup"><span data-stu-id="55713-131">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="55713-132">Birden çok araç, bir VM ve VHD toocreate mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="55713-132">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="55713-133">Yükleme ve yapılandırma [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) veya [KVM](http://www.linux-kvm.org/page/RunningKVM), toouse VHD, resim biçimi olarak ayırdığınız dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="55713-133">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="55713-134">Gerekirse, [bir görüntüyü dönüştürme](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) kullanarak `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="55713-134">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="55713-135">Hyper-V de kullanabilirsiniz [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) veya [Windows Server 2012/2012 R2 üzerinde](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="55713-135">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="55713-136">Azure'da Hello yeni VHDX biçimi desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="55713-136">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="55713-137">Bir VM oluşturun, VHD'yi hello biçiminde belirtin.</span><span class="sxs-lookup"><span data-stu-id="55713-137">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="55713-138">Gerekirse, VHDX diskleri tooVHD kullanarak dönüştürebilirsiniz [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) veya hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="55713-138">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="55713-139">Ayrıca, Azure tooconvert gerekir böylece dinamik VHD karşıya böyle diskleri toostatic VHD yüklemeden önce desteklemez.</span><span class="sxs-lookup"><span data-stu-id="55713-139">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="55713-140">Araçları gibi kullanabilir [Git için Azure VHD yardımcı programları](https://github.com/Microsoft/azure-vhd-utils-for-go) hello tooAzure karşıya yükleme işlemi sırasında tooconvert dinamik diskler.</span><span class="sxs-lookup"><span data-stu-id="55713-140">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 

* <span data-ttu-id="55713-141">Özel diskinizden oluşturulan VM'ler hello aynı bulunmalıdır hello disk kendisini depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="55713-141">VMs created from your custom disk must reside in hello same storage account as hello disk itself</span></span>
  * <span data-ttu-id="55713-142">Depolama hesabı ve kapsayıcı toohold özel disk ve oluşturulan sanal makineleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="55713-142">Create a storage account and container toohold both your custom disk and created VMs</span></span>
  * <span data-ttu-id="55713-143">Tüm Vm'lerinizi oluşturduktan sonra disk güvenle silebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="55713-143">After you have created all your VMs, you can safely delete your disk</span></span>

<span data-ttu-id="55713-144">Merhaba son olduğundan emin olun [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="55713-144">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="55713-145">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="55713-145">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="55713-146">Örnek parametre adları dahil `myResourceGroup`, `mystorageaccount`, ve `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="55713-146">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="55713-147"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="55713-147"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-disk-toobe-uploaded"></a><span data-ttu-id="55713-148">Karşıya hello disk toobe hazırlama</span><span class="sxs-lookup"><span data-stu-id="55713-148">Prepare hello disk toobe uploaded</span></span>
<span data-ttu-id="55713-149">Azure çeşitli Linux dağıtımları destekler (bkz [destekli dağıtımlar](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="55713-149">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="55713-150">aşağıdaki makaleleri hello size nasıl tooprepare hello Azure üzerinde desteklenen çeşitli Linux dağıtımları yol:</span><span class="sxs-lookup"><span data-stu-id="55713-150">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="55713-151">**[CentOS tabanlı dağıtımlar](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="55713-151">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="55713-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="55713-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="55713-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="55713-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="55713-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="55713-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="55713-155">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="55713-155">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="55713-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="55713-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="55713-157">**[Diğer - desteklenmeyen dağıtımlarla](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="55713-157">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="55713-158">Ayrıca bkz. hello  **[Linux yükleme notları](create-upload-generic.md#general-linux-installation-notes)**  için Azure Linux görüntüleri hazırlama hakkında daha fazla genel ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="55713-158">Also see hello **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="55713-159">Merhaba [Azure platformu SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) içinde ne zaman hello birini destekli dağıtımlar 'Sürümleri desteklenir' altında belirtildiği gibi hello yapılandırma ayrıntıları ile kullanılan yalnızca Linux çalıştıran tooVMs geçerlidir [Azure destekli Linux'ta Dağıtımları](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="55713-159">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="create-a-resource-group"></a><span data-ttu-id="55713-160">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="55713-160">Create a resource group</span></span>
<span data-ttu-id="55713-161">Kaynak grupları mantıksal olarak tüm hello Azure kaynaklarını toosupport hello sanal ağ ve depolama gibi sanal makinelerinizi birleştirin.</span><span class="sxs-lookup"><span data-stu-id="55713-161">Resource groups logically bring together all hello Azure resources toosupport your virtual machines, such as hello virtual networking and storage.</span></span> <span data-ttu-id="55713-162">Daha fazla bilgi kaynak grupları için bkz: [kaynak gruplarını genel bakış](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="55713-162">For more information resource groups, see [resource groups overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="55713-163">Özel diskinizin karşıya yükleme ve sanal makineleri oluşturma önce ilk toocreate sahip bir kaynak grubu gerek [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="55713-163">Before uploading your custom disk and creating VMs, you first need toocreate a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="55713-164">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `westus` konumu:</span><span class="sxs-lookup"><span data-stu-id="55713-164">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a><span data-ttu-id="55713-165">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="55713-165">Create a storage account</span></span>

<span data-ttu-id="55713-166">Özel disk ve VM'lerin için depolama hesabı oluşturma [az depolama hesabı oluşturma](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="55713-166">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="55713-167">Herhangi bir VM, özel bir disk gereksinimi toobe gelen oluşturduğunuz yönetilmeyen diskleri aynı depolama hesabı bu diski olarak hello.</span><span class="sxs-lookup"><span data-stu-id="55713-167">Any VMs with unmanaged disks that you create from your custom disk need toobe in hello same storage account as that disk.</span></span> 

<span data-ttu-id="55713-168">Merhaba aşağıdaki örnek adlı bir depolama hesabı oluşturur `mystorageaccount` daha önce oluşturduğunuz hello kaynak grubunda:</span><span class="sxs-lookup"><span data-stu-id="55713-168">hello following example creates a storage account named `mystorageaccount` in hello resource group previously created:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="55713-169">Depolama hesabı anahtarlarını Listele</span><span class="sxs-lookup"><span data-stu-id="55713-169">List storage account keys</span></span>
<span data-ttu-id="55713-170">Azure her depolama hesabı için iki 512 bit erişim tuşu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="55713-170">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="55713-171">Bu erişim anahtarlarını toocarry genişletme yazma işlemleri gibi toohello depolama hesabı kimlik doğrulaması yapılırken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="55713-171">These access keys are used when authenticating toohello storage account, such as toocarry out write operations.</span></span> <span data-ttu-id="55713-172">Daha fazla bilgi edinin [yönetme erişimi burada toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="55713-172">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="55713-173">İle Merhaba erişim tuşlarını görüntüleme [az depolama hesabı anahtarları listesi](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="55713-173">You view hello access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="55713-174">Görünüm hello erişim tuşları oluşturduğunuz hello depolama hesabı için:</span><span class="sxs-lookup"><span data-stu-id="55713-174">View hello access keys for hello storage account you created:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="55713-175">Merhaba çıkış benzer:</span><span class="sxs-lookup"><span data-stu-id="55713-175">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="55713-176">Not `key1` hello sonraki adımlarda depolama hesabınıza toointeract kullanacak şekilde.</span><span class="sxs-lookup"><span data-stu-id="55713-176">Make a note of `key1` as you will use it toointeract with your storage account in hello next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="55713-177">Depolama kapsayıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="55713-177">Create a storage container</span></span>
<span data-ttu-id="55713-178">Hello farklı dizinleri toologically oluşturduğunuz aynı şekilde düzenlemek, yerel dosya sistemi, disklerinizi bir depolama hesabı tooorganize kapsayıcılara oluşturun.</span><span class="sxs-lookup"><span data-stu-id="55713-178">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your disks.</span></span> <span data-ttu-id="55713-179">Bir depolama hesabı kapsayıcıların herhangi bir sayı içerebilir.</span><span class="sxs-lookup"><span data-stu-id="55713-179">A storage account can contain any number of containers.</span></span> <span data-ttu-id="55713-180">İle bir kapsayıcı oluşturmak [az depolama kapsayıcısı oluşturmak](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="55713-180">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="55713-181">Merhaba aşağıdaki örnek adlı bir kapsayıcı oluşturur `mydisks`:</span><span class="sxs-lookup"><span data-stu-id="55713-181">hello following example creates a container named `mydisks`:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a><span data-ttu-id="55713-182">VHD karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="55713-182">Upload VHD</span></span>
<span data-ttu-id="55713-183">Şimdi özel diskiniz ile karşıya [az depolama blob karşıya yükleme](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="55713-183">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="55713-184">Karşıya yükleme ve özel diskinizin bir sayfa blob'u olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="55713-184">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="55713-185">Erişim anahtarı, hello önceki adımda oluşturduğunuz hello kapsayıcısı belirtin ve yerel bilgisayarınızdaki yolu toohello özel diske hello:</span><span class="sxs-lookup"><span data-stu-id="55713-185">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-hello-vm"></a><span data-ttu-id="55713-186">Merhaba VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="55713-186">Create hello VM</span></span>
<span data-ttu-id="55713-187">toocreate VM yönetilmeyen disklerle hello URI tooyour disk belirtin (`--image`) ile [az vm oluşturma](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="55713-187">toocreate a VM with unmanaged disks, specify hello URI tooyour disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="55713-188">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM` daha önce karşıya hello sanal diski kullanarak:</span><span class="sxs-lookup"><span data-stu-id="55713-188">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

<span data-ttu-id="55713-189">Merhaba belirttiğiniz `--image` parametresiyle [az vm oluşturma](/cli/azure/vm#create) toopoint tooyour özel disk.</span><span class="sxs-lookup"><span data-stu-id="55713-189">You specify hello `--image` parameter with [az vm create](/cli/azure/vm#create) toopoint tooyour custom disk.</span></span> <span data-ttu-id="55713-190">Emin `--storage-account` eşleşmeleri hello özel diskinizin depolandığı depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="55713-190">Ensure that `--storage-account` matches hello storage account where your custom disk is stored.</span></span> <span data-ttu-id="55713-191">Aynı kapsayıcı Vm'leriniz özel disk toostore hello gibi hello toouse sahip değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="55713-191">You do not have toouse hello same container as hello custom disk toostore your VMs.</span></span> <span data-ttu-id="55713-192">Emin toocreate herhangi bir ek kapsayıcıdaki hello olun özel diskinizin karşıya yüklemeden önce önceki adımlarda şekilde hello aynı.</span><span class="sxs-lookup"><span data-stu-id="55713-192">Make sure toocreate any additional containers in hello same way as hello earlier steps before uploading your custom disk.</span></span>

<span data-ttu-id="55713-193">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM` özel diskinizden:</span><span class="sxs-lookup"><span data-stu-id="55713-193">hello following example creates a VM named `myVM` from your custom disk:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="55713-194">Hala toospecify gerekir veya yanıt ister, tüm hello tarafından gerekli ek parametreler hello **az vm oluşturma** kullanıcı adı ve SSH anahtarları gibi komutu.</span><span class="sxs-lookup"><span data-stu-id="55713-194">You still need toospecify, or answer prompts for, all hello additional parameters required by hello **az vm create** command such as username and SSH keys.</span></span>


## <a name="resource-manager-template"></a><span data-ttu-id="55713-195">Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="55713-195">Resource Manager template</span></span>
<span data-ttu-id="55713-196">Azure Resource Manager şablonları toobuild istediğiniz hello ortamını tanımlayan JavaScript nesne gösterimi (JSON) dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="55713-196">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define hello environment you wish toobuild.</span></span> <span data-ttu-id="55713-197">Merhaba şablonları toodifferent kaynak sağlayıcıları işlem veya ağ gibi ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="55713-197">hello templates are broken down in toodifferent resource providers such as compute or network.</span></span> <span data-ttu-id="55713-198">Var olan şablonları kullanın ya da kendi yazma.</span><span class="sxs-lookup"><span data-stu-id="55713-198">You can use existing templates or write your own.</span></span> <span data-ttu-id="55713-199">Daha fazla bilgi edinin [Resource Manager ve şablonlar kullanarak](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="55713-199">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="55713-200">Merhaba içinde `Microsoft.Compute/virtualMachines` sağlayıcı şablonunuzun elinizde bir `storageProfile` VM için hello yapılandırma ayrıntılarını içeren düğümü.</span><span class="sxs-lookup"><span data-stu-id="55713-200">Within hello `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains hello configuration details for your VM.</span></span> <span data-ttu-id="55713-201">Merhaba iki ana parametreleri tooedit olan hello `image` ve `vhd` tooyour özel disk ve yeni VM sanal disk noktası URI.</span><span class="sxs-lookup"><span data-stu-id="55713-201">hello two main parameters tooedit are hello `image` and `vhd` URIs that point tooyour custom disk and your new VM's virtual disk.</span></span> <span data-ttu-id="55713-202">Merhaba aşağıdaki özel bir disk kullanarak hello JSON örneği gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="55713-202">hello following shows an example of hello JSON for using a custom disk:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="55713-203">Kullanabileceğiniz [bu mevcut şablonu toocreate özel bir görüntü VM'den](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) veya ilgili bilgileri okuyun [kendi Azure Resource Manager şablonları oluşturma](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="55713-203">You can use [this existing template toocreate a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="55713-204">Yapılandırılmış bir şablonu oluşturduktan sonra kullanma [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create) toocreate Vm'leriniz.</span><span class="sxs-lookup"><span data-stu-id="55713-204">Once you have a template configured, use [az group deployment create](/cli/azure/group/deployment#create) toocreate your VMs.</span></span> <span data-ttu-id="55713-205">Merhaba ile Merhaba JSON şablonunuzu URI'sini belirtin `--template-uri` parametre:</span><span class="sxs-lookup"><span data-stu-id="55713-205">Specify hello URI of your JSON template with hello `--template-uri` parameter:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="55713-206">Yerel olarak bilgisayarınızda depolanan bir JSON dosyası varsa, hello kullanabilirsiniz `--template-file` parametresi bunun yerine:</span><span class="sxs-lookup"><span data-stu-id="55713-206">If you have a JSON file stored locally on your computer, you can use hello `--template-file` parameter instead:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="55713-207">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="55713-207">Next steps</span></span>
<span data-ttu-id="55713-208">Hazır ve özel sanal diskinizin karşıya sonra daha fazla bilgi edinebilirsiniz [Resource Manager ve şablonlar kullanarak](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="55713-208">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="55713-209">Ayrıca çok isteyebilir[bir veri diski Ekle](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour yeni VM'ler.</span><span class="sxs-lookup"><span data-stu-id="55713-209">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="55713-210">Tooaccess gerekir, Vm'lerde çalışan uygulamalarınız varsa, mutlaka çok[açık bağlantı noktalarını ve uç noktaları](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="55713-210">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

