---
title: "Sanal makineler için yüksek oranda kullanılabilirlik SAP NetWeaver SUSE Linux Enterprise Server üzerinde SAP uygulamaları için aaaAzure | Microsoft Docs"
description: "Yüksek kullanılabilirlik için Kılavuzu SAP NetWeaver SUSE Linux Enterprise Server üzerinde SAP uygulamaları için"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: mssedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: sedusch
ms.openlocfilehash: e944103df92d5ffec9196189f138e25972bea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a><span data-ttu-id="230da-103">SUSE Linux Enterprise Server üzerinde Azure vm'lerinde SAP NetWeaver SAP uygulamalar için yüksek kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="230da-103">High availability for SAP NetWeaver on Azure VMs on SUSE Linux Enterprise Server for SAP applications</span></span>

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
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

<span data-ttu-id="230da-113">Bu makalede nasıl toodeploy hello sanal makineler, hello sanal makineleri yapılandırma, hello küme Framework'ü yüklemek ve yüksek oranda kullanılabilir bir SAP NetWeaver 7.50 sistemi yükleyin açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="230da-113">This article describes how toodeploy hello virtual machines, configure hello virtual machines, install hello cluster framework and install a highly available SAP NetWeaver 7.50 system.</span></span>
<span data-ttu-id="230da-114">Merhaba örnek yapılandırmaları, vb. yükleme komutları. ASCS örnek numarasını 00, ERS örnek numarasını 02 ve SAP sistem kimliği NWS kullanılır.</span><span class="sxs-lookup"><span data-stu-id="230da-114">In hello example configurations, installation commands etc. ASCS instance number 00, ERS instance number 02 and SAP System ID NWS is used.</span></span> <span data-ttu-id="230da-115">Merhaba hello örnekte hello kaynakların (örneğin, sanal makineler, sanal ağlar) adları hello kullandığınızı varsayar [şablonu Yakınsanan] [ template-converged] SAP sistem kimliği NWS toocreate hello kaynaklara sahip.</span><span class="sxs-lookup"><span data-stu-id="230da-115">hello names of hello resources (for example virtual machines, virtual networks) in hello example assume that you have used hello [converged template][template-converged] with SAP system ID NWS toocreate hello resources.</span></span>

<span data-ttu-id="230da-116">SAP notlar ve incelemeleri önce aşağıdaki hello okuma</span><span class="sxs-lookup"><span data-stu-id="230da-116">Read hello following SAP Notes and papers first</span></span>

* <span data-ttu-id="230da-117">SAP Not [1928533], sahip olduğu:</span><span class="sxs-lookup"><span data-stu-id="230da-117">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="230da-118">SAP yazılım hello dağıtımı için desteklenen Azure VM boyutlarını listesi</span><span class="sxs-lookup"><span data-stu-id="230da-118">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="230da-119">Azure VM boyutlarını önemli kapasite bilgilerini</span><span class="sxs-lookup"><span data-stu-id="230da-119">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="230da-120">Desteklenen bir SAP yazılım ve işletim sistemi (OS) ve veritabanı birleşimler</span><span class="sxs-lookup"><span data-stu-id="230da-120">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="230da-121">Windows ve Microsoft Azure Linux için gerekli SAP çekirdek sürümü</span><span class="sxs-lookup"><span data-stu-id="230da-121">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="230da-122">SAP Not [2015553] azure'da SAP desteklenen SAP yazılım dağıtımları için önkoşulları listeler.</span><span class="sxs-lookup"><span data-stu-id="230da-122">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="230da-123">SAP Not [2205917] SUSE Linux Enterprise Server işletim sistemi ayarlarını SAP uygulamaları için önerilir</span><span class="sxs-lookup"><span data-stu-id="230da-123">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="230da-124">SAP Not [1944799] SAP HANA yönergeleri SUSE Linux Enterprise Server için SAP uygulamaları için vardır.</span><span class="sxs-lookup"><span data-stu-id="230da-124">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="230da-125">SAP Not [2178632] ayrıntılı Azure SAP için bildirilen tüm izleme ölçümleri hakkında bilgi sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="230da-125">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="230da-126">SAP Not [2191498] hello Azure Linux için SAP konak Aracısı sürümünü istedi.</span><span class="sxs-lookup"><span data-stu-id="230da-126">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="230da-127">SAP Not [2243692] Linux Azure üzerinde SAP lisanslama hakkında bilgi vardır.</span><span class="sxs-lookup"><span data-stu-id="230da-127">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="230da-128">SAP Not [1984787] SUSE Linux Enterprise Server 12 hakkında genel bilgi yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="230da-128">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="230da-129">SAP Not [1999351] hello Azure Gelişmiş izleme uzantısı SAP için ek sorun giderme bilgileri içeriyor.</span><span class="sxs-lookup"><span data-stu-id="230da-129">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="230da-130">[SAP topluluk WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) SAP notları Linux için gerekli tüm sahiptir.</span><span class="sxs-lookup"><span data-stu-id="230da-130">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="230da-131">[Azure sanal makineleri planlama ve uygulama Linux üzerinde SAP için][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="230da-131">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="230da-132">[(Bu makalede) Linux'ta SAP için Azure sanal makineler dağıtımı][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="230da-132">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="230da-133">[Linux üzerinde SAP için Azure sanal makineleri DBMS dağıtımı][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="230da-133">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="230da-134">[Senaryo SAP HANA SR performansı en iyi duruma getirilmiş][suse-hana-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="230da-134">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide]</span></span>  
  <span data-ttu-id="230da-135">SAP HANA sistem çoğaltma yerinde tüm gerekli bilgileri tooset Hello kılavuz içerir.</span><span class="sxs-lookup"><span data-stu-id="230da-135">hello guide contains all required information tooset up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="230da-136">Bu kılavuz, bir taban çizgisi olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="230da-136">Use this guide as a baseline.</span></span>
* <span data-ttu-id="230da-137">[Yüksek oranda kullanılabilir NFS depolama DRBD ve Pacemaker] [ suse-drbd-guide] Başlangıç Kılavuzu, tüm gerekli bilgileri tooset yüksek oranda kullanılabilir bir NFS sunucusu içerir.</span><span class="sxs-lookup"><span data-stu-id="230da-137">[Highly Available NFS Storage with DRBD and Pacemaker][suse-drbd-guide] hello guide contains all required information tooset up a highly available NFS server.</span></span> <span data-ttu-id="230da-138">Bu kılavuz, bir taban çizgisi olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="230da-138">Use this guide as a baseline.</span></span>


## <a name="overview"></a><span data-ttu-id="230da-139">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="230da-139">Overview</span></span>

<span data-ttu-id="230da-140">tooachieve yüksek kullanılabilirlik, SAP NetWeaver, bir NFS sunucusunun gerektirir.</span><span class="sxs-lookup"><span data-stu-id="230da-140">tooachieve high availability, SAP NetWeaver requires an NFS server.</span></span> <span data-ttu-id="230da-141">Merhaba NFS sunucusu ayrı bir kümede yapılandırılmış ve birden çok SAP sistemleri tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="230da-141">hello NFS server is configured in a separate cluster and can be used by multiple SAP systems.</span></span>

![SAP NetWeaver yüksek kullanılabilirlik genel bakış](./media/high-availability-guide-suse/img_001.png)

<span data-ttu-id="230da-143">Merhaba NFS sunucusu, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS ve hello SAP HANA veritabanına sanal ana bilgisayar adı ve sanal IP adresleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="230da-143">hello NFS server, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS and hello SAP HANA database use virtual hostname and virtual IP addresses.</span></span> <span data-ttu-id="230da-144">Azure üzerinde bir yük dengeleyici sanal IP adresi gerekli toouse ' dir.</span><span class="sxs-lookup"><span data-stu-id="230da-144">On Azure, a load balancer is required toouse a virtual IP address.</span></span> <span data-ttu-id="230da-145">Merhaba aşağıdaki liste hello yük dengeleyici hello yapılandırmasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="230da-145">hello following list shows hello configuration of hello load balancer.</span></span>

### <a name="nfs-server"></a><span data-ttu-id="230da-146">NFS sunucusu</span><span class="sxs-lookup"><span data-stu-id="230da-146">NFS Server</span></span>
* <span data-ttu-id="230da-147">Ön uç yapılandırma</span><span class="sxs-lookup"><span data-stu-id="230da-147">Frontend configuration</span></span>
  * <span data-ttu-id="230da-148">IP adresi 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="230da-148">IP address 10.0.0.4</span></span>
* <span data-ttu-id="230da-149">Arka uç yapılandırması</span><span class="sxs-lookup"><span data-stu-id="230da-149">Backend configuration</span></span>
  * <span data-ttu-id="230da-150">Tooprimary ağ arabirimleri hello NFS kümesinin parçası olması gereken tüm sanal makinelerin bağlı</span><span class="sxs-lookup"><span data-stu-id="230da-150">Connected tooprimary network interfaces of all virtual machines that should be part of hello NFS cluster</span></span>
* <span data-ttu-id="230da-151">Sonda bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="230da-151">Probe Port</span></span>
  * <span data-ttu-id="230da-152">Bağlantı noktası 61000</span><span class="sxs-lookup"><span data-stu-id="230da-152">Port 61000</span></span>
* <span data-ttu-id="230da-153">Loadbalancing kuralları</span><span class="sxs-lookup"><span data-stu-id="230da-153">Loadbalancing rules</span></span>
  * <span data-ttu-id="230da-154">2049 TCP</span><span class="sxs-lookup"><span data-stu-id="230da-154">2049 TCP</span></span> 
  * <span data-ttu-id="230da-155">2049 UDP</span><span class="sxs-lookup"><span data-stu-id="230da-155">2049 UDP</span></span>

### <a name="ascs"></a><span data-ttu-id="230da-156">(A) SCS</span><span class="sxs-lookup"><span data-stu-id="230da-156">(A)SCS</span></span>
* <span data-ttu-id="230da-157">Ön uç yapılandırma</span><span class="sxs-lookup"><span data-stu-id="230da-157">Frontend configuration</span></span>
  * <span data-ttu-id="230da-158">IP adresi 10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="230da-158">IP address 10.0.0.10</span></span>
* <span data-ttu-id="230da-159">Arka uç yapılandırması</span><span class="sxs-lookup"><span data-stu-id="230da-159">Backend configuration</span></span>
  * <span data-ttu-id="230da-160">Merhaba (A) SCS/ERS kümesinin parçası olması gereken tüm sanal makinelerin bağlı tooprimary ağ arabirimleri</span><span class="sxs-lookup"><span data-stu-id="230da-160">Connected tooprimary network interfaces of all virtual machines that should be part of hello (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="230da-161">Sonda bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="230da-161">Probe Port</span></span>
  * <span data-ttu-id="230da-162">Bağlantı noktası 620**&lt;n&gt;**</span><span class="sxs-lookup"><span data-stu-id="230da-162">Port 620**&lt;nr&gt;**</span></span>
* <span data-ttu-id="230da-163">Loadbalancing kuralları</span><span class="sxs-lookup"><span data-stu-id="230da-163">Loadbalancing rules</span></span>
  * <span data-ttu-id="230da-164">32**&lt;n&gt;**  TCP</span><span class="sxs-lookup"><span data-stu-id="230da-164">32**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="230da-165">36**&lt;n&gt;**  TCP</span><span class="sxs-lookup"><span data-stu-id="230da-165">36**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="230da-166">39**&lt;n&gt;**  TCP</span><span class="sxs-lookup"><span data-stu-id="230da-166">39**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="230da-167">81**&lt;n&gt;**  TCP</span><span class="sxs-lookup"><span data-stu-id="230da-167">81**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="230da-168">5**&lt;n&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="230da-168">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="230da-169">5**&lt;n&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="230da-169">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="230da-170">5**&lt;n&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="230da-170">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="ers"></a><span data-ttu-id="230da-171">ERS</span><span class="sxs-lookup"><span data-stu-id="230da-171">ERS</span></span>
* <span data-ttu-id="230da-172">Ön uç yapılandırma</span><span class="sxs-lookup"><span data-stu-id="230da-172">Frontend configuration</span></span>
  * <span data-ttu-id="230da-173">IP adresi 10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="230da-173">IP address 10.0.0.11</span></span>
* <span data-ttu-id="230da-174">Arka uç yapılandırması</span><span class="sxs-lookup"><span data-stu-id="230da-174">Backend configuration</span></span>
  * <span data-ttu-id="230da-175">Merhaba (A) SCS/ERS kümesinin parçası olması gereken tüm sanal makinelerin bağlı tooprimary ağ arabirimleri</span><span class="sxs-lookup"><span data-stu-id="230da-175">Connected tooprimary network interfaces of all virtual machines that should be part of hello (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="230da-176">Sonda bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="230da-176">Probe Port</span></span>
  * <span data-ttu-id="230da-177">Bağlantı noktası 621**&lt;n&gt;**</span><span class="sxs-lookup"><span data-stu-id="230da-177">Port 621**&lt;nr&gt;**</span></span>
* <span data-ttu-id="230da-178">Loadbalancing kuralları</span><span class="sxs-lookup"><span data-stu-id="230da-178">Loadbalancing rules</span></span>
  * <span data-ttu-id="230da-179">33**&lt;n&gt;**  TCP</span><span class="sxs-lookup"><span data-stu-id="230da-179">33**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="230da-180">5**&lt;n&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="230da-180">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="230da-181">5**&lt;n&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="230da-181">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="230da-182">5**&lt;n&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="230da-182">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="sap-hana"></a><span data-ttu-id="230da-183">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="230da-183">SAP HANA</span></span>
* <span data-ttu-id="230da-184">Ön uç yapılandırma</span><span class="sxs-lookup"><span data-stu-id="230da-184">Frontend configuration</span></span>
  * <span data-ttu-id="230da-185">IP adresi 10.0.0.12</span><span class="sxs-lookup"><span data-stu-id="230da-185">IP address 10.0.0.12</span></span>
* <span data-ttu-id="230da-186">Arka uç yapılandırması</span><span class="sxs-lookup"><span data-stu-id="230da-186">Backend configuration</span></span>
  * <span data-ttu-id="230da-187">Merhaba HANA kümesinin parçası olması gereken tüm sanal makinelerin tooprimary ağ arabirimleri bağlı</span><span class="sxs-lookup"><span data-stu-id="230da-187">Connected tooprimary network interfaces of all virtual machines that should be part of hello HANA cluster</span></span>
* <span data-ttu-id="230da-188">Sonda bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="230da-188">Probe Port</span></span>
  * <span data-ttu-id="230da-189">Bağlantı noktası 625**&lt;n&gt;**</span><span class="sxs-lookup"><span data-stu-id="230da-189">Port 625**&lt;nr&gt;**</span></span>
* <span data-ttu-id="230da-190">Loadbalancing kuralları</span><span class="sxs-lookup"><span data-stu-id="230da-190">Loadbalancing rules</span></span>
  * <span data-ttu-id="230da-191">3**&lt;n&gt;**15 TCP</span><span class="sxs-lookup"><span data-stu-id="230da-191">3**&lt;nr&gt;**15 TCP</span></span>
  * <span data-ttu-id="230da-192">3**&lt;n&gt;**17 TCP</span><span class="sxs-lookup"><span data-stu-id="230da-192">3**&lt;nr&gt;**17 TCP</span></span>

## <a name="setting-up-a-highly-available-nfs-server"></a><span data-ttu-id="230da-193">Yüksek oranda kullanılabilir bir NFS sunucusu kurma</span><span class="sxs-lookup"><span data-stu-id="230da-193">Setting up a highly available NFS server</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="230da-194">Linux dağıtma</span><span class="sxs-lookup"><span data-stu-id="230da-194">Deploying Linux</span></span>

<span data-ttu-id="230da-195">Hello Azure Market görüntü için SAP uygulamaları toodeploy yeni sanal makineleri kullanabilir 12 SUSE Linux Enterprise Server içerir.</span><span class="sxs-lookup"><span data-stu-id="230da-195">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use toodeploy new virtual machines.</span></span>
<span data-ttu-id="230da-196">Merhaba hızlı başlangıç şablonlarından birini github toodeploy üzerinde gerekli tüm kaynakları kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="230da-196">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="230da-197">Merhaba şablon hello sanal makineler, hello yük dengeleyici, kullanılabilirlik vb. kümesi dağıtır. Bu adımları toodeploy hello şablon izleyin:</span><span class="sxs-lookup"><span data-stu-id="230da-197">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="230da-198">Açık hello [SAP dosya sunucusu şablonu] [ template-file-server] hello Azure portal'ın</span><span class="sxs-lookup"><span data-stu-id="230da-198">Open hello [SAP file server template][template-file-server] in hello Azure portal</span></span>   
1. <span data-ttu-id="230da-199">Şu parametreler hello girin</span><span class="sxs-lookup"><span data-stu-id="230da-199">Enter hello following parameters</span></span>
   1. <span data-ttu-id="230da-200">Kaynak öneki</span><span class="sxs-lookup"><span data-stu-id="230da-200">Resource Prefix</span></span>  
      <span data-ttu-id="230da-201">Toouse istediğiniz hello öneki girin.</span><span class="sxs-lookup"><span data-stu-id="230da-201">Enter hello prefix you want toouse.</span></span> <span data-ttu-id="230da-202">Merhaba değer dağıtılan hello kaynaklar için önek olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="230da-202">hello value is used as a prefix for hello resources that are deployed.</span></span>
   2. <span data-ttu-id="230da-203">İşletim sistemi türü</span><span class="sxs-lookup"><span data-stu-id="230da-203">Os Type</span></span>  
      <span data-ttu-id="230da-204">Merhaba Linux dağıtımları birini seçin.</span><span class="sxs-lookup"><span data-stu-id="230da-204">Select one of hello Linux distributions.</span></span> <span data-ttu-id="230da-205">Bu örnekte, SLES 12 seçin</span><span class="sxs-lookup"><span data-stu-id="230da-205">For this example, select SLES 12</span></span>
   3. <span data-ttu-id="230da-206">Yönetici kullanıcı adı ve yönetici parolası</span><span class="sxs-lookup"><span data-stu-id="230da-206">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="230da-207">Yeni bir kullanıcı oluşturulur toohello makinede kullanılan toolog olabilir.</span><span class="sxs-lookup"><span data-stu-id="230da-207">A new user is created that can be used toolog on toohello machine.</span></span>
   4. <span data-ttu-id="230da-208">Alt ağ kimliği</span><span class="sxs-lookup"><span data-stu-id="230da-208">Subnet Id</span></span>  
      <span data-ttu-id="230da-209">için Hello kimliği hello alt toowhich hello sanal makinelerin bağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="230da-209">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span> <span data-ttu-id="230da-210">Yeni bir sanal ağ toocreate istediğiniz ya da VPN veya hızlı rota sanal ağ tooconnect hello sanal makine tooyour Şirket ağınızın hello alt ağ seçin, boş bırakın.</span><span class="sxs-lookup"><span data-stu-id="230da-210">Leave empty if you want toocreate a new virtual network or select hello subnet of your VPN or Express Route virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="230da-211">Merhaba kimliği genellikle /subscriptions/ gibi görünüyor**&lt;abonelik kimliği&gt;**/resourceGroups/**&lt;kaynak grubu adı&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;sanal ağ adı&gt;**/subnets/**&lt;alt ağ adı&gt;**</span><span class="sxs-lookup"><span data-stu-id="230da-211">hello ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="230da-212">Yükleme</span><span class="sxs-lookup"><span data-stu-id="230da-212">Installation</span></span>

<span data-ttu-id="230da-213">Merhaba aşağıdaki öğeleri ile ya da önek **[A]** -geçerli tooall düğümleri **[1]** -yalnızca geçerli toonode 1 veya **[2]** -yalnızca geçerli toonode 2.</span><span class="sxs-lookup"><span data-stu-id="230da-213">hello following items are prefixed with either **[A]** - applicable tooall nodes, **[1]** - only applicable toonode 1 or **[2]** - only applicable toonode 2.</span></span>

1. <span data-ttu-id="230da-214">**[A]**  SLES güncelleştir</span><span class="sxs-lookup"><span data-stu-id="230da-214">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="230da-215">**[1]**  Ssh erişimini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="230da-215">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="230da-216">**[2]**  Ssh erişimini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="230da-216">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="230da-217">**[1]**  Ssh erişimini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="230da-217">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="230da-218">**[A]**  Yükleme HA uzantısı</span><span class="sxs-lookup"><span data-stu-id="230da-218">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="230da-219">**[A]**  Kurulum ana bilgisayar adı çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="230da-219">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="230da-220">Bir DNS sunucusu kullanın veya tüm düğümlerde hello/etc/hosts değiştirin.</span><span class="sxs-lookup"><span data-stu-id="230da-220">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="230da-221">Bu örnek nasıl toouse hello/etc/hosts dosyasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="230da-221">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="230da-222">Başlangıç IP adresi ve hello hostname komutları aşağıdaki hello olarak değiştirin</span><span class="sxs-lookup"><span data-stu-id="230da-222">Replace hello IP address and hello hostname in hello following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="230da-223">Aşağıdaki satırları çok/etc/hosts hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="230da-223">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="230da-224">Başlangıç IP adresi ve ana bilgisayar adı toomatch ortamınızı değiştirme</span><span class="sxs-lookup"><span data-stu-id="230da-224">Change hello IP address and hostname toomatch your environment</span></span>   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. <span data-ttu-id="230da-225">**[1]**  Küme yükleyin</span><span class="sxs-lookup"><span data-stu-id="230da-225">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="230da-226">**[2]**  Düğüm toocluster Ekle</span><span class="sxs-lookup"><span data-stu-id="230da-226">**[2]** Add node toocluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="230da-227">**[A]**  Değişiklik hacluster parola toohello aynı parola</span><span class="sxs-lookup"><span data-stu-id="230da-227">**[A]** Change hacluster password toohello same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="230da-228">**[A]**  Corosync toouse diğer aktarım yapılandırmak ve listesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="230da-228">**[A]** Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="230da-229">Aksi takdirde, küme çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="230da-229">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="230da-230">Merhaba aşağıdaki kalın içerik toohello dosyasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="230da-230">Add hello following bold content toohello file.</span></span>
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>prod-nfs-0</b>
      ring0_addr:10.0.0.5
     }
     node {
      # IP address of <b>prod-nfs-1</b>
      ring0_addr:10.0.0.6
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   <span data-ttu-id="230da-231">Merhaba corosync hizmetini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="230da-231">Then restart hello corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="230da-232">**[A]**  Drbd bileşenlerini yükleme</span><span class="sxs-lookup"><span data-stu-id="230da-232">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="230da-233">**[A]**  Hello drbd cihaz için bir bölüm oluşturun</span><span class="sxs-lookup"><span data-stu-id="230da-233">**[A]** Create a partition for hello drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="230da-234">**[A]**  LVM oluşturma yapılandırmaları</span><span class="sxs-lookup"><span data-stu-id="230da-234">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. <span data-ttu-id="230da-235">**[A]**  Oluşturma hello NFS drbd aygıt</span><span class="sxs-lookup"><span data-stu-id="230da-235">**[A]** Create hello NFS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   <span data-ttu-id="230da-236">Merhaba yeni drbd aygıt ve çıkış Hello Yapılandırması Ekle</span><span class="sxs-lookup"><span data-stu-id="230da-236">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_nfs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>prod-nfs-0</b> {
         address   <b>10.0.0.5</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
      on <b>prod-nfs-1</b> {
         address   <b>10.0.0.6</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="230da-237">Merhaba drbd aygıtı oluşturun ve başlatın</span><span class="sxs-lookup"><span data-stu-id="230da-237">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="230da-238">**[1]**  Atla ilk eşitleme</span><span class="sxs-lookup"><span data-stu-id="230da-238">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="230da-239">**[1]**  Kümesi hello birincil düğüm</span><span class="sxs-lookup"><span data-stu-id="230da-239">**[1]** Set hello primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="230da-240">**[1]**  Hello yeni drbd aygıtları eşitlenir kadar bekleyin</span><span class="sxs-lookup"><span data-stu-id="230da-240">**[1]** Wait until hello new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="230da-241">**[1]**  Dosya sistemleri üzerinde hello drbd aygıtları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="230da-241">**[1]** Create file systems on hello drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="230da-242">Küme çerçeve Yapılandır</span><span class="sxs-lookup"><span data-stu-id="230da-242">Configure Cluster Framework</span></span>

1. <span data-ttu-id="230da-243">**[1]**  Hello varsayılan ayarları değiştir</span><span class="sxs-lookup"><span data-stu-id="230da-243">**[1]** Change hello default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="230da-244">**[1]**  Ekle hello NFS drbd aygıt toohello küme yapılandırması</span><span class="sxs-lookup"><span data-stu-id="230da-244">**[1]** Add hello NFS drbd device toohello cluster configuration</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_nfs \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_nfs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_nfs drbd_<b>NWS</b>_nfs \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="230da-245">**[1]**  Oluşturma hello NFS sunucusu</span><span class="sxs-lookup"><span data-stu-id="230da-245">**[1]** Create hello NFS server</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="230da-246">**[1]**  Hello NFS dosya sistemi kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="230da-246">**[1]** Create hello NFS File System resources</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive fs_<b>NWS</b>_sapmnt \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/srv/nfs/<b>NWS</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# group g-<b>NWS</b>_nfs fs_<b>NWS</b>_sapmnt

   crm(live)configure# order o-<b>NWS</b>_drbd_before_nfs inf: \
     ms-drbd_<b>NWS</b>_nfs:promote g-<b>NWS</b>_nfs:start
   
   crm(live)configure# colocation col-<b>NWS</b>_nfs_on_drbd inf: \
     g-<b>NWS</b>_nfs ms-drbd_<b>NWS</b>_nfs:Master

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="230da-247">**[1]**  Oluşturma hello NFS dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="230da-247">**[1]** Create hello NFS exports</span></span>

   <pre><code>
   sudo mkdir /srv/nfs/<b>NWS</b>/sidsys
   sudo mkdir /srv/nfs/<b>NWS</b>/sapmntsid
   sudo mkdir /srv/nfs/<b>NWS</b>/trans

   sudo crm configure

   crm(live)configure# primitive exportfs_<b>NWS</b> \
     ocf:heartbeat:exportfs \
     params directory="/srv/nfs/<b>NWS</b>" \
     options="rw,no_root_squash" \
     clientspec="*" fsid=0 \
     wait_for_leasetime_on_stop=true \
     op monitor interval="30s"

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add exportfs_<b>NWS</b>

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="230da-248">**[1]**  Bir sanal IP kaynak ve sistem durumu araştırması hello iç yük dengeleyici için oluşturma</span><span class="sxs-lookup"><span data-stu-id="230da-248">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive vip_<b>NWS</b>_nfs IPaddr2 \
     params ip=<b>10.0.0.4</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_nfs anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 610<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add nc_<b>NWS</b>_nfs
   crm(live)configure# modgroup g-<b>NWS</b>_nfs add vip_<b>NWS</b>_nfs

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

### <a name="create-stonith-device"></a><span data-ttu-id="230da-249">STONITH cihaz oluşturma</span><span class="sxs-lookup"><span data-stu-id="230da-249">Create STONITH device</span></span>

<span data-ttu-id="230da-250">Merhaba STONITH aygıt Microsoft Azure karşı bir hizmet sorumlusu tooauthorize kullanır.</span><span class="sxs-lookup"><span data-stu-id="230da-250">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="230da-251">Bu adımları toocreate bir hizmet sorumlusu izleyin.</span><span class="sxs-lookup"><span data-stu-id="230da-251">Follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="230da-252">Çok Git<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="230da-252">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="230da-253">Açık hello Azure Active Directory dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="230da-253">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="230da-254">TooProperties gidin ve dizin kimliği hello yazma Merhaba budur **Kiracı kimliği**.</span><span class="sxs-lookup"><span data-stu-id="230da-254">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="230da-255">Uygulama kayıtlar'ı tıklatın</span><span class="sxs-lookup"><span data-stu-id="230da-255">Click App registrations</span></span>
1. <span data-ttu-id="230da-256">Ekle'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="230da-256">Click Add</span></span>
1. <span data-ttu-id="230da-257">Bir ad girin, uygulama türü "Web uygulaması/API" seçin, bir oturum açma URL'si (örneğin http://localhost) girin ve Oluştur'u tıklatın</span><span class="sxs-lookup"><span data-stu-id="230da-257">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="230da-258">Merhaba oturum açma URL'si kullanılmaz ve geçerli bir URL olabilir</span><span class="sxs-lookup"><span data-stu-id="230da-258">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="230da-259">Select hello yeni uygulama ve anahtarları hello ayarları sekmesini tıklatın</span><span class="sxs-lookup"><span data-stu-id="230da-259">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="230da-260">Yeni bir anahtar için bir açıklama girin, "Her zaman geçerli olsun" seçin ve Kaydet</span><span class="sxs-lookup"><span data-stu-id="230da-260">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="230da-261">Değer Hello yazın.</span><span class="sxs-lookup"><span data-stu-id="230da-261">Write down hello Value.</span></span> <span data-ttu-id="230da-262">Hello kullanılan **parola** hello hizmet sorumlusu için</span><span class="sxs-lookup"><span data-stu-id="230da-262">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="230da-263">Uygulama Kimliği Hello yazma Kullanıcı adı hello olarak kullanılan (**oturum açma kimliği** hello adımlarda aşağıdaki) hello hizmet sorumlusu,</span><span class="sxs-lookup"><span data-stu-id="230da-263">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="230da-264">Merhaba hizmet asıl izinleri tooaccess varsayılan olarak Azure kaynaklarınızı yok.</span><span class="sxs-lookup"><span data-stu-id="230da-264">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="230da-265">Toogive hello hizmet asıl izinleri toostart gerekir ve durdurun (deallocate) hello kümenin tüm sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="230da-265">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="230da-266">Toohttps://Portal.Azure.com gidin</span><span class="sxs-lookup"><span data-stu-id="230da-266">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="230da-267">Açık hello tüm kaynak dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="230da-267">Open hello All resources blade</span></span>
1. <span data-ttu-id="230da-268">Merhaba sanal makineyi seçin</span><span class="sxs-lookup"><span data-stu-id="230da-268">Select hello virtual machine</span></span>
1. <span data-ttu-id="230da-269">Erişim denetimi (IAM) tıklatın</span><span class="sxs-lookup"><span data-stu-id="230da-269">Click Access control (IAM)</span></span>
1. <span data-ttu-id="230da-270">Ekle'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="230da-270">Click Add</span></span>
1. <span data-ttu-id="230da-271">Merhaba rol sahibi seçin</span><span class="sxs-lookup"><span data-stu-id="230da-271">Select hello role Owner</span></span>
1. <span data-ttu-id="230da-272">Merhaba, yukarıda oluşturduğunuz Merhaba uygulaması adını girin</span><span class="sxs-lookup"><span data-stu-id="230da-272">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="230da-273">Tamam'ı tıklatın</span><span class="sxs-lookup"><span data-stu-id="230da-273">Click OK</span></span>

#### <a name="1-create-hello-stonith-devices"></a><span data-ttu-id="230da-274">**[1]**  Hello STONITH aygıtları oluşturun</span><span class="sxs-lookup"><span data-stu-id="230da-274">**[1]** Create hello STONITH devices</span></span>

<span data-ttu-id="230da-275">Merhaba izinleri hello sanal makineler için düzenlenebilir sonra hello kümede hello STONITH cihazları yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="230da-275">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a><span data-ttu-id="230da-276">**[1]**  STONITH aygıtın hello kullanımını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="230da-276">**[1]** Enable hello use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a><span data-ttu-id="230da-277">(A) SCS ayarlama</span><span class="sxs-lookup"><span data-stu-id="230da-277">Setting up (A)SCS</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="230da-278">Linux dağıtma</span><span class="sxs-lookup"><span data-stu-id="230da-278">Deploying Linux</span></span>

<span data-ttu-id="230da-279">Hello Azure Market görüntü için SAP uygulamaları toodeploy yeni sanal makineleri kullanabilir 12 SUSE Linux Enterprise Server içerir.</span><span class="sxs-lookup"><span data-stu-id="230da-279">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use toodeploy new virtual machines.</span></span> <span data-ttu-id="230da-280">Merhaba Market görüntüsü için SAP NetWeaver hello kaynak aracısı içerir.</span><span class="sxs-lookup"><span data-stu-id="230da-280">hello marketplace image contains hello resource agent for SAP NetWeaver.</span></span>

<span data-ttu-id="230da-281">Merhaba hızlı başlangıç şablonlarından birini github toodeploy üzerinde gerekli tüm kaynakları kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="230da-281">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="230da-282">Merhaba şablon hello sanal makineler, hello yük dengeleyici, kullanılabilirlik vb. kümesi dağıtır. Bu adımları toodeploy hello şablon izleyin:</span><span class="sxs-lookup"><span data-stu-id="230da-282">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="230da-283">Açık hello [ASCS/SCS çoklu SID şablonu] [ template-multisid-xscs] veya hello [şablonu Yakınsanan] [ template-converged] hello Azure portal hello ASCS/SCS şablonunda yalnızca Merhaba yakınsanmış şablon de (örneğin, Microsoft SQL Server veya SAP HANA) bir veritabanı için hello Yük Dengeleme kuralları oluşturur ancak hello Yük Dengeleme kuralları hello SAP NetWeaver ASCS/SCS ve ERS (yalnızca Linux) örnekleri için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="230da-283">Open hello [ASCS/SCS Multi SID template][template-multisid-xscs] or hello [converged template][template-converged] on hello Azure portal hello ASCS/SCS template only creates hello load-balancing rules for hello SAP NetWeaver ASCS/SCS and ERS (Linux only) instances whereas hello converged template also creates hello load-balancing rules for a database (for example Microsoft SQL Server or SAP HANA).</span></span> <span data-ttu-id="230da-284">Tooinstall bir SAP NetWeaver temel sistem planlama ve ayrıca tooinstall hello veritabanı istiyorsanız üzerinde Merhaba aynı makineler, hello kullan [şablonu Yakınsanan][template-converged].</span><span class="sxs-lookup"><span data-stu-id="230da-284">If you plan tooinstall an SAP NetWeaver based system and you also want tooinstall hello database on hello same machines, use hello [converged template][template-converged].</span></span>
1. <span data-ttu-id="230da-285">Şu parametreler hello girin</span><span class="sxs-lookup"><span data-stu-id="230da-285">Enter hello following parameters</span></span>
   1. <span data-ttu-id="230da-286">Kaynak önek (yalnızca ASCS/SCS çoklu SID şablonu)</span><span class="sxs-lookup"><span data-stu-id="230da-286">Resource Prefix (ASCS/SCS Multi SID template only)</span></span>  
      <span data-ttu-id="230da-287">Toouse istediğiniz hello öneki girin.</span><span class="sxs-lookup"><span data-stu-id="230da-287">Enter hello prefix you want toouse.</span></span> <span data-ttu-id="230da-288">Merhaba değer dağıtılan hello kaynaklar için önek olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="230da-288">hello value is used as a prefix for hello resources that are deployed.</span></span>
   3. <span data-ttu-id="230da-289">SAP sistem kimliği (yalnızca yakınsanmış şablonu)</span><span class="sxs-lookup"><span data-stu-id="230da-289">Sap System Id (converged template only)</span></span>  
      <span data-ttu-id="230da-290">Merhaba tooinstall istediğiniz SAP sistemi Hello SAP sistemi kimliği girin.</span><span class="sxs-lookup"><span data-stu-id="230da-290">Enter hello SAP system Id of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="230da-291">Merhaba kimliği önek olarak dağıtılan hello kaynaklar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="230da-291">hello Id is used as a prefix for hello resources that are deployed.</span></span>
   4. <span data-ttu-id="230da-292">Yığın türü</span><span class="sxs-lookup"><span data-stu-id="230da-292">Stack Type</span></span>  
      <span data-ttu-id="230da-293">Merhaba SAP NetWeaver yığın türünü seçin</span><span class="sxs-lookup"><span data-stu-id="230da-293">Select hello SAP NetWeaver stack type</span></span>
   5. <span data-ttu-id="230da-294">İşletim sistemi türü</span><span class="sxs-lookup"><span data-stu-id="230da-294">Os Type</span></span>  
      <span data-ttu-id="230da-295">Merhaba Linux dağıtımları birini seçin.</span><span class="sxs-lookup"><span data-stu-id="230da-295">Select one of hello Linux distributions.</span></span> <span data-ttu-id="230da-296">Bu örnekte, SLES 12 BYOS seçin</span><span class="sxs-lookup"><span data-stu-id="230da-296">For this example, select SLES 12 BYOS</span></span>
   6. <span data-ttu-id="230da-297">DB türü</span><span class="sxs-lookup"><span data-stu-id="230da-297">Db Type</span></span>  
      <span data-ttu-id="230da-298">HANA seçin</span><span class="sxs-lookup"><span data-stu-id="230da-298">Select HANA</span></span>
   7. <span data-ttu-id="230da-299">SAP sistemi boyutu</span><span class="sxs-lookup"><span data-stu-id="230da-299">Sap System Size</span></span>  
      <span data-ttu-id="230da-300">SAP hello yeni sistem Hello miktarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="230da-300">hello amount of SAPS hello new system provides.</span></span> <span data-ttu-id="230da-301">SAP teknolojisi iş ortağı veya sistem Tümleştirici kaç SAP hello sistemi gerektirir emin değilseniz Lütfen isteyin</span><span class="sxs-lookup"><span data-stu-id="230da-301">If you are not sure how many SAPS hello system requires, please ask your SAP Technology Partner or System Integrator</span></span>
   8. <span data-ttu-id="230da-302">Sistem kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="230da-302">System Availability</span></span>  
      <span data-ttu-id="230da-303">HA seçin</span><span class="sxs-lookup"><span data-stu-id="230da-303">Select HA</span></span>
   9. <span data-ttu-id="230da-304">Yönetici kullanıcı adı ve yönetici parolası</span><span class="sxs-lookup"><span data-stu-id="230da-304">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="230da-305">Yeni bir kullanıcı oluşturulur toohello makinede kullanılan toolog olabilir.</span><span class="sxs-lookup"><span data-stu-id="230da-305">A new user is created that can be used toolog on toohello machine.</span></span>
   10. <span data-ttu-id="230da-306">Alt ağ kimliği</span><span class="sxs-lookup"><span data-stu-id="230da-306">Subnet Id</span></span>  
   <span data-ttu-id="230da-307">için Hello kimliği hello alt toowhich hello sanal makinelerin bağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="230da-307">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span>  <span data-ttu-id="230da-308">Kullanılan veya hello NFS sunucu dağıtımının bir parçası oluşturulan aynı alt ağ seçin hello ya da yeni bir sanal ağ toocreate istiyorsanız boş bırakın.</span><span class="sxs-lookup"><span data-stu-id="230da-308">Leave empty if you want toocreate a new virtual network or select hello same subnet that you used or created as part of hello NFS server deployment.</span></span> <span data-ttu-id="230da-309">Merhaba kimliği genellikle /subscriptions/ gibi görünüyor**&lt;abonelik kimliği&gt;**/resourceGroups/**&lt;kaynak grubu adı&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;sanal ağ adı&gt;**/subnets/**&lt;alt ağ adı&gt;**</span><span class="sxs-lookup"><span data-stu-id="230da-309">hello ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="230da-310">Yükleme</span><span class="sxs-lookup"><span data-stu-id="230da-310">Installation</span></span>

<span data-ttu-id="230da-311">Merhaba aşağıdaki öğeleri ile ya da önek **[A]** -geçerli tooall düğümleri **[1]** -yalnızca geçerli toonode 1 veya **[2]** -yalnızca geçerli toonode 2.</span><span class="sxs-lookup"><span data-stu-id="230da-311">hello following items are prefixed with either **[A]** - applicable tooall nodes, **[1]** - only applicable toonode 1 or **[2]** - only applicable toonode 2.</span></span>

1. <span data-ttu-id="230da-312">**[A]**  SLES güncelleştir</span><span class="sxs-lookup"><span data-stu-id="230da-312">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="230da-313">**[1]**  Ssh erişimini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="230da-313">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="230da-314">**[2]**  Ssh erişimini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="230da-314">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="230da-315">**[1]**  Ssh erişimini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="230da-315">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="230da-316">**[A]**  Yükleme HA uzantısı</span><span class="sxs-lookup"><span data-stu-id="230da-316">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="230da-317">**[A]**  Güncelleştirme SAP kaynak aracıları</span><span class="sxs-lookup"><span data-stu-id="230da-317">**[A]** Update SAP resource agents</span></span>  
   
   <span data-ttu-id="230da-318">Merhaba kaynak aracıları paket için bir düzeltme eki gerekli toouse hello bu makalede açıklanan yeni yapılandırma, ' dir.</span><span class="sxs-lookup"><span data-stu-id="230da-318">A patch for hello resource-agents package is required toouse hello new configuration, that is described in this article.</span></span> <span data-ttu-id="230da-319">Merhaba düzeltme eki komutu aşağıdaki hello ile zaten yüklüyse, kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="230da-319">You can check, if hello patch is already installed with hello following command</span></span>

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   <span data-ttu-id="230da-320">Merhaba çıktısı benzer olmalıdır</span><span class="sxs-lookup"><span data-stu-id="230da-320">hello output should be similar to</span></span>

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   <span data-ttu-id="230da-321">Hello grep komutu hello IS_ERS parametresi bulamazsa, listelenen tooinstall hello düzeltme eki gereksinim [hello SUSE indirme sayfası](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span><span class="sxs-lookup"><span data-stu-id="230da-321">If hello grep command does not find hello IS_ERS parameter, you need tooinstall hello patch listed on [hello SUSE download page](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span></span>

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. <span data-ttu-id="230da-322">**[A]**  Kurulum ana bilgisayar adı çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="230da-322">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="230da-323">Bir DNS sunucusu kullanın veya tüm düğümlerde hello/etc/hosts değiştirin.</span><span class="sxs-lookup"><span data-stu-id="230da-323">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="230da-324">Bu örnek nasıl toouse hello/etc/hosts dosyasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="230da-324">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="230da-325">Başlangıç IP adresi ve hello hostname komutları aşağıdaki hello olarak değiştirin</span><span class="sxs-lookup"><span data-stu-id="230da-325">Replace hello IP address and hello hostname in hello following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="230da-326">Aşağıdaki satırları çok/etc/hosts hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="230da-326">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="230da-327">Başlangıç IP adresi ve ana bilgisayar adı toomatch ortamınızı değiştirme</span><span class="sxs-lookup"><span data-stu-id="230da-327">Change hello IP address and hostname toomatch your environment</span></span>   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. <span data-ttu-id="230da-328">**[1]**  Küme yükleyin</span><span class="sxs-lookup"><span data-stu-id="230da-328">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="230da-329">**[2]**  Düğüm toocluster Ekle</span><span class="sxs-lookup"><span data-stu-id="230da-329">**[2]** Add node toocluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="230da-330">**[A]**  Değişiklik hacluster parola toohello aynı parola</span><span class="sxs-lookup"><span data-stu-id="230da-330">**[A]** Change hacluster password toohello same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="230da-331">**[A]**  Corosync toouse diğer aktarım yapılandırmak ve listesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="230da-331">**[A]** Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="230da-332">Aksi takdirde, küme çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="230da-332">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="230da-333">Merhaba aşağıdaki kalın içerik toohello dosyasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="230da-333">Add hello following bold content toohello file.</span></span>
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>nws-cl-0</b>
      ring0_addr:     10.0.0.14
     }
     node {
      # IP address of <b>nws-cl-1</b>
      ring0_addr:     10.0.0.13
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   <span data-ttu-id="230da-334">Merhaba corosync hizmetini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="230da-334">Then restart hello corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="230da-335">**[A]**  Drbd bileşenlerini yükleme</span><span class="sxs-lookup"><span data-stu-id="230da-335">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="230da-336">**[A]**  Hello drbd cihaz için bir bölüm oluşturun</span><span class="sxs-lookup"><span data-stu-id="230da-336">**[A]** Create a partition for hello drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="230da-337">**[A]**  LVM oluşturma yapılandırmaları</span><span class="sxs-lookup"><span data-stu-id="230da-337">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. <span data-ttu-id="230da-338">**[A]**  Oluşturma hello SCS drbd aygıt</span><span class="sxs-lookup"><span data-stu-id="230da-338">**[A]** Create hello SCS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   <span data-ttu-id="230da-339">Merhaba yeni drbd aygıt ve çıkış Hello Yapılandırması Ekle</span><span class="sxs-lookup"><span data-stu-id="230da-339">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_ascs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="230da-340">Merhaba drbd aygıtı oluşturun ve başlatın</span><span class="sxs-lookup"><span data-stu-id="230da-340">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. <span data-ttu-id="230da-341">**[A]**  Oluşturma hello ERS drbd aygıt</span><span class="sxs-lookup"><span data-stu-id="230da-341">**[A]** Create hello ERS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   <span data-ttu-id="230da-342">Merhaba yeni drbd aygıt ve çıkış Hello Yapılandırması Ekle</span><span class="sxs-lookup"><span data-stu-id="230da-342">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_ers {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="230da-343">Merhaba drbd aygıtı oluşturun ve başlatın</span><span class="sxs-lookup"><span data-stu-id="230da-343">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="230da-344">**[1]**  Atla ilk eşitleme</span><span class="sxs-lookup"><span data-stu-id="230da-344">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="230da-345">**[1]**  Kümesi hello birincil düğüm</span><span class="sxs-lookup"><span data-stu-id="230da-345">**[1]** Set hello primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="230da-346">**[1]**  Hello yeni drbd aygıtları eşitlenir kadar bekleyin</span><span class="sxs-lookup"><span data-stu-id="230da-346">**[1]** Wait until hello new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:93991268 nr:0 dw:93991268 dr:93944920 al:383 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 1: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:6047920 nr:0 dw:6047920 dr:6039112 al:34 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 2: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:5142732 nr:0 dw:5142732 dr:5133924 al:30 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="230da-347">**[1]**  Dosya sistemleri üzerinde hello drbd aygıtları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="230da-347">**[1]** Create file systems on hello drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="230da-348">Küme çerçeve Yapılandır</span><span class="sxs-lookup"><span data-stu-id="230da-348">Configure Cluster Framework</span></span>

<span data-ttu-id="230da-349">**[1]**  Hello varsayılan ayarları değiştir</span><span class="sxs-lookup"><span data-stu-id="230da-349">**[1]** Change hello default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a><span data-ttu-id="230da-350">SAP NetWeaver yükleme için hazırlama</span><span class="sxs-lookup"><span data-stu-id="230da-350">Prepare for SAP NetWeaver installation</span></span>

1. <span data-ttu-id="230da-351">**[A]**  Oluşturma hello paylaşılan dizinler</span><span class="sxs-lookup"><span data-stu-id="230da-351">**[A]** Create hello shared directories</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. <span data-ttu-id="230da-352">**[A]**  Autofs yapılandırın</span><span class="sxs-lookup"><span data-stu-id="230da-352">**[A]** Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="230da-353">Dosya Oluştur</span><span class="sxs-lookup"><span data-stu-id="230da-353">Create a file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   <span data-ttu-id="230da-354">AutoFS toomount hello yeni paylaşımlar yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="230da-354">Restart autofs toomount hello new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="230da-355">**[A]**  Yapılandırma TAKAS dosyası</span><span class="sxs-lookup"><span data-stu-id="230da-355">**[A]** Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="230da-356">Merhaba Aracısı tooactivate hello değişiklik yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="230da-356">Restart hello Agent tooactivate hello change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a><span data-ttu-id="230da-357">SAP NetWeaver ASCS/ERS yükleme</span><span class="sxs-lookup"><span data-stu-id="230da-357">Installing SAP NetWeaver ASCS/ERS</span></span>

1. <span data-ttu-id="230da-358">**[1]**  Bir sanal IP kaynak ve sistem durumu araştırması hello iç yük dengeleyici için oluşturma</span><span class="sxs-lookup"><span data-stu-id="230da-358">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm node standby <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ASCS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ascs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ASCS drbd_<b>NWS</b>_ASCS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ASCS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/usr/sap/<b>NWS</b>/ASCS<b>00</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ASCS IPaddr2 \
     params ip=<b>10.0.0.10</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ASCS anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 620<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0
   
   crm(live)configure# group g-<b>NWS</b>_ASCS nc_<b>NWS</b>_ASCS vip_<b>NWS</b>_ASCS fs_<b>NWS</b>_ASCS \
      meta resource-stickiness=3000

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ASCS inf: \
     ms-drbd_<b>NWS</b>_ASCS:promote g-<b>NWS</b>_ASCS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ASCS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ASCS:Master g-<b>NWS</b>_ASCS
   
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   <span data-ttu-id="230da-359">Merhaba küme durumunun Tamam olduğunu ve tüm kaynakları başlatıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="230da-359">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="230da-360">Hangi düğümün hello kaynaklar üzerinde çalışan önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="230da-360">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Node nws-cl-1: standby
   # <b>Online: [ nws-cl-0 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      Stopped: [ nws-cl-1 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   </code></pre>

1. <span data-ttu-id="230da-361">**[1]**  SAP NetWeaver ASCS yükleyin</span><span class="sxs-lookup"><span data-stu-id="230da-361">**[1]** Install SAP NetWeaver ASCS</span></span>  

   <span data-ttu-id="230da-362">SAP NetWeaver ASCS toohello IP adresi yapılandırmasının hello yük dengeleyici ön uç hello ASCS için örneğin eşleşen bir sanal ana bilgisayar adı kullanarak hello ilk düğümde kök Yükle <b>nws ascs</b>, <b>10.0.0.10</b>ve örneğin hello hello yük dengeleyici araştırması için kullanılan hello örnek numarasını <b>00</b>.</span><span class="sxs-lookup"><span data-stu-id="230da-362">Install SAP NetWeaver ASCS as root on hello first node using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello ASCS for example <b>nws-ascs</b>, <b>10.0.0.10</b> and hello instance number that you used for hello probe of hello load balancer for example <b>00</b>.</span></span>

   <span data-ttu-id="230da-363">Merhaba sapinst parametresi SAPINST_REMOTE_ACCESS_USER tooallow kök olmayan kullanıcı tooconnect toosapinst kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="230da-363">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="230da-364">**[1]**  Bir sanal IP kaynak ve sistem durumu araştırması hello iç yük dengeleyici için oluşturma</span><span class="sxs-lookup"><span data-stu-id="230da-364">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm node standby <b>nws-cl-0</b>
   sudo crm node online <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ERS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ers" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ERS drbd_<b>NWS</b>_ERS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ERS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd1 \
     directory=/usr/sap/<b>NWS</b>/ERS<b>02</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ERS IPaddr2 \
     params ip=<b>10.0.0.11</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ERS anything \
    params binfile="/usr/bin/nc" cmdline_options="-l -k 621<b>02</b>" \
    op monitor timeout=20s interval=10 depth=0

   crm(live)configure# group g-<b>NWS</b>_ERS nc_<b>NWS</b>_ERS vip_<b>NWS</b>_ERS fs_<b>NWS</b>_ERS

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ERS inf: \
     ms-drbd_<b>NWS</b>_ERS:promote g-<b>NWS</b>_ERS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ERS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ERS:Master g-<b>NWS</b>_ERS
   
   crm(live)configure# commit
   # WARNING: Resources nc_NWS_ASCS,nc_NWS_ERS,nc_NWS_nfs violate uniqueness for parameter "binfile": "/usr/bin/nc"
   # Do you still want toocommit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   <span data-ttu-id="230da-365">Merhaba küme durumunun Tamam olduğunu ve tüm kaynakları başlatıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="230da-365">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="230da-366">Hangi düğümün hello kaynaklar üzerinde çalışan önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="230da-366">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Node <b>nws-cl-0: standby</b>
   # <b>Online: [ nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   </code></pre>

1. <span data-ttu-id="230da-367">**[2]**  SAP NetWeaver ERS yükleyin</span><span class="sxs-lookup"><span data-stu-id="230da-367">**[2]** Install SAP NetWeaver ERS</span></span>  

   <span data-ttu-id="230da-368">SAP NetWeaver ERS hello yük dengeleyici ön uç yapılandırmasında hello ERS toohello IP adresini örneğin eşleşen bir sanal ana bilgisayar adı kullanarak hello ikinci düğümde kök Yükle <b>nws ers</b>, <b>10.0.0.11</b> ve örneğin hello hello yük dengeleyici araştırması için kullanılan hello örnek numarasını <b>02</b>.</span><span class="sxs-lookup"><span data-stu-id="230da-368">Install SAP NetWeaver ERS as root on hello second node using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello ERS for example <b>nws-ers</b>, <b>10.0.0.11</b> and hello instance number that you used for hello probe of hello load balancer for example <b>02</b>.</span></span>

   <span data-ttu-id="230da-369">Merhaba sapinst parametresi SAPINST_REMOTE_ACCESS_USER tooallow kök olmayan kullanıcı tooconnect toosapinst kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="230da-369">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > <span data-ttu-id="230da-370">Lütfen SWPM SP 20 PL 05 ya da daha yüksek kullanın.</span><span class="sxs-lookup"><span data-stu-id="230da-370">Please use SWPM SP 20 PL 05 or higher.</span></span> <span data-ttu-id="230da-371">Daha düşük sürümleri hello izinleri düzgün ayarlanmamış ve hello yükleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="230da-371">Lower versions do not set hello permissions correctly and hello installation will fail.</span></span>
   > 

1. <span data-ttu-id="230da-372">**[1]**  Hello ASCS/SCS ve ERS örneği profilleri uyarlama</span><span class="sxs-lookup"><span data-stu-id="230da-372">**[1]** Adapt hello ASCS/SCS and ERS instance profiles</span></span>
 
   * <span data-ttu-id="230da-373">ASCS/SCS profili</span><span class="sxs-lookup"><span data-stu-id="230da-373">ASCS/SCS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change hello restart command tooa start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add hello keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * <span data-ttu-id="230da-374">ERS profili</span><span class="sxs-lookup"><span data-stu-id="230da-374">ERS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. <span data-ttu-id="230da-375">**[A]**  Tutmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="230da-375">**[A]** Configure Keep Alive</span></span>

   <span data-ttu-id="230da-376">Merhaba ASCS/SCS hello SAP NetWeaver uygulama sunucusu arasındaki Hello iletişimi yazılım yük dengeleyici yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="230da-376">hello communication between hello SAP NetWeaver application server and hello ASCS/SCS is routed through a software load balancer.</span></span> <span data-ttu-id="230da-377">Merhaba yük dengeleyici yapılandırılabilir bir zaman aşımından sonra etkin olmayan bağlantıları bağlantısını keser.</span><span class="sxs-lookup"><span data-stu-id="230da-377">hello load balancer disconnects inactive connections after a configurable timeout.</span></span> <span data-ttu-id="230da-378">tooprevent bu tooset hello SAP NetWeaver ASCS/SCS profili parametresinde gerekir ve hello Linux sistem ayarlarını değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="230da-378">tooprevent this you need tooset a parameter in hello SAP NetWeaver ASCS/SCS profile and change hello Linux system settings.</span></span> <span data-ttu-id="230da-379">Lütfen okuyun [SAP Not 1410736] [ 1410736] daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="230da-379">Please read [SAP Note 1410736][1410736] for more information.</span></span>
   
   <span data-ttu-id="230da-380">Merhaba ASCS/SCS profili parametre CLR'yi/encni/set_so_keepalive hello son adımda zaten eklendi.</span><span class="sxs-lookup"><span data-stu-id="230da-380">hello ASCS/SCS profile parameter enque/encni/set_so_keepalive was already added in hello last step.</span></span>

   <pre><code> 
   # Change hello Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. <span data-ttu-id="230da-381">**[A]**  Hello yüklendikten sonra hello SAP kullanıcıları yapılandırın</span><span class="sxs-lookup"><span data-stu-id="230da-381">**[A]** Configure hello SAP users after hello installation</span></span>
 
   <pre><code>
   # Add sidadm toohello haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. <span data-ttu-id="230da-382">**[1]**  Hello ASCS ve ERS SAP Hizmetleri toohello sapservice Dosya Ekle</span><span class="sxs-lookup"><span data-stu-id="230da-382">**[1]** Add hello ASCS and ERS SAP services toohello sapservice file</span></span>

   <span data-ttu-id="230da-383">Merhaba ASCS hizmet girişi toohello ikinci düğümü ve kopyalama hello ERS hizmet girişi toohello ilk düğümü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="230da-383">Add hello ASCS service entry toohello second node and copy hello ERS service entry toohello first node.</span></span>

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. <span data-ttu-id="230da-384">**[1]**  Hello SAP küme kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="230da-384">**[1]** Create hello SAP cluster resources</span></span>

   <pre><code>
   sudo crm configure property maintenance-mode="true"

   sudo crm configure

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ASCS<b>00</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ASCS<b>00</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b>" \
    AUTOMATIC_RECOVER=false \
    meta resource-stickiness=5000 failure-timeout=60 migration-threshold=1 priority=10

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ERS<b>02</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ERS<b>02</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>" AUTOMATIC_RECOVER=false IS_ERS=true \
    meta priority=1000

   crm(live)configure# modgroup g-<b>NWS</b>_ASCS add rsc_sap_<b>NWS</b>_ASCS<b>00</b>
   crm(live)configure# modgroup g-<b>NWS</b>_ERS add rsc_sap_<b>NWS</b>_ERS<b>02</b>

   crm(live)configure# colocation col_sap_<b>NWS</b>_no_both -5000: g-<b>NWS</b>_ERS g-<b>NWS</b>_ASCS
   crm(live)configure# location loc_sap_<b>NWS</b>_failover_to_ers rsc_sap_<b>NWS</b>_ASCS<b>00</b> rule 2000: runs_ers_<b>NWS</b> eq 1
   crm(live)configure# order ord_sap_<b>NWS</b>_first_start_ascs Optional: rsc_sap_<b>NWS</b>_ASCS<b>00</b>:start rsc_sap_<b>NWS</b>_ERS<b>02</b>:stop symmetrical=false

   crm(live)configure# commit
   crm(live)configure# exit

   sudo crm configure property maintenance-mode="false"
   sudo crm node online <b>nws-cl-0</b>
   </code></pre>

   <span data-ttu-id="230da-385">Merhaba küme durumunun Tamam olduğunu ve tüm kaynakları başlatıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="230da-385">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="230da-386">Hangi düğümün hello kaynaklar üzerinde çalışan önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="230da-386">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Online: <b>[ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   </code></pre>

### <a name="create-stonith-device"></a><span data-ttu-id="230da-387">STONITH cihaz oluşturma</span><span class="sxs-lookup"><span data-stu-id="230da-387">Create STONITH device</span></span>

<span data-ttu-id="230da-388">Merhaba STONITH aygıt Microsoft Azure karşı bir hizmet sorumlusu tooauthorize kullanır.</span><span class="sxs-lookup"><span data-stu-id="230da-388">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="230da-389">Bu adımları toocreate bir hizmet sorumlusu izleyin.</span><span class="sxs-lookup"><span data-stu-id="230da-389">Follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="230da-390">Çok Git<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="230da-390">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="230da-391">Açık hello Azure Active Directory dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="230da-391">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="230da-392">TooProperties gidin ve dizin kimliği hello yazma Merhaba budur **Kiracı kimliği**.</span><span class="sxs-lookup"><span data-stu-id="230da-392">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="230da-393">Uygulama kayıtlar'ı tıklatın</span><span class="sxs-lookup"><span data-stu-id="230da-393">Click App registrations</span></span>
1. <span data-ttu-id="230da-394">Ekle'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="230da-394">Click Add</span></span>
1. <span data-ttu-id="230da-395">Bir ad girin, uygulama türü "Web uygulaması/API" seçin, bir oturum açma URL'si (örneğin http://localhost) girin ve Oluştur'u tıklatın</span><span class="sxs-lookup"><span data-stu-id="230da-395">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="230da-396">Merhaba oturum açma URL'si kullanılmaz ve geçerli bir URL olabilir</span><span class="sxs-lookup"><span data-stu-id="230da-396">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="230da-397">Select hello yeni uygulama ve anahtarları hello ayarları sekmesini tıklatın</span><span class="sxs-lookup"><span data-stu-id="230da-397">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="230da-398">Yeni bir anahtar için bir açıklama girin, "Her zaman geçerli olsun" seçin ve Kaydet</span><span class="sxs-lookup"><span data-stu-id="230da-398">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="230da-399">Değer Hello yazın.</span><span class="sxs-lookup"><span data-stu-id="230da-399">Write down hello Value.</span></span> <span data-ttu-id="230da-400">Hello kullanılan **parola** hello hizmet sorumlusu için</span><span class="sxs-lookup"><span data-stu-id="230da-400">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="230da-401">Uygulama Kimliği Hello yazma Kullanıcı adı hello olarak kullanılan (**oturum açma kimliği** hello adımlarda aşağıdaki) hello hizmet sorumlusu,</span><span class="sxs-lookup"><span data-stu-id="230da-401">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="230da-402">Merhaba hizmet asıl izinleri tooaccess varsayılan olarak Azure kaynaklarınızı yok.</span><span class="sxs-lookup"><span data-stu-id="230da-402">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="230da-403">Toogive hello hizmet asıl izinleri toostart gerekir ve durdurun (deallocate) hello kümenin tüm sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="230da-403">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="230da-404">Toohttps://Portal.Azure.com gidin</span><span class="sxs-lookup"><span data-stu-id="230da-404">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="230da-405">Açık hello tüm kaynak dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="230da-405">Open hello All resources blade</span></span>
1. <span data-ttu-id="230da-406">Merhaba sanal makineyi seçin</span><span class="sxs-lookup"><span data-stu-id="230da-406">Select hello virtual machine</span></span>
1. <span data-ttu-id="230da-407">Erişim denetimi (IAM) tıklatın</span><span class="sxs-lookup"><span data-stu-id="230da-407">Click Access control (IAM)</span></span>
1. <span data-ttu-id="230da-408">Ekle'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="230da-408">Click Add</span></span>
1. <span data-ttu-id="230da-409">Merhaba rol sahibi seçin</span><span class="sxs-lookup"><span data-stu-id="230da-409">Select hello role Owner</span></span>
1. <span data-ttu-id="230da-410">Merhaba, yukarıda oluşturduğunuz Merhaba uygulaması adını girin</span><span class="sxs-lookup"><span data-stu-id="230da-410">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="230da-411">Tamam'ı tıklatın</span><span class="sxs-lookup"><span data-stu-id="230da-411">Click OK</span></span>

#### <a name="1-create-hello-stonith-devices"></a><span data-ttu-id="230da-412">**[1]**  Hello STONITH aygıtları oluşturun</span><span class="sxs-lookup"><span data-stu-id="230da-412">**[1]** Create hello STONITH devices</span></span>

<span data-ttu-id="230da-413">Merhaba izinleri hello sanal makineler için düzenlenebilir sonra hello kümede hello STONITH cihazları yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="230da-413">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a><span data-ttu-id="230da-414">**[1]**  STONITH aygıtın hello kullanımını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="230da-414">**[1]** Enable hello use of a STONITH device</span></span>

<span data-ttu-id="230da-415">STONITH aygıt Hello kullanımını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="230da-415">Enable hello use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a><span data-ttu-id="230da-416">Veritabanını yükleme</span><span class="sxs-lookup"><span data-stu-id="230da-416">Install database</span></span>

<span data-ttu-id="230da-417">Bu örnekte bir SAP HANA sistem çoğaltma yüklenmiş ve yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="230da-417">In this example an SAP HANA System Replication is installed and configured.</span></span> <span data-ttu-id="230da-418">SAP HANA hello aynı küme hello SAP NetWeaver ASCS/SCS ve ERS çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="230da-418">SAP HANA will run in hello same cluster as hello SAP NetWeaver ASCS/SCS and ERS.</span></span> <span data-ttu-id="230da-419">SAP HANA adanmış bir kümede de yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="230da-419">You can also install SAP HANA on a dedicated cluster.</span></span> <span data-ttu-id="230da-420">Bkz: [SAP HANA, yüksek kullanılabilirlik'Azure sanal makineler (VM'ler) üzerinde] [ sap-hana-ha] daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="230da-420">See [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha] for more information.</span></span>

### <a name="prepare-for-sap-hana-installation"></a><span data-ttu-id="230da-421">SAP HANA yükleme için hazırlama</span><span class="sxs-lookup"><span data-stu-id="230da-421">Prepare for SAP HANA installation</span></span>

<span data-ttu-id="230da-422">Genellikle, veri ve günlük dosyalarını birimleri için LVM kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="230da-422">We generally recommend using LVM for volumes that store data and log files.</span></span> <span data-ttu-id="230da-423">Test amacıyla, doğrudan düz bir diskte toostore hello veri ve günlük dosyası da seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="230da-423">For testing purposes, you can also choose toostore hello data and log file directly on a plain disk.</span></span>

1. <span data-ttu-id="230da-424">**[A]**  LVM</span><span class="sxs-lookup"><span data-stu-id="230da-424">**[A]** LVM</span></span>  
   <span data-ttu-id="230da-425">Aşağıdaki Hello örnek hello sanal makineleri kullanılan toocreate iki birimlerin olmalıdır bağlı dört veri diskleri sahip olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="230da-425">hello example below assumes that hello virtual machines have four data disks attached that should be used toocreate two volumes.</span></span>
   
   <span data-ttu-id="230da-426">Toouse istediğiniz tüm disklerin fiziksel birimler oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="230da-426">Create physical volumes for all disks that you want toouse.</span></span>
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   <span data-ttu-id="230da-427">Merhaba veri dosyaları için bir birim grubu, hello günlük dosyaları için bir birim grubu ve SAP HANA hello paylaşılan dizini için bir tane oluşturun</span><span class="sxs-lookup"><span data-stu-id="230da-427">Create a volume group for hello data files, one volume group for hello log files and one for hello shared directory of SAP HANA</span></span>
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   <span data-ttu-id="230da-428">Merhaba mantıksal birim oluşturun</span><span class="sxs-lookup"><span data-stu-id="230da-428">Create hello logical volumes</span></span>
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   <span data-ttu-id="230da-429">Merhaba bağlama dizinler oluşturun ve hello UUID tüm mantıksal birimlerin kopyalama</span><span class="sxs-lookup"><span data-stu-id="230da-429">Create hello mount directories and copy hello UUID of all logical volumes</span></span>
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   <span data-ttu-id="230da-430">Merhaba AutoFS girişlerinde üç mantıksal birim oluşturma</span><span class="sxs-lookup"><span data-stu-id="230da-430">Create autofs entries for hello three logical volumes</span></span>
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   <span data-ttu-id="230da-431">Bu satırı toosudo VI /etc/auto.direct Ekle</span><span class="sxs-lookup"><span data-stu-id="230da-431">Insert this line toosudo vi /etc/auto.direct</span></span>
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   <span data-ttu-id="230da-432">Merhaba yeni birimleri bağlayın</span><span class="sxs-lookup"><span data-stu-id="230da-432">Mount hello new volumes</span></span>
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. <span data-ttu-id="230da-433">**[A]**  Düz diskleri</span><span class="sxs-lookup"><span data-stu-id="230da-433">**[A]** Plain Disks</span></span>  

   <span data-ttu-id="230da-434">Küçük veya gösteri sistemleri HANA veri ve günlük dosyalarınızı bir disk yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="230da-434">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="230da-435">Merhaba aşağıdaki komutları /dev/sdc üzerinde bir bölüm oluşturun ve xfs ile biçimlendirin.</span><span class="sxs-lookup"><span data-stu-id="230da-435">hello following commands create a partition on /dev/sdc and format it with xfs.</span></span>
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down hello id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   <span data-ttu-id="230da-436">Bu satırı too/etc/auto.direct Ekle</span><span class="sxs-lookup"><span data-stu-id="230da-436">Insert this line too/etc/auto.direct</span></span>
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   <span data-ttu-id="230da-437">Merhaba hedef dizin oluşturun ve hello diski bağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="230da-437">Create hello target directory and mount hello disk.</span></span>
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a><span data-ttu-id="230da-438">SAP HANA yükleme</span><span class="sxs-lookup"><span data-stu-id="230da-438">Installing SAP HANA</span></span>

<span data-ttu-id="230da-439">Merhaba aşağıdaki adımları hello bölüm 4 dayalı [SAP HANA SR performansı en iyi duruma getirilmiş senaryo Kılavuzu] [ suse-hana-ha-guide] tooinstall SAP HANA sistem çoğaltma.</span><span class="sxs-lookup"><span data-stu-id="230da-439">hello following steps are based on chapter 4 of hello [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span></span> <span data-ttu-id="230da-440">Lütfen hello yüklemeye devam etmeden önce bunu okuyun.</span><span class="sxs-lookup"><span data-stu-id="230da-440">Please read it before you continue hello installation.</span></span>

1. <span data-ttu-id="230da-441">**[A]**  Hdblcm HANA DVD hello çalıştırın</span><span class="sxs-lookup"><span data-stu-id="230da-441">**[A]** Run hdblcm from hello HANA DVD</span></span>
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. <span data-ttu-id="230da-442">**[A]**  Yükseltme SAP konak Aracısı</span><span class="sxs-lookup"><span data-stu-id="230da-442">**[A]** Upgrade SAP Host Agent</span></span>

   <span data-ttu-id="230da-443">Hello Hello son SAP konak Aracısı arşivi indir [SAP Softwarecenter] [ sap-swcenter] ve çalışma hello komutu tooupgrade hello aracısı aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="230da-443">Download hello latest SAP Host Agent archive from hello [SAP Softwarecenter][sap-swcenter] and run hello following command tooupgrade hello agent.</span></span> <span data-ttu-id="230da-444">Merhaba yolu toohello arşiv toopoint toohello dosyasını indirdiğiniz değiştirin.</span><span class="sxs-lookup"><span data-stu-id="230da-444">Replace hello path toohello archive toopoint toohello file you downloaded.</span></span>
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path tooSAP Host Agent SAR&gt;</b> 
   </code></pre>

1. <span data-ttu-id="230da-445">**[1]**  (Kök) olarak oluşturma HANA çoğaltma</span><span class="sxs-lookup"><span data-stu-id="230da-445">**[1]** Create HANA replication (as root)</span></span>  

   <span data-ttu-id="230da-446">Merhaba aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="230da-446">Run hello following command.</span></span> <span data-ttu-id="230da-447">SAP HANA yüklemenizin hello değerlerle emin tooreplace kalın dizeleri (HANA sistem kimliği HDB ile örnek numarasını 03) olun.</span><span class="sxs-lookup"><span data-stu-id="230da-447">Make sure tooreplace bold strings (HANA System ID HDB and instance number 03) with hello values of your SAP HANA installation.</span></span>
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. <span data-ttu-id="230da-448">**[A]**  (Kök) olarak bir anahtar girişi oluşturun</span><span class="sxs-lookup"><span data-stu-id="230da-448">**[A]** Create keystore entry (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. <span data-ttu-id="230da-449">**[1]**  Backup database (kök) olarak</span><span class="sxs-lookup"><span data-stu-id="230da-449">**[1]** Backup database (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. <span data-ttu-id="230da-450">**[1]**  Geçiş toohello HANA sapsid kullanıcı ve hello birincil site oluşturun.</span><span class="sxs-lookup"><span data-stu-id="230da-450">**[1]** Switch toohello HANA sapsid user and create hello primary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. <span data-ttu-id="230da-451">**[2]**  Toohello HANA sapsid kullanıcı geçin ve hello ikincil site oluştur.</span><span class="sxs-lookup"><span data-stu-id="230da-451">**[2]** Switch toohello HANA sapsid user and create hello secondary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. <span data-ttu-id="230da-452">**[1]**  Oluşturma SAP HANA küme kaynakları</span><span class="sxs-lookup"><span data-stu-id="230da-452">**[1]** Create SAP HANA cluster resources</span></span>

   <span data-ttu-id="230da-453">İlk olarak hello topoloji oluşturun.</span><span class="sxs-lookup"><span data-stu-id="230da-453">First, create hello topology.</span></span>
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number and HANA system id
   
   crm(live)configure# primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b>   ocf:suse:SAPHanaTopology \
     operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
     op monitor interval="10" timeout="600" \
     op start interval="0" timeout="600" \
     op stop interval="0" timeout="300" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"
    
   crm(live)configure# clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>
   
   <span data-ttu-id="230da-454">Ardından, hello HANA kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="230da-454">Next, create hello HANA resources</span></span>
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
    
   crm(live)configure# primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
     operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
     op start interval="0" timeout="3600" \
     op stop interval="0" timeout="3600" \
     op promote interval="0" timeout="3600" \
     op monitor interval="60" role="Master" timeout="700" \
     op monitor interval="61" role="Slave" timeout="700" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
     DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"
    
   crm(live)configure# ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
     target-role="Started" interleave="true"
    
   crm(live)configure# primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
     meta target-role="Started" is-managed="true" \ 
     operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
     op monitor interval="10s" timeout="20s" \ 
     params ip="<b>10.0.0.12</b>" 

   crm(live)configure# primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
     params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
     op monitor timeout=20s interval=10 depth=0 

   crm(live)configure# group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  

   crm(live)configure# order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   <span data-ttu-id="230da-455">Merhaba küme durumunun Tamam olduğunu ve tüm kaynakları başlatıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="230da-455">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="230da-456">Hangi düğümün hello kaynaklar üzerinde çalışan önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="230da-456">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # <b>Online: [ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Clone Set: cln_SAPHanaTopology_HDB_HDB03 [rsc_SAPHanaTopology_HDB_HDB03]
   #      <b>Started: [ nws-cl-0 nws-cl-1 ]</b>
   #  Master/Slave Set: msl_SAPHana_HDB_HDB03 [rsc_SAPHana_HDB_HDB03]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g_ip_HDB_HDB03
   #      rsc_ip_HDB_HDB03   (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      rsc_nc_HDB_HDB03   (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   # rsc_st_azure_1  (stonith:fence_azure_arm):      <b>Started nws-cl-0</b>
   # rsc_st_azure_2  (stonith:fence_azure_arm):      <b>Started nws-cl-1</b>
   </code></pre>

1. <span data-ttu-id="230da-457">**[1]**  Yükleme hello SAP NetWeaver veritabanı örneği</span><span class="sxs-lookup"><span data-stu-id="230da-457">**[1]** Install hello SAP NetWeaver database instance</span></span>

   <span data-ttu-id="230da-458">Yükleme hello SAP NetWeaver veritabanı örneği örneğin toohello IP adresi yapılandırmasının hello yük dengeleyici ön uç hello veritabanı için eşleşen bir sanal ana bilgisayar adı kullanarak kök olarak <b>nws db</b> ve <b>10.0.0.12</b>.</span><span class="sxs-lookup"><span data-stu-id="230da-458">Install hello SAP NetWeaver database instance as root using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello database for example <b>nws-db</b> and <b>10.0.0.12</b>.</span></span>

   <span data-ttu-id="230da-459">Merhaba sapinst parametresi SAPINST_REMOTE_ACCESS_USER tooallow kök olmayan kullanıcı tooconnect toosapinst kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="230da-459">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a><span data-ttu-id="230da-460">SAP NetWeaver uygulama sunucusu yükleme</span><span class="sxs-lookup"><span data-stu-id="230da-460">SAP NetWeaver application server installation</span></span>

<span data-ttu-id="230da-461">Bu adımları tooinstall SAP uygulama sunucusu izleyin.</span><span class="sxs-lookup"><span data-stu-id="230da-461">Follow these steps tooinstall an SAP application server.</span></span> <span data-ttu-id="230da-462">Merhaba adımları aşağıdaki varsayalım ASCS/SCS hello farklı bir sunucuda hello uygulama sunucusu ve HANA sunucularına yükleyin.</span><span class="sxs-lookup"><span data-stu-id="230da-462">hello steps bellow assume that you install hello application server on a server different from hello ASCS/SCS and HANA servers.</span></span> <span data-ttu-id="230da-463">Aksi takdirde (ana bilgisayar adı çözümlemesi yapılandırma gibi) hello adımları bazıları gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="230da-463">Otherwise some of hello steps below (like configuring host name resolution) are not needed.</span></span>

1. <span data-ttu-id="230da-464">Ana bilgisayar adı çözümlemesi Kurulumu</span><span class="sxs-lookup"><span data-stu-id="230da-464">Setup host name resolution</span></span>    
   <span data-ttu-id="230da-465">Bir DNS sunucusu kullanın veya tüm düğümlerde hello/etc/hosts değiştirin.</span><span class="sxs-lookup"><span data-stu-id="230da-465">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="230da-466">Bu örnek nasıl toouse hello/etc/hosts dosyasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="230da-466">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="230da-467">Başlangıç IP adresi ve hello hostname komutları aşağıdaki hello olarak değiştirin</span><span class="sxs-lookup"><span data-stu-id="230da-467">Replace hello IP address and hello hostname in hello following commands</span></span>
   ```bash
   sudo vi /etc/hosts
   ```
   <span data-ttu-id="230da-468">Aşağıdaki satırları çok/etc/hosts hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="230da-468">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="230da-469">Başlangıç IP adresi ve ana bilgisayar adı toomatch ortamınızı değiştirme</span><span class="sxs-lookup"><span data-stu-id="230da-469">Change hello IP address and hostname toomatch your environment</span></span>    
    
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of hello application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. <span data-ttu-id="230da-470">Merhaba sapmnt dizin oluşturun</span><span class="sxs-lookup"><span data-stu-id="230da-470">Create hello sapmnt directory</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. <span data-ttu-id="230da-471">AutoFS yapılandırın</span><span class="sxs-lookup"><span data-stu-id="230da-471">Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="230da-472">Yeni dosya oluştur</span><span class="sxs-lookup"><span data-stu-id="230da-472">Create a new file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   <span data-ttu-id="230da-473">AutoFS toomount hello yeni paylaşımlar yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="230da-473">Restart autofs toomount hello new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="230da-474">TAKAS dosyasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="230da-474">Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="230da-475">Merhaba Aracısı tooactivate hello değişiklik yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="230da-475">Restart hello Agent tooactivate hello change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. <span data-ttu-id="230da-476">SAP NetWeaver uygulama sunucusu yükleme</span><span class="sxs-lookup"><span data-stu-id="230da-476">Install SAP NetWeaver application server</span></span>

   <span data-ttu-id="230da-477">Bir birincil ya da ek SAP NetWeaver uygulamalar sunucusu yükleyin.</span><span class="sxs-lookup"><span data-stu-id="230da-477">Install a primary or additional SAP NetWeaver applications server.</span></span>

   <span data-ttu-id="230da-478">Merhaba sapinst parametresi SAPINST_REMOTE_ACCESS_USER tooallow kök olmayan kullanıcı tooconnect toosapinst kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="230da-478">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="230da-479">SAP HANA güvenli depolama güncelleştir</span><span class="sxs-lookup"><span data-stu-id="230da-479">Update SAP HANA secure store</span></span>

   <span data-ttu-id="230da-480">Güncelleştirme hello SAP HANA güvenli toopoint toohello sanal adını hello SAP HANA sistem çoğaltma Kurulum depolar.</span><span class="sxs-lookup"><span data-stu-id="230da-480">Update hello SAP HANA secure store toopoint toohello virtual name of hello SAP HANA System Replication setup.</span></span>
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a><span data-ttu-id="230da-481">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="230da-481">Next steps</span></span>
* <span data-ttu-id="230da-482">[Azure sanal makineleri planlama ve uygulama SAP için][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="230da-482">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="230da-483">[SAP için Azure sanal makineler dağıtımı][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="230da-483">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="230da-484">[SAP için Azure sanal makineleri DBMS dağıtımı][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="230da-484">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="230da-485">tooestablish yüksek kullanılabilirlik ve olağanüstü durum kurtarma SAP HANA planlama (büyük örnekler), azure'da nasıl görürüm toolearn [SAP HANA (büyük örnekler) Azure üzerinde yüksek kullanılabilirlik ve olağanüstü durum kurtarma](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="230da-485">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span>
* <span data-ttu-id="230da-486">tooestablish yüksek kullanılabilirlik ve olağanüstü durum kurtarma SAP HANA planlama Azure vm'lerinde nasıl görürüm toolearn [SAP HANA, yüksek kullanılabilirlik Azure Virtual Machines'de (VM'ler)][sap-hana-ha]</span><span class="sxs-lookup"><span data-stu-id="230da-486">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure VMs, see [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha]</span></span>
