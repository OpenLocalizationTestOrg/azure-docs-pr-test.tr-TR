---
title: "Karşıya yükleme veya Azure CLI 2.0 ile özel bir Linux VM Kopyala | Microsoft Docs"
description: "Karşıya yükleme veya Resource Manager dağıtım modeli ve Azure CLI 2.0 kullanarak özelleştirilmiş bir sanal makine kopyalama"
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
ms.openlocfilehash: 7c297725c26ea6c44403a10ecdcc3542f89f10b4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-the-azure-cli-20"></a><span data-ttu-id="58c50-103">Azure CLI 2.0 ile özel diskten bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="58c50-103">Create a Linux VM from custom disk with the Azure CLI 2.0</span></span>

<!-- rename to create-vm-specialized -->

<span data-ttu-id="58c50-104">Bu makalede, özelleştirilmiş sanal sabit disk (VHD) veya kopya yüklemeyi gösteren bir Azure varolan bir VHD'yi ve özel diskten yeni Linux sanal makineleri (VM'ler) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="58c50-104">This article shows you how to upload a customized virtual hard disk (VHD) or copy a an existing VHD in Azure and create new Linux virtual machines (VMs) from the custom disk.</span></span> <span data-ttu-id="58c50-105">Yükleme ve Linux distro gereksinimlerinize yapılandırmak ve hızlı bir şekilde yeni bir Azure sanal makine oluşturmak için bu VHD kullanın.</span><span class="sxs-lookup"><span data-stu-id="58c50-105">You can install and configure a Linux distro to your requirements and then use that VHD to quickly create a new Azure virtual machine.</span></span>

<span data-ttu-id="58c50-106">Özelleştirilmiş diskinizden birden çok VM oluşturmak istiyorsanız, görüntü, VM veya VHD oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="58c50-106">If you want to create multiple VMs from your customized disk, you should create an image from your VM or VHD.</span></span> <span data-ttu-id="58c50-107">Daha fazla bilgi için bkz: [Azure CLI kullanarak bir VM'nin özel bir görüntü oluşturun](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="58c50-107">For more information, see [Create a custom image of an Azure VM using the CLI](tutorial-custom-images.md).</span></span>

<span data-ttu-id="58c50-108">İki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="58c50-108">You have two options:</span></span>
* [<span data-ttu-id="58c50-109">Bir VHD’yi karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="58c50-109">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="58c50-110">Mevcut bir Azure VM'yi kopyalama</span><span class="sxs-lookup"><span data-stu-id="58c50-110">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a><span data-ttu-id="58c50-111">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="58c50-111">Quick commands</span></span>

<span data-ttu-id="58c50-112">Kullanarak yeni bir VM oluştururken [az vm oluşturma](/cli/azure/vm#create) özelleştirilmiş veya özelleştirilmiş bir diskten, **attach** disk (--attach-os-disk) yerine bir özel veya Market görüntüsü belirtme (--görüntü).</span><span class="sxs-lookup"><span data-stu-id="58c50-112">When creating a new VM using [az vm create](/cli/azure/vm#create) from a customized or specialized disk you **attach** the disk (--attach-os-disk) instead of specifying a custom or marketplace image (--image).</span></span> <span data-ttu-id="58c50-113">Aşağıdaki örnek, adlandırılmış bir VM'nin oluşturur *myVM* adlı Yönetilen diski kullanarak *myManagedDisk* özelleştirilmiş VHD'den oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="58c50-113">The following example creates a VM named *myVM* using the managed disk named *myManagedDisk* created from your customized VHD:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a><span data-ttu-id="58c50-114">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="58c50-114">Requirements</span></span>
<span data-ttu-id="58c50-115">Aşağıdaki adımları tamamlamak için gerekir:</span><span class="sxs-lookup"><span data-stu-id="58c50-115">To complete the following steps, you need:</span></span>

* <span data-ttu-id="58c50-116">Azure kullanıma hazır bir Linux sanal makine.</span><span class="sxs-lookup"><span data-stu-id="58c50-116">A Linux virtual machine that has been prepared for use in Azure.</span></span> <span data-ttu-id="58c50-117">[VM hazırlama](#prepare-the-vm) bu makalenin Azure Linux Azure düzgün çalışması VM ve, SSH kullanarak bağlanabilmesi gerekli olan Aracı (waagent) yükleme distro belirli bilgileri bulmak nasıl ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="58c50-117">The [Prepare the VM](#prepare-the-vm) section of this article covers how to find distro specific information on installing the Azure Linux Agent (waagent) which is required for the VM to work properly in Azure and for you to be able to connect to it using SSH.</span></span>
* <span data-ttu-id="58c50-118">Varolan bir VHD dosyasının [Linux Azure destekli dağıtım](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (veya bkz [desteklenmeyen dağıtımlarla bilgi](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) VHD biçiminde bir sanal disk için.</span><span class="sxs-lookup"><span data-stu-id="58c50-118">The VHD file from an existing [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="58c50-119">Bir VM ve VHD oluşturmak için birden çok araç mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="58c50-119">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="58c50-120">Yükleme ve yapılandırma [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) veya [KVM](http://www.linux-kvm.org/page/RunningKVM), alma, resim biçimi olarak VHD kullanmaya dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="58c50-120">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="58c50-121">Gerekirse, [bir görüntüyü dönüştürme](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) kullanarak **qemu img Dönüştür**.</span><span class="sxs-lookup"><span data-stu-id="58c50-121">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using **qemu-img convert**.</span></span>
  * <span data-ttu-id="58c50-122">Hyper-V de kullanabilirsiniz [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) veya [Windows Server 2012/2012 R2 üzerinde](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="58c50-122">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="58c50-123">Azure'da yeni VHDX biçimi desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="58c50-123">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="58c50-124">Bir VM oluşturduğunuzda, VHD biçiminde belirtin.</span><span class="sxs-lookup"><span data-stu-id="58c50-124">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="58c50-125">Gerekirse, VHD kullanarak VHDX diskleri dönüştürebilirsiniz [qemu img Dönüştür](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) veya [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="58c50-125">If needed, you can convert VHDX disks to VHD using [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="58c50-126">Ayrıca, Azure karşıya yüklemeden önce statik VHD'ler gibi diskleri dönüştürmeniz gerekir böylece dinamik VHD yüklemeyi desteklemez.</span><span class="sxs-lookup"><span data-stu-id="58c50-126">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="58c50-127">Araçları gibi kullanabilir [Git için Azure VHD yardımcı programları](https://github.com/Microsoft/azure-vhd-utils-for-go) Azure'a karşıya yükleme işlemi sırasında dinamik diskleri dönüştürme.</span><span class="sxs-lookup"><span data-stu-id="58c50-127">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>
> 
> 


* <span data-ttu-id="58c50-128">En son sahip olduğunuzdan emin olun [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve bir Azure hesabı kullanarak oturum açmış [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="58c50-128">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="58c50-129">Aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="58c50-129">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="58c50-130">Örnek parametre adları dahil *myResourceGroup*, *mystorageaccount*, ve *mydisks*.</span><span class="sxs-lookup"><span data-stu-id="58c50-130">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *mydisks*.</span></span>

<span data-ttu-id="58c50-131"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="58c50-131"><a id="prepimage"> </a></span></span>

## <a name="prepare-the-vm"></a><span data-ttu-id="58c50-132">VM’yi hazırlama</span><span class="sxs-lookup"><span data-stu-id="58c50-132">Prepare the VM</span></span>

<span data-ttu-id="58c50-133">Azure çeşitli Linux dağıtımları destekler (bkz [destekli dağıtımlar](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="58c50-133">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="58c50-134">Aşağıdaki makaleler Azure üzerinde desteklenen çeşitli Linux dağıtımları hazırlanma konusunda size kılavuzluk eder:</span><span class="sxs-lookup"><span data-stu-id="58c50-134">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span></span>

* [<span data-ttu-id="58c50-135">CentOS tabanlı dağıtımlar</span><span class="sxs-lookup"><span data-stu-id="58c50-135">CentOS-based Distributions</span></span>](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="58c50-136">Debian Linux</span><span class="sxs-lookup"><span data-stu-id="58c50-136">Debian Linux</span></span>](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="58c50-137">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="58c50-137">Oracle Linux</span></span>](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="58c50-138">Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="58c50-138">Red Hat Enterprise Linux</span></span>](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="58c50-139">SLES & openSUSE</span><span class="sxs-lookup"><span data-stu-id="58c50-139">SLES & openSUSE</span></span>](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="58c50-140">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="58c50-140">Ubuntu</span></span>](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="58c50-141">Diğer - desteklenmeyen dağıtımlarla</span><span class="sxs-lookup"><span data-stu-id="58c50-141">Other - Non-Endorsed Distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="58c50-142">Ayrıca bkz. [Linux yükleme notları](create-upload-generic.md#general-linux-installation-notes) için Azure Linux görüntüleri hazırlama hakkında daha fazla genel ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="58c50-142">Also see the [Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="58c50-143">[Azure platformu SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) içinde yalnızca doğrulanan dağıtımları birini 'Sürümleri desteklenir' altında belirtildiği gibi yapılandırma ayrıntıları ile kullanıldığında, Linux çalıştıran Vm'leri uygulandığı [Azure-Endorsed dağıtımları Linux'ta](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58c50-143">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="option-1-upload-a-vhd"></a><span data-ttu-id="58c50-144">Seçenek 1: bir VHD yüklemek</span><span class="sxs-lookup"><span data-stu-id="58c50-144">Option 1: Upload a VHD</span></span>

<span data-ttu-id="58c50-145">Yerel makinede çalışıyor olması veya başka bir buluttan dışarı özelleştirilmiş bir VHD'yi yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58c50-145">You can upload a customized VHD that you have running on a local machine or that you exported from another cloud.</span></span> <span data-ttu-id="58c50-146">Yeni bir Azure VM oluşturmak üzere VHD'yi kullanmak için bir depolama hesabına VHD'nin yüklenmesi ve yönetilen bir disk VHD'den oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="58c50-146">To use the VHD to create a new Azure VM, you need to upload the VHD to a storage account and create a managed disk from the VHD.</span></span> 

### <a name="create-a-resource-group"></a><span data-ttu-id="58c50-147">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="58c50-147">Create a resource group</span></span>

<span data-ttu-id="58c50-148">Özel diskinizin karşıya yükleme ve sanal makineleri oluşturma önce ilk sahip bir kaynak grubu oluşturmak ihtiyacınız [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="58c50-148">Before uploading your custom disk and creating VMs, you first need to create a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="58c50-149">Aşağıdaki örnek, bir kaynak grubu oluşturur *myResourceGroup* içinde *eastus* konumu: [Azure yönetilen diskleri genel bakış](../windows/managed-disks-overview.md)</span><span class="sxs-lookup"><span data-stu-id="58c50-149">The following example creates a resource group named *myResourceGroup* in the *eastus* location: [Azure Managed Disks overview](../windows/managed-disks-overview.md)</span></span>
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a><span data-ttu-id="58c50-150">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="58c50-150">Create a storage account</span></span>

<span data-ttu-id="58c50-151">Özel disk ve VM'lerin için depolama hesabı oluşturma [az depolama hesabı oluşturma](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="58c50-151">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> 

<span data-ttu-id="58c50-152">Aşağıdaki örnek adlı bir depolama hesabı oluşturur *mystorageaccount* daha önce oluşturduğunuz kaynak grubunda:</span><span class="sxs-lookup"><span data-stu-id="58c50-152">The following example creates a storage account named *mystorageaccount* in the resource group previously created:</span></span>

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a><span data-ttu-id="58c50-153">Depolama hesabı anahtarlarını Listele</span><span class="sxs-lookup"><span data-stu-id="58c50-153">List storage account keys</span></span>
<span data-ttu-id="58c50-154">Azure her depolama hesabı için iki 512 bit erişim tuşu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="58c50-154">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="58c50-155">Bu erişim anahtarlarını yazma işlemleri gerçekleştirme gibi depolama hesabı, kimlik doğrulaması yapılırken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="58c50-155">These access keys are used when authenticating to the storage account, like carrying out write operations.</span></span> <span data-ttu-id="58c50-156">Daha fazla bilgi edinin [depolama burada erişimi yönetme](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="58c50-156">Read more about [managing access to storage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="58c50-157">İle erişim tuşları görüntüleme [az depolama hesabı anahtarları listesi](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="58c50-157">You view the access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="58c50-158">Oluşturduğunuz depolama hesabının erişim anahtarlarını görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="58c50-158">View the access keys for the storage account you created:</span></span>

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

<span data-ttu-id="58c50-159">Çıktı şuna benzer olacaktır:</span><span class="sxs-lookup"><span data-stu-id="58c50-159">The output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="58c50-160">Not **key1** depolama hesabınız sonraki adımlarda ile etkileşim kurmak için kullanacağınız.</span><span class="sxs-lookup"><span data-stu-id="58c50-160">Make a note of **key1** as you will use it to interact with your storage account in the next steps.</span></span>

### <a name="create-a-storage-container"></a><span data-ttu-id="58c50-161">Depolama kapsayıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="58c50-161">Create a storage container</span></span>
<span data-ttu-id="58c50-162">Yerel dosya sisteminde mantıksal olarak düzenlemek için farklı dizin oluşturmak aynı şekilde, disklerinizi düzenlemek için bir depolama hesabı kapsayıcılara oluşturun.</span><span class="sxs-lookup"><span data-stu-id="58c50-162">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your disks.</span></span> <span data-ttu-id="58c50-163">Bir depolama hesabı kapsayıcıların herhangi bir sayı içerebilir.</span><span class="sxs-lookup"><span data-stu-id="58c50-163">A storage account can contain any number of containers.</span></span> <span data-ttu-id="58c50-164">İle bir kapsayıcı oluşturmak [az depolama kapsayıcısı oluşturmak](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="58c50-164">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="58c50-165">Aşağıdaki örnek adlı bir kapsayıcı oluşturur *mydisks*:</span><span class="sxs-lookup"><span data-stu-id="58c50-165">The following example creates a container named *mydisks*:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-the-vhd"></a><span data-ttu-id="58c50-166">VHD'nin yüklenmesi</span><span class="sxs-lookup"><span data-stu-id="58c50-166">Upload the VHD</span></span>
<span data-ttu-id="58c50-167">Şimdi özel diskiniz ile karşıya [az depolama blob karşıya yükleme](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="58c50-167">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="58c50-168">Karşıya yükleme ve özel diskinizin bir sayfa blob'u olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="58c50-168">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="58c50-169">Erişim anahtarınız, yerel bilgisayarınızda önceki adımı ve özel disk yolu oluşturulan kapsayıcı belirtin:</span><span class="sxs-lookup"><span data-stu-id="58c50-169">Specify your access key, the container you created in the previous step, and then the path to the custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
<span data-ttu-id="58c50-170">VHD karşıya biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="58c50-170">Uploading the VHD may take a while.</span></span>

### <a name="create-a-managed-disk"></a><span data-ttu-id="58c50-171">Yönetilen bir disk oluşturma</span><span class="sxs-lookup"><span data-stu-id="58c50-171">Create a managed disk</span></span>


<span data-ttu-id="58c50-172">Bir yönetilen VHD kullanımından disketi [az disketi](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="58c50-172">Create a managed disk from the VHD using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="58c50-173">Aşağıdaki örnek, adında yönetilen bir disk oluşturur *myManagedDisk* adlı depolama hesabı ve kapsayıcı için karşıya VHD'den:</span><span class="sxs-lookup"><span data-stu-id="58c50-173">The following example creates a managed disk named *myManagedDisk* from the VHD you uploaded to your named storage account and container:</span></span>

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a><span data-ttu-id="58c50-174">Seçenek 2: mevcut bir VM'yi kopyalama</span><span class="sxs-lookup"><span data-stu-id="58c50-174">Option 2: Copy an existing VM</span></span>

<span data-ttu-id="58c50-175">Ayrıca Azure'da özelleştirilmiş VM oluşturun ve ardından işletim sistemi diski kopyalayın ve başka bir kopya oluşturmak için yeni bir VM'e ekleyin.</span><span class="sxs-lookup"><span data-stu-id="58c50-175">You can also create the customized VM in Azure and then copy the OS disk and attach it to a new VM to create another copy.</span></span> <span data-ttu-id="58c50-176">Bu test etmek için uygundur, ancak mevcut bir Azure VM'i model olarak birden çok yeni VM'ler için kullanmak istiyorsanız, gerçekten oluşturmalısınız bir **görüntü** yerine.</span><span class="sxs-lookup"><span data-stu-id="58c50-176">This is fine for testing, but if you want to use an existing Azure VM as the model for multiple new VMs, you really should create an **image** instead.</span></span> <span data-ttu-id="58c50-177">Var olan bir Azure sanal makineden bir görüntü oluşturma hakkında daha fazla bilgi için bkz: [Azure CLI kullanarak bir VM'nin özel bir görüntü oluşturun](tutorial-custom-images.md)</span><span class="sxs-lookup"><span data-stu-id="58c50-177">For more information about creating an image from an existing Azure VM, see [Create a custom image of an Azure VM using the CLI](tutorial-custom-images.md)</span></span>

### <a name="create-a-snapshot"></a><span data-ttu-id="58c50-178">Bir anlık görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="58c50-178">Create a snapshot</span></span>

<span data-ttu-id="58c50-179">Bu örnek, adlandırılmış bir VM'nin bir anlık görüntü oluşturur *myVM* kaynak grubunda *myResourceGroup* ve adında bir anlık görüntü oluşturur *osDiskSnapshot*.</span><span class="sxs-lookup"><span data-stu-id="58c50-179">This example creates a snapshot of a VM named *myVM* in resource group *myResourceGroup* and creates a snapshot named *osDiskSnapshot*.</span></span>

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-the-managed-disk"></a><span data-ttu-id="58c50-180">Yönetilen disketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="58c50-180">Create the managed disk</span></span>

<span data-ttu-id="58c50-181">Yeni bir yönetilen disk anlık görüntüden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="58c50-181">Create a new managed disk from the snapshot.</span></span>

<span data-ttu-id="58c50-182">Anlık görüntü Kimliğini alın.</span><span class="sxs-lookup"><span data-stu-id="58c50-182">Get the ID of the snapshot.</span></span> <span data-ttu-id="58c50-183">Bu örnekte, anlık görüntü adlı *osDiskSnapshot* ve olarak *myResourceGroup* kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="58c50-183">In this example, the snapshot is named *osDiskSnapshot* and it is in the *myResourceGroup* resource group.</span></span>

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

<span data-ttu-id="58c50-184">Yönetilen diski oluşturun.</span><span class="sxs-lookup"><span data-stu-id="58c50-184">Create the managed disk.</span></span> <span data-ttu-id="58c50-185">Bu örnekte, adında yönetilen bir disk oluşturacağız *myManagedDisk* bizim anlık görüntüden 128 GB boyutunda standart depolama olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="58c50-185">In this example, we will create a managed disk named *myManagedDisk* from our snapshot, that is 128GB in size in standard storage.</span></span>

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-the-vm"></a><span data-ttu-id="58c50-186">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="58c50-186">Create the VM</span></span>

<span data-ttu-id="58c50-187">Şimdi, VM oluşturma [az vm oluşturma](/cli/azure/vm#create) ve ekleme (--attach-os-disk) işletim sistemi diski olarak yönetilen disk.</span><span class="sxs-lookup"><span data-stu-id="58c50-187">Now, create your VM with [az vm create](/cli/azure/vm#create) and attach (--attach-os-disk) the managed disk as the OS disk.</span></span> <span data-ttu-id="58c50-188">Aşağıdaki örnek, adlandırılmış bir VM'nin oluşturur *myNewVM* karşıya yüklenen VHD'den oluşturulan yönetilen diski kullanarak:</span><span class="sxs-lookup"><span data-stu-id="58c50-188">The following example creates a VM named *myNewVM* using the managed disk created from your uploaded VHD:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

<span data-ttu-id="58c50-189">Kaynak VM kimlik bilgilerini kullanarak VM içine SSH için görüyor olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="58c50-189">You should be able to SSH into the VM using the credentials from the source VM.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="58c50-190">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="58c50-190">Next steps</span></span>
<span data-ttu-id="58c50-191">Hazır ve özel sanal diskinizin karşıya sonra daha fazla bilgi edinebilirsiniz [Resource Manager ve şablonlar kullanarak](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="58c50-191">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="58c50-192">Ayrıca isteyebilirsiniz [bir veri diski Ekle](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) yeni Vm'leriniz için.</span><span class="sxs-lookup"><span data-stu-id="58c50-192">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span></span> <span data-ttu-id="58c50-193">Erişmesi gereken Vm'leriniz çalışan uygulamalar varsa, emin olun [açık bağlantı noktalarını ve uç noktaları](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58c50-193">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

