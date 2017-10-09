---
title: "aaaSQL veritabanı olağanüstü durum kurtarma | Microsoft Docs"
description: "Toorecover bölgesel veri merkezi kesintisinden veya başarısızlık veritabanından nasıl hello Azure SQL veritabanı etkin coğrafi çoğaltma ve coğrafi geri yükleme özellikleri hakkında bilgi edinin."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 4800960e-3f9d-40ce-9e55-fb7f2784c067
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: sashan
ms.openlocfilehash: bae08485863067748107ec4808e52d8e88e2de0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-database-or-failover-tooa-secondary"></a>Bir Azure SQL Database veya yük devretme tooa ikincil geri yükleme
Azure SQL veritabanı bir kesintisinden kurtarma özellikleri aşağıdaki hello sunar:

* [Etkin coğrafi çoğaltma](sql-database-geo-replication-overview.md)
* [Coğrafi geri yükleme](sql-database-recovery-using-backups.md#point-in-time-restore)

toolearn iş sürekliliği senaryoları ve bu senaryolar destekleyen hello özellikler hakkında bkz [iş sürekliliği](sql-database-business-continuity.md).

### <a name="prepare-for-hello-event-of-an-outage"></a>Bir kesinti Hello olayı için hazırlama
Aktif coğrafi çoğaltma veya coğrafi olarak yedekli Yedekleme kullanarak kurtarma tooanother veri bölgesi ile başarı için tooprepare başka bir veri merkezi kesintisinden toobecome hello yeni birincil sunucu Server'da hello ortaya yanı sıra iyi tanımlanmış adımlara sahip ihtiyacınız belgelenmiş ve test edilmiş tooensure kesintisiz kurtarma. Hazırlık adımları içerir:

* Merhaba mantıksal sunucusu başka bir bölge toobecome hello yeni birincil sunucu olarak belirleyin. Etkin coğrafi çoğaltma ile bu en az bir ve belki de her hello ikincil sunucular olacaktır. Coğrafi geri yükleme için bu genellikle hello Server'da olacaktır [eşleştirilmiş bölge](../best-practices-availability-paired-regions.md) veritabanınızın bulunduğu hello bölge için.
* Belirleyin ve isteğe bağlı olarak tanımlamak, hello sunucu düzeyinde güvenlik duvarı kuralları üzerinde kullanıcılar için yeni bir birincil veritabanı tooaccess hello.
* Nasıl tooredirect kullanıcılar toohello yeni birincil sunucu, gibi bağlantı dizeleri değiştirme veya DNS girdilerini değiştirerek adımıdır belirler.
* Tanımlamak, isteğe bağlı olarak oluşturun, hello yeni birincil sunucu üzerindeki hello ana veritabanındaki mevcut olması ve varsa bu oturumlar hello ana veritabanında uygun izinlere sahip olmak oturumları hello. Daha fazla bilgi için bkz: [SQL veritabanı güvenlik olağanüstü durum kurtarma işleminden sonra](sql-database-geo-replication-security-config.md)
* Toobe güncelleştirilmiş toomap toohello yeni birincil veritabanı gerekir uyarı kuralları tanımlar.
* Belge hello denetim yapılandırmasına hello geçerli birincil veritabanı
* Gerçekleştirmek bir [olağanüstü durum kurtarma ayrıntıya](sql-database-disaster-recovery-drills.md). coğrafi geri yükleme, kesinti bir toosimulate silin veya hello kaynak veritabanı toocause uygulama bağlantı hatası yeniden adlandırın. toosimulate kesinti aktif coğrafi çoğaltma için başlangıç web uygulaması veya sanal makineye bağlı toohello veritabanı veya yük devretme, hello veritabanı, toocause uygulama, bağlantı hataları devre dışı bırakabilirsiniz.

## <a name="when-tooinitiate-recovery"></a>Zaman tooinitiate kurtarma
Merhaba kurtarma işlemi Merhaba uygulaması etkiler. Merhaba SQL bağlantı dizesi veya DNS kullanarak yeniden yönlendirme değiştirilmesi gerektirir ve kalıcı veri kaybına neden olabilir. Bu nedenle, yalnızca hello kesinti büyük olasılıkla toolast uygulamanızın kurtarma süresi hedefi uzun olduğunda yapılmalıdır. Merhaba uygulama dağıtılan tooproduction olduğunda normal hello uygulama sistem durumunu izleme gerçekleştirmek ve veri kurtarma hello noktaları tooassert garanti aşağıdaki hello kullanmanız gerekir:

1. Merhaba uygulama katmanı toohello veritabanından kalıcı bağlantı hatası.
2. Hello Azure portal geniş etkiyle hello bölgede bir olay hakkında bir uyarı gösterir.
3. Hello Azure SQL Database sunucusu düşürülmüş olarak işaretlenir.

Uygulama dayanıklılık toodowntime ve olası iş yükümlülük bağlı olarak kurtarma seçenekleri aşağıdaki hello düşünebilirsiniz.

Kullanım hello [alma kurtarılabilir veritabanı](https://msdn.microsoft.com/library/dn800985.aspx) (*LastAvailableBackupDate*) tooget hello son coğrafi olarak çoğaltılmış geri yükleme noktası.

## <a name="wait-for-service-recovery"></a>Servis kurtarma için bekleyin
hızlı bir şekilde mümkün olduğunca ancak hello kök nedeni bağlı olarak, saat veya gün sürebilir gibi hello Azure ekipleri titizlikle toorestore hizmet kullanılabilirliği çalışmaktadır.  Uygulamanızın önemli kapalı kalma süresi dayanabileceği varsa hello kurtarma toocomplete için basitçe bekleyebilirsiniz. Bu durumda, herhangi bir eyleminiz gereklidir. Merhaba geçerli hizmet durumu görebilirsiniz bizim [Azure hizmet sağlığı panosunu](https://azure.microsoft.com/status/). Merhaba bölge Hello kurtarma işleminden sonra uygulamanızın kullanılabilirlik geri yüklenir.

## <a name="fail-over-toogeo-replicated-secondary-database"></a>Toogeo olarak çoğaltılmış ikincil veritabanının üzerine başarısız
Uygulamanızın kapalı kalma iş yükümlülük neden olabilir, uygulamanızda coğrafi olarak çoğaltılmış veritabanları kullanıyor olması gerekir. Merhaba uygulaması tooquickly geri yükleme kullanılabilirlik bir kesinti durumunda farklı bir bölgede olanak sağlar. Nasıl çok öğrenin[coğrafi çoğaltma yapılandırma](sql-database-geo-replication-portal.md).

Merhaba toorestore kullanılabilirliğini database(s) tooinitiate hello desteklenen yöntemlerden birini kullanarak yük devretme toohello coğrafi olarak çoğaltılmış ikincil hello.

Kılavuzlar toofail tooa coğrafi olarak çoğaltılmış ikincil veritabanı üzerinde aşağıdaki hello birini kullanın:

* [Tooa coğrafi olarak çoğaltılmış ikincil Azure Portal kullanarak'üzerinde başarısız](sql-database-geo-replication-portal.md)
* [Yük devretme tooa coğrafi olarak çoğaltılmış ikincil PowerShell'i kullanma](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
* [Tooa coğrafi olarak çoğaltılmış ikincil T-SQL kullanarak'üzerinde başarısız](sql-database-geo-replication-transact-sql.md)

## <a name="recover-using-geo-restore"></a>Coğrafi geri yükleme kullanarak kurtarma
Uygulamanızın kapalı kalma süresi içinde iş yükümlülük sağlamazsa kullanabileceğiniz [coğrafi geri yükleme](sql-database-recovery-using-backups.md) yöntemi toorecover olarak uygulama veritabanları. En son coğrafi olarak yedekli yedeklemesinden hello veritabanının bir kopyasını oluşturur.

## <a name="configure-your-database-after-recovery"></a>Kurtarma işleminden sonra veritabanını Yapılandır
Coğrafi çoğaltma yük devretme veya coğrafi geri yükleme toorecover kesintiden kullanıyorsanız, hello bağlantı toohello yeni veritabanları doğru yapılandırılmış olduğunu hello normal uygulama işlevi devam ettirilebilir böylece emin olmanız gerekir. Bu hazır kurtarılan veritabanı üretim görevleri tooget listesi verilmektedir.

### <a name="update-connection-strings"></a>Bağlantı dizelerini güncelleştirmek
Kurtarılan veritabanı içinde farklı bir sunucuya yer alacağı için uygulamanızın bağlantı dizesi toopoint toothat sunucusu tooupdate gerekiyor.

Bağlantı dizeleri değiştirme hakkında daha fazla bilgi için bkz: hello uygun geliştirme dilini, [bağlantı kitaplığı](sql-database-libraries.md).

### <a name="configure-firewall-rules"></a>Güvenlik duvarı kurallarını yapılandırma
Merhaba güvenlik duvarı kuralları sunucusunda ve hello veritabanı eşleşme hello birincil sunucu hem de birincil veritabanı yapılandırılan o yapılandırılmış emin toomake gerekir. Daha fazla bilgi için bkz: [nasıl yapılır: Güvenlik Duvarı ayarlarını yapılandırma (Azure SQL veritabanı)](sql-database-configure-firewall-settings.md).

### <a name="configure-logins-and-database-users"></a>Oturum açma ve veritabanı kullanıcıları yapılandırın
Uygulamanız tarafından kullanılan tüm hello oturumları, kurtarılan veritabanı barındırma hello sunucusu üzerinde var olduğundan emin toomake gerekir. Daha fazla bilgi için bkz: [coğrafi çoğaltma için Güvenlik Yapılandırması](sql-database-geo-replication-security-config.md).

> [!NOTE]
> Yapılandırma ve sunucunun güvenlik duvarı kuralları, oturum açma bilgileri (ve onların izinlerini) bir olağanüstü durum kurtarma ayrıntıya sırasında test gerekir. Bu sunucu düzeyi nesneleri ve bunların yapılandırmalarını hello kesintisi sırasında kullanılamayabilir.
> 
> 

### <a name="setup-telemetry-alerts"></a>Kurulum telemetri uyarıları
Varolan uyarı kuralı ayarlarınızı güncelleştirilmiş toomap toohello kurtarılan veritabanı ve hello farklı sunucu olmasını toomake gerekir.

Veritabanı uyarı kuralları hakkında daha fazla bilgi için bkz: [uyarı bildirimleri alma](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) ve [izleme hizmeti durumu](../monitoring-and-diagnostics/insights-service-health.md).

### <a name="enable-auditing"></a>Denetimi etkinleştirme
Denetim varsa, veritabanınızı gerekli tooaccess olan tooenable ihtiyacınız hello veritabanı kurtarma işleminden sonra Denetim. Daha fazla bilgi için bkz: [veritabanı denetimi](sql-database-auditing.md).

## <a name="next-steps"></a>Sonraki adımlar
* Azure SQL veritabanı otomatik yedeklemeler hakkında toolearn bakın [SQL veritabanı otomatik yedeklemeler](sql-database-automated-backups.md)
* toolearn iş sürekliliği tasarım ve kurtarma senaryoları hakkında bkz [sürekliliği senaryoları](sql-database-business-continuity.md)
* Kurtarma için otomatik yedeklemeler kullanma hakkında toolearn bakın [bir veritabanı hello hizmeti tarafından başlatılan yedeklerden geri yükleme](sql-database-recovery-using-backups.md)

