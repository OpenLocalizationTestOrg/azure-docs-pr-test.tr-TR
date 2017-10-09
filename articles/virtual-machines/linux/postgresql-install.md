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
# <a name="install-and-configure-postgresql-on-azure"></a>Azure’da PostgreSQL yükleme ve yapılandırma
PostgreSQL bir Gelişmiş açık kaynak veritabanı benzer tooOracle ve DB2 ' dir. Tam ACID uyumluluk, güvenilir işlem işleme ve çoklu sürüm eşzamanlılık denetimi gibi Kurumsal kullanıma hazır özellikler içerir. Ayrıca, ANSI SQL ve SQL/MED (Oracle, MySQL, MongoDB ve diğer birçok için yabancı veri sarmalayıcıları dahil) gibi standartlara destekler. Desteğiyle üzerinde 12 yordam diller, GIN ve GiST dizinleri, uzamsal veri desteği ve birden çok NoSQL benzeri özellikleri JSON veya anahtar-değer tabanlı uygulamalar için yüksek oranda genişletilebilir.

Bu makalede, öğreneceksiniz nasıl tooinstall ve bir Azure Linux çalıştıran sanal makine üzerinde PostgreSQL yapılandırın.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a>PostgreSQL yükleyin
> [!NOTE]
> Bu öğretici sipariş toocomplete Linux çalıştıran bir Azure sanal makinesi zaten olmalıdır. bkz: toocreate ve devam etmeden önce bir Linux VM ayarlama [Azure Linux VM'de Öğreticisi](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

Bu durumda, bağlantı noktası 1999 hello PostgreSQL bağlantı noktası kullanın.  

Toohello Linux PuTTY üzerinden oluşturulan VM bağlayın. Bu hello Azure Linux VM'de kullanmakta olduğunuz ilk kez kullanıyorsanız, bkz: [nasıl tooUse Linux Azure üzerinde SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) nasıl toouse PuTTY toolearn tooconnect tooa Linux VM.

1. Komut tooswitch toohello kök (Yönetici) aşağıdaki hello çalıştırın:
   
        # sudo su -
2. Bazı dağıtımları PostgreSQL yüklemeden önce yüklemelisiniz bağımlılıkları vardır. Bu listede, distro denetleyin ve hello uygun komutu çalıştırın:
   
   * Red Hat temel Linux:
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * Debian temel Linux:
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * SUSE Linux:
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. Merhaba kök dizinine PostgreSQL indirin ve hello paketin sıkıştırmasını açın:
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    Yukarıdaki Hello bir örnektir. Merhaba bulabilirsiniz daha ayrıntılı hello adresi karşıdan [dizin/pub programlarının/kaynak /](https://ftp.postgresql.org/pub/source/).
4. toostart hello derleme, bu komutları çalıştırın:
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. Merhaba belgeleri (HTML ve ADAM sayfaları) ve ek modülleri (contrib) dahil olmak üzere oluşturulabilir her şeyi toobuild istiyorsanız komutu yerine aşağıdaki hello çalıştırın:
   
        # gmake install-world
   
    Onay iletisi aşağıdaki hello almanız gerekir:
   
        PostgreSQL, contrib, and documentation successfully made. Ready tooinstall.

## <a name="configure-postgresql"></a>PostgreSQL yapılandırın
1. (İsteğe bağlı) Sembolik bağlantıyı tooshorten hello PostgreSQL başvuru oluşturmak toonot hello sürüm numarasını içerir:
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. Merhaba veritabanı için bir dizin oluşturun:
   
        # mkdir -p /opt/pgsql_data
3. Kök olmayan kullanıcı oluşturun ve o kullanıcının profilini değiştirin. Ardından, yeni kullanıcı toothis geçiş (adlı *postgres* örneğimizde):
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > Güvenlik nedenleriyle, kök olmayan kullanıcı tooinitialize PostgreSQL kullanır, başlatma veya hello veritabanı kapatın.
   > 
   > 
4. Merhaba Düzenle *bash_profile* hello aşağıdaki komutları girerek dosya. Bu satırlar hello toohello sonuna eklenecek *bash_profile* dosyası:
   
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
5. Merhaba yürütme *bash_profile* dosyası:
   
        $ source .bash_profile
6. Komutu aşağıdaki hello kullanarak yüklemenizi doğrulama:
   
        $ which psql
   
    Yükleme başarılı olursa, yanıt aşağıdaki hello görürsünüz:
   
        /opt/pgsql/bin/psql
7. Merhaba PostgreSQL sürümü de denetleyebilirsiniz:
   
        $ psql -V
8. Merhaba veritabanını başlatılamadı:
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    Çıktı aşağıdaki hello almanız gerekir:

![Görüntü](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a>PostgreSQL ayarlayın
<!--    [postgres@ test ~]$ exit -->

Merhaba aşağıdaki komutları çalıştırın:

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

Merhaba /etc/init.d/postgresql dosyasında iki değişkenleri değiştirin. Merhaba önekini PostgreSQL toohello yükleme konumunu ayarlayın: **/opt/pgsql**. PGDATA PostgreSQL toohello veri depolama alanı yolu ayarlayın: **/opt/pgsql_data**.

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![Görüntü](./media/postgresql-install/no2.png)

Değiştirme hello dosya toomake da çalıştırılabilir:

    # chmod +x /etc/init.d/postgresql

PostgreSQL başlatın:

    # /etc/init.d/postgresql start

PostgreSQL Hello uç noktasını üzerinde olup olmadığını kontrol edin:

    # netstat -tunlp|grep 1999

Çıktı aşağıdaki hello görmeniz gerekir:

![Görüntü](./media/postgresql-install/no3.png)

## <a name="connect-toohello-postgres-database"></a>Toohello Postgres veritabanına bağlanın
Bir kez daha toohello postgres kullanıcı anahtarı:

    # su - postgres

Postgres veritabanı oluşturun:

    $ createdb events

Yeni oluşturduğunuz toohello olayları veritabanına bağlanın:

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a>Oluşturun ve Postgres tablo silme
Toohello veritabanına bağlı, tablo içinde oluşturabilirsiniz.

Örneğin, komutu aşağıdaki hello kullanarak yeni bir örnek Postgres tablo oluşturun:

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

Şimdi hello ile dört sütunlu bir tablo ayarlamış olduğunuz sütun adları ve sınırlamaları aşağıdaki:

1. Merhaba VARCHAR komutu toobe tarafından altında 20 "ad" sütun bunlarla sınırlı hello karakter uzunluğunda.
2. Merhaba "yemek" sütun herkes getirecek hello yemek öğesi belirtir. Bu metin toobe 30 karakter altında VARCHAR sınırlar.
3. "hello kişi toohello Yemeğini Getir Partisi RSVP'd olup olmadığını hello sütun kayıtları onayladı". "Y" ve "N" Merhaba kabul edilebilir değerler şunlardır.
4. Bunlar hello olayı için kaydolurken tarih"hello" sütun gösterir. Tarih yyyy-aa-gg yazılması Postgres gerektirir

Tablonuz başarıyla oluşturulduysa hello şunları görmeniz gerekir:

![Görüntü](./media/postgresql-install/no4.png)

Ayrıca komut aşağıdaki hello kullanarak hello tablo yapısı kontrol edebilirsiniz:

![Görüntü](./media/postgresql-install/no5.png)

### <a name="add-data-tooa-table"></a>Veri tooa tablo ekleme
İlk olarak, bilgileri bir satıra Ekle:

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

Bu çıktı görmeniz gerekir:

![Görüntü](./media/postgresql-install/no6.png)

Birkaç daha fazla kişi toohello tablo de ekleyebilirsiniz. İşte birkaç seçenek veya kendi oluşturabilirsiniz:

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a>Tabloları Göster
Komut tooshow tablo aşağıdaki hello kullan:

    select * from potluck;

Merhaba çıktısı şöyledir:

![Görüntü](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a>Bir tablodaki verileri silme
Aşağıdaki tablodaki komut toodelete verileri hello kullan:

    delete from potluck where name=’John’;

Merhaba "John" satır tüm hello bilgileri siler. Merhaba çıktısı şöyledir:

![Görüntü](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a>Bir tablodaki verileri güncelleştirme
Aşağıdaki tablodaki komut tooupdate verileri hello kullanın. "N" den kendi RSVP çok değiştirmek şekilde bu biri için aynen katılan olmadığını, Sandy onayladığından "Y":

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a>PostgreSQL hakkında daha fazla bilgi alın
Merhaba yüklemesini PostgreSQL Azure Linux VM'de tamamladığınıza göre Azure'da kullanarak keyfini çıkarabilirsiniz. toolearn PostgreSQL, hakkında daha fazla ziyaret hello [PostgreSQL Web sitesi](http://www.postgresql.org/).

