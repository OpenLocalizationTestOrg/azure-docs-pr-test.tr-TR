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
# <a name="use-load-balanced-sets-tooclusterize-mysql-on-linux"></a>Yük dengeli kümeleri tooclusterize MySQL Linux'ta kullanın
> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager](../../../resource-manager-deployment-model.md) ve klasik. Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. A [Resource Manager şablonu](https://azure.microsoft.com/documentation/templates/mysql-replication/) toodeploy bir MySQL kümesi ihtiyacınız varsa kullanılabilir.

Bu makalede inceler ve hello farklı yaklaşımlar kullanılabilir toodeploy yüksek oranda kullanılabilir Linux tabanlı hizmetler MySQL Server yüksek kullanılabilirlik öncü olarak keşfetme Microsoft Azure üzerinde gösterilmektedir. Bu yaklaşım gösteren bir video kullanılabilir [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).

Biz DRBD, Corosync ve Pacemaker göre hiçbir şey paylaşılmayan, iki düğümlü ve tek yöneticili MySQL yüksek kullanılabilirlik çözümü özetler. Yalnızca bir düğüm MySQL aynı anda çalıştırır. Okuma ve yazma DRBD kaynak hello de sınırlı tooonly bir aynı anda düğümdür.

Microsoft Azure tooprovide hepsini işlevselliği ve uç nokta algılama, kaldırma ve hello VIP normal kurtarılması yük dengelemeli kümelerinde kullanacağınız çünkü LVS gibi bir VIP çözümü için gerek yoktur. Merhaba VIP hello bulut hizmeti ilk oluşturduğunuzda Microsoft Azure tarafından atanan genel olarak yönlendirilebilir bir IPv4 adresi değil.

Diğer olası mimari NBD küme, Percona, Galera ve en az bir de dahil olmak üzere çeşitli ara yazılımı çözümler de dahil olmak üzere MySQL için bir VM olarak kullanılabilir [VM deposu](http://vmdepot.msopentech.com). Bu çözümlerin tek noktaya yayın ve çok noktaya yayın veya yayın üzerinde çoğaltabilir ve paylaşılan depolama ortamı veya birden çok ağ arabirimi güvenmeyin sürece hello senaryoları kolay toodeploy Microsoft Azure üzerinde olmalıdır.

Bunlar mimarileri kümeleme PostgreSQL ve OpenLDAP gibi tooother ürün benzer bir şekilde genişletilebilir. Örneğin, bu yük dengeleyici yordamı paylaşılmadığı ile başarıyla çok ana OpenLDAP ile test edilmiştir ve bizim Channel 9 blogunda izleyebilirsiniz.

## <a name="get-ready"></a>Hazırlanma
Merhaba aşağıdakiler kaynakları ve yeteneklerini:

  - Bir Microsoft Azure hesap mümkün toocreate bir geçerli abonelik en az iki sanal makineleri (Bu örnekte XS kullanılan)
  - Bir ağ ve bir alt ağ
  - Bir benzeşim grubu
  - Bir kullanılabilirlik kümesi
  - özelliği toocreate VHD'ler hello hello hello bulut hizmeti ile aynı bölgeye ve toohello Linux VM'ler ekleme

### <a name="tested-environment"></a>Sınanan ortamı
* Ubuntu 13.10
  * DRBD
  * MySQL sunucusu
  * Corosync ve Pacemaker

### <a name="affinity-group"></a>Benzeşim grubu
Toohello Klasik Azure portalında oturum açarak hello çözüm için benzeşim grubu oluşturmak seçme **ayarları**ve bir benzeşim grubu oluşturma. Daha sonra oluşturulan ayrılan kaynakları toothis benzeşim grubu atanır.

### <a name="networks"></a>Ağlar
Yeni bir ağ oluşturulur ve bir alt ağ hello ağı içinde oluşturulur. Bu örnek 10.10.10.0/24 ağ içinde yalnızca bir /24 alt ağ ile kullanır.

### <a name="virtual-machines"></a>Sanal makineler
ilk Ubuntu 13.10 VM Endorsed Ubuntu galeri görüntüsü kullanılarak oluşturulur ve adlandırılır hello `hadb01`. Yeni bir bulut hizmeti hadb adlandırılan hello işlemde oluşturulur. Bu ad paylaşılan hello daha fazla kaynak eklendiğinde, hello hizmet olacak yük dengeli yapısı gösterilmektedir. Merhaba oluşturulmasını `hadb01` hello portal olaysız ve tamamlanan kullanmaktır. SSH için bir uç nokta otomatik olarak oluşturulur ve hello yeni bir ağ seçtiniz. Artık kullanılabilirlik Merhaba VM'ler kümesi oluşturabilirsiniz.

İlk VM (teknik olarak hello bulut hizmeti oluşturulduğunda) oluşturulur hello sonra oluşturma ikinci VM hello `hadb02`. Merhaba VM ikinci, Ubuntu 13.10 VM galeri hello hello portal kullanarak, ancak var olan bir bulut hizmetini kullanın `hadb.cloudapp.net`, yeni bir tane oluşturmak yerine. Merhaba ağ ve kullanılabilirlik kümesi otomatik olarak seçilmesi gerekir. Bir SSH uç noktası, çok oluşturulur.

Her iki VM oluşturulduktan sonra hello SSH bağlantı noktası için not edin `hadb01` (TCP 22) ve `hadb02` (otomatik olarak Azure tarafından atanan).

### <a name="attached-storage"></a>Bağlı depolama
Yeni bir disk tooboth VM'ler ekleyin ve hello işleminde 5 GB disk oluşturun. Merhaba diskleri hello VHD kapsayıcısı ana işletim sistemi diskleriniz için kullanımda barındırılır. Diskleri oluşturup bağlı sonra var. olduğundan hiçbir gerek toorestart Linux hello çekirdek hello yeni cihaz görürsünüz. Bu aygıt genellikle değil `/dev/sdc`. Denetleme `dmesg` hello çıktı.

Kullanarak her bir VM üzerinde bir bölüm oluşturmak `cfdisk` (birincil, Linux bölüm) ve hello yeni bölüm tablosu yazma. Bir dosya sistemi bu bölüme oluşturmayın.

## <a name="set-up-hello-cluster"></a>Merhaba kümesi
Her iki Ubuntu VM APT tooinstall Corosync, Pacemaker ve DRBD kullanın. toodo ile bunu `apt-get`çalıştırın hello aşağıdaki kodu:

    sudo apt-get install corosync pacemaker drbd8-utils.

MySQL şu anda yüklemeyin. Debian ve Ubuntu yükleme betikleri başlatma MySQL veri dizini üzerinde `/var/lib/mysql`, ancak hello dizin DRBD dosya sistemi tarafından değiştirilen çünkü daha sonra MySQL tooinstall gerekir.

Doğrulayın (kullanarak `/sbin/ifconfig`) her iki VM hello 10.10.10.0/24 alt ağ adresleri ve bunların birbirlerine ada göre ping atabildiğinizi kullanıyor. Aynı zamanda `ssh-keygen` ve `ssh-copy-id` toomake emin her iki VM, bir parola gerektirmeden SSH yoluyla kurabilir.

### <a name="set-up-drbd"></a>DRBD ayarlayın
Merhaba temel kullanan DRBD kaynak oluşturma `/dev/sdc1` tooproduce bölüm bir `/dev/drbd1` ext3 kullanılarak biçimlendirilmiş ve birincil ve ikincil düğüm kullanılan kaynak.

1. Açık `/etc/drbd.d/r0.res` ve kopyalama hello her iki sanal makinelerin kaynak tanımı aşağıdaki:

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

2. Merhaba kaynak kullanarak başlatmak `drbdadm` her iki VM üzerinde:

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. Üzerinde birincil VM hello (`hadb01`), hello DRBD kaynak (birincil) sahipliğini zorla:

        sudo drbdadm primary --force r0

/ Proc/drbd Merhaba içeriğine incelerseniz (`sudo cat /proc/drbd`) her iki VM üzerinde görmelisiniz `Primary/Secondary` üzerinde `hadb01` ve `Secondary/Primary` üzerinde `hadb02`, bu noktada hello çözümü ile tutarlı. Merhaba 5 GB disk, hiçbir ücret toocustomers hello 10.10.10.0/24 ağ üzerinden eşitlenir.

Merhaba disk eşitlendikten sonra hello dosya sistemi üzerinde oluşturabileceğiniz `hadb01`. Test amacıyla, ext2 kullandık ancak koddan hello ext3 dosya sistemi oluşturacak:

    mkfs.ext3 /dev/drbd1

### <a name="mount-hello-drbd-resource"></a>Merhaba DRBD kaynak Bağla
Merhaba DRBD kaynakları artık hazır toomount olduğunuz `hadb01`. Debian ve türevleri kullanım `/var/lib/mysql` MySQL'ın veri dizini olarak. MySQL yüklemediniz çünkü hello dizin oluşturun ve hello DRBD kaynak bağlayın. tooperform kod aşağıdaki hello çalıştırmak, bu seçenek `hadb01`:

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a>MySQL ayarlayın
Şimdi kullandığınız hazır tooinstall MySQL `hadb01`:

    sudo apt-get install mysql-server

İçin `hadb02`, iki seçeneğiniz vardır. Mysql /var/lib/mysql oluşturmak, yeni bir veri dizin ile doldurun ve hello içerikleri kaldırmak sunuculu, yükleyebilirsiniz. tooperform kod aşağıdaki hello çalıştırmak, bu seçenek `hadb02`:

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

Merhaba ikinci seçenektir toofailover çok`hadb02` ve orada mysql server yükleyin. Yükleme betikleri hello mevcut yükleme görürsünüz ve dokunma olmaz.

Çalışma hello aşağıdaki kodu üzerinde `hadb01`:

    sudo drbdadm secondary –force r0

Çalışma hello aşağıdaki kodu üzerinde `hadb02`:

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

Toofailover DRBD şimdi planlamıyorsanız hello ilk seçenek tartışmaya açık bir şekilde daha az rağmen Zarif daha kolay olur. Bu ayarladıktan sonra MySQL veritabanınızı üzerinde çalışmaya başlayabiliriz. Çalışma hello aşağıdaki kodu üzerinde `hadb02` (veya hello sunucuları hangi biri tooDRBD göre etkin olan):

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* tooroot;

> [!WARNING]
> Bu son deyim etkili bir şekilde bu tablodaki hello kök kullanıcı için kimlik doğrulaması devre dışı bırakır. Bu üretim-sınıf tarafından değiştirilmesi gereken verme deyimleri ve yalnızca tanımlayıcı amaçlarla yer alır.

(Bu kılavuzun amacı hello olan) dışında hello VM'ler toomake sorgularından isterseniz, ayrıca MySQL için ağ tooenable gerekir. Her iki VM üzerinde açmak `/etc/mysql/my.cnf` ve çok Git`bind-address`. Başlangıç adresi 127.0.0.1 değiştirmek too0.0.0.0. Merhaba dosya kaydedildikten sonra sorun bir `sudo service mysql restart` geçerli birincil üzerinde.

### <a name="create-hello-mysql-load-balanced-set"></a>Merhaba MySQL yük dengeli kümesi oluşturma
Toohello portalına geri dönün, çok Git`hadb01`ve seçin **uç noktaları**. uç noktası, bir toocreate seçin MySQL (TCP 3306) hello aşağı açılan liste ve seçin **oluştur Yeni Yük dengeli kümesi**. Ad hello yük dengeli uç nokta `lb-mysql`. Ayarlama **zaman** too5 saniye, en düşük.

Merhaba endpoint oluşturduktan sonra çok Git`hadb02`, seçin **uç noktaları**ve bir uç nokta oluşturun. Seçin `lb-mysql`ve ardından MySQL hello aşağı açılan listeden seçin. Bu adım için hello Azure CLI de kullanabilirsiniz.

Artık hello küme el ile işlem için gereken her şeyi sahipsiniz.

### <a name="test-hello-load-balanced-set"></a>Sınama Hello yük dengeli kümesi
Testleri bir dış makineden herhangi bir MySQL istemcisi kullanarak veya bir Azure Web sitesi olarak çalışan phpMyAdmin gibi belirli uygulamaları kullanarak gerçekleştirilebilir. Bu durumda, başka bir Linux kutuda MySQL'ın komut satırı aracı kullanılır:

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a>El ile yük devrediliyor
Yük devretme işlemlerini MySQL kapatılıyor DRBD'ın birincil değiştirme ve MySQL yeniden başlatmayı benzetimini yapabilirsiniz.

tooperform bu görevi hadb01 üzerinde koddan hello çalıştır:

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

Ardından, hadb02 üzerinde:

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

El ile yük devri sonra uzak sorgunuzu yineleyebilir ve mükemmel çalışması gerekir.

## <a name="set-up-corosync"></a>Corosync ayarlayın
Corosync Pacemaker toowork için gerekli hello temel küme altyapısıdır. Pacemaker işlevindeki daha benzer tooHeartbeat kalırken sinyal (ve Ultramonkey gibi diğer yöntemleri), Corosync hello CRM işlevleri, bir bölme içindir.

Merhaba ana Corosync için Azure üzerinde Corosync çok noktaya yayın üzerinden tek noktaya yayın iletişim tercih eder, ancak Microsoft Azure ağı yalnızca tek noktaya yayın destekler sınırlamadır.

Neyse ki, Corosync çalışma tek noktaya yayın modu vardır. Merhaba yalnızca gerçek tüm düğümlerin kendilerini arasında iletişim için IP adresleri de dahil olmak üzere, yapılandırma dosyalarında toodefine hello düğümleri gerekiyor sınırlamadır. Tek noktaya yayın ve değişiklik adresi, düğüm listeler ve günlük dizinleri bağlamak için biz hello Corosync örnek dosyalarını kullanabilirsiniz (Ubuntu kullanan `/var/log/corosync` hello örnek kullanım dosyalar sırada `/var/log/cluster`) ve çekirdek araçları sağlar.

> [!NOTE]
> Merhaba aşağıdaki kullanın `transport: udpu` yönergesi hello el ile tanımlanan ve her iki düğüm için IP adresi.

Çalışma hello aşağıdaki kodu üzerinde `/etc/corosync/corosync.conf` iki düğüm için:

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

Her iki VM üzerindeki bu yapılandırma dosyasını kopyalayın ve her iki düğüm Corosync Başlat:

    sudo service start corosync

Merhaba hizmeti başlatılıyor, kısa süre sonra hello küme hello geçerli halka kurulacaktır ve çekirdek constituted. Bu işlev günlükleri gözden geçirme veya koddan hello çalıştırarak kontrol edebilirsiniz:

    sudo corosync-quorumtool –l

Görüntü aşağıdaki çıktı benzer toohello görürsünüz:

![corosync quorumtool - m örnek çıkış](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a>Pacemaker ayarlayın
Pacemaker kullanır kaynaklar için küme toomonitor Merhaba, ne zaman ana Git aşağı tanımlamak ve bu kaynakları toosecondaries geçin. Kaynakların kullanılabilir komut kümesi ya da LSB'si (Init benzeri) komut dosyaları, diğer seçenekler arasında tanımlanabilir.

Pacemaker çok "kendi" Merhaba DRBD kaynak, hello bağlama noktası ve hello MySQL hizmeti istiyoruz. Pacemaker DRBD açıp kapatabilirsiniz, bağlama ve bunu çıkarın ve ardından başlatabilir ve MySQL hello sırası bozuk bir şey olduğunda, Kurulum tamamlandıktan hello birincil ile olur sağ durdurabilirsiniz.

Pacemaker ilk kez yüklediğinizde, yapılandırmanızı gösterilene benzer yeteri kadar basit olmalıdır:

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. Çalıştırarak Hello yapılandırmasını denetleyin `sudo crm configure show`.
2. Bir dosya oluşturun (gibi `/tmp/cluster.conf`) kaynakları aşağıdaki hello ile:

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

3. Merhaba dosyasına hello yapılandırma yük. Yalnızca toodo bu bir düğümünden gerekir.

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. Pacemaker her iki düğüm önyüklemede başladığından emin olun:

        sudo update-rc.d pacemaker defaults

5. Kullanarak `sudo crm_mon –L`, düğümleriniz birini hello küme için hello Yöneticisi olur ve tüm hello kaynakları çalıştıran doğrulayın. Merhaba kaynakları çalıştıran bağlama ve ps toocheck kullanabilirsiniz.

Aşağıdaki ekran görüntüsü gösterildiği hello `crm_mon` durdurulmuş bir düğümle (Ctrl + C seçerek çıkış):

![crm_mon düğüm durduruldu](./media/mysql-cluster/image002.png)

Bu ekran, düğüm, bir ana ve bir ikincil gösterir:

![crm_mon işletimsel ana/bağımlı](./media/mysql-cluster/image003.png)

## <a name="testing"></a>Test Etme
Otomatik Yük devretme benzetimi için hazırsınız. Var olan iki yolu toodo bu: yazılım ve donanım.

Merhaba yumuşak şekilde hello kümenin kapatma işlevini kullanır: ``crm_standby -U `uname -n` -v on``. Bu hello yöneticisinde kullanırsanız, hello bağımlı devreye girer. Bu geri toooff tooset unutmayın. Bunu yapmazsanız, crm_mon bekleme tek bir düğüm gösterir.

Merhaba sabit şekilde kapanıyor hello birincil VM (hadb01) hello Portalı aracılığıyla veya değiştirerek hello hello (diğer bir deyişle, durdurmak, kapatma) VM üzerinde çalışma düzeyi. Bu Corosync ve Pacemaker bu hello Yöneticisi'nin giderek aşağı sinyal tarafından yardımcı olur. Bu test edebilirsiniz (Bakım pencereleri için yararlıdır), ancak Ayrıca, hello VM dondurma tarafından hello senaryo zorlayabilirsiniz.

## <a name="stonith"></a>STONITH
Olası tooissue VM kapatma fiziksel bir aygıtı denetleyen STONITH komut dosyası yerine hello Azure CLI aracılığıyla olmalıdır. Kullanabileceğiniz `/usr/lib/stonith/plugins/external/ssh` Bankası ve hello kümenin yapılandırmasında STONITH etkinleştir. Azure CLI genel olarak yüklenmesi gerekir ve yayımlama hello ayarları ve profil hello kümenin kullanıcı için yüklenen.

Merhaba kaynak için örnek kod edinilebilir [GitHub](https://github.com/bureado/aztonith). Merhaba çok aşağıdaki ekleyerek Hello kümenin yapılandırmasını değiştirme`sudo crm configure`:

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> Merhaba betik denetimleri yukarı/aşağı gerçekleştirmez. 15 ping denetimleri Hello özgün SSH kaynak var, ancak bir Azure VM için kurtarma süresi daha fazla değişken olabilir.

## <a name="limitations"></a>Sınırlamalar
Merhaba aşağıdaki sınırlamalar uygulanır:

* Merhaba, bir kaynak olarak Pacemaker kullandığı DRBD yöneten linbit DRBD kaynak komut dosyası `drbdadm down` hello düğüm yalnızca bekleme durumuna geçiyor olsa bile bir düğüm kapanırken. Hello Yöneticisi yazma alır ancak hello bağımlı hello DRBD kaynak eşitleme değil çünkü bu ideal değildir. Hello Yöneticisi graciously başarısız olmaz, hello bağımlı daha eski bir dosya sistemi durumu alabilir. Bu çözümü iki olası yolu vardır:
  * Zorunlu bir `drbdadm up r0` tüm küme düğümlerinde yerel (clusterized değil) izleme olaylarını aracılığıyla içinde
  * Merhaba linbit DRBD komut dosyası düzenleme, dikkat ederek `down` çağrılmaz`/usr/lib/ocf/resource.d/linbit/drbd`
* Böylece uygulamaları küme durumunu algılayan ve zaman aşımı süresi daha dayanıklı hello yük dengeleyicinin en az beş saniyede toorespond gerekir. Uygulama sıraları ve sorgu middlewares gibi diğer mimarileri de yardımcı olabilir.
* MySQL ayarlama yazma yönetilebilir hızı yapılır gerekli tooensure ve önbellekleri temizlenmiş toodisk gibi bir sıklıkla olası toominimize bellek kaybı.
* Yazma performansı VM'de bağımlı bu DRBD tooreplicate hello aygıt tarafından kullanılan hello mekanizması olduğundan hello sanal anahtarda birbirine.
