---
title: "aaaReplicate uygulamaları (Azure tooAzure) | Microsoft Docs"
description: "Çalışan nasıl tooset çoğaltma, sanal makineleri bu makalede bir Azure bölgesindeki Azure çok başka bir bölgede."
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 5/22/2017
ms.author: asgang
ms.openlocfilehash: fb190dac14419f892a1c6b45a3d991d8005e4bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-virtual-machines-tooanother-azure-region"></a><span data-ttu-id="b1baa-103">Azure sanal makineleri tooanother Azure bölgesi Çoğalt</span><span class="sxs-lookup"><span data-stu-id="b1baa-103">Replicate Azure virtual machines tooanother Azure region</span></span>



>[!NOTE]
>
> <span data-ttu-id="b1baa-104">Azure sanal makineler için Site Recovery çoğaltma şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="b1baa-104">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>

<span data-ttu-id="b1baa-105">Çalışan nasıl tooset çoğaltma, sanal makineleri bu makalede bir Azure bölgesi tooanother Azure bölgesi içinde.</span><span class="sxs-lookup"><span data-stu-id="b1baa-105">This article describes how tooset up replication of virtual machines running in one Azure region tooanother Azure region.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1baa-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b1baa-106">Prerequisites</span></span>

* <span data-ttu-id="b1baa-107">Merhaba makale zaten Site kurtarma ve kurtarma Hizmetleri kasası hakkında bildiğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="b1baa-107">hello article assumes that you already know about Site Recovery and Recovery Services Vault.</span></span> <span data-ttu-id="b1baa-108">Toohave oluşturulan bir 'Kurtarma Hizmetleri Kasası' öncesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1baa-108">You need toohave a 'Recovery services vault' pre created.</span></span>

    >[!NOTE]
    >
    > <span data-ttu-id="b1baa-109">Sanal makineleri tooreplicate istediğiniz hello konumda 'Kurtarma Hizmetleri Kasası' hello oluşturmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="b1baa-109">It is recommended that you create hello 'Recovery services vault' in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="b1baa-110">Örneğin, hedef konumu 'Orta ABD' ise 'Orta ABD' kasası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b1baa-110">For example, if your target location is 'Central US', create vault in 'Central US'.</span></span>

* <span data-ttu-id="b1baa-111">Hello Azure Vm'leri üzerinde ağ güvenlik grupları (NSG) kuralları veya güvenlik duvarı proxy toocontrol erişim toooutbound internet bağlantısı kullanıyorsanız, bu, beyaz liste hello gerekli URL'leri veya IP'leri emin olun.</span><span class="sxs-lookup"><span data-stu-id="b1baa-111">If you are using Network Security Groups (NSG) rules or firewall proxy toocontrol access toooutbound internet connectivity on hello Azure VMs, ensure that you whitelist hello required URLs or IPs.</span></span> <span data-ttu-id="b1baa-112">Çok başvuran[Ağ Kılavuzu belge](./site-recovery-azure-to-azure-networking-guidance.md) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="b1baa-112">Refer too[Networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md) for more details.</span></span>

* <span data-ttu-id="b1baa-113">Bir ExpressRoute veya şirket içi ve hello arasında bir VPN bağlantısı varsa, kaynak Azure konumda, izleyin [Site kurtarma değerlendirmeleri Azure tooon içi ExpressRoute / VPN Yapılandırması](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) belge.</span><span class="sxs-lookup"><span data-stu-id="b1baa-113">If you have an ExpressRoute or a VPN connection between on-premises and hello source location in Azure, follow [Site Recovery Considerations for Azure tooon-premises ExpressRoute / VPN configuration](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span></span>

* <span data-ttu-id="b1baa-114">Azure kullanıcı hesabınızın toohave belirli gereken [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) bir Azure sanal makinesinin tooenable çoğaltma.</span><span class="sxs-lookup"><span data-stu-id="b1baa-114">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>

* <span data-ttu-id="b1baa-115">Azure aboneliğinizde etkin toocreate VM'ler olmalıdır hello hedef konumda DR bölge olarak toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="b1baa-115">Your Azure subscription should be enabled toocreate VMs in hello target location you want toouse as DR region.</span></span> <span data-ttu-id="b1baa-116">Destek tooenable hello gerekli kota başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1baa-116">You can contact support tooenable hello required quota.</span></span>

## <a name="enable-replication-from-azure-site-recovery-vault"></a><span data-ttu-id="b1baa-117">Azure Site Recovery kasası çoğaltmayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="b1baa-117">Enable replication from Azure Site Recovery vault</span></span>
<span data-ttu-id="b1baa-118">Bu çizim için biz hello 'Doğu Asya' Azure konumu toohello ' Güneydoğu Asya ' konumu çalıştıran VM'ler çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="b1baa-118">For this illustration, we will replicate VMs running  in hello ‘East Asia’ Azure location toohello ‘South East Asia’ location.</span></span> <span data-ttu-id="b1baa-119">Merhaba adımlar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="b1baa-119">hello steps are as follows:</span></span>

 <span data-ttu-id="b1baa-120">Tıklatın **+ Çoğalt** hello kasa tooenable çoğaltma hello sanal makineler için.</span><span class="sxs-lookup"><span data-stu-id="b1baa-120">Click **+Replicate** in hello vault tooenable replication for hello virtual machines.</span></span>

1. <span data-ttu-id="b1baa-121">**Kaynak:** toohello noktası bu durumda olan kaynak hello makinelerin başvurduğu **Azure**.</span><span class="sxs-lookup"><span data-stu-id="b1baa-121">**Source:** It refers toohello point of origin of hello machines which in this case is **Azure**.</span></span>

2. <span data-ttu-id="b1baa-122">**Kaynak Konum:** tooprotect sanal makinelerinizi nereye istediğiniz Azure bölgesini hello değil.</span><span class="sxs-lookup"><span data-stu-id="b1baa-122">**Source location:** It is hello Azure region from where you want tooprotect your virtual machines.</span></span> <span data-ttu-id="b1baa-123">Bu çizim için 'Doğu Asya' hello kaynak konumu olacaktır</span><span class="sxs-lookup"><span data-stu-id="b1baa-123">For this illustration, hello source location will be 'East Asia'</span></span>

3. <span data-ttu-id="b1baa-124">**Dağıtım modeli:** toohello Azure dağıtım modeli hello kaynak makinelerin başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="b1baa-124">**Deployment model:** It refers toohello Azure deployment model of hello source machines.</span></span> <span data-ttu-id="b1baa-125">Her iki Klasik seçebilir veya Kaynak Yöneticisi ve toohello modele ait makineler hello sonraki adımda koruma için listelenir.</span><span class="sxs-lookup"><span data-stu-id="b1baa-125">You can select either classic or resource manager and machines belonging toohello specific model will be listed for protection in hello next step.</span></span>

      >[!NOTE]
      >
      > <span data-ttu-id="b1baa-126">Yalnızca klasik bir sanal makine çoğaltabilir ve klasik sanal makine olarak kurtarın.</span><span class="sxs-lookup"><span data-stu-id="b1baa-126">You can only replicate a classic virtual machine and recover it as a classic virtual machine.</span></span> <span data-ttu-id="b1baa-127">Resource Manager sanal makine olarak kurtaramazsınız.</span><span class="sxs-lookup"><span data-stu-id="b1baa-127">You cannot recover it as a Resource Manager virtual machine.</span></span>

4. <span data-ttu-id="b1baa-128">**Kaynak grubu:** kaynak sanal makinelerinizi ait hello kaynak grubu toowhich kullanıcının.</span><span class="sxs-lookup"><span data-stu-id="b1baa-128">**Resource Group:** It’s hello resource group toowhich your source virtual machines belong.</span></span> <span data-ttu-id="b1baa-129">Merhaba sonraki adımda koruma için tüm hello VM'ler hello seçili kaynak grubu altında listelenir.</span><span class="sxs-lookup"><span data-stu-id="b1baa-129">All hello VMs under hello selected resource group will be listed for protection in hello next step.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

<span data-ttu-id="b1baa-131">İçinde **sanal makineleri > sanal makine Seç**, tıklatın ve tooreplicate istediğiniz her bir makine seçin.</span><span class="sxs-lookup"><span data-stu-id="b1baa-131">In **Virtual Machines > Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="b1baa-132">Yalnızca çoğaltmanın etkinleştirildiği makineleri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1baa-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="b1baa-133">Daha sonra Tamam'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b1baa-133">Then click OK.</span></span>
    <span data-ttu-id="b1baa-134">![Çoğaltmayı etkinleştirme](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span><span class="sxs-lookup"><span data-stu-id="b1baa-134">![Enable replication](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span></span>


<span data-ttu-id="b1baa-135">Ayarları bölümü altında hedef site özelliklerini yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1baa-135">Under Settings section you can configure target site properties</span></span>

1. <span data-ttu-id="b1baa-136">**Hedef konumu:** bu burada kaynak sanal makine verilerinizi çoğaltılabilir hello konumdur.</span><span class="sxs-lookup"><span data-stu-id="b1baa-136">**Target Location:**  This is hello location where your source virtual machine data will be replicated.</span></span> <span data-ttu-id="b1baa-137">Seçili makineler konumuna bağlı olarak, Site Recovery uygun hedef bölgelerin listesi hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="b1baa-137">Depending upon your selected machines location, Site Recovery will provide you hello list of suitable target regions.</span></span>

    > [!TIP]
    > <span data-ttu-id="b1baa-138">Tookeep hedef konumu önerilen aynı itibariyle, Kurtarma Hizmetleri kasası.</span><span class="sxs-lookup"><span data-stu-id="b1baa-138">It is recommended tookeep target location same as of your recovery services vault.</span></span>

2. <span data-ttu-id="b1baa-139">**Hedef kaynak grubu:** tüm çoğaltılmış sanal makinelere ait olur hello kaynak grubu toowhich değil. Varsayılan olarak ASR yeni bir kaynak grubu hello hedef bölgede "asr" sonekine sahip adıyla oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b1baa-139">**Target resource group :** It is hello resource group toowhich all your replicated virtual machines will belong.By default ASR will create a new resource group in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="b1baa-140">ASR tarafından önceden oluşturulmuş kaynak grubu mevcut olmaması durumunda, yeniden kullanılır. Toocustomize de seçebilirsiniz, hello bölümünde aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="b1baa-140">In case resource group created by ASR already exist, it will be reused.You can also choose toocustomize it as shown in hello section below.</span></span>    
3. <span data-ttu-id="b1baa-141">**Hedef sanal ağ:** varsayılan olarak, ASR yeni bir sanal ağ hello hedef bölgede "asr" sonekine sahip adıyla oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b1baa-141">**Target Virtual Network:** By default, ASR will create a new virtual network in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="b1baa-142">Bu eşlenen tooyour kaynak ağ olacaktır ve gelecekteki tüm koruma için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b1baa-142">This will be mapped tooyour source network and will be used for any future protection.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b1baa-143">[Ağ ayrıntıları denetlemek](site-recovery-network-mapping-azure-to-azure.md) tooknow ağ eşlemesi hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="b1baa-143">[Check networking details](site-recovery-network-mapping-azure-to-azure.md) tooknow more about network mapping.</span></span>

4. <span data-ttu-id="b1baa-144">**Depolama hesapları hedef:** varsayılan olarak, ASR kaynak VM depolama yapılandırmanızı mimicking hello yeni hedef depolama hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b1baa-144">**Target Storage accounts:** By default, ASR will create hello new target storage account mimicking your source VM storage configuration.</span></span> <span data-ttu-id="b1baa-145">ASR tarafından önceden oluşturulmuş depolama hesabı mevcut olmaması durumunda, yeniden kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b1baa-145">In case storage account created by ASR already exist, it will be reused.</span></span>

5. <span data-ttu-id="b1baa-146">**Depolama hesapları önbelleğe:** ASR önbellek depolama hello kaynak bölgede adlı ek depolama alanı hesabı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="b1baa-146">**Cache Storage accounts:** ASR needs extra storage account called cache storage in hello source region.</span></span> <span data-ttu-id="b1baa-147">Tüm kaynak VM'ler izlenen ve bu toohello hedef konumu çoğaltma önce toocache depolama hesabı gönderilen üzerinde hello gerçekleştiği değişiklikleri hello.</span><span class="sxs-lookup"><span data-stu-id="b1baa-147">All hello changes happening on hello source VMs are tracked and sent toocache storage account before replicating those toohello target location.</span></span>

6. <span data-ttu-id="b1baa-148">**Kullanılabilirlik kümesi:** varsayılan olarak, ASR hello hedef bölgede kümesi "asr" sonekine sahip adı ile yeni bir kullanılabilirlik oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b1baa-148">**Availability set :** By default, ASR will create a new availability set in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="b1baa-149">Kullanılabilirlik kümesi zaten ASR tarafından oluşturulan mevcut olmaması durumunda, yeniden kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b1baa-149">In case availability set created by ASR already exist, it will be reused.</span></span>

7.  <span data-ttu-id="b1baa-150">**Çoğaltma İlkesi:** kurtarma noktası bekletme geçmişi ve uygulama tutarlılığı anlık görüntü sıklığı hello ayarlarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b1baa-150">**Replication Policy:** It defines hello settings for recovery point retention history and app consistent snapshot frequency.</span></span> <span data-ttu-id="b1baa-151">Varsayılan olarak, ASR ' 24 saattir kurtarma noktası bekletme ve ' 60 dakika uygulama tutarlılığı anlık görüntü sıklığı için varsayılan ayarlarla yeni bir çoğaltma ilkesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b1baa-151">By default, ASR will create a new replication policy with default settings of ‘24 hours’ for recovery point retention and ’60 minutes’ for app consistent snapshot frequency.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a><span data-ttu-id="b1baa-153">Hedef kaynakları özelleştirme</span><span class="sxs-lookup"><span data-stu-id="b1baa-153">Customize target resources</span></span>

<span data-ttu-id="b1baa-154">ASR tarafından kullanılan toochange hello Varsayılanları olasılığına gereksinimlerinize göre hello ayarlarını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1baa-154">In case you want toochange hello defaults used by ASR, you can change hello settings based on your needs.</span></span>

1. <span data-ttu-id="b1baa-155">**Özelleştir:** toochange tıklatın hello varsayılanlar ASR tarafından kullanıldı.</span><span class="sxs-lookup"><span data-stu-id="b1baa-155">**Customize:** Click it toochange hello defaults used by ASR.</span></span>

2. <span data-ttu-id="b1baa-156">**Hedef kaynak grubu:** hello abonelik içindeki hello hedef konumda var olan tüm hello kaynak gruplarının hello listeden hello kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="b1baa-156">**Target resource group :**  You can select hello resource group from hello list of all hello resource groups existing in hello target location within hello subscription.</span></span>

3. <span data-ttu-id="b1baa-157">**Hedef sanal ağ:** hello hedef konumda bulunan tüm hello sanal ağ hello listesini bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1baa-157">**Target Virtual Network:** You can find hello list of all hello virtual network in hello target location.</span></span>

4. <span data-ttu-id="b1baa-158">**Kullanılabilirlik kümesi:** kullanılabilirlik kaynak bölgede bir parçası olan kullanılabilirlik kümeleri ayarları toohello sanal makineleri yalnızca ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1baa-158">**Availability set :** You can only add availability sets settings toohello virtual machines which are a part of availability in source region.</span></span>

5. <span data-ttu-id="b1baa-159">**Hedef depolama hesapları:**</span><span class="sxs-lookup"><span data-stu-id="b1baa-159">**Target Storage accounts:**</span></span>

<span data-ttu-id="b1baa-160">![Çoğaltmayı etkinleştirme](./media/site-recovery-replicate-azure-to-azure/customize.PNG) tıklayın **hedef kaynak oluşturma** ve çoğaltmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="b1baa-160">![Enable replication](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Click on **Create target resource** and Enable Replication</span></span>


<span data-ttu-id="b1baa-161">Korunan sanal makine sonra hello altında VM'ler sağlık durumunu kontrol edebilirsiniz **çoğaltılan öğeler**</span><span class="sxs-lookup"><span data-stu-id="b1baa-161">Once virtual machines are protected you can check hello status of VMs health under **Replicated items**</span></span>

>[!NOTE]
><span data-ttu-id="b1baa-162">Başlangıç sırasında zaman toorefresh durumunu alır ve bir süre için ilerleme görmüyorsanız olasılığı, ilk çoğaltma başlatılamadı.</span><span class="sxs-lookup"><span data-stu-id="b1baa-162">During hello time of initial replication there could a possibility that status takes time toorefresh and you don't see progress for some time.</span></span> <span data-ttu-id="b1baa-163">Merhaba dikey tooget hello en son durum hello üstte hello Yenile düğmesini tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1baa-163">You can click hello Refresh button on hello top of hello blade tooget hello latest status.</span></span>
>

![Çoğaltmayı etkinleştirme](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a><span data-ttu-id="b1baa-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b1baa-165">Next steps</span></span>
- <span data-ttu-id="b1baa-166">[Daha fazla bilgi edinin](site-recovery-test-failover-to-azure.md) yük devretme testi çalıştırma hakkında.</span><span class="sxs-lookup"><span data-stu-id="b1baa-166">[Learn more](site-recovery-test-failover-to-azure.md) about running a test failover.</span></span>
- <span data-ttu-id="b1baa-167">[Daha fazla bilgi edinin](site-recovery-failover.md) yerine, farklı türlerde hakkında ve nasıl toorun bunları.</span><span class="sxs-lookup"><span data-stu-id="b1baa-167">[Learn more](site-recovery-failover.md) about different types of failovers, and how toorun them.</span></span>
- <span data-ttu-id="b1baa-168">Daha fazla bilgi edinmek [kurtarma planlarına kullanarak](site-recovery-create-recovery-plans.md) tooreduce RTO.</span><span class="sxs-lookup"><span data-stu-id="b1baa-168">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
- <span data-ttu-id="b1baa-169">Daha fazla bilgi edinmek [Azure sanal makineleri yeniden korumayı](site-recovery-how-to-reprotect.md) yük devretme sonrasında.</span><span class="sxs-lookup"><span data-stu-id="b1baa-169">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>
