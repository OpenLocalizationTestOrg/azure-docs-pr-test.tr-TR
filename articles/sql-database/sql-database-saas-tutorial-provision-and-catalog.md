---
title: "Azure SQL Database kullanan çok kiracılı uygulama aaaProvision yeni kiracılar | Microsoft Docs"
description: "Nasıl tooprovision ve yeni katalog Kiracı hello Wingtip SaaS uygulama öğrenin"
keywords: "sql veritabanı öğreticisi"
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: sstein
ms.openlocfilehash: eb26f523305650c2124e36707d187dfcdad06fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-new-tenants-and-register-them-in-hello-catalog"></a>Yeni kiracılar sağlamak ve hello kataloğunda kaydetme

Bu öğreticide, hello sağlamak ve Katalog SaaS desenleri ve hello Wingtip SaaS uygulamasının nasıl uygulandığı hakkında bilgi edinin. Oluşturun ve yeni Kiracı veritabanlarını başlatmak ve bunları hello uygulamanın Kiracı kataloğunda kaydedin. başlangıç kataloğu hello eşlemesini hello SaaS uygulamanın birçok kiracılar ve verilerini tutan bir veritabanıdır. başlangıç kataloğu uygulama isteklerini toohello doğru veritabanı yönlendirerek önemli bir rol oynar.  

Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]

> * Nasıl bu uygulanan aracılığıyla atlama dahil olmak üzere tek yeni bir kiracı sağlama
> * Ek kiracı grubu sağlama


Bu öğretici, Önkoşullar aşağıdaki yapma emin hello tamamlanır toocomplete:

* Merhaba Wingtip SaaS uygulaması dağıtılır. beş dakikadan kısa toodeploy bakın [dağıtma ve Merhaba Wingtip SaaS uygulaması keşfedin.](sql-database-saas-tutorial.md)
* Azure PowerShell’in yüklendiğinden. Ayrıntılar için bkz. [Azure PowerShell’i kullanmaya başlama](https://docs.microsoft.com/powershell/azure/get-started-azureps)

## <a name="introduction-toohello-saas-catalog-pattern"></a>Giriş toohello SaaS katalog düzeni

Bir veritabanı yedeği çok kiracılı SaaS uygulamasına, her bir kiracı için bilgi depolandığı önemli tooknow değil. Merhaba SaaS katalog desende katalog her Kiracı arasında verilerini depolandıkları kullanılan toohold hello eşleme veritabanıdır. Merhaba Wingtip SaaS uygulaması tek Kiracı veritabanı mimarisi kullanır, ancak bir çok kiracılı veya tek Kiracı veritabanı kullanılıp kullanılmadığını Kiracı veritabanı eşleme bir katalogda depolanması hello temel desenini geçerlidir.

Her bir kiracı hello kataloğunda tanımlayan bir anahtar atanır ve olduğu hello uygun veritabanı toohello konumunu eşlenmiş. Merhaba Wingtip SaaS uygulamada karmasını hello kiracının adı hello anahtarı oluşturulur. Bu tooconstruct hello anahtarı hello uygulama URL'si toobe hello Kiracı adı kısmını kullanılan sağlar. Diğer Kiracı anahtar düzenleri kullanılabilir.  

başlangıç kataloğu hello adını veya Merhaba uygulaması üzerinde en az etkiyle değiştirilen hello veritabanı toobe konumunu sağlar.  Çok Kiracı veritabanı modelinde, bu da 'Kiracı veritabanları arasında taşıma' düzenler.  bir kiracı olup olmadığını Hello katalog de kullanılan tooindicate olabilir veya veritabanı bakım veya başka eylemler için çevrimdışı. Bu hello incelediniz [tek bir kiracı öğretici geri](sql-database-saas-tutorial-restore-single-tenant.md).

Ayrıca, bir SaaS uygulaması için bir yönetim veritabanı etkili olur, hello katalog ek Kiracı ya da veritabanı meta veri depolayabilir, hello gibi bir veritabanı, şema sürümü, hizmet planı veya SLA sürümünü veya katmanı tootenants ve diğer bilgiler, sunduğu Uygulama Yönetimi, müşteri desteği veya devops işlemler sağlar.  

SaaS uygulamasına Hello hello Katalog veritabanı araçları etkinleştirebilirsiniz.  Hello incelediniz kullanılan tooenable arası Kiracı sorgu Hello Wingtip SaaS örnek hello katalogdur [geçici analytics Öğreticisi](sql-database-saas-tutorial-adhoc-analytics.md). Veritabanları arası iş yönetimi hello incelediniz [Şema Yönetimi](sql-database-saas-tutorial-schema-management.md) ve [Kiracı analytics](sql-database-saas-tutorial-tenant-analytics.md) öğreticileri. 

Merhaba Wingtip SaaS uygulamada hello katalog hello hello parça yönetim özellikleri kullanılarak uygulanır [esnek veritabanı istemci kitaplığı (EDCL)](sql-database-elastic-database-client-library.md). bir uygulama toocreate Hello EDCL sağlar, yönetmek ve bir veritabanı yedeği parça eşleme kullanın. Bir parça eşleme parça (veritabanları) ve anahtarları (kiracılar) ile veritabanları arasında hello eşleme listesini içerir.  EDCL işlevleri Kiracı toocreate hello girişleri hello parça eşlemesindeki sağlama sırasında uygulamaları veya PowerShell betikleri kullanılabilir ve uygulamaları tooefficiently toohello doğru veritabanı bağlanın. EDCL bağlantı bilgileri toominimize hello trafiği toohello Katalog veritabanı ve Merhaba uygulaması hızlandırmak önbelleğe alır.  

> [!IMPORTANT]
> Merhaba eşleme verilerini hello katalog veritabanında erişilebilir durumda ancak *düzenleme yapmadığınız*! Eşleme verilerini yalnızca Elastik Veritabanı İstemci Kitaplığı API’sini kullanarak düzenleyin. Doğrudan hello bozulmasını riskleri katalog ve desteklenmeyen hello eşleme veri düzenleme.


## <a name="introduction-toohello-saas-provisioning-pattern"></a>Giriş toohello SaaS sağlama düzeni

Ne zaman ekleme tek Kiracı veritabanı modeli yeni bir kiracı veritabanı kullanan bir SaaS uygulaması yeni bir kiracı sağlanmalıdır.  Merhaba uygun konumu ve hizmet katmanı ile uygun şema ve başvuru verileri başlatılmadı ve hello uygun Kiracı anahtarı altında hello kataloğunda kayıtlı oluşturulması gerekir.  

Farklı yaklaşımlar SQL betikleri yürütülürken, bir bacpac dağıtma ya da 'Altın' şablon veritabanı kopyalayarak dahil sağlama, kullanılan toodatabase olabilir.  

kullandığınız yaklaşım sağlama hello yeni veritabanları ile en son şema hello sağlandığından emin olun, genel şema yönetim stratejinizi içinde comprehended gerekir.  Bu hello incelediniz [şema yönetimi Öğreticisi](sql-database-saas-tutorial-schema-management.md).  

Altın veritabanı kopyalayarak hello Wingtip SaaS uygulama hükümleri yeni kiracılar hello katalog sunucusunda dağıtılan basetenantdb adlı.  Sağlama Merhaba uygulaması bir kayıt deneyimi bir parçası olarak tümleştirilmiş ve/veya desteklenen komut dosyalarını kullanarak çevrimdışı. Bu öğretici, PowerShell kullanarak sağlama inceleyeceksiniz. Merhaba sağlama komut dosyalarını bir esnek havuz hello basetenantdb toocreate yeni bir kiracı veritabanı kopyalama sonra Kiracı özgü bilgiyle başlatmak ve hello katalog parça eşlemesinde kaydedin.  Merhaba örnek uygulamasında veritabanları hello Kiracı adına göre adları verilir, ancak bu hello düzeni önemli bir parçası değil – hello katalog hello kullanılmasına izin verir, herhangi bir ad atanan toobe toohello veritabanı. + 


## <a name="get-hello-wingtip-application-scripts"></a>Merhaba Wingtip uygulama komut dosyaları alma

Merhaba Wingtip SaaS komut dosyaları ve uygulama kaynak koduna hello kullanılabilir [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github depo. [Adımları toodownload hello Wingtip SaaS betikleri](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).


## <a name="provision-and-catalog-detailed-walkthrough"></a>Sağlama ve kataloğa kaydetme ile ilgili ayrıntılı kılavuz

toounderstand nasıl uygulama sağlama yeni Kiracı uygulayan Wingtip Merhaba, bir kesme noktası ekleyin ve bir kiracı sağlarken hello akışı adım:

1. Aç... \\Öğrenme modülleri\\ProvisionAndCatalog\\_Demo ProvisionAndCatalog.ps1_ ve kümesi hello aşağıdaki parametreleri:
   * **$TenantName** = hello yeni yerini hello adı (örneğin, *Bushwillow mavi*).
   * **$VenueType** hello önceden tanımlanmış salonundan türlerinden birini =: *mavi*, classicalmusic, dance jazz, judo, motorracing, çok amaçlı, opera, rockmusic, futbol.
   * **$DemoScenario** = **1**çok ayarlayın**1** çok*tek bir kiracı sağlama*.

1. İmlecinizi herhangi bir yere bildiren satır 48 hello satırda koyarak kesme noktası ekleme: *yeni Kiracı '*ve basın **F9**.

   ![kesme noktası](media/sql-database-saas-tutorial-provision-and-catalog/breakpoint.png)

1. toorun hello betik tuşuna **F5**.

1. Merhaba komut dosyası yürütme hello kesme noktasında durdurulduktan sonra basın **F11** hello koda toostep.

   ![kesme noktası](media/sql-database-saas-tutorial-provision-and-catalog/debug.png)



Hello kullanarak hello komut yürütmeyi **hata ayıklama** menü seçenekleri - **F10** ve **F11** toostep üzerinden veya hello işlevleri çağrılır. PowerShell komut dosyalarını hata ayıklama hakkında daha fazla bilgi için bkz: [ile çalışma ve PowerShell betikleri hata ayıklama ipuçları](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/how-to-debug-scripts-in-windows-powershell-ise).


Merhaba değil adımları tooexplicitly izleyin, ancak bir açıklama, aracılığıyla hello komut dosyası hata ayıklama sırasında adım hello akışının şunlardır:

1. **İçeri aktarma hello SubscriptionManagement.psm1** tooAzure imzalama ve hello çalıştığınız Azure aboneliği seçmek için işlevleri içeren modülü.
1. **İçeri aktarma hello CatalogAndDatabaseManagement.psm1** bir katalog ve Kiracı düzeyinde soyutlama hello sağlar Modülü [parça yönetim](sql-database-elastic-scale-shard-map-management.md) işlevleri. Bu hello katalog düzeni çoğunu yalıtır ve incelenmesi yararlı olan önemli bir modüldür.
1. **Yapılandırma ayrıntılarını alın**. Get-yapılandırmasını (F11) adımla ve nasıl hello uygulama yapılandırma belirtilen bakın. Kaynak adları ve diğer uygulamaya özgü değerleri burada tanımlanan ancak hello kodlarla bilginiz kadar bu değerleri değiştirmeyin.
1. **Başlangıç kataloğu nesnesini almak**. Oluşturur ve hello üst düzey komut dosyasında kullanılan bir katalog nesnesi döndüren Get katalog adımla.  Bu işlev üzerinden içe aktarılan parça yönetim işlevlerini kullanan **AzureShardManagement.psm1**. Merhaba Katalog nesnesi hello aşağıdakilerden oluşur:
   * $catalogServerFullyQualifiedName hello standart stem artı kullanıcı adınızı kullanarak yapılandırılmıştır: _katalog -\<kullanıcı\>. database.windows.net_.
   * $catalogDatabaseName hello yapılandırma dosyasından alınır: *tenantcatalog*.
   * $shardMapManager nesne hello katalog veritabanından başlatılır.
   * $shardMap nesne hello başlatılmış *tenantcatalog* hello katalog veritabanındaki parça eşleme.
   Bir katalog nesnesi oluşur ve döndürülen ve hello üst düzey komut dosyasında kullanılan.
1. **Merhaba yeni bir kiracı anahtarı hesaplamak**. Kullanılan toocreate hello Kiracı anahtarı hello Kiracı adı bir karma işlevdir.
1. **Merhaba Kiracı anahtarı olup olmadığını denetle**. başlangıç kataloğu tooensure hello anahtar kullanılabilir denetlenir.
1. **Merhaba Kiracı veritabanı ile yeni TenantDatabase sağlanır.** Kullanım **F11** içinde toostep ve nasıl hello veritabanı olup kullanılarak sağlanan bir [Azure Resource Manager şablonu](../azure-resource-manager/resource-manager-template-walkthrough.md).

Merhaba veritabanı adı toowhich Kiracı hangi parça ait işaretini hello Kiracı adı toomake oluşturulur. (Veritabanı adlandırma diğer stratejileri kolayca kullanılabilir.) + Bir Resource Manager şablonu hello katalog sunucusunda altın veritabanı (baseTenantDB) kopyalayarak kullanılan toocreate Kiracı veritabanı değil. Alternatif bir yaklaşım, boş bir veritabanı toocreate olmalı ve ardından bunu bir bacpac veya tooexecute içeri aktararak başlatma betiği iyi bilinen bir konumdan başlatılamıyor.  

Merhaba Resource Manager şablonu hello ...\Learning Modules\Common\ bulunan klasördür: *tenantdatabasecopytemplate.json*

Merhaba Kiracı veritabanı oluşturulduktan sonra daha sonra başka **hello salonundan (Kiracı) adı ve hello salonundan türü ile başlatılmış**. Burada, diğer başlatma işlemleri de yapılabilir.

Merhaba **hello Kataloğu'nda kayıtlı Kiracı veritabanı** ile *Ekle TenantDatabaseToCatalog* hello Kiracı anahtarı kullanarak. Kullanım **F11** toostep hello ayrıntıları içine:

* Merhaba Katalog veritabanı toohello parça eşleme (bilinen veritabanlarının listesini hello) eklenir.
* Bu bağlantılar hello anahtar değeri toohello parça eşleştirmeyi hello oluşturulur.
* Merhaba Kiracı hakkında ek meta veriler (Merhaba salonundan'ın adı) toohello kiracılar tablo hello kataloğunda eklenir.  Merhaba kiracılar tablo hello ShardManagement şema parçası olmayan ve EDCL hello tarafından yüklü değil.  Bu tabloda hello Katalog veritabanı toosupport ek uygulamaya özgü verileri nasıl Genişletilebilir gösterilmektedir.   


Sağlama tamamlandıktan sonra yürütme toohello özgün döndürür *Demo ProvisionAndCatalog* hello açar betik **olayları** sayfa hello tarayıcıda hello yeni Kiracı için:

   ![etkinlikler](media/sql-database-saas-tutorial-provision-and-catalog/new-tenant.png)


## <a name="provision-a-batch-of-tenants"></a>Kiracılar toplu sağlama

Bu alıştırmada 17 kiracılar toplu sağlar. Böylece birden fazla birkaç veritabanları toowork ile diğer Wingtip SaaS öğreticileri başlatmadan önce bu toplu kiracıların sağlamak önerilir.

1. Aç... \\Öğrenme modülleri\\ProvisionAndCatalog\\*Demo ProvisionAndCatalog.ps1* hello içinde *PowerShell ISE* hello değiştirip *$ DemoScenario* parametresi too3:
   * **$DemoScenario** = **3**, çok değiştirme**3** çok*kiracılar toplu sağlama*.
1. Tuşuna **F5** ve hello komut dosyasını çalıştırın.

Merhaba betik ek kiracılar toplu dağıtır. Kullandığı bir [Azure Resource Manager şablonu](../azure-resource-manager/resource-manager-template-walkthrough.md) hello toplu denetler ve her veritabanı tooa bağlantılı şablonunu sağlama atar. Bu şekilde şablonları kullanarak Azure Resource Manager toobroker hello sağlama işlemi betiğiniz sağlar. Şablonları sağlamak veritabanları burada olabilir ve gerekirse, yeniden deneme işler paralel hello genel işlem en iyi duruma getirme. Merhaba komut dosyası başarısız olduğunda veya herhangi bir nedenle durdurur ise ıdempotent bu nedenle onu yeniden çalıştırılır.

### <a name="verify-hello-batch-of-tenants-successfully-deployed"></a>Kiracıların başarıyla dağıtılan Hello toplu doğrulayın

* Açık hello *tenants1* tooyour hello sunucularının listesini giderek sunucu [Azure portal](https://portal.azure.com), tıklatın **SQL veritabanları**ve 17 ek veritabanlarının hello toplu şimdi doğrulayın Merhaba listesinde:

   ![veritabanı listesi öğesine tıklayın](media/sql-database-saas-tutorial-provision-and-catalog/database-list.png)



## <a name="other-provisioning-patterns"></a>Diğer sağlama düzenleri

Bu öğreticide yer almayan diğer sağlama düzenleri şunlardır:

**Veritabanlarını önceden hazırlama.** Desen önceden sağlama hello ek bir maliyeti esnek havuzdaki veritabanları eklemeyin hello olgu yararlanan. Merhaba esnek havuz için faturalama olduğunda, veritabanları hello değil ve boşta veritabanları hiçbir kaynaklarını tüketebilir. Bir havuzdaki veritabanları önceden sağlama ve bunları gerektiğinde ayırma Kiracı ekleme zamanı önemli ölçüde azaltılabilir. oranı sağlama gerekli tookeep hello için uygun bir arabellek beklenen şekilde önceden sağlanan veritabanı hello sayısı ayarlanmış.

**Otomatik sağlama.** Otomatik sağlama Hello desende bir adanmış sağlama kullanılan tooprovision sunucular, havuzları ve veritabanları otomatik olarak – önceden sağlama veritabanları esnek havuzları, isterseniz de dahil olmak üzere gerektiğinde hizmetidir. Ve istediğiniz gibi hizmet sağlama hello tarafından veritabanları XML'deki yaptırılan ve silinmiş, esnek havuzlar boşlukları doldurulabilir. Bu tür bir hizmet Örneğin, birden çok farklı coğrafyalara, sağlama işleme basit veya karmaşık – olabilir ve bu strateji olağanüstü durum kurtarma için kullanılırsa coğrafi çoğaltma otomatik olarak ayarlayabilirsiniz. Hello otomatik sağlama düzendeki bir istemci uygulama veya betik hizmet sağlama hello tarafından işlenen bir sağlama isteği tooa sıra toobe göndermek ve ardından hello hizmet toodetermine tamamlama yoklaması. Önceden hazırlama kullanılırsa, istekleri hızlı bir şekilde hello arka planda çalışan değiştirme veritabanı sağlama yönetme hello hizmeti ile ele alınması.



## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, şunları öğrendiniz:

> [!div class="checklist"]

> * Tek bir yeni kiracı sağlama
> * Ek kiracı grubu sağlama
> * Kiracılar sağlama ve hello kataloğuna kaydetme hello ayrıntılarını girme

Merhaba deneyin [performans izleme Öğreticisi](sql-database-saas-tutorial-performance-monitoring.md).

## <a name="additional-resources"></a>Ek Kaynaklar

* Ek [hello Wingtip SaaS uygulamasına yapı öğreticileri](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Elastik veritabanı istemci kitaplığı](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-database-client-library)
* [Windows PowerShell ISE tooDebug nasıl komutlar](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/how-to-debug-scripts-in-windows-powershell-ise)
