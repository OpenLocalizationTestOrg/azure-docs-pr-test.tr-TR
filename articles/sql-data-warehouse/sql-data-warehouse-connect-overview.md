---
title: "Azure SQL Veri Ambarı'na Bağlanma | Microsoft Belgeleri"
description: "Azure SQL Veri Ambarı için sunucu adı ve bağlantı dizesini bulma"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: e52872ca-ae74-4e25-9c56-d49c85c8d0f0
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 72c2b404e66611da421eca0dc30aa71e18c6d120
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-azure-sql-data-warehouse"></a><span data-ttu-id="5c043-103">Azure SQL Data Warehouse’a bağlanma</span><span class="sxs-lookup"><span data-stu-id="5c043-103">Connect to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="5c043-104">Bu makale SQL Veri Ambarı’na ilk kez bağlanmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="5c043-104">This article helps you get connected to SQL Data Warehouse for the first time.</span></span>

## <a name="find-your-server-name"></a><span data-ttu-id="5c043-105">Sunucu adınızı bulma</span><span class="sxs-lookup"><span data-stu-id="5c043-105">Find your server name</span></span>
<span data-ttu-id="5c043-106">SQL Veri Ambarına bağlanmanın ilk adımı, sunucunuzun adını bulmayı bilmektir.</span><span class="sxs-lookup"><span data-stu-id="5c043-106">The first step to connecting to SQL Data Warehouse is knowing how to find your server name.</span></span>  <span data-ttu-id="5c043-107">Örneğin, aşağıdaki örnekte sunucu adı sample.database.windows.net şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="5c043-107">For example, the server name in the following example is sample.database.windows.net.</span></span> <span data-ttu-id="5c043-108">Tam sunucu adını bulmak için:</span><span class="sxs-lookup"><span data-stu-id="5c043-108">To find the fully qualified server name:</span></span>

1. <span data-ttu-id="5c043-109">[Azure Portalı][Azure portal]’na gidin.</span><span class="sxs-lookup"><span data-stu-id="5c043-109">Go to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="5c043-110">**SQL veritabanları**’na tıklayın</span><span class="sxs-lookup"><span data-stu-id="5c043-110">Click on **SQL databases**</span></span> 
3. <span data-ttu-id="5c043-111">Bağlanmak istediğiniz veritabanına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5c043-111">Click on the database you want to connect to.</span></span>
4. <span data-ttu-id="5c043-112">Tam sunucu adını bulun.</span><span class="sxs-lookup"><span data-stu-id="5c043-112">Locate the full server name.</span></span>
   
    ![Tam sunucu adı][1]

## <a name="supported-drivers-and-connection-strings"></a><span data-ttu-id="5c043-114">Desteklenen sürücüler ve bağlantı dizeleri</span><span class="sxs-lookup"><span data-stu-id="5c043-114">Supported drivers and connection strings</span></span>
<span data-ttu-id="5c043-115">Azure SQL Veri Ambarı; [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP] ve [JDBC][JDBC]’yi destekler.</span><span class="sxs-lookup"><span data-stu-id="5c043-115">Azure SQL Data Warehouse supports [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP], and [JDBC][JDBC].</span></span> <span data-ttu-id="5c043-116">En son sürümü ve belgeleri bulmak için yukarıdaki sürücülerden birine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5c043-116">Click on one of the preceding drivers to find the latest version and documentation.</span></span> <span data-ttu-id="5c043-117">Azure portalından kullandığınız sürücünün bağlantı dizesini otomatik olarak oluşturmak için önceki örnekte bulunan **Veritabanı bağlantı dizelerini göster**’e tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c043-117">To automatically generate the connection string for the driver that you are using from the Azure portal, you can click on the **Show database connection strings** from the preceding example.</span></span>  <span data-ttu-id="5c043-118">Aşağıda ayrıca her sürücü için bir bağlantı dizesinin nasıl göründüğü ile ilgili bazı örnekler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="5c043-118">Following are also some examples of what a connection string looks like for each driver.</span></span>

> [!NOTE]
> <span data-ttu-id="5c043-119">Bağlantınızın kısa süreli kesintiler sırasında devam etmesi için bağlantı zaman aşımını 300 saniyeye ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5c043-119">Consider setting the connection timeout to 300 seconds to allow your connection to survive short periods of unavailability.</span></span>
> 
> 

### <a name="adonet-connection-string-example"></a><span data-ttu-id="5c043-120">ADO.NET bağlantı dizesi örneği</span><span class="sxs-lookup"><span data-stu-id="5c043-120">ADO.NET connection string example</span></span>
```C#
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

### <a name="odbc-connection-string-example"></a><span data-ttu-id="5c043-121">ODBC bağlantı dizesi örneği</span><span class="sxs-lookup"><span data-stu-id="5c043-121">ODBC connection string example</span></span>
```C#
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

### <a name="php-connection-string-example"></a><span data-ttu-id="5c043-122">PHP bağlantı dizesi örneği</span><span class="sxs-lookup"><span data-stu-id="5c043-122">PHP connection string example</span></span>
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting to SQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

### <a name="jdbc-connection-string-example"></a><span data-ttu-id="5c043-123">JDBC bağlantı dizesi örneği</span><span class="sxs-lookup"><span data-stu-id="5c043-123">JDBC connection string example</span></span>
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

## <a name="connection-settings"></a><span data-ttu-id="5c043-124">Bağlantı ayarları</span><span class="sxs-lookup"><span data-stu-id="5c043-124">Connection settings</span></span>
<span data-ttu-id="5c043-125">SQL Veri Ambarı, bağlantı ve nesne oluşturma sırasında bazı ayarları standart hale getirir.</span><span class="sxs-lookup"><span data-stu-id="5c043-125">SQL Data Warehouse standardizes some settings during connection and object creation.</span></span> <span data-ttu-id="5c043-126">Bu ayarlar geçersiz kılınamaz ve şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="5c043-126">These settings cannot be overridden and include:</span></span>

| <span data-ttu-id="5c043-127">Veritabanı Ayarı</span><span class="sxs-lookup"><span data-stu-id="5c043-127">Database Setting</span></span> | <span data-ttu-id="5c043-128">Değer</span><span class="sxs-lookup"><span data-stu-id="5c043-128">Value</span></span> |
|:--- |:--- |
| <span data-ttu-id="5c043-129">[ANSI_NULLS][ANSI_NULLS]</span><span class="sxs-lookup"><span data-stu-id="5c043-129">[ANSI_NULLS][ANSI_NULLS]</span></span> |<span data-ttu-id="5c043-130">AÇIK</span><span class="sxs-lookup"><span data-stu-id="5c043-130">ON</span></span> |
| <span data-ttu-id="5c043-131">[QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS]</span><span class="sxs-lookup"><span data-stu-id="5c043-131">[QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS]</span></span> |<span data-ttu-id="5c043-132">AÇIK</span><span class="sxs-lookup"><span data-stu-id="5c043-132">ON</span></span> |
| <span data-ttu-id="5c043-133">[DATEFORMAT][DATEFORMAT]</span><span class="sxs-lookup"><span data-stu-id="5c043-133">[DATEFORMAT][DATEFORMAT]</span></span> |<span data-ttu-id="5c043-134">mdy</span><span class="sxs-lookup"><span data-stu-id="5c043-134">mdy</span></span> |
| <span data-ttu-id="5c043-135">[DATEFIRST][DATEFIRST]</span><span class="sxs-lookup"><span data-stu-id="5c043-135">[DATEFIRST][DATEFIRST]</span></span> |<span data-ttu-id="5c043-136">7</span><span class="sxs-lookup"><span data-stu-id="5c043-136">7</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5c043-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5c043-137">Next steps</span></span>
<span data-ttu-id="5c043-138">Visual Studio ile bağlantı kurmak ve sorgulamak için bkz. [Visual Studio ile Sorgulama][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="5c043-138">To connect and query with Visual Studio, see [Query with Visual Studio][Query with Visual Studio].</span></span> <span data-ttu-id="5c043-139">Kimlik doğrulama seçenekleri hakkında daha fazla bilgi için bkz. [Azure SQL Veri Ambarı’nda kimlik doğrulama][Authentication to Azure SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="5c043-139">To learn more about authentication options, see [Authentication to Azure SQL Data Warehouse][Authentication to Azure SQL Data Warehouse].</span></span>

<!--Articles-->
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[Authentication to Azure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[ADO.NET]: https://msdn.microsoft.com/library/e80y5yhx(v=vs.110).aspx
[ODBC]: https://msdn.microsoft.com/library/jj730314.aspx
[PHP]: https://msdn.microsoft.com/library/cc296172.aspx?f=255&MSPPError=-2147217396
[JDBC]: https://msdn.microsoft.com/library/mt484311(v=sql.110).aspx
[ANSI_NULLS]: https://msdn.microsoft.com/library/ms188048.aspx
[QUOTED_IDENTIFIERS]: https://msdn.microsoft.com/library/ms174393.aspx
[DATEFORMAT]: https://msdn.microsoft.com/library/ms189491.aspx
[DATEFIRST]: https://msdn.microsoft.com/library/ms181598.aspx

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->
[1]: media/sql-data-warehouse-connect-overview/get-server-name.png


