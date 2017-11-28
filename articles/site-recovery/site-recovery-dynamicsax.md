---
title: "Azure Site Recovery kullanarak çok katmanlı Dynamics AX dağıtım çoğaltmak | Microsoft Docs"
description: "Bu makalede, çoğaltma ve Azure Site RECOVERY'yi kullanarak Dynamics AX korumak açıklar"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/24/2017
ms.author: asgang
ms.openlocfilehash: 03127c8f4841b67436c4819628319705af0b2cd5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="4fd91-103">Azure Site RECOVERY'yi kullanarak çok katmanlı Dynamics AX uygulamayı çoğaltma</span><span class="sxs-lookup"><span data-stu-id="4fd91-103">Replicate a multi-tier Dynamics AX application using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="4fd91-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="4fd91-104">Overview</span></span>


<span data-ttu-id="4fd91-105">Microsoft Dynamics AX standartlaştırılmış işleme kuruluşlar arasında en popüler ERP çözüm konumlar arasında biri, kaynakları ve uyumluluk basitleştirme yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4fd91-105">Microsoft Dynamics AX is one of the most popular ERP solution among enterprises to standardized process across locations, manage resources and simplifying compliance.</span></span> <span data-ttu-id="4fd91-106">Kuruluş için kritik iş uygulamasıdır considering emin olması durumunda olması çok önemlidir herhangi olağanüstü durum uygulama hazır ve çalışır en az sürede olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4fd91-106">Considering the application is business critical to an organization it is very important to be sure that if any disaster, application should be up and running in minimum time.</span></span>

<span data-ttu-id="4fd91-107">Bugün, Microsoft Dynamics AX tüm giden kutusu olağanüstü durum kurtarma özellikleri sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="4fd91-107">Today, Microsoft Dynamics AX  does not provide any out-of-the-box disaster recovery capabilities.</span></span> <span data-ttu-id="4fd91-108">Microsoft Dynamics AX Uygulama Nesne Sunucusu, Active Directory (AD), SQL veritabanı sunucusu, SharePoint Server, Raporlama sunucusu vb. gibi pek çok sunucu bileşenden oluşur. Olağanüstü durum kurtarma işlemi bu bileşenlerin her birini el ile yalnızca pahalı, ancak aynı zamanda hataya yönetmektir.</span><span class="sxs-lookup"><span data-stu-id="4fd91-108">Microsoft Dynamics AX consists of many server components like Application Object Server, Active Directory (AD), SQL Database Server, SharePoint Server, Reporting Server etc. To manage the disaster recovery of each of these components manually is not only expensive but also error-prone.</span></span>

<span data-ttu-id="4fd91-109">Bu makalede, nasıl bir olağanüstü durum kurtarma çözümü Dynamics AX kullanarak uygulamanızı için oluşturabileceğiniz hakkında ayrıntılı olarak açıklanmaktadır [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4fd91-109">This article explains in detail about how you can create a disaster recovery solution for your Dynamics AX application using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="4fd91-110">Ayrıca, tek tıklatmayla kurtarma planı, desteklenen yapılandırmalar ve önkoşullar kullanarak planlanan/planlanmamış/yük devretme sınaması işlemlerini kapsar.</span><span class="sxs-lookup"><span data-stu-id="4fd91-110">It also covers planned/unplanned/test failovers using one-click recovery plan, supported configurations, and prerequisites.</span></span>
<span data-ttu-id="4fd91-111">Azure Site Recovery dayalı olağanüstü durum kurtarma çözümü tam olarak test sertifikalı ve Microsoft Dynamics AX tarafından önerilir.</span><span class="sxs-lookup"><span data-stu-id="4fd91-111">Azure Site Recovery based disaster recovery solution is fully tested, certified, and recommended by Microsoft Dynamics AX.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="4fd91-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4fd91-112">Prerequisites</span></span>

<span data-ttu-id="4fd91-113">Azure Site Recovery kullanarak Dynamics AX uygulamasının olağanüstü durum kurtarma uygulama tamamlandı aşağıdaki önkoşulları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4fd91-113">Implementing disaster recovery for Dynamics AX application using Azure Site Recovery requires the following pre-requisites completed.</span></span>

<span data-ttu-id="4fd91-114">• Şirket içi Dynamics AX dağıtım ayarlanmış</span><span class="sxs-lookup"><span data-stu-id="4fd91-114">•   An on-premises Dynamics AX deployment has been set up</span></span>

<span data-ttu-id="4fd91-115">• Azure Site kurtarma Hizmetleri kasası Microsoft Azure aboneliğinin oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="4fd91-115">•   Azure Site Recovery Services vault has been created in Microsoft Azure subscription</span></span>

<span data-ttu-id="4fd91-116">• Azure kurtarma siteniz olduğunda çalıştırmak Azure sanal makine hazırlık Değerlendirme Aracı vm'lerde Azure Vm'leri ve Azure Site kurtarma Hizmetleri ile uyumlu olduklarından emin olun</span><span class="sxs-lookup"><span data-stu-id="4fd91-116">•   If Azure is your recovery site, run the Azure Virtual Machine Readiness Assessment tool  on VMs to ensure that they are compatible with Azure VMs and Azure Site Recovery Services</span></span>


## <a name="site-recovery-support"></a><span data-ttu-id="4fd91-117">Site kurtarma desteği</span><span class="sxs-lookup"><span data-stu-id="4fd91-117">Site Recovery support</span></span>

<span data-ttu-id="4fd91-118">Bu makalede oluşturmak amacıyla, Windows Server 2012 R2 Enterprise üzerinde Dynamics AX 2012R3 VMware sanal makineleri kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="4fd91-118">For the purpose of creating this article, VMware virtual machines with Dynamics AX  2012R3 on Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="4fd91-119">Site recovery çoğaltma uygulama belirsiz olduğundan, burada sağlanan öneriler de aşağıdaki senaryoları tutun beklenir.</span><span class="sxs-lookup"><span data-stu-id="4fd91-119">As site recovery replication is application agnostic, the recommendations provided here are expected to hold on following scenarios as well.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="4fd91-120">Kaynak ve hedef</span><span class="sxs-lookup"><span data-stu-id="4fd91-120">Source and target</span></span>

<span data-ttu-id="4fd91-121">**Senaryo**</span><span class="sxs-lookup"><span data-stu-id="4fd91-121">**Scenario**</span></span> | <span data-ttu-id="4fd91-122">**İkincil bir siteye**</span><span class="sxs-lookup"><span data-stu-id="4fd91-122">**To a secondary site**</span></span> | <span data-ttu-id="4fd91-123">**Azure'a**</span><span class="sxs-lookup"><span data-stu-id="4fd91-123">**To Azure**</span></span>
--- | --- | ---
<span data-ttu-id="4fd91-124">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="4fd91-124">**Hyper-V**</span></span> | <span data-ttu-id="4fd91-125">Evet</span><span class="sxs-lookup"><span data-stu-id="4fd91-125">Yes</span></span> | <span data-ttu-id="4fd91-126">Evet</span><span class="sxs-lookup"><span data-stu-id="4fd91-126">Yes</span></span>
<span data-ttu-id="4fd91-127">**VMware**</span><span class="sxs-lookup"><span data-stu-id="4fd91-127">**VMware**</span></span> | <span data-ttu-id="4fd91-128">Evet</span><span class="sxs-lookup"><span data-stu-id="4fd91-128">Yes</span></span> | <span data-ttu-id="4fd91-129">Evet</span><span class="sxs-lookup"><span data-stu-id="4fd91-129">Yes</span></span>
<span data-ttu-id="4fd91-130">**Fiziksel sunucu**</span><span class="sxs-lookup"><span data-stu-id="4fd91-130">**Physical server**</span></span> | <span data-ttu-id="4fd91-131">Evet</span><span class="sxs-lookup"><span data-stu-id="4fd91-131">Yes</span></span> | <span data-ttu-id="4fd91-132">Evet</span><span class="sxs-lookup"><span data-stu-id="4fd91-132">Yes</span></span>

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="4fd91-133">Azure Site RECOVERY'yi kullanarak Dynamics AX DR uygulamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="4fd91-133">Enable DR of Dynamics AX application using Azure Site Recovery</span></span>
### <a name="protect-your-dynamics-ax-application"></a><span data-ttu-id="4fd91-134">Dynamics AX uygulamanızı koruma</span><span class="sxs-lookup"><span data-stu-id="4fd91-134">Protect your Dynamics AX application</span></span>
<span data-ttu-id="4fd91-135">Dynamics AX her bileşenin tam uygulama çoğaltma ve kurtarma etkinleştirmek için korunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4fd91-135">Each component of the Dynamics AX needs to be protected to enable the complete application replication and recovery.</span></span> <span data-ttu-id="4fd91-136">Bu bölümde ele alınmaktadır:</span><span class="sxs-lookup"><span data-stu-id="4fd91-136">This section covers:</span></span>

<span data-ttu-id="4fd91-137">**1. Active Directory koruma**</span><span class="sxs-lookup"><span data-stu-id="4fd91-137">**1. Protection of Active Directory**</span></span>

<span data-ttu-id="4fd91-138">**2. SQL katmanının koruma**</span><span class="sxs-lookup"><span data-stu-id="4fd91-138">**2. Protection of SQL Tier**</span></span>

<span data-ttu-id="4fd91-139">**3. Uygulamanın ve Web katmanları koruma**</span><span class="sxs-lookup"><span data-stu-id="4fd91-139">**3. Protection of App and Web Tiers**</span></span>

<span data-ttu-id="4fd91-140">**4. Ağ yapılandırması**</span><span class="sxs-lookup"><span data-stu-id="4fd91-140">**4. Networking configuration**</span></span>

<span data-ttu-id="4fd91-141">**5. Kurtarma planı**</span><span class="sxs-lookup"><span data-stu-id="4fd91-141">**5. Recovery Plan**</span></span>

### <a name="1-setup-ad-and-dns-replication"></a><span data-ttu-id="4fd91-142">1. Kurulum AD ve DNS çoğaltması</span><span class="sxs-lookup"><span data-stu-id="4fd91-142">1. Setup AD and DNS replication</span></span>

<span data-ttu-id="4fd91-143">Active Directory DR sitesi Dynamics AX uygulama işlevi için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="4fd91-143">Active Directory is required on the DR site for Dynamics AX application to function.</span></span> <span data-ttu-id="4fd91-144">Bir müşterinin şirket içi ortamına karmaşıklığı önerilen iki seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="4fd91-144">There are two recommended choices based on the complexity of the customer’s on-premises environment.</span></span>

<span data-ttu-id="4fd91-145">**Seçenek 1**</span><span class="sxs-lookup"><span data-stu-id="4fd91-145">**Option 1**</span></span>

<span data-ttu-id="4fd91-146">Müşterinin az sayıda uygulamaları ve tek etki alanı denetleyicisi varsa, tüm site içi ve ikincil siteye (için geçerli DC makine çoğaltmak için ASR çoğaltma kullanmanızı öneririz sonra birlikte, tüm site başarısız Siteden siteye hem Azure siteye).</span><span class="sxs-lookup"><span data-stu-id="4fd91-146">If the customer has a small number of applications and a single domain controller for his entire on-premises site and will be failing over the entire site together, then we recommend using ASR-Replication to replicate the DC machine to secondary site (applicable for both Site to Site and Site to Azure).</span></span>

<span data-ttu-id="4fd91-147">**Seçenek 2**</span><span class="sxs-lookup"><span data-stu-id="4fd91-147">**Option 2**</span></span>

<span data-ttu-id="4fd91-148">Müşteri uygulamalar çok sayıda sahip bir Active Directory ormanı çalıştıran ve yük birkaç uygulamalar aynı anda devretme durumunda DR sitesi ek etki alanı denetleyicisinde ayarlama öneririz (ikincil site veya Azure).</span><span class="sxs-lookup"><span data-stu-id="4fd91-148">If the customer has a large number of applications and is running an Active Directory forest and will fail-over few applications at a time, then we recommend setting up an additional domain controller on the DR site (secondary site or in Azure).</span></span>

<span data-ttu-id="4fd91-149">Lütfen [bir etki alanı denetleyicisi DR sitede kullanılabilir hale getirme üzerinde yardımcı kılavuz](site-recovery-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="4fd91-149">Please refer to [companion guide on making a domain controller available on DR site](site-recovery-active-directory.md).</span></span> <span data-ttu-id="4fd91-150">Bu belgenin geri kalanında için DC DR sitesinden edinilebilir varsayacağız.</span><span class="sxs-lookup"><span data-stu-id="4fd91-150">For remainder of this document we will assume a DC is available on DR site.</span></span>

### <a name="2-setup-sql-server-replication"></a><span data-ttu-id="4fd91-151">2. SQL Server çoğaltması Kurulumu</span><span class="sxs-lookup"><span data-stu-id="4fd91-151">2. Setup SQL Server replication</span></span>
<span data-ttu-id="4fd91-152">Koruma için önerilen seçeneğinde yardımcı kılavuz ayrıntılı teknik kılavuzu için lütfen [SQL katmanı](site-recovery-sql.md).</span><span class="sxs-lookup"><span data-stu-id="4fd91-152">Please refer to companion guide  for detailed technical guidance on the recommended option for protecting [SQL tier](site-recovery-sql.md).</span></span>

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a><span data-ttu-id="4fd91-153">3. Dynamics AX İstemcisi ve AOS VM'ler için korumayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="4fd91-153">3. Enable protection for Dynamics AX client and AOS VMs</span></span>
<span data-ttu-id="4fd91-154">Olup VM'ler dağıtılan üzerinde temel ilgili Azure Site Recovery yapılandırmasını gerçekleştirmek [Hyper-V](site-recovery-hyper-v-site-to-azure.md) veya [VMware](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="4fd91-154">Perform relevant Azure Site Recovery configuration based on whether the VMs are deployed on [Hyper-V](site-recovery-hyper-v-site-to-azure.md) or on [VMware](site-recovery-vmware-to-azure.md).</span></span>

> [!TIP]
> <span data-ttu-id="4fd91-155">Kilitlenme tutarlı sıklığı önerilen yapılandırmak için 15 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="4fd91-155">Recommended Crash consistent frequency to configure is 15 minutes.</span></span>
>

<span data-ttu-id="4fd91-156">Anlık Görüntü 'Azure sitesine VMware' koruma senaryoda Dynamics bileşen Vm'leri koruma durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="4fd91-156">The below snapshot shows the protection status of Dynamics component VMs in ‘VMware site to Azure’ protection scenario.</span></span>
<span data-ttu-id="4fd91-157">![Korumalı öğeler](./media/site-recovery-dynamics-ax/protecteditems.png)</span><span class="sxs-lookup"><span data-stu-id="4fd91-157">![Protected items ](./media/site-recovery-dynamics-ax/protecteditems.png)</span></span>

### <a name="4-configure-networking"></a><span data-ttu-id="4fd91-158">4. Ağı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4fd91-158">4. Configure Networking</span></span>
<span data-ttu-id="4fd91-159">VM yapılandırma işlem ve ağ ayarları</span><span class="sxs-lookup"><span data-stu-id="4fd91-159">Configure VM Compute and Network Settings</span></span>

<span data-ttu-id="4fd91-160">Böylece VM ağları, yük devretme sonrasında doğru DR ağa bağlı AX İstemcisi ve AOS VM'ler için Azure Site Recovery ağ ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4fd91-160">For the AX client and AOS VMs configure network settings in Azure Site Recovery so that the VM networks get attached to the right DR network after failover.</span></span> <span data-ttu-id="4fd91-161">Bu katmanlar için DR ağ SQL katmanına yönlendirilebilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4fd91-161">Ensure the DR network for these tiers is routable to the SQL tier.</span></span>

<span data-ttu-id="4fd91-162">VM anlık görüntüde gösterildiği gibi ağ ayarlarını yapılandırmak için çoğaltılan öğe seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4fd91-162">You can select the VM in the replicated items to configure the network settings as shown in the snapshot below.</span></span>

* <span data-ttu-id="4fd91-163">AOS sunucuları doğru kullanılabilirlik kümesi seçin.</span><span class="sxs-lookup"><span data-stu-id="4fd91-163">For AOS servers select the correct availability set.</span></span>

* <span data-ttu-id="4fd91-164">Bir statik IP kullanarak yeniden yapılacağını sanal makine istediğiniz IP belirtin **hedef IP** alan ![ağ ayarları](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span><span class="sxs-lookup"><span data-stu-id="4fd91-164">If you are using a static IP then specify the IP that you want the virtual machine to take in the **Target IP** field ![Network Settings ](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span></span>



### <a name="5-creating-a-recovery-plan"></a><span data-ttu-id="4fd91-165">5. Bir kurtarma planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4fd91-165">5. Creating a recovery plan</span></span>

<span data-ttu-id="4fd91-166">Bir kurtarma planı yük devretme işlemini otomatikleştirmek için Azure Site Recovery oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4fd91-166">You can create a recovery plan in Azure Site Recovery to automate the failover process.</span></span> <span data-ttu-id="4fd91-167">Uygulama katmanı ve web katmanı kurtarma planındaki ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4fd91-167">Add app tier and web tier in the Recovery Plan.</span></span> <span data-ttu-id="4fd91-168">Böylece uygulama önce ön uç kapatma katmanı bunları farklı gruplarda sıralayın.</span><span class="sxs-lookup"><span data-stu-id="4fd91-168">Order them in different groups so that the front-end shutdown before app tier.</span></span>

1)  <span data-ttu-id="4fd91-169">Azure Site Recovery kasası aboneliğinizde seçin ve 'Kurtarma planları' kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4fd91-169">Select the Azure Site Recovery vault in your subscription and click on ‘Recovery Plans’ tile.</span></span>

2)  <span data-ttu-id="4fd91-170">Tıklayın ' + kurtarma planı ve bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="4fd91-170">Click on ‘+ Recovery plan and specify a name.</span></span>

3)  <span data-ttu-id="4fd91-171">'Target' ve 'Source' seçin.</span><span class="sxs-lookup"><span data-stu-id="4fd91-171">Select the ‘Source’ and ‘Target’.</span></span> <span data-ttu-id="4fd91-172">Hedef Azure veya ikincil site olabilir.</span><span class="sxs-lookup"><span data-stu-id="4fd91-172">The target can be Azure or secondary site.</span></span> <span data-ttu-id="4fd91-173">Azure seçtiğiniz durumunda dağıtım modelini belirtin</span><span class="sxs-lookup"><span data-stu-id="4fd91-173">In case you choose Azure, you must specify the deployment model</span></span>

![Kurtarma planı oluşturun](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  <span data-ttu-id="4fd91-175">İstemci sanal makineleri kurtarma planına ve AOS seçin ve ✓'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4fd91-175">Select the AOS and client VMs to the recovery plan and click ✓.</span></span>
<span data-ttu-id="4fd91-176">![Kurtarma planı oluşturun](./media/site-recovery-dynamics-ax/selectvms.png)</span><span class="sxs-lookup"><span data-stu-id="4fd91-176">![Create Recovery Plan](./media/site-recovery-dynamics-ax/selectvms.png)</span></span>


![Kurtarma planı](./media/site-recovery-dynamics-ax/recoveryplan.png)

<span data-ttu-id="4fd91-178">Aşağıda açıklandığı gibi çeşitli adımları ekleyerek kurtarma planı Dynamics AX uygulama için özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4fd91-178">You can customize the recovery plan for Dynamics AX application by adding various steps as detailed below.</span></span> <span data-ttu-id="4fd91-179">Yukarıdaki anlık tüm adımları ekledikten sonra tam kurtarma planı gösterir.</span><span class="sxs-lookup"><span data-stu-id="4fd91-179">The above snapshot shows the complete recovery plan after adding all the steps.</span></span>

<span data-ttu-id="4fd91-180">*Adımlar:*</span><span class="sxs-lookup"><span data-stu-id="4fd91-180">*Steps:*</span></span>

<span data-ttu-id="4fd91-181">*1. SQL Server üzerinde adımları başarısız*</span><span class="sxs-lookup"><span data-stu-id="4fd91-181">*1. SQL Server fail over steps*</span></span>

<span data-ttu-id="4fd91-182">Başvurmak ['SQL Server DR çözüm'](site-recovery-sql.md) kurtarma adımlarını belirli SQL Server hakkındaki ayrıntılar için yardımcı kılavuz.</span><span class="sxs-lookup"><span data-stu-id="4fd91-182">Refer to [‘SQL Server DR Solution’](site-recovery-sql.md) companion guide  for details about recovery steps specific to SQL server.</span></span>

<span data-ttu-id="4fd91-183">*2. Yük devretme Grup 1: Yük devretme AOS VM'ler*</span><span class="sxs-lookup"><span data-stu-id="4fd91-183">*2. Failover Group 1: Fail over the AOS VMs*</span></span>

<span data-ttu-id="4fd91-184">Seçilen kurtarma noktası PIT veritabanına mümkün olduğunca yakın ancak değil şimdi olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4fd91-184">Make sure that the recovery point selected is as close as possible to the database PIT but not ahead.</span></span>

<span data-ttu-id="4fd91-185">*3. Komut dosyası: Ekle yük dengeleyici (yalnızca E-A)* Ekle bir yük dengeleyici eklemek için bir komut dosyası (aracılığıyla Azure Otomasyonu) AOS VM gruptan sonra gelir.</span><span class="sxs-lookup"><span data-stu-id="4fd91-185">*3. Script: Add load balancer (Only E-A)* Add a script (via Azure automation) after AOS VM group comes up to add a load balancer to it.</span></span> <span data-ttu-id="4fd91-186">Bu görevi gerçekleştirmek için bir komut dosyası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4fd91-186">You can use a script to do this task.</span></span> <span data-ttu-id="4fd91-187">Makale başvuran [çok katmanlı uygulama DR için yük dengeleyici ekleme](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span><span class="sxs-lookup"><span data-stu-id="4fd91-187">Refer article [how to add load balancer for multi-tier application DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span></span>

<span data-ttu-id="4fd91-188">*4. Yük devretme Grup 2: AX İstemcisi VM'ler başarısız.*</span><span class="sxs-lookup"><span data-stu-id="4fd91-188">*4. Failover Group 2: Fail over the AX client VMs.*</span></span>
<span data-ttu-id="4fd91-189">Kurtarma planının bir parçası olarak VM'ler web katmanı yük devri.</span><span class="sxs-lookup"><span data-stu-id="4fd91-189">Fail over the web tier VMs as part of the recovery plan.</span></span>


### <a name="doing-a-test-failover"></a><span data-ttu-id="4fd91-190">Yük devretme sınamasını yapmak</span><span class="sxs-lookup"><span data-stu-id="4fd91-190">Doing a test failover</span></span>

<span data-ttu-id="4fd91-191">'AD DR çözüm' ve 'SQL Server DR çözüm' yardımcı kılavuzlar için konuları belirli AD için bakın ve SQL server yük devretme testi sırasında sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="4fd91-191">Refer to ‘AD DR Solution ’ and ‘SQL Server DR solution ’ companion guides for considerations specific to AD and SQL server respectively during Test Failover.</span></span>

1.  <span data-ttu-id="4fd91-192">Azure Portalı'na gidin ve Site Recovery kasanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="4fd91-192">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="4fd91-193">Dynamics AX için oluşturduğunuz kurtarma planı tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4fd91-193">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="4fd91-194">'Test yük devretme üzerinde' tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4fd91-194">Click on ‘Test Failover’.</span></span>
4.  <span data-ttu-id="4fd91-195">Test yük devretme işlemini başlatmak için sanal ağ seçin.</span><span class="sxs-lookup"><span data-stu-id="4fd91-195">Select the virtual network to start the test fail-over process.</span></span>
5.  <span data-ttu-id="4fd91-196">İkincil ortamı kurma olduğunda, doğrulama gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4fd91-196">Once the secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="4fd91-197">Doğrulama tamamlandıktan sonra 'Doğrulamaları tamamlamak' seçin ve yük devretme sınama ortamı temizlendi.</span><span class="sxs-lookup"><span data-stu-id="4fd91-197">Once the validations are complete, you can select ‘Validations complete’ and the test failover environment will be cleaned.</span></span>

<span data-ttu-id="4fd91-198">İzleyin [bu kılavuz](site-recovery-test-failover-to-azure.md) yük devretme sınamasını yapmak için.</span><span class="sxs-lookup"><span data-stu-id="4fd91-198">Follow [this guidance](site-recovery-test-failover-to-azure.md) to do a test failover.</span></span>

### <a name="doing-a-failover"></a><span data-ttu-id="4fd91-199">Bir yük devretme işleminden</span><span class="sxs-lookup"><span data-stu-id="4fd91-199">Doing a failover</span></span>

1.  <span data-ttu-id="4fd91-200">Azure Portalı'na gidin ve Site Recovery kasanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="4fd91-200">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="4fd91-201">Dynamics AX için oluşturduğunuz kurtarma planı tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4fd91-201">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="4fd91-202">'Üzerinde yük devretme' tıklatın ve 'Failover' seçin.</span><span class="sxs-lookup"><span data-stu-id="4fd91-202">Click on ‘Failover’ and select ‘ Failover’.</span></span>
4.  <span data-ttu-id="4fd91-203">Hedef ağ seçin ve yük devretme işlemini başlatmak için ✓ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4fd91-203">Select the target network and click ✓ to start the failover process.</span></span>

<span data-ttu-id="4fd91-204">İzleyin [bu kılavuz](site-recovery-failover.md) , yaparken bir yük devretme.</span><span class="sxs-lookup"><span data-stu-id="4fd91-204">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

### <a name="perform-a-failback"></a><span data-ttu-id="4fd91-205">Bir yeniden çalışma gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="4fd91-205">Perform a Failback</span></span>

<span data-ttu-id="4fd91-206">'SQL Server DR çözüm' yardımcı Kılavuzu SQL Server'a özel konular için yeniden çalışma sırasında bakın.</span><span class="sxs-lookup"><span data-stu-id="4fd91-206">Refer to ‘SQL Server DR Solution ’ companion guide for considerations specific to SQL server during Failback.</span></span>

1.  <span data-ttu-id="4fd91-207">Azure Portalı'na gidin ve Site Recovery kasanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="4fd91-207">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="4fd91-208">Dynamics AX için oluşturduğunuz kurtarma planı tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4fd91-208">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="4fd91-209">'Üzerinde yük devretme' tıklayın ve yük devretme seçin.</span><span class="sxs-lookup"><span data-stu-id="4fd91-209">Click on ‘Failover’ and select failover.</span></span>
4.  <span data-ttu-id="4fd91-210">'Üzerinde değişiklik yön' seçeneğini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4fd91-210">Click on ‘Change Direction’.</span></span>
5.  <span data-ttu-id="4fd91-211">-Veri eşitleme ve VM oluşturma seçenekleri uygun seçenekleri seçin</span><span class="sxs-lookup"><span data-stu-id="4fd91-211">Select the appropriate options - data synchronization and VM creation options</span></span>
6.  <span data-ttu-id="4fd91-212">✓ 'Yeniden çalışma' işlemini başlatmak için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4fd91-212">Click ✓ to start the ‘Failback’ process.</span></span>


<span data-ttu-id="4fd91-213">İzleyin [bu kılavuz](site-recovery-failback-azure-to-vmware.md) , yaparken bir yeniden çalışma.</span><span class="sxs-lookup"><span data-stu-id="4fd91-213">Follow [this guidance](site-recovery-failback-azure-to-vmware.md) when you are doing a failback.</span></span>

##<a name="summary"></a><span data-ttu-id="4fd91-214">Özet</span><span class="sxs-lookup"><span data-stu-id="4fd91-214">Summary</span></span>
<span data-ttu-id="4fd91-215">Azure Site Recovery kullanarak, Dynamics AX uygulamanız için bir tam otomatik olağanüstü durum kurtarma planı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4fd91-215">Using Azure Site Recovery, you can create a complete automated disaster recovery plan for your Dynamics AX application.</span></span> <span data-ttu-id="4fd91-216">Her yerden saniye içinde yük devretmeyi başlatın durumunda kesintisi ve get uygulama dakika içinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="4fd91-216">You can initiate the failover within seconds from anywhere in the event of a disruption and get the application up and running in minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fd91-217">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4fd91-217">Next steps</span></span>
<span data-ttu-id="4fd91-218">Okuma [hangi iş yüklerini koruyabilirim?](site-recovery-workload.md) Azure Site Recovery ile kurumsal iş yüklerini koruma hakkında daha fazla bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="4fd91-218">Read [What workloads can I protect?](site-recovery-workload.md) to learn more about protecting enterprise workloads with Azure Site Recovery.</span></span>
