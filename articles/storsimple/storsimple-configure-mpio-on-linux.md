---
title: "StorSimple Linux ana bilgisayarına MPIO yapılandırma | Microsoft Docs"
description: "MPIO CentOS 6.6 çalıştıran bir Linux konağına bağlı StorSimple yapılandırın"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: tysonn
ms.assetid: ca289eed-12b7-4e2e-9117-adf7e2034f2f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: alkohli
ms.openlocfilehash: add539351066f9ff94febeebfd5334773b360e8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a><span data-ttu-id="672cf-103">CentOS çalıştıran bir StorSimple konakta MPIO'yu yapılandırın</span><span class="sxs-lookup"><span data-stu-id="672cf-103">Configure MPIO on a StorSimple host running CentOS</span></span>
<span data-ttu-id="672cf-104">Bu makalede, Centos 6.6 ana bilgisayar sunucusunda çoklu yol oluşturma g/ç (MPIO) yapılandırmak için gereken adımları açıklar.</span><span class="sxs-lookup"><span data-stu-id="672cf-104">This article explains the steps required to configure Multipathing IO (MPIO) on your Centos 6.6 host server.</span></span> <span data-ttu-id="672cf-105">Ana bilgisayar sunucusu Microsoft Azure StorSimple Cihazınızı iSCSI başlatıcıları aracılığıyla yüksek kullanılabilirlik için bağlı.</span><span class="sxs-lookup"><span data-stu-id="672cf-105">The host server is connected to your Microsoft Azure StorSimple device for high availability via iSCSI initiators.</span></span> <span data-ttu-id="672cf-106">Bu, çok yollu aygıtlar ve yalnızca StorSimple birimler için özel kurulum otomatik olarak bulmayı ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="672cf-106">It describes in detail the automatic discovery of multipath devices and the specific setup only for StorSimple volumes.</span></span>

<span data-ttu-id="672cf-107">Bu yordam, StorSimple 8000 serisi cihazlar, tüm modelleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="672cf-107">This procedure is applicable to all the models of StorSimple 8000 series devices.</span></span>

> [!NOTE]
> <span data-ttu-id="672cf-108">Bu yordam, StorSimple sanal cihaz için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="672cf-108">This procedure cannot be used for a StorSimple virtual device.</span></span> <span data-ttu-id="672cf-109">Daha fazla bilgi için sanal cihazınız için ana bilgisayar sunucularının nasıl yapılandırılacağı bakın.</span><span class="sxs-lookup"><span data-stu-id="672cf-109">For more information, see how to configure host servers for your virtual device.</span></span>
> 
> 

## <a name="about-multipathing"></a><span data-ttu-id="672cf-110">Çoklu yol oluşturma hakkında</span><span class="sxs-lookup"><span data-stu-id="672cf-110">About multipathing</span></span>
<span data-ttu-id="672cf-111">Çoklu yol oluşturma özelliği, bir konak sunucusu ile bir depolama aygıtı arasında birden çok g/ç yollar yapılandırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="672cf-111">The multipathing feature allows you to configure multiple I/O paths between a host server and a storage device.</span></span> <span data-ttu-id="672cf-112">Bu g/ç yolları ayrı kablo, anahtarlar, ağ arabirimleri ve denetleyicileri dahil edebileceğiniz fiziksel SAN bağlantılardır.</span><span class="sxs-lookup"><span data-stu-id="672cf-112">These I/O paths are physical SAN connections that can include separate cables, switches, network interfaces, and controllers.</span></span> <span data-ttu-id="672cf-113">Çoklu yol oluşturma tüm toplanan yollar ile ilişkili yeni bir cihaz yapılandırmak için g/ç yolu toplar.</span><span class="sxs-lookup"><span data-stu-id="672cf-113">Multipathing aggregates the I/O paths, to configure a new device that is associated with all of the aggregated paths.</span></span>

<span data-ttu-id="672cf-114">Çoklu yol oluşturma amacı iki Katlama şöyledir:</span><span class="sxs-lookup"><span data-stu-id="672cf-114">The purpose of multipathing is two-fold:</span></span>

* <span data-ttu-id="672cf-115">**Yüksek kullanılabilirlik**: (örneğin, bir kablo, anahtar, ağ arabirimi veya denetleyicisi) g/ç yolunun herhangi bir öğeyi başarısız olursa alternatif bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="672cf-115">**High availability**: It provides an alternate path if any element of the I/O path (such as a cable, switch, network interface, or controller) fails.</span></span>
* <span data-ttu-id="672cf-116">**Yük Dengeleme**: depolama Cihazınızı yapılandırmasına bağlı olarak, g/ç yolu yükleri algılama ve dinamik olarak bu yükleri dengelenmesi performansı artırabilir.</span><span class="sxs-lookup"><span data-stu-id="672cf-116">**Load balancing**: Depending on the configuration of your storage device, it can improve the performance by detecting loads on the I/O paths and dynamically rebalancing those loads.</span></span>

### <a name="about-multipathing-components"></a><span data-ttu-id="672cf-117">Çoklu yol oluşturma bileşenleri hakkında</span><span class="sxs-lookup"><span data-stu-id="672cf-117">About multipathing components</span></span>
<span data-ttu-id="672cf-118">Çoklu yol oluşturma Linux içindeki çekirdek bileşenleri ve aşağıdaki tabloda gibi kullanıcı alanı bileşenleri oluşur.</span><span class="sxs-lookup"><span data-stu-id="672cf-118">Multipathing in Linux consists of kernel components and user-space components as tabulated below.</span></span>

* <span data-ttu-id="672cf-119">**Çekirdek**: ana bileşeni *aygıt Eşleyici* g/ç yeniden yönlendirmeler ve yolları ve yol grupları için yük devretmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="672cf-119">**Kernel**: The main component is the *device-mapper* that reroutes I/O and supports failover for paths and path groups.</span></span>

* <span data-ttu-id="672cf-120">**Kullanıcı alanı**: Bunlar *çok yollu Araçları* , multipathed cihazları yönetme aygıt Eşleyici çok yollu modülü yönlendirerek yapmanız gerekenler.</span><span class="sxs-lookup"><span data-stu-id="672cf-120">**User-space**: These are *multipath-tools* that manage multipathed devices by instructing the device-mapper multipath module what to do.</span></span> <span data-ttu-id="672cf-121">Araçları şunlardan oluşur:</span><span class="sxs-lookup"><span data-stu-id="672cf-121">The tools consist of:</span></span>
   
   * <span data-ttu-id="672cf-122">**Çok yollu**: listeler ve multipathed cihazları yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="672cf-122">**Multipath**: lists and configures multipathed devices.</span></span>
   * <span data-ttu-id="672cf-123">**Multipathd**: çok yollu yürütür ve yolları izler arka plan programı.</span><span class="sxs-lookup"><span data-stu-id="672cf-123">**Multipathd**: daemon that executes multipath and monitors the paths.</span></span>
   * <span data-ttu-id="672cf-124">**Devmap adı**: devmaps için udev için anlamlı bir aygıt adı sağlar.</span><span class="sxs-lookup"><span data-stu-id="672cf-124">**Devmap-name**: provides a meaningful device-name to udev for devmaps.</span></span>
   * <span data-ttu-id="672cf-125">**Kpartx**: Doğrusal devmaps çok yollu eşlemeleri bölümlenebilir olmak için aygıt bölümlere eşler.</span><span class="sxs-lookup"><span data-stu-id="672cf-125">**Kpartx**: maps linear devmaps to device partitions to make multipath maps partitionable.</span></span>
   * <span data-ttu-id="672cf-126">**MultiPath.conf**: yerleşik yapılandırma tablosunun üzerine yazmak için kullanılan çok yollu arka plan programı için yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="672cf-126">**Multipath.conf**: configuration file for multipath daemon that is used to overwrite the built-in configuration table.</span></span>

### <a name="about-the-multipathconf-configuration-file"></a><span data-ttu-id="672cf-127">Multipath.conf yapılandırma dosyası hakkında</span><span class="sxs-lookup"><span data-stu-id="672cf-127">About the multipath.conf configuration file</span></span>
<span data-ttu-id="672cf-128">Yapılandırma dosyası `/etc/multipath.conf` çoklu yol oluşturma özelliklerinin çoğu kullanıcı tarafından yapılandırılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="672cf-128">The configuration file `/etc/multipath.conf` makes many of the multipathing features user-configurable.</span></span> <span data-ttu-id="672cf-129">`multipath` Komut ve çekirdek arka plan programı `multipathd` bu dosyada bulunan bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="672cf-129">The `multipath` command and the kernel daemon `multipathd` use information found in this file.</span></span> <span data-ttu-id="672cf-130">Dosya, yalnızca çok yollu aygıtları yapılandırma sırasında alınmadığında.</span><span class="sxs-lookup"><span data-stu-id="672cf-130">The file is consulted only during the configuration of the multipath devices.</span></span> <span data-ttu-id="672cf-131">Çalıştırmadan önce tüm değişiklikleri yapıldığından emin olun `multipath` komutu.</span><span class="sxs-lookup"><span data-stu-id="672cf-131">Make sure that all changes are made before you run the `multipath` command.</span></span> <span data-ttu-id="672cf-132">Dosyayı daha sonra değiştirirseniz, durdurma ve multipathd için değişikliklerin etkili olması için yeniden başlatma gerekir.</span><span class="sxs-lookup"><span data-stu-id="672cf-132">If you modify the file afterwards, you will need to stop and start multipathd again for the changes to take effect.</span></span>

<span data-ttu-id="672cf-133">Multipath.conf beş bölümü vardır:</span><span class="sxs-lookup"><span data-stu-id="672cf-133">The multipath.conf has five sections:</span></span>

- <span data-ttu-id="672cf-134">**Sistem düzeyinde varsayılanlarını** *(varsayılan)*: sistem düzeyinde varsayılanlarını geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="672cf-134">**System level defaults** *(defaults)*: You can override system level defaults.</span></span>
- <span data-ttu-id="672cf-135">**Kara listede aygıtları** *(kara liste)*: cihaz Eşleyicisi tarafından denetlenmeyen cihazların listesini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="672cf-135">**Blacklisted devices** *(blacklist)*: You can specify the list of devices that should not be controlled by device-mapper.</span></span>
- <span data-ttu-id="672cf-136">**Özel durumlar kara listeye** *(blacklist_exceptions)*: kara listeye listelenen olsa bile çok yollu cihaz olarak kabul edilmesi için belirli cihazlar tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="672cf-136">**Blacklist exceptions** *(blacklist_exceptions)*: You can identify specific devices to be treated as multipath devices even if listed in the blacklist.</span></span>
- <span data-ttu-id="672cf-137">**Depolama denetleyicisi belirli ayarları** *(aygıtlar)*: Satıcı ve ürün bilgileri bulunduğu cihazlara uygulanacak olan yapılandırma ayarları belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="672cf-137">**Storage controller specific settings** *(devices)*: You can specify configuration settings that will be applied to devices that have Vendor and Product information.</span></span>
- <span data-ttu-id="672cf-138">**Aygıt belirli ayarları** *(multipaths)*: tek tek LUN'ları için yapılandırma ayarlarını ince ayar yapmak için bu bölümü kullanın.</span><span class="sxs-lookup"><span data-stu-id="672cf-138">**Device specific settings** *(multipaths)*: You can use this section to fine-tune the configuration settings for individual LUNs.</span></span>

## <a name="configure-multipathing-on-storsimple-connected-to-linux-host"></a><span data-ttu-id="672cf-139">Çoklu yol oluşturma Linux konağına bağlı StorSimple yapılandırın</span><span class="sxs-lookup"><span data-stu-id="672cf-139">Configure multipathing on StorSimple connected to Linux host</span></span>
<span data-ttu-id="672cf-140">Bir Linux konağına bağlı bir StorSimple cihazı, yüksek kullanılabilirlik ve Yük Dengeleme için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="672cf-140">A StorSimple device connected to a Linux host can be configured for high availability and load balancing.</span></span> <span data-ttu-id="672cf-141">Örneğin, iki arabirim SAN'a bağlı Linux ana bilgisayar varsa ve bu arabirimleri aynı alt ağda gibi olduğuna göre SAN'a bağlı iki arabirim aygıtın, ardından olacaktır 4 yolları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="672cf-141">For example, if the Linux host has two interfaces connected to the SAN and the device has two interfaces connected to the SAN such that these interfaces are on the same subnet, then there will be 4 paths available.</span></span> <span data-ttu-id="672cf-142">Her veri arabirimi cihaz ve ana bilgisayar arabirimde farklı bir IP alt ağ (ve değil yönlendirilebilir) varsa, ancak sonra yalnızca 2 yolları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="672cf-142">However, if each DATA interface on the device and host interface are on a different IP subnet (and not routable), then only 2 paths will be available.</span></span> <span data-ttu-id="672cf-143">Çoklu yol oluşturma otomatik olarak kullanılabilen tüm yolları Bul, bu yollar için bir Yük Dengeleme algoritması seçin, yalnızca StorSimple birimler için belirli yapılandırma ayarları uygulamak ve sonra etkinleştirin ve çoklu yol oluşturma doğrulayın yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="672cf-143">You can configure multipathing to automatically discover all the available paths, choose a load-balancing algorithm for those paths, apply specific configuration settings for StorSimple-only volumes, and then enable and verify multipathing.</span></span>

<span data-ttu-id="672cf-144">Aşağıdaki yordamda, iki ağ arabirimine sahip bir konağa iki ağ arabirimi ile bir StorSimple cihazı bağlı olduğunda çoklu yol oluşturma yapılandırmak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="672cf-144">The following procedure describes how to configure multipathing when a StorSimple device with two network interfaces is connected to a host with two network interfaces.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="672cf-145">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="672cf-145">Prerequisites</span></span>
<span data-ttu-id="672cf-146">Bu bölümde, CentOS sunucu ve StorSimple cihazınız için yapılandırma önkoşulları ayrıntıları verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="672cf-146">This section details the configuration prerequisites for CentOS server and your StorSimple device.</span></span>

### <a name="on-centos-host"></a><span data-ttu-id="672cf-147">CentOS konakta</span><span class="sxs-lookup"><span data-stu-id="672cf-147">On CentOS host</span></span>
1. <span data-ttu-id="672cf-148">CentOS ana bilgisayar 2 ağ arabirimleri etkin olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="672cf-148">Make sure that your CentOS host has 2 network interfaces enabled.</span></span> <span data-ttu-id="672cf-149">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="672cf-149">Type:</span></span>
   
    `ifconfig`
   
    <span data-ttu-id="672cf-150">İki ağ arabirimleri, aşağıdaki örnek çıkış şunları gösterir (`eth0` ve `eth1`) konakta yok.</span><span class="sxs-lookup"><span data-stu-id="672cf-150">The following example shows the output when two network interfaces (`eth0` and `eth1`) are present on the host.</span></span>
   
        [root@centosSS ~]# ifconfig
        eth0  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:41  
          inet addr:10.126.162.65  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3341/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3341/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
         RX packets:36536 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6312 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:13994127 (13.3 MiB)  TX bytes:645654 (630.5 KiB)
   
        eth1  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:42  
          inet addr:10.126.162.66  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3342/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3342/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25962 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:2597350 (2.4 MiB)  TX bytes:754 (754.0 b)
   
        loLink encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:12 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:720 (720.0 b)  TX bytes:720 (720.0 b)
2. <span data-ttu-id="672cf-151">Yükleme *iSCSI-Başlatıcı-yardımcı programları* CentOS sunucunuzda.</span><span class="sxs-lookup"><span data-stu-id="672cf-151">Install *iSCSI-initiator-utils* on your CentOS server.</span></span> <span data-ttu-id="672cf-152">Yüklemek için aşağıdaki adımları gerçekleştirin *iSCSI-Başlatıcı-yardımcı programları*.</span><span class="sxs-lookup"><span data-stu-id="672cf-152">Perform the following steps to install *iSCSI-initiator-utils*.</span></span>
   
   1. <span data-ttu-id="672cf-153">Oturum açma `root` CentOS ana bilgisayarınızın INTO.</span><span class="sxs-lookup"><span data-stu-id="672cf-153">Log on as `root` into your CentOS host.</span></span>
   2. <span data-ttu-id="672cf-154">Yükleme *iSCSI-Başlatıcı-yardımcı programları*.</span><span class="sxs-lookup"><span data-stu-id="672cf-154">Install the *iSCSI-initiator-utils*.</span></span> <span data-ttu-id="672cf-155">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="672cf-155">Type:</span></span>
      
       `yum install iscsi-initiator-utils`
   3. <span data-ttu-id="672cf-156">Sonra *iSCSI-Başlatıcı-yardımcı programları* başarıyla yüklendiyse, iSCSI hizmetini başlatın.</span><span class="sxs-lookup"><span data-stu-id="672cf-156">After the *iSCSI-Initiator-utils* is successfully installed, start the iSCSI service.</span></span> <span data-ttu-id="672cf-157">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="672cf-157">Type:</span></span>
      
       `service iscsid start`
      
       <span data-ttu-id="672cf-158">Olaylar üzerinde `iscsid` gerçekten başlatılamayabilir ve `--force` seçeneği gerekebilir</span><span class="sxs-lookup"><span data-stu-id="672cf-158">On occasions, `iscsid` may not actually start and the `--force` option may be needed</span></span>
   4. <span data-ttu-id="672cf-159">İSCSI başlatıcısı önyükleme süresince etkinleştirildiğinden emin olmak için kullanmak `chkconfig` hizmeti etkinleştirmek için komutu.</span><span class="sxs-lookup"><span data-stu-id="672cf-159">To ensure that your iSCSI initiator is enabled during boot time, use the `chkconfig` command to enable the service.</span></span>
      
       `chkconfig iscsi on`
   5. <span data-ttu-id="672cf-160">Oluştu, düzgün şekilde Kur'un doğrulamak için komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="672cf-160">To verify that that it was properly setup, run the command:</span></span>
      
       `chkconfig --list | grep iscsi`
      
       <span data-ttu-id="672cf-161">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="672cf-161">A sample output is shown below.</span></span>
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       <span data-ttu-id="672cf-162">Yukarıdaki örnekte, iSCSI ortamınızı önyükleme zamanında çalışma Düzey 2, 3, 4 ve 5 çalışacağını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="672cf-162">From the above example, you can see that your iSCSI environment will run on boot time on run levels 2, 3, 4, and 5.</span></span>
3. <span data-ttu-id="672cf-163">Yükleme *aygıt-Eşleyici-çok yollu*.</span><span class="sxs-lookup"><span data-stu-id="672cf-163">Install *device-mapper-multipath*.</span></span> <span data-ttu-id="672cf-164">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="672cf-164">Type:</span></span>
   
    `yum install device-mapper-multipath`
   
    <span data-ttu-id="672cf-165">Yükleme başlar.</span><span class="sxs-lookup"><span data-stu-id="672cf-165">The installation will start.</span></span> <span data-ttu-id="672cf-166">Tür **Y** onaylamanız istendiğinde devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="672cf-166">Type **Y** to continue when prompted for confirmation.</span></span>

### <a name="on-storsimple-device"></a><span data-ttu-id="672cf-167">StorSimple cihazında</span><span class="sxs-lookup"><span data-stu-id="672cf-167">On StorSimple device</span></span>
<span data-ttu-id="672cf-168">StorSimple Cihazınızı olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="672cf-168">Your StorSimple device should have:</span></span>

* <span data-ttu-id="672cf-169">İSCSI için iki arabirimin en az.</span><span class="sxs-lookup"><span data-stu-id="672cf-169">A minimum of two interfaces enabled for iSCSI.</span></span> <span data-ttu-id="672cf-170">İki arabirim StorSimple Cihazınızda iSCSI etkin olduğunu doğrulamak için StorSimple cihazınız için Azure Klasik portalında aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="672cf-170">To verify that two interfaces are iSCSI-enabled on your StorSimple device, perform the following steps in the Azure classic portal for your StorSimple device:</span></span>
  
  1. <span data-ttu-id="672cf-171">StorSimple cihazınız için Klasik portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="672cf-171">Log into the classic portal for your StorSimple device.</span></span>
  2. <span data-ttu-id="672cf-172">StorSimple Yöneticisi hizmetiniz seçin, **aygıtları** ve belirli StorSimple cihazı seçin.</span><span class="sxs-lookup"><span data-stu-id="672cf-172">Select your StorSimple Manager service, click **Devices** and choose the specific StorSimple device.</span></span> <span data-ttu-id="672cf-173">Tıklatın **yapılandırma** ve ağ arabirimi ayarlarını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="672cf-173">Click **Configure** and verify the network interface settings.</span></span> <span data-ttu-id="672cf-174">İki iSCSI etkin ağ arabirimlerine sahip bir ekran görüntüsü aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="672cf-174">A screenshot with two iSCSI-enabled network interfaces is shown below.</span></span> <span data-ttu-id="672cf-175">Burada veri 2 ve veri 3, her iki 10 GbE arabirimleri iSCSI için etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="672cf-175">Here DATA 2 and DATA 3, both 10 GbE interfaces are enabled for iSCSI.</span></span>
     
      ![MPIO StorsSimple veri 2 yapılandırma](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![MPIO StorSimple veri 3 yapılandırma](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      <span data-ttu-id="672cf-178">İçinde **yapılandırma** sayfası</span><span class="sxs-lookup"><span data-stu-id="672cf-178">In the **Configure** page</span></span>
     
     1. <span data-ttu-id="672cf-179">Her iki ağ arabirimleri iSCSI etkin olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="672cf-179">Ensure that both network interfaces are iSCSI-enabled.</span></span> <span data-ttu-id="672cf-180">**İSCSI etkin** alan ayarlanmalıdır **Evet**.</span><span class="sxs-lookup"><span data-stu-id="672cf-180">The **iSCSI enabled** field should be set to **Yes**.</span></span>
     2. <span data-ttu-id="672cf-181">Ağ arabirimleri aynı hızınız, ikisi de 1 GbE veya 10 GbE olmalıdır emin olun.</span><span class="sxs-lookup"><span data-stu-id="672cf-181">Ensure that the network interfaces have the same speed, both should be 1 GbE or 10 GbE.</span></span>
     3. <span data-ttu-id="672cf-182">İSCSI etkin arabirimlerin IPv4 adreslerini not alın ve ana bilgisayarda daha sonra kullanmak için kaydedin.</span><span class="sxs-lookup"><span data-stu-id="672cf-182">Note the IPv4 addresses of the iSCSI-enabled interfaces and save for later use on the host.</span></span>
* <span data-ttu-id="672cf-183">StorSimple Cihazınızı iSCSI arabirimlerde CentOS sunucudan erişilebilir olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="672cf-183">The iSCSI interfaces on your StorSimple device should be reachable from the CentOS server.</span></span>
      <span data-ttu-id="672cf-184">Bunu doğrulamak için StorSimple iSCSI etkin ağ arabirimlerinin IP adresleri, ana bilgisayar sunucusunda sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="672cf-184">To verify this, you need to provide the IP addresses of your StorSimple iSCSI-enabled network interfaces on your host server.</span></span> <span data-ttu-id="672cf-185">Kullanılan komutlar ve karşılık gelen çıktı veri2 ile (10.126.162.25) ve DATA3 (10.126.162.26) aşağıda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="672cf-185">The commands used and the corresponding output with DATA2 (10.126.162.25) and DATA3 (10.126.162.26) is shown below:</span></span>
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a><span data-ttu-id="672cf-186">Donanım yapılandırması</span><span class="sxs-lookup"><span data-stu-id="672cf-186">Hardware configuration</span></span>
<span data-ttu-id="672cf-187">Artıklık için ayrı yollar iki iSCSI ağ arabirimlerindeki bağlanmasını öneririz.</span><span class="sxs-lookup"><span data-stu-id="672cf-187">We recommend that you connect the two iSCSI network interfaces on separate paths for redundancy.</span></span> <span data-ttu-id="672cf-188">Aşağıdaki şekilde, yüksek kullanılabilirlik için önerilen donanım yapılandırması ve CentOS sunucunuz ve StorSimple cihazı için çoklu yol oluşturma Yük Dengeleme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="672cf-188">The figure below shows the recommended hardware configuration for high availability and load-balancing multipathing for your CentOS server and StorSimple device.</span></span>

![Linux ana bilgisayara StorSimple için MPIO donanım yapılandırması](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

<span data-ttu-id="672cf-190">Yukarıdaki şekilde gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="672cf-190">As shown in the preceding figure:</span></span>

* <span data-ttu-id="672cf-191">StorSimple Cihazınızı iki denetleyicileri Aktif-Pasif yapılandırmayla kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="672cf-191">Your StorSimple device is in an active-passive configuration with two controllers.</span></span>
* <span data-ttu-id="672cf-192">İki SAN anahtarları aygıt denetleyicilerinizi bağlanır.</span><span class="sxs-lookup"><span data-stu-id="672cf-192">Two SAN switches are connected to your device controllers.</span></span>
* <span data-ttu-id="672cf-193">StorSimple Cihazınızda iki iSCSI başlatıcıları etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="672cf-193">Two iSCSI initiators are enabled on your StorSimple device.</span></span>
* <span data-ttu-id="672cf-194">İki ağ arabirimi, CentOS ana bilgisayarda etkin.</span><span class="sxs-lookup"><span data-stu-id="672cf-194">Two network interfaces are enabled on your CentOS host.</span></span>

<span data-ttu-id="672cf-195">Ana bilgisayar ve veri arabirimleri yönlendirilebilir olması durumunda Yukarıdaki yapılandırma Cihazınızı ve ana bilgisayar arasında 4 ayrı yollar sunacak.</span><span class="sxs-lookup"><span data-stu-id="672cf-195">The above configuration will yield 4 separate paths between your device and the host if the host and data interfaces are routable.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="672cf-196">1 GbE ve çoklu yol oluşturma için 10 GbE ağ arabirimleri karıştırmamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="672cf-196">We recommend that you do not mix 1 GbE and 10 GbE network interfaces for multipathing.</span></span> <span data-ttu-id="672cf-197">İki ağ arabirimleri kullanılırken, her iki arabirimde aynı türde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="672cf-197">When using two network interfaces, both the interfaces should be the identical type.</span></span>
> * <span data-ttu-id="672cf-198">Veri2 ve DATA3 10 GbE ağ arabirimleri ise, StorSimple Cihazınızda DATA0, Veri1, DATA4 ve DATA5 1 GbE arabirimlerdir. |</span><span class="sxs-lookup"><span data-stu-id="672cf-198">On your StorSimple device, DATA0, DATA1, DATA4 and DATA5 are 1 GbE interfaces whereas DATA2 and DATA3 are 10 GbE network interfaces.|</span></span>
> 
> 

## <a name="configuration-steps"></a><span data-ttu-id="672cf-199">Yapılandırma adımları</span><span class="sxs-lookup"><span data-stu-id="672cf-199">Configuration steps</span></span>
<span data-ttu-id="672cf-200">Yapılandırma adımları çoklu yol oluşturma için çoklu yol oluşturma etkinleştirme ve son olarak yapılandırmasını doğrulama kullanmak için Yük Dengeleme algoritması belirtme, otomatik bulma için mevcut yolları yapılandırmayı içerir.</span><span class="sxs-lookup"><span data-stu-id="672cf-200">The configuration steps for multipathing involve configuring the available paths for automatic discovery, specifying the load-balancing algorithm to use, enabling multipathing and finally verifying the configuration.</span></span> <span data-ttu-id="672cf-201">Bu adımların her biri aşağıdaki bölümlerde ayrıntılı olarak ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="672cf-201">Each of these steps is discussed in detail in the following sections.</span></span>

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a><span data-ttu-id="672cf-202">1. adım: çoklu yol oluşturma otomatik bulma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="672cf-202">Step 1: Configure multipathing for automatic discovery</span></span>
<span data-ttu-id="672cf-203">Çok yollu desteklenen cihazları otomatik olarak bulunan ve yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="672cf-203">The multipath-supported devices can be automatically discovered and configured.</span></span>

1. <span data-ttu-id="672cf-204">Initialize `/etc/multipath.conf` dosya.</span><span class="sxs-lookup"><span data-stu-id="672cf-204">Initialize `/etc/multipath.conf` file.</span></span> <span data-ttu-id="672cf-205">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="672cf-205">Type:</span></span>
   
     `mpathconf --enable`
   
    <span data-ttu-id="672cf-206">Yukarıdaki komut oluşturacak bir `sample/etc/multipath.conf` dosyası.</span><span class="sxs-lookup"><span data-stu-id="672cf-206">The above command will create a `sample/etc/multipath.conf` file.</span></span>
2. <span data-ttu-id="672cf-207">Çok yollu hizmetini başlatın.</span><span class="sxs-lookup"><span data-stu-id="672cf-207">Start multipath service.</span></span> <span data-ttu-id="672cf-208">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="672cf-208">Type:</span></span>
   
    `service multipathd start`
   
    <span data-ttu-id="672cf-209">Şu çıktı görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="672cf-209">You will see the following output:</span></span>
   
    `Starting multipathd daemon:`
3. <span data-ttu-id="672cf-210">Multipaths otomatik olarak bulmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="672cf-210">Enable automatic discovery of multipaths.</span></span> <span data-ttu-id="672cf-211">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="672cf-211">Type:</span></span>
   
    `mpathconf --find_multipaths y`
   
    <span data-ttu-id="672cf-212">Bu varsayılan bölümünü değiştirmek, `multipath.conf` aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="672cf-212">This will modify the defaults section of your `multipath.conf` as shown below:</span></span>
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a><span data-ttu-id="672cf-213">2. adım: StorSimple birimler için çoklu yol oluşturmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="672cf-213">Step 2: Configure multipathing for StorSimple volumes</span></span>
<span data-ttu-id="672cf-214">Varsayılan olarak, tüm cihazlar multipath.conf dosyasında listelenen siyah ve atlanır.</span><span class="sxs-lookup"><span data-stu-id="672cf-214">By default, all devices are black listed in the multipath.conf file and will be bypassed.</span></span> <span data-ttu-id="672cf-215">Çoklu yol oluşturma StorSimple cihazları birimlerin izin veren kara liste özel durumlar oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="672cf-215">You will need to create blacklist exceptions to allow multipathing for volumes from StorSimple devices.</span></span>

1. <span data-ttu-id="672cf-216">Düzen `/etc/mulitpath.conf` dosya.</span><span class="sxs-lookup"><span data-stu-id="672cf-216">Edit the `/etc/mulitpath.conf` file.</span></span> <span data-ttu-id="672cf-217">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="672cf-217">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="672cf-218">Blacklist_exceptions bölüm multipath.conf dosyasında bulun.</span><span class="sxs-lookup"><span data-stu-id="672cf-218">Locate the blacklist_exceptions section in the multipath.conf file.</span></span> <span data-ttu-id="672cf-219">StorSimple Cihazınızı Bu bölümde bir kara liste özel olarak listelenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="672cf-219">Your StorSimple device needs to be listed as a blacklist exception in this section.</span></span> <span data-ttu-id="672cf-220">Bu dosyadaki (kullanın, kullanmakta olduğunuz cihaz yalnızca belirli modelinin) aşağıda gösterildiği gibi değiştirmek için ilgili satırlara açıklamadan çıkarın:</span><span class="sxs-lookup"><span data-stu-id="672cf-220">You can uncomment relevant lines in this file to modify it as shown below (use only the specific model of the device you are using):</span></span>
   
        blacklist_exceptions {
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8100*"
            }
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8600*"
            }
           }

### <a name="step-3-configure-round-robin-multipathing"></a><span data-ttu-id="672cf-221">3. adım: hepsini çoklu yol oluşturmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="672cf-221">Step 3: Configure round-robin multipathing</span></span>
<span data-ttu-id="672cf-222">Bu Yük Dengeleme algoritması etkin denetleyiciye tüm kullanılabilir multipaths Dengeli, hepsini bir biçimde kullanır.</span><span class="sxs-lookup"><span data-stu-id="672cf-222">This load-balancing algorithm uses all the available multipaths to the active controller in a balanced, round-robin fashion.</span></span>

1. <span data-ttu-id="672cf-223">Düzen `/etc/multipath.conf` dosya.</span><span class="sxs-lookup"><span data-stu-id="672cf-223">Edit the `/etc/multipath.conf` file.</span></span> <span data-ttu-id="672cf-224">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="672cf-224">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="672cf-225">Altında `defaults` bölümünde, `path_grouping_policy` için `multibus`.</span><span class="sxs-lookup"><span data-stu-id="672cf-225">Under the `defaults` section, set the `path_grouping_policy` to `multibus`.</span></span> <span data-ttu-id="672cf-226">`path_grouping_policy` Belirtilmeyen multipaths uygulamak için ilke gruplandırma varsayılan yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="672cf-226">The `path_grouping_policy` specifies the default path grouping policy to apply to unspecified multipaths.</span></span> <span data-ttu-id="672cf-227">Varsayılanları bölümü, aşağıda gösterildiği gibi görünecektir.</span><span class="sxs-lookup"><span data-stu-id="672cf-227">The defaults section will look as shown below.</span></span>
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> <span data-ttu-id="672cf-228">En yaygın değerlerini `path_grouping_policy` içerir:</span><span class="sxs-lookup"><span data-stu-id="672cf-228">The most common values of `path_grouping_policy` include:</span></span>
> 
> * <span data-ttu-id="672cf-229">Yük devretme öncelik grubu başına 1 yolu =</span><span class="sxs-lookup"><span data-stu-id="672cf-229">failover = 1 path per priority group</span></span>
> * <span data-ttu-id="672cf-230">multibus 1 önceliği grubundaki tüm geçerli yolu =</span><span class="sxs-lookup"><span data-stu-id="672cf-230">multibus = all valid paths in 1 priority group</span></span>
> 
> 

### <a name="step-4-enable-multipathing"></a><span data-ttu-id="672cf-231">4. adım: Etkinleştirme çoklu yol oluşturma</span><span class="sxs-lookup"><span data-stu-id="672cf-231">Step 4: Enable multipathing</span></span>
1. <span data-ttu-id="672cf-232">Yeniden `multipathd` arka plan programı.</span><span class="sxs-lookup"><span data-stu-id="672cf-232">Restart the `multipathd` daemon.</span></span> <span data-ttu-id="672cf-233">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="672cf-233">Type:</span></span>
   
    `service multipathd restart`
2. <span data-ttu-id="672cf-234">Çıktı aşağıda gösterildiği gibi olacaktır:</span><span class="sxs-lookup"><span data-stu-id="672cf-234">The output will be as shown below:</span></span>
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a><span data-ttu-id="672cf-235">5. adım: çoklu yol oluşturma doğrulayın</span><span class="sxs-lookup"><span data-stu-id="672cf-235">Step 5: Verify multipathing</span></span>
1. <span data-ttu-id="672cf-236">Önce iSCSI bağlantı StorSimple cihazı gibi kurulduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="672cf-236">First make sure that iSCSI connection is established with the StorSimple device as follows:</span></span>
   
   <span data-ttu-id="672cf-237">a.</span><span class="sxs-lookup"><span data-stu-id="672cf-237">a.</span></span> <span data-ttu-id="672cf-238">StorSimple Cihazınızı bulur.</span><span class="sxs-lookup"><span data-stu-id="672cf-238">Discover your StorSimple device.</span></span> <span data-ttu-id="672cf-239">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="672cf-239">Type:</span></span>
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on the device>:<iSCSI port on StorSimple device>
    ```
    
    <span data-ttu-id="672cf-240">Aşağıda gösterildiği gibi 10.126.162.25 DATA0 için IP adresi olduğundan ve bağlantı noktası 3260 giden iSCSI trafiği için StorSimple cihazında açıldığında çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="672cf-240">The output when IP address for DATA0 is 10.126.162.25 and port 3260 is opened on the StorSimple device for outbound iSCSI traffic is as shown below:</span></span>
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    <span data-ttu-id="672cf-241">StorSimple Cihazınızı IQN kopyalama `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, önceki çıktısından.</span><span class="sxs-lookup"><span data-stu-id="672cf-241">Copy the IQN of your StorSimple device, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, from the preceding output.</span></span>

   <span data-ttu-id="672cf-242">b.</span><span class="sxs-lookup"><span data-stu-id="672cf-242">b.</span></span> <span data-ttu-id="672cf-243">Aygıtına hedef IQN kullanarak bağlanın.</span><span class="sxs-lookup"><span data-stu-id="672cf-243">Connect to the device using target IQN.</span></span> <span data-ttu-id="672cf-244">StorSimple cihazı iSCSI burada hedefidir.</span><span class="sxs-lookup"><span data-stu-id="672cf-244">The StorSimple device is the iSCSI target here.</span></span> <span data-ttu-id="672cf-245">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="672cf-245">Type:</span></span>

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    <span data-ttu-id="672cf-246">Aşağıdaki örnek çıkış hedefiyle IQN gösterir, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span><span class="sxs-lookup"><span data-stu-id="672cf-246">The following example shows output with a target IQN of `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span></span> <span data-ttu-id="672cf-247">Çıktı Cihazınızda iki iSCSI etkin ağ arabirimi başarıyla bağlandıysanız gösterir.</span><span class="sxs-lookup"><span data-stu-id="672cf-247">The output indicates that you have successfully connected to the two iSCSI-enabled network interfaces on your device.</span></span>

    ```
    Logging in to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    <span data-ttu-id="672cf-248">Yalnızca bir ana bilgisayar arabirimi ve iki yollarını burada görürseniz, arabirimler konakta iSCSI için etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="672cf-248">If you see only one host interface and two paths here, then you need to enable both the interfaces on host for iSCSI.</span></span> <span data-ttu-id="672cf-249">İzleyebileceğiniz [ayrıntılı Linux belgelerindeki yönergeleri](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span><span class="sxs-lookup"><span data-stu-id="672cf-249">You can follow the [detailed instructions in Linux documentation](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span></span>

2. <span data-ttu-id="672cf-250">Bir birim StorSimple cihazı CentOS sunucuya açıktır.</span><span class="sxs-lookup"><span data-stu-id="672cf-250">A volume is exposed to the CentOS server from the StorSimple device.</span></span> <span data-ttu-id="672cf-251">Daha fazla bilgi için bkz: [6. adım: birim oluşturma](storsimple-deployment-walkthrough.md#step-6-create-a-volume) , StorSimple Cihazınızda Klasik Azure Portalı aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="672cf-251">For more information, see [Step 6: Create a volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via the Azure classic portal on your StorSimple device.</span></span>

3. <span data-ttu-id="672cf-252">Kullanılabilir yollar doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="672cf-252">Verify the available paths.</span></span> <span data-ttu-id="672cf-253">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="672cf-253">Type:</span></span>

      ```
      multipath –l
      ```

      <span data-ttu-id="672cf-254">Aşağıdaki örnek çıkış iki ağ arabirimi için iki kullanılabilir yola sahip bir tek ana bilgisayar ağ arabirimi için bağlı bir StorSimple cihazına gösterir.</span><span class="sxs-lookup"><span data-stu-id="672cf-254">The following example shows the output for two network interfaces on a StorSimple device connected to a single host network interface with two available paths.</span></span>

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        The following example shows the output for two network interfaces on a StorSimple device connected to two host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After the paths are configured, refer to the specific instructions on your host operating system (Centos 6.6) to mount and format this volume.

## <a name="troubleshoot-multipathing"></a><span data-ttu-id="672cf-255">Çoklu yol oluşturma sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="672cf-255">Troubleshoot multipathing</span></span>
<span data-ttu-id="672cf-256">Çoklu yol oluşturma yapılandırması sırasında herhangi bir sorunla çalıştırırsanız, bu bölümde bazı yararlı ipuçları sağlanır.</span><span class="sxs-lookup"><span data-stu-id="672cf-256">This section provides some helpful tips if you run into any issues during multipathing configuration.</span></span>

<span data-ttu-id="672cf-257">Q.</span><span class="sxs-lookup"><span data-stu-id="672cf-257">Q.</span></span> <span data-ttu-id="672cf-258">Değişiklikleri görüntülenmemesini `multipath.conf` etkisi alma dosyası.</span><span class="sxs-lookup"><span data-stu-id="672cf-258">I do not see the changes in `multipath.conf` file taking effect.</span></span>

<span data-ttu-id="672cf-259">A.</span><span class="sxs-lookup"><span data-stu-id="672cf-259">A.</span></span> <span data-ttu-id="672cf-260">Herhangi bir değişiklik yaptıysanız `multipath.conf` dosya, çoklu yol oluşturma hizmeti yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="672cf-260">If you have made any changes to the `multipath.conf` file, you will need to restart the multipathing service.</span></span> <span data-ttu-id="672cf-261">Aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="672cf-261">Type the following command:</span></span>

    service multipathd restart

<span data-ttu-id="672cf-262">Q.</span><span class="sxs-lookup"><span data-stu-id="672cf-262">Q.</span></span> <span data-ttu-id="672cf-263">StorSimple cihazında iki ağ arabirimi ve ana bilgisayarda iki ağ arabirimi etkin.</span><span class="sxs-lookup"><span data-stu-id="672cf-263">I have enabled two network interfaces on the StorSimple device and two network interfaces on the host.</span></span> <span data-ttu-id="672cf-264">Kullanılabilir yollar listelediğinizde, yalnızca iki yolu bakın.</span><span class="sxs-lookup"><span data-stu-id="672cf-264">When I list the available paths, I see only two paths.</span></span> <span data-ttu-id="672cf-265">Bkz. dört kullanılabilir yolları beklenir.</span><span class="sxs-lookup"><span data-stu-id="672cf-265">I expected to see four available paths.</span></span>

<span data-ttu-id="672cf-266">A.</span><span class="sxs-lookup"><span data-stu-id="672cf-266">A.</span></span> <span data-ttu-id="672cf-267">Yönlendirilebilir ve iki yolu aynı alt ağda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="672cf-267">Make sure that the two paths are on the same subnet and routable.</span></span> <span data-ttu-id="672cf-268">Ağ arabirimleri farklı VLAN'ları ve değil yönlendirilebilir varsa, yalnızca iki yolu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="672cf-268">If the network interfaces are on different vLANs and not routable, you will see only two paths.</span></span> <span data-ttu-id="672cf-269">Bu doğrulamanın bir yolu, her iki ana arabirimlerinden StorSimple cihazında bir ağ arabirimi ulaşabildiğimizden emin olmaktır.</span><span class="sxs-lookup"><span data-stu-id="672cf-269">One way to verify this is to make sure that you can reach both the host interfaces from a network interface on the StorSimple device.</span></span> <span data-ttu-id="672cf-270">Etmeniz [Microsoft Support başvurun](storsimple-contact-microsoft-support.md) gibi bu doğrulama yalnızca bir destek oturumu yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="672cf-270">You will need to [contact Microsoft Support](storsimple-contact-microsoft-support.md) as this verification can only be done via a support session.</span></span>

<span data-ttu-id="672cf-271">Q.</span><span class="sxs-lookup"><span data-stu-id="672cf-271">Q.</span></span> <span data-ttu-id="672cf-272">Kullanılabilir yollar listelediğinizde, herhangi bir çıktı görmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="672cf-272">When I list available paths, I do not see any output.</span></span>

<span data-ttu-id="672cf-273">A.</span><span class="sxs-lookup"><span data-stu-id="672cf-273">A.</span></span> <span data-ttu-id="672cf-274">Genellikle, öneren çoklu yol oluşturma arka plan programı ile ilgili bir sorun multipathed yollar görmesini değil ve bu büyük olasılıkla burada herhangi bir sorun arasındadır olduğunu `multipath.conf` dosya.</span><span class="sxs-lookup"><span data-stu-id="672cf-274">Typically, not seeing any multipathed paths suggests a problem with the multipathing daemon, and it’s most likely that any problem here lies in the `multipath.conf` file.</span></span>

<span data-ttu-id="672cf-275">Ayrıca, çok yollu listelerini yanıt ayrıca herhangi bir diski yok anlamına gelebilir gibi aslında bazı disklerin hedefe bağlandıktan sonra görebileceğini denetleme değer olacaktır.</span><span class="sxs-lookup"><span data-stu-id="672cf-275">It would also be worth checking that you can actually see some disks after connecting to the target, as no response from the multipath listings could also mean you don’t have any disks.</span></span>

* <span data-ttu-id="672cf-276">SCSI veri yolu yeniden taramak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="672cf-276">Use the following command to rescan the SCSI bus:</span></span>
  
    <span data-ttu-id="672cf-277">`$ rescan-scsi-bus.sh `(sg3_utils paketinin bir parçası)</span><span class="sxs-lookup"><span data-stu-id="672cf-277">`$ rescan-scsi-bus.sh `(part of sg3_utils package)</span></span>
* <span data-ttu-id="672cf-278">Aşağıdaki komutları yazın:</span><span class="sxs-lookup"><span data-stu-id="672cf-278">Type the following commands:</span></span>
  
    `$ dmesg | grep sd*`
     
     <span data-ttu-id="672cf-279">Veya</span><span class="sxs-lookup"><span data-stu-id="672cf-279">Or</span></span>
  
    `$ fdisk –l`
  
    <span data-ttu-id="672cf-280">Bu yakın zamanda eklenen diskler ayrıntılarını döndürür.</span><span class="sxs-lookup"><span data-stu-id="672cf-280">These will return details of recently added disks.</span></span>
* <span data-ttu-id="672cf-281">Bir StorSimple disk olup olmadığını belirlemek için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="672cf-281">To determine whether it is a StorSimple disk, use the following commands:</span></span>
  
    `cat /sys/block/<DISK>/device/model`
  
    <span data-ttu-id="672cf-282">Bu, bir StorSimple disk olup olmadığını belirleyen bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="672cf-282">This will return a string, which will determine if it’s a StorSimple disk.</span></span>

<span data-ttu-id="672cf-283">Büyük olasılıkla ancak olası nedeni daha az A eski iscsid da olabilir PID.</span><span class="sxs-lookup"><span data-stu-id="672cf-283">A less likely but possible cause could also be stale iscsid pid.</span></span> <span data-ttu-id="672cf-284">İSCSI oturumlardan oturumunu kapatmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="672cf-284">Use the following command to log off from the iSCSI sessions:</span></span>

    iscsiadm -m node --logout -p <Target_IP>

<span data-ttu-id="672cf-285">StorSimple cihazınız iSCSI hedef tüm bağlı ağ arabirimleri için bu komutu yineleyin.</span><span class="sxs-lookup"><span data-stu-id="672cf-285">Repeat this command for all the connected network interfaces on the iSCSI target, which is your StorSimple device.</span></span> <span data-ttu-id="672cf-286">Tüm iSCSI oturumlardan kapattınız sonra iSCSI oturumu yeniden kurmak için iSCSI hedef IQN kullanın.</span><span class="sxs-lookup"><span data-stu-id="672cf-286">Once you have logged off from all the iSCSI sessions, use the iSCSI target IQN to reestablish the iSCSI session.</span></span> <span data-ttu-id="672cf-287">Aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="672cf-287">Type the following command:</span></span>

    iscsiadm -m node --login -T <TARGET_IQN>


<span data-ttu-id="672cf-288">Q.</span><span class="sxs-lookup"><span data-stu-id="672cf-288">Q.</span></span> <span data-ttu-id="672cf-289">Cihazımı Güvenilenler listesine olup olmadığından emin değilim.</span><span class="sxs-lookup"><span data-stu-id="672cf-289">I am not sure if my device is whitelisted.</span></span>

<span data-ttu-id="672cf-290">A.</span><span class="sxs-lookup"><span data-stu-id="672cf-290">A.</span></span> <span data-ttu-id="672cf-291">Cihazınızı Güvenilenler listesine olup olmadığını doğrulamak için aşağıdaki sorun giderme etkileşimli komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="672cf-291">To verify whether your device is whitelisted, use the following troubleshooting interactive command:</span></span>

    multipathd –k
    multipathd> show devices
    available block devices:
    ram0 devnode blacklisted, unmonitored
    ram1 devnode blacklisted, unmonitored
    ram2 devnode blacklisted, unmonitored
    ram3 devnode blacklisted, unmonitored
    ram4 devnode blacklisted, unmonitored
    ram5 devnode blacklisted, unmonitored
    ram6 devnode blacklisted, unmonitored
    ram7 devnode blacklisted, unmonitored
    ram8 devnode blacklisted, unmonitored
    ram9 devnode blacklisted, unmonitored
    ram10 devnode blacklisted, unmonitored
    ram11 devnode blacklisted, unmonitored
    ram12 devnode blacklisted, unmonitored
    ram13 devnode blacklisted, unmonitored
    ram14 devnode blacklisted, unmonitored
    ram15 devnode blacklisted, unmonitored
    loop0 devnode blacklisted, unmonitored
    loop1 devnode blacklisted, unmonitored
    loop2 devnode blacklisted, unmonitored
    loop3 devnode blacklisted, unmonitored
    loop4 devnode blacklisted, unmonitored
    loop5 devnode blacklisted, unmonitored
    loop6 devnode blacklisted, unmonitored
    loop7 devnode blacklisted, unmonitored
    sr0 devnode blacklisted, unmonitored
    sda devnode whitelisted, monitored
    dm-0 devnode blacklisted, unmonitored
    dm-1 devnode blacklisted, unmonitored
    dm-2 devnode blacklisted, unmonitored
    sdb devnode whitelisted, monitored
    sdc devnode whitelisted, monitored
    dm-3 devnode blacklisted, unmonitored


<span data-ttu-id="672cf-292">Daha fazla bilgi için Git [etkileşimli komutu çoklu yol oluşturma için sorun giderme kullanmak](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span><span class="sxs-lookup"><span data-stu-id="672cf-292">For more information, go to [use troubleshooting interactive command for multipathing](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span></span>

## <a name="list-of-useful-commands"></a><span data-ttu-id="672cf-293">Yararlı komutların listesi</span><span class="sxs-lookup"><span data-stu-id="672cf-293">List of useful commands</span></span>
| <span data-ttu-id="672cf-294">Tür</span><span class="sxs-lookup"><span data-stu-id="672cf-294">Type</span></span> | <span data-ttu-id="672cf-295">Komut</span><span class="sxs-lookup"><span data-stu-id="672cf-295">Command</span></span> | <span data-ttu-id="672cf-296">Açıklama</span><span class="sxs-lookup"><span data-stu-id="672cf-296">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="672cf-297">**iSCSI**</span><span class="sxs-lookup"><span data-stu-id="672cf-297">**iSCSI**</span></span> |`service iscsid start` |<span data-ttu-id="672cf-298">İSCSI Hizmeti</span><span class="sxs-lookup"><span data-stu-id="672cf-298">Start iSCSI service</span></span> |
| &nbsp; |`service iscsid stop` |<span data-ttu-id="672cf-299">İSCSI hizmetini durdurun</span><span class="sxs-lookup"><span data-stu-id="672cf-299">Stop iSCSI service</span></span> |
| &nbsp; |`service iscsid restart` |<span data-ttu-id="672cf-300">İSCSI hizmetini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="672cf-300">Restart iSCSI service</span></span> |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |<span data-ttu-id="672cf-301">Belirtilen adres kullanılabilir hedeflerde Bul</span><span class="sxs-lookup"><span data-stu-id="672cf-301">Discover available targets on the specified address</span></span> |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |<span data-ttu-id="672cf-302">İSCSI hedef oturum açın</span><span class="sxs-lookup"><span data-stu-id="672cf-302">Log in to the iSCSI target</span></span> |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |<span data-ttu-id="672cf-303">İSCSI hedef Oturumu Kapat</span><span class="sxs-lookup"><span data-stu-id="672cf-303">Log out from the iSCSI target</span></span> |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |<span data-ttu-id="672cf-304">İSCSI Başlatıcı adı yazdırma</span><span class="sxs-lookup"><span data-stu-id="672cf-304">Print iSCSI initiator name</span></span> |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |<span data-ttu-id="672cf-305">İSCSI oturumu ve ana bilgisayarda bulunan birim durumunu denetleyin</span><span class="sxs-lookup"><span data-stu-id="672cf-305">Check the state of the iSCSI session and volume discovered on the host</span></span> |
| &nbsp; |`iscsi –m session` |<span data-ttu-id="672cf-306">Konak ve StorSimple cihazı arasında kurulan tüm iSCSI oturumları gösterir</span><span class="sxs-lookup"><span data-stu-id="672cf-306">Shows all the iSCSI sessions established between the host and the StorSimple device</span></span> |
|  | | |
| <span data-ttu-id="672cf-307">**Çoklu yol oluşturma**</span><span class="sxs-lookup"><span data-stu-id="672cf-307">**Multipathing**</span></span> |`service multipathd start` |<span data-ttu-id="672cf-308">Çok yollu arka plan programı Başlat</span><span class="sxs-lookup"><span data-stu-id="672cf-308">Start multipath daemon</span></span> |
| &nbsp; |`service multipathd stop` |<span data-ttu-id="672cf-309">Çok yollu arka plan programı durdurun</span><span class="sxs-lookup"><span data-stu-id="672cf-309">Stop multipath daemon</span></span> |
| &nbsp; |`service multipathd restart` |<span data-ttu-id="672cf-310">Çok yollu arka plan programı yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="672cf-310">Restart multipath daemon</span></span> |
| &nbsp; |`chkconfig multipathd on` </br> <span data-ttu-id="672cf-311">OR</span><span class="sxs-lookup"><span data-stu-id="672cf-311">OR</span></span> </br> `mpathconf –with_chkconfig y` |<span data-ttu-id="672cf-312">Önyükleme sırasında başlatmak çok yollu arka plan programı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="672cf-312">Enable multipath daemon to start at boot time</span></span> |
| &nbsp; |`multipathd –k` |<span data-ttu-id="672cf-313">Sorun giderme için etkileşimli konsolunu başlatın</span><span class="sxs-lookup"><span data-stu-id="672cf-313">Start the interactive console for troubleshooting</span></span> |
| &nbsp; |`multipath –l` |<span data-ttu-id="672cf-314">Liste çok yollu bağlantıları ve cihazlar</span><span class="sxs-lookup"><span data-stu-id="672cf-314">List multipath connections and devices</span></span> |
| &nbsp; |`mpathconf --enable` |<span data-ttu-id="672cf-315">Bir örnek mulitpath.conf dosya oluşturma`/etc/mulitpath.conf`</span><span class="sxs-lookup"><span data-stu-id="672cf-315">Create a sample mulitpath.conf file in `/etc/mulitpath.conf`</span></span> |
|  | | |

## <a name="next-steps"></a><span data-ttu-id="672cf-316">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="672cf-316">Next steps</span></span>
<span data-ttu-id="672cf-317">Linux ana bilgisayarına MPIO yapılandırma gibi aşağıdaki CentoS 6.6 belgelerine bakın gerekebilir:</span><span class="sxs-lookup"><span data-stu-id="672cf-317">As you are configuring MPIO on Linux host, you may also need to refer to the following CentoS 6.6 documents:</span></span>

* [<span data-ttu-id="672cf-318">CentOS MPIO ayarlama</span><span class="sxs-lookup"><span data-stu-id="672cf-318">Setting up MPIO on CentOS</span></span>](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [<span data-ttu-id="672cf-319">Linux eğitim Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="672cf-319">Linux Training Guide</span></span>](http://linux-training.be/files/books/LinuxAdm.pdf)

