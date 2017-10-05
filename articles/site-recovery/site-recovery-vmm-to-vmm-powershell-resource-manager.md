---
title: "İkincil bir siteye PowerShell (Azure Resource Manager) ile VMM Hyper-V Vm'lerini çoğaltma | Microsoft Docs"
description: "Çoğaltma, yük devretme ve VMM bulutlarındaki Hyper-V sanal makineleri Kurtarma (Resource Manager) PowerShell kullanarak bir ikincil VMM sitesi olarak düzenlemek için Azure Site Recovery dağıtmayı açıklar"
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
ms.openlocfilehash: 5a6e00877b0a2b139d5322f610c1901ad76a710f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-a-secondary-vmm-site-using-powershell-resource-manager"></a><span data-ttu-id="7b2fa-103">VMM bulutlarındaki Hyper-V sanal makinelerini (Resource Manager) PowerShell kullanarak bir ikincil VMM siteye çoğaltma</span><span class="sxs-lookup"><span data-stu-id="7b2fa-103">Replicate Hyper-V virtual machines in VMM clouds to a secondary VMM site using PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7b2fa-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7b2fa-104">Azure Portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="7b2fa-105">Klasik Portal</span><span class="sxs-lookup"><span data-stu-id="7b2fa-105">Classic Portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="7b2fa-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7b2fa-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="7b2fa-107">Azure Site Recovery'ye hoş geldiniz!</span><span class="sxs-lookup"><span data-stu-id="7b2fa-107">Welcome to Azure Site Recovery!</span></span> <span data-ttu-id="7b2fa-108">Şirket içi Hyper-V sanal makineleri çoğaltmak istiyorsanız bu makalede ikincil bir siteyi System Center Virtual Machine Manager (VMM) bulutlarında yönetilen kullanın.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-108">Use this article if you want to replicate on-premises Hyper-V  virtual machines managed in System Center Virtual Machine Manager (VMM) clouds to a secondary site.</span></span>

<span data-ttu-id="7b2fa-109">Bu makalede PowerShell System Center VMM bulutlarında ikincil site için System Center VMM bulutlarındaki Hyper-V sanal makineleri çoğaltmak için Azure Site Recovery ayarladığınızda, yapmanız gereken ortak görevleri otomatik hale getirmek için nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-109">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to System Center VMM clouds in secondary site.</span></span>

<span data-ttu-id="7b2fa-110">Makaleyi senaryonun önkoşulları içerir ve gösterir</span><span class="sxs-lookup"><span data-stu-id="7b2fa-110">The article includes prerequisites for the scenario, and shows you</span></span>

* <span data-ttu-id="7b2fa-111">Bir kurtarma Hizmetleri kasasını nasıl kurulur</span><span class="sxs-lookup"><span data-stu-id="7b2fa-111">How to set up a Recovery Services Vault</span></span>
* <span data-ttu-id="7b2fa-112">Kaynak VMM Sunucu ve hedef VMM sunucusunda Azure Site kurtarma Sağlayıcısı'nı yükleyin</span><span class="sxs-lookup"><span data-stu-id="7b2fa-112">Install the Azure Site Recovery Provider on the source VMM server and the target VMM server</span></span>
* <span data-ttu-id="7b2fa-113">VMM sunucuları kasaya kaydetmek</span><span class="sxs-lookup"><span data-stu-id="7b2fa-113">Register the VMM server(s) in the vault</span></span>
* <span data-ttu-id="7b2fa-114">Çoğaltma İlkesi VMM bulutu için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-114">Configure replication policy for the VMM Cloud.</span></span> <span data-ttu-id="7b2fa-115">Tüm korumalı sanal makineler için İlkesi'ndeki çoğaltma ayarları uygulanır</span><span class="sxs-lookup"><span data-stu-id="7b2fa-115">The replication settings in the policy will be applied to all protected virtual machines</span></span>
* <span data-ttu-id="7b2fa-116">Sanal makineler için korumayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-116">Enable protection for the virtual machines.</span></span>
* <span data-ttu-id="7b2fa-117">Ayrı ayrı veya her şeyin beklendiği gibi çalıştığından emin olmak için kurtarma planının bir parçası olarak sanal makineleri yük devretme sınamasını.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-117">Test the failover of VMs individually or as part of a recovery plan to make sure everything is working as expected.</span></span>
* <span data-ttu-id="7b2fa-118">Planlanmış veya planlanmamış bir yük devretme VM'lerin ayrı ayrı veya her şeyin beklendiği gibi çalıştığından emin olmak için kurtarma planının bir parçası olarak gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-118">Perform a planned or an unplanned failover of VMs individually or as part of a recovery plan to make sure everything is working as expected.</span></span>

<span data-ttu-id="7b2fa-119">Bu senaryoyu oluşturan ayarlama sorunlarını alıyorsanız, üzerinde sorularınızı [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="7b2fa-119">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="7b2fa-120">Azure, kaynak oluşturmak ve bu kaynaklarla çalışmak için iki [dağıtım modeli](../azure-resource-manager/resource-manager-deployment-model.md) kullanır: Azure Resource Manager ve klasik model.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-120">Azure has two different [deployment models](../azure-resource-manager/resource-manager-deployment-model.md) for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="7b2fa-121">Ayrıca Azure iki portala sahiptir: Klasik dağıtım modelini destekleyen klasik Azure portalı ve her iki dağıtım modeline de destek sağlayan Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-121">Azure also has two portals – the Azure classic portal that supports the classic deployment model, and the Azure portal with support for both deployment models.</span></span> <span data-ttu-id="7b2fa-122">Bu makalede Resource Manager dağıtım modeli anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-122">This article covers the Resource Manager deployment model.</span></span>
>
>

## <a name="on-premises-prerequisites"></a><span data-ttu-id="7b2fa-123">Şirket içi önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7b2fa-123">On-premises prerequisites</span></span>
<span data-ttu-id="7b2fa-124">İşte şirket içi birincil ve ikincil siteler bu senaryoyu dağıtmak için gerekenler:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-124">Here's what you'll need in the primary and secondary on-premises sites to deploy this scenario:</span></span>

| <span data-ttu-id="7b2fa-125">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="7b2fa-125">**Prerequisites**</span></span> | <span data-ttu-id="7b2fa-126">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="7b2fa-126">**Details**</span></span> |
| --- | --- |
| <span data-ttu-id="7b2fa-127">**VMM**</span><span class="sxs-lookup"><span data-stu-id="7b2fa-127">**VMM**</span></span> |<span data-ttu-id="7b2fa-128">VMM sunucusu birincil sitedeki ve ikincil sitedeki VMM sunucusu dağıtmak öneririz.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-128">We recommend you deploy a VMM server in the primary site and a VMM server in the secondary site.</span></span><br/><br/> <span data-ttu-id="7b2fa-129">Ayrıca [tek bir VMM sunucusundaki Bulutlar arasında çoğaltma](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span><span class="sxs-lookup"><span data-stu-id="7b2fa-129">You can also [replicate between clouds on a single VMM server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span></span> <span data-ttu-id="7b2fa-130">Bunu yapmak için VMM sunucusunda yapılandırılan en az iki bulut gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-130">To do this you'll need at least two clouds configured on the VMM server.</span></span><br/><br/> <span data-ttu-id="7b2fa-131">VMM sunucuları çalışıyor. en son güncelleştirmeleri içeren System Center 2012 SP1.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-131">VMM servers should be running at least System Center 2012 SP1 with the latest updates.</span></span><br/><br/> <span data-ttu-id="7b2fa-132">Her bir VMM sunucusunun tek sahip olmalı veya daha fazla bulut yapılandırılmış ve tüm Bulutlar Hyper-V Kapasite profili kümesine sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-132">Each VMM server must have at one or more clouds configured and all clouds must have the Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="7b2fa-133">Bulut bir veya daha fazla VMM ana bilgisayar grubu içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-133">Clouds must contain one or more VMM host groups.</span></span><br/><br/><span data-ttu-id="7b2fa-134">VMM bulutlarını ayarlama hakkında daha fazla bilgi [VMM bulut doku](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), ve [izlenecek yol: System Center 2012 SP1 VMM içeren özel bulut oluşturma](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b2fa-134">Learn more about setting up VMM clouds in [Configuring the VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), and [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span></span><br/><br/> <span data-ttu-id="7b2fa-135">VMM sunucuları Internet erişimine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-135">VMM servers should have internet access.</span></span> |
| <span data-ttu-id="7b2fa-136">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="7b2fa-136">**Hyper-V**</span></span> |<span data-ttu-id="7b2fa-137">Hyper-V sunucuları çalışıyor olmalıdır en az Windows Server 2012 Hyper-V rolüne sahip ve en son güncelleştirmelerin yüklü olması.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-137">Hyper-V servers must be running at least Windows Server 2012 with the Hyper-V role and have the latest updates installed.</span></span><br/><br/> <span data-ttu-id="7b2fa-138">Bir Hyper-V sunucusunun bir veya daha fazla VM içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-138">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="7b2fa-139">Hyper-V ana bilgisayar sunucularının birincil ve ikincil VMM bulutlarında konak gruplarındaki bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-139">Hyper-V host servers should be located in host groups in the primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="7b2fa-140">Windows Server 2012 R2'de bir kümede Hyper-V çalıştırıyorsanız, yüklemelisiniz [2961977 güncelleştir](https://support.microsoft.com/kb/2961977)</span><span class="sxs-lookup"><span data-stu-id="7b2fa-140">If you're running Hyper-V in a cluster on Windows Server 2012 R2 you should install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="7b2fa-141">Bir kümede küme aracısının Windows Server 2012 Not üzerinde Hyper-V çalıştırıyorsanız, bir statik IP adresi tabanlı kümeniz varsa otomatik olarak oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-141">If you're running Hyper-V in a cluster on Windows Server 2012 note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="7b2fa-142">Küme aracısını sizin yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-142">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="7b2fa-143">[Daha fazla bilgi](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b2fa-143">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span> |
| <span data-ttu-id="7b2fa-144">**Sağlayıcı**</span><span class="sxs-lookup"><span data-stu-id="7b2fa-144">**Provider**</span></span> |<span data-ttu-id="7b2fa-145">Site Recovery dağıtımı sırasında VMM sunucularına Azure Site kurtarma Sağlayıcısı'nı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-145">During Site Recovery deployment you install the Azure Site Recovery Provider on VMM servers.</span></span> <span data-ttu-id="7b2fa-146">Sağlayıcı, çoğaltmayı düzenlemek için HTTPS 443 üzerinden Site Recovery ile iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-146">The Provider communicates with Site Recovery over HTTPS 443 to orchestrate replication.</span></span> <span data-ttu-id="7b2fa-147">Veri çoğaltma, LAN veya bir VPN bağlantısı üzerinden birincil ve ikincil Hyper-V sunucuları arasında oluşur.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-147">Data replication occurs between the primary and secondary Hyper-V servers over the LAN or a VPN connection.</span></span><br/><br/> <span data-ttu-id="7b2fa-148">VMM sunucusunda çalışan sağlayıcı bu URL'leri erişmesi: *. hypervrecoverymanager.windowsazure.com; *. accesscontrol.windows.net; *. backup.windowsazure.com; *. blob.core.windows.net; *. store.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-148">The Provider running on the VMM server needs access to these URLs: *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.</span></span><br/><br/> <span data-ttu-id="7b2fa-149">Ayrıca VMM sunucularına gelen güvenlik duvarı iletişimi izin [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653) ve HTTPS (443) protokolüne izin verin.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-149">In addition allow firewall communication from the VMM servers to the [Azure datacenter IP ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and allow the HTTPS (443) protocol.</span></span> |

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="7b2fa-150">Ağ eşlemesi önkoşulları</span><span class="sxs-lookup"><span data-stu-id="7b2fa-150">Network mapping prerequisites</span></span>
<span data-ttu-id="7b2fa-151">Ağ eşlemesi eşlemeleri VMM VM ağ için birincil ve ikincil VMM sunucularındaki arasında:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-151">Network mapping maps between VMM VM networks on the primary and secondary VMM servers to:</span></span>

* <span data-ttu-id="7b2fa-152">En iyi şekilde çoğaltılan VM'ler üzerinde ikincil Hyper-V konakları yük devretme sonrasında yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-152">Optimally place replica VMs on secondary Hyper-V hosts after failover.</span></span>
* <span data-ttu-id="7b2fa-153">Çoğaltılan VM'ler için uygun VM ağları bağlayın.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-153">Connect replica VMs to appropriate VM networks.</span></span>
* <span data-ttu-id="7b2fa-154">Ağ eşlemesi çoğaltma sanal makineleri yük devretme sonrasında herhangi bir ağa bağlanmayacaktır yapılandırmazsanız.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-154">If you don't configure network mapping replica VMs won't be connected to any network after failover.</span></span>
* <span data-ttu-id="7b2fa-155">Ağ kurmak istiyorsanız, Site kurtarması sırasında eşleme gerekenler dağıtım burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-155">If you want to set up network mapping during Site Recovery deployment here's what you'll need:</span></span>

  * <span data-ttu-id="7b2fa-156">Kaynak Hyper-V ana bilgisayar sunucusundaki VM'lerin bir VMM VM ağına bağlı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-156">Make sure that VMs on the source Hyper-V host server are connected to a VMM VM network.</span></span> <span data-ttu-id="7b2fa-157">Bu ağın, bulutla ilişkilendirilen mantıksal bir ağ ile bağlantılı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-157">That network should be linked to a logical network that is associated with the cloud.</span></span>
  * <span data-ttu-id="7b2fa-158">Kurtarma için kullanacağınız ikincil bulut yapılandırılmış karşılık gelen VM ağı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-158">Verify that the secondary cloud that you'll use for recovery has a corresponding VM network configured.</span></span> <span data-ttu-id="7b2fa-159">Bir VM ağı ikincil bulutla ilişkilendirilen bir mantıksal ağ bağlantılı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-159">That VM network should be linked to a logical network that's associated with the secondary cloud.</span></span>

<span data-ttu-id="7b2fa-160">VMM ağları yapılandırma hakkında daha fazla bilgi makaleleri aşağıda</span><span class="sxs-lookup"><span data-stu-id="7b2fa-160">Learn more about configuring VMM networks in the below articles</span></span>

* [<span data-ttu-id="7b2fa-161">VMM'de Mantıksal ağlar yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7b2fa-161">How to configure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="7b2fa-162">VMM'de VM ağları ve ağ geçitlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7b2fa-162">How to configure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)

<span data-ttu-id="7b2fa-163">Ağ eşlemesinin nasıl çalıştığı hakkında [daha fazla bilgi edinin](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping).</span><span class="sxs-lookup"><span data-stu-id="7b2fa-163">[Learn more](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) about how network mapping works.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="7b2fa-164">PowerShell önkoşulları</span><span class="sxs-lookup"><span data-stu-id="7b2fa-164">PowerShell prerequisites</span></span>
<span data-ttu-id="7b2fa-165">Azure PowerShell davranmaya hazır olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-165">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="7b2fa-166">PowerShell zaten kullanıyorsanız, 0.8.10 sürümüne yükseltme veya üstü gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-166">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="7b2fa-167">PowerShell ayarlama hakkında daha fazla bilgi için bkz: [Azure PowerShell'i yükleme ve yapılandırma için kılavuz](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="7b2fa-167">For information about setting up PowerShell, see the [Guide to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="7b2fa-168">Ayarlama ve PowerShell yapılandırılmış sonra tüm kullanılabilir cmdlet'leri hizmeti görüntüleyebilirsiniz [burada](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7b2fa-168">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="7b2fa-169">Parametre değerleri, girişleri ve çıkışları genellikle Azure PowerShell'de işlenme gibi cmdlet'leri kullanın yardımcı olabilecek ipuçları hakkında bilgi edinmek için bkz [Azure cmdlet'leri kullanmaya başlama Kılavuzu](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="7b2fa-169">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see the [Guide to get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="7b2fa-170">1. adım: Abonelik ayarlama</span><span class="sxs-lookup"><span data-stu-id="7b2fa-170">Step 1: Set the subscription</span></span>
1. <span data-ttu-id="7b2fa-171">Azure powershell'den Azure hesabınızda oturum açın: aşağıdaki cmdlet'leri kullanarak</span><span class="sxs-lookup"><span data-stu-id="7b2fa-171">From Azure powershell, login to your Azure account: using the following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="7b2fa-172">Aboneliklerinizi listesini alın.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-172">Get a list of your subscriptions.</span></span> <span data-ttu-id="7b2fa-173">Bu da subscriptionIDs her abonelik için listeler.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-173">This will also list the subscriptionIDs for each of the subscriptions.</span></span> <span data-ttu-id="7b2fa-174">Kurtarma Hizmetleri kasası oluşturmak istediğiniz aboneliği Subscriptionıd unutmayın</span><span class="sxs-lookup"><span data-stu-id="7b2fa-174">Note down the subscriptionID of the subscription in which you wish to create the recovery services vault</span></span>    

        Get-AzureRmSubscription
3. <span data-ttu-id="7b2fa-175">Kurtarma Hizmetleri kasası abonelik kimliği söz tarafından oluşturulacak olan abonelik ayarlayın</span><span class="sxs-lookup"><span data-stu-id="7b2fa-175">Set the subscription in which the recovery services vault is to be created by mentioning the subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="7b2fa-176">2. Adım: Bir Kurtarma Hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="7b2fa-176">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="7b2fa-177">Zaten yoksa, bir Azure Resource Manager kaynak grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="7b2fa-177">Create an Azure Resource Manager resource group if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="7b2fa-178">Yeni bir kurtarma Hizmetleri kasası oluşturun ve oluşturulan ASR kasası nesnesi (daha sonra kullanılacak) bir değişkene kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-178">Create a new Recovery Services vault and save the created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="7b2fa-179">Get-AzureRMRecoveryServicesVault cmdlet'ini kullanarak ASR kasası nesne post oluşturma de alabilirsiniz:-</span><span class="sxs-lookup"><span data-stu-id="7b2fa-179">You can also retrieve the ASR vault object post creation using the Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="7b2fa-180">3. adım: Kurtarma Hizmetleri kasası bağlamını ayarlayın</span><span class="sxs-lookup"><span data-stu-id="7b2fa-180">Step 3: Set the Recovery Services Vault context</span></span>
1. <span data-ttu-id="7b2fa-181">Önceden oluşturulmuş bir kasası varsa çalıştırmak kasa için komutu aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-181">If you have a vault already created, run the below command to get the vault.</span></span>

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. <span data-ttu-id="7b2fa-182">Çalıştırarak kasası bağlamını ayarlayın aşağıda komutu.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-182">Set the vault context by running the below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="7b2fa-183">4. adım: Azure Site kurtarma Sağlayıcısı'nı yükleme</span><span class="sxs-lookup"><span data-stu-id="7b2fa-183">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="7b2fa-184">VMM makinesinde aşağıdaki komutu çalıştırarak bir dizin oluşturun:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-184">On the VMM machine, create a directory by running the following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="7b2fa-185">Aşağıdaki komutu çalıştırarak indirilen sağlayıcısını kullanarak dosyaları ayıklayın</span><span class="sxs-lookup"><span data-stu-id="7b2fa-185">Extract the files using the downloaded provider by running the following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="7b2fa-186">Aşağıdaki komutları kullanarak sağlayıcısını yükleyin:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-186">Install the provider using the following commands:</span></span>

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

   <span data-ttu-id="7b2fa-187">Yüklemesinin tamamlanması için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-187">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="7b2fa-188">Sunucu aşağıdaki komutu kullanarak kasaya kaydedin:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-188">Register the server in the vault using the following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a><span data-ttu-id="7b2fa-189">5. adım: Oluşturun ve bir çoğaltma ilkesi ilişkilendirin</span><span class="sxs-lookup"><span data-stu-id="7b2fa-189">Step 5: Create and associate a replication policy</span></span>
1. <span data-ttu-id="7b2fa-190">Aşağıdaki komutu çalıştırarak bir 2012 R2 Hyper-V çoğaltma ilkesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-190">Create a Hyper-V 2012 R2 replication policy by running the following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify the number of hours to retain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify the frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify the port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > <span data-ttu-id="7b2fa-191">VMM bulut (Hyper-V önkoşullarını belirtildiği gibi) Windows Server'ın farklı sürümlerini çalıştıran Hyper-V konakları içerebilir, ancak çoğaltma ilkesi OS belirli sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-191">The VMM cloud can contain Hyper-V hosts running different versions of Windows Server (as mentioned in the Hyper-V prerequisites), but the replication policy is OS version specific.</span></span> <span data-ttu-id="7b2fa-192">Farklı işletim sistemi sürümlerinde çalışan farklı ana bilgisayarınız varsa, her tür işletim sistemi sürümü için ayrı çoğaltma ilkeleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-192">If you have different hosts running on different operating system versions, then create separate replication policies for each type of OS version.</span></span> <span data-ttu-id="7b2fa-193">İçin örn: Windows sunucuları 2012 ve Windows Server 2012 R2'de üç çalışan beş ana bilgisayarınız varsa, iki oluşturmak çoğaltma ilkeleri – bir işletim sistemi sürümleri her tür.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-193">For eg: If you have five hosts running on Windows Servers 2012 and three on Windows Server 2012 R2, create two replication polices – one for each type of operating system versions.</span></span>

1. <span data-ttu-id="7b2fa-194">Birincil koruma kapsayıcısı (birincil VMM Bulutu) ve kurtarma koruma kapsayıcısı (Kurtarma VMM bulut) aşağıdaki komutları çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-194">Get the primary protection container (primary VMM Cloud) and recovery protection container (recovery VMM Cloud) by running the following commands:</span></span>

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. <span data-ttu-id="7b2fa-195">İlke kolay adını kullanarak 1. adımda oluşturduğunuz İlke Al</span><span class="sxs-lookup"><span data-stu-id="7b2fa-195">Retrieve the policy you created in step 1 using the friendly name of the policy</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="7b2fa-196">Koruma kapsayıcısı (VMM Bulutu) ilişkilendirme çoğaltma ilkesiyle başlatın:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-196">Start the association of the protection container (VMM Cloud) with the replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. <span data-ttu-id="7b2fa-197">İlke ilişkilendirme işin tamamlanması için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-197">Wait for the policy association job to complete.</span></span> <span data-ttu-id="7b2fa-198">Aşağıdaki PowerShell parçacığını kullanarak iş tamamlanıp tamamlanmadığını kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-198">You can check if the job has completed using the following PowerShell snippet.</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   <span data-ttu-id="7b2fa-199">İş işlemeyi bitirdikten sonra aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-199">After the job has finished processing, run the following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="7b2fa-200">İşlemin tamamlanması denetlemek için adımları [etkinliğini izleme](#monitor).</span><span class="sxs-lookup"><span data-stu-id="7b2fa-200">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-6-configure-network-mapping"></a><span data-ttu-id="7b2fa-201">6. adım: ağ eşlemesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7b2fa-201">Step 6: Configure network mapping</span></span>
1. <span data-ttu-id="7b2fa-202">İlk komut sunucuları için geçerli Azure Site Recovery kasası alır.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-202">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="7b2fa-203">Komut Microsoft Azure Site Recovery sunucuları $Servers dizi değişkeninde depolar.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-203">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="7b2fa-204">Kaynak VMM sunucusunu ve hedef VMM sunucusu için aşağıdaki komutları site kurtarma ağ alın.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-204">The below commands get the site recovery network for the source VMM server and the target VMM server.</span></span>

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > <span data-ttu-id="7b2fa-205">Kaynak VMM sunucusunu ilk veya ikinci bir sunucuları dizisindeki olabilir.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-205">The source VMM server can be the first one or the second one in the servers array.</span></span> <span data-ttu-id="7b2fa-206">VMM sunucularının adlarını denetleyin ve ağlar uygun şekilde Al</span><span class="sxs-lookup"><span data-stu-id="7b2fa-206">Check the names of the VMM servers and get the networks appropriately</span></span>


1. <span data-ttu-id="7b2fa-207">Son cmdlet birincil ağ ve kurtarma ağ arasında bir eşleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-207">The final cmdlet creates a mapping between the primary network and the recovery network.</span></span> <span data-ttu-id="7b2fa-208">Cmdlet birincil ağ $PrimaryNetworks ve $RecoveryNetworks ilk öğe olarak kurtarma ağ ilk öğe olarak belirtir.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-208">The cmdlet specifies the primary network as the first element of $PrimaryNetworks and the recovery network as the first element of $RecoveryNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a><span data-ttu-id="7b2fa-209">7. adım: depolama eşlemesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7b2fa-209">Step 7: Configure storage mapping</span></span>
1. <span data-ttu-id="7b2fa-210">Aşağıdaki komutunu depolama sınıflandırmaları $storageclassifications değişkeni içine listesini alır.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-210">The below command gets the list of storage classifications into $storageclassifications variable.</span></span>

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. <span data-ttu-id="7b2fa-211">Aşağıdaki komutları $SourceClassificaion değişkeni ve hedef sınıflandırma $TargetClassification değişkeni içine içine kaynak sınıflandırma alır.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-211">The below commands get the source classification into $SourceClassificaion variable and target classification into $TargetClassification variable.</span></span>

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > <span data-ttu-id="7b2fa-212">Kaynak ve hedef sınıflandırmaları dizideki her öğe olabilir.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-212">The source and target classifications can be any element in the array.</span></span> <span data-ttu-id="7b2fa-213">Çıkışına bakın kaynak ve hedef sınıflandırmaları $storageclassifications dizisindeki dizini bulmak için komutu aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-213">Refer to the output of the below command to figure the index of source and target classifications in $storageclassifications array.</span></span>

    > <span data-ttu-id="7b2fa-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object - FriendlyName özelliği, kimliği | Tablo Biçimlendir</span><span class="sxs-lookup"><span data-stu-id="7b2fa-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span></span>


1. <span data-ttu-id="7b2fa-215">Aşağıda cmdlet'ini kaynak sınıflandırma ve hedef sınıflandırma arasında bir eşleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-215">The below cmdlet creates a mapping between the source classification and the target classification.</span></span>

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a><span data-ttu-id="7b2fa-216">8. Adım: Sanal makinelere yönelik korumayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="7b2fa-216">Step 8: Enable protection for virtual machines</span></span>
<span data-ttu-id="7b2fa-217">Sunucular, Bulutlar ve ağlar doğru şekilde yapılandırıldıktan sonra buluttaki sanal makineler için korumayı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-217">After the servers, clouds and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span>

1. <span data-ttu-id="7b2fa-218">Korumayı etkinleştirmek için koruma kapsayıcısı almak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-218">To enable protection, run the following command to get the protection container:</span></span>

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. <span data-ttu-id="7b2fa-219">Korunan varlık (VM), aşağıdaki komutu çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-219">Get the protection entity (VM) by running the following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. <span data-ttu-id="7b2fa-220">Sanal makine için çoğaltmayı aşağıdaki komutu çalıştırarak etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-220">Enable replication for the VM by running the following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a><span data-ttu-id="7b2fa-221">Dağıtımınızı test edin</span><span class="sxs-lookup"><span data-stu-id="7b2fa-221">Test your deployment</span></span>
<span data-ttu-id="7b2fa-222">Dağıtımınızı test etmek için bir yük devretme sınaması için tek bir sanal makine çalıştırmak veya birden çok sanal makine içeren bir kurtarma planı oluşturmak ve bir yük devretme sınaması için plan çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-222">To test your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for the plan.</span></span> <span data-ttu-id="7b2fa-223">Yük devretme testi, yük devretme işleminizi ve kurtarma mekanizmanızı yalıtılmış bir ortamda benzetimli olarak gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-223">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span>

> [!NOTE]
> <span data-ttu-id="7b2fa-224">Azure Portalı'nda, uygulamanız için bir kurtarma planı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-224">You can create a recovery plan for your application in Azure portal.</span></span>
>
>

<span data-ttu-id="7b2fa-225">İşlemin tamamlanması denetlemek için adımları [etkinliğini izleme](#monitor).</span><span class="sxs-lookup"><span data-stu-id="7b2fa-225">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="7b2fa-226">Yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7b2fa-226">Run a test failover</span></span>
1. <span data-ttu-id="7b2fa-227">Çalıştırma Vm'leriniz için yük devretme sınamasını istediğiniz VM ağı almak için cmdlet'leri aşağıda.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-227">Run the below cmdlets to get the VM network to which you want to test failover your VMs to.</span></span>

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. <span data-ttu-id="7b2fa-228">Aşağıdakileri yaparak bir VM bir sınama yük devretmesi gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-228">Perform a test failover of a VM by doing the following:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. <span data-ttu-id="7b2fa-229">Aşağıdakileri yaparak bir kurtarma planı bir sınama yük devretmesi gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-229">Perform a test failover of a recovery plan by doing the following:</span></span>

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a><span data-ttu-id="7b2fa-230">Planlı yük devretmeyi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7b2fa-230">Run a planned failover</span></span>
1. <span data-ttu-id="7b2fa-231">Aşağıdakileri yaparak bir VM planlanmış bir yük devretme gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-231">Perform a planned failover of a VM by doing the following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. <span data-ttu-id="7b2fa-232">Aşağıdakileri yaparak bir kurtarma planı planlanan bir yük devretme gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-232">Perform a planned failover of a recovery plan by doing the following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="7b2fa-233">Planlanmamış bir yük devretmeyi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7b2fa-233">Run an unplanned failover</span></span>
1. <span data-ttu-id="7b2fa-234">Aşağıdakileri yaparak bir VM planlanmamış yük devretme gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-234">Perform an unplanned failover of a VM by doing the following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

<span data-ttu-id="7b2fa-235">2., aşağıdakileri yaparak bir kurtarma planı planlanmamış yük devretme gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7b2fa-235">2.Perform an unplanned failover of a recovery plan by doing the following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <span data-ttu-id="7b2fa-236"><a name=monitor></a>Etkinliğini izleme</span><span class="sxs-lookup"><span data-stu-id="7b2fa-236"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="7b2fa-237">Etkinliğini izlemek için aşağıdaki komutları kullanın.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-237">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="7b2fa-238">Bitirmek işleme işleri arasında beklemek zorunda unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-238">Note that you have to wait in between jobs for the processing to finish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="7b2fa-239">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7b2fa-239">Next steps</span></span>
<span data-ttu-id="7b2fa-240">[Daha fazla bilgi](/powershell/module/azurerm.recoveryservices.backup/#recovery) Azure Site Recovery ile Azure Resource Manager PowerShell cmdlet'leri hakkında.</span><span class="sxs-lookup"><span data-stu-id="7b2fa-240">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
