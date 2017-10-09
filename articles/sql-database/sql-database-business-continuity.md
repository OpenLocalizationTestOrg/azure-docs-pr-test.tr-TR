---
title: "aaaCloud iş sürekliliği - veritabanı kurtarma - SQL veritabanı | Microsoft Docs"
description: "Azure SQL Veritabanı'nın bulutta iş sürekliliği ve veritabanı kurtarmanın yanı sıra görev açısından kritik bulut uygulamalarının kesintisiz çalışması için sunduğu destek özelliklerini öğrenin."
keywords: "iş sürekliliği, bulutta iş sürekliliği, veritabanı olağanüstü durum kurtarma, veritabanı kurtarma"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 18e5d3f1-bfe5-4089-b6fd-76988ab29822
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/15/2017
ms.author: sashan
ms.openlocfilehash: c9a6ff86fbbc04ce839a4fca79594b573b71644c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-business-continuity-with-azure-sql-database"></a>Azure SQL Veritabanı'nda iş sürekliliğine genel bakış

Bu genel bakışta, iş devamlılığı ve olağanüstü durum kurtarma için Azure SQL veritabanı sağlar hello özellikleri açıklanmaktadır. Seçenekler, öneriler ve veri kaybına neden ya da, veritabanı ve uygulama toobecome kullanılamaz neden kesintiye uğratan olaylarından kurtarmak için öğreticiler hakkında bilgi edinin. Bir kullanıcı veya uygulama hatası veri bütünlüğü etkiler, bir Azure bölgesinin bir kesinti veya bakım uygulamanızın gerektirdiği olmadığında hangi toodo öğrenin.

## <a name="sql-database-features-that-you-can-use-tooprovide-business-continuity"></a>Tooprovide iş sürekliliği kullanabileceğiniz SQL veritabanı özellikleri

SQL Veritabanı; otomatik yedekleme ve isteğe bağlı veritabanı çoğaltma gibi birçok iş sürekliliği özelliği sunar. Her özellik, tahmini kurtarma süresi (ERT) ve son işlemler için olası veri kaybı açısından farklı özelliklere sahiptir. Bu seçenekleri kavradıktan sonra aralarından birini seçebilir ve çoğu senaryoda farklı durumlar için birden fazlasını birlikte kullanabilirsiniz. İş sürekliliği planınızın geliştirdikçe Merhaba uygulaması hello kesintiye uğratan olayından sonra tam olarak kurtarır - Bu, Kurtarma süresi hedefi (RTO) önce toounderstand hello maksimum kabul edilebilir süresi gerekir. Ayrıca toounderstand ihtiyacınız hello en son veri güncelleştirmeleri (zaman aralığı) başlangıç uygulaması miktarını tolerans kaybetme hello kesintiye uğratan olayından sonra kurtarırken - Bu, kurtarma noktası hedefi (RPO).

Aşağıdaki tablo karşılaştırır hello Ekle ve RPO hello üç yaygın senaryolar için hello.

| Özellik | Temel katman | Standart katman | Premium katman |
| --- | --- | --- | --- |
| Yedekten belirli bir noktaya geri yükleme |7 gün içinde herhangi bir geri yükleme noktasına |35 gün içinde herhangi bir geri yükleme noktasına |35 gün içinde herhangi bir geri yükleme noktasına |
| Coğrafi olarak çoğaltılmış yedeklerden coğrafi geri yükleme |ERT < 12 sa., RPO < 1 sa |ERT < 12 sa., RPO < 1 sa |ERT < 12 sa., RPO < 1 sa |
| Azure Backup Vault'tan geri yükleme |ERT < 12 sa., RPO < 1 hft. |ERT < 12 sa., RPO < 1 hft. |ERT < 12 sa., RPO < 1 hft. |
| Aktif coğrafi çoğaltma |ERT < 30 sn., RPO < 5 sn. |ERT < 30 sn., RPO < 5 sn. |ERT < 30 sn., RPO < 5 sn. |

### <a name="use-database-backups-toorecover-a-database"></a>Veritabanı Yedeklemeleri toorecover bir veritabanını kullanın

SQL veritabanı otomatik olarak tam veritabanı yedeklemeleri haftalık bir birleşimini gerçekleştirir, artımlı veritabanı yedeklemeleri saatlik ve işlem her beş günlük yedeklemelerine-veri kaybı, işinizi tooprotect on dakika. Bu yedeklemeler hello standart ve Premium hizmet katmanları veritabanları için 35 gün ve 7 gündür hello temel hizmet katmanında veritabanları için coğrafi olarak yedekli depolama alanında depolanır. Daha fazla bilgi için bkz: [hizmet katmanları](sql-database-service-tiers.md). Merhaba saklama dönemi, hizmet katmanı için iş gereksinimlerinizi karşılamıyorsa hello saklama dönemi tarafından artırabilirsiniz [hello Hizmet katmanını değiştirmeyi](sql-database-service-tiers.md). Merhaba tam ve fark veritabanı yedeklerini de çoğaltılmış tooa olan [eşleştirilmiş veri merkezi](../best-practices-availability-paired-regions.md) veri merkezi kesintisinden karşı koruma için. Daha fazla bilgi için bkz: [otomatik veritabanı yedeklemeyi](sql-database-automated-backups.md).

Merhaba yerleşik saklama dönemi, uygulamanız için yeterli değilse, bir veritabanı uzun vadeli bekletme ilkesi yapılandırarak genişletebilirsiniz. Daha fazla bilgi için bkz: [uzun vadeli bekletme](sql-database-long-term-retention.md).

Bu otomatik veritabanı yedeklemeleri toorecover hem veri merkezi ve tooanother veri merkezi içinde olmak üzere çeşitli kesintiye uğratan olayları veritabanından kullanabilirsiniz. Merhaba kurtarma süresini hello hello aynı kurtarma veritabanı toplam sayısı dahil olmak üzere çeşitli etkenlere bağlıdır tahmini otomatik veritabanı yedeklemeyi kullanarak, aynı zaman, hello hello işlem günlüğü boyutu, veritabanı boyutu ve ağ bant genişliği hello bölge. Merhaba kurtarma süresi genellikle değerinden 12 saattir. Tooanother veri bölgesinin kurtarırken hello olası veri kaybı sınırlı too1 hello coğrafi olarak yedekli depolama saatlik artımlı veritabanı yedeklemelerini tarafından saattir.

> [!IMPORTANT]
> toorecover kullanarak otomatik yedeklemeler, hello SQL Server katkıda bulunan rolü veya hello abonelik sahibi bir üyesi olmalıdır - bkz [RBAC: yerleşik roller](../active-directory/role-based-access-built-in-roles.md). Hello Azure portal, PowerShell veya hello REST API kullanarak kurtarabilirsiniz. Transact-SQL kullanamazsınız.
>

Uygulamanız aşağıdaki koşullara uygunsa iş sürekliliği ve kurtarma hizmeti olarak otomatik yedeklemeyi kullanabilirsiniz:

* Görev açısından kritik değilse.
* Bir bağlama SLA - 24 saatlik bir kapalı kalma süresi yok veya daha uzun süre içinde finansal yükümlülük sonuçlanmaz.
* Veri değişikliği (düşük işlemler saatte) düşük oranını sahiptir ve tooan kaybetme değişikliği kabul edilebilir veri kaybı saattir.
* Maliyetler önemliyse.

Daha hızlı kurtarma gerekiyorsa kullanın [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md) (sonraki bölümde açıklanmaktadır). 35 gün sayısından önceki bir dönemden toobe mümkün toorecover veri gerekiyorsa kullanın [uzun vadeli yedekleme bekletme](sql-database-long-term-retention.md). 

### <a name="use-active-geo-replication-and-auto-failover-groups-in-preview-tooreduce-recovery-time-and-limit-data-loss-associated-with-a-recovery"></a>Kurtarma ile ilişkilendirilen etkin coğrafi çoğaltma ve otomatik yük devretme grupları (Önizleme-) tooreduce kurtarma süresi ve sınırı veri kaybı kullanın

Bir iş kesintisi oluşursa ayrıca toousing veritabanı yedeklemeleri için veritabanı kurtarma, kullanabileceğiniz [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md) tooconfigure veritabanı toohave toofour okunabilir ikincil veritabanlarını hello bölgelerde, bir seçimdir. Bu ikincil veritabanları bir zaman uyumsuz çoğaltma mekanizması kullanarak hello birincil veritabanı ile eşitlenmiş olarak tutulur. Bu özellik, veri merkezi kesintisinden oluşursa iş kesintisi karşı veya uygulama yükseltme sırasında kullanılan tooprotect olur. Aktif coğrafi çoğaltma kullanılan tooprovide daha iyi sorgu performansını salt okunur sorguları dağınık toogeographically kullanıcılar için de olabilir.

tooenable otomatik ve şeffaf yük devretme, coğrafi olarak çoğaltılmış veritabanlarına düzenlediğiniz gruplar hello kullanarak [otomatik yük devretme grubu](sql-database-geo-replication-overview.md) SQL veritabanı (Önizleme-) özelliğidir.

Merhaba birincil veritabanı gider çevrimdışı beklenmedik veya tootake ihtiyacınız varsa çevrimdışı bakım etkinlikleri için hızla (bir yük devretme olarak da bilinir) ikincil toobecome hello birincil yükseltmek ve uygulamaları tooconnect yükseltilmiş toohello birincil yapılandırın. Uygulamanızı toohello veritabanlarını hello yük devretme grubu dinleyicisi kullanarak bağlanırsa, yük devretme sonrasında toochange hello SQL bağlantı dizesi yapılandırma gerekmez. Planlı yük devretme sayesinde veri kaybı yaşanmaz. Planlanmamış yük devretme kümelemesiyle bazı miktarda zaman uyumsuz çoğaltma toohello yapısı nedeniyle çok yeni işlemler için veri kaybı olabilir. Otomatik Yük devretme gruplarını (Önizleme-) kullanarak hello yük devretme İlkesi toominimize hello olası veri kaybı özelleştirebilirsiniz. Bir yük devretme sonrasında daha sonra yeniden çalışma için - according tooa plan veya ne zaman hello veri merkezi yeniden çevrimiçi olur. Tüm durumlarda, kullanıcılar kısa bir kapalı kalma süresi deneyimi ve tooreconnect gerekir.

> [!IMPORTANT]
> toouse etkin coğrafi çoğaltma ve otomatik yük devretme gruplar (Önizleme-), gerekir ya da hello abonelik sahibi veya SQL Server yönetici izinlerine sahip olmalıdır. Yapılandırma ve hello Azure portal, PowerShell kullanarak üzerinden başarısız veya REST Azure abonelik izinleri veya SQL Server izinleriyle Transact-SQL kullanarak API hello.
> 

Uygulamanız bu ölçütler hiçbirini karşılıyorsa etkin coğrafi çoğaltma ve otomatik yük devretme gruplar (önizlemede) kullanın:

* Görev açısından kritikse.
* 24 saat veya üzeri kesinti süresine izin vermeyen hizmet düzeyi sözleşmesine (SLA) sahipse.
* Kapalı kalma süresi içinde finansal yükümlülük neden olabilir.
* Veri değişiklik oranı yüksekse ve bir saatlik değişiklik kaybı kabul edilebilir değilse.
* Aktif coğrafi çoğaltma ek maliyetini Hello hello olası finansal yükümlülük ve ilişkili iş kaybı düşüktür.

>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-protecting-important-DBs-from-regional-disasters-is-easy/player]
>

## <a name="recover-a-database-after-a-user-or-application-error"></a>Kullanıcı veya uygulama hatasından sonra bir veritabanını kurtarma
*Hiç kimse mükemmel değildir! Bir kullanıcı yanlışlıkla veri silebilir, istemeden önemli bir tabloyu ve hatta bir veritabanının tamamını bırakabilir. Veya, bir uygulamanın tooan uygulama hatası nedeniyle hatalı verilerle sağlam verilerin yanlışlıkla üzerine.

Bu senaryoda kullanabileceğiniz kurtarma seçenekleri aşağıda verilmiştir.

### <a name="perform-a-point-in-time-restore"></a>Belirli bir noktaya geri yükleme gerçekleştirme
Koşuluyla zaman hello veritabanı saklama dönemi içinde hello otomatik yedeklemeler toorecover iyi noktası, zaman içindeki bilinen, veritabanı tooa bir kopyasını kullanabilirsiniz. Merhaba veritabanı geri yüklendikten sonra hello özgün veritabanına geri hello veritabanıyla değiştirebilir veya gerekli hello veri hello özgün veritabanına geri hello veri kopyalamak. Aktif coğrafi çoğaltma Hello veritabanı kullanıyorsa, hello özgün veritabanına geri hello kopyadan gerekli hello veri kopyalama öneririz. Merhaba özgün veritabanına geri hello veritabanıyla değiştirirseniz, tooreconfigure gerekir ve etkin coğrafi (hangi büyük bir veritabanı için oldukça biraz zaman alabilir) çoğaltma yeniden eşitleyin.

Daha fazla bilgi ve zaman kullanarak bir veritabanı tooa noktasına geri yüklemek için ayrıntılı adımlar için Azure portal hello veya PowerShell kullanarak, bkz. [zaman içinde nokta geri yükleme](sql-database-recovery-using-backups.md#point-in-time-restore). Transact-SQL kullanarak kurtarma gerçekleştiremezsiniz.

### <a name="restore-a-deleted-database"></a>Silinen veritabanını geri yükleme
Merhaba veritabanı silinir, ancak hello mantıksal sunucu silinmez, hangi silindi silinmiş hello veritabanı toohello noktası geri yükleyebilirsiniz. Bu bir veritabanı yedekleme toohello geri yükler, silinmiş aynı mantıksal SQL sunucusu. Merhaba özgün adı kullanarak geri yükleyin veya yeni bir ad veya geri hello veritabanı sağlar.

Azure portal veya PowerShell kullanarak hello kullanarak silinen bir veritabanını geri yüklemek için ayrıntılı adımlar ve daha fazla bilgi için bkz: [silinen bir veritabanını geri](sql-database-recovery-using-backups.md#deleted-database-restore). Transact-SQL kullanarak geri yükleme gerçekleştiremezsiniz.

> [!IMPORTANT]
> Merhaba mantıksal sunucu silinmişse, silinen bir veritabanını kurtaramazsınız.
>
>

### <a name="restore-from-azure-backup-vault"></a>Azure Backup Vault'tan geri yükleme
Merhaba geçerli Bekletme dönemi otomatik yedeklemeler için dışında Hello veri kaybı oluştu ve veritabanınızı uzun vadeli bekletme için yapılandırılmışsa, Azure yedekleme kasası tooa yeni veritabanındaki haftalık bir yedekten geri yükleyebilirsiniz. Bu noktada, hello özgün veritabanına geri hello veritabanı ile değiştirin veya gerekli hello veri hello özgün veritabanına geri hello veritabanından kopyalayın. Tooretrieve veritabanı önceki tooa ana uygulama yükseltmenizin eski bir sürümüne ihtiyacınız varsa, denetçi veya yasal bir sipariş isteğinden hello Azure yedekleme kasası kaydedilmiş tam yedekleme kullanarak bir veritabanı oluşturabilirsiniz karşılamak.  Daha fazla bilgi için bkz. [Uzun süreli saklama](sql-database-long-term-retention.md).

## <a name="recover-a-database-tooanother-region-from-an-azure-regional-data-center-outage"></a>Bir veritabanı tooanother bölgesi bir Azure bölgesel veri merkezi kesintisinden kurtarma
<!-- Explain this scenario -->

Çok sık olmasa da Azure veri merkezlerinde kesintiler yaşanabilir. Kesinti yaşandığında yalnızca birkaç dakika sürebilecek veya saatler alacak bir hizmet kesintisi söz konusu olabilir.

* Merhaba veri merkezi kesintisinden üzerinden bir seçenek veritabanı toocome tekrar çevrimiçi toowait olur. Bu toohave hello veritabanını çevrimdışı destekleyebilir uygulamalar için çalışır. Örneğin, geliştirme projesi veya ücretsiz deneme sürümü, toowork üzerinde sürekli gerekmez. Bir veri merkezinde bir kesinti olduğunda, böylece veritabanınızı biraz gerekmiyorsa, bu seçenek yalnızca çalışır, ne kadar süreyle hello kesinti son, bilmezsiniz.
* Başka bir seçenek aktif coğrafi çoğaltma kullanıyorsanız veya hello coğrafi olarak yedekli veritabanı yedeklemeleri (coğrafi geri yükleme) kullanarak bir veritabanını kurtarmak tooanother veri bölgesinin tooeither başarısız olur. Veritabanı kurtarma yedeklerden saat sürer ancak yük devretme yalnızca birkaç saniye sürer.

Eylem alırken, toorecover ve ne kadar uygulamanızın bu iş sürekliliği özelliklerini toouse nasıl karar üzerine veri kaybı tabi bağlıdır süreyi. Aslında, toouse veritabanı yedeklemeleri ve etkin coğrafi uygulama gereksinimlerinize bağlı olarak çoğaltma bileşimini seçebilirsiniz. Bu iş sürekliliği özelliklerini kullanan bağımsız veritabanları ve elastik havuzlarla ilgili dikkate alınacak uygulama tasarımı noktaları hakkında ayrıntılı bilgi için bkz. [Bulutta olağanüstü durum kurtarma için uygulama tasarlama](sql-database-designing-cloud-solutions-for-disaster-recovery.md) ve [Elastik havuz olağanüstü durum kurtarma stratejileri](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).

Merhaba aşağıdaki bölümler hello adımları toorecover veritabanı yedeklemeleri ya da etkin coğrafi çoğaltma kullanarak genel bir bakış sağlar. Planlama gereksinimleri, post kurtarma adımları ve nasıl toosimulate bir kesinti tooperform bir olağanüstü durum kurtarma ayrıntıya hakkında bilgi de dahil olmak üzere ayrıntılı adımlar için bkz: [bir SQL veritabanı bir kesintisinden kurtarma](sql-database-disaster-recovery.md).

### <a name="prepare-for-an-outage"></a>Kesinti için hazırlanma
İş sürekliliği özelliği kullandığınız hello bağımsız olarak yapmanız gerekir:

* Tanımlamak ve hello hedef sunucu, sunucu düzeyinde güvenlik duvarı kuralları, oturumlar ve ana veritabanı düzeyinde izinler de dahil olmak üzere hazırlayın.
* Belirlemek nasıl tooredirect istemciler ve istemci uygulamaları toohello yeni sunucu
* Denetim ayarları ve uyarılar gibi diğer bağımlılık belgelerini oluşturmak

Ayrıca, düzgün şekilde, bir yük devretme veya bir veritabanı kurtarma ek süre gerçekleştirildikten sonra çevrimiçi ve büyük olasılıkla uygulamalarınızı getiren değil hazırlıyorsanız stres - bozuk birlikte aynı anda sorun giderme gerektirir.

### <a name="fail-over-tooa-geo-replicated-secondary-database"></a>Tooa coğrafi olarak çoğaltılmış ikincil veritabanı üzerinde başarısız
Aktif coğrafi çoğaltma ve otomatik yük devretme grupları (Önizleme-), kurtarma mekanizması olarak kullanıyorsanız, bir otomatik yük devretme İlkesi yapılandırmak veya kullanmak [el ile yük devretme](sql-database-disaster-recovery.md#fail-over-to-geo-replicated-secondary-database). Başlatılan sonra hello yük devretme nedenler hello ikincil toobecome yeni birincil ve hazır toorecord yeni işlemleri hello ve tooqueries - henüz çoğaltılmış hello verileri için en düşük düzeyde veri kaybı olan yanıt. Merhaba yük devretme işlemini tasarlama hakkında daha fazla bilgi için bkz: [bulut olağanüstü durum kurtarma için bir uygulama tasarlamanızı](sql-database-designing-cloud-solutions-for-disaster-recovery.md).

> [!NOTE]
> Merhaba veri merkezi tekrar çevrimiçi olduğunda hello eski ana otomatik olarak yeniden toohello yeni birincil ve ikincil veritabanlarıyla haline gelir. Toorelocate hello birincil geri toohello özgün bölge gerekiyorsa, planlanmış bir yük devretme el ile başlatabilir (yeniden çalışma). 
> 

### <a name="perform-a-geo-restore"></a>Bir coğrafi geri yükleme gerçekleştirin
Coğrafi olarak yedekli depolama çoğaltma ile otomatik yedeklemeler kullanıyorsanız, kurtarma mekanizması olarak [coğrafi geri yükleme kullanarak bir veritabanı kurtarma](sql-database-disaster-recovery.md#recover-using-geo-restore). Kurtarma genellikle 12 saat içinde gerçekleşir - hello zaman tarafından belirlenen tooone saat yukarı veri kaybı çekildiği ve çoğaltılmış saatlik değişiklik yedeklemesi son. Merhaba kurtarma tamamlanana kadar hello veritabanı oluşturulamıyor toorecord işlemler veya tooany sorguları yanıt. Bu sürede bir veritabanı toohello son kullanılabilir noktası geri yüklerken hello coğrafi ikincil tooany noktası sürede geri yükleme şu anda desteklenmiyor.

> [!NOTE]
> Uygulamanızı toohello kurtarılan veritabanının üzerine geçiş yapmadan önce hello veri merkezi tekrar çevrimiçi olursa hello kurtarma iptal edebilirsiniz.  
>
>

### <a name="perform-post-failover--recovery-tasks"></a>Yük devretme/kurtarma sonrası görevleri gerçekleştirme
Ya da kurtarma mekanizması kurtarıldıktan sonra kullanıcılar ve uygulamalar yedekleme önce ek görevleri aşağıdaki ve çalışan hello gerçekleştirmeniz gerekir:

* İstemcileri ve istemci uygulamaları toohello yeni sunucu ve geri yüklenen veritabanı yeniden yönlendirme
* Uygun sunucu düzeyinde güvenlik duvarı kuralları kullanıcılar tooconnect için yerinde olduğundan emin olun (veya [veritabanı düzeyi güvenlik duvarları](sql-database-firewall-configure.md#creating-and-managing-firewall-rules))
* Uygun giriş bilgilerinin ve ana veritabanı düzeyi izinlerin mevcut olduğunu doğrulama ([kapsanan kullanıcıları](https://msdn.microsoft.com/library/ff929188.aspx) da kullanabilirsiniz)
* Denetimi uygun şekilde yapılandırma
* Uyarıları uygun şekilde yapılandırma

## <a name="upgrade-an-application-with-minimal-downtime"></a>Bir uygulamayı en az kesinti süresiyle yükseltme
Bazen bir uygulama gibi bir uygulama yükseltme planlı bakım nedeniyle çevrimdışına alınmalıdır. [Uygulama yükseltmelerini yönetme](sql-database-manage-application-rolling-upgrade.md) çalışırken, bulut uygulaması toominimize kalma süresi sırasında yükseltme toouse aktif coğrafi çoğaltma tooenable yükseltme nasıl açıklar ve bir sorun yaşanırsa kurtarma yolu sağlar. 

## <a name="next-steps"></a>Sonraki adımlar
Bağımsız veritabanları ve elastik havuzlarla ilgili dikkate alınacak uygulama tasarımı noktaları hakkında ayrıntılı bilgi için bkz. [Bulutta olağanüstü durum kurtarma için uygulama tasarlama](sql-database-designing-cloud-solutions-for-disaster-recovery.md) ve [Elastik havuz olağanüstü durum kurtarma stratejileri](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
