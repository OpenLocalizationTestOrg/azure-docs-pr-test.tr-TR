---
title: "aaaAuto hello Klasik Portalı'nda bir bulut hizmeti ölçeklendirin | Microsoft Docs"
description: "(Klasik) Nasıl toouse hello Klasik portal tooconfigure otomatik ölçek kuralı için bir bulut hizmeti web rolü veya Azure çalışan rolünde öğrenin."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: ddb5816d4d22192c6d2f51d7508e390779742078
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-classic-portal"></a><span data-ttu-id="c67dc-103">Tooconfigure otomatik olarak nasıl hello Klasik Portalı'nda bir bulut hizmeti için ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="c67dc-103">How tooconfigure auto scaling for a Cloud Service in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c67dc-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="c67dc-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="c67dc-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="c67dc-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="c67dc-106">Merhaba ölçek sayfasında hello Klasik Azure portalı, web rolü veya çalışan rolü için otomatik ölçeklendirme ayarlarını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c67dc-106">On hello Scale page of hello Azure classic portal, you can configure automatic scale settings for your web role or worker role.</span></span> <span data-ttu-id="c67dc-107">Alternatif olarak, el ile yerine otomatik ölçeklendirmeyi kural tabanlı ölçeklendirme yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c67dc-107">Alternatively, you can configure manual scaling instead of rules-based automatic scaling.</span></span>

> [!NOTE]
> <span data-ttu-id="c67dc-108">Bu makalede bulut hizmeti web ve çalışan rolleri odaklanır.</span><span class="sxs-lookup"><span data-stu-id="c67dc-108">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="c67dc-109">Bir sanal makine (Klasik) doğrudan oluşturduğunuzda, bir bulut hizmetinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="c67dc-109">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="c67dc-110">Bu bilgilerin bazıları, sanal makinelerin toothese türleri geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="c67dc-110">Some of this information applies toothese types of virtual machines.</span></span> <span data-ttu-id="c67dc-111">Sanal makinelerin bir kullanılabilirlik kümesi ölçeklendirme yalnızca bunları açma ve kapatma yapılandırdığınız hello ölçek kurallara göre kapatılıyor.</span><span class="sxs-lookup"><span data-stu-id="c67dc-111">Scaling an availability set of virtual machines is just shutting them on and off based on hello scale rules you configure.</span></span> <span data-ttu-id="c67dc-112">Sanal makineler ve kullanılabilirlik kümeleri hakkında daha fazla bilgi için bkz: [Yönet hello sanal makinelerin kullanılabilirliğini](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="c67dc-112">For more information about Virtual Machines and availability sets, see [Manage hello Availability of Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="c67dc-113">Uygulamanız için ölçeklendirme yapılandırmadan önce aşağıdaki bilgilerle hello dikkate almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c67dc-113">You should consider hello following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="c67dc-114">Ölçeklendirme Çekirdek kullanımını etkilenir.</span><span class="sxs-lookup"><span data-stu-id="c67dc-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="c67dc-115">Daha fazla sayıda çekirdek büyük rol örneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="c67dc-115">Larger role instances use more cores.</span></span> <span data-ttu-id="c67dc-116">Aboneliğiniz için çekirdek hello sınırı içinde yalnızca bir uygulama ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c67dc-116">You can scale an application only within hello limit of cores for your subscription.</span></span> <span data-ttu-id="c67dc-117">Örneğin, aboneliğiniz 20 olarak belirlenen çekirdek sınırına sahip söyleyin.</span><span class="sxs-lookup"><span data-stu-id="c67dc-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="c67dc-118">İki orta ölçekli bulut hizmetleriyle (4 çekirdeğe toplamı) bir uygulama çalıştırırsanız hello kalan 16 çekirdek tarafından aboneliğinizde diğer bulut hizmet dağıtımları yalnızca ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c67dc-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by hello remaining 16 cores.</span></span> <span data-ttu-id="c67dc-119">Boyutları hakkında daha fazla bilgi için bkz: [bulut hizmeti boyutları](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="c67dc-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="c67dc-120">Bir kuyruk oluşturun ve bir ileti eşiğine dayalı bir uygulama ölçeklendirebilirsiniz önce bir rolü ile ilişkilendir.</span><span class="sxs-lookup"><span data-stu-id="c67dc-120">You must create a queue and associate it with a role before you can scale an application based on a message threshold.</span></span> <span data-ttu-id="c67dc-121">Daha fazla bilgi için bkz: [nasıl toouse hello kuyruk depolama hizmeti](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="c67dc-121">For more information, see [How toouse hello Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="c67dc-122">Bağlantılı tooyour olan kaynaklar ölçeklendirebilirsiniz bulut hizmeti.</span><span class="sxs-lookup"><span data-stu-id="c67dc-122">You can scale resources that are linked tooyour cloud service.</span></span> <span data-ttu-id="c67dc-123">Kaynakları bağlama hakkında daha fazla bilgi için bkz: [nasıl yapılır: bir kaynak tooa bulut hizmeti bağlantı](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="c67dc-123">For more information about linking resources, see [How to: Link a resource tooa cloud service](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span></span>

* <span data-ttu-id="c67dc-124">Uygulamanızın tooenable yüksek kullanılabilirlik, iki veya daha fazla rol örneği ile dağıtılır emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="c67dc-124">tooenable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="c67dc-125">Daha fazla bilgi için bkz: [hizmet düzeyi sözleşmeleri](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="c67dc-125">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="schedule-scaling"></a><span data-ttu-id="c67dc-126">Zamanlama ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="c67dc-126">Schedule scaling</span></span>
<span data-ttu-id="c67dc-127">Varsayılan olarak, tüm rolleri belirli bir zamanlama izlemeyin.</span><span class="sxs-lookup"><span data-stu-id="c67dc-127">By default, all roles do not follow a specific schedule.</span></span> <span data-ttu-id="c67dc-128">Bu nedenle, değiştirilen tüm ayarlar tooall kez ve hello yıl boyunca her gün uygulanır.</span><span class="sxs-lookup"><span data-stu-id="c67dc-128">Therefore, any settings changed apply tooall times and all days throughout hello year.</span></span> <span data-ttu-id="c67dc-129">İsterseniz, el ile veya otomatik modları aşağıdaki hello biri için ölçeklendirme ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c67dc-129">If you want, you can setup manual or automatic scaling for one of hello following modes:</span></span>

* <span data-ttu-id="c67dc-130">Haftanın günü</span><span class="sxs-lookup"><span data-stu-id="c67dc-130">Weekdays</span></span>
* <span data-ttu-id="c67dc-131">Hafta sonları</span><span class="sxs-lookup"><span data-stu-id="c67dc-131">Weekends</span></span>
* <span data-ttu-id="c67dc-132">Hafta gece</span><span class="sxs-lookup"><span data-stu-id="c67dc-132">Week nights</span></span>
* <span data-ttu-id="c67dc-133">Hafta mornings</span><span class="sxs-lookup"><span data-stu-id="c67dc-133">Week mornings</span></span>
* <span data-ttu-id="c67dc-134">Belirli tarihleri</span><span class="sxs-lookup"><span data-stu-id="c67dc-134">Specific dates</span></span>
* <span data-ttu-id="c67dc-135">Belirli bir tarih aralığı</span><span class="sxs-lookup"><span data-stu-id="c67dc-135">Specific date ranges</span></span>

<span data-ttu-id="c67dc-136">Merhaba zamanlama ayarı hello yapılandırılmış [Klasik Azure portalı](https://manage.windowsazure.com/) hello üzerinde</span><span class="sxs-lookup"><span data-stu-id="c67dc-136">hello schedule setting is configured in hello [Azure classic portal](https://manage.windowsazure.com/) on hello</span></span>  
<span data-ttu-id="c67dc-137">**Bulut Hizmetleri** > **\[bulut hizmetiniz\]** > **ölçek**  >   **\[Üretim ve hazırlama\]**  sayfası.</span><span class="sxs-lookup"><span data-stu-id="c67dc-137">**Cloud Services** > **\[Your cloud service\]** > **Scale** > **\[Production or Staging\]** page.</span></span>

<span data-ttu-id="c67dc-138">Merhaba tıklatın **zamanlama süreleri ayarlamanız** düğmesini toochange istediğiniz her rol için.</span><span class="sxs-lookup"><span data-stu-id="c67dc-138">Click hello **set up schedule times** button for each role you want toochange.</span></span>

![Bulut hizmeti bir zamanlamaya göre otomatik ölçeklendirme][scale_schedules]

## <a name="manual-scale"></a><span data-ttu-id="c67dc-140">El ile ölçek</span><span class="sxs-lookup"><span data-stu-id="c67dc-140">Manual scale</span></span>
<span data-ttu-id="c67dc-141">Merhaba üzerinde **ölçek** sayfasında, el ile artırabilir veya örnekleri bir bulut hizmetinde çalışan sayısı hello azaltın.</span><span class="sxs-lookup"><span data-stu-id="c67dc-141">On hello **Scale** page, you can manually increase or decrease hello number of running instances in a cloud service.</span></span> <span data-ttu-id="c67dc-142">Bir zamanlama oluşturmadıysanız, bu ayar her oluşturduğunuz zamanlamayı veya tooall zaman için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="c67dc-142">This setting is configured for each schedule you've created or tooall time if you have not created a schedule.</span></span>

1. <span data-ttu-id="c67dc-143">Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com/), tıklatın **bulut Hizmetleri**ve ardından hello bulut hizmeti tooopen hello Panosu hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c67dc-143">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="c67dc-144">Bulut hizmetinizi görmüyorsanız, gelen toochange gerekebilir **üretim** çok**hazırlama** veya tam tersi.</span><span class="sxs-lookup"><span data-stu-id="c67dc-144">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="c67dc-145">Tıklatın **ölçek**.</span><span class="sxs-lookup"><span data-stu-id="c67dc-145">Click **Scale**.</span></span>
3. <span data-ttu-id="c67dc-146">Ölçeklendirme seçenekleri için toochange istediğiniz hello zamanlamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="c67dc-146">Select hello schedule you want toochange scaling options for.</span></span> <span data-ttu-id="c67dc-147">*Hayır programlanan zamanlarda* tanımlı bir zamanlama varsa hello varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="c67dc-147">*No scheduled times* is hello default if you have no schedules defined.</span></span>
4. <span data-ttu-id="c67dc-148">Hello bulur **ölçek ölçüm tarafından** bölümünde ve seçin **NONE**.</span><span class="sxs-lookup"><span data-stu-id="c67dc-148">Find hello **Scale by metric** section and select **NONE**.</span></span> <span data-ttu-id="c67dc-149">Bu ayar, tüm rolleri hello varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="c67dc-149">This setting is hello default for all roles.</span></span>
5. <span data-ttu-id="c67dc-150">Merhaba bulut hizmetindeki her rol örnekleri toouse hello sayısını değiştirmek için kaydırıcıyı sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c67dc-150">Each role in hello cloud service has a slider for changing hello number of instances toouse.</span></span>
   
    ![Bir bulut hizmet rolü elle ölçeklendirme][manual_scale]
   
    <span data-ttu-id="c67dc-152">Daha fazla örnekleri gerekiyorsa, toochange hello gerekebilir [bulut hizmeti sanal makine boyutu](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="c67dc-152">If you need more instances, you may need toochange hello [cloud service virtual machine size](cloud-services-sizes-specs.md).</span></span>
6. <span data-ttu-id="c67dc-153">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c67dc-153">Click **Save**.</span></span>  
   <span data-ttu-id="c67dc-154">Rol örnekleri eklenir veya seçimlerinizi tabanlı kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="c67dc-154">Role instances are added or removed based on your selections.</span></span>

> [!TIP]
> <span data-ttu-id="c67dc-155">Her gördüğünüz ![][tip_icon] fare tooit taşıyın ve hangi belirli bir ayarı yaptığı hakkında Yardım alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c67dc-155">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---cpu"></a><span data-ttu-id="c67dc-156">Otomatik ölçek - CPU</span><span class="sxs-lookup"><span data-stu-id="c67dc-156">Automatic scale - CPU</span></span>
<span data-ttu-id="c67dc-157">Merhaba ortalama CPU kullanım yüzdesini üstünde veya altında belirtilen eşikler kalırsa Bu mod ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="c67dc-157">This mode scales if hello average percentage of CPU usage goes above or below specified thresholds.</span></span> <span data-ttu-id="c67dc-158">Rol örnekleri oluşturulur veya böyle bir durumda silindi.</span><span class="sxs-lookup"><span data-stu-id="c67dc-158">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="c67dc-159">Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com/), tıklatın **bulut Hizmetleri**ve ardından hello bulut hizmeti tooopen hello Panosu hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c67dc-159">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="c67dc-160">Bulut hizmetinizi görmüyorsanız, gelen toochange gerekebilir **üretim** çok**hazırlama** veya tam tersi.</span><span class="sxs-lookup"><span data-stu-id="c67dc-160">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="c67dc-161">Tıklatın **ölçek**.</span><span class="sxs-lookup"><span data-stu-id="c67dc-161">Click **Scale**.</span></span>
3. <span data-ttu-id="c67dc-162">Ölçeklendirme seçenekleri için toochange istediğiniz hello zamanlamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="c67dc-162">Select hello schedule you want toochange scaling options for.</span></span> <span data-ttu-id="c67dc-163">*Hayır programlanan zamanlarda* tanımlı bir zamanlama varsa hello varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="c67dc-163">*No scheduled times* is hello default if you have no schedules defined.</span></span>
4. <span data-ttu-id="c67dc-164">Hello bulur **ölçek ölçüm tarafından** bölümünde ve seçin **CPU**.</span><span class="sxs-lookup"><span data-stu-id="c67dc-164">Find hello **Scale by metric** section and select **CPU**.</span></span>
5. <span data-ttu-id="c67dc-165">Artık rol örnekleri, hello hedef CPU kullanımı (ölçek büyütme bir tootrigger) ve kaç tane tooscale yukarı ve aşağı tarafından örnekleri minimum ve maksimum aralığını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c67dc-165">Now you can configure a minimum and maximum range of roles instances, hello target CPU usage (tootrigger a scale up), and how many instances tooscale up and down by.</span></span>

![Bir bulut hizmet rolü tarafından cpu yükünü ölçeklendirme][cpu_scale]

> [!TIP]
> <span data-ttu-id="c67dc-167">Her gördüğünüz ![][tip_icon] fare tooit taşıyın ve hangi belirli bir ayarı yaptığı hakkında Yardım alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c67dc-167">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---queue"></a><span data-ttu-id="c67dc-168">Otomatik ölçek - sırası</span><span class="sxs-lookup"><span data-stu-id="c67dc-168">Automatic scale - Queue</span></span>
<span data-ttu-id="c67dc-169">Sıradaki iletileri Hello sayısı üzerinde veya belirtilen eşiğin altında kalırsa bu modu otomatik olarak ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="c67dc-169">This mode automatically scales if hello number of messages in a queue goes above or below a specified threshold.</span></span> <span data-ttu-id="c67dc-170">Rol örnekleri oluşturulur veya böyle bir durumda silindi.</span><span class="sxs-lookup"><span data-stu-id="c67dc-170">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="c67dc-171">Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com/), tıklatın **bulut Hizmetleri**ve ardından hello bulut hizmeti tooopen hello Panosu hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c67dc-171">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="c67dc-172">Bulut hizmetinizi görmüyorsanız, gelen toochange gerekebilir **üretim** çok**hazırlama** veya tam tersi.</span><span class="sxs-lookup"><span data-stu-id="c67dc-172">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="c67dc-173">Tıklatın **ölçek**.</span><span class="sxs-lookup"><span data-stu-id="c67dc-173">Click **Scale**.</span></span>
3. <span data-ttu-id="c67dc-174">Hello bulur **ölçek ölçüm tarafından** bölümünde ve seçin **SIRA**.</span><span class="sxs-lookup"><span data-stu-id="c67dc-174">Find hello **Scale by metric** section and select **QUEUE**.</span></span>
4. <span data-ttu-id="c67dc-175">Artık rol örnekleri, hello kuyruk ve her bir örneği ve tarafından kaç örnekleri tooscale yukarı ve aşağı için kuyruk iletileri tooprocess sayısı minimum ve maksimum aralığını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c67dc-175">Now you can configure a minimum and maximum range of roles instances, hello queue and number of queue messages tooprocess for each instance, and how many instances tooscale up and down by.</span></span>

![İleti sırası tarafından bir bulut hizmet rolü ölçeklendirme][queue_scale]

> [!TIP]
> <span data-ttu-id="c67dc-177">Her gördüğünüz ![][tip_icon] fare tooit taşıyın ve hangi belirli bir ayarı yaptığı hakkında Yardım alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c67dc-177">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="scale-linked-resources"></a><span data-ttu-id="c67dc-178">Bağlı kaynaklar ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="c67dc-178">Scale linked resources</span></span>
<span data-ttu-id="c67dc-179">Genellikle bir rolü ölçeklendirdiğinizde Merhaba uygulaması da kullanarak faydalı tooscale hello veritabanı yok.</span><span class="sxs-lookup"><span data-stu-id="c67dc-179">Often when you scale a role, it's beneficial tooscale hello database that hello application is using also.</span></span> <span data-ttu-id="c67dc-180">Merhaba veritabanı toohello bulut hizmeti bağlantı varsa, hello uygun bağlantıyı tıklatarak o kaynağın ayarlarını ölçeklendirme hello erişebilir.</span><span class="sxs-lookup"><span data-stu-id="c67dc-180">If you link hello database toohello cloud service, you can access hello scaling settings for that resource by clicking hello appropriate link.</span></span>

1. <span data-ttu-id="c67dc-181">Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com/), tıklatın **bulut Hizmetleri**ve ardından hello bulut hizmeti tooopen hello Panosu hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c67dc-181">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="c67dc-182">Bulut hizmetinizi görmüyorsanız, gelen toochange gerekebilir **üretim** çok**hazırlama** veya tam tersi.</span><span class="sxs-lookup"><span data-stu-id="c67dc-182">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="c67dc-183">Tıklatın **ölçek**.</span><span class="sxs-lookup"><span data-stu-id="c67dc-183">Click **Scale**.</span></span>
3. <span data-ttu-id="c67dc-184">Hello bulur **bağlı kaynakları** 'ye tıklayın **bu veritabanı için ölçek yönetmek**.</span><span class="sxs-lookup"><span data-stu-id="c67dc-184">Find hello **linked resources** section and click **Manage scale for this database**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c67dc-185">Görmüyorsanız, bir **bağlı kaynakları** bölümünde, büyük olasılıkla herhangi bağlı kaynaklar yok.</span><span class="sxs-lookup"><span data-stu-id="c67dc-185">If you don't see a **linked resources** section, you probably do not have any linked resources.</span></span>

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
