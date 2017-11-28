---
title: "aaaAuto hello Portalı'nda bir bulut hizmeti ölçeklendirin | Microsoft Docs"
description: "Nasıl toouse hello portal tooconfigure otomatik ölçek kuralı için bir bulut hizmeti web rolü veya Azure çalışan rolünde öğrenin."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 701d4404-5cc0-454b-999c-feb94c1685c0
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 265f4c8ec5e1ec2f85585df25f18cd0d0c9946a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-portal"></a><span data-ttu-id="fd2d8-103">Tooconfigure otomatik olarak nasıl hello portalında bulut hizmeti için ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="fd2d8-103">How tooconfigure auto scaling for a Cloud Service in hello portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd2d8-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="fd2d8-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="fd2d8-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="fd2d8-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="fd2d8-106">Koşullar bir ölçekte veya işlemi uzaklaştırma tetikleyen bir bulut hizmeti çalışan rolü için ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-106">Conditions can be set for a cloud service worker role that trigger a scale in or out operation.</span></span> <span data-ttu-id="fd2d8-107">Merhaba rol Hello koşullarını hello CPU, disk veya ağ yükü hello rolünün temel alabilir.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-107">hello conditions for hello role can be based on hello CPU, disk, or network load of hello role.</span></span> <span data-ttu-id="fd2d8-108">Ayrıca, aboneliğinizle ilişkilendirilmiş diğer bazı Azure kaynak ileti sırası veya hello ölçüsü dayalı bir koşul ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-108">You can also set a condition based on a message queue or hello metric of some other Azure resource associated with your subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="fd2d8-109">Bu makalede bulut hizmeti web ve çalışan rolleri odaklanır.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-109">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="fd2d8-110">Bir sanal makine (Klasik) doğrudan oluşturduğunuzda, bir bulut hizmetinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-110">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="fd2d8-111">Standart bir sanal makine ile ilişkilendirerek ölçeklenebilen bir [kullanılabilirlik kümesi](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) ve bunları el ile açın veya kapatın.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-111">You can scale a standard virtual machine by associating it with an [availability set](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and manually turn them on or off.</span></span>

## <a name="considerations"></a><span data-ttu-id="fd2d8-112">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="fd2d8-112">Considerations</span></span>
<span data-ttu-id="fd2d8-113">Uygulamanız için ölçeklendirme yapılandırmadan önce aşağıdaki bilgilerle hello dikkate almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="fd2d8-113">You should consider hello following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="fd2d8-114">Ölçeklendirme Çekirdek kullanımını etkilenir.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="fd2d8-115">Daha fazla sayıda çekirdek büyük rol örneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-115">Larger role instances use more cores.</span></span> <span data-ttu-id="fd2d8-116">Aboneliğiniz için çekirdek hello sınırı içinde yalnızca bir uygulama ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-116">You can scale an application only within hello limit of cores for your subscription.</span></span> <span data-ttu-id="fd2d8-117">Örneğin, aboneliğiniz 20 olarak belirlenen çekirdek sınırına sahip söyleyin.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="fd2d8-118">İki orta ölçekli bulut hizmetleriyle (4 çekirdeğe toplamı) bir uygulama çalıştırırsanız hello kalan 16 çekirdek tarafından aboneliğinizde diğer bulut hizmet dağıtımları yalnızca ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by hello remaining 16 cores.</span></span> <span data-ttu-id="fd2d8-119">Boyutları hakkında daha fazla bilgi için bkz: [bulut hizmeti boyutları](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="fd2d8-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="fd2d8-120">Ölçeklendirmek bir kuyruk iletisi eşiğine dayalı.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-120">You can scale based on a queue message threshold.</span></span> <span data-ttu-id="fd2d8-121">Hakkında daha fazla bilgi için bkz: toouse sıraları [nasıl toouse hello kuyruk depolama hizmeti](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="fd2d8-121">For more information about how toouse queues, see [How toouse hello Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="fd2d8-122">Ayrıca, aboneliğinizle ilişkilendirilmiş diğer kaynakları ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-122">You can also scale other resources associated with your subscription.</span></span>

* <span data-ttu-id="fd2d8-123">Uygulamanızın tooenable yüksek kullanılabilirlik, iki veya daha fazla rol örneği ile dağıtılır emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-123">tooenable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="fd2d8-124">Daha fazla bilgi için bkz: [hizmet düzeyi sözleşmeleri](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="fd2d8-124">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>


## <a name="where-scale-is-located"></a><span data-ttu-id="fd2d8-125">Ölçek bulunduğu</span><span class="sxs-lookup"><span data-stu-id="fd2d8-125">Where scale is located</span></span>
<span data-ttu-id="fd2d8-126">Bulut hizmeti seçtikten sonra hello bulut hizmeti dikey görünür olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-126">After you select your cloud service, you should have hello cloud service blade visible.</span></span>

1. <span data-ttu-id="fd2d8-127">Merhaba üzerinde hello bulut hizmeti dikey **roller ve örnekler** kutucuğu, hello bulut hizmeti seçin hello adı.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-127">On hello cloud service blade, on hello **Roles and Instances** tile, select hello name of hello cloud service.</span></span>   
   <span data-ttu-id="fd2d8-128">**Önemli**: hizmet rolü, hello rolü rol örneği hello değil emin tooclick hello bulut olun.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-128">**IMPORTANT**: Make sure tooclick hello cloud service role, not hello role instance that is below hello role.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. <span data-ttu-id="fd2d8-129">Select hello **ölçek** döşeme.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-129">Select hello **scale** tile.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a><span data-ttu-id="fd2d8-130">Otomatik ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="fd2d8-130">Automatic scale</span></span>
<span data-ttu-id="fd2d8-131">Bir rol için ölçek ayarları ya da iki modlarıyla yapılandırabilirsiniz **el ile** veya **otomatik**.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-131">You can configure scale settings for a role with either two modes **manual** or **automatic**.</span></span> <span data-ttu-id="fd2d8-132">Beklediğiniz gibi el ile hello mutlak örneklerinin sayısını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-132">Manual is as you would expect, you set hello absolute count of instances.</span></span> <span data-ttu-id="fd2d8-133">Otomatik ancak nasıl ve nasıl tarafından çok yöneten kuralları ölçeklendirmeniz gerekir tooset sağlar.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-133">Automatic however allows you tooset rules that govern how and by how much you should scale.</span></span>

<span data-ttu-id="fd2d8-134">Set hello **göre Ölçeklendirmeniz** çok seçenek**zamanlama ve performans kuralları**.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-134">Set hello **Scale by** option too**schedule and performance rules**.</span></span>

![Bulut Hizmetleri ölçek ayarları profili ve kural](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. <span data-ttu-id="fd2d8-136">Varolan bir profili.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-136">An existing profile.</span></span>
2. <span data-ttu-id="fd2d8-137">Merhaba üst profil için bir kural ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-137">Add a rule for hello parent profile.</span></span>
3. <span data-ttu-id="fd2d8-138">Başka bir profili ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-138">Add another profile.</span></span>

<span data-ttu-id="fd2d8-139">Seçin **profili eklemek**.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-139">Select **Add Profile**.</span></span> <span data-ttu-id="fd2d8-140">Hello profil belirler hangi modu için hello ölçek toouse istediğiniz: **her zaman**, **yineleme**, **sabit tarihi**.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-140">hello profile determines which mode you want toouse for hello scale: **always**, **recurrence**, **fixed date**.</span></span>

<span data-ttu-id="fd2d8-141">Hello profili ve kuralları yapılandırdıktan sonra hello seçin **kaydetmek** hello üst simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-141">After you have configured hello profile and rules, select hello **Save** icon at hello top.</span></span>

#### <a name="profile"></a><span data-ttu-id="fd2d8-142">Profil</span><span class="sxs-lookup"><span data-stu-id="fd2d8-142">Profile</span></span>
<span data-ttu-id="fd2d8-143">Hello profil minimum ayarlar hello için en fazla örnek ölçeklendirme ve ayrıca bu ölçek aralığı etkin olduğunda.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-143">hello profile sets minimum and maximum instances for hello scale, and also when this scale range is active.</span></span>

* <span data-ttu-id="fd2d8-144">**Her zaman**</span><span class="sxs-lookup"><span data-stu-id="fd2d8-144">**Always**</span></span>

    <span data-ttu-id="fd2d8-145">Her zaman bu aralıktaki kullanılabilir örneklerinin tutun.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-145">Always keep this range of instances available.</span></span>  

    ![Her zaman ölçeklendirme bulut hizmeti](./media/cloud-services-how-to-scale-portal/select-always.png)
* <span data-ttu-id="fd2d8-147">**Yineleme**</span><span class="sxs-lookup"><span data-stu-id="fd2d8-147">**Recurrence**</span></span>

    <span data-ttu-id="fd2d8-148">Merhaba hafta tooscale gün kümesi seçin.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-148">Choose a set of days of hello week tooscale.</span></span>

    ![Bulut hizmeti ölçekli bir yineleme zamanlaması](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* <span data-ttu-id="fd2d8-150">**Sabit tarih**</span><span class="sxs-lookup"><span data-stu-id="fd2d8-150">**Fixed Date**</span></span>

    <span data-ttu-id="fd2d8-151">Bir sabit tarih aralığı tooscale hello rolü.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-151">A fixed date range tooscale hello role.</span></span>

    ![Bulut hizmeti ölçekli sabit tarih](./media/cloud-services-how-to-scale-portal/select-fixed.png)

<span data-ttu-id="fd2d8-153">Hello profil yapılandırdıktan sonra hello seçin **Tamam** hello profili dikey penceresi hello sonundaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-153">After you have configured hello profile, select hello **OK** button at hello bottom of hello profile blade.</span></span>

#### <a name="rule"></a><span data-ttu-id="fd2d8-154">Kural</span><span class="sxs-lookup"><span data-stu-id="fd2d8-154">Rule</span></span>
<span data-ttu-id="fd2d8-155">Kuralları tooa profile eklenir ve hello ölçek tetikleyen bir koşul temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-155">Rules are added tooa profile and represent a condition that triggers hello scale.</span></span>

<span data-ttu-id="fd2d8-156">Merhaba kural tetikleyici hello bulut hizmeti (CPU kullanımı, disk etkinliği veya ağ etkinliği) ölçüsü üzerinde temel toowhich koşullu bir değer ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-156">hello rule trigger is based on a metric of hello cloud service (CPU usage, disk activity, or network activity) toowhich you can add a conditional value.</span></span> <span data-ttu-id="fd2d8-157">Ayrıca, aboneliğinizle ilişkilendirilmiş diğer bazı Azure kaynak ileti sırası veya hello ölçüsü göre hello tetikleyici olabilir.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-157">Additionally you can have hello trigger based on a message queue or hello metric of some other Azure resource associated with your subscription.</span></span>

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

<span data-ttu-id="fd2d8-158">Hello kuralını yapılandırdıktan sonra hello seçin **Tamam** hello kural dikey penceresinde hello sonundaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-158">After you have configured hello rule, select hello **OK** button at hello bottom of hello rule blade.</span></span>

## <a name="back-toomanual-scale"></a><span data-ttu-id="fd2d8-159">Geri toomanual ölçek</span><span class="sxs-lookup"><span data-stu-id="fd2d8-159">Back toomanual scale</span></span>
<span data-ttu-id="fd2d8-160">Toohello gidin [ölçek ayarı](#where-scale-is-located) ve kümesi hello **göre Ölçeklendirmeniz** çok seçenek**el ile girdiğim bir örnek sayısı**.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-160">Navigate toohello [scale settings](#where-scale-is-located) and set hello **Scale by** option too**an instance count that I enter manually**.</span></span>

![Bulut Hizmetleri ölçek ayarları profili ve kural](./media/cloud-services-how-to-scale-portal/manual-basics.png)

<span data-ttu-id="fd2d8-162">Bu ayar otomatik ölçeklendirme hello rolden kaldırır ve ardından hello örnek sayısı doğrudan ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-162">This setting removes automated scaling from hello role and then you can set hello instance count directly.</span></span>

1. <span data-ttu-id="fd2d8-163">Merhaba Ölçek (el ile veya otomatik) seçeneği.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-163">hello scale (manual or automated) option.</span></span>
2. <span data-ttu-id="fd2d8-164">Bir rol örneği kaydırıcı tooset hello örnekleri tooscale için.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-164">A role instance slider tooset hello instances tooscale to.</span></span>
3. <span data-ttu-id="fd2d8-165">Merhaba rol tooscale örnekleri.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-165">Instances of hello role tooscale to.</span></span>

<span data-ttu-id="fd2d8-166">Merhaba ölçek ayarlarını yapılandırdıktan sonra hello seçin **kaydetmek** hello üst simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fd2d8-166">After you have configured hello scale settings, select hello **Save** icon at hello top.</span></span>
