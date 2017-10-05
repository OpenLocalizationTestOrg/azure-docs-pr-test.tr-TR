---
title: "Bir sanal makineden Azure DevTest Labs özel görüntü oluşturma | Microsoft Docs"
description: "Azure DevTest Labs Azure portalını kullanarak sağlanan bir VM'den içinde özel bir görüntü oluşturmayı öğrenin"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 9d2dcf7164985508d691e8a0c123efaf3b8aa19a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="431c9-103">Bir sanal makineden özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="431c9-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="431c9-104">Adım adım yönergeler</span><span class="sxs-lookup"><span data-stu-id="431c9-104">Step-by-step instructions</span></span>

<span data-ttu-id="431c9-105">Sağlanan bir sanal makineden özel bir görüntü oluşturun ve daha sonra aynı VM'ler oluşturmak için özel görüntü kullanın.</span><span class="sxs-lookup"><span data-stu-id="431c9-105">You can create a custom image from a provisioned VM, and afterwards use that custom image to create identical VMs.</span></span> <span data-ttu-id="431c9-106">Aşağıdaki adımlar, bir VM'den özel bir görüntü oluşturmak nasıl çalışılacağını:</span><span class="sxs-lookup"><span data-stu-id="431c9-106">The following steps illustrate how to create a custom image from a VM:</span></span>

1. <span data-ttu-id="431c9-107">[Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="431c9-107">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="431c9-108">**More services**’i (Daha fazla hizmet’i) seçip ardından listeden **DevTest Labs**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="431c9-108">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="431c9-109">İstenen Laboratuvar labs listesinden seçin.</span><span class="sxs-lookup"><span data-stu-id="431c9-109">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="431c9-110">Laboratuvar 's dikey penceresinde, seçin **My sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="431c9-110">On the lab's blade, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="431c9-111">Üzerinde **My sanal makineleri** dikey penceresinde istediğiniz özel görüntü oluşturmak VM seçin.</span><span class="sxs-lookup"><span data-stu-id="431c9-111">On the **My virtual machines** blade, select the VM from which you want to create the custom image.</span></span>

1. <span data-ttu-id="431c9-112">VM'ın dikey penceresinde, seçin **oluşturma özel görüntü (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="431c9-112">On the VM's blade, select **Create custom image (VHD)**.</span></span>

    ![Özel görüntü menü öğesi oluşturma](./media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="431c9-114">Üzerinde **oluşturma görüntü** dikey penceresinde, bir ad ve özel görüntünüzü açıklamasını girin.</span><span class="sxs-lookup"><span data-stu-id="431c9-114">On the **Create image** blade, enter a name and description for your custom image.</span></span> <span data-ttu-id="431c9-115">Bir VM oluşturduğunuzda, bu bilgileri tabanları listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="431c9-115">This information is displayed in the list of bases when you create a VM.</span></span>

    ![Özel görüntü dikey penceresi oluşturma](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="431c9-117">Sysprep VM üzerinde çalışan olup olmadığını seçin.</span><span class="sxs-lookup"><span data-stu-id="431c9-117">Select whether sysprep was run on the VM.</span></span> <span data-ttu-id="431c9-118">Sysprep VM çalıştırılmadı, sysprep bu özel görüntüsünü bir VM oluşturulduğunda çalıştırmak isteyip istemediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="431c9-118">If the sysprep was not run on the VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="431c9-119">Seçin **Tamam** özel görüntü oluşturmak için bitirdikten sonra.</span><span class="sxs-lookup"><span data-stu-id="431c9-119">Select **OK** when finished to create the custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="431c9-120">İlgili blog gönderileri</span><span class="sxs-lookup"><span data-stu-id="431c9-120">Related blog posts</span></span>

- [<span data-ttu-id="431c9-121">Özel resimler veya formüller?</span><span class="sxs-lookup"><span data-stu-id="431c9-121">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="431c9-122">Azure DevTest Labs arasında özel resimler kopyalama</span><span class="sxs-lookup"><span data-stu-id="431c9-122">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="431c9-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="431c9-123">Next steps</span></span>

- [<span data-ttu-id="431c9-124">Laboratuvarınızı için bir VM ekleme</span><span class="sxs-lookup"><span data-stu-id="431c9-124">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
