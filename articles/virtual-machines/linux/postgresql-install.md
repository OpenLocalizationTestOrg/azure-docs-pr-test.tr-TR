---
title: "bir Linux VM üzerinde PostgreSQL yukarı aaaSet | Microsoft Docs"
description: "Bilgi nasıl tooinstall ve azure'da bir Linux sanal makinede PostgreSQL yapılandırın"
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
ms.openlocfilehash: 40209647924dffce11500705eb2d9f41c14df6ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-postgresql-on-azure"></a><span data-ttu-id="fe4cb-103">Azure’da PostgreSQL yükleme ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fe4cb-103">Install and configure PostgreSQL on Azure</span></span>
<span data-ttu-id="fe4cb-104">PostgreSQL bir Gelişmiş açık kaynak veritabanı benzer tooOracle ve DB2 ' dir.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-104">PostgreSQL is an advanced open-source database similar tooOracle and DB2.</span></span> <span data-ttu-id="fe4cb-105">Tam ACID uyumluluk, güvenilir işlem işleme ve çoklu sürüm eşzamanlılık denetimi gibi Kurumsal kullanıma hazır özellikler içerir.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-105">It includes enterprise-ready features such as full ACID compliance, reliable transactional processing, and multi-version concurrency control.</span></span> <span data-ttu-id="fe4cb-106">Ayrıca, ANSI SQL ve SQL/MED (Oracle, MySQL, MongoDB ve diğer birçok için yabancı veri sarmalayıcıları dahil) gibi standartlara destekler.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-106">It also supports standards such as ANSI SQL and SQL/MED (including foreign data wrappers for Oracle, MySQL, MongoDB, and many others).</span></span> <span data-ttu-id="fe4cb-107">Desteğiyle üzerinde 12 yordam diller, GIN ve GiST dizinleri, uzamsal veri desteği ve birden çok NoSQL benzeri özellikleri JSON veya anahtar-değer tabanlı uygulamalar için yüksek oranda genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-107">It is highly extensible with support for over 12 procedural languages, GIN and GiST indexes, spatial data support, and multiple NoSQL-like features for JSON or key-value-based applications.</span></span>

<span data-ttu-id="fe4cb-108">Bu makalede, öğreneceksiniz nasıl tooinstall ve bir Azure Linux çalıştıran sanal makine üzerinde PostgreSQL yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-108">In this article, you will learn how tooinstall and configure PostgreSQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a><span data-ttu-id="fe4cb-109">PostgreSQL yükleyin</span><span class="sxs-lookup"><span data-stu-id="fe4cb-109">Install PostgreSQL</span></span>
> [!NOTE]
> <span data-ttu-id="fe4cb-110">Bu öğretici sipariş toocomplete Linux çalıştıran bir Azure sanal makinesi zaten olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-110">You must already have an Azure virtual machine running Linux in order toocomplete this tutorial.</span></span> <span data-ttu-id="fe4cb-111">bkz: toocreate ve devam etmeden önce bir Linux VM ayarlama [Azure Linux VM'de Öğreticisi](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe4cb-111">toocreate and set up a Linux VM before proceeding, see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

<span data-ttu-id="fe4cb-112">Bu durumda, bağlantı noktası 1999 hello PostgreSQL bağlantı noktası kullanın.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-112">In this case, use port 1999 as hello PostgreSQL port.</span></span>  

<span data-ttu-id="fe4cb-113">Toohello Linux PuTTY üzerinden oluşturulan VM bağlayın.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-113">Connect toohello Linux VM you created via PuTTY.</span></span> <span data-ttu-id="fe4cb-114">Bu hello Azure Linux VM'de kullanmakta olduğunuz ilk kez kullanıyorsanız, bkz: [nasıl tooUse Linux Azure üzerinde SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) nasıl toouse PuTTY toolearn tooconnect tooa Linux VM.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-114">If this is hello first time you're using an Azure Linux VM, see [How tooUse SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn how toouse PuTTY tooconnect tooa Linux VM.</span></span>

1. <span data-ttu-id="fe4cb-115">Komut tooswitch toohello kök (Yönetici) aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-115">Run hello following command tooswitch toohello root (admin):</span></span>
   
        # sudo su -
2. <span data-ttu-id="fe4cb-116">Bazı dağıtımları PostgreSQL yüklemeden önce yüklemelisiniz bağımlılıkları vardır.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-116">Some distributions have dependencies that you must install before installing PostgreSQL.</span></span> <span data-ttu-id="fe4cb-117">Bu listede, distro denetleyin ve hello uygun komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-117">Check for your distro in this list and run hello appropriate command:</span></span>
   
   * <span data-ttu-id="fe4cb-118">Red Hat temel Linux:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-118">Red Hat base Linux:</span></span>
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="fe4cb-119">Debian temel Linux:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-119">Debian base Linux:</span></span>
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="fe4cb-120">SUSE Linux:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-120">SUSE Linux:</span></span>
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. <span data-ttu-id="fe4cb-121">Merhaba kök dizinine PostgreSQL indirin ve hello paketin sıkıştırmasını açın:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-121">Download PostgreSQL into hello root directory, and then unzip hello package:</span></span>
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    <span data-ttu-id="fe4cb-122">Yukarıdaki Hello bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-122">hello above is an example.</span></span> <span data-ttu-id="fe4cb-123">Merhaba bulabilirsiniz daha ayrıntılı hello adresi karşıdan [dizin/pub programlarının/kaynak /](https://ftp.postgresql.org/pub/source/).</span><span class="sxs-lookup"><span data-stu-id="fe4cb-123">You can find hello more detailed download address in hello [Index of /pub/source/](https://ftp.postgresql.org/pub/source/).</span></span>
4. <span data-ttu-id="fe4cb-124">toostart hello derleme, bu komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-124">toostart hello build, run these commands:</span></span>
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. <span data-ttu-id="fe4cb-125">Merhaba belgeleri (HTML ve ADAM sayfaları) ve ek modülleri (contrib) dahil olmak üzere oluşturulabilir her şeyi toobuild istiyorsanız komutu yerine aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-125">If  you want toobuild everything that can be built, including hello documentation (HTML and man pages) and additional modules (contrib), run hello following command instead:</span></span>
   
        # gmake install-world
   
    <span data-ttu-id="fe4cb-126">Onay iletisi aşağıdaki hello almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-126">You should receive hello following confirmation message:</span></span>
   
        PostgreSQL, contrib, and documentation successfully made. Ready tooinstall.

## <a name="configure-postgresql"></a><span data-ttu-id="fe4cb-127">PostgreSQL yapılandırın</span><span class="sxs-lookup"><span data-stu-id="fe4cb-127">Configure PostgreSQL</span></span>
1. <span data-ttu-id="fe4cb-128">(İsteğe bağlı) Sembolik bağlantıyı tooshorten hello PostgreSQL başvuru oluşturmak toonot hello sürüm numarasını içerir:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-128">(Optional) Create a symbolic link tooshorten hello PostgreSQL reference toonot include hello version number:</span></span>
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. <span data-ttu-id="fe4cb-129">Merhaba veritabanı için bir dizin oluşturun:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-129">Create a directory for hello database:</span></span>
   
        # mkdir -p /opt/pgsql_data
3. <span data-ttu-id="fe4cb-130">Kök olmayan kullanıcı oluşturun ve o kullanıcının profilini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-130">Create a non-root user and modify that user’s profile.</span></span> <span data-ttu-id="fe4cb-131">Ardından, yeni kullanıcı toothis geçiş (adlı *postgres* örneğimizde):</span><span class="sxs-lookup"><span data-stu-id="fe4cb-131">Then, switch toothis new user (called *postgres* in our example):</span></span>
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > <span data-ttu-id="fe4cb-132">Güvenlik nedenleriyle, kök olmayan kullanıcı tooinitialize PostgreSQL kullanır, başlatma veya hello veritabanı kapatın.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-132">For security reasons, PostgreSQL uses a non-root user tooinitialize, start, or shut down hello database.</span></span>
   > 
   > 
4. <span data-ttu-id="fe4cb-133">Merhaba Düzenle *bash_profile* hello aşağıdaki komutları girerek dosya.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-133">Edit hello *bash_profile* file by entering hello commands below.</span></span> <span data-ttu-id="fe4cb-134">Bu satırlar hello toohello sonuna eklenecek *bash_profile* dosyası:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-134">These lines will be added toohello end of hello *bash_profile* file:</span></span>
   
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
5. <span data-ttu-id="fe4cb-135">Merhaba yürütme *bash_profile* dosyası:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-135">Execute hello *bash_profile* file:</span></span>
   
        $ source .bash_profile
6. <span data-ttu-id="fe4cb-136">Komutu aşağıdaki hello kullanarak yüklemenizi doğrulama:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-136">Validate your installation by using hello following command:</span></span>
   
        $ which psql
   
    <span data-ttu-id="fe4cb-137">Yükleme başarılı olursa, yanıt aşağıdaki hello görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-137">If your installation is successful, you will see hello following response:</span></span>
   
        /opt/pgsql/bin/psql
7. <span data-ttu-id="fe4cb-138">Merhaba PostgreSQL sürümü de denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-138">You can also check hello PostgreSQL version:</span></span>
   
        $ psql -V
8. <span data-ttu-id="fe4cb-139">Merhaba veritabanını başlatılamadı:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-139">Initialize hello database:</span></span>
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    <span data-ttu-id="fe4cb-140">Çıktı aşağıdaki hello almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-140">You should receive hello following output:</span></span>

![Görüntü](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a><span data-ttu-id="fe4cb-142">PostgreSQL ayarlayın</span><span class="sxs-lookup"><span data-stu-id="fe4cb-142">Set up PostgreSQL</span></span>
<!--    [postgres@ test ~]$ exit -->

<span data-ttu-id="fe4cb-143">Merhaba aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-143">Run hello following commands:</span></span>

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

<span data-ttu-id="fe4cb-144">Merhaba /etc/init.d/postgresql dosyasında iki değişkenleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-144">Modify two variables in hello /etc/init.d/postgresql file.</span></span> <span data-ttu-id="fe4cb-145">Merhaba önekini PostgreSQL toohello yükleme konumunu ayarlayın: **/opt/pgsql**.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-145">hello prefix is set toohello installation path of PostgreSQL: **/opt/pgsql**.</span></span> <span data-ttu-id="fe4cb-146">PGDATA PostgreSQL toohello veri depolama alanı yolu ayarlayın: **/opt/pgsql_data**.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-146">PGDATA is set toohello data storage path of PostgreSQL: **/opt/pgsql_data**.</span></span>

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![Görüntü](./media/postgresql-install/no2.png)

<span data-ttu-id="fe4cb-148">Değiştirme hello dosya toomake da çalıştırılabilir:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-148">Change hello file toomake it executable:</span></span>

    # chmod +x /etc/init.d/postgresql

<span data-ttu-id="fe4cb-149">PostgreSQL başlatın:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-149">Start PostgreSQL:</span></span>

    # /etc/init.d/postgresql start

<span data-ttu-id="fe4cb-150">PostgreSQL Hello uç noktasını üzerinde olup olmadığını kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-150">Check if hello endpoint of PostgreSQL is on:</span></span>

    # netstat -tunlp|grep 1999

<span data-ttu-id="fe4cb-151">Çıktı aşağıdaki hello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-151">You should see hello following output:</span></span>

![Görüntü](./media/postgresql-install/no3.png)

## <a name="connect-toohello-postgres-database"></a><span data-ttu-id="fe4cb-153">Toohello Postgres veritabanına bağlanın</span><span class="sxs-lookup"><span data-stu-id="fe4cb-153">Connect toohello Postgres database</span></span>
<span data-ttu-id="fe4cb-154">Bir kez daha toohello postgres kullanıcı anahtarı:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-154">Switch toohello postgres user once again:</span></span>

    # su - postgres

<span data-ttu-id="fe4cb-155">Postgres veritabanı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-155">Create a Postgres database:</span></span>

    $ createdb events

<span data-ttu-id="fe4cb-156">Yeni oluşturduğunuz toohello olayları veritabanına bağlanın:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-156">Connect toohello events database that you just created:</span></span>

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a><span data-ttu-id="fe4cb-157">Oluşturun ve Postgres tablo silme</span><span class="sxs-lookup"><span data-stu-id="fe4cb-157">Create and delete a Postgres table</span></span>
<span data-ttu-id="fe4cb-158">Toohello veritabanına bağlı, tablo içinde oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-158">Now that you have connected toohello database, you can create tables in it.</span></span>

<span data-ttu-id="fe4cb-159">Örneğin, komutu aşağıdaki hello kullanarak yeni bir örnek Postgres tablo oluşturun:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-159">For example, create a new example Postgres table by using hello following command:</span></span>

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

<span data-ttu-id="fe4cb-160">Şimdi hello ile dört sütunlu bir tablo ayarlamış olduğunuz sütun adları ve sınırlamaları aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-160">You have now set up a four-column table with hello following column names and restrictions:</span></span>

1. <span data-ttu-id="fe4cb-161">Merhaba VARCHAR komutu toobe tarafından altında 20 "ad" sütun bunlarla sınırlı hello karakter uzunluğunda.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-161">hello “name” column has been limited by hello VARCHAR command toobe under 20 characters long.</span></span>
2. <span data-ttu-id="fe4cb-162">Merhaba "yemek" sütun herkes getirecek hello yemek öğesi belirtir.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-162">hello “food” column indicates hello food item that each person will bring.</span></span> <span data-ttu-id="fe4cb-163">Bu metin toobe 30 karakter altında VARCHAR sınırlar.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-163">VARCHAR limits this text toobe under 30 characters.</span></span>
3. <span data-ttu-id="fe4cb-164">"hello kişi toohello Yemeğini Getir Partisi RSVP'd olup olmadığını hello sütun kayıtları onayladı".</span><span class="sxs-lookup"><span data-stu-id="fe4cb-164">hello “confirmed” column records whether hello person has RSVP’d toohello potluck.</span></span> <span data-ttu-id="fe4cb-165">"Y" ve "N" Merhaba kabul edilebilir değerler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-165">hello acceptable values are "Y" and "N".</span></span>
4. <span data-ttu-id="fe4cb-166">Bunlar hello olayı için kaydolurken tarih"hello" sütun gösterir.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-166">hello “date” column shows when they signed up for hello event.</span></span> <span data-ttu-id="fe4cb-167">Tarih yyyy-aa-gg yazılması Postgres gerektirir</span><span class="sxs-lookup"><span data-stu-id="fe4cb-167">Postgres requires that dates be written as yyyy-mm-dd.</span></span>

<span data-ttu-id="fe4cb-168">Tablonuz başarıyla oluşturulduysa hello şunları görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-168">You should see hello following if your table has been successfully created:</span></span>

![Görüntü](./media/postgresql-install/no4.png)

<span data-ttu-id="fe4cb-170">Ayrıca komut aşağıdaki hello kullanarak hello tablo yapısı kontrol edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-170">You can also check hello table structure by using hello following command:</span></span>

![Görüntü](./media/postgresql-install/no5.png)

### <a name="add-data-tooa-table"></a><span data-ttu-id="fe4cb-172">Veri tooa tablo ekleme</span><span class="sxs-lookup"><span data-stu-id="fe4cb-172">Add data tooa table</span></span>
<span data-ttu-id="fe4cb-173">İlk olarak, bilgileri bir satıra Ekle:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-173">First, insert information into a row:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

<span data-ttu-id="fe4cb-174">Bu çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-174">You should see this output:</span></span>

![Görüntü](./media/postgresql-install/no6.png)

<span data-ttu-id="fe4cb-176">Birkaç daha fazla kişi toohello tablo de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-176">You can add a couple more people toohello table as well.</span></span> <span data-ttu-id="fe4cb-177">İşte birkaç seçenek veya kendi oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-177">Here are some options, or you can create your own:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a><span data-ttu-id="fe4cb-178">Tabloları Göster</span><span class="sxs-lookup"><span data-stu-id="fe4cb-178">Show tables</span></span>
<span data-ttu-id="fe4cb-179">Komut tooshow tablo aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-179">Use hello following command tooshow a table:</span></span>

    select * from potluck;

<span data-ttu-id="fe4cb-180">Merhaba çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-180">hello output is:</span></span>

![Görüntü](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a><span data-ttu-id="fe4cb-182">Bir tablodaki verileri silme</span><span class="sxs-lookup"><span data-stu-id="fe4cb-182">Delete data in a table</span></span>
<span data-ttu-id="fe4cb-183">Aşağıdaki tablodaki komut toodelete verileri hello kullan:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-183">Use hello following command toodelete data in a table:</span></span>

    delete from potluck where name=’John’;

<span data-ttu-id="fe4cb-184">Merhaba "John" satır tüm hello bilgileri siler.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-184">This deletes all hello information in hello "John" row.</span></span> <span data-ttu-id="fe4cb-185">Merhaba çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="fe4cb-185">hello output is:</span></span>

![Görüntü](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a><span data-ttu-id="fe4cb-187">Bir tablodaki verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="fe4cb-187">Update data in a table</span></span>
<span data-ttu-id="fe4cb-188">Aşağıdaki tablodaki komut tooupdate verileri hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-188">Use hello following command tooupdate data in a table.</span></span> <span data-ttu-id="fe4cb-189">"N" den kendi RSVP çok değiştirmek şekilde bu biri için aynen katılan olmadığını, Sandy onayladığından "Y":</span><span class="sxs-lookup"><span data-stu-id="fe4cb-189">For this one, Sandy has confirmed that she is attending, so we will change her RSVP from "N" too"Y":</span></span>

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a><span data-ttu-id="fe4cb-190">PostgreSQL hakkında daha fazla bilgi alın</span><span class="sxs-lookup"><span data-stu-id="fe4cb-190">Get more information about PostgreSQL</span></span>
<span data-ttu-id="fe4cb-191">Merhaba yüklemesini PostgreSQL Azure Linux VM'de tamamladığınıza göre Azure'da kullanarak keyfini çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe4cb-191">Now that you have completed hello installation of PostgreSQL in an Azure Linux VM, you can enjoy using it in Azure.</span></span> <span data-ttu-id="fe4cb-192">toolearn PostgreSQL, hakkında daha fazla ziyaret hello [PostgreSQL Web sitesi](http://www.postgresql.org/).</span><span class="sxs-lookup"><span data-stu-id="fe4cb-192">toolearn more about PostgreSQL, visit hello [PostgreSQL website](http://www.postgresql.org/).</span></span>

