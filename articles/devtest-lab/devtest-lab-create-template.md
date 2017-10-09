---
title: "Azure DevTest Labs özel görüntüyü bir VHD dosyasından aaaCreate | Microsoft Docs"
description: "Nasıl toocreate VHD dosyasını kullanarak Azure DevTest Labs özel bir görüntü hello Azure portal öğrenin"
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
ms.openlocfilehash: 80af8ea1cb72380f868df0a76c4a0dcd92e63cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="4a321-103">Bir VHD dosyasındaki özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="4a321-103">Create a custom image from a VHD file</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="4a321-104">Adım adım yönergeler</span><span class="sxs-lookup"><span data-stu-id="4a321-104">Step-by-step instructions</span></span>

<span data-ttu-id="4a321-105">Merhaba aşağıdaki adımlar, özel bir görüntü hello Azure portal kullanarak bir VHD'yi dosyasından oluşturmada size yol:</span><span class="sxs-lookup"><span data-stu-id="4a321-105">hello following steps walk you through creating a custom image from a VHD file using hello Azure portal:</span></span>

1. <span data-ttu-id="4a321-106">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="4a321-106">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="4a321-107">Seçin **daha fazla hizmet**ve ardından **DevTest Labs** hello listeden.</span><span class="sxs-lookup"><span data-stu-id="4a321-107">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="4a321-108">Merhaba istenen Laboratuvar labs Hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="4a321-108">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="4a321-109">Merhaba Laboratuvar'ın dikey penceresinde, seçin **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="4a321-109">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="4a321-110">Merhaba Laboratuvar üzerinde **yapılandırma** dikey penceresinde, select **özel görüntülerini (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="4a321-110">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="4a321-111">Merhaba üzerinde **özel görüntüleri** dikey penceresinde, select **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4a321-111">On hello **Custom images** blade, select **+Add**.</span></span>

    ![Özel görüntü ekleme](./media/devtest-lab-create-template/add-custom-image.png)

1. <span data-ttu-id="4a321-113">Merhaba özel görüntü Hello adını girin.</span><span class="sxs-lookup"><span data-stu-id="4a321-113">Enter hello name of hello custom image.</span></span> <span data-ttu-id="4a321-114">Bu ad, bir VM oluşturulurken hello temel görüntü listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4a321-114">This name is displayed in hello list of base images when creating a VM.</span></span>

1. <span data-ttu-id="4a321-115">Merhaba özel görüntü Hello açıklamasını girin.</span><span class="sxs-lookup"><span data-stu-id="4a321-115">Enter hello description of hello custom image.</span></span> <span data-ttu-id="4a321-116">Bu açıklama, bir VM oluşturulurken hello temel görüntü listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4a321-116">This description is displayed in hello list of base images when creating a VM.</span></span>

1. <span data-ttu-id="4a321-117">Seçin **VHD**.</span><span class="sxs-lookup"><span data-stu-id="4a321-117">Select **VHD**.</span></span>

1. <span data-ttu-id="4a321-118">Merhaba gelen **VHD** dikey penceresinde, istenen select hello VHD dosyası.</span><span class="sxs-lookup"><span data-stu-id="4a321-118">From hello **VHD** blade, select hello desired VHD file.</span></span>

1. <span data-ttu-id="4a321-119">Seçin **Tamam** tooclose hello **VHD** dikey.</span><span class="sxs-lookup"><span data-stu-id="4a321-119">Select **OK** tooclose hello **VHD** blade.</span></span>

1. <span data-ttu-id="4a321-120">Seçin **işletim sistemi yapılandırması**.</span><span class="sxs-lookup"><span data-stu-id="4a321-120">Select **OS configuration**.</span></span>

1. <span data-ttu-id="4a321-121">Merhaba üzerinde **işletim sistemi yapılandırması** sekmesinde, ya da seçin **Windows** veya **Linux**.</span><span class="sxs-lookup"><span data-stu-id="4a321-121">On hello **OS configuration** tab, select either **Windows** or **Linux**.</span></span>

1. <span data-ttu-id="4a321-122">Varsa **Windows** olan hello onay kutusu seçildiyse olup olmadığını *Sysprep* hello makinede çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4a321-122">If **Windows** is selected, specify via hello checkbox whether *Sysprep* has been run on hello machine.</span></span> 

1. <span data-ttu-id="4a321-123">Seçin **Tamam** tooclose hello **işletim sistemi yapılandırması** dikey.</span><span class="sxs-lookup"><span data-stu-id="4a321-123">Select **OK** tooclose hello **OS configuration** blade.</span></span>

1. <span data-ttu-id="4a321-124">Seçin **Tamam** toocreate hello özel görüntü.</span><span class="sxs-lookup"><span data-stu-id="4a321-124">Select **OK** toocreate hello custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="4a321-125">İlgili blog gönderileri</span><span class="sxs-lookup"><span data-stu-id="4a321-125">Related blog posts</span></span>

- [<span data-ttu-id="4a321-126">Özel resimler veya formüller?</span><span class="sxs-lookup"><span data-stu-id="4a321-126">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="4a321-127">Azure DevTest Labs arasında özel resimler kopyalama</span><span class="sxs-lookup"><span data-stu-id="4a321-127">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="4a321-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4a321-128">Next steps</span></span>

- [<span data-ttu-id="4a321-129">VM tooyour Laboratuvar ekleme</span><span class="sxs-lookup"><span data-stu-id="4a321-129">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
