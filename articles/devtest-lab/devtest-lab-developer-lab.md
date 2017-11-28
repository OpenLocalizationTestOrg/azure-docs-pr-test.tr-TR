---
title: "Geliştiriciler için Azure DevTest Labs aaaUse | Microsoft Docs"
description: "Bilgi nasıl toouse Azure DevTest Labs Geliştirici senaryoları için."
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
ms.openlocfilehash: 16a3ef47c9fcbca3050dd50db5b472a9a1e3c62c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-developers"></a><span data-ttu-id="4f0a3-103">Geliştiriciler için Azure DevTest Labs kullanın</span><span class="sxs-lookup"><span data-stu-id="4f0a3-103">Use Azure DevTest Labs for developers</span></span>
<span data-ttu-id="4f0a3-104">Azure DevTest Labs birçok senaryoları ancak hello birincil senaryoları birini içerir geliştiriciler için DevTest Labs toohost geliştirme makineleri kullanarak kullanılan tooimplement olabilir.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-104">Azure DevTest Labs can be used tooimplement many key scenarios, but one of hello primary scenarios involves using DevTest Labs toohost development machines for developers.</span></span> <span data-ttu-id="4f0a3-105">Bu senaryoda, DevTest Labs şu avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="4f0a3-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="4f0a3-106">Geliştiriciler, geliştirme makinelerinin isteğe bağlı olarak hızlı bir şekilde sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-106">Developers can quickly provision their development machines on demand.</span></span>
- <span data-ttu-id="4f0a3-107">Geliştiriciler, geliştirme makinelerinin gerektiğinde kolayca özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-107">Developers can easily customize their development machines whenever needed.</span></span>
- <span data-ttu-id="4f0a3-108">Yöneticiler, sağlayarak maliyetleri denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4f0a3-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="4f0a3-109">Geliştiriciler, geliştirme için gerekenden daha fazla VMs alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-109">Developers cannot get more VMs than they need for development.</span></span>
  - <span data-ttu-id="4f0a3-110">Sanal makineleri ne zaman kullanılmıyor kapatılır.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-110">VMs are shut down when not in use.</span></span> 

![DevTest Labs için eğitim kullanın](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="4f0a3-112">Bu makalede kullanılan toomeet geliştirici gereksinimleri ve bir laboratuvar yukarı tooset izleyebileceğiniz ayrıntılı adımlar hello çeşitli Azure DevTest Labs özellikleri hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-112">In this article, you learn about various Azure DevTest Labs features that can be used toomeet developer requirements and hello detailed steps that you can follow tooset up a lab.</span></span>

## <a name="implementing-developer-environments-with-azure-devtest-labs"></a><span data-ttu-id="4f0a3-113">Azure DevTest Labs Geliştirici ortamlarıyla uygulama</span><span class="sxs-lookup"><span data-stu-id="4f0a3-113">Implementing developer environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="4f0a3-114">**Merhaba Laboratuvar oluşturma**</span><span class="sxs-lookup"><span data-stu-id="4f0a3-114">**Create hello lab**</span></span> 
   
    <span data-ttu-id="4f0a3-115">Labs hello Azure DevTest Labs'de başlangıç noktası var.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-115">Labs are hello starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="4f0a3-116">Bir laboratuvar oluşturduktan sonra kullanıcılar (geliştiriciler) toohello Laboratuvar, hızlı bir şekilde, oluşturabilirsiniz VM görüntülerini tanımlama, ayar ilkeleri toocontrol maliyetleri ve daha fazlasını ekleme gibi görevleri gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-116">Once you create a lab, you can perform tasks such as adding users (developers) toohello lab, setting policies toocontrol costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="4f0a3-117">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="4f0a3-117">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="4f0a3-118">Görev</span><span class="sxs-lookup"><span data-stu-id="4f0a3-118">Task</span></span> | <span data-ttu-id="4f0a3-119">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="4f0a3-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4f0a3-120">Azure DevTest Labs'de Laboratuvar oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f0a3-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="4f0a3-121">Azure DevTest Labs'de Laboratuvar bir toocreate hello Azure portalına nasıl öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-121">Learn how toocreate a lab in Azure DevTest Labs in hello Azure portal.</span></span> |
2. <span data-ttu-id="4f0a3-122">**Sanal makineleri hazır Market görüntülerini ve özel görüntüleri kullanarak dakikalar içinde oluşturma**</span><span class="sxs-lookup"><span data-stu-id="4f0a3-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="4f0a3-123">Görüntüler çok geniş bir yelpazedeki hazır görüntülerden hello Azure Marketi seçer ve hello laboratuarda kullanılabilmesini.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-123">You can pick ready-made images from a wide variety of images in hello Azure Marketplace and make them available in hello lab.</span></span> <span data-ttu-id="4f0a3-124">Merhaba hazır görüntüleri gereksinimlerinizi karşılamıyorsa, Laboratuvar hello Laboratuvar özel görüntü olarak Azure marketi, gereksinim duyduğunuz tüm hello yazılım yükleme ve kaydetme hello VM hazır bir görüntüden kullanarak VM oluşturarak özel bir görüntü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-124">If hello ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all hello software that you need, and saving hello VM as a custom image in hello lab.</span></span>

    <span data-ttu-id="4f0a3-125">Özel resimler kullanacaksanız, bir görüntü Fabrika toocreate kullanmayı düşünün ve resimlerinizi dağıtın.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-125">If you will be using custom images, consider using an image factory toocreate and distribute your images.</span></span> <span data-ttu-id="4f0a3-126">Bir görüntü Fabrika düzenli olarak oluşturur ve yapılandırılmış görüntülerinizin otomatik olarak dağıtan bir yapılandırma olarak kodu çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="4f0a3-127">Bir VM ile Merhaba oluşturulduktan sonra bu kaydeder hello gereken süre toomanually yapılandırma hello sistem işletim sistemi temel.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-127">This saves hello time required toomanually configure hello system after a VM has been created with hello base OS.</span></span>
  
    <span data-ttu-id="4f0a3-128">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="4f0a3-128">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="4f0a3-129">Görev</span><span class="sxs-lookup"><span data-stu-id="4f0a3-129">Task</span></span> | <span data-ttu-id="4f0a3-130">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="4f0a3-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4f0a3-131">Azure Market görüntülerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4f0a3-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="4f0a3-132">Beyaz liste Azure Market görüntülerini hello geliştiriciler için istediğiniz seçimi yalnızca hello görüntüleri için kullanılabilir hale getirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-132">Learn how you can whitelist Azure Marketplace images, making available for selection only hello images you want for hello developers.</span></span>|
   | [<span data-ttu-id="4f0a3-133">Özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="4f0a3-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="4f0a3-134">Böylece geliştiriciler, hızlı bir şekilde hello özel görüntü kullanarak bir VM oluşturabilir, gereken hello yazılımı yüklenerek özel bir görüntü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-134">Create a custom image by pre-installing hello software you need so that developers can quickly create a VM using hello custom image.</span></span>|
   | [<span data-ttu-id="4f0a3-135">Görüntü Fabrika hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="4f0a3-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="4f0a3-136">Açıklayan bir video izlemek nasıl tooset ayarlama ve bir görüntü Fabrika kullanın.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-136">Watch a video that describes how tooset up and use an image factory.</span></span>|

3. <span data-ttu-id="4f0a3-137">**Geliştirici makinelerinde için yeniden kullanılabilir şablonlar oluşturma**</span><span class="sxs-lookup"><span data-stu-id="4f0a3-137">**Create reusable templates for developer machines**</span></span> 
   
    <span data-ttu-id="4f0a3-138">Azure DevTest Labs formülde varsayılan özellik değerleri listesine toocreate VM kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-138">A formula in Azure DevTest Labs is a list of default property values used toocreate a VM.</span></span> <span data-ttu-id="4f0a3-139">Görüntü, VM boyutu (CPU ve RAM birleşimi) ve bir sanal ağı seçerek hello laboratuarda bir formül oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-139">You can create a formula in hello lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="4f0a3-140">Her geliştirici hello Laboratuvar hello formülde görebilir ve toocreate VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-140">Each developer can see hello formula in hello lab and use it toocreate a VM.</span></span> 
   
    <span data-ttu-id="4f0a3-141">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="4f0a3-141">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="4f0a3-142">Görev</span><span class="sxs-lookup"><span data-stu-id="4f0a3-142">Task</span></span> | <span data-ttu-id="4f0a3-143">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="4f0a3-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4f0a3-144">DevTest Labs formüller toocreate sanal makineleri yönetme</span><span class="sxs-lookup"><span data-stu-id="4f0a3-144">Manage DevTest Labs formulas toocreate VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="4f0a3-145">Görüntü, VM boyutu (CPU ve RAM birleşimi) ve bir sanal ağ seçerek bir formül nasıl oluşturabileceğinizi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

4. <span data-ttu-id="4f0a3-146">**Yapıları tooenable esnek VM özelleştirme oluşturma**</span><span class="sxs-lookup"><span data-stu-id="4f0a3-146">**Create artifacts tooenable flexible VM customization**</span></span>

   <span data-ttu-id="4f0a3-147">Yapıları kullanılan toodeploy olan ve bir VM sağlandıktan sonra uygulamanızı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-147">Artifacts are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="4f0a3-148">Yapıtlar şunlar olabilir:</span><span class="sxs-lookup"><span data-stu-id="4f0a3-148">Artifacts can be:</span></span>

   - <span data-ttu-id="4f0a3-149">Aracılar, Fiddler ve Visual Studio gibi hello VM - üzerinde tooinstall istediğiniz araçları.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-149">Tools that you want tooinstall on hello VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="4f0a3-150">Bir depoyu kopyalama gibi hello VM - üzerinde toorun istediğiniz eylemleri.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-150">Actions that you want toorun on hello VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="4f0a3-151">Tootest istediğiniz uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-151">Applications that you want tootest.</span></span>

   <span data-ttu-id="4f0a3-152">Birçok zaten kullanılabilir out-of--box ürünleridir.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-152">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="4f0a3-153">Özel ihtiyaçlarınız için daha fazla özelleştirme isterseniz kendi özel yapılar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-153">You can create your own custom artifacts if you want more customization for your specific needs.</span></span>

   <span data-ttu-id="4f0a3-154">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="4f0a3-154">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="4f0a3-155">Görev</span><span class="sxs-lookup"><span data-stu-id="4f0a3-155">Task</span></span> | <span data-ttu-id="4f0a3-156">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="4f0a3-156">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4f0a3-157">DevTest Labs VM için özel yapılar oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f0a3-157">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="4f0a3-158">Merhaba sanal makineler için kendi özel yapılar laboratuvarınızda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-158">Create your own custom artifacts for hello virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="4f0a3-159">Bir Git deposu toostore özel yapılar ve kullanmak için Azure Resource Manager şablonları Azure DevTest Labs'de ekleme</span><span class="sxs-lookup"><span data-stu-id="4f0a3-159">Add a Git repository toostore custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="4f0a3-160">Bilgi nasıl toostore kendi özel Git depodaki özel yapıtları.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-160">Learn how toostore your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="4f0a3-161">**Denetim maliyetleri**</span><span class="sxs-lookup"><span data-stu-id="4f0a3-161">**Control costs**</span></span>
   
    <span data-ttu-id="4f0a3-162">Azure DevTest Labs hello Laboratuvar toospecify hello en fazla sayıda hello laboratuarda bir geliştirici tarafından oluşturulan sanal makineleri tooset bir ilke sağlar.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-162">Azure DevTest Labs allows you tooset a policy in hello lab toospecify hello maximum number of VMs that can be created by a developer in hello lab.</span></span> 
   
    <span data-ttu-id="4f0a3-163">İş Çizelgesi kümesi Geliştirici ekibiniz varsa ve toostop tüm hello VM'ler hello günün belirli bir zamanda istediğiniz ve ardından bunları günü izleyen hello otomatik olarak yeniden bunu kolayca, ayarı otomatik kapatma ve otomatik başlatma ilkeleri hello laboratuarda tarafından gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-163">If your developer team has a set work schedule and you want toostop all hello VMs at a particular time of hello day and then automatically restart them hello following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in hello lab.</span></span> 
   
    <span data-ttu-id="4f0a3-164">Uygulama geliştirme tamamlandığında, son olarak, tüm hello sanal makineleri aynı anda tek bir PowerShell Betiği çalıştırarak silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-164">Finally, when app development is complete, you can delete all hello VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="4f0a3-165">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="4f0a3-165">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="4f0a3-166">Görev</span><span class="sxs-lookup"><span data-stu-id="4f0a3-166">Task</span></span> | <span data-ttu-id="4f0a3-167">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="4f0a3-167">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4f0a3-168">Laboratuvar ilkelerini tanımlama</span><span class="sxs-lookup"><span data-stu-id="4f0a3-168">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="4f0a3-169">Maliyetleri hello laboratuvarda ilkeleri ayarlayarak denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-169">Control costs by setting policies in hello lab.</span></span> |
   | [<span data-ttu-id="4f0a3-170">Tüm hello Laboratuvar bir PowerShell komut dosyası kullanarak sanal makineleri silin</span><span class="sxs-lookup"><span data-stu-id="4f0a3-170">Delete all hello lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="4f0a3-171">Geliştirme tamamlandığında, tek bir işlemde tüm hello labs silin.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-171">Delete all hello labs in one operation when development is complete.</span></span>|

1. <span data-ttu-id="4f0a3-172">**Sanal ağ tooa VM ekleme**</span><span class="sxs-lookup"><span data-stu-id="4f0a3-172">**Add a virtual network tooa VM**</span></span> 
   
    <span data-ttu-id="4f0a3-173">Her bir laboratuvar oluşturulduğunda DevTest Labs yeni bir sanal ağ (VNET) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-173">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="4f0a3-174">Kendi VNET-Örneğin, ExpressRoute veya siteden siteye VPN kullanarak – yapılandırdıysanız, Vm'leri oluştururken, böylece kullanılabilir VNET tooyour Laboratuvar kullanıcının bu sanal ağ ayarları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-174">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET tooyour lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="4f0a3-175">Ayrıca, bir Azure Active Directory etki alanı katılma yapı hello VM oluşturulduğunda, bir VM tooa etki alanına katılacak kullanılabilir yoktur.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-175">In addition, there is an Azure Active Directory domain join artifact available that will join a VM tooa domain when hello VM is being created.</span></span> 
   
    <span data-ttu-id="4f0a3-176">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="4f0a3-176">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="4f0a3-177">Görev</span><span class="sxs-lookup"><span data-stu-id="4f0a3-177">Task</span></span> | <span data-ttu-id="4f0a3-178">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="4f0a3-178">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4f0a3-179">Azure DevTest Labs'de sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4f0a3-179">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="4f0a3-180">Nasıl tooconfigure Azure DevTest Labs kullanarak bir sanal ağ hello Azure portal hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-180">Learn how tooconfigure a virtual network in Azure DevTest Labs using hello Azure portal.</span></span>|

6. <span data-ttu-id="4f0a3-181">**Her geliştirici paylaşımı hello laboratuvarla**</span><span class="sxs-lookup"><span data-stu-id="4f0a3-181">**Share hello lab with each developer**</span></span>
   
    <span data-ttu-id="4f0a3-182">Labs, geliştiricilere paylaşan bir bağlantıyı kullanarak doğrudan erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-182">Labs can be directly accessed using a link that you share with your developers.</span></span> <span data-ttu-id="4f0a3-183">Sahip oldukları sürece bile toohave bir Azure hesabı sahip olmayan bir [Microsoft hesabı](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="4f0a3-183">They don't even have toohave an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="4f0a3-184">Geliştiriciler, diğer geliştiriciler tarafından oluşturulan VM'ler göremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-184">Developers cannot see VMs created by other developers.</span></span>  
   
    <span data-ttu-id="4f0a3-185">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="4f0a3-185">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="4f0a3-186">Görev</span><span class="sxs-lookup"><span data-stu-id="4f0a3-186">Task</span></span> | <span data-ttu-id="4f0a3-187">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="4f0a3-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4f0a3-188">Azure DevTest Labs'de Geliştirici tooa Laboratuvar ekleme</span><span class="sxs-lookup"><span data-stu-id="4f0a3-188">Add a developer tooa lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="4f0a3-189">Hello Azure portal tooadd geliştiriciler tooyour Laboratuvar kullanın.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-189">Use hello Azure portal tooadd developers tooyour lab.</span></span>|
   | [<span data-ttu-id="4f0a3-190">Bir PowerShell Betiği kullanılarak geliştiriciler toohello Laboratuvar ekleme</span><span class="sxs-lookup"><span data-stu-id="4f0a3-190">Add developers toohello lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="4f0a3-191">Geliştiriciler tooyour Laboratuvar ekleme PowerShell tooautomate kullanın.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-191">Use PowerShell tooautomate adding developers tooyour lab.</span></span> |
   | [<span data-ttu-id="4f0a3-192">Bir bağlantı toohello Laboratuvar Al</span><span class="sxs-lookup"><span data-stu-id="4f0a3-192">Get a link toohello lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="4f0a3-193">Nasıl geliştiriciler Laboratuvar köprü üzerinden doğrudan erişebileceğiniz öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-193">Learn how developers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="4f0a3-194">**Daha fazla takımlar için laboratuvar oluşturmayı otomatikleştirmek**</span><span class="sxs-lookup"><span data-stu-id="4f0a3-194">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="4f0a3-195">Laboratuvar oluşturma, Resource Manager şablonu oluşturma ve toocreate aynı labs tekrar tekrar kullanarak özel ayarları da dahil olmak üzere otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-195">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it toocreate identical labs again and again.</span></span> 
   
    <span data-ttu-id="4f0a3-196">Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="4f0a3-196">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="4f0a3-197">Görev</span><span class="sxs-lookup"><span data-stu-id="4f0a3-197">Task</span></span> | <span data-ttu-id="4f0a3-198">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="4f0a3-198">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4f0a3-199">Resource Manager şablonu kullanarak bir laboratuvar oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f0a3-199">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="4f0a3-200">Labs Resource Manager şablonları kullanarak Azure DevTest Labs içinde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4f0a3-200">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

