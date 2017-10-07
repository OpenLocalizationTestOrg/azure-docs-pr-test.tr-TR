---
title: aaaDownload Azure Linux VHD'den | Microsoft Docs
description: Hello Azure CLI kullanarak bir Linux VHD indirin ve Azure portal hello.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a><span data-ttu-id="783c7-103">Azure'dan Linux VHD indirin</span><span class="sxs-lookup"><span data-stu-id="783c7-103">Download a Linux VHD from Azure</span></span>

<span data-ttu-id="783c7-104">Bu makalede, bilgi nasıl toodownload bir [Linux sanal sabit disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Azure kullanarak bir dosyadan hello Azure CLI ve Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="783c7-104">In this article, you learn how toodownload a [Linux virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) file from Azure using hello Azure CLI and Azure portal.</span></span> 

<span data-ttu-id="783c7-105">Sanal makineler (VM'ler) Azure kullanımda [diskleri](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) yer toostore bir işletim sistemini, uygulamaları ve verileri olarak.</span><span class="sxs-lookup"><span data-stu-id="783c7-105">Virtual machines (VMs) in Azure use [disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="783c7-106">Tüm Azure VM'ler en az iki disk – bir Windows işletim sistemi diski ve geçici bir diski var.</span><span class="sxs-lookup"><span data-stu-id="783c7-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="783c7-107">Merhaba işletim sistemi diski başlangıçta görüntüden oluşturulur ve hem hello işletim sistemi diski ve hello görüntü VHD'leri bir Azure depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="783c7-107">hello operating system disk is initially created from an image, and both hello operating system disk and hello image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="783c7-108">Sanal makineler ayrıca VHD'ler olarak da depolanan bir veya daha fazla veri diski olabilir.</span><span class="sxs-lookup"><span data-stu-id="783c7-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

<span data-ttu-id="783c7-109">Zaten yapmadıysanız, yükleme [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="783c7-109">If you haven't already done so, install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

## <a name="stop-hello-vm"></a><span data-ttu-id="783c7-110">Merhaba VM Durdur</span><span class="sxs-lookup"><span data-stu-id="783c7-110">Stop hello VM</span></span>

<span data-ttu-id="783c7-111">Azure'dan bir VHD onu bağlıysa indirilemiyor VM çalıştıran tooa.</span><span class="sxs-lookup"><span data-stu-id="783c7-111">A VHD can’t be downloaded from Azure if it's attached tooa running VM.</span></span> <span data-ttu-id="783c7-112">Toostop hello VM toodownload VHD gerekir.</span><span class="sxs-lookup"><span data-stu-id="783c7-112">You need toostop hello VM toodownload a VHD.</span></span> <span data-ttu-id="783c7-113">Bir VHD olarak toouse istiyorsanız bir [görüntü](tutorial-custom-images.md) toocreate diğer sanal makineleri yeni disklerle toodeprovision gerekir ve hello bulunan hello işletim sistemini genelleştirir dosya ve hello VM durdurun.</span><span class="sxs-lookup"><span data-stu-id="783c7-113">If you want toouse a VHD as an [image](tutorial-custom-images.md) toocreate other VMs with new disks, you need toodeprovision and generalize hello operating system contained in hello file and stop hello VM.</span></span> <span data-ttu-id="783c7-114">toouse hello VHD bir var olan VM veya veri diski yeni bir örneği için bir disk olarak yalnızca toostop gerekir ve hello VM serbest bırakma.</span><span class="sxs-lookup"><span data-stu-id="783c7-114">toouse hello VHD as a disk for a new instance of an existing VM or data disk, you only need toostop and deallocate hello VM.</span></span>

<span data-ttu-id="783c7-115">toouse VHD görüntüsü toocreate diğer VM'ler Merhaba, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="783c7-115">toouse hello VHD as an image toocreate other VMs, complete these steps:</span></span>

1. <span data-ttu-id="783c7-116">SSH, hello hesap adı ve hello VM tooconnect tooit hello genel IP adresi kullanın ve onu sağlamayı sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="783c7-116">Use SSH, hello account name, and hello public IP address of hello VM tooconnect tooit and deprovision it.</span></span> <span data-ttu-id="783c7-117">Merhaba + kullanıcı parametresi hello son sağlanan kullanıcı hesabının da kaldırır.</span><span class="sxs-lookup"><span data-stu-id="783c7-117">hello +user parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="783c7-118">Toohello VM hesabı kimlik bilgilerini Fırında pişirme bu bırakın + kullanıcı parametresi.</span><span class="sxs-lookup"><span data-stu-id="783c7-118">If you are baking account credentials in toohello VM, leave out this +user parameter.</span></span> <span data-ttu-id="783c7-119">Merhaba aşağıdaki örnek hello son sağlanan kullanıcı hesabını kaldırır:</span><span class="sxs-lookup"><span data-stu-id="783c7-119">hello following example removes hello last provisioned user account:</span></span>

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. <span data-ttu-id="783c7-120">İçinde tooyour Azure hesabı ile oturum [az oturum açma](https://docs.microsoft.com/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="783c7-120">Sign in tooyour Azure account with [az login](https://docs.microsoft.com/cli/azure/#login).</span></span>
3. <span data-ttu-id="783c7-121">Durdurun ve hello VM serbest bırakma.</span><span class="sxs-lookup"><span data-stu-id="783c7-121">Stop and deallocate hello VM.</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="783c7-122">Merhaba VM genelleştirin.</span><span class="sxs-lookup"><span data-stu-id="783c7-122">Generalize hello VM.</span></span> 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

<span data-ttu-id="783c7-123">toouse hello VHD bir var olan VM veya veri diski, yeni bir örneği için bir disk olarak aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="783c7-123">toouse hello VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="783c7-124">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="783c7-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="783c7-125">Merhaba Hub menüsünde **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="783c7-125">On hello Hub menu, click **Virtual Machines**.</span></span>
3.  <span data-ttu-id="783c7-126">Merhaba VM hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="783c7-126">Select hello VM from hello list.</span></span>
4.  <span data-ttu-id="783c7-127">Merhaba VM için Hello dikey penceresinde **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="783c7-127">On hello blade for hello VM, click **Stop**.</span></span>

    ![VM'yi Durdur](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="783c7-129">SAS URL oluştur</span><span class="sxs-lookup"><span data-stu-id="783c7-129">Generate SAS URL</span></span>

<span data-ttu-id="783c7-130">toodownload hello VHD dosyasına ihtiyacınız toogenerate bir [paylaşılan erişim imzası (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span><span class="sxs-lookup"><span data-stu-id="783c7-130">toodownload hello VHD file, you need toogenerate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="783c7-131">Merhaba URL oluşturulduğunda, sona erme süresi toohello URL atanır.</span><span class="sxs-lookup"><span data-stu-id="783c7-131">When hello URL is generated, an expiration time is assigned toohello URL.</span></span>

1.  <span data-ttu-id="783c7-132">Merhaba VM hello dikey penceresinde Hello menüsünde tıklatın **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="783c7-132">On hello menu of hello blade for hello VM, click **Disks**.</span></span>
2.  <span data-ttu-id="783c7-133">Merhaba hello VM için işletim sistemi diski seçin ve ardından **verme**.</span><span class="sxs-lookup"><span data-stu-id="783c7-133">Select hello operating system disk for hello VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="783c7-134">Tıklatın **URL'yi oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="783c7-134">Click **Generate URL**.</span></span>

    ![URL'yi oluşturmak](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a><span data-ttu-id="783c7-136">VHD indirin</span><span class="sxs-lookup"><span data-stu-id="783c7-136">Download VHD</span></span>

1.  <span data-ttu-id="783c7-137">Oluşturulan hello URL altında indirme hello VHD dosyası'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="783c7-137">Under hello URL that was generated, click Download hello VHD file.</span></span>

    ![VHD indirin](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="783c7-139">Tooclick gerekebilir **kaydetmek** hello tarayıcı toostart hello indirme içinde.</span><span class="sxs-lookup"><span data-stu-id="783c7-139">You may need tooclick **Save** in hello browser toostart hello download.</span></span> <span data-ttu-id="783c7-140">Merhaba varsayılan ad hello VHD dosyası için *abcd*.</span><span class="sxs-lookup"><span data-stu-id="783c7-140">hello default name for hello VHD file is *abcd*.</span></span>

    ![Merhaba tarayıcıda Kaydet'e tıklayın.](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="783c7-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="783c7-142">Next steps</span></span>

- <span data-ttu-id="783c7-143">Nasıl çok öğrenin[karşıya yükleme ve hello Azure CLI 2.0 ile özel diskten bir Linux VM oluşturma](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="783c7-143">Learn how too[upload and create a Linux VM from custom disk with hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
- <span data-ttu-id="783c7-144">[Azure diskleri hello Azure CLI yönetmek](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="783c7-144">[Manage Azure disks hello Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

