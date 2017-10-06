---
title: "aaaComparing özel resimler ve DevTest Labs formüller | Microsoft Docs"
description: "Hangisinin ortamınıza en uygun karar vermem VM taban gibi hello özel resimler ve formülleri arasındaki farklar hakkında bilgi edinin."
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
ms.openlocfilehash: 3c1d88dfe0ff94b8e825bb7a0b4aca3341c9330d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a><span data-ttu-id="6d066-103">Özel resimler ve DevTest Labs formüller karşılaştırma</span><span class="sxs-lookup"><span data-stu-id="6d066-103">Comparing custom images and formulas in DevTest Labs</span></span>
<span data-ttu-id="6d066-104">Her ikisi de [özel resimler](devtest-lab-create-template.md) ve [formüller](devtest-lab-manage-formulas.md) için tabanları olarak kullanılan [yeni VM'ler oluşturulan](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="6d066-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm-with-artifacts.md).</span></span> <span data-ttu-id="6d066-105">Ancak, özel resimler ve formülleri arasında hello anahtar fark özel görüntü yalnızca bir formül VHD dayanan bir görüntü olsa da bir VHD'de dayanan bir görüntü olmasıdır *ek olarak* ayarları - VM boyutunu, sanal ağ gibi önceden yapılandırılmış alt ağ ve yapıları.</span><span class="sxs-lookup"><span data-stu-id="6d066-105">However, hello key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span></span> <span data-ttu-id="6d066-106">Bu önceden yapılandırılmış ayarlar hello VM oluşturma sırasında geçersiz kılınabilir varsayılan değerlerle ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="6d066-106">These preconfigured settings are set up with default values that can be overridden at hello time of VM creation.</span></span> <span data-ttu-id="6d066-107">Bu makalede bazı hello avantajları (uzmanları için) açıklanır ve formülleri kullanma karşılaştırması (olumsuz) toousing özel resimler olumsuz.</span><span class="sxs-lookup"><span data-stu-id="6d066-107">This article explains some of hello advantages (pros) and disadvantages (cons) toousing custom images versus using formulas.</span></span>

## <a name="custom-image-pros-and-cons"></a><span data-ttu-id="6d066-108">Özel görüntü Artıları ve eksileri</span><span class="sxs-lookup"><span data-stu-id="6d066-108">Custom image pros and cons</span></span>
<span data-ttu-id="6d066-109">Özel resimler statik ve sabit bir yol toocreate istenen ortamından VM'ler sağlar.</span><span class="sxs-lookup"><span data-stu-id="6d066-109">Custom images provide a static, immutable way toocreate VMs from a desired environment.</span></span> 

<span data-ttu-id="6d066-110">**Uzmanları**</span><span class="sxs-lookup"><span data-stu-id="6d066-110">**Pros**</span></span>

* <span data-ttu-id="6d066-111">Merhaba görüntüden hiçbir şey değiştiğinde VM çalışmaya başlar hello sonra özel bir görüntüden sağlama VM hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="6d066-111">VM provisioning from a custom image is fast as nothing changes after hello VM is spun up from hello image.</span></span> <span data-ttu-id="6d066-112">Diğer bir deyişle, yalnızca bir resim ayarları olmadan hello özel görüntü olarak hiçbir ayarları tooapply vardır.</span><span class="sxs-lookup"><span data-stu-id="6d066-112">In other words, there are no settings tooapply as hello custom image is just an image without settings.</span></span> 
* <span data-ttu-id="6d066-113">Tek bir özel görüntüden oluşturulan VM'ler aynıdır.</span><span class="sxs-lookup"><span data-stu-id="6d066-113">VMs created from a single custom image are identical.</span></span>

<span data-ttu-id="6d066-114">**Simgeler**</span><span class="sxs-lookup"><span data-stu-id="6d066-114">**Cons**</span></span>

* <span data-ttu-id="6d066-115">Bazı yönlerinin hello özel görüntü tooupdate gerekiyorsa, hello görüntü yeniden oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6d066-115">If you need tooupdate some aspect of hello custom image, hello image must be recreated.</span></span>  

## <a name="formula-pros-and-cons"></a><span data-ttu-id="6d066-116">Formül Artıları ve eksileri</span><span class="sxs-lookup"><span data-stu-id="6d066-116">Formula pros and cons</span></span>
<span data-ttu-id="6d066-117">Formülleri dinamik şekilde toocreate VM'ler istenen hello yapılandırması/ayarlarını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="6d066-117">Formulas provide a dynamic way toocreate VMs from hello desired configuration/settings.</span></span>

<span data-ttu-id="6d066-118">**Uzmanları**</span><span class="sxs-lookup"><span data-stu-id="6d066-118">**Pros**</span></span>

* <span data-ttu-id="6d066-119">Merhaba ortam değişiklikleri hello kolay bir şekilde yapıları aracılığıyla yakalanır.</span><span class="sxs-lookup"><span data-stu-id="6d066-119">Changes in hello environment can be captured on hello fly via artifacts.</span></span> <span data-ttu-id="6d066-120">Merhaba en son sürüm hattınızı bitten yüklü olan bir VM istediğiniz veya hello en son kod, depodan listeleme, örneğin, yalnızca hello en son kod ile birlikte hello formülünde kaydeder veya hello son BITS dağıtan bir yapı belirleyebileceğiniz bir Hedef temel görüntü.</span><span class="sxs-lookup"><span data-stu-id="6d066-120">For example, if you want a VM installed with hello latest bits from your release pipeline or enlist hello latest code from your repository, you can simply specify an artifact that deploys hello latest bits or enlists hello latest code in hello formula together with a target base image.</span></span> <span data-ttu-id="6d066-121">Bu formülü kullanılan toocreate VM'ler olduğunda hello son BITS/kod toohello VM dağıtılan ve kayıtlı olan.</span><span class="sxs-lookup"><span data-stu-id="6d066-121">Whenever this formula is used toocreate VMs, hello latest bits/code are deployed/enlisted toohello VM.</span></span> 
* <span data-ttu-id="6d066-122">Formülleri özel resimler - VM boyutları ve sanal ağ ayarları gibi sağlayamaz varsayılan ayarlarını tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d066-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span></span> 
* <span data-ttu-id="6d066-123">Formül kaydedilmiş hello ayarları varsayılan değerler olarak gösterilir, ancak hello VM oluşturulduğunda değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="6d066-123">hello settings saved in a formula are shown as default values, but can be modified when hello VM is created.</span></span> 

<span data-ttu-id="6d066-124">**Simgeler**</span><span class="sxs-lookup"><span data-stu-id="6d066-124">**Cons**</span></span>

* <span data-ttu-id="6d066-125">Bir formülünden bir VM oluşturma, özel bir görüntüden bir VM oluşturma değerinden daha uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="6d066-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="6d066-126">İlgili blog gönderileri</span><span class="sxs-lookup"><span data-stu-id="6d066-126">Related blog posts</span></span>
* [<span data-ttu-id="6d066-127">Özel resimler veya formüller?</span><span class="sxs-lookup"><span data-stu-id="6d066-127">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="6d066-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6d066-128">Next steps</span></span>
- [<span data-ttu-id="6d066-129">DevTest Labs SSS</span><span class="sxs-lookup"><span data-stu-id="6d066-129">DevTest Labs FAQ</span></span>](devtest-lab-faq.md)