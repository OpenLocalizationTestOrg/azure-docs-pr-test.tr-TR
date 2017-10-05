---
title: "Azure SQL Veri Ambarı'na Bağlanma sqlcmd | Microsoft Belgeleri"
description: "Bir Azure SQL Veri Ambarı’na bağlanmak ve sorgu göndermek için [sqlcmd][sqlcmd] komut satırı yardımcı programını kullanın."
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
ms.openlocfilehash: 5a3fe1046c3417070ba8ff5bd18a0485e2152eff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-sqlcmd"></a><span data-ttu-id="978a3-103">sqlcmd ile SQL Data Warehouse'a bağlanma</span><span class="sxs-lookup"><span data-stu-id="978a3-103">Connect to SQL Data Warehouse with sqlcmd</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="978a3-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="978a3-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="978a3-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="978a3-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="978a3-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="978a3-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="978a3-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="978a3-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="978a3-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="978a3-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="978a3-109">Bir Azure SQL Veri Ambarı’na bağlanmak ve sorgu göndermek için [sqlcmd][sqlcmd] komut satırı yardımcı programını kullanın.</span><span class="sxs-lookup"><span data-stu-id="978a3-109">Use [sqlcmd][sqlcmd] command-line utility to connect to and query an Azure SQL Data Warehouse.</span></span>  

## <a name="1-connect"></a><span data-ttu-id="978a3-110">1. Bağlan</span><span class="sxs-lookup"><span data-stu-id="978a3-110">1. Connect</span></span>
<span data-ttu-id="978a3-111">**Sqlcmd** kullanmaya başlamadan önce komut istemini açın ve [sqlcmd][sqlcmd] öğesinden sonra SQL Veri Ambarı veritabanınızın bağlantı dizesini girin.</span><span class="sxs-lookup"><span data-stu-id="978a3-111">To get started with [sqlcmd][sqlcmd], open the command prompt and enter **sqlcmd** followed by the connection string for your SQL Data Warehouse database.</span></span> <span data-ttu-id="978a3-112">Bağlantı dizesi için aşağıdaki parametreler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="978a3-112">The connection string requires the following parameters:</span></span>

* <span data-ttu-id="978a3-113">**Server (-S):** `<`Sunucu Adı`>`.database.windows.net biçiminde belirtilmiş sunucu</span><span class="sxs-lookup"><span data-stu-id="978a3-113">**Server (-S):** Server in the form `<`Server Name`>`.database.windows.net</span></span>
* <span data-ttu-id="978a3-114">**Database (-d):** Veritabanı adı.</span><span class="sxs-lookup"><span data-stu-id="978a3-114">**Database (-d):** Database name.</span></span>
* <span data-ttu-id="978a3-115">**Tırnak İşaretli Tanımlayıcıları Etkinleştir (-I):** Bir SQL Veri Ambarı örneğine bağlanmak için tırnak işaretli tanımlayıcıların etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="978a3-115">**Enable Quoted Identifiers (-I):** Quoted identifiers must be enabled to connect to a SQL Data Warehouse instance.</span></span>

<span data-ttu-id="978a3-116">SQL Server Kimlik Doğrulamasını kullanmak için kullanıcı adı/parola parametrelerini eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="978a3-116">To use SQL Server Authentication, you need to add the username/password parameters:</span></span>

* <span data-ttu-id="978a3-117">**User (-U):** `<`Kullanıcı`>` biçimindeki sunucu kullanıcısı</span><span class="sxs-lookup"><span data-stu-id="978a3-117">**User (-U):** Server user in the form `<`User`>`</span></span>
* <span data-ttu-id="978a3-118">**Password (-P):** Kullanıcıyla ilişkili parola.</span><span class="sxs-lookup"><span data-stu-id="978a3-118">**Password (-P):** Password associated with the user.</span></span>

<span data-ttu-id="978a3-119">Örneğin, bağlantı dizeniz aşağıdaki gibi görünebilir:</span><span class="sxs-lookup"><span data-stu-id="978a3-119">For example, your connection string might look like the following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

<span data-ttu-id="978a3-120">Azure Active Directory Tümleşik kimlik doğrulamasını kullanmak için Azure Active Directory parametrelerini eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="978a3-120">To use Azure Active Directory Integrated authentication, you need to add the Azure Active Directory parameters:</span></span>

* <span data-ttu-id="978a3-121">**Azure Active Directory Kimlik Doğrulaması (-G):** Kimlik doğrulaması için Azure Active Directory kullanın</span><span class="sxs-lookup"><span data-stu-id="978a3-121">**Azure Active Directory Authentication (-G):** use Azure Active Directory for authentication</span></span>

<span data-ttu-id="978a3-122">Örneğin, bağlantı dizeniz aşağıdaki gibi görünebilir:</span><span class="sxs-lookup"><span data-stu-id="978a3-122">For example, your connection string might look like the following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> <span data-ttu-id="978a3-123">Active Directory kullanarak kimlik doğrulaması yapmak için [Azure Active Directory Kimlik Doğrulamasını etkinleştirmeniz](sql-data-warehouse-authentication.md) gerekir.</span><span class="sxs-lookup"><span data-stu-id="978a3-123">You need to [enable Azure Active Directory Authentication](sql-data-warehouse-authentication.md) to authenticate using Active Directory.</span></span>
> 
> 

## <a name="2-query"></a><span data-ttu-id="978a3-124">2. Sorgu</span><span class="sxs-lookup"><span data-stu-id="978a3-124">2. Query</span></span>
<span data-ttu-id="978a3-125">Bağlantının ardından desteklenen herhangi bir Transact-SQL deyimini örnekte yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="978a3-125">After connection, you can issue any supported Transact-SQL statements against the instance.</span></span>  <span data-ttu-id="978a3-126">Bu örnekte sorgular etkileşimli modda gönderilir.</span><span class="sxs-lookup"><span data-stu-id="978a3-126">In this example, queries are submitted in interactive mode.</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

<span data-ttu-id="978a3-127">Bu sonraki örnekler -Q seçeneği kullanarak veya SQL’i sqlcmd öğesine ekleyerek sorgularınızı toplu iş modunda nasıl çalıştırabileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="978a3-127">These next examples show how you can run your queries in batch mode using the -Q option or piping your SQL to sqlcmd.</span></span>

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a><span data-ttu-id="978a3-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="978a3-128">Next steps</span></span>
<span data-ttu-id="978a3-129">Sqlcmd’de kullanılabilen seçenekler hakkında daha fazla bilgi için bkz. [sqlcmd belgeleri][sqlcmd].</span><span class="sxs-lookup"><span data-stu-id="978a3-129">See [sqlcmd documentation][sqlcmd] for more about details about the options available in sqlcmd.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
