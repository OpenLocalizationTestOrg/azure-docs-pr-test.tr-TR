---
title: "Azure DevTest Labs özel görüntüyü bir VM'den aaaCreate | Microsoft Docs"
description: "Nasıl toocreate sağlanan bir VM kullanarak Azure DevTest Labs özel bir görüntü hello Azure portal öğrenin"
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
ms.openlocfilehash: 7dccb79d3db4aae676c7bd2f6b800301210491e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="f7fb7-103">Bir sanal makineden özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="f7fb7-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="f7fb7-104">Adım adım yönergeler</span><span class="sxs-lookup"><span data-stu-id="f7fb7-104">Step-by-step instructions</span></span>

<span data-ttu-id="f7fb7-105">Sağlanan bir sanal makineden özel bir görüntü oluşturun ve daha sonra bu özel görüntü toocreate kullanın aynı VM'ler.</span><span class="sxs-lookup"><span data-stu-id="f7fb7-105">You can create a custom image from a provisioned VM, and afterwards use that custom image toocreate identical VMs.</span></span> <span data-ttu-id="f7fb7-106">Aşağıdaki adımları hello nasıl toocreate özel bir görüntü bir VM'den gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f7fb7-106">hello following steps illustrate how toocreate a custom image from a VM:</span></span>

1. <span data-ttu-id="f7fb7-107">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f7fb7-107">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="f7fb7-108">Seçin **daha fazla hizmet**ve ardından **DevTest Labs** hello listeden.</span><span class="sxs-lookup"><span data-stu-id="f7fb7-108">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="f7fb7-109">Merhaba istenen Laboratuvar labs Hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="f7fb7-109">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="f7fb7-110">Merhaba Laboratuvar'ın dikey penceresinde, seçin **My sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="f7fb7-110">On hello lab's blade, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="f7fb7-111">Merhaba üzerinde **My sanal makineleri** dikey penceresinde, toocreate hello özel görüntü istediğiniz select hello VM.</span><span class="sxs-lookup"><span data-stu-id="f7fb7-111">On hello **My virtual machines** blade, select hello VM from which you want toocreate hello custom image.</span></span>

1. <span data-ttu-id="f7fb7-112">Merhaba VM'in dikey penceresinde, seçin **oluşturma özel görüntü (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="f7fb7-112">On hello VM's blade, select **Create custom image (VHD)**.</span></span>

    ![Özel görüntü menü öğesi oluşturma](./media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="f7fb7-114">Merhaba üzerinde **oluşturma görüntü** dikey penceresinde, bir ad ve özel görüntünüzü açıklamasını girin.</span><span class="sxs-lookup"><span data-stu-id="f7fb7-114">On hello **Create image** blade, enter a name and description for your custom image.</span></span> <span data-ttu-id="f7fb7-115">Bir VM oluşturduğunuzda, bu bilgileri hello tabanları listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f7fb7-115">This information is displayed in hello list of bases when you create a VM.</span></span>

    ![Özel görüntü dikey penceresi oluşturma](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="f7fb7-117">Sysprep hello VM üzerinde çalıştırıldığı olup olmadığını seçin.</span><span class="sxs-lookup"><span data-stu-id="f7fb7-117">Select whether sysprep was run on hello VM.</span></span> <span data-ttu-id="f7fb7-118">Merhaba sysprep hello VM üzerinde çalıştırılmadı, sysprep bu özel görüntüsünü bir VM oluşturulduğunda çalıştırmak isteyip istemediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="f7fb7-118">If hello sysprep was not run on hello VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="f7fb7-119">Seçin **Tamam** ne zaman sona toocreate hello özel görüntü.</span><span class="sxs-lookup"><span data-stu-id="f7fb7-119">Select **OK** when finished toocreate hello custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="f7fb7-120">İlgili blog gönderileri</span><span class="sxs-lookup"><span data-stu-id="f7fb7-120">Related blog posts</span></span>

- [<span data-ttu-id="f7fb7-121">Özel resimler veya formüller?</span><span class="sxs-lookup"><span data-stu-id="f7fb7-121">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="f7fb7-122">Azure DevTest Labs arasında özel resimler kopyalama</span><span class="sxs-lookup"><span data-stu-id="f7fb7-122">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="f7fb7-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f7fb7-123">Next steps</span></span>

- [<span data-ttu-id="f7fb7-124">VM tooyour Laboratuvar ekleme</span><span class="sxs-lookup"><span data-stu-id="f7fb7-124">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
