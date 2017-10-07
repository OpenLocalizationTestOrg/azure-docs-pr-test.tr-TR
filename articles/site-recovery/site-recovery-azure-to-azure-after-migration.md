---
title: "Site Recovery kullanarak geçiş tooAzure sonra Azure bölgeler arasında olağanüstü durum kurtarma yukarı aaaPrepare makineler tooset | Microsoft Docs"
description: "Bu makalede, Azure Site Recovery kullanarak geçiş tooAzure sonra Azure bölgeler arasında olağanüstü durum kurtarma yukarı tooset nasıl tooprepare makineleri açıklanmaktadır."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ponatara
ms.openlocfilehash: b6274e3df210c1d8a7b8289cc85868ee6414e523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-tooanother-region-after-migration-tooazure-by-using-azure-site-recovery"></a><span data-ttu-id="b623e-103">Azure Site Recovery kullanarak geçiş tooAzure sonra Azure Vm'lerinin tooanother bölge çoğaltma</span><span class="sxs-lookup"><span data-stu-id="b623e-103">Replicate Azure VMs tooanother region after migration tooAzure by using Azure Site Recovery</span></span>

>[!NOTE]
> <span data-ttu-id="b623e-104">Azure sanal makineleri (VM'ler) için Azure Site Recovery çoğaltma şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="b623e-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

## <a name="overview"></a><span data-ttu-id="b623e-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b623e-105">Overview</span></span>

<span data-ttu-id="b623e-106">Bu makalede, Azure sanal makineleri Azure Site Recovery kullanarak bir şirket içi ortamına tooAzure bu makineler geçirildikten sonra iki Azure bölgeler arasında çoğaltma hazırlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="b623e-106">This article helps you prepare Azure virtual machines for replication between two Azure regions after these machines have been migrated from an on-premises environment tooAzure by using Azure Site Recovery.</span></span>

## <a name="disaster-recovery-and-compliance"></a><span data-ttu-id="b623e-107">Olağanüstü durum kurtarma ve uyumluluk</span><span class="sxs-lookup"><span data-stu-id="b623e-107">Disaster recovery and compliance</span></span>
<span data-ttu-id="b623e-108">Bugün, daha da fazla kuruluşların kendi iş yükleri tooAzure taşıyor.</span><span class="sxs-lookup"><span data-stu-id="b623e-108">Today, more and more enterprises are moving their workloads tooAzure.</span></span> <span data-ttu-id="b623e-109">Kritik şirket içi üretim taşıma kuruluşlara iş yükleri tooAzure, bu iş yükleri için olağanüstü durum kurtarma ayarlama uyumluluk ve bir Azure bölgesindeki kesintileri karşı toosafeguard için zorunludur.</span><span class="sxs-lookup"><span data-stu-id="b623e-109">With enterprises moving mission-critical on-premises production workloads tooAzure, setting up disaster recovery for these workloads is mandatory for compliance and toosafeguard against any disruptions in an Azure region.</span></span>

## <a name="steps-for-preparing-migrated-machines-for-replication"></a><span data-ttu-id="b623e-110">Geçirilen makineleri çoğaltma için hazırlama adımları</span><span class="sxs-lookup"><span data-stu-id="b623e-110">Steps for preparing migrated machines for replication</span></span>
<span data-ttu-id="b623e-111">tooprepare çoğaltma tooanother Azure bölgesini ayarlamak için makineler geçişi:</span><span class="sxs-lookup"><span data-stu-id="b623e-111">tooprepare migrated machines for setting up replication tooanother Azure region:</span></span>

1. <span data-ttu-id="b623e-112">Geçişi tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="b623e-112">Complete migration.</span></span>
2. <span data-ttu-id="b623e-113">Merhaba gerekirse Azure aracısını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b623e-113">Install hello Azure agent if needed.</span></span>
3. <span data-ttu-id="b623e-114">Merhaba Mobility hizmeti kaldırın.</span><span class="sxs-lookup"><span data-stu-id="b623e-114">Remove hello Mobility service.</span></span>  
4. <span data-ttu-id="b623e-115">Merhaba VM yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="b623e-115">Restart hello VM.</span></span>

<span data-ttu-id="b623e-116">Aşağıdaki bölümlerde hello bölümlerinde daha ayrıntılı adımları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b623e-116">These steps are described in more detail in hello following sections.</span></span>

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-toorun-on-azure-vms"></a><span data-ttu-id="b623e-117">Adım 1: Hyper-V sanal makineleri, VMware Vm'lerini ve fiziksel sunucuları toorun Azure vm'lerinde çalışan iş yüklerini geçirme</span><span class="sxs-lookup"><span data-stu-id="b623e-117">Step 1: Migrate workloads running on Hyper-V VMs, VMware VMs, and physical servers toorun on Azure VMs</span></span>

<span data-ttu-id="b623e-118">tooset ayarlama çoğaltma ve, şirket içi Hyper-V, VMware ve fiziksel iş yükleri tooAzure hello adımları hello içinde geçirmek [Azure Site Recovery ile Azure bölgeler arasında geçirmek Azure Iaas sanal makineleri](site-recovery-migrate-to-azure.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="b623e-118">tooset up replication and migrate your on-premises Hyper-V, VMware, and physical workloads tooAzure, follow hello steps in hello [Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery](site-recovery-migrate-to-azure.md) article.</span></span> 

<span data-ttu-id="b623e-119">Geçişten sonra toocommit gerek yok veya bir yük devretme silin.</span><span class="sxs-lookup"><span data-stu-id="b623e-119">After migration, you don't need toocommit or delete a failover.</span></span> <span data-ttu-id="b623e-120">Bunun yerine, hello seçin **tam geçiş** seçeneği toomigrate istediğiniz her makine için:</span><span class="sxs-lookup"><span data-stu-id="b623e-120">Instead, select hello **Complete Migration** option for each machine you want toomigrate:</span></span>
1. <span data-ttu-id="b623e-121">İçinde **çoğaltılan öğeler**, hello VM sağ tıklayın ve **tam geçiş**.</span><span class="sxs-lookup"><span data-stu-id="b623e-121">In **Replicated Items**, right-click hello VM, and click **Complete Migration**.</span></span> <span data-ttu-id="b623e-122">Tıklatın **Tamam** toocomplete hello adım.</span><span class="sxs-lookup"><span data-stu-id="b623e-122">Click **OK** toocomplete hello step.</span></span> <span data-ttu-id="b623e-123">Merhaba tam geçiş işine izleyerek hello VM Özellikleri'nde ilerleme durumunu izleyebilirsiniz **Site Recovery işleri**.</span><span class="sxs-lookup"><span data-stu-id="b623e-123">You can track progress in hello VM properties by monitoring hello Complete Migration job in **Site Recovery jobs**.</span></span>
2. <span data-ttu-id="b623e-124">Merhaba **tam geçiş** eylem hello geçiş işlemi tamamlanır, hello makinesi için çoğaltma kaldırır ve hello makine için Site Recovery Faturalaması durdurulur.</span><span class="sxs-lookup"><span data-stu-id="b623e-124">hello **Complete Migration** action completes hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

   ![tamgeçiş](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-hello-azure-vm-agent-on-hello-virtual-machine"></a><span data-ttu-id="b623e-126">2. adım: hello Azure VM Aracısı hello sanal makineye yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b623e-126">Step 2: Install hello Azure VM agent on hello virtual machine</span></span>
<span data-ttu-id="b623e-127">Hello Azure [VM Aracısı](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) hello Site Recovery uzantısı toowork ve toohelp hello VM korumak için hello sanal makineye yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b623e-127">hello Azure [VM agent](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) must be installed on hello virtual machine for hello Site Recovery extension toowork and toohelp protect hello VM.</span></span>

>[!IMPORTANT]
><span data-ttu-id="b623e-128">Sürüm 9.7.0.0, Windows sanal makinelerde itibaren hello Mobility hizmeti yükleyicisinin hello en son kullanılabilir Azure VM Aracısı de yükler.</span><span class="sxs-lookup"><span data-stu-id="b623e-128">Beginning with version 9.7.0.0, on Windows virtual machines, hello Mobility service installer also installs hello latest available Azure VM agent.</span></span> <span data-ttu-id="b623e-129">Geçiş üzerinde aracı yüklemesi hello Site Recovery uzantısı dahil olmak üzere, herhangi bir VM uzantısı kullanılarak için önkoşul hello sanal makine karşılar.</span><span class="sxs-lookup"><span data-stu-id="b623e-129">On migration, hello virtual machine meets the agent installation prerequisite for using any VM extension, including hello Site Recovery extension.</span></span> <span data-ttu-id="b623e-130">yalnızca hello Mobility hizmeti hello üzerinde yüklü makine geçirdiyseniz el ile yüklenen hello Azure VM Aracısı gereksinimlerini toobe 9.6 veya önceki bir sürümü var.</span><span class="sxs-lookup"><span data-stu-id="b623e-130">hello Azure VM agent needs toobe manually installed only if hello Mobility service installed on hello migrated machine is version 9.6 or earlier.</span></span>

<span data-ttu-id="b623e-131">Merhaba aşağıdaki tabloda hello VM Aracısı yükleme ve yüklü olduğu doğrulanıyor hakkında ek bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="b623e-131">hello following table provides additional information about installing hello VM agent and validating that it was installed:</span></span>

| <span data-ttu-id="b623e-132">**İşlem**</span><span class="sxs-lookup"><span data-stu-id="b623e-132">**Operation**</span></span> | <span data-ttu-id="b623e-133">**Windows**</span><span class="sxs-lookup"><span data-stu-id="b623e-133">**Windows**</span></span> | <span data-ttu-id="b623e-134">**Linux**</span><span class="sxs-lookup"><span data-stu-id="b623e-134">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b623e-135">Merhaba VM Aracısı yükleniyor</span><span class="sxs-lookup"><span data-stu-id="b623e-135">Installing hello VM agent</span></span> |<span data-ttu-id="b623e-136">Merhaba yükleyip [aracı MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="b623e-136">Download and install hello [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="b623e-137">Yönetici ayrıcalıkları toocomplete hello yüklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b623e-137">You need administrator privileges toocomplete hello installation.</span></span> |<span data-ttu-id="b623e-138">Merhaba son yükleme [Linux Aracısı](../virtual-machines/linux/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="b623e-138">Install hello latest [Linux agent](../virtual-machines/linux/agent-user-guide.md).</span></span> <span data-ttu-id="b623e-139">Yönetici ayrıcalıkları toocomplete hello yüklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b623e-139">You need administrator privileges toocomplete hello installation.</span></span> <span data-ttu-id="b623e-140">Dağıtım depodan hello aracı yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="b623e-140">We recommend installing hello agent from your distribution repository.</span></span> <span data-ttu-id="b623e-141">Biz *değil önerilir* doğrudan Github'dan hello Linux VM Aracısı yükleme.</span><span class="sxs-lookup"><span data-stu-id="b623e-141">We *do not recommend* installing hello Linux VM agent directly from GitHub.</span></span>  |
| <span data-ttu-id="b623e-142">Merhaba VM Aracısı yüklemesini doğrulama</span><span class="sxs-lookup"><span data-stu-id="b623e-142">Validating hello VM agent installation</span></span> |<span data-ttu-id="b623e-143">1. Hello Azure VM toohello C:\WindowsAzure\Packages klasörüne göz atın.</span><span class="sxs-lookup"><span data-stu-id="b623e-143">1. Browse toohello C:\WindowsAzure\Packages folder in hello Azure VM.</span></span> <span data-ttu-id="b623e-144">Görmeniz gerekir hello WaAppAgent.exe dosyasını.</span><span class="sxs-lookup"><span data-stu-id="b623e-144">You should see hello WaAppAgent.exe file.</span></span> <br><span data-ttu-id="b623e-145">2. Merhaba dosyaya sağ tıklayın, çok Git**özellikleri**seçip hello **ayrıntıları** sekmesini hello **ürün sürümü** alanı 2.6.1198.718 olmalıdır ya da daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="b623e-145">2. Right-click hello file, go too**Properties**, and then select hello **Details** tab. hello **Product Version** field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="b623e-146">Yok</span><span class="sxs-lookup"><span data-stu-id="b623e-146">N/A</span></span> |


### <a name="step-3-remove-hello-mobility-service-from-hello-migrated-virtual-machine"></a><span data-ttu-id="b623e-147">3. adım: Sanal makine Kaldır hello hello Mobility hizmetinden geçişi</span><span class="sxs-lookup"><span data-stu-id="b623e-147">Step 3: Remove hello Mobility service from hello migrated virtual machine</span></span>

<span data-ttu-id="b623e-148">Şirket içi VMware makineleri veya fiziksel Windows/Linux sunucularda geçirdiyseniz, toomanually kaldırmak/hello Mobility hizmetinden hello geçirilen sanal makine gerekir.</span><span class="sxs-lookup"><span data-stu-id="b623e-148">If you have migrated your on-premises VMware machines or physical servers on Windows/Linux, you need toomanually remove/uninstall hello Mobility service from hello migrated virtual machine.</span></span>

>[!IMPORTANT]
><span data-ttu-id="b623e-149">Bu adım için Hyper-V sanal makineleri geçirilen tooAzure gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="b623e-149">This step is not required for Hyper-V VMs migrated tooAzure.</span></span>

#### <a name="uninstall-hello-mobility-service-on-a-windows-server-vm"></a><span data-ttu-id="b623e-150">Windows Server VM üzerinde Hello Mobility hizmetini kaldırma</span><span class="sxs-lookup"><span data-stu-id="b623e-150">Uninstall hello Mobility service on a Windows Server VM</span></span>
<span data-ttu-id="b623e-151">Bir Windows Server bilgisayarında yöntemleri toouninstall hello Mobility hizmeti aşağıdaki hello birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b623e-151">Use one of hello following methods toouninstall hello Mobility service on a Windows Server computer.</span></span>

##### <a name="uninstall-by-using-hello-windows-ui"></a><span data-ttu-id="b623e-152">Merhaba Windows kullanıcı arabirimini kullanarak kaldırma</span><span class="sxs-lookup"><span data-stu-id="b623e-152">Uninstall by using hello Windows UI</span></span>
1. <span data-ttu-id="b623e-153">Hello Denetim Masası'da, seçin **programlar**.</span><span class="sxs-lookup"><span data-stu-id="b623e-153">In hello Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="b623e-154">Seçin **Microsoft Azure Site Recovery Mobility hizmeti/ana hedef sunucu**ve ardından **kaldırma**.</span><span class="sxs-lookup"><span data-stu-id="b623e-154">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

##### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="b623e-155">Bir komut isteminde kaldırma</span><span class="sxs-lookup"><span data-stu-id="b623e-155">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="b623e-156">Yönetici olarak bir komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="b623e-156">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="b623e-157">toouninstall Mobility hizmeti Merhaba, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b623e-157">toouninstall hello Mobility service, run hello following command:</span></span>

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-hello-mobility-service-on-a-linux-computer"></a><span data-ttu-id="b623e-158">Bir Linux bilgisayarda Hello Mobility hizmetini kaldırma</span><span class="sxs-lookup"><span data-stu-id="b623e-158">Uninstall hello Mobility service on a Linux computer</span></span>
1. <span data-ttu-id="b623e-159">Linux sunucunuzda olarak oturum açın bir **kök** kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="b623e-159">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="b623e-160">Bir terminale çok/kullanıcı/yerel/ASR gidin.</span><span class="sxs-lookup"><span data-stu-id="b623e-160">In a terminal, go too/user/local/ASR.</span></span>
3. <span data-ttu-id="b623e-161">toouninstall Mobility hizmeti Merhaba, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b623e-161">toouninstall hello Mobility service, run hello following command:</span></span>

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-hello-vm"></a><span data-ttu-id="b623e-162">4. adım: hello VM yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="b623e-162">Step 4: Restart hello VM</span></span>

<span data-ttu-id="b623e-163">Merhaba Mobility hizmeti kaldırdıktan sonra önce yeniden başlatma hello VM çoğaltma tooanother Azure bölgesi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b623e-163">After you uninstall hello Mobility service, restart hello VM before you set up replication tooanother Azure region.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b623e-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b623e-164">Next steps</span></span>
- <span data-ttu-id="b623e-165">İş yükleri tarafından korumaya başlamak [Azure sanal makineleri çoğaltmak](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="b623e-165">Start protecting your workloads by [replicating Azure virtual machines](site-recovery-azure-to-azure.md).</span></span>
- <span data-ttu-id="b623e-166">Daha fazla bilgi edinmek [Azure sanal makineleri çoğaltmak için kılavuz ağ](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="b623e-166">Learn more about [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
