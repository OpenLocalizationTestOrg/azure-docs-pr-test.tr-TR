---
title: "bir Linux VM Azure üzerinde MySQL yukarı aaaSet | Microsoft Docs"
description: "Nasıl tooinstall hello MySQL yığın azure'da bir Linux sanal makine (Ubuntu veya RedHat ailesi işletim sistemi) hakkında bilgi edinin"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 153bae7c-897b-46b3-bd86-192a6efb94fa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: e47d0de7f0eb5bb873ad20e4bc35f1b5f8d33bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-mysql-on-azure"></a>Nasıl tooinstall Azure üzerinde MySQL
Bu makalede, öğreneceksiniz nasıl tooinstall ve MySQL Linux çalıştıran Azure sanal makinesi üzerinde yapılandırın.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a>MySQL sanal makinenize yükleyin
> [!NOTE]
> Bu öğretici sipariş toocomplete Linux çalıştıran bir Microsoft Azure sanal makine zaten olmalıdır. Lütfen bakın [Azure Linux VM'de öğretici](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate ve bir Linux VM ile ayarlama `mysqlnode` hello VM adı olarak ve `azureuser` devam etmeden önce kullanıcı olarak.
> 
> 

Bu durumda, 3306 bağlantı noktası hello MySQL bağlantı noktası kullanın.  

Toohello Linux putty üzerinden oluşturulan VM bağlayın. Bu hello Azure Linux VM'de kullandığınız ilk kez kullanıyorsanız, bkz: toouse putty tooa Linux VM nasıl bağlanacağını [burada](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Bu makaledeki örnek depo paket tooinstall MySQL5.6 kullanacağız. Aslında, MySQL5.6 performans MySQL5.5'den daha fazla geliştirme sahiptir.  Daha fazla bilgi [burada](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).

### <a name="how-tooinstall-mysql56-on-ubuntu"></a>Nasıl tooinstall MySQL5.6 Ubuntu üzerinde
Linux VM Ubuntu Azure ile burada kullanacağız.

* 1. adım: Yükleme MySQL Server 5.6 çok geçiş`root` kullanıcı:
  
            #[azureuser@mysqlnode:~]sudo su -
  
    MySQL server 5.6 yükleyin:
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    Yükleme sırasında bir iletişim penceresi poping görürsünüz tooask tooset MySQL kök parolayla aşağıdaki ve hello parola Burada ayarlanan.
  
    ![Görüntü](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    Giriş hello parola yeniden tooconfirm.

    ![Görüntü](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* 2. adım: Oturum açma MySQL sunucusu
  
    MySQL sunucusu yüklemesi tamamlandığında, MySQL hizmeti otomatik olarak başlatılır. MySQL Server ile oturum açabileceğiniz `root` kullanıcı.
    Komut toologin ve giriş parola aşağıda Hello kullanın.
  
             #[root@mysqlnode ~]# mysql -uroot -p
* 3. adım: MySQL hizmetini çalıştıran hello yönetme
  
    (a) MySQL hizmetinin durumunu Al
  
             #[root@mysqlnode ~]# service mysql status
  
    (b) MySQL hizmetini başlatın
  
             #[root@mysqlnode ~]# service mysql start
  
    (c) MySQL hizmetini durdurun
  
             #[root@mysqlnode ~]# service mysql stop
  
    (d) hello MySQL hizmetini yeniden başlatın
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-tooinstall-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a>Nasıl tooinstall MySQL Red Hat işletim sistemi ailesi üzerinde ister CentOS, Oracle Linux
Linux VM CentOS veya Oracle Linux burada kullanacağız.

* 1. adım: hello MySQL Yum Depo anahtarı çok ekleme`root` kullanıcı:
  
            #[azureuser@mysqlnode:~]sudo su -
  
    Karşıdan yükleyip hello MySQL yayın paketi:
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* 2. adım: dosya tooenable hello MySQL deposu hello MySQL5.6 paketini karşıdan yüklemek için aşağıda düzenleyin.
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    Bu dosya toobelow her değerini güncelleştirin:
  
        \# *Enable toouse MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* 3. adım: Yükleme MySQL yüklemek MySQL MySQL depodan:
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    MySQL RPM paketi ve tüm ilişkili paketleri yüklenir.
* 4. adım: MySQL hizmetini çalıştıran hello yönetme
  
    (a) hello MySQL server hello hizmet durumunu kontrol edin:
  
           #[root@mysqlnode ~]#service mysqld status
  
    (b) hello varsayılan bağlantı noktası, MySQL server çalışıp çalışmadığını kontrol edin:
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    (c) hello MySQL server başlatın:

           #[root@mysqlnode ~]#service mysqld start

    (d) hello MySQL server durdurun:

           #[root@mysqlnode ~]#service mysqld stop

    (e) MySQL toostart hello sistem önyükleme li ayarlanır:

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-tooinstall-mysql-on-suse-linux"></a>Nasıl tooinstall MySQL SUSE Linux
Linux VM ile OpenSUSE burada kullanacağız.

* 1. adım: MySQL Server yükleyip
  
    Çok geçiş`root` komutu altındaki kullanıcı arabiriminden:  
  
           #sudo su -
  
    Paketini indirin ve MySQL yükleyin:
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* 2. adım: MySQL hizmetini çalıştıran hello yönetme
  
    (a) hello MySQL server hello durumunu kontrol edin:
  
           #[root@mysqlnode ~]# rcmysql status
  
    (b) onay olup hello hello MySQL server varsayılan bağlantı noktası:
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    (c) hello MySQL server başlatın:

           #[root@mysqlnode ~]# rcmysql start

    (d) hello MySQL server durdurun:

           #[root@mysqlnode ~]# rcmysql stop

    (e) MySQL toostart hello sistem önyükleme li ayarlanır:

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a>Sonraki adım
Daha fazla kullanım ve MySQL ile ilgili bilgileri bulmak [burada](https://www.mysql.com/).

