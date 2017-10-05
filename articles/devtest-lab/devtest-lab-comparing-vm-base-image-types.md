---
title: "Özel resimler ve DevTest Labs formüller karşılaştırma | Microsoft Docs"
description: "Hangisinin ortamınıza en uygun karar vermem VM taban gibi özel resimler ve formülleri arasındaki farklar hakkında bilgi edinin."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a3cb259a-7d80-40ec-8ee8-45105704d589
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tarcher
ms.openlocfilehash: ff771abc26c08f0adb977c29739d2f5c91924b21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a><span data-ttu-id="9a44e-103">Özel resimler ve DevTest Labs formüller karşılaştırma</span><span class="sxs-lookup"><span data-stu-id="9a44e-103">Comparing custom images and formulas in DevTest Labs</span></span>
<span data-ttu-id="9a44e-104">Her ikisi de [özel resimler](devtest-lab-create-template.md) ve [formüller](devtest-lab-manage-formulas.md) için tabanları olarak kullanılan [yeni VM'ler oluşturulan](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="9a44e-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm-with-artifacts.md).</span></span> <span data-ttu-id="9a44e-105">Ancak, özel resimler ve formülleri arasında anahtar fark özel görüntü yalnızca bir formül VHD dayanan bir görüntü olsa da bir VHD'de dayanan bir görüntü olmasıdır *ek olarak* ayarları - VM boyutunu, sanal ağ, alt ağ ve yapıları gibi önceden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="9a44e-105">However, the key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span></span> <span data-ttu-id="9a44e-106">Önceden yapılandırılmış bu ayarları VM oluşturma sırasında geçersiz kılınabilir varsayılan değerlerle ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="9a44e-106">These preconfigured settings are set up with default values that can be overridden at the time of VM creation.</span></span> <span data-ttu-id="9a44e-107">Bu makalede (uzmanları için) olumlu ve olumsuz (olumsuz) bazıları formülleri kullanma karşı özel resimler kullanmaya açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9a44e-107">This article explains some of the advantages (pros) and disadvantages (cons) to using custom images versus using formulas.</span></span>

## <a name="custom-image-pros-and-cons"></a><span data-ttu-id="9a44e-108">Özel görüntü Artıları ve eksileri</span><span class="sxs-lookup"><span data-stu-id="9a44e-108">Custom image pros and cons</span></span>
<span data-ttu-id="9a44e-109">Özel resimler VM'ler istenen ortamından oluşturmak için statik, sabit bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a44e-109">Custom images provide a static, immutable way to create VMs from a desired environment.</span></span> 

<span data-ttu-id="9a44e-110">**Uzmanları**</span><span class="sxs-lookup"><span data-stu-id="9a44e-110">**Pros**</span></span>

* <span data-ttu-id="9a44e-111">VM çalışmaya görüntüden başlar sonra hiçbir şey değiştiğinde, özel bir görüntüden VM sağlamayı hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="9a44e-111">VM provisioning from a custom image is fast as nothing changes after the VM is spun up from the image.</span></span> <span data-ttu-id="9a44e-112">Diğer bir deyişle, özel görüntü ayarları olmadan yalnızca bir resim olarak uygulamak için ayar yok.</span><span class="sxs-lookup"><span data-stu-id="9a44e-112">In other words, there are no settings to apply as the custom image is just an image without settings.</span></span> 
* <span data-ttu-id="9a44e-113">Tek bir özel görüntüden oluşturulan VM'ler aynıdır.</span><span class="sxs-lookup"><span data-stu-id="9a44e-113">VMs created from a single custom image are identical.</span></span>

<span data-ttu-id="9a44e-114">**Simgeler**</span><span class="sxs-lookup"><span data-stu-id="9a44e-114">**Cons**</span></span>

* <span data-ttu-id="9a44e-115">Özel görüntü bazı yönlerinin güncellemeniz gerekiyorsa, görüntüyü yeniden oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9a44e-115">If you need to update some aspect of the custom image, the image must be recreated.</span></span>  

## <a name="formula-pros-and-cons"></a><span data-ttu-id="9a44e-116">Formül Artıları ve eksileri</span><span class="sxs-lookup"><span data-stu-id="9a44e-116">Formula pros and cons</span></span>
<span data-ttu-id="9a44e-117">Formülleri VM'ler istenen yapılandırma/ayarlarından oluşturmak için dinamik bir yolunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a44e-117">Formulas provide a dynamic way to create VMs from the desired configuration/settings.</span></span>

<span data-ttu-id="9a44e-118">**Uzmanları**</span><span class="sxs-lookup"><span data-stu-id="9a44e-118">**Pros**</span></span>

* <span data-ttu-id="9a44e-119">Ortam değişiklikleri yapıları aracılığıyla kolay bir şekilde yakalanır.</span><span class="sxs-lookup"><span data-stu-id="9a44e-119">Changes in the environment can be captured on the fly via artifacts.</span></span> <span data-ttu-id="9a44e-120">Örneğin, en son sürüm hattınızı bitten yüklü olan bir VM istediğiniz veya en son kodu, depodan listeleme, yalnızca, bir hedef temel görüntü birlikte formülünde en son kod kaydeder veya son BITS dağıtan bir yapıya belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a44e-120">For example, if you want a VM installed with the latest bits from your release pipeline or enlist the latest code from your repository, you can simply specify an artifact that deploys the latest bits or enlists the latest code in the formula together with a target base image.</span></span> <span data-ttu-id="9a44e-121">Bu formülü VM'ler oluşturmak için kullanılan her durumda, en son BITS/kodu dağıtılan/kayıtlı VM.</span><span class="sxs-lookup"><span data-stu-id="9a44e-121">Whenever this formula is used to create VMs, the latest bits/code are deployed/enlisted to the VM.</span></span> 
* <span data-ttu-id="9a44e-122">Formülleri özel resimler - VM boyutları ve sanal ağ ayarları gibi sağlayamaz varsayılan ayarlarını tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a44e-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span></span> 
* <span data-ttu-id="9a44e-123">Bir formüle, kaydedilen ayarlar, varsayılan değerler olarak gösterilir, ancak VM oluşturulduğunda değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="9a44e-123">The settings saved in a formula are shown as default values, but can be modified when the VM is created.</span></span> 

<span data-ttu-id="9a44e-124">**Simgeler**</span><span class="sxs-lookup"><span data-stu-id="9a44e-124">**Cons**</span></span>

* <span data-ttu-id="9a44e-125">Bir formülünden bir VM oluşturma, özel bir görüntüden bir VM oluşturma değerinden daha uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="9a44e-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="9a44e-126">İlgili blog gönderileri</span><span class="sxs-lookup"><span data-stu-id="9a44e-126">Related blog posts</span></span>
* [<span data-ttu-id="9a44e-127">Özel resimler veya formüller?</span><span class="sxs-lookup"><span data-stu-id="9a44e-127">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="9a44e-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9a44e-128">Next steps</span></span>
- [<span data-ttu-id="9a44e-129">DevTest Labs SSS</span><span class="sxs-lookup"><span data-stu-id="9a44e-129">DevTest Labs FAQ</span></span>](devtest-lab-faq.md)