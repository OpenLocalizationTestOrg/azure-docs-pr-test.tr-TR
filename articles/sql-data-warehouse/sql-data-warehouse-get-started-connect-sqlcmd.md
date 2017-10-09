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
# <a name="connect-toosql-data-warehouse-with-sqlcmd"></a><span data-ttu-id="d39a3-103">Sqlcmd ile tooSQL veri ambarına bağlanma</span><span class="sxs-lookup"><span data-stu-id="d39a3-103">Connect tooSQL Data Warehouse with sqlcmd</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d39a3-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="d39a3-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="d39a3-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d39a3-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="d39a3-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d39a3-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="d39a3-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="d39a3-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="d39a3-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="d39a3-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="d39a3-109">Kullanım [sqlcmd] [ sqlcmd] komut satırı yardımcı programını tooconnect tooand Azure SQL Data Warehouse sorgu.</span><span class="sxs-lookup"><span data-stu-id="d39a3-109">Use [sqlcmd][sqlcmd] command-line utility tooconnect tooand query an Azure SQL Data Warehouse.</span></span>  

## <a name="1-connect"></a><span data-ttu-id="d39a3-110">1. Bağlan</span><span class="sxs-lookup"><span data-stu-id="d39a3-110">1. Connect</span></span>
<span data-ttu-id="d39a3-111">tooget Başlarken [sqlcmd][sqlcmd], hello komut istemi açın ve girin **sqlcmd** hello bağlantı dizesi SQL Data Warehouse veritabanınız için izlediği.</span><span class="sxs-lookup"><span data-stu-id="d39a3-111">tooget started with [sqlcmd][sqlcmd], open hello command prompt and enter **sqlcmd** followed by hello connection string for your SQL Data Warehouse database.</span></span> <span data-ttu-id="d39a3-112">Merhaba bağlantı dizesi şu parametreler hello gerektirir:</span><span class="sxs-lookup"><span data-stu-id="d39a3-112">hello connection string requires hello following parameters:</span></span>

* <span data-ttu-id="d39a3-113">**Sunucu (-S):** sunucusuna hello biçiminde `<`sunucu adı`>`. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="d39a3-113">**Server (-S):** Server in hello form `<`Server Name`>`.database.windows.net</span></span>
* <span data-ttu-id="d39a3-114">**Database (-d):** Veritabanı adı.</span><span class="sxs-lookup"><span data-stu-id="d39a3-114">**Database (-d):** Database name.</span></span>
* <span data-ttu-id="d39a3-115">**Quoted Identifiers (-ı):** Quoted tanımlayıcıları etkin tooconnect tooa SQL Data Warehouse örneğine olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d39a3-115">**Enable Quoted Identifiers (-I):** Quoted identifiers must be enabled tooconnect tooa SQL Data Warehouse instance.</span></span>

<span data-ttu-id="d39a3-116">SQL Server kimlik doğrulaması toouse, tooadd hello kullanıcı adı/parola parametrelerini gerekir:</span><span class="sxs-lookup"><span data-stu-id="d39a3-116">toouse SQL Server Authentication, you need tooadd hello username/password parameters:</span></span>

* <span data-ttu-id="d39a3-117">**Kullanıcı (-U):** hello biçimindeki sunucu kullanıcısı `<`kullanıcı`>`</span><span class="sxs-lookup"><span data-stu-id="d39a3-117">**User (-U):** Server user in hello form `<`User`>`</span></span>
* <span data-ttu-id="d39a3-118">**Parola (-P):** hello kullanıcıyla ilişkili parola.</span><span class="sxs-lookup"><span data-stu-id="d39a3-118">**Password (-P):** Password associated with hello user.</span></span>

<span data-ttu-id="d39a3-119">Örneğin, bağlantı dizenizi hello şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="d39a3-119">For example, your connection string might look like hello following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

<span data-ttu-id="d39a3-120">toouse Azure Active Directory tümleşik kimlik doğrulaması, tooadd hello Azure Active Directory parametreleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="d39a3-120">toouse Azure Active Directory Integrated authentication, you need tooadd hello Azure Active Directory parameters:</span></span>

* <span data-ttu-id="d39a3-121">**Azure Active Directory Kimlik Doğrulaması (-G):** Kimlik doğrulaması için Azure Active Directory kullanın</span><span class="sxs-lookup"><span data-stu-id="d39a3-121">**Azure Active Directory Authentication (-G):** use Azure Active Directory for authentication</span></span>

<span data-ttu-id="d39a3-122">Örneğin, bağlantı dizenizi hello şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="d39a3-122">For example, your connection string might look like hello following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> <span data-ttu-id="d39a3-123">Çok ihtiyacınız[Azure Active Directory kimlik doğrulamasını etkinleştir](sql-data-warehouse-authentication.md) Active Directory'yi kullanarak tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="d39a3-123">You need too[enable Azure Active Directory Authentication](sql-data-warehouse-authentication.md) tooauthenticate using Active Directory.</span></span>
> 
> 

## <a name="2-query"></a><span data-ttu-id="d39a3-124">2. Sorgu</span><span class="sxs-lookup"><span data-stu-id="d39a3-124">2. Query</span></span>
<span data-ttu-id="d39a3-125">Bağlantının ardından desteklenen herhangi Transact-SQL deyimleri hello örneğiyle verebilir.</span><span class="sxs-lookup"><span data-stu-id="d39a3-125">After connection, you can issue any supported Transact-SQL statements against hello instance.</span></span>  <span data-ttu-id="d39a3-126">Bu örnekte sorgular etkileşimli modda gönderilir.</span><span class="sxs-lookup"><span data-stu-id="d39a3-126">In this example, queries are submitted in interactive mode.</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

<span data-ttu-id="d39a3-127">Bu sonraki örnekler hello -Q seçeneğiyle ya da SQL toosqlcmd cmdlet'ine toplu iş modunda sorgularınızı nasıl çalıştırabileceğiniz gösterir.</span><span class="sxs-lookup"><span data-stu-id="d39a3-127">These next examples show how you can run your queries in batch mode using hello -Q option or piping your SQL toosqlcmd.</span></span>

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a><span data-ttu-id="d39a3-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d39a3-128">Next steps</span></span>
<span data-ttu-id="d39a3-129">Bkz: [sqlcmd belgeleri] [ sqlcmd] sqlcmd içinde kullanılabilir hello seçenekleri ile ilgili ayrıntıları hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="d39a3-129">See [sqlcmd documentation][sqlcmd] for more about details about hello options available in sqlcmd.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
