---
title: "Linux VHD Azure'dan karşıdan | Microsoft Docs"
description: "Azure CLI ve Azure portalını kullanarak bir Linux VHD indirin."
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
ms.openlocfilehash: 3eb88478b43f8e3a36ae04bf3703f238e8cb1f3e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="download-a-linux-vhd-from-azure"></a><span data-ttu-id="558f5-103">Azure'dan Linux VHD indirin</span><span class="sxs-lookup"><span data-stu-id="558f5-103">Download a Linux VHD from Azure</span></span>

<span data-ttu-id="558f5-104">Bu makalede, nasıl yükleneceği hakkında bilgi edineceksiniz bir [Linux sanal sabit disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Azure CLI ve Azure portalını kullanarak Azure dosyasından.</span><span class="sxs-lookup"><span data-stu-id="558f5-104">In this article, you learn how to download a [Linux virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) file from Azure using the Azure CLI and Azure portal.</span></span> 

<span data-ttu-id="558f5-105">Sanal makineler (VM'ler) Azure kullanımda [diskleri](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) bir işletim sistemini, uygulamaları ve verileri depolamak için bir yer olarak.</span><span class="sxs-lookup"><span data-stu-id="558f5-105">Virtual machines (VMs) in Azure use [disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="558f5-106">Tüm Azure VM'ler en az iki disk – bir Windows işletim sistemi diski ve geçici bir diski var.</span><span class="sxs-lookup"><span data-stu-id="558f5-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="558f5-107">İşletim sistemi diski başlangıçta görüntüden oluşturulur ve hem işletim sistemi diski ve görüntünün VHD'leri bir Azure depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="558f5-107">The operating system disk is initially created from an image, and both the operating system disk and the image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="558f5-108">Sanal makineler ayrıca VHD'ler olarak da depolanan bir veya daha fazla veri diski olabilir.</span><span class="sxs-lookup"><span data-stu-id="558f5-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

<span data-ttu-id="558f5-109">Zaten yapmadıysanız, yükleme [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="558f5-109">If you haven't already done so, install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

## <a name="stop-the-vm"></a><span data-ttu-id="558f5-110">VM’yi durdurma</span><span class="sxs-lookup"><span data-stu-id="558f5-110">Stop the VM</span></span>

<span data-ttu-id="558f5-111">Çalışan bir VM bağlıysa VHD Azure'dan indirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="558f5-111">A VHD can’t be downloaded from Azure if it's attached to a running VM.</span></span> <span data-ttu-id="558f5-112">Bir VHD yüklemek için VM durdurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="558f5-112">You need to stop the VM to download a VHD.</span></span> <span data-ttu-id="558f5-113">Bir VHD'yi kullanılabilir olarak kullanmak istiyorsanız bir [görüntü](tutorial-custom-images.md) diğer VM'ler ile yeni diskler oluşturmak için yetkisini kaldırma ve dosyada bulunan işletim sistemini genelleştirir ve VM'yi durdurun gerekir.</span><span class="sxs-lookup"><span data-stu-id="558f5-113">If you want to use a VHD as an [image](tutorial-custom-images.md) to create other VMs with new disks, you need to deprovision and generalize the operating system contained in the file and stop the VM.</span></span> <span data-ttu-id="558f5-114">VHD'yi yeni bir örneğini bir var olan VM veya veri diski için disk olarak kullanmak için yalnızca durdurun ve VM ayırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="558f5-114">To use the VHD as a disk for a new instance of an existing VM or data disk, you only need to stop and deallocate the VM.</span></span>

<span data-ttu-id="558f5-115">VHD diğer sanal makineleri oluşturmak için bir resim olarak kullanmak için aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="558f5-115">To use the VHD as an image to create other VMs, complete these steps:</span></span>

1. <span data-ttu-id="558f5-116">SSH, hesap adını ve VM genel IP adresi bağlanmak ve bu yetkisini kaldırma için kullanın.</span><span class="sxs-lookup"><span data-stu-id="558f5-116">Use SSH, the account name, and the public IP address of the VM to connect to it and deprovision it.</span></span> <span data-ttu-id="558f5-117">+ Kullanıcı parametresi son sağlanan kullanıcı hesabının da kaldırır.</span><span class="sxs-lookup"><span data-stu-id="558f5-117">The +user parameter also removes the last provisioned user account.</span></span> <span data-ttu-id="558f5-118">Hesap kimlik bilgilerini VM Fırında pişirme bu bırakın + kullanıcı parametresi.</span><span class="sxs-lookup"><span data-stu-id="558f5-118">If you are baking account credentials in to the VM, leave out this +user parameter.</span></span> <span data-ttu-id="558f5-119">Aşağıdaki örnek, son sağlanan kullanıcı hesabını kaldırır:</span><span class="sxs-lookup"><span data-stu-id="558f5-119">The following example removes the last provisioned user account:</span></span>

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. <span data-ttu-id="558f5-120">Azure hesabınızda oturum açın [az oturum açma](https://docs.microsoft.com/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="558f5-120">Sign in to your Azure account with [az login](https://docs.microsoft.com/cli/azure/#login).</span></span>
3. <span data-ttu-id="558f5-121">Durdurun ve VM serbest bırakma.</span><span class="sxs-lookup"><span data-stu-id="558f5-121">Stop and deallocate the VM.</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="558f5-122">VM genelleştirin.</span><span class="sxs-lookup"><span data-stu-id="558f5-122">Generalize the VM.</span></span> 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

<span data-ttu-id="558f5-123">VHD'yi yeni bir örneğini bir var olan VM veya veri diski için disk olarak kullanmak için aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="558f5-123">To use the VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="558f5-124">[Azure Portal](https://portal.azure.com/) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="558f5-124">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="558f5-125">Hub menüsünde, **Virtual Machines**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="558f5-125">On the Hub menu, click **Virtual Machines**.</span></span>
3.  <span data-ttu-id="558f5-126">VM listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="558f5-126">Select the VM from the list.</span></span>
4.  <span data-ttu-id="558f5-127">VM için dikey penceresinde **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="558f5-127">On the blade for the VM, click **Stop**.</span></span>

    ![VM'yi Durdur](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="558f5-129">SAS URL oluştur</span><span class="sxs-lookup"><span data-stu-id="558f5-129">Generate SAS URL</span></span>

<span data-ttu-id="558f5-130">VHD dosyasını indirmek için oluşturmak gereken bir [paylaşılan erişim imzası (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span><span class="sxs-lookup"><span data-stu-id="558f5-130">To download the VHD file, you need to generate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="558f5-131">URL oluşturulduğunda, sona erme süresi URL atanır.</span><span class="sxs-lookup"><span data-stu-id="558f5-131">When the URL is generated, an expiration time is assigned to the URL.</span></span>

1.  <span data-ttu-id="558f5-132">VM için dikey pencerenin menüsünde **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="558f5-132">On the menu of the blade for the VM, click **Disks**.</span></span>
2.  <span data-ttu-id="558f5-133">VM için işletim sistemi diski seçin ve ardından **verme**.</span><span class="sxs-lookup"><span data-stu-id="558f5-133">Select the operating system disk for the VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="558f5-134">Tıklatın **URL'yi oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="558f5-134">Click **Generate URL**.</span></span>

    ![URL'yi oluşturmak](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a><span data-ttu-id="558f5-136">VHD indirin</span><span class="sxs-lookup"><span data-stu-id="558f5-136">Download VHD</span></span>

1.  <span data-ttu-id="558f5-137">Oluşturulan URL altında VHD dosyasını yükle'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="558f5-137">Under the URL that was generated, click Download the VHD file.</span></span>

    ![VHD indirin](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="558f5-139">' İ tıklatmanız gerekir **kaydetmek** karşıdan yüklemeyi başlatmak için tarayıcıda.</span><span class="sxs-lookup"><span data-stu-id="558f5-139">You may need to click **Save** in the browser to start the download.</span></span> <span data-ttu-id="558f5-140">VHD dosyası için varsayılan ad *abcd*.</span><span class="sxs-lookup"><span data-stu-id="558f5-140">The default name for the VHD file is *abcd*.</span></span>

    ![Tarayıcıda Kaydet'e tıklayın.](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="558f5-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="558f5-142">Next steps</span></span>

- <span data-ttu-id="558f5-143">Bilgi edinmek için nasıl [karşıya yükleyin ve Azure CLI 2.0 ile özel diskten bir Linux VM oluşturma](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="558f5-143">Learn how to [upload and create a Linux VM from custom disk with the Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
- <span data-ttu-id="558f5-144">[Azure diskleri Azure CLI yönetmek](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="558f5-144">[Manage Azure disks the Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

