---
title: "Azure CLI 1.0 ile özel bir Linux görüntüyü karşıya yüklemeden | Microsoft Docs"
description: "Oluşturun ve bir sanal sabit disk (VHD) için Azure Resource Manager dağıtım modeli ve Azure CLI 1.0 kullanarak özel bir Linux görüntü ile yükleyin."
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
ms.openlocfilehash: ca4c6cb9296028275b2b032af0c94baabeec1223
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-the-azure-cli-10"></a><span data-ttu-id="016f8-103">Karşıya yükleme ve Azure CLI 1.0 kullanarak özel bir disk görüntüsünü bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="016f8-103">Upload and create a Linux VM from custom disk image by using the Azure CLI 1.0</span></span>
<span data-ttu-id="016f8-104">Bu makalede Resource Manager dağıtım modelini kullanarak Azure'a bir sanal sabit disk (VHD) yükleyin ve Linux VM'ler bu özel görüntüsünü oluşturmak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="016f8-104">This article shows you how to upload a virtual hard disk (VHD) to Azure using the Resource Manager deployment model and create Linux VMs from this custom image.</span></span> <span data-ttu-id="016f8-105">Bu işlevsellik, yükleme ve Linux distro gereksinimlerinize yapılandırmak ve hızlı bir şekilde Azure sanal makineleri (VM'ler) oluşturmak için bu VHD kullanmak olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="016f8-105">This functionality allows you to install and configure a Linux distro to your requirements and then use that VHD to quickly create Azure virtual machines (VMs).</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="016f8-106">Görevi tamamlamak için kullanılacak CLI sürümleri</span><span class="sxs-lookup"><span data-stu-id="016f8-106">CLI versions to complete the task</span></span>
<span data-ttu-id="016f8-107">Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="016f8-107">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="016f8-108">[Azure CLI 1.0](#quick-commands) – bizim CLI Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="016f8-108">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="016f8-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): Kaynak yönetimi dağıtım modeline yönelik yeni nesil CLI'mız</span><span class="sxs-lookup"><span data-stu-id="016f8-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="016f8-110">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="016f8-110">Quick commands</span></span>
<span data-ttu-id="016f8-111">Bir VM için Azure karşıya yüklemek için hızlı bir şekilde, aşağıdaki bölümde ayrıntıları temel görevi gerekiyorsa komutları.</span><span class="sxs-lookup"><span data-stu-id="016f8-111">If you need to quickly accomplish the task, the following section details the base commands to upload a VM to Azure.</span></span> <span data-ttu-id="016f8-112">Her adım, belgenin geri kalanında bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](#requirements).</span><span class="sxs-lookup"><span data-stu-id="016f8-112">More detailed information and context for each step can be found the rest of the document, [starting here](#requirements).</span></span>

<span data-ttu-id="016f8-113">Bilgisayarınızda yüklü olduğundan emin olun [Azure CLI 1.0](../../cli-install-nodejs.md) oturum açmış ve Resource Manager modunu kullanma:</span><span class="sxs-lookup"><span data-stu-id="016f8-113">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="016f8-114">Aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="016f8-114">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="016f8-115">Örnek parametre adları dahil `myResourceGroup`, `mystorageaccount`, ve `myimages`.</span><span class="sxs-lookup"><span data-stu-id="016f8-115">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="016f8-116">İlk olarak, bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="016f8-116">First, create a resource group.</span></span> <span data-ttu-id="016f8-117">Aşağıdaki örnek, bir kaynak grubu oluşturur `myResourceGroup` içinde `WestUs` konumu:</span><span class="sxs-lookup"><span data-stu-id="016f8-117">The following example creates a resource group named `myResourceGroup` in the `WestUs` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

<span data-ttu-id="016f8-118">Sanal diskleri tutmak için bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="016f8-118">Create a storage account to hold your virtual disks.</span></span> <span data-ttu-id="016f8-119">Aşağıdaki örnek adlı bir depolama hesabı oluşturur `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="016f8-119">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

<span data-ttu-id="016f8-120">Depolama hesabınız için erişim anahtarlarını listeler.</span><span class="sxs-lookup"><span data-stu-id="016f8-120">List the access keys for your storage account.</span></span> <span data-ttu-id="016f8-121">Not `key1`:</span><span class="sxs-lookup"><span data-stu-id="016f8-121">Make a note of `key1`:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="016f8-122">Depolama hesabınızda aldığınız depolama anahtarı kullanarak bir kapsayıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="016f8-122">Create a container within your storage account using the storage key you obtained.</span></span> <span data-ttu-id="016f8-123">Aşağıdaki örnek adlı bir kapsayıcı oluşturur `myimages` depolama anahtarı değerini kullanarak `key1`:</span><span class="sxs-lookup"><span data-stu-id="016f8-123">The following example creates a container named `myimages` using the storage key value from `key1`:</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

<span data-ttu-id="016f8-124">Son olarak, VHD'yi oluşturduğunuz kapsayıcıya karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="016f8-124">Finally, upload your VHD to the container you created.</span></span> <span data-ttu-id="016f8-125">VHD altında yerel yolunu belirtin `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="016f8-125">Specify the local path to your VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

<span data-ttu-id="016f8-126">Karşıya yüklenen sanal diskten bir VM artık oluşturabilirsiniz [Resource Manager şablonu kullanarak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="016f8-126">You can now create a VM from your uploaded virtual disk [using a Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span></span> <span data-ttu-id="016f8-127">URI diskinize belirterek CLI de kullanabilirsiniz (`--image-urn`).</span><span class="sxs-lookup"><span data-stu-id="016f8-127">You can also use the CLI by specifying the URI to your disk (`--image-urn`).</span></span> <span data-ttu-id="016f8-128">Aşağıdaki örnek, adlandırılmış bir VM'nin oluşturur `myVM` sanal diski kullanarak daha önce karşıya:</span><span class="sxs-lookup"><span data-stu-id="016f8-128">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

<span data-ttu-id="016f8-129">Hedef depolama hesabının sanal diskinizin karşıya burada ile aynı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="016f8-129">The destination storage account has to be the same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="016f8-130">Belirtmeniz gerekir ya da yanıt ister gerektirdiği tüm ek parametreleri için `azure vm create` sanal ağ, genel IP adresi, kullanıcı adı ve SSH anahtarları gibi komutu.</span><span class="sxs-lookup"><span data-stu-id="016f8-130">You also need to specify, or answer prompts for, all the additional parameters required by the `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="016f8-131">Daha fazla bilgi edinebilirsiniz [kullanılabilir CLI Resource Manager parametreleri](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="016f8-131">You can read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="016f8-132">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="016f8-132">Requirements</span></span>
<span data-ttu-id="016f8-133">Aşağıdaki adımları tamamlamak için gerekir:</span><span class="sxs-lookup"><span data-stu-id="016f8-133">To complete the following steps, you need:</span></span>

* <span data-ttu-id="016f8-134">**Bir .vhd dosyası yüklü Linux işletim sistemi** -yüklemek bir [Linux Azure destekli dağıtım](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (veya bkz [desteklenmeyen dağıtımlarla bilgi](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) VHD biçiminde bir sanal disk için.</span><span class="sxs-lookup"><span data-stu-id="016f8-134">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="016f8-135">Bir VM ve VHD oluşturmak için birden çok araç mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="016f8-135">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="016f8-136">Yükleme ve yapılandırma [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) veya [KVM](http://www.linux-kvm.org/page/RunningKVM), alma, resim biçimi olarak VHD kullanmaya dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="016f8-136">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="016f8-137">Gerekirse, [bir görüntüyü dönüştürme](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) kullanarak `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="016f8-137">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="016f8-138">Hyper-V de kullanabilirsiniz [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) veya [Windows Server 2012/2012 R2 üzerinde](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="016f8-138">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="016f8-139">Azure'da yeni VHDX biçimi desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="016f8-139">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="016f8-140">Bir VM oluşturduğunuzda, VHD biçiminde belirtin.</span><span class="sxs-lookup"><span data-stu-id="016f8-140">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="016f8-141">Gerekirse, VHD kullanarak VHDX diskleri dönüştürebilirsiniz [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) veya [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="016f8-141">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="016f8-142">Ayrıca, Azure karşıya yüklemeden önce statik VHD'ler gibi diskleri dönüştürmeniz gerekir böylece dinamik VHD yüklemeyi desteklemez.</span><span class="sxs-lookup"><span data-stu-id="016f8-142">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="016f8-143">Araçları gibi kullanabilir [Git için Azure VHD yardımcı programları](https://github.com/Microsoft/azure-vhd-utils-for-go) Azure'a karşıya yükleme işlemi sırasında dinamik diskleri dönüştürme.</span><span class="sxs-lookup"><span data-stu-id="016f8-143">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>
> 
> 

* <span data-ttu-id="016f8-144">Özel görüntüden oluşturulan VM'ler görüntü olarak aynı depolama hesabındaki bulunmalıdır</span><span class="sxs-lookup"><span data-stu-id="016f8-144">VMs created from your custom image must reside in the same storage account as the image itself</span></span>
  * <span data-ttu-id="016f8-145">Bir depolama hesabı ve özel görüntü ve oluşturulan VM'ler tutmak için kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="016f8-145">Create a storage account and container to hold both your custom image and created VMs</span></span>
  * <span data-ttu-id="016f8-146">Tüm Vm'lerinizi oluşturduktan sonra görüntünüzü güvenle silebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="016f8-146">After you have created all your VMs, you can safely delete your image</span></span>

<span data-ttu-id="016f8-147">Bilgisayarınızda yüklü olduğundan emin olun [Azure CLI 1.0](../../cli-install-nodejs.md) oturum açmış ve Resource Manager modunu kullanma:</span><span class="sxs-lookup"><span data-stu-id="016f8-147">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="016f8-148">Aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="016f8-148">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="016f8-149">Örnek parametre adları dahil `myResourceGroup`, `mystorageaccount`, ve `myimages`.</span><span class="sxs-lookup"><span data-stu-id="016f8-149">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="016f8-150"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="016f8-150"><a id="prepimage"> </a></span></span>

## <a name="prepare-the-image-to-be-uploaded"></a><span data-ttu-id="016f8-151">Karşıya yüklenecek görüntüsünü hazırlama</span><span class="sxs-lookup"><span data-stu-id="016f8-151">Prepare the image to be uploaded</span></span>
<span data-ttu-id="016f8-152">Azure çeşitli Linux dağıtımları destekler (bkz [destekli dağıtımlar](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="016f8-152">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="016f8-153">Aşağıdaki makaleler Azure üzerinde desteklenen çeşitli Linux dağıtımları hazırlanma konusunda size kılavuzluk eder:</span><span class="sxs-lookup"><span data-stu-id="016f8-153">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="016f8-154">**[CentOS tabanlı dağıtımlar](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="016f8-154">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="016f8-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="016f8-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="016f8-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="016f8-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="016f8-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="016f8-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="016f8-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="016f8-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="016f8-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="016f8-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="016f8-160">**[Diğer - desteklenmeyen dağıtımlarla](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="016f8-160">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="016f8-161">Ayrıca bkz.  **[Linux yükleme notları](create-upload-generic.md#general-linux-installation-notes)**  için Azure Linux görüntüleri hazırlama hakkında daha fazla genel ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="016f8-161">Also see the **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="016f8-162">[Azure platformu SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) içinde yalnızca doğrulanan dağıtımları birini 'Sürümleri desteklenir' altında belirtildiği gibi yapılandırma ayrıntıları ile kullanıldığında, Linux çalıştıran Vm'leri uygulandığı [Azure-Endorsed dağıtımları Linux'ta](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="016f8-162">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="create-a-resource-group"></a><span data-ttu-id="016f8-163">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="016f8-163">Create a resource group</span></span>
<span data-ttu-id="016f8-164">Kaynak grupları, mantıksal olarak birlikte sanal ağ ve depolama gibi sanal makinelerinizi desteklemek için tüm Azure kaynaklarına duruma getirin.</span><span class="sxs-lookup"><span data-stu-id="016f8-164">Resource groups logically bring together all the Azure resources to support your virtual machines, such as the virtual networking and storage.</span></span> <span data-ttu-id="016f8-165">Daha fazla bilgi edinin [Azure kaynak gruplarını burada](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="016f8-165">Read more about [Azure resource groups here](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="016f8-166">Özel disk görüntünüzü karşıya yükleme ve sanal makineleri oluşturma önce ilk olarak bir kaynak grubu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="016f8-166">Before uploading your custom disk image and creating VMs, you first need to create a resource group.</span></span> 

<span data-ttu-id="016f8-167">Aşağıdaki örnek, bir kaynak grubu oluşturur `myResourceGroup` içinde `WestUS` konumu:</span><span class="sxs-lookup"><span data-stu-id="016f8-167">The following example creates a resource group named `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="016f8-168">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="016f8-168">Create a storage account</span></span>
<span data-ttu-id="016f8-169">Sanal makineleri bir depolama hesabındaki sayfa blobları olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="016f8-169">VMs are stored as page blobs within a storage account.</span></span> <span data-ttu-id="016f8-170">Daha fazla bilgi edinin [Azure blob depolama burada](../../storage/common/storage-introduction.md#blob-storage).</span><span class="sxs-lookup"><span data-stu-id="016f8-170">Read more about [Azure blob storage here](../../storage/common/storage-introduction.md#blob-storage).</span></span> <span data-ttu-id="016f8-171">Özel disk görüntüsü ve VM'ler için bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="016f8-171">You create a storage account for your custom disk image and VMs.</span></span> <span data-ttu-id="016f8-172">Özel disk görüntüden oluşturduğunuz herhangi bir VM, görüntü aynı depolama hesabındaki olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="016f8-172">Any VMs that you create from your custom disk image need to be in the same storage account as that image.</span></span>

<span data-ttu-id="016f8-173">Aşağıdaki örnek adlı bir depolama hesabı oluşturur `mystorageaccount` daha önce oluşturduğunuz kaynak grubunda:</span><span class="sxs-lookup"><span data-stu-id="016f8-173">The following example creates a storage account named `mystorageaccount` in the resource group previously created:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="016f8-174">Depolama hesabı anahtarlarını Listele</span><span class="sxs-lookup"><span data-stu-id="016f8-174">List storage account keys</span></span>
<span data-ttu-id="016f8-175">Azure her depolama hesabı için iki 512 bit erişim tuşu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="016f8-175">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="016f8-176">Bu erişim anahtarları, depolama hesabına gibi doğrulanırken, yazma işlemleri gerçekleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="016f8-176">These access keys are used when authenticating to the storage account, such as to carry out write operations.</span></span> <span data-ttu-id="016f8-177">Daha fazla bilgi edinin [depolama burada erişimi yönetme](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="016f8-177">Read more about [managing access to storage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="016f8-178">Erişim tuşları ile görüntüleyebilirsiniz `azure storage account keys list` komutu.</span><span class="sxs-lookup"><span data-stu-id="016f8-178">You can view access keys with the `azure storage account keys list` command.</span></span>

<span data-ttu-id="016f8-179">Oluşturduğunuz depolama hesabının erişim anahtarlarını görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="016f8-179">View the access keys for the storage account you created:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="016f8-180">Çıktı şuna benzer olacaktır:</span><span class="sxs-lookup"><span data-stu-id="016f8-180">The output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK

```
<span data-ttu-id="016f8-181">Not `key1` depolama hesabınız sonraki adımlarda ile etkileşim kurmak için kullanacağınız.</span><span class="sxs-lookup"><span data-stu-id="016f8-181">Make a note of `key1` as you will use it to interact with your storage account in the next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="016f8-182">Depolama kapsayıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="016f8-182">Create a storage container</span></span>
<span data-ttu-id="016f8-183">Yerel dosya sisteminde mantıksal olarak düzenlemek için farklı dizin oluşturmak aynı şekilde, sanal diskleri ve görüntüleri düzenlemek için bir depolama hesabı kapsayıcılara oluşturun.</span><span class="sxs-lookup"><span data-stu-id="016f8-183">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your virtual disks and images.</span></span> <span data-ttu-id="016f8-184">Bir depolama hesabı kapsayıcıların herhangi bir sayı içerebilir.</span><span class="sxs-lookup"><span data-stu-id="016f8-184">A storage account can contain any number of containers.</span></span> 

<span data-ttu-id="016f8-185">Aşağıdaki örnek adlı bir kapsayıcı oluşturur `myimages`, önceki adımda elde erişim tuşu belirtme (`key1`):</span><span class="sxs-lookup"><span data-stu-id="016f8-185">The following example creates a container named `myimages`, specifying the access key obtained in the previous step (`key1`):</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a><span data-ttu-id="016f8-186">VHD karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="016f8-186">Upload VHD</span></span>
<span data-ttu-id="016f8-187">Şimdi gerçekten özel disk görüntünüzü karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="016f8-187">Now you can actually upload your custom disk image.</span></span> <span data-ttu-id="016f8-188">Olarak VM'ler tarafından kullanılan tüm sanal diskler ile karşıya yükleme ve özel disk görüntünüzü sayfa blob'u olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="016f8-188">As with all virtual disks used by VMs, you upload and store your custom disk image as a page blob.</span></span>

<span data-ttu-id="016f8-189">Erişim anahtarınız, yerel bilgisayarınızda önceki adımı ve özel disk görüntüsünün yolunu oluşturulan kapsayıcı belirtin:</span><span class="sxs-lookup"><span data-stu-id="016f8-189">Specify your access key, the container you created in the previous step, and then the path to the custom disk image on your local computer:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a><span data-ttu-id="016f8-190">Özel görüntüden VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="016f8-190">Create VM from custom image</span></span>
<span data-ttu-id="016f8-191">VM'ler, özel bir disk görüntüsünü oluşturduğunuzda, disk görüntü URI'si belirtin.</span><span class="sxs-lookup"><span data-stu-id="016f8-191">When you create VMs from your custom disk image, specify the URI to the disk image.</span></span> <span data-ttu-id="016f8-192">Özel disk görüntünüzü depolandığı hedef depolama hesabı eşleşmeleri emin olun.</span><span class="sxs-lookup"><span data-stu-id="016f8-192">Ensure that the destination storage account matches where your custom disk image is stored.</span></span> <span data-ttu-id="016f8-193">Azure CLI veya Resource Manager JSON şablonunu kullanarak, VM oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="016f8-193">You can create your VM using the Azure CLI or Resource Manager JSON template.</span></span>

### <a name="create-a-vm-using-the-azure-cli"></a><span data-ttu-id="016f8-194">Azure CLI kullanarak bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="016f8-194">Create a VM using the Azure CLI</span></span>
<span data-ttu-id="016f8-195">Belirttiğiniz `--image-urn` parametresiyle `azure vm create` özel disk görüntüsüne işaret edecek şekilde komutu.</span><span class="sxs-lookup"><span data-stu-id="016f8-195">You specify the `--image-urn` parameter with the `azure vm create` command to point to your custom disk image.</span></span> <span data-ttu-id="016f8-196">Emin `--storage-account-name` özel disk görüntüsünün depolandığı depolama hesabını eşleşir.</span><span class="sxs-lookup"><span data-stu-id="016f8-196">Ensure that `--storage-account-name` matches the storage account where your custom disk image is stored.</span></span> <span data-ttu-id="016f8-197">Vm'leriniz depolamak için özel disk görüntüsü olarak aynı kapsayıcı kullanmak zorunda değil.</span><span class="sxs-lookup"><span data-stu-id="016f8-197">You do not have to use the same container as the custom disk image to store your VMs.</span></span> <span data-ttu-id="016f8-198">Özel disk görüntülerinizi karşıya yüklemeden önce önceki adımlarda aynı şekilde herhangi bir ek kapsayıcıdaki oluşturduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="016f8-198">Make sure to create any additional containers in the same way as the earlier steps before uploading your custom disk images.</span></span>

<span data-ttu-id="016f8-199">Aşağıdaki örnek, adlandırılmış bir VM'nin oluşturur `myVM` özel disk görüntüsünden:</span><span class="sxs-lookup"><span data-stu-id="016f8-199">The following example creates a VM named `myVM` from your custom disk image:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

<span data-ttu-id="016f8-200">Yine de belirtmeniz gerekiyorsa veya yanıt ister gerektirdiği tüm ek parametreleri için `azure vm create` sanal ağ, genel IP adresi, kullanıcı adı ve SSH anahtarları gibi komutu.</span><span class="sxs-lookup"><span data-stu-id="016f8-200">You still need to specify, or answer prompts for, all the additional parameters required by the `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="016f8-201">Daha fazla bilgi edinin [kullanılabilir CLI Resource Manager parametreleri](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="016f8-201">Read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

### <a name="create-a-vm-using-a-json-template"></a><span data-ttu-id="016f8-202">Bir JSON şablonu kullanarak bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="016f8-202">Create a VM using a JSON template</span></span>
<span data-ttu-id="016f8-203">Azure Resource Manager şablonları oluşturmak istediğiniz ortamını tanımlayan JavaScript nesne gösterimi (JSON) dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="016f8-203">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define the environment you wish to build.</span></span> <span data-ttu-id="016f8-204">Şablonlar, işlem veya ağ gibi farklı kaynak sağlayıcıları için ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="016f8-204">The templates are broken down in to different resource providers such as compute or network.</span></span> <span data-ttu-id="016f8-205">Var olan şablonları kullanın ya da kendi yazma.</span><span class="sxs-lookup"><span data-stu-id="016f8-205">You can use existing templates or write your own.</span></span> <span data-ttu-id="016f8-206">Daha fazla bilgi edinin [Resource Manager ve şablonlar kullanarak](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="016f8-206">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="016f8-207">İçinde `Microsoft.Compute/virtualMachines` sağlayıcı şablonunuzun elinizde bir `storageProfile` VM için yapılandırma ayrıntılarını içeren düğümü.</span><span class="sxs-lookup"><span data-stu-id="016f8-207">Within the `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains the configuration details for your VM.</span></span> <span data-ttu-id="016f8-208">Düzenlemek için iki ana parametreler `image` ve `vhd` özel disk görüntünüzü ve yeni VM sanal diske işaret URI.</span><span class="sxs-lookup"><span data-stu-id="016f8-208">The two main parameters to edit are the `image` and `vhd` URIs that point to your custom disk image and your new VM's virtual disk.</span></span> <span data-ttu-id="016f8-209">Aşağıdaki özel disk görüntüsü kullanmak için JSON örneği gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="016f8-209">The following shows an example of the JSON for using a custom disk image:</span></span>

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

<span data-ttu-id="016f8-210">Kullanabileceğiniz [özel bir görüntüden bir VM oluşturmak için bu mevcut şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) veya ilgili bilgileri okuyun [kendi Azure Resource Manager şablonları oluşturma](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="016f8-210">You can use [this existing template to create a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="016f8-211">Yapılandırılmış bir şablonu oluşturduktan sonra kullanarak, Vm'lerde oluşturma `azure group deployment create` komutu.</span><span class="sxs-lookup"><span data-stu-id="016f8-211">Once you have a template configured, you create your VMs using the `azure group deployment create` command.</span></span> <span data-ttu-id="016f8-212">JSON şablonunuzla URI'sini belirtin `--template-uri` parametre:</span><span class="sxs-lookup"><span data-stu-id="016f8-212">Specify the URI of your JSON template with the `--template-uri` parameter:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="016f8-213">Yerel olarak bilgisayarınızda depolanan bir JSON dosyası varsa, kullanabileceğiniz `--template-file` parametresi bunun yerine:</span><span class="sxs-lookup"><span data-stu-id="016f8-213">If you have a JSON file stored locally on your computer, you can use the `--template-file` parameter instead:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="016f8-214">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="016f8-214">Next steps</span></span>
<span data-ttu-id="016f8-215">Hazır ve özel sanal diskinizin karşıya sonra daha fazla bilgi edinebilirsiniz [Resource Manager ve şablonlar kullanarak](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="016f8-215">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="016f8-216">Ayrıca isteyebilirsiniz [bir veri diski Ekle](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) yeni Vm'leriniz için.</span><span class="sxs-lookup"><span data-stu-id="016f8-216">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span></span> <span data-ttu-id="016f8-217">Erişmesi gereken Vm'leriniz çalışan uygulamalar varsa, emin olun [açık bağlantı noktalarını ve uç noktaları](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="016f8-217">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

