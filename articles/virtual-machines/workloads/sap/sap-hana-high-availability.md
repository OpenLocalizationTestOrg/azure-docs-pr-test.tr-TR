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
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a>SAP HANA Azure sanal makinelerde (VM), yüksek kullanılabilirlik

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

Şirket içi ya da HANA sistemi çoğaltması kullanmak veya paylaşılan depolama tooestablish yüksek kullanılabilirlik için SAP HANA kullanın.
Şu anda yalnızca HANA sistem çoğaltma ayarlama Azure üzerinde destekliyoruz. SAP HANA çoğaltma, bir yönetici düğümü ve en az bir ikincil düğüm oluşur. Merhaba ana düğüm üzerinde veri olan değişiklikleri toohello toohello bağımlı düğümleri eşzamanlı veya zaman uyumsuz olarak çoğaltılan.

Bu makalede toodeploy hello sanal makineler, hello sanal makineleri yapılandırma, hello küme Framework'ü yüklemek, yüklemek ve nasıl SAP HANA sistem çoğaltma yapılandırma açıklanmaktadır.
Merhaba örnek yapılandırmaları, vb. örnek numarasını 03 yükleme komutları ve HANA sistem kimliği HDB kullanılır.

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
* [SAP HANA SR performansı en iyi duruma getirilmiş senaryo] [ suse-hana-ha-guide] hello Kılavuzu, şirket içinde için SAP HANA sistem çoğaltma tüm gerekli bilgileri tooset içerir. Bu kılavuz, bir taban çizgisi olarak kullanın.

## <a name="deploying-linux"></a>Linux dağıtma

SAP HANA Hello kaynak Aracısı SUSE Linux Enterprise Server SAP uygulamaları için dahil edilir.
Hello Azure Market görüntü SUSE Linux Enterprise Server için SAP uygulamaları 12 BYOS toodeploy yeni sanal makineler kullanabilirsiniz (Getir bilgisayarınızı kendi abonelik) ile içerir.

### <a name="manual-deployment"></a>El ile dağıtımı

1. Kaynak Grubu oluşturma
1. Bir sanal ağ oluşturma
1. İki depolama hesabı oluşturma
1. Kullanılabilirlik kümesi oluştur  
   Set max güncelleştirme etki alanı
1. Bir yük dengeleyiciye (dahili) oluşturma  
   Yukarıdaki adımı VNET seçin
1. Sanal makine 1 oluşturun  
   https://Portal.Azure.com/#Create/SuSE-byos.SLES-for-SAP-byos12-SP1  
   SAP uygulamaları 12 SP1 için SLES (BYOS)  
   1 depolama hesabı seçin  
   Kullanılabilirlik kümesi seçin  
1. Sanal makine 2 oluşturun  
   https://Portal.Azure.com/#Create/SuSE-byos.SLES-for-SAP-byos12-SP1  
   SAP uygulamaları 12 SP1 için SLES (BYOS)  
   Depolama hesabı 2 seçin   
   Kullanılabilirlik kümesi seçin  
1. Veri diski Ekle
1. Merhaba yük dengeleyici yapılandırma
    1. Bir ön uç IP havuzu oluşturma
        1. Açık hello yük dengeleyici, ön uç IP havuzu seçin ve Ekle'yi tıklatın
        1. Merhaba yeni ön uç IP havuzu (örneğin hana-ön uç) Hello adını girin
       1. Tamam'ı tıklatın
        1. Merhaba yeni ön uç IP havuzu oluşturulduktan sonra IP adresini yazma
    1. Arka uç havuzu oluşturma
        1. Açık hello yük dengeleyici arka uç havuzlarını seçin ve Ekle'yi tıklatın
        1. Merhaba yeni arka uç havuzu (örneğin hana-arka uç) Hello adını girin
        1. Bir sanal makine Ekle
        1. Merhaba daha önce oluşturduğunuz kullanılabilirlik kümesi seçin
        1. Merhaba SAP HANA kümesinin Hello sanal makineleri seçin
        1. Tamam'ı tıklatın
    1. Bir sistem durumu araştırması oluştur
       1. Açık hello yük dengeleyici, sistem durumu araştırmalarının seçin ve Ekle'yi tıklatın
        1. Merhaba yeni durumu araştırması (örneğin hana-hp) Hello adını girin
        1. TCP bağlantı noktası 625 protokolü olarak seçin**03**, aralığı 5 ile sağlıksız durum eşiği 2 tutun
        1. Tamam'ı tıklatın
    1. Yük dengeleme kuralları oluşturma
        1. Merhaba yük dengeleyici açın, Yük Dengeleme kuralları seçin ve Ekle'yi tıklatın
        1. Merhaba Yeni Yük Dengeleyici kuralı Hello adını girin (örneğin hana-lb-3**03**15)
        1. Daha önce oluşturduğunuz (örneğin hana-ön uç) araştırma SELECT hello ön uç IP adresi, arka uç havuzu ve sistem durumu
        1. Protokol TCP tutmak için bağlantı noktası 3 girin**03**15
        1. Boşta kalma zaman aşımı too30 dakika artırın
       1. **Emin tooenable olun kayan IP**
        1. Tamam'ı tıklatın
        1. Bağlantı noktası 3 için yukarıdaki Hello adımları yineleyin**03**17

### <a name="deploy-with-template"></a>Şablon ile dağıtım
Merhaba hızlı başlangıç şablonlarından birini github toodeploy üzerinde gerekli tüm kaynakları kullanabilir. Merhaba şablon hello sanal makineler, hello yük dengeleyici, kullanılabilirlik vb. kümesi dağıtır. Bu adımları toodeploy hello şablon izleyin:

1. Açık hello [veritabanı şablonu] [ template-multisid-db] veya hello [şablonu Yakınsanan] [ template-converged] hello Azure portalı üzerinde hello veritabanı şablonu yalnızca hello oluşturur. Merhaba yakınsanmış şablonu da oluşturur ancak bir veritabanı için Yük Dengeleme kuralları ASCS/SCS ve ERS (yalnızca Linux) örneği için Yük Dengeleme kuralları hello. Tooinstall bir SAP NetWeaver temel sistem planlama ve ayrıca tooinstall hello istiyorsanız ASCS/SCS hello üzerinde aynı örnek makinelerini kullanma hello [şablonu Yakınsanan][template-converged].
1. Şu parametreler hello girin
    1. SAP sistem kimliği  
       Merhaba tooinstall istediğiniz SAP sistemi Hello SAP sistemi kimliği girin. Merhaba kimliği önek olarak dağıtılan hello kaynaklar için kullanılır.
    1. Yığın türü (yalnızca hello yakınsanmış şablonu kullanıyorsanız geçerlidir)  
       Merhaba SAP NetWeaver yığın türünü seçin
    1. İşletim sistemi türü  
       Merhaba Linux dağıtımları birini seçin. Bu örnekte, SLES 12 BYOS seçin
    1. DB türü  
       HANA seçin
    1. SAP sistemi boyutu  
       SAP hello yeni sistem Hello miktarını sağlar. SAP teknolojisi iş ortağı veya sistem Tümleştirici kaç SAP hello sistem gerektirir emin değilseniz Lütfen isteyin
    1. Sistem kullanılabilirliği  
       HA seçin
    1. Yönetici kullanıcı adı ve yönetici parolası  
       Yeni bir kullanıcı oluşturulur toohello makinede kullanılan toolog olabilir.
    1. Yeni veya var olan bir alt ağ  
       Yeni sanal ağ ve alt oluşturulmalıdır ya da mevcut bir alt kullanılması gerektiğini belirler. Bağlı tooyour şirket içi ağ bir sanal ağ zaten varsa, varolan seçin.
    1. Alt ağ kimliği  
    için Hello kimliği hello alt toowhich hello sanal makinelerin bağlanması gerekir. VPN veya hızlı rota sanal ağ tooconnect hello sanal makine tooyour Şirket ağınızın Hello alt ağ seçin. Merhaba kimliği genellikle /subscriptions/ gibi görünüyor`<subscription id`> /resourceGroups/`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`>

## <a name="setting-up-linux-ha"></a>Ayarlama Linux HA

Aşağıdaki öğelerindeki hello ya da ile [A] - geçerli tooall düğümleri, [1] - 1 veya [2] yalnızca geçerli toonode - yalnızca geçerli toonode 2 öneki alır.

1. [A] SAP yalnızca - BYOS kaydetmek SLES toobe mümkün toouse hello depoları için SLES
1. [A] SLES SAP BYOS için yalnızca - genel bulut Modül Ekle
1. [A] güncelleştirme SLES
    ```bash
    sudo zypper update

    ```

1. [1] ssh erişimini etkinleştirme
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. [2] ssh erişimini etkinleştirme
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

1. [1] ssh erişimini etkinleştirme
    ```bash
    # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. [A] HA uzantısını yükleyin
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. [A] Kurulum disk düzeni
    1. LVM  
    Genellikle veri ve günlük dosyalarını birimlerin toouse LVM öneririz. Aşağıdaki Hello örnek hello sanal makineleri kullanılan toocreate iki birimlerin olmalıdır bağlı dört veri diskleri sahip olduğunuzu varsayar.
        * Toouse istediğiniz tüm disklerin fiziksel birimler oluşturursunuz.
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * Merhaba veri dosyaları için bir birim grubu, hello günlük dosyaları için bir birim grubu ve SAP HANA hello paylaşılan dizini için bir tane oluşturun
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * Merhaba mantıksal birim oluşturun
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * Merhaba bağlama dizinler oluşturun ve hello UUID tüm mantıksal birimlerin kopyalama
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * Merhaba fstab girişlerinde üç mantıksal birim oluşturma
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    Bu satırı çok/etc/fstab Ekle
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * Merhaba yeni birimleri bağlayın
    <pre><code>
    sudo mount -a
    </code></pre>
    1. Düz diskleri  
       Küçük veya gösteri sistemleri HANA veri ve günlük dosyalarınızı bir disk yerleştirin. Merhaba aşağıdaki komutları /dev/sdc üzerinde bir bölüm oluşturun ve xfs ile biçimlendirin.
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-hello-id-of-devsdc1"></a>/dev/sdc1 Hello kimliği yazma
    sudo/sbin/blkid sudo VI/etc/fstab
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

1. [A] tüm ana bilgisayarlar için ana bilgisayar adı çözümlemesi Kurulumu  
    Bir DNS sunucusu kullanın veya tüm düğümlerde hello/etc/hosts değiştirin. Bu örnek nasıl toouse hello/etc/hosts dosyasını gösterir.
   Başlangıç IP adresi ve hello hostname komutları aşağıdaki hello olarak değiştirin
    ```bash
    sudo vi /etc/hosts
    ```
    Aşağıdaki satırları çok/etc/hosts hello ekleyin. Başlangıç IP adresi ve ana bilgisayar adı toomatch ortamınızı değiştirme    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. [1] küme yükleyin
    ```bash
    sudo ha-cluster-init
    
    # Do you want toocontinue anyway? [y/N] -> y
    # Network address toobind too(e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish toouse SBD? [y/N] -> N
    # Do you wish tooconfigure an administration IP? [y/N] -> N
    ```
        
1. [2] düğüm toocluster Ekle
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured toostart at system boot.
    # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
    # Do you want toocontinue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. [A] değişiklik hacluster parola toohello aynı parola
    ```bash
    sudo passwd hacluster
    
    ```

1. [A] corosync toouse diğer aktarım yapılandırmak ve listesi ekleyin. Aksi takdirde, küme çalışmaz.
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

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
        ring0_addr:     < ip address of node 1 >
      }
      node {
        ring0_addr:     < ip address of node 2 > 
      } 
    }</b>
    logging {
      [...]
    </code></pre>

    Merhaba corosync hizmetini yeniden başlatın

    ```bash
    sudo service corosync restart
    
    ```

1. [A] HANA HA paket yüklemek için  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a>SAP HANA yükleme

Merhaba, Bölüm 4 izleyin [SAP HANA SR performansı en iyi duruma getirilmiş senaryo Kılavuzu] [ suse-hana-ha-guide] tooinstall SAP HANA sistem çoğaltma.

1. [A] hdblcm HANA DVD hello çalıştırın
    * Yüklemeyi seçin 1 ->
    * Yükleme -> için 1 ek bileşenleri seçin
    * Yükleme yolu [paylaşılan / hana /] girin: ENTER ->
    * Yerel ana bilgisayar adı [.] girin: ENTER ->
    * Tooadd diğer Konaklara toohello sistemin istiyor musunuz? (e/h) [n]: ENTER ->
    * SAP HANA sistem Kimliğini girin:<SID of HANA e.g. HDB>
    * Örnek [00] girin:   
  HANA örneği sayısı. Hello Azure şablonu kullanılan ya da yukarıdaki hello örnek ardından 03 kullanın
    * Veritabanı modunu seçin / dizin [1] girin: ENTER ->
    * Sistem kullanımı seçin / dizin [4] girin:  
  Merhaba sistem kullanımı seçin
    * Veri birimlerinin [/ data/hana/HDB] konumu girin: ENTER ->
    * Günlük birim [/ günlük/hana/HDB] konumu girin: ENTER ->
    * En fazla bellek ayırma kısıtlama? [n]: ENTER ->
    * '...' Ana bilgisayar için sertifika ana bilgisayar adını girin [...]: ENTER ->
    * SAP konak aracısı kullanıcısı (sapadm) parola girin:
    * SAP konak aracısı kullanıcısı (sapadm) parolayı onaylayın:
    * Sistem Yöneticisi (hdbadm) parola girin:
    * Sistem Yöneticisi (hdbadm) parolayı onaylayın:
    * Sistem Yöneticisi giriş dizini girin [/ usr/sap/HDB/giriş]: ENTER ->
    * Sistem Yöneticisi oturum açma kabuğu girin [/ bin/Paylaş]: ENTER ->
    * Sistem yöneticisinin kullanıcı kimliği [1001] girin: ENTER ->
    * Girin kimliği, kullanıcı grubu (sapsys) [79]: ENTER ->
    * Veritabanı kullanıcı (Sistem) parolasını girin:
    * Veritabanı kullanıcı (Sistem) parolayı onaylayın:
    * Sistem makine yeniden başlatıldıktan sonra yeniden başlatılsın mı? [n]: ENTER ->
    * Toocontinue istiyor musunuz? (e/h):  
  Merhaba Özet doğrulamak ve y toocontinue girin
1. [A] yükseltme SAP konak Aracısı  
  Hello Hello son SAP konak Aracısı arşivi indir [SAP Softwarecenter] [ sap-swcenter] ve çalışma hello komutu tooupgrade hello aracısı aşağıdaki. Merhaba yolu toohello arşiv toopoint toohello dosyasını indirdiğiniz değiştirin.
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path tooSAP Host Agent SAR>
    ```

1. [1] (kök olarak) HANA çoğaltma oluşturma  
    Merhaba aşağıdaki komutu çalıştırın. SAP HANA yüklemenizin hello değerlerle emin tooreplace kalın dizeleri (HANA sistem kimliği HDB ile örnek numarasını 03) olun.
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. [A] (kök olarak) bir anahtar girişi oluşturun
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. [1] yedek veritabanını (kök) olarak
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. [1] toohello sapsid kullanıcı (örneğin hdbadm) geçiş ve hello birincil site oluşturun.
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. [2] toohello sapsid kullanıcı (örneğin hdbadm) geçin ve hello ikincil site oluştur.
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a>Küme çerçeve Yapılandır

Merhaba varsayılan ayarlarını değiştirme

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

# <a name="now-we-load-hello-file-toohello-cluster"></a>Şimdi biz hello dosya toohello kümesi yükleme
sudo crm yük güncelleştirme crm-defaults.txt yapılandırın
</pre>

### <a name="create-stonith-device"></a>STONITH cihaz oluşturma

Merhaba STONITH aygıt Microsoft Azure karşı bir hizmet sorumlusu tooauthorize kullanır. Lütfen bu adımları toocreate bir hizmet sorumlusu izleyin.

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

Merhaba izinleri hello sanal makineler için düzenlenebilir sonra hello kümede hello STONITH cihazları yapılandırabilirsiniz.

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

# <a name="now-we-load-hello-file-toohello-cluster"></a>Şimdi biz hello dosya toohello kümesi yükleme
sudo crm yük güncelleştirme crm-fencing.txt yapılandırın
</pre>

### <a name="create-sap-hana-resources"></a>SAP HANA kaynakları oluşturun

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

# <a name="now-we-load-hello-file-toohello-cluster"></a>Şimdi biz hello dosya toohello kümesi yükleme
sudo crm yük güncelleştirme crm-saphanatop.txt yapılandırın
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

# <a name="now-we-load-hello-file-toohello-cluster"></a>Şimdi biz hello dosya toohello kümesi yükleme
sudo crm yük güncelleştirme crm-saphana.txt yapılandırın
</pre>

### <a name="test-cluster-setup"></a>Test kümesi Kurulumu
bölüm aşağıdaki hello kurulumunuzu test nasıl açıklanmaktadır. Her test kök olan ve hello SAP HANA ana hello sanal makine saphanavm1 üzerinde çalıştığını varsayar.

#### <a name="fencing-test"></a>Yalıtma Test

Düğüm saphanavm1 hello ağ arabiriminde devre dışı bırakarak hello Kurulum hello yalıtma Aracısı'nın test edebilirsiniz.

<pre><code>
sudo ifdown eth0
</code></pre>

Merhaba sanal makine şimdi yeniden veya küme yapılandırmanıza bağlı olarak durduruldu.
Merhaba stonith eylem toooff ayarlarsanız, hello sanal makine durdurulur ve sanal makine çalışırken geçirilen toohello hello kaynaklardır.

Merhaba sanal makine yeniden başladıktan sonra AUTOMATED_REGISTER ayarlarsanız hello SAP HANA kaynak ikincil olarak toostart başarısız olur = "false". Bu durumda, komutu aşağıdaki hello yürüterek tooconfigure hello HANA örneği ikincil olarak gerekir:

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a>El ile bir yük devretme sınaması

Düğüm saphanavm1 üzerinde hello pacemaker hizmetini durdurarak el ile bir yük devretme test edebilirsiniz.
<pre><code>
service pacemaker stop
</code></pre>

Merhaba yük devretme sonrasında hello hizmetini yeniden başlatabilirsiniz. Merhaba saphanavm1 SAP HANA kaynakta başarısız olur toostart ikincil olarak AUTOMATED_REGISTER ayarlarsanız = "false". Bu durumda, komutu aşağıdaki hello yürüterek tooconfigure hello HANA örneği ikincil olarak gerekir:

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

#### <a name="testing-a-migration"></a>Bir geçiş test etme

Komutu aşağıdaki hello yürüterek hello SAP HANA ana düğüm geçirebilirsiniz
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

Merhaba SAP HANA ana düğüm ve hello sanal IP adresi toosaphanavm2 içeren hello grubunu geçirmeniz gerekir.
Merhaba saphanavm1 SAP HANA kaynakta başarısız olur toostart ikincil olarak AUTOMATED_REGISTER ayarlarsanız = "false". Bu durumda, komutu aşağıdaki hello yürüterek tooconfigure hello HANA örneği ikincil olarak gerekir:

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

Merhaba geçiş yeniden silinmiş toobe gereken konum contraints oluşturur.

<pre><code>
crm configure edited

# delete location contraints that are named like hello following contraint. You should have two contraints, one for hello SAP HANA resource and one for hello IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

Ayrıca hello ikincil düğüme kaynağının toocleanup hello durumu gerekir

<pre><code>
# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a>Sonraki adımlar
* [Azure sanal makineleri planlama ve uygulama SAP için][planning-guide]
* [SAP için Azure sanal makineler dağıtımı][deployment-guide]
* [SAP için Azure sanal makineleri DBMS dağıtımı][dbms-guide]
* tooestablish yüksek kullanılabilirlik ve olağanüstü durum kurtarma SAP HANA planlama (büyük örnekler), azure'da nasıl görürüm toolearn [SAP HANA (büyük örnekler) Azure üzerinde yüksek kullanılabilirlik ve olağanüstü durum kurtarma](hana-overview-high-availability-disaster-recovery.md). 
