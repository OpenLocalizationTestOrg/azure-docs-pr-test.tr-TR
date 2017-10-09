---
title: "Azure CLI 1.0 ile özel bir Linux görüntü aaaUpload | Microsoft Docs"
description: "Oluşturun ve bir sanal sabit disk (VHD) tooAzure hello Resource Manager dağıtım modeli ve hello Azure CLI 1.0 kullanarak özel bir Linux görüntü ile yükleyin."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: iainfou
ms.openlocfilehash: 0bbd232debee1e632233d1c010e388dbc1548bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-hello-azure-cli-10"></a><span data-ttu-id="cbd6b-103">Karşıya yükleme ve hello Azure CLI 1.0 kullanarak özel bir disk görüntüsünü bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="cbd6b-103">Upload and create a Linux VM from custom disk image by using hello Azure CLI 1.0</span></span>
<span data-ttu-id="cbd6b-104">Bu makalede nasıl kullanarak bir sanal sabit disk (VHD) tooAzure tooupload Resource Manager dağıtım modeli hello ve Linux VM'ler bu özel görüntüsünü oluşturma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-104">This article shows you how tooupload a virtual hard disk (VHD) tooAzure using hello Resource Manager deployment model and create Linux VMs from this custom image.</span></span> <span data-ttu-id="cbd6b-105">Bu işlev tooinstall sağlar ve Linux distro tooyour gereksinimlerini yapılandırmak ve ardından bu VHD tooquickly Azure sanal makineleri (VM'ler) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-105">This functionality allows you tooinstall and configure a Linux distro tooyour requirements and then use that VHD tooquickly create Azure virtual machines (VMs).</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="cbd6b-106">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="cbd6b-106">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="cbd6b-107">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="cbd6b-107">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="cbd6b-108">[Azure CLI 1.0](#quick-commands) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="cbd6b-108">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="cbd6b-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="cbd6b-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="cbd6b-110">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="cbd6b-110">Quick commands</span></span>
<span data-ttu-id="cbd6b-111">Tooquickly gerekiyorsa hello görevi, hello bölüm ayrıntıları hello aşağıdaki komutları tooupload VM tooAzure temel.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-111">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VM tooAzure.</span></span> <span data-ttu-id="cbd6b-112">Her adım hello belgenin hello kalan bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](#requirements).</span><span class="sxs-lookup"><span data-stu-id="cbd6b-112">More detailed information and context for each step can be found hello rest of hello document, [starting here](#requirements).</span></span>

<span data-ttu-id="cbd6b-113">Bilgisayarınızda yüklü olduğundan emin olun [Azure CLI 1.0 hello](../../cli-install-nodejs.md) oturum açmış ve Resource Manager modunu kullanma:</span><span class="sxs-lookup"><span data-stu-id="cbd6b-113">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="cbd6b-114">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-114">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="cbd6b-115">Örnek parametre adları dahil `myResourceGroup`, `mystorageaccount`, ve `myimages`.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-115">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="cbd6b-116">İlk olarak, bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-116">First, create a resource group.</span></span> <span data-ttu-id="cbd6b-117">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `WestUs` konumu:</span><span class="sxs-lookup"><span data-stu-id="cbd6b-117">hello following example creates a resource group named `myResourceGroup` in hello `WestUs` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

<span data-ttu-id="cbd6b-118">Bir depolama hesabı toohold sanal diskleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-118">Create a storage account toohold your virtual disks.</span></span> <span data-ttu-id="cbd6b-119">Merhaba aşağıdaki örnek adlı bir depolama hesabı oluşturur `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="cbd6b-119">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

<span data-ttu-id="cbd6b-120">Depolama hesabınız için Hello erişim anahtarlarını listeler.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-120">List hello access keys for your storage account.</span></span> <span data-ttu-id="cbd6b-121">Not `key1`:</span><span class="sxs-lookup"><span data-stu-id="cbd6b-121">Make a note of `key1`:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="cbd6b-122">Depolama hesabınızda aldığınız hello depolama anahtarı kullanarak bir kapsayıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-122">Create a container within your storage account using hello storage key you obtained.</span></span> <span data-ttu-id="cbd6b-123">Merhaba aşağıdaki örnek adlı bir kapsayıcı oluşturur `myimages` hello depolama anahtarı değerini kullanarak `key1`:</span><span class="sxs-lookup"><span data-stu-id="cbd6b-123">hello following example creates a container named `myimages` using hello storage key value from `key1`:</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

<span data-ttu-id="cbd6b-124">Son olarak, oluşturduğunuz, VHD toohello kapsayıcı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-124">Finally, upload your VHD toohello container you created.</span></span> <span data-ttu-id="cbd6b-125">Merhaba yerel yol tooyour VHD belirtin altında `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="cbd6b-125">Specify hello local path tooyour VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

<span data-ttu-id="cbd6b-126">Karşıya yüklenen sanal diskten bir VM artık oluşturabilirsiniz [Resource Manager şablonu kullanarak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="cbd6b-126">You can now create a VM from your uploaded virtual disk [using a Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span></span> <span data-ttu-id="cbd6b-127">Merhaba URI tooyour disk belirterek hello CLI de kullanabilirsiniz (`--image-urn`).</span><span class="sxs-lookup"><span data-stu-id="cbd6b-127">You can also use hello CLI by specifying hello URI tooyour disk (`--image-urn`).</span></span> <span data-ttu-id="cbd6b-128">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM` daha önce karşıya hello sanal diski kullanarak:</span><span class="sxs-lookup"><span data-stu-id="cbd6b-128">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

<span data-ttu-id="cbd6b-129">Merhaba hedef depolama hesabının aynı sanal diskinizin burada karşıya olarak hello toobe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-129">hello destination storage account has toobe hello same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="cbd6b-130">Ayrıca toospecify gerekir veya yanıt ister, tüm hello tarafından gerekli ek parametreler hello `azure vm create` sanal ağ, genel IP adresi, kullanıcı adı ve SSH anahtarları gibi komutu.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-130">You also need toospecify, or answer prompts for, all hello additional parameters required by hello `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="cbd6b-131">Daha fazla bilgiyi hello hakkında [kullanılabilir CLI Resource Manager parametreleri](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="cbd6b-131">You can read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="cbd6b-132">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="cbd6b-132">Requirements</span></span>
<span data-ttu-id="cbd6b-133">toocomplete hello adımları izleyerek gerekir:</span><span class="sxs-lookup"><span data-stu-id="cbd6b-133">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="cbd6b-134">**Bir .vhd dosyası yüklü Linux işletim sistemi** -yüklemek bir [Linux Azure destekli dağıtım](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (veya bkz [desteklenmeyen dağıtımlarla bilgi](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) hello VHD tooa sanal diski biçimi.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-134">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="cbd6b-135">Birden çok araç, bir VM ve VHD toocreate mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="cbd6b-135">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="cbd6b-136">Yükleme ve yapılandırma [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) veya [KVM](http://www.linux-kvm.org/page/RunningKVM), toouse VHD, resim biçimi olarak ayırdığınız dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-136">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="cbd6b-137">Gerekirse, [bir görüntüyü dönüştürme](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) kullanarak `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-137">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="cbd6b-138">Hyper-V de kullanabilirsiniz [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) veya [Windows Server 2012/2012 R2 üzerinde](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbd6b-138">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="cbd6b-139">Azure'da Hello yeni VHDX biçimi desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-139">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="cbd6b-140">Bir VM oluşturun, VHD'yi hello biçiminde belirtin.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-140">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="cbd6b-141">Gerekirse, VHDX diskleri tooVHD kullanarak dönüştürebilirsiniz [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) veya hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-141">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="cbd6b-142">Ayrıca, Azure tooconvert gerekir böylece dinamik VHD karşıya böyle diskleri toostatic VHD yüklemeden önce desteklemez.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-142">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="cbd6b-143">Araçları gibi kullanabilir [Git için Azure VHD yardımcı programları](https://github.com/Microsoft/azure-vhd-utils-for-go) hello tooAzure karşıya yükleme işlemi sırasında tooconvert dinamik diskler.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-143">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 

* <span data-ttu-id="cbd6b-144">Özel görüntüden oluşturulan VM'ler hello aynı bulunmalıdır hello görüntü kendisini olarak depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="cbd6b-144">VMs created from your custom image must reside in hello same storage account as hello image itself</span></span>
  * <span data-ttu-id="cbd6b-145">Özel görüntü ve oluşturulan sanal makineleri bir depolama hesabı ve kapsayıcı toohold oluşturma</span><span class="sxs-lookup"><span data-stu-id="cbd6b-145">Create a storage account and container toohold both your custom image and created VMs</span></span>
  * <span data-ttu-id="cbd6b-146">Tüm Vm'lerinizi oluşturduktan sonra görüntünüzü güvenle silebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="cbd6b-146">After you have created all your VMs, you can safely delete your image</span></span>

<span data-ttu-id="cbd6b-147">Bilgisayarınızda yüklü olduğundan emin olun [Azure CLI 1.0 hello](../../cli-install-nodejs.md) oturum açmış ve Resource Manager modunu kullanma:</span><span class="sxs-lookup"><span data-stu-id="cbd6b-147">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="cbd6b-148">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-148">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="cbd6b-149">Örnek parametre adları dahil `myResourceGroup`, `mystorageaccount`, ve `myimages`.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-149">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="cbd6b-150"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="cbd6b-150"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-image-toobe-uploaded"></a><span data-ttu-id="cbd6b-151">Karşıya hello görüntü toobe hazırlama</span><span class="sxs-lookup"><span data-stu-id="cbd6b-151">Prepare hello image toobe uploaded</span></span>
<span data-ttu-id="cbd6b-152">Azure çeşitli Linux dağıtımları destekler (bkz [destekli dağıtımlar](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="cbd6b-152">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="cbd6b-153">aşağıdaki makaleleri hello size nasıl tooprepare hello Azure üzerinde desteklenen çeşitli Linux dağıtımları yol:</span><span class="sxs-lookup"><span data-stu-id="cbd6b-153">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="cbd6b-154">**[CentOS tabanlı dağıtımlar](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="cbd6b-154">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="cbd6b-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="cbd6b-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="cbd6b-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="cbd6b-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="cbd6b-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="cbd6b-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="cbd6b-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="cbd6b-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="cbd6b-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="cbd6b-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="cbd6b-160">**[Diğer - desteklenmeyen dağıtımlarla](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="cbd6b-160">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="cbd6b-161">Ayrıca bkz. hello  **[Linux yükleme notları](create-upload-generic.md#general-linux-installation-notes)**  için Azure Linux görüntüleri hazırlama hakkında daha fazla genel ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-161">Also see hello **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="cbd6b-162">Merhaba [Azure platformu SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) içinde ne zaman hello birini destekli dağıtımlar 'Sürümleri desteklenir' altında belirtildiği gibi hello yapılandırma ayrıntıları ile kullanılan yalnızca Linux çalıştıran tooVMs geçerlidir [Azure destekli Linux'ta Dağıtımları](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cbd6b-162">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="create-a-resource-group"></a><span data-ttu-id="cbd6b-163">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="cbd6b-163">Create a resource group</span></span>
<span data-ttu-id="cbd6b-164">Kaynak grupları mantıksal olarak tüm hello Azure kaynaklarını toosupport hello sanal ağ ve depolama gibi sanal makinelerinizi birleştirin.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-164">Resource groups logically bring together all hello Azure resources toosupport your virtual machines, such as hello virtual networking and storage.</span></span> <span data-ttu-id="cbd6b-165">Daha fazla bilgi edinin [Azure kaynak gruplarını burada](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cbd6b-165">Read more about [Azure resource groups here](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="cbd6b-166">Özel disk görüntünüzü karşıya yükleme ve sanal makineleri oluşturma önce ilk toocreate bir kaynak grubu gerekir.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-166">Before uploading your custom disk image and creating VMs, you first need toocreate a resource group.</span></span> 

<span data-ttu-id="cbd6b-167">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `WestUS` konumu:</span><span class="sxs-lookup"><span data-stu-id="cbd6b-167">hello following example creates a resource group named `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="cbd6b-168">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cbd6b-168">Create a storage account</span></span>
<span data-ttu-id="cbd6b-169">Sanal makineleri bir depolama hesabındaki sayfa blobları olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-169">VMs are stored as page blobs within a storage account.</span></span> <span data-ttu-id="cbd6b-170">Daha fazla bilgi edinin [Azure blob depolama burada](../../storage/common/storage-introduction.md#blob-storage).</span><span class="sxs-lookup"><span data-stu-id="cbd6b-170">Read more about [Azure blob storage here](../../storage/common/storage-introduction.md#blob-storage).</span></span> <span data-ttu-id="cbd6b-171">Özel disk görüntüsü ve VM'ler için bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-171">You create a storage account for your custom disk image and VMs.</span></span> <span data-ttu-id="cbd6b-172">İçinde özel disk görüntüsü gerek toobe gelen oluşturmak herhangi bir VM, görüntü aynı depolama hesabı hello.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-172">Any VMs that you create from your custom disk image need toobe in hello same storage account as that image.</span></span>

<span data-ttu-id="cbd6b-173">Merhaba aşağıdaki örnek adlı bir depolama hesabı oluşturur `mystorageaccount` daha önce oluşturduğunuz hello kaynak grubunda:</span><span class="sxs-lookup"><span data-stu-id="cbd6b-173">hello following example creates a storage account named `mystorageaccount` in hello resource group previously created:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="cbd6b-174">Depolama hesabı anahtarlarını Listele</span><span class="sxs-lookup"><span data-stu-id="cbd6b-174">List storage account keys</span></span>
<span data-ttu-id="cbd6b-175">Azure her depolama hesabı için iki 512 bit erişim tuşu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-175">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="cbd6b-176">Bu erişim anahtarlarını toocarry genişletme yazma işlemleri gibi toohello depolama hesabı kimlik doğrulaması yapılırken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-176">These access keys are used when authenticating toohello storage account, such as toocarry out write operations.</span></span> <span data-ttu-id="cbd6b-177">Daha fazla bilgi edinin [yönetme erişimi burada toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="cbd6b-177">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="cbd6b-178">Erişim tuşları hello ile görüntüleyebilirsiniz `azure storage account keys list` komutu.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-178">You can view access keys with hello `azure storage account keys list` command.</span></span>

<span data-ttu-id="cbd6b-179">Görünüm hello erişim tuşları oluşturduğunuz hello depolama hesabı için:</span><span class="sxs-lookup"><span data-stu-id="cbd6b-179">View hello access keys for hello storage account you created:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="cbd6b-180">Merhaba çıkış benzer:</span><span class="sxs-lookup"><span data-stu-id="cbd6b-180">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK

```
<span data-ttu-id="cbd6b-181">Not `key1` hello sonraki adımlarda depolama hesabınıza toointeract kullanacak şekilde.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-181">Make a note of `key1` as you will use it toointeract with your storage account in hello next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="cbd6b-182">Depolama kapsayıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cbd6b-182">Create a storage container</span></span>
<span data-ttu-id="cbd6b-183">Hello farklı dizinleri toologically oluşturduğunuz aynı şekilde düzenlemek, yerel dosya sistemi, bir depolama hesabı tooorganize kapsayıcılara sanal diskleri ve görüntüleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-183">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your virtual disks and images.</span></span> <span data-ttu-id="cbd6b-184">Bir depolama hesabı kapsayıcıların herhangi bir sayı içerebilir.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-184">A storage account can contain any number of containers.</span></span> 

<span data-ttu-id="cbd6b-185">Merhaba aşağıdaki örnek adlı bir kapsayıcı oluşturur `myimages`, hello önceki adımda elde hello erişim tuşu belirtme (`key1`):</span><span class="sxs-lookup"><span data-stu-id="cbd6b-185">hello following example creates a container named `myimages`, specifying hello access key obtained in hello previous step (`key1`):</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a><span data-ttu-id="cbd6b-186">VHD karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="cbd6b-186">Upload VHD</span></span>
<span data-ttu-id="cbd6b-187">Şimdi gerçekten özel disk görüntünüzü karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-187">Now you can actually upload your custom disk image.</span></span> <span data-ttu-id="cbd6b-188">Olarak VM'ler tarafından kullanılan tüm sanal diskler ile karşıya yükleme ve özel disk görüntünüzü sayfa blob'u olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-188">As with all virtual disks used by VMs, you upload and store your custom disk image as a page blob.</span></span>

<span data-ttu-id="cbd6b-189">Erişim anahtarı, hello önceki adımda oluşturduğunuz hello kapsayıcısı belirtin ve yol toohello özel disk görüntüsü, yerel bilgisayarınızda hello:</span><span class="sxs-lookup"><span data-stu-id="cbd6b-189">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk image on your local computer:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a><span data-ttu-id="cbd6b-190">Özel görüntüden VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="cbd6b-190">Create VM from custom image</span></span>
<span data-ttu-id="cbd6b-191">VM'ler, özel bir disk görüntüsünü oluşturduğunuzda, hello URI toohello disk görüntüsü belirtin.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-191">When you create VMs from your custom disk image, specify hello URI toohello disk image.</span></span> <span data-ttu-id="cbd6b-192">Bu hello özel disk görüntünüzü depolandığı hedef depolama hesabı eşleşmeleri emin olun.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-192">Ensure that hello destination storage account matches where your custom disk image is stored.</span></span> <span data-ttu-id="cbd6b-193">VM'nizi hello Azure CLI ya da Resource Manager JSON şablonunu kullanarak oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-193">You can create your VM using hello Azure CLI or Resource Manager JSON template.</span></span>

### <a name="create-a-vm-using-hello-azure-cli"></a><span data-ttu-id="cbd6b-194">Hello Azure CLI kullanarak bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="cbd6b-194">Create a VM using hello Azure CLI</span></span>
<span data-ttu-id="cbd6b-195">Merhaba belirttiğiniz `--image-urn` hello parametresiyle `azure vm create` komutu toopoint tooyour özel disk görüntüsü.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-195">You specify hello `--image-urn` parameter with hello `azure vm create` command toopoint tooyour custom disk image.</span></span> <span data-ttu-id="cbd6b-196">Emin `--storage-account-name` eşleşmeleri hello özel disk görüntüsünün depolandığı depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-196">Ensure that `--storage-account-name` matches hello storage account where your custom disk image is stored.</span></span> <span data-ttu-id="cbd6b-197">Aynı kapsayıcı Vm'leriniz özel disk görüntü toostore hello gibi hello toouse sahip değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-197">You do not have toouse hello same container as hello custom disk image toostore your VMs.</span></span> <span data-ttu-id="cbd6b-198">Emin toocreate herhangi bir ek kapsayıcıdaki hello olun aynı şekilde, özel disk görüntülerini karşıya yüklemeden önce önceki adımlarda hello.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-198">Make sure toocreate any additional containers in hello same way as hello earlier steps before uploading your custom disk images.</span></span>

<span data-ttu-id="cbd6b-199">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM` özel disk görüntüsünden:</span><span class="sxs-lookup"><span data-stu-id="cbd6b-199">hello following example creates a VM named `myVM` from your custom disk image:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

<span data-ttu-id="cbd6b-200">Hala toospecify gerekir veya yanıt ister, tüm hello tarafından gerekli ek parametreler hello `azure vm create` sanal ağ, genel IP adresi, kullanıcı adı ve SSH anahtarları gibi komutu.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-200">You still need toospecify, or answer prompts for, all hello additional parameters required by hello `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="cbd6b-201">Merhaba hakkında daha fazla bilgiyi [kullanılabilir CLI Resource Manager parametreleri](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="cbd6b-201">Read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

### <a name="create-a-vm-using-a-json-template"></a><span data-ttu-id="cbd6b-202">Bir JSON şablonu kullanarak bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="cbd6b-202">Create a VM using a JSON template</span></span>
<span data-ttu-id="cbd6b-203">Azure Resource Manager şablonları toobuild istediğiniz hello ortamını tanımlayan JavaScript nesne gösterimi (JSON) dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-203">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define hello environment you wish toobuild.</span></span> <span data-ttu-id="cbd6b-204">Merhaba şablonları toodifferent kaynak sağlayıcıları işlem veya ağ gibi ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-204">hello templates are broken down in toodifferent resource providers such as compute or network.</span></span> <span data-ttu-id="cbd6b-205">Var olan şablonları kullanın ya da kendi yazma.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-205">You can use existing templates or write your own.</span></span> <span data-ttu-id="cbd6b-206">Daha fazla bilgi edinin [Resource Manager ve şablonlar kullanarak](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cbd6b-206">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="cbd6b-207">Merhaba içinde `Microsoft.Compute/virtualMachines` sağlayıcı şablonunuzun elinizde bir `storageProfile` VM için hello yapılandırma ayrıntılarını içeren düğümü.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-207">Within hello `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains hello configuration details for your VM.</span></span> <span data-ttu-id="cbd6b-208">Merhaba iki ana parametreleri tooedit olan hello `image` ve `vhd` tooyour özel disk görüntüsü ve yeni VM sanal disk noktası URI.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-208">hello two main parameters tooedit are hello `image` and `vhd` URIs that point tooyour custom disk image and your new VM's virtual disk.</span></span> <span data-ttu-id="cbd6b-209">Merhaba aşağıdaki özel disk görüntüsü kullanmak için hello JSON örneği gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="cbd6b-209">hello following shows an example of hello JSON for using a custom disk image:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="cbd6b-210">Kullanabileceğiniz [bu mevcut şablonu toocreate özel bir görüntü VM'den](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) veya ilgili bilgileri okuyun [kendi Azure Resource Manager şablonları oluşturma](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="cbd6b-210">You can use [this existing template toocreate a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="cbd6b-211">Yapılandırılmış bir şablonu oluşturduktan sonra hello kullanarak, Vm'lerde oluşturma `azure group deployment create` komutu.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-211">Once you have a template configured, you create your VMs using hello `azure group deployment create` command.</span></span> <span data-ttu-id="cbd6b-212">Merhaba ile Merhaba JSON şablonunuzu URI'sini belirtin `--template-uri` parametre:</span><span class="sxs-lookup"><span data-stu-id="cbd6b-212">Specify hello URI of your JSON template with hello `--template-uri` parameter:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="cbd6b-213">Yerel olarak bilgisayarınızda depolanan bir JSON dosyası varsa, hello kullanabilirsiniz `--template-file` parametresi bunun yerine:</span><span class="sxs-lookup"><span data-stu-id="cbd6b-213">If you have a JSON file stored locally on your computer, you can use hello `--template-file` parameter instead:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="cbd6b-214">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cbd6b-214">Next steps</span></span>
<span data-ttu-id="cbd6b-215">Hazır ve özel sanal diskinizin karşıya sonra daha fazla bilgi edinebilirsiniz [Resource Manager ve şablonlar kullanarak](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cbd6b-215">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="cbd6b-216">Ayrıca çok isteyebilir[bir veri diski Ekle](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour yeni VM'ler.</span><span class="sxs-lookup"><span data-stu-id="cbd6b-216">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="cbd6b-217">Tooaccess gerekir, Vm'lerde çalışan uygulamalarınız varsa, mutlaka çok[açık bağlantı noktalarını ve uç noktaları](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cbd6b-217">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

