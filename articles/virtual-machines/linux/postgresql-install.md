---
title: "Bir Linux VM üzerinde PostgreSQL ayarlama | Microsoft Docs"
description: "Yükleme ve PostgreSQL azure'da bir Linux sanal makine yapılandırma hakkında bilgi edinin"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 1a747363-0cc5-4ba3-9be7-084dfeb04651
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: 0bccdc1cfdbda06b57da8cd662373ef137768672
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-configure-postgresql-on-azure"></a><span data-ttu-id="fef98-103">Azure’da PostgreSQL yükleme ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fef98-103">Install and configure PostgreSQL on Azure</span></span>
<span data-ttu-id="fef98-104">PostgreSQL Oracle ve DB2 için benzer bir Gelişmiş açık kaynak veritabanı yok.</span><span class="sxs-lookup"><span data-stu-id="fef98-104">PostgreSQL is an advanced open-source database similar to Oracle and DB2.</span></span> <span data-ttu-id="fef98-105">Tam ACID uyumluluk, güvenilir işlem işleme ve çoklu sürüm eşzamanlılık denetimi gibi Kurumsal kullanıma hazır özellikler içerir.</span><span class="sxs-lookup"><span data-stu-id="fef98-105">It includes enterprise-ready features such as full ACID compliance, reliable transactional processing, and multi-version concurrency control.</span></span> <span data-ttu-id="fef98-106">Ayrıca, ANSI SQL ve SQL/MED (Oracle, MySQL, MongoDB ve diğer birçok için yabancı veri sarmalayıcıları dahil) gibi standartlara destekler.</span><span class="sxs-lookup"><span data-stu-id="fef98-106">It also supports standards such as ANSI SQL and SQL/MED (including foreign data wrappers for Oracle, MySQL, MongoDB, and many others).</span></span> <span data-ttu-id="fef98-107">Desteğiyle üzerinde 12 yordam diller, GIN ve GiST dizinleri, uzamsal veri desteği ve birden çok NoSQL benzeri özellikleri JSON veya anahtar-değer tabanlı uygulamalar için yüksek oranda genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="fef98-107">It is highly extensible with support for over 12 procedural languages, GIN and GiST indexes, spatial data support, and multiple NoSQL-like features for JSON or key-value-based applications.</span></span>

<span data-ttu-id="fef98-108">Bu makalede, yüklemek ve bir Azure Linux çalıştıran sanal makine üzerinde PostgreSQL yapılandırmak öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="fef98-108">In this article, you will learn how to install and configure PostgreSQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a><span data-ttu-id="fef98-109">PostgreSQL yükleyin</span><span class="sxs-lookup"><span data-stu-id="fef98-109">Install PostgreSQL</span></span>
> [!NOTE]
> <span data-ttu-id="fef98-110">Bu öğreticiyi tamamlamak için Linux çalıştıran bir Azure sanal makinesi zaten olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fef98-110">You must already have an Azure virtual machine running Linux in order to complete this tutorial.</span></span> <span data-ttu-id="fef98-111">Oluşturma ve devam etmeden önce bir Linux VM ayarlamak için bkz: [Azure Linux VM'de Öğreticisi](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fef98-111">To create and set up a Linux VM before proceeding, see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

<span data-ttu-id="fef98-112">Bu durumda, bağlantı noktası 1999 PostgreSQL bağlantı noktası olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="fef98-112">In this case, use port 1999 as the PostgreSQL port.</span></span>  

<span data-ttu-id="fef98-113">PuTTY üzerinden oluşturulan VM Linux bağlayın.</span><span class="sxs-lookup"><span data-stu-id="fef98-113">Connect to the Linux VM you created via PuTTY.</span></span> <span data-ttu-id="fef98-114">Bir Azure Linux VM kullanmakta olduğunuz ilk kez kullanıyorsanız bkz [nasıl kullanmak ile SSH Linux Azure üzerinde](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) bir Linux VM bağlanmak için PuTTY kullanın öğrenmek için.</span><span class="sxs-lookup"><span data-stu-id="fef98-114">If this is the first time you're using an Azure Linux VM, see [How to Use SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to learn how to use PuTTY to connect to a Linux VM.</span></span>

1. <span data-ttu-id="fef98-115">(Yönetici) köküne geçmek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fef98-115">Run the following command to switch to the root (admin):</span></span>
   
        # sudo su -
2. <span data-ttu-id="fef98-116">Bazı dağıtımları PostgreSQL yüklemeden önce yüklemelisiniz bağımlılıkları vardır.</span><span class="sxs-lookup"><span data-stu-id="fef98-116">Some distributions have dependencies that you must install before installing PostgreSQL.</span></span> <span data-ttu-id="fef98-117">Bu listede, distro denetlemek ve uygun komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fef98-117">Check for your distro in this list and run the appropriate command:</span></span>
   
   * <span data-ttu-id="fef98-118">Red Hat temel Linux:</span><span class="sxs-lookup"><span data-stu-id="fef98-118">Red Hat base Linux:</span></span>
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="fef98-119">Debian temel Linux:</span><span class="sxs-lookup"><span data-stu-id="fef98-119">Debian base Linux:</span></span>
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="fef98-120">SUSE Linux:</span><span class="sxs-lookup"><span data-stu-id="fef98-120">SUSE Linux:</span></span>
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. <span data-ttu-id="fef98-121">Kök dizinine PostgreSQL yükleyin ve paketin sıkıştırmasını açın:</span><span class="sxs-lookup"><span data-stu-id="fef98-121">Download PostgreSQL into the root directory, and then unzip the package:</span></span>
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    <span data-ttu-id="fef98-122">Yukarıdaki örnek verilebilir.</span><span class="sxs-lookup"><span data-stu-id="fef98-122">The above is an example.</span></span> <span data-ttu-id="fef98-123">Daha ayrıntılı indirme adresi bulabilirsiniz [dizin/pub programlarının/kaynak /](https://ftp.postgresql.org/pub/source/).</span><span class="sxs-lookup"><span data-stu-id="fef98-123">You can find the more detailed download address in the [Index of /pub/source/](https://ftp.postgresql.org/pub/source/).</span></span>
4. <span data-ttu-id="fef98-124">Yapı başlatmak için şu komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fef98-124">To start the build, run these commands:</span></span>
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. <span data-ttu-id="fef98-125">Her şeyi içeren belgeleri (HTML ve ADAM sayfaları) ve ek modülleri (contrib) dahil olmak üzere oluşturulabilir oluşturmak istiyorsanız bunun yerine aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fef98-125">If  you want to build everything that can be built, including the documentation (HTML and man pages) and additional modules (contrib), run the following command instead:</span></span>
   
        # gmake install-world
   
    <span data-ttu-id="fef98-126">Aşağıdaki onay iletisini almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="fef98-126">You should receive the following confirmation message:</span></span>
   
        PostgreSQL, contrib, and documentation successfully made. Ready to install.

## <a name="configure-postgresql"></a><span data-ttu-id="fef98-127">PostgreSQL yapılandırın</span><span class="sxs-lookup"><span data-stu-id="fef98-127">Configure PostgreSQL</span></span>
1. <span data-ttu-id="fef98-128">(İsteğe bağlı) Sürüm numarasını içermeyecek şekilde PostgreSQL başvuru kısaltmak için sembolik bağlantı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="fef98-128">(Optional) Create a symbolic link to shorten the PostgreSQL reference to not include the version number:</span></span>
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. <span data-ttu-id="fef98-129">Veritabanı için bir dizin oluşturun:</span><span class="sxs-lookup"><span data-stu-id="fef98-129">Create a directory for the database:</span></span>
   
        # mkdir -p /opt/pgsql_data
3. <span data-ttu-id="fef98-130">Kök olmayan kullanıcı oluşturun ve o kullanıcının profilini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fef98-130">Create a non-root user and modify that user’s profile.</span></span> <span data-ttu-id="fef98-131">Ardından, bu yeni bir kullanıcıya geçiş (adlı *postgres* örneğimizde):</span><span class="sxs-lookup"><span data-stu-id="fef98-131">Then, switch to this new user (called *postgres* in our example):</span></span>
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > <span data-ttu-id="fef98-132">Güvenlik nedenleriyle, PostgreSQL kök olmayan kullanıcı başlatmak, başlatma veya veritabanı kapatmak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="fef98-132">For security reasons, PostgreSQL uses a non-root user to initialize, start, or shut down the database.</span></span>
   > 
   > 
4. <span data-ttu-id="fef98-133">Düzen *bash_profile* aşağıdaki komutları girerek dosya.</span><span class="sxs-lookup"><span data-stu-id="fef98-133">Edit the *bash_profile* file by entering the commands below.</span></span> <span data-ttu-id="fef98-134">Bu satırlar sonuna eklenecek *bash_profile* dosyası:</span><span class="sxs-lookup"><span data-stu-id="fef98-134">These lines will be added to the end of the *bash_profile* file:</span></span>
   
        cat >> ~/.bash_profile <<EOF
        export PGPORT=1999
        export PGDATA=/opt/pgsql_data
        export LANG=en_US.utf8
        export PGHOME=/opt/pgsql
        export PATH=\$PATH:\$PGHOME/bin
        export MANPATH=\$MANPATH:\$PGHOME/share/man
        export DATA=`date +"%Y%m%d%H%M"`
        export PGUSER=postgres
        alias rm='rm -i'
        alias ll='ls -lh'
        EOF
5. <span data-ttu-id="fef98-135">Yürütme *bash_profile* dosyası:</span><span class="sxs-lookup"><span data-stu-id="fef98-135">Execute the *bash_profile* file:</span></span>
   
        $ source .bash_profile
6. <span data-ttu-id="fef98-136">Aşağıdaki komutu kullanarak yüklemenizi doğrulama:</span><span class="sxs-lookup"><span data-stu-id="fef98-136">Validate your installation by using the following command:</span></span>
   
        $ which psql
   
    <span data-ttu-id="fef98-137">Yükleme başarılı olursa, aşağıdaki yanıt görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="fef98-137">If your installation is successful, you will see the following response:</span></span>
   
        /opt/pgsql/bin/psql
7. <span data-ttu-id="fef98-138">Ayrıca, PostgreSQL sürüm kontrol edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fef98-138">You can also check the PostgreSQL version:</span></span>
   
        $ psql -V
8. <span data-ttu-id="fef98-139">Veritabanını başlatılamadı:</span><span class="sxs-lookup"><span data-stu-id="fef98-139">Initialize the database:</span></span>
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    <span data-ttu-id="fef98-140">Aşağıdaki çıkış almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="fef98-140">You should receive the following output:</span></span>

![Görüntü](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a><span data-ttu-id="fef98-142">PostgreSQL ayarlayın</span><span class="sxs-lookup"><span data-stu-id="fef98-142">Set up PostgreSQL</span></span>
<!--    [postgres@ test ~]$ exit -->

<span data-ttu-id="fef98-143">Aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fef98-143">Run the following commands:</span></span>

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

<span data-ttu-id="fef98-144">/Etc/init.d/postgresql dosyasındaki iki değişkenleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fef98-144">Modify two variables in the /etc/init.d/postgresql file.</span></span> <span data-ttu-id="fef98-145">Öneki PostgreSQL yükleme konumunu ayarlayın: **/opt/pgsql**.</span><span class="sxs-lookup"><span data-stu-id="fef98-145">The prefix is set to the installation path of PostgreSQL: **/opt/pgsql**.</span></span> <span data-ttu-id="fef98-146">PGDATA PostgreSQL veri depolama yoluna ayarlayın: **/opt/pgsql_data**.</span><span class="sxs-lookup"><span data-stu-id="fef98-146">PGDATA is set to the data storage path of PostgreSQL: **/opt/pgsql_data**.</span></span>

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![Görüntü](./media/postgresql-install/no2.png)

<span data-ttu-id="fef98-148">Yürütülebilir yapabilmek için dosyayı değiştirin:</span><span class="sxs-lookup"><span data-stu-id="fef98-148">Change the file to make it executable:</span></span>

    # chmod +x /etc/init.d/postgresql

<span data-ttu-id="fef98-149">PostgreSQL başlatın:</span><span class="sxs-lookup"><span data-stu-id="fef98-149">Start PostgreSQL:</span></span>

    # /etc/init.d/postgresql start

<span data-ttu-id="fef98-150">PostgreSQL uç noktası üzerinde olup olmadığını kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="fef98-150">Check if the endpoint of PostgreSQL is on:</span></span>

    # netstat -tunlp|grep 1999

<span data-ttu-id="fef98-151">Şu çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="fef98-151">You should see the following output:</span></span>

![Görüntü](./media/postgresql-install/no3.png)

## <a name="connect-to-the-postgres-database"></a><span data-ttu-id="fef98-153">Postgres veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="fef98-153">Connect to the Postgres database</span></span>
<span data-ttu-id="fef98-154">Postgres kullanıcıya bir kez daha anahtarı:</span><span class="sxs-lookup"><span data-stu-id="fef98-154">Switch to the postgres user once again:</span></span>

    # su - postgres

<span data-ttu-id="fef98-155">Postgres veritabanı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="fef98-155">Create a Postgres database:</span></span>

    $ createdb events

<span data-ttu-id="fef98-156">Olayları veritabanına bağlan:</span><span class="sxs-lookup"><span data-stu-id="fef98-156">Connect to the events database that you just created:</span></span>

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a><span data-ttu-id="fef98-157">Oluşturun ve Postgres tablo silme</span><span class="sxs-lookup"><span data-stu-id="fef98-157">Create and delete a Postgres table</span></span>
<span data-ttu-id="fef98-158">Veritabanına bağlı, tablo içinde oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fef98-158">Now that you have connected to the database, you can create tables in it.</span></span>

<span data-ttu-id="fef98-159">Örneğin, aşağıdaki komutu kullanarak yeni bir örnek Postgres tablo oluşturun:</span><span class="sxs-lookup"><span data-stu-id="fef98-159">For example, create a new example Postgres table by using the following command:</span></span>

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

<span data-ttu-id="fef98-160">Aşağıdaki sütun adları ve kısıtlamaları ile dört sütunlu bir tablo şimdi ayarlamış olduğunuz:</span><span class="sxs-lookup"><span data-stu-id="fef98-160">You have now set up a four-column table with the following column names and restrictions:</span></span>

1. <span data-ttu-id="fef98-161">"Name" sütun altında 20 karakter uzunluğunda olacak şekilde VARCHAR komutu tarafından sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="fef98-161">The “name” column has been limited by the VARCHAR command to be under 20 characters long.</span></span>
2. <span data-ttu-id="fef98-162">"Yemek" sütun herkes getirecek yemek öğesi belirtir.</span><span class="sxs-lookup"><span data-stu-id="fef98-162">The “food” column indicates the food item that each person will bring.</span></span> <span data-ttu-id="fef98-163">VARCHAR altında 30 karakter olması için bu metni sınırlar.</span><span class="sxs-lookup"><span data-stu-id="fef98-163">VARCHAR limits this text to be under 30 characters.</span></span>
3. <span data-ttu-id="fef98-164">"Onaylanan" sütun, kişinin için Yemeğini Getir Partisi RSVP'd olup olmadığını kaydeder.</span><span class="sxs-lookup"><span data-stu-id="fef98-164">The “confirmed” column records whether the person has RSVP’d to the potluck.</span></span> <span data-ttu-id="fef98-165">Kabul edilebilir değerler "Y" ve "N" dir.</span><span class="sxs-lookup"><span data-stu-id="fef98-165">The acceptable values are "Y" and "N".</span></span>
4. <span data-ttu-id="fef98-166">Bunlar olayı için kaydolurken "tarih" sütun gösterir.</span><span class="sxs-lookup"><span data-stu-id="fef98-166">The “date” column shows when they signed up for the event.</span></span> <span data-ttu-id="fef98-167">Tarih yyyy-aa-gg yazılması Postgres gerektirir</span><span class="sxs-lookup"><span data-stu-id="fef98-167">Postgres requires that dates be written as yyyy-mm-dd.</span></span>

<span data-ttu-id="fef98-168">Tablonuz başarıyla oluşturulduysa aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="fef98-168">You should see the following if your table has been successfully created:</span></span>

![Görüntü](./media/postgresql-install/no4.png)

<span data-ttu-id="fef98-170">Aşağıdaki komutu kullanarak, tablo yapısı de denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fef98-170">You can also check the table structure by using the following command:</span></span>

![Görüntü](./media/postgresql-install/no5.png)

### <a name="add-data-to-a-table"></a><span data-ttu-id="fef98-172">Bir tabloya veri ekleme</span><span class="sxs-lookup"><span data-stu-id="fef98-172">Add data to a table</span></span>
<span data-ttu-id="fef98-173">İlk olarak, bilgileri bir satıra Ekle:</span><span class="sxs-lookup"><span data-stu-id="fef98-173">First, insert information into a row:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

<span data-ttu-id="fef98-174">Bu çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="fef98-174">You should see this output:</span></span>

![Görüntü](./media/postgresql-install/no6.png)

<span data-ttu-id="fef98-176">Birkaç daha fazla kişinin tabloya ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fef98-176">You can add a couple more people to the table as well.</span></span> <span data-ttu-id="fef98-177">İşte birkaç seçenek veya kendi oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fef98-177">Here are some options, or you can create your own:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a><span data-ttu-id="fef98-178">Tabloları Göster</span><span class="sxs-lookup"><span data-stu-id="fef98-178">Show tables</span></span>
<span data-ttu-id="fef98-179">Bir tablo göstermek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="fef98-179">Use the following command to show a table:</span></span>

    select * from potluck;

<span data-ttu-id="fef98-180">Çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="fef98-180">The output is:</span></span>

![Görüntü](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a><span data-ttu-id="fef98-182">Bir tablodaki verileri silme</span><span class="sxs-lookup"><span data-stu-id="fef98-182">Delete data in a table</span></span>
<span data-ttu-id="fef98-183">Bir tablodaki verileri silmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="fef98-183">Use the following command to delete data in a table:</span></span>

    delete from potluck where name=’John’;

<span data-ttu-id="fef98-184">"John" satırdaki tüm bilgileri siler.</span><span class="sxs-lookup"><span data-stu-id="fef98-184">This deletes all the information in the "John" row.</span></span> <span data-ttu-id="fef98-185">Çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="fef98-185">The output is:</span></span>

![Görüntü](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a><span data-ttu-id="fef98-187">Bir tablodaki verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="fef98-187">Update data in a table</span></span>
<span data-ttu-id="fef98-188">Bir tablodaki verileri güncelleştirmek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="fef98-188">Use the following command to update data in a table.</span></span> <span data-ttu-id="fef98-189">Biz "Y" için "N" den kendi RSVP değiştirecek şekilde aynen katılan olmadığını, bu biri için Sandy onayladığından:</span><span class="sxs-lookup"><span data-stu-id="fef98-189">For this one, Sandy has confirmed that she is attending, so we will change her RSVP from "N" to "Y":</span></span>

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a><span data-ttu-id="fef98-190">PostgreSQL hakkında daha fazla bilgi alın</span><span class="sxs-lookup"><span data-stu-id="fef98-190">Get more information about PostgreSQL</span></span>
<span data-ttu-id="fef98-191">Bir Azure Linux VM'de PostgreSQL yüklemesini tamamladığınıza göre Azure'da kullanarak keyfini çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fef98-191">Now that you have completed the installation of PostgreSQL in an Azure Linux VM, you can enjoy using it in Azure.</span></span> <span data-ttu-id="fef98-192">PostgreSQL hakkında daha fazla bilgi için [PostgreSQL Web sitesi](http://www.postgresql.org/).</span><span class="sxs-lookup"><span data-stu-id="fef98-192">To learn more about PostgreSQL, visit the [PostgreSQL website](http://www.postgresql.org/).</span></span>

