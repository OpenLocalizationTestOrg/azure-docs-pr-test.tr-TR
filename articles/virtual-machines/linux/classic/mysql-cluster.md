---
title: "Yük dengeli kümeleri ile aaaClusterize MySQL | Microsoft Docs"
description: "Linux MySQL kümesi azure'da hello Klasik dağıtım modeliyle oluşturulan bir yük dengeli, yüksek kullanılabilirlik ayarlama"
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
ms.openlocfilehash: 1829fd877c4b0ed177b23a8e3404dbb3db746561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-load-balanced-sets-tooclusterize-mysql-on-linux"></a><span data-ttu-id="198e1-103">Yük dengeli kümeleri tooclusterize MySQL Linux'ta kullanın</span><span class="sxs-lookup"><span data-stu-id="198e1-103">Use load-balanced sets tooclusterize MySQL on Linux</span></span>
> [!IMPORTANT]
> <span data-ttu-id="198e1-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager](../../../resource-manager-deployment-model.md) ve klasik.</span><span class="sxs-lookup"><span data-stu-id="198e1-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="198e1-105">Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="198e1-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="198e1-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="198e1-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="198e1-107">A [Resource Manager şablonu](https://azure.microsoft.com/documentation/templates/mysql-replication/) toodeploy bir MySQL kümesi ihtiyacınız varsa kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="198e1-107">A [Resource Manager template](https://azure.microsoft.com/documentation/templates/mysql-replication/) is available if you need toodeploy a MySQL cluster.</span></span>

<span data-ttu-id="198e1-108">Bu makalede inceler ve hello farklı yaklaşımlar kullanılabilir toodeploy yüksek oranda kullanılabilir Linux tabanlı hizmetler MySQL Server yüksek kullanılabilirlik öncü olarak keşfetme Microsoft Azure üzerinde gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="198e1-108">This article explores and illustrates hello different approaches available toodeploy highly available Linux-based services on Microsoft Azure, exploring MySQL Server high availability as a primer.</span></span> <span data-ttu-id="198e1-109">Bu yaklaşım gösteren bir video kullanılabilir [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span><span class="sxs-lookup"><span data-stu-id="198e1-109">A video illustrating this approach is available on [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span></span>

<span data-ttu-id="198e1-110">Biz DRBD, Corosync ve Pacemaker göre hiçbir şey paylaşılmayan, iki düğümlü ve tek yöneticili MySQL yüksek kullanılabilirlik çözümü özetler.</span><span class="sxs-lookup"><span data-stu-id="198e1-110">We will outline a shared-nothing, two-node, single-master MySQL high availability solution based on DRBD, Corosync, and Pacemaker.</span></span> <span data-ttu-id="198e1-111">Yalnızca bir düğüm MySQL aynı anda çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="198e1-111">Only one node runs MySQL at a time.</span></span> <span data-ttu-id="198e1-112">Okuma ve yazma DRBD kaynak hello de sınırlı tooonly bir aynı anda düğümdür.</span><span class="sxs-lookup"><span data-stu-id="198e1-112">Reading and writing from hello DRBD resource is also limited tooonly one node at a time.</span></span>

<span data-ttu-id="198e1-113">Microsoft Azure tooprovide hepsini işlevselliği ve uç nokta algılama, kaldırma ve hello VIP normal kurtarılması yük dengelemeli kümelerinde kullanacağınız çünkü LVS gibi bir VIP çözümü için gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="198e1-113">There's no need for a VIP solution like LVS, because you'll use load-balanced sets in Microsoft Azure tooprovide round-robin functionality and endpoint detection, removal, and graceful recovery of hello VIP.</span></span> <span data-ttu-id="198e1-114">Merhaba VIP hello bulut hizmeti ilk oluşturduğunuzda Microsoft Azure tarafından atanan genel olarak yönlendirilebilir bir IPv4 adresi değil.</span><span class="sxs-lookup"><span data-stu-id="198e1-114">hello VIP is a globally routable IPv4 address assigned by Microsoft Azure when you first create hello cloud service.</span></span>

<span data-ttu-id="198e1-115">Diğer olası mimari NBD küme, Percona, Galera ve en az bir de dahil olmak üzere çeşitli ara yazılımı çözümler de dahil olmak üzere MySQL için bir VM olarak kullanılabilir [VM deposu](http://vmdepot.msopentech.com).</span><span class="sxs-lookup"><span data-stu-id="198e1-115">There are other possible architectures for MySQL, including NBD Cluster, Percona, Galera, and several middleware solutions, including at least one available as a VM on [VM Depot](http://vmdepot.msopentech.com).</span></span> <span data-ttu-id="198e1-116">Bu çözümlerin tek noktaya yayın ve çok noktaya yayın veya yayın üzerinde çoğaltabilir ve paylaşılan depolama ortamı veya birden çok ağ arabirimi güvenmeyin sürece hello senaryoları kolay toodeploy Microsoft Azure üzerinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="198e1-116">As long as these solutions can replicate on unicast vs. multicast or broadcast and don't rely on shared storage or multiple network interfaces, hello scenarios should be easy toodeploy on Microsoft Azure.</span></span>

<span data-ttu-id="198e1-117">Bunlar mimarileri kümeleme PostgreSQL ve OpenLDAP gibi tooother ürün benzer bir şekilde genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="198e1-117">These clustering architectures can be extended tooother products like PostgreSQL and OpenLDAP in a similar fashion.</span></span> <span data-ttu-id="198e1-118">Örneğin, bu yük dengeleyici yordamı paylaşılmadığı ile başarıyla çok ana OpenLDAP ile test edilmiştir ve bizim Channel 9 blogunda izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="198e1-118">For example, this load-balancing procedure with shared nothing was successfully tested with multi-master OpenLDAP, and you can watch it on our Channel 9 blog.</span></span>

## <a name="get-ready"></a><span data-ttu-id="198e1-119">Hazırlanma</span><span class="sxs-lookup"><span data-stu-id="198e1-119">Get ready</span></span>
<span data-ttu-id="198e1-120">Merhaba aşağıdakiler kaynakları ve yeteneklerini:</span><span class="sxs-lookup"><span data-stu-id="198e1-120">You need hello following resources and abilities:</span></span>

  - <span data-ttu-id="198e1-121">Bir Microsoft Azure hesap mümkün toocreate bir geçerli abonelik en az iki sanal makineleri (Bu örnekte XS kullanılan)</span><span class="sxs-lookup"><span data-stu-id="198e1-121">A Microsoft Azure account with a valid subscription, able toocreate at least two VMs (XS was used in this example)</span></span>
  - <span data-ttu-id="198e1-122">Bir ağ ve bir alt ağ</span><span class="sxs-lookup"><span data-stu-id="198e1-122">A network and a subnet</span></span>
  - <span data-ttu-id="198e1-123">Bir benzeşim grubu</span><span class="sxs-lookup"><span data-stu-id="198e1-123">An affinity group</span></span>
  - <span data-ttu-id="198e1-124">Bir kullanılabilirlik kümesi</span><span class="sxs-lookup"><span data-stu-id="198e1-124">An availability set</span></span>
  - <span data-ttu-id="198e1-125">özelliği toocreate VHD'ler hello hello hello bulut hizmeti ile aynı bölgeye ve toohello Linux VM'ler ekleme</span><span class="sxs-lookup"><span data-stu-id="198e1-125">hello ability toocreate VHDs in hello same region as hello cloud service and attach them toohello Linux VMs</span></span>

### <a name="tested-environment"></a><span data-ttu-id="198e1-126">Sınanan ortamı</span><span class="sxs-lookup"><span data-stu-id="198e1-126">Tested environment</span></span>
* <span data-ttu-id="198e1-127">Ubuntu 13.10</span><span class="sxs-lookup"><span data-stu-id="198e1-127">Ubuntu 13.10</span></span>
  * <span data-ttu-id="198e1-128">DRBD</span><span class="sxs-lookup"><span data-stu-id="198e1-128">DRBD</span></span>
  * <span data-ttu-id="198e1-129">MySQL sunucusu</span><span class="sxs-lookup"><span data-stu-id="198e1-129">MySQL Server</span></span>
  * <span data-ttu-id="198e1-130">Corosync ve Pacemaker</span><span class="sxs-lookup"><span data-stu-id="198e1-130">Corosync and Pacemaker</span></span>

### <a name="affinity-group"></a><span data-ttu-id="198e1-131">Benzeşim grubu</span><span class="sxs-lookup"><span data-stu-id="198e1-131">Affinity group</span></span>
<span data-ttu-id="198e1-132">Toohello Klasik Azure portalında oturum açarak hello çözüm için benzeşim grubu oluşturmak seçme **ayarları**ve bir benzeşim grubu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="198e1-132">Create an affinity group for hello solution by signing in toohello Azure classic portal, selecting **Settings**, and creating an affinity group.</span></span> <span data-ttu-id="198e1-133">Daha sonra oluşturulan ayrılan kaynakları toothis benzeşim grubu atanır.</span><span class="sxs-lookup"><span data-stu-id="198e1-133">Allocated resources created later will be assigned toothis affinity group.</span></span>

### <a name="networks"></a><span data-ttu-id="198e1-134">Ağlar</span><span class="sxs-lookup"><span data-stu-id="198e1-134">Networks</span></span>
<span data-ttu-id="198e1-135">Yeni bir ağ oluşturulur ve bir alt ağ hello ağı içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="198e1-135">A new network is created, and a subnet is created inside hello network.</span></span> <span data-ttu-id="198e1-136">Bu örnek 10.10.10.0/24 ağ içinde yalnızca bir /24 alt ağ ile kullanır.</span><span class="sxs-lookup"><span data-stu-id="198e1-136">This example uses a 10.10.10.0/24 network with only one /24 subnet inside.</span></span>

### <a name="virtual-machines"></a><span data-ttu-id="198e1-137">Sanal makineler</span><span class="sxs-lookup"><span data-stu-id="198e1-137">Virtual machines</span></span>
<span data-ttu-id="198e1-138">ilk Ubuntu 13.10 VM Endorsed Ubuntu galeri görüntüsü kullanılarak oluşturulur ve adlandırılır hello `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="198e1-138">hello first Ubuntu 13.10 VM is created by using an Endorsed Ubuntu Gallery image and is called `hadb01`.</span></span> <span data-ttu-id="198e1-139">Yeni bir bulut hizmeti hadb adlandırılan hello işlemde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="198e1-139">A new cloud service is created in hello process, called hadb.</span></span> <span data-ttu-id="198e1-140">Bu ad paylaşılan hello daha fazla kaynak eklendiğinde, hello hizmet olacak yük dengeli yapısı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="198e1-140">This name illustrates hello shared, load-balanced nature that hello service will have when more resources are added.</span></span> <span data-ttu-id="198e1-141">Merhaba oluşturulmasını `hadb01` hello portal olaysız ve tamamlanan kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="198e1-141">hello creation of `hadb01` is uneventful and completed by using hello portal.</span></span> <span data-ttu-id="198e1-142">SSH için bir uç nokta otomatik olarak oluşturulur ve hello yeni bir ağ seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="198e1-142">An endpoint for SSH is automatically created, and hello new network is selected.</span></span> <span data-ttu-id="198e1-143">Artık kullanılabilirlik Merhaba VM'ler kümesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="198e1-143">Now you can create an availability set for hello VMs.</span></span>

<span data-ttu-id="198e1-144">İlk VM (teknik olarak hello bulut hizmeti oluşturulduğunda) oluşturulur hello sonra oluşturma ikinci VM hello `hadb02`.</span><span class="sxs-lookup"><span data-stu-id="198e1-144">After hello first VM is created (technically, when hello cloud service is created), create hello second VM, `hadb02`.</span></span> <span data-ttu-id="198e1-145">Merhaba VM ikinci, Ubuntu 13.10 VM galeri hello hello portal kullanarak, ancak var olan bir bulut hizmetini kullanın `hadb.cloudapp.net`, yeni bir tane oluşturmak yerine.</span><span class="sxs-lookup"><span data-stu-id="198e1-145">For hello second VM, use Ubuntu 13.10 VM from hello Gallery by using hello portal, but use an existing cloud service, `hadb.cloudapp.net`, instead of creating a new one.</span></span> <span data-ttu-id="198e1-146">Merhaba ağ ve kullanılabilirlik kümesi otomatik olarak seçilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="198e1-146">hello network and availability set should be automatically selected.</span></span> <span data-ttu-id="198e1-147">Bir SSH uç noktası, çok oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="198e1-147">An SSH endpoint will be created, too.</span></span>

<span data-ttu-id="198e1-148">Her iki VM oluşturulduktan sonra hello SSH bağlantı noktası için not edin `hadb01` (TCP 22) ve `hadb02` (otomatik olarak Azure tarafından atanan).</span><span class="sxs-lookup"><span data-stu-id="198e1-148">After both VMs have been created, take note of hello SSH port for `hadb01` (TCP 22) and `hadb02` (automatically assigned by Azure).</span></span>

### <a name="attached-storage"></a><span data-ttu-id="198e1-149">Bağlı depolama</span><span class="sxs-lookup"><span data-stu-id="198e1-149">Attached storage</span></span>
<span data-ttu-id="198e1-150">Yeni bir disk tooboth VM'ler ekleyin ve hello işleminde 5 GB disk oluşturun.</span><span class="sxs-lookup"><span data-stu-id="198e1-150">Attach a new disk tooboth VMs and create 5-GB disks in hello process.</span></span> <span data-ttu-id="198e1-151">Merhaba diskleri hello VHD kapsayıcısı ana işletim sistemi diskleriniz için kullanımda barındırılır.</span><span class="sxs-lookup"><span data-stu-id="198e1-151">hello disks are hosted in hello VHD container in use for your main operating system disks.</span></span> <span data-ttu-id="198e1-152">Diskleri oluşturup bağlı sonra var. olduğundan hiçbir gerek toorestart Linux hello çekirdek hello yeni cihaz görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="198e1-152">After disks are created and attached, there is no need toorestart Linux because hello kernel will see hello new device.</span></span> <span data-ttu-id="198e1-153">Bu aygıt genellikle değil `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="198e1-153">This device is usually `/dev/sdc`.</span></span> <span data-ttu-id="198e1-154">Denetleme `dmesg` hello çıktı.</span><span class="sxs-lookup"><span data-stu-id="198e1-154">Check `dmesg` for hello output.</span></span>

<span data-ttu-id="198e1-155">Kullanarak her bir VM üzerinde bir bölüm oluşturmak `cfdisk` (birincil, Linux bölüm) ve hello yeni bölüm tablosu yazma.</span><span class="sxs-lookup"><span data-stu-id="198e1-155">On each VM, create a partition by using `cfdisk` (primary, Linux partition) and write hello new partition table.</span></span> <span data-ttu-id="198e1-156">Bir dosya sistemi bu bölüme oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="198e1-156">Do not create a file system on this partition.</span></span>

## <a name="set-up-hello-cluster"></a><span data-ttu-id="198e1-157">Merhaba kümesi</span><span class="sxs-lookup"><span data-stu-id="198e1-157">Set up hello cluster</span></span>
<span data-ttu-id="198e1-158">Her iki Ubuntu VM APT tooinstall Corosync, Pacemaker ve DRBD kullanın.</span><span class="sxs-lookup"><span data-stu-id="198e1-158">Use APT tooinstall Corosync, Pacemaker, and DRBD on both Ubuntu VMs.</span></span> <span data-ttu-id="198e1-159">toodo ile bunu `apt-get`çalıştırın hello aşağıdaki kodu:</span><span class="sxs-lookup"><span data-stu-id="198e1-159">toodo so with `apt-get`, run hello following code:</span></span>

    sudo apt-get install corosync pacemaker drbd8-utils.

<span data-ttu-id="198e1-160">MySQL şu anda yüklemeyin.</span><span class="sxs-lookup"><span data-stu-id="198e1-160">Do not install MySQL at this time.</span></span> <span data-ttu-id="198e1-161">Debian ve Ubuntu yükleme betikleri başlatma MySQL veri dizini üzerinde `/var/lib/mysql`, ancak hello dizin DRBD dosya sistemi tarafından değiştirilen çünkü daha sonra MySQL tooinstall gerekir.</span><span class="sxs-lookup"><span data-stu-id="198e1-161">Debian and Ubuntu installation scripts will initialize a MySQL data directory on `/var/lib/mysql`, but because hello directory will be superseded by a DRBD file system, you need tooinstall MySQL later.</span></span>

<span data-ttu-id="198e1-162">Doğrulayın (kullanarak `/sbin/ifconfig`) her iki VM hello 10.10.10.0/24 alt ağ adresleri ve bunların birbirlerine ada göre ping atabildiğinizi kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="198e1-162">Verify (by using `/sbin/ifconfig`) that both VMs are using addresses in hello 10.10.10.0/24 subnet and that they can ping each other by name.</span></span> <span data-ttu-id="198e1-163">Aynı zamanda `ssh-keygen` ve `ssh-copy-id` toomake emin her iki VM, bir parola gerektirmeden SSH yoluyla kurabilir.</span><span class="sxs-lookup"><span data-stu-id="198e1-163">You can also use `ssh-keygen` and `ssh-copy-id` toomake sure both VMs can communicate via SSH without requiring a password.</span></span>

### <a name="set-up-drbd"></a><span data-ttu-id="198e1-164">DRBD ayarlayın</span><span class="sxs-lookup"><span data-stu-id="198e1-164">Set up DRBD</span></span>
<span data-ttu-id="198e1-165">Merhaba temel kullanan DRBD kaynak oluşturma `/dev/sdc1` tooproduce bölüm bir `/dev/drbd1` ext3 kullanılarak biçimlendirilmiş ve birincil ve ikincil düğüm kullanılan kaynak.</span><span class="sxs-lookup"><span data-stu-id="198e1-165">Create a DRBD resource that uses hello underlying `/dev/sdc1` partition tooproduce a `/dev/drbd1` resource that can be formatted by using ext3 and used in both primary and secondary nodes.</span></span>

1. <span data-ttu-id="198e1-166">Açık `/etc/drbd.d/r0.res` ve kopyalama hello her iki sanal makinelerin kaynak tanımı aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="198e1-166">Open `/etc/drbd.d/r0.res` and copy hello following resource definition on both VMs:</span></span>

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

2. <span data-ttu-id="198e1-167">Merhaba kaynak kullanarak başlatmak `drbdadm` her iki VM üzerinde:</span><span class="sxs-lookup"><span data-stu-id="198e1-167">Initialize hello resource by using `drbdadm` on both VMs:</span></span>

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. <span data-ttu-id="198e1-168">Üzerinde birincil VM hello (`hadb01`), hello DRBD kaynak (birincil) sahipliğini zorla:</span><span class="sxs-lookup"><span data-stu-id="198e1-168">On hello primary VM (`hadb01`), force ownership (primary) of hello DRBD resource:</span></span>

        sudo drbdadm primary --force r0

<span data-ttu-id="198e1-169">/ Proc/drbd Merhaba içeriğine incelerseniz (`sudo cat /proc/drbd`) her iki VM üzerinde görmelisiniz `Primary/Secondary` üzerinde `hadb01` ve `Secondary/Primary` üzerinde `hadb02`, bu noktada hello çözümü ile tutarlı.</span><span class="sxs-lookup"><span data-stu-id="198e1-169">If you examine hello contents of /proc/drbd (`sudo cat /proc/drbd`) on both VMs, you should see `Primary/Secondary` on `hadb01` and `Secondary/Primary` on `hadb02`, consistent with hello solution at this point.</span></span> <span data-ttu-id="198e1-170">Merhaba 5 GB disk, hiçbir ücret toocustomers hello 10.10.10.0/24 ağ üzerinden eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="198e1-170">hello 5-GB disk is synchronized over hello 10.10.10.0/24 network at no charge toocustomers.</span></span>

<span data-ttu-id="198e1-171">Merhaba disk eşitlendikten sonra hello dosya sistemi üzerinde oluşturabileceğiniz `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="198e1-171">After hello disk is synchronized, you can create hello file system on `hadb01`.</span></span> <span data-ttu-id="198e1-172">Test amacıyla, ext2 kullandık ancak koddan hello ext3 dosya sistemi oluşturacak:</span><span class="sxs-lookup"><span data-stu-id="198e1-172">For testing purposes, we used ext2, but hello following code will create an ext3 file system:</span></span>

    mkfs.ext3 /dev/drbd1

### <a name="mount-hello-drbd-resource"></a><span data-ttu-id="198e1-173">Merhaba DRBD kaynak Bağla</span><span class="sxs-lookup"><span data-stu-id="198e1-173">Mount hello DRBD resource</span></span>
<span data-ttu-id="198e1-174">Merhaba DRBD kaynakları artık hazır toomount olduğunuz `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="198e1-174">You're now ready toomount hello DRBD resources on `hadb01`.</span></span> <span data-ttu-id="198e1-175">Debian ve türevleri kullanım `/var/lib/mysql` MySQL'ın veri dizini olarak.</span><span class="sxs-lookup"><span data-stu-id="198e1-175">Debian and derivatives use `/var/lib/mysql` as MySQL's data directory.</span></span> <span data-ttu-id="198e1-176">MySQL yüklemediniz çünkü hello dizin oluşturun ve hello DRBD kaynak bağlayın.</span><span class="sxs-lookup"><span data-stu-id="198e1-176">Because you haven't installed MySQL, create hello directory and mount hello DRBD resource.</span></span> <span data-ttu-id="198e1-177">tooperform kod aşağıdaki hello çalıştırmak, bu seçenek `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="198e1-177">tooperform this option, run hello following code on `hadb01`:</span></span>

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a><span data-ttu-id="198e1-178">MySQL ayarlayın</span><span class="sxs-lookup"><span data-stu-id="198e1-178">Set up MySQL</span></span>
<span data-ttu-id="198e1-179">Şimdi kullandığınız hazır tooinstall MySQL `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="198e1-179">Now you're ready tooinstall MySQL on `hadb01`:</span></span>

    sudo apt-get install mysql-server

<span data-ttu-id="198e1-180">İçin `hadb02`, iki seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="198e1-180">For `hadb02`, you have two options.</span></span> <span data-ttu-id="198e1-181">Mysql /var/lib/mysql oluşturmak, yeni bir veri dizin ile doldurun ve hello içerikleri kaldırmak sunuculu, yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="198e1-181">You can install mysql-server, which will create /var/lib/mysql, fill it with a new data directory, and then remove hello contents.</span></span> <span data-ttu-id="198e1-182">tooperform kod aşağıdaki hello çalıştırmak, bu seçenek `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="198e1-182">tooperform this option, run hello following code on `hadb02`:</span></span>

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

<span data-ttu-id="198e1-183">Merhaba ikinci seçenektir toofailover çok`hadb02` ve orada mysql server yükleyin.</span><span class="sxs-lookup"><span data-stu-id="198e1-183">hello second option is toofailover too`hadb02` and then install mysql-server there.</span></span> <span data-ttu-id="198e1-184">Yükleme betikleri hello mevcut yükleme görürsünüz ve dokunma olmaz.</span><span class="sxs-lookup"><span data-stu-id="198e1-184">Installation scripts will notice hello existing installation and won't touch it.</span></span>

<span data-ttu-id="198e1-185">Çalışma hello aşağıdaki kodu üzerinde `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="198e1-185">Run hello following code on `hadb01`:</span></span>

    sudo drbdadm secondary –force r0

<span data-ttu-id="198e1-186">Çalışma hello aşağıdaki kodu üzerinde `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="198e1-186">Run hello following code on `hadb02`:</span></span>

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

<span data-ttu-id="198e1-187">Toofailover DRBD şimdi planlamıyorsanız hello ilk seçenek tartışmaya açık bir şekilde daha az rağmen Zarif daha kolay olur.</span><span class="sxs-lookup"><span data-stu-id="198e1-187">If you don't plan toofailover DRBD now, hello first option is easier although arguably less elegant.</span></span> <span data-ttu-id="198e1-188">Bu ayarladıktan sonra MySQL veritabanınızı üzerinde çalışmaya başlayabiliriz.</span><span class="sxs-lookup"><span data-stu-id="198e1-188">After you set this up, you can start working on your MySQL database.</span></span> <span data-ttu-id="198e1-189">Çalışma hello aşağıdaki kodu üzerinde `hadb02` (veya hello sunucuları hangi biri tooDRBD göre etkin olan):</span><span class="sxs-lookup"><span data-stu-id="198e1-189">Run hello following code on `hadb02` (or whichever one of hello servers is active, according tooDRBD):</span></span>

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* tooroot;

> [!WARNING]
> <span data-ttu-id="198e1-190">Bu son deyim etkili bir şekilde bu tablodaki hello kök kullanıcı için kimlik doğrulaması devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="198e1-190">This last statement effectively disables authentication for hello root user in this table.</span></span> <span data-ttu-id="198e1-191">Bu üretim-sınıf tarafından değiştirilmesi gereken verme deyimleri ve yalnızca tanımlayıcı amaçlarla yer alır.</span><span class="sxs-lookup"><span data-stu-id="198e1-191">This should be replaced by your production-grade GRANT statements and is included only for illustrative purposes.</span></span>

<span data-ttu-id="198e1-192">(Bu kılavuzun amacı hello olan) dışında hello VM'ler toomake sorgularından isterseniz, ayrıca MySQL için ağ tooenable gerekir.</span><span class="sxs-lookup"><span data-stu-id="198e1-192">If you want toomake queries from outside hello VMs (which is hello purpose of this guide), you also need tooenable networking for MySQL.</span></span> <span data-ttu-id="198e1-193">Her iki VM üzerinde açmak `/etc/mysql/my.cnf` ve çok Git`bind-address`.</span><span class="sxs-lookup"><span data-stu-id="198e1-193">On both VMs, open `/etc/mysql/my.cnf` and go too`bind-address`.</span></span> <span data-ttu-id="198e1-194">Başlangıç adresi 127.0.0.1 değiştirmek too0.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="198e1-194">Change hello address from 127.0.0.1 too0.0.0.0.</span></span> <span data-ttu-id="198e1-195">Merhaba dosya kaydedildikten sonra sorun bir `sudo service mysql restart` geçerli birincil üzerinde.</span><span class="sxs-lookup"><span data-stu-id="198e1-195">After saving hello file, issue a `sudo service mysql restart` on your current primary.</span></span>

### <a name="create-hello-mysql-load-balanced-set"></a><span data-ttu-id="198e1-196">Merhaba MySQL yük dengeli kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="198e1-196">Create hello MySQL load-balanced set</span></span>
<span data-ttu-id="198e1-197">Toohello portalına geri dönün, çok Git`hadb01`ve seçin **uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="198e1-197">Go back toohello portal, go too`hadb01`, and choose **Endpoints**.</span></span> <span data-ttu-id="198e1-198">uç noktası, bir toocreate seçin MySQL (TCP 3306) hello aşağı açılan liste ve seçin **oluştur Yeni Yük dengeli kümesi**.</span><span class="sxs-lookup"><span data-stu-id="198e1-198">toocreate an endpoint, choose MySQL (TCP 3306) from hello drop-down list and select **Create new load balanced set**.</span></span> <span data-ttu-id="198e1-199">Ad hello yük dengeli uç nokta `lb-mysql`.</span><span class="sxs-lookup"><span data-stu-id="198e1-199">Name hello load-balanced endpoint `lb-mysql`.</span></span> <span data-ttu-id="198e1-200">Ayarlama **zaman** too5 saniye, en düşük.</span><span class="sxs-lookup"><span data-stu-id="198e1-200">Set **Time** too5 seconds, minimum.</span></span>

<span data-ttu-id="198e1-201">Merhaba endpoint oluşturduktan sonra çok Git`hadb02`, seçin **uç noktaları**ve bir uç nokta oluşturun.</span><span class="sxs-lookup"><span data-stu-id="198e1-201">After you create hello endpoint, go too`hadb02`, choose **Endpoints**, and create an endpoint.</span></span> <span data-ttu-id="198e1-202">Seçin `lb-mysql`ve ardından MySQL hello aşağı açılan listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="198e1-202">Choose `lb-mysql`, and then select MySQL from hello drop-down list.</span></span> <span data-ttu-id="198e1-203">Bu adım için hello Azure CLI de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="198e1-203">You can also use hello Azure CLI for this step.</span></span>

<span data-ttu-id="198e1-204">Artık hello küme el ile işlem için gereken her şeyi sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="198e1-204">You now have everything you need for manual operation of hello cluster.</span></span>

### <a name="test-hello-load-balanced-set"></a><span data-ttu-id="198e1-205">Sınama Hello yük dengeli kümesi</span><span class="sxs-lookup"><span data-stu-id="198e1-205">Test hello load-balanced set</span></span>
<span data-ttu-id="198e1-206">Testleri bir dış makineden herhangi bir MySQL istemcisi kullanarak veya bir Azure Web sitesi olarak çalışan phpMyAdmin gibi belirli uygulamaları kullanarak gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="198e1-206">Tests can be performed from an outside machine by using any MySQL client, or by using certain applications, like phpMyAdmin running as an Azure website.</span></span> <span data-ttu-id="198e1-207">Bu durumda, başka bir Linux kutuda MySQL'ın komut satırı aracı kullanılır:</span><span class="sxs-lookup"><span data-stu-id="198e1-207">In this case, you used MySQL's command-line tool on another Linux box:</span></span>

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a><span data-ttu-id="198e1-208">El ile yük devrediliyor</span><span class="sxs-lookup"><span data-stu-id="198e1-208">Manually failing over</span></span>
<span data-ttu-id="198e1-209">Yük devretme işlemlerini MySQL kapatılıyor DRBD'ın birincil değiştirme ve MySQL yeniden başlatmayı benzetimini yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="198e1-209">You can simulate failovers by shutting down MySQL, switching DRBD's primary, and starting MySQL again.</span></span>

<span data-ttu-id="198e1-210">tooperform bu görevi hadb01 üzerinde koddan hello çalıştır:</span><span class="sxs-lookup"><span data-stu-id="198e1-210">tooperform this task, run hello following code on hadb01:</span></span>

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

<span data-ttu-id="198e1-211">Ardından, hadb02 üzerinde:</span><span class="sxs-lookup"><span data-stu-id="198e1-211">Then, on hadb02:</span></span>

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

<span data-ttu-id="198e1-212">El ile yük devri sonra uzak sorgunuzu yineleyebilir ve mükemmel çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="198e1-212">After you fail over manually, you can repeat your remote query and it should work perfectly.</span></span>

## <a name="set-up-corosync"></a><span data-ttu-id="198e1-213">Corosync ayarlayın</span><span class="sxs-lookup"><span data-stu-id="198e1-213">Set up Corosync</span></span>
<span data-ttu-id="198e1-214">Corosync Pacemaker toowork için gerekli hello temel küme altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="198e1-214">Corosync is hello underlying cluster infrastructure required for Pacemaker toowork.</span></span> <span data-ttu-id="198e1-215">Pacemaker işlevindeki daha benzer tooHeartbeat kalırken sinyal (ve Ultramonkey gibi diğer yöntemleri), Corosync hello CRM işlevleri, bir bölme içindir.</span><span class="sxs-lookup"><span data-stu-id="198e1-215">For Heartbeat (and other methodologies like Ultramonkey), Corosync is a split of hello CRM functionalities, while Pacemaker remains more similar tooHeartbeat in functionality.</span></span>

<span data-ttu-id="198e1-216">Merhaba ana Corosync için Azure üzerinde Corosync çok noktaya yayın üzerinden tek noktaya yayın iletişim tercih eder, ancak Microsoft Azure ağı yalnızca tek noktaya yayın destekler sınırlamadır.</span><span class="sxs-lookup"><span data-stu-id="198e1-216">hello main constraint for Corosync on Azure is that Corosync prefers multicast over broadcast over unicast communications, but Microsoft Azure networking only supports unicast.</span></span>

<span data-ttu-id="198e1-217">Neyse ki, Corosync çalışma tek noktaya yayın modu vardır.</span><span class="sxs-lookup"><span data-stu-id="198e1-217">Fortunately, Corosync has a working unicast mode.</span></span> <span data-ttu-id="198e1-218">Merhaba yalnızca gerçek tüm düğümlerin kendilerini arasında iletişim için IP adresleri de dahil olmak üzere, yapılandırma dosyalarında toodefine hello düğümleri gerekiyor sınırlamadır.</span><span class="sxs-lookup"><span data-stu-id="198e1-218">hello only real constraint is that because all nodes are not communicating among themselves, you need toodefine hello nodes in your configuration files, including their IP addresses.</span></span> <span data-ttu-id="198e1-219">Tek noktaya yayın ve değişiklik adresi, düğüm listeler ve günlük dizinleri bağlamak için biz hello Corosync örnek dosyalarını kullanabilirsiniz (Ubuntu kullanan `/var/log/corosync` hello örnek kullanım dosyalar sırada `/var/log/cluster`) ve çekirdek araçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="198e1-219">We can use hello Corosync example files for Unicast and change bind address, node lists, and logging directories (Ubuntu uses `/var/log/corosync` while hello example files use `/var/log/cluster`), and enable quorum tools.</span></span>

> [!NOTE]
> <span data-ttu-id="198e1-220">Merhaba aşağıdaki kullanın `transport: udpu` yönergesi hello el ile tanımlanan ve her iki düğüm için IP adresi.</span><span class="sxs-lookup"><span data-stu-id="198e1-220">Use hello following `transport: udpu` directive and hello manually defined IP addresses for both nodes.</span></span>

<span data-ttu-id="198e1-221">Çalışma hello aşağıdaki kodu üzerinde `/etc/corosync/corosync.conf` iki düğüm için:</span><span class="sxs-lookup"><span data-stu-id="198e1-221">Run hello following code on `/etc/corosync/corosync.conf` for both nodes:</span></span>

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

<span data-ttu-id="198e1-222">Her iki VM üzerindeki bu yapılandırma dosyasını kopyalayın ve her iki düğüm Corosync Başlat:</span><span class="sxs-lookup"><span data-stu-id="198e1-222">Copy this configuration file on both VMs and start Corosync in both nodes:</span></span>

    sudo service start corosync

<span data-ttu-id="198e1-223">Merhaba hizmeti başlatılıyor, kısa süre sonra hello küme hello geçerli halka kurulacaktır ve çekirdek constituted.</span><span class="sxs-lookup"><span data-stu-id="198e1-223">Shortly after starting hello service, hello cluster should be established in hello current ring, and quorum should be constituted.</span></span> <span data-ttu-id="198e1-224">Bu işlev günlükleri gözden geçirme veya koddan hello çalıştırarak kontrol edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="198e1-224">We can check this functionality by reviewing logs or by running hello following code:</span></span>

    sudo corosync-quorumtool –l

<span data-ttu-id="198e1-225">Görüntü aşağıdaki çıktı benzer toohello görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="198e1-225">You will see output similar toohello following image:</span></span>

![corosync quorumtool - m örnek çıkış](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a><span data-ttu-id="198e1-227">Pacemaker ayarlayın</span><span class="sxs-lookup"><span data-stu-id="198e1-227">Set up Pacemaker</span></span>
<span data-ttu-id="198e1-228">Pacemaker kullanır kaynaklar için küme toomonitor Merhaba, ne zaman ana Git aşağı tanımlamak ve bu kaynakları toosecondaries geçin.</span><span class="sxs-lookup"><span data-stu-id="198e1-228">Pacemaker uses hello cluster toomonitor for resources, define when primaries go down, and switch those resources toosecondaries.</span></span> <span data-ttu-id="198e1-229">Kaynakların kullanılabilir komut kümesi ya da LSB'si (Init benzeri) komut dosyaları, diğer seçenekler arasında tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="198e1-229">Resources can be defined from a set of available scripts or from LSB (init-like) scripts, among other choices.</span></span>

<span data-ttu-id="198e1-230">Pacemaker çok "kendi" Merhaba DRBD kaynak, hello bağlama noktası ve hello MySQL hizmeti istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="198e1-230">We want Pacemaker too"own" hello DRBD resource, hello mount point, and hello MySQL service.</span></span> <span data-ttu-id="198e1-231">Pacemaker DRBD açıp kapatabilirsiniz, bağlama ve bunu çıkarın ve ardından başlatabilir ve MySQL hello sırası bozuk bir şey olduğunda, Kurulum tamamlandıktan hello birincil ile olur sağ durdurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="198e1-231">If Pacemaker can turn on and off DRBD, mount and unmount it, and then start and stop MySQL in hello right order when something bad happens with hello primary, setup is complete.</span></span>

<span data-ttu-id="198e1-232">Pacemaker ilk kez yüklediğinizde, yapılandırmanızı gösterilene benzer yeteri kadar basit olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="198e1-232">When you first install Pacemaker, your configuration should be simple enough, something like:</span></span>

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. <span data-ttu-id="198e1-233">Çalıştırarak Hello yapılandırmasını denetleyin `sudo crm configure show`.</span><span class="sxs-lookup"><span data-stu-id="198e1-233">Check hello configuration by running `sudo crm configure show`.</span></span>
2. <span data-ttu-id="198e1-234">Bir dosya oluşturun (gibi `/tmp/cluster.conf`) kaynakları aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="198e1-234">Then create a file (like `/tmp/cluster.conf`) with hello following resources:</span></span>

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

3. <span data-ttu-id="198e1-235">Merhaba dosyasına hello yapılandırma yük.</span><span class="sxs-lookup"><span data-stu-id="198e1-235">Load hello file into hello configuration.</span></span> <span data-ttu-id="198e1-236">Yalnızca toodo bu bir düğümünden gerekir.</span><span class="sxs-lookup"><span data-stu-id="198e1-236">You only need toodo this in one node.</span></span>

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. <span data-ttu-id="198e1-237">Pacemaker her iki düğüm önyüklemede başladığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="198e1-237">Make sure that Pacemaker starts at boot in both nodes:</span></span>

        sudo update-rc.d pacemaker defaults

5. <span data-ttu-id="198e1-238">Kullanarak `sudo crm_mon –L`, düğümleriniz birini hello küme için hello Yöneticisi olur ve tüm hello kaynakları çalıştıran doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="198e1-238">By using `sudo crm_mon –L`, verify that one of your nodes has become hello master for hello cluster and is running all hello resources.</span></span> <span data-ttu-id="198e1-239">Merhaba kaynakları çalıştıran bağlama ve ps toocheck kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="198e1-239">You can use mount and ps toocheck that hello resources are running.</span></span>

<span data-ttu-id="198e1-240">Aşağıdaki ekran görüntüsü gösterildiği hello `crm_mon` durdurulmuş bir düğümle (Ctrl + C seçerek çıkış):</span><span class="sxs-lookup"><span data-stu-id="198e1-240">hello following screenshot shows `crm_mon` with one node stopped (exit by selecting Ctrl+C):</span></span>

![crm_mon düğüm durduruldu](./media/mysql-cluster/image002.png)

<span data-ttu-id="198e1-242">Bu ekran, düğüm, bir ana ve bir ikincil gösterir:</span><span class="sxs-lookup"><span data-stu-id="198e1-242">This screenshot shows both nodes, one master and one slave:</span></span>

![crm_mon işletimsel ana/bağımlı](./media/mysql-cluster/image003.png)

## <a name="testing"></a><span data-ttu-id="198e1-244">Test Etme</span><span class="sxs-lookup"><span data-stu-id="198e1-244">Testing</span></span>
<span data-ttu-id="198e1-245">Otomatik Yük devretme benzetimi için hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="198e1-245">You're ready for an automatic failover simulation.</span></span> <span data-ttu-id="198e1-246">Var olan iki yolu toodo bu: yazılım ve donanım.</span><span class="sxs-lookup"><span data-stu-id="198e1-246">There are two ways toodo this: soft and hard.</span></span>

<span data-ttu-id="198e1-247">Merhaba yumuşak şekilde hello kümenin kapatma işlevini kullanır: ``crm_standby -U `uname -n` -v on``.</span><span class="sxs-lookup"><span data-stu-id="198e1-247">hello soft way uses hello cluster's shutdown function: ``crm_standby -U `uname -n` -v on``.</span></span> <span data-ttu-id="198e1-248">Bu hello yöneticisinde kullanırsanız, hello bağımlı devreye girer.</span><span class="sxs-lookup"><span data-stu-id="198e1-248">If you use this on hello master, hello slave takes over.</span></span> <span data-ttu-id="198e1-249">Bu geri toooff tooset unutmayın.</span><span class="sxs-lookup"><span data-stu-id="198e1-249">Remember tooset this back toooff.</span></span> <span data-ttu-id="198e1-250">Bunu yapmazsanız, crm_mon bekleme tek bir düğüm gösterir.</span><span class="sxs-lookup"><span data-stu-id="198e1-250">If you don't, crm_mon will show one node on standby.</span></span>

<span data-ttu-id="198e1-251">Merhaba sabit şekilde kapanıyor hello birincil VM (hadb01) hello Portalı aracılığıyla veya değiştirerek hello hello (diğer bir deyişle, durdurmak, kapatma) VM üzerinde çalışma düzeyi.</span><span class="sxs-lookup"><span data-stu-id="198e1-251">hello hard way is shutting down hello primary VM (hadb01) via hello portal or by changing hello runlevel on hello VM (that is, halt, shutdown).</span></span> <span data-ttu-id="198e1-252">Bu Corosync ve Pacemaker bu hello Yöneticisi'nin giderek aşağı sinyal tarafından yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="198e1-252">This helps Corosync and Pacemaker by signaling that hello master's going down.</span></span> <span data-ttu-id="198e1-253">Bu test edebilirsiniz (Bakım pencereleri için yararlıdır), ancak Ayrıca, hello VM dondurma tarafından hello senaryo zorlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="198e1-253">You can test this (useful for maintenance windows), but you can also force hello scenario by freezing hello VM.</span></span>

## <a name="stonith"></a><span data-ttu-id="198e1-254">STONITH</span><span class="sxs-lookup"><span data-stu-id="198e1-254">STONITH</span></span>
<span data-ttu-id="198e1-255">Olası tooissue VM kapatma fiziksel bir aygıtı denetleyen STONITH komut dosyası yerine hello Azure CLI aracılığıyla olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="198e1-255">It should be possible tooissue a VM shutdown via hello Azure CLI in lieu of a STONITH script that controls a physical device.</span></span> <span data-ttu-id="198e1-256">Kullanabileceğiniz `/usr/lib/stonith/plugins/external/ssh` Bankası ve hello kümenin yapılandırmasında STONITH etkinleştir.</span><span class="sxs-lookup"><span data-stu-id="198e1-256">You can use `/usr/lib/stonith/plugins/external/ssh` as a base and enable STONITH in hello cluster's configuration.</span></span> <span data-ttu-id="198e1-257">Azure CLI genel olarak yüklenmesi gerekir ve yayımlama hello ayarları ve profil hello kümenin kullanıcı için yüklenen.</span><span class="sxs-lookup"><span data-stu-id="198e1-257">Azure CLI should be globally installed, and hello publish settings and profile should be loaded for hello cluster's user.</span></span>

<span data-ttu-id="198e1-258">Merhaba kaynak için örnek kod edinilebilir [GitHub](https://github.com/bureado/aztonith).</span><span class="sxs-lookup"><span data-stu-id="198e1-258">Sample code for hello resource is available on [GitHub](https://github.com/bureado/aztonith).</span></span> <span data-ttu-id="198e1-259">Merhaba çok aşağıdaki ekleyerek Hello kümenin yapılandırmasını değiştirme`sudo crm configure`:</span><span class="sxs-lookup"><span data-stu-id="198e1-259">Change hello cluster's configuration by adding hello following too`sudo crm configure`:</span></span>

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> <span data-ttu-id="198e1-260">Merhaba betik denetimleri yukarı/aşağı gerçekleştirmez.</span><span class="sxs-lookup"><span data-stu-id="198e1-260">hello script doesn't perform up/down checks.</span></span> <span data-ttu-id="198e1-261">15 ping denetimleri Hello özgün SSH kaynak var, ancak bir Azure VM için kurtarma süresi daha fazla değişken olabilir.</span><span class="sxs-lookup"><span data-stu-id="198e1-261">hello original SSH resource had 15 ping checks, but recovery time for an Azure VM might be more variable.</span></span>

## <a name="limitations"></a><span data-ttu-id="198e1-262">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="198e1-262">Limitations</span></span>
<span data-ttu-id="198e1-263">Merhaba aşağıdaki sınırlamalar uygulanır:</span><span class="sxs-lookup"><span data-stu-id="198e1-263">hello following limitations apply:</span></span>

* <span data-ttu-id="198e1-264">Merhaba, bir kaynak olarak Pacemaker kullandığı DRBD yöneten linbit DRBD kaynak komut dosyası `drbdadm down` hello düğüm yalnızca bekleme durumuna geçiyor olsa bile bir düğüm kapanırken.</span><span class="sxs-lookup"><span data-stu-id="198e1-264">hello linbit DRBD resource script that manages DRBD as a resource in Pacemaker uses `drbdadm down` when shutting down a node, even if hello node is just going on standby.</span></span> <span data-ttu-id="198e1-265">Hello Yöneticisi yazma alır ancak hello bağımlı hello DRBD kaynak eşitleme değil çünkü bu ideal değildir.</span><span class="sxs-lookup"><span data-stu-id="198e1-265">This is not ideal because hello slave will not be synchronizing hello DRBD resource while hello master gets writes.</span></span> <span data-ttu-id="198e1-266">Hello Yöneticisi graciously başarısız olmaz, hello bağımlı daha eski bir dosya sistemi durumu alabilir.</span><span class="sxs-lookup"><span data-stu-id="198e1-266">If hello master does not fail graciously, hello slave can take over an older file system state.</span></span> <span data-ttu-id="198e1-267">Bu çözümü iki olası yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="198e1-267">There are two potential ways of solving this:</span></span>
  * <span data-ttu-id="198e1-268">Zorunlu bir `drbdadm up r0` tüm küme düğümlerinde yerel (clusterized değil) izleme olaylarını aracılığıyla içinde</span><span class="sxs-lookup"><span data-stu-id="198e1-268">Enforcing a `drbdadm up r0` in all cluster nodes via a local (not clusterized) watchdog</span></span>
  * <span data-ttu-id="198e1-269">Merhaba linbit DRBD komut dosyası düzenleme, dikkat ederek `down` çağrılmaz`/usr/lib/ocf/resource.d/linbit/drbd`</span><span class="sxs-lookup"><span data-stu-id="198e1-269">Editing hello linbit DRBD script, making sure that `down` is not called in `/usr/lib/ocf/resource.d/linbit/drbd`</span></span>
* <span data-ttu-id="198e1-270">Böylece uygulamaları küme durumunu algılayan ve zaman aşımı süresi daha dayanıklı hello yük dengeleyicinin en az beş saniyede toorespond gerekir.</span><span class="sxs-lookup"><span data-stu-id="198e1-270">hello load balancer needs at least five seconds toorespond, so applications should be cluster-aware and be more tolerant of timeout.</span></span> <span data-ttu-id="198e1-271">Uygulama sıraları ve sorgu middlewares gibi diğer mimarileri de yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="198e1-271">Other architectures, like in-app queues and query middlewares, can also help.</span></span>
* <span data-ttu-id="198e1-272">MySQL ayarlama yazma yönetilebilir hızı yapılır gerekli tooensure ve önbellekleri temizlenmiş toodisk gibi bir sıklıkla olası toominimize bellek kaybı.</span><span class="sxs-lookup"><span data-stu-id="198e1-272">MySQL tuning is necessary tooensure that writing is done at a manageable pace and caches are flushed toodisk as frequently as possible toominimize memory loss.</span></span>
* <span data-ttu-id="198e1-273">Yazma performansı VM'de bağımlı bu DRBD tooreplicate hello aygıt tarafından kullanılan hello mekanizması olduğundan hello sanal anahtarda birbirine.</span><span class="sxs-lookup"><span data-stu-id="198e1-273">Write performance is dependent in VM interconnect in hello virtual switch because this is hello mechanism used by DRBD tooreplicate hello device.</span></span>
