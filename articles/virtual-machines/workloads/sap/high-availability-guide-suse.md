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
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a>SUSE Linux Enterprise Server üzerinde Azure vm'lerinde SAP NetWeaver SAP uygulamalar için yüksek kullanılabilirlik

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

Bu makalede nasıl toodeploy hello sanal makineler, hello sanal makineleri yapılandırma, hello küme Framework'ü yüklemek ve yüksek oranda kullanılabilir bir SAP NetWeaver 7.50 sistemi yükleyin açıklanmaktadır.
Merhaba örnek yapılandırmaları, vb. yükleme komutları. ASCS örnek numarasını 00, ERS örnek numarasını 02 ve SAP sistem kimliği NWS kullanılır. Merhaba hello örnekte hello kaynakların (örneğin, sanal makineler, sanal ağlar) adları hello kullandığınızı varsayar [şablonu Yakınsanan] [ template-converged] SAP sistem kimliği NWS toocreate hello kaynaklara sahip.

SAP notlar ve incelemeleri önce aşağıdaki hello okuma

* SAP Not [1928533], sahip olduğu:
  * SAP yazılım hello dağıtımı için desteklenen Azure VM boyutlarını listesi
  * Azure VM boyutlarını önemli kapasite bilgilerini
  * Desteklenen bir SAP yazılım ve işletim sistemi (OS) ve veritabanı birleşimler
  * Windows ve Microsoft Azure Linux için gerekli SAP çekirdek sürümü

* SAP Not [2015553] azure'da SAP desteklenen SAP yazılım dağıtımları için önkoşulları listeler.
* SAP Not [2205917] SUSE Linux Enterprise Server işletim sistemi ayarlarını SAP uygulamaları için önerilir
* SAP Not [1944799] SAP HANA yönergeleri SUSE Linux Enterprise Server için SAP uygulamaları için vardır.
* SAP Not [2178632] ayrıntılı Azure SAP için bildirilen tüm izleme ölçümleri hakkında bilgi sağlanmıştır.
* SAP Not [2191498] hello Azure Linux için SAP konak Aracısı sürümünü istedi.
* SAP Not [2243692] Linux Azure üzerinde SAP lisanslama hakkında bilgi vardır.
* SAP Not [1984787] SUSE Linux Enterprise Server 12 hakkında genel bilgi yer almaktadır.
* SAP Not [1999351] hello Azure Gelişmiş izleme uzantısı SAP için ek sorun giderme bilgileri içeriyor.
* [SAP topluluk WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) SAP notları Linux için gerekli tüm sahiptir.
* [Azure sanal makineleri planlama ve uygulama Linux üzerinde SAP için][planning-guide]
* [(Bu makalede) Linux'ta SAP için Azure sanal makineler dağıtımı][deployment-guide]
* [Linux üzerinde SAP için Azure sanal makineleri DBMS dağıtımı][dbms-guide]
* [Senaryo SAP HANA SR performansı en iyi duruma getirilmiş][suse-hana-ha-guide]  
  SAP HANA sistem çoğaltma yerinde tüm gerekli bilgileri tooset Hello kılavuz içerir. Bu kılavuz, bir taban çizgisi olarak kullanın.
* [Yüksek oranda kullanılabilir NFS depolama DRBD ve Pacemaker] [ suse-drbd-guide] Başlangıç Kılavuzu, tüm gerekli bilgileri tooset yüksek oranda kullanılabilir bir NFS sunucusu içerir. Bu kılavuz, bir taban çizgisi olarak kullanın.


## <a name="overview"></a>Genel Bakış

tooachieve yüksek kullanılabilirlik, SAP NetWeaver, bir NFS sunucusunun gerektirir. Merhaba NFS sunucusu ayrı bir kümede yapılandırılmış ve birden çok SAP sistemleri tarafından kullanılabilir.

![SAP NetWeaver yüksek kullanılabilirlik genel bakış](./media/high-availability-guide-suse/img_001.png)

Merhaba NFS sunucusu, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS ve hello SAP HANA veritabanına sanal ana bilgisayar adı ve sanal IP adresleri kullanın. Azure üzerinde bir yük dengeleyici sanal IP adresi gerekli toouse ' dir. Merhaba aşağıdaki liste hello yük dengeleyici hello yapılandırmasını gösterir.

### <a name="nfs-server"></a>NFS sunucusu
* Ön uç yapılandırma
  * IP adresi 10.0.0.4
* Arka uç yapılandırması
  * Tooprimary ağ arabirimleri hello NFS kümesinin parçası olması gereken tüm sanal makinelerin bağlı
* Sonda bağlantı noktası
  * Bağlantı noktası 61000
* Loadbalancing kuralları
  * 2049 TCP 
  * 2049 UDP

### <a name="ascs"></a>(A) SCS
* Ön uç yapılandırma
  * IP adresi 10.0.0.10
* Arka uç yapılandırması
  * Merhaba (A) SCS/ERS kümesinin parçası olması gereken tüm sanal makinelerin bağlı tooprimary ağ arabirimleri
* Sonda bağlantı noktası
  * Bağlantı noktası 620**&lt;n&gt;**
* Loadbalancing kuralları
  * 32**&lt;n&gt;**  TCP
  * 36**&lt;n&gt;**  TCP
  * 39**&lt;n&gt;**  TCP
  * 81**&lt;n&gt;**  TCP
  * 5**&lt;n&gt;**13 TCP
  * 5**&lt;n&gt;**14 TCP
  * 5**&lt;n&gt;**16 TCP

### <a name="ers"></a>ERS
* Ön uç yapılandırma
  * IP adresi 10.0.0.11
* Arka uç yapılandırması
  * Merhaba (A) SCS/ERS kümesinin parçası olması gereken tüm sanal makinelerin bağlı tooprimary ağ arabirimleri
* Sonda bağlantı noktası
  * Bağlantı noktası 621**&lt;n&gt;**
* Loadbalancing kuralları
  * 33**&lt;n&gt;**  TCP
  * 5**&lt;n&gt;**13 TCP
  * 5**&lt;n&gt;**14 TCP
  * 5**&lt;n&gt;**16 TCP

### <a name="sap-hana"></a>SAP HANA
* Ön uç yapılandırma
  * IP adresi 10.0.0.12
* Arka uç yapılandırması
  * Merhaba HANA kümesinin parçası olması gereken tüm sanal makinelerin tooprimary ağ arabirimleri bağlı
* Sonda bağlantı noktası
  * Bağlantı noktası 625**&lt;n&gt;**
* Loadbalancing kuralları
  * 3**&lt;n&gt;**15 TCP
  * 3**&lt;n&gt;**17 TCP

## <a name="setting-up-a-highly-available-nfs-server"></a>Yüksek oranda kullanılabilir bir NFS sunucusu kurma

### <a name="deploying-linux"></a>Linux dağıtma

Hello Azure Market görüntü için SAP uygulamaları toodeploy yeni sanal makineleri kullanabilir 12 SUSE Linux Enterprise Server içerir.
Merhaba hızlı başlangıç şablonlarından birini github toodeploy üzerinde gerekli tüm kaynakları kullanabilir. Merhaba şablon hello sanal makineler, hello yük dengeleyici, kullanılabilirlik vb. kümesi dağıtır. Bu adımları toodeploy hello şablon izleyin:

1. Açık hello [SAP dosya sunucusu şablonu] [ template-file-server] hello Azure portal'ın   
1. Şu parametreler hello girin
   1. Kaynak öneki  
      Toouse istediğiniz hello öneki girin. Merhaba değer dağıtılan hello kaynaklar için önek olarak kullanılır.
   2. İşletim sistemi türü  
      Merhaba Linux dağıtımları birini seçin. Bu örnekte, SLES 12 seçin
   3. Yönetici kullanıcı adı ve yönetici parolası  
      Yeni bir kullanıcı oluşturulur toohello makinede kullanılan toolog olabilir.
   4. Alt ağ kimliği  
      için Hello kimliği hello alt toowhich hello sanal makinelerin bağlanması gerekir. Yeni bir sanal ağ toocreate istediğiniz ya da VPN veya hızlı rota sanal ağ tooconnect hello sanal makine tooyour Şirket ağınızın hello alt ağ seçin, boş bırakın. Merhaba kimliği genellikle /subscriptions/ gibi görünüyor**&lt;abonelik kimliği&gt;**/resourceGroups/**&lt;kaynak grubu adı&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;sanal ağ adı&gt;**/subnets/**&lt;alt ağ adı&gt;**

### <a name="installation"></a>Yükleme

Merhaba aşağıdaki öğeleri ile ya da önek **[A]** -geçerli tooall düğümleri **[1]** -yalnızca geçerli toonode 1 veya **[2]** -yalnızca geçerli toonode 2.

1. **[A]**  SLES güncelleştir

   <pre><code>
   sudo zypper update
   </code></pre>

1. **[1]**  Ssh erişimini etkinleştirme

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. **[2]**  Ssh erişimini etkinleştirme

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

1. **[1]**  Ssh erişimini etkinleştirme

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. **[A]**  Yükleme HA uzantısı
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. **[A]**  Kurulum ana bilgisayar adı çözümlemesi   

   Bir DNS sunucusu kullanın veya tüm düğümlerde hello/etc/hosts değiştirin. Bu örnek nasıl toouse hello/etc/hosts dosyasını gösterir.
   Başlangıç IP adresi ve hello hostname komutları aşağıdaki hello olarak değiştirin

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   Aşağıdaki satırları çok/etc/hosts hello ekleyin. Başlangıç IP adresi ve ana bilgisayar adı toomatch ortamınızı değiştirme   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. **[1]**  Küme yükleyin
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. **[2]**  Düğüm toocluster Ekle
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. **[A]**  Değişiklik hacluster parola toohello aynı parola

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. **[A]**  Corosync toouse diğer aktarım yapılandırmak ve listesi ekleyin. Aksi takdirde, küme çalışmaz.
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   Merhaba aşağıdaki kalın içerik toohello dosyasına ekleyin.
   
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

   Merhaba corosync hizmetini yeniden başlatın

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. **[A]**  Drbd bileşenlerini yükleme

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. **[A]**  Hello drbd cihaz için bir bölüm oluşturun

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. **[A]**  LVM oluşturma yapılandırmaları

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. **[A]**  Oluşturma hello NFS drbd aygıt

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   Merhaba yeni drbd aygıt ve çıkış Hello Yapılandırması Ekle

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

   Merhaba drbd aygıtı oluşturun ve başlatın

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. **[1]**  Atla ilk eşitleme

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. **[1]**  Kümesi hello birincil düğüm

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. **[1]**  Hello yeni drbd aygıtları eşitlenir kadar bekleyin

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. **[1]**  Dosya sistemleri üzerinde hello drbd aygıtları oluşturun.

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a>Küme çerçeve Yapılandır

1. **[1]**  Hello varsayılan ayarları değiştir

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Ekle hello NFS drbd aygıt toohello küme yapılandırması

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

1. **[1]**  Oluşturma hello NFS sunucusu

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Hello NFS dosya sistemi kaynakları oluşturun

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

1. **[1]**  Oluşturma hello NFS dışarı aktarma

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

1. **[1]**  Bir sanal IP kaynak ve sistem durumu araştırması hello iç yük dengeleyici için oluşturma

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

### <a name="create-stonith-device"></a>STONITH cihaz oluşturma

Merhaba STONITH aygıt Microsoft Azure karşı bir hizmet sorumlusu tooauthorize kullanır. Bu adımları toocreate bir hizmet sorumlusu izleyin.

1. Çok Git<https://portal.azure.com>
1. Açık hello Azure Active Directory dikey penceresi  
   TooProperties gidin ve dizin kimliği hello yazma Merhaba budur **Kiracı kimliği**.
1. Uygulama kayıtlar'ı tıklatın
1. Ekle'ye tıklayın.
1. Bir ad girin, uygulama türü "Web uygulaması/API" seçin, bir oturum açma URL'si (örneğin http://localhost) girin ve Oluştur'u tıklatın
1. Merhaba oturum açma URL'si kullanılmaz ve geçerli bir URL olabilir
1. Select hello yeni uygulama ve anahtarları hello ayarları sekmesini tıklatın
1. Yeni bir anahtar için bir açıklama girin, "Her zaman geçerli olsun" seçin ve Kaydet
1. Değer Hello yazın. Hello kullanılan **parola** hello hizmet sorumlusu için
1. Uygulama Kimliği Hello yazma Kullanıcı adı hello olarak kullanılan (**oturum açma kimliği** hello adımlarda aşağıdaki) hello hizmet sorumlusu,

Merhaba hizmet asıl izinleri tooaccess varsayılan olarak Azure kaynaklarınızı yok. Toogive hello hizmet asıl izinleri toostart gerekir ve durdurun (deallocate) hello kümenin tüm sanal makineler.

1. Toohttps://Portal.Azure.com gidin
1. Açık hello tüm kaynak dikey penceresi
1. Merhaba sanal makineyi seçin
1. Erişim denetimi (IAM) tıklatın
1. Ekle'ye tıklayın.
1. Merhaba rol sahibi seçin
1. Merhaba, yukarıda oluşturduğunuz Merhaba uygulaması adını girin
1. Tamam'ı tıklatın

#### <a name="1-create-hello-stonith-devices"></a>**[1]**  Hello STONITH aygıtları oluşturun

Merhaba izinleri hello sanal makineler için düzenlenebilir sonra hello kümede hello STONITH cihazları yapılandırabilirsiniz.

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

#### <a name="1-enable-hello-use-of-a-stonith-device"></a>**[1]**  STONITH aygıtın hello kullanımını etkinleştir

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a>(A) SCS ayarlama

### <a name="deploying-linux"></a>Linux dağıtma

Hello Azure Market görüntü için SAP uygulamaları toodeploy yeni sanal makineleri kullanabilir 12 SUSE Linux Enterprise Server içerir. Merhaba Market görüntüsü için SAP NetWeaver hello kaynak aracısı içerir.

Merhaba hızlı başlangıç şablonlarından birini github toodeploy üzerinde gerekli tüm kaynakları kullanabilir. Merhaba şablon hello sanal makineler, hello yük dengeleyici, kullanılabilirlik vb. kümesi dağıtır. Bu adımları toodeploy hello şablon izleyin:

1. Açık hello [ASCS/SCS çoklu SID şablonu] [ template-multisid-xscs] veya hello [şablonu Yakınsanan] [ template-converged] hello Azure portal hello ASCS/SCS şablonunda yalnızca Merhaba yakınsanmış şablon de (örneğin, Microsoft SQL Server veya SAP HANA) bir veritabanı için hello Yük Dengeleme kuralları oluşturur ancak hello Yük Dengeleme kuralları hello SAP NetWeaver ASCS/SCS ve ERS (yalnızca Linux) örnekleri için oluşturur. Tooinstall bir SAP NetWeaver temel sistem planlama ve ayrıca tooinstall hello veritabanı istiyorsanız üzerinde Merhaba aynı makineler, hello kullan [şablonu Yakınsanan][template-converged].
1. Şu parametreler hello girin
   1. Kaynak önek (yalnızca ASCS/SCS çoklu SID şablonu)  
      Toouse istediğiniz hello öneki girin. Merhaba değer dağıtılan hello kaynaklar için önek olarak kullanılır.
   3. SAP sistem kimliği (yalnızca yakınsanmış şablonu)  
      Merhaba tooinstall istediğiniz SAP sistemi Hello SAP sistemi kimliği girin. Merhaba kimliği önek olarak dağıtılan hello kaynaklar için kullanılır.
   4. Yığın türü  
      Merhaba SAP NetWeaver yığın türünü seçin
   5. İşletim sistemi türü  
      Merhaba Linux dağıtımları birini seçin. Bu örnekte, SLES 12 BYOS seçin
   6. DB türü  
      HANA seçin
   7. SAP sistemi boyutu  
      SAP hello yeni sistem Hello miktarını sağlar. SAP teknolojisi iş ortağı veya sistem Tümleştirici kaç SAP hello sistemi gerektirir emin değilseniz Lütfen isteyin
   8. Sistem kullanılabilirliği  
      HA seçin
   9. Yönetici kullanıcı adı ve yönetici parolası  
      Yeni bir kullanıcı oluşturulur toohello makinede kullanılan toolog olabilir.
   10. Alt ağ kimliği  
   için Hello kimliği hello alt toowhich hello sanal makinelerin bağlanması gerekir.  Kullanılan veya hello NFS sunucu dağıtımının bir parçası oluşturulan aynı alt ağ seçin hello ya da yeni bir sanal ağ toocreate istiyorsanız boş bırakın. Merhaba kimliği genellikle /subscriptions/ gibi görünüyor**&lt;abonelik kimliği&gt;**/resourceGroups/**&lt;kaynak grubu adı&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;sanal ağ adı&gt;**/subnets/**&lt;alt ağ adı&gt;**

### <a name="installation"></a>Yükleme

Merhaba aşağıdaki öğeleri ile ya da önek **[A]** -geçerli tooall düğümleri **[1]** -yalnızca geçerli toonode 1 veya **[2]** -yalnızca geçerli toonode 2.

1. **[A]**  SLES güncelleştir

   <pre><code>
   sudo zypper update
   </code></pre>

1. **[1]**  Ssh erişimini etkinleştirme

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. **[2]**  Ssh erişimini etkinleştirme

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

1. **[1]**  Ssh erişimini etkinleştirme

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. **[A]**  Yükleme HA uzantısı
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. **[A]**  Güncelleştirme SAP kaynak aracıları  
   
   Merhaba kaynak aracıları paket için bir düzeltme eki gerekli toouse hello bu makalede açıklanan yeni yapılandırma, ' dir. Merhaba düzeltme eki komutu aşağıdaki hello ile zaten yüklüyse, kontrol edebilirsiniz

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   Merhaba çıktısı benzer olmalıdır

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   Hello grep komutu hello IS_ERS parametresi bulamazsa, listelenen tooinstall hello düzeltme eki gereksinim [hello SUSE indirme sayfası](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. **[A]**  Kurulum ana bilgisayar adı çözümlemesi   

   Bir DNS sunucusu kullanın veya tüm düğümlerde hello/etc/hosts değiştirin. Bu örnek nasıl toouse hello/etc/hosts dosyasını gösterir.
   Başlangıç IP adresi ve hello hostname komutları aşağıdaki hello olarak değiştirin

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   Aşağıdaki satırları çok/etc/hosts hello ekleyin. Başlangıç IP adresi ve ana bilgisayar adı toomatch ortamınızı değiştirme   
   
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

1. **[1]**  Küme yükleyin
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. **[2]**  Düğüm toocluster Ekle
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. **[A]**  Değişiklik hacluster parola toohello aynı parola

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. **[A]**  Corosync toouse diğer aktarım yapılandırmak ve listesi ekleyin. Aksi takdirde, küme çalışmaz.
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   Merhaba aşağıdaki kalın içerik toohello dosyasına ekleyin.
   
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

   Merhaba corosync hizmetini yeniden başlatın

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. **[A]**  Drbd bileşenlerini yükleme

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. **[A]**  Hello drbd cihaz için bir bölüm oluşturun

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. **[A]**  LVM oluşturma yapılandırmaları

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. **[A]**  Oluşturma hello SCS drbd aygıt

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   Merhaba yeni drbd aygıt ve çıkış Hello Yapılandırması Ekle

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

   Merhaba drbd aygıtı oluşturun ve başlatın

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. **[A]**  Oluşturma hello ERS drbd aygıt

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   Merhaba yeni drbd aygıt ve çıkış Hello Yapılandırması Ekle

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

   Merhaba drbd aygıtı oluşturun ve başlatın

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. **[1]**  Atla ilk eşitleme

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. **[1]**  Kümesi hello birincil düğüm

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. **[1]**  Hello yeni drbd aygıtları eşitlenir kadar bekleyin

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

1. **[1]**  Dosya sistemleri üzerinde hello drbd aygıtları oluşturun.

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a>Küme çerçeve Yapılandır

**[1]**  Hello varsayılan ayarları değiştir

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a>SAP NetWeaver yükleme için hazırlama

1. **[A]**  Oluşturma hello paylaşılan dizinler

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. **[A]**  Autofs yapılandırın
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   Dosya Oluştur

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   AutoFS toomount hello yeni paylaşımlar yeniden başlatın

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. **[A]**  Yapılandırma TAKAS dosyası
 
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

   Merhaba Aracısı tooactivate hello değişiklik yeniden başlatın

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a>SAP NetWeaver ASCS/ERS yükleme

1. **[1]**  Bir sanal IP kaynak ve sistem durumu araştırması hello iç yük dengeleyici için oluşturma

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

   Merhaba küme durumunun Tamam olduğunu ve tüm kaynakları başlatıldığından emin olun. Hangi düğümün hello kaynaklar üzerinde çalışan önemli değildir.

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

1. **[1]**  SAP NetWeaver ASCS yükleyin  

   SAP NetWeaver ASCS toohello IP adresi yapılandırmasının hello yük dengeleyici ön uç hello ASCS için örneğin eşleşen bir sanal ana bilgisayar adı kullanarak hello ilk düğümde kök Yükle <b>nws ascs</b>, <b>10.0.0.10</b>ve örneğin hello hello yük dengeleyici araştırması için kullanılan hello örnek numarasını <b>00</b>.

   Merhaba sapinst parametresi SAPINST_REMOTE_ACCESS_USER tooallow kök olmayan kullanıcı tooconnect toosapinst kullanabilirsiniz.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. **[1]**  Bir sanal IP kaynak ve sistem durumu araştırması hello iç yük dengeleyici için oluşturma

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
 
   Merhaba küme durumunun Tamam olduğunu ve tüm kaynakları başlatıldığından emin olun. Hangi düğümün hello kaynaklar üzerinde çalışan önemli değildir.

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

1. **[2]**  SAP NetWeaver ERS yükleyin  

   SAP NetWeaver ERS hello yük dengeleyici ön uç yapılandırmasında hello ERS toohello IP adresini örneğin eşleşen bir sanal ana bilgisayar adı kullanarak hello ikinci düğümde kök Yükle <b>nws ers</b>, <b>10.0.0.11</b> ve örneğin hello hello yük dengeleyici araştırması için kullanılan hello örnek numarasını <b>02</b>.

   Merhaba sapinst parametresi SAPINST_REMOTE_ACCESS_USER tooallow kök olmayan kullanıcı tooconnect toosapinst kullanabilirsiniz.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > Lütfen SWPM SP 20 PL 05 ya da daha yüksek kullanın. Daha düşük sürümleri hello izinleri düzgün ayarlanmamış ve hello yükleme başarısız olur.
   > 

1. **[1]**  Hello ASCS/SCS ve ERS örneği profilleri uyarlama
 
   * ASCS/SCS profili

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

   * ERS profili

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. **[A]**  Tutmayı yapılandırma

   Merhaba ASCS/SCS hello SAP NetWeaver uygulama sunucusu arasındaki Hello iletişimi yazılım yük dengeleyici yönlendirilir. Merhaba yük dengeleyici yapılandırılabilir bir zaman aşımından sonra etkin olmayan bağlantıları bağlantısını keser. tooprevent bu tooset hello SAP NetWeaver ASCS/SCS profili parametresinde gerekir ve hello Linux sistem ayarlarını değiştirebilir. Lütfen okuyun [SAP Not 1410736] [ 1410736] daha fazla bilgi için.
   
   Merhaba ASCS/SCS profili parametre CLR'yi/encni/set_so_keepalive hello son adımda zaten eklendi.

   <pre><code> 
   # Change hello Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. **[A]**  Hello yüklendikten sonra hello SAP kullanıcıları yapılandırın
 
   <pre><code>
   # Add sidadm toohello haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. **[1]**  Hello ASCS ve ERS SAP Hizmetleri toohello sapservice Dosya Ekle

   Merhaba ASCS hizmet girişi toohello ikinci düğümü ve kopyalama hello ERS hizmet girişi toohello ilk düğümü ekleyin.

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. **[1]**  Hello SAP küme kaynakları oluşturun

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

   Merhaba küme durumunun Tamam olduğunu ve tüm kaynakları başlatıldığından emin olun. Hangi düğümün hello kaynaklar üzerinde çalışan önemli değildir.

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

### <a name="create-stonith-device"></a>STONITH cihaz oluşturma

Merhaba STONITH aygıt Microsoft Azure karşı bir hizmet sorumlusu tooauthorize kullanır. Bu adımları toocreate bir hizmet sorumlusu izleyin.

1. Çok Git<https://portal.azure.com>
1. Açık hello Azure Active Directory dikey penceresi  
   TooProperties gidin ve dizin kimliği hello yazma Merhaba budur **Kiracı kimliği**.
1. Uygulama kayıtlar'ı tıklatın
1. Ekle'ye tıklayın.
1. Bir ad girin, uygulama türü "Web uygulaması/API" seçin, bir oturum açma URL'si (örneğin http://localhost) girin ve Oluştur'u tıklatın
1. Merhaba oturum açma URL'si kullanılmaz ve geçerli bir URL olabilir
1. Select hello yeni uygulama ve anahtarları hello ayarları sekmesini tıklatın
1. Yeni bir anahtar için bir açıklama girin, "Her zaman geçerli olsun" seçin ve Kaydet
1. Değer Hello yazın. Hello kullanılan **parola** hello hizmet sorumlusu için
1. Uygulama Kimliği Hello yazma Kullanıcı adı hello olarak kullanılan (**oturum açma kimliği** hello adımlarda aşağıdaki) hello hizmet sorumlusu,

Merhaba hizmet asıl izinleri tooaccess varsayılan olarak Azure kaynaklarınızı yok. Toogive hello hizmet asıl izinleri toostart gerekir ve durdurun (deallocate) hello kümenin tüm sanal makineler.

1. Toohttps://Portal.Azure.com gidin
1. Açık hello tüm kaynak dikey penceresi
1. Merhaba sanal makineyi seçin
1. Erişim denetimi (IAM) tıklatın
1. Ekle'ye tıklayın.
1. Merhaba rol sahibi seçin
1. Merhaba, yukarıda oluşturduğunuz Merhaba uygulaması adını girin
1. Tamam'ı tıklatın

#### <a name="1-create-hello-stonith-devices"></a>**[1]**  Hello STONITH aygıtları oluşturun

Merhaba izinleri hello sanal makineler için düzenlenebilir sonra hello kümede hello STONITH cihazları yapılandırabilirsiniz.

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

#### <a name="1-enable-hello-use-of-a-stonith-device"></a>**[1]**  STONITH aygıtın hello kullanımını etkinleştir

STONITH aygıt Hello kullanımını etkinleştirme

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a>Veritabanını yükleme

Bu örnekte bir SAP HANA sistem çoğaltma yüklenmiş ve yapılandırılmış. SAP HANA hello aynı küme hello SAP NetWeaver ASCS/SCS ve ERS çalıştırır. SAP HANA adanmış bir kümede de yükleyebilirsiniz. Bkz: [SAP HANA, yüksek kullanılabilirlik'Azure sanal makineler (VM'ler) üzerinde] [ sap-hana-ha] daha fazla bilgi için.

### <a name="prepare-for-sap-hana-installation"></a>SAP HANA yükleme için hazırlama

Genellikle, veri ve günlük dosyalarını birimleri için LVM kullanmanızı öneririz. Test amacıyla, doğrudan düz bir diskte toostore hello veri ve günlük dosyası da seçebilirsiniz.

1. **[A]**  LVM  
   Aşağıdaki Hello örnek hello sanal makineleri kullanılan toocreate iki birimlerin olmalıdır bağlı dört veri diskleri sahip olduğunuzu varsayar.
   
   Toouse istediğiniz tüm disklerin fiziksel birimler oluşturursunuz.
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   Merhaba veri dosyaları için bir birim grubu, hello günlük dosyaları için bir birim grubu ve SAP HANA hello paylaşılan dizini için bir tane oluşturun
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   Merhaba mantıksal birim oluşturun
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   Merhaba bağlama dizinler oluşturun ve hello UUID tüm mantıksal birimlerin kopyalama
   
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
   
   Merhaba AutoFS girişlerinde üç mantıksal birim oluşturma
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   Bu satırı toosudo VI /etc/auto.direct Ekle
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   Merhaba yeni birimleri bağlayın
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. **[A]**  Düz diskleri  

   Küçük veya gösteri sistemleri HANA veri ve günlük dosyalarınızı bir disk yerleştirin. Merhaba aşağıdaki komutları /dev/sdc üzerinde bir bölüm oluşturun ve xfs ile biçimlendirin.
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down hello id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   Bu satırı too/etc/auto.direct Ekle
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   Merhaba hedef dizin oluşturun ve hello diski bağlayabilir.
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a>SAP HANA yükleme

Merhaba aşağıdaki adımları hello bölüm 4 dayalı [SAP HANA SR performansı en iyi duruma getirilmiş senaryo Kılavuzu] [ suse-hana-ha-guide] tooinstall SAP HANA sistem çoğaltma. Lütfen hello yüklemeye devam etmeden önce bunu okuyun.

1. **[A]**  Hdblcm HANA DVD hello çalıştırın
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. **[A]**  Yükseltme SAP konak Aracısı

   Hello Hello son SAP konak Aracısı arşivi indir [SAP Softwarecenter] [ sap-swcenter] ve çalışma hello komutu tooupgrade hello aracısı aşağıdaki. Merhaba yolu toohello arşiv toopoint toohello dosyasını indirdiğiniz değiştirin.
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path tooSAP Host Agent SAR&gt;</b> 
   </code></pre>

1. **[1]**  (Kök) olarak oluşturma HANA çoğaltma  

   Merhaba aşağıdaki komutu çalıştırın. SAP HANA yüklemenizin hello değerlerle emin tooreplace kalın dizeleri (HANA sistem kimliği HDB ile örnek numarasını 03) olun.
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. **[A]**  (Kök) olarak bir anahtar girişi oluşturun

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. **[1]**  Backup database (kök) olarak

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. **[1]**  Geçiş toohello HANA sapsid kullanıcı ve hello birincil site oluşturun.

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. **[2]**  Toohello HANA sapsid kullanıcı geçin ve hello ikincil site oluştur.

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. **[1]**  Oluşturma SAP HANA küme kaynakları

   İlk olarak hello topoloji oluşturun.
   
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
   
   Ardından, hello HANA kaynakları oluşturun
   
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

   Merhaba küme durumunun Tamam olduğunu ve tüm kaynakları başlatıldığından emin olun. Hangi düğümün hello kaynaklar üzerinde çalışan önemli değildir.

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

1. **[1]**  Yükleme hello SAP NetWeaver veritabanı örneği

   Yükleme hello SAP NetWeaver veritabanı örneği örneğin toohello IP adresi yapılandırmasının hello yük dengeleyici ön uç hello veritabanı için eşleşen bir sanal ana bilgisayar adı kullanarak kök olarak <b>nws db</b> ve <b>10.0.0.12</b>.

   Merhaba sapinst parametresi SAPINST_REMOTE_ACCESS_USER tooallow kök olmayan kullanıcı tooconnect toosapinst kullanabilirsiniz.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a>SAP NetWeaver uygulama sunucusu yükleme

Bu adımları tooinstall SAP uygulama sunucusu izleyin. Merhaba adımları aşağıdaki varsayalım ASCS/SCS hello farklı bir sunucuda hello uygulama sunucusu ve HANA sunucularına yükleyin. Aksi takdirde (ana bilgisayar adı çözümlemesi yapılandırma gibi) hello adımları bazıları gerekli değildir.

1. Ana bilgisayar adı çözümlemesi Kurulumu    
   Bir DNS sunucusu kullanın veya tüm düğümlerde hello/etc/hosts değiştirin. Bu örnek nasıl toouse hello/etc/hosts dosyasını gösterir.
   Başlangıç IP adresi ve hello hostname komutları aşağıdaki hello olarak değiştirin
   ```bash
   sudo vi /etc/hosts
   ```
   Aşağıdaki satırları çok/etc/hosts hello ekleyin. Başlangıç IP adresi ve ana bilgisayar adı toomatch ortamınızı değiştirme    
    
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

1. Merhaba sapmnt dizin oluşturun

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. AutoFS yapılandırın
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   Yeni dosya oluştur

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   AutoFS toomount hello yeni paylaşımlar yeniden başlatın

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. TAKAS dosyasını yapılandırma
 
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

   Merhaba Aracısı tooactivate hello değişiklik yeniden başlatın

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. SAP NetWeaver uygulama sunucusu yükleme

   Bir birincil ya da ek SAP NetWeaver uygulamalar sunucusu yükleyin.

   Merhaba sapinst parametresi SAPINST_REMOTE_ACCESS_USER tooallow kök olmayan kullanıcı tooconnect toosapinst kullanabilirsiniz.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. SAP HANA güvenli depolama güncelleştir

   Güncelleştirme hello SAP HANA güvenli toopoint toohello sanal adını hello SAP HANA sistem çoğaltma Kurulum depolar.
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a>Sonraki adımlar
* [Azure sanal makineleri planlama ve uygulama SAP için][planning-guide]
* [SAP için Azure sanal makineler dağıtımı][deployment-guide]
* [SAP için Azure sanal makineleri DBMS dağıtımı][dbms-guide]
* tooestablish yüksek kullanılabilirlik ve olağanüstü durum kurtarma SAP HANA planlama (büyük örnekler), azure'da nasıl görürüm toolearn [SAP HANA (büyük örnekler) Azure üzerinde yüksek kullanılabilirlik ve olağanüstü durum kurtarma](hana-overview-high-availability-disaster-recovery.md).
* tooestablish yüksek kullanılabilirlik ve olağanüstü durum kurtarma SAP HANA planlama Azure vm'lerinde nasıl görürüm toolearn [SAP HANA, yüksek kullanılabilirlik Azure Virtual Machines'de (VM'ler)][sap-hana-ha]
