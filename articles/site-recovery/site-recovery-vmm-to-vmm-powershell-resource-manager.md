---
title: aaaReplicate PowerShell (Azure Resource Manager) ile Hyper-V sanal makineleri VMM tooa ikincil sitedeki | Microsoft Docs
description: "Nasıl toodeploy Azure Site Recovery tooorchestrate çoğaltma, yük devretme ve kurtarma Hyper-V vm'lerinde VMM Bulutu tooa (Resource Manager) PowerShell kullanarak ikincil VMM sitesi açıklar"
services: site-recovery
documentationcenter: 
author: sujaytalasila
manager: rochakm
editor: raynew
ms.assetid: 9d38e9c3-217c-4e44-830c-575e9a4141f2
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: a769dcc68d66c18b9dc47539071f4d0e0f1db70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-powershell-resource-manager"></a><span data-ttu-id="111ad-103">Hyper-V sanal makineleri (Resource Manager) PowerShell kullanarak VMM Bulutları tooa ikincil VMM sitesi Çoğalt</span><span class="sxs-lookup"><span data-stu-id="111ad-103">Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site using PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="111ad-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="111ad-104">Azure Portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="111ad-105">Klasik Portal</span><span class="sxs-lookup"><span data-stu-id="111ad-105">Classic Portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="111ad-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="111ad-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="111ad-107">Site Recovery tooAzure Hoş Geldiniz!</span><span class="sxs-lookup"><span data-stu-id="111ad-107">Welcome tooAzure Site Recovery!</span></span> <span data-ttu-id="111ad-108">Tooreplicate içi System Center Virtual Machine Manager (VMM) Bulutlar tooa ikincil sitede yönetilen Hyper-V sanal makinelerin istiyorsanız, bu makaleyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="111ad-108">Use this article if you want tooreplicate on-premises Hyper-V  virtual machines managed in System Center Virtual Machine Manager (VMM) clouds tooa secondary site.</span></span>

<span data-ttu-id="111ad-109">Bu makalede, System Center VMM Bulutları tooSystem Center VMM bulutlarında ikincil sitede Azure Site Recovery tooreplicate Hyper-V sanal makineleri ayarladığınızda nasıl toouse PowerShell tooautomate ortak görevleri tooperform ihtiyacınız gösterir.</span><span class="sxs-lookup"><span data-stu-id="111ad-109">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooSystem Center VMM clouds in secondary site.</span></span>

<span data-ttu-id="111ad-110">Merhaba makale hello senaryonun önkoşulları içerir ve gösterir</span><span class="sxs-lookup"><span data-stu-id="111ad-110">hello article includes prerequisites for hello scenario, and shows you</span></span>

* <span data-ttu-id="111ad-111">Nasıl tooset bir kurtarma Hizmetleri kasası ayarlama</span><span class="sxs-lookup"><span data-stu-id="111ad-111">How tooset up a Recovery Services Vault</span></span>
* <span data-ttu-id="111ad-112">Merhaba kaynak VMM sunucusunda ve hello hedef VMM sunucusunda Hello Azure Site Recovery sağlayıcısı yükleme</span><span class="sxs-lookup"><span data-stu-id="111ad-112">Install hello Azure Site Recovery Provider on hello source VMM server and hello target VMM server</span></span>
* <span data-ttu-id="111ad-113">Merhaba VMM sunucuları hello kasaya kaydetmek</span><span class="sxs-lookup"><span data-stu-id="111ad-113">Register hello VMM server(s) in hello vault</span></span>
* <span data-ttu-id="111ad-114">Merhaba VMM bulutu için çoğaltma ilkesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="111ad-114">Configure replication policy for hello VMM Cloud.</span></span> <span data-ttu-id="111ad-115">hello İlkesi'nde Hello çoğaltma ayarları uygulanan tooall korumalı sanal makineler olacaktır</span><span class="sxs-lookup"><span data-stu-id="111ad-115">hello replication settings in hello policy will be applied tooall protected virtual machines</span></span>
* <span data-ttu-id="111ad-116">Merhaba sanal makineler için korumayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="111ad-116">Enable protection for hello virtual machines.</span></span>
* <span data-ttu-id="111ad-117">VM'nin hello yük devretme testi ayrı ayrı veya bir kurtarmanın parçası olarak toomake her şeyin beklendiği gibi çalıştığından emin planlayın.</span><span class="sxs-lookup"><span data-stu-id="111ad-117">Test hello failover of VMs individually or as part of a recovery plan toomake sure everything is working as expected.</span></span>
* <span data-ttu-id="111ad-118">Planlanmış veya planlanmamış bir yük devretme VM'lerin ayrı ayrı veya bir kurtarma planı toomake her şeyin beklendiği gibi çalıştığından emin bir parçası olarak gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="111ad-118">Perform a planned or an unplanned failover of VMs individually or as part of a recovery plan toomake sure everything is working as expected.</span></span>

<span data-ttu-id="111ad-119">Bu senaryoyu oluşturan ayarlama sorunlarını alıyorsanız, üzerinde hello sorularınızı [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="111ad-119">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="111ad-120">Azure, kaynak oluşturmak ve bu kaynaklarla çalışmak için iki [dağıtım modeli](../azure-resource-manager/resource-manager-deployment-model.md) kullanır: Azure Resource Manager ve klasik model.</span><span class="sxs-lookup"><span data-stu-id="111ad-120">Azure has two different [deployment models](../azure-resource-manager/resource-manager-deployment-model.md) for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="111ad-121">Ayrıca Azure iki portala – hello Klasik dağıtım modelini destekleyen Klasik Azure portalı hello ve her iki dağıtım modeline de destek Azure portal hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="111ad-121">Azure also has two portals – hello Azure classic portal that supports hello classic deployment model, and hello Azure portal with support for both deployment models.</span></span> <span data-ttu-id="111ad-122">Bu makalede, hello Resource Manager dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="111ad-122">This article covers hello Resource Manager deployment model.</span></span>
>
>

## <a name="on-premises-prerequisites"></a><span data-ttu-id="111ad-123">Şirket içi önkoşullar</span><span class="sxs-lookup"><span data-stu-id="111ad-123">On-premises prerequisites</span></span>
<span data-ttu-id="111ad-124">İşte hello birincil gerekenler ve bu senaryo ikincil şirket içi siteler toodeploy:</span><span class="sxs-lookup"><span data-stu-id="111ad-124">Here's what you'll need in hello primary and secondary on-premises sites toodeploy this scenario:</span></span>

| <span data-ttu-id="111ad-125">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="111ad-125">**Prerequisites**</span></span> | <span data-ttu-id="111ad-126">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="111ad-126">**Details**</span></span> |
| --- | --- |
| <span data-ttu-id="111ad-127">**VMM**</span><span class="sxs-lookup"><span data-stu-id="111ad-127">**VMM**</span></span> |<span data-ttu-id="111ad-128">Bir VMM sunucusunun hello birincil sitede ve hello ikincil sitedeki VMM sunucusu dağıtmak öneririz.</span><span class="sxs-lookup"><span data-stu-id="111ad-128">We recommend you deploy a VMM server in hello primary site and a VMM server in hello secondary site.</span></span><br/><br/> <span data-ttu-id="111ad-129">Ayrıca [tek bir VMM sunucusundaki Bulutlar arasında çoğaltma](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span><span class="sxs-lookup"><span data-stu-id="111ad-129">You can also [replicate between clouds on a single VMM server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span></span> <span data-ttu-id="111ad-130">toodo bu hello VMM sunucusunda yapılandırılmış en az iki bulut gerekir.</span><span class="sxs-lookup"><span data-stu-id="111ad-130">toodo this you'll need at least two clouds configured on hello VMM server.</span></span><br/><br/> <span data-ttu-id="111ad-131">VMM sunucuları çalışıyor. en az hello en son güncelleştirmeleri içeren System Center 2012 SP1.</span><span class="sxs-lookup"><span data-stu-id="111ad-131">VMM servers should be running at least System Center 2012 SP1 with hello latest updates.</span></span><br/><br/> <span data-ttu-id="111ad-132">Her bir VMM sunucusunun tek sahip olmalı veya daha fazla bulut yapılandırılmış ve tüm Bulutlar hello Hyper-V Kapasite profili kümesine sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="111ad-132">Each VMM server must have at one or more clouds configured and all clouds must have hello Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="111ad-133">Bulut bir veya daha fazla VMM ana bilgisayar grubu içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="111ad-133">Clouds must contain one or more VMM host groups.</span></span><br/><br/><span data-ttu-id="111ad-134">VMM bulutlarını ayarlama hakkında daha fazla bilgi [yapılandırma hello VMM bulut doku](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), ve [izlenecek yol: System Center 2012 SP1 VMM içeren özel bulut oluşturma](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span><span class="sxs-lookup"><span data-stu-id="111ad-134">Learn more about setting up VMM clouds in [Configuring hello VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), and [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span></span><br/><br/> <span data-ttu-id="111ad-135">VMM sunucuları Internet erişimine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="111ad-135">VMM servers should have internet access.</span></span> |
| <span data-ttu-id="111ad-136">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="111ad-136">**Hyper-V**</span></span> |<span data-ttu-id="111ad-137">Hyper-V sunucuları çalışıyor olmalıdır en az Windows Server 2012 hello Hyper-V rolüne sahip ve hello son güncelleştirmelerin yüklü olması.</span><span class="sxs-lookup"><span data-stu-id="111ad-137">Hyper-V servers must be running at least Windows Server 2012 with hello Hyper-V role and have hello latest updates installed.</span></span><br/><br/> <span data-ttu-id="111ad-138">Bir Hyper-V sunucusunun bir veya daha fazla VM içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="111ad-138">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="111ad-139">Hyper-V ana bilgisayar sunucuları konak grupları hello birincil ve ikincil VMM bulutlarında yer.</span><span class="sxs-lookup"><span data-stu-id="111ad-139">Hyper-V host servers should be located in host groups in hello primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="111ad-140">Windows Server 2012 R2'de bir kümede Hyper-V çalıştırıyorsanız, yüklemelisiniz [2961977 güncelleştir](https://support.microsoft.com/kb/2961977)</span><span class="sxs-lookup"><span data-stu-id="111ad-140">If you're running Hyper-V in a cluster on Windows Server 2012 R2 you should install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="111ad-141">Bir kümede küme aracısının Windows Server 2012 Not üzerinde Hyper-V çalıştırıyorsanız, bir statik IP adresi tabanlı kümeniz varsa otomatik olarak oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="111ad-141">If you're running Hyper-V in a cluster on Windows Server 2012 note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="111ad-142">El ile tooconfigure hello küme Aracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="111ad-142">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="111ad-143">[Daha fazla bilgi edinin](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span><span class="sxs-lookup"><span data-stu-id="111ad-143">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span> |
| <span data-ttu-id="111ad-144">**Sağlayıcı**</span><span class="sxs-lookup"><span data-stu-id="111ad-144">**Provider**</span></span> |<span data-ttu-id="111ad-145">Site Recovery dağıtımı sırasında VMM sunucularına Azure Site Recovery sağlayıcısı hello yükleyin.</span><span class="sxs-lookup"><span data-stu-id="111ad-145">During Site Recovery deployment you install hello Azure Site Recovery Provider on VMM servers.</span></span> <span data-ttu-id="111ad-146">Merhaba sağlayıcısı HTTPS 443 tooorchestrate çoğaltma Site Recovery ile iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="111ad-146">hello Provider communicates with Site Recovery over HTTPS 443 tooorchestrate replication.</span></span> <span data-ttu-id="111ad-147">Veri çoğaltma hello LAN üzerinden hello birincil ve ikincil Hyper-V sunucuları veya bir VPN bağlantısı arasında oluşur.</span><span class="sxs-lookup"><span data-stu-id="111ad-147">Data replication occurs between hello primary and secondary Hyper-V servers over hello LAN or a VPN connection.</span></span><br/><br/> <span data-ttu-id="111ad-148">Merhaba hello VMM sunucusunda çalışan sağlayıcı toothese URL'leri erişimi gerektirir: *. hypervrecoverymanager.windowsazure.com; *. accesscontrol.windows.net; *. backup.windowsazure.com; *. blob.core.windows.net; *. store.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="111ad-148">hello Provider running on hello VMM server needs access toothese URLs: *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.</span></span><br/><br/> <span data-ttu-id="111ad-149">Ayrıca hello VMM sunucuları toohello gelen güvenlik duvarı iletişimi izin [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653) ve hello HTTPS (443) protokolüne izin verin.</span><span class="sxs-lookup"><span data-stu-id="111ad-149">In addition allow firewall communication from hello VMM servers toohello [Azure datacenter IP ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and allow hello HTTPS (443) protocol.</span></span> |

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="111ad-150">Ağ eşlemesi önkoşulları</span><span class="sxs-lookup"><span data-stu-id="111ad-150">Network mapping prerequisites</span></span>
<span data-ttu-id="111ad-151">Ağ eşlemesi eşlemeleri hello birincil ve ikincil VMM sunucuları için VMM VM ağlarında arasında:</span><span class="sxs-lookup"><span data-stu-id="111ad-151">Network mapping maps between VMM VM networks on hello primary and secondary VMM servers to:</span></span>

* <span data-ttu-id="111ad-152">En iyi şekilde çoğaltılan VM'ler üzerinde ikincil Hyper-V konakları yük devretme sonrasında yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="111ad-152">Optimally place replica VMs on secondary Hyper-V hosts after failover.</span></span>
* <span data-ttu-id="111ad-153">Çoğaltma sanal makineleri tooappropriate VM ağları bağlayın.</span><span class="sxs-lookup"><span data-stu-id="111ad-153">Connect replica VMs tooappropriate VM networks.</span></span>
* <span data-ttu-id="111ad-154">Ağ yapılandırmazsanız çoğaltma eşleme VM'ler bağlı tooany Ağ Yük devretme sonrasında olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="111ad-154">If you don't configure network mapping replica VMs won't be connected tooany network after failover.</span></span>
* <span data-ttu-id="111ad-155">Ağ tooset istiyorsanız Site kurtarması sırasında eşleme gerekenler dağıtım burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="111ad-155">If you want tooset up network mapping during Site Recovery deployment here's what you'll need:</span></span>

  * <span data-ttu-id="111ad-156">Merhaba kaynağı Hyper-V konak sunucusu üzerinde sanal makineleri bağlı tooa VMM VM ağ olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="111ad-156">Make sure that VMs on hello source Hyper-V host server are connected tooa VMM VM network.</span></span> <span data-ttu-id="111ad-157">Bu ağ hello Bulutu ile ilişkili mantıksal ağ bağlantılı tooa olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="111ad-157">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
  * <span data-ttu-id="111ad-158">Kurtarma için kullanacağınız hello ikincil bulut yapılandırılmış karşılık gelen VM ağı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="111ad-158">Verify that hello secondary cloud that you'll use for recovery has a corresponding VM network configured.</span></span> <span data-ttu-id="111ad-159">Bir VM ağı hello ikincil bulutla ilişkilendirilen mantıksal ağ bağlantılı tooa olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="111ad-159">That VM network should be linked tooa logical network that's associated with hello secondary cloud.</span></span>

<span data-ttu-id="111ad-160">Merhaba makaleleri aşağıda VMM ağları yapılandırma hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="111ad-160">Learn more about configuring VMM networks in hello below articles</span></span>

* [<span data-ttu-id="111ad-161">Nasıl tooconfigure vmm'de Mantıksal ağlar</span><span class="sxs-lookup"><span data-stu-id="111ad-161">How tooconfigure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="111ad-162">Nasıl tooconfigure VM ağları ve ağ geçitlerini vmm'de</span><span class="sxs-lookup"><span data-stu-id="111ad-162">How tooconfigure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)

<span data-ttu-id="111ad-163">Ağ eşlemesinin nasıl çalıştığı hakkında [daha fazla bilgi edinin](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping).</span><span class="sxs-lookup"><span data-stu-id="111ad-163">[Learn more](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) about how network mapping works.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="111ad-164">PowerShell önkoşulları</span><span class="sxs-lookup"><span data-stu-id="111ad-164">PowerShell prerequisites</span></span>
<span data-ttu-id="111ad-165">Azure PowerShell hazır toogo olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="111ad-165">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="111ad-166">PowerShell zaten kullanıyorsanız, tooupgrade tooversion 0.8.10 gerekir ya da daha sonra.</span><span class="sxs-lookup"><span data-stu-id="111ad-166">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="111ad-167">Merhaba PowerShell ayarlama hakkında daha fazla bilgi için bkz [Kılavuzu tooinstall ve Azure PowerShell yapılandırma](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="111ad-167">For information about setting up PowerShell, see hello [Guide tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="111ad-168">Ayarlama ve PowerShell yapılandırılmış sonra tüm hello hizmeti için kullanılabilir cmdlet'leri hello görüntüleyebilirsiniz [burada](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="111ad-168">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="111ad-169">parametre değerleri, girişleri ve çıkışları genellikle Azure PowerShell'de işlenme gibi hello cmdlet'leri kullanmanıza yardımcı olabilecek ipuçları hakkında toolearn bkz hello [tooget Azure cmdlet'leri ile Başlarken Kılavuzu](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="111ad-169">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see hello [Guide tooget Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="111ad-170">1. adım: hello abonelik ayarlama</span><span class="sxs-lookup"><span data-stu-id="111ad-170">Step 1: Set hello subscription</span></span>
1. <span data-ttu-id="111ad-171">Azure powershell, oturum açma tooyour Azure hesabı üzerinden: hello aşağıdaki cmdlet'leri kullanarak</span><span class="sxs-lookup"><span data-stu-id="111ad-171">From Azure powershell, login tooyour Azure account: using hello following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="111ad-172">Aboneliklerinizi listesini alın.</span><span class="sxs-lookup"><span data-stu-id="111ad-172">Get a list of your subscriptions.</span></span> <span data-ttu-id="111ad-173">Bu da hello subscriptionIDs her hello abonelikler için listeler.</span><span class="sxs-lookup"><span data-stu-id="111ad-173">This will also list hello subscriptionIDs for each of hello subscriptions.</span></span> <span data-ttu-id="111ad-174">Toocreate hello kurtarma Hizmetleri kasası istediğiniz hello aboneliğin Hello Subscriptionıd unutmayın</span><span class="sxs-lookup"><span data-stu-id="111ad-174">Note down hello subscriptionID of hello subscription in which you wish toocreate hello recovery services vault</span></span>    

        Get-AzureRmSubscription
3. <span data-ttu-id="111ad-175">Hangi hello kurtarma Hizmetleri kasası hello abonelik kimliği söz tarafından oluşturulan toobe olan hello abonelik ayarlayın</span><span class="sxs-lookup"><span data-stu-id="111ad-175">Set hello subscription in which hello recovery services vault is toobe created by mentioning hello subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="111ad-176">2. Adım: Bir Kurtarma Hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="111ad-176">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="111ad-177">Zaten yoksa, bir Azure Resource Manager kaynak grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="111ad-177">Create an Azure Resource Manager resource group if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="111ad-178">Yeni bir kurtarma Hizmetleri kasası oluşturun ve ASR kasası nesne (daha sonra kullanılacak) bir değişkende oluşturulan hello kaydedin.</span><span class="sxs-lookup"><span data-stu-id="111ad-178">Create a new Recovery Services vault and save hello created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="111ad-179">Merhaba ASR kasası nesne post oluşturma hello Get-AzureRMRecoveryServicesVault cmdlet'ini kullanarak elde edebilirsiniz:-</span><span class="sxs-lookup"><span data-stu-id="111ad-179">You can also retrieve hello ASR vault object post creation using hello Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="111ad-180">3. adım: hello kurtarma Hizmetleri kasası bağlamını ayarlayın</span><span class="sxs-lookup"><span data-stu-id="111ad-180">Step 3: Set hello Recovery Services Vault context</span></span>
1. <span data-ttu-id="111ad-181">Önceden oluşturulmuş bir kasa varsa, komut tooget hello kasası altındaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="111ad-181">If you have a vault already created, run hello below command tooget hello vault.</span></span>

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. <span data-ttu-id="111ad-182">Hello aşağıdaki komutu çalıştırarak Hello kasası bağlamını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="111ad-182">Set hello vault context by running hello below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="111ad-183">Adım 4: hello Azure Site Recovery sağlayıcısı yükleme</span><span class="sxs-lookup"><span data-stu-id="111ad-183">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="111ad-184">Merhaba VMM makinede hello aşağıdaki komutu çalıştırarak bir dizin oluşturun:</span><span class="sxs-lookup"><span data-stu-id="111ad-184">On hello VMM machine, create a directory by running hello following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="111ad-185">Merhaba aşağıdaki komutu çalıştırarak indirilen hello sağlayıcısını kullanarak hello dosyaları ayıklayın</span><span class="sxs-lookup"><span data-stu-id="111ad-185">Extract hello files using hello downloaded provider by running hello following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="111ad-186">Merhaba Sağlayıcı komutları aşağıdaki hello kullanarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="111ad-186">Install hello provider using hello following commands:</span></span>

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   <span data-ttu-id="111ad-187">Merhaba yükleme toofinish bekleyin.</span><span class="sxs-lookup"><span data-stu-id="111ad-187">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="111ad-188">Hello sunucu komutu aşağıdaki hello kullanarak hello kasasına kaydedin:</span><span class="sxs-lookup"><span data-stu-id="111ad-188">Register hello server in hello vault using hello following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a><span data-ttu-id="111ad-189">5. adım: Oluşturun ve bir çoğaltma ilkesi ilişkilendirin</span><span class="sxs-lookup"><span data-stu-id="111ad-189">Step 5: Create and associate a replication policy</span></span>
1. <span data-ttu-id="111ad-190">Merhaba aşağıdaki komutu çalıştırarak bir 2012 R2 Hyper-V çoğaltma ilkesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="111ad-190">Create a Hyper-V 2012 R2 replication policy by running hello following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify hello number of hours tooretain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify hello frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify hello port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > <span data-ttu-id="111ad-191">Merhaba VMM bulut (Merhaba Hyper-V önkoşullarını belirtildiği gibi) Windows Server'ın farklı sürümlerini çalıştıran Hyper-V konakları içerebilir, ancak hello çoğaltma ilkedir belirli işletim sistemi sürümü.</span><span class="sxs-lookup"><span data-stu-id="111ad-191">hello VMM cloud can contain Hyper-V hosts running different versions of Windows Server (as mentioned in hello Hyper-V prerequisites), but hello replication policy is OS version specific.</span></span> <span data-ttu-id="111ad-192">Farklı işletim sistemi sürümlerinde çalışan farklı ana bilgisayarınız varsa, her tür işletim sistemi sürümü için ayrı çoğaltma ilkeleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="111ad-192">If you have different hosts running on different operating system versions, then create separate replication policies for each type of OS version.</span></span> <span data-ttu-id="111ad-193">İçin örn: Windows sunucuları 2012 ve Windows Server 2012 R2'de üç çalışan beş ana bilgisayarınız varsa, iki oluşturmak çoğaltma ilkeleri – bir işletim sistemi sürümleri her tür.</span><span class="sxs-lookup"><span data-stu-id="111ad-193">For eg: If you have five hosts running on Windows Servers 2012 and three on Windows Server 2012 R2, create two replication polices – one for each type of operating system versions.</span></span>

1. <span data-ttu-id="111ad-194">Hello birincil koruma kapsayıcısı (birincil VMM Bulutu) ve kurtarma koruma kapsayıcısı (Kurtarma VMM bulut) hello aşağıdaki komutları çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="111ad-194">Get hello primary protection container (primary VMM Cloud) and recovery protection container (recovery VMM Cloud) by running hello following commands:</span></span>

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. <span data-ttu-id="111ad-195">1. adım kullanarak oluşturduğunuz hello İlkesi almak hello İlkesi hello kolay adı</span><span class="sxs-lookup"><span data-stu-id="111ad-195">Retrieve hello policy you created in step 1 using hello friendly name of hello policy</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="111ad-196">Merhaba koruma kapsayıcısı (VMM Bulutu) Hello ilişkilendirmesini hello çoğaltma ilkesiyle başlatın:</span><span class="sxs-lookup"><span data-stu-id="111ad-196">Start hello association of hello protection container (VMM Cloud) with hello replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. <span data-ttu-id="111ad-197">Hello İlkesi ilişkilendirme iş toocomplete bekleyin.</span><span class="sxs-lookup"><span data-stu-id="111ad-197">Wait for hello policy association job toocomplete.</span></span> <span data-ttu-id="111ad-198">Merhaba iş PowerShell parçacığını aşağıdaki hello kullanarak tamamlandı kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="111ad-198">You can check if hello job has completed using hello following PowerShell snippet.</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   <span data-ttu-id="111ad-199">Hello iş işlemeyi bitirdikten sonra hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="111ad-199">After hello job has finished processing, run hello following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="111ad-200">Merhaba işleminin toocheck hello tamamlanması izleyin hello adımlarda [etkinliğini izleme](#monitor).</span><span class="sxs-lookup"><span data-stu-id="111ad-200">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-6-configure-network-mapping"></a><span data-ttu-id="111ad-201">6. adım: ağ eşlemesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="111ad-201">Step 6: Configure network mapping</span></span>
1. <span data-ttu-id="111ad-202">Merhaba ilk komut sunucuları için geçerli Azure Site Recovery kasası hello alır.</span><span class="sxs-lookup"><span data-stu-id="111ad-202">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="111ad-203">Merhaba komut hello Microsoft Azure Site Recovery sunucuları hello $Servers dizi değişkeninde depolar.</span><span class="sxs-lookup"><span data-stu-id="111ad-203">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="111ad-204">Merhaba komutları aşağıda hello site kurtarma ağ hello kaynak VMM sunucusunu ve hello hedef VMM sunucusu için alın.</span><span class="sxs-lookup"><span data-stu-id="111ad-204">hello below commands get hello site recovery network for hello source VMM server and hello target VMM server.</span></span>

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > <span data-ttu-id="111ad-205">Merhaba kaynak VMM sunucusunu olması hello birinci veya hello ikinci bir söz hello sunucuları dizi.</span><span class="sxs-lookup"><span data-stu-id="111ad-205">hello source VMM server can be hello first one or hello second one in hello servers array.</span></span> <span data-ttu-id="111ad-206">Hello VMM sunucularının Hello adlarını denetleyin ve hello ağları uygun şekilde Al</span><span class="sxs-lookup"><span data-stu-id="111ad-206">Check hello names of hello VMM servers and get hello networks appropriately</span></span>


1. <span data-ttu-id="111ad-207">Merhaba son cmdlet'i hello birincil ağ ve hello kurtarma ağ arasında bir eşleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="111ad-207">hello final cmdlet creates a mapping between hello primary network and hello recovery network.</span></span> <span data-ttu-id="111ad-208">Merhaba cmdlet hello birincil ağ kurtarma ağ $PrimaryNetworks ve hello $RecoveryNetworks hello ilk öğesi olarak hello ilk öğesi olarak belirtir.</span><span class="sxs-lookup"><span data-stu-id="111ad-208">hello cmdlet specifies hello primary network as hello first element of $PrimaryNetworks and hello recovery network as hello first element of $RecoveryNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a><span data-ttu-id="111ad-209">7. adım: depolama eşlemesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="111ad-209">Step 7: Configure storage mapping</span></span>
1. <span data-ttu-id="111ad-210">Merhaba komutu aşağıda depolama sınıflandırmaları $storageclassifications değişkeni içine hello listesini alır.</span><span class="sxs-lookup"><span data-stu-id="111ad-210">hello below command gets hello list of storage classifications into $storageclassifications variable.</span></span>

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. <span data-ttu-id="111ad-211">Merhaba komutları aşağıda hello kaynak sınıflandırma $SourceClassificaion değişkeni içine ve hedef sınıflandırma $TargetClassification değişkeni içine alın.</span><span class="sxs-lookup"><span data-stu-id="111ad-211">hello below commands get hello source classification into $SourceClassificaion variable and target classification into $TargetClassification variable.</span></span>

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > <span data-ttu-id="111ad-212">Merhaba kaynak ve hedef sınıflandırmaları hello dizisinde herhangi bir öğe olabilir.</span><span class="sxs-lookup"><span data-stu-id="111ad-212">hello source and target classifications can be any element in hello array.</span></span> <span data-ttu-id="111ad-213">Kaynak ve hedef sınıflandırmaları $storageclassifications dizisindeki komutu toofigure hello dizini altındaki hello toohello çıktısını bakın.</span><span class="sxs-lookup"><span data-stu-id="111ad-213">Refer toohello output of hello below command toofigure hello index of source and target classifications in $storageclassifications array.</span></span>

    > <span data-ttu-id="111ad-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object - FriendlyName özelliği, kimliği | Tablo Biçimlendir</span><span class="sxs-lookup"><span data-stu-id="111ad-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span></span>


1. <span data-ttu-id="111ad-215">Aşağıdaki cmdlet'i Hello hello kaynak sınıflandırma ve hello Hedef Sınıflandırma arasında bir eşleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="111ad-215">hello below cmdlet creates a mapping between hello source classification and hello target classification.</span></span>

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a><span data-ttu-id="111ad-216">8. Adım: Sanal makinelere yönelik korumayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="111ad-216">Step 8: Enable protection for virtual machines</span></span>
<span data-ttu-id="111ad-217">Merhaba sunucular, Bulutlar ve ağlar doğru şekilde yapılandırıldıktan sonra hello bulutta sanal makineler için korumayı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="111ad-217">After hello servers, clouds and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span>

1. <span data-ttu-id="111ad-218">tooenable koruma, çalıştırma hello aşağıdaki tooget hello koruma kapsayıcısı komutu:</span><span class="sxs-lookup"><span data-stu-id="111ad-218">tooenable protection, run hello following command tooget hello protection container:</span></span>

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. <span data-ttu-id="111ad-219">Merhaba koruma varlık (VM) hello aşağıdaki komutu çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="111ad-219">Get hello protection entity (VM) by running hello following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. <span data-ttu-id="111ad-220">Merhaba VM için çoğaltma hello aşağıdaki komutu çalıştırarak etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="111ad-220">Enable replication for hello VM by running hello following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a><span data-ttu-id="111ad-221">Dağıtımınızı test edin</span><span class="sxs-lookup"><span data-stu-id="111ad-221">Test your deployment</span></span>
<span data-ttu-id="111ad-222">tootest bir yük devretme sınaması için tek bir sanal makine çalıştırmak veya birden çok sanal makine içeren ve bir yük devretme testi hello için bir kurtarma planı oluşturun, dağıtımınızı planlayın.</span><span class="sxs-lookup"><span data-stu-id="111ad-222">tootest your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for hello plan.</span></span> <span data-ttu-id="111ad-223">Yük devretme testi, yük devretme işleminizi ve kurtarma mekanizmanızı yalıtılmış bir ortamda benzetimli olarak gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="111ad-223">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span>

> [!NOTE]
> <span data-ttu-id="111ad-224">Azure Portalı'nda, uygulamanız için bir kurtarma planı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="111ad-224">You can create a recovery plan for your application in Azure portal.</span></span>
>
>

<span data-ttu-id="111ad-225">Merhaba işleminin toocheck hello tamamlanması izleyin hello adımlarda [etkinliğini izleme](#monitor).</span><span class="sxs-lookup"><span data-stu-id="111ad-225">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="111ad-226">Yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="111ad-226">Run a test failover</span></span>
1. <span data-ttu-id="111ad-227">Vm'leriniz için tootest yük devretme istediğiniz cmdlet'leri tooget hello VM ağ toowhich aşağıda Hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="111ad-227">Run hello below cmdlets tooget hello VM network toowhich you want tootest failover your VMs to.</span></span>

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. <span data-ttu-id="111ad-228">VM bir sınama yük devretmesi hello aşağıdakileri yaparak gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="111ad-228">Perform a test failover of a VM by doing hello following:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. <span data-ttu-id="111ad-229">Bir kurtarma planı bir sınama yük devretmesi hello aşağıdakileri yaparak gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="111ad-229">Perform a test failover of a recovery plan by doing hello following:</span></span>

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a><span data-ttu-id="111ad-230">Planlı yük devretmeyi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="111ad-230">Run a planned failover</span></span>
1. <span data-ttu-id="111ad-231">Merhaba aşağıdakileri yaparak bir VM planlanmış bir yük devretme gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="111ad-231">Perform a planned failover of a VM by doing hello following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. <span data-ttu-id="111ad-232">Merhaba aşağıdakileri yaparak bir kurtarma planı planlanan bir yük devretme gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="111ad-232">Perform a planned failover of a recovery plan by doing hello following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="111ad-233">Planlanmamış bir yük devretmeyi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="111ad-233">Run an unplanned failover</span></span>
1. <span data-ttu-id="111ad-234">Merhaba aşağıdakileri yaparak bir VM planlanmamış yük devretme gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="111ad-234">Perform an unplanned failover of a VM by doing hello following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

<span data-ttu-id="111ad-235">2. hello aşağıdakileri yaparak bir kurtarma planı planlanmamış yük devretme gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="111ad-235">2.Perform an unplanned failover of a recovery plan by doing hello following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <span data-ttu-id="111ad-236"><a name=monitor></a>Etkinliğini izleme</span><span class="sxs-lookup"><span data-stu-id="111ad-236"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="111ad-237">Aşağıdaki komutları toomonitor hello etkinlik hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="111ad-237">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="111ad-238">Merhaba işleme toofinish işleri arasında toowait gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="111ad-238">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="111ad-239">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="111ad-239">Next steps</span></span>
<span data-ttu-id="111ad-240">[Daha fazla bilgi](/powershell/module/azurerm.recoveryservices.backup/#recovery) Azure Site Recovery ile Azure Resource Manager PowerShell cmdlet'leri hakkında.</span><span class="sxs-lookup"><span data-stu-id="111ad-240">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
