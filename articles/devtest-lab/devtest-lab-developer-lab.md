---
title: "Geliştiriciler için Azure DevTest Labs kullanın | Microsoft Docs"
description: "Azure DevTest Labs Geliştirici senaryoları için kullanmayı öğrenin."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 22e070e5-3d1a-49fe-9d4c-5e07cb0b7fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: tarcher
ms.openlocfilehash: c187819e9392908c8979556f80e8c94739eb14d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-devtest-labs-for-developers"></a><span data-ttu-id="fbabc-103">Geliştiriciler için Azure DevTest Labs kullanın</span><span class="sxs-lookup"><span data-stu-id="fbabc-103">Use Azure DevTest Labs for developers</span></span>
<span data-ttu-id="fbabc-104">Azure DevTest Labs pek çok temel senaryolar uygulamak için kullanılabilir, ancak birincil senaryolardan biri, geliştiriciler için geliştirme makineleri barındıracak şekilde DevTest Labs kullanarak içerir.</span><span class="sxs-lookup"><span data-stu-id="fbabc-104">Azure DevTest Labs can be used to implement many key scenarios, but one of the primary scenarios involves using DevTest Labs to host development machines for developers.</span></span> <span data-ttu-id="fbabc-105">Bu senaryoda, DevTest Labs şu avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="fbabc-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="fbabc-106">Geliştiriciler, geliştirme makinelerinin isteğe bağlı olarak hızlı bir şekilde sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbabc-106">Developers can quickly provision their development machines on demand.</span></span>
- <span data-ttu-id="fbabc-107">Geliştiriciler, geliştirme makinelerinin gerektiğinde kolayca özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbabc-107">Developers can easily customize their development machines whenever needed.</span></span>
- <span data-ttu-id="fbabc-108">Yöneticiler, sağlayarak maliyetleri denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fbabc-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="fbabc-109">Geliştiriciler, geliştirme için gerekenden daha fazla VMs alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="fbabc-109">Developers cannot get more VMs than they need for development.</span></span>
  - <span data-ttu-id="fbabc-110">Sanal makineleri ne zaman kullanılmıyor kapatılır.</span><span class="sxs-lookup"><span data-stu-id="fbabc-110">VMs are shut down when not in use.</span></span> 

![DevTest Labs için eğitim kullanın](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="fbabc-112">Bu makalede, geliştirici gereksinimlerini karşılamak için kullanılabilecek çeşitli Azure DevTest Labs özellikleri ve bir laboratuvarı ayarlamanız için izleyebileceğiniz ayrıntılı adımlar hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="fbabc-112">In this article, you learn about various Azure DevTest Labs features that can be used to meet developer requirements and the detailed steps that you can follow to set up a lab.</span></span>

## <a name="implementing-developer-environments-with-azure-devtest-labs"></a><span data-ttu-id="fbabc-113">Azure DevTest Labs Geliştirici ortamlarıyla uygulama</span><span class="sxs-lookup"><span data-stu-id="fbabc-113">Implementing developer environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="fbabc-114">**Laboratuvar oluşturma**</span><span class="sxs-lookup"><span data-stu-id="fbabc-114">**Create the lab**</span></span> 
   
    <span data-ttu-id="fbabc-115">Labs Azure DevTest Labs başlangıç noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="fbabc-115">Labs are the starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="fbabc-116">Bir laboratuvar oluşturduktan sonra hızlı bir şekilde, oluşturabilirsiniz VM görüntülerini tanımlama maliyetleri ve daha fazlasını denetlemek için ilkeler ayarlama Laboratuvar için kullanıcı (geliştiriciler) ekleme gibi görevleri gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="fbabc-116">Once you create a lab, you can perform tasks such as adding users (developers) to the lab, setting policies to control costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="fbabc-117">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="fbabc-117">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="fbabc-118">Görev</span><span class="sxs-lookup"><span data-stu-id="fbabc-118">Task</span></span> | <span data-ttu-id="fbabc-119">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="fbabc-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="fbabc-120">Azure DevTest Labs'de Laboratuvar oluşturma</span><span class="sxs-lookup"><span data-stu-id="fbabc-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="fbabc-121">Azure portalında Azure DevTest Labs'de Laboratuvar oluşturma öğrenin.</span><span class="sxs-lookup"><span data-stu-id="fbabc-121">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span></span> |
2. <span data-ttu-id="fbabc-122">**Sanal makineleri hazır Market görüntülerini ve özel görüntüleri kullanarak dakikalar içinde oluşturma**</span><span class="sxs-lookup"><span data-stu-id="fbabc-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="fbabc-123">Azure Marketi'nde görüntüler çok geniş bir yelpazedeki hazır görüntülerden seçer ve laboratuvara kullanılabilmesini.</span><span class="sxs-lookup"><span data-stu-id="fbabc-123">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available in the lab.</span></span> <span data-ttu-id="fbabc-124">Hazır görüntüleri gereksinimlerinizi karşılamıyorsa, Laboratuvar hazır resim Laboratuvar özel görüntü olarak Azure marketi, ihtiyacınız olan tüm yazılım yükleme ve kaydetme VM kullanarak VM oluşturarak özel bir görüntü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbabc-124">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need, and saving the VM as a custom image in the lab.</span></span>

    <span data-ttu-id="fbabc-125">Özel resimler kullanacaksa, oluşturmak ve görüntüleri dağıtmak için bir resim Fabrika kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="fbabc-125">If you will be using custom images, consider using an image factory to create and distribute your images.</span></span> <span data-ttu-id="fbabc-126">Bir görüntü Fabrika düzenli olarak oluşturur ve yapılandırılmış görüntülerinizin otomatik olarak dağıtan bir yapılandırma olarak kodu çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="fbabc-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="fbabc-127">Bu, temel işletim sistemiyle bir VM oluşturulduktan sonra sistem el ile yapılandırmak için gereken süreyi kaydeder.</span><span class="sxs-lookup"><span data-stu-id="fbabc-127">This saves the time required to manually configure the system after a VM has been created with the base OS.</span></span>
  
    <span data-ttu-id="fbabc-128">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="fbabc-128">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="fbabc-129">Görev</span><span class="sxs-lookup"><span data-stu-id="fbabc-129">Task</span></span> | <span data-ttu-id="fbabc-130">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="fbabc-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="fbabc-131">Azure Market görüntülerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="fbabc-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="fbabc-132">Beyaz liste Azure Market görüntülerini, yalnızca geliştiriciler için istediğiniz görüntüleri seçim için kullanılabilir hale getirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="fbabc-132">Learn how you can whitelist Azure Marketplace images, making available for selection only the images you want for the developers.</span></span>|
   | [<span data-ttu-id="fbabc-133">Özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="fbabc-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="fbabc-134">Böylece geliştiriciler, hızlı bir şekilde özel görüntü kullanarak bir VM oluşturabilir, gereken yazılımı yüklenerek özel bir görüntü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fbabc-134">Create a custom image by pre-installing the software you need so that developers can quickly create a VM using the custom image.</span></span>|
   | [<span data-ttu-id="fbabc-135">Görüntü Fabrika hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="fbabc-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="fbabc-136">Bir görüntü Fabrika ayarlamak ve nasıl kullanılacağını açıklayan bir videoyu izleyin.</span><span class="sxs-lookup"><span data-stu-id="fbabc-136">Watch a video that describes how to set up and use an image factory.</span></span>|

3. <span data-ttu-id="fbabc-137">**Geliştirici makinelerinde için yeniden kullanılabilir şablonlar oluşturma**</span><span class="sxs-lookup"><span data-stu-id="fbabc-137">**Create reusable templates for developer machines**</span></span> 
   
    <span data-ttu-id="fbabc-138">Azure DevTest Labs formülde bir VM oluşturmak için kullanılan varsayılan özellik değerleri listesidir.</span><span class="sxs-lookup"><span data-stu-id="fbabc-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span></span> <span data-ttu-id="fbabc-139">Görüntü, VM boyutu (CPU ve RAM birleşimi) ve bir sanal ağı seçerek laboratuvarda bir formül oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbabc-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="fbabc-140">Her geliştirici Laboratuvar formülde görebilir ve bir VM oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="fbabc-140">Each developer can see the formula in the lab and use it to create a VM.</span></span> 
   
    <span data-ttu-id="fbabc-141">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="fbabc-141">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="fbabc-142">Görev</span><span class="sxs-lookup"><span data-stu-id="fbabc-142">Task</span></span> | <span data-ttu-id="fbabc-143">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="fbabc-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="fbabc-144">Sanal makineleri oluşturmak için DevTest Labs formüller yönetme</span><span class="sxs-lookup"><span data-stu-id="fbabc-144">Manage DevTest Labs formulas to create VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="fbabc-145">Görüntü, VM boyutu (CPU ve RAM birleşimi) ve bir sanal ağ seçerek bir formül nasıl oluşturabileceğinizi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="fbabc-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

4. <span data-ttu-id="fbabc-146">**Esnek VM özelleştirmeyi etkinleştirmek için yapıları oluşturma**</span><span class="sxs-lookup"><span data-stu-id="fbabc-146">**Create artifacts to enable flexible VM customization**</span></span>

   <span data-ttu-id="fbabc-147">Yapılar, dağıtmak ve bir VM sağlandıktan sonra Uygulamanızı yapılandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fbabc-147">Artifacts are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="fbabc-148">Yapıtlar şunlar olabilir:</span><span class="sxs-lookup"><span data-stu-id="fbabc-148">Artifacts can be:</span></span>

   - <span data-ttu-id="fbabc-149">Aracılar, Fiddler ve Visual Studio gibi VM - yüklemek istediğiniz araçları.</span><span class="sxs-lookup"><span data-stu-id="fbabc-149">Tools that you want to install on the VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="fbabc-150">Bir depoyu kopyalama gibi VM üzerinde-çalıştırmak istediğiniz eylemleri.</span><span class="sxs-lookup"><span data-stu-id="fbabc-150">Actions that you want to run on the VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="fbabc-151">Test etmek istediğiniz uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="fbabc-151">Applications that you want to test.</span></span>

   <span data-ttu-id="fbabc-152">Birçok zaten kullanılabilir out-of--box ürünleridir.</span><span class="sxs-lookup"><span data-stu-id="fbabc-152">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="fbabc-153">Özel ihtiyaçlarınız için daha fazla özelleştirme isterseniz kendi özel yapılar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbabc-153">You can create your own custom artifacts if you want more customization for your specific needs.</span></span>

   <span data-ttu-id="fbabc-154">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="fbabc-154">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="fbabc-155">Görev</span><span class="sxs-lookup"><span data-stu-id="fbabc-155">Task</span></span> | <span data-ttu-id="fbabc-156">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="fbabc-156">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="fbabc-157">DevTest Labs VM için özel yapılar oluşturma</span><span class="sxs-lookup"><span data-stu-id="fbabc-157">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="fbabc-158">Sanal makineler için kendi özel yapılar laboratuvarınızda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fbabc-158">Create your own custom artifacts for the virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="fbabc-159">Özel yapılar ve kullanmak için Azure Resource Manager şablonları Azure DevTest Labs'de depolamak için bir Git deposu ekleme</span><span class="sxs-lookup"><span data-stu-id="fbabc-159">Add a Git repository to store custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="fbabc-160">Özel yapıtları kendi özel Git deposuna depolamayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="fbabc-160">Learn how to store your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="fbabc-161">**Denetim maliyetleri**</span><span class="sxs-lookup"><span data-stu-id="fbabc-161">**Control costs**</span></span>
   
    <span data-ttu-id="fbabc-162">Azure DevTest Labs laboratuvarda bir geliştirici tarafından oluşturulan VM'ler en büyük sayısını belirtmek için laboratuvarda bir ilke ayarlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="fbabc-162">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a developer in the lab.</span></span> 
   
    <span data-ttu-id="fbabc-163">Çalışma kümesi, geliştirici ekibiniz varsa, zamanlama ve günün belirli bir zamanda tüm sanal makineleri durdurmak ve ardından bunları sonraki gün otomatik olarak yeniden istiyorsanız, laboratuar ortamında otomatik kapatma ve otomatik başlatma ilkeleri ayarlayarak, kolayca gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbabc-163">If your developer team has a set work schedule and you want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span></span> 
   
    <span data-ttu-id="fbabc-164">Uygulama geliştirme tamamlandığında, son olarak, tüm sanal makineleri aynı anda tek bir PowerShell Betiği çalıştırarak silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbabc-164">Finally, when app development is complete, you can delete all the VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="fbabc-165">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="fbabc-165">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="fbabc-166">Görev</span><span class="sxs-lookup"><span data-stu-id="fbabc-166">Task</span></span> | <span data-ttu-id="fbabc-167">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="fbabc-167">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="fbabc-168">Laboratuvar ilkelerini tanımlama</span><span class="sxs-lookup"><span data-stu-id="fbabc-168">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="fbabc-169">Laboratuar ortamında ilkeleri ayarlayarak maliyetleri denetler.</span><span class="sxs-lookup"><span data-stu-id="fbabc-169">Control costs by setting policies in the lab.</span></span> |
   | [<span data-ttu-id="fbabc-170">Tüm Laboratuvar bir PowerShell komut dosyası kullanarak sanal makineleri silin</span><span class="sxs-lookup"><span data-stu-id="fbabc-170">Delete all the lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="fbabc-171">Geliştirme tamamlandığında, tek bir işlemde tüm labs silin.</span><span class="sxs-lookup"><span data-stu-id="fbabc-171">Delete all the labs in one operation when development is complete.</span></span>|

1. <span data-ttu-id="fbabc-172">**Bir VM sanal ağ ekleme**</span><span class="sxs-lookup"><span data-stu-id="fbabc-172">**Add a virtual network to a VM**</span></span> 
   
    <span data-ttu-id="fbabc-173">Her bir laboratuvar oluşturulduğunda DevTest Labs yeni bir sanal ağ (VNET) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fbabc-173">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="fbabc-174">Kendi VNET-Örneğin, ExpressRoute veya siteden siteye VPN kullanarak – yapılandırdıysanız, sanal makineleri oluşturulurken kullanılabilir olmasını sağlamak için Laboratuvarınızı ait sanal ağ ayarları bu VNET ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbabc-174">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET to your lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="fbabc-175">Ayrıca, bir Azure Active Directory etki alanı katılma yapı VM oluşturulduğunda, bir VM bir etki alanına katılacak kullanılabilir yoktur.</span><span class="sxs-lookup"><span data-stu-id="fbabc-175">In addition, there is an Azure Active Directory domain join artifact available that will join a VM to a domain when the VM is being created.</span></span> 
   
    <span data-ttu-id="fbabc-176">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="fbabc-176">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="fbabc-177">Görev</span><span class="sxs-lookup"><span data-stu-id="fbabc-177">Task</span></span> | <span data-ttu-id="fbabc-178">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="fbabc-178">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="fbabc-179">Azure DevTest Labs'de sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fbabc-179">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="fbabc-180">Azure portalını kullanarak Azure DevTest Labs içinde bir sanal ağ yapılandırma konusunda bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="fbabc-180">Learn how to configure a virtual network in Azure DevTest Labs using the Azure portal.</span></span>|

6. <span data-ttu-id="fbabc-181">**Laboratuvar her developer ile paylaşma**</span><span class="sxs-lookup"><span data-stu-id="fbabc-181">**Share the lab with each developer**</span></span>
   
    <span data-ttu-id="fbabc-182">Labs, geliştiricilere paylaşan bir bağlantıyı kullanarak doğrudan erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="fbabc-182">Labs can be directly accessed using a link that you share with your developers.</span></span> <span data-ttu-id="fbabc-183">Sahip oldukları sürece bile bir Azure hesabına sahip sahip olmayan bir [Microsoft hesabı](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="fbabc-183">They don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="fbabc-184">Geliştiriciler, diğer geliştiriciler tarafından oluşturulan VM'ler göremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbabc-184">Developers cannot see VMs created by other developers.</span></span>  
   
    <span data-ttu-id="fbabc-185">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="fbabc-185">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="fbabc-186">Görev</span><span class="sxs-lookup"><span data-stu-id="fbabc-186">Task</span></span> | <span data-ttu-id="fbabc-187">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="fbabc-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="fbabc-188">Azure DevTest Labs laboratuarda bir geliştirici ekleyin</span><span class="sxs-lookup"><span data-stu-id="fbabc-188">Add a developer to a lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="fbabc-189">Geliştiriciler için Laboratuvarınızı eklemek için Azure Portalı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="fbabc-189">Use the Azure portal to add developers to your lab.</span></span>|
   | [<span data-ttu-id="fbabc-190">Geliştiriciler bir PowerShell Betiği kullanılarak laboratuvara ekleme</span><span class="sxs-lookup"><span data-stu-id="fbabc-190">Add developers to the lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="fbabc-191">Laboratuvarınızı ekleme geliştiricilerine otomatikleştirmek için PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="fbabc-191">Use PowerShell to automate adding developers to your lab.</span></span> |
   | [<span data-ttu-id="fbabc-192">Laboratuvar bağlantısını Al</span><span class="sxs-lookup"><span data-stu-id="fbabc-192">Get a link to the lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="fbabc-193">Nasıl geliştiriciler Laboratuvar köprü üzerinden doğrudan erişebileceğiniz öğrenin.</span><span class="sxs-lookup"><span data-stu-id="fbabc-193">Learn how developers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="fbabc-194">**Daha fazla takımlar için laboratuvar oluşturmayı otomatikleştirmek**</span><span class="sxs-lookup"><span data-stu-id="fbabc-194">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="fbabc-195">Laboratuvar oluşturma, özel ayarlar bir Resource Manager şablonu oluşturma ve aynı labs yeniden oluşturmak için kullanma dahil olmak üzere otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbabc-195">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span></span> 
   
    <span data-ttu-id="fbabc-196">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="fbabc-196">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="fbabc-197">Görev</span><span class="sxs-lookup"><span data-stu-id="fbabc-197">Task</span></span> | <span data-ttu-id="fbabc-198">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="fbabc-198">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="fbabc-199">Resource Manager şablonu kullanarak bir laboratuvar oluşturma</span><span class="sxs-lookup"><span data-stu-id="fbabc-199">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="fbabc-200">Labs Resource Manager şablonları kullanarak Azure DevTest Labs içinde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fbabc-200">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

