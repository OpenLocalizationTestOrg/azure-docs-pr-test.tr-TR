---
title: "Esnek veritabanı istemci Kitaplığı'nda kimlik bilgilerini yönetme | Microsoft Docs"
description: "Doğru düzeyde kimlik bilgileri, yönetici salt okunur, esnek veritabanı uygulamaları için nasıl kurulur"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 72e0edaf-795e-4856-84a5-6594f735fb7e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 46908be2846062a0520d21e06db3091a4d711b0b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="credentials-used-to-access-the-elastic-database-client-library"></a><span data-ttu-id="7d0dd-103">Esnek veritabanı istemci kitaplığına erişmek için kullanılan kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="7d0dd-103">Credentials used to access the Elastic Database client library</span></span>
<span data-ttu-id="7d0dd-104">[Esnek veritabanı istemci Kitaplığı](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) erişmek için kullandığı kimlik bilgilerini üç farklı türde [parça eşleme Yöneticisi](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="7d0dd-104">The [Elastic Database client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) uses three different kinds  of credentials to access the [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="7d0dd-105">Gereken bağlı olarak, kimlik bilgisi erişim olası en düşük düzeyde ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-105">Depending on the need, use the credential with  the lowest level of access possible.</span></span>

* <span data-ttu-id="7d0dd-106">**Yönetim kimlik bilgilerini**: oluşturmak veya bir parça eşleme Yöneticisi düzenleme.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-106">**Management credentials**: for creating or manipulating a shard map manager.</span></span> <span data-ttu-id="7d0dd-107">(Bkz [sözlüğü](sql-database-elastic-scale-glossary.md).)</span><span class="sxs-lookup"><span data-stu-id="7d0dd-107">(See the [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
* <span data-ttu-id="7d0dd-108">**Erişim kimlik bilgilerini**: parça hakkında bilgi edinmek için mevcut bir parça eşleme Yöneticisi'ne erişmek için.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-108">**Access credentials**: to access an existing shard map manager to obtain information about shards.</span></span>
* <span data-ttu-id="7d0dd-109">**Bağlantı kimlik bilgilerini**: parça için bağlanmak için.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-109">**Connection credentials**: to connect to shards.</span></span> 

<span data-ttu-id="7d0dd-110">Ayrıca bkz. [veritabanları ve Azure SQL veritabanında oturumları yönetme](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="7d0dd-110">See also [Managing databases and logins in Azure SQL Database](sql-database-manage-logins.md).</span></span> 

## <a name="about-management-credentials"></a><span data-ttu-id="7d0dd-111">Yönetim kimlik bilgileri ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="7d0dd-111">About management credentials</span></span>
<span data-ttu-id="7d0dd-112">Yönetim kimlik bilgileri oluşturmak için kullanılan bir [ **ShardMapManager** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) nesne parça eşlemeleri işleyen uygulamalar için.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-112">Management credentials are used to create a [**ShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) object for applications that manipulate shard maps.</span></span> <span data-ttu-id="7d0dd-113">(Örneğin, [esnek veritabanı araçlarını kullanarak bir parça ekleme](sql-database-elastic-scale-add-a-shard.md) ve [veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md)) esnek ölçek istemci kitaplığı kullanıcı SQL oturum açma bilgileri ve SQL kullanıcılar oluşturur ve her verilir emin olur Genel parça okuma/yazma izinleri veritabanını ve tüm parça veritabanlarını da eşleyin.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-113">(For example, see [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md)) The user of the elastic scale client library creates the SQL users and SQL logins and makes sure each is granted the read/write permissions on the global shard map database and all shard databases as well.</span></span> <span data-ttu-id="7d0dd-114">Bu kimlik bilgileri, parça eşleme değişiklikleri gerçekleştirildiğinde genel parça eşleme ve yerel parça eşlemeleri korumak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-114">These credentials are used to maintain the global shard map and the local shard maps when changes to the shard map are performed.</span></span> <span data-ttu-id="7d0dd-115">Örneğin, parça eşleme Yöneticisi nesnesi oluşturmak için yönetim kimlik bilgilerini kullanın (kullanarak [ **GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx):</span><span class="sxs-lookup"><span data-stu-id="7d0dd-115">For instance, use the management credentials to create the shard map manager object (using [**GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx):</span></span> 

    // Obtain a shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmAdminConnectionString, 
            ShardMapManagerLoadPolicy.Lazy 
    ); 

<span data-ttu-id="7d0dd-116">Değişkeni **smmAdminConnectionString** yönetim kimlik bilgilerini içeren bir bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-116">The variable **smmAdminConnectionString** is a connection string that contains the management credentials.</span></span> <span data-ttu-id="7d0dd-117">Kullanıcı kimliği ve parola parça eşleme veritabanı ve tek tek parça okuma/yazma erişimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-117">The user ID and password provides read/write access to both shard map database and individual shards.</span></span> <span data-ttu-id="7d0dd-118">Yönetim bağlantı dizesini de sunucu adını ve genel parça eşleme veritabanını tanımlamak için veritabanı adını içerir.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-118">The management connection string also includes the server name and database name to identify the global shard map database.</span></span> <span data-ttu-id="7d0dd-119">Bu amaç için tipik bağlantı dizesi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="7d0dd-119">Here is a typical connection string for that purpose:</span></span>

     "Server=<yourserver>.database.windows.net;Database=<yourdatabase>;User ID=<yourmgmtusername>;Password=<yourmgmtpassword>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;” 

<span data-ttu-id="7d0dd-120">Değerler biçiminde kullanmayın "username@server" — yalnızca "username" değerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-120">Do not use values in the form of "username@server"—instead just use the "username" value.</span></span>  <span data-ttu-id="7d0dd-121">Bu durum, kimlik bilgileri parça eşleme manager veritabanı ve farklı sunucularda olabilir tek tek parça karşı çalışmanız gerekir çünkü.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-121">This is because credentials must work against both the shard map manager database and individual shards, which may be on different servers.</span></span>

## <a name="access-credentials"></a><span data-ttu-id="7d0dd-122">Erişim kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="7d0dd-122">Access credentials</span></span>
<span data-ttu-id="7d0dd-123">Bir parça parça eşlemeleri yönetme olmayan bir uygulamada harita Yöneticisi oluştururken, genel parça harita üzerinde salt okuma izinlerine sahip kimlik bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-123">When creating a shard map manager in an application that does not administer shard maps, use credentials that have read-only permissions on the global shard map.</span></span> <span data-ttu-id="7d0dd-124">Bu kimlik bilgileri altında genel parça eşlemesinden alındı bilgileri için kullanılan [veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md) ve istemci üzerindeki parça eşleme önbelleğini doldurmak için.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-124">The information retrieved from the global shard map under these credentials are used for [data-dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and to populate the shard map cache on the client.</span></span> <span data-ttu-id="7d0dd-125">Aynı çağrı düzeni aracılığıyla sağlanan kimlik bilgileri **GetSqlShardMapManager** yukarıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="7d0dd-125">The credentials are provided through the same call pattern to **GetSqlShardMapManager** as shown above:</span></span> 

    // Obtain shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmReadOnlyConnectionString, 
            ShardMapManagerLoadPolicy.Lazy
    );  

<span data-ttu-id="7d0dd-126">Kullanımına dikkat edin **smmReadOnlyConnectionString** adına bu erişimi için farklı kimlik bilgileri kullanımını yansıtacak şekilde **yönetici olmayan** kullanıcılar: Bu kimlik bilgileri yazma izinleri sağlamalıdır değil Genel parça eşleme.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-126">Note the use of the **smmReadOnlyConnectionString** to reflect the use of different credentials for this access on behalf of **non-admin** users: these credentials should not provide write permissions on the global shard map.</span></span> 

## <a name="connection-credentials"></a><span data-ttu-id="7d0dd-127">Bağlantı kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="7d0dd-127">Connection credentials</span></span>
<span data-ttu-id="7d0dd-128">Ek kimlik bilgileri kullanılırken gereklidir [ **OpenConnectionForKey** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) parçalama anahtar ile ilişkili bir parça erişim yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-128">Additional credentials are needed when using the [**OpenConnectionForKey**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) method to access a shard associated with a sharding key.</span></span> <span data-ttu-id="7d0dd-129">Bu kimlik bilgileri parça üzerinde bulunan yerel parça eşleme tablolarını salt okunur erişim izinlerini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-129">These credentials need to provide permissions for read-only access to the local shard map tables residing on the shard.</span></span> <span data-ttu-id="7d0dd-130">Bu, veri bağımlı üzerinde parça yönlendirme için bağlantı doğrulama gerçekleştirmek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-130">This is needed to perform connection validation for data-dependent routing on the shard.</span></span> <span data-ttu-id="7d0dd-131">Bu kod parçacığını veri erişimini veri bağımlı yönlendirme bağlamında sağlar:</span><span class="sxs-lookup"><span data-stu-id="7d0dd-131">This code snippet allows data access in the context of data dependent routing:</span></span> 

    using (SqlConnection conn = rangeMap.OpenConnectionForKey<int>( 
    targetWarehouse, smmUserConnectionString, ConnectionOptions.Validate)) 

<span data-ttu-id="7d0dd-132">Bu örnekte, **smmUserConnectionString** kullanıcı kimlik bilgileri için bağlantı dizesini içerir.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-132">In this example, **smmUserConnectionString** holds the connection string for the user credentials.</span></span> <span data-ttu-id="7d0dd-133">Azure SQL DB için kullanıcı kimlik bilgileri için tipik bağlantı dizesini şöyledir:</span><span class="sxs-lookup"><span data-stu-id="7d0dd-133">For Azure SQL DB, here is a typical connection string for user credentials:</span></span> 

    "User ID=<yourusername>; Password=<youruserpassword>; Trusted_Connection=False; Encrypt=True; Connection Timeout=30;”  

<span data-ttu-id="7d0dd-134">Yönetici kimlik olduğu gibi yok değerleri biçiminde "username@server".</span><span class="sxs-lookup"><span data-stu-id="7d0dd-134">As with the admin credentials, do not values in the form of "username@server".</span></span> <span data-ttu-id="7d0dd-135">Bunun yerine, yalnızca "username" kullanın.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-135">Instead, just use "username".</span></span>  <span data-ttu-id="7d0dd-136">Ayrıca, bağlantı dizesi bir sunucu adı ve veritabanı adı içermediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-136">Also note that the connection string does not contain a server name and database name.</span></span> <span data-ttu-id="7d0dd-137">Çünkü **OpenConnectionForKey** çağrı otomatik olarak anahtarına göre doğru parça bağlantısı doğrudan.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-137">That is because the **OpenConnectionForKey** call will automatically direct the connection to the correct shard based on the key.</span></span> <span data-ttu-id="7d0dd-138">Bu nedenle, sunucu adını ve veritabanı adı sağlanmadı.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-138">Hence, the database name and server name are not provided.</span></span> 

## <a name="see-also"></a><span data-ttu-id="7d0dd-139">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="7d0dd-139">See also</span></span>
[<span data-ttu-id="7d0dd-140">Azure SQL Veritabanında veritabanlarını ve oturum açma bilgilerini yönetme</span><span class="sxs-lookup"><span data-stu-id="7d0dd-140">Managing databases and logins in Azure SQL Database</span></span>](sql-database-manage-logins.md)

[<span data-ttu-id="7d0dd-141">SQL Veritabanınızı güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="7d0dd-141">Securing your SQL Database</span></span>](sql-database-security-overview.md)

[<span data-ttu-id="7d0dd-142">Esnek veritabanı işlerine Başlarken</span><span class="sxs-lookup"><span data-stu-id="7d0dd-142">Getting started with Elastic Database jobs</span></span>](sql-database-elastic-jobs-getting-started.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

