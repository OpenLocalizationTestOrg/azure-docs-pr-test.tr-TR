---
title: "Yük dengeli kümeleri MySQL clusterize | Microsoft Docs"
description: "Linux MySQL kümesi azure'da Klasik dağıtım modeliyle oluşturulan bir yük dengeli, yüksek kullanılabilirlik ayarlama"
services: virtual-machines-linux
documentationcenter: 
author: bureado
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6c413a16-e9b5-4ffe-a8a3-ae67046bbdf3
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/14/2015
ms.author: jparrel
ms.openlocfilehash: 4eaf86c9ac3e4dc2b51b88383626eda774cab0e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-load-balanced-sets-to-clusterize-mysql-on-linux"></a><span data-ttu-id="f8bfc-103">MySQL Linux'ta clusterize için yük dengeli kümeleri kullanın</span><span class="sxs-lookup"><span data-stu-id="f8bfc-103">Use load-balanced sets to clusterize MySQL on Linux</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f8bfc-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager](../../../resource-manager-deployment-model.md) ve klasik.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="f8bfc-105">Bu makale klasik dağıtım modelini incelemektedir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="f8bfc-106">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="f8bfc-107">A [Resource Manager şablonu](https://azure.microsoft.com/documentation/templates/mysql-replication/) MySQL Küme dağıtımı yapmanız gerekirse kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-107">A [Resource Manager template](https://azure.microsoft.com/documentation/templates/mysql-replication/) is available if you need to deploy a MySQL cluster.</span></span>

<span data-ttu-id="f8bfc-108">Bu makalede inceler ve MySQL Server yüksek kullanılabilirlik öncü olarak keşfetme Microsoft Azure üzerinde yüksek oranda kullanılabilir Linux tabanlı hizmetler dağıtmak kullanılabilir farklı yaklaşımlara göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-108">This article explores and illustrates the different approaches available to deploy highly available Linux-based services on Microsoft Azure, exploring MySQL Server high availability as a primer.</span></span> <span data-ttu-id="f8bfc-109">Bu yaklaşım gösteren bir video kullanılabilir [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span><span class="sxs-lookup"><span data-stu-id="f8bfc-109">A video illustrating this approach is available on [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span></span>

<span data-ttu-id="f8bfc-110">Biz DRBD, Corosync ve Pacemaker göre hiçbir şey paylaşılmayan, iki düğümlü ve tek yöneticili MySQL yüksek kullanılabilirlik çözümü özetler.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-110">We will outline a shared-nothing, two-node, single-master MySQL high availability solution based on DRBD, Corosync, and Pacemaker.</span></span> <span data-ttu-id="f8bfc-111">Yalnızca bir düğüm MySQL aynı anda çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-111">Only one node runs MySQL at a time.</span></span> <span data-ttu-id="f8bfc-112">Aynı zamanda okuma ve yazma DRBD kaynaktan aynı anda yalnızca bir düğüme sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-112">Reading and writing from the DRBD resource is also limited to only one node at a time.</span></span>

<span data-ttu-id="f8bfc-113">Yük dengeli kümeleri Microsoft Azure'da hepsini işlevselliği ve uç nokta algılama, kaldırma ve VIP normal kurtarılmasını sağlamak için kullanacağınız çünkü LVS gibi bir VIP çözümü için gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-113">There's no need for a VIP solution like LVS, because you'll use load-balanced sets in Microsoft Azure to provide round-robin functionality and endpoint detection, removal, and graceful recovery of the VIP.</span></span> <span data-ttu-id="f8bfc-114">VIP, bulut hizmeti ilk oluşturduğunuzda Microsoft Azure tarafından atanan genel olarak yönlendirilebilir bir IPv4 adresidir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-114">The VIP is a globally routable IPv4 address assigned by Microsoft Azure when you first create the cloud service.</span></span>

<span data-ttu-id="f8bfc-115">Diğer olası mimari NBD küme, Percona, Galera ve en az bir de dahil olmak üzere çeşitli ara yazılımı çözümler de dahil olmak üzere MySQL için bir VM olarak kullanılabilir [VM deposu](http://vmdepot.msopentech.com).</span><span class="sxs-lookup"><span data-stu-id="f8bfc-115">There are other possible architectures for MySQL, including NBD Cluster, Percona, Galera, and several middleware solutions, including at least one available as a VM on [VM Depot](http://vmdepot.msopentech.com).</span></span> <span data-ttu-id="f8bfc-116">Bu çözümlerin tek noktaya yayın ve çok noktaya yayın veya yayın üzerinde çoğaltabilir ve paylaşılan depolama ortamı veya birden çok ağ arabirimi güvenmeyin sürece senaryolar Microsoft Azure'da dağıtmak kolay olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-116">As long as these solutions can replicate on unicast vs. multicast or broadcast and don't rely on shared storage or multiple network interfaces, the scenarios should be easy to deploy on Microsoft Azure.</span></span>

<span data-ttu-id="f8bfc-117">Bunlar mimarileri kümeleme PostgreSQL ve OpenLDAP gibi diğer ürünlere yönelik benzer bir şekilde genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-117">These clustering architectures can be extended to other products like PostgreSQL and OpenLDAP in a similar fashion.</span></span> <span data-ttu-id="f8bfc-118">Örneğin, bu yük dengeleyici yordamı paylaşılmadığı ile başarıyla çok ana OpenLDAP ile test edilmiştir ve bizim Channel 9 blogunda izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-118">For example, this load-balancing procedure with shared nothing was successfully tested with multi-master OpenLDAP, and you can watch it on our Channel 9 blog.</span></span>

## <a name="get-ready"></a><span data-ttu-id="f8bfc-119">Hazırlanma</span><span class="sxs-lookup"><span data-stu-id="f8bfc-119">Get ready</span></span>
<span data-ttu-id="f8bfc-120">Aşağıdaki kaynaklar ve yeteneklerini gerekir:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-120">You need the following resources and abilities:</span></span>

  - <span data-ttu-id="f8bfc-121">Geçerli bir abonelik, en az iki VM oluşturabilmek için bir Microsoft Azure hesabı (Bu örnekte XS kullanılan)</span><span class="sxs-lookup"><span data-stu-id="f8bfc-121">A Microsoft Azure account with a valid subscription, able to create at least two VMs (XS was used in this example)</span></span>
  - <span data-ttu-id="f8bfc-122">Bir ağ ve bir alt ağ</span><span class="sxs-lookup"><span data-stu-id="f8bfc-122">A network and a subnet</span></span>
  - <span data-ttu-id="f8bfc-123">Bir benzeşim grubu</span><span class="sxs-lookup"><span data-stu-id="f8bfc-123">An affinity group</span></span>
  - <span data-ttu-id="f8bfc-124">Bir kullanılabilirlik kümesi</span><span class="sxs-lookup"><span data-stu-id="f8bfc-124">An availability set</span></span>
  - <span data-ttu-id="f8bfc-125">Bulut hizmeti ile aynı bölgede VHD oluşturma ve Linux VM'ler ekleme olanağı</span><span class="sxs-lookup"><span data-stu-id="f8bfc-125">The ability to create VHDs in the same region as the cloud service and attach them to the Linux VMs</span></span>

### <a name="tested-environment"></a><span data-ttu-id="f8bfc-126">Sınanan ortamı</span><span class="sxs-lookup"><span data-stu-id="f8bfc-126">Tested environment</span></span>
* <span data-ttu-id="f8bfc-127">Ubuntu 13.10</span><span class="sxs-lookup"><span data-stu-id="f8bfc-127">Ubuntu 13.10</span></span>
  * <span data-ttu-id="f8bfc-128">DRBD</span><span class="sxs-lookup"><span data-stu-id="f8bfc-128">DRBD</span></span>
  * <span data-ttu-id="f8bfc-129">MySQL sunucusu</span><span class="sxs-lookup"><span data-stu-id="f8bfc-129">MySQL Server</span></span>
  * <span data-ttu-id="f8bfc-130">Corosync ve Pacemaker</span><span class="sxs-lookup"><span data-stu-id="f8bfc-130">Corosync and Pacemaker</span></span>

### <a name="affinity-group"></a><span data-ttu-id="f8bfc-131">Benzeşim grubu</span><span class="sxs-lookup"><span data-stu-id="f8bfc-131">Affinity group</span></span>
<span data-ttu-id="f8bfc-132">Azure Klasik portalında oturum açarak çözüm için benzeşim grubu oluşturmak seçme **ayarları**ve bir benzeşim grubu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-132">Create an affinity group for the solution by signing in to the Azure classic portal, selecting **Settings**, and creating an affinity group.</span></span> <span data-ttu-id="f8bfc-133">Daha sonra oluşturulan ayrılan kaynakları bu benzeşim grubuna atanır.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-133">Allocated resources created later will be assigned to this affinity group.</span></span>

### <a name="networks"></a><span data-ttu-id="f8bfc-134">Ağlar</span><span class="sxs-lookup"><span data-stu-id="f8bfc-134">Networks</span></span>
<span data-ttu-id="f8bfc-135">Yeni bir ağ oluşturulur ve bir alt ağ içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-135">A new network is created, and a subnet is created inside the network.</span></span> <span data-ttu-id="f8bfc-136">Bu örnek 10.10.10.0/24 ağ içinde yalnızca bir /24 alt ağ ile kullanır.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-136">This example uses a 10.10.10.0/24 network with only one /24 subnet inside.</span></span>

### <a name="virtual-machines"></a><span data-ttu-id="f8bfc-137">Sanal makineler</span><span class="sxs-lookup"><span data-stu-id="f8bfc-137">Virtual machines</span></span>
<span data-ttu-id="f8bfc-138">İlk Ubuntu 13.10 VM Endorsed Ubuntu galeri görüntüsü kullanılarak oluşturulur ve adlandırılır `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-138">The first Ubuntu 13.10 VM is created by using an Endorsed Ubuntu Gallery image and is called `hadb01`.</span></span> <span data-ttu-id="f8bfc-139">Yeni bir bulut hizmeti hadb adlandırılan işlemde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-139">A new cloud service is created in the process, called hadb.</span></span> <span data-ttu-id="f8bfc-140">Bu ad, daha fazla kaynak eklendiğinde, hizmet olacak paylaşılan, yük dengelemeli yapısı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-140">This name illustrates the shared, load-balanced nature that the service will have when more resources are added.</span></span> <span data-ttu-id="f8bfc-141">Oluşturulmasını `hadb01` portal olaysız ve tamamlanan kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-141">The creation of `hadb01` is uneventful and completed by using the portal.</span></span> <span data-ttu-id="f8bfc-142">SSH için bir uç nokta otomatik olarak oluşturulur ve yeni bir ağ seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-142">An endpoint for SSH is automatically created, and the new network is selected.</span></span> <span data-ttu-id="f8bfc-143">Artık bir kullanılabilirlik VM'ler için kümesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-143">Now you can create an availability set for the VMs.</span></span>

<span data-ttu-id="f8bfc-144">(Teknik olarak, bulut hizmeti oluşturulduğunda) ilk VM oluşturulduktan sonra ikinci VM oluşturma `hadb02`.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-144">After the first VM is created (technically, when the cloud service is created), create the second VM, `hadb02`.</span></span> <span data-ttu-id="f8bfc-145">İkinci VM için Ubuntu 13.10 VM Galeriden Portalı'nı kullanarak, ancak var olan bir bulut hizmetini kullanın `hadb.cloudapp.net`, yeni bir tane oluşturmak yerine.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-145">For the second VM, use Ubuntu 13.10 VM from the Gallery by using the portal, but use an existing cloud service, `hadb.cloudapp.net`, instead of creating a new one.</span></span> <span data-ttu-id="f8bfc-146">Ağ ve kullanılabilirlik kümesi otomatik olarak seçilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-146">The network and availability set should be automatically selected.</span></span> <span data-ttu-id="f8bfc-147">Bir SSH uç noktası, çok oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-147">An SSH endpoint will be created, too.</span></span>

<span data-ttu-id="f8bfc-148">Her iki VM oluşturulduktan sonra SSH bağlantı noktasını not edin `hadb01` (TCP 22) ve `hadb02` (otomatik olarak Azure tarafından atanan).</span><span class="sxs-lookup"><span data-stu-id="f8bfc-148">After both VMs have been created, take note of the SSH port for `hadb01` (TCP 22) and `hadb02` (automatically assigned by Azure).</span></span>

### <a name="attached-storage"></a><span data-ttu-id="f8bfc-149">Bağlı depolama</span><span class="sxs-lookup"><span data-stu-id="f8bfc-149">Attached storage</span></span>
<span data-ttu-id="f8bfc-150">Her iki VM için yeni bir disk ekleyin ve işleminde 5 GB disk oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-150">Attach a new disk to both VMs and create 5-GB disks in the process.</span></span> <span data-ttu-id="f8bfc-151">Disklerin ana işletim sistemi disklerinizi kullanılmak VHD kapsayıcısında barındırılır.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-151">The disks are hosted in the VHD container in use for your main operating system disks.</span></span> <span data-ttu-id="f8bfc-152">Diskleri oluşturup bağlı sonra çekirdek yeni cihaz görürsünüz çünkü Linux yeniden başlatmaya gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-152">After disks are created and attached, there is no need to restart Linux because the kernel will see the new device.</span></span> <span data-ttu-id="f8bfc-153">Bu aygıt genellikle değil `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-153">This device is usually `/dev/sdc`.</span></span> <span data-ttu-id="f8bfc-154">Denetleme `dmesg` çıktısı için.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-154">Check `dmesg` for the output.</span></span>

<span data-ttu-id="f8bfc-155">Kullanarak her bir VM üzerinde bir bölüm oluşturmak `cfdisk` (birincil, Linux bölüm) ve yeni bölüm tablosuna yazma.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-155">On each VM, create a partition by using `cfdisk` (primary, Linux partition) and write the new partition table.</span></span> <span data-ttu-id="f8bfc-156">Bir dosya sistemi bu bölüme oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-156">Do not create a file system on this partition.</span></span>

## <a name="set-up-the-cluster"></a><span data-ttu-id="f8bfc-157">Küme ayarlama</span><span class="sxs-lookup"><span data-stu-id="f8bfc-157">Set up the cluster</span></span>
<span data-ttu-id="f8bfc-158">APT Corosync, Pacemaker ve DRBD her iki Ubuntu VM yüklemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-158">Use APT to install Corosync, Pacemaker, and DRBD on both Ubuntu VMs.</span></span> <span data-ttu-id="f8bfc-159">İle bunun için `apt-get`, aşağıdaki kodu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-159">To do so with `apt-get`, run the following code:</span></span>

    sudo apt-get install corosync pacemaker drbd8-utils.

<span data-ttu-id="f8bfc-160">MySQL şu anda yüklemeyin.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-160">Do not install MySQL at this time.</span></span> <span data-ttu-id="f8bfc-161">Debian ve Ubuntu yükleme betikleri başlatma MySQL veri dizini üzerinde `/var/lib/mysql`, ancak dizin DRBD dosya sistemi tarafından değiştirilen çünkü MySQL daha sonra yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-161">Debian and Ubuntu installation scripts will initialize a MySQL data directory on `/var/lib/mysql`, but because the directory will be superseded by a DRBD file system, you need to install MySQL later.</span></span>

<span data-ttu-id="f8bfc-162">Doğrulayın (kullanarak `/sbin/ifconfig`) her iki VM 10.10.10.0/24 alt ağ adresleri ve bunların birbirlerine ada göre ping atabildiğinizi kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-162">Verify (by using `/sbin/ifconfig`) that both VMs are using addresses in the 10.10.10.0/24 subnet and that they can ping each other by name.</span></span> <span data-ttu-id="f8bfc-163">Aynı zamanda `ssh-keygen` ve `ssh-copy-id` her iki VM, bir parola gerektirmeden SSH yoluyla kurabilir emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-163">You can also use `ssh-keygen` and `ssh-copy-id` to make sure both VMs can communicate via SSH without requiring a password.</span></span>

### <a name="set-up-drbd"></a><span data-ttu-id="f8bfc-164">DRBD ayarlayın</span><span class="sxs-lookup"><span data-stu-id="f8bfc-164">Set up DRBD</span></span>
<span data-ttu-id="f8bfc-165">Arka plandaki kullanan DRBD kaynak oluşturma `/dev/sdc1` üretmek için bölüm bir `/dev/drbd1` ext3 kullanılarak biçimlendirilmiş ve birincil ve ikincil düğüm kullanılan kaynak.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-165">Create a DRBD resource that uses the underlying `/dev/sdc1` partition to produce a `/dev/drbd1` resource that can be formatted by using ext3 and used in both primary and secondary nodes.</span></span>

1. <span data-ttu-id="f8bfc-166">Açık `/etc/drbd.d/r0.res` ve her iki VM aşağıdaki kaynak tanımında kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-166">Open `/etc/drbd.d/r0.res` and copy the following resource definition on both VMs:</span></span>

        resource r0 {
          on `hadb01` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.4:7789;
            meta-disk internal;
          }
          on `hadb02` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.5:7789;
            meta-disk internal;
          }
        }

2. <span data-ttu-id="f8bfc-167">Kaynak kullanarak başlatmak `drbdadm` her iki VM üzerinde:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-167">Initialize the resource by using `drbdadm` on both VMs:</span></span>

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. <span data-ttu-id="f8bfc-168">Birincil VM üzerinde (`hadb01`), DRBD kaynak (birincil) sahipliğini zorla:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-168">On the primary VM (`hadb01`), force ownership (primary) of the DRBD resource:</span></span>

        sudo drbdadm primary --force r0

<span data-ttu-id="f8bfc-169">/ Proc/drbd içeriğini incelerseniz (`sudo cat /proc/drbd`) her iki VM üzerinde görmelisiniz `Primary/Secondary` üzerinde `hadb01` ve `Secondary/Primary` üzerinde `hadb02`, bu noktada çözümü ile tutarlı.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-169">If you examine the contents of /proc/drbd (`sudo cat /proc/drbd`) on both VMs, you should see `Primary/Secondary` on `hadb01` and `Secondary/Primary` on `hadb02`, consistent with the solution at this point.</span></span> <span data-ttu-id="f8bfc-170">5 GB disk, müşterilere ücret ödemeden 10.10.10.0/24 ağ üzerinden eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-170">The 5-GB disk is synchronized over the 10.10.10.0/24 network at no charge to customers.</span></span>

<span data-ttu-id="f8bfc-171">Disk eşitlendikten sonra dosya sistemi üzerinde oluşturabileceğiniz `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-171">After the disk is synchronized, you can create the file system on `hadb01`.</span></span> <span data-ttu-id="f8bfc-172">Test amacıyla, ext2 kullandık, ancak aşağıdaki kodu ext3 dosya sistemi oluşturacak:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-172">For testing purposes, we used ext2, but the following code will create an ext3 file system:</span></span>

    mkfs.ext3 /dev/drbd1

### <a name="mount-the-drbd-resource"></a><span data-ttu-id="f8bfc-173">DRBD kaynak Bağla</span><span class="sxs-lookup"><span data-stu-id="f8bfc-173">Mount the DRBD resource</span></span>
<span data-ttu-id="f8bfc-174">Üzerinde DRBD kaynakları bağlamak artık hazırsınız `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-174">You're now ready to mount the DRBD resources on `hadb01`.</span></span> <span data-ttu-id="f8bfc-175">Debian ve türevleri kullanım `/var/lib/mysql` MySQL'ın veri dizini olarak.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-175">Debian and derivatives use `/var/lib/mysql` as MySQL's data directory.</span></span> <span data-ttu-id="f8bfc-176">MySQL yüklemediniz olduğundan dizin oluşturun ve DRBD kaynak bağlayın.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-176">Because you haven't installed MySQL, create the directory and mount the DRBD resource.</span></span> <span data-ttu-id="f8bfc-177">Bu seçenek gerçekleştirmek için aşağıdaki kodu çalıştırmak `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-177">To perform this option, run the following code on `hadb01`:</span></span>

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a><span data-ttu-id="f8bfc-178">MySQL ayarlayın</span><span class="sxs-lookup"><span data-stu-id="f8bfc-178">Set up MySQL</span></span>
<span data-ttu-id="f8bfc-179">MySQL yüklemek hazır artık `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-179">Now you're ready to install MySQL on `hadb01`:</span></span>

    sudo apt-get install mysql-server

<span data-ttu-id="f8bfc-180">İçin `hadb02`, iki seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-180">For `hadb02`, you have two options.</span></span> <span data-ttu-id="f8bfc-181">Mysql /var/lib/mysql oluşturmak, yeni bir veri dizin ile doldurun ve ardından içeriği kaldırmak sunuculu, yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-181">You can install mysql-server, which will create /var/lib/mysql, fill it with a new data directory, and then remove the contents.</span></span> <span data-ttu-id="f8bfc-182">Bu seçenek gerçekleştirmek için aşağıdaki kodu çalıştırmak `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-182">To perform this option, run the following code on `hadb02`:</span></span>

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

<span data-ttu-id="f8bfc-183">Yük devretme için ikinci seçenek, `hadb02` ve orada mysql server yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-183">The second option is to failover to `hadb02` and then install mysql-server there.</span></span> <span data-ttu-id="f8bfc-184">Yükleme betikleri mevcut yükleme görürsünüz ve touch olmaz.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-184">Installation scripts will notice the existing installation and won't touch it.</span></span>

<span data-ttu-id="f8bfc-185">Aşağıdaki kod çalıştıracağınız `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-185">Run the following code on `hadb01`:</span></span>

    sudo drbdadm secondary –force r0

<span data-ttu-id="f8bfc-186">Aşağıdaki kod çalıştıracağınız `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-186">Run the following code on `hadb02`:</span></span>

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

<span data-ttu-id="f8bfc-187">Yük devretme DRBD şimdi planlamıyorsanız, ilk seçenek tartışmaya açık bir şekilde daha az rağmen Zarif daha kolay olur.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-187">If you don't plan to failover DRBD now, the first option is easier although arguably less elegant.</span></span> <span data-ttu-id="f8bfc-188">Bu ayarladıktan sonra MySQL veritabanınızı üzerinde çalışmaya başlayabiliriz.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-188">After you set this up, you can start working on your MySQL database.</span></span> <span data-ttu-id="f8bfc-189">Aşağıdaki kod çalıştıracağınız `hadb02` (veya hangi sunucuların birini DRBD göre etkindir):</span><span class="sxs-lookup"><span data-stu-id="f8bfc-189">Run the following code on `hadb02` (or whichever one of the servers is active, according to DRBD):</span></span>

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* TO root;

> [!WARNING]
> <span data-ttu-id="f8bfc-190">Bu son deyim etkili bir şekilde bu tablodaki kök kullanıcı için kimlik doğrulaması devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-190">This last statement effectively disables authentication for the root user in this table.</span></span> <span data-ttu-id="f8bfc-191">Bu üretim-sınıf tarafından değiştirilmesi gereken verme deyimleri ve yalnızca tanımlayıcı amaçlarla yer alır.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-191">This should be replaced by your production-grade GRANT statements and is included only for illustrative purposes.</span></span>

<span data-ttu-id="f8bfc-192">(Bu kılavuzun amacı olan) VM'ler dışında sorgularından yapmak istiyorsanız, ayrıca ağ MySQL için etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-192">If you want to make queries from outside the VMs (which is the purpose of this guide), you also need to enable networking for MySQL.</span></span> <span data-ttu-id="f8bfc-193">Her iki VM üzerinde açmak `/etc/mysql/my.cnf` ve Git `bind-address`.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-193">On both VMs, open `/etc/mysql/my.cnf` and go to `bind-address`.</span></span> <span data-ttu-id="f8bfc-194">Adres 127.0.0.1 0.0.0.0 olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-194">Change the address from 127.0.0.1 to 0.0.0.0.</span></span> <span data-ttu-id="f8bfc-195">Dosyayı kaydettikten sonra sorun bir `sudo service mysql restart` geçerli birincil üzerinde.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-195">After saving the file, issue a `sudo service mysql restart` on your current primary.</span></span>

### <a name="create-the-mysql-load-balanced-set"></a><span data-ttu-id="f8bfc-196">MySQL yük dengeli kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8bfc-196">Create the MySQL load-balanced set</span></span>
<span data-ttu-id="f8bfc-197">Portalına geri dönün, Git `hadb01`ve seçin **uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-197">Go back to the portal, go to `hadb01`, and choose **Endpoints**.</span></span> <span data-ttu-id="f8bfc-198">Bir uç nokta oluşturmak için MySQL (TCP 3306) aşağı açılan listeden seçip **oluştur Yeni Yük dengeli kümesi**.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-198">To create an endpoint, choose MySQL (TCP 3306) from the drop-down list and select **Create new load balanced set**.</span></span> <span data-ttu-id="f8bfc-199">Yük dengeli uç nokta adı `lb-mysql`.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-199">Name the load-balanced endpoint `lb-mysql`.</span></span> <span data-ttu-id="f8bfc-200">Ayarlama **zaman** 5 saniye, en düşük.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-200">Set **Time** to 5 seconds, minimum.</span></span>

<span data-ttu-id="f8bfc-201">Uç nokta oluşturduktan sonra Git `hadb02`, seçin **uç noktaları**ve bir uç nokta oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-201">After you create the endpoint, go to `hadb02`, choose **Endpoints**, and create an endpoint.</span></span> <span data-ttu-id="f8bfc-202">Seçin `lb-mysql`ve ardından MySQL aşağı açılan listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-202">Choose `lb-mysql`, and then select MySQL from the drop-down list.</span></span> <span data-ttu-id="f8bfc-203">Bu adım için Azure CLI de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-203">You can also use the Azure CLI for this step.</span></span>

<span data-ttu-id="f8bfc-204">Şimdi küme el ile işlem için gereken her şeyi sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-204">You now have everything you need for manual operation of the cluster.</span></span>

### <a name="test-the-load-balanced-set"></a><span data-ttu-id="f8bfc-205">Sınama yük dengeli kümesi</span><span class="sxs-lookup"><span data-stu-id="f8bfc-205">Test the load-balanced set</span></span>
<span data-ttu-id="f8bfc-206">Testleri bir dış makineden herhangi bir MySQL istemcisi kullanarak veya bir Azure Web sitesi olarak çalışan phpMyAdmin gibi belirli uygulamaları kullanarak gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-206">Tests can be performed from an outside machine by using any MySQL client, or by using certain applications, like phpMyAdmin running as an Azure website.</span></span> <span data-ttu-id="f8bfc-207">Bu durumda, başka bir Linux kutuda MySQL'ın komut satırı aracı kullanılır:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-207">In this case, you used MySQL's command-line tool on another Linux box:</span></span>

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a><span data-ttu-id="f8bfc-208">El ile yük devrediliyor</span><span class="sxs-lookup"><span data-stu-id="f8bfc-208">Manually failing over</span></span>
<span data-ttu-id="f8bfc-209">Yük devretme işlemlerini MySQL kapatılıyor DRBD'ın birincil değiştirme ve MySQL yeniden başlatmayı benzetimini yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-209">You can simulate failovers by shutting down MySQL, switching DRBD's primary, and starting MySQL again.</span></span>

<span data-ttu-id="f8bfc-210">Bu görevi gerçekleştirmek için aşağıdaki kodu hadb01 üzerinde çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-210">To perform this task, run the following code on hadb01:</span></span>

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

<span data-ttu-id="f8bfc-211">Ardından, hadb02 üzerinde:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-211">Then, on hadb02:</span></span>

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

<span data-ttu-id="f8bfc-212">El ile yük devri sonra uzak sorgunuzu yineleyebilir ve mükemmel çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-212">After you fail over manually, you can repeat your remote query and it should work perfectly.</span></span>

## <a name="set-up-corosync"></a><span data-ttu-id="f8bfc-213">Corosync ayarlayın</span><span class="sxs-lookup"><span data-stu-id="f8bfc-213">Set up Corosync</span></span>
<span data-ttu-id="f8bfc-214">Corosync çalışmaya Pacemaker için gereken temel küme altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-214">Corosync is the underlying cluster infrastructure required for Pacemaker to work.</span></span> <span data-ttu-id="f8bfc-215">Pacemaker işlevindeki sinyal daha benzer kalırken sinyal (ve Ultramonkey gibi diğer yöntemleri), Corosync CRM işlevleri bölme içindir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-215">For Heartbeat (and other methodologies like Ultramonkey), Corosync is a split of the CRM functionalities, while Pacemaker remains more similar to Heartbeat in functionality.</span></span>

<span data-ttu-id="f8bfc-216">Ana Corosync için Azure üzerinde Corosync çok noktaya yayın üzerinden tek noktaya yayın iletişim tercih eder, ancak Microsoft Azure ağı yalnızca tek noktaya yayın destekler sınırlamadır.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-216">The main constraint for Corosync on Azure is that Corosync prefers multicast over broadcast over unicast communications, but Microsoft Azure networking only supports unicast.</span></span>

<span data-ttu-id="f8bfc-217">Neyse ki, Corosync çalışma tek noktaya yayın modu vardır.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-217">Fortunately, Corosync has a working unicast mode.</span></span> <span data-ttu-id="f8bfc-218">Tüm düğümlerin kendilerini arasında iletişim için IP adresleri de dahil olmak üzere, yapılandırma dosyalarındaki düğümleri tanımlama gerektiğini yalnızca gerçek sınırlamadır.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-218">The only real constraint is that because all nodes are not communicating among themselves, you need to define the nodes in your configuration files, including their IP addresses.</span></span> <span data-ttu-id="f8bfc-219">Tek noktaya yayın ve değişiklik adresi, düğüm listeler ve günlük dizinleri bağlamak için biz Corosync örnek dosyalarını kullanabilirsiniz (Ubuntu kullanan `/var/log/corosync` örnek kullanım dosyalar sırada `/var/log/cluster`) ve çekirdek araçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-219">We can use the Corosync example files for Unicast and change bind address, node lists, and logging directories (Ubuntu uses `/var/log/corosync` while the example files use `/var/log/cluster`), and enable quorum tools.</span></span>

> [!NOTE]
> <span data-ttu-id="f8bfc-220">Aşağıdaki `transport: udpu` yönergesi ve her iki düğüm için el ile tanımlanan IP adresi.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-220">Use the following `transport: udpu` directive and the manually defined IP addresses for both nodes.</span></span>

<span data-ttu-id="f8bfc-221">Aşağıdaki kod çalıştıracağınız `/etc/corosync/corosync.conf` iki düğüm için:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-221">Run the following code on `/etc/corosync/corosync.conf` for both nodes:</span></span>

    totem {
      version: 2
      crypto_cipher: none
      crypto_hash: none
      interface {
        ringnumber: 0
        bindnetaddr: 10.10.10.0
        mcastport: 5405
        ttl: 1
      }
      transport: udpu
    }

    logging {
      fileline: off
      to_logfile: yes
      to_syslog: yes
      logfile: /var/log/corosync/corosync.log
      debug: off
      timestamp: on
      logger_subsys {
        subsys: QUORUM
        debug: off
        }
      }

    nodelist {
      node {
        ring0_addr: 10.10.10.4
        nodeid: 1
      }

      node {
        ring0_addr: 10.10.10.5
        nodeid: 2
      }
    }

    quorum {
      provider: corosync_votequorum
    }

<span data-ttu-id="f8bfc-222">Her iki VM üzerindeki bu yapılandırma dosyasını kopyalayın ve her iki düğüm Corosync Başlat:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-222">Copy this configuration file on both VMs and start Corosync in both nodes:</span></span>

    sudo service start corosync

<span data-ttu-id="f8bfc-223">Hizmeti başlatılıyor, kısa süre sonra küme geçerli halka kurulacaktır ve çekirdek constituted.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-223">Shortly after starting the service, the cluster should be established in the current ring, and quorum should be constituted.</span></span> <span data-ttu-id="f8bfc-224">Bu işlev günlükleri gözden geçirme veya aşağıdaki kodu çalıştırarak kontrol edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-224">We can check this functionality by reviewing logs or by running the following code:</span></span>

    sudo corosync-quorumtool –l

<span data-ttu-id="f8bfc-225">Aşağıdaki görüntüye benzer bir çıktı görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-225">You will see output similar to the following image:</span></span>

![corosync quorumtool - m örnek çıkış](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a><span data-ttu-id="f8bfc-227">Pacemaker ayarlayın</span><span class="sxs-lookup"><span data-stu-id="f8bfc-227">Set up Pacemaker</span></span>
<span data-ttu-id="f8bfc-228">Pacemaker küme kaynakları için izleme, ne zaman ana Git aşağı tanımlamak ve bu kaynakları için ikincil anahtar için kullanır.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-228">Pacemaker uses the cluster to monitor for resources, define when primaries go down, and switch those resources to secondaries.</span></span> <span data-ttu-id="f8bfc-229">Kaynakların kullanılabilir komut kümesi ya da LSB'si (Init benzeri) komut dosyaları, diğer seçenekler arasında tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-229">Resources can be defined from a set of available scripts or from LSB (init-like) scripts, among other choices.</span></span>

<span data-ttu-id="f8bfc-230">"DRBD kaynak, bağlama noktası ve MySQL hizmeti sahip olmasını" Pacemaker istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-230">We want Pacemaker to "own" the DRBD resource, the mount point, and the MySQL service.</span></span> <span data-ttu-id="f8bfc-231">Pacemaker DRBD açıp bağlama ve bunu çıkarın ve sonra durdurup başlatın hatalı bir şey birincil ile olduğunda MySQL doğru sırada, Kurulum işlemi tamamlanmış olur.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-231">If Pacemaker can turn on and off DRBD, mount and unmount it, and then start and stop MySQL in the right order when something bad happens with the primary, setup is complete.</span></span>

<span data-ttu-id="f8bfc-232">Pacemaker ilk kez yüklediğinizde, yapılandırmanızı gösterilene benzer yeteri kadar basit olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-232">When you first install Pacemaker, your configuration should be simple enough, something like:</span></span>

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. <span data-ttu-id="f8bfc-233">Çalıştırarak yapılandırmasını denetleyin `sudo crm configure show`.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-233">Check the configuration by running `sudo crm configure show`.</span></span>
2. <span data-ttu-id="f8bfc-234">Bir dosya oluşturun (gibi `/tmp/cluster.conf`) aşağıdaki kaynaklarla:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-234">Then create a file (like `/tmp/cluster.conf`) with the following resources:</span></span>

        primitive drbd_mysql ocf:linbit:drbd \
              params drbd_resource="r0" \
              op monitor interval="29s" role="Master" \
              op monitor interval="31s" role="Slave"

        ms ms_drbd_mysql drbd_mysql \
              meta master-max="1" master-node-max="1" \
                clone-max="2" clone-node-max="1" \
                notify="true"

        primitive fs_mysql ocf:heartbeat:Filesystem \
              params device="/dev/drbd/by-res/r0" \
              directory="/var/lib/mysql" fstype="ext3"

        primitive mysqld lsb:mysql

        group mysql fs_mysql mysqld

        colocation mysql_on_drbd \
               inf: mysql ms_drbd_mysql:Master

        order mysql_after_drbd \
               inf: ms_drbd_mysql:promote mysql:start

        property stonith-enabled=false

        property no-quorum-policy=ignore

3. <span data-ttu-id="f8bfc-235">Dosya yapılandırmaya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-235">Load the file into the configuration.</span></span> <span data-ttu-id="f8bfc-236">Yalnızca bu bir düğümünden yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-236">You only need to do this in one node.</span></span>

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. <span data-ttu-id="f8bfc-237">Pacemaker her iki düğüm önyüklemede başladığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-237">Make sure that Pacemaker starts at boot in both nodes:</span></span>

        sudo update-rc.d pacemaker defaults

5. <span data-ttu-id="f8bfc-238">Kullanarak `sudo crm_mon –L`, düğümlerinden biri için Küme Yöneticisi hale geldi ve tüm kaynakları çalıştıran doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-238">By using `sudo crm_mon –L`, verify that one of your nodes has become the master for the cluster and is running all the resources.</span></span> <span data-ttu-id="f8bfc-239">Kaynakları çalıştığını denetlemek için bağlama ve ps kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-239">You can use mount and ps to check that the resources are running.</span></span>

<span data-ttu-id="f8bfc-240">Aşağıdaki ekran görüntüsü gösterildiği `crm_mon` durdurulmuş bir düğümle (Ctrl + C seçerek çıkış):</span><span class="sxs-lookup"><span data-stu-id="f8bfc-240">The following screenshot shows `crm_mon` with one node stopped (exit by selecting Ctrl+C):</span></span>

![crm_mon düğüm durduruldu](./media/mysql-cluster/image002.png)

<span data-ttu-id="f8bfc-242">Bu ekran, düğüm, bir ana ve bir ikincil gösterir:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-242">This screenshot shows both nodes, one master and one slave:</span></span>

![crm_mon işletimsel ana/bağımlı](./media/mysql-cluster/image003.png)

## <a name="testing"></a><span data-ttu-id="f8bfc-244">Test Etme</span><span class="sxs-lookup"><span data-stu-id="f8bfc-244">Testing</span></span>
<span data-ttu-id="f8bfc-245">Otomatik Yük devretme benzetimi için hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-245">You're ready for an automatic failover simulation.</span></span> <span data-ttu-id="f8bfc-246">Bunu yapmanın iki yolu vardır: yazılım ve donanım.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-246">There are two ways to do this: soft and hard.</span></span>

<span data-ttu-id="f8bfc-247">Kümenin kapatma işlevi yumuşak biçimini kullanır: ``crm_standby -U `uname -n` -v on``.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-247">The soft way uses the cluster's shutdown function: ``crm_standby -U `uname -n` -v on``.</span></span> <span data-ttu-id="f8bfc-248">Bu ana kullanırsanız, ikincil devreye girer.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-248">If you use this on the master, the slave takes over.</span></span> <span data-ttu-id="f8bfc-249">Bu geri off olarak ayarlamayı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-249">Remember to set this back to off.</span></span> <span data-ttu-id="f8bfc-250">Bunu yapmazsanız, crm_mon bekleme tek bir düğüm gösterir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-250">If you don't, crm_mon will show one node on standby.</span></span>

<span data-ttu-id="f8bfc-251">Sabit şekilde portalı üzerinden veya çalışma düzeyi (diğer bir deyişle, durdurmak, kapatma) VM'de değiştirerek birincil VM (hadb01) kapatılıyor.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-251">The hard way is shutting down the primary VM (hadb01) via the portal or by changing the runlevel on the VM (that is, halt, shutdown).</span></span> <span data-ttu-id="f8bfc-252">Bu Corosync ve ana giderek aşağı sinyal tarafından Pacemaker yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-252">This helps Corosync and Pacemaker by signaling that the master's going down.</span></span> <span data-ttu-id="f8bfc-253">Bu test edebilirsiniz (Bakım pencereleri için yararlıdır), ancak Ayrıca, VM dondurma tarafından senaryo zorlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-253">You can test this (useful for maintenance windows), but you can also force the scenario by freezing the VM.</span></span>

## <a name="stonith"></a><span data-ttu-id="f8bfc-254">STONITH</span><span class="sxs-lookup"><span data-stu-id="f8bfc-254">STONITH</span></span>
<span data-ttu-id="f8bfc-255">VM kapatma fiziksel bir aygıtı denetleyen STONITH komut dosyası yerine Azure CLI aracılığıyla mümkün olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-255">It should be possible to issue a VM shutdown via the Azure CLI in lieu of a STONITH script that controls a physical device.</span></span> <span data-ttu-id="f8bfc-256">Kullanabileceğiniz `/usr/lib/stonith/plugins/external/ssh` Bankası ve kümenin yapılandırmasında STONITH etkinleştir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-256">You can use `/usr/lib/stonith/plugins/external/ssh` as a base and enable STONITH in the cluster's configuration.</span></span> <span data-ttu-id="f8bfc-257">Azure CLI genel olarak yüklenmelidir ve yayımlama ayarlarını ve profil kümenin kullanıcı için yüklenen.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-257">Azure CLI should be globally installed, and the publish settings and profile should be loaded for the cluster's user.</span></span>

<span data-ttu-id="f8bfc-258">Kaynak için örnek kod edinilebilir [GitHub](https://github.com/bureado/aztonith).</span><span class="sxs-lookup"><span data-stu-id="f8bfc-258">Sample code for the resource is available on [GitHub](https://github.com/bureado/aztonith).</span></span> <span data-ttu-id="f8bfc-259">Aşağıdakileri ekleyerek küme yapılandırmasını değiştirme `sudo crm configure`:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-259">Change the cluster's configuration by adding the following to `sudo crm configure`:</span></span>

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> <span data-ttu-id="f8bfc-260">Komut dosyası denetimleri yukarı/aşağı gerçekleştirmez.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-260">The script doesn't perform up/down checks.</span></span> <span data-ttu-id="f8bfc-261">15 ping denetimleri özgün SSH kaynak var, ancak bir Azure VM için kurtarma süresi daha fazla değişken olabilir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-261">The original SSH resource had 15 ping checks, but recovery time for an Azure VM might be more variable.</span></span>

## <a name="limitations"></a><span data-ttu-id="f8bfc-262">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="f8bfc-262">Limitations</span></span>
<span data-ttu-id="f8bfc-263">Aşağıdaki sınırlamalar uygulanır:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-263">The following limitations apply:</span></span>

* <span data-ttu-id="f8bfc-264">Bir kaynak olarak Pacemaker kullandığı DRBD yönetir linbit DRBD kaynak betik `drbdadm down` düğümü yalnızca bekleme durumuna geçiyor olsa bile bir düğüm kapanırken.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-264">The linbit DRBD resource script that manages DRBD as a resource in Pacemaker uses `drbdadm down` when shutting down a node, even if the node is just going on standby.</span></span> <span data-ttu-id="f8bfc-265">Asıl yazma alır ancak ikincil DRBD kaynak eşitleme değil çünkü bu ideal değildir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-265">This is not ideal because the slave will not be synchronizing the DRBD resource while the master gets writes.</span></span> <span data-ttu-id="f8bfc-266">Asıl graciously başarısız olmaz, ikincil daha eski bir dosya sistemi durumu alabilir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-266">If the master does not fail graciously, the slave can take over an older file system state.</span></span> <span data-ttu-id="f8bfc-267">Bu çözümü iki olası yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="f8bfc-267">There are two potential ways of solving this:</span></span>
  * <span data-ttu-id="f8bfc-268">Zorunlu bir `drbdadm up r0` tüm küme düğümlerinde yerel (clusterized değil) izleme olaylarını aracılığıyla içinde</span><span class="sxs-lookup"><span data-stu-id="f8bfc-268">Enforcing a `drbdadm up r0` in all cluster nodes via a local (not clusterized) watchdog</span></span>
  * <span data-ttu-id="f8bfc-269">Dikkat ederek linbit DRBD betik düzenleme `down` çağrılmaz`/usr/lib/ocf/resource.d/linbit/drbd`</span><span class="sxs-lookup"><span data-stu-id="f8bfc-269">Editing the linbit DRBD script, making sure that `down` is not called in `/usr/lib/ocf/resource.d/linbit/drbd`</span></span>
* <span data-ttu-id="f8bfc-270">Yük dengeleyicinin en az beş saniyede uygulamaları küme durumunu algılayan ve zaman aşımı süresi daha dayanıklı şekilde yanıt vermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-270">The load balancer needs at least five seconds to respond, so applications should be cluster-aware and be more tolerant of timeout.</span></span> <span data-ttu-id="f8bfc-271">Uygulama sıraları ve sorgu middlewares gibi diğer mimarileri de yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-271">Other architectures, like in-app queues and query middlewares, can also help.</span></span>
* <span data-ttu-id="f8bfc-272">MySQL ayarlama yazma yönetilebilir hızı yapılır ve bellek kaybını en aza indirmek için mümkün olduğunca sık diske önbellekleri Temizlenen sağlamak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-272">MySQL tuning is necessary to ensure that writing is done at a manageable pace and caches are flushed to disk as frequently as possible to minimize memory loss.</span></span>
* <span data-ttu-id="f8bfc-273">Yazma performansı VM'de bağımlı bu DRBD tarafından cihaz çoğaltmak için kullanılan mekanizma olduğundan sanal anahtarında birbirine.</span><span class="sxs-lookup"><span data-stu-id="f8bfc-273">Write performance is dependent in VM interconnect in the virtual switch because this is the mechanism used by DRBD to replicate the device.</span></span>
