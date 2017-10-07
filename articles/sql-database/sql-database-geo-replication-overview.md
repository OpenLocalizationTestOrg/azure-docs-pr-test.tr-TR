---
title: "aaaFailover grupları ve etkin coğrafi çoğaltma - Azure SQL veritabanı | Microsoft Docs"
description: "Aktif coğrafi çoğaltma otomatik yük devretme gruplarıyla toosetup 4 çoğaltmalarını veritabanınızın herhangi bir hello Azure veri merkezleri ve kesinti hello olayı içinde autoomatically yük devretme sağlar."
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 2a29f657-82fb-4283-9a83-e14a144bfd93
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 07/10/2017
ms.author: sashan
ms.openlocfilehash: 7a39af8505624c0f19c5abccff051af836b1f9bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-failover-groups-and-active-geo-replication"></a>Genel Bakış: Yük devretme grupları ve etkin coğrafi çoğaltma
Aktif coğrafi çoğaltma toofour okunabilir ikincil veritabanlarını hello içinde tooconfigure sağlar aynı veya farklı veri merkezi konumlarını (bölge). İkincil veritabanları, yük devretme hello durumda bir veri merkezi kesintisi veya hello bağlanamama tooconnect toohello birincil veritabanının ve sorgulama için kullanılabilir. Merhaba yük devretme hello kullanıcı hello uygulama tarafından el ile başlatılması gerekir. Yük devretme sonrasında hello yeni birincil farklı bağlantı uç noktası vardır. 

> [!NOTE]
> Aktif coğrafi çoğaltma, tüm hizmet katmanlarında tüm bölgelerde tüm veritabanları için kullanılabilir.
>  

Azure SQL veritabanı otomatik yük devretme grupları (Önizleme-) olan bir SQL veritabanı tasarlanmış özelliği tooautomatically coğrafi çoğaltma ilişkisi, bağlantı ve yük devretme ölçekte yönetme. Bununla, hello müşteriler kazanç hello özelliği tooautomatically kurtarmak hello ikincil bölge içinde birden çok ilişkili veritabanlarını geri dönülemez bölgesel arızalara veya SQL veritabanı hizmetinin tam veya kısmi hello kaybına neden diğer planlanmamış olayları sonra Merhaba birincil bölge'de kullanılabilirliği. Ayrıca, bunlar Merhaba, okunabilir ikincil veritabanları toooffload salt okunur iş yükleri kullanabilirsiniz.  Otomatik Yük devretme grupları birden çok veritabanı içerdiğinden hello birincil sunucuda yapılandırılmalıdır. Birincil ve ikincil sunucular hello olmalıdır aynı abonelik. Otomatik Yük devretme grupları tüm veritabanlarının çoğaltma hello Grup tooonly bir ikincil sunucu farklı bir bölgede destekler. Tüm bölgelerdeki too4 ikinciller yukarı etkin coğrafi çoğaltma, otomatik yük devretme grupları olmadan sağlar.

Aktif coğrafi çoğaltma kullanıyorsanız ve nedeni, birincil veritabanı başarısız veya yalnızca çevrimdışına gereksinimlerini toobe yük devretme tooany ikincil veritabanlarınızın başlatabilirsiniz. Yük devretme hello ikincil veritabanları etkinleştirilmiş tooone olduğunda, diğer tüm ikinciller otomatik olarak bağlantılı toohello olan yeni birincil. Otomatik Yük devretme kullanıyorsanız (Önizleme-) toomanage veritabanını kurtarma ve bir veya birkaç hello grubu otomatik yük devretme sonuçlarında hello veritabanlarında etkiler herhangi kesinti gruplandırır. Uygulamanızın gereksinimlerine en iyi karşılayan hello otomatik yük devretme İlkesi yapılandırabilir veya devre dışı bırakmak ve el ile etkinleştirme kullanın. Ayrıca, otomatik yük devretme grupları (Önizleme-) okuma-yazma sağlayın ve yük devretme işlemleri sırasında kalır salt okunur dinleyicisi uç noktalarının değişmedi. El ile veya otomatik yük devretme etkinleştirme kullanıp, yük devretme tüm ikincil veritabanları hello Grup tooprimary geçer. Merhaba veritabanı yük devretme tamamlandıktan sonra hello DNS kaydı otomatik olarak güncelleştirilen tooredirect hello uç noktalarının toohello yeni bölgedir.

Çoğaltma ve tek bir veritabanının yük devretmesi veya bir sunucuya veya aktif coğrafi çoğaltma kullanarak esnek havuzdaki veritabanları kümesi yönetebilirsiniz. Bu kullanarak yapabilirsiniz hello [Azure portal](sql-database-geo-replication-portal.md), [PowerShell](sql-database-geo-replication-powershell.md), [Transact-SQL](sql-database-geo-replication-transact-sql.md), veya hello [REST API](https://msdn.microsoft.com/library/azure/mt163685.aspx). Yük devretme sonrasında hello yeni birincil sunucu ve veritabanı hello kimlik doğrulama gereksinimleri yapılandırılmış emin olun. Ayrıntılar için bkz [olağanüstü durum kurtarma işleminden sonra SQL veritabanı güvenlik](sql-database-geo-replication-security-config.md). Bu, her iki tooactive coğrafi çoğaltma ve otomatik yük devretme grupları (Önizleme-) uygulanır.

Aktif coğrafi çoğaltma yararlanır hello [her zaman açık](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) SQL Server tooasynchronously teknolojisini çoğaltmak Okunmuş kaydedilen anlık görüntü yalıtım (RCSI) kullanarak hello birincil veritabanı tooa ikincil veritabanı üzerinde yürütülen işlemler. Otomatik Yük devretme grupları aktif coğrafi çoğaltma, ancak aynı zaman uyumsuz çoğaltma mekanizması kullanılan hello üstünde hello Grup semantiği sağlar. Herhangi bir noktada belirtilen sırada, hello ikincil veritabanı hello birincil veritabanı biraz olabilir, hello ikincil veri garanti toonever kısmi işlemler vardır. Çapraz bölge artıklık uygulamaları tooquickly bozulmayı kalıcı kaybı veri merkezinin tamamı veya doğal afetler, geri dönülemez insan hataları veya kötü amaçlı davranışlara neden bir veri merkezinde bölümlerini etkinleştirir. Merhaba belirli RPO veri bulunabilir [iş sürekliliği genel bakış](sql-database-business-continuity.md).

Merhaba aşağıdaki şekilde bir örneği aktif coğrafi çoğaltma yapılandırılmış ile Merhaba bölgede Kuzey Orta ABD birincil ve ikincil hello Orta Güney ABD bölgesinde gösterilmektedir.

![coğrafi çoğaltma ilişkisi](./media/sql-database-active-geo-replication/geo-replication-relationship.png)

Merhaba ikincil veritabanlarıyla okunabilir olduğundan, bunlar raporlama işleri gibi kullanılan toooffload salt okunur iş yükleri olabilir. Aktif coğrafi çoğaltma kullanıyorsanız, olası toocreate hello ikincil veritabanı olan hello hello birincil, ancak aynı bölgede hello uygulamanın esnekliği toocatastrophic hatalarını artmaz. Otomatik Yük devretme grupları (Önizleme-) kullanıyorsanız, ikincil veritabanınıza her zaman farklı bir bölgede oluşturulur.

Ayrıca toodisaster kurtarma etkin coğrafi çoğaltma senaryoları aşağıdaki hello kullanılabilir:

* **Veritabanı geçiş**: en düşük kapalı kalma süresi ile aktif coğrafi çoğaltma toomigrate çevrimiçi bir sunucu tooanother veritabanından kullanabilirsiniz.
* **Uygulama yükseltme**: uygulama yükseltmeler sırasında başarısız geri kopya olarak fazladan bir ikincil oluşturabilirsiniz.

veri merkezleri arasında veritabanı artıklığı ekleme tooachieve gerçek iş sürekliliği hello çözüm yalnızca bir parçası olur. Yıkıcı bir hatadan kurtarma hello hizmeti oluşturan tüm bileşenleri ve bağımlı hizmetlerin gerektirir sonra bir uygulama (hizmeti) uçtan uca kurtarma. Bu bileşenlerin örnekleri hello istemci yazılımı (örneğin, bir tarayıcı özel bir JavaScript ile), web ön uçları, depolama ve DNS içerir. Tüm bileşenleri dayanıklı toohello aynı hatalarıdır ve hello kurtarma süresi hedefi, uygulamanızın içinde (RTO) kullanılabilir hale kritik öneme sahiptir. Bu nedenle, tüm bağımlı hizmetlerin tooidentify gerekir ve hello garanti ve sağladıkları yetenekleri anladığınızdan emin olun. Ardından, bağımlı olduğu hello Hizmetleri yük devretmesi sırasında hizmetinizin hello yeterli adımları tooensure almanız gerekir. Olağanüstü durum kurtarma çözümleri tasarlama hakkında daha fazla bilgi için bkz: [olağanüstü durum kurtarma'yı kullanarak etkin coğrafi çoğaltma için bulut çözümleri tasarlama](sql-database-designing-cloud-solutions-for-disaster-recovery.md).

## <a name="active-geo-replication-capabilities"></a>Aktif coğrafi çoğaltma özellikleri
Merhaba aktif coğrafi çoğaltma özelliği temel özelliklerini aşağıdaki hello sağlar:
* **Otomatik olarak zaman uyumsuz çoğaltma**: tooan varolan veritabanı ekleyerek yalnızca ikincil bir veritabanı oluşturabilirsiniz. Merhaba ikincil herhangi bir Azure SQL veritabanı sunucusu oluşturulabilir. Bir kez oluşturduktan sonra hello ikincil veritabanı hello birincil veritabanından kopyalanan hello verilerle doldurulur. Bu işlem, dengeli olarak bilinir. İkincil veritabanı oluşturulan ve dağıtılan sonra toohello birincil veritabanı olan zaman uyumsuz olarak güncelleştirmeleri toohello ikincil veritabanı otomatik olarak çoğaltılıyor. Zaman uyumsuz çoğaltma çoğaltılmış toohello ikincil veritabanı önce işlemleri hello birincil veritabanında yapıldığından anlamına gelir. 
* **Okunabilir ikincil veritabanları**: bir uygulama kullanarak salt okunur işlemler hello aynı veya farklı güvenlik sorumluları kullanılan hello birincil veritabanına erişmek için ikincil bir veritabanı erişebilirsiniz. Merhaba ikincil veritabanlarıyla çalışır anlık görüntü yalıtımı modu tooensure çoğaltma (günlük yeniden yürütme) hello güncelleştirmelerinin hello birincil, ikincil hello sorgular tarafından Gecikmeli değil.

   > [!NOTE]
   > Merhaba hello ikincil veritabanında bir şema kilidi iste birincil gelen aldığından emin şema güncelleştirmeleri varsa hello günlük yeniden yürütme hello ikincil veritabanı üzerinde ertelendi. 
   > 

* **Birden çok okunabilir ikinciller**: iki veya daha fazla ikincil veritabanları artırmak artıklık ve hello birincil veritabanı ve uygulama için bir koruma düzeyi. Birden fazla ikincil veritabanı yoksa, hello ikincil veritabanlarından birini başarısız olsa bile Merhaba uygulaması korumalı olarak kalır. Yalnızca bir ikincil veritabanı yoktur ve bu başarısız olursa, Merhaba uygulaması sunulan yeni bir ikincil veritabanı oluşturulana kadar toohigher risk.

   > [!NOTE]
   > Aktif coğrafi çoğaltma toobuild genel olarak dağıtılmış bir uygulamayı kullanıyorsanız ve 4'ten fazla bölgelerdeki toodata tooprovide salt okunur erişim varsa, ikincil (zincirleme olarak bilinen işlem), ikincil oluşturabilirsiniz. Bu şekilde veritabanı çoğaltma neredeyse sınırsız ölçeği elde edebilirsiniz. Ayrıca, zincirleme hello birincil veritabanı çoğaltmasını hello ek yükünü azaltır. Merhaba dengelemeyi hello artan çoğaltma gecikmesi hello yaprak çoğu ikincil veritabanlarında ' dir. . 
   >

* **Esnek havuz veritabanlarının Destek**: aktif coğrafi çoğaltma, herhangi bir esnek havuzdaki herhangi bir veritabanı için yapılandırılabilir. Merhaba ikincil veritabanını başka bir esnek havuzda olabilir. Normal veritabanları için hello ikincil bir esnek havuz olmalı ve bunun tersi de aynı hello hello hizmet katmanları olduğu sürece. 
* **Merhaba ikincil veritabanının yapılandırılabilir performans düzeyini**: ikincil bir veritabanı hello daha düşük performans düzeyine sahip birincil oluşturulabilir. Birincil ve ikincil veritabanları gerekli toohave hello aynı hizmet katmanı. Bir yük devretme sonrasında önemli veri kaybı hello Hello artan çoğaltma gecikmesi artırır çünkü bu seçenek yüksek veritabanı yazma etkinliği ile uygulamalar için önerilmez. Merhaba kadar Yeni Yük devretme hello uygulamanızın performansı etkilenir sonra ek olarak, birincil yükseltilmiş tooa daha yüksek performans düzeyi. Merhaba günlük GÇ yüzdesi grafik Azure Portal'daki sağlar en iyi yolu tooestimate hello en az düzeyde performans gerekli toosustain hello çoğaltma yükü hello ikincil düzeyini. Örneğin, birincil veritabanı P6 ise (1000 DTU) ve kendi günlük GÇ yüzde %50 hello ikincil gereken toobe en az P4 (500 DTU). Merhaba günlük GÇ kullanarak verileri de alabilirsiniz [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) veya [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) veritabanı görünümleri.  Merhaba SQL veritabanı performans düzeyleri hakkında daha fazla bilgi için bkz: [SQL Database seçenekleri ve performansı](sql-database-service-tiers.md). 
* **Kullanıcı tarafından denetlenen yük devretme ve yeniden çalışma**: ikincil bir veritabanı açıkça hello uygulama veya hello kullanıcı tarafından herhangi bir zamanda anahtarlı toohello birincil rolü olabilir. Gerçek kesinti hello sırasında "planlanmamış" seçeneği, hangi hemen ikincil toobe hello birincil yükseltir kullanılmalıdır. Merhaba başarısız birincil kurtarır ve kullanılabilir olduğunda yeniden hello sistem otomatik olarak işaretleri hello ikincil olarak birincil kurtarıldı ve hello yeni birincil ile güncel duruma getirmek. Merhaba en son değişiklikleri toohello ikincil çoğaltılmadan önce birincil başarısız olursa toohello zaman uyumsuz yapısı çoğaltma, çok küçük miktarda veri planlanmamış yük devretme işlemleri sırasında kaybolur. Birden fazla ikincil kopya ile birincil devrettiğinde hello sistem hello çoğaltma ilişkileri otomatik olarak yeniden yapılandırır ve kullanıcı müdahalesi gerektirmeden birincil ikinciller toohello yeni kalan bağlantılar hello yükseltilmiş. Merhaba yük devretme neden hello kesinti azaltıldığından sonra arzu tooreturn hello uygulama toohello birincil bölge olabilir. Merhaba yük devri komutu ile Merhaba çağrılır, toodo "seçeneği planlanan". 
* **Kimlik bilgileri ve güvenlik duvarı kuralları eşitlenmiş şekilde kalmasının**: kullanmanızı öneririz [veritabanı güvenlik duvarı kuralları](sql-database-firewall-configure.md) veritabanları için coğrafi olarak çoğaltılmış hello veritabanı tooensure ile bu kuralları çoğaltılabilir tüm ikincil veritabanlarına sahip, bu nedenle Merhaba birincil olarak aynı güvenlik duvarı kuralları hello. Bu yaklaşım toomanually hem hello birincil ve ikincil veritabanlarını barındıran sunucular üzerinde güvenlik duvarı kuralları yapılandırıp müşteriler hello gereksinimini ortadan kaldırır. Benzer şekilde, kullanarak [bulunan veritabanı kullanıcıları](sql-database-manage-logins.md) birincil ve ikincil veritabanları her zaman aynı kullanıcı kimlik bilgileri bir yük devretme sırasında; böylece herhangi kesinti hello sahip erişim verilerini sağlar oturumları ile son toomismatches ve parolalar. Merhaba eklenmesi ile [Azure Active Directory](../active-directory/active-directory-whatis.md), müşteriler, kullanıcı, erişim tooboth birincil ve ikincil veritabanları yönetebilir ve hello ortadan gereken kimlik bilgilerini veritabanlarında tamamen yönetmek için.

## <a name="auto-failover-group-capabilities"></a>Otomatik Yük devretme grubu özellikleri

Otomatik Yük devretme grupları özelliği, grup düzeyinde çoğaltma ve otomatik yük devretme destekleyerek aktif coğrafi çoğaltma, güçlü bir Özet sağlar. Ayrıca, hello ek dinleyicisi uç noktalarının sağlayarak yük devretme sonrasında hello gerekliliğini toochange hello SQL bağlantı dizesi kaldırır. 

* **Yük devretme grubu**: farklı bölgelerde (birincil ve ikincil sunucular) iki sunucu arasında bir veya daha çok yük devretme grupları oluşturulabilir. Her grup tüm veya bazı birincil veritabanı hello birincil bölgede tooan kesilmesi nedeniyle kullanılamaz hale durumunda, bir birim olarak kurtarılan bir veya daha çok veritabanı içerebilir.  
* **Birincil sunucu**: hello yük devretme grubundaki hello birincil veritabanı barındıran bir sunucu.
* **İkincil sunucu**: hello yük devretme grubundaki hello ikincil veritabanı barındıran bir sunucu. Merhaba ikincil sunucu hello olamaz hello birincil sunucu ile aynı bölgeye.
* **Ekleme veritabanları toofailover grubu**: bir sunucu içindeki birden fazla veritabanı put veya hello aynı içinde bir esnek havuz yük devretme grubu. Bir tek başına veritabanı toohello grubu eklerseniz, ikincil bir veritabanı otomatik olarak oluşturur kullanarak hello aynı sürüme ve performans düzeyi. Merhaba birincil veritabanını bir esnek havuz ise, hello ikincil otomatik olarak hello esnek havuzda hello ile aynı oluşturulan adı. İkincil bir veritabanı hello ikincil sunucuya zaten bir veritabanı eklerseniz, bu coğrafi çoğaltma hello grubu tarafından devralınır.

   > [!NOTE]
   > İkincil bir veritabanı hello yük devretme grubunun parçası olmayan bir sunucu zaten bir veritabanı eklerken, yeni ikincil hello ikincil sunucuya oluşturulur. 
   >

* **Yük devretme grubu okuma-yazma dinleyicisi**: DNS CNAME kaydı biçimlendirilmiş olarak  **&lt;yük devretme grup adı&gt;. database.windows.net** toohello geçerli birincil sunucu URL noktaları. Okuma-yazma SQL uygulamaların hello sağlayan tootransparently hello birincil yük devretme sonrasında değiştiğinde toohello birincil veritabanı yeniden bağlanın. 
* **Yük devretme grubu salt okunur dinleyicisi**: DNS CNAME kaydı biçimlendirilmiş olarak  **&lt;yük devretme grup adı&gt;. secondary.database.windows.net** toohello ikincil sunucu URL'SİNİN işaret. Tootransparently bağlanmak salt okunur SQL uygulamaların hello sağlayan hello kullanarak toohello ikincil veritabanını belirtilen yük dengeleyici kuralları. İsteğe bağlı olarak, salt okunur hello istiyorsanız hello ikincil sunucu kullanılamadığında trafiği toobe otomatik olarak toohello birincil sunucu yeniden yönlendirilmiş belirtebilirsiniz.
* **Otomatik Yük devretme İlkesi**: varsayılan olarak, hello yük devretme grubu otomatik yük devretme İlkesi ile yapılandırılır. Merhaba hatası algılandı hemen hello sistem yük devretmeyi tetikler. Merhaba uygulaması toocontrol hello yük devretme iş akışını istiyorsanız, devre dışı otomatik yük devretme kapatabilirsiniz. 
* **El ile yük devretme**: yük devretme el ile Merhaba otomatik yük devretme yapılandırması bağımsız olarak herhangi bir zamanda başlatabilirsiniz. Otomatik Yük devretme İlkesi yapılandırılmış el ile yük devretme değilse hello yük devretme grubundaki gerekli toorecover veritabanlarının olur. (İle tam veri eşitlemesi) zorlanmış veya kolay yük devretme işlemi başlatabilirsiniz. Merhaba ikinci kullanılan toorelocate hello active server toohello birincil bölge olabilir. Yük devretme tamamlandığında hello DNS kayıtları otomatik olarak güncelleştirilen tooensure bağlantı toohello doğru sunucuyu belirtir.
* **Veri kaybı yetkisiz kullanım süresi**: hello birincil ve ikincil veritabanları kullanarak eşitlenmiş olduğundan zaman uyumsuz çoğaltma hello yük devretme veri kaybına neden. Uygulamanızın dayanıklılık toodata kaybı hello otomatik yük devretme İlkesi tooreflect özelleştirebilirsiniz. Yapılandırarak **GracePeriodWithDataLossHours**, hello sistem büyük olasılıkla tooresult veri kaybı hello yük devretmeyi başlatmadan önce bekleyeceği süreyi kontrol edebilirsiniz. 

   > [!NOTE]
   > Sistem algıladığında hello grubundaki hello veritabanlarının hala çevrimiçi olduğu (örneğin, hello kesinti yalnızca hello hizmet denetim düzlemi etkilenebilir) hello değer bağımsız olarak tam veri eşitlemesi (kolay yük devretme) ile Merhaba yük devretme hemen etkinleştirir tarafından belirlenen **GracePeriodWithDataLossHours**. Bu davranış hello Kurtarma sırasında veri kaybı olmasını sağlar. yalnızca kolay bir yük devretme olası olmadığında hello yetkisiz kullanım süresi etkinleşir. Merhaba yetkisiz kullanım süresi dolmadan hello kesinti azaltılan, hello yük devretme etkinleştirilmedi.
   >

* **Birden çok yük devretme grubu**: hello için birden çok yük devretme grupları yapılandırabilirsiniz sunucuları toocontrol hello yerine ölçeğini aynı çifti. Her grubu üzerinden bağımsız olarak başarısız olur. Çok kiracılı uygulamanızı esnek havuzlar kullanıyorsa, bu yetenek toomix birincil ve ikincil veritabanları her havuzda kullanabilirsiniz. Bu şekilde bir kesinti tooonly hello etkisini hello kiracılar yarısı azaltabilir.

## <a name="best-practices-of-building-highly-available-service"></a>Yüksek oranda kullanılabilir hizmet oluşturmanın en iyi uygulamalar

Azure SQL veritabanı hello müşteriler kullanan yüksek oranda kullanılabilir bir hizmet toobuild şu yönergeleri izlemelidir:
- **Yük devretme grup**: farklı bölgelerde (birincil ve ikincil sunucular) iki sunucu arasında bir veya daha çok yük devretme grupları oluşturulabilir. Her grup tüm veya bazı birincil veritabanı hello birincil bölgede tooan kesilmesi nedeniyle kullanılamaz hale durumunda, bir birim olarak kurtarılan bir veya daha çok veritabanı içerebilir. Merhaba yük devretme grubu ikincil coğrafi çoğaltmalı veritabanı ile aynı olarak birincil hello hedefi hizmet hello oluşturur. Aynı hizmet düzeyi hedefi olarak hello ile yapılandırılmış bir varolan coğrafi çoğaltma ilişkisi toohello yük devretme grubu yapma emin hello coğrafi-ikincil eklerseniz, birincil hello.
- **OLTP iş yükü için okuma-yazma dinleyici kullanın**: OLTP işlemleri kullanım gerçekleştirirken  **&lt;yük devretme grup adı&gt;. database.windows.net** hello sunucusu URL'si ve hello bağlantılar olarak otomatik olarak yönlendirilmiş toohello birincil. Bu URL hello yük devretme sonrasında değiştirmez.  
Not hello yük devretme hello istemci bağlantılarını yeniden yönlendirilen toohello hello istemci sonra yalnızca birincil DNS Önbellek yenileninceye yeni olması için DNS kaydı hello güncelleştirilmesini gerektirir.
- **Salt okunur iş yükü için salt okunur bir dinleyici kullanın**: dayanıklı toocertain eskime durumu verilerinin olduğu mantıksal olarak yalıtılmış bir salt okunur yükünü varsa hello ikincil veritabanı hello uygulamada kullanabilirsiniz. Salt okunur oturumları kullanmak için  **&lt;yük devretme grup adı&gt;. secondary.database.windows.net** otomatik olarak yönlendirilmiş toohello ikincil hello sunucusu URL'si ve hello bağlantı olarak. Bağlantı dizesinde amacı kullanarak okunur belirtmek ayrıca önerilir **ApplicationIntent ReadOnly =**. 
- **Performans düşüşünü için hazır**: SQL yük devretme karardır hello geri kalanından Merhaba uygulaması ya da kullanılan diğer hizmetlerin bağımsız. Merhaba uygulaması "tek bir bölge ve bazı durumlarda başka bazı bileşenleri ile karışık". tooavoid hello Bozulması hello gereksiz uygulama dağıtımı hello DR bölgede emin olun ve bu makalede hello yönergeleri izleyin.  
Not Merhaba uygulaması hello DR bölgede toouse farklı bir bağlantı dizesi yok.  
- **Veri kaybı hazırlama**: kesinti algılanırsa, sıfır veri kaybı toohello bizim bilgisi en iyi SQL otomatik olarak okuma-yazma yük devretmeyi tetikler. Aksi halde, belirtilen tarafından hello süresi için bekler **GracePeriodWithDataLossHours**. Belirttiyseniz **GracePeriodWithDataLossHours**, veri kaybı hazırlıklı. Genel olarak, kesintiler sırasında Azure kullanılabilirlik korur. Veri kaybını göze alamayacağınız emin tooset olun **GracePeriodWithDataLossHours** 24 saat gibi tooa yeterli büyüklükte numarası. 


## <a name="upgrading-or-downgrading-a-primary-database"></a>Yükseltme veya bir birincil veritabanı önceki sürüme indirme
Yükseltme veya bir birincil veritabanı tooa farklı performans düzeyini düşürmek (Merhaba içinde aynı hizmet katmanını) olmadan tüm ikincil veritabanları bağlantısı kesiliyor. Yükseltme yaparken, hello ikincil veritabanı yükseltmeniz ve ardından hello birincil yükseltmeniz önerilir. Önceki sürüme indirme zaman hello tersine: hello birincil ilk düşürmek ve hello ikincil düşürmek. Bu öneri, yükseltme veya hello veritabanı tooa farklı hizmet katmanı düşürmek uygulanır. 

> [!NOTE]
> Merhaba yük devretme grubu yapılandırmasının bir parçası ikincil veritabanı oluşturduysanız şu önerilen toodowngrade hello ikincil veritabanı değil. Bu tooensure olan yük devretme etkinleştirildikten sonra veri katmanı normal iş yükünüzün yeterli kapasitesi tooprocess sahiptir. 
>

## <a name="preventing-hello-loss-of-critical-data"></a>Merhaba kritik verilerin kaybını önleme
Sürekli kopyalama toohello yüksek gecikme geniş ağlar, bir zaman uyumsuz çoğaltma mekanizması kullanır. Zaman uyumsuz çoğaltma bir hata oluşursa bazı veri kaybı kaçınılmaz hale getirir. Ancak, bazı uygulamalar, veri kaybı gerektirebilir. tooprotect Bu kritik güncelleştirmeler, uygulama geliştiricisi hello çağırabilir [sp_wait_for_database_copy_sync](https://msdn.microsoft.com/library/dn467644.aspx) hello işlemi sonlandırdı hemen sonra sistem yordamı. Çağırma **sp_wait_for_database_copy_sync** hello son kaydedilmiş işlemi kadar iş parçacığı çağırma blokları hello aktarılan toohello ikincil veritabanı. Ancak, yeniden ve ikincil hello kaydedilen aktarılan hello işlemleri toobe için beklemez. **sp_wait_for_database_copy_sync** kapsamlı tooa belirli sürekli kopyalama bağlantıdır. Merhaba bağlantı hakları toohello birincil veritabanı ile herhangi bir kullanıcı, bu yordamı çağırabilirsiniz.

> [!NOTE]
> **sp_wait_for_database_copy_sync** veri kaybı yük devretme sonrasında engeller, ancak okuma erişimi için tam eşitleme garanti değil. Merhaba gecikme nedeniyle bir **sp_wait_for_database_copy_sync** yordam çağrısı önemli olabilir ve hello çağrısı hello aynı anda hello hello işlem günlüğü boyutuna bağlıdır. 
> 

## <a name="programmatically-managing-failover-groups-and-active-geo-replication"></a>Yük devretme grupları ve etkin coğrafi çoğaltma programlı olarak yönetme
Otomatik Yük devretme grupları (Önizleme-) ve etkin daha önce açıklandığı gibi coğrafi çoğaltma program aracılığıyla Azure PowerShell kullanılarak da yönetilebilir ve REST API hello. Merhaba tabloları aşağıdaki komutlar kullanılabilir hello kümesi açıklanmaktadır.

**Azure Resource Manager API ve rol tabanlı güvenlik**: aktif coğrafi çoğaltma içeren bir dizi Azure Resource Manager API'leri hello dahil olmak üzere Yönetim için [Azure SQL Database REST API'sini](https://docs.microsoft.com/rest/api/sql/) ve [Azure PowerShell cmdlet'leri](https://docs.microsoft.com/powershell/azure/overview). Bu API'ları kaynak grupları hello kullanılmasını gerektirir ve rol tabanlı güvenlik (RBAC) desteği. Nasıl tooimplement erişim rolleri ile ilgili daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-what-is.md).

> [!NOTE]
> Aktif coğrafi çoğaltma pek çok yeni özelliği kullanarak yalnızca desteklenen [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) göre [Azure SQL REST API](https://msdn.microsoft.com/library/azure/mt163571.aspx) ve [Azure SQL Database PowerShell cmdlet'leri](https://msdn.microsoft.com/library/azure/mt574084.aspx). Merhaba [(Klasik) REST API](https://msdn.microsoft.com/library/azure/dn505719.aspx) ve [Azure SQL Database (Klasik) cmdlet'leri](https://msdn.microsoft.com/library/azure/dn546723.aspx) bunu Azure Resource Manager tabanlı API'ler önerilir hello kullanarak geriye dönük uyumluluk için desteklenir. 
> 

## <a name="manage-sql-database-failover-using-using-transact-sql"></a>SQL veritabanı Transact-SQL kullanarak yük devretme kullanarak yönetme

| Komut | Açıklama |
| --- | --- |
| [ALTER DATABASE (Azure SQL veritabanı)](https://msdn.microsoft.com/library/mt574871.aspx) |İkincil üzerinde Sunucu Ekle bağımsız değişkeni toocreate ikincil bir veritabanı için varolan bir veritabanını kullanın ve veri çoğaltma başlatır |
| [ALTER DATABASE (Azure SQL veritabanı)](https://msdn.microsoft.com/library/mt574871.aspx) |Yük DEVRETME veya FORCE_FAILOVER_ALLOW_DATA_LOSS tooswitch ikincil veritabanı toobe birincil tooinitiate yük devretme kullanın |
| [ALTER DATABASE (Azure SQL veritabanı)](https://msdn.microsoft.com/library/mt574871.aspx) |İkincil üzerinde SUNUCUSUNU Kaldır tooterminate bir SQL veritabanı ve hello belirtilen ikincil veritabanı arasında veri kopyalama kullanın. |
| [sys.geo_replication_links (Azure SQL veritabanı)](https://msdn.microsoft.com/library/mt575501.aspx) |Hello Azure SQL Database mantıksal sunucusu üzerindeki her veritabanı için tüm yineleme bağlantıları hakkında bilgi döndürür. |
| [sys.dm_geo_replication_link_status (Azure SQL veritabanı)](https://msdn.microsoft.com/library/mt575504.aspx) |Son çoğaltma saati, son çoğaltma gecikmesi ve hello çoğaltma bağlantısı belirli bir SQL veritabanı için ilgili diğer bilgileri alır hello. |
| [sys.dm_operation_status (Azure SQL veritabanı)](https://msdn.microsoft.com/library/dn270022.aspx) |Merhaba hello çoğaltma bağlantılarının durumunu da dahil olmak üzere tüm veritabanı işlemleri için Hello durumunu gösterir. |
| [sp_wait_for_database_copy_sync (Azure SQL veritabanı)](https://msdn.microsoft.com/library/dn467644.aspx) |tüm kaydedilmiş işlemleri çoğaltılır ve hello etkin ikincil veritabanı tarafından onaylanan kadar hello uygulama toowait neden olur. |
|  | |

## <a name="manage-sql-database-failover-using-using-powershell"></a>SQL veritabanı yük devretme PowerShell kullanarak yönetme

| Cmdlet | Açıklama |
| --- | --- |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase) |Bir veya daha fazla veritabanı alır. |
| [AzureRmSqlDatabaseSecondary yeni](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary) |Var olan bir veritabanı için ikincil bir veritabanı oluşturur ve veri çoğaltma başlatır. |
| [Set-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary) |Bir ikincil veritabanı toobe birincil tooinitiate yük devretme geçer. |
| [Remove-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) |Bir SQL veritabanı ve hello belirtilen ikincil veritabanı arasında veri kopyalama sonlandırır. |
| [Get-AzureRmSqlDatabaseReplicationLink](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) |Bir Azure SQL Database ve bir kaynak grubu veya SQL Server arasındaki Hello coğrafi Çoğaltma bağlantılarını alır. |
| [AzureRmSqlDatabaseFailoverGroup yeni](/powershell/module/azurerm.sql/set-azurermsqldatabasefailovergroup) |   Bu komut, bir yük devretme grubu oluşturur ve birincil ve ikincil sunucularda kaydeder|
| [Remove-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/remove-azurermsqldatabasefailovergroup) | Merhaba yük devretme grubu hello sunucusundan kaldırır ve tüm ikincil veritabanları dahil hello grubunu siler |
| [Get-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/get-azurermsqldatabasefailovergroup) | Merhaba yük devretme grubu yapılandırmasını alır. |
| [Set-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/set-azurermsqldatabasefailovergroup) |   Merhaba yük devretme grubunun Hello yapılandırmasını değiştirir |
| [Anahtar AzureRMSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/switch-azurermsqldatabasefailovergroup) | Merhaba yük devretme grubu toohello ikincil sunucu Tetikleyicileri yük devretme |
|  | |

> [!IMPORTANT]
> Örnek komut dosyaları için bkz: [Yapılandır ve yük devretme aktif coğrafi çoğaltma kullanarak tek bir veritabanı](scripts/sql-database-setup-geodr-and-failover-database-powershell.md), [Yapılandır ve yük devretme aktif coğrafi çoğaltma kullanarak havuza alınmış bir veritabanı](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md), ve [Yapılandır ve yük devretme bir tek veritabanı (Önizleme) için yük devretme grubu] (komut dosyaları/sql-database-setup-geodr-failover-database-failover-group-powershell.md.
>

## <a name="manage-sql-database-failover-using-hello-rest-api"></a>SQL veritabanı yük devretme Hello REST API kullanarak yönetme
| API | Açıklama |
| --- | --- |
| [Oluşturma veya güncelleştirme veritabanı (createMode = geri yükle)](/rest/api/sql/Databases/CreateOrUpdate) |Oluşturur, güncelleştirir veya bir birincil veya ikincil bir veritabanını geri yükler. |
| [Get oluştur veya veritabanı durumunu güncelleştir](/rest/api/sql/Databases/CreateOrUpdate) |Oluşturma işlemi sırasında hello durumu döndürür. |
| [İkincil veritabanının birincil (Planlı yük devretme) olarak ayarlayın](https://docs.microsoft.com/rest/api/sql/replicationlinkss#ReplicationLinks_Failover) |Hangi veritabanı çoğaltmasını birincil yapabilmesini hello geçerli birincil çoğaltma veritabanından göre ayarlar. |
| [İkincil veritabanının birincil (planlanmamış yük devretme) olarak ayarlayın](https://docs.microsoft.com/rest/api/sql/replicationlinks#ReplicationLinks_FailoverAllowDataLoss) |Hangi veritabanı çoğaltmasını birincil yapabilmesini hello geçerli birincil çoğaltma veritabanından göre ayarlar. Bu işlem, veri kaybına neden olabilir. |
| [Çoğaltma bağlantısı Al](/rest/api/sql/replicationlinks/get) |Belirli çoğaltma bağlantısı belirli bir SQL veritabanında bir coğrafi çoğaltma ortaklığı alır. Merhaba sys.geo_replication_links katalog görünümünde görülebilir hello bilgi alır. |
| [Çoğaltma bağlantılarını - veritabanı göre listesi](/rest/api/sql/replicationlinks/listbydatabase) | Coğrafi çoğaltma ortaklığı belirli bir SQL veritabanında tüm çoğaltma bağlantılarını alır. Merhaba sys.geo_replication_links katalog görünümünde görülebilir hello bilgi alır. |
| [Çoğaltma bağlantısı Sil](/rest/api/sql/databases/delete) | Bir veritabanı yinelemesi siler. Yük devretme sırasında yapılamaz. |
| [Oluşturma veya güncelleştirme yük devretme grubu] / rest/api/sql/failovergroups/createorupdate) | Oluşturur veya bir yük devretme grubu güncelleştirir |
| [Yük devretme grubu Sil](/rest/api/sql/failovergroups/delete) | Merhaba yük devretme grubu hello sunucusundan kaldırır |
| [Yük devretme (planlanmış)](/rest/api/sql/failovergroups/failover) | Merhaba geçerli birincil sunucu toothis sunucudan yöneltilir. |
| [Zorla yük devretme veri kaybı izin ver](/rest/api/sql/failovergroups/forcefailoverallowdataloss) |üzerinden hello geçerli birincil sunucu toothis sunucusundan ails. Bu işlem, veri kaybına neden olabilir. |
| [Get yük devretme grubu](/rest/api/sql/failovergroups/get) | Bir yük devretme grubunu alır. |
| [Sunucu tarafından listesi yük devretme grupları](/rest/api/sql/failovergroups/listbyserver) | Sunucu Hello yük devretme grupları listeler. |
| [Yük devretme grubu güncelleştir](/rest/api/sql/failovergroups/update) | Bir yük devretme grubu güncelleştirir. |
|  | |

## <a name="next-steps"></a>Sonraki adımlar
* Örnek komut dosyaları için bkz:
   - [Yapılandırma ve yük devretme aktif coğrafi çoğaltma kullanarak tek bir veritabanı](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
   - [Yapılandırma ve yük devretme aktif coğrafi çoğaltma kullanarak havuza alınmış bir veritabanı](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md)
   - [Yapılandırma ve yük devretme yük devretme bir grup için tek bir veritabanına (Önizleme)](scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md)
* İş sürekliliğine genel bakış ve senaryolar için bkz: [iş sürekliliğine genel bakış](sql-database-business-continuity.md)
* Azure SQL veritabanı otomatik yedeklemeler hakkında toolearn bkz [SQL veritabanı yedeklemeleri otomatik](sql-database-automated-backups.md).
* Kurtarma için otomatik yedeklemeler kullanma hakkında toolearn bkz [bir veritabanını hello hizmeti tarafından başlatılan yedeklerden geri](sql-database-recovery-using-backups.md).
* Yeni birincil sunucu ve veritabanı için kimlik doğrulama gereksinimleri hakkında toolearn bkz [olağanüstü durum kurtarma işleminden sonra SQL veritabanı güvenlik](sql-database-geo-replication-security-config.md).

