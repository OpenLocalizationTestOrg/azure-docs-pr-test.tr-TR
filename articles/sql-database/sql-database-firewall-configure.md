---
title: "aaaAzure SQL veritabanı güvenlik duvarı kuralları | Microsoft Docs"
description: "Nasıl tooconfigure bir SQL veritabanı sunucusu ve veritabanı düzeyi güvenlik duvarı kuralları toomanage erişim güvenlik duvarıyla öğrenin."
keywords: "veritabanı güvenlik duvarı"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: ac57f84c-35c3-4975-9903-241c8059011e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 04/10/2017
ms.author: rickbyh
ms.openlocfilehash: 6a8cdf629d0d0e55421a5e9f9b894a21371be568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-server-level-and-database-level-firewall-rules"></a>Azure SQL veritabanı sunucusu ve veritabanı düzeyi güvenlik duvarı kuralları 

Microsoft Azure SQL Veritabanı, Azure ile diğer İnternet tabanlı uygulamalar için ilişkisel veritabanı hizmeti sunar. toohelp verilerinizi korumaya, hangi bilgisayarların izniniz belirtmediğiniz sürece tüm erişim tooyour veritabanı sunucusu güvenlik duvarları engellemek. Merhaba Güvenlik Duvarı'nı her istek IP adresi kaynaklanan hello üzerinde dayalı erişim toodatabases verir.

## <a name="overview"></a>Genel Bakış

Başlangıçta, tüm Transact-SQL tooyour Azure SQL Server'a erişim hello güvenlik duvarı tarafından engellendi. Azure SQL sunucunuzun toobegin tooyour Azure SQL Server'a erişim sağlayan bir veya daha fazla sunucu düzeyinde güvenlik duvarı kuralları belirtmeniz gerekir. Merhaba güvenlik duvarı kuralları toospecify Internet izin verilen hello hangi IP adres aralıkları ve Azure uygulamalarını tooconnect tooyour Azure SQL server olup deneyebilirsiniz kullanın.

tooselectively grant erişim toojust Azure SQL sunucunuza hello veritabanlarında biri, hello gerekli veritabanı için veritabanı düzeyi kuralı oluşturmanız gerekir. IP adresi aralığından hello sunucu düzeyinde güvenlik duvarı kuralında belirtilen ve hello istemcinin IP adresini hello hello veritabanı düzeyi kuralda belirtilen hello aralığında olduğundan emin olmak hello dışındadır hello veritabanı güvenlik duvarı kuralı için bir IP adresi aralığı belirtin.

Internet bağlantısı saldırılara karşı hello ve Azure SQL server veya SQL veritabanı ulaşabilir önce Azure ilk hello güvenlik duvarı üzerinden hello Aşağıdaki diyagramda gösterildiği gibi geçmesi gerekir:

   ![Güvenlik duvarı yapılandırmasını açıklayan diyagram.][1]

* **Sunucu düzeyinde güvenlik duvarı kuralları:** bu kurallar istemcileri tooaccess tüm Azure SQL server'ınızdaki etkinleştirmek için diğer bir deyişle, içindeki tüm hello veritabanları aynı mantıksal sunucu hello. Bu kurallar hello depolanan **ana** veritabanı. Sunucu düzeyinde güvenlik duvarı kuralları hello portalını kullanarak veya Transact-SQL deyimi kullanarak yapılandırılabilir. Hello Azure portal veya PowerShell kullanarak toocreate sunucu düzeyinde güvenlik duvarı kuralları hello abonelik sahibi veya abonelik Katılımcısı olması gerekir. toocreate Transact-SQL kullanarak sunucu düzeyinde güvenlik duvarı kuralı, toohello SQL veritabanı örneğinde hello sunucu düzeyinde asıl oturum açma veya (yani bir sunucu düzeyinde güvenlik duvarı kuralı önce oluşturulmalıdır hello Azure Active Directory yönetici olarak bağlamanız gerekir bir kullanıcı tarafından Azure düzeyi izinleri ile).
* **Veritabanı düzeyi güvenlik duvarı kuralları:** tooaccess istemcileri (güvenli) veritabanları hello içinde aynı belirli kurallar etkinleştirmek mantıksal sunucu. Her veritabanı için bu kurallar oluşturabilirsiniz (Merhaba dahil olmak üzere **ana** database0) ve hello tek tek veritabanlarında depolanır. Veritabanı düzeyinde güvenlik duvarı kuralları yalnızca Transact-SQL deyimi kullanarak yapılandırılabilir ve yalnızca yapılandırdıktan sonra ilk sunucu düzeyinde güvenlik duvarı hello. Merhaba sunucu düzeyinde güvenlik duvarı kuralında belirtilen dış hello aralığı hello veritabanı düzeyinde güvenlik duvarı kuralında bir IP adresi aralığı belirtirseniz, yalnızca hello veritabanı düzeyi aralığındaki IP adreslerine sahip istemciler hello veritabanına erişebilir. Bir veritabanı için en fazla 128 veritabanı düzeyinde güvenlik duvarı kuralınız olabilir. Ana ve kullanıcı veritabanları için veritabanı düzeyinde güvenlik duvarı kuralları yalnızca oluşturulur ve Transact-SQL yönetilir. Makale ve bakın hello örnekte daha sonra bu veritabanı düzeyinde güvenlik duvarı kuralları yapılandırma hakkında daha fazla bilgi için bkz [sp_set_database_firewall_rule (Azure SQL veritabanları)](https://msdn.microsoft.com/library/dn270010.aspx).

**Öneri:** Microsoft önerir veritabanı düzeyinde güvenlik duvarı kurallarını kullanarak her olası tooenhance güvenlik ve toomake veritabanınızı daha taşınabilir. Merhaba sahip birçok veritabanı varsa aynı erişim gereksinimlerini ve her veritabanı ayrı ayrı yapılandırma toospend zaman istemiyorsanız ve Yöneticiler için sunucu düzeyinde güvenlik duvarı kuralları kullanın.

> [!Note]
> İş sürekliliği hello bağlamda taşınabilir veritabanları hakkında daha fazla bilgi için bkz: [olağanüstü durum kurtarma için kimlik doğrulama gereksinimleri](sql-database-geo-replication-security-config.md).
>

### <a name="connecting-from-hello-internet"></a>Merhaba Internet ' bağlanma

Bir bilgisayar tooconnect tooyour veritabanı hello Internet sunucusundan denediğinde hello Güvenlik Duvarı'nı ilk IP adresi hello hello bağlantı isteğinde hello veritabanı için veritabanı düzeyinde güvenlik duvarı kuralları karşı hello isteğinin kaynaklandığı hello denetler:

* Başlangıç IP adresi hello isteğinin hello veritabanı düzeyinde güvenlik duvarı kurallarında belirtilen hello aralıkları biri içinde ise, hello bağlantı toohello hello kuralı içeren bir SQL veritabanında verilir.
* Başlangıç IP adresi hello isteğinin hello veritabanı düzeyinde güvenlik duvarı kuralında belirtilen hello aralıkları biri içinde değilse, hello sunucu düzeyinde güvenlik duvarı kuralları denetlenir. Başlangıç IP adresi hello isteğinin hello sunucu düzeyinde güvenlik duvarı kurallarında belirtilen hello aralıkları biri içinde ise, hello bağlantısı verilir. Sunucu düzeyinde güvenlik duvarı kuralları tooall SQL veritabanları hello Azure SQL server üzerinde uygulanır.  
* Başlangıç IP adresi hello isteğinin içinde değilse hello aralıkları hello veritabanı düzeyi hiçbirinde belirtilen veya sunucu düzeyinde güvenlik duvarı kuralları, hello bağlantı isteği başarısız olur.

> [!NOTE]
> tooaccess Azure SQL veritabanı, yerel bilgisayarınızdan olun ağ ve yerel bilgisayar hello güvenlik duvarının TCP bağlantı noktası 1433 giden iletişime olanak sağlar.
> 

### <a name="connecting-from-azure"></a>Azure'dan bağlanma
Azure tooconnect tooyour Azure SQL server'ı Azure bağlantıları tooallow uygulamalardan etkinleştirilmesi gerekir. Tooconnect tooyour veritabanı sunucusu bir uygulamadan Azure girişiminde bulunduğunda hello Güvenlik Duvarı'nı Azure bağlantılarına izin verildiğini doğrular. Başlangıç ve bitiş adresi eşit too0.0.0.0 ile ayarlama Güvenlik Duvarı'nı bu bağlantılarına izin verilip verilmeyeceğini belirtir. Merhaba bağlantı denemesi izin verilmiyorsa hello isteği hello Azure SQL Database sunucusu ulaşmaz.

> [!IMPORTANT]
> Bu seçenek, diğer müşterilerden hello abonelikleri Azure dahil olmak üzere bağlantılarından gelen tüm bağlantıları hello güvenlik duvarı tooallow yapılandırır. Yetkili kullanıcıların ne zaman bu seçeneğin belirlenmesi ve emin olun, oturum açma kullanıcı izinlerini erişim tooonly sınırlayın.
> 

## <a name="creating-and-managing-firewall-rules"></a>Güvenlik duvarı kuralları oluşturmayı ve yönetmeyi
Merhaba ilk sunucu düzeyinde güvenlik duvarı ayarı hello kullanılarak oluşturulabilir [Azure portal](https://portal.azure.com/) veya program aracılığıyla kullanarak [Azure PowerShell](https://msdn.microsoft.com/library/azure/dn546724.aspx), [Azure CLI](/cli/azure/sql/server/firewall-rule#create), veya hello [REST API](https://msdn.microsoft.com/library/azure/dn505712.aspx). Sunucu düzeyinde sonraki güvenlik duvarı kuralları ise bu yöntemler kullanılarak ve Transact-SQL aracılığıyla oluşturulup yönetilebilir. 

> [!IMPORTANT]
> Veritabanı düzeyinde güvenlik duvarı kuralları yalnızca oluşturulabilir ve Transact-SQL kullanılarak yönetilebilir. 
>

tooimprove performans, sunucu düzeyinde güvenlik duvarı kuralları hello veritabanı düzeyinde geçici olarak önbelleğe alınır. toorefresh hello önbellek, bkz: [DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx). 

> [!TIP]
> Kullanabileceğiniz [SQL veritabanı denetimi](sql-database-auditing.md) tooaudit sunucu ve veritabanı düzeyi güvenlik duvarı değişikliklerinin.
>

### <a name="azure-portal"></a>Azure portalına

tooset bir sunucu düzeyinde güvenlik duvarı kuralı hello Azure portal, Azure veritabanı mantıksal sunucunuz için Azure SQL veritabanı veya hello genel bakış sayfasında ya da toohello Genel Bakış sayfasına gidebilirsiniz.

> [!TIP]
> Bir öğretici için bkz: [hello Azure portal oluşturma bir DB kullanarak](sql-database-get-started-portal.md).
>

**Veritabanı genel bakış sayfasında**

1. tooset hello veritabanı genel bakış sayfasında, sunucu düzeyinde güvenlik duvarı kural'ı tıklatın **ayarlayın sunucu Güvenlik Duvarı** hello görüntü aşağıdaki gösterildiği gibi hello araç çubuğunda: Merhaba **Güvenlik Duvarı ayarları** hello SQL için sayfası Veritabanı sunucusu açar.

      ![sunucu güvenlik duvarı kuralı](./media/sql-database-get-started-portal/server-firewall-rule.png) 

2. Tıklatın **istemci IP'si Ekle** hello bilgisayarın hello araç tooadd hello IP adresine kullanmakta olduğunuz ve ardından **kaydetmek**. Geçerli IP adresiniz için bir sunucu düzeyi güvenlik duvarı kuralı oluşturulur.

      ![sunucu güvenlik duvarı kuralı ayarla](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

**Server genel bakış sayfasında**

Merhaba hello tam olarak gösteren, sunucu açılır genel bakış sayfasında tam sunucu adını (gibi **mynewserver20170403.database.windows.net**) ve diğer yapılandırmalar için seçenekler sağlar.

1. tooset server genel bakış sayfasında, sunucu düzeyi kuraldan tıklatın **Güvenlik Duvarı** görüntü aşağıdaki hello gösterdi gibi ayarları altında hello sol menüde: 

     ![mantıksal sunucusuna genel bakış](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. Tıklatın **istemci IP'si Ekle** hello bilgisayarın hello araç tooadd hello IP adresine kullanmakta olduğunuz ve ardından **kaydetmek**. Geçerli IP adresiniz için bir sunucu düzeyi güvenlik duvarı kuralı oluşturulur.

     ![sunucu güvenlik duvarı kuralı ayarla](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

### <a name="transact-sql"></a>Transact-SQL
| Katalog Görünümü veya Saklı Yordam | Düzey | Açıklama |
| --- | --- | --- |
| [sys.firewall_rules](https://msdn.microsoft.com/library/dn269980.aspx) |Sunucu |Merhaba geçerli sunucu düzeyinde güvenlik duvarı kurallarını görüntüler |
| [sp_set_firewall_rule](https://msdn.microsoft.com/library/dn270017.aspx) |Sunucu |Sunucu düzeyinde güvenlik duvarı kuralları oluşturur veya güncelleştirir |
| [sp_delete_firewall_rule](https://msdn.microsoft.com/library/dn270024.aspx) |Sunucu |Sunucu düzeyinde güvenlik duvarı kurallarını kaldırır |
| [sys.database_firewall_rules](https://msdn.microsoft.com/library/dn269982.aspx) |Database |Merhaba geçerli veritabanı düzeyinde güvenlik duvarı kurallarını görüntüler |
| [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) |Database |Oluşturur veya güncelleştirir hello veritabanı düzeyinde güvenlik duvarı kuralları |
| [sp_delete_database_firewall_rule](https://msdn.microsoft.com/library/dn270030.aspx) |Veritabanları |Veritabanı düzeyinde güvenlik duvarı kurallarını kaldırır |


Merhaba aşağıdaki örneklerde hello varolan kuralları gözden geçirin, bir IP adresi aralığı Contoso hello sunucuda etkinleştirmek ve bir güvenlik duvarı kuralını siler:
   
```sql
SELECT * FROM sys.firewall_rules ORDER BY name;
```
  
Daha sonra bir güvenlik duvarı kuralı ekleyin.
   
```sql
EXECUTE sp_set_firewall_rule @name = N'ContosoFirewallRule',
   @start_ip_address = '192.168.1.1', @end_ip_address = '192.168.1.10'
```

toodelete bir sunucu düzeyinde güvenlik duvarı kuralı hello sp_delete_firewall_rule saklı yordamını yürütün. Merhaba aşağıdaki örnek ContosoFirewallRule adlı hello kuralını siler:
   
```sql
EXECUTE sp_delete_firewall_rule @name = N'ContosoFirewallRule'
```   

### <a name="azure-powershell"></a>Azure PowerShell
| Cmdlet | Düzey | Açıklama |
| --- | --- | --- |
| [Get-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546731.aspx) |Sunucu |Merhaba geçerli sunucu düzeyinde güvenlik duvarı kurallarını döndürür |
| [New-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546724.aspx) |Sunucu |Sunucu düzeyinde yeni bir güvenlik duvarı kuralı oluşturur |
| [Set-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546739.aspx) |Sunucu |Mevcut bir sunucu düzeyinde güvenlik duvarı kuralı Hello özelliklerini güncelleştirir |
| [Remove-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546727.aspx) |Sunucu |Sunucu düzeyinde güvenlik duvarı kurallarını kaldırır |


Aşağıdaki örnek hello PowerShell kullanarak bir sunucu düzeyinde güvenlik duvarı kuralı ayarlar:

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
```

> [!TIP]
> PowerShell ilişkin örnekler için hızlı başlangıç hello bağlamda bkz [oluşturma DB - PowerShell](sql-database-get-started-powershell.md) ve [tek bir veritabanı oluşturabilirsiniz ve PowerShell kullanarak bir güvenlik duvarı kuralı yapılandırma](scripts/sql-database-create-and-configure-database-powershell.md)
>

### <a name="azure-cli"></a>Azure CLI
| Cmdlet | Düzey | Açıklama |
| --- | --- | --- |
| [az sql server güvenlik duvarı oluşturma](/cli/azure/sql/server/firewall-rule#create) | Merhaba girilen IP adresi aralığından hello sunucusunda bir güvenlik duvarı kuralı tooallow erişim tooall SQL veritabanları oluşturur.|
| [az sql server güvenlik duvarı Sil](/cli/azure/sql/server/firewall-rule#delete)| Bir güvenlik duvarı kuralını siler.|
| [az sql server güvenlik duvarı listesi](/cli/azure/sql/server/firewall-rule#list)| Merhaba güvenlik duvarı kuralları listeler.|
| [az sql server güvenlik duvarı kuralı Göster](/cli/azure/sql/server/firewall-rule#show)| Bir güvenlik duvarı kuralı Hello ayrıntılarını gösterir.|
| [SQL server güvenlik duvarı kuralı güncelleştirmesi ax](/cli/azure/sql/server/firewall-rule#update)| Bir güvenlik duvarı kuralı güncelleştirir.

Aşağıdaki örnek hello hello Azure CLI kullanarak bir sunucu düzeyinde güvenlik duvarı kuralı ayarlar: 

```azurecli-interactive
az sql server firewall-rule create --resource-group myResourceGroup --server $servername \
    -n AllowYourIp --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0
```

> [!TIP]
> Bir Azure CLI örneği hızlı bir başlangıç için hello bağlamda bkz [oluşturma Çiftazalanbakiye - Azure CLI](sql-database-get-started-cli.md) ve [tek bir veritabanı oluşturabilirsiniz ve hello Azure CLI kullanarak bir güvenlik duvarı kuralı yapılandırma](scripts/sql-database-create-and-configure-database-cli.md)
>

### <a name="rest-api"></a>REST API
| API | Düzey | Açıklama |
| --- | --- | --- |
| [Güvenlik Duvarı Kurallarını Listele](https://msdn.microsoft.com/library/azure/dn505715.aspx) |Sunucu |Merhaba geçerli sunucu düzeyinde güvenlik duvarı kurallarını görüntüler |
| [Güvenlik Duvarı Kuralı Oluştur](https://msdn.microsoft.com/library/azure/dn505712.aspx) |Sunucu |Sunucu düzeyinde güvenlik duvarı kuralları oluşturur veya güncelleştirir |
| [Güvenlik Duvarı Kuralı Ayarla](https://msdn.microsoft.com/library/azure/dn505707.aspx) |Sunucu |Mevcut bir sunucu düzeyinde güvenlik duvarı kuralı Hello özelliklerini güncelleştirir |
| [Güvenlik Duvarı Kuralını Sil](https://msdn.microsoft.com/library/azure/dn505706.aspx) |Sunucu |Sunucu düzeyinde güvenlik duvarı kurallarını kaldırır |

## <a name="server-level-firewall-rule-versus-a-database-level-firewall-rule"></a>Sunucu düzeyinde güvenlik duvarı kuralı veritabanı düzeyinde güvenlik duvarı kuralı karşılaştırması
Q. Bir veritabanının kullanıcıları başka bir veritabanından tamamen yalıtılmış olması gerekiyor mu?   
  Yanıt Evet ise, veritabanı düzeyinde güvenlik duvarı kurallarını kullanarak erişim izni. Bu, savunma hello derinliğini azaltma tooall veritabanları hello güvenlik duvarı üzerinden erişime sunucu düzeyinde güvenlik duvarı kurallarını kullanarak önler.   
 
Q. Başlangıç IP adresi'nın kullanıcılar tooall veritabanlarına erişim?   
  Sunucu düzeyinde güvenlik duvarı kuralları tooreduce hello sayısı güvenlik duvarı kuralları yapılandırmalısınız kullanın.   

Q. Hello kişi ya da yalnızca hello güvenlik duvarı kuralları yapılandırma takım aracılığıyla Azure portalı, PowerShell hello veya REST API hello erişimi var mı?   
  Sunucu düzeyinde güvenlik duvarı kuralları kullanmanız gerekir. Veritabanı düzeyinde güvenlik duvarı kuralları yalnızca Transact-SQL kullanılarak yapılandırılabilir.  

Q. Merhaba kişi veya hello güvenlik duvarı kuralları yapılandırma takım hello veritabanı düzeyinde üst düzey iznine sahip yasaklanmış?   
  Sunucu düzeyinde güvenlik duvarı kurallarını kullanın. Transact-SQL kullanarak veritabanı düzeyinde güvenlik duvarı kuralları yapılandırma en azından `CONTROL DATABASE` hello veritabanı düzeyinde izni.  

Q. Hello kişi yapılandırma veya hello güvenlik duvarı kuralları, Denetim takım güvenlik duvarı kuralları çoğu için merkezi olarak yönetmek mi (belki de 100s) veritabanlarının?   
  Bu seçim, gereksinimleri ve ortam bağlıdır. Sunucu düzeyinde güvenlik duvarı kuralları daha kolay tooconfigure olabilir, ancak komut dosyası kuralları veritabanı düzeyi hello yapılandırabilirsiniz. Ve sunucu düzeyinde güvenlik duvarı kuralları kullansanız bile, tooaudit hello veritabanı güvenlik duvarı kuralları, toosee gerekebilir kullanıcılarla `CONTROL` izni hello veritabanında veritabanı düzeyinde güvenlik duvarı kuralları oluşturdunuz.   

Q. Her iki sunucu ve veritabanı düzeyi güvenlik duvarı kuralları bir karışımını kullanabilir miyim?   
  Evet. Yöneticiler gibi bazı kullanıcıların sunucu düzeyinde güvenlik duvarı kuralları gerekebilir. Kullanıcıların bir veritabanı uygulamasının gibi diğer kullanıcıların veritabanı düzeyinde güvenlik duvarı kuralları gerekebilir.   

## <a name="troubleshooting-hello-database-firewall"></a>Merhaba veritabanı güvenlik duvarı sorunlarını giderme
Merhaba beklediğiniz gibi erişim toohello Microsoft Azure SQL veritabanı hizmetinin davranıyor değil, aşağıdaki noktaları göz önünde bulundurun:

* **Yerel güvenlik duvarı yapılandırmasını:** bilgisayarınızı Azure SQL veritabanı erişmeden önce TCP bağlantı noktası 1433 için bilgisayarınızda toocreate bir güvenlik duvarı özel durumu gerekebilir. Hello Azure bulut sınır içinde bağlantıları yapıyorsanız, tooopen ek bağlantı noktaları olabilir. Merhaba daha fazla bilgi için bkz **SQL Database: içinde vs dışındaki** bölümünü [ADO.NET 4.5 ve SQL veritabanı için 1433 dışındaki bağlantı noktaları](sql-database-develop-direct-route-ports-adonet-v12.md).
* **Ağ adresi çevirisi (NAT):** son tooNAT, SQL veritabanı, bilgisayar IP yapılandırma ayarları'nda gösterilen başlangıç IP adresi farklı, bilgisayar tooconnect tooAzure tarafından kullanılan başlangıç IP adresi. Bilgisayarınız tooview başlangıç IP adresi tooconnect tooAzure kullanarak toohello Portalı'nda oturum açın ve toohello gidin **yapılandırma** veritabanınızı barındıran hello sunucu sekmesinde. Merhaba altında **izin verilen IP adreslerini** hello bölümünde **geçerli istemci IP adresi** görüntülenir. Tıklatın **Ekle** toohello **izin verilen IP adreslerini** tooallow bu bilgisayar tooaccess hello sunucusu.
* **Değişiklikleri toohello izin verilenler listesine etkili olmamıştır değil:** için beş dakikalık bir gecikmeyle toohello Azure SQL veritabanı güvenlik duvarı yapılandırması tootake etkili değişiklikler kadar olabilir.
* **Merhaba oturum açma yetkisi yok veya hatalı bir parolanın kullanıldı:** bir oturum açma izinleri hello Azure SQL veritabanı sunucusunda yok veya kullanılan hello parola yanlış hello bağlantı toohello Azure SQL veritabanı sunucusu reddedildi. Bir güvenlik duvarı ayarı oluşturma istemciler yalnızca bir fırsat tooattempt tooyour sunucusuyla bağlantı kuruluyor sağlar; her istemci hello gerekli güvenlik kimlik bilgilerini sağlamanız gerekir. Oturumları hazırlama hakkında daha fazla bilgi için bkz. Azure SQL Veritabanında Veritabanı, Oturum ve Kullanıcıları Yönetme.
* **Dinamik IP adresi:** dinamik IP adresleme ile Internet bağlantınız varsa ve hello güvenlik duvarı üzerinden alma sorun yaşıyorsanız, çözümleri aşağıdaki hello birini deneyebilirsiniz:
  
  * Başlangıç IP adresi aralığı, Internet servis sağlayıcısı (ISS) erişim hello Azure SQL veritabanı sunucusunu tooyour istemci bilgisayarlara atanan isteyin ve sonra başlangıç IP adresi aralığı bir güvenlik duvarı kuralı ekleyin.
  * Statik IP bunun yerine istemci bilgisayarlarınız için adresleme alın ve ardından güvenlik duvarı kuralları hello IP adreslerini ekleyin.

## <a name="next-steps"></a>Sonraki adımlar

- Hızlı bir başlangıç bir veritabanı ve sunucu düzeyinde güvenlik duvarı kuralı oluşturma hakkında bilgi için bkz: [bir Azure SQL veritabanı oluşturma](sql-database-get-started-portal.md).
- Açık kaynak ya da üçüncü taraf uygulamalar bağlanan tooan Azure SQL veritabanında Yardım için bkz. [istemcisi hızlı başlangıç kod örnekleri tooSQL veritabanı](https://msdn.microsoft.com/library/azure/ee336282.aspx).
- Merhaba tooopen gerekebilir ek bağlantı noktaları hakkında bilgi için bkz: **SQL veritabanı: içinde vs dışındaki** bölümünü [ADO.NET 4.5 ve SQL veritabanı için 1433 dışındaki bağlantı noktaları](sql-database-develop-direct-route-ports-adonet-v12.md)
- Azure SQL Database güvenliğine genel bakış için bkz: [veritabanınızın güvenliğini sağlama](sql-database-security-overview.md)

<!--Image references-->
[1]: ./media/sql-database-firewall-configure/sqldb-firewall-1.png
