---
title: "VM ve PaaS aaaUse Azure DevTest Labs test ortamları | Microsoft Docs"
description: "Nasıl toouse Azure DevTest Labs VM ve PaaS için test ortamı senaryoları hakkında bilgi edinin."
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
ms.openlocfilehash: 9285090da768491e1275942318b094fae89e3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a><span data-ttu-id="2e43c-103">Sınama ortamlarında kullanım Azure DevTest Labs VM ve PaaS</span><span class="sxs-lookup"><span data-stu-id="2e43c-103">Use Azure DevTest Labs for VM and PaaS test environments</span></span>

<span data-ttu-id="2e43c-104">Azure DevTest Labs tooimplement birçok senaryoları kullanabilirsiniz, ancak Sınayıcılar için DevTest Labs toohost makineleri kullanarak birincil bir senaryo içerir.</span><span class="sxs-lookup"><span data-stu-id="2e43c-104">You can use Azure DevTest Labs tooimplement many key scenarios, but a primary scenario involves using DevTest Labs toohost machines for testers.</span></span> 

<span data-ttu-id="2e43c-105">Bu senaryoda, DevTest Labs şu avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="2e43c-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="2e43c-106">Sınayıcılar hızlı bir şekilde yeniden kullanılabilir şablonlar ve yapıları kullanarak Windows ve Linux ortamlar sağlama tarafından hello kendi uygulamasının en son sürümünü test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e43c-106">Testers can test hello latest version of their application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span>
- <span data-ttu-id="2e43c-107">Sınayıcılar kendi yükleme birden çok test aracılarını sağlama tarafından testi yukarı ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e43c-107">Testers can scale up their load testing by provisioning multiple test agents.</span></span>
- <span data-ttu-id="2e43c-108">Yöneticiler, sağlayarak maliyetleri denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2e43c-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="2e43c-109">Sınayıcılar ihtiyaç duydukları olandan daha fazla VMs alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="2e43c-109">Testers cannot get more VMs than they need.</span></span>
  - <span data-ttu-id="2e43c-110">Sanal makineleri ne zaman kullanılmıyor kapatılır.</span><span class="sxs-lookup"><span data-stu-id="2e43c-110">VMs are shut down when not in use.</span></span>

![DevTest Labs için eğitim kullanın](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="2e43c-112">Bu makalede, çeşitli Azure DevTest Labs kullanılan özellikler toomeet tester gereksinimleri hakkında bilgi edinin ve ayrıntılı adımlar toofollow tooset bir laboratuvar yukarı hello.</span><span class="sxs-lookup"><span data-stu-id="2e43c-112">In this article, you learn about various Azure DevTest Labs features used toomeet tester requirements and hello detailed steps toofollow tooset up a lab.</span></span>

## <a name="implementing-test-environments-with-azure-devtest-labs"></a><span data-ttu-id="2e43c-113">Azure DevTest Labs içeren test ortamlarında uygulama</span><span class="sxs-lookup"><span data-stu-id="2e43c-113">Implementing test environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="2e43c-114">**Merhaba Laboratuvar oluşturma**</span><span class="sxs-lookup"><span data-stu-id="2e43c-114">**Create hello lab**</span></span> 
   
    <span data-ttu-id="2e43c-115">Labs hello Azure DevTest Labs'de başlangıç noktası var.</span><span class="sxs-lookup"><span data-stu-id="2e43c-115">Labs are hello starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="2e43c-116">Bir laboratuvar oluşturduktan sonra kullanıcılar (sınayıcılar) toohello Laboratuvar, hızlı bir şekilde, oluşturabilirsiniz VM görüntülerini tanımlama, ayar ilkeleri toocontrol maliyetleri ve daha fazlasını ekleme gibi görevleri gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e43c-116">Once you create a lab, you can perform tasks such as adding users (testers) toohello lab, setting policies toocontrol costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="2e43c-117">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="2e43c-117">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="2e43c-118">Görev</span><span class="sxs-lookup"><span data-stu-id="2e43c-118">Task</span></span> | <span data-ttu-id="2e43c-119">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="2e43c-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="2e43c-120">Azure DevTest Labs'de Laboratuvar oluşturma</span><span class="sxs-lookup"><span data-stu-id="2e43c-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="2e43c-121">Azure DevTest Labs'de Laboratuvar bir toocreate hello Azure portalına nasıl öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2e43c-121">Learn how toocreate a lab in Azure DevTest Labs in hello Azure portal.</span></span> |
2. <span data-ttu-id="2e43c-122">**Sanal makineleri hazır Market görüntülerini ve özel görüntüleri kullanarak dakikalar içinde oluşturma**</span><span class="sxs-lookup"><span data-stu-id="2e43c-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="2e43c-123">Görüntüler çok geniş bir yelpazedeki hazır görüntülerden hello Azure Marketi seçer ve hello laboratuarda kullanılabilmesini.</span><span class="sxs-lookup"><span data-stu-id="2e43c-123">You can pick ready-made images from a wide variety of images in hello Azure Marketplace and make them available in hello lab.</span></span> <span data-ttu-id="2e43c-124">Merhaba hazır görüntüleri gereksinimlerinizi karşılamıyorsa, Laboratuvar hello Laboratuvar özel görüntü olarak Azure marketi, gereksinim duyduğunuz tüm hello yazılım yükleme ve kaydetme hello VM hazır bir görüntüden kullanarak VM oluşturarak özel bir görüntü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e43c-124">If hello ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all hello software that you need, and saving hello VM as a custom image in hello lab.</span></span>

    <span data-ttu-id="2e43c-125">Özel resimler kullanacaksanız, bir görüntü Fabrika toocreate kullanmayı düşünün ve resimlerinizi dağıtın.</span><span class="sxs-lookup"><span data-stu-id="2e43c-125">If you will be using custom images, consider using an image factory toocreate and distribute your images.</span></span> <span data-ttu-id="2e43c-126">Bir görüntü Fabrika düzenli olarak oluşturur ve yapılandırılmış görüntülerinizin otomatik olarak dağıtan bir yapılandırma olarak kodu çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="2e43c-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="2e43c-127">Bir VM ile Merhaba oluşturulduktan sonra bu kaydeder hello gereken süre toomanually yapılandırma hello sistem işletim sistemi temel.</span><span class="sxs-lookup"><span data-stu-id="2e43c-127">This saves hello time required toomanually configure hello system after a VM has been created with hello base OS.</span></span>
  
    <span data-ttu-id="2e43c-128">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="2e43c-128">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="2e43c-129">Görev</span><span class="sxs-lookup"><span data-stu-id="2e43c-129">Task</span></span> | <span data-ttu-id="2e43c-130">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="2e43c-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="2e43c-131">Azure Market görüntülerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="2e43c-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="2e43c-132">Beyaz liste Azure Market görüntülerini hello Sınayıcılar için istediğiniz seçimi yalnızca hello görüntüleri için kullanılabilir hale getirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2e43c-132">Learn how you can whitelist Azure Marketplace images, making available for selection only hello images you want for hello testers.</span></span>|
   | [<span data-ttu-id="2e43c-133">Özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="2e43c-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="2e43c-134">Sınayıcılar hızlı bir şekilde hello özel görüntü kullanarak bir VM oluşturmak için gereksinim duyduğunuz hello yazılımı yüklenerek özel bir görüntü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2e43c-134">Create a custom image by pre-installing hello software you need so that testers can quickly create a VM using hello custom image.</span></span>|
   | [<span data-ttu-id="2e43c-135">Görüntü Fabrika hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="2e43c-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="2e43c-136">Açıklayan bir video izlemek nasıl tooset ayarlama ve bir görüntü Fabrika kullanın.</span><span class="sxs-lookup"><span data-stu-id="2e43c-136">Watch a video that describes how tooset up and use an image factory.</span></span>|

3. <span data-ttu-id="2e43c-137">**Test makinelerini için yeniden kullanılabilir şablonlar oluşturma**</span><span class="sxs-lookup"><span data-stu-id="2e43c-137">**Create reusable templates for test machines**</span></span> 
   
    <span data-ttu-id="2e43c-138">Azure DevTest Labs formülde varsayılan özellik değerleri listesine toocreate VM kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2e43c-138">A formula in Azure DevTest Labs is a list of default property values used toocreate a VM.</span></span> <span data-ttu-id="2e43c-139">Görüntü, VM boyutu (CPU ve RAM birleşimi) ve bir sanal ağı seçerek hello laboratuarda bir formül oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e43c-139">You can create a formula in hello lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="2e43c-140">Her tester hello Laboratuvar hello formülde görebilir ve toocreate VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="2e43c-140">Each tester can see hello formula in hello lab and use it toocreate a VM.</span></span> 
   
    <span data-ttu-id="2e43c-141">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="2e43c-141">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="2e43c-142">Görev</span><span class="sxs-lookup"><span data-stu-id="2e43c-142">Task</span></span> | <span data-ttu-id="2e43c-143">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="2e43c-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="2e43c-144">DevTest Labs formüller toocreate sanal makineleri yönetme</span><span class="sxs-lookup"><span data-stu-id="2e43c-144">Manage DevTest Labs formulas toocreate VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="2e43c-145">Görüntü, VM boyutu (CPU ve RAM birleşimi) ve bir sanal ağ seçerek bir formül nasıl oluşturabileceğinizi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2e43c-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

3. <span data-ttu-id="2e43c-146">**Çoklu VM test ortamları oluşturma**</span><span class="sxs-lookup"><span data-stu-id="2e43c-146">**Create multi-VM test environments**</span></span> 
   
    <span data-ttu-id="2e43c-147">Azure Resource Manager şablonları toodefine hello altyapı ve Azure çözümünüzü yapılandırmasını kullanır ve art arda birden çok test tutarlı bir durumda VM'ler dağıtın.</span><span class="sxs-lookup"><span data-stu-id="2e43c-147">You can use Azure Resource Manager templates toodefine hello infrastructure and configuration of your Azure solution and repeatedly deploy multiple test VMs in a consistent state.</span></span>

    <span data-ttu-id="2e43c-148">Azure PaaS kaynaklarına bir ortamda bir Resource Manager şablonunda sağlanabilir ve maliyet izlemesi görünür.</span><span class="sxs-lookup"><span data-stu-id="2e43c-148">Azure PaaS resources can be provisioned in an environment from a Resource Manager template and appear in cost tracking.</span></span> <span data-ttu-id="2e43c-149">Ancak, VM otomatik kapatma tooPaaS kaynakların geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="2e43c-149">However, VM auto shutdown does not apply tooPaaS resources.</span></span>

    <span data-ttu-id="2e43c-150">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="2e43c-150">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="2e43c-151">Görev</span><span class="sxs-lookup"><span data-stu-id="2e43c-151">Task</span></span> | <span data-ttu-id="2e43c-152">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="2e43c-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="2e43c-153">Azure Resource Manager şablonları ile çoklu VM ortamları ve PaaS kaynakları oluşturma</span><span class="sxs-lookup"><span data-stu-id="2e43c-153">Create multi-VM environments and PaaS resources with Azure Resource Manager templates</span></span>](devtest-lab-create-environment-from-arm.md) |<span data-ttu-id="2e43c-154">Tutarlı bir durumda birden çok VM test ortamınızı nasıl dağıtabileceğiniz hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="2e43c-154">Learn how you can deploy multiple VMs in a consistent state for your test environment.</span></span>|

4. <span data-ttu-id="2e43c-155">**Yapıları tooenable esnek VM özelleştirme oluşturma**</span><span class="sxs-lookup"><span data-stu-id="2e43c-155">**Create artifacts tooenable flexible VM customization**</span></span>

   <span data-ttu-id="2e43c-156">Yapıları kullanılan toodeploy olan ve bir VM sağlandıktan sonra uygulamanızı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2e43c-156">Artifacts are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="2e43c-157">Yapıtlar şunlar olabilir:</span><span class="sxs-lookup"><span data-stu-id="2e43c-157">Artifacts can be:</span></span>

   - <span data-ttu-id="2e43c-158">Aracılar, Fiddler ve Visual Studio gibi hello VM - üzerinde tooinstall istediğiniz araçları.</span><span class="sxs-lookup"><span data-stu-id="2e43c-158">Tools that you want tooinstall on hello VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="2e43c-159">Bir depoyu kopyalama gibi hello VM - üzerinde toorun istediğiniz eylemleri.</span><span class="sxs-lookup"><span data-stu-id="2e43c-159">Actions that you want toorun on hello VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="2e43c-160">Tootest istediğiniz uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="2e43c-160">Applications that you want tootest.</span></span>

   <span data-ttu-id="2e43c-161">Birçok zaten kullanılabilir out-of--box ürünleridir.</span><span class="sxs-lookup"><span data-stu-id="2e43c-161">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="2e43c-162">Ancak, özel gereksinimlerinizi karşılamak için daha fazla özelleştirme istiyorsanız, özel yapıtları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e43c-162">But if you want more customization for your specific needs, you can create your own custom artifacts.</span></span>

   <span data-ttu-id="2e43c-163">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="2e43c-163">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="2e43c-164">Görev</span><span class="sxs-lookup"><span data-stu-id="2e43c-164">Task</span></span> | <span data-ttu-id="2e43c-165">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="2e43c-165">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="2e43c-166">DevTest Labs VM için özel yapılar oluşturma</span><span class="sxs-lookup"><span data-stu-id="2e43c-166">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="2e43c-167">Merhaba sanal makineler için kendi özel yapılar laboratuvarınızda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2e43c-167">Create your own custom artifacts for hello virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="2e43c-168">Bir Git deposu toostore özel yapılar ve kullanmak için Azure Resource Manager şablonları Azure DevTest Labs'de ekleme</span><span class="sxs-lookup"><span data-stu-id="2e43c-168">Add a Git repository toostore custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="2e43c-169">Bilgi nasıl toostore kendi özel Git depodaki özel yapıtları.</span><span class="sxs-lookup"><span data-stu-id="2e43c-169">Learn how toostore your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="2e43c-170">**Denetim maliyetleri**</span><span class="sxs-lookup"><span data-stu-id="2e43c-170">**Control costs**</span></span>
   
    <span data-ttu-id="2e43c-171">Azure DevTest Labs hello Laboratuvar toospecify hello en fazla sayıda hello laboratuarda tester tarafından oluşturulan sanal makineleri tooset bir ilke sağlar.</span><span class="sxs-lookup"><span data-stu-id="2e43c-171">Azure DevTest Labs allows you tooset a policy in hello lab toospecify hello maximum number of VMs that can be created by a tester in hello lab.</span></span> 
   
    <span data-ttu-id="2e43c-172">İş Çizelgesi kümesi test ekibiniz varsa ve toostop tüm hello VM'ler hello günün belirli bir zamanda istediğiniz ve ardından bunları günü izleyen hello otomatik olarak yeniden bunu kolayca, ayarı otomatik kapatma ve otomatik başlatma ilkeleri hello laboratuarda tarafından gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e43c-172">If your test team has a set work schedule and you want toostop all hello VMs at a particular time of hello day and then automatically restart them hello following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in hello lab.</span></span> 
   
    <span data-ttu-id="2e43c-173">Uygulama geliştirme tamamlandığında, son olarak, tüm hello sanal makineleri aynı anda tek bir PowerShell Betiği çalıştırarak silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e43c-173">Finally, when app development is complete, you can delete all hello VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="2e43c-174">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="2e43c-174">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="2e43c-175">Görev</span><span class="sxs-lookup"><span data-stu-id="2e43c-175">Task</span></span> | <span data-ttu-id="2e43c-176">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="2e43c-176">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="2e43c-177">Laboratuvar ilkelerini tanımlama</span><span class="sxs-lookup"><span data-stu-id="2e43c-177">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="2e43c-178">Maliyetleri hello laboratuvarda ilkeleri ayarlayarak denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e43c-178">Control costs by setting policies in hello lab.</span></span> |
   | [<span data-ttu-id="2e43c-179">Tüm hello Laboratuvar bir PowerShell komut dosyası kullanarak sanal makineleri silin</span><span class="sxs-lookup"><span data-stu-id="2e43c-179">Delete all hello lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="2e43c-180">Test tamamlandığında tek bir işlemde tüm hello labs silin.</span><span class="sxs-lookup"><span data-stu-id="2e43c-180">Delete all hello labs in one operation when testing is complete.</span></span>|

1. <span data-ttu-id="2e43c-181">**Sanal ağ tooa Laboratuvar ekleme**</span><span class="sxs-lookup"><span data-stu-id="2e43c-181">**Add a virtual network tooa Lab**</span></span> 
   
    <span data-ttu-id="2e43c-182">Her bir laboratuvar oluşturulduğunda DevTest Labs yeni bir sanal ağ (VNET) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2e43c-182">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="2e43c-183">Kendi VNET-Örneğin, ExpressRoute veya siteden siteye VPN kullanarak – yapılandırdıysanız, Vm'leri oluştururken, böylece kullanılabilir VNET tooyour Laboratuvar kullanıcının bu sanal ağ ayarları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e43c-183">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET tooyour lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="2e43c-184">Ayrıca, hello VM oluşturulduğunda, bir VM tooa etki alanına katılan bir Azure Active Directory etki alanı katılma yapıya kullanılabilir yoktur.</span><span class="sxs-lookup"><span data-stu-id="2e43c-184">In addition, there is an Azure Active Directory domain join artifact available that joins a VM tooa domain when hello VM is being created.</span></span> 
   
    <span data-ttu-id="2e43c-185">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="2e43c-185">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="2e43c-186">Görev</span><span class="sxs-lookup"><span data-stu-id="2e43c-186">Task</span></span> | <span data-ttu-id="2e43c-187">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="2e43c-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="2e43c-188">Azure DevTest Labs'de sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2e43c-188">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="2e43c-189">Nasıl tooconfigure Azure DevTest Labs kullanarak bir sanal ağ hello Azure portal hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="2e43c-189">Learn how tooconfigure a virtual network in Azure DevTest Labs using hello Azure portal.</span></span>|

6. <span data-ttu-id="2e43c-190">**Merhaba Laboratuvar her tester ile paylaşma**</span><span class="sxs-lookup"><span data-stu-id="2e43c-190">**Share hello lab with each tester**</span></span>
   
    <span data-ttu-id="2e43c-191">Labs, denetleyicilerle paylaşmanızı bir bağlantıyı kullanarak doğrudan erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="2e43c-191">Labs can be directly accessed using a link that you share with your testers.</span></span> <span data-ttu-id="2e43c-192">Sahip oldukları sürece bile toohave bir Azure hesabı sahip olmayan bir [Microsoft hesabı](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="2e43c-192">They don't even have toohave an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="2e43c-193">Sınayıcılar diğer test eden tarafından oluşturulan VM'ler göremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e43c-193">Testers cannot see VMs created by other testers.</span></span>  
   
    <span data-ttu-id="2e43c-194">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="2e43c-194">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="2e43c-195">Görev</span><span class="sxs-lookup"><span data-stu-id="2e43c-195">Task</span></span> | <span data-ttu-id="2e43c-196">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="2e43c-196">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="2e43c-197">Azure DevTest Labs'de tester tooa Laboratuvar ekleme</span><span class="sxs-lookup"><span data-stu-id="2e43c-197">Add a tester tooa lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="2e43c-198">Hello Azure portal tooadd sınayıcılar tooyour Laboratuvar kullanın.</span><span class="sxs-lookup"><span data-stu-id="2e43c-198">Use hello Azure portal tooadd testers tooyour lab.</span></span>|
   | [<span data-ttu-id="2e43c-199">Bir PowerShell Betiği kullanılarak sınayıcılar toohello Laboratuvar ekleme</span><span class="sxs-lookup"><span data-stu-id="2e43c-199">Add testers toohello lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="2e43c-200">Sınayıcılar tooyour Laboratuvar ekleme PowerShell tooautomate kullanın.</span><span class="sxs-lookup"><span data-stu-id="2e43c-200">Use PowerShell tooautomate adding testers tooyour lab.</span></span> |
   | [<span data-ttu-id="2e43c-201">Bir bağlantı toohello Laboratuvar Al</span><span class="sxs-lookup"><span data-stu-id="2e43c-201">Get a link toohello lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="2e43c-202">Nasıl sınayıcılar Laboratuvar köprü üzerinden doğrudan erişebileceğiniz öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2e43c-202">Learn how testers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="2e43c-203">**Daha fazla takımlar için laboratuvar oluşturmayı otomatikleştirmek**</span><span class="sxs-lookup"><span data-stu-id="2e43c-203">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="2e43c-204">Laboratuvar oluşturma, Resource Manager şablonu oluşturma ve toocreate aynı labs tekrar tekrar kullanarak özel ayarları da dahil olmak üzere otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e43c-204">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it toocreate identical labs again and again.</span></span> 
   
    <span data-ttu-id="2e43c-205">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="2e43c-205">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="2e43c-206">Görev</span><span class="sxs-lookup"><span data-stu-id="2e43c-206">Task</span></span> | <span data-ttu-id="2e43c-207">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="2e43c-207">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="2e43c-208">Resource Manager şablonu kullanarak bir laboratuvar oluşturma</span><span class="sxs-lookup"><span data-stu-id="2e43c-208">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="2e43c-209">Labs Resource Manager şablonları kullanarak Azure DevTest Labs içinde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2e43c-209">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

