---
title: "aaaRemove sunucuları ve koruma devre dışı bırakma | Microsoft Docs"
description: "Bu makalede nasıl toounregister sunucuları bir Site kurtarma kasası ve sanal makineleri ve fiziksel sunucuları için toodisable korumayı açıklar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a><span data-ttu-id="2d5c5-103">Sunucuları kaldırma ve korumayı devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="2d5c5-103">Remove servers and disable protection</span></span>

<span data-ttu-id="2d5c5-104">Hello Azure Site Recovery hizmeti tooyour iş devamlılığı ve olağanüstü durum kurtarma (BCDR) stratejinize katkı sağlar.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-104">hello Azure Site Recovery service contributes tooyour business continuity and disaster recovery (BCDR) strategy.</span></span> <span data-ttu-id="2d5c5-105">Çoğaltma, yük devretme ve sanal makinelerin ve fiziksel sunucuları kurtarma Hello hizmet düzenler.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-105">hello service orchestrates replication, failover and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="2d5c5-106">Makineler çoğaltılmış tooAzure veya tooa ikincil şirket içi veri merkezi olabilir.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-106">Machines can be replicated tooAzure, or tooa secondary on-premises data center.</span></span> <span data-ttu-id="2d5c5-107">Hızlı bir genel bakış için [Azure Site Recovery nedir?](site-recovery-overview.md) konusunu okuyun.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-107">For a quick overview read [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>

<span data-ttu-id="2d5c5-108">Bu makalede nasıl hello Azure portal toounregister sunucularından bir kurtarma Hizmetleri kasası ve nasıl toodisable koruma makineler için Site Recovery tarafından korunan açıklanır.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-108">This article describes how toounregister servers from a Recovery Services vault in hello Azure portal, and how toodisable protection for machines protected by Site Recovery.</span></span>

<span data-ttu-id="2d5c5-109">Tüm yorumlarınızı ve sorularınızı bu makalenin veya hello hello altındaki sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="2d5c5-109">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="unregister-a-connected-configuration-server"></a><span data-ttu-id="2d5c5-110">Bağlantılı yapılandırma sunucusu kaydı</span><span class="sxs-lookup"><span data-stu-id="2d5c5-110">Unregister a connected configuration server</span></span>

<span data-ttu-id="2d5c5-111">VMware Vm'leri veya Windows/Linux fiziksel sunucuları tooAzure çoğaltma durumunda bir kasa bağlı yapılandırma sunucusundan gibi kaydını kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2d5c5-111">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister a connected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="2d5c5-112">Makine korumasını devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-112">Disable machine protection.</span></span> <span data-ttu-id="2d5c5-113">İçinde **korunan öğeler** > **çoğaltılan öğeler**, sağ hello makine > **silmek**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-113">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="2d5c5-114">Tüm ilkeler ilişkisini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-114">Disassociate any policies.</span></span> <span data-ttu-id="2d5c5-115">İçinde **Site Recovery altyapısı** > **için VMWare ve fiziksel makineler** > **çoğaltma ilkeleri**, hello çift tıklatın ilişkili ilke.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-115">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="2d5c5-116">Sağ hello yapılandırma sunucusu > **ilişkisini**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-116">Right-click hello configuration server > **Disassociate**.</span></span>
3. <span data-ttu-id="2d5c5-117">Herhangi bir ek şirket içi işlem veya ana hedef sunucuları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-117">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="2d5c5-118">İçinde **Site Recovery altyapısı** > **için VMWare ve fiziksel makineler** > **yapılandırma sunucularına**, sağ hello sunucu > **Silmek**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-118">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="2d5c5-119">Merhaba yapılandırma sunucusu silin.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-119">Delete hello configuration server.</span></span>
5. <span data-ttu-id="2d5c5-120">Merhaba ana hedef sunucu üzerinde çalışan hello mobilite hizmetini elle kaldırın (Bu ya da ayrı bir olacak sunucu veya hello yapılandırma sunucusu üzerinde çalışan).</span><span class="sxs-lookup"><span data-stu-id="2d5c5-120">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
6. <span data-ttu-id="2d5c5-121">Herhangi bir ek işlem sunucusu kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-121">Uninstall any additional process servers.</span></span>
7. <span data-ttu-id="2d5c5-122">Merhaba yapılandırma sunucusundan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-122">Uninstall hello configuration server.</span></span>
8. <span data-ttu-id="2d5c5-123">Merhaba yapılandırma sunucusunda Site Recovery tarafından yüklenen MySQL hello örneğini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-123">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
9. <span data-ttu-id="2d5c5-124">Merhaba yapılandırma sunucusu Hello kayıt defterinde hello anahtarını silmek ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-124">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-unconnected-configuration-server"></a><span data-ttu-id="2d5c5-125">Bağlantısız yapılandırma sunucusu kaydı</span><span class="sxs-lookup"><span data-stu-id="2d5c5-125">Unregister a unconnected configuration server</span></span>

<span data-ttu-id="2d5c5-126">VMware Vm'leri veya Windows/Linux fiziksel sunucuları tooAzure çoğaltma durumunda bir kasa bağlantısız yapılandırma sunucusundan gibi kaydını kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2d5c5-126">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister an unconnected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="2d5c5-127">Makine korumasını devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-127">Disable machine protection.</span></span> <span data-ttu-id="2d5c5-128">İçinde **korunan öğeler** > **çoğaltılan öğeler**, sağ hello makine > **silmek**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-128">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span> <span data-ttu-id="2d5c5-129">Seçin **hello makineyi yönetmeyi Durdur**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-129">Select **Stop managing hello machine**.</span></span>
2. <span data-ttu-id="2d5c5-130">Herhangi bir ek şirket içi işlem veya ana hedef sunucuları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-130">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="2d5c5-131">İçinde **Site Recovery altyapısı** > **için VMWare ve fiziksel makineler** > **yapılandırma sunucularına**, sağ hello sunucu > **Silmek**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-131">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
3. <span data-ttu-id="2d5c5-132">Merhaba yapılandırma sunucusu silin.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-132">Delete hello configuration server.</span></span>
4. <span data-ttu-id="2d5c5-133">Merhaba ana hedef sunucu üzerinde çalışan hello mobilite hizmetini elle kaldırın (Bu ya da ayrı bir olacak sunucu veya hello yapılandırma sunucusu üzerinde çalışan).</span><span class="sxs-lookup"><span data-stu-id="2d5c5-133">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
5. <span data-ttu-id="2d5c5-134">Herhangi bir ek işlem sunucusu kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-134">Uninstall any additional process servers.</span></span>
6. <span data-ttu-id="2d5c5-135">Merhaba yapılandırma sunucusundan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-135">Uninstall hello configuration server.</span></span>
7. <span data-ttu-id="2d5c5-136">Merhaba yapılandırma sunucusunda Site Recovery tarafından yüklenen MySQL hello örneğini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-136">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
8. <span data-ttu-id="2d5c5-137">Merhaba yapılandırma sunucusu Hello kayıt defterinde hello anahtarını silmek ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-137">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-connected-vmm-server"></a><span data-ttu-id="2d5c5-138">Bağlı bir VMM sunucusunun kaydı silinemedi</span><span class="sxs-lookup"><span data-stu-id="2d5c5-138">Unregister a connected VMM server</span></span>

<span data-ttu-id="2d5c5-139">En iyi uygulama, bu tooAzure bağlandığında hello VMM sunucusunun kaydı öneririz.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-139">As a best practice, we recommend that you unregister hello VMM server when it's connected tooAzure.</span></span> <span data-ttu-id="2d5c5-140">Bu ayarları hello VMM sunucularında (ve diğer eşleştirilmiş bulut VMM sunucularıyla) düzgün temizlendiğinden sağlar.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-140">This ensures that settings on hello VMM servers (and on other VMM servers with paired clouds) are cleaned up properly.</span></span> <span data-ttu-id="2d5c5-141">Bağlantı kalıcı bir sorun varsa, bağlantısız bir sunucu yalnızca kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-141">You should only remove an unconnected server if there's a permanent issue with connectivity.</span></span> <span data-ttu-id="2d5c5-142">Merhaba VMM sunucusu bağlı değil, gerekir toomanually betik tooclean ayarlarını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-142">If hello VMM server isn’t connected, you will need toomanually run a script tooclean up settings.</span></span>

1. <span data-ttu-id="2d5c5-143">Merhaba tooremove istediğiniz VMM sunucusu üzerinde bulutlarındaki sanal makineleri çoğaltmak durdurun.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-143">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="2d5c5-144">Merhaba toodelete istediğiniz VMM sunucusunu bulutlarda tarafından kullanılan tüm ağ eşlemeleri silin.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-144">Delete any network mappings used by clouds on hello VMM server you want toodelete.</span></span> <span data-ttu-id="2d5c5-145">İçinde **Site Recovery altyapısı** > **için System Center VMM** > **ağ eşlemesi**, hello ağ eşlemesi sağ tıklayın >  **Silme**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-145">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="2d5c5-146">Merhaba tooremove istediğiniz VMM sunucusunu bulutlarda ilkelerden çoğaltma ilişkisini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-146">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="2d5c5-147">İçinde **Site Recovery altyapısı** > **için System Center VMM** >  **çoğaltma ilkeleri**, ilişkili hello ilkeye çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-147">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="2d5c5-148">Merhaba buluta sağ tıklayın > **ilişkisini**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-148">Right-click hello cloud > **Disassociate**.</span></span>
4. <span data-ttu-id="2d5c5-149">Merhaba VMM sunucusu veya etkin VMM düğümü silin.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-149">Delete hello VMM server or active VMM node.</span></span> <span data-ttu-id="2d5c5-150">İçinde **Site Recovery altyapısı** > **için System Center VMM** > **VMM sunucuları**, sağ hello server >  **Silme**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-150">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
5. <span data-ttu-id="2d5c5-151">Merhaba sağlayıcısı hello VMM sunucusunda el ile kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-151">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="2d5c5-152">Bir kümeniz varsa, tüm düğümlerden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-152">If you have a cluster, remove from all nodes.</span></span>
6. <span data-ttu-id="2d5c5-153">TooAzure çoğaltıyorsanız el ile silinmiş hello bulutlarındaki Hyper-V konakları hello Microsoft Kurtarma Hizmetleri Aracısı'nı kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-153">If you're replicating tooAzure, manually remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>



### <a name="unregister-an-unconnected-vmm-server"></a><span data-ttu-id="2d5c5-154">Bağlantısız bir VMM sunucusunun kaydı silinemedi</span><span class="sxs-lookup"><span data-stu-id="2d5c5-154">Unregister an unconnected VMM server</span></span>

1. <span data-ttu-id="2d5c5-155">Merhaba tooremove istediğiniz VMM sunucusu üzerinde bulutlarındaki sanal makineleri çoğaltmak durdurun.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-155">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="2d5c5-156">Toodelete istediğiniz hello VMM sunucusundaki Bulutlar tarafından kullanılan tüm ağ eşlemeleri silin.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-156">Delete any network mappings used by clouds on hello VMM server that you want toodelete.</span></span> <span data-ttu-id="2d5c5-157">İçinde **Site Recovery altyapısı** > **için System Center VMM** > **ağ eşlemesi**, hello ağ eşlemesi sağ tıklayın >  **Silme**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-157">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="2d5c5-158">Merhaba VMM sunucusu Hello Kimliğini not alın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-158">Note hello ID of hello VMM server.</span></span>
4. <span data-ttu-id="2d5c5-159">Merhaba tooremove istediğiniz VMM sunucusunu bulutlarda ilkelerden çoğaltma ilişkisini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-159">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="2d5c5-160">İçinde **Site Recovery altyapısı** > **için System Center VMM** >  **çoğaltma ilkeleri**, ilişkili hello ilkeye çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-160">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="2d5c5-161">Merhaba buluta sağ tıklayın > **ilişkisini**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-161">Right-click hello cloud > **Disassociate**.</span></span>
5. <span data-ttu-id="2d5c5-162">Merhaba VMM sunucusu veya etkin düğüm silin.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-162">Delete hello VMM server or active node.</span></span> <span data-ttu-id="2d5c5-163">İçinde **Site Recovery altyapısı** > **için System Center VMM** > **VMM sunucuları**, sağ hello server >  **Silme**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-163">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
6. <span data-ttu-id="2d5c5-164">İndirme ve çalıştırma hello [temizleme betiğini](http://aka.ms/asr-cleanup-script-vmm) hello VMM sunucusunda.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-164">Download and run hello [cleanup script](http://aka.ms/asr-cleanup-script-vmm) on hello VMM server.</span></span> <span data-ttu-id="2d5c5-165">PowerShell ile Merhaba açmak **yönetici olarak çalıştır** seçeneği, toochange hello yürütme İlkesi hello varsayılan (LocalMachine) kapsam için.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-165">Open PowerShell with hello **Run as Administrator** option, toochange hello execution policy for hello default (LocalMachine) scope.</span></span> <span data-ttu-id="2d5c5-166">Merhaba komut dosyasında hello tooremove istediğiniz VMM sunucusunu hello Kimliğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-166">In hello script, specify hello ID of hello VMM server you want tooremove.</span></span> <span data-ttu-id="2d5c5-167">Merhaba betik kaydı ve bulut eşleştirme bilgilerini hello sunucusundan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-167">hello script removes registration and cloud pairing information from hello server.</span></span>
5. <span data-ttu-id="2d5c5-168">Merhaba tooremove istediğiniz VMM sunucusu üzerinde Bulutları ile eşleştirilmiş bulut içeren herhangi bir VMM sunucularında Hello temizleme betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-168">Run hello cleanup script on any other VMM servers that contain clouds that are paired with clouds on hello VMM server you want tooremove.</span></span>
6. <span data-ttu-id="2d5c5-169">Merhaba sağlayıcısı yüklü olan tüm diğer pasif VMM küme düğümlerine Hello temizleme betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-169">Run hello  cleanup script on any other passive VMM cluster nodes that have hello Provider installed.</span></span>
7. <span data-ttu-id="2d5c5-170">Merhaba sağlayıcısı hello VMM sunucusunda el ile kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-170">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="2d5c5-171">Bir kümeniz varsa, tüm düğümlerden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-171">If you have a cluster, remove from all nodes.</span></span>
8. <span data-ttu-id="2d5c5-172">TooAzure çoğaltma, hello Microsoft Kurtarma Hizmetleri aracısını silinmiş hello bulutlarındaki Hyper-V konakları kaldırırsanız.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-172">If you replicating tooAzure, you can remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a><span data-ttu-id="2d5c5-173">Bir Hyper-V sitesi bir Hyper-V ana bilgisayar kaydı</span><span class="sxs-lookup"><span data-stu-id="2d5c5-173">Unregister a Hyper-V host in a Hyper-V Site</span></span>

<span data-ttu-id="2d5c5-174">VMM tarafından yönetilmeyen Hyper-V konaklarının, Hyper-V sitesi toplanır.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-174">Hyper-V hosts that aren't managed by VMM are gathered into a Hyper-V site.</span></span> <span data-ttu-id="2d5c5-175">Bir konak bir Hyper-V sitede aşağıdaki gibi kaldırın:</span><span class="sxs-lookup"><span data-stu-id="2d5c5-175">Remove a host in a Hyper-V site as follows:</span></span>

1. <span data-ttu-id="2d5c5-176">Hyper-V hello ana bilgisayarda yer alan VM'ler için çoğaltma devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-176">Disable replication for Hyper-V VMs located on hello host.</span></span>
2. <span data-ttu-id="2d5c5-177">Merhaba Hyper-V sitesi için ilkeler ilişkisini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-177">Disassociate policies for hello Hyper-V site.</span></span> <span data-ttu-id="2d5c5-178">İçinde **Site Recovery altyapısı** > **için Hyper-V sitelerini** >  **çoğaltma ilkeleri**, ilişkili hello ilkeye çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-178">In **Site Recovery Infrastructure** > **For Hyper-V Sites** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="2d5c5-179">Sağ hello site > **ilişkisini**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-179">Right-click hello site > **Disassociate**.</span></span>
3. <span data-ttu-id="2d5c5-180">Hyper-V konakları silin.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-180">Delete Hyper-V hosts.</span></span> <span data-ttu-id="2d5c5-181">İçinde **Site Recovery altyapısı** > **için System Center VMM** > **Hyper-V konakları**, sağ hello server >  **Silme**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-181">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Hosts**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="2d5c5-182">Tüm konaklar ondan temizlendikten sonra hello Hyper-V sitesi silin.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-182">Delete hello Hyper-V site after all hosts have been removed from it.</span></span> <span data-ttu-id="2d5c5-183">İçinde **Site Recovery altyapısı** > **için System Center VMM** > **Hyper-V sitelerini**, sağ hello site >  **Silme**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-183">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Sites**, right-click hello site > **Delete**.</span></span>
5. <span data-ttu-id="2d5c5-184">Komut dosyası kaldırdığınız her Hyper-V ana bilgisayarda aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-184">Run hello following script on each Hyper-V host that you removed.</span></span> <span data-ttu-id="2d5c5-185">Merhaba betik hello sunucusundaki ayarları temizler ve hello kasasından kaydını siler.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-185">hello script cleans up settings on hello server, and unregisters it from hello vault.</span></span>


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping hello Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a><span data-ttu-id="2d5c5-186">VMware VM veya fiziksel sunucu için koruma devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="2d5c5-186">Disable protection for a VMware VM or physical server</span></span>

1. <span data-ttu-id="2d5c5-187">İçinde **korunan öğeler** > **çoğaltılan öğeler**, sağ hello makine > **silmek**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-187">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="2d5c5-188">İçinde **makineyi Kaldır**, aşağıdaki seçeneklerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="2d5c5-188">In **Remove Machine**, select one of these options:</span></span>
    - <span data-ttu-id="2d5c5-189">**(Önerilen) hello makine için korumayı devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-189">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="2d5c5-190">Bu seçenek toostop Hello makinenin çoğaltıldığını kullanın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-190">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="2d5c5-191">Site Recovery ayarları otomatik olarak temizlenecek.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-191">Site Recovery settings will be cleaned up automatically.</span></span> <span data-ttu-id="2d5c5-192">Aşağıdaki durumlarda hello bu seçeneği yalnızca görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="2d5c5-192">You will only see this option in hello following circumstances:</span></span>
        - <span data-ttu-id="2d5c5-193">**Merhaba VM birim yeniden boyutlandırılıyor**— sanal bir birim hello yeniden boyutlandırdığınızda makine kritik duruma geçer.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-193">**You've resized hello VM volume**—When you resize a volume hello virtual machine goes into a critical state.</span></span> <span data-ttu-id="2d5c5-194">Kurtarma noktalarının azure'da korurken bu seçeneği toodisables koruma seçin.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-194">Select this option toodisables protection while retaining recovery points in Azure.</span></span> <span data-ttu-id="2d5c5-195">Merhaba makine için korumayı yeniden etkinleştirdiğinizde, hello veri hello yeniden boyutlandırılmış birim için aktarılan tooAzure olur.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-195">When you enable protection for hello machine again, hello data for hello resized volume will be transferred tooAzure.</span></span>
        - <span data-ttu-id="2d5c5-196">**Bir yük devretme yakın zamanda çalıştırdıysanız**— ortamınızın bir yük devretme tootest çalıştırdıktan sonra şirket içi makineleri yeniden koruma bu seçeneği toostart seçin.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-196">**You've recently run a failover**—After you've run a failover tootest your environment, select this option toostart protecting on-premises machines again.</span></span> <span data-ttu-id="2d5c5-197">Her bir sanal makine devre dışı bırakır ve ardından tooenable koruma için yeniden gereksinim duyarsınız.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-197">It disables each virtual machine, and then you need tooenable protection for them again.</span></span> <span data-ttu-id="2d5c5-198">Bu ayar devre dışı bırakma hello makineyle azure'da hello çoğaltma sanal makine etkilemez.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-198">Disabling hello machine with this setting doesn't affect hello replica virtual machine in Azure.</span></span> <span data-ttu-id="2d5c5-199">Merhaba Mobility hizmeti hello makineden kaldırmak yok.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-199">Don't uninstall hello Mobility service from hello machine.</span></span>
    - <span data-ttu-id="2d5c5-200">**Merhaba makineyi yönetmeyi Durdur**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-200">**Stop managing hello machine**.</span></span> <span data-ttu-id="2d5c5-201">Bu seçeneği belirlerseniz, hello makine yalnızca hello kasadan kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-201">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="2d5c5-202">Şirket içi hello makine için koruma ayarları etkilenmeyecek.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-202">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="2d5c5-203">tooremove ayarları hello makinesindeki ve tooremove hello hello Azure aboneliği makineden hello Mobility hizmeti kaldırarak tooclean hello ayarlarının gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-203">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings by uninstalling hello Mobility service.</span></span>

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a><span data-ttu-id="2d5c5-204">VMM bulutundaki Hyper-V VM için korumayı devre dışı</span><span class="sxs-lookup"><span data-stu-id="2d5c5-204">Disable protection for a Hyper-V VM in a VMM cloud</span></span>

1. <span data-ttu-id="2d5c5-205">İçinde **korunan öğeler** > **çoğaltılan öğeler**, sağ hello makine > **silmek**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-205">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="2d5c5-206">İçinde **makineyi Kaldır**, aşağıdaki seçeneklerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="2d5c5-206">In **Remove Machine**, select one of these options:</span></span>

    - <span data-ttu-id="2d5c5-207">**(Önerilen) hello makine için korumayı devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-207">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="2d5c5-208">Bu seçenek toostop Hello makinenin çoğaltıldığını kullanın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-208">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="2d5c5-209">Site Recovery ayarları otomatik olarak temizlenecek.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-209">Site Recovery settings will be cleaned up automatically.</span></span>
    - <span data-ttu-id="2d5c5-210">**Merhaba makineyi yönetmeyi Durdur**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-210">**Stop managing hello machine**.</span></span> <span data-ttu-id="2d5c5-211">Bu seçeneği belirlerseniz, hello makine yalnızca hello kasadan kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-211">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="2d5c5-212">Şirket içi hello makine için koruma ayarları etkilenmeyecek.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-212">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="2d5c5-213">tooremove ayarları hello makinesindeki ve tooremove hello hello Azure aboneliği makineden, tooclean hello ayarlarının yukarı el ile aşağıdaki hello yönergeleri kullanarak gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-213">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings up manually, using hello instructions below.</span></span> <span data-ttu-id="2d5c5-214">Toodelete hello sanal makine ve sabit disk seçin, bunlar hello hedef konumundan kaldırılması olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-214">Note that if you select toodelete hello virtual machine and its hard disks, they'll be removed from hello target location.</span></span>

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a><span data-ttu-id="2d5c5-215">Koruma ayarlarını - çoğaltma tooa ikincil VMM sitesi Temizle</span><span class="sxs-lookup"><span data-stu-id="2d5c5-215">Clean up protection settings - replication tooa secondary VMM site</span></span>

<span data-ttu-id="2d5c5-216">Seçtiyseniz **hello makineyi yönetmeyi Durdur** ve tooa ikincil site, çoğaltma çalıştırdığınız bu betiği hello birincil sunucu tooclean hello ayarlarını hello birincil sanal makine için.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-216">If you selected **Stop managing hello machine** and you replicating tooa secondary site, run this script on hello primary server tooclean up hello settings for hello primary virtual machine.</span></span> <span data-ttu-id="2d5c5-217">Merhaba VMM konsolunda hello PowerShell düğmesi tooopen hello VMM PowerShell Konsolu'nu tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-217">In hello VMM console click hello PowerShell button tooopen hello VMM PowerShell console.</span></span> <span data-ttu-id="2d5c5-218">SQLVM1 sanal makineniz hello adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-218">Replace SQLVM1 with hello name of your virtual machine.</span></span>

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="2d5c5-219">Bu komut dosyası tooclean hello ayarlarını hello ikincil sanal makinenin Hello ikincil VMM sunucusunda çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2d5c5-219">On hello secondary VMM server run this script tooclean up hello settings for hello secondary virtual machine:</span></span>

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. <span data-ttu-id="2d5c5-220">Böylece Hello ikincil VM yeniden hello VMM konsolunda algılanan hello ikincil VMM sunucusunda hello Hyper-V konak sunucusunda hello sanal makineleri yenileyin.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-220">On hello secondary VMM server, refresh hello virtual machines on hello Hyper-V host server, so that hello secondary VM gets detected again in hello VMM console.</span></span>
4. <span data-ttu-id="2d5c5-221">Yukarıdaki adımları Hello hello çoğaltma ayarları hello VMM sunucusunda temizlenir.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-221">hello above steps clear up hello replication settings on hello VMM server.</span></span> <span data-ttu-id="2d5c5-222">Merhaba sanal makinesi, aşağıdaki komut dosyası hello çalıştırmak için toostop çoğaltma istiyorsanız, birincil ve ikincil VM'ler hello.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-222">If you want toostop replication for hello virtual machine, run hello following script oh hello primary and secondary VMs.</span></span> <span data-ttu-id="2d5c5-223">SQLVM1 sanal makineniz hello adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-223">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a><span data-ttu-id="2d5c5-224">Koruma ayarlarını - çoğaltma tooAzure Temizle</span><span class="sxs-lookup"><span data-stu-id="2d5c5-224">Clean up protection settings - replication tooAzure</span></span>

1. <span data-ttu-id="2d5c5-225">Seçtiyseniz **hello makineyi yönetmeyi Durdur** ve çoğaltma tooAzure, hello VMM konsolundan PowerShell kullanarak hello kaynak VMM sunucusunda, bu komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-225">If you selected **Stop managing hello machine** and you replicate tooAzure, run this script on hello source VMM server, using PowerShell from hello VMM console.</span></span>
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="2d5c5-226">Yukarıdaki adımları Hello hello VMM sunucusundaki hello çoğaltma ayarları temizleyin.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-226">hello above steps clear hello replication settings on hello VMM server.</span></span> <span data-ttu-id="2d5c5-227">toostop çoğaltma hello Hyper-V ana bilgisayar sunucusunda çalışan hello sanal makine için bu komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-227">toostop replication for hello virtual machine running on hello Hyper-V host server, run this script.</span></span> <span data-ttu-id="2d5c5-228">SQLVM1 hello adıyla bir sanal makine ve host01.contoso.com hello hello Hyper-V konak sunucusu adını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-228">Replace SQLVM1 with hello name of your virtual machine, and host01.contoso.com with hello name of hello Hyper-V host server.</span></span>

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a><span data-ttu-id="2d5c5-229">Bir Hyper-V sitesindeki bir Hyper-V sanal makine için korumayı devre dışı bırakın</span><span class="sxs-lookup"><span data-stu-id="2d5c5-229">Disable protection for a Hyper-V VM in a Hyper-V Site</span></span>

<span data-ttu-id="2d5c5-230">Bir VMM Sunucu olmadan Hyper-V sanal makineleri tooAzure çoğaltma yapıyorsanız bu yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-230">Use this procedure if you're replicating Hyper-V VMs tooAzure without a VMM server.</span></span>

1. <span data-ttu-id="2d5c5-231">İçinde **korunan öğeler** > **çoğaltılan öğeler**, sağ hello makine > **silmek**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-231">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="2d5c5-232">İçinde **makineyi Kaldır**, aşağıdaki seçenekleri şu hello seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2d5c5-232">In **Remove Machine**, you can select hello following options:</span></span>

   - <span data-ttu-id="2d5c5-233">**(Önerilen) hello makine için korumayı devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-233">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="2d5c5-234">Bu seçenek toostop Hello makinenin çoğaltıldığını kullanın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-234">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="2d5c5-235">Site Recovery ayarları otomatik olarak temizlenecek.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-235">Site Recovery settings will be cleaned up automatically.</span></span>
   - <span data-ttu-id="2d5c5-236">**Merhaba makineyi yönetmeyi Durdur**.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-236">**Stop managing hello machine**.</span></span> <span data-ttu-id="2d5c5-237">Bu seçeneği belirlerseniz hello makine hello kasadan yalnızca kaldırılacak.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-237">If you select this option hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="2d5c5-238">Şirket içi hello makine için koruma ayarları etkilenmeyecek.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-238">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="2d5c5-239">tooremove ayarları hello makinesindeki ve hello Azure aboneliği tooremove hello sanal makineden, tooclean hello ayarlarını yukarı el ile yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-239">tooremove settings on hello machine, and tooremove hello virtual machine from hello Azure subscription, you need tooclean hello settings up manually.</span></span> <span data-ttu-id="2d5c5-240">Toodelete hello sanal makine ve kendi sabit diskleri seçerseniz hello hedef konumundan kaldırılacak.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-240">If you select toodelete hello virtual machine and its hard disks they will be removed from hello target location.</span></span>
3. <span data-ttu-id="2d5c5-241">Seçtiyseniz **hello makineyi yönetmeyi Durdur**, tooremove çoğaltma hello sanal makine için bu betiği hello kaynak Hyper-V ana bilgisayar sunucusunda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-241">If you selected **Stop managing hello machine**, run this script on hello source Hyper-V host server, tooremove replication for hello virtual machine.</span></span> <span data-ttu-id="2d5c5-242">SQLVM1 sanal makineniz hello adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2d5c5-242">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
