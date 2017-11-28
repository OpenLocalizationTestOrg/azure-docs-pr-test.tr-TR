---
title: "aaaAzure Danışmanı yüksek kullanılabilirlik önerileri | Microsoft Docs"
description: "Azure Danışmanı tooimprove yüksek kullanılabilirliğini Azure dağıtımlarınızı kullanın."
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
ms.openlocfilehash: 3ac75ce401271f0212d198d7a7dc75ab702b6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-high-availability-recommendations"></a><span data-ttu-id="06eea-103">Advisor yüksek kullanılabilirlik önerileri</span><span class="sxs-lookup"><span data-stu-id="06eea-103">Advisor High Availability recommendations</span></span>

<span data-ttu-id="06eea-104">Azure Danışmanı emin olun ve iş açısından kritik uygulamalar hello sürekliliği artırmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="06eea-104">Azure Advisor helps you ensure and improve hello continuity of your business-critical applications.</span></span> <span data-ttu-id="06eea-105">Hello Danışmanı göre yüksek kullanılabilirlik öneriler alabilirsiniz **yüksek kullanılabilirlik** hello Danışmanı Pano sekmesi.</span><span class="sxs-lookup"><span data-stu-id="06eea-105">You can get high availability recommendations by Advisor from hello **High Availability** tab of hello Advisor dashboard.</span></span>

![Merhaba Danışmanı Panoda yüksek kullanılabilirlik düğmesi](./media/advisor-high-availability-recommendations/advisor-high-availability-tab.png)


## <a name="ensure-virtual-machine-fault-tolerance"></a><span data-ttu-id="06eea-107">Sanal makine hataya dayanıklılık sağlamak</span><span class="sxs-lookup"><span data-stu-id="06eea-107">Ensure virtual machine fault tolerance</span></span>

<span data-ttu-id="06eea-108">Advisor bir kullanılabilirlik kümesi ve bir kullanılabilirlik kümesine taşıma önerir parçası olmayan sanal makineleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="06eea-108">Advisor identifies virtual machines that are not part of an availability set and recommends moving them into an availability set.</span></span> <span data-ttu-id="06eea-109">Artıklık tooyour uygulama sağlamak için bir kullanılabilirlik kümesinde iki veya daha fazla sanal makineyi gruplandırmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="06eea-109">To provide redundancy tooyour application, we recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="06eea-110">Bu yapılandırma ya da bir planlı veya plansız bir bakım olayı sırasında en az bir sanal makine kullanılabilir ve Azure sanal makinesi SLA karşılıyor hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="06eea-110">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine is available and meets hello Azure virtual machine SLA.</span></span> <span data-ttu-id="06eea-111">Merhaba sanal makine ya da tooadd hello sanal makine tooan varolan kullanılabilirlik kümesi için bir kullanılabilirlik ya da toocreate seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06eea-111">You can choose either toocreate an availability set for hello virtual machine or tooadd hello virtual machine tooan existing availability set.</span></span>

> [!NOTE]
> <span data-ttu-id="06eea-112">Bir kullanılabilirlik toocreate seçerseniz ayarla, en az bir daha fazla sanal makine içine eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="06eea-112">If you choose toocreate an availability set, you must add at least one more virtual machine into it.</span></span> <span data-ttu-id="06eea-113">İki grup veya tooensure daha fazla sanal makine bir kullanılabilirlik kümesi öneririz en az bir makine kesinti sırasında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="06eea-113">We recommend that you group two or more virtual machines in an availability set tooensure that at least one machine is available during an outage.</span></span>

![Advisor öneri: sanal makine artıklık için kullanılabilirlik kümelerini kullanın](./media/advisor-high-availability-recommendations/advisor-high-availability-create-availability-set.png)

## <a name="ensure-availability-set-fault-tolerance"></a><span data-ttu-id="06eea-115">Hataya dayanıklılık kullanılabilirlik kümesi emin olun</span><span class="sxs-lookup"><span data-stu-id="06eea-115">Ensure availability set fault tolerance</span></span> 

<span data-ttu-id="06eea-116">Advisor tek bir sanal makine içeren kullanılabilirlik kümeleri tanımlar ve bir veya daha fazla sanal makine tooit ekleme önerir.</span><span class="sxs-lookup"><span data-stu-id="06eea-116">Advisor identifies availability sets that contain a single virtual machine and recommends adding one or more virtual machines tooit.</span></span> <span data-ttu-id="06eea-117">Artıklık tooyour uygulama sağlamak için bir kullanılabilirlik kümesinde iki veya daha fazla sanal makineyi gruplandırmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="06eea-117">To provide redundancy tooyour application, we recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="06eea-118">Bu yapılandırma ya da bir planlı veya plansız bir bakım olayı sırasında en az bir sanal makine kullanılabilir ve Azure sanal makinesi SLA karşılıyor hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="06eea-118">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine is available and meets hello Azure virtual machine SLA.</span></span> <span data-ttu-id="06eea-119">Bir sanal makine veya toouse var olan bir sanal makine ve tooadd ya da toocreate seçebilirsiniz, toohello kullanılabilirlik kümesi.</span><span class="sxs-lookup"><span data-stu-id="06eea-119">You can choose either toocreate a virtual machine or toouse an existing virtual machine, and tooadd it toohello availability set.</span></span>  

![Advisor öneri: bir veya daha fazla sanal makineleri toothis kullanılabilirlik kümesi Ekle](./media/advisor-high-availability-recommendations/advisor-high-availability-add-vm-to-availability-set.png)


## <a name="ensure-application-gateway-fault-tolerance"></a><span data-ttu-id="06eea-121">Uygulama ağ geçidi hataya dayanıklılık sağlamak</span><span class="sxs-lookup"><span data-stu-id="06eea-121">Ensure application gateway fault tolerance</span></span>
<span data-ttu-id="06eea-122">Uygulama ağ geçidi tarafından desteklenen kritik uygulamaların tooensure hello iş sürekliliği, Advisor hataya dayanıklılık için yapılandırılmamış uygulama ağ geçidi örnekleri tanımlar ve yapabileceğiniz düzeltme eylemleri önerir .</span><span class="sxs-lookup"><span data-stu-id="06eea-122">tooensure hello business continuity of mission-critical applications that are powered by application gateways, Advisor identifies application gateway instances that are not configured for fault tolerance, and it suggests remediation actions that you can take.</span></span> <span data-ttu-id="06eea-123">Orta veya büyük tek örnekli uygulama ağ geçitleri Danışmanı tanımlar ve en az bir daha fazla örneğini eklemede önerir.</span><span class="sxs-lookup"><span data-stu-id="06eea-123">Advisor identifies medium or large single-instance application gateways, and it recommends adding at least one more instance.</span></span> <span data-ttu-id="06eea-124">Ayrıca, tek veya birden çok instance küçük uygulama ağ geçitleri tanımlar ve geçirme toomedium veya büyük SKU'ları önerir.</span><span class="sxs-lookup"><span data-stu-id="06eea-124">It also identifies single- or multi-instance small application gateways and recommends migrating toomedium or large SKUs.</span></span> <span data-ttu-id="06eea-125">Advisor, uygulama ağ geçidi örnekleri yapılandırılmış toosatisfy hello bu kaynaklar için geçerli SLA gereksinimleri olan bu eylemleri tooensure önerir.</span><span class="sxs-lookup"><span data-stu-id="06eea-125">Advisor recommends these actions tooensure that your application gateway instances are configured toosatisfy hello current SLA requirements for these resources.</span></span>

![Advisor öneri: iki veya daha fazla Orta veya büyük boyutlu uygulama ağ geçidi örnekleri dağıtma](./media/advisor-high-availability-recommendations/advisor-high-availability-application-gateway.png)

## <a name="improve-hello-performance-and-reliability-of-virtual-machine-disks"></a><span data-ttu-id="06eea-127">Merhaba performans ve sanal makine disklerini güvenilirliğini artırmak</span><span class="sxs-lookup"><span data-stu-id="06eea-127">Improve hello performance and reliability of virtual machine disks</span></span>

<span data-ttu-id="06eea-128">Advisor standart diskler ile sanal makineleri tanımlar ve toopremium diskleri yükseltme önerir.</span><span class="sxs-lookup"><span data-stu-id="06eea-128">Advisor identifies virtual machines with standard disks and recommends upgrading toopremium disks.</span></span>
 
<span data-ttu-id="06eea-129">Azure Premium depolama g/Ç kullanımı yoğun iş yükleri çalıştıran sanal makineler için yüksek performanslı, düşük gecikmeli disk desteği sunar.</span><span class="sxs-lookup"><span data-stu-id="06eea-129">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines that run I/O-intensive workloads.</span></span> <span data-ttu-id="06eea-130">Premium depolama hesapları kullanan sanal makine diskler katı hal sürücüleri (SSD) verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="06eea-130">Virtual machine disks that use premium storage accounts store data on solid-state drives (SSDs).</span></span> <span data-ttu-id="06eea-131">Merhaba en iyi performans için uygulamanız için yüksek IOPS toopremium depolama gerektiren herhangi bir sanal makine disklerini geçirmek öneririz.</span><span class="sxs-lookup"><span data-stu-id="06eea-131">For hello best performance for your application, we recommend that you migrate any virtual machine disks requiring high IOPS toopremium storage.</span></span> 

<span data-ttu-id="06eea-132">Disklerinizi yüksek IOPS ihtiyacınız yoksa, standart depolama tutarak maliyetleri sınırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06eea-132">If your disks do not require high IOPS, you can limit costs by maintaining them in standard storage.</span></span> <span data-ttu-id="06eea-133">Standart depolama SSD yerine sabit disk sürücülerinin (HDD'ler) üzerinde sanal makine disk verilerini depolar.</span><span class="sxs-lookup"><span data-stu-id="06eea-133">Standard storage stores virtual machine disk data on hard disk drives (HDDs) instead of SSDs.</span></span> <span data-ttu-id="06eea-134">Sanal makine disklerini toopremium disklerinizi toomigrate seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06eea-134">You can choose toomigrate your virtual machine disks toopremium disks.</span></span> <span data-ttu-id="06eea-135">Premium diskleri çoğu sanal makine SKU'ları üzerinde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="06eea-135">Premium disks are supported on most virtual machine SKUs.</span></span> <span data-ttu-id="06eea-136">Toouse premium diskler, isterseniz, ancak bazı durumlarda, tooupgrade, sanal makinenize SKU'ları da gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="06eea-136">However, in some cases, if you want toouse premium disks, you might need tooupgrade your virtual machine SKUs as well.</span></span>

![Advisor öneri: toopremium diskleri yükselterek, sanal makine diskleriniz hello güvenilirliğini geliştirmeye](./media/advisor-high-availability-recommendations/advisor-high-availability-upgrade-to-premium-disks.png)

## <a name="protect-your-virtual-machine-data-from-accidental-deletion"></a><span data-ttu-id="06eea-138">Sanal makine verilerinizi yanlışlıkla silinmeye karşı koru</span><span class="sxs-lookup"><span data-stu-id="06eea-138">Protect your virtual machine data from accidental deletion</span></span>
<span data-ttu-id="06eea-139">Advisor burada yedekleme etkin değil ve yedekleme etkinleştirme önerir sanal makineleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="06eea-139">Advisor identifies virtual machines where backup is not enabled, and it recommends enabling backup.</span></span> <span data-ttu-id="06eea-140">Sanal makine yedekleme ayarı Merhaba, iş açısından kritik verilerin kullanılabilirliğini sağlar ve yanlışlıkla silme veya bozulmasına karşı koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="06eea-140">Setting up virtual machine backup ensures hello availability of your business-critical data and offers protection against accidental deletion or corruption.</span></span>

![Advisor öneri: sanal makine yedekleme tooprotect kritik verilerinizi yapılandırın](./media/advisor-high-availability-recommendations/advisor-high-availability-virtual-machine-backup.png)

## <a name="access-high-availability-recommendations-in-advisor"></a><span data-ttu-id="06eea-142">Advisor erişim yüksek kullanılabilirlik önerileri</span><span class="sxs-lookup"><span data-stu-id="06eea-142">Access high availability recommendations in Advisor</span></span>

1. <span data-ttu-id="06eea-143">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="06eea-143">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="06eea-144">Merhaba sol bölmede **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="06eea-144">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="06eea-145">Hello menü bölmesi altında hizmet **izleme ve Yönetim**, tıklatın **Azure Danışmanı**.</span><span class="sxs-lookup"><span data-stu-id="06eea-145">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="06eea-146">Merhaba Danışmanı Panosu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="06eea-146">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="06eea-147">Hello Danışmanı Panoda hello tıklatın **yüksek kullanılabilirlik** sekmesini tıklatın ve ardından tooreceive önerileri istediğiniz hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="06eea-147">On hello Advisor dashboard, click hello **High Availability** tab, and then select hello subscription for which you want tooreceive recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="06eea-148">tooaccess Advisor önerileri, şunları yapmalısınız ilk *aboneliğinizi kaydetmek* Danışmanı ile.</span><span class="sxs-lookup"><span data-stu-id="06eea-148">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="06eea-149">Bir abonelik kayıtlı olduğunda bir *abonelik sahibi* başlatır hello Danışmanı Pano ve tıklama hello **alma önerileri** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="06eea-149">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="06eea-150">Bu bir *tek seferlik işlem*.</span><span class="sxs-lookup"><span data-stu-id="06eea-150">This is a *one-time operation*.</span></span> <span data-ttu-id="06eea-151">Merhaba abonelik kaydedildikten sonra Advisor önerileri olarak erişebilir *sahibi*, *katkıda bulunan*, veya *okuyucu* abonelik, bir kaynak grubu için veya bir belirli kaynak.</span><span class="sxs-lookup"><span data-stu-id="06eea-151">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06eea-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="06eea-152">Next steps</span></span>

<span data-ttu-id="06eea-153">Advisor önerileri hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="06eea-153">For more information about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="06eea-154">Giriş tooAzure Danışmanı</span><span class="sxs-lookup"><span data-stu-id="06eea-154">Introduction tooAzure Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="06eea-155">Danışman’ı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="06eea-155">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="06eea-156">Advisor maliyet önerileri</span><span class="sxs-lookup"><span data-stu-id="06eea-156">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="06eea-157">Advisor performans önerileri</span><span class="sxs-lookup"><span data-stu-id="06eea-157">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="06eea-158">Advisor güvenlik önerileri</span><span class="sxs-lookup"><span data-stu-id="06eea-158">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)

