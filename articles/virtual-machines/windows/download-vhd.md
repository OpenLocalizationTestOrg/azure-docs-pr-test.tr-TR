---
title: aaaDownload Azure Windows VHD'den | Microsoft Docs
description: Windows hello Azure portal kullanarak VHD indirin.
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
ms.openlocfilehash: d0ca8842db98f22751f01648c0ba4e5cde090043
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-windows-vhd-from-azure"></a><span data-ttu-id="413c0-103">VHD Windows Azure'dan indirin</span><span class="sxs-lookup"><span data-stu-id="413c0-103">Download a Windows VHD from Azure</span></span>

<span data-ttu-id="413c0-104">Bu makalede, bilgi nasıl toodownload bir [Windows sanal sabit disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Azure kullanarak bir dosyadan hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="413c0-104">In this article, you learn how toodownload a [Windows virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) file from Azure using hello Azure portal.</span></span> 

<span data-ttu-id="413c0-105">Sanal makineler (VM'ler) Azure kullanımda [diskleri](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) yer toostore bir işletim sistemini, uygulamaları ve verileri olarak.</span><span class="sxs-lookup"><span data-stu-id="413c0-105">Virtual machines (VMs) in Azure use [disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="413c0-106">Tüm Azure VM'ler en az iki disk – bir Windows işletim sistemi diski ve geçici bir diski var.</span><span class="sxs-lookup"><span data-stu-id="413c0-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="413c0-107">Merhaba işletim sistemi diski başlangıçta görüntüden oluşturulur ve hem hello işletim sistemi diski ve hello görüntü VHD'leri bir Azure depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="413c0-107">hello operating system disk is initially created from an image, and both hello operating system disk and hello image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="413c0-108">Sanal makineler ayrıca VHD'ler olarak da depolanan bir veya daha fazla veri diski olabilir.</span><span class="sxs-lookup"><span data-stu-id="413c0-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

## <a name="stop-hello-vm"></a><span data-ttu-id="413c0-109">Merhaba VM Durdur</span><span class="sxs-lookup"><span data-stu-id="413c0-109">Stop hello VM</span></span>

<span data-ttu-id="413c0-110">Azure'dan bir VHD onu bağlıysa indirilemiyor VM çalıştıran tooa.</span><span class="sxs-lookup"><span data-stu-id="413c0-110">A VHD can’t be downloaded from Azure if it's attached tooa running VM.</span></span> <span data-ttu-id="413c0-111">Toostop hello VM toodownload VHD gerekir.</span><span class="sxs-lookup"><span data-stu-id="413c0-111">You need toostop hello VM toodownload a VHD.</span></span> <span data-ttu-id="413c0-112">Bir VHD'yi kullanılabilir olarak toouse istiyorsanız bir [görüntü](tutorial-custom-images.md) toocreate kullandığınız diğer sanal makineleri yeni disklerle [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello işletim sistemi hello dosyasında yer alan ve hello VM durdurun.</span><span class="sxs-lookup"><span data-stu-id="413c0-112">If you want toouse a VHD as an [image](tutorial-custom-images.md) toocreate other VMs with new disks, you use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello operating system contained in hello file and then stop hello VM.</span></span> <span data-ttu-id="413c0-113">toouse hello VHD bir var olan VM veya veri diski yeni bir örneği için bir disk olarak yalnızca toostop gerekir ve hello VM serbest bırakma.</span><span class="sxs-lookup"><span data-stu-id="413c0-113">toouse hello VHD as a disk for a new instance of an existing VM or data disk, you only need toostop and deallocate hello VM.</span></span>

<span data-ttu-id="413c0-114">toouse VHD görüntüsü toocreate diğer VM'ler Merhaba, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="413c0-114">toouse hello VHD as an image toocreate other VMs, complete these steps:</span></span>

1.  <span data-ttu-id="413c0-115">Zaten yapmadıysanız, toohello içinde oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="413c0-115">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="413c0-116">[Toohello VM bağlanmak](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="413c0-116">[Connect toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
3.  <span data-ttu-id="413c0-117">Hello VM, bir yönetici olarak hello komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="413c0-117">On hello VM, open hello Command Prompt window as an administrator.</span></span>
4.  <span data-ttu-id="413c0-118">Merhaba dizini çok değiştirmek*%windir%\system32\sysprep* ve sysprep.exe çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="413c0-118">Change hello directory too*%windir%\system32\sysprep* and run sysprep.exe.</span></span>
5.  <span data-ttu-id="413c0-119">Merhaba Sistem Hazırlama Aracı iletişim kutusunda seçin **girin sistem Out-of-Box deneyimi (OOBE)**, emin olun **Generalize** seçilir.</span><span class="sxs-lookup"><span data-stu-id="413c0-119">In hello System Preparation Tool dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that **Generalize** is selected.</span></span>
6.  <span data-ttu-id="413c0-120">Kapatma seçenekleri belirleyin **kapatma**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="413c0-120">In Shutdown Options, select **Shutdown**, and then click **OK**.</span></span> 

<span data-ttu-id="413c0-121">toouse hello VHD bir var olan VM veya veri diski, yeni bir örneği için bir disk olarak aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="413c0-121">toouse hello VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="413c0-122">Merhaba Hub menüsünde hello Azure portal'ın **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="413c0-122">On hello Hub menu in hello Azure portal, click **Virtual Machines**.</span></span>
2.  <span data-ttu-id="413c0-123">Merhaba VM hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="413c0-123">Select hello VM from hello list.</span></span>
3.  <span data-ttu-id="413c0-124">Merhaba VM için Hello dikey penceresinde **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="413c0-124">On hello blade for hello VM, click **Stop**.</span></span>

    ![VM'yi Durdur](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="413c0-126">SAS URL oluştur</span><span class="sxs-lookup"><span data-stu-id="413c0-126">Generate SAS URL</span></span>

<span data-ttu-id="413c0-127">toodownload hello VHD dosyasına ihtiyacınız toogenerate bir [paylaşılan erişim imzası (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span><span class="sxs-lookup"><span data-stu-id="413c0-127">toodownload hello VHD file, you need toogenerate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="413c0-128">Merhaba URL oluşturulduğunda, sona erme süresi toohello URL atanır.</span><span class="sxs-lookup"><span data-stu-id="413c0-128">When hello URL is generated, an expiration time is assigned toohello URL.</span></span>

1.  <span data-ttu-id="413c0-129">Merhaba VM hello dikey penceresinde Hello menüsünde tıklatın **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="413c0-129">On hello menu of hello blade for hello VM, click **Disks**.</span></span>
2.  <span data-ttu-id="413c0-130">Merhaba hello VM için işletim sistemi diski seçin ve ardından **verme**.</span><span class="sxs-lookup"><span data-stu-id="413c0-130">Select hello operating system disk for hello VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="413c0-131">Merhaba sona erme süresini hello URL'nin çok ayarlamak*36000*.</span><span class="sxs-lookup"><span data-stu-id="413c0-131">Set hello expiration time of hello URL too*36000*.</span></span>
4.  <span data-ttu-id="413c0-132">Tıklatın **URL'yi oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="413c0-132">Click **Generate URL**.</span></span>

    ![URL'yi oluşturmak](./media/download-vhd/export-generate.png)

> [!NOTE]
> <span data-ttu-id="413c0-134">Merhaba süre sonu zamanı hello varsayılan tooprovide toodownload hello büyük VHD dosyasını bir Windows Server işletim sistemi için yeterli süre artar.</span><span class="sxs-lookup"><span data-stu-id="413c0-134">hello expiration time is increased from hello default tooprovide enough time toodownload hello large VHD file for a Windows Server operating system.</span></span> <span data-ttu-id="413c0-135">Bağlantınızı bağlı olarak birkaç saat toodownload hello Windows Server işletim sistemi tootake içeren bir VHD dosyası bekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="413c0-135">You can expect a VHD file that contains hello Windows Server operating system tootake several hours toodownload depending on your connection.</span></span> <span data-ttu-id="413c0-136">Veri diski için bir VHD yüklüyorsanız hello varsayılan süre yeterli olur.</span><span class="sxs-lookup"><span data-stu-id="413c0-136">If you are downloading a VHD for a data disk, hello default time is sufficient.</span></span> 
> 
> 

## <a name="download-vhd"></a><span data-ttu-id="413c0-137">VHD indirin</span><span class="sxs-lookup"><span data-stu-id="413c0-137">Download VHD</span></span>

1.  <span data-ttu-id="413c0-138">Oluşturulan hello URL altında indirme hello VHD dosyası'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="413c0-138">Under hello URL that was generated, click Download hello VHD file.</span></span>

    ![VHD indirin](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="413c0-140">Tooclick gerekebilir **kaydetmek** hello tarayıcı toostart hello indirme içinde.</span><span class="sxs-lookup"><span data-stu-id="413c0-140">You may need tooclick **Save** in hello browser toostart hello download.</span></span> <span data-ttu-id="413c0-141">Merhaba varsayılan ad hello VHD dosyası için *abcd*.</span><span class="sxs-lookup"><span data-stu-id="413c0-141">hello default name for hello VHD file is *abcd*.</span></span>

    ![Merhaba tarayıcıda Kaydet'e tıklayın.](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="413c0-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="413c0-143">Next steps</span></span>

- <span data-ttu-id="413c0-144">Nasıl çok öğrenin[bir VHD dosyası tooAzure karşıya](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="413c0-144">Learn how too[upload a VHD file tooAzure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
- <span data-ttu-id="413c0-145">[Bir depolama hesabı yönetilmeyen disklerden yönetilen diskleri oluşturma](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="413c0-145">[Create managed disks from unmanaged disks in a storage account](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
- <span data-ttu-id="413c0-146">[PowerShell ile Azure diskleri yönetme](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="413c0-146">[Manage Azure disks with PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

