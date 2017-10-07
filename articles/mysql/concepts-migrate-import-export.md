---
title: "aaaImport ve Azure veritabanı'nda MySQL için dışarı aktarma | Microsoft Docs"
description: "Bu makalede Azure veritabanında ortak yolları tooimport ve dışarı aktarma veritabanları, MySQL için MySQL çalışma ekranı gibi araçları kullanarak açıklanmaktadır."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: e2c036773d975df2eea2a59d166ea10567218a41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-mysql-database-by-using-import-and-export"></a>İçeri aktarma kullanarak MySQL veritabanınızı geçirin ve dışarı aktarma
Bu makalede, MySQL çalışma ekranı kullanarak iki ortak yaklaşımlar tooimporting ve dışarı aktarma veri tooan Azure veritabanı MySQL sunucusu için açıklanmaktadır. 

## <a name="before-you-begin"></a>Başlamadan önce
toostep bu nasıl tooguide aracılığıyla, aşağıdakiler gerekir:
- MySQL sunucusu için izleyerek, Azure veritabanı [Azure portalını kullanarak MySQL sunucusu için bir Azure veritabanı oluşturma](quickstart-create-mysql-server-database-using-azure-portal.md).
- MySQL çalışma ekranı [indirilen](https://dev.mysql.com/downloads/workbench/), veya başka bir MySQL aracı tooimport ve dışarı aktarma.

## <a name="use-common-tools"></a>Ortak araçlarını kullanma
MySQL çalışma ekranı, kurbağa veya Navicat tooremotely bağlanmak ve içeri aktarma veya veri Azure veritabanına MySQL için dışarı aktarma gibi genel araçlarını kullanın. 

MySQL için bir Internet bağlantısı tooconnect tooAzure veritabanı ile istemci makinenizde gibi araçlar kullanın. Bir SSL şifreli bağlantı açıklandığı gibi en iyi güvenlik uygulamalarını kullanın [yapılandırma SSL bağlantısı MySQL için Azure veritabanında](concepts-ssl-connection-security.md).

Değil toomove almanız gerekir ve tooAzure veritabanı için MySQL geçirilirken dosyaları tooany özel bulut konumunu verin. 

## <a name="create-a-database-on-hello-azure-database-for-mysql-server"></a>Hello Azure veritabanı MySQL sunucusu için bir veritabanı oluşturma
Hello Azure veritabanı toomigrate hello verilerin istediğiniz MySQL sunucusu için boş bir veritabanı oluşturun. MySQL çalışma ekranı, kurbağa veya Navicat toocreate hello veritabanı gibi bir araç kullanın. Merhaba veritabanı hello yazılan hello verileri veya içeren hello veritabanı farklı bir adla bir veritabanı oluşturmak gibi aynı adı olabilir.

bağlı, tooget bulun hello bağlantı bilgilerini hello üzerinde **özellikleri** Azure veritabanı için MySQL bölmesinde.

![Hello Azure portal Hello bağlantı bilgilerini Bul](./media/concepts-migrate-import-export/1_server-properties-name-login.png)

Merhaba bağlantı bilgileri tooMySQL çalışma ekranı ekleyin.

![MySQL çalışma ekranı bağlantı dizesi](./media/concepts-migrate-import-export/2_setup-new-connection.png)

## <a name="determine-when-toouse-import-and-export-techniques-instead-of-a-dump-and-restore"></a>Ne zaman toouse alma ve teknikleri döküm ve geri yükleme yerine verme belirleme
MySQL araçları tooimport kullanın ve veritabanları senaryoları aşağıdaki hello Azure MySQL veritabanına verin. Diğer senaryolarda hello kullanarak yararlanabilir [dökümü ve geri yükleme](concepts-migrate-dump-restore.md) yerine yaklaşımını. 

- Tooselectively gerektiğinde birkaç tabloları tooimport varolan bir MySQL veritabanından Azure MySQL veritabanına seçin, buna ait en iyi toouse alma hello ve teknik dışarı aktarma.  Bunu yaparak, hello geçiş toosave zaman ve kaynak gereksiz tüm tablolardan atlayabilirsiniz. Örneğin, hello kullan `--include-tables` veya `--exclude-tables` anahtarı ile [mysqlpump](https://dev.mysql.com/doc/refman/5.7/en/mysqlpump.html#option_mysqlpump_include-tables) ve hello `--tables` anahtarı ile [mysqldump](https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html#option_mysqldump_tables).
- Açıkça hello veritabanı nesnelerini tabloları dışında taşırken bunları oluşturun. Toomigrate istediğiniz herhangi bir veritabanı nesneleri ve kısıtlamalar (birincil anahtar, yabancı anahtar, dizinler), görünümleri, işlevleri, yordamlar, Tetikleyiciler içerir.
- Bir MySQL veritabanı dışında dış veri kaynaklarından veri geçişini, düz dosyalarını oluşturmak ve bunları kullanarak içeri [mysqlimport](https://dev.mysql.com/doc/refman/5.7/en/mysqlimport.html).

Azure veritabanına veri MySQL için yüklemekte olduğunuz zaman hello veritabanındaki tüm tabloların hello InnoDB depolama altyapısı kullandığınızdan emin olun. Azure veritabanı için MySQL yalnızca hello InnoDB depolama altyapısı destekler, bu nedenle alternatif depolama altyapılarını desteklemiyor. Alternatif depolama altyapılarını tablolarınızı ihtiyacınız varsa emin tooconvert olması bunları hello geçiş tooAzure MySQL veritabanını daha önce toouse hello InnoDB altyapısı biçimi. 

Merhaba MyISAM altyapısını kullanan bir WordPress veya web uygulaması varsa, örneğin, ilk hello tabloları hello veri geçişi InnoDB tablolara Dönüştür. Ardından tooAzure veritabanı için MySQL geri yükleyin. Kullanım hello yan tümcesi `ENGINE=INNODB` tooset hello tablo oluşturma için altyapısı ve hello geçişten önce hello uyumlu tabloya hello veri aktarın. 

   ```sql
   INSERT INTO innodb_table SELECT * FROM myisam_table ORDER BY primary_key_columns
   ```

## <a name="performance-recommendations-for-import-and-export"></a>İçeri ve dışarı aktarma için performans önerileri
-   Kümelenmiş dizinler ve birincil anahtarlar veri yüklemeden önce oluşturun. Birincil anahtar sırayla veri yükleyin. 
-   Gecikme veri kadar sonra ikincil dizinlerin oluşturulmasını yüklenir. Tüm İkincil dizinler yüklemeden sonra oluşturun. 
-   Yüklemeden önce yabancı anahtar kısıtlamaları devre dışı bırakın. Yabancı anahtar denetimleri devre dışı bırakma önemli ölçüde performans artışı sağlar. Hello kısıtlamaları etkinleştirin ve sonra hello yük tooensure başvuru bütünlüğü hello veri doğrulayın.
-   Paralel veri yükleyin. Kaynak sınırına toohit neden, ve kaynakları hello ölçümleri hello Azure portalında kullanılabilir kullanarak izlemek çok fazla paralellik kaçının. 
-   Uygun olduğunda bölümlenmiş tabloları kullanın.

## <a name="import-and-export-by-using-mysql-workbench"></a>İçeri ve dışarı aktarma MySQL çalışma ekranı kullanarak
MySQL çalışma ekranı içinde tooexport ve içeri aktarma verileri iki yolu vardır. Her farklı bir amaca hizmet eder. 

### <a name="table-data-export-and-import-wizards-from-hello-object-browsers-context-menu"></a>Tablo verisi sihirbazları hello nesne tarayıcının bağlam menüsünden alma ve verme
![Merhaba nesne tarayıcının bağlam menüsünde MySQL çalışma ekranı sihirbazları](./media/concepts-migrate-import-export/p1.png)

Tablo verisi için Hello sihirbazları alma desteği ve CSV ve JSON dosyaları kullanılarak verme işlemleri. Ayırıcılar, sütun seçimi ve kodlama seçimi gibi çeşitli yapılandırma seçenekleri içerirler. Yerel veya uzaktan bağlı MySQL sunucuları karşı her bir sihirbazın gerçekleştirebilirsiniz. Merhaba alma eylemi tablo, sütun ve tür eşlemesi içerir. 

Bir tablo sağ tıklayarak, bu sihirbazlar hello nesne tarayıcının bağlam menüsünden erişebilirsiniz. Ya da seçin **tablo verileri dışarı Aktarma Sihirbazı** veya **tablo veri içeri aktarma Sihirbazı'nı**. 

#### <a name="table-data-export-wizard"></a>Tablo verileri dışarı Aktarma Sihirbazı
Merhaba aşağıdaki örnek hello tablo tooa CSV dosyası verir: 
1. Dışa aktarılan hello veritabanı toobe Merhaba tablonun sağ tıklayın. 
2. Seçin **tablo verileri dışarı Aktarma Sihirbazı'nı**. Verdiğiniz hello sütunları toobe satır uzaklığı (varsa) seçin ve (varsa) sayısı. 
3. Merhaba üzerinde **seçin verileri dışarı aktarma** sayfasında, **sonraki**. Merhaba dosya yolu, CSV veya JSON seçin dosya türü. Ayrıca hello satır ayırıcı dizeler ve alan ayırıcı kapsayan yöntemi seçin. 
4. Merhaba üzerinde **Select çıkış dosyasının konumu** sayfasında, **sonraki**. 
5. Merhaba üzerinde **dışarı veri** sayfasında, **sonraki**.

#### <a name="table-data-import-wizard"></a>Tablo verileri İçeri Aktarma Sihirbazı
Merhaba aşağıdaki örnek hello tablo bir CSV dosyasından içeri aktarır:
1. Alınan hello veritabanı toobe Merhaba tablonun sağ tıklayın. 
2. Gözat tooand seçin, içe aktarılan CSV dosyasını toobe hello ve ardından **sonraki**. 
3. Seçin veya temizleyin hello seçip Hello hedef tablosu (yeni veya varolan) **içe aktarma işleminden önce Truncate table** onay kutusu. **İleri**’ye tıklayın.
4. İçeri aktarılan kodlama ve hello sütunları toobe seçin ve ardından **sonraki**. 
5. Merhaba üzerinde **veri içeri aktarma** sayfasında, **sonraki**. Merhaba Sihirbazı uygun şekilde hello verileri içeri aktarır.

### <a name="sql-data-export-and-import-wizards-from-hello-navigator-pane"></a>SQL veri sihirbazları hello Gezgini bölmesinden alma ve verme
Sihirbaz tooexport kullanın veya MySQL çalışma ekranından oluşturulan veya hello mysqldump komuttan üretilen SQL içeri aktarın. Bu sihirbazlar hello erişim **Gezgini** bölmesinde veya seçerek **Server** hello ana menüden. Ardından **verilerini dışa aktarma** veya **veri alma**. 

#### <a name="data-export"></a>Verileri dışarı aktarma
![Merhaba Gezgin bölmesini kullanarak MySQL çalışma ekranı verileri dışarı aktarma](./media/concepts-migrate-import-export/p2.png)

Merhaba kullanabilirsiniz **verilerini dışa aktarma** tooexport MySQL verilerinizi sekmesinde. 
1. Tooexport isterseniz, isteğe bağlı olarak her şemadan belirli şema nesneleri/tabloları seçin ve hello verme oluşturmak, her şema seçin. Yapılandırma seçenekleri verme tooa proje klasörünü veya kendi içinde bulunan SQL dosyası dahil, saklı yordamları ve olayları dökümü veya tablo verileri atlayabilirsiniz. 
 
   Alternatif olarak, kullanın **bir sonuç kümesi verme** tooexport belirli bir sonuç kümesi biçiminde hello SQL Düzenleyicisi tooanother, CSV, JSON, HTML ve XML gibi. 
3. Merhaba veritabanı nesneleri tooexport'ı seçin ve yapılandırın hello ilgili seçenekler.
4. Tıklatın **yenileme** tooload hello geçerli nesneleri.
5. İsteğe bağlı olarak, hello açmak **Gelişmiş Seçenekler** sekmesinde toorefine hello dışa aktarma işlemi. Örneğin, tablo kilitleri, kullanım Değiştir INSERT deyimleri ve teklif tanımlayıcıları backtick karakterlerle yerine ekleyin.
6. Tıklatın **Başlat verme** toobegin hello dışa aktarma işlemi.


#### <a name="data-import"></a>Veri alma
![Yönetim Gezgini kullanarak MySQL çalışma ekranı veri alma](./media/concepts-migrate-import-export/p3.png)

Merhaba kullanabilirsiniz **veri alma** tooimport sekmesinde veya dışarı aktarılan verileri hello verileri dışarı aktarma işlemi ya da hello mysqldump komutu geri yükleyin. 
1. Hello proje klasörünü veya kendi içinde bulunan SQL dosyasını seçin, hello şema tooimport içine seçin ya da seçin **yeni** toodefine yeni bir şema. 
2. Tıklatın **Başlat alma** toobegin hello içeri aktarma işlemi.

## <a name="next-steps"></a>Sonraki adımlar
Başka bir geçiş yaklaşım okuma [dökümü ve geri yükleme, Azure veritabanı'nda MySQL için MySQL veritabanı kullanarak geçiş](concepts-migrate-dump-restore.md). 
