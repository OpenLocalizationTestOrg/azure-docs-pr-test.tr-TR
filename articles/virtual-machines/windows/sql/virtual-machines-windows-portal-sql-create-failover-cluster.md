---
title: SQL Server FCI - Azure sanal makineleri | Microsoft Docs
description: "Bu makalede Azure sanal makinelerde SQL Server Yük devretme kümesi örneği oluşturma açıklanmaktadır."
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
ms.openlocfilehash: 439353b7d22fb7376049ea8e1433a8d5840d3e0f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a><span data-ttu-id="56e97-103">SQL Server Yük devretme kümesi örneği üzerinde Azure sanal makineleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="56e97-103">Configure SQL Server Failover Cluster Instance on Azure Virtual Machines</span></span>

<span data-ttu-id="56e97-104">Bu makalede, Resource Manager modelinde Azure sanal makinelerde bir SQL Server Yük devretme kümesi örneği (FCI) oluşturma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="56e97-104">This article explains how to create a SQL Server Failover Cluster Instance (FCI) on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="56e97-105">Bu çözümü kullanan [depolama alanları doğrudan Windows Server 2016 Datacenter edition \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) Windows kümesi (Azure VM) düğümleri arasında (veri diskleri) depolama eşitleyen bir yazılım tabanlı sanal SAN olarak.</span><span class="sxs-lookup"><span data-stu-id="56e97-105">This solution uses [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) as a software-based virtual SAN that synchronizes the storage (data disks) between the nodes (Azure VMs) in a Windows Cluster.</span></span> <span data-ttu-id="56e97-106">S2D, Windows Server 2016'da yeni bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="56e97-106">S2D is new in Windows Server 2016.</span></span>

<span data-ttu-id="56e97-107">Aşağıdaki diyagramda, Azure sanal makinelerde eksiksiz çözüm gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="56e97-107">The following diagram shows the complete solution on Azure virtual machines:</span></span>

![Kullanılabilirlik grubu](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

<span data-ttu-id="56e97-109">Önceki diyagramda gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="56e97-109">The preceding diagram shows:</span></span>

- <span data-ttu-id="56e97-110">İki Azure sanal makinelerinde Windows Yük devretme kümesi.</span><span class="sxs-lookup"><span data-stu-id="56e97-110">Two Azure virtual machines in a Windows Failover Cluster.</span></span> <span data-ttu-id="56e97-111">Bir sanal makine bir yük devretme kümesinde olduğunda da adlandırılır bir *küme düğümü*, veya *düğümleri*.</span><span class="sxs-lookup"><span data-stu-id="56e97-111">When a virtual machine is in a failover cluster it is also called a *cluster node*, or *nodes*.</span></span>
- <span data-ttu-id="56e97-112">Her sanal makinenin iki veya daha fazla veri diski var.</span><span class="sxs-lookup"><span data-stu-id="56e97-112">Each virtual machine has two or more data disks.</span></span>
- <span data-ttu-id="56e97-113">S2D verileri diskteki verileri eşitler ve bir depolama havuzu olarak eşitlenmiş depolama sunar.</span><span class="sxs-lookup"><span data-stu-id="56e97-113">S2D synchronizes the data on the data disk and presents the synchronized storage as a storage pool.</span></span>
- <span data-ttu-id="56e97-114">Depolama havuzu ve yük devretme kümesine Küme Paylaşılan birimi (CSV) gösterir.</span><span class="sxs-lookup"><span data-stu-id="56e97-114">The storage pool presents a cluster shared volume (CSV) to the failover cluster.</span></span>
- <span data-ttu-id="56e97-115">SQL Server FCI küme rolünü CSV veri sürücüleri için kullanır.</span><span class="sxs-lookup"><span data-stu-id="56e97-115">The SQL Server FCI cluster role uses the CSV for the data drives.</span></span>
- <span data-ttu-id="56e97-116">IP adresi için SQL Server FCI tutmak için bir Azure yük dengeleyici.</span><span class="sxs-lookup"><span data-stu-id="56e97-116">An Azure load balancer to hold the IP address for the SQL Server FCI.</span></span>
- <span data-ttu-id="56e97-117">Bir Azure kullanılabilirlik kümesi tüm kaynakları tutar.</span><span class="sxs-lookup"><span data-stu-id="56e97-117">An Azure availability set holds all the resources.</span></span>

   >[!NOTE]
   ><span data-ttu-id="56e97-118">Tüm Azure diyagramda kaynaklardır aynı kaynak grubunda yer alan.</span><span class="sxs-lookup"><span data-stu-id="56e97-118">All Azure resources are in the diagram are in the same resource group.</span></span>

<span data-ttu-id="56e97-119">S2D hakkında daha fazla ayrıntı için bkz: [depolama alanları doğrudan Windows Server 2016 Datacenter edition \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span><span class="sxs-lookup"><span data-stu-id="56e97-119">For details about S2D, see [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span></span>

<span data-ttu-id="56e97-120">S2D mimarileri - yakınsanmış ve hiper yakınsanmış iki türlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="56e97-120">S2D supports two types of architectures - converged and hyper-converged.</span></span> <span data-ttu-id="56e97-121">Bu belgedeki hiper yakınsanmış bir mimaridir.</span><span class="sxs-lookup"><span data-stu-id="56e97-121">The architecture in this document is hyper-converged.</span></span> <span data-ttu-id="56e97-122">Hiper yakınsanmış bir altyapı depolama kümelenmiş uygulama ana bilgisayar aynı sunuculara yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="56e97-122">A hyper-converged infrastructure places the storage on the same servers that host the clustered application.</span></span> <span data-ttu-id="56e97-123">Bu mimaride, depolama, üzerinde her SQL Server FCI düğümdür.</span><span class="sxs-lookup"><span data-stu-id="56e97-123">In this architecture, the storage is on each SQL Server FCI node.</span></span>

### <a name="example-azure-template"></a><span data-ttu-id="56e97-124">Örnek Azure şablonu</span><span class="sxs-lookup"><span data-stu-id="56e97-124">Example Azure template</span></span>

<span data-ttu-id="56e97-125">Çözümün tamamında Azure'da bir şablondan oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56e97-125">You can create the entire solution in Azure from a template.</span></span> <span data-ttu-id="56e97-126">Şablon örneği Github'da kullanılabilir [Azure hızlı başlangıç şablonlarını](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span><span class="sxs-lookup"><span data-stu-id="56e97-126">An example of a template is available in the GitHub [Azure Quickstart Templates](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span></span> <span data-ttu-id="56e97-127">Bu örnekte değil tasarlanmış veya belirli bir iş yükü için test.</span><span class="sxs-lookup"><span data-stu-id="56e97-127">This example is not designed or tested for any specific workload.</span></span> <span data-ttu-id="56e97-128">Etki alanınıza bağlı S2D depolama ile bir SQL Server FCI oluşturmak için şablon çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56e97-128">You can run the template to create a SQL Server FCI with S2D storage connected to your domain.</span></span> <span data-ttu-id="56e97-129">Şablon değerlendirin ve amaçlarınız için değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56e97-129">You can evaluate the template, and modify it for your purposes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="56e97-130">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="56e97-130">Before you begin</span></span>

<span data-ttu-id="56e97-131">Bilmeniz gereken birkaç şey ve, önce yerinde devam şunları vardır.</span><span class="sxs-lookup"><span data-stu-id="56e97-131">There are a few things you need to know and a couple of things that you need in place before you proceed.</span></span>

### <a name="what-to-know"></a><span data-ttu-id="56e97-132">Bilinmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="56e97-132">What to know</span></span>
<span data-ttu-id="56e97-133">Aşağıdaki teknolojileri işletimsel bir anlamış olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="56e97-133">You should have an operational understanding of the following technologies:</span></span>

- [<span data-ttu-id="56e97-134">Windows Küme teknolojileri</span><span class="sxs-lookup"><span data-stu-id="56e97-134">Windows cluster technologies</span></span>](http://technet.microsoft.com/library/hh831579.aspx)
-  <span data-ttu-id="56e97-135">[SQL Server Yük devretme kümesi örnekleri](http://msdn.microsoft.com/library/ms189134.aspx).</span><span class="sxs-lookup"><span data-stu-id="56e97-135">[SQL Server Failover Cluster Instances](http://msdn.microsoft.com/library/ms189134.aspx).</span></span>

<span data-ttu-id="56e97-136">Ayrıca, aşağıdaki teknolojileri genel bir anlamış olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="56e97-136">Also, you should have a general understanding of the following technologies:</span></span>

- [<span data-ttu-id="56e97-137">Depolama alanları doğrudan Windows Server 2016 kullanarak Hyper-yakınsanmış çözüm</span><span class="sxs-lookup"><span data-stu-id="56e97-137">Hyper-converged solution using Storage Spaces Direct in Windows Server 2016</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [<span data-ttu-id="56e97-138">Azure kaynak grupları</span><span class="sxs-lookup"><span data-stu-id="56e97-138">Azure resource groups</span></span>](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-to-have"></a><span data-ttu-id="56e97-139">Ne sağlamak için</span><span class="sxs-lookup"><span data-stu-id="56e97-139">What to have</span></span>

<span data-ttu-id="56e97-140">Bu makaledeki yönergeleri izlemeden önce olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="56e97-140">Before following the instructions in this article, you should already have:</span></span>

- <span data-ttu-id="56e97-141">Microsoft Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="56e97-141">A Microsoft Azure subscription.</span></span>
- <span data-ttu-id="56e97-142">Bir Windows etki alanı Azure sanal makinelerde.</span><span class="sxs-lookup"><span data-stu-id="56e97-142">A Windows domain on Azure virtual machines.</span></span>
- <span data-ttu-id="56e97-143">Azure sanal makinede nesneleri oluşturma izni olan bir hesap.</span><span class="sxs-lookup"><span data-stu-id="56e97-143">An account with permission to create objects in the Azure virtual machine.</span></span>
- <span data-ttu-id="56e97-144">Bir Azure sanal ağ ve alt yeterli IP adres alanı aşağıdaki bileşenler için:</span><span class="sxs-lookup"><span data-stu-id="56e97-144">An Azure virtual network and subnet with sufficient IP address space for the following components:</span></span>
   - <span data-ttu-id="56e97-145">Her iki sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="56e97-145">Both virtual machines.</span></span>
   - <span data-ttu-id="56e97-146">Yük devretme küme IP adresi.</span><span class="sxs-lookup"><span data-stu-id="56e97-146">The failover cluster IP address.</span></span>
   - <span data-ttu-id="56e97-147">Her FCI için bir IP adresi.</span><span class="sxs-lookup"><span data-stu-id="56e97-147">An IP address for each FCI.</span></span>
- <span data-ttu-id="56e97-148">DNS etki alanı denetleyicilerine işaret eden Azure ağ üzerinde yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="56e97-148">DNS configured on the Azure Network, pointing to the domain controllers.</span></span>

<span data-ttu-id="56e97-149">Bu önkoşulları yerine getirilince, yük devretme kümesi oluşturmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56e97-149">With these prerequisites in place, you can proceed with building your failover cluster.</span></span> <span data-ttu-id="56e97-150">Sanal makineler oluşturmak için ilk adımdır bakın.</span><span class="sxs-lookup"><span data-stu-id="56e97-150">The first step is to create the virtual machines.</span></span>

## <a name="step-1-create-virtual-machines"></a><span data-ttu-id="56e97-151">1. adım: sanal makineler oluşturma</span><span class="sxs-lookup"><span data-stu-id="56e97-151">Step 1: Create virtual machines</span></span>

1. <span data-ttu-id="56e97-152">Oturum [Azure portal](http://portal.azure.com) aboneliğinizle.</span><span class="sxs-lookup"><span data-stu-id="56e97-152">Log in to the [Azure portal](http://portal.azure.com) with your subscription.</span></span>

1. <span data-ttu-id="56e97-153">[Azure kullanılabilirlik kümesi oluştur](../tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="56e97-153">[Create an Azure availability set](../tutorial-availability-sets.md).</span></span>

   <span data-ttu-id="56e97-154">Kullanılabilirlik grupları sanal makineleri hata etki alanlarında ayarlayın ve güncelleme etki alanları.</span><span class="sxs-lookup"><span data-stu-id="56e97-154">The availability set groups virtual machines across fault domains and update domains.</span></span> <span data-ttu-id="56e97-155">Kullanılabilirlik kümesi, uygulamanızın tek hata noktaları, ağ anahtarı veya güç ünitesi bir sunucu rafı gibi etkilenmez emin olur.</span><span class="sxs-lookup"><span data-stu-id="56e97-155">The availability set makes sure that your application is not affected by single points of failure, like the network switch or the power unit of a rack of servers.</span></span>

   <span data-ttu-id="56e97-156">Sanal makineleriniz için kaynak grubu oluşturmadıysanız, bunu bir Azure kullanılabilirlik kümesi oluşturduğunuzda.</span><span class="sxs-lookup"><span data-stu-id="56e97-156">If you have not created the resource group for your virtual machines, do it when you create an Azure availability set.</span></span> <span data-ttu-id="56e97-157">Kullanılabilirlik kümesi oluşturmak için Azure portalını kullanıyorsanız, aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="56e97-157">If you're using the Azure portal to create the availability set, do the following steps:</span></span>

   - <span data-ttu-id="56e97-158">Azure portalında tıklatın  **+**  Azure Marketi açın.</span><span class="sxs-lookup"><span data-stu-id="56e97-158">In the Azure portal, click **+** to open the Azure Marketplace.</span></span> <span data-ttu-id="56e97-159">Arama **kullanılabilirlik kümesi**.</span><span class="sxs-lookup"><span data-stu-id="56e97-159">Search for **Availability set**.</span></span>
   - <span data-ttu-id="56e97-160">Tıklatın **kullanılabilirlik kümesi**.</span><span class="sxs-lookup"><span data-stu-id="56e97-160">Click **Availability set**.</span></span>
   - <span data-ttu-id="56e97-161">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="56e97-161">Click **Create**.</span></span>
   - <span data-ttu-id="56e97-162">Üzerinde **kullanılabilirlik kümesi oluştur** dikey penceresinde, aşağıdaki değerleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="56e97-162">On the **Create availability set** blade, set the following values:</span></span>
      - <span data-ttu-id="56e97-163">**Ad**: kullanılabilirlik kümesi için bir ad.</span><span class="sxs-lookup"><span data-stu-id="56e97-163">**Name**: A name for the availability set.</span></span>
      - <span data-ttu-id="56e97-164">**Abonelik**: bilgisayarınızı Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="56e97-164">**Subscription**: Your Azure subscription.</span></span>
      - <span data-ttu-id="56e97-165">**Kaynak grubu**: varolan bir grubu kullanmak istiyorsanız, tıklatın **var olanı kullan** ve Grup aşağı açılan listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="56e97-165">**Resource group**: If you want to use an existing group, click **Use existing** and select the group from the drop-down list.</span></span> <span data-ttu-id="56e97-166">Seçmediğiniz **Yeni Oluştur** ve grup için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="56e97-166">Otherwise choose **Create New** and type a name for the group.</span></span>
      - <span data-ttu-id="56e97-167">**Konum**: sanal makinelerinizi oluştururken planladığınız konumunu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="56e97-167">**Location**: Set the location where you plan to create your virtual machines.</span></span>
      - <span data-ttu-id="56e97-168">**Hata etki alanları**: varsayılan (3) kullanın.</span><span class="sxs-lookup"><span data-stu-id="56e97-168">**Fault domains**: Use the default (3).</span></span>
      - <span data-ttu-id="56e97-169">**Güncelleme etki alanları**: varsayılan (5) kullanın.</span><span class="sxs-lookup"><span data-stu-id="56e97-169">**Update domains**: Use the default (5).</span></span>
   - <span data-ttu-id="56e97-170">Tıklatın **oluşturma** kullanılabilirlik oluşturmak için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="56e97-170">Click **Create** to create the availability set.</span></span>

1. <span data-ttu-id="56e97-171">Sanal makineler kullanılabilirlik kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="56e97-171">Create the virtual machines in the availability set.</span></span>

   <span data-ttu-id="56e97-172">Azure kullanılabilirlik kümesinde iki SQL Server sanal makine sağlayın.</span><span class="sxs-lookup"><span data-stu-id="56e97-172">Provision two SQL Server virtual machines in the Azure availability set.</span></span> <span data-ttu-id="56e97-173">Yönergeler için bkz: [Azure portalında bir SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="56e97-173">For instructions, see [Provision a SQL Server virtual machine in the Azure portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

   <span data-ttu-id="56e97-174">Her iki sanal makine koyun:</span><span class="sxs-lookup"><span data-stu-id="56e97-174">Place both virtual machines:</span></span>

   - <span data-ttu-id="56e97-175">Aynı Azure, kullanılabilirlik kümesi kaynak grubu değil.</span><span class="sxs-lookup"><span data-stu-id="56e97-175">In the same Azure resource group that your availability set is in.</span></span>
   - <span data-ttu-id="56e97-176">Etki alanı denetleyicisi olarak aynı ağ üzerinde.</span><span class="sxs-lookup"><span data-stu-id="56e97-176">On the same network as your domain controller.</span></span>
   - <span data-ttu-id="56e97-177">Sanal makineler hem bu kümede sonunda kullanabilir tüm Fcı'lerde için yeterli IP adres alanı ile bir alt ağ üzerinde.</span><span class="sxs-lookup"><span data-stu-id="56e97-177">On a subnet with sufficient IP address space for both virtual machines, and all FCIs that you may eventually use on this cluster.</span></span>
   - <span data-ttu-id="56e97-178">Azure kullanılabilirlik kümesinde.</span><span class="sxs-lookup"><span data-stu-id="56e97-178">In the Azure availability set.</span></span>   

      >[!IMPORTANT]
      ><span data-ttu-id="56e97-179">Ayarlayın veya bir sanal makine oluşturulduktan sonra ayarlanmış kullanılabilirlik değiştirin.</span><span class="sxs-lookup"><span data-stu-id="56e97-179">You cannot set or change availability set after a virtual machine has been created.</span></span>

   <span data-ttu-id="56e97-180">Azure Marketi'nde bir görüntü seçin.</span><span class="sxs-lookup"><span data-stu-id="56e97-180">Choose an image from the Azure Marketplace.</span></span> <span data-ttu-id="56e97-181">Bir Market kullanabilirsiniz, görüntü, Windows Server ve SQL Server ya da yalnızca Windows Server içerir.</span><span class="sxs-lookup"><span data-stu-id="56e97-181">You can use a Marketplace image with that includes Windows Server and SQL Server, or just the Windows Server.</span></span> <span data-ttu-id="56e97-182">Ayrıntılar için bkz [genel bakış SQL Server'ın Azure sanal makineler üzerinde](../../virtual-machines-windows-sql-server-iaas-overview.md)</span><span class="sxs-lookup"><span data-stu-id="56e97-182">For details, see [Overview of SQL Server on Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)</span></span>

   <span data-ttu-id="56e97-183">Resmi SQL Server görüntülerini Azure galerisinde yüklü SQL Server örneğini ve SQL Server yükleme yazılım ve gereken anahtar içerir.</span><span class="sxs-lookup"><span data-stu-id="56e97-183">The official SQL Server images in the Azure Gallery include an installed SQL Server instance, plus the SQL Server installation software, and the required key.</span></span>

   <span data-ttu-id="56e97-184">SQL Server Lisans için ödeme yapmak istediğiniz nasıl göre uygun görüntüyü seçin:</span><span class="sxs-lookup"><span data-stu-id="56e97-184">Choose the right image according to how you want to pay for the SQL Server license:</span></span>

   - <span data-ttu-id="56e97-185">**Kullanım lisansı başına ödeme**: SQL Server Lisansı bu görüntülerin dakika başına maliyet içerir:</span><span class="sxs-lookup"><span data-stu-id="56e97-185">**Pay per usage licensing**: The per-minute cost of these images includes the SQL Server licensing:</span></span>
      - <span data-ttu-id="56e97-186">**Windows Server Datacenter 2016 üzerinde SQL Server 2016 Enterprise**</span><span class="sxs-lookup"><span data-stu-id="56e97-186">**SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="56e97-187">**Windows Server Datacenter 2016 SQL Server 2016 standardı**</span><span class="sxs-lookup"><span data-stu-id="56e97-187">**SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="56e97-188">**Windows Server Datacenter 2016 SQL Server 2016 Geliştirici**</span><span class="sxs-lookup"><span data-stu-id="56e97-188">**SQL Server 2016 Developer on Windows Server Datacenter 2016**</span></span>

   - <span data-ttu-id="56e97-189">**Getir bilgisayarınızı-kendi-lisans (KLG)**</span><span class="sxs-lookup"><span data-stu-id="56e97-189">**Bring-your-own-license (BYOL)**</span></span>

      - <span data-ttu-id="56e97-190">**{KLG} Windows Server Datacenter 2016 üzerinde SQL Server 2016 Enterprise**</span><span class="sxs-lookup"><span data-stu-id="56e97-190">**{BYOL} SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="56e97-191">**{KLG} Windows Server Datacenter 2016 SQL Server 2016 standardı**</span><span class="sxs-lookup"><span data-stu-id="56e97-191">**{BYOL} SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="56e97-192">Sanal makineyi oluşturduktan sonra önceden yüklenmiş tek başına SQL Server örneğini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="56e97-192">After you create the virtual machine, remove the pre-installed standalone SQL Server instance.</span></span> <span data-ttu-id="56e97-193">Yük devretme kümesi ve S2D yapılandırdıktan sonra SQL Server FCI oluşturmak için önceden yüklenmiş SQL Server medya kullanır.</span><span class="sxs-lookup"><span data-stu-id="56e97-193">You will use the pre-installed SQL Server media to create the SQL Server FCI after you configure the failover cluster and S2D.</span></span>

   <span data-ttu-id="56e97-194">Alternatif olarak, yalnızca işletim sistemi ile Azure Market görüntülerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56e97-194">Alternatively, you can use Azure Marketplace images with just the operating system.</span></span> <span data-ttu-id="56e97-195">Seçin bir **Windows Server 2016 Datacenter** görüntü ve yük devretme kümesi ve S2D yapılandırdıktan sonra SQL Server FCI yükleyin.</span><span class="sxs-lookup"><span data-stu-id="56e97-195">Choose a **Windows Server 2016 Datacenter** image and install the SQL Server FCI after you configure the failover cluster and S2D.</span></span> <span data-ttu-id="56e97-196">Bu görüntü, SQL Server yükleme medyasını içermiyor.</span><span class="sxs-lookup"><span data-stu-id="56e97-196">This image does not contain SQL Server installation media.</span></span> <span data-ttu-id="56e97-197">Yükleme medyasındaki her sunucu için SQL Server yüklemesi çalıştırdığı bir konuma yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="56e97-197">Place the installation media in a location where you can run the SQL Server installation for each server.</span></span>

1. <span data-ttu-id="56e97-198">Azure sanal makinelerinizi oluşturduktan sonra her sanal makinenin RDP ile bağlanır.</span><span class="sxs-lookup"><span data-stu-id="56e97-198">After Azure creates your virtual machines, connect to each virtual machine with RDP.</span></span>

   <span data-ttu-id="56e97-199">İlk RDP ile bir sanal makineye bağlandığınızda, bilgisayar bu Bilgisayara ağ üzerinde bulunabilir izin vermek isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="56e97-199">When you first connect to a virtual machine with RDP, the computer asks if you want to allow this PC to be discoverable on the network.</span></span> <span data-ttu-id="56e97-200">**Evet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="56e97-200">Click **Yes**.</span></span>

1. <span data-ttu-id="56e97-201">SQL Server tabanlı sanal makine görüntülerden birini kullanıyorsanız, SQL Server örneğini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="56e97-201">If you are using one of the SQL Server-based virtual machine images, remove the SQL Server instance.</span></span>

   - <span data-ttu-id="56e97-202">İçinde **programlar ve Özellikler**, sağ **Microsoft SQL Server 2016 (64 bit)** tıklatıp **Kaldır/Değiştir**.</span><span class="sxs-lookup"><span data-stu-id="56e97-202">In **Programs and Features**, right-click **Microsoft SQL Server 2016 (64-bit)** and click **Uninstall/Change**.</span></span>
   - <span data-ttu-id="56e97-203">Tıklatın **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="56e97-203">Click **Remove**.</span></span>
   - <span data-ttu-id="56e97-204">Varsayılan örneği seçin.</span><span class="sxs-lookup"><span data-stu-id="56e97-204">Select the default instance.</span></span>
   - <span data-ttu-id="56e97-205">Tüm Özellikleri'nin altında kaldırmak **veritabanı altyapısı Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="56e97-205">Remove all features under **Database Engine Services**.</span></span> <span data-ttu-id="56e97-206">Kaldırmayın **Paylaşılan Özellikler**.</span><span class="sxs-lookup"><span data-stu-id="56e97-206">Do not remove **Shared Features**.</span></span> <span data-ttu-id="56e97-207">Aşağıdaki resme bakın:</span><span class="sxs-lookup"><span data-stu-id="56e97-207">See the following picture:</span></span>

      ![Özellikleri Kaldır](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - <span data-ttu-id="56e97-209">Tıklatın **sonraki**ve ardından **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="56e97-209">Click **Next**, and then click **Remove**.</span></span>

1. <span data-ttu-id="56e97-210"><a name="ports"></a>Güvenlik Duvarı bağlantı noktalarını açın.</span><span class="sxs-lookup"><span data-stu-id="56e97-210"><a name="ports"></a>Open the firewall ports.</span></span>

   <span data-ttu-id="56e97-211">Her bir sanal makine Windows Güvenlik Duvarı'nda aşağıdaki bağlantı noktalarını açın.</span><span class="sxs-lookup"><span data-stu-id="56e97-211">On each virtual machine, open the following ports on the Windows Firewall.</span></span>

   | <span data-ttu-id="56e97-212">Amaç</span><span class="sxs-lookup"><span data-stu-id="56e97-212">Purpose</span></span> | <span data-ttu-id="56e97-213">TCP bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="56e97-213">TCP Port</span></span> | <span data-ttu-id="56e97-214">Notlar</span><span class="sxs-lookup"><span data-stu-id="56e97-214">Notes</span></span>
   | ------ | ------ | ------
   | <span data-ttu-id="56e97-215">SQL Server</span><span class="sxs-lookup"><span data-stu-id="56e97-215">SQL Server</span></span> | <span data-ttu-id="56e97-216">1433</span><span class="sxs-lookup"><span data-stu-id="56e97-216">1433</span></span> | <span data-ttu-id="56e97-217">SQL Server'ın varsayılan örnekleri için normal bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="56e97-217">Normal port for default instances of SQL Server.</span></span> <span data-ttu-id="56e97-218">Galeriden bir görüntü kullandıysanız, bu bağlantı noktası otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="56e97-218">If you used an image from the gallery, this port is automatically opened.</span></span>
   | <span data-ttu-id="56e97-219">Sistem durumu araştırması</span><span class="sxs-lookup"><span data-stu-id="56e97-219">Health probe</span></span> | <span data-ttu-id="56e97-220">59999</span><span class="sxs-lookup"><span data-stu-id="56e97-220">59999</span></span> | <span data-ttu-id="56e97-221">Herhangi bir TCP bağlantı noktasını açın.</span><span class="sxs-lookup"><span data-stu-id="56e97-221">Any open TCP port.</span></span> <span data-ttu-id="56e97-222">Bir sonraki adımda, yük dengeleyici yapılandırma [durumu araştırması](#probe) ve bu bağlantı noktasını kullanmak üzere küme.</span><span class="sxs-lookup"><span data-stu-id="56e97-222">In a later step, configure the load balancer [health probe](#probe) and the cluster to use this port.</span></span>  

1. <span data-ttu-id="56e97-223">Depolama sanal makineye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="56e97-223">Add storage to the virtual machine.</span></span> <span data-ttu-id="56e97-224">Ayrıntılı bilgi için bkz: [depolama ekleme](../../../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="56e97-224">For detailed information, see [add storage](../../../storage/common/storage-premium-storage.md).</span></span>

   <span data-ttu-id="56e97-225">Her iki sanal makinelerin en az iki veri diskleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="56e97-225">Both virtual machines need at least two data disks.</span></span>

   <span data-ttu-id="56e97-226">Ham diskleri - bağlamanız değil NTFS biçimli disk.</span><span class="sxs-lookup"><span data-stu-id="56e97-226">Attach raw disks - not NTFS formatted disks.</span></span>
      >[!NOTE]
      ><span data-ttu-id="56e97-227">NTFS biçimli disk eklerseniz, yalnızca hiçbir disk uygunluk denetimi ile S2D etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56e97-227">If you attach NTFS-formatted disks, you can only enable S2D with no disk eligibility check.</span></span>  

   <span data-ttu-id="56e97-228">En az iki Premium Storage (SSD diskleri) her VM'e ekleyin.</span><span class="sxs-lookup"><span data-stu-id="56e97-228">Attach a minimum of two Premium Storage (SSD disks) to each VM.</span></span> <span data-ttu-id="56e97-229">En az öneririz P30 (1 TB) diskler.</span><span class="sxs-lookup"><span data-stu-id="56e97-229">We recommend at least P30 (1 TB) disks.</span></span>

   <span data-ttu-id="56e97-230">Kümesi konak için önbelleğe almayı **salt okunur**.</span><span class="sxs-lookup"><span data-stu-id="56e97-230">Set host caching to **Read-only**.</span></span>

   <span data-ttu-id="56e97-231">Üretim ortamlarında kullanmak depolama kapasitesi, iş yüküne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="56e97-231">The storage capacity you use in production environments depends on your workload.</span></span> <span data-ttu-id="56e97-232">Bu makalede açıklanan tanıtım ve test için değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="56e97-232">The values described in this article are for demonstration and testing.</span></span>

1. <span data-ttu-id="56e97-233">[Sanal makineleri önceden var olan etki alanınıza ekleyin](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="56e97-233">[Add the virtual machines to your pre-existing domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

<span data-ttu-id="56e97-234">Sanal makineler oluşturup yapılandırılmış sonra Yük devretme kümesini yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56e97-234">After the virtual machines are created and configured, you can configure the failover cluster.</span></span>

## <a name="step-2-configure-the-windows-failover-cluster-with-s2d"></a><span data-ttu-id="56e97-235">2. adım: S2D ile Windows Yük devretme kümesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="56e97-235">Step 2: Configure the Windows Failover Cluster with S2D</span></span>

<span data-ttu-id="56e97-236">Sonraki adım, yük devretme kümesi ile S2D yapılandırmaktır.</span><span class="sxs-lookup"><span data-stu-id="56e97-236">The next step is to configure the failover cluster with S2D.</span></span> <span data-ttu-id="56e97-237">Bu adımda, aşağıdaki alt adımlar yapar:</span><span class="sxs-lookup"><span data-stu-id="56e97-237">In this step, you will do the following substeps:</span></span>

1. <span data-ttu-id="56e97-238">Windows Yük Devretme Kümelemesi özelliğini ekleyin</span><span class="sxs-lookup"><span data-stu-id="56e97-238">Add Windows Failover Clustering feature</span></span>
1. <span data-ttu-id="56e97-239">Küme doğrulama</span><span class="sxs-lookup"><span data-stu-id="56e97-239">Validate the cluster</span></span>
1. <span data-ttu-id="56e97-240">Yük devretme kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="56e97-240">Create the failover cluster</span></span>
1. <span data-ttu-id="56e97-241">Bulut tanığı oluşturma</span><span class="sxs-lookup"><span data-stu-id="56e97-241">Create the cloud witness</span></span>
1. <span data-ttu-id="56e97-242">Depolama ekleme</span><span class="sxs-lookup"><span data-stu-id="56e97-242">Add storage</span></span>

### <a name="add-windows-failover-clustering-feature"></a><span data-ttu-id="56e97-243">Windows Yük Devretme Kümelemesi özelliğini ekleyin</span><span class="sxs-lookup"><span data-stu-id="56e97-243">Add Windows Failover Clustering feature</span></span>

1. <span data-ttu-id="56e97-244">Başlamak için Yerel yöneticilerin üyesi olan ve Active Directory'deki nesneleri oluşturma izni olan bir etki alanı hesabı kullanarak RDP ile ilk sanal makineye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="56e97-244">To begin, connect to the first virtual machine with RDP using a domain account that is a member of local administrators, and has permissions to create objects in Active Directory.</span></span> <span data-ttu-id="56e97-245">Bu hesap yapılandırması geri kalanı için kullanın.</span><span class="sxs-lookup"><span data-stu-id="56e97-245">Use this account for the rest of the configuration.</span></span>

1. <span data-ttu-id="56e97-246">[Her bir sanal makine için Yük Devretme Kümelemesi özelliği eklemek](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="56e97-246">[Add Failover Clustering feature to each virtual machine](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

   <span data-ttu-id="56e97-247">Kullanıcı Arabiriminden Yük Devretme Kümelemesi özelliğini yüklemek için her iki sanal makinede aşağıdaki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="56e97-247">To install Failover Clustering feature from the UI, do the following steps on both virtual machines.</span></span>
   - <span data-ttu-id="56e97-248">İçinde **Sunucu Yöneticisi'ni**, tıklatın **Yönet**ve ardından **rol ve Özellik Ekle**.</span><span class="sxs-lookup"><span data-stu-id="56e97-248">In **Server Manager**, click **Manage**, and then click **Add Roles and Features**.</span></span>
   - <span data-ttu-id="56e97-249">İçinde **Ekle roller ve Özellikler Sihirbazı**, tıklatın **sonraki** için elde edene kadar **Özellikleri Seç**.</span><span class="sxs-lookup"><span data-stu-id="56e97-249">In **Add Roles and Features Wizard**, click **Next** until you get to **Select Features**.</span></span>
   - <span data-ttu-id="56e97-250">İçinde **Özellikleri Seç**, tıklatın **Yük Devretme Kümelemesi**.</span><span class="sxs-lookup"><span data-stu-id="56e97-250">In **Select Features**, click **Failover Clustering**.</span></span> <span data-ttu-id="56e97-251">Tüm gerekli özellikleri ve yönetim araçlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="56e97-251">Include all required features and the management tools.</span></span> <span data-ttu-id="56e97-252">Tıklatın **özelliklere**.</span><span class="sxs-lookup"><span data-stu-id="56e97-252">Click **Add Features**.</span></span>
   - <span data-ttu-id="56e97-253">Tıklatın **sonraki** ve ardından **son** özellikleri yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="56e97-253">Click **Next** and then click **Finish** to install the features.</span></span>

   <span data-ttu-id="56e97-254">PowerShell ile Yük Devretme Kümelemesi özelliğini yüklemek için aşağıdaki betiği bir yönetici PowerShell oturumundan sanal makinelerden birini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="56e97-254">To install the Failover Clustering feature with PowerShell, run the following script from an administrator PowerShell session on one of the virtual machines.</span></span>

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

<span data-ttu-id="56e97-255">Başvuru için sonraki adımlar adım 3'ün altında yönergeleri [depolama alanları doğrudan Windows Server 2016 kullanarak Hyper-yakınsanmış çözüm](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="56e97-255">For reference, the next steps follow the instructions under Step 3 of [Hyper-converged solution using Storage Spaces Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span></span>

### <a name="validate-the-cluster"></a><span data-ttu-id="56e97-256">Küme doğrulama</span><span class="sxs-lookup"><span data-stu-id="56e97-256">Validate the cluster</span></span>

<span data-ttu-id="56e97-257">Bu kılavuzda altındaki yönergeleri başvuruyor [küme doğrulama](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span><span class="sxs-lookup"><span data-stu-id="56e97-257">This guide refers to instructions under [validate cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span></span>

<span data-ttu-id="56e97-258">Küme kullanıcı arabirimini veya PowerShell ile doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="56e97-258">Validate the cluster in the UI or with PowerShell.</span></span>

<span data-ttu-id="56e97-259">Kullanıcı Arabirimi ile küme doğrulamak için aşağıdaki adımları sanal makinelerin birini yapın.</span><span class="sxs-lookup"><span data-stu-id="56e97-259">To validate the cluster with the UI, do the following steps from one of the virtual machines.</span></span>

1. <span data-ttu-id="56e97-260">İçinde **Sunucu Yöneticisi'ni**, tıklatın **Araçları**, ardından **yük devretme kümesi Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="56e97-260">In **Server Manager**, click **Tools**, then click **Failover Cluster Manager**.</span></span>
1. <span data-ttu-id="56e97-261">İçinde **yük devretme kümesi Yöneticisi**, tıklatın **eylem**, ardından **yapılandırmasını doğrula...** .</span><span class="sxs-lookup"><span data-stu-id="56e97-261">In **Failover Cluster Manager**, click **Action**, then click **Validate Configuration...**.</span></span>
1. <span data-ttu-id="56e97-262">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="56e97-262">Click **Next**.</span></span>
1. <span data-ttu-id="56e97-263">Üzerinde **sunucuları Seç veya küme**, her iki sanal makine adını yazın.</span><span class="sxs-lookup"><span data-stu-id="56e97-263">On **Select Servers or a Cluster**, type the name of both virtual machines.</span></span>
1. <span data-ttu-id="56e97-264">Üzerinde **testi seçenekleri**, seçin **yalnızca seçtiğim Testleri Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="56e97-264">On **Testing options**, choose **Run only tests I select**.</span></span> <span data-ttu-id="56e97-265">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="56e97-265">Click **Next**.</span></span>
1. <span data-ttu-id="56e97-266">Üzerinde **Test seçimi**, dışındaki tüm testleri dahil **depolama**.</span><span class="sxs-lookup"><span data-stu-id="56e97-266">On **Test selection**, include all tests except **Storage**.</span></span> <span data-ttu-id="56e97-267">Aşağıdaki resme bakın:</span><span class="sxs-lookup"><span data-stu-id="56e97-267">See the following picture:</span></span>

   ![Testleri doğrula](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. <span data-ttu-id="56e97-269">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="56e97-269">Click **Next**.</span></span>
1. <span data-ttu-id="56e97-270">Üzerinde **onay**, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="56e97-270">On **Confirmation**, click **Next**.</span></span>

<span data-ttu-id="56e97-271">**Yapılandırma Doğrulama Sihirbazı** doğrulama testleri çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="56e97-271">The **Validate a Configuration Wizard** runs the validation tests.</span></span>

<span data-ttu-id="56e97-272">PowerShell ile küme doğrulamak için aşağıdaki komut dosyasını bir yönetici PowerShell oturumundan sanal makinelerden birini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="56e97-272">To validate the cluster with PowerShell, run the following script from an administrator PowerShell session on one of the virtual machines.</span></span>

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

<span data-ttu-id="56e97-273">Kümeyi doğrulamaya sonra Yük devretme kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="56e97-273">After you validate the cluster, create the failover cluster.</span></span>

### <a name="create-the-failover-cluster"></a><span data-ttu-id="56e97-274">Yük devretme kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="56e97-274">Create the failover cluster</span></span>

<span data-ttu-id="56e97-275">Bu kılavuz başvurduğu [yük devretme kümesi oluşturma](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span><span class="sxs-lookup"><span data-stu-id="56e97-275">This guide refers to [Create the failover cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span></span>

<span data-ttu-id="56e97-276">Yük devretme kümesi oluşturmak için gerekir:</span><span class="sxs-lookup"><span data-stu-id="56e97-276">To create the failover cluster, you need:</span></span>
- <span data-ttu-id="56e97-277">Küme düğümleri duruma sanal makineleri adları.</span><span class="sxs-lookup"><span data-stu-id="56e97-277">The names of the virtual machines that become the cluster nodes.</span></span>
- <span data-ttu-id="56e97-278">Yük devretme kümesi için bir ad</span><span class="sxs-lookup"><span data-stu-id="56e97-278">A name for the failover cluster</span></span>
- <span data-ttu-id="56e97-279">Yük devretme kümesi için bir IP adresi.</span><span class="sxs-lookup"><span data-stu-id="56e97-279">An IP address for the failover cluster.</span></span> <span data-ttu-id="56e97-280">Aynı Azure sanal ağ ve alt küme düğümleri olarak kullanılmayan bir IP adresi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56e97-280">You can use an IP address that is not used on the same Azure virtual network and subnet as the cluster nodes.</span></span>

<span data-ttu-id="56e97-281">Aşağıdaki PowerShell yük devretme kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="56e97-281">The following PowerShell creates a failover cluster.</span></span> <span data-ttu-id="56e97-282">Düğümler (sanal makine adları) ve Azure VNET kullanılabilir bir IP adresinden adlarıyla betik güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="56e97-282">Update the script with the names of the nodes (the virtual machine names) and an available IP address from the Azure VNET:</span></span>

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a><span data-ttu-id="56e97-283">Bir bulut tanığı oluşturma</span><span class="sxs-lookup"><span data-stu-id="56e97-283">Create a cloud witness</span></span>

<span data-ttu-id="56e97-284">Bulut tanığı, küme çekirdek tanığı bir Azure depolama Blob depolanan yeni türüdür.</span><span class="sxs-lookup"><span data-stu-id="56e97-284">Cloud Witness is a new type of cluster quorum witness stored in an Azure Storage Blob.</span></span> <span data-ttu-id="56e97-285">Bu, bir Tanık paylaşımı barındırma ayrı bir VM gereksinimini ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="56e97-285">This removes the need of a separate VM hosting a witness share.</span></span>

1. <span data-ttu-id="56e97-286">[Yük devretme kümesi için bir bulut tanığı oluşturma](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="56e97-286">[Create a cloud witness for the failover cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span>

1. <span data-ttu-id="56e97-287">Bir blob kapsayıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="56e97-287">Create a blob container.</span></span>

1. <span data-ttu-id="56e97-288">Erişim tuşları ve kapsayıcı URL'si kaydedin.</span><span class="sxs-lookup"><span data-stu-id="56e97-288">Save the access keys and the container URL.</span></span>

1. <span data-ttu-id="56e97-289">Yük devretme kümesi küme çekirdek tanığı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="56e97-289">Configure the failover cluster cluster quorum witness.</span></span> <span data-ttu-id="56e97-290">[Kullanıcı arabiriminde çekirdek tanığı yapılandırma], bakın. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) kullanıcı arabiriminde.</span><span class="sxs-lookup"><span data-stu-id="56e97-290">See, [Configure the quorum witness in the user interface].(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in the UI.</span></span>

### <a name="add-storage"></a><span data-ttu-id="56e97-291">Depolama ekleme</span><span class="sxs-lookup"><span data-stu-id="56e97-291">Add storage</span></span>

<span data-ttu-id="56e97-292">S2D diskler boş ve bölümleri veya diğer veri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="56e97-292">The disks for S2D need to be empty and without partitions or other data.</span></span> <span data-ttu-id="56e97-293">Temizlemek için diskleri izleyin [bu kılavuzdaki adımları](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span><span class="sxs-lookup"><span data-stu-id="56e97-293">To clean disks follow [the steps in this guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span></span>

1. <span data-ttu-id="56e97-294">[Etkinleştirme depolama alanları doğrudan \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="56e97-294">[Enable Store Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span></span>

   <span data-ttu-id="56e97-295">Aşağıdaki PowerShell doğrudan depolama alanları sağlar.</span><span class="sxs-lookup"><span data-stu-id="56e97-295">The following PowerShell enables storage spaces direct.</span></span>  

   ```PowerShell
   Enable-ClusterS2D
   ```

   <span data-ttu-id="56e97-296">İçinde **yük devretme kümesi Yöneticisi**, depolama havuzu şimdi görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56e97-296">In **Failover Cluster Manager**, you can now see the storage pool.</span></span>

1. <span data-ttu-id="56e97-297">[Bir birim oluşturmak](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span><span class="sxs-lookup"><span data-stu-id="56e97-297">[Create a volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span></span>

   <span data-ttu-id="56e97-298">S2D özelliklerden biri, etkinleştirdiğinizde, otomatik olarak bir depolama havuzu oluşturmasıdır.</span><span class="sxs-lookup"><span data-stu-id="56e97-298">One of the features of S2D is that it automatically creates a storage pool when you enable it.</span></span> <span data-ttu-id="56e97-299">Şimdi bir birim oluşturmak hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="56e97-299">You are now ready to create a volume.</span></span> <span data-ttu-id="56e97-300">PowerShell komutunu `New-Volume` biçimlendirme, kümeye ekleme ve Küme Paylaşılan birimi (CSV) oluşturma gibi birim oluşturma işlemini otomatikleştirir.</span><span class="sxs-lookup"><span data-stu-id="56e97-300">The PowerShell commandlet `New-Volume` automates the volume creation process, including formatting, adding to the cluster, and creating a cluster shared volume (CSV).</span></span> <span data-ttu-id="56e97-301">Aşağıdaki örnek, bir 800 gigabayt (GB) CSV oluşturur.</span><span class="sxs-lookup"><span data-stu-id="56e97-301">The following example creates an 800 gigabyte (GB) CSV.</span></span>

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   <span data-ttu-id="56e97-302">Bu komut tamamlandıktan sonra bir 800 GB birimin küme kaynağı olarak bağlı.</span><span class="sxs-lookup"><span data-stu-id="56e97-302">After this command completes, an 800 GB volume is mounted as a cluster resource.</span></span> <span data-ttu-id="56e97-303">Birim altındadır `C:\ClusterStorage\Volume1\`.</span><span class="sxs-lookup"><span data-stu-id="56e97-303">The volume is at `C:\ClusterStorage\Volume1\`.</span></span>

   <span data-ttu-id="56e97-304">Aşağıdaki diyagramda, Küme Paylaşılan birimi S2D ile gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="56e97-304">The following diagram shows a cluster shared volume with S2D:</span></span>

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a><span data-ttu-id="56e97-306">3. adım: Test yük devretme küme yük devretmesi</span><span class="sxs-lookup"><span data-stu-id="56e97-306">Step 3: Test failover cluster failover</span></span>

<span data-ttu-id="56e97-307">Yük Devretme Kümesi Yöneticisi'nde, diğer küme düğümüne depolama kaynağı taşıyabildiğinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="56e97-307">In Failover Cluster Manager, verify that you can move the storage resource to the other cluster node.</span></span> <span data-ttu-id="56e97-308">İle yük devretme kümesine bağlanabiliyorsa **yük devretme kümesi Yöneticisi** ve bir düğümden diğerine, depolama birimini taşımak, FCI yapılandırmaya hazırsınız demektir.</span><span class="sxs-lookup"><span data-stu-id="56e97-308">If you can connect to the failover cluster with **Failover Cluster Manager** and move the storage from one node to the other, you are ready to configure the FCI.</span></span>

## <a name="step-4-create-sql-server-fci"></a><span data-ttu-id="56e97-309">4. adım: SQL Server FCI oluşturma</span><span class="sxs-lookup"><span data-stu-id="56e97-309">Step 4: Create SQL Server FCI</span></span>

<span data-ttu-id="56e97-310">Yük devretme kümesi ve depolama da dahil olmak üzere tüm küme bileşenleri yapılandırdıktan sonra SQL Server FCI oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56e97-310">After you have configured the failover cluster and all cluster components including storage, you can create the SQL Server FCI.</span></span>

1. <span data-ttu-id="56e97-311">RDP ile ilk sanal makineye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="56e97-311">Connect to the first virtual machine with RDP.</span></span>

1. <span data-ttu-id="56e97-312">İçinde **yük devretme kümesi Yöneticisi**, tüm küme çekirdek kaynakları ilk sanal makinede olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="56e97-312">In **Failover Cluster Manager**, make sure all cluster core resources are on the first virtual machine.</span></span> <span data-ttu-id="56e97-313">Gerekirse, tüm kaynaklar bu sanal makineyi taşıyın.</span><span class="sxs-lookup"><span data-stu-id="56e97-313">If necessary, move all resources to this virtual machine.</span></span>

1. <span data-ttu-id="56e97-314">Yükleme medyasındaki bulun.</span><span class="sxs-lookup"><span data-stu-id="56e97-314">Locate the installation media.</span></span> <span data-ttu-id="56e97-315">Sanal makine Azure Marketi görüntülerden birini kullanıyorsa, medya konumundadır `C:\SQLServer_<version number>_Full`.</span><span class="sxs-lookup"><span data-stu-id="56e97-315">If the virtual machine uses one of the Azure Marketplace images, the media is located at `C:\SQLServer_<version number>_Full`.</span></span> <span data-ttu-id="56e97-316">Tıklatın **Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="56e97-316">Click **Setup**.</span></span>

1. <span data-ttu-id="56e97-317">İçinde **SQL Server Yükleme Merkezi'ni**, tıklatın **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="56e97-317">In the **SQL Server Installation Center**, click **Installation**.</span></span>

1. <span data-ttu-id="56e97-318">Tıklatın **yeni SQL Server Yük devretme kümesi yükleme**.</span><span class="sxs-lookup"><span data-stu-id="56e97-318">Click **New SQL Server failover cluster installation**.</span></span> <span data-ttu-id="56e97-319">SQL Server FCI yüklemek için sihirbazdaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="56e97-319">Follow the instructions in the wizard to install the SQL Server FCI.</span></span>

   <span data-ttu-id="56e97-320">FCI veri dizinlerini kümelenmiş depolama biriminde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="56e97-320">The FCI data directories need to be on clustered storage.</span></span> <span data-ttu-id="56e97-321">S2D ile paylaşılan bir disk, ancak her sunucu üzerindeki bir birime bir bağlama noktası olmadığı.</span><span class="sxs-lookup"><span data-stu-id="56e97-321">With S2D, it's not a shared disk, but a mount point to a volume on each server.</span></span> <span data-ttu-id="56e97-322">S2D birimin her iki düğüm arasında eşitler.</span><span class="sxs-lookup"><span data-stu-id="56e97-322">S2D synchronizes the volume between both nodes.</span></span> <span data-ttu-id="56e97-323">Birim kümeye Küme Paylaşılan birimi olarak sunulur.</span><span class="sxs-lookup"><span data-stu-id="56e97-323">The volume is presented to the cluster as a cluster shared volume.</span></span> <span data-ttu-id="56e97-324">CSV bağlama noktası veri dizinler için kullanın.</span><span class="sxs-lookup"><span data-stu-id="56e97-324">Use the CSV mount point for the data directories.</span></span>

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. <span data-ttu-id="56e97-326">Kurulum Sihirbazı'nı tamamladıktan sonra bir SQL Server FCI ilk düğümde yükleyecek.</span><span class="sxs-lookup"><span data-stu-id="56e97-326">After you complete the wizard, Setup will install a SQL Server FCI on the first node.</span></span>

1. <span data-ttu-id="56e97-327">Kurulum, ilk düğümde FCI başarıyla yüklendikten sonra ikinci düğüme RDP ile bağlanın.</span><span class="sxs-lookup"><span data-stu-id="56e97-327">After Setup successfully installs the FCI on the first node, connect to the second node with RDP.</span></span>

1. <span data-ttu-id="56e97-328">Açık **SQL Server Yükleme Merkezi'ni**.</span><span class="sxs-lookup"><span data-stu-id="56e97-328">Open the **SQL Server Installation Center**.</span></span> <span data-ttu-id="56e97-329">Tıklatın **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="56e97-329">Click **Installation**.</span></span>

1. <span data-ttu-id="56e97-330">Tıklatın **bir SQL Server Yük devretme kümesine Ekle düğümü**.</span><span class="sxs-lookup"><span data-stu-id="56e97-330">Click **Add node to a SQL Server failover cluster**.</span></span> <span data-ttu-id="56e97-331">SQL server yükleyin ve bu sunucu için FCI eklemek için sihirbazdaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="56e97-331">Follow the instructions in the wizard to install SQL server and add this server to the FCI.</span></span>

   >[!NOTE]
   ><span data-ttu-id="56e97-332">SQL Server ile bir Azure Market galeri görüntüsü kullandıysanız, SQL Server araçları görüntüsüne dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="56e97-332">If you used an Azure Marketplace gallery image with SQL Server, SQL Server tools were included with the image.</span></span> <span data-ttu-id="56e97-333">Bu görüntü kullanmadıysanız, SQL Server araçları ayrı olarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="56e97-333">If you did not use this image, install the SQL Server tools separately.</span></span> <span data-ttu-id="56e97-334">Bkz: [karşıdan SQL Server Management Studio'yu (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="56e97-334">See [Download SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="step-5-create-azure-load-balancer"></a><span data-ttu-id="56e97-335">5. adım: Azure yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="56e97-335">Step 5: Create Azure load balancer</span></span>

<span data-ttu-id="56e97-336">Azure sanal makinelerde kümeleri aynı anda bir küme düğümünde olması gereken bir IP adresi tutmak için bir yük dengeleyici kullanın.</span><span class="sxs-lookup"><span data-stu-id="56e97-336">On Azure virtual machines, clusters use a load balancer to hold an IP address that needs to be on one cluster node at a time.</span></span> <span data-ttu-id="56e97-337">Bu çözümde, SQL Server FCI için IP adresini yük dengeleyici tutar.</span><span class="sxs-lookup"><span data-stu-id="56e97-337">In this solution, the load balancer holds the IP address for the SQL Server FCI.</span></span>

<span data-ttu-id="56e97-338">[Oluşturma ve Azure yük dengeleyici yapılandırma](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="56e97-338">[Create and configure an Azure load balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

### <a name="create-the-load-balancer-in-the-azure-portal"></a><span data-ttu-id="56e97-339">Azure portalında yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="56e97-339">Create the load balancer in the Azure portal</span></span>

<span data-ttu-id="56e97-340">Yük Dengeleyici oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="56e97-340">To create the load balancer:</span></span>

1. <span data-ttu-id="56e97-341">Azure portalında sanal makinelerle kaynak grubuna gidin.</span><span class="sxs-lookup"><span data-stu-id="56e97-341">In the Azure portal, go to the Resource Group with the virtual machines.</span></span>

1. <span data-ttu-id="56e97-342">Tıklatın **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="56e97-342">Click **+ Add**.</span></span> <span data-ttu-id="56e97-343">Market arama **yük dengeleyici**.</span><span class="sxs-lookup"><span data-stu-id="56e97-343">Search the Marketplace for **Load Balancer**.</span></span> <span data-ttu-id="56e97-344">Tıklatın **yük dengeleyici**.</span><span class="sxs-lookup"><span data-stu-id="56e97-344">Click **Load Balancer**.</span></span>

1. <span data-ttu-id="56e97-345">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="56e97-345">Click **Create**.</span></span>

1. <span data-ttu-id="56e97-346">Yük Dengeleyici ile yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="56e97-346">Configure the load balancer with:</span></span>

   - <span data-ttu-id="56e97-347">**Ad**: yük dengeleyici tanımlayan bir ad.</span><span class="sxs-lookup"><span data-stu-id="56e97-347">**Name**: A name that identifies the load balancer.</span></span>
   - <span data-ttu-id="56e97-348">**Tür**: yük dengeleyici, genel veya özel olabilir.</span><span class="sxs-lookup"><span data-stu-id="56e97-348">**Type**: The load balancer can be either public or private.</span></span> <span data-ttu-id="56e97-349">Özel yük dengeleyici aynı sanal ağ içinde erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="56e97-349">A private load balancer can be accessed from within the same VNET.</span></span> <span data-ttu-id="56e97-350">Çoğu Azure uygulamaları özel yük dengeleyici kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56e97-350">Most Azure applications can use a private load balancer.</span></span> <span data-ttu-id="56e97-351">Uygulamanızın doğrudan Internet üzerinden SQL Server erişmesi gerekirse bir genel yük dengeleyiciye kullanın.</span><span class="sxs-lookup"><span data-stu-id="56e97-351">If your application needs access to SQL Server directly over the Internet, use a public load balancer.</span></span>
   - <span data-ttu-id="56e97-352">**Sanal ağ**: sanal makineleri aynı ağ.</span><span class="sxs-lookup"><span data-stu-id="56e97-352">**Virtual Network**: The same network as the virtual machines.</span></span>
   - <span data-ttu-id="56e97-353">**Alt ağ**: sanal makineler aynı alt ağda.</span><span class="sxs-lookup"><span data-stu-id="56e97-353">**Subnet**: The same subnet as the virtual machines.</span></span>
   - <span data-ttu-id="56e97-354">**Özel IP adresi**: SQL Server FCI küme ağ kaynağına atanan aynı IP adresi.</span><span class="sxs-lookup"><span data-stu-id="56e97-354">**Private IP address**: The same IP address that you assigned to the SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="56e97-355">**Abonelik**: bilgisayarınızı Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="56e97-355">**subscription**: Your Azure subscription.</span></span>
   - <span data-ttu-id="56e97-356">**Kaynak grubu**: sanal makinelerinizi aynı kaynak grubunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="56e97-356">**Resource Group**: Use the same resource group as your virtual machines.</span></span>
   - <span data-ttu-id="56e97-357">**Konum**: aynı Azure konumunda sanal makinelerinizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="56e97-357">**Location**: Use the same Azure location as your virtual machines.</span></span>
   <span data-ttu-id="56e97-358">Aşağıdaki resme bakın:</span><span class="sxs-lookup"><span data-stu-id="56e97-358">See the following picture:</span></span>

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-the-load-balancer-backend-pool"></a><span data-ttu-id="56e97-360">Yük Dengeleyici arka uç havuzunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="56e97-360">Configure the load balancer backend pool</span></span>

1. <span data-ttu-id="56e97-361">Sanal makineler ile Azure kaynak grubu geri dönün ve Yeni Yük Dengeleyici bulun.</span><span class="sxs-lookup"><span data-stu-id="56e97-361">Return to the Azure Resource Group with the virtual machines and locate the new load balancer.</span></span> <span data-ttu-id="56e97-362">Kaynak grubu görünümü yenilemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="56e97-362">You may have to refresh the view on the Resource Group.</span></span> <span data-ttu-id="56e97-363">Yük Dengeleyici'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="56e97-363">Click the load balancer.</span></span>

1. <span data-ttu-id="56e97-364">Yük Dengeleyici dikey penceresinde **arka uç havuzları**.</span><span class="sxs-lookup"><span data-stu-id="56e97-364">On the load balancer blade, click **Backend pools**.</span></span>

1. <span data-ttu-id="56e97-365">Tıklatın **+ Ekle** bir arka uç havuzu eklemek için.</span><span class="sxs-lookup"><span data-stu-id="56e97-365">Click **+ Add** to add a backend pool.</span></span>

1. <span data-ttu-id="56e97-366">Arka uç havuzu için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="56e97-366">Type a name for the backend pool.</span></span>

1. <span data-ttu-id="56e97-367">Tıklatın **bir sanal makine Ekle**.</span><span class="sxs-lookup"><span data-stu-id="56e97-367">Click **Add a virtual machine**.</span></span>

1. <span data-ttu-id="56e97-368">Üzerinde **sanal makineleri seçin** dikey penceresinde tıklatın **bir kullanılabilirlik kümesi seçin**.</span><span class="sxs-lookup"><span data-stu-id="56e97-368">On the **Choose virtual machines** blade, click **Choose an availability set**.</span></span>

1. <span data-ttu-id="56e97-369">SQL Server sanal makinelere yerleştirilen kullanılabilirlik kümesi'ni seçin.</span><span class="sxs-lookup"><span data-stu-id="56e97-369">Choose the availability set that you placed the SQL Server virtual machines in.</span></span>

1. <span data-ttu-id="56e97-370">Üzerinde **sanal makineleri seçin** dikey penceresinde tıklatın **sanal makineleri seçin**.</span><span class="sxs-lookup"><span data-stu-id="56e97-370">On the **Choose virtual machines** blade, click **Choose the virtual machines**.</span></span>

   <span data-ttu-id="56e97-371">Azure portalı, aşağıdaki resimde gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="56e97-371">Your Azure portal should look like the following picture:</span></span>

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. <span data-ttu-id="56e97-373">Tıklatın **seçin** üzerinde **sanal makineleri seçin** dikey.</span><span class="sxs-lookup"><span data-stu-id="56e97-373">Click **Select** on the **Choose virtual machines** blade.</span></span>

1. <span data-ttu-id="56e97-374">Tıklatın **Tamam** iki kez.</span><span class="sxs-lookup"><span data-stu-id="56e97-374">Click **OK** twice.</span></span>

### <a name="configure-a-load-balancer-health-probe"></a><span data-ttu-id="56e97-375">Bir yük dengeleyici durum araştırması yapılandırın</span><span class="sxs-lookup"><span data-stu-id="56e97-375">Configure a load balancer health probe</span></span>

1. <span data-ttu-id="56e97-376">Yük Dengeleyici dikey penceresinde **sistem durumu araştırmalarının**.</span><span class="sxs-lookup"><span data-stu-id="56e97-376">On the load balancer blade, click **Health probes**.</span></span>

1. <span data-ttu-id="56e97-377">Tıklatın **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="56e97-377">Click **+ Add**.</span></span>

1. <span data-ttu-id="56e97-378">Üzerinde **Ekle durumu araştırması** dikey penceresinde <a name="probe"> </a>sistem araştırma parametreleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="56e97-378">On the **Add health probe** blade, <a name="probe"></a>Set the health probe parameters:</span></span>

   - <span data-ttu-id="56e97-379">**Ad**: durumu araştırması için bir ad.</span><span class="sxs-lookup"><span data-stu-id="56e97-379">**Name**: A name for the health probe.</span></span>
   - <span data-ttu-id="56e97-380">**Protokol**: TCP.</span><span class="sxs-lookup"><span data-stu-id="56e97-380">**Protocol**: TCP.</span></span>
   - <span data-ttu-id="56e97-381">**Bağlantı noktası**: bir kullanılabilir TCP bağlantı noktasına ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="56e97-381">**Port**: Set to an available TCP port.</span></span> <span data-ttu-id="56e97-382">Bu bağlantı noktası açık güvenlik duvarı bağlantı noktası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="56e97-382">This port requires an open firewall port.</span></span> <span data-ttu-id="56e97-383">Kullanım [aynı bağlantı noktasını](#ports) sistem durumu araştırması için güvenlik duvarında ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="56e97-383">Use the [same port](#ports) you set for the health probe at the firewall.</span></span>
   - <span data-ttu-id="56e97-384">**Aralığı**: 5 saniye.</span><span class="sxs-lookup"><span data-stu-id="56e97-384">**Interval**: 5 Seconds.</span></span>
   - <span data-ttu-id="56e97-385">**Sağlıksız eşik**: 2 art arda hatalar.</span><span class="sxs-lookup"><span data-stu-id="56e97-385">**Unhealthy threshold**: 2 consecutive failures.</span></span>

1. <span data-ttu-id="56e97-386">Tamam'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="56e97-386">Click OK.</span></span>

### <a name="set-load-balancing-rules"></a><span data-ttu-id="56e97-387">Yük Dengeleme kuralları ayarlama</span><span class="sxs-lookup"><span data-stu-id="56e97-387">Set load balancing rules</span></span>

1. <span data-ttu-id="56e97-388">Yük Dengeleyici dikey penceresinde **Yük Dengeleme kuralları**.</span><span class="sxs-lookup"><span data-stu-id="56e97-388">On the load balancer blade, click **Load balancing rules**.</span></span>

1. <span data-ttu-id="56e97-389">Tıklatın **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="56e97-389">Click **+ Add**.</span></span>

1. <span data-ttu-id="56e97-390">Yük Dengeleme kuralları parametreleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="56e97-390">Set the load balancing rules parameters:</span></span>

   - <span data-ttu-id="56e97-391">**Ad**: Yük Dengeleme kuralları için bir ad.</span><span class="sxs-lookup"><span data-stu-id="56e97-391">**Name**: A name for the load balancing rules.</span></span>
   - <span data-ttu-id="56e97-392">**Ön uç IP adresi**: SQL Server FCI küme ağ kaynağı için IP adresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="56e97-392">**Frontend IP address**: Use the IP address for the SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="56e97-393">**Bağlantı noktası**: SQL Server FCI TCP bağlantı noktası için ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="56e97-393">**Port**: Set for the SQL Server FCI TCP port.</span></span> <span data-ttu-id="56e97-394">Varsayılan örneği bağlantı noktası 1433'tür.</span><span class="sxs-lookup"><span data-stu-id="56e97-394">The default instance port is 1433.</span></span>
   - <span data-ttu-id="56e97-395">**Arka uç bağlantı noktası**: aynı bağlantı noktası olarak bu değeri kullanır **bağlantı noktası** değeri, etkinleştirdiğinizde **kayan IP (doğrudan sunucu dönüşü)**.</span><span class="sxs-lookup"><span data-stu-id="56e97-395">**Backend port**: This value uses the same port as the **Port** value when you enable **Floating IP (direct server return)**.</span></span>
   - <span data-ttu-id="56e97-396">**Arka uç havuzu**: daha önce yapılandırılmış arka uç havuzu adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="56e97-396">**Backend pool**: Use the backend pool name that you configured earlier.</span></span>
   - <span data-ttu-id="56e97-397">**Sistem durumu araştırma**: daha önce yapılandırılmış durumu araştırması kullanın.</span><span class="sxs-lookup"><span data-stu-id="56e97-397">**Health probe**: Use the health probe that you configured earlier.</span></span>
   - <span data-ttu-id="56e97-398">**Oturum kalıcılığı**: yok.</span><span class="sxs-lookup"><span data-stu-id="56e97-398">**Session persistence**: None.</span></span>
   - <span data-ttu-id="56e97-399">**Boşta kalma zaman aşımı (dakika)**: 4.</span><span class="sxs-lookup"><span data-stu-id="56e97-399">**Idle timeout (minutes)**: 4.</span></span>
   - <span data-ttu-id="56e97-400">**Kayan IP (doğrudan sunucu dönüşü)**: etkin</span><span class="sxs-lookup"><span data-stu-id="56e97-400">**Floating IP (direct server return)**: Enabled</span></span>

1. <span data-ttu-id="56e97-401">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="56e97-401">Click **OK**.</span></span>

## <a name="step-6-configure-cluster-for-probe"></a><span data-ttu-id="56e97-402">Adım 6: küme araştırma için yapılandırın</span><span class="sxs-lookup"><span data-stu-id="56e97-402">Step 6: Configure cluster for probe</span></span>

<span data-ttu-id="56e97-403">Küme araştırma port parametresi PowerShell'de ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="56e97-403">Set the cluster probe port parameter in PowerShell.</span></span>

<span data-ttu-id="56e97-404">Küme araştırma bağlantı noktası parametresini ayarlamak için aşağıdaki komut dosyası, ortamınızdan değişkenlerde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="56e97-404">To set the cluster probe port parameter, update variables in the following script from your environment.</span></span>

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name).
   $IPResourceName = "IP Address Resource Name" # the IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # the IP Address of the Internal Load Balancer (ILB). This is the static IP address for the load balancer you configured in the Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a><span data-ttu-id="56e97-405">7. adım: Test FCI yük devretme</span><span class="sxs-lookup"><span data-stu-id="56e97-405">Step 7: Test FCI failover</span></span>

<span data-ttu-id="56e97-406">Yük devretme küme işlevselliğini doğrulamak için FCI.</span><span class="sxs-lookup"><span data-stu-id="56e97-406">Test failover of the FCI to validate cluster functionality.</span></span> <span data-ttu-id="56e97-407">Aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="56e97-407">Do the following steps:</span></span>

1. <span data-ttu-id="56e97-408">RDP ile SQL Server FCI küme düğümlerinden birinin bağlayın.</span><span class="sxs-lookup"><span data-stu-id="56e97-408">Connect to one of the SQL Server FCI cluster nodes with RDP.</span></span>

1. <span data-ttu-id="56e97-409">Açık **yük devretme kümesi Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="56e97-409">Open **Failover Cluster Manager**.</span></span> <span data-ttu-id="56e97-410">Tıklatın **rolleri**.</span><span class="sxs-lookup"><span data-stu-id="56e97-410">Click **Roles**.</span></span> <span data-ttu-id="56e97-411">SQL Server FCI rol sahibi olan düğümü dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="56e97-411">Notice which node owns the SQL Server FCI role.</span></span>

1. <span data-ttu-id="56e97-412">SQL Server FCI role sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="56e97-412">Right-click the SQL Server FCI role.</span></span>

1. <span data-ttu-id="56e97-413">Tıklatın **taşıma** tıklatıp **olası iyi düğüme**.</span><span class="sxs-lookup"><span data-stu-id="56e97-413">Click **Move** and click **Best Possible Node**.</span></span>

<span data-ttu-id="56e97-414">**Yük Devretme Kümesi Yöneticisi** rolü ve kaynaklarını çevrimdışı duruma gösterir.</span><span class="sxs-lookup"><span data-stu-id="56e97-414">**Failover Cluster Manager** shows the role and its resources go offline.</span></span> <span data-ttu-id="56e97-415">Kaynakları taşıma ve başka bir düğümde çevrimiçi olması.</span><span class="sxs-lookup"><span data-stu-id="56e97-415">The resources then move and come online on the other node.</span></span>

### <a name="test-connectivity"></a><span data-ttu-id="56e97-416">Bağlantıyı test etme</span><span class="sxs-lookup"><span data-stu-id="56e97-416">Test connectivity</span></span>

<span data-ttu-id="56e97-417">Bağlantıyı sınamak için aynı sanal ağda başka bir sanal makinede oturum açın.</span><span class="sxs-lookup"><span data-stu-id="56e97-417">To test connectivity, log in to another virtual machine in the same virtual network.</span></span> <span data-ttu-id="56e97-418">Açık **SQL Server Management Studio** ve SQL Server FCI adına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="56e97-418">Open **SQL Server Management Studio** and connect to the SQL Server FCI name.</span></span>

>[!NOTE]
><span data-ttu-id="56e97-419">Gerekirse, aşağıdakileri yapabilirsiniz, [SQL Server Management Studio'yu indirme](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="56e97-419">If necessary, you can [download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="limitations"></a><span data-ttu-id="56e97-420">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="56e97-420">Limitations</span></span>
<span data-ttu-id="56e97-421">Azure sanal makinelerde RPC bağlantı noktası, yük dengeleyici tarafından desteklenmediği için Microsoft Dağıtılmış İşlem Düzenleyicisi (DTC) Fcı'lerde üzerinde desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="56e97-421">On Azure virtual machines, Microsoft Distributed Transaction Coordinator (DTC) is not supported on FCIs because the RPC port is not supported by the load balancer.</span></span>

## <a name="see-also"></a><span data-ttu-id="56e97-422">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="56e97-422">See Also</span></span>

[<span data-ttu-id="56e97-423">Uzak Masaüstü'nü (Azure) S2D Kurulumu</span><span class="sxs-lookup"><span data-stu-id="56e97-423">Setup S2D with remote desktop (Azure)</span></span>](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

<span data-ttu-id="56e97-424">[Depolama alanları doğrudan ile çözüm Hyper yakınsanmış](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="56e97-424">[Hyper-converged solution with storage spaces direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span></span>

[<span data-ttu-id="56e97-425">Depolama alanına doğrudan genel bakış</span><span class="sxs-lookup"><span data-stu-id="56e97-425">Storage Space Direct Overview</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[<span data-ttu-id="56e97-426">S2D için SQL Server desteği</span><span class="sxs-lookup"><span data-stu-id="56e97-426">SQL Server support for S2D</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
