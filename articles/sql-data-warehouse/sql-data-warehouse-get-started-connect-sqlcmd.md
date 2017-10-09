---
title: aaaConnect tooAzure SQL Data Warehouse sqlcmd | Microsoft Docs
description: "[Sqlcmd] [sqlcmd] komut satırı yardımcı programını tooconnect tooand sorgu Azure SQL Data Warehouse kullanın."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 6e2b69e5-4806-4e91-9ea1-e2b63bf28c46
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 0334df7b969da1966ba29c97f835a2dc9e383e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sqlcmd"></a>Sqlcmd ile tooSQL veri ambarına bağlanma
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Kullanım [sqlcmd] [ sqlcmd] komut satırı yardımcı programını tooconnect tooand Azure SQL Data Warehouse sorgu.  

## <a name="1-connect"></a>1. Bağlan
tooget Başlarken [sqlcmd][sqlcmd], hello komut istemi açın ve girin **sqlcmd** hello bağlantı dizesi SQL Data Warehouse veritabanınız için izlediği. Merhaba bağlantı dizesi şu parametreler hello gerektirir:

* **Sunucu (-S):** sunucusuna hello biçiminde `<`sunucu adı`>`. database.windows.net
* **Database (-d):** Veritabanı adı.
* **Quoted Identifiers (-ı):** Quoted tanımlayıcıları etkin tooconnect tooa SQL Data Warehouse örneğine olması gerekir.

SQL Server kimlik doğrulaması toouse, tooadd hello kullanıcı adı/parola parametrelerini gerekir:

* **Kullanıcı (-U):** hello biçimindeki sunucu kullanıcısı `<`kullanıcı`>`
* **Parola (-P):** hello kullanıcıyla ilişkili parola.

Örneğin, bağlantı dizenizi hello şuna benzeyebilir:

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

toouse Azure Active Directory tümleşik kimlik doğrulaması, tooadd hello Azure Active Directory parametreleri gerekir:

* **Azure Active Directory Kimlik Doğrulaması (-G):** Kimlik doğrulaması için Azure Active Directory kullanın

Örneğin, bağlantı dizenizi hello şuna benzeyebilir:

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> Çok ihtiyacınız[Azure Active Directory kimlik doğrulamasını etkinleştir](sql-data-warehouse-authentication.md) Active Directory'yi kullanarak tooauthenticate.
> 
> 

## <a name="2-query"></a>2. Sorgu
Bağlantının ardından desteklenen herhangi Transact-SQL deyimleri hello örneğiyle verebilir.  Bu örnekte sorgular etkileşimli modda gönderilir.

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

Bu sonraki örnekler hello -Q seçeneğiyle ya da SQL toosqlcmd cmdlet'ine toplu iş modunda sorgularınızı nasıl çalıştırabileceğiniz gösterir.

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a>Sonraki adımlar
Bkz: [sqlcmd belgeleri] [ sqlcmd] sqlcmd içinde kullanılabilir hello seçenekleri ile ilgili ayrıntıları hakkında daha fazla bilgi için.

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
