---
title: "Sunucuları kaldırın ve koruma devre dışı bırakma | Microsoft Docs"
description: "Bu makalede Site Recovery kasası sunucularından kaydı ve sanal makineleri ve fiziksel sunucuları için korumayı devre dışı bırakmak için açıklar."
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
ms.openlocfilehash: 43f92a35dc9b04584badd1c9f1152470246b5012
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="remove-servers-and-disable-protection"></a><span data-ttu-id="e9f8b-103">Sunucuları kaldırma ve korumayı devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="e9f8b-103">Remove servers and disable protection</span></span>

<span data-ttu-id="e9f8b-104">Azure Site Recovery hizmeti, iş sürekliliği ve olağanüstü durum kurtarma (BCDR) stratejinize katkı sağlar.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-104">The Azure Site Recovery service contributes to your business continuity and disaster recovery (BCDR) strategy.</span></span> <span data-ttu-id="e9f8b-105">Hizmet, çoğaltma, yük devretme ve sanal makinelerin ve fiziksel sunucuları kurtarma düzenler.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-105">The service orchestrates replication, failover and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="e9f8b-106">Makineler, Azure'a veya bir ikincil şirket içi veri merkezine çoğaltılabilir.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-106">Machines can be replicated to Azure, or to a secondary on-premises data center.</span></span> <span data-ttu-id="e9f8b-107">Hızlı bir genel bakış için [Azure Site Recovery nedir?](site-recovery-overview.md) konusunu okuyun.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-107">For a quick overview read [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>

<span data-ttu-id="e9f8b-108">Bu makalede, Azure portalında bir kurtarma Hizmetleri kasası sunucularından kaydı etme ve Site Recovery tarafından korunan makineler için korumayı devre dışı bırakma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-108">This article describes how to unregister servers from a Recovery Services vault in the Azure portal, and how to disable protection for machines protected by Site Recovery.</span></span>

<span data-ttu-id="e9f8b-109">Tüm yorumlarınızı ve sorularınızı bu makalenin alt kısmında veya [Azure Kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)'nda paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-109">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="unregister-a-connected-configuration-server"></a><span data-ttu-id="e9f8b-110">Bağlantılı yapılandırma sunucusu kaydı</span><span class="sxs-lookup"><span data-stu-id="e9f8b-110">Unregister a connected configuration server</span></span>

<span data-ttu-id="e9f8b-111">VMware Vm'leri veya Windows/Linux fiziksel sunucuları Azure'a çoğaltma durumunda bir kasa bağlı yapılandırma sunucusundan gibi kaydını kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e9f8b-111">If you replicate VMware VMs or Windows/Linux physical servers to Azure, you can unregister a connected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="e9f8b-112">Makine korumasını devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-112">Disable machine protection.</span></span> <span data-ttu-id="e9f8b-113">İçinde **korunan öğeler** > **çoğaltılan öğeler**, makine adını sağ tıklayın > **silmek**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-113">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="e9f8b-114">Tüm ilkeler ilişkisini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-114">Disassociate any policies.</span></span> <span data-ttu-id="e9f8b-115">İçinde **Site Recovery altyapısı** > **için VMWare ve fiziksel makineler** > **çoğaltma ilkeleri**, ilişkili ilkeye çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-115">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="e9f8b-116">Yapılandırma sunucusu sağ tıklayın > **ilişkisini**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-116">Right-click the configuration server > **Disassociate**.</span></span>
3. <span data-ttu-id="e9f8b-117">Herhangi bir ek şirket içi işlem veya ana hedef sunucuları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-117">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="e9f8b-118">İçinde **Site Recovery altyapısı** > **için VMWare ve fiziksel makineler** > **yapılandırma sunucularına**, sunucuya sağ tıklayın > **silmek**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-118">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click the server > **Delete**.</span></span>
4. <span data-ttu-id="e9f8b-119">Yapılandırma sunucusu silin.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-119">Delete the configuration server.</span></span>
5. <span data-ttu-id="e9f8b-120">Ana hedef sunucu üzerinde çalışan mobilite hizmetini elle kaldırın (Bu ya da ayrı bir olacak sunucu veya yapılandırma sunucusu üzerinde çalışan).</span><span class="sxs-lookup"><span data-stu-id="e9f8b-120">Manually uninstall the Mobility service running on the master target server (this will be either a separate server, or running on the configuration server).</span></span>
6. <span data-ttu-id="e9f8b-121">Herhangi bir ek işlem sunucusu kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-121">Uninstall any additional process servers.</span></span>
7. <span data-ttu-id="e9f8b-122">Yapılandırma sunucusundan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-122">Uninstall the configuration server.</span></span>
8. <span data-ttu-id="e9f8b-123">Yapılandırma sunucusunda Site Recovery tarafından yüklenen MySQL örneğini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-123">On the configuration server, uninstall the instance of MySQL that was installed by Site Recovery.</span></span>
9. <span data-ttu-id="e9f8b-124">Yapılandırma sunucusu kayıt defterinde anahtar silinmeye ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-124">In the registry of the configuration server delete the key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-unconnected-configuration-server"></a><span data-ttu-id="e9f8b-125">Bağlantısız yapılandırma sunucusu kaydı</span><span class="sxs-lookup"><span data-stu-id="e9f8b-125">Unregister a unconnected configuration server</span></span>

<span data-ttu-id="e9f8b-126">VMware Vm'leri veya Windows/Linux fiziksel sunucuları Azure'a çoğaltma durumunda bir kasa bağlantısız yapılandırma sunucusundan gibi kaydını kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e9f8b-126">If you replicate VMware VMs or Windows/Linux physical servers to Azure, you can unregister an unconnected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="e9f8b-127">Makine korumasını devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-127">Disable machine protection.</span></span> <span data-ttu-id="e9f8b-128">İçinde **korunan öğeler** > **çoğaltılan öğeler**, makine adını sağ tıklayın > **silmek**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-128">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span> <span data-ttu-id="e9f8b-129">Seçin **makineyi yönetmeyi Durdur**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-129">Select **Stop managing the machine**.</span></span>
2. <span data-ttu-id="e9f8b-130">Herhangi bir ek şirket içi işlem veya ana hedef sunucuları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-130">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="e9f8b-131">İçinde **Site Recovery altyapısı** > **için VMWare ve fiziksel makineler** > **yapılandırma sunucularına**, sunucuya sağ tıklayın > **silmek**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-131">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click the server > **Delete**.</span></span>
3. <span data-ttu-id="e9f8b-132">Yapılandırma sunucusu silin.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-132">Delete the configuration server.</span></span>
4. <span data-ttu-id="e9f8b-133">Ana hedef sunucu üzerinde çalışan mobilite hizmetini elle kaldırın (Bu ya da ayrı bir olacak sunucu veya yapılandırma sunucusu üzerinde çalışan).</span><span class="sxs-lookup"><span data-stu-id="e9f8b-133">Manually uninstall the Mobility service running on the master target server (this will be either a separate server, or running on the configuration server).</span></span>
5. <span data-ttu-id="e9f8b-134">Herhangi bir ek işlem sunucusu kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-134">Uninstall any additional process servers.</span></span>
6. <span data-ttu-id="e9f8b-135">Yapılandırma sunucusundan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-135">Uninstall the configuration server.</span></span>
7. <span data-ttu-id="e9f8b-136">Yapılandırma sunucusunda Site Recovery tarafından yüklenen MySQL örneğini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-136">On the configuration server, uninstall the instance of MySQL that was installed by Site Recovery.</span></span>
8. <span data-ttu-id="e9f8b-137">Yapılandırma sunucusu kayıt defterinde anahtar silinmeye ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-137">In the registry of the configuration server delete the key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-connected-vmm-server"></a><span data-ttu-id="e9f8b-138">Bağlı bir VMM sunucusunun kaydı silinemedi</span><span class="sxs-lookup"><span data-stu-id="e9f8b-138">Unregister a connected VMM server</span></span>

<span data-ttu-id="e9f8b-139">En iyi uygulama, Azure'a bağlıyken VMM sunucusunun kaydı öneririz.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-139">As a best practice, we recommend that you unregister the VMM server when it's connected to Azure.</span></span> <span data-ttu-id="e9f8b-140">Bu ayarları VMM sunucularında (ve diğer eşleştirilmiş bulut VMM sunucularıyla) düzgün temizlendiğinden sağlar.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-140">This ensures that settings on the VMM servers (and on other VMM servers with paired clouds) are cleaned up properly.</span></span> <span data-ttu-id="e9f8b-141">Bağlantı kalıcı bir sorun varsa, bağlantısız bir sunucu yalnızca kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-141">You should only remove an unconnected server if there's a permanent issue with connectivity.</span></span> <span data-ttu-id="e9f8b-142">VMM sunucusu bağlı değilse, el ile ayarlarını temizlemek için bir komut dosyasını çalıştırmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-142">If the VMM server isn’t connected, you will need to manually run a script to clean up settings.</span></span>

1. <span data-ttu-id="e9f8b-143">Kaldırmak istediğiniz VMM sunucusundaki sanal makineleri çoğaltmak durdurun.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-143">Stop replicating VMs in clouds on the VMM server you want to remove.</span></span>
2. <span data-ttu-id="e9f8b-144">Silmek istediğiniz VMM sunucusundaki Bulutlar tarafından kullanılan tüm ağ eşlemeleri silin.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-144">Delete any network mappings used by clouds on the VMM server you want to delete.</span></span> <span data-ttu-id="e9f8b-145">İçinde **Site Recovery altyapısı** > **için System Center VMM** > **ağ eşlemesi**, ağ eşlemesi sağ tıklayın > **silmek**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-145">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click the network mapping > **Delete**.</span></span>
3. <span data-ttu-id="e9f8b-146">Kaldırmak istediğiniz VMM sunucusundaki Bulutlar ilkelerden çoğaltma ilişkisini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-146">Disassociate replication policies from clouds on the VMM server you want to remove.</span></span>  <span data-ttu-id="e9f8b-147">İçinde **Site Recovery altyapısı** > **için System Center VMM** >  **çoğaltma ilkeleri**, ilişkili ilkeye çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-147">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="e9f8b-148">Buluta sağ tıklayın > **ilişkisini**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-148">Right-click the cloud > **Disassociate**.</span></span>
4. <span data-ttu-id="e9f8b-149">VMM sunucusu veya etkin VMM düğümü silin.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-149">Delete the VMM server or active VMM node.</span></span> <span data-ttu-id="e9f8b-150">İçinde **Site Recovery altyapısı** > **için System Center VMM** > **VMM sunucuları**, sunucuya sağ tıklayın > **silmek**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-150">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click the server > **Delete**.</span></span>
5. <span data-ttu-id="e9f8b-151">Sağlayıcı VMM sunucusunda el ile kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-151">Uninstall the Provider manually on the VMM server.</span></span> <span data-ttu-id="e9f8b-152">Bir kümeniz varsa, tüm düğümlerden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-152">If you have a cluster, remove from all nodes.</span></span>
6. <span data-ttu-id="e9f8b-153">El ile Azure'da çoğaltıyorsanız Microsoft Kurtarma Hizmetleri aracısını silinen bulutlarındaki Hyper-V konakları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-153">If you're replicating to Azure, manually remove the Microsoft Recovery Services agent from Hyper-V hosts in the deleted clouds.</span></span>



### <a name="unregister-an-unconnected-vmm-server"></a><span data-ttu-id="e9f8b-154">Bağlantısız bir VMM sunucusunun kaydı silinemedi</span><span class="sxs-lookup"><span data-stu-id="e9f8b-154">Unregister an unconnected VMM server</span></span>

1. <span data-ttu-id="e9f8b-155">Kaldırmak istediğiniz VMM sunucusundaki sanal makineleri çoğaltmak durdurun.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-155">Stop replicating VMs in clouds on the VMM server you want to remove.</span></span>
2. <span data-ttu-id="e9f8b-156">Silmek istediğiniz VMM sunucusundaki Bulutlar tarafından kullanılan tüm ağ eşlemeleri silin.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-156">Delete any network mappings used by clouds on the VMM server that you want to delete.</span></span> <span data-ttu-id="e9f8b-157">İçinde **Site Recovery altyapısı** > **için System Center VMM** > **ağ eşlemesi**, ağ eşlemesi sağ tıklayın > **silmek**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-157">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click the network mapping > **Delete**.</span></span>
3. <span data-ttu-id="e9f8b-158">VMM sunucusu Kimliğini not alın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-158">Note the ID of the VMM server.</span></span>
4. <span data-ttu-id="e9f8b-159">Kaldırmak istediğiniz VMM sunucusundaki Bulutlar ilkelerden çoğaltma ilişkisini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-159">Disassociate replication policies from clouds on the VMM server you want to remove.</span></span>  <span data-ttu-id="e9f8b-160">İçinde **Site Recovery altyapısı** > **için System Center VMM** >  **çoğaltma ilkeleri**, ilişkili ilkeye çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-160">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="e9f8b-161">Buluta sağ tıklayın > **ilişkisini**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-161">Right-click the cloud > **Disassociate**.</span></span>
5. <span data-ttu-id="e9f8b-162">VMM sunucusu veya etkin düğüm silin.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-162">Delete the VMM server or active node.</span></span> <span data-ttu-id="e9f8b-163">İçinde **Site Recovery altyapısı** > **için System Center VMM** > **VMM sunucuları**, sunucuya sağ tıklayın > **silmek**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-163">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click the server > **Delete**.</span></span>
6. <span data-ttu-id="e9f8b-164">İndirme ve çalıştırma [temizleme betiğini](http://aka.ms/asr-cleanup-script-vmm) VMM sunucusunda.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-164">Download and run the [cleanup script](http://aka.ms/asr-cleanup-script-vmm) on the VMM server.</span></span> <span data-ttu-id="e9f8b-165">PowerShell ile açmak **yönetici olarak çalıştır** seçeneği, varsayılan (LocalMachine) kapsamı yürütme ilkesini değiştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-165">Open PowerShell with the **Run as Administrator** option, to change the execution policy for the default (LocalMachine) scope.</span></span> <span data-ttu-id="e9f8b-166">Komut dosyasında, kaldırmak istediğiniz VMM sunucusunu Kimliğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-166">In the script, specify the ID of the VMM server you want to remove.</span></span> <span data-ttu-id="e9f8b-167">Betik kaydı ve bulut eşleştirme bilgilerini sunucusundan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-167">The script removes registration and cloud pairing information from the server.</span></span>
5. <span data-ttu-id="e9f8b-168">Kaldırmak istediğiniz VMM sunucusundaki Bulutlar ile eşleştirilmiş bulut içeren herhangi bir VMM sunucularında temizleme betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-168">Run the cleanup script on any other VMM servers that contain clouds that are paired with clouds on the VMM server you want to remove.</span></span>
6. <span data-ttu-id="e9f8b-169">Yüklü sağlayıcı olan tüm diğer pasif VMM küme düğümlerine temizleme betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-169">Run the  cleanup script on any other passive VMM cluster nodes that have the Provider installed.</span></span>
7. <span data-ttu-id="e9f8b-170">Sağlayıcı VMM sunucusunda el ile kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-170">Uninstall the Provider manually on the VMM server.</span></span> <span data-ttu-id="e9f8b-171">Bir kümeniz varsa, tüm düğümlerden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-171">If you have a cluster, remove from all nodes.</span></span>
8. <span data-ttu-id="e9f8b-172">Azure'a çoğaltma, Microsoft Kurtarma Hizmetleri aracısını Hyper-V konakları silinen bulutlarındaki kaldırabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e9f8b-172">If you replicating to Azure, you can remove the Microsoft Recovery Services agent from Hyper-V hosts in the deleted clouds.</span></span>

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a><span data-ttu-id="e9f8b-173">Bir Hyper-V sitesi bir Hyper-V ana bilgisayar kaydı</span><span class="sxs-lookup"><span data-stu-id="e9f8b-173">Unregister a Hyper-V host in a Hyper-V Site</span></span>

<span data-ttu-id="e9f8b-174">VMM tarafından yönetilmeyen Hyper-V konaklarının, Hyper-V sitesi toplanır.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-174">Hyper-V hosts that aren't managed by VMM are gathered into a Hyper-V site.</span></span> <span data-ttu-id="e9f8b-175">Bir konak bir Hyper-V sitede aşağıdaki gibi kaldırın:</span><span class="sxs-lookup"><span data-stu-id="e9f8b-175">Remove a host in a Hyper-V site as follows:</span></span>

1. <span data-ttu-id="e9f8b-176">Hyper-V ana bilgisayarda yer alan VM'ler için çoğaltma devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-176">Disable replication for Hyper-V VMs located on the host.</span></span>
2. <span data-ttu-id="e9f8b-177">Hyper-V sitesi için ilkeler ilişkisini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-177">Disassociate policies for the Hyper-V site.</span></span> <span data-ttu-id="e9f8b-178">İçinde **Site Recovery altyapısı** > **için Hyper-V sitelerini** >  **çoğaltma ilkeleri**, ilişkili ilkeye çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-178">In **Site Recovery Infrastructure** > **For Hyper-V Sites** >  **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="e9f8b-179">Sitesi > **ilişkisini**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-179">Right-click the site > **Disassociate**.</span></span>
3. <span data-ttu-id="e9f8b-180">Hyper-V konakları silin.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-180">Delete Hyper-V hosts.</span></span> <span data-ttu-id="e9f8b-181">İçinde **Site Recovery altyapısı** > **için System Center VMM** > **Hyper-V konakları**, sunucuya sağ tıklayın > **silmek**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-181">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Hosts**, right-click the server > **Delete**.</span></span>
4. <span data-ttu-id="e9f8b-182">Tüm konaklar ondan temizlendikten sonra Hyper-V sitesi silin.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-182">Delete the Hyper-V site after all hosts have been removed from it.</span></span> <span data-ttu-id="e9f8b-183">İçinde **Site Recovery altyapısı** > **için System Center VMM** > **Hyper-V sitelerini**, siteye sağ tıklayın > **silmek**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-183">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Sites**, right-click the site > **Delete**.</span></span>
5. <span data-ttu-id="e9f8b-184">Aşağıdaki komut dosyasını kaldırdığınız her Hyper-V ana bilgisayarda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-184">Run the following script on each Hyper-V host that you removed.</span></span> <span data-ttu-id="e9f8b-185">Betik sunucu ayarları temizler ve kasadan kaydını siler.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-185">The script cleans up settings on the server, and unregisters it from the vault.</span></span>


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run the script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove the old Azure Site Recovery Provider related properties. Do you want to continue (Y/N) ?"
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
                "Stopping the Azure Site Recovery service..."
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

            # First retrive all the certificates to be deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete the certs
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



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a><span data-ttu-id="e9f8b-186">VMware VM veya fiziksel sunucu için koruma devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="e9f8b-186">Disable protection for a VMware VM or physical server</span></span>

1. <span data-ttu-id="e9f8b-187">İçinde **korunan öğeler** > **çoğaltılan öğeler**, makine adını sağ tıklayın > **silmek**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-187">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="e9f8b-188">İçinde **makineyi Kaldır**, aşağıdaki seçeneklerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="e9f8b-188">In **Remove Machine**, select one of these options:</span></span>
    - <span data-ttu-id="e9f8b-189">**(Önerilen) makine için korumayı devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-189">**Disable protection for the machine (recommended)**.</span></span> <span data-ttu-id="e9f8b-190">Makine çoğaltmasını durdurmak için bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-190">Use this option to stop replicating the machine.</span></span> <span data-ttu-id="e9f8b-191">Site Recovery ayarları otomatik olarak temizlenecek.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-191">Site Recovery settings will be cleaned up automatically.</span></span> <span data-ttu-id="e9f8b-192">Yalnızca aşağıdaki durumlarda bu seçenek görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="e9f8b-192">You will only see this option in the following circumstances:</span></span>
        - <span data-ttu-id="e9f8b-193">**VM birim yeniden boyutlandırılıyor**— sanal makine bir kritik duruma geçer bir birim yeniden boyutlandırdığınızda.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-193">**You've resized the VM volume**—When you resize a volume the virtual machine goes into a critical state.</span></span> <span data-ttu-id="e9f8b-194">Kurtarma noktalarının azure'da korurken devre dışı bırakır koruma için bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-194">Select this option to disables protection while retaining recovery points in Azure.</span></span> <span data-ttu-id="e9f8b-195">Makine için korumayı yeniden etkinleştirdiğinizde, yeniden boyutlandırılmış birim için verileri Azure'a aktarılır.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-195">When you enable protection for the machine again, the data for the resized volume will be transferred to Azure.</span></span>
        - <span data-ttu-id="e9f8b-196">**Bir yük devretme yakın zamanda çalıştırdıysanız**— ortamınızı test etmek için bir yük devretme çalıştırdıktan sonra şirket içi makineler yeniden korumaya başlamak için bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-196">**You've recently run a failover**—After you've run a failover to test your environment, select this option to start protecting on-premises machines again.</span></span> <span data-ttu-id="e9f8b-197">Her bir sanal makine devre dışı bırakır ve sonra bunlar için korumayı yeniden etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-197">It disables each virtual machine, and then you need to enable protection for them again.</span></span> <span data-ttu-id="e9f8b-198">Bu ayar makineyle devre dışı bırakma Azure içinde çoğaltma sanal makinesi etkilemez.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-198">Disabling the machine with this setting doesn't affect the replica virtual machine in Azure.</span></span> <span data-ttu-id="e9f8b-199">Mobility hizmetinin makineden kaldırmak yok.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-199">Don't uninstall the Mobility service from the machine.</span></span>
    - <span data-ttu-id="e9f8b-200">**Makineyi yönetmeyi Durdur**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-200">**Stop managing the machine**.</span></span> <span data-ttu-id="e9f8b-201">Bu seçeneği seçerseniz, makine yalnızca kasadan kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-201">If you select this option, the machine will only be removed from the vault.</span></span> <span data-ttu-id="e9f8b-202">Şirket içi makine için koruma ayarları etkilenmeyecek.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-202">On-premises protection settings for the machine won’t be affected.</span></span> <span data-ttu-id="e9f8b-203">Makine ayarlarını kaldırın ve makine Azure aboneliğinden kaldırmak için Mobility hizmeti kaldırarak ayarları temizlemek gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-203">To remove settings on the machine, and to remove the machine from the Azure subscription, you need to clean the settings by uninstalling the Mobility service.</span></span>

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a><span data-ttu-id="e9f8b-204">VMM bulutundaki Hyper-V VM için korumayı devre dışı</span><span class="sxs-lookup"><span data-stu-id="e9f8b-204">Disable protection for a Hyper-V VM in a VMM cloud</span></span>

1. <span data-ttu-id="e9f8b-205">İçinde **korunan öğeler** > **çoğaltılan öğeler**, makine adını sağ tıklayın > **silmek**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-205">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="e9f8b-206">İçinde **makineyi Kaldır**, aşağıdaki seçeneklerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="e9f8b-206">In **Remove Machine**, select one of these options:</span></span>

    - <span data-ttu-id="e9f8b-207">**(Önerilen) makine için korumayı devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-207">**Disable protection for the machine (recommended)**.</span></span> <span data-ttu-id="e9f8b-208">Makine çoğaltmasını durdurmak için bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-208">Use this option to stop replicating the machine.</span></span> <span data-ttu-id="e9f8b-209">Site Recovery ayarları otomatik olarak temizlenecek.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-209">Site Recovery settings will be cleaned up automatically.</span></span>
    - <span data-ttu-id="e9f8b-210">**Makineyi yönetmeyi Durdur**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-210">**Stop managing the machine**.</span></span> <span data-ttu-id="e9f8b-211">Bu seçeneği seçerseniz, makine yalnızca kasadan kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-211">If you select this option, the machine will only be removed from the vault.</span></span> <span data-ttu-id="e9f8b-212">Şirket içi makine için koruma ayarları etkilenmeyecek.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-212">On-premises protection settings for the machine won’t be affected.</span></span> <span data-ttu-id="e9f8b-213">Makine ayarlarını kaldırın ve makine Azure aboneliğinden kaldırmak için ayarları el ile temizlemek aşağıdaki yönergeleri kullanarak gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-213">To remove settings on the machine, and to remove the machine from the Azure subscription, you need to clean the settings up manually, using the instructions below.</span></span> <span data-ttu-id="e9f8b-214">Sanal makine ve sabit diskleri silmek için seçerseniz, bunlar hedef konumundan kaldırılması olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-214">Note that if you select to delete the virtual machine and its hard disks, they'll be removed from the target location.</span></span>

### <a name="clean-up-protection-settings---replication-to-a-secondary-vmm-site"></a><span data-ttu-id="e9f8b-215">Koruma ayarlarını - ikincil VMM sitesi için çoğaltma Temizle</span><span class="sxs-lookup"><span data-stu-id="e9f8b-215">Clean up protection settings - replication to a secondary VMM site</span></span>

<span data-ttu-id="e9f8b-216">Seçtiyseniz **makineyi yönetmeyi Durdur** ve birincil sanal makine ayarlarını temizlemek için birincil sunucuda bu komut dosyasını çalıştırın, ikincil bir siteye çoğaltmak.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-216">If you selected **Stop managing the machine** and you replicating to a secondary site, run this script on the primary server to clean up the settings for the primary virtual machine.</span></span> <span data-ttu-id="e9f8b-217">VMM konsolundan VMM PowerShell konsolunu açmak için PowerShell düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-217">In the VMM console click the PowerShell button to open the VMM PowerShell console.</span></span> <span data-ttu-id="e9f8b-218">SQLVM1, sanal makine adı ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-218">Replace SQLVM1 with the name of your virtual machine.</span></span>

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="e9f8b-219">İkincil VMM sunucusunda ikincil sanal makinenin ayarlarını temizlemek için bu komut dosyasını çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e9f8b-219">On the secondary VMM server run this script to clean up the settings for the secondary virtual machine:</span></span>

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. <span data-ttu-id="e9f8b-220">Böylece ikincil VM yeniden VMM konsolunda algılanan ikincil VMM sunucusunda Hyper-V ana bilgisayar sunucusunda sanal makineleri yenileyin.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-220">On the secondary VMM server, refresh the virtual machines on the Hyper-V host server, so that the secondary VM gets detected again in the VMM console.</span></span>
4. <span data-ttu-id="e9f8b-221">VMM sunucusundaki çoğaltma ayarlarını yukarıdaki adımları temizleyin.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-221">The above steps clear up the replication settings on the VMM server.</span></span> <span data-ttu-id="e9f8b-222">Sanal makine için çoğaltma durdurmak istiyorsanız, aşağıdaki komut dosyasını birincil ve ikincil VM'ler çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-222">If you want to stop replication for the virtual machine, run the following script oh the primary and secondary VMs.</span></span> <span data-ttu-id="e9f8b-223">SQLVM1, sanal makine adı ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-223">Replace SQLVM1 with the name of your virtual machine.</span></span>

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-to-azure"></a><span data-ttu-id="e9f8b-224">Koruma ayarlarını - Azure'a çoğaltma için temizleme</span><span class="sxs-lookup"><span data-stu-id="e9f8b-224">Clean up protection settings - replication to Azure</span></span>

1. <span data-ttu-id="e9f8b-225">Seçtiyseniz **makineyi yönetmeyi Durdur** ve kaynak VMM sunucusunda bu komut dosyası çalıştırma Azure PowerShell kullanarak VMM konsolundan çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-225">If you selected **Stop managing the machine** and you replicate to Azure, run this script on the source VMM server, using PowerShell from the VMM console.</span></span>
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="e9f8b-226">Yukarıdaki adımları VMM sunucusundaki çoğaltma ayarları temizleyin.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-226">The above steps clear the replication settings on the VMM server.</span></span> <span data-ttu-id="e9f8b-227">Hyper-V ana bilgisayar sunucusunda çalışan sanal makine için çoğaltma durdurmak için bu komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-227">To stop replication for the virtual machine running on the Hyper-V host server, run this script.</span></span> <span data-ttu-id="e9f8b-228">SQLVM1 adıyla bir sanal makine ve host01.contoso.com Hyper-V konak sunucusu adını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-228">Replace SQLVM1 with the name of your virtual machine, and host01.contoso.com with the name of the Hyper-V host server.</span></span>

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a><span data-ttu-id="e9f8b-229">Bir Hyper-V sitesindeki bir Hyper-V sanal makine için korumayı devre dışı bırakın</span><span class="sxs-lookup"><span data-stu-id="e9f8b-229">Disable protection for a Hyper-V VM in a Hyper-V Site</span></span>

<span data-ttu-id="e9f8b-230">Azure için Hyper-V sanal makinelerini çoğaltıyorsanız olmadan bir VMM sunucusu, bu yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-230">Use this procedure if you're replicating Hyper-V VMs to Azure without a VMM server.</span></span>

1. <span data-ttu-id="e9f8b-231">İçinde **korunan öğeler** > **çoğaltılan öğeler**, makine adını sağ tıklayın > **silmek**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-231">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="e9f8b-232">İçinde **makineyi Kaldır**, aşağıdaki seçenekleri seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e9f8b-232">In **Remove Machine**, you can select the following options:</span></span>

   - <span data-ttu-id="e9f8b-233">**(Önerilen) makine için korumayı devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-233">**Disable protection for the machine (recommended)**.</span></span> <span data-ttu-id="e9f8b-234">Makine çoğaltmasını durdurmak için bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-234">Use this option to stop replicating the machine.</span></span> <span data-ttu-id="e9f8b-235">Site Recovery ayarları otomatik olarak temizlenecek.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-235">Site Recovery settings will be cleaned up automatically.</span></span>
   - <span data-ttu-id="e9f8b-236">**Makineyi yönetmeyi Durdur**.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-236">**Stop managing the machine**.</span></span> <span data-ttu-id="e9f8b-237">Bu seçeneği seçerseniz, makine kasadan yalnızca kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-237">If you select this option the machine will only be removed from the vault.</span></span> <span data-ttu-id="e9f8b-238">Şirket içi makine için koruma ayarları etkilenmeyecek.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-238">On-premises protection settings for the machine won’t be affected.</span></span> <span data-ttu-id="e9f8b-239">Makine ayarlarını kaldırın ve sanal makineyi Azure aboneliğinden kaldırmak için ayarları el ile temizlenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-239">To remove settings on the machine, and to remove the virtual machine from the Azure subscription, you need to clean the settings up manually.</span></span> <span data-ttu-id="e9f8b-240">Sanal makine ve sabit diskleri silmek için seçerseniz hedef konumundan kaldırılacak.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-240">If you select to delete the virtual machine and its hard disks they will be removed from the target location.</span></span>
3. <span data-ttu-id="e9f8b-241">Seçtiyseniz **makineyi yönetmeyi Durdur**, sanal makine için çoğaltmayı kaldırmak için kaynak Hyper-V ana bilgisayarı sunucusunda, bu komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-241">If you selected **Stop managing the machine**, run this script on the source Hyper-V host server, to remove replication for the virtual machine.</span></span> <span data-ttu-id="e9f8b-242">SQLVM1, sanal makine adı ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e9f8b-242">Replace SQLVM1 with the name of your virtual machine.</span></span>

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
