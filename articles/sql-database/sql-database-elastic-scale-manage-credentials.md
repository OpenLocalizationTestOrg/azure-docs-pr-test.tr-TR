---
title: "Merhaba esnek veritabanı istemci Kitaplığı'nda aaaManaging kimlik | Microsoft Docs"
description: "Nasıl tooset hello doğru düzeyde kimlik bilgileri, yönetici tooread esnek veritabanı uygulamaları için yalnızca,"
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
ms.openlocfilehash: 218783ca2a07e3c0a4b089aa92634f32c41386e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="credentials-used-tooaccess-hello-elastic-database-client-library"></a><span data-ttu-id="a9089-103">Kimlik bilgileri kullanılan tooaccess hello esnek veritabanı istemci kitaplığı</span><span class="sxs-lookup"><span data-stu-id="a9089-103">Credentials used tooaccess hello Elastic Database client library</span></span>
<span data-ttu-id="a9089-104">Merhaba [esnek veritabanı istemci Kitaplığı](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) kimlik bilgileri tooaccess hello üç farklı türde kullanan [parça eşleme Yöneticisi](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="a9089-104">hello [Elastic Database client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) uses three different kinds  of credentials tooaccess hello [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="a9089-105">Hello gerek bağlı olarak hello kimlik bilgisi hello düşük düzeyde erişim olası ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="a9089-105">Depending on hello need, use hello credential with  hello lowest level of access possible.</span></span>

* <span data-ttu-id="a9089-106">**Yönetim kimlik bilgilerini**: oluşturmak veya bir parça eşleme Yöneticisi düzenleme.</span><span class="sxs-lookup"><span data-stu-id="a9089-106">**Management credentials**: for creating or manipulating a shard map manager.</span></span> <span data-ttu-id="a9089-107">(Merhaba bkz [sözlüğü](sql-database-elastic-scale-glossary.md).)</span><span class="sxs-lookup"><span data-stu-id="a9089-107">(See hello [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
* <span data-ttu-id="a9089-108">**Erişim kimlik bilgilerini**: tooaccess var olan bir parça parça Yöneticisi tooobtain bilgilerini eşleyin.</span><span class="sxs-lookup"><span data-stu-id="a9089-108">**Access credentials**: tooaccess an existing shard map manager tooobtain information about shards.</span></span>
* <span data-ttu-id="a9089-109">**Bağlantı kimlik bilgilerini**: tooconnect tooshards.</span><span class="sxs-lookup"><span data-stu-id="a9089-109">**Connection credentials**: tooconnect tooshards.</span></span> 

<span data-ttu-id="a9089-110">Ayrıca bkz. [veritabanları ve Azure SQL veritabanında oturumları yönetme](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="a9089-110">See also [Managing databases and logins in Azure SQL Database](sql-database-manage-logins.md).</span></span> 

## <a name="about-management-credentials"></a><span data-ttu-id="a9089-111">Yönetim kimlik bilgileri ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="a9089-111">About management credentials</span></span>
<span data-ttu-id="a9089-112">Yönetim kimlik bilgileri olan kullanılan toocreate bir [ **ShardMapManager** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) nesne parça eşlemeleri işleyen uygulamalar için.</span><span class="sxs-lookup"><span data-stu-id="a9089-112">Management credentials are used toocreate a [**ShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) object for applications that manipulate shard maps.</span></span> <span data-ttu-id="a9089-113">(Örneğin, [esnek veritabanı araçlarını kullanarak bir parça ekleme](sql-database-elastic-scale-add-a-shard.md) ve [veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md)) hello kullanıcı hello esnek ölçek istemci kitaplığının hello SQL kullanıcılar ve SQL oturumu oluşturur ve her emin olur verilen hello genel parça hello okuma/yazma izinleri veritabanını ve tüm parça veritabanlarını da eşleyin.</span><span class="sxs-lookup"><span data-stu-id="a9089-113">(For example, see [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md)) hello user of hello elastic scale client library creates hello SQL users and SQL logins and makes sure each is granted hello read/write permissions on hello global shard map database and all shard databases as well.</span></span> <span data-ttu-id="a9089-114">Değişiklikleri toohello parça eşleme gerçekleştirilir, bu kimlik bilgileri kullanılan toomaintain hello genel parça eşleme ve hello yerel parça eşlemeleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="a9089-114">These credentials are used toomaintain hello global shard map and hello local shard maps when changes toohello shard map are performed.</span></span> <span data-ttu-id="a9089-115">Örneği için hello yönetim kimlik bilgileri toocreate hello parça eşleme Yöneticisi nesnesi kullanın (kullanarak [ **GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx):</span><span class="sxs-lookup"><span data-stu-id="a9089-115">For instance, use hello management credentials toocreate hello shard map manager object (using [**GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx):</span></span> 

    // Obtain a shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmAdminConnectionString, 
            ShardMapManagerLoadPolicy.Lazy 
    ); 

<span data-ttu-id="a9089-116">Merhaba değişkeni **smmAdminConnectionString** hello yönetim kimlik bilgilerini içeren bir bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="a9089-116">hello variable **smmAdminConnectionString** is a connection string that contains hello management credentials.</span></span> <span data-ttu-id="a9089-117">Merhaba kullanıcı kimliği ve parola okuma/yazma erişimi tooboth parça eşleme veritabanı ve tek tek parça sağlar.</span><span class="sxs-lookup"><span data-stu-id="a9089-117">hello user ID and password provides read/write access tooboth shard map database and individual shards.</span></span> <span data-ttu-id="a9089-118">Merhaba yönetim bağlantı dizesi hello sunucu adını ve veritabanını, ad tooidentify, hello genel parça, harita veritabanını da içerir.</span><span class="sxs-lookup"><span data-stu-id="a9089-118">hello management connection string also includes hello server name and database name tooidentify hello global shard map database.</span></span> <span data-ttu-id="a9089-119">Bu amaç için tipik bağlantı dizesi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="a9089-119">Here is a typical connection string for that purpose:</span></span>

     "Server=<yourserver>.database.windows.net;Database=<yourdatabase>;User ID=<yourmgmtusername>;Password=<yourmgmtpassword>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;” 

<span data-ttu-id="a9089-120">Değerleri hello biçiminde kullanmayın "username@server" — yalnızca hello "username" değerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a9089-120">Do not use values in hello form of "username@server"—instead just use hello "username" value.</span></span>  <span data-ttu-id="a9089-121">Bu durum, kimlik bilgileri hello parça eşleme manager veritabanı ve farklı sunucularda olabilir tek tek parça karşı çalışmanız gerekir çünkü.</span><span class="sxs-lookup"><span data-stu-id="a9089-121">This is because credentials must work against both hello shard map manager database and individual shards, which may be on different servers.</span></span>

## <a name="access-credentials"></a><span data-ttu-id="a9089-122">Erişim kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="a9089-122">Access credentials</span></span>
<span data-ttu-id="a9089-123">Bir parça parça eşlemeleri yönetme olmayan bir uygulamada harita Yöneticisi oluştururken, hello genel parça harita üzerinde salt okuma izinlerine sahip kimlik bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="a9089-123">When creating a shard map manager in an application that does not administer shard maps, use credentials that have read-only permissions on hello global shard map.</span></span> <span data-ttu-id="a9089-124">Merhaba bu kimlik bilgileri altında hello genel parça eşlemesinden alındı bilgileri için kullanılır [veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md) ve toopopulate hello parça hello istemci önbelleği eşleyin.</span><span class="sxs-lookup"><span data-stu-id="a9089-124">hello information retrieved from hello global shard map under these credentials are used for [data-dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and toopopulate hello shard map cache on hello client.</span></span> <span data-ttu-id="a9089-125">Merhaba aynı düzeni çok çağrı hello kimlik bilgileri sağlanır**GetSqlShardMapManager** yukarıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="a9089-125">hello credentials are provided through hello same call pattern too**GetSqlShardMapManager** as shown above:</span></span> 

    // Obtain shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmReadOnlyConnectionString, 
            ShardMapManagerLoadPolicy.Lazy
    );  

<span data-ttu-id="a9089-126">Not hello hello **smmReadOnlyConnectionString** adına bu erişim için farklı kimlik bilgileri tooreflect hello kullanımı **yönetici olmayan** kullanıcılar: Bu kimlik bilgileri yazma sağlamalıdır değil Merhaba genel parça eşleme izinleri.</span><span class="sxs-lookup"><span data-stu-id="a9089-126">Note hello use of hello **smmReadOnlyConnectionString** tooreflect hello use of different credentials for this access on behalf of **non-admin** users: these credentials should not provide write permissions on hello global shard map.</span></span> 

## <a name="connection-credentials"></a><span data-ttu-id="a9089-127">Bağlantı kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="a9089-127">Connection credentials</span></span>
<span data-ttu-id="a9089-128">Ek kimlik bilgileri gerekli hello kullanırken [ **OpenConnectionForKey** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) yöntemi tooaccess parçalama anahtar ile ilişkili bir parça.</span><span class="sxs-lookup"><span data-stu-id="a9089-128">Additional credentials are needed when using hello [**OpenConnectionForKey**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) method tooaccess a shard associated with a sharding key.</span></span> <span data-ttu-id="a9089-129">Bu kimlik bilgileri, salt okunur erişim toohello yerel parça eşleme tablolarının hello parça üzerinde bulunan tooprovide izinlerinizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9089-129">These credentials need tooprovide permissions for read-only access toohello local shard map tables residing on hello shard.</span></span> <span data-ttu-id="a9089-130">Veri bağımlı hello parça üzerinde yönlendirme için gerekli tooperform bağlantısı doğrulama budur.</span><span class="sxs-lookup"><span data-stu-id="a9089-130">This is needed tooperform connection validation for data-dependent routing on hello shard.</span></span> <span data-ttu-id="a9089-131">Bu kod parçacığını veri erişimini veri bağımlı yönlendirme hello bağlamında sağlar:</span><span class="sxs-lookup"><span data-stu-id="a9089-131">This code snippet allows data access in hello context of data dependent routing:</span></span> 

    using (SqlConnection conn = rangeMap.OpenConnectionForKey<int>( 
    targetWarehouse, smmUserConnectionString, ConnectionOptions.Validate)) 

<span data-ttu-id="a9089-132">Bu örnekte, **smmUserConnectionString** hello bağlantı dizesi hello için kullanıcı kimlik bilgilerini tutar.</span><span class="sxs-lookup"><span data-stu-id="a9089-132">In this example, **smmUserConnectionString** holds hello connection string for hello user credentials.</span></span> <span data-ttu-id="a9089-133">Azure SQL DB için kullanıcı kimlik bilgileri için tipik bağlantı dizesini şöyledir:</span><span class="sxs-lookup"><span data-stu-id="a9089-133">For Azure SQL DB, here is a typical connection string for user credentials:</span></span> 

    "User ID=<yourusername>; Password=<youruserpassword>; Trusted_Connection=False; Encrypt=True; Connection Timeout=30;”  

<span data-ttu-id="a9089-134">Merhaba yönetici kimlik'de olduğu gibi olmayan değerleri hello biçiminde "username@server".</span><span class="sxs-lookup"><span data-stu-id="a9089-134">As with hello admin credentials, do not values in hello form of "username@server".</span></span> <span data-ttu-id="a9089-135">Bunun yerine, yalnızca "username" kullanın.</span><span class="sxs-lookup"><span data-stu-id="a9089-135">Instead, just use "username".</span></span>  <span data-ttu-id="a9089-136">Ayrıca hello bağlantı dizesi bir sunucu adı ve veritabanı adı içermediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a9089-136">Also note that hello connection string does not contain a server name and database name.</span></span> <span data-ttu-id="a9089-137">Çünkü hello **OpenConnectionForKey** çağrı otomatik olarak hello bağlantı toohello parça dayalı hello anahtarı doğru doğrudan.</span><span class="sxs-lookup"><span data-stu-id="a9089-137">That is because hello **OpenConnectionForKey** call will automatically direct hello connection toohello correct shard based on hello key.</span></span> <span data-ttu-id="a9089-138">Bu nedenle, hello veritabanı adı ve sunucu adı sağlanmadı.</span><span class="sxs-lookup"><span data-stu-id="a9089-138">Hence, hello database name and server name are not provided.</span></span> 

## <a name="see-also"></a><span data-ttu-id="a9089-139">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="a9089-139">See also</span></span>
[<span data-ttu-id="a9089-140">Azure SQL Veritabanında veritabanlarını ve oturum açma bilgilerini yönetme</span><span class="sxs-lookup"><span data-stu-id="a9089-140">Managing databases and logins in Azure SQL Database</span></span>](sql-database-manage-logins.md)

[<span data-ttu-id="a9089-141">SQL Veritabanınızı güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="a9089-141">Securing your SQL Database</span></span>](sql-database-security-overview.md)

[<span data-ttu-id="a9089-142">Esnek veritabanı işlerine Başlarken</span><span class="sxs-lookup"><span data-stu-id="a9089-142">Getting started with Elastic Database jobs</span></span>](sql-database-elastic-jobs-getting-started.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

