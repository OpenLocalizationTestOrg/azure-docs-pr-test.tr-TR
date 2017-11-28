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
# <a name="mariadb-mysql-cluster-azure-tutorial"></a><span data-ttu-id="c79d4-103">MariaDB (MySQL) küme: Azure Öğreticisi</span><span class="sxs-lookup"><span data-stu-id="c79d4-103">MariaDB (MySQL) cluster: Azure tutorial</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c79d4-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager](../../../resource-manager-deployment-model.md) ve klasik.</span><span class="sxs-lookup"><span data-stu-id="c79d4-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="c79d4-105">Bu makalede, hello Klasik dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="c79d4-105">This article covers hello classic deployment model.</span></span> <span data-ttu-id="c79d4-106">Microsoft, en yeni dağıtımların hello Azure Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="c79d4-106">Microsoft recommends that most new deployments use hello Azure Resource Manager model.</span></span>

> [!NOTE]
> <span data-ttu-id="c79d4-107">MariaDB Kurumsal küme hello Azure Marketi'nde kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="c79d4-107">MariaDB Enterprise cluster is now available in hello Azure Marketplace.</span></span> <span data-ttu-id="c79d4-108">Merhaba yenilik MariaDB Galera küme üzerinde Azure Resource Manager otomatik olarak dağıtacaktır.</span><span class="sxs-lookup"><span data-stu-id="c79d4-108">hello new offering will automatically deploy a MariaDB Galera cluster on Azure Resource Manager.</span></span> <span data-ttu-id="c79d4-109">Merhaba yenilik gelen kullanması gereken [Azure Marketi](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span><span class="sxs-lookup"><span data-stu-id="c79d4-109">You should use hello new offering from [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span></span>
>
>

<span data-ttu-id="c79d4-110">Bu makale size nasıl gösterir toocreate çok asıl [Galera](http://galeracluster.com/products/) kümesinin [MariaDBs](https://mariadb.org/en/about/) (MySQL için güçlü, ölçeklenebilir ve güvenilir içeri kayma yenileme) Azure üzerinde yüksek oranda kullanılabilir bir ortamda toowork sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="c79d4-110">This article shows you how toocreate a multi-Master [Galera](http://galeracluster.com/products/) cluster of [MariaDBs](https://mariadb.org/en/about/) (a robust, scalable, and reliable drop-in replacement for MySQL) toowork in a highly available environment on Azure virtual machines.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="c79d4-111">Mimariye genel bakış</span><span class="sxs-lookup"><span data-stu-id="c79d4-111">Architecture overview</span></span>
<span data-ttu-id="c79d4-112">Bu makalede nasıl toocomplete hello aşağıdaki adımları açıklanır:</span><span class="sxs-lookup"><span data-stu-id="c79d4-112">This article describes how toocomplete hello following steps:</span></span>

- <span data-ttu-id="c79d4-113">Üç düğümlü bir küme oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c79d4-113">Create a three-node cluster.</span></span>
- <span data-ttu-id="c79d4-114">Veri disklerinden hello işletim sistemi diski ayrı hello.</span><span class="sxs-lookup"><span data-stu-id="c79d4-114">Separate hello data disks from hello OS disk.</span></span>
- <span data-ttu-id="c79d4-115">RAID-0/şeritli ayarı tooincrease IOPS Hello veri diski oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c79d4-115">Create hello data disks in RAID-0/striped setting tooincrease IOPS.</span></span>
- <span data-ttu-id="c79d4-116">Azure yük dengeleyici toobalance hello yük hello üç düğümleri için kullanın.</span><span class="sxs-lookup"><span data-stu-id="c79d4-116">Use Azure Load Balancer toobalance hello load for hello three nodes.</span></span>
- <span data-ttu-id="c79d4-117">toominimize yineleyen iş, MariaDB + Galera içeren bir VM görüntüsü oluşturmanız ve onu kullanmanız toocreate hello diğer küme VM'ler.</span><span class="sxs-lookup"><span data-stu-id="c79d4-117">toominimize repetitive work, create a VM image that contains MariaDB + Galera and use it toocreate hello other cluster VMs.</span></span>

![Sistem Mimarisi](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> <span data-ttu-id="c79d4-119">Bu konuda hello kullanan [Azure CLI](../../../cli-install-nodejs.md) araçları, bu nedenle emin toodownload olun bunları ve bunları tooyour Azure aboneliği according toohello yönergeleri bağlayın.</span><span class="sxs-lookup"><span data-stu-id="c79d4-119">This topic uses hello [Azure CLI](../../../cli-install-nodejs.md) tools, so make sure toodownload them and connect them tooyour Azure subscription according toohello instructions.</span></span> <span data-ttu-id="c79d4-120">Merhaba hello Azure CLI kullanılabilir bir başvuru toohello komutları gerekirse bkz [Azure CLI komut başvurusu](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="c79d4-120">If you need a reference toohello commands available in hello Azure CLI, see hello [Azure CLI command reference](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="c79d4-121">Ayrıca çok gerekir[kimlik doğrulaması için SSH anahtarı oluşturma] ve hello .pem dosya konumunu not edin.</span><span class="sxs-lookup"><span data-stu-id="c79d4-121">You will also need too[create an SSH key for authentication] and make note of hello .pem file location.</span></span>
>
>

## <a name="create-hello-template"></a><span data-ttu-id="c79d4-122">Merhaba şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="c79d4-122">Create hello template</span></span>
### <a name="infrastructure"></a><span data-ttu-id="c79d4-123">Altyapı</span><span class="sxs-lookup"><span data-stu-id="c79d4-123">Infrastructure</span></span>
1. <span data-ttu-id="c79d4-124">Bir benzeşim grubu toohold hello kaynakları birlikte oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c79d4-124">Create an affinity group toohold hello resources together.</span></span>

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. <span data-ttu-id="c79d4-125">Bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c79d4-125">Create a virtual network.</span></span>

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. <span data-ttu-id="c79d4-126">Bir depolama hesabı toohost bizim tüm diskleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c79d4-126">Create a storage account toohost all our disks.</span></span> <span data-ttu-id="c79d4-127">Birden fazla 40 yoğun olarak kullanılan diskler üzerinde hello yerleştirdiğiniz döndürmemelidir hello 20.000 IOPS depolama hesabı sınırı basarsa aynı depolama hesabı tooavoid.</span><span class="sxs-lookup"><span data-stu-id="c79d4-127">You shouldn't place more than 40 heavily used disks on hello same storage account tooavoid hitting hello 20,000 IOPS storage account limit.</span></span> <span data-ttu-id="c79d4-128">Bu durumda, her şeyi kolaylık sağlamak için aynı hesabı hello depolayacağınız için o sınırın altına iyi demektir.</span><span class="sxs-lookup"><span data-stu-id="c79d4-128">In this case, you're well below that limit, so you'll store everything on hello same account for simplicity.</span></span>

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. <span data-ttu-id="c79d4-129">Merhaba CentOS 7 sanal makine görüntüsü Hello adını bulun.</span><span class="sxs-lookup"><span data-stu-id="c79d4-129">Find hello name of hello CentOS 7 virtual machine image.</span></span>

        azure vm image list | findstr CentOS
   <span data-ttu-id="c79d4-130">Merhaba çıktı aşağıdakine benzer olacaktır `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span><span class="sxs-lookup"><span data-stu-id="c79d4-130">hello output will be something like `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span></span>

   <span data-ttu-id="c79d4-131">Bu adı adım aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c79d4-131">Use that name in hello following step.</span></span>
5. <span data-ttu-id="c79d4-132">Merhaba VM şablonu oluşturma ve /path/to/key.pem oluşturulan hello .pem SSH anahtarı saklandığı hello yolu ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c79d4-132">Create hello VM template and replace /path/to/key.pem with hello path where you stored hello generated .pem SSH key.</span></span>

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. <span data-ttu-id="c79d4-133">Merhaba RAID yapılandırması kullanmak için dört 500 GB veri diskleri toohello VM ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c79d4-133">Attach four 500-GB data disks toohello VM for use in hello RAID configuration.</span></span>

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. <span data-ttu-id="c79d4-134">SSH toosign toohello şablonu mariadbhatemplate.cloudapp.net:22 sırasında oluşturulan VM kullanın ve özel anahtarınızı kullanarak bağlanın.</span><span class="sxs-lookup"><span data-stu-id="c79d4-134">Use SSH toosign in toohello template VM that you created at mariadbhatemplate.cloudapp.net:22, and connect by using your private key.</span></span>

### <a name="software"></a><span data-ttu-id="c79d4-135">Yazılım</span><span class="sxs-lookup"><span data-stu-id="c79d4-135">Software</span></span>
1. <span data-ttu-id="c79d4-136">Merhaba kök alın.</span><span class="sxs-lookup"><span data-stu-id="c79d4-136">Get hello root.</span></span>

        sudo su

2. <span data-ttu-id="c79d4-137">RAID desteği yükleyin:</span><span class="sxs-lookup"><span data-stu-id="c79d4-137">Install RAID support:</span></span>

    <span data-ttu-id="c79d4-138">a.</span><span class="sxs-lookup"><span data-stu-id="c79d4-138">a.</span></span> <span data-ttu-id="c79d4-139">Mdadm yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c79d4-139">Install mdadm.</span></span>

              yum install mdadm

    <span data-ttu-id="c79d4-140">b.</span><span class="sxs-lookup"><span data-stu-id="c79d4-140">b.</span></span> <span data-ttu-id="c79d4-141">Merhaba RADI0/stripe yapılandırmasını EXT4 dosya sistemi ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c79d4-141">Create hello RAID0/stripe configuration with an EXT4 file system.</span></span>

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    <span data-ttu-id="c79d4-142">c.</span><span class="sxs-lookup"><span data-stu-id="c79d4-142">c.</span></span> <span data-ttu-id="c79d4-143">Merhaba bağlama noktası dizini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c79d4-143">Create hello mount point directory.</span></span>

              mkdir /mnt/data
    <span data-ttu-id="c79d4-144">d.</span><span class="sxs-lookup"><span data-stu-id="c79d4-144">d.</span></span> <span data-ttu-id="c79d4-145">Yeni oluşturulan hello RAID aygıtı UUID'si Hello alın.</span><span class="sxs-lookup"><span data-stu-id="c79d4-145">Retrieve hello UUID of hello newly created RAID device.</span></span>

              blkid | grep /dev/md0
    <span data-ttu-id="c79d4-146">e.</span><span class="sxs-lookup"><span data-stu-id="c79d4-146">e.</span></span> <span data-ttu-id="c79d4-147">/Etc/fstab düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="c79d4-147">Edit /etc/fstab.</span></span>

              vi /etc/fstab
    <span data-ttu-id="c79d4-148">f.</span><span class="sxs-lookup"><span data-stu-id="c79d4-148">f.</span></span> <span data-ttu-id="c79d4-149">Merhaba değerle hello UUID değiştirme başlatmada takma hello aygıt tooenable otomatik elde hello önceki eklemek **blkid** komutu.</span><span class="sxs-lookup"><span data-stu-id="c79d4-149">Add hello device tooenable auto mounting on reboot, replacing hello UUID with hello value obtained from hello previous **blkid** command.</span></span>

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    <span data-ttu-id="c79d4-150">g.</span><span class="sxs-lookup"><span data-stu-id="c79d4-150">g.</span></span> <span data-ttu-id="c79d4-151">Merhaba yeni bölüm bağlayın.</span><span class="sxs-lookup"><span data-stu-id="c79d4-151">Mount hello new partition.</span></span>

              mount /mnt/data

3. <span data-ttu-id="c79d4-152">MariaDB yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c79d4-152">Install MariaDB.</span></span>

    <span data-ttu-id="c79d4-153">a.</span><span class="sxs-lookup"><span data-stu-id="c79d4-153">a.</span></span> <span data-ttu-id="c79d4-154">Merhaba MariaDB.repo dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c79d4-154">Create hello MariaDB.repo file.</span></span>

                vi /etc/yum.repos.d/MariaDB.repo

    <span data-ttu-id="c79d4-155">b.</span><span class="sxs-lookup"><span data-stu-id="c79d4-155">b.</span></span> <span data-ttu-id="c79d4-156">Merhaba depodaki dosya içeriği aşağıdaki hello ile doldurun:</span><span class="sxs-lookup"><span data-stu-id="c79d4-156">Fill hello repo file with hello following content:</span></span>

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    <span data-ttu-id="c79d4-157">c.</span><span class="sxs-lookup"><span data-stu-id="c79d4-157">c.</span></span> <span data-ttu-id="c79d4-158">tooavoid çakışmaları, varolan sonek ve mariadb kitaplıklar kaldırın.</span><span class="sxs-lookup"><span data-stu-id="c79d4-158">tooavoid conflicts, remove existing postfix and mariadb-libs.</span></span>

           yum remove postfix mariadb-libs-*
    <span data-ttu-id="c79d4-159">d.</span><span class="sxs-lookup"><span data-stu-id="c79d4-159">d.</span></span> <span data-ttu-id="c79d4-160">MariaDB Galera ile yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c79d4-160">Install MariaDB with Galera.</span></span>

           yum install MariaDB-Galera-server MariaDB-client galera

4. <span data-ttu-id="c79d4-161">Merhaba MySQL veri dizini toohello RAID blok aygıtı taşıyın.</span><span class="sxs-lookup"><span data-stu-id="c79d4-161">Move hello MySQL data directory toohello RAID block device.</span></span>

    <span data-ttu-id="c79d4-162">a.</span><span class="sxs-lookup"><span data-stu-id="c79d4-162">a.</span></span> <span data-ttu-id="c79d4-163">Merhaba geçerli MySQL dizini yeni konumuna kopyalayın ve hello eski dizini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="c79d4-163">Copy hello current MySQL directory into its new location and remove hello old directory.</span></span>

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    <span data-ttu-id="c79d4-164">b.</span><span class="sxs-lookup"><span data-stu-id="c79d4-164">b.</span></span> <span data-ttu-id="c79d4-165">Merhaba yeni dizin izinlerini uygun şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c79d4-165">Set permissions for hello new directory accordingly.</span></span>

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    <span data-ttu-id="c79d4-166">c.</span><span class="sxs-lookup"><span data-stu-id="c79d4-166">c.</span></span> <span data-ttu-id="c79d4-167">Merhaba eski dizin toohello yeni konumunda hello RAID bölüm işaret eden bir simgesel oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c79d4-167">Create a symlink that points hello old directory toohello new location on hello RAID partition.</span></span>

           ln -s /mnt/data/mysql /var/lib/mysql

5. <span data-ttu-id="c79d4-168">Çünkü [SELinux uğratan hello küme işlemleriyle](http://galeracluster.com/documentation-webpages/configuration.html#selinux), gerekli toodisable olan hello geçerli oturum için.</span><span class="sxs-lookup"><span data-stu-id="c79d4-168">Because [SELinux interferes with hello cluster operations](http://galeracluster.com/documentation-webpages/configuration.html#selinux), it is necessary toodisable it for hello current session.</span></span> <span data-ttu-id="c79d4-169">Düzen `/etc/selinux/config` toodisable sonraki yeniden başlatmalar için.</span><span class="sxs-lookup"><span data-stu-id="c79d4-169">Edit `/etc/selinux/config` toodisable it for subsequent restarts.</span></span>

            setenforce 0

            then editing `/etc/selinux/config` tooset `SELINUX=permissive`
6. <span data-ttu-id="c79d4-170">MySQL çalıştırır doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c79d4-170">Validate MySQL runs.</span></span>

   <span data-ttu-id="c79d4-171">a.</span><span class="sxs-lookup"><span data-stu-id="c79d4-171">a.</span></span> <span data-ttu-id="c79d4-172">MySQL başlatın.</span><span class="sxs-lookup"><span data-stu-id="c79d4-172">Start MySQL.</span></span>

           service mysql start
   <span data-ttu-id="c79d4-173">b.</span><span class="sxs-lookup"><span data-stu-id="c79d4-173">b.</span></span> <span data-ttu-id="c79d4-174">Merhaba MySQL yükleme güvenli, hello kök parola ayarlama, anonim kullanıcılar toodisable uzak kök oturumu kaldırın ve hello test veritabanını kaldır.</span><span class="sxs-lookup"><span data-stu-id="c79d4-174">Secure hello MySQL installation, set hello root password, remove anonymous users toodisable remote root login, and remove hello test database.</span></span>

           mysql_secure_installation
   <span data-ttu-id="c79d4-175">c.</span><span class="sxs-lookup"><span data-stu-id="c79d4-175">c.</span></span> <span data-ttu-id="c79d4-176">Merhaba veritabanında küme işlemleri için ve isteğe bağlı olarak, uygulamalarınız için bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c79d4-176">Create a user on hello database for cluster operations, and optionally for your applications.</span></span>

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* too'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   <span data-ttu-id="c79d4-177">d.</span><span class="sxs-lookup"><span data-stu-id="c79d4-177">d.</span></span> <span data-ttu-id="c79d4-178">MySQL durdurun.</span><span class="sxs-lookup"><span data-stu-id="c79d4-178">Stop MySQL.</span></span>

            service mysql stop
7. <span data-ttu-id="c79d4-179">Bir yapılandırma yer tutucu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c79d4-179">Create a configuration placeholder.</span></span>

   <span data-ttu-id="c79d4-180">a.</span><span class="sxs-lookup"><span data-stu-id="c79d4-180">a.</span></span> <span data-ttu-id="c79d4-181">Merhaba MySQL yapılandırma toocreate hello küme ayarları için bir yer tutucu düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="c79d4-181">Edit hello MySQL configuration toocreate a placeholder for hello cluster settings.</span></span> <span data-ttu-id="c79d4-182">Merhaba değiştirmeyin  **`<Variables>`**  veya artık açıklamadan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="c79d4-182">Do not replace hello **`<Variables>`** or uncomment now.</span></span> <span data-ttu-id="c79d4-183">Bu şablonu kullanarak bir VM oluşturduktan sonra gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="c79d4-183">That will happen after you create a VM from this template.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="c79d4-184">b.</span><span class="sxs-lookup"><span data-stu-id="c79d4-184">b.</span></span> <span data-ttu-id="c79d4-185">Merhaba Düzenle  **[galera]**  bölümünde ve temizleyin.</span><span class="sxs-lookup"><span data-stu-id="c79d4-185">Edit hello **[galera]** section and clear it out.</span></span>

   <span data-ttu-id="c79d4-186">c.</span><span class="sxs-lookup"><span data-stu-id="c79d4-186">c.</span></span> <span data-ttu-id="c79d4-187">Merhaba Düzenle **[mariadb]** bölümü.</span><span class="sxs-lookup"><span data-stu-id="c79d4-187">Edit hello **[mariadb]** section.</span></span>

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
8. <span data-ttu-id="c79d4-188">Merhaba Güvenlik Duvarı'nda gerekli bağlantı noktaları üzerinde CentOS 7 FirewallD kullanarak açın.</span><span class="sxs-lookup"><span data-stu-id="c79d4-188">Open required ports on hello firewall by using FirewallD on CentOS 7.</span></span>

   * <span data-ttu-id="c79d4-189">MySQL:`firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="c79d4-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span></span>
   * <span data-ttu-id="c79d4-190">GALERA:`firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="c79d4-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span></span>
   * <span data-ttu-id="c79d4-191">GALERA IST:`firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="c79d4-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span></span>
   * <span data-ttu-id="c79d4-192">RSYNC:`firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="c79d4-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span></span>
   * <span data-ttu-id="c79d4-193">Merhaba Güvenlik Duvarı'nı yeniden yükleyin:`firewall-cmd --reload`</span><span class="sxs-lookup"><span data-stu-id="c79d4-193">Reload hello firewall: `firewall-cmd --reload`</span></span>

9. <span data-ttu-id="c79d4-194">Merhaba sistem performansı en iyi duruma getirme.</span><span class="sxs-lookup"><span data-stu-id="c79d4-194">Optimize hello system for performance.</span></span> <span data-ttu-id="c79d4-195">Daha fazla bilgi için bkz: [performans stratejisi ayarlama](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="c79d4-195">For more information, see [performance tuning strategy](optimize-mysql.md).</span></span>

   <span data-ttu-id="c79d4-196">a.</span><span class="sxs-lookup"><span data-stu-id="c79d4-196">a.</span></span> <span data-ttu-id="c79d4-197">Merhaba MySQL yapılandırma dosyasını yeniden düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="c79d4-197">Edit hello MySQL configuration file again.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="c79d4-198">b.</span><span class="sxs-lookup"><span data-stu-id="c79d4-198">b.</span></span> <span data-ttu-id="c79d4-199">Merhaba Düzenle **[mariadb]** bölümünde ve içeriği aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c79d4-199">Edit hello **[mariadb]** section and append hello following content:</span></span>

   > [!NOTE]
   > <span data-ttu-id="c79d4-200">Bu innodb öneririz\_arabellek\_pool_size olan VM bellek yüzde 70 '.</span><span class="sxs-lookup"><span data-stu-id="c79d4-200">We recommend that innodb\_buffer\_pool_size is 70 percent of your VM's memory.</span></span> <span data-ttu-id="c79d4-201">Merhaba Orta 3.5 GB RAM'i olan Azure VM için bu örnekte, 2,45 GB olarak ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="c79d4-201">In this example, it has been set at 2.45 GB for hello medium Azure VM with 3.5 GB of RAM.</span></span>
   >
   >

           innodb_buffer_pool_size = 2508M # hello buffer pool contains buffered data and hello index. This is usually set too70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give hello server more time toorecycle idled connections
           innodb_file_per_table = 1 # Speed up hello table space transmission and optimize hello debris management performance
           innodb_log_buffer_size = 128M # hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit
           innodb_flush_log_at_trx_commit = 2 # hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. <span data-ttu-id="c79d4-202">MySQL durdurun, hello küme bir düğüm eklerken kesintiye başlangıç tooavoid üzerinde çalışmasını MySQL hizmetini devre dışı bırakın ve hello makine sağlamayı sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="c79d4-202">Stop MySQL, disable MySQL service from running on startup tooavoid disrupting hello cluster when adding a node, and deprovision hello machine.</span></span>

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. <span data-ttu-id="c79d4-203">Merhaba VM hello portal üzerinden yakalayın.</span><span class="sxs-lookup"><span data-stu-id="c79d4-203">Capture hello VM through hello portal.</span></span> <span data-ttu-id="c79d4-204">(Şu anda [#1268 hello Azure CLI araçlarında sorun](https://github.com/Azure/azure-xplat-cli/issues/1268) hello Azure CLI araçlarını tarafından yakalanan görüntüleri bağlı hello veri diskleri yakalamayın hello olgu açıklanmaktadır.)</span><span class="sxs-lookup"><span data-stu-id="c79d4-204">(Currently, [issue #1268 in hello Azure CLI tools](https://github.com/Azure/azure-xplat-cli/issues/1268) describes hello fact that images captured by hello Azure CLI tools do not capture hello attached data disks.)</span></span>

    <span data-ttu-id="c79d4-205">a.</span><span class="sxs-lookup"><span data-stu-id="c79d4-205">a.</span></span> <span data-ttu-id="c79d4-206">Merhaba portal üzerinden hello makineyi kapatın.</span><span class="sxs-lookup"><span data-stu-id="c79d4-206">Shut down hello machine through hello portal.</span></span>

    <span data-ttu-id="c79d4-207">b.</span><span class="sxs-lookup"><span data-stu-id="c79d4-207">b.</span></span> <span data-ttu-id="c79d4-208">Tıklatın **yakalama** ve hello görüntü adı olarak belirtmeniz **mariadb galera görüntü**.</span><span class="sxs-lookup"><span data-stu-id="c79d4-208">Click **Capture** and specify hello image name as **mariadb-galera-image**.</span></span> <span data-ttu-id="c79d4-209">Bir açıklama girin ve denetimi "Waagent Çalıştır."</span><span class="sxs-lookup"><span data-stu-id="c79d4-209">Provide a description and check "I have run waagent."</span></span>
      
      ![Merhaba sanal makinesi yakalama](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-hello-cluster"></a><span data-ttu-id="c79d4-211">Merhaba kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c79d4-211">Create hello cluster</span></span>
<span data-ttu-id="c79d4-212">Üç VM'ler ile oluşturulan ve yapılandırmak ve hello küme Başlat hello şablonu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c79d4-212">Create three VMs with hello template you created, and then configure and start hello cluster.</span></span>

1. <span data-ttu-id="c79d4-213">Merhaba mariadb galera görüntü ilk CentOS 7 VM'den görüntü oluşturduğunuz, aşağıdaki bilgilerle hello sağlama hello oluşturun:</span><span class="sxs-lookup"><span data-stu-id="c79d4-213">Create hello first CentOS 7 VM from hello mariadb-galera-image image you created, providing hello following information:</span></span>

 - <span data-ttu-id="c79d4-214">Sanal ağ adı: mariadbvnet</span><span class="sxs-lookup"><span data-stu-id="c79d4-214">Virtual network name: mariadbvnet</span></span>
 - <span data-ttu-id="c79d4-215">Alt ağ: mariadb</span><span class="sxs-lookup"><span data-stu-id="c79d4-215">Subnet: mariadb</span></span>
 - <span data-ttu-id="c79d4-216">Makine boyutu: Orta</span><span class="sxs-lookup"><span data-stu-id="c79d4-216">Machine size: medium</span></span>
 - <span data-ttu-id="c79d4-217">Bulut hizmet adı: mariadbha (veya mariadbha.cloudapp.net erişilen toobe istediğiniz ne olursa olsun adı)</span><span class="sxs-lookup"><span data-stu-id="c79d4-217">Cloud service name: mariadbha (or whatever name you want toobe accessed through mariadbha.cloudapp.net)</span></span>
 - <span data-ttu-id="c79d4-218">Makine adı: mariadb1</span><span class="sxs-lookup"><span data-stu-id="c79d4-218">Machine name: mariadb1</span></span>
 - <span data-ttu-id="c79d4-219">Kullanıcı adı: azureuser</span><span class="sxs-lookup"><span data-stu-id="c79d4-219">Username: azureuser</span></span>
 - <span data-ttu-id="c79d4-220">SSH erişimini: etkin</span><span class="sxs-lookup"><span data-stu-id="c79d4-220">SSH access: enabled</span></span>
 - <span data-ttu-id="c79d4-221">Merhaba SSH sertifika .pem dosyasını geçirerek ve /path/to/key.pem hello saklandığı hello yolu ile değiştirerek .pem SSH anahtarı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c79d4-221">Passing hello SSH certificate .pem file and replacing /path/to/key.pem with hello path where you stored hello generated .pem SSH key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c79d4-222">Merhaba aşağıdaki komutları daha anlaşılır olması için birden çok satır üzerinden bölünür, ancak her bir satır olarak girmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c79d4-222">hello following commands are split over multiple lines for clarity, but you should enter each as one line.</span></span>
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
2. <span data-ttu-id="c79d4-223">Toohello mariadbha bulut hizmetine bağlanarak iki daha fazla sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c79d4-223">Create two more virtual machines by connecting them toohello mariadbha cloud service.</span></span> <span data-ttu-id="c79d4-224">Değişiklik hello VM adı ve SSH bağlantı noktası tooa benzersiz bağlantı noktası ile diğer VM'lerin değil çakışan hello aynı bulut hizmetine hello.</span><span class="sxs-lookup"><span data-stu-id="c79d4-224">Change hello VM name and hello SSH port tooa unique port not conflicting with other VMs in hello same cloud service.</span></span>

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
  <span data-ttu-id="c79d4-225">MariaDB3 için:</span><span class="sxs-lookup"><span data-stu-id="c79d4-225">For MariaDB3:</span></span>

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
3. <span data-ttu-id="c79d4-226">Merhaba sonraki adımda tooget hello iç IP adresi her bir hello üç VM'ler gerekir:</span><span class="sxs-lookup"><span data-stu-id="c79d4-226">You will need tooget hello internal IP address of each of hello three VMs for hello next step:</span></span>

    ![IP adresi alınıyor](./media/mariadb-mysql-cluster/IP.png)
4. <span data-ttu-id="c79d4-228">SSH toosign toohello üç Vm'lerde kullanın ve bunların her birini hello yapılandırma dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="c79d4-228">Use SSH toosign in toohello three VMs and edit hello configuration file on each of them.</span></span>

        sudo vi /etc/my.cnf.d/server.cnf

    <span data-ttu-id="c79d4-229">Açıklamadan çıkarın  **`wsrep_cluster_name`**  ve  **`wsrep_cluster_address`**  hello kaldırarak  **#**  hello başında başlangıç satırı.</span><span class="sxs-lookup"><span data-stu-id="c79d4-229">Uncomment **`wsrep_cluster_name`** and **`wsrep_cluster_address`** by removing hello **#** at hello beginning of hello line.</span></span>
    <span data-ttu-id="c79d4-230">Ayrıca, yerine  **`<ServerIP>`**  içinde  **`wsrep_node_address`**  ve  **`<NodeName>`**  içinde  **`wsrep_node_name`**  hello ile Sanal makinenin IP adresi ve adı, sırasıyla ve de bu satırlardaki yorumları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="c79d4-230">Additionally, replace **`<ServerIP>`** in **`wsrep_node_address`** and **`<NodeName>`** in **`wsrep_node_name`** with hello VM's IP address and name, respectively, and uncomment those lines as well.</span></span>
5. <span data-ttu-id="c79d4-231">Hello küme üzerinde MariaDB1 başlatmak ve başlangıçta çalışmasına izin verin.</span><span class="sxs-lookup"><span data-stu-id="c79d4-231">Start hello cluster on MariaDB1 and let it run at startup.</span></span>

        sudo service mysql bootstrap
        chkconfig mysql on
6. <span data-ttu-id="c79d4-232">MySQL MariaDB2 ve MariaDB3 başlatmak ve başlangıçta çalışmasına izin verin.</span><span class="sxs-lookup"><span data-stu-id="c79d4-232">Start MySQL on MariaDB2 and MariaDB3 and let it run at startup.</span></span>

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-hello-cluster"></a><span data-ttu-id="c79d4-233">Yük Dengeleme hello küme</span><span class="sxs-lookup"><span data-stu-id="c79d4-233">Load balance hello cluster</span></span>
<span data-ttu-id="c79d4-234">Kümelenmiş hello VM'ler oluşturduğunuzda, clusteravset tooensure farklı hata ve güncelleştirme etki alanlarında konmuş ve Azure hiçbir zaman bakım tüm makinelerde aynı anda yaptığı adlı bir kullanılabilirlik kümesine eklenir.</span><span class="sxs-lookup"><span data-stu-id="c79d4-234">When you created hello clustered VMs, you added them into an availability set called clusteravset tooensure that they were put on different fault and update domains and that Azure never does maintenance on all machines at once.</span></span> <span data-ttu-id="c79d4-235">Bu yapılandırma toobe hello Azure hizmet düzeyi sözleşmesi (SLA) tarafından desteklenen hello gereksinimleri karşılıyor.</span><span class="sxs-lookup"><span data-stu-id="c79d4-235">This configuration meets hello requirements toobe supported by hello Azure service level agreement (SLA).</span></span>

<span data-ttu-id="c79d4-236">Artık Azure yük dengeleyici toobalance istekleri hello üç düğümler arasında kullanır.</span><span class="sxs-lookup"><span data-stu-id="c79d4-236">Now use Azure Load Balancer toobalance requests between hello three nodes.</span></span>

<span data-ttu-id="c79d4-237">Hello Azure CLI kullanarak komutları makinenizde aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c79d4-237">Run hello following commands on your machine by using hello Azure CLI.</span></span>

<span data-ttu-id="c79d4-238">Merhaba komut parametreleri yapıdır:`azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span><span class="sxs-lookup"><span data-stu-id="c79d4-238">hello command parameters structure is: `azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span></span>

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

<span data-ttu-id="c79d4-239">Merhaba CLI biraz uzun olabilecek hello yük dengeleyici yoklama aralığı too15 saniye cinsinden ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c79d4-239">hello CLI sets hello load balancer probe interval too15 seconds, which might be a bit too long.</span></span> <span data-ttu-id="c79d4-240">Merhaba portalında altında değiştirme **uç noktaları** herhangi bir hello VM'ler için.</span><span class="sxs-lookup"><span data-stu-id="c79d4-240">Change it in hello portal under **Endpoints** for any of hello VMs.</span></span>

![Uç noktayı Düzenle](./media/mariadb-mysql-cluster/Endpoint.PNG)

<span data-ttu-id="c79d4-242">Seçin **RECONFIGURE hello yük dengelemeli mimarilerde ayarlamak**.</span><span class="sxs-lookup"><span data-stu-id="c79d4-242">Select **Reconfigure hello Load-Balanced Set**.</span></span>

![Yeniden hello yük dengeli kümesi](./media/mariadb-mysql-cluster/Endpoint2.PNG)

<span data-ttu-id="c79d4-244">Değişiklik **yoklama aralığı** too5 saniye ve değişikliklerinizi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c79d4-244">Change **Probe Interval** too5 seconds and save your changes.</span></span>

![Değiştirme yoklama aralığı](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-hello-cluster"></a><span data-ttu-id="c79d4-246">Merhaba küme doğrulama</span><span class="sxs-lookup"><span data-stu-id="c79d4-246">Validate hello cluster</span></span>
<span data-ttu-id="c79d4-247">Merhaba sabit çalışma yapılır.</span><span class="sxs-lookup"><span data-stu-id="c79d4-247">hello hard work is done.</span></span> <span data-ttu-id="c79d4-248">Merhaba küme olmalıdır şimdi en erişilebilir `mariadbha.cloudapp.net:3306`hello yük dengeleyici isabetler ve rota istekleri arasında sorunsuz ve verimli bir şekilde üç VM'ler hello.</span><span class="sxs-lookup"><span data-stu-id="c79d4-248">hello cluster should be now accessible at `mariadbha.cloudapp.net:3306`, which hits hello load balancer and route requests between hello three VMs smoothly and efficiently.</span></span>

<span data-ttu-id="c79d4-249">Sık kullanılan MySQL istemci tooconnect kullanın veya bu küme çalışma hello VM'ler tooverify birinden bağlanın.</span><span class="sxs-lookup"><span data-stu-id="c79d4-249">Use your favorite MySQL client tooconnect, or connect from one of hello VMs tooverify that this cluster is working.</span></span>

     mysql -u cluster -h mariadbha.cloudapp.net -p

<span data-ttu-id="c79d4-250">Ardından bir veritabanı oluşturun ve bazı verilerle doldurmak.</span><span class="sxs-lookup"><span data-stu-id="c79d4-250">Then create a database and populate it with some data.</span></span>

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

<span data-ttu-id="c79d4-251">oluşturduğunuz hello veritabanı aşağıdaki tablonun hello döndürür:</span><span class="sxs-lookup"><span data-stu-id="c79d4-251">hello database you created returns hello following table:</span></span>

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="c79d4-252">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c79d4-252">Next steps</span></span>
<span data-ttu-id="c79d4-253">Bu makalede, bir üç düğümü MariaDB oluşturulan + Galera yüksek oranda kullanılabilir küme sanal Azure üzerinde çalışan CentOS 7 makineleri.</span><span class="sxs-lookup"><span data-stu-id="c79d4-253">In this article, you created a three-node MariaDB + Galera highly available cluster on Azure virtual machines running CentOS 7.</span></span> <span data-ttu-id="c79d4-254">Merhaba VM'ler Azure yük dengeleyici ile dengeleneceğini.</span><span class="sxs-lookup"><span data-stu-id="c79d4-254">hello VMs are load balanced with Azure Load Balancer.</span></span>

<span data-ttu-id="c79d4-255">Konumundaki toolook isteyebilirsiniz [başka bir şekilde toocluster Linux'ta MySQL](mysql-cluster.md) ve yolları çok[iyileştirmek ve Azure Linux VM'ler MySQL performansı test](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="c79d4-255">You might want toolook at [another way toocluster MySQL on Linux](mysql-cluster.md) and ways too[optimize and test MySQL performance on Azure Linux VMs](optimize-mysql.md).</span></span>

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
