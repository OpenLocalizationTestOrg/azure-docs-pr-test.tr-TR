---
title: "VHD Windows Azure'dan karşıdan | Microsoft Docs"
description: "Windows Azure portalını kullanarak VHD indirin."
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
ms.openlocfilehash: d8bf89a4b7c2a158302f9ba09a182a3d8d062adc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="download-a-windows-vhd-from-azure"></a><span data-ttu-id="1cfc9-103">VHD Windows Azure'dan indirin</span><span class="sxs-lookup"><span data-stu-id="1cfc9-103">Download a Windows VHD from Azure</span></span>

<span data-ttu-id="1cfc9-104">Bu makalede, nasıl yükleneceği hakkında bilgi edineceksiniz bir [Windows sanal sabit disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Azure portalını kullanarak Azure dosyasından.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-104">In this article, you learn how to download a [Windows virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) file from Azure using the Azure portal.</span></span> 

<span data-ttu-id="1cfc9-105">Sanal makineler (VM'ler) Azure kullanımda [diskleri](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) bir işletim sistemini, uygulamaları ve verileri depolamak için bir yer olarak.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-105">Virtual machines (VMs) in Azure use [disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="1cfc9-106">Tüm Azure VM'ler en az iki disk – bir Windows işletim sistemi diski ve geçici bir diski var.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="1cfc9-107">İşletim sistemi diski başlangıçta görüntüden oluşturulur ve hem işletim sistemi diski ve görüntünün VHD'leri bir Azure depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-107">The operating system disk is initially created from an image, and both the operating system disk and the image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="1cfc9-108">Sanal makineler ayrıca VHD'ler olarak da depolanan bir veya daha fazla veri diski olabilir.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

## <a name="stop-the-vm"></a><span data-ttu-id="1cfc9-109">VM’yi durdurma</span><span class="sxs-lookup"><span data-stu-id="1cfc9-109">Stop the VM</span></span>

<span data-ttu-id="1cfc9-110">Çalışan bir VM bağlıysa VHD Azure'dan indirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-110">A VHD can’t be downloaded from Azure if it's attached to a running VM.</span></span> <span data-ttu-id="1cfc9-111">Bir VHD yüklemek için VM durdurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-111">You need to stop the VM to download a VHD.</span></span> <span data-ttu-id="1cfc9-112">Bir VHD'yi kullanılabilir olarak kullanmak istiyorsanız bir [görüntü](tutorial-custom-images.md) diğer VM'ler ile yeni diskler oluşturmak için kullandığınız [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) dosyada bulunan işletim sistemini genelleştirir ve VM'yi durdurun.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-112">If you want to use a VHD as an [image](tutorial-custom-images.md) to create other VMs with new disks, you use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) to generalize the operating system contained in the file and then stop the VM.</span></span> <span data-ttu-id="1cfc9-113">VHD'yi yeni bir örneğini bir var olan VM veya veri diski için disk olarak kullanmak için yalnızca durdurun ve VM ayırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-113">To use the VHD as a disk for a new instance of an existing VM or data disk, you only need to stop and deallocate the VM.</span></span>

<span data-ttu-id="1cfc9-114">VHD diğer sanal makineleri oluşturmak için bir resim olarak kullanmak için aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="1cfc9-114">To use the VHD as an image to create other VMs, complete these steps:</span></span>

1.  <span data-ttu-id="1cfc9-115">Önceden yapmadıysanız, [Azure portal](https://portal.azure.com/)da oturum açın</span><span class="sxs-lookup"><span data-stu-id="1cfc9-115">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="1cfc9-116">[VM'ye bağlanın](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1cfc9-116">[Connect to the VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
3.  <span data-ttu-id="1cfc9-117">VM, bir yönetici olarak komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-117">On the VM, open the Command Prompt window as an administrator.</span></span>
4.  <span data-ttu-id="1cfc9-118">Dizinine değiştirin *%windir%\system32\sysprep* ve sysprep.exe çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-118">Change the directory to *%windir%\system32\sysprep* and run sysprep.exe.</span></span>
5.  <span data-ttu-id="1cfc9-119">Sistem Hazırlama Aracı iletişim kutusunda seçin **girin sistem Out-of-Box deneyimi (OOBE)**, emin olun **Generalize** seçilir.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-119">In the System Preparation Tool dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that **Generalize** is selected.</span></span>
6.  <span data-ttu-id="1cfc9-120">Kapatma seçenekleri belirleyin **kapatma**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-120">In Shutdown Options, select **Shutdown**, and then click **OK**.</span></span> 

<span data-ttu-id="1cfc9-121">VHD'yi yeni bir örneğini bir var olan VM veya veri diski için disk olarak kullanmak için aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="1cfc9-121">To use the VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="1cfc9-122">Azure portalında Hub menüsünde **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-122">On the Hub menu in the Azure portal, click **Virtual Machines**.</span></span>
2.  <span data-ttu-id="1cfc9-123">VM listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-123">Select the VM from the list.</span></span>
3.  <span data-ttu-id="1cfc9-124">VM için dikey penceresinde **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-124">On the blade for the VM, click **Stop**.</span></span>

    ![VM'yi Durdur](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="1cfc9-126">SAS URL oluştur</span><span class="sxs-lookup"><span data-stu-id="1cfc9-126">Generate SAS URL</span></span>

<span data-ttu-id="1cfc9-127">VHD dosyasını indirmek için oluşturmak gereken bir [paylaşılan erişim imzası (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-127">To download the VHD file, you need to generate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="1cfc9-128">URL oluşturulduğunda, sona erme süresi URL atanır.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-128">When the URL is generated, an expiration time is assigned to the URL.</span></span>

1.  <span data-ttu-id="1cfc9-129">VM için dikey pencerenin menüsünde **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-129">On the menu of the blade for the VM, click **Disks**.</span></span>
2.  <span data-ttu-id="1cfc9-130">VM için işletim sistemi diski seçin ve ardından **verme**.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-130">Select the operating system disk for the VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="1cfc9-131">Sona erme süresini URL'sini ayarlayın *36000*.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-131">Set the expiration time of the URL to *36000*.</span></span>
4.  <span data-ttu-id="1cfc9-132">Tıklatın **URL'yi oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-132">Click **Generate URL**.</span></span>

    ![URL'yi oluşturmak](./media/download-vhd/export-generate.png)

> [!NOTE]
> <span data-ttu-id="1cfc9-134">Bir Windows Server işletim sistemi için büyük VHD dosyasını karşıdan yüklemek için yeterli süre sağlamak için varsayılan süre artar.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-134">The expiration time is increased from the default to provide enough time to download the large VHD file for a Windows Server operating system.</span></span> <span data-ttu-id="1cfc9-135">Bağlantınızı bağlı olarak yüklemek için birkaç saat sürebilir Windows Server işletim sistemini içeren bir VHD dosyasının bekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-135">You can expect a VHD file that contains the Windows Server operating system to take several hours to download depending on your connection.</span></span> <span data-ttu-id="1cfc9-136">Veri diski için bir VHD yüklüyorsanız, varsayılan saat yeterli olur.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-136">If you are downloading a VHD for a data disk, the default time is sufficient.</span></span> 
> 
> 

## <a name="download-vhd"></a><span data-ttu-id="1cfc9-137">VHD indirin</span><span class="sxs-lookup"><span data-stu-id="1cfc9-137">Download VHD</span></span>

1.  <span data-ttu-id="1cfc9-138">Oluşturulan URL altında VHD dosyasını yükle'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-138">Under the URL that was generated, click Download the VHD file.</span></span>

    ![VHD indirin](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="1cfc9-140">' İ tıklatmanız gerekir **kaydetmek** karşıdan yüklemeyi başlatmak için tarayıcıda.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-140">You may need to click **Save** in the browser to start the download.</span></span> <span data-ttu-id="1cfc9-141">VHD dosyası için varsayılan ad *abcd*.</span><span class="sxs-lookup"><span data-stu-id="1cfc9-141">The default name for the VHD file is *abcd*.</span></span>

    ![Tarayıcıda Kaydet'e tıklayın.](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="1cfc9-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1cfc9-143">Next steps</span></span>

- <span data-ttu-id="1cfc9-144">Bilgi edinmek için nasıl [VHD dosyasını Azure'a yüklemeniz](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1cfc9-144">Learn how to [upload a VHD file to Azure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
- <span data-ttu-id="1cfc9-145">[Bir depolama hesabı yönetilmeyen disklerden yönetilen diskleri oluşturma](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1cfc9-145">[Create managed disks from unmanaged disks in a storage account](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
- <span data-ttu-id="1cfc9-146">[PowerShell ile Azure diskleri yönetme](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1cfc9-146">[Manage Azure disks with PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

