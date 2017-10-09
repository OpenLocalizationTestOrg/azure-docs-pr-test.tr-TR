---
title: "aaaCreate ve Linux VHD tooAzure karşıya | Microsoft Docs"
description: "Oluşturma ve bir Azure sanal sabit hello Klasik dağıtım modeli kullanarak hello Linux işletim sistemini içeren disk (VHD) yükleme"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8058ff98-db03-4309-9bf4-69842bd64dd4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: iainfou
ms.openlocfilehash: 77b01316386c4a6eb68c129fa68d42f0a8996edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-hello-linux-operating-system"></a><span data-ttu-id="2aa5e-103">Oluşturma ve bir Sanal Sabit Disk, Linux işletim sistemi içerir hello karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="2aa5e-103">Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="2aa5e-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2aa5e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2aa5e-105">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="2aa5e-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="2aa5e-107">Ayrıca [Azure Kaynak Yöneticisi'ni kullanarak bir özel disk görüntüsü karşıya](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2aa5e-107">You can also [upload a custom disk image using Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="2aa5e-108">Bu makalede nasıl toocreate ve karşıya yükleme bir sanal sabit disk (VHD), kendi olarak kullanabilmek için Azure toocreate sanal makinelerde görüntü gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-108">This article shows you how toocreate and upload a virtual hard disk (VHD) so you can use it as your own image toocreate virtual machines in Azure.</span></span> <span data-ttu-id="2aa5e-109">Nasıl tooprepare hello toocreate kullanabilmesi için birden çok sanal makine üzerinde görüntü tabanlı bir işletim sistemine öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-109">Learn how tooprepare hello operating system so you can use it toocreate multiple virtual machines based on that image.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="2aa5e-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2aa5e-110">Prerequisites</span></span>
<span data-ttu-id="2aa5e-111">Bu makalede aşağıdaki öğelerindeki hello olduğunu varsayar:</span><span class="sxs-lookup"><span data-stu-id="2aa5e-111">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="2aa5e-112">**Bir .vhd dosyası yüklü Linux işletim sistemi** -yüklü olduğu bir [Linux Azure destekli dağıtım](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (veya bkz [desteklenmeyen dağıtımlarla bilgi](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa sanal disk Merhaba VHD biçiminde.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-112">**Linux operating system installed in a .vhd file** - You have installed an [Azure-endorsed Linux distribution](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="2aa5e-113">Birden çok araç, bir VM ve VHD toocreate mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="2aa5e-113">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="2aa5e-114">Yükleme ve yapılandırma [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) veya [KVM](http://www.linux-kvm.org/page/RunningKVM), toouse VHD, resim biçimi olarak ayırdığınız dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-114">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="2aa5e-115">Gerekirse, [bir görüntüyü dönüştürme](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) kullanarak `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-115">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="2aa5e-116">Hyper-V de kullanabilirsiniz [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) veya [Windows Server 2012/2012 R2 üzerinde](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="2aa5e-116">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="2aa5e-117">Azure'da Hello yeni VHDX biçimi desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-117">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="2aa5e-118">Bir VM oluşturun, VHD'yi hello biçiminde belirtin.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-118">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="2aa5e-119">Gerekirse, VHDX diskleri tooVHD kullanarak dönüştürebilirsiniz [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) veya hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-119">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="2aa5e-120">Ayrıca, Azure tooconvert gerekir böylece dinamik VHD karşıya böyle diskleri toostatic VHD yüklemeden önce desteklemez.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-120">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="2aa5e-121">Araçları gibi kullanabilir [Git için Azure VHD yardımcı programları](https://github.com/Microsoft/azure-vhd-utils-for-go) hello tooAzure karşıya yükleme işlemi sırasında tooconvert dinamik diskler.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-121">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>

* <span data-ttu-id="2aa5e-122">**Azure komut satırı arabirimi** -son yükleme hello [Azure komut satırı arabirimi](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooupload hello VHD.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-122">**Azure Command-line Interface** - Install hello latest [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooupload hello VHD.</span></span>

<span data-ttu-id="2aa5e-123"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="2aa5e-123"><a id="prepimage"> </a></span></span>

## <a name="step-1-prepare-hello-image-toobe-uploaded"></a><span data-ttu-id="2aa5e-124">1. adım: karşıya hello görüntü toobe hazırlama</span><span class="sxs-lookup"><span data-stu-id="2aa5e-124">Step 1: Prepare hello image toobe uploaded</span></span>
<span data-ttu-id="2aa5e-125">Azure çeşitli Linux dağıtımları destekler (bkz [destekli dağıtımlar](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="2aa5e-125">Azure supports various Linux distributions (see [Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="2aa5e-126">aşağıdaki makaleleri hello size nasıl tooprepare hello Azure üzerinde desteklenen çeşitli Linux dağıtımları yol.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-126">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure.</span></span> <span data-ttu-id="2aa5e-127">Kılavuzları aşağıdaki hello hello adımları tamamladıktan sonra hazır tooupload tooAzure bir VHD dosya olduktan sonra tekrar buraya gelin:</span><span class="sxs-lookup"><span data-stu-id="2aa5e-127">After you complete hello steps in hello following guides, come back here once you have a VHD file that is ready tooupload tooAzure:</span></span>

* <span data-ttu-id="2aa5e-128">**[CentOS tabanlı dağıtımlar](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="2aa5e-128">**[CentOS-based Distributions](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="2aa5e-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="2aa5e-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="2aa5e-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="2aa5e-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="2aa5e-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="2aa5e-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="2aa5e-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="2aa5e-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="2aa5e-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="2aa5e-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="2aa5e-134">**[Diğer - desteklenmeyen dağıtımlarla](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="2aa5e-134">**[Other - Non-Endorsed Distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

> [!NOTE]
> <span data-ttu-id="2aa5e-135">Hello Azure platformu SLA toovirtual makineleri yalnızca hello birini destekli dağıtımlar Linux OS 'Sürümleri desteklenir' altında belirtildiği gibi hello yapılandırma ayrıntılarını olarak kullanılan hello çalışır durumda geçerlidir [Azure-Endorsed dağıtımları Linux'ta ](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2aa5e-135">hello Azure platform SLA applies toovirtual machines running hello Linux OS only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="2aa5e-136">Tüm Linux dağıtımları hello Azure görüntü Galerisi içinde hello gerekli yapılandırma ile doğrulanan dağıtımları ' dir.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-136">All Linux distributions in hello Azure image gallery are endorsed distributions with hello required configuration.</span></span>
> 
> 

<span data-ttu-id="2aa5e-137">Ayrıca bkz. hello  **[Linux yükleme notları](../create-upload-generic.md#general-linux-installation-notes)**  için Azure Linux görüntüleri hazırlama hakkında daha fazla genel ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-137">Also see hello **[Linux Installation Notes](../create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

<span data-ttu-id="2aa5e-138"><a id="connect"> </a></span><span class="sxs-lookup"><span data-stu-id="2aa5e-138"><a id="connect"> </a></span></span>

## <a name="step-2-prepare-hello-connection-tooazure"></a><span data-ttu-id="2aa5e-139">2. adım: hello bağlantı tooAzure hazırlama</span><span class="sxs-lookup"><span data-stu-id="2aa5e-139">Step 2: Prepare hello connection tooAzure</span></span>
<span data-ttu-id="2aa5e-140">Hello Azure CLI hello Klasik dağıtım modelinde kullandığınızdan emin olun (`azure config mode asm`), tooyour hesabında oturum açın:</span><span class="sxs-lookup"><span data-stu-id="2aa5e-140">Make sure you are using hello Azure CLI in hello classic deployment model (`azure config mode asm`), then log in tooyour account:</span></span>

```azurecli
azure login
```


<span data-ttu-id="2aa5e-141"><a id="upload"> </a></span><span class="sxs-lookup"><span data-stu-id="2aa5e-141"><a id="upload"> </a></span></span>

## <a name="step-3-upload-hello-image-tooazure"></a><span data-ttu-id="2aa5e-142">3. adım: Karşıya yükleme hello görüntü tooAzure</span><span class="sxs-lookup"><span data-stu-id="2aa5e-142">Step 3: Upload hello image tooAzure</span></span>
<span data-ttu-id="2aa5e-143">VHD dosyasına yönelik bir depolama hesabı tooupload gerekir.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-143">You need a storage account tooupload your VHD file to.</span></span> <span data-ttu-id="2aa5e-144">Mevcut bir depolama hesabını ya da seçebilirsiniz veya [yeni bir tane oluşturun](../../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="2aa5e-144">You can either pick an existing storage account or [create a new one](../../../storage/common/storage-create-storage-account.md).</span></span>

<span data-ttu-id="2aa5e-145">Hello Azure CLI tooupload hello görüntü komutu aşağıdaki hello kullanarak kullanın:</span><span class="sxs-lookup"><span data-stu-id="2aa5e-145">Use hello Azure CLI tooupload hello image by using hello following command:</span></span>

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

<span data-ttu-id="2aa5e-146">Merhaba önceki örnekte:</span><span class="sxs-lookup"><span data-stu-id="2aa5e-146">In hello previous example:</span></span>

* <span data-ttu-id="2aa5e-147">**BlobStorageURL** toouse planladığınız hello depolama hesabı hello URL'si</span><span class="sxs-lookup"><span data-stu-id="2aa5e-147">**BlobStorageURL** is hello URL for hello storage account you plan toouse</span></span>
* <span data-ttu-id="2aa5e-148">**YourImagesFolder** hello blob depolama içinde istediğiniz yere toostore görüntülerinizi kapsayıcıdır</span><span class="sxs-lookup"><span data-stu-id="2aa5e-148">**YourImagesFolder** is hello container within blob storage where you want toostore your images</span></span>
* <span data-ttu-id="2aa5e-149">**VHDName** portal tooidentify hello sanal sabit disk görünür hello etiket.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-149">**VHDName** is hello label that appears in portal tooidentify hello virtual hard disk.</span></span>
* <span data-ttu-id="2aa5e-150">**PathToVHDFile** hello tam yol ve makinenizde hello .vhd dosyasının adı.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-150">**PathToVHDFile** is hello full path and name of hello .vhd file on your machine.</span></span>

<span data-ttu-id="2aa5e-151">komutu aşağıdaki hello tam bir örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="2aa5e-151">hello following command shows a complete example:</span></span>

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-hello-image"></a><span data-ttu-id="2aa5e-152">4. adım: hello görüntüsünden bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="2aa5e-152">Step 4: Create a VM from hello image</span></span>
<span data-ttu-id="2aa5e-153">Kullanarak bir VM oluşturun `azure vm create` Merhaba, normal bir VM ile aynı şekilde.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-153">You create a VM using `azure vm create` in hello same way as a regular VM.</span></span> <span data-ttu-id="2aa5e-154">Görüntünüzü hello önceki adımda verdiğiniz hello adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-154">Specify hello name you gave your image in hello previous step.</span></span> <span data-ttu-id="2aa5e-155">Aşağıdaki örneğine hello kullanırız hello **myImage** hello önceki adımda belirtilen görüntü adı:</span><span class="sxs-lookup"><span data-stu-id="2aa5e-155">In hello following example, we use hello **myImage** image name given in hello previous step:</span></span>

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

<span data-ttu-id="2aa5e-156">toocreate kendi sanal makineleri, kendi kullanıcı adı + parola, konum, DNS adı ve görüntü adı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="2aa5e-156">toocreate your own VMs, provide your own username + password, location, DNS name, and image name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2aa5e-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2aa5e-157">Next steps</span></span>
<span data-ttu-id="2aa5e-158">Daha fazla bilgi için bkz: [hello Azure Klasik dağıtım modeli için Azure CLI başvurusu](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="2aa5e-158">For more information, see [Azure CLI reference for hello Azure classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

[Step 1: Prepare hello image toobe uploaded]:#prepimage
[Step 2: Prepare hello connection tooAzure]:#connect
[Step 3: Upload hello image tooAzure]:#upload
