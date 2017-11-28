---
title: "aaaCommon bulut hizmeti yönetim görevleri | Microsoft Docs"
description: "Toomanage bulut hello Azure portal hizmetleri nasıl öğrenin. Bu örnekler hello Azure portalını kullanın."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: cb218ad9-77d4-4149-83db-71159c00767e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: ade8a18a7754edbaae4903230c26c009fef63ed7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-cloud-services"></a><span data-ttu-id="2d352-104">TooManage Cloud Services nasıl</span><span class="sxs-lookup"><span data-stu-id="2d352-104">How tooManage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2d352-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="2d352-105">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="2d352-106">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="2d352-106">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="2d352-107">Merhaba, **bulut Hizmetleri (Klasik)** alanı hello Azure portal, hizmet rolü veya bir dağıtım güncelleştirmek, aşamalı dağıtım tooproduction yükseltmek, yapabilirsiniz hello kaynak görebilmeniz için kaynakları tooyour bulut hizmeti bağlantı Bağımlılıklar ve ölçek kaynakları birlikte hello ve bir bulut hizmeti veya bir dağıtımı silin.</span><span class="sxs-lookup"><span data-stu-id="2d352-107">In hello **Cloud Services (classic)** area of hello Azure portal, you can update a service role or a deployment, promote a staged deployment tooproduction, link resources tooyour cloud service so that you can see hello resource dependencies and scale hello resources together, and delete a cloud service or a deployment.</span></span>

<span data-ttu-id="2d352-108">Nasıl tooscale bulut hizmetiniz kullanılabilir olduğu hakkında daha fazla bilgi [burada](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2d352-108">More information about how tooscale your cloud service is available [here](cloud-services-how-to-scale-portal.md).</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="2d352-109">Nasıl yapılır: bir bulut hizmet rolü veya dağıtım güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="2d352-109">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="2d352-110">Bulut hizmetiniz için tooupdate hello uygulama kodu gerekiyorsa kullanın **güncelleştirme** hello bulut hizmeti dikey.</span><span class="sxs-lookup"><span data-stu-id="2d352-110">If you need tooupdate hello application code for your cloud service, use **Update** on hello cloud service blade.</span></span> <span data-ttu-id="2d352-111">Tek bir rol veya tüm rolleri güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d352-111">You can update a single role or all roles.</span></span> <span data-ttu-id="2d352-112">tooupdate, yeni hizmet paketi ya da hizmet yapılandırma dosyasını karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d352-112">tooupdate, you can upload a new service package or service configuration file.</span></span>

1. <span data-ttu-id="2d352-113">Merhaba, [Azure portal][Azure portal], tooupdate istediğiniz hello bulut hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="2d352-113">In hello [Azure portal][Azure portal], select hello cloud service you want tooupdate.</span></span> <span data-ttu-id="2d352-114">Bu adım hello bulut hizmeti örneği dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="2d352-114">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="2d352-115">Merhaba dikey penceresinde hello tıklayın **güncelleştirme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2d352-115">In hello blade, click hello **Update** button.</span></span>

    ![Güncelleştir düğmesi](./media/cloud-services-how-to-manage-portal/update-button.png)

3. <span data-ttu-id="2d352-117">Merhaba dağıtım yeni hizmet paketi dosyasının (.cspkg) ve hizmet yapılandırma dosyasının (.cscfg) ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="2d352-117">Update hello deployment with a new service package file (.cspkg) and service configuration file (.cscfg).</span></span>

    ![UpdateDeployment](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. <span data-ttu-id="2d352-119">**İsteğe bağlı olarak** hello dağıtım etiketi ve hello depolama hesabı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="2d352-119">**Optionally** update hello deployment label and hello storage account.</span></span>
5. <span data-ttu-id="2d352-120">Herhangi bir rolü yalnızca bir rol örneği varsa, hello seçin **bir veya daha fazla rol tek bir örnek içeriyorsa bile Dağıt** tooenable hello yükseltme tooproceed.</span><span class="sxs-lookup"><span data-stu-id="2d352-120">If any roles have only one role instance, select hello **Deploy even if one or more roles contain a single instance** tooenable hello upgrade tooproceed.</span></span>

    <span data-ttu-id="2d352-121">Her role en az iki rol örnekleri (sanal makineler) varsa azure yalnızca 99,95 yüzde hizmet kullanılabilirliği bir bulut hizmet güncelleştirmesi sırasında garanti edebilir.</span><span class="sxs-lookup"><span data-stu-id="2d352-121">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="2d352-122">Merhaba diğer güncelleştirilirken iki rol örneği ile bir sanal makine istemci isteklerini işler.</span><span class="sxs-lookup"><span data-stu-id="2d352-122">With two role instances, one virtual machine processes client requests while hello other is updated.</span></span>

6. <span data-ttu-id="2d352-123">Denetleme **Başlat dağıtım** toohave hello güncelleştirme hello paketinin hello karşıya yükleme tamamlandıktan sonra uygulanır.</span><span class="sxs-lookup"><span data-stu-id="2d352-123">Check **Start deployment** toohave hello update applied after hello upload of hello package has finished.</span></span>
7. <span data-ttu-id="2d352-124">Tıklatın **Tamam** hello hizmeti güncelleştirme toobegin.</span><span class="sxs-lookup"><span data-stu-id="2d352-124">Click **OK** toobegin updating hello service.</span></span>

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a><span data-ttu-id="2d352-125">Nasıl yapılır: bir aşamalı dağıtım tooproduction dağıtımları toopromote değiştirme</span><span class="sxs-lookup"><span data-stu-id="2d352-125">How to: Swap deployments toopromote a staged deployment tooproduction</span></span>
<span data-ttu-id="2d352-126">Ne zaman toodeploy yeni sürümde bir bulut hizmeti, aşama karar verin ve yeni sürüm, bulut hizmeti hazırlama ortamınızda sınayın.</span><span class="sxs-lookup"><span data-stu-id="2d352-126">When you decide toodeploy a new release of a cloud service, stage and test your new release in your cloud service staging environment.</span></span> <span data-ttu-id="2d352-127">Kullanım **takas** hangi hello iki dağıtım giderilmesini ve yeni bir sürüm tooproduction Yükselt tooswitch hello URL'leri.</span><span class="sxs-lookup"><span data-stu-id="2d352-127">Use **Swap** tooswitch hello URLs by which hello two deployments are addressed and promote a new release tooproduction.</span></span>

<span data-ttu-id="2d352-128">Merhaba dağıtımlarından takas **bulut Hizmetleri** sayfa veya hello Pano.</span><span class="sxs-lookup"><span data-stu-id="2d352-128">You can swap deployments from hello **Cloud Services** page or hello dashboard.</span></span>

1. <span data-ttu-id="2d352-129">Merhaba, [Azure portal][Azure portal], tooupdate istediğiniz hello bulut hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="2d352-129">In hello [Azure portal][Azure portal], select hello cloud service you want tooupdate.</span></span> <span data-ttu-id="2d352-130">Bu adım hello bulut hizmeti örneği dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="2d352-130">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="2d352-131">Merhaba dikey penceresinde hello tıklayın **takas** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2d352-131">In hello blade, click hello **Swap** button.</span></span>

    ![Bulut Hizmetleri değiştirme](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. <span data-ttu-id="2d352-133">Merhaba aşağıdaki onay istemi açılır.</span><span class="sxs-lookup"><span data-stu-id="2d352-133">hello following confirmation prompt opens.</span></span>

    ![Bulut Hizmetleri değiştirme](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. <span data-ttu-id="2d352-135">Merhaba dağıtım bilgileri doğruladıktan sonra tıklatın **Tamam** tooswap hello dağıtımları.</span><span class="sxs-lookup"><span data-stu-id="2d352-135">After you verify hello deployment information, click **OK** tooswap hello deployments.</span></span>

    <span data-ttu-id="2d352-136">değişiklikleri hello tek şey hello sanal IP adresleri (VIP) olduğundan hello dağıtımı takas hello dağıtımları için hızlı bir şekilde gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="2d352-136">hello deployment swap happens quickly because hello only thing that changes is hello virtual IP addresses (VIPs) for hello deployments.</span></span>

    <span data-ttu-id="2d352-137">toosave işlem maliyetleri, üretim dağıtımınızın beklendiği gibi çalıştığını doğruladıktan sonra dağıtım hazırlama hello silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d352-137">toosave compute costs, you can delete hello staging deployment after you verify that your production deployment is working as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="2d352-138">Dağıtımları değiştirme hakkında sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="2d352-138">Common questions about swapping deployments</span></span>

<span data-ttu-id="2d352-139">**Dağıtımları takas hello Önkoşullar nelerdir?**</span><span class="sxs-lookup"><span data-stu-id="2d352-139">**What are hello prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="2d352-140">Başarılı dağıtım Takas için iki anahtar Önkoşullar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2d352-140">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="2d352-141">İçin üretim yuvası toouse statik bir IP adresi kullanmak isterseniz, bir hazırlama yuvası da ayırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d352-141">If you would like toouse a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="2d352-142">Aksi takdirde hello takas başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="2d352-142">Otherwise, hello swap fails.</span></span>

- <span data-ttu-id="2d352-143">Merhaba takas gerçekleştirmeden önce tüm örneklerini rollerinizi çalıştırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d352-143">All instances of your roles must be running before you can perform hello swap.</span></span> <span data-ttu-id="2d352-144">Merhaba, örneklerini hello genel bakış dikey penceresinde hello Azure portal durumunu kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d352-144">You can check hello status of your instances in hello overview blade of hello Azure portal.</span></span> <span data-ttu-id="2d352-145">Alternatif olarak, hello kullanabilirsiniz [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) Windows PowerShell komutu.</span><span class="sxs-lookup"><span data-stu-id="2d352-145">Alternatively, you can use hello [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) command in Windows PowerShell.</span></span>

<span data-ttu-id="2d352-146">Konuk işletim sistemi güncelleştirmeleri ve hizmet işlemleri düzeltme dağıtım neden olabilir Not toofail değiştirir.</span><span class="sxs-lookup"><span data-stu-id="2d352-146">Note that Guest OS updates and service healing operations can also cause deployment swaps toofail.</span></span> <span data-ttu-id="2d352-147">Daha fazla bilgi için bkz: [bulut hizmeti dağıtım sorunlarını giderme](cloud-services-troubleshoot-deployment-problems.md).</span><span class="sxs-lookup"><span data-stu-id="2d352-147">For more information, see [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md).</span></span>

<span data-ttu-id="2d352-148">**Bir takas Uygulamam için kapalı kalma süresi maliyetine neden olabilir mi? Bunu nasıl işlemesi gerekir?**</span><span class="sxs-lookup"><span data-stu-id="2d352-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="2d352-149">Yalnızca bir yapılandırma değişikliği hello Azure yük dengeleyici içinde olduğundan hello son bölümünde açıklandığı gibi bir dağıtımı takas genellikle hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="2d352-149">As described in hello last section, a deployment swap is typically fast since it is just a configuration change in hello Azure load balancer.</span></span> <span data-ttu-id="2d352-150">Bazı durumlarda, Bununla birlikte, en az on dakika sürer ve geçici bağlantı hatalarına neden.</span><span class="sxs-lookup"><span data-stu-id="2d352-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="2d352-151">toolimit etkisi tooyour müşteriler, göz önünde bulundurun uygulama [istemci yeniden deneme mantığı](../best-practices-retry-general.md).</span><span class="sxs-lookup"><span data-stu-id="2d352-151">toolimit impact tooyour customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-tooa-cloud-service"></a><span data-ttu-id="2d352-152">Nasıl yapılır: bir kaynak tooa bulut hizmetine bağlama</span><span class="sxs-lookup"><span data-stu-id="2d352-152">How to: Link a resource tooa cloud service</span></span>
<span data-ttu-id="2d352-153">Hello Azure portal birlikte hello geçerli Klasik Azure portalı yaptığı gibi kaynakları bağlantı vermiyor.</span><span class="sxs-lookup"><span data-stu-id="2d352-153">hello Azure portal does not link resources together like hello current Azure classic portal does.</span></span> <span data-ttu-id="2d352-154">Bunun yerine, ek kaynaklar toohello dağıtmak hello bulut hizmeti tarafından kullanılan aynı kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="2d352-154">Instead, deploy additional resources toohello same resource group being used by hello Cloud Service.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="2d352-155">Nasıl yapılır: dağıtımları ve bulut hizmeti Sil</span><span class="sxs-lookup"><span data-stu-id="2d352-155">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="2d352-156">Bir bulut hizmeti silebilmek için önce varolan her dağıtım silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d352-156">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="2d352-157">toosave işlem maliyetleri, üretim dağıtımınızın beklendiği gibi çalıştığını doğruladıktan sonra dağıtım hazırlama hello silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d352-157">toosave compute costs, you can delete hello staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="2d352-158">İşlem maliyetleri durdurulur dağıtılan rol örnekleri için faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="2d352-158">You are billed for compute costs for deployed role instances that are stopped.</span></span>

<span data-ttu-id="2d352-159">Aşağıdaki yordam toodelete hello dağıtımı veya Bulut hizmetiniz kullanın.</span><span class="sxs-lookup"><span data-stu-id="2d352-159">Use hello following procedure toodelete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="2d352-160">Merhaba, [Azure portal][Azure portal], toodelete istediğiniz hello bulut hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="2d352-160">In hello [Azure portal][Azure portal], select hello cloud service you want toodelete.</span></span> <span data-ttu-id="2d352-161">Bu adım hello bulut hizmeti örneği dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="2d352-161">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="2d352-162">Merhaba dikey penceresinde hello tıklayın **silmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2d352-162">In hello blade, click hello **Delete** button.</span></span>

    ![Bulut Hizmetleri değiştirme](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. <span data-ttu-id="2d352-164">Denetleyerek hello tüm bulut hizmeti silebilirsiniz **bulut hizmeti ve hizmetin dağıtımları** veya seçin ya da hello **Üretim dağıtımı** veya hello **hazırlama dağıtımı**.</span><span class="sxs-lookup"><span data-stu-id="2d352-164">You can delete hello entire cloud service by checking **Cloud service and its deployments** or choose either hello **Production deployment** or hello **Staging deployment**.</span></span>

    ![Bulut Hizmetleri değiştirme](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. <span data-ttu-id="2d352-166">Merhaba tıklatın **silmek** hello altındaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2d352-166">Click hello **Delete** button at hello bottom.</span></span>
5. <span data-ttu-id="2d352-167">toodelete hello bulut hizmeti tıklatın **Delete bulut hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="2d352-167">toodelete hello cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="2d352-168">Merhaba onay isteminde ardından **Evet**.</span><span class="sxs-lookup"><span data-stu-id="2d352-168">Then, at hello confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="2d352-169">Bir bulut hizmeti silindi ve ayrıntılı izleme yapılandırılmış hello veri depolama hesabınızdan el ile silmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="2d352-169">When a cloud service is deleted, and verbose monitoring is configured, you must delete hello data manually from your storage account.</span></span> <span data-ttu-id="2d352-170">Burada toofind hello ölçümleri tabloları hakkında daha fazla bilgi için bkz: [bu](cloud-services-how-to-monitor.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="2d352-170">For information about where toofind hello metrics tables, see [this](cloud-services-how-to-monitor.md) article.</span></span>


## <a name="how-to-find-more-information-about-failed-deployments"></a><span data-ttu-id="2d352-171">Nasıl yapılır: başarısız dağıtımları hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="2d352-171">How to: Find more information about failed deployments</span></span>
<span data-ttu-id="2d352-172">Merhaba **genel bakış** dikey penceresinde hello üstünde durum çubuğu vardır.</span><span class="sxs-lookup"><span data-stu-id="2d352-172">hello **Overview** blade has a status bar at hello top.</span></span> <span data-ttu-id="2d352-173">Merhaba Çubuğu'nu tıklatın, yeni bir dikey pencere açar ve hata bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2d352-173">When you click hello bar, a new blade opens and displays any error information.</span></span> <span data-ttu-id="2d352-174">Merhaba dağıtım hatalarını içermiyorsa hello bilgi dikey boştur.</span><span class="sxs-lookup"><span data-stu-id="2d352-174">If hello deployment does not contain any errors, hello information blade is blank.</span></span>

![Bulut Hizmetleri değiştirme](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="2d352-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2d352-176">Next steps</span></span>
* <span data-ttu-id="2d352-177">[Genel yapılandırma bulut hizmetinizin](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2d352-177">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="2d352-178">Nasıl çok öğrenin[bir bulut hizmetinin dağıtılacağı](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2d352-178">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="2d352-179">Yapılandırma bir [özel etki alanı adı](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2d352-179">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="2d352-180">Yapılandırma [ssl sertifikalarını](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2d352-180">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
