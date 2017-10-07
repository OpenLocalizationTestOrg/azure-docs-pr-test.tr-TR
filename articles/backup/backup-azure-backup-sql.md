---
title: "DPM kullanarak SQL Server iş yükleri için yedekleme aaaAzure | Microsoft Docs"
description: "Bir giriş toobacking hello Azure Yedekleme hizmetini kullanarak SQL Server veritabanlarını"
services: backup
documentationcenter: 
author: adigan
manager: Nkolli
editor: 
ms.assetid: 59df5bec-d959-457d-8731-7b20f7f1013e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adigan;giridham;jimpark;markgal;trinadhk
ms.openlocfilehash: ba78dbf1c7934a259a7bd0bdb7d4467ac75d05a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-sql-server-tooazure-as-a-dpm-workload"></a>SQL Server tooAzure DPM iş yükü yedekleyin
Bu makalede hello yapılandırma adımları Azure Yedekleme'yi kullanarak SQL Server veritabanlarının yedekleme için size yol gösterir.

SQL Server veritabanları tooAzure yukarı tooback, bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).

SQL Server veritabanı yedekleme tooAzure ve Azure kurtarma Hello Yönetimi üç adımdan oluşur:

1. Bir yedekleme İlkesi tooprotect SQL Server veritabanları tooAzure oluşturun.
2. İsteğe bağlı yedek kopyaları tooAzure oluşturun.
3. Merhaba veritabanını Azure'dan kurtarma.

## <a name="before-you-start"></a>Başlamadan önce
Başlamadan önce tüm hello olun [Önkoşullar](backup-azure-dpm-introduction.md#prerequisites) tooprotect iş yükleri için Microsoft Azure Yedekleme kullanılarak karşılandığından. Kapak görevler gibi Hello Önkoşullar: Azure Yedekleme aracısı ve hello kasası ile kaydediliyor hello sunucu hello kasa kimlik bilgilerini yükleme, indirme bir yedekleme kasası oluşturma.

## <a name="create-a-backup-policy-tooprotect-sql-server-databases-tooazure"></a>Bir yedekleme İlkesi tooprotect SQL Server veritabanları tooAzure oluşturma
1. Merhaba DPM sunucusunda hello tıklatın **koruma** çalışma.
2. Merhaba araç şeridinde tıklatın **yeni** toocreate yeni bir koruma grubu.

    ![Koruma grubu oluşturma](./media/backup-azure-backup-sql/protection-group.png)
3. DPM gösterir hello Başlangıç ekranına hello yönlendirme ile oluşturma ile ilgili bir **koruma grubu**. **İleri**’ye tıklayın.
4. Seçin **sunucuları**.

    ![Koruma grubu türü - 'Sunucuları' seçin](./media/backup-azure-backup-sql/pg-servers.png)
5. Yedeklenen hello veritabanları toobe nerede bulunduğunu hello SQL Server makinesinde genişletin. DPM, o sunucudan yedeklenebilir çeşitli veri kaynakları gösterir. Merhaba genişletin **tüm SQL paylaşımları** seçin (Bu durumda biz seçili ReportServer$ MSDPM2012 ve ReportServer$ MSDPM2012TempDB) hello veritabanları toobe yedeklendi. **İleri**’ye tıklayın.

    ![SQL DB seçin](./media/backup-azure-backup-sql/pg-databases.png)
6. Merhaba koruma grubu için bir ad ve seçin hello **çevrimiçi koruma istiyorum** onay kutusu.

    ![Veri koruma yöntemini - kısa süreli disk ve çevrimiçi Azure](./media/backup-azure-backup-sql/pg-name.png)
7. Merhaba, **kısa vadeli hedefleri belirtin** ekranında, hello gerekli girişleri toocreate yedekleme noktaları toodisk içerir.

    Burada, gösteriliyor **bekletme aralığı** çok ayarlanır*5 gün*, **eşitleme sıklığı** tooonce ayarlamak her *15 dakika* hello olduğu Yedekleme yapılmadı sıklığı. **Hızlı tam yedekleme** çok ayarlanır*fiyatlara*.

    ![Kısa vadeli hedefleri](./media/backup-azure-backup-sql/pg-shortterm.png)

   > [!NOTE]
   > 8: (toohello ekran giriş göre) 00'da hello değiştirilmiş hello veri aktarılarak bir yedekleme noktasının her gün oluşturulan önceki günün 8:00 PM yedekleme noktası. Bu işlem çağrılırken **hızlı tam yedekleme**. Merhaba işlem günlüklerini eşitlenirken 15 varsa bir gereksinim toorecover hello veritabanı 9: 00'da – hello gelen hello günlüklerini tekrarlamak tarafından oluşturulan başlangıç noktası sonra dakikada en son tam yedekleme noktası (Bu durumda 8 pm) hızlı.
   >
   >

8. **İleri**’ye tıklayın

    DPM gösterir, genel depolama alanı kullanılabilir ve hello olası disk alanı kullanımı hello.

    ![Disk ayırma](./media/backup-azure-backup-sql/pg-storage.png)

    Varsayılan olarak, DPM hello ilk yedek kopya için kullanılan veri kaynağı (SQL Server veritabanı) başına tek bir birim oluşturur. Bu yaklaşımı kullanarak, hello Mantıksal Disk Yöneticisi (LDM) DPM koruma too300 veri kaynakları (SQL Server veritabanları) sınırlar. select hello bu sınırlamaya geçici toowork **DPM depolama Havuzu'ndaki verileri birlikte bulundur**, seçeneği. Bu seçeneği kullanırsanız, DPM tek bir birimde birden çok veri kaynakları için DPM tooprotect too2000 SQL veritabanlarını sağlayan kullanır.

    Varsa **hello birimleri otomatik olarak büyütün** seçeneği seçildiğinde, DPM hello üretim verileri büyüdükçe artan hello yedekleme birimi için hesap. Varsa **hello birimleri otomatik olarak büyütün** seçeneği seçili değilse, DPM hello kullanılan yedekleme depolama toohello veri kaynakları hello koruma grubundaki sınırlar.
9. Yöneticiler bu ilk yedekleme el ile (Kapalı ağ) tooavoid bant genişliği tıkanıklık aktarılması veya hello ağ üzerinden hello seçeneği sunulur. Bunlar ilk aktarım sırasında hangi hello oluşabilir hello zaman da yapılandırabilirsiniz. **İleri**’ye tıklayın.

    ![İlk çoğaltma yöntemi](./media/backup-azure-backup-sql/pg-manual.png)

    Merhaba ilk yedek kopyayı hello tüm veri kaynağı (SQL Server veritabanı) aktarımını üretim sunucusu (SQL Server makinesinde) toohello DPM sunucusundan gerektirir. Bu veri büyük olabilir ve bant genişliği hello ağ üzerinden dosya aktarımı hello veri aşabilir. Bu nedenle, yöneticiler tootransfer hello ilk yedeklemeyi seçebilirsiniz: **el ile** (çıkarılabilir medya kullanarak) tooavoid bant genişliği tıkanıklık veya **hello ağ üzerinden otomatik olarak** (sırasında belirtilen saat).

    Hello ilk Yedekleme tamamlandıktan sonra hello rest hello yedeklerini hello ilk yedek kopyayı artımlı yedeklemelerin şunlardır. Artımlı yedeklemeler toobe küçük eğilimindedir ve hello ağ üzerinden kolayca aktarılır.
10. Merhaba tutarlılık denetimi toorun istediğiniz zaman'ı seçip tıklatın **sonraki**.

    ![Tutarlılık denetimi](./media/backup-azure-backup-sql/pg-consistent.png)

    DPM, bir tutarlılık denetimi toocheck hello bütünlüğü hello yedekleme noktası gerçekleştirebilirsiniz. Merhaba sağlama toplamı, DPM, bu dosya için hello yedekleme dosyasının hello üretim sunucusunda (SQL Server makinesinde bu senaryoda) ve hello yedeklenmiş verileri hesaplar. Bir çakışma Hello durumda o hello varsayılır DPM, yedeklenen dosyası bozuk. DPM, toohello sağlama toplamı eşleşmezliği karşılık gelen hello blokları göndererek hello yedeklenmiş verileri rectifies. Hello tutarlılık denetimi performansı yoğun bir işlem olduğundan, yöneticilerin hello tutarlılık denetimi zamanlaması veya otomatik olarak çalıştırarak hello seçeneğiniz vardır.
11. hello veri kaynaklarının çevrimiçi korumasını toospecify, select hello veritabanları toobe korumalı tıklayın ve tooAzure **sonraki**.

    ![Veri kaynakları seçin](./media/backup-azure-backup-sql/pg-sqldatabases.png)
12. Yöneticiler, yedekleme zamanlamaları ve kuruluşun ilkelerini uygun bekletme ilkeleri seçebilirsiniz.

    ![Zamanlama ve bekletme](./media/backup-azure-backup-sql/pg-schedule.png)

    Bu örnekte, yedeklemeleri günde bir kez 12: 00'dan ve 8 PM (Merhaba ekranın alt bölümünün) alınır

    > [!NOTE]
    > İyi bir uygulama toohave olan Hızlı Kurtarma için diskteki birkaç kısa vadeli kurtarma noktaları. Bu kurtarma noktaları "işletimsel kurtarma için" kullanılır. Azure yüksek SLA ile iyi site dışı konumu olarak hizmet verir ve kullanılabilirliğini garanti.
    >
    >

    **En iyi uygulaması**: DPM kullanarak yerel disk yedeklemeler hello tamamlandıktan sonra zamanlanmış Azure yedeklemeler emin olun. Bu hello en son disk kopyalanan yedekleme toobe tooAzure sağlar.

13. Merhaba bekletme ilkesi zamanlamayı seçin. Merhaba bekletme ilkesi nasıl çalıştığı hakkında hello bilgi sırasında sağlanan [Azure Yedekleme'yi tooreplace bant altyapısı Makalenizi](backup-azure-backup-cloud-as-tape.md).

    ![Bekletme İlkesi](./media/backup-azure-backup-sql/pg-retentionschedule.png)

    Bu örnekte:

    * Yedekleme günde bir kez 12: 00'dan ve 8 PM (Merhaba ekranın alt bölümünün) alınır ve 180 gün için korunur.
    * 12: 00'da Cumartesi Hello yedekleme 104 hafta boyunca tutulur
    * Son 12: 00'da Cumartesi Hello yedekleme 60 ay korunur
    * Son Cumartesi 12: 00'da Mart Hello yedekleme 10 yılı aşkın korunur
14. Tıklatın **sonraki** ve hello hello ilk yedek kopyayı tooAzure aktarmak için uygun seçeneği seçin. Seçebileceğiniz **hello ağ üzerinden otomatik olarak** veya **Çevrimdışı Yedekleme**.

    * **Merhaba ağ üzerinden otomatik olarak** aktarımları hello yedekleme verilerini tooAzure yedekleme için seçilen hello zamanlama göredir.
    * Nasıl **Çevrimdışı Yedekleme** works açıklanmıştır adresindeki [Çevrimdışı Yedekleme iş akışı Azure Yedekleme'de](backup-azure-backup-import-export.md).

    Merhaba ilgili aktarım mekanizması toosend hello ilk yedek kopyayı tooAzure tıklatın seçip **sonraki**.
15. Merhaba hello ilkesi ayrıntıları gözden geçirin sonra **Özet** ekranında, üzerinde hello tıklatın **Grup Oluştur** düğmesini toocomplete hello iş akışı. Merhaba tıklayabilirsiniz **Kapat** izleme çalışma alanı düğmesi ve İzleyicisi Merhaba işi sürüyor.

    ![Devam eden için koruma grubu oluşturma](./media/backup-azure-backup-sql/pg-summary.png)

## <a name="on-demand-backup-of-a-sql-server-database"></a>İsteğe bağlı bir SQL Server veritabanının yedeğini
Bir yedekleme İlkesi Hello önceki adımları oluşturulmuş olsa da, bir "kurtarma noktası" yalnızca hello ilk yedekleme gerçekleştiğinde oluşturulur. Merhaba Zamanlayıcı tookick için beklemek yerine, bir kurtarma tetikleyici hello oluşturulmasını hello adımları el ile gelin.

1. Merhaba koruma grubu durumunu görüntüleyene kadar bekleyin **Tamam** hello kurtarma noktası oluşturmadan önce hello veritabanı için.

    ![Koruma grubu üyeleri](./media/backup-azure-backup-sql/sqlbackup-recoverypoint.png)
2. Merhaba veritabanını sağ tıklatın ve seçin **kurtarma noktası oluştur**.

    ![Çevrimiçi kurtarma noktası oluştur](./media/backup-azure-backup-sql/sqlbackup-createrp.png)
3. Seçin **çevrimiçi koruma** hello açılan menüsüne ve ardından içinde **Tamam**. Bu, Azure'da hello bir kurtarma noktası oluşturma başlatır.

    ![Kurtarma noktası oluştur](./media/backup-azure-backup-sql/sqlbackup-azure.png)
4. Hello hello iş ilerleme durumunu görüntüleyebilirsiniz **izleme** burada bulabilirsiniz etmekte olan bir çalışma alanında bir hello sonraki çizimde gösterilen hello gibi iş.

    ![İzleme konsolu](./media/backup-azure-backup-sql/sqlbackup-monitoring.png)

## <a name="recover-a-sql-server-database-from-azure"></a>SQL Server veritabanını Azure'dan kurtarma
Merhaba aşağıdaki gerekli toorecover (SQL Server veritabanı) azure'dan bir Korunan varlık adımlardır.

1. Merhaba DPM sunucusu Yönetim Konsolu'nu açın. Çok gidin**kurtarma** burada görebilirsiniz hello sunucuları çalışma DPM tarafından yedeklenen. Merhaba gerekli veritabanında (Bu örnek ReportServer$ MSDPM2012) göz atın. Seçin bir **kurtarma** ile biten zaman **çevrimiçi**.

    ![Kurtarma noktası seçin](./media/backup-azure-backup-sql/sqlbackup-restorepoint.png)
2. Merhaba veritabanı adını sağ tıklatıp **kurtarmak**.

    ![Azure'dan kurtarma](./media/backup-azure-backup-sql/sqlbackup-recover.png)
3. DPM hello kurtarma noktası hello ayrıntılarını gösterir. **İleri**’ye tıklayın. toooverwrite hello veritabanı, select hello kurtarma türünü **SQL Server örneğine Kurtar toooriginal**. **İleri**’ye tıklayın.

    ![TooOriginal konum kurtarma](./media/backup-azure-backup-sql/sqlbackup-recoveroriginal.png)

    Bu örnekte, DPM hello veritabanı tooanother SQL Server örneği veya tooa tek başına ağ klasörüne kurtarma sağlar.
4. Merhaba, **belirtin Kurtarma Seçenekleri** ekran, ağ bant genişliği kullanımını kurtarma tarafından kullanılan toothrottle hello bant genişliği azaltma gibi hello kurtarma seçeneklerini seçebilirsiniz. **İleri**’ye tıklayın.
5. Merhaba, **Özet** ekran, o ana kadarki sağlanan tüm hello kurtarma yapılandırmaları bakın. Tıklatın **kurtarmak**.

    Kurtarılan hello veritabanı Hello kurtarma durumunu gösterir. Tıklayabilirsiniz **Kapat** tooclose hello Sihirbazı ve görünüm hello ediyor hello **izleme** çalışma.

    ![Kurtarma işlemini başlatın](./media/backup-azure-backup-sql/sqlbackup-recoverying.png)

    Merhaba Kurtarma tamamlandıktan sonra geri hello uygulama tutarlı veritabanıdır.

### <a name="next-steps"></a>Sonraki Adımlar:
• [Azure Backup ile ilgili SSS](backup-azure-backup-faq.md)
