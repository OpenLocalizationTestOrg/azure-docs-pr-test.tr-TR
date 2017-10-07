---
title: "aaaCreate & Azure SQL sunucuları ve veritabanlarını yönetme | Microsoft Docs"
description: "Azure SQL veritabanı sunucusu ve veritabanı kavramları hakkında ve oluşturma hakkında daha fazla bilgi edinin ve yönetme sunucular ve veritabanları kullanarak Azure portal, PowerShell, hello Azure CLI, Transact-SQL ve hello REST API hello."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 0f526e388a5a620349f5a14e8d57a8355ac451ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-sql-database-servers-and-databases"></a>Azure SQL veritabanı sunucuları ve veritabanları oluşturma ve yönetme

Bir Azure SQL veritabanı içinde oluşturulan Microsoft Azure yönetilen bir veritabanında olan bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) tanımlanan bir dizi [farklı iş yükleri için işlem ve depolama kaynaklarını](sql-database-service-tiers.md). Azure SQL veritabanını, belirli bir Azure bölge içinde oluşturulan bir Azure SQL Database mantıksal sunucusu ile ilişkilidir. 

## <a name="an-azure-sql-database-can-be-a-single-pooled-or-partitioned-database"></a>Bir Azure SQL veritabanı bir tek, havuza alınmış veya Bölümlenmiş veritabanı olabilir

Bir Azure SQL veritabanı olabilir:

- [Kendi kaynak kümesine](sql-database-what-is-a-dtu.md#what-are-database-transaction-units-dtus) (DTU) sahip tek veritabanı
- Parçası bir [SQL esnek havuzu](sql-database-elastic-pool.md) , [bir kaynak kümesini paylaşır](sql-database-what-is-a-dtu.md#what-are-elastic-database-transaction-units-edtus) (Edtu'lar)
- Tek başına veya havuza eklenmiş veritabanlarından oluşan [parçalı veritabanlarından oluşan ölçeği genişletilmiş kümenin](sql-database-elastic-scale-introduction.md#horizontal-and-vertical-scaling) bir parçası
- [Çok kiracılı SaaS tasarım desenine](sql-database-design-patterns-multi-tenancy-saas-applications.md) katılan ve veritabanları tek başına ya da havuza eklenmiş (veya her ikisi de) olabilecek bir veritabanı kümesinin bir parçası 

> [!TIP]
> Geçerli veritabanı adları için bkz. [Veritabanı Tanımlayıcıları](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers). 
>
 
- Microsoft Azure SQL veritabanı tarafından kullanılan hello varsayılan veritabanı harmanlama **sql_latin1_general_cp1_cı_as**, burada **LATIN1_GENERAL** İngilizce (Birleşik Devletler) **CP1** kod sayfası 1252, **CI** , küçük harf duyarlıdır ve **AS** aksan duyarlı değil. Nasıl tooset hello harmanlama hakkında daha fazla bilgi için bkz: [COLLATE (Transact-SQL)](https://msdn.microsoft.com/library/ms184391.aspx).
- Microsoft Azure SQL veritabanı tablo veri akışı (TDS) Protokolü istemci sürümü 7.3 veya üst sürümünü destekler.
- Yalnızca TCP/IP bağlantılarını izin verilir.

## <a name="what-is-an-azure-sql-logical-server"></a>Bir Azure SQL mantıksal sunucusuna nedir?

Merkezi bir yönetim noktası dahil olmak üzere birden çok veritabanı için bir mantıksal sunucu görür [SQL esnek havuzu](sql-database-elastic-pool.md) [oturumları](sql-database-manage-logins.md), [güvenlik duvarı kuralları](sql-database-firewall-configure.md), [denetleme kuralları](sql-database-auditing.md), [tehdit algılama ilkeleri](sql-database-threat-detection.md), ve [yük devretme grupları](sql-database-geo-replication-overview.md). Bir mantıksal sunucu, kaynak grubu farklı bir bölgede olabilir. hello Azure SQL veritabanı oluşturmadan önce hello mantıksal sunucunun mevcut olması gerekir. Bir sunucudaki tüm veritabanları aynı hello içinde oluşturulan bölge hello mantıksal sunucusu olarak. 


> [!IMPORTANT]
> SQL veritabanı'nda bir sunucu hello şirket içi dünyada alışkın olabileceğiniz bir SQL Server örneği farklıdır mantıksal bir yapıdır. Özellikle, hello SQL veritabanı hizmetinin garanti hello veritabanlarına ilişkin ilişkisinde tootheir mantıksal sunucu yapar ve hiçbir örnek düzeyinde erişim veya özellikleri gösterir.
> 

Bir mantıksal sunucu oluşturduğunuzda, oturum açma hesabı ve bu sunucu üzerinde yönetici hakları toohello ana veritabanı ve bu sunucuda oluşturulan tüm veritabanlarına sahip parola bir sunucu belirtin. Bir SQL oturum açma hesabı bu ilk hesaptır. Azure SQL veritabanı SQL kimlik doğrulaması ve Azure Active Directory kimlik doğrulaması için kimlik doğrulamasını destekler. Oturum açma ve kimlik doğrulama hakkında daha fazla bilgi için bkz: [yönetme veritabanları ve oturum açma bilgileri Azure SQL veritabanında](sql-database-manage-logins.md). Windows Kimlik Doğrulaması desteklenmez. 

> [!TIP]
> Geçerli bir kaynak grubu ve sunucu adları için bkz: [adlandırma kuralları ve sınırlamaları](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).
>

Azure SQL Veritabanı mantıksal sunucusu:

- Bir Azure aboneliği oluşturuldu, ancak onun içerdiği kaynakların tooanother aboneliğe taşınabilmesi
- Veritabanları, esnek havuzlar ve veri ambarlarında Hello üst kaynağı
- Veritabanları, esnek havuzlar ve veri ambarlarında için bir ad alanı sağlar
- Olan mantıksal bir kapsayıcı güçlü ömrü semantiği - bir sunucu ve siler Sil ile Merhaba kapsanan veritabanları, esnek havuzlar ve veri ambarlarında
- Katılan [Azure rol tabanlı erişim denetimi (RBAC)](/active-directory/role-based-access-control-what-is) -veritabanları, esnek havuzlar ve bir sunucu içindeki veri ambarlarında hello sunucudan erişim hakları devral
- Yönetim amacıyla hello kimliğini veritabanları, esnek havuzlar ve Azure kaynağı için veri ambarları, yüksek sıralı öğesidir (Merhaba URL'i veritabanları ve havuzları düzeni)
- Bir bölgedeki kaynakları birlikte bulundurur
- Veritabanı erişimi için bağlantı uç noktası sağlar (<serverName>.database.windows.net)
- Dmv'leri aracılığıyla bağlanan tooa ana veritabanı tarafından kapsanan kaynaklara ilişkin erişim toometadata sağlar 
- Merhaba kapsamını tooits veritabanları - oturumları uygulamak, güvenlik duvarı, Denetim, tehdit algılama, vb. yönetim ilkeleri için sağlar. 
- Merhaba üst abonelik içindeki bir kota tarafından kısıtlanmış (varsayılan - abonelik başına altı sunucu [abonelik sınırlar buraya bakın](../azure-subscription-service-limits.md))
- Hello kaynaklar (45000 DTU gibi) içerdiği için veritabanı kota ve DTU kota Hello kapsamın sağlar
- Merhaba sürüm oluşturma kapsamı içindeki kaynaklara etkinleştirilen özellikleri için 
- Sunucu düzeyinde asıl kullanıcı bilgileri bir sunucudaki tüm veritabanlarını yönetebilir
- Oturum açma bilgileri içerebilir erişim tooone ya da daha fazla veritabanı hello sunucuda verilir ve olabilir, şirket içinde SQL Server örneklerinde benzer toothose verilen sınırlı yönetim hakları. Daha fazla bilgi için bkz. [Kullanıcı Bilgileri](sql-database-manage-logins.md).

## <a name="azure-sql-databases-protected-by-sql-database-firewall"></a>SQL veritabanı güvenlik duvarı tarafından korunan azure SQL veritabanları

toohelp, verilerinizi korumaya bir [SQL veritabanı Güvenlik Duvarı](sql-database-firewall-configure.md) tüm erişim tooyour veritabanı sunucusu veya Azure aboneliği bağlantınızı üzerinden doğrudan bağlantı toohello sunucunuza dışında kendi veritabanlarından birini engeller. tooenable ek bağlantı gerekir [bir veya daha fazla güvenlik duvarı kuralları oluşturma](sql-database-firewall-configure.md#creating-and-managing-firewall-rules). Oluşturma ve SQL esnek havuzlarını yönetmek için bkz: [esnek havuzlar](sql-database-elastic-pool.md).

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-azure-portal"></a>Azure SQL sunucuları, veritabanları ve güvenlik duvarları hello Azure portal kullanarak yönetme

Hello Azure SQL Database'in kaynak grubu vaktinden veya hello sunucusunun kendisi oluştururken oluşturabilirsiniz. Tooa yeni SQL server form, yeni bir SQL server oluşturarak veya yeni bir veritabanı oluşturmak bir parçası olarak almak için birden çok yöntem bulunmaktadır. 

### <a name="create-a-blank-sql-server-logical-server"></a>Boş bir SQL server (mantıksal sunucu) oluşturun

bir Azure SQL veritabanı sunucusu (olmadan bir veritabanı) kullanarak toocreate hello [Azure portal](https://portal.azure.com), tooa boş SQL server (mantıksal sunucu) form gidin. Hello aşağıdaki ekran görüntüsü bir form toocreate açmak için bir yöntem boş bir mantıksal SQL sunucusu gösterir. 

   ![mantıksal sunucu tamamlandı formu oluşturma](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

Başka bir yöntemi kullanarak toothis form alırsanız, hello formdaki hello bilgileri aynıdır.

### <a name="create-a-blank-or-sample-sql-database"></a>Boş veya örnek bir SQL veritabanı oluşturma

bir Azure SQL veritabanı kullanarak toocreate hello [Azure portal](https://portal.azure.com), tooa boş SQL veritabanı formu gidin ve sağlamak hello istenen bilgileri. Hello Azure SQL Database'in kaynak grubu ve mantıksal sunucu vaktinden veya hello veritabanının kendisi oluştururken oluşturabilirsiniz. Boş bir veritabanı oluşturmayı veya Adventure Works LT. üzerinde temel bir örnek veritabanı oluşturma 

  ![create database-1](./media/sql-database-get-started-portal/create-database-1.png)

> [ÖNEMLİ] Fiyatlandırma katmanı veritabanınız için hello seçme konusunda daha fazla bilgi için bkz: [hizmet katmanları](sql-database-service-tiers.md).
>

### <a name="manage-an-existing-sql-server"></a>Mevcut bir SQL server'ı yönetme

toomanage var olan bir sunucu kullanarak çeşitli yöntemler - gibi belirli SQL veritabanı sayfası uğradıysa hello toohello sunucusuna gidin **SQL sunucuları** sayfa veya hello **tüm kaynakları** sayfası. ekran görüntüsü gösterildiği nasıl aşağıdaki hello hello sunucu düzeyinde güvenlik duvarı ayarını toobegin **genel bakış** bir sunucu için sayfa. 

   ![mantıksal sunucusuna genel bakış](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

Varolan bir veritabanını toomanage gidin toohello **SQL veritabanları** sayfasında ve hello veritabanını toomanage tıklayın. ekran görüntüsü gösterildiği nasıl aşağıdaki hello hello bir veritabanı için bir sunucu düzeyinde güvenlik duvarı ayarını toobegin **genel bakış** bir veritabanı için sayfası. 

   ![sunucu güvenlik duvarı kuralı](./media/sql-database-get-started-portal/server-firewall-rule.png) 

> [!IMPORTANT]
> bir veritabanı tooconfigure performans özelliklerini görmek [hizmet katmanları](sql-database-service-tiers.md).
>

> [!TIP]
> Bir Azure portalı hızlı başlangıç öğreticisi için bkz: [hello Azure portalında bir Azure SQL veritabanı oluşturma](sql-database-get-started-portal.md).
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-powershell"></a>Azure SQL sunucuları, veritabanları ve güvenlik duvarları PowerShell kullanarak yönetme

toocreate ve Azure SQL server, veritabanları ve güvenlik duvarları Azure PowerShell ile yönetme, PowerShell cmdlet'leri aşağıdaki hello kullanın. PowerShell yükseltme veya tooinstall gerekir, bkz: [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps). Oluşturma ve SQL esnek havuzlarını yönetmek için bkz: [esnek havuzlar](sql-database-elastic-pool.md).

| Cmdlet | Açıklama |
| --- | --- |
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Bir veritabanı oluşturur |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Bir veya daha fazla veritabanı alır|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Bir veritabanı özelliklerini ayarlar ya da varolan bir veritabanını bir esnek havuza taşır|
|[Remove-AzureRmSqlDatabase](/powershell/module/azurerm.sql/remove-azurermsqldatabase)|Bir veritabanı kaldırır|
|[Yeni-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)|Bir kaynak grubu oluşturur]
|[AzureRmSqlServer yeni](/powershell/module/azurerm.sql/new-azurermsqlserver)|Sunucu oluşturur|
|[Get-AzureRmSqlServer](/powershell/module/azurerm.sql/get-azurermsqlserver)|Sunucuları hakkında bilgi döndürür|
|[Set-AzureRmSqlServer](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/set-azurermsqlserver)|Bir sunucu özelliklerini değiştirir|
|[Remove-AzureRmSqlServer](/powershell/module/azurerm.sql/remove-azurermsqlserver)|Bir sunucuyu kaldırır|
|[New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule)|Bir sunucu düzeyinde güvenlik duvarı kuralı oluşturur |
|[Get-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/get-azurermsqlserverfirewallrule)|Bir sunucu için güvenlik duvarı kurallarını alır|
|[Set-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/set-azurermsqlserverfirewallrule)|Bir sunucu güvenlik duvarı kuralında değiştirir|
|[Remove-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/remove-azurermsqlserverfirewallrule)|Bir güvenlik duvarı kuralı bir sunucudan siler.|

> [!TIP]
> PowerShell hızlı başlangıç öğreticisi için bkz: [PowerShell kullanarak tek bir Azure SQL veritabanı oluşturma](sql-database-get-started-portal.md). PowerShell örnek komut dosyaları için bkz: [kullanım PowerShell toocreate tek bir Azure SQL veritabanı ve bir güvenlik duvarı kuralı yapılandırın](scripts/sql-database-create-and-configure-database-powershell.md) ve [İzleyici ve ölçek tek bir SQL veritabanı PowerShell kullanarak](scripts/sql-database-monitor-and-scale-database-powershell.md).
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-azure-cli"></a>Azure SQL sunucuları, veritabanları ve güvenlik duvarları hello Azure CLI kullanarak yönetme

toocreate ve Azure SQL server, veritabanları ve güvenlik duvarları hello ile yönetme [Azure CLI](/cli/azure/overview), hello aşağıdaki kullanın [Azure CLI SQL veritabanı](/cli/azure/sql/db) komutları. Kullanım hello [bulut Kabuk](/azure/cloud-shell/overview) tarayıcınızda toorun hello CLI veya [yükleme](/cli/azure/install-azure-cli) macOS, Linux veya Windows üzerinde. Oluşturma ve SQL esnek havuzlarını yönetmek için bkz: [esnek havuzlar](sql-database-elastic-pool.md).

| Cmdlet | Açıklama |
| --- | --- |
|[az sql db oluştur](/cli/azure/sql/db#create) |Bir veritabanı oluşturur|
|[az sql db listesi](/cli/azure/sql/db#list)|Veritabanları ve tüm veri ambarlarında bir sunucu veya esnek havuzdaki tüm veritabanları listeler.|
|[az sql db listesi-sürümleri](/cli/azure/sql/db#list-editions)|Listeleri kullanılabilir hizmet hedefleri ve depolama sınırları|
|[az sql db listesi-kullanımları](/cli/azure/sql/db#list-usages)|Kullanımları döndürür veritabanı|
|[az sql db Göster](/cli/azure/sql/db#show)|Bir veritabanı veya veri ambarı alır|
|[az sql db güncelleştirme](/cli/azure/sql/db#update)|Bir veritabanını güncelleştirir|
|[az sql db Sil](/cli/azure/sql/db#delete)|Bir veritabanı kaldırır|
|[az grubu oluşturma](/cli/azure/group#create)|Bir kaynak grubu oluşturur|
|[az sql server oluşturun](/cli/azure/sql/server#create)|Sunucu oluşturur|
|[az sql sunucu listesi](/cli/azure/sql/server#list)|Sunucuları listeler|
|[az sql server listesi-kullanımları](/cli/azure/sql/server#list-usages)|Sunucu kullanımları döndürür|
|[az sql server Göster](/cli/azure/sql/server#show)|Bir sunucu alır|
|[az sql server güncelleştirmesi](/cli/azure/sql/server#update)|Bir sunucu güncelleştirir|
|[az sql server silme](/cli/azure/sql/server#delete)|Bir sunucu siler|
|[az sql server güvenlik duvarı kuralı oluşturma](/cli/azure/sql/server/firewall-rule#create)|Sunucu güvenlik duvarı kuralı oluşturur|
|[az sql server güvenlik duvarı kuralı listesi](/cli/azure/sql/server/firewall-rule#list)|Bir sunucuda Hello güvenlik duvarı kurallarını listeler|
|[az sql server güvenlik duvarı kuralı Göster](/cli/azure/sql/server/firewall-rule#show)|Bir güvenlik duvarı kuralı Hello ayrıntılarını gösterir|
|[az sql server güvenlik duvarı kuralı güncelleştirme](/cli/azure/sql/server/firewall-rule#update)|Bir güvenlik duvarı kuralını güncelleştirir|
|[az sql server güvenlik duvarı kuralını Sil](/cli/azure/sql/server/firewall-rule#delete)|Bir güvenlik duvarı kuralını siler|

> [!TIP]
> Bir Azure CLI hızlı başlangıç öğreticisi için bkz: [hello Azure CLI kullanarak tek bir Azure SQL veritabanı oluşturma](sql-database-get-started-cli.md). Azure CLI örnek komut dosyaları için bkz: [kullanım CLI toocreate tek bir Azure SQL veritabanı ve bir güvenlik duvarı kuralı yapılandırın](scripts/sql-database-create-and-configure-database-cli.md) ve [kullanım CLI toomonitor ve ölçek tek bir SQL veritabanı](scripts/sql-database-monitor-and-scale-database-cli.md).
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-transact-sql"></a>Azure SQL sunucuları, veritabanları ve güvenlik duvarları Transact-SQL kullanarak yönetme

toocreate ve Azure SQL server, veritabanları ve güvenlik duvarları Transact-SQL ile yönetmek için aşağıdaki T-SQL komutlarıyla hello kullanın. Hello Azure portal kullanarak bu komutlar gönderebilirsiniz [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [Visual Studio Code](https://code.visualstudio.com/docs), veya tooan Azure SQL veritabanı sunucusuna bağlanmak ve Transact-SQL geçirmek başka bir programı komutları. SQL esnek havuzlarını yönetmek için bkz: [esnek havuzlar](sql-database-elastic-pool.md).

> [!IMPORTANT]
> Oluşturamaz veya Transact-SQL kullanarak bir sunucu silme.
>

| Komut | Açıklama |
| --- | --- |
|[Veritabanı (Azure SQL veritabanı) oluşturma](/sql/t-sql/statements/create-database-azure-sql-database)|Yeni bir veritabanı oluşturur. Bağlı toohello ana veritabanı toocreate yeni bir veritabanı olmalıdır.|
| [ALTER DATABASE (Azure SQL veritabanı)](/sql/t-sql/statements/alter-database-azure-sql-database) |Bir Azure SQL veritabanı değiştirir. |
|[ALTER DATABASE (Azure SQL veri ambarı)](/sql/t-sql/statements/alter-database-azure-sql-data-warehouse)|Bir Azure SQL veri ambarı değiştirir.|
|[VERİTABANINI (Transact-SQL)](/sql/t-sql/statements/drop-database-transact-sql)|Bir veritabanını siler.|
|[sys.database_service_objectives (Azure SQL veritabanı)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Döndürür edition (hizmet katmanı), hizmet hedefi (fiyatlandırma katmanı) ve esnek havuz adı, varsa Azure SQL veritabanına veya Azure SQL Data Warehouse için hello. Azure SQL Database sunucusu ana veritabanında toohello oturum açmış, bilgiler tüm veritabanlarını döndürür. Azure SQL Data Warehouse için bağlı toohello ana veritabanı olmalıdır.|
|[sys.dm_db_resource_stats (Azure SQL veritabanı)](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database)| Bir Azure SQL Database veritabanı için CPU, g/ç ve bellek tüketimini döndürür. Hello veritabanında hiçbir etkinlik olsa 15 dakikada için bir satır yok.|
|[sys.resource_stats (Azure SQL veritabanı)](/sql/relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database)|CPU kullanımı ve depolama verileri için bir Azure SQL veritabanına döndürür. Merhaba veriler toplanır ve beş dakikalık aralıklarla içinde toplanır.|
|[sys.database_connection_stats (Azure SQL veritabanı)](/sql/relational-databases/system-catalog-views/sys-database-connection-stats-azure-sql-database)|SQL veritabanı veritabanı bağlantı olayları, bir veritabanı bağlantısı başarı ve başarısızlık durumlarının özetini istatistiklerini içerir. |
|[sys.event_log (Azure SQL veritabanı)](/sql/relational-databases/system-catalog-views/sys-event-log-azure-sql-database)|Başarılı Azure SQL Database veritabanı bağlantıları, bağlantı hataları ve kilitlenmeleri döndürür. Bu bilgi tootrack veya veritabanı etkinliklerinizi SQL veritabanı ile ilgili sorunları giderme kullanabilirsiniz.|
|[sp_set_firewall_rule (Azure SQL veritabanı)](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)|Oluşturur veya SQL veritabanı sunucunuzun hello sunucu düzeyinde güvenlik duvarı ayarlarını güncelleştirir. Bu saklı yordam yalnızca hello ana veritabanı toohello sunucu düzeyinde asıl oturum açma kullanılabilir. Sunucu düzeyinde güvenlik duvarı kuralı yalnızca Azure düzeyi izinleri olan bir kullanıcı tarafından hello ilk sunucu düzeyinde güvenlik duvarı kural oluşturulduktan sonra Transact-SQL kullanılarak oluşturulabilir|
|[sys.firewall_rules (Azure SQL veritabanı)](/sql/relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database)|Microsoft Azure SQL veritabanı ile ilişkili hello sunucu düzeyinde güvenlik duvarı ayarları hakkında bilgi verir.|
|[sp_delete_firewall_rule (Azure SQL veritabanı)](/sql/relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database)|Sunucu düzeyinde güvenlik duvarı ayarları, SQL veritabanı sunucusundan kaldırır. Bu saklı yordam yalnızca hello ana veritabanı toohello sunucu düzeyinde asıl oturum açma kullanılabilir.|
|[sp_set_database_firewall_rule (Azure SQL veritabanı)](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)|Oluşturur veya Azure SQL Database veya SQL Data Warehouse için hello veritabanı düzeyinde güvenlik duvarı kuralları güncelleştirir. Veritabanı güvenlik duvarı kuralları ve SQL Database kullanıcı veritabanlarında hello ana veritabanı için yapılandırılabilir. Veritabanı güvenlik duvarı kurallarını kullanarak, veritabanı kullanıcıları bağımsız faydalıdır. |
|[sys.database_firewall_rules (Azure SQL veritabanı)](/sql/relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database)|Microsoft Azure SQL veritabanı ile ilişkili hello veritabanı düzeyinde güvenlik duvarı ayarları hakkında bilgi verir. |
|[sp_delete_database_firewall_rule (Azure SQL veritabanı)](/sql/relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database)|Veritabanı düzeyi güvenlik duvarı ayarı, Azure SQL Database veya SQL Data Warehouse kaldırır. |


> [!TIP]
> Microsoft Windows üzerinde SQL Server Management Studio'yu kullanarak hızlı başlangıç öğreticisi için bkz: [Azure SQL Database: SQL Server Management Studio'yu kullanın tooconnect ve sorgu veri](sql-database-connect-query-ssms.md). Visual Studio Code hello macOS, Linux veya Windows üzerinde kullanarak bir hızlı başlangıç öğreticisi için bkz: [Azure SQL Database: kullanım Visual Studio Code tooconnect ve sorgu veri](sql-database-connect-query-vscode.md).

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-rest-api"></a>Azure SQL sunucuları, veritabanları ve güvenlik duvarları hello REST API kullanarak yönetme

toocreate ve Azure SQL server, veritabanları ve güvenlik duvarları hello REST API kullanarak yönetmek için bkz: [Azure SQL Database REST API'sini](/rest/api/sql/).

## <a name="next-steps"></a>Sonraki adımlar

- SQL esnek havuzu kullanarak veritabanlarını yoklaması hakkında toolearn bkz [esnek havuzlar](sql-database-elastic-pool.md).
- Hello Azure SQL veritabanı hizmetinin hakkında daha fazla bilgi için bkz: [SQL Database nedir?](sql-database-technical-overview.md).
- bir SQL Server veritabanı tooAzure geçirme hakkında toolearn bkz [tooAzure SQL veritabanı geçiş](sql-database-cloud-migrate.md).
- Desteklenen özellikler hakkında bilgi edinmek için bkz. [Özellikler](sql-database-features.md).
