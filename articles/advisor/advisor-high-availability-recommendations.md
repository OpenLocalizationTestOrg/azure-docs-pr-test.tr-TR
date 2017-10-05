---
title: "Azure Danışmanı yüksek kullanılabilirlik önerileri | Microsoft Docs"
description: "Azure dağıtımlarınızı yüksek kullanılabilirliğini artırmak için Azure Danışmanı'nı kullanın."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 23c159471a6e5a7ad9cb545840e8afd3ac72ecba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-high-availability-recommendations"></a><span data-ttu-id="a7181-103">Advisor yüksek kullanılabilirlik önerileri</span><span class="sxs-lookup"><span data-stu-id="a7181-103">Advisor High Availability recommendations</span></span>

<span data-ttu-id="a7181-104">Azure Danışmanı emin olun ve iş açısından kritik uygulamalarınızı sürekliliği artırmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a7181-104">Azure Advisor helps you ensure and improve the continuity of your business-critical applications.</span></span> <span data-ttu-id="a7181-105">Danışmanına göre yüksek kullanılabilirlik öneriler alabilirsiniz **yüksek kullanılabilirlik** Danışmanı Pano sekmesi.</span><span class="sxs-lookup"><span data-stu-id="a7181-105">You can get high availability recommendations by Advisor from the **High Availability** tab of the Advisor dashboard.</span></span>

![Advisor Panoda yüksek kullanılabilirlik düğmesi](./media/advisor-high-availability-recommendations/advisor-high-availability-tab.png)


## <a name="ensure-virtual-machine-fault-tolerance"></a><span data-ttu-id="a7181-107">Sanal makine hataya dayanıklılık sağlamak</span><span class="sxs-lookup"><span data-stu-id="a7181-107">Ensure virtual machine fault tolerance</span></span>

<span data-ttu-id="a7181-108">Advisor bir kullanılabilirlik kümesi ve bir kullanılabilirlik kümesine taşıma önerir parçası olmayan sanal makineleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a7181-108">Advisor identifies virtual machines that are not part of an availability set and recommends moving them into an availability set.</span></span> <span data-ttu-id="a7181-109">Uygulamanıza yedeklilik sağlamak için bir kullanılabilirlik kümesinde iki veya daha fazla sanal makinenin gruplandırılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="a7181-109">To provide redundancy to your application, we recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="a7181-110">Bu yapılandırma ya da bir planlı veya plansız bir bakım olayı sırasında en az bir sanal makine kullanılabilir ve Azure sanal makinesi SLA karşılayan sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7181-110">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine is available and meets the Azure virtual machine SLA.</span></span> <span data-ttu-id="a7181-111">Kullanılabilirlik kümesi için sanal makine oluşturmak için ya da sanal makineyi var olan bir kullanılabilirlik kümesine eklemeyi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7181-111">You can choose either to create an availability set for the virtual machine or to add the virtual machine to an existing availability set.</span></span>

> [!NOTE]
> <span data-ttu-id="a7181-112">Bir kullanılabilirlik kümesi oluşturmayı seçerseniz, en az bir daha fazla sanal makine içine eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7181-112">If you choose to create an availability set, you must add at least one more virtual machine into it.</span></span> <span data-ttu-id="a7181-113">En az bir makine olduğundan emin olmak için iki veya daha fazla sanal makine bir kullanılabilirlik kümesi bu, Grup kesinti sırasında kullanılabilir öneririz.</span><span class="sxs-lookup"><span data-stu-id="a7181-113">We recommend that you group two or more virtual machines in an availability set to ensure that at least one machine is available during an outage.</span></span>

![Advisor öneri: sanal makine artıklık için kullanılabilirlik kümelerini kullanın](./media/advisor-high-availability-recommendations/advisor-high-availability-create-availability-set.png)

## <a name="ensure-availability-set-fault-tolerance"></a><span data-ttu-id="a7181-115">Hataya dayanıklılık kullanılabilirlik kümesi emin olun</span><span class="sxs-lookup"><span data-stu-id="a7181-115">Ensure availability set fault tolerance</span></span> 

<span data-ttu-id="a7181-116">Advisor tek bir sanal makine içeren kullanılabilirlik kümeleri tanımlar ve bir veya daha fazla sanal makine eklemeyi önerir.</span><span class="sxs-lookup"><span data-stu-id="a7181-116">Advisor identifies availability sets that contain a single virtual machine and recommends adding one or more virtual machines to it.</span></span> <span data-ttu-id="a7181-117">Uygulamanıza yedeklilik sağlamak için bir kullanılabilirlik kümesinde iki veya daha fazla sanal makinenin gruplandırılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="a7181-117">To provide redundancy to your application, we recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="a7181-118">Bu yapılandırma ya da bir planlı veya plansız bir bakım olayı sırasında en az bir sanal makine kullanılabilir ve Azure sanal makinesi SLA karşılayan sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7181-118">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine is available and meets the Azure virtual machine SLA.</span></span> <span data-ttu-id="a7181-119">Ya da bir sanal makine oluşturmak için veya mevcut bir sanal makine kullanmayı ve kullanılabilirlik kümesine eklemek için seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7181-119">You can choose either to create a virtual machine or to use an existing virtual machine, and to add it to the availability set.</span></span>  

![Advisor öneri: bir veya daha fazla sanal makine bu kullanılabilirlik kümesine ekleme](./media/advisor-high-availability-recommendations/advisor-high-availability-add-vm-to-availability-set.png)


## <a name="ensure-application-gateway-fault-tolerance"></a><span data-ttu-id="a7181-121">Uygulama ağ geçidi hataya dayanıklılık sağlamak</span><span class="sxs-lookup"><span data-stu-id="a7181-121">Ensure application gateway fault tolerance</span></span>
<span data-ttu-id="a7181-122">Uygulama ağ geçidi tarafından desteklenen kritik uygulamaların iş sürekliliğini sağlamak için hataya dayanıklılık için yapılandırılmamış uygulama ağ geçidi örnekleri Danışmanı tanımlar ve yapabileceğiniz düzeltme eylemleri önerir.</span><span class="sxs-lookup"><span data-stu-id="a7181-122">To ensure the business continuity of mission-critical applications that are powered by application gateways, Advisor identifies application gateway instances that are not configured for fault tolerance, and it suggests remediation actions that you can take.</span></span> <span data-ttu-id="a7181-123">Orta veya büyük tek örnekli uygulama ağ geçitleri Danışmanı tanımlar ve en az bir daha fazla örneğini eklemede önerir.</span><span class="sxs-lookup"><span data-stu-id="a7181-123">Advisor identifies medium or large single-instance application gateways, and it recommends adding at least one more instance.</span></span> <span data-ttu-id="a7181-124">Ayrıca, tek veya birden çok instance küçük uygulama ağ geçitleri tanımlar ve orta veya büyük SKU'ları için geçiş önerir.</span><span class="sxs-lookup"><span data-stu-id="a7181-124">It also identifies single- or multi-instance small application gateways and recommends migrating to medium or large SKUs.</span></span> <span data-ttu-id="a7181-125">Advisor, uygulama ağ geçidi örnekleri bu kaynakların geçerli SLA gereksinimlerini karşılamak için yapılandırıldığından emin olmak için bu eylemleri önerir.</span><span class="sxs-lookup"><span data-stu-id="a7181-125">Advisor recommends these actions to ensure that your application gateway instances are configured to satisfy the current SLA requirements for these resources.</span></span>

![Advisor öneri: iki veya daha fazla Orta veya büyük boyutlu uygulama ağ geçidi örnekleri dağıtma](./media/advisor-high-availability-recommendations/advisor-high-availability-application-gateway.png)

## <a name="improve-the-performance-and-reliability-of-virtual-machine-disks"></a><span data-ttu-id="a7181-127">Sanal makine disklerini güvenilirliğini ve performansını geliştirmek</span><span class="sxs-lookup"><span data-stu-id="a7181-127">Improve the performance and reliability of virtual machine disks</span></span>

<span data-ttu-id="a7181-128">Advisor standart diskler ile sanal makineleri tanımlar ve premium disklere yükseltme önerir.</span><span class="sxs-lookup"><span data-stu-id="a7181-128">Advisor identifies virtual machines with standard disks and recommends upgrading to premium disks.</span></span>
 
<span data-ttu-id="a7181-129">Azure Premium depolama g/Ç kullanımı yoğun iş yükleri çalıştıran sanal makineler için yüksek performanslı, düşük gecikmeli disk desteği sunar.</span><span class="sxs-lookup"><span data-stu-id="a7181-129">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines that run I/O-intensive workloads.</span></span> <span data-ttu-id="a7181-130">Premium depolama hesapları kullanan sanal makine diskler katı hal sürücüleri (SSD) verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="a7181-130">Virtual machine disks that use premium storage accounts store data on solid-state drives (SSDs).</span></span> <span data-ttu-id="a7181-131">Uygulamanız için en iyi performans için premium depolama alanına yüksek IOPS gerektiren herhangi bir sanal makine disklerini geçirmek öneririz.</span><span class="sxs-lookup"><span data-stu-id="a7181-131">For the best performance for your application, we recommend that you migrate any virtual machine disks requiring high IOPS to premium storage.</span></span> 

<span data-ttu-id="a7181-132">Disklerinizi yüksek IOPS ihtiyacınız yoksa, standart depolama tutarak maliyetleri sınırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7181-132">If your disks do not require high IOPS, you can limit costs by maintaining them in standard storage.</span></span> <span data-ttu-id="a7181-133">Standart depolama SSD yerine sabit disk sürücülerinin (HDD'ler) üzerinde sanal makine disk verilerini depolar.</span><span class="sxs-lookup"><span data-stu-id="a7181-133">Standard storage stores virtual machine disk data on hard disk drives (HDDs) instead of SSDs.</span></span> <span data-ttu-id="a7181-134">Sanal makine disklerinizi premium diskleri geçirmek seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7181-134">You can choose to migrate your virtual machine disks to premium disks.</span></span> <span data-ttu-id="a7181-135">Premium diskleri çoğu sanal makine SKU'ları üzerinde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a7181-135">Premium disks are supported on most virtual machine SKUs.</span></span> <span data-ttu-id="a7181-136">Premium diskleri kullanmak istiyorsanız, ancak bazı durumlarda, sanal makinenize SKU'ları da yükseltmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="a7181-136">However, in some cases, if you want to use premium disks, you might need to upgrade your virtual machine SKUs as well.</span></span>

![Advisor öneri: premium diskleri yükselterek, sanal makine diskleriniz güvenilirliğini geliştirmeye](./media/advisor-high-availability-recommendations/advisor-high-availability-upgrade-to-premium-disks.png)

## <a name="protect-your-virtual-machine-data-from-accidental-deletion"></a><span data-ttu-id="a7181-138">Sanal makine verilerinizi yanlışlıkla silinmeye karşı koru</span><span class="sxs-lookup"><span data-stu-id="a7181-138">Protect your virtual machine data from accidental deletion</span></span>
<span data-ttu-id="a7181-139">Advisor burada yedekleme etkin değil ve yedekleme etkinleştirme önerir sanal makineleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a7181-139">Advisor identifies virtual machines where backup is not enabled, and it recommends enabling backup.</span></span> <span data-ttu-id="a7181-140">Sanal makine yedekleme ayarı, iş açısından kritik verilerin kullanılabilirliğini sağlar ve yanlışlıkla silme veya bozulmasına karşı koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7181-140">Setting up virtual machine backup ensures the availability of your business-critical data and offers protection against accidental deletion or corruption.</span></span>

![Advisor öneri: Görev açısından kritik verilerinizi korumak için sanal makine yedeklemeyi yapılandırma](./media/advisor-high-availability-recommendations/advisor-high-availability-virtual-machine-backup.png)

## <a name="access-high-availability-recommendations-in-advisor"></a><span data-ttu-id="a7181-142">Advisor erişim yüksek kullanılabilirlik önerileri</span><span class="sxs-lookup"><span data-stu-id="a7181-142">Access high availability recommendations in Advisor</span></span>

1. <span data-ttu-id="a7181-143">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a7181-143">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="a7181-144">Sol bölmede **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="a7181-144">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="a7181-145">Hizmet menü bölmesinde altında **izleme ve Yönetim**, tıklatın **Azure Danışmanı**.</span><span class="sxs-lookup"><span data-stu-id="a7181-145">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="a7181-146">Advisor Panosu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a7181-146">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="a7181-147">Advisor Panoda tıklatın **yüksek kullanılabilirlik** sekmesini tıklatın ve ardından önerileri almak istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="a7181-147">On the Advisor dashboard, click the **High Availability** tab, and then select the subscription for which you want to receive recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="a7181-148">Advisor önerileri erişmek için öncelikle *aboneliğinizi kaydetmek* Danışmanı ile.</span><span class="sxs-lookup"><span data-stu-id="a7181-148">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="a7181-149">Bir abonelik kayıtlı olduğunda bir *abonelik sahibi* Danışmanı Pano başlatır ve tıkladığında **alma önerileri** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a7181-149">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="a7181-150">Bu bir *tek seferlik işlem*.</span><span class="sxs-lookup"><span data-stu-id="a7181-150">This is a *one-time operation*.</span></span> <span data-ttu-id="a7181-151">Abonelik kaydedildikten sonra Advisor önerileri olarak erişebilir *sahibi*, *katkıda bulunan*, veya *okuyucu* bir abonelik, bir kaynak grubu ya da belirli bir kaynak için.</span><span class="sxs-lookup"><span data-stu-id="a7181-151">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7181-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a7181-152">Next steps</span></span>

<span data-ttu-id="a7181-153">Advisor önerileri hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="a7181-153">For more information about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="a7181-154">Azure Danışmanı giriş</span><span class="sxs-lookup"><span data-stu-id="a7181-154">Introduction to Azure Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="a7181-155">Danışman’ı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a7181-155">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="a7181-156">Advisor maliyet önerileri</span><span class="sxs-lookup"><span data-stu-id="a7181-156">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="a7181-157">Advisor performans önerileri</span><span class="sxs-lookup"><span data-stu-id="a7181-157">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="a7181-158">Advisor güvenlik önerileri</span><span class="sxs-lookup"><span data-stu-id="a7181-158">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)

