---
title: aaaSQL Server FCI - Azure sanal makineleri | Microsoft Docs
description: "Bu makalede açıklanır toocreate SQL Server Yük devretme kümesi örneği nasıl Azure sanal makinelerde."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a><span data-ttu-id="e6397-103">SQL Server Yük devretme kümesi örneği üzerinde Azure sanal makineleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e6397-103">Configure SQL Server Failover Cluster Instance on Azure Virtual Machines</span></span>

<span data-ttu-id="e6397-104">Bu makalede, nasıl toocreate bir SQL Server Yük devretme küme açıklanmaktadır Resource Manager modelinde Azure sanal makinelerde örneği (FCI).</span><span class="sxs-lookup"><span data-stu-id="e6397-104">This article explains how toocreate a SQL Server Failover Cluster Instance (FCI) on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="e6397-105">Bu çözümü kullanan [depolama alanları doğrudan Windows Server 2016 Datacenter edition \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) hello düğümleri (Azure VM) arasındaki hello depolama (veri diskleri) eşitleyen bir yazılım tabanlı sanal SAN olarak bir Windows Küme.</span><span class="sxs-lookup"><span data-stu-id="e6397-105">This solution uses [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) as a software-based virtual SAN that synchronizes hello storage (data disks) between hello nodes (Azure VMs) in a Windows Cluster.</span></span> <span data-ttu-id="e6397-106">S2D, Windows Server 2016'da yeni bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="e6397-106">S2D is new in Windows Server 2016.</span></span>

<span data-ttu-id="e6397-107">Merhaba Aşağıdaki diyagramda hello eksiksiz bir çözüm Azure sanal makinelerde gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="e6397-107">hello following diagram shows hello complete solution on Azure virtual machines:</span></span>

![Kullanılabilirlik grubu](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

<span data-ttu-id="e6397-109">Önceki diyagramda gösterildiği hello:</span><span class="sxs-lookup"><span data-stu-id="e6397-109">hello preceding diagram shows:</span></span>

- <span data-ttu-id="e6397-110">İki Azure sanal makinelerinde Windows Yük devretme kümesi.</span><span class="sxs-lookup"><span data-stu-id="e6397-110">Two Azure virtual machines in a Windows Failover Cluster.</span></span> <span data-ttu-id="e6397-111">Bir sanal makine bir yük devretme kümesinde olduğunda da adlandırılır bir *küme düğümü*, veya *düğümleri*.</span><span class="sxs-lookup"><span data-stu-id="e6397-111">When a virtual machine is in a failover cluster it is also called a *cluster node*, or *nodes*.</span></span>
- <span data-ttu-id="e6397-112">Her sanal makinenin iki veya daha fazla veri diski var.</span><span class="sxs-lookup"><span data-stu-id="e6397-112">Each virtual machine has two or more data disks.</span></span>
- <span data-ttu-id="e6397-113">S2D hello verileri diskteki hello verileri eşitler ve bir depolama havuzu olarak eşitlenen hello depolama sunar.</span><span class="sxs-lookup"><span data-stu-id="e6397-113">S2D synchronizes hello data on hello data disk and presents hello synchronized storage as a storage pool.</span></span>
- <span data-ttu-id="e6397-114">Merhaba depolama havuzu, bir Küme Paylaşılan birimi (CSV) toohello yük devretme kümesi sunar.</span><span class="sxs-lookup"><span data-stu-id="e6397-114">hello storage pool presents a cluster shared volume (CSV) toohello failover cluster.</span></span>
- <span data-ttu-id="e6397-115">Merhaba SQL Server FCI küme rolünü hello CSV hello veri sürücüleri için kullanır.</span><span class="sxs-lookup"><span data-stu-id="e6397-115">hello SQL Server FCI cluster role uses hello CSV for hello data drives.</span></span>
- <span data-ttu-id="e6397-116">Azure yük dengeleyici toohold hello için bir IP adresi hello SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="e6397-116">An Azure load balancer toohold hello IP address for hello SQL Server FCI.</span></span>
- <span data-ttu-id="e6397-117">Bir Azure kullanılabilirlik kümesi tüm hello kaynakları tutar.</span><span class="sxs-lookup"><span data-stu-id="e6397-117">An Azure availability set holds all hello resources.</span></span>

   >[!NOTE]
   ><span data-ttu-id="e6397-118">Tüm Azure hello şemada kaynaklardır hello olan aynı kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="e6397-118">All Azure resources are in hello diagram are in hello same resource group.</span></span>

<span data-ttu-id="e6397-119">S2D hakkında daha fazla ayrıntı için bkz: [depolama alanları doğrudan Windows Server 2016 Datacenter edition \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span><span class="sxs-lookup"><span data-stu-id="e6397-119">For details about S2D, see [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span></span>

<span data-ttu-id="e6397-120">S2D mimarileri - yakınsanmış ve hiper yakınsanmış iki türlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="e6397-120">S2D supports two types of architectures - converged and hyper-converged.</span></span> <span data-ttu-id="e6397-121">Merhaba bu belgedeki hiper yakınsanmış bir mimaridir.</span><span class="sxs-lookup"><span data-stu-id="e6397-121">hello architecture in this document is hyper-converged.</span></span> <span data-ttu-id="e6397-122">Bir altyapı hiper yakınsanmış yerler hello depolama aynı sunucuları, konak hello kümelenmiş uygulama hello.</span><span class="sxs-lookup"><span data-stu-id="e6397-122">A hyper-converged infrastructure places hello storage on hello same servers that host hello clustered application.</span></span> <span data-ttu-id="e6397-123">Bu mimaride hello depolama her SQL Server FCI düğümde ' dir.</span><span class="sxs-lookup"><span data-stu-id="e6397-123">In this architecture, hello storage is on each SQL Server FCI node.</span></span>

### <a name="example-azure-template"></a><span data-ttu-id="e6397-124">Örnek Azure şablonu</span><span class="sxs-lookup"><span data-stu-id="e6397-124">Example Azure template</span></span>

<span data-ttu-id="e6397-125">Bir şablondan Azure'da hello tüm çözüm oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6397-125">You can create hello entire solution in Azure from a template.</span></span> <span data-ttu-id="e6397-126">Şablon örneği hello GitHub kullanılabilir [Azure hızlı başlangıç şablonlarını](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span><span class="sxs-lookup"><span data-stu-id="e6397-126">An example of a template is available in hello GitHub [Azure Quickstart Templates](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span></span> <span data-ttu-id="e6397-127">Bu örnekte değil tasarlanmış veya belirli bir iş yükü için test.</span><span class="sxs-lookup"><span data-stu-id="e6397-127">This example is not designed or tested for any specific workload.</span></span> <span data-ttu-id="e6397-128">Merhaba şablonu toocreate S2D depolama bağlı tooyour etki alanı ile bir SQL Server FCI çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6397-128">You can run hello template toocreate a SQL Server FCI with S2D storage connected tooyour domain.</span></span> <span data-ttu-id="e6397-129">Merhaba şablon değerlendirin ve amaçlarınız için değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6397-129">You can evaluate hello template, and modify it for your purposes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e6397-130">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="e6397-130">Before you begin</span></span>

<span data-ttu-id="e6397-131">Devam etmeden önce tooknow ve gereken şunları yerinde gereken birkaç nokta vardır.</span><span class="sxs-lookup"><span data-stu-id="e6397-131">There are a few things you need tooknow and a couple of things that you need in place before you proceed.</span></span>

### <a name="what-tooknow"></a><span data-ttu-id="e6397-132">Hangi tooknow</span><span class="sxs-lookup"><span data-stu-id="e6397-132">What tooknow</span></span>
<span data-ttu-id="e6397-133">İşletimsel bir teknolojileri aşağıdaki hello anlamış olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e6397-133">You should have an operational understanding of hello following technologies:</span></span>

- [<span data-ttu-id="e6397-134">Windows Küme teknolojileri</span><span class="sxs-lookup"><span data-stu-id="e6397-134">Windows cluster technologies</span></span>](http://technet.microsoft.com/library/hh831579.aspx)
-  <span data-ttu-id="e6397-135">[SQL Server Yük devretme kümesi örnekleri](http://msdn.microsoft.com/library/ms189134.aspx).</span><span class="sxs-lookup"><span data-stu-id="e6397-135">[SQL Server Failover Cluster Instances](http://msdn.microsoft.com/library/ms189134.aspx).</span></span>

<span data-ttu-id="e6397-136">Ayrıca, hello teknolojileri aşağıdaki genel bir anlamış olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e6397-136">Also, you should have a general understanding of hello following technologies:</span></span>

- [<span data-ttu-id="e6397-137">Depolama alanları doğrudan Windows Server 2016 kullanarak Hyper-yakınsanmış çözüm</span><span class="sxs-lookup"><span data-stu-id="e6397-137">Hyper-converged solution using Storage Spaces Direct in Windows Server 2016</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [<span data-ttu-id="e6397-138">Azure kaynak grupları</span><span class="sxs-lookup"><span data-stu-id="e6397-138">Azure resource groups</span></span>](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-toohave"></a><span data-ttu-id="e6397-139">Hangi toohave</span><span class="sxs-lookup"><span data-stu-id="e6397-139">What toohave</span></span>

<span data-ttu-id="e6397-140">Bu makaledeki Hello yönergeleri izlemeden önce olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e6397-140">Before following hello instructions in this article, you should already have:</span></span>

- <span data-ttu-id="e6397-141">Microsoft Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="e6397-141">A Microsoft Azure subscription.</span></span>
- <span data-ttu-id="e6397-142">Bir Windows etki alanı Azure sanal makinelerde.</span><span class="sxs-lookup"><span data-stu-id="e6397-142">A Windows domain on Azure virtual machines.</span></span>
- <span data-ttu-id="e6397-143">Hello Azure sanal makinesi izni toocreate nesneleri olan bir hesap.</span><span class="sxs-lookup"><span data-stu-id="e6397-143">An account with permission toocreate objects in hello Azure virtual machine.</span></span>
- <span data-ttu-id="e6397-144">Bir Azure sanal ağ ve alt ağ bileşenleri aşağıdaki hello için yeterli IP adresi alanı ile:</span><span class="sxs-lookup"><span data-stu-id="e6397-144">An Azure virtual network and subnet with sufficient IP address space for hello following components:</span></span>
   - <span data-ttu-id="e6397-145">Her iki sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="e6397-145">Both virtual machines.</span></span>
   - <span data-ttu-id="e6397-146">Merhaba yük devretme küme IP adresi.</span><span class="sxs-lookup"><span data-stu-id="e6397-146">hello failover cluster IP address.</span></span>
   - <span data-ttu-id="e6397-147">Her FCI için bir IP adresi.</span><span class="sxs-lookup"><span data-stu-id="e6397-147">An IP address for each FCI.</span></span>
- <span data-ttu-id="e6397-148">Merhaba toohello etki alanı denetleyicileri işaret eden Azure ağ üzerinde yapılandırılmış DNS.</span><span class="sxs-lookup"><span data-stu-id="e6397-148">DNS configured on hello Azure Network, pointing toohello domain controllers.</span></span>

<span data-ttu-id="e6397-149">Bu önkoşulları yerine getirilince, yük devretme kümesi oluşturmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6397-149">With these prerequisites in place, you can proceed with building your failover cluster.</span></span> <span data-ttu-id="e6397-150">Merhaba ilk toocreate hello sanal makineleri bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="e6397-150">hello first step is toocreate hello virtual machines.</span></span>

## <a name="step-1-create-virtual-machines"></a><span data-ttu-id="e6397-151">1. adım: sanal makineler oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6397-151">Step 1: Create virtual machines</span></span>

1. <span data-ttu-id="e6397-152">İçinde toohello oturum [Azure portal](http://portal.azure.com) aboneliğinizle.</span><span class="sxs-lookup"><span data-stu-id="e6397-152">Log in toohello [Azure portal](http://portal.azure.com) with your subscription.</span></span>

1. <span data-ttu-id="e6397-153">[Azure kullanılabilirlik kümesi oluştur](../tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="e6397-153">[Create an Azure availability set](../tutorial-availability-sets.md).</span></span>

   <span data-ttu-id="e6397-154">Merhaba kullanılabilirlik grupları sanal makineleri hata etki alanlarında ayarlayın ve güncelleme etki alanları.</span><span class="sxs-lookup"><span data-stu-id="e6397-154">hello availability set groups virtual machines across fault domains and update domains.</span></span> <span data-ttu-id="e6397-155">Merhaba kullanılabilirlik kümesi, uygulamanızın hatanın Merhaba ağ anahtarı veya bir sunucu rafı hello güç ünitesi gibi tek nokta etkilenmez emin olur.</span><span class="sxs-lookup"><span data-stu-id="e6397-155">hello availability set makes sure that your application is not affected by single points of failure, like hello network switch or hello power unit of a rack of servers.</span></span>

   <span data-ttu-id="e6397-156">Sanal makineleriniz için hello kaynak grubu oluşturmadıysanız, bunu bir Azure kullanılabilirlik kümesi oluşturduğunuzda.</span><span class="sxs-lookup"><span data-stu-id="e6397-156">If you have not created hello resource group for your virtual machines, do it when you create an Azure availability set.</span></span> <span data-ttu-id="e6397-157">Hello Azure portal toocreate hello kullanılabilirlik kümesi kullanıyorsanız, adımları hello:</span><span class="sxs-lookup"><span data-stu-id="e6397-157">If you're using hello Azure portal toocreate hello availability set, do hello following steps:</span></span>

   - <span data-ttu-id="e6397-158">Hello Azure portal'ı tıklatın  **+**  tooopen hello Azure Marketi.</span><span class="sxs-lookup"><span data-stu-id="e6397-158">In hello Azure portal, click **+** tooopen hello Azure Marketplace.</span></span> <span data-ttu-id="e6397-159">Arama **kullanılabilirlik kümesi**.</span><span class="sxs-lookup"><span data-stu-id="e6397-159">Search for **Availability set**.</span></span>
   - <span data-ttu-id="e6397-160">Tıklatın **kullanılabilirlik kümesi**.</span><span class="sxs-lookup"><span data-stu-id="e6397-160">Click **Availability set**.</span></span>
   - <span data-ttu-id="e6397-161">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e6397-161">Click **Create**.</span></span>
   - <span data-ttu-id="e6397-162">Merhaba üzerinde **kullanılabilirlik kümesi oluştur** dikey penceresinde, aşağıdaki değerleri kümesi hello:</span><span class="sxs-lookup"><span data-stu-id="e6397-162">On hello **Create availability set** blade, set hello following values:</span></span>
      - <span data-ttu-id="e6397-163">**Ad**: hello kullanılabilirlik kümesi için bir ad.</span><span class="sxs-lookup"><span data-stu-id="e6397-163">**Name**: A name for hello availability set.</span></span>
      - <span data-ttu-id="e6397-164">**Abonelik**: bilgisayarınızı Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="e6397-164">**Subscription**: Your Azure subscription.</span></span>
      - <span data-ttu-id="e6397-165">**Kaynak grubu**: toouse varolan bir grubu istiyorsanız, **var olanı kullan** ve hello aşağı açılan listeden seçim hello grubu.</span><span class="sxs-lookup"><span data-stu-id="e6397-165">**Resource group**: If you want toouse an existing group, click **Use existing** and select hello group from hello drop-down list.</span></span> <span data-ttu-id="e6397-166">Seçmediğiniz **Yeni Oluştur** ve hello grubu için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="e6397-166">Otherwise choose **Create New** and type a name for hello group.</span></span>
      - <span data-ttu-id="e6397-167">**Konum**: sanal makinelerinizi planlama nerede toocreate hello konumunu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e6397-167">**Location**: Set hello location where you plan toocreate your virtual machines.</span></span>
      - <span data-ttu-id="e6397-168">**Hata etki alanları**: hello varsayılan (3) kullanın.</span><span class="sxs-lookup"><span data-stu-id="e6397-168">**Fault domains**: Use hello default (3).</span></span>
      - <span data-ttu-id="e6397-169">**Güncelleme etki alanları**: hello varsayılan (5) kullanın.</span><span class="sxs-lookup"><span data-stu-id="e6397-169">**Update domains**: Use hello default (5).</span></span>
   - <span data-ttu-id="e6397-170">Tıklatın **oluşturma** toocreate hello kullanılabilirlik kümesi.</span><span class="sxs-lookup"><span data-stu-id="e6397-170">Click **Create** toocreate hello availability set.</span></span>

1. <span data-ttu-id="e6397-171">Merhaba kullanılabilirlik kümesinde Hello sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e6397-171">Create hello virtual machines in hello availability set.</span></span>

   <span data-ttu-id="e6397-172">Hello Azure kullanılabilirlik kümesindeki iki SQL Server sanal makine sağlayın.</span><span class="sxs-lookup"><span data-stu-id="e6397-172">Provision two SQL Server virtual machines in hello Azure availability set.</span></span> <span data-ttu-id="e6397-173">Yönergeler için bkz: [hello Azure portal'ın SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="e6397-173">For instructions, see [Provision a SQL Server virtual machine in hello Azure portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

   <span data-ttu-id="e6397-174">Her iki sanal makine koyun:</span><span class="sxs-lookup"><span data-stu-id="e6397-174">Place both virtual machines:</span></span>

   - <span data-ttu-id="e6397-175">Hello, kullanılabilirlik kümesi aynı Azure kaynak grubu değil.</span><span class="sxs-lookup"><span data-stu-id="e6397-175">In hello same Azure resource group that your availability set is in.</span></span>
   - <span data-ttu-id="e6397-176">Merhaba üzerinde aynı etki alanı denetleyicisi olarak ağ.</span><span class="sxs-lookup"><span data-stu-id="e6397-176">On hello same network as your domain controller.</span></span>
   - <span data-ttu-id="e6397-177">Sanal makineler hem bu kümede sonunda kullanabilir tüm Fcı'lerde için yeterli IP adres alanı ile bir alt ağ üzerinde.</span><span class="sxs-lookup"><span data-stu-id="e6397-177">On a subnet with sufficient IP address space for both virtual machines, and all FCIs that you may eventually use on this cluster.</span></span>
   - <span data-ttu-id="e6397-178">Hello Azure kullanılabilirlik kümesinde.</span><span class="sxs-lookup"><span data-stu-id="e6397-178">In hello Azure availability set.</span></span>   

      >[!IMPORTANT]
      ><span data-ttu-id="e6397-179">Ayarlayın veya bir sanal makine oluşturulduktan sonra ayarlanmış kullanılabilirlik değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e6397-179">You cannot set or change availability set after a virtual machine has been created.</span></span>

   <span data-ttu-id="e6397-180">Azure Market hello bir görüntü seçin.</span><span class="sxs-lookup"><span data-stu-id="e6397-180">Choose an image from hello Azure Marketplace.</span></span> <span data-ttu-id="e6397-181">Bir Market kullanabilirsiniz, görüntü, Windows Server ve SQL Server ya da yalnızca hello Windows Server içerir.</span><span class="sxs-lookup"><span data-stu-id="e6397-181">You can use a Marketplace image with that includes Windows Server and SQL Server, or just hello Windows Server.</span></span> <span data-ttu-id="e6397-182">Ayrıntılar için bkz [genel bakış SQL Server'ın Azure sanal makineler üzerinde](../../virtual-machines-windows-sql-server-iaas-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e6397-182">For details, see [Overview of SQL Server on Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)</span></span>

   <span data-ttu-id="e6397-183">hello Azure Galerisi Hello resmi SQL Server görüntülerinin bir yüklü SQL Server örneği, artı hello SQL Server yükleme yazılımı ve hello gereken anahtar içerir.</span><span class="sxs-lookup"><span data-stu-id="e6397-183">hello official SQL Server images in hello Azure Gallery include an installed SQL Server instance, plus hello SQL Server installation software, and hello required key.</span></span>

   <span data-ttu-id="e6397-184">Merhaba sağ görüntü toopay hello SQL Server Lisans için istediğiniz toohow göre seçin:</span><span class="sxs-lookup"><span data-stu-id="e6397-184">Choose hello right image according toohow you want toopay for hello SQL Server license:</span></span>

   - <span data-ttu-id="e6397-185">**Kullanım lisansı başına ödeme**: Bu görüntülerin hello dakika başına maliyet içerir hello SQL Server Lisansı:</span><span class="sxs-lookup"><span data-stu-id="e6397-185">**Pay per usage licensing**: hello per-minute cost of these images includes hello SQL Server licensing:</span></span>
      - <span data-ttu-id="e6397-186">**Windows Server Datacenter 2016 üzerinde SQL Server 2016 Enterprise**</span><span class="sxs-lookup"><span data-stu-id="e6397-186">**SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="e6397-187">**Windows Server Datacenter 2016 SQL Server 2016 standardı**</span><span class="sxs-lookup"><span data-stu-id="e6397-187">**SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="e6397-188">**Windows Server Datacenter 2016 SQL Server 2016 Geliştirici**</span><span class="sxs-lookup"><span data-stu-id="e6397-188">**SQL Server 2016 Developer on Windows Server Datacenter 2016**</span></span>

   - <span data-ttu-id="e6397-189">**Getir bilgisayarınızı-kendi-lisans (KLG)**</span><span class="sxs-lookup"><span data-stu-id="e6397-189">**Bring-your-own-license (BYOL)**</span></span>

      - <span data-ttu-id="e6397-190">**{KLG} Windows Server Datacenter 2016 üzerinde SQL Server 2016 Enterprise**</span><span class="sxs-lookup"><span data-stu-id="e6397-190">**{BYOL} SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="e6397-191">**{KLG} Windows Server Datacenter 2016 SQL Server 2016 standardı**</span><span class="sxs-lookup"><span data-stu-id="e6397-191">**{BYOL} SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="e6397-192">Merhaba sanal makineyi oluşturduktan sonra hello önceden yüklenmiş tek başına SQL Server örneğini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e6397-192">After you create hello virtual machine, remove hello pre-installed standalone SQL Server instance.</span></span> <span data-ttu-id="e6397-193">Merhaba yük devretme kümesi ve S2D yapılandırdıktan sonra hello önceden yüklü SQL Server medya toocreate hello SQL Server FCI kullanır.</span><span class="sxs-lookup"><span data-stu-id="e6397-193">You will use hello pre-installed SQL Server media toocreate hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span>

   <span data-ttu-id="e6397-194">Alternatif olarak, yalnızca hello işletim sistemiyle Azure Market görüntülerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6397-194">Alternatively, you can use Azure Marketplace images with just hello operating system.</span></span> <span data-ttu-id="e6397-195">Seçin bir **Windows Server 2016 Datacenter** görüntü ve hello yük devretme kümesi ve S2D yapılandırdıktan sonra hello SQL Server FCI yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e6397-195">Choose a **Windows Server 2016 Datacenter** image and install hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span> <span data-ttu-id="e6397-196">Bu görüntü, SQL Server yükleme medyasını içermiyor.</span><span class="sxs-lookup"><span data-stu-id="e6397-196">This image does not contain SQL Server installation media.</span></span> <span data-ttu-id="e6397-197">Merhaba yükleme medyasını hello SQL Server yüklemesi her sunucu için çalıştırdığı bir konuma yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="e6397-197">Place hello installation media in a location where you can run hello SQL Server installation for each server.</span></span>

1. <span data-ttu-id="e6397-198">Azure sanal makinelerinizi oluşturduktan sonra tooeach sanal makinenin RDP ile bağlanır.</span><span class="sxs-lookup"><span data-stu-id="e6397-198">After Azure creates your virtual machines, connect tooeach virtual machine with RDP.</span></span>

   <span data-ttu-id="e6397-199">RDP ile ilk tooa sanal makineye bağlandığınızda hello bilgisayar, tooallow bu PC toobe hello ağ üzerinde bulunabilir isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="e6397-199">When you first connect tooa virtual machine with RDP, hello computer asks if you want tooallow this PC toobe discoverable on hello network.</span></span> <span data-ttu-id="e6397-200">**Evet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e6397-200">Click **Yes**.</span></span>

1. <span data-ttu-id="e6397-201">Merhaba SQL Server tabanlı sanal makine görüntülerden birini kullanıyorsanız, hello SQL Server örneğini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e6397-201">If you are using one of hello SQL Server-based virtual machine images, remove hello SQL Server instance.</span></span>

   - <span data-ttu-id="e6397-202">İçinde **programlar ve Özellikler**, sağ **Microsoft SQL Server 2016 (64 bit)** tıklatıp **Kaldır/Değiştir**.</span><span class="sxs-lookup"><span data-stu-id="e6397-202">In **Programs and Features**, right-click **Microsoft SQL Server 2016 (64-bit)** and click **Uninstall/Change**.</span></span>
   - <span data-ttu-id="e6397-203">Tıklatın **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="e6397-203">Click **Remove**.</span></span>
   - <span data-ttu-id="e6397-204">Merhaba varsayılan örneği seçin.</span><span class="sxs-lookup"><span data-stu-id="e6397-204">Select hello default instance.</span></span>
   - <span data-ttu-id="e6397-205">Tüm Özellikleri'nin altında kaldırmak **veritabanı altyapısı Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="e6397-205">Remove all features under **Database Engine Services**.</span></span> <span data-ttu-id="e6397-206">Kaldırmayın **Paylaşılan Özellikler**.</span><span class="sxs-lookup"><span data-stu-id="e6397-206">Do not remove **Shared Features**.</span></span> <span data-ttu-id="e6397-207">Resim aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="e6397-207">See hello following picture:</span></span>

      ![Özellikleri Kaldır](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - <span data-ttu-id="e6397-209">Tıklatın **sonraki**ve ardından **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="e6397-209">Click **Next**, and then click **Remove**.</span></span>

1. <span data-ttu-id="e6397-210"><a name="ports"></a>Merhaba güvenlik duvarı bağlantı noktalarını açın.</span><span class="sxs-lookup"><span data-stu-id="e6397-210"><a name="ports"></a>Open hello firewall ports.</span></span>

   <span data-ttu-id="e6397-211">Her sanal makineye hello üzerinde Windows Güvenlik Duvarı bağlantı noktaları aşağıdaki hello açın.</span><span class="sxs-lookup"><span data-stu-id="e6397-211">On each virtual machine, open hello following ports on hello Windows Firewall.</span></span>

   | <span data-ttu-id="e6397-212">Amaç</span><span class="sxs-lookup"><span data-stu-id="e6397-212">Purpose</span></span> | <span data-ttu-id="e6397-213">TCP bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="e6397-213">TCP Port</span></span> | <span data-ttu-id="e6397-214">Notlar</span><span class="sxs-lookup"><span data-stu-id="e6397-214">Notes</span></span>
   | ------ | ------ | ------
   | <span data-ttu-id="e6397-215">SQL Server</span><span class="sxs-lookup"><span data-stu-id="e6397-215">SQL Server</span></span> | <span data-ttu-id="e6397-216">1433</span><span class="sxs-lookup"><span data-stu-id="e6397-216">1433</span></span> | <span data-ttu-id="e6397-217">SQL Server'ın varsayılan örnekleri için normal bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="e6397-217">Normal port for default instances of SQL Server.</span></span> <span data-ttu-id="e6397-218">Merhaba Galeriden bir görüntü kullandıysanız, bu bağlantı noktası otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="e6397-218">If you used an image from hello gallery, this port is automatically opened.</span></span>
   | <span data-ttu-id="e6397-219">Sistem durumu araştırması</span><span class="sxs-lookup"><span data-stu-id="e6397-219">Health probe</span></span> | <span data-ttu-id="e6397-220">59999</span><span class="sxs-lookup"><span data-stu-id="e6397-220">59999</span></span> | <span data-ttu-id="e6397-221">Herhangi bir TCP bağlantı noktasını açın.</span><span class="sxs-lookup"><span data-stu-id="e6397-221">Any open TCP port.</span></span> <span data-ttu-id="e6397-222">Bir sonraki adımda hello yük dengeleyici yapılandırmanız [durumu araştırması](#probe) ve bu bağlantı noktası küme toouse hello.</span><span class="sxs-lookup"><span data-stu-id="e6397-222">In a later step, configure hello load balancer [health probe](#probe) and hello cluster toouse this port.</span></span>  

1. <span data-ttu-id="e6397-223">Depolama toohello sanal makine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e6397-223">Add storage toohello virtual machine.</span></span> <span data-ttu-id="e6397-224">Ayrıntılı bilgi için bkz: [depolama ekleme](../../../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="e6397-224">For detailed information, see [add storage](../../../storage/common/storage-premium-storage.md).</span></span>

   <span data-ttu-id="e6397-225">Her iki sanal makinelerin en az iki veri diskleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6397-225">Both virtual machines need at least two data disks.</span></span>

   <span data-ttu-id="e6397-226">Ham diskleri - bağlamanız değil NTFS biçimli disk.</span><span class="sxs-lookup"><span data-stu-id="e6397-226">Attach raw disks - not NTFS formatted disks.</span></span>
      >[!NOTE]
      ><span data-ttu-id="e6397-227">NTFS biçimli disk eklerseniz, yalnızca hiçbir disk uygunluk denetimi ile S2D etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6397-227">If you attach NTFS-formatted disks, you can only enable S2D with no disk eligibility check.</span></span>  

   <span data-ttu-id="e6397-228">En az iki Premium Storage (SSD diskleri) tooeach VM ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e6397-228">Attach a minimum of two Premium Storage (SSD disks) tooeach VM.</span></span> <span data-ttu-id="e6397-229">En az öneririz P30 (1 TB) diskler.</span><span class="sxs-lookup"><span data-stu-id="e6397-229">We recommend at least P30 (1 TB) disks.</span></span>

   <span data-ttu-id="e6397-230">Çok önbelleğe alma kümesi konak**salt okunur**.</span><span class="sxs-lookup"><span data-stu-id="e6397-230">Set host caching too**Read-only**.</span></span>

   <span data-ttu-id="e6397-231">üretim ortamlarında kullanmak hello depolama kapasitesi, iş yüküne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="e6397-231">hello storage capacity you use in production environments depends on your workload.</span></span> <span data-ttu-id="e6397-232">Bu makalede açıklanan hello tanıtım ve test için değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="e6397-232">hello values described in this article are for demonstration and testing.</span></span>

1. <span data-ttu-id="e6397-233">[Merhaba sanal makineleri tooyour önceden var olan etki alanı ekleme](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="e6397-233">[Add hello virtual machines tooyour pre-existing domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

<span data-ttu-id="e6397-234">Merhaba sanal makineler oluşturup yapılandırılmış sonra hello yük devretme kümesini yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6397-234">After hello virtual machines are created and configured, you can configure hello failover cluster.</span></span>

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a><span data-ttu-id="e6397-235">2. adım: hello Windows Yük devretme kümesi ile S2D yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e6397-235">Step 2: Configure hello Windows Failover Cluster with S2D</span></span>

<span data-ttu-id="e6397-236">Merhaba sonraki S2D ile tooconfigure hello yük devretme kümesi adımdır.</span><span class="sxs-lookup"><span data-stu-id="e6397-236">hello next step is tooconfigure hello failover cluster with S2D.</span></span> <span data-ttu-id="e6397-237">Bu adımda, ne yapacağını hello alt adımlar:</span><span class="sxs-lookup"><span data-stu-id="e6397-237">In this step, you will do hello following substeps:</span></span>

1. <span data-ttu-id="e6397-238">Windows Yük Devretme Kümelemesi özelliğini ekleyin</span><span class="sxs-lookup"><span data-stu-id="e6397-238">Add Windows Failover Clustering feature</span></span>
1. <span data-ttu-id="e6397-239">Merhaba küme doğrulama</span><span class="sxs-lookup"><span data-stu-id="e6397-239">Validate hello cluster</span></span>
1. <span data-ttu-id="e6397-240">Merhaba yük devretme kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6397-240">Create hello failover cluster</span></span>
1. <span data-ttu-id="e6397-241">Merhaba bulut tanığı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6397-241">Create hello cloud witness</span></span>
1. <span data-ttu-id="e6397-242">Depolama ekleme</span><span class="sxs-lookup"><span data-stu-id="e6397-242">Add storage</span></span>

### <a name="add-windows-failover-clustering-feature"></a><span data-ttu-id="e6397-243">Windows Yük Devretme Kümelemesi özelliğini ekleyin</span><span class="sxs-lookup"><span data-stu-id="e6397-243">Add Windows Failover Clustering feature</span></span>

1. <span data-ttu-id="e6397-244">toobegin, Yerel yöneticilerin üyesi olduğunu ve izinleri toocreate nesneleri Active Directory'de bir etki alanı hesabı kullanarak RDP toohello ilk sanal makineye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="e6397-244">toobegin, connect toohello first virtual machine with RDP using a domain account that is a member of local administrators, and has permissions toocreate objects in Active Directory.</span></span> <span data-ttu-id="e6397-245">Bu hesabı hello yapılandırma hello kalanı için kullanın.</span><span class="sxs-lookup"><span data-stu-id="e6397-245">Use this account for hello rest of hello configuration.</span></span>

1. <span data-ttu-id="e6397-246">[Yük Devretme Kümelemesi özelliğini tooeach sanal makine eklemek](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="e6397-246">[Add Failover Clustering feature tooeach virtual machine](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

   <span data-ttu-id="e6397-247">tooinstall Yük Devretme Kümelemesi özelliğini hello UI, hello her iki sanal makine aşağıdaki adımları.</span><span class="sxs-lookup"><span data-stu-id="e6397-247">tooinstall Failover Clustering feature from hello UI, do hello following steps on both virtual machines.</span></span>
   - <span data-ttu-id="e6397-248">İçinde **Sunucu Yöneticisi'ni**, tıklatın **Yönet**ve ardından **rol ve Özellik Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e6397-248">In **Server Manager**, click **Manage**, and then click **Add Roles and Features**.</span></span>
   - <span data-ttu-id="e6397-249">İçinde **Ekle roller ve Özellikler Sihirbazı**, tıklatın **sonraki** çok alana kadar**Özellikleri Seç**.</span><span class="sxs-lookup"><span data-stu-id="e6397-249">In **Add Roles and Features Wizard**, click **Next** until you get too**Select Features**.</span></span>
   - <span data-ttu-id="e6397-250">İçinde **Özellikleri Seç**, tıklatın **Yük Devretme Kümelemesi**.</span><span class="sxs-lookup"><span data-stu-id="e6397-250">In **Select Features**, click **Failover Clustering**.</span></span> <span data-ttu-id="e6397-251">Tüm gerekli özellikleri ve hello yönetim araçlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="e6397-251">Include all required features and hello management tools.</span></span> <span data-ttu-id="e6397-252">Tıklatın **özelliklere**.</span><span class="sxs-lookup"><span data-stu-id="e6397-252">Click **Add Features**.</span></span>
   - <span data-ttu-id="e6397-253">Tıklatın **sonraki** ve ardından **son** tooinstall hello özellikleri.</span><span class="sxs-lookup"><span data-stu-id="e6397-253">Click **Next** and then click **Finish** tooinstall hello features.</span></span>

   <span data-ttu-id="e6397-254">tooinstall hello Yük Devretme Kümelemesi özelliğiyle PowerShell, komut dosyası bir yönetici PowerShell oturumundan hello sanal makineleri biri üzerinde aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e6397-254">tooinstall hello Failover Clustering feature with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

<span data-ttu-id="e6397-255">Başvuru için sonraki adımlar hello hello adım 3'ün altında yönergeleri [depolama alanları doğrudan Windows Server 2016 kullanarak Hyper-yakınsanmış çözüm](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="e6397-255">For reference, hello next steps follow hello instructions under Step 3 of [Hyper-converged solution using Storage Spaces Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span></span>

### <a name="validate-hello-cluster"></a><span data-ttu-id="e6397-256">Merhaba küme doğrulama</span><span class="sxs-lookup"><span data-stu-id="e6397-256">Validate hello cluster</span></span>

<span data-ttu-id="e6397-257">Bu kılavuz altında tooinstructions başvuruyor [küme doğrulama](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span><span class="sxs-lookup"><span data-stu-id="e6397-257">This guide refers tooinstructions under [validate cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span></span>

<span data-ttu-id="e6397-258">Merhaba küme hello kullanıcı Arabirimi veya PowerShell ile doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e6397-258">Validate hello cluster in hello UI or with PowerShell.</span></span>

<span data-ttu-id="e6397-259">Merhaba UI, toovalidate hello kümeyle hello hello sanal makineleri birinden aşağıdaki adımları.</span><span class="sxs-lookup"><span data-stu-id="e6397-259">toovalidate hello cluster with hello UI, do hello following steps from one of hello virtual machines.</span></span>

1. <span data-ttu-id="e6397-260">İçinde **Sunucu Yöneticisi'ni**, tıklatın **Araçları**, ardından **yük devretme kümesi Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="e6397-260">In **Server Manager**, click **Tools**, then click **Failover Cluster Manager**.</span></span>
1. <span data-ttu-id="e6397-261">İçinde **yük devretme kümesi Yöneticisi**, tıklatın **eylem**, ardından **yapılandırmasını doğrula...** .</span><span class="sxs-lookup"><span data-stu-id="e6397-261">In **Failover Cluster Manager**, click **Action**, then click **Validate Configuration...**.</span></span>
1. <span data-ttu-id="e6397-262">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e6397-262">Click **Next**.</span></span>
1. <span data-ttu-id="e6397-263">Üzerinde **sunucuları Seç veya küme**, her iki sanal makine türü hello adı.</span><span class="sxs-lookup"><span data-stu-id="e6397-263">On **Select Servers or a Cluster**, type hello name of both virtual machines.</span></span>
1. <span data-ttu-id="e6397-264">Üzerinde **testi seçenekleri**, seçin **yalnızca seçtiğim Testleri Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="e6397-264">On **Testing options**, choose **Run only tests I select**.</span></span> <span data-ttu-id="e6397-265">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e6397-265">Click **Next**.</span></span>
1. <span data-ttu-id="e6397-266">Üzerinde **Test seçimi**, dışındaki tüm testleri dahil **depolama**.</span><span class="sxs-lookup"><span data-stu-id="e6397-266">On **Test selection**, include all tests except **Storage**.</span></span> <span data-ttu-id="e6397-267">Resim aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="e6397-267">See hello following picture:</span></span>

   ![Testleri doğrula](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. <span data-ttu-id="e6397-269">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e6397-269">Click **Next**.</span></span>
1. <span data-ttu-id="e6397-270">Üzerinde **onay**, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e6397-270">On **Confirmation**, click **Next**.</span></span>

<span data-ttu-id="e6397-271">Merhaba **Yapılandırma Doğrulama Sihirbazı** hello doğrulama sınamalarını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="e6397-271">hello **Validate a Configuration Wizard** runs hello validation tests.</span></span>

<span data-ttu-id="e6397-272">PowerShell komut dosyası bir yönetici PowerShell oturumundan hello sanal makineleri biri üzerinde aşağıdaki hello çalıştırmak ile toovalidate hello kümesi.</span><span class="sxs-lookup"><span data-stu-id="e6397-272">toovalidate hello cluster with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

<span data-ttu-id="e6397-273">Merhaba küme doğrulama sonra hello yük devretme kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e6397-273">After you validate hello cluster, create hello failover cluster.</span></span>

### <a name="create-hello-failover-cluster"></a><span data-ttu-id="e6397-274">Merhaba yük devretme kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6397-274">Create hello failover cluster</span></span>

<span data-ttu-id="e6397-275">Bu kılavuzda çok başvuruyor[oluşturma hello yük devretme kümesi](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span><span class="sxs-lookup"><span data-stu-id="e6397-275">This guide refers too[Create hello failover cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span></span>

<span data-ttu-id="e6397-276">toocreate hello yük devretme kümesi, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="e6397-276">toocreate hello failover cluster, you need:</span></span>
- <span data-ttu-id="e6397-277">Merhaba adları hello sanal makinelerin, hello küme düğümleri haline gelir.</span><span class="sxs-lookup"><span data-stu-id="e6397-277">hello names of hello virtual machines that become hello cluster nodes.</span></span>
- <span data-ttu-id="e6397-278">Merhaba yük devretme kümesi için bir ad</span><span class="sxs-lookup"><span data-stu-id="e6397-278">A name for hello failover cluster</span></span>
- <span data-ttu-id="e6397-279">Merhaba yük devretme kümesi için bir IP adresi.</span><span class="sxs-lookup"><span data-stu-id="e6397-279">An IP address for hello failover cluster.</span></span> <span data-ttu-id="e6397-280">Merhaba üzerinde kullanılmayan bir IP adresi kullanabileceğiniz aynı Azure sanal ağ ve küme düğümleri hello gibi alt.</span><span class="sxs-lookup"><span data-stu-id="e6397-280">You can use an IP address that is not used on hello same Azure virtual network and subnet as hello cluster nodes.</span></span>

<span data-ttu-id="e6397-281">PowerShell aşağıdaki hello bir yük devretme kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e6397-281">hello following PowerShell creates a failover cluster.</span></span> <span data-ttu-id="e6397-282">Merhaba betik (Merhaba sanal makine adları) hello düğümlerinin hello adlarla ve hello Azure VNET kullanılabilir bir IP adresinden güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="e6397-282">Update hello script with hello names of hello nodes (hello virtual machine names) and an available IP address from hello Azure VNET:</span></span>

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a><span data-ttu-id="e6397-283">Bir bulut tanığı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6397-283">Create a cloud witness</span></span>

<span data-ttu-id="e6397-284">Bulut tanığı, küme çekirdek tanığı bir Azure depolama Blob depolanan yeni türüdür.</span><span class="sxs-lookup"><span data-stu-id="e6397-284">Cloud Witness is a new type of cluster quorum witness stored in an Azure Storage Blob.</span></span> <span data-ttu-id="e6397-285">Bu, bir Tanık paylaşımı barındırma ayrı bir VM hello gereksinimini ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="e6397-285">This removes hello need of a separate VM hosting a witness share.</span></span>

1. <span data-ttu-id="e6397-286">[Merhaba yük devretme kümesi için bir bulut tanığı oluşturma](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="e6397-286">[Create a cloud witness for hello failover cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span>

1. <span data-ttu-id="e6397-287">Bir blob kapsayıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e6397-287">Create a blob container.</span></span>

1. <span data-ttu-id="e6397-288">Merhaba erişim tuşları ve hello kapsayıcı URL'si kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e6397-288">Save hello access keys and hello container URL.</span></span>

1. <span data-ttu-id="e6397-289">Merhaba yük devretme kümesi küme çekirdek tanığı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e6397-289">Configure hello failover cluster cluster quorum witness.</span></span> <span data-ttu-id="e6397-290">Bakın, [hello çekirdek tanığı hello kullanıcı arabiriminde Yapılandır]. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) hello UI içinde.</span><span class="sxs-lookup"><span data-stu-id="e6397-290">See, [Configure hello quorum witness in hello user interface].(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in hello UI.</span></span>

### <a name="add-storage"></a><span data-ttu-id="e6397-291">Depolama ekleme</span><span class="sxs-lookup"><span data-stu-id="e6397-291">Add storage</span></span>

<span data-ttu-id="e6397-292">S2D Hello diskler boş ve bölümleri veya diğer veri olmadan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6397-292">hello disks for S2D need toobe empty and without partitions or other data.</span></span> <span data-ttu-id="e6397-293">tooclean diskleri izleyin [hello bu kılavuzdaki adımları](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span><span class="sxs-lookup"><span data-stu-id="e6397-293">tooclean disks follow [hello steps in this guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span></span>

1. <span data-ttu-id="e6397-294">[Etkinleştirme depolama alanları doğrudan \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="e6397-294">[Enable Store Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span></span>

   <span data-ttu-id="e6397-295">PowerShell aşağıdaki hello doğrudan depolama alanları sağlar.</span><span class="sxs-lookup"><span data-stu-id="e6397-295">hello following PowerShell enables storage spaces direct.</span></span>  

   ```PowerShell
   Enable-ClusterS2D
   ```

   <span data-ttu-id="e6397-296">İçinde **yük devretme kümesi Yöneticisi**, hello depolama havuzu şimdi görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6397-296">In **Failover Cluster Manager**, you can now see hello storage pool.</span></span>

1. <span data-ttu-id="e6397-297">[Bir birim oluşturmak](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span><span class="sxs-lookup"><span data-stu-id="e6397-297">[Create a volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span></span>

   <span data-ttu-id="e6397-298">Merhaba özelliklerinden biri S2D, etkinleştirdiğinizde, otomatik olarak bir depolama havuzu oluşturmasıdır.</span><span class="sxs-lookup"><span data-stu-id="e6397-298">One of hello features of S2D is that it automatically creates a storage pool when you enable it.</span></span> <span data-ttu-id="e6397-299">Hazır toocreate bir birim sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="e6397-299">You are now ready toocreate a volume.</span></span> <span data-ttu-id="e6397-300">PowerShell komutunu hello `New-Volume` biçimlendirme, toohello küme ekleme ve Küme Paylaşılan birimi (CSV) oluşturma gibi hello birim oluşturma işlemini otomatikleştirir.</span><span class="sxs-lookup"><span data-stu-id="e6397-300">hello PowerShell commandlet `New-Volume` automates hello volume creation process, including formatting, adding toohello cluster, and creating a cluster shared volume (CSV).</span></span> <span data-ttu-id="e6397-301">Aşağıdaki örnek hello 800 bir gigabayt (GB) CSV oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e6397-301">hello following example creates an 800 gigabyte (GB) CSV.</span></span>

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   <span data-ttu-id="e6397-302">Bu komut tamamlandıktan sonra bir 800 GB birimin küme kaynağı olarak bağlı.</span><span class="sxs-lookup"><span data-stu-id="e6397-302">After this command completes, an 800 GB volume is mounted as a cluster resource.</span></span> <span data-ttu-id="e6397-303">Hello birimdir adresindeki `C:\ClusterStorage\Volume1\`.</span><span class="sxs-lookup"><span data-stu-id="e6397-303">hello volume is at `C:\ClusterStorage\Volume1\`.</span></span>

   <span data-ttu-id="e6397-304">Aşağıdaki diyagramda hello S2D ile Küme Paylaşılan birimi gösterir:</span><span class="sxs-lookup"><span data-stu-id="e6397-304">hello following diagram shows a cluster shared volume with S2D:</span></span>

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a><span data-ttu-id="e6397-306">3. adım: Test yük devretme küme yük devretmesi</span><span class="sxs-lookup"><span data-stu-id="e6397-306">Step 3: Test failover cluster failover</span></span>

<span data-ttu-id="e6397-307">Yük Devretme Kümesi Yöneticisi'nde, diğer küme düğümünde hello depolama kaynak toohello taşıyabildiğinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e6397-307">In Failover Cluster Manager, verify that you can move hello storage resource toohello other cluster node.</span></span> <span data-ttu-id="e6397-308">Bağlanabiliyorsa toohello yük devretme kümesi **yük devretme kümesi Yöneticisi** ve tek bir düğüm toohello diğer hello depolama birimini taşımak, hazır tooconfigure hello FCI olur.</span><span class="sxs-lookup"><span data-stu-id="e6397-308">If you can connect toohello failover cluster with **Failover Cluster Manager** and move hello storage from one node toohello other, you are ready tooconfigure hello FCI.</span></span>

## <a name="step-4-create-sql-server-fci"></a><span data-ttu-id="e6397-309">4. adım: SQL Server FCI oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6397-309">Step 4: Create SQL Server FCI</span></span>

<span data-ttu-id="e6397-310">Merhaba yük devretme kümesi ve depolama da dahil olmak üzere tüm küme bileşenleri yapılandırdıktan sonra SQL Server FCI hello oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6397-310">After you have configured hello failover cluster and all cluster components including storage, you can create hello SQL Server FCI.</span></span>

1. <span data-ttu-id="e6397-311">RDP ile toohello ilk sanal makineye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="e6397-311">Connect toohello first virtual machine with RDP.</span></span>

1. <span data-ttu-id="e6397-312">İçinde **yük devretme kümesi Yöneticisi**, tüm küme çekirdek kaynakları hello ilk sanal makinede olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e6397-312">In **Failover Cluster Manager**, make sure all cluster core resources are on hello first virtual machine.</span></span> <span data-ttu-id="e6397-313">Gerekirse, tüm kaynakları toothis sanal makineyi taşıyın.</span><span class="sxs-lookup"><span data-stu-id="e6397-313">If necessary, move all resources toothis virtual machine.</span></span>

1. <span data-ttu-id="e6397-314">Merhaba yükleme medyasını bulun.</span><span class="sxs-lookup"><span data-stu-id="e6397-314">Locate hello installation media.</span></span> <span data-ttu-id="e6397-315">Merhaba sanal makine hello Azure Marketi görüntülerden birini kullanıyorsa, hello medya konumundadır `C:\SQLServer_<version number>_Full`.</span><span class="sxs-lookup"><span data-stu-id="e6397-315">If hello virtual machine uses one of hello Azure Marketplace images, hello media is located at `C:\SQLServer_<version number>_Full`.</span></span> <span data-ttu-id="e6397-316">Tıklatın **Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="e6397-316">Click **Setup**.</span></span>

1. <span data-ttu-id="e6397-317">Merhaba, **SQL Server Yükleme Merkezi'ni**, tıklatın **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="e6397-317">In hello **SQL Server Installation Center**, click **Installation**.</span></span>

1. <span data-ttu-id="e6397-318">Tıklatın **yeni SQL Server Yük devretme kümesi yükleme**.</span><span class="sxs-lookup"><span data-stu-id="e6397-318">Click **New SQL Server failover cluster installation**.</span></span> <span data-ttu-id="e6397-319">Merhaba Sihirbazı tooinstall hello SQL Server FCI'Hello yönergelerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="e6397-319">Follow hello instructions in hello wizard tooinstall hello SQL Server FCI.</span></span>

   <span data-ttu-id="e6397-320">Merhaba FCI veri dizinlerini toobe kümelenmiş depolama gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6397-320">hello FCI data directories need toobe on clustered storage.</span></span> <span data-ttu-id="e6397-321">S2D ile paylaşılan bir disk, ancak her sunucu üzerindeki bir bağlama noktası tooa birimi değil.</span><span class="sxs-lookup"><span data-stu-id="e6397-321">With S2D, it's not a shared disk, but a mount point tooa volume on each server.</span></span> <span data-ttu-id="e6397-322">Her iki düğüm arasında hello birim S2D eşitler.</span><span class="sxs-lookup"><span data-stu-id="e6397-322">S2D synchronizes hello volume between both nodes.</span></span> <span data-ttu-id="e6397-323">Merhaba birim toohello Küme Küme Paylaşılan birimi olarak sunulur.</span><span class="sxs-lookup"><span data-stu-id="e6397-323">hello volume is presented toohello cluster as a cluster shared volume.</span></span> <span data-ttu-id="e6397-324">Merhaba CSV bağlama noktası hello veri dizinler için kullanın.</span><span class="sxs-lookup"><span data-stu-id="e6397-324">Use hello CSV mount point for hello data directories.</span></span>

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. <span data-ttu-id="e6397-326">Merhaba Sihirbazı tamamladıktan sonra kurulumu bir SQL Server FCI hello ilk düğüme yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e6397-326">After you complete hello wizard, Setup will install a SQL Server FCI on hello first node.</span></span>

1. <span data-ttu-id="e6397-327">Kurulum başarıyla hello ilk düğümde hello FCI yüklendikten sonra toohello İkinci düğüm RDP ile bağlanır.</span><span class="sxs-lookup"><span data-stu-id="e6397-327">After Setup successfully installs hello FCI on hello first node, connect toohello second node with RDP.</span></span>

1. <span data-ttu-id="e6397-328">Açık hello **SQL Server Yükleme Merkezi'ni**.</span><span class="sxs-lookup"><span data-stu-id="e6397-328">Open hello **SQL Server Installation Center**.</span></span> <span data-ttu-id="e6397-329">Tıklatın **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="e6397-329">Click **Installation**.</span></span>

1. <span data-ttu-id="e6397-330">Tıklatın **Ekle düğüm tooa SQL Server Yük devretme kümesi**.</span><span class="sxs-lookup"><span data-stu-id="e6397-330">Click **Add node tooa SQL Server failover cluster**.</span></span> <span data-ttu-id="e6397-331">Merhaba Sihirbazı tooinstall SQL Server'daki Hello yönergeleri izleyin ve bu sunucu toohello FCI ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e6397-331">Follow hello instructions in hello wizard tooinstall SQL server and add this server toohello FCI.</span></span>

   >[!NOTE]
   ><span data-ttu-id="e6397-332">SQL Server ile bir Azure Market galeri görüntüsü kullandıysanız, SQL Server araçları hello görüntüsüne dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="e6397-332">If you used an Azure Marketplace gallery image with SQL Server, SQL Server tools were included with hello image.</span></span> <span data-ttu-id="e6397-333">Bu görüntü kullanmadıysanız hello SQL Server araçları ayrı olarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e6397-333">If you did not use this image, install hello SQL Server tools separately.</span></span> <span data-ttu-id="e6397-334">Bkz: [karşıdan SQL Server Management Studio'yu (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="e6397-334">See [Download SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="step-5-create-azure-load-balancer"></a><span data-ttu-id="e6397-335">5. adım: Azure yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6397-335">Step 5: Create Azure load balancer</span></span>

<span data-ttu-id="e6397-336">Azure sanal makinelerde kümeleri bir yük dengeleyici toohold aynı anda bir küme düğümünde toobe gerektiren bir IP adresi kullanın.</span><span class="sxs-lookup"><span data-stu-id="e6397-336">On Azure virtual machines, clusters use a load balancer toohold an IP address that needs toobe on one cluster node at a time.</span></span> <span data-ttu-id="e6397-337">Bu çözümde hello yük dengeleyici hello SQL Server FCI için başlangıç IP adresi tutar.</span><span class="sxs-lookup"><span data-stu-id="e6397-337">In this solution, hello load balancer holds hello IP address for hello SQL Server FCI.</span></span>

<span data-ttu-id="e6397-338">[Oluşturma ve Azure yük dengeleyici yapılandırma](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="e6397-338">[Create and configure an Azure load balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="e6397-339">Hello Azure portal Hello yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6397-339">Create hello load balancer in hello Azure portal</span></span>

<span data-ttu-id="e6397-340">toocreate hello yük dengeleyici:</span><span class="sxs-lookup"><span data-stu-id="e6397-340">toocreate hello load balancer:</span></span>

1. <span data-ttu-id="e6397-341">Hello Azure portal, hello sanal makinelerle toohello kaynak grubuna gidin.</span><span class="sxs-lookup"><span data-stu-id="e6397-341">In hello Azure portal, go toohello Resource Group with hello virtual machines.</span></span>

1. <span data-ttu-id="e6397-342">Tıklatın **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e6397-342">Click **+ Add**.</span></span> <span data-ttu-id="e6397-343">Arama hello Market için **yük dengeleyici**.</span><span class="sxs-lookup"><span data-stu-id="e6397-343">Search hello Marketplace for **Load Balancer**.</span></span> <span data-ttu-id="e6397-344">Tıklatın **yük dengeleyici**.</span><span class="sxs-lookup"><span data-stu-id="e6397-344">Click **Load Balancer**.</span></span>

1. <span data-ttu-id="e6397-345">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e6397-345">Click **Create**.</span></span>

1. <span data-ttu-id="e6397-346">Merhaba yük dengeleyici ile yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="e6397-346">Configure hello load balancer with:</span></span>

   - <span data-ttu-id="e6397-347">**Ad**: hello yük dengeleyici tanımlayan bir ad.</span><span class="sxs-lookup"><span data-stu-id="e6397-347">**Name**: A name that identifies hello load balancer.</span></span>
   - <span data-ttu-id="e6397-348">**Tür**: hello yük dengeleyici, genel veya özel olabilir.</span><span class="sxs-lookup"><span data-stu-id="e6397-348">**Type**: hello load balancer can be either public or private.</span></span> <span data-ttu-id="e6397-349">Özel yük dengeleyici içinden erişilebilir aynı sanal ağı hello.</span><span class="sxs-lookup"><span data-stu-id="e6397-349">A private load balancer can be accessed from within hello same VNET.</span></span> <span data-ttu-id="e6397-350">Çoğu Azure uygulamaları özel yük dengeleyici kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6397-350">Most Azure applications can use a private load balancer.</span></span> <span data-ttu-id="e6397-351">Uygulamanızı hello Internet üzerinden doğrudan erişim tooSQL sunucu gerekiyorsa, bir genel yük dengeleyiciye kullanın.</span><span class="sxs-lookup"><span data-stu-id="e6397-351">If your application needs access tooSQL Server directly over hello Internet, use a public load balancer.</span></span>
   - <span data-ttu-id="e6397-352">**Sanal ağ**: aynı ağ hello sanal makine olarak hello.</span><span class="sxs-lookup"><span data-stu-id="e6397-352">**Virtual Network**: hello same network as hello virtual machines.</span></span>
   - <span data-ttu-id="e6397-353">**Alt ağ**: Merhaba hello sanal makineler aynı alt ağda.</span><span class="sxs-lookup"><span data-stu-id="e6397-353">**Subnet**: hello same subnet as hello virtual machines.</span></span>
   - <span data-ttu-id="e6397-354">**Özel IP adresi**: Merhaba toohello SQL Server FCI küme ağ kaynağı atanmış aynı IP adresi.</span><span class="sxs-lookup"><span data-stu-id="e6397-354">**Private IP address**: hello same IP address that you assigned toohello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="e6397-355">**Abonelik**: bilgisayarınızı Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="e6397-355">**subscription**: Your Azure subscription.</span></span>
   - <span data-ttu-id="e6397-356">**Kaynak grubu**: kullanım hello aynı kaynak grubu, sanal makineleriniz olarak.</span><span class="sxs-lookup"><span data-stu-id="e6397-356">**Resource Group**: Use hello same resource group as your virtual machines.</span></span>
   - <span data-ttu-id="e6397-357">**Konum**: kullanım hello aynı sanal makinelerinizi olarak Azure konumu.</span><span class="sxs-lookup"><span data-stu-id="e6397-357">**Location**: Use hello same Azure location as your virtual machines.</span></span>
   <span data-ttu-id="e6397-358">Resim aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="e6397-358">See hello following picture:</span></span>

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a><span data-ttu-id="e6397-360">Merhaba yük dengeleyici arka uç havuzunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e6397-360">Configure hello load balancer backend pool</span></span>

1. <span data-ttu-id="e6397-361">Toohello Azure kaynak grubu hello sanal makinelerle dönün ve hello Yeni Yük Dengeleyici bulun.</span><span class="sxs-lookup"><span data-stu-id="e6397-361">Return toohello Azure Resource Group with hello virtual machines and locate hello new load balancer.</span></span> <span data-ttu-id="e6397-362">Toorefresh hello görünüm olabilir hello kaynak grubu üzerinde.</span><span class="sxs-lookup"><span data-stu-id="e6397-362">You may have toorefresh hello view on hello Resource Group.</span></span> <span data-ttu-id="e6397-363">Merhaba yük dengeleyici'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e6397-363">Click hello load balancer.</span></span>

1. <span data-ttu-id="e6397-364">Merhaba yük dengeleyici dikey penceresinde **arka uç havuzları**.</span><span class="sxs-lookup"><span data-stu-id="e6397-364">On hello load balancer blade, click **Backend pools**.</span></span>

1. <span data-ttu-id="e6397-365">Tıklatın **+ Ekle** tooadd bir arka uç havuzu.</span><span class="sxs-lookup"><span data-stu-id="e6397-365">Click **+ Add** tooadd a backend pool.</span></span>

1. <span data-ttu-id="e6397-366">Merhaba arka uç havuzu için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="e6397-366">Type a name for hello backend pool.</span></span>

1. <span data-ttu-id="e6397-367">Tıklatın **bir sanal makine Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e6397-367">Click **Add a virtual machine**.</span></span>

1. <span data-ttu-id="e6397-368">Merhaba üzerinde **sanal makineleri seçin** dikey penceresinde tıklatın **bir kullanılabilirlik kümesi seçin**.</span><span class="sxs-lookup"><span data-stu-id="e6397-368">On hello **Choose virtual machines** blade, click **Choose an availability set**.</span></span>

1. <span data-ttu-id="e6397-369">Merhaba SQL Server sanal makinelerinizde yerleştirilen Hello kullanılabilirlik kümesi'ni seçin.</span><span class="sxs-lookup"><span data-stu-id="e6397-369">Choose hello availability set that you placed hello SQL Server virtual machines in.</span></span>

1. <span data-ttu-id="e6397-370">Merhaba üzerinde **sanal makineleri seçin** dikey penceresinde tıklatın **hello sanal makineleri seçin**.</span><span class="sxs-lookup"><span data-stu-id="e6397-370">On hello **Choose virtual machines** blade, click **Choose hello virtual machines**.</span></span>

   <span data-ttu-id="e6397-371">Azure portal'ınızın hello resim aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="e6397-371">Your Azure portal should look like hello following picture:</span></span>

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. <span data-ttu-id="e6397-373">Tıklatın **seçin** hello üzerinde **sanal makineleri seçin** dikey.</span><span class="sxs-lookup"><span data-stu-id="e6397-373">Click **Select** on hello **Choose virtual machines** blade.</span></span>

1. <span data-ttu-id="e6397-374">Tıklatın **Tamam** iki kez.</span><span class="sxs-lookup"><span data-stu-id="e6397-374">Click **OK** twice.</span></span>

### <a name="configure-a-load-balancer-health-probe"></a><span data-ttu-id="e6397-375">Bir yük dengeleyici durum araştırması yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e6397-375">Configure a load balancer health probe</span></span>

1. <span data-ttu-id="e6397-376">Merhaba yük dengeleyici dikey penceresinde **sistem durumu araştırmalarının**.</span><span class="sxs-lookup"><span data-stu-id="e6397-376">On hello load balancer blade, click **Health probes**.</span></span>

1. <span data-ttu-id="e6397-377">Tıklatın **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e6397-377">Click **+ Add**.</span></span>

1. <span data-ttu-id="e6397-378">Merhaba üzerinde **Ekle durumu araştırması** dikey penceresinde <a name="probe"> </a>Set hello sistem durumu araştırma Parametreler:</span><span class="sxs-lookup"><span data-stu-id="e6397-378">On hello **Add health probe** blade, <a name="probe"></a>Set hello health probe parameters:</span></span>

   - <span data-ttu-id="e6397-379">**Ad**: hello durumu araştırması için bir ad.</span><span class="sxs-lookup"><span data-stu-id="e6397-379">**Name**: A name for hello health probe.</span></span>
   - <span data-ttu-id="e6397-380">**Protokol**: TCP.</span><span class="sxs-lookup"><span data-stu-id="e6397-380">**Protocol**: TCP.</span></span>
   - <span data-ttu-id="e6397-381">**Bağlantı noktası**: tooan kullanılabilir TCP bağlantı noktası ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e6397-381">**Port**: Set tooan available TCP port.</span></span> <span data-ttu-id="e6397-382">Bu bağlantı noktası açık güvenlik duvarı bağlantı noktası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e6397-382">This port requires an open firewall port.</span></span> <span data-ttu-id="e6397-383">Kullanım hello [aynı bağlantı noktasını](#ports) hello güvenlik duvarında hello sistem durumu araştırması için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e6397-383">Use hello [same port](#ports) you set for hello health probe at hello firewall.</span></span>
   - <span data-ttu-id="e6397-384">**Aralığı**: 5 saniye.</span><span class="sxs-lookup"><span data-stu-id="e6397-384">**Interval**: 5 Seconds.</span></span>
   - <span data-ttu-id="e6397-385">**Sağlıksız eşik**: 2 art arda hatalar.</span><span class="sxs-lookup"><span data-stu-id="e6397-385">**Unhealthy threshold**: 2 consecutive failures.</span></span>

1. <span data-ttu-id="e6397-386">Tamam'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e6397-386">Click OK.</span></span>

### <a name="set-load-balancing-rules"></a><span data-ttu-id="e6397-387">Yük Dengeleme kuralları ayarlama</span><span class="sxs-lookup"><span data-stu-id="e6397-387">Set load balancing rules</span></span>

1. <span data-ttu-id="e6397-388">Merhaba yük dengeleyici dikey penceresinde **Yük Dengeleme kuralları**.</span><span class="sxs-lookup"><span data-stu-id="e6397-388">On hello load balancer blade, click **Load balancing rules**.</span></span>

1. <span data-ttu-id="e6397-389">Tıklatın **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e6397-389">Click **+ Add**.</span></span>

1. <span data-ttu-id="e6397-390">Merhaba Yük Dengeleme kuralları parametrelerini ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="e6397-390">Set hello load balancing rules parameters:</span></span>

   - <span data-ttu-id="e6397-391">**Ad**: hello Yük Dengeleme kuralları için bir ad.</span><span class="sxs-lookup"><span data-stu-id="e6397-391">**Name**: A name for hello load balancing rules.</span></span>
   - <span data-ttu-id="e6397-392">**Ön uç IP adresi**: SQL Server FCI küme ağ kaynağı hello için başlangıç IP adresi kullanın.</span><span class="sxs-lookup"><span data-stu-id="e6397-392">**Frontend IP address**: Use hello IP address for hello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="e6397-393">**Bağlantı noktası**: Merhaba SQL Server FCI TCP bağlantı noktası ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e6397-393">**Port**: Set for hello SQL Server FCI TCP port.</span></span> <span data-ttu-id="e6397-394">Merhaba varsayılan örnek bağlantı noktası 1433'tür.</span><span class="sxs-lookup"><span data-stu-id="e6397-394">hello default instance port is 1433.</span></span>
   - <span data-ttu-id="e6397-395">**Arka uç bağlantı noktası**: Bu değer aynı bağlantı noktası hello hello kullanan **bağlantı noktası** değeri, etkinleştirdiğinizde **kayan IP (doğrudan sunucu dönüşü)**.</span><span class="sxs-lookup"><span data-stu-id="e6397-395">**Backend port**: This value uses hello same port as hello **Port** value when you enable **Floating IP (direct server return)**.</span></span>
   - <span data-ttu-id="e6397-396">**Arka uç havuzu**: daha önce yapılandırılmış hello arka uç havuzu adını kullan.</span><span class="sxs-lookup"><span data-stu-id="e6397-396">**Backend pool**: Use hello backend pool name that you configured earlier.</span></span>
   - <span data-ttu-id="e6397-397">**Sistem durumu araştırma**: daha önce yapılandırılmış hello durumu araştırması kullanın.</span><span class="sxs-lookup"><span data-stu-id="e6397-397">**Health probe**: Use hello health probe that you configured earlier.</span></span>
   - <span data-ttu-id="e6397-398">**Oturum kalıcılığı**: yok.</span><span class="sxs-lookup"><span data-stu-id="e6397-398">**Session persistence**: None.</span></span>
   - <span data-ttu-id="e6397-399">**Boşta kalma zaman aşımı (dakika)**: 4.</span><span class="sxs-lookup"><span data-stu-id="e6397-399">**Idle timeout (minutes)**: 4.</span></span>
   - <span data-ttu-id="e6397-400">**Kayan IP (doğrudan sunucu dönüşü)**: etkin</span><span class="sxs-lookup"><span data-stu-id="e6397-400">**Floating IP (direct server return)**: Enabled</span></span>

1. <span data-ttu-id="e6397-401">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e6397-401">Click **OK**.</span></span>

## <a name="step-6-configure-cluster-for-probe"></a><span data-ttu-id="e6397-402">Adım 6: küme araştırma için yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e6397-402">Step 6: Configure cluster for probe</span></span>

<span data-ttu-id="e6397-403">Merhaba küme araştırma port parametresi PowerShell'de ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e6397-403">Set hello cluster probe port parameter in PowerShell.</span></span>

<span data-ttu-id="e6397-404">tooset küme araştırma port parametresi Merhaba, ortamınızdan komut dosyası izleyen hello değişkenlerde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e6397-404">tooset hello cluster probe port parameter, update variables in hello following script from your environment.</span></span>

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a><span data-ttu-id="e6397-405">7. adım: Test FCI yük devretme</span><span class="sxs-lookup"><span data-stu-id="e6397-405">Step 7: Test FCI failover</span></span>

<span data-ttu-id="e6397-406">Merhaba FCI toovalidate küme işlevselliğini yük devretme sınamasını.</span><span class="sxs-lookup"><span data-stu-id="e6397-406">Test failover of hello FCI toovalidate cluster functionality.</span></span> <span data-ttu-id="e6397-407">Adımları hello:</span><span class="sxs-lookup"><span data-stu-id="e6397-407">Do hello following steps:</span></span>

1. <span data-ttu-id="e6397-408">Merhaba SQL Server FCI küme düğümlerinin tooone RDP ile bağlanır.</span><span class="sxs-lookup"><span data-stu-id="e6397-408">Connect tooone of hello SQL Server FCI cluster nodes with RDP.</span></span>

1. <span data-ttu-id="e6397-409">Açık **yük devretme kümesi Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="e6397-409">Open **Failover Cluster Manager**.</span></span> <span data-ttu-id="e6397-410">Tıklatın **rolleri**.</span><span class="sxs-lookup"><span data-stu-id="e6397-410">Click **Roles**.</span></span> <span data-ttu-id="e6397-411">Merhaba SQL Server FCI rol sahibi olan düğümü dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e6397-411">Notice which node owns hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="e6397-412">Merhaba SQL Server FCI role sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e6397-412">Right-click hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="e6397-413">Tıklatın **taşıma** tıklatıp **olası iyi düğüme**.</span><span class="sxs-lookup"><span data-stu-id="e6397-413">Click **Move** and click **Best Possible Node**.</span></span>

<span data-ttu-id="e6397-414">**Yük Devretme Kümesi Yöneticisi** gösterir hello rolü ve kaynaklarını çevrimdışı.</span><span class="sxs-lookup"><span data-stu-id="e6397-414">**Failover Cluster Manager** shows hello role and its resources go offline.</span></span> <span data-ttu-id="e6397-415">Merhaba kaynakları sonra taşıyın ve çevrimiçi duruma açık, başka bir düğüme hello.</span><span class="sxs-lookup"><span data-stu-id="e6397-415">hello resources then move and come online on hello other node.</span></span>

### <a name="test-connectivity"></a><span data-ttu-id="e6397-416">Bağlantıyı test etme</span><span class="sxs-lookup"><span data-stu-id="e6397-416">Test connectivity</span></span>

<span data-ttu-id="e6397-417">tootest bağlantısı, hello tooanother sanal makinede günlüğüne aynı sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="e6397-417">tootest connectivity, log in tooanother virtual machine in hello same virtual network.</span></span> <span data-ttu-id="e6397-418">Açık **SQL Server Management Studio** ve toohello SQL Server FCI adı bağlanın.</span><span class="sxs-lookup"><span data-stu-id="e6397-418">Open **SQL Server Management Studio** and connect toohello SQL Server FCI name.</span></span>

>[!NOTE]
><span data-ttu-id="e6397-419">Gerekirse, aşağıdakileri yapabilirsiniz, [SQL Server Management Studio'yu indirme](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="e6397-419">If necessary, you can [download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="limitations"></a><span data-ttu-id="e6397-420">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="e6397-420">Limitations</span></span>
<span data-ttu-id="e6397-421">Azure sanal makinelerde Hello RPC bağlantı noktası hello yük dengeleyici tarafından desteklenmediği için Microsoft Dağıtılmış İşlem Düzenleyicisi (DTC) Fcı'lerde üzerinde desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="e6397-421">On Azure virtual machines, Microsoft Distributed Transaction Coordinator (DTC) is not supported on FCIs because hello RPC port is not supported by hello load balancer.</span></span>

## <a name="see-also"></a><span data-ttu-id="e6397-422">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="e6397-422">See Also</span></span>

[<span data-ttu-id="e6397-423">Uzak Masaüstü'nü (Azure) S2D Kurulumu</span><span class="sxs-lookup"><span data-stu-id="e6397-423">Setup S2D with remote desktop (Azure)</span></span>](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

<span data-ttu-id="e6397-424">[Depolama alanları doğrudan ile çözüm Hyper yakınsanmış](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="e6397-424">[Hyper-converged solution with storage spaces direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span></span>

[<span data-ttu-id="e6397-425">Depolama alanına doğrudan genel bakış</span><span class="sxs-lookup"><span data-stu-id="e6397-425">Storage Space Direct Overview</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[<span data-ttu-id="e6397-426">S2D için SQL Server desteği</span><span class="sxs-lookup"><span data-stu-id="e6397-426">SQL Server support for S2D</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
