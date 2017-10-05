---
title: "Azure Site Recovery kullanarak geçiş sonrasında Azure bölgeler arasında olağanüstü durum kurtarma ayarlamak için makineler hazırlama | Microsoft Docs"
description: "Bu makalede, Azure Site Recovery kullanarak Azure geçişten sonra Azure bölgeler arasında olağanüstü durum kurtarma ayarlamak için makineler hazırlama açıklar."
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
ms.openlocfilehash: 2aee0fb8d1ba1ff1584bee91b4d1cc34b654d97f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-vms-to-another-region-after-migration-to-azure-by-using-azure-site-recovery"></a><span data-ttu-id="b0de8-103">Azure Vm'lerini başka bir bölgeye Azure geçişten sonra Azure Site Recovery kullanarak çoğaltma</span><span class="sxs-lookup"><span data-stu-id="b0de8-103">Replicate Azure VMs to another region after migration to Azure by using Azure Site Recovery</span></span>

>[!NOTE]
> <span data-ttu-id="b0de8-104">Azure sanal makineleri (VM'ler) için Azure Site Recovery çoğaltma şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="b0de8-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

## <a name="overview"></a><span data-ttu-id="b0de8-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b0de8-105">Overview</span></span>

<span data-ttu-id="b0de8-106">Bu makalede, Azure sanal makineleri bu makinelere şirket içi ortamından Azure için Azure Site Recovery kullanarak geçirildikten sonra iki Azure bölgeler arasında çoğaltma hazırlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="b0de8-106">This article helps you prepare Azure virtual machines for replication between two Azure regions after these machines have been migrated from an on-premises environment to Azure by using Azure Site Recovery.</span></span>

## <a name="disaster-recovery-and-compliance"></a><span data-ttu-id="b0de8-107">Olağanüstü durum kurtarma ve uyumluluk</span><span class="sxs-lookup"><span data-stu-id="b0de8-107">Disaster recovery and compliance</span></span>
<span data-ttu-id="b0de8-108">Bugün, daha da fazla kuruluşlar, iş yüklerini Azure'a taşıyor.</span><span class="sxs-lookup"><span data-stu-id="b0de8-108">Today, more and more enterprises are moving their workloads to Azure.</span></span> <span data-ttu-id="b0de8-109">Kuruluşlara kritik taşıma üretim içi iş yüklerini azure'a, uyumluluk ve bir Azure bölgesindeki kesintileri karşı koruma için bu iş yükleri için olağanüstü durum kurtarma kurma zorunludur.</span><span class="sxs-lookup"><span data-stu-id="b0de8-109">With enterprises moving mission-critical on-premises production workloads to Azure, setting up disaster recovery for these workloads is mandatory for compliance and to safeguard against any disruptions in an Azure region.</span></span>

## <a name="steps-for-preparing-migrated-machines-for-replication"></a><span data-ttu-id="b0de8-110">Geçirilen makineleri çoğaltma için hazırlama adımları</span><span class="sxs-lookup"><span data-stu-id="b0de8-110">Steps for preparing migrated machines for replication</span></span>
<span data-ttu-id="b0de8-111">Hazırlamak için başka bir Azure bölgesine çoğaltma ayarlama makineler geçişi:</span><span class="sxs-lookup"><span data-stu-id="b0de8-111">To prepare migrated machines for setting up replication to another Azure region:</span></span>

1. <span data-ttu-id="b0de8-112">Geçişi tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="b0de8-112">Complete migration.</span></span>
2. <span data-ttu-id="b0de8-113">Gerekirse Azure aracısını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b0de8-113">Install the Azure agent if needed.</span></span>
3. <span data-ttu-id="b0de8-114">Mobility hizmeti kaldırın.</span><span class="sxs-lookup"><span data-stu-id="b0de8-114">Remove the Mobility service.</span></span>  
4. <span data-ttu-id="b0de8-115">VM'yi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="b0de8-115">Restart the VM.</span></span>

<span data-ttu-id="b0de8-116">Bu adımları aşağıdaki bölümlerde daha ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b0de8-116">These steps are described in more detail in the following sections.</span></span>

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-to-run-on-azure-vms"></a><span data-ttu-id="b0de8-117">Adım 1: Hyper-V sanal makineleri, VMware sanal makinelerini ve Azure Vm'lerinde çalıştırmak için fiziksel sunucularda çalışan iş yüklerini geçirme</span><span class="sxs-lookup"><span data-stu-id="b0de8-117">Step 1: Migrate workloads running on Hyper-V VMs, VMware VMs, and physical servers to run on Azure VMs</span></span>

<span data-ttu-id="b0de8-118">Çoğaltmayı ayarlama ve şirket içi geçirmek için Hyper-V, VMware ve fiziksel iş yüklerini azure'a, adımları [Azure Site Recovery ile Azure bölgeler arasında geçirmek Azure Iaas sanal makineleri](site-recovery-migrate-to-azure.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="b0de8-118">To set up replication and migrate your on-premises Hyper-V, VMware, and physical workloads to Azure, follow the steps in the [Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery](site-recovery-migrate-to-azure.md) article.</span></span> 

<span data-ttu-id="b0de8-119">Geçişten sonra yürütün veya bir yük devretme silme gerekmez.</span><span class="sxs-lookup"><span data-stu-id="b0de8-119">After migration, you don't need to commit or delete a failover.</span></span> <span data-ttu-id="b0de8-120">Bunun yerine, seçin **tam geçiş** seçeneği geçiş yapmak istediğiniz her makine için:</span><span class="sxs-lookup"><span data-stu-id="b0de8-120">Instead, select the **Complete Migration** option for each machine you want to migrate:</span></span>
1. <span data-ttu-id="b0de8-121">**Çoğaltılan Öğeler**’de VM’ye sağ tıklayıp **Geçişi Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b0de8-121">In **Replicated Items**, right-click the VM, and click **Complete Migration**.</span></span> <span data-ttu-id="b0de8-122">Tıklatın **Tamam** adımı tamamlamak için.</span><span class="sxs-lookup"><span data-stu-id="b0de8-122">Click **OK** to complete the step.</span></span> <span data-ttu-id="b0de8-123">Tam geçiş işine izleyerek VM Özellikleri'nde ilerleme durumunu izleyebilirsiniz **Site Recovery işleri**.</span><span class="sxs-lookup"><span data-stu-id="b0de8-123">You can track progress in the VM properties by monitoring the Complete Migration job in **Site Recovery jobs**.</span></span>
2. <span data-ttu-id="b0de8-124">**Tam geçiş** eylem geçiş işlemi tamamlandığında, makine için çoğaltmayı kaldırır ve makine için Site Recovery Faturalaması durdurulur.</span><span class="sxs-lookup"><span data-stu-id="b0de8-124">The **Complete Migration** action completes the migration process, removes replication for the machine, and stops Site Recovery billing for the machine.</span></span>

   ![tamgeçiş](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-the-azure-vm-agent-on-the-virtual-machine"></a><span data-ttu-id="b0de8-126">2. adım: Azure VM Aracısı sanal makineye yükleme</span><span class="sxs-lookup"><span data-stu-id="b0de8-126">Step 2: Install the Azure VM agent on the virtual machine</span></span>
<span data-ttu-id="b0de8-127">Azure [VM Aracısı](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) çözmek ve VM korunmasına yardımcı olmak için Site Recovery uzantı sanal makineye yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0de8-127">The Azure [VM agent](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) must be installed on the virtual machine for the Site Recovery extension to work and to help protect the VM.</span></span>

>[!IMPORTANT]
><span data-ttu-id="b0de8-128">Sürüm 9.7.0.0, Windows sanal makinelerde itibaren Mobility hizmeti yükleyicisinin en son kullanılabilir Azure VM Aracısı de yükler.</span><span class="sxs-lookup"><span data-stu-id="b0de8-128">Beginning with version 9.7.0.0, on Windows virtual machines, the Mobility service installer also installs the latest available Azure VM agent.</span></span> <span data-ttu-id="b0de8-129">Geçiş, sanal makine Site Recovery uzantısına dahil, herhangi bir VM uzantısı kullanılarak için önkoşul aracı yüklemesi karşılar.</span><span class="sxs-lookup"><span data-stu-id="b0de8-129">On migration, the virtual machine meets the agent installation prerequisite for using any VM extension, including the Site Recovery extension.</span></span> <span data-ttu-id="b0de8-130">Azure VM Aracısı yalnızca geçirilen makinede Mobility hizmeti 9.6 veya önceki bir sürümü ise el ile yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0de8-130">The Azure VM agent needs to be manually installed only if the Mobility service installed on the migrated machine is version 9.6 or earlier.</span></span>

<span data-ttu-id="b0de8-131">Aşağıdaki tabloda, yüklü olduğu VM Aracısı'nı yükleme ve doğrulama hakkında ek bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="b0de8-131">The following table provides additional information about installing the VM agent and validating that it was installed:</span></span>

| <span data-ttu-id="b0de8-132">**İşlem**</span><span class="sxs-lookup"><span data-stu-id="b0de8-132">**Operation**</span></span> | <span data-ttu-id="b0de8-133">**Windows**</span><span class="sxs-lookup"><span data-stu-id="b0de8-133">**Windows**</span></span> | <span data-ttu-id="b0de8-134">**Linux**</span><span class="sxs-lookup"><span data-stu-id="b0de8-134">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b0de8-135">VM Aracısı yükleme</span><span class="sxs-lookup"><span data-stu-id="b0de8-135">Installing the VM agent</span></span> |<span data-ttu-id="b0de8-136">[Aracı MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409) dosyasını indirip yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b0de8-136">Download and install the [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="b0de8-137">Yüklemeyi tamamlamak için yönetici ayrıcalıkları gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0de8-137">You need administrator privileges to complete the installation.</span></span> |<span data-ttu-id="b0de8-138">En son yükleme [Linux Aracısı](../virtual-machines/linux/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="b0de8-138">Install the latest [Linux agent](../virtual-machines/linux/agent-user-guide.md).</span></span> <span data-ttu-id="b0de8-139">Yüklemeyi tamamlamak için yönetici ayrıcalıkları gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0de8-139">You need administrator privileges to complete the installation.</span></span> <span data-ttu-id="b0de8-140">Aracı dağıtım depodan yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="b0de8-140">We recommend installing the agent from your distribution repository.</span></span> <span data-ttu-id="b0de8-141">Biz *değil önerilir* doğrudan Github'dan Linux VM Aracısı yükleme.</span><span class="sxs-lookup"><span data-stu-id="b0de8-141">We *do not recommend* installing the Linux VM agent directly from GitHub.</span></span>  |
| <span data-ttu-id="b0de8-142">VM Aracısı yüklemesini doğrulama</span><span class="sxs-lookup"><span data-stu-id="b0de8-142">Validating the VM agent installation</span></span> |<span data-ttu-id="b0de8-143">1. Azure VM'de C:\WindowsAzure\Packages klasöre göz atın.</span><span class="sxs-lookup"><span data-stu-id="b0de8-143">1. Browse to the C:\WindowsAzure\Packages folder in the Azure VM.</span></span> <span data-ttu-id="b0de8-144">WaAppAgent.exe dosyasını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0de8-144">You should see the WaAppAgent.exe file.</span></span> <br><span data-ttu-id="b0de8-145">2. Dosyaya sağ tıklayın, **Özellikler**'e gidin ve ardından **Ayrıntılar** sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="b0de8-145">2. Right-click the file, go to **Properties**, and then select the **Details** tab.</span></span> <span data-ttu-id="b0de8-146">**Ürün sürümü** alanı 2.6.1198.718 olmalıdır ya da daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="b0de8-146">The **Product Version** field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="b0de8-147">Yok</span><span class="sxs-lookup"><span data-stu-id="b0de8-147">N/A</span></span> |


### <a name="step-3-remove-the-mobility-service-from-the-migrated-virtual-machine"></a><span data-ttu-id="b0de8-148">3. adım: Mobility hizmeti geçirilen sanal makineden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="b0de8-148">Step 3: Remove the Mobility service from the migrated virtual machine</span></span>

<span data-ttu-id="b0de8-149">Şirket içi VMware makineleri veya fiziksel Windows/Linux sunucularda geçirdiyseniz, el ile Kaldır/geçirilen sanal makine Mobility hizmetinden kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0de8-149">If you have migrated your on-premises VMware machines or physical servers on Windows/Linux, you need to manually remove/uninstall the Mobility service from the migrated virtual machine.</span></span>

>[!IMPORTANT]
><span data-ttu-id="b0de8-150">Hyper-V Vm'lerini Azure'a geçişi için bu adım gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="b0de8-150">This step is not required for Hyper-V VMs migrated to Azure.</span></span>

#### <a name="uninstall-the-mobility-service-on-a-windows-server-vm"></a><span data-ttu-id="b0de8-151">Windows Server VM Mobility hizmeti Kaldır</span><span class="sxs-lookup"><span data-stu-id="b0de8-151">Uninstall the Mobility service on a Windows Server VM</span></span>
<span data-ttu-id="b0de8-152">Windows Server bilgisayarındaki Mobility hizmeti kaldırmak için aşağıdaki yöntemlerden birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b0de8-152">Use one of the following methods to uninstall the Mobility service on a Windows Server computer.</span></span>

##### <a name="uninstall-by-using-the-windows-ui"></a><span data-ttu-id="b0de8-153">Windows kullanıcı arabirimini kullanarak kaldırma</span><span class="sxs-lookup"><span data-stu-id="b0de8-153">Uninstall by using the Windows UI</span></span>
1. <span data-ttu-id="b0de8-154">Denetim Masası'nda seçin **programlar**.</span><span class="sxs-lookup"><span data-stu-id="b0de8-154">In the Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="b0de8-155">Seçin **Microsoft Azure Site Recovery Mobility hizmeti/ana hedef sunucu**ve ardından **kaldırma**.</span><span class="sxs-lookup"><span data-stu-id="b0de8-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

##### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="b0de8-156">Bir komut isteminde kaldırma</span><span class="sxs-lookup"><span data-stu-id="b0de8-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="b0de8-157">Yönetici olarak bir komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="b0de8-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="b0de8-158">Mobility hizmetini kaldırmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b0de8-158">To uninstall the Mobility service, run the following command:</span></span>

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-the-mobility-service-on-a-linux-computer"></a><span data-ttu-id="b0de8-159">Bir Linux bilgisayar üzerindeki mobilite hizmetini kaldırın</span><span class="sxs-lookup"><span data-stu-id="b0de8-159">Uninstall the Mobility service on a Linux computer</span></span>
1. <span data-ttu-id="b0de8-160">Linux sunucunuzda olarak oturum açın bir **kök** kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="b0de8-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="b0de8-161">Bir terminale için /user/local/ASR gidin.</span><span class="sxs-lookup"><span data-stu-id="b0de8-161">In a terminal, go to /user/local/ASR.</span></span>
3. <span data-ttu-id="b0de8-162">Mobility hizmetini kaldırmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b0de8-162">To uninstall the Mobility service, run the following command:</span></span>

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-the-vm"></a><span data-ttu-id="b0de8-163">4. adım: VM yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="b0de8-163">Step 4: Restart the VM</span></span>

<span data-ttu-id="b0de8-164">Mobility hizmetinin kaldırdıktan sonra başka bir Azure bölgesine çoğaltma ayarlama önce VM'yi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="b0de8-164">After you uninstall the Mobility service, restart the VM before you set up replication to another Azure region.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b0de8-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b0de8-165">Next steps</span></span>
- <span data-ttu-id="b0de8-166">İş yükleri tarafından korumaya başlamak [Azure sanal makineleri çoğaltmak](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="b0de8-166">Start protecting your workloads by [replicating Azure virtual machines](site-recovery-azure-to-azure.md).</span></span>
- <span data-ttu-id="b0de8-167">Daha fazla bilgi edinmek [Azure sanal makineleri çoğaltmak için kılavuz ağ](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="b0de8-167">Learn more about [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
