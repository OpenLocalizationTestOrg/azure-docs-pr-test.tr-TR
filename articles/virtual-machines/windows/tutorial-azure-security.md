---
title: "azure'da aaaAzure Güvenlik Merkezi ve Windows sanal makineler | Microsoft Docs"
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
ms.openlocfilehash: 238bf4e266a24a536d35dd647db6056ab39a1f1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a><span data-ttu-id="72092-103">Azure Güvenlik Merkezi'ni kullanarak sanal makine güvenlik izleme</span><span class="sxs-lookup"><span data-stu-id="72092-103">Monitor virtual machine security by using Azure Security Center</span></span>

<span data-ttu-id="72092-104">Azure Güvenlik Merkezi güvenlik uygulamaları, Azure kaynak görünürlük elde size yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="72092-104">Azure Security Center can help you gain visibility into your Azure resource security practices.</span></span> <span data-ttu-id="72092-105">Güvenlik Merkezi, tümleşik güvenlik izleme sunar.</span><span class="sxs-lookup"><span data-stu-id="72092-105">Security Center offers integrated security monitoring.</span></span> <span data-ttu-id="72092-106">Kaçabilecek tehditleri algılayabilir.</span><span class="sxs-lookup"><span data-stu-id="72092-106">It can detect threats that otherwise might go unnoticed.</span></span> <span data-ttu-id="72092-107">Bu öğreticide, Azure Güvenlik Merkezi hakkında bilgi edinmek ve nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="72092-107">In this tutorial, you learn about Azure Security Center, and how to:</span></span>
 
> [!div class="checklist"]
> * <span data-ttu-id="72092-108">Veri toplamayı ayarlama</span><span class="sxs-lookup"><span data-stu-id="72092-108">Set up data collection</span></span>
> * <span data-ttu-id="72092-109">Güvenlik ilkeleri Ayarla</span><span class="sxs-lookup"><span data-stu-id="72092-109">Set up security policies</span></span>
> * <span data-ttu-id="72092-110">Görüntüleme ve yapılandırma sistem durumu sorunları giderin</span><span class="sxs-lookup"><span data-stu-id="72092-110">View and fix configuration health issues</span></span>
> * <span data-ttu-id="72092-111">Algılanan tehditler gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="72092-111">Review detected threats</span></span>  

## <a name="security-center-overview"></a><span data-ttu-id="72092-112">Güvenlik Merkezi'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="72092-112">Security Center overview</span></span>

<span data-ttu-id="72092-113">Güvenlik Merkezi olası sanal makine (VM) yapılandırma sorunları tanımlar ve güvenlik tehditlerini hedeflenen.</span><span class="sxs-lookup"><span data-stu-id="72092-113">Security Center identifies potential virtual machine (VM) configuration issues and targeted security threats.</span></span> <span data-ttu-id="72092-114">Bu ağ güvenlik grupları, şifrelenmemiş diskleri ve kaba kuvvet Uzak Masaüstü Protokolü (RDP) saldırıları eksik olan VM'ler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="72092-114">These might include VMs that are missing network security groups, unencrypted disks, and brute-force Remote Desktop Protocol (RDP) attacks.</span></span> <span data-ttu-id="72092-115">Merhaba bilgiler kolay okunur grafiklerde hello Güvenlik Merkezi panosunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="72092-115">hello information is shown on hello Security Center dashboard in easy-to-read graphs.</span></span>

<span data-ttu-id="72092-116">tooaccess hello Güvenlik Merkezi panosunda hello hello menüsünde select Azure portal **Güvenlik Merkezi**.</span><span class="sxs-lookup"><span data-stu-id="72092-116">tooaccess hello Security Center dashboard, in hello Azure portal, on hello menu, select  **Security Center**.</span></span> <span data-ttu-id="72092-117">Merhaba Panoda Azure ortamınıza hello güvenlik durumunu görmek, geçerli önerileri sayısını bulun ve tehdit uyarıları hello geçerli durumunu görüntülemek.</span><span class="sxs-lookup"><span data-stu-id="72092-117">On hello dashboard, you can see hello security health of your Azure environment, find a count of current recommendations, and view hello current state of threat alerts.</span></span> <span data-ttu-id="72092-118">Daha fazla ayrıntı her üst düzey grafik toosee genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72092-118">You can expand each high-level chart toosee more detail.</span></span>

![Güvenlik Merkezi Panosu](./media/tutorial-azure-security/asc-dash.png)

<span data-ttu-id="72092-120">Güvenlik Merkezi veri bulma tooprovide önerileri algıladığı sorunların ötesinde gider.</span><span class="sxs-lookup"><span data-stu-id="72092-120">Security Center goes beyond data discovery tooprovide recommendations for issues that it detects.</span></span> <span data-ttu-id="72092-121">Örneğin, bir VM bir bağlı ağ güvenlik grubu dağıttıysanız, Güvenlik Merkezi ile yapabileceğiniz düzeltme adımları bir öneri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="72092-121">For example, if a VM was deployed without an attached network security group, Security Center displays a recommendation, with remediation steps you can take.</span></span> <span data-ttu-id="72092-122">Güvenlik Merkezi Merhaba içeriğine ayrılmadan otomatik düzeltme alın.</span><span class="sxs-lookup"><span data-stu-id="72092-122">You get automated remediation without leaving hello context of Security Center.</span></span>  

![Öneriler](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a><span data-ttu-id="72092-124">Veri toplamayı ayarlama</span><span class="sxs-lookup"><span data-stu-id="72092-124">Set up data collection</span></span>

<span data-ttu-id="72092-125">VM Güvenlik yapılandırmaları görünürlük sağlayabilmek için önce Güvenlik Merkezi veri toplama yukarı tooset gerekir.</span><span class="sxs-lookup"><span data-stu-id="72092-125">Before you can get visibility into VM security configurations, you need tooset up Security Center data collection.</span></span> <span data-ttu-id="72092-126">Bu, veri koleksiyonu açık kapatarak ve bir Azure depolama hesabı toohold toplanan verileri oluşturma içerir.</span><span class="sxs-lookup"><span data-stu-id="72092-126">This involves turning on data collection and creating an Azure storage account toohold collected data.</span></span> 

1. <span data-ttu-id="72092-127">Merhaba Güvenlik Merkezi panosunda tıklatın **Güvenlik İlkesi**, aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="72092-127">On hello Security Center dashboard, click **Security policy**, and then select your subscription.</span></span> 
2. <span data-ttu-id="72092-128">İçin **veri toplama**seçin **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="72092-128">For **Data collection**, select **On**.</span></span>
3. <span data-ttu-id="72092-129">toocreate bir depolama hesabı seçin **depolama hesabı seç**.</span><span class="sxs-lookup"><span data-stu-id="72092-129">toocreate a storage account, select **Choose a storage account**.</span></span> <span data-ttu-id="72092-130">Ardından, seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="72092-130">Then, select **OK**.</span></span>
4. <span data-ttu-id="72092-131">Merhaba üzerinde **Güvenlik İlkesi** dikey penceresinde, select **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="72092-131">On hello **Security Policy** blade, select **Save**.</span></span> 

<span data-ttu-id="72092-132">Merhaba Güvenlik Merkezi veri toplama Aracısı sonra tüm Vm'lere yüklü ve veri toplama başlar.</span><span class="sxs-lookup"><span data-stu-id="72092-132">hello Security Center data collection agent is then installed on all VMs, and data collection begins.</span></span> 

## <a name="set-up-a-security-policy"></a><span data-ttu-id="72092-133">Bir güvenlik ilkesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="72092-133">Set up a security policy</span></span>

<span data-ttu-id="72092-134">Güvenlik ilkeleri, Güvenlik Merkezi veri toplar ve öneriler sağlar kullanılan toodefine hello öğelerdir.</span><span class="sxs-lookup"><span data-stu-id="72092-134">Security policies are used toodefine hello items for which Security Center collects data and makes recommendations.</span></span> <span data-ttu-id="72092-135">Farklı güvenlik ilkeleri toodifferent Azure kaynaklarını kümesi uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72092-135">You can apply different security policies toodifferent sets of Azure resources.</span></span> <span data-ttu-id="72092-136">Varsayılan olarak Azure kaynaklarına karşı tüm ilke öğeleri değerlendirilir rağmen tüm Azure kaynakları için veya bir kaynak grubu için tek tek ilke öğelerini devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72092-136">Although by default Azure resources are evaluated against all policy items, you can turn off individual policy items for all Azure resources or for a resource group.</span></span> <span data-ttu-id="72092-137">Güvenlik Merkezi güvenlik ilkeleri hakkında ayrıntılı bilgi için bkz: [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](../../security-center/security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="72092-137">For in-depth information about Security Center security policies, see [Set security policies in Azure Security Center](../../security-center/security-center-policies.md).</span></span> 

<span data-ttu-id="72092-138">Tüm Azure kaynakları için güvenlik ilkesi tooset:</span><span class="sxs-lookup"><span data-stu-id="72092-138">tooset up a security policy for all Azure resources:</span></span>

1. <span data-ttu-id="72092-139">Merhaba Güvenlik Merkezi panosunda seçin **Güvenlik İlkesi**, aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="72092-139">On hello Security Center dashboard, select **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="72092-140">Seçin **önleme İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="72092-140">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="72092-141">Açma veya Azure kaynaklarını tooapply tooall istediğiniz ilke öğeleri devre dışı bırakma.</span><span class="sxs-lookup"><span data-stu-id="72092-141">Turn on or turn off policy items that you want tooapply tooall Azure resources.</span></span>
4. <span data-ttu-id="72092-142">Ayarlarınızı seçerek tamamladığınızda seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="72092-142">When you're finished selecting your settings, select **OK**.</span></span>
5. <span data-ttu-id="72092-143">Merhaba üzerinde **Güvenlik İlkesi** dikey penceresinde, select **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="72092-143">On hello **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="72092-144">belirli bir kaynak grubunun İlkesi tooset:</span><span class="sxs-lookup"><span data-stu-id="72092-144">tooset up a policy for a specific resource group:</span></span>

1. <span data-ttu-id="72092-145">Merhaba Güvenlik Merkezi panosunda seçin **Güvenlik İlkesi**, bir kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="72092-145">On hello Security Center dashboard, select **Security policy**, and then select a resource group.</span></span>
2. <span data-ttu-id="72092-146">Seçin **önleme İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="72092-146">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="72092-147">Açma veya tooapply toohello kaynak grubu istediğiniz ilke öğeleri devre dışı bırakma.</span><span class="sxs-lookup"><span data-stu-id="72092-147">Turn on or turn off policy items that you want tooapply toohello resource group.</span></span>
4. <span data-ttu-id="72092-148">Altında **DEVRALMA**seçin **benzersiz**.</span><span class="sxs-lookup"><span data-stu-id="72092-148">Under **INHERITANCE**, select **Unique**.</span></span>
5. <span data-ttu-id="72092-149">Ayarlarınızı seçerek tamamladığınızda seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="72092-149">When you're finished selecting your settings, select **OK**.</span></span>
6. <span data-ttu-id="72092-150">Merhaba üzerinde **Güvenlik İlkesi** dikey penceresinde, select **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="72092-150">On hello **Security policy** blade, select **Save**.</span></span>  

<span data-ttu-id="72092-151">Bu sayfada belirli bir kaynak grubu için verilerin toplanmasını kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72092-151">You also can turn off data collection for a specific resource group on this page.</span></span>

<span data-ttu-id="72092-152">Aşağıdaki örneğine hello adlı bir kaynak grubu için benzersiz bir ilke oluşturuldu *myResoureGroup*.</span><span class="sxs-lookup"><span data-stu-id="72092-152">In hello following example, a unique policy has been created for a resource group named *myResoureGroup*.</span></span> <span data-ttu-id="72092-153">Bu ilkede disk şifreleme ve web uygulaması güvenlik duvarı önerileri devre dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="72092-153">In this policy, disk encryption and web application firewall recommendations are turned off.</span></span>

![Benzersiz bir ilke](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a><span data-ttu-id="72092-155">VM yapılandırma durumunu görüntüle</span><span class="sxs-lookup"><span data-stu-id="72092-155">View VM configuration health</span></span>

<span data-ttu-id="72092-156">Veri toplama açık ve bir güvenlik ilkesi ayarladıktan sonra Güvenlik Merkezi tooprovide uyarısı ve öneri başlar.</span><span class="sxs-lookup"><span data-stu-id="72092-156">After you've turned on data collection and set a security policy, Security Center begins tooprovide alerts and recommendations.</span></span> <span data-ttu-id="72092-157">Sanal makineleri dağıtılan gibi hello veri toplama Aracısı yüklenir.</span><span class="sxs-lookup"><span data-stu-id="72092-157">As VMs are deployed, hello data collection agent is installed.</span></span> <span data-ttu-id="72092-158">Güvenlik Merkezi hello için verilerle doldurulur sonra yeni VM'ler.</span><span class="sxs-lookup"><span data-stu-id="72092-158">Security Center is then populated with data for hello new VMs.</span></span> <span data-ttu-id="72092-159">VM yapılandırma sistem durumu hakkında ayrıntılı bilgi için bkz: [Güvenlik Merkezi'nde, Vm'leri koruma](../../security-center/security-center-virtual-machine-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="72092-159">For in-depth information about VM configuration health, see [Protect your VMs in Security Center](../../security-center/security-center-virtual-machine-recommendations.md).</span></span> 

<span data-ttu-id="72092-160">Toplanan veriler gibi her bir VM ve ilgili Azure kaynağı için hello kaynak durumu toplanır.</span><span class="sxs-lookup"><span data-stu-id="72092-160">As data is collected, hello resource health for each VM and related Azure resource is aggregated.</span></span> <span data-ttu-id="72092-161">Hello bilgiler bir kolay okunur grafiğinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="72092-161">hello information is shown in an easy-to-read chart.</span></span> 

<span data-ttu-id="72092-162">tooview kaynak durumu:</span><span class="sxs-lookup"><span data-stu-id="72092-162">tooview resource health:</span></span>

1.  <span data-ttu-id="72092-163">Merhaba Güvenlik Merkezi panosunda altında **kaynak güvenlik durumu**seçin **işlem**.</span><span class="sxs-lookup"><span data-stu-id="72092-163">On hello Security Center dashboard, under **Resource security health**, select **Compute**.</span></span> 
2.  <span data-ttu-id="72092-164">Merhaba üzerinde **işlem** dikey penceresinde, select **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="72092-164">On hello **Compute** blade, select **Virtual machines**.</span></span> <span data-ttu-id="72092-165">Bu görünüm tüm VM'ler için hello yapılandırma durumunun bir özetini sağlar.</span><span class="sxs-lookup"><span data-stu-id="72092-165">This view provides a summary of hello configuration status for all your VMs.</span></span>

![İşlem durumu](./media/tutorial-azure-security/compute-health.png)

<span data-ttu-id="72092-167">toosee bir VM için tüm öneriler hello VM seçin.</span><span class="sxs-lookup"><span data-stu-id="72092-167">toosee all recommendations for a VM, select hello VM.</span></span> <span data-ttu-id="72092-168">Öneriler ve düzeltme hello Bu öğreticinin sonraki bölümünde daha ayrıntılı olarak ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="72092-168">Recommendations and remediation are covered in more detail in hello next section of this tutorial.</span></span>

## <a name="remediate-configuration-issues"></a><span data-ttu-id="72092-169">Yapılandırma sorunlarını düzeltmek</span><span class="sxs-lookup"><span data-stu-id="72092-169">Remediate configuration issues</span></span>

<span data-ttu-id="72092-170">Güvenlik Merkezi ile yapılandırma verilerini toopopulate başladıktan sonra öneriler ayarladığınız hello güvenlik ilkesine göre yapılır.</span><span class="sxs-lookup"><span data-stu-id="72092-170">After Security Center begins toopopulate with configuration data, recommendations are made based on hello security policy you set up.</span></span> <span data-ttu-id="72092-171">Örneğin, bir VM ilişkili ağ güvenlik grubu olmadan ayarlarsanız, bir öneri toocreate bir yapılır.</span><span class="sxs-lookup"><span data-stu-id="72092-171">For instance, if a VM was set up without an associated network security group, a recommendation is made toocreate one.</span></span> 

<span data-ttu-id="72092-172">toosee tüm önerilerin bir listesi:</span><span class="sxs-lookup"><span data-stu-id="72092-172">toosee a list of all recommendations:</span></span> 

1. <span data-ttu-id="72092-173">Merhaba Güvenlik Merkezi panosunda seçin **önerileri**.</span><span class="sxs-lookup"><span data-stu-id="72092-173">On hello Security Center dashboard, select **Recommendations**.</span></span>
2. <span data-ttu-id="72092-174">Belirli bir öneri seçin.</span><span class="sxs-lookup"><span data-stu-id="72092-174">Select a specific recommendation.</span></span> <span data-ttu-id="72092-175">Kendisi için tüm kaynakların hello öneri geçerli bir listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="72092-175">A list of all resources for which hello recommendation applies appears.</span></span>
3. <span data-ttu-id="72092-176">tooapply bir öneri, belirli bir kaynak seçin.</span><span class="sxs-lookup"><span data-stu-id="72092-176">tooapply a recommendation, select a specific resource.</span></span> 
4. <span data-ttu-id="72092-177">Düzeltme adımları Hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="72092-177">Follow hello instructions for remediation steps.</span></span> 

<span data-ttu-id="72092-178">Çoğu durumda, Güvenlik Merkezi işlem yapılabilir adımları sağlar. Güvenlik Merkezi ayrılmadan bir öneri tooaddress alabilir.</span><span class="sxs-lookup"><span data-stu-id="72092-178">In many cases, Security Center provides actionable steps you can take tooaddress a recommendation without leaving Security Center.</span></span> <span data-ttu-id="72092-179">Aşağıdaki örneğine hello sınırsız bir gelen kuralı sahip bir ağ güvenlik grubu Güvenlik Merkezi algılar.</span><span class="sxs-lookup"><span data-stu-id="72092-179">In hello following example, Security Center detects a network security group that has an unrestricted inbound rule.</span></span> <span data-ttu-id="72092-180">Merhaba öneri sayfasında hello seçebilirsiniz **gelen kuralları Düzenle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="72092-180">On hello recommendation page, you can select hello **Edit inbound rules** button.</span></span> <span data-ttu-id="72092-181">Merhaba gerekli toomodify hello kural kullanıcı Arabirimi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="72092-181">hello UI that is needed toomodify hello rule appears.</span></span> 

![Öneriler](./media/tutorial-azure-security/remediation.png)

<span data-ttu-id="72092-183">Öneriler çözümlendi olarak çözümlendi olarak işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="72092-183">As recommendations are remediated, they are marked as resolved.</span></span> 

## <a name="view-detected-threats"></a><span data-ttu-id="72092-184">Algılanan tehditler görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="72092-184">View detected threats</span></span>

<span data-ttu-id="72092-185">Ayrıca tooresource yapılandırma önerileri, Güvenlik Merkezi, tehdit algılama uyarıları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="72092-185">In addition tooresource configuration recommendations, Security Center displays threat detection alerts.</span></span> <span data-ttu-id="72092-186">Merhaba güvenlik uyarıları özelliği her VM, Azure ağ günlükleri ve bağlı iş ortağı çözümleri toodetect güvenlik tehditlerine karşı Azure kaynaklarını toplanan verileri toplar.</span><span class="sxs-lookup"><span data-stu-id="72092-186">hello security alerts feature aggregates data collected from each VM, Azure networking logs, and connected partner solutions toodetect security threats against Azure resources.</span></span> <span data-ttu-id="72092-187">Güvenlik Merkezi tehdit algılaması özellikleri hakkında ayrıntılı bilgi için bkz: [Azure Güvenlik Merkezi algılama özellikleri](../../security-center/security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="72092-187">For in-depth information about Security Center threat detection capabilities, see [Azure Security Center detection capabilities](../../security-center/security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="72092-188">Merhaba güvenlik uyarıları özelliği gerektirir hello güvenlik katmanı toobe gelen artan fiyatlandırma Merkezi *serbest* çok*standart*.</span><span class="sxs-lookup"><span data-stu-id="72092-188">hello security alerts feature requires hello Security Center pricing tier toobe increased from *Free* too*Standard*.</span></span> <span data-ttu-id="72092-189">30 günlük **ücretsiz deneme sürümü** toothis fiyatlandırma katmanı daha yüksek taşıdığınızda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="72092-189">A 30-day **free trial** is available when you move toothis higher pricing tier.</span></span> 

<span data-ttu-id="72092-190">toochange hello fiyatlandırma katmanı:</span><span class="sxs-lookup"><span data-stu-id="72092-190">toochange hello pricing tier:</span></span>  

1. <span data-ttu-id="72092-191">Merhaba Güvenlik Merkezi panosunda tıklatın **Güvenlik İlkesi**, aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="72092-191">On hello Security Center dashboard, click **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="72092-192">Seçin **fiyatlandırma katmanı**.</span><span class="sxs-lookup"><span data-stu-id="72092-192">Select **Pricing tier**.</span></span>
3. <span data-ttu-id="72092-193">Merhaba yeni katmanı seçin ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="72092-193">Select hello new tier, and then select **Select**.</span></span>
4. <span data-ttu-id="72092-194">Merhaba üzerinde **Güvenlik İlkesi** dikey penceresinde, select **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="72092-194">On hello **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="72092-195">Fiyatlandırma katmanı hello değiştirdikten sonra güvenlik tehditleri algılandığında hello güvenlik uyarıları grafik toopopulate başlar.</span><span class="sxs-lookup"><span data-stu-id="72092-195">After you've changed hello pricing tier, hello security alerts graph begins toopopulate as security threats are detected.</span></span>

![Güvenlik uyarıları](./media/tutorial-azure-security/security-alerts.png)

<span data-ttu-id="72092-197">Bir uyarı tooview bilgileri seçin.</span><span class="sxs-lookup"><span data-stu-id="72092-197">Select an alert tooview information.</span></span> <span data-ttu-id="72092-198">Örneğin, hello tehdit, hello algılama zamanı, tüm tehdit girişimleri açıklamasını görmek ve önerilen düzeltme hello.</span><span class="sxs-lookup"><span data-stu-id="72092-198">For example, you can see a description of hello threat, hello detection time, all threat attempts, and hello recommended remediation.</span></span> <span data-ttu-id="72092-199">Aşağıdaki örneğine hello bir RDP yanılma saldırısı, ile 294 başarısız RDP deneme algılandı.</span><span class="sxs-lookup"><span data-stu-id="72092-199">In hello following example, an RDP brute-force attack was detected, with 294 failed RDP attempts.</span></span> <span data-ttu-id="72092-200">Önerilen çözüm sağlanır.</span><span class="sxs-lookup"><span data-stu-id="72092-200">A recommended resolution is provided.</span></span>

![RDP saldırısı](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a><span data-ttu-id="72092-202">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="72092-202">Next steps</span></span>
<span data-ttu-id="72092-203">Bu öğretici, Azure Güvenlik Merkezi ayarlayın ve ardından VM'ler Güvenlik Merkezi'nde gözden.</span><span class="sxs-lookup"><span data-stu-id="72092-203">In this tutorial, you set up Azure Security Center, and then reviewed VMs in Security Center.</span></span> <span data-ttu-id="72092-204">Şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="72092-204">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="72092-205">Veri toplamayı ayarlama</span><span class="sxs-lookup"><span data-stu-id="72092-205">Set up data collection</span></span>
> * <span data-ttu-id="72092-206">Güvenlik ilkeleri Ayarla</span><span class="sxs-lookup"><span data-stu-id="72092-206">Set up security policies</span></span>
> * <span data-ttu-id="72092-207">Görüntüleme ve yapılandırma sistem durumu sorunları giderin</span><span class="sxs-lookup"><span data-stu-id="72092-207">View and fix configuration health issues</span></span>
> * <span data-ttu-id="72092-208">Algılanan tehditler gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="72092-208">Review detected threats</span></span>

<span data-ttu-id="72092-209">Toohello sonraki öğretici toolearn toocreate CI/CD kanal nasıl ile Visual Studio Team Services ve IIS çalıştıran bir Windows VM ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="72092-209">Advance toohello next tutorial toolearn how toocreate a CI/CD pipeline with Visual Studio Team Services and a Windows VM running IIS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="72092-210">Visual Studio Team Services CI/CD ardışık düzen</span><span class="sxs-lookup"><span data-stu-id="72092-210">Visual Studio Team Services CI/CD pipeline</span></span>](./tutorial-vsts-iis-cicd.md)
