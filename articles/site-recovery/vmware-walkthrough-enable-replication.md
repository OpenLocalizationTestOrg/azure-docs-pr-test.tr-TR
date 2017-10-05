---
title: "Azure Site Recovery ile azure'a VMware Vm'lerini çoğaltma için çoğaltma etkinleştirme | Microsoft Docs"
description: "Azure VM'ler için çoğaltma VMware Azure Site Recovery hizmetini kullanarak etkinleştirmek için gereken adımları özetler"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 519c5559-7032-4954-b8b5-f24f5242a954
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 470b9ddd8df4a4e74ec7174f79020c252323e502
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="step-11-enable-replication-for-vmware-virtual-machines-to-azure"></a><span data-ttu-id="57ee2-103">11. adım: Azure VMware sanal makineler için çoğaltmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="57ee2-103">Step 11: Enable replication for VMware virtual machines to Azure</span></span>


<span data-ttu-id="57ee2-104">Bu makalede Azure, şirket içi VMware sanal makineler için çoğaltma etkinleştirme kullanarak [Azure Site Recovery](site-recovery-overview.md) Azure portalında hizmet.</span><span class="sxs-lookup"><span data-stu-id="57ee2-104">This article describes how to enable replication for on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="57ee2-105">POST açıklamaları ve soruları alt bu makalenin veya üzerinde [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="57ee2-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="57ee2-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="57ee2-106">Before you start</span></span>

- <span data-ttu-id="57ee2-107">VMware sanal makinelerini olmalıdır [Mobility hizmeti bileşeninin yüklü](vmware-walkthrough-install-mobility.md).</span><span class="sxs-lookup"><span data-stu-id="57ee2-107">VMware VMs must have the [Mobility service component installed](vmware-walkthrough-install-mobility.md).</span></span> <span data-ttu-id="57ee2-108">-Bir VM gönderme yüklemesi için hazırlanmış, çoğaltma etkinleştirdiğinizde işlem sunucusu otomatik olarak Mobility hizmetini yükler.</span><span class="sxs-lookup"><span data-stu-id="57ee2-108">- If a VM is prepared for push installation, the process server automatically installs the Mobility service when you enable replication.</span></span>
- <span data-ttu-id="57ee2-109">Azure kullanıcı hesabınızın belirli gereken [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) Azure bir VM'nin çoğaltmayı etkinleştirmek için</span><span class="sxs-lookup"><span data-stu-id="57ee2-109">Your Azure user account needs specific [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of a VM to Azure</span></span>
- <span data-ttu-id="57ee2-110">Ekleyin veya VM'ler değiştirdiğinizde, 15 dakika veya daha uzun değişikliklerin etkili olması ve sunumların portalda görünebilmesi kadar sürebilir.</span><span class="sxs-lookup"><span data-stu-id="57ee2-110">When you add or modify VMs, it can take up to 15 minutes or longer for changes to take effect, and for them to appear in the portal.</span></span>
- <span data-ttu-id="57ee2-111">Vm'lerde bulunan en son ne zaman denetleyebilir **yapılandırma sunucularına** > **en son kişi**.</span><span class="sxs-lookup"><span data-stu-id="57ee2-111">You can check the last discovered time for VMs in **Configuration Servers** > **Last Contact At**.</span></span>
- <span data-ttu-id="57ee2-112">VM'ler için zamanlanmış bulma beklemeden eklemek için yapılandırma sunucusu vurgulayın (tıklatın yok), tıklatıp **yenileme**.</span><span class="sxs-lookup"><span data-stu-id="57ee2-112">To add VMs without waiting for the scheduled discovery, highlight the configuration server (don’t click it), and click **Refresh**.</span></span>



## <a name="exclude-disks-from-replication"></a><span data-ttu-id="57ee2-113">Diskleri çoğaltmanın dışında tutma</span><span class="sxs-lookup"><span data-stu-id="57ee2-113">Exclude disks from replication</span></span>

<span data-ttu-id="57ee2-114">Varsayılan olarak, bir makine üzerindeki tüm diskleri çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="57ee2-114">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="57ee2-115">Diskleri çoğaltmanın dışında bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57ee2-115">You can exclude disks from replication.</span></span> <span data-ttu-id="57ee2-116">Örneğin, geçici veriler veya her zaman bir makine yeniledi veri disklerini çoğaltmak istemeyebilirsiniz veya (örneğin pagefile.sys ya da SQL Server tempdb) uygulamasını yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="57ee2-116">For example you might not want to replicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="57ee2-117">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="57ee2-117">Learn more</span></span>](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a><span data-ttu-id="57ee2-118">Vm'lerini çoğaltma</span><span class="sxs-lookup"><span data-stu-id="57ee2-118">Replicate VMs</span></span>

<span data-ttu-id="57ee2-119">Başlamadan önce hızlı bir video genel bakış izleyin</span><span class="sxs-lookup"><span data-stu-id="57ee2-119">Before you start, watch a quick video overview</span></span>

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. <span data-ttu-id="57ee2-120">**2. Adım: Uygulama çoğaltma** > **Kaynak** seçeneklerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="57ee2-120">Click **Step 2: Replicate application** > **Source**.</span></span>
2. <span data-ttu-id="57ee2-121">İçinde **kaynak**, yapılandırma sunucusu seçin.</span><span class="sxs-lookup"><span data-stu-id="57ee2-121">In **Source**, select the configuration server.</span></span>
3. <span data-ttu-id="57ee2-122">İçinde **makine türü**seçin **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="57ee2-122">In **Machine type**, select **Virtual Machines**.</span></span>
4. <span data-ttu-id="57ee2-123">İçinde **vCenter/vSphere hiper yönetici**vSphere ana yöneten vCenter sunucusu seçin veya konağı seçin.</span><span class="sxs-lookup"><span data-stu-id="57ee2-123">In **vCenter/vSphere Hypervisor**, select the vCenter server that manages the vSphere host, or select the host.</span></span>
5. <span data-ttu-id="57ee2-124">İşlem sunucusu seçin.</span><span class="sxs-lookup"><span data-stu-id="57ee2-124">Select the process server.</span></span> <span data-ttu-id="57ee2-125">Herhangi bir ek işlem sunucusu oluşturmadıysanız bu yapılandırma sunucusu olacaktır.</span><span class="sxs-lookup"><span data-stu-id="57ee2-125">If you haven't created any additional process servers this will be the configuration server.</span></span> <span data-ttu-id="57ee2-126">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="57ee2-126">Then click **OK**.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/vmware-walkthrough-enable-replication/enable-replication2.png)

6. <span data-ttu-id="57ee2-128">İçinde **hedef**, abonelik ve başarısız VM'ler üzerinde oluşturmak istediğiniz kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="57ee2-128">In **Target**, select the subscription and the resource group in which you want to create the failed over VMs.</span></span> <span data-ttu-id="57ee2-129">Devredilen sanal makineleri için Azure (Yönetim), Klasik veya resource kullanmak istediğiniz dağıtım modelini seçin.</span><span class="sxs-lookup"><span data-stu-id="57ee2-129">Choose the deployment model that you want to use in Azure (classic or resource management), for the failed over VMs.</span></span>


7. <span data-ttu-id="57ee2-130">Veri çoğaltmak için kullanmak istediğiniz Azure depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="57ee2-130">Select the Azure storage account you want to use for replicating data.</span></span> <span data-ttu-id="57ee2-131">Ayarlamış bir hesap kullanmak istemiyorsanız, yeni bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57ee2-131">If you don't want to use an account you've already set up, you can create a new one.</span></span>

8. <span data-ttu-id="57ee2-132">Yük devretme sonrasında oluşturulan Azure VM'lerinin bağlanacağı Azure ağını ve alt ağını seçin.</span><span class="sxs-lookup"><span data-stu-id="57ee2-132">Select the Azure network and subnet to which Azure VMs will connect, when they're created after failover.</span></span> <span data-ttu-id="57ee2-133">Koruma için seçtiğiniz tüm makinelere ağ ayarını uygulamak için **Seçili makineler için şimdi yapılandır**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="57ee2-133">Select **Configure now for selected machines**, to apply the network setting to all machines you select for protection.</span></span> <span data-ttu-id="57ee2-134">Makineler için Azure ağını ayrı ayrı seçmek için **Daha sonra yapılandır**'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="57ee2-134">Select **Configure later** to select the Azure network per machine.</span></span> <span data-ttu-id="57ee2-135">Varolan bir ağı kullanmak istemiyorsanız, bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57ee2-135">If you don't want to use an existing network, you can create one.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/vmware-walkthrough-enable-replication/enable-rep3.png)
9. <span data-ttu-id="57ee2-137">**Sanal Makineler** > **Sanal makine seçin** seçeneklerine tıklayın ve çoğaltmak istediğiniz makineleri seçin.</span><span class="sxs-lookup"><span data-stu-id="57ee2-137">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="57ee2-138">Yalnızca çoğaltmanın etkinleştirildiği makineleri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57ee2-138">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="57ee2-139">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="57ee2-139">Then click **OK**.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/vmware-walkthrough-enable-replication/enable-replication5.png)
10. <span data-ttu-id="57ee2-141">İçinde **özellikleri** > **özelliklerini yapılandırma**, işlem sunucusu tarafından otomatik olarak makinede Mobility hizmeti yüklemek için kullanılacak hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="57ee2-141">In **Properties** > **Configure properties**, select the account that will be used by the process server to automatically install the Mobility service on the machine.</span></span>
11. <span data-ttu-id="57ee2-142">Varsayılan olarak tüm diskler çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="57ee2-142">By default all disks are replicated.</span></span> <span data-ttu-id="57ee2-143">Tıklatın **tüm diskleri** ve çoğaltmak için istemediğiniz tüm diskleri temizleyin.</span><span class="sxs-lookup"><span data-stu-id="57ee2-143">Click **All Disks** and clear any disks you don't want to replicate.</span></span> <span data-ttu-id="57ee2-144">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="57ee2-144">Then click **OK**.</span></span> <span data-ttu-id="57ee2-145">Ek VM özellikleri daha sonra ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57ee2-145">You can set additional VM properties later.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/vmware-walkthrough-enable-replication/enable-replication6.png)
11. <span data-ttu-id="57ee2-147">İçinde **çoğaltma ayarları** > **çoğaltma ayarlarını yapılandırın**, doğru Çoğaltma İlkesi'nin seçili olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="57ee2-147">In **Replication settings** > **Configure replication settings**, verify that the correct replication policy is selected.</span></span> <span data-ttu-id="57ee2-148">Bir ilkeyi değiştirirseniz, değişiklikler makinenin çoğaltıldığını ve yeni makinelere uygulanır.</span><span class="sxs-lookup"><span data-stu-id="57ee2-148">If you modify a policy, changes will be applied to replicating machine, and to new machines.</span></span>
12. <span data-ttu-id="57ee2-149">Etkinleştirme **çoklu VM tutarlılığını** makineler çoğaltma grubuna toplayın ve grup için bir ad belirtmek istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="57ee2-149">Enable **Multi-VM consistency** if you want to gather machines into a replication group, and specify a name for the group.</span></span> <span data-ttu-id="57ee2-150">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="57ee2-150">Then click **OK**.</span></span> <span data-ttu-id="57ee2-151">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="57ee2-151">Note that:</span></span>

    * <span data-ttu-id="57ee2-152">Çoğaltma gruplarındaki makineler birlikte çoğaltılır ve kilitlenme tutarlı ve uygulamayla tutarlı kurtarma noktaları üzerinden başarısız olduğunda paylaşılan.</span><span class="sxs-lookup"><span data-stu-id="57ee2-152">Machines in replication groups replicate together, and have shared crash-consistent and app-consistent recovery points when they fail over.</span></span>
    * <span data-ttu-id="57ee2-153">Böylece, iş yüklerini yansıtma sanal makineleri ve fiziksel sunucuları araya toplamak öneririz.</span><span class="sxs-lookup"><span data-stu-id="57ee2-153">We recommend that you gather VMs and physical servers together so that they mirror your workloads.</span></span> <span data-ttu-id="57ee2-154">Çoklu VM tutarlılığını etkinleştirmek, iş yükü performansını etkileyebilir ve yalnızca makineler aynı iş yükünü çalıştırıyorsa ve tutarlılık ihtiyacınız varsa kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="57ee2-154">Enabling multi-VM consistency can impact workload performance, and should only be used if machines are running the same workload and you need consistency.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/vmware-walkthrough-enable-replication/enable-replication7.png)
13. <span data-ttu-id="57ee2-156">Tıklatın **çoğaltmasını etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="57ee2-156">Click **Enable Replication**.</span></span> <span data-ttu-id="57ee2-157">İlerleme durumunu izleyebilirsiniz **korumayı etkinleştir** iş **ayarları** > **işleri** > **Site Recovery işleri**.</span><span class="sxs-lookup"><span data-stu-id="57ee2-157">You can track progress of the **Enable Protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span> <span data-ttu-id="57ee2-158">**Korumayı Sonlandır** işi çalıştırıldıktan sonra makine yük devretme için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="57ee2-158">After the **Finalize Protection** job runs the machine is ready for failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57ee2-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="57ee2-159">Next steps</span></span>

<span data-ttu-id="57ee2-160">Git [adım 12: yük devretme testi çalıştırma](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="57ee2-160">Go to [Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
