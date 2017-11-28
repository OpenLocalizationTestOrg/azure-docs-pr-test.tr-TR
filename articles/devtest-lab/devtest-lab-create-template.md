---
title: "Bir VHD dosyasından Azure DevTest Labs özel görüntü oluşturma | Microsoft Docs"
description: "Azure DevTest Labs Azure portalını kullanarak bir VHD'yi dosyasından içinde özel bir görüntü oluşturmayı öğrenin"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: b795bc61-7c28-40e6-82fc-96d629ee0568
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 9983ea9b847f44ed18a6169a4bdb224b63626a64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="9f722-103">Bir VHD dosyasındaki özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="9f722-103">Create a custom image from a VHD file</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="9f722-104">Adım adım yönergeler</span><span class="sxs-lookup"><span data-stu-id="9f722-104">Step-by-step instructions</span></span>

<span data-ttu-id="9f722-105">Aşağıdaki adımlar, Azure portalını kullanarak bir VHD'yi dosyasından özel görüntü oluşturmada size yol:</span><span class="sxs-lookup"><span data-stu-id="9f722-105">The following steps walk you through creating a custom image from a VHD file using the Azure portal:</span></span>

1. <span data-ttu-id="9f722-106">[Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9f722-106">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="9f722-107">**More services**’i (Daha fazla hizmet’i) seçip ardından listeden **DevTest Labs**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="9f722-107">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="9f722-108">İstenen Laboratuvar labs listesinden seçin.</span><span class="sxs-lookup"><span data-stu-id="9f722-108">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="9f722-109">Laboratuvar 's dikey penceresinde, seçin **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="9f722-109">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="9f722-110">Laboratuvar üzerinde **yapılandırma** dikey penceresinde, select **özel görüntülerini (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="9f722-110">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="9f722-111">Üzerinde **özel görüntüleri** dikey penceresinde, select **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="9f722-111">On the **Custom images** blade, select **+Add**.</span></span>

    ![Özel görüntü ekleme](./media/devtest-lab-create-template/add-custom-image.png)

1. <span data-ttu-id="9f722-113">Özel görüntü adı girin.</span><span class="sxs-lookup"><span data-stu-id="9f722-113">Enter the name of the custom image.</span></span> <span data-ttu-id="9f722-114">Bu ad, bir VM oluşturulurken temel görüntü listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9f722-114">This name is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="9f722-115">Özel görüntü açıklamasını girin.</span><span class="sxs-lookup"><span data-stu-id="9f722-115">Enter the description of the custom image.</span></span> <span data-ttu-id="9f722-116">Bu açıklama, bir VM oluşturulurken temel görüntü listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9f722-116">This description is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="9f722-117">Seçin **VHD**.</span><span class="sxs-lookup"><span data-stu-id="9f722-117">Select **VHD**.</span></span>

1. <span data-ttu-id="9f722-118">Gelen **VHD** dikey penceresinde istenen VHD dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="9f722-118">From the **VHD** blade, select the desired VHD file.</span></span>

1. <span data-ttu-id="9f722-119">Seçin **Tamam** kapatmak için **VHD** dikey.</span><span class="sxs-lookup"><span data-stu-id="9f722-119">Select **OK** to close the **VHD** blade.</span></span>

1. <span data-ttu-id="9f722-120">Seçin **işletim sistemi yapılandırması**.</span><span class="sxs-lookup"><span data-stu-id="9f722-120">Select **OS configuration**.</span></span>

1. <span data-ttu-id="9f722-121">Üzerinde **işletim sistemi yapılandırması** sekmesinde, ya da seçin **Windows** veya **Linux**.</span><span class="sxs-lookup"><span data-stu-id="9f722-121">On the **OS configuration** tab, select either **Windows** or **Linux**.</span></span>

1. <span data-ttu-id="9f722-122">Varsa **Windows** olan onay kutusunu seçildiyse olup olmadığını *Sysprep* makinede çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9f722-122">If **Windows** is selected, specify via the checkbox whether *Sysprep* has been run on the machine.</span></span> 

1. <span data-ttu-id="9f722-123">Seçin **Tamam** kapatmak için **işletim sistemi yapılandırması** dikey.</span><span class="sxs-lookup"><span data-stu-id="9f722-123">Select **OK** to close the **OS configuration** blade.</span></span>

1. <span data-ttu-id="9f722-124">Seçin **Tamam** özel görüntüsü oluşturulamadı.</span><span class="sxs-lookup"><span data-stu-id="9f722-124">Select **OK** to create the custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="9f722-125">İlgili blog gönderileri</span><span class="sxs-lookup"><span data-stu-id="9f722-125">Related blog posts</span></span>

- [<span data-ttu-id="9f722-126">Özel resimler veya formüller?</span><span class="sxs-lookup"><span data-stu-id="9f722-126">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="9f722-127">Azure DevTest Labs arasında özel resimler kopyalama</span><span class="sxs-lookup"><span data-stu-id="9f722-127">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="9f722-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9f722-128">Next steps</span></span>

- [<span data-ttu-id="9f722-129">Laboratuvarınızı için bir VM ekleme</span><span class="sxs-lookup"><span data-stu-id="9f722-129">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
