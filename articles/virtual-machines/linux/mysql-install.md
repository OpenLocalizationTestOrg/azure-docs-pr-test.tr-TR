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
# <a name="how-tooinstall-mysql-on-azure"></a><span data-ttu-id="d81bf-103">Nasıl tooinstall Azure üzerinde MySQL</span><span class="sxs-lookup"><span data-stu-id="d81bf-103">How tooinstall MySQL on Azure</span></span>
<span data-ttu-id="d81bf-104">Bu makalede, öğreneceksiniz nasıl tooinstall ve MySQL Linux çalıştıran Azure sanal makinesi üzerinde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d81bf-104">In this article, you will learn how tooinstall and configure MySQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a><span data-ttu-id="d81bf-105">MySQL sanal makinenize yükleyin</span><span class="sxs-lookup"><span data-stu-id="d81bf-105">Install MySQL on your virtual machine</span></span>
> [!NOTE]
> <span data-ttu-id="d81bf-106">Bu öğretici sipariş toocomplete Linux çalıştıran bir Microsoft Azure sanal makine zaten olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d81bf-106">You must already have a Microsoft Azure virtual machine running Linux in order toocomplete this tutorial.</span></span> <span data-ttu-id="d81bf-107">Lütfen bakın [Azure Linux VM'de öğretici](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate ve bir Linux VM ile ayarlama `mysqlnode` hello VM adı olarak ve `azureuser` devam etmeden önce kullanıcı olarak.</span><span class="sxs-lookup"><span data-stu-id="d81bf-107">Please see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate and set up a Linux VM with `mysqlnode` as hello VM name and `azureuser` as user before proceeding.</span></span>
> 
> 

<span data-ttu-id="d81bf-108">Bu durumda, 3306 bağlantı noktası hello MySQL bağlantı noktası kullanın.</span><span class="sxs-lookup"><span data-stu-id="d81bf-108">In this case, use 3306 port as hello MySQL port.</span></span>  

<span data-ttu-id="d81bf-109">Toohello Linux putty üzerinden oluşturulan VM bağlayın.</span><span class="sxs-lookup"><span data-stu-id="d81bf-109">Connect toohello Linux VM you created via putty.</span></span> <span data-ttu-id="d81bf-110">Bu hello Azure Linux VM'de kullandığınız ilk kez kullanıyorsanız, bkz: toouse putty tooa Linux VM nasıl bağlanacağını [burada](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d81bf-110">If this is hello first time you use Azure Linux VM, see how toouse putty connect tooa Linux VM [here](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d81bf-111">Bu makaledeki örnek depo paket tooinstall MySQL5.6 kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="d81bf-111">We will use repository package tooinstall MySQL5.6 as an example in this article.</span></span> <span data-ttu-id="d81bf-112">Aslında, MySQL5.6 performans MySQL5.5'den daha fazla geliştirme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d81bf-112">Actually, MySQL5.6 has more improvement in performance than MySQL5.5.</span></span>  <span data-ttu-id="d81bf-113">Daha fazla bilgi [burada](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span><span class="sxs-lookup"><span data-stu-id="d81bf-113">More information [here](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span></span>

### <a name="how-tooinstall-mysql56-on-ubuntu"></a><span data-ttu-id="d81bf-114">Nasıl tooinstall MySQL5.6 Ubuntu üzerinde</span><span class="sxs-lookup"><span data-stu-id="d81bf-114">How tooinstall MySQL5.6 on Ubuntu</span></span>
<span data-ttu-id="d81bf-115">Linux VM Ubuntu Azure ile burada kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="d81bf-115">We will use Linux VM with Ubuntu from Azure here.</span></span>

* <span data-ttu-id="d81bf-116">1. adım: Yükleme MySQL Server 5.6 çok geçiş`root` kullanıcı:</span><span class="sxs-lookup"><span data-stu-id="d81bf-116">Step 1: Install MySQL Server 5.6   Switch too`root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="d81bf-117">MySQL server 5.6 yükleyin:</span><span class="sxs-lookup"><span data-stu-id="d81bf-117">Install mysql-server 5.6:</span></span>
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    <span data-ttu-id="d81bf-118">Yükleme sırasında bir iletişim penceresi poping görürsünüz tooask tooset MySQL kök parolayla aşağıdaki ve hello parola Burada ayarlanan.</span><span class="sxs-lookup"><span data-stu-id="d81bf-118">During installation, you will see a dialog window poping up tooask you tooset MySQL root password below, and you need set hello password here.</span></span>
  
    ![Görüntü](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    <span data-ttu-id="d81bf-120">Giriş hello parola yeniden tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="d81bf-120">Input hello password again tooconfirm.</span></span>

    ![Görüntü](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* <span data-ttu-id="d81bf-122">2. adım: Oturum açma MySQL sunucusu</span><span class="sxs-lookup"><span data-stu-id="d81bf-122">Step 2: Login MySQL Server</span></span>
  
    <span data-ttu-id="d81bf-123">MySQL sunucusu yüklemesi tamamlandığında, MySQL hizmeti otomatik olarak başlatılır.</span><span class="sxs-lookup"><span data-stu-id="d81bf-123">When MySQL server installation finished, MySQL service will be started automatically.</span></span> <span data-ttu-id="d81bf-124">MySQL Server ile oturum açabileceğiniz `root` kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="d81bf-124">You can login MySQL Server with `root` user.</span></span>
    <span data-ttu-id="d81bf-125">Komut toologin ve giriş parola aşağıda Hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="d81bf-125">Use hello below command toologin and input password.</span></span>
  
             #[root@mysqlnode ~]# mysql -uroot -p
* <span data-ttu-id="d81bf-126">3. adım: MySQL hizmetini çalıştıran hello yönetme</span><span class="sxs-lookup"><span data-stu-id="d81bf-126">Step 3: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="d81bf-127">(a) MySQL hizmetinin durumunu Al</span><span class="sxs-lookup"><span data-stu-id="d81bf-127">(a) Get status of MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql status
  
    <span data-ttu-id="d81bf-128">(b) MySQL hizmetini başlatın</span><span class="sxs-lookup"><span data-stu-id="d81bf-128">(b) Start MySQL Service</span></span>
  
             #[root@mysqlnode ~]# service mysql start
  
    <span data-ttu-id="d81bf-129">(c) MySQL hizmetini durdurun</span><span class="sxs-lookup"><span data-stu-id="d81bf-129">(c) Stop MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql stop
  
    <span data-ttu-id="d81bf-130">(d) hello MySQL hizmetini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="d81bf-130">(d) Restart hello MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-tooinstall-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a><span data-ttu-id="d81bf-131">Nasıl tooinstall MySQL Red Hat işletim sistemi ailesi üzerinde ister CentOS, Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="d81bf-131">How tooinstall MySQL on Red Hat OS family like CentOS, Oracle Linux</span></span>
<span data-ttu-id="d81bf-132">Linux VM CentOS veya Oracle Linux burada kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="d81bf-132">We will use Linux VM with CentOS or Oracle Linux here.</span></span>

* <span data-ttu-id="d81bf-133">1. adım: hello MySQL Yum Depo anahtarı çok ekleme`root` kullanıcı:</span><span class="sxs-lookup"><span data-stu-id="d81bf-133">Step 1: Add hello MySQL Yum repository   Switch too`root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="d81bf-134">Karşıdan yükleyip hello MySQL yayın paketi:</span><span class="sxs-lookup"><span data-stu-id="d81bf-134">Download and install hello MySQL release package:</span></span>
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* <span data-ttu-id="d81bf-135">2. adım: dosya tooenable hello MySQL deposu hello MySQL5.6 paketini karşıdan yüklemek için aşağıda düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="d81bf-135">Step 2: Edit below file tooenable hello MySQL repository for downloading hello MySQL5.6 package.</span></span>
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    <span data-ttu-id="d81bf-136">Bu dosya toobelow her değerini güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="d81bf-136">Update each value of this file toobelow:</span></span>
  
        \# *Enable toouse MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* <span data-ttu-id="d81bf-137">3. adım: Yükleme MySQL yüklemek MySQL MySQL depodan:</span><span class="sxs-lookup"><span data-stu-id="d81bf-137">Step 3: Install MySQL from MySQL repository   Install MySQL:</span></span>
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    <span data-ttu-id="d81bf-138">MySQL RPM paketi ve tüm ilişkili paketleri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="d81bf-138">MySQL RPM package and all related packages will be installed.</span></span>
* <span data-ttu-id="d81bf-139">4. adım: MySQL hizmetini çalıştıran hello yönetme</span><span class="sxs-lookup"><span data-stu-id="d81bf-139">Step 4: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="d81bf-140">(a) hello MySQL server hello hizmet durumunu kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="d81bf-140">(a) Check hello service status of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]#service mysqld status
  
    <span data-ttu-id="d81bf-141">(b) hello varsayılan bağlantı noktası, MySQL server çalışıp çalışmadığını kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="d81bf-141">(b) Check whether hello default port of  MySQL server is running:</span></span>
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    <span data-ttu-id="d81bf-142">(c) hello MySQL server başlatın:</span><span class="sxs-lookup"><span data-stu-id="d81bf-142">(c) Start hello MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld start

    <span data-ttu-id="d81bf-143">(d) hello MySQL server durdurun:</span><span class="sxs-lookup"><span data-stu-id="d81bf-143">(d) Stop hello MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld stop

    <span data-ttu-id="d81bf-144">(e) MySQL toostart hello sistem önyükleme li ayarlanır:</span><span class="sxs-lookup"><span data-stu-id="d81bf-144">(e) Set MySQL toostart when hello system boot-up:</span></span>

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-tooinstall-mysql-on-suse-linux"></a><span data-ttu-id="d81bf-145">Nasıl tooinstall MySQL SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="d81bf-145">How tooinstall MySQL on SUSE Linux</span></span>
<span data-ttu-id="d81bf-146">Linux VM ile OpenSUSE burada kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="d81bf-146">We will use Linux VM with OpenSUSE here.</span></span>

* <span data-ttu-id="d81bf-147">1. adım: MySQL Server yükleyip</span><span class="sxs-lookup"><span data-stu-id="d81bf-147">Step 1: Download and install MySQL Server</span></span>
  
    <span data-ttu-id="d81bf-148">Çok geçiş`root` komutu altındaki kullanıcı arabiriminden:</span><span class="sxs-lookup"><span data-stu-id="d81bf-148">Switch too`root` user through below command:</span></span>  
  
           #sudo su -
  
    <span data-ttu-id="d81bf-149">Paketini indirin ve MySQL yükleyin:</span><span class="sxs-lookup"><span data-stu-id="d81bf-149">Download and install MySQL package:</span></span>
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* <span data-ttu-id="d81bf-150">2. adım: MySQL hizmetini çalıştıran hello yönetme</span><span class="sxs-lookup"><span data-stu-id="d81bf-150">Step 2: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="d81bf-151">(a) hello MySQL server hello durumunu kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="d81bf-151">(a) Check hello status of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]# rcmysql status
  
    <span data-ttu-id="d81bf-152">(b) onay olup hello hello MySQL server varsayılan bağlantı noktası:</span><span class="sxs-lookup"><span data-stu-id="d81bf-152">(b) Check whether hello default port of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    <span data-ttu-id="d81bf-153">(c) hello MySQL server başlatın:</span><span class="sxs-lookup"><span data-stu-id="d81bf-153">(c) Start hello MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql start

    <span data-ttu-id="d81bf-154">(d) hello MySQL server durdurun:</span><span class="sxs-lookup"><span data-stu-id="d81bf-154">(d) Stop hello MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql stop

    <span data-ttu-id="d81bf-155">(e) MySQL toostart hello sistem önyükleme li ayarlanır:</span><span class="sxs-lookup"><span data-stu-id="d81bf-155">(e) Set MySQL toostart when hello system boot-up:</span></span>

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a><span data-ttu-id="d81bf-156">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="d81bf-156">Next Step</span></span>
<span data-ttu-id="d81bf-157">Daha fazla kullanım ve MySQL ile ilgili bilgileri bulmak [burada](https://www.mysql.com/).</span><span class="sxs-lookup"><span data-stu-id="d81bf-157">Find more usage and information regarding MySQL [Here](https://www.mysql.com/).</span></span>

