---
title: "bir Azure SQL veritabanı aaaCopy | Microsoft Docs"
description: "Bir Azure SQL veritabanının bir kopyasını oluşturun"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5aaf6bcd-3839-49b5-8c77-cbdf786e359b
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 64a297d819d6da89600fda60abe8394ae405abfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-an-azure-sql-database"></a>Bir Azure SQL veritabanını kopyalama

Azure SQL veritabanı sağlar var olan bir Azure SQL işlemsel olarak tutarlı bir kopyasını oluşturmak için çeşitli yöntemler veritabanı üzerinde ya da hello aynı sunucu veya farklı bir sunucu. Hello Azure portal, PowerShell veya T-SQL kullanarak bir SQL veritabanı kopyalayabilirsiniz. 

## <a name="overview"></a>Genel Bakış

Bir veritabanı kopyası hello kopya isteğini hello süresini itibariyle hello kaynak veritabanı anlık görüntüsüdür. Seçebileceğiniz hello aynı sunucuya veya farklı bir sunucu, hizmet katmanını ve performans düzeyini veya hello içindeki farklı performans düzeyi aynı hizmet Katmanı (sürüm). Merhaba kopyalama işlemi tamamlandıktan sonra tam olarak işlevsel, bağımsız bir veritabanı haline gelir. Bu noktada, yükseltme veya tooany edition düşürmek. Merhaba oturumlar, kullanıcılar ve izinler bağımsız olarak yönetilebilir.  

## <a name="logins-in-hello-database-copy"></a>Merhaba veritabanı kopyası oturumlar

Bir veritabanı toohello kopyaladığınızda aynı mantıksal sunucu, hello aynı oturum açma bilgileri hem veritabanlarında kullanılabilir. Merhaba güvenlik sorumlusu toocopy hello veritabanını kullanmak hello yeni veritabanı üzerinde hello veritabanı sahibi olur. Tüm veritabanı kullanıcıları, izinlerini ve bunların güvenlik tanımlayıcılarını (SID'ler) olan toohello veritabanı kopyası kopyalanır.  

Veritabanı tooa farklı bir mantıksal sunucu kopyaladığınızda, hello yeni sunucuda hello sorumlunun hello yeni veritabanı üzerinde hello veritabanı sahibi olur. Kullanırsanız [bulunan veritabanı kullanıcıları](sql-database-manage-logins.md) veri erişimi için hem birincil hello ve ikincil veritabanları her zaman hello kopyalama tamamlandıktan sonra tamamlamanız için aynı kullanıcı kimlik bilgileri, hemen erişebilir hello içerdiğinden emin olun ile Merhaba aynı kimlik bilgileri. 

Kullanırsanız [Azure Active Directory](../active-directory/active-directory-whatis.md), tamamen hello kopyalama kimlik bilgilerini yönetmek için hello gerekliliğini ortadan kaldırabilir. Merhaba veritabanı tooa yeni sunucu kopyaladığınızda, hello oturumları hello yeni sunucuda bulunmadığı için ancak hello oturum açma tabanlı erişim, çalışmayabilir. Veritabanı tooa farklı bir mantıksal sunucu, kopyaladığınızda oturumları yönetme hakkında toolearn bkz [nasıl toomanage Azure SQL veritabanı güvenlik olağanüstü durum kurtarma işleminden sonra](sql-database-geo-replication-security-config.md). 

Merhaba kopyalama başarılı olduktan sonra ve diğer kullanıcıların eşleştirilir önce yalnızca hello hello veritabanı sahibi'hello kopyalama, başlatılan oturum açma toohello yeni veritabanı oturum açabilir. bkz: hello işlemi kopyalama tamamlandıktan sonra tooresolve oturumları [gidermek oturumları](#resolve-logins).

## <a name="copy-a-database-by-using-hello-azure-portal"></a>Hello Azure portal kullanarak bir veritabanını kopyalama

kullanarak bir veritabanı Azure portalı, veritabanınızın, açık hello sayfasında hello ve ardından toocopy **kopya**. 

   ![Veritabanı kopyalama](./media/sql-database-copy/database-copy.png)

## <a name="copy-a-database-by-using-powershell"></a>PowerShell kullanarak bir veritabanını kopyalama

toocopy PowerShell, kullanım hello kullanarak bir veritabanı [yeni AzureRmSqlDatabaseCopy](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) cmdlet'i. 

```PowerShell
New-AzureRmSqlDatabaseCopy -ResourceGroupName "myResourceGroup" `
    -ServerName $sourceserver `
    -DatabaseName "MySampleDatabase" `
    -CopyResourceGroupName "myResourceGroup" `
    -CopyServerName $targetserver `
    -CopyDatabaseName "CopyOfMySampleDatabase"
```

Bir tam örnek betik için bkz: [veritabanı tooa yeni bir sunucu kopyalama](scripts/sql-database-copy-database-to-new-server-powershell.md).

## <a name="copy-a-database-by-using-transact-sql"></a>Transact-SQL kullanarak bir veritabanını kopyalama

Toohello asıl veritabanı hello sunucu düzeyinde asıl oturum açma veya toocopy istediğiniz hello veritabanı oluşturulan hello oturum açma ile oturum açın. Toosucceed kopyalama veritabanı için hello sunucu düzeyinde sorumlu olmayan oturumlar hello dbmanager rolünün üyeleri olmalıdır. Oturum açma bilgileri ve bağlantı toohello sunucusu hakkında daha fazla bilgi için bkz: [oturumları yönetme](sql-database-manage-logins.md).

Merhaba ile Merhaba kaynak veritabanı kopyalama işlemini başlatmak [CREATE DATABASE](https://msdn.microsoft.com/library/ms176061.aspx) deyimi. Bu deyimi yürütme hello veritabanı kopyalama işlemi başlatır. Veritabanı kopyalama zaman uyumsuz bir işlem olduğundan, veritabanı hello kopyalama tamamlanmadan önce hello CREATE DATABASE deyimi döndürür.

### <a name="copy-a-sql-database-toohello-same-server"></a>Bir SQL veritabanı toohello kopyalamak aynı sunucu
Toohello asıl veritabanı hello sunucu düzeyinde asıl oturum açma veya toocopy istediğiniz hello veritabanı oluşturulan hello oturum açma ile oturum açın. Toosucceed kopyalama veritabanı için hello sunucu düzeyinde sorumlu olmayan oturumlar hello dbmanager rolünün üyeleri olmalıdır.

Bu komut Database1 tooa yeni veritabanı üzerinde hello Database2 adlı kopyalar aynı sunucu. Veritabanınızı Hello boyutuna bağlı olarak, bazı zaman toocomplete işlemi kopyalama hello alabilir.

    -- Execute on hello master database.
    -- Start copying.
    CREATE DATABASE Database1_copy AS COPY OF Database1;

### <a name="copy-a-sql-database-tooa-different-server"></a>Bir SQL veritabanı tooa farklı sunucusuna kopyalayın

Toohello asıl veritabanı hello hedef sunucunun, hello yeni veritabanı oluşturulan toobe olduğu hello SQL veritabanı sunucusuna oturum açın. Aynı adı ve parola hello veritabanı hello kaynak SQL veritabanı sunucusundaki hello kaynak veritabanının sahibi olarak hello sahip bir oturum açma kullanın. Hello oturum açma hello hedef sunucuda da hello dbmanager rolünün bir üyesi olmanız veya hello sunucu düzeyinde asıl oturum açmayı olması gerekir.

Bu komut Database1 Database2 Sunucu2'adlı Sunucu1 tooa yeni veritabanı üzerinde kopyalar. Veritabanınızı Hello boyutuna bağlı olarak, bazı zaman toocomplete işlemi kopyalama hello alabilir.

    -- Execute on hello master database of hello target server (server2)
    -- Start copying from Server1 tooServer2
    CREATE DATABASE Database1_copy AS COPY OF server1.Database1;


### <a name="monitor-hello-progress-of-hello-copying-operation"></a>Kopyalama işlemi hello Hello ilerlemesini izlemek

Merhaba sys.databases ve sys.dm_database_copies görünümleri sorgulayarak Hello kopyalama işlemini izleyin. Merhaba kopyalama işlemi sürerken hello **state_desc** hello sys.databases görünümünün hello yeni veritabanı için sütunu olarak ayarlanmış çok**kopyalama**.

* Merhaba kopyalama başarısız olursa, hello **state_desc** hello sys.databases görünümünün hello yeni veritabanı için sütunu olarak ayarlanmış çok**ŞÜPHELENİYORSANIZ**. Yeni bir veritabanı hello üzerinde Hello DROP deyimi yürütün ve daha sonra yeniden deneyin.
* Merhaba kopyalama, hello başarılı olursa **state_desc** hello sys.databases görünümünün hello yeni veritabanı için sütunu olarak ayarlanmış çok**çevrimiçi**. Merhaba kopyalama tamamlandıktan ve hello yeni veritabanı hello kaynak veritabanı bağımsız olarak değiştirilebilir normal bir veritabanıdır.

> [!NOTE]
> Merhaba devam ederken toocancel hello kopyalama karar verirseniz, yürütme [DROP DATABASE](https://msdn.microsoft.com/library/ms178613.aspx) deyimi hello yeni veritabanı üzerinde. Alternatif olarak, hello kaynak veritabanında hello DROP DATABASE deyimi yürütme ayrıca hello kopyalama işlemini iptal eder.
> 

## <a name="resolve-logins"></a>Oturum açma bilgileri çözümleyin

Merhaba yeni veritabanı hello hedef sunucuda çevrimiçi olduktan sonra hello kullan [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) deyimi tooremap hello hello kullanıcılardan yeni toologins hello hedef sunucuda veritabanı. yalnız bırakılmış tooresolve kullanıcıları, bakın [sahipsiz kullanıcıların sorun giderme](https://msdn.microsoft.com/library/ms175475.aspx). Ayrıca bkz. [nasıl toomanage Azure SQL veritabanı güvenlik olağanüstü durum kurtarma işleminden sonra](sql-database-geo-replication-security-config.md).

Merhaba yeni veritabanındaki tüm kullanıcılar sahip oldukları hello kaynak veritabanında hello izinlerini korur. Merhaba veritabanı kopyası başlatan hello kullanıcı hello yeni veritabanının hello veritabanı sahibi olur ve yeni bir güvenlik tanımlayıcısı (SID) atanır. Merhaba kopyalama başarılı olduktan sonra ve diğer kullanıcıların eşleştirilir önce yalnızca hello hello veritabanı sahibi'hello kopyalama, başlatılan oturum açma toohello yeni veritabanı oturum açabilir.

Veritabanı tooa farklı bir mantıksal sunucu, kopyaladığınızda, kullanıcıları ve oturum açma bilgileri yönetmeyle ilgili toolearn bkz [nasıl toomanage Azure SQL veritabanı güvenlik olağanüstü durum kurtarma işleminden sonra](sql-database-geo-replication-security-config.md).

## <a name="next-steps"></a>Sonraki adımlar

* Oturum açma bilgileri hakkında daha fazla bilgi için bkz: [oturumları yönetme](sql-database-manage-logins.md) ve [nasıl toomanage Azure SQL veritabanı güvenlik olağanüstü durum kurtarma işleminden sonra](sql-database-geo-replication-security-config.md).
* tooexport bir veritabanı bkz [hello veritabanı tooa BACPAC verme](sql-database-export.md).
