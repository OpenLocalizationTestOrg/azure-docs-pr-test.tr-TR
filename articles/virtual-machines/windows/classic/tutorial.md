---
title: aaaCreate VM hello Azure portal ile | Microsoft Docs
description: "Bir Windows sanal makine hello Azure portal oluşturun."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 3848a3d06a7ce377633db78ea385826ed40f94fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-running-windows-in-hello-azure-portal"></a><span data-ttu-id="c9135-103">Windows hello Azure portalı çalıştıran bir sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="c9135-103">Create a virtual machine running Windows in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c9135-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="c9135-104">Azure portal</span></span>](tutorial.md)
> * [<span data-ttu-id="c9135-105">PowerShell: Klasik dağıtım</span><span class="sxs-lookup"><span data-stu-id="c9135-105">PowerShell: Classic deployment</span></span>](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="c9135-106">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c9135-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c9135-107">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="c9135-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="c9135-108">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="c9135-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="c9135-109">Nasıl çok öğrenin[hello Resource Manager dağıtım modelini kullanarak bu adımları uygulamadan](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello kullanarak **Azure portal**.</span><span class="sxs-lookup"><span data-stu-id="c9135-109">Learn how too[perform these steps using hello Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) using hello **Azure portal**.</span></span>

<span data-ttu-id="c9135-110">Bu öğretici şunların nasıl yapıldığını gösterir toocreate Azure Windows hello Azure portalı çalıştıran sanal makine (VM).</span><span class="sxs-lookup"><span data-stu-id="c9135-110">This tutorial shows you how toocreate an Azure virtual machine (VM) running Windows in hello Azure portal.</span></span> <span data-ttu-id="c9135-111">Örnek olarak bir Windows Server görüntüsü kullanacağız, ancak yalnızca bir Merhaba birçok görüntüleri Azure sunar.</span><span class="sxs-lookup"><span data-stu-id="c9135-111">We'll use a Windows Server image as an example, but that's just one of hello many images Azure offers.</span></span> <span data-ttu-id="c9135-112">Görüntü seçenekleriniz aboneliğinize göre değişir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c9135-112">Note that your image choices depend on your subscription.</span></span> <span data-ttu-id="c9135-113">Örneğin, Windows Masaüstü görüntülerini kullanılabilir tooMSDN abone olabilir.</span><span class="sxs-lookup"><span data-stu-id="c9135-113">For example, Windows desktop images may be available tooMSDN subscribers.</span></span>

<span data-ttu-id="c9135-114">Bu bölümde, nasıl gösterilir toouse hello **Pano** Azure portal tooselect hello ve hello sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c9135-114">This section shows you how toouse hello **Dashboard** in hello Azure portal tooselect and then create hello virtual machine.</span></span>

<span data-ttu-id="c9135-115">Kullanarak sanal makineleri oluşturabilirsiniz [kendi görüntüleri](createupload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="c9135-115">You can also create VMs using [your own images](createupload-vhd.md).</span></span> <span data-ttu-id="c9135-116">toolearn bu ve diğer yöntemler hakkında bkz [farklı şekillerde toocreate Windows sanal makine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c9135-116">toolearn about this and other methods, see [Different ways toocreate a Windows virtual machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<!-- 02/27/2017 Video removed as it was based on hello classic portal. -->

## <span data-ttu-id="c9135-117"><a id="createvirtualmachine"></a>Hello sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="c9135-117"><a id="createvirtualmachine"> </a>Create hello virtual machine</span></span>
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a><span data-ttu-id="c9135-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c9135-118">Next steps</span></span>
* <span data-ttu-id="c9135-119">Nasıl çok öğrenin[hello Resource Manager dağıtım modeli kullanarak bir VM oluşturma](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="c9135-119">Learn how too[create a VM using hello Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in hello Azure portal.</span></span>
* <span data-ttu-id="c9135-120">Toohello sanal makinede oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c9135-120">Log on toohello virtual machine.</span></span> <span data-ttu-id="c9135-121">Yönergeler için bkz: [tooa sanal Windows Server çalıştıran makinede oturum](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="c9135-121">For instructions, see [Log on tooa virtual machine running Windows Server](connect-logon.md).</span></span>
* <span data-ttu-id="c9135-122">Bir disk toostore veri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c9135-122">Attach a disk toostore data.</span></span> <span data-ttu-id="c9135-123">Boş diskleri ve verileri içeren diskleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9135-123">You can attach both empty disks and disks that contain data.</span></span> <span data-ttu-id="c9135-124">Merhaba yönergeler için bkz [bir veri diski tooa Windows hello Klasik dağıtım modeliyle oluşturulan sanal makinenin ekleme](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="c9135-124">For instructions, see hello [Attach a data disk tooa Windows virtual machine created with hello classic deployment model](attach-disk.md).</span></span>
