---
title: "Azure Site Recovery kullanarak çok katmanlı Dynamics AX dağıtım aaaReplicate | Microsoft Docs"
description: "Bu makalede nasıl tooreplicate ve Azure Site RECOVERY'yi kullanarak Dynamics AX koruyun"
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
ms.openlocfilehash: b974315ec50ab2ec43846b3d3f95c7de88b72fc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="627af-103">Azure Site RECOVERY'yi kullanarak çok katmanlı Dynamics AX uygulamayı çoğaltma</span><span class="sxs-lookup"><span data-stu-id="627af-103">Replicate a multi-tier Dynamics AX application using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="627af-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="627af-104">Overview</span></span>


<span data-ttu-id="627af-105">Microsoft Dynamics AX hello en popüler ERP çözüm kuruluşların toostandardized işlem arasında konumlar arasında biri, kaynakları ve uyumluluk basitleştirme yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="627af-105">Microsoft Dynamics AX is one of hello most popular ERP solution among enterprises toostandardized process across locations, manage resources and simplifying compliance.</span></span> <span data-ttu-id="627af-106">İş kritik tooan kuruluş Hello uygulamasıdır considering çok önemli toobe emin olup, bir olağanüstü durum uygulama hazır ve çalışır en az sürede olup olmayacağını.</span><span class="sxs-lookup"><span data-stu-id="627af-106">Considering hello application is business critical tooan organization it is very important toobe sure that if any disaster, application should be up and running in minimum time.</span></span>

<span data-ttu-id="627af-107">Bugün, Microsoft Dynamics AX tüm giden kutusu olağanüstü durum kurtarma özellikleri sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="627af-107">Today, Microsoft Dynamics AX  does not provide any out-of-the-box disaster recovery capabilities.</span></span> <span data-ttu-id="627af-108">Microsoft Dynamics AX oluşur uygulama nesne sunucusu, Active Directory (AD), SQL veritabanı sunucusu, SharePoint Server gibi birçok sunucu bileşenlerinin, Raporlama sunucusu vb. toomanage hello olağanüstü durum kurtarma, bu bileşenlerin her birini el ile yalnızca Ayrıca hataya ancak pahalı.</span><span class="sxs-lookup"><span data-stu-id="627af-108">Microsoft Dynamics AX consists of many server components like Application Object Server, Active Directory (AD), SQL Database Server, SharePoint Server, Reporting Server etc. toomanage hello disaster recovery of each of these components manually is not only expensive but also error-prone.</span></span>

<span data-ttu-id="627af-109">Bu makalede, nasıl bir olağanüstü durum kurtarma çözümü Dynamics AX kullanarak uygulamanızı için oluşturabileceğiniz hakkında ayrıntılı olarak açıklanmaktadır [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="627af-109">This article explains in detail about how you can create a disaster recovery solution for your Dynamics AX application using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="627af-110">Ayrıca, tek tıklatmayla kurtarma planı, desteklenen yapılandırmalar ve önkoşullar kullanarak planlanan/planlanmamış/yük devretme sınaması işlemlerini kapsar.</span><span class="sxs-lookup"><span data-stu-id="627af-110">It also covers planned/unplanned/test failovers using one-click recovery plan, supported configurations, and prerequisites.</span></span>
<span data-ttu-id="627af-111">Azure Site Recovery dayalı olağanüstü durum kurtarma çözümü tam olarak test sertifikalı ve Microsoft Dynamics AX tarafından önerilir.</span><span class="sxs-lookup"><span data-stu-id="627af-111">Azure Site Recovery based disaster recovery solution is fully tested, certified, and recommended by Microsoft Dynamics AX.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="627af-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="627af-112">Prerequisites</span></span>

<span data-ttu-id="627af-113">Azure Site Recovery kullanarak Dynamics AX uygulamasının olağanüstü durum kurtarma uygulama tamamlandı ön koşullar aşağıdaki hello gerektirir.</span><span class="sxs-lookup"><span data-stu-id="627af-113">Implementing disaster recovery for Dynamics AX application using Azure Site Recovery requires hello following pre-requisites completed.</span></span>

<span data-ttu-id="627af-114">• Şirket içi Dynamics AX dağıtım ayarlanmış</span><span class="sxs-lookup"><span data-stu-id="627af-114">•   An on-premises Dynamics AX deployment has been set up</span></span>

<span data-ttu-id="627af-115">• Azure Site kurtarma Hizmetleri kasası Microsoft Azure aboneliğinin oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="627af-115">•   Azure Site Recovery Services vault has been created in Microsoft Azure subscription</span></span>

<span data-ttu-id="627af-116">• Azure kurtarma siteniz olduğunda çalıştırmak hello Azure sanal makine hazırlık değerlendirme aracı üzerinde sanal makineleri tooensure Azure Vm'leri ve Azure Site kurtarma Hizmetleri ile uyumlu olan</span><span class="sxs-lookup"><span data-stu-id="627af-116">•   If Azure is your recovery site, run hello Azure Virtual Machine Readiness Assessment tool  on VMs tooensure that they are compatible with Azure VMs and Azure Site Recovery Services</span></span>


## <a name="site-recovery-support"></a><span data-ttu-id="627af-117">Site kurtarma desteği</span><span class="sxs-lookup"><span data-stu-id="627af-117">Site Recovery support</span></span>

<span data-ttu-id="627af-118">Bu makalede oluşturma hello amaç için VMware sanal makineleri üzerinde Windows Server 2012 R2 Enterprise Dynamics AX 2012R3 kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="627af-118">For hello purpose of creating this article, VMware virtual machines with Dynamics AX  2012R3 on Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="627af-119">Site recovery çoğaltma uygulama belirsiz olduğu gibi hello önerileri burada beklenen toohold de aşağıdaki senaryoları sağlanır.</span><span class="sxs-lookup"><span data-stu-id="627af-119">As site recovery replication is application agnostic, hello recommendations provided here are expected toohold on following scenarios as well.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="627af-120">Kaynak ve hedef</span><span class="sxs-lookup"><span data-stu-id="627af-120">Source and target</span></span>

<span data-ttu-id="627af-121">**Senaryo**</span><span class="sxs-lookup"><span data-stu-id="627af-121">**Scenario**</span></span> | <span data-ttu-id="627af-122">**tooa ikincil site**</span><span class="sxs-lookup"><span data-stu-id="627af-122">**tooa secondary site**</span></span> | <span data-ttu-id="627af-123">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="627af-123">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="627af-124">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="627af-124">**Hyper-V**</span></span> | <span data-ttu-id="627af-125">Evet</span><span class="sxs-lookup"><span data-stu-id="627af-125">Yes</span></span> | <span data-ttu-id="627af-126">Evet</span><span class="sxs-lookup"><span data-stu-id="627af-126">Yes</span></span>
<span data-ttu-id="627af-127">**VMware**</span><span class="sxs-lookup"><span data-stu-id="627af-127">**VMware**</span></span> | <span data-ttu-id="627af-128">Evet</span><span class="sxs-lookup"><span data-stu-id="627af-128">Yes</span></span> | <span data-ttu-id="627af-129">Evet</span><span class="sxs-lookup"><span data-stu-id="627af-129">Yes</span></span>
<span data-ttu-id="627af-130">**Fiziksel sunucu**</span><span class="sxs-lookup"><span data-stu-id="627af-130">**Physical server**</span></span> | <span data-ttu-id="627af-131">Evet</span><span class="sxs-lookup"><span data-stu-id="627af-131">Yes</span></span> | <span data-ttu-id="627af-132">Evet</span><span class="sxs-lookup"><span data-stu-id="627af-132">Yes</span></span>

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="627af-133">Azure Site RECOVERY'yi kullanarak Dynamics AX DR uygulamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="627af-133">Enable DR of Dynamics AX application using Azure Site Recovery</span></span>
### <a name="protect-your-dynamics-ax-application"></a><span data-ttu-id="627af-134">Dynamics AX uygulamanızı koruma</span><span class="sxs-lookup"><span data-stu-id="627af-134">Protect your Dynamics AX application</span></span>
<span data-ttu-id="627af-135">Her bir bileşeninin hello Dynamics AX gereksinimlerini toobe tooenable hello tam uygulama çoğaltma ve kurtarma korumalı.</span><span class="sxs-lookup"><span data-stu-id="627af-135">Each component of hello Dynamics AX needs toobe protected tooenable hello complete application replication and recovery.</span></span> <span data-ttu-id="627af-136">Bu bölümde ele alınmaktadır:</span><span class="sxs-lookup"><span data-stu-id="627af-136">This section covers:</span></span>

<span data-ttu-id="627af-137">**1. Active Directory koruma**</span><span class="sxs-lookup"><span data-stu-id="627af-137">**1. Protection of Active Directory**</span></span>

<span data-ttu-id="627af-138">**2. SQL katmanının koruma**</span><span class="sxs-lookup"><span data-stu-id="627af-138">**2. Protection of SQL Tier**</span></span>

<span data-ttu-id="627af-139">**3. Uygulamanın ve Web katmanları koruma**</span><span class="sxs-lookup"><span data-stu-id="627af-139">**3. Protection of App and Web Tiers**</span></span>

<span data-ttu-id="627af-140">**4. Ağ yapılandırması**</span><span class="sxs-lookup"><span data-stu-id="627af-140">**4. Networking configuration**</span></span>

<span data-ttu-id="627af-141">**5. Kurtarma planı**</span><span class="sxs-lookup"><span data-stu-id="627af-141">**5. Recovery Plan**</span></span>

### <a name="1-setup-ad-and-dns-replication"></a><span data-ttu-id="627af-142">1. Kurulum AD ve DNS çoğaltması</span><span class="sxs-lookup"><span data-stu-id="627af-142">1. Setup AD and DNS replication</span></span>

<span data-ttu-id="627af-143">Active Directory hello DR sitesi Dynamics AX uygulama toofunction için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="627af-143">Active Directory is required on hello DR site for Dynamics AX application toofunction.</span></span> <span data-ttu-id="627af-144">Merhaba müşterinin şirket içi ortamına hello kapsamına bağlı iki önerilen seçenek vardır.</span><span class="sxs-lookup"><span data-stu-id="627af-144">There are two recommended choices based on hello complexity of hello customer’s on-premises environment.</span></span>

<span data-ttu-id="627af-145">**Seçenek 1**</span><span class="sxs-lookup"><span data-stu-id="627af-145">**Option 1**</span></span>

<span data-ttu-id="627af-146">Hello müşteri varsa, az sayıda uygulamayı ve onun tüm tek etki alanı denetleyicisi şirket içi site ve ASR çoğaltma tooreplicate hello DC makine toosecondary site (kullanmanızı öneririz sonra hello tüm site birlikte başarısız olması Geçerli Site tooSite ve Site tooAzure için).</span><span class="sxs-lookup"><span data-stu-id="627af-146">If hello customer has a small number of applications and a single domain controller for his entire on-premises site and will be failing over hello entire site together, then we recommend using ASR-Replication tooreplicate hello DC machine toosecondary site (applicable for both Site tooSite and Site tooAzure).</span></span>

<span data-ttu-id="627af-147">**Seçenek 2**</span><span class="sxs-lookup"><span data-stu-id="627af-147">**Option 2**</span></span>

<span data-ttu-id="627af-148">Merhaba müşteri uygulamalar çok sayıda sahip bir Active Directory ormanı çalıştıran ve yük birkaç uygulamalar aynı anda devretme durumunda hello DR sitesi ek etki alanı denetleyicisinde ayarlama öneririz (ikincil site veya Azure).</span><span class="sxs-lookup"><span data-stu-id="627af-148">If hello customer has a large number of applications and is running an Active Directory forest and will fail-over few applications at a time, then we recommend setting up an additional domain controller on hello DR site (secondary site or in Azure).</span></span>

<span data-ttu-id="627af-149">Lütfen çok başvurun[bir etki alanı denetleyicisi DR sitede kullanılabilir hale getirme üzerinde yardımcı kılavuz](site-recovery-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="627af-149">Please refer too[companion guide on making a domain controller available on DR site](site-recovery-active-directory.md).</span></span> <span data-ttu-id="627af-150">Bu belgenin geri kalanında için DC DR sitesinden edinilebilir varsayacağız.</span><span class="sxs-lookup"><span data-stu-id="627af-150">For remainder of this document we will assume a DC is available on DR site.</span></span>

### <a name="2-setup-sql-server-replication"></a><span data-ttu-id="627af-151">2. SQL Server çoğaltması Kurulumu</span><span class="sxs-lookup"><span data-stu-id="627af-151">2. Setup SQL Server replication</span></span>
<span data-ttu-id="627af-152">Lütfen koruma seçeneği önerilen hello ayrıntılı teknik kılavuzluk etmesi için toocompanion Kılavuzu başvurun [SQL katmanı](site-recovery-sql.md).</span><span class="sxs-lookup"><span data-stu-id="627af-152">Please refer toocompanion guide  for detailed technical guidance on hello recommended option for protecting [SQL tier](site-recovery-sql.md).</span></span>

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a><span data-ttu-id="627af-153">3. Dynamics AX İstemcisi ve AOS VM'ler için korumayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="627af-153">3. Enable protection for Dynamics AX client and AOS VMs</span></span>
<span data-ttu-id="627af-154">Olup hello VM'ler dağıtılan üzerinde temel ilgili Azure Site Recovery yapılandırmasını gerçekleştirmek [Hyper-V](site-recovery-hyper-v-site-to-azure.md) veya [VMware](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="627af-154">Perform relevant Azure Site Recovery configuration based on whether hello VMs are deployed on [Hyper-V](site-recovery-hyper-v-site-to-azure.md) or on [VMware](site-recovery-vmware-to-azure.md).</span></span>

> [!TIP]
> <span data-ttu-id="627af-155">Önerilen kilitlenme tutarlı sıklığı tooconfigure 15 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="627af-155">Recommended Crash consistent frequency tooconfigure is 15 minutes.</span></span>
>

<span data-ttu-id="627af-156">Anlık görüntü aşağıda Hello 'VMware sitesi tooAzure' koruma senaryoda Dynamics bileşen VM'ler hello koruma durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="627af-156">hello below snapshot shows hello protection status of Dynamics component VMs in ‘VMware site tooAzure’ protection scenario.</span></span>
<span data-ttu-id="627af-157">![Korumalı öğeler](./media/site-recovery-dynamics-ax/protecteditems.png)</span><span class="sxs-lookup"><span data-stu-id="627af-157">![Protected items ](./media/site-recovery-dynamics-ax/protecteditems.png)</span></span>

### <a name="4-configure-networking"></a><span data-ttu-id="627af-158">4. Ağı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="627af-158">4. Configure Networking</span></span>
<span data-ttu-id="627af-159">VM yapılandırma işlem ve ağ ayarları</span><span class="sxs-lookup"><span data-stu-id="627af-159">Configure VM Compute and Network Settings</span></span>

<span data-ttu-id="627af-160">Merhaba VM ağları, yük devretme sonrasında ekli toohello doğru DR ağ elde etmeniz hello AX İstemcisi ve AOS VM'ler için Azure Site Recovery ağ ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="627af-160">For hello AX client and AOS VMs configure network settings in Azure Site Recovery so that hello VM networks get attached toohello right DR network after failover.</span></span> <span data-ttu-id="627af-161">Bu katmanlar için Hello DR ağ yönlendirilebilir toohello SQL katmanı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="627af-161">Ensure hello DR network for these tiers is routable toohello SQL tier.</span></span>

<span data-ttu-id="627af-162">Seçebileceğiniz hello hello VM çoğaltılan öğeler tooconfigure hello ağ ayarlarını aşağıdaki hello anlık görüntüde gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="627af-162">You can select hello VM in hello replicated items tooconfigure hello network settings as shown in hello snapshot below.</span></span>

* <span data-ttu-id="627af-163">AOS sunucuları hello doğru kullanılabilirlik kümesi seçin.</span><span class="sxs-lookup"><span data-stu-id="627af-163">For AOS servers select hello correct availability set.</span></span>

* <span data-ttu-id="627af-164">Bir statik IP kullanarak yeniden hello içinde sanal makine tootake hello istediğiniz hello IP belirtin **hedef IP** alan ![ağ ayarları](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span><span class="sxs-lookup"><span data-stu-id="627af-164">If you are using a static IP then specify hello IP that you want hello virtual machine tootake in hello **Target IP** field ![Network Settings ](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span></span>



### <a name="5-creating-a-recovery-plan"></a><span data-ttu-id="627af-165">5. Bir kurtarma planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="627af-165">5. Creating a recovery plan</span></span>

<span data-ttu-id="627af-166">Azure Site Recovery tooautomate hello yük devretme işleminde bir kurtarma planı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="627af-166">You can create a recovery plan in Azure Site Recovery tooautomate hello failover process.</span></span> <span data-ttu-id="627af-167">Uygulama katmanı ve web katmanı hello Kurtarma planlaması ekleyin.</span><span class="sxs-lookup"><span data-stu-id="627af-167">Add app tier and web tier in hello Recovery Plan.</span></span> <span data-ttu-id="627af-168">Uygulama katmanı önce ön uç kapatma hello için bunları farklı gruplarda sıralayın.</span><span class="sxs-lookup"><span data-stu-id="627af-168">Order them in different groups so that hello front-end shutdown before app tier.</span></span>

1)  <span data-ttu-id="627af-169">Aboneliğinizde Hello Azure Site Recovery kasası seçin ve 'Kurtarma planları' kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="627af-169">Select hello Azure Site Recovery vault in your subscription and click on ‘Recovery Plans’ tile.</span></span>

2)  <span data-ttu-id="627af-170">Tıklayın ' + kurtarma planı ve bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="627af-170">Click on ‘+ Recovery plan and specify a name.</span></span>

3)  <span data-ttu-id="627af-171">Merhaba 'Source' ve 'Target' seçin.</span><span class="sxs-lookup"><span data-stu-id="627af-171">Select hello ‘Source’ and ‘Target’.</span></span> <span data-ttu-id="627af-172">Merhaba hedef Azure veya ikincil site olabilir.</span><span class="sxs-lookup"><span data-stu-id="627af-172">hello target can be Azure or secondary site.</span></span> <span data-ttu-id="627af-173">Azure seçtiğiniz durumda hello dağıtım modelini belirtin</span><span class="sxs-lookup"><span data-stu-id="627af-173">In case you choose Azure, you must specify hello deployment model</span></span>

![Kurtarma planı oluşturun](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  <span data-ttu-id="627af-175">Merhaba AOS ve istemci VM'ler toohello kurtarma planı seçin ve ✓'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="627af-175">Select hello AOS and client VMs toohello recovery plan and click ✓.</span></span>
<span data-ttu-id="627af-176">![Kurtarma planı oluşturun](./media/site-recovery-dynamics-ax/selectvms.png)</span><span class="sxs-lookup"><span data-stu-id="627af-176">![Create Recovery Plan](./media/site-recovery-dynamics-ax/selectvms.png)</span></span>


![Kurtarma planı](./media/site-recovery-dynamics-ax/recoveryplan.png)

<span data-ttu-id="627af-178">Aşağıda açıklandığı gibi çeşitli adımları ekleyerek hello kurtarma planı Dynamics AX uygulama için özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="627af-178">You can customize hello recovery plan for Dynamics AX application by adding various steps as detailed below.</span></span> <span data-ttu-id="627af-179">Anlık görüntü yukarıda Hello hello adımların tümünü ekledikten sonra hello tam kurtarma planı gösterir.</span><span class="sxs-lookup"><span data-stu-id="627af-179">hello above snapshot shows hello complete recovery plan after adding all hello steps.</span></span>

<span data-ttu-id="627af-180">*Adımlar:*</span><span class="sxs-lookup"><span data-stu-id="627af-180">*Steps:*</span></span>

<span data-ttu-id="627af-181">*1. SQL Server üzerinde adımları başarısız*</span><span class="sxs-lookup"><span data-stu-id="627af-181">*1. SQL Server fail over steps*</span></span>

<span data-ttu-id="627af-182">Çok başvuran['SQL Server DR çözüm'](site-recovery-sql.md) kurtarma adımları belirli tooSQL sunucu hakkındaki ayrıntılar için yardımcı kılavuz.</span><span class="sxs-lookup"><span data-stu-id="627af-182">Refer too[‘SQL Server DR Solution’](site-recovery-sql.md) companion guide  for details about recovery steps specific tooSQL server.</span></span>

<span data-ttu-id="627af-183">*2. Yük devretme Grup 1: hello AOS VM'ler başarısız*</span><span class="sxs-lookup"><span data-stu-id="627af-183">*2. Failover Group 1: Fail over hello AOS VMs*</span></span>

<span data-ttu-id="627af-184">Seçili hello kurtarma noktası olası toohello veritabanı PIT olarak Kapat ancak değil şimdi olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="627af-184">Make sure that hello recovery point selected is as close as possible toohello database PIT but not ahead.</span></span>

<span data-ttu-id="627af-185">*3. Komut dosyası: Ekle yük dengeleyici (yalnızca E-A)* tooadd bir yük dengeleyici tooit gelen AOS VM gruptan sonra bir komut dosyası (aracılığıyla Azure Otomasyonu) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="627af-185">*3. Script: Add load balancer (Only E-A)* Add a script (via Azure automation) after AOS VM group comes up tooadd a load balancer tooit.</span></span> <span data-ttu-id="627af-186">Bu görev bir betiği toodo kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="627af-186">You can use a script toodo this task.</span></span> <span data-ttu-id="627af-187">Makale başvuran [nasıl tooadd yük dengeleyici çok katmanlı uygulama DR için](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span><span class="sxs-lookup"><span data-stu-id="627af-187">Refer article [how tooadd load balancer for multi-tier application DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span></span>

<span data-ttu-id="627af-188">*4. Yük devretme Grup 2: hello AX İstemcisi VM'ler başarısız.*</span><span class="sxs-lookup"><span data-stu-id="627af-188">*4. Failover Group 2: Fail over hello AX client VMs.*</span></span>
<span data-ttu-id="627af-189">Merhaba web katmanı VM'ler hello kurtarma planının bir parçası olarak yük devri.</span><span class="sxs-lookup"><span data-stu-id="627af-189">Fail over hello web tier VMs as part of hello recovery plan.</span></span>


### <a name="doing-a-test-failover"></a><span data-ttu-id="627af-190">Yük devretme sınamasını yapmak</span><span class="sxs-lookup"><span data-stu-id="627af-190">Doing a test failover</span></span>

<span data-ttu-id="627af-191">Too'AD DR çözüm başvuran ' ve 'SQL Server DR çözüm' yardımcı Kılavuzlar konuları belirli tooAD ve SQL server yük devretme testi sırasında sırasıyla için.</span><span class="sxs-lookup"><span data-stu-id="627af-191">Refer too‘AD DR Solution ’ and ‘SQL Server DR solution ’ companion guides for considerations specific tooAD and SQL server respectively during Test Failover.</span></span>

1.  <span data-ttu-id="627af-192">TooAzure portal gidin ve Site Recovery kasanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="627af-192">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="627af-193">Dynamics AX için oluşturduğunuz hello kurtarma planı tıklayın.</span><span class="sxs-lookup"><span data-stu-id="627af-193">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="627af-194">'Test yük devretme üzerinde' tıklayın.</span><span class="sxs-lookup"><span data-stu-id="627af-194">Click on ‘Test Failover’.</span></span>
4.  <span data-ttu-id="627af-195">Merhaba sanal ağ toostart hello test yük devretme işlemini seçin.</span><span class="sxs-lookup"><span data-stu-id="627af-195">Select hello virtual network toostart hello test fail-over process.</span></span>
5.  <span data-ttu-id="627af-196">Merhaba ikincil ortamı kurma olduğunda, doğrulama gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="627af-196">Once hello secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="627af-197">Hello doğrulama tamamlandıktan sonra 'Doğrulamaları tamamlamak' seçin ve yük devretme sınama ortamı hello temizlenecek.</span><span class="sxs-lookup"><span data-stu-id="627af-197">Once hello validations are complete, you can select ‘Validations complete’ and hello test failover environment will be cleaned.</span></span>

<span data-ttu-id="627af-198">İzleyin [bu kılavuz](site-recovery-test-failover-to-azure.md) toodo yük devretme sınaması.</span><span class="sxs-lookup"><span data-stu-id="627af-198">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

### <a name="doing-a-failover"></a><span data-ttu-id="627af-199">Bir yük devretme işleminden</span><span class="sxs-lookup"><span data-stu-id="627af-199">Doing a failover</span></span>

1.  <span data-ttu-id="627af-200">TooAzure portal gidin ve Site Recovery kasanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="627af-200">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="627af-201">Dynamics AX için oluşturduğunuz hello kurtarma planı tıklayın.</span><span class="sxs-lookup"><span data-stu-id="627af-201">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="627af-202">'Üzerinde yük devretme' tıklatın ve 'Failover' seçin.</span><span class="sxs-lookup"><span data-stu-id="627af-202">Click on ‘Failover’ and select ‘ Failover’.</span></span>
4.  <span data-ttu-id="627af-203">Merhaba hedef ağ seçin ve ✓ toostart hello yük devretme işlemi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="627af-203">Select hello target network and click ✓ toostart hello failover process.</span></span>

<span data-ttu-id="627af-204">İzleyin [bu kılavuz](site-recovery-failover.md) , yaparken bir yük devretme.</span><span class="sxs-lookup"><span data-stu-id="627af-204">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

### <a name="perform-a-failback"></a><span data-ttu-id="627af-205">Bir yeniden çalışma gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="627af-205">Perform a Failback</span></span>

<span data-ttu-id="627af-206">Too'SQL sunucu DR çözüm başvuran ' yeniden çalışma sırasında dikkat edilecek noktalar belirli tooSQL sunucusu için yardımcı kılavuz.</span><span class="sxs-lookup"><span data-stu-id="627af-206">Refer too‘SQL Server DR Solution ’ companion guide for considerations specific tooSQL server during Failback.</span></span>

1.  <span data-ttu-id="627af-207">TooAzure portal gidin ve Site Recovery kasanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="627af-207">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="627af-208">Dynamics AX için oluşturduğunuz hello kurtarma planı tıklayın.</span><span class="sxs-lookup"><span data-stu-id="627af-208">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="627af-209">'Üzerinde yük devretme' tıklayın ve yük devretme seçin.</span><span class="sxs-lookup"><span data-stu-id="627af-209">Click on ‘Failover’ and select failover.</span></span>
4.  <span data-ttu-id="627af-210">'Üzerinde değişiklik yön' seçeneğini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="627af-210">Click on ‘Change Direction’.</span></span>
5.  <span data-ttu-id="627af-211">Merhaba uygun seçenekleri - veri eşitleme ve VM oluşturma seçeneklerini belirtin</span><span class="sxs-lookup"><span data-stu-id="627af-211">Select hello appropriate options - data synchronization and VM creation options</span></span>
6.  <span data-ttu-id="627af-212">✓ toostart hello 'Yeniden çalışma' işlemi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="627af-212">Click ✓ toostart hello ‘Failback’ process.</span></span>


<span data-ttu-id="627af-213">İzleyin [bu kılavuz](site-recovery-failback-azure-to-vmware.md) , yaparken bir yeniden çalışma.</span><span class="sxs-lookup"><span data-stu-id="627af-213">Follow [this guidance](site-recovery-failback-azure-to-vmware.md) when you are doing a failback.</span></span>

##<a name="summary"></a><span data-ttu-id="627af-214">Özet</span><span class="sxs-lookup"><span data-stu-id="627af-214">Summary</span></span>
<span data-ttu-id="627af-215">Azure Site Recovery kullanarak, Dynamics AX uygulamanız için bir tam otomatik olağanüstü durum kurtarma planı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="627af-215">Using Azure Site Recovery, you can create a complete automated disaster recovery plan for your Dynamics AX application.</span></span> <span data-ttu-id="627af-216">Her yerden saniye içinde hello yük devretme başlatabilirsiniz hello kesilme olayı ve dakika içinde çalışır durumda hello uygulama alın.</span><span class="sxs-lookup"><span data-stu-id="627af-216">You can initiate hello failover within seconds from anywhere in hello event of a disruption and get hello application up and running in minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="627af-217">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="627af-217">Next steps</span></span>
<span data-ttu-id="627af-218">Okuma [hangi iş yüklerini koruyabilirim?](site-recovery-workload.md) toolearn Azure Site Recovery ile kurumsal iş yüklerini koruma hakkında daha fazla.</span><span class="sxs-lookup"><span data-stu-id="627af-218">Read [What workloads can I protect?](site-recovery-workload.md) toolearn more about protecting enterprise workloads with Azure Site Recovery.</span></span>
