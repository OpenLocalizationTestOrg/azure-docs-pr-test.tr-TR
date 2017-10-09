---
title: "aaaCortana Intelligence çözüm Değerlendirme Aracı | Microsoft Docs"
description: "Microsoft Partner toofollow toopublish Cortana Intelligence çözüm tooAppSource gerek duyduğunuz tüm hello adımlar şunlardır."
services: machine-learning
documentationcenter: 
author: AnupamMicrosoft
manager: jhubbard
editor: cgronlun
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: anupams;v-bruham;garye
ms.openlocfilehash: 76cde4e2090c121683b7026f3d80f90f64566607
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-evaluation-tool"></a>Cortana Intelligence çözüm değerlendirme aracı
## <a name="overview"></a>Genel Bakış
Microsoft tarafından önerilen en iyi yöntemlere için de Gelişmiş analiz çözümleriniz hello Cortana Intelligence çözüm Değerlendirme Aracı tooassess kullanabilirsiniz. Microsoft, ortaklarımızın ile Çoğalması toowork (ISV'ler / SIS) müşteriler, satıcılar ve uygulama için tooprovide yüksek kaliteli çözümler. Bu kılavuz çözümünüzle birlikte hello çözüm Değerlendirme Aracı kullanmanın hello işleminde size rehberlik ve belirli en iyi yöntemleri denetler hello açıklayın.

## <a name="getting-started"></a>Başlarken
Lütfen [karşıdan](https://aka.ms/aa-evaluation-tool-download) ve hello Cortana Intelligence çözüm değerlendirme aracı yükleyin.

Ön koşullar:
- Windows 10: [Windows 10 için resmi sitesi](https://www.microsoft.com/en-us/windows)
- Azure Powershell: [yükleyin ve Azure PowerShell yapılandırma](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).

## <a name="identifying-your-app"></a>Uygulamanızı tanımlama
Yükleme tamamlandıktan sonra hello aracını açın ve ilk değerlendirmeniz başlayın.

![Açık değerlendirme aracı](./media/cortana-intelligence-appsource-evaluation-tool/1-open-evaluation-tool.png)

Çözümünüzü hakkında tanıtıcı bilgi sağlar.

![Azure aboneliğine bağlanma](./media/cortana-intelligence-appsource-evaluation-tool/2-connect-azure-subscription.png)

Tooyour Azure aboneliğine bağlanma ve hello uygulamanızı içeren kaynak grubu sağlar.

![kaynakları seçin](./media/cortana-intelligence-appsource-evaluation-tool/3-select-resources.png)

Lütfen Hello kaynak grubu yüklendikten sonra çözümünüz içinde bulunur ve tüm veri kaynakları olarak hello erişilebilirliğini tanımlamak hello kaynakları seçin:
- Alım
- Tüketim
- İç

Bu bilgileri kullanırız toobetter anlamak nasıl çözümünüzü çeşitli bileşenleri kullanan ve tooensure kullanıcı dönük bileşenleri en iyi yöntemlerle uyumlu.

### <a name="ingestion"></a>Alım
Alım bu durumda, dış hello çözümden verilerinde kullanılan toopull ya da hizmetlerin hello çözüm dışında toopush verilerini içine kullandığınız herhangi bir veri kaynağına anlamına gelir.

### <a name="consumption"></a>Tüketim
Tüketim, bu durumda kullanılan toopush veri tooend kullanıcıları, doğrudan veya dolaylı olarak olan herhangi bir veri kümeleri anlamına gelir. Örneğin:
- Powerbı doğrudan sorgu dizesinde bir veri kümesi.
- Bir WebApp sorgulanan bir veri kümesi.

>[!NOTE]
Belirli bir kaynak alımı ve tüketimi için kullanılırsa, lütfen seçin **tüketim**.

### <a name="internal"></a>İç
Yalnızca dahili uygulama işlemede kullanılan tüm veri kaynakları için iç kullanın.

Ardından, istendiğinde tooprovide hello önceki adımda belirtilen tüm veritabanları için geçerli kimlik bilgileri olacaktır:

![Set test önkoşulları](./media/cortana-intelligence-appsource-evaluation-tool/4-set-test-prerequisites.png)

## <a name="solution-test-cases"></a>Çözüm test çalışmaları
Merhaba çözüm aracı otomatikleştirilmiş testleri koleksiyonu çözümünüzü üzerinde gerçekleştirir.

![Set test yürütmesi](./media/cortana-intelligence-appsource-evaluation-tool/5-set-test-execution.png)

Hello sınamalar tamamladıktan sonra olacak bir açıklama veya neden çözümünüzü hello gereksinim ile uyumlu değil için yaslamayı tooprovide istedi.

![İş gerekçe](./media/cortana-intelligence-appsource-evaluation-tool/6-provide-business-justification.png)

Örneğin, çözümünüzü tooAzure SQL DW yayımlarsa tooAzure Analysis Services, tooalso testleri gerektiren hello değerlendirme yayımlayın. 

Çözümünüzü Sql Server Analysis Services yerine Azure Analysis Services çalışan Iaas sanal makineleri kullanabilir. Bu kabul edilebilir bir nedenden dolayı hello test başarısız olacaktır.
## <a name="packaging-your-evaluation-results"></a>Değerlendirme sonuçları paketleme
Merhaba test çalışmaları işlemini tamamladıktan sonra değerlendirme paketinizi dışarı aktarılan tooa zip dosyası olacaktır ve tooprovide geri bildirim hello değerlendirme aracı üzerinde istenir. 

Bu test sonuçları eklenen onay toobe almadan önce hesaplanan, çözüm toobe için Microsoft ile zip dosyası tooshare gerek tooAppSource

![Sınıf Değerlendirme Aracı](./media/cortana-intelligence-appsource-evaluation-tool/7-grade-evaluation-tool.png)

Bu bölümün yukarısında makale kapsamaktadır hello aracı çeşitli özellikleri, artık bize türlerini bu aracı değerlendirir en iyi uygulamaları gözden geçirme.

## <a name="security-evaluation-considerations"></a>Güvenlik Değerlendirme konuları
### <a name="databases-should-use-azure-active-directory-authentication"></a>Veritabanları Azure Active Directory kimlik doğrulaması kullanmanız gerekir
Azure Active Directory (AAD) kimlik doğrulaması ile Azure SQL veya Azure SQL DW alanındaki herhangi bir kaynağa hello sloution etkinleştirilmesi gerekir. AAD tek konumdan toomanage tüm kimlikleri ve rolleri sağlar.

| Hakkında daha fazla bilgi için | Bu makaleye bakın |
| --- | --- |
| AAD ile SQL Database ve SQL veri ambarı | [SQL Database veya SQL Data Warehouse ile kimlik doğrulaması için Azure Active Directory kimlik doğrulaması kullanma](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication) |
| Yapılandırma ve AAD yönetme | [Yapılandırma ve SQL Database veya SQL Data Warehouse ile Azure Active Directory kimlik doğrulaması yönetme](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication-configure) |
| Azure WebApps kimlik doğrulaması | [Kimlik doğrulama ve yetkilendirme Azure uygulama hizmeti](https://docs.microsoft.com/en-us/azure/app-service/app-service-authentication-overview) |
| AAD ile WebApps yapılandırın | [Nasıl tooconfigure App Service uygulama toouse Azure Active Directory oturum açma](https://docs.microsoft.com/en-us/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)|

### <a name="datasets-accessible-tooend-users-should-support-role-based-access-control"></a>Veri kümeleri erişilebilir tooend kullanıcılara rol tabanlı erişim denetimi desteklemesi gerekir
Merhaba Değerlendirme Aracı yürütülürken, siz olacaksınız herhangi raporlama veya kaynakları yayımlama toospecify istedi. Bu kaynaklara erişim için son kullanıcılar tarafından değil geliştiriciler tasarlanmıştır varsayılır. Bu kaynaklar olması sağlayacağını rol tabanlı erişim denetimi (RBAC) sipariş tooensure son kullanıcılar yalnızca mümkün tooaccess veri yetkili olduğunu.

Özellikle, aşağıdaki Azure kaynakları hello hiçbirini RBAC ile yapılandırılabilir ve kabul edilebilir olarak kabul edilir:
- Hdınsight güvenliğini sağlamak için bkz: [etki alanına katılmış Hdınsight kümeleri ile bir giriş tooHadoop güvenliği](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-domain-joined-introduction)
- Azure SQL bkz [ile Azure SQL AAD kimlik doğrulaması]( https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication)
- Azure Analysis Services, bkz: [için Azure Analysis Services veritabanı rolleri ve kullanıcıları yönetme](https://docs.microsoft.com/azure/analysis-services/analysis-services-database-users)
- Azure SQL veri ambarı (SQL DW RBAC desteklemediğinden, bu doğrudan son kullanıcı erişimi için önerilmez unutmayın.)

Lütfen RBAC destekleyen farklı bir kaynak türü kullanıyorsanız, hello test çalışması düzenlemede belirtin.

### <a name="azure-data-lake-store-should-use-at-rest-encryption"></a>Azure Data Lake Store rest sırasında şifreleme kullanmanız gerekir
Azure Data Lake deposu (ADLS) çalışmıyorken şifreleme ADLS yönetilen şifreleme anahtarları kullanılarak varsayılan olarak destekler. Azure anahtar kasası kullanarak şifreleme de yapılandırabilirsiniz.

ADLS şifreleme ayarlarını belirtme hakkında bilgi için [bir Azure Data Lake Store hesabı oluşturma](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-portal#create-an-azure-data-lake-store-account).

### <a name="azure-sql-and-azure-sql-data-warehouse-should-use-encryption"></a>Azure SQL ve Azure SQL Data Warehouse şifreleme kullanmalıdır
Saydam veri şifreleme (gerçek zamanlı şifreleme ve şifre çözme veri ve günlük dosyalarının sağlayan TDE), Azure SQL hem de Azure SQL DW destekler.

| Hakkında daha fazla bilgi için | Bu makaleye bakın |
| --- | --- |
| Saydam veri şifreleme (TDE) | [Saydam veri şifreleme](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-tde) |
| TDE ile Azure SQL veri ambarı | [Encrption TDE TSQL SQL veri ambarı](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-encryption-tde-tsql) |
| Azure SQL TDE'nin ile yapılandırma | [Saydam veri şifrelemesi ile Azure SQL veritabanı](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database) |
| Her zaman şifreli ile Azure SQL yapılandırın | [SQL veritabanı Azure anahtar kasası her zaman şifrelenir.](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-always-encrypted-azure-key-vault)|

Ayrıca tooTDE, Azure SQL ayrıca her zaman şifreli destekler, veri şifrelenir sağlayan yeni bir veri şifreleme teknolojisi yalnızca çalışmıyorken ve istemci ile sunucu arasında aynı zamanda veriler taşıma sırasında hello sunucuda komutları yürütülürken kullanılıyor.

### <a name="any-virtual-machines-must-be-deployed-from-hello-azure-marketplace"></a>Herhangi bir sanal makine hello Azure Marketi dağıtılmalıdır
Sipariş tooprovide güvenlik AppSource arasında tutarlı bir düzeyde, Cortana Intelligence çözümün bir parçası dağıtılan tüm sanal makineleri sertifikalı ve Azure Marketi hello üzerinde yayımlanan gerektirir.

toosearch hello geçerli Azure Market görüntülerini listesini [Microsoft Azure Market](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute).

Nasıl toopublish bir sanal makine görüntü için Azure Marketi hakkında daha fazla bilgi için bkz: [Kılavuzu toocreate hello Azure Marketi için bir sanal makine görüntüsü](https://docs.microsoft.com/en-us/azure/marketplace-publishing/marketplace-publishing-vm-image-creation).

## <a name="scalability-evaluation-considerations"></a>Ölçeklenebilirlik değerlendirme konuları
### <a name="cortana-intelligence-solutions-should-include-a-scalable-big-data-platform"></a>Cortana Intelligence çözümleri ölçeklenebilir büyük veri platformu içermelidir
Cortana Intelligence çözümleri toovery büyük veri boyutları ölçeklendirmeniz gerekir. Azure'da hello iki Petabayt ölçekli veri platformu birini içermelidir anlamına gelir:
- Azure Data Lake Store
- Azure SQL Veri Ambarı

Lütfen çözümünüzü bu veri boyutları için destek gerektirmiyorsa veya bir alternatif veri platformu kullanılıyorsa, bu hello test çalışması düzenlemede açıklanmaktadır.
### <a name="cortana-intelligence-solutions-should-include-dedicated-ingestion-data-environments"></a>Cortana Intelligence çözümleri ayrılmış alım veri ortamları içermelidir
Cortana Intelligence çözümler genellikle doğrudan veri ilişkisel veri kaynakları ekleme kaçınmalısınız. Bunun yerine, Azure Data Factory kullanarak herhangi bir ilişkisel depolarını ıdempotent ekler/güncelleştirmelerini ile yapılandırılmamış bir ortamda ham verileri depolanması gerekir.

Azure Data Factory ile veri kopyalama hakkında daha fazla bilgi için [öğretici: Visual Studio kullanarak kopyalama etkinliği ile işlem hattı oluşturma](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-copy-activity-tutorial-using-visual-studio).

### <a name="azure-sql-data-warehouse-should-use-polybase-for-data-ingestion"></a>Azure SQL veri ambarı veri alımı için PolyBase kullanmanız gerekir
Azure SQL DW düzeyde ölçeklenebilir, paralel veri alımı için PolyBase destekler. PolyBase, Azure Blob Storage veya Azure Data Lake Store içinde depolanan dış veri kümeleri toouse Azure SQL DW tooissue sorguları sağlar. Bu, toplu güncelleştirmeler tooalternative yöntemlerini üstün performans sağlar.

PolyBase ve Azure SQL DW Başlarken ile ilgili yönergeler için bkz: [SQL Data warehouse'da PolyBase ile veri yükleme](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-get-started-load-with-polybase).

PolyBase ve Azure SQL DW ile en iyi uygulamalar hakkında daha fazla bilgi için bkz: [SQL Data Warehouse'da PolyBase kullanarak Kılavuzu](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide).

## <a name="availability-evaluation-considerations"></a>Kullanılabilirlik değerlendirme konuları

### <a name="datasets-accessible-tooend-users-should-support-a-large-volume-of-concurrent-users"></a>Eşzamanlı kullanıcı büyük miktarda veri kümeleri erişilebilir tooend kullanıcılar desteklemesi gerekir
Merhaba Değerlendirme Aracı yürütülürken, siz olacaksınız herhangi raporlama veya kaynakları yayımlama toospecify istedi. Bu kaynaklara erişim için son kullanıcılar tarafından değil geliştiriciler tasarlanmıştır varsayılır. Bu kaynaklar Orta çok sayıda eşzamanlı kullanıcıyı desteklemesi gerekir.

Özellikle, Azure SQL Data Warehouse hello tek veri kaynağı kullanılabilir tooend kullanıcıları olmamalıdır. Azure SQL DW Power Users için bir kaynak olarak sağlanırsa, Azure Analysis Services kullanılabilir tootypical kullanıcılara yapılmalıdır.

Azure SQL DW eşzamanlılık sınırları hakkında daha fazla bilgi için bkz: [SQL Data Warehouse eşzamanlılık ve iş yükü yönetimi](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-develop-concurrency).

Azure Analysis Services hakkında daha fazla bilgi için bkz: [Analysis Services'e genel bakış](https://docs.microsoft.com/azure/analysis-services/analysis-services-overview).

### <a name="azure-sql-resources-should-have-a-read-only-replica-for-failover"></a>Azure SQL kaynaklarını yük devretme için salt okunur bir çoğaltmaya sahip olmalıdır
Azure SQL veritabanları coğrafi çoğaltma tooa ikincil örneği destekler. Bu örnek bir yük devretme örneği tooprovide yüksek kullanılabilirlik uygulamaları olarak kullanılabilir.

Azure SQL veritabanları için coğrafi çoğaltma hakkında daha fazla bilgi için bkz: [SQL veritabanı coğrafi Çoğaltmaya genel bakış](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-overview).

Yönergeler için tooconfigure Azure SQL için coğrafi çoğaltma Bkz [aktif coğrafi çoğaltma Transact-SQL ile Azure SQL veritabanı için yapılandırma](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-transact-sql).

### <a name="azure-sql-data-warehouse-should-have-geo-redundant-backups-enabled"></a>Azure SQL Data Warehouse coğrafi olarak yedekli yedeklemeleri etkin olması gerekir
Azure SQL DW günlük yedekleri toogeo yedekli depolama destekler. Bu coğrafi çoğaltma, birincil bölgenizde depolanan anlık görüntü nerede erişemiyor durumlarda bile hello veri ambarını geri sağlar. Bu özellik varsayılan olarak açıktır ve Cortana Intelligence çözümleri için devre dışı olmaması gerekir.

Azure SQL DW yedekleme ve geri yükleme hakkında daha fazla bilgi için burada gördüğünüz [SQL veri ambarı yedekleri](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-backups).

### <a name="virtual-machines-should-be-configured-with-availability-sets"></a>Sanal makineler kullanılabilirlik kümeleri ile yapılandırılmalıdır
Azure sanal makinelerde sipariş toominimize hello planlanmış ve planlanmamış bakım olayları etkisini kullanılabilirlik kümelerinde yapılandırılması gerekir.

Azure sanal makinesi kullanılabilirliği hakkında daha fazla bilgi için bkz: [hello azure'da Windows sanal makinelerin kullanılabilirliğini yönetme](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability).

## <a name="other-evaluation-considerations"></a>Diğer değerlendirme konuları
### <a name="cortana-intelligence-apps-should-use-a-centralized-tool-for-data-orchestration"></a>Cortana Intelligence uygulamalar veri düzenlemesi için merkezi bir araç kullanmanız gerekir
Yönetme ve veri taşıma ve dönüştürme zamanlama için tek bir aracı kullanarak, görev açısından kritik verilerin etrafına tutarlı olmasını sağlar. Yeniden deneme mantığı, bağımlılık yönetimi, uyarı/günlük vb. geçici Temizle mantığı sağlar. Merhaba kullanılmasını öneririz [Azure Data Factory](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-introduction) Azure veri düzenleme için.

Veri düzenlemesi için Azure Data Factory dışında bir aracı kullanıyorsanız, hangi aracı veya kullandığınız araçları açıklanmaktadır.
### <a name="azure-machine-learning-models-should-be-retrained-using-azure-data-factory"></a>Azure Machine Learning modellerini retrained Azure Data Factory
Azure Machine Learning (AzureML) hello oluşturulmasını ve dağıtımını Tahmine dayalı modelleme ve makine öğrenimi işlem hatları için kolay toouse araçlar sağlar. Bununla birlikte, bu AzureML modellerinin üretim dağıtımları tek bir sabit veri kümesine bağlı değildir, ancak bunun yerine gerçek phenomena dinamikleri kaydırma toohello uyum önemlidir.

Yeniden eğitme web Hizmetleri içinde AzureML oluşturma hakkında daha fazla bilgi için bkz: [yeniden eğitme Machine Learning modellerini programlama aracılığıyla](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-retrain-models-programmatically).

Azure Data Factory kullanarak hello model Eğitim işlemini otomatikleştirme hakkında daha fazla bilgi için bkz: [kaynak güncelleştirme etkinliği kullanarak güncelleştirme Azure Machine Learning modellerini](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-azure-ml-update-resource-activity).

## <a name="existing-documentation"></a>Var olan belgeler
[Microsoft Azure sertifikalı toogrow bulut iş](https://azure.microsoft.com/en-us/marketplace/programs/certified/)

[Microsoft Azure Cortana Intellignece için sertifikalı](https://azure.microsoft.com/en-us/marketplace/programs/certified/cortana/)

