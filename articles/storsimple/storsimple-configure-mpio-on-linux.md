---
title: "StorSimple Linux konağında MPIO aaaConfigure | Microsoft Docs"
description: "CentOS 6.6 çalıştıran bağlı StorSimple tooa Linux konağında MPIO yapılandırma"
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
ms.openlocfilehash: d9f7e02903243494c909313fb2c33ac690764274
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a><span data-ttu-id="6fbb7-103">CentOS çalıştıran bir StorSimple konakta MPIO'yu yapılandırın</span><span class="sxs-lookup"><span data-stu-id="6fbb7-103">Configure MPIO on a StorSimple host running CentOS</span></span>
<span data-ttu-id="6fbb7-104">Bu makalede, Centos 6.6 ana bilgisayar sunucusunda hello adımları gerekli tooconfigure çoklu yol oluşturma g/ç (MPIO) açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-104">This article explains hello steps required tooconfigure Multipathing IO (MPIO) on your Centos 6.6 host server.</span></span> <span data-ttu-id="6fbb7-105">iSCSI başlatıcıları aracılığıyla yüksek kullanılabilirlik için bağlı tooyour Microsoft Azure StorSimple cihaz Hello konak sunucusudur.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-105">hello host server is connected tooyour Microsoft Azure StorSimple device for high availability via iSCSI initiators.</span></span> <span data-ttu-id="6fbb7-106">Ayrıntı hello otomatik bulma çok yollu cihazların ve yalnızca StorSimple birimler için özel kurulum hello açıklar.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-106">It describes in detail hello automatic discovery of multipath devices and hello specific setup only for StorSimple volumes.</span></span>

<span data-ttu-id="6fbb7-107">Bu yordam, StorSimple 8000 serisi cihazlar geçerli tooall hello modellerinin kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-107">This procedure is applicable tooall hello models of StorSimple 8000 series devices.</span></span>

> [!NOTE]
> <span data-ttu-id="6fbb7-108">Bu yordam, StorSimple sanal cihaz için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-108">This procedure cannot be used for a StorSimple virtual device.</span></span> <span data-ttu-id="6fbb7-109">Nasıl tooconfigure konak sunucuları sanal cihazınız için daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-109">For more information, see how tooconfigure host servers for your virtual device.</span></span>
> 
> 

## <a name="about-multipathing"></a><span data-ttu-id="6fbb7-110">Çoklu yol oluşturma hakkında</span><span class="sxs-lookup"><span data-stu-id="6fbb7-110">About multipathing</span></span>
<span data-ttu-id="6fbb7-111">Merhaba çoklu yol oluşturma özelliği sağlar, tooconfigure ana sunucu ile bir depolama aygıtı arasında birden çok g/ç yollar.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-111">hello multipathing feature allows you tooconfigure multiple I/O paths between a host server and a storage device.</span></span> <span data-ttu-id="6fbb7-112">Bu g/ç yolları ayrı kablo, anahtarlar, ağ arabirimleri ve denetleyicileri dahil edebileceğiniz fiziksel SAN bağlantılardır.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-112">These I/O paths are physical SAN connections that can include separate cables, switches, network interfaces, and controllers.</span></span> <span data-ttu-id="6fbb7-113">Çoklu yol oluşturma hello g/ç yolu, tooconfigure tüm toplanan hello yollar ile ilişkili yeni bir cihaz toplar.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-113">Multipathing aggregates hello I/O paths, tooconfigure a new device that is associated with all of hello aggregated paths.</span></span>

<span data-ttu-id="6fbb7-114">Çoklu yol oluşturma Hello amacı iki Katlama şöyledir:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-114">hello purpose of multipathing is two-fold:</span></span>

* <span data-ttu-id="6fbb7-115">**Yüksek kullanılabilirlik**: hello g/ç yolu (örneğin, bir kablo, anahtar, ağ arabirimi veya denetleyicisi) herhangi bir öğeyi başarısız olursa alternatif bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-115">**High availability**: It provides an alternate path if any element of hello I/O path (such as a cable, switch, network interface, or controller) fails.</span></span>
* <span data-ttu-id="6fbb7-116">**Yük Dengeleme**: depolama Cihazınızı hello yapılandırmasına bağlı olarak bu hello hello g/ç yolları yükleri algılama ve dinamik olarak bu yükleri dengelenmesi performansı artırabilir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-116">**Load balancing**: Depending on hello configuration of your storage device, it can improve hello performance by detecting loads on hello I/O paths and dynamically rebalancing those loads.</span></span>

### <a name="about-multipathing-components"></a><span data-ttu-id="6fbb7-117">Çoklu yol oluşturma bileşenleri hakkında</span><span class="sxs-lookup"><span data-stu-id="6fbb7-117">About multipathing components</span></span>
<span data-ttu-id="6fbb7-118">Çoklu yol oluşturma Linux içindeki çekirdek bileşenleri ve aşağıdaki tabloda gibi kullanıcı alanı bileşenleri oluşur.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-118">Multipathing in Linux consists of kernel components and user-space components as tabulated below.</span></span>

* <span data-ttu-id="6fbb7-119">**Çekirdek**: hello ana bileşendir hello *aygıt Eşleyici* g/ç yeniden yönlendirmeler ve yolları ve yol grupları için yük devretmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-119">**Kernel**: hello main component is hello *device-mapper* that reroutes I/O and supports failover for paths and path groups.</span></span>

* <span data-ttu-id="6fbb7-120">**Kullanıcı alanı**: Bunlar *çok yollu Araçları* , multipathed cihazları yönetme hello aygıt Eşleyici çok yollu modülü yönlendirerek hangi toodo.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-120">**User-space**: These are *multipath-tools* that manage multipathed devices by instructing hello device-mapper multipath module what toodo.</span></span> <span data-ttu-id="6fbb7-121">Merhaba araçları şunlardan oluşur:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-121">hello tools consist of:</span></span>
   
   * <span data-ttu-id="6fbb7-122">**Çok yollu**: listeler ve multipathed cihazları yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-122">**Multipath**: lists and configures multipathed devices.</span></span>
   * <span data-ttu-id="6fbb7-123">**Multipathd**: arka plan programı çok yollu ve izleyiciler hello yolları yürütür.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-123">**Multipathd**: daemon that executes multipath and monitors hello paths.</span></span>
   * <span data-ttu-id="6fbb7-124">**Devmap adı**: devmaps için anlamlı bir aygıt adı tooudev sağlar.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-124">**Devmap-name**: provides a meaningful device-name tooudev for devmaps.</span></span>
   * <span data-ttu-id="6fbb7-125">**Kpartx**: Doğrusal devmaps toodevice bölümleri toomake çok yollu eşlemeleri bölümlenebilir eşler.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-125">**Kpartx**: maps linear devmaps toodevice partitions toomake multipath maps partitionable.</span></span>
   * <span data-ttu-id="6fbb7-126">**MultiPath.conf**: kullanılan toooverwrite hello yerleşik yapılandırma tablosu çok yollu arka plan programı için yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-126">**Multipath.conf**: configuration file for multipath daemon that is used toooverwrite hello built-in configuration table.</span></span>

### <a name="about-hello-multipathconf-configuration-file"></a><span data-ttu-id="6fbb7-127">Merhaba multipath.conf yapılandırma dosyası hakkında</span><span class="sxs-lookup"><span data-stu-id="6fbb7-127">About hello multipath.conf configuration file</span></span>
<span data-ttu-id="6fbb7-128">Merhaba yapılandırma dosyası `/etc/multipath.conf` hello çoğunu çoklu yol oluşturma özellikleri kullanıcı tarafından yapılandırılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-128">hello configuration file `/etc/multipath.conf` makes many of hello multipathing features user-configurable.</span></span> <span data-ttu-id="6fbb7-129">Merhaba `multipath` komut ve hello çekirdek arka plan programı `multipathd` bu dosyada bulunan bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-129">hello `multipath` command and hello kernel daemon `multipathd` use information found in this file.</span></span> <span data-ttu-id="6fbb7-130">Merhaba dosya yalnızca hello çok yollu cihazların Merhaba yapılandırması sırasında alınmadığında.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-130">hello file is consulted only during hello configuration of hello multipath devices.</span></span> <span data-ttu-id="6fbb7-131">Merhaba çalıştırmadan önce tüm değişiklikleri yapıldığından emin olun `multipath` komutu.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-131">Make sure that all changes are made before you run hello `multipath` command.</span></span> <span data-ttu-id="6fbb7-132">Daha sonra hello dosyasını değiştirirseniz toostop gerekir ve multipathd hello değişiklikleri tootake etkisi için yeniden başlatma.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-132">If you modify hello file afterwards, you will need toostop and start multipathd again for hello changes tootake effect.</span></span>

<span data-ttu-id="6fbb7-133">Merhaba multipath.conf beş bölümü vardır:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-133">hello multipath.conf has five sections:</span></span>

- <span data-ttu-id="6fbb7-134">**Sistem düzeyinde varsayılanlarını** *(varsayılan)*: sistem düzeyinde varsayılanlarını geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-134">**System level defaults** *(defaults)*: You can override system level defaults.</span></span>
- <span data-ttu-id="6fbb7-135">**Kara listede aygıtları** *(kara liste)*: cihaz Eşleyicisi tarafından denetlenmeyen cihazların Merhaba listesi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-135">**Blacklisted devices** *(blacklist)*: You can specify hello list of devices that should not be controlled by device-mapper.</span></span>
- <span data-ttu-id="6fbb7-136">**Özel durumlar kara listeye** *(blacklist_exceptions)*: hello kara listeye listelenen olsa bile çok yollu cihazlar kabul belirli aygıtları toobe tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-136">**Blacklist exceptions** *(blacklist_exceptions)*: You can identify specific devices toobe treated as multipath devices even if listed in hello blacklist.</span></span>
- <span data-ttu-id="6fbb7-137">**Depolama denetleyicisi belirli ayarları** *(aygıtlar)*: Satıcı ve ürün bilgilerine sahip uygulanan toodevices olacaktır yapılandırma ayarları belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-137">**Storage controller specific settings** *(devices)*: You can specify configuration settings that will be applied toodevices that have Vendor and Product information.</span></span>
- <span data-ttu-id="6fbb7-138">**Aygıt belirli ayarları** *(multipaths)*: Bu bölümde toofine ayarlama hello yapılandırma ayarlarını tek tek LUN'larını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-138">**Device specific settings** *(multipaths)*: You can use this section toofine-tune hello configuration settings for individual LUNs.</span></span>

## <a name="configure-multipathing-on-storsimple-connected-toolinux-host"></a><span data-ttu-id="6fbb7-139">Çoklu yol oluşturma StorSimple bağlı tooLinux ana bilgisayarda yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6fbb7-139">Configure multipathing on StorSimple connected tooLinux host</span></span>
<span data-ttu-id="6fbb7-140">Bir StorSimple cihazı bağlı tooa Linux ana yüksek kullanılabilirlik için yapılandırılabilir ve Yük Dengeleme.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-140">A StorSimple device connected tooa Linux host can be configured for high availability and load balancing.</span></span> <span data-ttu-id="6fbb7-141">Örneğin, iki arabirim toohello SAN bağlı bağlı toohello SAN ve hello aygıtın iki arabirim Hello Linux ana bilgisayar varsa, bu arabirimleri olan gibi hello aynı alt ağda sonra olacaktır 4 yolları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-141">For example, if hello Linux host has two interfaces connected toohello SAN and hello device has two interfaces connected toohello SAN such that these interfaces are on hello same subnet, then there will be 4 paths available.</span></span> <span data-ttu-id="6fbb7-142">Her veri arabirimi hello cihaz ve ana bilgisayar arabirimde farklı bir IP alt ağ (ve değil yönlendirilebilir) varsa, ancak sonra yalnızca 2 yolları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-142">However, if each DATA interface on hello device and host interface are on a different IP subnet (and not routable), then only 2 paths will be available.</span></span> <span data-ttu-id="6fbb7-143">Çoklu yol oluşturma tooautomatically yapılandırabileceğiniz tüm hello kullanılabilir yolları Bul, bu yollar için bir Yük Dengeleme algoritması seçin, yalnızca StorSimple birimler için belirli yapılandırma ayarları uygulamak ve ardından etkinleştirmek ve çoklu yol oluşturma doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-143">You can configure multipathing tooautomatically discover all hello available paths, choose a load-balancing algorithm for those paths, apply specific configuration settings for StorSimple-only volumes, and then enable and verify multipathing.</span></span>

<span data-ttu-id="6fbb7-144">Merhaba aşağıdaki yordamı nasıl tooconfigure olması bir StorSimple cihaz kaydedildiğinde iki ağ arabirimi ile iki ağ arabirimi ile bağlı tooa konak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-144">hello following procedure describes how tooconfigure multipathing when a StorSimple device with two network interfaces is connected tooa host with two network interfaces.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6fbb7-145">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6fbb7-145">Prerequisites</span></span>
<span data-ttu-id="6fbb7-146">Bu bölümde, CentOS sunucu ve StorSimple cihazınız için yapılandırma önkoşulları hello ayrıntıları verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-146">This section details hello configuration prerequisites for CentOS server and your StorSimple device.</span></span>

### <a name="on-centos-host"></a><span data-ttu-id="6fbb7-147">CentOS konakta</span><span class="sxs-lookup"><span data-stu-id="6fbb7-147">On CentOS host</span></span>
1. <span data-ttu-id="6fbb7-148">CentOS ana bilgisayar 2 ağ arabirimleri etkin olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-148">Make sure that your CentOS host has 2 network interfaces enabled.</span></span> <span data-ttu-id="6fbb7-149">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-149">Type:</span></span>
   
    `ifconfig`
   
    <span data-ttu-id="6fbb7-150">iki ağ arabirimleri hello aşağıdaki örnek hello çıkış gösterir (`eth0` ve `eth1`) hello konakta yok.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-150">hello following example shows hello output when two network interfaces (`eth0` and `eth1`) are present on hello host.</span></span>
   
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
2. <span data-ttu-id="6fbb7-151">Yükleme *iSCSI-Başlatıcı-yardımcı programları* CentOS sunucunuzda.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-151">Install *iSCSI-initiator-utils* on your CentOS server.</span></span> <span data-ttu-id="6fbb7-152">Aşağıdaki adımları tooinstall hello gerçekleştirmek *iSCSI-Başlatıcı-yardımcı programları*.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-152">Perform hello following steps tooinstall *iSCSI-initiator-utils*.</span></span>
   
   1. <span data-ttu-id="6fbb7-153">Oturum açma `root` CentOS ana bilgisayarınızın INTO.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-153">Log on as `root` into your CentOS host.</span></span>
   2. <span data-ttu-id="6fbb7-154">Merhaba yüklemek *iSCSI-Başlatıcı-yardımcı programları*.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-154">Install hello *iSCSI-initiator-utils*.</span></span> <span data-ttu-id="6fbb7-155">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-155">Type:</span></span>
      
       `yum install iscsi-initiator-utils`
   3. <span data-ttu-id="6fbb7-156">Merhaba sonra *iSCSI-Başlatıcı-yardımcı programları* başarıyla yüklenmiş hello iSCSI hizmetini başlatın.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-156">After hello *iSCSI-Initiator-utils* is successfully installed, start hello iSCSI service.</span></span> <span data-ttu-id="6fbb7-157">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-157">Type:</span></span>
      
       `service iscsid start`
      
       <span data-ttu-id="6fbb7-158">Olaylar üzerinde `iscsid` gerçekten başlatmak ve hello Mayıs `--force` seçeneği gerekebilir</span><span class="sxs-lookup"><span data-stu-id="6fbb7-158">On occasions, `iscsid` may not actually start and hello `--force` option may be needed</span></span>
   4. <span data-ttu-id="6fbb7-159">iSCSI başlatıcısı kullanım hello önyükleme süre boyunca etkin olduğunu tooensure `chkconfig` tooenable hello hizmet komutu.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-159">tooensure that your iSCSI initiator is enabled during boot time, use hello `chkconfig` command tooenable hello service.</span></span>
      
       `chkconfig iscsi on`
   5. <span data-ttu-id="6fbb7-160">düzgün şekilde olan Kurulum, tooverify hello komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-160">tooverify that that it was properly setup, run hello command:</span></span>
      
       `chkconfig --list | grep iscsi`
      
       <span data-ttu-id="6fbb7-161">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-161">A sample output is shown below.</span></span>
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       <span data-ttu-id="6fbb7-162">Yukarıdaki örnek Hello iSCSI ortamınızı önyükleme zamanında çalışma Düzey 2, 3, 4 ve 5 çalışacağını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-162">From hello above example, you can see that your iSCSI environment will run on boot time on run levels 2, 3, 4, and 5.</span></span>
3. <span data-ttu-id="6fbb7-163">Yükleme *aygıt-Eşleyici-çok yollu*.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-163">Install *device-mapper-multipath*.</span></span> <span data-ttu-id="6fbb7-164">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-164">Type:</span></span>
   
    `yum install device-mapper-multipath`
   
    <span data-ttu-id="6fbb7-165">Merhaba yüklemesi başlatılır.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-165">hello installation will start.</span></span> <span data-ttu-id="6fbb7-166">Tür **Y** onaylamanız istendiğinde toocontinue.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-166">Type **Y** toocontinue when prompted for confirmation.</span></span>

### <a name="on-storsimple-device"></a><span data-ttu-id="6fbb7-167">StorSimple cihazında</span><span class="sxs-lookup"><span data-stu-id="6fbb7-167">On StorSimple device</span></span>
<span data-ttu-id="6fbb7-168">StorSimple Cihazınızı olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-168">Your StorSimple device should have:</span></span>

* <span data-ttu-id="6fbb7-169">İSCSI için iki arabirimin en az.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-169">A minimum of two interfaces enabled for iSCSI.</span></span> <span data-ttu-id="6fbb7-170">iki arabirim StorSimple Cihazınızda iSCSI etkin tooverify hello StorSimple cihazınız için Klasik Azure Portalı'ndaki adımları izleyerek hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-170">tooverify that two interfaces are iSCSI-enabled on your StorSimple device, perform hello following steps in hello Azure classic portal for your StorSimple device:</span></span>
  
  1. <span data-ttu-id="6fbb7-171">StorSimple cihazınız için hello Klasik portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-171">Log into hello classic portal for your StorSimple device.</span></span>
  2. <span data-ttu-id="6fbb7-172">StorSimple Yöneticisi hizmetiniz seçin, **aygıtları** ve hello belirli StorSimple cihazı seçin.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-172">Select your StorSimple Manager service, click **Devices** and choose hello specific StorSimple device.</span></span> <span data-ttu-id="6fbb7-173">Tıklatın **yapılandırma** ve hello ağ arabirimi ayarlarını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-173">Click **Configure** and verify hello network interface settings.</span></span> <span data-ttu-id="6fbb7-174">İki iSCSI etkin ağ arabirimlerine sahip bir ekran görüntüsü aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-174">A screenshot with two iSCSI-enabled network interfaces is shown below.</span></span> <span data-ttu-id="6fbb7-175">Burada veri 2 ve veri 3, her iki 10 GbE arabirimleri iSCSI için etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-175">Here DATA 2 and DATA 3, both 10 GbE interfaces are enabled for iSCSI.</span></span>
     
      ![MPIO StorsSimple veri 2 yapılandırma](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![MPIO StorSimple veri 3 yapılandırma](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      <span data-ttu-id="6fbb7-178">Merhaba, **yapılandırma** sayfası</span><span class="sxs-lookup"><span data-stu-id="6fbb7-178">In hello **Configure** page</span></span>
     
     1. <span data-ttu-id="6fbb7-179">Her iki ağ arabirimleri iSCSI etkin olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-179">Ensure that both network interfaces are iSCSI-enabled.</span></span> <span data-ttu-id="6fbb7-180">Merhaba **iSCSI etkin** alan çok ayarlanmalıdır**Evet**.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-180">hello **iSCSI enabled** field should be set too**Yes**.</span></span>
     2. <span data-ttu-id="6fbb7-181">Merhaba ağ arabirimleri hello sahip olduğundan emin olun aynı hızı, ikisi de 1 GbE veya 10 GbE olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-181">Ensure that hello network interfaces have hello same speed, both should be 1 GbE or 10 GbE.</span></span>
     3. <span data-ttu-id="6fbb7-182">Merhaba iSCSI etkin arabirimlerin Hello IPv4 adreslerini not edin ve hello ana bilgisayarda daha sonra kullanmak için kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-182">Note hello IPv4 addresses of hello iSCSI-enabled interfaces and save for later use on hello host.</span></span>
* <span data-ttu-id="6fbb7-183">StorSimple Cihazınızda Hello iSCSI arabirimleri hello CentOS sunucusundan erişilebilir olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-183">hello iSCSI interfaces on your StorSimple device should be reachable from hello CentOS server.</span></span>
      <span data-ttu-id="6fbb7-184">tooverify Bu, ana bilgisayar sunucusunda tooprovide hello IP adresleri, StorSimple iSCSI etkin ağ arabirimlerinin gerekir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-184">tooverify this, you need tooprovide hello IP addresses of your StorSimple iSCSI-enabled network interfaces on your host server.</span></span> <span data-ttu-id="6fbb7-185">Merhaba kullanılan komutlar ve karşılık gelen çıktı veri2 ile Merhaba (10.126.162.25) ve DATA3 (10.126.162.26) aşağıda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-185">hello commands used and hello corresponding output with DATA2 (10.126.162.25) and DATA3 (10.126.162.26) is shown below:</span></span>
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a><span data-ttu-id="6fbb7-186">Donanım yapılandırması</span><span class="sxs-lookup"><span data-stu-id="6fbb7-186">Hardware configuration</span></span>
<span data-ttu-id="6fbb7-187">Merhaba iki iSCSI ağ arabirimleri artıklık için ayrı yazmalar bağlanmak öneririz.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-187">We recommend that you connect hello two iSCSI network interfaces on separate paths for redundancy.</span></span> <span data-ttu-id="6fbb7-188">Aşağıdaki Hello şekilde hello yüksek kullanılabilirlik için önerilen donanım yapılandırması ve CentOS sunucunuz ve StorSimple cihazı için çoklu yol oluşturma Yük Dengeleme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-188">hello figure below shows hello recommended hardware configuration for high availability and load-balancing multipathing for your CentOS server and StorSimple device.</span></span>

![StorSimple tooLinux ana bilgisayar için MPIO donanım yapılandırması](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

<span data-ttu-id="6fbb7-190">Şekil önceki hello gösterildiği gibi kullanın:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-190">As shown in hello preceding figure:</span></span>

* <span data-ttu-id="6fbb7-191">StorSimple Cihazınızı iki denetleyicileri Aktif-Pasif yapılandırmayla kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-191">Your StorSimple device is in an active-passive configuration with two controllers.</span></span>
* <span data-ttu-id="6fbb7-192">İki SAN anahtarları bağlı tooyour aygıt denetleyicileri etkilenir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-192">Two SAN switches are connected tooyour device controllers.</span></span>
* <span data-ttu-id="6fbb7-193">StorSimple Cihazınızda iki iSCSI başlatıcıları etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-193">Two iSCSI initiators are enabled on your StorSimple device.</span></span>
* <span data-ttu-id="6fbb7-194">İki ağ arabirimi, CentOS ana bilgisayarda etkin.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-194">Two network interfaces are enabled on your CentOS host.</span></span>

<span data-ttu-id="6fbb7-195">Merhaba ana bilgisayar ve veri arabirimleri yönlendirilebilir olması durumunda yapılandırma yukarıda hello cihaz ve hello ana bilgisayar arasında 4 ayrı yollar sunacak.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-195">hello above configuration will yield 4 separate paths between your device and hello host if hello host and data interfaces are routable.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="6fbb7-196">1 GbE ve çoklu yol oluşturma için 10 GbE ağ arabirimleri karıştırmamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-196">We recommend that you do not mix 1 GbE and 10 GbE network interfaces for multipathing.</span></span> <span data-ttu-id="6fbb7-197">İki ağ arabirimleri kullanılırken, her iki hello arabirimleri hello aynı türde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-197">When using two network interfaces, both hello interfaces should be hello identical type.</span></span>
> * <span data-ttu-id="6fbb7-198">Veri2 ve DATA3 10 GbE ağ arabirimleri ise, StorSimple Cihazınızda DATA0, Veri1, DATA4 ve DATA5 1 GbE arabirimlerdir. |</span><span class="sxs-lookup"><span data-stu-id="6fbb7-198">On your StorSimple device, DATA0, DATA1, DATA4 and DATA5 are 1 GbE interfaces whereas DATA2 and DATA3 are 10 GbE network interfaces.|</span></span>
> 
> 

## <a name="configuration-steps"></a><span data-ttu-id="6fbb7-199">Yapılandırma adımları</span><span class="sxs-lookup"><span data-stu-id="6fbb7-199">Configuration steps</span></span>
<span data-ttu-id="6fbb7-200">Merhaba yapılandırma adımları için çoklu yol oluşturma hello kullanılabilir yollar çoklu yol oluşturma etkinleştirme ve son olarak hello yapılandırmasını doğrulama hello Yük Dengeleme algoritması toouse, belirtme, otomatik bulma için yapılandırmayı içerir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-200">hello configuration steps for multipathing involve configuring hello available paths for automatic discovery, specifying hello load-balancing algorithm toouse, enabling multipathing and finally verifying hello configuration.</span></span> <span data-ttu-id="6fbb7-201">Bu adımların her biri aşağıdaki bölümlerde hello ayrıntılı ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-201">Each of these steps is discussed in detail in hello following sections.</span></span>

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a><span data-ttu-id="6fbb7-202">1. adım: çoklu yol oluşturma otomatik bulma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6fbb7-202">Step 1: Configure multipathing for automatic discovery</span></span>
<span data-ttu-id="6fbb7-203">Merhaba çok yollu desteklenen cihazları otomatik olarak bulunan ve yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-203">hello multipath-supported devices can be automatically discovered and configured.</span></span>

1. <span data-ttu-id="6fbb7-204">Initialize `/etc/multipath.conf` dosya.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-204">Initialize `/etc/multipath.conf` file.</span></span> <span data-ttu-id="6fbb7-205">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-205">Type:</span></span>
   
     `mpathconf --enable`
   
    <span data-ttu-id="6fbb7-206">Merhaba komutu yukarıda oluşturacak bir `sample/etc/multipath.conf` dosyası.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-206">hello above command will create a `sample/etc/multipath.conf` file.</span></span>
2. <span data-ttu-id="6fbb7-207">Çok yollu hizmetini başlatın.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-207">Start multipath service.</span></span> <span data-ttu-id="6fbb7-208">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-208">Type:</span></span>
   
    `service multipathd start`
   
    <span data-ttu-id="6fbb7-209">Çıktı aşağıdaki hello görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-209">You will see hello following output:</span></span>
   
    `Starting multipathd daemon:`
3. <span data-ttu-id="6fbb7-210">Multipaths otomatik olarak bulmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-210">Enable automatic discovery of multipaths.</span></span> <span data-ttu-id="6fbb7-211">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-211">Type:</span></span>
   
    `mpathconf --find_multipaths y`
   
    <span data-ttu-id="6fbb7-212">Bunu hello Varsayılanları bölümünü değiştirmek, `multipath.conf` aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-212">This will modify hello defaults section of your `multipath.conf` as shown below:</span></span>
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a><span data-ttu-id="6fbb7-213">2. adım: StorSimple birimler için çoklu yol oluşturmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6fbb7-213">Step 2: Configure multipathing for StorSimple volumes</span></span>
<span data-ttu-id="6fbb7-214">Varsayılan olarak, tüm cihazların Merhaba multipath.conf dosyasında listelenen siyah ve atlanır.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-214">By default, all devices are black listed in hello multipath.conf file and will be bypassed.</span></span> <span data-ttu-id="6fbb7-215">StorSimple cihazları birimlerin toocreate kara liste özel durumları tooallow olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-215">You will need toocreate blacklist exceptions tooallow multipathing for volumes from StorSimple devices.</span></span>

1. <span data-ttu-id="6fbb7-216">Merhaba Düzenle `/etc/mulitpath.conf` dosya.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-216">Edit hello `/etc/mulitpath.conf` file.</span></span> <span data-ttu-id="6fbb7-217">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-217">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="6fbb7-218">Merhaba multipath.conf dosyasında Hello blacklist_exceptions bölümünü bulun.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-218">Locate hello blacklist_exceptions section in hello multipath.conf file.</span></span> <span data-ttu-id="6fbb7-219">StorSimple Cihazınızı Bu bölümde bir kara liste özel olarak listelenen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-219">Your StorSimple device needs toobe listed as a blacklist exception in this section.</span></span> <span data-ttu-id="6fbb7-220">İlgili bu dosya toomodify bunu (kullanımı yalnızca hello belirli modelinin kullanmakta olduğunuz hello aygıt) gösterildiği gibi satırları açıklamadan çıkarın:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-220">You can uncomment relevant lines in this file toomodify it as shown below (use only hello specific model of hello device you are using):</span></span>
   
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

### <a name="step-3-configure-round-robin-multipathing"></a><span data-ttu-id="6fbb7-221">3. adım: hepsini çoklu yol oluşturmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6fbb7-221">Step 3: Configure round-robin multipathing</span></span>
<span data-ttu-id="6fbb7-222">Bu Yük Dengeleme algoritması tüm hello kullanılabilir multipaths toohello etkin denetleyicisi Dengeli, hepsini bir biçimde kullanır.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-222">This load-balancing algorithm uses all hello available multipaths toohello active controller in a balanced, round-robin fashion.</span></span>

1. <span data-ttu-id="6fbb7-223">Merhaba Düzenle `/etc/multipath.conf` dosya.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-223">Edit hello `/etc/multipath.conf` file.</span></span> <span data-ttu-id="6fbb7-224">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-224">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="6fbb7-225">Merhaba altında `defaults` bölümü, kümesi hello `path_grouping_policy` çok`multibus`.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-225">Under hello `defaults` section, set hello `path_grouping_policy` too`multibus`.</span></span> <span data-ttu-id="6fbb7-226">Merhaba `path_grouping_policy` hello varsayılan yolu gruplandırma İlkesi tooapply toounspecified multipaths belirtir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-226">hello `path_grouping_policy` specifies hello default path grouping policy tooapply toounspecified multipaths.</span></span> <span data-ttu-id="6fbb7-227">Merhaba Varsayılanları bölümü, aşağıda gösterildiği gibi görünecektir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-227">hello defaults section will look as shown below.</span></span>
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> <span data-ttu-id="6fbb7-228">Merhaba en yaygın değerlerini `path_grouping_policy` içerir:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-228">hello most common values of `path_grouping_policy` include:</span></span>
> 
> * <span data-ttu-id="6fbb7-229">Yük devretme öncelik grubu başına 1 yolu =</span><span class="sxs-lookup"><span data-stu-id="6fbb7-229">failover = 1 path per priority group</span></span>
> * <span data-ttu-id="6fbb7-230">multibus 1 önceliği grubundaki tüm geçerli yolu =</span><span class="sxs-lookup"><span data-stu-id="6fbb7-230">multibus = all valid paths in 1 priority group</span></span>
> 
> 

### <a name="step-4-enable-multipathing"></a><span data-ttu-id="6fbb7-231">4. adım: Etkinleştirme çoklu yol oluşturma</span><span class="sxs-lookup"><span data-stu-id="6fbb7-231">Step 4: Enable multipathing</span></span>
1. <span data-ttu-id="6fbb7-232">Merhaba yeniden `multipathd` arka plan programı.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-232">Restart hello `multipathd` daemon.</span></span> <span data-ttu-id="6fbb7-233">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-233">Type:</span></span>
   
    `service multipathd restart`
2. <span data-ttu-id="6fbb7-234">Merhaba çıktı aşağıda gösterildiği gibi olacaktır:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-234">hello output will be as shown below:</span></span>
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a><span data-ttu-id="6fbb7-235">5. adım: çoklu yol oluşturma doğrulayın</span><span class="sxs-lookup"><span data-stu-id="6fbb7-235">Step 5: Verify multipathing</span></span>
1. <span data-ttu-id="6fbb7-236">Önce iSCSI bağlantı hello StorSimple aygıtla şu şekilde kurulduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-236">First make sure that iSCSI connection is established with hello StorSimple device as follows:</span></span>
   
   <span data-ttu-id="6fbb7-237">a.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-237">a.</span></span> <span data-ttu-id="6fbb7-238">StorSimple Cihazınızı bulur.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-238">Discover your StorSimple device.</span></span> <span data-ttu-id="6fbb7-239">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-239">Type:</span></span>
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on hello device>:<iSCSI port on StorSimple device>
    ```
    
    <span data-ttu-id="6fbb7-240">Aşağıda gösterildiği gibi 10.126.162.25 DATA0 için IP adresi olduğundan ve bağlantı noktası 3260 hello StorSimple cihazı giden iSCSI trafiği için açıldığında hello çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-240">hello output when IP address for DATA0 is 10.126.162.25 and port 3260 is opened on hello StorSimple device for outbound iSCSI traffic is as shown below:</span></span>
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    <span data-ttu-id="6fbb7-241">Kopya hello StorSimple Cihazınızı IQN `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, çıktı önceki hello gelen.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-241">Copy hello IQN of your StorSimple device, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, from hello preceding output.</span></span>

   <span data-ttu-id="6fbb7-242">b.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-242">b.</span></span> <span data-ttu-id="6fbb7-243">Toohello aygıt hedef IQN kullanarak bağlanın.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-243">Connect toohello device using target IQN.</span></span> <span data-ttu-id="6fbb7-244">Merhaba StorSimple cihaz burada hello iSCSI hedefi değil.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-244">hello StorSimple device is hello iSCSI target here.</span></span> <span data-ttu-id="6fbb7-245">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-245">Type:</span></span>

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    <span data-ttu-id="6fbb7-246">Merhaba aşağıdaki örnek çıkış hedefiyle IQN gösterir, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-246">hello following example shows output with a target IQN of `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span></span> <span data-ttu-id="6fbb7-247">Merhaba çıkış aygıtınızda toohello iki iSCSI etkin ağ arabirimi başarıyla bağlandıysanız gösterir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-247">hello output indicates that you have successfully connected toohello two iSCSI-enabled network interfaces on your device.</span></span>

    ```
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    <span data-ttu-id="6fbb7-248">Yalnızca bir ana bilgisayar arabirimi ve iki yollarını burada görürseniz, sonra tooenable ana bilgisayar üzerindeki her iki hello arabirimleri iSCSI için yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-248">If you see only one host interface and two paths here, then you need tooenable both hello interfaces on host for iSCSI.</span></span> <span data-ttu-id="6fbb7-249">Merhaba izleyebilirsiniz [ayrıntılı Linux belgelerindeki yönergeleri](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span><span class="sxs-lookup"><span data-stu-id="6fbb7-249">You can follow hello [detailed instructions in Linux documentation](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span></span>

2. <span data-ttu-id="6fbb7-250">Gösterilen toohello CentOS hello StorSimple cihazı sunucusundan bir birimdir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-250">A volume is exposed toohello CentOS server from hello StorSimple device.</span></span> <span data-ttu-id="6fbb7-251">Daha fazla bilgi için bkz: [6. adım: birim oluşturma](storsimple-deployment-walkthrough.md#step-6-create-a-volume) Merhaba, StorSimple Cihazınızda Klasik Azure Portalı aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-251">For more information, see [Step 6: Create a volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via hello Azure classic portal on your StorSimple device.</span></span>

3. <span data-ttu-id="6fbb7-252">Merhaba kullanılabilir yollar doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-252">Verify hello available paths.</span></span> <span data-ttu-id="6fbb7-253">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-253">Type:</span></span>

      ```
      multipath –l
      ```

      <span data-ttu-id="6fbb7-254">Aşağıdaki örneğine hello hello çıktı iki ağ arabirimi için bir StorSimple cihazı bağlı tooa tek ana bilgisayar ağ arabiriminde iki kullanılabilir yollar ile gösterilir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-254">hello following example shows hello output for two network interfaces on a StorSimple device connected tooa single host network interface with two available paths.</span></span>

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        hello following example shows hello output for two network interfaces on a StorSimple device connected tootwo host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After hello paths are configured, refer toohello specific instructions on your host operating system (Centos 6.6) toomount and format this volume.

## <a name="troubleshoot-multipathing"></a><span data-ttu-id="6fbb7-255">Çoklu yol oluşturma sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="6fbb7-255">Troubleshoot multipathing</span></span>
<span data-ttu-id="6fbb7-256">Çoklu yol oluşturma yapılandırması sırasında herhangi bir sorunla çalıştırırsanız, bu bölümde bazı yararlı ipuçları sağlanır.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-256">This section provides some helpful tips if you run into any issues during multipathing configuration.</span></span>

<span data-ttu-id="6fbb7-257">Q.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-257">Q.</span></span> <span data-ttu-id="6fbb7-258">Merhaba değişiklikleri görüntülenmemesini `multipath.conf` etkisi alma dosyası.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-258">I do not see hello changes in `multipath.conf` file taking effect.</span></span>

<span data-ttu-id="6fbb7-259">A.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-259">A.</span></span> <span data-ttu-id="6fbb7-260">Tüm değişiklikleri toohello yaptıysanız `multipath.conf` dosyası toorestart hello çoklu yol oluşturma hizmeti gerekir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-260">If you have made any changes toohello `multipath.conf` file, you will need toorestart hello multipathing service.</span></span> <span data-ttu-id="6fbb7-261">Merhaba aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-261">Type hello following command:</span></span>

    service multipathd restart

<span data-ttu-id="6fbb7-262">Q.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-262">Q.</span></span> <span data-ttu-id="6fbb7-263">Merhaba StorSimple cihazı iki ağ arabirimlerindeki ve iki ağ arabirimi hello ana bilgisayarda etkin.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-263">I have enabled two network interfaces on hello StorSimple device and two network interfaces on hello host.</span></span> <span data-ttu-id="6fbb7-264">Merhaba kullanılabilir yollar listelediğinizde, yalnızca iki yolu bakın.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-264">When I list hello available paths, I see only two paths.</span></span> <span data-ttu-id="6fbb7-265">I toosee dört kullanılabilir yollar bekleniyordu.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-265">I expected toosee four available paths.</span></span>

<span data-ttu-id="6fbb7-266">A.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-266">A.</span></span> <span data-ttu-id="6fbb7-267">Merhaba iki yolları hello üzerinde olduğundan emin olun aynı alt ağ ve yönlendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-267">Make sure that hello two paths are on hello same subnet and routable.</span></span> <span data-ttu-id="6fbb7-268">Merhaba ağ arabirimleri farklı VLAN'ları ve değil yönlendirilebilir varsa, yalnızca iki yolu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-268">If hello network interfaces are on different vLANs and not routable, you will see only two paths.</span></span> <span data-ttu-id="6fbb7-269">Tek yönlü tooverify bu toomake hello StorSimple cihazı bir ağ arabiriminde hem hello konak arabirimlerden ulaşabildiğimizden emin olur.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-269">One way tooverify this is toomake sure that you can reach both hello host interfaces from a network interface on hello StorSimple device.</span></span> <span data-ttu-id="6fbb7-270">Çok gerekir[Microsoft Support başvurun](storsimple-contact-microsoft-support.md) gibi bu doğrulama yalnızca bir destek oturumu yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-270">You will need too[contact Microsoft Support](storsimple-contact-microsoft-support.md) as this verification can only be done via a support session.</span></span>

<span data-ttu-id="6fbb7-271">Q.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-271">Q.</span></span> <span data-ttu-id="6fbb7-272">Kullanılabilir yollar listelediğinizde, herhangi bir çıktı görmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-272">When I list available paths, I do not see any output.</span></span>

<span data-ttu-id="6fbb7-273">A.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-273">A.</span></span> <span data-ttu-id="6fbb7-274">Genellikle, öneren hello çoklu yol oluşturma arka plan programı ile ilgili bir sorun multipathed yollar görmesini değil ve bu büyük olasılıkla herhangi bir sorun burada hello arasındadır `multipath.conf` dosya.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-274">Typically, not seeing any multipathed paths suggests a problem with hello multipathing daemon, and it’s most likely that any problem here lies in hello `multipath.conf` file.</span></span>

<span data-ttu-id="6fbb7-275">Hello çok yollu listelerini yanıt ayrıca herhangi bir diski yok anlamına gelebilir gibi aslında bazı disklerin toohello hedef bağlandıktan sonra görebileceğini denetleme değer olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-275">It would also be worth checking that you can actually see some disks after connecting toohello target, as no response from hello multipath listings could also mean you don’t have any disks.</span></span>

* <span data-ttu-id="6fbb7-276">Komut toorescan hello SCSI veri yolu izleyerek hello kullan:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-276">Use hello following command toorescan hello SCSI bus:</span></span>
  
    <span data-ttu-id="6fbb7-277">`$ rescan-scsi-bus.sh `(sg3_utils paketinin bir parçası)</span><span class="sxs-lookup"><span data-stu-id="6fbb7-277">`$ rescan-scsi-bus.sh `(part of sg3_utils package)</span></span>
* <span data-ttu-id="6fbb7-278">Merhaba aşağıdaki komutları yazın:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-278">Type hello following commands:</span></span>
  
    `$ dmesg | grep sd*`
     
     <span data-ttu-id="6fbb7-279">Veya</span><span class="sxs-lookup"><span data-stu-id="6fbb7-279">Or</span></span>
  
    `$ fdisk –l`
  
    <span data-ttu-id="6fbb7-280">Bu yakın zamanda eklenen diskler ayrıntılarını döndürür.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-280">These will return details of recently added disks.</span></span>
* <span data-ttu-id="6fbb7-281">toodetermine bir StorSimple disk olup olmadığını hello aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-281">toodetermine whether it is a StorSimple disk, use hello following commands:</span></span>
  
    `cat /sys/block/<DISK>/device/model`
  
    <span data-ttu-id="6fbb7-282">Bu, bir StorSimple disk olup olmadığını belirleyen bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-282">This will return a string, which will determine if it’s a StorSimple disk.</span></span>

<span data-ttu-id="6fbb7-283">Büyük olasılıkla ancak olası nedeni daha az A eski iscsid da olabilir PID.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-283">A less likely but possible cause could also be stale iscsid pid.</span></span> <span data-ttu-id="6fbb7-284">Merhaba iSCSI oturumunu kapatmak komutu toolog aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-284">Use hello following command toolog off from hello iSCSI sessions:</span></span>

    iscsiadm -m node --logout -p <Target_IP>

<span data-ttu-id="6fbb7-285">StorSimple cihazınız hello iSCSI hedef tüm bağlı hello ağ arabirimleri için bu komutu yineleyin.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-285">Repeat this command for all hello connected network interfaces on hello iSCSI target, which is your StorSimple device.</span></span> <span data-ttu-id="6fbb7-286">Tüm hello iSCSI oturumlardan kapattınız sonra hello iSCSI hedef IQN tooreestablish hello iSCSI oturumu kullanın.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-286">Once you have logged off from all hello iSCSI sessions, use hello iSCSI target IQN tooreestablish hello iSCSI session.</span></span> <span data-ttu-id="6fbb7-287">Merhaba aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-287">Type hello following command:</span></span>

    iscsiadm -m node --login -T <TARGET_IQN>


<span data-ttu-id="6fbb7-288">Q.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-288">Q.</span></span> <span data-ttu-id="6fbb7-289">Cihazımı Güvenilenler listesine olup olmadığından emin değilim.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-289">I am not sure if my device is whitelisted.</span></span>

<span data-ttu-id="6fbb7-290">A.</span><span class="sxs-lookup"><span data-stu-id="6fbb7-290">A.</span></span> <span data-ttu-id="6fbb7-291">tooverify Cihazınızı Güvenilenler listesine, olup, sorun giderme etkileşimli komutunu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-291">tooverify whether your device is whitelisted, use hello following troubleshooting interactive command:</span></span>

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


<span data-ttu-id="6fbb7-292">Daha fazla bilgi için çok Git[etkileşimli komutu çoklu yol oluşturma için sorun giderme kullanmak](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span><span class="sxs-lookup"><span data-stu-id="6fbb7-292">For more information, go too[use troubleshooting interactive command for multipathing](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span></span>

## <a name="list-of-useful-commands"></a><span data-ttu-id="6fbb7-293">Yararlı komutların listesi</span><span class="sxs-lookup"><span data-stu-id="6fbb7-293">List of useful commands</span></span>
| <span data-ttu-id="6fbb7-294">Tür</span><span class="sxs-lookup"><span data-stu-id="6fbb7-294">Type</span></span> | <span data-ttu-id="6fbb7-295">Komut</span><span class="sxs-lookup"><span data-stu-id="6fbb7-295">Command</span></span> | <span data-ttu-id="6fbb7-296">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6fbb7-296">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6fbb7-297">**iSCSI**</span><span class="sxs-lookup"><span data-stu-id="6fbb7-297">**iSCSI**</span></span> |`service iscsid start` |<span data-ttu-id="6fbb7-298">İSCSI Hizmeti</span><span class="sxs-lookup"><span data-stu-id="6fbb7-298">Start iSCSI service</span></span> |
| &nbsp; |`service iscsid stop` |<span data-ttu-id="6fbb7-299">İSCSI hizmetini durdurun</span><span class="sxs-lookup"><span data-stu-id="6fbb7-299">Stop iSCSI service</span></span> |
| &nbsp; |`service iscsid restart` |<span data-ttu-id="6fbb7-300">İSCSI hizmetini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="6fbb7-300">Restart iSCSI service</span></span> |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |<span data-ttu-id="6fbb7-301">Belirtilen hello kullanılabilir hedeflerde Bul adresi</span><span class="sxs-lookup"><span data-stu-id="6fbb7-301">Discover available targets on hello specified address</span></span> |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |<span data-ttu-id="6fbb7-302">Toohello iSCSI hedef oturum</span><span class="sxs-lookup"><span data-stu-id="6fbb7-302">Log in toohello iSCSI target</span></span> |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |<span data-ttu-id="6fbb7-303">Merhaba iSCSI hedefi Oturumu Kapat</span><span class="sxs-lookup"><span data-stu-id="6fbb7-303">Log out from hello iSCSI target</span></span> |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |<span data-ttu-id="6fbb7-304">İSCSI Başlatıcı adı yazdırma</span><span class="sxs-lookup"><span data-stu-id="6fbb7-304">Print iSCSI initiator name</span></span> |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |<span data-ttu-id="6fbb7-305">Merhaba iSCSI oturumu ve hello konakta bulunan birim Hello durumunu denetleyin</span><span class="sxs-lookup"><span data-stu-id="6fbb7-305">Check hello state of hello iSCSI session and volume discovered on hello host</span></span> |
| &nbsp; |`iscsi –m session` |<span data-ttu-id="6fbb7-306">Merhaba StorSimple cihazı Hello konak arasında kurulan tüm hello iSCSI oturumları gösterir</span><span class="sxs-lookup"><span data-stu-id="6fbb7-306">Shows all hello iSCSI sessions established between hello host and hello StorSimple device</span></span> |
|  | | |
| <span data-ttu-id="6fbb7-307">**Çoklu yol oluşturma**</span><span class="sxs-lookup"><span data-stu-id="6fbb7-307">**Multipathing**</span></span> |`service multipathd start` |<span data-ttu-id="6fbb7-308">Çok yollu arka plan programı Başlat</span><span class="sxs-lookup"><span data-stu-id="6fbb7-308">Start multipath daemon</span></span> |
| &nbsp; |`service multipathd stop` |<span data-ttu-id="6fbb7-309">Çok yollu arka plan programı durdurun</span><span class="sxs-lookup"><span data-stu-id="6fbb7-309">Stop multipath daemon</span></span> |
| &nbsp; |`service multipathd restart` |<span data-ttu-id="6fbb7-310">Çok yollu arka plan programı yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="6fbb7-310">Restart multipath daemon</span></span> |
| &nbsp; |`chkconfig multipathd on` </br> <span data-ttu-id="6fbb7-311">OR</span><span class="sxs-lookup"><span data-stu-id="6fbb7-311">OR</span></span> </br> `mpathconf –with_chkconfig y` |<span data-ttu-id="6fbb7-312">Çok yollu arka plan programı toostart önyükleme sırasında etkinleştir</span><span class="sxs-lookup"><span data-stu-id="6fbb7-312">Enable multipath daemon toostart at boot time</span></span> |
| &nbsp; |`multipathd –k` |<span data-ttu-id="6fbb7-313">Sorun giderme için hello etkileşimli konsolunu başlatın</span><span class="sxs-lookup"><span data-stu-id="6fbb7-313">Start hello interactive console for troubleshooting</span></span> |
| &nbsp; |`multipath –l` |<span data-ttu-id="6fbb7-314">Liste çok yollu bağlantıları ve cihazlar</span><span class="sxs-lookup"><span data-stu-id="6fbb7-314">List multipath connections and devices</span></span> |
| &nbsp; |`mpathconf --enable` |<span data-ttu-id="6fbb7-315">Bir örnek mulitpath.conf dosya oluşturma`/etc/mulitpath.conf`</span><span class="sxs-lookup"><span data-stu-id="6fbb7-315">Create a sample mulitpath.conf file in `/etc/mulitpath.conf`</span></span> |
|  | | |

## <a name="next-steps"></a><span data-ttu-id="6fbb7-316">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6fbb7-316">Next steps</span></span>
<span data-ttu-id="6fbb7-317">Linux ana bilgisayarına MPIO yapılandırma gibi CentoS 6.6 belgeleri aşağıdaki toorefer toohello de gerekebilir:</span><span class="sxs-lookup"><span data-stu-id="6fbb7-317">As you are configuring MPIO on Linux host, you may also need toorefer toohello following CentoS 6.6 documents:</span></span>

* [<span data-ttu-id="6fbb7-318">CentOS MPIO ayarlama</span><span class="sxs-lookup"><span data-stu-id="6fbb7-318">Setting up MPIO on CentOS</span></span>](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [<span data-ttu-id="6fbb7-319">Linux eğitim Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="6fbb7-319">Linux Training Guide</span></span>](http://linux-training.be/files/books/LinuxAdm.pdf)

