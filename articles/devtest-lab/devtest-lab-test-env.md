---
title: "VM ve PaaS ortamlarında test için Azure DevTest Labs kullanın | Microsoft Docs"
description: "Azure DevTest Labs VM ve PaaS test ortamı senaryoları için kullanmayı öğrenin."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: d4e2c334-643a-40c9-9051-625b8f39fc86
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tarcher
ms.openlocfilehash: a556cee9d7b665cd7df23c97e7e2c8c2afabbe58
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a><span data-ttu-id="dd8c4-103">Sınama ortamlarında kullanım Azure DevTest Labs VM ve PaaS</span><span class="sxs-lookup"><span data-stu-id="dd8c4-103">Use Azure DevTest Labs for VM and PaaS test environments</span></span>

<span data-ttu-id="dd8c4-104">Birçok temel senaryolar uygulamak için Azure DevTest Labs kullanabilirsiniz, ancak birincil senaryo Sınayıcılar için ana makineler için DevTest Labs kullanmakla ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-104">You can use Azure DevTest Labs to implement many key scenarios, but a primary scenario involves using DevTest Labs to host machines for testers.</span></span> 

<span data-ttu-id="dd8c4-105">Bu senaryoda, DevTest Labs şu avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="dd8c4-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="dd8c4-106">Sınayıcılar hızlı bir şekilde yeniden kullanılabilir şablonlar ve yapıları kullanarak Windows ve Linux ortamlar sağlama tarafından kendi uygulamasının en son sürümünü test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-106">Testers can test the latest version of their application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span>
- <span data-ttu-id="dd8c4-107">Sınayıcılar kendi yükleme birden çok test aracılarını sağlama tarafından testi yukarı ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-107">Testers can scale up their load testing by provisioning multiple test agents.</span></span>
- <span data-ttu-id="dd8c4-108">Yöneticiler, sağlayarak maliyetleri denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="dd8c4-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="dd8c4-109">Sınayıcılar ihtiyaç duydukları olandan daha fazla VMs alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-109">Testers cannot get more VMs than they need.</span></span>
  - <span data-ttu-id="dd8c4-110">Sanal makineleri ne zaman kullanılmıyor kapatılır.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-110">VMs are shut down when not in use.</span></span>

![DevTest Labs için eğitim kullanın](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="dd8c4-112">Bu makalede, tester gereksinimleri ve bir laboratuvarı ayarlamanız için ayrıntılı adımlar izlemek için karşılamak üzere kullanılan çeşitli Azure DevTest Labs özellikler hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-112">In this article, you learn about various Azure DevTest Labs features used to meet tester requirements and the detailed steps to follow to set up a lab.</span></span>

## <a name="implementing-test-environments-with-azure-devtest-labs"></a><span data-ttu-id="dd8c4-113">Azure DevTest Labs içeren test ortamlarında uygulama</span><span class="sxs-lookup"><span data-stu-id="dd8c4-113">Implementing test environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="dd8c4-114">**Laboratuvar oluşturma**</span><span class="sxs-lookup"><span data-stu-id="dd8c4-114">**Create the lab**</span></span> 
   
    <span data-ttu-id="dd8c4-115">Labs Azure DevTest Labs başlangıç noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-115">Labs are the starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="dd8c4-116">Bir laboratuvar oluşturduktan sonra hızlı bir şekilde, oluşturabilirsiniz VM görüntülerini tanımlama maliyetleri ve daha fazlasını denetlemek için ilkeler ayarlama Laboratuvar için kullanıcı (sınayıcılar) ekleme gibi görevleri gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-116">Once you create a lab, you can perform tasks such as adding users (testers) to the lab, setting policies to control costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="dd8c4-117">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="dd8c4-117">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="dd8c4-118">Görev</span><span class="sxs-lookup"><span data-stu-id="dd8c4-118">Task</span></span> | <span data-ttu-id="dd8c4-119">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="dd8c4-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="dd8c4-120">Azure DevTest Labs'de Laboratuvar oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd8c4-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="dd8c4-121">Azure portalında Azure DevTest Labs'de Laboratuvar oluşturma öğrenin.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-121">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span></span> |
2. <span data-ttu-id="dd8c4-122">**Sanal makineleri hazır Market görüntülerini ve özel görüntüleri kullanarak dakikalar içinde oluşturma**</span><span class="sxs-lookup"><span data-stu-id="dd8c4-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="dd8c4-123">Azure Marketi'nde görüntüler çok geniş bir yelpazedeki hazır görüntülerden seçer ve laboratuvara kullanılabilmesini.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-123">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available in the lab.</span></span> <span data-ttu-id="dd8c4-124">Hazır görüntüleri gereksinimlerinizi karşılamıyorsa, Laboratuvar hazır resim Laboratuvar özel görüntü olarak Azure marketi, ihtiyacınız olan tüm yazılım yükleme ve kaydetme VM kullanarak VM oluşturarak özel bir görüntü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-124">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need, and saving the VM as a custom image in the lab.</span></span>

    <span data-ttu-id="dd8c4-125">Özel resimler kullanacaksa, oluşturmak ve görüntüleri dağıtmak için bir resim Fabrika kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-125">If you will be using custom images, consider using an image factory to create and distribute your images.</span></span> <span data-ttu-id="dd8c4-126">Bir görüntü Fabrika düzenli olarak oluşturur ve yapılandırılmış görüntülerinizin otomatik olarak dağıtan bir yapılandırma olarak kodu çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="dd8c4-127">Bu, temel işletim sistemiyle bir VM oluşturulduktan sonra sistem el ile yapılandırmak için gereken süreyi kaydeder.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-127">This saves the time required to manually configure the system after a VM has been created with the base OS.</span></span>
  
    <span data-ttu-id="dd8c4-128">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="dd8c4-128">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="dd8c4-129">Görev</span><span class="sxs-lookup"><span data-stu-id="dd8c4-129">Task</span></span> | <span data-ttu-id="dd8c4-130">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="dd8c4-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="dd8c4-131">Azure Market görüntülerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="dd8c4-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="dd8c4-132">Beyaz liste Azure Market görüntülerini, yalnızca Sınayıcılar için istediğiniz görüntüleri seçim için kullanılabilir hale getirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-132">Learn how you can whitelist Azure Marketplace images, making available for selection only the images you want for the testers.</span></span>|
   | [<span data-ttu-id="dd8c4-133">Özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="dd8c4-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="dd8c4-134">Sınayıcılar hızla özel görüntü kullanarak bir VM oluşturmak için ihtiyacınız olan yazılım yüklenerek özel bir görüntü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-134">Create a custom image by pre-installing the software you need so that testers can quickly create a VM using the custom image.</span></span>|
   | [<span data-ttu-id="dd8c4-135">Görüntü Fabrika hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="dd8c4-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="dd8c4-136">Bir görüntü Fabrika ayarlamak ve nasıl kullanılacağını açıklayan bir videoyu izleyin.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-136">Watch a video that describes how to set up and use an image factory.</span></span>|

3. <span data-ttu-id="dd8c4-137">**Test makinelerini için yeniden kullanılabilir şablonlar oluşturma**</span><span class="sxs-lookup"><span data-stu-id="dd8c4-137">**Create reusable templates for test machines**</span></span> 
   
    <span data-ttu-id="dd8c4-138">Azure DevTest Labs formülde bir VM oluşturmak için kullanılan varsayılan özellik değerleri listesidir.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span></span> <span data-ttu-id="dd8c4-139">Görüntü, VM boyutu (CPU ve RAM birleşimi) ve bir sanal ağı seçerek laboratuvarda bir formül oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="dd8c4-140">Her tester Laboratuvar formülde görebilir ve bir VM oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-140">Each tester can see the formula in the lab and use it to create a VM.</span></span> 
   
    <span data-ttu-id="dd8c4-141">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="dd8c4-141">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="dd8c4-142">Görev</span><span class="sxs-lookup"><span data-stu-id="dd8c4-142">Task</span></span> | <span data-ttu-id="dd8c4-143">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="dd8c4-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="dd8c4-144">Sanal makineleri oluşturmak için DevTest Labs formüller yönetme</span><span class="sxs-lookup"><span data-stu-id="dd8c4-144">Manage DevTest Labs formulas to create VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="dd8c4-145">Görüntü, VM boyutu (CPU ve RAM birleşimi) ve bir sanal ağ seçerek bir formül nasıl oluşturabileceğinizi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

3. <span data-ttu-id="dd8c4-146">**Çoklu VM test ortamları oluşturma**</span><span class="sxs-lookup"><span data-stu-id="dd8c4-146">**Create multi-VM test environments**</span></span> 
   
    <span data-ttu-id="dd8c4-147">Azure Resource Manager şablonları altyapısı ve Azure çözümünüzü yapılandırmasını tanımlayın ve art arda birden çok test tutarlı bir durumda sanal makineleri dağıtmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-147">You can use Azure Resource Manager templates to define the infrastructure and configuration of your Azure solution and repeatedly deploy multiple test VMs in a consistent state.</span></span>

    <span data-ttu-id="dd8c4-148">Azure PaaS kaynaklarına bir ortamda bir Resource Manager şablonunda sağlanabilir ve maliyet izlemesi görünür.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-148">Azure PaaS resources can be provisioned in an environment from a Resource Manager template and appear in cost tracking.</span></span> <span data-ttu-id="dd8c4-149">Ancak, VM otomatik kapatma PaaS kaynaklarına geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-149">However, VM auto shutdown does not apply to PaaS resources.</span></span>

    <span data-ttu-id="dd8c4-150">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="dd8c4-150">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="dd8c4-151">Görev</span><span class="sxs-lookup"><span data-stu-id="dd8c4-151">Task</span></span> | <span data-ttu-id="dd8c4-152">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="dd8c4-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="dd8c4-153">Azure Resource Manager şablonları ile çoklu VM ortamları ve PaaS kaynakları oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd8c4-153">Create multi-VM environments and PaaS resources with Azure Resource Manager templates</span></span>](devtest-lab-create-environment-from-arm.md) |<span data-ttu-id="dd8c4-154">Tutarlı bir durumda birden çok VM test ortamınızı nasıl dağıtabileceğiniz hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-154">Learn how you can deploy multiple VMs in a consistent state for your test environment.</span></span>|

4. <span data-ttu-id="dd8c4-155">**Esnek VM özelleştirmeyi etkinleştirmek için yapıları oluşturma**</span><span class="sxs-lookup"><span data-stu-id="dd8c4-155">**Create artifacts to enable flexible VM customization**</span></span>

   <span data-ttu-id="dd8c4-156">Yapılar, dağıtmak ve bir VM sağlandıktan sonra Uygulamanızı yapılandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-156">Artifacts are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="dd8c4-157">Yapıtlar şunlar olabilir:</span><span class="sxs-lookup"><span data-stu-id="dd8c4-157">Artifacts can be:</span></span>

   - <span data-ttu-id="dd8c4-158">Aracılar, Fiddler ve Visual Studio gibi VM - yüklemek istediğiniz araçları.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-158">Tools that you want to install on the VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="dd8c4-159">Bir depoyu kopyalama gibi VM üzerinde-çalıştırmak istediğiniz eylemleri.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-159">Actions that you want to run on the VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="dd8c4-160">Test etmek istediğiniz uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-160">Applications that you want to test.</span></span>

   <span data-ttu-id="dd8c4-161">Birçok zaten kullanılabilir out-of--box ürünleridir.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-161">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="dd8c4-162">Ancak, özel gereksinimlerinizi karşılamak için daha fazla özelleştirme istiyorsanız, özel yapıtları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-162">But if you want more customization for your specific needs, you can create your own custom artifacts.</span></span>

   <span data-ttu-id="dd8c4-163">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="dd8c4-163">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="dd8c4-164">Görev</span><span class="sxs-lookup"><span data-stu-id="dd8c4-164">Task</span></span> | <span data-ttu-id="dd8c4-165">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="dd8c4-165">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="dd8c4-166">DevTest Labs VM için özel yapılar oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd8c4-166">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="dd8c4-167">Sanal makineler için kendi özel yapılar laboratuvarınızda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-167">Create your own custom artifacts for the virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="dd8c4-168">Özel yapılar ve kullanmak için Azure Resource Manager şablonları Azure DevTest Labs'de depolamak için bir Git deposu ekleme</span><span class="sxs-lookup"><span data-stu-id="dd8c4-168">Add a Git repository to store custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="dd8c4-169">Özel yapıtları kendi özel Git deposuna depolamayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-169">Learn how to store your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="dd8c4-170">**Denetim maliyetleri**</span><span class="sxs-lookup"><span data-stu-id="dd8c4-170">**Control costs**</span></span>
   
    <span data-ttu-id="dd8c4-171">Azure DevTest Labs laboratuvarda bir test laboratuvarında tarafından oluşturulan VM'ler en büyük sayısını belirtmek için bir ilke ayarlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-171">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a tester in the lab.</span></span> 
   
    <span data-ttu-id="dd8c4-172">Çalışma kümesi test ekibiniz varsa, zamanlama ve günün belirli bir zamanda tüm sanal makineleri durdurmak ve ardından bunları sonraki gün otomatik olarak yeniden istiyorsanız, laboratuar ortamında otomatik kapatma ve otomatik başlatma ilkeleri ayarlayarak, kolayca gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-172">If your test team has a set work schedule and you want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span></span> 
   
    <span data-ttu-id="dd8c4-173">Uygulama geliştirme tamamlandığında, son olarak, tüm sanal makineleri aynı anda tek bir PowerShell Betiği çalıştırarak silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-173">Finally, when app development is complete, you can delete all the VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="dd8c4-174">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="dd8c4-174">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="dd8c4-175">Görev</span><span class="sxs-lookup"><span data-stu-id="dd8c4-175">Task</span></span> | <span data-ttu-id="dd8c4-176">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="dd8c4-176">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="dd8c4-177">Laboratuvar ilkelerini tanımlama</span><span class="sxs-lookup"><span data-stu-id="dd8c4-177">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="dd8c4-178">Laboratuar ortamında ilkeleri ayarlayarak maliyetleri denetler.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-178">Control costs by setting policies in the lab.</span></span> |
   | [<span data-ttu-id="dd8c4-179">Tüm Laboratuvar bir PowerShell komut dosyası kullanarak sanal makineleri silin</span><span class="sxs-lookup"><span data-stu-id="dd8c4-179">Delete all the lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="dd8c4-180">Test tamamlandığında tek bir işlemde tüm labs silin.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-180">Delete all the labs in one operation when testing is complete.</span></span>|

1. <span data-ttu-id="dd8c4-181">**Sanal ağ için bir laboratuvar ekleme**</span><span class="sxs-lookup"><span data-stu-id="dd8c4-181">**Add a virtual network to a Lab**</span></span> 
   
    <span data-ttu-id="dd8c4-182">Her bir laboratuvar oluşturulduğunda DevTest Labs yeni bir sanal ağ (VNET) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-182">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="dd8c4-183">Kendi VNET-Örneğin, ExpressRoute veya siteden siteye VPN kullanarak – yapılandırdıysanız, sanal makineleri oluşturulurken kullanılabilir olmasını sağlamak için Laboratuvarınızı ait sanal ağ ayarları bu VNET ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-183">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET to your lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="dd8c4-184">Ayrıca, VM oluşturulduğunda, bir VM için bir etki alanına katılan bir Azure Active Directory etki alanı katılma yapıya kullanılabilir yoktur.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-184">In addition, there is an Azure Active Directory domain join artifact available that joins a VM to a domain when the VM is being created.</span></span> 
   
    <span data-ttu-id="dd8c4-185">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="dd8c4-185">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="dd8c4-186">Görev</span><span class="sxs-lookup"><span data-stu-id="dd8c4-186">Task</span></span> | <span data-ttu-id="dd8c4-187">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="dd8c4-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="dd8c4-188">Azure DevTest Labs'de sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="dd8c4-188">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="dd8c4-189">Azure portalını kullanarak Azure DevTest Labs içinde bir sanal ağ yapılandırma konusunda bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-189">Learn how to configure a virtual network in Azure DevTest Labs using the Azure portal.</span></span>|

6. <span data-ttu-id="dd8c4-190">**Laboratuvar her tester ile paylaşma**</span><span class="sxs-lookup"><span data-stu-id="dd8c4-190">**Share the lab with each tester**</span></span>
   
    <span data-ttu-id="dd8c4-191">Labs, denetleyicilerle paylaşmanızı bir bağlantıyı kullanarak doğrudan erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-191">Labs can be directly accessed using a link that you share with your testers.</span></span> <span data-ttu-id="dd8c4-192">Sahip oldukları sürece bile bir Azure hesabına sahip sahip olmayan bir [Microsoft hesabı](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="dd8c4-192">They don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="dd8c4-193">Sınayıcılar diğer test eden tarafından oluşturulan VM'ler göremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-193">Testers cannot see VMs created by other testers.</span></span>  
   
    <span data-ttu-id="dd8c4-194">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="dd8c4-194">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="dd8c4-195">Görev</span><span class="sxs-lookup"><span data-stu-id="dd8c4-195">Task</span></span> | <span data-ttu-id="dd8c4-196">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="dd8c4-196">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="dd8c4-197">Azure DevTest Labs laboratuarda bir tester ekleyin</span><span class="sxs-lookup"><span data-stu-id="dd8c4-197">Add a tester to a lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="dd8c4-198">Sınayıcılar için Laboratuvarınızı eklemek için Azure Portalı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-198">Use the Azure portal to add testers to your lab.</span></span>|
   | [<span data-ttu-id="dd8c4-199">Sınayıcılar bir PowerShell Betiği kullanılarak laboratuvara ekleme</span><span class="sxs-lookup"><span data-stu-id="dd8c4-199">Add testers to the lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="dd8c4-200">Laboratuvarınızı ekleme edenlere otomatikleştirmek için PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-200">Use PowerShell to automate adding testers to your lab.</span></span> |
   | [<span data-ttu-id="dd8c4-201">Laboratuvar bağlantısını Al</span><span class="sxs-lookup"><span data-stu-id="dd8c4-201">Get a link to the lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="dd8c4-202">Nasıl sınayıcılar Laboratuvar köprü üzerinden doğrudan erişebileceğiniz öğrenin.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-202">Learn how testers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="dd8c4-203">**Daha fazla takımlar için laboratuvar oluşturmayı otomatikleştirmek**</span><span class="sxs-lookup"><span data-stu-id="dd8c4-203">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="dd8c4-204">Laboratuvar oluşturma, özel ayarlar bir Resource Manager şablonu oluşturma ve aynı labs yeniden oluşturmak için kullanma dahil olmak üzere otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-204">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span></span> 
   
    <span data-ttu-id="dd8c4-205">Aşağıdaki tabloda bağlantıları tıklayarak edinin:</span><span class="sxs-lookup"><span data-stu-id="dd8c4-205">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="dd8c4-206">Görev</span><span class="sxs-lookup"><span data-stu-id="dd8c4-206">Task</span></span> | <span data-ttu-id="dd8c4-207">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="dd8c4-207">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="dd8c4-208">Resource Manager şablonu kullanarak bir laboratuvar oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd8c4-208">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="dd8c4-209">Labs Resource Manager şablonları kullanarak Azure DevTest Labs içinde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd8c4-209">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

