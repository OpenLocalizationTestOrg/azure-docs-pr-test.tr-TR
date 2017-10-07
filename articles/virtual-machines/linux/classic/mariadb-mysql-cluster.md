---
title: "aaaRun MariaDB (MySQL) küme Azure üzerinde | Microsoft Docs"
description: "Bir MariaDB Oluştur + Galera MySQL Azure sanal makineleri küme"
services: virtual-machines-linux
documentationcenter: 
author: sabbour
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d0d21937-7aac-4222-8255-2fdc4f2ea65b
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/15/2015
ms.author: asabbour
ms.openlocfilehash: f9a4d6c45d76478a8a3526b407c7bbe6aeb40423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="mariadb-mysql-cluster-azure-tutorial"></a>MariaDB (MySQL) küme: Azure Öğreticisi
> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager](../../../resource-manager-deployment-model.md) ve klasik. Bu makalede, hello Klasik dağıtım modeli yer almaktadır. Microsoft, en yeni dağıtımların hello Azure Resource Manager modelini kullanmasını önerir.

> [!NOTE]
> MariaDB Kurumsal küme hello Azure Marketi'nde kullanıma sunulmuştur. Merhaba yenilik MariaDB Galera küme üzerinde Azure Resource Manager otomatik olarak dağıtacaktır. Merhaba yenilik gelen kullanması gereken [Azure Marketi](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).
>
>

Bu makale size nasıl gösterir toocreate çok asıl [Galera](http://galeracluster.com/products/) kümesinin [MariaDBs](https://mariadb.org/en/about/) (MySQL için güçlü, ölçeklenebilir ve güvenilir içeri kayma yenileme) Azure üzerinde yüksek oranda kullanılabilir bir ortamda toowork sanal makineler.

## <a name="architecture-overview"></a>Mimariye genel bakış
Bu makalede nasıl toocomplete hello aşağıdaki adımları açıklanır:

- Üç düğümlü bir küme oluşturun.
- Veri disklerinden hello işletim sistemi diski ayrı hello.
- RAID-0/şeritli ayarı tooincrease IOPS Hello veri diski oluşturun.
- Azure yük dengeleyici toobalance hello yük hello üç düğümleri için kullanın.
- toominimize yineleyen iş, MariaDB + Galera içeren bir VM görüntüsü oluşturmanız ve onu kullanmanız toocreate hello diğer küme VM'ler.

![Sistem Mimarisi](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> Bu konuda hello kullanan [Azure CLI](../../../cli-install-nodejs.md) araçları, bu nedenle emin toodownload olun bunları ve bunları tooyour Azure aboneliği according toohello yönergeleri bağlayın. Merhaba hello Azure CLI kullanılabilir bir başvuru toohello komutları gerekirse bkz [Azure CLI komut başvurusu](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2). Ayrıca çok gerekir[kimlik doğrulaması için SSH anahtarı oluşturma] ve hello .pem dosya konumunu not edin.
>
>

## <a name="create-hello-template"></a>Merhaba şablonu oluşturma
### <a name="infrastructure"></a>Altyapı
1. Bir benzeşim grubu toohold hello kaynakları birlikte oluşturun.

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. Bir sanal ağ oluşturun.

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. Bir depolama hesabı toohost bizim tüm diskleri oluşturun. Birden fazla 40 yoğun olarak kullanılan diskler üzerinde hello yerleştirdiğiniz döndürmemelidir hello 20.000 IOPS depolama hesabı sınırı basarsa aynı depolama hesabı tooavoid. Bu durumda, her şeyi kolaylık sağlamak için aynı hesabı hello depolayacağınız için o sınırın altına iyi demektir.

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. Merhaba CentOS 7 sanal makine görüntüsü Hello adını bulun.

        azure vm image list | findstr CentOS
   Merhaba çıktı aşağıdakine benzer olacaktır `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.

   Bu adı adım aşağıdaki hello kullanabilirsiniz.
5. Merhaba VM şablonu oluşturma ve /path/to/key.pem oluşturulan hello .pem SSH anahtarı saklandığı hello yolu ile değiştirin.

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. Merhaba RAID yapılandırması kullanmak için dört 500 GB veri diskleri toohello VM ekleyin.

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. SSH toosign toohello şablonu mariadbhatemplate.cloudapp.net:22 sırasında oluşturulan VM kullanın ve özel anahtarınızı kullanarak bağlanın.

### <a name="software"></a>Yazılım
1. Merhaba kök alın.

        sudo su

2. RAID desteği yükleyin:

    a. Mdadm yükleyin.

              yum install mdadm

    b. Merhaba RADI0/stripe yapılandırmasını EXT4 dosya sistemi ile oluşturun.

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    c. Merhaba bağlama noktası dizini oluşturun.

              mkdir /mnt/data
    d. Yeni oluşturulan hello RAID aygıtı UUID'si Hello alın.

              blkid | grep /dev/md0
    e. /Etc/fstab düzenleyin.

              vi /etc/fstab
    f. Merhaba değerle hello UUID değiştirme başlatmada takma hello aygıt tooenable otomatik elde hello önceki eklemek **blkid** komutu.

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    g. Merhaba yeni bölüm bağlayın.

              mount /mnt/data

3. MariaDB yükleyin.

    a. Merhaba MariaDB.repo dosyası oluşturun.

                vi /etc/yum.repos.d/MariaDB.repo

    b. Merhaba depodaki dosya içeriği aşağıdaki hello ile doldurun:

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    c. tooavoid çakışmaları, varolan sonek ve mariadb kitaplıklar kaldırın.

           yum remove postfix mariadb-libs-*
    d. MariaDB Galera ile yükleyin.

           yum install MariaDB-Galera-server MariaDB-client galera

4. Merhaba MySQL veri dizini toohello RAID blok aygıtı taşıyın.

    a. Merhaba geçerli MySQL dizini yeni konumuna kopyalayın ve hello eski dizini kaldırın.

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    b. Merhaba yeni dizin izinlerini uygun şekilde ayarlayın.

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    c. Merhaba eski dizin toohello yeni konumunda hello RAID bölüm işaret eden bir simgesel oluşturun.

           ln -s /mnt/data/mysql /var/lib/mysql

5. Çünkü [SELinux uğratan hello küme işlemleriyle](http://galeracluster.com/documentation-webpages/configuration.html#selinux), gerekli toodisable olan hello geçerli oturum için. Düzen `/etc/selinux/config` toodisable sonraki yeniden başlatmalar için.

            setenforce 0

            then editing `/etc/selinux/config` tooset `SELINUX=permissive`
6. MySQL çalıştırır doğrulayın.

   a. MySQL başlatın.

           service mysql start
   b. Merhaba MySQL yükleme güvenli, hello kök parola ayarlama, anonim kullanıcılar toodisable uzak kök oturumu kaldırın ve hello test veritabanını kaldır.

           mysql_secure_installation
   c. Merhaba veritabanında küme işlemleri için ve isteğe bağlı olarak, uygulamalarınız için bir kullanıcı oluşturun.

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* too'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   d. MySQL durdurun.

            service mysql stop
7. Bir yapılandırma yer tutucu oluşturun.

   a. Merhaba MySQL yapılandırma toocreate hello küme ayarları için bir yer tutucu düzenleyin. Merhaba değiştirmeyin  **`<Variables>`**  veya artık açıklamadan çıkarın. Bu şablonu kullanarak bir VM oluşturduktan sonra gerçekleşir.

            vi /etc/my.cnf.d/server.cnf
   b. Merhaba Düzenle  **[galera]**  bölümünde ve temizleyin.

   c. Merhaba Düzenle **[mariadb]** bölümü.

           wsrep_provider=/usr/lib64/galera/libgalera_smm.so
           binlog_format=ROW
           wsrep_sst_method=rsync
           bind-address=0.0.0.0 # When set too0.0.0.0, hello server listens tooremote connections
           default_storage_engine=InnoDB
           innodb_autoinc_lock_mode=2

           wsrep_sst_auth=cluster:p@ssw0rd # CHANGE: Username and password you created for hello SST cluster MySQL user
           #wsrep_cluster_name='mariadbcluster' # CHANGE: Uncomment and set your desired cluster name
           #wsrep_cluster_address="gcomm://mariadb1,mariadb2,mariadb3" # CHANGE: Uncomment and Add all your servers
           #wsrep_node_address='<ServerIP>' # CHANGE: Uncomment and set IP address of this server
           #wsrep_node_name='<NodeName>' # CHANGE: Uncomment and set hello node name of this server
8. Merhaba Güvenlik Duvarı'nda gerekli bağlantı noktaları üzerinde CentOS 7 FirewallD kullanarak açın.

   * MySQL:`firewall-cmd --zone=public --add-port=3306/tcp --permanent`
   * GALERA:`firewall-cmd --zone=public --add-port=4567/tcp --permanent`
   * GALERA IST:`firewall-cmd --zone=public --add-port=4568/tcp --permanent`
   * RSYNC:`firewall-cmd --zone=public --add-port=4444/tcp --permanent`
   * Merhaba Güvenlik Duvarı'nı yeniden yükleyin:`firewall-cmd --reload`

9. Merhaba sistem performansı en iyi duruma getirme. Daha fazla bilgi için bkz: [performans stratejisi ayarlama](optimize-mysql.md).

   a. Merhaba MySQL yapılandırma dosyasını yeniden düzenleyin.

            vi /etc/my.cnf.d/server.cnf
   b. Merhaba Düzenle **[mariadb]** bölümünde ve içeriği aşağıdaki hello ekleyin:

   > [!NOTE]
   > Bu innodb öneririz\_arabellek\_pool_size olan VM bellek yüzde 70 '. Merhaba Orta 3.5 GB RAM'i olan Azure VM için bu örnekte, 2,45 GB olarak ayarlandı.
   >
   >

           innodb_buffer_pool_size = 2508M # hello buffer pool contains buffered data and hello index. This is usually set too70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give hello server more time toorecycle idled connections
           innodb_file_per_table = 1 # Speed up hello table space transmission and optimize hello debris management performance
           innodb_log_buffer_size = 128M # hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit
           innodb_flush_log_at_trx_commit = 2 # hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. MySQL durdurun, hello küme bir düğüm eklerken kesintiye başlangıç tooavoid üzerinde çalışmasını MySQL hizmetini devre dışı bırakın ve hello makine sağlamayı sonlandırın.

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. Merhaba VM hello portal üzerinden yakalayın. (Şu anda [#1268 hello Azure CLI araçlarında sorun](https://github.com/Azure/azure-xplat-cli/issues/1268) hello Azure CLI araçlarını tarafından yakalanan görüntüleri bağlı hello veri diskleri yakalamayın hello olgu açıklanmaktadır.)

    a. Merhaba portal üzerinden hello makineyi kapatın.

    b. Tıklatın **yakalama** ve hello görüntü adı olarak belirtmeniz **mariadb galera görüntü**. Bir açıklama girin ve denetimi "Waagent Çalıştır."
      
      ![Merhaba sanal makinesi yakalama](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-hello-cluster"></a>Merhaba kümesi oluşturma
Üç VM'ler ile oluşturulan ve yapılandırmak ve hello küme Başlat hello şablonu oluşturun.

1. Merhaba mariadb galera görüntü ilk CentOS 7 VM'den görüntü oluşturduğunuz, aşağıdaki bilgilerle hello sağlama hello oluşturun:

 - Sanal ağ adı: mariadbvnet
 - Alt ağ: mariadb
 - Makine boyutu: Orta
 - Bulut hizmet adı: mariadbha (veya mariadbha.cloudapp.net erişilen toobe istediğiniz ne olursa olsun adı)
 - Makine adı: mariadb1
 - Kullanıcı adı: azureuser
 - SSH erişimini: etkin
 - Merhaba SSH sertifika .pem dosyasını geçirerek ve /path/to/key.pem hello saklandığı hello yolu ile değiştirerek .pem SSH anahtarı oluşturulur.

   > [!NOTE]
   > Merhaba aşağıdaki komutları daha anlaşılır olması için birden çok satır üzerinden bölünür, ancak her bir satır olarak girmeniz gerekir.
   >
   >
        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 22
        --vm-name mariadb1
        mariadbha mariadb-galera-image azureuser
2. Toohello mariadbha bulut hizmetine bağlanarak iki daha fazla sanal makine oluşturun. Değişiklik hello VM adı ve SSH bağlantı noktası tooa benzersiz bağlantı noktası ile diğer VM'lerin değil çakışan hello aynı bulut hizmetine hello.

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 23
        --vm-name mariadb2
        --connect mariadbha mariadb-galera-image azureuser
  MariaDB3 için:

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 24
        --vm-name mariadb3
        --connect mariadbha mariadb-galera-image azureuser
3. Merhaba sonraki adımda tooget hello iç IP adresi her bir hello üç VM'ler gerekir:

    ![IP adresi alınıyor](./media/mariadb-mysql-cluster/IP.png)
4. SSH toosign toohello üç Vm'lerde kullanın ve bunların her birini hello yapılandırma dosyasını düzenleyin.

        sudo vi /etc/my.cnf.d/server.cnf

    Açıklamadan çıkarın  **`wsrep_cluster_name`**  ve  **`wsrep_cluster_address`**  hello kaldırarak  **#**  hello başında başlangıç satırı.
    Ayrıca, yerine  **`<ServerIP>`**  içinde  **`wsrep_node_address`**  ve  **`<NodeName>`**  içinde  **`wsrep_node_name`**  hello ile Sanal makinenin IP adresi ve adı, sırasıyla ve de bu satırlardaki yorumları kaldırın.
5. Hello küme üzerinde MariaDB1 başlatmak ve başlangıçta çalışmasına izin verin.

        sudo service mysql bootstrap
        chkconfig mysql on
6. MySQL MariaDB2 ve MariaDB3 başlatmak ve başlangıçta çalışmasına izin verin.

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-hello-cluster"></a>Yük Dengeleme hello küme
Kümelenmiş hello VM'ler oluşturduğunuzda, clusteravset tooensure farklı hata ve güncelleştirme etki alanlarında konmuş ve Azure hiçbir zaman bakım tüm makinelerde aynı anda yaptığı adlı bir kullanılabilirlik kümesine eklenir. Bu yapılandırma toobe hello Azure hizmet düzeyi sözleşmesi (SLA) tarafından desteklenen hello gereksinimleri karşılıyor.

Artık Azure yük dengeleyici toobalance istekleri hello üç düğümler arasında kullanır.

Hello Azure CLI kullanarak komutları makinenizde aşağıdaki hello çalıştırın.

Merhaba komut parametreleri yapıdır:`azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

Merhaba CLI biraz uzun olabilecek hello yük dengeleyici yoklama aralığı too15 saniye cinsinden ayarlar. Merhaba portalında altında değiştirme **uç noktaları** herhangi bir hello VM'ler için.

![Uç noktayı Düzenle](./media/mariadb-mysql-cluster/Endpoint.PNG)

Seçin **RECONFIGURE hello yük dengelemeli mimarilerde ayarlamak**.

![Yeniden hello yük dengeli kümesi](./media/mariadb-mysql-cluster/Endpoint2.PNG)

Değişiklik **yoklama aralığı** too5 saniye ve değişikliklerinizi kaydedin.

![Değiştirme yoklama aralığı](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-hello-cluster"></a>Merhaba küme doğrulama
Merhaba sabit çalışma yapılır. Merhaba küme olmalıdır şimdi en erişilebilir `mariadbha.cloudapp.net:3306`hello yük dengeleyici isabetler ve rota istekleri arasında sorunsuz ve verimli bir şekilde üç VM'ler hello.

Sık kullanılan MySQL istemci tooconnect kullanın veya bu küme çalışma hello VM'ler tooverify birinden bağlanın.

     mysql -u cluster -h mariadbha.cloudapp.net -p

Ardından bir veritabanı oluşturun ve bazı verilerle doldurmak.

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

oluşturduğunuz hello veritabanı aşağıdaki tablonun hello döndürür:

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, bir üç düğümü MariaDB oluşturulan + Galera yüksek oranda kullanılabilir küme sanal Azure üzerinde çalışan CentOS 7 makineleri. Merhaba VM'ler Azure yük dengeleyici ile dengeleneceğini.

Konumundaki toolook isteyebilirsiniz [başka bir şekilde toocluster Linux'ta MySQL](mysql-cluster.md) ve yolları çok[iyileştirmek ve Azure Linux VM'ler MySQL performansı test](optimize-mysql.md).

<!--Anchors-->
[Architecture overview]:#architecture-overview
[Creating hello template]:#creating-the-template
[Creating hello cluster]:#creating-the-cluster
[Load balancing hello cluster]:#load-balancing-the-cluster
[Validating hello cluster]:#validating-the-cluster
[Next steps]:#next-steps

<!--Image references-->

<!--Link references-->
[Galera]:http://galeracluster.com/products/
[MariaDBs]:https://mariadb.org/en/about/
[kimlik doğrulaması için SSH anahtarı oluşturma]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/
[issue #1268 in hello Azure CLI]:https://github.com/Azure/azure-xplat-cli/issues/1268
