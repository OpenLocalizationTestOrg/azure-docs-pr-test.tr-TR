---
title: "aaaManaging ölçeklendirilmiş bulut veritabanları | Microsoft Docs"
description: "Merhaba esnek veritabanı iş hizmeti gösterir"
metakeywords: azure sql database elastic databases
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 6fa47cf2-1162-4534-a206-6e2d95b78580
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: b6d330cd712421b8cba781e835830772e6e5b77e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-scaled-out-cloud-databases"></a>Ölçeklendirilen bulut veritabanlarını yönetme
toomanage ölçeklendirilmiş parçalı veritabanları, hello **esnek veritabanı işleri** (Önizleme) etkinleştirir, tooreliably veritabanları dahil olmak üzere, bir grup arasında bir Transact-SQL (T-SQL) komut dosyası yürütme özellik:

* Özel tanımlı bir koleksiyon veritabanlarının (aşağıda açıklanmıştır)
* tüm veritabanları bir [esnek havuz](sql-database-elastic-pool.md)
* Parça kümesi (kullanılarak oluşturulan [esnek veritabanı istemci Kitaplığı](sql-database-elastic-database-client-library.md)). 

## <a name="documentation"></a>Belgeler
* [Merhaba esnek veritabanı iş bileşenlerini yüklemek](sql-database-elastic-jobs-service-installation.md). 
* [Esnek veritabanı işleri ile çalışmaya başlama](sql-database-elastic-jobs-getting-started.md).
* [PowerShell kullanarak işleri oluşturmak ve yönetmek](sql-database-elastic-jobs-powershell.md).
* [Oluşturma ve Azure SQL veritabanlarını ölçeklendirilmiş yönetme](sql-database-elastic-jobs-getting-started.md)

**Esnek veritabanı iş** şu anda bir müşteri tarafından barındırılan Azure bulut hello yürütme geçici olarak adlandırılan zamanlanmış yönetim görevlerini ve sağlayan bir hizmettir **işleri**. İşleri ile kolayca ve Transact-SQL betikleri tooperform yönetim işlemleri çalıştırarak Azure SQL veritabanları oluşan büyük gruplar güvenilir bir şekilde yönetin. 

![Esnek veritabanı iş hizmeti][1]

## <a name="why-use-jobs"></a>İşlerini neden kullanılır?
**Yönetme**

Kolayca şema değişiklikleri, kimlik bilgileri yönetimi, başvuru veri güncelleştirmeleri, performans verileri toplama veya Kiracı (müşteri) telemetri koleksiyonu.

**Raporlar**

Koleksiyona tek hedef tablo Azure SQL veritabanları birleşik veriler.

**Ek yükü azaltın**

Normalde, tooeach veritabanında bağımsız olarak sipariş toorun Transact-SQL deyimleri bağlanmak veya diğer yönetim görevleri gerçekleştirin. Bir işi hello hedef grubu tooeach veritabanında oturum hello görev işler. Ayrıca tanımlamak, korumak ve bir Azure SQL veritabanları grubu boyunca yürütülen Transact-SQL betikleri toobe kalır.

**Hesap oluşturma**

İşlerini hello durumunu komut dosyası ve günlük hello her veritabanı için yürütme çalıştırın. Hatalar oluştuğunda, otomatik yeniden deneme de alırsınız.

**Esneklik**

Bir işi zamanlamaları tanımlamak ve Azure SQL veritabanlarının özel grupları tanımlayın.

> [!NOTE]
> Hello Azure portal, yalnızca sınırlı sayıda işlevi tooSQL Azure esnek sınırlı havuzları mevcut değil. Merhaba PowerShell API'lerinden tooaccess hello kümesini geçerli işlevi kullanın.
> 
> 

## <a name="applications"></a>Uygulamalar
* Yeni bir şema dağıtımı gibi yönetim görevlerini gerçekleştirin.
* Başvuru verileri ürün bilgileri ortak tüm veritabanları arasında güncelleştirin. Veya her hafta içi günü, saat sonra zamanlamaları otomatik güncelleştirmeler.
* Dizinleri tooimprove sorgu performansını yeniden oluşturun. Merhaba yeniden yapılandırılmış tooexecute veritabanlarının düzenli olarak, bir koleksiyon üzerinden gibi yoğun olmayan saatlerde olabilir.
* Sorgu sonuçları veritabanları kümesinden bir devam eden temelinde merkezi bir tabloya toplayın. Performans sorguları sürekli olarak çalıştırılabilir ve yürütülen tootrigger ek görevleri toobe yapılandırılır.
* Çok sayıda veritabanları arasında daha uzun çalışan veri işleme sorguları yürütmek, örneğin müşteri telemetri koleksiyonunu hello. Sonuçlar daha fazla çözümleme için bir tek hedef tabloya toplanır.

## <a name="elastic-database-jobs-end-to-end"></a>Esnek veritabanı iş: uçtan uca
1. Merhaba yüklemek **esnek veritabanı işleri** bileşenleri. Daha fazla bilgi için bkz: [esnek veritabanı yükleme işleri](sql-database-elastic-jobs-service-installation.md). Merhaba yüklemesi başarısız olursa bkz [nasıl toouninstall](sql-database-elastic-jobs-uninstall.md).
2. Merhaba PowerShell API'lerinden tooaccess zamanlamaları ekleme ve/veya sonuç kümelerini toplama özel tanımlı veritabanı koleksiyonları, örneğin oluşturmak daha fazla işlevini kullanın. Kullanım hello portal basit yükleme ve oluşturma/izleme işlerin karşı tooexecution sınırlı bir **esnek havuz**. 
3. İş yürütme için şifrelenmiş kimlik bilgileri oluşturun ve [hello grubunda hello kullanıcı (veya rol) tooeach veritabanı Ekle](sql-database-security-overview.md).
4. Idempotent hello grubundaki her veritabanı karşı çalıştırabilirsiniz T-SQL komut dosyası oluşturun. 
5. Bu adımları toocreate işleri Hello Azure portal kullanarak izleyin: [oluşturma ve esnek veritabanı işlerini yönetme](sql-database-elastic-jobs-create-and-manage.md). 
6. Veya PowerShell betikleri kullanma: [oluşturma ve PowerShell (Önizleme) kullanarak bir SQL Database esnek veritabanı işlerini yönetmek](sql-database-elastic-jobs-powershell.md).

## <a name="idempotent-scripts"></a>Idempotent komut dosyaları
Merhaba betikleri olmalıdır [ıdempotent](https://en.wikipedia.org/wiki/Idempotence). Basitçe "ıdempotent" Merhaba betik başarılı olursa ve yeniden çalıştırın hello aynı sonucu oluştuğunu anlamına gelir. Bir komut dosyası tootransient ağ sorunları başarısız olabilir. Bu durumda, hello iş çalışan hello betik hazır kaç kez desisting önce otomatik olarak yeniden deneyecek. Idempotent komut dosyası başarıyla iki kez çalıştırılmış olsa bile aynı sonucu hello sahiptir. 

Basit bir Taktik bunun tootest onu oluşturmadan önce hello varlığını bir nesne için ' dir.  

    IF NOT EXIST (some_object)
    -- Create hello object 
    -- If it exists, drop hello object before recreating it.

Benzer şekilde, bir komut dosyası mümkün tooexecute başarıyla için mantıksal olarak test ederek olmalıdır ve ilgili koşulları countering bulur.

## <a name="failures-and-logs"></a>Hataları ve günlükleri
Bir komut dosyası birden çok denemeden sonra başarısız olursa, hello iş hello Hata günlüklerini ve devam eder. (Merhaba grubundaki tüm veritabanlarının karşı çalıştırma anlamına gelir), bir iş sona erdikten sonra başarısız girişim listesini kontrol edebilirsiniz. Merhaba günlükleri ayrıntıları toodebug hatalı komut dosyaları sağlar. 

## <a name="group-types-and-creation"></a>Grup türleri ve oluşturma
İki tür Grup vardır: 

1. Parça kümeleri
2. Özel gruplar

Parça kümesi grupları hello kullanarak oluşturulur [esnek veritabanı araçlarını](sql-database-elastic-scale-introduction.md). Bir parça kümesi grubu oluşturduğunuzda, veritabanları eklenemez veya hello grubundan otomatik olarak kaldırılamaz. Örneğin, toohello parça eşleme eklediğinizde, yeni bir parça otomatik olarak hello grubunda olacaktır. Bir işi hello Grup karşı çalıştırabilirsiniz.

Özel gruplar üzerinde diğer yandan Merhaba, aracılığı tanımlanır. Açıkça ekleyin veya özel gruplarından veritabanlarını kaldırmanız gerekir. Merhaba gruptaki bir veritabanı bağlantı kesilirse hello iş toorun hello betik hello veritabanında bir nihai karşılanamamasına dener. Şu anda Hello Azure portalını kullanarak oluşturduğunuz özel gruplar gruplarıdır. 

## <a name="components-and-pricing"></a>Bileşenleri ve fiyatlandırma
Merhaba aşağıdaki bileşenleri birlikte toocreate yönetim işlemleri geçici olarak yürütülmesini sağlar bir Azure bulut hizmetinde çalışır. Merhaba bileşenler yüklenir ve aboneliğinizde Kurulum sırasında otomatik olarak yapılandırılır. Bunların tümü sahip hello gibi aynı otomatik olarak oluşturulan hello Hizmetleri tanımlayabilirsiniz adı. Merhaba adının benzersiz olduğundan ve "Merhaba önek edj 21 rastgele oluşturulmuş karakterle devam etmelidir" oluşur.

* **Azure bulut hizmeti**: esnek veritabanı işleri (Önizleme) bir müşteri barındırılan Azure bulut olarak teslim hizmeti tooperform hello yürütülmesi istenen görevler. Merhaba Portalı'ndan hello hizmet dağıtılan ve Microsoft Azure aboneliğiniz barındırılır. yüksek kullanılabilirlik için iki çalışan rolleri hello az Hello dağıtılan varsayılan hizmeti çalışır. Her çalışan rolü (ElasticDatabaseJobWorker) Hello varsayılan boyutu A0 örneği üzerinde çalışır. Fiyatlandırma için bkz: [fiyatlandırma bulut Hizmetleri](https://azure.microsoft.com/pricing/details/cloud-services/). 
* **Azure SQL veritabanı**: hello hizmetinin kullandığı hello bilinen bir Azure SQL veritabanı **denetim veritabanı** toostore tüm hello işi meta verileri. Merhaba varsayılan hizmet katmanına bir S0 ' dir. Fiyatlandırma için bkz: [SQL Database fiyatlandırması](https://azure.microsoft.com/pricing/details/sql-database/).
* **Azure Service Bus**: bir Azure hizmet veri yolu hello iş hello Azure bulut hizmeti içinde eşgüdümünü içindir. Bkz: [hizmet veri yolu fiyatlandırma](https://azure.microsoft.com/pricing/details/service-bus/).
* **Azure depolama**: bir Azure depolama hesabı kullanılır toostore tanılama çıktı sorunu daha fazla hata ayıklama gerektiren hello olay günlüğü (bkz [Azure Cloud Services ve sanal makineleri etkinleştirme tanılamada](../cloud-services/cloud-services-dotnet-diagnostics.md)). Fiyatlandırma için bkz: [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-elastic-database-jobs-work"></a>Esnek veritabanı işleri nasıl çalışır
1. Bir Azure SQL veritabanı belirlenmiş bir **denetim veritabanı** tüm meta verileri ve Durum verilerini depolar.
2. Merhaba denetim veritabanı hello tarafından erişilen **iş hizmeti** toolaunch ve izleme işleri tooexecute.
3. İki farklı roller hello denetim veritabanı ile iletişim kurar: 
   * Denetleyicisi: yeni iş görevleri oluşturarak görevleri tooperform hello iş ve yeniden deneme başarısız olan işler istenen hangi işlerin gerektiren belirler.
   * İş görevi yürütmede: hello iş görevleri gerçekleştirir.

### <a name="job-task-types"></a>İş görev türleri
İşlerini yürütme taşımak iş görevleri birden çok tür vardır:

* ShardMapRefresh: Kullanılan tüm hello veritabanlarını parça parça eşleme toodetermine sorguları Merhaba
* ScriptSplit: hello komut dosyası toplu işleri 'Git' deyime arasında böler.
* ExpandJob: alt işleri her veritabanı için bir grubu hedefleyen bir işten oluşturur
* ScriptExecution: bir komut dosyası tanımlanmış kimlik bilgilerini kullanarak belirli bir veritabanında yürütür
* Dacpac: belirli kimlik bilgileri kullanılarak DACPAC tooa belirli bir veritabanının uygular

## <a name="end-to-end-job-execution-work-flow"></a>Uçtan uca iş yürütme iş akışı
1. Merhaba Portal veya PowerShell API'si hello kullanarak, bir iş hello eklenen **denetim veritabanı**. Merhaba iş belirli kimlik bilgileri kullanılarak veritabanlarının bir gruba göre bir Transact-SQL betiği yürütülmesini istiyor.
2. Merhaba denetleyicisi hello yeni iş tanımlar. İş görevleri oluşturulur ve toosplit hello betik ve toorefresh hello grubun veritabanları yürütülür. Son olarak, yeni bir iş oluşturulur ve tooexpand hello iş yürütülen ve yeni alt her bir alt iş belirtilen tooexecute hello Transact-SQL betiği hello grubundaki tek bir veritabanının karşı olduğu işleri oluşturun.
3. Merhaba denetleyicisi oluşturulan alt işleri hello tanımlar. Her iş için hello denetleyicisi oluşturur ve bir iş görevi tooexecute hello komut dosyası bir veritabanında tetikler. 
4. Tüm iş görevleri tamamladıktan sonra hello denetleyicisi hello işleri tamamlandı tooa durumunu güncelleştirir. 
   İş yürütme sırasında herhangi bir noktada hello PowerShell API'si kullanılan tooview olabilir hello iş yürütme geçerli durumu. Tüm saatler UTC PowerShell API'lerinden temsil edilen hello tarafından döndürülen. İsterseniz, iptal isteğini başlatılan toostop bir iş olabilir. 

## <a name="next-steps"></a>Sonraki adımlar
[Merhaba bileşenlerini yüklemek](sql-database-elastic-jobs-service-installation.md), ardından [oluşturun ve veritabanlarının hello grubundaki tooeach veritabanında bir günlük ekleyin](sql-database-manage-logins.md). toofurther iş oluşturulması ve Yönetimi anlamak, [esnek veritabanı işleri oluşturmaya ve yönetmeye](sql-database-elastic-jobs-create-and-manage.md). Ayrıca bkz. [esnek veritabanı işlerine Başlarken](sql-database-elastic-jobs-getting-started.md).

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-overview/elastic-jobs.png
<!--anchors-->


