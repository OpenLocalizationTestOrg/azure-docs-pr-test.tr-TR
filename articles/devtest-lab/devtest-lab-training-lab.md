---
title: "Azure DevTest Labs için eğitim kullanın | Microsoft Docs"
description: "Eğitim senaryoları için Azure DevTest Labs kullanmayı öğrenin."
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
ms.openlocfilehash: a85999b7963e9a07d3f91ec47f298f91439c0808
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-devtest-labs-for-training"></a><span data-ttu-id="5d922-103">Azure DevTest Labs için eğitim kullanın</span><span class="sxs-lookup"><span data-stu-id="5d922-103">Use Azure DevTest Labs for training</span></span>
<span data-ttu-id="5d922-104">Azure DevTest Labs, geliştirme ve test ek olarak birçok temel senaryolar uygulamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5d922-104">Azure DevTest Labs can be used to implement many key scenarios in addition to dev/test.</span></span> <span data-ttu-id="5d922-105">Bu senaryolardan biri, eğitim için bir laboratuvar ayarlamaktır.</span><span class="sxs-lookup"><span data-stu-id="5d922-105">One of those scenarios is to set up a lab for training.</span></span> <span data-ttu-id="5d922-106">Azure DevTest Labs, burada her Yardımcısı Eğitim aynı ve yalıtılmış ortamlar oluşturmak için kullanabileceğiniz özel şablonlar sağlayabilir Laboratuvar oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="5d922-106">Azure DevTest Labs allows you to create a lab where you can provide custom templates that each trainee can use to create identical and isolated environments for training.</span></span> <span data-ttu-id="5d922-107">Yalnızca bunları ihtiyaç duydukları ve sanal makineleri için eğitim gerekli gibi-yeterli kaynak - içeren zaman eğitim ortamlar için her Yardımcısı kullanılabilir olduğundan emin olmak için ilkeleri uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5d922-107">You can apply policies to ensure that training environments are available to each trainee only when they need them and contain enough resources - such as virtual machines - required for the training.</span></span> <span data-ttu-id="5d922-108">Son olarak, tek bir tıklatmayla erişebilirsiniz trainees ile kolayca Laboratuvar paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5d922-108">Finally, you can easily share the lab with trainees, which they can access in one click.</span></span>

![DevTest Labs için eğitim kullanın](./media/devtest-lab-training-lab/devtest-lab-training.png)

<span data-ttu-id="5d922-110">Azure DevTest Labs, herhangi bir sanal ortam eğitim yürütmek için gerekli aşağıdaki gereksinimleri karşılayan:</span><span class="sxs-lookup"><span data-stu-id="5d922-110">Azure DevTest Labs meets the following requirements that are required to conduct training in any virtual environment:</span></span> 

* <span data-ttu-id="5d922-111">Trainees diğer trainees tarafından oluşturulan VM'ler göremiyorum</span><span class="sxs-lookup"><span data-stu-id="5d922-111">Trainees cannot see VMs created by other trainees</span></span>
* <span data-ttu-id="5d922-112">Her eğitim makine özdeş olmalıdır</span><span class="sxs-lookup"><span data-stu-id="5d922-112">Every training machine should be identical</span></span>
* <span data-ttu-id="5d922-113">Trainees eğitim ortamlarının hızlı bir şekilde sağlayabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5d922-113">Trainees can quickly provision their training environments</span></span>
* <span data-ttu-id="5d922-114">Bunları kullanmıyorsanız eğitim ve kapatma VM'ler için de gereksinim olandan daha fazla VMs trainees alınamıyor sağlayarak maliyet denetimi</span><span class="sxs-lookup"><span data-stu-id="5d922-114">Control cost by ensuring that trainees cannot get more VMs than they need for the training and also shutdown VMs when they are not using them</span></span>
* <span data-ttu-id="5d922-115">Eğitim Laboratuvar her Yardımcısı ile kolayca paylaşın</span><span class="sxs-lookup"><span data-stu-id="5d922-115">Easily share the training lab with each trainee</span></span>
* <span data-ttu-id="5d922-116">Eğitim Laboratuvar yeniden yeniden</span><span class="sxs-lookup"><span data-stu-id="5d922-116">Reuse the training lab again and again</span></span>

<span data-ttu-id="5d922-117">Bu makalede, eğitim için laboratuvarı ayarlamanız için izleyebileceğiniz ayrıntılı adımlar ve daha önce açıklanan eğitim gereksinimlerini karşılamak için kullanılabilecek çeşitli Azure DevTest Labs özellikleri hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="5d922-117">In this article, you learn about various Azure DevTest Labs features that can be used to meet the previously described training requirements and detailed steps that you can follow to set up a lab for training.</span></span>  

## <a name="implementing-training-with-azure-devtest-labs"></a><span data-ttu-id="5d922-118">Azure DevTest Labs eğitime uygulama</span><span class="sxs-lookup"><span data-stu-id="5d922-118">Implementing training with Azure DevTest Labs</span></span>
1. <span data-ttu-id="5d922-119">**Laboratuvar oluşturma**</span><span class="sxs-lookup"><span data-stu-id="5d922-119">**Create the lab**</span></span> 
   
    <span data-ttu-id="5d922-120">Labs Azure DevTest Labs başlangıç noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="5d922-120">Labs are the starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="5d922-121">Bir laboratuvar oluşturduktan sonra görevleri gerçekleştirebilirsiniz gibi kullanıcıların (trainees) Laboratuvar için ekledikçe maliyetlerini denetlemenize, hızlı bir şekilde oluşturabilirsiniz VM görüntüleri ve daha fazlasını tanımlamak için ilkeler ayarlama.</span><span class="sxs-lookup"><span data-stu-id="5d922-121">Once you create a lab, you can perform tasks such as add users (trainees) to the lab, set policies to control costs, define VM images that can create quickly, and more.</span></span>   
   
    <span data-ttu-id="5d922-122">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="5d922-122">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="5d922-123">Görev</span><span class="sxs-lookup"><span data-stu-id="5d922-123">Task</span></span> | <span data-ttu-id="5d922-124">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="5d922-124">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="5d922-125">Azure DevTest Labs'de Laboratuvar oluşturma</span><span class="sxs-lookup"><span data-stu-id="5d922-125">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="5d922-126">Azure portalında Azure DevTest Labs'de Laboratuvar oluşturma öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5d922-126">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span></span> |
2. <span data-ttu-id="5d922-127">**Eğitim VM'ler hazır Market görüntülerini ve özel görüntüleri kullanarak dakikalar içinde oluşturma**</span><span class="sxs-lookup"><span data-stu-id="5d922-127">**Create training VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="5d922-128">Azure Marketi'nde görüntüler çok geniş bir yelpazedeki hazır görüntülerden seçer ve laboratuvara trainees için kullanılabilir duruma getirmek.</span><span class="sxs-lookup"><span data-stu-id="5d922-128">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available for the trainees in the lab.</span></span> <span data-ttu-id="5d922-129">Hazır görüntüleri gereksinimlerinizi karşılamıyorsa, Laboratuvar Azure Laboratuvar özel görüntü olarak VM kaydetme ve eğitim için gereken tüm yazılım yükleme Marketi'nden hazır bir görüntü kullanarak VM oluşturarak özel bir görüntü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5d922-129">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need for the training, and saving the VM as custom image in the lab.</span></span> 
   
    <span data-ttu-id="5d922-130">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="5d922-130">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="5d922-131">Görev</span><span class="sxs-lookup"><span data-stu-id="5d922-131">Task</span></span> | <span data-ttu-id="5d922-132">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="5d922-132">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="5d922-133">Azure Market görüntülerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5d922-133">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="5d922-134">Beyaz liste Azure Market görüntülerini öğrenin; yalnızca görüntüleri seçim için kullanılabilir hale getirme için eğitim istiyor.</span><span class="sxs-lookup"><span data-stu-id="5d922-134">Learn how you can whitelist Azure Marketplace images; making available for selection only the images you want for the training.</span></span> |
   | [<span data-ttu-id="5d922-135">Özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="5d922-135">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="5d922-136">Özel bir görüntü trainees hızlı bir şekilde özel görüntü kullanarak bir VM'i oluşturabilmeniz için eğitim gereken yazılımı yüklenerek oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5d922-136">Create a custom image by pre-installing the software you need for the training so that trainees can quickly create a VM using the custom image.</span></span> |
3. <span data-ttu-id="5d922-137">**Eğitim makineler için yeniden kullanılabilir şablonlar oluşturma**</span><span class="sxs-lookup"><span data-stu-id="5d922-137">**Create reusable templates for training machines**</span></span> 
   
    <span data-ttu-id="5d922-138">Azure DevTest Labs formülde bir VM oluşturmak için kullanılan varsayılan özellik değerleri listesidir.</span><span class="sxs-lookup"><span data-stu-id="5d922-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span></span> <span data-ttu-id="5d922-139">Görüntü, VM boyutu (CPU ve RAM birleşimi) ve bir sanal ağı seçerek laboratuvarda bir formül oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5d922-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="5d922-140">Her Yardımcısı Laboratuvar formülde görebilir ve bir VM oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="5d922-140">Each trainee can see the formula in the lab and use it to create a VM.</span></span> 
   
    <span data-ttu-id="5d922-141">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="5d922-141">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="5d922-142">Görev</span><span class="sxs-lookup"><span data-stu-id="5d922-142">Task</span></span> | <span data-ttu-id="5d922-143">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="5d922-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="5d922-144">Sanal makineleri oluşturmak için DevTest Labs formüller yönetme</span><span class="sxs-lookup"><span data-stu-id="5d922-144">Manage DevTest Labs formulas to create VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="5d922-145">Görüntü, VM boyutu (CPU ve RAM birleşimi) ve bir sanal ağ seçerek bir formül nasıl oluşturabileceğinizi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5d922-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span> |
4. <span data-ttu-id="5d922-146">**Denetim maliyetleri**</span><span class="sxs-lookup"><span data-stu-id="5d922-146">**Control costs**</span></span>
   
    <span data-ttu-id="5d922-147">Azure DevTest Labs laboratuvara Yardımcısı tarafından oluşturulan VM'ler en büyük sayısını belirtmek için laboratuvarda bir ilke ayarlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="5d922-147">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a trainee in the lab.</span></span> 
   
    <span data-ttu-id="5d922-148">Birden çok gün eğitim gerçekleştirme ve tüm sanal makineleri günün belirli bir zamanda durdurun ve ardından bunları sonraki gün otomatik olarak yeniden istiyorsanız kolayca otomatik kapatma ayarlayarak bunu yapmaya ve otomatik başlatma Laboratuvar ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="5d922-148">If you are conducting multi-day training and want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span></span> 
   
    <span data-ttu-id="5d922-149">Eğitim tamamlandığında, son olarak, tüm sanal makineleri aynı anda tek bir PowerShell Betiği çalıştırarak silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5d922-149">Finally, when training is complete you can delete all the VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="5d922-150">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="5d922-150">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="5d922-151">Görev</span><span class="sxs-lookup"><span data-stu-id="5d922-151">Task</span></span> | <span data-ttu-id="5d922-152">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="5d922-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="5d922-153">Laboratuvar ilkelerini tanımlama</span><span class="sxs-lookup"><span data-stu-id="5d922-153">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="5d922-154">Laboratuar ortamında ilkeleri ayarlayarak maliyetleri denetler.</span><span class="sxs-lookup"><span data-stu-id="5d922-154">Control costs by setting policies in the lab.</span></span> |
   | [<span data-ttu-id="5d922-155">Tüm Laboratuvar bir PowerShell komut dosyası kullanarak sanal makineleri silin</span><span class="sxs-lookup"><span data-stu-id="5d922-155">Delete all the lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="5d922-156">Eğitim tamamlandığında, tek bir işlemde tüm labs silin.</span><span class="sxs-lookup"><span data-stu-id="5d922-156">Delete all the labs in one operation when the training is complete.</span></span> |
5. <span data-ttu-id="5d922-157">**Laboratuvar her Yardımcısı ile paylaşma**</span><span class="sxs-lookup"><span data-stu-id="5d922-157">**Share the lab with each trainee**</span></span>
   
    <span data-ttu-id="5d922-158">Labs, trainees ile paylaştığınız bir bağlantıyı kullanarak doğrudan erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="5d922-158">Labs can be directly accessed using a link that you share with your trainees.</span></span> <span data-ttu-id="5d922-159">Sahip oldukları sürece, trainees bile bir Azure hesabınızın olması gerekmez bir [Microsoft hesabı](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="5d922-159">Your trainees don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="5d922-160">Trainees diğer trainees tarafından oluşturulan VM'ler göremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="5d922-160">Trainees cannot see VMs created by other trainees.</span></span>  
   
    <span data-ttu-id="5d922-161">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="5d922-161">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="5d922-162">Görev</span><span class="sxs-lookup"><span data-stu-id="5d922-162">Task</span></span> | <span data-ttu-id="5d922-163">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="5d922-163">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="5d922-164">Azure DevTest Labs laboratuarda bir Yardımcısı ekleyin</span><span class="sxs-lookup"><span data-stu-id="5d922-164">Add a trainee to a lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="5d922-165">Eğitim Laboratuvarınızı trainees eklemek için Azure Portalı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="5d922-165">Use the Azure portal to add trainees to your training lab.</span></span> |
   | [<span data-ttu-id="5d922-166">Bir PowerShell Betiği kullanılarak Laboratuvar trainees Ekle</span><span class="sxs-lookup"><span data-stu-id="5d922-166">Add trainees to the lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="5d922-167">Eğitim laboratuvarınız için ekleme trainees otomatikleştirmek için PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="5d922-167">Use PowerShell to automate adding trainees to your training lab.</span></span> |
   | [<span data-ttu-id="5d922-168">Laboratuvar bağlantısını Al</span><span class="sxs-lookup"><span data-stu-id="5d922-168">Get a link to the lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="5d922-169">Nasıl bir laboratuvar doğrudan bir köprü erişilebilen öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5d922-169">Learn how a lab can be directly accessed via a hyperlink.</span></span> |
6. <span data-ttu-id="5d922-170">**Laboratuvar yeniden yeniden**</span><span class="sxs-lookup"><span data-stu-id="5d922-170">**Reuse the lab again and again**</span></span> 
   
    <span data-ttu-id="5d922-171">Laboratuvar oluşturma, özel ayarlar bir Resource Manager şablonu oluşturma ve aynı labs yeniden oluşturmak için kullanma dahil olmak üzere otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5d922-171">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span></span> 
   
    <span data-ttu-id="5d922-172">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="5d922-172">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="5d922-173">Görev</span><span class="sxs-lookup"><span data-stu-id="5d922-173">Task</span></span> | <span data-ttu-id="5d922-174">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="5d922-174">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="5d922-175">Resource Manager şablonu kullanarak bir laboratuvar oluşturma</span><span class="sxs-lookup"><span data-stu-id="5d922-175">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="5d922-176">Labs Resource Manager şablonları kullanarak Azure DevTest Labs içinde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5d922-176">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

