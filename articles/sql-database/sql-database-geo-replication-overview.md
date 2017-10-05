---
title: "Yük devretme grupları ve etkin coğrafi çoğaltma - Azure SQL veritabanı | Microsoft Docs"
description: "Aktif coğrafi çoğaltma otomatik yük devretme gruplarıyla veritabanınızın herhangi bir Azure veri merkezleri ile autoomatically yük devretme bir kesinti durumunda 4 çoğaltmaları Kurulum olanak sağlar."
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
ms.openlocfilehash: 9a2171f59c6192115dc1820e7f033fd783c9e077
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="overview-failover-groups-and-active-geo-replication"></a>Genel Bakış: Yük devretme grupları ve etkin coğrafi çoğaltma
Aktif coğrafi çoğaltma, en fazla dört okunabilir ikincil veritabanları aynı veya farklı bir veri merkezi konumlarını (bölge) yapılandırmanıza olanak sağlar. İkincil veritabanları, yük devretme veri merkezi kesintisinden veya birincil veritabanına bağlanamama söz konusu olduğunda ve sorgulama için kullanılabilir. Yük devretme kullanıcı uygulama tarafından el ile başlatılması gerekir. Yük devretme işleminden sonra yeni birincil farklı bağlantı uç noktası vardır. 

> [!NOTE]
> Aktif coğrafi çoğaltma, tüm hizmet katmanlarında tüm bölgelerde tüm veritabanları için kullanılabilir.
>  

Azure SQL veritabanı otomatik yük devretme grupları (Önizleme-) coğrafi çoğaltma ilişkisi, bağlantı ve yük devretme ölçekte otomatik olarak yönetmek üzere tasarlanmış bir özelliktir SQL veritabanı. Bununla, müşterilerin otomatik olarak geri dönülemez bölgesel arızalara veya SQL veritabanı hizmetinin kullanılabilirlik tam veya kısmi kaybına neden diğer planlanmamış olayları sonra ikincil bölge içinde birden çok ilişkili veritabanlarını kurtarma olanağı elde birincil bölge. Ayrıca, bunlar salt okunur iş yükleri boşaltmak için okunabilir ikincil veritabanları kullanabilirsiniz.  Otomatik Yük devretme grupları birden çok veritabanı içerdiğinden birincil sunucuda yapılandırılmalıdır. Birincil ve ikincil sunucular aynı abonelikte olması gerekir. Otomatik Yük devretme grupları için farklı bir bölgede yalnızca bir ikincil sunucu grubundaki tüm veritabanlarının çoğaltma destekler. Herhangi bir bölgede en fazla 4 ikincil etkin coğrafi çoğaltma, otomatik yük devretme grupları olmadan sağlar.

Aktif coğrafi çoğaltma kullanıyorsanız ve için birincil veritabanı başarısız olmasına neden veya çevrimdışı duruma gerekiyor, yük devretme ikincil veritabanlarınızı birini başlatabilirsiniz. Yük devretme ikincil veritabanlarıyla birine etkinleştirildiğinde, yeni birincil diğer tüm ikinciller otomatik olarak bağlanır. Otomatik Yük devretme grupları (Önizleme-) veritabanı kurtarma ve bir veya birkaç Grup sonuçları veritabanlarında etkiler herhangi kesinti yönetmek için otomatik yük devretme kümesinde kullanıyorsanız. Uygulamanızın gereksinimlerine en iyi karşılayan otomatik yük devretme İlkesi yapılandırabilir veya devre dışı bırakmak ve el ile etkinleştirme kullanın. Ayrıca, otomatik yük devretme grupları (Önizleme-) okuma-yazma sağlayın ve yük devretme işlemleri sırasında kalır salt okunur dinleyicisi uç noktalarının değişmedi. El ile veya otomatik yük devretme etkinleştirme kullanıp kullanmayacağınızı yük devretme için birincil gruptaki tüm ikincil veritabanları geçer. Veritabanı yük devretme tamamlandıktan sonra yeni bölge için uç noktalarının yönlendirmek için DNS kaydını otomatik olarak güncelleştirilir.

Çoğaltma ve tek bir veritabanının yük devretmesi veya bir sunucuya veya aktif coğrafi çoğaltma kullanarak esnek havuzdaki veritabanları kümesi yönetebilirsiniz. Bu kullanarak yapabilirsiniz [Azure portal](sql-database-geo-replication-portal.md), [PowerShell](sql-database-geo-replication-powershell.md), [Transact-SQL](sql-database-geo-replication-transact-sql.md), veya [REST API](https://msdn.microsoft.com/library/azure/mt163685.aspx). Yük devretme işleminden sonra yeni birincil sunucu ve veritabanı için kimlik doğrulama gereksinimlerini yapılandırılmış emin olun. Ayrıntılar için bkz [olağanüstü durum kurtarma işleminden sonra SQL veritabanı güvenlik](sql-database-geo-replication-security-config.md). Bu, hem etkin coğrafi çoğaltma ve otomatik yük devretme gruplar (Önizleme-) için geçerlidir.

Aktif coğrafi çoğaltma yararlanır [her zaman açık](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) teknolojisini kullanarak bir ikincil veritabanının birincil veritabanı üzerinde yürütülen işlemler zaman uyumsuz olarak çoğaltmak için SQL Server'ın kaydedilen anlık görüntü yalıtım (RCSI) okuyun. Otomatik Yük devretme grupları aktif coğrafi çoğaltma üstünde Grup semantiği sağlar ancak aynı zaman uyumsuz çoğaltma mekanizması kullanılır. Herhangi bir noktada verilen ederken, ikincil veritabanı biraz birincil veritabanı olabilir, ikincil veri hiçbir zaman kısmi hareket olması garanti edilmez. Çapraz bölge artıklık kalıcı kaybı veri merkezinin tamamı veya doğal afetler, geri dönülemez insan hataları veya kötü amaçlı davranışlara neden bir veri merkezinde bölümlerini hızla kurtarılır uygulamaları etkinleştirir. Belirli RPO verileri bulunabilir [iş sürekliliği genel bakış](sql-database-business-continuity.md).

Aşağıdaki şekilde Orta Güney ABD bölgesinde birincil bölgede Kuzey Orta ABD ile yapılandırılmış ve ikincil etkin coğrafi çoğaltma örneği gösterir.

![coğrafi çoğaltma ilişkisi](./media/sql-database-active-geo-replication/geo-replication-relationship.png)

İkincil veritabanlarıyla okunabilir olmadığından, raporlama işleri gibi salt okunur iş yükleri boşaltmak için kullanılabilir. Aktif coğrafi çoğaltma kullanıyorsanız, birincil ile aynı bölgede ikincil veritabanını oluşturmak mümkündür, ancak uygulamanın esnekliği yıkıcı hatalarına artırmaz. Otomatik Yük devretme grupları (Önizleme-) kullanıyorsanız, ikincil veritabanınıza her zaman farklı bir bölgede oluşturulur.

Ek olarak olağanüstü durum kurtarma etkin coğrafi çoğaltma aşağıdaki senaryolarda kullanılabilir:

* **Veritabanı geçiş**: aktif coğrafi çoğaltma veritabanını başka bir çevrimiçi en düşük kapalı kalma süresi ile bir sunucudan geçirmek için kullanabilirsiniz.
* **Uygulama yükseltme**: uygulama yükseltmeler sırasında başarısız geri kopya olarak fazladan bir ikincil oluşturabilirsiniz.

Gerçek iş sürekliliği elde etmek için veri merkezleri arasında veritabanı artıklığı ekleme yalnızca çözüm parçasıdır. Yıkıcı bir hatadan kurtarma hizmeti oluşturan tüm bileşenleri ve bağımlı hizmetlerin gerektirir sonra bir uygulama (hizmeti) uçtan uca kurtarma. İstemci yazılımı (örneğin, bir tarayıcı özel bir JavaScript ile), web ön uçları, depolama ve DNS bu bileşenlerin örneklerindendir. Tüm bileşenleri aynı hatalarına dayanıklı ve kurtarma süresi hedefi, uygulamanızın içinde (RTO) kullanılabilir hale kritik öneme sahiptir. Bu nedenle, tüm bağımlı hizmetlerin tanımlamak ve garanti ve sağladıkları yetenekleri anlamanız gerekir. Ardından, bağımlı olduğu hizmetlerin yük devretme sırasında hizmetinizin emin olmak için yeterli adımlar atmanız gerekir. Olağanüstü durum kurtarma çözümleri tasarlama hakkında daha fazla bilgi için bkz: [olağanüstü durum kurtarma'yı kullanarak etkin coğrafi çoğaltma için bulut çözümleri tasarlama](sql-database-designing-cloud-solutions-for-disaster-recovery.md).

## <a name="active-geo-replication-capabilities"></a>Aktif coğrafi çoğaltma özellikleri
Aktif coğrafi çoğaltma özelliği aşağıdaki temel yetenekleri sağlar:
* **Otomatik olarak zaman uyumsuz çoğaltma**: varolan bir veritabanına ekleyerek yalnızca ikincil bir veritabanı oluşturabilirsiniz. İkincil herhangi bir Azure SQL veritabanı sunucusu oluşturulabilir. Oluşturduktan sonra ikincil veritabanı birincil veritabanından kopyalanan verileri ile doldurulur. Bu işlem, dengeli olarak bilinir. İkincil veritabanı oluşturulan ve dağıtılan sonra birincil veritabanı güncelleştirmeleri zaman uyumsuz olarak ikincil veritabanını otomatik olarak çoğaltılır. Zaman uyumsuz çoğaltma ikincil veritabanına çoğaltılırken işlemleri birincil veritabanında yapıldığından anlamına gelir. 
* **Okunabilir ikincil veritabanları**: uygulamanın birincil veritabanına erişmek için kullanılan aynı veya farklı güvenlik sorumluları kullanarak salt okunur işlemleri için ikincil bir veritabanı erişebilirsiniz. Güncelleştirmeler (günlük yeniden yürütme) birincil çoğaltma ikincil sorgular tarafından ertelendi değil emin olmak için anlık görüntü yalıtım modunda ikincil veritabanlarıyla çalışır.

   > [!NOTE]
   > İkincil bir şema kilidi gerektiren birincil sunucudan alma şema güncelleştirmesi olduğunda günlük yeniden yürütme ikincil veritabanını ertelendi. 
   > 

* **Birden çok okunabilir ikinciller**: iki veya daha fazla ikincil veritabanları artırmak artıklık ve birincil veritabanı ve uygulama için bir koruma düzeyi. Birden fazla ikincil veritabanı yoksa, ikincil veritabanlarıyla biri başarısız olsa bile uygulama korumalı olarak kalır. Yeni bir ikincil veritabanı oluşturulana kadar yalnızca bir ikincil veritabanı yoktur ve bu başarısız olursa, uygulama için daha yüksek risk açıktır.

   > [!NOTE]
   > Genel olarak dağıtılmış bir uygulama oluşturun ve 4'ten fazla bölgelerindeki veri salt okunur erişim sağlamak gereken etkin coğrafi çoğaltma kullanıyorsanız, ikincil (zincirleme olarak bilinen işlem), ikincil oluşturabilirsiniz. Bu şekilde veritabanı çoğaltma neredeyse sınırsız ölçeği elde edebilirsiniz. Ayrıca, zincirleme birincil veritabanından çoğaltma ek yükünü azaltır. Dengelemeyi yaprak çoğu ikincil veritabanları hakkında daha fazla çoğaltma gecikmesi ' dir. . 
   >

* **Esnek havuz veritabanlarının Destek**: aktif coğrafi çoğaltma, herhangi bir esnek havuzdaki herhangi bir veritabanı için yapılandırılabilir. İkincil veritabanını başka bir esnek havuzda olabilir. Hizmet katmanları aynı olduğu sürece normal veritabanları için ikincil bir esnek havuz tersi olabilir. 
* **İkincil veritabanını yapılandırılabilir performans düzeyini**: birincil daha düşük performans düzeyine sahip ikincil bir veritabanı oluşturulabilir. Birincil ve ikincil veritabanları aynı hizmet katmanı için gereklidir. Artan çoğaltma gecikmesi, yük devretme sonrasında önemli veri kaybı riski artırır çünkü bu seçenek ile yüksek veritabanı yazma etkinliği uygulamalar için önerilmez. Ayrıca, yeni birincil daha yüksek bir performans düzeyine yükseltilene kadar yük devretme sonrasında uygulamanızın performansı etkilenir. Azure portalında günlük GÇ yüzdesi grafik ikincil çoğaltma yükü sürdürebilmek için gereken en düşük performans düzeyini tahmin etmek için en iyi yolu sağlar. Örneğin, birincil veritabanı P6 ise (1000 DTU) ve kendi günlük GÇ yüzde 50 ikincil en az olması gerekir % P4 (500 DTU). Kullanarak günlük GÇ verilerini de alabilirsiniz [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) veya [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) veritabanı görünümleri.  SQL veritabanı performans düzeyleri hakkında daha fazla bilgi için bkz: [SQL Database seçenekleri ve performansı](sql-database-service-tiers.md). 
* **Kullanıcı tarafından denetlenen yük devretme ve yeniden çalışma**: ikincil bir veritabanı açıkça birincil role herhangi bir zamanda uygulama veya kullanıcı tarafından değiştirilebilir. Gerçek bir kesinti sırasında "planlanmamış" seçeneği, hangi hemen ikincil yükseltir birincil olarak kullanılmalıdır. Başarısız birincil kurtarır ve yeniden kullanılabilir olduğunda, sistem otomatik olarak kurtarılan birincil ikincil olarak işaretler ve yeni birincil ile güncel duruma getirmek. En son değişiklikleri ikincil çoğaltılmadan önce birincil başarısız olursa çoğaltma zaman uyumsuz yapısı nedeniyle, çok küçük miktarda veri planlanmamış yük devretme işlemleri sırasında kaybolur. Birden fazla ikincil kopya ile birincil devrettiğinde sistem otomatik olarak çoğaltma ilişkileri yeniden yapılandırır ve kullanıcı müdahalesi gerektirmeden yeni yükseltilen birincil kalan ikincil bağlar. Yük devretme neden kesinti azaltıldığından sonra birincil bölge uygulamaya dönmek istenebilir. Bunu yapmak için yük devretme komutunu ve "Planlanan" seçeneğiyle çağrılmalıdır. 
* **Kimlik bilgileri ve güvenlik duvarı kuralları eşitlenmiş şekilde kalmasının**: kullanmanızı öneririz [veritabanı güvenlik duvarı kuralları](sql-database-firewall-configure.md) tüm ikincil veritabanlarına sahip olmak için veritabanı ile bu kuralları çoğaltılabilir şekilde coğrafi olarak çoğaltılmış veritabanları için birincil olarak aynı güvenlik duvarı kuralları. Bu yaklaşım, hem birincil ve ikincil veritabanlarını barındıran sunucular üzerinde güvenlik duvarı kurallarını el ile yapılandırıp müşteriler gereksinimini ortadan kaldırır. Benzer şekilde, kullanarak [bulunan veritabanı kullanıcıları](sql-database-manage-logins.md) için veri erişim birincil ve ikincil veritabanları her zaman aynı sağlar kullanıcı kimlik bilgileri bir yük devretme sırasında; böylece herhangi kesinti nedeniyle oturum açma bilgileri ve parolaları ile uyuşmuyor. Eklenmesi ile [Azure Active Directory](../active-directory/active-directory-whatis.md), müşteriler, hem birincil hem de ikincil veritabanlarına kullanıcı erişimi yönetebilir ve yönetme ihtiyacını ortadan kimlik bilgileri veritabanlarında tamamen.

## <a name="auto-failover-group-capabilities"></a>Otomatik Yük devretme grubu özellikleri

Otomatik Yük devretme grupları özelliği, grup düzeyinde çoğaltma ve otomatik yük devretme destekleyerek aktif coğrafi çoğaltma, güçlü bir Özet sağlar. Ayrıca, ek dinleyicisi uç noktalarının sağlayarak yük devretme sonrasında SQL bağlantı dizesini değiştirmek için gerekliliğini kaldırır. 

* **Yük devretme grubu**: farklı bölgelerde (birincil ve ikincil sunucular) iki sunucu arasında bir veya daha çok yük devretme grupları oluşturulabilir. Her grup tüm veya bazı birincil veritabanı kesinti birincil bölge içinde nedeniyle kullanılamaz hale durumunda, bir birim olarak kurtarılan bir veya daha çok veritabanı içerebilir.  
* **Birincil sunucu**: yük devretme grubundaki birincil veritabanı barındıran bir sunucu.
* **İkincil sunucu**: yük devretme grubu ikincil veritabanları barındıran bir sunucu. İkincil sunucu, birincil sunucu ile aynı bölgede olamaz.
* **Yük devretme grubuna veritabanları ekleme**: birkaç veritabanını bir esnek havuz veya bir sunucu içinde aynı yük devretme grubuna koyabilirsiniz. Bir tek başına veritabanı grubuna eklerseniz, otomatik olarak performans düzeyinin ve aynı sürümü kullanan ikincil bir veritabanı oluşturur. Birincil veritabanını bir esnek havuz ise ikincil aynı ada sahip bir esnek havuzdaki otomatik olarak oluşturulur. İkincil bir veritabanı zaten ikincil sunucuya sahip bir veritabanı eklerseniz, bu coğrafi çoğaltma grubu tarafından devralınır.

   > [!NOTE]
   > İkincil bir veritabanı yük devretme grubunun parçası olmayan bir sunucu zaten bir veritabanı eklerken, yeni ikincil ikincil sunucuya oluşturulur. 
   >

* **Yük devretme grubu okuma-yazma dinleyicisi**: DNS CNAME kaydı biçimlendirilmiş olarak  **&lt;yük devretme grup adı&gt;. database.windows.net** geçerli birincil sunucu URL'si işaret eder. Yük devretme sonrasında birincil değiştiğinde, birincil veritabanına bağlanmaktadır için okuma-yazma SQL uygulamaları sağlar. 
* **Yük devretme grubu salt okunur dinleyicisi**: DNS CNAME kaydı biçimlendirilmiş olarak  **&lt;yük devretme grup adı&gt;. secondary.database.windows.net** ikincil sunucunun URL'sine işaret eder. Saydam belirtilen yük dengeleyici kuralları kullanarak ikincil veritabanına bağlanmak salt okunur SQL uygulamaları sağlar. İsteğe bağlı olarak, salt okunur trafiğinin ikincil sunucu kullanılabilir olmadığında otomatik olarak birincil sunucuya yeniden yönlendirilmiş olmasını isteyip istemediğinizi belirtebilirsiniz.
* **Otomatik Yük devretme İlkesi**: varsayılan olarak, yük devretme grubu otomatik yük devretme İlkesi ile yapılandırılır. Hata algılandığında hemen sonra sistem yük devretmeyi tetikler. Uygulama yük devretme iş akışını denetlemek istiyorsanız, devre dışı otomatik yük devretme kapatabilirsiniz. 
* **El ile yük devretme**: yük devretme el ile otomatik yük devretme yapılandırması bağımsız olarak herhangi bir zamanda başlatabilirsiniz. Otomatik Yük devretme İlkesi yapılandırılmış el ile yük devretme değilse yük devretme grubunda veritabanlarını kurtarmak için gereklidir. (İle tam veri eşitlemesi) zorlanmış veya kolay yük devretme işlemi başlatabilirsiniz. İkinci etkin sunucunun birincil bölge konumunu değiştirmek için kullanılabilir. Yük devretme tamamlandığında, DNS kayıtları doğru sunucu bağlantı sağlamak için otomatik olarak güncelleştirilir.
* **Veri kaybı yetkisiz kullanım süresi**: yük devretme veri kaybına neden olabilir zaman uyumsuz çoğaltma kullanılarak birincil ve ikincil veritabanları eşitlenmiş olduğundan. Otomatik Yük devretme İlkesi uygulamanızın dayanıklılık veri kaybından yansıtacak şekilde özelleştirebilirsiniz. Yapılandırarak **GracePeriodWithDataLossHours**, sistem sonuç veri kaybına büyük olasılıkla yük devretmeyi başlatmadan önce bekleyeceği süreyi kontrol edebilirsiniz. 

   > [!NOTE]
   > Sistem algıladığında grubundaki veritabanı hala çevrimiçi olduğu (örneğin, kesinti yalnızca hizmet denetim düzlemi etkilenebilir) tarafındanayarlanandeğerbağımsızolaraktamverieşitlemesi(kolayyükdevretme)ileyükdevretmehemenetkinleştirir **GracePeriodWithDataLossHours**. Bu davranış, Kurtarma sırasında veri kaybı olmasını sağlar. Yalnızca kolay bir yük devretme mümkün değilse, yetkisiz kullanım süresi etkinleşir. Yetkisiz kullanım süresi dolmadan kesinti azaltılan, yük devretme etkinleştirilmedi.
   >

* **Birden çok yük devretme grubu**: yük devretme işlemlerini ölçeğini denetlemek için birden çok yük devretme grubu sunucuları aynı çifti için yapılandırabilirsiniz. Her grubu üzerinden bağımsız olarak başarısız olur. Çok kiracılı uygulamanızı esnek havuzlar kullanıyorsa, birincil ve ikincil veritabanları her havuzda karıştırmak için bu özelliği kullanabilirsiniz. Bu şekilde bir kesinti etkisini yalnızca yarısı kiracılar için azaltabilir.

## <a name="best-practices-of-building-highly-available-service"></a>Yüksek oranda kullanılabilir hizmet oluşturmanın en iyi uygulamalar

Müşteriler, Azure SQL veritabanı kullanan yüksek oranda kullanılabilir bir hizmet oluşturmak için bu yönergeleri izlemelidir:
- **Yük devretme grup**: farklı bölgelerde (birincil ve ikincil sunucular) iki sunucu arasında bir veya daha çok yük devretme grupları oluşturulabilir. Her grup tüm veya bazı birincil veritabanı kesinti birincil bölge içinde nedeniyle kullanılamaz hale durumunda, bir birim olarak kurtarılan bir veya daha çok veritabanı içerebilir. Yük devretme grubu, birincil olarak aynı hizmet hedefi ile ikincil coğrafi çoğaltmalı veritabanı oluşturur. Var olan bir coğrafi çoğaltma ilişkisinin yük devretme grubuna eklerseniz coğrafi ikincil ile aynı hizmet düzeyi hedefi birincil olarak yapılandırıldığından emin olun.
- **OLTP iş yükü için okuma-yazma dinleyici kullanın**: OLTP işlemleri kullanım gerçekleştirirken  **&lt;yük devretme grup adı&gt;. database.windows.net** sunucusu URL'si ve bağlantıları olacaktır. otomatik olarak birincil yönlendirilmiş. Bu URL, yük devretme sonrasında değiştirmez.  
Not yük devretme, yalnızca istemci DNS önbelleğinde yenilendiğini sonra istemci bağlantıları için yeni birincil yönlendirilir ve DNS kaydı güncelleştirilmesini gerektirir.
- **Salt okunur iş yükü için salt okunur bir dinleyici kullanın**: belirli veri eskime durumu için dayanıklı olan mantıksal olarak yalıtılmış bir salt okunur yükünü varsa, ikincil veritabanı uygulamada kullanabilirsiniz. Salt okunur oturumları kullanmak için  **&lt;yük devretme grup adı&gt;. secondary.database.windows.net** sunucunun URL'sini ve bağlantı otomatik olarak ikincil yönlendirilir. Bağlantı dizesinde amacı kullanarak okunur belirtmek ayrıca önerilir **ApplicationIntent ReadOnly =**. 
- **Performans düşüşünü için hazır**: SQL yük devretme karardır uygulama ya da kullanılan diğer hizmetlerin geri kalanından bağımsız. Uygulama "tek bir bölge ve bazı durumlarda başka bazı bileşenleri ile karışık". Düşüşünü önlemek için DR bölge olarak yedekli uygulama dağıtımında emin olun ve bu makaledeki yönergeleri izleyin.  
Not DR bölge uygulamada farklı bir bağlantı dizesi kullanmak mevcut değil.  
- **Veri kaybı hazırlama**: kesinti algılanırsa, sıfır veri kaybı için en iyisi bizim bilgi varsa SQL otomatik olarak okuma-yazma yük devretmeyi tetikler. Aksi halde, belirtilen süre boyunca bekler **GracePeriodWithDataLossHours**. Belirttiyseniz **GracePeriodWithDataLossHours**, veri kaybı hazırlıklı. Genel olarak, kesintiler sırasında Azure kullanılabilirlik korur. Veri kaybını göze alamıyorsanız, ayarladığınızdan emin olun **GracePeriodWithDataLossHours** 24 saat gibi yeterli büyüklükte bir sayı. 


## <a name="upgrading-or-downgrading-a-primary-database"></a>Yükseltme veya bir birincil veritabanı önceki sürüme indirme
Yükseltme veya ikincil bir veritabanınız kesmeden birincil veritabanı farklı performans düzeyine (içinde aynı hizmet katmanı) düşürmek. Yükseltme yaparken, ikincil veritabanı yükseltmeniz ve ardından birincil yükseltmeniz önerilir. Eski sürüme düşürmeyi, ters sırada: birincil ilk düşürmek ve ikincil düşürmek. Bu öneri, yükseltin veya farklı bir hizmet katmanı veritabanına düşürmek uygulanır. 

> [!NOTE]
> Yük devretme grubu yapılandırmasının bir parçası ikincil veritabanı oluşturduysanız, ikincil veritabanı düşürmek için önerilmez. Bu, veri katmanı yük devretme etkinleştirildikten sonra normal iş yükünü işlemek için yeterli kapasiteye sahip emin olmaktır. 
>

## <a name="preventing-the-loss-of-critical-data"></a>Önemli verilerin kaybını önleme
Geniş alan ağları yüksek gecikme nedeniyle sürekli kopyalama bir zaman uyumsuz çoğaltma mekanizması kullanır. Zaman uyumsuz çoğaltma bir hata oluşursa bazı veri kaybı kaçınılmaz hale getirir. Ancak, bazı uygulamalar, veri kaybı gerektirebilir. Bu kritik güncelleştirmeler korumak için uygulama geliştiricisi çağırabilirsiniz [sp_wait_for_database_copy_sync](https://msdn.microsoft.com/library/dn467644.aspx) işlemi sonlandırdı hemen sonra sistem yordamı. Çağırma **sp_wait_for_database_copy_sync** son kaydedilmiş işlem ikincil veritabanına gönderilene kadar çağıran iş parçacığı engeller. Ancak, yeniden ve ikincil kaydedilen iletilen işlemler için beklemez. **sp_wait_for_database_copy_sync** belirli sürekli kopyalama bağlantısı kapsamlıdır. Birincil veritabanına bağlantı haklarıyla herhangi bir kullanıcı, bu yordamı çağırabilirsiniz.

> [!NOTE]
> **sp_wait_for_database_copy_sync** veri kaybı yük devretme sonrasında engeller, ancak okuma erişimi için tam eşitleme garanti değil. Nedeni gecikme bir **sp_wait_for_database_copy_sync** yordam çağrısı önemli olabilir ve çağrı aynı anda işlem günlüğü boyutuna bağlıdır. 
> 

## <a name="programmatically-managing-failover-groups-and-active-geo-replication"></a>Yük devretme grupları ve etkin coğrafi çoğaltma programlı olarak yönetme
Otomatik Yük devretme grupları (Önizleme-) ve etkin daha önce açıklandığı gibi coğrafi çoğaltma program aracılığıyla Azure PowerShell ve REST API'si kullanılarak da yönetilebilir. Aşağıdaki tablolar kullanılabilir komutlar kümesi açıklamaktadır.

**Azure Resource Manager API ve rol tabanlı güvenlik**: aktif coğrafi çoğaltma içeren Azure Resource Manager API'leri bir dizi yönetim için de dahil olmak üzere [Azure SQL Database REST API'sini](https://docs.microsoft.com/rest/api/sql/) ve [Azure PowerShell cmdlet'leri](https://docs.microsoft.com/powershell/azure/overview). Bu API'ları kaynak gruplarının kullanımı gerektirir ve rol tabanlı güvenlik (RBAC) desteği. Erişim rolleri gerçekleştirme hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-what-is.md).

> [!NOTE]
> Aktif coğrafi çoğaltma pek çok yeni özelliği kullanarak yalnızca desteklenen [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) göre [Azure SQL REST API](https://msdn.microsoft.com/library/azure/mt163571.aspx) ve [Azure SQL Database PowerShell cmdlet'leri](https://msdn.microsoft.com/library/azure/mt574084.aspx). [(Klasik) REST API](https://msdn.microsoft.com/library/azure/dn505719.aspx) ve [Azure SQL Database (Klasik) cmdlet'leri](https://msdn.microsoft.com/library/azure/dn546723.aspx) Azure Resource Manager tabanlı API'lerini kullanarak önerilir şekilde geriye dönük uyumluluk için desteklenir. 
> 

## <a name="manage-sql-database-failover-using-using-transact-sql"></a>SQL veritabanı Transact-SQL kullanarak yük devretme kullanarak yönetme

| Komut | Açıklama |
| --- | --- |
| [ALTER DATABASE (Azure SQL veritabanı)](https://msdn.microsoft.com/library/mt574871.aspx) |Varolan bir veritabanını ve başlatır veri çoğaltma için ikincil bir veritabanı oluşturmak için ikincil üzerinde Sunucu Ekle bağımsız değişkenini kullanın |
| [ALTER DATABASE (Azure SQL veritabanı)](https://msdn.microsoft.com/library/mt574871.aspx) |Yük devretme başlatmak için birincil olarak ikincil bir veritabanı geçiş yapmak için yük DEVRETME veya FORCE_FAILOVER_ALLOW_DATA_LOSS kullanın |
| [ALTER DATABASE (Azure SQL veritabanı)](https://msdn.microsoft.com/library/mt574871.aspx) |Bir SQL veritabanı ve belirtilen ikincil veritabanı arasında veri kopyalama sonlandırmak için ikincil üzerinde SUNUCUSUNU Kaldır kullanın. |
| [sys.geo_replication_links (Azure SQL veritabanı)](https://msdn.microsoft.com/library/mt575501.aspx) |Azure SQL Database mantıksal sunucusunda her veritabanı için tüm yineleme bağlantıları hakkında bilgi verir. |
| [sys.dm_geo_replication_link_status (Azure SQL veritabanı)](https://msdn.microsoft.com/library/mt575504.aspx) |Belirli bir SQL veritabanı için son çoğaltma saati, son çoğaltma gecikmesi ve çoğaltma bağlantısı hakkında diğer bilgi alır. |
| [sys.dm_operation_status (Azure SQL veritabanı)](https://msdn.microsoft.com/library/dn270022.aspx) |Çoğaltma bağlantılarının durumunu da dahil olmak üzere tüm veritabanı işlemleri için durumunu gösterir. |
| [sp_wait_for_database_copy_sync (Azure SQL veritabanı)](https://msdn.microsoft.com/library/dn467644.aspx) |tüm kaydedilmiş işlemleri çoğaltılır ve etkin ikincil veritabanı tarafından onaylanan kadar beklemeniz uygulamanın neden olur. |
|  | |

## <a name="manage-sql-database-failover-using-using-powershell"></a>SQL veritabanı yük devretme PowerShell kullanarak yönetme

| Cmdlet | Açıklama |
| --- | --- |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase) |Bir veya daha fazla veritabanı alır. |
| [AzureRmSqlDatabaseSecondary yeni](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary) |Var olan bir veritabanı için ikincil bir veritabanı oluşturur ve veri çoğaltma başlatır. |
| [Set-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary) |Yük devretme başlatmak için birincil olarak ikincil bir veritabanı geçer. |
| [Remove-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) |Bir SQL veritabanı ve belirtilen ikincil veritabanı arasında veri kopyalama sonlandırır. |
| [Get-AzureRmSqlDatabaseReplicationLink](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) |Bir Azure SQL Database ve bir kaynak grubu veya SQL Server arasındaki coğrafi Çoğaltma bağlantılarını alır. |
| [AzureRmSqlDatabaseFailoverGroup yeni](/powershell/module/azurerm.sql/set-azurermsqldatabasefailovergroup) |   Bu komut, bir yük devretme grubu oluşturur ve birincil ve ikincil sunucularda kaydeder|
| [Remove-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/remove-azurermsqldatabasefailovergroup) | Yük devretme grubu sunucusundan kaldırır ve tüm siler ikincil veritabanları dahil grubu |
| [Get-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/get-azurermsqldatabasefailovergroup) | Yük devretme grubu yapılandırmasını alır. |
| [Set-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/set-azurermsqldatabasefailovergroup) |   Yük devretme grubunun yapılandırmasını değiştirir |
| [Anahtar AzureRMSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/switch-azurermsqldatabasefailovergroup) | İkincil sunucuya Yük devretme grubu Tetikleyicileri yük devretme |
|  | |

> [!IMPORTANT]
> Örnek komut dosyaları için bkz: [Yapılandır ve yük devretme aktif coğrafi çoğaltma kullanarak tek bir veritabanı](scripts/sql-database-setup-geodr-and-failover-database-powershell.md), [Yapılandır ve yük devretme aktif coğrafi çoğaltma kullanarak havuza alınmış bir veritabanı](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md), ve [Yapılandır ve yük devretme bir tek veritabanı (Önizleme) için yük devretme grubu] (komut dosyaları/sql-database-setup-geodr-failover-database-failover-group-powershell.md.
>

## <a name="manage-sql-database-failover-using-the-rest-api"></a>SQL veritabanı yük devretme REST API kullanarak yönetme
| API | Açıklama |
| --- | --- |
| [Oluşturma veya güncelleştirme veritabanı (createMode = geri yükle)](/rest/api/sql/Databases/CreateOrUpdate) |Oluşturur, güncelleştirir veya bir birincil veya ikincil bir veritabanını geri yükler. |
| [Get oluştur veya veritabanı durumunu güncelleştir](/rest/api/sql/Databases/CreateOrUpdate) |Durum oluşturma işlemi sırasında döndürür. |
| [İkincil veritabanının birincil (Planlı yük devretme) olarak ayarlayın](https://docs.microsoft.com/rest/api/sql/replicationlinkss#ReplicationLinks_Failover) |Hangi veritabanı çoğaltmasını birincil yapabilmesini geçerli birincil çoğaltma veritabanından göre ayarlar. |
| [İkincil veritabanının birincil (planlanmamış yük devretme) olarak ayarlayın](https://docs.microsoft.com/rest/api/sql/replicationlinks#ReplicationLinks_FailoverAllowDataLoss) |Hangi veritabanı çoğaltmasını birincil yapabilmesini geçerli birincil çoğaltma veritabanından göre ayarlar. Bu işlem, veri kaybına neden olabilir. |
| [Çoğaltma bağlantısı Al](/rest/api/sql/replicationlinks/get) |Belirli çoğaltma bağlantısı belirli bir SQL veritabanında bir coğrafi çoğaltma ortaklığı alır. Sys.geo_replication_links katalog görünümünde görünür bilgi alır. |
| [Çoğaltma bağlantılarını - veritabanı göre listesi](/rest/api/sql/replicationlinks/listbydatabase) | Coğrafi çoğaltma ortaklığı belirli bir SQL veritabanında tüm çoğaltma bağlantılarını alır. Sys.geo_replication_links katalog görünümünde görünür bilgi alır. |
| [Çoğaltma bağlantısı Sil](/rest/api/sql/databases/delete) | Bir veritabanı yinelemesi siler. Yük devretme sırasında yapılamaz. |
| [Oluşturma veya güncelleştirme yük devretme grubu] / rest/api/sql/failovergroups/createorupdate) | Oluşturur veya bir yük devretme grubu güncelleştirir |
| [Yük devretme grubu Sil](/rest/api/sql/failovergroups/delete) | Yük devretme grubu sunucudan kaldırır |
| [Yük devretme (planlanmış)](/rest/api/sql/failovergroups/failover) | Geçerli birincil sunucudan bu sunucuya yöneltilir. |
| [Zorla yük devretme veri kaybı izin ver](/rest/api/sql/failovergroups/forcefailoverallowdataloss) |üzerinden bu sunucu için geçerli birincil sunucudan ails. Bu işlem, veri kaybına neden olabilir. |
| [Get yük devretme grubu](/rest/api/sql/failovergroups/get) | Bir yük devretme grubunu alır. |
| [Sunucu tarafından listesi yük devretme grupları](/rest/api/sql/failovergroups/listbyserver) | Bir sunucu yük devretme gruplarında listeler. |
| [Yük devretme grubu güncelleştir](/rest/api/sql/failovergroups/update) | Bir yük devretme grubu güncelleştirir. |
|  | |

## <a name="next-steps"></a>Sonraki adımlar
* Örnek komut dosyaları için bkz:
   - [Yapılandırma ve yük devretme aktif coğrafi çoğaltma kullanarak tek bir veritabanı](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
   - [Yapılandırma ve yük devretme aktif coğrafi çoğaltma kullanarak havuza alınmış bir veritabanı](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md)
   - [Yapılandırma ve yük devretme yük devretme bir grup için tek bir veritabanına (Önizleme)](scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md)
* İş sürekliliğine genel bakış ve senaryolar için bkz: [iş sürekliliğine genel bakış](sql-database-business-continuity.md)
* Veritabanı Yedeklemeleri otomatik Azure SQL hakkında bilgi edinmek için bkz: [SQL veritabanı yedeklemeleri otomatik](sql-database-automated-backups.md).
* Kurtarma için otomatik yedeklemeler kullanma hakkında bilgi edinmek için bkz: [bir veritabanını hizmeti tarafından başlatılan yedeklerden geri](sql-database-recovery-using-backups.md).
* Yeni birincil sunucu ve veritabanı için kimlik doğrulama gereksinimleri hakkında bilgi edinmek için [olağanüstü durum kurtarma işleminden sonra SQL veritabanı güvenlik](sql-database-geo-replication-security-config.md).

