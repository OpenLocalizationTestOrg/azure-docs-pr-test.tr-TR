---
title: "Uygulamaları (Azure için Azure) çoğaltmak | Microsoft Docs"
description: "Bu makalede, azure'da başka bir bölge için bir Azure bölgesinde çalışan sanal makinelerin çoğaltmasını ayarlama açıklar."
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
ms.openlocfilehash: f9f97cf840b722c8cfee169dd1640e0682f287ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-virtual-machines-to-another-azure-region"></a><span data-ttu-id="7fb92-103">Başka bir Azure bölgesine çoğaltma Azure sanal makineler</span><span class="sxs-lookup"><span data-stu-id="7fb92-103">Replicate Azure virtual machines to another Azure region</span></span>



>[!NOTE]
>
> <span data-ttu-id="7fb92-104">Azure sanal makineler için Site Recovery çoğaltma şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="7fb92-104">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>

<span data-ttu-id="7fb92-105">Bu makalede, başka bir Azure bölgesine bir Azure bölgesinde çalışan sanal makinelerin çoğaltmasını ayarlama açıklar.</span><span class="sxs-lookup"><span data-stu-id="7fb92-105">This article describes how to set up replication of virtual machines running in one Azure region to another Azure region.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fb92-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7fb92-106">Prerequisites</span></span>

* <span data-ttu-id="7fb92-107">Makaleyi zaten Site kurtarma ve kurtarma Hizmetleri kasası hakkında bildiğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="7fb92-107">The article assumes that you already know about Site Recovery and Recovery Services Vault.</span></span> <span data-ttu-id="7fb92-108">Oluşturulan bir 'Kurtarma Hizmetleri Kasası' öncesi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fb92-108">You need to have a 'Recovery services vault' pre created.</span></span>

    >[!NOTE]
    >
    > <span data-ttu-id="7fb92-109">Vm'leriniz çoğaltmak istediğiniz konumu 'Kurtarma Hizmetleri Kasası' oluşturmak önerilir.</span><span class="sxs-lookup"><span data-stu-id="7fb92-109">It is recommended that you create the 'Recovery services vault' in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="7fb92-110">Örneğin, hedef konumu 'Orta ABD' ise 'Orta ABD' kasası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7fb92-110">For example, if your target location is 'Central US', create vault in 'Central US'.</span></span>

* <span data-ttu-id="7fb92-111">Azure vm'lerinde giden internet bağlantısı erişimi denetlemek için ağ güvenlik grupları (NSG) kuralları veya güvenlik duvarı proxy kullanıyorsanız, bu, beyaz liste gerekli URL'leri veya IP'leri.</span><span class="sxs-lookup"><span data-stu-id="7fb92-111">If you are using Network Security Groups (NSG) rules or firewall proxy to control access to outbound internet connectivity on the Azure VMs, ensure that you whitelist the required URLs or IPs.</span></span> <span data-ttu-id="7fb92-112">Başvurmak [Ağ Kılavuzu belge](./site-recovery-azure-to-azure-networking-guidance.md) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="7fb92-112">Refer to [Networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md) for more details.</span></span>

* <span data-ttu-id="7fb92-113">Bir ExpressRoute veya şirket içi ve Azure kaynak konumu arasında bir VPN bağlantısı varsa, izleyin [şirket içi ExpressRoute için Azure Site kurtarma değerlendirmeleri / VPN Yapılandırması](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) belge.</span><span class="sxs-lookup"><span data-stu-id="7fb92-113">If you have an ExpressRoute or a VPN connection between on-premises and the source location in Azure, follow [Site Recovery Considerations for Azure to on-premises ExpressRoute / VPN configuration](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span></span>

* <span data-ttu-id="7fb92-114">Azure kullanıcı hesabınızın belirli sahip olması [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) bir Azure sanal makinesi çoğaltmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="7fb92-114">Your Azure user account needs to have certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of an Azure virtual machine.</span></span>

* <span data-ttu-id="7fb92-115">DR bölge kullanmak istediğiniz hedef konumda VM'ler oluşturmak için Azure aboneliğinizin etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fb92-115">Your Azure subscription should be enabled to create VMs in the target location you want to use as DR region.</span></span> <span data-ttu-id="7fb92-116">Gerekli Kotayı etkinleştirmek için desteğine başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7fb92-116">You can contact support to enable the required quota.</span></span>

## <a name="enable-replication-from-azure-site-recovery-vault"></a><span data-ttu-id="7fb92-117">Azure Site Recovery kasası çoğaltmayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="7fb92-117">Enable replication from Azure Site Recovery vault</span></span>
<span data-ttu-id="7fb92-118">Bu çizim için biz 'Doğu Asya' çalışan sanal makineler çoğaltılacak ' Güneydoğu Asya ' konumuna Azure konumu.</span><span class="sxs-lookup"><span data-stu-id="7fb92-118">For this illustration, we will replicate VMs running  in the ‘East Asia’ Azure location to the ‘South East Asia’ location.</span></span> <span data-ttu-id="7fb92-119">Adımlar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="7fb92-119">The steps are as follows:</span></span>

 <span data-ttu-id="7fb92-120">Tıklatın **+ Çoğalt** sanal makineler için çoğaltmayı etkinleştirmek için kasada.</span><span class="sxs-lookup"><span data-stu-id="7fb92-120">Click **+Replicate** in the vault to enable replication for the virtual machines.</span></span>

1. <span data-ttu-id="7fb92-121">**Kaynak:** , bu durumda olan kaynak makinelerin noktasına başvurduğu **Azure**.</span><span class="sxs-lookup"><span data-stu-id="7fb92-121">**Source:** It refers to the point of origin of the machines which in this case is **Azure**.</span></span>

2. <span data-ttu-id="7fb92-122">**Kaynak Konum:** sanal makinelerinizi korumak istediğiniz Azure bölgesidir.</span><span class="sxs-lookup"><span data-stu-id="7fb92-122">**Source location:** It is the Azure region from where you want to protect your virtual machines.</span></span> <span data-ttu-id="7fb92-123">Bu çizim için kaynak konumu 'Doğu Asya' olacaktır</span><span class="sxs-lookup"><span data-stu-id="7fb92-123">For this illustration, the source location will be 'East Asia'</span></span>

3. <span data-ttu-id="7fb92-124">**Dağıtım modeli:** kaynak makinelerden Azure dağıtım modeline başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="7fb92-124">**Deployment model:** It refers to the Azure deployment model of the source machines.</span></span> <span data-ttu-id="7fb92-125">Her iki Klasik seçebilir veya bir sonraki adımda koruma için kaynak yöneticisi ve belirli modele ait makineler listelenir.</span><span class="sxs-lookup"><span data-stu-id="7fb92-125">You can select either classic or resource manager and machines belonging to the specific model will be listed for protection in the next step.</span></span>

      >[!NOTE]
      >
      > <span data-ttu-id="7fb92-126">Yalnızca klasik bir sanal makine çoğaltabilir ve klasik sanal makine olarak kurtarın.</span><span class="sxs-lookup"><span data-stu-id="7fb92-126">You can only replicate a classic virtual machine and recover it as a classic virtual machine.</span></span> <span data-ttu-id="7fb92-127">Resource Manager sanal makine olarak kurtaramazsınız.</span><span class="sxs-lookup"><span data-stu-id="7fb92-127">You cannot recover it as a Resource Manager virtual machine.</span></span>

4. <span data-ttu-id="7fb92-128">**Kaynak grubu:** kaynak sanal makinelerinizi ait olduğu kaynak grubu değil.</span><span class="sxs-lookup"><span data-stu-id="7fb92-128">**Resource Group:** It’s the resource group to which your source virtual machines belong.</span></span> <span data-ttu-id="7fb92-129">Seçilen kaynak grubundaki tüm sanal makineleri, sonraki adımda koruma için listelenir.</span><span class="sxs-lookup"><span data-stu-id="7fb92-129">All the VMs under the selected resource group will be listed for protection in the next step.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

<span data-ttu-id="7fb92-131">İçinde **sanal makineleri > sanal makine Seç**tıklayın ve çoğaltmak istediğiniz makineleri seçin.</span><span class="sxs-lookup"><span data-stu-id="7fb92-131">In **Virtual Machines > Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="7fb92-132">Yalnızca çoğaltmanın etkinleştirildiği makineleri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7fb92-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="7fb92-133">Daha sonra Tamam'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7fb92-133">Then click OK.</span></span>
    <span data-ttu-id="7fb92-134">![Çoğaltmayı etkinleştirme](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span><span class="sxs-lookup"><span data-stu-id="7fb92-134">![Enable replication](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span></span>


<span data-ttu-id="7fb92-135">Ayarları bölümü altında hedef site özelliklerini yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7fb92-135">Under Settings section you can configure target site properties</span></span>

1. <span data-ttu-id="7fb92-136">**Hedef konumu:** bu burada kaynak sanal makine verilerinizi çoğaltılabilir konumdur.</span><span class="sxs-lookup"><span data-stu-id="7fb92-136">**Target Location:**  This is the location where your source virtual machine data will be replicated.</span></span> <span data-ttu-id="7fb92-137">Seçili makineler konumuna bağlı olarak, Site Recovery, uygun hedef bölgelerin listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="7fb92-137">Depending upon your selected machines location, Site Recovery will provide you the list of suitable target regions.</span></span>

    > [!TIP]
    > <span data-ttu-id="7fb92-138">Hedef konumu tutmanız önerilir aynı itibariyle, Kurtarma Hizmetleri kasası.</span><span class="sxs-lookup"><span data-stu-id="7fb92-138">It is recommended to keep target location same as of your recovery services vault.</span></span>

2. <span data-ttu-id="7fb92-139">**Hedef kaynak grubu:** hangi tüm çoğaltılmış sanal makinelere ait olur kaynak grubu değil. Varsayılan olarak ASR yeni bir kaynak grubu hedef bölgede "asr" sonekine sahip adıyla oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7fb92-139">**Target resource group :** It is the resource group to which all your replicated virtual machines will belong.By default ASR will create a new resource group in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="7fb92-140">ASR tarafından önceden oluşturulmuş kaynak grubu mevcut olmaması durumunda, yeniden kullanılır. Aşağıdaki bölümde gösterildiği gibi özelleştirmek seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7fb92-140">In case resource group created by ASR already exist, it will be reused.You can also choose to customize it as shown in the section below.</span></span>    
3. <span data-ttu-id="7fb92-141">**Hedef sanal ağ:** varsayılan olarak, ASR yeni bir sanal ağ hedef bölgede "asr" sonekine sahip adıyla oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7fb92-141">**Target Virtual Network:** By default, ASR will create a new virtual network in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="7fb92-142">Bu kaynak ağınıza eşlenecek ve gelecekteki tüm koruma için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7fb92-142">This will be mapped to your source network and will be used for any future protection.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7fb92-143">[Ağ ayrıntıları denetlemek](site-recovery-network-mapping-azure-to-azure.md) ağ eşlemesi hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="7fb92-143">[Check networking details](site-recovery-network-mapping-azure-to-azure.md) to know more about network mapping.</span></span>

4. <span data-ttu-id="7fb92-144">**Depolama hesapları hedef:** varsayılan olarak, ASR kaynak VM depolama yapılandırmanızı mimicking yeni hedef depolama hesabı oluşturacak.</span><span class="sxs-lookup"><span data-stu-id="7fb92-144">**Target Storage accounts:** By default, ASR will create the new target storage account mimicking your source VM storage configuration.</span></span> <span data-ttu-id="7fb92-145">ASR tarafından önceden oluşturulmuş depolama hesabı mevcut olmaması durumunda, yeniden kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7fb92-145">In case storage account created by ASR already exist, it will be reused.</span></span>

5. <span data-ttu-id="7fb92-146">**Depolama hesapları önbelleğe:** ASR önbellek depolama kaynağı bölgede adlı ek depolama alanı hesabı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="7fb92-146">**Cache Storage accounts:** ASR needs extra storage account called cache storage in the source region.</span></span> <span data-ttu-id="7fb92-147">Kaynak sanal makinelerin gerçekleştiği tüm değişiklikleri izlenen ve bu hedef konumuna çoğaltma önce önbellek depolama hesabına gönderilir.</span><span class="sxs-lookup"><span data-stu-id="7fb92-147">All the changes happening on the source VMs are tracked and sent to cache storage account before replicating those to the target location.</span></span>

6. <span data-ttu-id="7fb92-148">**Kullanılabilirlik kümesi:** varsayılan olarak, hedef bölgede kümesi "asr" sonekine sahip adı ile yeni bir kullanılabilirlik ASR oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7fb92-148">**Availability set :** By default, ASR will create a new availability set in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="7fb92-149">Kullanılabilirlik kümesi zaten ASR tarafından oluşturulan mevcut olmaması durumunda, yeniden kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7fb92-149">In case availability set created by ASR already exist, it will be reused.</span></span>

7.  <span data-ttu-id="7fb92-150">**Çoğaltma İlkesi:** kurtarma noktası bekletme geçmişi ve uygulama tutarlılığı anlık görüntü sıklığı ayarlarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7fb92-150">**Replication Policy:** It defines the settings for recovery point retention history and app consistent snapshot frequency.</span></span> <span data-ttu-id="7fb92-151">Varsayılan olarak, ASR ' 24 saattir kurtarma noktası bekletme ve ' 60 dakika uygulama tutarlılığı anlık görüntü sıklığı için varsayılan ayarlarla yeni bir çoğaltma ilkesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7fb92-151">By default, ASR will create a new replication policy with default settings of ‘24 hours’ for recovery point retention and ’60 minutes’ for app consistent snapshot frequency.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a><span data-ttu-id="7fb92-153">Hedef kaynakları özelleştirme</span><span class="sxs-lookup"><span data-stu-id="7fb92-153">Customize target resources</span></span>

<span data-ttu-id="7fb92-154">ASR tarafından kullanılan varsayılan değerleri değiştirmek istemeniz durumunda, gereksinimlerinize göre ayarlarını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7fb92-154">In case you want to change the defaults used by ASR, you can change the settings based on your needs.</span></span>

1. <span data-ttu-id="7fb92-155">**Özelleştir:** ASR tarafından kullanılan varsayılan değerleri değiştirmek için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7fb92-155">**Customize:** Click it to change the defaults used by ASR.</span></span>

2. <span data-ttu-id="7fb92-156">**Hedef kaynak grubu:** abonelik içindeki hedef konumda var olan tüm kaynak gruplarının listesini kaynak grubunu seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7fb92-156">**Target resource group :**  You can select the resource group from the list of all the resource groups existing in the target location within the subscription.</span></span>

3. <span data-ttu-id="7fb92-157">**Hedef sanal ağ:** hedef konumda bulunan tüm sanal ağ listesini bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7fb92-157">**Target Virtual Network:** You can find the list of all the virtual network in the target location.</span></span>

4. <span data-ttu-id="7fb92-158">**Kullanılabilirlik kümesi:** kullanılabilirlik kaynak bölgede bir parçası olan sanal makineler için kullanılabilirlik kümeleri ayarlarını yalnızca ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7fb92-158">**Availability set :** You can only add availability sets settings to the virtual machines which are a part of availability in source region.</span></span>

5. <span data-ttu-id="7fb92-159">**Hedef depolama hesapları:**</span><span class="sxs-lookup"><span data-stu-id="7fb92-159">**Target Storage accounts:**</span></span>

<span data-ttu-id="7fb92-160">![Çoğaltmayı etkinleştirme](./media/site-recovery-replicate-azure-to-azure/customize.PNG) tıklayın **hedef kaynak oluşturma** ve çoğaltmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="7fb92-160">![Enable replication](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Click on **Create target resource** and Enable Replication</span></span>


<span data-ttu-id="7fb92-161">Korunan sanal makine sonra altında VM'ler sağlık durumunu kontrol edebilirsiniz **çoğaltılan öğeler**</span><span class="sxs-lookup"><span data-stu-id="7fb92-161">Once virtual machines are protected you can check the status of VMs health under **Replicated items**</span></span>

>[!NOTE]
><span data-ttu-id="7fb92-162">İlk çoğaltma süre boyunca durum yenilemesinin zaman almasıdır ve biraz zaman ilerleme görmüyorsanız olasılığı verebilir.</span><span class="sxs-lookup"><span data-stu-id="7fb92-162">During the time of initial replication there could a possibility that status takes time to refresh and you don't see progress for some time.</span></span> <span data-ttu-id="7fb92-163">En son durumunu almak için dikey pencerenin üst kısmında Yenile düğmesini tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7fb92-163">You can click the Refresh button on the top of the blade to get the latest status.</span></span>
>

![Çoğaltmayı etkinleştirme](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a><span data-ttu-id="7fb92-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7fb92-165">Next steps</span></span>
- <span data-ttu-id="7fb92-166">[Daha fazla bilgi edinin](site-recovery-test-failover-to-azure.md) yük devretme testi çalıştırma hakkında.</span><span class="sxs-lookup"><span data-stu-id="7fb92-166">[Learn more](site-recovery-test-failover-to-azure.md) about running a test failover.</span></span>
- <span data-ttu-id="7fb92-167">[Daha fazla bilgi edinin](site-recovery-failover.md) farklı türdeki yük devretmeler ve bunları çalıştırma hakkında.</span><span class="sxs-lookup"><span data-stu-id="7fb92-167">[Learn more](site-recovery-failover.md) about different types of failovers, and how to run them.</span></span>
- <span data-ttu-id="7fb92-168">Daha fazla bilgi edinmek [kurtarma planlarına kullanarak](site-recovery-create-recovery-plans.md) RTO azaltmak için.</span><span class="sxs-lookup"><span data-stu-id="7fb92-168">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) to reduce RTO.</span></span>
- <span data-ttu-id="7fb92-169">Daha fazla bilgi edinmek [Azure sanal makineleri yeniden korumayı](site-recovery-how-to-reprotect.md) yük devretme sonrasında.</span><span class="sxs-lookup"><span data-stu-id="7fb92-169">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>
