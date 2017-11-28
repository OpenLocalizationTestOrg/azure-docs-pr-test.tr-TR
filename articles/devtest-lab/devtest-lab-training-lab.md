---
title: "Eğitim için Azure DevTest Labs aaaUse | Microsoft Docs"
description: "Bilgi nasıl toouse Azure DevTest Labs eğitim senaryoları için."
services: devtest-lab,virtual-machines
documentationcenter: na
author: steved0x
manager: douge
editor: 
ms.assetid: 57ff4e30-7e33-453f-9867-e19b3fdb9fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/12/2016
ms.author: sdanie
ms.openlocfilehash: 4a5f44a282d8f6a58849c730ff89237ccff39ca8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-training"></a><span data-ttu-id="41082-103">Azure DevTest Labs için eğitim kullanın</span><span class="sxs-lookup"><span data-stu-id="41082-103">Use Azure DevTest Labs for training</span></span>
<span data-ttu-id="41082-104">Azure DevTest Labs kullanılan tooimplement toplama toodev ve test birçok anahtar senaryolarda olabilir.</span><span class="sxs-lookup"><span data-stu-id="41082-104">Azure DevTest Labs can be used tooimplement many key scenarios in addition toodev/test.</span></span> <span data-ttu-id="41082-105">Bu senaryolarda bir laboratuvar eğitim için yukarı tooset biridir.</span><span class="sxs-lookup"><span data-stu-id="41082-105">One of those scenarios is tooset up a lab for training.</span></span> <span data-ttu-id="41082-106">Azure DevTest Labs toocreate özel şablonlar sağlayabileceğiniz bir laboratuvar verir her Yardımcısı toocreate aynı ve yalıtılmış ortamlar için eğitim kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41082-106">Azure DevTest Labs allows you toocreate a lab where you can provide custom templates that each trainee can use toocreate identical and isolated environments for training.</span></span> <span data-ttu-id="41082-107">Yalnızca bunları ihtiyaç duydukları ve sanal makineleri için hello eğitim gerekli gibi-yeterli kaynak - içeren kullandığınızda eğitim ortamları kullanılabilir tooeach Yardımcısı olduğunu ilkeleri tooensure uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41082-107">You can apply policies tooensure that training environments are available tooeach trainee only when they need them and contain enough resources - such as virtual machines - required for hello training.</span></span> <span data-ttu-id="41082-108">Son olarak, tek bir tıklatmayla erişebilirsiniz trainees ile kolayca hello Laboratuvar paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41082-108">Finally, you can easily share hello lab with trainees, which they can access in one click.</span></span>

![DevTest Labs için eğitim kullanın](./media/devtest-lab-training-lab/devtest-lab-training.png)

<span data-ttu-id="41082-110">Azure DevTest Labs herhangi bir sanal ortam gerekli tooconduct Eğitim gereksinimleri aşağıdaki hello uyuyor:</span><span class="sxs-lookup"><span data-stu-id="41082-110">Azure DevTest Labs meets hello following requirements that are required tooconduct training in any virtual environment:</span></span> 

* <span data-ttu-id="41082-111">Trainees diğer trainees tarafından oluşturulan VM'ler göremiyorum</span><span class="sxs-lookup"><span data-stu-id="41082-111">Trainees cannot see VMs created by other trainees</span></span>
* <span data-ttu-id="41082-112">Her eğitim makine özdeş olmalıdır</span><span class="sxs-lookup"><span data-stu-id="41082-112">Every training machine should be identical</span></span>
* <span data-ttu-id="41082-113">Trainees eğitim ortamlarının hızlı bir şekilde sağlayabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="41082-113">Trainees can quickly provision their training environments</span></span>
* <span data-ttu-id="41082-114">Bunları kullanmıyorsanız, bunlar hello eğitim ve ayrıca kapatma VM'ler için gerekenden daha fazla VMs trainees alınamıyor sağlayarak maliyet denetimi</span><span class="sxs-lookup"><span data-stu-id="41082-114">Control cost by ensuring that trainees cannot get more VMs than they need for hello training and also shutdown VMs when they are not using them</span></span>
* <span data-ttu-id="41082-115">Merhaba eğitim Laboratuvar her Yardımcısı ile kolayca paylaşın</span><span class="sxs-lookup"><span data-stu-id="41082-115">Easily share hello training lab with each trainee</span></span>
* <span data-ttu-id="41082-116">Merhaba eğitim Laboratuvar yeniden yeniden</span><span class="sxs-lookup"><span data-stu-id="41082-116">Reuse hello training lab again and again</span></span>

<span data-ttu-id="41082-117">Bu makalede, Eğitim gereksinimleri ve eğitim için bir laboratuvar yukarı tooset izleyebileceğiniz ayrıntılı adımlar toomeet hello daha önce açıklanan kullanılabilen çeşitli Azure DevTest Labs özelliklerini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="41082-117">In this article, you learn about various Azure DevTest Labs features that can be used toomeet hello previously described training requirements and detailed steps that you can follow tooset up a lab for training.</span></span>  

## <a name="implementing-training-with-azure-devtest-labs"></a><span data-ttu-id="41082-118">Azure DevTest Labs eğitime uygulama</span><span class="sxs-lookup"><span data-stu-id="41082-118">Implementing training with Azure DevTest Labs</span></span>
1. <span data-ttu-id="41082-119">**Merhaba Laboratuvar oluşturma**</span><span class="sxs-lookup"><span data-stu-id="41082-119">**Create hello lab**</span></span> 
   
    <span data-ttu-id="41082-120">Labs hello Azure DevTest Labs'de başlangıç noktası var.</span><span class="sxs-lookup"><span data-stu-id="41082-120">Labs are hello starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="41082-121">Bir laboratuvar oluşturduktan sonra görevleri hızla oluşturabilirsiniz VM görüntüleri gibi kullanıcıların (trainees) toohello Laboratuvar, kümesi ilkeleri toocontrol maliyetleri ekledikçe tanımlayın ve daha fazlasını gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41082-121">Once you create a lab, you can perform tasks such as add users (trainees) toohello lab, set policies toocontrol costs, define VM images that can create quickly, and more.</span></span>   
   
    <span data-ttu-id="41082-122">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="41082-122">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="41082-123">Görev</span><span class="sxs-lookup"><span data-stu-id="41082-123">Task</span></span> | <span data-ttu-id="41082-124">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="41082-124">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="41082-125">Azure DevTest Labs'de Laboratuvar oluşturma</span><span class="sxs-lookup"><span data-stu-id="41082-125">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="41082-126">Azure DevTest Labs'de Laboratuvar bir toocreate hello Azure portalına nasıl öğrenin.</span><span class="sxs-lookup"><span data-stu-id="41082-126">Learn how toocreate a lab in Azure DevTest Labs in hello Azure portal.</span></span> |
2. <span data-ttu-id="41082-127">**Eğitim VM'ler hazır Market görüntülerini ve özel görüntüleri kullanarak dakikalar içinde oluşturma**</span><span class="sxs-lookup"><span data-stu-id="41082-127">**Create training VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="41082-128">Görüntüler çok geniş bir yelpazedeki hazır görüntülerden hello Azure Marketi seçer ve hello laboratuarda hello trainees için kullanılabilir duruma getirmek.</span><span class="sxs-lookup"><span data-stu-id="41082-128">You can pick ready-made images from a wide variety of images in hello Azure Marketplace and make them available for hello trainees in hello lab.</span></span> <span data-ttu-id="41082-129">Merhaba hazır görüntüleri gereksinimlerinizi karşılamıyorsa, Laboratuvar Azure hello Laboratuvar özel görüntü olarak hello VM kaydetme ve hello eğitim için gereken tüm hello yazılım yükleme Marketi'nden hazır bir görüntü kullanarak VM oluşturarak özel bir görüntü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41082-129">If hello ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all hello software that you need for hello training, and saving hello VM as custom image in hello lab.</span></span> 
   
    <span data-ttu-id="41082-130">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="41082-130">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="41082-131">Görev</span><span class="sxs-lookup"><span data-stu-id="41082-131">Task</span></span> | <span data-ttu-id="41082-132">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="41082-132">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="41082-133">Azure Market görüntülerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="41082-133">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="41082-134">Beyaz liste Azure Market görüntülerini öğrenin; Seçimi yalnızca hello görüntüler için kullanılabilir hale getirme için hello eğitim istiyor.</span><span class="sxs-lookup"><span data-stu-id="41082-134">Learn how you can whitelist Azure Marketplace images; making available for selection only hello images you want for hello training.</span></span> |
   | [<span data-ttu-id="41082-135">Özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="41082-135">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="41082-136">Özel bir görüntü trainees hızlı bir şekilde hello özel görüntü kullanarak bir VM'i oluşturabilmeniz için hello eğitim ihtiyacınız hello yazılım yüklenerek oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41082-136">Create a custom image by pre-installing hello software you need for hello training so that trainees can quickly create a VM using hello custom image.</span></span> |
3. <span data-ttu-id="41082-137">**Eğitim makineler için yeniden kullanılabilir şablonlar oluşturma**</span><span class="sxs-lookup"><span data-stu-id="41082-137">**Create reusable templates for training machines**</span></span> 
   
    <span data-ttu-id="41082-138">Azure DevTest Labs formülde varsayılan özellik değerleri listesine toocreate VM kullanılır.</span><span class="sxs-lookup"><span data-stu-id="41082-138">A formula in Azure DevTest Labs is a list of default property values used toocreate a VM.</span></span> <span data-ttu-id="41082-139">Görüntü, VM boyutu (CPU ve RAM birleşimi) ve bir sanal ağı seçerek hello laboratuarda bir formül oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41082-139">You can create a formula in hello lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="41082-140">Her Yardımcısı hello Laboratuvar hello formülde görebilir ve toocreate VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="41082-140">Each trainee can see hello formula in hello lab and use it toocreate a VM.</span></span> 
   
    <span data-ttu-id="41082-141">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="41082-141">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="41082-142">Görev</span><span class="sxs-lookup"><span data-stu-id="41082-142">Task</span></span> | <span data-ttu-id="41082-143">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="41082-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="41082-144">DevTest Labs formüller toocreate sanal makineleri yönetme</span><span class="sxs-lookup"><span data-stu-id="41082-144">Manage DevTest Labs formulas toocreate VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="41082-145">Görüntü, VM boyutu (CPU ve RAM birleşimi) ve bir sanal ağ seçerek bir formül nasıl oluşturabileceğinizi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="41082-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span> |
4. <span data-ttu-id="41082-146">**Denetim maliyetleri**</span><span class="sxs-lookup"><span data-stu-id="41082-146">**Control costs**</span></span>
   
    <span data-ttu-id="41082-147">Azure DevTest Labs hello Laboratuvar toospecify hello en fazla sayıda hello laboratuarda Yardımcısı tarafından oluşturulan sanal makineleri tooset bir ilke sağlar.</span><span class="sxs-lookup"><span data-stu-id="41082-147">Azure DevTest Labs allows you tooset a policy in hello lab toospecify hello maximum number of VMs that can be created by a trainee in hello lab.</span></span> 
   
    <span data-ttu-id="41082-148">Birden çok gün eğitim gerçekleştirme ve toostop tüm hello VM'ler hello günün belirli bir zamanda istediğiniz ve ardından bunları günü izleyen hello otomatik olarak yeniden, kolayca otomatik kapatma ayarı tarafından gerçekleştirmek ve otomatik başlatma hello Laboratuvar ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="41082-148">If you are conducting multi-day training and want toostop all hello VMs at a particular time of hello day and then automatically restart them hello following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in hello lab.</span></span> 
   
    <span data-ttu-id="41082-149">Eğitim tamamlandığında, son olarak, tüm hello sanal makineleri aynı anda tek bir PowerShell Betiği çalıştırarak silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41082-149">Finally, when training is complete you can delete all hello VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="41082-150">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="41082-150">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="41082-151">Görev</span><span class="sxs-lookup"><span data-stu-id="41082-151">Task</span></span> | <span data-ttu-id="41082-152">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="41082-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="41082-153">Laboratuvar ilkelerini tanımlama</span><span class="sxs-lookup"><span data-stu-id="41082-153">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="41082-154">Maliyetleri hello laboratuvarda ilkeleri ayarlayarak denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41082-154">Control costs by setting policies in hello lab.</span></span> |
   | [<span data-ttu-id="41082-155">Tüm hello Laboratuvar bir PowerShell komut dosyası kullanarak sanal makineleri silin</span><span class="sxs-lookup"><span data-stu-id="41082-155">Delete all hello lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="41082-156">Merhaba eğitim tamamlandığında, tek bir işlemde tüm hello labs silin.</span><span class="sxs-lookup"><span data-stu-id="41082-156">Delete all hello labs in one operation when hello training is complete.</span></span> |
5. <span data-ttu-id="41082-157">**Paylaşım hello laboratuvarla her Yardımcısı**</span><span class="sxs-lookup"><span data-stu-id="41082-157">**Share hello lab with each trainee**</span></span>
   
    <span data-ttu-id="41082-158">Labs, trainees ile paylaştığınız bir bağlantıyı kullanarak doğrudan erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="41082-158">Labs can be directly accessed using a link that you share with your trainees.</span></span> <span data-ttu-id="41082-159">Sahip oldukları sürece, trainees bile toohave bir Azure hesabınız yoksa bir [Microsoft hesabı](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="41082-159">Your trainees don't even have toohave an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="41082-160">Trainees diğer trainees tarafından oluşturulan VM'ler göremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="41082-160">Trainees cannot see VMs created by other trainees.</span></span>  
   
    <span data-ttu-id="41082-161">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="41082-161">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="41082-162">Görev</span><span class="sxs-lookup"><span data-stu-id="41082-162">Task</span></span> | <span data-ttu-id="41082-163">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="41082-163">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="41082-164">Azure DevTest Labs'de Yardımcısı tooa Laboratuvar ekleme</span><span class="sxs-lookup"><span data-stu-id="41082-164">Add a trainee tooa lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="41082-165">Hello Azure portal tooadd trainees tooyour eğitim Laboratuvar kullanın.</span><span class="sxs-lookup"><span data-stu-id="41082-165">Use hello Azure portal tooadd trainees tooyour training lab.</span></span> |
   | [<span data-ttu-id="41082-166">Bir PowerShell Betiği kullanılarak trainees toohello Laboratuvar ekleme</span><span class="sxs-lookup"><span data-stu-id="41082-166">Add trainees toohello lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="41082-167">PowerShell tooautomate trainees tooyour eğitim Laboratuvar ekleme kullanın.</span><span class="sxs-lookup"><span data-stu-id="41082-167">Use PowerShell tooautomate adding trainees tooyour training lab.</span></span> |
   | [<span data-ttu-id="41082-168">Bir bağlantı toohello Laboratuvar Al</span><span class="sxs-lookup"><span data-stu-id="41082-168">Get a link toohello lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="41082-169">Nasıl bir laboratuvar doğrudan bir köprü erişilebilen öğrenin.</span><span class="sxs-lookup"><span data-stu-id="41082-169">Learn how a lab can be directly accessed via a hyperlink.</span></span> |
6. <span data-ttu-id="41082-170">**Merhaba Laboratuvar yeniden yeniden**</span><span class="sxs-lookup"><span data-stu-id="41082-170">**Reuse hello lab again and again**</span></span> 
   
    <span data-ttu-id="41082-171">Laboratuvar oluşturma, Resource Manager şablonu oluşturma ve toocreate aynı labs tekrar tekrar kullanarak özel ayarları da dahil olmak üzere otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41082-171">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it toocreate identical labs again and again.</span></span> 
   
    <span data-ttu-id="41082-172">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="41082-172">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="41082-173">Görev</span><span class="sxs-lookup"><span data-stu-id="41082-173">Task</span></span> | <span data-ttu-id="41082-174">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="41082-174">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="41082-175">Resource Manager şablonu kullanarak bir laboratuvar oluşturma</span><span class="sxs-lookup"><span data-stu-id="41082-175">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="41082-176">Labs Resource Manager şablonları kullanarak Azure DevTest Labs içinde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41082-176">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

