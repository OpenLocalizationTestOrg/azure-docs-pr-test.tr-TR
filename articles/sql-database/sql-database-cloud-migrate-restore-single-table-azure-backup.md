---
title: "Azure SQL veritabanı yedeğinden tek bir tabloyu aaaRestore | Microsoft Docs"
description: "Nasıl toorestore tek bir tablo Azure SQL veritabanı yedeğinden öğrenin."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: 696d2ac87a70bccdf063bfecb8255723404aa5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a>Nasıl toorestore tek bir tablo bir Azure SQL veritabanı yedeğinden
İçinde yanlışlıkla bir SQL veritabanında bazı verileri değiştiren bir durum karşılaşabilirsiniz ve şimdi toorecover hello tek etkilenen tablo istiyorsunuz. Tek bir nasıl toorestore tablo hello SQL veritabanı birinden bir veritabanında bu makalede [otomatik yedeklemeler](sql-database-automated-backups.md).

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a>Hazırlık adımları: hello tablo yeniden adlandırın ve hello veritabanının bir kopyasını geri yükleme
1. Azure SQL veritabanınızı geri hello kopyayla tooreplace istediğiniz Hello tabloda tanımlayın. Microsoft SQL Management Studio'yu toorename hello tabloyu kullanın. Örneğin, hello tablo olarak yeniden adlandırın &lt;tablo adı&gt;_old.
   
   > [!NOTE]
   > engellenme, tooavoid adlandırdığınız hello tablo üzerinde çalışan herhangi bir etkinlik olduğundan emin olun. Sorunlarla karşılaşırsanız, bir bakım penceresi sırasında bu yordamı gerçekleştirmek emin olun.
   >

2. Veritabanı tooa noktasının toorecover toousing hello istediğiniz zaman bir yedeğini geri [noktası-In_Time geri](sql-database-recovery-using-backups.md#point-in-time-restore) adımları.
   
   > [!NOTE]
   > Merhaba geri hello veritabanının adını hello DBName + zaman damgası biçimde olacaktır; Örneğin, **Adventureworks2012_2016-01-01T22-12Z**. Bu adım hello varolan bir veritabanı adı hello sunucuda üzerine değildir. Bu bir güvenlik önlemi ve amaçlıdır tooallow, tooverify hello geri veritabanı önce geçerli kendi veritabanını bırakın ve üretim kullanımı için geri hello veritabanını yeniden adlandırın.
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a>Merhaba SQL veritabanı geçiş aracını kullanarak veritabanı hello kopyalama hello tablosundan geri

1. Merhaba yükleyip [SQL veritabanı Geçiş Sihirbazı'nı](https://sqlazuremw.codeplex.com).
2. Merhaba hello SQL veritabanı Geçiş Sihirbazı'nı Aç **seçin işlem** sayfasında, seçin **Çözümle/geçirme altında veritabanına**ve ardından **sonraki**.

   ![SQL veritabanı Geçiş Sihirbazı - işlemi seçin](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. Merhaba, **tooServer bağlanmak** iletişim kutusunda, ayarları aşağıdaki hello Uygula:

   * Sunucu adı: **bilgisayarınızı SQL server**
   * Kimlik doğrulaması: **SQL Server kimlik doğrulaması**
   * Oturum açma: **, oturum açma**
   * Parola: **parolanızı**
   * Veritabanı: **Master DB'de (tüm veritabanlarını listeler)**
   
   > [!NOTE]
   > Varsayılan olarak, oturum açma bilgilerinizi hello sihirbaz kaydeder. Kendisine istemiyorsanız belirleyin **unutursanız oturum açma bilgilerini**.
   >
   
     ![SQL veritabanı Geçiş Sihirbazı - Kaynak Seç - adım 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. Merhaba, **Kaynağı Seç** iletişim kutusu, geri select hello veritabanı hello adından **hazırlık adımları** bölümünde, kaynağı olarak ve ardından **sonraki**.
   
    ![SQL veritabanı Geçiş Sihirbazı - Kaynak Seç - adım 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. Merhaba, **seçin nesneleri** iletişim kutusu, select hello **belirli veritabanı nesneleri seçin** seçeneğini ve ardından hello table(or tables) toomigrate toohello hedef sunucu istediğinizi seçin.
   ![SQL veritabanı Geçiş Sihirbazı - nesneleri seçin](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)
6. Merhaba üzerinde **komut dosyası Sihirbazı Özet** sayfasında, **Evet** sorulduğunda hazır toogenerate bir SQL betiği olmanıza hakkında. Ayrıca, daha sonra kullanmak için hello seçeneği toosave hello TSQL komut dosyası vardır.
   ![SQL veritabanı Geçiş Sihirbazı - komut dosyası Sihirbazı Özeti](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)
7. Merhaba üzerinde **sonuç özeti** sayfasında, **sonraki**.
   ![SQL veritabanı Geçiş Sihirbazı - sonuç özeti](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)
8. Merhaba üzerinde **Kurulum hedef sunucu bağlantısı** sayfasında, **tooServer bağlanmak**ve ardından aşağıdaki gibi hello ayrıntıları girin:
   
   * **Sunucu adı**: hedef sunucu örneği
   * **Kimlik doğrulama**: **SQL Server kimlik doğrulaması**. Oturum açma kimlik bilgilerinizi girin.
   * **Veritabanı**: **Master DB'de (tüm veritabanları liste)**. Bu seçenek hello hedef sunucu üzerindeki tüm hello veritabanlarını listeler.
     
     ![SQL veritabanı Geçiş Sihirbazı - Kurulum hedef sunucu bağlantısı](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. Tıklatın **Bağlan**seçin toomove hello tabloya istediğiniz ve ardından hello hedef veritabanı **sonraki**. Bu daha önce oluşturulan hello betik çalıştıran tamamlanmalıdır ve hello yeni tablo kopyalanan toohello hedef veritabanının taşınır görmeniz gerekir.

## <a name="verification-step"></a>Doğrulama adımı

- Sorgu ve test hello yeni tablo toomake hello veri sağlam olduğundan emin kopyalanır. Onaylama sonra yeniden adlandırılmış hello tablo formuna düşürebilir **hazırlık adımları** bölümü. (örneğin, &lt;tablo adı&gt;_old).

## <a name="next-steps"></a>Sonraki adımlar
[SQL veritabanı otomatik yedekleme](sql-database-automated-backups.md)

