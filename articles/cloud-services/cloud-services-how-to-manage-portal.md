---
title: "Genel bulut hizmeti yönetim görevleri | Microsoft Docs"
description: "Azure portalında bulut Hizmetleri yönetmeyi öğrenin. Bu örnekler Azure Portalı'nı kullanın."
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
ms.openlocfilehash: 4650cebe18153e3b10bbec685a66a590348c99e9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-manage-cloud-services"></a><span data-ttu-id="25756-104">Bulut Hizmetleri yönetme</span><span class="sxs-lookup"><span data-stu-id="25756-104">How to Manage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="25756-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="25756-105">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="25756-106">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="25756-106">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="25756-107">İçinde **bulut Hizmetleri (Klasik)** alanı Azure portal, hizmet rolü veya bir dağıtım güncelleştirmek, aşamalı bir dağıtım üretime yükseltmek, yapabilirsiniz; böylece kaynak bağımlılıkları bakın ve kaynakları birlikte ölçeği ve bir bulut hizmeti ya da dağıtım silmek bulut hizmetinize bağlamak kaynakları.</span><span class="sxs-lookup"><span data-stu-id="25756-107">In the **Cloud Services (classic)** area of the Azure portal, you can update a service role or a deployment, promote a staged deployment to production, link resources to your cloud service so that you can see the resource dependencies and scale the resources together, and delete a cloud service or a deployment.</span></span>

<span data-ttu-id="25756-108">Bulut hizmetinizi ölçeklendirme hakkında daha fazla bilgi kullanılabilir [burada](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="25756-108">More information about how to scale your cloud service is available [here](cloud-services-how-to-scale-portal.md).</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="25756-109">Nasıl yapılır: bir bulut hizmet rolü veya dağıtım güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="25756-109">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="25756-110">Bulut hizmetiniz için uygulama kodu güncellemeniz gerekiyorsa kullanın **güncelleştirme** bulut hizmeti dikey.</span><span class="sxs-lookup"><span data-stu-id="25756-110">If you need to update the application code for your cloud service, use **Update** on the cloud service blade.</span></span> <span data-ttu-id="25756-111">Tek bir rol veya tüm rolleri güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="25756-111">You can update a single role or all roles.</span></span> <span data-ttu-id="25756-112">Güncelleştirmek için yeni hizmet paketi ya da hizmet yapılandırma dosyasını karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="25756-112">To update, you can upload a new service package or service configuration file.</span></span>

1. <span data-ttu-id="25756-113">İçinde [Azure portal][Azure portal], güncelleştirmek istediğiniz bulut hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="25756-113">In the [Azure portal][Azure portal], select the cloud service you want to update.</span></span> <span data-ttu-id="25756-114">Bu adım bulut hizmeti örneği dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="25756-114">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="25756-115">Dikey penceresinde tıklayın **güncelleştirme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="25756-115">In the blade, click the **Update** button.</span></span>

    ![Güncelleştir düğmesi](./media/cloud-services-how-to-manage-portal/update-button.png)

3. <span data-ttu-id="25756-117">Dağıtım, yeni hizmet paketi dosyasının (.cspkg) ve hizmet yapılandırma dosyasının (.cscfg) ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="25756-117">Update the deployment with a new service package file (.cspkg) and service configuration file (.cscfg).</span></span>

    ![UpdateDeployment](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. <span data-ttu-id="25756-119">**İsteğe bağlı olarak** dağıtım etiketi ve depolama hesabı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="25756-119">**Optionally** update the deployment label and the storage account.</span></span>
5. <span data-ttu-id="25756-120">Herhangi bir rolü yalnızca bir rol örneği varsa, seçin **bir veya daha fazla rol tek bir örnek içeriyorsa bile Dağıt** devam etmek yükseltmeyi etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="25756-120">If any roles have only one role instance, select the **Deploy even if one or more roles contain a single instance** to enable the upgrade to proceed.</span></span>

    <span data-ttu-id="25756-121">Her role en az iki rol örnekleri (sanal makineler) varsa azure yalnızca 99,95 yüzde hizmet kullanılabilirliği bir bulut hizmet güncelleştirmesi sırasında garanti edebilir.</span><span class="sxs-lookup"><span data-stu-id="25756-121">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="25756-122">Diğer güncelleştirilirken iki rol örneği ile bir sanal makine istemci isteklerini işler.</span><span class="sxs-lookup"><span data-stu-id="25756-122">With two role instances, one virtual machine processes client requests while the other is updated.</span></span>

6. <span data-ttu-id="25756-123">Denetleme **Başlat dağıtım** paketin karşıya yükleme tamamlandıktan sonra uygulanan güncelleştirme sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="25756-123">Check **Start deployment** to have the update applied after the upload of the package has finished.</span></span>
7. <span data-ttu-id="25756-124">Tıklatın **Tamam** hizmeti güncelleştirme başlamak için.</span><span class="sxs-lookup"><span data-stu-id="25756-124">Click **OK** to begin updating the service.</span></span>

## <a name="how-to-swap-deployments-to-promote-a-staged-deployment-to-production"></a><span data-ttu-id="25756-125">Nasıl yapılır: takas aşamalı bir dağıtım üretime yükseltmek için dağıtımlar</span><span class="sxs-lookup"><span data-stu-id="25756-125">How to: Swap deployments to promote a staged deployment to production</span></span>
<span data-ttu-id="25756-126">Bir bulut hizmeti, aşama yeni bir sürümünü dağıtmak ve yeni sürüm, bulut hizmeti hazırlama ortamında test etmek karar verdiğinizde.</span><span class="sxs-lookup"><span data-stu-id="25756-126">When you decide to deploy a new release of a cloud service, stage and test your new release in your cloud service staging environment.</span></span> <span data-ttu-id="25756-127">Kullanım **takas** , iki dağıtım giderilmesini ve üretim yeni bir sürüme yükseltmek URL'leri geçiş yapmak için.</span><span class="sxs-lookup"><span data-stu-id="25756-127">Use **Swap** to switch the URLs by which the two deployments are addressed and promote a new release to production.</span></span>

<span data-ttu-id="25756-128">Dağıtımlarından takas **bulut Hizmetleri** sayfası veya Pano'dan.</span><span class="sxs-lookup"><span data-stu-id="25756-128">You can swap deployments from the **Cloud Services** page or the dashboard.</span></span>

1. <span data-ttu-id="25756-129">İçinde [Azure portal][Azure portal], güncelleştirmek istediğiniz bulut hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="25756-129">In the [Azure portal][Azure portal], select the cloud service you want to update.</span></span> <span data-ttu-id="25756-130">Bu adım bulut hizmeti örneği dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="25756-130">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="25756-131">Dikey penceresinde tıklayın **takas** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="25756-131">In the blade, click the **Swap** button.</span></span>

    ![Bulut Hizmetleri değiştirme](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. <span data-ttu-id="25756-133">Aşağıdaki onay istemi açılır.</span><span class="sxs-lookup"><span data-stu-id="25756-133">The following confirmation prompt opens.</span></span>

    ![Bulut Hizmetleri değiştirme](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. <span data-ttu-id="25756-135">Dağıtım bilgileri doğruladıktan sonra tıklatın **Tamam** dağıtımlarını değiştirmek için.</span><span class="sxs-lookup"><span data-stu-id="25756-135">After you verify the deployment information, click **OK** to swap the deployments.</span></span>

    <span data-ttu-id="25756-136">Sanal IP adresleri (VIP) değişiklikleri tek şey olduğu için dağıtımı takas dağıtımları için hızlı bir şekilde gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="25756-136">The deployment swap happens quickly because the only thing that changes is the virtual IP addresses (VIPs) for the deployments.</span></span>

    <span data-ttu-id="25756-137">İşlem maliyetleri kaydetmek için üretim dağıtımınızın beklendiği gibi çalıştığını doğruladıktan sonra hazırlama dağıtım silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="25756-137">To save compute costs, you can delete the staging deployment after you verify that your production deployment is working as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="25756-138">Dağıtımları değiştirme hakkında sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="25756-138">Common questions about swapping deployments</span></span>

<span data-ttu-id="25756-139">**Dağıtımları takas önkoşulları nelerdir?**</span><span class="sxs-lookup"><span data-stu-id="25756-139">**What are the prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="25756-140">Başarılı dağıtım Takas için iki anahtar Önkoşullar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="25756-140">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="25756-141">Statik bir IP adresi, üretim yuvası için kullanmak istiyorsanız, bir hazırlama yuvası da ayırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="25756-141">If you would like to use a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="25756-142">Aksi takdirde değiştirme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="25756-142">Otherwise, the swap fails.</span></span>

- <span data-ttu-id="25756-143">Takas gerçekleştirmeden önce tüm örneklerini rollerinizi çalıştırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="25756-143">All instances of your roles must be running before you can perform the swap.</span></span> <span data-ttu-id="25756-144">Genel Bakış dikey penceresinde örneklerinizi Azure portal'ın durumunu kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="25756-144">You can check the status of your instances in the overview blade of the Azure portal.</span></span> <span data-ttu-id="25756-145">Alternatif olarak, kullanabileceğiniz [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) Windows PowerShell komutu.</span><span class="sxs-lookup"><span data-stu-id="25756-145">Alternatively, you can use the [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) command in Windows PowerShell.</span></span>

<span data-ttu-id="25756-146">Not Konuk işletim sistemi güncelleştirmeleri ve hizmet işlemleri düzeltme dağıtım takasları başarısız olmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="25756-146">Note that Guest OS updates and service healing operations can also cause deployment swaps to fail.</span></span> <span data-ttu-id="25756-147">Daha fazla bilgi için bkz: [bulut hizmeti dağıtım sorunlarını giderme](cloud-services-troubleshoot-deployment-problems.md).</span><span class="sxs-lookup"><span data-stu-id="25756-147">For more information, see [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md).</span></span>

<span data-ttu-id="25756-148">**Bir takas Uygulamam için kapalı kalma süresi maliyetine neden olabilir mi? Bunu nasıl işlemesi gerekir?**</span><span class="sxs-lookup"><span data-stu-id="25756-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="25756-149">Yalnızca Azure yük dengeleyici yapılandırması değişikliği olduğundan son bölümde açıklandığı gibi bir dağıtımı takas genellikle hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="25756-149">As described in the last section, a deployment swap is typically fast since it is just a configuration change in the Azure load balancer.</span></span> <span data-ttu-id="25756-150">Bazı durumlarda, Bununla birlikte, en az on dakika sürer ve geçici bağlantı hatalarına neden.</span><span class="sxs-lookup"><span data-stu-id="25756-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="25756-151">Müşterilerinize etkilerini sınırlamaktır uygulayın [istemci yeniden deneme mantığı](../best-practices-retry-general.md).</span><span class="sxs-lookup"><span data-stu-id="25756-151">To limit impact to your customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-to-a-cloud-service"></a><span data-ttu-id="25756-152">Nasıl yapılır: bir bulut hizmeti için bir kaynak Bağla</span><span class="sxs-lookup"><span data-stu-id="25756-152">How to: Link a resource to a cloud service</span></span>
<span data-ttu-id="25756-153">Geçerli Azure Klasik portalı yaptığı gibi Azure portalındaki kaynakları birlikte bağlantı vermiyor.</span><span class="sxs-lookup"><span data-stu-id="25756-153">The Azure portal does not link resources together like the current Azure classic portal does.</span></span> <span data-ttu-id="25756-154">Bunun yerine, bulut hizmeti tarafından kullanılan aynı kaynak grubuna ek kaynaklar dağıtın.</span><span class="sxs-lookup"><span data-stu-id="25756-154">Instead, deploy additional resources to the same resource group being used by the Cloud Service.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="25756-155">Nasıl yapılır: dağıtımları ve bulut hizmeti Sil</span><span class="sxs-lookup"><span data-stu-id="25756-155">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="25756-156">Bir bulut hizmeti silebilmek için önce varolan her dağıtım silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="25756-156">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="25756-157">İşlem maliyetleri kaydetmek için üretim dağıtımınızın beklendiği gibi çalıştığını doğruladıktan sonra hazırlama dağıtım silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="25756-157">To save compute costs, you can delete the staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="25756-158">İşlem maliyetleri durdurulur dağıtılan rol örnekleri için faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="25756-158">You are billed for compute costs for deployed role instances that are stopped.</span></span>

<span data-ttu-id="25756-159">Bir dağıtımı veya Bulut hizmeti silmek için aşağıdaki yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="25756-159">Use the following procedure to delete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="25756-160">İçinde [Azure portal][Azure portal], silmek istediğiniz bulut hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="25756-160">In the [Azure portal][Azure portal], select the cloud service you want to delete.</span></span> <span data-ttu-id="25756-161">Bu adım bulut hizmeti örneği dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="25756-161">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="25756-162">Dikey penceresinde tıklayın **silmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="25756-162">In the blade, click the **Delete** button.</span></span>

    ![Bulut Hizmetleri değiştirme](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. <span data-ttu-id="25756-164">Kontrol ederek tüm bulut hizmeti silebilirsiniz **bulut hizmeti ve hizmetin dağıtımları** veya seçin ya da **Üretim dağıtımı** veya **hazırlama dağıtımı**.</span><span class="sxs-lookup"><span data-stu-id="25756-164">You can delete the entire cloud service by checking **Cloud service and its deployments** or choose either the **Production deployment** or the **Staging deployment**.</span></span>

    ![Bulut Hizmetleri değiştirme](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. <span data-ttu-id="25756-166">Tıklatın **silmek** altındaki düğmesini.</span><span class="sxs-lookup"><span data-stu-id="25756-166">Click the **Delete** button at the bottom.</span></span>
5. <span data-ttu-id="25756-167">Bulut hizmeti silmek için tıklatın **Delete bulut hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="25756-167">To delete the cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="25756-168">Ardından, onay isteminde **Evet**.</span><span class="sxs-lookup"><span data-stu-id="25756-168">Then, at the confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="25756-169">Bir bulut hizmeti silindi ve ayrıntılı izleme yapılandırılmış veri depolama hesabınızdan el ile silmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="25756-169">When a cloud service is deleted, and verbose monitoring is configured, you must delete the data manually from your storage account.</span></span> <span data-ttu-id="25756-170">Ölçümleri tabloları nerede bulacağını hakkında daha fazla bilgi için bkz: [bu](cloud-services-how-to-monitor.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="25756-170">For information about where to find the metrics tables, see [this](cloud-services-how-to-monitor.md) article.</span></span>


## <a name="how-to-find-more-information-about-failed-deployments"></a><span data-ttu-id="25756-171">Nasıl yapılır: başarısız dağıtımları hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="25756-171">How to: Find more information about failed deployments</span></span>
<span data-ttu-id="25756-172">**Genel bakış** dikey durum çubuğu üstünde vardır.</span><span class="sxs-lookup"><span data-stu-id="25756-172">The **Overview** blade has a status bar at the top.</span></span> <span data-ttu-id="25756-173">Çubuğu'nu tıklatın, yeni bir dikey pencere açar ve hata bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="25756-173">When you click the bar, a new blade opens and displays any error information.</span></span> <span data-ttu-id="25756-174">Dağıtım hatalarını içermiyorsa, bilgi dikey boştur.</span><span class="sxs-lookup"><span data-stu-id="25756-174">If the deployment does not contain any errors, the information blade is blank.</span></span>

![Bulut Hizmetleri değiştirme](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="25756-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="25756-176">Next steps</span></span>
* <span data-ttu-id="25756-177">[Genel yapılandırma bulut hizmetinizin](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="25756-177">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="25756-178">Bilgi edinmek için nasıl [bir bulut hizmetinin dağıtılacağı](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="25756-178">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="25756-179">Yapılandırma bir [özel etki alanı adı](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="25756-179">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="25756-180">Yapılandırma [ssl sertifikalarını](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="25756-180">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
