---
title: "SAP HANA, kullanılabilirlik Azure sanal makineler (VM'ler) üzerinde aaaHigh | Microsoft Docs"
description: "SAP HANA Azure sanal makinelerde (VM'ler) yüksek kullanılabilirliğini kurun."
services: virtual-machines-linux
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: sedusch
ms.openlocfilehash: dcb9bb70594f9d97f8a888cec76300bcbe0bf1ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a><span data-ttu-id="2cc38-103">SAP HANA Azure sanal makinelerde (VM), yüksek kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="2cc38-103">High Availability of SAP HANA on Azure Virtual Machines (VMs)</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

[2205917]:https://launchpad.support.sap.com/#/notes/2205917
[1944799]:https://launchpad.support.sap.com/#/notes/1944799
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

<span data-ttu-id="2cc38-113">Şirket içi ya da HANA sistemi çoğaltması kullanmak veya paylaşılan depolama tooestablish yüksek kullanılabilirlik için SAP HANA kullanın.</span><span class="sxs-lookup"><span data-stu-id="2cc38-113">On-premises, you can use either HANA System Replication or use shared storage tooestablish high availability for SAP HANA.</span></span>
<span data-ttu-id="2cc38-114">Şu anda yalnızca HANA sistem çoğaltma ayarlama Azure üzerinde destekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="2cc38-114">We currently only support setting up HANA System Replication on Azure.</span></span> <span data-ttu-id="2cc38-115">SAP HANA çoğaltma, bir yönetici düğümü ve en az bir ikincil düğüm oluşur.</span><span class="sxs-lookup"><span data-stu-id="2cc38-115">SAP HANA Replication consists of one master node and at least one slave node.</span></span> <span data-ttu-id="2cc38-116">Merhaba ana düğüm üzerinde veri olan değişiklikleri toohello toohello bağımlı düğümleri eşzamanlı veya zaman uyumsuz olarak çoğaltılan.</span><span class="sxs-lookup"><span data-stu-id="2cc38-116">Changes toohello data on hello master node are replicated toohello slave nodes synchronously or asynchronously.</span></span>

<span data-ttu-id="2cc38-117">Bu makalede toodeploy hello sanal makineler, hello sanal makineleri yapılandırma, hello küme Framework'ü yüklemek, yüklemek ve nasıl SAP HANA sistem çoğaltma yapılandırma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2cc38-117">This article describes how toodeploy hello virtual machines, configure hello virtual machines, install hello cluster framework, install and configure SAP HANA System Replication.</span></span>
<span data-ttu-id="2cc38-118">Merhaba örnek yapılandırmaları, vb. örnek numarasını 03 yükleme komutları ve HANA sistem kimliği HDB kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2cc38-118">In hello example configurations, installation commands etc. instance number 03 and HANA System ID HDB is used.</span></span>

<span data-ttu-id="2cc38-119">SAP notlar ve incelemeleri önce aşağıdaki hello okuma</span><span class="sxs-lookup"><span data-stu-id="2cc38-119">Read hello following SAP Notes and papers first</span></span>

* <span data-ttu-id="2cc38-120">SAP Not [1928533], sahip olduğu:</span><span class="sxs-lookup"><span data-stu-id="2cc38-120">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="2cc38-121">SAP yazılım hello dağıtımı için desteklenen Azure VM boyutlarını listesi</span><span class="sxs-lookup"><span data-stu-id="2cc38-121">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="2cc38-122">Azure VM boyutlarını önemli kapasite bilgilerini</span><span class="sxs-lookup"><span data-stu-id="2cc38-122">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="2cc38-123">Desteklenen bir SAP yazılım ve işletim sistemi (OS) ve veritabanı birleşimler</span><span class="sxs-lookup"><span data-stu-id="2cc38-123">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="2cc38-124">Windows ve Microsoft Azure Linux için gerekli SAP çekirdek sürümü</span><span class="sxs-lookup"><span data-stu-id="2cc38-124">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>
* <span data-ttu-id="2cc38-125">SAP Not [2015553] azure'da SAP desteklenen SAP yazılım dağıtımları için önkoşulları listeler.</span><span class="sxs-lookup"><span data-stu-id="2cc38-125">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="2cc38-126">SAP Not [2205917] SUSE Linux Enterprise Server işletim sistemi ayarlarını SAP uygulamaları için önerilir</span><span class="sxs-lookup"><span data-stu-id="2cc38-126">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="2cc38-127">SAP Not [1944799] SAP HANA yönergeleri SUSE Linux Enterprise Server için SAP uygulamaları için vardır.</span><span class="sxs-lookup"><span data-stu-id="2cc38-127">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="2cc38-128">SAP Not [2178632] ayrıntılı Azure SAP için bildirilen tüm izleme ölçümleri hakkında bilgi sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2cc38-128">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="2cc38-129">SAP Not [2191498] hello Azure Linux için SAP konak Aracısı sürümünü istedi.</span><span class="sxs-lookup"><span data-stu-id="2cc38-129">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="2cc38-130">SAP Not [2243692] Linux Azure üzerinde SAP lisanslama hakkında bilgi vardır.</span><span class="sxs-lookup"><span data-stu-id="2cc38-130">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="2cc38-131">SAP Not [1984787] SUSE Linux Enterprise Server 12 hakkında genel bilgi yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="2cc38-131">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="2cc38-132">SAP Not [1999351] hello Azure Gelişmiş izleme uzantısı SAP için ek sorun giderme bilgileri içeriyor.</span><span class="sxs-lookup"><span data-stu-id="2cc38-132">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="2cc38-133">[SAP topluluk WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) SAP notları Linux için gerekli tüm sahiptir.</span><span class="sxs-lookup"><span data-stu-id="2cc38-133">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="2cc38-134">[Azure sanal makineleri planlama ve uygulama Linux üzerinde SAP için][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="2cc38-134">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="2cc38-135">[(Bu makalede) Linux'ta SAP için Azure sanal makineler dağıtımı][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="2cc38-135">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="2cc38-136">[Linux üzerinde SAP için Azure sanal makineleri DBMS dağıtımı][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="2cc38-136">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="2cc38-137">[SAP HANA SR performansı en iyi duruma getirilmiş senaryo] [ suse-hana-ha-guide] hello Kılavuzu, şirket içinde için SAP HANA sistem çoğaltma tüm gerekli bilgileri tooset içerir.</span><span class="sxs-lookup"><span data-stu-id="2cc38-137">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] hello guide contains all required information tooset up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="2cc38-138">Bu kılavuz, bir taban çizgisi olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="2cc38-138">Use this guide as a baseline.</span></span>

## <a name="deploying-linux"></a><span data-ttu-id="2cc38-139">Linux dağıtma</span><span class="sxs-lookup"><span data-stu-id="2cc38-139">Deploying Linux</span></span>

<span data-ttu-id="2cc38-140">SAP HANA Hello kaynak Aracısı SUSE Linux Enterprise Server SAP uygulamaları için dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="2cc38-140">hello resource agent for SAP HANA is included in SUSE Linux Enterprise Server for SAP Applications.</span></span>
<span data-ttu-id="2cc38-141">Hello Azure Market görüntü SUSE Linux Enterprise Server için SAP uygulamaları 12 BYOS toodeploy yeni sanal makineler kullanabilirsiniz (Getir bilgisayarınızı kendi abonelik) ile içerir.</span><span class="sxs-lookup"><span data-stu-id="2cc38-141">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 with BYOS (Bring Your Own Subscription) that you can use toodeploy new virtual machines.</span></span>

### <a name="manual-deployment"></a><span data-ttu-id="2cc38-142">El ile dağıtımı</span><span class="sxs-lookup"><span data-stu-id="2cc38-142">Manual Deployment</span></span>

1. <span data-ttu-id="2cc38-143">Kaynak Grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="2cc38-143">Create a Resource Group</span></span>
1. <span data-ttu-id="2cc38-144">Bir sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="2cc38-144">Create a Virtual Network</span></span>
1. <span data-ttu-id="2cc38-145">İki depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2cc38-145">Create two Storage Accounts</span></span>
1. <span data-ttu-id="2cc38-146">Kullanılabilirlik kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="2cc38-146">Create an Availability Set</span></span>  
   <span data-ttu-id="2cc38-147">Set max güncelleştirme etki alanı</span><span class="sxs-lookup"><span data-stu-id="2cc38-147">Set max update domain</span></span>
1. <span data-ttu-id="2cc38-148">Bir yük dengeleyiciye (dahili) oluşturma</span><span class="sxs-lookup"><span data-stu-id="2cc38-148">Create a Load Balancer (internal)</span></span>  
   <span data-ttu-id="2cc38-149">Yukarıdaki adımı VNET seçin</span><span class="sxs-lookup"><span data-stu-id="2cc38-149">Select VNET of step above</span></span>
1. <span data-ttu-id="2cc38-150">Sanal makine 1 oluşturun</span><span class="sxs-lookup"><span data-stu-id="2cc38-150">Create Virtual Machine 1</span></span>  
   <span data-ttu-id="2cc38-151">https://Portal.Azure.com/#Create/SuSE-byos.SLES-for-SAP-byos12-SP1</span><span class="sxs-lookup"><span data-stu-id="2cc38-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="2cc38-152">SAP uygulamaları 12 SP1 için SLES (BYOS)</span><span class="sxs-lookup"><span data-stu-id="2cc38-152">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="2cc38-153">1 depolama hesabı seçin</span><span class="sxs-lookup"><span data-stu-id="2cc38-153">Select Storage Account 1</span></span>  
   <span data-ttu-id="2cc38-154">Kullanılabilirlik kümesi seçin</span><span class="sxs-lookup"><span data-stu-id="2cc38-154">Select Availability Set</span></span>  
1. <span data-ttu-id="2cc38-155">Sanal makine 2 oluşturun</span><span class="sxs-lookup"><span data-stu-id="2cc38-155">Create Virtual Machine 2</span></span>  
   <span data-ttu-id="2cc38-156">https://Portal.Azure.com/#Create/SuSE-byos.SLES-for-SAP-byos12-SP1</span><span class="sxs-lookup"><span data-stu-id="2cc38-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="2cc38-157">SAP uygulamaları 12 SP1 için SLES (BYOS)</span><span class="sxs-lookup"><span data-stu-id="2cc38-157">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="2cc38-158">Depolama hesabı 2 seçin</span><span class="sxs-lookup"><span data-stu-id="2cc38-158">Select Storage Account 2</span></span>   
   <span data-ttu-id="2cc38-159">Kullanılabilirlik kümesi seçin</span><span class="sxs-lookup"><span data-stu-id="2cc38-159">Select Availability Set</span></span>  
1. <span data-ttu-id="2cc38-160">Veri diski Ekle</span><span class="sxs-lookup"><span data-stu-id="2cc38-160">Add Data Disks</span></span>
1. <span data-ttu-id="2cc38-161">Merhaba yük dengeleyici yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2cc38-161">Configure hello load balancer</span></span>
    1. <span data-ttu-id="2cc38-162">Bir ön uç IP havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="2cc38-162">Create a frontend IP pool</span></span>
        1. <span data-ttu-id="2cc38-163">Açık hello yük dengeleyici, ön uç IP havuzu seçin ve Ekle'yi tıklatın</span><span class="sxs-lookup"><span data-stu-id="2cc38-163">Open hello load balancer, select frontend IP pool and click Add</span></span>
        1. <span data-ttu-id="2cc38-164">Merhaba yeni ön uç IP havuzu (örneğin hana-ön uç) Hello adını girin</span><span class="sxs-lookup"><span data-stu-id="2cc38-164">Enter hello name of hello new frontend IP pool (for example hana-frontend)</span></span>
       1. <span data-ttu-id="2cc38-165">Tamam'ı tıklatın</span><span class="sxs-lookup"><span data-stu-id="2cc38-165">Click OK</span></span>
        1. <span data-ttu-id="2cc38-166">Merhaba yeni ön uç IP havuzu oluşturulduktan sonra IP adresini yazma</span><span class="sxs-lookup"><span data-stu-id="2cc38-166">After hello new frontend IP pool is created, write down its IP address</span></span>
    1. <span data-ttu-id="2cc38-167">Arka uç havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="2cc38-167">Create a backend pool</span></span>
        1. <span data-ttu-id="2cc38-168">Açık hello yük dengeleyici arka uç havuzlarını seçin ve Ekle'yi tıklatın</span><span class="sxs-lookup"><span data-stu-id="2cc38-168">Open hello load balancer, select backend pools and click Add</span></span>
        1. <span data-ttu-id="2cc38-169">Merhaba yeni arka uç havuzu (örneğin hana-arka uç) Hello adını girin</span><span class="sxs-lookup"><span data-stu-id="2cc38-169">Enter hello name of hello new backend pool (for example hana-backend)</span></span>
        1. <span data-ttu-id="2cc38-170">Bir sanal makine Ekle</span><span class="sxs-lookup"><span data-stu-id="2cc38-170">Click Add a virtual machine</span></span>
        1. <span data-ttu-id="2cc38-171">Merhaba daha önce oluşturduğunuz kullanılabilirlik kümesi seçin</span><span class="sxs-lookup"><span data-stu-id="2cc38-171">Select hello Availability Set you created earlier</span></span>
        1. <span data-ttu-id="2cc38-172">Merhaba SAP HANA kümesinin Hello sanal makineleri seçin</span><span class="sxs-lookup"><span data-stu-id="2cc38-172">Select hello virtual machines of hello SAP HANA cluster</span></span>
        1. <span data-ttu-id="2cc38-173">Tamam'ı tıklatın</span><span class="sxs-lookup"><span data-stu-id="2cc38-173">Click OK</span></span>
    1. <span data-ttu-id="2cc38-174">Bir sistem durumu araştırması oluştur</span><span class="sxs-lookup"><span data-stu-id="2cc38-174">Create a health probe</span></span>
       1. <span data-ttu-id="2cc38-175">Açık hello yük dengeleyici, sistem durumu araştırmalarının seçin ve Ekle'yi tıklatın</span><span class="sxs-lookup"><span data-stu-id="2cc38-175">Open hello load balancer, select health probes and click Add</span></span>
        1. <span data-ttu-id="2cc38-176">Merhaba yeni durumu araştırması (örneğin hana-hp) Hello adını girin</span><span class="sxs-lookup"><span data-stu-id="2cc38-176">Enter hello name of hello new health probe (for example hana-hp)</span></span>
        1. <span data-ttu-id="2cc38-177">TCP bağlantı noktası 625 protokolü olarak seçin**03**, aralığı 5 ile sağlıksız durum eşiği 2 tutun</span><span class="sxs-lookup"><span data-stu-id="2cc38-177">Select TCP as protocol, port 625**03**, keep Interval 5 and Unhealthy threshold 2</span></span>
        1. <span data-ttu-id="2cc38-178">Tamam'ı tıklatın</span><span class="sxs-lookup"><span data-stu-id="2cc38-178">Click OK</span></span>
    1. <span data-ttu-id="2cc38-179">Yük dengeleme kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="2cc38-179">Create load balancing rules</span></span>
        1. <span data-ttu-id="2cc38-180">Merhaba yük dengeleyici açın, Yük Dengeleme kuralları seçin ve Ekle'yi tıklatın</span><span class="sxs-lookup"><span data-stu-id="2cc38-180">Open hello load balancer, select load balancing rules and click Add</span></span>
        1. <span data-ttu-id="2cc38-181">Merhaba Yeni Yük Dengeleyici kuralı Hello adını girin (örneğin hana-lb-3**03**15)</span><span class="sxs-lookup"><span data-stu-id="2cc38-181">Enter hello name of hello new load balancer rule (for example hana-lb-3**03**15)</span></span>
        1. <span data-ttu-id="2cc38-182">Daha önce oluşturduğunuz (örneğin hana-ön uç) araştırma SELECT hello ön uç IP adresi, arka uç havuzu ve sistem durumu</span><span class="sxs-lookup"><span data-stu-id="2cc38-182">Select hello frontend IP address, backend pool and health probe you created earlier (for example hana-frontend)</span></span>
        1. <span data-ttu-id="2cc38-183">Protokol TCP tutmak için bağlantı noktası 3 girin**03**15</span><span class="sxs-lookup"><span data-stu-id="2cc38-183">Keep protocol TCP, enter port 3**03**15</span></span>
        1. <span data-ttu-id="2cc38-184">Boşta kalma zaman aşımı too30 dakika artırın</span><span class="sxs-lookup"><span data-stu-id="2cc38-184">Increase idle timeout too30 minutes</span></span>
       1. <span data-ttu-id="2cc38-185">**Emin tooenable olun kayan IP**</span><span class="sxs-lookup"><span data-stu-id="2cc38-185">**Make sure tooenable Floating IP**</span></span>
        1. <span data-ttu-id="2cc38-186">Tamam'ı tıklatın</span><span class="sxs-lookup"><span data-stu-id="2cc38-186">Click OK</span></span>
        1. <span data-ttu-id="2cc38-187">Bağlantı noktası 3 için yukarıdaki Hello adımları yineleyin**03**17</span><span class="sxs-lookup"><span data-stu-id="2cc38-187">Repeat hello steps above for port 3**03**17</span></span>

### <a name="deploy-with-template"></a><span data-ttu-id="2cc38-188">Şablon ile dağıtım</span><span class="sxs-lookup"><span data-stu-id="2cc38-188">Deploy with template</span></span>
<span data-ttu-id="2cc38-189">Merhaba hızlı başlangıç şablonlarından birini github toodeploy üzerinde gerekli tüm kaynakları kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="2cc38-189">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="2cc38-190">Merhaba şablon hello sanal makineler, hello yük dengeleyici, kullanılabilirlik vb. kümesi dağıtır. Bu adımları toodeploy hello şablon izleyin:</span><span class="sxs-lookup"><span data-stu-id="2cc38-190">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="2cc38-191">Açık hello [veritabanı şablonu] [ template-multisid-db] veya hello [şablonu Yakınsanan] [ template-converged] hello Azure portalı üzerinde hello veritabanı şablonu yalnızca hello oluşturur. Merhaba yakınsanmış şablonu da oluşturur ancak bir veritabanı için Yük Dengeleme kuralları ASCS/SCS ve ERS (yalnızca Linux) örneği için Yük Dengeleme kuralları hello.</span><span class="sxs-lookup"><span data-stu-id="2cc38-191">Open hello [database template][template-multisid-db] or hello [converged template][template-converged] on hello Azure Portal hello database template only creates hello load-balancing rules for a database whereas hello converged template also creates hello load-balancing rules for an ASCS/SCS and ERS (Linux only) instance.</span></span> <span data-ttu-id="2cc38-192">Tooinstall bir SAP NetWeaver temel sistem planlama ve ayrıca tooinstall hello istiyorsanız ASCS/SCS hello üzerinde aynı örnek makinelerini kullanma hello [şablonu Yakınsanan][template-converged].</span><span class="sxs-lookup"><span data-stu-id="2cc38-192">If you plan tooinstall an SAP NetWeaver based system and you also want tooinstall hello ASCS/SCS instance on hello same machines, use hello [converged template][template-converged].</span></span>
1. <span data-ttu-id="2cc38-193">Şu parametreler hello girin</span><span class="sxs-lookup"><span data-stu-id="2cc38-193">Enter hello following parameters</span></span>
    1. <span data-ttu-id="2cc38-194">SAP sistem kimliği</span><span class="sxs-lookup"><span data-stu-id="2cc38-194">Sap System Id</span></span>  
       <span data-ttu-id="2cc38-195">Merhaba tooinstall istediğiniz SAP sistemi Hello SAP sistemi kimliği girin.</span><span class="sxs-lookup"><span data-stu-id="2cc38-195">Enter hello SAP system Id of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="2cc38-196">Merhaba kimliği önek olarak dağıtılan hello kaynaklar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2cc38-196">hello Id will be used as a prefix for hello resources that are deployed.</span></span>
    1. <span data-ttu-id="2cc38-197">Yığın türü (yalnızca hello yakınsanmış şablonu kullanıyorsanız geçerlidir)</span><span class="sxs-lookup"><span data-stu-id="2cc38-197">Stack Type (only applicable if you use hello converged template)</span></span>  
       <span data-ttu-id="2cc38-198">Merhaba SAP NetWeaver yığın türünü seçin</span><span class="sxs-lookup"><span data-stu-id="2cc38-198">Select hello SAP NetWeaver stack type</span></span>
    1. <span data-ttu-id="2cc38-199">İşletim sistemi türü</span><span class="sxs-lookup"><span data-stu-id="2cc38-199">Os Type</span></span>  
       <span data-ttu-id="2cc38-200">Merhaba Linux dağıtımları birini seçin.</span><span class="sxs-lookup"><span data-stu-id="2cc38-200">Select one of hello Linux distributions.</span></span> <span data-ttu-id="2cc38-201">Bu örnekte, SLES 12 BYOS seçin</span><span class="sxs-lookup"><span data-stu-id="2cc38-201">For this example, select SLES 12 BYOS</span></span>
    1. <span data-ttu-id="2cc38-202">DB türü</span><span class="sxs-lookup"><span data-stu-id="2cc38-202">Db Type</span></span>  
       <span data-ttu-id="2cc38-203">HANA seçin</span><span class="sxs-lookup"><span data-stu-id="2cc38-203">Select HANA</span></span>
    1. <span data-ttu-id="2cc38-204">SAP sistemi boyutu</span><span class="sxs-lookup"><span data-stu-id="2cc38-204">Sap System Size</span></span>  
       <span data-ttu-id="2cc38-205">SAP hello yeni sistem Hello miktarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="2cc38-205">hello amount of SAPS hello new system will provide.</span></span> <span data-ttu-id="2cc38-206">SAP teknolojisi iş ortağı veya sistem Tümleştirici kaç SAP hello sistem gerektirir emin değilseniz Lütfen isteyin</span><span class="sxs-lookup"><span data-stu-id="2cc38-206">If you are not sure how many SAPS hello system will require, please ask your SAP Technology Partner or System Integrator</span></span>
    1. <span data-ttu-id="2cc38-207">Sistem kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="2cc38-207">System Availability</span></span>  
       <span data-ttu-id="2cc38-208">HA seçin</span><span class="sxs-lookup"><span data-stu-id="2cc38-208">Select HA</span></span>
    1. <span data-ttu-id="2cc38-209">Yönetici kullanıcı adı ve yönetici parolası</span><span class="sxs-lookup"><span data-stu-id="2cc38-209">Admin Username and Admin Password</span></span>  
       <span data-ttu-id="2cc38-210">Yeni bir kullanıcı oluşturulur toohello makinede kullanılan toolog olabilir.</span><span class="sxs-lookup"><span data-stu-id="2cc38-210">A new user is created that can be used toolog on toohello machine.</span></span>
    1. <span data-ttu-id="2cc38-211">Yeni veya var olan bir alt ağ</span><span class="sxs-lookup"><span data-stu-id="2cc38-211">New Or Existing Subnet</span></span>  
       <span data-ttu-id="2cc38-212">Yeni sanal ağ ve alt oluşturulmalıdır ya da mevcut bir alt kullanılması gerektiğini belirler.</span><span class="sxs-lookup"><span data-stu-id="2cc38-212">Determines whether a new virtual network and subnet should be created or an existing subnet should be used.</span></span> <span data-ttu-id="2cc38-213">Bağlı tooyour şirket içi ağ bir sanal ağ zaten varsa, varolan seçin.</span><span class="sxs-lookup"><span data-stu-id="2cc38-213">If you already have a virtual network that is connected tooyour on-premises network, select existing.</span></span>
    1. <span data-ttu-id="2cc38-214">Alt ağ kimliği</span><span class="sxs-lookup"><span data-stu-id="2cc38-214">Subnet Id</span></span>  
    <span data-ttu-id="2cc38-215">için Hello kimliği hello alt toowhich hello sanal makinelerin bağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2cc38-215">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span> <span data-ttu-id="2cc38-216">VPN veya hızlı rota sanal ağ tooconnect hello sanal makine tooyour Şirket ağınızın Hello alt ağ seçin.</span><span class="sxs-lookup"><span data-stu-id="2cc38-216">Select hello subnet of your VPN or Express Route virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="2cc38-217">Merhaba kimliği genellikle /subscriptions/ gibi görünüyor`<subscription id`> /resourceGroups/`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`></span><span class="sxs-lookup"><span data-stu-id="2cc38-217">hello ID usually looks like /subscriptions/`<subscription id`>/resourceGroups/`<resource group name`>/providers/Microsoft.Network/virtualNetworks/`<virtual network name`>/subnets/`<subnet name`></span></span>

## <a name="setting-up-linux-ha"></a><span data-ttu-id="2cc38-218">Ayarlama Linux HA</span><span class="sxs-lookup"><span data-stu-id="2cc38-218">Setting up Linux HA</span></span>

<span data-ttu-id="2cc38-219">Aşağıdaki öğelerindeki hello ya da ile [A] - geçerli tooall düğümleri, [1] - 1 veya [2] yalnızca geçerli toonode - yalnızca geçerli toonode 2 öneki alır.</span><span class="sxs-lookup"><span data-stu-id="2cc38-219">hello following items are prefixed with either [A] - applicable tooall nodes, [1] - only applicable toonode 1 or [2] - only applicable toonode 2.</span></span>

1. <span data-ttu-id="2cc38-220">[A] SAP yalnızca - BYOS kaydetmek SLES toobe mümkün toouse hello depoları için SLES</span><span class="sxs-lookup"><span data-stu-id="2cc38-220">[A] SLES for SAP BYOS only - Register SLES toobe able toouse hello repositories</span></span>
1. <span data-ttu-id="2cc38-221">[A] SLES SAP BYOS için yalnızca - genel bulut Modül Ekle</span><span class="sxs-lookup"><span data-stu-id="2cc38-221">[A] SLES for SAP BYOS only - Add public-cloud module</span></span>
1. <span data-ttu-id="2cc38-222">[A] güncelleştirme SLES</span><span class="sxs-lookup"><span data-stu-id="2cc38-222">[A] Update SLES</span></span>
    ```bash
    sudo zypper update

    ```

1. <span data-ttu-id="2cc38-223">[1] ssh erişimini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="2cc38-223">[1] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. <span data-ttu-id="2cc38-224">[2] ssh erişimini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="2cc38-224">[2] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa

    # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. <span data-ttu-id="2cc38-225">[1] ssh erişimini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="2cc38-225">[1] Enable ssh access</span></span>
    ```bash
    # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. <span data-ttu-id="2cc38-226">[A] HA uzantısını yükleyin</span><span class="sxs-lookup"><span data-stu-id="2cc38-226">[A] Install HA extension</span></span>
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. <span data-ttu-id="2cc38-227">[A] Kurulum disk düzeni</span><span class="sxs-lookup"><span data-stu-id="2cc38-227">[A] Setup disk layout</span></span>
    1. <span data-ttu-id="2cc38-228">LVM</span><span class="sxs-lookup"><span data-stu-id="2cc38-228">LVM</span></span>  
    <span data-ttu-id="2cc38-229">Genellikle veri ve günlük dosyalarını birimlerin toouse LVM öneririz.</span><span class="sxs-lookup"><span data-stu-id="2cc38-229">We generally recommend toouse LVM for volumes that store data and log files.</span></span> <span data-ttu-id="2cc38-230">Aşağıdaki Hello örnek hello sanal makineleri kullanılan toocreate iki birimlerin olmalıdır bağlı dört veri diskleri sahip olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="2cc38-230">hello example below assumes that hello virtual machines have four data disks attached that should be used toocreate two volumes.</span></span>
        * <span data-ttu-id="2cc38-231">Toouse istediğiniz tüm disklerin fiziksel birimler oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="2cc38-231">Create physical volumes for all disks that you want toouse.</span></span>
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * <span data-ttu-id="2cc38-232">Merhaba veri dosyaları için bir birim grubu, hello günlük dosyaları için bir birim grubu ve SAP HANA hello paylaşılan dizini için bir tane oluşturun</span><span class="sxs-lookup"><span data-stu-id="2cc38-232">Create a volume group for hello data files, one volume group for hello log files and one for hello shared directory of SAP HANA</span></span>
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * <span data-ttu-id="2cc38-233">Merhaba mantıksal birim oluşturun</span><span class="sxs-lookup"><span data-stu-id="2cc38-233">Create hello logical volumes</span></span>
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * <span data-ttu-id="2cc38-234">Merhaba bağlama dizinler oluşturun ve hello UUID tüm mantıksal birimlerin kopyalama</span><span class="sxs-lookup"><span data-stu-id="2cc38-234">Create hello mount directories and copy hello UUID of all logical volumes</span></span>
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * <span data-ttu-id="2cc38-235">Merhaba fstab girişlerinde üç mantıksal birim oluşturma</span><span class="sxs-lookup"><span data-stu-id="2cc38-235">Create fstab entries for hello three logical volumes</span></span>
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    <span data-ttu-id="2cc38-236">Bu satırı çok/etc/fstab Ekle</span><span class="sxs-lookup"><span data-stu-id="2cc38-236">Insert this line too/etc/fstab</span></span>
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * <span data-ttu-id="2cc38-237">Merhaba yeni birimleri bağlayın</span><span class="sxs-lookup"><span data-stu-id="2cc38-237">Mount hello new volumes</span></span>
    <pre><code>
    sudo mount -a
    </code></pre>
    1. <span data-ttu-id="2cc38-238">Düz diskleri</span><span class="sxs-lookup"><span data-stu-id="2cc38-238">Plain Disks</span></span>  
       <span data-ttu-id="2cc38-239">Küçük veya gösteri sistemleri HANA veri ve günlük dosyalarınızı bir disk yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="2cc38-239">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="2cc38-240">Merhaba aşağıdaki komutları /dev/sdc üzerinde bir bölüm oluşturun ve xfs ile biçimlendirin.</span><span class="sxs-lookup"><span data-stu-id="2cc38-240">hello following commands create a partition on /dev/sdc and format it with xfs.</span></span>
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-hello-id-of-devsdc1"></a><span data-ttu-id="2cc38-241">/dev/sdc1 Hello kimliği yazma</span><span class="sxs-lookup"><span data-stu-id="2cc38-241">write down hello id of /dev/sdc1</span></span>
    <span data-ttu-id="2cc38-242">sudo/sbin/blkid sudo VI/etc/fstab</span><span class="sxs-lookup"><span data-stu-id="2cc38-242">sudo /sbin/blkid  sudo vi /etc/fstab</span></span>
    ```

    Insert this line too/etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create hello target directory and mount hello disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. <span data-ttu-id="2cc38-243">[A] tüm ana bilgisayarlar için ana bilgisayar adı çözümlemesi Kurulumu</span><span class="sxs-lookup"><span data-stu-id="2cc38-243">[A] Setup host name resolution for all hosts</span></span>  
    <span data-ttu-id="2cc38-244">Bir DNS sunucusu kullanın veya tüm düğümlerde hello/etc/hosts değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2cc38-244">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="2cc38-245">Bu örnek nasıl toouse hello/etc/hosts dosyasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="2cc38-245">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="2cc38-246">Başlangıç IP adresi ve hello hostname komutları aşağıdaki hello olarak değiştirin</span><span class="sxs-lookup"><span data-stu-id="2cc38-246">Replace hello IP address and hello hostname in hello following commands</span></span>
    ```bash
    sudo vi /etc/hosts
    ```
    <span data-ttu-id="2cc38-247">Aşağıdaki satırları çok/etc/hosts hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2cc38-247">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="2cc38-248">Başlangıç IP adresi ve ana bilgisayar adı toomatch ortamınızı değiştirme</span><span class="sxs-lookup"><span data-stu-id="2cc38-248">Change hello IP address and hostname toomatch your environment</span></span>    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. <span data-ttu-id="2cc38-249">[1] küme yükleyin</span><span class="sxs-lookup"><span data-stu-id="2cc38-249">[1] Install Cluster</span></span>
    ```bash
    sudo ha-cluster-init
    
    # Do you want toocontinue anyway? [y/N] -> y
    # Network address toobind too(e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish toouse SBD? [y/N] -> N
    # Do you wish tooconfigure an administration IP? [y/N] -> N
    ```
        
1. <span data-ttu-id="2cc38-250">[2] düğüm toocluster Ekle</span><span class="sxs-lookup"><span data-stu-id="2cc38-250">[2] Add node toocluster</span></span>
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured toostart at system boot.
    # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
    # Do you want toocontinue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. <span data-ttu-id="2cc38-251">[A] değişiklik hacluster parola toohello aynı parola</span><span class="sxs-lookup"><span data-stu-id="2cc38-251">[A] Change hacluster password toohello same password</span></span>
    ```bash
    sudo passwd hacluster
    
    ```

1. <span data-ttu-id="2cc38-252">[A] corosync toouse diğer aktarım yapılandırmak ve listesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2cc38-252">[A] Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="2cc38-253">Aksi takdirde, küme çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="2cc38-253">Cluster will not work otherwise.</span></span>
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    <span data-ttu-id="2cc38-254">Merhaba aşağıdaki kalın içerik toohello dosyasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2cc38-254">Add hello following bold content toohello file.</span></span>
    
    <pre><code> 
    [...]
      interface { 
          [...] 
      }
      <b>transport:      udpu</b>
    } 
    <b>nodelist {
      node {
        ring0_addr:     < ip address of node 1 >
      }
      node {
        ring0_addr:     < ip address of node 2 > 
      } 
    }</b>
    logging {
      [...]
    </code></pre>

    <span data-ttu-id="2cc38-255">Merhaba corosync hizmetini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="2cc38-255">Then restart hello corosync service</span></span>

    ```bash
    sudo service corosync restart
    
    ```

1. <span data-ttu-id="2cc38-256">[A] HANA HA paket yüklemek için</span><span class="sxs-lookup"><span data-stu-id="2cc38-256">[A] Install HANA HA packages</span></span>  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a><span data-ttu-id="2cc38-257">SAP HANA yükleme</span><span class="sxs-lookup"><span data-stu-id="2cc38-257">Installing SAP HANA</span></span>

<span data-ttu-id="2cc38-258">Merhaba, Bölüm 4 izleyin [SAP HANA SR performansı en iyi duruma getirilmiş senaryo Kılavuzu] [ suse-hana-ha-guide] tooinstall SAP HANA sistem çoğaltma.</span><span class="sxs-lookup"><span data-stu-id="2cc38-258">Follow chapter 4 of hello [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span></span>

1. <span data-ttu-id="2cc38-259">[A] hdblcm HANA DVD hello çalıştırın</span><span class="sxs-lookup"><span data-stu-id="2cc38-259">[A] Run hdblcm from hello HANA DVD</span></span>
    * <span data-ttu-id="2cc38-260">Yüklemeyi seçin 1 -></span><span class="sxs-lookup"><span data-stu-id="2cc38-260">Choose installation -> 1</span></span>
    * <span data-ttu-id="2cc38-261">Yükleme -> için 1 ek bileşenleri seçin</span><span class="sxs-lookup"><span data-stu-id="2cc38-261">Select additional components for installation -> 1</span></span>
    * <span data-ttu-id="2cc38-262">Yükleme yolu [paylaşılan / hana /] girin: ENTER -></span><span class="sxs-lookup"><span data-stu-id="2cc38-262">Enter Installation Path [/hana/shared]: -> ENTER</span></span>
    * <span data-ttu-id="2cc38-263">Yerel ana bilgisayar adı [.] girin: ENTER -></span><span class="sxs-lookup"><span data-stu-id="2cc38-263">Enter Local Host Name [..]: -> ENTER</span></span>
    * <span data-ttu-id="2cc38-264">Tooadd diğer Konaklara toohello sistemin istiyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="2cc38-264">Do you want tooadd additional hosts toohello system?</span></span> <span data-ttu-id="2cc38-265">(e/h) [n]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="2cc38-265">(y/n) [n]: -> ENTER</span></span>
    * <span data-ttu-id="2cc38-266">SAP HANA sistem Kimliğini girin:<SID of HANA e.g. HDB></span><span class="sxs-lookup"><span data-stu-id="2cc38-266">Enter SAP HANA System ID: <SID of HANA e.g. HDB></span></span>
    * <span data-ttu-id="2cc38-267">Örnek [00] girin:</span><span class="sxs-lookup"><span data-stu-id="2cc38-267">Enter Instance Number [00]:</span></span>   
  <span data-ttu-id="2cc38-268">HANA örneği sayısı.</span><span class="sxs-lookup"><span data-stu-id="2cc38-268">HANA Instance number.</span></span> <span data-ttu-id="2cc38-269">Hello Azure şablonu kullanılan ya da yukarıdaki hello örnek ardından 03 kullanın</span><span class="sxs-lookup"><span data-stu-id="2cc38-269">Use 03 if you used hello Azure Template or followed hello example above</span></span>
    * <span data-ttu-id="2cc38-270">Veritabanı modunu seçin / dizin [1] girin: ENTER -></span><span class="sxs-lookup"><span data-stu-id="2cc38-270">Select Database Mode / Enter Index [1]: -> ENTER</span></span>
    * <span data-ttu-id="2cc38-271">Sistem kullanımı seçin / dizin [4] girin:</span><span class="sxs-lookup"><span data-stu-id="2cc38-271">Select System Usage / Enter Index [4]:</span></span>  
  <span data-ttu-id="2cc38-272">Merhaba sistem kullanımı seçin</span><span class="sxs-lookup"><span data-stu-id="2cc38-272">Select hello system Usage</span></span>
    * <span data-ttu-id="2cc38-273">Veri birimlerinin [/ data/hana/HDB] konumu girin: ENTER -></span><span class="sxs-lookup"><span data-stu-id="2cc38-273">Enter Location of Data Volumes [/hana/data/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="2cc38-274">Günlük birim [/ günlük/hana/HDB] konumu girin: ENTER -></span><span class="sxs-lookup"><span data-stu-id="2cc38-274">Enter Location of Log Volumes [/hana/log/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="2cc38-275">En fazla bellek ayırma kısıtlama?</span><span class="sxs-lookup"><span data-stu-id="2cc38-275">Restrict maximum memory allocation?</span></span> <span data-ttu-id="2cc38-276">[n]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="2cc38-276">[n]: -> ENTER</span></span>
    * <span data-ttu-id="2cc38-277">'...' Ana bilgisayar için sertifika ana bilgisayar adını girin [...]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="2cc38-277">Enter Certificate Host Name For Host '...' [...]: -> ENTER</span></span>
    * <span data-ttu-id="2cc38-278">SAP konak aracısı kullanıcısı (sapadm) parola girin:</span><span class="sxs-lookup"><span data-stu-id="2cc38-278">Enter SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="2cc38-279">SAP konak aracısı kullanıcısı (sapadm) parolayı onaylayın:</span><span class="sxs-lookup"><span data-stu-id="2cc38-279">Confirm SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="2cc38-280">Sistem Yöneticisi (hdbadm) parola girin:</span><span class="sxs-lookup"><span data-stu-id="2cc38-280">Enter System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="2cc38-281">Sistem Yöneticisi (hdbadm) parolayı onaylayın:</span><span class="sxs-lookup"><span data-stu-id="2cc38-281">Confirm System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="2cc38-282">Sistem Yöneticisi giriş dizini girin [/ usr/sap/HDB/giriş]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="2cc38-282">Enter System Administrator Home Directory [/usr/sap/HDB/home]: -> ENTER</span></span>
    * <span data-ttu-id="2cc38-283">Sistem Yöneticisi oturum açma kabuğu girin [/ bin/Paylaş]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="2cc38-283">Enter System Administrator Login Shell [/bin/sh]: -> ENTER</span></span>
    * <span data-ttu-id="2cc38-284">Sistem yöneticisinin kullanıcı kimliği [1001] girin: ENTER -></span><span class="sxs-lookup"><span data-stu-id="2cc38-284">Enter System Administrator User ID [1001]: -> ENTER</span></span>
    * <span data-ttu-id="2cc38-285">Girin kimliği, kullanıcı grubu (sapsys) [79]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="2cc38-285">Enter ID of User Group (sapsys) [79]: -> ENTER</span></span>
    * <span data-ttu-id="2cc38-286">Veritabanı kullanıcı (Sistem) parolasını girin:</span><span class="sxs-lookup"><span data-stu-id="2cc38-286">Enter Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="2cc38-287">Veritabanı kullanıcı (Sistem) parolayı onaylayın:</span><span class="sxs-lookup"><span data-stu-id="2cc38-287">Confirm Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="2cc38-288">Sistem makine yeniden başlatıldıktan sonra yeniden başlatılsın mı?</span><span class="sxs-lookup"><span data-stu-id="2cc38-288">Restart system after machine reboot?</span></span> <span data-ttu-id="2cc38-289">[n]: ENTER -></span><span class="sxs-lookup"><span data-stu-id="2cc38-289">[n]: -> ENTER</span></span>
    * <span data-ttu-id="2cc38-290">Toocontinue istiyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="2cc38-290">Do you want toocontinue?</span></span> <span data-ttu-id="2cc38-291">(e/h):</span><span class="sxs-lookup"><span data-stu-id="2cc38-291">(y/n):</span></span>  
  <span data-ttu-id="2cc38-292">Merhaba Özet doğrulamak ve y toocontinue girin</span><span class="sxs-lookup"><span data-stu-id="2cc38-292">Validate hello summary and enter y toocontinue</span></span>
1. <span data-ttu-id="2cc38-293">[A] yükseltme SAP konak Aracısı</span><span class="sxs-lookup"><span data-stu-id="2cc38-293">[A] Upgrade SAP Host Agent</span></span>  
  <span data-ttu-id="2cc38-294">Hello Hello son SAP konak Aracısı arşivi indir [SAP Softwarecenter] [ sap-swcenter] ve çalışma hello komutu tooupgrade hello aracısı aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="2cc38-294">Download hello latest SAP Host Agent archive from hello [SAP Softwarecenter][sap-swcenter] and run hello following command tooupgrade hello agent.</span></span> <span data-ttu-id="2cc38-295">Merhaba yolu toohello arşiv toopoint toohello dosyasını indirdiğiniz değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2cc38-295">Replace hello path toohello archive toopoint toohello file you downloaded.</span></span>
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path tooSAP Host Agent SAR>
    ```

1. <span data-ttu-id="2cc38-296">[1] (kök olarak) HANA çoğaltma oluşturma</span><span class="sxs-lookup"><span data-stu-id="2cc38-296">[1] Create HANA replication (as root)</span></span>  
    <span data-ttu-id="2cc38-297">Merhaba aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2cc38-297">Run hello following command.</span></span> <span data-ttu-id="2cc38-298">SAP HANA yüklemenizin hello değerlerle emin tooreplace kalın dizeleri (HANA sistem kimliği HDB ile örnek numarasını 03) olun.</span><span class="sxs-lookup"><span data-stu-id="2cc38-298">Make sure tooreplace bold strings (HANA System ID HDB and instance number 03) with hello values of your SAP HANA installation.</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. <span data-ttu-id="2cc38-299">[A] (kök olarak) bir anahtar girişi oluşturun</span><span class="sxs-lookup"><span data-stu-id="2cc38-299">[A] Create keystore entry (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. <span data-ttu-id="2cc38-300">[1] yedek veritabanını (kök) olarak</span><span class="sxs-lookup"><span data-stu-id="2cc38-300">[1] Backup database (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. <span data-ttu-id="2cc38-301">[1] toohello sapsid kullanıcı (örneğin hdbadm) geçiş ve hello birincil site oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2cc38-301">[1] Switch toohello sapsid user (for example hdbadm) and create hello primary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. <span data-ttu-id="2cc38-302">[2] toohello sapsid kullanıcı (örneğin hdbadm) geçin ve hello ikincil site oluştur.</span><span class="sxs-lookup"><span data-stu-id="2cc38-302">[2] Switch toohello sapsid user (for example hdbadm) and create hello secondary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a><span data-ttu-id="2cc38-303">Küme çerçeve Yapılandır</span><span class="sxs-lookup"><span data-stu-id="2cc38-303">Configure Cluster Framework</span></span>

<span data-ttu-id="2cc38-304">Merhaba varsayılan ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="2cc38-304">Change hello default settings</span></span>

<pre>
sudo vi crm-defaults.txt
# enter hello following toocrm-defaults.txt
<code>
property $id="cib-bootstrap-options" \
  no-quorum-policy="ignore" \
  stonith-enabled="true" \
  stonith-action="reboot" \
  stonith-timeout="150s"
rsc_defaults $id="rsc-options" \
  resource-stickiness="1000" \
  migration-threshold="5000"
op_defaults $id="op-options" \
  timeout="600"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="2cc38-305">Şimdi biz hello dosya toohello kümesi yükleme</span><span class="sxs-lookup"><span data-stu-id="2cc38-305">now we load hello file toohello cluster</span></span>
<span data-ttu-id="2cc38-306">sudo crm yük güncelleştirme crm-defaults.txt yapılandırın</span><span class="sxs-lookup"><span data-stu-id="2cc38-306">sudo crm configure load update crm-defaults.txt</span></span>
</pre>

### <a name="create-stonith-device"></a><span data-ttu-id="2cc38-307">STONITH cihaz oluşturma</span><span class="sxs-lookup"><span data-stu-id="2cc38-307">Create STONITH device</span></span>

<span data-ttu-id="2cc38-308">Merhaba STONITH aygıt Microsoft Azure karşı bir hizmet sorumlusu tooauthorize kullanır.</span><span class="sxs-lookup"><span data-stu-id="2cc38-308">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="2cc38-309">Lütfen bu adımları toocreate bir hizmet sorumlusu izleyin.</span><span class="sxs-lookup"><span data-stu-id="2cc38-309">Please follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="2cc38-310">Çok Git<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="2cc38-310">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="2cc38-311">Açık hello Azure Active Directory dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="2cc38-311">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="2cc38-312">TooProperties gidin ve dizin kimliği hello yazma Merhaba budur **Kiracı kimliği**.</span><span class="sxs-lookup"><span data-stu-id="2cc38-312">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="2cc38-313">Uygulama kayıtlar'ı tıklatın</span><span class="sxs-lookup"><span data-stu-id="2cc38-313">Click App registrations</span></span>
1. <span data-ttu-id="2cc38-314">Ekle'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2cc38-314">Click Add</span></span>
1. <span data-ttu-id="2cc38-315">Bir ad girin, uygulama türü "Web uygulaması/API" seçin, bir oturum açma URL'si (örneğin http://localhost) girin ve Oluştur'u tıklatın</span><span class="sxs-lookup"><span data-stu-id="2cc38-315">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="2cc38-316">Merhaba oturum açma URL'si kullanılmaz ve geçerli bir URL olabilir</span><span class="sxs-lookup"><span data-stu-id="2cc38-316">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="2cc38-317">Select hello yeni uygulama ve anahtarları hello ayarları sekmesini tıklatın</span><span class="sxs-lookup"><span data-stu-id="2cc38-317">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="2cc38-318">Yeni bir anahtar için bir açıklama girin, "Her zaman geçerli olsun" seçin ve Kaydet</span><span class="sxs-lookup"><span data-stu-id="2cc38-318">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="2cc38-319">Değer Hello yazın.</span><span class="sxs-lookup"><span data-stu-id="2cc38-319">Write down hello Value.</span></span> <span data-ttu-id="2cc38-320">Hello kullanılan **parola** hello hizmet sorumlusu için</span><span class="sxs-lookup"><span data-stu-id="2cc38-320">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="2cc38-321">Uygulama Kimliği Hello yazma Kullanıcı adı hello olarak kullanılan (**oturum açma kimliği** hello adımlarda aşağıdaki) hello hizmet sorumlusu,</span><span class="sxs-lookup"><span data-stu-id="2cc38-321">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="2cc38-322">Merhaba hizmet asıl izinleri tooaccess varsayılan olarak Azure kaynaklarınızı yok.</span><span class="sxs-lookup"><span data-stu-id="2cc38-322">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="2cc38-323">Toogive hello hizmet asıl izinleri toostart gerekir ve durdurun (deallocate) hello kümenin tüm sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="2cc38-323">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="2cc38-324">Toohttps://Portal.Azure.com gidin</span><span class="sxs-lookup"><span data-stu-id="2cc38-324">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="2cc38-325">Açık hello tüm kaynak dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="2cc38-325">Open hello All resources blade</span></span>
1. <span data-ttu-id="2cc38-326">Merhaba sanal makineyi seçin</span><span class="sxs-lookup"><span data-stu-id="2cc38-326">Select hello virtual machine</span></span>
1. <span data-ttu-id="2cc38-327">Erişim denetimi (IAM) tıklatın</span><span class="sxs-lookup"><span data-stu-id="2cc38-327">Click Access control (IAM)</span></span>
1. <span data-ttu-id="2cc38-328">Ekle'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2cc38-328">Click Add</span></span>
1. <span data-ttu-id="2cc38-329">Merhaba rol sahibi seçin</span><span class="sxs-lookup"><span data-stu-id="2cc38-329">Select hello role Owner</span></span>
1. <span data-ttu-id="2cc38-330">Merhaba, yukarıda oluşturduğunuz Merhaba uygulaması adını girin</span><span class="sxs-lookup"><span data-stu-id="2cc38-330">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="2cc38-331">Tamam'ı tıklatın</span><span class="sxs-lookup"><span data-stu-id="2cc38-331">Click OK</span></span>

<span data-ttu-id="2cc38-332">Merhaba izinleri hello sanal makineler için düzenlenebilir sonra hello kümede hello STONITH cihazları yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2cc38-332">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre>
sudo vi crm-fencing.txt
# enter hello following toocrm-fencing.txt
# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="2cc38-333">Şimdi biz hello dosya toohello kümesi yükleme</span><span class="sxs-lookup"><span data-stu-id="2cc38-333">now we load hello file toohello cluster</span></span>
<span data-ttu-id="2cc38-334">sudo crm yük güncelleştirme crm-fencing.txt yapılandırın</span><span class="sxs-lookup"><span data-stu-id="2cc38-334">sudo crm configure load update crm-fencing.txt</span></span>
</pre>

### <a name="create-sap-hana-resources"></a><span data-ttu-id="2cc38-335">SAP HANA kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="2cc38-335">Create SAP HANA resources</span></span>

<pre>
sudo vi crm-saphanatop.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number and HANA system id
<code>
primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHanaTopology \
    operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
    op monitor interval="10" timeout="600" \
    op start interval="0" timeout="600" \
    op stop interval="0" timeout="300" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"

clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="2cc38-336">Şimdi biz hello dosya toohello kümesi yükleme</span><span class="sxs-lookup"><span data-stu-id="2cc38-336">now we load hello file toohello cluster</span></span>
<span data-ttu-id="2cc38-337">sudo crm yük güncelleştirme crm-saphanatop.txt yapılandırın</span><span class="sxs-lookup"><span data-stu-id="2cc38-337">sudo crm configure load update crm-saphanatop.txt</span></span>
</pre>

<pre>
sudo vi crm-saphana.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
<code>
primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
    operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
    op start interval="0" timeout="3600" \
    op stop interval="0" timeout="3600" \
    op promote interval="0" timeout="3600" \
    op monitor interval="60" role="Master" timeout="700" \
    op monitor interval="61" role="Slave" timeout="700" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
    DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"

ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
    target-role="Started" interleave="true"

primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
    meta target-role="Started" is-managed="true" \ 
    operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
    op monitor interval="10s" timeout="20s" \ 
    params ip="<b>10.0.0.21</b>" 
primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
    params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
    op monitor timeout=20s interval=10 depth=0 
group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
 
colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  
order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="2cc38-338">Şimdi biz hello dosya toohello kümesi yükleme</span><span class="sxs-lookup"><span data-stu-id="2cc38-338">now we load hello file toohello cluster</span></span>
<span data-ttu-id="2cc38-339">sudo crm yük güncelleştirme crm-saphana.txt yapılandırın</span><span class="sxs-lookup"><span data-stu-id="2cc38-339">sudo crm configure load update crm-saphana.txt</span></span>
</pre>

### <a name="test-cluster-setup"></a><span data-ttu-id="2cc38-340">Test kümesi Kurulumu</span><span class="sxs-lookup"><span data-stu-id="2cc38-340">Test cluster setup</span></span>
<span data-ttu-id="2cc38-341">bölüm aşağıdaki hello kurulumunuzu test nasıl açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2cc38-341">hello following chapter describe how you can test your setup.</span></span> <span data-ttu-id="2cc38-342">Her test kök olan ve hello SAP HANA ana hello sanal makine saphanavm1 üzerinde çalıştığını varsayar.</span><span class="sxs-lookup"><span data-stu-id="2cc38-342">Every test assumes that you are root and hello SAP HANA master is running on hello virtual machine saphanavm1.</span></span>

#### <a name="fencing-test"></a><span data-ttu-id="2cc38-343">Yalıtma Test</span><span class="sxs-lookup"><span data-stu-id="2cc38-343">Fencing Test</span></span>

<span data-ttu-id="2cc38-344">Düğüm saphanavm1 hello ağ arabiriminde devre dışı bırakarak hello Kurulum hello yalıtma Aracısı'nın test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2cc38-344">You can test hello setup of hello fencing agent by disabling hello network interface on node saphanavm1.</span></span>

<pre><code>
sudo ifdown eth0
</code></pre>

<span data-ttu-id="2cc38-345">Merhaba sanal makine şimdi yeniden veya küme yapılandırmanıza bağlı olarak durduruldu.</span><span class="sxs-lookup"><span data-stu-id="2cc38-345">hello virtual machine should now get restarted or stopped depending on your cluster configuration.</span></span>
<span data-ttu-id="2cc38-346">Merhaba stonith eylem toooff ayarlarsanız, hello sanal makine durdurulur ve sanal makine çalışırken geçirilen toohello hello kaynaklardır.</span><span class="sxs-lookup"><span data-stu-id="2cc38-346">If you set hello stonith-action toooff, hello virtual machine will be stopped and hello resources are migrated toohello running virtual machine.</span></span>

<span data-ttu-id="2cc38-347">Merhaba sanal makine yeniden başladıktan sonra AUTOMATED_REGISTER ayarlarsanız hello SAP HANA kaynak ikincil olarak toostart başarısız olur = "false".</span><span class="sxs-lookup"><span data-stu-id="2cc38-347">Once you start hello virtual machine again, hello SAP HANA resource will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="2cc38-348">Bu durumda, komutu aşağıdaki hello yürüterek tooconfigure hello HANA örneği ikincil olarak gerekir:</span><span class="sxs-lookup"><span data-stu-id="2cc38-348">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a><span data-ttu-id="2cc38-349">El ile bir yük devretme sınaması</span><span class="sxs-lookup"><span data-stu-id="2cc38-349">Testing a manual failover</span></span>

<span data-ttu-id="2cc38-350">Düğüm saphanavm1 üzerinde hello pacemaker hizmetini durdurarak el ile bir yük devretme test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2cc38-350">You can test a manual failover by stopping hello pacemaker service on node saphanavm1.</span></span>
<pre><code>
service pacemaker stop
</code></pre>

<span data-ttu-id="2cc38-351">Merhaba yük devretme sonrasında hello hizmetini yeniden başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2cc38-351">After hello failover, you can start hello service again.</span></span> <span data-ttu-id="2cc38-352">Merhaba saphanavm1 SAP HANA kaynakta başarısız olur toostart ikincil olarak AUTOMATED_REGISTER ayarlarsanız = "false".</span><span class="sxs-lookup"><span data-stu-id="2cc38-352">hello SAP HANA resource on saphanavm1 will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="2cc38-353">Bu durumda, komutu aşağıdaki hello yürüterek tooconfigure hello HANA örneği ikincil olarak gerekir:</span><span class="sxs-lookup"><span data-stu-id="2cc38-353">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a><span data-ttu-id="2cc38-354">Bir geçiş test etme</span><span class="sxs-lookup"><span data-stu-id="2cc38-354">Testing a migration</span></span>

<span data-ttu-id="2cc38-355">Komutu aşağıdaki hello yürüterek hello SAP HANA ana düğüm geçirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2cc38-355">You can migrate hello SAP HANA master node by executing hello following command</span></span>
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="2cc38-356">Merhaba SAP HANA ana düğüm ve hello sanal IP adresi toosaphanavm2 içeren hello grubunu geçirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2cc38-356">This should migrate hello SAP HANA master node and hello group that contains hello virtual IP address toosaphanavm2.</span></span>
<span data-ttu-id="2cc38-357">Merhaba saphanavm1 SAP HANA kaynakta başarısız olur toostart ikincil olarak AUTOMATED_REGISTER ayarlarsanız = "false".</span><span class="sxs-lookup"><span data-stu-id="2cc38-357">hello SAP HANA resource on saphanavm1 will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="2cc38-358">Bu durumda, komutu aşağıdaki hello yürüterek tooconfigure hello HANA örneği ikincil olarak gerekir:</span><span class="sxs-lookup"><span data-stu-id="2cc38-358">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

<span data-ttu-id="2cc38-359">Merhaba geçiş yeniden silinmiş toobe gereken konum contraints oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2cc38-359">hello migration creates location contraints that need toobe deleted again.</span></span>

<pre><code>
crm configure edited

# delete location contraints that are named like hello following contraint. You should have two contraints, one for hello SAP HANA resource and one for hello IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="2cc38-360">Ayrıca hello ikincil düğüme kaynağının toocleanup hello durumu gerekir</span><span class="sxs-lookup"><span data-stu-id="2cc38-360">You also need toocleanup hello state of hello secondary node resource</span></span>

<pre><code>
# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a><span data-ttu-id="2cc38-361">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2cc38-361">Next steps</span></span>
* <span data-ttu-id="2cc38-362">[Azure sanal makineleri planlama ve uygulama SAP için][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="2cc38-362">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="2cc38-363">[SAP için Azure sanal makineler dağıtımı][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="2cc38-363">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="2cc38-364">[SAP için Azure sanal makineleri DBMS dağıtımı][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="2cc38-364">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="2cc38-365">tooestablish yüksek kullanılabilirlik ve olağanüstü durum kurtarma SAP HANA planlama (büyük örnekler), azure'da nasıl görürüm toolearn [SAP HANA (büyük örnekler) Azure üzerinde yüksek kullanılabilirlik ve olağanüstü durum kurtarma](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="2cc38-365">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span> 
