---
title: aaaOptimize MySQL performans Linux'ta | Microsoft Docs
description: "Bilgi nasıl toooptimize MySQL çalıştıran bir Azure Linux çalıştıran sanal makine üzerinde (VM)."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0c1c7fc5-a528-4d84-b65d-2df225f2233f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: ningk
ms.openlocfilehash: 9e6458723233721e06f30b9de33635d403eefcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a>Azure Linux VM'ler MySQL performansı en iyi duruma getirme
Hem sanal donanım seçimi ve yazılım yapılandırmasını Azure üzerinde MySQL performansı etkileyen pek çok etken vardır. Bu makalede, depolama, sistem ve veritabanı yapılandırmalarını en iyi duruma getirme performans odaklanır.

> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager](../../../resource-manager-deployment-model.md) ve klasik. Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Linux VM iyileştirmeler hello Resource Manager modeli hakkında daha fazla bilgi için bkz: [Linux VM'NİZDE Azure ile ilgili en iyi duruma getirme](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="utilize-raid-on-an-azure-virtual-machine"></a>Bir Azure sanal makinesi üzerinde RAID kullanma
Depolama bulut ortamlarında veritabanı performansını etkiler hello anahtar faktördür. Karşılaştırılan tooa tek disk RAID eşzamanlılık üzerinden daha hızlı erişim sağlar. Daha fazla bilgi için bkz: [standart RAID düzeyleri](http://en.wikipedia.org/wiki/Standard_RAID_levels).   

Disk g/ç işleme ve g/ç yanıt süresi Azure RAID artırılabilir. Bizim Laboratuvar testleri disk g/ç işleme iki katına ve RAID disklerini hello sayısı iki katına olduğunda (iki toofour, dört tooeight, vb.) g/ç yanıt süresi yarı oranında ortalama azaltılabilir gösterir. Bkz: [ek A](#AppendixA) Ayrıntılar için.  

Ayrıca hello RAID düzeyi artırdığınızda toodisk g/ç, MySQL performansı artırır.  Bkz: [ek B](#AppendixB) Ayrıntılar için.  

Ayrıca tooconsider hello öbek boyutu isteyebilirsiniz. Daha büyük bir öbek boyutu varsa, genel olarak, ek yükü, özellikle büyük yazmalar için daha düşük sahip olursunuz. Ancak, Hello öbek boyutu çok büyük olduğunda RAID yararlanarak engeller ek yükü ekleyebilirsiniz. Merhaba geçerli varsayılan boyutu toobe en genel üretim ortamları için en iyi kanıtlanmış 512 KB ' tır. Bkz: [ek C](#AppendixC) Ayrıntılar için.   

Başka bir sanal makine türleri için ekleyebilirsiniz kaç disklerde sınırları vardır. Bu sınırlar içinde ayrıntılı [Azure için sanal makine ve bulut hizmeti boyutları](http://msdn.microsoft.com/library/azure/dn197896.aspx). Daha az disklerle RAID yukarı tooset seçebilmenize rağmen dört ekli veri diskleri toofollow hello RAID örneği bu makalede, gerekir.  

Bu makalede, Linux sanal makine oluşturmuş ve MYSQL yüklenmiş ve yapılandırılmış varsayar. Kullanmaya başlama hakkında daha fazla bilgi için bkz. nasıl tooinstall Azure üzerinde MySQL.  

### <a name="set-up-raid-on-azure"></a>Azure üzerinde RAID ayarlama
Merhaba aşağıdaki adımlar nasıl toocreate RAID Azure'da hello Azure portal kullanarak gösterir. Windows PowerShell komut dosyalarını kullanarak RAID de ayarlayabilirsiniz.
Bu örnekte, şu dört disklerle RAID 0 yapılandırır.  

#### <a name="add-a-data-disk-tooyour-virtual-machine"></a>Bir veri diski tooyour sanal makine Ekle
Hello Azure portal, toohello panonuzu ve hello sanal makine toowhich tooadd bir veri diski istediğinizi seçin. Bu örnekte, mysqlnode1 hello sanal makinedir.  

<!--![Virtual machines][1]-->

Tıklatın **diskleri** ve ardından **Attach yeni**.

![Sanal makineler disk ekleme](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

Yeni bir 500 GB disk oluşturun. Olduğundan emin olun **konak önbelleği tercihi** çok ayarlanır**hiçbiri**.  İşiniz bittiğinde tıklatın **Tamam**.

![Boş diski kullanıma açın](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


Bu bir boş disk, sanal makineye ekler. Böylece dört veri diskleri için RAID sahip bu üç kez tekrarlayın.  

Eklenen hello görebilirsiniz hello çekirdek ileti günlüğüne bakarak hello sanal makinede sürücüler. Örneğin, toosee bu Ubuntu, komutu aşağıdaki kullanım hello:  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-hello-additional-disks"></a>RAID ile Merhaba ek disk oluşturabilirsiniz.
Merhaba aşağıdaki adımları nasıl çok açıklamak[yazılım RAID Linux üzerinde yapılandırma](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

> [!NOTE]
> Merhaba XFS dosya sistemi kullanıyorsanız, RAID oluşturduktan sonra aşağıdaki adımları hello yürütün.
>
>

komutu aşağıdaki Debian, Ubuntu ya da Linux Naneli kullanım hello üzerinde tooinstall XFS:  

    apt-get -y install xfsprogs  

komutu aşağıdaki Fedora, CentOS veya RHEL, kullanım hello üzerinde tooinstall XFS:  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a>Yeni bir depolama yol ayarla
Yeni bir depolama yol komutu tooset aşağıdaki hello kullan:  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-hello-original-data-toohello-new-storage-path"></a>Merhaba özgün veri toohello yeni depolama birimi yolu kopyalayın
Komut toocopy veri toohello yeni depolama birimi yolu izleyerek hello kullan:  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-hello-data-disk"></a>MySQL erişebilmesi için (okuma ve yazma) değiştirme izinleri hello veri diski
Aşağıdaki komut toomodify izinleri hello kullan:  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-hello-disk-io-scheduling-algorithm"></a>Merhaba disk g/ç algoritması zamanlama ayarlama
Linux algoritmaları zamanlama g/ç dört tür uygular:  

* SEKMEYİ algoritması (No işlem)
* Son tarih algoritması (son)
* Tamamen Orta Sıralama algoritması (CFQ)
* Bütçe dönem algoritması (Anticipatory)  

Farklı senaryolar toooptimize performans altında farklı g/ç zamanlayıcılar seçebilirsiniz. Tamamen rastgele erişim ortamında değil hello CFQ ve performans için son tarih algoritmaları arasında önemli bir fark yoktur. Merhaba MySQL veritabanı ortamı tooDeadline kararlılık için ayarlamanızı öneririz. Çok sayıda sıralı g/ç ise CFQ disk g/ç performansını düşürebilir.   

SSD ve diğer donanım için SEKMEYİ veya son hello varsayılan Zamanlayıcı daha iyi performans elde edebilirsiniz.   

Önceki toohello çekirdek 2.5, hello varsayılan g/ç algoritması zamanlama son ' dir. Merhaba çekirdek 2.6.18 ile başlayarak, CFQ hello varsayılan g/ç zamanlama algoritma hale geldi.  Bu ayarı çekirdek önyükleme zaman belirtin veya hello sistem çalışırken dinamik olarak bu ayarı değiştirin.  

Aşağıdaki örneğine hello nasıl toocheck ve kümesi varsayılan Zamanlayıcı toohello SEKMEYİ algoritma hello Debian dağıtım ailesindeki hello gösterir.  

### <a name="view-hello-current-io-scheduler"></a>Görünüm hello geçerli g/ç Zamanlayıcı
tooview hello Zamanlayıcı hello aşağıdaki komutu çalıştırın:  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

Merhaba geçerli Zamanlayıcı gösterir çıktı aşağıdaki görürsünüz:  

    noop [deadline] cfq


### <a name="change-hello-current-device-devsda-of-hello-io-scheduling-algorithm"></a>Merhaba g/ç zamanlama algoritmasının Hello geçerli aygıtı (/ dev/sda) değiştirme
Aşağıdaki komutları toochange hello geçerli cihaz hello çalıştırın:  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> Bu/dev/sda için tek başına ayarı kullanışlı değildir. Merhaba veritabanının bulunduğu tüm veri disklerde ayarlanmalıdır.  
>
>

Çıktı aşağıdaki, grub.cfg başarıyla yeniden oluşturuldu ve bu hello varsayılan Zamanlayıcı güncelleştirilmiş tooNOOP bırakıldı gösteren hello görmeniz gerekir:  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

Hello Red Hat dağıtım ailesi için aşağıdaki komut yalnızca hello:

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a>Sistem dosyası işlemleri ayarlarını yapılandırma
Bir en iyi uygulamadır toodisable hello *atime* hello dosya sistemi günlük kaydı özelliği. Atime hello son dosya erişim zamanı ' dir. Bir dosya erişildiğinde hello dosya sistemi kayıtları zaman damgası hello günlüğünde hello. Ancak, bu bilgileri nadiren kullanılır. Hangi genel disk erişim süresini azaltır, onu gereksiniminiz yoksa devre dışı bırakabilirsiniz.  

toodisable atime günlüğü, toomodify hello dosya sistemi yapılandırma dosyası /etc/ fstab ve gerekir hello eklemek **noatime** seçeneği.  

Örneğin, aşağıdaki örnek hello gösterildiği gibi hello noatime ekleyerek, hello VIM /etc/fstab dosyasını düzenleyin:  

    # CLOUD_IMG: This file was created/modified by hello Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add hello “noatime” option below toodisable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

Ardından, hello dosya sistemi ile komutu aşağıdaki hello yeniden bağlayın:  

    mount -o remount /RAID0

Test hello sonuç değiştirdi. Merhaba test dosyasını değiştirdiğinizde, hello erişim zamanı güncelleştirilmez. Aşağıdaki örneklerde gösterildiği hangi hello kodu önce ve sonra değişiklik benzer hello.

Önce:        

![Erişim değişiklikten önce kod][5]

Sonra:

![Erişimi değiştirme sonrasında kod][6]

## <a name="increase-hello-maximum-number-of-system-handles-for-high-concurrency"></a>Hello en yüksek eşzamanlılık için sistem işleyicilerin sayısını artırın
MySQL yüksek eşzamanlılık veritabanıdır. Merhaba varsayılan eşzamanlı tanıtıcıları 1024 Linux için her zaman yeterli olmayan sayısıdır. Adımları tooincrease hello en fazla eş zamanlı tanıtıcıları hello sistem toosupport yüksek eşzamanlılığı MySQL, aşağıdaki hello kullanın.

### <a name="modify-hello-limitsconf-file"></a>Merhaba limits.conf dosyasını değiştirme
tooincrease hello en fazla eş zamanlı tanıtıcıları izin, dört satırlardan hello /etc/security/limits.conf dosyasında hello ekleyin. 65536 hello sistemin destekleyebileceği en fazla hello olduğuna dikkat edin.   

    * yazılım nofile 65536
    * Sabit nofile 65536
    * yazılım nproc 65536
    * Sabit nproc 65536

### <a name="update-hello-system-for-hello-new-limits"></a>Merhaba sistemi hello yeni sınırları için güncelleştirme
tooupdate hello sistemi, hello aşağıdaki komutları çalıştırın:  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-hello-limits-are-updated-at-boot-time"></a>Önyükleme sırasında Hello sınırları güncelleştirildiğinden emin olun
Merhaba, önyükleme sırasında etkili şekilde hello /etc/rc.local dosyasındaki başlatma komutları aşağıdaki yerleştirin.  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a>MySQL veritabanı en iyi duruma getirme
Azure üzerinde MySQL tooconfigure, kullanabileceğiniz hello aynı performans ayarlama stratejisi bir şirket içi makinede kullanın.  

Merhaba ana g/ç iyileştirme kurallar şunlardır:   

* Merhaba önbellek boyutunu artırın.
* G/ç yanıt süresini azaltın.  

toooptimize MySQL sunucu ayarları, hem sunucu hem de istemci bilgisayarlar hello varsayılan yapılandırma dosyası hello my.cnf dosyasını güncelleştirebilirsiniz.  

Merhaba aşağıdaki yapılandırma öğelerini hello MySQL performansı etkileyen ana faktörler şunlardır:  

* **innodb_buffer_pool_size**: hello arabellek havuzu arabelleğe alınan verileri ve hello dizini içerir. Bu, genellikle fiziksel bellek yüzdesi too70 ayarlanır.
* **innodb_log_file_size**: hello Yinele günlük boyutu budur. Yazma işlemleri hızlı, güvenilir ve kurtarılabilir kilitlenme sonrasında Yinele günlükleri tooensure kullanın. Bu yazma işlemleri günlüğe kaydetme için yeterince alan verecektir too512 MB ayarlanır.
* **max_connections**: bazen uygulamaları bağlantıları düzgün kapatmayın. Daha büyük bir değer hello sunucu bağlantıları toorecycle idled daha fazla zaman verir. Merhaba en fazla bağlantı sayısı, 10.000 olmakla birlikte hello en fazla 5000 önerilir.
* **Innodb_file_per_table**: Bu ayar etkinleştirir ya da ayrı dosyalar InnoDB toostore tablolarda hello özelliğini devre dışı bırakır. Birçok gelişmiş yönetim işlemleri verimli bir şekilde uygulanabilir hello seçeneği tooensure üzerinde etkinleştirin. Bir performans açısından bakıldığında, bu hello tablo alanı aktarım hızı ve hello debris yönetim performansı en iyi duruma getirme. Merhaba bu seçenek ayarı ON önerilir.</br></br>
MySQL 5.6 hello varsayılan ayarı ON, olduğundan hiçbir eyleme gerek yoktur. Önceki sürümler için OFF hello varsayılan ayardır. veriler yüklenmeden önce yalnızca yeni oluşturulan tabloları etkilendiği hello ayarı değiştirilmelidir.
* **innodb_flush_log_at_trx_commit**: hello varsayılan değer 1'dir, ile Merhaba too0 kapsamını Ayarla ~ 2. tek başına MySQL veritabanı için en uygun seçeneği hello Hello varsayılan değerdir. Merhaba ayar 2 etkinleştirir, çoğu veri bütünlüğü hello ve MySQL kümesi yöneticisinde için uygundur. Merhaba ayarı 0 (daha iyi performans ile bazı durumlarda) güvenilirlik etkileyebilir ve MySQL kümedeki ikincil için uygun veri kaybı sağlar.
* **Innodb_log_buffer_size**: hello günlük arabellek tooflush hello günlük toodisk hello işlemleri tamamlama önce gerek kalmadan işlemleri toorun sağlar. Ancak, ikili büyük nesne veya metin alanını ise hello önbellek hızla dolacaktır ve sık disk g/ç tetiklenir. Innodb_log_waits durumu değişken değilse daha iyi hello arabellek boyutunu artırın olan 0.
* **query_cache_size**: hello en iyi seçenektir toodisable hello outset ondan. (MySQL 5.6 de hello varsayılan ayar budur) query_cache_size too0 ayarlayabilir ve diğer yöntemleri toospeed sorguları yukarı kullanabilirsiniz.  

Bkz: [ek D](#AppendixD) önce ve sonra hello iyileştirme performans karşılaştırması.

## <a name="turn-on-hello-mysql-slow-query-log-for-analyzing-hello-performance-bottleneck"></a>Merhaba MySQL yavaş sorgu günlüğü hello performans düşüklüğü çözümlemek için Aç
Merhaba MySQL yavaş sorgu günlüğü hello yavaş sorgular için MySQL belirlemenize yardımcı olabilir. Merhaba MySQL yavaş sorgu günlüğü etkinleştirdikten sonra MySQL araçları gibi kullanabilirsiniz **mysqldumpslow** tooidentify hello performans düşüklüğü.  

Varsayılan olarak, bu etkin değil. Merhaba yavaş sorgu oturum açma kapatma bazı CPU kaynaklarını tüketebilir. Bu geçici olarak performans sorunları gidermek için etkinleştirmenizi öneririz. tooturn hello yavaş sorgu oturum:

1. Merhaba my.cnf dosyası aşağıdaki satırları toohello son hello ekleyerek değiştirin:

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. Merhaba MySQL sunucusunu yeniden başlatın.

        service  mysql  restart

3. Hello kullanarak Hello ayarı etkisi sürüyor olup olmadığını denetleyin **Göster** komutu.

![Yavaş-query-log ON][7]   

![Yavaş-query-günlük sonuçları][8]

Bu örnekte, bu hello yavaş sorgu özelliği etkinleştirildi görebilirsiniz. Merhaba sonra kullanabileceğiniz **mysqldumpslow** dizinleri ekleme gibi performansı iyileştirmek ve aracı toodetermine performans sorunları.

## <a name="appendices"></a>Ekler
Merhaba, hedeflenen laboratuvar ortamında üretilen örnek performans test verileri verilmiştir. Genel arka plan hello performans veri eğilimi üzerinde farklı performans yaklaşımlar ayarlama ile sağlarlar. Merhaba sonuçları altında farklı ortamı veya ürün sürümleri değişebilir.

### <a name="AppendixA"></a>Ek A  
**Farklı RAID düzeyleri ile disk performansı (IOPS)**

![IOPS diskle farklı RAID düzeyleri][9]

**Test komutları**  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> Bu test Hello iş yükünü tooreach hello üst sınır RAID çalışırken 64 iş parçacığı kullanır.
>
>

### <a name="AppendixB"></a>Ek B  
**Farklı RAID düzeyleri ile MySQL performans (performans) karşılaştırma**   
(XFS dosya sistemi)

![Farklı RAID düzeyleri ile MySQL performans karşılaştırma][10]  
![Farklı RAID düzeyleri ile MySQL performans karşılaştırma][11]

**Test komutları**

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

**Farklı RAID düzeyleri ile MySQL performans (OLTP) karşılaştırma**  
![Farklı RAID düzeyleri ile MySQL performans (OLTP) karşılaştırma][12]

**Test komutları**

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <a name="AppendixC"></a>Ek C   
**Farklı öbek boyutları için disk performans (IOPS) karşılaştırması**  
(XFS dosya sistemi)

![][13]

**Test komutları**  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

Bu test için kullanılan hello dosya boyutları 30 GB ve 1 GB, sırasıyla, RAID 0 (4 disk) ile XFS dosya sistemi.

### <a name="AppendixD"></a>Ek D  
**MySQL performans (performans) karşılaştırma önce ve sonra en iyi duruma getirme**  
(XFS dosya sistemi)

![MySQL performans (performans) karşılaştırma önce ve sonra en iyi duruma getirme][14]

**Test komutları**

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

**Varsayılan ve en iyi duruma getirme için Hello yapılandırma ayarı aşağıdaki gibidir:**

| Parametreler | Varsayılan | İyileştirme |
| --- | --- | --- |
| **innodb_buffer_pool_size** |None |7 GB |
| **innodb_log_file_size** |5 MB |512 MB |
| **max_connections** |100 |5000 |
| **innodb_file_per_table** |0 |1 |
| **innodb_flush_log_at_trx_commit** |1 |2 |
| **innodb_log_buffer_size** |8 MB |128 MB |
| **query_cache_size** |16 MB |0 |

Daha ayrıntılı için [en iyi duruma getirme yapılandırma parametrelerini](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), toohello başvuran [MySQL resmi yönergeleri](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).  

  **Test ortamı**  

| Donanım | Ayrıntılar |
| --- | --- |
| CPU |AMD Opteron(tm) işlemci 4171 HE / 4 çekirdek |
| Bellek |14 GB |
| Disk |10 GB/disk |
| İşletim Sistemi |Ubuntu 14.04.1 LTS |

[1]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-01.png
[2]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-02.png
[3]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-03.png
[4]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-04.png
[5]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-05.png
[6]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-06.png
[7]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-07.png
[8]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-08.png
[9]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-09.png
[10]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-10.png
[11]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-11.png
[12]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-12.png
[13]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-13.png
[14]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-14.png

