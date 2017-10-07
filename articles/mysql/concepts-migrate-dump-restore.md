---
title: "MySQL veritabanı kullanarak dökümü ve geri yükleme, Azure veritabanı'nda MySQL için aaaMigrate | Microsoft Docs"
description: "Bu makalede, MySQL, mysqldump, MySQL çalışma ekranı ve PHPMyAdmin gibi araçları kullanarak için iki ortak yolları tooback yedeklemek ve geri yükleme veritabanları Azure veritabanınızdaki açıklanmaktadır."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: d05d483ff53483df8e005eae2d9a4f8190e8f663
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-mysql-database-tooazure-database-for-mysql-using-dump-and-restore"></a>MySQL veritabanı tooAzure veritabanı için MySQL döküm ve geri yükleme kullanarak geçirme
Bu makalede yukarı iki genel yolu tooback açıklar ve MySQL için Azure veritabanınızdaki veritabanlarını geri yükleyin
- Döküm ve geri yükleme komut satırı (mysqldump kullanarak) hello 
- Döküm ve PHPMyAdmin kullanarak geri yükleme 

## <a name="before-you-begin"></a>Başlamadan önce
toostep bu nasıl tooguide aracılığıyla toohave gerekir:
- [MySQL server - Azure portalında Azure veritabanı oluşturma](quickstart-create-mysql-server-database-using-azure-portal.md)
- [mysqldump](https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html) komut satırı yardımcı programı bir makinede yüklü.
- MySQL çalışma ekranı [çalışma ekranı MySQL karşıdan](https://dev.mysql.com/downloads/workbench/), kurbağa, Navicat veya dökümü ve geri yükleme komutları diğer üçüncü taraf MySQL aracı toodo.

## <a name="use-common-tools"></a>Ortak araçlarını kullanma
MySQL çalışma ekranı, mysqldump, kurbağa veya Navicat tooremotely gibi araçları bağlanmak ve veri MySQL için Azure veritabanına geri yükleme ve genel yardımcı programını kullanın. MySQL için bir Internet bağlantısı tooconnect toohello Azure veritabanı ile istemci makinenizde gibi araçlar kullanın. Bir SSL şifreli bağlantı için en iyi güvenlik uygulamalarını kullanın, ayrıca bkz. [yapılandırma SSL bağlantısı MySQL için Azure veritabanında](concepts-ssl-connection-security.md). TooAzure veritabanı için MySQL geçirilirken toomove hello döküm dosyaları tooany özel bulut konumu gerekmez. 

## <a name="common-uses-for-dump-and-restore"></a>Ortak kullanımlar döküm ve geri yükleme için
Bir Azure MySQL veritabanına MySQL yardımcı programları mysqldump ve mysqlpump toodump ve yük veritabanları gibi birkaç ortak senaryoda kullanabilir. Diğer senaryolarda hello kullanabilir [içeri ve dışarı aktarma](concepts-migrate-import-export.md) yerine yaklaşımını.

- Merhaba tüm veritabanını geçirilirken veritabanını kullan dökümünü yapar. Bu öneri, büyük miktarda MySQL veri taşırken ya da Canlı siteler veya uygulamalar için toominimize hizmet kesintisi istediğinizde barındırır. 
-  Verileri için MySQL Azure veritabanına yüklenirken hello veritabanındaki tüm tabloların hello InnoDB depolama altyapısı kullandığınızdan emin olun. Azure veritabanı için MySQL yalnızca InnoDB depolama altyapısını destekler ve bu nedenle alternatif depolama altyapılarını desteklemez. Tablolarınızı diğer depolama altyapılarını ile yapılandırılmışsa, bunları hello InnoDB altyapısı biçimi önce geçiş tooAzure veritabanı için MySQL dönüştürün.
   WordPress veya hello MyISAM tabloları kullanarak WebApp varsa, örneğin, önce bu tablolar için MySQL tooAzure veritabanını geri yüklemeden önce InnoDB biçimine geçirerek dönüştürün. Kullanım hello yan tümcesi `ENGINE=InnoDB` tooset hello yeni bir tablo oluştururken kullanılan altyapısının sonra hello geri önce hello uyumlu tabloya hello veri aktarma. 

   ```sql
   INSERT INTO innodb_table SELECT * FROM myisam_table ORDER BY primary_key_columns
   ```
- tooavoid tüm uyumluluk sorunları, MySQL aynı sürümü hello kaynak ve hedef sistemlerde veritabanları çıkarırken kullanılan hello emin olun. Örneğin, mevcut MySQL sunucunuzu sürüm 5.7 ise, tooAzure veritabanı için MySQL yapılandırılmış toorun sürüm 5.7 geçirmeniz gerekir. Merhaba `mysql_upgrade` komutu MySQL sunucusu için bir Azure veritabanındaki çalışmaz ve desteklenmez. MySQL sürümleri arasında tooupgrade gerekiyorsa, ilk dökümü veya alt sürüm veritabanınızı MySQL daha yüksek bir sürüm kendi ortamınızda verin. Ardından çalıştırın `mysql_upgrade`, MySQL için bir Azure veritabanına geçiş işlemini denemeden önce.

## <a name="performance-considerations"></a>Performansla ilgili önemli noktalar
toooptimize performans, büyük veritabanları çıkarırken Bu noktalar Al duyuru:
-   Kullanım hello `exclude-triggers` veritabanları çıkarırken mysqldump seçeneği. Tetikleyiciler döküm dosyaları tooavoid hello tetikleyici komutları hello veri geri yükleme sırasında tetikleme dışında bırakın. 
-   Merhaba kaçının `single-transaction` çok büyük veritabanları çıkarırken mysqldump seçeneği. Tek bir işlem içinde çok sayıda tabloya dökme ek depolama alanı neden olur ve bellek kaynakları toobe geri yükleme sırasında tüketilen ve performans gecikmeler veya kaynak kısıtlamaları neden olabilir.
-   SQL toominimize deyimi yürütme yükü ile veritabanları çıkarırken yüklenirken kullanım çoklu değer ekler. Çoklu değer ekler mysqldump yardımcı programı tarafından üretilen döküm dosyaları kullanırken, varsayılan olarak etkinleştirilir. 
-  Kullanım hello `order-by-primary` veritabanları, böylece birincil anahtar sırayla hello veri komut dosyasıyla çıkarırken mysqldump seçeneği.
-   Kullanım hello `disable-keys` veri, toodisable yabancı anahtar kısıtlamaları, yük önce çıkarırken mysqldump seçeneği. Yabancı anahtar denetimleri devre dışı bırakma performans artışı sağlar. Hello kısıtlamaları etkinleştirin ve sonra hello yük tooensure başvuru bütünlüğü hello veri doğrulayın.
-   Uygun olduğunda bölümlenmiş tabloları kullanın.
-   Paralel veri yükleyin. Kaynak sınırına toohit neden, ve hello ölçümleri hello Azure portalında kullanılabilir kullanarak kaynakları izlemek çok fazla paralellik kaçının. 
-   Kullanım hello `defer-table-indexes` veritabanları, böylece dizin oluşturma tabloları veriler yüklendikten sonra gerçekleşir çıkarırken mysqlpump seçeneği.

## <a name="create-a-backup-file-from-hello-command-line-using-mysqldump"></a>Bir yedekleme dosyası hello komut satırı oluşturmak mysqldump kullanma
tooback mevcut bir MySQL veritabanı hello yerel yukarı şirket içi sunucu veya bir sanal makine hello aşağıdaki komutu çalıştırın: 
```bash
$ mysqldump --opt -u [uname] -p[pass] [dbname] > [backupfile.sql]
```

Merhaba parametreleri tooprovide şunlardır:
- [uname] Veritabanı kullanıcı adı 
- [geçiş] hello parola veritabanınız için (-p hello parola arasındaki alan yok unutmayın) 
- Veritabanınızın [dbname] hello adı 
- Veritabanı yedeklemesi için [backupfile.sql] hello dosya adı 
- [--opt] hello mysqldump seçeneği 

Örneğin, bir veritabanını tooback 'testdb' MySQL sunucunuzda hello kullanıcıadı 'testuser' ile hiçbir parola tooa dosya testdb_backup.sql adlı, komutu aşağıdaki hello kullanın. Merhaba komutu yedekler hello `testdb` adlı bir dosya veritabanına `testdb_backup.sql`, tüm hello SQL deyimleri içeren toore gerekli-hello veritabanı oluşturun. 

```bash
$ mysqldump -u root -p testdb > testdb_backup.sql
```
tooselect belirli, veritabanı tooback tablolarda, liste hello tablo adlarının boşlukla ayrılmış. Örneğin, tooback hello 'testdb','ün yalnızca tablo1 ve tablo2 tablolarının tablolardan ayarlama, bu örnek izleyin: 
```bash
$ mysqldump -u root -p testdb table1 table2 > testdb_tables_backup.sql
```

Veritabanı tooback anda kullanım hello--birden fazla veritabanını geçin ve liste hello veritabanı adları boşluklarla ayrılmış. 
```bash
$ mysqldump -u root -p --databases testdb1 testdb3 testdb5 > testdb135_backup.sql 
```
tooback aynı anda hello Server'daki tüm hello veritabanlarını hello--tüm veritabanları seçeneği kullanmanız gerekir.
```
$ mysqldump -u root -p --all-databases > alldb_backup.sql 
```

## <a name="create-a-database-on-hello-target-azure-database-for-mysql-server"></a>MySQL sunucusu için hello hedef Azure veritabanı bir veritabanı oluşturma
Hedefte hello Azure veritabanı toomigrate hello verilerin istediğiniz MySQL sunucusu için boş bir veritabanı oluşturun. MySQL çalışma ekranı, kurbağa veya Navicat toocreate hello veritabanı gibi bir araç kullanın. Merhaba veritabanı aynı kapsanan hello yazılan veriler hello veritabanı olarak ad hello sahip olabilir veya farklı bir adla bir veritabanı oluşturabilirsiniz.

tooget bağlı, MySQL için Azure veritabanı'nda hello özellikleri sayfasında hello bağlantı bilgilerini bulun.
![Hello Azure portal Hello bağlantı bilgilerini Bul](./media/concepts-migrate-dump-restore/1_server-properties-name-login.png)

MySQL çalışma ekranı Hello bağlantı bilgilerini ekleyin.
![MySQL çalışma ekranı bağlantı dizesi](./media/concepts-migrate-dump-restore/2_setup-new-connection.png)


## <a name="restore-your-mysql-database-using-command-line-or-mysql-workbench"></a>Komut satırı kullanarak MySQL veritabanı veya MySQL çalışma ekranı geri yükleme
Merhaba hedef veritabanı oluşturduktan sonra hello mysql komutu ya da yeni veritabanı hello döküm dosyasından oluşturulan MySQL çalışma ekranı toorestore hello verisine hello belirli kullanabilirsiniz.
```bash
mysql -h [hostname] -u [uname] -p[pass] [db_to_restore] < [backupfile.sql]
```
Bu örnekte, veritabanı hedefte hello Azure veritabanı MySQL sunucusu için yeni oluşturulan hello içine hello verileri geri yükleyin.
```bash
$ mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p testdb < testdb_backup.sql
```

## <a name="export-using-phpmyadmin"></a>PHPMyAdmin kullanarak dışa aktarın
tooexport, hangi zaten yerel olarak ortamınızda yüklü hello ortak aracı phpMyAdmin, kullanabilirsiniz. tooexport PHPMyAdmin kullanarak MySQL veritabanını:
- PhpMyAdmin açın.
- Veritabanınızı seçin. Merhaba soldaki hello listesinde Hello veritabanı adını tıklatın. 
- Merhaba tıklatın **verme** bağlantı. Tooview hello döküm veritabanının yeni bir sayfa görüntülenir.
- Merhaba Hello dışa aktarma alanını tıklatın **Tümünü Seç** veritabanınızdaki toochoose hello tablolar bağlantı. 
- Hello SQL Seçenekleri alanında, hello uygun seçenekleri'ni tıklatın. 
- Hello tıklatın **dosyası olarak kaydetmeniz** seçeneği hello karşılık gelen sıkıştırma seçeneğini tıklatın ve sonra hello **gidin** düğmesi. Bir iletişim kutusu sorulma, toosave hello dosyasını yerel olarak görünmelidir.

## <a name="import-using-phpmyadmin"></a>PHPMyAdmin kullanarak içe aktarma
Veritabanınızı alma benzer tooexporting olur. Aşağıdaki işlemleri hello:
- PhpMyAdmin açın. 
- Merhaba phpMyAdmin Kurulum sayfasında tıklatın **Ekle** tooadd Azure veritabanı için MySQL sunucu. Merhaba bağlantı ayrıntılarını ve oturum açma bilgileri sağlayın.
- Uygun adlandırılmış bir veritabanı oluşturun ve Merhaba ekranında hello solda seçin. toorewrite varolan bir veritabanını Merhaba, hello veritabanı adına tıklayın, tüm hello hello tablo adlarının yanındaki onay kutularını seçin ve seçin **bırakma** toodelete hello var olan tablo. 
- Merhaba tıklatın **SQL** bağlantı tooshow hello sayfa buradan SQL komutları yazın, veya SQL dosyanızı karşıya yükleyin. 
- Kullanım hello **Gözat** düğmesini toofind hello veritabanı dosyası. 
- Merhaba tıklatın **Git** düğmesini tooexport hello yedekleme, hello SQL komutları yürütün ve veritabanınızı yeniden oluşturun.

## <a name="next-steps"></a>Sonraki adımlar
[MySQL için uygulamalar tooAzure veritabanına bağlan](./howto-connection-string.md)
