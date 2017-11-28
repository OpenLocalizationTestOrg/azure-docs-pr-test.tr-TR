---
title: "Azure Güvenlik Merkezi ve Windows sanal makineleri azure'da | Microsoft Docs"
description: "Azure Güvenlik Merkezi ile Azure Windows sanal makineniz için güvenlik hakkında bilgi edinin."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: adb00e28b0b204858a763f83836ee2ac96f8f9e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a><span data-ttu-id="53759-103">Azure Güvenlik Merkezi'ni kullanarak sanal makine güvenlik izleme</span><span class="sxs-lookup"><span data-stu-id="53759-103">Monitor virtual machine security by using Azure Security Center</span></span>

<span data-ttu-id="53759-104">Azure Güvenlik Merkezi güvenlik uygulamaları, Azure kaynak görünürlük elde size yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="53759-104">Azure Security Center can help you gain visibility into your Azure resource security practices.</span></span> <span data-ttu-id="53759-105">Güvenlik Merkezi, tümleşik güvenlik izleme sunar.</span><span class="sxs-lookup"><span data-stu-id="53759-105">Security Center offers integrated security monitoring.</span></span> <span data-ttu-id="53759-106">Kaçabilecek tehditleri algılayabilir.</span><span class="sxs-lookup"><span data-stu-id="53759-106">It can detect threats that otherwise might go unnoticed.</span></span> <span data-ttu-id="53759-107">Bu öğreticide, Azure Güvenlik Merkezi hakkında bilgi edinmek ve nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="53759-107">In this tutorial, you learn about Azure Security Center, and how to:</span></span>
 
> [!div class="checklist"]
> * <span data-ttu-id="53759-108">Veri toplamayı ayarlama</span><span class="sxs-lookup"><span data-stu-id="53759-108">Set up data collection</span></span>
> * <span data-ttu-id="53759-109">Güvenlik ilkeleri Ayarla</span><span class="sxs-lookup"><span data-stu-id="53759-109">Set up security policies</span></span>
> * <span data-ttu-id="53759-110">Görüntüleme ve yapılandırma sistem durumu sorunları giderin</span><span class="sxs-lookup"><span data-stu-id="53759-110">View and fix configuration health issues</span></span>
> * <span data-ttu-id="53759-111">Algılanan tehditler gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="53759-111">Review detected threats</span></span>  

## <a name="security-center-overview"></a><span data-ttu-id="53759-112">Güvenlik Merkezi'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="53759-112">Security Center overview</span></span>

<span data-ttu-id="53759-113">Güvenlik Merkezi olası sanal makine (VM) yapılandırma sorunları tanımlar ve güvenlik tehditlerini hedeflenen.</span><span class="sxs-lookup"><span data-stu-id="53759-113">Security Center identifies potential virtual machine (VM) configuration issues and targeted security threats.</span></span> <span data-ttu-id="53759-114">Bu ağ güvenlik grupları, şifrelenmemiş diskleri ve kaba kuvvet Uzak Masaüstü Protokolü (RDP) saldırıları eksik olan VM'ler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="53759-114">These might include VMs that are missing network security groups, unencrypted disks, and brute-force Remote Desktop Protocol (RDP) attacks.</span></span> <span data-ttu-id="53759-115">Bilgiler, kolay okunur grafiklerde Güvenlik Merkezi panosunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="53759-115">The information is shown on the Security Center dashboard in easy-to-read graphs.</span></span>

<span data-ttu-id="53759-116">Güvenlik Merkezi panosunda menüsünde Azure portalına erişmek için seçin **Güvenlik Merkezi**.</span><span class="sxs-lookup"><span data-stu-id="53759-116">To access the Security Center dashboard, in the Azure portal, on the menu, select  **Security Center**.</span></span> <span data-ttu-id="53759-117">Panoda Azure ortamınıza güvenlik durumunu görmek, geçerli önerileri sayısını bulun ve tehdit uyarıları geçerli durumunu görüntülemek.</span><span class="sxs-lookup"><span data-stu-id="53759-117">On the dashboard, you can see the security health of your Azure environment, find a count of current recommendations, and view the current state of threat alerts.</span></span> <span data-ttu-id="53759-118">Daha fazla ayrıntı için her bir üst düzey grafik genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53759-118">You can expand each high-level chart to see more detail.</span></span>

![Güvenlik Merkezi Panosu](./media/tutorial-azure-security/asc-dash.png)

<span data-ttu-id="53759-120">Güvenlik Merkezi algıladığı sorunlar için önerilerle sağlamak için veri bulma ötesine gider.</span><span class="sxs-lookup"><span data-stu-id="53759-120">Security Center goes beyond data discovery to provide recommendations for issues that it detects.</span></span> <span data-ttu-id="53759-121">Örneğin, bir VM bir bağlı ağ güvenlik grubu dağıttıysanız, Güvenlik Merkezi ile yapabileceğiniz düzeltme adımları bir öneri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="53759-121">For example, if a VM was deployed without an attached network security group, Security Center displays a recommendation, with remediation steps you can take.</span></span> <span data-ttu-id="53759-122">Güvenlik Merkezi bağlamında ayrılmadan otomatik düzeltme alın.</span><span class="sxs-lookup"><span data-stu-id="53759-122">You get automated remediation without leaving the context of Security Center.</span></span>  

![Öneriler](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a><span data-ttu-id="53759-124">Veri toplamayı ayarlama</span><span class="sxs-lookup"><span data-stu-id="53759-124">Set up data collection</span></span>

<span data-ttu-id="53759-125">VM Güvenlik yapılandırmaları görünürlük sağlayabilmek için önce Güvenlik Merkezi veri toplama ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="53759-125">Before you can get visibility into VM security configurations, you need to set up Security Center data collection.</span></span> <span data-ttu-id="53759-126">Bu, veri koleksiyonu açık kapatarak ve toplanan verileri tutmak için bir Azure depolama hesabı oluşturmayı içerir.</span><span class="sxs-lookup"><span data-stu-id="53759-126">This involves turning on data collection and creating an Azure storage account to hold collected data.</span></span> 

1. <span data-ttu-id="53759-127">Güvenlik Merkezi panosunda tıklatın **Güvenlik İlkesi**, aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="53759-127">On the Security Center dashboard, click **Security policy**, and then select your subscription.</span></span> 
2. <span data-ttu-id="53759-128">İçin **veri toplama**seçin **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="53759-128">For **Data collection**, select **On**.</span></span>
3. <span data-ttu-id="53759-129">Bir depolama hesabı oluşturmak için seçin **depolama hesabı seç**.</span><span class="sxs-lookup"><span data-stu-id="53759-129">To create a storage account, select **Choose a storage account**.</span></span> <span data-ttu-id="53759-130">Ardından, seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="53759-130">Then, select **OK**.</span></span>
4. <span data-ttu-id="53759-131">Üzerinde **Güvenlik İlkesi** dikey penceresinde, select **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="53759-131">On the **Security Policy** blade, select **Save**.</span></span> 

<span data-ttu-id="53759-132">Güvenlik Merkezi veri toplama Aracısı sonra tüm Vm'lere yüklü ve veri toplama başlar.</span><span class="sxs-lookup"><span data-stu-id="53759-132">The Security Center data collection agent is then installed on all VMs, and data collection begins.</span></span> 

## <a name="set-up-a-security-policy"></a><span data-ttu-id="53759-133">Bir güvenlik ilkesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="53759-133">Set up a security policy</span></span>

<span data-ttu-id="53759-134">Güvenlik ilkeleri, kendisi için Güvenlik Merkezi veri toplar ve öneriler yapar öğeleri tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="53759-134">Security policies are used to define the items for which Security Center collects data and makes recommendations.</span></span> <span data-ttu-id="53759-135">Farklı Azure kaynakları için farklı güvenlik ilkeleri uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53759-135">You can apply different security policies to different sets of Azure resources.</span></span> <span data-ttu-id="53759-136">Varsayılan olarak Azure kaynaklarına karşı tüm ilke öğeleri değerlendirilir rağmen tüm Azure kaynakları için veya bir kaynak grubu için tek tek ilke öğelerini devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53759-136">Although by default Azure resources are evaluated against all policy items, you can turn off individual policy items for all Azure resources or for a resource group.</span></span> <span data-ttu-id="53759-137">Güvenlik Merkezi güvenlik ilkeleri hakkında ayrıntılı bilgi için bkz: [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](../../security-center/security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="53759-137">For in-depth information about Security Center security policies, see [Set security policies in Azure Security Center](../../security-center/security-center-policies.md).</span></span> 

<span data-ttu-id="53759-138">Tüm Azure kaynakları için bir güvenlik ilkesi ayarlamak için:</span><span class="sxs-lookup"><span data-stu-id="53759-138">To set up a security policy for all Azure resources:</span></span>

1. <span data-ttu-id="53759-139">Güvenlik Merkezi panosunda seçin **Güvenlik İlkesi**, aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="53759-139">On the Security Center dashboard, select **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="53759-140">Seçin **önleme İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="53759-140">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="53759-141">Açma veya tüm Azure kaynaklarına uygulamak istediğiniz ilke öğeleri kapatın.</span><span class="sxs-lookup"><span data-stu-id="53759-141">Turn on or turn off policy items that you want to apply to all Azure resources.</span></span>
4. <span data-ttu-id="53759-142">Ayarlarınızı seçerek tamamladığınızda seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="53759-142">When you're finished selecting your settings, select **OK**.</span></span>
5. <span data-ttu-id="53759-143">Üzerinde **Güvenlik İlkesi** dikey penceresinde, select **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="53759-143">On the **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="53759-144">Belirli bir kaynak grubu için bir ilke ayarlamak için:</span><span class="sxs-lookup"><span data-stu-id="53759-144">To set up a policy for a specific resource group:</span></span>

1. <span data-ttu-id="53759-145">Güvenlik Merkezi panosunda seçin **Güvenlik İlkesi**, bir kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="53759-145">On the Security Center dashboard, select **Security policy**, and then select a resource group.</span></span>
2. <span data-ttu-id="53759-146">Seçin **önleme İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="53759-146">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="53759-147">Açma veya kaynak grubuna uygulamak istediğiniz ilke öğeleri kapatın.</span><span class="sxs-lookup"><span data-stu-id="53759-147">Turn on or turn off policy items that you want to apply to the resource group.</span></span>
4. <span data-ttu-id="53759-148">Altında **DEVRALMA**seçin **benzersiz**.</span><span class="sxs-lookup"><span data-stu-id="53759-148">Under **INHERITANCE**, select **Unique**.</span></span>
5. <span data-ttu-id="53759-149">Ayarlarınızı seçerek tamamladığınızda seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="53759-149">When you're finished selecting your settings, select **OK**.</span></span>
6. <span data-ttu-id="53759-150">Üzerinde **Güvenlik İlkesi** dikey penceresinde, select **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="53759-150">On the **Security policy** blade, select **Save**.</span></span>  

<span data-ttu-id="53759-151">Bu sayfada belirli bir kaynak grubu için verilerin toplanmasını kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53759-151">You also can turn off data collection for a specific resource group on this page.</span></span>

<span data-ttu-id="53759-152">Aşağıdaki örnekte, bir kaynak grubu için benzersiz bir ilke oluşturuldu *myResoureGroup*.</span><span class="sxs-lookup"><span data-stu-id="53759-152">In the following example, a unique policy has been created for a resource group named *myResoureGroup*.</span></span> <span data-ttu-id="53759-153">Bu ilkede disk şifreleme ve web uygulaması güvenlik duvarı önerileri devre dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="53759-153">In this policy, disk encryption and web application firewall recommendations are turned off.</span></span>

![Benzersiz bir ilke](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a><span data-ttu-id="53759-155">VM yapılandırma durumunu görüntüle</span><span class="sxs-lookup"><span data-stu-id="53759-155">View VM configuration health</span></span>

<span data-ttu-id="53759-156">Veri toplama açık ve bir güvenlik ilkesi ayarladıktan sonra uyarıları ve öneriler sağlamak üzere Güvenlik Merkezi başlar.</span><span class="sxs-lookup"><span data-stu-id="53759-156">After you've turned on data collection and set a security policy, Security Center begins to provide alerts and recommendations.</span></span> <span data-ttu-id="53759-157">Sanal makineleri dağıtılan gibi veri toplama Aracısı yüklenir.</span><span class="sxs-lookup"><span data-stu-id="53759-157">As VMs are deployed, the data collection agent is installed.</span></span> <span data-ttu-id="53759-158">Güvenlik Merkezi, ardından yeni VM'ler için verilerle doldurulur.</span><span class="sxs-lookup"><span data-stu-id="53759-158">Security Center is then populated with data for the new VMs.</span></span> <span data-ttu-id="53759-159">VM yapılandırma sistem durumu hakkında ayrıntılı bilgi için bkz: [Güvenlik Merkezi'nde, Vm'leri koruma](../../security-center/security-center-virtual-machine-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="53759-159">For in-depth information about VM configuration health, see [Protect your VMs in Security Center](../../security-center/security-center-virtual-machine-recommendations.md).</span></span> 

<span data-ttu-id="53759-160">Toplanan veriler gibi her bir VM ve ilgili Azure kaynağı için kaynak durumu toplanır.</span><span class="sxs-lookup"><span data-stu-id="53759-160">As data is collected, the resource health for each VM and related Azure resource is aggregated.</span></span> <span data-ttu-id="53759-161">Bilgiler bir kolay okunur grafiğinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="53759-161">The information is shown in an easy-to-read chart.</span></span> 

<span data-ttu-id="53759-162">Kaynak durumu görüntülemek için:</span><span class="sxs-lookup"><span data-stu-id="53759-162">To view resource health:</span></span>

1.  <span data-ttu-id="53759-163">Güvenlik Merkezi panosunda, altında **kaynak güvenlik durumu**seçin **işlem**.</span><span class="sxs-lookup"><span data-stu-id="53759-163">On the Security Center dashboard, under **Resource security health**, select **Compute**.</span></span> 
2.  <span data-ttu-id="53759-164">Üzerinde **işlem** dikey penceresinde, select **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="53759-164">On the **Compute** blade, select **Virtual machines**.</span></span> <span data-ttu-id="53759-165">Bu görünüm tüm VM'ler için yapılandırma durumu özetini sağlar.</span><span class="sxs-lookup"><span data-stu-id="53759-165">This view provides a summary of the configuration status for all your VMs.</span></span>

![İşlem durumu](./media/tutorial-azure-security/compute-health.png)

<span data-ttu-id="53759-167">Bir VM için tüm önerilerini görmek için VM seçin.</span><span class="sxs-lookup"><span data-stu-id="53759-167">To see all recommendations for a VM, select the VM.</span></span> <span data-ttu-id="53759-168">Öneriler ve düzeltme bu öğreticinin sonraki bölümünde daha ayrıntılı olarak ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="53759-168">Recommendations and remediation are covered in more detail in the next section of this tutorial.</span></span>

## <a name="remediate-configuration-issues"></a><span data-ttu-id="53759-169">Yapılandırma sorunlarını düzeltmek</span><span class="sxs-lookup"><span data-stu-id="53759-169">Remediate configuration issues</span></span>

<span data-ttu-id="53759-170">Güvenlik Merkezi ile yapılandırma verilerini doldurmak başladıktan sonra öneriler ayarladığınız güvenlik ilkesine göre yapılır.</span><span class="sxs-lookup"><span data-stu-id="53759-170">After Security Center begins to populate with configuration data, recommendations are made based on the security policy you set up.</span></span> <span data-ttu-id="53759-171">Örneğin, bir VM ilişkili ağ güvenlik grubu olmadan ayarlarsanız, oluşturmak için bir öneri yapılır.</span><span class="sxs-lookup"><span data-stu-id="53759-171">For instance, if a VM was set up without an associated network security group, a recommendation is made to create one.</span></span> 

<span data-ttu-id="53759-172">Tüm öneriler listesini görmek için:</span><span class="sxs-lookup"><span data-stu-id="53759-172">To see a list of all recommendations:</span></span> 

1. <span data-ttu-id="53759-173">Güvenlik Merkezi panosunda seçin **önerileri**.</span><span class="sxs-lookup"><span data-stu-id="53759-173">On the Security Center dashboard, select **Recommendations**.</span></span>
2. <span data-ttu-id="53759-174">Belirli bir öneri seçin.</span><span class="sxs-lookup"><span data-stu-id="53759-174">Select a specific recommendation.</span></span> <span data-ttu-id="53759-175">Kendisi için tüm kaynakların öneri geçerli bir listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="53759-175">A list of all resources for which the recommendation applies appears.</span></span>
3. <span data-ttu-id="53759-176">Bir öneri uygulamak için belirli bir kaynak seçin.</span><span class="sxs-lookup"><span data-stu-id="53759-176">To apply a recommendation, select a specific resource.</span></span> 
4. <span data-ttu-id="53759-177">Düzeltme adımları için yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="53759-177">Follow the instructions for remediation steps.</span></span> 

<span data-ttu-id="53759-178">Çoğu durumda, Güvenlik Merkezi Güvenlik Merkezi ayrılmadan bir öneri adres için uygulayabileceğiniz tıklatılabilir adımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="53759-178">In many cases, Security Center provides actionable steps you can take to address a recommendation without leaving Security Center.</span></span> <span data-ttu-id="53759-179">Aşağıdaki örnekte, Güvenlik Merkezi sınırsız bir gelen kuralı sahip bir ağ güvenlik grubu algılar.</span><span class="sxs-lookup"><span data-stu-id="53759-179">In the following example, Security Center detects a network security group that has an unrestricted inbound rule.</span></span> <span data-ttu-id="53759-180">Öneri sayfasında seçtiğiniz **gelen kuralları Düzenle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="53759-180">On the recommendation page, you can select the **Edit inbound rules** button.</span></span> <span data-ttu-id="53759-181">Kural değiştirmek için gerekli kullanıcı Arabirimi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="53759-181">The UI that is needed to modify the rule appears.</span></span> 

![Öneriler](./media/tutorial-azure-security/remediation.png)

<span data-ttu-id="53759-183">Öneriler çözümlendi olarak çözümlendi olarak işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="53759-183">As recommendations are remediated, they are marked as resolved.</span></span> 

## <a name="view-detected-threats"></a><span data-ttu-id="53759-184">Algılanan tehditler görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="53759-184">View detected threats</span></span>

<span data-ttu-id="53759-185">Kaynak yapılandırma önerilerine ek olarak Güvenlik Merkezi tehdit algılama uyarıları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="53759-185">In addition to resource configuration recommendations, Security Center displays threat detection alerts.</span></span> <span data-ttu-id="53759-186">Güvenlik Uyarıları özelliği her VM, Azure ağ günlükleri ve bağlı iş ortağı çözümlerinden güvenlik tehditlerine karşı Azure kaynaklarını algılamak için toplanan verileri toplar.</span><span class="sxs-lookup"><span data-stu-id="53759-186">The security alerts feature aggregates data collected from each VM, Azure networking logs, and connected partner solutions to detect security threats against Azure resources.</span></span> <span data-ttu-id="53759-187">Güvenlik Merkezi tehdit algılaması özellikleri hakkında ayrıntılı bilgi için bkz: [Azure Güvenlik Merkezi algılama özellikleri](../../security-center/security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="53759-187">For in-depth information about Security Center threat detection capabilities, see [Azure Security Center detection capabilities](../../security-center/security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="53759-188">Güvenlik Uyarıları özellik gelen artırılacak güvenlik fiyatlandırma katmanı merkezi gerektirir *serbest* için *standart*.</span><span class="sxs-lookup"><span data-stu-id="53759-188">The security alerts feature requires the Security Center pricing tier to be increased from *Free* to *Standard*.</span></span> <span data-ttu-id="53759-189">30 günlük **ücretsiz deneme sürümü** bu daha yüksek fiyatlandırma katmanı taşıdığınızda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="53759-189">A 30-day **free trial** is available when you move to this higher pricing tier.</span></span> 

<span data-ttu-id="53759-190">Fiyatlandırma katmanını değiştirmek için:</span><span class="sxs-lookup"><span data-stu-id="53759-190">To change the pricing tier:</span></span>  

1. <span data-ttu-id="53759-191">Güvenlik Merkezi panosunda tıklatın **Güvenlik İlkesi**, aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="53759-191">On the Security Center dashboard, click **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="53759-192">Seçin **fiyatlandırma katmanı**.</span><span class="sxs-lookup"><span data-stu-id="53759-192">Select **Pricing tier**.</span></span>
3. <span data-ttu-id="53759-193">Yeni katman seçin ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="53759-193">Select the new tier, and then select **Select**.</span></span>
4. <span data-ttu-id="53759-194">Üzerinde **Güvenlik İlkesi** dikey penceresinde, select **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="53759-194">On the **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="53759-195">Fiyatlandırma katmanı değiştirdikten sonra güvenlik uyarıları grafik tehditler algılanır güvenlik doldurmak başlar.</span><span class="sxs-lookup"><span data-stu-id="53759-195">After you've changed the pricing tier, the security alerts graph begins to populate as security threats are detected.</span></span>

![Güvenlik uyarıları](./media/tutorial-azure-security/security-alerts.png)

<span data-ttu-id="53759-197">Bilgileri görüntülemek için bir uyarı seçin.</span><span class="sxs-lookup"><span data-stu-id="53759-197">Select an alert to view information.</span></span> <span data-ttu-id="53759-198">Örneğin, tehdit, algılama zamanı, tüm tehdit girişimleri ve önerilen düzeltme açıklamasını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53759-198">For example, you can see a description of the threat, the detection time, all threat attempts, and the recommended remediation.</span></span> <span data-ttu-id="53759-199">Aşağıdaki örnekte, bir RDP yanılma saldırısı, ile 294 başarısız RDP deneme algılandı.</span><span class="sxs-lookup"><span data-stu-id="53759-199">In the following example, an RDP brute-force attack was detected, with 294 failed RDP attempts.</span></span> <span data-ttu-id="53759-200">Önerilen çözüm sağlanır.</span><span class="sxs-lookup"><span data-stu-id="53759-200">A recommended resolution is provided.</span></span>

![RDP saldırısı](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a><span data-ttu-id="53759-202">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="53759-202">Next steps</span></span>
<span data-ttu-id="53759-203">Bu öğretici, Azure Güvenlik Merkezi ayarlayın ve ardından VM'ler Güvenlik Merkezi'nde gözden.</span><span class="sxs-lookup"><span data-stu-id="53759-203">In this tutorial, you set up Azure Security Center, and then reviewed VMs in Security Center.</span></span> <span data-ttu-id="53759-204">Size nasıl öğrenilen için:</span><span class="sxs-lookup"><span data-stu-id="53759-204">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="53759-205">Veri toplamayı ayarlama</span><span class="sxs-lookup"><span data-stu-id="53759-205">Set up data collection</span></span>
> * <span data-ttu-id="53759-206">Güvenlik ilkeleri Ayarla</span><span class="sxs-lookup"><span data-stu-id="53759-206">Set up security policies</span></span>
> * <span data-ttu-id="53759-207">Görüntüleme ve yapılandırma sistem durumu sorunları giderin</span><span class="sxs-lookup"><span data-stu-id="53759-207">View and fix configuration health issues</span></span>
> * <span data-ttu-id="53759-208">Algılanan tehditler gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="53759-208">Review detected threats</span></span>

<span data-ttu-id="53759-209">Visual Studio Team Services ve IIS çalıştıran bir Windows VM ile CI/CD işlem hattı oluşturma konusunda bilgi almak için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="53759-209">Advance to the next tutorial to learn how to create a CI/CD pipeline with Visual Studio Team Services and a Windows VM running IIS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="53759-210">Visual Studio Team Services CI/CD ardışık düzen</span><span class="sxs-lookup"><span data-stu-id="53759-210">Visual Studio Team Services CI/CD pipeline</span></span>](./tutorial-vsts-iis-cicd.md)
