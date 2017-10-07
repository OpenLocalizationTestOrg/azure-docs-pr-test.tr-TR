---
title: "Azure PowerShell: SQL veritabanı oluşturma | Microsoft Docs"
description: "Azure portal toocreate SQL Database mantıksal sunucusu, sunucu düzeyinde güvenlik duvarı kuralı ve veritabanlarında nasıl hello öğrenin."
keywords: "sql veritabanı öğreticisi, sql veritabanı oluşturma"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PowerShell
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: e89f68b44083a3b64e61f95117dbbedfa6647ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-powershell"></a>PowerShell kullanarak tek Azure SQL veritabanı oluşturma

PowerShell kullanılan toocreate olan ve hello komut satırından veya komut dosyalarında Azure kaynaklarını yönetin. Bir Azure SQL veritabanında bu kılavuzu kullanarak PowerShell toodeploy ayrıntılarını bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) içinde bir [Azure SQL Database mantıksal sunucusu](sql-database-features.md).

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz](https://azure.microsoft.com/free/) bir hesap oluşturun.

Bu öğretici hello Azure PowerShell modülü sürüm 4.0 veya üstünü gerektirir. Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps). 

## <a name="log-in-tooazure"></a>İçinde tooAzure oturum

İçinde tooyour Azure aboneliği hello kullanarak oturum [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) komut ve hello ekrandaki yönergeleri izleyin.

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a>Değişken oluşturma

Bu hızlı başlangıç hello komut içinde kullanmak için değişkenleri tanımlayın.

```powershell
# hello data center and resource name for your resources
$resourcegroupname = "myResourceGroup"
$location = "WestEurope"
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
$servername = "server-$(Get-Random)"
# Set an admin login and password for your database
# hello login information for hello server
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# hello ip address range that you want tooallow tooaccess your server - change as appropriate
$startip = "0.0.0.0"
$endip = "0.0.0.0"
# hello database name
$databasename = "mySampleDatabase"
```

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Oluşturma bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) hello kullanarak [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) komutu. Kaynak grubu, Azure kaynaklarının grup olarak dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `westeurope` konumu.

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a>Mantıksal sunucu oluşturma

Oluşturma bir [Azure SQL Database mantıksal sunucusu](sql-database-features.md) hello kullanarak [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) komutu. Mantıksal sunucu, grup olarak yönetilen bir veritabanı grubu içerir. Merhaba aşağıdaki örnek rastgele adlandırılmış bir sunucu, kaynak grubunda adlı bir yönetici oturum açma ile oluşturur `ServerAdmin` ve bir parola `ChangeYourAdminPassword1`. Bu önceden tanımlı değerleri istediğiniz gibi değiştirin.

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a>Sunucu güvenlik duvarı kurallarını yapılandırma

Oluşturma bir [Azure SQL veritabanı sunucu düzeyinde güvenlik duvarı kuralı](sql-database-firewall-configure.md) hello kullanarak [yeni AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) komutu. Sunucu düzeyinde güvenlik duvarı kuralı SQL Server Management Studio veya hello SQLCMD yardımcı programını tooconnect tooa SQL veritabanı gibi hello SQL Database hizmeti güvenlik duvarı üzerinden bir dış uygulamaya verir. Aşağıdaki örneğine hello hello Güvenlik Duvarı'nı yalnızca diğer Azure kaynakları için açıldı. tooenable harici bağlantı, başlangıç IP adresi tooan uygun adresini Değiştir ortamınız için. tooopen tüm IP adresleri hello bitiş adresi başlangıç IP adresi ve 255.255.255.255 hello olarak 0.0.0.0 kullanın.

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> SQL Veritabanı 1433 numaralı bağlantı noktası üzerinden iletişim kurar. Bir şirket ağından gelen tooconnect çalışıyorsanız, bağlantı noktası 1433 üzerinden giden trafik, ağınızın güvenlik duvarı tarafından izin verilmiyor. Öyleyse, BT departmanınızın 1433 numaralı bağlantı noktasını açar sürece mümkün tooconnect tooyour Azure SQL veritabanı sunucusu olmaz.
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a>Merhaba sunucu örnek verilerle bir veritabanı oluşturun

Bir veritabanı oluşturmak bir [S0 performans düzeyi](sql-database-service-tiers.md) hello kullanarak hello Server'daki [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) komutu. Merhaba aşağıdaki örnek adlı bir veritabanı oluşturur `mySampleDatabase` ve bu veritabanına yükleri hello AdventureWorksLT örnek verileri. Bu önceden tanımlanmış Değiştir istendiği gibi (Bu koleksiyonu yapıda Bu hızlı başlangıç hello değerleri bağlı diğer hızlı başlar) değerleri.

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a>Kaynakları temizleme

Bu koleksiyondaki diğer hızlı başlangıçlar, bu hızlı başlangıca göre belirlenir. 

> [!TIP]
> Sonraki hızlı başlangıçlar ile toowork üzerinde toocontinue planlıyorsanız, temiz oluşturulan bu hızlı başlangıç kaynakları başlatılmaz. Toocontinue düşünmüyorsanız bu hızlı başlangıç bölümünde hello Azure portal tarafından oluşturulan tüm kaynakları adımları toodelete aşağıdaki hello kullanın.
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Sonraki adımlar

Artık bir veritabanınız olduğuna göre, sık kullandığınız araçlarla bağlanabilir ve sorgulayabilirsiniz. Aşağıdan aracınızı seçerek daha fazla bilgi edinin:

- [SQL Server Management Studio](sql-database-connect-query-ssms.md)
- [Visual Studio Code](sql-database-connect-query-vscode.md)
- [.NET](sql-database-connect-query-dotnet.md)
- [PHP](sql-database-connect-query-php.md)
- [Node.js](sql-database-connect-query-nodejs.md)
- [Java](sql-database-connect-query-java.md)
- [Python](sql-database-connect-query-python.md)
- [Ruby](sql-database-connect-query-ruby.md)

